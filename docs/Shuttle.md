---
title: Shuttle
nav_order: 1
parent: StealthChanger Components
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->
# Shuttle

This is the part that goes on your X carriage to mate and pickup each tool. It will mate with a BACKPLATE that's made specifically for your toolhead. All shuttles have a vertical flag at the top that interacts with an OptoTap sensor mounted on the backplate to detect the tool and register taps on the build plate<br>

## Shuttle Options
<table>
<tr>
	<td valign="top"> 
	<h3><a href="https://www.fysetc.com/products/fysetc-stealthchanger-cnc-shuttle-kit-sb-combo-v2-board-tool-distribution-board-h36-board?variant=44927105040559">Fystec CNC Shuttle</a></h3><br>
	<ul>
		<li>It comes with pins, N52 magnets, and screws for 6 backplates also!</li>
		<li>No instructions are included, so you need to use the printed shuttle build instructions</li>
	</ul></td>
	<td valign="top">
	<img src="media/Shuttle/Fystec_CNC_Shuttle.jpg" width=200>
	</td></tr>
	 
<tr>
	<td valign="top">
	<h3><a href="https://kb-3d.com/store/voron/6008-ldo-motors-stealth-changer-cnc-shuttle-kit-6975415159350.html">LDO Kit CNC Shuttle</a></h3><br>
	<ul>
	<li>Not sure what comes with this kit; shuttle seems similar to the Fystec</li>
	</ul></td>
	<td valign="top">
	<img src="media/Shuttle/LDO_CNC_shuttle.jpg" width=200>
	</td></tr>
		
<tr>
	<td valign="top" width="50%">
	<h3><a href="https://github.com/DraftShift/StealthChanger?tab=readme-ov-file">Print your own</a></h3><br>
	<ul><li>These are thicker so you loose a bit more Y in print volume, and they are less rigid than CNC shuttles</li>
	</ul>
  	<h3>Bill of materials</h3>
  	<ul>
		<li>[3] 6×3 mm magnets (N52 recommended)</li>
		<li>[4] M3×6 BHCS (MGN bolts), M3×12 if using shuttle keeper</li>
		<li>[3] 4×6×6 mm brass bushing</li>
 		<li>[2] M3×40 SHCS (optional, fully threaded)</li>
 	 </ul>
	</td>
	<td valign="top">
	<img src="media/Shuttle/printed_backplate_v1.1.jpg" width=200>
	</td></tr>
<tr><td valign="top">
	<h3>Printing shuttle</h3>
	<ul>
    	<li>See <a href="Printing.md">Printing</a> before printing the shuttle</li>
    	<li>Shuttle orientation is flat on the back with supports enabled</li>
  	</ul>
	</td><td valign="top">
	<img src="media/Print_orientation.jpg" width="320" alt="Print Orientation">
	</td></tr>
</table>

## Assembling Shuttle and Backplates
In order to get proper matching set you should:
- insert pins in your best backplate (straightest)
- press bushings in the shuttle and ensure a smooth mating between the parts.
- inset 2x M3x8mm SHCS screws in the top 2 pins to secure, and a M3x6 or 8mm BHCS screw in the bottom pin. If needed, you can glue in the pins.
- if everything feels smooth, pop the bushings out and glue them in place using either superglue or epoxy
- see [Heat Treating](#heat-treating) for fine-tuning the fit after gluing.
- be sure to test that the mating still feels smooth after the glue sets.
- You can now use the shuttle as a "master blank" for glueing the pins into all your backplates.

**NOTE: Currently pins may feel very loose, this is by design to allow for room for glue or epoxy (recommended) to set.  Normally press fit is good enough for testing, but for actual use make sure to secure the pins properly.**
  
## Installing Shuttle
Print <a href="https://github.com/DraftShift/StealthChanger/tree/main/STLs/Extras/BeltHelper">BeltHelper</a> to help make this easier!<br>
See the excellent Draftshift <a href="https://github.com/DraftShift/StealthChanger/blob/main/Manual/Stealthchanger_Assembly_Guide.pdf">assembly guide</a> for installation instructions.

## Backplate Preload
(move this to backplate section?)
Every backplate needs to be adjusted. Preload is meant remove all the wiggle when it's fully seated by preloading the pins onto the bushings. To set your preload you want to back the FSCS screws till they are just touching the magnest on the shuttle. 

You can use a piece of paper per side to make sure they both have the same pressure.
Big thank you to `ButtSlark` on Discord for this technique.


## Tips and Tricks

### Heat Treating
If you printed the shuttle and backplate and things are just not smooth or you have slight binding, you can Heat Treat it and here is how.
- Fully assemble the shuttle and backplate with Bushing, Pins, Screws and Magnets
- Set your heat bed to 100-110°C
- Once at temperature, mate both parts fully, and set them on the bed with the backplate (tool side) down
- After 20+ minutes pick them up and slide them 3-4 times, then fully mate them once again
- With both parts still fully mated, set them down with the backplate (tool side) down someplace flat and at room temperature and let them fully cool without touching them for 5+ hours
- Try and slide them again and you should feel an improvement, you can try this multiple times if you are still not satisfied

Big thank you to `unguided-wanderer` on Discord for this technique.


### Cleaning out bushings
Sometimes the bushings aren't debured or do not slide well when you recieve them.

- Find a drill bit 4mm or smaller (I’m using 3mm in the video at the link)
- Using your thumb, apply pressure onto the bush and roll back and forth on the drill bit. 
- Test on the pin again
- Rinse and repeat.
- Some bushings take multiple tries, but try not to over do it, just enough that the bushing falls on the pin.
- Big thank you to `BT123` on Discord for this technique.
  
[![Bushing Cleaning](https://img.youtube.com/vi/AHlydBsMJro/0.jpg)](https://www.youtube.com/watch?v=AHlydBsMJro)

## Mods

* [Split keeper for 9mm belts/monolith](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/BT123/Split%20Keeper)
* [Belt helper 3mm spacing for Micron/V0](https://github.com/DraftShift/StealthChanger/tree/main/UserMods/N3MI-DG/Belt_Helper_3mm)
* [Shuttle with 5.5mm OD bushings](https://github.com/DraftShift/StealthChanger/blob/main/UserMods/traxman25/Bushings_5.5/README.md)
  
