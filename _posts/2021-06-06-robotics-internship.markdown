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
`27/05/2021` Introduction to ROS2 and the basics of robotics systems

### Weekly Updates :chart_with_upwards_trend:
`Week-1` **(23rd - 29th May)** ROS2 installation; completed ROS2 beginner tutorials<br>
`Week-2` **(30th May - 5th June)** completed ROS2 CLI Libraries tutorials; encountered a dependency error (rosdep dependencies were missing); started ROS2 Intermediate tutorial and encountered a colcon build fail error while "creating an action file"

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