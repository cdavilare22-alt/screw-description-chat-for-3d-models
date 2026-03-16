# CNC Operator Quickstart (Buttons + XYZ Zero)

Use this as a practical training checklist. Control labels vary by machine (`Fanuc`, `Haas`, `Mach3/4`, `GRBL`, `Masso`, etc.), but the workflow is similar.

## Absolute Beginner Basics (No Prior CNC Experience)

- CNC means the machine follows programmed coordinates to move tool and part.
- `X/Y` usually move left-right and front-back; `Z` is up-down.
- Positive `Z` is away from the part (safer); negative `Z` moves into cutting depth.
- You always need two references:
  - machine reference (home),
  - part reference (work offset like `G54`).

### What Each Core Control Does in Plain Language

- `E-STOP`: cuts motion immediately for danger situations. Use only when necessary.
- `RESET`: cancels run state/alarms; use after stops or errors before restarting.
- `HOME / REF ALL`: tells machine where absolute position zero is.
- `JOG`: manual movement using buttons.
- `HANDWHEEL / MPG`: very fine manual movement in small steps.
- `MDI`: type one command at a time (for setup/test commands).
- `CYCLE START`: run or resume program motion.
- `FEED HOLD`: pause cutting motion without emergency shutdown.
- `SINGLE BLOCK`: run one line of code per start press (safe proving mode).
- `OPTIONAL STOP`: if program has `M01`, machine pauses there when enabled.
- `FEED OVERRIDE`: slow/raise cutting speed percentage.
- `RAPID OVERRIDE`: slow down fast travel moves (non-cutting moves).
- `SPINDLE OVERRIDE`: adjust spindle RPM percentage.

### Modes You Will Usually Use

- `JOG/HANDLE`: setup and zeroing.
- `MDI`: manual commands (like spindle on/off tests).
- `AUTO/MEM`: running a loaded program.

## Best Way To Learn Safely

1. Load code in simulator/backplot first.
2. Run an air cut (tool above stock, no material contact).
3. Use single-block and low feed/rapid override for first run.
4. Keep hand on feed hold; know where E-stop is before cycle start.

## Common Button Functions (Most Controllers)

- `E-STOP`: immediate emergency stop.
- `RESET`: clears alarms / stops execution state.
- `CYCLE START`: starts or resumes program.
- `FEED HOLD`: pauses axis feed safely.
- `SINGLE BLOCK`: executes one block at a time.
- `OPTIONAL STOP`: honors `M01` stops when enabled.
- `JOG`: manual axis movement.
- `HOME / REF ALL`: sends axes to machine home.
- `MDI`: manual command entry.
- `HANDWHEEL / MPG`: fine manual jog increments.
- `FEED OVERRIDE`: scales programmed feed rate.
- `RAPID OVERRIDE`: scales rapid moves.
- `SPINDLE OVERRIDE`: scales spindle speed.

## Button Process Flow (What To Press and When)

### A) Power-Up and Reference

1. Release `E-STOP` (if engaged), then power control/servos.
2. Press `RESET` to clear startup/alarm state.
3. Press `HOME / REF ALL` to establish machine zero.
4. Use `JOG` / `HANDWHEEL` only for safe positioning after homing.

### B) Setup and Zeroing

1. Enter `JOG` or `HANDLE` mode and move to part datum.
2. Set `G54 X` and `G54 Y` at your chosen origin.
3. Jog down carefully and set `G54 Z` (paper, probe, or tool setter method).
4. Verify active offset is `G54` and units are correct (`G20`/`G21`).

### C) Prove-Out (First Run)

1. Enable `SINGLE BLOCK`.
2. Reduce `FEED OVERRIDE` and `RAPID OVERRIDE` (for example 10-25%).
3. Press `CYCLE START` to run one block at a time.
4. Use `FEED HOLD` anytime motion is not as expected.
5. Press `CYCLE START` again to continue after each check.

### D) Production Run

1. Disable `SINGLE BLOCK` after proof is clean.
2. Set normal overrides.
3. Press `CYCLE START` for full run.
4. Use `OPTIONAL STOP` (`M01`) when you want programmed inspection pauses.

### E) Stop and Recovery

- Normal pause: `FEED HOLD` -> inspect -> `CYCLE START` to resume.
- Program abort: `RESET` -> re-check mode/offset/tool line before restart.
- Immediate danger: `E-STOP` -> resolve issue -> re-home/re-verify as required by controller.

## Machine Zero vs Work Zero

- Machine zero: fixed by homing, controller reference frame.
- Work zero (`G54`..`G59`): your part/program origin.
- Most job setup errors come from wrong or stale work offsets.

## XYZ Zero Setup (Mill/Router Workflow)

1. Home machine (`REF ALL` / `HOME`) after power-up.
2. Install tool and verify tool length method (manual setter, probe, or tool table).
3. Set `X` and `Y` work zero:
   - Jog to chosen part datum (corner/center/feature).
   - Zero or write offset for `G54 X` and `G54 Y`.
4. Set `Z` work zero:
   - Jog down using low increment.
   - Use paper/feeler gauge, touch plate, or tool setter.
   - Store `G54 Z` (or tool length offset + work offset per controller method).
5. Confirm active coordinate system (`G54`) and units (`G20`/`G21`).
6. Run dry pass above stock to verify path and clearance.

## Pre-Run Checklist

- Correct program and post-processor for your controller.
- Correct tool loaded and tool number/offset active.
- Workholding tight; clamps clear toolpath.
- Correct spindle direction/speed and coolant strategy.
- Starting line and safe retract verified.
- Feed/rapid override reduced for first proof run.

## Notes Template (Fill Per Machine Model)

- Controller model:
- Location of `E-STOP`:
- Button/softkey for `HOME`:
- Button/softkey for `G54` page:
- Procedure to set `X/Y`:
- Procedure to set `Z`:
- Tool length offset method:
- Safe startup block used at this shop:
- Common alarms and fixes:

## Model-Specific Cheat Sheet (Fill This First)

Use this section as the exact operating reference for your machine model.

- Machine make/model:
- Controller model/version:
- Axis travel limits (X/Y/Z):
- Default mode for startup:
- Exact button for `AUTO`:
- Exact button for `MDI`:
- Exact button for `JOG/HANDLE`:
- Exact key sequence to open work offset page (`G54`):
- Exact key sequence to open tool offset page (`H`/length):
- Tool-change procedure used on this machine (`T#`, `M6`, ATC key flow):
- Spindle warm-up routine:
- Safe retract position before tool change:
- Required overrides for first prove-out run:

## Red-Ball Probe Workflow (Touch Probe / Electronic Edge Finder)

If your machine uses a conductive stem with a red ball and touch detection, follow this process.

### What It Does

- Detects contact location between probe ball and work surface.
- Software/macro compensates by probe radius (`ball diameter / 2`) to find true edge/center.

### Setup

1. Confirm probe is electrically detected (touch test in diagnostics if available).
2. Enter probe ball diameter exactly in the probing macro/settings.
3. Set low jog/feed for probing moves.
4. Ensure spindle is stopped unless your procedure explicitly requires otherwise.

### Find One Edge (X Example)

1. Move close to left edge in `JOG`.
2. Run probe move toward edge until contact is detected.
3. Record contact position `X_touch`.
4. Compute true edge:
   - If probing from left toward +X: `X_edge = X_touch + ball_radius`
   - If probing from right toward -X: `X_edge = X_touch - ball_radius`

### Find True Center (Recommended: Opposite-Side Method)

1. Probe left side and record `X_left_touch`.
2. Probe right side and record `X_right_touch`.
3. Compute center:
   - `X_center = (X_left_touch + X_right_touch) / 2`
4. Repeat for Y:
   - `Y_center = (Y_front_touch + Y_back_touch) / 2`

Note: when both opposite sides are measured with the same probe, radius error mostly cancels in the average.

### Apply Work Zero

1. Move to computed center (`X_center`, `Y_center`).
2. Set `G54 X` and `G54 Y` to zero at that point.
3. Set `Z` using your normal touch plate/paper/tool setter method.
4. Run air cut proof before cutting stock.

### Common Probe Errors

- Wrong ball diameter in settings -> consistent offset error.
- Probe not electrically connected -> no trigger or false trigger.
- Chip/coolant film on contact surfaces -> noisy or early trigger.
- Too-fast probe feed -> overshoot and bad repeatability.
