
通过句号和类名来调用该对象，并向括号内传递任何参数。

## 类变量和对象变量

每个对象都有自己的一套函数和变量，你可以独立于相同类型的对象来操作这些变量。此外，某些类变量被设置为所有该类的默认值，并且可以在全局范围内进行操作。

此脚本演示了创建两个 `dog` 类的对象，每个对象都有自己的名称：

```python
class dog(object):
    name = "Lassie"
    def bark(self):
        print self.name + " says Woof!"
    def setName(self, name):
        self.name = name
fluffy = dog()
fluffy.bark()
poppy = dog()
poppy.setName("Poppy")
poppy.bark()
```

该代码输出如下：

- Lassie says 'Woof!'
- Poppy says 'Woof!'

每只狗初始的名称都是 Lassie，但它被自定义了。请记住，Python 的赋值默认是引用的，这意味着每个方法都有对类名变量的引用，当你使用 `setName()` 方法进行赋值时，引用就会丢失。这意味着任何没有改变的引用都可以被全局操作。因此，如果你更改了一个类的变量，所有没有为该变量设置自己值的类实例也会随之改变。例如：

```python
class dog(object):
    name = "Lassie"
    color = "brown"
fluffy = dog()
poppy = dog()
print fluffy.color
dog.color = "black"
print poppy.color
poppy.color = "yellow"
print fluffy.color
print poppy.color
```

因此，狗的默认颜色是棕色——`fluffy` 和 `poppy` 对象开始时都是棕色。通过 `dog.color`，默认颜色变为黑色，由于这两个对象都没有自己的颜色值，它们被更新为黑色。倒数第三行代码使用 `.color` 为 `poppy` 对象设置了自定义颜色值——`poppy` 变成了黄色，但 `fluffy` 和 `dog` 类本身保持保持黑色。

## 构造函数和析构函数

为了帮助自动化对象的创建和删除，你可以轻松地覆盖两个默认方法：`__init__` 和 `__del__`。这些是 Python 在类实例化和释放时调用的方法，分别称为构造函数和析构函数。

当你需要为创建的每个对象接受一组参数时，拥有自定义的构造函数是非常棒的。例如，你可能希望每只狗在创建时都有自己的名称，可以通过以下代码实现这一点：

```python
class dog(object):
    def __init__(self, name):
        self.name = name
fluffy = dog("Fluffy")
```

如果你在创建 `dog` 对象时没有提供 `name` 参数，Python 会报告错误并停止。当然，你可以根据需要请求任意数量的构造参数，尽管通常只请求需要的参数，并在其余部分使用其他函数会更好。

另一方面是析构方法，它允许你对对象销毁时发生的情况有更多控制。通过使用这两个方法，你可以通过在对象创建和删除时打印消息来展示对象的生命周期：

```python
class dog(object):
    def __init__(self, name):
        self.name = name
        print self.name + " * is alive!"
    def __del__(self):
        print self.name + " is no more!"
fluffy = dog("Fluffy")
```

析构函数是为了让你有机会释放分配给对象的资源，或者将某些内容记录到文件中。

## 类继承

Python 允许你通过继承一个类或多个类来重用代码。例如，汽车、卡车和摩托车都是车辆，并且共享许多相似的属性。在这种情况下，你不会希望在它们之间复制粘贴函数；更明智（也更容易！）的方法是有一个 `vehicle` 类定义了所有共享功能，然后让每个车辆都继承该类。

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

这创建了一个具有默认颜色的类，并提供了一个 `setColor()` 函数，以便人们可以更改自己的颜色。现在，你开什么车上班？是汽车吗？当然是，但它很可能是福特、道奇、吉普或其他品牌——你不会在没有品牌的情况下得到汽车。另一方面，无论你想为多少种品牌定义类，只需给它赋予 `accelerateTo()`、`setColor()` 以及基础汽车拥有的其他方法，而不需要为法拉利、日产等品牌编写完全相同的代码。

解决方案是使用继承：定义一个包含所有品牌所有函数和变量的类，然后从那里继承。在 Python 中，你通过在类声明的括号内放入要继承的类名来实现，如下：

```python
class car(object):
    color = "black"
    speed = 0
    def accelerateTo(self, speed):
        self.speed = speed
    def setColor(self, color):
        self.color = color
```

```python
class ford(car): pass
class nissan(car): pass
mycar = ford()
print mycar.color
```
