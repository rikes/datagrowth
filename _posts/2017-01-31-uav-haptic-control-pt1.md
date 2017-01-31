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

Speaking of starting to develop with libnifalcon; there's an excelent tutorial on getting started with the library written by radarsat1 that you can find [here](https://github.com/radarsat1/dimple/blob/master/doc/novint_falcon_howto.md)

## Things learned while working with libnifalcon

### Could not load firmware issue

Just when I started with Falcon I run into some trouble with loading firmware on Linux. When I tried to launch some Falcon examples I would get 'Could not load firmware' error. The issue is described quite well on [github](https://github.com/libnifalcon/libnifalcon/issues/45). What seemed to work for me was running a _findfalcons_ example as root 3 times. Afterwards every other example that comes with the library worked for me

### Coordinate system

By default Falcon has the following coordinate system:

* *X* - Left/Right 
* *Y* - Top/Down 
* *Z* - Forward/Backwards

From what I understood from working with Falcon for those couple of weeks you have to enter Homing mode to correct the origin of the grip. The recommendation is to home the system before enacting any torques calculated from positions. If you ever work with Falcon then please check the documentation so you have this part covered! Otherwise *violence happens* (and I'm quoting the documentation here)!

# Pixhawk

Pixhawk is super fun. Normally I would prefer to stick with *Arducopter* however since my personal Pixhawk is currently about 1500 km away from me I decided to use Software In The Loop approach. 
