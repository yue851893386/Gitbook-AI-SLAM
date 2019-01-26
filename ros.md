---
title: "ROS"
---

# Resources
## 中国大学MOOC---《机器人操作系统入门》
- [ROS机器人操作系统入门-中国大学MOOC](https://www.bilibili.com/video/av24585414/?p=7&t=231)
- [中国大学MOOC---《机器人操作系统入门》课程讲义](https://sychaichangkun.gitbooks.io/ros-tutorial-icourse163/content/)
- [《机器人操作系统入门》课程讲义-Github](https://github.com/sychaichangkun/ROS-Academy-for-Beginners.git)
- [重德智能-github](https://github.com/DroidAITech)
- [Bilibili Vedio](https://www.bilibili.com/video/av24585414/?p=7)

## Projects
- [servicesim](https://bitbucket.org/osrf/servicesim)
- [OpenSourceRoboticsFoundation OSRF](https://bitbucket.org/osrf/)


# ROS foundationals

## __Important Notes__

- make sure **anaconda** is not installed, it may cause uncertain errors later. I encountered many unkown problems when compile SLAM and kinetic. And not use anaconda to install Python. Then install anaconda after everything works fun (not add anaconda to \$PATH is renewcommand).

- Select  proper Linux Version

According to [ROS Kinetic installation instructions](http://wiki.ros.org/kinetic/Installation),

>  ROS Kinetic installation instructions
>
> These instructions will install the **ROS Kinetic Kame** distribution, which is available for Ubuntu Wily (15.10) and Ubuntu Xenial (16.04 LTS), among other platform options.

## Install ROS Kinetic

```sh
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116

sudo apt-get install ros-kinetic-desktop-full

sudo rosdep init
rosdep update

echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
source ~/.bashrc

sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential

```

## gazebo

Upgrade gazebo:

```sh
sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
sudo apt-get update
sudo apt-get install gazebo7
```

## Shell Environment
```sh
#ROS
source /opt/ros/kinetic/setup.bash
source ~/catkin_ws/devel/setup.sh
```


## Commands

###  catkin_create_pkg
```sh
cd src/
catkin_create_pkg Test roscpp rospy std_msgs nav_msgs
```
### rospack list

```sh
rospack list | grep catkin_ws
source devel/setup.sh
```
### rospack
```sh
rospack find robot_sim_demo
```
### rosls
```sh
rosls topic_demo
```
###  rosed
```sh
rosed topic_demo CMakeLists.txt
```
### roscd
```sh
roscd topic_demo
```

### roslaunch
```sh
roslaunch [pkg_name] [file_name.launch]
```

### master
start ros master, rosout, parameter server:

```sh
roscore
```

### node
```sh
rosrun [pkg_name] [node_name]
rosnode list
rosnode info [node_name]
rosnode kill [node_name]
```
### rostopic
```sh
rostopic list
rostopic info /topic_name
rostopic echo /topic_name
rostopic pub /topic_name
```

### rosmsg
```sh
rosmsg list
rosmsg show /msg_name
```
### rosservice
```sh
rosservice list
rosservice info service_name
rosservice call service_name args
```
### rossrv
```sh
rossrv list
rossrv show srv_name
```
### rosparam

```sh
rosparam list
rosparam get param_key
rosparam set param_key param_value
rosparam dump file_name
rosparam load file_name
rosparam delete param_key
```

### rosbag
```sh
rosbag record <topic-names>
rosbag record -a
rosbag play <bag-files>
```

## Communication
- Topic
- Message (msg)
- Service (srv)
- parameter server
- Action

![topic-vs-service](https://i.imgur.com/S9VF64i.png){#fig:}

## Tools
- gazebo (OSRF)
ODE
- RViz
- rqt
  - rqt_graph
  - rqt_plot
  - rqt_console
- rosbag
- TF (TransForm)

![ros-link-fram](https://i.imgur.com/fTCBJv4.png){#fig:}

- URDF(Unified Robot Description Format)

## Client Library
- roscpp
- rospy
- roslisp

## SLAMs IN ROS
- Gmapping
- Karto



# robot_sim_demo

[重德智能-github](https://github.com/DroidAITech)

## Download anc Make

```sh
cd ~/catkin_ws/src
git clone https://github.com/DroidAITech/ROS-Academy-for-Beginners.git
cd ~/catkin_ws
rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
catkin_make
source ~/catkin_ws/devel/setup.bash
```

## How to use

```sh
$ rospack profile
$ roslaunch robot_sim_demo robot_spawn.launch

yubao@yubao-Z370M-S01:~/catkin_ws/src/ROS-Academy-for-Beginners$ rosnode list
/cmd_vel_mux
/gazebo
/gazebo_gui
/mobile_base_nodelet_manager
/rosout
/xbot/robot_state_publisher
/xbot/spawner

yubao@yubao-Z370M-S01:~/catkin_ws/src/ROS-Academy-for-Beginners$ rosnode info /cmd_vel_mux
--------------------------------------------------------------------------------
Node [/cmd_vel_mux]
Publications:
 * /mobile_base_nodelet_manager/bond [bond/Status]
 * /rosout [rosgraph_msgs/Log]

Subscriptions:
 * /clock [rosgraph_msgs/Clock]
 * /mobile_base_nodelet_manager/bond [bond/Status]

Services:
 * /cmd_vel_mux/get_loggers
 * /cmd_vel_mux/set_logger_level


contacting node http://yubao-Z370M-S01:40381/ ...
Pid: 20597
Connections:
 * topic: /rosout
    * to: /rosout
    * direction: outbound
    * transport: TCPROS
 * topic: /mobile_base_nodelet_manager/bond
    * to: /cmd_vel_mux
    * direction: outbound
    * transport: INTRAPROCESS
 * topic: /mobile_base_nodelet_manager/bond
    * to: /mobile_base_nodelet_manager
    * direction: outbound
    * transport: TCPROS
 * topic: /clock
    * to: /gazebo (http://yubao-Z370M-S01:45907/)
    * direction: inbound
    * transport: TCPROS
 * topic: /mobile_base_nodelet_manager/bond
    * to: /cmd_vel_mux (http://yubao-Z370M-S01:40381/)
    * direction: inbound
    * transport: INTRAPROCESS
 * topic: /mobile_base_nodelet_manager/bond
    * to: /mobile_base_nodelet_manager (http://yubao-Z370M-S01:42755/)
    * direction: inbound
    * transport: TCPROS

```

Control:

```sh
~/catkin_ws/src/ROS-Academy-for-Beginners$ rosrun robot_sim_demo robot_keyboard_teleop.py

Control The Robot!
---------------------------
Moving around:
   u    i    o
   j    k    l
   m    ,    .

q/z : increase/decrease max speeds by 10%
w/x : increase/decrease only linear speed by 10%
e/c : increase/decrease only angular speed by 10%
space key, k : force stop
anything else : stop smoothly

CTRL-C to quit

currently:	speed 0.2	turn 1
```
Add Image view;

```sh
 rosrun image_view image_view image:=/camera/rgb/image_raw
```




# Robots
- [willowgarage](http://www.willowgarage.com/)

## PR2
![pr2](https://i.imgur.com/9TaafSl.png){#fig:}

```sh
roslaunch pr2_bringup pr2.launch
```
