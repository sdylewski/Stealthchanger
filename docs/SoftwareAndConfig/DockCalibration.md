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

**Note:** For details on how the docking/undocking movement sequence works, see the [Docking/Undocking Movement](Configuration.md#dockingundocking-movement) section in the Configuration page.

---

**Next:** [Slicers & Macros](Slicers.md) → Configure your slicer and print_start macro for multi-tool printing

## FAQ

**Quick Links:**
- [Moving from and to the dock is so slow](#moving-from-and-to-the-dock-is-so-slow)
- [I can't get past 50mm/s Z velocity](#i-cant-seem-to-get-past-50mms-z-velocity-before-it-makes-really-angry-noises-and-skips-steps)
- [My tool pickup failed](#my-tool-pickup-failed-and-it-halted-klipper-so-the-print-is-lost-can-i-make-it-pause-so-it-can-recover-and-resume)

---

### Moving from and to the dock is so slow
You can increase the printer Z speed `max_z_velocity` and acceleration `max_z_accel`, depending on your motors and motor drivers. It's recommended to increase this in small steps because lost steps due to a loose belt will violently skew the gantry and might break your motor mounts. For example, 24V Moons motors with TMC2209 drivers can reliably get `max_z_velocity: 200` and `max_z_accel: 750` if the rest of the hardware is fine. That speed reduces dropoff/pickup to ~10 seconds.

### I can't seem to get past 50mm/s Z velocity before it makes really angry noises and skips steps
Make sure you have [StealthChop](https://www.klipper3d.org/TMC_Drivers.html#setting-spreadcycle-vs-stealthchop-mode) disabled on all of the Z motors. SpreadCycle is louder but gives much more torque that's required to run the Z velocity at a higher speed. If you have [TMC autotune](https://github.com/andrewmcgr/klipper_tmc_autotune), make sure to set the Z motors profile to `performance` - by default Z motors will be on the silent profile.

### My tool pickup failed and it halted Klipper so the print is lost. Can I make it pause so it can recover and resume?
You can use the `error_gcode` and `recover_gcode` of toolchanger for this:

1. The tool is not being detected by the VERIFY_TOOL call in the pickup gcode (assuming your path has a 'verify': 1 somewhere)
2. It runs the `error_gcode` and puts the toolchanger software in an error state. Adding `PAUSE_BASE` in `error_gcode` will pause the printer. Do not use `PAUSE` if you have Mainsail, as Mainsail overrides it to move the toolhead to the back and you don't want that.
3. Fix the toolhead issue and do everything to prepare the printer to continue. Put the toolhead on the shuttle and move the gantry to a safe position. It will move in a straight line (`G0`) to where the toolhead is supposed to go after the pickup, so be careful!
4. Run `INITIALIZE_TOOLCHANGER RECOVER=1` to return to its normal state and run the `recover_gcode` section. Adding `RESUME_BASE` in `recover_gcode` will resume the printer. Do not use `RESUME` if you have Mainsail for the same reason as above.
5. The printer should now continue the print with the tool that failed to pick up.

