---
title: Dock Calibration
nav_order: 4
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Dock Calibration

Dock positions define where each tool parks when not in use. This is critical for reliable tool changes.

## Setting Dock Positions

When setting your dock position in your tool config, X and Y are pretty self explanatory - put the tool in the right spot for it to sit. However, Z should be the point where 1 more mm down will untrigger the tap module.

## Calibration Methods

You can calibrate dock positions using either method:

- **[Dock Tuner](DockTuner.md) (Recommended)** - Interactive macro that guides you through the calibration process step-by-step
- **[Manual Calibration](#dock-parking-calibration-procedure)** - Manual method using console commands and M114

## Dock Parking Calibration Procedure (Manual Method)

**⚠️ WARNING:** When calibrating dock positions for T1, T2, or any non-T0 tool:
- **ALWAYS home with T0 first** (`G28` with T0 on the shuttle)
- **Then manually switch to Tn** (either manually place it on the shuttle or use T0 to pick it up)
- **DO NOT run `G28` or home with Tn** - This establishes Tn's coordinate system and will make your dock positions incorrect
- **Avoid running `INITIALIZE_TOOLCHANGER` with Tn during calibration** - While technically okay if your gcode_offsets are already perfectly calibrated, it applies offsets which can make M114 readings confusing. It's safer to skip it and work directly in T0's coordinate system.

Dock positions must be calibrated relative to T0's coordinate system. If you home with Tn, the dock positions will be wrong and tools will crash into docks during tool changes.

**IMPORTANT:** 
- Set `params_close_y` to your highest `params_park_y` + 30 in `toolchanger-config.cfg`
- Set `params_safe_y` to `params_close_y` + the thickness of your thickest tool + 10 in `toolchanger-config.cfg`
- **Remove these parameters from individual tool config files** - they should only be in the main toolchanger config

**Alternative for `params_safe_y`:** With a tool on the shuttle, move freely behind the dock without hitting any docked tools and note that Y position.

This sets the dock park position (`params_park_x`, `params_park_y`, `params_park_z`) for each tool in `stealthchanger/tools/Tn.cfg`.

**For T0:**
1. Put T0 on the shuttle and run `INITIALIZE_TOOLCHANGER`
2. Run `G28` and `QUAD_GANTRY_LEVEL` 
3. Remove T0 from the shuttle and place it in its [dock](../Docks.md)
4. Move the gantry as if to pick up the tool - watch for the [OctoTap](../Probes.md#tap) LED to change state (indicates tool detection)
5. Raise Z by 1mm to ensure clearance
6. Run `M114` and record the values to `params_park_x`, `params_park_y`, and `params_park_z` in `[tool T0]` of the tool config file (`stealthchanger/tools/T0.cfg`)
7. Run `G28` to return to home
8. Test the docking path: Run `SET_TOOL_PARAMETER PARAMETER='params_path_speed' VALUE=300`
9. Run `TEST_TOOL_DOCKING RESTORE_AXIS=XYZ` to verify the path works
10. Run `RESET_TOOL_PARAMETER PARAMETER='params_path_speed'` to restore normal speed

**For T1, T2, and other tools (CRITICAL - Read the warning above):**
1. **With T0 on the shuttle**, run `INITIALIZE_TOOLCHANGER` and `G28` to home with T0
2. Run `QUAD_GANTRY_LEVEL` 
3. **Manually switch to Tn** 
4. **Avoid running `INITIALIZE_TOOLCHANGER` with Tn** - While it's technically okay if your gcode_offsets are already correct, it applies offsets which can make M114 readings confusing. It's safer to work directly in T0's coordinate system. **DO NOT run `G28` with Tn** - This establishes Tn's coordinate system and will break calibration.
5. Remove Tn from the shuttle and place it in its [dock](../Docks.md)
6. Move the gantry as if to pick up the tool - watch for the [OctoTap](../Probes.md#tap) LED to change state (indicates tool detection)
7. Raise Z by 1mm to ensure clearance
8. Run `M114` and record the values to `params_park_x`, `params_park_y`, and `params_park_z` in `[tool Tn]` of the tool config file (`stealthchanger/tools/Tn.cfg`)
9. **Return to T0** - Manually place T0 back on the shuttle
10. Run `G28` to return to home
11. Test the docking path: Run `SET_TOOL_PARAMETER PARAMETER='params_path_speed' VALUE=300`
12. Run `TEST_TOOL_DOCKING RESTORE_AXIS=XYZ` to verify the path works
13. Run `RESET_TOOL_PARAMETER PARAMETER='params_path_speed'` to restore normal speed
14. Repeat this process for all remaining tools
15. Run `FIRMWARE_RESTART` to apply changes

## Docking/Undocking Movement

The movement using config parameters is as follows:

| Current tool | No tool | Next tool |
|--------------|---------|-----------|
| `safe_y`, `park_x` -> `park_z` -> `close_y` -> `path` | `close_y` -> `park_x` | `path` -> `safe_y` -> `t_command_restore_axis` |

---

**Next:** [Slicers & Printing](Slicers.md) → Configure your slicer for multi-tool printing

