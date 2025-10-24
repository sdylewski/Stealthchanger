---
title: Probes
nav_order: 6
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
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
// todo:  add pros/cons for different methods

### Sexball
// TODO

### Nudge
// TODO
https://github.com/zruncho3d/nudge

### Axiscope
[Axiscope](https://github.com/nic335/Axiscope) uses a camera instead of a physical probe to align each toolhead nozzle. With its provided web interface it's really easy to go through the toolheads, align them and determine the offsets. It also supports a physical endstop to determine the gcode Z offsets (make sure your nozzle is clean).

Physical probes only works if the bore hole of your nozzle is exactly in the center, which is not always the case with very cheap nozzles. If it's not it will introduce a bias and thus the nozzles will remain misaligned. With a camera you remove the reliance of good tolerances out of the equation, you visually align the nozzle bore hole and those offsets will be perfect. It also has the added benefit that you inspect your nozzle closely so you don't forget to remove crud when determining the gcode Z-offsets.

While it requires more manual alignment than a physical probe, aligning 5 toolheads is still done in a couple of minutes.

### Using test print instead
// TODO
https://www.printables.com/model/201707-x-y-and-z-calibration-tool-for-idex-dual-extruder



(below from BOM page)

## Sexball probe

![Sexball probe](https://github.com/DraftShift/StealthChanger/blob/main/media/sexball-probe.jpg?raw=true)

Image By asoli

Calibration probe option that just replaces the shaft on a sexbolt.
- [Probe](https://s.click.aliexpress.com/e/_oB1egOH)
- [12mm Ball with M5 Threads](https://s.click.aliexpress.com/e/_o2DGfvf)
- [M5x30mm External Thread Pin](https://s.click.aliexpress.com/e/_omw2qxX)

**NOTE:** For micron M5x25mm Pin is tall enough

**NOTE:** Only use the hartk style bodys with the sleeves, knockoffs have too much slop.

![Sexball probe types](https://github.com/DraftShift/StealthChanger/blob/main/media/sexball-probe-types.jpg?raw=true)

Image by BT123


## Affiliate Links

| Parts   	  | Link 1     | Link 2    | Link 3    |
|-----------  |------------|-----------|-----------|
| Bushing 	  | [AliExpress](https://s.click.aliexpress.com/e/_Dmsh3LJ) | [US Amazon](https://amzn.to/3RAjKtY) | [UK Amazon](https://amzn.to/48jnoPO) | 
| Pin     	  | [AliExpress](https://s.click.aliexpress.com/e/_DCQkrFP) | [US Amazon](https://amzn.to/3GZBSZn) | [UK Amazon](https://amzn.to/488gP2v) |

Due to QC issues, this is an [Alternative bushing](https://s.click.aliexpress.com/e/_DFJQgtN) which has also been tested and works fine.

Alternatively you can purchase check on our official [vendors list](Building/Vendors-and-Kits.md)

