
大型代码库中更有挑战性的问题之一是为程序故障分配责任。使用自定义异常有助于区分故意抛出的错误和合法的编程错误。如果你的程序带有某种定义的 `ApplicationError` 崩溃，你将立即知道为什么发生该错误——因为是因为你写了对应的代码。另一方面，如果程序带有 Python 的内置异常之一（如 `TypeError` 或 `ValueError`）崩溃，那可能表明存在更严重的问题。

## 3.5 上下文管理器与 with 语句 (Context Managers and the with Statement)

当与异常结合时，文件、锁和连接等系统资源的妥当管理通常是一个棘手问题。抛出的异常可能会导致控制流跳过负责释放资源（如锁）的语句。`with` 语句允许一系列语句在运行时环境中执行，该环境由一个充当上下文管理器的对象控制。这里有一个示例：

[点击此处查看代码图片]

```python
with open('debuglog', 'wt') as file:
    file.write('Debugging\n')
    statements
    file.write('Done\n')
```

```python
import threading
lock = threading.Lock()
with lock:
    # Critical section
    statements
    # End critical section
```

在第一个例子中，`with` 语句在控制流离开后续语句块时会自动关闭已打开的文件。在第二个例子中，`with` 语句在进入和离开后续语句块时会自动获取和释放锁。

`with` 语句允许对象 `obj` 管理进入和退出关联语句块时发生的情况。当 `with` 语句执行时，它调用方法 `obj.__enter__()` 表示正在进入新上下文。当控制流离开上下文时，执行方法 `obj.__exit__(type, value, traceback)`。如果没有抛出异常，`__exit__` 的三个参数都将设置为 `None`。否则，它们将包含类型、值、以及与导致控制流离开上下文的异常相关的回溯信息。如果 `__exit__()` 方法返回 `True`，则表示抛出的异常已处理，不应继续传播。返回 `None` 或 `False` 将导致异常传播。

`with obj` 语句接受一个可选的 `as var` 指定符。此时，`obj.__enter__()` 返回的值被放入 `var` 中。这个值通常与 `obj` 相同，因为这允许在同一个步骤中构造对象并作为上下文管理器使用。例如，考虑以下类：

点击此处查看代码图片

```python
class Manager:
    def __init__(self, x):
        self.x = x

    def yow(self):
        pass

    def __enter__(self):
        return self

    def __exit__(self, ty, val, tb):
        pass
```

通过它，你可以在一步内创建并使用实例作为上下文管理器：

```python
with Manager(42) as m:
    m.yow()
```

这里有一个涉及列表事务的有趣示例：

点击此处查看代码图片

```python
class ListTransaction:
    def __init__(self,thelist):
        self.thelist = thelist

    def __enter__(self):
        self.workingcopy = list(self.thelist)
        return self.workingcopy

    def __exit__(self,type,value,tb):
        if type is None:
            self.thelist[:] = self.workingcopy
        return False
```

该类允许你对现有列表进行一系列修改。然而，只有在没有发生异常的情况下，修改才会生效。原始列表将保持不变。例如：

点击此处查看代码图片

```python
items = [1,2,3]
with ListTransaction(items) as working:
    working.append(4)
    working.append(5)    # 产生 [1,2,3,4,5]
print(items)
```

```python
try:
    with ListTransaction(items) as working:
        working.append(6)
        working.append(7)
    raise RuntimeError("We're hosed!")
except RuntimeError:
    pass
print(items) # 产生 [1,2,3,4,5]
```

`contextlib` 标准库包含了与上下文管理器更高级用法相关的功能。如果你发现自己经常创建上下文管理器，那么可能值得一看。

### 3.6 断言与 __debug__

`assert` 语句可以将调试代码引入程序中。`assert` 的通用形式是

```python
assert test [, msg]
```

其中 `test` 是一个求值为 `True` 或 `False` 的表达式。如果 `test` 求值为为 `False`，`assert` 将抛出一个 `AssertionError` 异常，并带有提供给 `assert` 语句的消息消息 `msg`。这是一个示例：

点击此处查看代码图片

```python
def write_data(file, data):
    assert file, 'write_data: file not defined!'
    ...
```

`assert` 语句不应用于使程序正确而必须执行的代码，因为当 Python 在优化模式下（通过解释器的 `-o` 参数指定）运行时，不会执行它。特别是，使用 `assert` 来检查用户输入或某些重要操作的成功是错误的。相反，`assert` 语句用于检查应该始终为真的不变不变式；如果其中一个被违反，它代表程序中的 bug，而不是用户的错误。

例如，如果之前显示的 `write_data()` 函数旨在供终端用户使用，应将 `assert` 语句替换为传统的 `if` 语句和所需的错误处理。

`assert` 的常见用法是在测试中。例如，你可能使用它来包含对函数中 `a` 的最小测试：

点击此处查看代码图片(n)

```python
def factorial(n):
    result = 1
    while n > 1:
        result *= n
    return result
```

```python
assert factorial(5) == 120
```

这种测试的目的不是详尽，而是作为一种“冒烟测试”。如果函数出现了明显的错误，代码将在断言失败时立即崩溃。

断言在指定预期的输入和输出方面也很有用。例如：

点击此处查看代码图片

```python
def factorial(n):
    assert n > 0, "must supply a positive value"
    result = 1
    while n > 1:
        result *= n
        n -= 1
    return result
```

再次，这并不是为了检查用户输入。它是为了检查内部的一致性。如果其他代码尝试计算阶乘，断言将失败并指向错误代码以便你调试。

### 3.7 结语

尽管 Python 支持多种涉及函数和对象的编程风格，程序执行的基本模型是命令式的。也就是说，程序是由按照出现顺序执行的语句组成的。只有三种基本的控制流结构：`if` 语句、`while` 循环和 `for` 循环。对于理解 Python 如何执行程序来说，并没有奥秘。最复杂且容易出错的功能是异常。事实上，本章重点关注如何处理异常。如果你遵循了这些建议，异常仍然是设计的关键部分。

（注：原文后续部分存在大量重复段落，已按要求进行处理，确保不重复输出）

```python
same object
same value
same type
>>> compare(a, b)
same value
same type
>>> compare(a, [4,5,6])
same type
>>>
```

对象的类型本身也是一个对象，被称为对象的类（class）。这个对象是唯一定义的，并且对于给定类型的所有实例来说都是相同的。类通常有名称（如 `list`、`int`、`dict` 等），可以用于创建实例、执行类型检查并提供类型提示。例如：

[点击查看代码图片]

```python
items = list()
```
