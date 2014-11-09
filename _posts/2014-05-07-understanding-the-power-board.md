---
title: Understanding the Power Board
layout: post
tags: [electronics, power-board, soldering]
---
![]({{ site.baseurl }}/inside__control_box/images/img_3027.jpg)

# The Fix

There is far more to this story, and I will get the details down. In short - after probing, tracing and then making experimental versions of the blocks on the board, I determined that the 555 had been destroyed, but this was because the motor speed pot had gone, and shorted all tree parts without much resistance. It didn't always do it - but as you sweep it - every now and again the part would fail like this. This catastrophic failure caused far too much current through the motor, destroying the FET, and caused far too much current across the 555 taking it out, and once that fails it dead shorts the regulator so that blew. 
 
 So I bought replacement parts, and found a new pot. Unfortunately none were a fit for the front panel area, however, I found a hole on the rear panel which I have now used for the pot.
 
 I resoldered the other parts, and made it work again. There are photos and video to follow of the process. I now understand that power board fairly intimately, and have the schematics for it.
 
# Links

I have come across a number of sites with people spending time on this machine

<http://lab.whitequark.org/notes/2014-02-11/cnc3020t-fixing-power-supply/>

<h1>Comments</h1>
{% include comments.html %}
