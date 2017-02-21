---
layout: post
title: ROS industrial is coming to kinetic!
description: "ROS industrial will soon be supported by Kinetic Kame distribution. This tutorial will show how to install it"
modified: 2017-02-21
comments: true
tags: [Robotics, ROS, ROS-industrial]
image:
  feature: kinetic_kame.png
---

*ROS industrial* for *ROS Kinetic* distribution is on the verge of being [released](https://github.com/ros-industrial/industrial_core/commits/kinetic-devel). If you are like me and are anxious to test it out but can't wait until is available on PPAs then read on, I will show you how to make ROS industrial work with Kinetic distro!

<!-- more -->

# Update

ROS industrial is now available on PPAs!  This makes this post largely redundant. But I will keep it here for reference, maybe it will be helpful to someone at some point in time.

* Update your PPAs: `sudo apt-get update`
* Install ros kinetic: `sudo apt-get install ros-kinetic-industrial-core`

Aaand you can enjoy your ros industrial now, it's that simple.

# The old way (before official release)
If you want to run ros-industrial with kinetic today then you will have to compile it from source. Here are the steps you need to take in order to make it work:

* Install *moveit*: `sudo apt-get install ros-kinetic-moveit`
* Install *controller manager*: `sudo apt-get install ros-kinetic-controller-manager`
* Create *catkin workspace*. For example: `mkdir ~/catkin_ws && mkdir ~/catkin_ws/src`
* Navigate to your *catkin workspace* src directory: `cd ~/catkin_ws/src`
* Clone *industrial-core* repo: `git clone git@github.com:ros-industrial/industrial_core.git`
* Verify you are on kinetic-devel branch: `cd ~/catkin_ws/src/industrial_core && git branch`
* Make your *catkin package*: `cd ~/catkin_ws/ && catkin_make`
* Source the files: `source devel/setup.bash`

Now, if everything goes well your *ROS industrial* package will work! If you have any errors when executing catkin_make
then make sure all of your ROS packages are up to date.

If everything works well then follow the same pattern to install [*universal robot* package](https://github.com/ros-industrial/universal_robot),
complete the tutorials from readme file and explore further!

If you are interested in some more ROS tutorials then be sure to let me know, if there is enough interested I'll jump at making them happen!
