---
title: Installation
nav_order: 1
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Installation

All sections are required, so please follow all steps carefully.

**Prerequisites:**
- **Klipper version:** Must be newer than Jun 14, 2024 (commit 1591a51)
- **DangerKlipper:** Not currently supported
- **Before starting:** Remove your existing `PRINT_START` and `PRINT_END` macros from your config, as klipper-toolchanger-easy provides specific versions required for toolchanging

## Installing klipper-toolchanger-easy

[klipper-toolchanger-easy](https://github.com/jwellman80/klipper-toolchanger-easy) is the recommended toolchanger software for StealthChanger. The original [klipper-toolchanger](https://github.com/viesturz/klipper-toolchanger/) is no longer maintained and the "easy" fork is actively developed.

### Installation Methods

#### Method 1: Installation Script (Recommended)

The easiest way to install klipper-toolchanger-easy is using the provided installation script:

**On your Klipper host system:**
```bash
cd ~
git clone https://github.com/jwellman80/klipper-toolchanger-easy.git
cd klipper-toolchanger-easy
./install.sh
```

The installation script will:
- Install the toolchanger files to your Klipper config directory
- Set up the necessary directory structure
- Configure Moonraker for automatic updates (optional)

#### Method 2: Manual Installation

If you prefer manual installation or need more control:

**On your Klipper host system:**
```bash
cd ~
git clone https://github.com/jwellman80/klipper-toolchanger-easy.git
cd klipper-toolchanger-easy
# Copy files to your config directory
cp -r stealthchanger ~/printer_data/config/
```

### Moonraker Update Manager (Recommended)

To keep klipper-toolchanger-easy automatically updated, add this to your `moonraker.conf`:

```ini
[update_manager klipper-toolchanger-easy]
type: git_repo
path: ~/klipper-toolchanger-easy
origin: https://github.com/jwellman80/klipper-toolchanger-easy.git
primary_branch: main
managed_services: klipper
```

**Note:** If you make manual changes to the installed files, they will be overwritten when Moonraker updates. Use the configuration override files instead (see [Configuration](Configuration.md)).

### Include in printer.cfg

Add this line to your `printer.cfg` to include the toolchanger configuration:

```ini
[include stealthchanger/toolchanger-config.cfg]
```

## Post-Installation Configuration

After installation, you need to:

1. **Configure tool files:** Update `stealthchanger/tools/Tx.cfg` for each tool (T0.cfg, T1.cfg, etc.)
2. **Update toolchanger-config.cfg:** Configure:
   - `homing_override_config` - Your homing sequence
   - `_CALIBRATION_SWITCH` section - If using a calibration probe
   - `tools_calibrate` - Tool calibration settings
3. **Set up tool configurations:** See [Configuration](Configuration.md) for detailed instructions

**Important Notes:**
- When using sensorless Y homing, ensure `homing_retract_dist` in `[stepper_y]` is set to `0` as per [Voron Docs](https://docs.vorondesign.com/community/howto/clee/sensorless_xy_homing.html)
- The installation creates a `stealthchanger` directory in your config folder with all necessary files
- Tool configuration files are located in `stealthchanger/tools/`

See [Configuration](Configuration.md) for the next steps.
