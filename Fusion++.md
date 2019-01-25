
# 2018-Fusion++: Volumetric Object-Level SLAM

## Overview
体积对象级SLAM

- Paper [PDF](https://www.doc.ic.ac.uk/~sleutene/publications/fusion_plusplus_3dv_camera_ready.pdf)

- [matterport/Mask_RCNN](https://github.com/matterport/Mask_RCNN)
This is an implementation of Mask R-CNN on Python 3, Keras, and TensorFlow. The model generates bounding boxes and segmentation masks for each instance of an object in the image. It's based on Feature Pyramid Network (FPN) and a ResNet101 backbone.
- [andyzeng/tsdf-fusion](https://github.com/andyzeng/tsdf-fusion)
- [tensorpack/tensorpack](https://github.com/tensorpack/tensorpack)

- Demo-Youtube

<iframe width="640" height="480" src="https://www.youtube.com/embed/2luKNC03x4k" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- cite:


McCormac, John, et al. "Fusion++: Volumetric object-level slam." 2018 International Conference on 3D Vision (3DV). IEEE, 2018.

- Authors

John McCormac∗ Ronald Clark∗ Michael Bloesch Andrew J. Davison Stefan Leutenegger
Dyson Robotics Laboratory
Department of Computing, Imperial College London

## Abstract

我们提出了一个在线对象级SLAM系统,持久且准确的构建任意重建对象的3D图形图(graph map)。
当RGB-D相机浏览时一个杂乱的室内场景，Mask-RCNN instance segmentations 被用于初始化紧凑的每对象具有对象尺寸相关分辨率和新颖的3D前景蒙版的Truncated
Signed Distance Function（TSDF）重建。重建的对象存储在可优化的中
6DoF位姿图，它是我们唯一的持久地图表示。物体通过深度融合逐步细化（refined），并用于跟踪，重定位和閉環检测。閉環导致对象实例的相对姿势估计的调整，但没有内部对象（intra-object）的變形。每个对象还携带语义信息,並隨着時間的推移不断更新（refined），和一个存在概率来解释虚假的实例的预测. 我们在手持RGB-D上展示了我们的方法从一个包含大量
和各种对象实例杂乱的办公室场景中，突出显示系统如何实现闭环并在重复的循环中充分利用现有对象。
我们定量地评估我们的系统相对于RGB-D SLAM基准的基线方法的轨迹误差，并定性地比较YCB视频数据集上发现的对象的重建质量。性能评估显示我们的方法具有高内存效率，并且在4-8Hz（不包括重定位）的情况下在线运行，尽管没有在软件级别进行优化。

We propose an online **object-level** SLAM system which
builds a persistent and accurate 3D graph map of arbi-
trary reconstructed objects. As an RGB-D camera browses
a cluttered indoor scene, Mask-RCNN instance segmenta-
tions are used to initialise compact per-object Truncated
Signed Distance Function (TSDF) reconstructions with ob-
ject size-dependent resolutions and a novel 3D foreground
mask. Reconstructed objects are stored in an optimisable
6DoF pose graph which is our only persistent map repre-
sentation. Objects are incrementally refined via depth fu-
sion, and are used for tracking, relocalisation and loop clo-
sure detection. Loop closures cause adjustments in the rel-
ative pose estimates of object instances, but no intra-object
warping. Each object also carries semantic information
which is refined over time and an existence probability to
account for spurious instance predictions.


We demonstrate our approach on a hand-held RGB-D
sequence from a cluttered office scene with a large number
and variety of object instances, highlighting how the sys-
tem closes loops and makes good use of existing objects on
repeated loops.

We quantitatively evaluate the trajectory er-
ror of our system against a baseline approach on the RGB-
D SLAM benchmark, and qualitatively compare reconstruc-
tion quality of discovered objects on the YCB video dataset.
Performance evaluation shows our approach is highly mem-
ory efficient and runs online at 4-8Hz (excluding relocalisa-
tion) despite not being optimised at the software level.

## Introduction

Indoor scene understanding and 3D mapping is a foundational technology that can enable autonomous real-world
robotic task completion and also provide a common interface for more intelligent and intuitive **human-map and
human-robot interactions**. To enable this requires a careful
choice of map representation. One particularly useful repre-
sentation is to build an **object-oriented map**. We argue this
is a natural and efficient way to represent the things that are
most important for robotic scene understanding, planning
and interaction; and it is also highly suitable as the basis for
human-robot communication.


**Limitations**:

This approach also naturally paves the way towards interaction and dynamic object reasoning, although our system currently assumes a static environment and does not yet aim to track individual dynamic objects.
