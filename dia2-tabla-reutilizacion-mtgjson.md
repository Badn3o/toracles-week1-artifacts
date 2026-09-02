# Día 2 — Tabla ejecutiva de reutilización de MTGJSON

Fecha:
2026-09-02

| Pieza actual | Reutilizable ahora | Bloquear / rehacer / posponer |
|---|---|---|
| `database.py` con esquema `meta`, `sets`, `cards`, `card_legalities`, `prices_raw`, `price_rankings` | Sí, como base del modelo de datos del MVP | Mantener; no exponer `prices_raw` sin criterio |
| Tabla `cards` | Sí | Mantener |
| Tabla `sets` | Sí | Mantener |
| Tabla `card_legalities` | Sí | Mantener |
| Tabla `price_rankings` | Sí, es la pieza más útil para MVP de rankings | Mantener |
| Tabla `prices_raw` completa | Solo parcialmente, como origen interno para detalle y analytics | Bloquear como superficie pública directa |
| `etl.py` | Sí, como base de ingestión interna | Rehacer después solo si hay necesidad; no exponer como parte pública |
| `analytics.py` | Sí, aporta valor directo a rankings | Mantener |
| `sync_service.py` | Parcialmente | Bloquear la exposición pública del trigger |
| `scheduler.py` | Parcialmente, para operación interna | Posponer como pipeline serio de producción |
| `config.py` | Sí | Mantener, pero separar config pública/operativa más adelante |
| `GET /api/status` | Sí | Mantener con posible poda de campos operativos |
| `GET /api/sets` | Sí | Mantener |
| `GET /api/cards` | Sí, con foco MVP | Mantener y medir coste |
| `GET /api/rankings` | Sí, P0 claro | Mantener |
| `GET /api/cards/{uuid}` | Sí, pero con cautela | Rehacer o adelgazar payload si el histórico completo pesa demasiado |
| `GET /api/suggest` | Sí, funcionalmente | Rehacer más adelante por coste potencial del fuzzy actual |
| `POST /api/sync` | No | Bloquear en beta pública |
| `index.html` estructura general | Sí | Mantener como scaffold |
| Pestaña `Top Subidas / Bajadas` | Sí | Mantener |
| Pestaña `Buscador de Cartas` | Sí | Mantener |
| Pestaña `Estado ETL` | No para público | Bloquear o mover a admin interno |
| Botón `Sincronizar Ahora` | No para público | Bloquear |
| Modal de detalle de carta | Sí | Mantener con payload más controlado si hace falta |
| `static/js/api.js` | Sí | Mantener, pero revisar estrategia `getApiUrl()` en despliegue real |
| `static/js/app.js` | Sí, parcialmente | Recortar lo ligado a ETL público |
| `static/js/autocomplete.js` | Sí | Mantener, con optimización futura del backend |
| `static/css/styles.css` | Sí | Mantener |
| CORS abierto a `*` | No | Rehacer antes de exposición pública |
| Base SQLite en `/mnt/e` | No | Bloquear como base pública |
| Operación con WAL sobre esa ubicación | No | Bloquear |

## Lectura rápida

Reutilizar ahora:
- modelo de datos útil
- rankings
- búsqueda
- detalle de carta
- scaffold frontend

Bloquear ya:
- `/mnt/e` como base pública
- `POST /api/sync`
- pestaña ETL pública
- CORS abierto

Posponer:
- migración a Postgres
- endurecimiento total del scheduler
- optimización profunda del fuzzy search si antes no valida el MVP