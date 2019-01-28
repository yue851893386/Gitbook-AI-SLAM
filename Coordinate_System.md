



# Rotation Matrix

## 2D (Method 1)
![Coordinate Roatation](assets/markdown-img-paste-20190126225013479.png){#fig:}

P(x,y):

$$
\left\{\begin{matrix}
x = \overline{OP} cos \alpha  & \\
y = \overline{OP} sin \alpha
\end{matrix}\right.
$${#eq:}

After rotation, we get $P \prime (x \prime, y \prime)$:

$$
\left\{\begin{matrix}
x \prime = \overline{OP} cos(\alpha + \theta) \\
y \prime = \overline{OP} sin(\alpha + \theta)
\end{matrix}\right. \\
=
\left\{\begin{matrix}
x \prime = \overline{OP}(cos \alpha cos \theta - sin\alpha\sin \theta) \\
y \prime = \overline{OP}(sin \alpha cos \theta + cos \alpha sin \theta)
\end{matrix}\right. \\
=
\left\{\begin{matrix}
x \prime = x cos \theta - y\sin \theta \\
y \prime = y cos \theta + x sin \theta
\end{matrix}\right.
$${#eq:}

=>

$$
\begin{bmatrix}
{x}'\\
{y}'
\end{bmatrix}
=
\begin{bmatrix}
cos \theta  & -sin\theta \\
sin \theta & cos \theta
\end{bmatrix}
\begin{bmatrix}
x\\
y
\end{bmatrix}
$${#eq:}

## 2D (Method 2)

![Rotation Matrix in 2D[^XiaoXiangXueYuan]](assets/markdown-img-paste-20190128163102101.png){#fig:}



$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
r00 & r01 \\
r10 & r11
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

Use two vectors $(1, 0)$ and $(0, 1)$, we can calculate the unkonwn parameters.


![Rotated Coordinate Frames in 2D [^RotatedCoordinate2D]](assets/markdown-img-paste-20190128164555171.png){#fig:}












# Reference
[^XiaoXiangXueYuan]: [小象学院 2018最新SLAM无人驾驶、VR/AR课程](https://www.bilibili.com/video/av37063566/?p=2)

[^RotatedCoordinate2D]: Corke, Peter. Robotics, Vision and Control: Fundamental Algorithms In MATLAB® Second, Completely Revised. Vol. 118. Springer, 2017.
