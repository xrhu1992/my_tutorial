# 单视图几何（Single-View Geometry）
---
## 1. 消影点（Vanishing Point）
### 1.1 定义
图像中平行于某一方向的线段在图像中交汇的点。对于一个三维空间中的平行线段，在二维图像中会收敛于一个消影点。消影点代表某一方向的无穷远点。
- **如何形成：** 如图所示，C为相机的光心，$X_1、X_2、X_3、X_4$是三维空间共线的点，当点$X_n$趋近于无穷远时，$CX_i=CD$，消影点为$v'$。因此，所有平行于$X_{i-1}X_i$的线段在图像中都会交汇于消影点$v'$。
- **平行线方向：** 相机光心到消影点的方向与物理空间中的平行线方向一致。
  <p align="center">
  <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/vanishing_point_book.png" width = "400">
  <br>消影点的形成</p>
### 1.2 应用
  - 估计相机的旋转(如单目多视图下估计相机或物体的旋转矩阵)
  - 估计运动物体的运动方向（如汽车的行驶方向/飞行器的飞行方向）
  - 利用影子判断太阳方向（太阳可以看作无穷远处平行光线）
  - AI生成图片/视频鉴别
  <p align="center">
  <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/tutorial_vanishing-point-application-1.jpg" height = "250">
  <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/tutorial_vanishing-point-application-2.jpg" height = "250">
  <img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/tutorial_vanishing-point-application-3.jpg" height = "250">
  <br>利用消影点鉴别AI图片</p>

## 2. 畸变模型（Distortion Model）
### 2.1 针孔相机畸变模型（Pinhole Camera Distortion Model）
设归一化相机坐标系下的理想（未畸变）坐标为$(x,y)$，畸变后的坐标为$(x_d,y_d)$
$$
x = \frac{u-c_x}{f_x} \\
y = \frac{v-c_y}{f_y}
$$

- **径向畸变（Radial Distortion）：** 
  $$
  \delta_{dr}=x(k_1r^2+k_2r^4+k_3r^6) \\
  \delta_{dr}=y(k_1r^2+k_2r^4+k_3r^6)
  $$
- **切向畸变（Tangential Distortion）：** 
  $$
  \delta_{dt}=2p_1xy+p_2(r^2+2x^2) \\
  \delta_{dt}=p_1(r^2+2y^2)+2p_2xy
  $$
- **总畸变模型：** 
  $$\left\{ 
  \begin{aligned}
  x_d &= x+\delta_{dr}+\delta_{dt} = x(1+k_1r^2+k_2r^4+k_3r^6)+2p_1xy+p_2(r^2+2x^2) \\
  y_d &= y+\delta_{dr}+\delta_{dt} = y(1+k_1r^2+k_2r^4+k_3r^6)+2p_1(r^2+2y^2)+2p_2xy \\
  r^2 &= x^2+y^2
  \end{aligned}
  \right.$$

- **不动点迭代（Fixed Point Iteration）求解：** 给定畸变后的坐标$(x_d,y_d)$ 和畸变系数 $k_1,k_2,k_3,p_1,p_2$ ，求解理想坐标$(x,y)$。迭代公式为：
  - 初始值
    $$x_0=x_d\\
    y_0=y_d$$
  - 迭代公式
  $$\begin{aligned}
  x_{n+1} &= \frac{x_n-2p_1x_ny_n-p_2(r_n^2+2x_n^2)}{1+k_1r_n^2+k_2r_n^4+k_3r_n^6} \\
  y_{n+1} &= \frac{y_n-2p_1(r_n^2+2y_n^2)-2p_2x_ny_n}{1+k_1r_n^2+k_2r_n^4+k_3r_n^6} \\
  r_n &= x_n^2+y_n^2
  \end{aligned}$$

<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/radial_distort.png" height = "240">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/tangential_distort.png" height = "200">
<br>经向畸变 & 切向畸变</p>

