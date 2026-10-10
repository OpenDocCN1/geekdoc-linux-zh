
# Inheritance

> Note
> Inheritance is an advanced OOP topic, of concern primarily to those doing serious development. If you're doing small- to moderate-sized projects, you can safely choose to skip the “Inheritance” section.

Object orientation allows construction of programs in parts rather than tasks. Often these parts represent tangible objects or business entities. At such times, it's handy to classify these objects or entities the way we do in English. Consider the following:

- Animal
  - Bird
    - Duck
    - Robin
    - Owl
- Fish
  - Trout
  - Catfish

You can think of the relationships of this hierarchy as an “is a” relationship. In other words, a bird is a(n) animal with wings. A robin is a bird. The robin “inherits” traits from birds `wings` and traits from animals `movement`.

Here's another example:

- Person
  - Employee

An employee is a person.

Now let's look at some code:

```
class person:
    def __init__(self, lname, fname):
        self._lname = lname
        self._fname = fname
    def getFirstname(self):
        return self._fname
    def getLastName(self):
        return self._lname
    def putfirstname(self, s):
        self._fname = s
    def putlastname(self, s):
        self._lname = s

p = person("Jones", "Paul")
print "*", p.getFirstName(), p.getLastName(), "*"
```

In the preceding code, the person's name is set upon instantiation by the `__init__` method, so the print statement prints the correct name:

- * John Jones *

Modularity has the basis of cost-effective, reliable, easy-to-repair systems from the dawn of the industrial revolution. Object-oriented programming's potential for enables these advantages in software. Tight encapsulation makes programs scalable, meaning they can grow without reaching a point where the interaction combinations grow geometrically and prevent further growth. The road to tight encapsulation is deciding what each class represents and creating a very few public functions to allow other software entities to control its behavior and query it for information.

# Programming in Python

CHAPTER 27

> Note
> Inheritance is an advanced OOP topic, of concern primarily to those doing serious development. If you're doing small- to moderate-sized projects, you can safely choose to skip the “Inheritance” section.

# Python 编程 第 27 章 893

## 注意事项

Python 中在类内部定义的任何函数或变量，如果其名称以至少两个下划线开头且结尾没有多于一个下划线，则被定义为私有。私有变量无法从类定义之外的代码访问。

Python 提供了一种在类定义之外访问私有变量的“后门”方法。本章将不讨论这一点，因为这样做会违背面向对象编程的目的，并破坏程序的模块化。

对于使用 `person` 类实例的程序员来说，该人的姓名是否恰好存储在私有类变量 `__fname` 和 `__lname` 中是完全不重要的。事实上，这两个变量无法在类代码之外访问。考虑尝试直接访问 `__fname`：

```
p = person()
print p.__fname
```

上述代码会抛出属性错误 `attribute error`。由于 `__fname` 是私有的，无法通过 `p.__fname` 访问。它在类定义之外的任何地方无法被查看或修改。`__fname` 和 `__lname` 相当于磁带的偏置电路或汽车的正时机构，程序不需要、绝对不应该知道它们。因此，`__fname` 和 `__lname` 被称为封装。将除预期访问的之外所有变量和方法进行封装的过程称为封装。良好的封装要求每个类都为其他程序部分运行该类的对象提供所需的最少公共函数。这种“薄接口”使得 OOP 程序具有极高的模块化、可靠性、易于修改且易于故障排除。而且是的，它使得程序的类具有可重用性。

之前定义的 `person` 类通过 `getFirstName()` 和 `putFirstName()` 方法提供了对 `__fname` 的必要访问，就像汽车通过刹车提供对制动钳的必要访问一样。`person` 类的工作原理显而易见。调用 `putFirstName()` 会改变 `__fname`，调用 `getFirstName()` 则检索 `__fname`。对于姓名的方法和变量也是如此。

![](img/f36419c0b225d12fa66de83fa271829b_926_0.png)

## 开发环境

第四部分

现在你可以添加以下代码来练习 `person` 类代码：

```
p = person()
print "*", p.getFirstName(), p.getLastName(), "*"
p.putFirstName('John')
p.putLastName('Smith')
print "*", p.getFirstName(), p.getLastName(), "*"
```

上述代码实例化了一个名为 `p` 的 `person` 对象，打印了 `目前为空的` 姓和名，设置了姓名，然后再次打印了它们。输出如下：

- * *

* John Smith *

## 类构造函数

现在我们准备好添加类构造函数了。类构造函数始终被调用 `__init__()`。只能定义一个类构造函数。在这种情况下，我们创建了类构造函数，使得姓名在实例化时被定义：

```
class person:
    def __init__(self, lname, fname):
        self.__lname = lname
        self.__fname = fname
    def getFirstName(self):
        return self.__fname
    def getLastName(self):
        return self.__lname
    def putFirstName(self, s):
        self.__fname = s
    def putLastName(self, s):
        self.__lname = s
    __fname = "*"
    __lname = "*"
```
