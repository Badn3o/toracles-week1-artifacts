# Plan de 30 días — TORACLES + mtgdeckbuilding.com

**Objetivo:** usar TORACLES como marca editorial/SEO principal y mtgdeckbuilding.com como dominio de producto/herramientas, coordinados pero no mezclados.

**Principio de reparto de roles**
- TORACLES = medio editorial, SEO, guías, autoridad de nicho, series, hubs y contenido evergreen.
- mtgdeckbuilding.com = capa de utilidad, datos y herramientas públicas de deckbuilding.
- Relación entre ambos = TORACLES capta y educa; mtgdeckbuilding convierte utilidad en recurrencia.

**Reglas del plan**
- No rebrandear TORACLES.
- No duplicar contenidos entre ambos dominios.
- Todo contenido de intención editorial vive en TORACLES.
- Toda utilidad interactiva o dataset navegable vive en mtgdeckbuilding.com.
- Cada entrega de semana debe dejar un activo verificable: URL, archivo, endpoint o página funcional.

---

## Arquitectura objetivo al día 30

**TORACLES debe tener:**
1. Bloque editorial principal estabilizado.
2. Hubs y guías principales con capa visual coherente.
3. Un primer pilar evergreen enlazando hacia el ecosistema.
4. CTAs claros hacia la futura herramienta.

**mtgdeckbuilding.com debe tener:**
1. Landing pública real con propuesta de valor.
2. App inicial online o preproducción verificable.
3. Primeras utilidades visibles: rankings, buscador, detalle de carta.
4. Conexión clara desde y hacia TORACLES.

---

## Semana 1 — Días 1 a 7
### Meta de la semana
Cerrar el reparto estratégico entre dominios y dejar lista la base de publicación y producto.

### TORACLES
1. Confirmar el inventario de páginas ya intervenidas y su estado real.
2. Cerrar la validación del bloque visual/captions/tooltips en la categoría Commander de la Semana y anotar el estado certificado.
3. Releer el plan original por días y marcar qué tareas siguen vigentes, cuáles ya se hicieron y cuáles cambiaron por la ola visual.
4. Definir una nueva regla editorial por intención:
   - Informacional/editorial -> TORACLES
   - Interactiva/comparativa/herramienta -> mtgdeckbuilding.com
5. Diseñar 3 CTAs estándar para usar más adelante en TORACLES:
   - “Explora precios y variaciones”
   - “Busca cartas para completar tu mazo”
   - “Consulta staples y movimientos por color/set”

### mtgdeckbuilding.com
1. Decidir el posicionamiento exacto del dominio:
   - “Herramientas de deckbuilding para Commander”
   - no “red social de mazos”, no “competidor de Moxfield”.
2. Definir el MVP público del producto a partir de MTGJSON:
   - rankings de subidas/bajadas
   - buscador de cartas
   - detalle de carta con histórico
3. Resolver la arquitectura de datos mínima para producción:
   - mover o clonar la base fuera de `/mnt/e` si sigue en WSL/NTFS
   - definir ruta Linux estable para SQLite o alternativa de motor
4. Decidir despliegue inicial:
   - local endurecido
   - VPS
   - o subdominio temporal de pruebas
5. Crear landing mínima con:
   - propuesta de valor
   - 3 bloques de utilidad
   - CTA a lista de espera o acceso temprano

### Entregables de fin de semana 1
- Documento de reparto editorial/producto.
- Landing draft o publicada para mtgdeckbuilding.com.
- Decisión cerrada de infraestructura de base de datos.
- Lista de CTAs que TORACLES usará para enviar tráfico.

---

## Semana 2 — Días 8 a 14
### Meta de la semana
Publicar la primera capa visible de mtgdeckbuilding.com y seguir fortaleciendo TORACLES como motor de adquisición.

### TORACLES
1. Ejecutar las tareas vivas del bloque editorial pendiente del plan original:
   - páginas de comandante individual prioritarias
   - Academia del Oráculo piloto
2. Crear el primer pilar evergreen:
   - `Cómo jugar a Commander desde cero`
3. Añadir enlaces editoriales internos desde hubs y guías hacia ese pilar.
4. Preparar 2 piezas con intención puente hacia el producto:
   - “Cómo construir mejor tu base de maná en Commander”
   - “Qué cartas de Commander están subiendo y por qué”
5. Insertar CTAs suaves hacia mtgdeckbuilding.com en posts donde encaje.

### mtgdeckbuilding.com
1. Publicar el frontend inicial conectado a la API:
   - rankings
   - buscador
   - ficha de carta
2. Endurecer la API mínima:
   - `/api/status`
   - `/api/cards`
   - `/api/rankings`
   - `/api/cards/{uuid}`
   - `/api/suggest`
3. Corregir acoplamientos local-first del frontend.
4. Definir branding mínimo compatible con TORACLES:
   - visual sobrio
   - sin intentar parecer otro medio editorial
5. Añadir una sección “próximamente” con las siguientes utilidades:
   - completa tu mazo
   - filtros por color/legality/set
   - staples por arquetipo

### Entregables de fin de semana 2
- MVP navegable de mtgdeckbuilding.com.
- 1 pilar evergreen nuevo en TORACLES.
- 2-3 artículos/hubs de TORACLES ya conectados con CTA al producto.

---

## Semana 3 — Días 15 a 21
### Meta de la semana
Hacer que ambos dominios se refuercen mutuamente y no compitan entre sí.

### TORACLES
1. Revisar contenido legacy con más potencial de puente comercial y de tráfico.
2. Crear una plantilla de bloque editorial “datos del mercado” para futuros artículos:
   - top subidas 7d
   - top bajadas 30d
   - staples que recuperan precio
3. Priorizar contenidos donde los datos aporten valor real:
   - staples por color
   - tierras
   - precons que mejorar
   - commanders con piezas clave caras
4. Preparar una página o hub “Herramientas” dentro de TORACLES que apunte al dominio nuevo.

### mtgdeckbuilding.com
1. Añadir la primera utilidad con verdadero sabor de producto:
   - `Completa tu mazo` en fase alfa o especificación cerrada + landing de espera.
2. Optimizar rendimiento y queries más costosas:
   - sugerencias
   - detalle de carta
   - rankings por periodos
3. Definir páginas SEO propias que NO canibalicen TORACLES:
   - rankings por set
   - rankings por color
   - cartas por legalidad
   - páginas utilitarias, no ensayos
4. Crear esquema de medición:
   - visitas
   - búsquedas
   - clics a detalle
   - CTA desde TORACLES

### Entregables de fin de semana 3
- Hub “Herramientas” o equivalente en TORACLES.
- Primer bloque editorial reutilizable basado en datos.
- Primera utilidad diferencial o al menos alfa cerrada en mtgdeckbuilding.com.

---

## Semana 4 — Días 22 a 30
### Meta de la semana
Cerrar el primer ciclo operativo con medición, reparto claro de funciones y roadmap de siguiente fase.

### TORACLES
1. Hacer la primera medición post-intervención sobre el plan original donde ya toque.
2. Evaluar qué tipos de contenidos envían mejor tráfico al producto.
3. Ajustar los CTAs editoriales según resultados.
4. Dejar cerrada una lista de próximas piezas evergreen que alimenten al producto.

### mtgdeckbuilding.com
1. Pasar de MVP a beta pública controlada.
2. Añadir páginas de utilidad visibles desde Google y desde TORACLES:
   - Top gainers 7d
   - Top losers 30d
   - Search cards
   - Card detail
3. Definir la siguiente fase técnica:
   - si seguir con SQLite endurecido
   - si migrar a Postgres
   - si separar ETL/API/frontend
4. Dejar lista la integración editorial:
   - snippets o widgets embebibles
   - enlaces profundos desde artículos de TORACLES

### Entregables del día 30
- TORACLES estabilizado como marca editorial con capa evergreen en marcha.
- mtgdeckbuilding.com operativo como herramienta o beta pública.
- Mapa de enlaces entre ambos dominios.
- Cuadro de métricas iniciales.
- Backlog priorizado para días 31-90.

---

## Qué vive en cada dominio

### TORACLES
- Rankings editoriales
- Guías de commander
- Staples por color
- Combos explicados
- Precons
- Academia del Oráculo
- Opinión, criterio, contexto y tono de marca

### mtgdeckbuilding.com
- Buscador de cartas
- Variaciones de precio
- Rankings de mercado
- Herramienta “completa tu mazo”
- Comparadores utilitarios
- Filtros, datos y exploración interactiva

---

## Riesgos a vigilar

1. Canibalización SEO
- evitar páginas gemelas entre dominios
- una intención, un dominio principal

2. Sobrecarga operativa
- no abrir 20 features nuevas en mtgdeckbuilding.com antes de estabilizar 3

3. Mezcla de marca
- TORACLES no debe perder su voz editorial por parecer una herramienta
- mtgdeckbuilding.com no debe imitar el tono editorial de TORACLES

4. Base de datos
- la situación actual de SQLite sobre `/mnt/e` en WSL es una alerta técnica

---

## Prioridades P0 / P1 / P2

### P0
- Cerrar reparto estratégico de dominios
- Publicar landing/MVP de mtgdeckbuilding.com
- Estabilizar base de datos e infraestructura mínima
- Mantener TORACLES como dominio editorial principal

### P1
- Crear el pilar evergreen de Academia del Oráculo
- Integrar CTAs TORACLES -> mtgdeckbuilding.com
- Añadir la primera utilidad diferencial de producto

### P2
- Widgets embebibles
- Páginas SEO utilitarias por set/color/legalidad
- Roadmap de monetización y crecimiento

---

## Resultado esperado al día 30

- TORACLES gana claridad: medio editorial sólido, más evergreen y con mejor estructura interna.
- mtgdeckbuilding.com deja de ser un redirect genérico y pasa a ser un activo con propósito.
- Ambos dominios dejan de competir por identidad y empiezan a funcionar como sistema:
  - TORACLES atrae, explica y posiciona
  - mtgdeckbuilding.com retiene, ayuda y prepara producto
