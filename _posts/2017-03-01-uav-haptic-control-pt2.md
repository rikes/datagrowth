---
layout: post
title: UAV haptic control using Novint Falcon - pt 2
description: "I managed to implement Novint Falcon as UAV controller using ROS and libnifalcon. In this post I'm describing what I learned and showing my results "
modified: 2017-03-01
comments: true
tags: [Robotics, ROS, Pixhawk, UAVs, Mechatronics]
categories: [1ppm]
image:
  feature: falcon_code_large.png
---

I consider the second and final part of the falcon project as finished from [1PPM]({{site.url}}/1ppm/12-Technical-Challanges/) perspective. Most of the project I already described in the [previous post]({{site.url}}/1ppm/uav-haptic-control-pt1) 
 
Short summary of achieved results:

* All the work done and test for Px4 SITL(jmavsim)
* Mavros is used to talk to pixhawk (or SITL in this case)
* Falcon is not suitable for flying real models (it isn't reliable enough)

Without furthere due, here is the video showing the proof of concept in action:

*TODO: video (use Kazam to capture screen), pitivi to put everything together*


Want to know more about the project? Read on!

<!-- more -->

## Architecture

All of the work was done using ROS. The diagram below shows main relations between modules.

<figure class="center">
  <img src="{{site.url}}/images/falcon_arch.jpg" alt="Proof of concept system architecture">
	<figcaption>Relationship between ROS nodes and falcon/Px4</figcaption>
</figure>

I had a bit of an issue with making novint falcon work with ROS, here are some troubleshooting tips:

* Check if your falcon is connected to power supply (I lost 5 minutes of my life on that once!)
* Remember that there is [this](https://github.com/libnifalcon/libnifalcon/issues/45) issue
* You need C++14 compiler to make libnifalcon work with ROS, make sure you adjust your CMakeLists.txt file

## mavros

Mavros worked out rather well for me, however there are some things to look out for:

* Px4 needs to be in offboard mode for mavros velocity setpoints to be accepted
* Requests to mavros have to be sent with rate of at least 2Hz
* Messages sent to need a valid timestamp
* Mavros expects velocity setpoints to be in earth referenced, so there is a need for converting from body frame

## Testing

Unfortunately I won't be able to test this solution with a real multirotor any time soon. The huge disadvantage that comes with novint falcon is lack of portability (it needs 30V 1A power supply). Also I still don't have my pixhawk.

The reason I don't recommend using falcon for real aircraft is that I found it a bit unreliable. Sometimes it seems as if force feedback stops working for a short period of time. If you want to use it with a real aircraf then **make sure that you have some safety mode that you can fall back to**.

## Future work

I consider the project finished as a proof of concept. I might commit something more here and there to the github repo but I'm not planning to keep the project fully maintained. 

* Implement yaw rotation using digital buttons (lame, I know)
* Implement homing mode on starting program (for offsetting novint falcon encoders)
* Programatically establish minimum and maximum values for positions received from Falcon for each axis
* Clean up the code
* Review offb_node.cpp timings (especially refresh rates)

[Here](https://github.com/msadowski/px4_falcon) you can find the repo with all the code I created. Feel free to fork, and do pull requests! 
