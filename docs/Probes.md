---
title: Probes
nav_order: 6
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
# Probes

StealthChanger requires two types of probes for different purposes:

| Probe Type | Purpose | When Used |
|------------|---------|-----------|
| **Z-Probe** | Z homing and bed leveling | Every print (determines Z=0) |
| **Tool Offset Probe** | Calibrate X, Y, Z offsets between tools | Initial setup and after hardware changes |

**Quick Summary:**
- **Z-Probe**: Required for every toolhead. Uses OctoTap (TAP) or Beacon/Carto for contactless homing.
- **Tool Offset Probe**: Optional but recommended. Calibrates nozzle positions so all tools print in the same location. Can use Sexball, Nudge, Axiscope, or printable calibration method.

See the [Toolhead Calibration](SoftwareAndConfig/ToolCalibration.md) guide for detailed setup procedures.

## Z-Probes

Z-probes determine the Z=0 position for each toolhead. You need one per toolhead.

### TAP (Recommended for most users)
Uses the [OctoTap PCB](../Shuttle.md#do-i-need-an-octotap-board-per-toolhead) (already required for tool detection) for Z homing via nozzle contact.

**Setup:**
- OctoTap PCB is required per toolhead regardless of Z-probe choice
- Z-offset will be negative (trigger occurs after nozzle contact)
- Install a wiper and use `CLEAN_NOZZLE` macro after homing—filament residue affects accuracy

| Pros | Cons |
|------|------|
| No additional hardware (OctoTap already needed) | Requires tool on shuttle (no toolless homing) |
| Accurate with clean nozzle | Slower for QGL and large bed meshes |
| | May dimple PEI plates (especially smooth ones with N52 magnets) |
   
### Beacon/Carto (For toolless homing)
Magnetic field sensor that detects the build plate without contact, even while moving.

**Setup:**
- Requires one per tool or shuttle mount (Klipper doesn't tolerate sensor appearing/disappearing)
- Extra umbilical cable to shuttle
- Some variants may be unstable at elevated temperatures

| Pros | Cons |
|------|------|
| Toolless homing (no tool required) | Additional cost and wiring |
| Much faster than TAP | Requires shuttle-mounted option for toolless operation |

**Mounts:**
- [Carto mounts for CNC shuttles](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/Carto_Mounts)
- [Beacon/Carto Mount for Fystec/LDO CNC Shuttle with Top Brace](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/cekim-git/CNCShuttleMount/)
- [Fysect Shuttle Cartograper Mount](https://www.printables.com/model/1455180-fysect-shuttle-cartograper-mount/files)

## Tool Offset Probes

Tool offset probes calibrate X, Y, and Z offsets between tools so all nozzles print in the same location. **Optional but highly recommended**—hardware probes are faster and more accurate than printable calibration methods.

### Sexball (Most Popular)
A [sexbolt](https://mods.vorondesign.com/details/t1DBVlcUBbdEK6habEsVzg) mod with a ball top that self-centers by [probing](https://www.youtube.com/watch?v=gKaL7Oxud2c) each side. Automatically determines X, Y, and Z offsets.

<img src="media/Probes/sexball-probe.jpg" width="200">
*Image by asoli*

| Pros | Cons |
|------|------|
| Automated calibration with scripts | Requires 6mm clearance on all four sides (limits mounting locations) |
| Calibrates X, Y, and Z in one process | Needs tight tolerances: no play in sexball, concentric nozzles required |
| Easy setup | Sideways force on sphere can cause issues |

**Setup:** See [Toolhead Calibration](../SoftwareAndConfig/ToolCalibration.md) for configuration.

#### BOM
Replaces the shaft on a sexbolt:
- [Probe](https://s.click.aliexpress.com/e/_oB1egOH)
- [12mm Ball with M5 Threads](https://s.click.aliexpress.com/e/_o2DGfvf)
- [M5x30mm External Thread Pin](https://s.click.aliexpress.com/e/_omw2qxX) (M5x25mm for Micron)

**Important:** Only use Hartk-style bodies with sleeves—knockoffs have too much slop.

<img src="media/Probes/sexball-probe-types.jpg" width="300"> *Image by BT123*

**Parts:**
- **Bushing:** [AliExpress](https://s.click.aliexpress.com/e/_Dmsh3LJ) | [US Amazon](https://amzn.to/3RAjKtY) | [UK Amazon](https://amzn.to/48jnoPO) | [Alternative](https://s.click.aliexpress.com/e/_DFJQgtN)
- **Pin:** [AliExpress](https://s.click.aliexpress.com/e/_DCQkrFP) | [US Amazon](https://amzn.to/3GZBSZn) | [UK Amazon](https://amzn.to/488gP2v)

Also available from [official vendors](Building/Vendors-and-Kits.md).

#### Mods

* [Sexball top mount](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/Dumplap/SexBolt%202020%20Top%20Mount)
* [Sexball rest mount](https://www.printables.com/model/1094209-sexball-probe-rest-mount-for-stealthchanger-calibr)
* [Alternative with 4mm dowels instead of ball](https://www.printables.com/model/1073728-shorter-multi-tool-calibration-probe-with-4mm-dowe) ([discord link](https://discord.com/channels/1226846451028725821/1306506750509449258))
* [Dockable bed-top mount](https://www.printables.com/model/1453289-stealthchanger-dockable-nudge-or-sexbolt-mount)

### [Axiscope](https://github.com/nic335/Axiscope) (Visual Alignment)
Camera-based system with web interface for visual nozzle alignment. Manual but eliminates tolerance issues.

<table>
<tr>
 <td><img src="media/Probes/axiscope_camera.jpg" width="200"></td>
 <td><img src="media/Probes/axiscope_aligment.gif" width="600"></td>
</tr>
 <tr><td colspan="2">*Images from [printables](https://www.printables.com/model/1099576-xy-nozzle-alignment-camera)*</td></tr>
</table>

| Pros | Cons |
|------|------|
| Visual approach eliminates tolerance issues | Manual alignment (~2 minutes per tool) |
| Reveals nozzle problems (stuck filament, etc.) | Z offset requires separate endstop |

**BOM:**
- OV9726 camera module
- 5V 3mm round white LEDs (6000-6500k) x 4
- [3D printed camera module holder](https://www.printables.com/model/1099576-xy-nozzle-alignment-camera)

**Tip:** Camera USB cable is short—consider a [USB keystone insert](https://www.printables.com/model/609433-voron-skirt-keystone-for-usbethernet) at the front.
   
### [Nudge](https://github.com/zruncho3d/nudge) (DIY Build)
3D-printable probe using a vertical pole and spring tension to complete a circuit.

<img src="media/Probes/Nudge.jpg" width="200"> *Image from Nudge site*

| Pros | Cons |
|------|------|
| Mostly 3D printed with common parts | Requires careful tuning to avoid jamming |
| Less horizontal-to-vertical motion translation than Sexball | Must use copper SHCS screws (stainless steel doesn't work reliably) |

**Setup:** See [Toolhead Calibration](../SoftwareAndConfig/ToolCalibration.md) for usage.


#### Mods

* [Stronger Dockable bed-top mount](https://www.printables.com/model/1453289-stealthchanger-dockable-nudge-or-sexbolt-mount)
* [2.4 Dockable Nudge Mount](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/MRSalguod/2.4%20Dockable%20Nudge%20Mount)


### Printable Calibration (No Hardware)
Print reference plates and visually measure offsets. Free but time-consuming.

<img src="media/Probes/xy_print_cal.jpg" width="300">

**⚠️ Warning:** If `gcode_z_offsets` are unknown, set them high before printing to prevent lower nozzles from digging into the bed.

**Method:** [X, Y and Z calibration tool for IDEX](https://www.printables.com/model/201707-x-y-and-z-calibration-tool-for-idex-dual-extruder)

| Pros | Cons |
|------|------|
| No hardware required | Very time-consuming (especially for 5-6 tools) |
| Visual confirmation | Risk of damaging PEI plate if Z offset is wrong |
   
## FAQ

**Quick Links:**
- [My sexball probe doesn't work](#my-sexball-probe-doesnt-work-its-always-triggered)
- [My OctoTAP board doesn't trigger reliably](#my-octotap-board-doesnt-trigger-reliably)
- [Do I need to cut the trace on the OctoTAP board?](#do-i-need-to-cut-the-trace-on-the-octotap-board)
- [Can I use `SAVE_CONFIG` after `PROBE_CALIBRATE`?](#can-i-use-save_config-after-probe_calibrate)
- [My Nudge reports "endstop triggered before contact"](#my-nudge-reports-endstop-triggered-before-contact)
- [Do I need to calibrate offsets on every print?](#do-i-need-to-calibrate-offsets-on-every-print)
- [What is toolless homing?](#what-is-toolless-homing)

---

### My sexball probe doesn't work, it's always triggered
With [sensorless homing](../Endstops.md#sensorless-homing), ensure [endstops](../Endstops.md)/micro switches use ports that don't share pins with motor diag pins (e.g., use Z motor ports). Check your mainboard manual for pin assignments.

### My OctoTAP board doesn't trigger reliably
See [Shuttle FAQ](../Shuttle.md#do-i-need-an-octotap-board-per-toolhead) for details. Common fixes:
1. Mount PCB as low as possible—push down before tightening screws (screw holes have play)
2. Ensure optical sensor is straight and perpendicular to the board

### Do I need to cut the trace on the OctoTAP board?
Generally no. If supplying 5V from the [toolhead](../Toolheads/Toolheads.md) board, it works fine. Cutting the trace disables the 24V→5V regulator (makes board 5V-only) and is only needed if the regulator interferes.

### Can I use `SAVE_CONFIG` after `PROBE_CALIBRATE`?
No. `SAVE_CONFIG` saves z-offset at the bottom of printer.cfg, not in the tool's probe section. Z-offset is fetched from the active tool and applied in homing_override. See [calibration configuration](../SoftwareAndConfig/ToolCalibration.md) for proper setup.

### My Nudge reports "endstop triggered before contact"
Bad electrical connections. Use copper SHCS screws and check resistance between output pins.

### Do I need to calibrate offsets on every print?
No. Offsets remain stable unless hardware changes ([toolhead](../Toolheads/Toolheads.md) disassembly, [backplate preload screws](../Shuttle.md#backplate-preload), nozzle swap, etc.). Check periodically for drift, especially before long multicolor prints.

### What is toolless homing?
Homing with just the [shuttle](../Shuttle.md) (no tool required). Benefits:
- Park last tool in [dock](../Docks.md) (prevents ooze, keeps [umbilicals](../CableManagement/Umbilicals.md) in arc shape)
- Move empty shuttle behind bed (gantry out of the way, ready for next print)

