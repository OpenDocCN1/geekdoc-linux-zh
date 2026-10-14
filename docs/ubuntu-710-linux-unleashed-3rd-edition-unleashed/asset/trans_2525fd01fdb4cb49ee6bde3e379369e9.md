

## 类变量和对象变量

每个对象都有自己的一套函数和变量，并且你可以独立于同类型的对象来操作这些变量。此外，一些类变量被设置为所有类的默认值，并且可以全局操作。

本脚本演示了创建了 dog 类的两个对象，每个对象都有自己的名字：

```
class dog(object):
    name = "Lassie"
    def bark(self):
        print self.name + " says 'Woof!'"
    def setName(self, name):
        self.name = name

fluffy = dog()
fluffy.bark()
poppy = dog()
poppy.setName("Poppy")
poppy.bark()
```

输出如下：

```
Lassie says 'Woof!'
Poppy says 'Woof!'
```

这里，每个狗起初的名字都是 Lassie，但它会被自定义。请记住，Python 默认按引用赋值，这意味着每个对象都引用类的 name 变量，并且当我们使用 setName() 方法为其赋值时，该引用就会丢失。这意味着我们未更改的任何引用都可以被全局操作。因此，如果我们更改类的变量，它也会在所有尚未为该变量设置自己的值的该类实例中发生变化。例如：

```
class dog(object):
    name = "Lassie"
    color = "brown"
fluffy = dog()
poppy = dog()
print fluffy.color
dog.color = "black"
print poppy.color
fluffy.color = "yellow"
print fluffy.color
print poppy.color
```

因此，狗的默认颜色是棕色——fluffy 和 poppy 两个狗对象起初都是棕色。然后，使用 dog.color，我们将默认颜色设置为黑色，并且由于这两个对象都没有设置自己的颜色值，它们会被更新为黑色。倒数第三行使用 `poppy.color` 为 poppy 对象设置自定义颜色值——poppy 变成了黄色，而 fluffy 和狗类总体上仍然是黑色。

## 构造函数和析构函数

为了帮助你自动化对象的创建和删除，你可以轻松重写两个默认方法：`__init__` 和 `__del__`。这些是 Python 在类被实例化和释放时调用的方法，分别称为 *构造函数* 和 *析构函数*。

拥有自定义构造函数在你需要为每个创建的对象接受一组参数时非常有用。例如，你可能希望每只狗在创建时都有自己的名字，你可以用这段代码实现：

```
class dog(object):
    def __init__(self, name):
        self.name = name

fluffy = dog("Fluffy")
print fluffy.name
```

如果你在创建 dog 对象时没有提供 name 参数，Python 会报错并停止。当然，你可以要求任意多的构造函数参数，但通常最好只要求你需要的参数，并通过其他函数来填充其余部分。

另一边是析构函数方法，它允许你在对象被销毁时更好地控制会发生什么。使用这两个方法，我们可以通过在对象创建和删除时打印消息来展示对象的生命周期：

```
class dog(object):
    def __init__(self, name):
        self.name = name
        print self.name + ' is alive!'
    def __del__(self):
        print self.name + ' is no more!'
fluffy = dog("Fluffy")
```

析构函数的作用是给你一个机会来释放分配给对象的资源，或许也可以将某些内容记录到文件中。

## 类继承

Python 允许你通过继承一个或多个其他类来重用代码。例如，狮子、老虎和熊都是哺乳动物，因此共享许多相似的属性。在这种情况下，你不希望在它们之间复制粘贴函数；更聪明、也更简单的做法是创建一个 mammal 类来定义所有共享功能，然后让每个动物从它继承。

考虑以下代码：

```
class car(object):
    color = "black"
    speed = 0
    def accelerateTo(self, speed):
        self.speed = speed
    def setColor(self, color):
        self.color = color

mycar = car()
print mycar.color
```

这创建了一个 car 类，具有默认颜色，并提供了一个 setColor() 函数，以便人们可以更改自己的颜色。现在，你开车去上班吗？是汽车吗？当然是，但很可能是一辆福特，或道奇，或吉普，或其他某个品牌——你不会得到没有品牌的汽车。另一方面，你也不想必须定义一个 Ford 类，给它 accelerateTo()、setColor() 以及基础汽车所拥有的其他方法，然后对 Ferrari、Nissan 等重复做同样的事情。

解决方案是使用继承：定义一个包含所有品牌共享的函数和变量的 car 类，然后从它继承。在 Python 中，你通过在类声明的括号内放置要继承的类名来实现，如下所示：

```
class car(object):
    color = "black"
    speed = 0
    def accelerateTo(self, speed):
        self.speed = speed
    def setColor(self, color):
        self.color = color

class ford(car): pass
class nissan(car): pass

mycar = ford()
print mycar.color
```

pass 指令是一个空语句——它意味着我们的类没有新增内容。然而，由于 ford 和 nissan 类继承自 car 类，它们获得了父类提供的 color、speed、accelerateTo() 和 setColor()。请注意，对于 ford 和 nissan，我们不需要在类名后写 object，因为它们是从已存在的类 car 继承的。

