

我们本可以使用类型测试，尽管这在面向对象编程中通常是一种糟糕的做法。

```python
    def __repr__(self):
        return "Length('%.6fm'" % self.__amount

    def __str__(self):
        return "%.3fm" % self._amount
```

Python 的浮点数精度取决于其编译时使用的编译器，但很可能比我们为“表示”方法所选择的六位小数更加精确。

对于字符串表示，我们不需要那么高的精度，也不需要返回一个可以被 `eval()` 执行的字符串，因此我们直接返回原始长度值和米单位。如果 `Length` 类的用户想要使用其他单位的字符串表示，他们可以使用 `to()`——例如，`"%.2f miles" % length.Length("200 ft").to("miles")`。

```python
    def __add__(self, other):
        return Length("%fm" % (self._amount + other._amount))

    def __iadd__(self, other):
        self._amount += other._amount
        return self
```

我们使用了两个特殊方法来说支持加法。第一个方法支持二元 `+` 操作，长度操作数可以位于任意一侧。它构建并返回一个新的 Length 对象。第二个方法支持 `+=`，用于将一个长度增加到另一个长度上。它们允许我们编写如下代码：

```python
x = length.Length("30ft")
y = length.Length("250cm")
z = x + y     # z == Length('11.643554m')
x += y        # x == Length('11.643554m')
```

实现 `__radd__` (1) 来支持混合类型算术也是可能的，但我们没有这样做，因为这对 Length 类来说没有意义。

我们将省略支持减法的代码，因为它与加法的代码几乎相同（并且包含在源文件中）。

```python
    def __mul__(self, other):
        if isinstance(other, Length):
            raise ValueError("\n    \"Length * Length produces an area not a Length\"")
        return Length("%fm" % (self._amount * other))
```

```python
def __rmul__(self, other):
    return Length("%fm" % (other * self._amount))

def __imul__(self, other):
    self._amount *= other
    return self
```

对于乘法方法，我们提供了支持长度乘以数字的功能。如果我们假设 $x$ 是一个长度，`__mul__()` 支持诸如 $x * 5$ 这样的用法，而 `__rmul__()` 支持诸如 $5 * x$ 这样的用法。我们必须明确禁止在 `__mul__()` 中将长度相乘，因为结果将是一个面积而不是一个长度。我们不需要在 `__rmul__()` 中这样做，因为 `__mul__()` 总是先被尝试，如果它抛出异常，Python 就不会尝试 `__rmul__()`。`__imul__()` 方法支持原地（增强）乘法——例如，$x *= 5$。

```python
def __truediv__(self, other):
    return Length("%fm" % (self._amount / other))

def __itruediv__(self, other):
    self._amount /= other
    return self
```

除法特殊方法的实现与其他算术方法具有相似的结构。展示它们的一个原因是提醒我们，`/` 和 `/=` 运算符执行浮点数除法是因为在 `length.py` 文件开头有 `from __future__ import division` 指令。也可以重新实现截断除法，但对于 Length 类来说这不合适。

展示它们的另一个原因是它们与我们刚刚看到的加法方法有微妙的不同。尽管加法和减法仅作用于长度，但乘法和除法则作用于长度和数字。

```python
def __float__(self):
    return self._amount

def __int__(self):
    return int(round(self._amount))
```

我们选择支持两种类型转换，这两种转换都易于编写和理解。之前实现的 `__str__()` 方法也是一种类型转换（转换为类型 `str`）。

既然我们已经看到了如何实现自定义数据类型，我们将把注意力转向实现自定义集合类。

## 集合类

在 Python 中，集合是序列（如列表和字符串）、映射（如字典）或集合。如果我们实现自己的集合类，我们可以使用特殊方法使我们的集合能够使用与内置集合类型相同的语法和语义。表 3.3 列出了集合通用的特殊方法，在本节中我们将讨论每种集合类型的某些具体细节。

对于序列，常见的是实现 `__add__()` 和 `__radd__()` 以支持使用 `+` 进行连接，对于可变集合，也实现 `__iadd__()` 以支持 `+=`。类似地，应实现 `__mul__()` 方法以支持使用 `*` 重复集合。如果给定的索引无效，我们应抛出 `IndexError` 异常。除了特殊方法外，自定义序列集合还应实现 `append()`、`count()`、`index()`、`insert()`、`extend()`、`pop()`、`remove()`、`reverse()` 和 `sort()`。

对于映射，如果给定的键无效，我们应抛出 `KeyError`。除了特殊方法外，我们至少应实现 `copy()` 和 `get()`，以及 `items()`、`keys()` 和 `values()`，还有它们的迭代器版本，如 `iteritems()`。Python 迭代器是返回连续值的函数或方法——例如字符串中的每个字符，或列表或字典中的每个项。它们通常由生成器实现。

对于集合，如果使用了无效的键，我们也应抛出 `KeyError`；例如，在调用 `remove()` 时。集合类应实现 `issubset()`、`issuperset()`、`union()`、`intersection()`、`difference()`、`symmetric_difference()` 和 `copy()`。对于可变集合，应提供额外的方法，包括 `add()`、`remove()` 和 `discard()`。

### 示例：OrderedDict 类

Python 标准库中一个罕见的缺失是有序字典。普通字典提供非常快的查找，但不提供顺序。例如，如果我们想按键顺序迭代字典的值，我们会将键复制到列表中，对列表进行排序，然后迭代列表，使用列表的元素来访问字典的值。对于小字典或很少这样做的时候，排序可能没问题，但当字典很大或频繁排序时，每次排序在计算上可能代价很高。

一个明显的解决方案是创建一个有序字典，这就是我们要做的。

理解 `OrderedDict` 示例对于学习 GUI 编程并非必要，但我们在稍后涵盖的一些程序中使用了这里解释的技术和方法。不过，你现在可以安全地跳到第 99 页开始的下一节，然后在后续章节中遇到这些技术时再回到这里理解它们。

#### 表 3.3 选定的集合特殊方法

| 方法 | 语法 | 描述 |
| :--- | :--- | :--- |
| `__contains__(self, x)` | `x in y` | 如果 x 在序列 y 中或 x 是字典 y 中的键，则返回 True。此方法也用于 not in。 |
| `__len__ (self)` | `len(y)` | 返回 y 中的项目数量 |
| `__getitem__ (self, k)` | `y[k]` | 返回序列 y 的第 k 项或字典 y 中键 k 的值 |
| `__setitem__ (self, k, v)` | `y[k] = v` | 将序列 y 的第 k 项或字典 y 中键 k 的值设置为 v |
| `__delitem__ (self, k)` | `del y[k]` | 删除序列 y 的第 k 项或字典 y 中键为 k 的项 |
| `__iter__(self)` | `for x in y: pass` | 返回进入集合 y 的迭代器 |

一种方法是继承 dict，但我们将使用聚合（也称为组合），并将继承的考虑推迟到下一节。

为了获得有序字典，我们将创建一个类，该类存储一个普通字典，并与其并列存储一个有序字典键列表。我们将实现所有的 dict API，但我们不会展示 `update()` 或 `fromkeys()`，因为它们都超出了我们所涵盖的内容以及 GUI 编程所需的内容。（当然，这两个方法都在源代码中，chap03/ordereddict.py）。

文件中的第一条可执行语句是一个导入语句：

```python
import bisect
```

bisect 模块提供了使用二分查找算法搜索有序序列（如列表）的方法。当我们看到它被使用时，我们将稍后讨论它。

对于这个类，我们不需要任何静态数据，因此我们将通过查看类语句和 `__init__()` 的定义来开始：

```python
class OrderedDict(object):

    def __init__(self, dictionary=None):
        self._keys = []
        self._dict = {}
        if dictionary is not None:
            if isinstance(dictionary, OrderedDict):
                self._dict = dictionary._dict.copy()
                self._keys = dictionary._keys[:]
            else:
```

