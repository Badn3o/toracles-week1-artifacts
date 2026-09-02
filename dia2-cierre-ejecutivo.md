# Día 2 — Cierre ejecutivo

Fecha:
2026-09-02

---

## Veredicto sobre viabilidad mínima

Sí hay viabilidad mínima para `mtgdeckbuilding.com` como producto estrecho de utilidad.

No hay viabilidad aceptable para publicar la beta si depende de la base SQLite actual en `/mnt/e` y de la app pública tal como está hoy.

Traducción operativa:
- la idea de producto pasa
- la forma actual de servir datos no pasa

---

## Decisión de almacenamiento

Decisión cerrada del Día 2:
- no usar `/mnt/e/AIProyects/MTGJSON/data/mtg_analytics.db` como base operativa pública
- sí usar SQLite en filesystem Linux nativo para la beta, con base separada del prototipo y preferencia por snapshot/subset público
- Postgres no se impone todavía como requisito de semana 1

Esto cierra el Gate 1 a nivel de decisión.
No lo cierra todavía a nivel de implementación.

---

## Qué pasa al Día 3

El Día 3 debe convertir esta decisión en arquitectura mínima concreta:
- dónde vive la API
- dónde vive el frontend
- dónde vive la base operativa pública
- qué endpoints quedan públicos
- qué endpoints quedan internos
- cómo se separa ETL interno de producto público
- qué configuración mínima hace falta para levantar la beta

---

## Blockers reales

1. Riesgo real de SQLite en `/mnt/e`
- ya hubo `disk I/O error`
- la estabilidad observada fue solo en readonly/immutable

2. Superficie pública demasiado abierta
- CORS `*`
- sin auth
- sin rate limiting
- `POST /api/sync` expuesto

3. Mezcla entre panel operativo y producto público
- la app actual mezcla rankings, búsqueda y ETL manual

4. Coste no cerrado de algunos endpoints
- `suggest` hace fuzzy sobre nombres cargados desde la tabla de cartas
- detalle de carta puede arrastrar histórico completo

---

## Checklist de cierre

- [x] Existe informe técnico principal del Día 2
- [x] Existe decisión escrita de almacenamiento para beta
- [x] Existe tabla ejecutiva de reutilización
- [x] Existe cierre ejecutivo del Día 2
- [x] La decisión sobre `/mnt/e` queda explícita
- [x] No se declara resuelto el problema de `/mnt/e`
- [x] No se toca producción, DNS ni WordPress
- [x] No se migra la base realmente
- [x] Se deja listo el paso al Día 3

---

## Veredicto final del Día 2

Día 2 completado: sí.

Condición de ese cierre:
- completado como auditoría y decisión
- no completado como remediación técnica todavía

Go para Día 3:
- sí, porque ya existe una decisión explícita sobre almacenamiento para beta
- con la obligación de diseñar una arquitectura que no dependa de `/mnt/e` como base pública