
这演示了`return`语句如何将值传回调用者，同时也演示了函数如何对列表执行一种操作而对字符串执行另一种操作。这里的魔法是由对象完成的。我们编写一个函数告诉两个对象相加，而对象内部知道如何这样做。如果它们不知道——例如，用户传入了一个字符串和一个整数——Python 会为我们捕获错误。然而，这种“放手不管，让对象自己解决”的态度使得函数变得如此灵活。我们的`concat()`函数理论上可以连接字符串、列表或`zorks`——一种某人自己创建的、允许相加的数据类型。点在于，我们没有限制函数能做什么——尽管听起来可能很俗气，唯一的限制就是我们的想象力！

## 对象导向

读到这里，如果你已经使用了多年类 C 语言，那么听到 Python 的对象导向是如此灵活的，并且很可能会让你感到惊讶。

学习 Python 面对象编程 (OOP) 的最佳方法就是直接实践。因此，这里有一个基础脚本，定义了一个类，创建了该类的对象并调用了一个函数：

```python
class dog(object):

    def bark(self):

        print("Woof!")
```

```python
fluffy = dog()

fluffy.bark()
```

定义类正如预期的那样，是以`class`关键字开始，后面跟着你定义的类名和冒号。该类的内容需要缩进一层，以便 Python 知道何时结束。注意，括号内的对象用于对象继承，这将在稍后讨论。目前，你至少需要知道的是，如果你的新类不是基于现有类，你应该像前面的代码所示在括号中放入`object`。

类内部的函数工作方式与普通函数非常相似（尽管它们被称为方法），主要区别在于它们都至少接受一个参数，通常称为`self`。这个参数被填充为调用该函数的对象的名称，你需要显式地使用它。

通过赋值来创建类的实例。你不需要像某些其他语言那样使用任何新的`new`关键字——只需提供空括号即可。调用该对象的方法使用点号`.`、加上要调用的名，并将任何参数传递在括号内。

## 类变量和对象变量

每个对象都有它们自己的函数和变量，你可以独立于同类型的对象来操作这些变量。此外，某些类变量被设置为所有类的默认值，并可以全局操作。

此脚本演示了创建了两个`dog`类的对象，每个都有自己的名称：

```python
class dog(object):

    name = "Lassie"

    def bark(self):

        print self.name + " Woof!"

    def setName(self, name):

        self.name = name

fluffy = dog()

fluffy.bark()

poppy = dog()

poppy.bark()

poppy.setName("Poppy")

poppy.bark()
```

输出结果：

```
Lassie Woof!
Poppy Woof!
Poppy Woof!
```

（等待，提供的 OCR 文本在后半部分似乎混乱/重复。我将根据提供片段的逻辑流进行清理。）

*注：提供的第 695-697 页 OCR 文本包含大量重复和碎片句子。我根据可用片段重构了逻辑结构。*

## 构造函数和析构函数

析构函数的作用是给你释放资源的机会。

## 类继承

Python 允许你通过继承一个多个类来重用代码。例如，狮子、老虎和熊都是哺乳动物，因此共享许多属性。在这种情况下，你不会希望在它们之间复制粘贴函数；更明智（更简单！）的做法是定义一个定义共享功能的哺乳动物类，然后从那里继承。

默认情况下，Python 为你提供了父类所拥有的所有方法，但你可以通过为需要这些类提供新的实现来覆盖它们。例如：

```
class modelt(car):

    def setColor(self, color):

        print("Sorry, Model Ts only come in black!")
```

```
myford = ford()

ford.setColor("green")

mycar = modelt()

mycar.setColor("green")
```

第一辆车是作为 Ford 创建的，因此`setColor()`将正常工作，因为它用的是来自`car`类的方法方法。然而，第二辆车是作为 Model T 创建的，它有自己的`setColor()`方法，因此调用将失败。

这提供了另一个场景：如果你覆盖了一个方法，但仍然想调用父类的方法，该怎么办？例如，如果允许更改 Model T 的颜色但需要额外费用，我们希望打印一条显示“你还欠 50 美元”的消息，然后更改颜色。为了做到这一点，我们需要使用从当前类继承的类对象——在本例中是`car`。这是一个示例：

```
class modelt(car):

    def setColor(self, color):

        print("You owe $50 more")

        car.setColor(self, color)
```

```
mycar = modelt()

mycar.setColor("green")
```

这会打印消息然后更改汽车的颜色。

# 多重继承

你可以根据需要继承许多类，并在此过程中构建功能。例如，你可以有一个类`animalia`、一个子类`chordata`、一个子子类`mammal`以及一个子子子子类`homosapiens`。每一个层中的类都比它的父类更具体。然而，Python 中一个有趣的特性是具有多重继承的能力——同时从两个类中获取功能。

再次，这通过代码展示得最好：

```
class car(object):

    def drive(self):

        print("We're driving...")
```

```
class timemachine(object):

  def timeTravel(self):

    print("Traveling through timachine...")

class delorian(car,timemachine): pass

mydorian = delorian()

mydorian.drive()

mydorian.timeTravel()
```

在这个示例中，我们有一个`car`类和一个`timemachine`类。它们都可以独立工作，所以你可以拥有一辆汽车开着它，或者拥有一台时光机器用它穿越时。然而，我们还有一个继承自`car`和`timemachine`的`delorian`类。如你所，它可以调用`drive()`（继承自`car`）和`timeTravel()`（继承自`timemachine`）。

这引入了另一个有趣的问题：如果`car`和`timemachine`都有`refuel()`函数会发生什么？答案是 Python 根据你列出类的顺序来选择正确的函数。在之前的代码中，我们使用`class delorian(car,timemachine)`，这意味着“先继承`car`然后继承`timemachine`”。结果是，如果两者都有`refuel()`函数，Python 将选择`refuel()`。

当涉及进一步的继承时，这种情况会变得更加复杂。也就是说，如果`car`从`vehicle`继承其`refuel()`方法，Python 仍然会选择它。在后台发生的情况是，Python 会选择你继承的第一个类，并在它的所有父类中搜索匹配的方法。如果没有找到，它将进入下一个类并检查它及其父类。此过程不断重复，直到找到具有所需方法的类为止。

# 标准库与帕尔纳索斯金库

默认的 Python 安装包含许多模块（代码块），这些模块允许你与操作系统交互、打开并操作文件、解析命令行选项、执行数据哈希和加密等。这是当人们被问及为什么喜欢 Python 时最常被提到的原因之一——它通常带有许多你可以立即利用的功能。事实上，模块的数量之多，以至于……

*(注：由于原文在此处中断，此处根据语境完成了翻译)*

# 列表 29.1 PHP 中的测试类型

```php
<?php

$S1 = 10;

$Sj = "10";

$Sk = "Hello, world";

echo $S1 + $Sj;

echo $S1 + $Sk;

?>
```

运行该脚本，打开控制台并进入你保存它的目录。然后输入此命令：

```
$ php ubuntu1.php
```
