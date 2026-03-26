# Python Tutorial
> [Python官方教程](https://docs.python.org/zh-cn/3/tutorial/index.html)
> 
> [Python内置函数列表](https://docs.python.org/zh-cn/3/library/functions.html)
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
> [!NOTE]
> 1. *字符串是不可变的(Immutable)*
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
print(f'{name} is {age} years old.') # 使用格式化字符串字面值(f-string)
print('{0} is {1} years old.'.format(name, age)) # 使用位置参数
print(name + ' is ' + str(age) +' years old.') # 使用字符串拼接
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
### 2.3 比较
* 比较运算符(返回布尔值True或False)
  - `in` 和 `not in`用于执行确定一个值是否存在（或不存在）于某个容器中的成员检测
  - `is` 和 `is not`用于比较两个对象是否是同一个对象
  - 比较运算符优先级相同，且支持链式操作，如`a < b <= c`等同于`(a < b) and (b <= c)`
* 布尔运算符
  - 优先级顺序：`not`>`and`>`or`
  - 短路求值：`and`和`or`会根据第一个操作数的值决定是否计算第二个操作数
  ```python
  result_and = 1 and 2  # 第1个和第二个都为True，返回2
  result_or = 1 or 2    # 第一个为True，返回1
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
### 2.5 文件读写
* 打开文件
  ```python
  # 使用open()函数打开文件，返回文件对象
  file = open('example.txt', 'r')  # 'r'-只读模式，'w'-写入模式，'a'-追加模式
  # 读取整个文件内容
  content = file.read()
  print(content)
  file.close() # 关闭文件释放资源
  ```
  ```python
  # 逐行读取文件内容（句子结束后自动关闭文件）
  with open('example.txt', 'r') as file:
      for line in file:
          print(line, end='')  # end=''避免重复换行
  ```
* 写入文件内容
  ```python
  # 写入内容到文件
  with open('output.txt', 'w') as file:  # 'w'表示写入模式
      file.write('Hello, World!\n')
      file.write('This is a test file.\n')
  ```

## 3. 数据结构
### 3.1 List 列表  
* 简单的例子
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
* 列表常用方法
  ```python
  # 列表常用方法 
  list.append(6)    # 在列表末尾添加元素6，等同于list[len(list):]=[6]
  list.extend([7,8]) # 在列表末尾添加多个元素7和8，等同于list[len(list):]=[7,8]
  list.insert(2, 7) # 在索引2处插入元素7
  list.remove(1)    # 删除第一个值为1的元素
  list.pop()        # 删除并返回最后一个元素
  list.sort()       # 对列表进行排序
  list.reverse()    # 反转列表顺序
  index_of_5 = list.index(5)  # 获取值为5的元素的索引
  count_of_1 =list.count(1)   # 计算值为1的元素个数
  list.clear()      # 清空列表，等同于list[:] = []或del list[:]
  list.copy()       # 返回列表的浅拷贝，等同于list[:]
  ```
* 列表推导式
  ```python
  # 创建一个包含0到9的平方数的列表
  squares = [x**2 for x in range(10)]
  # 创建一个包含偶数的列表
  evens = [x for x in range(10) if x % 2 == 0]
  # 嵌套列表推导式，生成一个3x4的矩阵
  matrix = [
      [1, 2, 3, 4],
      [5, 6, 7, 8],
      [9, 10, 11, 12]
  ]
  # 转置矩阵，注意嵌套的for循环顺序
  matrix = [[row[i] for row in matrix] for i in range(4)]
  # 等同于
  transposed = []
  for i in range(4):
    transposed.append([row[i] for row in matrix])
  ``` 
* `del`语句删除列表元素
  ```python
  # 删除列表中的元素
  a = ['apple', 'banana', 'cherry', 'date']
  del a[1]        # 删除索引1处的元素 'banana'
  del a[1:3]     # 删除索引1到2的元素 'cherry' 和 'date'
  del a[:]       # 删除列表中的所有元素
  del a          # 删除整个列表变量
  ```
> [!NOTE]
> 1. *使用[ ]初始化列表；*
> 2. *列表里的元素可以是不同类型的；*
> 3. *列表是可变的(Mutable)*
> 4. *复制列表应使用切片操作，如`list_copy = list_original[:]`*

### 3.2 Tuple 元组
* Tuple 元组: <mark>**不可变的(Immutable)**</mark>
  ```python
  # 用()创建一个元组，可以是不同类型
  zoo = ('python','elephant','penguin') # 也可以不要括号
  new_zoo = ('monkey','camel',zoo)
  single_animal = ('only one',)  # 创建只有一个元素的元组，逗号不能省略
  ```

### 3.3 Set 集合 & Dictionary 字典
* **Set 集合**: <mark>**无序不重复**</mark>元素集合，支持数学集合操作（并集、交集、差集等）
  ```python
  # 创建一个集合(集合没有顺序概率，因此不能使用切片或索引)
  basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'} # 重复元素会被自动去除
  'oringe' in basket  # 检查元素是否在集合中，结果为True
  print(basket)  # 无序输出集合内容，重复元素只出现一次
  # 集合操作
  set1 = {1, 2, 3}
  set2 = {3, 4, 5}
  print(set1 | set2)  # 并集
  print(set1 & set2)  # 交集
  print(set1 - set2)  # 差集
  print(set1 ^ set2)  # 去除and b的交集后的并集
  ```

* Dictionary 字典: <mark>**键-值(key-value)对的无序集合**</mark>
  ```python
  # 创建一个字典
  ab = {
  'Swaroop': 'swaroop@swaroopch.com',
  'Larry': 'larry@wall.org',
  'Matsumoto': 'matz@ruby-lang.org',
  'Spammer': 'spammer@hotmail.com'} 
  print("Swaroop's address is", ab['Swaroop'])
  dic = dict(sape=4139, guido=4127, jack=4098) # 使用dict()创建字典

  # 删除一对键值—值配对
  del ab['Spammer']
  print('\nThere are {} contacts in the address-book\n'.format(len(ab)))
  for name, address in ab.items():
  print('Contact {} at {}'.format(name, address))

  # 添加一对键值—值配对
  ab['Guido'] = 'guido@python.org'
  if 'Guido' in ab:
  print("\nGuido's address is", ab['Guido'])

  # 字典常用方法
  list(ab.keys())    # 返回所有键的列表
  list(ab.values())  # 返回所有值的列表
  list(ab.items())   # 返回所有键-值对的列表
  ab.clear()        # 清空字典
  ab.copy()         # 返回字典的浅拷贝

  # 字典遍历
  for key in ab:
    print(key, '=>', ab[key])
  # 另一种遍历方式
  for key, value in ab.items():
    print(key, '=>', value)

  ```
  > [!NOTE]
  > *键(key)是不可变的，值(value)是可变的*

## 4. 函数与模块
### 4.1 函数
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

### 4.2 模块
* 模块(module): 一个包含Python定义和语句的文件，文件名以.py结尾，模块名即文件名去掉.py
  ```python
  # 编写一个模块 mymodule.py
  def greet(name):
      print("Hello, " + name + "!")
  ```

* 导入模块
  ```python
  # 1. 导入整个模块
  import mymodule
  mymodule.greet("Alice")  # 输出: Hello, Alice!
  # 模块名
  print(mymodule.__name__)  # 输出: mymodule
  # 2. 使用from-import语句导入模块中的特定函数
  from mymodule import greet
  greet("Bob")  # 输出: Hello, Bob!
  # 3. 使用as关键字为模块或函数指定别名
  import mymodule as mm
  mm.greet("Charlie")  # 输出: Hello, Charlie!
  from mymodule import greet as greeting
  greeting("David")  # 输出: Hello, David!
  ```

* 标准模块库
  ```python
  # 修改sys.path以包含自定义模块路径
  import sys
  sys.path.append('/path/to/your/module_directory')
  # 导入自定义模块
  import mymodule
  mymodule.greet("Eve")  # 输出: Hello, Eve!
  ```

* `dir()`函数列出模块中的所有属性和方法
  ```python
  import math
  print(dir(math))  # 输出math模块中的所有属性和方法
  ```
* 包：包含一系列模块.py的文件夹，文件夹内必须包含一个`__init__.py`文件（可以为空），例如
  ```
  sound/                          最高层级的包
        __init__.py               初始化 sound 包
        formats/                  用于文件格式转换的子包
                __init__.py
                wavread.py
                wavwrite.py
                aiffread.py
                aiffwrite.py
                auread.py
                auwrite.py
                ...
        effects/                  用于音效的子包
                __init__.py
                echo.py
                surround.py
                reverse.py
                ...
  ```
  ```python
  # 导入单个模块
  from sound.effects import echo # 导入echo模块
  echo.echofilter(input, output, delay=0.7, atten=4) # 使用echo模块中的echofilter函数
  # 或者
  import sound.effects.echo      
  sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
  # 导入多个模块
  from sound.effects import echo, surround
  ```
  ```python
  # 相对导入
  from . import echo             # 导入当前包中的echo模块
  from .. import formats         # 导入上级包中的formats模块
  from ..formats import wavread  # 从上级包的formats模块中导入wavread模块
  ```

## 5. 面向对象
### 5.1 类变量 & 对象变量
* 类变量：类的所有实例共享（类似C++的static），通过Class分配和引用（或`self.__class__.value`）
* 对象变量：每个实例独有，通过self分配和引用

### 5.2 类方法 & 静态方法
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


## 6. 常用
* `pass`站位符
```python
# 用于占位，什么都不做
while True:
    pass
```
* `range()` 生成整数序列
```python
range(5) # 0到4
range(2, 6)  # 2到5
range(1, 10, 2)  # 1到9，步长为2
list(range(5))  # [0, 1, 2, 3, 4]
# 生成一个整数序列
for i in range(1, 10, 2):  # 1到9，步长为2
    print(i, end=' ')
```
* `zip()` 打包
```python
# 将多个可迭代对象打包成元组列表
names = ['Alice', 'Bob', 'Charlie']
ages = [25, 30, 35]
for name, age in zip(names, ages):
    print(f'{name} is {age} years old.')
```
* `shuffle()` 随机打乱顺序
```python
import random
items = [1, 2, 3, 4, 5]
random.shuffle(items)
print(items)  # 输出打乱顺序后的列表
```


