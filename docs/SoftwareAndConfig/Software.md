---
title: Software & Configuration
nav_order: 3
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Software & Configuration

Congratulations! You've built a StealthChanger with at least one toolhead and dock, and you're ready for the *real* fun. This section will guide you through installing, configuring, and calibrating your printer to get your first multi-colored print.

## Process Overview

Follow these steps in order:

1. **[Install](Installation.md)** klipper-toolchanger-easy - Set up the toolchanger software
2. **[Configure](Configuration.md)** all your parameters for each toolhead - Set up tool files, offsets, and dock positions
3. **[Calibrate](Calibration.md)** your Z offsets, toolhead XY offsets, and dock locations - Ensure accurate tool alignment
4. **[Setup your slicer](Slicers.md)** and print-start macros - Configure your slicer for multi-tool printing
5. **Print!** - Start your first multi-color print

## About klipper-toolchanger-easy

StealthChanger uses [klipper-toolchanger-easy](https://github.com/jwellman80/klipper-toolchanger-easy) for toolchanging functionality. This is a maintained fork of the original klipper-toolchanger project, specifically designed to be easier to install and configure.

**Key features:**
- Simple installation script
- Automatic Moonraker update management
- Comprehensive configuration examples
- Active development and support


# FAQ
SW Setup issues:
* if using "fan0 or fan2" from slicer, need to change those back to named fans.

### After a tool change the ooze of my toolhead gets deposited onto my print / the picked up tool drags over the print to the prime tower
By default after a tool change only the Z axis gets restored, that means whichever tool you pick up will return to center Y and X whatever your dock position of that tool is. If your print is in the path to the next move from the slicer it will not Z-hop (the slicer does not change Z) and drag over it, depositing any ooze the nozzle has on the print.

To mitigate that do the following:
1. Enable multitool ramming in your slicer. The slicer will move to the prime tower to do so
2. Restore not just Z but also X and Y, `t_command_restore_axis: XYZ`  in `[toolchanger]`. This will return the toolhead back from where the previous tool was in all 3 axes.
3. The pickup_gcode in `[toolchanger]` runs the restore path at the end. Raise the Z travel by a fixed amount, e.g. 5mm
  {% raw %}
   ```
    {% if 'Z' in restore_position %}
      #Travel with Z 5 higher to the restore position
      ROUNDED_G0 Z={restore_position.Z + 5} F={fast} D=150
    {% endif %}
   ```
   {% endraw %}
   After the pickup gcode has ran the toolchanging software will move the toolhead to the correct Z so no further change is necessary.

### Can I skip a number in the tool numbering?
No, Klipper requires sequential numbering starting from 0. Skipping a number will make it complain.

### The wrong tool heats up
Make sure *all* of your `extruder` references are correct per tool and you didn't forget to change one. Use `extruder` for T0, `extruder1` for T1 and so on. E.g. `[tmc2209 extruder]` becomes `[tmc2209 extruder1]` for T1 and so on. Unfortunately the different naming scheme of extruders for T0 makes it easy to gloss over `extruder` references. 

### I'm getting some weird behaviour where the wrong tool gets selected, heated, part cooling fan is wrong, etc.
Make sure you don't accidentally have overridden any macros. If you copy T0 cfg to T1 and forget to change any reference to T0 you'll run into weird behavior. Read through T1 cfg closely and make sure you don't have anything still referencing T0. Gcode macro definitions will override the previously defined one (in T0 cfg). If you've forgotten to change the name of the gcode macro but have changed all references to T1 inside that macro then when that macro is called for T0 it will do all the things it's supposed to with T1 instead of T0.

### What are these T0, T1, ... macros?
The slicer uses these macros to initiate a tool change to the given tool. `T1` is the equivalent of `SELECT_TOOL T=1`.

### Can I park the active tool and not select a new one?
Yes with `UNSELECT_TOOL`. If the macro is not available make sure you have set `require_tool_present: False` in `[toolchanger]`.

### I'm getting errors about a T3, I don't even have a T3
This happens when your slicer emits a `M106 P3 S0` or ` M106 P2 S0` (if you have a T2 not assigned error).
Disable the chamber exhaust fan and auxilary cooling in your slicer, slicers use P2 as auxilary cooling fan P3 as chamber fan and it gets interpreted as T2 or T3 by the software. 

### My pressure advance doesn't work
Make sure to put the PA values in your filament settings in the slicer. If you have multitool ramming enabled it will set pressure advance to 0 when ramming on the wipe tower and if it's not in the filament settings it can't put it back to what it's supposed to be during the print.

### My tool pickup failed and it halted klipper so the print is lost. Can I just not make it pause so it can recover and resume?
You can use the `error_gcode` and `recover_gcode` of toolchanger for this.

1. The tool is not being detected by the VERIFY_TOOL call in the pickup gcode (assuming your path has a 'verify': 1 somewhere)
2. It runs the `error_gcode` and puts the toolchanger software in an error state. Adding `PAUSE_BASE` in `error_gcode` will pause the printer. Do not use `PAUSE` if you have mainsail, mainsail overrides it to move the toolhead to the back and you don't want that.
3. Fix the toolhead issue and do everything to prepare the printer to continue. Put the toolhead on the shuttle and move the gantry to a safe position. It will move in a straight line (`G0`) to where the toolhead is supposed to go after the pickup so be careful!
4. Run `INITIALIZE_TOOLCHANGER RECOVER=1` to return to its normal state and run the `recover_gcode` section. Adding `RESUME_BASE` will resume in `recover_gcode` will resure the printer. Do not use `RESUME` if you have mainsail for the same reason as above.
5. The printer should now continue the print with the tool that failed to pick up.

### I'm getting a Klipper error about multi_fan or fan_generic
You likely had an older install or copied the config from an older install. This was changed and a fan reference each tool section `[tool]` is now `fan: Tx_partfan`.

### Can I use Kalico instead of mainline Klipper?
No, not at the moment.

### I'm getting "invalid syntax"
Make sure you are using at least python 3.





