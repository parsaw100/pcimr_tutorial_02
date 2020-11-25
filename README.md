# Practical Course: Intelligent Mobile Robots with ROS (PCIMR)

## Tutorial 02: Robotics hardware & kinematics

### Introduction

The purpose of this tutorial is to develop an algorithm to prevent robots from colliding with obstacles. 
Two robots are available in the simulation, one with differential and the other with omnidirectional drive mode. 
Inside the simulation environment, there are several obstacles that all are visible to the LIDAR sensor. 
Makes it easier to ignore other sensors and work only with 245 data points. 
Unfortunately, the robots cannot prevent collisions from moving backwards since the sensor angle is limited. 

### Approach

A simple subscriber/publisher controller node was implemented to read the keyboard inputs as well as the LIDAR sensor 
and publish the appropriate angular and linear velocities. 
The controller finds the minimum distance among the 245 data points and then it calculates the respective angle.
Afterwards, it calculates the width and compares it to the safety distance. 
If the width of the passage is wide enough the controller allows the robot to go on with full speed. 
if the width is lower or close to the safety distance the controller adjusts the velocities proportional to the distance using a tanh_based velocity model. 
Since both robots cannot move linearly in the Y direction the controller only applies the velocity model to the X direction.

### Learning Outcomes
Not a huge difference was noted while testing the controller for both robots, the same controller worked fine for both but some unstablities were noticed while 
turning or rotating. 

### Launching 

export ROBOT=rto-1 or p3dx

roslaunch scan_it safe_drive.launch

rosrun teleop_twist_keyboard teleop_twist_keyboard.py cmd_vel:=/input/cmd_vel

