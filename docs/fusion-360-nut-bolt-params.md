# Fusion 360 Nut-and-Bolt Parameter Template

Use these User Parameters so mount models update quickly when hardware size changes.

## Core Parameters

- `Fastener_Dia`
- `Clearance_Close`
- `Clearance_Normal`
- `Clearance_Loose`
- `Washer_OD`
- `Washer_Thickness`
- `Nut_AF`
- `Nut_Thickness`
- `NutTrap_AF`
- `NutTrap_Depth`
- `Boss_OD`
- `Edge_Min`

## Recommended Expressions

- `Boss_OD = Fastener_Dia * 2.0`
- `Edge_Min = Fastener_Dia * 2.0`
- `NutTrap_AF = Nut_AF + 0.30 mm` (adjust by printer calibration)
- `NutTrap_Depth = Nut_Thickness + 0.30 mm`

## Example Parameter Set (M5)

- `Fastener_Dia = 5.0 mm`
- `Clearance_Normal = 5.5 mm`
- `Washer_OD = 10.0 mm`
- `Washer_Thickness = 1.0 mm`
- `Nut_AF = 8.0 mm`
- `Nut_Thickness = 4.0 mm`
- `NutTrap_AF = 8.3 mm`
- `NutTrap_Depth = 4.3 mm`
- `Boss_OD = 10.0 mm`
- `Edge_Min = 10.0 mm`

## Example Parameter Set (1/4-20)

- `Fastener_Dia = 6.35 mm`
- `Clearance_Normal = 6.8 mm`
- `Washer_OD = 18.0 mm`
- `Washer_Thickness = 1.6 mm`
- `Nut_AF = 11.11 mm`
- `Nut_Thickness = 5.56 mm`
- `NutTrap_AF = 11.5 mm`
- `NutTrap_Depth = 6.0 mm`
- `Boss_OD = 12.7 mm`
- `Edge_Min = 12.7 mm`

## Workflow Tip

Create one parameter group per hardware family (for example `M5_*`, `QTR20_*`) and drive all holes/pockets from those parameters only.
