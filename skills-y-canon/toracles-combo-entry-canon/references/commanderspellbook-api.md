# Commander Spellbook — obtención y verificación de datos de combos

Receta verificada para listar los combos más buscados por identidad de color y verificar sus componentes antes de redactar (paso 1 del canon). Todo funciona sin autenticación.

## API REST (no GraphQL)

- Base: `https://backend.commanderspellbook.com`
- Endpoint principal: `GET /variants/` con parámetros:
  - `q=identity:wu` — filtro de búsqueda. La sintaxis es `identity:<colores>`; `ci:...` y `ci:mono-white` devuelven HTTP 400.
  - `ordering=-popularity` — orden server-side por popularidad (contador de búsquedas/usos en la plataforma; el mejor proxy objetivo de "más buscado"). Otros orderings documentados (`-numberOfFindings`) se aceptan silenciosamente pero no ordenan de verdad: verifica siempre con el valor `popularity` del primer resultado.
  - `groupByCombo=true` — una variante por combo.
  - `limit` (max 100) + `offset` para paginar.
- Cada variante trae: `uses` (cartas con `zoneLocations` y `mustBeCommander`), `produces` (features resultantes), `requires` (templates), `notablePrerequisites`, `easyPrerequisites`, `manaNeeded`, `bracketTag`, `prices`, `identity`, `popularity`. Úsalos para la ficha táctica y los requisitos sin re-consultar.

## Deduplicación: clave por conjunto de cartas, no por `of[0]`

`of` es una LISTA de combo ids y `variant.id` no es el id de combo. Deduplicar por `of[0]` mezcla combos distintos bajo la misma clave cuando dos variantes comparten el primer id. Deduplica siempre por `frozenset(nombres de cartas de uses)`: es la identidad real de una línea de juego.

## Identidad exacta

`identity:wu` del filtro devuelve variantes cuya identidad ESTÁ DENTRO de wu (incluye monocolor). Si el ranking es por identidad exacta, filtra localmente comparando el campo `identity` de la variante con el valor exacto.

## Reglas editoriales de selección (para tandas "top N por color")

- Máximo 1 combo por familia de cartas: sin esta regla, un solo permanente popular genera 3-4 entradas casi idénticas (misma carta + distintos aceleradores de maná) y la ola se canibaliza a sí misma.
- En multicolor, 1 combo por par de colores: cubre WU/UB/BR/RG/GW antes de repetir par.
- Registra la fecha de captura si citas `popularity`: es un contador vivo, no un hecho estable.

## Patrón de extracción completo

```python
import json, urllib.request, urllib.parse

def get(path, **params):
    url = "https://backend.commanderspellbook.com" + path + "?" + urllib.parse.urlencode(params)
    req = urllib.request.Request(url, headers={"User-Agent": "Mozilla/5.0", "Accept": "application/json"})
    with urllib.request.urlopen(req, timeout=60) as r:
        return json.loads(r.read().decode())

def top_por_identidad(idt, n=40):
    rows, seen, offset = [], set(), 0
    while len(rows) < n:
        d = get("/variants/", q=f"identity:{idt}", groupByCombo="true",
                ordering="-popularity", limit=100, offset=offset)
        if not d.get("results"):
            break
        for v in d["results"]:
            key = frozenset(u["card"]["name"] for u in v["uses"])
            if key in seen:
                continue
            seen.add(key)
            rows.append({
                "cards": sorted(key),
                "combo_ids": v["of"],
                "popularity": v.get("popularity"),
                "identity": v.get("identity"),
                "produces": [p["feature"]["name"] for p in v.get("produces", [])],
                "requires": [r.get("template", {}).get("name") for r in v.get("requires", []) if r.get("template")],
                "notable_prereqs": v.get("notablePrerequisites") or [],
                "bracketTag": v.get("bracketTag"),
                "prices": v.get("prices"),
            })
        offset += 100
    return rows[:n]
```

## Verificación Scryfall por lote

```python
def scryfall_collection(names):
    req = urllib.request.Request(
        "https://api.scryfall.com/cards/collection",
        data=json.dumps({"identifiers": [{"name": n} for n in names]}).encode(),
        headers={"Content-Type": "application/json", "User-Agent": "TORACLES-editorial/1.0",
                 "Accept": "application/json"})
    with urllib.request.urlopen(req, timeout=60) as r:
        d = json.loads(r.read().decode())
    # d["data"]: cartas con name/color_identity/legalities; d["not_found"]: sin match
    return {c["name"]: c for c in d.get("data", [])}, d.get("not_found", [])
```

Verifica por carta: `legalities["commander"] == "legal"`, `color_identity` compatible con la identidad declarada por Spellbook, y nombre exacto (split en ` //` para anversos dobles). Ejecuta la verificación DESPUÉS de fijar la selección final, no sobre el ranking crudo: así el lote es pequeño y cubre exactamente lo que se publicará.
