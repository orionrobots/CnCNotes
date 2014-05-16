---
title: Using Heeks CAD to Mill an STL file
layout: default
tags: [software, heeks, toolpath]
---
After playing with a few different types of CAM software, I settled on [Heeks CNC](https://sites.google.com/site/heekscad/).
Heeks CNC is open source and free, although Windows users are asked to pay £10 for the binaries. 
This is a modest sum - so I've no trouble paying that.

Heeks is a very capable bit of software. It has a simple CAD system, and a very functional CnC system. While I prefer using Creo or SketchUp for the design, this works for actually turning that into a millable object. I started looking first at PyCAM in my previous post, and discovered that PyCAM is one of the components that HeeksCNC is built with. 

Since the documentation for it is a little lacking IMHO - here is a tutorial on how I got a 3D part out of heeks.

# Tutorial

## The short version 

You will need to create 2 pocket machining jobs from heeks - one as a roughing pass, and one as a finishing pass. You will need your 3d object, some tabs, a stock and a sketch. Create a surface from the 3d object and tabs, create a stock from a stock cuboid. Make a simple rectangle sketch on the stock. Make a rough pocket operation to take out material layer by layer, and a finishing pocket operation to go over the job smoothly.

## Step 1 - Real world preparation and measuring

You will need to prepare and have measure the stock you will be milling. Stock - the block of wood, plastic or metal you will use. Make sure you know the depth, and to state the obvious - make sure your 3d design will fit in it. 

Ensure you have a spoil board under the stock if your operation will mill the final object right out, and that you have the whole setup very well clamped down. I have ruined jobs by having them move under the mill in the late stages/last few layers of milling! A very time-expensive mistake.

Make sure you know the end mill (the tool you clamp into the spindle of your CNC machine) - you need to know its diameter, and the operational length (or stick-out I think is the correct terminology). If the stock is deeper than this - it is not going to work. 

Make sure you know the routers operating limits - and have experimented with long empty rapids so you have the 
acceleration and rapid feed rates correct - if they are too high, you will have steppers that beep and fail to go anywhere - which will ruin your job. 

You will also need to have some idea of the feed rate - the speed at which you can cut through the material, given the RPM of your Cnc spindle, the type of endmill and the material itself. If it is too high - you risk damaging the tool and snapping it off, if it is too low, you risk burning material or heating the tool. There is a relatively wide sweet spot, and you want to err to the higher end of this for the optimal setting.

Now turn the router off - there are a number of software things to prepare before you get going.

## Step 2 - Importing the 3D files

Import your CAD items into Heeks. I used an STL file for this. If it was done in heeks, or is multiple objects, I suggest grouping them here to make them easier to manipulate. 

Ensure that they are at the right scale, and that they are not distant from the zero point (0,0,0). You will want it *below* this point, and make sure that the top is facing up (Z-positive).

You will want to add tabs - so when the object is milled out of the stock, it still has a couple of small attachments and does fly off or into the mill and get gouged. I need to experiment with it - but I chose 1mm deep tabs, with a width of 10mm - around the object. Small enough to be able to manually take out, but not so flimsy they accidentally detach.

From the machining menu, select "other operations->Surface", and pick your object plus the tabs. Create the surface.

Save at this point.

## Step 3 - Stock

For stock, I suggest creating a cuboid that is the same depth as your stock. In terms of X/Y size - make it at least larger than the 3d file, potentially you could make it the size of your whole stock sheet, but it need not be. Make it at least large enough to visualise the cut out, and to see if the path would result in any collisions or gouges.

Position the stock so the point where you want to start milling from (where you will 0 the mill), will be at 0,0,0 in heeks. Make sure that the stock is BELOW this point - in the negative Z direction, but the top of the stock is Z=0. In my opinion, the stock should be milled in the positive X and Y direction from 0.

Using the properties panel on the left, set the stock opacity to 30% so you can place the 3D object in the stock.


Position the 3D object and the tabs so they are at the bottom of the stock - and to the right and forward of it. Make sure to leave some material clearance to cut the 3d object clear out of the stock.

Create a sketch on the stock - a simple rectangle on the XY plane at Z=0, which covers the top of the object you are going to mill, and the clearance too. This will be the pocketing sketch.

From machining menu, choose "other operations->stock", and choose the stock cuboid.

You may want to set the stock visibility to off here. If you wish to see its bounds - select the object from the structure panel on the left.

Save again here.

## Step 4 - Endmill and first pocket

Use the machining menu to add your endmill with the correct parameters that you took above.
You can right click to save the tools selection as a default for further projects - and you will be able to skip this step in later projects.

When you are milling out a chunk of material, including the material around an objcet you are cutting out stock, this is a pocket operation. 

For reasons of speed, and precision, it is common when machining to have multiple passes. The first is a "roughing" pass - the intention of which is take off as much stock material as possibel around your object, but leaving some for refining later. This is then followed by a "finishing" pass - a pass made with much finer sweeps, that is much slower, but will only need to take off a small amount of material. Machining the whole part in finishing would take a very long time - hence a roughing step.

From the machining menu, choose "operations->add pocket operation". Set the stepover to around half the mill diameter. Step the stepdown to 1 mm - you may be able to use larger, I am yet to experiment with this. 
There is a start depth - set to 0, and an end depth - set to the bottom of the stock (a negative Z value - in my case it was -20) if you will mill the part out entirely. Now choose the surface you created earlier, and the sketch you made on the stock. Choose the endmill. 

Set the other parameters to your choosing, and ok this. You now have the roughing pocket - yuou may want to use the properties dialog to name it as that.

Save your work.

## Step 5 - Finishing Pocket

Again, use Add pocketing operation, but now set the stepover to a smaller value - like 0.25mm, and stepdown to 1mm. 
Set the start and end depth to the bottom of your stock. It will then only 1 pass.

Choose the same surface and sketch. I have considered making a smaller sketch to exclude as much of the tab material as possible - but I've not experimented with that.

Ok this, and you will have a second operation in your structure.

Use the properties to set your machien details in the program object, and save.
You are now ready to start generating toolpaths.

## Step 6 - Generating toolpaths

First - from machining, select "G0" - to start creating the toolpath program. It will make Python Code (PyCAM I think), that contains a higher level description of the CnC operations.

wait for this to complete, and then use the Machining->"G0 to NC Post" option. This will postprocess the python (by running it with pyCAm and other libraries) into the GCode for your machine. If you have the output window visible - you will see the GCode, and when this is complete, you will also see the toolpath lines.

I had to turn off the visibility of these - as it seemed to slow down my laptop rendering.

## Step 7 - Preview

This is a CRUCIAL step before milling. I am not hugely experienced but I'd still expect those who are to try the preview/simulation before going on a real machine.

Select the preview/simulate option from the machining menu. Once in there, maximize the preview window, and use the mouse wheel to zoom out to see the whole stock. 

The press the "Play" button. You can use the slider to increase the speed. 
If you see any red marks, your mill has *gouged* your job, and things may be about to go wrong. As you watch - you will see how the material is coming out of it, and if the mill is doing anything alarming or inefficiently. If things are wrong - you may have to go back and alter the parameters for the operations above to get this right. Do not send it to the actual router until you are happy with this.

Save your work

## Step 8 - Go

At this point, you can use the menu "Machining - save NC" to save out the GCode for your machine. Awesome!



I will later add images and video to make this tutorial a bit more visual.
