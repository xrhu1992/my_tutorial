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