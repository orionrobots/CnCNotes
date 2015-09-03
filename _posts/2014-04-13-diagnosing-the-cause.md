---
layout: post
title: Diagnosing the Cause of the blown components
tags: [electronics, control board]
---
After some investigation, it turned out that more than the FET was blown - the 7812 was gone, along with the fuses. So I had to determine how this happened. 
{% capture gallery %}{{ site.baseurl}}/galleries/2014-04-13-diagnosing-the-cause{% endcapture %}
![The whole control board]({{ gallery }}/the_whole_control_board.jpg)

First was to gain a better understanding of the 555 timer based PWM circuit driving the FET. Going back to [the teardown]({{ site.baseurl }}/2014/02/05/teardown.html), there are two boards. The one above is the stepper control and computer interface board. This was not affected.
 
The board below, with the big green screw terminals is the power and spindle control board. The problems are all on this board, and I will be talking about it for the rest of the write up.

After removing this board, I got a series of photos of the underside of the board - since it appears to be a one sided board, this will allow me to trace it in more detail.

![Underside of board]({{ gallery }}/20140209_152209_4.jpg)

After my previous teardown, I found a few people had traced out fairly similar circuits for the board already so I can then cross reference this, taking into account that it may be slightly different.
 
![Sketchy Trace Of The Board]({{gallery }}/YOC-PW3024-E-Diagram.jpg}

Refreshing the damage - parts had been blown through, a FET, and a 7812. The damage was severe enough to leave a great big crack in one of the devices cases - something had pulled a large amount of current through it.

![Damaged Device]({{gallery}}/20140209_152239_1.jpg)

The 7812 was the part with the most damage.

![The 7812 Id'd]({{gallery}}/20140209_152321.jpg)

After the teardown and ordering the new parts for my board
I started by replacing the obviously damaged 7812.
I tried powering the board but the spindle did not move.
I sat on the problem for a while before truing to understand the board better.

At this point - I also bought a few tubes of spares - 7812's, 555's, replacement fuses, replacement FET's. This way - I was ready to handle anything. 

This meant learning a whole bunch of stuff about analogue electronics, power circuits, 555s and op amps oh my!

So I spent a few weeks playing with the 555. watching eevblog tutorials on op amps and power supply design.
I got a simple led and 555 in stable mode going. figured out current sense and voltage regulators.

Then I looked at the board and it's schematic and started seeing the blocks.

# The Parts

12v regulated supply

pwm from a 555

FET motor control

High voltage/high current supply for the motor

current sense.

# Probing and tracing

Now I'd got some parts, and some background, I decided to start by debugging it with a scope and a small rig. I used 4xAA batteries, 6v as a supply - and clipped it onto the board - a ground, and the +ve rail for the low voltage side, where the 7812 output would be.

![]({{gallery}}/IMG_3402.JPG) 

![]({{gallery}}/IMG_3403.JPG)

I then plugged in the pwm pot, and hooked up my scope probes to it.  What I first saw is this: 

![]({{gallery}}/IMG_3407.JPG)

Its worth explaining this flat line. This would have pulled all the current through the 7812, kept the FET turned on, and spun the spindle as fast as it would go. Not good - it would have blown itself again immediately.

The 555 for pwm was charging through one diode and discharging through another - each via the potentiometer - the large spindle speed dial. The proportion of one side to the other should exactly control the PWM duty cycle.
 
If I nudged the pot - I could get the PWM traces - but they were wrong:
 
![]({{gallery}}/IMG_3404.JPG)
![]({{gallery}}/IMG_3405.JPG)
 
I have to hold like the image below to get a regular trace:

![]({{gallery}}/IMG_3406.JPG)

I took a video of this part of the diagnosis:

<iframe width="560" height="315" src="//www.youtube.com/embed/5dG0UPwRt30" frameborder="0" allowfullscreen="true"></iframe>

My next task is to find a suitable pot - or a place to mount it.

 
# Links

I have come across a number of sites with people spending time on this machine

<http://lab.whitequark.org/notes/2014-02-11/cnc3020t-fixing-power-supply/>

<h1>Comments</h1>
{% include comments.html %}
