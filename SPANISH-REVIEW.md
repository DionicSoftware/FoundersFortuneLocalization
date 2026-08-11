# Spanish translation — review notes

Written 2026-08-11 alongside the pass that filled in the 229 missing Spanish strings.
The LatAm leftovers, the two typos and the `hermanoHermana` gender-dictionary bug that
this pass turned up have all been fixed in the same commit; what remains below is the
dialect evidence, the terminology splits nobody has unified yet, and the reasoning
behind the new strings.

## Dialect: European Spanish

The existing translation is **European (Spain) Spanish**, decisively:

| Marker | Spain form | Count | LatAm form | Count |
|---|---|---:|---|---:|
| potato | `patata` | 11 | `papa` | 0 |
| strawberry | `fresa` | 8 | `frutilla` | 1 → 0 |
| to annoy | `enfadar` | 5 | `enojar` | 1 → 0 |
| mouse (device) | `ratón` | ✓ | — | — |
| costs | `costes` | ✓ | `costos` | 0 |

`coger` is also used freely, which a Latin American translator would avoid.
All 229 new strings were written in this style.

## Note on `piso` vs `suelo`

The walking-surface sense of *floor* was normalised to **`suelo`** in this pass, because
in Spain `piso` means *flat/apartment*. The **storey** sense was deliberately left as
`piso`, where it is perfectly idiomatic in Spain:

- `uiGeneral.json :: floorUp` / `floorDown` — "Subir/Bajar un piso"
- `uiIngame.json :: switchFloors` / `switchFloorsDescription`
- `uiIngame.json :: constructionCostsAdditionalOnFloor`

If a future pass wants these uniform, `planta` is the more formal Spain term for a
building level ("la primera planta").

## Terminology that is split in the existing translation

Not wrong, just inconsistent. Listed in case a future pass wants to unify.

- **Storage**: `almacén` (23) / `depósito` (16) / `almacenamiento` (6). The new strings
  use `almacenamiento` for the UI panel (matching the existing `storage` key) and
  `el almacén` in running prose.
- **Shelf**: `estante` (39) / `estantería` (27), sometimes for the same object.
- **Capitalisation of object names** in `gameObjects.json`: 126 multi-word names use
  Title Case ("Gabinete de Pociones Curativas"), 168 use sentence case ("Cómoda simple
  de madera"). Spanish does not title-case, so sentence case is the correct default;
  the new entries use it, except `gardenSoil` → "Tierra para Flores" which deliberately
  matches its `farm*Soil` siblings ("Tierra para Tomates", "Tierra para Patatas").
- **Colonist vs villager**: the English source mixes *colonist* and *villager* for the
  same entity; Spanish has `colono` and `aldeano`. The new `multipleVillagerSelection`
  uses `colonos`, since it selects the player's own colonists.

## Decisions made for the new strings

Recorded so a later reviewer doesn't have to re-derive them.

- **Quotation marks** — `quotation_start` / `quotation_end` are `«` / `»` (RAE-correct
  for Spain; no inner spaces, unlike the French entry). The 16 painting titles use the
  same marks. If the UI font ever renders these badly, all 18 strings need to change
  together.
- **Hobby names** — the *Woodworking* and *Masonry* hobbies carve statues (see
  `HobbyModule.cs`, `lowSkilledWoodworkingProducts` etc.), so they are
  **"Talla en madera"** and **"Cantería"**, not the `Carpintería` / `Albañilería` used
  by `tech.json` and `professions.json` for the genuinely different profession skills.
  Interactions follow: `DoWoodworking` → "Talla la madera", `DoMasonry` → "Talla la piedra".
- **Hobby (noun)** → **`afición`** ("Aficiones", "Es su afición principal"). `hobby` is
  also current in Spain, but `afición` reads better in a UI and inflects cleanly.
- **Painting (noun)** → **`cuadro`** for the physical object (`RemovePainting` → "Retira
  el cuadro", `paintingCompleted` → "Cuadro terminado"), **`pintura`** for the activity
  (`hobbyTitle_Painting` → "Pintura"). This is the natural Spanish split. Note the
  pre-existing `paintingGoodVibes` → "Pintura de Buenas Vibras" uses `pintura` for an
  object; left alone.
- **Localised references** — `paintingHorse` "Bullseye" → **"Perdigón"** (the horse's
  name in the Spain dub of *Toy Story*); `paintingPanorama` "Everything the light
  touches" → **"Todo lo que ilumina el sol"** (the Spain dub line from *The Lion King*).
  Both would need the Latin American variants (*Tiro al Blanco*, *todo lo que toca la
  luz*) if the translation ever forks by region.
- **Achievement labels** — `normalAchievements` and `challengerAchievement` end in a
  colon, because `AchievementHandler.GetAchievementStatusTitle` concatenates them with
  `available`/`disabled`; without the colon "Logros normales Desactivado" would not
  agree in number. French and Portuguese solved it the same way.
- **`trapUses`** — English is "Number of times trap can be reset", rendered as
  `LABEL: 3/5`. Shortened to "Usos restantes de la trampa" to fit, matching what German
  and Czech did.
- **Rations** — `smallRationsTooltip_Title` etc. use "Raciones de comida pequeñas /
  medianas / grandes", aligning with `foodRations` → "Raciones de comida". The existing
  `thoughts.json` titles use the other word order ("Pequeñas raciones de comida");
  both are correct Spanish, so they were left as they are.

## Coverage at time of writing

| Area | Status |
|---|---|
| 24 top-level `.json` + `mods/` (2) | 2935 / 2935 entries |
| `achievements/1104330_loc_spanish.vdf` | 41 / 41 tokens |
| `websites/steam.md` | all 16 sections present |
