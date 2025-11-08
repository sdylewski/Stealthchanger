---
title: Slicers & Printing
nav_order: 4
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Slicers & Printing

After [installing](Installation.md), [configuring](Configuration.md), and [calibrating](Calibration.md) klipper-toolchanger-easy, you need to set up your slicer to work with the toolchanger system.

## Print Start Macro

klipper-toolchanger-easy provides a `PRINT_START` macro that must be used. It initializes the toolchanger, performs homing and QGL, and handles tool selection and heating. Your slicer should call it with the following parameters:

**Required Parameters:**
- `TOOL` - The initial tool number to use (e.g., `0`, `1`, `2`)
- `TOOL_TEMP` - The temperature for the initial tool
- `BED_TEMP` - The bed temperature

**Optional Parameters (for multi-tool prints):**
- `T0_TEMP`, `T1_TEMP`, `T2_TEMP`, etc. - Pre-heat temperatures for tools that will be used in the print

**Example:**
```gcode
PRINT_START TOOL=0 TOOL_TEMP=220 BED_TEMP=60 T0_TEMP=220 T1_TEMP=230
```

**What the macro does:**
1. Initializes the toolchanger (`INITIALIZE_TOOLCHANGER`)
2. Stops tool probe crash detection
3. Heats the bed to `BED_TEMP`
4. Homes all axes (`G28`)
5. Selects T0
6. Runs Quad Gantry Level (`QUAD_GANTRY_LEVEL`)
7. Re-homes Z after QGL
8. Selects the specified `TOOL` and heats it to `TOOL_TEMP`
9. Pre-heats other tools if `T0_TEMP`, `T1_TEMP`, etc. are provided
10. Restarts tool probe crash detection

**Important:** Do not override the `PRINT_START` macro. If you need custom startup behavior, modify the macro in `stealthchanger/macros.cfg` or use the provided hooks.

**Note:** The `_PARK_ON_COOLING_PAD` macro in `PRINT_START` is not needed for StealthChanger and can be commented out or removed if present.

## Overview

1. [Slicer Software](#slicer-software) - Supported slicers for multi-tool printing
2. [Slicer GCODEs](#slicer-gcodes) - Required start G-code and tool change G-code for each slicer

## Slicer Software

| Name | Multitool | Issue | Discussion | Notes |
|:------:|:------:|:------:|:------:|------|
| Cura | <span style="color: green;">✓</span> | | | As of 5.8, select new printer, select DraftShift Design, select the size from the voron list, allows up to 8 extruders |
| OrcaSlicer | <span style="color: green;">✓</span> | | | As of 2.2 |
| PrusaSlicer | <span style="color: green;">✓</span> | | | |
| Simplify3D | <span style="color: silver;">?</span> | | | |
| Slic3r | <span style="color: silver;">?</span> | | | |
| SuperSlicer | <span style="color: green;">✓</span> | | | See [2197](https://github.com/supermerill/SuperSlicer/issues/2197) |

## Slicer GCODEs

### Prusa

Printer -> Custom G-code -> **Start G-code** - all must be a single line
```
PRINT_START TOOL_TEMP={first_layer_temperature[initial_tool]} {if is_extruder_used[0]}T0_TEMP={first_layer_temperature[0]}{endif} {if is_extruder_used[1]}T1_TEMP={first_layer_temperature[1]}{endif} {if is_extruder_used[2]}T2_TEMP={first_layer_temperature[2]}{endif} {if is_extruder_used[3]}T3_TEMP={first_layer_temperature[3]}{endif} {if is_extruder_used[4]}T4_TEMP={first_layer_temperature[4]}{endif} {if is_extruder_used[5]}T5_TEMP={first_layer_temperature[5]}{endif}  BED_TEMP=[first_layer_bed_temperature] TOOL=[initial_tool]
```

Printer -> Custom G-code -> **Tool change G-code**
```
M104 S{temperature[next_extruder]} T[next_extruder] ; set new tool temperature so it can start heating while changing
```

**NOTE**: add this as a second line if you use prime tower
```
G1 X{wipe_tower_x} Y{wipe_tower_y} F{travel_speed*60} ; Move to wipe tower before tool change
```

### Orca

Printer settings -> Machine G-code -> **Machine start G-code** - all must be a single line
```
PRINT_START TOOL_TEMP={first_layer_temperature[initial_tool]} {if is_extruder_used[0]}T0_TEMP={first_layer_temperature[0]}{endif} {if is_extruder_used[1]}T1_TEMP={first_layer_temperature[1]}{endif} {if is_extruder_used[2]}T2_TEMP={first_layer_temperature[2]}{endif} {if is_extruder_used[3]}T3_TEMP={first_layer_temperature[3]}{endif} {if is_extruder_used[4]}T4_TEMP={first_layer_temperature[4]}{endif} {if is_extruder_used[5]}T5_TEMP={first_layer_temperature[5]}{endif}  BED_TEMP=[first_layer_bed_temperature] TOOL=[initial_tool]
```

Printer settings -> Machine G-code -> **Change Filament G-code**
```
;Leave blank
```

### Cura

Machine Settings -> Printer -> **Start G-code** - all must be a single line

**For single tool prints:**
```
PRINT_START TOOL_TEMP={material_print_temperature_layer_0} BED_TEMP={material_bed_temperature_layer_0} TOOL={initial_extruder_nr}
```

**For multi-tool prints (Cura 5.8+):**
```
PRINT_START TOOL_TEMP={material_print_temperature_layer_0} T{initial_extruder_nr}_TEMP={material_print_temperature_layer_0} {if material_print_temperature_layer_0[1]!=0}T1_TEMP={material_print_temperature_layer_0[1]}{endif} {if material_print_temperature_layer_0[2]!=0}T2_TEMP={material_print_temperature_layer_0[2]}{endif} {if material_print_temperature_layer_0[3]!=0}T3_TEMP={material_print_temperature_layer_0[3]}{endif} {if material_print_temperature_layer_0[4]!=0}T4_TEMP={material_print_temperature_layer_0[4]}{endif} {if material_print_temperature_layer_0[5]!=0}T5_TEMP={material_print_temperature_layer_0[5]}{endif} BED_TEMP={material_bed_temperature_layer_0} TOOL={initial_extruder_nr}
```

Machine Settings -> Printer ->  Tool n -> **Extruder Start G-code**
```
;Leave blank
```

Machine Settings -> Printer ->  Tool n -> **Pre tool change G-code** - 5.10+
```
M104 S{material_print_temperature} T{extruder_nr}
```

---

**Optional Next Steps:**
- [LEDs](LEDs.md) → Configure color LEDs and lighting effects
