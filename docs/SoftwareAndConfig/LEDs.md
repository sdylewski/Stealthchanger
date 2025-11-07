---
title: LEDs
nav_order: 5
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# LEDs

StealthChanger supports various types of addressable RGB LEDs for both functional lighting and aesthetic effects. This guide covers how to configure and control color LEDs on your StealthChanger.

## Overview

StealthChanger can use addressable RGB LEDs in several locations:
- **Toolhead LEDs** - Nozzle LEDs and part cooling fan LEDs on each toolhead
- **Logo LEDs** - StealthChanger logo PCBs with integrated LEDs (Rainbow Barf)
- **Frame LEDs** - Optional LED strips for frame lighting
- **Status Indicators** - Functional LEDs for printer status

### Supported LED Types

- **WS2812/WS2812B** - Most common, 3-wire (5V, Data, GND)
- **SK6812** - Similar to WS2812, supports RGBW variants
- **SK6805-EC15** - Used in SC Barf PCBs (1.5mm RGB LEDs)
- **Neopixel** - Generic term often referring to WS2812-compatible LEDs

**Note:** Most addressable LEDs use the same protocol and can be controlled the same way in Klipper.

## Basic LED Configuration

### Neopixel Configuration

For basic LED control, configure a `[neopixel]` section in your `printer.cfg`:

```ini
[neopixel my_leds]
pin: ar6                    # GPIO pin connected to LED data line
chain_count: 16             # Number of LEDs in the chain
color_order: GRB            # Color order (GRB, RGB, RGBW, etc.)
initial_RED: 0.3            # Initial red brightness (0.0-1.0)
initial_GREEN: 0.3          # Initial green brightness
initial_BLUE: 0.0           # Initial blue brightness
```

### Toolhead LEDs

Each toolhead can have its own LED configuration. In your tool config files (`stealthchanger/tools/Tx.cfg`), you can define LEDs specific to that tool:

```ini
[neopixel toolhead_leds]
pin: toolhead:PB3           # Pin on toolhead board (CAN bus)
chain_count: 3              # Number of LEDs (e.g., nozzle LEDs)
color_order: GRB
```

**Important:** 
- Toolhead LEDs are typically controlled via CAN bus
- Each tool can have different LED configurations
- RGB LEDs are recommended (not RGBW) for compatibility with some effects

### Controlling LEDs

Basic LED control via G-code:

```gcode
# Set all LEDs to a specific color
SET_LED LED=my_leds RED=1.0 GREEN=0.0 BLUE=0.0

# Set brightness
SET_LED LED=my_leds RED=0.5 GREEN=0.5 BLUE=0.5

# Turn off LEDs
SET_LED LED=my_leds RED=0 GREEN=0 BLUE=0
```

## Rainbow Barf LEDs (SC Barf)

Rainbow Barf LEDs are custom PCBs with 1.5mm RGB LEDs arranged in the StealthChanger logo pattern. Available in both Voron and Micron styles.

### Hardware

- **PCB Source:** [SC Barf LEDs](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/SC_Barf)
- **LED Type:** SK6805-EC15 (1.5mm RGB LEDs)
- **LED Count:** 
  - 21 LEDs for Voron style
  - 19 LEDs for Micron style

### Configuration

Add this to your `printer.cfg`:

```ini
[neopixel rgb_logo]
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

### Toolhead-Specific Rainbow Barf

Some toolheads have mods for SC Barf LEDs:
- [Stealthburner SC Barf](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/StealthBurner_SC_Barf) - Note: Requires RGB nozzle LEDs, not RGBW

## LED Effects Plugin

[LED Effects](https://github.com/julianschill/klipper-led_effect) is a powerful Klipper plugin that enables dynamic lighting effects and animations for addressable LEDs.

### Installation

#### Method 1: Manual Installation

1. **Clone the repository:**
   ```bash
   cd ~
   git clone https://github.com/julianschill/klipper-led_effect.git
   ```

2. **Stop Klipper:**
   ```bash
   sudo systemctl stop klipper
   ```

3. **Create symbolic link:**
   ```bash
   ln -s ~/klipper-led_effect/src/led_effect.py ~/klipper/klippy/extras/led_effect.py
   ```

4. **Start Klipper:**
   ```bash
   sudo systemctl start klipper
   ```

5. **Add to Moonraker for updates:**
   
   Add this to your `moonraker.conf`:
   ```ini
   [update_manager led_effect]
   type: git_repo
   path: ~/klipper-led_effect
   origin: https://github.com/julianschill/klipper-led_effect.git
   is_system_service: False
   ```

#### Method 2: KIAUH Installation

If you use [KIAUH](https://github.com/th33xitus/kiauh), LED Effects can be installed through the KIAUH interface:
1. Run KIAUH: `./kiauh/kiauh.sh`
2. Select "Advanced" → "Install KlipperLED"
3. Follow the prompts

### Configuration

After installation, configure LED effects in your `printer.cfg`:

#### Basic Effect Example

```ini
[led_effect my_effect]
autostart: true                    # Start effect automatically
frame_rate: 24                     # Frames per second
leds:
    neopixel:rgb_logo              # Reference your neopixel section
layers:
    breathing 10 1 top (0.5, 0.5, 1)  # Breathing effect, blue color
```

#### Common Effects

**Breathing:**
```ini
layers:
    breathing 10 1 top (1.0, 0.0, 0.0)  # Red breathing, 10s cycle
```

**Rainbow:**
```ini
layers:
    rainbow 5 1 top                 # Rainbow effect, 5s cycle
```

**Static Color:**
```ini
layers:
    static 1 top (0.0, 1.0, 0.0)    # Static green
```

**Chase:**
```ini
layers:
    chase 2 1 top (1.0, 1.0, 0.0)   # Yellow chase effect
```

**Knight Rider:**
```ini
layers:
    knight_rider 3 1 top (1.0, 0.0, 0.0)  # Red knight rider
```

#### Multiple Layers

You can combine multiple effects:

```ini
[led_effect complex_effect]
autostart: false
frame_rate: 30
leds:
    neopixel:rgb_logo
layers:
    rainbow 10 0.5 top              # Rainbow base layer
    chase 2 1 top (1.0, 1.0, 1.0)  # White chase overlay
```

### Controlling Effects via G-code

**Start an effect:**
```gcode
SET_LED_EFFECT EFFECT=my_effect
```

**Stop an effect:**
```gcode
SET_LED_EFFECT EFFECT=my_effect STOP=1
```

**Fade in effect:**
```gcode
SET_LED_EFFECT EFFECT=my_effect FADETIME=1.0
```

**List available effects:**
```gcode
HELP SET_LED_EFFECT
```

### Status-Based Effects

LED Effects can respond to printer status:

```ini
[led_effect print_status]
autostart: true
frame_rate: 24
leds:
    neopixel:rgb_logo
layers:
    static 1 top (0.0, 1.0, 0.0)    # Green when idle
    static 1 printing (0.0, 0.0, 1.0)  # Blue when printing
    static 1 error (1.0, 0.0, 0.0)  # Red on error
```

### Advanced Configuration

For more complex effects and full documentation, see the [LED Effects GitHub repository](https://github.com/julianschill/klipper-led_effect).

## Troubleshooting

### LEDs Not Working

1. **Check wiring:**
   - Verify 5V power supply is adequate (each LED can draw ~60mA at full brightness)
   - Check data line connection
   - Ensure proper ground connection

2. **Check configuration:**
   - Verify `chain_count` matches actual LED count
   - Check `color_order` (GRB vs RGB)
   - Confirm GPIO pin is correct

3. **Check Klipper:**
   - Restart Klipper after configuration changes
   - Check Klipper logs for LED-related errors

### LED Effects Not Working

1. **Verify installation:**
   - Check that `led_effect.py` is linked in `~/klipper/klippy/extras/`
   - Restart Klipper after installation

2. **Check configuration:**
   - Ensure `leds:` section references correct neopixel name
   - Verify effect syntax is correct

3. **Check Moonraker:**
   - If using Moonraker updates, ensure the update manager section is correct

### Color Issues

- **Wrong colors:** Try different `color_order` values (GRB, RGB, RGBW)
- **Dim LEDs:** Increase brightness values or check power supply
- **Flickering:** May indicate insufficient power or poor wiring

## Additional Resources

- [LED Effects Documentation](https://github.com/julianschill/klipper-led_effect)
- [Klipper Neopixel Documentation](https://www.klipper3d.org/Config_Reference.html#neopixel)
- [SC Barf LED Repository](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/SC_Barf)
- [Stealthburner SC Barf Mod](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/StealthBurner_SC_Barf)
