# Día 2 — Auditoría técnica de MTGJSON

Estado:
Documento de auditoría técnica implementado sobre lectura real del prototipo en `/mnt/e/AIProyects/MTGJSON` y sobre evidencia previa ya medida para la base SQLite.

Fecha:
2026-09-02

---

## Resumen ejecutivo

Veredicto corto:
- El activo MTGJSON sí contiene piezas reutilizables para una beta estrecha de `mtgdeckbuilding.com`.
- No está listo para exposición pública tal como está.
- El bloqueo principal no es de idea de producto, sino de operación de datos y superficie pública.

Lo reutilizable de verdad:
- esquema de datos ya definido
- lógica ETL base
- rankings calculados
- endpoints P0 ya presentes
- frontend estático con 3 superficies claras

Lo que impide publicar tal cual:
- base SQLite operando en `/mnt/e` con historial real de `disk I/O error`
- conexión normal no estable; acceso seguro observado solo en readonly/immutable
- CORS abierto a `*`
- `POST /api/sync` expuesto sin auth ni cierre operativo
- búsquedas fuzzy y detalle de carta con coste potencial alto sobre dataset grande
- mezcla de superficie pública y superficie operativa en la misma app

Conclusión técnica del Día 2:
- MTGJSON sirve como base de prototipo y fuente de reutilización.
- No sirve todavía como stack público de beta si se mantiene exactamente en su forma y ubicación actuales.

---

## Inventario técnico en 4 bloques

### 1. ETL

Archivos observados:
- `etl.py`
- `sync_service.py`
- `scheduler.py`
- `config.py`
- `database.py`

Capacidades detectadas:
- descarga `Meta.json` desde MTGJSON para decidir si hay actualización
- descarga `AllPrintings.sqlite.zip`
- descarga `AllPricesToday.json.gz` y `AllPrices.json.gz`
- inicializa esquema local SQLite
- sincroniza sets, cards y legalities
- sincroniza histórico de precios en `prices_raw`
- calcula rankings materializados mediante `analytics.py`
- permite sync manual en background vía API
- incluye scheduler de comprobación cada 6 horas

Observaciones reales de implementación:
- `check_meta()` compara `last_card_date` y `last_price_date` contra MTGJSON Meta.
- `sync_cards()` importa desde SQLite de MTGJSON a la base local del proyecto.
- `sync_prices()` inserta precios en batches y decide entre seed amplio o update diario.
- `run_background_sync()` ejecuta ETL + recálculo de rankings.
- `start_scheduler()` deja un daemon simple con `sleep` de 6 horas.

Riesgos del bloque ETL:
- mismo almacén SQLite soporta ingestión, lectura API y analytics.
- la app pública contiene endpoint para disparar sync.
- no hay separación clara entre plano operativo interno y plano público.
- el scheduler es simple; no hay cola, locking persistente ni aislamiento de carga.

Juicio:
- reutilizable para operación interna y para un MVP estrecho.
- no publicable tal cual como backend abierto.

### 2. Datos

Archivo principal observado:
- `data/mtg_analytics.db`

Esquema observado en `database.py`:
- `meta`
- `sets`
- `cards`
- `card_legalities`
- `prices_raw`
- `price_rankings`

Índices declarados:
- nombre, set, rarity, mana_value, colors, color_identity, type_line
- legalities por formato/status
- `prices_raw` por lookup y fecha
- `price_rankings` por ventanas 1d/7d/30d/365d

Evidencia heredada ya medida para esta auditoría:
- riesgo real con SQLite en `/mnt/e` bajo WSL/NTFS
- acceso normal ya devolvió `disk I/O error`
- acceso estable solo observado en readonly/immutable
- base actual: `/mnt/e/AIProyects/MTGJSON/data/mtg_analytics.db`
- tamaño aproximado observado previamente: ~19G
- conteos observados previamente en readonly:
  - `sets`: 869
  - `cards`: 113748
  - `card_legalities`: 1327359
  - `prices_raw`: 63850028
  - `price_rankings`: 581838
- meta observada previamente:
  - `last_card_date = 2026-09-01`
  - `last_price_date = 2026-09-01`

Lectura técnica del modelo de datos:
- el esquema sí cubre el MVP de lookup, filtros, legalidad y rankings
- `prices_raw` es demasiado grande para tratarlo como superficie pública ingenua
- `price_rankings` ya actúa como capa materializada útil para producto
- `cards` + `sets` + `card_legalities` bastan para gran parte de la beta

Riesgos del bloque datos:
- `/mnt/e` no es base operativa pública fiable para este uso
- WAL y SQLite sobre NTFS/WSL siguen siendo una fuente real de fragilidad
- el prototipo intenta usar `PRAGMA journal_mode=WAL;` en la conexión normal
- el acceso detail puede arrastrar mucho histórico desde `prices_raw`

Juicio:
- los datos son valiosos
- la ubicación y el modo operativo actual no lo son

### 3. API

Archivo observado:
- `server.py`

Endpoints detectados por lectura real:
- `GET /`
- `GET /api/status`
- `GET /api/sets`
- `GET /api/suggest`
- `GET /api/cards`
- `GET /api/rankings`
- `GET /api/cards/{uuid}`
- `POST /api/sync`

Qué hace cada endpoint:
- `/api/status`: devuelve estado general, fechas meta, conteos y `sync_state`
- `/api/sets`: lista sets ordenados por fecha
- `/api/suggest`: sugerencias fuzzy de nombres
- `/api/cards`: búsqueda filtrable con joins a sets y `price_rankings`
- `/api/rankings`: top gainers/losers para 1d/7d/30d/365d
- `/api/cards/{uuid}`: detalle completo con legalities, price history y métricas
- `/api/sync`: dispara ETL y analytics en background

Hallazgos de superficie pública:
- CORS configurado con `allow_origins=["*"]`, `allow_methods=["*"]`, `allow_headers=["*"]`
- no hay auth
- no hay rate limit
- no hay separación entre endpoint público y endpoint operativo
- no hay versionado API

Riesgos reales por endpoint:
- `/api/sync` no debe quedar público en beta abierta
- `/api/cards/{uuid}` puede devolver payload pesado por `price_history` completo desde `prices_raw`
- `/api/suggest` llama a `get_fuzzy_matching_names()`
- `get_fuzzy_matching_names()` hace `SELECT DISTINCT name FROM cards` y luego fuzzy en Python sobre todos los nombres observados en la tabla
- `/api/cards` resuelve nombre mediante fuzzy previo y luego filtra con joins; es funcional, pero no está claro como endpoint de tráfico real sin medición adicional

Juicio:
- existe una API útil
- la API actual es de prototipo local, no de publicación directa

### 4. Frontend

Archivos observados:
- `index.html`
- `static/js/app.js`
- `static/js/api.js`
- `static/js/autocomplete.js`
- `static/css/styles.css`

Superficies frontend detectadas por lectura real:
1. pestaña `Top Subidas / Bajadas`
2. pestaña `Buscador de Cartas`
3. pestaña `Estado ETL`
4. modal de detalle de carta con gráfico de precios

Comportamiento detectado:
- carga inicial de sets, rankings y status en `DOMContentLoaded`
- filtros de ranking por periodo, provider, finish y precio mínimo
- buscador con autocompletado y búsqueda fuzzy
- grid de cartas con precio actual y delta 7d
- modal de detalle con imagen, oracle text e histórico de precios en Chart.js
- frontend decide URL API con `getApiUrl()` y cae a `http://localhost:8008` en varios casos

Hallazgos UX/técnicos:
- hay un frontend ya navegable para demo local
- mezcla una pestaña operativa interna (`Estado ETL`) con la experiencia pública
- el lookup está orientado a prototipo local, no a experiencia pública recortada
- el detalle de carta depende de traer historial completo
- el JS asume backend disponible en `localhost:8008` en varios contextos

Juicio:
- hay scaffold reutilizable
- no todo debe viajar al MVP público

---

## Endpoints detectados

Detectados por lectura real de `server.py`:
- `GET /`
- `GET /api/status`
- `GET /api/sets`
- `GET /api/suggest`
- `GET /api/cards`
- `GET /api/rankings`
- `GET /api/cards/{uuid}`
- `POST /api/sync`

Endpoints P0 con valor directo para el MVP:
- `/api/status`
- `/api/sets`
- `/api/cards`
- `/api/rankings`
- `/api/cards/{uuid}`
- `/api/suggest`

Endpoint no publicable todavía:
- `POST /api/sync`

---

## Superficies frontend detectadas

Detectadas por lectura real de `index.html` y JS:
- Rankings de subidas/bajadas
- Buscador de cartas
- Estado ETL / sincronización manual
- Modal de detalle de carta con gráfico

Superficies con mejor encaje para beta estrecha:
- rankings
- buscador
- detalle de carta

Superficie que no debe ir al MVP público:
- estado ETL / botón de sincronización manual

---

## Riesgos reales

1. Riesgo estructural de almacenamiento
- la base en `/mnt/e` ya mostró `disk I/O error`
- la estabilidad observada fue solo en readonly/immutable
- seguir ahí como base pública contradice el Gate 1

2. Riesgo de mezcla entre operación y producto
- la misma app expone estado, lectura pública y disparo de sync
- no hay frontera entre admin interno y frontend público

3. Riesgo de apertura excesiva
- CORS abierto a todo origen
- sin auth ni rate limits
- sin cierre básico de abuso

4. Riesgo de payload y coste
- detalle de carta trae histórico completo desde `prices_raw`
- suggest hace carga amplia de nombres únicos y fuzzy en Python
- eso puede degradarse con tráfico real

5. Riesgo de dependencia del dataset completo
- el prototipo está pensado sobre base muy grande
- la beta no necesita toda la complejidad del dataset bruto público

6. Riesgo de promesa de producto desalineada
- la pestaña ETL y el sync manual empujan el activo hacia herramienta interna de operación, no hacia MVP público de utilidad para Commander

---

## Piezas reutilizables para MVP

Reutilizables ahora mismo, con recorte y cierre:
- esquema SQLite actual como base conceptual
- tabla `cards`
- tabla `sets`
- tabla `card_legalities`
- tabla `price_rankings`
- lógica de cálculo de rankings en `analytics.py`
- endpoint `/api/status` para health y frescura de datos
- endpoint `/api/sets`
- endpoint `/api/cards`
- endpoint `/api/rankings`
- endpoint `/api/cards/{uuid}` con posible poda posterior de payload
- endpoint `/api/suggest` si se acepta que necesita rediseño o cache más adelante
- scaffold estático del frontend
- pestaña de rankings
- pestaña de búsqueda
- modal de detalle

Reutilización razonable para semana 2:
- lookup de cartas
- rankings por periodo/proveedor/acabado
- consulta de legalidad
- ficha básica de carta

---

## Piezas no publicables todavía

No publicables tal como están hoy:
- base operativa en `/mnt/e`
- `POST /api/sync` en superficie pública
- pestaña `Estado ETL`
- botón `Sincronizar Ahora`
- CORS abierto a `*`
- operación normal con WAL sobre esta ubicación
- detalle de carta devolviendo histórico completo sin validar coste
- búsqueda fuzzy basada en `SELECT DISTINCT name FROM cards` + procesamiento Python para tráfico público no medido
- scheduler/daemon como si ya fuera pipeline de producción

---

## Veredicto técnico del Día 2

Sí existe una base técnica aprovechable.

No existe todavía una base operativa pública segura si se mantiene:
- la DB en `/mnt/e`
- la app con CORS abierto
- `POST /api/sync` expuesto
- la mezcla entre ETL interno y frontend público

Por tanto:
- la viabilidad mínima del producto es real
- la publicación pública de beta solo es defendible si la decisión de almacenamiento cambia y la superficie pública se recorta

Este documento se considera suficiente para pasar al ADR/decisión de almacenamiento del Día 2.