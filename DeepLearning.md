# Deep Learning
> [Neural Network and Deep Learning-ch](doc/Neural%20Network%20and%20Deep%20Learning-ch.pdf)
>
> [PaddlePaddle 教程](https://www.paddlepaddle.org.cn/tutorials/projectdetail/5604804)

## 1. 基础概念
### 1.1 激活函数 (Activation Function)
激活函数是神经网络中的关键组件，决定了神经元的输出。
* 激活函数的选择
  - 目的：<mark>引入非线性</mark>，使神经网络能够学习复杂的模式。
  - 原则：连续可导，且计算简单，这样便于反向传播算法的实现。
* 常见类型  
  常用的激活函数包括ReLU、Sigmoid和Tanh。ReLU在隐藏层中表现良好，而Sigmoid和Tanh适用于输出层。
  - Sigmoid：将输入映射到(0, 1)区间，常用作二分类问题的输出层激活函数。但是在深层网络中，由于**梯度消失**问题，Sigmoid函数在反向传播时的效果不是很好。
  ```math
  \text{Sigmoid}(x) = \frac{1}{1 + e^{-x}}
  ```
  - ReLU：输出为输入的最大值，即`max(0, x)`。简单且计算效率高，解决了梯度消失问题，但是在输入为负数时会导致“死亡ReLU”问题（即梯度为0，无法更新权重）。
  ```math
  \text{ReLU}(x) = \max(0, x)
  ```
  - Tanh：将输入映射到(-1, 1)区间，与Sigmoid函数类似，但是输出的均值为0，这在某些情况下更方便。
  ```math
  \text{Tanh}(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}
  ```
  <p align="center">
  <img src="https://ai-studio-static-online.cdn.bcebos.com/56c693f93293460498f0b37a7472ee037c7224c4bcb4435c8bf0450ce7abc6cc" height="180">
  <img src="https://ai-studio-static-online.cdn.bcebos.com/56c693f93293460498f0b37a7472ee037c7224c4bcb4435c8bf0450ce7abc6cc" height="180">
  <img src="https://ai-studio-static-online.cdn.bcebos.com/05510f67623b4dfb83460e30ed4084fac10d2759f3084fd0a57b1394ad4f09e8" height="180">
  <br>Sigmoid / ReLU / Tanh<br>
  </p>
### 1.2 损失函数 (Loss Function)
有时也被称为代价函数或目标函数。损失函数用于衡量模型预测值与真实值之间的差距，是训练过程中优化的目标。
* 常见损失函数 
  - 均方误差 (Mean Squared Error, MSE)：适用于回归问题，计算预测值与真实值之间的平方差的平均值。
  ```math
  \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
  ```
  - 交叉熵损失 (Cross-Entropy Loss)：适用于分类问题，衡量两个概率分布之间的差异。
  ```math
  \text{Cross-Entropy} = -\sum_{i=1}^{n} y_i \log(\hat{y}_i)
  ```
### 1.3 优化算法 (Optimization Algorithms)
优化算法用于调整神经网络的权重，以最小化损失函数。 常见的优化算法包括随机梯度下降 (SGD)、Adam和RMSprop。
* 随机梯度下降 (SGD)：每次迭代使用<mark>一个小样本</mark>进行权重更新(epoch)，计算效率高，但收敛速度较慢且不稳定。
  ````math
  \theta_t = \theta_{t-1} - \alpha \cdot \nabla L(\theta_{t-1})
  ````
  其中，$\theta_t$ 是第 $t$ 次迭代的参数值，$\alpha$ 是学习率，$\nabla L(\theta_{t-1})$ 是损失函数 $\mathcal{L}$ 对参数 $\theta_{t-1}$ 的梯度。

* 动量梯度下降 (Momentum GD)：在SGD的基础上引入动量项，加速收敛并避免局部最优解。
  ```math
  \theta_t = \theta_{t-1} - \alpha \cdot v_t
  ```
  其中，$\theta_t$ 是第 $t$ 次迭代的参数值，$\alpha$ 是学习率，$v_t$ 是动量项，定义为：
  ```math
  v_t = \beta \cdot v_{t-1} - \alpha \cdot \nabla L(\theta_{t-1})
  ```
  其中，$\beta$ 是动量系数，$\nabla L(\theta_{t-1})$ 是损失函数 $\mathcal{L}$ 对参数 $\theta_{t-1}$ 的梯度。