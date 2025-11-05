---
title: Installation
nav_order: 1
parent: Software & Configuration
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

(original page, needs to be updated)


All sections are required, so please follow all steps carefully.

1. [Klipper Addon](#klipper-addon)
2. [Toolchanger Configuration](#toolchanger-configuration)

**NOTE:** DangerKlipper is not currently supported


**NOTE:** Your klipper version eneds to be newer than Jun 14, 2024 (1591a51)


**NOTE:** Before you start remove your `PRINT_START` and `PRINT_END` macros out of the config as toolchanging requires a specific version of these to initialize and start printing.

## Klipper Addon

You must install [klipper-toolchanger-easy](https://github.com/jwellman80/klipper-toolchanger-easy), Follow instruction on the linked page.

***Note*** The original [klipper-toolchanger](https://github.com/viesturz/klipper-toolchanger/) isn't working and the "easy" fork is recommended.


## Toolchanger Configuration

* update your config file for each tool in toolchanger/tools/Tx.cfg (T0.cfg, T1.cfg, etc)
* look through toolchanger-config.cfg and update
	* homing_override_config
	* _CALIBRATION_SWITCH section
	* tools_calibrate



**NOTE:** when using sensorless Y make sure that the `homing_retract_dist` in the `[stepper_y]` section is set to 0 as per [Voron Docs](https://docs.vorondesign.com/community/howto/clee/sensorless_xy_homing.html)

You can either add them manually to your klipper install, or alternatively, you can integrate them to your config so that moonraker keeps them up to date with your other software if they change. Below are the steps for the integrated way. If you make any changes to the files though, they will be overwritten if you update. If you choose to manually add them, make sure your printer.cfg reflects the location of them.

**On the Klipper System** 
```
cd ~
git clone https://github.com/viesturz/tapchanger.git --no-checkout --depth 1 --filter=blob:none
cd tapchanger
git sparse-checkout init --cone
git sparse-checkout set Klipper
git checkout
cd ~
ln -s ~/tapchanger/Klipper/config-example ~/printer_data/config/tapchanger
```

**Add to moonraker.conf**
```
[update_manager tapchanger]
type: git_repo
path: ~/tapchanger
origin: https://github.com/viesturz/tapchanger.git
primary_branch: main
managed_services: klipper
```
