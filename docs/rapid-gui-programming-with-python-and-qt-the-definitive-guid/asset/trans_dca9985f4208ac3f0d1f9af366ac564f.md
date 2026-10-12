

使用 `del` 对切片进行操作，或将零长度切片赋值给一个切片，可以删除多个连续项。要插入多个项，我们可以使用切片，也可以使用运算符 `+` 进行切片，而在末尾添加则可以使用 `extend()`。有关适用于列表的方法和函数的摘要，请参阅表 1.4。

## 字典

`dict` 类型是一种数据字典，也称为关联数组。字典保存一组无序的键值对，并提供非常快速的键查找。键是唯一的，且必须为不可变类型，如 Python 字符串、数字或元组；值可以是任意类型（包括集合类型），因此可以创建任意嵌套的数据结构。虽然字典不是序列，但我们仍可以获取其键和值的序列，这将在下一章中详细说明。

其他语言中也存在类似的数据结构——例如 Perl 的哈希（hash）、Java 的 HashMap 以及 C++ 的 unordered_map。

请注意，元组可以作为字典的键，但列表不行，因为字典的键必须是不可变的。在仅提供简单键（如字符串和数字）的语言中，希望使用多项目键的程序员不得不将他们的各项转换为字符串，但在 Python 中，得益于元组，这种变通方法是不必要的。

以下是一些示例，展示了如何创建字典以及访问其中的项：

```python
>>> insects = {"Dragonfly": 5000, "Praying Mantis": 2000,
"Fly": 120000, "Beetle": 350000}
>>> insects
{'Fly': 120000, 'Dragonfly': 5000, 'Praying Mantis': 2000,
'Beetle': 350000}
>>> insects["Dragonfly"]
5000
>>> insects["Grasshopper"] = 20000
>>> insects
{'Fly': 120000, 'Dragonfly': 5000, 'Praying Mantis': 2000,
'Grasshopper': 20000, 'Beetle': 350000}
```

可以从字典中删除项，其方式与从列表中删除项相同。例如：

```python
>>> del insects["Fly"]
>>> insects
{'Dragonfly': 5000, 'Praying Mantis': 2000, 'Grasshopper': 20000,
'Beetle': 350000}
>>> insects.pop("Beetle")
350000
>>> insects
{'Dragonfly': 5000, 'Praying Mantis': 2000, 'Grasshopper': 20000}
```

### 表 1.5 选定的字典方法和函数

| 语法 | 描述 |
| :--- | :--- |
| `x in d` | 如果项 x 在字典 d 中，则返回 True |
| `x not in d` | 如果 x 不在字典 d 中，则返回 True |
| `len(d)` | 返回字典 d 中的项数 |
| `d.clear()` | 从字典 d 中移除所有项 |
| `d.copy()` | 返回字典 d 的浅拷贝 |
| `d.keys()` | 返回字典 d 中所有键的列表 |
| `d.values()` | 返回字典 d 中所有值的列表 |
| `d.items()` | 返回字典 d 中所有 (键, 值) 对的元组列表 |
| `d.get(k)` | 返回键 k 对应的值，若无则返回 None |
| `d.get(k, x)` | 如果 k 在字典 d 中，则返回键 k 对应的值；否则返回 x |
| `d.setdefault(k, x)` | 与 get() 方法相同，区别在于如果键不在字典 d 中，则插入一个新项，其键为给定键，值默认为 None，如果提供了 x 则为 x |
| `d.pop(k)` | 返回并移除键 k 对应的项；如果字典 d 中没有该键，则引发 KeyError 异常 |
| `d.pop(k, x)` | 如果 k 在字典 d 中，则返回并移除键 k 对应的项；否则返回 x |

可以使用 `dict()` 构造函数来构建字典，如果键恰好是有效的标识符（即以字母开头的字母数字组合，且不含空白字符），我们可以使用更便捷的语法：

```python
>>> vitamins = dict(B12=1000, B6=250, A=380, C=5000, D3=400)
>>> vitamins
{'A': 380, 'C': 5000, 'B12': 1000, 'D3': 400, 'B6': 250}
```

我们之前提到字典的键可以是元组；这里提供最后一个示例来展示这一特性：

```python
>>> points3d = {(3, 7, -2): 'Green', (4, -1, 11): 'Blue',
(8, 15, 6): 'Yellow'}
>>> points3d
{(4, -1, 11): 'Blue', (8, 15, 6): 'Yellow', (3, 7, -2): 'Green'}
>>> points3d[(8, 15, 6)]
'Yellow'
```

在第 2 章中，我们将学习如何以“自然”的任意顺序以及按键顺序对字典进行迭代。

## 集合

Python 提供了两种集合类型：`set` 和 `frozenset`。两者都是无序的，因此都不是序列。集合是可变的，因此可以添加和移除项。冻结集合（frozensets）是不可变的，不能修改；不过，这意味着它们适合作为字典的键。

集合中的每个项都是唯一的；如果我们尝试添加一个已存在的项，`add()` 调用将不会执行任何操作。如果两个集合包含相同的项，无论这些项的插入顺序如何，这两个集合都是相等的。集合类似于只有键而没有值的字典。另一方面，列表保持其项的插入顺序（除非已排序），并允许重复项。

冻结集合通过单个序列参数构建——例如元组或列表。集合可以以相同方式构建。例如：

```python
>>> unicorns = set(("Narwhal", "Oryx", "Eland"))
>>> "Mutant Goat" in unicorns
False
>>> "Oryx" in unicorns
True
```

由于我们创建的是一个集合而非冻结集合，因此可以添加和移除项。例如：

```python
>>> unicorns.add("Mutant Goat")
>>> unicorns
set(['Oryx', 'Mutant Goat', 'Eland', 'Narwhal'])
>>> unicorns.add("Eland")
>>> unicorns
set(['Oryx', 'Mutant Goat', 'Eland', 'Narwhal'])
>>> unicorns.remove("Narwhal")
>>> unicorns
set(['Oryx', 'Mutant Goat', 'Eland'])
```

集合类还支持标准的集合运算——例如并集、交集和差集——某些运算同时提供方法和运算符，如表 1.6 所示。

### 表 1.6 选定的集合方法和函数

| 语法 | 描述 |
| :--- | :--- |
| `x in s` | 如果项 *x* 在集合 *s* 中，则返回 True |
| `x not in s` | 如果项 *x* 不在集合 *s* 中，则返回 True |
| `len(s)` | 返回集合 *s* 中的项数 |
| `s.clear()` | 从集合 *s* 中移除所有项 |
| `s.copy()` | 返回集合 *s* 的浅拷贝 |
| `s.add(x)` | 如果项 *x* 尚未在 *s* 中，则将其添加到集合 *s* |
| `s.remove(x)` | 从集合 *s* 中移除项 *x*，如果 *x* 不在 *s* 中则引发 `KeyError` 异常 |
| `s.discard(x)` | 如果项 *x* 在集合 *s* 中，则将其移除 |
| `s.issubset(t)` 或 `s <= t` | 如果集合 *s* 是集合 *t* 的子集，则返回 True |
| `s.issuperset(t)` 或 `s >= t` | 如果集合 *s* 是集合 *t* 的超集，则返回 True |
| `s.union(t)` 或 `s \| t` | 返回一个新集合，包含集合 *s* 和集合 *t* 中的所有项 |
| `s.intersection(t)` 或 `s & t` | 返回一个新集合，包含同时存在于集合 *s* 和集合 *t* 中的每个项 |
| `s.difference(t)` 或 `s - t` | 返回一个新集合，包含在集合 *s* 中但不在集合 *t* 中的每个项 |
| `s.symmetric_difference(t)` 或 `s ^ t` | 返回一个新集合，包含在 *s* 或 *t* 中但不同时在两者中的项 |

## 内置函数

如前所述，Python 有许多内置函数和运算符；例如 `del`、`print`、`len()` 和 `type()`。表 1.7–1.9 展示了一些其他有用的内置函数，其中一些我们将在本节中讨论。

在 IDLE 中，或直接在 Python 解释器中，我们可以使用 `help()` 函数获取有关对象的信息，或进入 Python 的交互式帮助系统。例如：

```python
>>> help(str)
```

### 表 1.7 选定的序列相关内置函数

| 语法 | 描述 |
| :--- | :--- |
| `all(q)` | 如果 *q* 中的所有项都为 True，则返回 True；*q* 是一个*可迭代对象*——例如字符串或列表等序列 |
| `any(q)` | 如果 *q* 中任何项为 True，则返回 True |
| `x in q` | 如果项 *x* 在序列 *q* 中，则返回 True；也适用于字典 |
| `x not in q` | 如果项 *x* 不在序列 *q* 中，则返回 True；也适用于字典 |
| `len(q)` | 返回序列 *q* 中的项数；也适用于字典 |
| `max(q)` | 返回序列 *q* 中的最大项 |
| `min(q)` | 返回序列 *q* 中的最小项 |
| `sum(q)` | 返回序列 *q* 中各项的总和 |

