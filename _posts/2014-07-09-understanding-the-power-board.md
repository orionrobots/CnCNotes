---
title: Understanding the Power Board
layout: post
tags: [electronics, power-board, soldering]
---
![]({{ site.baseurl }}/inside__control_box/images/img_3027.jpg)
After the teardown and ordering the new parts for my board
I started by replacing the obviously damaged 7812.
I tried powering the board but the spindle did not move.
I sat on the problem for a while before truing to understand the board better.

This meant learning a whole bunch of stuff about analogue electronics, power circuits, 555s and op amps oh my!

So I spent a few weeks playing with the 555. watching eevblog tutorials on op amps and power supply design.
I got a simple led and 555 in stable mode going. figured out current sense and voltage regulators.

Then I looked at the board and it's schematic and stated seeing the blocks.

# The Parts

12v regulated supply

pwm from a 555

FET motor control

current sense.

# The Fix

There is far more to this story, and I will get the details down. In short - after probing, tracing and then making experimental versions of the blocks on the board, I determined that the 555 had been destroyed, but this was because the motor speed pot had gone, and shorted all tree parts without much resistance. It didn't always do it - but as you sweep it - every now and again the part would fail like this. This catastrophic failure caused far too much current through the motor, destroying the FET, and caused far too much current across the 555 taking it out, and once that fails it dead shorts the regulator so that blew. 
 
 So I bought replacement parts, and found a new pot. Unfortunately none were a fit for the front panel area, however, I found a hole on the rear panel which I have now used for the pot.
 
 I resoldered the other parts, and made it work again. There are photos and video to follow of the process. I now understand that power board fairly intimately, and have the schematics for it.
 
# Links

I have come across a number of sites with people spending time on this machine

<http://lab.whitequark.org/notes/2014-02-11/cnc3020t-fixing-power-supply/>
