

# 2015-SLAM++: Simultaneous Localisation and Mapping at the Level of Objecs


## SLAM++: Simultaneous Localisation and Mapping at the Level of Objecs

**Authors**: Renato F. Salas-Moreno, Richard A. Newcombe, Hauke Strasdat, Paul H.J. Kelly, **Andrew J. Davison**[1]

[1] Professor, Department of Computing, Imperial College London, vision and AI technology for next generation home robotics

**Cite**:The IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2013, pp. 1352-1359

---

## Author Introduction: **Andrew J. Davison**

<img align="right" width=30% height=30% src="/Assets/images/papers/SLAM++/AndrewDavison_photo.png" >

- Currently his main research interests are in improving the performance in terms of **dynamics, scale, detail level, efficiency and semantic understanding of real-time 3D vision**

- He believes that SLAM is evolving into something even more important that I am calling "**Spatial AI**"(Refer:[**FutureMapping: The Computational Structure of Spatial AI Systems**](https://arxiv.org/pdf/1803.11288.pdf) )

---

## Overview [Demo-Youtube](https://www.youtube.com/watch?v=tmrAh1CqCRo&t=1s)

![](/Assets/images/papers/SLAM++/SLAMPlusPlus_YoutubeDemo.png)



## SLAM++ - A Pure Object-Level SLAM System

<img align="right" width=60% height=100% src="/Assets/images/papers/SLAM++/SLAMPlusPlus-chairs.png">

 In SLAM++, a cluttered 3D scene is efficiently **tracked and mapped in real-time** directly at the **object level**. </br>

A new **object oriented** 3D SLAM paradigm, which takes full advantage in the loop of prior knowledge that many scenes consist of repeated, domain-specific objects and structures.



## Abstract
Demonstrate real-time incremental SLAM:
- in large, cluttered environments, **scenes consit of repeated, domain-specific objects and structures**
- with relocalisation and loop closure
- with the detection of moved objects
- with **the generation of an object level scene description**
- with the potential to enable **interaction**

---

## Introduction - Current SLAM

Most current real-time SLAM systems operate at the level of
- **low-level primitives** (points, lines, patches or non-parametric surface representations such as depth maps), which must be
- **robustly matched**,
- **geometrically transformed**
-  and **optimised over** in order that
- **maps** represent **the intricacies of the real world**.

---

## Introduction - Object SLAM

- Much interest is now turning to **semantic labelling** of this geometry in terms of the objects and regions that are known to exist in the scene

However, this maybe reveals **a huge amount of wasted computational effort**
- The potential for a much better way of **taking account of domain knowledge in the loop of SLAM operation itself**
- Object SLAM has many characteristics of a return to feature-based SLAM methods

---
## Introduction - Proposed
This paper propose
- a paradigm for **real-time localisation** and
- **mapping** which harnesses **3D object recognition** to **jump over low level geometry processing** and
- **produce** incrementally built **maps** directly at the **object oriented** level.

---

## SLAM++ - A Pure Object-Level SLAM System

<img  align="right" width=60% height=60% src="/Assets/images/papers/SLAM++/SLAMPlusPlus_A_Pure_Object-Level_SLAM_System.png">

L: A live view at the **current camera pose** and the **synthetic rendered objects** </br>

R: Contrast **a raw depth camera normal map** with **the corresponding high quality prediction** from object graph

---

## Mapping Directly at the Object Level
## Advantages:

1. Instant **semantic understanding** enables **interaction** (Robotics, AR)
1. Dense representation and full predictive power of **KinectFusion** but **very memory-efficient**
1. Some aspects of a return to feature-based paradigm — full joint **optimisation of a graph** in real-time is feasible

---

## System Overview
<center>
<img height= 90% width=90% src="/Assets/images/papers/SLAM++/Outline_of_the_SLAM++_pipeline.png">
</center>

**Real-Time Loop**: </br>
- Currently uses depth data only (no RGB).
- Most components implemented primarily on GPU (not the pose graph optimisation which uses g2o).

---

## Methods - Overview

$D_l$: a live depth map;  $N_l$ :  normal map
First compute  a surface measurement in the form of a vertex and $N_l$ providing to the sequentially computed camera tracking and object detection pipelines

![](/Assets/images/papers/SLAM++/Outline_of_the_SLAM++_pipeline.png)

---

## Method - Overview - Step  1
**Track the live camera pose $T_{wl}$** with an iterative closest point (ICP) approach using the dense multi-object scene prediction  captured in the current SLAM graph $G$
![](/Assets/images/papers/SLAM++/Outline_of_the_SLAM++_pipeline.png)

---

## Method - Overview - Step 2

Attempt to **detect objects**, previously stored in a database, that are present in the live frame, **generating detection candidates** with **an estimated pose** in the scene. Candidates are first refined or rejected using a second ICP estimation initialised with the detected pose
![](/Assets/images/papers/SLAM++/Outline_of_the_SLAM++_pipeline.png)

---

## Method - Overview - Step 3

Add successfully **detected objects $g$** into the SLAM graph in the form of a **object-pose** vertex connected to the live estimated **camera-pose** vertex via a measurement edge
![](/Assets/images/papers/SLAM++/Outline_of_the_SLAM++_pipeline.png)

---

## Method - Overview - Step 4

Rendering objects from the SLAM graph produce a **predicted depth $D_r$** and **normal map $N_r$** into the live estimated frame, enabling us to actively **search only those pixels not described by current objects in the graph**. Run an individual ICP between each object and the live image resulting in the addition of a new camera-object constraint into the SLAM graph.
![55% center](/Assets/images/papers/SLAM++/Outline_of_the_SLAM++_pipeline.png)

---

## Object Database
<img align="right" height=40%  width=40%  src="/Assets/images/papers/SLAM++/SLAM++-Object_Database.png">

**Currently a small number of precisely known objects**:

Carefully scanned using **KinectFusion** and manually segmented

---

## Real-Time Object Detection

![center 60%](/Assets/images/papers/SLAM++/SLAM++-RealTimeObjectDetection.png)

From ‘Model Globally, Match Locally’, Drost et al., CVPR 2010
- Each object is described in terms of all point-pair features (PPF) across their whole 3D surface
- Point pair features are grouped and stored in a hash table

---

## Real-Time Object Detection - PPF
<center>
<img align="middle" height=80%  width=80%  src=/Assets/images/papers/SLAM++/SLAM++-RealTimeObjectDetection.png>
 </center>

$F$: PPF of two oriented points
$F_1$: the distance of the points
$F_2$: the angle between the normals and $F_1$
$F_4$: the angle between the two normals

---

## Real-Time Object Detection
<center>
<img align="middle" height=80%  width=80%  src=/Assets/images/papers/SLAM++/SLAM++-RealTimeObjectDetection.png>
 </center>

The global model description
Left: Point pairs on the model surface with **similar feature vector $F$**
Right: Those point pairs are stored in the same slot in the hash table

---

##  ICP Algorithm Overview
![50% center](/Assets/images/papers/SLAM++/ICP_breif_description.png)

- **Idea**: iterate to find alignmen
- **Wanted**: translation t and rotation R that minimizes the sum of the squared error:

![50% center](/Assets/images/papers/SLAM++/ICP_Minimum_Error.png)
Where  $x_i$ and $p_i$ are corresponding points

---

## ICP Refinement

<img align="right" height=60% width=60% src="/Assets/images/papers/SLAM++/SLAM++-ICPReinformance.png">

Noisy raw detected poses refined with ICP against object model:
- False detections removed with threshold after ICP
- Accurate object-camera constraints achieved and added to graph


---

## Camera Tracking
Camera is tracked using ICP against a depth map raycasted from the current whole world model at last pose:
- Very much the same as KinectFusion; but we track against our perfect, **complete object models**
- Full prediction and **occlusion handling**, even for recently acquired objects.

---

## Graph Optimisation

<img align=right src="/Assets/images/papers/SLAM++/Example_graph_illustrating.png">

- Reprsent the world as a graph
- Each node stores estimated $SE(3)$ pose (rotation and translation relative to a fixed world frame)

**Goal**: minimize the sum over all measurement constraints


---

## Graph Optimisation Presentation

<img align=right src="/Assets/images/papers/SLAM++/Example_graph_illustrating.png">

- $T_{woj}$:  $SE(3)$ pose of object $j$
- $T_{wi}$:  SE(3) pose of the historical pose of the camera at timestep $i$.
- $Z_{i,oj}$: constraints, which links one camera pose and one object pose

---


## Map Representation

<img align="right" height=60%  width=60%  src="/Assets/images/papers/SLAM++/SLAM++-Map_reprsentation.png">

**A Pure Graph of Objects**:

A pose graph where all constraints are 6DoF

---

## Moved Object Detection

<img align="right" height=60% width=60% src="/Assets/images/papers/SLAM++/SLAM++-MovedObjectDetection.png">

This paper demonstrate the ability to detect the movement of objects, which fail ICP gating due to inconsistency

---

## Relocalisation
<img align=right height=50% width=50% src="/Assets/images/papers/SLAM++/Relocalization_procedure.png">
 When camera tracking is lost the system enters a relocalisation mode.

 The matched vertex with highest vote in the long-term graph is used instead of the currently observed vertex in the local graph and camera tracking is resumed from it, discarding the local map.

---

## Augmented Reality with Objects
![center 80%](/Assets/images/papers/SLAM++/AugmentedRealityWithObjects.png)

The ability to semantically predict complete surface geometry from partial views allows novel context aware AR capabilities such as path finding, to gracefully avoid obstacles while reaching target objects

---


# Any Questions?

---

# Conclusions
- Using **high performance 3D object recognition** in the loop permits a new approach to real-time SLAM with large advantages in terms of **efficient and semantic scene description**.
- Suit to locations like **the interiors of public buildings** with many **repeated, identical elements**.
