---
layout: post
title: UAV haptic control using Novint Falcon - pt 2
description: "I managed to implement Novint Falcon as  UAV controller in "
modified: 2017-02-28
comments: true
tags: [Robotics, ROS, Pixhawk, UAVs, Mechatronics]
categories: [1ppm]
image:
  feature: falcon_code_large.png
---

I consider the second and final part of the falcon project as finished from [1PPM]({{site.url}}/1ppm/12-Technical-Challanges/) perspective. Most of the project I already described in the [previous post]({{site.url}}/1ppm/uav-haptic-control-pt1) 

<figure class="half center">
  <img src="{{site.url}}/images/Novint_Falcon.jpg" alt="Novint Falcon Haptic Controller">
	<figcaption>Just reminding you how Falcon looks like</figcaption>
</figure>
  
Short summary of achieved results:

* All the work done and test for Px4 SITL(jmavsim)
* Mavros is used to talk to pixhawk (or SITL in this case)
* Falcon is not suitable for flying real models (it isn't reliable enough)

<!-- more -->

Future work:

* Implement yaw rotation using digital buttons (lame, I know)
* Implement homing mode on starting program (for offsetting falcon encoders)
* Programatically establish minimum and maximum values for positions received from Falcon for each axis
* Clean up the code


