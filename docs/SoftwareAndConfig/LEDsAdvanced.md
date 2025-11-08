---
title: Advanced LEDs
nav_order: 6
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Advanced LEDs

This page covers advanced LED options including custom logo PCBs for StealthChanger.

## Rainbow Barf LEDs

Rainbow Barf LEDs are small PCBs with 1.5mm RGB LEDs arranged in the Voron or Micron logo pattern. These compact boards are designed to mount on toolheads and provide logo lighting. They can be purchased online now without ordering PCBs yourself.

### Hardware

- **PCB Source:** [Rainbow Barf LEDs](https://github.com/tanaes/whopping_Voron_mods/tree/main/LEDs/Rainbow_Barf_Logo_LED)
- **LED Type:** SK6805-EC15 (1.5mm RGB LEDs)

- **Use Case:** Toolhead-mounted logo lighting

### Configuration

Configure in your tool config file (`stealthchanger/tools/Tx.cfg`) for toolhead mounting:

```ini
[neopixel rainbow_barf]
pin: toolhead:PB3           # Pin on toolhead board (CAN bus)
color_order: GRB            # SK6805 uses GRB order
chain_count: 21             # 21 for Voron, 19 for Micron
initial_RED: 0.3
initial_GREEN: 0.3
initial_BLUE: 0.0
```

Or in `printer.cfg` for frame mounting:

```ini
[neopixel rainbow_barf]
pin: PB3                    # GPIO pin (adjust to your setup)
color_order: GRB
chain_count: 21
initial_RED: 0.3
initial_GREEN: 0.3
initial_BLUE: 0.0
```

## StealthChanger Barf (SC Barf) LEDs

SC Barf LEDs are larger PCBs with 1.5mm RGB LEDs arranged in the StealthChanger logo pattern. These are designed for frame mounting and provide prominent logo lighting.

### Hardware

- **PCB Source:** [SC Barf LEDs](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/SC_Barf)
- **LED Type:** SK6805-EC15 (1.5mm RGB LEDs)

- **Use Case:** Frame-mounted StealthChanger logo lighting

### Configuration

Add this to your `printer.cfg`:

```ini
[neopixel sc_barf_logo]
pin: PB3                    # GPIO pin (adjust to your setup)
color_order: GRB            # SK6805 uses GRB order
chain_count: 21             # 21 for Voron, 19 for Micron
initial_RED: 0.3
initial_GREEN: 0.3
initial_BLUE: 0.0
```

### Ordering PCBs

The SC Barf PCBs can be ordered from JLCPCB:

1. Add the Gerber zip file from the [SC Barf repository](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/SC_Barf)
2. Select PCB quantity and color
3. Select `Order Number(Specify Position)`
4. Enable PCB Assembly
5. Select `Added by Customer` in Tooling holes section
6. Add BOM file `BOM-JLC.csv`
7. Add CPL file `CPL-JLC.csv`
8. Process BOM & CPL and verify component placement
9. Complete checkout

**Note:** If `SK6805-EC15` is out of stock, `DY-S1515065/RGBC/6805-5T` by TONYU is compatible but the JLC footprint is rotated 180 degrees. Verify correct orientation during placement.

### Toolhead-Specific SC Barf

Some toolheads have mods for SC Barf LEDs:
- [Stealthburner SC Barf](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/StealthBurner_SC_Barf) - Note: Requires RGB nozzle LEDs, not RGBW to work with LED Effects
- Dragonburner

## Additional Resources

- [SC Barf LED Repository](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/SC_Barf)
- [Stealthburner SC Barf Mod](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/StealthBurner_SC_Barf)

