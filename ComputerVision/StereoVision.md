# 立体视觉（Stereo Vision）
---
# 1. 单目散斑结构光（Single-View Structured Light）
## 1.1 原理
<p align="center">
<img src="https://developer-orbbec-oss.oss-cn-shenzhen.aliyuncs.com/images/c35783fb-17e3-45fe-aec4-5c1d8ef269cd.png" height = "450">
<br>图1.1.1 单目散斑结构光原理
</p>

## 1.2 参考图
* 参考图：在垂直相机光轴的某一**固定距离**拍摄，并经过**极线校正**后的图像(也可以引入参考平面方程，可避免调垂直相机光轴位置和距离)
* 为什么不用DOE设计图（这样的话原理上更接近双目视觉）：参考图包含了系统的畸变信息，能更好地匹配实时图，也免去了对投射系统畸变建模的复杂过程
* 在3D视觉系统中，深度$z$与视差$\delta$成反比： $z = \frac{f \cdot B}{\delta}$，其中$f$为焦距，$B$为基线长度，将视差看成相对值，距离也可通过相对于参考距离计算得到。参考图1.2.1。
  ```math
  \Delta =\delta_1 - \delta_0= \frac{f \cdot B}{z_1} - \frac{f \cdot B}{z_0} = f \cdot B \cdot \frac{z_0 - z_1}{z_0 \cdot z_1}
  \implies
  z_1 = \frac{f \cdot B \cdot z_0}{f \cdot B + \Delta \cdot z_0}
  ```
* 问题：参考图和实时图像都是同一个相机拍摄的，需要对参考图做极线校正吗？
* 回答：不存在畸变的前提下，参考图与实时图的极线其实就是optical center与对应点的连线(不对！)
  
<p align="center">
<img src="https://i-blog.csdnimg.cn/blog_migrate/8a6ce8360b49dd42ddac20aef6000e2a.png#pic_center" width = "800">
<br>图1.2.1 参考平面与实时图的视差关系
<br>
<img src="https://tse1.mm.bing.net/th/id/OIP.Le1xFiqJ62hC9ZdFvbYe9QAAAA?rs=1&pid=ImgDetMain&o=7&rm=3" width = "800">
<br>图1.2.2 实时图-参考图的块匹配
</p> 

## 1.3 标定
* [方法1](https://blog.csdn.net/memmolo/article/details/136760798): 基于圆点阵标定板，将散斑投射到白色高反圆点上
  <p align="center">
  <img src="https://i-blog.csdnimg.cn/blog_migrate/7d167846a869a4ddf2dcc6debcfbbace.png#pic_center" height = "500">
  <br>图1.3.1 单目散斑结构光标定的一种方法
  </p>
---
# 2. 对极几何（Epipolar Geometry）
## 2.1 点-线-面的性质
### 2.1.1 2D空间表示
- **平面点：** $\overrightarrow{x}=(x,y)^T$ ，齐次表示： $\overrightarrow{x}=(x,y,1)^T$
- **平面线：** $ax+by+c=0$，向量表示：$\overrightarrow{l}=(a,b,c)^T$，其中$\overrightarrow{n}=(a,b)$$为线的法向量

> [!NOTE] 
> 点的齐次坐标表示为$\overrightarrow{x}=(x,y,w)^T$ ，其中$w$是一个非零的缩放因子。对于一个点的齐次坐标可以通过除以$w$来得到其对应的非齐次坐标，即$(\frac{x}{w}, \frac{y}{w})$。当$w=0$时，表示一个点在无穷远处。

### 2.1.2 2D空间性质
- **点在直线上：** $\overrightarrow{x}^T\overrightarrow{l}=0$，注意$\overrightarrow{x}$是齐次坐标（其实就是直线方程表达式）
- **线-线的交点：** $\overrightarrow{x}=\overrightarrow{l}_1 \times \overrightarrow{l}_2$，注意$\overrightarrow{l}$是向量表示
- **两点确定的直线：** $\overrightarrow{l}=\overrightarrow{x}_1 \times \overrightarrow{x}_2$，注意$\overrightarrow{x}$是齐次坐标

### 2.1.3 3D空间表示
- **空间点：** $\overrightarrow{X}=(X,Y,Z)^T$，齐次表示： $\overrightarrow{X}=(X,Y,Z,1)^T$
- **空间线：** $\overrightarrow{L}=(\overrightarrow{P},\overrightarrow{V})$，其中$\overrightarrow{P}$为线上的一个点，$\overrightarrow{V}$为线的方向向量
- **空间面：** $aX+bY+cZ+d=0$，向量表示：$\overrightarrow{S}=(a,b,c,d)^T$，其中$\overrightarrow{n}=(a,b,c)$为面的法向量

### 2.1.4 3D空间性质
- **点在面上：** $\overrightarrow{X}^T\overrightarrow{S}=0$，注意$\overrightarrow{X}$是齐次坐标（其实就是平面方程表达式）
- **两点确定的面：** $\overrightarrow{S}=\overrightarrow{X}_1 \times \overrightarrow{X}_2$，注意$\overrightarrow{X}$是齐次坐标
- **线-线的交面：** $\overrightarrow{S}=\overrightarrow{L}_1 \times \overrightarrow{L}_2$，其中$\overrightarrow{L}$是向量表示

## 2.2 基本矩阵$F$（Fundamental Matrix）
### 2.2.1 基本矩阵的定义
- **定义：** $F$是一个秩为2的3x3矩阵，如果一个3维空间点$P$在第一、第二幅视图中的像分别为$\overrightarrow{x}$和$\overrightarrow{x}'$，则这两个图像点满足关系
  $$\overrightarrow{x}'^T F \overrightarrow{x} = 0$$
  - **对极点（Epipole）：** 连接两相机光心的直线（基线）与像平面的交点。（图中$e_l$和$e_r$点）
  - **对极平面（Epipolar Plane）：** 包含两个相机光心和空间点$P$的平面。（图中$PO_lO_r$平面）
  - **对极线（Epipolar Line）：** 对极平面与图像平面的交线。
    <p align="center">
    <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/epipolar_geometry.png" width = "450">
    <br>对极几何
    </p>
  - **性质：** $F$是一个秩为2的矩阵，具有7个自由度，可以通过至少7对匹配点来估计。对于图像中的一个点$\overrightarrow{x}$，其对应的对极线可以通过$F\overrightarrow{x}$计算得到。

### 2.2.2 基本矩阵的推导证明
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/epipolar_geometry_book_1.png" width = "600">
<br>对极几何
</p>

- **代数推导：**
  - STEP1：空间点$X$在第一、第二幅视图中的像分别为 $\overrightarrow{x}$ 和 $\overrightarrow{x}'$ ，则有
    $$\overrightarrow{x} = K [I | 0] \overrightarrow{X}$$
    $$\overrightarrow{x}' = K' [R | t] \overrightarrow{X}$$
    其中 $K$ 和 $K'$ 是两相机的内参矩阵， $R$ 和 $t$ 是两相机之间的旋转和平移关系。
  - STEP2：将$\overrightarrow{X}$表示为$\overrightarrow{x}$的函数，即$\overrightarrow{X} = K^{-1} \overrightarrow{x}$，代入第二幅视图 的像方程中，得到
    $$\overrightarrow{x}' = K' [R | t] K^{-1} \overrightarrow{x}$$
  - STEP3：定义基本矩阵$F$为$F = K' [R | t] K^{-1}$，则有
    $$\overrightarrow{x}'^T F \overrightarrow{x} = \overrightarrow{x}'^T K' [R | t] K^{-1} \overrightarrow{x} = 0$$
    其中$\overrightarrow{x}'^T K' [R | t] K^{-1} \overrightarrow{x}$表示$\overrightarrow{x}'$与$\overrightarrow{x}$之间的关系，满足对极几何约束.
- **几何推导：**
  - STEP1：$H_\pi$是两幅图像上的点$x$和$x'$通过平面$\pi$的转移映射（单应矩阵），则有
    $$\overrightarrow{x}' = H_\pi \overrightarrow{x}$$
  - STEP2：给定点$x'$，通过$x'$和极点$e'$的对极线$l'$为
    $$\overrightarrow{l'} = \overrightarrow{e'} \times \overrightarrow{x'} = [\overrightarrow{e'}]_\times \overrightarrow{x'}$$
  - STEP3：将$H_\pi$代入对极线方程中，得到
    $$\overrightarrow{l'} = [\overrightarrow{e'}]_\times H_\pi \overrightarrow{x}$$
    定义基本矩阵$F$为$F = [\overrightarrow{e'}]_\times H_\pi$，则有
    $$\overrightarrow{l'} = F \overrightarrow{x}$$
    $x'$是$l'$上的点，有
    $$\overrightarrow{x'}^T \overrightarrow{l'} = \overrightarrow{x'}^T F \overrightarrow{x} = 0$$
- **总结：** 基本矩阵$F$可以通过两种方式计算得到：
  - 由内外参计算$F$
    $$F = K' [R | t] K^{-1}$$
  - 由单应矩阵和极点计算$F$
    $$F = [\overrightarrow{e'}]_\times H_\pi$$
> [!NOTE]
> 叉乘可以表示为一个3x3反对称矩阵与向量的乘积：
>  $$\overrightarrow{a} \times \overrightarrow{b} = [\overrightarrow{a}]_\times \overrightarrow{b}$$
>  其中$[\overrightarrow{a}]_\times$是由$\overrightarrow{a}$构成的反对称矩阵：
>  $$[\overrightarrow{a}]_\times = \begin{bmatrix}
>  0 & -a_z & a_y \\
>  a_z & 0 & -a_x \\
>  -a_y & a_x & 0
>  \end{bmatrix}$$

### 2.2.3 基本矩阵的性质
- $F$是自由度为7的秩2齐次矩阵
- **点对应关系**：如果$x$和$x'$是同一空间点在两幅图像中的对应点，则满足$\overrightarrow{x}'^T F \overrightarrow{x} = 0$。
- **对极线**
  - $\overrightarrow{l'}=F\overrightarrow{x}$是对应于$x$的对极线，所有对应于$x$的点$x'$都在$l'$上。
  - $\overrightarrow{l}=F^T\overrightarrow{x'}$是对应于$x'$的对极线，所有对应于$x'$的点$x$都在$l$上。
- **对极点**
  - $F\overrightarrow{e}=0$，其中$\overrightarrow{e}$是左图的对极点。
  - $F^T\overrightarrow{e'}=0$，其中$\overrightarrow{e'}$是右图的对极点。
  