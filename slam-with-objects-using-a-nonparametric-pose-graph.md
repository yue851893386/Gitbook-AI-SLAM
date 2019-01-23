## Slam with objects using a nonparametric pose graph

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

- [paper-pdf](https://arxiv.org/pdf/1704.05959.pdf)

### Contribution
1. This paper proposes a novel nonparametric pose graph that models data association and SLAM in a single framework.
1. An algorithm is further introduced to alternate between inferring data association and performing SLAM. 


### Abstract

Mapping and self-localization in unknown environments are fundamental capabilities in many robotic applications. These tasks typically involve the identification of objects as unique features or landmarks, which requires the objects both to be detected and then assigned a unique identifier that can be maintained when viewed from different perspectives and in different images

The **data association and simultaneous localization and mapping (SLAM)** problems are, individually, well-studied in the literature. But these two problems are inherently tightly **coupled**, and that has not been well-addressed.
Without accurate SLAM, possible data associations are combinatorial and become intractable easily. Without accurate data association, the error of SLAM algorithms diverge easily.

This paper proposes a novel nonparametric pose graph that
models data association and SLAM in a single framework. An
algorithm is further introduced to alternate between inferring
data association and performing SLAM. Experimental results
show that our approach has the new capability of associating
object detections and localizing objects at the same time, leading
to significantly better performance on both the data association
and SLAM problems than achieved by considering only one and
ignoring imperfections in the other.

在未知环境中进行建图和自我定位是许多机器人应用程序的基本功能。这些任务通常涉及对象的识别，作为独特的特征或标识（landmarks）,因此需要检测出这些物体，并分配一个唯一的标识符，以便能够在不同的角度，不同的图像中能保持与维护这些对象特征。数据关联和SLAM问题已经单独地在文献中有很好的研究。但是这两个问题本质上是紧密耦合的，而且还没有得到很好的解决。如果没有准确的SLAM，可能的数据关联是组合的，并且很容易变得难以处理。如果没有准确的数据关联，SLAM算法的很容易发生各种各样的错误。本文提出了一种新的非参数姿态图
在单个框架中建模数据关联和SLAM。进一步引入算法以实现数据关联的推断和运行SLAM之间的相互交替。实验结果表明，我们的方法具有同时关联对象检测和同时对象定位的新功能，使得同时考虑数据关联与SLAM问题比只考虑一方而忽略另一方的情况有更明显的性能优势



 




























