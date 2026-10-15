
类型提示的引入并没有改变类的实际运行运行行为——也就是说，会进行额外的检查，但没有什么能阻止用户在代码中设置错误的值。然而，这些提示在编辑器中为用户提供了更有用的信息，在疏忽的使用错误发生之前将其防止。

在实践中，准确的类型提示可能是困难的。例如，`Account`类允许人们使用`int`而不是`float`吗？或者`Decimal`呢？你会发现所有这些都可以工作，尽管提示看起来可能并非如此。

点击此处查看代码图片

```python
from decimal import Decimal

a = Account('Guido', Decimal('1000.0'))
a.withdraw(Decimal('50.0'))
print(a.inquiry())  # -> 950
```

在此类情况下如何妥善组织类型超出了本书的范围。如果有疑问，除非你正在积极使用检查代码类型的工具，否则可能猜猜更好。

## 7.17 属性 (Properties)

如上一节所述，Python 对属性值或类型没有运行时的限制。但是，如果你将属性放在所谓“属性”（property）的管理之下，这种强制是可能的。属性是一种特殊的属性类型，它可以拦截属性访问并通过用户定义的方法进行处理。这些方法可以根据你的需要自由地管理属性。这里有一个示例：

点击此处查看代码图片

```python
import string
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    @property
    def owner(self):
        return self.owner

    @owner.setter
    def owner(self, value):
        if not isinstance(value, str):
            raise TypeError('Expected str')
        if not all(c in string.ascii_uppercase for c in value):
            raise ValueError('Must be uppercase ASCII')
        if len(value) > 10:
            raise ValueError('Must be 10 characters or less')
        self._owner = value
```

在这里，`owner`属性被限制为非常企业级的10字符大大写ASCII字符串。当你尝试使用该类时，工作原理如下：

点击查看代码图片

```python
>>> a = Account('GUIDO', 1000.0)
>>> a.owner = 'EVA'
>>> a.owner = 42
Traceback (most recent call last):
...
TypeError: Expected str
>>> a.owner = 'Carol'
Traceback (most recent call last):
...
ValueError: Must be uppercase ASCII
>>> a.owner = 'RENÉE'
Traceback (most recent call last):
...
ValueError: Must be uppercase ASCII
```

```python
class A:
    pass
```

```python
class B(A):
    pass
```

```python
class C:
    pass
```

```python
a = A()              # 'A' 的实例
b = B(A)           # 'B' 的实例
c = C(A)              # 'C' 的实例
```

```python
type(a)               # 返回类对象 A
isinstance(a, A)   # 返回 True
isinstance(b, A)   # 返回 True, B 派自 A
isubclass(b, C)    # 返回 False, B 未派生自 C
```

同样，内置的`subclass(A, B)`在类A是类B的子类时返回True。这里有一个示例：

点击此处查看代码图片

```python
issubclass(B, A)   # 返回 True
issubclass(C, A)   # 返回 False
```

点击此处查看代码图片

```python
class Stream:
    def receive(self):
        raise NotImplementedError()

    def send(self, msg):
        raise NotImplementedError()

    def close(self):
        raise NotImplementedError()
```

### Example

```python
def send_request(stream, request):
    if not isinstance(stream, Stream):
        raise TypeError('Expected a Stream')
    send(request)
    return stream.receive()
```

这种代码的预期并不是直接使用`Stream`。相反，不同的类将继承自`Stream`并实现所需的功能。用户将实例化这些类中的一个。例如：

点击此处查看代码图片

```python
class SocketStream(Stream):
    def receive(self):
        ...
    def send(self, msg):
        ...
    def close(self):
        ...
```

```python
class PipeStream(Stream):
    def receive(self):
        ...
    def send(self, msg):
        ...
    def close(self):
        ...
```

### Example
```python
s = SocketStream()
send_request(s, request)
```

示例中值得讨论的是`send_request()`中接口的运行时强制。是否应该使用类型提示？

点击此处查看代码图片

```python
# 将接口指定为类型提示
def send_request(stream:Stream, request):
    stream.send(request)
    return stream.receive()
```

鉴于类型提示并不被强制执行，如何根据接口验证参数的决定实际上取决于你想让它发生——在运行时、作为代码检查，或者完全不进行。

这种接口类的用法在大型框架和应用的组织中更为常见。然而，使用这种方法，你需要确保子类在程序后运行过程中确实实现了所需的接口。例如，如果子类没有实现所需的方法之一，或者只是出现了一个简单的拼写错误，其影响最初可能不会被察觉，因为代码在通常情况下仍然可以工作。但是，如果调用了未实现的方法，程序将会崩溃。自然，这只会在生产环境的凌晨3:30发生。

为了防止这个问题，可以使用`abc`模块将接口定义为抽象基类。该模块定义了一个基类（`ABC`）和一个装饰器（`@abstractmethod`），它们被结合使用来描述接口。这里有一个示例：

点击此处查看代码图片

```python
from abc import ABC, abstractmethod

class Stream(ABC):
    @abstractmethod
    def receive(self):
        pass

    @abstractmethod
    def send(self, msg):
        pass

    def close(self):
        pass
```

抽象类不是设计用于直接实例化的。事实上，如果你尝试创建一个`Stream`实例，你会得到一个错误：

点击此处查看代码图片

```python
>>> s = Stream()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class Stream with abstract
  methods close, receive
```

错误信息会准确地告诉你`Stream`需要实现哪些方法。这为编写子类提供了指南。假设你写了一个子类但犯了错误：
