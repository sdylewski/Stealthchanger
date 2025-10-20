---
title: Toolheads
nav_order: 2
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
# Toolheads

Many of the most common toolheads are supported.  You may build a dock for your existing toolhead, and then built new toolheads as other types. You can mix and match, but the configs get more complicated because you need to have different ones for each toolhead. 

Note that toolheads go hand-in-hand with their associated docks, and the options/mods available for them. 

## Selecting a new toolhead?
### Extruders
* [Awesome-Extruders](https://github.com/SartorialGrunt0/Awesome-Toolheads?tab=readme-ov-file)
[Extruder comparision](https://3dp-info.fyi/extruder-comparison)
### Toolheads
* [Awesome-Toolheads](https://github.com/SartorialGrunt0/Awesome-Toolheads?tab=readme-ov-file)
* [Toolhead comparison](https://3dp-info.fyi/toolhead-comparison)

Each toolhead page will contain specifics for the backplate, dock, and modifications for that toolhead.


<table>
<tr><th>Toolhead</th><th>Quick Summary</th></tr>
<tr><td valign=top><strong><a href="Anthead.md">AntHead<br>
	<img src="../media/Toolheads/Anthead.png" width=200></a></strong></td>
	<td valign=top><ul><li>Popular and modern.</li>
		<li>Uses 60mm wide docks</li>
    <li>Can use stubby docks?</li>
    <li>Default cowl and dock has built-in magnet holes for better docking</li>
	</ul></td></tr>
	
<tr>
	<td valign=top><strong><a href="A4T.md">A4T<br>
	<img src="../media/Toolheads/A4t.png" width=200></a></strong>
	</td>
	<td valign=top><ul><li>Slightly less supported with mods, but performance is supposed to be good.</li>
	<li>Requires Shorter Z joints like <a href="https://github.com/VoronDesign/VoronUsers/tree/main/printer_mods/hartk1213/Voron2.4_GE5C">Ge5C z-joints</a> so you don't bottom out your carriage when homing.</li>
		<li>Requires new smaller front idlers like the <a href="https://github.com/clee/VoronBFI">BFI</a> or <a href="https://github.com/DraftShift/StealthChanger/tree/main/UserMods/BT123/MiniBFI%20%2B%20MicroBFI">Mini BFI</a></li>
	</ul></td></tr>
	
<tr>
	<td valign=top><strong><a href="Dragonburner.md">Dragonburner & Rapidburner<br>
    <img src="../media/Toolheads/Dragonburner.png" width=200></a></strong>
	</td>
	<td valign=top><ul><li>Uses 60mm wide docks. Can use stubby docks. </li>
	<li><a href="https://github.com/bigtreetech/EBB/blob/master/EBB%20CAN%20V1.1%20and%20V1.2%20(STM32G0B1)/EBB36%20CAN%20V1.1%20and%20V1.2/Hardware/EBB36%20CAN%20V1.1%26V1.2-PIN.png">EBB36 CAN Toolhead Board</a>, using UserMod <a href="https://github.com/DraftShift/StealthChanger/tree/main/UserMods/TheSin-/PCB36_Mount">TheSin PCB36 Mount</a></li>
		<li><a href="https://www.printables.com/model/1440113-m3-heatset-standoffs-10mm-30mm">22mm standoffs</a> to mount the toolhead board to Orbiter 2 extruder</li>
		<li><a href="https://discord.com/channels/1226846451028725821/1320029517376655462/1347878802751230005">Magnetic dock</a> for Dragonburner, Discord only</li>
	<li><a href="https://github.com/DraftShift/StealthChanger/tree/main/UserMods/traxman25">Dragonburner numbered cowls</a> (not compatible with magnetic bases)</li>
	</ul>
  **NOTE: If you plan on using the Tapchanger Dragonburner dock you must use the [custom cowl by OstroMa](https://github.com/DraftShift/StealthChanger/blob/main/UserMods/OstroMa/DB_Cowl_v8_with_TapChanger_Dock_Hooks.stl). 
We always recommend to use the original cowls when possible and the [Modular Dock](https://github.com/DraftShift/ModularDock) does not require any special Cowl, print the original from the Dragonburner repo.**

  
  </td></tr>
	
<tr>
	<td valign=top><strong><a href="Stealthburner.md">Stealthburner<br>
    <img src="../media/Toolheads/Stealthburner.png" width=200></a></strong>
	</td>
	<td valign=top><ul>
	<li>76mm wide dock. </li>
	<li>Docking is a bit harder? </li>
	<li>Needs work on umbilical attachment for 3mm spring steel umbuilical from N3MI.</li>
		<li>Recommend the <a href="https://www.printables.com/model/1384948-stealthchanger-stealthburner-backplate-v11-magnet">screw-in backplate mod</a> for better 4mm pin positioning</li>
		<li>and magnetic backplate (same file above) for better control of stealthburner on dock.</li>
		<li><a href="https://www.printables.com/model/994635-stealthchanger-stealthburner-minimal-docks-aka-hap">Happy Crab Docks</a></li>
		<li><a href="https://www.printables.com/model/1358108-stealtchanger-stealthburner-backplate-with-screwed/comments">Screwed pins backplate</a></li>
		</ul></td></tr>
		
<tr>
	<td valign=top><strong><a href="SV08.md">SV08<br>
	<img src="../media/Toolheads/SV08.png" width=200></a></strong>
	</td>
	<td valign=top>
	<ul>
	<li></li>
	<li></li>
	</ul>
	</td></tr>
		
<tr>
	<td valign=top><strong><a href="XOL.md">XOL<br>
	<img src="../media/Toolheads/Xol.png" width=200></a></strong>
	</td>
	<td valign=top>
	<ul>
	<li></li>
	<li></li>
	</ul>
	</td></tr>
<tr>
	<td valign=top><strong><a href="Yavoth.md">Yavoth<br>
	<img src="../media/Toolheads/yavoth.png" width=200></a></strong>
	</td>
	<td valign=top>
	<ul>
	<li></li>
	<li></li>
	</ul>
	</td></tr>

</table>



