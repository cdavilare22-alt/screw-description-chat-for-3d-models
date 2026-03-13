# Shop Reference: Mechanical + Electrical

This repo is now split into two clear sections.

## 1) Screw Sizes, 3D Modeling, and Measuring

Use this section for:

- Screw and tap sizes (inch + metric)
- Through-hole measurement with calipers
- Fusion 360 parameter-driven mount design
- Nut/bolt mounting details (nut traps, washer sizing, bolt length)
- Pipe/clamp sizing for printed mounts

Entry point:

- `docs/mechanical-fasteners-index.md`

Quick mechanical rules:

- Hole type first:
  - `Clearance hole`: screw passes through.
  - `Tapped hole`: threads are in this part.
  - `Pilot hole`: self-threading screw starts in material.
- Do not mix metric and inch threads even if they almost fit.
- Minimum tapped engagement starter rule:
  - Steel: `1.0 x diameter`
  - Aluminum/brass: `1.5 x diameter`
  - Plastics: `2.0 x diameter`
- Through-hole caliper workflow:
  1. Measure hole ID with calipers.
  2. Use inch or metric quick chart.
  3. Confirm against major diameter + clearance table.

Common values you will use:

- Metric tap drills:
  - `M3 x 0.5 -> 2.5 mm`
  - `M4 x 0.7 -> 3.3 mm`
  - `M5 x 0.8 -> 4.2 mm`
  - `M6 x 1.0 -> 5.0 mm`
- UNC tap drills:
  - `#6-32 -> #36 (2.71 mm)`
  - `#8-32 -> #29 (3.45 mm)`
  - `#10-24 -> #25 (3.80 mm)`
  - `1/4-20 -> #7 (5.11 mm)`
- Standard branch mounting screws you will see often:
  - Metric: `M3`, `M4`, `M5`, `M6`
  - Inch: `#6`, `#8`, `#10`, `1/4-20`

Pipe/clamp memory anchors (bare OD):

- `1/2 in pipe -> 0.840 in (21.34 mm)`
- `3/4 in pipe -> 1.050 in (26.67 mm)`
- `1 in pipe -> 1.315 in (33.40 mm)`
- `2 in pipe -> 2.375 in (60.33 mm)`
- Measure no-paint OD when possible; paint/coating can increase measured OD.

Detailed mechanical files:

- `SCREW_GUIDE.md`
- `docs/through-hole-caliper-quick-chart.md`
- `docs/through-hole-caliper-quick-chart-metric.md`
- `docs/fusion-360-nut-bolt-params.md`
- `docs/nut-and-bolt-mount-recipes.md`
- `data/common_tap_drills.csv`
- `data/clearance_hole_sizes.csv`

Mechanical visuals:

- `images/inch-metric-conversion.svg`
- `images/hole-selection-flow.svg`
- `images/panel-tools-overview.svg`

## 2) Wire, Cable, and Electrical Energy Basics

Use this section for:

- AWG sizes and ampacity reference
- Understanding amps, volts, watts, and basic power math
- Common voltage system references
- Quick conductor selection starting points

Entry point:

- `docs/electrical-wire-index.md`

Quick electrical terms:

- **Voltage (V):** electrical pressure
- **Current (A):** flow
- **Power (W):** electrical work rate
- Core formula: `W = V x A`

Quick electrical formulas:

- `A = W / V`
- `V = W / A`
- `Vdrop = I x R`

Examples:

- `1200W @ 120V = 10A`
- `1200W @ 240V = 5A`
- Same power at higher voltage means lower current.

Wire gauge memory points (U.S. copper branch-circuit starters):

- `14 AWG -> 15A`
- `12 AWG -> 20A`
- `10 AWG -> 30A`

30A quick answer:

- Typically `10 AWG copper` (or `8 AWG aluminum` in many cases), then confirm final code/derating conditions.

Detailed electrical files:

- `docs/electrical-basics-wire-sizing.md`
- `data/us_copper_awg_ampacity_quick_chart.csv`
- `data/awg_common_sizes_reference.csv`
- `data/electrical_power_formula_cheatsheet.csv`
- `data/common_voltage_levels_us_quick_reference.csv`
- `images/electrical-basics-cheatsheet.svg`

## Scope and Safety

These files are practical field references for design and planning.
Final mechanical and electrical decisions must be verified against actual hardware specs, equipment ratings, and local code requirements.
