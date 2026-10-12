
Traceback (most recent call last):

File "stdin", line 1, in <module>

TypeError: unsupported operand type(s) for: 'int' and 'Complex'

>>>

```

操作 `c + 4.0` 完美运行。Python 的内置数字类型已经具有 `.real` 和 `.imag` 属性。

操作 `4.0 + c` 完全无法工作，因为内置的浮点类型并不知道 `Complex` 类的信息。要修复这个问题，你可以为 `Complex` 类实现反向操作方法（reversed-operand methods）：

```python
class Complex(object):
    def __add__(self, other):
        return Complex(other.real + self.real, other.imag + self.imag)
    def __sub__(self, other):
        return Complex(other.real - self.real, other.imag - self.imag)
```
```

这些方法作为备选。如果操作 `4.0 + c` 失败，Python 在抛出 `TypeError` 之前尝试执行 `c.__add__(4.0)`。

旧版本的 Python 在混合类型操作中尝试过各种处理复数的方法。例如，你可能会遇到实现 `coerce()` 方法的旧版 Python 类。这在 Python 2.6 或 Python 3 中不再使用。此外，不要被 `__int__()`、`__float__()` 或 `__complex__()` 等特殊方法误导。尽管它们会被 `int(x)` 或 `float(x)` 等显式转换调用，但它们永远不会被隐式调用来执行混合算术类型中的类型转换。因此，如果你正在编写运算符必须处理混合类型所需的类，你必须在每个运算符的实现中显式处理类型转换。

## 类型与类成员测试

当你创建一个类的实例时，该实例的类型就是类本身。要测试是否属于某个类，请使用内置的 `isinstance(obj, cname)`。如果对象 `obj` 属于类 `cname` 或派生自 `cname` 的任何类，该函数返回 `True`。这是一个示例：

```python
class A(object): pass
class B(A): pass
class C(object): pass
```

```python
a = A()                # 'A' 的实例
b = B()                # 'B' 的实例
c = C()                # 'C' 的实例
```

```python
type(a)               # 返回类 A
isinstance(a,A)      # 返回 True
isinstance(b,A)      # 返回 True, B 继承自 A
isinstance(b,C)      # 返回 False, C 未继承自 A
```

同样，内置函数 `issubclass(A,B)` 在类 `A` 是类 `B` 的子类时返回 `True`。这是一个示例：

```python
issubclass(B,A)      # 返回 True
issubclass(C,A)      # 返回 False
```

对象类型检查中一个微妙的问题是，程序员经常绕过继承，创建模拟另一个对象行为的类。例如，考虑这两个类：

```python
class Foo(object):
    def spam(self, a, b):
        pass
```

```python
class FooProxy(object):
    def __init__(self, f):
        self._f = f
    def spam(self, a, b):
        return self._f.spam(a,b)
```

在这个示例中，`FooProxy` 在功能上与 `Foo` 相同。它实现了这些方法并在底层使用了 `Foo`。然而，在类型系统中，`FooProxy` 与 `Foo` 不同。例如：

```python
f = Foo()                  # 创建一个 Foo
g = FooProxy(f)        # 创建一个 FooProxy
isinstance(g, Foo)      # 返回 False
```

如果程序编写为使用 `isinstance()` 显式检查是否为 `Foo`，那么它无法与 `FooProxy` 对象一起工作。然而，这种严格程度通常不是你所想要的。相反，断言一个对象可以被 `Foo` 简单使用可能意义，因为可以定义一个对象来重新定义 `isinstance()` 和 `issubclass()` 的行为，以便对对象进行分组和类型检查。这是一个示例：

```python
class IClass(object):
    def __init__(self):
        self._implementors = set()
    def register(self, C):
        self._implementors.add(C)
    def __instancecheck__(self, type):
        return self.__subclasscheck__(type)
    def __subclasscheck__(self, sub):
        return any(c in sub.implementors for c in sub.mro())
```

# 现在，使用上面的对象
`IFoo = IClass()`
`IFoo.register(Foo)`
`IFoo.register(FooProxy)`

在这个示例中，`IClass` 创建了一个仅仅用于对其他类进行分组的对象。

抽象类机制通过允许将预存对象组织成用户定义的类型层次来解决这个问题。此外

## 元类 (Metaclasses)

在 Python 中定义一个类时，类定义本身变成了一个对象。如下：

```python
class Foo(object): pass
isinstance(Foo,object)      # 返回 True
```

如果你对此思考足够久，你会发现类对象的创建是为了通过一种被称为“元类”的特殊对象来创建 `Foo` 对象。简单来说，元类是一个知道如何创建和管理类的对象。

在前面的例子中，控制 `Foo` 创建的元类是一个类型。事实上，如果你显示 `Foo` 的类型，你会发现它是一个 `type`：

```python
>>> type (Foo)
<type 'type'>
```

当使用 `class` 语句定义新类时，会发生很多事情。首先，类体会在其自己的私有字典中作为一系列语句执行。语句的执行与普通代码完全相同，区别在于会对私有成员进行名称处理（以 `__` 开头的名称）。最后，类的名称、基类列表和字典被传递给元类的构造函数，以创建相应的类对象。以下是工作原理示例：

```python
class_name = "Foo"               # 类名
class_parents = (object,)      # 基类
class_body = """
    def __init__(self,x):
        self.x = x
    def blah(self):
        print("Hello World")
"""
class_dict = {
    # 在本地字典 class_dict 中执行类体
exec(class_body,globals(),class_dict)
```

```python
# 创建类对象 Foo
Poo = type(class_name,class_parents,class_dict)
```

类创建中调用元类 `type()` 的最后一步是可以自定义的。类定义最后一步中发生的情况可以通过多种方式控制。首先，类可以显式指定其元类，通过设置 `_metaclass__` 类变量（Python 2），或者在基类元组中提供 `metaclass` 关键字参数（Python 3）。

```python
class Foo:
    # 在 Python 3 中，使用以下语法
    _metaclass__ = type Foo(metaclass=type)
```

如果没有显式指定元类，`class` 语句将检查基类元组中的第一个元素（如果有）。在这种情况下，元类与第一个基类的类型相同。因此，当你写：

```python
class Foo(object): pass
```
