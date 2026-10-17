
```
>>> list4 = ["a", "b", "c"]
>>> list5 = list4[:]
>>> list4 = list4 + ["d"]
>>> list5
['a', 'b', 'c']
>>> list4
['a', 'b', 'c', 'd']
```

列表有它们自己的内置方法集合，例如 `sort()`、`append()` 和 `pop()`。后者接收参数并从列表末尾移除元素，且 `pop()` 还会返回被移除的元素。这里有一个例子：

```
>>> list5 = ["nick", "paul", "Julian", "graham"]
>>> list5.sort()
>>> list5
['graham', 'Julian', 'nick', 'paul']
>>> list5.pop('paul')
>>> list5
['graham', 'julian', 'nick']
>>> list5.append("Rebecca")
```

此外，字符串的一种有趣方法返回列表：`split()`。它接受一个字符作为分隔符，并给你一个列表，其中每个元素都是字符串中的一个块。这里有一个例子：

```
>>> string = "This is a test string"
>>> string.split(" ")
['This', 'is', 'a', 'test', 'string']
```

列表在 Python 中被广泛使用，尽管随着语言的成熟，这种情况正在缓慢变化。在 3.x 中，列表的比较和排序方式发生了变化，因此在尝试执行这些任务时，务必检查最新的文档。

## 字典

与列表不同，字典是一个没有固定顺序的集合。相反，它有一个**键**（key，元素的名称）和一个**值**（value，元素的内容），Python 会为了最大性能在任何需要的地方放置字典。在定义字典时，你可能需要使用大括号 `{}` 和冒号 `:`。你从一个左括号开始，为每个元素提供一个键和一个值，用冒号分隔，如下所示：

```
>>> mydict = { "perl": "a language", "php": "another language" }
>>> mydict
{'php': 'another language', 'perl': 'a language'}
```

这个例子包含了 `perl` 和 `php` 键。然而，当打印字典时，你会发现 `php` 在 `perl` 之前；Python 并不遵循你输入它们的顺序。你可以使用普通代码对字典进行索引：

```
>>> mydict["perl"] = 'a language'
```

你可以使用 `break` 和 `continue` 关键字来控制循环。`break` 退出循环并立即继续后续处理，而 `continue` 则跳转到下一次迭代。

同样，从 2.x 到 3.x 发生了许多细微的变化。大多数条件判断和循环的工作方式相同，由于我们在本节中提到过这一点，我们应该注意到：在 3.x 中 `print` 不再是一个语句，而是一个函数调用。这为我们讨论函数铺平了道路。

## 函数

某些语言（例如 PHP）在执行代码之前会先读取并处理整个文件，这意味着你可以在函数定义之前调用它，因为编译器在尝试调用函数之前会读取该函数的定义。Python 则不同：如果你在调用函数时还没有到达该函数的定义，你将得到错误。这种行为背后的原因是 Python 实际上为你的函数创建了一个对象，这又意味着两点：第一，你可以在脚本中多次定义同一个函数，并在运行时选择正确的那个；第二，你可以在使用函数时直接将其赋值给另一个名称。

函数定义以 `def` 开始，然后是函数名、括号和参数列表，最后是一个冒号：函数的体内容需要比定义至少缩进一级。因此，通过函数赋值和动态声明，你可以编写一个以迂回方式打印问候的脚本：

```python
def hello_english(Name):
    print "Hello, " + Name + "!"

def hello_hungarian(Name):
    print "Szia, " + Name + "!"

>>> hello = hello_hungarian
>>> hello("Paul")
>>> hello = hello_english
>>> hello("Paul")
```

注意，函数定义不包含类型信息。如前所述，函数是无类型的。这样做的好处是你可以写一个函数来完成某些操作：

```python
def concat(First, Second):
    return First + Second
...
>>> concat(["python"], ["perl"])
['python', 'perl']
>>> concat("Hello, ", "world!")'Hello, world!'
```

这个示例演示了 `return` 语句如何将值传回调用者，以及函数如何对列表执行某项操作而对字符串执行另一项操作。这里的魔法是通过对象实现的。你写一个函数告诉两个对象相加，而对象本身本质上知道如何这样做。它们并不知道——也许用户传递了字符串和整数——Python 会为你捕获错误。然而，这种“放手不管，让它们去解决”的态度让函数如此灵活。`concat()` 函数理论上可以拼接字符串、列表或 zones（某人在添加功能时自己创建的数据类型）。也就是说，Python 并不限制你的函数能做什么。尽管听起来可能像老陈调，但唯一的限制就是你的想象力。

## 面向对象

读到这里，如果你听到 Python 的面向对象是非常灵活的，你不必感到惊讶；如果你长期使用类 C 语言，这可能会让你感到惊讶。

学习面向对象编程（OOP）最好的方法就是动手做。这是一个基础脚本，定义了一个类，创建了该类的对象并调用了一个函数：

```python
class Dog(object):
    def bark(self):
        print "Woof!"

fluffy = Dog()
fluffy.bark()
```

定义类正如预料的，是以 `class` 关键字开始，后面跟着你定义的类名和冒号。类内容需要缩进，以便 Python 知道它在哪里结束。注意，括号内的对象是为了对象继承的，这将在稍后讨论。现在，你需要知道，如果你的新类不是基于现有的类，你应该像前面的代码那样在括号中放入 `object`。

类内部的函数工作方式与普通函数相同（尽管它们通常被称为方法）；区别在于，它们都应该至少接受一个参数，称为 `self`。这个参数被填充为调用函数时的对象名称，你需要使用它。

创建类的实例是通过赋值完成的。你不需要像某些其他语言那样使用任何 `new` 关键字；提供括号即可标识创建。调用对象的方法是使用点 `.` 和要调用的类名，并将任何参数通过括号传递。

### 类变量和对象变量

每个对象都有自己的变量，你可以独立于同类型的对象来操纵这些变量。此外，类变量可以为所有类设置一个默认值，在这种情况下，可以对其进行全局操作。

该脚本演示了创建两个类的类的对象，每个对象都有自己的名字：

```python
class Dog(object):
    name = "Lassie"
    def bark(self):
        print self.name + " Woof!"
    def set_name(self, name):
        self.name = name

fluffy = Dog()
fluffy.bark()
poppy = Dog()
poppy.set_name("Poppy")
poppy.bark()
```

输出如下：

- Lassie says 'Woof!'

- Poppy says 'Woof!'

在这里，每只狗都从名字 Lassie 开始，但它被定制化了。请记住，默认情况下，Python 按引用赋值，这意味着每个对象都有一个指向类名变量的引用，正如你通过 `set_name()` 方法所看到的，引用丢失了。这意味着你的引用无法被全局操纵。因此，如果你更改了类的变量，该类所有未设置变量值的实例也会随之发生变化。考虑这个例子：

```python
class Dog(object):
    name = "Lassie"
    color = "brown"

fluffy = Dog()
poppy = Dog()
print fluffy.color
print poppy.color
```

### 构造函数和析构函数

为了自动化对象的创建和删除，你可以轻松地覆盖两个方法：`__init__` 和 `__del__`。这些是 Python 在类实例化和释放时调用的方法，分别被称为构造函数和析构函数。

当你需要为每个创建的对象接受一组参数时，拥有自定义构造函数是非常棒的。例如，你可能希望每只狗在创建时都有自己的名字，你可以这样实现：

```python
class Dog(object):
    def __init__(self, name):
        self.name = name
```

析构函数通过在创建和删除时打印消息来显示对象的生命周期：

```python
class dog(object):
    def __init__(self, name):
        self.name = name
        print self.name + " is alive!"
    def __del__(self):
        print self.name + " is no more!"

fluffy = Dog("Fluffy")
```

析构函数在这里有机会释放分配对象的资源或者记录日志。注意，虽然可以覆盖 `__del__` 方法，但这样做是非常危险的，因为无法保证在解释器退出时仍然存在的对象的 `__del__` 方法会被调用。Python 文档详细解释了这一点：`https://docs.python.org/reference/datamodel.html#object.__del__`

### 类继承

Python 允许你通过继承一个或多个类来重用代码。例如，狮子、老虎和熊共享许多相似的属性。在这种情况下，你不想在它们之间复制粘贴函数；更明智且更容易的方法是定义一个包含所有共享功能的主类，然后让每个动物继承该类。

考虑以下代码：

```python
class Car(object):
    color = "black"
    speed = 0
    def accelerate_to(self, speed):
        self.speed = speed
    def set_color(self, color):
        self.color = color
mycar = Car()
print mycar.color
```

这个示例创建了一个带有颜色的 `Car` 类，并提供了一个 `set_color()` 函数以便人们可以更改颜色。现在，你工作的工具是什么？它是一辆车吗？当然是，它是一辆福特、道奇、吉普，或者其他品牌；你不会得到没有品牌的汽车。另一方面，你并不需要定义一个 `Ford` 类并赋予它 `accelerate_to()`、`set_color()` 以及基础汽车所需的所有方法，然后对法拉利、日产进行重复的操作。

解决方案是使用继承：定义一个包含所有品牌共享函数和变量的汽车类（car），然后从它继承。在 Python 中，你可以在类声明的括号中放入要继承的类名来实现，如下所示：

```python
class Car(Object):
    color = "black"
    speed = 0
    def accelerate_to(self, speed):
        self.speed = speed
    def set_color(self, color):
        self.color = color
class Ford(Car): pass
class Nissan(Car): pass
mycar = Ford()
print mycar.color
```

`pass` 指令是一个空语句；意味着该类不包含任何新内容。然而，由于 `Ford` 和 `Nissan` 类继承自 `car` 类，它们获得了父类提供的 `color`、`speed`、`accelerate_to()` 和 `set_color()`。（注意，`Ford` 和 `Nissan` 类名后不需要对象，因为它们继承自已有的类：`car`。）

默认情况下，Python 会赋予你父类的所有的方法，但你可以通过为需要的类提供新的实现来覆盖它们。这是一个示例：

```python
class Model(Car):
    def set_color(self, color):
        print("对不起，Model T 只有黑色!")
```

```python
myford = Ford()
Ford.set_color("green")
mycar = Model()
mycar.set_color("green")
```

第一辆车是作为 `Ford` 创建的，所以 `set_color()` 可以正常工作，因为它使用了 `car` 类的方法。然而，第二辆车是作为 `Model` 创建的，它有自己的 `set_color()` 方法，所以调用失败了。

这暗示了一个有趣的场景：如果你覆盖了一个方法，但又想调用父类的方法该怎么办？例如，如果允许更改 Model T 的颜色但需要支付费用，你可能希望打印一条显示“你还欠 50 美元”的消息并更改颜色。要做到这一点，你需要使用当前 `Car` 继承自类对象（在本例中为 `Car`）。这里是一个示例：

```python
class Modelt(Car):
    def set_color(self, color):
        print("你还欠 50 美元")
        Car.set_color(self, color)
```

mycar = Modelt()

mycar.set_color("green")

print mycar.color
