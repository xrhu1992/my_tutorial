# 立体视觉（Stereo Vision）

## 1. 单目散斑结构光（Single-View Structured Light）
### 1.1 原理
<p align="center">
<img src="https://developer-orbbec-oss.oss-cn-shenzhen.aliyuncs.com/images/c35783fb-17e3-45fe-aec4-5c1d8ef269cd.png" height = "450">
<br>
图1.1.1 单目散斑结构光原理
</p>

### 1.2 参考图
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
<br>
图1.2.1 参考平面与实时图的视差关系
<br>
<img src="https://tse1.mm.bing.net/th/id/OIP.Le1xFiqJ62hC9ZdFvbYe9QAAAA?rs=1&pid=ImgDetMain&o=7&rm=3" width = "800">
<br>
图1.2.2 实时图-参考图的块匹配
</p> 

### 1.3 标定
* [方法1](https://blog.csdn.net/memmolo/article/details/136760798): 基于圆点阵标定板，将散斑投射到白色高反圆点上
  <p align="center">
  <img src="https://i-blog.csdnimg.cn/blog_migrate/7d167846a869a4ddf2dcc6debcfbbace.png#pic_center" height = "500">
  <br>
  图1.3.1 单目散斑结构光标定的一种方法
  </p>

## 2. 双目立体视觉（Binocular Stereo Vision）
### 2.1 点-线-面的性质（Point-Line-Face Properties）
#### 2.1.1 平面表示
- **平面点：** $\overrightarrow{x}=(x,y)^T$ ，齐次表示： $\overrightarrow{x}=(x,y,1)^T$
- **平面线：** $ax+by+c=0$，向量表示：$\overrightarrow{l}=(a,b,c)^T$，其中$\overrightarrow{n}=(a,b)$$为线的法向量

#### 2.1.2 空间表示
- **空间点：** $\overrightarrow{X}=(X,Y,Z)^T$，齐次表示： $\overrightarrow{X}=(X,Y,Z,1)^T$
- **空间线：** $\overrightarrow{L}=(\overrightarrow{P},\overrightarrow{V})$，其中$\overrightarrow{P}$为线上的一个点，$\overrightarrow{V}$为线的方向向量
- **空间面：** $aX+bY+cZ+d=0$，向量表示：$\overrightarrow{S}=(a,b,c,d)^T$，其中$\overrightarrow{n}=(a,b,c)$为面的法向量