
从 `iterable` 中的项创建一个排序列表。关键字参数是一个在传递给函数之前转换数值的单参数函数。关键字参数 `reverse` 是一个布尔值，指定结果列表是否按倒序排序。`key` 和 `reverse` 参数必须使用关键字指定——例如：`sorted(a, key=get_name)`。

```python
staticmethod(func)
```

为类创建静态方法。此函数通过 `@staticmethod` 装饰器隐式调用。

```python
str([object])
```

字符串类型。在 Python 2 中，字符串包含 8 位字符，而在 Python 3 中字符串是 Unicode。如果指定了 `object`，则通过调用其 `__str__` 方法创建值的字符串表示。这就是你在打印对象时看到的内容。如果没有参数，则创建一个空字符串。

```python
sum(items[, initial])
```

计算迭代对象 `items` 中序列的和。`initial` 提供起始值并默认为 0。此函数仅适用于数字。

```python
super(type[, object])
```

返回一个表示 `type` 超类的对象。此主要目的是调用基类中的方法。这里有一个例子：

```python
class B(A):
  def foo(self):
    super(B, self).foo()
```

如果 `object` 是对象，则 `isinstance(object, type)` 必须为真。如果 `object` 是类型，那么它是 `type` 的子类。更多细节请参见第 7 章“类与面向对象编程”。在 Python 3 中，你可以在方法中无参数使用 `super()`。在这种情况下，`type` 被设置为定义该方法的类，`object` 被设置为方法的第一个参数。

## 内置函数与类型 211

```python
tuple([items])
```

表示元组的类型。如果提供了 `items`，它将是一个用于填充元组的可迭代对象。然而，如果 `items` 已经是一个元组，则将其原样返回而不作任何修改。如果没有提供参数，则返回一个空元组。

```python
type(object)
```

Python 中所有类型的基类。当作为函数调用时，返回对象的类型。对于整数、浮点数和列表等常见类型，该类型将指向内置类之一，如 `int`、`float`、`list` 等。对于用户定义对象，类型是其关联的类。对于 Python 内部对象，你通常会得到一个指向 `types` 模块中定义的某个类的引用。

```python
type(name,bases,dict)
```

创建一个新对象（这等同于定义一个新类）。`name` 是新类型的名称，`bases` 是类元组，`dict` 是一个包含类体对应定义的字典。此函数最常用于处理元类（metaclasses）时。这将在第 7 章中详细描述。

```python
chr(x)
```

将整数或长整数 `x`（范围为 0 <= x <= 65535）转换为单个 Unicode 字符。仅限 Python 2。在 Python 3 中，请使用该函数。

```python
encode(string, encoding, [errors])
```

在 Python 2 中，这会将字符串转换为 Unicode。`encoding` 指定数据编码字符串。如果未命名，则使用 `sys.getdefaultencoding()` 返回的默认编码。`errors` 指定如何处理编码错误，可选 `'strict'`、`'ignore'`、`'replace'`、`'backslashreplace'` 或 `'xmlreplace'` 之一。详情请参考第 9 章和第 3 章。Python 3 中不可用。

```python
vars(object)
```

返回对象的符号表（通常在 `__dict__` 属性中）。如果没有提供参数，则返回一个对应于本地命名空间的字典。此函数返回的字典应该是只读的。修改其内容是不安全的。

```python
range([start], stop, [step])
```

表示从 `start` 到 `stop`（不包含 `stop`）的整数范围的类型。`step` 提供了一个可选的步长。这些值不会被实际存储，而是在访问时按需计算的。在 Python 2 中，当你想要对整数范围进行循环时，`xrange()` 是首选函数。在 Python 3 中，`xrange()` 已重命名为 `range()` 且 `xrange()` 不再可用。`start`、`stop` 和 `step` 受限于机器整数支持的数值集合（通常为 32 位）。

```python
zip([s1, s2, ...])
```

在 Python 2 中，返回一个元组列表，其中第 n 个元组是 `s1[n]`, `s2[n]`, ....。结果列表将根据截断到最短参数序列的长度。如果没有提供参数，则返回一个空列表。在 Python 3 中，行为类似，但结果是一个产生元组序列的迭代器。在 Python 2 中，请注意对长输入序列使用 `zip()` 可能会无意中消耗大量内存。考虑使用 `itertools.izip()`。

## 第 12 章 内置函数与异常

## 内置异常

内置异常包含 `exceptions` 模块中，该模块在执行任何程序之前总是会被加载。异常被定义为类。

## 异常基类

以下异常作为其他异常的基类：

`BaseException`

所有异常的根类。所有内置异常都派生自此类。

`Exception`

所有程序相关异常的类，包含了 `SystemExit`、`GeneratorExit` 和 `KeyboardInterrupt` 之外的所有内置异常。用户定义的异常应该通过继承 `Exception` 来定义。

`ArithmeticError`

算术异常的类，包括 `OverflowError`、`ZeroDivisionError` 和 `FloatingPointError`。

`LookupError`

索引和键错误的基类，包括 `IndexError` 和 `KeyError`。

`EnvironmentError`

发生在 Python 外部的错误的基类，包括 `IOError` 和 `OSError`。前面的异常永远不会被显式抛出。然而，它们可以用于捕获任何类型的错误。例如，以下代码将捕获任何类型的数值错误。

```python
# Some操作
try:
    pass
except ArithmeticError as e:
    # 数学错误
```

## 异常实例

当抛出异常时，会创建一个异常类的实例。该实例被放置在提供给 `except` 语句的变量中。这里有一个示例：

```python
except IOError as e:
    # 处理错误
    # 'e' 有一个 IOError 实例
```

异常实例 `e` 具有几个标准属性，可能有助于检查和/或操作某些应用程序。

`e.args`

在抛出异常时提供的参数元组。在大多数情况下，这是一个带有描述错误的字符串单项元组。对于 `Environment` 异常，该值是一个包含整数、字符串消息和可选文件名的 2 元元组或 3 元元组。如果你需要在不同的上下文中重新创建异常，那么此元组的内容可能很有用；例如，在不同的 Python 解释器进程中抛出异常。

`e.message`

表示在显示异常时打印的错误消息的字符串（仅限 Python 2）。

`e.__cause__`

使用显式链式异常时的之前的异常（仅限 Python 3）。见附录 A。

`e.__context__`

隐式链式异常的之前的异常（仅限 Python 3）。见附录 A。

`e.__traceback__`

与异常关联的 `Traceback` 对象（仅限 Python 3）。见附录 A。

## 预定义异常类

以下异常由程序抛出：

`AssertionError`

断言语句执行失败。

`AttributeError`

属性引用或赋值失败。

`EOFError`

文件末尾。由内置函数 `input()` 和 `raw_input()` 生成。应该注意的是，大多数 I/O 操作 `read()` 和 `readline()` 方法返回空字符串来指示 EOF，而不是抛出异常。

`FloatingPointError`

浮点运算失败。应该注意到，如果配置了 Python，则会抛出该异常。

`GeneratorExit`

在生成器函数内部抛出以指示终止。这发生在生成器被销毁（在消耗所有生成值之前）调用 `close()` 方法时。如果生成器调用此异常，生成器将终止且异常被忽略。

## 第 12 章 内置函数与异常

`IOError`

I/O 操作失败。该值是一个具有 `errno`、`stderr` 和 `filename` 属性的 `OSError` 实例。`errno` 是整数，`stderr` 是字符串消息，`filename` 是可选的文件。`OSE` 的子类。

`ImportError`

当 `import` 语句找不到模块或从 无法在模块中找到名称时抛出。

`IndentationError`

缩进错误。`SyntaxError` 的子类。

`IndexError`

序列下标越界。`LookupError` 的子类。

`KeyError`
