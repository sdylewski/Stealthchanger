---
title: Stealthburner
nav_order: 3
parent: Toolheads
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
# Stealthburner

<img src="../media/Toolheads/Stealthburner.png" width=200>

## References
* [Stealthburner reference page](https://github.com/VoronDesign/Voron-Stealthburner)

## Backplate
**Note:** heatsets on the SB version in from the opposite side as the Voron instructions, slightly longer screws on the CW2 attachment may be required

* [Stealthburner Backplate](https://github.com/sdylewski/StealthChanger/blob/main/STLs/Backplates/StealthBurner.stl)
* OR - [Stealthburner magnetic backplate](https://www.printables.com/model/1346474-stealthchanger-stealthburner-backplate-v11-magnet/files)
* OR - [Stealthburner screw-in pins backplate](https://www.printables.com/model/1358108-stealtchanger-stealthburner-backplate-with-screwed)
* OR - [Stealthburner screw-in pins and magnetic backplate](https://www.printables.com/model/1384948-stealthchanger-stealthburner-backplate-v11-magnet)
* [Backplate assembly instructions](https://github.com/sdylewski/StealthChanger/blob/main/Manual/Stealthchanger_Assembly_Guide.pdf)
* Requires supports. [Printing instructions](../Building/Printing.md)

Having magnets that keep the toolhead in place in the docks and nicely aligned with the shuttle is recommended for smooth dropoff/pickup.

### Backplate BOM for All Tools

- [4] m3 heat inserts
- [3] Ø4x12mm ssRod (dowel pin) with a rounded end **(if it has female threads on the back it will be listed as an M3, but make sure the pin is 4mm OD, that is what is important. We recommend the threaded pins for better fixing)**
- [1] 6x3mm magnet (N52 Highly recommended to counter the pull from the umbilicals. Note that most magnets not from a reputable source may say N52 but aren't actually. Recommend one of the two links below.)
- [2] m3x6 or m3x8 FHCS (Flat head countersunk screw, MUST BE MAGNETIC. no stainless, as per TAP)
- [1] [OptoTap](https://s.click.aliexpress.com/e/_DEGsGTV) (only the sensor PCB is required)
- [1] m3x8 BHCS (optional in v1.1)


### BOM Additions for Stealthburner
- [Recommended for DraftShift Dock] Several 5x2 or 5x3 N52 magnets to hold toolhead to dock

## Toolhead Options & Mods
* [Stealthburner numbered cowls](https://github.com/sdylewski/StealthChanger/tree/main/UserMods/Dumplap/Stealthburner%20Number%20Cowls)
* [SC Barf LED for Stealthburner](https://github.com/sdylewski/StealthChanger/tree/main/UserMods/N3MI-DG/StealthBurner_SC_Barf)
* [FilaMAtrix](https://github.com/thunderkeys/FilamATrix) for runout sensor, cutter and ECAS fitting

## StealthChanger Requirements
* Requires Shorter Z joints like <a href="https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/hartk1213/Voron2.4_GE5C">Ge5C z-joints</a> so you don't bottom out your carriage when homing.
* Requires new smaller front idlers like the <a href="https://github.com/clee/VoronBFI">BFI</a> or <a href="https://github.com/DraftShift/StealthChanger/tree/main/UserMods/BT123/MiniBFI%20%2B%20MicroBFI">Mini BFI</a> so it doesn't collide with the idlers.

## Dock
* Dock width: 76mm
* Common components for [your dock type](.../Dock.md)
* [Modular dock assembly guide](https://github.com/DraftShift/ModularDock/blob/main/Manual/ModularDock_Assembly_Guide.pdf)
* Stealthburner is not compatible with stubby docks.

### Dock options
* Original Draftshift Design [Stealthburner Back and Base](https://github.com/DraftShift/ModularDock/tree/main/STLs/Stealthburner)
* [Stealthburner magnetic dock](https://www.printables.com/model/1346474-stealthchanger-stealthburner-backplate-v11-magnet/files)
* [Happy Crab docks](https://www.printables.com/model/994635-stealthchanger-stealthburner-minimal-docks-aka-hap) (no verticals, crossbar attachment only)
* [One piece docks](https://www.printables.com/model/1063297-one-piece-docks-remix-of-crabby-docks-with-uhf-var) (include UHF variant)
* [Screw docks](https://www.printables.com/model/911717-stealthchanger-screw-docks) (for hooking on toolheads)


## Tips & Suggestions
* TBD



