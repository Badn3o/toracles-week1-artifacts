# Skills y canon — TORACLES Combo Pipeline

Última actualización: 2026-09-28 (Tramo 6 Multicolor completo y publicado)

## Contenido

- `toracles-combo-entry-canon/` — skill Hermes completa (SKILL.md + references/) que define el canon
  editorial para las entradas de "Combo de la Semana" de TORACLES: estructura del artículo, metadatos
  de "Anatomía de Jugada", generación de imágenes IA, verificación Oracle/Scryfall, y protocolo de
  publicación y auditoría adversarial.

## Cambios de esta ronda (Tramo 6 Multicolor, 16 combos)

Actualizaciones aplicadas al canon tras la auditoría adversarial de los 16 combos multicolor:

1. **Distinción habilidad de maná vs. disparada normal** — nueva regla explícita: nunca describir una
   mana ability como "contrarrestable" o que "va a la pila". Caso real corregido: Kinnan, Bonder Prodigy
   (post 1989) describía su duplicación de maná como respondible, cuando la ruling oficial dice
   "It doesn't use the stack and can't be responded to".

2. **No asumir requisitos de "equipar/adjuntar" sin verificar Oracle text letra por letra** — caso real
   corregido: Nim Deathmantle (post 1977) exigía como prerrequisito estar "equipado" a Breya con coste de
   Equip {4} previo; el Oracle text real muestra que el trigger es independiente y el attach ocurre como
   parte de la resolución del propio disparo.

3. **Sección nueva: protocolo de recuperación de timeouts de delegación masiva** — documenta el patrón de
   fallo observado repetidamente al delegar 3-4 combos completos (texto + 2 imágenes IA + 6 metadatos) a
   un solo subagente: casi siempre agota el límite de 600s en la fase de generación de imágenes, dejando
   el post con placeholder de imagen sin reemplazar y metadatos vacíos. Incluye protocolo de diagnóstico y
   reparación manual sin necesidad de relanzar el combo entero desde cero.

## Combos publicados esta ronda (Tramo 6 — Multicolor, 16 entradas)

| Franja | Post ID | Combo |
|---|---|---|
| 2 colores | 1989 | Kinnan, Bonder Prodigy + Basalt Monolith |
| 2 colores | 1992 | Aurelia, the Warleader + Helm of the Host |
| 2 colores | 2007 | Niv-Mizzet, Parun + Curiosity |
| 2 colores | 2021 | Squee, the Immortal + Food Chain |
| 3 colores | 1968 | Kaalia of the Vast + Master of Cruelties |
| 3 colores | 1973 | Nekusar, the Mindrazer + Peer into the Abyss |
| 3 colores | 1974 | Derevi, Empyrial Tactician + Emiel the Blessed + Gaea's Cradle |
| 3 colores | 1975 | Apex Altisaur + Wrathful Raptors + Akroma's Will |
| 4 colores | 1976 | Atraxa, Praetors' Voice + Magistrate's Scepter + Contagion Engine |
| 4 colores | 1977 | Nim Deathmantle + Ashnod's Altar + Breya, Etherium Shaper |
| 4 colores | 1978 | Retreat to Coralhelm + Llanowar Scout + Boros Garrison |
| 4 colores | 1980 | Miirym, Sentinel Wyrm + Bladewing the Risen + Terror of the Peaks |
| 5 colores | 1962 | Ulalek, Fused Atrocity + Echoes of Eternity + Glaring Fleshraker |
| 5 colores | 1963 | The World Tree + Maskwood Nexus |
| 5 colores | 1964 | Najeela, the Blade-Blossom + Derevi, Empyrial Tactician |
| 5 colores | 1965 | Hibernation Sliver + Morophon, the Boundless + Syphon Sliver + Lavabelly Sliver |

Todos publicados (`post_status=publish`), auditados adversarialmente (2 hallazgos GRAVE corregidos: 1977,
1989), y verificados en vivo en https://toracles.com/combos/ (43 combos únicos totales, sin duplicados).
