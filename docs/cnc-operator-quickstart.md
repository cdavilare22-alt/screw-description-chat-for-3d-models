# CNC Operator Quickstart (Buttons + XYZ Zero)

Use this as a practical training checklist. Control labels vary by machine (`Fanuc`, `Haas`, `Mach3/4`, `GRBL`, `Masso`, etc.), but the workflow is similar.

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
