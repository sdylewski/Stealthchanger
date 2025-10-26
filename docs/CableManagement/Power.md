---
title: Power Supply
nav_order: 5
parent: Electronics & Cable Management
---
<!-- Use the page layout at TOC.md:  https://github.com/sdylewski/StealthChanger/blob/main/docs/TOC.md -->

# Power
More toolheads active at the same time means you will need more baseload power required. A 200W 24V PSU might not suffice if all of your toolheads are heating up at the same time, 

Calculate the maximum power by tallying up all your heater wattages, add some margin for the motors and other things that are powered by 24V and use that as a reference number to select your PSU.

But this is only if all the toolheads are on at the same time and at maximum power.  If you can turn each toolhead on and wait until it reaches the set temperature before moving to the next one, your maximum power requirements will be much less.

### Example
For 24V power, and Power = I * V

| Toolhead Power| Current | x 2 | x 4 | x 6 |
| --- | --- | --- | --- | --- |
| 70W | 70W/24V=2.9A |  6.8A | 11.6A | 17.4A |

## Power supplies

Common options are the Meanwell LRS-24-350 for 350w, LRS-24-450 for 450w and LRS-24-600 for 600W. Make sure you have enough room in your electronics bay because they are not all the same size.
Note that unlike the 200W version the 450 and 600W are actively cooled with an annoyingly loud fan that will kick in when its temperature gets too hot so good electronic bay ventilation is recommended.

Other options are UHP variants with a smaller form factor (//TODO), often using 2 low wattages PSUs combined. Make sure if you use multiple PSUs that you tie the GND of each one together to have a common reference point otherwise communications issues will arise 

// TODO: power management mitigation in SW so all heaters aren't on at the same time (add link to code or slicer settings?)


