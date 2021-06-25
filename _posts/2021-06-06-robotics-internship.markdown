---
layout: post
title:  "Robotics Internship"
date:   2021-06-06 20:36:50 +0530
categories: jekyll update
cat: assets/images/cat.png
forest: assets/images/forest.png
---
## **Timeline** :hourglass_flowing_sand:

### Briefings :desktop_computer:
`19/05/2021` Overview of the internship and current project run through<br>
`27/05/2021` Introduction to ROS2 and the basics of robotics systems<br>
`15/06/2021` Briefed about URDF; given an overview of the upcoming work<br>
`25/06/2021` <b>Product Team Meeting</b> Assigned task for the next month<br>

### Weekly Updates :chart_with_upwards_trend:
`Week-1` **(23rd - 29th May)** ROS2 installation; completed ROS2 beginner tutorials<br>
`Week-2` **(30th May - 5th June)** Completed ROS2 CLI Libraries tutorials; encountered a dependency error (rosdep dependencies were missing); started ROS2 Intermediate tutorial and encountered a colcon build fail error while "creating an action file"<br>
`Week-3` **(6th - 12th June)** Introduction to Gazebo, Rviz and Nav2 module<br>
`Week-4` **(13th June - 19th June)** Introduction to URDF files and set up files <br>

### Installations and Errors :interrobang:
<u>linux kernel upgradation</u><br> Couldn't find the boot menu; was stuck for an hour and a half :alarm_clock:<br>
Later I accessed it through the **GRUB** screen<br>
It took me half a day to manually update my linux kernel from **18.10** to **20.04 LTS release (focal)**<br>

<u>catkin package source installation</u><br> Had to go with source installation as it was missing from the ROS2 setup<br>

<u>rosdep dependencies missing</u><br> Led to an error in **CLI libraries** tutorial
{% highlight ruby %}
rosdep install -i --from-path src --rosdistro <distro> -y
# <distro> is foxy in this case
{% endhighlight %}

<u>cross compilation error</u><br> The libraries in anaconda and ros-foxy led to a runtime error due to cross compilation; we tried upgrading colcon but that did not work; we then referred to an article and changed the path as mentioned
[article](https://blog.csdn.net/weixin_37532614/article/details/105552101)<br>
The error still persisted, but this time, there was no cross compilation error, it was "something different"<br>
We figured out that changing from the base environment to the root environment might help; so I deleted the entire `action_ws` workspace and started again, this time doing it in the root environment<br>
And this solved the error; colcon build was successful here :heavy_check_mark: <br>

<u>error in server-client file compilation</u><br>
The colcon build just failed here (again! :woman_facepalming:)<br>
We tried changing the file extensions (in `#include` lines in server cpp code) from `.hpp` to `.h` and `.cpp` none of which worked<br>
Turns out that the dependensies weren't being called and the compilation wasn't done as well<br>
`the hpp file is communicating with visibility code script where a bridge has been created between the dependencies` - cause of error as explained by the project mentor :man_mechanic:<br>

<u>"frame [map] does not exist" error while following nav2 tutorial</u><br>
The tutorial specified that Gazebo and Rviz GUIs should open up with a simple map; however in my case, it was taking a lot of time (around 5 minutes) for Gazebo to even start and the entire system would just hang up :interrobang:<br> 
I run through some basic commands to see if Gazebo and Rviz were working with ROS2, Gazebo was working fine and I could even make a simple robot move in it (again, I followed a tutorial suggested by my mentor to verify the working) :checkered_flag:<br>
I then run the command `ros2 run rviz2 rviz2` and Rviz window popped up meaning that Rviz was working fine as well<br>
I resumed to following the Nav2 tutorial, and this time, I waited for a while (2-3 minutes) and both Gazebo and Rviz started up. I eventually completed the tutorial (moving a robot from a point to navigation goal) :robot:

<u>colcon build failed in the "Robot State Publisher" section</u><br>
The errors somewhat hinted towards an incorrect launch folder location; I tried changing the location of the launch folder, yet the colcon build failed<br>
I went on and made a different workspace and placed the launch folder in the root location of the package to be built and it worked! yay! :partying_face:<br>