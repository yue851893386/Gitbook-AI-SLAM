---
Title:ROS
Date: Nov. 3 2018
---

# DEMO
## 中科院软件所柴长坤老师
- 转自https://www.icourse163.org/course/ISCAS-1002580008 来源为中国大学MOOC，ROS机器人操作系统，主讲人是中科院软件所柴长坤老师。
- [课程讲义](https://www.gitbook.com/book/sychaichangkun/ros-tutorial-icourse163/details)
- [github 代码示例](https://github.com/DroidAITech/ROS-Academy-for-Beginners)
- [Bilibili Vedio](https://www.bilibili.com/video/av24585414/?p=7)

# Errors
1. Invoking "make -j12 -l12" failed
- Error description

```sh
[  6%] Linking CXX executable /home/yubao/catkin_ws/devel/lib/tf_demo/tf_listerner
[  6%] Built target tf_listerner
Makefile:138: recipe for target 'all' failed
make: *** [all] Error 2
Invoking "make -j12 -l12" failed
```
- Solutions
```sh
pip install empy
```




# ROS Installation

- [Installation](http://wiki.ros.org/catkin/Tutorials)
- [environment variables](http://wiki.ros.org/ROS/EnvironmentVariables)
- [ROS_ROOT](http://wiki.ros.org/ROS/EnvironmentVariables#ROS_ROOT)
- [ROS_PACKAGE_PATH](http://wiki.ros.org/ROS/EnvironmentVariables#ROS_PACKAGE_PATH)
- [ROS file system tutorial](http://wiki.ros.org/ROS/Tutorials/NavigatingTheFilesystem)

### Environment setup

```sh
echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

If you have more than one ROS distribution installed, ~/.bashrc must only source the setup.bash for the version you are currently using.
If you just want to change the environment of your current shell, instead of the above you can type:

```sh
source /opt/ros/kinetic/setup.bash
```

If you use zsh instead of bash you need to run the following commands to set up your shell:

```sh
echo "source /opt/ros/kinetic/setup.zsh" >> ~/.zshrc
source ~/.zshrc
```

```
$ printenv | grep ROS
```

```sh
yubao@yubaoLiu:~/Desktop$ printenv |grep ROS
ROS_ROOT=/opt/ros/kinetic/share/ros
ROS_PACKAGE_PATH=/opt/ros/kinetic/share
ROS_MASTER_URI=http://localhost:11311
ROS_VERSION=1
ROSLISP_PACKAGE_DIRECTORIES=
ROS_DISTRO=kinetic
ROS_ETC_DIR=/opt/ros/kinetic/etc/ros
```

If you just installed ROS from `apt` on Ubuntu then you will have setup.*sh files in '`/opt/ros/<distro>/`', and you could source them like so:

```
$ source /opt/ros/<distro>/setup.bash
```

Using the short name of your ROS distribution instead of `<distro>`

If you installed ROS Kinetic, that would be:

```
$ source /opt/ros/kinetic/setup.bash
```

You will need to run this command on every new shell you open to have access to the ROS commands, unless you add this line to your .bashrc. This process allows you to install several ROS distributions (e.g. indigo and kinetic) on the same computer and switch between them.



# Navigating the ROS Filesystem

## Overview

You may have noticed a pattern with the naming of the ROS tools:

- rospack = ros + pack(age)
- roscd = ros + cd
- rosls = ros + ls

## Prerequisites

For this tutorial we will inspect a package in ros-tutorials, please install it using

```
$ sudo apt-get install ros-<distro>-ros-tutorials
```

Replace '<distro>' (including the '<>') with the name of your [ROS distribution](http://wiki.ros.org/Distributions) (e.g. indigo, kinetic, lunar etc.)

## Quick Overview of Filesystem Concepts

- **Packages:** Packages are the software organization unit of ROS code. Each package can contain libraries, executables, scripts, or other artifacts.
- **Manifests (package.xml):** A manifest is a description of a *package*. It serves to define dependencies between *packages* and to capture meta information about the *package* like version, maintainer, license, etc...

## Filesystem Tools

Code is spread across many ROS packages. Navigating with command-line tools such as `ls` and `cd` can be very tedious which is why ROS provides tools to help you.

### Using rospack

[rospack](http://wiki.ros.org/rospack) allows you to get information about packages. In this tutorial, we are only going to cover the `find` option, which returns the path to package.

Usage:

```
$ rospack find [package_name]
```

Example:

```
$ rospack find roscpp
```

would return:

```
YOUR_INSTALL_PATH/share/roscpp
```

### Using roscd

[roscd](http://wiki.ros.org/rosbash#roscd) is part of the [rosbash](http://wiki.ros.org/rosbash) suite. It allows you to change directory ([cd](http://ss64.com/bash/cd.html)) directly to a package or a stack.

Usage:

```
$ roscd [locationname[/subdir]]
```

To verify that we have changed to the roscpp package directory, run this example:

```
$ roscd roscpp
```

Now let's print the working directory using the Unix command [pwd](http://ss64.com/bash/pwd.html):

```
$ pwd
```

You should see:

```
YOUR_INSTALL_PATH/share/roscpp
```

You can see that `YOUR_INSTALL_PATH/share/roscpp` is the same path that `rospack find` gave in the previous exampleNote that [roscd](http://wiki.ros.org/roscd), like other ROS tools, will *only* find ROS packages that are within the directories listed in your [ROS_PACKAGE_PATH](http://wiki.ros.org/ROS/EnvironmentVariables#ROS_PACKAGE_PATH). To see what is in your [ROS_PACKAGE_PATH](http://wiki.ros.org/ROS/EnvironmentVariables#ROS_PACKAGE_PATH), type:

```
$ echo $ROS_PACKAGE_PATH
```

Your [ROS_PACKAGE_PATH](http://wiki.ros.org/ROS/EnvironmentVariables#ROS_PACKAGE_PATH) should contain a list of directories where you have ROS packages separated by colons. A typical [ROS_PACKAGE_PATH](http://wiki.ros.org/ROS/EnvironmentVariables#ROS_PACKAGE_PATH) might look like this:

```
/opt/ros/kinetic/base/install/share
```

Similarly to other environment paths, you can add additional directories to your [ROS_PACKAGE_PATH](http://wiki.ros.org/ROS/EnvironmentVariables#ROS_PACKAGE_PATH), with each path separated by a colon ':'..

**Subdirectories**

[roscd](http://wiki.ros.org/rosbash#roscd) can also move to a subdirectory of a package or stack.

Try:

```
$ roscd roscpp/cmake
$ pwd
```

You should see:

  ```
  YOUR_INSTALL_PATH/share/roscpp/cmake
  ```

### roscd log

`roscd log` will take you to the folder where ROS stores log files. Note that if you have not run any ROS programs yet, this will yield an error saying that it does not yet exist.

If you have run some ROS program before, try:

```
$ roscd log
```

### Using rosls

[rosls](http://wiki.ros.org/rosbash#rosls) is part of the [rosbash](http://wiki.ros.org/rosbash) suite. It allows you to [ls](http://ss64.com/bash/ls.html) directly in a package by name rather than by absolute path.

Usage:

```
$ rosls [locationname[/subdir]]
```

Example:

```
$ rosls roscpp_tutorials
```

would return:

```
cmake launch package.xml  srv
```

### Tab Completion

It can get tedious to type out an entire package name. In the previous example, `roscpp_tutorials` is a fairly long name. Luckily, some ROS tools support [TAB completion](http://en.wikipedia.org/wiki/Command_line_completion).

Start by typing:

```
$ roscd roscpp_tut<<< now push the TAB key >>>
```

After pushing the **TAB** key, the command line should fill out the rest:

```
$ roscd roscpp_tutorials/
```

This works because `roscpp_tutorials` is currently the only ROS package that starts with `roscpp_tut`.

Now try typing:

```
$ roscd tur<<< now push the TAB key >>>
```

After pushing the **TAB** key, the command line should fill out as much as possible:

```
$ roscd turtle
```

However, in this case there are multiple packages that begin with `turtle`. Try typing **TAB** another time. This should display all the ROS packages that begin with `turtle`:

```
turtle_actionlib/  turtlesim/         turtle_tf/
```

On the command line you should still have:

```
$ roscd turtle
```

Now type an `s` after `turtle` and then push **TAB**:

```
$ roscd turtles<<< now push the TAB key >>>
```

Since there is only one package that starts with `turtles`, you should see:

```
$ roscd turtlesim/
```

If you want to see a list of all currently installed packages, you can use tab completion for that as well:

```
$ rosls <<< now push the TAB key twice >>>
```

# Creating a ROS Package





# ROS Tutorials

## Resources

- [ROS Tutorials-Official](http://wiki.ros.org/ROS/Tutorials)
