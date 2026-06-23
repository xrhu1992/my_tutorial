# 多视图几何（Multi-View Geometry）
---

# 1. 点-线-面的表示与性质（Point-Line-Surface Representation and Properties）
## 1.1 2D平面点-线表示
- **平面点：** $\overrightarrow{x}=(x,y)^T$ ，齐次表示： $\overrightarrow{x}=(x,y,1)^T$
- **平面线：** $ax+by+c=0$，向量表示：$\overrightarrow{l}=(a,b,c)^T$，其中$\overrightarrow{n}=(a,b)$$为线的法向量

> [!NOTE] 
> 点的齐次坐标表示为$\overrightarrow{x}=(x,y,w)^T$ ，其中$w$是一个非零的缩放因子。对于一个点的齐次坐标可以通过除以$w$来得到其对应的非齐次坐标，即$(\frac{x}{w}, \frac{y}{w})$。当$w=0$时，表示一个点在无穷远处。

## 1.2 2D平面点-线性质
- **点在直线上：** $\overrightarrow{x}^T\overrightarrow{l}=0$，注意$\overrightarrow{x}$是齐次坐标（其实就是把点$\overrightarrow{x}$代入直线方程表达式）
- **线-线的交点：** $\overrightarrow{x}=\overrightarrow{l}_1 \times \overrightarrow{l}_2$，注意$\overrightarrow{l}$是向量表示
- **两点确定的直线：** $\overrightarrow{l}=\overrightarrow{x}_1 \times \overrightarrow{x}_2$，注意$\overrightarrow{x}$是齐次坐标

## 1.3 3D空间点-线-面表示
- **空间点：** $\overrightarrow{X}=(X,Y,Z)^T$，齐次表示： $\overrightarrow{X}=(X,Y,Z,1)^T$
- **空间线：** $\overrightarrow{L}=(\overrightarrow{P},\overrightarrow{V})$，其中$\overrightarrow{P}$为线上的一个点，$\overrightarrow{V}$为线的方向向量
- **空间面：** $aX+bY+cZ+d=0$，向量表示：$\overrightarrow{S}=(a,b,c,d)^T$，其中$\overrightarrow{n}=(a,b,c)$为面的法向量

## 1.4 3D空间点-线-面性质
- **点在面上：** $\overrightarrow{X}^T\overrightarrow{S}=0$，注意$\overrightarrow{X}$是齐次坐标（其实就是点$\overrightarrow{X}$代入平面方程表达式）
---

# 2. 对极几何（Epipolar Geometry）
## 2.1 基本矩阵$F$（Fundamental Matrix）
### 2.1.1 基本矩阵的定义
- **定义：** $F$是一个秩为2的3x3矩阵，如果一个3维空间点$P$在第一、第二幅视图中的像分别为$\overrightarrow{x}$和$\overrightarrow{x}'$，则这两个图像点满足关系
  $$
  \overrightarrow{x}'^T F \overrightarrow{x} = 0
  $$
  - **对极点（Epipole）：** 连接两相机光心的直线（基线）与像平面的交点。（图中$e_l$和$e_r$点）
  - **对极平面（Epipolar Plane）：** 包含两个相机光心和空间点$P$的平面。（图中$PO_lO_r$平面）
  - **对极线（Epipolar Line）：** 对极平面与图像平面的交线。
    <p align="center">
    <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/epipolar_geometry.png" width = "400">
    <br>对极几何
    </p>
  - **性质：** $F$是一个秩为2的矩阵，具有7个自由度，可以通过至少7对匹配点来估计。对于图像中的一个点$\overrightarrow{x}$，其对应的对极线可以通过$F\overrightarrow{x}$计算得到。

### 2.1.2 基本矩阵的推导证明
- **代数推导：**
  - 空间点$P$在第一、第二相机中的空间坐标分别为 $\overrightarrow{X}$ 和 $\overrightarrow{X}'$ （注意是非齐次空间坐标），则有
    $$
    \overrightarrow{X}' = R\overrightarrow{X} + \overrightarrow{t}
    $$
    其中 $R$ 和 $t$ 是两相机之间的旋转和平移关系。（注意 $R$ 和 $t$ 是由第一相机转到第二相机，在第二相机视角下的坐标）
  - 两边同时叉乘 $\overrightarrow{t}$ ，得到由 $\overrightarrow{X}$ 表示的对极线$l$，则有（注意到$\overrightarrow{t} \times \overrightarrow{t}=0$）
    $$
    \overrightarrow{t} \times \overrightarrow{X}' = \overrightarrow{t} \times R\overrightarrow{X} + \overrightarrow{t} \times \overrightarrow{t} = \overrightarrow{t} \times R\overrightarrow{X}
    $$
  - 两边同时左乘 $\overrightarrow{X}'^T$ ，得到
    $$
    \overrightarrow{X}'^T(\overrightarrow{t} \times \overrightarrow{X}') = \overrightarrow{X}'^T(\overrightarrow{t} \times R\overrightarrow{X})
    $$
    注意到等式左边 $\overrightarrow{X}'^T(\overrightarrow{t} \times R\overrightarrow{X})$ 中，$\overrightarrow{t} \times R\overrightarrow{X}$ 表示与对极平面垂直的向量，而向量 $\overrightarrow{X}'$ 与对极平面垂直，所以 $\overrightarrow{X}'^T(\overrightarrow{t} \times R\overrightarrow{X}) = 0$。由此可得
    $$\overrightarrow{X}'^T(\overrightarrow{t} \times R\overrightarrow{X})=0$$
    写成矩阵型式为
    $$\overrightarrow{X}'^T [\overrightarrow{t}] _\times R\overrightarrow{X} = 0$$
  - 令本质矩阵为 $E = [\overrightarrow{t}] \times R$，则有
    $$\overrightarrow{X}'^T E \overrightarrow{X} = 0$$
  - 假设第一、第二相机的内参矩阵为$K$和$K'$，空间点$P$在相机中的像素坐标分别为 $\overrightarrow{x}$ 和 $\overrightarrow{x}'$ ，有
  $$
  \overrightarrow{x} = KX \implies \overrightarrow{X} = K^{-1} \overrightarrow{x} \\
  \overrightarrow{x}' = K'X' \implies \overrightarrow{X}' = K'^{-1} \overrightarrow{x}'
  $$
  代入本质矩阵方程可得
  $$
  \overrightarrow{X}'^T [\overrightarrow{t}] _\times R\overrightarrow{X} = \overrightarrow{x}'^T K'^{-T}  [\overrightarrow{t}] _\times RK^{-1} \overrightarrow{x}
  $$
  - 令基础矩阵为 $F = K'^{-T}  [\overrightarrow{t}] _\times RK^{-1}$，则有
  $$
  \overrightarrow{x}'^T F \overrightarrow{x} = 0
  $$

- **几何推导：**
  - $H_\pi$是两幅图像上的点$x$和$x'$通过诱导平面$\pi$的转移映射（单应矩阵），则有
    $$
    \overrightarrow{x}' = H_\pi \overrightarrow{x}
    $$
  - 给定点$x'$，通过$x'$和极点$e'$的对极线$l'$为
    $$
    \overrightarrow{l'} = \overrightarrow{e'} \times \overrightarrow{x'} = [\overrightarrow{e'}]_\times \overrightarrow{x'}
    $$
  - 将$H_\pi$代入对极线方程中，得到
    $$
    \overrightarrow{l'} = [\overrightarrow{e'}]_\times H_\pi \overrightarrow{x}
    $$
    定义基本矩阵$F$为$F = [\overrightarrow{e'}]_\times H_\pi$，则有
    $$
    \overrightarrow{l'} = F \overrightarrow{x}
    $$
    $x'$是$l'$上的点，有
    $$
    \overrightarrow{x'}^T \overrightarrow{l'} = \overrightarrow{x'}^T F \overrightarrow{x} = 0
    $$
  <p align="center">
  <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/epipolar_geometry_book_1.png" width = "500">
  <br>基础矩阵的几何推导</p>

- **总结：** 基本矩阵$F$可以通过两种方式计算得到：
  - 由内外参计算$F$
    $$F = K'^{-T}  [\overrightarrow{t}] _\times RK^{-1}$$
  - 由单应矩阵和极点计算$F$
    $$F = [\overrightarrow{e'}]_\times H_\pi$$

> [!NOTE]
> 叉乘可以表示为一个3x3反对称矩阵与向量的乘积：
>  $$\overrightarrow{a} \times \overrightarrow{b} = [\overrightarrow{a}]_\times \overrightarrow{b}$$
>  其中$[\overrightarrow{a}]_\times$是由$\overrightarrow{a}$构成的反对称矩阵：
>  $$
> [\overrightarrow{a}]_\times = \begin{bmatrix}
>  0 & -a_z & a_y \\
>  a_z & 0 & -a_x \\
>  -a_y & a_x & 0
>  \end{bmatrix}
> $$

### 2.1.3 基本矩阵的性质
- $F$是自由度为7的秩2齐次矩阵
- **点对应关系**：如果$x$和$x'$是同一空间点在两幅图像中的对应点，则满足$\overrightarrow{x}'^T F \overrightarrow{x} = 0$。
- **对极线**
  - $\overrightarrow{l'}=F\overrightarrow{x}$是对应于$x$的对极线，所有对应于$x$的点$x'$都在$l'$上。
  - $\overrightarrow{l}=F^T\overrightarrow{x'}$是对应于$x'$的对极线，所有对应于$x'$的点$x$都在$l$上。
- **对极点**
  - $F\overrightarrow{e}=0$，其中$\overrightarrow{e}$是左图的对极点。
  - $F^T\overrightarrow{e'}=0$，其中$\overrightarrow{e'}$是右图的对极点。
- **对极线的单应：** 对极线在两幅图像之间存在单应关系，即如果$l$和$l'$分别是图像中的对极线，则有：
  $$
  \overrightarrow{l'} = F[\overrightarrow{e}]_\times \overrightarrow{l}
  \\
  \overrightarrow{l} = F^T[\overrightarrow{e'}]_\times \overrightarrow{l'}
  $$
  <p align="center">
  <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/epipolar_line_book.png" width = "360">
  <br>对极线的单应</p>
  
## 2.2 极线校正（Epipolar Rectification）
[参考《Learning OpenCV3》](https://github.com/jash-git/Learning-OpenCV-3/blob/master/Learning%20OpenCV%203.pdf)
### 2.2.1 理想的双目三角关系
- **理想的双目三角关系：**
  - 两相机成像平面共面（Coplanar），焦距相同$f_l=f_r$，两光轴平行（Parallel）并且与基线垂直（Perpendicular）。本质：极点无穷远
  - 像素行对其（Row-Aligned），方便立体匹配（Stereo Matching）。
  - 理想关系下其三角几何关系可描述为：
  $$
  Z=\frac{f_l f_r T}{f_l x_r - f_r x_l} \quad \text{或} \quad Z=\frac{f T}{x_r - x_l}
  $$

- **极线校正的目的：** 通过对图像进行单应变换，使得两幅图像满足上述理想的三角几何关系，从而简化立体匹配问题。校正后的图像中，对极线与图像行平行，且对应点在同一行上（匹配点的y坐标相同）。
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/epipolar_rectification2.png" height = "250">
<img src="  https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/epipolar_rectification1.png" height = "250">
<br>理想的双目三角关系 & 极线校正</p>

### 2.2.2 Bouguet算法（公式推导有误，待修正。。。）
- **相机坐标系视角（左相机）**
- **核心思想：** 最小化重投影畸变（校正后图像变化最小）

- **STEP 1 - 使左右相机光轴平行：** 将两相机的旋转矩阵$R_{l2r}$分解成两部分$r_l$和$r_r$，分别使左右相机旋转一半。可使用Rodrigues变换表示，即：
  $$\begin{aligned}
  V_{l2r} &= \text{Rodrigues}(R_{l2r}) \\
  r_r &= \text{Rodrigues}(\frac{1}{2} V_{l2r}) \\
  r_l &= \text{Rodrigues}(\frac{1}{2} V_{l2r})
  \end{aligned}$$
  > [!NOTE]
  > 1. 这一步看起来有点多此一举了，实际上在Fusiello算法中省略了这一步，直接将两相机旋转到新坐标系下，而非两次旋转。这样做的目的是为了使得两相机旋转的程度相同，保证校正后的图像变化最小，但实际应用中可以通过修改内参矩阵的fx和fy来达到相似的效果。
  > 2. 需要注意，旋转后相机外参的旋转矩阵$R$和平移矩阵$T$也需要相应地进行变换才能继续应用到后续步骤中。（蝴蝶书中对此未作说明和推导，容易误导）

- **STEP 2 - 使左右相机光轴垂直于基线：** 以基线方向为x轴建立一个新的坐标系，并构造旋转矩阵，使得左右相机的光轴垂直于基线，极点无穷远
  $$R = [\overrightarrow{e_1}, \overrightarrow{e_2}, \overrightarrow{e_3}]^T$$
  - $\overrightarrow{e_1}$为基线方向，即
  $$
  \overrightarrow{e_1}=\frac{\overrightarrow{T}}{\|\overrightarrow{T} \|}
  $$
  - $\overrightarrow{e_2}$垂直于左相机光轴和基线的平面，即
  $$\begin{aligned}
  \overrightarrow{e} &= [0,0,1]^T \times [Tx,Ty,Tz]^T \\ 
  &= [-Ty,Tx,0]^T \\ 
  \overrightarrow{e_2} &= \frac{\overrightarrow{e}}{\|\overrightarrow{e} \|}
  \end{aligned}$$
  - $\overrightarrow{e_3}$为$\overrightarrow{e_1}$和$\overrightarrow{e_2}$的叉积
  $$
  \overrightarrow{e_3} = \overrightarrow{e_1} \times \overrightarrow{e_2}
  $$
  - 得到的旋转矩阵$R$是将新坐标系下的点转换到左相机坐标系的旋转矩阵，对其取逆（或转置-单位正交阵的性质）即可得到将左相机坐标系转换到新坐标系的旋转矩阵$R_{rect}$
  $$\begin{aligned}
  R_{rect} &= R^{-1}=R^T \\ 
  &= \begin{bmatrix}
     \overrightarrow{e_1}^T \\
     \overrightarrow{e_2}^T \\
     \overrightarrow{e_3}^T
     \end{bmatrix}
  \end{aligned}$$
> [!NOTE] 
> 为了确保新的坐标系与原相机坐标系方向大致相同，需注意使 $e_1.x>0,e_2.y>0,e_3.z>0$

- **STEP 3- 构建新的相机内参矩阵：** 为了使左右相机平面共面且行对其，需要使左右相机内参矩阵相等，为此构建新的相机内参矩阵$M_{rect}$
  - 在新的坐标系下任意空间点P，其在左右相机的像素坐标分别为
  $$\begin{aligned}
  P_l =M_{rect,l} \dot {P_l} \\
  P_r =M_{rect,r} \dot {P_r}
  \end{aligned}$$



- **STEP 4 - 应用旋转矩阵：** 将得到的旋转矩阵$R_{rect}$应用于两幅图像，完成极线校正。
  - 左右相机的旋转矩阵分别为
  $$
  R_l = R_{rect} r_l \\
  R_r = R_{rect} r_r
  $$
  - 校正后的内参矩阵可以选择为两相机内参的平均值，即$K_{rect} = \frac{K_l + K_r}{2}$。
  - 最终得到的校正后相机参数为：
  $$\begin{aligned}
  P_l &= K_{rect} [R_l | t_l] \\
  P_r &= K_{rect} [R_r | t_r]
  \end{aligned}$$

### 2.2.3 Fusiello算法
> [A Compact Algorithm for Rectification of Stereo Pairs]()

待补充。。。

--- 
# 3. 三角测量（Triangulation）
> [《多视图几何》-Chapter-12]()
## 3.1 双目系统三角测量（Stereo Triangulation）
### 3.1.1 双目系统模型
设双目系统的相机参数分别为$K_1$和$K_2$，像素的齐次坐标分别为$x_1=[u_1,v_1,1]^T$和$x_2=[u_2,v_2,1]^T$，外参矩阵为$R_{12}$和$t_{12}$，摄像机矩阵分别为$P_1$和$P_2$，空间点在主相机1的坐标系下的齐次坐标为$X=[x,y,z,1]^T$，则有
$$ \begin{aligned}
z_{c1}\begin{bmatrix}u_1\\v_1\\1\end{bmatrix} &= K_1 [I | 0]X = P_1 X \\
z_{c2}\begin{bmatrix}u_2\\v_2\\1\end{bmatrix} &= K_2 [R_{12} | t_{12}]X = P_2 X \\
\end{aligned}$$

### 3.1.2 二维匹配点的线性三角测量
> [OpenCV三角测量重建triangulatePoints原理解析](https://blog.csdn.net/weixin_43956164/article/details/124266267)
- **核心思想：** 已知双目匹配点的像素位置，利用双目系统的空间关系，求解出空间点在相机坐标系下的空间坐标。
- **适用场景：** 通过二维匹配获得匹配点对，如利用特征匹配进行稀疏重建。对应于OpenCV中的`cv::triangulatePoints()`函数。
- **推导：** 设摄像机矩阵$P=[\mathbf{p_1};\mathbf{p_2};\mathbf{p_3}]$，像素的齐次坐标$\overrightarrow{x}=[u,v,1]^T$，空间点在主相机坐标系下的齐次坐标$\overrightarrow{X}=[x,y,z,1]^T$
  $$
  z_c\overrightarrow{x}=P\overrightarrow{X} \\ 
  z_c\begin{bmatrix}u\\v\\1\end{bmatrix}
  =P\overrightarrow{X}
  =\begin{bmatrix}\mathbf{p_1} \\ \mathbf{p_2} \\\mathbf{p_3}\end{bmatrix}\overrightarrow{X}
  =\begin{bmatrix}\mathbf{p_1}\overrightarrow{X} \\ \mathbf{p_2}\overrightarrow{X} \\\mathbf{p_3}\overrightarrow{X}\end{bmatrix}
  =\mathbf{p_3}\overrightarrow{X}\begin{bmatrix}\frac{\mathbf{p_1}\overrightarrow{X}}{\mathbf{p_3}\overrightarrow{X}} \\ \frac{\mathbf{p_2}\overrightarrow{X}}{\mathbf{p_3}\overrightarrow{X} } \\1\end{bmatrix}\\
  \Downarrow \\
  \begin{bmatrix}u\\v\end{bmatrix}
  =\begin{bmatrix}\frac{\mathbf{p_1}\overrightarrow{X}}{\mathbf{p_3}\overrightarrow{X}} \\ \frac{\mathbf{p_2}\overrightarrow{X}}{\mathbf{p_3}\overrightarrow{X} } \end{bmatrix}\\
  \Downarrow \\
  \begin{bmatrix}u\\v\end{bmatrix}
  -\begin{bmatrix}\frac{\mathbf{p_1}\overrightarrow{X}}{\mathbf{p_3}\overrightarrow{X}} \\ \frac{\mathbf{p_2}\overrightarrow{X}}{\mathbf{p_3}\overrightarrow{X} } \end{bmatrix}
  =\begin{bmatrix}u-\frac{\mathbf{p_1}\overrightarrow{X}}{\mathbf{p_3}\overrightarrow{X}} \\ v-\frac{\mathbf{p_2}\overrightarrow{X}}{\mathbf{p_3}\overrightarrow{X} } \end{bmatrix}=0
  $$
  等式两边同时乘以$\mathbf{p_3}\overrightarrow{X}$，可得
  $$
  \begin{bmatrix}u\mathbf{p_3}\overrightarrow{X}-\mathbf{p_1}\overrightarrow{X} \\ v\mathbf{p_3}\overrightarrow{X}-\mathbf{p_2}\overrightarrow{X} \end{bmatrix}
  =\begin{bmatrix}u\mathbf{p_3}-\mathbf{p_1} \\ v\mathbf{p_3}-\mathbf{p_2} \end{bmatrix}\overrightarrow{X}=0\\
  \Downarrow
  $$
  
  $$\begin{equation}
  \begin{bmatrix}u\mathbf{p_3}-\mathbf{p_1} \\ v\mathbf{p_3}-\mathbf{p_2} \end{bmatrix}\overrightarrow{X}=0
  \tag{3.1}
  \end{equation}$$
  将双目相机$P$和$P'$的两个匹配点$\overrightarrow{x}=[u,v,1]^T$和$\overrightarrow{x'}=[u',v',1]^T$代入等式，可得到由4个方程组成的超静定方程组
  $$
  \begin{bmatrix}
  u\mathbf{p_3}-\mathbf{p_1} \\
  v\mathbf{p_3}-\mathbf{p_2} \\
  u'\mathbf{p_3'}-\mathbf{p_1'} \\
  v'\mathbf{p_3'}-\mathbf{p_2'} \\
  \end{bmatrix}
  \begin{bmatrix}x\\y\\z\\1\end{bmatrix}=0
  $$
  使用SVD求最小二乘解，可得到空间点在主相机坐标系下的齐次坐标
  $$
  X=\begin{bmatrix}x\\y\\z\\1\end{bmatrix}=\begin{bmatrix}x_0/x_3\\x_1/x_3\\x_2/x_3\\x_3/x_3\end{bmatrix}
  $$
  对于存在多个不确定匹配点的场景，还可以利用反投影误差来选择最优的匹配点对。
  
> [!NOTE]
> 在《多视图几何》书中，使用共线的向量叉乘等于0向量这一性质来简化推导，即
> $$z_c\begin{bmatrix}u\\v\\1\end{bmatrix}=P\begin{bmatrix}x\\y\\z\\1\end{bmatrix}\\
> z_c\overrightarrow{x}=P\overrightarrow{X}$$
> $\overrightarrow{x}$ 与 $P\overrightarrow{X}$ 是共线（线性相关）的，所以
> $$\overrightarrow{x} \times (P\overrightarrow{X}) = 0$$
> 其中$\overrightarrow{x}=[u,v,1]^T$和$\overrightarrow{X}=[x,y,z,1]^T$，$P=[\mathbf{p_1};\mathbf{p_2};\mathbf{p_3}]$是摄像机矩阵，$z_c$ 是在相机坐标系下的空间点的z坐标。
> 将$\overrightarrow{x}$的叉乘写成反对称矩阵型式有
> $$
> \overrightarrow{x} \times (P\overrightarrow{X}) = \begin{bmatrix}
> 0 & -1 & v \\
> 1 & 0 & -u \\
> -v & u & 0
> \end{bmatrix}
> \begin{bmatrix}
> \mathbf{p_1}  \\ \mathbf{p_2}  \\\mathbf{p_3}
> \end{bmatrix}
> \begin{bmatrix}x\\y\\z\\1\end{bmatrix} = 
> \begin{bmatrix}
> -\mathbf{p_2}+v\mathbf{p_3} \\
> \mathbf{p_1}-u\mathbf{p_3}  \\
> -v\mathbf{p_1}+u\mathbf{p_2} \\
> \end{bmatrix}
> \begin{bmatrix}x\\y\\z\\1\end{bmatrix}=0
> $$
> 等式右边第三行与第一二行线性相关，所以可以将第三行消去，得到
> $$
> \begin{bmatrix}
> -\mathbf{p_2}+v\mathbf{p_3} \\
> \mathbf{p_1}-u\mathbf{p_3}  \\
> \end{bmatrix}
> \begin{bmatrix}x\\y\\z\\1\end{bmatrix}=0
> $$
> 该方程与之前推导的公式(3.1)相同。

### 3.1.3 最小化几何误差（Minimization of Geometric Error）
双目匹配测量点往往是一组不满足对极几何约束的含噪声点对 $x \leftrightarrow x'$ ，实际对应图像点的正确值应该是在测量点附近的点 $\widehat{x} \leftrightarrow \widehat{x}'$ ,且精确满足对极几何约束 $\widehat{x}'^T F \widehat{x}=0$。为了计算这样的点对，寻找最小化误差函数（等价于最小化 $\widehat{X}$ 的反投影误差函数）
$$\begin{aligned}
&C(\mathbf{x},\mathbf{x'}) = d(\mathbf{x},\mathbf{\widehat{x}})+d(\mathbf{x'},\mathbf{\widehat{x}'}) \\
and:\quad &\mathbf{\widehat{x}'}^T F \mathbf{\widehat{x}} = 0
\end{aligned}$$
可使用最大似然估计(MLE) 或 Levenberg-Marquardt 或 Sampson 算法来最小化误差函数。
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/minimization_of_geometric_error.png" width = "450">
<br>最小化几何误差</p>


