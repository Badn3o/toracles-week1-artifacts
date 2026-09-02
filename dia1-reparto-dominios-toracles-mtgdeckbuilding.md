# Día 1 — Reparto de dominios, límites y exclusiones del MVP

Estado:
Documento de decisión. No es brainstorming.

Objetivo:
Congelar desde el primer día qué papel juega cada dominio, qué no debe hacer cada uno y qué queda expresamente fuera del MVP para evitar canibalización, deriva de marca y scope creep.

Fecha:
2026-09-02

---

## Decisión principal

Se adopta el siguiente reparto de roles:

- TORACLES = dominio editorial principal, SEO principal, autoridad de marca y contenido evergreen.
- mtgdeckbuilding.com = dominio de producto/herramientas, utilidad interactiva, datos y exploración práctica.

Este reparto NO es temporal salvo revisión explícita posterior.

---

## Frase operativa de cada dominio

### TORACLES
TORACLES existe para atraer, explicar, ordenar y dar criterio sobre Commander y Magic con voz editorial propia.

### mtgdeckbuilding.com
mtgdeckbuilding.com existe para ayudar al usuario a consultar, explorar y usar datos prácticos de cartas y construcción de mazos de forma interactiva.

---

## Regla de oro

Si una pieza vive mejor como lectura, contexto, guía, criterio, comparación explicada o contenido evergreen, vive en TORACLES.

Si una pieza vive mejor como búsqueda, filtro, exploración, ranking dinámico, detalle utilitario o herramienta accionable, vive en mtgdeckbuilding.com.

---

## Tabla de reparto (3 columnas)

| Vive en TORACLES | Vive en mtgdeckbuilding.com | No entra en el MVP |
|---|---|---|
| Guías de Commander | Buscador de cartas | Red social de mazos |
| Staples por color | Rankings de subidas y bajadas | Login/usuarios/cuentas |
| Combos explicados | Histórico de precios | Guardado de mazos |
| Precons y upgrades narrados | Ficha de carta con datos | Comentarios sociales, follows, favoritos |
| Commander de la Semana | Filtros por color, set, rareza, legalidad, proveedor | Clon de Moxfield / Archidekt / TopDecked |
| Academia del Oráculo | Utilidades de deckbuilding | Monetización compleja desde el día 1 |
| Rankings editoriales | Exploración de dataset | Newsletter como pieza central |
| Opinión, análisis, contexto y recomendaciones | Páginas utilitarias basadas en datos reales | App móvil/PWA avanzada |
| Hubs de categoría |  | Internacionalización |
| Piezas evergreen: “cómo jugar”, “cómo construir”, “qué tener en cuenta” |  | Páginas SEO programáticas masivas antes de validar MVP |

---

## Límites explícitos por dominio

### Lo que TORACLES no debe hacer
- No debe convertirse en un visor de datos disfrazado.
- No debe absorber el producto nuevo dentro del contenido editorial como si todo viviera en WordPress.
- No debe crear páginas utilitarias pobres solo por captar keywords de herramienta.
- No debe perder voz de marca para sonar como un dashboard.
- No debe enlazar a un producto roto o inmaduro.

### Lo que mtgdeckbuilding.com no debe hacer
- No debe intentar ser un medio editorial paralelo.
- No debe replicar artículos de TORACLES con otro dominio.
- No debe arrancar como plataforma social.
- No debe intentar resolver “todo deckbuilding” desde la beta.
- No debe salir a público si depende de una infraestructura de datos frágil.

---

## Promesa exacta de mtgdeckbuilding.com

Promesa de producto, versión Día 1:

“Una herramienta práctica para Commander que permite explorar cartas, consultar rankings y usar datos útiles para construir mejor tus mazos.”

Elementos incluidos en esa promesa:
- búsqueda
- rankings
- datos útiles
- foco Commander

Elementos excluidos de esa promesa:
- comunidad
- deckbuilder completo
- red social
- colección personal
- suite total de MTG

---

## Audiencia principal por dominio

### TORACLES
- Jugador que busca entender
- Jugador que busca criterio
- Jugador que descubre arquetipos, comandantes, staples y líneas de juego
- Usuario que llega por Google con intención informacional/editorial

### mtgdeckbuilding.com
- Jugador que ya está en modo utilidad
- Usuario que quiere buscar una carta, comparar señales o consultar datos concretos
- Usuario que necesita una herramienta rápida mientras afina decisiones
- Usuario que ya está construyendo o ajustando un mazo

---

## Intención de búsqueda por dominio

### Intención principal de TORACLES
- informacional
- editorial
- comparativa explicada
- evergreen de aprendizaje

Ejemplos:
- mejores cartas verdes para commander
- cómo jugar commander desde cero
- guía de atraxa commander
- mejores tierras para commander
- combos commander explicados

### Intención principal de mtgdeckbuilding.com
- utilitaria
- exploratoria
- lookup
- ranking dinámico
- uso práctico del dato

Ejemplos:
- mtg price gainers commander
- buscar carta commander por color y coste
- cartas legales en commander con subida de precio
- staples por set/color/rareza

---

## 5 superficies editoriales de TORACLES compatibles con futuro CTA al producto

1. Staples por color
- Encaje: alto
- CTA natural: explorar cartas relacionadas / rankings / consulta de staples

2. Artículos sobre tierras y base de maná
- Encaje: alto
- CTA natural: buscar tierras por color, coste o tendencias

3. Piezas sobre cartas que suben o bajan
- Encaje: muy alto
- CTA natural: ver rankings dinámicos y detalle de carta

4. Guías de color y guías de comandante
- Encaje: medio-alto
- CTA natural: buscar piezas del mazo o consultar cartas clave

5. Precons y upgrades
- Encaje: alto
- CTA natural: explorar cartas de mejora y filtros prácticos

---

## Reglas de CTA entre dominios

Aún no se implementan. Solo se congelan las reglas.

Reglas:
- TORACLES enlaza al producto cuando añade utilidad inmediata al lector.
- TORACLES no enlaza por rutina ni por relleno.
- TORACLES debe enlazar a una página útil concreta del producto, no siempre a la home.
- mtgdeckbuilding.com enlaza de vuelta a TORACLES cuando el usuario necesita contexto editorial, no solo dato.
- Ningún CTA debe competir con el H1 o la intención principal de la página.

---

## KPI operativo inicial de la semana 1

### TORACLES
KPI operativo de semana 1:
- capacidad de definir y localizar puntos de salida útiles hacia el producto sin degradar intención editorial

KPI cuantitativo inicial para semana 2-4:
- clics salientes cualificados hacia mtgdeckbuilding.com

### mtgdeckbuilding.com
KPI operativo de semana 1:
- claridad de promesa y alcance mínimo del producto

KPI cuantitativo inicial para semana 2-4:
- visitas a landing
- uso del CTA principal
- primeras acciones útiles dentro del MVP

---

## Exclusiones del MVP (lista cerrada)

Queda expresamente fuera del MVP inicial:
- cuentas de usuario
- login
- guardado de mazos
- importación/exportación avanzada de listas
- comentarios o funciones sociales
- marketplace
- monetización compleja
- recomendaciones automáticas completas de deckbuilding
- builders competitivos tipo Moxfield
- páginas SEO masivas por combinatoria
- app móvil dedicada
- integración con tienda si no existe todavía un flujo claro

Toda propuesta futura que toque estos puntos deberá entrar como fase posterior, no como expansión silenciosa del MVP.

---

## Riesgos que esta decisión intenta evitar

1. Canibalización SEO
- dos dominios peleando por la misma intención

2. Dilución de marca
- TORACLES perdiendo identidad editorial

3. Scope creep
- mtgdeckbuilding.com intentando nacer como suite total

4. Mala secuenciación
- abrir CTAs o páginas del producto antes de tener destino sólido

5. Deuda operativa temprana
- publicar un producto mayor de lo que la infraestructura soporta

---

## Decisiones derivadas para el Día 2

Este documento obliga a que la auditoría técnica del Día 2 responda estas preguntas:
- ¿qué parte de MTGJSON sirve de verdad al MVP definido?
- ¿qué parte es prototipo local no publicable?
- ¿qué subset de datos es suficiente para una beta estrecha?
- ¿qué arquitectura mínima soporta el reparto de dominios sin romperlo?

---

## Veredicto del Día 1

Queda decidido lo siguiente:
- TORACLES seguirá siendo la marca editorial principal.
- mtgdeckbuilding.com se desarrollará como activo de producto/herramientas.
- El MVP del dominio nuevo será estrecho y utilitario.
- El producto no intentará competir desde el día 1 con plataformas de deckbuilding social.
- Ningún puente editorial se activará antes de validar el destino técnico.

Este documento se considera base vinculante para la semana 1 y para el go/no-go de la semana 2.
