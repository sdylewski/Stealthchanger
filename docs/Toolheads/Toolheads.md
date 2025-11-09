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

| Toolhead | Dock Width | Supported PCBs | Stubby Dock | Special Requirements | Notes |
|----------|------------|----------------|-------------|---------------------|-------|
| [<img src="../media/Toolheads/Anthead.png" width=50> **Anthead**](Anthead.md) | 60mm | EBB36, Nighthawk36, SHT36 | ✅ Yes | None | Modern, popular, built-in magnet holes |
| [<img src="../media/Toolheads/Stealthburner.png" width=50> **StealthBurner**](Stealthburner.md) | 76mm | EBB36, SB2040, SB2209 | ❌ No | None | Most common, well-supported |
| [<img src="../media/Toolheads/Dragonburner.png" width=50> **DragonBurner**](Dragonburner.md) | 60mm | EBB36, Nighthawk36, SHT36 | ✅ Yes | None | Good extruder compatibility |
| [<img src="../media/Toolheads/Dragonburner.png" width=50> **RapidBurner**](Dragonburner.md) | 60mm | EBB36, Nighthawk36, SHT36 | ✅ Yes | None | UHF version of DragonBurner |
| [<img src="../media/Toolheads/MiniSB.png" width=50> **MiniSB**](MiniSB.md) | 60mm | EBB36, Nighthawk36, SHT36 | ✅ Yes | None | Compact StealthBurner variant |
| [<img src="../media/Toolheads/yavoth.png" width=50> **Yavoth**](Yavoth.md) | 60mm | EBB36, Nighthawk36, SHT36 | ✅ Yes | None | V0-style toolhead |
| [<img src="../media/Toolheads/Xol.png" width=50> **XOL**](XOL.md) | 76mm | EBB36, Nighthawk36, SHT36 | ❌ No | Requires shorter Z joints, smaller front idlers | Compact design |
| [<img src="../media/Toolheads/A4t.png" width=50> **A4T**](A4T.md) | 76mm | EBB36, Nighthawk36, SHT36 | ❌ No | Requires shorter Z joints, smaller front idlers | Compact design |
| [<img src="../media/Toolheads/SV08.png" width=50> **SV08**](SV08.md) | 60mm | EBB36, Nighthawk36, SHT36 | ✅ Yes | None | Integrated extruder toolhead |
| [<img src="../media/Toolheads/Blackbird.jpg" width=50> **Blackbird**](Blackbird.md) | 76mm | EBB36, Nighthawk36, SHT36 | ❌ No | None | Archetype series toolhead |
| [<img src="../media/Toolheads/Jabberwocky.png" width=50> **Jabberwocky**](Jabberwocky.md) | 76mm | EBB36, Nighthawk36, SHT36 | ❌ No | None | Kinematic toolhead |

**Notes:**
- **Dock Width**: Determines which dock size you need. 60mm docks are more compact, 76mm docks provide more space.
- **Supported PCBs**: Most toolheads support EBB36, Nighthawk36 (NH36), and SHT36 boards. Some may have specific mounts available - check individual toolhead pages for details.
- **Stubby Dock**: Whether the toolhead can use shorter "stubby" docks (no vertical supports, crossbar attachment only).
- **Special Requirements**: Additional printer modifications needed (e.g., shorter Z joints, different idlers).

**PCB Compatibility:**
- **EBB36**: Most common CAN bus toolhead board (BTT EBB36)
- **Nighthawk36 (NH36)**: Alternative CAN bus toolhead board
- **SHT36**: Alternative CAN bus toolhead board (formerly Mellow36)
- **SB2040/SB2209**: StealthBurner-specific boards (less common)

For specific PCB mounting solutions, see each toolhead's individual page.

---



## Selecting a new toolhead?

### Toolheads
* [Awesome-Toolheads](https://github.com/SartorialGrunt0/Awesome-Toolheads?tab=readme-ov-file)
* [Toolhead comparison](https://3dp-info.fyi/toolhead-comparison)

### Extruders
* [Awesome-Extruders](https://github.com/SartorialGrunt0/Awesome-Toolheads?tab=readme-ov-file)
* [Extruder comparision](https://3dp-info.fyi/extruder-comparison)

### Hotends

Common hotends (AI-generated, so please confirm values):

| Hotend Model | Max Flow Rate (mm³/s) | Weight (g) | Max Temp (°C) | Wattage (W) | Notes |
|--------------|----------------------|------------|---------------|-------------|-------|
| **[E3D V6](https://e3d-online.com/products/v6-all-metal-hotend)** | ~11 | ~45 | 285 | 40 | Standard all-metal, widely compatible |
| **[E3D Revo 6](https://e3d-online.com/products/revo-6-hotend)** | ~15 | ~50 | 300 | 50 | Quick-swap nozzles, no tools needed |
| **[Phaetus Dragon HF](https://www.phaetus.com/products/dragon-high-flow-hotend)** | ~24 | ~35 | 500 | 50 | High-flow, lightweight, popular choice |
| **[Phaetus Dragon UHF](https://www.phaetus.com/products/dragon-ultra-high-flow-hotend)** | ~30 | ~35 | 500 | 50 | Ultra-high-flow variant |
| **[Phaetus Rapido HF](https://www.phaetus.com/products/rapido-hotend)** | ~24 | ~30 | 500 | 50 | Fast heating, high-flow |
| **[Phaetus Rapido UHF](https://www.phaetus.com/products/rapido-ultra-high-flow-hotend)** | ~30 | ~30 | 500 | 50 | Ultra-high-flow, fastest heating |
| **[Slice Engineering Mosquito](https://www.sliceengineering.com/products/mosquito-hotend)** | ~31 | ~37 | 500 | 50 | Modular design, easy maintenance |
| **[Slice Engineering Mosquito Magnum](https://www.sliceengineering.com/products/mosquito-magnum-hotend)** | ~34 | ~41 | 500 | 50 | Enhanced flow, larger melt zone |
| **[Micro Swiss FlowTech CHT](https://store.micro-swiss.com/products/flowtech-cht-hotend)** | ~50 | ~45 | 300 | 40 | Multi-chamber design, highest flow |
| **[TriangleLab Rapido](https://www.trianglelab.net/products/rapido-hotend)** | ~45 | ~30 | 500 | 50 | High-flow, integrated heatsink |
| **[TriangleLab Rapido Ace](https://www.trianglelab.net/products/rapido-ace-hotend)** | ~50 | ~30 | 500 | 60 | Enhanced flow, higher wattage heater |
| **[TriangleLab Dragon Ace](https://www.trianglelab.net/products/dragon-ace-hotend)** | ~35 | ~35 | 500 | 50 | High-flow Dragon variant with enhanced heater |
| **[TriangleLab Dragon Ace HF](https://www.trianglelab.net/products/dragon-ace-hf-hotend)** | ~40 | ~35 | 500 | 50 | High-flow variant of Dragon Ace |
| **[TriangleLab Dragon Ace UHF](https://www.trianglelab.net/products/dragon-ace-uhf-hotend)** | ~45 | ~35 | 500 | 60 | Ultra-high-flow variant with higher wattage heater |

**Notes:**
- **Max Flow Rate**: Maximum volumetric flow rate in mm³/s. Actual performance depends on filament type, temperature, and nozzle size.
- **Weight**: Approximate hotend weight. Lighter hotends allow higher accelerations and better print quality at speed.
- **Max Temp**: Maximum safe operating temperature. Higher temps enable printing high-temperature materials (ABS, PC, etc.).
- **Wattage**: Heater cartridge power rating. Higher wattage enables faster heating and better temperature stability at high flow rates.
- Flow rates are approximate and can vary based on nozzle size, filament type, and temperature settings.
- UHF (Ultra-High-Flow) variants typically require higher temperatures and may need more powerful heaters for optimal performance.
- Check individual toolhead pages for specific mount requirements and compatibility.

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








