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

## Temperature, Resistance, Current, and Cold Starts

Temperature changes resistance, but the direction depends on the material or device.

For copper wire:

- colder copper has lower resistance
- hotter copper has higher resistance
- lower wire resistance means less voltage drop for the same current

For a simple fixed-resistance heater or incandescent lamp:

- lower resistance at a fixed voltage allows more current
- startup current can be higher while the element is still cold
- as the element heats up, resistance usually rises and current settles

For an NTC thermistor:

- colder means higher resistance
- higher resistance at a fixed voltage means lower current through that thermistor path

For motors, pumps, and fans:

- cold oil, grease, bearings, or fluid can increase mechanical load
- higher mechanical load can make motor current rise
- this is different from wire resistance; it is the motor working harder

Practical rule:

- If amps rise in cold conditions, check whether the cause is electrical resistance, mechanical load,
  low voltage, or a constant-power supply trying to maintain output power.

## Fast Math You Will Use

- `W = V x A`
- `A = W / V`
- `V = W / A`
- `V = I x R`
- `I = V / R`
- `R = V / I`
- `Vdrop = I x R`

For `Vdrop = I x R`:

- `I` is current in amps flowing through the conductor.
- `R` is total conductor-path resistance in ohms.
- On a normal 2-wire path, compute `R` using round-trip length:
  `R = (wire ohms per foot) x (2 x one-way feet)`.

Examples:

- 1200W load on 120V: `A = 1200 / 120 = 10A`
- 1200W load on 240V: `A = 1200 / 240 = 5A`

## Choosing Wire Gauge (Practical Flow)

1. Determine load current (nameplate or `A = W / V`).
2. Choose wire gauge with ampacity above load current.
3. Check breaker pairing norms.
4. Check run length for voltage drop (longer run may need larger wire).
5. Confirm terminals are rated for selected wire size and temperature class.

## How To Use 60C / 75C / 90C Ampacity Ratings

- `60C`, `75C`, and `90C` are temperature ratings tied to insulation and terminations.
- Ampacity increases across those columns for the same gauge, but you cannot always use the highest one.
- Final conductor ampacity is limited by the lowest-rated component in the path:
  wire insulation, lugs/terminals/devices, and equipment listing.
- Example: if wire is `90C` but connected terminations are only `60C`, size from `60C`.
- Then apply any additional derating required by ambient temperature and conductor bundling.

## Breaker Basics (What They Are and How They Work)

What a breaker is:

- A breaker is an automatic safety switch that opens when current exceeds safe limits.
- It mainly protects conductors and wiring from overheating.

How breakers trip:

- Thermal element trips on sustained overload (time delay).
- Magnetic element trips quickly on short-circuit/high-fault current.
- This is inverse-time behavior: bigger faults trip faster.

Common breaker types:

- Standard thermal-magnetic.
- `GFCI` breaker (ground-fault shock protection).
- `AFCI` breaker (arc-fault protection).
- Dual-function `AFCI/GFCI`.
- Single-pole vs double-pole common-trip.

Practical rules:

- Match breaker rating to wire ampacity, terminals, and equipment ratings.
- Do not upsize a breaker unless wire/equipment ratings allow it.
- Frequent tripping means investigate overload, fault, inrush, or wiring issues.

## Resistor Basics (Why They Are Used and When Needed)

What a resistor is:

- A resistor limits current and helps set voltages in a controlled way.
- Resistance is measured in ohms (`ohm`).

Common reasons to use resistors:

- Current limiting for LEDs and sensitive inputs/outputs.
- Pull-up/pull-down on digital inputs to prevent floating logic states.
- Voltage divider networks for ADC scaling and logic-level adaptation.
- Feedback/gain setting in analog circuits and regulator setpoints.
- RC timing or filtering for debounce and noise reduction.
- Series damping/termination for high-speed digital signal quality.
- Bleeder/discharge paths for capacitors.

Quick checks:

- If direct connection causes too much current, a resistor is required.
- If an input can float randomly, use pull-up or pull-down resistor.
- If measured signal exceeds input rating, use divider/scaling resistors.
- If signal has ringing/noise, add damping/termination resistance.

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

## Related Guides

- `docs/temperature-sensors-rtd-pt100.md`
- `docs/heat-trace-basics.md`
