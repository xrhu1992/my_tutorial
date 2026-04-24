# 立体视觉重建（Stereo Vision Reconstruction）
---
# 1. 单目散斑结构光（Single-View Structured Light）
## 1.1 原理
<p align="center">
<img src="https://developer-orbbec-oss.oss-cn-shenzhen.aliyuncs.com/images/c35783fb-17e3-45fe-aec4-5c1d8ef269cd.png" height = 320">
<img src="https://picx.zhimg.com/v2-c01ce5dbc0b4a0401b16c4425a8dd6b7_1440w.jpg" height = "320">
<br>图1.1.1 单目散斑结构光原理
</p>

- **参考图：** 在垂直相机光轴的某一**固定距离**拍摄，并经过**极线校正**后的图像。也可以引入参考平面方程$Ax+By+z=D$，可避免调垂直相机光轴位置和距离，降低标定难度。
- 在3D视觉系统中，深度$z$与视差$\delta$成反比： $z = \frac{f \cdot B}{\delta}$，其中$f$为焦距，$B$为基线长度，将视差看成相对值，距离也可通过相对于参考距离计算得到。参考图1.1.1。
  $$
  \Delta =\delta_1 - \delta_0= \frac{f \cdot B}{z_1} - \frac{f \cdot B}{z_0} = f \cdot B \cdot \frac{z_0 - z_1}{z_0 \cdot z_1}
  \implies
  z_1 = \frac{f \cdot B \cdot z_0}{f \cdot B + \Delta \cdot z_0}
  $$

> [!NOTE]
> 1. 为什么不用DOE设计图（这样的话原理上更接近双目视觉）：参考图包含了系统的畸变信息，能更好地匹配实时图，也免去了对投射系统畸变建模。
> 2. sensor与基线不平行

## 1.2 极线配准
<p align="center">
<img src="https://i-blog.csdnimg.cn/blog_migrate/dc49f512068aebf0f71a8ba4711a6c56.png" width = "400">
<br>图1.2.1 双目系统的极线配准
</p>
- 单目结构光参考图和实时图的极线是重合的，只要计算出极点位置（极点不一定在图像上），就可以将参考图和实时图进行极线配准。
- 参考图和实时图的极线校正参数是相同的。



## 1.3 局部块匹配（Local Block Matching）
<p align="center">
<img src="https://tse1.mm.bing.net/th/id/OIP.Le1xFiqJ62hC9ZdFvbYe9QAAAA?rs=1&pid=ImgDetMain&o=7&rm=3" width = "600">
<br>图1.2.1 实时图-参考图的块匹配
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

## 1.5 De Bruijn序列编码
> [扑克魔术：神奇的德布鲁因序列](https://halfrost.com/go_s2_de_bruijn/)
### 1.5.1 定义
- **定义：** 德布鲁因序列(De Bruijn sequence)，记为B(k, n)，是 k 个元素构成的循环序列。所有长度为 n 的 k 元素构成序列都在它的子序列（以环状形式）中，出现并且仅出现一次。
  - 例如，序列 00010111 属于B(2,3)。 00010111 的所有长度为3的子序列为000,001,010,101,011,111,110,100，正好构成了 {0,1} ^3^ 的所有组合。
- **长度：** B(k, n) 的长度为 $k^n$。
  - 例如，对于由k=2个元素（0和1）构成的长度为n=3的德布鲁因序列B(2,3)，其长度为 $2*2*2=8$，即00010111(首尾相接，若首尾不相接则写成0001011100，多n-1位)。
- **编码种类数：** 德布鲁因序列 B(k,n) 的种类数量为 $\frac{(k!)^{k^{n-1}}}{k^n}$。

### 1.5.2 结构光编码设计
- **条纹结构光编码：** 假设以蓝（0）绿（1）和蓝绿混合的青色（2）三种颜色编码，即k=3，当编码长度为n=4时，德布鲁因序列B(3,4)的长度为 $3^4=81$，可以编码81+(4-1)=84个条纹。当n=3时，B(3,3)的长度为 $3^3=27$，可以编码27+(3-1)=29个条纹。
- 