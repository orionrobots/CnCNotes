---
title: Using Heeks CAD to Mill an STL file
layout: post
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

Save at this point.

## Step 3 - Stock



Not complete...


