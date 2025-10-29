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


## Stealthchanger Overview
StealthChanger is a project to convert a Voron 2.4 printer into one with multiple toolheads.

Mounting of the toolhead to the shuttle is done by using bushings and pins, with magnets to help create a strong mounting connection for high-speed printing, and uses the same principles as [TAP](https://github.com/VoronDesign/Voron-Tap) to measure Z offsets.

StealthChanger draws from many different projects including [tapchanger](https://github.com/viesturz/tapchanger), and involves the contributions of many people who work together to make it better. 

# Stealthchanger Components
The stealthchanger system consists of multiple parts. Some are essential, some have many different options, and some are optional. 

<img src="media/CableManagement/LDO_Stealthchanger_back_annotated.png" width="400"/>

## [Shuttle](Shuttle.md) & [Toolhead Backplate](Toolheads/Toolheads.md)
<img src="media/Shuttle/shuttle_manual_docking.gif" width="350" align="right" > The shuttle replaces your Voron shuttle with one that has bushings to connect to the backplate of each toolhead. Backplates and docks are available for the following toolheads: 

* [Anthead](Toolheads/Anthead.md)
* [Stealthburner](Toolheads/Stealthburner.md)
* [Dragonburner/Rapidburner](Toolheads/Dragonburner.md)
* [A4T](Toolheads/A4T.md)
* [SV08](Toolheads/SV08.md)
* [Yavoth](Toolheads/Yavoth.md)
* [XOL](Toolheads/XOL.md)
* [Mini Stealthburner](Toolheads/MiniSB.md)
* [Blackbird](Toolheads/Blackbird.md)

See the <a href="Toolheads/Toolheads.md">Toolheads</a> page for a comparison of each toolhead.

## [Dock, Crossbar, and Door Buffer](Docks.md)
<img src="media/Dock/dock_front.png" width="400" align="right" /> 
The modular dock mounts to the top front of your printer to hold/dock the toolheads when not in use. May also contain a crossbar at the bottom of the dock. Some docks just use the crossbar.

* [Modular Dock](Docks.md)
* [Crossbar (optional)](Docks.md)
* [Door buffer (optional)](Docks.md) Needed if mounting crossbar to front of frame.


## [Electronics & Cable Management](CableManagement/CableManagement.md)
<img src="media/CableManagement/wire_management.jpg" width="180" align="right" /> 
Lots of toolheads mean lots of extra wires and filament that needs to be managed properly. With the umbilicals going to the exhaust port there are several options to connect them and to clean up the bundle with a "backpack" mounted on the back of the printer.<br>Power and data needs to be distributed from your main board to each toolhead, along with your filament.

* [Backpack & Electrical Distribution](CableManagement/ElectricalDistribution.md)
* [Umbilicals](CableManagement/Umbilicals.md) and exhaust plates
* [Power Supply](CableManagement/Power.md)
* [Filament management](CableManagement/FilamentManagement.md)


## [Top Hat](TopHat.md)
[<img src="media/TopHat/printed_tophat.png" width="200" align="right"/>](TopHat.md) 

With the dock at the top of the printer and umbilicals extending upward, enclosed printers will want to extend the top of the printer using a top hat. <br>

There is a printable top hat or you can use 2020 railing with clear panels.

## [Probes](Probes.md)
<img src="media/Probes/sexball-probe.jpg" width="180" align="right"/> 

Physical probes are used to measure the X and Y offsets of your tools relative to Tool 0. Endstop switches are included here also.

* [Probes](Probes.md) for determing offsets
* [Endstops](Endstops.md) for X and Y gantry endstops

## [Klipper Toolchanger](SoftwareAndConfig/Software.md)
<img src="media/Logos/klipper_toolchanger_logo.png" width="180" align="right"/> 

Klipper needs to be toolchanger aware with added code.

* [Klipper Toolchanger Installation](SoftwareAndConfig/Installation.md)
* [Configuration](SoftwareAndConfig/Configuration.md)
* [Calibration](SoftwareAndConfig/Calibration.md)
* [Slicers](SoftwareAndConfig/Slicers.md)


# Building
This is a challenging build/conversion, even for existing experienced Voron owners. Expect it to take a while, to re-print things frequently, and have to order random parts that you forgot the first time. 

### [Checklist](Building/Checklist.md)
### [Vendors and Kits](Building/Vendors-and-Kits.md)
### [Bill of Materials](Building/Bill-of-Materials.md)
### [Printing](Building/Printing.md)
### [Cost calculator](https://docs.google.com/spreadsheets/d/1cjlZ4xi84sUbo09nV3CDkOrLjz3leInTZ9sxwSzPscE)

MikeyMike created an [approximate cost calculator](https://docs.google.com/spreadsheets/d/1cjlZ4xi84sUbo09nV3CDkOrLjz3leInTZ9sxwSzPscE) for building a StealthChanger with x number of toolheads. It assumes you have a working Voron 2.4 and this does not include top hat extrusions,panels.

### [Reference CAD (.step) by N3MI](https://github.com/N3MI-DG/sc-guides)
N3MI created a [reference CAD file](https://github.com/N3MI-DG/sc-guides) of a StealthChanger with Anthead toolheads, docks with crossbar, top hat, umbilicals and fanny pack.

#[Support](Support/Support.md)

### [Contributing & Donating](Support/Contributing-and-Donating.md)
### [Serials](Support/Serials.md)
### [Team & Credits](Support/Team-and-Credits.md)
### TBD: How to convince your partner to go along with this project.


