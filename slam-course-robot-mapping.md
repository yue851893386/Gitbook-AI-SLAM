---
title: 'Robot Mapping Study Notes'
---

# Resources

- [Robot Mapping - WS 2013/14](http://ais.informatik.uni-freiburg.de/teaching/ws13/mapping/)

# Introduction to Robot Mapping
## What is SLAM?
- Computing the robot's poses and the map of the environment at the same time

- **Localization**: estimating the robot's location

- **SLAM**: building a map and localizing the robot simultaneously
  - What the environment looks like?
  - where the robot actually is?

Estimate the robot’s poses given landmarks
    
![Localization Example](/assets/Estimate the Robot Pose.png)  

Estimate the landmarks given the robot’s poses

![Localization Example](/assets/Estimate Landmarks.png)

Estimate the robot’s poses and the landmarks at the same time

![Localization Example](/assets/Screen Shot 2019-01-28 at 7.20.23.png)

**The SLAM Problem:**
- SLAM is a chicken-or-egg problem: 
  - a map is needed for localization and
  - a pose estimate is needed for mapping

It's a kind of a joint estimation task. We cannot fully decouple localization from mapping we actually have to solve this at the same point in time.

**SLAM is Relevant**:
- It is considered a fundamental problem for truly autonomous robots
- SLAM is the basis for most navigation systems


**SLAM Applications**:

SLAM is central to a range of indoor, outdoor, air and underwater applications for both manned and autonomous vehicles.

Examples:
  - At home: vacuum cleaner, lawn mower
  - Air: surveillance with unmanned air vehicles
  - Underwater: reef monitoring
  - Underground: exploration of mines
  - Space: terrain mapping for localization



  
# References

- [Robot Mapping - WS 2013/14](http://ais.informatik.uni-freiburg.de/teaching/ws13/mapping/)
  