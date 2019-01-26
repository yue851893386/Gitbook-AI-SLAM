---
title: "hdl_graph_slam"
---

# Overview

- [hdl_graph_slam-Github](https://github.com/koide3/hdl_graph_slam)
- [video](https://drive.google.com/file/d/0B9f5zFkpn4soSG96Tkt4SFFTbms/view)

>
hdl_graph_slam is an open source ROS package for real-time 6DOF SLAM using a 3D LIDAR. It is based on 3D Graph SLAM with NDT scan matching-based odometry estimation and loop detection. It also supports several graph constraints, such as GPS, IMU acceleration (gravity vector), IMU orientation (magnetic sensor), and floor plane (detected in a point cloud). We have tested this package with Velodyne (HDL32e, VLP16) and RoboSense (16 channels) sensors in indoor and outdoor environments.


![hdl_graph_slam](https://github.com/koide3/hdl_graph_slam/raw/master/imgs/hdl_graph_slam.png){#fig:}

# Requirements

```sh
sudo apt-get install ros-kinetic-geodesy ros-kinetic-pcl-ros ros-kinetic-nmea-msgs ros-kinetic-libg2o

cd catkin_ws/src
git clone https://github.com/koide3/ndt_omp.git

```
>
Note that, in case use are using ros indigo, hdl_graph_slam cannot be built with the ros g2o binaries (ros-indigo-libg2o). Install the latest g2o: The latest g2o causes segfault. Use commit a48ff8c42136f18fbe215b02bfeca48fa0c67507 instead of the latest one:

```sh
sudo apt-get install libsuitesparse-dev
git clone https://github.com/RainerKuemmerle/g2o.git
cd g2o
git checkout a48ff8c42136f18fbe215b02bfeca48fa0c67507
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=RELEASE
make -j8
sudo make install
```
