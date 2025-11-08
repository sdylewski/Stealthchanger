---
title: LEDs
nav_order: 7
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# LEDs

StealthChanger supports various types of addressable RGB LEDs for both functional lighting and aesthetic effects. This guide covers how to configure and control color LEDs on your StealthChanger.

## Multi-Toolhead LED Control

Since StealthChanger has multiple toolheads, controlling LEDs works differently than on a single-toolhead machine:

### No Different Libraries Required

**You don't need different libraries** - StealthChanger uses the same Klipper `[neopixel]` support that works on any Klipper printer. The LED Effects plugin also works the same way across all your LEDs.

### Key Differences

1. **Per-Tool Configuration**: Each toolhead can have its own LED configuration defined in its tool config file (`stealthchanger/tools/Tx.cfg`). This means:
   - T0 might have 3 nozzle LEDs
   - T1 might have 5 LEDs (nozzle + additional lighting)
   - Each tool's LEDs are independent

2. **CAN Bus Control**: Toolhead LEDs are typically controlled via CAN bus using the `toolhead:PB3` pin format, while frame/logo LEDs use direct GPIO pins on the main board.

3. **Active Tool LEDs**: When a tool is active on the shuttle, you control that tool's LEDs. When you switch tools, you're now controlling a different set of LEDs.

4. **Multiple LED Sections**: You'll have multiple `[neopixel]` sections:
   - One (or more) for frame/logo LEDs in `printer.cfg`
   - One for each toolhead's LEDs in their respective `Tx.cfg` files

### Example Setup

```ini
# In printer.cfg - Frame/Logo LEDs
[neopixel rgb_logo]
pin: PB3
chain_count: 21
color_order: GRB

# In stealthchanger/tools/T0.cfg - T0 toolhead LEDs
[neopixel T0_nozzle_leds]
pin: toolhead:PB3
chain_count: 3
color_order: GRB

# In stealthchanger/tools/T1.cfg - T1 toolhead LEDs  
[neopixel T1_nozzle_leds]
pin: toolhead:PB3
chain_count: 3
color_order: GRB
```

### LED Effects with Multiple Toolheads

The LED Effects plugin can control LEDs from multiple toolheads simultaneously. Simply reference all the LED sections you want in your effect:

```ini
[led_effect all_tools]
leds:
    neopixel:rgb_logo          # Frame/logo LEDs
    neopixel:T0_nozzle_leds     # T0 LEDs (when T0 is active)
    neopixel:T1_nozzle_leds     # T1 LEDs (when T1 is active)
layers:
    rainbow 5 1 top
```

**Note:** Toolhead LEDs are only accessible when that tool is active on the shuttle. If you want effects that work regardless of which tool is active, focus on frame/logo LEDs or create separate effects for each tool.

## Overview

StealthChanger can use addressable RGB LEDs in several locations:
- **Toolhead LEDs** - Nozzle LEDs and part cooling fan LEDs on each toolhead
- **Logo LEDs** - Custom logo PCBs with integrated LEDs (see [Advanced LEDs](LEDsAdvanced.md))
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

## Advanced LED Options

For custom logo PCBs including Rainbow Barf (Voron/Micron logo) and SC Barf (StealthChanger logo) LEDs, see [Advanced LEDs](LEDsAdvanced.md).

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
- [Advanced LEDs](LEDsAdvanced.md) - Custom logo PCBs and advanced LED options
