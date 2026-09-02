# Plan operativo de 30 días — TORACLES + mtgdeckbuilding.com

> Para Hermes: este plan está pensado para ejecución progresiva, con validación al cierre de cada día y sin mezclar roles entre dominios.

Objetivo:
En 30 días, dejar TORACLES consolidado como marca editorial/SEO y mtgdeckbuilding.com activado como dominio de producto/herramientas, con reparto claro de funciones, primeros activos públicos y conexión operativa entre ambos dominios.

Arquitectura:
TORACLES será el dominio de adquisición, autoridad y contenido evergreen. mtgdeckbuilding.com será el dominio de utilidad interactiva, datos y herramientas. Ambos deben reforzarse mutuamente mediante enlazado, CTAs y bloques de contenido complementario, sin canibalización SEO.

Tech stack / activos implicados:
- TORACLES WordPress
- MTGJSON local app/API en `/mnt/e/AIProyects/MTGJSON`
- Dominio `mtgdeckbuilding.com`
- Search Console / métricas SEO
- SQLite actual (con riesgo conocido por ubicación WSL/NTFS)

---

## Reglas de operación

1. No rebrandear TORACLES.
2. No duplicar contenidos entre dominios.
3. Una intención principal por dominio:
   - editorial / informacional -> TORACLES
   - utilitaria / interactiva / datos -> mtgdeckbuilding.com
4. Cada día debe cerrar con un artefacto verificable:
   - archivo
   - URL
   - endpoint
   - validación
   - informe
5. Si una tarea técnica bloquea el día, dejar constancia y avanzar con la siguiente no bloqueada.
6. Prioridades:
   - P0 = imprescindible para que el plan tenga sentido
   - P1 = muy recomendable en este ciclo de 30 días
   - P2 = mejora valiosa pero no bloqueante

---

## Reparto funcional entre dominios

### TORACLES
Vive aquí:
- guías de Commander
- staples por color
- combos explicados
- precons
- hubs editoriales
- Academia del Oráculo
- análisis, criterio y tono de marca

### mtgdeckbuilding.com
Vive aquí:
- buscador de cartas
- rankings de subidas/bajadas
- histórico de precios
- detalle de carta
- utilidades de deckbuilding
- filtros, exploración y dataset público

---

## Prioridades globales

### P0
- estabilizar el reparto de roles entre dominios
- sacar a mtgdeckbuilding.com del estado de redirect vacío
- resolver la base de datos / arquitectura mínima para servir el producto
- mantener TORACLES como marca editorial principal
- definir enlazado y CTAs entre ambos

### P1
- lanzar un pilar evergreen fuerte en TORACLES
- conectar TORACLES con el producto mediante bloques y CTAs
- endurecer la API y UX inicial de mtgdeckbuilding.com
- crear una primera utilidad diferencial de producto

### P2
- widgets embebibles
- páginas SEO utilitarias por set/color/legalidad
- roadmap de monetización y expansión

---

## Semana 1 — Dirección, reparto y base técnica

### Día 1 — Congelar estrategia y mapa de dominios
Prioridad: P0

Objetivo:
Cerrar por escrito qué vive en cada dominio y qué no.

Tareas TORACLES:
- Listar los tipos de contenido actuales de TORACLES.
- Marcar qué piezas seguirán siendo exclusivamente editoriales.
- Detectar qué piezas podrían apuntar al producto sin canibalizar.

Tareas mtgdeckbuilding.com:
- Definir la promesa exacta del dominio.
- Elegir posicionamiento: “herramientas de deckbuilding para Commander”.
- Prohibir deriva hacia “red social de mazos” o “clon de Moxfield”.

Entregable del día:
- documento de reparto editorial/producto
- tabla “esto vive aquí / esto no vive aquí”

Criterio de cierre:
- existe una decisión explícita de roles por dominio

---

### Día 2 — Auditoría del activo técnico MTGJSON
Prioridad: P0

Objetivo:
Determinar si la base técnica actual puede ponerse en producción mínima o requiere cirugía previa.

Tareas:
- Revisar backend, ETL, analytics, frontend y DB.
- Confirmar conteos de tablas, estado de meta y endpoints.
- Documentar el riesgo actual de SQLite en `/mnt/e`.
- Decidir si el stack de salida será:
  - SQLite en filesystem Linux
  - Postgres
  - dual setup dev/prod

Entregable del día:
- informe técnico de estado de MTGJSON
- decisión de almacenamiento para la beta

Criterio de cierre:
- hay una decisión cerrada sobre dónde y cómo se servirá la base

---

### Día 3 — Arquitectura mínima de despliegue
Prioridad: P0

Objetivo:
Cerrar el camino más corto para publicar mtgdeckbuilding.com sin rehacer media plataforma.

Tareas:
- Definir dónde vive la API.
- Definir dónde vive el frontend.
- Elegir si el despliegue será monolítico o separado.
- Decidir puerto, dominio, reverse proxy y estrategia de logs.
- Dejar esquema de variables/config necesario.

Entregable del día:
- mini documento de despliegue
- checklist de prerequisitos para publicar

Criterio de cierre:
- se sabe exactamente qué hay que levantar para servir el MVP

---

### Día 4 — Landing de mtgdeckbuilding.com
Prioridad: P0

Objetivo:
Sacar el dominio del limbo y convertirlo en un activo con intención.

Tareas:
- Diseñar la landing inicial.
- Redactar propuesta de valor.
- Añadir bloques:
  - qué problema resuelve
  - qué incluye hoy
  - qué llegará pronto
  - enlace a TORACLES
- Definir CTA principal.

Entregable del día:
- landing publicada o HTML listo para publicar

Criterio de cierre:
- el dominio deja de ser solo un redirect ciego

---

### Día 5 — CTAs y puente editorial desde TORACLES
Prioridad: P0

Objetivo:
Preparar el tráfico editorial para derivarlo con sentido al producto.

Tareas:
- Escribir 3 CTAs estándar para TORACLES.
- Decidir en qué páginas van primero.
- Crear plantilla de bloque “herramienta relacionada”.
- Anotar reglas de uso para no forzar el enlace donde no aporte valor.

Entregable del día:
- biblioteca de CTAs y bloque editorial reutilizable

Criterio de cierre:
- existe un patrón claro de enlace TORACLES -> mtgdeckbuilding.com

---

### Día 6 — Revisión del plan TORACLES heredado
Prioridad: P1

Objetivo:
Mapear el plan histórico por días con la nueva realidad de dos dominios.

Tareas:
- Marcar qué tareas del plan original están cerradas.
- Marcar cuáles siguen vigentes.
- Marcar cuáles pasan a depender del dominio nuevo.
- Reordenar el backlog para que no haya contradicción entre SEO y producto.

Entregable del día:
- tabla de estado del plan original

Criterio de cierre:
- ya no hay ambigüedad entre el plan viejo y el nuevo

---

### Día 7 — Cierre semanal y validación
Prioridad: P0

Objetivo:
Cerrar semana 1 con decisiones, no solo ideas.

Tareas:
- Revisar que haya 4 artefactos:
  - reparto de dominios
  - decisión de base de datos
  - arquitectura mínima
  - landing/CTA
- Registrar bloqueos.
- Confirmar prioridades de la semana 2.

Entregable del día:
- informe de cierre de semana 1

Criterio de cierre:
- puedes explicar en una frase qué hace cada dominio

---

## Semana 2 — Publicación del MVP y refuerzo editorial

### Día 8 — TORACLES: pilar evergreen
Prioridad: P1

Objetivo:
Iniciar la capa evergreen que alimentará ambos dominios.

Tareas:
- Crear o rehacer “Cómo jugar a Commander desde cero”.
- Añadir estructura viva: fecha de actualización, bloques de contexto, enlaces a guías base.
- Preparar hueco para CTA al producto futuro.

Entregable del día:
- borrador o publicación del primer pilar evergreen

---

### Día 9 — MTGJSON: API mínima servible
Prioridad: P0

Objetivo:
Dejar operativos los endpoints que el frontend necesita de verdad.

Tareas:
- Validar `/api/status`
- Validar `/api/sets`
- Validar `/api/cards`
- Validar `/api/rankings`
- Validar `/api/cards/{uuid}`
- Validar `/api/suggest`
- corregir fallos obvios de configuración si aparecen

Entregable del día:
- batería de endpoints comprobados

---

### Día 10 — Frontend MVP: rankings
Prioridad: P0

Objetivo:
Publicar una primera utilidad visible y entendible.

Tareas:
- Hacer funcionar la pestaña de rankings en entorno real.
- Revisar filtros de periodo/proveedor/finish.
- Corregir errores de fetch o de URL base.
- Verificar carga vacía, error y éxito.

Entregable del día:
- rankings navegables en dominio o staging

---

### Día 11 — Frontend MVP: buscador de cartas
Prioridad: P0

Objetivo:
Dejar útil el buscador de cartas como segunda superficie principal.

Tareas:
- Validar autocompletado.
- Corregir lógica de `getApiUrl()` si estorba.
- Comprobar filtros por set, rareza y formato.
- Verificar tiempos de respuesta y UX básica.

Entregable del día:
- buscador funcional

---

### Día 12 — Frontend MVP: detalle de carta
Prioridad: P1

Objetivo:
Cerrar el circuito básico de exploración.

Tareas:
- Verificar modal/ficha.
- Validar gráfico de precios.
- Comprobar comportamiento con cartas sin precio o sin histórico.
- Revisar payload por si hay que adelgazarlo.

Entregable del día:
- detalle de carta usable

---

### Día 13 — TORACLES: artículos puente
Prioridad: P1

Objetivo:
Conectar intención editorial y utilidad práctica.

Tareas:
- preparar dos piezas de contenido puente:
  - base de maná
  - cartas que suben / staples calientes
- insertar CTA suave al producto donde encaje
- reforzar enlazado interno

Entregable del día:
- 2 piezas puente o sus borradores finales

---

### Día 14 — Publicación controlada de la beta inicial
Prioridad: P0

Objetivo:
Tener algo real y visible en mtgdeckbuilding.com.

Tareas:
- levantar frontend + API
- validar landing + navegación básica
- comprobar que el dominio responde
- registrar fallos críticos remanentes

Entregable del día:
- beta inicial publicada o staging verificable

Criterio de cierre de semana 2:
- el dominio nuevo ya muestra una utilidad real

---

## Semana 3 — Integración entre dominios y primera utilidad diferencial

### Día 15 — Hub de herramientas en TORACLES
Prioridad: P1

Objetivo:
Crear un punto editorial que explique la capa de producto.

Tareas:
- diseñar la página/hub “Herramientas”
- enlazar a mtgdeckbuilding.com
- explicar qué resuelve y para quién

Entregable del día:
- hub o página de herramientas

---

### Día 16 — Optimización de sugerencias
Prioridad: P1

Objetivo:
Reducir el coste del fuzzy search actual.

Tareas:
- medir el coste de `SELECT DISTINCT name FROM cards`
- definir alternativa más eficiente
- prototipar mejora o dejar especificación cerrada

Entregable del día:
- informe de optimización o mejora aplicada

---

### Día 17 — Diseñar “Completa tu mazo”
Prioridad: P1

Objetivo:
Cerrar la primera utilidad diferencial real del dominio nuevo.

Tareas:
- definir entradas aceptadas
- definir parser
- definir flujo de usuario
- definir qué devuelve y qué enlaza

Entregable del día:
- especificación funcional de “Completa tu mazo”

---

### Día 18 — TORACLES: bloque editorial basado en datos
Prioridad: P1

Objetivo:
Preparar un patrón reutilizable para artículos enriquecidos con datos.

Tareas:
- diseñar bloque “Top subidas 7d”
- diseñar bloque “Top bajadas 30d”
- definir cuándo encajan editorialmente
- decidir si serán manuales, capturados o embebidos

Entregable del día:
- plantilla de bloque editorial de mercado

---

### Día 19 — Páginas utilitarias candidatas
Prioridad: P2

Objetivo:
Definir qué páginas SEO sí puede atacar mtgdeckbuilding.com sin canibalizar.

Tareas:
- listar páginas candidatas:
  - gainers por set
  - losers por color
  - cartas por legalidad
  - staples por filtro utilitario
- descartar cualquier cosa demasiado editorial

Entregable del día:
- backlog SEO utilitario del dominio nuevo

---

### Día 20 — Instrumentación mínima
Prioridad: P1

Objetivo:
Empezar a medir el uso real del producto.

Tareas:
- definir eventos clave
- medir visitas a landing
- medir uso de buscador
- medir aperturas de detalle
- medir clics desde TORACLES

Entregable del día:
- cuadro mínimo de métricas del producto

---

### Día 21 — Cierre semanal
Prioridad: P0

Objetivo:
Cerrar el encaje real entre los dos dominios.

Tareas:
- validar navegación cruzada
- revisar si los CTAs tienen sentido
- confirmar que no hay duplicación temática grave
- priorizar lo que entra en semana 4

Entregable del día:
- informe de integración semana 3

---

## Semana 4 — Medición, ajuste y cierre del ciclo

### Día 22 — Revisión de contenidos con mejor encaje producto
Prioridad: P1

Objetivo:
Seleccionar qué piezas de TORACLES deben enviar más tráfico al dominio nuevo.

Tareas:
- revisar staples por color
- revisar tierras
- revisar combos
- revisar guías de commander donde precio/datos aporten más

Entregable del día:
- shortlist de páginas puente prioritarias

---

### Día 23 — Revisar UX del producto
Prioridad: P1

Objetivo:
Eliminar fricción del MVP.

Tareas:
- revisar errores frecuentes
- revisar estados vacíos
- revisar mensajes de error
- revisar tiempos de carga

Entregable del día:
- lista de mejoras UX de beta

---

### Día 24 — Preparar snippets/widgets futuros
Prioridad: P2

Objetivo:
Dejar diseñada la futura integración embebible.

Tareas:
- definir snippet de “Top subidas 7d”
- definir snippet de “Carta destacada”
- definir enlaces profundos hacia detalle de carta

Entregable del día:
- especificación de widgets embebibles

---

### Día 25 — Medición SEO/editorial de TORACLES
Prioridad: P1

Objetivo:
Retomar la medición del plan SEO original donde ya toque.

Tareas:
- descargar export nuevo de Search Console
- comparar contra línea base
- revisar CTR / posición / clics
- comprobar si el top 3 pierde peso relativo

Entregable del día:
- informe de medición TORACLES

---

### Día 26 — Medición de uso del producto
Prioridad: P1

Objetivo:
Entender si mtgdeckbuilding.com ya aporta algo más que presencia.

Tareas:
- revisar tráfico
- revisar búsquedas
- revisar páginas más vistas
- revisar clics desde TORACLES
- revisar qué funcionalidad engancha más

Entregable del día:
- informe de uso inicial de mtgdeckbuilding.com

---

### Día 27 — Ajuste del enlazado entre dominios
Prioridad: P1

Objetivo:
Refinar el sistema según las primeras señales.

Tareas:
- mover CTAs que no funcionen
- reforzar CTAs que sí encajen
- mejorar anchor text y contexto

Entregable del día:
- mapa ajustado de enlaces y CTAs

---

### Día 28 — Backlog 31-60
Prioridad: P1

Objetivo:
Preparar la siguiente fase sin improvisar.

Tareas:
- priorizar mejoras de producto
- priorizar siguientes piezas evergreen
- decidir si entra Postgres, widgets o la utilidad “Completa tu mazo”

Entregable del día:
- backlog priorizado de 30 días siguientes

---

### Día 29 — Validación de cierre
Prioridad: P0

Objetivo:
Comprobar que el ciclo de 30 días deja dos activos más fuertes que al inicio.

Tareas:
- validar TORACLES como marca editorial
- validar mtgdeckbuilding.com como activo útil
- revisar métricas mínimas
- revisar bloqueos abiertos

Entregable del día:
- checklist de cierre

---

### Día 30 — Informe final y decisión de fase 2
Prioridad: P0

Objetivo:
Cerrar el ciclo con decisión ejecutiva, no solo con trabajo hecho.

Tareas:
- resumir logros por dominio
- resumir métricas
- resumir bloqueos
- decidir foco 31-90:
  - más SEO
  - más producto
  - integración
  - monetización

Entregable del día:
- informe final de 30 días
- decisión de fase 2

---

## Checklist de aceptación al día 30

### TORACLES
- mantiene su rol editorial principal
- tiene al menos un pilar evergreen fuerte
- tiene piezas puente hacia el producto
- tiene CTAs consistentes
- tiene medición actualizada

### mtgdeckbuilding.com
- ya no es solo un redirect
- tiene landing y propuesta de valor
- tiene MVP o beta navegable
- tiene API y frontend mínimos validados
- tiene una hoja de ruta clara para la siguiente utilidad

### Sistema conjunto
- no hay duplicación grave de intención SEO
- existe enlazado útil entre ambos
- cada dominio tiene una función entendible
- hay backlog claro para días 31-60

---

## Resultado esperado

Al final del día 30:
- TORACLES debe quedar más fuerte como autoridad editorial y máquina de adquisición.
- mtgdeckbuilding.com debe quedar activado como producto real o beta seria.
- ambos dominios deben funcionar como sistema complementario:
  - TORACLES atrae y educa
  - mtgdeckbuilding.com resuelve y retiene
