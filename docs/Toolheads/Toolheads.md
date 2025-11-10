---
title: Toolheads
nav_order: 2
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
# Toolheads

Many of the most common toolheads are supported.  You may build a dock for your existing toolhead, and then built new toolheads as other types. You can mix and match, but the configs get more complicated because you need to have different ones for each toolhead. 

Note that toolheads go hand-in-hand with their associated docks, and the options/mods available for them. 

Each toolhead page will contain specifics for the backplate, dock, and modifications for that toolhead.

## Toolhead Comparison

Use this table to compare toolheads and help select the right one for your needs:

| Toolhead | Dock Width | Stubby Dock | Crabby Dock | Special Requirements | Notes |
|----------|------------|-------------|-------------|---------------------|-------|
| [<img src="../media/Toolheads/Anthead.png" width=50> **Anthead**](Anthead.md) | 60mm | ✅ Yes | ✅ Yes (Usermod) | None | Modern, popular, built-in magnet holes |
| [<img src="../media/Toolheads/Stealthburner.png" width=50> **StealthBurner**](Stealthburner.md) | 76mm | ❌ No | ✅ Yes (Usermod) | None | Most common, well-supported |
| [<img src="../media/Toolheads/Dragonburner.png" width=50> **DragonBurner**](Dragonburner.md) | 60mm | ✅ Yes | ❌ No | None | Good extruder compatibility |
| [<img src="../media/Toolheads/Dragonburner.png" width=50> **RapidBurner**](Dragonburner.md) | 60mm | ✅ Yes | ❌ No | None | UHF version of DragonBurner |
| [<img src="../media/Toolheads/MiniSB.png" width=50> **MiniSB**](MiniSB.md) | 60mm | ✅ Yes | ❌ No | None | Compact StealthBurner variant |
| [<img src="../media/Toolheads/yavoth.png" width=50> **Yavoth**](Yavoth.md) | 60mm | ✅ Yes | ❌ No | None | V0-style toolhead |
| [<img src="../media/Toolheads/Xol.png" width=50> **XOL**](XOL.md) | 76mm | ❌ No | ❌ No | Requires shorter Z joints, smaller front idlers | Compact design |
| [<img src="../media/Toolheads/A4t.png" width=50> **A4T**](A4T.md) | 76mm | ❌ No | ❌ No | Requires shorter Z joints, smaller front idlers | Compact design |
| [<img src="../media/Toolheads/SV08.png" width=50> **SV08**](SV08.md) | 60mm | ✅ Yes | ❌ No | None | Integrated extruder toolhead |
| [<img src="../media/Toolheads/Blackbird.jpg" width=50> **Blackbird**](Blackbird.md) | 76mm | ❌ No | ❌ No | None | Archetype series toolhead |
| [<img src="../media/Toolheads/Jabberwocky.png" width=50> **Jabberwocky**](Jabberwocky.md) | 76mm | ❌ No | ❌ No | None | Kinematic toolhead |

**Notes:**
- **Dock Width**: Determines which dock size you need. 60mm docks are more compact, 76mm docks provide more space.
- **Stubby Dock**: Whether the toolhead can use shorter "stubby" docks - saves ~10mm Y build space. Official from Draftshift Design.
- **Crabby Dock**: Whether "crabby" style docks are available as user mods. Crabby docks are minimal docks with no vertical supports - just a shaped plate bolted directly to the crossbar. They may require additional securing methods (screws with PTFE tubes, magnets) to keep toolheads properly positioned. All crabby docks are user mods, not official Draftshift Design.
- **Special Requirements**: Additional printer modifications needed (e.g., shorter Z joints, different idlers).



---



## Selecting a new toolhead?

### Toolheads
* [Awesome-Toolheads](https://github.com/SartorialGrunt0/Awesome-Toolheads?tab=readme-ov-file)
* [Toolhead comparison](https://3dp-info.fyi/toolhead-comparison)

### Extruders
* [Awesome-Extruders](https://github.com/SartorialGrunt0/Awesome-Toolheads?tab=readme-ov-file)
* [Extruder comparision](https://3dp-info.fyi/extruder-comparison)



# Toolheads FAQ

**Quick Links:**
- [Can I mix and match different toolheads and hotends?](#can-i-mix-and-match-different-toolheads-and-hotends)
- [What about different hotends that have higher/lower flow rates?](#what-about-different-hotends-that-have-higherlower-flow-rates)
- [What about different nozzle sizes?](#what-about-different-nozzle-sizes)
- [What is ooze prevention and pre-heating?](#what-is-ooze-prevention-and-pre-heating)
- [It picks up the tool and then waits for a long time](#it-picks-up-the-tool-and-then-waits-for-a-long-time-before-continuing)
- [The wires of my toolboard get snagged](#the-wires-of-my-toolboard-get-snagged-when-doing-a-tool-change)

---

### Can I mix and match different toolheads and hotends?
Yes to a certain degree. The parking position of the various toolheads has to be more or less the same, if one toolhead is significantly higher or lower then the gantry will bump into the pins of its backplate when trying to pick up other tools. You would need to add dock spacers to ensure that all the pins of each backplate are somewhat on the same height. Calibration for things like pressure advance is also more difficult, but possible.

### What about different hotends that have higher/lower flow rates
Yes, you would need to configure that in your slicer per extruder. If you can't you would need to make a filament profile per extruder (PLA - T0, PLA - T1) and configure it that way, assigning the correct filament profile to the right tool.

### What about different nozzle sizes?
Yes, if your slicer supports it. Orca slicer does.

### What is ooze prevention and pre-heating
Orca slicer has a feature to prevent oozing of tools that are actively being used, by dropping their temperature to an idle temperature. It also can ramp up the temperature back up by a set amount of seconds before the tool is actually being called to make sure the toolhead is ready to go without waiting. This also has the added benefit of not cooking your filament for long periods of time and preventing heat creep, so it's definitely recommended.
(add link for how to enable)

### It picks up the tool and then waits for a long time before continuing
This is likely Klipper waiting for the temperature of the hotend to settle to the target temperature. If your hotend is not well PID tuned it can sometimes oscillate indefinitely around the target temperature. By default this margin is quite small, only 0.5°C. This is usually not a problem for single toolhead printers as your hotend only heats up once, but with a toolchanger where it heats up the tool every tool call this can introduce a lot of delay. Depending on your klipper-toolchanger version you can mitigate this by increasing the deadband, the amount of °C around the target temperature that is considered "good enough to continue".

### The wires of my toolboard get snagged when doing a tool change
Either shorten your wires, tuck them away with zip ties or use a pcb cover if your toolhead has one
<br/>
<img src="../media/Toolheads/toolhead_pcbcover.jpg" width=200>








