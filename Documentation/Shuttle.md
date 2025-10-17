# Shuttle

1. [Shuttle Options](#shuttle-options)
2. [Assembling Shuttle and Backplates](#assembling-shuttle-and-backplates)
3. [Installing Shuttle](#installing-shuttle)
4. [Backplate Preload](#preload)
5. [Tips and Tricks](#tips-and-tricks)

This is the part that goes on your X carriage to mate and pickup each tool. It will mate with a BACKPLATE that's made specifically for your toolhead. <br>

## Shuttle Options
<table>
<tr><td valign="top">
		<img src="/media/Shuttle/Fystec_CNC_Shuttle.jpg" width=200></td>
	<td valign="top">
			<a href="https://www.fysetc.com/products/fysetc-stealthchanger-cnc-shuttle-kit-sb-combo-v2-board-tool-distribution-board-h36-board?variant=44927105040559">Fystec CNC Shuttle</a><br>
		<ul>
			<li>It comes with pins, N52 magnets, and screws for 6 backplates also!</li>
			<li>No instructions are included, so you need to use the printed shuttle build instructions</li>
		</ul></td></tr>
	
<tr><td valign="top">
		<img src="/media/Shuttle/LDO_CNC_shuttle.jpg" width=200></td>
	<td valign="top">
			<a href="https://kb-3d.com/store/voron/6008-ldo-motors-stealth-changer-cnc-shuttle-kit-6975415159350.html">LDO Kit CNC Shuttle</a><br>
		<ul>
			<li>Not sure what comes with this kit; shuttle seems similar to the Fystec</li>
		</ul></td></tr>
<tr><td valign="top">
		<img src="/media/Shuttle/printed_backplate_v1.1.jpg" width=200></td><td valign="top">
			<a href="https://github.com/DraftShift/StealthChanger?tab=readme-ov-file">Print your own</a><br>
			<ul><li>These are thicker so you loose a bit more Y in print volume, and they are less rigid than CNC shuttles</li>
		</ul>
		<b>Bill of materials</b>
		<ul>
		<li>[3] 6x3mm magnets (N52 Highly recommended to counter the pull from the umbilicals)</li>
		<li>[4] m3x6 BHCS head (mgn bolts) m3x12 if used with the shuttle keeper</li>
		<li>[3] 4x6x6mm brass bushing (4mm id x 6mm od x 6mm tall)</li>
		<li>[2] m3x40 SHCS (Optional: to stiffen the shuttle, Fully threaded, no shoulder)</li>
		</ul>
</td></tr>
</table>


**NOTE: D2HW shuttle is not compatible with Hall Effects, and D2HW back plate will affect cooling.**

## Assembling Shuttle and Backplates
In order to get proper matching set you should:
- insert pins in your best backplate (straightest)
- press bushings in the shuttle and ensure a smooth mating between the parts.
- inset 2x M3x8mm SHCS screws in the top 2 pins to secure, and a M3x6 or 8mm BHCS screw in the bottom pin. The StealthBurner back plate needs the pins glued so this is done as the last step
- if everything feels smooth, so pop the bushings out and glue them in place using either superglue or epoxy, other wise see [Heat Treating](#heat-treating)
- be sure to test that the mating still feels smooth after the glue sets.
- You can now use the shuttle as a "master blank" for glueing the pins into all your backplates.

**NOTE: Currently pins may feel very loose, this is by design to allow for room for glue or epoxy (recommended) to set.  Normally press fit is good enough for testined, but for actual use make sure to secure the pins properly.**
  
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


