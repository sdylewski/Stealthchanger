# <img src="media/Logos/Stealthchanger_logo.png" style="height:50px;vertical-align:text-top" /> StealthChanger

<b>Tool changing system for Vorons and other front mount printer motion systems.</b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
 <a href="https://discord.gg/draftshift" target="_blank" alt="Join our Discord">![Discord](https://img.shields.io/discord/1226846451028725821?logo=discord&logoColor=%23ffffff&label=Join%20our%20Discord&labelColor=%237785cc&color=%23adf5ff)</a>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://github.com/sponsors/DraftShift" target="_blank" alt="Sponsor Us">![GitHub Sponsors](https://img.shields.io/github/sponsors/DraftShift?logo=githubsponsors&label=Sponsors&labelColor=rgb(246%2C%20248%2C%20250)&color=rgb(191%2C%2057%2C%20137))</a>


## Stealthchanger Overview
StealthChanger is a project to convert a Voron 2.4 printer into one with multiple toolheads.

Mounting of the toolhead to the shuttle is done by using bushings and pins, with magnets to help create a strong mounting connection for high-speed printing, and uses the same principles as [TAP](https://github.com/VoronDesign/Voron-Tap) to measure Z offsets.

StealthChanger draws from many different projects including [tapchanger](https://github.com/viesturz/tapchanger), and involves the contributions of many people who work together to make it better. 

## Stealthchanger Components
The stealthchanger system consists of multiple parts. Some are essential, some have many different options, and some are optional. 

<table>
 <tr><td valign="top" width="50%"><h3><a href="Shuttle.md">Shuttle</a> & <a href="Toolheads.md">Backplates</a></h3>
The shuttle replaces your Voron shuttle with one that has bushings to connect to the backplate of each toolhead
</td><td valign="top" width="50%">
<img src="media/Shuttle/shuttle.jpg" width="200">
</td></tr>
 
<tr><td valign="top" width="50%"><h3><a href="Docks.md">Modular Dock</a></h3>
This mounts to the top front of your printer to hold/dock the toolheads when not in use. May also contain a crossbar at the bottom of the dock. Some docks just use the crossbar. <br>
<ul>
<li><a href="Docks.md">Modular Dock</a></li>
<li><a href="Crossbar.md">Crossbar [optional]</a></li>
<li><a href="DoorBuffer.md">Door buffer [optional]. Needed if mounting crossbar to front of frame.</li>
</td><td valign="top" width="50%">
<img src="media/Dock/dock_front.png" width="400">
</td></tr>

<tr><td valign="top" width="50%"><h3><a href="CableManagement.md">Cable Management</a></h3>
Power and data needs to be distributed from your main board to each toolhead, along with your filament.  
<ul>
<li><a href="FannyPack.md">Fanny Pack</a> mounts a CAN or USB distribution board on the back of the printer</li>
<li><a href="Umbilicals.md">Umbilicals</a> and exhaust plates</li>
<li><a href="FilamentManagement.md">Filament management</a></li>
</ul>
</td><td valign="top" width="50%">
<img src="media/CableManagement/wire_management.jpg" width="180">
</td></tr>

<tr><td valign="top" width="50%"><h3><a href="TopHat.md">Top Hat</a></h3>
With the dock at the top of the printer and umbilicals extending upward, enclosed printers will want to extend the top of the printer using a top hat.  
</td><td valign="top" width="50%">
<img src="media/TopHat/printed_tophat.png" width="180">
</td></tr>

<tr><td valign="top" width="50%"><h3><a href="Probes.md">Probes</a></h3>
Physical probes are used to measure the X and Y offsets of your tools relative to Tool 0. Endstop switches are included here also
<ul>
<li><a href="Probes.md">Probes</a> for determing offsets</li>
<li><a href="Endstops.md">Endstops</a> for X and Y gantry endstops</li>
</ul>
</td><td valign="top" width="50%">
<img src="media/Probes/sexball-probe.jpg" width="180">
</td></tr>

<tr><td valign="top" width="50%"><h3><a href="Software.md">Klipper Toolchanger</a></h3>
Klipper needs to be toolchanger aware with added code.
<ul>
<li><a href="Software.md">Klipper Toolchanger</a></li>
</ul>
</td><td valign="top" width="50%">
<img src="media/Logos/klipper_toolchanger_logo.png" width="180">
</td></tr>

</table>

<em>Ready to get started?</em>

## Next --> [Planning](Planning.md)




