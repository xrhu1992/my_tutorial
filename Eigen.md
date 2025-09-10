![Eigen](pic/eigen_logo.png)
# Eigen
*Eigen是一个专注于线性代数、矩阵运算及数值算法的高层次C++开源库，核心功能涵盖固定/动态尺寸矩阵、稀疏矩阵操作、标准及自定义数值类型支持，并提供矩阵分解、几何特征求解等算法。该库仅依赖C++标准库，通过纯头文件实现跨平台兼容，支持CMake构建和模块化调用，广泛应用于计算机视觉、机器人、人工智能等领域。*<br>
>[*Eigen官方文档*](https://libeigen.gitlab.io/eigen/docs-nightly/)
## Eigen库包含的模块
![Eigen Modules](pic/eigen_modules.png)
使用时一般包含Dense即可<br>
```cxx
#include <Eigen/Dense>
```
## 基本数据类型
* 固定大小类型
```cxx
// 矩阵
Matrix<float, 3, 3>
Matrix<double, 3, 3>
// 方阵
Matrix3d
Matrix3f
// 向量
Vector3f
Vector3d
```
* 动态大小类型
```cxx
// 动态大小矩阵
MatrixXf
MatrixXd
// 动态大小向量
VectorXf
VectorXd
```
* 特殊矩阵
```cxx
// 对角矩阵
DiagonalMatrix<T, Size>
// 稀疏矩阵
SparseMatrix<T>
// 示例
DiagonalMatrix<double, 3>
DiagonalMatrix<double, Dynamic>
SparseMatrix<double> sparse(1000,1000);
```
## 矩阵初始化
```cxx
// 零矩阵
Matrix3d zero = Matrix3d::Zero();
// 单位矩阵
Matrix3d identity = Matrix3d::Identity();
// 随机矩阵
Matrix3d random = Matrix3d::Random();
// 常数矩阵
Matrix3d constant = Matrix3d::Constant(1.0);
// 逗号初始化(矩阵阵列也可以初始化矩阵)
Matrix3d m;
m << 1, 2, 3,
     4, 5, 6,
     7, 8, 9;
```
## 元素访问
* 访问/修改元素
  - 使用 () 运算符：matrix(i,j)，可读写
  - 使用 .coeff(i,j) 只读访问，.coeffRef(i,j)可修改访问。有边界检查更安全
  - 行列访问：.row(i), .col(j)
```cxx
// ()访问
matrix(0,0) = 1.0; 
// .coeff()访问，只读
double val = matrix.coeff(i,j); 
// .coeffRef(访问)，可读写
matrix.coeffRef(i,j) = 2.0; 
// 获取第1行
auto row = matrix.row(0); 
// 获取第1列
Vector3d col =matrix.col(1); 
// 整行操作 
matrix.row(0).array() += 1.0;
```
* 矩阵块操作
  - 固定大小块：.block<p,q>(i,j)
  - 动态大小块：.block(i,j,p,q)
  - 行块：.row(i)
  - 列块：.col(j)
```cxx
// 提取2x2块，起始于(1,1)
Matrix4d m;
auto block = m.block<2,2>(1,1);
// 同样提取2x2块
MatrixXd m(4,4);
auto block = m.block(1,1,2,2);  
// 头尾部和边角
auto top_rows = m.topRows(2) // 前2行
auto bottom_cols = m.bottomCols(2) // 后2行
auto left_cols = m.leftCols(2) // 左2列
auto topLeft = m.topLeftCorner(2,2); // 左上角
auto bottomRight = m.bottomRightCorner(2,2); // 右下角
```
## 矩阵属性
* 大小：.rows(), .cols(), .size(), .empty()
* 最大/最小值：.maxCoeff(), .minCoeff()
* 和、平均：.sum()，.mean()
* 迹、行列式：.trace() .determinant()
* 范数：.lpNorm<1>(), .norm()
* 转置、逆：.tanspose(), .inverse()
* 其它：.isZero(), .isOnes(), .isIdentity(), .isDiagonal()
```cxx
// 带索引的最值查找
Matrix3d m = Matrix3d::Random();
Index max_row, max_col;
double max_val = m.maxCoedd(&max_row, &max_col); // 返回最大值的同时返回索引位置
```
## 向量创建和初始化
```cxx
// 固定大小向量，()初始化
Vector3d v1(1,2,3);
// 动态大小初始化，逗号初始化
VectorXd v2(5);
v2 << 1,2,3,4,5;
// 零向量
Vector3d v3 = Vector::Zero();
// 1向量
Vector3d v4 = Vector::Ones();
// 随机向量
Vector3d v5 = Vector::Random();
```
## 向量的访问
```cxx
// []或()访问，()检查边界更安全
double x = v1(0);
double y = v1(1);
// x y z访问，意义更明确
double z = v1.z();
// 获取前N/后N个元素
auto head = v1.head(2);
auto head = v1.tail(2);
```
## 向量的运算





