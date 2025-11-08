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

### I'm getting a lot of "Timer Too Close" errors, what gives?
There are several possible reasons for Timer Too Close (TTC) errors from Klipper:

1. Your wires have **flaky crimps**:
If the problem is always with one specific toolhead and the bytes_retransmit shoots up suddenly it's likely a bad crimp or broken wire on the cable. It's possible that issues only show themselves in a fully heated chamber, or with specific movements of the toolhead during a print.

2. Your host is doing too much work: **CPU load is high** and Klipper can't process messages in time. Make sure you don't run too many things, assign Klipper to a separate core and run the host with the performance governor so CPU doesn't scale down in speed. Also make sure your host isn't overheating, the CPU throttles if it does.

3. Your host is running out of memory (>= 60-70% of available memory is used). Once memory pressure starts to build up Klipper will try to garbage collect to free up some memory. However if those GC events take too long this will result in a TTC. Avoid memory pressure at all costs. Some Klipper addons might be taking up considerable amount of memory so consider commenting out unnecessary things for printing in in the printer config.

4. You **saturated the USB bus or USB controller**, especially for USB2.0: A high resolution fast FPS webcam will saturate the bus quickly, leaving little room for other messages to get through in time. This is also a problem with CAN bus because you're using an USB to CAN adapter or your mainboard is acting as a CAN bridge and communication with the host and mainboard is also over USB.

5. You **saturated the CAN bus**:
LED effects will greatly increase the number of messages the CAN bus has to process. Using a rounded path with very fine resolution also causes a ton of messages, this will overload the CAN bus queue and messages won't be processed in time.

6. Your CAN bus is **not having enough resistance between CAN High and CAN Low**:
Make sure you have 60ohms (if possible) between CAN high and CAN low, any less and noise might muddy up the signals, causing retransmits and potentially not having messages processed in time. Have only 2 termination resistors on the bus (unless you have SB2209s which might need more). See [CAN termination layout and common issues](../CableManagement/ElectricalDistribution.md#can-termination-layout-and-common-issues).

7. Your MCU and host version of Klipper is too different
This is usually not a problem and Klipper is generally pretty good at keeping compatibility with older firmware versions but it's always possible that something fundamentally changed that the old Klipper firmware does not know how to deal with well. Make sure your firmware and host Klipper versions are in sync.

8. You've angered the 3d printer gods:
Try praying or sacrifice an Ender3 in the parking lot.
