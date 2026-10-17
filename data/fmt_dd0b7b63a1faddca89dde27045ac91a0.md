
虽然写一个类可能更熟悉，但代码更复杂且运行较慢。在作者的机器上测试，将大量块喂给接收器，使用生成器比此类代码快约 40–50%。这些节省大部分归功于消除了实例属性的查找——局部变量更快。

还有许多其他潜在的应用，需要记住点是：如果你在不涉及迭代的上下文中看到 `yield`，它可能使用了如 `send()` 和 `throw()` 等增强功能。

# 6.7 生成器与等待的桥梁

生成器函数的经典用法位于异步 I/O 相关的库中，例如标准库 `asyncio`。然而，自 Python 3.5 以来，许多功能已移动到与异步函数和 `await` 语句相关的不同语言（见第 5 章最后）。

`await` 语句涉及与伪装的生成器交互。以下是一个使用 `await` 说明底层协议的示例：

点击此处查看代码图片

```python
class Awaiting:
    def __await__(self):
        print('About to await')
        yield # 必须是一个生成器
        print('Resuming')
```

# 兼容 "await" 的函数。返回一个“等待对象”

```python
def function():
    return Awaitable()
```

```python
async def main():
    await function()
```

以下是你如何使用 `asyncio` 尝试代码：

```
>>> import asyncio
>>> asyncio.run(main())
About to await
Resuming
>>>
```

了解它的工作原理绝对本质吗？可能不需要。所有这些机制通常都是不可见的。但是，如果你发现自己正在使用异步函数，只需知道内部某处隐藏着一个生成器。只要你继续深入挖掘技术细节，你最终会发现它的。

# 6.8 结语：生成器的简史与展望

生成器是 Python 最有趣的成功案例之一。它们也是关于迭代的宏大故事的一部分。迭代是所有编程任务任务之一。在 Python 的早期版本中，迭代是通过序列索引和 `__getitem__()` 方法实现的。这在后来演变为基于基于 `__iter__()` 和 `__next__()` 方法的迭代协议。生成器在不久之后出现，作为一种实现迭代器的更方便的方法。在现代 Python 中，几乎没有理由使用生成器以外的任何东西来实现迭代器。即使对于你可能定义的迭代对象，`__iter__()` 方法本身也是如此。

# 7 类与面向对象编程

类被用于创建新的对象。本章涵盖了类的细节——但并非深入探讨面向对象的设计。本章讨论了 Python 中常见的模式，以及你可以自定义类行为的方式。本章的整体结构是自上而下的。首先描述高级概念和技术。在本章的后续部分，内容将更具技术性并关注实现。

# 7.1 对象

Python 中的几乎代码都涉及创建和对对象进行操作。例如，你可能会创建一个字符串对象并对其操作：

点击此处查看代码图片

```
>>> s = "Hello World"
>>> s.upper()
'HELLO WORLD'
>>> s.replace('Hello', 'Hello Cruel')
'Hello Cruel World'
>>> s.split()
['Hello', 'World']
>>>
```

或者列表对象：

```
>>> names = ['Paula', 'Thomas']
>>> names.append('Lewis')
```

```
>>> names
['Paula', 'Thomas', 'Lewis']
>>> names[1] = 'Tom'
>>>
```

每个对象的本质特征是它通常具有某种状态——字符串的字符、列表的元素等，以及操作该状态的方法。方法通过对象本身调用——就像通过点 (`.`) 运算符附加到对象上的函数一样。

对象始终有一个类型。你可以使用 `type()` 查看它：

点击此处查看代码图片

```
>>> type(names)
<class 'list'>
>>>
```

对象被称为其类型的实例。例如，`names` 是 `list` 的一个实例。

## 7.2 class 语句

使用 `class` 语句定义新对象。类通常由一组构成方法的集合组成。示例：

点击此处查看代码图片

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount
```

```python
def withdraw(self, amount):
    self.balance -= amount

def inquiry(self):
    return self.balance
```

需要注意的是，类本身并不会创建类的实例。例如，在前面的示例中，实际上并没有创建任何账户。相反，类仅仅持有了之后创建的实例上可用的方法。你可以将其看作一个蓝图。

在类内部定义的函数被称为方法（methods）。实例方法是在类实例上操作的函数，该实例被作为第一个参数传递。按照惯例，这个参数被称为 `self`。在前面的示例中，`deposit()`、`withdraw()` 和 `inquiry()` 都是实例方法的示例。

类的 `__init__()` 和 `__repr__()` 方法是所谓的特殊方法或魔术方法（magic methods）的示例。这些方法对解释器运行时具有特殊含义。`__init__()` 方法用于在创建新实例时初始化状态。`__repr__()` 方法返回一个用于查看对象的字符串。定义这个方法是可选的，但这样做可以简化调试，并更容易从交互式提示符中查看对象。

类定义可以可选包含一个文档字符串（documentation string）和类型提示（type hints）。例如：

[点击此处查看代码图片]

```python
class Account:
    """
    简单的银行账户
    """
    owner: str
    balance: float

    def __init__(self, owner:str, balance:float):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount:float):
    self.balance += amount

    def withdraw(self, amount:float):
    self.balance -= amount

    def inquiry(self) -> float:
    return self.balance
```

类型提示不会改变类运行的任何方面——也就是说，它们没有引入任何额外的检查或验证。它们纯粹是元数据，可能对第三方工具或 IDE 有用，或者被某些高级编程技术使用。它们在大多数示例中都没有使用。

## 7.3 实例

类的实例是通过调用类对象作为函数创建的。这会创建一个新实例，然后将其传递给 `__init__()` 方法。`__init__()` 的参数包括新创建的实例 `self` 以及调用类对象时提供的参数。例如：

[点击此处查看代码图片]

```python
# 创建几个账户

a = Account('Guido', 1000.0)
# 调用 Account.__init__(a, 'Guido', 1000.0)

b = Account('Eva', 10.0)
# 调用 Account.__init__(b, 'Eva', 10.0)
```

在 `__init__` 内部，属性通过赋值给 `self` 保存在实例上上。例如，`self.owner = owner` 是于在实例上保存了一个属性。一旦新创建的实例被返回，这些属性以及类的方法就可以使用点（`.`）运算符来访问：

[点击此处查看代码图片]

```python
a.deposit(100.0)   # 调用 Account.deposit(a, 100.0)
b.withdraw(50.0)      # 调用 Account.withdraw(b, 50.0)
owner = a.owner        # 获取账户所有者
```

重要的是，每个实例都有自己的状态。你可以使用 `vars()` 函数查看实例变量。例如：

[点击此处查看代码图片]
