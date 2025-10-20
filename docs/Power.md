---
title: Power considerations
nav_order: 1
parent: Home
---


More toolheads active at the same time means you will need more baseload power required. A 200W 24V PSU might not suffice if all of your toolheads are heating up at the same time, 

Calculate the maximum power by tallying up all your heater wattages, add some margin for the motors and other things that are powered by 24V and use that as a reference number to select your PSU.

Common options are the Meanwell LRS-24-350 for 350w, LRS-24-450 for 450w and LRS-24-600 for 600W. Make sure you have enough room in your electronics bay because they are not all the same size.
Note that unlike the 200W version the 450 and 600W are actively cooled with an annoyingly loud fan that will kick in when its temperature gets too hot so good electronic bay ventilation is recommended.

Other options are UHP variants with a smaller form factor (//TODO), often using 2 low wattages PSUs combined. Make sure if you use multiple PSUs that you tie the GND of each one together to have a common reference point otherwise communications issues will arise 

// TODO

