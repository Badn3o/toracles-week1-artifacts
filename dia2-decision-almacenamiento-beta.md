# Día 2 — Decisión de almacenamiento para la beta

Estado:
Decisión cerrada para Gate 1 de semana 1.

Fecha:
2026-09-02

---

## Decisión ejecutiva

Decisión recomendada para la beta:
- NO servir la beta pública desde la base SQLite actual ubicada en `/mnt/e/AIProyects/MTGJSON/data/mtg_analytics.db`.
- Sí preparar una base operativa separada para beta en filesystem Linux nativo.
- Mantener SQLite para la beta si el alcance sigue estrecho.
- Operar la beta pública sobre una copia/snapshot o subset controlado en Linux nativo, no sobre la base activa problemática en `/mnt/e`.

Decisión para semana 2:
- escenario elegido = `SQLite en filesystem Linux nativo + separación entre base operativa pública beta y prototipo/ETL actual`.

Esto no implica migrar hoy.
Implica cerrar la dirección correcta y prohibir explícitamente que la beta nazca sobre `/mnt/e`.

---

## Opciones consideradas

### Opción A — Seguir con SQLite en `/mnt/e`

Qué sería:
- usar la base actual tal cual, en la ruta actual, con el backend actual.

Pros:
- cero trabajo de cambio inmediato
- reaprovecha el activo existente sin copiar ni separar

Contras:
- ya existe evidencia real de `disk I/O error`
- el acceso estable observado fue solo en readonly/immutable
- contradice el Gate 1 de la semana 1
- mezcla ETL, lectura pública y riesgo de escritura/WAL en una ubicación frágil bajo WSL/NTFS
- deja la beta colgada de un comportamiento no fiable

Veredicto:
- descartada

### Opción B — SQLite en filesystem Linux nativo

Qué sería:
- mantener SQLite, pero mover la base operativa de beta a un filesystem Linux real
- servir desde una copia/snapshot o subset controlado

Pros:
- conserva simplicidad de stack
- evita el punto de fragilidad ya conocido en `/mnt/e`
- encaja con un MVP estrecho sin meter Postgres todavía
- permite separar base de operación interna y base pública beta
- menor coste de cambio que una migración relacional completa

Contras:
- sigue exigiendo disciplina de separación entre ETL y lectura pública
- no resuelve por sí sola CORS, `POST /api/sync` o payloads pesados
- puede quedarse corta más adelante si el producto se ensancha mucho

Veredicto:
- recomendada para beta estrecha

### Opción C — Postgres ya

Qué sería:
- migrar ahora el backend de datos a Postgres antes de abrir beta

Pros:
- mejor camino si el producto fuese a escalar rápido
- mejor separación futura para concurrencia y operación multi-servicio

Contras:
- aumenta alcance, tiempo y superficie de fallo esta semana
- no es necesario para probar un MVP estrecho
- movería el foco desde validar producto mínimo a rehacer infraestructura

Veredicto:
- no recomendada para semana 1 ni como requisito previo del Día 2
- se deja como posible fase posterior si la beta valida uso y volumen

### Opción D — dual setup dev/prod

Qué sería:
- seguir desarrollando con un origen y servir producción/beta con otro
- por ejemplo: prototipo/ETL en una base y snapshot público en otra

Pros:
- separa bien operación interna y exposición pública
- reduce riesgo de publicar el entorno de trabajo tal cual
- encaja con un enfoque de snapshot/subset para beta

Contras:
- añade disciplina operativa
- obliga a definir qué datos exactos entran en la copia pública

Veredicto:
- útil como patrón operativo
- compatible con la opción recomendada

---

## Opción recomendada

Recomendación cerrada:
- `SQLite en filesystem Linux nativo` para la beta
- con patrón de `dual setup` ligero:
  - origen de trabajo/prototipo puede seguir existiendo aparte
  - base servida al público debe ser otra, en filesystem Linux nativo
  - preferiblemente snapshot o subset orientado al MVP

En una frase:
- Beta sí con SQLite; beta no desde `/mnt/e`.

---

## Por qué NO vale seguir en `/mnt/e` como base operativa pública

Porque ya hay evidencia adversarial suficiente de que no es un riesgo teórico:
- el acceso normal a SQLite ya dio `disk I/O error`
- el acceso estable solo se observó en readonly/immutable
- la base ronda ~19G y contiene `prices_raw` muy grande
- la conexión normal del código activa WAL
- WSL + NTFS + SQLite + WAL ya ha mostrado el patrón exacto de fragilidad que el Gate 1 intenta bloquear

Decisión binaria:
- si la base pública depende de `/mnt/e`, el Gate 1 no está superado
- si la beta usa Linux filesystem nativo para la base operativa, el Gate 1 puede pasar a amarillo/verde condicionado

---

## Qué significa esta decisión en la práctica

Semana 2 debe asumir esto:
- no se publica el backend apuntando a `/mnt/e/AIProyects/MTGJSON/data/mtg_analytics.db`
- no se vende como resuelto el problema actual de almacenamiento
- se prepara una base pública separada
- la base pública debe vivir fuera de `/mnt/e`
- el MVP debe apoyarse primero en superficies estrechas:
  - rankings
  - búsqueda
  - ficha de carta
- la beta no necesita exponer toda la operación ETL ni todo el dataset crudo

---

## Decisión para semana 2

Decisión operativa cerrada:
- Semana 2 entra con `SQLite en filesystem Linux nativo` como opción de salida para beta.
- Se recomienda hacerlo mediante copia/snapshot o subset público separado del prototipo.
- Postgres queda pospuesto salvo que aparezca un bloqueo nuevo que haga inviable SQLite fuera de `/mnt/e`.

No decidido todavía en este documento:
- ruta exacta
- proceso de snapshot
- topología de despliegue
- recorte exacto de payloads

Eso pasa al Día 3.

---

## Riesgos que siguen abiertos incluso con la opción recomendada

Esta decisión arregla la dirección del almacenamiento, no todo el sistema.
Siguen abiertos:
- cierre de CORS
- retirar o proteger `POST /api/sync`
- separar superficie pública de superficie operativa
- validar coste real de `/api/cards`, `/api/suggest` y `/api/cards/{uuid}`
- definir si la beta usa snapshot completo o subset más estrecho

---

## Veredicto del Día 2 sobre almacenamiento

Decisión tomada:
- NO seguir con `/mnt/e` como base operativa pública
- SÍ usar SQLite fuera de `/mnt/e` para beta estrecha
- Postgres no entra como obligación de esta semana

Gate 1:
- queda resuelto a nivel de decisión
- no queda resuelto todavía a nivel de implementación