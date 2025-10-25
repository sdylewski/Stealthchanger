---
title: Calibration
nav_order: 3
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

A multi-tool printer requires a lot of calibration. This page explains what to calibrate, and describes some of the useful tools and techniques.

# Preparing to calibrate

Make sure you [set the preload
screws](/StealthChanger/Shuttle.html#backplate-preload) on each backplate
before calibrating, since this affects the Z position of each tool. If you find
your Z calibration is drifting, it’s likely that one of the preload screws has
come loose.

FIXME: what to do about this

**Before you start calibrating you must "break in" each tool probe.  Heat-soak
your machine and run a couple `PROBE_ACCURACY SAMPLES=100` per tool.**

# Bed probing

A Voron 2.4-style printer needs a bed probe in order to perform quad gantry
leveling (QGL). Typically, the probe is also used as the Z endstop, and to
calculate a bed mesh if desired.

The default on StealthChanger is to use the OptoTap board on each tool as the
bed probe. This board is needed anyway to detect which tool is active, and to
detect toolchange failures.

With this probing method, the tool will move downward until the nozzle contacts
the bed. As the gantry continues to lower, the tool will slide upwards on the
shuttle until the OptoTap board no longer registers the presence of the
shuttle, at which point the probe is considered triggered. This is conceptually
the same as [Voron Tap](https://github.com/VoronDesign/Voron-Tap), with the
StealthChanger pins and bushings taking the place of the Tap linear rail.

FIXME: Something about nozzle temperatures and cleaning

X and Y probe offsets are zero, because the nozzle is the probe. The probe Z
offset will be equal to the distance the shuttle had to travel after the tool
made contact with the bed and before the OptoTap triggered. It is specified by
the `z_offset` parameter within `[tool_probe Tn]` (where Tn = T0, T1, …). It is
always a negative number, because the trigger point is “below” the bed. As with
any printer, this value must be tuned to get the right amount of first-layer
squish. Follow [Ellis's
method](https://ellis3dp.com/Print-Tuning-Guide/articles/first_layer_squish.html),
the [paper test](https://www.klipper3d.org/Bed_Level.html#the-paper-test) or
any other method you prefer; there is nothing really special about
StealthChanger here. A more negative probe Z offset means less squish; a less
negative (closer to zero) value means more squish, as the tool will not rise as
far from the trigger point.

Each tool will have its own probe Z offset, because of variation in the
assembly of the tool, the preload screws, and the OptoTap board itself. It is
typical to set up the print start macro such that T0 is always used for the
final QGL and Z homing before printing. Then it is only necessary to fine-tune
the probe Z offset on T0. Other tools need only be close enough for an initial
Z homing before picking up T0.

It is possible to use other bed probes like Cartographer or Beacon with
StealthChanger, but this is not really supported or documented yet. (FIXME: say
more here)

# G-code offsets

Besides the probe offsets, you will also need to calibrate the differences
between the nozzle positions on each tool, so that parts of a model printed
with different tools will line up correctly. This is necessary even with
“identical” tools because of the tolerances of the parts used and the assembly
procedure.

By convention, these G-code offsets are set to 0 for T0. The offsets for other
tools specify the distance that tool needs to move to place its nozzle in
exactly the same position that T0’s would be. This can be either positive or
negative on each axis. G-code offsets are typically stable from print to print,
but they may need adjustment if you rebuild a tool or have a particularly hard
crash.

G-code offsets are specified by `gcode_x_offset`, `gcode_y_offset`, and
`gcode_z_offset` within `[tool Tn]` (where Tn = T1, T2, …). These parameters
should be set to 0 for T0.

## Manual calibration

The simplest but most tedious method of calibrating G-code offsets is to print
a bunch of test objects like [this
one](https://www.printables.com/model/201707-x-y-and-z-calibration-tool-for-idex-dual-extruder).
For X and Y you are looking at the [vernier
scales](https://en.wikipedia.org/wiki/Vernier_scale); for Z you are looking to
have the same amount of squish on both sides (remember, T0 squish is set by the
probe Z offset, not G-code offset).

## Mechanical calibration probes

A mechanical calibration probe is basically an endstop that can be triggered by
the nozzle moving along any axis. By tapping the probe from ±X, ±Y and +Z
directions, the position of the nozzle opening can be determined (assuming a
clean nozzle that is bored concentric to its outer surfaces).

Several designs are available:

* [Sexball](https://github.com/DraftShift/StealthChanger/wiki/Bill-of-Materials#sexball-probe),
  which replaces the pin of hartk’s Sexbolt endstop with a ball
  (FIXME: elaborate instead of linking to old docs)

* [Nudge](https://github.com/zruncho3d/nudge)

* Multiple designs in the [NozzleAlign](https://github.com/viesturz/NozzleAlign) repo

LDO StealthChanger kits come with a Sexball probe and this is probably a good
place to start for new users.

You can permanently mount any of these probes in the overtravel region at the
front or rear of the bed. With Sexball it is easy to remove the ball and pin,
so that tools do not collide during printing. Alternately, you can make the
whole probe assembly removable, as long as you have some way to rigidly attach
it on or near the bed for calibration. (FIXME: some examples of this)

Any of these probes is basically the same from the firmware perspective and you
can consult the [NozzleAlign](https://github.com/viesturz/NozzleAlign) docs for
information on configuration and commands.

Due to thermal expansion, it is best to probe as close to printing conditions
as possible, though you must also ensure that the nozzle stays clean and does
not ooze. 150°C is a good default.

FIXME: automatic calibration on every print, is it possible?

## Optical calibration

Another approach for XY offsets is to use a camera looking up at the nozzle.
Some hardware options:

* [CXC by Ember Prototypes](https://www.emberprototypes.com/products/cxc)

* [DIY version](https://www.printables.com/model/1099576-xy-nozzle-alignment-camera)
  using OV9726 camera module

* Any USB microscope, if you can mount it rigidly

For software, you can use:

* [kTAMV](https://github.com/TypQxQ/kTAMV), which automatically locates the
  nozzle using machine vision

* [Axiscope](https://github.com/nic335/Axiscope), which provides a web
  interface for manually locating nozzles. This involves more manual effort
  than kTAMV, but is simpler and can be more reliable. Axiscope can also
  interact with a Sexbolt or other Z endstop to calculate Z offsets.

# Dock locations

FIXME: write about setting dock locations

In the meantime, see below.

# Other per-tool stuff

PID, E-steps, input shaper

FIXME: write about these

# Specific calibration routines

FIXME: This section is copied over from the old docs. It should be cleaned up and merged with the above.

## Z Offset

**NOTE:** Tn is the tool on the shuttle, ie T0

1. Put a tool on the shuttle and run `INITIALIZE_TOOLCHANGER`
2. Run `G28`
3. Run `QUAD_GANTRY_LEVEL`
4. Run `G28`
5. Do a [Manual Paper Test](https://www.klipper3d.org/Bed_Level.html#the-paper-test) as normal like a single toolhead head printer and adjust the Z
5. Copy the offset and save this to `z_offset` in `[tool_probe Tn]` of the tool conf file
6. Repeat from `step 1` for all tools (`step 2` and `step 3` are optional after first tool)
7. Run `FIRMWARE_RESTART`


## GCODE Z Offset

**NOTE:** Tn is the tool on the shuttle, ie T1

**NOTE:** only home or probe with T0 during this calibration

**NOTE:** `gcode_z_offset` on Tool 0 is always 0.

1. Set [z_offset](#z-offset) for all tools first
2. Make sure T0 is on the shuttle and run `INITIALIZE_TOOLCHANGER`
3. Run `G28`
4. `QUAD_GANTRY_LEVEL` 
5. Run `G28`
6. Run `G1 Z10 F600`
7. Manually remove current tool and place the next tool in its place on the shuttle
8. Do a [Manual Paper Test](https://www.klipper3d.org/Bed_Level.html#the-paper-test) as normal like a single toolhead head printer and adjust the Z
9. Once done run `M114` and copy the Z value to `gcode_z_offset` in `[tool Tn]` of the tool conf file
10. Repeat from `step 6` for all tools
11. Run `FIRMWARE_RESTART`


## Dock Parking

**NOTE:** Set the `params_close_y` to your highest `params_park_y` + 30, and set `params_safe_y` to `params_close_y` + the thickness of your thickest tool + 10 in the `toolchanger.cfg` and **remove them from the tool config files**

**NOTE:** For `params_safe_y` you could also just make sure when you have a tool on the shuttle you can move freely behind the dock and not hit any other docked tools and note that `y` position.

1. Put a tool on the shuttle and run `INITIALIZE_TOOLCHANGER`
2. Run `G28` and `QUAD_GANTRY_LEVEL` 
3. Remove the tool from the shuttle and place it in the dock
4. Move the gantry as if to pick up the tool, as soon as the light on the optotap pcb changes
5. Raise Z by 1
6. Run `M114` and record the values to `params_park_x`, `params_park_y` and `params_park_z` in `[Tool Tn]` of the tool conf file
7. Run `G28`
8. Run `SET_TOOL_PARAMETER PARAMETER='params_path_speed' VALUE=300`
9. Run `TEST_TOOL_DOCKING RESTORE_AXIS=XYZ`
10. Run `RESET_TOOL_PARAMETER PARAMETER='params_path_speed'`
11. Repeat this for all tools
12. Run `FIRMWARE_RESTART`

### Docking/Undocking

The Moving using config parameters is as such:

| Current tool | No tool | Next tool |
|--------------|---------|-----------|
|`safe_y`, `park_x` -> `park_z` -> `close_y` -> `path` | `close_y` -> `park_x` | `path` -> `safe_y` -> `t_command_restore_axis` |
