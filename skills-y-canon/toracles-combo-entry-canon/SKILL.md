---
name: toracles-combo-entry-canon
description: Use when drafting TORACLES combo posts. Apply canon.
version: 1.1.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [toracles, commander, combo, wordpress, editorial, canon, validation]
    related_skills: [toracles-wordpress-editorial, toracles-editorial-polish, toracles-post-publisher, toracles-wordpress-card-embeds, toracles-wordpress-maintenance]
---

# Canon de Combo de la Semana — TORACLES

## Cuándo usarlo

Aplica este canon a entradas largas de `Combo de la Semana` para Commander, EDH o cEDH. Úsalo junto con `toracles-wordpress-editorial` para voz y metadatos, `toracles-post-publisher` para el borrador y `toracles-wordpress-maintenance` para la comprobación visual real.

No lo uses como sustituto de una consulta de reglas: verifica las líneas de juego antes de redactar.

## Flujo obligatorio

0. Resuelve duplicados antes de redactar o publicar.
   - Lista todos los borradores relacionados por pareja de comandantes, título, slug y fecha de modificación.
   - Distingue tandas por fecha, taxonomía, tipo editorial y contenido; no elijas el ID más alto a ciegas.
   - Conserva los slugs vivos y crea un backup remoto de cada ID y sus metadatos antes de escribir.
   - Si dos tandas representan la misma idea, documenta cuál es la versión moderna y deja la antigua sin tocar hasta que exista una decisión editorial explícita.

1. Verifica el combo antes de escribir.
   - Consulta el texto Oracle exacto y la identidad de color de cada componente mediante Scryfall. Cuando el cuerpo vaya a explicar una lectura de reglas (diálogo Oráculo/Aprendiz, letra pequeña, restricción de objetivo), copia el texto Oracle LITERAL entre comillas antes de escribir la explicación: parafrasear de memoria inventa restricciones que no existen (por ejemplo, asumir que dos modos de una misma habilidad comparten la misma restricción de control cuando el texto real solo la impone en uno). Si el combo depende de una asimetría entre dos modos o cláusulas, compáralas palabra por palabra contra el Oracle real antes de redactar el "error de lectura" que el Oráculo va a corregir — de lo contrario la corrección puede ser tan incorrecta como el error que pretende señalar.
   - Para obtener o rankear combos desde Commander Spellbook (tops por color, "más buscados", ficha de variante), usa `references/commanderspellbook-api.md`: endpoint REST, sintaxis de búsqueda, deduplicación por conjunto de cartas y verificación Scryfall por lote.
   - Recorre la secuencia como estados: requisitos, coste, acción, recursos resultantes, condición para repetir y resultado.
   - Separa hechos garantizados de atajos que dependen de cartas extra, tamaño de cementerio, objetivos, prioridad o contexto de mesa.
   - Identifica ventanas de interacción reales; no digas simplemente que un mazo puede “responder”.

2. Fija la promesa editorial y de búsqueda.
   - El H1 debe ser un nombre evocador que describa el efecto, peligro o fantasía del combo, no una lista de cartas.
   - Conserva los nombres exactos de las cartas en el título SEO, slug, ficha táctica y explicaciones para satisfacer la intención de búsqueda. En el sitio hay DOS capas de título: el `post_title` de WordPress sigue el patrón `Carta + Carta: combo Commander <identidad>` (búsqueda clara) y el H1 del cuerpo es el gancho evocador (efecto/peligro/fantasía). Nunca cambies el slug para encajar el patrón: el slug es la URL viva.
   - Declara el público y la banda de potencia; no presentes una línea cEDH como recomendación universal.

3. Prepara los metadatos fuera del cuerpo visible.
   - Título SEO, slug, meta descripción, extracto, categorías, serie, tags y tesis.
   - El cuerpo visible debe empezar directamente con `# H1` después del último campo. No insertes `---` u otra línea antes del H1: los parsers de paquetes editoriales pueden incorporarla al último campo de metadatos y crear taxonomías defectuosas.
   - Cada campo de metadatos va como etiqueta sola en su propia línea (`Título SEO:` sin nada detrás del `:`), con el valor empezando en la línea siguiente. `publish_toracles_post.py` solo reconoce ese patrón exacto (regla `^Campo:\s*$`); un `Campo: valor` en la misma línea no hace match y el campo se descarta en silencio, sin error — el `--dry-run` te devuelve `title`/`slug` vacíos y esa es la única señal. Comprueba siempre que `title` y `slug` salen no vacíos en el `--dry-run` antes de dar el paquete por bien formado.

4. Redacta con esta progresión.
   - H1 y entradilla NO son solo campos de metadatos: se renderizan como cuerpo visible. Inmediatamente debajo del `# H1` van, cada uno en su propio párrafo en cursiva (`*texto*`), primero el Subtítulo y después el Extracto/entradilla completos — exactamente como aparecen en el post canónico de referencia. Si solo los dejas en el bloque de metadatos y no los repites como párrafos en cursiva al inicio del cuerpo, el post se ve genérico aunque los metadatos estén completos: esto fue exactamente lo que le faltó a la primera tanda de borradores hasta que se comparó contra un post ya publicado.
   - H1 y entradilla: qué amenaza o transformación representa la línea en una mesa real.
   - Ficha táctica: componentes, coste mínimo, colores, pieza central, resultado, montaje, resiliencia/ventanas de freno y accesibilidad.
   - Por qué importa: velocidad, compacidad, consistencia y qué la diferencia de una sinergia.
   - Requisitos antes de empezar: zona de cada carta, maná, cartas disponibles, objetivos y cualquier umbral.
   - Montaje numerado: una acción de juego por paso, con recursos que entran y salen explícitos.
   - Bucle y resultado: explica cómo se repite, qué se incrementa y cómo se convierte en victoria; distingue el hechizo original de sus copias y no simplifiques el maná o el cementerio como infinitos si requieren combustible.
   - Dónde se corta: interacción por prioridad, pieza permanente, pila, cementerio y objetivos; explica qué respuesta sigue funcionando y cuál llega tarde.
   - Variantes y encaje: sustitutos honestos, comandantes/arquetipos que lo sostienen y coste de incluirlo.
   - FAQ: por defecto cuatro preguntas sobre requisito crítico, funcionamiento, respuesta rival y mesa adecuada.
   - Sigue explorando: dos o tres enlaces internos reales, no slugs inventados ni notas de planificación. Cada enlace debe ser un `<a href="...">`/Markdown link a una URL que responda `200` (compruébalo con `curl -s -o /dev/null -w '%{http_code}'`) — una simple mención de carta con `[mtg_card]` en esa sección no sustituye al enlace real.

5. Trata las referencias de cartas como contenido verificable.
   - Valida cada nombre exacto, identidad de color y legalidad actual del formato antes de incluirlo.
   - Si una pieza está prohibida, no la presentes como receta legal actual: etiqueta la línea como histórica/no legal o sustitúyela por una línea verificada.
   - Usa `[mtg_card]Nombre exacto[/mtg_card]` para cada carta citada en el cuerpo; no uses shortcodes en SEO, slug, extracto o taxonomías.
   - No confundas contrarrestar un hechizo con impedir habilidades disparadas ya puestas en pila, ni removal posterior con impedir una habilidad ya activada.
   - Trata `Dockside Extortionist` y cualquier carta con estado cambiante como una comprobación obligatoria, no como una pieza heredada de un modelo antiguo.
   - Verifica en Scryfall CUALQUIER carta que menciones, incluidas las que solo aparecen como ejemplo lateral o sugerencia de respuesta ("si además tenéis X", "un efecto como Y") — no solo las piezas centrales del combo. Un modelo de lenguaje puede inventar un nombre plausible que no existe (verificado con fuzzy+exact search antes de publicar) o sugerir una carta real pero de un color fuera de la identidad del combo que estás describiendo (p. ej. proponer una respuesta blanca dentro de una línea mono-negra) — ambos son errores que un lector detecta al instante y que dañan la credibilidad de todo el artículo.
   - Cuando el efecto de una carta tenga una distinción mecánica precisa en las reglas de Magic (daño vs. pérdida de vida, exilio vs. cementerio, contrarrestar vs. responder a una habilidad ya en pila, coste reducible con piso vs. sin piso), usa la categoría exacta que dice el Oracle text, nunca la aproximada o la más natural en prosa. "Pierde vida" y "recibe daño" no son intercambiables: cambian qué efectos de prevención, protección o indestructibilidad aplican, y describir uno como el otro es un error de reglas, no una licencia narrativa.
  - Distingue SIEMPRE una habilidad de maná (mana ability) de una habilidad disparada normal antes de escribir la sección "Dónde se corta la línea": una habilidad de maná (identificable porque añade maná y no tiene objetivo, o está definida como tal en el Oracle/ruling) NO usa la pila y NO puede ser contrarrestada ni respondida por ningún efecto — la única interacción real es remover la fuente ANTES de que se active. Presentarla como "contrarrestable" (caso real: la duplicación de maná de Kinnan, Bonder Prodigy) es un hallazgo GRAVE de auditoría, no un matiz menor. Verifica en Scryfall/Gatherer si la ruling dice explícitamente "It doesn't use the stack and can't be responded to" antes de describir cualquier ventana de interacción sobre una habilidad de maná.
  - No asumas que una pieza necesita estar "equipada", "encantada" o "unida" a otra para que su disparador funcione, sin verificarlo letra por letra en el Oracle text. Caso real (Nim Deathmantle): su disparador ("Whenever a nontoken creature is put into your graveyard from the battlefield, you may pay {4}...") es independiente de estar equipado a nada — el "attach" a la criatura devuelta ocurre como PARTE de la resolución del propio trigger, no como prerrequisito previo con coste de Equip aparte. Inventar un paso de Equip previo no solo es impreciso: añade un coste de maná falso a la ficha táctica y confunde al lector sobre cómo montar la línea.

6. Construye los metadatos estructurados de "Anatomía de Jugada" — NO OPCIONAL.
   - El sitio renderiza combos con una plantilla dedicada (`content-combo.php`) que SOLO se activa cuando el post tiene el meta `_toracles_editorial_type = combo`. Sin ese meta, WordPress cae a la plantilla de post estándar y el combo se ve como un artículo genérico, muy por debajo del estándar canónico del sitio (ejemplo de referencia: `underworld-breach-lions-eye-diamond-brain-freeze-combo-commander`).
   - Además del `post_content` normal (el artículo largo con H1, ficha táctica, montaje, FAQ, etc.), cada combo necesita estos 5 campos de postmeta adicionales, escritos en prosa concisa y verificada (NO copiar el cuerpo largo, son resúmenes independientes de 2-5 frases cada uno):
     - `_toracles_combo_pieces` — lista de piezas separadas por `|`, cada pieza en formato `Etiqueta :: Nombre de la carta :: Descripción de una frase`. Etiqueta el formato como `Pieza 1/N`, `Pieza 2/N`, etc., donde N es el número real de cartas del combo (2 para combos de 2 piezas, 3 para combos de 3 piezas — no fuerces siempre 3).
     - `_toracles_combo_line` — resumen de la secuencia completa del bucle en un solo párrafo (qué se activa, qué se paga, qué se repite).
     - `_toracles_combo_response_windows` — resumen de la ventana de interacción real: qué objeto exacto hay que atacar y en qué momento, distinguiendo respuestas que llegan a tiempo de las que llegan tarde.
     - `_toracles_combo_resources` — requisitos de mesa antes de montar la línea (piezas en qué zona, maná disponible, identidad de color).
     - `_toracles_combo_risks` — qué rompe la línea antes de que arranque y qué trampas de lectura son comunes (combustible finito, requisitos mal contados, etc.).
   - Escribe estos 5 campos DESPUÉS de redactar el cuerpo completo del artículo, resumiendo con tus propias palabras las secciones ya verificadas (Ficha táctica, Montaje, Dónde se corta, Requisitos) — no inventes contenido nuevo en el resumen que no esté ya verificado en el cuerpo.
   - Aplica los metadatos vía `wp post meta update <ID> <meta_key> "<valor>"` en el servidor (o el mecanismo equivalente disponible), nunca dejándolos vacíos ni delegando en el fallback automático de la plantilla (el fallback solo cubre el caso legacy de "Underworld Breach" hardcodeado; cualquier combo nuevo sin estos metas se ve genérico).
   - Verifica el resultado en navegador real: la URL debe mostrar el kicker "ANATOMÍA DE JUGADA", el índice con 6 anclas (#piezas, #linea, #responder, #recursos, #riesgos, #articulo-completo), y una tarjeta por pieza en `.combo-piece-grid` con el conteo exacto de cartas del combo — no un número fijo.

7. Diseña el par visual antes de publicar — hazlo en la MISMA pasada de redacción, no como retoque posterior tras feedback del usuario.
   - Genera dos ilustraciones IA originales 16:9 sin texto, logotipos, marcas de agua, marcos, interfaz ni cartas reconocibles.
   - Para generar con el proveedor `openai-codex` sin pasar por el tool `image_generate` (por ejemplo en un script batch), carga el plugin directamente: `importlib.util.spec_from_file_location(...,  ".../plugins/image_gen/openai-codex/__init__.py")`, instancia `OpenAICodexImageGenProvider()` y llama a `.generate(prompt=..., aspect_ratio='landscape')`; redimensiona el resultado a 1600x900 con recorte central antes de subirlo (ver `toracles-wordpress-editorial/references/image-generation-fallbacks.md`).
   - Sube ambas imágenes a la biblioteca de medios con `wp media import <ruta> --title=... --alt=... --porcelain` (devuelve el ID de adjunto), obtén la URL real con `wp post get <media_id> --field=guid`, fija el HERO como `_thumbnail_id` del post con `wp post meta update <post_id> _thumbnail_id <media_id>`, e inserta la imagen interna como `<img>` dentro del HTML del cuerpo en el punto de mayor tensión narrativa (justo tras el H2 de la sección de interacción/ventanas), nunca al final del artículo.
   - Define una dirección común de paleta, iluminación y lenguaje visual. El HERO representa la promesa o impacto del combo; la imagen intermedia representa el motor, la secuencia o la tensión táctica.
   - Las dos escenas deben ser distintas; no uses una copia, un recorte ni una tira de cartas como imagen intermedia.
   - Asigna el HERO como `featured_media`; inserta la imagen interna antes de la sección que profundiza en las piezas o el funcionamiento.
   - Añade `alt_text` descriptivo y deja el caption vacío salvo petición expresa del usuario.
   - `publish_toracles_post.py` regenera `*_wp_clean.html` desde el `.md` fuente en CADA ejecución, incluido `--dry-run`: cualquier edición manual hecha directamente sobre el `.html` ya generado (como insertar la URL real de la imagen interna) se pierde en la siguiente ejecución del script. Inserta primero un marcador en el `.md` fuente en el punto exacto del cuerpo (`![alt](__INNER_IMAGE_URL__)`), ejecuta el publicador para generar el HTML limpio, y solo entonces sustituye el marcador por la URL real ya subida — nunca al revés, y nunca vuelvas a correr el publicador sobre el `.md` sin haber quitado antes el marcador o haberlo actualizado con la URL real.

8. Publica como borrador y verifica la lectura real.
   - Ejecuta primero el publicador en `--dry-run`.
   - Crea o actualiza en `draft` salvo orden explícita de publicar; una orden explícita de publicación exige igualmente backup, validación y rollback preparado.
   - Lee el post por REST y confirma ID, estado, autor, H1, slug, extracto, categorías, tags, imagen destacada e imagen interna.
   - Cuando se publica una ola de entradas, verifica cada ID individualmente y después la ola completa: estado `publish`, slug único, H1 visible, metadatos Candidate2 presentes y ausencia de `Card not found` o shortcodes crudos.
   - Compara IDs de categorías y tags como conjuntos si el orden no es semántico: REST puede reordenarlos sin que exista diferencia editorial.
   - Comprueba que `content.rendered` no contiene shortcodes crudos ni `Card not found`, y que todas las imágenes editoriales responden.
   - Abre el borrador o URL pública en navegador: valida primer viewport, HERO, ausencia de caption visible no deseado, imagen interna, shortcodes renderizados y al menos un tooltip de carta con geometría correcta.
   - Antes de publicar una tanda nueva (y obligatorio si el usuario pide una comprobación adversarial explícita), corre una pasada de auditoría independiente que NO reutilice el razonamiento de quien escribió el post: re-verifica desde cero el Oracle text y la línea de combo real contra Scryfall/Commander Spellbook, con instrucción explícita de buscar (a) cartas citadas que no existan, (b) confusiones de categoría mecánica (daño/vida, exilio/cementerio), (c) sugerencias de respuesta fuera de la identidad de color declarada, y (d) matices aritméticos del coste (pisos de reducción, topes). Solo corrige lo marcado como grave con una edición quirúrgica (localizar la frase exacta y sustituirla), sin reescribir el post entero.
   - Cuando la migración se delega a subagentes en paralelo (una ola de N posts), NO des por buena su respuesta JSON de autoreporte para invariantes críticos (aviso de baneo intacto, slug sin cambios, cero enlaces `deckbox_link` restantes): re-ejecuta tú mismo el `grep`/`wp post get` correspondiente sobre cada post al terminar. Un subagente puede reportar `false` en un campo booleano que en realidad SÍ se cumplió (falso negativo por lectura apresurada) o `true` en uno que no — la única fuente de verdad es el contenido real en el servidor, no el resumen que el subagente escribe sobre sí mismo.
   - La misma regla aplica al editar campos SEO (título/descripción de The SEO Framework) por navegador en un lote de posts: la sesión de wp-admin puede expirar a mitad de lote sin que el botón de guardar lo refleje — el texto del botón ("Guardar") sigue apareciendo como éxito aunque la petición subyacente haya sido redirigida a login. Verifica CADA post individualmente con un `goto()` fresco justo tras guardarlo (releyendo el valor real de los campos), nunca guardes el lote completo y verifiques solo al final; si alguno no persistió, reautentica y repite solo ese subconjunto uno por uno. La prueba más fuerte de que el cambio llegó al lector es un `curl` a la URL pública comprobando `<title>` y `<meta name="description">` en el HTML servido, no solo lo que muestra el editor.

9. Antes de migrar una ola existente a un canon nuevo, diagnostica el estado real de cada post, no asumas que todos necesitan el mismo trabajo.
   - Un borrador puede ya tener H1 literario, entradilla en `<em>`, `[mtg_card]` y ambas imágenes correctas, y solo faltarle los 6 metadatos técnicos (`_toracles_editorial_type` vacío) — en ese caso el trabajo es AÑADIR metadatos, no regenerar contenido ni imágenes nuevas. Verifica con `wp post get <ID> --field=post_content | head` y `wp post meta get <ID> _toracles_editorial_type` antes de asignar la tarea a un subagente, para no gastar generación de imágenes ni reescritura en algo que ya está bien.
   - Agrupa los posts de una ola por estado real (ya-bueno-solo-falta-metadata / usa-enlaces-deckbox-crudos / formato Gutenberg legacy completo / baneado-histórico) y da a cada subagente solo el subconjunto con el mismo perfil de trabajo — instrucciones más estrechas y correctas por grupo, en vez de una instrucción genérica "aplica el canon" que un subagente podría sobre-ejecutar (regenerando contenido ya bueno) o sub-ejecutar (dejando huecos).

## Reescritura de posts antiguos "Hola Aprendices" (formato Gutenberg legacy) a canon

Cuando el post original es un bloque Gutenberg suelto (`<!-- wp:paragraph -->`) con tono "Hola Aprendices" y sin H1 literario ni las 6 secciones canónicas, trátalo como reescritura completa, no como polish incremental:

1. Lee el post_content original completo y extrae los datos ya verificados en él (coste real, piezas, líneas de juego, advertencias) — son la base factual, no la prosa.
2. Re-verifica cada carta contra Scryfall igualmente aunque el post antiguo ya diera un coste/efecto: los posts legacy con frecuencia inflan restricciones (asimetrías entre modos de una habilidad) o dan costes de maná ligeramente erróneos.
3. Si el post ya tenía los metadatos `_toracles_combo_*` de una pasada de auditoría previa (verifícalo con `wp post meta get <ID> _toracles_editorial_type` antes de asumir que faltan), esos metadatos suelen ser MÁS correctos que la prosa Gutenberg original porque ya pasaron por verificación Scryfall — úsalos como fuente de verdad para el nuevo cuerpo en vez de reescribir desde cero.
4. Un combo/candado de solo 2 piezas no necesita forzar 3; ajusta el conteo N de `Pieza X/N` al número real.
5. Para posts baneados (aviso `<!-- TORACLES-COMBO-STATUS: BANEADO -->` al inicio del post_content), NUNCA reescribas el cuerpo ni añadas H1 nuevo — solo verifica/crea los 6 metadatos técnicos con contenido que dejando claro que es una línea histórica no legal; el aviso de baneo debe permanecer literalmente igual y en la misma posición (primera línea del content).

## Verificación post-publicación: aparición en el archivo de combos

Publicar un post con `_toracles_editorial_type=combo` no basta para que aparezca en `/combos/`: la plantilla de archivo (`page-combos.php`) filtra por meta Y por categoría, y ambos filtros pueden ocultar entradas ya publicadas por causas no obvias. Tras publicar cualquier tanda, valida SIEMPRE las 2-3 páginas del archivo en navegador (no solo el `post_status`) y si falta alguna entrada, diagnostica en este orden:

1. **Taxonomía jerárquica mal excluida.** Si la consulta usa `tax_query` con `operator => NOT IN` sobre una categoría padre (p. ej. excluir "comandantes" para separar el catálogo de combos del de comandantes), WordPress expande la exclusión a TODAS las categorías hijas por defecto (`include_children` es `true` salvo que se declare lo contrario). Un combo etiquetado con una categoría hija legítima (p. ej. "CEDH", hija de "Commander") queda excluido aunque nunca tuviera la categoría padre. Diagnóstico: compara el conteo de un `WP_Query` idéntico con y sin el `tax_query` (`wp eval-file` con un script PHP tempora l cargando `WP_Query` directamente, más rápido y fiable que `wp eval` con comillas anidadas por SSH). Si el conteo sube al quitar el `tax_query`, revisa la jerarquía de categorías (`wp db query "SELECT term_id,name,parent FROM wp_term_taxonomy..."`) antes de asumir que es un problema de caché. Fix: añadir `'include_children' => false` al bloque del `tax_query`.
2. **Categorización incorrecta hecha por un subagente.** Un subagente que redacta un combo puede asignarle categorías de WordPress incorrectas (p. ej. "comandantes" en vez de o además de "combos") sin que ningún campo de su JSON de autoreporte lo refleje — el checklist de verificación de un subagente suele cubrir solo los 6 metadatos y las imágenes, no las categorías de WordPress. Tras cualquier tanda delegada, verifica `wp post term list <ID> category --field=slug` en CADA post nuevo y compáralo contra el patrón de posts ya correctos del mismo tipo; corrige con `wp post term remove/add <ID> category <slug>`.
3. **Orden inestable en `WP_Query` paginado.** Si una tanda de posts se publica en la misma sesión (fechas de creación separadas por segundos), un `orderby` sin desempate explícito puede devolver el mismo post en dos páginas de paginación distintas (y omitir otro) porque MySQL no garantiza orden estable ante valores de fecha casi idénticos. Fix preventivo: `'orderby' => ['date' => 'DESC', 'ID' => 'DESC']` en cualquier `WP_Query` de archivo que pagine.

Siempre haz backup del archivo de plantilla (`cp archivo.php archivo.php.bak-<timestamp>`) antes de tocar `page-combos.php` u otra plantilla de tema en producción, y corre `php -l` tanto en local como tras subir por `scp` antes de purgar caché.

## Delegación masiva a subagentes: patrón de timeout y recuperación

Cuando se delega la creación de N combos completos (contenido + 2 imágenes IA + 6 metadatos + categorías) a un subagente en batch de 3-4 posts, es MUY frecuente que el subagente haga timeout (límite de 600s) antes de terminar el último o los últimos posts de su lote — el cuello de botella real es la generación de imágenes IA (dos llamadas de ~30-40s cada una por post), no la redacción del texto. Patrón observado repetidamente: el subagente redacta el `post_content` completo y crea el post en WordPress, pero se queda sin tiempo justo antes de generar/subir las imágenes y aplicar los metadatos — el post queda a medias con el placeholder `__INNER_IMAGE_URL__` sin reemplazar, sin `_thumbnail_id`, sin `_toracles_editorial_type`, y con los 5 campos de Anatomía de Jugada vacíos (longitud 0), aunque las categorías `combos`/`combo-de-la-semana` sí suelen quedar bien asignadas.

Protocolo de recuperación (más rápido que relanzar desde cero, y preserva contenido ya bueno):
1. Tras cualquier timeout, NO asumas que no se creó nada: busca por título (`wp post list --post_status=draft --fields=ID,post_title | grep -i <nombre carta>`) antes de relanzar la tarea completa.
2. Si el post existe, diagnóstica exactamente qué falta con una sola pasada: `h1`, `<img>`, placeholders `__INNER__`/`__HERO__` sin reemplazar, `_thumbnail_id`, `_toracles_editorial_type`, longitud de los 5 metadatos de Disector, `wp post list --post_type=attachment --post_parent=<ID>` (si no hay adjuntos, faltan las 2 imágenes por completo).
3. Completa manualmente solo lo que falta: genera las imágenes con el provider `openai-codex` cargado vía `importlib.util.spec_from_file_location`, recorta a 1600x900, sube con `wp media import --porcelain`, asigna `_thumbnail_id`, sustituye el placeholder en el `post_content` ya escrito (nunca regeneres el cuerpo desde cero si ya es bueno), y escribe los 5 metadatos resumiendo el cuerpo ya verificado.
4. Para escribir metadatos con texto largo o con comillas/apóstrofes (común en prosa en español), `wp post meta update <ID> <key> '<valor>'` por SSH puede fallar por escaping del shell ("Too many positional arguments") o quedar vacío si usas un pipe a `-`. El método fiable es escribir un script PHP tempo con el valor dentro de un heredoc, subirlo con `scp`, y ejecutarlo con `wp eval-file /tmp/script.php` llamando a `update_post_meta()` directamente — evita por completo el escaping de argumentos de línea de comandos.
5. Cuando relances la parte fallida de un batch, divide en subagentes de 1-2 combos como máximo (no 3-4): un batch de 2 combos completos (texto+imágenes+metadatos) tarda típicamente 250-400s, dejando margen real antes del límite de 600s; un batch de 4 casi siempre lo agota.

## Nota de flujo probado (combo de 3 piezas, generación completa punta a punta)

El mismo flujo end-to-end funciona igual para combos de 3 piezas (ejemplo: Underworld Breach + Wheel of Fortune + Jeska's Will, post 1924): el único ajuste real es `_toracles_combo_pieces` con formato `Pieza 1/3 :: ... :: ...|Pieza 2/3 :: ... :: ...|Pieza 3/3 :: ... :: ...` y el título SEO en formato `Carta + Carta + Carta: combo Commander <identidad>`. El resto del pipeline (imágenes IA, publish --dry-run luego real, metadata vía heredoc SSH, verificación en la misma sesión) es idéntico al de 2 piezas.

## Nota de flujo probado (combo de 2 piezas, generación completa punta a punta)

Flujo verificado end-to-end para un combo nuevo desde cero (Gravecrawler + Phyrexian Altar, post 1912): leer post canónico de referencia por SSH (`wp post get <ID> --field=post_content` + `wp post meta list <ID>`) para copiar estructura exacta → escribir el `.md` con placeholder `__INNER_IMAGE_URL__` en el punto de tensión → generar ambas imágenes con el provider `openai-codex` cargado directamente vía `importlib.util.spec_from_file_location` (funciona sin pasar por el tool `image_generate`) → recorte-centro a 1600x900 con PIL → `scp` a `/tmp/` del servidor → `wp media import --porcelain` (devuelve el media ID directamente, sin parsear salida) → `wp post get <media_id> --field=guid` para la URL real → sustituir el placeholder en el `.md` fuente (nunca en el `_wp_clean.html` generado, se pierde en cada re-run) → `--dry-run` comprobando `title`/`slug` no vacíos → publish real `--status draft` → aplicar los 6 metadatos con heredoc `ssh ... bash -s <<'EOF'` en una sola llamada (mucho más rápido que 6 llamadas SSH separadas) → verificar en la MISMA sesión SSH: post_status, conteo de `<h1`, conteo de `deckbox_link`, conteo de `<img`, y `Card not found` vía `wp eval` con `apply_filters('the_content', ...)`. Todo el ciclo (2 imágenes IA + publish + metadata + verificación) cabe en menos de 10 llamadas de herramienta si se agrupan los pasos SSH.

## Voz y precisión

- El Oráculo enseña, advierte y corrige; los aprendices pueden plantear dudas plausibles dentro de la prosa sin convertir el texto en una obra de teatro ni insultar al lector.
- Usa uno o dos intercambios breves por entrada cuando aporten una corrección mecánica, de secuenciación o de nivel de mesa. Evita repetir `Oráculo:` y `Aprendiz:` como etiquetas en cada párrafo.
- Usa `ZASCA!!!` sólo después de una pregunta obvia o una respuesta incorrecta y sigue inmediatamente con la regla o el cálculo correcto; no lo uses como adorno ni más de dos veces por entrada.
- Prioriza claridad táctica sobre teatralidad. La voz TORACLES debe enseñar, divertir y reconocer los límites de la línea.
- Traduce la mecánica a consecuencias de mesa: prioridad, recursos, presión, coste de oportunidad y resiliencia.
- Usa `mazo` como término de casa salvo que un contexto literal exija otro término.
- No inventes turnos, precios, porcentajes, consistencia ni poder; formula las condiciones que hacen rápida o frágil a una línea.
- No todo combo es un bucle infinito estricto: si la línea consume un recurso finito en cada vuelta (biblioteca real del rival, cartas de un mazo, etc.) en vez de repetirse sobre un recurso renovable, etiquétalo "near-infinite"/"casi infinito" y explica la condición de salida real (deck-out, 0 de vida) — nunca lo llames "infinito" solo porque la fuente (Commander Spellbook, foros) usa esa palabra de forma informal. Comprueba el texto que la propia API de Commander Spellbook usa en `produces` ("Infinite X" vs "Near-infinite X") como señal objetiva antes de redactar.

## Criterios de cierre

Una entrada está lista únicamente si:

- [ ] Oracle, identidad y secuencia de cada carta están verificados.
- [ ] El H1 es editorial y los nombres de cartas permanecen presentes para SEO y consulta.
- [ ] El lector puede reproducir el bucle y entender su combustible, resultado y condición de salida.
- [ ] La interacción rival distingue ventanas y objetos de juego correctamente.
- [ ] Las referencias de carta se renderizan sin errores.
- [ ] HERO e imagen interna son IA, 16:9, coherentes, distintas, sin texto ni cartas reconocibles; los alt están presentes y captions vacíos.
- [ ] El estado remoto es `draft`, salvo autorización explícita para publicar.
- [ ] REST y navegador confirman el contenido que verá el lector.
- [ ] Los 5 metadatos de Anatomía de Jugada (`_toracles_editorial_type=combo`, `_toracles_combo_pieces`, `_toracles_combo_line`, `_toracles_combo_response_windows`, `_toracles_combo_resources`, `_toracles_combo_risks`) están escritos y el render en navegador muestra la plantilla canónica (kicker "ANATOMÍA DE JUGADA", índice de 6 anclas, tarjetas de piezas), no la plantilla de post genérica.
- [ ] Todas las menciones de carta usan `[mtg_card]Nombre[/mtg_card]`, nunca enlaces crudos `<a class="deckbox_link">` — el tooltip nuevo (hover, imagen normal de Scryfall, `max-width: 360px` en `candidate2.css`) solo se dispara sobre el shortcode. Un post con enlaces deckbox antiguos se ve inconsistente con el resto del sitio aunque el resto del canon esté aplicado.
- [ ] Tras publicar, el post aparece realmente en `/combos/` (revisa las páginas de paginación necesarias, no solo la primera) — verifica categorías de WordPress asignadas, no solo el estado `publish` y los 6 metadatos.
