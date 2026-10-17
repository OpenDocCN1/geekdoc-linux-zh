
在这里，我们导入了通过 `PyQt4` 模块提供给我们的 `QtCore` 模块中的所有类。当我们执行涉及 `QStrings` 和 Python 字符串的操作时，结果字符串始终为 `QStrings`，如 `type()` 函数所示。

使用 `PyQt` 时，接受字符串参数的 `Qt` 方法可以接收 `str`、`unicode` 或 `QString` 类型的参数，并且 `PyQt` 会自动执行必要的转换。返回字符串的 `Qt` 方法始终返回 `QStrings`。鉴于 Python 的动态类型特性，我们很容易混淆，不确定拥有的是 `QString` 还是 `Python` 字符串。因此，明智的做法是确定一个字符串使用策略，以便我们始终清楚自己的立场。

我们在 `PyQt` 中使用的策略如下：

- 仅在处理严格的 7 位 `ASCII` 字符串或原始 8 位数据（即原始字节）时，才使用 `str` 类型。
- 对于仅由 `PyQt` 函数使用的字符串，例如由一个 `PyQt` 函数返回并随后传递给另一个 `PyQt` 函数的字符串——不要转换此类字符串。简单地保持它们为 `QStrings`。
- 在所有其他情况下，使用 `unicode` 字符串，并尽快将 `QStrings` 转换为 `unicode`。换句话说，一旦从 `Qt` 函数返回 `QString`，始终立即将其转换为 `unicode` 类型。

这一策略意味着我们避免了关于 8 位字符串编码的错误假设（因为我们使用 `Unicode`）。它还确保传递给 `Python` 函数的字符串具有 `Python` 预期的方法；由于 `QStrings` 具有与 `str` 和 `unicode` 不同的方法，因此将它们传递给 `Python` 函数可能会导致错误。`PyQt` 使用 `QString` 而不是 `unicode`，因为在 `PyQt` 最初创建时，Python 的 Unicode 支持远不如今天完善。

## 集合

一旦我们拥有了变量，即指向特定类型对象的单独命名对象引用，我们很自然希望拥有整个对象引用集合。Python 的标准集合类型持有对象引用，因此实际上可以持有任意类型对象的集合。集合使用对象引用的另一个结果是，它们可以引用不同类型的对象：它们并不限制只持有单一类型的项。

内置集合类型包括 `tuple`（元组）、`list`（列表）、`dict`（字典）、`set`（集合）和 `frozenset`（不可变集合）。除了 `tuple` 和 `frozenset` 之外，其他都是可变的，因此可以从列表、字典和集合中添加和删除项。`collections` 模块提供了其他一些可变集合类型。

Python 标准库中有一种集合类型不持有对象引用；相反，它持有指定类型的数字。这就是 `array`（数组）类型，它用于需要尽可能高效地存储和处理大量数字的情况。

在本节中，我们将查看 Python 的内置集合类型。

### 元组

元组是零个或多个对象引用的有序序列。与字符串（正如我们将很快看到的那样，也与列表）类似，元组支持序列函数如 `len()`，以及我们之前看到的相同切片语法。这使得从元组中提取项目非常容易。然而，元组是不可变的，因此我们无法替换或删除其中的任何项。如果我们想修改有序序列，只需使用列表代替元组；或者如果我们已经有一个元组但想修改它，只需将其转换为列表，然后应用我们的更改。

我们之前已经非正式地接触过元组；例如，我们在 IDLE 中的某些交互产生了以元组形式包裹的结果，我们还使用元组为 `%` 运算符提供多个参数。以下是一些构造元组的示例：

```python
>>> empty = ()
>>> type(empty)
<type 'tuple'>
>>> one = ("Canary")
```

*`Qt` 库为 C++ 提供了自己丰富的容器类集合，但这些在 `PyQt` 中不可用，而且无论如何，Python 自己的集合类已经足够好了。*

```python
>>> type(one)
<type 'str'>
>>> one = ("Canary",)
>>> type(one)
<type 'tuple'>
```

创建一个空元组很简单，但对于包含单个元素的元组，我们必须使用逗号来将其与带括号的表达式区分开来：

```python
>>> things = ("Parrot", 3.5, u"€")
>>> type(things)
<type 'tuple'>
```

元组可以容纳任意类型的元素；在这里我们有 `str`、`float` 和 `unicode` 类型的元素。对于至少包含两个元素且含义明确的元组，还可以省略括号：

```python
>>> items = "Dog", 99, "Cow", 28
>>> type(items)
<type 'tuple'>
```

元组可以任意嵌套，也可以进行切片，如下例所示：

```python
>>> names = "Albert", "Brenda", "Cecil", "Donna"
>>> names[:3]
('Albert', 'Brenda', 'Cecil')
>>> names[1]
'Brenda'
```

我们创建了一个姓名元组，然后取前三个元素的切片，再查看索引位置为 1 的元素。与所有 Python 序列一样，第一个元素位于位置 0：

```python
>>> names = names[0], names[1], "Bernadette", names[2], names[3]
>>> names
('Albert', 'Brenda', 'Bernadette', 'Cecil', 'Donna')
```

现在我们将 `names` 元组更改为引用一个在中间多了一个元素的新元组。可能会有人想用 `names[:1]` 代替 `names[0]`，以及用 `names[2:]` 代替后面两个名字，但如果这样做，结果会得到一个包含三个元素的元组：

```python
(('Albert', 'Brenda'), 'Bernadette', ('Cecil', 'Donna'))
```

这是因为当我们在元组上使用切片时，切片的结果始终也是元组本身。

```python
>>> names
('Albert', 'Brenda', 'Bernadette', 'Cecil', 'Donna')
>>> names = names[1:4]
>>> names
('Albert', 'Brenda', 'Bernadette', 'Cecil')
```

在这里，我们实际上是通过取前 4 个元素的元组（即索引位置为 0、1、2 和 3 的元素）截去了最后一个名字。在切片中，第一个数字是起始索引，该元素包含在结果中；第二个数字是结束索引，该元素不包含在结果中。

```python
>>> names
('Albert', 'Brenda', 'Bernadette', 'Cecil')
>>> names = names[: -1]
>>> names
('Albert', 'Brenda', 'Bernadette')
```

另一种截去最后一个元素的方法是从末尾开始索引；这样我们就不必知道元组的长度。但如果我们想了解长度，可以使用 `len()` 函数：

```python
>>> pets = (('Dog', 2), ('Cat', 3), ('Hamster', 14))
>>> len(pets)
3
>>> pets
(('Dog', 2), ('Cat', 3), ('Hamster', 14))
>>> pets[2][1]
14
>>> pets[1][0:2]
('Cat', 3)
>>> pets[1]
('Cat', 3)
```

元组可以嵌套，并使用尽可能多的方括号访问元素。

任何序列都可以传递给 `tuple` 构造函数来创建元组。例如：

```python
>>> tuple("some text")
('s', 'o', 'm', 'e', ' ', 't', 'e', 'x', 't')
```

当我们需要一个固定顺序的对象集合时，元组非常有用。它们也用作某些函数和方法的参数。例如，从 Python 2.5 开始，`str.endswith()` 方法接受单个字符串参数（例如 ".png"）或字符串元组（例如 `(".png", ".jpg", ".jpeg")`）。

## 列表

列表类型是一种有序序列类型，类似于元组类型。我们在处理字符串和元组时看到的序列函数和切片操作，对于列表也以完全相同的方式工作。元组与列表的区别在于，列表是可变的，并且拥有我们可以用来修改它们的方法。

而且，尽管元组使用括号创建，但列表使用方括号（或使用 `list()` 构造函数）创建。

让我们看一些提取列表部分的切片示例：

```python
>>> fruit = ["Apple", "Hawthorn", "Loquat", "Medlar", "Pear", "Quince"]
>>> fruit[:2]
['Apple', 'Hawthorn']
>>> fruit[-1]
'Quince'
>>> fruit[2:5]
['Loquat', 'Medlar', 'Pear']
```

在这里，我们使用了熟悉的切片语法，这些语法之前已用于字符串和元组。
