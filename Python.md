# Python
## 注意事项
* shell下输入python3进入python环境，exit()退出
* python下标从0开始
* 使用help()查看帮助
  ```python
  # 查看关于int的帮助，按q退出
  help(int)
  ```
## 基础语法
* **字符串**<br>
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
* **控制流**<br>
  - if-else
    ```python
    # if-else语句(注意':'不能缺少)
    if a==b:
        func1()
    elif a<b:
        func2()
    else:
        func3()
    ```
  - while
    ```python
    # while语句(注意':'不能缺少)
    while condition:
        func1()
    else:
        func2()
    ```
  - for
    ```python
    # for循环(注意':'不能缺少)
    for i in rang(1,5):
        func1()
    else:
        func2()
    ```
* **函数**<br>
  - 定义一个函数
    ```python
    # 定义一个函数
    def func(a, b, c=0):
        d=a+b+c
        return d
    # 使用函数
    print(func(1,b=2))
    ```
  - DocString
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
* **模块**
    ```python
    # 导入一个模块(标准库模块)
    import sys
    # 导入模块中的某一功能
    from math import sqrt
    ```
  *包：包含一系列模块.py的文件夹*
* **基本数据结构**  
  - List 列表  
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
  - Tuple 元组
    ```python
    # 用()创建一个元组，可以是不同类型
    zoo = ('python','elephant','penguin')
    new_zoo = ('monkey','camel',zoo)
    ```
    *注意：*
    1. *使用( )初始化列表；*
    2. *元组是不可变的(Immutable)*
  - Dictionary 字典
    ```python
    
    ```
  - Set 集合
  - $\alpha$


  
