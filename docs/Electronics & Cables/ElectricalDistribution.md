---
title: Electrical Distribution
nav_order: 1
parent: Electronics & Cable Management
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

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


## CAN termination layout and common issues

Unless the toolheads are daisy chained together the CAN bus is more of a CAN star network. That is out of spec but is usually fine. Terminate the CAN bus with 2 termination resistors (usually you have jumpers for that) as usual, one on the main board, one on one of the toolheads. Omit the jumper on the rest of the toolheads to prevent reducing the resistance between CAN L and CAN H.

If you have SB2209s however you might need to add more termination resistors. Add one termination resistor at the time and test if all the boards get picked up, if not add more or move them around, it's unclear what's causing the SB2209 to be more sensitive to reflections, other boards don't have this issue.

Other common issues are usually resolved by going through Esotericals CAN guide https://canbus.esoterical.online/, it's the same process for each toolhead.




