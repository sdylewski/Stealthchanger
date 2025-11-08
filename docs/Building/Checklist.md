---
title: Checklist
nav_order: 1
parent: Building
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Checklist

## Planning & Preparation

 - [ ] Read and understand all the documentation
 - [ ] Decide on the tools to use - See [Docks](../Docks.md) for a calculation of how many will fit
 - [ ] Decide on dock types - [Modular Dock](../Docks.md) or other
 - [ ] Decide if you are going top mount, or use a cross bar, 2040 or [Door Buffer](../Docks.md) or [MiniBFI](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/BT123/MiniBFI%20%2B%20MicroBFI)
 - [ ] Decide on a [Tophat](../TopHat.md)
 - [ ] Decide on [umbilical management](../CableManagement/CableManagement.md)
 - [ ] Visit the [BOM](Bill-of-Materials.md) to make sure you have ordered everything you need for the conversion

## Printing Parts

 - [ ] Visit our [Printing](Printing.md) guide and start printing
 - [ ] At this point please inspect your prints, take extra note that your hexes are very uniform. If they are misshapen, chances are you need to reprint as you will have alignment issues. It doesn't take much to be out by a lot. Try printing at a slower speed if you have issues.

## Building

 - [ ] [Assemble](../Shuttle.md) the shuttle and backplates
 - [ ] Build your toolheads and backplates - See [Toolheads](../Toolheads/Toolheads.md) for supported toolheads
 - [ ] Update endstops if needed - See [Endstops](../Endstops.md) for homing configuration
 - [ ] Install probes - See [Probes](../Probes.md) for probe setup (OctoTap is required for each toolhead)

## Software & Configuration

 - [ ] [Install](../SoftwareAndConfig/Installation.md) klipper-toolchanger-easy
 - [ ] [Configure](../SoftwareAndConfig/Configuration.md) tool files and toolchanger settings

## Calibration

 - [ ] [Calibrate Probe Z Offsets](../SoftwareAndConfig/ToolCalibration.md#probe-z-offset-tool_probe-offsets) for each tool
 - [ ] [Calibrate G-code Offsets](../SoftwareAndConfig/ToolCalibration.md#g-code-offsets-t0---tn-offsets) (X, Y, Z) between tools
 - [ ] [Calibrate Dock Positions](../SoftwareAndConfig/DockCalibration.md) - Use [Dock Tuner](../SoftwareAndConfig/DockTuner.md) (recommended) or manual method

## Slicer Setup

 - [ ] [Configure your slicer](../SoftwareAndConfig/Slicers.md) for multi-tool printing
 - [ ] Set up print start macros and tool change G-code

## Optional

 - [ ] [Configure LEDs](../SoftwareAndConfig/LEDs.md) for status indicators and lighting effects

## Final Steps

 - [ ] Register for a [serial](../Support/Serials.md)
 - [ ] Visit our [sponsor](https://github.com/sponsors/DraftShift) page
