---
title: Probes
nav_order: 1
parent: Home
---
# Probes

## What

There are 2 types of probes used in StealthChanger. One is the familiar Z-probe to do Z homing and find the bed position at Z=0 (along with `z-offset`, the distance from the bed to the trigger point of the probe). The other is used for inter-tool offsets (`gcode_offset` in `[tool]` section), as each nozzle will be ever so slightly different in terms of X,Y,Z position, the offsets relative to the first tool (T0) have to be taken into account so the printer prints in the expected location after a tool swap.

## 1. Z-probes

### TAP
Each toolhead of Stealthchanger has a OctoTap PCB boards, this can be used for homing with the nozzle just like Voron TAP. Even if you use a different z-probe, you still need an OctoTap PCB per toolhead as it is also used to detect which tool is active on the shuttle and whether the pickup of a new tool has succeeded.
Note that the z-offset will be negative for TAP as the motors will continue to go below the zero (= bed level) point to trigger the OctoTap sensor by pushing the toolhead up out of the shuttle until it triggers the OctoTap.

### Beacon/Carto
The beacon/carto is mounted on the shuttle, so the shuttle will require an extra umbilical
// TODO

### Eddy
// TODO (requires modification to Klipper code iirc)


## 2. Calibration probes

### Sexball
// TODO

### Nudge
// TODO
https://github.com/zruncho3d/nudge

### Axiscope
// TODO
https://github.com/nic335/Axiscope
