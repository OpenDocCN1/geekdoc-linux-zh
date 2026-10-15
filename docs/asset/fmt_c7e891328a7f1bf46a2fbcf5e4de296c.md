
Szia, Paul!

`hello = hello_english`

`hello("Paul")`

请注意，函数定义不包含任何类型信息。函数是无类型的，就像我们所说的那样。好处是你可以写一个函数来做多件事：

```python
def concat(First, Second):
    return First + Second
```

```python
concat(["python"], ["perl"])
['python', 'perl']
```

```python
concat("Hello, ", "world!")
'Hello, world!'
```

这演示了 `return` 语句如何将值传回调用者，但也演示了函数如何对列表做一件事，对字符串做另一件事。这里的魔力是由对象完成的。我们写一个函数告诉两个对象把自己加在一起，而对象本身就知道如何做到这一点。如果它们不知道——如果用户也许传入了一个字符串和一个整数——Python 会替我们捕获这个错误。然而，正是这种放手的、“让对象自己解决”的态度使得函数如此灵活。我们的 `concat()` 函数理论上可以连接字符串、列表，或 `zonks`——一种用户自己创建的数据类型，允许相加。重点是我们不对函数能做什么设限——听起来可能有点俗气，但唯一的限制就是你的想象力！

## Object Orientation

读到这里，你不应该对 Python 的面向对象特性感到惊讶，它很灵活，如果你使用 C 语言类语言多年，很可能会让你感到惊讶。

学习 Python 面向对象编程 OOP 的最好方法就是直接做。所以，这里有一个基本脚本，它定义了一个类，创建了该类的一个对象，并调用了一个函数：

```python
class dog(object):
    def bark(self):
        print "Woof!"

fluffy = dog()
fluffy.bark()
```

定义一个类可以预料地以 `class` 关键字开始，后跟你要定义的类名和一个冒号。类的内容需要缩进一级，以便 Python 知道它在哪里结束。请注意，括号中的 `object` 是为了对象继承，后面会讨论。现在，你至少需要知道的是，如果你的新类不是基于现有类，你应该像前面的代码所示那样在括号内放入 `object`。

类中的函数在工作方式上与普通函数非常相似（尽管它们通常被称为方法），主要区别在于它们都应该至少接受一个参数，通常称为 `self`。这个参数会被填充为调用该函数的对象的名称，并且你需要显式使用它。

创建类的实例是通过赋值完成的。你不需要像某些其他语言那样使用 `new` 关键字——你只需提供空括号即可。调用该对象的函数是通过使用句点、要调用的类名，并将任何参数放在括号内传递来完成的。

## 类变量和对象变量

每个对象都有自己的一组函数和变量，并且你可以独立于同类型的对象来操作这些变量。此外，一些类变量被设置为所有类的默认值，并且可以全局操作。

本脚本演示了创建了 `dog` 类的两个对象，每个对象都有自己的名字：

```python
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

这里，每只狗最初的名字都是 `Lassie`，但它会被自定义。请记住，Python 默认按引用赋值，这意味着每个对象都引用类的 `name` 变量，并且当我们使用 `setName()` 方法为其赋值时，该引用就会丢失。这意味着我们未更改的任何引用都可以被全局操作。因此，如果我们更改类的变量，它也会在所有尚未为该变量设置自己的值的该类实例中发生变化。例如：

```python
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

因此，狗的默认颜色是棕色——`fluffy` 和 `poppy` 两个狗对象最初都是棕色。然后，使用 `dog.color`，我们将默认颜色设置为黑色，并且由于这两个对象都没有设置自己的颜色值，它们会被更新为黑色。倒数第三行使用 `poppy.color` 为 `poppy` 对象设置自定义颜色值——`poppy` 变成了黄色，而 `fluffy` 和狗类总体上仍然是黑色。

## 构造函数和析构函数

为了帮助你自动化对象的创建和删除，你可以轻松重写两个默认方法：`__init__` 和 `__del__`。当类被实例化并释放时，Python 会调用这些方法，分别称为构造函数和析构函数。

拥有自定义构造函数在你需要为每个创建的对象接受一组参数时非常有用。例如，你可能希望每只狗在创建时都有自己的名字，你可以用这段代码实现：

```python
class dog(object):
    def __init__(self, name):
        self.name = name

fluffy = dog("Fluffy")
print fluffy.name
```

如果你在创建狗对象时没有提供 `name` 参数，Python 会报错并停止。当然，你可以要求任意数量的构造函数参数，但通常最好只要求你需要的参数，并通过其他函数来填充其余部分。

另一方面是析构函数方法，它允许你在对象被销毁时更好地控制会发生什么。利用这两个方法，我们可以通过在对象创建和删除时打印消息来展示对象的生命周期：

```python
class dog(object):
    def __init__(self, name):
        self.name = name
        print self.name + " is alive!"
    def __del__(self):
        print self.name + " is no more!"

fluffy = dog("Fluffy")
```

析构函数的作用是给你一个机会来释放分配给对象的资源，或许也可以将某些内容记录到文件中。

## 类继承

Python 允许你通过继承一个或多个其他类来重用代码。例如，狮子、老虎和熊都是哺乳动物，因此共享许多相似的属性。在这种情况下，你不希望在它们之间复制粘贴函数；更明智、更简单的做法是！拥有一个哺乳动物类来定义所有共享功能，然后让每个动物从它继承。

考虑以下代码：

```python
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

这创建了一个 `car` 类，具有默认颜色，并提供了一个 `setColor()` 函数，以便人们可以更改自己的颜色。现在，你开车去上班吗？是汽车吗？当然是，但很可能是一辆福特，或道奇，或吉普，或其他某个品牌——你不会得到没有品牌的汽车。另一方面，你也不想不得不定义一个 `Ford` 类，给它 `accelerateTo()`、`setColor()` 以及基础汽车所拥有的其他所有方法，然后对 `Ferrari`、`Nissan` 等重复做同样的事情。

解决方案是使用继承：定义一个包含所有品牌共享函数和变量的 `car` 类，然后从它继承。在 Python 中，你通过在类声明中的括号内放置要继承的类的名称来实现，如下所示：

```python
class car(object):
    color = 'black'
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
