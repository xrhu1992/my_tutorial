# Python
## 注意事项
* shell下输入`python3`或`py`进入python环境，`exit()`退出
* python下标从0开始
* 使用help()查看帮助
  ```python
  # 查看关于int的帮助，按q退出
  help(int)
  ```
## 基础语法
### 字符串
```python
# 使用单引号'string' 或双引号"string"括起来的文本被称为字符串
'This is a string'
"This is also a string"
# 使用三引号'''string''' 或 """string"""括起来的文本被称为多行字符串
'''This is a 
multi-line string'''
"""This is also a 
multi-line string"""
# 格式化输出
age = 20
name = 'Bander'
print('{0} is {1} years old.'.format(name, age))
print(name + ' is ' + str(age) +' years old.')
# 为避免转义字符干扰，可使用原始字面量
R"Newlines are indicated by \n"
```
*注意：字符串是不可变的*
### 控制流
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
* for
  ```python
  # for循环(注意':'不能缺少)
  for i in rang(1,5):
      func1()
  else:
      func2()
  ```
### 函数
* 定义一个函数
  ```python
  # 定义一个函数
  def func(a, b, c=0):
      d=a+b+c
      return d
  # 使用函数
  print(func(1,b=2))
  ```
* DocString
  ```python
  # 对函数功能的描述，使用.__doc__输出
  def print_max(x, y):
      '''
      打印两个数值中的最大数。
      这两个数都应该是整数
      '''
      # 如果可能，将其转换至整数类型
      x = int(x)
      y = int(y)
      if x > y:
          print(x, 'is maximum')
      else:
          print(y, 'is maximum')
  # 显示函数注释内容
  print(print_max.__doc__)
  ```
### 模块
  ```python
  # 导入一个模块(标准库模块)
  import sys
  # 导入模块中的某一功能
  from math import sqrt
  ```
*包：包含一系列模块.py的文件夹*
### 基本数据结构  
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
  ```
  *注意：*
  1. *使用[ ]初始化列表；*
  2. *列表里的元素可以是不同类型的；*
  3. *列表是可变的(Mutable)*
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
## 面向对象
### 类变量 & 对象变量
* 类变量：类的所有实例共享（类似C++的static），通过Class分配和引用（或`self.__class__.value`）
* 对象变量：每个实例独有，通过self分配和引用

## 类方法 & 静态方法
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
### 继承
* 支持单继承和多继承
* 使用`super()`调用父类方法
```pythonpython
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
### 魔术方法







  
