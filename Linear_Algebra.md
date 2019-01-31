
# Subspace
A Subspace subsject to:
$$
\vec 0 \in S \\
\vec v_1, \vec v_2 \in S \rightarrow \vec v_1 + \vec v_2 \in S \\
c \in R, \vec v \in S \rightarrow cv_1 \in S
$$

**Example**

**Proof** $$A:m \times n, N=\{\vec x \in R^n | A \vec x = \vec 0\}$$ is a subspace.

**Derivation**:


![Subspace 1[^Introduction-to-the-null-space-of-a-matrix]](assets/markdown-img-paste-20190130195118230.png){#fig:}



![Subspace 2 [^Introduction-to-the-null-space-of-a-matrix]](assets/markdown-img-paste-2019013019581072.png){#fig:}


# Nullspace

![Null Space 1[^Introduction-to-the-null-space-of-a-matrix] ](assets/markdown-img-paste-20190130201002981.png){#fig:}


rref =>reduced row echelon form

![Null Space 2 [^Introduction-to-the-null-space-of-a-matrix]](assets/markdown-img-paste-20190130201739754.png)


# Linear Independence

![Relation of null space to linear independence of matrix [^Introduction-to-the-null-space-of-a-matrix]](assets/markdown-img-paste-20190130202834901.png){#fig:}

# Column Space

![Column space of a matrix [^Column-space-of-a-matrix]](assets/markdown-img-paste-20190130203903327.png){#fig:}

> This matrix has m rows. So each of these guys are going to have m components. So they're all members of Rm. So the column space is defined as all of the possible linear combinations of these columns vectors.[^Column-space-of-a-matrix]

![Column space of a matrix 2 [^Column-space-of-a-matrix] ](assets/markdown-img-paste-20190130204722510.png){#fig:}

> The column space is all of the linear combinations of the column vectors, which another interpretation is all of the values that Ax can take on.

>So if I try to set Ax to some value that it can't take on, clearly I'm not going to have some solution. If I am able to find a solution, I am able to find some x value where Ax is equal to b2, then b2 definitely is one of the values that Ax can take on. [^Column-space-of-a-matrix]

# Example: Null space and column space basis

![Null space and column space basis 1 [^Null-space-and-column-space-basis] ](assets/markdown-img-paste-20190130210638584.png){#fig:}


![ Null space and column space basis 2 [^Null-space-and-column-space-basis]  ](assets/markdown-img-paste-20190130212201825.png){#fig:}


![ Null space and column space basis 3 [^Null-space-and-column-space-basis]](assets/markdown-img-paste-20190130213508119.png){#fig:}


![Null space and column space basis 4 [^Null-space-and-column-space-basis]](assets/markdown-img-paste-20190130213958537.png){#fig:}

Another Method:

![Null space and column space basis 5 [^Null-space-and-column-space-basis]](assets/markdown-img-paste-20190130214813592.png){#fig:}


You can always represent the non-pivot columns as linear combinations of the pivot columns.



# SVD: Singular Value Decomposition

## Defination
![Multiview Geometry-SVD [^Multiple-View-Geometry-Lecture2-Youtube] ](assets/markdown-img-paste-20190131165720920.png){#fig:}

**Formular**:

$$
A = U \Sigma V^T
$$

$$
A^T A = ( U \Sigma V^T)^T ( U \Sigma V^T) = V (\Sigma^T \Sigma )V^T \\
A A^T = ( U \Sigma V^T ) ( U \Sigma V^T)^T =  U (\Sigma \Sigma^T) U^T
$$

**Conclusion:**

- $\Sigma^2$ is the eigen value of $A^T A$ and $A A^T$
- $V$ is the eigen vector of $A^T A$
- $U$ is the eigen vector of $A A^T$
- $\Sigma$: Streching matrix; $V$ and $U$ are rotation matrix

## Proof


![ Proof of SVD Decomposition 2 [^Multiple-View-Geometry-Lecture2-Youtube] ](assets/markdown-img-paste-20190131175921243.png){#fig:}


## A Geometric interpretation of SVD


![2-dims rotation and streching [^Youtube-Lecture-SVD] ](assets/markdown-img-paste-20190131174143917.png){#fig:}

Here I went from one orthonormal basis to another orthonormal basis.

![proof of SVD [^Youtube-Lecture-SVD] ](assets/markdown-img-paste-20190131180037728.png){#fig:}

Inverse is the same as the complex conjugate.

n阶复方阵U的n个列向量是U空间的一个标准正交基，则U是酉矩阵(Unitary Matrix)。显然酉矩阵是正交矩阵往复数域上的推广。[^baidu]


![Multiview Geometry-a Geometry interpretation of SVD [^Multiple-View-Geometry-Lecture2-Youtube]](assets/markdown-img-paste-20190131175650795.png){#fig:}

## How to Compute U and V


![ Calculate U and V[^Youtube-Lecture-SVD]](assets/markdown-img-paste-20190131182652460.png){#fig:}


## Application
- PCA


# References
- [Khan Academy- Linear algebra](https://www.khanacademy.org/math/linear-algebra)
- [1.3.4Null Space (kernel) and Existence Uniqueness of Solutions](https://ocw.mit.edu/courses/chemical-engineering/10-34-numerical-methods-applied-to-chemical-engineering-fall-2005/lecture-notes/lecturenotes134.pdf)
- [Youtube-Singular Value Decomposition (the SVD)](https://www.youtube.com/watch?v=mBcLRGuAFUk)
- [Youtube-Lecture: The Singular Value Decomposition (SVD)](https://www.youtube.com/watch?v=EokL7E6o1AE)




[^baidu]:https://baike.baidu.com/item/%E9%85%89%E7%9F%A9%E9%98%B5/2967660
[^Youtube-Lecture-SVD]:https://www.youtube.com/watch?v=EokL7E6o1AE
[^Introduction-to-the-null-space-of-a-matrix]: https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/null-column-space/v/introduction-to-the-null-space-of-a-matrix
[^Column-space-of-a-matrix]: https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/null-column-space/v/column-space-of-a-matrix
[^Null-space-and-column-space-basis]: https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/null-column-space/v/null-space-and-column-space-basis
[^Multiple-View-Geometry-Lecture2-Youtube]: https://www.youtube.com/watch?v=6VbbYXpBIqA&index=2&list=PLTBdjV_4f-EJn6udZ34tht9EVIW7lbeo4
