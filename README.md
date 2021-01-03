# README #

This repository contains the SW of a 2-drive wheeled robot simulation in gazebo with slam.
Based on http://moorerobots.com/ and https://github.com/richardw05/mybot_ws

Admin of this repository and the author: Burak Y\"uksel

## Important to know

* The content of this repo works with Ubuntu 20.04 (original work was done with ubuntu 16.04). Many things have been adapted accordingly, e.g. calling xacro --inline instead of xacro.py in launch files, or using turtlebot3 instead of turtlebot.

### How do I get set up? ###

* You have ROS [installed](http://wiki.ros.org/noetic/Installation/Ubuntu)
* See the ROS [tutorials] (http://wiki.ros.org/ROS/Tutorials) for more.
* Create your workspace and set it up [catkin_ws](http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment)
* in your ~\.bashrc you have
```js
source /opt/ros/<ROS-DISTRO>/setup.bash
source ~/catkin_ws/devel/setup.bash
```
* Clone this repository under the appropriate folder (e.g. under ~/catkin_ws/src or a new ws e.g. ~/robot_ws/src):
```console
$ git clone https://burakyuksel@bitbucket.org/burakyuksel/mybot_ros.git
```
* This repo is a ros package. Build the package (when e.g. under ~/catkin_ws)
```console
$ catkin_make
```
* source the path to this package in bashrc. Either in terminal (each) as:
```console
$ source devel/setup.bash
```
or by adding the following in ~/.bashrc:
```js
source ~/catkin_ws/devel/setup.bash
```
or your own new workspace:
```js
source ~/robot_ws/devel/setup.bash
```

## SLAM with turtlebot3

* source [here](https://automaticaddison.com/how-to-launch-the-turtlebot3-simulation-with-ros/#top)
* run the world:
```console
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
* run the slam (with gmapping):
```console
$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
* run the slam (nominal):
```console
$ roslaunch turtlebot3_slam turtlebot3_slam.launch
```

* control the robot manually:
```console
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
* control the robot automatically:
```console
$ roslaunch turtlebot3_gazebo turtlebot3_simulation.launch
```

### What is this repository for? ###

* I am trying to implement a similar algoritm here (using gazebo for testing) for roboros.
* run:
```console
$ roslaunch mybot_description mybot_tb3_world.launch
```
* in case you cannot find the mybot_ using roslaunch, then for some stupid reason linux might not be reading the bashrc "source" correctly. I could not figure it out yet why. Then do:
```console
$ cd roboros_ws/mybot_ws
$ source devel/setup.bash
$ roslaunch mybot_description mybot_tb3_world.launch
```
* control it manually:
```console
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
* save the map:
```console
$ rosrun map_server map_saver -f /tmp/test_map
```
* loading the map:
```console
$ roslaunch mybot_gazebo mybot_tb3_world.launch
$ roslaunch mybot_navigation mybot_navigation.launch map_file:=/tmp/test_map.yaml
```
* in rviz, estimate initial pose - click 2D Pose Estimate and click the approximate location of the robot on the map, and drag to indicate the direction.
* start teleop and move the robot around. The estimated positions should converge on the true position pretty quickly.
```console
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
* In rviz, send a few 2D Navigation Goals (click on `2D Nav Goal and click/drag to set position/orientation) and watch the robot autonomously navigate to the goal.

### Who do I talk to? ###

* Burak Y\"uksel