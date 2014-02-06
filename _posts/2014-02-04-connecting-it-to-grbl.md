---
title: Connecting my CnC 3020 to grbl
description: Connecting my CnC 3020 to grbl
tags: [arduino, grbl, electronics, parallel port]
layout: default
---

# Connections

The Machine came with little more than a single sheet and a CD full of Chinese versions of Mach3 and drivers for that. See [Unboxing and setup]({% post_url 2014-02-03-unboxing-and-setup %}) for what else was in the device. The eBay auction also had a link to a MS Word document, which importantly had some of the pin connections so mach3 could be configured. I could cross ref this with the [grbl connections](http://github.com/grbl/grbl/wiki/Connecting-Grbl) to create a wiring plan for attaching it to my machine.

I flashed grbl onto an Arduino Uno R3 compatible board, using the hex file and the recommended windows file to upload this. I was able to use putty to talk to grbl and get responses from it. 

I wired this into the parallel connector at the back of the control box, and started up the machine.
Grbl resets when the machine is powered on - however, putty is still connected - this may mean some power related fluctation - I had also connected the Arduino to what I think was a ground on that port too - for the signals to make sense - they needed a common ground.

<table>
<tr><th>Arduino Pin</th><th>Parallel port CnC Pin</th></tr>
<tr><td>A0</td><td>Stop/Emergency reset 10</td></tr>
<tr><td>2</td><td>Step Pulse X 2</td></tr>
<tr><td>3</td><td>Step Pulse Y 4</td></tr>
<tr><td>4</td><td>Step Pulse Z 6</td></tr>
<tr><td>5</td><td>Step Dir X 3</td></tr>
<tr><td>6</td><td>Step Dir Y 5</td></tr>
<tr><td>7</td><td>Step Dir Z 7</td></tr>
<tr><td>Ground</td><td>Ground 18-25</td></tr>
</table>

I then proceeded to check the grbl settings - and was able to leave them at the defaults - they looked close to the mach3 settings in the screenshots from the manual.

I then issued my first attempt at a gCode command ```G00 X 50``` which I think should make the X axis move from where it is now (an assumed zero/home point).
 
Nothing happened on the router - it stayed motionless. I knew from unboxing it that the stepper controllers were talking to the steppers, and I had been able to power up the spindle. I was able to use the ```?``` command in grbl to see that it was trying to move.

I've am both awaiting a tiny mini-itx based pc to try with, and going to teardown/diagnose the controller to understand what is in it - and see what I may be doing wrong.

Thoughts - the reset may mean I had the wrong pin as ground - not a ground. Perhaps I have managed to offset or reverse stuff?
