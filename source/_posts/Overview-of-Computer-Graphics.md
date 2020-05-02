---
title: GAMES-101：Modern Computer Graphics
top: true
cover: true
toc: true
mathjax: true
date: 2020-05-02 14:02:50
password:
summary: 持续更新中
tags:
 - 图形学
 - 基础知识
categories:
 - 图形学
---

GAMES101是闫令琪老师的现代图形学入门，本文是二刷这个mooc的小总结，（flag）拟三天内完成。

## 0. Overview of Computer Graphics

### What is Computer Graphics?

The use of computers to synthesize and manipulate visual information.

### Why Study Computer Graphics?

#### Applications

0. Video Games: e.g. "_SEKIRO: Shadows Die Twice_",  "_Borderlands 3_";

1. Movies: e.g. "_The Matrix（1999）_","_Avatar（2009）_";

2. Animations: e.g. "_Zootopia（2016）_","_Frozen 2（2019）_";

3. Design: e.g. CAD , CAM ;

4. Visualization: e.g Science, Engineering, Medicin, Journalism, etc. ;

5. Virtual Reality & Augemented Reality;

6. Digital Illustration: e.g. PhotoShop;

7. Simulation: "_Black hole_"（simulate the light/ray）,"_Dust Bowl phenomena_";

8. GUI: Graphical User Interfaces;

9. Typography: Font（about vector or lattice） ;

   Rmk: “_The Quick Brown Fox Jumps Over The Lazy Dog._" usually be used in this application because it contain 26 alphabets.

#### Fundamental Intellectual Challenges

0. Creates and interacts with realistic virtual world

1. Requires understanding of all aspects of physical world

3. New computing methods, displays, technologies

#### Technical Challenges

0. Math of （perspective） projections, curves,surfaces

1. Physics of lighting and shading

2. Repressenting/ operating shapes in 3D

### Course Topics

#### Rasterization

0. Project <font color=red>geometry  primitives</font> （3D triangles / polygons） onto the screen;

1. Break projected primitives into <font color=red>fragments（pixels）</font> ;

2. Gold standard in Video Games（Real-time Application）.

   p.s : Real-time Application: biger than 30 fps.

#### Curves and Meshes

​	How to represent geometry in Computer Graphics

#### Ray Tracing 

0. Shoot rays from the camera though each pixel;
   0. Calculate <font color=red>intersection</font> and <font color=red>shading</font>;
   1. <font color=red>Continue to Bounce</font> the rays till they hit light sources.

1. Gold standard in Animations/ Movies（Offline Applications）.

#### Animation / Simulation

0. Key frame Animation;

1. Mass-spring System.（弹簧振子系统）

### Differences between CV and CG

Everything that needs to be guessed belongs to Computer Verson, and in this MOOC, we don't introduce it.

"MODEL" use CG（rendering） to "IMAGE", and "IMAGE" use CV to "MODEL"."MODEL" usually uesd in CG like modeling, simulation; "IMAGE" usually uesd in CV,like Image Processing.

But CV and CG have not clear boundaries.

## 1. Linear Algebra

### Vector

0. Usually written as $\vec a$ or in bold $\bold a$;

1. Or using start and end points $\vec {AB}=B-A$;

2. The vector contain direcition and length;

3.  Vector have no absolute starting position（we can see this property in homogeneous coordinate）;

4. Magnitude（length） of a vector written as $||\vec a||$（二范数，模长等中文名）;

5. Unit vector （Vector Normalization）

   0. A vector with Magnitude（length） of 1;

   1. Finding the unit vector of a vector（normalization）: 
      $$
      \hat a=\frac{\vec a}{||\vec a||}
      $$
      $\hat a$ read as "_a hat_".

   2. Used to represent directions.

6. Vector Addition

   0. Geometrically: Parallelogram la or Triangle law;

   1. Algebraically: Simply add coordinates.

7. Cartesian Coordinates —笛卡尔坐标系

   p.s. The defination of Cartesian Coordinates should get some basic in Set Theorey, Cartesian product. So we pass this defination.

   X and Y can be any （usually orthogonal unit ） vectors:
   $$
   A=\left(
   \begin{matrix}
   x\\\\
   y
   \end{matrix}
   \right),A^T=(x,y), ||A||=\sqrt{x^2+y^2}
   $$
   the symbol $T$  represent the transposition, it is also used in Matrix.

8. Dot（scalar：标量） Product
   $$
   {\vec a} \cdot {\vec b}=||\vec a||||\vec b||cos\theta,cos\theta=\frac{\vec a \cdot\vec b}{||\vec a||||\vec b||}
   $$

   0. For unit vector $cos\theta=\hat a\cdot\hat b$.

   2. properties:

      0. $\vec a \cdot\vec b=\vec b \cdot\vec a$;

      1. $\vec a \cdot （\vec b+\vec c）=\vec a \cdot \vec b+\vec a \cdot \vec c$;

      2. $（k\vec a）\cdot \vec b=\vec a\cdot （k\vec b）=k（\vec a\cdot \vec b ）$;

      3. In artesian Coordinates: Component-wise multiplication ,then adding up（$\vec a=（x_1,x_2,...,x_n）^T,\vec b=（y_1,
         y_2,...,y_n）^T$）
         $$
         \vec a \cdot \vec b=\displaystyle\sum_{i=1}^nx_iy_i
         $$

      4. Usage: 

         0. Find angle between two vectors:

         1. Finding  <font color=red>projection</font>  of one vector on another:

            $\vec b_{\perp}$:projection of $\vec b$ onto $\vec a$.

            1. $\vec b_{\perp}=k\hat a$;
            2. $k=||\vec b_{\perp}||=||\vec b||cos\theta$.

         2. Measure how close two directions are;

         3. Decompose a vector;

         4. Determine forward（clockwise） / backword（anticlockwise）;

9. Cross（vector） product

   0. Cross product is orthogonal to two initial vectors;

   1. Direction determined by right-hand rule;

   2. Useful in constructing coordinate systems（later）.

   3. properties 

      0. $\vec a  \times \vec b=-\vec b \times \vec a$;

      1. $\vec a \times \vec a= \vec 0$;
      2. $\vec a\times （\vec b+\vec c）=\vec a\times \vec b+\vec a\times \vec  c$;
      3. $\vec a\times（k\vec b）=k（\vec a\times\vec b）$.

   4. Cartsesian Formula
      $$
      \vec a\times \vec b=\left(\begin{matrix}y_az_b-y_bz_a\\\\z_ax_b-x_az_b\\\\x_ay_b-y_ax_b\end{matrix}\right)
      $$
      Later 
      $$
      \vec a\times \vec b=A^*b=\left(\begin{matrix}0&-z_a&y_a\\\\z_a&0&-x_a\\\\-y_a&x_a&0\end{matrix}\right)\left(\begin{matrix}x_b\\\\y_b\\\\z_b\end{matrix}\right)
      $$

   5. Usage

      0. Determine **left / right**;

      1. Determine **inside / outside** ;

10. Orthonormal bases and coordinate frames

    it is important for representing points, positions, locations, and many sets of coordinate systems such as Clobal, local ,world, etc. And critical issue is transforming between these systems/bases.

    Any set of 3 vectors (in 3D) that （$\vec p$ is projection）
    $$
    ||\vec u||=||\vec v||=||\vec w||=1\\\\
    \vec u \cdot \vec v=\vec v\cdot \vec w=\vec  u \cdot \vec w=0\\\\
    \vec w=\vec u \times \vec v（right\space handed）\\\\
    \vec p=(\vec p \cdot \vec u)\vec u+(\vec p \cdot \vec v)\vec v+(\vec p \cdot \vec w)\vec w
    $$

### Matrices

In Graphics, pervasively used to represent transformations （include Translation, Rotation, Shear, Scale）.

0. What is a matrix
   0. Array of numbers（$m\times n=m\space rows,n\space columns$）

   $$
   \left(
   \begin{matrix}1&3\\\\5&2\\\\0&4\end{matrix}\right)
   $$

   1. Addition and multiplication by a scalar are trivial: element by element.

1. Matrix-Matrix Multiplication

   if$A\times B$, then the columns in A must =rows in B, namely $(M\times N)(N\times P)=(M\times P)$.

   0. Element $(i,j)$ in the product is the dot product of row i from A and column j from B.

   1. propertise:

      0. Generally speaking, the Multiplication is **non-commutative**, namely AB and BA are different **in general**;

      1. Associative and distributive

         0. $(AB)C=A(BC)$;（can accelarate the speed by dp）

         1. $A(B+C)=AB+AC$;
         2. $(A+B)C=AC+BC$.

2. Matrix-VectorMultiplication

   0. Treat vector as a column matrix($m\times 1$)

   1. Key for transforming points.

   2. Official spoiler: 2D reflection about y=axis
      $$
      \left(\begin{matrix}-1&0\\\\0&1\end{matrix}\right)
      \left(\begin{matrix}x\\\\y\end{matrix}\right)
      =\left(\begin{matrix}-x\\\\y\end{matrix}\right)
      $$

3. Transpose of a Matrix

   0. Switch rows and columns（$（i,j）\rightarrow（j,i）$）;

   1. $(AB)^T=B^TA^T$.

4. Identity Matrix and Inverses

   0. Identity Matrix:

   $$
   I_{3\times3}=\left(\begin{matrix}1&0&0\\\\0&1&0\\\\0&0&1\end{matrix}\right)
   $$

   1. Inverses:

      0. $AA^{-1}=A^{-1}A=I$;

      1. $(AB)^{-1}=B^{-1}A^{-1}$.

### Transformation

0. Why study transformation

   0. Modeling 
   1. Viewing

1. 2D transformations: rotation, scale, shear

   0. Representing transformations using matrices

   1. The matrix

      0. Rotation：Suppose rotate about the origin $(0,0)$ ,  anticlockwise by default and rotate angel is $\theta$.So the matrix is :
         $$
         R_{\theta}=\left[ \begin {matrix} cos\theta&-sin\theta\\\\sin\theta&cos\theta\end{matrix}\right]
         $$
         $proof:$

         ​	Get a Cartesian Coordinates $Oxy$, all the vectors, begin from origin, write as $V$.

         ​	Suppose  we want $\vec {OP}=(x,y)$ rotate to $\vec {OP'}=(x',y')$, and $\angle {xOP}=\alpha, \angle{POP'}=\theta$ and $||\vec OP||=r$, we can get the following equations
         $$
         \begin{cases}
         x=rcos\alpha\\\\
         y=rsin\alpha\\\\
         x'=rcos(\alpha+\theta)\\\\
         y'=rsin(\alpha+\theta)
         \end{cases}
         $$
         and then we can get
         $$
         \begin{cases}
         x'=xcos\theta-ysin\theta\\\\
         y'=xsin\theta+xcos\theta
         \end {cases}
         $$
         and get the coefficient to the matrix is $R_{\theta}$.

         And we can get the 
         $$
         R_{-\theta}=\left[ \begin {matrix} cos\theta&sin\theta\\\\-sin\theta&cos\theta\end{matrix}\right]=R_\theta^T
         $$
         Infact, if the $detM=1or-1$, we called $M$ is **Orthogonality Matrix **, and $M^{-1}=M^t$

      1. Scale(Non uniform)：Suppose $k_{axis}$ is the scale ratio, so the scale matrix is
         $$
         \left[ \begin {matrix}x'\\\\y' \end{matrix}\right]=
         \left[ \begin {matrix} k_x&0\\\\0&k_y\end{matrix}\right]
         \left[ \begin {matrix} x\\\\y\end{matrix}\right]
         $$

      2. Shear：Suppose horizontal shift is $0$ at $y=0$, horizontal shift is $a$ at $y=1$ and vertical shift is always $0$, so the shear matrix is
         $$
         \left[ \begin {matrix}x'\\\\y' \end{matrix}\right]=
         \left[ \begin {matrix} 1&a\\\\0&1\end{matrix}\right]
         \left[ \begin {matrix} x\\\\1\end{matrix}\right]
         $$

      3. Reflection: To mirror y-axis.
         $$
         \left[ \begin {matrix}x'\\\\y' \end{matrix}\right]=
         \left[ \begin {matrix} -1&0\\\\0&1\end{matrix}\right]
         \left[ \begin {matrix} x\\\\y\end{matrix}\right]
         $$

2. **Linear Transforms = Matrices (of the same dimension)**

3. Homogeneous coordinates

   0. Why homogeneous coordinates : 
      0. To represent the translation by **linear transforms**;
         0. The equations of translation
            $$
            \begin{cases}
            x'=x+t_x\\\\
            y'=y+t_y
            \end{cases}
            $$

         1. If keep the dimension, we only represent it in matrix form
            $$
            \left[ \begin {matrix}x'\\\\y' \end{matrix}\right]=
            \left[ \begin {matrix} a&b\\\\c&d\end{matrix}\right]
            \left[ \begin {matrix} x\\\\y\end{matrix}\right]+
            \left[ \begin {matrix} t_x\\\\t_y\end{matrix}\right]
            $$

         2. But we don't want to be this special case. So we import the homogeneous coordinates

            0. Add an extra coodinate (w-coordinate): 2D point =$(x,y,1)^T$ and 2D vector =$(x,y,0)^T$

            1. the the Matrix Representation of translations is 
               $$
               \left[ \begin {matrix}x'\\\\y'\\\\w' \end{matrix}\right]=
               \left[ \begin {matrix} 1&0&t_x\\\\0&1&t_y\\\\0&0&1\end{matrix}\right]
               \left[ \begin {matrix} x\\\\y\\\\1\end{matrix}\right]=
               \left[ \begin {matrix} x+t_x\\\\y+t_y\\\\1\end{matrix}\right]
               $$

         3. **Tradeoff**: We should consider the extra cost by importing the homogeneous coordinates, because **there is no free lunch in the world**.

      1. To distinguish the vector and the point( coordinate ).

         we have introduced the homogeneous coordinates, but why we should put the extra dimension to $1$ (in point) or $0$ (in vector)?

         Because the vector have the property — translation invariance. So we want, after the transformation, the vector won't be change.

         And the Valid operation if w-coordinate of result is 1 or 0

          0. vector + vector = vector;

          1. point - point = vector;

          2. point + vector = point ;

          3. point + point = Special Case

          4. Special Case: if the w-coordinate is not both 0 or 1, we let the point normalization. After the normalization, we can get a point. (In the Num 3 operation, we will get the mid point between 2 points). 
             $$
             \left[ \begin {matrix}x\\\\y\\\\w \end{matrix}\right]=\left[ \begin {matrix}\frac xw\\\\ \frac yw\\\\1 \end{matrix}\right],w\neq0
             $$

   2. Affine transformation（仿射变换）

      0. Affine map = linear map + translation. So using homogeneous coordinates, we can get

      $$
      \left[ \begin {matrix}x'\\\\y'\\\\w' \end{matrix}\right]=
      \left[ \begin {matrix} a&b&t_x\\\\c&d&t_y\\\\0&0&1\end{matrix}\right]
      \left[ \begin {matrix} x\\\\y\\\\1\end{matrix}\right]
      $$

      1. Transformation by homogeneous coordinates：Add another column and let the column assignment $(0,0,...,0,1)$
      2. Invers Transform $M^-1$, it map to the inverse matrix

4. Composing Transforms

   0. Suppose we want to rotate and translate the picture, we can get the 2 ways: The first is translation then rotation, the other is rotation then translation. **But** compare the two picture, we get the difference picture. So we should know that the transformation sequence/ordering is **matters**.

      Associate the matrix multiple and we can easily understand it. But note that martices are applied **right to left**.

   1. We can pre-multiply $n$ matrixs to obtain a single matrix representing combined transform, wich are important for performance (pre-multiply is faster).

5. Decomposing Complex Transforms

6. 3D Transformation

   0. Use homogeneous coordinates: 3D point =$(x,y,z,1)^T$ and 3D vector =$(x,y,z,0)^T$

   1. In general $(x,y,z,w),w\neq0$ is the 3D point 
      $$
      (\frac xw,\frac yw,\frac zw)
      $$

   2. And use $4\times4$ matrices for affine transformations（Other transformation is simliar to this case）
      $$
      \cdot \left[ \begin {matrix} x'\\\\y'\\\\z'\\\\1\end{matrix}\right]=
      \left[ \begin {matrix} a&b&c&t_x\\\\d&e&f&t_y\\\\g&h&i&t_z\\\\0&0&0&1\end{matrix}\right]
      \cdot \left[ \begin {matrix} x\\\\y\\\\z\\\\1\end{matrix}\right]
      $$

   3. Be careful this transformation is linear transformation then translation.

   4.  Rotate matrices around $x-$, $y-$ or $z-axis$  are
      $$
      R_x(\theta)=\left[ 
      \begin {matrix} 
      1&0&0&0
      \\\\0&cos\theta&-sin\theta&0
      \\\\0&sin\theta&cos\theta&0
      \\\\0&0&0&1
      \end{matrix}\right]
      \\\\
      R_y(\theta)=\left[ 
      \begin {matrix} cos\theta&0&sin\theta&0
      \\\\0&1&0&0
      \\\\-sin\theta&0&cos\theta&0
      \\\\0&0&0&1
      \end{matrix}\right]
      \\\\
      R_z(\theta)=\left[ 
      \begin {matrix} cos\theta&-sin\theta&0&0
      \\\\sin\theta&cos\theta&0&0
      \\\\0&0&1&0
      \\\\0&0&0&1
      \end{matrix}\right]
      $$
      we can notice a fact that the $R_y(\theta)$ is special, if you want to know more, review the "_coss product_" and you will know why this phenomenon will occur. 

   5. Euler angles: To compose any 3D rotation from $R_x,R_y,R_z$
      $$
      R_{xyz}(\alpha,\beta,\gamma)=R_x（\alpha）R_y（\beta）R_z（\gamma）
      $$
      And we often used in flight simulators : roll, pitch, yaw.（中文：偏航、俯仰和滚转）

      Althou the Euler angles can't avoid the Gimbal Lock（ a kind of deadlock ）, and it can't finish the smooth interpolation of sphere, but it can easily sovle the 3D rotation problem. So we omit it. （If you want to know more, you can google it） .

      0. **Rodrigues' Rotation Formula**: By angle $\alpha$ round axis $n$, $I$ is **Identity matrix**, and the last matrix we called **dual matrix**
         $$
         R(\vec n,\alpha)=cos(\alpha)I+(1-cos\alpha)\vec n \vec n^T+sin(\alpha)
         \left[ 
         \begin {matrix} 0&-n_z&n_y
         \\\\n_z&0&-n_x
         \\\\-n_y&n_x&0
         \end{matrix}\right]
         $$

      1. The method of **Quaternions（四元数）**is to solve the interpolation of the rotation. And we omis it in this Blog.

### Viewing Transformaton

0. View（视图）/ Camera transformation

   0. What is view transformation — associate the photo when we take.

      Generally, when we take a photo, we always do as follows:

      0. Find a good place and arrange the elments(Model transformation)
      1. Find a good _angle_ to put the camera(View transformation)
      2. Cheese(Projection transformation)

   1. How to perform view transformation?

      0. Define the camera: mark $\vec e$ as position, $\hat g$ as look-at/gaze direction and $\hat t$ as up direction(assuming perp. to look at)

      1. Key observation: If the camera and all objects move together, the photo will be the same. So we always transform the camera to the origin, up at $Y$, look at the $-Z$, and transform the objects along with the camera.

      2. Transform the camera by $M_{view}$, so it's located a the origin, up at $Y$, look at $-Z$. In math descibe, we called 

         0. Translates $\vec e$ to origin;

         1. Rotates $\hat g$ to $-Z$;

         2. Rotates $\hat t$ to $Y$;

         3. Rotatse $\hat g \times \hat t$ to $X$

         4. And we write $M_{view}=R_{view}T_{view}$, then translate $\vec e$ to origin
            $$
            T_{view}=\left[\begin{matrix} 
            1&0&0&-x_e
            \\\\
            0&1&0&-y_e
            \\\\
            0&0&1&-z_e
            \\\\
            0&0&0&1
            \end{matrix}\right]
            $$
            Then rotate $\hat g$  to $-Z$, $\hat t$ to $Y$, $(g\times t)$ to $X$, we find that it hard to caculate, consider the Orthogonality Matrix, we can find the $R_{view}^{-1}$ is easy to caculate.

            Just inverse the rotation $X$ to $(g\times t)$, $Y$ to $\hat t$ and $Z$ to $-\hat g$, then 
            $$
            R_{view}^{-1}=\left[\begin{matrix} 
            x_{\hat g\times \hat t}&x_t&x_{-g}&0
            \\\\
            y_{\hat g\times \hat t}&y_t&y_{-g}&0
            \\\\
            z_{\hat g\times \hat t}&z_t&z_{-g}&0
            \\\\
            0&0&0&1
            \end{matrix}\right]
            $$
            Because of the property $M^{-1}=M^t$, we can get 
            $$
            R_{view}=
            \left[\begin{matrix} 
            x_{\hat g\times \hat t}&y_{\hat g\times \hat t}&z_{\hat g\times \hat t}&0
            \\\\
            x_t&y_t&z_t&0
            \\\\
            x_{-g}&y_{-g}&z_{-g}&0
            \\\\
            0&0&0&1
            \end{matrix}\right]
            $$
            So this is View Transformation Matrix.

      3. Summery 

         0. Transform objects together with the camera
         1. Until camera's at the origin, up at $Y$, look at $-Z$

      4. Also known as Model/View Transformation

1. Projection transformation: 3D to 2D

   0. Orthographic projection

   1. Perspective（透视） projection

## 2. Rasterization



## 3. Shading 



## 4. Geometry



## 5. Ray Tracing



## 6. Materials and Appearances



## 7. Advanced Topics in rendering



## 8. Cameras, Lenses and Light Fields



## 9. Color and Perception



## 10. Animation

