# Semana 1 — Arranque operativo adversarial para TORACLES + mtgdeckbuilding.com

Objetivo:
Definir una semana 1 que reduzca ambigüedad estratégica, riesgo técnico y canibalización SEO antes de decidir qué implementar en TORACLES y en mtgdeckbuilding.com.

Arquitectura de roles:
- TORACLES = marca editorial, SEO, evergreen, criterio, hubs y captación.
- mtgdeckbuilding.com = producto/utilidad interactiva, datos, búsqueda, rankings y herramientas.

Fuentes incorporadas en esta síntesis:
- Vision/Batman: estrategia holística y guardrails.
- Hulk/Thor: camino crítico y tareas secuenciales de bajo arrepentimiento.
- Antigravity/Wonder Woman: crítica adversarial, riesgos, falsas urgencias y gates binarios.

---

## Veredicto estratégico de la oleada SuperHeroes

La semana 1 NO debe usarse para construir mucho. Debe usarse para descartar malas decisiones.

Consenso de agentes:
1. No rebrandear TORACLES.
2. No convertir mtgdeckbuilding.com en un clon de Moxfield/Archidekt.
3. No publicar una beta sobre la base SQLite actual en `/mnt/e` como si ya fuera infraestructura estable.
4. No meter CTAs en TORACLES ni abrir páginas SEO del dominio nuevo hasta validar que el producto mínimo tiene destino fiable.
5. Llegar al día 7 con un dossier de decisión y un go/no-go real para semana 2.

Principio rector:
- TORACLES atrae y educa.
- mtgdeckbuilding.com resuelve y retiene.

---

## Los 4 gates binarios antes de implementar

Si cualquiera falla al cierre de la semana 1, la decisión correcta es reducir scope o posponer la publicación del dominio nuevo.

### Gate 1 — Datos operables
Debe quedar validado uno de estos escenarios:
- base operativa fuera de `/mnt/e` en filesystem Linux nativo, o
- snapshot/read-only equivalente, o
- subconjunto de datos reducido que sirva al MVP sin I/O frágil.

No vale:
- seguir sirviendo la base de ~20 GB en `/mnt/e` con errores de `disk I/O error`.

### Gate 2 — Endpoints P0 medidos con datos reales
Deben medirse de verdad, no asumir:
- `/api/status`
- `/api/cards`
- `/api/rankings`
- `/api/cards/{uuid}`
- `/api/suggest`

No vale:
- publicar el prototipo sin saber latencia, tamaño de payload o coste de consultas.

### Gate 3 — Superficie pública mínimamente cerrada
Antes de exposición pública debe quedar decidido:
- qué pasa con CORS abierto
- qué pasa con `POST /api/sync`
- qué endpoints son públicos y cuáles operativos
- cómo se evita abuso básico

No vale:
- exponer tal cual un backend con `sync` público y superficie abierta indiscriminada.

### Gate 4 — Mapa de intención SEO entre dominios firmado
Debe quedar claro:
- qué búsquedas ataca TORACLES
- qué búsquedas ataca mtgdeckbuilding.com
- qué no se duplica
- cómo se enlaza sin competir

No vale:
- abrir páginas utilitarias o CTAs antes de cerrar esa frontera.

---

## Qué NO hacer en semana 1

Lista consolidada adversarial:
- No migrar ya a Postgres por doctrina si antes no se valida el slice público mínimo.
- No abrir login, usuarios, guardado de mazos, perfiles ni funciones sociales.
- No crear páginas SEO programáticas por set/color/legalidad todavía.
- No rehacer el frontend entero ni hacer branding completo.
- No endurecer todo el ETL, workers, colas o scheduler de producción esta semana.
- No publicar landing conectada a un backend frágil solo por “tener algo visible”.
- No meter CTAs desde TORACLES si el destino aún no es fiable.
- No confundir “lo que el prototipo ya hace” con “lo que el MVP debe exponer”.

---

## Prioridades de la semana 1

### P0
- Congelar el reparto de roles entre dominios.
- Auditar viabilidad operativa mínima de MTGJSON.
- Cerrar decisión de datos para una beta segura.
- Definir arquitectura mínima de publicación.
- Definir el alcance exacto del MVP utilitario.
- Diseñar el puente TORACLES → producto, pero sin activarlo aún.
- Cerrar la semana con checklist go/no-go.

### P1
- Reordenar backlog heredado de TORACLES bajo el modelo de dos dominios.
- Definir CTAs y bloque editorial reutilizable.
- Decidir KPIs mínimos por dominio.

### P2
- Branding más amplio.
- Widgets embebibles.
- Páginas SEO utilitarias futuras.
- Roadmap de monetización.

---

## Plan operativo día a día

### Día 1 — Mapa de dominios y límites
Prioridad: P0

Objetivo:
Congelar el mandato de cada dominio y frenar scope creep desde el primer día.

Tareas:
- Escribir un documento de una página con la regla base:
  - TORACLES = editorial/SEO
  - mtgdeckbuilding.com = producto/herramientas
- Definir la promesa exacta de mtgdeckbuilding.com en una frase.
- Hacer una tabla de 3 columnas:
  - vive en TORACLES
  - vive en mtgdeckbuilding.com
  - no entra en MVP
- Listar 5 tipos de páginas TORACLES compatibles con un futuro CTA al producto:
  - staples
  - subidas de precio
  - base de maná
  - guías de color
  - precons
- Definir un KPI operativo inicial por dominio:
  - TORACLES = clics salientes útiles al producto
  - mtgdeckbuilding.com = visitas a landing / uso del CTA principal

Entregable:
- documento de reparto de dominios

Criterio de cierre:
- cada dominio puede explicarse en una frase sin solapamiento
- existe una lista explícita de exclusiones del MVP

---

### Día 2 — Auditoría del activo MTGJSON
Prioridad: P0

Objetivo:
Auditar el prototipo solo para decidir viabilidad mínima, no para optimizarlo.

Tareas:
- Revisar backend, ETL, analytics, frontend y DB.
- Inventariar endpoints ya presentes.
- Inventariar superficies de frontend ya existentes.
- Documentar el riesgo real de SQLite en `/mnt/e`.
- Decidir preliminarmente qué piezas pueden reutilizarse en semana 2.
- Declarar fuera de auditoría esta semana el tuning profundo y el multiusuario.

Entregable:
- inventario técnico con 4 bloques: ETL, datos, API, frontend

Criterio de cierre:
- el riesgo de `/mnt/e` queda escrito como bloqueo operativo real
- existe una lista corta de piezas reutilizables y piezas no publicables

---

### Día 3 — ADR de arquitectura mínima
Prioridad: P0

Objetivo:
Cerrar el camino más corto y soportable para una beta mínima.

Tareas:
- Elegir topología mínima: mismo dominio sirviendo landing + frontend + API.
- Definir camino de despliegue mínimo.
- Especificar runtime mínimo: base, puerto, variables, logs y reinicio.
- Definir solo 3 entornos: local, staging ligero opcional y producción mínima.
- Decidir explícitamente qué no se migra todavía.

Entregable:
- ADR corto de despliegue y datos

Criterio de cierre:
- otra persona puede entender dónde vive frontend, API, base y logs sin adivinar

---

### Día 4 — Especificación del MVP utilitario
Prioridad: P0

Objetivo:
Recortar el producto hasta una utilidad estrecha y defendible.

Tareas:
- Decidir el primer MVP público exacto.
- Elegir una promesa principal.
- Definir 1-2 casos de uso principales.
- Definir pantallas mínimas.
- Definir qué datos se mostrarán y cuáles no.
- Definir exclusiones de features.
- Escribir wireframe textual corto.

Entregable:
- especificación funcional cerrada del MVP

Criterio de cierre:
- el MVP puede describirse sin usar “y además” cinco veces
- hay una única promesa principal y un único CTA principal

---

### Día 5 — Puente editorial-producto
Prioridad: P1, con gate previo

Precondición:
Solo se diseña el puente. No se activa si Gate 1-4 siguen abiertos.

Objetivo:
Preparar el enlace TORACLES → producto sin todavía empujar tráfico.

Tareas:
- Redactar 3 CTAs reutilizables.
- Diseñar bloque editorial estándar.
- Definir dónde entra cada CTA y dónde se prohíbe.
- Elegir 5 URLs o 5 tipos de piezas candidatas para insertar el puente en semana 2.
- Definir que TORACLES no enlaza siempre a la home del producto.
- Dejar definida la convención de medición del puente.

Entregable:
- matriz de enlazado + biblioteca de CTAs

Criterio de cierre:
- cada CTA tiene uso permitido y prohibido
- hay al menos 5 superficies editoriales candidatas

---

### Día 6 — Reordenación del backlog heredado
Prioridad: P1

Objetivo:
Cruzar el plan histórico de TORACLES con el modelo de dos dominios.

Tareas:
- Etiquetar cada tarea heredada.
- Recortar trabajos de alto arrepentimiento.
- Sacar un backlog corto de semana 2 con máximo 5 frentes.
- Marcar dependencias críticas.
- Registrar bloqueadores frente a simples mejoras.

Entregable:
- backlog reconciliado para semana 2 y 3

Criterio de cierre:
- el plan viejo deja de competir con el nuevo
- las dependencias reales quedan explícitas

---

### Día 7 — Acta de cierre con semáforo y go/no-go
Prioridad: P0

Objetivo:
Terminar la semana con decisiones vinculantes y condiciones de entrada para implementación.

Tareas:
- Revisar que existan 5 artefactos cerrados.
- Preparar informe de cierre con semáforo.
- Evaluar los 4 gates binarios.
- Redactar criterios de entrada para semana 2.
- Escribir la secuencia exacta de ejecución de semana 2 en 5 pasos o menos.
- Asignar dueño a cada riesgo abierto.

Entregable:
- acta de cierre de semana 1 con veredicto go/no-go

Criterio de cierre:
- la semana termina con decisiones operativas, no con brainstorming
- si no hay go, queda escrito por qué no hay go

---

## Checklist de aceptación de semana 1

Debe existir todo esto al cierre:
- documento de reparto de dominios
- tabla de exclusiones del MVP
- inventario técnico real de MTGJSON
- decisión escrita sobre datos para beta
- ADR de despliegue mínimo
- especificación funcional cerrada del MVP
- biblioteca de CTAs y matriz de enlazado
- backlog reconciliado con el plan histórico
- acta de cierre con gates y go/no-go

---

## Recomendación adversarial final

No aprobar implementación en semana 2 si sigue en rojo cualquiera de estos puntos:
- base no accesible de forma estable fuera de `/mnt/e`
- endpoints P0 sin medir con datos reales
- superficie pública expuesta sin cierre mínimo
- frontera SEO entre dominios sin firmar

Si pasa todo:
- semana 2 puede entrar en publicación mínima, no en expansión.

Si falla uno:
- reducir scope.

Si fallan dos o más:
- posponer mtgdeckbuilding.com como producto público y mantenerlo como activo interno o landing estática temporal.
