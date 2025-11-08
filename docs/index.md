---
title: StealthChanger Components
nav_order: 1
has_children: true
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# <img src="media/Logos/Stealthchanger_logo.png" style="height:50px;vertical-align:text-top" /> StealthChanger

<b>Tool changing system for Vorons and other front mount printer motion systems.</b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
 <a href="https://discord.gg/draftshift" target="_blank" alt="Join our Discord">![Discord](https://img.shields.io/discord/1226846451028725821?logo=discord&logoColor=%23ffffff&label=Join%20our%20Discord&labelColor=%237785cc&color=%23adf5ff)</a>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://github.com/sponsors/DraftShift" target="_blank" alt="Sponsor Us">![GitHub Sponsors](https://img.shields.io/github/sponsors/DraftShift?logo=githubsponsors&label=Sponsors&labelColor=rgb(246%2C%20248%2C%20250)&color=rgb(191%2C%2057%2C%20137))</a>

## Overview

StealthChanger converts a Voron 2.4 (and other front-mount motion systems) into a multi-tool printer. The shuttle exchanges toolheads that are mounted on backplates and docks at the front of the machine. Bushings, pins, and magnets create a rigid connection, while OctoTap sensing provides TAP-style Z probing.

StealthChanger builds on projects such as [tapchanger](https://github.com/viesturz/tapchanger) and the work of many community contributors. Join the community on [Discord](https://discord.gg/draftshift) to see what is new and share your build.

<img src="media/CableManagement/LDO_Stealthchanger_back_annotated.png" width="400"/>



This is a challenging conversion, even for experienced Voron builders. Expect reprints, tuning, and iteration. Start with these resources:



## Hardware

### Shuttle & Toolheads

<table>
<tr>
<td valign="top">
The shuttle replaces the stock Voron carriage with a bushing-and-pin interface that mates to each toolhead backplate. Backplates and docks exist for many toolheads (Anthead, Stealthburner, Dragonburner/Rapidburner, A4T, SV08, Yavoth, XOL, Mini Stealthburner, Blackbird, and more). 

See the [Toolheads overview](Toolheads/Toolheads.md) for comparisons and BOMs.
</td>
<td valign="top" width="320">
<img src="media/Shuttle/shuttle_manual_docking.gif" width="300" />
</td>
</tr>
</table>

### Docks & Mounting Hardware

<table>
<tr>
<td valign="top">
The modular dock holds tools when they are not in use. It can mount to a front crossbar, door buffer, or top frame. 

Learn about options and mounting strategies in [Docks, Crossbar, and Door Buffer](Docks.md).
</td>
<td valign="top" width="300">
<img src="media/Dock/dock_front.png" width="280" />
</td>
</tr>
</table>

### Electronics & Cable Management

<table>
<tr>
<td valign="top">
Multiple toolheads mean more wiring, CAN/USB connections, and filament paths. Key resources:

- [Electronics & Cable Management](CableManagement/CableManagement.md)
- [Backpack & Electrical Distribution](CableManagement/ElectricalDistribution.md)
- [Umbilicals](CableManagement/Umbilicals.md)
- [Power](CableManagement/Power.md)
- [Filament Management](CableManagement/FilamentManagement.md)
</td>
<td valign="top" width="220">
<img src="media/CableManagement/wire_management.jpg" width="200" />
</td>
</tr>
</table>

### Enclosure / Top Hat

<table>
<tr>
<td valign="top">
With docks mounted high and umbilicals arcing upward, most enclosed printers need a taller top enclosure. Options include printable top hats and 2020 extrusion frames. See [Top Hat](TopHat.md).
</td>
<td valign="top" width="220">
<a href="TopHat.md"><img src="media/TopHat/printed_tophat.png" width="200" /></a>
</td>
</tr>
</table>

### Probes & Endstops

<table>
<tr>
<td valign="top">
Physical probes (Sexball, Nudge, Axiscope, etc.) and relocated endstops simplify tool alignment and gantry homing. Hardware details are covered in [Probes](Probes.md) and [Endstops](Endstops.md).
</td>
<td valign="top" width="220">
<img src="media/Probes/sexball-probe.jpg" width="200" />
</td>
</tr>
</table>

## Building
1. **Plan the build** – [Checklist](Building/Checklist.md) and [Bill of Materials](Building/Bill-of-Materials.md)
2. **Order parts** – [Vendors and Kits](Building/Vendors-and-Kits.md)
3. **Print components** – [Printing guide](Building/Printing.md)
4. **Estimate cost** – [Approximate cost calculator](https://docs.google.com/spreadsheets/d/1cjlZ4xi84sUbo09nV3CDkOrLjz3leInTZ9sxwSzPscE)
5. **Visualize the assembly** – [Reference CAD (.step) by N3MI](https://github.com/N3MI-DG/sc-guides)
## Software & Configuration

<img src="media/Logos/klipper_toolchanger_logo.png" width="160" align="right" />

Klipper must be toolchanger-aware for StealthChanger. The typical flow looks like this:


1. [Installation](SoftwareAndConfig/Installation.md) – install klipper-toolchanger-easy to add StealthChanger macros and configs
2. [Tool Configuration](SoftwareAndConfig/ToolConfiguration.md) – set up tool files and toolchanger settings for your hardware
3. [Toolhead Calibration](SoftwareAndConfig/Calibration.md) – set probe offsets and tool alignment
4. [Dock Calibration](SoftwareAndConfig/DockCalibration.md) – set dock positions for reliable tool changes
5. [Slicers & Printing](SoftwareAndConfig/Slicers.md) – configure slicer and macros for multi-tool printing
6. [LEDs](SoftwareAndConfig/LEDs.md) – optional post-install lighting effects and status indicators



## Support & Resources




<a href="https://discord.gg/draftshift" target="_blank" alt="Join our Discord">![Discord](https://img.shields.io/discord/1226846451028725821?logo=discord&logoColor=%23ffffff&label=Join%20our%20Discord&labelColor=%237785cc&color=%23adf5ff)</a>&nbsp;&nbsp; <a href="https://github.com/sponsors/DraftShift" target="_blank" alt="Sponsor Us">![GitHub Sponsors](https://img.shields.io/github/sponsors/DraftShift?logo=githubsponsors&label=Sponsors&labelColor=rgb(246%2C%20248%2C%20250)&color=rgb(191%2C%2057%2C%20137))</a>

- [Support](Support/Support.md)
- [Contributing & Donating](Support/Contributing-and-Donating.md)
- [Serials](Support/Serials.md)
- [Team & Credits](Support/Team-and-Credits.md)




