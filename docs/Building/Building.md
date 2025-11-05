---
title: Building
nav_order: 2
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Building

Converting or building a StealthChanger is a challenging build. Before getting started, you will need to have experience printing ABS/ASA with an existing printer, along with the ability to solder and crimp wires for your toolheads. There are many ways to build a StealthChanger- the list below is just a suggestion. 

### The "default" hardware is the following
* [CNC Shuttle](../Shuttle.md)
* [Modular dock](../Docks.md)
* [Crossbar](../Docks.md) mounted outside front extrusions
* [Door Bufer](../Docks.md)
* [Anthead](../Toolheads/Anthead.md) Toolhead
* [FannyPack](../CableManagement/ElectricalDistribution.md) backpack
* [N3MI umbilicals](../CableManagement/Umbilicals.md)
* [SexBolt](../Probes.md)

### Upgrading existing printer
1. Decide on what you want to do! Then be prepared to change your mind halfway through, and re-print some stuff, take everything apart, and do it again.
2. Order a bunch of parts for the shuttle, toolheads, tophat, docks/crossbars, etc.  Wait a week or two while reading and doing more planning.
3. Upgrade to CAN or USB toolhead board for primary toolhead if you don't already have it. 
2. Install CAN or USB distribution board and "backpack"
3. Install umbilical cable to primary toolhead (T0)
4. Install CNC shuttle and backplate for your toolhead
5. Get printer working again to print other parts.
6. Print door buffer (done anytime)
7. Install top hat (done anytime)
8. Install Docks for your toolhead (getting harder)
9. Build 2nd + toolheads, install with umbilicals.
10. Install Klipper-toolchanger-easy (KTE)
11. Configure KTE
12. Calibrate offsets
13. Calibrate dock locations
14. Add Additional toolheads and docks