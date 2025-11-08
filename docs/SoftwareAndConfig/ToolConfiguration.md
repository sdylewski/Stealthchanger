---
title: Tool Configuration
nav_order: 2
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Tool Configuration

After installing [klipper-toolchanger-easy](Installation.md), you need to configure it for your specific setup. This guide covers the essential configuration steps.

**Important:** Tool numbering starts at 0 and counts up. For all configs, ensure you change all sections accordingly. For example, in your T1 config, use `extruder1`, `fan1`, etc. **The only exception is T0 - the extruder has no number (just `extruder`, not `extruder0`).**

## Post-Installation Setup

After installation, the following directory structure is created in your config folder:
- `stealthchanger/` - Main toolchanger directory
- `stealthchanger/tools/` - Tool configuration files (T0.cfg, T1.cfg, etc.)
- `stealthchanger/toolchanger-config.cfg` - Main toolchanger configuration

You need to configure:

1. **Tool files:** Update `stealthchanger/tools/Tx.cfg` for each tool (T0.cfg, T1.cfg, etc.)
2. **Toolchanger settings:** Update `stealthchanger/toolchanger-config.cfg`:
   - `homing_override_config` - Your homing sequence
   - `_CALIBRATION_SWITCH` section - If using a calibration probe
   - `tools_calibrate` - Tool calibration settings

**Important Notes:**
- If using sensorless Y homing, ensure `homing_retract_dist` in `[stepper_y]` is set to `0` as per [Voron Docs](https://docs.vorondesign.com/community/howto/clee/sensorless_xy_homing.html)
- If you make manual changes to the installed files, they will be overwritten when Moonraker updates. Use the configuration override files instead.

## Configuration Overview

1. [Toolhead Configuration](#toolhead-configuration)
2. [Toolchanger Settings](#toolchanger-settings)
3. [Dock Positions](#dock-positions)
4. [close_y and safe_y](#close_y-and-safe_y)
5. [Docking Path](#docking-path)
6. [Print Start Macro](#print-start-macro)

## Toolhead Configuration

Each toolhead needs its own configuration file. These are located in `stealthchanger/tools/Tx.cfg` (e.g., `T0.cfg`, `T1.cfg`, etc.).

### Example Configuration Files

**For klipper-toolchanger-easy:** Example tool configuration files compatible with klipper-toolchanger-easy are available in the [Examples directory](Examples/):

**Generic Examples (EBB36 pin names):**
- [T0 configuration example](Examples/T0.md) - Tool 0 configuration template
- [T1 configuration example](Examples/T1.md) - Tool 1+ configuration template

**Board-Specific Examples (with correct pin names for each board):**
- **EBB36:** [T0](Examples/EBB36_T0.md) | [T1](Examples/EBB36_T1.md)
- **Nighthawk36:** [T0](Examples/Nighthawk36_T0.md) | [T1](Examples/Nighthawk36_T1.md)
- **SHT36:** [T0](Examples/SHT36_T0.md) | [T1](Examples/SHT36_T1.md)

**Note:** The examples in the [StealthChanger Klipper repo](https://github.com/DraftShift/StealthChanger/tree/main/Klipper) use the older klipper-toolchanger format (`multi_fan`, `params_sc_path`) and are not compatible with klipper-toolchanger-easy. Use the examples in the Examples directory instead.

### Setting Up Tool Files

1. **Copy the example tool config** from the [Examples directory](Examples/) based on your toolhead board type:
   - **EBB36:** Use [EBB36 T0](Examples/EBB36_T0.md) and [EBB36 T1](Examples/EBB36_T1.md) examples
   - **Nighthawk36:** Use [Nighthawk36 T0](Examples/Nighthawk36_T0.md) and [Nighthawk36 T1](Examples/Nighthawk36_T1.md) examples
   - **SHT36:** Use [SHT36 T0](Examples/SHT36_T0.md) and [SHT36 T1](Examples/SHT36_T1.md) examples
   - **Other boards or generic:** Use [T0 configuration example](Examples/T0.md) and [T1 configuration example](Examples/T1.md) (uses EBB36 pin names as default)
2. **Copy to your config directory:** Place the files in `stealthchanger/tools/` as `T0.cfg`, `T1.cfg`, `T2.cfg`, etc.
3. **Update all references for each tool:**
   - T0: `extruder` (no number), `fan: T0_partfan`, `heater: extruder`, etc.
   - T1: `extruder1`, `fan: T1_partfan`, `heater: extruder1`, etc.
   - T2: `extruder2`, `fan: T2_partfan`, `heater: extruder2`, etc.
4. **Customize for your hardware:**
   - Update MCU CAN bus UUIDs
   - Update pin assignments for your toolhead board
   - Update extruder rotation_distance and gear_ratio
   - Calibrate probe z_offset
   - Set dock park positions (params_park_x/y/z)
5. **Include in printer.cfg:**
   ```ini
   [include stealthchanger/tools/T0.cfg]
   [include stealthchanger/tools/T1.cfg]
   # ... etc for each tool
   ```

6. **Remove or move** your existing extruder/hotend config from `printer.cfg` (it's now in the tool files)

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

**Example Configuration:**

See [toolchanger-config.cfg example](Examples/toolchanger-config.cfg) for a reference implementation. Copy the relevant `[homing_override]` section to your `stealthchanger/toolchanger-config.cfg` and adjust the G28 commands based on your specific homing setup (sensorless vs switch-based for X and Y axes).

### Calibration Switch (Optional but recommended)

If using a calibration probe (Sexball, Nudge, etc.), configure the `_CALIBRATION_SWITCH` section with your probe's endstop pin. See [Calibration](Calibration.md) for detailed calibration setup and procedures.

## Dock Positions

When setting your dock position in your tool config, X and Y are pretty self explanatory. Put the tool in the right spot for it to sit. However, Z should be the point where 1 more mm down will untrigger the tap module.

**Note:** Detailed instructions for calibrating dock positions are covered in the [Dock Calibration](DockCalibration.md) section. You'll configure `params_park_x`, `params_park_y`, and `params_park_z` for each tool during calibration. 

## close_y and safe_y

It is important to get this right. If you don't, you will have changing issues, or crash your tools into your docks. This is where we recommend you start:

- close_y = park_y + 30
- safe_y = park_y + thickness of your thickest tool (plus a little buffer)

For example, if your Y park position is -15. Your close Y should be 15. If your Y park position is 0, it should be 30. Safe Y should be slighty further out.


**Example with park_y = -15:**
- `park_y = -15` (tool docked)
- `close_y = 15` (park_y + 30 = -15 + 30 = 15)
- `safe_y = 25+` (park_y + tool thickness + buffer, e.g., -15 + 40 = 25)

**Note:** These values are configured in `stealthchanger/toolchanger-config.cfg` and are covered in detail in the [Dock Calibration](DockCalibration.md) section. 

## Docking Path

The docking path (`params_sc_path` or `params_path`) defines the movement sequence when picking up or dropping off tools. This can be confusing, so let's break it down.

### Path Format

Paths are lists of relative movements from the park position. In klipper-toolchanger-easy:
- **Dropoff path** (`params_dropoff_path`): Executes **left to right** (top to bottom in the list) when placing a tool in its dock
- **Pickup path** (`params_pickup_path`): Executes **left to right** (top to bottom in the list) when retrieving a tool from its dock

Each movement is relative to the previous position, not the park position.

### Example Path (klipper-toolchanger-easy)

klipper-toolchanger-easy uses separate `params_dropoff_path` and `params_pickup_path` for more precise control. These paths define the movement sequence when dropping off and picking up tools.

**Dropoff Path** - Used when placing a tool in its dock:
```python
params_dropoff_path: [
    {'y':9.5, 'z':4}, 
    {'y':9.5, 'z':2}, 
    {'y':5.5, 'z':0}, 
    {'z':0, 'y':0, 'f':0.5}, 
    {'z':-10, 'y':0}, 
    {'z':-10, 'y':16}
]
```

**Pickup Path** - Used when retrieving a tool from its dock:
```python
params_pickup_path: [
    {'z':-10, 'y':16}, 
    {'z':-10, 'y':0}, 
    {'z':0, 'y':0, 'f':0.5, 'verify':1}, 
    {'y':5.5, 'z':0}, 
    {'y':9.5, 'z':2}, 
    {'y':9.5, 'z':4}
]
```

### Path Breakdown

**Key Concepts:**
- All movements are **relative** to your `params_park_x`, `params_park_y`, and `params_park_z` positions
- The `f` parameter controls speed multiplier (0.5 = 50% of `params_path_speed`)
- The `verify:1` parameter in pickup paths checks that the tool is detected at that point
- Dropoff path executes **left to right** (top to bottom in the list)
- Pickup path executes **left to right** (top to bottom in the list) - it's already reversed from dropoff

**Example with park position `x=20, y=-10, z=240`:**

**Dropoff sequence:**
1. Start at park: `x=20, y=-10, z=240`
2. After step 1: `x=20, y=-0.5, z=244` (moved forward, raised)
3. After step 2: `x=20, y=-0.5, z=242` (lowered slightly)
4. After step 3: `x=20, y=-4.5, z=240` (moved closer, at park Z)
5. After step 4: `x=20, y=-10, z=240` (at exact park position, slow)
6. After step 5: `x=20, y=-10, z=230` (lowered to unhook)
7. After step 6: `x=20, y=6, z=230` (moved forward to clear)

**Pickup sequence:**
1. Start at dock clearance: `x=20, y=6, z=230`
2. After step 1: `x=20, y=6, z=230` (already at start position)
3. After step 2: `x=20, y=-10, z=230` (moved back to dock)
4. After step 3: `x=20, y=-10, z=240` (raised to park Z, moved to park Y at slow speed) - **`verify:1` checks tool detection here** - ensures the tool is properly engaged before continuing
5. After step 4: `x=20, y=-4.5, z=240` (moved back, starting to lift)
6. After step 5: `x=20, y=-0.5, z=242` (continued back, raised)
7. After step 6: `x=20, y=-0.5, z=244` (fully clear of dock)




### Tips for Path Configuration


- Adjust based on your dock positions - paths are relative to your `params_park_*` positions
- Use small movements near the dock to avoid collisions
- The `f` parameter controls speed (0.5 = 50% of configured speed)
- The `verify:1` parameter in pickup paths checks tool detection at that point
- Test paths carefully using `TEST_TOOL_DOCKING` before printing
- If using `params_sc_path`, it's used for both pickup and dropoff (reversed for pickup)
- If using `params_dropoff_path` and `params_pickup_path`, they are separate paths for each direction

---

**Next:** [Toolhead Calibration](Calibration.md) → Set up probe offsets and G-code offsets

## FAQ

### Can I skip a number in the tool numbering?
No, Klipper requires sequential numbering starting from 0. Skipping a number (e.g., having T0 and T2 but no T1) will cause Klipper to complain. Tools must be numbered sequentially: T0, T1, T2, etc.

### The wrong tool heats up
Make sure *all* of your `extruder` references are correct per tool and you didn't forget to change one. Use `extruder` for T0, `extruder1` for T1 and so on. For example, `[tmc2209 extruder]` becomes `[tmc2209 extruder1]` for T1. Unfortunately, the different naming scheme of extruders for T0 (no number) makes it easy to miss `extruder` references when copying configurations.

### I'm getting weird behavior where the wrong tool gets selected, heated, part cooling fan is wrong, etc.
Make sure you don't accidentally have overridden any macros. If you copy T0.cfg to T1.cfg and forget to change any reference to T0, you'll run into weird behavior. Read through T1.cfg closely and make sure you don't have anything still referencing T0. G-code macro definitions will override the previously defined one (in T0.cfg). If you've forgotten to change the name of the g-code macro but have changed all references to T1 inside that macro, then when that macro is called for T0, it will do all the things it's supposed to with T1 instead of T0.

### What are these T0, T1, ... macros?
The slicer uses these macros to initiate a tool change to the given tool. `T1` is the equivalent of `SELECT_TOOL T=1`. These macros are automatically created by klipper-toolchanger-easy for each tool you configure.

### Can I park the active tool and not select a new one?
Yes, with `UNSELECT_TOOL`. If the macro is not available, make sure you have set `require_tool_present: False` in `[toolchanger]` in your `toolchanger-config.cfg`.

### I'm getting errors about a T3, I don't even have a T3
This happens when your slicer emits a `M106 P3 S0` or `M106 P2 S0` (if you have a T2 not assigned error). Disable the chamber exhaust fan and auxiliary cooling in your slicer. Slicers use P2 as auxiliary cooling fan and P3 as chamber fan, and these get interpreted as T2 or T3 by the software.

### I'm getting a Klipper error about multi_fan or fan_generic
You likely had an older install or copied the config from an older install. This was changed and the fan reference in each tool section `[tool]` is now `fan: Tx_partfan` (e.g., `fan: T0_partfan` for T0, `fan: T1_partfan` for T1).
