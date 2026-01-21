# 立体视觉

### 1. 单目散斑结构光
### 1.1 原理
<p align="center">
<img src="https://developer-orbbec-oss.oss-cn-shenzhen.aliyuncs.com/images/c35783fb-17e3-45fe-aec4-5c1d8ef269cd.png" height = "450">
<br>
图1.1.1 单目散斑结构光原理
</p>

### 1.2 参考图
* 参考图：在垂直相机光轴的某一**固定距离**拍摄，并经过**极线校正**后的图像(也可以引入参考平面方程，可避免调垂直相机光轴位置和距离)
* 为什么不用DOE设计图：参考图包含了系统的畸变信息，能更好地匹配实时图，也免去了对投射系统畸变建模的复杂过程
* 在3D视觉系统中，深度$z$与视差$\delta$成反比： $z = \frac{f \cdot B}{\delta}$，其中$f$为焦距，$B$为基线长度，将视差看成相对值，距离也可通过相对于参考距离计算得到
  ```math
  \Delta =\delta_1 - \delta_0= \frac{f \cdot B}{z_1} - \frac{f \cdot B}{z_0} = f \cdot B \cdot \frac{z_0 - z_1}{z_0 \cdot z_1}
  \implies
  z_1 = \frac{f \cdot B \cdot z_0}{f \cdot B + \Delta \cdot z_0}
  ```
* 问题：参考图和实时图像都是同一个相机拍摄的，需要对参考图做极线校正吗？
  
<p align="center">
<img src="https://i-blog.csdnimg.cn/blog_migrate/8a6ce8360b49dd42ddac20aef6000e2a.png#pic_center" width = "800">
<br>
图1.2.1 参考图
<br>
<img src="https://tse1.mm.bing.net/th/id/OIP.Le1xFiqJ62hC9ZdFvbYe9QAAAA?rs=1&pid=ImgDetMain&o=7&rm=3" width = "800">
<br>
图1.2.2 实时图-参考图的块匹配
</p> 

### 1.3 标定
* [方法1:基于圆点阵标定板](https://blog.csdn.net/memmolo/article/details/136760798)
<p align="center">
<img src="https://i-blog.csdnimg.cn/blog_migrate/7d167846a869a4ddf2dcc6debcfbbace.png#pic_center" height = "500">
<br>
图1.3.1 单目散斑结构光标定的一种方法
</p> 