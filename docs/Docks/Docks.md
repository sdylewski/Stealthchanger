---
title: Docks
nav_order: 3
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
# Docks


## Crossbar, dock, and door buffer
A crossbar is recommended for stability, but there are options for how to mount it, and then that enables/disables other things.  You need to pick one of these options below.
<br>Essential information: <a href="https://github.com/DraftShift/ModularDock">Draftshift Modular Dock</a>
<br>Draftshift <a href="https://github.com/DraftShift/ModularDock/blob/main/Manual/ModularDock_Assembly_Guide.pdf">modular dock assembly guide.</a>
<table>
<tr><th>Crossbar options</th><th>Details</th></tr>
<tr><td>No crossbar / Top mount<br>
		<img src="media/Dock/Dock_top_mount.png" width=200></td><td>
			<ul><li>Least sturdy option</li>
			<li>Requires several printed braces & links to help stabilize the docks</li>
			<li>No need for <a href="https://github.com/DraftShift/DoorBuffer">door buffer</a>?</li>
		</ul></td></tr>
	<tr><td>Crossbar mounted outside front extrusions<br>
		<img src="media/Dock/LDO_Dock.png" width=200></td><td>
			<ul><li>Probably the most common setup</li>
				<li>Strongest setup (least dock movement potential)</li>
			<li>Requires a <a href="https://github.com/DraftShift/DoorBuffer">door buffer</a> so your door will still have something flat on the front of the printer</li>
			<li>This option is what comes with the LDO kit</li>
		</ul></td></tr>
	<tr><td>Crossbar mounted <em>between</em> front extrusions<br>
		<img src="media/Dock/Dock_crabby.png" width=200></td><td>
			<ul><li>No need for <a href="https://github.com/DraftShift/DoorBuffer">door buffer</a></li>
         <li>Needs tight bolts to keep from rotating</li>
         <li>An other tips from people who've done this?</li>
         <li>For existing builds with 2020 sides, front idlers will hit the crossbar, so you need to change idlers to use the <a href="https://github.com/DraftShift/StealthChanger/tree/main/UserMods/BT123/MiniBFI%20%2B%20MicroBFI">MiniBFI</a>.</li>
			<li>20mm less Y build space unless you use shorter "stubby" docks.  Even with stubby docks, the Y build space is 10mm less than the outside-mounted crossbar?</li>
         <li>Another option for new builds is to use 2040 front extrusions, and a 2020 crossbar this way.</li>
			<li>Image from @drakarah and <a href="https://www.printables.com/model/994635-stealthchanger-stealthburner-minimal-docks-aka-hap/comments">Happy Crab Docks</a></li>
		</ul></td></tr>
   
</table>

## Modular Dock

The team has created their own dock as a solution. It allows for mounting from both the top bar, as well as a crossbar (or both). While its currently still in testing, its an option if you can do some work without having a full readme. You can view it here: [DraftShift Modular Dock](https://github.com/DraftShift/ModularDock)

Currently all docks used with [Viesturz's Tapchanger](https://github.com/viesturz/tapchanger) are compatible.

To calculate how many tools you can fit on the front of your printer you ened to know the tools to use first and the amount of room for your front idlers (stock gantry also can't move the entire length of X so make sure you factor that in as well.

   - Dragon Burners/Yavoth require 60mm per tool (I recommend 5mm between for extruder handles)
   - Blackbird, Stealth Burners and XOL require 76mm per tool
   - The gantry required about 20mm per side to be able to pass the tools.  To know how many tools you can fit it's simple math, measure that top bar -40mm to gantry and then divide the remainder by the size of your toolhead.

Once you have this add it all up and subtracked the length of your front extrusion.

Example: Voron 350 is 470mm total, 5 stealthburners is 76 x 5 = 380 -> 380 + 40 - 470 = 50, so that means you can fit 5 Stealthburners and have 50mm to spare which is not enoguh for any other tools.
