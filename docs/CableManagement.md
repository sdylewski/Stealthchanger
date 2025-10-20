<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
---
title: Cable management
nav_order: 4
parent: Home
---

# What 

Lots of toolheads mean lots of extra wires that need to be managed properly. With the umbilicals going to the exhaust there are several options to connect them and to clean up the bundle with a backpack.

## Backpack

FannyPack (https://github.com/DraftShift/CableManagement/tree/main/FannyPack) is most used to create a backpack to mount distribution boards and clean up the mess at the back. 

There is also Hexa backpack https://github.com/MikeYankeeOscarBeta/hexabackpack 

Specifically for the Fysetc Hexa distro fusion board (https://www.printables.com/model/1366367-fysetc-hexa-distro-fusion-backpack) (though there is also a usermod for the Fysetc hexa distro fusion board for FannyPack: https://github.com/patrezp/CableManagement/tree/main/UserMods/patrezp/Fysetc_Hexa_distro_fusion_mod)

# Distribution

## USB
* // TODO usb distribution boards
## CAN

* Wago's: the cheapest and easiest way is to connect all your V_in, GND, CAN_L and CAN_H respectively together with wago's.

* Fysetc Hexa distro fusion board https://wiki.fysetc.com/docs/hexa_distro_fusion
* Fysetc CAN BUS distribution board (this is the predecessor to the hexa distro fusion board)
* CEB
* // TODO all the other common options 


Make sure that the V_in and GND wire that goes from the PSU to your wago's or distribution board has a thicker gauge as it will carry the power of all the toolheads combined. To calculate the wire gauge, calculate the max power consumption of all your toolheads combined, take a healthy margin and use a wire gauge calculator that gives you the cross section or AWG required.

## Bowden tube routing
Depending on where you have your filament spools https://github.com/DraftShift/CableManagement/tree/main/UserMods/N3MI-DG/Filament_Entry can be useful to clean up the bowden tube paths.


## CAN termination layout and common issues

Unless the toolheads are daisy chained together the CAN bus is more of a CAN star network. That is out of spec but is usually fine. Terminate the CAN bus with 2 termination resistors (usually you have jumpers for that) as usual, one on the main board, one on one of the toolheads. Omit the jumper on the rest of the toolheads to prevent reducing the resistance between CAN L and CAN H.

If you have SB2209s however you might need to add more termination resistors. Add one termination resistor at the time and test if all the boards get picked up, if not add more or move them around, it's unclear what's causing the SB2209 to be more sensitive to reflections, other boards don't have this issue.

Other common issues are usually resolved by going through Esotericals CAN guide https://canbus.esoterical.online/, it's the same process for each toolhead.


