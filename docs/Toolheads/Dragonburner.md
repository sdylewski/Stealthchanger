---
title: Dragonburner
nav_order: 2
parent: Toolheads
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Dragonburner

<img src="../media/Toolheads/Dragonburner.png" width=200>

## References
* [Dragonburner Reference Page](https://github.com/chirpy2605/voron)

## Backplate
* [recommended] [theSin Dragonburner backplate]() for ebb36-style boards with Orbiter 2.5 or HGX Sherpa.
* Draftshift Design [Dragonburner Backplate](https://github.com/DraftShift/StealthChanger/blob/main/STLs/Backplates/DragonBurner.stl) (no connection to toolhead board)
* [Dragonburner spacer](https://github.com/DraftShift/StealthChanger/blob/main/STLs/Backplates/DragonBurner_Spacer.stl) (Required. goes between backplate and toolhead).
* [Backplate assembly instructions](https://github.com/DraftShift/StealthChanger/blob/main/Manual/Stealthchanger_Assembly_Guide.pdf)
* Requires supports. [Printing instructions](../Building/Printing.md)

### Backplate BOM for All Tools

- [4] m3 heat inserts
- [3] Ø4x12mm ssRod (dowel pin) with a rounded end **(if it has female threads on the back it will be listed as an M3, but make sure the pin is 4mm OD, that is what is important. We recommend the threaded pins for better fixing)**
- [1] 6x3mm magnet (N52 Highly recommended to counter the pull from the umbilicals. Note that most magnets not from a reputable source may say N52 but aren't actually. Recommend one of the two links below.)
- [2] m3x6 or m3x8 FHCS (Flat head countersunk screw, MUST BE MAGNETIC. no stainless, as per TAP)
- [1] [OptoTap](https://s.click.aliexpress.com/e/_DEGsGTV) (only the sensor PCB is required)
- [1] m3x8 BHCS (optional in v1.1)

### BOM Additions for Dragonburner
- [1] m3x12 BHCS (optional to keep spacer in place)
- [2] m3x35 SHCS
- [2] m3 heat inserts
- [2] m3x8 BHCS (optional in v1.1)
- Several 5x2 or 5x3 N52 magnets to hold toolhead to dock (Highly recommended for non-magnetic docks)


## Toolhead Options & Mods
**Note:** Dragonburner [extended mount](https://github.com/chirpy2605/voron/tree/main/general/Alternative_Voron_Mounts/Extended_Extruder_Mounts) is required depending on extruder

* [Dragonburner numbered cowls](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/traxman25) (non-magnetic)
* [Dragonburner cowl mods](https://github.com/DraftShift/StealthChanger/blob/main/UserMods/OstroMa/README.md)
* [Eddy Coil Mount in a DragonBurner Tool-head](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/cekim-git/EddyMount)
  
### PCB mounts
* [recommended] [TheSin's PCB36 mount and backplate](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/TheSin-/PCB36_Mount) for Orbiter 2.5 and HGX Sherpa extruders. Needs [22mm standoffs](https://www.printables.com/model/1440113-m3-heatset-standoffs-10mm-30mm) for Oribiter 2 extruders. 
* [Dragon Burner EBB36 mount for the Orbiter2.0 extruder](https://github.com/DraftShift/StealthChanger/blob/main/UserMods/cekim/Readme.md)
* [Dragonburner Orbiter  EBB36 mount](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/traxman25/Dragonburner_EBB36_SC_Mount)

### Umbilical attachment

* [NH36 Sock](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/Nic335/NH36Sock) for board using theSin's PCB36 mount. But zip-ties work also.


## Dock
* Dock width: 60mm
* Common components for [your dock type](../Docks.md)
* [Modular dock assembly guide](https://github.com/DraftShift/ModularDock/blob/main/Manual/ModularDock_Assembly_Guide.pdf)
* Dragonburner can use stubby docks

### Dock options
* Draftshift official [Dragonburner Back and Base](https://github.com/DraftShift/ModularDock/tree/main/STLs/Dragonburner)
* [Dragonburner magnetic dock](https://www.printables.com/model/1431016-stealthchanger-dragon-burner-modular-dock-6-mag) (no uprights needed)
* DraftShift official [Stubby base](https://github.com/DraftShift/ModularDock/tree/main/STLs/Dragonburner)
* [Angry docks for magnetic Dragonburner](https://www.printables.com/model/1461410-angrydock-dragonburner-for-stealthchanger)  ([discord link](https://discord.com/channels/1226846451028725821/1372881432187506739))
* [Screw docks](https://www.printables.com/model/911717-stealthchanger-screw-docks) (for hooking on toolheads)


## Tips & Suggestions
* NOTE: If you plan on using the Tapchanger Dragonburner dock you must use the [custom cowl by OstroMa](https://github.com/DraftShift/StealthChanger/blob/main/UserMods/OstroMa/DB_Cowl_v8_with_TapChanger_Dock_Hooks.stl). 

* We always recommend to use the original cowls when possible and the [Modular Dock](https://github.com/DraftShift/ModularDock) does not require any special Cowl, print the original from the Dragonburner repo.






