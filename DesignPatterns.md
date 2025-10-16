# 设计模式 (Design Patterns)
> [爱编程的大丙](https://subingwen.cn/design-patterns/#3-%E7%BB%93%E6%9E%84%E5%9E%8B%E6%A8%A1%E5%BC%8F)

## 设计模式三原则
* **单一职责原则** C++面向对象三大特性之一的封装指的就是将单一事物抽象出来组合成一个类，所以我们在设计类的时候每个类中处理的是单一事物而不是某些事物的集合。

设计模式中所谓的单一职责原则，就是对一个类而言，应该仅有一个引起它变化的原因，其实就是将这个类所承担的职责单一化（就跟海贼王中的能力者一样，每个人只能吃一颗恶魔果实，拥有某一种能力【黑胡子这个Bug除外】）。

如果一个类承担的职责过多，就等于把这些职责耦合到了一起，一个职责的变化可能会削弱或者抑制这个类完成其他职责的能力。这种耦合会导致设计变得脆弱，当变化发生时，设计会遭受到意想不到的破坏。







---
## UML类图

* **类(Class)**： 上层是类名，中间层是属性（类的成员变量），下层是方法（类的成员函数）  
  - 可见性：+ 表示public、# 表示protected、- 表示private、__(下划线)表示static
  - 属性的表示方式：[可见性][属性名称]:[类型]= { 缺省值，可选 }
  - 方法的表示方式：[可见性][方法名称]([参数名 : 参数类型，……]）:[返回值类型]<br>
![UML_class](pic/DesignPatterns/UML_class.png)  

* **抽象类(Abstract)**： 对于抽象类（类中有虚函数），类名使用***斜体***显示
  - 虚函数也使用斜体表示
  - 纯虚函数需要指定=0<br>
![UML_abstract](pic/DesignPatterns/UML_abstract.png) 

* **继承关系(Generalization)**： 使用**带空心三角形箭头的实线指向父类**<br>
![UML_generalization](pic/DesignPatterns/UML_generalization.png)

* **关联关系(Assocition)**： 一个类被另一个类包含（作为成员变量）
  - **单向关联**：使用带单向箭头的实线指向被包含的类<br>
  ![UML_association](pic/DesignPatterns/UML_association_1.png)
  - **双向关联**：使用带双向箭头或不带箭头的实线指向被包含的类<br>
  ![UML_association](pic/DesignPatterns/UML_association_2.png)
  ![UML_association](pic/DesignPatterns/UML_association_3.png)
  - **自关联**：使用带单向箭头的实线指向自己<br>
  ![UML_association](pic/DesignPatterns/UML_association_4.png)

* **聚合关系(Aggregation)**： 表示**整体**与**部分**的关系，成员对象是整体的一部分，但是成员对象可以脱离整体对象独立存在（例如：Forest与Plant、Animal、Water、Sunshine）。聚合关系用**带空心菱形的直线**表示。<br>
![UML_aggregation](pic/DesignPatterns/UML_aggregation.png)

* **组合关系(Composition)**： 也表示**整体**与**部分**的关系，但组合关系中整体对象可以控制成员对象的生命周期，一旦整体对象不存在，成员对象也不存在，整体对象和成员对象之间具有同生共死的关系（例如：Tree和Root、Trunk、Branch、Leaf）。组合关系用**带实心菱形的直线**表示。<br>
![UML_aggregation](pic/DesignPatterns/UML_composition.png)

* **依赖关系(Dependency)**： 是一种使用关系，特定事物的改变有可能会影响到使用该事物的其他事物，在需要表示一个事物使用另一个事物时使用依赖关系，大多数情况下依赖关系体现在某个类的方法使用另一个类的对象作为参数（例如：树木（Tree）的生长，需要将空气（Air）、水（Water）、土壤（Soil）对象作为参数传递给 Tree 类的 grow（）方法）。依赖关系用**带箭头的虚线**表示，由依赖的一方指向被依赖的一方。依赖关系通常通过三种方式来实现：
  - 将一个类的对象作为另一个类中方法的参数
  - 在一个类的方法中将另一个类的对象作为其对象的局部变量
  - 在一个类的方法中调用另一个类的静态方法<br>
![UML_aggregation](pic/DesignPatterns/UML_dependency.png)


