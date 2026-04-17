# Temperature Sensors, RTDs, and PT100 Quick Guide

This guide explains common temperature-sensor words used in controls, wiring, and troubleshooting.

## Fast Definitions

- **Temperature sensor:** any device used to measure temperature.
- **RTD:** `Resistance Temperature Detector`.
- **PT100:** platinum RTD that measures `100 ohms` at `0C`.
- **PT1000:** platinum RTD that measures `1000 ohms` at `0C`.
- **Thermistor:** resistor made to change resistance strongly with temperature.
- **NTC:** negative temperature coefficient thermistor; resistance goes down as temperature rises.
- **PTC:** positive temperature coefficient device; resistance goes up as temperature rises.
- **Thermocouple:** two dissimilar metals that create a small voltage from temperature difference.
- **Transmitter:** electronics that convert a sensor signal into a usable output such as `4-20 mA`,
  `0-10 V`, or Modbus.

## How Sensors Fit Into A Heat Trace System

Heat trace systems often need a temperature input so the controller knows when to turn heating on or
off.

Simple chain:

```text
Pipe/equipment temperature -> sensor -> controller -> heater output
```

Common sensor choices:

| Sensor type | What the controller sees | Beginner note |
|---|---|---|
| RTD/PT100 | Resistance that rises with temperature | Common industrial accurate sensor |
| NTC thermistor | Resistance that falls with temperature | Common low-cost electronics sensor |
| Thermocouple | Small voltage from temperature difference | Common for high temperature |
| Thermostat switch | Open/closed contact | Simple on/off temperature switch |
| Transmitter | `4-20 mA`, `0-10 V`, or digital data | Sensor plus electronics in one package |

Do not assume all temperature sensors wire the same way. Identify the sensor type before replacing
or testing it.

## RTD Meaning

`RTD` stands for `Resistance Temperature Detector`.

An RTD is a temperature sensor that changes resistance in a predictable way as temperature changes.
Most industrial RTDs use platinum because it is stable and repeatable.

Common RTD names:

| Name | Meaning | Resistance at 0C |
|---|---|---:|
| PT100 | Platinum RTD | 100 ohms |
| PT1000 | Platinum RTD | 1000 ohms |

For a platinum RTD, resistance increases as temperature increases. That means:

- colder than `0C` -> less than nominal resistance
- `0C` -> `100 ohms` for PT100, `1000 ohms` for PT1000
- hotter than `0C` -> more than nominal resistance

Approximate memory points for PT100:

| Temperature | PT100 resistance, approximate |
|---:|---:|
| -50C | 80 ohms |
| 0C | 100 ohms |
| 100C | 138.5 ohms |
| 200C | 175.9 ohms |

## PT100 Wiring Types

RTDs are often wired with 2, 3, or 4 wires.

| Wiring | What it means | Use case |
|---|---|---|
| 2-wire | Sensor resistance plus wire resistance | Short leads, low accuracy needs |
| 3-wire | Compensates for lead resistance if wires match | Common industrial RTD wiring |
| 4-wire | Measures sensor resistance with best lead compensation | Higher accuracy or longer runs |

Main field mistake:

- A 2-wire PT100 on a long cable reads high because the cable resistance adds to the sensor
  resistance. Since PT100 resistance rises with temperature, extra lead resistance looks like extra
  temperature.

## RTD Interface Chips

Many microcontrollers cannot read a PT100 directly. They need an RTD interface circuit.

One common chip family is `MAX31865`.

What it does:

- sends a small measurement current through the RTD
- measures the RTD resistance
- reports the result digitally to a microcontroller, often over SPI
- can report faults such as open sensor, shorted sensor, or out-of-range wiring

Workspace notes mention thermal controller designs using `3 RTD input` hardware and `MAX31865`
style RTD-to-digital conversion. That is the normal pattern:

```text
PT100/PT1000 sensor -> RTD interface chip -> microcontroller -> control decision
```

Important beginner point:

- The RTD is not a power device. It is only a sensor.
- The heater or heat trace is switched by a separate relay, solid-state relay, triac, or power
  controller.

## Thermistor vs RTD

| Sensor | Behavior | Common use |
|---|---|---|
| PT100/PT1000 RTD | Predictable, fairly linear, stable | Industrial temperature measurement |
| NTC thermistor | Resistance decreases as it gets hotter | Electronics, battery packs, HVAC probes |
| PTC thermistor/device | Resistance increases as it gets hotter | Protection, resettable limiting, sensing |

Important difference:

- PT100 and PT1000 are PTC-style sensors because their resistance rises with temperature.
- Many small electronics temperature probes are NTC thermistors, which do the opposite.

## Cold, Resistance, Amps, and Power

Be specific about what material or load you are talking about.

For copper wire:

- colder copper has lower resistance
- hotter copper has higher resistance
- lower wire resistance causes less voltage drop for the same current

For a simple fixed-resistance heater or lamp:

- lower resistance at a fixed voltage allows more current
- more current can mean more startup/inrush power
- as the element heats up, resistance usually rises and current settles

For an NTC thermistor:

- colder means higher resistance
- higher resistance at a fixed voltage means lower current through the thermistor path

For motors and mechanical loads:

- cold oil, grease, bearings, pumps, or fans can require more torque
- more torque demand can make motor current rise
- in that case, the increased current is from mechanical load, not just wire resistance

Practical troubleshooting rule:

- If amps rise in the cold, ask whether the cause is lower electrical resistance, higher mechanical
  load, low supply voltage, or a control circuit trying to maintain constant power.

## Sensor Selection Memory Points

- Use `PT100` or `PT1000` for stable industrial temperature measurement.
- Use `3-wire RTD` as a common industrial default when cable resistance matters.
- Use `4-wire RTD` when accuracy matters more than wiring cost.
- Use `NTC thermistor` for low-cost electronics temperature sensing.
- Use `thermocouple` for very high temperatures or rugged measurement over a wide range.
- Use a `transmitter` when the controller expects `4-20 mA`, `0-10 V`, or a digital protocol.

## Common Mistakes

- Confusing RTD and thermistor behavior.
- Forgetting that PT100 lead-wire resistance changes the reading.
- Assuming every temperature sensor outputs voltage.
- Connecting an RTD directly to a digital input instead of an RTD input or transmitter.
- Ignoring shield/grounding needs on long low-level analog sensor wiring.

## Quick Check Questions

Before replacing or troubleshooting a temperature sensor, ask:

- Is it RTD, thermistor, thermocouple, thermostat, or transmitter?
- Is it 2-wire, 3-wire, or 4-wire?
- What does the controller input expect?
- Is the sensor used only for display, or does it control heater output?
- Does the controller show an open-sensor or short-sensor fault?
- Is the cable run long enough that lead resistance matters?
