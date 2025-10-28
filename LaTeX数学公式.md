# LaTeX数学公式
## **基本语法结构**
* **$\lceil$行中公式$\rfloor$和$\lceil$独立公式$\rfloor$**<br>
  - 行中公式一般为单独行或嵌入在文本中，写法为<br>
    `$ 数学公式 $`  
    `上文 $a + b = c$ 下文`<br>
    显示为  
    上文 $a + b = c$ 下文
  - 独立公式一般为单独行或段，并以双斜杠\\\续行，写法为<br>
    `$$ 数学公式 $$`
    或\```math  数学公式 ```（这种写法可兼容Github显示）
    ```
    $$
    x + y = 10 \\
    x - y = 6 \\
    2x = 16 \\
    x = 8 \\
    y = 2
    $$
    ```
    显示为
    $$
    x + y = 10 \\
    x - y = 6 \\
    2x = 16 \\
    x = 8 \\
    y = 2
    $$

    ```math
    x + y = 10 \\
    x - y = 6 \\
    2x = 16 \\
    x = 8 \\
    y = 2
    ```
* **基本表示方法**
  - **希腊字母&命令**：以反斜杠 \ 开头<br>
    ` \alpha \sum `  显示为：$\alpha$ $\sum$
  - **参数**：用花括号 { } 包围<br>
    `\frac{a}{b}`  显示为：$\frac{a}{b}$
  - **上下标**：上标 ^, 下标 _<br>
    `x^2 x_2`  显示为：$x^2$  $x_2$
  - **分组**：用花括号将多个字符组合<br>
    `x_{i+1}`  显示为：$x_{i+1}$
## **希腊字母**
![希腊字母](pic/markdown/greek_letters.png)

## **运算符**
* **四则运算**
  - 加减 `x+y=z`  $x+y=z$
  - 正负号 `x \pm y`  $x \pm y$
  - 叉乘 `x \times y=z`  $x \times y=z$
  - 点乘 `x \cdot y=z`  $x \cdot y=z$
  - 星乘 `x \ast y=z`  $x \ast y=z$
  - 除法 `x \div y=z`  $x \div y=z$
  - 斜除 `x/y=z`  $x/y=z$
  - 分式1(fraction) `\frac{x+y}{a+b}`  $\frac{x+y}{a+b}$
  - 分式2 `{x+y} \over {a+b}`  ${x+y} \over {a+b}$
  - 绝对值 `|x+y|`  $|x+y|$
* **逻辑运算符**
  - 大于  `x>y` $x>y$
  - 大于等于  `x>=y` $x>=y$
* **高等运算符**
  - 平均数  `\overline{xyz}` $\overline{xyz}$
  - 二次方根  `\sqrt x` $\sqrt x$
  - 三次方根  `\sqrt[3] {x+y}` $\sqrt[3] {x+y}$
  - 对数 `\log(x)` $\log(x)$
  - 极限 `\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}` $\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$
  - 求和1 `\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}` $\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$
  - 求和2 `\displaystyle \sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}` $\displaystyle \sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$
  - 积分1 `\int^{\infty}_{0}{xdx}` $\int^{\infty}_{0}{xdx}$
  - 积分2 `\displaystyle \int^{\infty}_{0}{xdx}` $\displaystyle \int^{\infty}_{0}{xdx}$
  - 微分 `\frac{\partial x}{\partial y}` $\frac{\partial x}{\partial y}$

## **数学结构**
![数学结构](pic/markdown/math_constructs.png)
$\frac{abc}{xyz}$  
$\overrightarrow{v}$
## **定界符**
![定界符](pic/markdown/delimiters.png)
*注：将定界符与\left和、right组合使用可以自动匹配内容高度，适合矩阵形式的书写*<br>
$[$ $x$ $y$ $z$ $]$
## **矩阵**  
  ```
  \begin{类型}
  公式
  \end{类型}
  ```
* 矩阵中的元素用&分割，双反斜杠\\\换行*<br>
* 类型可以是：矩阵 `matrix` `pmatrix`(A) `bmatrix`[A] `Bmatrix`{A} `vmatrix`|A| `Vmatrix`||A||、条件表达式 `cases`、多行对齐方程式 `aligned`、数组 `array`
* 有框矩阵，将 `matrix` 替换为 `pmatrix`(A) `bmatrix`[A] `Bmatrix`{A} `vmatrix`|A| `Vmatri`||A||
  ```
  \begin{vmatrix}
  x & y \\
  z & v
  \end{vmatrix}
  ```
  ``` math
  \begin{vmatrix}
  x & y \\
  z & v
  \end{vmatrix}
  ```
    ```
  \begin{Vmatrix}
  x & y \\
  z & v
  \end{Vmatrix}
  ```
  ``` math
  \begin{Vmatrix}
  x & y \\
  z & v
  \end{Vmatrix}
  ```
* 使用 `\cdots` ⋯ `\ddots` ⋱ `\vdots` ⋮ 来输入省略符号
  ```
  \begin{bmatrix}
  0      & \cdots & 0      \\
  \vdots & \ddots & \vdots \\
  0      & \cdots & 0
  \end{bmatrix}
  ```
  ```math
  \begin{bmatrix}
  0      & \cdots & 0      \\
  \vdots & \ddots & \vdots \\
  0      & \cdots & 0
  \end{bmatrix}
  ```



