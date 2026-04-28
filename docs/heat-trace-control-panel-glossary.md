# Heat Trace Control Panel Glossary

This guide is for interns and panel builders who need to recognize the parts, labels, and acronyms
that show up in heat trace control panels.

It is not a wiring manual. Use drawings, datasheets, labels, and qualified supervision for actual
panel work.

## Fast Mental Model

A heat trace control panel usually does four jobs:

1. Bring power into the panel safely.
2. Read temperature or status signals.
3. Decide whether heat is needed.
4. Switch power to heat trace, heater pads, or appliance heaters.

Simple chain:

```text
Power in -> breaker/fuse/GFEP -> controller -> relay/SSR/contactor -> heater or heat trace
                                      ^
                                      |
                              PT100/RTD/thermostat
```

## Temperature and Sensor Terms

| Term | Stands for / Means | Intern-friendly meaning |
|---|---|---|
| RTD | Resistance Temperature Detector | A temperature sensor whose resistance changes with temperature. |
| PT100 | Platinum 100 ohm RTD | `Pt` means platinum. `100` means about `100 ohms` at `0C`. |
| PT1000 | Platinum 1000 ohm RTD | Same idea as PT100, but `1000 ohms` at `0C`. |
| 2-wire RTD | Two wires to the RTD | Simple, but wire resistance adds error. |
| 3-wire RTD | Three wires to the RTD | Common industrial style; helps cancel lead-wire resistance. |
| 4-wire RTD | Four wires to the RTD | More accurate; used when lead resistance really matters. |
| Thermistor | Temperature-sensitive resistor | Often low-cost electronics sensor. NTC types go down in resistance as temperature rises. |
| NTC | Negative Temperature Coefficient | Resistance goes down when temperature goes up. |
| PTC | Positive Temperature Coefficient | Resistance goes up when temperature goes up. PT100/PT1000 behave this way. |
| Thermocouple | Two different metals making a tiny voltage | Common for high temperature; not the same signal as an RTD. |
| Thermostat | Temperature-operated switch | Opens or closes contacts at a temperature setpoint. |
| High limit | Safety temperature cutoff | Stops heating if something gets too hot. |
| Ambient sensor | Air temperature sensor | Turns heat on based on surrounding air temperature. |
| Pipe sensor | Pipe/equipment temperature sensor | Controls based on the actual protected pipe or appliance. |

PT100 memory:

- `PT100` is not a heater. It is only a temperature sensor.
- `PT` or `Pt` means platinum.
- `100` means `100 ohms at 0C`.
- As a PT100 gets hotter, its resistance goes up.

## Controller and Board Terms

| Term | Stands for / Means | Intern-friendly meaning |
|---|---|---|
| Controller | Control device or board | Reads inputs, runs logic, and commands outputs. |
| MCU | Microcontroller Unit | Small computer on a board. ESP32 and RP2040/Pico-style boards are examples. |
| PLC | Programmable Logic Controller | Industrial controller used for inputs, outputs, logic, and alarms. |
| HMI | Human-Machine Interface | Screen/keypad where a person views status or changes settings. |
| Firmware | Program inside the controller | The code that tells the controller what to do. |
| Setpoint | Target value | Temperature the system tries to maintain. |
| Hysteresis | On/off deadband | Prevents rapid clicking by turning on below one value and off above another. |
| Alarm | Fault or warning condition | Tells the operator something needs attention. |
| Interlock | Required condition before output can turn on | Example: do not energize heat if a safety switch is open. |
| Watchdog | Fault monitor/reset feature | Helps recover if firmware locks up. |

## RTD Interface and Electronics Terms

| Term | Stands for / Means | Intern-friendly meaning |
|---|---|---|
| MAX31865 | RTD-to-digital converter chip | Chip that lets a microcontroller read PT100/PT1000 sensors. |
| SPI | Serial Peripheral Interface | Short board-level communication bus used by chips like MAX31865. |
| CS | Chip Select | SPI line that chooses which chip is being talked to. |
| MISO | Master In, Slave Out | SPI data line from chip back to controller. |
| MOSI | Master Out, Slave In | SPI data line from controller to chip. |
| SCK | Serial Clock | SPI clock line. |
| ADC | Analog-to-Digital Converter | Converts a voltage into a number the controller can read. |
| DAC | Digital-to-Analog Converter | Converts a number into an analog voltage/current output. |
| Pull-up / pull-down | Bias resistor | Holds a signal at a known on/off state when nothing else drives it. |
| Optocoupler | Optical isolator | Passes a signal across isolation without direct electrical connection. |
| Isolation | Electrical separation | Keeps noisy/high-voltage areas separated from logic or user-side wiring. |

Trasor-style RTD board memory:

- Multiple RTD channels may share SPI lines.
- Each RTD channel normally has its own chip-select pin.
- A MAX31865 can report faults like open sensor, shorted sensor, or out-of-range wiring.

## Power Switching Terms

| Term | Stands for / Means | Intern-friendly meaning |
|---|---|---|
| Relay | Electromechanical switch | A coil pulls contacts open/closed. You may hear it click. |
| SSR | Solid-State Relay | Electronic relay with no moving contacts. Often used for heater switching. |
| Contactor | Heavy-duty relay | Used for larger loads or groups of loads. |
| Triac | AC semiconductor switch | Electronic AC switch used in some controllers and SSRs. |
| MOSFET | Metal-Oxide-Semiconductor Field-Effect Transistor | Efficient electronic switch, common for DC loads. |
| Coil | Electromagnet winding in relay/contactor | The control side that makes contacts move. |
| Contacts | Power switching points | The side that opens/closes the load circuit. |
| NO | Normally Open | Contact is open until energized. |
| NC | Normally Closed | Contact is closed until energized. |
| COM | Common | Shared contact terminal on relay/switch. |
| Flyback diode | Coil suppression diode | Protects electronics from voltage spikes when a DC coil turns off. |
| Snubber | Spike/noise suppression network | Often resistor/capacitor across contacts or loads. |
| Heat sink | Metal part that removes heat | SSRs and power devices may need one. |

SSR memory:

- SSR input and output are separate sides.
- Match AC SSR to AC load, DC SSR to DC load.
- SSRs can leak a tiny current when off, so a meter may show ghost voltage.
- SSRs make heat when carrying current, so mounting and heat sinking matter.

## Heat Trace and Heater Load Terms

| Term | Stands for / Means | Intern-friendly meaning |
|---|---|---|
| Heat trace | Electric heating cable | Cable installed on pipe/equipment to prevent freezing or maintain temperature. |
| Self-regulating cable | Heat output changes with temperature | Colder sections make more heat; warmer sections make less. |
| Constant-wattage cable | Fixed watts per foot | More dependent on correct control and installation. |
| W/ft | Watts per foot | Heat output rating per foot of cable. |
| Heater pad | Flat electric heater | Used on tanks, enclosures, appliances, or surfaces. |
| Cartridge heater | Cylindrical heater | Slides into a drilled hole or heated block. |
| Power kit | Approved heat trace connection kit | Connects supply wiring to the heating cable. |
| End seal | Sealed far end of heat trace | Keeps moisture out and conductors separated. |
| Splice / tee kit | Approved cable joining kit | Joins or branches heat trace where allowed. |
| Cold lead | Non-heating power lead | Wire section feeding a heater or cable. |
| Inrush / cold start | Higher startup current | Some heaters or self-regulating cables draw more current when cold. |
| Maintain temp | Temperature to hold | Target pipe/equipment temperature. |
| Max exposure temp | Highest temperature cable can survive | Limit from external/process heat. |

## Protection and Safety Terms

| Term | Stands for / Means | Intern-friendly meaning |
|---|---|---|
| Breaker | Resettable overcurrent device | Trips when current is too high. |
| MCB | Miniature Circuit Breaker | Small DIN-rail breaker common in panels. |
| Fuse | One-time overcurrent device | Opens when current is too high; must be replaced. |
| Fuse holder | Mount for fuse | Lets fuses be installed and replaced safely. |
| GFCI | Ground-Fault Circuit Interrupter | Trips on small leakage current; often personnel/shock protection. |
| GFEP | Ground-Fault Equipment Protection | Ground-fault protection often used for heat trace equipment. |
| E-stop | Emergency stop | Button/switch to quickly stop equipment. |
| Disconnect | Main isolation switch | Turns off panel or equipment power for service. |
| Surge protector | MOV/TVS/SPD device | Clamps voltage spikes. |
| MOV | Metal Oxide Varistor | Common AC surge clamp component. |
| TVS diode | Transient Voltage Suppression diode | Fast surge clamp, common on DC/signal lines. |
| Ground / PE | Protective Earth | Safety grounding path. |
| Bonding | Connecting metal parts to ground | Helps make fault current trip protection. |
| Megger | Insulation resistance tester | Finds leakage/damaged insulation using high test voltage. |

Heat trace protection memory:

- Ground-fault trips can mean wet insulation, damaged cable, failed end seal, or bad power kit.
- Do not bypass GFEP/GFCI to make heat trace run.
- A normal ohm check does not prove insulation is safe.

## Panel Hardware You Will Handle

| Term | Means | Intern-friendly meaning |
|---|---|---|
| Enclosure | Panel box | Protects components and wiring. |
| Backplate / subpanel | Mounting plate inside enclosure | Where DIN rail, wire duct, and devices are mounted. |
| DIN rail | Standard metal mounting rail | Snaps in breakers, terminal blocks, relays, and power supplies. |
| Wire duct | Slotted plastic wire channel | Keeps panel wiring organized. |
| Terminal block | Wire landing point | Joins field wiring to panel wiring. |
| Ground terminal | PE/ground terminal block | Bonds ground wires to panel ground. |
| Jumper / bridge | Terminal block connector | Connects several terminals together. |
| Ferrule | Crimp sleeve on stranded wire | Makes a clean, reliable terminal connection. |
| Ring/fork/spade lug | Crimp terminal | Attaches wire to screws or studs. |
| Cable gland | Cord grip/strain relief | Seals and grips cable entering an enclosure. |
| Grommet | Edge protector | Protects wire passing through a hole. |
| Nameplate | Device label | Identifies device, voltage, function, or warning. |
| Wire marker | Wire label | Helps troubleshoot and match drawings. |

Panel builder memory:

- Cut, strip, crimp, land, label, tug-test, and torque-check.
- Ferrules are for stranded wire in many screw-clamp terminals.
- Labels are not decoration; they are how the next person troubleshoots.

## Power Supply and Voltage Terms

| Term | Means | Intern-friendly meaning |
|---|---|---|
| Line / L | Hot conductor | Energized supply conductor. |
| Neutral / N | Grounded circuit conductor | Return conductor on many AC systems. |
| PE | Protective Earth | Safety ground, not a normal current return. |
| 24V DC | Common control voltage | Often used for sensors, relays, PLC inputs, and indicators. |
| Power supply / PSU | Converts voltage | Example: `120V AC` to `24V DC`. |
| Transformer | AC voltage converter/isolation device | Steps AC voltage up/down or provides isolation. |
| Buck converter | DC step-down converter | Efficiently makes lower DC voltage. |
| LDO | Low Dropout regulator | Linear regulator for low-noise, low-current rails. |
| VA | Volt-amps | Apparent power rating, common for transformers. |
| Load | Device using power | Heater, relay coil, fan, controller, light, etc. |

## Signals, Communications, and Modbus Terms

| Term | Stands for / Means | Intern-friendly meaning |
|---|---|---|
| RS-485 | Differential serial wiring standard | Robust communication over twisted pair in noisy panels/field wiring. |
| Modbus RTU | Industrial serial protocol | Common way controllers and devices exchange numbers/status. |
| Slave ID / Unit ID | Device address | Number that identifies one Modbus device on the bus. |
| Baud rate | Communication speed | Example: `9600`, `19200`, or `115200`. |
| 8N1 | 8 data bits, no parity, 1 stop bit | Common serial setting. |
| DE pin | Driver Enable | Turns an RS-485 transmitter on/off. |
| A/B | RS-485 pair labels | Differential communication wires; vendor polarity can be confusing. |
| Termination | End-of-line resistor | Helps prevent signal reflections on long RS-485 runs. |
| Biasing | Idle-state resistors | Keeps RS-485 line stable when nobody is talking. |
| Coil | Modbus bit output | On/off value the controller may read/write. |
| Discrete input | Modbus bit input | On/off status input. |
| Holding register | Modbus read/write number | Setting or command value. |
| Input register | Modbus read-only number | Measurement/status value. |

Modbus memory:

- Modbus is not the wire. RS-485 is the common wire type; Modbus RTU is the message language.
- Every device on the same RS-485 bus needs a unique slave ID.
- Wrong baud/parity/address can look like a dead device.

## Current, Power, and Feedback Terms

| Term | Stands for / Means | Intern-friendly meaning |
|---|---|---|
| CT | Current Transformer | Sensor that measures AC current without putting meter electronics directly in series. |
| Shunt | Precision low-value resistor | Measures current by measuring small voltage drop. |
| Energy meter IC | Power measurement chip | Measures voltage/current/power for status or fault detection. |
| BL0939 / BL0910 | Energy metering chips | Chips used in some controller designs to measure electrical load. |
| Load current | Current through heater/load | Helps prove the heater actually energized. |
| Open load | Load not connected or broken | Controller output may be on, but no current flows. |
| Short circuit | Fault with too little resistance | Causes very high current and trips protection. |
| Leakage current | Small unwanted current path | Important for ground-fault devices and SSR off-state behavior. |

## Common Test Questions

- What does `PT100` mean?
- What is the difference between RTD, thermistor, and thermocouple?
- Why does a 3-wire RTD exist?
- What does an SSR do, and why can it need a heat sink?
- What is the difference between GFCI and GFEP?
- What does a MAX31865 do?
- What is RS-485 vs Modbus RTU?
- What are coils and holding registers in Modbus?
- Why does heat trace need an end seal?
- Why can missing insulation make a good heat trace system fail?
- Why should a ground-fault trip not be bypassed?

## One-Line Study Cards

- `RTD`: sensor that changes resistance with temperature.
- `PT100`: platinum RTD, 100 ohms at 0C.
- `MAX31865`: chip that reads RTDs for a microcontroller.
- `SSR`: electronic relay, often used for heaters.
- `GFEP`: ground-fault equipment protection, common for heat trace.
- `DIN rail`: standard metal rail for mounting panel devices.
- `Ferrule`: crimp sleeve for stranded wire in terminals.
- `RS-485`: robust two-wire serial electrical layer.
- `Modbus RTU`: message protocol used over serial links like RS-485.
- `Holding register`: Modbus setting/value that can usually be read and written.
