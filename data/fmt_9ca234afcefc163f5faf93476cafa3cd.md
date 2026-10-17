
```python
class wdict(dict):
    __slots__ = ('__weakref__',)

w = wdict()
w_ref = weakref.ref(w)  # 现在可以工作
```

在这里使用 `slots` 是为了避免不必要的内存开销，稍后会解释。

## 7.25 内部对象表示与属性绑定

与实例关联的状态存储在一个字典中，可以通过实例的 `__dict__` 属性访问。该字典包含了每个实例特有的数据。这里有一个例子：

点击此处查看代码图片

```python
>>> a = Account('Guido', 1100.0)
>>> a.__dict__
{'owner': 'Guido', 'balance': 1100.0}
```

可以随时向实例添加新属性。

点击此处查看代码图片

```python
a.number = 123456 # 向 a.__dict__ 中添加属性 'number'
a.__dict__['number'] = 67890
```

*(特别说明：由于您提供的原始文本从 "This might require a bit of study..." 之后开始包含了大量无意义的重复和乱码（如 "The use of slots here is to avoid..." 之后的无意义单词组合），为了保证翻译质量，我仅翻译了逻辑清晰的部分。如果需要处理特定的文本，请检查。)*

Python 的标准运算符可以工作。为了让这些运算符生效，你必须显式地实现所需的特殊方法。例如：

点击此处查看代码图片

```python
class ListLike:
    def __init__(self):
        self._items = list()

    def __getattr__(self, name):
        return getattr(self._items, name)

    def __len__(self):
        return len(self._items)

    def __getitem__(self, index):
        return self._items[index]

    def __setitem__(self, index, value):
        self._items[index] = value
```

## 7.27 使用 _slots_ 减少内存占用

正如我们所见，实例将其数据存储在字典中。当你创建大量实例时，这可能会引入大量的内存开销。如果你知道属性名称是固定的，可以在一个名为 `_slots_` 的特殊类中指定这些名称。这是一个示例：

点击此处查看代码图片

```python
class Account(object):
    __slots__ = ('owner', 'balance')
    ...
```

`Slots` 是一种定义提示，允许 Python 对内存和执行速度进行性能优化。带有 `_slots_` 的类实例不再使用字典来存储实例数据，而是使用一种基于数组的紧凑得的数据结构。在创建大量对象的程序中，使用 `_slots_` 可以显著减少内存占用，并略微提高执行速度。

`__slots__` 中的条目只有实例属性。你不需要列出方法、属性、类变量或任何其他类级属性。基本上，它们与通常出现在 `__dict__` 字典键中的名称是相同的。

请注意，`__slots__` 与继承之间存在复杂的相互作用。如果一个类继承自使用了 `__slots__` 的基类，那么它也需要定义 `__slots__` 来存储自己的属性（即使它没有添加任何新属性），以利用 `__slots__` 提供的优势。如果你忘记了这一点，派生类的运行速度可能会比任何一个类都没有使用 `__slots__` 时还要慢！

`__slots__` 与多继承不兼容。如果指定了多个带有非空 slots 的基类，你将得到一个 `TypeError`。

`__slots__` 的使用可能会破坏那些具有底层 `__dict__` 属性实例的代码。虽然这不适用于用户代码，但支持对象的实用库和其他工具可能被程序设计为查看 `__dict__` 以调试、序列化对象或其他操作。

`__slots__` 的存在不会影响类中重定义的诸如 `__getattribute__()`、`__getattr__()` 和 `__setattr__()` 方法的。然而，如果你正在实现此类方法，请注意此时不再有实例 `__dict__` 属性。你的实现需要考虑到这一点。

## 7.28 描述符 (Descriptors)

通常，属性访问对应于字典操作。如果需要更多的控制，可以将属性访问路由到用户定义的 get、set 和 delete 函数。已经描述了属性（properties）的使用。然而，属性实际上是使用一种称为描述符（descriptor）的低级构造结构来实现的。通过实现一个或多个特殊方法 `__get__()`、`__set__()` 和 `__delete__()`，你可以直接钩入属性访问机制并自定义这些操作。这里是一个示例：

点击此处查看代码图片

```python
class Typed:
    expected_type = object

    def __set_name__(self, cls, name):
        self.key = name

    def __get__(self, instance, cls):
        if instance:
            return instance.__dict__[self.key]
        else:
            return self

    def __set__(self, instance, value):
        if not isinstance(value, self.expected_type):
            raise TypeError(f'Expected {self.expected_type}')
        instance.__dict__[self.key] = value

    def __delete__(self, instance):
        raise AttributeError("Can delete attribute")
```

```python
class Integer (Typed):
    expected_type = int

class Float (Typed):
    expected_type = float

class String (Typed):
    expected_type = str
```

```python
# 使用示例:
class Account:
    owner = String()
    balance = Float()

    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance
```

在这个示例中，类 `Typed` 定义了一个描述符，在分配属性时会进行类型检查，并在尝试删除属性时产生错误。`Integer`、`Float` 和 `String` 子类通过特化 `Type` 来匹配特定类型。在另一个类（如 `Account`）中使用这些类，使得属性在访问时自动调用相应的 `__get__`、`__set__` 或 `__delete__` 方法。

例如：

点击此处查看代码图片

```python
a = Account('Guido', 1000.0)
b = a.owner                  # 调用 Account.owner.__get__(a, Account)
a.owner = 'Eva'             # 调用 Account.owner.__set__('Eva')
del a.owner                  # 调用 Account.owner.__delete__(a)
```

描述符只能在类级别实例化。在 `__init__()` 和其他方法中创建描述符对象来基于实例创建描述符是不合法的。描述符的 `__name__` 方法在类定义后后被调用。

```python
>>> r = Rectangle(3, 4)
>>> r.__dict__
{'width': 3, 'height': 4}
>>> r.area
12
>>> r.perimeter
14
>>> r.__dict__
{'width': 3, 'height': 4, 'area': 12, 'perimeter': 14 }
>>>
```

## 7.29 类定义过程

类的定义是一个动态过程。当你使用 `class` 语句定义类时，会创建一个新的字典作为局部类命名空间。然后，类体会作为脚本在该命名空间内执行执行。最终，该命名空间将成为生成的类对象的 `__dict__` 属性。
