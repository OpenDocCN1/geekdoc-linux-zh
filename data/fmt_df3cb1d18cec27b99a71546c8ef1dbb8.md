
```python
connections.Client(address [, family [, authenticate [, authkey]]])
connections.Listener(address [, family [, authenticate [, authkey]]])
```

`Client` 用于连接到远程管理器对象，其地址是传递给 `BaseManager` 构造函数的。`Listener` 用于监听连接。如果 `family` 缺失，则默认使用 `socket`。如果 `authenticate` 缺失，则不进行认证。如果 `authkey` 缺失，则不使用密钥。

```python
connections.Client(address [, family [, authenticate [, authkey]]])
connections.Listener(address [, family [, authenticate [, authkey]]])
```

一个用于连接的类。如果 `authenticate` 失败，则抛出异常。

```python
connections.Client(address [, family [, authenticate [, authkey]]])
connections.Listener(address [, family [, authenticate [, authkey]]])
```

如果 `address` 缺失，则 。返回一个 。

```python
connections.Client(address [, family [, authenticate [, authkey]]])
connections.Listener(address [, family [, authenticate [, authkey]]])
```

# 示例代码：

```python
import multiprocessing
from multiprocessing.managers import BaseManager

class A(Object):
    def __init__(self, value):
        self.x = value
    def __repr__(self):
        return "A(%s)" % self.x
    def getx(self):
        return self.x
    def setX(self, value):
        self.x = value
    def __add__(self, value):
        self.x += value
        return self

class MyManager(BaseManager): pass
MyManager.register("A", A)

if __name__ == '__main__':
    m = MyManager()
    m.start()
    # 创建一个托管对象
    a = m.A(37)
```

在此示例中，最后一条语句创建了 `A` 的实例，该实例运行在管理器服务器上。之前代码中的变量 `a` 仅是该实例的代理。该代理的行为与服务器上的对象类似（但并不完全相同）refer.

# 432 第 20 章 线程与并发

首先，你会发现数据属性和属性无法被访问。相反，你必须使用访问函数：

```python
>>> a.x
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
AttributeError: 'AutoProxy[A]' object has no attribute 'x'
>>> a.get()
37
>>> a.setX(42)
```

使用代理时，`repr()` 返回一个表示代理的字符串，而 `str()` 返回被引用对象的 `__repr__()` 的输出。例如：

```python
>>> a
<AutoProxy[A] object, typed 'A' at 0xcef230
>>> print(a)
A(37)
>>>
```

特殊方法和任何以下划线 (`_`) 开头的方法在代理上都是不可用的。例如，如果你尝试调用 `a.__iadd__()`，它是不起作用的：

```python
>>> a += 1
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: unsupported operand type for +=: 'AutoProxy[A]' and 'int'
>>> a.__iadd__(37)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
AttributeError: 'AutoProxy[A]' object has no attribute '__iadd__'
>>>
```

在高级应用中，可以自定义代理以更仔细地控制访问。这是通过定义继承自 `multiprocessing.managers` 中 `BaseProxy` 的类来实现的。以下代码展示了如何为前一个示例中的 `A` 类创建一个自定义代理，以正确暴露 `__iadd__()` 方法并使用代理来暴露属性：

```python
from multiprocessing.managers import BaseProxy

class AProxy(BaseProxy):
    # 被引用对象暴露的所有属性的列表
    exposed = ('__iadd__', 'getX', 'setX')
    # 实现代理的公共接口
    def __iadd__(self, value):
        return self._callmethod('__iadd__', (value,))
    @property
    def x(self):
        return self._callmethod('getX')
    @x.setter
    def x(self, value):
        return self._callmethod('setX', (value,))

class MyManager(BaseManager):
    Manager.register("A", A, proxytype=APProxy)
```

派自 `BaseProxy` 的类实例具有以下方法：

```python
proxy._callmethod([name, args [, kwargs]])
```

在代理的被引用对象上调用方法名。`name` 是包含名称的字符串，`args` 是包含位置参数的元组，`kwargs` 是关键字参数的字典。该方法名必须显式暴露。通常通过将名称包含在代理类的 `exposed_` 类属性中来实现。

```python
proxy.get()
```

在调用者中返回被引用对象的副本。如果此调用发生在不同的进程中，被引用对象将被序列化（pickle）、发送给调用者并反序列化。如果被引用对象无法序列化，则抛出异常。

# 连接

使用 `multiprocessing` 模块的程序可以与运行在同一机器或远程系统上的进程进行消息传递。如果你想将一个编写为单一系统的程序通过在集群上计算来扩展它，这将非常有用。`multiprocessing.connection` 子模块提供了为此目的的类：

```python
connections.Client(address [, family [, authenticate [, authkey]]])
connections.Listener(address [, family [, authenticate [, authkey]]])
```

用于此目的的类包括：

```python
connections.Client(address [, family [, authenticate [, authkey]]])
connections.Listener(address [, family [, authenticate [, authkey]]])
```

`Client` 用于连接到远程管理器对象，其地址是传递给 `BaseManager` 构造函数的。`Listener` 用于监听连接。如果 `family` 缺失，则默认使用 `socket`。如果 `authenticate` 缺失，则不进行认证。如果 `authkey` 缺失，则不使用密钥。

```python
connections.Client(address [, family [, authenticate [, authkey]]])
connections.Listener(address [, family [, authenticate [, authkey]]])
```
