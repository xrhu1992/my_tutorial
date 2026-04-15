# 线性代数（Linear Algebra）

# 1. 向量运算（Vector Operations）
## 1.1 叉乘（Cross Product）
### 1.1.1 定义与性质
- **定义:** 对于两个三维向量$\overrightarrow{a}=(a_x,a_y,a_z)^T$和$\overrightarrow{b}=(b_x,b_y,b_z)^T$，它们的叉乘定义为：
  $$\overrightarrow{a} \times \overrightarrow{b} = (a_y b_z - a_z b_y, a_z b_x - a_x b_z, a_x b_y - a_y b_x)^T$$
  可根据右手定则确定叉乘的方向（与两个向量都垂直）。
- **性质:**
  - 反对称性：$\overrightarrow{a} \times \overrightarrow{b} = -(\overrightarrow{b} \times \overrightarrow{a})$
  - 分配律：$\overrightarrow{a} \times (\overrightarrow{b} + \overrightarrow{c}) = \overrightarrow{a} \times \overrightarrow{b} + \overrightarrow{a} \times \overrightarrow{c}$
  - 与标量的关系：$(k\overrightarrow{a}) \times \overrightarrow{b} = k(\overrightarrow{a} \times \overrightarrow{b})$，其中$k$为标量
  - 与点积的关系：$\overrightarrow{a} \cdot (\overrightarrow{b} \times \overrightarrow{c}) = (\overrightarrow{a} \times \overrightarrow{b}) \cdot \overrightarrow{c}$，这是一个标量值，称为混合积（Scalar Triple Product），表示三个向量构成的平行六面体的体积。
  - 若$\overrightarrow{a}$和$\overrightarrow{b}$平行，则$\overrightarrow{a} \times \overrightarrow{b} = \overrightarrow{0}$。
### 1.1.2 矩阵型式
- 叉乘可以表示为一个3x3反对称矩阵与向量的乘积：
  $$\overrightarrow{a} \times \overrightarrow{b} = [\overrightarrow{a}]_\times \overrightarrow{b}$$
  其中$[\overrightarrow{a}]_\times$是由$\overrightarrow{a}$构成的反对称矩阵：
  $$[\overrightarrow{a}]_\times = \begin{bmatrix}
  0 & -a_z & a_y \\
  a_z & 0 & -a_x \\
  -a_y & a_x & 0
  \end{bmatrix}$$
  并且
  $$\overrightarrow{a} \times \overrightarrow{b} = [\overrightarrow{a}]_\times \overrightarrow{b} = (\overrightarrow{a}^T[\overrightarrow{b}]_\times)^T$$