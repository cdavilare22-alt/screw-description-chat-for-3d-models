# Nut-and-Bolt Mount Recipes (No Heat Inserts)

These patterns are intended for 3D printed mounts that use through-holes, washers, and nuts.

## 1) Flat Bracket Mount

Use for attaching a printed bracket to a flat surface.

- Hole type: through-hole in printed part.
- Hardware: bolt + washer under head + washer under nut + hex nut.
- Printed part tips:
  - Boss OD around hole: at least `2.0 x bolt diameter`.
  - Wall near hole: at least `1.5 x bolt diameter`.
  - Fillet at boss base to reduce cracking.

## 2) Standoff Mount

Use for spacing boards/sensors from a wall or plate.

- Through-hole in mount leg and mating plate.
- Add a hex nut trap pocket when back-side access is limited.
- Keep standoff wall thick enough to prevent splitting:
  - Min wall: `>= 2.0 mm` for M3/M4
  - Min wall: `>= 3.0 mm` for M5/M6

## 3) Slot-Adjustable Mount

Use when alignment is uncertain.

- Replace round hole on one side with slot:
  - Slot width = normal clearance hole size.
  - Slot length = width + adjustment travel.
- Add washer pockets if you need flush hardware.

## 4) Hinge or Pivot Mount

Use shoulder-like stack: printed ear -> washer -> moving part -> washer -> nut.

- Use locknut or threadlocker for vibration.
- Do not clamp pivot so tight it binds; leave controlled preload.
- For plastic ears, prefer larger washer OD to reduce local stress.

## 5) Wall/Frame Clamp Mount

Use two bolts spaced apart to prevent rotation.

- Bolt spacing rule: center-to-center >= `3 x bolt diameter`.
- Edge distance: >= `2 x bolt diameter` from hole center.
- Add ribs between hole bosses for stiffness.

## Quick Build Checklist

- Correct thread standard (inch vs metric)
- Through-hole size chosen from clearance chart
- Nut trap size chosen from `data/nut_trap_sizes_hex.csv`
- Washer OD fits pocket and does not interfere
- Bolt length checked with `docs/bolt-length-selector.md`
