# Día 1 — CTAs candidatos TORACLES → mtgdeckbuilding.com

> IMPORTANTE: estos CTAs están en estado de especificación / bosquejo. No están implementados todavía. Su activación queda sujeta a los gates técnicos de la semana 1 (Gate 1, 2, 3 y 4). No se publican hasta que el destino técnico sea fiable.

---

## 1. Regla general de uso

1. TORACLES enlaza al producto solo cuando añade utilidad inmediata al lector.
2. TORACLES no enlaza por rutina ni por relleno.
3. TORACLES enlaza a una URL útil concreta del producto, no siempre a la home.
4. El CTA no debe competir con el H1 ni la intención principal de la página.
5. mtgdeckbuilding.com enlaza de vuelta a TORACLES cuando el usuario necesita contexto editorial, no solo dato.

---

## 2. CTAs candidatos (sin implementar)

| CTA | Texto candidato | URL destino candidata | Condición de uso |
|---|---|---|---|
| CTA-1 | Ver staples en ranking dinámico | `/rankings/staples-commander` | Páginas: Staples por color, tierras, cartas que suben/bajan |
| CTA-2 | Consultar esta carta | `/cards/{id-artista-o-set}` | Páginas: combos, precons, upgrades, fichas de carta dentro de guías |
| CTA-3 | Filtrar cartas de Commander | `/search?format=commander` | Páginas: guías de color, commander de la semana, académia |

---

## 3. 5 superficies editoriales candidatas (compatibles)

1. **Staples por color** — Encaje alto. CTA-1 y CTA-2 aplicables.
2. **Artículos sobre tierras y base de maná** — Encaje alto. CTA-1 y CTA-3 aplicables.
3. **Piezas sobre cartas que suben o bajan** — Encaje muy alto. CTA-1 y CTA-2 aplicables.
4. **Guías de color y guías de comandante** — Encaje medio-alto. CTA-3 aplicable.
5. **Precons y upgrades** — Encaje alto. CTA-2 aplicable.

---

## 4. Reglas de cuándo NO enlazar

- Cuando el destino aún depende de la base SQLite en `/mnt/e` con riesgo conocido de `disk I/O error` (Gate 1 abierto).
- Cuando la superficie pública del producto aún no tiene cierre mínimo de CORS y endpoints (Gate 3 abierto).
- Cuando la frontera SEO entre dominios no está firmada (Gate 4 abierto).
- Siempre que el CTA compita con el H1 o la intención principal de la página.
- En páginas cuya intención es puramente editorial y donde un enlace a utilidad robaría coherencia al texto.
- Si el ranking o la ficha de carta aún no han sido medidos con datos reales (Gate 2 abierto).

---

## 5. KPI para validación de CTAs (semana 2)

- TORACLES: clics salientes cualificados hacia mtgdeckbuilding.com.
- mtgdeckbuilding.com: visitas a landing + uso del CTA principal + primeras acciones útiles dentro del MVP.
