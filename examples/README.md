# Example Modules

Two kinds of examples: **local** (in this folder, framework-styled, engine-verified) and **external** (full production modules in their own repos, each with its own revision history).

## Local examples (open in your browser — no install)

| File | What it shows |
|---|---|
| [`../template/ephemeral-template.html`](../template/ephemeral-template.html) | The teaching skeleton: simply supported beam check (bending/shear/deflection, NDS-style ASD). Deliberately minimal — this is the file an AI copies from. Includes the branding module: firm name/address fields, drag-drop **logo**, and a live **brand color picker** that re-skins the whole deliverable. |
| [`door-window-wind-calc.html`](door-window-wind-calc.html) | A "minimalist wind calc": ASCE 7-22 Ch. 30 C&C wall Zones 4/5 pressures for doors/windows. Engine ported from the production repo below and verified against its two documented test cases (13/13 checks). Shows the letter-generator-adjacent style: zone diagram, log-interpolated GCp, 16 psf minimum flagging, ult + ASD table. |
| [`criteria-opinion-letter/criteria-opinion-letter.html`](criteria-opinion-letter.html) | A **document** module rather than a calc: a criteria-and-opinion letter (worked example — stand-alone off-grid solar lighting). No engine, no numbers — it is here to show print-exact pages, an auto-fit that measures the laid-out sheet instead of trusting font metrics, four swappable SVG figure archetypes, and the same JSON input state as the calc modules. Structure (purpose → numbered criteria → opinion bound to the criteria → limitations → figure) transfers to any classification or applicability letter. See [`criteria-opinion-letter.md`](criteria-opinion-letter.md). |

## External production modules (oasiseng)

| Module | Domain | Repo |
|---|---|---|
| Door/Window Wind Pressure (ASCE 7-22) | C&C wall zones 4/5, product-approval comparisons | [oasiseng/ASCE-7-22-Door-Window-Wind-Pressure-Calculator](https://github.com/oasiseng/ASCE-7-22-Door-Window-Wind-Pressure-Calculator) — note it ships its own `SKILL.md` and in-code verification cases |
| Fence Wind Calc | Freestanding wall/fence, Fig. 29.3-1 force coefficients, member + post checks | [oasiseng/windcalculations.com → fence-wind-calc](https://github.com/oasiseng/windcalculations.com/tree/main/fence-wind-calc) |
| Pergola Wind Calc | Open structure wind | [oasiseng/windcalculations.com → pergola-wind-calc](https://github.com/oasiseng/windcalculations.com/tree/main/pergola-wind-calc) |
| Canopy Wind Calc | Attached canopy pressures | [oasiseng/windcalculations.com → canopy-wind-calc](https://github.com/oasiseng/windcalculations.com/tree/main/canopy-wind-calc) |
| Glass Railing | Guard/glazing checks | [oasiseng/windcalculations.com → glass railing](https://github.com/oasiseng/windcalculations.com/tree/main/glass%20railing) |
| Wind Speed Tool | Site wind-speed lookup | [oasiseng/windcalculations.com → wind-speed-tool](https://github.com/oasiseng/windcalculations.com/tree/main/wind-speed-tool) |

## Contributing a module

1. Build from the template following [`../skill/ephemeral-eng/SKILL.md`](../skill/ephemeral-eng/SKILL.md).
2. 2. Complete [VERIFICATION.md](../VERIFICATION.md) and **include the worked hand-calc example**. *Document modules with no engine (e.g. letter generators) instead document their guardrails and page-fit behaviour — see `criteria-opinion-letter.md`.*
3. Open a PR adding a row. Modules without a verification example are not listed.

## NOTE

Modules are not limited to calculations — the same single-file pattern generates sealed documents (letters, opinions, transmittals) with print-exact pages and live figures. See the criteria-letter example.
