# Python Tutorial
> [Python官方教程](https://docs.python.org/zh-cn/3/tutorial/index.html)
## 1. 如何使用
### 1.1 进入python解释器环境
* shell下输入`python3`或`py`进入python环境，`exit()`或`quit()`退出
* 使用`help()`查看帮助
  ```python
  # 查看关于int的帮助，按q退出
  help(int)
  ```
### 1.2 脚本参数
* 使用`sys.argv`获取脚本参数
  ```python
  import sys
  print('Script name:', sys.argv[0])
  for i in range(1, len(sys.argv)):
      print('Argument {}: {}'.format(i, sys.argv[i]))
  ```
### 1.3 源文件字符编码
* 在源文件开头添加`# -*- coding: utf-8 -*-`指定编码格式为utf-8
---
## 2. 基础语法
### 2.1 基本运算
* 基本运算符
```python
17/3     # 除法，结果为浮点数 5.6666666666666
17//3    # 整除，结果为整数 5
17%3     # 取模，结果为1
2**3     # 幂运算，结果为8
```
* 交互模式下，上次输出的表达式会赋给变量 _（当作计算器用时比较方便）
```bash
>>> 100+200
300.0
>>> _ * 1.5 # 上次结果乘以1.5
450.0
```
* 一个简单的例子
```python
# 交换两个数的值
a, b = 5, 10
a, b = b, a
# 使用print()输出结果
print("a =", a, "b =", b,end=",")  # end参数指定结尾符
print("a={}, b={}".format(a,b))  # 使用format格式化输出
```
### 2.2 字符串
* 定义字符串
```python
# 使用单引号'string' 或双引号"string"(没有区别)括起来的文本被称为字符串
"This is also a string"
# 使用三引号'''string''' 或 """string"""括起来的文本被称为多行字符串
"""This is a 
multi-line string"""
```
* 格式化输出 `format()`
```python
age = 20
name = 'Bander'
print('{0} is {1} years old.'.format(name, age))
print(name + ' is ' + str(age) +' years old.')
```
* 转义字符
```python
# 常用转义字符
\n  # 换行
\t  # 制表符
\\  # 反斜杠
\'  # 单引号
\"  # 双引号
# 为避免转义字符干扰，可使用原始字面量
R"Newlines are indicated by \n"
```
> [!NOTE]
> 1. *字符串是不可变的(Immutable)*

### 2.3 基本数据结构  
* List 列表  
  ```python
  # 用[]创建一个列表，可以是不同类型
  fruits = ['apple','mango',100,'banana']
  # 使用for循环打印内容，空格结尾
  for item in fruits
      print(item, end=' ')
  # 使用append向列表尾追加
  fruits.append('pear')
  # 删除一个元素 100
  del fruits[2]
  # 列表支持合并操作
  fruits_and_veggies = fruits + ['tomato','potato']
  # 列表切片操作（索引范围不包含末尾）
  print(fruits[1:3])  # 输出索引1到2的元素
  ```
  > [!NOTE]
  > 1. *使用[ ]初始化列表；*
  > 2. *列表里的元素可以是不同类型的；*
  > 3. *列表是可变的(Mutable)*
  > 4. *复制列表应使用切片操作，如`list_copy = list_original[:]`*

* Tuple 元组
  ```python
  # 用()创建一个元组，可以是不同类型
  zoo = ('python','elephant','penguin')
  new_zoo = ('monkey','camel',zoo)
  ```
  *注意：*
  1. *使用( )初始化列表；*
  2. *元组是不可变的(Immutable)*
* Dictionary 字典
  ```python
  # “ab”是地址（ Address） 簿（ Book） 的缩写
  ab = {
  'Swaroop': 'swaroop@swaroopch.com',
  'Larry': 'larry@wall.org',
  'Matsumoto': 'matz@ruby-lang.org',
  'Spammer': 'spammer@hotmail.com'} 
  print("Swaroop's address is", ab['Swaroop'])

  # 删除一对键值—值配对
  del ab['Spammer']
  print('\nThere are {} contacts in the address-book\n'.format(len(ab)))
  for name, address in ab.items():
  print('Contact {} at {}'.format(name, address))

  # 添加一对键值—值配对
  ab['Guido'] = 'guido@python.org'
  if 'Guido' in ab:
  print("\nGuido's address is", ab['Guido'])
  ```
  *注意：*
  1. *使用{ }初始化列表；*
  2. *键(key)是不可变的，值(value)是可变的*
* Sequence 序列 & Set 集合
  - Sequence: 包含List和Tuple，支持索引和切片操作
  - Set: 无序不重复元素集合，支持数学集合操作（并集、交集、差集等）
  - 常用操作
    ```python
    # 序列操作
    seq = [1, 2, 3, 4, 5]
    print(seq[0])      # 索引访问
    print(seq[1:4])    # 切片访问

    # 集合操作
    set1 = {1, 2, 3}
    set2 = {3, 4, 5}
    print(set1 | set2)  # 并集
    print(set1 & set2)  # 交集
    print(set1 - set2)  # 差集

    # 序列的拷贝
    seq_copy = seq # 引用同一对象，而非副本拷贝
    seq_copy = seq[:]  # 序列的副本拷贝
    ```
### 2.4 控制流
* if-else
  ```python
  # if-else语句(注意':'不能缺少)
  if a==b:
      func1()
  elif a<b:
      func2()
  else:
      func3()
  ```
* while
  ```python
  # while语句(注意':'不能缺少)
  while condition:
      func1()
  else:
      func2()
  ```
* match case (Python 3.10+)
  ```python
  # match-case语句(注意':'不能缺少)
  # 只有第一个被命中的case会被执行
  match status:
      case 100:
          func1()
      case 200 | 201:  # 多个值匹配
          func2()
      case _:  # _ 默认情况
          func3()
  ```
* for
  ```python
  # for循环(注意':'不能缺少)
  for i in rang(1,5):
      func1()
  else:
      func2()
  ```
### 2.5 函数
* 定义一个函数
  ```python
  def ask_ok(prompt, retries=4, reminder='Please try again!'):
      # 对函数功能的描述，通过.__doc__输出
      '''
      根据用户输入的'y'或'n'返回True或False
      prompt: 提示信息
      retries: 重试次数
      reminder: 重试提示信息
      '''
    while True:
        reply = input(prompt)
        if reply in {'y', 'ye', 'yes'}:
            return True
        if reply in {'n', 'no', 'nop', 'nope'}:
            return False
        retries = retries - 1
        if retries < 0:
            raise ValueError('invalid user response')
        print(reminder)

  # 显示函数注释内容
  print(print_max.__doc__)
  # 调用函数
  is_ok=ask_ok('Do you really want to quit?')
  ```
  * *name(元组) 和 **name(字典) 用于传递可变数量的参数*
  ```python
  def total(a=5, *numbers, **phonebook):
      print('a', a)
      # 遍历元组中的所有项目
      for single_item in numbers:
          print('single_item', single_item)
      # 遍历字典中的所有项目
      for first_part, second_part in phonebook.items():
          print(first_part, second_part)
  # 调用函数
  total(10, 1, 2, 3, Jack=1123, John=2231, Inge=1560)
  ```

### 2.6 模块
  ```python
  # 导入一个模块(标准库模块)
  import sys
  # 导入模块中的某一功能
  from math import sqrt
  ```
*包：包含一系列模块.py的文件夹*
## 3. 面向对象
### 3.1 类变量 & 对象变量
* 类变量：类的所有实例共享（类似C++的static），通过Class分配和引用（或`self.__class__.value`）
* 对象变量：每个实例独有，通过self分配和引用

### 3.2 类方法 & 静态方法
* 类方法：使用`@classmethod`装饰器，第一个参数为cls，表示类本身
* 静态方法：使用`@staticmethod`装饰器，无需传递类或实例参数
```python
class MyClass:
    class_variable = 0  # 类变量
    def __init__(self, value):
        self.instance_variable = value  # 对象变量
    @classmethod
    def class_method(cls):
        print("This is a class method. Class variable:", cls.class_variable)
    @staticmethod
    def static_method():
        print("This is a static method.")
# 使用类方法和静态方法
MyClass.class_method()
MyClass.static_method()
``` 
### 3.3 继承
* 支持单继承和多继承
* 使用`super()`调用父类方法
```python
class Parent:
    def show(self):
        print("This is the Parent class.")
class Child(Parent):
    def show(self):
        super().show()  # 调用父类方法
        print("This is the Child class.")
# 创建Child类实例并调用show方法
c = Child()
c.show()
```





## 常用
* `pass`站位符
```python
# 用于占位，什么都不做
while True:
    pass
```
* `range()`函数
```python
range(5) # 0到4
range(2, 6)  # 2到5
range(1, 10, 2)  # 1到9，步长为2
list(range(5))  # [0, 1, 2, 3, 4]
# 生成一个整数序列
for i in range(1, 10, 2):  # 1到9，步长为2
    print(i, end=' ')
```
* 列表推导式
```python
# 创建一个包含0到9的平方数的列表
squares = [x**2 for x in range(10)]
print(squares)
# 创建一个包含偶数的列表
evens = [x for x in range(10) if x % 2 == 0]
print(evens)
```
