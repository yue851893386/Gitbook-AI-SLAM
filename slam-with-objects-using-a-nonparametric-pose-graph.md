<!-- toc -->

## Slam with objects using a nonparametric pose graph（2016）

- Cite

```bibtex
@inproceedings{mu2016slam,
title={Slam with objects using a nonparametric pose graph},
author={Mu, Beipeng and Liu, Shih-Yuan and Paull, Liam and Leonard, John and How, Jonathan P},
booktitle={Intelligent Robots and Systems (IROS), 2016 IEEE/RSJ International Conference on},
pages={4602--4609},
year={2016},
organization={IEEE}
}
```

- [Dr. Michael Kaess](http://people.csail.mit.edu/kaess/)
- [paper-pdf](https://arxiv.org/pdf/1704.05959.pdf)
- [Demo-Youtube](https://youtu.be/YANUWdVLJD4)


<iframe width="640" height="480" src="https://www.youtube.com/embed/YANUWdVLJD4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### Problems Solving

The **data association and simultaneous localization and mapping (SLAM)** problems are, individually, well-studied in the literature. But these two problems are inherently tightly **coupled**, and that has not been well-addressed.
Without accurate SLAM, possible data associations are combinatorial and become intractable easily. Without accurate data association, the error of SLAM algorithms diverge easily.


### Contribution

- Creating a nonparametric pose graph model that couples data association and SLAM.
- Proposing an algorithm that jointly infers data associations and optimizes robot poses/object locations over nonparametric pose graphs.
- Developing an approach to generate object measurements from RGB and depth images in 3D space via deep learning object detection.
- Demonstrating the performance of the proposed approach via both simulated and real-world data.

This paper proposes a novel nonparametric pose graph that models data association and SLAM in a single framework.

An algorithm is further introduced to alternate between inferring data association and performing SLAM.


our approach has the new capability of associating object detections and localizing objects at the same time, leading to significantly better performance on both the data association and SLAM problems than achieved by considering only one and ignoring imperfections in the other.



### Abstract

Mapping and self-localization in unknown environments are fundamental capabilities in many robotic applications. These tasks typically involve the identification of objects as unique features or landmarks, which requires the objects both to be detected and then assigned a unique identifier that can be maintained when viewed from different perspectives and in different images

The **data association and simultaneous localization and mapping (SLAM)** problems are, individually, well-studied in the literature. But these two problems are inherently tightly **coupled**, and that has not been well-addressed.
Without accurate SLAM, possible data associations are combinatorial and become intractable easily. Without accurate data association, the error of SLAM algorithms diverge easily.

This paper proposes a novel nonparametric pose graph that models data association and SLAM in a single framework. An algorithm is further introduced to alternate between inferring data association and performing SLAM.

Experimental results show that our approach has the new capability of associating object detections and localizing objects at the same time, leading to significantly better performance on both the data association and SLAM problems than achieved by considering only one and ignoring imperfections in the other.

在未知环境中进行建图和自我定位是许多机器人应用程序的基本功能。这些任务通常涉及对象的识别，作为独特的特征或标识（landmarks）,因此需要检测出这些物体，并分配一个唯一的标识符，以便能够在不同的角度，不同的图像中能保持与维护这些对象特征。数据关联和SLAM问题已经单独地在文献中有很好的研究。但是这两个问题本质上是紧密耦合的，而且还没有得到很好的解决。如果没有准确的SLAM，可能的数据关联是组合的，并且很容易变得难以处理。如果没有准确的数据关联，SLAM算法的很容易发生各种各样的错误。本文提出了一种新的非参数姿态图
在单个框架中建模数据关联和SLAM。进一步引入算法以实现数据关联的推断和运行SLAM之间的相互交替。实验结果表明，我们的方法具有同时关联对象检测和同时对象定位的新功能，使得同时考虑数据关联与SLAM问题比只考虑一方而忽略另一方的情况有更明显的性能优势。

## Introduction

-  Occupancy grid map with LiDAR or laser range finders

 In occupancy based approaches, the world is represented by 2D/3D grids composed of free spaces and occupied spaces. New scans from the LiDAR or laser range finders are compared and matched with previous scans to incrementally build such maps.

  **However**, The successful matching of two scans relies on geometric features such as corners.  In places that lack such features, like long hallways, SLAM using occupancy grid maps tends to fail.

- SLAM with 3D dense mapping and RGB-D cameras

 This line of work is able to utilize both the geometric information from depth
cameras and the color information from RGB cameras to reconstruct environments in dense 3D maps.

 Incoming depth and color images are converted into volumes or deformation
 surfaces, then matched with previously constructed volumes or surfaces to incrementally build the map.

 3D densemaps provide photographic details of the environment with millions of volumes or surfaces.

 **However**, they rely heavily on parallel computation enabled by GPUs, and do not scale very well.

-  factor graph

 A factor graph encodes the poses of the robot and the observed landmarks along the trajectory.

 **However**, the convergence of factor graph SLAM algorithms relies heavily on correct data association of the landmarks.

- Objective of this paper

 The focus on of this work is on SLAM in unknown environment by recognizing objects and utilizing their positions (object SLAM).

- Object SLAM

 Object SLAM requires the robot to be able to detect objects, generate measurements, and associate these measurements to unique identifiers.

- object detection

  object detection refers to the problem of identifying the occurrence of objects of some predefined object classes within an image. An object measurement is a 3D location of the detected object with respect to the robot pose.

- Data association

  Data association refers to the problem of associating object measurements to unique identifiers across images.

- problem of object detection

 The problem of object detection has been an important topic in the computer vision  community.

 Some recent work on Region-based Convolutional Neural Networks [15, 19] gained significant success on training deep learning models to detect multiple objects instances within a single image.
  **However**, object detections only suggest the existence of objects of certain predefined object classes in an image, but provide no data association between images. given that an object of a certain class is detected in two images, the object detector provides no information on whether or not the detected objects in the two images are the same object.
  This is problematic for SLAM especially when there are multiple objects of the same object class in an environment.

 How reliably SLAM can be achieved using only these ambiguous object detections remains an open question.

 The robot would need to establish the data association of object detections across images from different views.




## iSAM - Source Code Simulation

- [Github-Source Code-BeipengMu/objectSLAM](https://github.com/BeipengMu/objectSLAM)
- [Github- JuliaRobotics/IncrementalInference.jl](https://github.com/JuliaRobotics/IncrementalInference.jl)
- [Github-BeipengMu/focused_slam](https://github.com/BeipengMu/focused_slam)
- [Online Documentation](http://people.csail.mit.edu/kaess/isam/doc/index.html)
- [iSAM: Incremental Smoothing and Mapping](http://people.csail.mit.edu/kaess/isam/)

### What is iSAM?

iSAM is an optimization library for sparse nonlinear problems as encountered in simultaneous localization and mapping (SLAM). The iSAM library provides efficient algorithms for batch and incremental optimization, recovering the exact least-squares solution. The library can easily be extended to new problems, and functionality for often encountered 2D and 3D SLAM problems is already provided. The iSAM algorithm was originally developed by Michael Kaess and Frank Dellaert at Georgia Tech.

### Directory tree

```sh
isamlib/  - Source code for the iSAM library
include/  - Header files for the iSAM library
isam/     - Source code for main iSAM executable
examples/ - Example code for iSAM
doc/      - Documentation (after calling "make doc")
misc/     - Code referenced from publications
data/     - Example data files for 2D and 3D
lib/      - iSAM library (after calling "make")
bin/      - Executables (after calling "make")
```


### iSAM library

Folder isam contains the modified isam library to optimize pose graphs. There are pre-compiled executable file isam is under the bin folder To compile from source, following the commands on ubuntu:

```sh
cd isam
mkdir build && cd build && cmake ..
make
```
Fore more details about the library, refer to readme file under isam folder.

### Simulation
To generate simulated dataset, run generateSimData.m. Ground truth objects are randomly generated. Click in the figure to generate the ground truth trajectory, make sure there are enough loop closures. When finished, press enter button on the keyboard.

To run the algorithm and compared algorithms, run main_simulation.m








## Refereces

1. "iSAM: Incremental Smoothing and Mapping" by M. Kaess, A. Ranganathan, and F. Dellaert, IEEE Trans. on Robotics, TRO, vol. 24, no. 6, Dec. 2008, pp. 1365-1378, [PDF](http://www.cc.gatech.edu/~kaess/pub/Kaess08tro.pdf)
1. "Covariance Recovery from a Square Root Information Matrix for Data Association" by M. Kaess and F. Dellaert, Journal of Robotics and Autonomous Systems, RAS, vol. 57, Dec. 2009, pp. 1198-1210, [PDF](http://www.cc.gatech.edu/~kaess/pub/Kaess09ras.pdf)
1. "An Incremental Trust-Region Method for Robust Online Sparse Least-Squares Estimation" by D.M. Rosen, M. Kaess and J.J. Leonard, International Conference on Robotics and Automation (ICRA), May 2012, [PDF](http://people.csail.mit.edu/kaess/pub/Rosen12icra.pdf)
