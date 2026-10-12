

方法中，我们使用 self.height 来引用实例变量，而直接使用 height 来引用参数，即局部变量。同样，在 area() 方法中，我们调用了两个 Rectangle 方法，再次使用了 self。这与 C++ 和 Java 有很大不同，在那些语言中，实例是被默认假定的。

在 C++ 中，实现运算符是可能的，即为我们的数据类型提供运算符的自定义实现。C++ 语法使用关键字 operator 后跟运算符本身——例如 operator+()——但在 Python 中，每个运算符都有一个名称，因此在 Python 中实现类的 + 运算符需要实现 __add__() 方法。Python 中用于实现运算符的所有方法都是特殊方法，这一点通过它们以两个下划线开头和结尾的命名来表示。

为了更好地将我们的自定义类集成到 Python 中，还有一些其他通用的特殊方法可能值得实现。例如，我们可能希望支持比较运算符，并为类实例提供布尔值。我们将在 Rectangle 类中添加一些方法来展示其实际效果，但为了简洁起见，我们不会重复类声明和已实现的方法。我们将首先介绍比较：

```python
def __cmp__(self, other):
    return cmp(self.area(), other.area())
```

如果我们愿意，可以为每个比较运算符实现一个特殊方法。例如，如果我们实现了 __lt__()（“小于”），我们就可以用 < 运算符比较我们类的实例。然而，如果我们不想单独实现比较运算符，我们可以简单地实现 __cmp__()，就像这里所做的那样。如果实现了特定的特殊方法，Python 将在比较时使用该方法；否则，将回退到使用 __cmp__()。因此，仅通过实现这一个特殊方法，所有比较运算符 (<, <=, ==, !=, >=, >) 都可以用于 Rectangle 对象：

```python
rectA = Rectangle(4, 4)
rectB = Rectangle(8, 2)
rectA == rectB     # 由于两者面积相同，结果为 True
rectA < rectB      # False
```

我们使用内置的 cmp() 函数来实现 __cmp__()。cmp() 函数接受两个对象，如果第一个小于第二个，则返回 -1；如果相等，则返回 0；否则返回 1。我们使用矩形的面积作为比较依据，这就是为什么我们在示例中得到了相当令人惊讶的 True 结果。更严格且可能更好的实现可能是：

```python
def __cmp__(self, other):
    if (self.width != other.width):
        return cmp(self.width, other.width)
    return cmp(self.height, other.height)
```

这里，如果宽度相同，我们返回比较高度的结果；否则，我们返回比较宽度的结果。

如果我们没有重新实现任何比较特殊方法，在大多数情况下，Python 会很乐意为我们执行比较，尽管不一定以我们希望的方式进行。如果我们要创建比较有意义的类，我们应当实现 \_\_cmp\_\_()。对于其他类，最安全的做法是实现一个主体为 return NotImplemented error 的 \_\_cmp\_\_()。

```python
def __nonzero__(self):
    return self.width or self.height
```

当对象处于布尔上下文中时，会使用这个特殊方法；例如 bool(rectA)，或 if rectB: 并且如果对象“非零”，则返回 True。

```python
def __repr__(self):
    return "Rectangle(%d, %d)" % (self.width, self.height)
```

“表示”（representation）特殊方法必须返回一个字符串，如果对该字符串求值（例如使用 eval()），将构造出一个与被调用对象具有相同属性的对象。有些对象过于复杂而无法支持这一点，对于某些对象（例如 GUI 中的窗口或按钮），这样做没有意义；因此，此类类不提供 \_\_repr\_\_() 实现。在字符串 % 运算符的格式字符串中，我们使用 \*r 来获取此特殊方法的结果；我们也可以使用 repr() 函数或反引号 \*\*\* 运算符。反引号只是使用 repr() 的一种语法替代形式。例如，repr(x) 和 \*x\* 都返回相同的结果：对象 x 的表示，由 x 的 \_\_repr\_\_() 方法返回。

还有一个 \_\_str\_\_() 特殊方法，它必须返回被调用对象的字符串表示（类似于 Java 的 toString() 方法），但与 \_\_repr\_\_() 不同，该表示旨在供人类阅读，且不一定是可求值的（eval()-able）。如果 \_\_str\_\_() 方法未实现（如本例所示），Python 将转而使用 \_\_repr\_\_() 方法。例如：

```python
rect = Rectangle(8, 9)
print rect    # 使用 __repr__() 打印 "Rectangle(8, 9)"
```

如果我们希望获得类的人类可读的 Unicode 字符串表示，我们可以实现 \_\_unicode\_\_()。

还有一些通用的特殊方法我们可以实现，但它们不适合 Rectangle 类。所有常见实现的通用特殊方法列在表 3.1 中。

| 方法语法 | 方法语法 |
| :--- | :--- |
| _float_ (self) | float(x) |
| _int_ (self) | int(x) |
| _abs_ (self) | abs(x) |
| _neg_ (self) | -x |
| _add_ (self, other) | x + y |
| _sub_ (self, other) | x - y |
| _iadd_ (self, other) | x += y |
| _isub_ (self, other) | x -= y |
| _radd_ (self, other) | y + x |
| _rsub_ (self, other) | y - x |
| _mul_ (self, other) | x * y |
| _mod_ (self, other) | x % y |
| _imul_ (self, other) | x *= y |
| _imod_ (self, other) | x %= y |
| _rmul_ (self, other) | y * x |
| _rmod_ (self, other) | y % x |
| _floordiv_ (self, other) | x // y |
| _truediv_ (self, other) | x / y |
| _ifloordiv_ (self, other) | x //= y |
| _itruediv_ (self, other) | x /= y |
| _rfloordiv_ (self, other) | y // x |
| _rtruediv_ (self, other) | y / x |

对象。如果我们确实需要对象的副本，可以使用 copy 模块中的 copy() 或 deepcopy() 函数，前者用于没有嵌套属性的对象或浅拷贝足以满足需求的情况，后者用于必须完全复制的对象。或者，我们可以提供自己的复制方法，通常命名为 copy()，因为这是常规的 Python 实践。

对于数值类，提供支持标准数值运算符（如 + 和 *）的功能通常很方便。这在 Python 中通常通过实现各种特殊方法来实现。如果我们只实现 +，Python 将使用它来提供 *，但通常实现两者更好，因为这给予我们更精细的控制，并使优化操作变得更加容易。

最常实现的数值特殊方法列在表 3.2 中。未列出的包括位移位运算符以及十六进制和八进制转换运算符。

存在两个不同的除法运算符的原因是，Python 可以执行整数或浮点数除法，如第 17 页所述。

一些特殊方法有两个或三个版本；例如，_add_ ()、_radd_ () 和 _iadd_ ()。“r” 版本（例如 _radd_ ()）用于左侧操作数没有合适方法但右侧操作数有的情况。例如，对于表达式 x + y，其中 x 和 y 的类型分别为 X 和 Y，Python 首先通过调用 X._add_ (x, y) 来尝试求值表达式。但如果类型 X 没有此方法，Python 将尝试调用 Y._radd_ (y, x)（原文此处逻辑似有笔误，按上下文修正为 Y 的方法，若 Y 也无此方法则抛出异常，此处依原文“ If Y has no such method, an exception will be raised”保留逻辑，但通常 radd 是右操作数的方法）。*注：原文此处表述略有混淆，标准行为是若左操作数方法不可用，则查右操作数的 r 方法。若 Y 也没有该方法，则抛出异常。*

在“i”版本中，“i”代表“原地”（in-place）。它们用于增强赋值运算符，如 +=。很快就会看到一个示例，展示这些方法在实际中的应用，但首先我们必须学习如何创建静态数据和静态方法。

## 静态数据、静态方法和装饰器

在某些情况下，拥有与整个类（而非其实例）相关联的数据是非常有用的。例如，如果有一个 Balloon 类，我们可能想知道使用了多少种独特的颜色：

```python
class Balloon(object):
    unique_colors = set()

    def __init__(self, color):
        self.color = color
        Balloon.unique_colors.add(color)

    @staticmethod
    def uniqueColorCount():
        return len(Balloon.unique_colors)

    @staticmethod
    def uniqueColors():
        return Balloon.unique_colors.copy()
```

静态数据在类块内部创建，但在任何 def 语句外部。要访问静态数据，必须限定名称，最简单的方法是使用类名称，正如我们在 Balloon 类的静态方法中所做的那样。我们将在下一小节中在更现实的上下文中看到静态数据和方法。

@staticmethod 是一个装饰器。装饰器是一个函数，它接受一个函数作为参数，以某种方式包装它，并将包装后的函数重新赋值给原始函数的名称，其效果等同于编写以下内容：

```python
def uniqueColors():
    return Balloon.unique_colors.copy()
uniqueColors = staticmethod(uniqueColors)
```

@ 符号用于标识装饰器。staticmethod() 函数是 Python 内置函数之一。

我们可以使用多个装饰器。例如，可以编写合适的装饰器来记录函数和方法的调用，或记录每次方法调用。例如：

```python
@logger
@recalculate
def changeWidth(self, width):
    self.width = width
```

这里，每当对象的宽度发生变化时，两个装饰器都会应用：logger()（可能会在日志文件或数据库中记录变更）和 recalculate()（可能会更新对象的面积）。

