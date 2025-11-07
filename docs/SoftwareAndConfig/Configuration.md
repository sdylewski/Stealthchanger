---
title: Configuration
nav_order: 2
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Configuration

After installing [klipper-toolchanger-easy](Installation.md), you need to configure it for your specific setup. This guide covers the essential configuration steps.

**Important:** Tool numbering starts at 0 and counts up. For all configs, ensure you change all sections accordingly. For example, in your T1 config, use `extruder1`, `fan1`, etc. **The only exception is T0 - the extruder has no number (just `extruder`, not `extruder0`).**

## Configuration Overview

1. [Toolhead Configuration](#toolhead-configuration)
2. [Toolchanger Settings](#toolchanger-settings)
3. [Offsets](#offsets)
4. [Dock Positions](#dock-positions)
5. [close_y and safe_y](#close_y-and-safe_y)
6. [Docking Path](#docking-path)
7. [Print Start Macro](#print-start-macro)

## Toolhead Configuration

Each toolhead needs its own configuration file. These are located in `stealthchanger/tools/Tx.cfg` (e.g., `T0.cfg`, `T1.cfg`, etc.).

### Example Configuration Files

Reference configuration files are available in the [StealthChanger Klipper repo](https://github.com/DraftShift/StealthChanger/tree/main/Klipper). Use these as starting points and customize them with your specific values.

### Setting Up Tool Files

1. **Copy the example tool config** from the StealthChanger repo or klipper-toolchanger-easy
2. **Rename and number appropriately:** `T0.cfg`, `T1.cfg`, `T2.cfg`, etc.
3. **Update all references:**
   - T0: `extruder`, `heater`, `fan`, etc. (no numbers)
   - T1: `extruder1`, `heater1`, `fan1`, etc.
   - T2: `extruder2`, `heater2`, `fan2`, etc.
4. **Include in printer.cfg:**
   ```ini
   [include stealthchanger/tools/T0.cfg]
   [include stealthchanger/tools/T1.cfg]
   # ... etc for each tool
   ```

5. **Remove or move** your existing extruder/hotend config from `printer.cfg` (it's now in the tool files)

### Important Tool Configuration Notes

- **`t_command_restore_axis`:** Should be set to `z` (or `XYZ` if you want to restore all axes). If blank, set it to `z`.
- **Tool detection:** Each tool needs an `[tool_probe]` section with the OctoTap sensor configured
- **Fans:** Use `fan: Tx_partfan` format in the `[tool]` section (not `multi_fan` or `fan_generic`)

## Toolchanger Settings

The main toolchanger configuration is in `stealthchanger/toolchanger-config.cfg`. Key settings to configure:

### Homing Override

Configure `homing_override_config` to match your homing sequence. This typically includes:
- X and Y homing (sensorless or endstops)
- Z homing using the tool probe
- Quad gantry leveling (QGL)

### Calibration Switch (Optional)

If using a calibration probe (Sexball, Nudge, etc.), configure the `_CALIBRATION_SWITCH` section with your probe's endstop pin.

### Tool Calibration Settings

Configure `tools_calibrate` section if you want to use automatic calibration routines.

## Offsets

There are 2 places to set offsets in your toolhead config files. There is gcode_(x/y/z)_offset in the [tool] section, and (x/y/z)_offset in the [tool_probe] section. These do different things. The ones in the [tool] section are always relative to a specific tool. IE, if you homed with T0, then the gcode offsets are relative to T0. When you do multi-material prints, you will have to choose 1 tool to always do the homing, even if you don't use it, because all the other offsets need to be set against it. The [tool_probe] offset is only ever applied when homing with that tool. The gcode offsets are applied when changing a tool.

You should set all the `[tool_probe]` offsets as well though. If you are only using a single tool, you can home with that tool, and it will use the offset in the `[tool_probe]` section. You won't need to home with your primary tool first then before you start a print. 

To try and further clarify. Lets say you have 3 tools, T0, T1, and T2. We will say that T0 is your "primary" tool. Setup the probe z_offset like you would any other printer. Make sure the offset is set in `z_offset` (IE, make sure when you home and go to Z 0, the nozzle is actually in that spot). Its location in x/y/z is always going to be 0 in relation to the other tools. So after T0 is homed, T1 and T2 (may) need to have their `gcode_(x/y/z)_offset` changed so they match the location that the primary tool actually is. There are 2 main ways of doing this. You can use a test print to print layers on top of or next to each other (something like this: [Nozzle Alignment Assist](https://www.printables.com/model/109267-nozzle-alignment-assist)) or you can use a camera (something like [kTAMV Klipper Tool Alignment](https://github.com/TypQxQ/kTAMV) or [IDEX Nozzle Calibration Tool](https://github.com/Life0fBrian/Brians-IDEX-Nozzle-Calibration-tool)).

## Dock Positions

When setting your dock position in your tool config, X and Y are pretty self explanatory. Put the tool in the right spot for it to sit. However, Z should be the point where 1 more mm down will untrigger the tap module. 

## close_y and safe_y

It is important to get this right. If you don't, you will have changing issues, or crash your tools into your docks. This is where we recommend you start:

- close_y = park_y + 30
- safe_y = park_y + thickness of your thickest tool (plus a little buffer)

IE, if you Y park position is -15. Your close Y should be 15. If your Y park position is 0, it should be 30. Safe Y should be slighty further out. 

## Docking Path

The docking path (`params_sc_path` or `params_path`) defines the movement sequence when picking up or dropping off tools. This can be confusing, so let's break it down.

### Path Format

The path is a list of relative movements from the park position. Movements are executed **left to right** when dropping off, and **right to left** when picking up.

### Example Path

```python
params_sc_path: [
    {'y':9.5, 'z':4}, 
    {'y':9.5, 'z':2}, 
    {'y':5.5, 'z':0}, 
    {'z':0, 'y':0, 'f':0.5}, 
    {'z':-10, 'y':0}, 
    {'z':-10, 'y':16}
]
```

### Path Breakdown

Assuming your park position is `x=20, y=-10, z=240` and `close_y=20`:

**When dropping off (left to right):**
1. `{'y':9.5, 'z':4}` → Move to `x=20, y=-0.5, z=244` (approach from above)
2. `{'y':9.5, 'z':2}` → Move to `x=20, y=-0.5, z=242` (lower slightly)
3. `{'y':5.5, 'z':0}` → Move to `x=20, y=-4.5, z=240` (get closer)
4. `{'z':0, 'y':0, 'f':0.5}` → Slowly move to park position `x=20, y=-10, z=240` (f is feedrate/speed)
5. `{'z':-10, 'y':0}` → Lower to `z=230` to start unhooking
6. `{'z':-10, 'y':16}` → Move to `z=230, y=6` to clear the tool

**When picking up (right to left):**
The sequence runs in reverse, starting from the tool's dock position and ending at `close_y`.

### Tips for Path Configuration

- Start with the example path and adjust based on your dock positions
- Use small movements near the dock to avoid collisions
- The `f` parameter controls speed (0.5 = 50% of configured speed)
- Test paths carefully using `TEST_TOOL_DOCKING` before printing

## Print Start Macro

klipper-toolchanger-easy provides a `PRINT_START` macro that must be used. It initializes the toolchanger and handles tool selection. Your slicer should call it with parameters:

```gcode
PRINT_START TOOL_TEMP={temperature} BED_TEMP={bed_temp} TOOL={tool_number}
```

**Important:** Do not override the `PRINT_START` macro. If you need custom startup behavior, modify the macro in `stealthchanger/macros.cfg` or use the provided hooks.

**Note:** The `_PARK_ON_COOLING_PAD` macro in `PRINT_START` is not needed for StealthChanger and can be commented out or removed if present.
