# UR5-control-with-RG2
using TCP/IP network comunication to control UR5 robot with a RG2 gripper

## Motivation

There are many ways to control a UR5 robot, and ROS is the very common way. But in some cases we would not like to use ROS since it is quite hard to learn and configure...

So the more basic way to control UR5 is using TCP/IP network protocol and in a pure python way.

No any other requirement and installation, just in python we could control a real UR5 robot.


## Code Structure
The main functions are writen in ` test_main.py `.

`get_current_tcp()` to get the current tool center position of UR5 (x, y, z, rx, ry, rz)

`get_current_pos()` to get the current tool center position of UR5 (x, y, theta), where theta is the top-down orientation

`move_to_tcp()` to control UR5 to move to a target tool center position (x, y, z, rx, ry, rz)

`increase_move()` to control UR5 to move a increase distance from current position (delta_x, delta_y, delta_z, delta_theta), where delta_theta is the increase distance of the top-down orientation

`operate_gripper()` to control the RG2 gripper to open to a desired width (target_width)

`check_grasp()` to check if the gripper is grasping an object. while the gripper is not fully closed, the function returns True

`move_down()` just move the tool down to a desired z coordinate

`move_up()` just up the tool down to a desired z coordinate

`grasp()` open gripper then move down then close gripper then move up then check the grasp.

`go_home()` control UR5 to move to the initial position

and file `rtde.py` and `serialize.py` is from the UR5 official examples and without any modification.

file `util.py` contains some coordinate transformation functions.


