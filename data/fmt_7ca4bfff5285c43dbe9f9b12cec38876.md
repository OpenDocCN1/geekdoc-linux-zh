
在这个示例中，对 `r.send(None)` 的初始调用是必要的，以便生成器执行通向第一个 `yield` 表达式的语句。此时，生成器挂起，等待使用关联生成器对象 `r` 的 `send()` 方法向其发送值。传递给 `send()` 的值由生成器中的 `yield` 表达式返回。接收到值后，生成器执行语句直到遇到下一个 `yield`。

如代码所示，该函数会无限运行。可以使用 `close()` 方法按照如下所示关闭生成器：

点击此处查看代码图像

```python
>>> r.close()
>>> r.send(4)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>>
```

`close()` 操作会在生成器内部的当前 `yield` 处抛出一个 `GeneratorExit` 异常。通常，这会导致生成器静默终止；如果你愿意，可以捕获它来执行清理工作。一旦关闭，如果在适当的情况下使用 `throw(ty, tb)` 方法，则会抛出一个 `StopIteration`，其中 `ty` 是异常类型，`val` 是异常参数，`tb` 是可选的回溯跟踪。点击此处查看代码图像

```python
>>> r = receiver()
>>> r.send(None)
Ready to receive
>>> r.throw(RuntimeError, "Dead")
Traceback (most recent call last):
  File "receiver.py", line 14, in receiver
RuntimeError: Dead
>>>
```

## 6.6 增强型生成器的应用

增强型生成器是一种特殊的编程结构。与自然驱动 `for` 循环的简单生成器不同，没有核心语言特性来驱动增强型生成器。那么，你为什么想要一个需要接收值的函数？这仅仅是学术性的吗？

在历史上，增强型生成器被用于并发库——特别是基于 I/O 的库。在这种背景下，它们通常被称为“协程”或“基于生成器的协程”。然而，许多此类功能已转化为 Python 的 `async` 和 `await` 特性。对于这种特定情况，使用 `yield` 并没有实际理由。尽管如此，仍然有一些实际应用。

像生成器一样，增强型生成器可以实现不同类型的求值和控制流。一个示例是 `contextlib` 模块中的 `@contextmanager` 装饰器。例如：

点击此处查看代码图像

```python
from contextlib import contextmanager

@contextmanager
def manager():
    print("Entering")
    try:
        yield 'somevalue'
    except Exception as e:
        print("An error occurred", e)
    finally:
        print("Leaving")
```

在这里，生成器被用于将上下文管理器的部分连接在一起。记得上下文管理器是由实现以下协议的对象定义的：

点击此处查看代码图像

```python
class Manager:
    def __enter__(self):
        return somevalue
    def __exit__(self, ty, val, tb):
        if ty:
            # 发生了异常
            ...
            # 如果处理则返回 True，否则 False
```

对于 `contextmanager` 生成器，`yield` 语句之前的内容在管理器进入时执行（通过 `__enter__` 方法）。`yield` 之后的所有内容在管理器退出时执行（通过 `__exit__` 方法）。如果发生了错误，它将作为异常在 `yield` 语句处报告。这是一个示例：

点击此处查看代码图像

```python
>>> with manager() as val:
    print(val)
...
...
Entering
somevalue
Leaving
>>> with manager() as val:
    print(int(val))
...
...
Entering
An error occurred invalid literal for int() with base 10:
'somevalue'
Leaving
>>>
```

为了实现这一点，使用了一个包装类。这是一个简化的实现，用于说明基本思想：

点击此处查看代码图片

```python
class Manager:
    def __init__(self, gen):
        self.gen = gen
    def __enter__(self):
        # 运行到 yield
        return self.gen.send(None)
    def __exit__(self, ty, val, tb):
        try:
            if ty:
                try:
                    self.gen.throw(ty, val, tb)
                except ty:
                    return False
        else:
            self.gen.send(None)
        except StopIteration:
            return True
```

扩展生成器的另一个应用是使用函数封装一个“工作”任务。函数调用的核心特征之一是建立了一个局部变量的环境。对这些变量的访问经过高度优化——比访问类和实例的属性快得多。由于生成器在显式关闭或销毁之前一直保持存，可以使用生成器来设置一个长持续任务。这是一个接收字节片段并将其组合成行的生成器示例：

点击此处查看代码图片

```python
@consumer
def line_receiver():
    data = bytearray()
    line = None
```

```python
linecount = 0
while True:
    part = yield line
    linecount += part.count(b'\n')
    data.extend(part)
    if linecount > 0:
        index = data.index(b'\n')
        line = bytes(data[:index+1])
        data = data[index+1:]
        linecount -= 1
    else:
        line = None
```

在这个示例中，生成器接收字节片段，这些片段被收集到一个字节数组中。否则，如果数组包含换行符，则提取并返回一行。否则返回 None。以下是一个说明其如何工作的示例：

点击此处查看代码图片

```python
>>> r = line_receiver()
>>> r.send(b'hello')
>>> r.send(b'world\n ')
b'hello world\n'
>>> r.send(b'works!')
>>> r.send(b'\n')
b'it works!\n'
>>>
```

类似的代码可以写成类，例如：

点击此处查看代码图片

```python
class LineReceiver:
    def __init__(self):
        self.data = bytearray()
        self.linecount = 0
    def send(self, part):
        self.linecount += part.count(b'\n')
        self.data.extend(part)
```

```python
if self.linecount > 0:
    index = self.data.index(b'\n')
    line = bytes(self.data[:index+1])
    self.data = self.data[index+1:]
    self.linecount -= 1
    return line
```

```python
else:
    return None
```
