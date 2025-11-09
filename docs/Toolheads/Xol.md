---
title: Xol
nav_order: 7
parent: Toolheads
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
# XOL

<img src="../media/Toolheads/Xol.png" width="150">

## References

* [Xol reference page](https://github.com/Armchair-Heavy-Industries/Xol-Toolhead)

## Backplate

* [Backplate (short/medium)](https://github.com/DraftShift/StealthChanger/tree/main/STLs/Backplates)

### Backplate BOM for All Tools

- [4] m3 heat inserts
- [3] Ø4x12mm ssRod (dowel pin) with a rounded end **(if it has female threads on the back it will be listed as an M3, but make sure the pin is 4mm OD, that is what is important. We recommend the threaded pins for better fixing)**
- [1] 6x3mm magnet (N52 Highly recommended to counter the pull from the umbilicals. Note that most magnets not from a reputable source may say N52 but aren't actually. Recommend one of the two links below.)
- [2] m3x6 or m3x8 FHCS (Flat head countersunk screw, MUST BE MAGNETIC. no stainless, as per TAP)
- [1] [OptoTap](https://s.click.aliexpress.com/e/_DEGsGTV) (only the sensor PCB is required)
- [1] m3x8 BHCS (optional in v1.1)

### BOM Additions for XOL

- [2] m3x6 BHCS (backplate lower mounting screws. m3x8 will be too long)
- [2] m3x20 BHCS (backplate upper mounting screws)
- [2] m3x8 BHCS (extruder mount to backplate)
- [2] m3x6 FHCS **magnetic** (preload screws. m3x8 will be too long)
- You will **not be able** to use stock 2.4 Z joints with XOL or A4T.
- Replacement of your Z joints with something with a lower profile such as [hartk123's GE5C Z Joint](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/hartk1213/Voron2.4_GE5C) or [Ellis'Short Z Joints](https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/Ellis/Short_Z_Joints) is necessary to avoid bottoming out your Z carriage on the deck panel when using XOL or A4T.

## PCB Mounting Options

### Official PCB Mounts (Draftshift Design)

*No official PCB mounts from Draftshift Design. See User Mods below.*

### User Mods

*No user mod PCB mounts documented yet. Check the [StealthChanger UserMods](https://github.com/DraftShift/StealthChanger/tree/main/UserMods) directory for community contributions.*

## Toolhead Options & Mods

* [Fan splitter](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/dudewithan02/A4T-Xol-Fan-Splitter-PCB)

## StealthChanger Requirements

* ***Requires*** Shorter Z joints like <a href="https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/hartk1213/Voron2.4_GE5C">Ge5C z-joints</a> so you don't bottom out your carriage when homing.
* Requires new smaller front idlers like the <a href="https://github.com/clee/VoronBFI">BFI</a> or <a href="https://github.com/DraftShift/StealthChanger/tree/main/UserMods/BT123/MiniBFI%20%2B%20MicroBFI">Mini BFI</a> so it doesn't collide with the idlers.

## Dock

| Dock Width | Stubby Dock Compatible |
|------------|------------------------|
| 76mm | ❌ No |

### Official Dock Types (Draftshift Design)

| Dock Type | Description | Link |
|-----------|-------------|------|
| Standard Dock | Full-height dock with back and base | [XOL Back and Base](https://github.com/DraftShift/ModularDock/tree/main/STLs/XOL) |

**Note:** XOL is not compatible with stubby docks due to toolhead geometry.

### User Mods

| Dock Type | Size | Description | Link |
|-----------|------|-------------|------|
| Magdock Adapter | 76mm | Magnetic dock adapter | [Xol Magdock adapter](https://github.com/DraftShift/ModularDock/tree/main/UserMods/MikeYankeeOscarBeta/Xol_magdock_adapter) |
| Magdock Feet | 76mm | Magnetic dock feet | [Xol Magdock feet](https://github.com/DraftShift/ModularDock/tree/main/UserMods/MikeYankeeOscarBeta/Xol_magdock_feet) |
  
