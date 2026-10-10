
| `get_color` | |

| `Shape` | |

| `self.shape` | |

| `__init__` | |

| `get_shape` | |

图 27.1 列表 27.20 的图化视图

注意列表 27.20 中对命名 `__init__` 调用的使用。在构造函数中，通过名称调用其基类的 `__init__` 函数。这允许直接调用特定继承类的 `__init__` 函数。最后，在 `Thing` 类中，你提供了两个辅助函数，用于返回类数据的列表和元组表示。

# 列表 27.20 展示 Python 的多重继承

```python
class Shape:

    def __init__(self, shape):
        self.shape = shape

    def get_shape(self):
        return self.shape
```

```python
class Color(Shape):

    def __init__(self, color, shape):
        Shape.__init__(self, shape)
        self.color = color

    def get_color(self):
        return self.color
```

```python
class Size(Color):

    def __init__(self, size, color, shape):
        Color.__init__(self, color, shape)
        self.size = size

    def get_size(self):
        return self.size
```

```python
class Thing(Size):

    def __init__(self, size, color, shape):
        Size.__init__(self, size, color, shape)
```

```python
def thing_tuple(self):
    return (self.get_size(), self.get_color(),
    self.get_shape())
```

```python
def thing_list(self):
    return [self.get_size(), self.get_color(),
    self.get_shape()]
```

多重继承的使用并不是没有问题，在某些情况下它是很有用的。避免名称冲突是需要注意的问题之一，但通过适当的命名规范，可以很容易避免。

# 高级特性

现在是时候探索 Python 的一些与其他语言区别开来的高级特性了。本节回顾了 Python 的动态代码、函数式编程、异常管理以及其他一些特性。

## 动态代码

将代码视为数据将数据视为代码的能力是动态语言最引人注目的之一。在函数式语言中，这被称为高阶函数（接受函数作为输入或提供函数作为输出）。列表 27.21 展示了 Python 中的这种能力。首先，你创建一个简单返回数字平方的函数。接下来通过求平方和演示了这一点。接着，你创建一个包含代码元素的列表（计算两个平方的和）。将它们连接成一个字符串，然后传递给 `eval()` 将新字符串作为代码进行评估。如所示，你可以在 Python 程序的范围内动态地创建新代码并执行它。

# 列表 27.21 Python 中的高阶函数

```python
>>> def square(x):
    return x*x
>>> square(5)+square(7)
74
>>> l = ['square', '(5)', '+', 'square', '(7)']
>>> mycode = "".join(l)
>>> print(l)
['square', '(5)', '+', 'square', '(7)']
>>> print(mycode)
'square(5)+square(7)'
>>> eval(mycode)
74
>>>
```

## 函数式编程

在上一节中，你探索了 Python 中的高阶函数，这是它的许多函数式编程范式之一。在本章更早的时候，你还查看了 `map` 操作作为一种简化和构建更具读性函数的方法。本节现在探索 Python 的其他一些函数式元素。

回想 `map` 函数允许你将用户定义的函数应用于列表的每个元素，为迭代器提供了极大的可读性。`map` 函数产生一个返回值的新列表。另一个操作列表的函数是 `reduce`。区别在于 `map` 和 `reduce` 会对列表元素操作直到其为空。列表 27.22 显示了一个示例。该示例导致了元素之间的一系列乘法。

# 列表 27.22 使用 reduce 函数进行计算

```python
>>> def mul(x,y):
    ...
    return x*y
...
>>> reduce(mul, range(1,5))
24
>>>
```

Python 还包含了函数式编程的一个重要方面，称为 `lambda` 函数。`lambda` 函数是在运行时创建的匿名函数。查看在 Python 中创建和使用 lambda 函数的示例（见列表 27.23）。

# 列表 27.23 创建并使用 lambda 函数

```python
>>> g = lambda x: x*x
>>> g(7)
49
>>>
```

这个示例看起来和函数非常相似，但这些函数可以被不同的处理。现在查看在 Python 中创建和使用 lambda 函数的示例（见列表 27.24）。

# 列表 27.24 使用 lambda 创建动态函数

```python
>>> func = lambda x: x*x
>>> func(5)
25
>>>
```

## 异常处理

Python 丰富的异常处理机制机制允许你处理应用程序中的运行时错误或特殊情况。这与其他语言中的异常处理相似，`try` 子句包裹代码块，`except` 子句提供错误处理代码。

```
try:
    ...要检查的代码...
except:
    ...错误处理...
```

现在来看一个具体的示例。列表 27.25 演示了一个简单的示例。在这种情况下，你创建一个从字符串创建列表的函数并返回列表。但如果传递函数的参数不是字符串，你需要处理这种情况，而不是简单地抛出异常（稍后将探讨）。如果提供的不是列表，你只需返回空列表。

# 列表 27.25 使用 try/except 处理异常

```python
>>> def str2list(str):
    ...
    try:
        return str.split()
    ...
    except:
        return []
    ...
>>> print str2list('this is a string')
['this', 'is', 'a', 'test', 'string']
>>> print str2list(5)
[]
>>>
```

这种解决方案唯一的问题是你向调用者隐藏了错误。这在很多情况下是有用的，但在其他情况下，有必要通知调用者问题，以便其以需要的方式进行处理。在这种情况下，你从 `str2list` 函数中移除异常处理，而是将其移动到调用者处并更新以处理特定异常（如列表 27.26 所示）。

# 列表 27.26 处理命名的异常

```python
>>> def str2list(str):
    ...
    return str.split()
...
>>> try:
...
    print str2list(5)
...
except AttributeError:
...
    print "caught attribute error"
```

caught attribute error

# 第 27 章 使用 Python 脚本 539

**表 27.2** Python 常见异常（不完整）

| Python 异常 | 含义 |
|---|---|
| `ArithmeticError` | 表示溢出、除以零、浮点错误 |
| `AssertionError` | 当断言（`assert`）失败时抛出 |
| `AttributeError` | 对象不支持属性引用 |
| `MemoryError` | 操作内存不足 |
| `NameError` | 命名空间未找到本地或全局变量 |
| `SystemError` | 解释器内部错误 |

## 总结

希望这段简短的回顾能让你看到 Python 优势的示例，以及为什么它是当今最流行的脚本语言之一。凭借 Python 的内置函数和海量的标准库，你可以轻松构建程序，完成惊人的功能，且代码量比其他高层语言少上一个数量级。Python 是在已经拥挤的脚本领域中的另一种面向对象的脚本语言，但学习和使用它它是非常值得的。

## 资源

Python 编程语言——官方网站：`http://www.python.org/`。
