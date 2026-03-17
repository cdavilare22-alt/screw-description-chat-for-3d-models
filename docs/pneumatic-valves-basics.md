# Pneumatic Valves Basics

This guide explains what pneumatic valves are, what they operate with, and when to use them.

## What a Pneumatic Valve Is

- A pneumatic valve controls compressed gas flow in a pneumatic system.
- In most shop and industrial systems, the working medium is compressed air.
- Valves are used to start/stop flow, route flow paths, regulate pressure, or set flow rate.

Typical operating medium:

- Compressed air (common plant supply often around `80-120 psi`).
- In some systems, inert gases such as `nitrogen`.

## Why Pneumatic Valves Are Useful

- Fast, repeatable actuator motion (cylinders and grippers).
- Good for high-cycle automation.
- Clean operation compared with hydraulic oil systems.
- Straightforward maintenance in many production environments.

## Core Valve Functions

| Function | What It Does | Typical Use |
|---|---|---|
| Directional control | Routes air to extend/retract actuators | Cylinder and gripper motion control |
| Pressure regulation | Holds downstream pressure at setpoint | Protect tools/actuators from over-pressure |
| Flow control | Restricts flow to set actuator speed | Smooth extension/retraction timing |
| Check/non-return | Allows one-way flow only | Hold pressure, prevent backflow |
| Quick exhaust | Dumps actuator air locally for faster motion | Faster cylinder response |
| Soft start/dump | Gradual pressurization and safe venting | Safer startup/shutdown and maintenance |

## Directional Valve Types (Ports/Ways and Positions)

| Valve Type | Meaning | Typical Application |
|---|---|---|
| `2/2` | 2 ports, 2 positions | Basic on/off air supply |
| `3/2` | 3 ports, 2 positions | Single-acting cylinder control |
| `5/2` | 5 ports, 2 positions | Double-acting cylinder extend/retract |
| `5/3` | 5 ports, 3 positions | Double-acting cylinder with defined center behavior |

Port/position logic:

- `Ports` are physical air connection points.
- `Positions` are internal switching states.
- Example: `5/2` means 5 ports and 2 positions.

Common letter markings (vendor conventions vary):

- `P` = pressure supply (air in)
- `A` = work port A (to actuator side A)
- `B` = work port B (to actuator side B)
- `R` / `EA` = exhaust from A side
- `S` / `EB` = exhaust from B side

Common ISO number mapping:

- `1` = `P` (supply)
- `2` = `A`
- `4` = `B`
- `3` = exhaust for A side
- `5` = exhaust for B side

## Actuation Styles

- Solenoid-operated (electrical coil shifts spool/poppet).
- Pilot-operated (air pilot shifts main stage).
- Manual/mechanical lever or roller.

## When to Choose Pneumatic Valves

Use pneumatics when:

- Compressed air is already available.
- Motion is linear/clamping/pick-place with moderate force.
- High cycle rate and quick response are important.

Choose alternatives when:

- Very high force density is required (`hydraulics` may fit better).
- Tight closed-loop position control is required without extra hardware (`electric servo` may fit better).
- Compressed air infrastructure is unavailable.

## Practical Selection Checklist

- Valve type (`3/2`, `5/2`, `5/3`) based on actuator and fail-state.
- Port size and flow capacity (`Cv`/`Kv`) for speed targets.
- Coil voltage/control interface (`24V DC` common in panels).
- Pressure range and media compatibility.
- Normal state (`normally closed`, `normally open`, spring return, detented).
- Environmental rating (`IP`, temperature, contamination tolerance).
- Safety and maintenance features (manual override, dump/lockout strategy).

## Fast Integration Notes

- Use `FRL` (or filter-regulator where no lubrication is needed) to stabilize air quality/pressure.
- Place flow controls near cylinder ports for better speed tuning.
- Add silencers on exhaust ports to reduce noise.
- Define de-energized safe state clearly in controls and schematics.
