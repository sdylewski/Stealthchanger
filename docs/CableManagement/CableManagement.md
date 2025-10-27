---
title: Electronics & Cable Management
nav_order: 4
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Electronics & Cable Management
Lots of toolheads mean lots of extra wires and filament that needs to be managed properly. With the umbilicals going to the exhaust port there are several options to connect them and to clean up the bundle with a "backpack" mounted on the back of the printer.

<img src="../media/CableManagement/LDO_Stealthchanger_back_annotated.png" width="400">

## Components
* [Backpack](#Backpack) - holds any power and data distribution boards 
* [Umbilicals](Umbilicals.md) & Umbilical plate - wiring and bowden tube going from toolhead to rear of printer.
* [Power Requirements](Power.md) - Make sure you're getting enough power.
* [Filament management](FilamentManagement.md) - Options for how to manage 2-6 spools and tubes going everywhere.

# FAQ

### I'm getting a lot of TTCs, what gives
There are several possible reasons for Timer Too Close errors from Klipper:

1. Your host is doing too much work: CPU load is high and Klipper can't process messages in time. Make sure you don't run too many things, assign Klipper to a separate core and run the host with the performance governor so CPU doesn't scale down in speed. Also make sure your host isn't overheating, the CPU throttles if it does.

2. You saturate the USB bus or USB controller, especially for USB2.0: A high resolution fast FPS webcam will saturate the bus quickly, leaving little room for other messages to get through in time. This is also a problem with CAN bus because you're using an USB to CAN adapter or your mainboard is acting as a CAN bridge and communication with the host and mainboard is also over USB.

3. Your wires have flaky crimps: 
If the problem is always with one specific toolhead and the bytes_retransmit shoots up suddenly it's likely a bad crimp or broken wire on the cable. It's possible that issues only show themselves in a fully heated chamber, or with specific movements of the toolhead during a print.

4. You saturated the CAN bus:
LED effects will greatly increase the number of messages the CAN bus has to process. Using a rounded path with very fine resolution also causes a ton of messages, this will overload the CAN bus queue and messages won't be processed in time.

5. You've angered the 3d printer gods:
Try praying?








