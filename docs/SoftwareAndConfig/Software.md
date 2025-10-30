---
title: Software & Configuration
nav_order: 3
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

(Scott's notes page, needs to be updated)

# Software

Congratulations!  You've built a StealthChanger with at least 1 toolhead and/or dock, and you're ready for the *real* fun?  This will guide you through the process of installing, configuring, and calibrating your printer to get your first multi-colored print.

##Process

### 1. [Install](Installation.md) Klipper-toolchanger
### 2. [Configure](Configuration.md) all your parameters for each toolhead
### 3. [Calibrate](Calibration.md) your Z offsets, toolhead XY offsets, and dock locations.
### 4. [Setup your slicer](Slicers.md) and print-start macros
### 5. Print!



this page should give an overview of the software, plus:
* Detailed klipper-toolchanger and/or KTE install instructions
* Any configureation needed for the SW
* links to next pages for config or calibration?

Previous notes:

Sounds like I should use "Klipper-toolchanger-easy" instead of the default repo.  
* https://github.com/jwellman80/klipper-toolchanger-easy?tab=readme-ov-file
* Even when using klipper-toolchanger-easy, use the examples in the [Draftshift Klipper-toolchanger folder](https://github.com/DraftShift/klipper-toolchanger)
* Klipper-toolchanger-easy is just for installation.  After installing that, still follow the [stealthchanger wiki](https://github.com/DraftShift/StealthChanger/wiki/Calibration) for configuration and setup!
* Nudge XY calibration
* [Dock Tuner macro]((https://github.com/Contomo/klipper-toolchanger-hard/blob/main/examples/dock%20location/fixed/dock_tuner.cfg)  how to install?
* LEDs: [Example from Draftshift](https://github.com/DraftShift/klipper-toolchanger?tab=readme-ov-file) designs page
* [LED Effects](https://github.com/julianschill/klipper-led_effect) TBD

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






