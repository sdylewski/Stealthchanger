---
title: PRINT_START Macro Example
parent: Examples
---

# PRINT_START Macro Example

This is an example `PRINT_START` macro compatible with klipper-toolchanger-easy. This macro initializes the toolchanger, performs homing and QGL, and handles tool selection and heating.

**Important:** klipper-toolchanger-easy provides a `PRINT_START` macro by default. This example shows what the macro does and can be used as a reference if you need to customize it. If you need custom startup behavior, modify the macro in `stealthchanger/macros.cfg` or use the provided hooks.

**Note:** The `_PARK_ON_COOLING_PAD` macro call (if present) is not needed for StealthChanger and can be commented out or removed.

{% raw %}
```ini
[gcode_macro PRINT_START]
description: "Initialize toolchanger, home, QGL, and prepare for printing"
gcode:
    # Initialize toolchanger
    INITIALIZE_TOOLCHANGER
    
    # Stop tool probe crash detection during startup
    STOP_TOOL_PROBE_CRASH_DETECTION
    
    # Set bed temperature
    M140 S{params.BED_TEMP|default(60)|float}
    
    # Home all axes
    G28
    
    # Select T0 for QGL (always use T0 for final QGL and Z homing)
    T0
    
    # Heat nozzle to 150C for QGL (softens any leftover filament)
    M109 S150
    
    # Run Quad Gantry Level
    QUAD_GANTRY_LEVEL
    
    # Re-home Z after QGL
    G28 Z
    
    # Stop heating (actual tool will be selected and heated next)
    M109 S0
    
    # Pre-heat tools that will be used in the print
    {% for tool_nr in printer.toolchanger.tool_numbers %}
        {% set tooltemp_param = 'T' ~ tool_nr|string ~ '_TEMP' %}
        {% if tooltemp_param in params %}
            M104 T{tool_nr} S{params[tooltemp_param]|float}
        {% endif %}
    {% endfor %}
    
    # Select the initial tool for printing
    {% if params.TOOL is defined %}
        T{params.TOOL|int}
    {% else %}
        T0  # Default to T0 if not specified
    {% endif %}
    
    # Heat the initial tool to printing temperature
    M109 S{params.TOOL_TEMP|default(220)|float}
    
    # Restart tool probe crash detection
    START_TOOL_PROBE_CRASH_DETECTION
    
    # Optional: Prime the nozzle (uncomment if needed)
    # G92 E0
    # G1 Z0.2 F3000
    # G1 X10 Y10 E5 F1000
    # G92 E0
```
{% endraw %}

## Parameters

**Required:**
- `TOOL` - The initial tool number to use (e.g., `0`, `1`, `2`)
- `TOOL_TEMP` - The temperature for the initial tool
- `BED_TEMP` - The bed temperature

**Optional (for multi-tool prints):**
- `T0_TEMP`, `T1_TEMP`, `T2_TEMP`, etc. - Pre-heat temperatures for tools that will be used in the print

## Example Usage

**Single tool print:**
```gcode
PRINT_START TOOL=0 TOOL_TEMP=220 BED_TEMP=60
```

**Multi-tool print:**
```gcode
PRINT_START TOOL=0 TOOL_TEMP=220 BED_TEMP=60 T0_TEMP=220 T1_TEMP=230 T2_TEMP=250
```

## What This Macro Does

1. Initializes the toolchanger (`INITIALIZE_TOOLCHANGER`)
2. Stops tool probe crash detection
3. Sets and waits for bed temperature (`M140` / `M190`)
4. Homes all axes (`G28`)
5. Selects T0 (always used for QGL)
6. Heats T0 to 150°C for QGL
7. Runs Quad Gantry Level (`QUAD_GANTRY_LEVEL`)
8. Re-homes Z after QGL
9. Pre-heats other tools if `T0_TEMP`, `T1_TEMP`, etc. are provided
10. Selects the specified `TOOL` and heats it to `TOOL_TEMP`
11. Restarts tool probe crash detection

## Customization

If you need to customize the `PRINT_START` macro:

1. **Do not override it** - Instead, modify the macro in `stealthchanger/macros.cfg`
2. **Use hooks** - klipper-toolchanger-easy may provide hooks for customization
3. **Common additions:**
   - Nozzle cleaning (`_CLEAN_NOZZLE`)
   - Bed mesh calibration (`BED_MESH_CALIBRATE`)
   - Prime lines or purge sequences
   - LED status indicators

**Note:** Always ensure T0 is used for the final QGL and Z homing, as this is critical for accurate tool alignment.

