# 多视图几何（Multi-View Geometry）
---
# 1. 单视图几何（Single-View Geometry）
## 1.1 消影点（Vanishing Point）
- **定义：** 图像中平行于某一方向的线段在图像中交汇的点。对于一个三维空间中的平行线段，在二维图像中会收敛于一个消影点。消影点代表某一方向的无穷远点。
- **如何形成：** 如图所示，C为相机的光心，$X_1、X_2、X_3、X_4$是三维空间共线的点，当点$X_n$趋近于无穷远时，$CX_i=CD$，消影点为$v'$。因此，所有平行于$X_{i-1}X_i$的线段在图像中都会交汇于消影点$v'$。
  <p align="center">
  <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/vanishing_point_book.png" width = "400">
  <br>消影点的形成
  </p>
- **应用：**
  - 估计相机的旋转
  - 估计运动物体的运动方向（如汽车的行驶方向/飞行器的飞行方向）



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
  - STEP2：将 $\overrightarrow{X}$ 表示为 $\overrightarrow{x}$ 的函数，即 $\overrightarrow{X} = K^{-1} \overrightarrow{x}$ ，代入第二幅视图 的像方程中，得到
    $$\overrightarrow{x}' = K' [R | t] K^{-1} \overrightarrow{x}$$
  - STEP3：定义基本矩阵 $F$ 为 $F=K'[R|t]K^{-1}$ ，则有
    $$\overrightarrow{x}'^T F \overrightarrow{x} = \overrightarrow{x}'^T K' [R | t] K^{-1} \overrightarrow{x} = 0$$
    其中 $\overrightarrow{x}'^T K' [R | t] K^{-1} \overrightarrow{x}$ 表示 $\overrightarrow{x}'$ 与 $\overrightarrow{x}$ 之间的关系，满足对极几何约束.
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
- **对极线的单应：** 对极线在两幅图像之间存在单应关系，即如果$l$和$l'$分别是图像中的对极线，则有：
  $$\overrightarrow{l'} = F[\overrightarrow{e}]_\times \overrightarrow{l}$$
  $$\overrightarrow{l} = F^T[\overrightarrow{e'}]_\times \overrightarrow{l'}$$
  <p align="center">
  <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/epipolar_line_book.png" width = "400">
  <br>对极线的单应
  </p>