---
title: Calibration
nav_order: 3
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Calibration

A multi-tool printer requires calibration. This page explains what to calibrate, and describes some of the useful tools and techniques.

## Calibration Overview

StealthChanger requires several types of calibration:

1. **[Probe Z Offset](#probe-z-offset-tool_probe-offsets)** - Sets where Z=0 is for each tool when homing
2. **[G-code Offsets](#g-code-offsets)** - Aligns nozzle positions between tools (X, Y, Z)
3. **[Dock Positions](#dock-positions)** - Sets where each tool docks when not in use
4. **[Tool Offset Calibration](#tool-offset-calibration)** - Measure and set X, Y, and Z offsets between tools

# Preparing to calibrate

Make sure you [set the preload
screws](../Shuttle.md#backplate-preload) on each backplate
before calibrating, since this affects the Z position of each [tool](../Toolheads/Toolheads.md). If you find
your Z calibration is drifting, it’s likely that one of the preload screws has
come loose.


**Before you start calibrating you should "break in" each tool probe.  Heat-soak
your machine and run a couple `PROBE_ACCURACY SAMPLES=100` per tool.**

## Probe Z Offset (`[tool_probe]` Offsets)

A Voron 2.4-style printer needs a bed probe in order to perform quad gantry leveling (QGL). The default on StealthChanger is to use the OptoTap board on each tool as the bed probe.

### How It Works

With this probing method, the tool will move downward until the nozzle contacts the bed. As the gantry continues to lower, the tool will slide upwards on the shuttle until the OptoTap board no longer registers the presence of the shuttle, at which point the probe is considered triggered. This is conceptually the same as [Voron Tap](https://github.com/VoronDesign/Voron-Tap), with the StealthChanger pins and bushings taking the place of the Tap linear rail.

### Understanding Probe Z Offset

- **Applied only when homing** with that specific tool
- **X and Y probe offsets are zero** - because the nozzle is the probe
- **Z offset** is specified by `z_offset` in `[tool_probe Tn]` (where Tn = T0, T1, etc.)
- **Always a negative number** - the trigger point is "below" the bed
- **Each tool has its own offset** - due to variation in assembly, preload screws, and OptoTap board

A more negative probe Z offset means less squish; a less negative (closer to zero) value means more squish, as the tool will not rise as far from the trigger point.

### Z_offset Calibration Procedure

1. Manually put a tool on the [shuttle](../Shuttle.md) and run `INITIALIZE_TOOLCHANGER`
2. Warm your nozzle to 150C or clean it well.
3. Run `G28` to home all axes
4. Run `QUAD_GANTRY_LEVEL` to level the gantry
5. Run `G28` again to re-home after QGL
6. Do a [Manual Paper Test](https://www.klipper3d.org/Bed_Level.html#the-paper-test) as normal (like a single toolhead printer) and adjust the Z
7. Copy the offset value and save it to `z_offset` in `[tool_probe Tn]` of the tool config file (`stealthchanger/tools/Tn.cfg`)
8. Repeat from step 1 for all tools
9. Run `FIRMWARE_RESTART` to apply changes

**Note:** It is typical to set up the print start macro such that T0 is always used for the final QGL and Z homing before printing. Then it is only necessary to fine-tune the probe Z offset on T0. Other tools need only be close enough for an initial Z homing before picking up T0.

**Tip:** Follow [Ellis's method](https://ellis3dp.com/Print-Tuning-Guide/articles/first_layer_squish.html) or the [paper test](https://www.klipper3d.org/Bed_Level.html#the-paper-test) to get the right amount of first-layer squish.

## G-code Offsets

G-code offsets align nozzle positions between tools so that parts of a model printed with different tools will line up correctly. This is necessary even with "identical" tools because of tolerances in parts and assembly.

### Understanding G-code Offsets

- **Applied when changing tools** during printing
- **Relative to your primary tool** (the one you always home with, typically T0)
- **Primary tool:** `gcode_*_offset = 0` (it's the reference)
- **Other tools:** Set to match the primary tool's position
- **Specified by:** `gcode_x_offset`, `gcode_y_offset`, and `gcode_z_offset` in `[tool Tn]`
- **Stable from print to print** - but may need adjustment if you rebuild a tool or have a crash

By convention, these offsets are set to 0 for T0. The offsets for other tools specify the distance that tool needs to move to place its nozzle in exactly the same position that T0's would be. This can be either positive or negative on each axis.

### Setup Process

**Single Tool:**
- Set `[tool_probe]` offsets - you're done
- Can home directly with that tool

**Multiple Tools:**
1. Choose a primary tool (typically T0)
2. Set primary tool's `[tool_probe]` offsets correctly
3. Set primary tool's `gcode_*_offset = 0`
4. Calibrate other tools' `gcode_*_offset` to match primary tool position
5. Always home with the primary tool

<div style="background-color: #e7f3ff; border-left: 4px solid #2196F3; padding: 12px; margin: 12px 0;">

**Note:** You can setup your printer to home with TN if you're only using that one tool during printing, but it requires a more advanced print_start macro (add link to example)

</div>

### G-code Z Offset Calibration Procedure

**IMPORTANT:** 
- Only home or probe with T0 during this calibration
- `gcode_z_offset` on Tool 0 is always 0 (T0 is the reference tool)
- Set probe Z offset for all tools first before doing G-code offsets

1. Set probe Z offset for all tools first
2. Make sure T0 is on the shuttle and run `INITIALIZE_TOOLCHANGER`
3. Run `G28` to home all axes
4. Run `QUAD_GANTRY_LEVEL` to level the gantry
5. Run `G28` again to re-home after QGL
6. Run `G1 Z10 F600` to move to a safe height
7. Manually remove the current tool and place the next tool (T1, T2, etc.) on the shuttle
8. Do a [Manual Paper Test](https://www.klipper3d.org/Bed_Level.html#the-paper-test) as normal and adjust the Z
9. Once done, run `M114` and copy the Z value to `gcode_z_offset` in `[tool Tn]` of the tool config file (`stealthchanger/tools/Tn.cfg`)
10. Repeat from step 6 for all remaining tools
11. Run `FIRMWARE_RESTART` to apply changes

### Calibration Methods

#### Manual Calibration (Test Prints)

The simplest but most tedious method is to print test objects like [this one](https://www.printables.com/model/201707-x-y-and-z-calibration-tool-for-idex-dual-extruder) or [Nozzle Alignment Assist](https://www.printables.com/model/109267-nozzle-alignment-assist). For X and Y you are looking at the [vernier scales](https://en.wikipedia.org/wiki/Vernier_scale); for Z you are looking to have the same amount of squish on both sides (remember, T0 squish is set by the probe Z offset, not G-code offset).

#### Mechanical Calibration Probes

A mechanical calibration probe is basically an endstop that can be triggered by the nozzle moving along any axis. By tapping the probe from ±X, ±Y and +Z directions, the position of the nozzle opening can be determined (assuming a clean nozzle that is bored concentric to its outer surfaces).

**Available Probes:**

- **[Sexball](https://github.com/DraftShift/StealthChanger/wiki/Bill-of-Materials#sexball-probe)** - Replaces the pin of hartk's Sexbolt endstop with a ball. LDO StealthChanger kits come with a Sexball probe and this is probably a good place to start for new users.
- **[Nudge](https://github.com/zruncho3d/nudge)** - Another popular calibration probe design
- **Multiple designs** in the [NozzleAlign](https://github.com/viesturz/NozzleAlign) repo

**Mounting:**

You can permanently mount any of these probes in the overtravel region at the front or rear of the bed. With Sexball it is easy to remove the ball and pin, so that tools do not collide during printing. Alternately, you can make the whole probe assembly removable, as long as you have some way to rigidly attach it on or near the bed for calibration.

**Configuration:**

Any of these probes is basically the same from the firmware perspective. Consult the [NozzleAlign](https://github.com/viesturz/NozzleAlign) docs for information on configuration and commands.

**Temperature:**

Due to thermal expansion, it is best to probe as close to printing conditions as possible, though you must also ensure that the nozzle stays clean and does not ooze. 150°C is a good default.

#### Optical Calibration (Camera Tools)

Another approach for XY offsets is to use a camera looking up at the nozzle.

**Hardware Options:**
- [CXC by Ember Prototypes](https://www.emberprototypes.com/products/cxc)
- [DIY version](https://www.printables.com/model/1099576-xy-nozzle-alignment-camera) using OV9726 camera module
- Any USB microscope, if you can mount it rigidly

**Software Options:**
- **[kTAMV](https://github.com/TypQxQ/kTAMV)** - Automatically locates the nozzle using machine vision
- **[IDEX Nozzle Calibration Tool](https://github.com/Life0fBrian/Brians-IDEX-Nozzle-Calibration-tool)** - Another camera-based calibration tool
- **[Axiscope](https://github.com/nic335/Axiscope)** - Provides a web interface for manually locating nozzles. This involves more manual effort than kTAMV, but is simpler and can be more reliable. Axiscope can also interact with a Sexbolt or other Z endstop to calculate Z offsets.

## Dock Positions

Dock positions define where each tool parks when not in use. This is critical for reliable tool changes.

### Setting Dock Positions

When setting your dock position in your tool config, X and Y are pretty self explanatory - put the tool in the right spot for it to sit. However, Z should be the point where 1 more mm down will untrigger the tap module.

### Dock Parking Calibration Procedure

**IMPORTANT:** 
- Set `params_close_y` to your highest `params_park_y` + 30 in `toolchanger-config.cfg`
- Set `params_safe_y` to `params_close_y` + the thickness of your thickest tool + 10 in `toolchanger-config.cfg`
- **Remove these parameters from individual tool config files** - they should only be in the main toolchanger config

**Alternative for `params_safe_y`:** With a tool on the shuttle, move freely behind the dock without hitting any docked tools and note that Y position.

This sets the dock park position (`params_park_x`, `params_park_y`, `params_park_z`) for each tool in `stealthchanger/tools/Tn.cfg`.

1. Put a tool on the shuttle and run `INITIALIZE_TOOLCHANGER`
2. Run `G28` and `QUAD_GANTRY_LEVEL` 
3. Remove the tool from the shuttle and place it in its [dock](../Docks.md)
4. Move the gantry as if to pick up the tool - watch for the [OctoTap](../Probes.md#tap) LED to change state (indicates tool detection)
5. Raise Z by 1mm to ensure clearance
6. Run `M114` and record the values to `params_park_x`, `params_park_y`, and `params_park_z` in `[tool Tn]` of the tool config file (`stealthchanger/tools/Tn.cfg`)
7. Run `G28` to return to home
8. Test the docking path: Run `SET_TOOL_PARAMETER PARAMETER='params_path_speed' VALUE=300`
9. Run `TEST_TOOL_DOCKING RESTORE_AXIS=XYZ` to verify the path works
10. Run `RESET_TOOL_PARAMETER PARAMETER='params_path_speed'` to restore normal speed
11. Repeat this process for all tools
12. Run `FIRMWARE_RESTART` to apply changes

### Docking/Undocking Movement

The movement using config parameters is as follows:

| Current tool | No tool | Next tool |
|--------------|---------|-----------|
| `safe_y`, `park_x` -> `park_z` -> `close_y` -> `path` | `close_y` -> `park_x` | `path` -> `safe_y` -> `t_command_restore_axis` |

## Tool Offset Calibration

A calibration probe (Sexball, Nudge, Axiscope, etc.) automatically measures the position differences between tools and sets the `gcode_x_offset`, `gcode_y_offset`, and `gcode_z_offset` values in your tool configuration files. This provides more accurate and repeatable tool alignment than manual calibration methods.

To use a calibration probe, configure the `_CALIBRATION_SWITCH` section in `stealthchanger/toolchanger-config.cfg` with your probe's endstop pin. This enables automatic calibration routines.

Example:
```ini
[_CALIBRATION_SWITCH]
pin: ^ar21  # Your calibration probe endstop pin
```

For information on available calibration probes and how to use them, see the [Mechanical Calibration Probes](#mechanical-calibration-probes) section below.

## Other Per-Tool Calibration

Additional calibration that may be needed per tool:

- **PID Tuning** - Each tool's heater may need PID tuning
- **E-steps** - Extruder steps per mm calibration
- **Input Shaper** - Vibration compensation (typically done once for the machine, not per tool)

These follow standard Klipper calibration procedures and are not specific to StealthChanger.

---

**Next:** [Slicers & Printing](Slicers.md) → Configure your slicer for multi-tool printing
