# EasyEDA PCB Design Guide (Detailed Workflow + Fast Decisions)

This guide is for getting back up to speed quickly in EasyEDA and designing boards with fewer respins.

## 1) What Must Exist on a Real PCB Design

Every board should explicitly include:

- Power entry and protection (connector, polarity protection, fuse/PTC, TVS where needed).
- Regulation (buck/LDO as needed, with input/output caps per datasheet).
- Controller/logic block (MCU or control IC, clock/reset/program header if applicable).
- Interfaces (UART/SPI/I2C/RS-485/USB/etc., with required transceivers).
- Load-driving stage (MOSFET/driver/relay/SSR path sized for load).
- Decoupling and bulk capacitance.
- Test points for rails and key signals.
- Mounting holes, keepouts, and connector orientation clarity.
- Clear silkscreen labels (polarity, connector names, revision, pin-1 markers).

If any of these are missing, assembly/debug time increases sharply.

## 2) End-to-End EasyEDA Workflow

1. Define requirements first:
   - Input voltage range, load current, environment, interfaces, safety constraints.
2. Capture schematic by functional blocks:
   - Power -> control -> interfaces -> outputs.
3. Assign validated footprints:
   - Verify package, pitch, pad style, courtyard, and 3D orientation.
   - If using assembly services, confirm each part's purchasable part number and stock status before layout is finalized.
4. Run ERC and clean warnings intentionally:
   - Do not ignore warnings without a reason.
5. Move to PCB and set board outline + rules:
   - Clearance, trace width rules, via sizes, creepage rules as needed.
   - Load fab-specific design rules at the start so DRC reflects real manufacturing limits.
6. Place components by signal/power flow:
   - Keep power path short and obvious.
7. Route critical nets first:
   - Power rails, clocks, differential/noise-sensitive nets.
8. Pour ground and check return paths:
   - Ensure returns can flow under/near outgoing signals.
9. Run DRC and fix root causes (not cosmetic reroutes only).
10. Generate outputs:
   - Gerbers, drill files, BOM, pick-and-place/CPL (if assembly), and reviewed fabrication notes.

## 3) Placement Logic (Where Most Speed Is Gained)

- Put connectors at edges first and lock them.
- Place regulators close to power entry/load zones they serve.
- Place decoupling capacitors at IC power pins first, then route.
- Keep high-current loops compact (input cap -> switch/regulator -> return).
- Separate noisy switching area from sensitive analog/sensor area.
- Keep crystal/clock parts tight to MCU clock pins with short symmetric routing.

Speed rule:

- Placement solves most routing pain. Spend more time placing, less time fighting traces.

## 4) Routing Logic That Prevents Rework

- Route from constraints:
  - High current/critical timing/noise-sensitive first.
- Use consistent power strategy:
  - Wider traces or pours for current paths, avoid neck-down bottlenecks.
- Prefer continuous reference planes for signal integrity.
- Minimize vias on high-current and sensitive nets.
- Avoid long parallel runs for noisy aggressor + sensitive victim nets.

For 2-layer boards:

- Treat one layer as mostly ground where possible.
- Keep return path continuity in mind when crossing splits/gaps.

## 5) Component Selection: When to Use and Not Use

### Regulators

- Use `LDO` when:
  - Current is low/moderate and low noise is important.
- Avoid `LDO` when:
  - `Vin - Vout` and load current create excessive heat.
- Use `buck converter` when:
  - Step-down efficiency and thermal performance matter.
- Avoid poor buck layouts:
  - Switch node loops too large cause EMI/ripple/debug issues.

### Switching Loads

- Use `MOSFET` when:
  - DC switching, PWM, silent operation, high cycle count are needed.
- Avoid `MOSFET`-only switching when:
  - You need true galvanic isolation at the load path.
- Use `relay` when:
  - You need mechanical isolation/contact behavior or AC mains switching.
- Avoid `relay` when:
  - You need high-frequency PWM or very high switching cycle life.
- Use `SSR` when:
  - High-cycle silent switching is needed and leakage/thermal behavior is acceptable.
- Avoid `SSR` when:
  - Off-state leakage or voltage drop/heat cannot be tolerated.

### Protection Parts

- Use `TVS` on exposed IO/power entry where transients/ESD are plausible.
- Use `flyback diode` for coils (relay, solenoid, valves).
- Use `fuse/PTC` near power entry, not deep inside the board.

### Interface Parts

- Use `RS-485 transceiver` for long/noisy field wiring.
- Use `USB-UART bridge` for reliable service/debug access.
- Use level shifting/isolation when voltage domains or ground conditions require it.

### When Not to Add "Extra" Components

- Do not add both `buck` and `LDO` on the same rail unless you need a clear reason (noise cleanup, sequencing, or thermal constraints).
- Do not add 0 ohm jumpers "just in case" everywhere; add only where debug/reconfiguration value is clear.
- Do not add optional protection parts without checking their normal-operation impact (leakage, capacitance, or voltage drop).

## 6) Common Beginner-to-Intermediate Traps

- Footprint symbol mismatch (pin order swapped or rotated).
- Missing pull-ups/pull-downs on control lines.
- No test points for rails/debug nets.
- Ground pour present but return path broken by splits.
- Overreliance on autoroute without review of current/return logic.
- Ignoring package thermal limits while only checking electrical ratings.

## 7) Fast DRC/ERC Triage Method

1. Power/ground shorts or unconnected rails first.
2. Footprint pin mapping and polarized part orientation second.
3. Clearance/width/annular constraints third.
4. Silkscreen overlaps and cosmetic cleanup last.

This order prevents wasting time polishing a board that still has functional faults.

## 8) Manufacturing-Ready Output Checklist

- Gerber layers reviewed in viewer (not just exported).
- Drill file verified against plated/non-plated intent.
- BOM includes exact manufacturer part numbers and alternates where possible.
- CPL/position file orientation checked against footprints (pin-1 and rotation).
- Assembly notes include polarity and critical install constraints.
- Board revision and date marked on silkscreen.

## 9) Practical Advice to Design Faster

- Reuse proven blocks from your own prior boards (power entry, RS-485 node, MOSFET driver stage).
- Keep a personal EasyEDA checklist and run it before each release.
- Name nets clearly (`24V_IN`, `5V_REG`, `VALVE_A_DRV`, `485_A`, `485_B`).
- Place and lock critical components early.
- Do one deliberate self-review pass focused only on failure modes.
- Keep one reusable template project with your preferred rules, layer stack notes, title block, and output settings.

## 10) Suggested "First Board Back" Practice Project

Build a small control board with:

- `24V` input -> buck to `5V` -> LDO to `3.3V`
- MCU + debug header
- One MOSFET low-side load output with flyback path
- One RS-485 transceiver
- Status LEDs and test points

This touches power, control, communication, protection, and layout discipline in one manageable design.
