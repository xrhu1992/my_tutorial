# 结构光编码(Structed Light Encoding)
---
# 1. 结构光编码分类
结构光编码可分为两大类：
- 时域编码（Temporal Coding）：通过多次投射不同的图案来实现编码。
- 空域编码（Spatial Coding）：通过单次投射（One Shot）一个复杂的图案来实现编码。
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/structed_light.png" width = "450">
<br> 结构光编码分类</p>

---
# 2. 格雷码(Gray Code)
> [基于结构光投影三维重建：格雷码编码与解码](https://zhuanlan.zhihu.com/p/362816973)
## 2.1 定义
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

## 2.2 编码规则
  - **二进制码 -> Gray码：** 对于n位二进制的码字，从右到左，以0到 n-1编号，如果二进制码字的第i位和i+1位相同，则对应的格雷码的第i位为0，否则为1。
  ``` C++
  unsigned int binaryToGray(unsigned int binary) { return binary ^ (binary >> 1); }
  ```
  - **Gray码 -> 二进制码：** 从左边第二位起，将每位与左边一位解码后的值异或，作为该位解码后的值（最左边一位依然不变）。依次异或，直到最低位。依次异或转换后的值就是格雷码转换 后的二进制值。
  ``` C++
  unsigned int grayToBinary(unsigned int gray)
  {
    unsigned int binary = gray;
    binary ^= binary >> 16;
    binary ^= binary >> 8;
    binary ^= binary >> 4;
    binary ^= binary >> 2;
    binary ^= binary >> 1;
    return binary;
  }
  ```

## 2.3 互补格雷码（Complementary Gray Code）
- **定义：** 为了解决Gray码在处理明暗边界时容易误匹配的问题，引入了互补格雷码。互补格雷码将常规格雷码平移半个周期（对应相位周期 $\pi$ ），通过两套错开的Gray码序列，实现明暗边界之间的平滑过渡。缺点是Gray码的投射图案需要增加一倍。
- **解码：** 由相位码解码得到的相位 $\phi$ ，结合Gray码的周期数 $k_{normal}$ 和平移Gray码的周期数 $k_{shifted}$ ，确定真实的周期数 $k_{real}$
  - 当 $\phi < \frac{\pi}{2}$ 时，常规格雷码处于左边界区域，平移格雷码处于非边界可信区域，应根据平移码确定真实周期数，$k_{real} = k_{shifted}+1$
  - 当 $\frac{\pi}{2} \leq \phi \leq \frac{3\pi}{2}$ 时，常规格雷码处于非边界可信区域，平移格雷码处于边界区域，应根据常规码确定真实周期数$k_{real} = k_{normal}$
  - 当 $\phi > \frac{3\pi}{2}$ 时，常规格雷码处于右边界区域，平移格雷码处于非边界可信区域，应根据平移码确定真实周期数，$k_{real} = k_{shifted}$
    $$
    \begin{aligned}
    &\phi < \frac{\pi}{2} \implies k_{real} = k_{shifted}+1 \\
    \frac{\pi}{2} \leq &\phi \leq \frac{3\pi}{2} \implies k_{real} = k_{normal}\\
    &\phi > \frac{3\pi}{2} \implies k_{real} = k_{shifted}
    \end{aligned}
    $$

---
# 3. 相位编码（Phase Shift）
> [经典结构光编码方法：从二值编码到相位编码](https://zhuanlan.zhihu.com/p/2015611076994162783)
## 3.1 定义
- **定义：** 投射带有不同相位的正弦波灰度条纹 $I(x) = A + B \cdot \cos\phi$ ，通过解码相位 $\phi$ 信息得到编码位置信息。（连续的时域编码）
- **优点：** 正弦波在空间上是连续变化的，因此它天然支持亚像素级别的精度。
- **缺点：** 相位缠绕（Phase Wrapping）：由于相位是一个周期性的量，相位值超过一个周期后会重新开始计数，导致解码错误。可以通过多频率编码（Multi-Frequency Coding）或结合格雷码来解决，低频确定周期，高频确定位置。

## 3.2 四步相移法（Four-Step Phase Shifting）
依次投射四个相位分别为$0$、$\frac{\pi}{2}$、$\pi$、$\frac{3\pi}{2}$的正弦波图案，这四张图案的强度分别为：
$$
\begin{aligned}
I_1 &= A + B \cdot \cos\phi \\
I_2 &= A + B \cdot \cos\left(\phi + \frac{\pi}{2}\right) = A - B \cdot \sin\phi \\
I_3 &= A + B \cdot \cos\left(\phi + \pi\right) = A - B \cdot \cos\phi \\
I_4 &= A + B \cdot \cos\left(\phi + \frac{3\pi}{2}\right) = A + B \cdot \sin\phi
\end{aligned}
$$
其中，$\phi$是相位。通过这四个图案的强度值，可以计算出相位$\phi$：
$$ \phi = \arctan\left(\frac{I_4 - I_2}{I_1 - I_3}\right) $$
此外，$A$是背景光强（Background Intensity），$B$是调制幅度（Modulation Amplitude），$B$调制幅度反映了条纹质量。
$$
\begin{aligned}
A &= \frac{I_1 + I_2 + I_3 + I_4}{4}\\
B &= \frac{\sqrt{(I_1 - I_3)^2 + (I_4 - I_2)^2}}{2}
\end{aligned}
$$
对比度$\gamma$（Contrast）对比度越大，编码的可信度越高：
$$ 
\begin{aligned}
I_{max} &= A + B \\
I_{min} &= A - B \\
\gamma &= \frac{I_{max}-I_{min}}{I_{max}+I_{min}} = \frac{B}{A} 
\end{aligned}
$$
<p align="center">
<img src="https://pic4.zhimg.com/v2-95f0b52e858e14df16fabfda90ec410d_1440w.jpg" width = "600">
<br>四步相移法</p>

## 3.3 三步相移法（Three-Step Phase Shifting）
依次投射三个相位分别为$0$、$\frac{2\pi}{3}$、$\frac{4\pi}{3}$的正弦波图案，这三个图案的强度分别为：
$$
\begin{aligned}
I_1 &= A + B \cdot \cos\phi \\
I_2 &= A + B \cdot \cos\left(\phi + \frac{2\pi}{3}\right) \\
I_3 &= A + B \cdot \cos\left(\phi + \frac{4\pi}{3}\right)
\end{aligned}
$$
其中，$A$是背景光强，$B$是调制幅度，$\phi$是相位。通过这三个图案的强度值，可以计算出各参数：
$$
\begin{aligned}
\phi &= \arctan\left(\frac{\sqrt{3}(I_3 - I_2)}{2I_1 - I_2 - I_3}\right)\\
A &= \frac{I_1 + I_2 + I_3}{3}\\
B &= \frac{\sqrt{3(I_2 - I_3)^2 + (2I_1 - I_2 - I_3)^2}}{3}
\end{aligned}
$$

> [!NOTE]
> - 四步相移法构成超静定方程，可以更好地抑制噪声
> - 三步相移法计算更简单，但对噪声更敏感

## 3.4 多频外差（Multi-Frequency Heterodyne）

---
# 4 混合编码（Hybrid Encoding）
## 4.1 定义
- **定义：** 将两种或多种编码方法结合使用，例如先使用格雷码确定大致位置，再使用相位编码进行亚像素级别的精细定位，以提高编码的鲁棒性和精度。
- **Gray码+相移码：** Gray码粗定位确定条纹级数(Fringe Order)，相移码对每个粗条纹进行包裹相位(Wrapped Phase)，最后再进行相位展开(unwrapPhase)。

## 4.2 级数跳变
- **现象：** 由于Gray码边界模糊带来的误匹配，可能会导致条纹黑白边界处的级数跳变（Fringe Order Jump），在相移码相位展开时会导致位置相差一个周期，边界处深度突变和缺失。
- **平移gray码（Shifted Gray Code）：** 图案的黑白逻辑不变，但整个条纹图案在空间上平移了半个最小周期（1/2 Pitch）。

## 4.3 解码流程（互补格雷码+相移）
1. 投射纯黑和纯白图案，用于区分背景区域和投影区域，得到投影区域的mask（背景区域置零）和Gray码解码阈值： 
   $$I_{threshold}=\frac{I_{white} + I_{black}}{2}$$
2. 投射常规格雷码+平移格雷码+相移码，根据相位码解包裹得到的相位 $\phi$ (范围 $[0, 2\pi)$ )，结合Gray码的周期数 $k_{normal}$ 和平移Gray码的周期数 $k_{shifted}$ ，确定真实的周期数 $k_{real}$。
3. 根据相位 $\phi$ 、周期数 $k_{real}$ 和每周期的像素数 $pixel$ 进行相位展开，计算出编码位置信息。
   $$coord = (\frac{\phi}{2\pi} + k_{real}) \cdot pixel$$


---
# 5. De Bruijn序列编码（De Bruijn Sequence）
> [扑克魔术：神奇的德布鲁因序列](https://halfrost.com/go_s2_de_bruijn/)
## 5.1 定义
- **定义：** 德布鲁因序列(De Bruijn sequence)，记为B(k, n)，是 k 个元素构成的循环序列。所有长度为 n 的 k 元素构成序列都在它的子序列（以环状形式）中，出现并且仅出现一次。
  - 例如，序列 00010111 属于B(2,3)。 00010111 的所有长度为3的子序列为000,001,010,101,011,111,110,100，正好构成了 {0,1} ^3^ 的所有组合。
- **长度：** B(k, n) 的长度为 $k^n$。
  - 例如，对于由k=2个元素（0和1）构成的长度为n=3的德布鲁因序列B(2,3)，其长度为 $2*2*2=8$，即00010111(首尾相接，若首尾不相接则写成0001011100，多n-1位)。
- **编码种类数：** 德布鲁因序列 B(k,n) 的种类数量为 $\frac{(k!)^{k^{n-1}}}{k^n}$。
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/Actual-color-stripe-indexing-pattern-based-on-De-Bruijn-sequence-n-3-k-5.png" height = "260">
<br> 由k=5个元素（红、绿、蓝、黄、紫）构成的长度为n=3的德布鲁因序列B(5,3)的条纹编码(不对！)</p>

## 5.2 编码规则
- **条纹结构光编码：** 假设以蓝（0）绿（1）和蓝绿混合的青色（2）三种颜色编码，即k=3，当编码长度为n=4时，德布鲁因序列B(3,4)的长度为 $3^4=81$，可以编码81+(4-1)=84个条纹。当n=3时，B(3,3)的长度为 $3^3=27$，可以编码27+(3-1)=29个条纹。
 





