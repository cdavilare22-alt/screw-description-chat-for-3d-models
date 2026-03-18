# Embedded Communications Quick Guide (UART, SPI, I2C, Modbus RTU/RS-485)

This guide gives quick protocol-selection rules for embedded systems and controls.

## Protocol Summaries

- `UART`: simple asynchronous serial. Best for one-to-one links and debug ports.
- `SPI`: fast synchronous bus with dedicated chip select per peripheral.
- `I2C`: two-wire addressed bus for multiple lower-speed peripherals.
- `Modbus RTU over RS-485`: robust industrial serial network for multi-node field devices.

## Practical Logic Example: SC16IS752

The `SC16IS752` is a useful example of how these methods fit together.

- The chip provides `2` external UART channels: `UART A` and `UART B`.
- The MCU does not talk to those UART channels directly.
- The MCU talks to the `SC16IS752` over either `SPI` or `I2C`.

That means the structure is:

- `MCU -> SPI -> SC16IS752 -> UART A -> external device 1`
- `MCU -> SPI -> SC16IS752 -> UART B -> external device 2`

Or with I2C instead:

- `MCU -> I2C -> SC16IS752 -> UART A -> external device 1`
- `MCU -> I2C -> SC16IS752 -> UART B -> external device 2`

Practical interpretation:

- `UART` is the actual external serial link used by the end devices.
- `SPI` is the internal high-speed link from the MCU to the UART-expander chip.
- `I2C` is an alternative internal link from the MCU to that same chip, using fewer pins but lower bandwidth.

Rule of thumb:

- Use `SPI` when speed matters and you can spare the pins.
- Use `I2C` when pin count matters more than speed.
- Use `UART` when you are talking directly to a serial device, or when a bridge chip is giving you extra UART ports.

## Selection Cheat Sheet

| Protocol | Use It When | Avoid It When | Typical Applications |
|---|---|---|---|
| UART | You need simple, low-overhead point-to-point serial | You need many devices on one bus | Debug consoles, GPS, modem links |
| SPI | You need high speed and deterministic transfer timing | Cable is long or many off-board nodes are needed | ADC/DAC, flash memory, TFT/OLED displays |
| I2C | You need many peripherals with minimal pins | Bus is long/noisy or address collisions exist | IMU/temp sensors, RTCs, IO expanders |
| Modbus RTU over RS-485 | You need long-distance, noise-tolerant, multi-drop industrial communication | You need very high throughput or spontaneous peer-to-peer messaging | PLC to drives, remote IO, power meters, SCADA polling |

## Modbus RTU + RS-485 Practical Notes

1. Use MCU `UART` + external RS-485 transceiver (`MAX485`/`SN65HVD`/similar).
2. For half-duplex transceivers, control `DE`/`RE` pin direction from firmware.
3. Keep one continuous trunk; place 120 ohm termination only at both ends.
4. Add bias resistors at one bus location if not built into hardware.
5. Match serial settings across all nodes (baud, parity, stop bits).
6. Assign unique slave/server addresses (typically `1..247`).
7. Use CRC, timeout, retry, and exception-code logging for robust behavior.

## Common Failure Logic (Fast Debug)

- If the whole bus is unstable, confirm termination is only at the two physical ends of the trunk.
- If only one node fails, verify its address is unique and not duplicated elsewhere.
- If you get CRC errors/timeouts with visible traffic, check baud/parity/stop-bit framing on every node.
- If transmit seems fine but receive is dead (or reversed), check firmware timing for `DE`/`RE` direction control.
- If someone expects spontaneous messages from field nodes, clarify that Modbus RTU server/slave devices reply when polled; they do not normally initiate frames.

## Quick Decision Flow

1. One device and shortest implementation time: pick `UART`.
2. Need fastest board-level link: pick `SPI`.
3. Need many low/medium-speed board devices on two wires: pick `I2C`.
4. Need long, noisy, multi-node field bus: pick `Modbus RTU over RS-485`.

## Related Data

- `data/serial_protocol_selection_cheatsheet.csv`
- `data/modbus_rs485_quick_reference.csv`
