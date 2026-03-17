# PCB Components Primer (What They Do and When To Use Them)

This guide is for learning common parts used in real boards and projects.

For a full EasyEDA design workflow (requirements -> schematic -> layout -> DRC -> manufacturing package), see:

- `docs/easyeda-pcb-design-guide.md`

## Core Idea

- Most PCB designs are built from repeatable "blocks":
  power, control, switching, protection, interfaces, sensing, and connectors.

## Common Components and Typical Use

| Component Type | What It Does | Use It When | Common Mistake |
|---|---|---|---|
| Resistor | Limits current / sets voltage | LED limiting, pull-up/down, dividers, feedback | Missing pull-up/down on digital inputs |
| Capacitor | Stores charge / filters noise | Decoupling, smoothing supplies, RC timing | Not placing decoupling caps close to IC power pins |
| Inductor | Stores energy in magnetic field | Buck/boost converters, filtering | Using wrong current rating (saturation) |
| Diode | One-way current path | Reverse polarity, flyback, rectification | No flyback diode on relay/coil loads |
| TVS diode | Fast surge clamp | ESD/transient protection on IO/power lines | Picking standoff voltage too low/high |
| Fuse/PTC | Overcurrent protection | Input power safety and fault containment | Putting protection too far from power entry |
| Relay | Isolated electromechanical switch | Switching AC mains/high voltage/high current loads | Driving coil directly from MCU pin |
| MOSFET | Efficient electronic switch | DC load switching, PWM control, motor/heater control | Wrong gate drive (logic-level mismatch) |
| BJT transistor | Current-controlled switch/amplifier | Small signal stages, simple low-side switching | No base resistor |
| Optocoupler | Signal isolation | Noisy grounds, high-voltage domain isolation | Ignoring CTR/current requirements |
| Op-amp | Analog amplification/conditioning | Sensor scaling, filtering, active analog circuits | Choosing part without required rail-to-rail behavior |
| Comparator | Threshold detection | "Above/below limit" decisions, clean digital edge from analog | No hysteresis, causing chatter/noise triggers |
| LDO regulator | Linear voltage regulation | Low-noise rails, small drop conversions | Excess heat from high Vin-Vout drop |
| Buck converter | Efficient step-down conversion | Powering logic rails from higher DC input | Poor layout causing ripple/noise |
| MCU/SoC | Main logic + firmware control | System control, protocol handling, state machines | Underestimating pin/flash/RAM/peripheral needs |
| EEPROM/Flash | Non-volatile storage | Calibration values, settings, logs | Too-frequent writes without endurance planning |
| RS-485 transceiver | Differential serial interface | Modbus RTU and long/noisy serial runs | Missing termination/bias strategy |
| USB-UART bridge | USB to serial conversion | PC debug/configure interface | Voltage-level mismatch with target logic |
| Driver IC (ULN/H-bridge/gate driver) | Drives loads from logic signals | Relays, motors, solenoids, high-side/low-side gates | Driving loads directly from MCU IO |

## Relay vs MOSFET (Quick Decision)

- Use `relay` when you need galvanic isolation or to switch AC mains/mechanical contacts.
- Use `MOSFET` when you need fast, silent, high-cycle DC switching or PWM.
- For inductive loads (relay coil, solenoid, motor): always add flyback suppression.

## Standard Board Blocks Interns Should Recognize

1. Power input block: connector, reverse protection, fuse/PTC, TVS.
2. Regulation block: buck/LDO and bulk + decoupling capacitors.
3. Controller block: MCU, crystal/clock, reset/program/debug header.
4. IO protection block: series resistor, clamp/TVS, filtering.
5. Interface block: UART/SPI/I2C/RS-485/CAN transceivers.
6. Load-driving block: transistor/MOSFET/relay + driver + flyback path.

## "When Is A Chip Needed?" Rule of Thumb

- If MCU pin current is insufficient for a load, add a driver transistor/MOSFET/driver IC.
- If voltage domains differ, add a regulator and level-shifting/isolation where required.
- If cable is long/noisy, add proper physical-layer transceivers (for example RS-485).
- If safety or fault energy is possible, add protection parts first, not as an afterthought.

## Practical Checklist Before Layout

- Identify max voltage/current on each net.
- Confirm each component's voltage/current/temperature rating margin.
- Add decoupling for every IC power pin group.
- Add test points for power rails and key signals.
- Define ground strategy (single reference vs isolated domains).
- Verify connector pinout and field wiring polarity.
