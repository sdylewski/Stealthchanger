---
title: Endstops
nav_order: 7
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
<!-- This page has the liquid html rendering image off so the gcode renders properly -->

# What 

The gantry needs to home its X and Y position, preferably with repeated accuracy as the X,Y position becomes important to pick up and drop off toolheads properly.

The X endstop on a toolhead will no longer work so that needs to be relocated or discarded altogether.

# Options

## Sensorless homing

Most common, easiest, just fiddly to get right, especially with TMC5160 drivers.
https://docs.vorondesign.com/tuning/sensorless.html


## Relocation mod
This moves X and Y endstops to the motor mount, there are a couple of options:

* [DraftShift Design](https://github.com/DraftShift/StealthChanger/tree/main/STLs/Endstops)
* [Endstop by Vin-Y](https://github.com/sdylewski/StealthChanger/tree/main/UserMods/VIN-y/Endstops)
* [Endstop mounts for printed and CNC shuttle](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/Endstop_Mounts)
  
## Endstop repeatability macro 
By @Contomo

Run with `TEST_ENDSTOP_REPEATABILITY AXIS=X`

{% raw %}
```
[gcode_macro TEST_ENDSTOP_REPEATABILITY]
variable_cache: {}
gcode:
    {% set axis    = params.get('AXIS','')|upper %}
    {% set cycles  = params.get('CYCLES', 10)|int %}
    {% set retract = params.get('RETRACT', 5)|float %}

    {% if axis not in ['X','Y','Z'] %}
        { action_respond_info("AXIS must be X, Y or Z") }
    {% elif cycles < 2 %}
        { action_respond_info("CYCLES must be ≥ 2") }
    {% else %}
        {% set step_name = 'stepper_' ~ axis|lower %}
        SET_GCODE_VARIABLE MACRO=TEST_ENDSTOP_REPEATABILITY VARIABLE=cache VALUE="{ { 'name': step_name, 'l': [] } }"
        {% set sign = '-' if printer.configfile.settings[step_name].get('homing_positive_dir', False) else '' %}
        { action_respond_info("Running test on %s-axis — %d cycles, retract %.2f mm" % (axis, cycles, retract)) }
        {% for i in range(cycles) %}
            G28 {axis}
            M400
            _TEST_ENDSTOP_REPEATABILITY RECORD={axis}
            G91
            G0 {axis}{sign}{retract}      ; relative retract
            G90
            M400
            G4 P100
        {% endfor %}
        _TEST_ENDSTOP_REPEATABILITY PROCESS={axis}
    {% endif %}
```
{% endraw %}

Depending on how strong the umbilical affects the toolhead in the corners, it might be more accurate to return to the center position before homing the other axis, that way the homing is always done in the middle of the gantry and any effect of umbilicals or gantry being racked does not affect the homing precision.






