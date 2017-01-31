---
layout: post
title: UAV haptic control using Novint Falcon - pt 1
description: "In the first month of 1PPM I explore the idea of using Novint Falcon as a UAV controller"
modified: 2017-01-31
comments: true
tags: [Robotics, ROS, Pixhawk, UAVs, Mechatronics]
categories: [1ppm]
image:
  feature: jmavSim.png
---

As my first [1PPM]({{site.url}}/1ppm/12-Technical-Challanges/) project I choose to explore possibilities of using a Novint Falcon haptic device as a high level controller for an UAV. In this post I will describe the tools I chose to solve the problem. 

<figure class="half center">
  <img src="{{site.url}}/images/Novint_Falcon.jpg" alt="Novint Falcon Haptic Controller">
	<figcaption>Novint Falcon Haptic Device</figcaption>
</figure>

Tl;dr of things I learned while working on this project:

* Bit of ROS (Robot Operating System)
* Using _libnifalcon_ library to interface with the falcon
* Some random bits about Pixhawk (Px4 and ArduCopter Firmware)

<!-- more -->

# Novint Falcon

## Intro

I love the idea behind the Falcon. It is basically a parallel manipulator with 3 actuators that apply force feedback letting you 'feel' the objects shapes, surfaces or even viscosity! If you get a chance to play with one I highly recommend going through the demo files that come with the drivers. 

According to [Wikipedia](https://en.wikipedia.org/wiki/Novint_Technologies) Falcon was announced in 2007 and it seems they mainly envisioned this device for gamers. Sadly it seems that it didn't catch on, but who know, maybe it will come back given the growing market for VR hardware and software. As of writing this article(30.01.2017) [Novint website](http://www.novint.com/) is offline. Also some people at [reddit](https://www.reddit.com/r/oculus/comments/1wibk9/what_happened_to_the_novint_falcon/) say company had financial issues and it might not be recovering any time soon.

## libnifalcon

*libnifalcon* is an open source driver for the Novint Falcon. You can find its repo [here](https://github.com/libnifalcon/libnifalcon). 

I found the documentation of libnifalcon to be very good! I haven't found it anywhere online, so you will have to use doxygen to make it yourself. 

The library comes with some simple [examples](https://github.com/libnifalcon/libnifalcon/tree/master/examples). I highly recommend them before starting. 

Speaking of starting to develop with libnifalcon; there's an excellent tutorial on getting started with the library written by radarsat1 that you can find [here](https://github.com/radarsat1/dimple/blob/master/doc/novint_falcon_howto.md)

## Things learned while working with libnifalcon

### Could not load firmware issue

Just when I started with Falcon I run into some trouble with loading firmware on Linux. When I tried to launch some Falcon examples I would get 'Could not load firmware' error. The issue is described quite well on [github](https://github.com/libnifalcon/libnifalcon/issues/45). What seemed to work for me was running a _findfalcons_ example as root 3 times. Afterwards every other example that comes with the library worked for me.

### Coordinate system

By default Falcon has the following coordinate system:

* *X* - Left/Right 
* *Y* - Top/Down 
* *Z* - Forward/Backwards

From what I understood from working with Falcon for those couple of weeks you have to enter Homing mode to correct the origin of the grip. The recommendation is to home the system before enacting any torques calculated from positions. If you ever work with Falcon then please check the documentation so you have this part covered! Otherwise *violence happens* (and I'm quoting the documentation here)!

# UAV 

Before I go into some nitty-gritty details about Pixhawk let me quickly introduce some concepts relevant to multirotor side of the project. Let's start with control.

## UAV control

The three basic control modes for a UAV are:

* Acrobatic / Rates mode (control rate of rotation)
* Attitude mode (control angles)
* Position hold / Loiter mode (control groundspeed and climbrate)

Let's assume you are flying your multirotor with a transmitter. If you are in Acrobatic mode, you started some rotation and let go of the sticks the rotation aircraft will keep rotating (and you will end up in the snow).


<figure class="half center">
  <img src="{{site.url}}/images/quad_snow.jpg" alt="Quadrocopter full of snow">
	<figcaption>Sometimes flying in a snow seems like a great idea. Until it doesn't. </figcaption>
</figure>

If you fly in attitude mode you command directly an angle when moving your attitude related sticks. As soon as you let go the commanded angles will be 0 (if everything goes as planned). Note that this doesn't mean that the speed of the aircraft will also be 0!

Position hold (or Loiter) is the most attractive position for this project. In this mode you usually command the aircraft groundspeed (speed relative to the ground, usually derived from GPS position). 

The reason position/loiter mode is attractive is because we can tolerate (to some extend) non-real time behaviour of the system, i.e. if the command don't arrive in time for whatever reason the UAV will remain stable, which probably wouldn't happen in the two _lower modes_. 

# Pixhawk

Pixhawk is super fun. Normally I would prefer to stick with *Arducopter* however since my personal Pixhawk is currently about 1500 km away from me I decided to use Software In The Loop approach. In my opinion the SITL is much better documented for Px4 and because I want to move fast I decided to stick with it.

## SITL

For SITL I really like using *jmavsim* that comes with Px4 firmware. It's very easy to run and seems to play very nicely with *mavros*. The tests I run so far seem hopeful and I'm pretty sure next month I will end up with a working proof of concept in SITL mode (until I get my pixhawk).

## Offboard mode

In order to be able to control the autopilot from anything else than transmitter you have to enter [offboard mode](https://dev.px4.io/offboard-control.html). If you try this it's important that you set up your transmitter in such way that you can always regain manual control (or at least that's what I'm going to do at some point of this project!). 

If you intend to use offboard mode it's important that you stream your request faster than 2Hz, otherwise it won't work. In case you are using *mavros* you also need to make sure that your timestamps are correct.

# Summary

There is still lots to do for me to complete this project. I definitely learned a lot this month but there is much more to come. I will make sure that I'll post updates to the blog as I go and maybe write some tutorials if I find any tricky parts. 

## The master plan

The plan for now is to get the Falcon to work with a Px4 SITL ASAP. Afterwards I want to spend some time on Falcon actuation so it _bounces back_ as you move it around. Ideally if you let go it will come back to the origin until you move it again. Longer term I'm planning to modify my quadrocopter to incorporate Pixhawk on it, if needed attach a companion computer and then try flying using Falcon with real drone. I bet it will be super fun! 

Keep on flying!
