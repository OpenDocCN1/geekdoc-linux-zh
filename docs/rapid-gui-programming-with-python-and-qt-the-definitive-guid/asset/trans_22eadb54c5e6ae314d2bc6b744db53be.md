

称为格式化说明符的 % 项，格式化字符串中至少包含一个。格式化说明符由百分号（%）符号后跟一个格式化字符组成。百分号符号本身可以通过使用 %% 来指定。在示例中，我们使用了表示整数的 `%i`，表示字符串的 `%s`，以及表示浮点数的 `%f`。

之前我们研究了如何将子串插入到字符串中。我们展示了如何使用切片来完成此操作，以及使用字符串 `join()` 方法的更 Pythonic 的方式。这里介绍第三种方法，即使用格式化说明符：

```python
>>> p = "pad"
>>> p = "%s%s" % (p[::1], p[2:])
>>> p
'pod'
```

在这里，我们创建了一个新字符串，它由一个字符串（来自 p 的第一个切片）、"o" 和另一个字符串（来自 p 的第二个切片）组成。前面展示的 `join()` 方法用于字符串拼接；而这种方法用于字符串的“组合”。

我们可以在 % 项和字母之间添加一些信息，从而对 % 项的格式化进行一定程度的控制。例如，若要仅显示浮点数小数点后两位，我们可以使用说明符 `%.2f`：

```python
>>> "The length is %.2f meters" % 72.8958
'The length is 72.90 meters'
```

以下是更多示例，其中两个示例展示了 % 运算符与 print 语句配合使用的情况：

```python
>>> print "An integer", 5, "and a float", 65.3
An integer 5 and a float 65.3
>>> print "An integer %i and a float %f" % (5, 65.3)
An integer 5 and a float 65.300000
>>> print "An integer %i and a float %.1f" % (5, 65.3)
An integer 5 and a float 65.3
```

在许多情况下，`%i`（及其同义词 `%d`）、`%f` 和 `%s` 就足够了。关于可用的格式化说明符及其如何修改以获得特定结果的完整细节，请参阅 Python 文档；在此情况下，请查找“String Formatting Operations”（字符串格式化操作）。Python 中也可以使用其他字符串格式化方法，例如，string 模块中的 Template 类提供了类似 Perl 的插值功能。甚至可以使用类 C++ 语法；请参阅 *Python Cookbook* 中的配方 “Using a C++-like iostream Syntax”（使用类 C++ 的 iostream 语法）（参见侧边栏“Python 文档”）。

请注意，print 语句在打印的每个参数之间会自动输出一个空格。可以使用 `sys.stdout.write()` 代替 print 来避免这种情况；关于 `write()` 的更多说明将在第 6 章中给出。

## Python 文档

Python 附带了大量文档。大部分文档质量很高，但有些领域的覆盖范围相对较薄。使用 HTML 版本浏览文档需要练习，因为它更像是一本实体书而非在线文档，且页面之间的交叉引用链接太少。

Windows 用户在此方面比较幸运，因为文档以 Windows 帮助文件格式提供。单击 开始 → 所有程序 → Python 2.x → Python Manuals 即可启动 Windows 帮助浏览器。该工具具有索引和搜索功能，使查找文档变得容易。例如，若要查找有关字符串格式化说明符的信息，只需在索引行的编辑框中输入 "formatting"，条目 `formatting, string (%)` 将会出现。

浏览文档是非常值得的。我们建议查看 "Library Reference"（库参考）页面（lib.html），以了解 Python 标准库提供了哪些功能，并点击进入感兴趣主题的相关文档。这应该能让你对可用资源有一个初步印象，也有助于你建立关于在哪里可以找到感兴趣文档的心理图像。

请注意，某些主题在一个以上的标题下都有涵盖。例如，要阅读有关字符串的内容，请参阅 "Sequence Types"（序列类型）、"String Methods"（字符串方法）、"String Formatting Operations"（字符串格式化操作）和 "String Services"（字符串服务）。同样，对于文件和目录，请参阅 "File and Directory Access"（文件和目录访问）、"Data Compression and Archiving"（数据压缩和归档）以及 "Files and Directories"（文件和目录）。

对于更喜欢印刷版信息的人，以下几本书值得考虑。

-  Wesley Chun 著《Core PYTHON Programming》（核心 Python 编程）。这是一本 Python 教程，如果你完全是 Python 新手，并且希望比本书第一部分提供更慢的节奏，这本书可能适合你。
-  Alex Martelli 著《Python in a Nutshell》（Python 实战精要）。这是一本优秀的参考书，对 Python 语言和 Python 标准库进行了详细且准确的介绍。
-  由 Alex Martelli、Anna Martelli Ravenscroft 和 David Ascher 编辑的《Python Cookbook 2nd Edition》（Python 食谱第二版）。这本书提供了许多小的实用函数、类、代码片段和想法，有助于拓宽任何 Python 程序员对 Python 可能性的认识。这些食谱也可以在线 http://asp.activestate.com/ASP/Python/Cookbook 获取。

对于在线 Python 信息，起点是 http://www.python.org。该站点也是 Python wiki 的主页。可在 http://www.riverbankcomputing.co.uk 获取特定于 Python 的信息。PyQt wiki 位于 http://www.dio2ave.li.net/PyQtWiki。

使用 **PyQt** 时，我们可以访问一种额外的字符串类型 **QString**。与 Python 的 **str** 和 **unicode** 不同，**QString** 是可变的；这意味着我们可以原地更改 **QStrings**，插入和删除子串，以及更改单个字符。**QString** 的 API 与 **str** 和 **unicode** 提供的 API 有所不同。Qt 提供 **QString** 是因为 **Qt** 是用 C++ 编写的，而 C++ 尚未具备内置的 Unicode 支持。

**QString** 保存 Unicode 字符，但根据我们使用的 Python 版本不同，内部表示可能与 Python 的 Unicode 表示不同；这并不重要，因为 **PyQt** 可以轻松地在 **unicode** 和 **QString** 之间进行转换。例如：

```python
>>> from PyQt4.QtCore import *
>>> a = QString("apple")
>>> b = unicode("baker")
>>> print a + b
applebaker
>>> type(a + b)
<class 'PyQt4.QtCore.QString'>
```

在这里，我们导入了通过 **PyQt4** 模块提供给我们的 **QtCore** 模块中的所有类。当我们执行涉及 **QStrings** 和 Python 字符串的操作时，结果字符串始终为 **QStrings**，如 **type()** 函数所示。

使用 **PyQt** 时，接受字符串参数的 **Qt** 方法可以接收 **str**、**unicode** 或 **QString** 类型的参数，并且 **PyQt** 会自动执行必要的转换。返回字符串的 **Qt** 方法始终返回 **QStrings**。鉴于 Python 的动态类型特性，我们很容易混淆，不确定拥有的是 **QString** 还是 **Python** 字符串。因此，明智的做法是确定一个字符串使用策略，以便我们始终清楚自己的立场。

我们在 **PyQt** 中使用的策略如下：

- 仅在处理严格的 7 位 **ASCII** 字符串或原始 8 位数据（即原始字节）时，才使用 **str** 类型。
- 对于仅由 **PyQt** 函数使用的字符串，例如由一个 **PyQt** 函数返回并随后传递给另一个 **PyQt** 函数的字符串——不要转换此类字符串。简单地保持它们为 **QStrings**。
- 在所有其他情况下，使用 **unicode** 字符串，并尽快将 **QStrings** 转换为 **unicode**。换句话说，一旦从 **Qt** 函数返回 **QString**，始终立即将其转换为 **unicode** 类型。

这一策略意味着我们避免了关于 8 位字符串编码的错误假设（因为我们使用 **Unicode**）。它还确保传递给 **Python** 函数的字符串具有 **Python** 预期的方法；由于 **QStrings** 具有与 **str** 和 **unicode** 不同的方法，因此将它们传递给 **Python** 函数可能会导致错误。PyQt 使用 QString 而不是 unicode，因为在 PyQt 最初创建时，Python 的 Unicode 支持远不如今天完善。

## 集合

一旦我们拥有了变量，即指向特定类型对象的单独命名对象引用，我们很自然希望拥有整个对象引用集合。Python 的标准集合类型持有对象引用，因此实际上可以持有任意类型对象的集合。集合使用对象引用的另一个结果是，它们可以引用不同类型的对象：它们并不限制只持有单一类型的项。

内置集合类型包括 tuple（元组）、list（列表）、dict（字典）、set（集合）和 frozenset（不可变集合）。除了 tuple 和 frozenset 之外，其他都是可变的，因此可以从列表、字典和集合中添加和删除项。collections 模块提供了其他一些可变集合类型。

Python 标准库中有一种集合类型不持有对象引用；相反，它持有指定类型的数字。这就是 array（数组）类型，它用于需要尽可能高效地存储和处理大量数字的情况。

在本节中，我们将查看 Python 的内置集合类型。

### 元组

元组是零个或多个对象引用的有序序列。与字符串（正如我们将很快看到的那样，也与列表）类似，元组支持序列函数如 `len()`，以及我们之前看到的相同切片语法。这使得从元组中提取项目非常容易。然而，元组是不可变的，因此我们无法替换或删除其中的任何项。如果我们想修改有序序列，只需使用列表代替元组；或者如果我们已经有一个元组但想修改它，只需将其转换为列表，然后应用我们的更改。

我们之前已经非正式地接触过元组；例如，我们在 IDLE 中的某些交互产生了以元组形式包裹的结果，我们还使用元组为 % 运算符提供多个参数。以下是一些构造元组的示例：

```python
>>> empty = ()
>>> type(empty)
<type 'tuple'>
>>> one = ("Canary")
```

*Qt 库为 C++ 提供了自己丰富的容器类集合，但这些在 PyQt 中不可用，而且无论如何，Python 自己的集合类已经足够好了。*

