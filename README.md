# UR5-control-with-RG2
using TCP/IP network comunication to control UR5 robot with a RG2 gripper

## Motivation

There are many ways to control a UR5 robot, and ROS is the very common way. But in some cases we would not like to use ROS since it is quite hard to learn and configure...

So the more basic way to control UR5 is using TCP/IP network protocol and in a pure python way.

No any other requirement and installation, just in python we could control a real UR5 robot.

本项目的动机是为了简单化机械臂的控制。一般来说，控制机械臂常用的是ROS，但ROS一方面比较难学，更难配置- -。所以有时候不太想用ROS去操作机械臂，因此整了这么一个东西，可以直接通过TCP/IP socket套接字网络通信来对UR5机械臂进行控制。
就是纯python了，不存在其他的乱七八糟的配置。

## Code Structure
The main functions are writen in ` test_main.py `.

主要的控制功能函数都写在`test_main.py`文件里了

`get_current_tcp()` to get the current tool center position of UR5 (x, y, z, rx, ry, rz) 

本函数获取当前UR5机械臂工具末端位置，与示教器中的表示相同，6维浮点值

`get_current_pos()` to get the current tool center position of UR5 (x, y, theta), where theta is the top-down orientation

本函数获取当前UR5机械臂工具末端位置，但仅关心x、y和末端执行器（夹爪）垂直向下的转角

`move_to_tcp()` to control UR5 to move to a target tool center position (x, y, z, rx, ry, rz)

本函数控制机械臂末端运动到一个给定的位置

`increase_move()` to control UR5 to move a increase distance from current position (delta_x, delta_y, delta_z, delta_theta), where delta_theta is the increase distance of the top-down orientation

本函数控制机械臂从当前位置以增量的方式运动，delta_x即x坐标的增量，其他同理。

`operate_gripper()` to control the RG2 gripper to open to a desired width (target_width)

本函数控制机械臂夹爪开闭，函数参数为夹爪的目标宽度（RG2夹爪的宽度范围是0~130mm）

`check_grasp()` to check if the gripper is grasping an object. while the gripper is not fully closed, the function returns True

本函数检测某次抓取是否成功。如果成功，则夹爪不会完全闭合。

`move_down()` just move the tool down to a desired z coordinate

本函数控制机械臂末端向下运动，仅z轴坐标变化

`move_up()` just up the tool down to a desired z coordinate

与`move_done()`相反

`grasp()` open gripper then move down then close gripper then move up then check the grasp.

本函数执行一次抓取，先打开夹爪，再向下运动，再闭合夹爪，再向上运动，再检测抓取是否成功

`go_home()` control UR5 to move to the initial position

让机械臂回到初始点，该初始点需要自行修改

and file `rtde.py` and `serialize.py` are from the UR5 official examples and without any modification.

`rtde.py` 和 `serialize.py`这两个文件是直接从ur5官方例子中拉过来的，没有做修改，（其实也没去读。。）

file `util.py` contains some coordinate transformation functions.

`util.py`这个文件包含了一些坐标变换的函数。

## Contact
if any questions please contact me via zhixinc@buaa.edu.cn 

如果有问题的话，可以邮箱联系我，zhixinc@buaa.edu.cn 陈狗翔
