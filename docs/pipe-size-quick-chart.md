# Pipe Size Quick Chart (No Headaches)

This is the simple version for design work and memory:

- **NPS (nominal pipe size) is not the measured OD.**
- For mounts/clamps, care about **actual outside diameter (OD)**.

## Fast Memory Anchors

- `1/2 in pipe -> 0.840 in OD (21.34 mm)`
- `3/4 in pipe -> 1.050 in OD (26.67 mm)`
- `1 in pipe -> 1.315 in OD (33.40 mm)`
- `2 in pipe -> 2.375 in OD (60.33 mm)`

## What to Use in CAD

1. Model around **actual OD** from table.
2. For pass-through holes, start with:
   - Close fit: OD + `0.3 to 0.5 mm`
   - Normal fit: OD + `0.8 to 1.2 mm`
3. For printed clamps, add extra clearance if your printer tends to undersize holes.

## Notes

- Pipe **schedule changes wall thickness and inside diameter**, but OD stays fixed for each NPS.
- This sheet is for quick mount design and shop decisions.

## Data File

- `data/pipe_nominal_to_actual_od_quick_chart.csv`
