# Día 1 — Cierre ejecutivo

---

## Decisiones cerradas

1. **Reparto de roles por dominio.**
   - TORACLES = editorial, SEO, autoridad, contenido evergreen.
   - mtgdeckbuilding.com = producto/herramientas, utilidad interactiva, datos, exploración práctica.

2. **Promesa operativa de mtgdeckbuilding.com (versión Día 1).**
   - “Una herramienta práctica para Commander que permite explorar cartas, consultar rankings y usar datos útiles para construir mejor tus mazos.”
   - Incluye: búsqueda, rankings, datos útiles, foco Commander.
   - Excluye: comunidad, deckbuilder completo, red social, colección personal, suite total de MTG.

3. **Tabla operativa de dominios aprobada.**
   - 3 columnas: vive en TORACLES | vive en mtgdeckbuilding.com | no entra en MVP.

4. **CTAs candidatos especificados.**
   - 3 CTAs candidatos con textos, URLs destino y condiciones de uso.
   - Ningún CTA está implementado.

5. **Reglas de CTA entre dominios congeladas.**
   - Enlaces deben aportar utilidad inmediata. No enlaces por rutina.
   - Nunca competir con el H1 ni la intención principal de la página.

6. **Exclusiones del MVP explicitadas.**
   - Ver sección “Exclusiones del MVP”.

---

## Exclusiones del MVP (lista cerrada)

- Red social de mazos
- Login / usuarios / cuentas
- Guardado de mazos
- Comentarios sociales, follows, favoritos compartidos
- Clon de Moxfield / Archidekt / TopDecked
- Monetización compleja desde el día 1
- Newsletter como pieza central
- App móvil / PWA avanzada
- Internacionalización
- Páginas SEO programáticas masivas antes de validar el producto mínimo
- Importación/exportación avanzada de listas
- Comentarios o funciones sociales
- Marketplace
- Recomendaciones automáticas completas de deckbuilding
- Builders competitivos tipo Moxfield
- Páginas SEO masivas por combinatoria
- Integración con tienda sin flujo claro

---

## Preguntas que pasan al Día 2

1. ¿Qué parte de MTGJSON sirve de verdad al MVP definido en el Día 1?
2. ¿Qué parte del prototipo es solo local/no publicable por el riesgo de SQLite en `/mnt/e`?
3. ¿Qué subset de datos es suficiente para una beta estrecha sin depender de la base completa?
4. ¿Qué arquitectura mínima soporta el reparto de dominios sin romperlo?
5. ¿Qué endpoints P0 (`/api/status`, `/api/cards`, `/api/rankings`, `/api/cards/{uuid}`, `/api/suggest`) están medidos con datos reales?

---

## Veredicto: Día 1 completado ✅

Se cumplieron todos los criterios de cierre del Día 1:

- [x] Existe una decisión explícita de roles por dominio.
- [x] Existe una tabla operativa de 3 columnas (vive en TORACLES / vive en mtgdeckbuilding.com / fuera de MVP).
- [x] Existen 3 CTAs candidatos sin implementar.
- [x] Existen 5 superficies editoriales compatibles con el puente.
- [x] Existen reglas de cuándo NO enlazar.
- [x] Existe una lista explícita de exclusiones del MVP.
- [x] No se ha tocado producción, WordPress, DNS, MTGJSON (solo lectura de contexto) ni se ha implementado código de producto.
