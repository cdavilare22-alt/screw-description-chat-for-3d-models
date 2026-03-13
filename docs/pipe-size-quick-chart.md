# Pipe Size Quick Chart (Clamp Buying + Caliper Workflow)

This is the simple version for mount design and online clamp ordering.

## Key Idea

- **NPS (nominal pipe size) is not measured OD.**
- Clamps are usually sold by **nominal pipe size label** (`1/2 in pipe clamp`, `1 in pipe clamp`, etc.).
- Your calipers read **actual OD**, and paint/coating makes OD read larger.

## Fast Memory Anchors (Bare Pipe OD)

- `1/2 in pipe -> 0.840 in OD (21.34 mm)`
- `3/4 in pipe -> 1.050 in OD (26.67 mm)`
- `1 in pipe -> 1.315 in OD (33.40 mm)`
- `2 in pipe -> 2.375 in OD (60.33 mm)`

## No-Paint vs Painted Measurement Rule

1. If possible, measure a bare/unpainted section.
2. If paint/powder coat is present, measured OD may be about `+0.2 to +0.8 mm` larger.
3. Use `data/caliper_to_pipe_clamp_size_crosswalk.csv` to map measured OD to clamp label.
4. If you are near range boundaries, choose adjustable/cushioned clamps.

## What to Use in CAD

- For clamp seat diameter, start from **actual OD** (bare value when known).
- For pass-through holes around pipe:
  - Close fit: OD + `0.3 to 0.5 mm`
  - Normal fit: OD + `0.8 to 1.2 mm`
- For printed clamps, add printer compensation as needed.

## Notes

- Pipe **schedule changes wall thickness and ID**, but OD is fixed for each NPS.
- For clamp purchases, search by nominal label (example: `1 in pipe clamp`) not by measured OD only.

## Data Files

- `data/pipe_nominal_to_actual_od_quick_chart.csv`
- `data/caliper_to_pipe_clamp_size_crosswalk.csv`
