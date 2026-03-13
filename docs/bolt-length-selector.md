# Bolt Length Selector for Printed Mounts

Use this to choose bolt length quickly for through-bolt assemblies.

## Formula

`bolt length ~= total clamped thickness + washer stack + nut thickness + exposed threads`

Recommended exposed threads beyond nut:

- Standard nut: `1 to 2 threads`
- Locknut (nyloc): `2 to 3 threads`

## Step-by-Step

1. Add all clamped part thicknesses.
2. Add washer thicknesses (head side + nut side if used).
3. Add nut height.
4. Add thread allowance.
5. Round up to nearest standard bolt length.

## Example 1 (Metric)

- Bracket: 6.0 mm
- Panel: 2.0 mm
- Two washers: 2 x 1.0 mm = 2.0 mm
- M5 nut: ~4.0 mm
- Thread allowance: 1.5 mm

Total = `6 + 2 + 2 + 4 + 1.5 = 15.5 mm`

Pick `M5 x 16 mm`.

## Example 2 (Inch)

- Printed part: 0.250 in
- Mating plate: 0.125 in
- Two washers: 0.126 in total
- 1/4-20 nut: 0.219 in
- Thread allowance: 0.060 in

Total = `0.250 + 0.125 + 0.126 + 0.219 + 0.060 = 0.780 in`

Pick `1/4-20 x 7/8 in`.

## Common Mistakes

- Forgetting washer thickness in stack-up
- Picking exact calculated length with zero thread margin
- Ignoring nyloc extra height
