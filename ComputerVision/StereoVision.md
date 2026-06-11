# 立体视觉重建（Stereo Vision Reconstruction）
---
# 1. 单目散斑结构光（Single-View Structured Light）
## 1.1 原理
<p align="center">
<img src="https://developer-orbbec-oss.oss-cn-shenzhen.aliyuncs.com/images/c35783fb-17e3-45fe-aec4-5c1d8ef269cd.png" height = 300">
<img src="https://picx.zhimg.com/v2-c01ce5dbc0b4a0401b16c4425a8dd6b7_1440w.jpg" height = "300">
<br>图1.1.1 单目散斑结构光原理<br>
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/relation%20of%20depth%20and%20disparity.png" height = "320">
<br>深度与视差的关系</p>

- **参考图：** 在垂直相机光轴的某一**固定距离**拍摄，并经过**极线校正**后的图像。也可以引入参考平面方程$Ax+By+z=D$，可避免调垂直相机光轴位置和距离，降低标定难度。
- 在3D视觉系统中，深度$z$与视差$\delta$成反比： $z = \frac{f \cdot B}{\delta}$，其中$f$为焦距，$B$为基线长度，将视差看成相对值，距离也可通过相对于参考距离计算得到。参考图1.1.1。
  $$
  \Delta =\delta_1 - \delta_0= \frac{f \cdot B}{z_1} - \frac{f \cdot B}{z_0} = f \cdot B \cdot \frac{z_0 - z_1}{z_0 \cdot z_1}
  \implies
  z_1 = \frac{f \cdot B \cdot z_0}{f \cdot B + \Delta \cdot z_0}
  $$

> [!NOTE]
> 1. 为什么不用DOE设计图（这样的话原理上更接近双目视觉）：参考图包含了系统的畸变信息，能更好地匹配实时图，也免去了对投射系统畸变建模。
> 2. sensor与基线不平行的情况如何处理？

## 1.2 极线配准
<p align="center">
<img src="https://i-blog.csdnimg.cn/blog_migrate/dc49f512068aebf0f71a8ba4711a6c56.png" width = "400">
<br>图1.2.1 双目系统的极线配准
</p>
- 单目结构光参考图和实时图的极线是重合的，只要计算出极点位置（极点不一定在图像上），就可以将参考图和实时图进行极线配准。
- 参考图和实时图的极线校正参数是相同的。


## 1.3 局部匹配（Local Matching）
<p align="center">
<img src="https://i-blog.csdnimg.cn/blog_migrate/b0bd7cae3d54567ecddc14572b56d598.png#pic_center" height = "300">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/matching%20cost%20computation.png" height = "300">
<br>图1.3.1 实时图-参考图的极线校正与匹配
</p> 

## 1.4 标定
## 1.4.1 圆点和棋盘
- **棋盘格**
  - 优点：角点位置不受透视变换和畸变影响，容易检测和定位
  - 缺点：当景深较小时，如果角点模糊，会导致角点检测精度下降
- **圆点阵**
  - 优点：抗干扰能力强，即使在模糊情况下也能检测到圆心位置，适用于景深较小的情况
  - 缺点：圆点位置受透视变换和畸变影响较大，需要做偏差校正
- 对于口扫场景，精度要求搞，景深较小，使用圆点阵标定板更合适（圆点也更适合小标定板的加工制造）。

- [方法1](https://blog.csdn.net/memmolo/article/details/136760798): 基于圆点阵标定板，将散斑投射到白色高反圆点上
  <p align="center">
  <img src="https://i-blog.csdnimg.cn/blog_migrate/7d167846a869a4ddf2dcc6debcfbbace.png#pic_center" height = "400">
  <br>图1.4.1 单目散斑结构光标定的一种方法<br>
  <img src="https://mmbiz.qpic.cn/mmbiz_png/Q0FNTB1XHicxyVNEAicrWE8dyaphS4uhWgdwkpibickPDrTHiamTEAIWjVBKib1LCJgjqVoTKNrQ2RcJK2YaYLz9f0KQ/640?tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0" height = "220">
  <br>应用局部单应矩阵反投影
  </p>

