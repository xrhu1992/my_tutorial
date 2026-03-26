# 光学(Optics)

## 1. 波动光学（Wave Optics）
### 1.1 波面与波线(Wavefront & Wave Ray)
- **波面**：波面是指在空间中具有相同相位的点的集合。对于一个点光源发出的球面波，波面是一个以光源为中心的球面；对于一个平行光束，波面是一个平面。波面的形状和位置决定了光的传播方向和性质。（例如水面的波纹就是波面，每个波纹都具有相同的震动状态）
- **波线**：传播方向相同的光线集合称为波线。波线是垂直于波面的曲线，表示光的传播路径。对于一个点光源发出的球面波，波线是从光源向外辐射的直线；对于一个平行光束，波线是平行的直线。波线的密度表示光的强度，密度越大表示光越强。
<p align="center">
<img src="https://image1.slideserve.com/3372415/slide14-l.jpg" height = "300">
<br>波面与波线
</p>

### 1.2 惠更斯原理(Huygens' Principle)
惠更斯原理指出，波前上的每一点都可以看作是次级球面波的波源，这些次级波的包络面构成了新的波前。这一原理可以用来解释光的反射、折射、衍射和干涉现象。
<p align="center">
<img src="https://th.bing.com/th/id/R.598729442f58d041f12fe46c6a92fd74?rik=hJidU5IvN5%2fNIA&riu=http%3a%2f%2fhomepage.ufp.pt%2fbiblioteca%2fSequential+Stratigraphy%2fFigjpgPlates%2fFichasP162.jpg&ehk=aGVSXF83BKU1HQNIykE52bnqOMPhyMb2pqvRDA7Pkyk%3d&risl=&pid=ImgRaw&r=0" height = "280">
<img src="https://images2017.cnblogs.com/blog/401477/201710/401477-20171027143908023-705648426.jpg" height = "280">
<br>惠更斯原理 & 波的反射与折射
</p>

### 1.3 干涉 & 衍射(Interference & Diffraction)
#### 1.3.1 衍射(Diffraction)
- 衍射是波遇到障碍物或通过狭缝时发生的弯曲和扩散现象
- 形成机制：波在传播过程中遇到障碍物或狭缝
- 应用：光栅、衍射光学元件、光学测量等
- 简述：当波遇到障碍物或通过狭缝时，波前会发生弯曲和扩散，形成衍射图样。衍射现象在光学中尤为重要，影响光的传播和成像质量。在光学系统设计中，需要考虑衍射效应以优化性能。
<p align="center">
<img src="https://pic1.zhimg.com/v2-e5a80ef5069a4dd094f91e7a922830e8_b.webp" height = "280">
<br>光衍射传播
</p>

#### 1.3.2 双缝干涉(Double-slit Interference)
> [!NOTE]
> 1. 两个波叠加后的强度为其**振幅项**。带时间的瞬态不能作为观察的光强度！
> 2. 判断相干条纹只需要看相位差（光程差），相位差相同则条纹相同
- 双缝干涉是指当相干光通过两条狭缝后，在屏幕上形成明暗相间的干涉条纹现象。波在通过狭缝后发生衍射，其在屏幕上各个位置的光程差不同。两个狭缝的衍射波在屏幕上同一位置由于存在光程差/相位差，波叠加后在屏幕上形成干涉条纹。
- 当光程差为波长的整数倍时，发生**建设性干涉**，形成亮纹；当光程差为波长的奇数倍时，发生**破坏性干涉**，形成暗纹。
- 相干光叠加的强度计算公式：
  ```math
  I=I_1+I_2+2\sqrt{I_1I_2}cos(\delta)
  ```
  其中，I₁ 和 I₂ 分别是两个波的强度，δ 是它们之间的相位差。
<p align="center">
<img src="https://pic2.zhimg.com/v2-600560c80f0ea0d98d38fd48a3e8a715_r.jpg" width = "500">
<br>双缝干涉
</p> 

#### 1.3.4 散斑(Speckle)
- 散斑是由于相干光（如激光）照射在粗糙表面或通过不均匀介质后产生的明暗斑点图案（常见于单色投影激光器）
- 形成机制：相干光在粗糙表面反射或通过不均匀介质时，不同路径的光波相互干涉，产生明暗变化
- 应用：散斑干涉测量、散斑成像、散斑相关技术等
- 简述：当相干光照射到粗糙表面时，表面的微小不规则结构会导致反射光的相位发生变化。不同位置反射回来的光波由于路径差异，在空间上产生干涉现象，形成明暗交替的散斑图案。这种现象在激光投影、激光显示等应用中尤为明显，可能影响图像质量。
<p align="center">
<img src="https://static.mianbaoban-assets.eet-china.com/xinyu-images/MBXY-CR-953a25f3b3d44e88e15bba5fd7b75a65.png" width = "450">
<br>激光投影散斑现象
</p>

## 2. 几何光学（Geometric Optics）
### 2.1 斯奈尔公式（Snell's Law）
- 斯奈尔公式描述了光在两种不同介质界面上的折射现象（折射的本质是光在不同材料下传播速度的不同导致的，可由波动光学中的惠更斯原理解释）
  ```math
  n_1 \ast sin(\theta_2) = n_2 \ast sin(\theta_2)
  ```
  其中，n₁ 和 n₂ 分别是两种介质的折射率，θ₁ 是入射角，θ₂ 是折射角。
- **折射率**：光在不同材质下传播速度的衰减$n=\frac{c}{v}$，常见材料的折射率
  - 空气：约为 1.0003
  - 水：约为 1.33
  - 玻璃：约为 1.5 到 1.9（H-K9L折射率1.5168）
  
### 2.2 全反射（Total Internal Reflection）
- **全反射临界角** 此时折射角为90°，入射角大于临界角后只有反射光无折射光
  ```math
  \theta=arcsin\frac{n2}{n1}
  ```
  <center>
  <img src="https://my-tutorial-1384742255.cos.ap-nanjing.myqcloud.com/Optics/Reflexion_totale_interne.png" title="全反射" width = "300">
  <br>
  全反射
  </center>
- 全反射镜（如直角棱镜）反射效率高于镀膜平面反射镜（反射效率约90%）

## 3. 光学元器件(Optical Components)
### 3.1 衍射光学元件DOE(Diffractive Optical Elements)
#### 3.1.1 原理
- 衍射光学元件（DOE）是一种利用光的衍射效应来控制和调制光波前的光学元件，当光学元件的尺寸与光波波长相近或比波长更小时衍射现象十分明显。DOE通过在其表面设计微小的结构，使入射光经过衍射后形成特定的光强分布或相位分布。
<p align="center">
<img src="https://pic2.zhimg.com/v2-3a51f40145c6786d5faae14d77ad4c1d_1440w.jpg" height = "300">
<img src="https://pic1.zhimg.com/v2-76dbe7eb9fa15390ee13d6fb9551584c_1440w.jpg" height = "300">
<br>DOE
</p>

#### 3.1.2 作用
- 将光整形成任意的光强分布或相位分布，如光束整形器、匀化器、扩散片、分束器、多焦点DOE等。
  <p align="center">
  <img src="https://pic1.zhimg.com/v2-8e94f345ed108e7cecd22e1bb8e2bb78_1440w.jpg" height = "180">
  <img src="https://pic3.zhimg.com/v2-182bd7253d286156aebfdffbf331e344_1440w.jpg" height = "180">
  <img src="https://pic4.zhimg.com/v2-e92cd89e258eef4f32bd10598358c235_1440w.jpg" height = "180">
  <img src="https://pic3.zhimg.com/v2-29db2cfe3d7c4792a4b81199c583283a_1440w.jpg" height = "180">
  <img src="https://pic4.zhimg.com/v2-49383aa15c8f39f28947edfa3540317d_1440w.jpg" height = "180">
  </br>
  光束整形器 - 匀化器 - 扩散片 - 分束器 - 多焦点DOE
  </p>

### 3.2 波片(Wave Plate)
波片也叫相位延迟片（Phase Delay Plate, PDP），常见有四分之一波片（Quarter-wave Plate）和半波片（Half-wave Plate）。
#### 3.2.1 原理
- **光的极化**:光有极化方向，使用偏振镜片可以筛选出任意特定极化方向的光。从数学角度可以将某极化方向看成为两个互相垂直的分量的合成，两个同相位的分量（红色和蓝色）合成线偏振光，如下示意图：
  <p align="center">
  <video src="https://xrhu-store.oss-cn-shanghai.aliyuncs.com/obsidian/Note/Physics/Quarter-wave-Plate_1.mp4?x-oss-credential=TMP.3KzTe66ph3RYhvMsWAE1WTHAdLrE8aCoZRoFSoJFbmJYnYR4pELRkukHJZKL1uE3dfjWTr1z1A4DTFrjWb6RZjLvQGub8L%2F20260326%2Fcn-shanghai%2Foss%2Faliyun_v4_request&x-oss-date=20260326T053951Z&x-oss-expires=3600&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-signature=f532d7d37d11ee65bc8419f5280874ebd6a345ecc402119bd283ff284603013f" heigth = "450" loop controls></video><br>
  两个同相位的分量（红色和蓝色）合成线偏振光
  </p> 
- 有一类各向异性材料（单轴双折射晶体），对于不同偏振方向的入射光，会有不同的折射率（也就是有不同的传播速度，快轴和慢轴）。而1/4波片就是控制材料和厚度使光经过波片后，两个不同偏振方向的光产生1/4波长的相位差，在此相位差下合成的光为圆偏振光，如下示意图：
  <p align="center">
  <video src="https://xrhu-store.oss-cn-shanghai.aliyuncs.com/obsidian/Note/Physics/Quarter-wave-Plate_2.mp4?x-oss-credential=TMP.3KzTe66ph3RYhvMsWAE1WTHAdLrE8aCoZRoFSoJFbmJYnYR4pELRkukHJZKL1uE3dfjWTr1z1A4DTFrjWb6RZjLvQGub8L%2F20260326%2Fcn-shanghai%2Foss%2Faliyun_v4_request&x-oss-date=20260326T054022Z&x-oss-expires=3600&x-oss-signature-version=OSS4-HMAC-SHA256&x-oss-signature=a943f92c26de2f725d4d21fb5477add984ece461fd8fe62da8d45eba052d4698" heigth = "450" loop controls></video><br>
  红色分量相位延迟1/4波长后与蓝色分量合成圆偏振光
  </p> 
- 总结：四分之一波片能够**将线偏振光转换为圆偏振光，或将圆偏振光转换为线偏振光**。它的工作原理是利用双折射效应，使入射光的两个正交分量之间产生90度的相位差。
> [!NOTE] 
> 1. 线偏振光还可以继续在非垂直方向上矢量分解。随机偏振光经过线偏振片后，光强衰减为1/2；
> 2. 线偏振光偏振方向与四分之一波片的快轴或慢轴成45°/135°角时（这样线偏振光才可沿快慢轴矢量分解成两个相位和幅度相等的分量），出射光才能是圆偏振光，否则为椭圆偏振或保持线偏振。

#### 3.2.2 作用
- **隔离反射光**：激光器发出的经过偏振片选择后的线偏振光，经过1/4波片后，两个分量产生1/4波长相位差，反射回来后，两个分量的方向和相位差不变，再次经过1/4波片，两个分量再次叠加1/4波长相位差，共1/2相位差，所以合成的光为线偏振光，且偏振方向与原方向垂直，所以无法再次通过偏振片。
  <br>
  随机偏振激光 -> 偏振片（线偏振） -> 1/4波片(1/4相位差圆偏振光) -> 反射面 -> 1/4波片(1/2相位差线偏振光) -> 偏振片(偏振方向垂直无法通过)
  <p align="center">
  <img src="https://i-blog.csdnimg.cn/blog_migrate/3072dc5e173c797c65c701f7305756c4.png" height = "250">
  <br>光隔离器
  </p>
- **圆偏振片**：四分之一波片可将线偏振光转变为圆偏振光，于是有，线偏振片+1/4波片=圆偏振片。
  <br>
  随机偏振激光 -> 偏振片（线偏振） -> 1/4波片(圆偏振，注意线偏与快慢轴成45°/135°角)
  <p align="center">
  <img src="https://i-blog.csdnimg.cn/blog_migrate/9579ce34746c4884af0a0a9862e01b50.png" height = "250">
  <br>线偏振片+1/4波片=圆偏振片
  </p>
- **偏振发生器**：激光束垂直入射至偏振片，经过偏振器选偏调制后，得到线偏振光；被调制的线偏振光入射至1/2波片，出射光偏振方向发生偏转；出射光再入射到1/4波片，当1/4波片与入射的线偏振光偏振方向一致时，出射光为线偏光，此时1/2波片可用于调整偏振方向；而快轴方向与偏振方向不一致时，出射光为椭圆偏振光或圆偏振光，此时1/4波片则用来调整椭圆度和旋向。利用此组合装置可实现任意偏振态输出。偏振片+1/2波片+1/4波片=偏振态发生器
  <p align="center">
  <img src="https://i-blog.csdnimg.cn/blog_migrate/eb25cb4a8952ebc6680e5dfe7e854a96.png" height = "250">
  <br>偏振片+1/2波片+1/4波片=偏振态发生器
  </p>
- **光强调节器/光衰减器**：四分之一波片可用于改变偏振光偏振方向，偏振片+1/4波片=光强调节器。(改变1/4波片快慢轴与偏振片偏振方向的夹角，形成椭圆偏振光，即可改变出射偏振光的强度)两个偏振片似乎也能实现同样的效果???
  <br>随机偏振激光 -> 偏振片（线偏振） -> 1/4波片(椭圆偏振，调节快慢轴角度) -> 偏振片(线偏振，强度随快慢轴角度变化)
  <p align="center">
  <img src="https://i-blog.csdnimg.cn/blog_migrate/664c6091101fd55322ebff07a7b573b5.png" height = "250">
  <br>偏振片+1/4波片=光强调节器
  </p>

## 4. 光学成像（Optical Imaging）
### 4.1. 光阑（Stop）
#### 4.1.1 作用
- Lens不能无限大，需要限制透镜宽度
- 提高成像质量，因为只有旁轴附近的光线成像质量较好
- 限制光通量，主要是对平行光的控制

#### 4.1.2 孔径光阑(Aperture Stop)
光学系统中限制通过光束直径的光阑称为孔径光阑，是所有成像光束的公共入口。对发光的物点来说，孔径光阑的大小限制了成像光束的立体角，也即限制了光通量。在摄影用相机镜头中，孔阑通常是一个尺寸可调整的光阑(Stop)，用于控制光通量.
<p align="center">
<img src="../pic/Optics/ApertureStop.png" height = "300">
<br>
孔径光阑
</p>

### 4.2 入瞳(Entrance Pupil)与出瞳(Exit Pupil)
入瞳是物空间中孔径光阑的像，出瞳是像空间中孔径光阑的像。入瞳和出瞳的位置和大小决定了光学系统的光通量特性。
<p align="center">
<img src="../pic/Optics/Entrance&ExitPupil.png" height = "300">
<img src="https://wiki.yanding.com/lib/exe/fetch.php?w=600&tok=cbd5f9&media=yanding:%E5%85%A5%E7%9E%B33.png" height = "300">
<br>
孔径光阑与入瞳
</p>

### 4.3 主光线与入瞳(Entrance Pupil)
入瞳可以确定孔阑对成像光束的限制(上图)。入瞳的大小与孔阑的大小成正比，但其位置可能与孔阑不同。在摄影用相机镜头中，入瞳通常是一个虚像，可以通过调整光圈来改变其大小。<br>
设想将孔阑缩小使其变为一个小孔，直至只有过孔阑中心的光线可以通过系统成像，这样的光线称为主光线。主光线定义了一个物点发出的光束在成像过程中的传播方向，此外，主光线与各光学面的交点又与像差有着十分紧密的联系，对像差校正有着十分重要的意义。理想情况下，不同物点发出的主光线交汇于孔阑中心，因此，主光线（或其延长线）也一定交汇于入瞳中心。与主光线相对应，经过孔阑（入瞳）边缘的光线，称为边缘光线。
<p align="center">
<img src="https://wiki.yanding.com/lib/exe/fetch.php?w=600&tok=ad619e&media=yanding:%E5%85%A5%E7%9E%B34.png" height = "300">
<br>
主光线与入瞳
</p>