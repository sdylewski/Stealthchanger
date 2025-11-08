---
title: Probes
nav_order: 6
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
# Probes

StealthChanger uses two types of probes:
1. **Z-probes** - For Z homing and [bed leveling](../SoftwareAndConfig/Calibration.md#bed-probing) (determines Z=0 and `z-offset`)
2. **Inter-tool offset probes** - For calibrating X,Y,Z offsets between tools (`gcode_offset` in `[tool]` section). See [calibration guide](../SoftwareAndConfig/Calibration.md) for setup.

**Note:** Keep nozzles clean for accurate measurements. XY probes must be mounted on bed extrusions or securely attached to the bed during calibration.

## 1. Z-probes

### TAP
Uses the [OctoTap PCB](../Shuttle.md#do-i-need-an-octotap-board-per-toolhead) (required for [tool detection](../Shuttle.md)) for Z homing via nozzle contact, similar to Voron TAP. **Note:** You need an OctoTap PCB per [toolhead](../Toolheads/Toolheads.md) even if using a different Z-probe.

**Important:** Z-offset will be negative since the trigger occurs after nozzle contact. Install a wiper and use a `CLEAN_NOZZLE` macro after initial home and before [QGL](../SoftwareAndConfig/Calibration.md#bed-probing)—any leftover filament affects accuracy.

**Pros:**
- Free (OctoTap already required)
- Accurate with clean nozzle

**Cons:**
- Requires tool on [shuttle](../Shuttle.md) (no toolless homing)
- Slow for [QGL](../SoftwareAndConfig/Calibration.md#bed-probing) and large bed meshes
- May dimple PEI plates (especially smooth ones with N52 magnets)
   
### Beacon/Carto
Magnetic field sensor that detects the build plate without contact, even while moving.

**Pros:**
- Toolless homing
- Much faster than TAP

**Cons:**
- Requires one per tool or [shuttle](../Shuttle.md) mount (Klipper doesn't tolerate sensor appearing/disappearing at runtime)
- Extra [umbilical](../CableManagement/Umbilicals.md) to shuttle
- Some variants unstable at elevated temperatures

#### Mounts
* [Carto mounts for CNC shuttles](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/Carto_Mounts)
* [Beacon/Carto Mount for Fystec/LDO CNC Shuttle with Top Brace](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/cekim-git/CNCShuttleMount/)
* [Fysect Shuttle Cartograper Mount](https://www.printables.com/model/1455180-fysect-shuttle-cartograper-mount/files)

## 2. Inter-tool offset calibration probes

**Note:** Hardware isn't required—you can calibrate X, Y, and Z by printing reference plates. However, a dedicated probe yields better results faster. See [printable calibration](#using-a-printable-calibration) below.

### Sexball
A [sexbolt](https://mods.vorondesign.com/details/t1DBVlcUBbdEK6habEsVzg) mod with a ball top that self-centers by [probing](https://www.youtube.com/watch?v=gKaL7Oxud2c) each side. Determines X,Y,Z offsets relative to T0, saved as `gcode_offset` in `[tool]` sections.

<img src="media/Probes/sexball-probe.jpg" width="200">
*Image by asoli*

**Pros:**
- Easy setup (may need to move bed for tool access)
- Calibrates X, Y, and Z offsets with scripts

**Cons:**
- Requires 6mm travel past center on all four sides (limits mounting locations)
- Needs tight tolerances: no play in sexball, concentric nozzles required (cheap nozzles often aren't)
- Sideways force on sphere can cause issues

See [tool calibration configuration](../SoftwareAndConfig/Calibration.md) to set up calibration config and macros.

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

### [Axiscope](https://github.com/nic335/Axiscope)
Camera-based alignment system with web interface for visual nozzle alignment. Supports physical [endstop](../Endstops.md) for Z offset calibration.

<table>
<tr>
 <td><img src="media/Probes/axiscope_camera.jpg" width="200"></td>
 <td><img src="media/Probes/axiscope_aligment.gif" width="600"></td>
</tr>
 <tr><td colspan="2">*Images from [printables](https://www.printables.com/model/1099576-xy-nozzle-alignment-camera)*</td></tr>
</table>

**Pros:**
- Visual approach eliminates tolerance issues and nozzle inaccuracies
- Close-up inspection reveals issues (e.g., stuck filament affecting Z)

**Cons:**
- Manual alignment required (~2 minutes per [tool](../Toolheads/Toolheads.md))
- Z offset requires [endstop](../Endstops.md); set X,Y offsets before calibrating Z

**Tip:** Camera USB cable is short—consider a [USB keystone insert](https://www.printables.com/model/609433-voron-skirt-keystone-for-usbethernet) at the front.

**BOM:**
- OV9726 camera module
- 5V 3mm round white LEDs (6000-6500k) x 4
- [3D printed camera module holder](https://www.printables.com/model/1099576-xy-nozzle-alignment-camera)
   
### [Nudge](https://github.com/zruncho3d/nudge)
<img src="media/Probes/Nudge.jpg" width="200"> *Image from Nudge site*

Buildable probe: vertical pole held against bolts by spring tension, completing a circuit. Pushing the top breaks the circuit at the bottom, registering contact.

**Pros:**
- Mostly 3D printed with common parts
- Less horizontal-to-vertical motion translation than Sexball

**Cons:**
- Requires tuning to avoid jamming (driving pole too far in Z)
- Use copper SHCS screws (SS screws don't work reliably)

See [calibration section](../SoftwareAndConfig/Calibration.md) for usage.


#### Mods

* [Stronger Dockable bed-top mount](https://www.printables.com/model/1453289-stealthchanger-dockable-nudge-or-sexbolt-mount)
* [2.4 Dockable Nudge Mount](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/MRSalguod/2.4%20Dockable%20Nudge%20Mount)


### Using a printable calibration
No hardware required—print reference plates for calibration (more work, but free).

**⚠️ Warning:** If gcode_z_offsets are unknown, set them high before printing to prevent lower nozzles from digging into the bed. See [calibration guide](../SoftwareAndConfig/Calibration.md) for proper setup.

<img src="media/Probes/xy_print_cal.jpg" width="300">

**Method:** [X, Y and Z calibration tool for IDEX](https://www.printables.com/model/201707-x-y-and-z-calibration-tool-for-idex-dual-extruder)

**Pros:**
- Visual approach (what you see is what you get)

**Cons:**
- Very time-consuming (especially for 5-6 [tools](../Toolheads/Toolheads.md))
- Bad Z offset can damage PEI plate
   
## FAQ

### My sexball probe doesn't work, it's always triggered
With [sensorless homing](../Endstops.md#sensorless-homing), ensure [endstops](../Endstops.md)/micro switches use ports that don't share pins with motor diag pins (e.g., use Z motor ports). Check your mainboard manual for pin assignments.

### My OctoTAP board doesn't trigger reliably
See [Shuttle FAQ](../Shuttle.md#do-i-need-an-octotap-board-per-toolhead) for details. Common fixes:
1. Mount PCB as low as possible—push down before tightening screws (screw holes have play)
2. Ensure optical sensor is straight and perpendicular to the board

### Do I need to cut the trace on the OctoTAP board?
Generally no. If supplying 5V from the [toolhead](../Toolheads/Toolheads.md) board, it works fine. Cutting the trace disables the 24V→5V regulator (makes board 5V-only) and is only needed if the regulator interferes.

### Can I use `SAVE_CONFIG` after `PROBE_CALIBRATE`?
No. `SAVE_CONFIG` saves z-offset at the bottom of printer.cfg, not in the tool's probe section. Z-offset is fetched from the active tool and applied in homing_override. See [calibration configuration](../SoftwareAndConfig/Calibration.md) for proper setup.

### My Nudge reports "endstop triggered before contact"
Bad electrical connections. Use copper SHCS screws and check resistance between output pins.

### Do I need to calibrate offsets on every print?
No. Offsets remain stable unless hardware changes ([toolhead](../Toolheads/Toolheads.md) disassembly, [backplate preload screws](../Shuttle.md#backplate-preload), nozzle swap, etc.). Check periodically for drift, especially before long multicolor prints.

### What is toolless homing?
Homing with just the [shuttle](../Shuttle.md) (no tool required). Benefits:
- Park last tool in [dock](../Docks.md) (prevents ooze, keeps [umbilicals](../CableManagement/Umbilicals.md) in arc shape)
- Move empty shuttle behind bed (gantry out of the way, ready for next print)

