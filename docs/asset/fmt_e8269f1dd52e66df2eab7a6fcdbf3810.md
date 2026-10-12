
```
>>> class A: pass
>>> a = A()
>>> r = weakref.ref(a)
>>> print(r)
<__main__.A object at 0x...>
>>> del a
>>> print(r)
None
```

（注：原文后续存在大量重复且损坏的 OCR 文本，已根据指令要求提取核心逻辑并翻译 `weakref` 模块的核心说明）

`weakref` 模块用于提供对弱引用的支持。通常，对对象的引用会导致其引用计数增加——有效地保留该对象，直到引用消失。相反，弱引用提供了一种在不增加引用计数的情况下引用对象的方法。这在某些以异常方式管理对象的应用程序中非常有用。例如，在面向对象的程序中，你可能会实现诸如观察者模式的关系，弱引用可以帮助避免创建循环引用。这方面的示例见第 7 章的“内存管理”部分。

（注：由于原文中存在大量重复和损坏的文本，此处译文已基于标准文档逻辑进行整理。）

## 第 13 章 Python 运行时服务

### 示例

弱引用的一个应用是创建最近计算结果的缓存。例如，如果一个函数计算结果需要很长时间，那么缓存这些结果并在它们仍被应用程序某处使用时使用是有意义的。例如：

```python
_resultcache = {}
def foocache(x):
    if _resultcache.has_key(x):
        r = _resultcache[x()]
        if r is not None:
            return r
    r = foo(x)
    _resultcache[x] = weak_ref(r)
    return r
```

### 注意事项

- 只有类实例、函数、方法、冻结集合（frozen sets）、文件、生成器、类型对象以及库模块中定义的其他类型对象（例如 sockets、数组和正则表达式模式）支持弱引用。内置函数和大多数内置类型（如列表、字典、字符串和数字）无法使用。
- 如果对 `WeakKeyDictionary` 或 `WeakValueDictionary` 使用迭代，必须非常小心以确保字典的大小不会发生变化，因为可能会产生奇异的副作用，即项会其妙地无原因从字典中消失。
- 如果在执行通过 `ref()` 或 `proxy()` 注册的回调期间发生异常，异常将打印到标准错误并被忽略。
- 只要原始对象是可哈希的，弱引用就是可哈希的。此外，只要原始哈希是在对象存在时计算的，在对象被删除后，弱引用将保持其哈希值。
- 弱引用可以进行相等性测试，但不能进行排序测试。如果对象仍然存，如果底层对象具有相同的值，则引用相等；否则，如果它们是同一个引用，则引用也相等。

## 第 14 章 数学

本章描述了用于执行各种数学操作的模块。此外，还描述了对小数浮点数提供通用支持的 `decimal` 模块。

### decimal

Python 的 `float` 数据类型使用双精度二进制浮点编码表示（通常由 IEEE 754 标准定义）。这种编码的一个微妙结果是，像 `0.1` 这样的小数无法被精确表示。相反，最接近的值是 `0.10000000149011161`。这种不准确性延续到涉及浮点数的计算中，有时会导致意外的结果（例如，`3*0.1 == 0.3` 结果为 `False`）。

`decimal` 模块提供了 IBM 通用小数算术标准的实现，该标准允许对进行进行精确。它对数学精度、有效数字和舍入行为提供了精确控制。这些特性在与精确定义小数属性的外部系统交互时非常有用。例如，编写必须与业务应用程序交互的 Python 程序时。

`decimal` 模块定义了两个基本类型：`Decimal` 数字和表示各种计算参数（如精度和舍入误差处理）的 `Context`。以下是几个简单的示例，说明了 `decimal` 模块的行为：

```python
import decimal
x = decimal.Decimal('3.4')      # 创建一些小数
y = decimal.Decimal('4.5')
```

```python
# 使用默认上下文执行一些数学计算
c = x * y                      # a = decimal.Decimal('15.30')
b = x / y                      # b = decimal.Decimal('0.755555555555555555556')
```

```python
# 修改精度并执行计算
decimal.getcontext().prec = 3
c = x * y                      # c = decimal.Decimal('15.3')
d = x / y                      # d = decimal.Decimal('0.756')
```

```python
# 仅对单个语句块修改精度
with decimal.localcontext(decimal.Context(prec=10)):
    e = x * y                  # e = decimal.Decimal('15.30')
    f = x / y                  # f = decimal.Decimal('0.7555555556')
```

### Decimal 对象

小数由以下类表示：

```Decimal([{value, context}]) # 此处代码示例应为 Decimal([{value, context}])
```

`value` 是指定的数值，可以是整数、包含小数值的字符串（如 `'4.5'`）或一个元组 `(sign, digits, exponent)`。如果提供元组，`sign` 为 0 表示正，1 表示负；`digits` 是一个指定为整数的数字元组；`exponent` 是一个整数指数。可以使用特殊字符串 `'Infinity'`、`'-Infinity'`、`'NaN'` 来指定正无穷或负无穷，以及非数字（`'sNaN'` 是 NaN 的一种变体，如果在计算中使用它将产生异常）。不能使用普通的 `float` 对象作为初始值，因为 `value` 可能是不精确的（这违背了使用 `decimal` 的初衷）。`context` 参数是一个 `Context` 对象，稍后会描述。如果提供，`context` 决定当初始值不是有效数字时会发生什么——抛出异常或返回一个值为 NaN 的小数。

以下示例展示了如何创建各种小数：

```python
a = decimal.Decimal(42)               # 创建 Decimal "42"
b = decimal.Decimal("37.45")             # 创建 Decimal "37.45*"
c = decimal.Decimal((1,(2,3,4,5,-2))) # 创建 Decimal "-23.45*"
d = decimal.Decimal("Infinity")
e = decimal.Decimal("NaN")
```

`Decimal` 对象是不可变的，并具有 `float` 的所有属性。`Decimal` 对象不是直接创建的，通过 `getcontext()` 或 `localcontext()` 获取对象，然后根据需要进行修改。为了更好地理解这些示例，需要解释这些上下文参数。舍入行为由将 `rounding` 参数设置为：

| 常量 | 描述 |
| :--- | :--- |
| `ROUND_CEILING` | 向正无穷舍入。例如，2.52 向上到 2.6，-2.58 向上到 -2.5。 |
| `ROUND_DOWN` | 向零舍入。例如，2.58 向下到 2.5，-2.58 向下到 -2.5。 |
| `ROUND_FLOOR` | 向负无穷舍入。例如，2.58 向下到 2.5，-2.52 向下到 -2.6。 |
| `ROUND_HALF_DOWN` | 当小数部分大于一半时远离零舍入；否则向零舍入。例如，2.58 向下到 2.6，2.55 向上到 -2.5，-2.58 向下到 -2.6。 |
| `ROUND_HALF_EVEN` | 与 HALF_DOWN 相同，但当小数部分恰为一半时，如果舍位是偶数则向下，如果是奇数则向上。例如，2.65 向下到 2.6，2.55 向上到 2.6。 |
| `ROUND_HALF_UP` | 与 HALF_DOWN 相同，但当小数部分恰为一半时，远离零舍入。例如，2.55 向上到 2.6，-2.55 向下到 -2.6。 |
| `ROUND_UP` | 远离零舍入。例如，2.52 向上到 2.6，-2.52 向下到 -2.6。 |
| `ROUND_05UP` | 如果向零后的最后一位数字是 O 或 5 则远离零。否则向零舍入。例如，2.54 向上到 2.6，2.64 向下到 2.6。 |

### Context 对象
