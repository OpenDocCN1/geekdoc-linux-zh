
`list1` 的第一个元素 (`alpha`) 与 `list2` 的第一个元素 (`alpha`) 进行比较，因为它们相等，所以检查下一个元素。那个也相等，所以检查第三个元素，它是不同的。`gamma` 中的 `g` 在字母表中排在 `delta` 中的 `d` 之后，所以 `gamma` 被认为大于 `delta`，`list1` 被认为大于 `list2`。

循环有两种类型，两者都同样灵活。例如，`for` 循环可以遍历字符串中的字母或列表中的元素：

```
>>> string = "Hello, Python!"

>>> for s in string: print s,

...

H e l l o ,   P y t h o n !
```

```
Pos: (1,1)

Pos: (1,2)

Pos: (2,0)

Pos: (2,1)

Pos: (2,2)
```

你可以使用 `break` 和 `continue` 关键字来控制循环。`break` 退出循环并立即继续之后的后续处理，而 `continue` 跳转到下一次循环迭代。

### Functions

其他语言——例如 PHP——在执行之前会读取并处理整个文件，这意味着你可以在函数定义之前调用它，因为编译器在尝试调用它之前会先读取函数的定义。Python 不同：如果在你尝试调用它时尚未到达函数定义，你会得到一个错误。这种行为背后的原因是 Python 实际上为你的函数创建了一个对象，这反过来意味着两件事。首先，你可以在脚本中多次定义同一个函数，并让脚本在运行时选择正确的那个。其次，你可以通过使用 `=` 将函数赋给另一个名称。

函数定义以 `def` 开始，然后是函数名，然后是括号和参数列表，最后是一个冒号。函数的内容需要在定义之外至少缩进一个层级。因此，利用函数赋值和动态声明，你可以写出一种迂回的方式打印正确问候语的脚本：

```
>>> def hello_english(Name):
...     print "Hello, " + Name + "!"
...
>>> def hello_hungarian(Name):
...     print "Szia, " + Name + "!"
...
>>> hello = hello_hungarian
>>> hello("Paul")
Szia, Paul!
>>> hello = hello_english
>>> hello("Paul")
```

注意函数定义不包含任何类型信息。函数是无类型的，就像我们所说的那样。这带来的好处是你可以用一个函数做多件事：

```
>>> def concat(First, Second):
...     return First + Second
...
>>> concat(['python'], ['perl'])
['python', 'perl']
```

```
>>> concat("Hello, ", "world!")
'Hello, world!'
```

这演示了 `return` 语句如何将值发送回调用者，但也演示了函数如何对列表做一件事，对字符串做另一件事。这里的魔力是由对象完成的。我们写一个函数告诉两个对象把自己加在一起，而对象本身就知道如何做到这一点。如果它们不知道——如果用户也许传入了一个字符串和一个整数——Python 会为我们捕获这个错误。然而，正是这种放手、“让对象自行解决”的态度使得函数如此灵活。我们的 `concat()` 函数完全可以连接字符串、列表或 `zonks`——一种用户自己创建的数据类型，允许相加。重点是我们不对函数能做什么设限——听起来可能很俗套，但唯一的限制就是你的想象力！

### Object Orientation

读到这里，你不应该对听到 Python 的面向对象是灵活的并且如果你使用 C 类似语言多年可能会让你惊讶感到意外。

学习 Python 面向对象编程 (`OOP`) 的最好方式就是直接做它。所以，这里有一个基本脚本，它定义了一个类，创建了该类的一个对象，并调用了一个函数：

```
class dog(object):
    def bark(self):
        print "Woof!"

fluffy = dog()
fluffy.bark()
```

定义类从可以预见的 `class` 关键字开始，后跟你要定义的类名和一个冒号。类的内容需要缩进一个层级，以便 Python 知道它何时结束。注意括号内的 `object` 是为了对象继承，后面会讨论。现在，你至少需要知道的是，如果你的新类不是基于现有类，你应该像前面的代码所示那样在括号内放入 `object`。

类中的函数与普通函数的工作方式基本相同（尽管它们通常被称为方法），主要区别在于它们都应至少接受一个参数，通常称为 `self`。该参数会被填充为调用该函数的对象的名称，并且你需要显式使用它。

创建类的实例是通过赋值完成的。你不需要像某些其他语言那样使用任何 `new` 关键字——你只需提供空括号。调用该对象的函数是通过使用句点、要调用的类名，并将任何参数传递在括号内来完成的。

### 类变量和对象变量

每个对象都有自己的一套函数和变量，并且你可以独立于同类型的对象来操作这些变量。此外，一些类变量被设置为所有类的默认值，并且可以全局操作。

本脚本演示了创建了 `dog` 类的两个对象，每个对象都有自己的名字：

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

这里，每个狗起初的名字都是 `Lassie`，但它会被自定义。请记住，Python 默认按引用赋值，这意味着每个对象都引用类的 `name` 变量，并且当我们使用 `setName()` 方法为其赋值时，该引用就会丢失。这意味着我们未更改的任何引用都可以被全局操作。因此，如果我们更改类的变量，它也会在所有尚未为该变量设置自己的值的该类实例中发生变化。例如：

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

因此，狗的默认颜色是棕色——`fluffy` 和 `poppy` 两个狗对象起初都是棕色。然后，使用 `dog.color`，我们将默认颜色设置为黑色，并且由于这两个对象都没有设置自己的颜色值，它们会被更新为黑色。倒数第三行使用 `poppy.color` 为 `poppy` 对象设置自定义颜色值——`poppy` 变成了黄色，而 `fluffy` 和狗类总体上仍然是黑色。

### 构造函数和析构函数

为了帮助你自动化对象的创建和删除，你可以轻松重写两个默认方法：`__init__` 和 `__del__`。这些是 Python 在类被实例化和释放时调用的方法，分别称为 *构造函数* 和 *析构函数*。

拥有自定义构造函数在你需要为每个创建的对象接受一组参数时非常有用。例如，你可能希望每只狗在创建时都有自己的名字，你可以用这段代码实现：

```
class dog(object):
    def __init__(self, name):
        self.name = name

fluffy = dog("Fluffy")
print fluffy.name
```

如果你在创建 `dog` 对象时没有提供 `name` 参数，Python 会报错并停止。当然，你可以要求任意多的构造函数参数，但通常最好只要求你需要的参数，并通过其他函数来填充其余部分。

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
