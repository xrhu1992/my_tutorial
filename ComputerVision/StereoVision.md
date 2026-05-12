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

# 2. 结构光编码（Structured Light Encoding）
结构光编码可分为两大类：
- 时域编码（Temporal Coding）：通过多次投射不同的图案来实现编码。
- 空域编码（Spatial Coding）：通过单次投射（One Shot）一个复杂的图案来实现编码。
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/structed_light.png" width = "500">
<br> 结构光编码分类
</p>

## 2.1 De Bruijn序列编码（De Bruijn Sequence Encoding）
> [扑克魔术：神奇的德布鲁因序列](https://halfrost.com/go_s2_de_bruijn/)
### 2.1.1 定义
- **定义：** 德布鲁因序列(De Bruijn sequence)，记为B(k, n)，是 k 个元素构成的循环序列。所有长度为 n 的 k 元素构成序列都在它的子序列（以环状形式）中，出现并且仅出现一次。
  - 例如，序列 00010111 属于B(2,3)。 00010111 的所有长度为3的子序列为000,001,010,101,011,111,110,100，正好构成了 {0,1} ^3^ 的所有组合。
- **长度：** B(k, n) 的长度为 $k^n$。
  - 例如，对于由k=2个元素（0和1）构成的长度为n=3的德布鲁因序列B(2,3)，其长度为 $2*2*2=8$，即00010111(首尾相接，若首尾不相接则写成0001011100，多n-1位)。
- **编码种类数：** 德布鲁因序列 B(k,n) 的种类数量为 $\frac{(k!)^{k^{n-1}}}{k^n}$。
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/Actual-color-stripe-indexing-pattern-based-on-De-Bruijn-sequence-n-3-k-5.png" height = "260">
<br> 由k=5个元素（红、绿、蓝、黄、紫）构成的长度为n=3的德布鲁因序列B(5,3)的条纹编码(不对！)</p>

### 2.1.2 编码规则
- **条纹结构光编码：** 假设以蓝（0）绿（1）和蓝绿混合的青色（2）三种颜色编码，即k=3，当编码长度为n=4时，德布鲁因序列B(3,4)的长度为 $3^4=81$，可以编码81+(4-1)=84个条纹。当n=3时，B(3,3)的长度为 $3^3=27$，可以编码27+(3-1)=29个条纹。

## 2.2 Gray码编码（Gray Code Encoding）
> [基于结构光投影三维重建：格雷码编码与解码](https://zhuanlan.zhihu.com/p/362816973)
## 2.2.1 定义
- **定义：** Gray码是一种二进制编码方式，其特点是**相邻的两个码字只有一位不同**，具有很好的抗干扰能力。(离散的时域编码)
  - 例如下图中：十进制码5和6对应的Gray码为111-101，只有一位不同；而十进制码4和5对应的Gray码为101-110，有两位不同。
    <p align="center">
    <img src="https://pica.zhimg.com/v2-ebd087107008086b188a69e7e47713d4_1440w.jpg" width = "580">
    <br>编码过程<br>
    <img src="https://pica.zhimg.com/v2-871d00cead87b25fd8394bd13ed4e712_1440w.jpg" height = "230">
    <img src="https://picx.zhimg.com/v2-c1edce7754f8151d1ce8982dc5e7a261_1440w.jpg" height = "230">
    <br>3位Gray码 & 二进制码<br>
    <img src="https://pica.zhimg.com/v2-87eda030e646d2aac749d6231f58598a_1440w.jpg" width = "580">
    <br>二进制码序列 & Gray码序列</p>
- **编码长度：** n位Gray码的编码数为 $2^n$，在结构光中需要投射n个编码图案。
- **优点：** 
  - 明暗交接处更少（如下图）,减少了边界模糊带来的误匹配，同时条纹更宽。
  - 相邻码字只有一位不同，具有很好的抗干扰能力。如图：
  <p align="center">
  <img src="https://pic3.zhimg.com/v2-dc58882964c2bdf8375f73865957d4e6_1440w.jpg" width = "600">
  <br>Gray码具有更好的抗干扰能力（每次只改变一位）</p>
- **缺点：** 
  - 当图案模糊时，在处理明暗边界时容易误匹配
  - Gray码编码是离散的，精度受投射器分辨率限制，无法达到亚像素精度

### 2.2.2 编码规则
  - **二进制码 -> Gray码：** 对于n位二进制的码字，从右到左，以0到 n-1编号，如果二进制码字的第i位和i+1位相同，则对应的格雷码的第i位为0，否则为1。
  - **Gray码 -> 二进制码：** 从左边第二位起，将每位与左边一位解码后的值异或，作为该位解码后的值（最左边一位依然不变）。依次异或，直到最低位。依次异或转换后的值就是格雷码转换 后的二进制值。

### 2.2.3 注意事项
- 实际投射时，还需要补充全黑和全白图案，以便于区分条纹边界。二值化阈值为: $I_{threshold}=\frac{I_{white} + I_{black}}{2}$

## 2.3 相位编码（Phase Shift Encoding）
> [经典结构光编码方法：从二值编码到相位编码](https://zhuanlan.zhihu.com/p/2015611076994162783)
## 2.3.1 定义
- **定义：** 投射带有不同相位的正弦波灰度条纹，通过解码相位信息得到编码位置信息。（连续的时域编码）
- **优点：** 正弦波在空间上是连续变化的，因此它天然支持亚像素级别的精度。
- **缺点：** 相位缠绕（Phase Wrapping）：由于相位是一个周期性的量，相位值超过一个周期后会重新开始计数，导致解码错误。可以通过多频率编码（Multi-Frequency Coding）来解决，低频确定周期，高频确定位置。

## 2.3.2 相移法（Phase Shifting Method）
- **四步相移法（Four-Step Phase Shifting）：** 依次投射四个相位分别为$0$、$\frac{\pi}{2}$、$\pi$、$\frac{3\pi}{2}$的正弦波图案，这四张图案的强度分别为：
$$
\begin{aligned}
I_1 &= A + B \cdot \cos\phi \\
I_2 &= A + B \cdot \cos\left(\phi + \frac{\pi}{2}\right) = A - B \cdot \sin\phi \\
I_3 &= A + B \cdot \cos\left(\phi + \pi\right) = A - B \cdot \cos\phi \\
I_4 &= A + B \cdot \cos\left(\phi + \frac{3\pi}{2}\right) = A + B \cdot \sin\phi
\end{aligned}
$$
其中，$A$是背景光强，$B$是调制幅度，$\phi$是相位。通过这四个图案的强度值，可以计算出相位$\phi$：
$$\phi = \arctan\left(\frac{I_4 - I_2}{I_1 - I_3}\right)$$
<p align="center">
<img src="https://pic4.zhimg.com/v2-95f0b52e858e14df16fabfda90ec410d_1440w.jpg" width = "600">
<br>四步相移法</p>

- **三步相移法（Three-Step Phase Shifting）：** 依次投射三个相位分别为$0$、$\frac{2\pi}{3}$、$\frac{4\pi}{3}$的正弦波图案，这三个图案的强度分别为：
$$
\begin{aligned}
I_1 &= A + B \cdot \cos\phi \\
I_2 &= A + B \cdot \cos\left(\phi + \frac{2\pi}{3}\right) \\
I_3 &= A + B \cdot \cos\left(\phi + \frac{4\pi}{3}\right)
\end{aligned}
$$
其中，$A$是背景光强，$B$是调制幅度，$\phi$是相位。通过这三个图案的强度值，可以计算出相位$\phi$：
$$\phi = \arctan\left(\frac{I_3 - I_1}{I_2 - I_1}\right)$$
- **比较：** 四步相移法构成超静定方程，可以更好地抑制噪声；三步相移法计算更简单，但对噪声更敏感。

## 2.4 混合编码（Hybrid Coding）
- **定义：** 将两种或多种编码方法结合使用，例如先使用格雷码确定大致位置，再使用相位编码进行亚像素级别的精细定位，以提高编码的鲁棒性和精度。