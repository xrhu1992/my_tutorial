# 手持式3D扫描仪(Handheld Laser 3D Scanner)

## 1. 扫描模式（Scanning Mode）
以 [Artec Point](https://www.artec3d.cn/portable-3d-scanners/laser-point#overview) 为例，其具有三种扫描模式：
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/Artec3D-1.png" width = "300">
<br>Artec Point Metrology-grade handheld laser 3D scanner</p>

- **超快速扫描模式（Ultra-fast scanning mode）：** 适用于快速捕捉大面积物体的表面几何形状。使用17×17的交叉激光网格快速捕捉大型物体，精准高效地加速工作流程，同时将多边形数量降至最低，实现轻量化的3D模型。缺点是细节较少。
<p align="center">
<video src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/video/artec-point-mode-1.mp4" width = "450" loop controls></video>
<br>Ultra-fast scanning</p>

- **超精细扫描模式（Hyper-fine scanning mode）：** 适用于需要高分辨率的场景。使用7条平行激光束扫描。
<p align="center">
<video src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/video/artec-point-mode-2.mp4" width = "450" loop controls></video>
<br>Hyper-fine scanning</p>

- **深孔扫描模式（Deep hole scanning mode）：** 适用于深孔、凹槽等难以接触的区域。使用单条激光线扫描，捕捉难以接触的区域。缺点是扫描速度较慢。
<p align="center">
<video src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/video/artec-point-mode-3.mp4" width = "450" loop controls></video>
<br>Deep hole scanning</p>

## 2. 光源分析（Light Source Analysis）
- **蓝光多线激光：** 扫描仪中间四颗光源为多通道线激光光源，其中左右两颗为斜向平行的多线激光，构成平行交叉多线激光，分时点亮，用于快速扫描模式。上下两颗光源分别为单线和平行多线激光，分别用于深孔扫描模式和超精细。
- **标记点蓝光补光光源：** 推测扫描仪上下两处环形光源为蓝光补光光源，为拍摄标记点提供照明。其点亮时序可能是与线激光分时的（无干扰易检测，但有运动延时且降低扫描帧率），也可能与线激光同时点亮（线激光干扰，标记点易检测失败，但无运动延时且帧率高）。

## 3. 供应商（Suppliers）
### 3.1 多线激光
- [东莞蓝宇激光](https://www.bu-laser.com/product/39/)
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/bu-laser-1.jpg" height = "200">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/bu-laser-2.jpg" height = "200">
<br>450nm1.6W多通道激光器（交叉线7线+7线+1线）</p>

- [西安赫胥尔镭得激光](http://www.xahxrld.com/product/81.html)
<p align="center">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/LD-4A-1.jpg" height = "150">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/LD-4A-2.jpg" height = "150">
<br>多通道激光器LD-4A<br>
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/LD-5A-1.jpg" height = "150">
<img src="https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/tutorial/LD-5A-2.jpg" height = "150">
<br>多通道激光器LD-5A-450</p>

- [常熟德晟光电](https://www.dershinelaser.com/product/?yingyong=5)
  - 据该公司老板称，国内头部扫描仪厂商均使用其激光器产品，如先临、创想、中观、启源、派姆特、惟景。我司与其也有合作。
  - [产品手册](https://pub-4f6dc840a1174fbebb56297e77b4fc2f.r2.dev/doc/%E5%BE%B7%E6%99%9F%E5%85%89%E7%94%B5%E4%BA%A7%E5%93%81%E6%89%8B%E5%86%8C-24.pdf)




