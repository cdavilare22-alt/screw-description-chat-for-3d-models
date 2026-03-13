# Electrical Basics + Wire Sizing Quick Guide

This guide helps with day-to-day decisions around wire gauge, amp load, and power math.

## Safety First

- Treat this as a field reference, not a replacement for electrical code.
- Final wire size must account for insulation type, temperature rating, conductor count, installation method, and local code.
- Verify breaker, terminal, and wire temperature rating compatibility.

## What the Main Terms Mean

- **Voltage (V):** electrical pressure pushing current.
- **Current (A or amps):** flow of electric charge.
- **Power (W or watts):** work being done, usually `W = V x A`.
- **Resistance (ohms):** opposition to current flow.
- **Power factor (PF):** AC efficiency factor; motors often have PF < 1.

## How They Work Together

- If voltage stays fixed and power goes up, current goes up.
- For the same power, higher voltage means lower current.
- Lower current usually allows smaller wire or lower voltage drop.

## Fast Math You Will Use

- `W = V x A`
- `A = W / V`
- `V = W / A`
- `Vdrop = I x R`

Examples:

- 1200W load on 120V: `A = 1200 / 120 = 10A`
- 1200W load on 240V: `A = 1200 / 240 = 5A`

## Choosing Wire Gauge (Practical Flow)

1. Determine load current (nameplate or `A = W / V`).
2. Choose wire gauge with ampacity above load current.
3. Check breaker pairing norms.
4. Check run length for voltage drop (longer run may need larger wire).
5. Confirm terminals are rated for selected wire size and temperature class.

## Common U.S. Copper Branch-Circuit Memory Points

- 14 AWG -> 15A branch circuits
- 12 AWG -> 20A branch circuits
- 10 AWG -> 30A branch circuits

## When to Upsize Wire

- Long cable runs (voltage drop concerns)
- Warm environments
- Bundled conductors
- Motor/inrush loads
- Future load growth

## Related Data Files

- `data/us_copper_awg_ampacity_quick_chart.csv`
- `data/awg_common_sizes_reference.csv`
- `data/electrical_power_formula_cheatsheet.csv`
- `data/common_voltage_levels_us_quick_reference.csv`
