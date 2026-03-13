# Intern Quickstart

If you are not sure what hole to drill, follow this exactly:

1. Read the screw label (example: `M5x0.8` or `#10-24`).
2. Ask: does this part need threads?
   - Yes -> use `data/common_tap_drills.csv`
   - No -> use `data/clearance_hole_sizes.csv`
3. Check part material:
   - For aluminum/plastic, make sure enough thread depth exists (`data/material_thread_engagement.csv`).
4. If the part is very thin, switch to a nut/insert/rivnut.
5. For printed parts, test one coupon before printing the full assembly.

Quick rule: if uncertain, pick normal-fit clearance holes for pass-through and standard tap drills for threaded holes.
