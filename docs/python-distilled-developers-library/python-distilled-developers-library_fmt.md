
# Python 精粹（开发者库）

## 关于本书

ePUB 是一种开放的、行业标准的电子书格式。然而，不同阅读设备和应用程序对 ePUB 及其各项功能的支持程度各异。请使用您的设备或应用程序设置，根据个人喜好自定义显示效果。您可以自定义的设置通常包括字体、字体大小、单列或双列显示、横屏或竖屏模式，以及可以通过点击或轻触放大的插图。有关阅读设备或应用程序设置和功能的更多信息，请访问设备制造商的网站。

许多书籍包含编程代码或配置示例。为了优化这些元素的呈现效果，请在单列、横屏模式下阅读电子书，并将字体大小调整为最小设置。除了以可重排文本格式呈现代码和配置外，我们还包含了模拟印刷版呈现效果的代码图像；因此，在可重排格式可能会损害代码清单显示效果的地方，您将看到一个“点击此处查看代码图像”的链接。点击该链接即可查看与印刷版一致的代码图像。要返回之前查看的页面，请点击设备或应用程序上的“返回”按钮。

## 前言

距离我编写 `Python Essential Reference` 已经过去 20 多年。在那个时候，Python 还是一个规模小得多的语言，它的标准库提供了一套非常有用的“电池”。它在很大程度上是可以全部装在脑子里的。`Essential Reference` 反映了那个时代。它是一本小书，你可以随身携带，在荒岛上或秘密金库里编写一些 Python 代码。在随后的三次修订中，`Essential Reference` 始终坚持这个愿景：成为一本紧凑但完整的语言参考书——因为如果你打算在度假时用 Python 编程，为什么不把它的所有功能都用上呢？

如今，距离上一版的出版已经过去十多年，Python 的世界发生了巨大的变化。Python 不再是一门小众语言，而已成为世界上最受欢迎的编程语言之一。Python 程序员还能通过高级编辑器、IDE、notebook、网页等方式随时获取海量信息。事实上，当几乎任何你想要的参考资料只需敲击几个键就能出现在眼前时，可能几乎不需要再去查阅参考书了。

如果说有什么问题，那就是信息检索的便捷性和 Python 宇宙的庞大规模带来了一种不同类型的挑战。如果你刚刚开始学习或需要解决一个新问题，面对如此之多的内容，可能会感到无从下手。而且，将各种工具的特性与核心语言本身区分开来也可能很困难。这些问题正是本书的编写初衷。

`Python Distilled` 是一本关于 Python 编程的书。它并不试图记录 Python 中所有可能实现的功能或已经完成的工作。它的重点是呈现一个现代且经过精选（或称“蒸馏”）的语言核心。这本书得益于我多年来向科学家、工程师和软件专业人士教授 Python 的经验。

然而，它也是编写软件库、探索 Python 运行机制的边界并寻找最实用功能的产物。

在很大程度上，本书侧重于 Python 编程本身。这包括抽象技术、程序结构、数据、函数、对象、模块等等——这些主题将使任何规模的 Python 项目的程序员受益。可以通过 IDE 轻松获取的纯参考资料（如函数列表、命令名称、参数等）通常被省略了。我还特意选择不描述快速变化的 Python 工具世界——编辑器、IDE、部署及其相关事项。

也许会有争议，但我通常不关注与大规模软件项目管理相关的语言特性。Python 有时被用于构建庞大且严肃的项目——包含数百万行代码。此类应用需要专门的工具、设计和特性。它们还涉及委员会、会议以及关于非常重要事项的决策。所有这些对于这本小书来说都太多了。但或许诚实的答案是：我不用 Python 来编写此类应用——你也不应该这么做。至少作为业余爱好时不要这么做。

在写书时，对于不断演进的语言特性总有一个截断点。本书编写于 Python 3.9 时代。因此，它不包括后续版本计划中的一些重大新增功能——例如结构化模式匹配（structural pattern matching）。那是另一个时间、另一个地点的讨论主题。

最后但同样重要的一点是，我认为保持编程的乐趣至关重要。我希望我的书不仅能帮助你成为一名高效的 Python 程序员，还能捕捉到那些启发人们使用 Python 去探索星空、在火星上驾驶直升机以及在后院用水炮喷松鼠的魔力。

## 致谢

我要感谢技术审稿人 Shawn Brown、Sophie Tabac 和 Pete Fein 提供的宝贵建议。我还要感谢我的长期编辑 Debra Williams Cauley 在本项目及以往项目中的工作。许多参加过我课程的学生在间接层面给本书涵盖的主题产生了重大影响。最后，我要感谢 Paula、Thomas 和 Lewis 的支持与爱。

## 关于作者

**David Beazley** 是 `Python Essential Reference, Fourth Edition`（Addison-Wesley, 2010）和 `Python Cookbook, Third Edition`（O'Reilly, 2013）的作者。他目前通过自己的公司 Dabeaz LLC（`www.dabeaz.com`）教授高级计算机科学课程。他自 1996 年以来一直使用、编写、演讲并教授 Python。

# 1. Python 基础

本章将对 Python 语言的核心内容进行概述。涵盖变量、数据类型、表达式、控制流、函数、类以及输入/输出。本章最后将讨论模块、脚本编写、包，以及关于组织大型程序的几点技巧。本章并不旨在全面涵盖每一个特性，也不涉及围绕大型 Python 项目可能产生的所有工具链。然而，经验丰富的程序员应该能够根据这里的材料推演并编写更高级的程序。鼓励初学者在简单的环境中尝试示例，例如终端窗口和基础文本编辑器。

## 1.1 运行 Python

Python 程序由解释器执行。Python 解释器可以在许多不同的环境中运行——IDE、浏览器或终端窗口。然而，在这一切之下，解释器的核心是一个基于文本的应用程序，可以通过在 `bash` 等命令壳层中输入 `python` 来启动。由于同一台机器上可能同时安装了 Python 2 和 Python 3，你可能需要输入 `python2` 或 `python3` 来选择版本。本书假设使用 Python 3.8 或更新版本。

当解释器启动时，会出现一个提示符，你可以在一个所谓的“读取-求值-打印循环”（或 REPL）中输入程序。例如，在下面的输出中，解释器显示其版权信息并向用户呈现 `>>>` 提示符，用户在此输入一个熟悉的 “Hello World” 程序：

```text
Python 3.8.0 (default, Feb 3 2019, 05:53:21)
[GCC 4.2.1 Compatible Apple LLVM 8.0.0 (clang-800.0.38)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print('Hello World')
Hello World
>>>
```

某些环境可能会显示不同的提示符。以下输出来自 `ipython`（Python 的另一种壳层）：

```text
Python 3.8.0 (default, Feb 4, 2019, 07:39:16)
Type 'copyright', 'credits' or 'license' for more information
IPython 6.5.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: print('Hello World')
Hello World

In [2]:
```

无论你看到的输出形式如何，其底层原理是相同的。你输入一个命令，它运行，然后你立即看到输出。

Python 的交互模式是其最实用的特性之一，因为你可以输入任何有效的语句并立即看到结果。这对于调试和实验非常有用。包括作者在内的许多人都将交互式 Python 用作桌面计算器。例如：

```text
>>> 6000 + 4523.50 + 134.25
10657.75
>>> _ + 8192.75
18850.5
>>>
```

在交互式使用 Python 时，变量 `_` 保存上一次操作的结果。如果你想在随后的语句中使用该结果，这会非常方便。这个变量仅在交互模式下定义，因此请不要在保存的程序中使用它。

你可以通过输入 `quit()` 或 EOF（文件结束）字符来退出交互式解释器。在 UNIX 上，EOF 是 `Ctrl+D`；在 Windows 上，它是 `Ctrl+Z`。

## 1.2 Python 程序

如果你想创建一个可以重复运行的程序，请将语句放入一个文本文件中。例如：

```python
# hello.py

print('Hello World')
```

Python 源文件是 UTF-8 编码的文本文件，通常具有 `.py` 后缀。`#` 字符表示注释，注释一直延伸到行尾。只要你使用 UTF-8 编码，就可以在源代码中自由使用国际（Unicode）字符（大多数编辑器默认采用此编码，但如果你不确定，检查编辑器设置总是没有坏处的）。

要执行 `hello.py` 文件，请按如下方式将文件名提供给解释器：

```text
shell % python3 hello.py
Hello World
shell %
```

通常在程序的第一行使用 `#!` 来指定解释器，如下所示：

```python
#!/usr/bin/env python3

print('Hello World')
```

在 UNIX 上，如果你赋予该文件执行权限（例如通过 `chmod +x hello.py`），你就可以通过在 shell 中输入 `hello.py` 来运行该程序。

在 Windows 上，你可以双击 `.py` 文件，或在 Windows 开始菜单的“运行”命令中输入程序名称来启动它。如果提供了 `#!` 行，它将用于选择解释器版本（Python 2 与 3）。程序的执行可能会在一个控制台窗口中进行，该窗口在程序完成后会立即消失——通常在你阅读其输出之前就消失了。为了调试，最好在 Python 开发环境中运行程序。

解释器按顺序执行语句，直到到达输入文件的末尾。此时，程序终止，Python 退出。

## 1.3 原语、变量和表达式

Python 提供了一组原语类型，如整数、浮点数和字符串：

```python
42          # int
4.2         # float
'forty-two' # str
True        # bool
```

变量是一个引用值的名称。值代表某个类型的对象：

```python
x = 42
```

有时你可能会看到一个类型被显式地附加到名称上。例如：

```python
x: int = 42
```

该类型仅仅是一个用于提高代码可读性的提示。它可以被第三方代码检查工具使用。否则，它会被完全忽略。它并不会阻止你以后为其分配另一种类型的值。

表达式是原语、名称和运算符的组合，它会产生一个值：

```python
2 + 3 * 4          # -> 14
```

以下程序使用变量和表达式来执行复利计算：

```python
# interest.py

principal = 1000          # 初始金额
rate = 0.05               # 利率
numyears = 5              # 年数
year = 1

while year <= numyears:
    principal = principal * (1 + rate)
    print(year, principal)
    year += 1
```

执行时，它产生以下输出：

```text
1 1050.0
2 1102.5
3 1157.625
4 1215.5062500000001
5 1276.281562500003
```

`while` 语句测试紧随其后的条件表达式。如果测试条件为真，则执行 `while` 语句的主体。然后重新测试条件并再次执行主体，直到条件变为假。循环的主体由缩进表示。因此，`interest.py` 中 `while` 之后的三个语句在每次迭代时都会执行。Python 没有规定必须缩进的量，只要在同一个块内保持一致即可。最常见的是每级缩进使用四个空格。

`interest.py` 程序的一个问题是输出不够美观。为了改进它，你可以让列右对齐，并将本金的精度限制在两位小数。将 `print()` 函数改为使用所谓的 f-string，如下所示：

```python
print(f'{year:>3d} {principal:0.2f}')
```

在 f-string 中，可以通过将变量名和表达式括在花括号中来进行求值。可选地，每个替换项可以附加一个格式说明符。`'>3d'` 表示一个三位数的十进制数，右对齐。`'0.2f'` 表示一个精确到两位小数的浮点数。关于这些格式代码的更多信息可以在第 9 章中找到。

现在程序的输出如下所示：

```text
1 1050.00
2 1102.50
3 1157.62
4 1215.51
5 1276.28
```

## 1.4 算术运算符

Python 有一套标准的数学运算符，如表 1.1 所示。这些运算符的含义与大多数其他编程语言中的含义相同。

### 表 1.1 算术运算符

| 操作 | 描述 |
|---|---|
| `x + y` | 加法 |
| `x - y` | 减法 |
| `x * y` | 乘法 |
| `x / y` | 除法 |
| `x // y` | 截断除法 |
| `x ** y` | 幂（x 的 y 次幂） |
| `x % y` | 取模（x mod y）。余数 |
| `-x` | 一元负号 |
| `+x` | 一元正号 |

除法运算符（`/`）应用于整数时会产生一个浮点数。因此，`7 / 4` 为 `1.75`。截断除法运算符 `//`（也称为地板除）将结果截断为整数，且同时适用于整数和浮点数。取模运算符返回除法 `x // y` 的余数。例如，`7 % 4` 为 `3`。对于浮点数，取模运算符返回 `x // y` 的浮点数余数，即 `x - (x // y) * y`。

此外，表 1.2 中的内置函数提供了几个更常用的数值操作。

### 表 1.2 常用数学函数

| 函数 | 描述 |
|---|---|
| `abs(x)` | 绝对值 |
| `divmod(x, y)` | 返回 `(x // y, x % y)` |
| `pow(x, y [, modulo])` | 返回 `(x ** y) % modulo` |
| `round(x, [n])` | 四舍五入到 10 的 n 次方的最近倍数。 |

`round()` 函数实现了“银行家舍入法”。如果被舍入的值与两个倍数距离相等，它将被舍入到最接近的偶数倍（例如，`0.5` 被四舍五入为 `0.0`，`1.5` 被四舍五入为 `2.0`）。

整数提供了几个额外的运算符来支持位操作，如表 1.3 所示。

### 表 1.3 位操作运算符

| 操作 | 描述 |
|---|---|
| `x << y` | 左移 |
| `x >> y` | 右移 |
| `x & y` | 按位与 |
| `x | y` | 按位或 |
| `x ^ y` | 按位异或 |
| `~x` | 按位取反 |

人们通常将这些运算符与二进制整数一起使用。例如：

```python
a = 0b11001001
mask = 0b11110000
x = (a & mask) >> 4    # x = 0b1100 (12)
```

在这个例子中，`0b11001001` 是编写二进制整数值的方式。你也可以将其写成十进制的 `201` 或十六进制的 `0xc9`，但如果你在处理位，二进制能让你更容易地可视化你的操作。

位运算符的语义假设整数使用补码二进制表示，并且符号位向左无限扩展。如果你处理的是旨在映射到硬件原生整数的原始位模式，则需要格外小心。这是因为 Python 不会对位进行截断，也不允许数值溢出——相反，结果的绝对值将任意增大。你需要确保结果的大小正确，或者在必要时进行截断。

要比较数字，请使用表 1.4 中的比较运算符。

### 表 1.4 比较运算符

| 操作 | 描述 |
|---|---|
| `x == y` | 等于 |
| `x != y` | 不等于 |
| `x < y` | 小于 |
| `x > y` | 大于 |
| `x >= y` | 大于或等于 |
| `x <= y` | 小于或等于 |

比较的结果是一个布尔值 `True` 或 `False`。

`and`、`or` 和 `not` 运算符（不要与上面的位操作运算符混淆）可以构建更复杂的布尔表达式。这些运算符的行为如表 1.5 所示。

### 表 1.5 逻辑运算符

| 运算符 | 描述 |
|---|---|
| `x or y` | 如果 `x` 为假，返回 `y`；否则返回 `x`。 |
| `x and y` | 如果 `x` 为假，返回 `x`；否则返回 `y`。 |
| `not x` | 如果 `x` 为假，返回 `True`；否则返回 `False`。 |

如果一个值字面上是 `False`、`None`、数值零或为空，则被视为假。否则，被视为真。

编写一个更新值的表达式是很常见的。例如：

```python
x = x + 1
y = y * n
```

对于这些，你可以改为编写以下简写操作：

```python
x += 1
y *= n
```

这种简写形式的更新可以与任何 `+`、`-`、`*`、`**`、`/`、`//`、`%`、`&`、`|`、`^`、`<<`、`>>` 运算符一起使用。Python 没有在某些其他语言中可见的自增（`++`）或自减（`--`）运算符。

## 1.5 条件语句和控制流

`while`、`if` 和 `else` 语句用于循环和条件代码执行。这里有一个例子：

```python
if a < b:
    print('Computer says Yes')
else:
    print('Computer says No')
```



`if` 和 `else` 子句的主体通过缩进来表示。`else` 子句是可选的。要创建一个空子句，请使用 `pass` 语句，如下所示：

```python
if a < b:
    pass    # 不做任何事
else:
    print('Computer says No')
```

要处理多个测试用例，请使用 `elif` 语句：

```python
if suffix == '.htm':
    content = 'text/html'
elif suffix == '.jpg':
    content = 'image/jpeg'
elif suffix == '.png':
    content = 'image/png'
```

如果你在进行测试的同时要赋值，请使用条件表达式：

```python
maxval = a if a > b else b
```

这与较长的写法相同：

```python
if a > b:
    maxval = a
else:
    maxval = b
```

有时，你可能会看到变量赋值和条件结合在一起使用 `:=` 运算符。这被称为赋值表达式（或者更通俗地称为“海象运算符”，因为 `:=` 看起来像一只侧翻的海象——大概是在装死）。例如：

```python
x = 0
while (x := x + 1) < 10:    # 打印 1, 2, 3, ..., ..., 9
    print(x)
```

用于包围赋值表达式的括号是必须的。

`break` 语句可用于提前终止循环。它仅适用于最内层循环。例如：

```python
x = 0
while x < 10:
    if x == 5:
        break # 停止循环。移至下方的 Done
    print(x)
```

`continue` 语句跳过循环体的其余部分并返回到循环顶部。例如：

```python
x = 0
while x < 10:
    x += 1
    if x == 5:
        continue  # 跳过 print(x)。返回循环开始处。
    print(x)
print('Done')
```

## 1.6 文本字符串

要定义一个字符串字面量，将其包含在单引号、双引号或三引号中，如下所示：

```python
a = 'Hello World'
b = "Python is groovy"
c = '''Computer says no.'''
d = """Computer still says no."""
```

用于开始字符串的引号类型必须用于终止它。三引号字符串会捕获所有文本，直到终止的三引号为止——而单引号和双引号字符串必须指定在一条逻辑行内。当字符串字面量的内容跨越多行文本时，三引号字符串非常有用：

```python
print('''Content-type: text/html

<h1> Hello World </h1>

Click <a href="http://www.python.org">here</a>.

''')
```

紧邻的字符串字面量会被拼接成一个单一字符串。因此，上述示例也可以写成：

```python
print(
'Content-type: text/html\n'
'\n'
'<h1> Hello World </h1>\n'
'Click <a href="http://www.python.org">here</a>\n'
)
```

如果字符串的起始引号前有一个 `f`，则字符串内的转义表达式将被求值。例如，在之前的例子中，使用了以下语句来输出计算值：

```python
print(f'{year:>3d} {principal:0.2f}')
```

虽然这里只使用了简单的变量名，但任何有效的表达式都可以出现。例如：

```python
base_year = 2020
...
print(f'{(base_year + year):>4d} {principal:0.2f}')
```

作为 f-string 的替代方案，`format()` 方法和 `%` 运算符有时也用于格式化字符串。例如：

```python
print('{0:>3d} {1:0.2f}'.format(year, principal))
print('%3d %0.2f' % (year, principal))
```

关于字符串格式化的更多信息见第 9 章。

字符串被存储为由整数索引的 Unicode 字符序列，从零开始。负索引从字符串末尾开始索引。字符串 `s` 的长度使用 `len(s)` 计算。要提取单个字符，请使用索引运算符 `s[i]`，其中 `i` 是索引。

```python
a = 'Hello World'
print(len(a))                    # 11
b = a[4]                         # b = 'o'
c = a[-1]                        # c = 'd'
```

要提取子字符串，请使用切片运算符 `s[i:j]`。它提取 `s` 中所有索引 `k` 在范围 `i <= k < j` 内的字符。如果省略任一索引，则分别假设为字符串的开头或结尾：

```python
c = a[:5]                        # c = 'Hello'
d = a[6:]                        # d = 'World'
e = a[3:8]                       # e = 'lo Wo'
f = a[-5:]                       # f = 'World'
```

字符串具有多种用于操作其内容的方法。例如，`replace()` 方法执行简单的文本替换：

```python
g = a.replace('Hello', 'Hello Cruel')  # g = 'Hello Cruel World'
```

表 1.6 显示了一些常用的字符串方法。在此处和其他地方，包含在方括号中的参数是可选的。

### 表 1.6 常用字符串方法

| 方法 | 描述 |
|--------|------|
| `s.endswith(prefix [,start [,end]])` | 检查字符串是否以 `prefix` 结尾。 |
| `s.find(sub [,start [,end]])` | 查找指定子字符串 `sub` 第一次出现的位置，若未找到则返回 -1。 |
| `s.lower()` | 转换为小写。 |
| `s.replace(old, new [,maxreplace])` | 替换子字符串。 |
| `s.split([sep [,maxsplit]])` | 使用 `sep` 作为分隔符拆分字符串。`maxsplit` 是执行拆分的最大次数。 |
| `s.startswith(prefix [,start [,end]])` | 检查字符串是否以 `prefix` 开头。 |
| `s.strip([chrs])` | 移除开头和结尾的空白字符或 `chrs` 中指定的字符。 |
| `s.upper()` | 将字符串转换为大写。 |

字符串使用加号 (+) 运算符进行拼接：

```python
g = a + 'ly'    # g = 'Hello Worldly'
```

Python 永远不会将字符串的内容隐式地解释为数值数据。因此，+ 总是用于拼接字符串：

```python
x = '37'
y = '42'
z = x + y    # z = '3742' (字符串拼接)
```

要进行数学计算，必须首先使用 `int()` 或 `float()` 等函数将字符串转换为数值。例如：

```python
z = int(x) + int(y)    # z = 79 (整数加法)
```

非字符串值可以通过使用 `str()`、`repr()` 或 `format()` 函数转换为字符串表示形式。示例如下：

```python
s = 'The value of x is ' + str(x)
s = 'The value of x is ' + repr(x)
s = 'The value of x is ' + format(x, '4d')
```

虽然 `str()` 和 `repr()` 都能创建字符串，但它们的输出通常不同。`str()` 产生的是当你使用 `print()` 函数时得到的输出，而 `repr()` 创建的是你在程序中输入以准确表示对象值的字符串。例如：

```python
>>> s = 'hello\nworld'
>>> print(str(s))
hello
world
>>> print(repr(s))
'hello\nworld'
>>>
```

在调试时，请使用 `repr(s)` 来产生输出，因为它能向你展示关于值及其类型的更多信息。

`format()` 函数用于将单个值转换为应用了特定格式的字符串。例如：

```python
>>> x = 12.34567
>>> format(x, '0.2f')
'12.35'
>>>
```

传递给 `format()` 的格式代码与在生成格式化输出时使用 f-string 的代码相同。例如，上述代码可以用以下代码代替：

```python
>>> f'{x:0.2f}'
'12.35'
>>>
```

## 1.7 文件输入与输出

以下程序打开一个文件并将其内容逐行作为文本字符串读取：

```python
with open('data.txt') as file:
    for line in file:
        print(line, end='') # end='' 省略额外的换行符
```

`open()` 函数返回一个新的文件对象。其前面的 `with` 语句声明了一个语句块（或上下文），在该块中将使用该文件 (`file`)。一旦控制流离开该块，文件会自动关闭。如果你不使用 `with` 语句，代码需要写成这样：

```python
file = open('data.txt')
for line in file:
    print(line, end='') # end='' 省略额外的换行符
file.close()
```

人们很容易忘记调用 `close()` 这个额外步骤，因此最好使用 `with` 语句让系统为你关闭文件。

`for` 循环会对文件进行逐行迭代，直到没有更多数据可用。

如果你想将整个文件作为一个字符串读取，请像这样使用 `read()` 方法：

```python
with open('data.txt') as file:
    data = file.read()
```

如果你想分块读取大文件，请按如下方式向 `read()` 方法提供一个大小提示：

```python
with open('data.txt') as file:
    while (chunk := file.read(10000)):
        print(chunk, end='')
```

本例中使用的 `:=` 运算符（海象运算符）将值赋给变量并返回该值，以便 `while` 循环对其进行测试以决定是否跳出。当到达文件末尾时，`read()` 返回一个空字符串。

编写上述函数的另一种方式是使用 `break`：

```python
with open('data.txt') as file:
    while True:
        chunk = file.read(10000)
        if not chunk:
            break
        print(chunk, end='')
```

若要将程序的输出定向到文件，请向 `print()` 函数提供一个文件参数：

```python
with open('out.txt', 'wt') as out:
    while year <= numyears:
        principal = principal * (1 + rate)
        print(f'{year:>3d} {principal:0.2f}', file=out)
        year += 1
```

此外，文件对象支持 `write()` 方法，可用于写入字符串数据。例如，前一个例子中的 `print()` 函数也可以这样写：

```python
out.write(f'{year:3d} {principal:0.2f}\n')
```

默认情况下，文件包含以 UTF-8 编码的文本。如果你使用的是不同的文本编码，在打开文件时请使用额外的 `encoding` 参数。例如：

```python
with open('data.txt', encoding='latin-1') as file:
    data = file.read()
```

有时你可能想读取在控制台中交互式输入的数据。为此，请使用 `input()` 函数。例如：

```python
name = input('Enter your name : ')
print('Hello', name)
```

`input()` 函数返回所有输入的文本，直到遇到终止换行符为止（换行符本身不包含在内）。

## 1.8 列表

列表是任意对象的有序集合。通过将值括在方括号中来创建列表：

```python
names = [ 'Dave', 'Paula', 'Thomas', 'Lewis' ]
```

列表通过整数进行索引，从零开始。使用索引运算符来访问和修改列表中的单个项：

```python
a = names[2]                            # 返回列表的第三项，'Thomas'
names[2] = 'Tom'                        # 将第三项更改为 'Tom'
print(names[-1])                        # 打印最后一项 ('Lewis')
```

要将新项追加到列表末尾，请使用 `append()` 方法：

```python
names.append('Alex')
```

要在列表的特定位置插入一项，请使用 `insert()` 方法：

```python
names.insert(2, 'Aya')
```

要遍历列表中的项，请使用 `for` 循环：

```python
for name in names:
    print(name)
```

你可以使用切片运算符提取或重新赋值列表的一部分：

```python
b = names[0:2]          # b -> ['Dave', 'Paula']
c = names[2:]           # c -> ['Aya', 'Tom', 'Lewis', 'Alex']
names[1] = 'Becky'      # 将 'Paula' 替换为 'Becky'
names[0:2] = ['Dave', 'Mark', 'Jeff'] # 将前两项替换为 ['Dave','Mark','Jeff']
```

使用加号 (+) 运算符来拼接列表：

```python
a = ['x','y'] + ['z','z','y']  # 结果是 ['x','y','z','z','y']
```

可以通过两种方式创建空列表：

```python
names = []           # 空列表
names = list()       # 空列表
```

使用 `[]` 来表示空列表更符合惯用法。`list` 是与列表类型相关联的类名。它更常用于将数据转换为列表。例如：

```python
letters = list('Dave')    # letters = ['D', 'a', 'v', 'e']
```

大多数情况下，列表中的所有项都是相同类型的（例如，数字列表或字符串列表）。然而，列表可以包含任何 Python 对象的混合，包括其他列表，如下例所示：

```python
a = [1, 'Dave', 3.14, ['Mark', 7, 9, [100, 101]], 10]
```

嵌套列表中的项通过应用多次索引操作来访问：

```python
a[1]                    # 返回 'Dave'
a[3][2]                 # 返回 9
a[3][3][1]              # 返回 101
```

以下程序 `pcost.py` 说明了如何将数据读取到列表中并进行简单的计算。在本例中，假设各行包含以逗号分隔的值。该程序计算两列乘积之和。

```python
# pcost.py
#
# Reads input lines of the form 'NAME,SHARES,PRICE'.
# For example:
#
#    SYM,123,456.78
import sys
if len(sys.argv) != 2:
    raise SystemExit(f'Usage: {sys.argv[0]} filename')

rows = []
with open(sys.argv[1], 'rt') as file:
    for line in file:
        rows.append(line.split(','))

# rows is a list of this form
# [
#    ['SYM', '123', '456.78']
#    ...
# ]

total = sum([int(row[1]) * float(row[2]) for row in rows ])
```



```python
print(f'Total cost: {total:0.2f}')
```

该程序的第一行使用`import`语句从 Python 库中加载`sys`模块。该模块用于获取存储在`sys.argv`列表中的命令行参数。初步检查是为了确保已提供文件名。如果没有，则抛出一个带有提示错误信息的`SystemExit`异常。在该消息中，`sys.argv[0]`会插入当前正在运行的程序名称。

`open()`函数使用了在命令行中指定的文件名。`for line in file`循环逐行读取文件。每一行使用逗号字符作为分隔符被拆分成一个小列表。这个列表被追加到`rows`中。最终结果`rows`是一个列表的列表——请记住，列表可以包含任何内容，包括其他列表。

表达式`[ int(row[1]) * float(row[2]) for row in rows ]`通过遍历`rows`中的所有列表并计算第二项和第三项的乘积来构建一个新列表。这种构建列表的实用技术被称为列表推导式（list comprehension）。同样的计算可以用更冗长的形式表达如下：

```python
values = []

for row in rows:
    values.append(int(row[1]) * float(row[2]))

total = sum(values)
```

通常情况下，列表推导式是执行简单计算的首选技术。内置的`sum()`函数计算序列中所有项的总和。

## 1.9 元组（Tuples）

为了创建简单的数据结构，你可以将一组值打包到一个称为元组（tuple）的不可变对象中。你可以通过将一组值括在圆括号内来创建元组：

```python
holding = ('GOOG', 100, 490.10)

address = ('www.python.org', 80)
```

为了完整起见，也可以定义 0 元和 1 元元组，但它们有特殊的语法：

```python
a = ()         # 0-元组（空元组）

b = (item,)    # 1-元组（注意末尾的逗号）
```

元组中的值可以通过数值索引提取，就像列表一样。然而，更常见的做法是将元组解包（unpack）到一组变量中，如下所示：

```python
name, shares, price = holding

host, port = address
```

虽然元组支持与列表大部分相同的操作（如索引、切片和拼接），但元组的元素在创建后不能被更改——也就是说，你不能在现有元组中替换、删除或追加新元素。元组最好被视为一个由多个部分组成的单个不可变对象，而不是像列表那样的一组独立对象的集合。

元组和列表经常一起用于表示数据。例如，下面的程序展示了你如何读取一个包含由逗号分隔的数据列的文件：

```python
# File containing lines of the form "name,shares,price"

filename = 'portfolio.csv'

portfolio = []

with open(filename) as file:
    for line in file:
        row = line.split(',')

        name = row[0]
        shares = int(row[1])
        price = float(row[2])

        holding = (name, shares, price)
        portfolio.append(holding)
```

该程序创建的`portfolio`列表看起来像一个由行和列组成的二维数组。每一行由一个元组表示，可以通过以下方式访问：

```python
>>> portfolio[0]
('AA', 100, 32.2)

>>> portfolio[1]
('IBM', 50, 91.1)

>>>
```

单个数据项可以这样访问：

```python
>>> portfolio[1][1]
50

>>> portfolio[1][2]
91.1

>>>
```

以下是如何遍历所有记录并将字段解包到一组变量中：

```python
total = 0.0

for name, shares, price in portfolio:
    total += shares * price
```

或者，你可以使用列表推导式：

```python
total = sum([shares * price for _, shares, price in portfolio])
```

在迭代元组时，变量`_`可用于表示被丢弃的值。在上述计算中，它意味着我们忽略了第一个项（名称）。

## 1.10 集合（Sets）

集合是一个无序的、包含唯一对象的集合。集合用于查找不重复的值或管理与成员资格相关的问题。

要创建集合，请将一组值括在花括号中，或者将一个现有的项集合传递给`set()`。例如：

```python
names1 = {'IBM', 'MSFT', 'AA'}

names2 = set(['IBM', 'MSFT', 'HPE', 'IBM', 'CAT'])
```

集合的元素通常限制为不可变对象。例如，你可以创建数字、字符串或元组的集合。但是，你不能创建包含列表的集合。不过，大多数常见的对象可能都能在集合中使用——如果不确定，请尝试一下。

与列表和元组不同，集合是无序的，不能通过数字索引。此外，集合中的元素永远不会重复。例如，如果你检查前一段代码中`names2`的值，你会得到以下结果：

```python
>>> names2
{'CAT', 'IBM', 'MSFT', 'HPE'}

>>>
```

注意`'IBM'`只出现了一次。此外，项的顺序是不可预测的；输出结果可能与所示不同。甚至在同一台计算机上的不同解释器运行之间，顺序也可能会发生变化。

如果处理现有数据，你还可以使用集合推导式（set comprehension）来创建集合。例如，这条语句将前一节数据中的所有股票名称转换为一个集合：

```python
names = {s[0] for s in portfolio}
```

要创建空集合，请使用不带参数的`set()`：

```python
r = set()    # 初始空集合
```

集合支持一组标准的集合操作，包括并集、交集、差集和对称差集。这里有一个示例：

```python
a = t | s             # 并集 {'MSFT', 'CAT', 'HPE', 'AA', 'IBM'}

b = t & s             # 交集 {'IBM', 'MSFT'}

c = t - s             # 差集 {'CAT', 'HPE'}

d = s - t             # 差集 {'AA'}

e = t ^ s             # 对称差集 {'CAT', 'HPE', 'AA'}
```

差集操作`s - t`给出在`s`中但不在`t`中的项。对称差集`s ^ t`给出在`s`或`t`中但不同时在两者中出现的项。

可以使用`add()`或`update()`向集合中添加新项：

```python
t.add('DIS')                        # 添加单个项

s.update({'JJ', 'GE', 'ACME'})      # 向 s 添加多个项
```

可以使用`remove()`或`discard()`删除项：

```python
t.remove('IBM')         # 删除 'IBM'，如果不存在则抛出 KeyError。

s.discard('SCOX')       # 如果 'SCOX' 存在则将其删除。
```

`remove()`和`discard()`的区别在于，如果项不存在，`discard()`不会抛出异常。

## 1.11 字典（Dictionaries）

字典是键（key）和值（value）之间的映射。你可以通过将键值对（每对由冒号分隔）括在花括号（`{}`）中来创建字典，如下所示：

```python
s = {
    'name': 'GOOG',
    'shares': 100,
    'price': 490.10
}
```

要访问字典的成员，请使用如下的索引运算符：

```python
name = s['name']

cost = s['shares'] * s['price']
```

插入或修改对象的操作如下：

```python
s['shares'] = 75

s['date'] = '2007-06-07'
```

字典是一种定义由命名字段组成的对象的高效方式。此外，字典也常被用作映射，以便在无序数据中进行快速查找。例如，这是一个股票价格字典：

```python
prices = {
    'GOOG': 490.1,
    'AAPL': 123.5,
    'IBM': 91.5,
    'MSFT': 52.13
}
```

有了这样一个字典，你可以查找价格：

```python
p = prices['IBM']
```

使用`in`运算符测试字典的成员资格：

```python
if 'IBM' in prices:
    p = prices['IBM']
else:
    p = 0.0
```

这一特定的步骤序列也可以使用`get()`方法更简洁地完成：

```python
p = prices.get('IBM', 0.0)
```

使用`del`语句删除字典中的一个元素：

```python
del prices['GOOG']
```

虽然字符串是最常见的键类型，但你也可以使用许多其他 Python 对象，包括数字和元组。例如，元组经常被用来构建复合键或多部分键：

```python
prices = {}

prices['IBM', '2015-02-03'] = 91.23

prices['IBM', '2015-02-04'] = 91.42     # 省略了括号
```

任何类型的对象都可以放入字典中，包括其他字典。然而，可变数据结构（如列表、集合和字典）不能用作键。

字典经常被用作各种算法和数据处理问题的构建块。其中一个典型问题是制表（tabulation）。例如，以下是如何统计之前数据中每个股票名称的总持有股数：

```python
portfolio = [
    ('ACME', 50, 92.34),
    ('IBM', 75, 102.25),
    ('PHP', 40, 74.50),
    ('IBM', 50, 124.75)
]

total_shares = {s[0]: 0 for s in portfolio}

for name, shares, _ in portfolio:
    total_shares[name] += shares

# total_shares = {'IBM': 125, 'ACME': 50, 'PHP': 40}
```

在这个例子中，`{s[0]: 0 for s in portfolio}`是字典推导式的一个例子。它从另一个数据集合创建键值对字典。在这种情况下，它创建了一个将股票名称映射到 0 的初始字典。随后的`for`循环遍历该字典，并累加每个股票代码的所有持有股数。

许多像这样的常见数据处理任务已经由库模块实现。例如，`collections`模块有一个`Counter`对象可以用在此任务中：

```python
from collections import Counter

total_shares = Counter()

for name, shares, _ in portfolio:
    total_shares[name] += shares

# total_shares = Counter({'IBM': 125, 'ACME': 50, 'PHP': 40})
```

空字典可以通过两种方式之一创建：

```python
prices = {}          # 一个空字典

prices = dict()      # 一个空字典
```

对于空字典，使用`{}`更符合惯用法——但需要小心，因为它看起来像是在尝试创建一个空集合（请改用`set()`）。`dict()`通常用于从键值对创建字典。例如：

```python
pairs = [('IBM', 125), ('ACME', 50), ('PHP', 40)]

d = dict(pairs)
```

要获取字典键的列表，可以将字典转换为列表：

```python
syms = list(prices)     # syms = ['AAPL', 'MSFT', 'IBM', 'GOOG']
```

或者，你可以使用`dict.keys()`获取键：

```python
syms = prices.keys()
```

这两种方法之间的区别在于，`keys()`返回一个特殊的“键视图（keys view）”，该视图附加在字典上，并能实时反映对字典所做的更改。例如：

```python
>>> d = {'x': 2, 'y': 3}

>>> k = d.keys()

>>> k
dict_keys(['x', 'y'])

>>> d['z'] = 4

>>> k
dict_keys(['x', 'y', 'z'])
```

键总是按照项目最初插入字典的顺序出现。上述列表转换将保留此顺序。当字典被用于表示从文件和其他数据源读取的键值数据时，这一点非常有用。字典将保留输入顺序，这有助于提高可读性和调试。如果你想将数据写回文件，这也很方便。然而，在 Python 3.6 之前，这种顺序是不保证的，因此如果需要与旧版本 Python 兼容，你不能依赖它。如果发生了多次删除和插入操作，顺序同样不保证。

要获取存储在字典中的值，请使用`dict.values()`方法。要获取键值对，请使用`dict.items()`。例如，以下是如何将字典的全部内容作为键值对进行迭代：

```python
for sym, price in prices.items():
    print(f'{sym} = {price}')
```

## 1.12 迭代与循环

最广泛使用的循环结构是`for`语句，它遍历一个项目集合。一种常见的迭代形式是循环遍历序列的所有成员——例如字符串、列表或元组。这里有一个例子：

```python
for n in [1, 2, 3, 4, 5, 6, 7, 8, 9]:
    print(f'2 to the {n} power is {2**n}')
```

在这个例子中，变量`n`在每次迭代时将依次被赋值为列表`[1, 2, 3, 4, ..., 9]`中的项。由于遍历整数范围非常常见，因此有一个快捷方式：

```python
for n in range(1, 10):
    print(f'2 to the {n} power is {2**n}')
```

`range(i, j [,step])`函数创建一个对象，该对象表示一个整数范围，数值从`i`开始，直到（但不包括）`j`。如果省略起始值，则默认为零。还可以将可选的步长（stride）作为第三个参数给出。这里有一些例子：

```python
a = range(5)           # a = 0, 1, 2, 3, 4

b = range(1, 8)        # b = 1, 2, 3, 4, 5, 6, 7

c = range(0, 14, 3)    # c = 0, 3, 6, 9, 12

d = range(8, 1, -1)    # d = 8, 7, 6, 5, 4, 3, 2
```

`range()`创建的对象在请求查找时按需计算其表示的值。因此，即使在很大的数字范围中使用它也非常高效。

`for`语句并不局限于整数序列。它可以用于迭代许多种类的对象，包括字符串、列表、字典和文件。这里有一个例子：

```python
message = 'Hello World'

# 打印出 message 中的单个字符
for c in message:
    print(c)

names = ['Dave', 'Mark', 'Ann', 'Phil']

# 打印出列表的成员
for name in names:
    print(name)

prices = {'GOOG': 490.10, 'IBM': 91.50, 'AAPL': 123.15}

# 打印出字典的所有成员
for key in prices:
    print(key, '=', prices[key])

# 打印文件中的所有行
with open('foo.txt') as file:
    for line in file:
        print(line, end='')
```

`for`循环是 Python 最强大的语言特性之一，因为你可以创建自定义的迭代器对象和生成器函数来为其提供值序列。关于迭代器和生成器的更多细节可以在后面的第 6 章中找到。

## 1.13 函数

使用`def`语句定义一个函数：

```python
def remainder(a, b):
    q = a // b          # // 是截断除法。
    r = a - q * b
    return r
```



要调用函数，请使用其名称，后跟括号内的参数，例如`result = remainder(37, 15)`。

函数将文档字符串（documentation string）作为第一条语句是常见做法。该字符串为`help()`命令提供内容，并可被 IDE 和其他开发工具用于辅助程序员。例如：

```python
def remainder(a, b):
    '''
    计算 a 除以 b 的余数
    '''
    q = a // b
    r = a - q * b
    return r
```

如果函数的输入和输出从其名称中不明确，可以使用类型注解：

```python
def remainder(a: int, b: int) -> int:
    '''
    计算 a 除以 b 的余数
    '''
    q = a // b
    r = a - q * b
    return r
```

```python
r = a - q * b
return r
```

此类注解仅提供信息，在运行时并不会被强制执行。人们仍然可以用非整数值来调用上述函数，例如`result = remainder(37.5, 3.2)`。

使用元组（tuple）从函数中返回多个值：

```python
def divide(a, b):
    q = a // b           # 如果 a 和 b 是整数，则 q 是整数
    r = a - q * b
    return (q, r)
```

当在元组中返回多个值时，可以将它们像这样解包到单独的变量中：

```python
quotient, remainder = divide(1456, 33)
```

要为函数参数分配默认值，请使用赋值语句：

```python
def connect(hostname, port, timeout=300):
    # 函数体
    ...
```

当函数定义中给出了默认值时，在随后的函数调用中可以省略这些参数。被省略的参数将采用提供的默认值。示例如下：

```python
connect('www.python.org', 80)
connect('www.python.org', 80, 500)
```

默认参数通常用于可选功能。如果此类参数过多，可读性会降低。因此，建议使用关键字参数（keyword arguments）来指定此类参数。

例如：

```python
connect('www.python.org', 80, timeout=500)
```

如果你知道参数的名称，在调用函数时可以对所有参数进行命名。一旦命名，列出它们的顺序就不重要了。例如，这样做是可以的：

```python
connect(port=80, hostname='www.python.org')
```

当变量在函数内部创建或赋值时，其作用域是局部的。也就是说，该变量仅在函数体内部定义，并在函数返回时被销毁。函数也可以访问定义在函数外部的变量，只要它们定义在同一个文件中。例如：

```python
debug = True     # 全局变量

def read_data(filename):
    if debug:
        print('Reading', filename)
    ...
```

作用域规则在第 5 章中有更详细的描述。

## 1.14 异常

如果程序中发生错误，则会引发异常并出现追溯（traceback）消息：

```python
Traceback (most recent call last):
  File "readport.py", line 9, in <module>
    shares = int(row[1])
```

`ValueError: invalid literal for int() with base 10: 'N/A'`

追溯消息指出了发生错误的类型及其位置。通常，错误会导致程序终止。但是，你可以使用`try`和`except`语句来捕获并处理异常，如下所示：

```python
portfolio = []
with open('portfolio.csv') as file:
    for line in file:
        row = line.split(',')
        try:
            name = row[0]
            shares = int(row[1])
            price = float(row[2])
            holding = (name, shares, price)
            portfolio.append(holding)
    except ValueError as err:
        print('Bad row:', row)
        print('Reason:', err)
```

在这段代码中，如果发生了`ValueError`，有关错误原因的详细信息将放入`err`中，并且控制权将传递给`except`块中的代码。如果引发了其他类型的异常，程序将照常崩溃。如果没有发生错误，`except`块中的代码将被忽略。当异常被处理后，程序执行将从最后一个`except`块紧随其后的语句开始恢复。程序不会返回到异常发生的位置。

`raise`语句用于发出异常信号。你需要提供一个异常的名称。例如，以下是如何引发内置异常`RuntimeError`的方法：

```python
raise RuntimeError('Computer says no')
```

当结合异常处理时，对锁、文件和网络连接等系统资源的妥善管理通常比较棘手。有时无论发生什么都必须执行某些操作。为此，请使用`try-finally`。这里有一个关于必须释放锁以避免死锁的示例：

```python
import threading
lock = threading.Lock()
...
lock.acquire()
# 如果已经获取了锁，则必须释放它
try:
    ...
    statements
    ...
finally:
    lock.release()        # 总是运行
```

为了简化此类编程，大多数涉及资源管理的对象也支持`with`语句。以下是上述代码的修改版本：

```python
with lock:
    ...
    statements
    ...
```

在这个例子中，当`with`语句执行时，`lock`对象会被自动获取。当执行离开`with`块的上下文时，锁会被自动释放。无论`with`块内部发生了什么，这都会执行。例如，如果发生异常，当控制权离开块的上下文时，锁会被释放。

`with`语句通常仅与涉及系统资源或执行环境的对象兼容——例如文件、连接和锁。然而，用户定义的对象也可以有自己的自定义处理，详见第 3 章。

## 1.15 程序终止

当输入程序中不再有语句可执行，或者引发了未捕获的`SystemExit`异常时，程序终止。如果你想强制程序退出，可以这样做：

```python
raise SystemExit()                          # 无错误消息退出
raise SystemExit("Something is wrong")      # 带有错误消息退出
```

在退出时，解释器会尽最大努力对所有活动对象进行垃圾回收。但是，如果你需要执行特定的清理操作（删除文件、关闭连接），你可以使用`atexit`模块进行注册，如下所示：

```python
import atexit

# 示例
connection = open_connection("deaddot.com")

def cleanup():
    print "Going away..."
    close_connection(connection)

atexit.register(cleanup)
```

## 1.16 对象与类

程序中使用的所有值都是对象。一个对象由内部数据和执行涉及该数据的各种操作的方法组成。在处理字符串和列表等内置类型时，你已经使用了对象和方法。例如：

```python
items = [37, 42]      # 创建一个列表对象
items.append(73)       # 调用 append() 方法
```

`dir()`函数列出了对象上可用方法。在没有高级 IDE 可用时，它是进行交互式实验的有用工具。例如：

```python
>>> items = [37, 42]
>>> dir(items)
['__add__', '__class__', '__contains__', '__delattr__',
'__delitem__',
...
'append', 'count', 'extend', 'index', 'insert', 'pop',
'remove', 'reverse', 'sort']
>>>
```

在检查对象时，你会看到列出了熟悉的`append()`和`insert()`等方法。然而，你还会看到名称以双下划线开头和结尾的特殊方法。这些方法实现了各种运算符。例如，`__add__()`方法用于实现`+`运算符。这些方法在后面的章节中会有更详细的解释。

```python
>>> items.__add__([73, 101])
[37, 42, 73, 101]
>>>
```

`class`语句用于定义新类型的对象以及面向对象编程。例如，以下类定义了一个具有`push()`和`pop()`操作的栈：

```python
class Stack:
    def __init__(self):
        self._items = []                         # 初始化栈

    def push(self, item):
        self._items.append(item)

    def pop(self):
        return self._items.pop()

    def __repr__(self):
        return f'<{type(self).__name__} at 0x{id(self):x}, size={len(self)}>'

    def __len__(self):
        return len(self._items)
```

在类定义内部，使用`def`语句定义方法。每个方法中的第一个参数始终是指向对象本身。按照惯例，`self`是该参数的名称。所有涉及对象属性的操作必须显式引用`self`变量。前后带有双下划线的方法是特殊方法。例如，`__init__`用于初始化对象。在这种情况下，`__init__`创建一个内部列表用于存储栈数据。

要使用一个类，请编写如下代码：

```python
s = Stack()                         # 创建一个栈
s.push('Dave')                      # 向其中压入一些东西
s.push(42)
s.push([3, 4, 5])
x = s.pop()                         # x 获得 [3,4,5]
y = s.pop()                         # y 获得 42
```

在类中，你会注意到方法使用了一个内部变量`_items`。Python 没有提供任何隐藏或保护数据。然而，有一种编程约定，即以单个下划线开头的名称被视为“私有的”。在这个例子中，`_items`应该（由你）被视为内部实现，而不应在`Stack`类本身之外使用。请注意，这种约定并没有实际的强制执行——如果你想访问`_items`，你可以随时这样做。你只需要在同事审查你的代码时向他们交代即可。

`__repr__()`和`__len__()`方法的存在是为了让对象能与环境中的其他部分良好协作。这里，`__len__()`使`Stack`能够与内置的`len()`函数配合工作，而`__repr__()`则改变了`Stack`的显示和打印方式。始终定义`__repr__()`是个好主意，因为它可以简化调试过程。

```python
>>> s = Stack()
>>> s.push('Dave')
>>> s.push(42)
>>> len(s)
2
>>> s
<Stack at 0x10108c1d0, size=2>
>>>
```

对象的一个主要特性是，你可以通过继承来增加或重新定义现有类的功能。

假设你想添加一个方法来交换栈顶的两个项目。你可能会编写这样一个类：

```python
class MyStack(Stack):
    def swap(self):
        a = self.pop()
        b = self.pop()
        self.push(a)
        self.push(b)
```

`MyStack`与`Stack`完全相同，不同之处在于它有一个新方法`swap()`。

```python
>>> s = MyStack()
>>> s.push('Dave')
>>> s.push(42)
>>> s.swap()
>>> s.pop()
'Dave'
>>> s.pop()
42
>>>
```

继承也可以用来改变现有方法的行为。假设你想限制栈只能持有数字数据。编写一个如下类：

```python
class NumericStack(Stack):
    def push(self, item):
        if not isinstance(item, (int, float)):
            raise TypeError('Expected an int or float')
        super().push(item)
```

在这个例子中，`push()`方法被重新定义以增加额外的检查。`super()`操作是一种调用之前定义的`push()`的方式。这个类的工作方式如下：

```python
>>> s = NumericStack()
>>> s.push(42)
>>> s.push('Dave')
Traceback (most recent call last):
    ...
TypeError: Expected an int or float
>>>
```

通常，继承并不是最佳解决方案。假设你想定义一个简单的基于栈的四则运算计算器，运行方式如下：

```python
>>> # 计算 2 + 3 * 4
>>> calc = Calculator()
>>> calc.push(2)
>>> calc.push(3)
>>> calc.push(4)
>>> calc.mul()
>>> calc.add()
>>> calc.pop()
14
>>>
```

你可能会看到这段代码，看到`push()`和`pop()`的使用，并认为`Calculator`可以通过继承`Stack`来定义。虽然这样做可行，但将`Calculator`定义为一个完全独立的类可能会更好：

```python
class Calculator:
    def __init__(self):
        self._stack = Stack()

    def push(self, item):
        self._stack.push(item)

    def pop(self):
        return self._stack.pop()

    def add(self):
        self.push(self.pop() + self.pop())

    def mul(self):
        self.push(self.pop() * self.pop())

    def sub(self):
        right = self.pop()
        self.push(self.pop() - right)

    def div(self):
        right = self.pop()
        self.push(self.pop() / right)
```

在这种实现中，`Calculator`将`Stack`作为一个内部实现细节包含在内。这是一个*组合*（composition）的例子。`push()`和`pop()`方法将任务委派给内部的`Stack`。采用这种方法的主要原因是，你并不真正地将`Calculator`视为一个`Stack`。它是一个独立的概念——一种不同类型的对象。类比来说，你的手机包含一个中央处理器（CPU），但你通常不会认为你的手机是一种 CPU。

## 1.17 模块

随着程序的规模增长，你会希望将它们分解到多个文件中以便于维护。为此，请使用`import`语句。要创建一个模块，请将相关的语句和定义放入一个以`.py`为后缀且与模块同名的文件中。这里有一个例子：

```python
# readport.py
#
# 读取一个包含 'NAME,SHARES,PRICE' 数据的文件
def read_portfolio(filename):
    portfolio = []
    with open(filename) as file:
        for line in file:
            row = line.split(',')
            try:
```



`name = row[0]`

`shares = int(row[1])`

`price = float(row[2])`

`holding = (name, shares, price)`

`portfolio.append(holding)`

`except ValueError as err:`

`print('Bad row:', row)`

`print('Reason:', err)`

`return portfolio`

要在其他文件中使用你的模块，请使用 `import` 语句。例如，这里有一个模块 `pcost.py` 使用了上面的 `read_portfolio()` 函数：

```python
# pcost.py
import readport

def portfolio_cost(filename):
    '''
    计算投资组合的总额（持股数 * 价格）
    '''
    port = readport.read_portfolio(filename)
    return sum(shares * price for _, shares, price in port)
```

`import` 语句会创建一个新的命名空间（或环境），并在该命名空间内执行相关 `.py` 文件中的所有语句。导入后，要访问该命名空间的内容，请使用模块名称作为前缀，如前例中的 `readport.read_portfolio()`。

如果 `import` 语句因 `ImportError` 异常而失败，你需要检查环境中的几件事。首先，确保你创建了一个名为 `readport.py` 的文件。接着，检查 `sys.path` 中列出的目录。如果你的文件没有保存在这些目录之一中，Python 将无法找到它。

如果你想以不同的名称导入模块，可以在 `import` 语句中提供一个可选的 `as` 限定符：

```python
import readport as rp
port = rp.read_portfolio('portfolio.dat')
```

若要将特定定义导入当前命名空间，请使用 `from` 语句：

```python
from readport import read_portfolio
port = read_portfolio('portfolio.dat')
```

与对象一样，`dir()` 函数可以列出模块的内容。它是进行交互式实验的有用工具。

```python
>>> import readport
>>> dir(readport)
['__builtins__', '__cached__', '__doc__', '__file__',
 '__loader__',
 '__name__', '__package__', '__spec__', 'read_portfolio']
...
>>>
```

Python 提供了一个庞大的标准模块库，可以简化某些编程任务。例如，`csv` 模块是处理逗号分隔值文件的标准库。你可以在程序中这样使用它：

```python
# readport.py
#
# 读取一个包含 'NAME,SHARES,PRICE' 数据的文件
import csv

def read_portfolio(filename):
    portfolio = []
    with open(filename) as file:
        rows = csv.reader(file)
        for row in rows:
            try:
                name = row[0]
                shares = int(row[1])
                price = float(row[2])
                holding = (name, shares, price)
                portfolio.append(holding)
            except ValueError as err:
                print('Bad row:', row)
                print('Reason:', err)
    return portfolio
```

Python 还有大量的第三方模块可以安装，用以解决几乎任何可以想象的任务（包括读取 CSV 文件）。请参阅 https://pypi.org。

## 1.18 脚本编写

任何文件既可以作为脚本执行，也可以作为被 `import` 导入的库。为了更好地支持导入，脚本代码通常被包含在一个针对模块名称的条件检查中：

```python
# readport.py
#
# 读取一个包含 'NAME,SHARES,PRICE' 数据的文件
import csv

def read_portfolio(filename):
    ...

def main():
    portfolio = read_portfolio('portfolio.csv')
```

```python
for name, shares, price in portfolio:
    print(f'{name:>10s} {shares:10d} {price:10.2f}')
```

```python
if __name__ == '__main__':
    main()
```

`__name__` 是一个内置变量，始终包含封闭模块的名称。如果程序是以主脚本形式运行的（例如使用 `python readport.py` 命令），则 `__name__` 变量被设置为 `'__main__'`。否则，如果代码是通过 `import readport` 之类的语句导入的，则 `__name__` 变量被设置为 `'readport'`。

如上所示，该程序硬编码使用了文件名 `portfolio.csv`。相反，你可能希望提示用户输入文件名，或者将文件名作为命令行参数接收。为此，可以使用内置的 `input()` 函数或 `sys.argv` 列表。例如，以下是 `main()` 函数的修改版本：

```python
def main(argv):
    if len(argv) == 1:
        filename = input('Enter filename: ')
    elif len(argv) == 2:
        filename = argv[1]
    else:
        raise SystemExit(f'Usage: {argv[0]} [ filename ]')

    portfolio = read_portfolio(filename)
    for name, shares, price in portfolio:
        print(f'{name:>10s} {shares:10d} {price:10.2f}')
```

```python
if __name__ == '__main__':
    import sys
    main(sys.argv)
```

该程序可以通过命令行以两种不同的方式运行：

```bash
bash % python readport.py
Enter filename: portfolio.csv
...
bash % python readport.py portfolio.csv
...
bash % python readport.py a b c
Usage: readport.py [ filename ]
bash %
```

对于非常简单的程序，像这样处理 `sys.argv` 中的参数通常就足够了。对于更高级的用法，可以使用 `argparse` 标准库模块。

## 1.19 包 (Packages)

在大型程序中，将代码组织成包是很常见的。包是模块的分层集合。在文件系统中，将你的代码作为文件集合放置在如下目录中：

```
tutorial/
    __init__.py
    readport.py
    pcost.py
    stack.py
    ...
```

该目录应包含一个 `__init__.py` 文件，该文件可以是空的。完成此操作后，你就能够使用嵌套导入语句。例如：

```python
import tutorial.readport
port = tutorial.readport.read_portfolio('portfolio.dat')
```

如果你不喜欢这么长的名称，可以使用如下导入方式来简化：

```python
from tutorial.readport import read_portfolio
port = read_portfolio('portfolio.dat')
```

包中一个棘手的问题是同一包内文件之间的导入。在之前的示例中，展示了一个 `pcost.py` 模块，它以如下导入语句开头：

```python
# pcost.py
import readport
...
```

如果 `pcost.py` 和 `readport.py` 文件被移动到一个包中，这个导入语句就会失效。为了修复它，你必须使用全限定模块导入：

```python
# pcost.py
from tutorial import readport
...
```

或者，你可以使用如下的包相对导入：

```python
# pcost.py
from . import readport
...
```

后一种形式的优点是不硬编码包名。这使得以后重命名包或在项目中移动包更加容易。

关于包的其他细微细节将在稍后讨论（见第 8 章）。

## 1.20 应用程序的结构化

当你开始编写更多 Python 代码时，可能会发现自己在开发包含自定义代码和第三方依赖项的大型应用程序。管理所有这些内容是一个复杂且不断演进的话题。关于什么是“最佳实践”，也存在许多相互矛盾的观点。然而，有几个基本方面是你应该了解的。

首先，将大型代码库组织成包（即包含特殊 `__init__.py` 文件的 `.py` 文件目录）是标准做法。这样做时，请为顶层目录选择一个唯一的包名。包目录的主要目的是管理编程时使用的 `import` 语句和模块的命名空间。你希望你的代码与其他人的代码隔离。

除了主项目源代码之外，你可能还会有测试、示例、脚本和文档。这些附加材料通常存放在与包含源代码的包不同的目录集中。因此，通常会为项目创建一个封闭的顶层目录，并将所有工作放在该目录下。例如，一个相当典型的项目组织结构可能如下所示：

```
tutorial-project/
    tutorial/
        __init__.py
        readport.py
        pcost.py
        stack.py
        ...
    tests/
        test_stack.py
        test_pcost.py
        ...
    examples/
        sample.py
        ...
    doc/
        tutorial.txt
        ...
```

请记住，实现方式不止一种。你所解决的问题性质可能会决定不同的结构。尽管如此，只要你的主源代码文件位于一个正确的包中（同样是指包含 `__init__.py` 文件的目录），就没问题。

## 1.21 管理第三方包

Python 拥有一个庞大的贡献包库，可以在 Python 包索引 (https://pypi.org) 中找到。在自己的代码中，你可能需要依赖其中一些包。要安装第三方包，请使用类似 pip 的命令：

```bash
bash % python3 -m pip install somepackage
```

安装的包被放置在一个特殊的 `site-packages` 目录中，如果你检查 `sys.path` 的值就可以找到它。例如，在 UNIX 机器上，包可能会被放置在 `/usr/local/lib/python3.8/site-packages`。如果你想知道某个包是从哪里来的，可以在解释器中导入该包后检查其 `__file__` 属性：

```python
>>> import pandas
>>> pandas.__file__
'/usr/local/lib/python3.8/site-packages/pandas/__init__.py'
>>>
```

安装包的一个潜在问题是，你可能没有权限更改本地安装的 Python 版本。即使你有权限，这可能仍然不是一个好主意。例如，许多系统已经安装了 Python 以供各种系统工具使用。修改该版本的 Python 安装通常是个坏主意。

为了创建一个你可以安装包并工作而无需担心破坏任何内容的沙箱，可以通过如下命令创建虚拟*环境*：

```bash
bash % python3 -m venv myproject
```

这将在名为 `myproject/` 的目录中为你设置一个专用的 Python 安装。在该目录中，你会找到一个解释器可执行文件和库，你可以在其中安全地安装包。例如，如果你运行 `myproject/bin/python3`，你将获得一个为你个人使用而配置的解释器。你可以向这个解释器安装包，而无需担心破坏默认 Python 安装的任何部分。要安装包，像之前一样使用 `pip`，但请确保指定正确的解释器：

```bash
bash % ./myproject/bin/python3 -m pip install somepackage
```

有各种工具旨在简化 `pip` 和 `venv` 的使用。这些事务也可能由你的 IDE 自动处理。由于这是 Python 中一个流动且不断演进的部分，此处不再给出进一步的建议。

## 1.22 Python：契合你的思维

在 Python 的早期阶段，“契合你的思维 (it fits your brain)” 是一个常见的座右铭。即便在今天，Python 的核心仍然是一门小巧的编程语言，以及一组有用的内置对象——列表、集合和字典。绝大多数实际问题都可以仅使用本章介绍的基本功能来解决。当你开始你的 Python 冒险时，请记住这一点——虽然解决问题总有更复杂的方法，但可能也存在一种使用基础功能来实现的简单方法。

Python 已经提供的功能。当你犹豫不决时，你可能会感谢过去那个坚持这样做的自己。

# 2. 运算符、表达式与数据操纵

本章介绍 Python 的表达式、运算符以及与数据操纵相关的求值规则。表达式是执行有用计算的核心。此外，第三方库可以通过自定义 Python 的行为来提供更好的用户体验。本章将在高层级上描述表达式。第 3 章将描述可用于自定义解释器行为的底层协议。

## 2.1 字面量

字面量是指直接在程序中输入的数值，例如 `42`、`4.2` 或 `'forty-two'`。

整数字面量表示任意大小的有符号整数值。可以使用二进制、八进制或十六进制来指定整数：

```python
42
0b101010  # 二进制整数
0o52      # 八进制整数
0x2a      # 十六进制整数
```

进制基数不作为整数值的一部分存储。如果打印，上述所有字面量都将显示为 `42`。你可以使用内置函数 `bin(x)`、`oct(x)` 或 `hex(x)` 将整数转换为表示其在不同基数下值的字符串。

浮点数可以通过添加小数点或使用科学计数法（用 `e` 或 `E` 指定指数）来编写。以下全部都是浮点数：

```python
4.2
42.
.42
4.2e+2
4.2E2
-4.2e-2
```

在内部，浮点数被存储为 IEEE 754 双精度（64 位）值。

在数值字面量中，单个下划线（`_`）可用作数字之间的视觉分隔符。例如：

```python
123_456_789
0x1234_5678
0b111_00_101
123.789_012
```

数字分隔符不作为数字的一部分存储——它仅用于在源代码中使较大的数值字面量更易读。

布尔字面量写作 `True` 和 `False`。

字符串字面量通过用单引号、双引号或三引号将字符包围来编写。单引号和双引号字符串必须出现在同一行。三引号字符串可以跨越多行。例如：

```python
'hello world'
"hello world"
'''hello world'''
"""hello world"""
```

元组、列表、集合和字典字面量编写如下：

```python
(1, 2, 3)               # tuple (元组)
[1, 2, 3]               # list (列表)
{1, 2, 3}               # set (集合)
{'x':1, 'y':2, 'z': 3}  # dict (字典)
```

## 2.2 表达式与位置

表达式代表一个计算过程，其结果为一个具体的值。它由字面量、名称、运算符以及函数或方法调用组合而成。表达式总是可以出现在赋值语句的右侧，可用作其他表达式中操作的运算数，或者作为函数参数传递。例如：

```python
value = 2 + 3 * 5 + sqrt(6+7)
```

运算符（如 `+` 加法或 `*` 乘法）代表对作为运算数提供的对象执行的操作。`sqrt()` 是一个应用于输入参数的函数。

赋值语句的左侧代表存储对象引用的位置。如前例所示，该位置可能是一个简单的标识符（如 `value`），也可以是一个对象的属性或容器中的索引。例如：

```python
a = 4 + 2
b[1] = 4 + 2
```



```python
c['key'] = 4 + 2
```

```python
d.value = 4 + 2
```

从某个位置读回数值同样是一个表达式。例如：

```python
value = a + b[1] + c['key']
```

值的赋值与表达式的求值是两个不同的概念。特别是，你不能将赋值运算符作为表达式的一部分：

```python
while line=file.readline():
    print(line)  # 语法错误 (Syntax Error)
```

然而，可以使用“赋值表达式”运算符（`:=`）来执行这种求值与赋值的组合操作。例如：

```python
while (line:=file.readline()):
    print(line)
```

`:=` 运算符通常与 `if` 和 `while` 等语句结合使用。事实上，除非用括号将其包围，否则将其作为普通赋值运算符使用会导致语法错误。

## 2.3 标准运算符

Python 对象可以与表 2.1 中的任何运算符协同工作。

**表 2.1 标准运算符**

| 操作 | 描述 |
|:---|:---|
| `x + y` | 加法 |
| `x - y` | 减法 |
| `x * y` | 乘法 |
| `x / y` | 除法 |
| `x // y` | 整除（截断除法） |
| `x @ y` | 矩阵乘法 |
| `x ** y` | 幂（x 的 y 次方） |
| `x % y` | 取模 (x mod y)。余数。 |
| `x << y` | 左移 |
| `x >> y` | 右移 |
| `x & y` | 按位与 |
| `x \| y` | 按位或 |
| `x ^ y` | 按位异或 |
| `~x` | 按位取反 |
| `-x` | 一元负号 |
| `+x` | 一元正号 |
| `abs(x)` | 绝对值 |
| `divmod(x,y)` | 返回 (x // y, x % y) |
| `pow(x,y [,modulo])` | 返回 (x ** y) % modulo |
| `round(x,[n])` | 四舍五入到最近的 10-n 倍数 |

通常这些运算符具有数值含义。但也有一些显著的特例。例如，`+` 运算符也用于连接序列，`*` 运算符用于复制序列，`-` 用于集合差集，而 `%` 执行字符串格式化：

```python
[1,2,3] + [4,5]     # [1,2,3,4,5]

[1,2,3] * 4         # [1,2,3,1,2,3,1,2,3,1,2,3]

'%s has %d messages' % ('Dave', 37)
```

运算符的检查是一个动态过程。涉及混合数据类型的操作，如果在直觉上可行，通常也能“正常工作”。例如，你可以将整数和分数相加：

```python
>>> from fractions import Fraction

>>> a = Fraction(2, 3)

>>> b = 5

>>> a + b

Fraction(17, 3)
```

然而，这并非总是万无一失。例如，它不适用于 `decimal` 类型。

```python
>>> from decimal import Decimal

>>> from fractions import Fraction

>>> a = Fraction(2, 3)

>>> b = Decimal('5')

>>> a + b

Traceback (most recent call last):

  File "<stdin>", line 1, in <module>

TypeError: unsupported operand type(s) for +: 'Fraction' and 'decimal.Decimal'
```

不过，对于大多数数字组合，Python 遵循一套标准的数值层级：布尔值 → 整数 → 分数 → 浮点数 → 复数。混合类型操作将直接生效——你无需为此担心。

## 2.4 原地赋值

Python 提供了表 2.2 中的“原地”（in-place）或“增强”（augmented）赋值操作。

**表 2.2 增强赋值运算符**

| 操作 | 描述 |
|:---|:---|
| `x += y` | `x = x + y` |
| `x -= y` | `x = x - y` |
| `x *= y` | `x = x * y` |
| `x /= y` | `x = x / y` |
| `x //= y` | `x = x // y` |
| `x **= y` | `x = x ** y` |
| `x %= y` | `x = x % y` |
| `x @= y` | `x = x @ y` |
| `x &= y` | `x = x & y` |
| `x \|= y` | `x = x \| y` |
| `x ^= y` | `x = x ^ y` |
| `x >>= y` | `x = x >> y` |
| `x <<= y` | `x = x << y` |

这些不被认为是表达式。相反，它们是用于原地更新值的语法便捷写法。例如：

```python
a = 3

a = a + 1

a += 1
```

可变对象可以使用这些运算符来执行数据的原地修改以进行优化。考虑这个例子：

```python
>>> a = [1, 2, 3]

>>> b = a              # 创建一个指向 a 的新引用

>>> a += [4, 5]        # 原地更新（不创建新列表）

>>> a

[1, 2, 3, 4, 5]

>>> b

[1, 2, 3, 4, 5]
```

在这个例子中，`a` 和 `b` 引用同一个列表。当执行 `a += [4, 5]` 时，它原地更新了列表对象而没有创建新列表。因此，`b` 也能看到这个更新。这通常会让人感到惊讶。

## 2.5 对象比较

相等运算符（`x == y`）测试 `x` 和 `y` 的值是否相等。对于列表和元组，它们必须大小相等、元素相等且顺序相同。对于字典，只有当 `x` 和 `y` 具有相同的键集，且所有具有相同键的对象具有相等的值时，才返回 `True`。如果两个集合具有相同的元素，则它们相等。

在不兼容类型的对象之间进行相等比较，例如文件

在实践中，使用 `is` 运算符比较对象几乎从来都不是你想要的结果。除非你有充分的理由预期两个对象具有相同的标识，否则请使用 `==` 运算符进行所有比较。

## 2.6 有序比较运算符

表 2.3 中的有序比较运算符对数字具有标准的数学解释。它们返回一个布尔值。

**表 2.3 有序比较运算符**

| 操作 | 描述 |
|:---|:---|
| `x < y` | 小于 |
| `x > y` | 大于 |
| `x >= y` | 大于或等于 |
| `x <= y` | 小于或等于 |

对于集合，`x < y` 测试 `x` 是否为 `y` 的真子集（即元素更少，且不等于 `y`）。

在比较两个序列时，会首先比较每个序列的第一个元素。如果它们不同，则由此决定结果。如果它们相同，则比较移动到每个序列的第二个元素。这个过程一直持续到找到两个不同的元素，或者其中一个序列中不再有元素为止。如果两个序列都到达末尾，则认为这两个序列相等。如果 `a` 是 `b` 的子序列，那么 `a < b`。

字符串和字节使用字典序进行比较。每个字符被分配一个由字符集（如 ASCII 或 Unicode）决定的唯一数值索引。如果一个字符的索引较小，则该字符小于另一个字符。

并非所有类型都支持有序比较。例如，尝试在字典上使用 `<` 是未定义的，会导致 `TypeError`。同样，将有序比较应用于不兼容的类型（例如字符串和数字）也会导致 `TypeError`。

## 2.7 布尔表达式与真值

`and`、`or` 和 `not` 运算符可以构建复杂的布尔表达式。这些运算符的行为如表 2.4 所示。

### 表 2.4 逻辑运算符

| 运算符 | 描述 |
|:---|:---|
| `x or y` | 如果 `x` 为假，返回 `y`；否则，返回 `x`。 |
| `x and y` | 如果 `x` 为假，返回 `x`；否则，返回 `y`。 |
| `not x` | 如果 `x` 为假，返回 `True`；否则，返回 `False`。 |

当你使用表达式来确定真假值时，`True`、任何非零数字、非空字符串、列表、元组或字典都被视为真。`False`、零、`None` 以及空列表、元组和字典的求值为假。

布尔表达式从左到右求值，并且仅在需要确定最终值时才消耗右操作数。例如，`a and b` 仅在 `a` 为真时才对 `b` 求值。这被称为短路求值。它在简化涉及测试及后续操作的代码时非常有用。例如：

```python
if y != 0:
    result = x / y
else:
    result = 0

# 替代方案

result = y and x / y
```

在第二个版本中，只有在 `y` 为非零时才会执行 `x / y` 除法。

依赖于对象的隐式“真值性”可能会导致难以发现的 Bug。例如，考虑这个函数：

```python
def f(x, items=None):
    if not items:
        items = []

    items.append(x)
    return items
```

这个函数有一个可选参数，如果不提供该参数，则会创建一个新列表并返回。例如：

```python
>>> foo(4)

[4]
```

然而，如果你向它传递一个现有的空列表作为参数，该函数会有非常奇怪的行为：

```python
>>> a = []

>>> foo(3, a)

[3]

>>> a                    # 注意 a 并没有被更新

[]
```

这是一个真值检查 Bug。空列表的求值为 `False`，因此代码创建了一个新列表，而不是使用作为参数传递进来的那个列表（`a`）。要修复此问题，你需要更精确地检查是否为 `None`：

```python
def f(x, items=None):
    if items is None:
        items = []

    items.append(x)
    return items
```

在编写条件检查时，保持精确始终是一个良好的实践。

## 2.8 条件表达式

一种常见的编程模式是根据表达式的结果有条件地赋值。例如：

```python
if a <= b:
    minvalue = a
else:
    minvalue = b
```

这段代码可以使用条件表达式来简化。例如：

```python
minvalue = a if a <= b else b
```

在这样的表达式中，首先对中间的条件进行求值。如果结果为 `True`，则对 `if` 左侧的表达式求值。否则，对 `else` 之后的表达式求值。`else` 子句是必须的。

## 2.9 涉及可迭代对象的操作

迭代是 Python 的一个重要特性，由所有 Python 容器（列表、元组、字典等）、文件以及生成器函数支持。表 2.5 中的操作可以应用于任何可迭代对象 `s`。

**表 2.5 可迭代对象上的操作**

| 操作 | 描述 |
|:---|:---|
| `for vars in s:` | 迭代 |
| `v1, v2, ... = s` | 变量解包 |
| `x in s, x not in s` | 成员资格判断 |
| `[a, *s, b], (a, *s, b), {a, *s, b}` | 在列表、元组或集合字面量中扩展 |

可迭代对象最核心的操作是 `for` 循环。这就是你逐个迭代值的方式。所有其他操作都基于此构建。

`x in s` 运算符测试对象 `x` 是否作为可迭代对象 `s` 产生的一个项出现，并返回 `True` 或 `False`。`x not in s` 运算符与 `not (x in s)` 相同。对于字符串，`in` 和 `not in` 运算符接受子字符串。例如，`'hello' in 'hello world'` 产生 `True`。请注意，`in` 运算符不支持通配符或任何形式的模式匹配。

任何支持迭代的对象都可以将其值解包到一系列位置中。例如：

```python
items = [3, 4, 5]

x, y, z = items                 # x = 3, y = 4, z = 5

letters = "abc"

x, y, z = letters               # x = 'a', y = 'b', z = 'c'
```

左侧的位置不一定是简单的变量名。任何可以出现在等号左侧的有效位置都是可以接受的。因此，你可以编写如下代码：

```python
items = [3, 4, 5]

d = {}

d['x'], d['y'], d['z'] = items
```

在将值解包到位置时，左侧位置的数量必须与右侧可迭代对象中的项数完全匹配。对于嵌套数据结构，请遵循相同的结构模式来匹配位置和数据。考虑这个解包两个嵌套 3-元组的示例：

```python
datetime = ((5, 19, 2008), (10, 30, "am"))

(month, day, year), (hour, minute, am_pm) = datetime
```

有时，在解包时使用 `_` 变量来表示丢弃的值。例如，如果你只关心日期和小时，可以使用：

```python
(_, day, _), (hour, _, _) = datetime
```

如果不知道要解包的项数，可以使用扩展形式的解包，通过包含一个星号变量，如下例中的 `*extra`：

```python
items = [1, 2, 3, 4, 5]

a, b, *extra = items      # a = 1, b = 2, extra = [3,4,5]

*extra, a, b               # extra = [1,2,3], a = 4, b = 5

a, *extra, b               # a = 1, extra = [2,3,4], b = 5
```

在这个例子中，`*extra` 接收所有额外的项。它始终是一个列表。在解包单个可迭代对象时，不能使用超过一个星号变量。然而，在解包涉及不同可迭代对象的更复杂数据结构时，可以使用多个星号变量。例如：

```python
datetime = ((5, 19, 2008), (10, 30, "am"))

(month, *_), (hour, *_)) = datetime
```

在编写列表、元组和集合字面量时，任何可迭代对象都可以被扩展。这同样是通过星号（`*`）完成的。例如：

```python
items = [1, 2, 3]

a = [10, *items, 11]       # a = [10, 1, 2, 3, 11] (list)

b = (*items, 10, *items)   # b = (1, 2, 3, 10, 1, 2, 3) (tuple)

c = {10, 11, *items}       # c = {1, 2, 3, 10, 11} (set)
```

在这个例子中，`items` 的内容被简单地粘贴到正在创建的列表、元组或集合中，就像你在该位置直接输入一样。这种扩展被称为 “splatting”。在定义字面量时，你可以包含任意数量的 `*` 扩展。但是，许多可迭代对象（如文件或生成器）仅支持一次性迭代。如果你使用 `*` 扩展，内容将被消耗，该可迭代对象在随后的迭代中将不再产生任何值。

多种内置函数接受任何可迭代对象作为输入。表 2.6 显示了其中一些操作。

### 表 2.6 消耗可迭代对象的函数

| 函数 | 描述 |
|:---|:---|
| `list(s)` | 从 `s` 创建一个列表 |
| `tuple(s)` | 从 `s` 创建一个元组 |
| `set(s)` | 从 `s` 创建一个集合 |
| `min(s [,key])` | `s` 中的最小项 |
| `max(s [,key])` | `s` 中的最大项 |
| `any(s)` | 如果 `s` 中有任何一项为真，则返回 `True` |
| `all(s)` | 如果 `s` 中所有项都为真，则返回 `True` |
| `sum(s [, initial])` | 项之和，带有一个可选的初始值 |
| `sorted(s [, key])` | 创建一个排序后的列表 |

这也适用于许多其他库函数——例如 `statistics` 模块中的函数。

## 2.10 序列操作

序列是一个可迭代的容器，它具有大小，并允许通过从 0 开始的整数索引来访问项目。示例包括字符串、列表和元组。除了所有涉及迭代的操作外，表 2.7 中的运算符也可以应用于序列。

**表 2.7 序列操作**

| 操作 | 描述 |
|:---|:---|
| `s + r` | 连接 |
| `s * n, n * s` | 创建 `n` 个 `s` 的副本，其中 `n` 是一个整数 |
| `s[i]` | 索引 |
| `s[i:j]` | 切片 |
| `s[i:j:stride]` | 扩展切片 |
| `len(s)` | 长度 |

`+` 运算符连接两个相同类型的序列。例如：

```python
>>> a = [3, 4, 5]

>>> b = [6, 7]

>>> a + b

[3, 4, 5, 6, 7]

>>>
```

`s * n` 运算符创建序列的 `n` 个副本。然而，这些是浅拷贝，仅通过引用复制元素。考虑以下代码：

```python
>>> a = [3, 4, 5]

>>> b = [a]

>>> c = 4 * b

>>> c

[[3, 4, 5], [3, 4, 5], [3, 4, 5], [3, 4, 5]]

>>> a[0] = -7

>>> c
```



`[[-7, 4, 5], [-7, 4, 5], [-7, 4, 5], [-7, 4, 5]]`

>>>

请注意，对 `a` 的更改如何修改了列表 `c` 的每个元素。在这种情况下，对列表 `a` 的引用被放入了列表 `b` 中。当 `b` 被复制时，创建了四个额外的对 `a` 的引用。最后，当 `a` 被修改时，此更改传播到了 `a` 的所有其他副本中。序列乘法的这种行为通常不是程序员的意图。解决这个问题的一种方法是通过复制 `a` 的内容来手动构建复制的序列。这里有一个示例：

```python
a = [ 3, 4, 5 ]
c = [list(a) for _ in range(4)]  # list() 创建 a 的副本
```

索引运算符 `s[n]` 返回序列中的第 `n` 个对象；`s[0]` 是第一个对象。负索引可用于从序列末尾获取字符。例如，`s[-1]` 返回最后一项。否则，尝试访问超出范围的元素会导致 `IndexError` 异常。

切片运算符 `s[i:j]` 从 `s` 中提取一个由索引为 `k` 的元素组成的子序列，其中 `i <= k < j`。`i` 和 `j` 必须都是整数。如果省略起始或结束索引，则分别假设为序列的开始或结束。允许使用负索引，并假设它们相对于序列末尾。

切片运算符可以给一个可选的步长 `s[i:j:stride]`，使切片跳过某些元素。不过，其行为稍微复杂一些。如果提供了步长，`i` 是起始索引，`j` 是结束索引，产生的子序列是元素 `s[i]`、`s[i+stride]`、`s[i+2*stride]` 等，直到达到索引 `j`（不包括 `j`）。`stride` 也可以是负数。如果省略起始索引 `i`，则在 `stride` 为正时设置为序列开始，在 `stride` 为负时设置为序列末尾。如果省略结束索引 `j`，则在 `stride` 为正时设置为序列末尾，在 `stride` 为负时设置为序列开始。这里有一些示例：

```python
a = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
a[2:5]       # [2, 3, 4]
a[:3]        # [0, 1, 2]
a[-3:]       # [7, 8, 9]
a[::2]       # [0, 2, 4, 6, 8 ]
a[::-2]      # [9, 7, 5, 3, 1 ]
a[0:5:2]     # [0, 2, 4]
a[5:0:-2]    # [5, 3, 1]
a[:5:1]      # [0, 1, 2, 3, 4]
a[:5:-1]     # [9, 8, 7, 6, 5]
a[5::1]      # [5, 6, 7, 8, 9]
a[5::-1]     # [5, 4, 3, 2, 1, 0]
a[5:0:-1]    # [5, 4, 3, 2, 1]
```

花哨的切片可能会导致以后难以理解的代码。因此，可能需要一定的判断。切片可以使用 `slice()` 命名。例如：

```python
firstfive = slice(0, 5)
s = 'hello world'
print(s[firstfive])      # 打印 'hello'
```

## 2.11 可变序列操作

字符串和元组是不可变的，创建后不能修改。列表或其他可变序列的内容可以使用表 2.8 中的运算符进行就地修改。

**表 2.8** 可变序列操作

| 操作 | 描述 |
|-----------|-------------|
| `s[i] = x` | 索引赋值 |
| `s[i:j] = r` | 切片赋值 |
| `s[i:j:stride] = r` | 扩展切片赋值 |
| `del s[i]` | 删除一个元素 |
| `del s[i:j]` | 删除一个切片 |
| `del s[i:j:stride]` | 删除一个扩展切片 |

`s[i] = x` 运算符将序列的元素 `i` 更改为引用对象 `x`，从而增加 `x` 的引用计数。负索引相对于列表末尾，尝试为超出范围的索引赋值会导致 `IndexError` 异常。切片赋值运算符 `s[i:j] = r` 将元素 `k`（其中 `i <= k < j`）替换为序列 `r` 中的元素。索引的含义与切片相同。如有必要，序列 `s` 的大小可能会扩大或缩小，以容纳 `r` 中的所有元素。这里有一个示例：

```python
a = [1, 2, 3, 4, 5]
a[1] = 6
# a = [1, 6, 3, 4, 5]
a[2:4] = [10, 11]
# a = [1, 6, 10, 11, 5]
a[3:4] = [-1, -2, -3]
# a = [1, 6, 10, -1, -2, -3, 5]
a[2:] = [0]
# a = [1, 6, 0]
```

切片赋值可以提供一个可选的步长参数。然而，此时行为会受到更多限制，即右侧的参数必须具有与被替换切片完全相同的元素数量。这里有一个示例：

```python
a = [1, 2, 3, 4, 5]
a[1::2] = [10, 11]        # a = [1, 10, 3, 11, 5]
a[1::2] = [30, 40, 50]   # ValueError. 左侧切片中只有两个元素
```

`del s[i]` 运算符从序列中移除元素 `i` 并递减其引用计数。`del s[i:j]` 移除切片中的所有元素。也可以提供步长，如 `del s[i:j:stride]`。

这里描述的语义适用于内置的列表类型。涉及序列切片的操作在第三方包中是一个丰富的自定义领域。您可能会发现，非列表对象上的切片在重新赋值、删除和对象共享方面具有不同的规则。例如，流行的 `numpy` 包具有与 Python 列表不同的切片语义。

## 2.12 集合操作

集合是一个由唯一值组成且无序的集合。表 2.9 中的操作可以对集合执行。

**表 2.9** 集合操作

| 操作 | 描述 |
|-----------|-------------|
| `s \| t` | `s` 和 `t` 的并集 |
| `s & t` | `s` 和 `t` 的交集 |
| `s - t` | 集合差集（在 `s` 中但不在 `t` 中的项） |
| `s ^ t` | 对称差集（不在 `s` 和 `t` 两者中同时存在的项） |
| `len(s)` | 集合中项目的数量 |
| `item in s, item not in s` | 成员测试 |
| `s.add(item)` | 向集合 `s` 添加一项 |
| `s.remove(item)` | 如果 `s` 中存在该项则移除（否则报错） |
| `s.discard(item)` | 如果 `s` 中存在该项则丢弃 |

这里有一些示例：

```python
>>> a = {'a', 'b', 'c'}
>>> b = {'c', 'd'}
>>> a | b
{'a', 'b', 'c', 'd'}
>>> a & b
{'c'}
>>> a - b
{'a', 'b'}
>>> b - a
{'d'}
>>> a ^ b
{'a', 'b', 'd'}
>>>
```

集合操作同样适用于字典的键视图（key-view）和项视图（item-view）对象。例如，要找出两个字典共同拥有的键，可以这样做：

```python
>>> a = { 'x': 1, 'y': 2, 'z': 3 }
>>> b = { 'z': 3, 'w': 4, 'q': 5 }
>>> a.keys() & b.keys()
{ 'z' }
>>>
```

## 2.13 映射操作

映射是键与值之间的关联。内置的 `dict` 类型就是一个例子。表 2.10 中的操作可应用于映射。

**表 2.10** 映射操作

| 操作 | 描述 |
|-----------|-------------|
| `x = m[k]` | 通过键索引 |
| `m[k] = x` | 通过键赋值 |
| `del m[k]` | 通过键删除一项 |
| `k in m` | 成员测试 |
| `len(m)` | 映射中项目的数量 |
| `m.keys()` | 返回键 |
| `m.values()` | 返回值 |
| `m.items()` | 返回 (键, 值) 对 |

键值可以是任何不可变对象，例如字符串、数字和元组。当使用元组作为键时，可以省略括号，像这样编写以逗号分隔的值：

```python
d = { }
d[1,2,3] = "foo"
d[1,0,3] = "bar"
```

在这种情况下，键值代表一个元组，使得这些赋值等同于以下内容：

```python
d[(1,2,3)] = "foo"
d[(1,0,3)] = "bar"
```

使用元组作为键是创建映射中复合键的一种常用技术。例如，一个键可以由“名（first name）”和“姓（last name）”组成。

## 2.14 列表、集合和字典推导式

涉及数据最常见的操作之一是将一个数据集合转换为另一种数据结构。例如，在这里我们获取列表中的所有项目，执行某种操作，并创建一个新列表：

```python
nums = [1, 2, 3, 4, 5]
squares = []
for n in nums:
    squares.append(n * n)
```

由于这类操作非常常见，因此它被提供为一个名为“列表推导式（list comprehension）”的运算符。以下是该代码的更紧凑版本：

```python
nums = [1, 2, 3, 4, 5]
squares = [n * n for n in nums]
```

此外，还可以对操作应用过滤器：

```python
squares = [n * n for n in nums if n > 2]     # [9, 16, 25]
```

列表推导式的通用语法如下：

```python
[expression for item1 in iterable1 if condition1
     for item2 in iterable2 if condition2
     ...
     for itemN in iterableN if conditionN]
```

该语法等同于以下代码：

```python
result = []
for item1 in iterable1:
    if condition1:
        for item2 in iterable2:
            if condition2:
                ...
                for itemN in iterableN:
                    if conditionN:
                        result.append(expression)
```

列表推导式是处理各种形式列表数据的非常有效的方法。以下是一些实际示例：

```python
# 一些数据（字典列表）
portfolio = [
    {'name': 'IBM', 'shares': 100, 'price': 91.1 },
    {'name': 'MSFT', 'shares': 50, 'price': 45.67 },
    {'name': 'HPE', 'shares': 75, 'price': 34.51 },
    {'name': 'CAT', 'shares': 60, 'price': 67.89 },
    {'name': 'IBM', 'shares': 200, 'price': 95.25 }
]

# 收集所有名称 ['IBM', 'MSFT', 'HPE', 'CAT', 'IBM' ]
names = [s['name'] for s in portfolio]

# 查找所有持股超过 100 的条目 ['IBM']
more100 = [s['name'] for s in portfolio if s['shares'] > 100 ]

# 计算总股数*价格
cost = sum([s['shares']*s['price'] for s in portfolio])

# 收集 (名称, 股数) 元组
name_shares = [ (s['name'], s['shares']) for s in portfolio ]
```

列表推导式内部使用的所有变量都对该推导式私有。你不必担心这些变量会覆盖其他同名变量。例如：

```python
>>> x = 42
>>> squares = [x*x for x in [1,2,3]]
>>> squares
[1, 4, 9]
>>> x
42
>>>
```

除了创建列表，你还可以通过将方括号改为花括号来创建集合。这被称为“集合推导式（set comprehension）”。集合推导式将为你提供一组不重复的值。例如：

```python
# 集合推导式
names = { s['name'] for s in portfolio }
# names = { 'IBM', 'MSFT', 'HPE', 'CAT' }
```

如果你指定 `键:值` 对，则会创建一个字典。这被称为“字典推导式（dictionary comprehension）”。例如：

```python
prices = { s['name']:s['price'] for s in portfolio }
# prices = { 'IBM': 95.25, 'MSFT': 45.67, 'HPE': 34.51, 'CAT': 67.89 }
```

在创建集合和字典时，请注意后面的条目可能会覆盖前面的条目。例如，在 `prices` 字典中，你获得的是 `'IBM'` 的最后一个价格，第一个价格丢失了。

在推导式内部，无法包含任何形式的异常处理。如果这是一个问题，可以考虑使用函数来包装异常，如下所示：

```python
def toint(x):
    try:
        return int(x)
    except ValueError:
        return None

values = [ '1', '2', '-4', 'n/a', '-3', '5' ]
data1 = [ toint(x) for x in values ]
# data1 = [1, 2, -4, None, -3, 5]
data2 = [ toint(x) for x in values if toint(x) is not None ]
# data2 = [1, 2, -4, -3, 5]
```

最后一个示例中 `toint(x)` 的重复计算可以通过使用 `:=` 运算符（海象运算符）来避免。例如：

```python
data3 = [ v for x in values if (v:=toint(x)) is not None ]
# data3 = [1, 2, -4, -3, 5]
data4 = [ v for x in values if (v:=toint(x)) is not None and v >= 0 ]
# data4 = [1, 2, 5]
```

## 2.15 生成器表达式

生成器表达式是一个执行与列表推导式相同计算但迭代产生结果的对象。其语法与列表推导式相同，不同之处在于使用圆括号而不是方括号。这里有一个例子：

```python
nums = [1,2,3,4]
squares = (x*x for x in nums)
```

与列表推导式不同，生成器表达式并不会实际创建列表，也不会立即计算圆括号内的表达式。相反，它创建了一个生成器对象，该对象通过迭代按需产生值。如果你查看上述示例的结果，你会看到以下内容：

```python
>>> squares
<generator object at 0x590a8>
>>> next(squares)
1
>>> next(squares)
4
...
>>> for n in squares:
...     print(n)
9
16
>>>
```

生成器表达式只能使用一次。如果你尝试第二次迭代，将无法获得任何内容：

```python
>>> for n in squares:
...     print(n)
...
>>>
```

列表推导式和生成器表达式之间的区别很重要但很微妙。使用列表推导式，Python 实际上创建了一个包含结果数据的列表。而使用生成器表达式，Python 创建了一个仅知道如何按需产生数据的生成器。在某些应用中，这可以大大提高性能并减少内存使用。这里有一个例子：

```python
# 读取文件
f = open('data.txt')          # 打开文件
lines = (t.strip() for t in f)  # 读取行，去除首尾空白字符
comments = (t for t in lines if t[0] == '#') # 所有注释
for c in comments:
    print(c)
```

在这个示例中，提取行并去除空白字符的生成器表达式并不会实际将整个文件读取并保存在内存中。提取注释的表达式也是如此。相反，当程序在随后的循环中开始迭代时，文件的每一行会被逐一读取。在这次迭代过程中，文件的行被按需产生并相应地过滤。事实上，在整个过程中，整个文件都不会被加载到内存中。因此，这是一种从数 GB 大小的 Python 源文件中提取注释的高效方法。

与列表推导式不同，生成器表达式创建的对象不像序列那样工作。它不能被索引，且任何通常的列表操作（如 `append()`）都无法生效。然而，生成器表达式产生的项目可以使用 `list()` 转换为列表：

```python
clist = list(comments)
```



当作为单个函数参数传递时，可以去掉一组圆括号。例如，以下语句是等价的：

```python
sum((x*x for x in values))

sum(x*x for x in values)     # 移除了额外的圆括号
```

在这两种情况下，都会创建生成器`(x*x for x in values)`并将其传递给`sum()`函数。

## 2.16 属性（`.`）运算符

点号（`.`）运算符用于访问对象的属性。这里有一个例子：

```python
foo.x = 3

print(foo.y)

a = foo.bar(3,4,5)
```

在单个表达式中可以出现多个点运算符，例如`foo.y.a.b`。点运算符也可以应用于函数的中间结果，如`a = foo.bar(3,4,5).spam`。不过，从代码风格来看，程序中很少创建如此长的属性查找链。

## 2.17 函数调用`()`运算符

`f(args)`运算符用于对`f`进行函数调用。传递给函数的每个参数都是一个表达式。在调用函数之前，所有参数表达式都将从左到右被完全计算。这被称为“适用顺序求值（applicative order evaluation）”。关于函数的更多信息可以在第 5 章中找到。

## 2.18 求值顺序

表 2.11 列出了 Python 运算符的操作顺序（优先级规则）。除幂（`**`）运算符外，所有运算符都从左到右求值，并按优先级从高到低列在表中。也就是说，表中先列出的运算符在后列出的运算符之前求值。包含在一起的运算符……

在子部分中，例如`x * y`、`x / y`、`x // y`、`x @ y`和`x % y`具有相同的优先级。

### 表 2.11 求值顺序（从最高优先级到最低优先级）

| 运算符 | 名称 |
| --- | --- |
| `(...)`、`[...]`、`{...}` | 元组、列表和字典创建 |
| `s[i]`、`s[i:j]` | 索引和切片 |
| `s.attr` | 属性查找 |
| `f(...)` | 函数调用 |
| `+x`、`-x`、`~x` | 一元运算符 |
| `x ** y` | 幂运算（右结合） |
| `x * y`、`x / y`、`x // y`、`x % y`、`x @ y` | 乘法、除法、整除、取模、矩阵乘法 |
| `x + y`、`x - y` | 加法、减法 |
| `x << y`、`x >> y` | 位移 |
| `x & y` | 按位与 |
| `x ^ y` | 按位异或 |
| `x \| y` | 按位或 |
| `x < y`、`x <= y`、`x > y`、`x >= y`、`x == y`、`x != y`、`x is y`、`x is not y`、`x in y`、`x not in y` | 比较、身份和序列成员测试 |
| `not x` | 逻辑非 |
| `x and y` | 逻辑与 |
| `x or y` | 逻辑或 |
| `lambda args: expr` | 匿名函数 |
| `expr if expr else expr` | 条件表达式 |
| `name := expr` | 赋值表达式 |

表 2.11 中的求值顺序不依赖于`x`和`y`的类型。因此，尽管用户定义对象可以重新定义单个运算符，但无法自定义底层的求值顺序、优先级和结合性规则。

关于优先级规则的一个常见混淆是，当按位与（`&`）和按位或（`|`）运算符被用来表示逻辑与（`and`）和逻辑或（`or`）时。例如：

```python
>>> a = 10

>>> a <= 10 and 1 < a

True

>>> a <= 10 & 1 < a

False

>>>
```

后一个表达式被求值为`a <= (10 & 1) < a`或`a <= 0 < a`。你可以通过添加括号来修复它：

```python
>>> (a <= 10) & (1 < a)

True

>>>
```

这看起来可能像是一个冷门的边缘情况，但在一些面向数据的包（如`numpy`和`pandas`）中经常出现。由于逻辑运算符`and`和`or`无法被自定义，因此使用了按位运算符——尽管它们的优先级更高，并且在用于布尔关系时求值方式不同。

## 2.19 结语：数据的秘密生活

Python 最频繁的用途之一是在涉及数据操纵和分析的应用中。在这里，Python 为思考问题提供了一种“领域语言”。内置运算符和表达式是该语言的核心，其他一切都构建在其之上。因此，一旦你对 Python 的内置对象和操作建立起一种直觉，你会发现这种直觉可以应用于任何地方。

举个例子，假设你正在处理一个数据库，并希望遍历查询返回的记录。很可能你会使用`for`语句来完成这项工作。或者，假设你正在处理数值数组并希望对数组执行逐元素数学运算。你可能会认为标准的数学运算符可以奏效——而你的直觉是正确的。或者，假设你正在使用一个库通过 HTTP 获取数据，并希望访问 HTTP 标头的内容。很有可能这些数据将以类似字典的方式呈现。

关于 Python 内部协议及其自定义方式的更多信息将在第 4 章中给出。

# 3. 程序结构和控制流

本章涵盖程序结构和控制流的细节。主题包括条件语句、循环、异常和上下文管理器。

## 3.1 程序结构与执行

Python 程序被组织为一系列语句。所有语言特性，包括变量赋值、表达式、函数定义、类和模块导入，都是与所有其他语句具有同等地位的语句——这意味着任何语句几乎可以放置在程序的任何位置（尽管某些语句如`return`只能出现在函数内部）。例如，下面的代码在一个条件语句内部定义了两个不同版本的函数：

```python
if debug:

    def square(x):

        if not isinstance(x,float):

            raise TypeError('Expected a float')

        return x * x

else:

    def square(x):

        return x * x
```

在加载源文件时，解释器按照语句出现的顺序执行，直到没有更多语句可执行。这种执行模型既适用于作为主程序运行的文件，也适用于通过`import`加载的库文件。

## 3.2 条件执行

`if`、`else`和`elif`语句控制代码的条件执行。条件语句的一般格式为：

```python
if expression:

    statements

elif expression:

    statements

elif expression:

    statements

...

else:

    statements
```

如果没有需要执行的操作，你可以省略条件语句的`else`和`elif`子句。如果某个特定子句中不存在任何语句，请使用`pass`语句：

```python
if expression:

    pass            # 待办：请实现

else:

    statements
```

## 3.3 循环与迭代

你使用`for`和`while`语句来实现循环。这里有一个例子：

```python
while expression:

    statements
```

```python
for i in s:

    statements
```

`while`语句会重复执行语句，直到相关表达式的求值结果为`False`。`for`语句会遍历`s`的所有元素，直到没有更多可用元素。`for`语句适用于任何支持迭代的对象。这包括内置的序列类型（如列表、元组和字符串），以及任何实现了迭代器协议的对象。

在语句`for i in s`中，变量`i`被称为迭代变量。在每次循环迭代中，它从`s`中接收一个新值。迭代变量的作用域并不是`for`语句私有的。如果之前定义了一个同名变量，该值将被覆盖。此外，迭代变量在循环完成后会保留最后一个值。

如果迭代产生的元素是大小相同的可迭代对象，你可以使用如下语句将它们的值解包到单独的迭代变量中：

```python
s = [ (1, 2, 3), (4, 5, 6) ]

for x, y, z in s:

    statements
```

在这个例子中，`s`必须包含或产生每个具有三个元素的可迭代对象。在每次迭代中，变量`x`、`y`和`z`的内容被赋值为相应可迭代对象的项。虽然这种用法最常见于`s`是元组序列的情况，但只要`s`中的项是任何种类的可迭代对象（包括列表、生成器和字符串），解包都能奏效。

有时在解包时会使用像`_`这样的丢弃变量。例如：

```python
for x, _, z in s:

    statements
```

在这个例子中，值仍然被放入`_`变量中，但该变量的名称暗示它在随后的语句中并不重要或没有用处。

如果可迭代对象产生的项大小不一，你可以使用通配符解包将多个值放入一个变量中。例如：

```python
s = [ (1, 2), (3, 4, 5), (6, 7, 8, 9) ]

for x, y, *extra in s:

    statements

    # x = 1, y = 2, extra = []

    # x = 3, y = 4, extra = [5]

    # x = 6, y = 7, extra = [8, 9]

    # ...
```

在这个例子中，至少需要两个值`x`和`y`，而`*extra`接收可能存在的任何额外值。这些值总是被放入一个列表中。在单次解包中，最多只能出现一个带星号的变量，但它可以出现在任何位置。因此，以下两种变体都是合法的：

```python
for *first, x, y in s:

    ...

for x, *middle, y in s:

    ...
```

在循环时，除了数据值之外，记录一个数值索引有时很有用。这里有一个例子：

```python
i = 0

for x in s:

    statements

    i += 1
```

Python 提供了一个内置函数`enumerate()`，可以用来简化这段代码：

```python
for i, x in enumerate(s):

    statements
```

`enumerate(s)`创建一个迭代器，产生元组`(0, s[0])`、`(1, s[1])`、`(2, s[2])`等。可以通过向`enumerate()`提供`start`关键字参数来指定不同的计数起始值：

```python
for i, x in enumerate(s, start=100):

    statements
```

在这种情况下，将产生形式为`(100, s[0])`、`(101, s[1])`等的元组。

另一个常见的循环问题是并行迭代两个或多个可迭代对象——例如，编写一个循环，在每次迭代中从不同的序列中获取项：

```python
# s 和 t 是两个序列

i = 0

while i < len(s) and i < len(t):

    x = s[i]            # 从 s 中获取一项

    y = t[i]            # 从 t 中获取一项

    statements

    i += 1
```

这段代码可以使用`zip()`函数来简化。例如：

```python
# s 和 t 是两个序列

for x, y in zip(s, t):

    statements
```

`zip(s, t)`将可迭代对象`s`和`t`组合成一个由元组`(s[0], t[0])`、`(s[1], t[1])`、`(s[2], t[2])`等组成的迭代器；如果两者长度不等，则在最短的那个结束时停止。`zip()`的结果是一个迭代器，在迭代时产生结果。如果你想将结果转换为列表，请使用`list(zip(s, t))`。

要跳出循环，请使用`break`语句。例如，以下代码从文件中读取文本行，直到遇到空行：

```python
with open('foo.txt') as file:

    for line in file:

        stripped = line.strip()

        if not stripped:

            break        # 空行，停止读取

        # 处理去掉空白字符的行

        ...
```

要跳转到循环的下一次迭代（跳过循环体的剩余部分），请使用`continue`语句。当你反转测试条件而导致缩进增加一层，使得程序嵌套过深或不必要地复杂时，该语句非常有用。例如，以下循环会跳过文件中的所有空行：

```python
with open('foo.txt') as file:

    for line in file:

        stripped = line.strip()

        if not stripped:

            continue     # 跳过空行

        # 处理去掉空白字符的行

        ...
```

`break`和`continue`语句仅适用于当前正在执行的最内层循环。如果你需要跳出深层嵌套的循环结构，可以使用异常。Python 没有提供“goto”语句。你还可以将`else`语句附加到循环结构中，如下例所示：

```python
# for-else

with open('foo.txt') as file:

    for line in file:

        stripped = line.strip()

        if not stripped:

            break

        # 处理去掉空白字符的行

        ...

else:

    raise RuntimeError('Missing section separator')
```

循环的`else`子句仅在循环运行完毕时执行。这可能发生在立即开始时（如果循环根本不执行）或在最后一次迭代之后。如果循环使用`break`语句提前终止，则跳过`else`子句。

循环`else`子句的主要用例是：在迭代数据的代码中，如果循环提前中断，需要设置或检查某种标志或条件。例如，如果你不使用`else`，之前的代码可能需要使用标志变量重写如下：

```python
found_separator = False

with open('foo.txt') as file:

    for line in file:

        stripped = line.strip()

        if not stripped:

            found_separator = True

            break

        # 处理去掉空白字符的行

        ...

if not found_separator:

    raise RuntimeError('Missing section separator')
```

## 3.4 异常

异常表示错误，并会中断程序的正常控制流。使用`raise`语句引发异常。`raise`语句的一般格式为`raise Exception([value])`，其中`Exception`是异常类型，`value`是一个可选值，用于提供关于异常的具体详细信息。这里有一个示例：

```python
raise RuntimeError('Unrecoverable Error')
```

要捕获异常，请使用`try`和`except`语句，如这里所示：

```python
try:

    file = open('foo.txt', 'rt')

except FileNotFoundError as e:

    statements
```

当异常发生时，解释器停止执行`try`块中的语句，并寻找与所发生的异常类型匹配的`except`子句。如果找到了，控制权将传递给`except`子句中的第一个语句。`except`子句执行完毕后，控制权将继续执行整个`try-except`块之后出现的第一个语句。

`try`语句不必匹配所有可能发生的异常。如果没有找到匹配的`except`子句，异常将继续传播，并可能在其他能够处理该异常的`try-except`块中被捕获。从编程风格来看，你应该只捕获代码能够实际恢复的异常。如果无法恢复，通常更好的做法是让异常继续传播。

如果异常一直传播到程序的顶层而未被捕获，解释器将终止并显示错误消息。

如果单独使用`raise`语句，则会再次引发最后一次生成的异常。这仅在处理之前引发的异常时有效。例如：

```python
try:

    file = open('foo.txt', 'rt')

except FileNotFoundError:

    print("Well, that didn't work.")

    raise        # 重新引发当前异常
```



每个`except`子句可以使用`as var`修饰符，该修饰符为变量命名，如果发生异常，异常类型的实例将被放入该变量中。异常处理程序可以检查此值以进一步了解异常原因。例如，你可以使用`isinstance()`来检查异常类型。

异常有几个标准属性，在需要针对错误执行进一步操作的代码中可能会很有用：

- `e.args`：引发异常时提供的参数元组。在大多数情况下，这是一个包含描述错误的字符串的一项元组。对于`OSError`异常，该值是一个包含整数错误代码、字符串错误消息和可选文件名的 2 元组或 3 元组。
- `e.__cause__`：如果该异常是为了响应处理另一个异常而故意引发的，则为之前的异常。请参阅稍后关于链式异常的章节。
- `e.__context__`：如果异常是在处理另一个异常时引发的，则为之前的异常。
- `e.__traceback__`：与异常关联的堆栈回溯对象。

用于持有异常值的变量仅在关联的`except`块内部可访问。一旦控制权离开该块，该变量将变得未定义。例如：

```python
try:
    int('N/A')                 # 引发 ValueError
except ValueError as e:
    print('Failed:', e)
print(e)     # 失败 -> NameError. 'e' not defined.
```

可以使用多个`except`子句来指定多个异常处理块：

```python
try:
    do something
except TypeError as e:
    # 处理 Type 错误
    ...
except ValueError as e:
    # 处理 Value 错误
    ...
```

单个处理子句可以像这样捕获多种异常类型：

```python
try:
    do something
except (TypeError, ValueError) as e:
    # 处理 Type 或 Value 错误
    ...
```

要忽略异常，请如下使用`pass`语句：

```python
try:
    do something
except ValueError:
    pass                # 什么都不做（耸肩）。
```

静默地忽略错误通常是很危险的，并且是难以发现的错误的根源。即便选择忽略，将错误选择性地记录在日志或其他可以稍后检查的地方通常也是明智的。

要捕获除程序退出相关的异常之外的所有异常，请像这样使用`Exception`：

```python
try:
    do something
except Exception as e:
    print(f'An error occurred : {e!r}')
```

在捕获所有异常时，你应该非常小心地向用户报告准确的错误信息。例如，在之前的代码中，打印了错误消息和相关的异常值。如果你不包含任何关于异常值的信息，那么在代码因你意想不到的原因而失败时，调试将变得非常困难。

`try`语句还支持`else`子句，它必须紧跟在最后一个`except`子句之后。如果`try`块中的代码没有抛出异常，则执行此代码。示例如下：

```python
try:
    file = open('foo.txt', 'rt')
except FileNotFoundError as e:
    print(f'Unable to open foo : {e}')
    data = ''
else:
    data = file.read()
    file.close()
```

`finally`语句定义了一个清理操作，无论`try-except`块中发生了什么，该操作都必须执行。示例如下：

```python
file = open('foo.txt', 'rt')
try:
    # 执行一些操作
    ...
finally:
    file.close()
    # 无论发生了什么，文件都会关闭
```

`finally`子句不用于捕获错误。相反，它用于无论是否发生错误都必须执行的代码。如果没有抛出异常，`finally`子句中的代码将在`try`块中的代码执行后立即执行。如果发生了异常，首先执行匹配的`except`块（如果有），然后控制权传递给`finally`子句的第一条语句。如果这段代码执行后异常仍然处于挂起状态，该异常将被重新抛出，以便被另一个异常处理器捕获。

## 3.4.1 异常层次结构

处理异常的一个挑战是管理程序中可能出现的极大量异常。例如，仅内置异常就有 60 多个。再加上标准库的其余部分，可能的异常就变成了数百个。此外，通常没有办法预先轻松确定代码的任何部分可能会抛出什么样的异常。异常既不会作为函数调用签名的部分被记录，也没有任何编译器来验证代码中异常处理的正确性。因此，异常处理有时会让人觉得随机且无组织。

意识到异常是通过继承组织成层次结构的会有所帮助。与其针对特定的错误，不如关注更通用的错误类别，这样可能会更容易。例如，考虑在容器中查找值时可能出现的不同错误：

```python
try:
    item = items[index]
except IndexError:         # 如果 items 是序列则抛出
    ...
except KeyError:           # 如果 items 是映射则抛出
    ...
```

与其编写代码来处理两个高度具体的异常，不如这样做：

```python
try:
    item = items[index]
except LookupError:
    ...
```

`LookupError`是一个表示异常高层分组的类。`IndexError`和`KeyError`都继承自`LookupError`，因此这个`except`子句可以捕获其中任何一个。然而，`LookupError`又不像那么宽泛，以至于包含了与查找无关的错误。

表 3.1 描述了最常见的内置异常类别。

### 表 3.1 异常类别

| 异常类 | 描述 |
|-----------------|-------------|
| `BaseException` | 所有异常的根类 |
| `Exception` | 所有程序相关错误的基类 |
| `ArithmeticError` | 所有数学相关错误的基类 |
| `ImportError` | 所有`import`相关错误的基类 |
| `LookupError` | 所有容器查找错误的基类 |
| `OSError` | 所有系统相关错误的基类。`IOError`和`EnvironmentError`是其别名。 |
| `ValueError` | 所有值相关错误的基类，包括 Unicode |
| `UnicodeError` | Unicode 字符串编码相关错误的基类 |

`BaseException`类很少直接用于异常处理，因为它匹配所有可能的异常。这包括影响控制流的特殊异常，如`SystemExit`、`KeyboardInterrupt`和`StopIteration`。捕获这些异常通常不是你想要的。相反，所有普通的程序相关错误都继承自`Exception`。`ArithmeticError`是所有数学相关错误的基类，例如`ZeroDivisionError`、`FloatingPointError`和`OverflowError`。`ImportError`是所有导入相关错误的基类。`LookupError`是所有容器查找相关错误的基类。`OSError`是所有源自操作系统和环境的错误的基类。`OSError`涵盖了与文件、网络连接、权限、管道、超时等相关的广泛异常。当向操作提供错误的输入值时，通常会抛出`ValueError`异常。`UnicodeError`是`ValueError`的子类，将所有与 Unicode 相关的编码和解码错误分组在一起。

表 3.2 显示了一些直接继承自`Exception`但不属于更大异常组的常见内置异常。

### 表 3.2 其他内置异常

| 异常类 | 描述 |
|-----------------|-------------|
| `AssertionError` | `assert`语句失败 |
| `AttributeError` | 对象的属性查找错误 |
| `EOFError` | 文件末尾 |
| `MemoryError` | 可恢复的内存不足错误 |
| `NameError` | 在局部或全局命名空间中未找到名称 |
| `NotImplementedError` | 未实现的功能 |
| `RuntimeError` | 一个通用的“发生了某些糟糕的事情”的错误 |
| `TypeError` | 操作应用于错误类型的对象 |
| `UnboundLocalError` | 在赋值之前使用了局部变量 |

## 3.4.2 异常与控制流

通常，异常是预留给错误处理的。然而，少数异常被用于改变控制流。这些异常如表 3.3 所示，直接继承自`BaseException`。

### 表 3.3 用于控制流的异常

| 异常类 | 描述 |
|-----------------|-------------|
| `SystemExit` | 抛出以指示程序退出 |
| `KeyboardInterrupt` | 当程序通过 Control-C 被中断时抛出 |
| `StopIteration` | 抛出以发出迭代结束的信号 |

`SystemExit`异常用于使程序故意终止。作为参数，你可以提供一个整数退出代码或一个字符串消息。如果提供了字符串，它将被打印到`sys.stderr`，并且程序以退出代码 1 终止。

```python
import sys

if len(sys.argv) != 2:
    raise SystemExit(f'Usage: {sys.argv[0]} filename')

filename = sys.argv[1]
```

当程序接收到 SIGINT 信号（通常是在终端中按下 Control-C）时，会抛出`KeyboardInterrupt`异常。这个异常有点不寻常，因为它是异步的——这意味着它几乎可以在任何时间以及程序的任何语句中发生。Python 的默认行为是在发生这种情况时直接终止。如果你想控制 SIGINT 的传递，可以使用`signal`库模块（见第 9 章）。

`StopIteration`异常是迭代协议的一部分，用于发出迭代结束的信号。

## 3.4.3 定义新异常

所有内置异常都是以类定义的。要创建新异常，请创建一个继承自`Exception`的新类定义，如下所示：

```python
class NetworkError(Exception):
    pass
```

要使用你的新异常，请按如下方式使用`raise`语句：

```python
raise NetworkError('Cannot find host')
```

在抛出异常时，随`raise`语句提供的可选值将用作异常类构造函数的参数。大多数情况下，这是一个包含某种形式的错误消息。然而，用户自定义的异常可以编写为接收一个或多个异常值，如下例所示：

```python
class DeviceError(Exception):
    def __init__(self, errno, msg):
        self.args = (errno, msg)
        self.errno = errno
        self.errmsg = msg

# 抛出异常（多个参数）
raise DeviceError(1, 'Not Responding')
```

当你创建重新定义了`__init__()`的自定义异常类时，重要的是要像示例中那样，将包含`__init__()`参数的元组赋值给属性`self.args`。该属性在打印异常追溯（traceback）消息时被使用。如果你不对其进行定义，用户在发生错误时将无法看到关于该异常的任何有用信息。

可以使用继承将异常组织成一个层次结构。例如，之前定义的`NetworkError`异常可以作为多种更具体错误的基类。这里有一个示例：

```python
class HostnameError(NetworkError):
    pass

class TimeoutError(NetworkError):
    pass

def error1():
    raise HostnameError('Unknown host')

def error2():
    raise TimeoutError('Timed out')
```

```python
try:
    error1()
except NetworkError as e:
    if type(e) is HostnameError:
        # 为这类错误执行特殊操作
        ...
```

在这种情况下，`except NetworkError`子句会捕获任何派生自`NetworkError`的异常。为了找到抛出的具体错误类型，可以使用`type()`检查执行值的类型。

## 3.4.4 链式异常

有时，为了响应某个异常，你可能想要抛出另一个不同的异常。为此，请抛出一个链式异常：

```python
class ApplicationError(Exception):
    pass

def do_something():
    x = int('N/A')     # 抛出 ValueError

def spam():
    try:
        do_something()
    except Exception as e:
        raise ApplicationError('It failed') from e
```

如果发生未捕获的`ApplicationError`，你将收到一条包含这两个异常的消息。例如：

```
>>> spam()
Traceback (most recent call last):
  File "c.py", line 9, in spam
     do_something()
  File "c.py", line 5, in do_something
     x = int('N/A')
ValueError: invalid literal for int() with base 10: 'N/A'

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "c.py", line 11, in spam
    raise ApplicationError('It failed') from e
__main__.ApplicationError: It failed
>>>
```

如果你捕获了`ApplicationError`，生成的异常的`__cause__`属性将包含另一个异常。例如：

```python
try:
    spam()
except ApplicationError as e:
    print('It failed. Reason:', e.__cause__)
```

如果你想抛出一个新异常而不包含其他异常链，请像这样从`None`抛出错误：

```python
def spam():
    try:
        do_something()
    except Exception as e:
        raise ApplicationError('It failed') from None
```

出现在`except`块中的编程错误也会导致链式异常，但其运作方式略有不同。例如，假设你有这样一段有缺陷的代码：

```python
def spam():
    try:
        do_something()
    except Exception as e:
        print('It failed:', err)    # err 未定义（拼写错误）
```

由此产生的异常追溯消息略有不同：

```
>>> spam()
Traceback (most recent call last):
  File "d.py", line 9, in spam
    do_something()
  File "d.py", line 5, in do_something
    x = int('N/A')
ValueError: invalid literal for int() with base 10: 'N/A'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "d.py", line 11, in spam
    print('It failed: Reason: ', err)
NameError: name 'err' is not defined
>>>
```

如果在处理另一个异常时抛出了意外异常，`__context__`属性（而非`__cause__`）将保存发生错误时正在处理的异常信息。例如：



```python
try:
    spam()
except Exception as e:
    print('It failed. Reason:', e)
    if e.__context__:
        print('While handling:', e.__context__)
```

在异常链中，预期异常（expected exceptions）和意外异常（unexpected exceptions）之间有一个重要的区别。在第一个例子中，代码编写时已经预料到了异常的可能性。例如，代码被明确地包裹在`try-except`块中：

```python
try:
    do_something()
except Exception as e:
    raise ApplicationError('It failed') from e
```

在第二个案例中，`except`块中存在编程错误：

```python
try:
    do_something()
except Exception as e:
    print('It failed:', err)     # err 未定义
```

这两种情况之间的区别虽然微妙但很重要。这就是为什么异常链信息被分别放入`__cause__`或`__context__`属性中。`__cause__`属性保留给当你预期可能会失败的情况。`__context__`属性在两种情况下都会被设置，但对于在处理另一个异常时抛出的意外异常，它将是唯一的信息来源。

### 3.4.5 异常追溯

异常具有相关的栈追溯（stack traceback），可提供关于错误发生位置的信息。追溯存储在异常的`__traceback__`属性中。出于报告或调试的目的，你可能希望自己生成追溯消息。可以使用`traceback`模块来实现这一点。

例如：

```python
import traceback

try:
    spam()
except Exception as e:
    tblines = traceback.format_exception(type(e), e, e.__traceback__)
    tbmsg = ''.join(tblines)
    print('It failed:')
    print(tbmsg)
```

在这段代码中，`format_exception()`生成一个字符串列表，其中包含 Python 在追溯消息中通常会产生的输出。作为输入，你需要提供异常类型、值和追溯。

### 3.4.6 异常处理建议

在大型程序中，异常处理是最难做正确的事情之一。不过，有一些经验法则可以使其变得更容易。

第一条规则是：不要捕获在代码该特定位置无法处理的异常。考虑这样一个函数：

```python
def read_data(filename):
    with open(filename, 'rt') as file:
        rows = []
        for line in file:
            row = line.split()
            rows.append((row[0], int(row[1]), float(row[2])))
        return rows
```

假设`open()`函数因为文件名错误而失败。这是一个应该在该函数中使用`try-except`语句捕获的错误吗？可能不是。如果调用者提供了一个错误的文件名，那么没有合理的恢复方法。没有文件可打开，没有数据可读取，也没有其他可行方案。更好的做法是让操作失败并将异常报告回调用者。在`read_data()`中避免错误检查并不意味着异常永远不会在任何地方被处理——它仅仅意味着处理它不是`read_data()`的职责。也许提示用户输入文件名的那段代码会处理这个异常。

对于习惯于依赖特殊错误代码或包装结果类型的语言的程序员来说，这个建议可能与他们的经验相悖。在那些语言中，必须非常小心地确保在所有操作上始终检查返回代码以确认错误。但在 Python 中不需要这样做。如果一个操作可能会失败且你无法采取任何措施恢复，那么最好直接让它失败。异常将传播到程序的上层，在那里通常由其他代码负责处理它。

另一方面，函数可能能够从错误数据中恢复。例如：

```python
def read_data(filename):
    with open(filename, 'rt') as file:
        rows = []
        for line in file:
            row = line.split()
            try:
                rows.append((row[0], int(row[1]), float(row[2])))
            except ValueError as e:
                print('Bad row:', row)
                print('Reason:', e)
        return rows
```

在捕获错误时，请尽量使`except`子句在合理的范围内尽可能狭窄。上面的代码可以使用`except Exception`来捕获所有错误。然而，这样做会导致代码捕获到那些可能不应该被忽略的正当编程错误。不要这样做——这会增加调试的难度。

最后，如果你在显式地抛出异常，请考虑创建自己的异常类型。例如：

```python
class ApplicationError(Exception):
    pass

class UnauthorizedUserError(ApplicationError):
    pass

def spam():
    ...
    raise UnauthorizedUserError('Go away')
    ...
```

在大型代码库中，最具挑战性的问题之一就是为程序故障分配责任。如果你定义自己的异常，你将能够更好地区分有意抛出的错误和正当的编程失误。如果你的程序由于上述某种`ApplicationError`而崩溃，你将立即知道为什么抛出该错误——因为是你编写的代码要求这么做的。另一方面，如果程序由于 Python 的内置异常（如`TypeError`或`ValueError`）而崩溃，这可能预示着一个更严重的问题。

## 3.5 上下文管理器和`with`语句

当与异常结合时，对文件、锁和连接等系统资源的妥善管理往往是一个棘手的问题。例如，抛出的异常可能会导致控制流跳过负责释放关键资源（如锁）的语句。

`with`语句允许一系列语句在一个由充当上下文管理器的对象控制的运行时上下文中执行。这里有一个示例：

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

在第一个示例中，当控制流离开随后的语句块时，`with`语句会自动关闭打开的文件。在第二个示例中，当控制流进入和离开随后的语句块时，`with`语句会自动获取和释放锁。

`with obj`语句允许对象`obj`管理控制流进入和退出其关联的后续语句块时发生的情况。当`with obj`语句执行时，它会调用`obj.__enter__()`方法来发出进入新上下文的信号。当控制流离开上下文时，`obj.__exit__(type, value, traceback)`方法将被执行。如果没有抛出异常，`__exit__()`的三个参数都将被设置为`None`。否则，它们包含与导致控制流离开上下文的异常相关联的类型、值和回溯信息。如果`__exit__()`方法返回`True`，则表示抛出的异常已被处理，不再应继续传播。返回`None`或`False`将导致异常继续传播。

`with obj`语句接受一个可选的`as var`指定符。如果提供了该指定符，`obj.__enter__()`返回的值将被放入`var`中。这个值通常与`obj`相同，因为这允许在同一个步骤中构造对象并将其用作上下文管理器。例如，考虑这个类：

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

使用它，你可以在一个步骤中创建实例并将其用作上下文管理器：

```python
with Manager(42) as m:
    m.yow()
```

这里有一个涉及列表事务的更有意思的示例：

```python
class ListTransaction:
    def __init__(self, thelist):
        self.thelist = thelist

    def __enter__(self):
        self.workingcopy = list(self.thelist)
        return self.workingcopy

    def __exit__(self, type, value, tb):
        if type is None:
            self.thelist[:] = self.workingcopy
        return False
```

这个类允许你对现有列表进行一系列修改。然而，只有在没有发生异常的情况下，这些修改才会生效。否则，原始列表将保持不变。例如：

```python
items = [1, 2, 3]

with ListTransaction(items) as working:
    working.append(4)
    working.append(5)
print(items)            # 输出 [1, 2, 3, 4, 5]

try:
    with ListTransaction(items) as working:
        working.append(6)
        working.append(7)
        raise RuntimeError("We're hosed!")
except RuntimeError:
    pass

print(items)            # 输出 [1, 2, 3, 4, 5]
```

`contextlib`标准库模块包含了与上下文管理器高级用法相关的功能。如果你发现自己经常创建上下文管理器，那么这个模块值得一看。

## 3.6 断言和`__debug__`

`assert`语句可以将调试代码引入程序。`assert`的一般形式是：

```
assert test [, msg]
```

其中`test`是一个应该计算为`True`或`False`的表达式。如果`test`计算为`False`，`assert`将抛出一个`AssertionError`异常，并附带传递给`assert`语句的可选消息`msg`。这里有一个示例：

```python
def write_data(file, data):
    assert file, 'write_data: file not defined!'
    ...
```

`assert`语句不应用于必须执行以确保程序正确运行的代码，因为如果 Python 在优化模式下运行（通过给解释器传递`-O`选项指定），它将不会被执行。特别是，使用`assert`来检查用户输入或某些重要操作是否成功是一个错误。相反，`assert`语句用于检查应该始终为真的不变式；如果某个不变式被违反，则代表程序中存在 bug，而不是用户的错误。

例如，如果之前显示的`write_data()`函数旨在供最终用户使用，则应将`assert`语句替换为常规的`if`语句和相应的错误处理。

`assert`的一个常见用途是在测试中。例如，你可以使用它来对函数进行最小化测试：

```python
def factorial(n):
    result = 1
    while n > 1:
        result *= n
        n -= 1
    return result

assert factorial(5) == 120
```

此类测试的目的不是为了穷举，而是作为一种“冒烟测试”。如果函数中存在明显的问题，代码在导入时会立即因断言失败而崩溃。

断言在指定关于预期输入和输出的某种编程契约时也非常有用。例如：

```python
def factorial(n):
    assert n > 0, "must supply a positive value"
    result = 1
    while n > 1:
        result *= n
        n -= 1
    return result
```

同样，这并不是为了检查用户输入，而更多的是一种对程序内部一致性的检查。如果其他代码尝试计算负数的阶乘，断言将失败并指向出错的代码，以便你进行调试。

## 3.7 结语

尽管 Python 支持多种涉及函数和对象的不同编程风格，但程序执行的基本模型是命令式编程。也就是说，程序由一系列语句组成，它们按照在源文件中出现的顺序依次执行。只有三种基本的控制流结构：`if`语句、`while`循环和`for`循环。在理解 Python 如何执行你的程序方面，几乎没有什么谜团。

到目前为止，最复杂且最容易出错的特性就是异常。事实上，本章的大部分内容都集中在如何正确思考异常处理上。即使你遵循了这些建议，异常在设计库、框架和 API 时仍然是一个微妙的部分。异常还可能破坏资源的正确管理——这是一个可以通过使用上下文管理器和`with`语句来解决的问题。

本章未涵盖的技巧是那些可以用来定制几乎所有 Python 语言特性的技术——包括内置运算符，甚至包括本章描述的控制流方面。尽管 Python 程序在结构上往往显得简单，但幕后经常运行着惊人的“魔法”。其中大部分内容将在下一章中描述。

# 4. 对象、类型和协议

Python 程序操作各种类型的对象。有许多内置类型，如数字、字符串、列表、集合和字典。此外，你可以使用类来创建自己的类型。本章描述了底层的 Python 对象模型以及使所有对象运行的机制。特别关注定义各种对象核心行为的“协议”。

## 4.1 核心概念

程序中存储的每一块数据都是一个对象。每个对象都有一个身份（identity）、一个类型（type，也称为其类）和一个值（value）。例如，当你编写`a = 42`时，会创建一个值为 42 的整数对象。对象的身份是一个代表其在内存中位置的数字；`a`是一个指向这个特定位置的标签，尽管该标签本身不是对象的一部分。

对象的类型（也称为对象的类）定义了对象的内部数据表示以及支持的方法。当创建特定类型的对象时，该对象被称为该类型的一个*实例*（instance）。实例创建后，其身份不会改变。如果对象的值可以被修改，则称该对象是可变的（mutable）。如果值不能被修改，则称该对象是不可变的（immutable）。持有对其他对象引用的对象被称为容器（container）。

对象的特征由其属性（attributes）决定。属性是与对象相关联的值，使用点运算符 (.) 来访问。属性可能是一个简单的数值，例如一个数字。然而，一个`attribute`也可以是一个被调用以执行某些操作的`function`。这类函数被称为`methods`（方法）。以下示例演示了对`attributes`的访问：

```python
a = 34                 # 创建一个整数
n = a.numerator        # 获取分子（一个属性）

b = [1, 2, 3]          # 创建一个列表
b.append(7)            # 使用 append 方法添加一个新元素
```

对象还可以实现各种运算符，例如`+`运算符。例如：

```python
c = a + 10             # c = 13 + 4j
d = b + [4, 5]         # d = [1, 2, 3, 4, 5]
```

虽然运算符使用了不同的语法，但它们最终都被映射到方法上。例如，编写`a + 10`实际上执行了方法`a.__add__(10)`。

## 4.2 对象身份与类型

内置函数`id()`返回对象的身份。身份是一个整数，通常对应于对象在内存中的位置。`is`和`is not`运算符用于比较两个对象的身份。`type()`返回对象的类型。以下是比较两个对象的几种不同方式的示例：

```python
# 比较两个对象
def compare(a, b):
    if a is b:
        print('same object')
    if a == b:
        print('same value')
    if type(a) is type(b):
        print('same type')
```

该函数的工作方式如下：



```python
>>> a = [1, 2, 3]
>>> b = [1, 2, 3]
>>> compare(a, a)
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

对象的类型本身也是一个对象，称为对象的类。这个对象是唯一定义的，对于给定类型的所有实例来说总是相同的。类通常有名称（`list`、`int`、`dict` 等），可用于创建实例、进行类型检查以及提供类型提示。例如：

```python
items = list()

if isinstance(items, list):
    items.append(item)
def removeall(items: list, item) -> list:
    return [i for i in items if i != item]
```

*子类型*（subtype）是通过继承定义的类型。它承载了原始类型的所有特性，以及额外的和/或重新定义的方法。继承将在第 7 章中详细讨论，这里是一个定义列表子类型并为其添加新方法的示例：

```python
class mylist(list):
    def removeall(self, val):
        return [i for i in self if i != val]

# 示例
items = mylist([5, 8, 2, 7, 2, 13, 9])
x = items.removeall(2)
print(x)     # [5, 8, 7, 13, 9]
```

`isinstance(instance, type)` 函数是检查值是否符合某种类型的首选方式，因为它能够识别子类型。它还可以针对多种可能的类型进行检查。例如：

```python
if isinstance(items, (list, tuple)):
    maxval = max(items)
```

虽然可以在程序中添加类型检查，但这往往不像你想象的那么有用。首先，过多的检查会影响性能。其次，程序定义的对象并不总是能整齐地适应一个完美的类型层级。例如，如果上面的 `isinstance(items, list)` 语句的目的是测试 `items` 是否“像列表一样”，那么它对于那些具有与列表相同编程接口但没有直接继承自内置 `list` 类型的对象（例如 `collections` 模块中的 `deque`）将不起作用。

## 4.3 引用计数与垃圾回收

Python 通过自动垃圾回收来管理对象。所有对象都通过引用计数（reference-counted）管理。每当对象被分配给一个新名称或被放入容器（如列表、元组或字典）时，其引用计数就会增加：

```python
a = 37       # 创建一个值为 37 的对象
b = a        # 增加 37 的引用计数
c = []
c.append(b)  # 增加 37 的引用计数
```

这个示例创建了一个包含值 37 的单一对象。`a` 是一个起初指向新创建对象的名称。当 `b` 被赋值为 `a` 时，`b` 变成了同一个对象的新名称，对象的引用计数增加。当你将 `b` 放入列表时，对象的引用计数再次增加。在整个示例中，只有一个对象对应于 37。所有其他操作都是在创建指向该对象的引用。

```python
del a         # 降低 37 的引用计数
b = 42        # 降低 37 的引用计数
c[0] = 2.0    # 降低 37 的引用计数
```

可以使用 `sys.getrefcount()` 函数获取对象的当前引用计数。例如：

```python
>>> a = 37
>>> import sys
>>> sys.getrefcount(a)
7
>>>
```

引用计数通常比你预期的要高得多。对于数字和字符串等不可变数据，解释器会在程序的不同部分之间激进地共享对象以节省内存。你只是没有注意到，因为这些对象是不可变的。

当对象的引用计数达到零时，它会被垃圾回收。然而，在某些情况下，不再使用的对象集合中可能存在循环依赖。这里有一个示例：

```python
a = { }
b = { }
a['b'] = b     # a 包含对 b 的引用
b['a'] = a     # b 包含对 a 的引用
del a
del b
```

在这个例子中，`del` 语句降低了 `a` 和 `b` 的引用计数，并销毁了用于引用底层对象的名称。然而，由于每个对象都包含对另一个对象的引用，引用计数不会掉到零，对象仍然被分配。解释器不会泄露内存，但对象的销毁将被延迟，直到循环检测器执行以查找并删除不可访问的对象。随着解释器在执行期间分配越来越多的内存，循环检测算法会定期运行。具体行为可以通过 `gc` 标准库模块中的函数进行微调和控制。`gc.collect()` 函数可用于立即调用循环垃圾回收器。

在大多数程序中，垃圾回收是自动发生的，你无需过多思考。然而，在某些情况下，手动删除对象可能是合理的。一种场景是在处理巨大的数据结构时。例如，考虑这段代码：

```python
def some_calculation():
    data = create_giant_data_structure()
    # 在计算的某个部分使用 data
```

```python
...
# Release the data
del data

# Calculation continues
...
```

在这段代码中，使用 `del data` 语句表明 `data` 变量不再需要。如果这导致引用计数达到 0，该对象此时将被垃圾回收。如果没有 `del` 语句，该对象将持续存在一段不确定的时间，直到函数结束时 `data` 变量超出作用域。你可能只有在尝试弄清楚为什么程序使用的内存比预期要多时，才会注意到这一点。

## 4.4 引用与副本

当程序执行类似 `b = a` 的赋值时，会创建一个对 `a` 的新引用。对于数字和字符串等不可变对象，这种赋值看起来像是创建了 `a` 的副本（尽管事实并非如此）。然而，对于列表和字典等可变对象，其行为截然不同。这里有一个示例：

```python
>>> a = [1,2,3,4]
>>> b = a              # b 是对 a 的引用
>>> b is a
True
>>> b[2] = -100        # 修改 b 中的一个元素
>>> a                  # 注意 a 也随之改变了
[1, 2, -100, 4]
>>>
```

在这个例子中，由于 `a` 和 `b` 指向同一个对象，对其中一个变量所做的更改会反映在另一个变量中。为了避免这种情况，你必须创建对象的副本，而不是创建新引用。

对于列表和字典等容器对象，有两种类型的复制操作：浅拷贝（shallow copy）和深拷贝（deep copy）。浅拷贝会创建一个新对象，但用原对象中包含的项的引用来填充它。这里有一个示例：

```python
>>> a = [ 1, 2, [3,4] ]
>>> b = list(a)                 # 创建 a 的浅拷贝
>>> b is a
False
>>> b.append(100)               # 向 b 添加元素
>>> b
[1, 2, [3, 4], 100]
>>> a                           # 注意 a 没有改变
[1, 2, [3, 4]]
>>> b[2][0] = -100             # 修改 b 内部的一个元素
>>> b
[1, 2, [-100, 4], 100]
>>> a                           # 注意 a 内部发生了改变
[1, 2, [-100, 4]]
>>>
```

在这种情况下，`a` 和 `b` 是独立的列表对象，但它们包含的元素是共享的。因此，如上所示，对 `a` 的其中一个元素进行修改也会修改 `b` 的相应元素。

深拷贝会创建一个新对象，并递归地复制它包含的所有对象。Python 没有内置的运算符来创建对象的深拷贝，但你可以使用标准库中的 `copy.deepcopy()` 函数。

```python
>>> import copy
>>> a = [1, 2, [3, 4]]
>>> b = copy.deepcopy(a)
>>> b[2][0] = -100
>>> b
[1, 2, [-100, 4]]
>>> a                              # 注意 a 没有改变
[1, 2, [3, 4]]
>>>
```

在大多数程序中，不建议积极推荐使用 `deepcopy()`。复制对象速度慢，且通常是不必要的。请将 `deepcopy()` 留给那些你确实需要副本的情况，例如你即将修改数据且不希望更改影响原对象时。此外，请注意 `deepcopy()` 在处理涉及系统或运行时状态的对象（如打开的文件、网络连接、线程、生成器等）时会失败。

## 4.5 对象表示与打印

程序经常需要显示对象——例如，向用户展示数据或为了调试目的而将其打印出来。如果你将对象 `x` 传递给 `print(x)` 函数或使用 `str(x)` 将其转换为字符串，你通常会得到一个“美观”的、人类可读的对象值表示。例如，考虑一个涉及日期的例子：

```python
>>> from datetime import date
>>> d = date(2012, 12, 21)
>>> print(d)
2012-12-21
>>> str(d)
'2012-12-21'
>>>
```

这种“美观”的对象表示对于调试可能并不足够。例如，在上述代码的输出中，没有明显的方法可以知道变量 `d` 是一个 `date` 实例，还是一个包含文本 '2012-12-21' 的简单字符串。为了获取更多信息，请使用 `repr(x)` 函数，它会创建一个字符串，该字符串表示你在源代码中创建该对象时必须输入的形式。例如：

```python
>>> d = date(2012, 12, 21)
>>> repr(d)
'datetime.date(2012, 12, 21)'
>>> print(repr(d))
datetime.date(2012, 12, 21)
>>> print(f'The date is: {d!r}')
The date is: datetime.date(2012, 12, 21)
>>>
```

在字符串格式化中，可以在值后面添加 `!r` 后缀，以生成其 `repr()` 值而不是正常的字符串转换。

## 4.6 一等对象

Python 中的所有对象都被称为*一等对象*（first-class）。这意味着所有可以被赋值给名称的对象也可以被当作数据处理。作为数据，对象可以存储在变量中，作为参数传递，从函数中返回，与其他对象进行比较，等等。例如，这里有一个包含两个值的简单字典：

```python
items = {
    'number' : 42,
    'text' : "Hello World"
}
```

通过向这个字典中添加一些更不寻常的项，可以看到对象的一等特性：

```python
items['func'] = abs
import math
items['mod'] = math
items['error'] = ValueError
nums = [1,2,3,4]
items['append'] = nums.append
```

在这个例子中，`items` 字典现在包含一个函数、一个模块、一个异常和一个另一个对象的方法。如果你愿意，可以使用对 `items` 的字典查找来代替原始名称，代码依然可以运行。例如：

```python
>>> items['func'](-45)  # 执行 abs(-45)
45
>>> items['mod'].sqrt(4)  # 执行 math.sqrt(4)
2.0
>>> try:
...	x = int('a lot')
... except items['error'] as e:  # 等同于 except ValueError as e
...	print("Couldn't convert")
...
Couldn't convert
>>> items['append'](100)  # 执行 nums.append(100)
>>> nums
[1, 2, 3, 4, 100]
>>>
```

Python 中一切皆为一等对象这一事实，初学者往往没有充分意识到。然而，它可以用来编写非常简洁且灵活的代码。

例如，假设你有一行文本，如 “ACME,100,490.10”，你想将其转换为一个经过适当类型转换的值列表。这里有一个巧妙的方法：创建一个类型列表（类型也是一等对象），并执行一些常见的列表处理操作：

```python
>>> line = 'ACME,100,490.10'
>>> column_types = [str, int, float]
>>> parts = line.split(',')
>>> row = [ty(val) for ty, val in zip(column_types, parts)]
>>> row
['ACME', 100, 490.1]
>>>
```

将函数或类放入字典中是消除复杂 `if-elif-else` 语句的一种常用技术。例如，如果你有这样的代码：

```python
if format == 'text':
    formatter = TextFormatter()
elif format == 'csv':
    formatter = CSVFormatter()
elif format == 'html':
    formatter = HTMLFormatter()
else:
    raise RuntimeError('Bad format')
```

你可以使用字典将其重写：

```python
_formats = {
    'text': TextFormatter,
    'csv': CSVFormatter,
    'html': HTMLFormatter
}

if format in _formats:
    formatter = _formats[format]()
else:
    raise RuntimeError('Bad format')
```

后一种形式也更加灵活，因为可以通过在字典中插入更多条目来添加新情况，而无需修改庞大的 `if-elif-else` 语句块。

## 4.7 使用 `None` 表示可选或缺失数据

有时程序需要表示一个可选值或缺失值。`None` 是专门为此目的保留的特殊实例。不显式返回值的函数会返回 `None`。`None` 也经常用作可选参数的默认值，这样函数就可以检测调用者是否实际为该参数传递了值。`None` 没有属性，在布尔表达式中求值为 `False`。

在内部，`None` 被存储为一个单例（singleton）——也就是说，解释器中只有一个 `None` 值。因此，测试一个值是否为 `None` 的常用方法是像这样使用 `is` 运算符：

```python
if value is None:
    statements
    ...
```

使用 `==` 运算符测试 `None` 同样可行，但不推荐这样做，并且可能会被代码检查工具标记为风格错误。

## 4.8 对象协议与数据抽象

大多数 Python 语言特性是由*协议*（protocols）定义的。考虑以下函数：

```python
def compute_cost(unit_price, num_units):
    return unit_price * num_units
```

现在，问问你自己：允许什么样的输入？答案简单得令人惊讶——所有输入都被允许！乍一看，这个函数似乎只适用于数字：

```python
>>> compute_cost(1.25, 50)
62.5
>>>
```

的确，它的运行符合预期。然而，该函数的适用范围广得多。你可以使用分数或小数等特殊数字：

```python
>>> from fractions import Fraction
>>> compute_cost(Fraction(5, 4), 50)
Fraction(125, 2)
>>> from decimal import Decimal
>>> compute_cost(Decimal('1.25'), Decimal('50'))
Decimal('62.50')
>>>
```

不仅如此，该函数还适用于来自 `numpy` 等包的数组和其他复杂结构。例如：

```python
>>> import numpy as np
>>> prices = np.array([1.25, 2.10, 3.05])
>>> units = np.array([50, 20, 25])
>>> compute_cost(prices, units)
array([62.5 , 42. , 76.25])
>>>
```

该函数甚至可能以出人意料的方式运行：

```python
>>> compute_cost('a lot', 10)
'a lota lota lota lota lota lota lota lot'
>>>
```

然而，某些类型的组合会失败：

```python
>>> compute_cost(Fraction(5, 4), Decimal('50'))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in compute_cost
TypeError: unsupported operand type(s) for *: 'Fraction' and 'decimal.Decimal'
>>>
```



与静态语言的编译器不同，Python 不会提前验证程序的正确行为。相反，对象的行为是由一个动态过程决定的，该过程涉及所谓的“特殊”或“魔法”方法的调度。这些特殊方法的名称总是以双下划线（`__`）开头并以双下划线结尾。这些方法在程序执行时由解释器自动触发。例如，操作 `x * y` 是通过方法 `x.__mul__(y)` 执行的。这些方法及其对应的运算符是硬编码的。任何给定对象的行为完全取决于它所实现的特殊方法集。

接下来的几个章节将描述与不同类别的核心解释器功能相关的特殊方法。这些类别有时被称为“协议”。一个对象（包括用户定义的类）可以定义这些功能的任意组合，以使对象表现出不同的行为。

## 4.9 对象协议

表 4.1 中的方法与对象的整体管理相关。这包括对象的创建、初始化、销毁和表示。

### 表 4.1 对象管理方法

| 方法 | 描述 |
|:---|:---|
| `__new__(cls [, *args [, **kwargs]])` | 用于创建新实例的静态方法。 |
| `__init__(self [, *args [, **kwargs]])` | 在新实例创建后被调用，用于初始化实例。 |
| `__del__(self)` | 在实例被销毁时被调用。 |
| `__repr__(self)` | 创建字符串表示形式。 |

`__new__()` 和 `__init__()` 方法共同用于创建和初始化实例。当通过调用 `SomeClass(args)` 创建对象时，它被转换为以下步骤：

```python
x = SomeClass.__new__(SomeClass, args)
if isinstance(x, SomeClass):
    x.__init__(args)
```

通常，这些步骤在幕后处理，你不需要担心。类中最常用的实现方法是 `__init__()`。使用 `__new__()` 几乎总是意味着存在与实例创建相关的高级魔法（例如，它用于想要绕过 `__init__()` 的类方法，或用于某些创建型设计模式，如单例或缓存）。`__new__()` 的实现不一定需要返回该类的实例——如果不是，则在创建时随后对 `__init__()` 的调用将被跳过。

`__del__()` 方法在实例即将被垃圾回收时被调用。该方法仅在实例不再被使用时被调用。请注意，语句 `del x` 仅减少实例的引用计数，并不一定会导致调用此函数。除非实例在销毁时需要执行额外的资源管理步骤，否则几乎从不定义 `__del__()`。

`__repr__()` 方法由内置的 `repr()` 函数调用，它创建对象的字符串表示，这对于调试和打印非常有用。这也是在交互式解释器中检查变量时，负责创建你看到的数值输出的方法。惯例是 `__repr__()` 返回一个表达式字符串，该字符串可以使用 `eval()` 计算以重新创建对象。例如：

```python
a = [2, 3, 4, 5]   # 创建一个列表
s = repr(a)        # s = '[2, 3, 4, 5]'
b = eval(s)        # 将 s 变回列表
```

如果无法创建字符串表达式，惯例是 `__repr__()` 返回一个形如 `<...message...>` 的字符串，如下所示：

```python
f = open('foo.txt')
a = repr(f)
# a = "<_io.TextIOWrapper name='foo.txt' mode='r' encoding='UTF-8'>"
```

## 4.10 数字协议

表 4.2 列出了对象为了提供数学运算必须实现的特殊方法。

### 表 4.2 数学运算方法

| 方法 | 运算 |
|:---|:---|
| `__add__(self, other)` | `self + other` |
| `__sub__(self, other)` | `self - other` |
| `__mul__(self, other)` | `self * other` |
| `__truediv__(self, other)` | `self / other` |
| `__floordiv__(self, other)` | `self // other` |
| `__mod__(self, other)` | `self % other` |
| `__matmul__(self, other)` | `self @ other` |
| `__divmod__(self, other)` | `divmod(self, other)` |
| `__pow__(self, other [, modulo])` | `self ** other, pow(self, other, modulo)` |
| `__lshift__(self, other)` | `self << other` |
| `__rshift__(self, other)` | `self >> other` |
| `__and__(self, other)` | `self & other` |
| `__or__(self, other)` | `self \| other` |
| `__xor__(self, other)` | `self ^ other` |
| `__radd__(self, other)` | `other + self` |
| `__rsub__(self, other)` | `other - self` |
| `__rmul__(self, other)` | `other * self` |
| `__rtruediv__(self, other)` | `other / self` |
| `__rfloordiv__(self, other)` | `other // self` |
| `__rmod__(self, other)` | `other % self` |
| `__rmatmul__(self, other)` | `other @ self` |
| `__rdivmod__(self, other)` | `divmod(other, self)` |
| `__rpow__(self, other)` | `other ** self` |
| `__rlshift__(self, other)` | `other << self` |
| `__rrshift__(self, other)` | `other >> self` |
| `__rand__(self, other)` | `other & self` |
| `__ror__(self, other)` | `other \| self` |
| `__rxor__(self, other)` | `other ^ self` |
| `__iadd__(self, other)` | `self += other` |
| `__isub__(self, other)` | `self -= other` |
| `__imul__(self, other)` | `self *= other` |
| `__itruediv__(self, other)` | `self /= other` |
| `__ifloordiv__(self, other)` | `self //= other` |
| `__imod__(self, other)` | `self %= other` |
| `__imatmul__(self, other)` | `self @= other` |
| `__ipow__(self, other)` | `self **= other` |
| `__iand__(self, other)` | `self &= other` |
| `__ior__(self, other)` | `self \|= other` |
| `__ixor__(self, other)` | `self ^= other` |
| `__ilshift__(self, other)` | `self <<= other` |
| `__irshift__(self, other)` | `self >>= other` |
| `__neg__(self)` | `-self` |
| `__pos__(self)` | `+self` |
| `__invert__(self)` | `~self` |
| `__abs__(self)` | `abs(self)` |
| `__round__(self, n)` | `round(self, n)` |
| `__floor__(self)` | `math.floor(self)` |
| `__ceil__(self)` | `math.ceil(self)` |
| `__trunc__(self)` | `math.trunc(self)` |

当遇到像 `x + y` 这样的表达式时，解释器会调用 `x.__add__(y)` 或 `y.__radd__(x)` 方法的组合来执行运算。初始选择是在所有情况下都尝试 `x.__add__(y)`，除非在 `y` 恰好是 `x` 的子类型这一特殊情况下，此时将执行 `y.__radd__(x)`。

首先。如果初始方法失败并返回 `NotImplemented`，则会尝试使用反向操作数调用，例如 `y.__radd__(x)`。如果第二次尝试也失败，则整个操作失败。这里有一个示例：

```python
>>> a = 42          # int
>>> b = 3.7         # float
>>> a.__add__(b)
NotImplemented
>>> b.__radd__(a)
45.7
>>>
```

这个例子看起来可能令人惊讶，但它反映了一个事实：整数实际上并不了解浮点数。然而，浮点数知道整数——因为从数学上讲，整数是浮点数的一种特殊类型。因此，反向操作数产生了正确的结果。

`__iadd__()`、`__isub__()` 等方法用于支持原位算术运算符，如 `a += b` 和 `a -= b`（也称为增强赋值）。这些运算符与标准算术方法之间有所区别，因为原位运算符的实现可能能够提供某些自定义或性能优化。例如，如果对象未被共享，则可以直接修改对象的值，而无需为结果分配一个新创建的对象。如果原位运算符未定义，则像 `a += b` 这样的操作将改为使用 `a = a + b` 来求值。

没有可以用来定义逻辑 `and`、`or` 和 `not` 运算符行为的方法。`and` 和 `or` 运算符实现了短路求值，即如果最终结果已经可以确定，则停止求值。例如：

```python
>>> True or 1 / 0         # 不会对 1/0 进行求值
True
```

这种涉及未求值子表达式的行为无法使用普通函数或方法的求值规则来表达。因此，没有用于重新定义它的协议或方法集。相反，它在 Python 自身的底层实现中作为一个特例来处理。

## 4.11 比较协议

对象可以通过多种方式进行比较。最基本的检查是使用 `is` 运算符进行身份检查。例如，`a is b`。身份检查不考虑对象内部存储的值，即使它们恰好相同。例如：

```python
>>> a = [1, 2, 3]
>>> b = a
>>> a is b
True
>>> c = [1, 2, 3]
>>> a is c
False
>>>
```

`is` 运算符是 Python 的内部组成部分，无法被重新定义。对象的所有其他比较都通过表 4.3 中的方法实现。

### 表 4.3 实例比较和哈希方法

| 方法 | 描述 |
|--------|-------------|
| `__bool__(self)` | 用于真值测试，返回 `False` 或 `True` |
| `__eq__(self, other)` | `self == other` |
| `__ne__(self, other)` | `self != other` |
| `__lt__(self, other)` | `self < other` |
| `__le__(self, other)` | `self <= other` |
| `__gt__(self, other)` | `self > other` |
| `__ge__(self, other)` | `self >= other` |
| `__hash__(self)` | 计算整数哈希索引 |

如果存在 `__bool__()` 方法，它将被用于在对象作为条件或条件表达式的一部分进行测试时确定其真值。例如：

```python
if a:
    # 执行 a.__bool__()
    ...
else:
    ...
```

如果 `__bool__()` 未定义，则使用 `__len__()` 作为后备方案。如果 `__bool__()` 和 `__len__()` 都未定义，则对象被简单地认为是 `True`。

`__eq__()` 方法用于确定 `==` 和 `!=` 运算符使用的基本相等性。`__eq__()` 的默认实现使用 `is` 运算符通过身份来比较对象。如果存在 `__ne__()` 方法，它可以用于为 `!=` 实现特殊处理，但只要定义了 `__eq__()`，通常就不需要它。

顺序由关系运算符（`<`、`>`、`<=` 和 `>=`）使用 `__lt__()` 和 `__gt__()` 等方法来确定。与其他数学运算一样，求值规则较为微妙。为了计算 `a < b`，解释器首先会尝试执行 `a.__lt__(b)`，除非 `b` 是 `a` 的子类型。在这种特定情况下，将执行 `b.__gt__(a)`。如果初始方法未定义或返回 `NotImplemented`，解释器将尝试反向比较，调用 `b.__gt__(a)`。类似的规则也适用于 `<=` 和 `>=` 等运算符。例如，计算 `<=` 首先尝试计算 `a.__le__(b)`。如果未实现，则尝试 `b.__ge__(a)`。

每个比较方法接收两个参数，并允许返回任何类型的值，包括布尔值、列表或任何其他 Python 类型。例如，一个数值包可能会利用这一点对两个矩阵进行逐元素比较，并返回一个包含结果的矩阵。如果无法进行比较，这些方法应返回内置对象 `NotImplemented`。这与 `NotImplementedError` 异常不同。例如：

```python
>>> a = 42		# int
>>> b = 52.3	# float
>>> a.__lt__(b)
NotImplemented
>>> b.__gt__(a)
True
>>>
```

有序对象不需要实现表 4.3 中的所有比较操作。如果你希望能够对对象进行排序或使用 `min()` 或 `max()` 等函数，那么必须至少定义 `__lt__()`。如果你正在为用户定义类添加比较运算符，`functools` 模块中的 `@total_ordering` 类装饰器可能会有所帮助。只要你至少实现了 `__eq__()` 和其他任何一个比较方法，它就可以生成所有其他方法。

`__hash__()` 方法定义在需要放入集合或用作映射（字典）键的实例上。返回的值是一个整数，对于比较相等的两个实例，该值应该是相同的。此外，`__eq__()` 应该始终与 `__hash__()` 一起定义，因为这两个方法协同工作。`__hash__()` 返回的值通常被用作各种数据结构的内部实现细节。然而，两个不同的对象可能会有相同的哈希值。因此，`__eq__()` 对于解决潜在的冲突是必要的。

## 4.12 转换协议

有时，你必须将对象转换为内置类型，如字符串或数字。为此可以定义表 4.4 中的方法。

### 表 4.4 转换方法

| 方法 | 描述 |
| --- | --- |
| `__str__(self)` | 转换为字符串 |
| `__bytes__(self)` | 转换为字节 |
| `__format__(self, format_spec)` | 创建格式化表示 |
| `__bool__(self)` | `bool(self)` |
| `__int__(self)` | `int(self)` |
| `__float__(self)` | `float(self)` |
| `__complex__(self)` | `complex(self)` |
| `__index__(self)` | 转换为整数索引 `[self]` |

`__str__()` 方法由内置的 `str()` 函数以及与打印相关的函数调用。`__format__()` 方法由 `format()` 函数或字符串的 `format()` 方法调用。`format_spec` 参数是一个包含格式规范的字符串。该字符串与 `format()` 的 `format_spec` 参数相同。

例如：

```python
f'{x:spec}'  # 调用 x.__format__('spec')
format(x, 'spec')  # 调用 x.__format__('spec')
'x is {0:spec}'.format(x)  # 调用 x.__format__('spec')
```

格式规范的语法是任意的，可以根据每个对象的需要进行自定义。不过，内置类型使用了一套标准的约定。关于字符串格式化的更多信息（包括说明符的一般格式）可以在第 9 章中找到。

如果将一个实例传递给 `bytes()`，`__bytes__()` 方法用于创建字节表示。并非所有类型都支持字节转换。

数值转换 `__bool__()`、`__int__()`、`__float__()` 和 `__complex__()` 预期会产生对应内置类型的值。

Python 绝不会使用这些方法进行隐式类型转换。因此，即使对象 `x` 实现了 `__int__()` 方法，表达式 `3 + x` 仍然会产生 `TypeError`。执行 `__int__()` 的唯一方法是通过显式使用 `int()` 函数。



`__index__()` 方法在对象被用于需要整数值的操作时执行整数转换。这包括序列操作中的索引。例如，如果 `items` 是一个列表，执行 `items[x]` 这样的操作，如果 `x` 不是整数，将尝试执行 `items[x.__index__()]`。`__index__()` 还用于各种基数转换，如 `oct(x)` 和 `hex(x)`。

## 4.13 容器协议

表 4.5 中的方法被那些想要实现各种容器（列表、字典、集合等）的对象使用。

表 4.5 容器方法

| 方法 | 描述 |
|--------|-------------|
| `__len__(self)` | 返回 `self` 的长度 |
| `__getitem__(self, key)` | 返回 `self[key]` |
| `__setitem__(self, key, value)` | 设置 `self[key] = value` |
| `__delitem__(self, key)` | 删除 `self[key]` |
| `__contains__(self, obj)` | `obj` in `self` |

```python
a = [1, 2, 3, 4, 5, 6]
len(a)                    # a.__len__()
x = a[2]                  # x = a.__getitem__(2)
a[1] = 7                  # a.__setitem__(1,7)
del a[2]                  # a.__delitem__(2)
5 in a                    # a.__contains__(5)
```

内置的 `len()` 函数会调用 `__len__()` 方法以返回一个非负的长度。除非同时定义了 `__bool__()` 方法，否则该函数还决定了真值。

对于访问单个项目，`__getitem__()` 方法可以通过键值返回一个项目。键可以是任何 Python 对象，但对于列表和数组等有序序列，键通常预期为整数。`__setitem__()` 方法为元素赋值。每当对单个元素应用 `del` 操作时，就会调用 `__delitem__()` 方法。`__contains__()` 方法用于实现 `in` 运算符。

诸如 `x = s[i:j]` 的切片操作也是使用 `__getitem__()`、`__setitem__()` 和 `__delitem__()` 实现的。对于切片，一个特殊的 `slice` 实例被作为键传递。该实例具有描述所请求切片范围的属性。例如：

```python
a = [1,2,3,4,5,6]
x = a[1:5]                # x = a.__getitem__(slice(1, 5, None))
a[1:3] = [10,11,12]       # a.__setitem__(slice(1, 3, None), [10, 11, 12])
del a[1:4]               # a.__delitem__(slice(1, 4, None))
```

Python 的切片功能比许多程序员意识到的要强大得多。例如，以下扩展切片的变体都得到了支持，并且在处理矩阵和数组等多维数据结构时可能非常有用：

```python
a = m[0:100:10]            # 步长切片 (step=10)
b = m[1:10, 3:20]          # 多维切片
c = m[0:100:10, 50:75:5]   # 带有步长的多维切片
m[0:5, 5:10] = n           # 扩展切片赋值
del m[:10, 15:]            # 扩展切片删除
```

扩展切片的每个维度的通用格式为 `i:j[:stride]`，其中 `stride`（步长）是可选的。与普通切片一样，你可以省略切片每个部分的起始值或结束值。

此外，`Ellipsis`（写作 `...`）可用于表示扩展切片中任意数量的尾随或前导维度：

```python
a = m[..., 10:20]       # 使用 Ellipsis 的扩展切片访问
m[10:20, ...] = n
```

在使用扩展切片时，`__getitem__()`、`__setitem__()` 和 `__delitem__()` 方法分别实现访问、修改和删除。但是，传递给这些方法的值不再是一个整数，而是一个包含 `slice` 或 `Ellipsis` 对象组合的元组。例如，

```python
a = m[0:10, 0:100:5, ...]
```

会按如下方式调用 `__getitem__()`：

```python
a = m.__getitem__((slice(0,10,None), slice(0,100,5), Ellipsis))
```

Python 的字符串、元组和列表目前提供对扩展切片的部分支持。Python 及其标准库的没有任何部分使用多维切片或 `Ellipsis`。这些功能纯粹是为第三方库和框架保留的。你最常见到它们被使用的地方可能是像 `numpy` 这样的库中。

## 4.14 迭代协议

如果一个实例 `obj` 支持迭代，它会提供一个返回迭代器的 `obj.__iter__()` 方法。而迭代器 `iter` 实现了一个单一的方法 `iter.__next__()`，该方法返回下一个对象，或者抛出 `StopIteration` 以发出迭代结束的信号。这些方法被 `for` 语句的实现以及其他隐式执行迭代的操作所使用。例如，语句 `for x in s` 是通过执行以下步骤完成的：

```python
_iter = s.__iter__()
while True:
    try:
        x = _iter.__next__()
    except StopIteration:
        break
    # 执行 for 循环体中的语句
    ...
```

如果对象实现了 `__reversed__()` 特殊方法，它可以选择性地提供一个反向迭代器。该方法应返回一个与普通迭代器接口相同的迭代器对象（即具有在迭代结束时抛出 `StopIteration` 的 `__next__()` 方法）。此方法被内置的 `reversed()` 函数使用。

例如：

```python
>>> for x in reversed([1,2,3]):
...     print(x)
3
2
1
>>>
```

一种常见的迭代实现技术是使用涉及 `yield` 的生成器函数。例如：

```python
class FRange:
    def __init__(self, start, stop, step):
        self.start = start
        self.stop = stop
        self.step = step

    def __iter__(self):
        x = self.start
        while x < self.stop:
            yield x
            x += self.step

# 使用示例：
nums = FRange(0.0, 1.0, 0.1)
for x in nums:
    print(x)         # 0.0, 0.1, 0.2, 0.3, ...
```

这种方法之所以有效，是因为生成器函数本身就符合迭代协议。通过这种方式实现迭代器会简单一些，因为你只需要关注 `__iter__()` 方法，其余的迭代机制已由生成器提供。

## 4.15 属性协议

表 4.6 中的方法分别使用点 (`.`) 运算符和 `del` 运算符来读取、写入和删除对象的属性。

### 表 4.6 属性访问方法

| 方法 | 描述 |
| :--- | :--- |
| `__getattribute__(self, name)` | 返回属性 `self.name` |
| `__getattr__(self, name)` | 如果通过 `__getattribute__()` 未找到，则返回属性 `self.name` |
| `__setattr__(self, name, value)` | 设置属性 `self.name = value` |
| `__delattr__(self, name)` | 删除属性 `del self.name` |

每当访问属性时，都会调用 `__getattribute__()` 方法。如果找到了该属性，则返回其值。否则，将调用 `__getattr__()` 方法。`__getattr__()` 的默认行为是抛出 `AttributeError` 异常。在设置属性时总是会调用 `__setattr__()` 方法，在删除属性时总是会调用 `__delattr__()` 方法。

这些方法相当粗犷——因为它们允许一个类型完全重新定义所有属性的属性访问。用户定义类可以定义属性（`properties`）和描述符（`descriptors`），从而实现对属性访问更精细的控制。这将在第 7 章中进一步讨论。

## 4.16 函数协议

对象可以通过提供 `__call__()` 方法来模拟函数。如果一个对象 `x` 提供了此方法，它就可以像函数一样被调用。也就是说，`x(arg1, arg2, ...)` 会调用 `x.__call__(arg1, arg2, ...)`。

许多内置类型支持函数调用。例如，类型实现了 `__call__()` 以创建新实例。绑定方法实现 `__call__()` 以将 `self` 参数传递给实例方法。像 `functools.partial()` 这样的库函数也会创建模拟函数的对象。

## 4.17 上下文管理器协议

`with` 语句允许一系列语句在被称为上下文管理器的实例控制下执行。通用语法如下：

```python
with context [ as var]:
    statements
```

此处所示的上下文对象预期实现表 4.7 中列出的方法。

### 表 4.7 上下文管理器方法

| 方法 | 描述 |
| :--- | :--- |
| `__enter__(self)` | 在进入新上下文时调用。返回值被放置在 `with` 语句 `as` 指定符列出的变量中。 |
| `__exit__(self, type, value, tb)` | 在离开上下文时调用。如果发生了异常，`type`、`value` 和 `tb` 分别包含异常类型、值和回溯信息。 |

当 `with` 语句执行时，会调用 `__enter__()` 方法。该方法返回的值被放入由可选的 `as var` 指定符指定的变量中。一旦控制流离开与 `with` 语句相关联的语句块，就会调用 `__exit__()` 方法。作为参数，如果抛出了异常，`__exit__()` 将接收当前的异常类型、值和回溯。如果没有处理错误，这三个值都将被设置为 `None`。`__exit__()` 方法应返回 `True` 或 `False`，以指示抛出的异常是否被处理。如果返回 `True`，任何待处理的异常将被清除，程序执行将从 `with` 块之后的第一个语句正常继续。

上下文管理接口的主要用途是允许对涉及系统状态（如打开的文件、网络连接和锁）的对象进行简化的资源控制。通过实现此接口，对象可以在执行时安全地清理资源。

留下一个对象正在被使用的上下文。更多详情请参阅第 3 章。

## 4.18 结语：关于 Pythonic

一个经常被提及的设计目标是编写“Pythonic”的代码”。这可以意味着很多事情，但基本上它鼓励你遵循 Python 社区公认的惯用法。这意味着需要了解 Python 关于容器、可迭代对象、资源管理等方面的协议。许多最受欢迎的 Python 框架都使用这些协议来提供良好的用户体验。你也应该为此而努力。

在不同的协议中，有三个由于被广泛使用而值得特别关注。一是使用 `__repr__()` 方法创建合适的对象表示。Python 程序经常在交互式 REPL 中进行调试和实验。使用 `print()` 或日志库来输出对象也很常见。如果你能让观察对象状态变得简单，那么所有这些事情都会变得更容易。

其次，遍历数据是最常见的编程任务之一。如果你要执行此操作，你应该让你的代码与 Python 的 `for` 语句协作。Python 的许多核心部分和标准库都被设计为与可迭代对象协作。通过以常规方式支持迭代，你将自动获得大量额外的功能，并且你的代码对于其他程序员来说将是非常直观的。

最后，对于那些语句被夹在某种启动和拆除步骤之间的常见编程模式——例如，打开和关闭资源、获取和释放锁、订阅和取消订阅等等——请使用上下文管理器和 `with` 语句。

# 5. 函数

函数是大多数 Python 程序的基础构建块。本章描述了函数定义、函数应用、作用域规则、闭包、装饰器以及其他函数式编程特性。本章将特别关注与函数相关的不同编程惯用法、求值模型和模式。

## 5.1 函数定义

函数使用 `def` 语句定义：

```python
def add(x, y):
    return x + y
```

函数定义的第一部分指定了函数名称和代表输入值的参数名称。函数的主体是一系列在函数被调用或应用时执行的语句。你通过编写函数名，后跟括号内包含的参数来将函数应用于参数：`a = add(3, 4)`。参数在执行函数体之前会按照从左到右的顺序被完全求值。例如，`add(1+1, 2+2)` 在调用函数之前首先被简化为 `add(2, 4)`。这被称为 *应用顺序求值 (applicative evaluation order)*。参数的顺序和数量必须与函数定义中给出的参数匹配。如果存在不匹配，则会引发 `TypeError` 异常。调用函数的结构（例如所需参数的数量）被称为函数的调用签名。

## 5.2 默认参数

你可以通过在函数定义中赋值，为函数参数附加默认值。例如：

```python
def split(line, delimiter=','):
    statements
```

当一个函数定义了一个具有默认值的参数时，该参数以及随后的所有参数都是可选的。在任何具有默认值的参数之后，不能指定没有默认值的参数。

默认参数值在函数首次定义时被求值一次，而不是在每次调用函数时求值。如果使用可变对象作为默认值，这通常会导致令人惊讶的行为：

```python
def func(x, items=[]):
    items.append(x)
    return items

func(1)         # returns [1]
func(2)         # returns [1, 2]
func(3)         # returns [1, 2, 3]
```

请注意默认参数是如何保留之前调用所做修改的。为了防止这种情况，更好的做法是使用 `None` 并且

字典的 `pop()` 方法会从字典中删除一个项目，如果该项目未定义，则返回一个可能的默认值。本代码中使用的 `parms.pop('fgcolor', 'black')` 表达式模拟了带有默认值的关键字参数的行为。

## 5.6 接收所有输入的函数

通过同时使用 `*` 和 `**`，你可以编写一个能够接收任何参数组合的函数。位置参数将作为元组（`tuple`）传递，而关键字参数将作为字典（`dictionary`）传递。例如：

```python
# 接收可变数量的位置参数或关键字参数
def func(*args, **kwargs):
    # args 是位置参数的元组
    # kwargs 是关键字参数的字典
    ...
```

这种 `*args` 和 `**kwargs` 的结合使用通常用于编写包装器（`wrappers`）、装饰器（`decorators`）、代理（`proxies`）以及类似的函数。例如，假设你有一个函数用来解析从可迭代对象中获取的文本行：

```python
def parse_lines(lines, separator=',', types=(), debug=False):
    for line in lines:
        ...
        statements
        ...
```

现在，假设你想创建一个特殊情况的函数，改为解析由文件名指定的文件的内容。为此，你可以这样写：

```python
def parse_file(filename, *args, **kwargs):
    with open(filename, 'rt') as file:
        return parse_lines(file, *args, **kwargs)
```

这种方法的优点是 `parse_file()` 函数不需要了解 `parse_lines()` 的任何参数信息。它接收调用者提供的任何额外参数并将其转发。这也简化了 `parse_file()` 函数的维护。例如，如果 `parse_lines()` 添加了新参数，这些参数也会在 `parse_file()` 函数中神奇地生效。

## 5.7 仅限位置参数

许多 Python 内置函数仅接受通过位置传递的参数。在各种帮助工具和 IDE 显示的函数调用签名中，你会看到斜杠 (`/`) 表示这一点。例如，你可能会看到类似 `func(x, y, /)` 的形式。这意味着出现在斜杠之前的所有参数只能通过位置来指定。因此，你可以调用 `func(2, 3)`，但不能调用 `func(x=2, y=3)`。为了完整性，这种语法也可以用于定义函数。例如，你可以写成：

```python
def func(x, y, /):
    pass

func(1, 2)        # 正确
func(1, y=2)     # 错误
```

这种定义形式在代码中很少见，因为它直到 Python 3.8 才开始支持。然而，它可以成为避免参数名称之间潜在名称冲突的一种有效方法。例如，考虑以下代码：



```python
import time

def after(seconds, func, /, *args, **kwargs):
    time.sleep(seconds)
    return func(*args, **kwargs)

def duration(*, seconds, minutes, hours):
    return seconds + 60 * minutes + 3600 * hours

after(5, duration, seconds=20, minutes=3, hours=2)
```

在这段代码中，`seconds` 被作为关键字参数传递，但它是打算传递给传递给 `after()` 的 `duration` 函数使用的。在 `after()` 中使用仅限位置参数，防止了与首先出现的 `seconds` 参数产生名称冲突。

## 5.8 名称、文档字符串和类型提示

函数的标准命名约定是使用小写字母，并使用下划线（`_`）作为单词分隔符——例如，使用 `read_data()` 而不是 `readData()`。如果一个函数不打算被直接使用（因为它是辅助函数或某种内部实现细节），其名称通常会在前面加上一个下划线——例如 `_helper()`。不过，这些仅仅是约定。只要名称是有效的标识符，你可以随意为函数命名。

函数的名称可以通过 `__name__` 属性获取。这在调试时有时很有用。

```python
>>> def square(x):
...     return x * x
...
>>> square.__name__
'square'
>>>
```

函数的第一个语句通常是一个描述其用法的文档字符串（documentation string）。例如：

```python
def factorial(n):
    '''
    计算 n 的阶乘。例如：

    >>> factorial(6)
    120
    >>>
    '''

    if n <= 1:
        return 1
    else:
        return n*factorial(n-1)
```

文档字符串存储在函数的 `__doc__` 属性中。IDE 经常访问它以提供交互式帮助。

函数还可以使用类型提示（type hints）进行注解。例如：

```python
def factorial(n: int) -> int:
    if n <= 1:
        return 1
    else:
        return n * factorial(n - 1)
```

类型提示不会改变函数的求值方式。也就是说，提示的存在不会带来性能提升或额外的运行时错误检查。这些提示仅存储在函数的 `__annotations__` 属性中，该属性是一个将参数名称映射到所提供提示的字典。IDE 和代码检查器等第三方工具可能会将这些提示用于各种目的。

有时你会看到类型提示附加在函数内部的局部变量上。例如：

```python
def factorial(n:int) -> int:
    result: int = 1    # 类型提示的局部变量
    while n > 1:
        result *= n
        n -= 1
    return result
```

此类提示会被解释器完全忽略。它们不会被检查、存储甚至求值。再次强调，提示的目的是帮助第三方代码检查工具。除非你正在积极使用利用这些提示的代码检查工具，否则不建议在函数中添加类型提示。类型提示很容易指定错误——而且，除非你使用检查工具，否则错误将一直未被发现，直到有人决定在你的代码上运行类型检查工具。

## 5.9 函数应用与参数传递

当函数被调用时，函数参数是与传递的输入对象绑定的局部名称。Python“原样”地将提供的对象传递给函数，不进行任何额外的复制。如果传递的是可变对象（如列表或字典），则需要小心。如果进行了修改，这些修改将反映在原始对象中。这里有一个例子：

```python
def square(items):
    for i, x in enumerate(items):
        items[i] = x * x    # 原地修改 items

a = [1, 2, 3, 4, 5]
square(a)                 # 将 a 改变为 [1, 4, 9, 16, 25]
```

那些修改其输入值或在后台改变程序其他部分状态的函数被认为具有“副作用（side effects）”。通常情况下，最好避免副作用。随着程序规模和复杂度的增加，它们可能成为微妙编程错误的来源——从阅读函数调用中可能无法明显看出一个函数是否具有副作用。此类函数在涉及线程和并发的程序中交互效果较差，因为副作用通常需要由锁来保护。

区分修改对象和重新分配变量名非常重要。考虑这个函数：

```python
def sum_squares(items):
    items = [x*x for x in items]   # 重新分配 "items" 名称
    return sum(items)

a = [1, 2, 3, 4, 5]
result = sum_squares(a)
print(a)                    # [1, 2, 3, 4, 5]   (未改变)
```

在这个例子中，看起来 `sum_squares()` 函数可能会覆盖传递的 `items` 变量。是的，局部的 `items` 标签被重新分配给了一个新值。但原始输入值（`a`）并没有被该操作改变。相反，局部变量名 `items` 被绑定到了一个完全不同的对象上——即内部列表推导式的结果。分配变量名与修改对象之间存在区别。当你将一个值分配给一个名称时，你并不是在覆盖已经存在于那里的对象，而只是将该名称重新分配给另一个对象。

从风格上讲，具有副作用的函数通常返回 `None` 作为结果。例如，考虑列表的 `sort()` 方法：

```python
>>> items = [10, 3, 2, 9, 5]
>>> items.sort()        # Observe: no return value
>>> items
[2, 3, 5, 9, 10]
>>>
```

`sort()` 方法对列表项执行就地（in-place）排序。它不返回任何结果。缺乏返回值是一个强烈的信号，表明该操作产生了副作用——在这个例子中，列表中的元素被重新排列了。

有时你可能已经拥有一个序列或映射中的数据，并希望将其传递给函数。为此，你可以在函数调用中使用 `*` 和 `**`。例如：

```python
def func(x, y, z):
    ...

s = (1, 2, 3)
# 将序列作为参数传递
result = func(*s)

# 将映射作为关键字参数传递
d = { 'x':1, 'y':2, 'z':3 }
result = func(**d)
```

你可能会从多个来源获取数据，甚至显式地提供部分参数，只要函数获得了所有必需的参数、没有重复且调用签名完全匹配，这一切都能正常工作。你甚至可以在同一个函数调用中多次使用 `*` 和 `**`。如果你缺失了一个参数或为某个参数指定了重复的值，将会触发错误。Python 绝不会允许你用不满足其签名的参数来调用函数。

## 5.10 返回值

`return` 语句从函数中返回一个值。如果没有指定值或省略了 `return` 语句，则返回 `None`。要返回多个值，请将它们放入一个元组中：

```python
def parse_value(text):
    '''
    将形式为 name=val 的文本拆分为 (name, val)
    '''
    parts = text.split('=', 1)
    return (parts[0].strip(), parts[1].strip())
```

在元组中返回的值可以解包到独立的变量中：

```python
name, value = parse_value('url=http://www.python.org')
```

有时可以使用命名元组（named tuples）作为替代方案：

```python
from typing import NamedTuple

class ParseResult(NamedTuple):
    name: str
    value: str

def parse_value(text):
    '''
    将形式为 name=val 的文本拆分为 (name, val)
    '''
    parts = text.split('=', 1)
    return ParseResult(parts[0].strip(), parts[1].strip())
```

命名元组的工作方式与普通元组相同（你可以执行所有相同的操作和解包），但你还可以使用命名属性来引用返回的值：

```python
r = parse_value('url=http://www.python.org')
print(r.name, r.value)
```

## 5.11 错误处理

上一节中 `parse_value()` 函数的一个问题是错误处理。如果输入文本格式错误且无法返回正确结果，应该采取什么行动？

一种方法是将结果视为可选的——也就是说，函数要么通过返回答案来工作，要么返回 `None`（通常用于表示缺失值）。例如，可以将函数修改如下：

```python
def parse_value(text):
    parts = text.split('=', 1)
    if len(parts) == 2:
        return ParseResult(parts[0].strip(), parts[1].strip())
    else:
        return None
```

在这种设计下，检查可选结果的责任落在了调用者身上：

```python
result = parse_value(text)
if result:
    name, value = result
```

或者，在 Python 3.8+ 中，可以更紧凑地写成：

```python
if result := parse_value(text):
    name, value = result
```

与其返回 `None`，你也可以通过引发异常将格式错误的文本视为错误。例如：

```python
def parse_value(text):
    parts = text.split('=', 1)
    if len(parts) == 2:
        return ParseResult(parts[0].strip(), parts[1].strip())
    else:
        raise ValueError('Bad value')
```

在这种情况下，调用者可以选择使用 `try-except` 来处理错误值。例如：

```python
try:
    name, value = parse_value(text)
    ...
except ValueError:
    ...
```

是否使用异常的选择并不总是那么明确。作为一般原则，异常是处理异常结果更常用的方式。然而，如果异常频繁发生，其开销也会很大。如果你在编写对性能有要求的代码，返回 `None`、`False`、`-1` 或其他特殊值来表示失败可能会更好。

## 5.12 作用域规则

每次函数执行时，都会创建一个局部命名空间。这个命名空间是一个环境，其中包含了函数参数的名称和值，以及在函数体内部定义的所有变量。名称的绑定在函数定义时就已预先确定，所有在函数体内部赋值的名称都被绑定到局部环境中。所有在函数体中使用但未赋值的其他名称（自由变量）则在全局命名空间中动态查找，全局命名空间始终是定义该函数的封闭模块。

在函数执行过程中可能会出现两种与名称相关的错误。在全局环境中查找未定义的自由变量名称会导致 `NameError` 异常。查找尚未赋值的局部变量会导致 `UnboundLocalError` 异常。后者通常是控制流 bug 导致的。例如：

```python
def func(x):
    if x > 0:
        y = 42
    return x + y     # 如果条件为假，y 未被赋值

func(10)          # 返回 52
func(-10)         # UnboundLocalError: y referenced before assignment
```

`UnboundLocalError` 有时也是由于粗心地使用就地赋值运算符引起的。诸如 `n += 1` 的语句被处理为 `n = n + 1`。如果在 `n` 被赋予初始值之前使用，它将失败。

```python
def func():
    n += 1    # 错误: UnboundLocalError
```

必须强调的是，变量名称永远不会改变它们的作用域——它们要么是全局变量，要么是局部变量，这在函数定义时就决定了。这里有一个例子来说明这一点：

```python
x = 42
def func():
    print(x)        # 失败。UnboundLocalError
    x = 13

func()
```

在这个例子中，看起来 `print()` 函数应该输出全局变量 `x` 的值。然而，后面出现的 `x` 赋值操作将 `x` 标记为了局部变量。该错误是由于访问了一个尚未赋值的局部变量而导致的。

如果你移除 `print()` 函数，你得到的代码看起来像是在重新赋值全局变量。例如，考虑这个例子：

```python
x = 42
def func():
    x = 13

func()
# x 仍然是 42
```

当这段代码执行时，尽管看起来它在函数 `func` 内部修改了全局变量 `x`，但 `x` 仍然保留其值 42。当变量在函数内部被赋值时，它们始终被绑定为局部变量；因此，函数体中的变量 `x` 指向的是一个包含值 13 的全新对象，而不是外部变量。要改变这种行为，请使用 `global` 语句。`global` 将名称声明为属于全局命名空间，当需要修改全局变量时，它是必需的。例如：

```python
x = 42
y = 37
def func():
    global x        # 'x' 处于全局命名空间
    x = 13
    y = 0

func()
# x 现在是 13。y 仍然是 37。
```

需要注意的是，使用 `global` 语句通常被认为是糟糕的 Python 风格。如果你在编写需要函数在后台改变状态的代码，请考虑使用类定义，并通过修改实例变量或类变量来改变状态。例如：

```python
class Config:
    x = 42

def func():
    Config.x = 13
```

Python 允许嵌套函数定义。例如：

```python
def countdown(start):
    n = start

    def display():     # 嵌套函数定义
        print('T-minus', n)

    while n > 0:
        display()
        n -= 1
```

嵌套函数中的变量使用词法作用域（lexical scoping）进行绑定。也就是说，名称首先在局部作用域中解析，然后在从最内层到最外层的连续封闭作用域中解析。同样，这不是一个动态过程——名称的绑定在函数定义时根据语法一次性确定。与全局变量一样，内部函数不能重新赋值定义在外部函数中的局部变量。

```python
def countdown(start):
    n = start
    def display():
        print('T-minus', n)
    def decrement():
        n -= 1                 # Fails: UnboundLocalError
    while n > 0:
        display()
        decrement()
```

要修复这个问题，你可以像这样将 `n` 声明为 `nonlocal`：

```python
def countdown(start):
    n = start
    def display():
        print('T-minus', n)
    def decrement():
        nonlocal n
        n -= 1                 # Modifies the outer n
    while n > 0:
        display()
        decrement()
```

`nonlocal` 不能用于引用全局变量——它必须引用外部作用域中的局部变量。因此，如果一个函数在为全局变量赋值，你仍然应该像之前描述的那样使用 `global` 声明。

使用嵌套函数和 `nonlocal` 声明并不是一种常见的编程风格。例如，内部函数没有外部可见性，这可能会使测试和调试变得复杂。尽管如此，嵌套函数有时对于将复杂的计算分解为较小的部分以及隐藏内部实现细节非常有用。

## 5.13 递归

Python 支持递归函数。例如：

```python
def sumn(n):
    if n == 0:
        return 0
    else:
        return n + sumn(n-1)
```

然而，递归函数调用的深度是有上限的。函数 `sys.getrecursionlimit()` 返回当前的最大递归深度，而函数 `sys.setrecursionlimit()` 可用于更改该值。默认值为 1000。虽然可以增加这个值，但程序仍然受到宿主操作系统强制执行的栈大小（stack size）的限制。当超过递归深度限制时，会抛出 `RuntimeError` 异常。如果限制增加过多，Python 可能会因为段错误（segmentation fault）或其他操作系统错误而崩溃。



在实践中，递归限制问题仅在你处理深度嵌套的递归数据结构（如树和图）时才会出现。许多涉及树的算法自然适合采用递归方案——而且，如果你的数据结构过大，可能会撑爆栈限制。不过，有一些巧妙的解决方法；请参阅第 6 章关于生成器的示例。

## 5.14 `lambda` 表达式

可以使用 `lambda` 表达式定义一个匿名（无名）函数：

```python
lambda args: expression
```

`args` 是一个由逗号分隔的参数列表，而`expression`是一个涉及这些参数的表达式。这里有一个示例：

```python
a = lambda x, y: x + y
r = a(2, 3)         # r 得到 5
```

用 `lambda` 定义的代码必须是一个有效的表达式。`lambda` 表达式中不能出现多个语句，也不能出现非表达式语句（如 `try` 和 `while`）。

`lambda` 的主要用途之一是定义小型回调函数。例如，你可能会看到它与内置操作 `sorted()` 一起使用。例如：

```python
# 根据唯一字母的数量对单词列表进行排序
result = sorted(words, key=lambda word: len(set(word)))
```

当 `lambda` 表达式包含自由变量（未指定为参数的变量）时，需要格外小心。考虑这个例子：

```python
x = 2
f = lambda y: x * y
x = 3
g = lambda y: x * y

print(f(10))       # --> 打印 30
print(g(10))       # --> 打印 30
```

在这个例子中，你可能期望调用 `f(10)` 打印 20，以反映定义时 `x` 为 2 的事实。然而，事实并非如此。作为自由变量，`f(10)` 的求值使用 `x` 在求值时刻所具有的任何值。这可能与 `lambda` 函数定义时的值不同。这种行为有时被称为*延迟绑定（late binding）*。

如果在定义时捕获变量的值很重要，请使用默认参数：

```python
x = 2
f = lambda y, x=x: x * y

x = 3
g = lambda y, x=x: x * y
print(f(10))      # --> 打印 20
print(g(10))      # --> 打印 30
```

这样做之所以有效，是因为默认参数值仅在函数定义时求值，因此会捕获 `x` 的当前值。

## 5.15 高阶函数

Python 支持*高阶函数*的概念。这意味着函数可以作为参数传递给其他函数，放在数据结构中，并由函数作为结果返回。函数被认为是*一等对象（first-class objects）*，这意味着处理函数与处理任何其他类型的数据没有任何区别。这里有一个示例函数，它接收另一个函数作为输入，并在一段时间延迟后调用它——例如，用来模拟云端微服务的性能：

```python
import time

def after(seconds, func):
    time.sleep(seconds)
    func()

# 示例用法
def greeting():
    print('Hello World')


after(10, greeting)        # 10 秒后打印 'Hello World'
```

在这里，传递给 `after()` 的 `func` 参数就是所谓的*回调函数（callback function）*的一个例子。这指的是 `after()` 函数会“回调”作为参数提供的函数。

当函数作为数据传递时，它隐式地携带了与该函数定义环境相关的信息。例如，假设 `greeting()` 函数像这样使用一个变量：

```python
def main():
    name = 'Guido'
    def greeting():
        print('Hello', name)
    after(10, greeting)     # 输出: 'Hello Guido'

main()
```

在这个例子中，变量 `name` 被 `greeting()` 使用，但它是外部 `main()` 函数的局部变量。当 `greeting` 被传递给 `after()` 时，该函数记得它的环境并使用所需的 `name` 变量的值。这依赖于一个被称为*闭包（closure）*的特性。闭包是一个函数以及一个包含执行函数体所需所有变量的环境。

当你基于延迟求值（lazy or delayed evaluation）的概念编写代码时，闭包和嵌套函数非常有用。上面所示的 `after()` 函数就是这个概念的 illustration。它接收一个不会立即被求值的函数——该函数仅在稍后的某个时间点才被执行。这是一种在其他上下文中经常出现的通用编程模式。例如，一个程序可能有仅在响应事件（如按键、鼠标移动、网络数据包到达等）时才执行的函数。在所有这些情况下，函数求值都被推迟到发生有趣的事情时。当函数最终执行时，闭包确保函数能获得其所需的一切。

你还可以编写创建并返回其他函数的函数。例如：

```python
def make_greeting(name):
    def greeting():
        print('Hello', name)
    return greeting

f = make_greeting('Guido')
g = make_greeting('Ada')

f() # 输出: 'Hello Guido'
g() # 输出: 'Hello Ada'
```

在这个例子中，`make_greeting()` 函数本身不执行任何有趣的计算。相反，它创建并返回一个执行实际工作的 `greeting()` 函数。只有在以后该函数被求值时，工作才会执行。

在这个例子中，两个变量 `f` 和 `g` 持有 `greeting()` 函数的两个不同版本。尽管创建这些函数的 `make_greeting()` 函数已不再执行，但 `greeting()` 函数仍然记得定义好的 `name` 变量——它是每个函数闭包的一部分。

关于闭包的一个注意事项是，对变量名的绑定不是一个“快照”，而是一个动态过程——这意味着闭包指向的是 `name` 变量及其最近被分配的值。这很微妙，但这里有一个例子说明问题可能会在哪里出现：

```python
def make_greetings(names):
    funcs = []
    for name in names:
        funcs.append(lambda: print('Hello', name))
    return funcs

# 尝试运行
a, b, c = make_greetings(['Guido', 'Ada', 'Margaret'])
```

```python
a()     # Prints 'Hello Margaret'
b()     # Prints 'Hello Margaret'
c()     # Prints 'Hello Margaret'
```

在这个例子中，创建了一个由不同函数组成的列表（使用了 lambda）。看起来它们似乎都在使用一个唯一的 name 值，因为 name 在 for 循环的每次迭代中都会改变。但事实并非如此。所有函数最终使用的都是同一个 name 值——即当外部 `make_greetings()` 函数返回时的那个值。

这可能是出乎意料的，且不是你想要的结果。如果你想捕获变量的一个副本，请将其作为默认参数捕获，正如前面所描述的：

```python
def make_greetings(names):
    funcs = []
    for name in names:
        funcs.append(lambda name=name: print('Hello', name))
    return funcs
```

```python
# 尝试运行
a, b, c = make_greetings(['Guido', 'Ada', 'Margaret'])
a()     # Prints 'Hello Guido'
b()     # Prints 'Hello Ada'
c()     # Prints 'Hello Margaret'
```

在最后两个例子中，函数是使用 lambda 定义的。这通常被用作创建小型回调函数的快捷方式。然而，这并不是严格的要求。你也可以将其改写如下：

```python
def make_greetings(names):
    funcs = []
    for name in names:
        def greeting(name=name):
            print('Hello', name)
        funcs.append(greeting)
    return funcs
```

选择何时以及何处使用 `lambda` 取决于个人喜好和代码清晰度。如果它让代码变得难以阅读，那么或许应该避免使用。

## 5.16 回调函数中的参数传递

回调函数中一个具有挑战性的问题是如何向提供的函数传递参数。考虑之前编写的 `after()` 函数：

```python
import time


def after(seconds, func):
    time.sleep(seconds)
    func()
```

在这段代码中，`func()` 被硬编码为在调用时不带任何参数。如果你想传递额外的参数，那就没那么简单了。例如，你可能会尝试这样做：

```python
def add(x, y):
    print(f'{x} + {y} -> {x+y}')
    return x + y
```

```python
after(10, add(2, 3))     # 失败：add() 被立即调用
```

在这个例子中，`add(2, 3)` 函数立即运行并返回 `5`。然后 `after()` 函数在 10 秒后崩溃，因为它尝试执行 `5()`。这绝对不是你的本意。然而，如果 `add()` 需要带着预期的参数被调用，似乎没有显而易见的方法能让它正常工作。

这个问题暗示了一个关于函数使用和通用函数式编程的更深层设计问题——函数组合（function composition）。当函数以各种方式混合在一起时，你需要思考函数的输入和输出是如何连接的。这并不总是简单的。

在这种情况下，一种解决方案是使用 `lambda` 将计算封装到一个零参数函数中。例如：

```python
after(10, lambda: add(2, 3))
```

像这样的小型零参数函数有时被称为*thunk*。基本上，它是一个表达式，将在以后被最终调用为零参数函数时才被求值。这可以成为一种通用方法，用来将任何表达式的求值延迟到稍后的时间点：将表达式放入 `lambda` 中，并在你真正需要该值时调用该函数。

作为使用 `lambda` 的替代方案，你可以使用 `functools.partial()` 来创建一个部分求值的函数，如下所示：

```python
from functools import partial

after(10, partial(add, 2, 3))
```

`partial()` 创建一个可调用对象，其中一个或多个参数已经指定并被缓存。这是一种有用的方法，可以让不符合要求的函数匹配回调函数或其他应用中预期的调用签名。这里有几个使用 `partial()` 的更多示例：

```python
def func(a, b, c, d):
    print(a, b, c, d)

f = partial(func, 1, 2)     # 固定 a=1, b=2
f(3, 4)                      # func(1, 2, 3, 4)
f(10, 20)                    # func(1, 2, 10, 20)

g = partial(func, 1, 2, d=4) # 固定 a=1, b=2, d=4
g(3)                         # func(1, 2, 3, 4)
g(10)                        # func(1, 2, 10, 4)
```

`partial()` 和 `lambda` 可以用于类似的目的，但两种技术之间存在一个重要的语义区别。使用 `partial()` 时，参数在部分函数首次定义时就被求值并绑定。而对于零参数 `lambda`，参数在 `lambda` 函数稍后实际执行时才被求值并绑定（所有内容的求值都被延迟了）。为了说明这一点：

```python
>>> def func(x, y):
...     return x + y
...
>>> a = 2
>>> b = 3
>>> f = lambda: func(a, b)
>>> g = partial(func, a, b)
>>> a = 10
>>> b = 20
>>> f()     # 使用 a, b 的当前值
30
>>> g()     # 使用 a, b 的初始值
5
>>>
```

由于部分函数是完全求值的，因此由 `partial()` 创建的可调用对象是可以通过序列化转换为字节、保存到文件，甚至通过网络连接传输的对象（例如，使用 `pickle` 标准库模块）。这在使用 lambda 函数时是无法实现的。因此，在需要传递函数（可能传递给在不同进程或不同机器上运行的 Python 解释器）的应用中，你会发现 `partial()` 具有更好的适应性。

顺便提一下，部分函数应用与一个被称为*currying*（柯里化）的概念密切相关。柯里化是一种函数式编程技术，其中一个多参数函数被表达为一系列嵌套的单参数函数链。这里有一个例子：

```python
# 三参数函数
def f(x, y, z):
    return x + y + z

# 柯里化版本
def fc(x):
    return lambda y: (lambda z: x + y + z)

# 使用示例
a = f(2, 3, 4)        # 3 参数函数
b = fc(2)(3)(4)       # 柯里化版本
```

这在 Python 编程中并不常见，而且几乎没有实际的理由这样做。然而……

回到参数传递的原始问题，向回调函数传递参数的另一种选择是将它们作为外部调用函数的独立参数接收。考虑这个版本的 `after()` 函数：

```python
def after(seconds, func, *args):
    time.sleep(seconds)
    func(*args)
```

`after(10, add, 2, 3)` # 10 秒后调用 add(2, 3)

你会注意到，不支持向 `func()` 传递关键字参数。这是故意设计的。关键字参数的一个问题是，给定函数的参数名称可能会与已经在使用的参数名称（即 `seconds` 和 `func`）发生冲突。关键字参数还可能被预留用于指定 `after()` 函数本身的选项。例如：

```python
def after(seconds, func, *args, debug=False):
    time.sleep(seconds)
    if debug:
        print('About to call', func, args)
    func(*args)
```

不过，并非毫无办法。如果你需要为 `func()` 指定关键字参数，仍然可以使用 `partial()`。例如：

`after(10, partial(add, y=3), 2)`

如果你希望 `after()` 函数接受关键字参数，一种安全的方法是使用仅限位置参数（positional-only arguments）。例如：

```python
def after(seconds, func, debug=False, /, *args, **kwargs):
    time.sleep(seconds)
    if debug:
        print('About to call', func, args, kwargs)
    func(*args, **kwargs)
```

`after(10, add, 2, y=3)`

另一个可能令人不安的见解是，`after()` 实际上代表了两个不同的函数调用合并在一起。或许参数传递的问题可以分解为像这样的两个函数：

```python
def after(seconds, func, debug=False):
    def call(*args, **kwargs):
        time.sleep(seconds)
        if debug:
            print('About to call', func, args, kwargs)
        func(*args, **kwargs)
    return call
```

```python
after(10, add)(2, y=3)
```

现在，`after()` 的参数与 `func` 的参数之间完全没有冲突。不过，这样做可能会在你和你的同事之间引入冲突。

## 5.17 从回调函数返回结果

前一节未讨论的另一个问题是如何返回计算结果。考虑这个修改后的 `after()` 函数：

```python
def after(seconds, func, *args):
    time.sleep(seconds)
    return func(*args)
```

这可以工作，但由于涉及两个独立的函数——`after()` 函数本身和提供的回调函数 `func`，因此会出现一些微妙的边缘情况。

其中一个问题涉及异常处理。例如，尝试以下两个示例：

```python
after("1", add, 2, 3)    # 失败：TypeError (预期为整数)
after(1, add, "2", 3)    # 失败：TypeError (无法将 int 连接到 str)
```



在这两种情况下都会抛出 `TypeError`，但原因完全不同，且发生在不同的函数中。第一个错误是由 `after()` 函数本身的问题引起的：传递给 `time.sleep()` 的参数不正确。第二个错误则是由于回调函数 `func(*args)` 执行时出现的问题。

如果区分这两种情况很重要，有几种方案可以选择。一种方案是依赖于链式异常（chained exceptions）。其核心思想是以不同的方式对回调函数产生的错误进行封装，从而允许将它们与其它类型的错误分开处理。例如：

```python
class CallbackError(Exception):
    pass

def after(seconds, func, *args):
    time.sleep(seconds)
    try:
        return func(*args)
    except Exception as err:
        raise CallbackError('Callback function failed') from err
```

这段修改后的代码将来自所提供回调函数的错误隔离到其自身的异常类别中。使用方式如下：

```python
try:
    r = after(delay, add, x, y)
except CallbackError as err:
    print("It failed. Reason", err.__cause__)
```

如果 `after()` 本身的执行出现问题，该异常将直接向上传播且不被捕获。另一方面，与所提供的回调函数执行相关的问题将被捕获并作为 `CallbackError` 报告。这一切虽然非常微妙，但在实践中，错误管理是非常困难的。这种方法使得责任归属更加精准，且 `after()` 的行为更容易编写文档。具体来说，如果回调函数中出现问题，它总是被报告为 `CallbackError`。

另一种方案是将回调函数的执行结果封装进某种结果实例中，该实例同时持有值（value）和错误（error）。例如，定义一个如下的类：

```python
class Result:
    def __init__(self, value=None, exc=None):
        self.value = value
        self._exc = exc
    def result(self):
        if self._exc:
            raise self._exc
        else:
            return self.value
```

然后，使用这个类从 `after()` 函数返回结果：

```python
def after(seconds, func, *args):
    time.sleep(seconds)
    try:
        return Result(value=func(*args))
    except Exception as err:
        return Result(exc=err)
```

使用示例：

```python
r = after(1, add, 2, 3)
print(r.result())                      # 打印 5

s = after("1", add, 2, 3)             # 立即抛出 TypeError。
# sleep() 参数错误。

t = after(1, add, "2", 3)            # 返回一个 "Result" 实例
print(t.result())                     # 抛出 TypeError
```

第二种方案的工作原理是将回调函数的结果报告推迟到一个独立的步骤中。如果 `after()` 出现问题，它会立即被报告。如果回调函数 `func()` 出现问题，则在用户尝试通过调用 `result()` 方法获取结果时才会报告。

这种将结果装箱（boxing）到一个特殊实例中并在稍后拆箱（unwrapped）的风格，是现代编程语言中一种日益常见的模式。使用它的一大原因是它有利于类型检查。例如，如果你为 `after()` 添加类型提示，其行为就得到了完整定义——它总是返回一个 `Result` 对象，没有其它可能：

```python
def after(seconds, func, *args) -> Result:
    ...
```

虽然这种模式在 Python 代码中并不那么常见，但在处理线程（threads）和进程（processes）等并发原语时，它会定期出现。例如，在处理线程池时，所谓的 `Future` 实例就表现出这种行为。例如：

```python
from concurrent.futures import ThreadPoolExecutor

pool = ThreadPoolExecutor(16)
r = pool.submit(add, 2, 3)     # 返回一个 Future
print(r.result())              # 拆箱 Future 结果
```

## 5.18 装饰器

装饰器是一个在另一个函数周围创建包装器（wrapper）的函数。这种包装的主要目的是改变或增强被包装对象的行为。在语法上，装饰器使用特殊的 `@` 符号表示，如下所示：

```python
@decorate
def func(x):
    ...
```

上述代码是以下内容的简写：

```python
def func(x):
    ...
func = decorate(func)
```

在示例中，定义了一个函数 `func()`。然而，在其定义之后，函数对象本身被传递给函数 `decorate()`，后者返回一个替代原 `func` 的对象。

作为一个具体实现的示例，这里有一个 `@trace` 装饰器，它可以为函数添加调试信息：

```python
def trace(func):
    def call(*args, **kwargs):
        print('Calling', func.__name__)
        return func(*args, **kwargs)
    return call
```

使用示例：

```python
@trace
def square(x):
    return x * x
```

在这段代码中，`trace()` 创建了一个包装函数，该函数会写入一些调试输出，然后调用原始函数对象。因此，如果你调用 `square()`，你将看到包装器中 `print()` 函数的输出。

如果事情真的这么简单就好了！在实践中，函数还包含元数据，例如函数名、文档字符串（doc string）和类型提示。如果你在函数周围加上包装器，这些信息就会被隐藏。在编写装饰器时，最佳实践是使用 `@wraps()` 装饰器，如本例所示：

```python
from functools import wraps

def trace(func):
    @wraps(func)
    def call(*args, **kwargs):
        print('Calling', func.__name__)
        return func(*args, **kwargs)
    return call
```

`@wraps()` 装饰器将各种函数元数据复制到替代函数中。在这种情况下，给定函数 `func()` 的元数据被复制到了返回的包装函数 `call()` 中。

当应用装饰器时，它们必须出现在函数之前的独立行上。可以应用多个装饰器。这里有一个示例：

```python
@decorator1
@decorator2
def func(x):
    pass
```

在这种情况下，装饰器的应用顺序如下：

```python
def func(x):
    pass

func = decorator1(decorator2(func))
```

装饰器出现的顺序可能会产生影响。例如，在类定义中，像 `@classmethod` 和 `@staticmethod` 这样的装饰器通常必须放置在最外层。例如：

```python
class SomeClass(object):
    @classmethod    # 正确
    @trace
    def a(cls):
        pass

    @trace           # 错误。失败。
    @classmethod
    def b(cls):
        pass
```

这种位置限制的原因与 `@classmethod` 返回的值有关。有时装饰器会返回一个与普通函数不同的对象。如果最外层的装饰器没有预料到这一点，程序可能会崩溃。在这种情况下，`@classmethod` 创建了一个类方法描述符对象（见第 7 章）。除非 `@trace` 装饰器在编写时考虑到了这一点，否则如果装饰器排列顺序错误，它将会失败。

装饰器也可以接收参数。假设你想修改 `@trace` 装饰器，以允许自定义消息，如下所示：

```python
@trace("You called {func.__name__}")
def func():
    pass
```

如果提供了参数，装饰过程的语义如下：

```python
def func():
    pass

# 创建装饰函数
temp = trace("You called {func.__name__}")

# 将其应用于 func
func = temp(func)
```

在这种情况下，接收参数的最外层函数负责创建一个装饰函数。然后调用该函数并传入要装饰的函数，以获得最终结果。装饰器的实现可能如下所示：

```python
from functools import wraps

def trace(message):
    def decorate(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            print(message.format(func=func))
            return func(*args, **kwargs)
        return wrapper
    return decorate
```

这个实现的一个有趣特性是，外层函数实际上是一种“装饰器工厂”。假设你发现自己在编写如下代码：

```python
@trace('You called {func.__name__}')
def func1():
    ...
```

```python
pass

@trace('You called {func.__name__}')
def func2():
    pass
```

那样做很快就会变得冗长。你可以通过调用一次外部装饰函数并重复使用其结果来简化它，如下所示：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_207_0.png)

```python
logged = trace('You called {func.__name__}')
```

```python
@logged
def func1():
    pass
```

```python
@logged
def func2():
    pass
```

装饰器并不一定非要替换原函数。有时装饰器仅执行某种操作，例如注册。例如，如果你正在构建一个事件处理程序注册表，你可以定义一个这样工作的装饰器：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_207_1.png)

```python
@eventhandler('BUTTON')
def handle_button(msg):
    ...
```

```python
@eventhandler('RESET')
def handle_reset(msg):
    ...
```

这是一个管理该过程的装饰器：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_207_2.png)

```python
# Event handler decorator
_event_handlers = { }
def eventhandler(event):
    def register_function(func):
        _event_handlers[event] = func
        return func
    return register_function
```

## 5.19 Map, Filter, and Reduce

熟悉函数式语言的程序员经常询问关于常见的列表操作，如 `map`、`filter` 和 `reduce`。其中大部分功能可以通过列表推导式和生成器表达式来实现。例如：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_208_0.png)

```python
def square(x):
    return x * x

nums = [1, 2, 3, 4, 5]
squares = [ square(x) for x in nums ]  # [1, 4, 9, 16, 25]
```

从技术上讲，你甚至不需要那个简短的一行函数。你可以写成：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_208_1.png)

```python
squares = [ x * x for x in nums ]
```

过滤操作也可以通过列表推导式来完成：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_208_2.png)

```python
a = [ x for x in nums if x > 2 ]  # [3, 4, 5]
```

如果你使用生成器表达式，你将获得一个通过迭代逐步产生结果的生成器。例如：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_208_3.png)

```python
squares = (x*x for x in nums)     # Creates a generator
for n in squares:
    print(n)
```

Python 提供了一个内置的 `map()` 函数，它与使用生成器表达式映射函数的效果相同。例如，上面的例子可以写成：

```python
squares = map(lambda x: x*x, nums)
for n in squares:
    print(n)
```

内置的 `filter()` 函数创建了一个过滤值的生成器：

```python
for n in filter(lambda x: x > 2, nums):
    print(n)
```

如果你想累积或规约（reduce）值，可以使用 `functools.reduce()`。例如：

```python
from functools import reduce
total = reduce(lambda x, y: x + y, nums)
```

在通用形式中，`reduce()` 接收一个双参数函数、一个可迭代对象和一个初始值。这里有几个示例：

```python
nums = [1, 2, 3, 4, 5]
total = reduce(lambda x, y: x + y, nums)              # 15
product = reduce(lambda x, y: x * y, nums, 1)         # 120

pairs = reduce(lambda x, y: (x, y), nums, None)
# ((((None, 1), 2), 3), 4), 5)
```

`reduce()` 在提供的可迭代对象上从左到右累积值。这被称为左折叠（left-fold）操作。以下是 `reduce(func, items, initial):` 的伪代码：

```python
def reduce(func, items, initial):
    result = initial
    for item in items:
        result = func(result, item)
    return result
```

在实践中使用 `reduce()` 可能会令人困惑。此外，常见的规约操作如 `sum()`、`min()` 和 `max()` 已经是内置的了。如果你使用这些内置函数而不是尝试用 `reduce()` 来实现常见操作，你的代码将更容易阅读（并且运行速度可能更快）。

## 5.20 函数内省、属性和签名

正如你所见，函数是对象——这意味着它们可以被赋值给变量，放在数据结构中，并且像程序中的任何其他类型的数据一样被使用。它们还可以通过各种方式被检查。表 5.1 显示了一些常见的函数属性。其中许多属性在调试、日志记录以及其他涉及函数的操作中非常有用。

**表 5.1** 函数属性

| 属性 | 描述 |
|---|---|
| `f.__name__` | 函数名称 |
| `f.__qualname__` | 全限定名（如果存在嵌套） |
| `f.__module__` | 定义该函数的模块名称 |
| `f.__doc__` | 文档字符串 |
| `f.__annotations__` | 类型提示 |
| `f.__globals__` | 作为全局命名空间的字典 |
| `f.__closure__` | 闭包变量（如果有） |
| `f.__code__` | 底层代码对象 |

`f.__name__` 属性包含定义函数时使用的名称。`f.__qualname__` 是一个更长的名称，包含了关于周围定义环境的额外信息。



`f.__module__` 属性是一个字符串，保存了定义该函数的模块名称。`f.__globals__` 属性是一个字典，充当该函数的全局命名空间。它通常与关联的模块对象所附带的字典是同一个。

`f.__doc__` 保存函数的文档字符串。`f.__annotations__` 属性是一个字典，保存类型提示（如果有）。

`f.__closure__` 保存嵌套函数闭包变量值的引用。这些内容隐藏得较深，但下面的例子展示了如何查看它们：

```python
def add(x, y):
    def do_add():
        return x + y
    return do_add

>>> a = add(2, 3)
>>> a.__closure__
(<cell at 0x10edf1e20: int object at 0x10ecc1950>,
 <cell at 0x10edf1d90: int object at 0x10ecc1970>)
>>> a.__closure__[0].cell_contents
2
>>>
```

`f.__code__` 对象代表函数体的编译后的解释器字节码。

函数可以附带任意属性。这里有一个例子：

```python
def func():
    pass # statements

func.secure = 1
func.private = 1
```

属性在函数体内部是不可见的——它们不是局部变量，也不会出现在执行环境的名称中。函数属性的主要用途是存储额外的元数据。有时框架或各种元编程技术会利用函数标记（function tagging）——即给函数附加属性。一个例子是在抽象基类方法上使用的 `@abstractmethod` 装饰器。该装饰器所做的唯一事情就是附加一个属性：

```python
def abstractmethod(func):
    func.__isabstractmethod__ = True
    return func
```

其他某些代码（在这种情况下是一个元类）会查找此属性，并利用它在实例创建时增加额外的检查。

如果你想了解更多关于函数参数的信息，可以使用 `inspect.signature()` 函数获取其签名：

```python
import inspect

def func(x: int, y: float, debug=False) -> float:
    pass

sig = inspect.signature(func)
```

签名对象提供了许多便捷的功能，用于打印和获取关于参数的详细信息。例如：

```python
# 以美观的形式打印签名
print(sig)    # 输出 (x: int, y: float, debug=False) -> float

# 获取参数名称列表
print(list(sig.parameters))    # 输出 [ 'x', 'y', 'debug']

# 遍历参数并打印各种元数据
for p in sig.parameters.values():
    print('name', p.name)
    print('annotation', p.annotation)
    print('kind', p.kind)
    print('default', p.default)
```

签名是描述函数性质的元数据——包括如何调用它、类型提示等等。你可以对签名进行各种操作。其中一个有用的操作是比较。例如，以下是检查两个函数是否具有相同签名的方法：

```python
def func1(x, y):
    pass

def func2(x, y):
    pass

assert inspect.signature(func1) == inspect.signature(func2)
```

这类比较在框架中可能会非常有用。例如，一个框架可以使用签名比较来检查你编写的函数或方法是否符合预期的原型。

如果存储在函数的 `__signature__` 属性中，签名将显示在帮助消息中，并在后续使用 `inspect.signature()` 时被返回。例如：

```python
def func(x, y, z=None):
    ...

func.__signature__ = inspect.signature(lambda x,y: None)
```

在这个例子中，可选参数 `z` 将在后续对 `func` 的检查中被隐藏。相反，`inspect.signature()` 将返回附加的签名。

## 5.21 环境检查

函数可以使用内置函数 `globals()` 和 `locals()` 来检查其执行环境。`globals()` 返回充当全局命名空间的字典。这与 `func.__globals__` 属性相同。这通常就是持有封闭模块内容的那个字典。

`locals()` 返回一个包含所有局部变量和闭包变量值的字典。该字典并不是用于持有这些变量的实际数据结构。局部变量可以来自外部函数（通过闭包）或在内部定义。`locals()` 收集所有这些变量并将它们放入一个字典中供你使用。修改 `locals()` 字典中的项对底层变量没有影响。例如：

```python
def func():
    y = 20
    locs = locals()
    locs['y'] = 30       # 尝试修改 y
    print(locs['y'])     # 输出 30
    print(y)             # 输出 20
```

如果你希望更改生效，必须使用正常的赋值将其复制回局部变量。

```python
def func():
    y = 20
    locs = locals()
    locs['y'] = 30
    y = locs['y']
```

函数可以使用 `inspect.currentframe()` 获取自身的堆栈帧。函数可以通过帧上的 `f.f_back` 属性追踪堆栈回溯，从而获取其调用者的堆栈帧。这里有一个示例：

```python
import inspect

def spam(x, y):
    z = x + y
    grok(z)

def grok(a):
    b = a * 10
    # outputs: {'a':5, 'b':50 }
    print(inspect.
```

```python
async def main():
    for name in ['Paula', 'Thomas', 'Lewis']:
        a = await make_greeting(name)
        print(a)

# Run it. Will see greetings for Paula, Thomas, and Lewis
asyncio.run(main())
```

`await` 的使用仅在封闭的 `async` 函数定义内有效。它也是使异步函数执行的必要组成部分。如果你省略了 `await`，你会发现代码无法正常运行。

使用 `await` 的要求暗示了异步函数在通用使用上的一个问题。即，它们不同的求值模型导致它们无法与其他 Python 部分结合使用。具体来说，永远不可能在非异步函数中编写调用异步函数的代码：

[点击此处查看代码图片](url)

```python
async def twice(x):
    return 2 * x

def main():
    print(twice(2))         # Error. Doesn't execute the function
    print(await twice(2))   # Error. Can't use await here.
```

在同一个应用程序中结合异步和非异步功能是一个复杂的话题，特别是如果你考虑到涉及高阶函数、回调和装饰器的某些编程技巧。在大多数情况下，对异步函数的支持必须作为一种特殊情况来构建。

Python 正是对迭代器和上下文管理器协议做了如此处理。例如，可以使用类中的 `__aenter__()` 和 `__aexit__()` 方法来定义异步上下文管理器，如下所示：

[点击此处查看代码图片](url)

```python
class AsyncManager(object):
    def __init__(self, x):
        self.x = x

    async def yow(self):
        pass

    async def __aenter__(self):
        return self

    async def __aexit__(self, ty, val, tb):
        pass
```

请注意，这些方法是异步函数，因此可以使用 `await` 执行其他异步函数。要使用此类管理器，必须使用特殊的 `async with` 语法，该语法仅在异步函数内合法：

[点击此处查看代码图片]

```python
# Example use
async def main():
    async with AsyncManager(42) as m:
        await m.yow()

asyncio.run(main())
```

类似地，一个类可以通过定义 `__aiter__()` 和 `__anext__()` 方法来定义异步迭代器。这些方法被 `async for` 语句使用，该语句同样只能出现在异步函数内部。

从实际角度来看，异步函数的行为与普通函数完全相同——只不过它必须在诸如 `asyncio` 之类的管理环境中执行。除非你明确决定在这样的环境中工作，否则你应该继续前行并忽略异步函数。这样你会轻松得多。

## 5.24 结语：关于函数与组合的思考

任何系统都是由组件组合而成的。在 Python 中，这些组件包括各种类型的库和对象。然而，所有这一切的底层都是函数。函数是将系统组合在一起的胶水，也是数据传输的基本机制。

本章的大部分讨论集中在函数的本质及其接口上。输入如何传递给函数？输出如何处理？错误如何报告？如何能更紧密地控制并更好地理解所有这些事情？

在处理大型项目时，函数之间的交互作为潜在的复杂性来源是值得思考的。这往往决定了一个 API 是直观易用还是混乱不堪。

# 6. 生成器

生成器函数是 Python 最有趣且最强大的特性之一。生成器通常被呈现为定义新型迭代模式的一种便捷方式。然而，它们远不止于此：生成器还可以从根本上改变函数的整个执行模型。本章将讨论生成器、生成器委托、基于生成器的协程以及生成器的常见应用。

## 6.1 生成器与 `yield`

如果一个函数使用了 `yield` 关键字，它就定义了一个被称为生成器的对象。生成器的主要用途是产生用于迭代的值。这里有一个示例：

点击此处查看代码图片

```python
def countdown(n):
    print('Counting down from', n)
    while n > 0:
        yield n
        n -= 1
```

```python
# Example use
for x in countdown(10):
    print('T-minus', x)
```

如果你调用这个函数，你会发现它的代码都没有开始执行。例如：

点击此处查看代码图片

```python
>>> c = countdown(10)
>>> c
<generator object countdown at 0x105f73740>
```

相反，它创建了一个生成器对象。而生成器对象只有在你开始对其进行迭代时才会执行函数。一种方法是对其调用 `next()`：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_225_0.png)

```python
>>> next(c)
Counting down from 10
10
>>> next(c)
 9
```

当 `next()` 被调用时，生成器函数执行语句直到遇到 `yield` 语句。`yield` 语句返回一个结果，此时函数的执行被暂停，直到 `next()` 再次被调用。在暂停期间，函数保留其所有的局部变量和执行环境。当恢复执行时，从 `yield` 之后的语句继续执行。

`next()` 是调用生成器上 `__next__()` 方法的简写。例如，你也可以这样做：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_225_1.png)

```python
>>> c.__next__()
8
>>> c.__next__()
7
```

通常你不会直接在生成器上调用 `next()`，而是使用 `for` 语句或其他消耗项目的操作。例如：

![](img/24ecec9a39ceab2751d0d39b3c5512ce_225_2.png)

```python
for n in countdown(10):
    statements
```

```python
a = sum(countdown(10))
```

生成器函数会不断产生项目，直到它返回——通过到达函数末尾或使用 `return` 语句。这将引发一个 `StopIteration` 异常，从而终止 `for` 循环。如果生成器函数返回一个非 `None` 值，该值将被附在 `StopIteration` 异常上。例如，这个生成器函数同时使用了 `yield` 和 `return`：

```python
def func():
    yield 37
    return 42
```

以下是代码执行的方式：

点击此处查看代码图片

```python
>>> f = func()
>>> f
<generator object func at 0x10b7cd480>
>>> next(f)
37
>>> next(f)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration: 42
```

观察到返回值被附在 `StopIteration` 上。要收集这个值，你需要显式地捕获 `StopIteration` 并提取该值：

点击此处查看代码图片

```python
try:
    next(f)
except StopIteration as e:
    value = e.value
```

通常，生成器函数不返回值。生成器几乎总是被 `for` 循环消耗，而 `for` 循环无法获取异常值。这意味着获取该值的唯一实际方法是通过显式的 `next()` 调用手动驱动生成器。大多数涉及生成器的代码根本不会这样做。

生成器的一个微妙问题是生成器函数仅被部分消耗的情况。例如，考虑这段提前终止循环的代码：

点击此处查看代码图片

```python
for n in countdown(10):
    if n == 2:
        break
    statements
```

在这个例子中，`for` 循环通过调用 `break` 中止，相关的生成器从未运行到完全结束。如果你的生成器函数执行某种清理操作很重要，请确保使用 `try-finally` 或上下文管理器。例如：

点击此处查看代码图片

```python
def countdown(n):
    print('Counting down from', n)
    try:
        while n > 0:
            yield n
            n = n - 1
    finally:
        print('Only made it to', n)
```

即使生成器没有被完全消耗，也能保证执行 `finally` 块中的代码——当被遗弃的生成器被垃圾回收时，它将执行。同样地，任何清理涉及上下文管理器的代码在生成器终止时也保证会执行：

```python
def func(filename):
    with open(filename) as file:
        ...
        yield data
        ...

# 即使生成器被放弃，文件在此处也会关闭
```

正确清理资源是一个棘手的问题。只要你使用 `try-finally` 或上下文管理器等结构，即使生成器被提前终止，也能保证其执行正确的清理操作。

## 6.2 可重启的生成器

通常情况下，生成器函数仅执行一次。例如：

```python
>>> c = countdown(3)
>>> for n in c:
...     print('T-minus', n)
...
T-minus 3
T-minus 2
T-minus 1
>>> for n in c:
...     print('T-minus', n)
...
>>>
```

如果你想要一个允许重复迭代的对象，请将其定义为一个类，并将 `__iter__()` 方法定义为生成器：

```python
class countdown:
    def __init__(self, start):
        self.start = start

    def __iter__(self):
        n = self.start
        while n > 0:
            yield n
            n -= 1
```

这样可行是因为每次迭代时，`__iter__()` 都会创建一个全新的生成器。

## 6.3 生成器委托

生成器的一个核心特性是，包含 `yield` 的函数永远不会自行执行——它必须由其他代码通过 `for` 循环或显式的 `next()` 调用来驱动。这使得编写包含 `yield` 的库函数变得有些困难，因为仅仅调用生成器函数不足以使其执行。为了解决这个问题，可以使用 `yield from` 语句。例如：



```python
def countup(stop):
    n = 1
    while n <= stop:
        yield n
        n += 1

def countdown(start):
    n = start
    while n > 0:
        yield n
        n -= 1

def up_and_down(n):
    yield from countup(n)
    yield from countdown(n)
```

`yield from`有效地将迭代过程委托给了一个外部迭代。例如，你会编写如下代码来驱动迭代：

```python
>>> for x in up_and_down(5):
...     print(x, end=' ')
1 2 3 4 5 4 3 2 1
>>>
```

`yield from`主要是为了让你不必亲自驱动迭代。如果没有这个特性，你必须将`up_and_down(n)`写成如下形式：

```python
def up_and_down(n):
    for x in countup(n):
        yield x
    for x in countdown(n):
        yield x
```

在编写必须递归迭代嵌套可迭代对象的代码时，`yield from`尤其有用。例如，这段代码可以展平嵌套列表：

```python
def flatten(items):
    for i in items:
        if isinstance(i, list):
            yield from flatten(i)
        else:
            yield i
```

这是一个工作示例：

```python
>>> a = [1, 2, [3, [4, 5], 6, 7], 8]
>>> for x in flatten(a):
...     print(x, end=' ')
...
1 2 3 4 5 6 7 8
>>>
```

该实现的一个限制是它仍然受 Python 递归深度限制的影响，因此无法处理深度嵌套的结构。这将在下一节中解决。

## 6.4 生成器的实际应用

乍一看，除了定义简单的迭代器之外，如何将生成器用于实际问题可能并不明显。然而，生成器在构建与管道（pipelines）和工作流（workflows）相关的数据处理问题时特别有效。

生成器的一个有用应用是作为重构由深度嵌套的`for`循环和条件语句组成代码的工具。考虑这个脚本，它在 Python 文件目录中搜索所有包含单词“spam”的注释：

```python
import pathlib
import re

for path in pathlib.Path('.').rglob('*.py'):
    if path.exists():
        with path.open('rt', encoding='latin-1') as file:
            for line in file:
                m = re.match('.*(#.*)$', line)
                if m:
                    comment = m.group(1)
                    if 'spam' in comment:
                        print(comment)
```

请注意嵌套控制流的层数。当你查看这段代码时，眼睛已经开始感到疲劳了。现在，考虑这个使用生成器的版本：

```python
import pathlib
import re

def get_paths(topdir, pattern):
    for path in pathlib.Path(topdir).rglob(pattern):
        if path.exists():
            yield path

def get_files(paths):
    for path in paths:
        with path.open('rt', encoding='latin-1') as file:
            yield file

def get_lines(files):
    for file in files:
        yield from file

def get_comments(lines):
    for line in lines:
        m = re.match('.*(#.*)$', line)
        if m:
            yield m.group(1)

def print_matching(lines, substring):
    for line in lines:
        if substring in line:
            print(line)

paths = get_paths('.', '*.py')
files = get_files(paths)
lines = get_lines(files)
comments = get_comments(lines)
print_matching(comments, 'spam')
```

在这一版本中，问题被分解为更小的自包含组件。每个组件只关注特定的任务。例如，`get_paths()`生成器仅关注路径名，`get_files()`生成器仅关注打开文件，以此类推。只有在最后，这些生成器才被串联成一个工作流来解决问题。

使每个组件小型化且隔离是一种良好的抽象技术。例如，考虑`get_comments()`生成器。它接受任何产生文本行的可迭代对象作为输入。这些文本几乎可以来自任何地方——文件、列表、生成器等等。因此，这种功能比嵌入在涉及文件的深度嵌套`for`循环中时要强大得多，且适应性更强。因此，生成器通过将问题分解为小型且定义良好的计算任务来鼓励代码复用。较小的任务也更容易进行推理、调试和测试。

生成器还可用于改变函数应用的常规求值规则。通常，当你调用一个函数时，它会立即执行并产生结果。生成器则并非如此。当生成器函数被调用时，其执行会被延迟，直到其他代码对其调用`next()`（无论是显式调用还是通过`for`循环）。

作为一个例子，再次考虑用于展平嵌套列表的生成器函数：

```python
def flatten(items):
    for i in items:
        if isinstance(i, list):
            yield from flatten(i)
        else:
            yield i
```

该实现的一个问题是，由于 Python 的递归限制，它无法处理深度嵌套的结构。这可以通过使用栈（stack）以不同的方式驱动迭代来修复。考虑这个版本：

```python
def flatten(items):
    stack = [ iter(items) ]
    while stack:
        try:
            item = next(stack[-1])
            if isinstance(item, list):
                stack.append(iter(item))
            else:
                yield item
        except StopIteration:
            stack.pop()
```

该实现构建了一个内部的迭代器栈。它不受 Python 递归限制的影响，因为它将数据存放在内部列表中，而不是在内部解释器栈上构建帧。因此，如果你发现自己需要展平某个异常深的数据结构（例如数百万层），你会发现这个版本运行良好。

这些例子是否意味着你应该使用疯狂的生成器模式来重写所有代码？并非如此。核心观点是，生成器的延迟求值允许你改变常规函数求值的时空维度。在许多现实场景中，这些技术非常有用，并能以出人意料的方式被应用。

## 6.5 增强型生成器与`yield`表达式

在生成器函数内部，`yield`语句也可以作为表达式，出现在赋值运算符的右侧。例如：

```python
def receiver():
    print('Ready to receive')
    while True:
        n = yield
        print('Got', n)
```

以这种方式使用`yield`的函数有时被称为“增强生成器（enhanced generator）”或“基于生成器的协程（generator-based coroutine）”。遗憾的是，这些术语不够精确，而且由于近年来“协程”更多地与异步函数相关联，使得情况变得更加混乱。为了避免这种混淆，我们将使用“增强生成器”这个术语，以明确我们讨论的仍然是使用`yield`的标准函数。

将`yield`用作表达式的函数仍然是一个生成器，但其用法有所不同。它不再是产生值，而是响应发送给它的值而执行。例如：

```python
>>> r = receiver()
>>> r.send(None)       # 推进到第一个 yield
Ready to receive
>>> r.send(1)
Got 1
>>> r.send(2)
Got 2
>>> r.send('Hello')
Got Hello
>>>
```

在这个例子中，初始调用`r.send(None)`是必要的，这样生成器才能执行到达第一个`yield`表达式之前的语句。此时，生成器挂起，等待通过相关联的生成器对象`r`的`send()`方法发送一个值。传递给`send()`的值由生成器中的`yield`表达式返回。在接收到值后，生成器会执行语句直到遇到下一个`yield`。

按照目前的写法，该函数将无限运行。可以使用`close()`方法来关闭生成器，如下所示：

```python
>>> r.close()
>>> r.send(4)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>>
```

`close()`操作会在生成器当前`yield`处引发一个`GeneratorExit`异常。通常情况下，这会导致生成器静默终止；如果你愿意，可以捕获该异常以执行清理操作。一旦关闭，如果再次向生成器发送值，将引发`StopIteration`异常。

可以使用`throw(ty[,val [,tb]])`方法在生成器内部引发异常，其中`ty`是异常类型，`val`是异常参数（或参数元组），`tb`是可选的回溯信息（traceback）。例如：

```python
>>> r = receiver()
Ready to receive
>>> r.throw(RuntimeError, "Dead")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "receiver.py", line 14, in receiver
    n = yield
RuntimeError: Dead
>>>
```

无论通过哪种方式引发的异常，都会从生成器中当前执行的`yield`语句向上传播。生成器可以选择捕获该异常并进行适当处理。如果生成器没有处理该异常，它将传播出生成器，在更高层级被处理。

## 6.6 增强生成器的应用

增强生成器是一种奇怪的编程结构。与自然地供给`for`循环的简单生成器不同，没有核心语言特性来驱动增强生成器。那么，为什么你会需要一个需要发送值给它的函数呢？这纯粹是学术探讨吗？

从历史上看，增强生成器一直被用于并发库中——尤其是那些基于异步 I/O 的库。在这种语境下，它们通常被称为“协程”或“基于生成器的协程”。然而，大部分这类功能已经合并到了 Python 的`async`和`await`特性中。对于那个特定的用例，几乎没有实际理由再使用`yield`。即便如此，它仍然有一些实际应用。

与生成器一样，增强生成器可用于实现不同类型的求值和控制流。一个例子是`contextlib`模块中的`@contextmanager`装饰器。例如：

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

在这里，生成器被用来将上下文管理器的两个部分粘合在一起。回想一下，上下文管理器是由实现以下协议的对象定义的：

```python
class Manager:
    def __enter__(self):
        return somevalue

    def __exit__(self, ty, val, tb):
        if ty:
            # 发生了异常
            ...
            # 如果已处理则返回 True，否则返回 False
```

通过`@contextmanager`生成器，`yield`语句之前的所有内容在管理器进入时执行（通过`__enter__()`方法）。`yield`之后的所有内容在管理器退出时执行（通过`__exit__()`方法）。如果发生了错误，它会作为异常在`yield`语句处报告。这是一个例子：

```python
>>> with manager() as val:
...         print(val)
...
Entering
somevalue
Leaving
>>> with manager() as val:
...         print(int(val))
...
Entering
An error occurred invalid literal for int() with base 10: 'somevalue'
Leaving
>>>
```

为了实现这一点，使用了一个包装类。这是一个简化的实现，用于阐明基本思路：

```python
class Manager:
    def __init__(self, gen):
        self.gen = gen

    def __enter__(self):
        # 运行到 yield
        return self.gen.send(None)

    def __exit__(self, ty, val, tb):
        # 传播异常（如果有）
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

扩展生成器的另一个应用是使用函数来封装一个“工作者（worker）”任务。函数调用的核心特性之一是它会建立一个局部变量环境。对这些变量的访问经过高度优化——比访问类和实例的属性要快得多。由于生成器在被显式关闭或销毁之前一直保持活跃，人们可以使用生成器来建立一个长生命周期的任务。这里有一个接收字节片段并将其组装成行的生成器示例：

```python
@consumer
def line_receiver():
    data = bytearray()
    line = None
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

在这个例子中，生成器接收收集到字节数组中的字节片段。如果数组包含换行符，则提取并返回一行。否则，返回`None`。以下是一个演示其工作方式的例子：

```python
>>> r = line_receiver()
>>> r.send(b'hello')
>>> r.send(b'world\nit ')
b'hello world\n'
>>> r.send(b'works!')
>>> r.send(b'\n')
b'it works!\n'
>>>
```

类似的代码可以用类来编写，如下所示：



```python
class LineReceiver:
    def __init__(self):
        self.data = bytearray()
        self.linecount = 0

    def send(self, part):
        self.linecount += part.count(b'\n')
        self.data.extend(part)
        if self.linecount > 0:
            index = self.data.index(b'\n')
            line = bytes(self.data[:index+1])
            self.data = self.data[index+1:]
            self.linecount -= 1
            return line
        else:
            return None
```

虽然编写类可能更熟悉，但代码更复杂且运行速度较慢。在作者的机器上测试，将大量数据块喂给接收器时，使用生成器比使用这个类代码快约 40–50%。大部分性能提升归功于消除了实例属性查找——局部变量速度更快。

虽然还有许多其他潜在应用，但需要记住的一点是，如果你看到 `yield` 被用于非迭代的语境中，它很可能使用了 `send()` 或 `throw()` 等增强特性。

## 6.7 生成器与 Awaiting 的桥梁

生成器函数的一个经典用途是在与异步 I/O 相关的库中，例如标准库的 `asyncio` 模块。然而，自 Python 3.5 起，这类功能大部分已被移至与 `async` 函数和 `await` 语句相关的不同语言特性中（参见第 5 章的最后一部分）。

`await` 语句实际上涉及与一个伪装的生成器进行交互。下面是一个示例，阐明了 `await` 所使用的底层协议：

```python
class Awaitable:
    def __await__(self):
        print('About to await')
        yield   # 必须是一个生成器
        print('Resuming')

# 与 "await" 兼容的函数。返回一个 "awaitable" 对象
def function():
    return Awaitable()

async def main():
    await function()
```

以下是你尝试使用 `asyncio` 运行该代码的方式：

```python
>>> import asyncio
>>> asyncio.run(main())
About to await
Resuming
>>>
```

绝对有必要了解它是如何工作的吗？可能没必要。所有这些机制通常都被隐藏在视线之外。然而，如果你发现自己在用 `async` 函数，只需知道内部某个地方埋着一个生成器函数即可。如果你坚持把技术债的坑挖得足够深，最终你一定会找到它的。

## 6.8 结语：生成器的简史与展望

生成器是 Python 最有趣的成功故事之一。它们也是关于迭代这个更宏大故事的一部分。迭代是所有编程任务中最常见的任务之一。在 Python 的早期版本中，迭代是通过序列索引和 `__getitem__()` 方法实现的。这后来演变成了基于 `__iter__()` 和 `__next__()` 方法的当前迭代协议。不久之后，生成器作为一种更便捷的实现迭代器的方式出现了。在现代 Python 中，几乎没有任何理由使用除生成器以外的其他方式来实现迭代器。即使在你自定义的可迭代对象中，`__iter__()` 方法本身也可以方便地以这种方式实现。

在随后的 Python 版本中，生成器在演进过程中获得了与协程相关的增强特性——`send()` 和 `throw()` 方法，从而承担了新的角色。这些方法不再局限于迭代，而是开启了在其他上下文中利用生成器的可能性。最显著的是，这构成了许多用于网络编程和并发的所谓“异步”框架的基础。然而，随着异步编程的演进，其中大部分内容已经转化为使用 `async/await` 语法的后续特性。因此，在迭代（生成器的原始用途）上下文之外看到生成器函数已不再常见。事实上，如果你发现自己在定义一个生成器函数且 *并非* 在执行迭代，你可能应该重新考虑你的方案。或许有更好或更现代的方法来完成你的工作。

# 7. 类与面向对象编程

类用于创建新类型的对象。本章涵盖了类的细节，但并不旨在成为关于面向对象编程和设计的深度参考手册。文中讨论了一些 Python 中常见的编程模式，以及你可以自定义类以实现有趣行为的方法。本章的整体结构是自顶向下的。首先描述使用类的高层概念和技术。在本章的后续部分，内容将变得更具技术性，并侧重于内部实现。

## 7.1 对象

Python 中的几乎所有代码都涉及创建 *对象* 并对其执行操作。例如，你可以创建一个字符串对象并如下操纵它：

```python
>>> s = "Hello World"
>>> s.upper()
'HELLO WORLD'
>>> s.replace('Hello', 'Hello Cruel')
'Hello Cruel World'
>>> s.split()
['Hello', 'World']
>>>
```

或者一个列表对象：

```python
>>> names = ['Paula', 'Thomas']
>>> names.append('Lewis')
>>> names
['Paula', 'Thomas', 'Lewis']
>>> names[1] = 'Tom'
>>>
```

每个对象的一个核心特性是它通常具有某种状态——字符串的字符、列表的元素等等，以及操作该状态的方法。方法通过对象本身调用——就像是通过点（`.`）运算符附加到对象上的函数一样。

对象总是有一个关联的类型。你可以使用 `type()` 来查看它：

```python
>>> type(names)
<class 'list'>
>>>
```

一个对象被说是其类型的 *实例*（instance）。例如，`names` 是 `list` 的一个实例。

## 7.2 `class` 语句

新对象使用 `class` 语句定义。一个类通常由一组构成方法的函数集合组成。这里有一个示例：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

    def inquiry(self):
        return self.balance
```

需要注意的是，类语句本身并不会创建类的任何实例。例如，在前例中并没有实际创建任何账户。相反，类仅仅持有以后创建的实例将可用的方法。你可以将其视为一个蓝图。

在类内部定义的函数被称为方法。实例方法是一个操作类实例的函数，该实例作为第一个参数传递。按照惯例，这个参数被称为 `self`。在前例中，`deposit()`、`withdraw()` 和 `inquiry()` 都是实例方法的例子。

类的 `__init__()` 和 `__repr__()` 方法是所谓特殊方法或魔术方法的例子。这些方法对解释器运行时具有特殊含义。`__init__()` 方法用于在创建新实例时初始化状态。`__repr__()` 方法返回一个用于查看对象的字符串。定义此方法是可选的，但这样做可以简化调试，并使在交互式提示符中查看对象变得更容易。

类定义可以可选地包含文档字符串和类型提示。例如：

```python
class Account:
    '''
    A simple bank account
    '''
    owner: str
    balance: float

    def __init__(self, owner: str, balance: float):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount: float):
        self.balance += amount

    def withdraw(self, amount: float):
        self.balance -= amount

    def inquiry(self) -> float:
        return self.balance
```

类型提示不会改变类的任何工作方式——也就是说，它们不会引入任何额外的检查或验证。它们纯粹是元数据，可能对第三方工具或 IDE 有用，或者被某些高级编程技术使用。在随后的大多数示例中不会使用它们。

## 7.3 实例

类的实例是通过将类对象像函数一样调用而创建的。这会创建一个新实例，然后将其传递给 `__init__()` 方法。`__init__()` 的参数包括新创建的实例 `self` 以及在调用类对象时提供的参数。例如：

```python
# 创建几个账户
a = Account('Guido', 1000.0)
# 调用 Account.__init__(a, 'Guido', 1000.0)

b = Account('Eva', 10.0)
# 调用 Account.__init__(b, 'Eva', 10.0)
```

在 `__init__()` 内部，通过赋值给 `self` 将属性保存到实例中。例如，`self.owner = owner` 就是在实例上保存一个属性。一旦新创建的实例被返回，这些属性以及类的方法都可以使用点（`.`）运算符访问：

```python
a.deposit(100.0)                # 调用 Account.deposit(a, 100.0)
b.withdraw(50.00)              # 调用 Account.withdraw(b, 50.0)
owner = a.owner                # 获取账户所有者
```

需要强调的是，每个实例都有自己的状态。你可以使用 `vars()` 函数查看实例变量。例如：

```python
>>> a = Account('Guido', 1000.0)
>>> b = Account('Eva', 10.0)
>>> vars(a)
{'owner': 'Guido', 'balance': 1000.0}
>>> vars(b)
{'owner': 'Eva', 'balance': 10.0}
>>>
```

注意这里没有出现方法。方法是在类上找到的。每个实例通过其关联的类型保留一个指向其类的链接。例如：

```python
>>> type(a)
<class 'Account'>
>>> type(b)
<class 'Account'>
>>> type(a).deposit
<function Account.deposit at 0x10a032158>
>>> type(a).inquiry
<function Account.inquiry at 0x10a032268>
>>>
```

后面的章节将讨论属性绑定的实现细节以及实例与类之间的关系。

## 7.4 属性访问

对实例可以执行的基本操作只有三种：获取、设置和删除属性。例如：

```python
>>> a = Account('Guido', 1000.0)
>>> a.owner                     # get
'Guido'
>>> a.balance = 750.0          # set
>>> del a.balance              # delete
>>> a.balance
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Account' object has no attribute 'balance'
>>>
```

Python 中的一切都是动态过程，限制非常少。如果你想在对象创建之后为其添加一个新属性，你可以随意这样做。例如：

```python
>>> a = Account('Guido', 1000.0)
>>> a.creation_date = '2019-02-14'
>>> a.nickname = 'Former BDFL'
>>> a.creation_date
'2019-02-14'
>>>
```

除了使用点号（`.`）来执行这些操作外，你还可以将属性名称作为字符串传递给 `getattr()`、`setattr()` 和 `delattr()` 函数。`hasattr()` 函数用于测试属性是否存在。例如：

```python
>>> a = Account('Guido', 1000.0)
>>> getattr(a, 'owner')
'Guido'
>>> setattr(a, 'balance', 750.0)
>>> delattr(a, 'balance')
>>> hasattr(a, 'balance')
False
>>> getattr(a, 'withdraw')(100)    # Method call
>>> a
Account('Guido', 650.0)
>>>
```

`a.attr` 和 `getattr(a, 'attr')` 是可以互换的，因此 `getattr(a, 'withdraw')(100)` 与 `a.withdraw(100)` 相同。无论 `withdraw()` 是否为方法都一样。

`getattr()` 函数的一个显著特点是可以接收一个可选的默认值。如果你想查找一个可能存在也可能不存在的属性，可以这样做：

```python
>>> a = Account('Guido', 1000.0)
>>> getattr(a, 'balance', 'unknown')
1000.0
>>> getattr(a, 'creation_date', 'unknown')
'unknown'
>>>
```

当你将方法作为属性访问时，你会得到一个被称为*绑定*（bound）方法的对象。例如：

```python
>>> a = Account('Guido', 1000.0)
>>> w = a.withdraw
>>> w
<bound method Account.withdraw of Account('Guido', 1000.0)>
>>> w(100)
>>> a
Account('Guido', 900.0)
>>>
```

绑定方法是一个同时包含实例（`self`）和实现该方法的函数的对象。当你通过添加括号和参数来调用绑定方法时，它会执行该方法，并将附加的实例作为第一个参数传递。例如，上述调用 `w(100)` 会转化为对 `Account.withdraw(a, 100)` 的调用。

## 7.5 作用域规则

虽然类为方法定义了一个独立的命名空间，但该命名空间并不作为方法内部所用名称的解析作用域。因此，在实现类时，对属性和方法的引用必须是限定完整的。例如，在方法中，你总是通过 `self` 来引用实例的属性。因此，你应该使用 `self.balance` 而不是 `balance`。如果你想从一个方法中调用另一个方法，情况同样如此。例如，假设你想通过存入负数来实现 `withdraw()`：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.deposit(-amount)  # Must use self.deposit()

    def inquiry(self):
        return self.balance
```

缺乏类级作用域是 Python 与 C++ 或 Java 不同的一个领域。如果你使用过那些语言，Python 中的 `self` 参数就相当于所谓的 "this" 指针，不同之处在于 Python 中你必须始终显式地使用它。

## 7.6 运算符重载与协议

在第 4 章中，我们讨论了 Python 的数据模型。我们特别关注了实现 Python 运算符和协议的所谓特殊方法。例如，`len(obj)` 函数会调用 `obj.__len__()`，而 `obj[n]` 会调用 `obj.__getitem__(n)`。

在定义新类时，定义其中一些方法是很常见的。`Account` 类中的 `__repr__()` 方法就是这样一个用于改善调试输出的方法。如果你在创建更复杂的东西（例如自定义容器），可能会定义更多此类方法。例如，假设你想创建一个账户组合（portfolio）：



```python
class AccountPortfolio:
    def __init__(self):
        self.accounts = []

    def add_account(self, account):
        self.accounts.append(account)

    def total_funds(self):
        return sum(account.inquiry() for account in self.accounts)

    def __len__(self):
        return len(self.accounts)

    def __getitem__(self, index):
        return self.accounts[index]

    def __iter__(self):
        return iter(self.accounts)

# Example
port = AccountPortfolio()
port.add_account(Account('Guido', 1000.0))
port.add_account(Account('Eva', 50.0))

print(port.total_funds())  # -> 1050.0
len(port)  # -> 2

# Print the accounts
for account in port:
    print(account)

# Access an individual account by index
port[1].inquiry()  # -> 50.0
```

出现在末尾的特殊方法（如 `__len__()`、`__getitem__()` 和 `__iter__()`）使得 `AccountPortfolio` 能够配合 Python 的运算符（如索引和迭代）工作。

有时你会听到 "Pythonic" 这个词，比如 "这段代码很 Pythonic"。这个术语是非正式的，但它通常是指一个对象是否能与 Python 环境的其他部分良好协作。这意味着在合理的范围内支持 Python 的核心特性，如迭代、索引和其他操作。你几乎总是通过让你的类实现第 4 章中描述的预定义特殊方法来完成这一点。

## 7.7 继承

继承是一种创建新类从而特化（specialize）或修改现有类行为的机制。原类被称为基类（base class）、超类（superclass）或父类（parent class）。新类被称为派生类（derived class）、子类（child class）、子类（subclass）或子类型（subtype）。当通过继承创建类时，它会继承基类定义的属性。然而，派生类可以重新定义这些属性中的任何一个，并添加自己的新属性。

继承在类语句中通过一个以逗号分隔的基类名称列表来指定。如果没有指定基类，类将隐式地继承自 `object`。`object` 是所有 Python 对象的根类；它提供了某些常用方法的默认实现，如 `__str__()` 和 `__repr__()`。

继承的一个用途是用新方法扩展现有类。例如，假设你想给 `Account` 添加一个 `panic()` 方法来取出所有资金。方法如下：

```python
class MyAccount(Account):
    def panic(self):
        self.withdraw(self.balance)

# Example
a = MyAccount('Guido', 1000.0)
a.withdraw(23.0)          # a.balance = 977.0
a.panic()                 # a.balance = 0
```

继承也可以用来重新定义已经存在的方法。例如，这是一个 `Account` 的特化版本，它重新定义了 `inquiry()` 方法，以定期夸大余额，希望某些不注意的人会在支付次级抵押贷款时透支账户并产生巨额罚款：

```python
import random
class EvilAccount(Account):
    def inquiry(self):
        if random.randint(0,4) == 1:
            return self.balance * 1.10
        else:
            return self.balance

a = EvilAccount('Guido', 1000.0)
a.deposit(10.0)           # Calls Account.deposit(a, 10.0)
available = a.inquiry()   # Calls EvilAccount.inquiry(a)
```

在这个例子中，`EvilAccount` 的实例与 `Account` 的实例完全相同，唯一的区别是重新定义了 `inquiry()` 方法。

有时，派生类在重新实现一个方法的同时，还需要调用原有的实现。方法可以使用 `super()` 显式地调用原方法：

```python
class EvilAccount(Account):
    def inquiry(self):
        if random.randint(0,4) == 1:
            return 1.10 * super().inquiry()
        else:
            return super().inquiry()
```

在这个示例中，`super()` 允许你访问一个此前定义过的方法。`super().inquiry()` 调用使用的是 `inquiry()` 在被 `EvilAccount` 重定义之前的原始定义。

虽然较不常见，但继承也可以用来为实例添加额外的属性。以下是如何将上述示例中的 1.10 因子改为一个可以调整的实例级属性：

```python
class EvilAccount(Account):
    def __init__(self, owner, balance, factor):
        super().__init__(owner, balance)
        self.factor = factor

    def inquiry(self):
        if random.randint(0,4) == 1:
            return self.factor * super().inquiry()
        else:
            return super().inquiry()
```

添加属性时一个棘手的问题是处理现有的 `__init__()` 方法。在这个示例中，我们定义了一个新版本的 `__init__()`，其中包含了额外的实例变量 `factor`。然而，当 `__init__()` 被重定义时，子类有责任如上所示地使用 `super().__init__()` 来初始化其父类。如果你忘记这样做，最终会得到一个初始化不完全的对象，从而导致所有功能崩溃。由于父类的初始化需要额外的参数，这些参数仍必须传递给子类的 `__init__()` 方法。

继承可能会以微妙的方式破坏代码。考虑 `Account` 类的 `__repr__()` 方法：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'
```

这个方法的目的是通过生成美观的输出辅助调试。然而，该方法硬编码使用了 `Account` 这个名称。如果你开始使用继承，你会发现输出是错误的：

```python
>>> class EvilAccount(Account):
...     pass
...
>>> a = EvilAccount('Eva', 10.0)
>>> a
Account('Eva', 10.0)    # 注意这里有误导性的输出
>>> type(a)
<class 'EvilAccount'>
>>>
```

为了修复这个问题，你需要修改 `__repr__()` 方法以使用正确的类型名称。例如：

```python
class Account:
    ...
    def __repr__(self):
        return f'{type(self).__name__}({self.owner!r}, {self.balance!r})'
```

现在你会看到更准确的输出。并不是每个类都会使用继承，但如果你在编写类时预见到会有这种用例，你就需要注意这类细节。一般而言，应避免硬编码类名。

继承在类型系统中建立了一种关系，即任何子类在类型检查时都被视为父类。例如：

```python
>>> a = EvilAccount('Eva', 10)
>>> type(a)
<class 'EvilAccount'>
>>> isinstance(a, Account)
True
>>>
```

这就是所谓的“是一个（is a）”关系：`EvilAccount` 是一个 `Account`。有时，“是一个”继承关系被用来定义对象类型的本体论或分类法。例如：

```python
class Food:
    pass

class Sandwich(Food):
    pass

class RoastBeef(Sandwich):
    pass

class GrilledCheese(Sandwich):
    pass

class Taco(Food):
    pass
```

在实践中，以这种方式组织对象可能相当困难且充满风险。假设你想在上述层级结构中添加一个 `HotDog` 类。它应该放在哪里？考虑到热狗有面包卷，你可能会倾向于将其设为 `Sandwich` 的子类。然而，基于面包卷整体的弧形形状以及内部美味的填充物，也许热狗实际上更像一个 `Taco`。也许你决定让它同时成为两者的子类：

```python
class HotDog(Sandwich, Taco):
    pass
```

此时，所有人都崩溃了，办公室陷入了激烈的争论。这正好是个提及 Python 支持多重继承的好时机。为此，只需将多个类列为父类即可。生成的子类将继承所有父类的组合特性。关于多重继承的更多内容，请参阅第 7.19 节。

## 7.8 通过组合避免继承

继承的一个担忧是所谓的“实现继承（implementation inheritance）”。为了说明这一点，假设你想创建一个具有 `push` 和 `pop` 操作的栈数据结构。一种快捷的方法是继承 `list` 并为其添加一个新方法：

```python
class Stack(list):
    def push(self, item):
        self.append(item)

# 示例
s = Stack()
s.push(1)
s.push(2)
s.push(3)
s.pop()      # -> 3
s.pop()      # -> 2
```

确实，这个数据结构像栈一样工作，但它也拥有 `list` 的所有其他特性——插入、排序、切片重新赋值等等。这就是实现继承——你利用继承来复用一些代码并在此基础上构建其他功能，但你也获得了一堆与实际要解决的问题无关的特性。用户可能会觉得这个对象很奇怪：为什么一个栈会有排序方法？

更好的方法是组合。不要通过继承 `list` 来构建栈，而应该将栈构建为一个独立的类，恰好在内部包含一个 `list`。内部包含一个 `list` 是一个实现细节。例如：

```python
class Stack:
    def __init__(self):
        self._items = list()

    def push(self, item):
        self._items.append(item)

    def pop(self):
        return self._items.pop()

    def __len__(self):
        return len(self._items)

# 示例用法
s = Stack()
s.push(1)
s.push(2)
s.push(3)
s.pop()      # -> 3
s.pop()      # -> 2
```

这个对象的工作方式与之前完全相同，但它专注于只做一个栈。没有多余的 `list` 方法或非栈特性。其目的更加明确。

这种实现的一个微小扩展是接受内部列表类作为一个可选参数：

```python
class Stack:
    def __init__(self, *, container=None):
        if container is None:
            container = list()
        self._items = container

    def push(self, item):
        self._items.append(item)

    def pop(self):
        return self._items.pop()

    def __len__(self):
        return len(self._items)
```

这种方法的一个好处是它促进了组件的松耦合。例如，你可能想创建一个将元素存储在类型化数组（typed array）而不是列表中的栈。你可以这样做：

```python
import array

s = Stack(container=array.array('i'))
s.push(42)
s.push(23)
s.push('a lot')    # TypeError.
```

这也是一个所谓的 *依赖注入（dependency injection）* 的例子。你没有将 `Stack` 硬编码为依赖于 `list`，而是使其可以依赖于用户决定传入的任何容器，只要该容器实现了所需的接口。

更广泛地说，将内部列表设为隐藏的实现细节与数据抽象问题相关。也许你后来决定甚至不想使用列表。上述设计使得更改变得简单。例如，如果你将实现改为使用如下的链式元组，`Stack` 的用户甚至不会察觉：

```python
class Stack:
    def __init__(self):
        self._items = None
        self._size = 0

    def push(self, item):
        self._items = (item, self._items)
        self._size += 1

    def pop(self):
        (item, self._items) = self._items
        self._size -= 1
        return item

    def __len__(self):
        return self._size
```

在决定是否使用继承时，你应该退一步问问自己：你构建的对象是父类的一个特化版本，还是仅仅将其作为构建其他东西的一个组件。如果是后者，请不要使用继承。

## 7.9 通过函数避免继承

有时你会发现自己编写的类只有一个需要定制的方法。例如，也许你写了一个像这样的数据解析类：

```python
class DataParser:
    def parse(self, lines):
        records = []
```

```python
for line in lines:
    row = line.split(',')
    
    record = self.make_record(row)
    records.append(row)
return records
```

```python
def make_record(self, row):
    raise NotImplementedError()
```

```python
class PortfolioDataParser(DataParser):
    def make_record(self, row):
        return {
            'name': row[0],
            'shares': int(row[1]),
            'price': float(row[2])
        }
```

```python
parser = PortfolioDataParser()
data = parser.parse(open('portfolio.csv'))
```

这里的“管线”工作（plumbing）太多了。如果你在编写大量仅包含单个方法的类，请考虑改用函数。例如：

```python
def parse_data(lines, make_record):
    records = []
    for line in lines:
        row = line.split(',')
        record = make_record(row)
        records.append(row)
    return records

def make_dict(row):
    return {
        'name': row[0],
        'shares': int(row[1]),
        'price': float(row[2])
    }
```

```python
data = parse_data(open('portfolio.csv'), make_dict)
```



这段代码要简单得多，而且同样灵活，此外简单的函数更容易测试。如果以后需要将其扩展为类，你随时可以这样做。过早的抽象通常不是一件好事。

## 7.10 动态绑定与鸭子类型

动态绑定是 Python 在运行时用于查找对象属性的机制。这使得 Python 能够处理实例而无需关心其类型。在 Python 中，变量名没有关联的类型。因此，属性绑定过程与`obj`是什么样的对象无关。如果你进行一次查找，例如`obj.name`，只要任何一个`obj`恰好拥有`name`属性，它就能正常工作。这种行为有时被称为鸭子类型（duck typing）——源于这样一句格言：“如果它看起来像鸭子，叫起来像鸭子，走起来像鸭子，那么它就是一只鸭子。”

Python 程序员经常编写依赖于这种行为的程序。例如，如果你想创建一个现有对象的自定义版本，你可以选择继承它，或者创建一个外观和行为都像它但除此之外毫无关系的全新对象。后一种方法通常用于保持程序组件之间的松耦合。例如，代码可以被编写为与任何对象协作，只要该对象拥有一组特定的方法。最常见的例子之一是标准库中定义的各种可迭代对象。有各种各样的对象可以通过`for`循环产生值——列表、文件、生成器、字符串等等。然而，它们都没有继承自任何特殊的`Iterable`基类。它们仅仅实现了执行迭代所需的方法——而且一切都能正常运行。

## 7.11 继承内置类型的危险

Python 允许继承内置类型。然而，这样做会带来风险。举个例子，如果你决定子类化`dict`以强制所有键为大写，你可能会像这样重新定义`__setitem__()`方法：

```python
class udict(dict):
    def __setitem__(self, key, value):
        super().__setitem__(key.upper(), value)
```

事实上，起初它看起来确实有效：

```python
>>> u = udict()
>>> u['name'] = 'Guido'
>>> u['number'] = 37
>>> u
{ 'NAME': 'Guido', 'NUMBER': 37 }
>>>
```

然而，进一步使用会发现它只是“看起来”有效。事实上，它根本就没有真正起作用：

```python
>>> u = udict(name='Guido', number=37)
>>> u
{ 'name': 'Guido', 'number': 37 }
>>> u.update(color='blue')
>>> u
{ 'name': 'Guido', 'number': 37, 'color': 'blue' }
>>>
```

这里的问题在于，Python 的内置类型并不是像普通的 Python 类那样实现的——它们是用 C 实现的。大多数方法在 C 的世界中运行。例如，`dict.update()`方法直接操作字典数据，而从未通过你在自定义`udict`类中重新定义的`__setitem__()`方法。

`collections`模块提供了特殊的类`UserDict`、`UserList`和`UserString`，可用于创建`dict`、`list`和`str`类型的安全子类。例如，你会发现这个解决方案效果好得多：

```python
from collections import UserDict

class udict(UserDict):
    def __setitem__(self, key, value):
        super().__setitem__(key.upper(), value)
```

以下是这个新版本在实际运行中的示例：

```python
>>> u = udict(name='Guido', num=37)
>>> u.update(color='Blue')
>>> u
{'NAME': 'Guido', 'NUM': 37, 'COLOR': 'Blue'}
>>> v = udict(u)
>>> v['title'] = 'BDFL'
>>> v
{'NAME': 'Guido', 'NUM': 37, 'COLOR': 'Blue', 'TITLE': 'BDFL'}
>>>
```

大多数情况下，可以避免子类化内置类型。例如，在构建新容器时，最好创建一个新类，如 7.8 节中`Stack`类的示例。如果你确实需要子类化内置类型，其工作量可能比你想象的要大得多。

## 7.12 类变量与类方法

在类定义中，所有函数都被假设为操作一个实例，该实例始终作为第一个参数`self`传递。然而，类本身也是一个对象，可以携带状态并被操作。例如，你可以使用类变量`num_accounts`来追踪创建了多少个实例：

```python
class Account:
    num_accounts = 0

    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance
        Account.num_accounts += 1

    def __repr__(self):
        return f'{type(self).__name__} ({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.deposit(-amount)    # 必须使用 self.deposit()

    def inquiry(self):
        return self.balance
```

类变量定义在普通的`__init__()`方法之外。要修改它们，请使用类而不是`self`。例如：

```python
>>> a = Account('Guido', 1000.0)
>>> b = Account('Eva', 10.0)
>>> Account.num_accounts
2
>>>
```

虽然有点不寻常，但类变量也可以通过实例访问。例如：

```python
>>> a.num_accounts
2
>>> c = Account('Ben', 50.0)
>>> Account.num_accounts
3
>>> c.num_accounts
3
>>>
```

这样做能成功是因为在实例上进行属性查找时，如果在实例本身上找不到匹配的属性，它会检查关联的类。这与 Python 通常查找方法的方式相同。

此外，还可以定义所谓的类方法。类方法是应用于类本身而非实例的方法。类方法的一个常见用途是定义替代的实例构造函数。例如，假设有一个需求，需要从旧的企业级输入格式创建`Account`实例：

```python
data = '''
<account>
    <owner>Guido</owner>
    <amount>1000.0</amount>
</account>
'''
```

为此，你可以编写一个像这样的`@classmethod`：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    @classmethod
    def from_xml(cls, data):
        from xml.etree.ElementTree import XML
        doc = XML(data)
        return cls(doc.findtext('owner'), float(doc.findtext('amount')))
```

```python
# 使用示例
data = '''
<account>
    <owner>Guido</owner>
    <amount>1000.0</amount>
</account>
'''
a = Account.from_xml(data)
```

类方法的第一个参数始终是类本身。按照惯例，这个参数通常被命名为`cls`。在这个例子中，`cls`被设置为`Account`。如果类方法的目的是创建新实例，则必须采取显式步骤来实现。在示例的最后一行中，调用`cls(..., ...)`与对这两个参数调用`Account(..., ...)`是一样的。

类作为参数传递这一事实解决了一个与继承相关的重要问题。假设你定义了一个...的子类

`Account`并且现在想要创建该类的一个实例。你会发现它仍然有效：

```python
class EvilAccount(Account):
    pass

e = EvilAccount.from_xml(data)   # 创建一个 'EvilAccount' 实例
```

这段代码之所以有效，是因为`EvilAccount`现在被作为`cls`传递。因此，`from_xml()`类方法的最后一条语句现在创建的是一个`EvilAccount`实例。

类变量和类方法有时被结合使用，用来配置和控制实例的操作方式。作为另一个例子，考虑以下`Date`类：

```python
import time

class Date:
    datefmt = '{year}-{month:02d}-{day:02d}'
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    def __str__(self):
        return self.datefmt.format(year=self.year,
                                   month=self.month,
                                   day=self.day)

    @classmethod
    def from_timestamp(cls, ts):
        tm = time.localtime(ts)
        return cls(tm.tm_year, tm.tm_mon, tm.tm_mday)

    @classmethod
    def today(cls):
        return cls.from_timestamp(time.time())
```

这个类包含一个类变量`datefmt`，用于调整`__str__()`方法的输出。这是可以通过继承来定制的：

```python
class MDYDate(Date):
    datefmt = '{month}/{day}/{year}'

class DMYDate(Date):
    datefmt = '{day}/{month}/{year}'

# 示例
a = Date(1967, 4, 9)
print(a)        # 1967-04-09

b = MDYDate(1967, 4, 9)
print(b)        # 4/9/1967

c = DMYDate(1967, 4, 9)
print(c)        # 9/4/1967
```

像这样通过类变量和继承进行配置，是调整实例行为的常用工具。类方法的使用对于实现这一点至关重要，因为它们确保了创建出正确类型的对象。例如：

```python
a = MDYDate.today()
b = DMYDate.today()
print(a)    # 2/13/2019
print(b)    # 13/2/2019
```

到目前为止，实例的替代构造方式是类方法最常见的用途。此类方法的一种通用命名约定是包含`from_`作为前缀，例如`from_timestamp()`。你会看到这种命名约定被广泛应用于标准库和第三方包的类方法中。例如，字典有一个类方法，用于从一组键创建预初始化字典：

```python
>>> dict.from_keys(['a','b','c'], 0)
{'a': 0, 'b': 0, 'c': 0}
```

关于类方法的一个注意事项是，Python 并没有将它们管理在一个与实例方法分开的命名空间中。结果是，它们仍然可以在实例上被调用。例如：

```python
d = Date(1967, 4, 9)
b = d.today()    # 调用 Date.today(Date)
```

这可能会相当令人困惑，因为调用`d.today()`实际上与实例`d`没有任何关系。然而，在 IDE 和文档中，你可能会看到`today()`被列为`Date`实例的有效方法。

## 7.13 静态方法

有时一个类仅仅被用作函数的命名空间，这些函数使用`@staticmethod`声明为静态方法。与普通方法或类方法不同，静态方法不接收额外的`self`或`cls`参数。静态方法就是一个恰好定义在类内部的普通函数。例如：

```python
class Ops:
    @staticmethod
    def add(x, y):
        return x + y

    @staticmethod
    def sub(x, y):
        return x - y
```

通常你不需要创建此类类的实例。相反，直接通过类调用这些函数：

```python
a = Ops.add(2, 3)        # a = 5
b = Ops.sub(4, 5)        # b = -1
```

有时其他类会使用这样的一组静态方法来实现“可交换”或“可配置”的行为，或者作为一种对导入模块行为的宽松模拟。思考在之前的`Account`示例中使用继承的情况：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'{type(self).__name__} ({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

    def inquiry(self):
        return self.balance

# 一个特殊的 "Evil" 账户
class EvilAccount(Account):
    def deposit(self, amount):
        self.balance += 0.95 * amount

    def inquiry(self):
        if random.randint(0,4) == 1:
            return 1.10 * self.balance
        else:
            return self.balance
```

这里使用继承有点奇怪。它引入了两种不同类型的对象：`Account`和`EvilAccount`。而且没有明显的方法可以将现有的`Account`实例转换为`EvilAccount`或反之，因为这涉及到更改实例类型。也许将“邪恶”表现为一种账户策略（policy）会更好。下面是一个使用静态方法实现的`Account`替代方案：



```python
class StandardPolicy:
    @staticmethod
    def deposit(account, amount):
        account.balance += amount

    @staticmethod
    def withdraw(account, amount):
        account.balance -= amount

    @staticmethod
    def inquiry(account):
        return account.balance

class EvilPolicy(StandardPolicy):
    @staticmethod
    def deposit(account, amount):
        account.balance += 0.95 * amount

    @staticmethod
    def inquiry(account):
        if random.randint(0,4) == 1:
            return 1.10 * account.balance
        else:
            return account.balance

class Account:
    def __init__(self, owner, balance, *, policy=StandardPolicy):
        self.owner = owner
        self.balance = balance
        self.policy = policy

    def __repr__(self):
        return f'Account({self.policy}, {self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.policy.deposit(self, amount)

    def withdraw(self, amount):
        self.policy.withdraw(self, amount)

    def inquiry(self):
        return self.policy.inquiry(self)
```

在这种重新构建中，只创建一种类型的实例：`Account`。然而，它有一个特殊的 `policy` 属性，提供了各种方法的具体实现。如果需要，可以在现有的 `Account` 实例上动态更改策略：

```python
>>> a = Account('Guido', 1000.0)
>>> a.policy
<class 'StandardPolicy'>
>>> a.deposit(500)
>>> a.inquiry()
1500.0
>>> a.policy = EvilPolicy
>>> a.deposit(500)
>>> a.inquiry()         # 可能会随机多出 1.10 倍
1975.0
```

在这里使用 `@staticmethod` 的原因之一是，没有必要创建 `StandardPolicy` 或 `EvilPolicy` 的实例。这些类的主要目的是组织一组方法，而不是存储与 `Account` 相关的额外实例数据。尽管如此，Python 的松耦合特性当然允许将策略升级为持有自己的数据。像这样将静态方法更改为普通的实例方法：

```python
class EvilPolicy(StandardPolicy):
    def __init__(self, deposit_factor, inquiry_factor):
        self.deposit_factor = deposit_factor
        self.inquiry_factor = inquiry_factor

    def deposit(self, account, amount):
        account.balance += self.deposit_factor * amount

    def inquiry(self, account):
        if random.randint(0,4) == 1:
            return self.inquiry_factor * account.balance
        else:
            return account.balance
```

```python
# Example use
a = Account('Guido', 1000.0, policy=EvilPolicy(0.95, 1.10))
```

这种将方法委托给辅助类的方法，是状态机和类似对象的常用实现策略。每个操作状态都可以封装在自己的方法类中（通常是静态方法）。然后可以使用一个可变的实例变量（例如本例中的 `policy` 属性）来持有与当前操作状态相关的具体实现细节。

## 7.14 关于设计模式

在编写面向对象程序时，程序员有时会执着于实现命名的设计模式——例如“策略模式”、“享元模式”、“单例模式”等等。其中许多模式源自 Erich Gamma, Richard Helm, Ralph Johnson 和 John Vlissides 所著的著名书籍 *Design Patterns*。

如果你熟悉这些模式，其他语言中使用的通用设计原则当然也可以应用于 Python。然而，许多记录在案的模式旨在解决 C++ 或 Java 严格的静态类型系统所带来的特定问题。Python 的动态特性使得许多此类模式变得过时、过度设计或根本不需要。

即便如此，编写优秀软件仍有一些核心原则——例如力求编写可调试、可测试且可扩展的代码。一些基础策略，如为类编写有用的 `__repr__()` 方法、优先使用组合而非继承，以及允许依赖注入，对于实现这些目标大有裨益。Python 程序员还喜欢编写所谓的“Pythonic”代码。通常这意味着对象遵循各种内置协议，如迭代、容器或上下文管理。例如，Python 程序员不会尝试实现 Java 编程书中某种奇异的数据遍历模式，而可能会通过一个向 `for` 循环提供数据的生成器函数来实现，或者直接用几次字典查询替换整个模式。

## 7.15 数据封装与私有属性

在 Python 中，类的所有属性和方法都是 *public*（公开的），也就是说，访问它们没有任何限制。在需要隐藏或封装内部实现细节的面向对象应用中，这种情况通常是不理想的。

为了解决这个问题，Python 依赖命名约定来暗示预期用途。其中一个约定是：以单个前导下划线 (`_`) 开头的名称表示内部实现。例如，这里是一个 `Account` 类的版本，其中余额已被转换为“私有”属性：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self._balance!r})'

    def deposit(self, amount):
        self._balance += amount

    def withdraw(self, amount):
        self._balance -= amount

    def inquiry(self):
        return self._balance
```

在这段代码中，`_balance` 属性旨在作为内部细节。没有任何机制能阻止用户直接访问它，但前导下划线是一个强烈的信号，提示用户应该寻找更面向公开的接口——例如 `Account.inquiry()` 方法。

一个灰色地带是内部属性是否可用于子类。例如，之前的继承示例是否允许直接访问其父类的 `_balance` 属性？

```python
class EvilAccount(Account):
    def inquiry(self):
        if random.randint(0,4) == 1:
            return 1.10 * self._balance
        else:
            return self._balance
```

根据通用原则，这在 Python 中被认为是可接受的。IDE 和其他工具可能会暴露此类属性。如果你来自 C++、Java 或其他类似的面向对象语言，可以将 `_balance` 视为类似于“protected”（受保护）的属性。

如果你希望属性更加私有，请在名称前加上两个前导下划线 (`__`)。所有类似 `__name` 的名称都会被自动重命名为 `_Classname__name` 形式的新名称。这确保了在超类中使用的私有名称不会被子类中相同的名称覆盖。以下示例说明了这一行为：

```python
class A:
    def __init__(self):
        self.__x = 3      # 混淆为 self._A__x

    def __spam(self):     # 混淆为 _A__spam()
        print('A.__spam', self.__x)

    def bar(self):
        self.__spam()     # 仅调用 A.__spam()


class B(A):
    def __init__(self):
        A.__init__(self)
        self.__x = 37     # 混淆为 self._B__x

    def __spam(self):     # 混淆为 _B__spam()
        print('B.__spam', self.__x)

    def grok(self):
        self.__spam()     # 调用 B.__spam()
```

在这个例子中，有两个不同的赋值给了 `__x` 属性。此外，看起来类 B 试图通过继承来重写 `__spam()` 方法，但事实并非如此。名称混淆（Name mangling）导致每个定义都使用了唯一的名称。尝试以下示例：

```python
>>> b = B()
>>> b.bar()
A.__spam 3
>>> b.grok()
B.__spam 37
>>>
```

如果你查看底层的实例变量，可以直接看到混淆后的名称：

```python
>>> vars(b)
{ '_A__x': 3, '_B__x': 37 }
>>> b._A__spam()
A.__spam 3
>>> b._B__spam()
B.__spam 37
>>>
```

虽然这种方案提供了数据隐藏的错觉，但并没有实际机制来防止访问类的“私有”属性。特别是，如果已知类名和对应的私有属性名，仍然可以使用混淆后的名称来访问。如果对这种私有属性的访问仍有顾虑，你也许可以考虑更严格的代码审查流程。

乍一看，名称混淆似乎是一个额外的处理步骤。然而，混淆过程实际上只在类定义时发生一次。它不会在方法执行期间发生，也不会增加程序执行的额外开销。请注意，在 `getattr()`、`hasattr()`、`setattr()` 或 `delattr()` 等属性名以字符串指定形式传递的函数中，不会发生名称混淆。对于这些函数，你需要显式地使用混淆后的名称（如 `_Classname__name`）来访问属性。

在实践中，最好不要过度思考名称的私有性。单下划线名称非常常见，双下划线名称则较少见。虽然你可以采取进一步措施尝试真正隐藏属性，但额外的精力和增加的复杂度很难带来对等的收益。也许最有用的一点是记住：如果你在名称上看到前导下划线，它几乎肯定某种内部细节，最好不要去动它。

## 7.16 类型提示

用户定义类的属性在类型或值上没有约束。事实上，你可以将属性设置为任何你想要的任何东西。例如：

```python
>>> a = Account('Guido', 1000.0)
>>> a.owner
'Guido'
>>> a.owner = 37
>>> a.owner
37
>>> b = Account('Eva', 'a lot')
>>> b.deposit(' more')
>>> b.inquiry()
'a lot more'
>>>
```

如果这是一个实际的顾虑，有几种可能的解决方案。一种很简单——不要那样做！另一种是依赖外部工具，如 linter 和类型检查器。为此，类允许为选定属性指定可选的类型提示。例如：

```python
class Account:
    owner: str          # 类型提示
    _balance: float     # 类型提示

    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance
    ...
```

引入类型提示不会改变类的实际运行时行为——也就是说，没有额外的检查发生，也没有任何东西能阻止用户在代码中设置错误的值。然而，这些提示可以在编辑器的提示中给用户提供更有用的信息，从而在不经意的使用错误发生前将其防止。

在实践中，准确的类型提示可能很困难。例如，`Account` 类是否允许某人使用 `int` 而不是 `float`？或者使用 `Decimal` 呢？你会发现所有这些都能正常工作，尽管提示似乎暗示并非如此。

```python
from decimal import Decimal
```

```python
a = Account('Guido', Decimal('1000.0'))
a.withdraw(Decimal('50.0'))
print(a.inquiry())    # -> 950.0
```

在这种情况下，如何正确组织类型已经超出了本书的讨论范围。当你犹豫不决时，除非你正在积极使用能够对代码进行类型检查的工具，否则最好不要凭直觉猜测。

## 7.17 属性 (Properties)

正如前一节所述，Python 在运行时不对属性的值或类型进行任何限制。然而，如果你将一个属性置于所谓的*属性 (property)* 管理之下，这种强制执行就成为可能。*属性* 是一种特殊的属性，它能拦截对属性的访问，并通过*用户定义*的方法来处理。这些方法拥有完全的自由，可以根据需要管理该属性。这里有一个示例：

```python
import string

class Account:

    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance

    @property
    def owner(self):
        return self._owner

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

在这里，`owner` 属性被限制为一个非常“企业级”的 10 字符大写 ASCII 字符串。当你尝试使用该类时，其工作方式如下：

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
>>> a.owner = 'RAMAKRISHNAN'
Traceback (most recent call last):
...
ValueError: Must be 10 characters or less
>>>
```

`@property` 装饰器用于将一个属性建立为“属性”。在本例中，它被应用于 `owner` 属性。该装饰器总是首先应用于一个获取属性值的方法。在这种情况下，该方法返回存储在私有属性 `_owner` 中的实际值。随后的 `@owner.setter` 装饰器用于选择性地实现一个设置属性值的方法。该方法在将值存储到私有属性 `_owner` 之前，会进行各种类型和值的检查。



属性的一个关键特性是，与之关联的名称（例如示例中的 `owner`）变得“神奇”了。也就是说，对该属性的任何使用都会自动路由到你实现的 getter/setter 方法中。你不需要修改任何现有代码即可实现此功能。例如，无需对 `Account.__init__()` 方法进行任何更改。这可能会让你感到惊讶，因为 `__init__()` 执行的是 `self.owner = owner` 赋值，而不是使用私有属性 `self._owner`。这正是设计使然——`owner` 属性的核心目的就是验证属性值。你肯定希望在创建实例时就进行验证。你会发现它的运行效果完全符合预期：

```python
>>> a = Account('Guido', 1000.0)

Traceback (most recent call last):
  File "account.py", line 5, in __init__
    self.owner = owner
  File "account.py", line 15, in owner
    raise ValueError('Must be uppercase ASCII')
ValueError: Must be uppercase ASCII
>>>
```

由于对属性的每次访问都会自动调用一个方法，因此实际值需要存储在一个不同的名称下。这就是为什么在 getter 和 setter 方法内部使用 `_owner` 的原因。你不能使用 `owner` 作为存储位置，因为那样会导致无限递归。

通常，属性允许拦截任何特定的属性名称。你可以实现获取、设置或删除属性值的方法。例如：

```python
class SomeClass:
    @property
    def attr(self):
        print('Getting')

    @attr.setter
    def attr(self, value):
        print('Setting', value)

    @attr.deleter
    def attr(self):
        print('Deleting')

# Example
s = SomeClass()
s.attr          # Getting
s.attr = 13     # Setting 13
del s.attr      # Deleting
```

并不需要实现属性的所有部分。事实上，通常使用属性来实现在线计算的只读数据属性。例如：

```python
class Box(object):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    @property
    def area(self):
        return self.width * self.height

    @property
    def perimeter(self):
        return 2*self.width + 2*self.height

# Example use
b = Box(4, 5)
print(b.area)        # -> 20
print(b.perimeter)  # -> 18
b.area = 5          # Error: can't set attribute
```

在定义类时需要考虑的一点是，尽量使编程接口保持统一。如果没有属性，某些值将作为简单属性访问（如 `b.width` 或 `b.height`），而其他值则作为方法访问（如 `b.area()` 和 `b.perimeter()`）。记住何时需要添加额外的 `()` 会造成不必要的困惑。属性可以帮助解决这个问题。

Python 程序员经常没有意识到，方法本身就被隐式地处理为一种属性。考虑这个类：

```python
class SomeClass:
    def yow(self):
        print('Yow!')
```

当用户创建实例（如 `s = SomeClass()`）然后访问 `s.yow` 时，返回的并不是原始函数对象 `yow`。相反，你会得到一个像这样的绑定方法（bound method）：

```python
>>> s = SomeClass()
>>> s.yow
<bound method SomeClass.yow of <__main__.SomeClass object at 0x10e2572b0>>
>>>
```

这是怎么发生的？事实证明，当函数被放置在类中时，它们的行为非常像属性。具体来说，函数会神奇地拦截属性访问，并在幕后创建绑定方法。当你使用 `@staticmethod` 和 `@classmethod` 定义静态方法和类方法时，你实际上是在改变这个过程。`@staticmethod` 将方法函数“原样”返回，不进行任何特殊的封装或处理。关于此过程的更多信息将在 7.28 节中介绍。

## 7.18 类型、接口与抽象基类（Types, Interfaces, and Abstract Base Classes）

当你创建类的一个实例时，该实例的类型就是类本身。要测试一个对象是否属于某个类，请使用内置函数 `isinstance(obj, cls)`。如果对象 `obj` 属于类 `cls` 或任何派生自 `cls` 的类，该函数将返回 `True`。这里有一个示例：

```python
class A:
    pass

class B(A):
    pass

class C:
    pass

a = A()                # 'A' 的实例
b = B()                # 'B' 的实例
c = C()                # 'C' 的实例

type(a)                # 返回类对象 A
isinstance(a, A)       # 返回 True
isinstance(b, A)       # 返回 True，B 派生自 A
isinstance(b, C)       # 返回 False，B 未派生自 C
```

类似地，内置函数 `issubclass(A, B)` 如果类 `A` 是类 `B` 的子类，则返回 `True`。这里有一个示例：

```python
issubclass(B, A)    # 返回 True
issubclass(C, A)    # 返回 False
```

类类型关系的一个常见用途是指定编程接口。例如，可以实现一个顶级基类来指定编程接口的要求。然后，该基类可用于类型提示，或通过 `isinstance()` 进行防御性的类型强制执行：

```python
class Stream:

    def receive(self):
        raise NotImplementedError()

    def send(self, msg):
        raise NotImplementedError()

    def close(self):
        raise NotImplementedError()

# Example.
def send_request(stream, request):
    if not isinstance(stream, Stream):
        raise TypeError('Expected a Stream')
    stream.send(request)
    return stream.receive()
```

这类代码的预期并不是直接使用 `Stream`。相反，不同的类将继承 `Stream` 并实现所需的功能。用户将实例化这些类中的一个。例如：

```python
class SocketStream(Stream):
    def receive(self):
        ...
```

```python
def send(self, msg):
    ...

def close(self):
    ...

class PipeStream(Stream):
    def receive(self):
        ...

    def send(self, msg):
        ...

    def close(self):
        ...
```

### 示例

```python
s = SocketStream()
send_request(s, request)
```

在这个示例中，值得讨论的是 `send_request()` 中接口的运行时强制执行。是否应该改用类型提示（type hint）？

点击此处查看代码图片

### 将接口指定为类型提示

```python
def send_request(stream:Stream, request):
    stream.send(request)
    return stream.receive()
```

由于类型提示不会被强制执行，因此如何根据接口验证参数的决定实际上取决于你希望验证何时发生——是在运行时、作为代码检查步骤，还是完全不验证。

这种使用接口类的方法在大型框架和应用程序的组织中更为常见。然而，使用这种方法，你需要确保子类确实实现了所需的接口。例如，如果子类选择不实现其中一个必需的方法，或者出现了简单的拼写错误，其影响最初可能不会被察觉，因为代码在常见情况下可能仍然可以工作。然而，随后如果调用了未实现的方法，程序将会崩溃。当然，这种情况通常只会在凌晨 3:30 的生产环境中发生。

为了防止这个问题，通常使用 `abc` 模块将接口定义为抽象基类（abstract base classes）。该模块定义了一个基类（`ABC`）和一个装饰器（`@abstractmethod`），两者结合使用来描述一个接口。这是一个示例：

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

    @abstractmethod
    def close(self):
        pass
```

抽象类不旨在被直接实例化。事实上，如果你尝试创建一个 `Stream` 实例，你会得到一个错误：

点击此处查看代码图片

```python
>>> s = Stream()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class Stream with abstract methods close, receive, send
>>>
```

错误消息准确地告诉你 `Stream` 需要实现哪些方法。这为编写子类提供了指南。假设你编写了一个子类但犯了一个错误：

点击此处查看代码图片

```python
class SocketStream(Stream):
    def read(self):
        ...
        # 命名错误

    def send(self, msg):
        ...

    def close(self):
        ...
```

抽象基类将在实例化时捕获该错误。这非常有用，因为错误能被及早发现。

点击此处查看代码图片

```python
>>> s = SocketStream()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class SocketStream with abstract methods receive
>>>
```

虽然抽象类不能被实例化，但它可以定义方法和属性供子类使用。此外，基类中的抽象方法仍然可以在子类中被调用。例如，在子类中调用 `super().receive()` 是允许的。

## 7.19 多重继承、接口与 Mixins

Python 支持多重继承。如果一个子类列出了多个父类，该子类将继承所有父类的特性。例如：

```python
class Duck:
    def walk(self):
        print('Waddle')

class Trombonist:
    def noise(self):
        print('Blat!')

class DuckBonist(Duck, Trombonist):
    pass

d = DuckBonist()
d.walk()        # -> Waddle
d.noise()       # -> Blat!
```

从概念上讲，这是一个很棒的想法，但随后实际情况开始显现。例如，当 `Duck` 和 `Trombonist` 各自定义一个 `__init__()` 方法时会发生什么？或者如果它们都定义了 `noise()` 方法呢？突然间，你会意识到多重继承充满了危险。

为了更好地理解多重继承的实际用途，请退后一步，将其视为一种用于组织和代码复用的高度专业化工具，而非一种通用编程技术。具体来说，将一组任意且不相关的类通过多重继承组合在一起，以此创造奇怪的变异鸭子音乐家，并不是标准做法。千万不要这样做。

多重继承更常见的用途是组织类型和接口关系。例如，上一节介绍了抽象基类的概念。抽象基类的目的是指定一个编程接口。例如，你可能会有如下各种抽象类：

```python
from abc import ABC, abstractmethod

class Stream(ABC):
    @abstractmethod
    def receive(self):
        pass

    @abstractmethod
    def send(self, msg):
        pass

    @abstractmethod
    def close(self):
        pass

class Iterable(ABC):
    @abstractmethod
    def __iter__(self):
        pass
```

有了这些类，多重继承可用于指定子类实现了哪些接口：

点击此处查看代码图片

```python
class MessageStream(Stream, Iterable):
    def receive(self):
        ...

    def send(self):
        ...

    def close(self):
        ...

    def __iter__(self):
        ...
```

再次强调，这里对多重继承的使用并非为了实现细节，而是为了类型关系。例如，在这个例子中，继承的方法甚至没有任何实际操作，不存在代码复用。主要的是，继承关系允许你执行如下的类型检查：

点击此处查看代码图片

```python
m = MessageStream()

isinstance(m, Stream)    # -> True
isinstance(m, Iterable)  # -> True
```

多重继承的另一个用途是定义 mixin 类（mixin classes）。Mixin 类是一个修改或扩展其他类功能的类。考虑以下类定义：

点击此处查看代码图片

```python
class Duck:
    def noise(self):
        return 'Quack'

    def waddle(self):
        return 'Waddle'

class Trombonist:
    def noise(self):
        return 'Blat!'

    def march(self):
        return 'Clomp'

class Cyclist:
    def noise(self):
        return 'On your left!'

    def pedal(self):
        return 'Pedaling'
```

这些类彼此完全无关。它们之间没有继承关系，且实现了不同的方法。

然而，它们有一个共同点，即都定义了一个 `noise()` 方法。以此为线索，你可以定义以下类：

点击此处查看代码图片

```python
class LoudMixin:
    def noise(self):
        return super().noise().upper()

class AnnoyingMixin:
    def noise(self):
        return 3*super().noise()
```

乍一看，这些类似乎有问题。它们只有一个孤立的方法，并且使用 `super()` 将调用委托给一个不存在的父类。这些类甚至无法正常工作：

点击此处查看代码图片

```python
>>> a = AnnoyingMixin()
>>> a.noise()
Traceback (most recent call last):
...
AttributeError: 'super' object has no attribute 'noise'
>>>
```

这些就是 Mixin 类。它们唯一能工作的方式是与其他实现了缺失功能的类相结合。例如：

点击此处查看代码图片



```python
class LoudDuck(LoudMixin, Duck):
    pass

class AnnoyingTrombonist(AnnoyingMixin, Trombonist):
    pass

class AnnoyingLoudCyclist(AnnoyingMixin, LoudMixin, Cyclist):
    pass

d = LoudDuck()
d.noise() # -> 'QUACK'

t = AnnoyingTrombonist()
t.noise() # -> 'Blat!Blat!Blat!'

c = AnnoyingLoudCyclist()
c.noise() # -> 'ON YOUR LEFT!ON YOUR LEFT!ON YOUR LEFT!'
```

由于 `Mixin` 类的定义方式与普通类相同，因此最好在类名中包含 `"Mixin"` 字样。这种命名约定能提供更清晰的目的说明。

要充分理解 Mixins，你需要进一步了解继承和 `super()` 函数的工作原理。

首先，每当你使用继承时，Python 都会构建一个类线性链，称为*方法解析顺序*（Method Resolution Order），简称 MRO。这可以通过类的 `__mro__` 属性获取。以下是一些单继承的示例：

点击此处查看代码图片

```python
class Base:
    pass

class A(Base):
    pass

class B(A):
    pass

Base.__mro__ # -> (<class 'Base'>, <class 'object'>)
A.__mro__ # -> (<class 'A'>, <class 'Base'>, <class 'object'>)
B.__mro__ # -> (<class 'B'>, <class 'A'>, <class 'Base'>, <class 'object'>)
```

MRO 指定了属性查找的搜索顺序。具体来说，每当你搜索实例或类上的属性时，MRO 列表中的每个类都会按列出顺序被检查。当找到第一个匹配项时，搜索停止。`object` 类被列在 MRO 中，是因为所有类都继承自 `object`，无论它是否被列为父类。

为了支持多重继承，Python 实现了所谓的“协作式多重继承（cooperative multiple inheritance）”。在协作式继承中，所有类根据两条主要的排序规则被放置在 MRO 列表中。第一条规则规定，子类必须始终在任何父类之前被检查。第二条规则规定，如果一个类有多个父类，这些父类必须按照它们在子类继承列表中编写的顺序被检查。

在大多数情况下，这些规则产生的 MRO 是合理的。然而，对类进行排序的精确算法实际上相当复杂，并不是基于深度优先或广度优先搜索等简单方法。相反，排序是根据 C3 线性化算法确定的，该算法在论文 `"A Monotonic Superclass Linearization for Dylan"`（K. Barrett 等人发表于 OOPSLA'96）中有详细描述。

该算法一个微妙之处在于，某些类层级结构会被 Python 拒绝并抛出 `TypeError`。这里有一个示例：

```python
class X: pass
class Y(X): pass
class Z(X,Y): pass  # TypeError.
                    # Can't create consistent MRO
```

在这种情况下，方法解析算法拒绝类 `Z`，因为它无法确定一个合理的基类排序。这里，类 `X` 在继承列表中出现在类 `Y` 之前，因此必须先检查 `X`。然而，类 `Y` 继承自 `X`，所以如果先检查 `X`，就违反了子类优先检查的规则。

在实践中，这些问题很少出现——如果出现了，通常表明存在更严重的设计问题。

作为一个实践中 MRO 的示例，这里是之前展示的 `AnnoyingLoudCyclist` 类的 MRO：

```python
class AnnoyingLoudCyclist(AnnoyingMixin, LoudMixin, Cyclist):
    pass

AnnoyingLoudCyclist.__mro__
# (<class 'AnnoyingLoudCyclist'>, <class 'AnnoyingMixin'>,
# <class 'LoudMixin'>, <class 'Cyclist'>, <class 'object'>)
```

在这个 MRO 中，你可以看到两条规则是如何被满足的。具体来说，任何子类始终列在其父类之前。`object` 类列在最后，因为它是所有其他类的父类。多个父类按照它们在代码中出现的顺序排列。

`super()` 函数的行为与底层的 MRO 绑定在一起。具体来说，它的作用是将属性委托给 MRO 上的下一个类。这是基于使用 `super()` 的类。

例如，当 `AnnoyingMixin` 类使用 `super()` 时，它会查看实例的 MRO 以找到自己的位置。然后，它将属性查找委托给下一个类。在这个例子中，在 `AnnoyingMixin` 类中使用 `super().noise()` 会调用 `LoudMixin.noise()`。这是因为 `LoudMixin` 是 `AnnoyingLoudCyclist` 的 MRO 中列出的下一个类。

接着，`LoudMixin` 类中的 `super().noise()` 操作会委托给 `Cyclist` 类。对于任何 `super()` 的使用，下一个类的选择根据实例的类型而变化。例如，如果你创建一个 `AnnoyingTrombonist` 的实例，那么 `super().noise()` 将改为调用 `Trombonist.noise()`。

为协作式多重继承和 mixins 设计是一项挑战。这里有一些设计指南。

首先，在 MRO 中，子类总是先于任何基类被检查。因此，mixins 共享一个共同父类，并且该父类提供方法的空实现是很常见的。如果同时使用多个 mixin 类，它们将依次排列。共同父类将出现在最后，在此它可以提供默认实现或错误检查。例如：

```python
class NoiseMixin:
    def noise(self):
        raise NotImplementedError('noise() not implemented')

class LoudMixin(NoiseMixin):
    def noise(self):
        return super().noise().upper()

class AnnoyingMixin(NoiseMixin):
    def noise(self):
        return 3 * super().noise()
```

第二个指南是，mixin 方法的所有实现应该具有相同的函数签名。mixin 的一个问题是它们是可选的，并且经常以不可预测的顺序混合在一起。为了使其工作，你必须保证无论下一个类是什么，涉及 `super()` 的操作都能成功。为此，调用链中的所有方法都需要具有兼容的调用签名。

最后，你需要确保在所有地方都使用 `super()`。有时你会遇到一个直接调用其父类的类：

```python
class Base:
    def yow(self):
        print('Base.yow')

class A(Base):
    def yow(self):
        print('A.yow')
        Base.yow(self)     # 直接调用父类

class B(Base):
    def yow(self):
        print('B.yow')
        super().yow()

class C(A, B):
    pass

c = C()
c.yow()
# 输出:
#    A.yow
#    Base.yow
```

此类类在多重继承中使用是不安全的。这样做会破坏正确的方法调用链并导致混乱。例如，在上述示例中，尽管 `B.yow()` 是继承层级的一部分，但从未出现其输出。如果你在处理多重继承，应该使用 `super()` 而不是直接调用超类中的方法。

## 7.20 基于类型的分发

有时你需要编写基于特定类型进行分发的代码。例如：

```python
if isinstance(obj, Duck):
    handle_duck(obj)
elif isinstance(obj, Trombonist):
    handle_trombonist(obj)
elif isinstance(obj, Cyclist):
    handle_cyclist(obj)
else:
    raise RuntimeError('Unknown object')
```

这样庞大的 `if-elif-else` 块是不优雅且脆弱的。一个常用的解决方案是通过字典进行分发：

```python
handlers = {
    Duck: handle_duck,
    Trombonist: handle_trombonist,
    Cyclist: handle_cyclist
}

# 分发
def dispatch(obj):
    func = handlers.get(type(obj))
    if func:
        return func(obj)
    else:
        raise RuntimeError(f'No handler for {obj}')
```

该方案假设类型精确匹配。如果在此类分发中还需要支持继承，则需要遍历 MRO：

```python
def dispatch(obj):
    for ty in type(obj).__mro__:
        func = handlers.get(ty)
        if func:
            return func(obj)
    raise RuntimeError(f'No handler for {obj}')
```

有时分发是通过使用 `getattr()` 的基于类的接口来实现的，如下所示：

```python
class Dispatcher:
    def handle(self, obj):
        for ty in type(obj).__mro__:
            meth = getattr(self, f'handle_{ty.__name__}', None)
            if meth:
                return meth(obj)
        raise RuntimeError(f'No handler for {obj}')

    def handle_Duck(self, obj):
        ...

    def handle_Trombonist(self, obj):
        ...

    def handle_Cyclist(self, obj):
        ...

# 示例
dispatcher = Dispatcher()
dispatcher.handle(Duck())      # -> handle_Duck()
dispatcher.handle(Cyclist())   # -> handle_Cyclist()
```

最后这个使用 `getattr()` 将分发到类方法的示例是一个相当常见的编程模式。

## 7.21 类装饰器

有时你希望在类定义之后执行额外的处理步骤——例如将类添加到注册表中或生成额外的支持代码。一种方法是使用类装饰器。类装饰器是一个以类作为输入并以类作为输出的函数。例如，以下是如何维护一个注册表：

```python
_registry = { }
def register_decorator(cls):
    for mt in cls.mimetypes:
        _registry[mt.mimetype] = cls
    return cls
```

```python
# 使用注册表的工厂函数
def create_decoder(mimetype):
    return _registry[mimetype]()
```

在这个例子中，`register_register_decoder()` 函数会检查类中是否具有 `mimetuples` 属性。如果找到了，它会将该类添加到一个将 MIME 类型映射到类对象的字典中。要使用这个函数，你只需将其作为装饰器放在类定义之前：

```python
@register_decoder
class TextDecoder:
    mimetuples = [ 'text/plain' ]
    def decode(self, data):
        ...

@register_decoder
class HTMLDecoder:
    mimetuples = [ 'text/html' ]
    def decode(self, data):
        ...

@register_decoder
class ImageDecoder:
    mimetuples = [ 'image/png', 'image/jpg', 'image/gif' ]
    def decode(self, data):
        ...
```

```python
# 使用示例
decoder = create_decoder('image/jpg')
```

类装饰器可以随意修改它所接收的类的内容。例如，它甚至可以重写现有的方法。这是 mixin 类或多重继承的一种常见替代方案。例如，考虑以下装饰器：

```python
def loud(cls):
    orig_noise = cls.noise
    def noise(self):
        return orig_noise(self).upper()
    cls.noise = noise
    return cls

def annoying(cls):
    orig_noise = cls.noise
    def noise(self):
        return 3 * orig_noise(self)
    cls.noise = noise
    return cls

@annoying
@loud
class Cyclist(object):
    def noise(self):
        return 'On your left!'

    def pedal(self):
        return 'Pedaling'
```

这个例子产生的结果与前一节中 mixin 的例子相同。但是，这里没有多重继承，也没有使用 `super()`。在每个装饰器内部，对 `cls.noise` 的查找执行的操作与 `super()` 相同。但由于这仅在应用装饰器时（定义时）发生一次，因此最终对 `noise()` 的调用运行速度会稍微快一些。

类装饰器也可以用来创建全新的代码。例如，在编写类时，一个常见的任务是编写一个有用的 `__repr__()` 方法以改进调试：

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __repr__(self):
        return f'{type(self).__name__} ({self.x!r}, {self.y!r})'
```

编写这类方法通常很繁琐。或许类装饰器可以为你创建这个方法？

```python
import inspect
def with_repr(cls):
    args = list(inspect.signature(cls).parameters)
    argvals = ', '.join('{self.%s!r}' % arg for arg in args)
    code = 'def __repr__(self):\n'
    code += f' return f"{cls.__name__}({argvals})"\n'
    locs = { }
    exec(code, locs)
    cls.__repr__ = locs['__repr__']
    return cls

# 示例
@with_repr
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

在这个例子中，`__repr__()` 方法是根据 `__init__()` 方法的调用签名生成的。该方法被创建为一个文本字符串，并传递给 `exec()` 来创建函数。然后该函数被附加到类上。

标准库的部分内容中也使用了类似的代码生成技术。例如，定义数据结构的一种便捷方法是使用 dataclass：

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int
```

dataclass 会根据类的类型提示自动创建诸如 `__init__()` 和 `__repr__()` 之类的方法。这些方法使用 `exec()` 创建，与之前的例子类似。以下是生成的 Point 类的运行方式：

```python
>>> p = Point(2, 3)
>>> p
Point(x=2, y=3)
>>>
```

这种方法的一个缺点是启动性能较差。使用 `exec()` 动态创建代码会绕过 Python 通常应用于模块的编译优化。因此，以这种方式定义大量类可能会显著减慢代码的导入速度。

本节所示的示例阐明了类装饰器的常见用途——注册、代码重写、代码生成、验证等等。类装饰器的一个问题是它们必须显式地应用于每个使用的类。这并不总是理想的。下一节将介绍一种允许隐式操作类的功能。



## 7.22 监督继承（Supervised Inheritance）

正如你在前一节中看到的，有时你想要定义一个类并执行额外的操作。类装饰器是实现这一目标的机制之一。然而，父类也可以代表其子类执行额外操作。这是通过实现`__init_subclass__(cls)`类方法来完成的。例如：

```python
class Base:
    @classmethod
    def __init_subclass__(cls):
        print('Initializing', cls)

# 示例（每个类都应看到 'Initializing' 消息）
class A(Base):
    pass

class B(A):
    pass
```

如果存在`__init_subclass__()`方法，它将在定义任何子类时自动触发。即使子类深埋在继承层级中，这种情况也会发生。

许多通常使用类装饰器执行的任务可以使用`__init_subclass__()`来代替。例如，类注册：

```python
class DecoderBase:
    _registry = { }

    @classmethod
    def __init_subclass__(cls):
        for mt in cls.mimetypes:
            DecoderBase._registry[mt.mimetype] = cls

# 使用注册表的工厂函数
def create_decoder(mimetype):
    return DecoderBase._registry[mimetype]()

class TextDecoder(DecoderBase):
    mimetypes = [ 'text/plain' ]

    def decode(self, data):
        ...

class HTMLDecoder(DecoderBase):
    mimetypes = [ 'text/html' ]

    def decode(self, data):
        ...

class ImageDecoder(DecoderBase):
    mimetypes = [ 'image/png', 'image/jpg', 'image/gif' ]

    def decode(self, data):
        ...

# 使用示例
decoder = create_decoder('image/jpg')
```

这是一个类示例，它根据类`__init__()`方法的签名自动创建`__repr__()`方法：

```python
import inspect

class Base:
    @classmethod
    def __init_subclass__(cls):
        # 创建一个 __repr__ 方法
        args = list(inspect.signature(cls).parameters)
        argvals = ', '.join('{self.%s!r}' % arg for arg in args)

        code = 'def __repr__(self):\n'
        code += f' return f\"{cls.__name__}({argvals})\"\n'
        locs = {}
        exec(code, locs)
        cls.__repr__ = locs['__repr__']

class Point(Base):
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

如果使用了多重继承，你应该使用`super()`，以确保所有实现了`__init_subclass__()`的类都被调用。例如：

```python
class A:
    @classmethod
    def __init_subclass__(cls):
        print('A.init_subclass')
        super().__init_subclass__()

class B:
    @classmethod
    def __init_subclass__(cls):
        print('B.init_subclass')
        super().__init_subclass__()

# 这里应该看到两个类的输出
class C(A, B):
    pass
```

使用`__init_subclass__()`监督继承是 Python 最强大的定制功能之一。其大部分威力来自于它的隐式特性。顶级基类可以使用它来安静地监督整个子类层级。这种监督可以注册类、重写方法、执行验证等等。

## 7.23 对象生命周期与内存管理

当一个类被定义时，生成的类就是用于创建新实例的工厂。例如：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

# 创建一些 Account 实例
a = Account('Guido', 1000.0)
b = Account('Eva', 25.0)
```

实例的创建分两步进行：使用创建新实例的特殊方法`__new__()`以及初始化该实例的`__init__()`方法。例如，操作`a = Account('Guido', 1000.0)`执行以下步骤：

```python
a = Account.__new__(Account, 'Guido', 1000.0)
if isinstance(a, Account):
    Account.__init__(a, 'Guido', 1000.0)
```

除了第一个参数（是类而不是实例）之外，`__new__()`通常接收与`__init__()`相同的参数。然而，`__new__()`的默认实现直接忽略了它们。你有时会看到`__new__()`仅以单个参数被调用。例如，这段代码同样有效：

```python
a = Account.__new__(Account)
Account.__init__(a, 'Guido', 1000.0)
```

直接使用`__new__()`方法并不常见，但有时它被用来在绕过`__init__()`方法调用的情况下创建实例。其中一个用途是在类方法（class methods）中。例如：

```python
import time

class Date:

    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    @classmethod
    def today(cls):
        t = time.localtime()
        self = cls.__new__(cls)     # 创建实例
        self.year = t.tm_year
        self.month = t.tm_month
        self.day = t.tm_day
        return self
```

执行对象序列化的模块（如`pickle`）在反序列化对象时也会利用`__new__()`来重建实例。这一过程完全不需要调用`__init__()`。

有时，如果类希望改变实例创建的某些方面，它会定义`__new__()`。典型的应用包括实例缓存、单例模式和不可变性。例如，你可能希望`Date`类执行日期驻留（date interning）——也就是说，缓存并复用具有相同年、月、日的`Date`实例。以下是一种可能的实现方式：

```python
class Date:

    _cache = { }

    @staticmethod
    def __new__(cls, year, month, day):
        self = Date._cache.get((year, month, day))
        if not self:
            self = super().__new__(cls)
            self.year = year
            self.month = month
            self.day = day
            Date._cache[year, month, day] = self
        return self

    def __init__(self, year, month, day):
        pass
```

```python
# 示例
d = Date(2012, 12, 21)
e = Date(2012, 12, 21)
assert d is e        # 同一个对象
```

在这个例子中，类内部维护了一个之前创建的`Date`实例字典。在创建新`Date`时，首先会查询缓存。如果找到匹配项，则返回该实例。否则，创建一个新实例并进行初始化。

这个方案的一个微妙细节是空的`__init__()`方法。尽管实例被缓存了，但每次调用`Date()`仍然会触发`__init__()`。为了避免重复工作，该方法简单地不做任何处理——实例的创建实际上在第一次创建实例时在`__new__()`中完成了。

有一些方法可以避免对`__init__()`的额外调用，但需要一些巧妙的技巧。一种方法是让`__new__()`返回一个完全不同类型的实例——例如，属于另一个类的实例。另一种解决方案（稍后描述）是使用元类（metaclass）。

实例一旦被创建，就由引用计数（reference counting）来管理。如果引用计数达到零，实例会被立即销毁。当实例即将被销毁时，解释器首先查找与该对象关联的`__del__()`方法并调用它。例如：

```python
class Account(object):
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __del__(self):
        print('Deleting Account')
```

```python
>>> a = Account('Guido', 1000.0)
>>> del a
Deleting Account
>>>
```

偶尔，程序会像这样使用`del`语句来删除对对象的引用。如果这导致对象的引用计数达到零，则会调用`__del__()`方法。然而，通常情况下，`del`语句并不会直接调用`__del__()`，因为在其他地方可能还存在该对象的引用。对象被删除还有很多其他方式——例如，重新给变量名赋值，或者变量在函数中超出作用域：

```python
>>> a = Account('Guido', 1000.0)
>>> a = 42
Deleting Account
>>> def func():
...     a = Account('Guido', 1000.0)
...
>>> func()
Deleting Account
>>>
```

在实践中，类很少需要定义`__del__()`方法。唯一的例外是当对象的销毁需要额外的清理操作时——例如关闭文件、关闭网络连接或释放其他系统资源。即使在这些情况下，依赖`__del__()`来进行正确关闭也是危险的，因为无法保证该方法会在你认为它应该被调用的时候被调用。为了确保资源能干净地关闭，你应该为对象提供一个显式的`close()`方法。你还应该让你的类支持上下文管理器协议，以便它可以与`with`语句一起使用。下面是一个涵盖所有情况的示例：

```python
class SomeClass:
    def __init__(self):
        self.resource = open_resource()

    def __del__(self):
        self.close()

    def close(self):
        self.resource.close()

    def __enter__(self):
        return self

    def __exit__(self, ty, val, tb):
        self.close()

# 通过 __del__() 关闭
s = SomeClass()
del s

# 显式关闭
s = SomeClass()
s.close()

# 在上下文块结束时关闭
with SomeClass() as s:
    ...
```

再次强调，在类中编写`__del__()`几乎永远是不必要的。Python 已经有了垃圾回收机制，除非在对象销毁时需要执行某些额外操作，否则根本不需要这么做。即便如此，你可能仍然不需要`__del__()`，因为对象可能已经被编程为在你不采取任何行动的情况下也能正确地清理自身。

除了引用计数和对象销毁带来的风险外，某些编程模式——尤其是涉及父子关系、图或缓存的模式——可能会导致对象创建所谓的*引用循环（reference cycle）*。这里有一个例子：

```python
class SomeClass:
    def __del__(self):
        print('Deleting')

parent = SomeClass()
child = SomeClass()

# 创建子父引用循环
parent.child = child
child.parent = parent

# 尝试删除（__del__ 没有输出）
del parent
del child
```

在这个例子中，变量名被销毁了，但你从未看到`__del__()`方法被执行。这两个对象各自持有对方的内部引用，因此引用计数永远无法降至`0`。为了处理这种情况，一个特殊的循环检测垃圾回收器会定期运行。最终这些对象会被回收，但很难预测这会在何时发生。如果你想强制进行垃圾回收，可以调用`gc.collect()`。`gc`模块还提供了许多其他与循环垃圾回收器和内存监控相关的函数。

由于垃圾回收的时间不可预测，`__del__()`方法受到了一些限制。首先，任何从`__del__()`向上传播的异常都会被打印到`sys.stderr`，但除此之外会被忽略。其次，`__del__()`方法应避免执行诸如获取锁或其他资源的操作。这样做可能会导致死锁，因为`__del__()`可能会在执行与信号处理和线程无关的函数内部的第七层回调循环中出乎意料地被触发。如果你必须定义`__del__()`，请保持其简单。

## 7.24 弱引用

有时，当你更希望对象被销毁时，它们却被保持存活。在之前的例子中，展示了一个具有内部实例缓存的`Date`类。该实现的一个问题是，实例永远无法从缓存中被移除。因此，缓存会随着时间的推移而变得越来越大。

解决这个问题的一种方法是使用`weakref`模块创建弱引用（weak reference）。弱引用是一种在不增加对象引用计数的情况下创建对象引用的方法。要使用弱引用，你必须添加一段额外的代码来检查被引用对象是否仍然存在。以下是如何创建弱引用的示例：

```python
>>> a = Account('Guido', 1000.0)
>>> import weakref
>>> a_ref = weakref.ref(a)
>>> a_ref
```

```python
<weakref at 0x104617188; to 'Account' at 0x1046105c0>
>>>
```

与普通引用不同，弱引用（weak reference）允许原始对象被回收。例如：

```python
>>> del a
>>> a_ref
<weakref at 0x104617188; dead>
>>>
```

弱引用包含一个对对象的可选引用。要获取实际对象，需要将弱引用作为无参数函数进行调用。这将返回被指向的对象或`None`。例如：

```python
acct = a_ref()

if acct is not None:
    acct.withdraw(10)

# 另一种写法
if acct := a_ref():
    acct.withdraw(10)
```

弱引用通常与缓存和其他高级内存管理结合使用。下面是一个修改后的`Date`类，当不再有引用存在时，它会自动将对象从缓存中移除：



```python
import weakref

class Date:
    _cache = { }

    @staticmethod
    def __new__(cls, year, month, day):
        selfref = Date._cache.get((year, month, day))
        if not selfref:
            self = super().__new__(cls)
            self.year = year
            self.month = month
            self.day = day
            Date._cache[year, month, day] = weakref.ref(self)
        else:
            self = selfref()
        return self

    def __init__(self, year, month, day):
        pass

    def __del__(self):
        del Date._cache[self.year, self.month, self.day]
```

这可能需要花点时间研究，但下面的交互式会话展示了它的工作原理。请注意，一旦不再有对其的引用，缓存项是如何被移除的：

```python
>>> Date._cache
{}
>>> a = Date(2012, 12, 21)
>>> Date._cache
{(2012, 12, 21): <weakref at 0x10c7ee2c8; to 'Date' at 0x10c805518>}
>>> b = Date(2012, 12, 21)
>>> a is b
True
>>> del a
>>> Date._cache
{(2012, 12, 21): <weakref at 0x10c7ee2c8; to 'Date' at 0x10c805518>}
>>> del b
>>> Date._cache
{}
>>>
```

正如前面提到的，类的 `__del__()` 方法仅在对象的引用计数达到零时被调用。在本例中，第一个 `del a` 语句降低了引用计数。然而，由于仍然有另一个指向同一个对象的引用，该对象仍然保留在 `Date._cache` 中。当第二个对象被删除时，`__del__()` 被调用，缓存被清除。

对弱引用的支持要求实例具有可变的 `__weakref__` 属性。用户定义类的实例默认通常具有此属性。然而，内置类型和某些特殊数据结构（如命名元组、带有 `slots` 的类）则没有。如果你想为这些类型创建弱引用，可以通过定义添加了 `__weakref__` 属性的变体来实现：

```python
class wdict(dict):
    __slots__ = ('__weakref__',)

w = wdict()
w_ref = weakref.ref(w)     # 现在可以工作了
```

这里使用 `slots` 是为了避免不必要的内存开销，稍后将详细解释。

## 7.25 内部对象表示与属性绑定

与实例关联的状态存储在一个可以通过实例的 `__dict__` 属性访问的字典中。该字典包含每个实例独有的数据。示例如下：

```python
>>> a = Account('Guido', 1100.0)
>>> a.__dict__
{'owner': 'Guido', 'balance': 1100.0}
```

可以在任何时候向实例添加新属性：

```python
a.number = 123456 # 向 a.__dict__ 添加属性 'number'
a.__dict__['number'] = 654321
```

除非属性由 `property` 管理，否则对实例的修改总是会反映在本地 `__dict__` 属性中。同样，如果你直接修改 `__dict__`，这些修改也会反映在属性中。

实例通过一个特殊的 `__class__` 属性链接回它们的类。类本身也只是一个薄层，其上方是一个可以通过其自身的 `__dict__` 属性找到的字典。类字典是存放方法的地方。例如：

```python
>>> a.__class__
<class '__main__.Account'>
>>> Account.__dict__.keys()
dict_keys(['__module__', '__init__', '__repr__', 'deposit', 'withdraw', 'inquiry', '__dict__', '__weakref__', '__doc__'])
>>> Account.__dict__['withdraw']
<function Account.withdraw at 0x108204158>
>>>
```

类通过一个特殊的 `__bases__` 属性链接到它们的基类，该属性是一个基类元组。`__bases__` 属性仅用于提供信息。继承的实际运行时实现使用了 `__mro__` 属性，它是一个按搜索顺序排列的所有父类元组。这个底层结构是所有获取、设置或删除实例属性操作的基础。

每当使用 `obj.name = value` 设置属性时，都会调用特殊方法 `obj.__setattr__('name', value)`。如果使用 `del obj.name` 删除属性，则调用特殊方法 `obj.__delattr__('name')`。除非请求的属性恰好对应于 `property` 或描述符（descriptor），否则这些方法的默认行为是修改或删除 `obj` 本地 `__dict__` 中的值。在这种情况下，设置和删除操作将由与该 `property` 关联的设置和删除函数执行。

对于属性查找（如 `obj.name`），会调用特殊方法 `obj.__getattribute__('name')`。该方法执行属性搜索，通常包括检查 `property`、在本地 `__dict__` 中查找、检查类字典以及搜索 MRO。如果搜索失败，将通过调用类的 `obj.__getattribute__('name')` 方法（如果定义了）进行最后一次尝试。如果仍然失败，则抛出 `AttributeError` 异常。

如果需要，用户定义类可以实现自己的属性访问函数。例如，下面是一个限制可设置属性名称的类：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __setattr__(self, name, value):
        if name not in {'owner', 'balance'}:
            raise AttributeError(f'No attribute {name}!')
        super().__setattr__(name, value)

# 示例
a = Account('Guido', 1000.0)
a.balance = 940.25       # 正常
a.amount = 540.2         # AttributeError: No attribute amount
```

重新实现这些方法的类应该依赖于 `super()` 提供的默认实现来执行实际的属性操作。这是因为默认实现处理了类的高级特性，例如描述符和 `property`。如果你不使用 `super()`，你将不得不自己处理这些细节。

## 7.26 代理、包装器与委托

有时类会在另一个对象周围实现一个包装层（wrapper layer）以创建一种代理对象（proxy object）。代理是一个暴露与另一个对象相同接口的对象，但出于某种原因，它并不通过继承与原对象相关联。这与组合（composition）不同，组合是从其他对象创建完全的新对象，但具有自己独特的一组方法和属性。

在许多实际场景中会出现这种情况。例如，在分布式计算中，对象的实际实现可能位于云端的远程服务器上。与该服务器交互的客户端可能会使用一个看起来像服务器上对象的代理，但在后台，它通过网络消息将其所有方法调用委托（delegate）出去。

代理的一种常用实现技术涉及 `__getattr__()` 方法。这是一个简单的示例：

```python
class A:
    def spam(self):
        print('A.spam')

    def grok(self):
        print('A.grok')
```

```python
def yow(self):
    print('A.yow')

class LoggedA:
    def __init__(self):
        self._a = A()
    def __getattr__(self, name):
        print("Accessing", name)
        # Delegate to internal A instance
        return getattr(self._a, name)
```

```python
# Example use
a = LoggedA()
a.spam()      # prints "Accessing spam" and "A.spam"
a.yow()       # prints "Accessing yow" and "A.yow"
```

委派（Delegation）有时被用作继承的替代方案。这里有一个示例：

```python
class A:
    def spam(self):
        print('A.spam')

    def grok(self):
        print('A.grok')

    def yow(self):
        print('A.yow')

class B:
    def __init__(self):
        self._a = A()

    def grok(self):
        print('B.grok')

    def __getattr__(self, name):
        return getattr(self._a, name)
```

```python
# Example use
b = B()
b.spam()        # -> A.spam
b.grok()        # -> B.grok  (redefined method)
b.yow()         # -> A.yow
```

在这个例子中，看起来类 B 像是继承了类 A 并重新定义了一个方法。这确实是观察到的行为——但实际上并没有使用继承。相反，B 在内部持有一个 A 的引用。A 的某些方法可以被重新定义。然而，所有其他的方法都通过 `__getattr__()` 方法被委派。

通过 `__getattr__()` 转发属性查找是一种常用技术。但请注意，它不适用于映射到特殊方法的操作。例如，考虑这个类：

```python
class ListLike:
    def __init__(self):
        self._items = list()

    def __getattr__(self, name):
        return getattr(self._items, name)
```

```python
# Example
a = ListLike()
a.append(1)            # Works
a.insert(0, 2)         # Works
a.sort()               # Works
len(a)                        # Fails. No __len__() method
a[0]                        # Fails. No __getitem__() method
```

在这里，该类成功地将所有标准列表方法（`list.sort()`、`list.append()` 等）转发给内部列表。然而，Python 的标准运算符都无法工作。要使它们工作，你必须显式地实现所需的特殊方法。例如：

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

## 7.27 使用 `__slots__` 减少内存使用

正如我们所见，实例将其数据存储在字典中。如果你创建大量实例，这可能会引入大量的内存开销。如果你知道属性名称是固定的，可以在名为 `__slots__` 的特殊类变量中指定这些名称。这里有一个例子：

```python
class Account(object):
    __slots__ = ('owner', 'balance')
    ...
```

`Slots` 是一个定义提示，允许 Python 对内存使用和执行速度进行性能优化。具有 `__slots__` 的类实例不再使用字典来存储实例数据。相反，它使用一种基于数组的、更为紧凑的数据结构。在创建大量对象的程序中，使用 `__slots__` 可以显著减少内存使用并适度提高执行时间。

`__slots__` 中的唯一条目是实例属性。你不需要列出方法、属性、类变量或任何其他类级属性。基本上，它就是那些通常会出现于实例 `__dict__` 字典键中的名称。

请注意，`__slots__` 与继承之间存在复杂的交互。如果一个类继承自使用 `__slots__` 的基类，它本身也需要定义 `__slots__` 来存储自己的属性（即使它没有添加任何属性），才能利用 `__slots__` 提供的优势。如果你忘记了这一点，派生类的运行速度会变慢——而且比在任何类中都不使用 `__slots__` 时消耗更多的内存！

`__slots__` 与多重继承不兼容。如果指定了多个基类，且每个基类都有非空的 `slots`，你将收到一个 `TypeError`。

使用 `__slots__` 还可能会破坏那些期望实例具有底层 `__dict__` 属性的代码。虽然这通常不适用于用户代码，但用于支持对象的实用库和其他工具可能会被编程为通过查看 `__dict__` 来进行调试、对象序列化和其他操作。

`__slots__` 的存在对于 `__getattribute__()`、`__getattr__()` 和 `__setattr__()` 等方法的调用没有影响（如果它们在类中被重新定义）。但是，如果你正在实现这些方法，请意识到不再有实例 `__dict__` 属性。你的实现需要考虑到这一点。

## 7.28 描述符

通常，属性访问对应于字典操作。如果需要更多控制，属性访问可以通过用户定义的 `get`、`set` 和 `delete` 函数进行路由。属性（properties）的使用已经描述过了。然而，属性实际上是使用一种称为描述符（descriptor）的底层结构实现的。描述符是一个管理属性访问的类级对象。通过实现一个或多个特殊方法 `__get__()`、`__set__()` 和 `__delete__()`，你可以直接挂载到属性访问机制并自定义这些操作。这里有一个例子：

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
        raise AttributeError("Can't delete attribute")

class Integer(Typed):
    expected_type = int
```

```python
class Float(Typed):
    expected_type = float

class String(Typed):
    expected_type = str
```

```python
# Example use:
class Account:
    owner = String()
    balance = Float()

    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance
```



在这个例子中，`Typed` 类定义了一个描述符，在给属性赋值时进行类型检查，并在尝试删除属性时产生错误。`Integer`、`Float` 和 `String` 子类使 `Typed` 专门化以匹配特定类型。在另一个类（如 `Account`）中使用这些类，使得这些属性在访问时会自动调用相应的 `__get__()`、`__set__()` 或 `__delete__()` 方法。例如：

```python
a = Account('Guido', 1000.0)
b = a.owner                     # Calls Account.owner.__get__(a, Account)
a.owner = 'Eva'                 # Calls Account.owner.__set__(a, 'Eva')
del a.owner                     # Calls Account.owner.__delete__(a)
```

描述符只能在类级别实例化。在 `__init__()` 和其他方法内部创建描述符对象，以在每个实例的基础上创建描述符是不合法的。描述符的 `__set_name__()` 方法在类定义之后、任何实例创建之前被调用，目的是告知描述符在类中使用的名称。例如，`balance = Float()` 定义会调用 `Float.__set_name__(Account, 'balance')`，来告知描述符所使用的类和名称。

具有 `__set__()` 方法的描述符总是优先于实例字典中的项。例如，如果一个描述符恰好与实例字典中的键同名，描述符具有优先权。在上面的 `Account` 例子中，你会看到即使实例字典中有一个匹配项，描述符仍然在执行类型检查：

```python
>>> a = Account('Guido', 1000.0)
>>> a.__dict__
{'owner': 'Guido', 'balance': 1000.0 }
>>> a.balance = 'a lot'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "descrp.py", line 63, in __set__
    raise TypeError(f'Expected {self.expected_type}')
TypeError: Expected <class 'float'>
>>>
```

描述符的 `__get__(instance, cls)` 方法同时接收实例和类作为参数。`__get__()` 可能会在类级别被调用，在这种情况下，实例参数为 `None`。在大多数情况下，如果没有提供实例，`__get__()` 会返回描述符本身。例如：

```python
>>> Account.balance
<__main__.Float object at 0x110606710>
>>>
```

仅实现 `__get__()` 的描述符被称为方法描述符（method descriptor）。它比同时具有 `get`/`set` 能力的描述符绑定更弱。具体来说，方法描述符的 `__get__()` 方法只有在实例字典中没有匹配项时才被调用。

它之所以被称为方法描述符，是因为这种描述符主要用于实现 Python 的各种方法类型——包括实例方法、类方法和静态方法。

例如，这里有一个骨架实现，展示了如何从零开始实现 `@classmethod` 和 `@staticmethod`（实际的实现效率更高）：

```python
import types

class classmethod:
    def __init__(self, func):
        self.__func = func

    # 返回一个以 cls 为第一个参数的绑定方法
    def __get__(self, instance, cls):
        return types.MethodType(self.__func__, cls)

class staticmethod:
    def __init__(self, func):
        self.__func__ = func

    # 返回原始函数
    def __get__(self, instance, cls):
        return self.__func__
```

由于方法描述符仅在实例字典中没有匹配项时才起作用，因此它们也可用于实现属性的各种形式的延迟计算（lazy evaluation）。例如：

```python
class Lazy:
    def __init__(self, func):
        self.func = func

    def __set_name__(self, cls, name):
        self.key = name

    def __get__(self, instance, cls):
        if instance:
            value = self.func(instance)
            instance.__dict__[self.key] = value
            return value
        else:
            return self
```

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    area = Lazy(lambda self: self.width * self.height)
    perimeter = Lazy(lambda self: 2*self.width + 2*self.height)
```

在这个例子中，`area` 和 `perimeter` 是按需计算并存储在实例字典中的属性。一旦计算完成，值将直接从实例字典中返回。

```python
>>> r = Rectangle(3, 4)
>>> r.__dict__
{'width': 3, 'height': 4 }
>>> r.area
12
>>> r.perimeter
14
>>> r.__dict__
{'width': 3, 'height': 4, 'area': 12, 'perimeter': 14 }
>>>
```

## 7.29 类定义过程

类的定义是一个动态过程。当你使用 `class` 语句定义一个类时，会创建一个新的字典作为本地类命名空间。随后，类的正文在这个命名空间中像脚本一样执行。最终，这个命名空间变成了结果类对象的 `__dict__` 属性。

类正文中允许出现任何合法的 Python 语句。通常，你只需定义函数和变量，但控制流、导入、嵌套类以及所有其他内容都是允许的。例如，这里有一个根据条件定义方法的类：

```python
debug = True

class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    if debug:
        import logging
        log = logging.getLogger(f'{__module__}.{__qualname__}')

        def deposit(self, amount):
            Account.log.debug('Depositing %f', amount)
            self.balance += amount

        def withdraw(self, amount):
            Account.log.debug('Withdrawing %f', amount)
            self.balance -= amount
    else:
        def deposit(self, amount):
            self.balance += amount

        def withdraw(self, amount):
            self.balance -= amount
```

在这个例子中，全局变量 `debug` 被用来有条件地定义方法。`__qualname__` 和 `__module__` 是预定义的字符串，持有关于类名和包含模块的信息。类正文中的语句可以使用它们。在这个例子中，它们被用来配置日志系统。组织上述代码可能还有更简洁的方法，但关键点在于你可以在类中放入任何你想要的东西。

关于类定义的一个关键点是，用于持有类正文内容的命名空间并不是一个变量作用域。在方法内部使用的任何名称（例如上述示例中的 `Account.log`）都需要使用全限定名。

如果在类正文中（但不在方法内部）使用像 `locals()` 这样的函数，它将返回用于类命名空间的字典。

## 7.30 动态类创建

通常，类是使用 `class` 语句创建的，但这并非强制要求。正如前一节所述，类的定义是通过执行类正文来填充一个命名空间。如果你能够用自己的定义填充一个字典，你就可以在不使用 `class` 语句的情况下创建类。为此，请使用 `types.new_class()`：

```python
import types

# 一些方法（不在类中）
def __init__(self, owner, balance):
    self.owner = owner
    self.balance = balance

def deposit(self, amount):
    self.balance += amount

def withdraw(self, amount):
    self.balance -= amount

methods = {
    '__init__': __init__,
    'deposit': deposit,
    'withdraw': withdraw,
}

Account = types.new_class(
    'Account',
    (),
    exec_body=lambda ns: ns.update(methods)
)

# 你现在拥有一个类
a = Account('Guido', 1000.0)
a.deposit(50)
a.withdraw(25)
```

`new_class()` 函数需要一个类名、一个基类元组以及一个负责填充类命名空间的回调函数。该回调函数接收类命名空间字典作为参数，并应原地更新此字典。回调函数的返回值会被忽略。

如果你想从数据结构创建类，动态类创建可能会很有用。例如，在关于描述符的章节中，定义了以下类：

```python
class Integer(Typed):
    expected_type = int

class Float(Typed):
    expected_type = float

class String(Typed):
    expected_type = str
```

这段代码重复性很高。也许采用数据驱动的方法会更好：

```python
typed_classes = [
    ('Integer', int),
    ('Float', float),
    ('String', str),
    ('Bool', bool),
    ('Tuple', tuple),
]

globals().update(
    (name, types.new_class(
        name,
        (Typed,),
        exec_body=lambda ns, ty=ty: ns.update(expected_type=ty)
    ))
    for name, ty in typed_classes
)
```

在这个例子中，全局模块命名空间通过使用 `types.new_class()` 被更新为动态创建的类。如果你想创建更多类，只需在 `typed_classes` 列表中添加相应的项。

有时你会看到使用 `type()` 来动态创建类。例如：

```python
Account = type('Account', (), methods)
```

这可行，但它没有考虑到一些更高级的类机制，例如元类（稍后讨论）。在现代代码中，请尝试使用 `types.new_class()`。

## 7.31 元类

在 Python 中定义一个类时，类定义本身就变成了一个对象。这里有一个例子：

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

isinstance(Account, object)     # -> True
```

如果你深思这个问题，你会意识到如果 `Account` 是一个对象，那么一定有某个东西创建了它。这种类对象的创建是由一种特殊的类控制的，称为元类（metaclass）。简单来说，元类就是创建类实例的类。

在前面的例子中，创建 `Account` 的元类是一个名为 `type` 的内置类。事实上，如果你检查 `Account` 的类型，你会发现它是 `type` 的一个实例：

```python
>>> Account.__class__
<class 'type'>
```

这有点绕脑，但它与整数类似。例如，如果你写 `x = 42` 然后查看 `x.__class__`，你会得到 `int`，即创建整数的类。同样，`type` 创建类型或类的实例。

当使用 `class` 语句定义新类时，会发生一系列事情。首先，会为该类创建一个新的命名空间。

接下来，类的正文将在该命名空间中执行。最后，使用类名、基类和填充后的命名空间来创建类实例。以下代码演示了所发生的底层步骤：

```python
# Step 1: Create the class namespace
namespace = type.__prepare__('Account', ())

# Step 2: Execute the class body
exec('''
def __init__(self, owner, balance):
    self.owner = owner
    self.balance = balance

def deposit(self, amount):
    self.balance += amount

def withdraw(self, amount):
    self.balance -= amount
''', globals(), namespace)

# Step 3: Create the final class object
Account = type('Account', (), namespace)
```

在定义过程中，会与 `type` 类进行交互以创建类命名空间并创建最终的类对象。使用 `type` 的选择是可以自定义的——类可以通过指定不同的元类（metaclass）来选择由不同的类型类来处理。这可以通过在继承中使用 `metaclass` 关键字参数来实现：

```python
class Account(metaclass=type):
    ...
```

如果没有给出元类，`class` 语句将检查基类元组（如果有）中第一个条目的类型，并将其作为元类。因此，如果你写 `class Account(object)`，生成的 `Account` 类将与 `object` 具有相同的类型（即 `type`）。请注意，完全没有指定任何父类的类总是继承自 `object`，因此此规则依然适用。

要创建新的元类，请定义一个继承自 `type` 的类。在这个类中，你可以重新定义一个或多个在类创建过程中使用的方法。通常，这包括用于创建类命名空间的 `__prepare__()` 方法，用于创建类实例的 `__new__()` 方法，在类创建之后调用的 `__init__()` 方法，以及用于创建新实例的 `__call__()` 方法。下面的示例实现了一个元类，它仅仅打印每个方法的输入参数，以便你进行实验：



```python
class mytype(type):

    # Creates the class namespace
    @classmethod
    def __prepare__(meta, clsname, bases):
        print("Preparing:", clsname, bases)
        return super().__prepare__(clsname, bases)

    # Creates the class instance after body has executed
    @staticmethod
    def __new__(meta, clsname, bases, namespace):
        print("Creating:", clsname, bases, namespace)
        return super().__new__(meta, clsname, bases, namespace)

    # Initializes the class instance
    def __init__(cls, clsname, bases, namespace):
        print("Initializing:", clsname, bases, namespace)
        super().__init__(clsname, bases, namespace)

    # Creates new instances of the class
    def __call__(cls, *args, **kwargs):
        print("Creating instance:", args, kwargs)
        return super().__call__(*args, **kwargs)
```

## 示例

```python
class Base(metaclass=mytype):
    pass

# Definition of the Base produces the following output
# Preparing: Base ()
# Creating: Base () {'__module__': '__main__', '__qualname__': 'Base'}
# Initializing: Base () {'__module__': '__main__', '__qualname__': 'Base'}

b = Base()
# Creating instance: () {}
```

使用元类的一个棘手方面是变量的命名以及对涉及的各种实体的跟踪。在上述代码中，`meta` 名称指的是元类本身。`cls` 名称指的是由元类创建的类实例。虽然这里没有用到，但 `self` 名称指的是由类创建的普通实例。

元类通过继承进行传播。因此，如果你定义了一个使用不同元类的基类，所有子类也将使用该元类。尝试这个示例来看看你的自定义元类是如何工作的：

```python
class Account(Base):
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

print(type(Account))    # -> <class 'mytype'>
```

元类的主要用途是在你希望对类定义环境和创建过程实施极低级别控制的情况下。但在继续之前，请记住 Python 已经提供了许多用于监控和修改类定义的功能（例如 `__init_subclass__()` 方法、类装饰器、描述符、混入 mixins 等）。大多数时候，你可能不需要元类。即便如此，接下来的几个示例将展示元类是唯一合理解决方案的情况。

元类的一个用途是在创建类对象之前重写类命名空间的内容。类的某些特性在定义时就已确定，之后无法修改。`__slots__` 就是这样一个特性。如前所述，`__slots__` 是与实例内存布局相关的性能优化。这里有一个元类，它根据 `__init__()` 方法的调用签名自动设置 `__slots__` 属性。

```python
import inspect

class SlotMeta(type):
    @staticmethod
    def __new__(meta, clsname, bases, methods):
        if '__init__' in methods:
            sig = inspect.signature(methods['__init__'])
            __slots__ = tuple(sig.parameters)[1:]
        else:
            __slots__ = ()
        methods['__slots__'] = __slots__
        return super().__new__(meta, clsname, bases, methods)

class Base(metaclass=SlotMeta):
    pass

# Example
class Point(Base):
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

在这个示例中，创建的 `Point` 类会自动带有一个值为 `('x', 'y')` 的 `__slots__`。结果是 `Point` 的实例现在可以在无需知道使用了 slots 的情况下节省内存。它不需要被直接指定。这种技巧无法通过类装饰器或 `__init_subclass__()` 实现，因为这些功能仅在类创建之后才对其操作。到那时，应用 `__slots__` 优化已经太晚了。

元类的另一个用途是改变类定义环境。例如，在类定义期间对同一个名称的重复定义通常会导致静默错误——第二个定义会覆盖第一个。假设你想捕获这种情况。这里有一个元类，它通过为类命名空间定义一种不同类型的字典来实现这一点：

```python
class NoDupeDict(dict):
    def __setitem__(self, key, value):
        if key in self:
            raise AttributeError(f'{key} already defined')
        super().__setitem__(key, value)

class NoDupeMeta(type):
    @classmethod
    def __prepare__(meta, clsname, bases):
        return NoDupeDict()

class Base(metaclass=NoDupeMeta):
    pass

# Example
class SomeClass(Base):
    def yow(self):
        print('Yow!')

    def yow(self, x):        # Fails. Already defined
        print('Different Yow!')
```

这只是可能实现的功能的一小部分。对于框架构建者来说，元类提供了一个机会来紧密控制类定义期间发生的事情——允许类充当一种领域特定语言（DSL）。

从历史上看，元类被用来完成各种现在无法通过其他手段实现的任务。特别是 `__init_subclass__()` 方法，可以用来处理许多曾经应用元类的用例。这包括将类注册到中央注册表、方法的自动装饰以及代码生成。

## 7.32 实例和类的内置对象

本节将详细介绍用于表示类型和实例的底层对象。这些信息在底层元编程和需要直接操作类型的代码中可能会很有用。

表 7.1 显示了类型对象 `cls` 常用的属性。

**表 7.1 类型的属性**

| 属性 | 描述 |
|---|---|
| `cls.__name__` | 类名 |
| `cls.__module__` | 定义该类的模块名 |
| `cls.__qualname__` | 限定类的全名 |
| `cls.__bases__` | 基类元组 |
| `cls.__mro__` | 方法解析顺序 (MRO) 元组 |
| `cls.__dict__` | 包含类方法和变量的字典 |
| `cls.__doc__` | 文档字符串 |
| `cls.__annotations__` | 类类型提示字典 |
| `cls.__abstractmethods__` | 抽象方法名称集合（如果没有定义则可能为空）。 |

`cls.__name__` 属性包含简短的类名。`cls.__qualname__` 属性包含一个全名，并带有关于周围上下文的附加信息（如果类定义在函数内部或创建了嵌套类定义，这可能会很有用）。`cls.__annotations__` 字典包含类级别的类型提示（如果有）。

表 7.2 展示了实例 `i` 的特殊属性。

**表 7.2 实例属性**

| 属性 | 描述 |
|---|---|
| `i.__class__` | 实例所属的类 |
| `i.__dict__` | 包含实例数据的字典（如果已定义） |

`__dict__` 属性通常是存储与实例相关的所有数据的地方。然而，如果用户定义的类使用了 `__slots__`，则会使用更高效的内部表示，且实例将没有 `__dict__` 属性。

## 7.33 结语：保持简单

本章介绍了大量关于类以及自定义和控制类的方法的信息。然而，在编写类时，保持简单通常是最好的策略。是的，你可以使用基于抽象的类、元类、描述符、类装饰器、属性（properties）、多重继承、混入（mixins）、设计模式和类型提示。但你也可以只写一个普通的类。很有可能这个类就已经足够好了，而且每个人都能理解它在做什么。

从大局来看，退一步考虑几个通常理想的代码质量是非常有用的。首先且最重要的是，可读性至关重要——如果你堆叠了太多的抽象层，可读性往往会受损。其次，你应该尝试编写易于观察和调试的代码，并且不要忘记使用 REPL。最后，使代码可测试通常是良好设计的良好驱动力。如果你的代码无法测试或者测试起来太尴尬，那么可能有一种更好的方式来组织你的解决方案。

# 8. 模块与包

Python 程序被组织成通过 `import` 语句加载的模块和包。本章将更详细地描述模块和包系统。重点在于如何使用模块和包进行编程，而不是将代码打包分发给他人的过程。关于后者，请参阅最新的文档：https://packaging.python.org/tutorials/packaging-projects/。

## 8.1 模块与 `import` 语句

任何 Python 源文件都可以作为模块导入。例如：

```python
# module.py

a = 37

def func():
    print(f'func says that a is {a}')

class SomeClass:
    def method(self):
        print('method says hi')

print('loaded module')
```

该文件包含常见的编程元素——包括一个全局变量、一个函数、一个类定义和一个独立的语句。这个例子说明了模块加载的一些重要（有时是微妙的）特性。

要加载模块，请使用语句 `import module`。例如：

```python
>>> import module
loaded module
>>> module.a
37
>>> module.func()
func says that a is 37
>>> s = module.SomeClass()
>>> s.method()
method says hi
>>>
```

在执行导入时，会发生几件事：

1. 查找模块源代码。如果找不到，将抛出 `ImportError` 异常。
2. 创建一个新的模块对象。该对象作为模块内所有全局定义的容器。它有时被称为*命名空间*。
3. 模块源代码在 newly 创建的模块命名空间中执行。
4. 如果没有发生错误，将在调用者内部创建一个指向新模块对象的名称。该名称与模块名称匹配，但不带任何文件名后缀。例如，如果代码位于文件 `module.py` 中，则模块名称为 `module`。

在这些步骤中，第一步（定位模块）是最复杂的。新手经常失败的原因是使用了错误的文件名或将代码放在了未知的位置。模块文件名必须遵循与变量名相同的规则（字母、数字和下划线）并具有 `.py` 后缀——例如 `module.py`。

使用 `import` 时，指定不带后缀的名称：`import module`，而不是 `import module.py`（后者会产生一个相当令人困惑的错误消息）。文件需要放置在 `sys.path` 找到的目录之一中。

其余步骤都与模块为代码定义隔离环境有关。出现在模块中的所有定义都与该模块隔离。因此，变量、函数和类的名称不会与其它模块中相同的名称发生冲突。在访问模块中的定义时，请使用全名，例如 `module.func()`。

`import` 会执行加载的源文件中的所有语句。如果模块除了定义对象外还进行了计算或产生输出，你将看到结果——例如上述示例中打印的“loaded module”消息。关于模块的一个常见困惑是访问类。模块总是定义一个命名空间，因此如果文件 `module.py` 定义了一个类 `SomeClass`，请使用名称 `module.SomeClass` 来引用该类。

使用单个 `import` 导入多个模块，请使用逗号分隔的名称列表：

```python
import socket, os, re
```

有时，使用 `as` 限定符来更改用于引用模块的本地名称。例如：

```python
import module as mo
mo.func()
```

后一种 `import` 风格在数据分析领域是标准做法。例如，你经常会看到：

```python
import numpy as np
import pandas as pd
import matplotlib as plt
...
```

当模块被重命名时，新名称仅适用于 `import` 语句出现的内容。其它无关的程序模块仍然可以使用原始名称加载该模块。

为导入的模块分配不同的名称可以是管理通用功能的多种不同实现或编写可扩展程序的有用工具。例如，如果你有两个模块 `unixmodule.py` 和 `winmodule.py` 都定义了一个函数 `func()`，但涉及平台相关的实现细节，你可以编写代码来选择性地导入模块：

```python
if platform == 'unix':
    import unixmodule as module
elif platform == 'windows':
    import winmodule as module

...
r = module.func()
```

模块在 Python 中是一等公民对象。这意味着它们可以被赋值给变量，放入数据结构中，并在程序中作为数据传递。例如，上述示例中的 `module` 名称就是一个指向相应模块对象的变量。

## 8.2 模块缓存

无论你使用 `import` 语句的次数多少，模块的源代码仅被加载和执行一次。随后的 `import` 语句将模块名称绑定到由之前导入已创建的模块对象上。

新手经常遇到的一个困惑是：当一个模块被导入到交互式会话中，然后其源代码被修改（例如，为了修复 bug），但新的 `import` 无法加载修改后的代码。这是模块缓存造成的。即使底层的源代码已经更新，Python 也永远不会重新加载之前导入过的模块。

你可以在 `sys.modules` 中找到所有当前已加载模块的缓存，它是一个将模块名称映射到模块对象的字典。该字典的内容用于确定 `import` 是加载模块的新副本还是使用缓存。从缓存中删除一个模块将强制它在下一个 `import` 语句时重新加载。然而，出于[第 8.5 节](#)中关于模块重新加载的原因，这样做很少是安全的。

有时你会看到 `import` 被像这样用在函数内部：

```python
def f(x):
    import math
    return math.sin(x) + math.cos(x)
```

乍一看，这种实现似乎会非常慢——每次调用都要加载一次模块。实际上，`import` 的开销极小——它仅仅是一次简单的字典查找，因为 Python 会立即在缓存中找到该模块。将 `import` 放在函数内部的主要反对意见在于代码风格——通常将所有模块导入列在文件的顶部，这样更易于查看。另一方面，如果你有一个极少被调用的特殊函数，将该函数的导入依赖项放在函数体内部可以加快程序的加载速度。在这种情况下，只有在真正需要时才会加载所需的模块。

## 8.3 从模块导入选定的名称

你可以使用 `from module import name` 语句将模块中的特定定义加载到当前命名空间中。它与 `import` 相同，不同之处在于，它不是创建一个指向新创建的模块命名空间的名称，而是将模块中定义的一个或多个对象的引用放入当前命名空间中：

```python
from module import func  # 导入 module 并将 func 放入当前命名空间
func()                   # 调用 module.func()
module.func()            # 失败。NameError: module
```

如果你需要多个定义，`from` 语句接受以逗号分隔的名称。例如：



```python
from module import func, SomeClass
```

从语义上讲，`from module import name` 语句执行了从模块缓存到本地命名空间的名称复制。也就是说，Python 首先在后台执行 `import module`。随后，它将缓存中的对象赋值给本地名称，例如 `name = sys.modules['module'].name`。

一个常见的误区是认为 `from module import name` 语句更高效——可能只加载了模块的一部分。事实并非如此。无论哪种方式，整个模块都会被加载并存储在缓存中。

使用 `from` 语法导入函数不会改变它们的作用域规则。当函数查找变量时，它们仅在定义该函数的文件中查找，而不在函数被导入并调用的命名空间中查找。例如：

```python
>>> from module import func
>>> a = 42
>>> func()
func says that a is 37
>>> func.__module__
'module'
>>> func.__globals__['a']
37
>>>
```

一个相关的混淆点涉及全局变量的行为。例如，考虑这段同时导入了 `func` 及其所使用的全局变量 `a` 的代码：

```python
from module import a, func

a = 42                        # 修改变量
func()                        # 打印 "func says a is 37"
print(a)                      # 打印 "42"
```

Python 中的变量赋值不是存储操作。也就是说，本例中的名称 `a` 并不代表某种存储值的“盒子”。初始导入将本地名称 `a` 与原始对象 `module.a` 关联起来。然而，随后的重新赋值 `a = 42` 将本地名称 `a` 移到了一个完全不同的对象上。此时，`a` 不再绑定到导入模块中的值。因此，无法使用 `from` 语句使变量像 C 等语言中的全局变量那样运行。如果你希望在程序中使用可变的全局参数，请将它们放在一个模块中并显式使用 `import` 语句——例如 `module.a`。

星号（`*`）通配符有时用于加载模块中的所有定义，除了那些以底线开头的定义。示例如下：

```python
# 将所有定义加载到当前命名空间
from module import *
```

`from module import *` 语句只能在模块的顶层作用域中使用。特别是，在函数体内部使用这种形式的导入是非法的。

模块可以通过定义 `__all__` 列表来精确控制被 `from module import *` 导入的名称集。示例如下：

```python
# module: module.py
__all__ = [ 'func', 'SomeClass' ]

a = 37                    # 不导出

def func():                # 导出
    ...

class SomeClass:          # 导出
    ...
```

在交互式 Python 提示符下，使用 `from module import *` 可能是操作模块的一种便捷方式。然而，在程序中使用这种导入风格是不被鼓励的。过度使用会污染本地命名空间并导致混淆。例如：

```python
from math import *
from random import *
from statistics import *

a = gauss(1.0, 0.25)      # 来自哪个模块？
```

通常最好显式指定名称：

```python
from math import sin, cos, sqrt
from random import gauss
from statistics import mean

a = gauss(1.0, 0.25)
```

## 8.4 循环导入

如果两个模块相互导入，就会出现一个奇怪的问题。例如，假设你有两个文件：

```python
# -------------------
# moda.py

import modb

def func_a():
    modb.func_b()

class Base:
    pass
```

```python
# -------------------
# modb.py

import moda

def func_b():
    print('B')

class Child(moda.Base):
    pass
```

这段代码中存在奇怪的导入顺序依赖。先使用 `import modb` 可以正常工作，但如果你先写 `import moda`，它会因为 `moda.Base` 未定义而报错。

要理解发生了什么，你必须跟踪控制流。`import moda` 开始执行 `moda.py` 文件。它遇到的第一个语句是 `import modb`。于是，控制权转移到 `modb.py`。该文件中的第一个语句是 `import moda`。为了避免进入递归循环，这次导入由模块缓存满足，控制权继续执行 `modb.py` 中的下一个语句。这很好——循环导入不会导致 Python 死锁或进入一个新的时空维度。然而，在执行到此时，模块 `moda` 仅被部分评估。当控制流到达 `class Child(moda.Base)` 语句时，它就崩溃了。所需的 `Base` 类尚未定义。

解决这个问题的一种方法是将 `import modb` 语句移动到其他地方。例如，你可以将导入移至真正需要定义的 `func_a()` 内部：

```python
# moda.py

def func_a():
    import modb
    modb.func_b()


class Base:
    pass
```

你也可以将导入移到文件的较后位置：

```python
# moda.py

def func_a():
    modb.func_b()


class Base:
    pass

import modb        # 必须在 Base 定义之后
```

这两种解决方案在代码审查时都可能会引起质疑。大多数情况下，你不会看到模块导入出现在文件末尾。循环导入的存在几乎总是暗示代码组织存在问题。更好的处理方法可能是将 `Base` 的定义移到一个独立的文件 `base.py` 中，并将 `modb.py` 重写如下：

```python
# modb.py
import base

def func_b():
    print('B')

class Child(base.Base):
    pass
```

## 8.5 模块的重新加载与卸载

对于之前导入模块的重新加载（reloading）或卸载（unloading），并没有可靠的支持。虽然你可以从 `sys.modules` 中移除一个模块，但这并不能将其从内存中卸载。这是因为在其他导入了该模块的模块中，仍然存在对缓存模块对象的引用。此外，如果模块中定义了类且存在其实例，这些实例包含指向其类对象的引用，而类对象又持有对其定义所在模块的引用。

由于模块引用存在于许多地方，在修改其实现后重新加载模块通常是不切实际的。例如，如果你从 `sys.modules` 中删除一个模块并使用 `import` 重新加载它，这不会追溯地更改程序中所有之前的模块引用。相反，你将拥有一个由最近的 `import` 语句创建的新模块引用，以及一组由代码其他部分导入创建的旧模块引用。这通常不是你想要的结果。除非你能仔细控制整个执行环境，否则在任何理智的生产代码中使用模块重新加载都是不安全的。

`importlib` 库中提供了一个用于重新加载模块的 `reload()` 函数。你需要将已经加载的模块作为参数传递给它。例如：

```python
>>> import module
>>> import importlib
>>> importlib.reload(module)
loaded module
<module 'module' from 'module.py'>
>>>
```

`reload()` 的工作原理是加载新版本的模块源代码，然后在现有的模块命名空间之上执行它。这一过程不会清除之前的命名空间。这实际上就相当于你在不重启解释器的情况下，在旧代码之上输入了新源代码。

如果其他模块之前使用标准的 `import` 语句（如 `import module`）导入了被重新加载的模块，重新加载将使它们像变魔术一样看到更新后的代码。然而，这里仍然存在很多风险。首先，重新加载不会重新加载被重新加载的文件可能导入的任何模块。它不是递归的——它仅适用于传递给 `reload()` 的单个模块。其次，如果任何模块使用了 `from module import name` 形式的导入，这些导入将无法看到重新加载的效果。最后，如果已经创建了类的实例，重新加载不会更新其底层的类定义。事实上，你现在会在同一个程序中拥有同一个类的两个不同定义——一个是重新加载时仍被所有现有实例使用的旧定义，另一个是用于新实例的新定义。这几乎总是令人困惑的。

最后需要注意的是，Python 的 C/C++ 扩展无法以任何安全的方式被卸载或重新加载。对此没有提供支持，而且底层的操作系统可能会禁止这样做。在这种情况下，最好的办法是重启 Python 解释器进程。

## 8.6 模块编译

模块在首次导入时，会被编译成解释器字节码。这些代码被写入到一个特殊目录 `__pycache__` 下的 `.pyc` 文件中。该目录通常位于原始 `.py` 文件所在的同一个目录下。当程序在另一次运行时再次发生相同的导入时，将加载编译后的字节码。这显著加快了导入过程。

字节码的缓存是一个自动过程，你几乎不需要担心。如果原始源代码发生更改，文件会自动重新生成。它就是这样高效运行的。

尽管如此，了解这个缓存和编译过程仍然有其必要性。首先，有时 Python 文件被安装（通常是无意地）在一个用户没有操作系统权限创建所需 `__pycache__` 目录的环境中。Python 仍然可以工作，但每次导入现在都要加载原始源代码并将其编译为字节码。程序的加载速度将比正常情况慢得多。同样，在部署或打包 Python 应用程序时，包含编译后的字节码可能会很有优势，因为这可以显著加快程序的启动速度。

了解模块缓存的另一个好理由是，某些编程技术会干扰它。涉及动态代码生成和 `exec()` 函数的高级元编程技术会抵消字节码缓存的优势。一个显著的例子是 `dataclasses` 的使用：

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: float
    y: float
```

`dataclasses` 的工作原理是将方法函数生成为文本片段，然后使用 `exec()` 执行它们。这些生成的代码都没有被导入系统缓存。对于单个类定义，你不会注意到。然而，如果你有一个包含 100 个 `dataclass` 的模块，你可能会发现它的导入速度比一个用普通（虽然不那么简洁）方式编写类的同类模块慢近 20 倍。

## 8.7 模块搜索路径

导入模块时，解释器会搜索 `sys.path` 中的目录列表。`sys.path` 中的第一个条目通常是一个空字符串 `''`，它指的是当前工作目录。或者，如果你运行一个脚本，`sys.path` 中的第一个条目就是该脚本所在的目录。`sys.path` 中的其他条目通常由目录名称和 `.zip` 归档文件混合组成。`sys.path` 中条目的排列顺序决定了导入模块时的搜索顺序。要向搜索路径添加新条目，请将它们添加到此列表中。这可以直接完成，也可以通过设置 `PYTHONPATH` 环境变量来实现。例如，在 UNIX 上：

```bash
$ env PYTHONPATH=/some/path python3 script.py
```

ZIP 归档文件是将一组模块捆绑到单个文件中的便捷方式。例如，假设你创建了两个模块 `foo.py` 和 `bar.py`，并将它们放在一个文件 `mymodules.zip` 中。该文件可以通过以下方式添加到 Python 搜索路径中：

```python
import sys
sys.path.append('mymodules.zip')
import foo, bar
```

`.zip` 文件目录结构中的特定位置也可以用作路径。此外，`.zip` 文件可以与常规路径组件混合使用。这里有一个示例：

```python
sys.path.append('/tmp/modules.zip/lib/python')
```

ZIP 文件不一定非要有 `.zip` 后缀才能被使用。从历史上看，在路径中经常会遇到 `.egg` 文件。`.egg` 文件起源于一个早期的 Python 包管理工具 `setuptools`。然而，`.egg` 文件不过是一个普通的 `.zip` 文件或目录，并添加了一些额外的元数据（版本号、依赖关系等）。

## 8.8 作为主程序执行

虽然本节讨论的是 `import` 语句，但 Python 文件经常被作为主脚本执行。例如：

```bash
% python3 module.py
```

每个模块都包含一个变量 `__name__`，它保存着模块的名称。代码可以通过检查这个变量来确定它们正在哪个模块中执行。解释器的顶层模块被命名为 `__main__`。在命令行中指定或交互式输入的程序都在 `__main__` 模块中运行。有时，程序可能会根据它是被作为模块导入还是在 `__main__` 中运行而改变其行为。例如，一个模块可能包含一段代码，如果该模块被用作主程序则执行，而如果该模块只是被另一个模块导入则不执行。

```python
# 检查是否作为程序运行
if __name__ == '__main__':
    # 是的。作为主脚本运行
    statements
else:
    # 不是，我一定是被作为模块导入的
    statements
```

旨在作为库使用的源文件可以使用这种技术来包含可选的测试或示例代码。在开发模块时，你可以放入用于测试功能的调试代码...

如所示在 `if` 语句内部定义库，并将你的模块作为主程序运行 Python。对于那些导入你的库的用户来说，这段代码不会运行。

如果你创建了一个 Python 代码目录，只要该目录包含一个特殊的 `__main__.py` 文件，你就可以执行该目录。例如，如果你创建这样一个目录：

```
myapp/
    foo.py
    bar.py
    __main__.py
```

你可以通过输入 `python3 myapp` 来运行它。执行将从 `__main__.py` 文件开始。如果你将 `myapp` 目录转换为 ZIP 压缩档，这种方法同样有效。输入 `python3 myapp.zip` 会寻找顶层的 `__main__.py` 文件，并在找到后执行它。

## 8.9 包（Packages）

除了最简单的程序外，Python 代码通常组织成*包（packages）*。包是一组模块的集合，它们被组合在一个共同的顶层名称之下。这种分组有助于解决不同应用程序中使用的模块名称之间的冲突，并将你的代码与他人的代码分开。定义一个包的方法是创建一个具有独特名称的目录，并在该目录中放置一个初始为空的 `__init__.py` 文件。然后，根据需要在此目录中放置额外的 Python 文件和子包。例如，一个包可以组织如下：

```
graphics/
    __init__.py
    primitive/
        __init__.py
        lines.py
        fill.py
        text.py
        ...
    graph2d/
        __init__.py
        plot2d.py
        ...
    graph3d/
        __init__.py
        plot3d.py
        ...
    formats/
        __init__.py
        gif.py
        png.py
        tiff.py
        jpeg.py
```

`import` 语句用于从包中加载模块，其方式与用于简单模块的方式相同，不同之处在于现在的名称更长。例如：

```python
# 全路径
import graphics.primitive.fill
...
graphics.primitive.fill.floodfill(img, x, y, color)
```

```python
# 加载特定的子模块
from graphics.primitive import fill
...
fill.floodfill(img, x, y, color)
```

```python
# 从子模块加载特定的函数
from graphics.primitive.fill import floodfill
...
floodfill(img, x, y, color)
```

每当包的任何部分被首次导入时，`__init__.py` 文件中的代码会首先执行（如果该文件存在）。如前所述，此文件可以为空，但它也可以包含执行包特定初始化操作的代码。如果导入一个深层嵌套的子模块，在遍历目录结构时遇到的所有 `__init__.py` 文件都会被执行。因此，语句 `import graphics.primitive.fill` 会先执行 `graphics/` 目录下的 `__init__.py` 文件，随后执行 `primitive/` 目录下的 `__init__.py` 文件。



敏锐的 Python 用户可能会观察到，即使省略 `__init__.py` 文件，包似乎仍然可以工作。这是事实——即使一个 Python 代码目录不包含 `__init__.py`，你也可以将其作为包来使用。然而，不明显的是，缺少 `__init__.py` 文件的目录实际上定义了一种不同类型的包，称为*命名空间包（namespace package）*。这是一个高级特性，有时被非常庞大的库和框架用来实现分散的插件系统。在作者看来，这很少是你想要的结果——在创建包时，你应该始终创建正确的 `__init__.py` 文件。

## 8.10 包内导入（Imports Within a Package）

`import` 语句的一个关键特性是，所有模块导入都需要绝对路径或完全限定的包路径。这包括在包内部使用的 `import` 语句。例如，假设 `graphics.primitive.fill` 模块想要导入 `graphics.primitive.lines` 模块。像 `import lines` 这样简单的语句是行不通的——你会得到一个 `ImportError` 异常。相反，你需要像这样完全限定导入：

```python
# graphics/primitives/fill.py

# 完全限定的子模块导入
from graphics.primitives import lines
```

遗憾的是，像那样写出完整的包名既麻烦又脆弱。例如，有时重命名一个包是有意义的——也许你想重命名它以便使用不同的版本。如果包名被硬编码在代码中，你就无法这样做。更好的选择是使用如下的包相对导入：

```python
# graphics/primitives/fill.py

# 包相对导入
from . import lines
```

这里，语句 `from . import lines` 中使用的 `.` 指的是与导入模块相同的目录。因此，该语句会在 `fill.py` 文件所在的同一个目录中寻找名为 `lines` 的模块。

相对导入还可以指定同一包中不同目录下的子模块。例如，如果模块 `graphics.graph2d.plot2d` 想要导入 `graphics.primitives.lines`，它可以使用如下语句：

```python
# graphics/graph2d/plot2d.py
from ..primitive import lines
```

这里，`..` 向上移动一级目录，而 `primitive` 则进入一个不同的子包目录。

相对导入只能使用 `import` 语句的 `from module import symbol` 形式来指定。因此，诸如 `import ..primitive.lines` 或 `import .lines` 之类的语句是语法错误。此外，`symbol` 必须是一个简单的标识符，因此诸如 `from .. import primitive.lines` 之类的语句也是非法的。最后，相对导入只能在包内部使用；使用相对导入来引用仅仅位于文件系统中不同目录的模块是非法的。

## 8.11 将包子模块作为脚本运行（Running a Package Submodule as a Script）

组织成包的代码与简单脚本具有不同的运行环境。它有一个包含的包名、子模块，并且使用了相对导入（相对导入仅在包内部有效）。一个不再起作用的特性是直接在包源代码文件上运行 Python 的能力。例如，假设你正在处理 `graphics/graph2d/plot2d.py` 文件，并在底部添加了一些测试代码：

```python
# graphics/graph2d/plot2d.py
from ..primitive import lines, text

class Plot2D:
    ...

if __name__ == '__main__':
    print('Testing Plot2D')
    p = Plot2D()
    ...
```

如果你尝试直接运行它，你会遇到一个关于相对导入语句的崩溃报错：

```bash
$ python3 graphics/graph2d/plot2d.py
Traceback (most recent call last):
  File "graphics/graph2d/plot2d.py", line 1, in <module>
    from ..primitive import line, text
ValueError: attempted relative import beyond top-level package
```

你也无法进入包目录并在那里运行它：

```bash
$ cd graphics/graph2d/
$ python3 plot2d.py
Traceback (most recent call last):
  File "plot2d.py", line 1, in <module>
    from ..primitive import line, text
ValueError: attempted relative import beyond top-level package
```

要将子模块作为主脚本运行，你需要使用解释器的 `-m` 选项。例如：

```bash
$ python3 -m graphics.graph2d.plot2d
Testing Plot2D
```

`-m` 将一个模块或包指定为主程序。Python 将在适当的环境中运行该模块，以确保导入能够正常工作。Python 的许多内置包都有可以通过 `-m` 使用的“秘密”功能。其中最著名的是使用 `python3 -m http.server` 在当前目录运行一个 Web 服务器。

你也可以在自己的包中提供类似的功能。如果提供给 `python -m name` 的名称对应于一个包目录，Python 会在该目录中查找是否存在 `__main__.py`，并将其作为脚本运行。

## 8.12 控制包命名空间（Controlling the Package Namespace）

包的主要目的是作为代码的顶层容器。有时用户只会导入顶层名称而没有其他导入。例如：

```python
import graphics
```

此导入语句没有指定任何特定的子模块，也不会使包的其他部分变得可访问。例如，你会发现如下代码会运行失败：

```python
import graphics
graphics.primitive.fill.floodfill(img,x,y,color)  # Fails!
```

当仅给出顶层包导入时，唯一被导入的文件是相关的 `__init__.py` 文件。在本例中，即 `graphics/__init__.py` 文件。

`__init__.py` 文件的主要目的是构建和/或管理顶层包命名空间的内容。这通常涉及从低级子模块中导入选定的函数、类和其他对象。例如，如果本例中的 `graphics` 包由数百个低级函数组成，但大多数细节都被封装在少数几个高级类中，那么 `__init__.py` 文件可能会选择仅公开这些类：

```python
# graphics/__init__.py

from .graph2d.plot2d import Plot2D
from .graph3d.plot3d import Plot3D
```

有了这个 `__init__.py` 文件，`Plot2D` 和 `Plot3D` 这两个名称就会出现在包的顶层。用户随后可以使用这些名称，就像 `graphics` 是一个简单的模块一样：

```python
from graphics import Plot2D
plt = Plot2D(100, 100)
plt.clear()
...
```

这对于用户来说通常方便得多，因为他们不必了解你实际上是如何组织代码的。从某种意义上说，你在代码结构之上增加了一个更高层次的抽象。Python 标准库中的许多模块都是以此方式构建的。例如，流行的 `collections` 模块实际上是一个包。`collections/__init__.py` 文件将来自几个不同地点的定义整合在一起，并将其作为单一的统一命名空间呈现给用户。

## 8.13 控制包的导出

一个问题涉及 `__init__.py` 文件与低级子模块之间的交互。例如，包的用户可能只想关注存在于顶层包命名空间中的对象和函数。然而，包的实现者可能更关心如何将代码组织成可维护的子模块。

为了更好地管理这种组织复杂度，包的子模块通常通过定义 `__all__` 变量来声明一个显式的导出列表。这是一个应该被提升到包命名空间上一级的所有名称列表。例如：

```python
# graphics/graph2d/plot2d.py

__all__ = ['Plot2D']

class Plot2D:
    ...
```

随后，相关的 `__init__.py` 文件使用类似下面的 `*` 导入来导入其子模块：

```python
# graphics/graph2d/__init__.py

# 仅加载 __all__ 变量中明确列出的名称
from .plot2d import *

# 将 __all__ 传播到下一级（如果需要）
__all__ = plot2d.__all__
```

这个提升过程一直持续到顶层包的 `__init__.py`。例如：

```python
# graphics/__init__.py
from .graph2d import *
from .graph3d import *

# 整合导出内容
__all__ = [
    *graph2d.__all__,
    *graph3d.__all__
]
```

其核心在于包的每个组件都使用 `__all__` 变量显式声明其导出内容。然后 `__init__.py` 文件将这些导出向上传播。在实践中，这可能会变得复杂，但这种方法避免了将特定的导出名称硬编码到 `__init__.py` 文件中的问题。相反，如果一个子模块想要导出某些内容，其名称仅在一个地方列出——即 `__all__` 变量中。然后，它会像魔法一样传播到包命名空间中的正确位置。

值得注意的是，虽然在用户代码中使用 `*` 导入是不受欢迎的，但在包的 `__init__.py` 文件中这是一种普遍做法。它在包中可行的原因是，这通常受到更多的控制和限制——它是由 `__all__` 变量的内容驱动的，而不是一种“随便导入所有内容”的随意态度。

## 8.14 包数据

有时一个包包含需要加载的数据文件（而非源代码）。在包内部，`__file__` 变量会给你提供关于特定源文件的位置信息。然而，包的情况很复杂。它们可能被捆绑在 ZIP 归档文件中，或者从不寻常的环境中加载。`__file__` 变量本身可能是不可靠的，甚至是未定义的。因此，加载数据文件通常不仅仅是将文件名传递给内置的 `open()` 函数并读取数据那么简单。

要读取包数据，请使用 `pkgutil.get_data(package, resource)`。例如，如果你的包结构如下：

```text
mycode/
    resources/
        data.json
    __init__.py
    spam.py
    yow.py
```

要在 `spam.py` 文件中加载 `data.json` 文件，请执行以下操作：

```python
# mycode/spam.py
import pkgutil
import json

def func():
    rawdata = pkgutil.get_data(__package__,
                                'resources/data.json')
    textdata = rawdata.decode('utf-8')
    data = json.loads(textdata)
    print(data)
```

`get_data()` 函数尝试查找指定的资源，并将其内容作为原始字节字符串返回。示例中显示的 `__package__` 变量是一个包含封闭包名称的字符串。任何进一步的解码（如将字节转换为文本）和解析都由你决定。在示例中，数据被解码并从 JSON 解析为 Python 字典。

包并不是存储巨型数据文件的理想场所。请将包资源预留给配置数据和其他使你的包能够运行的杂项内容。

## 8.15 模块对象

模块是一等公民对象。表 8.1 列出了模块中常见的属性。

### 表 8.1 模块属性

| 属性 | 描述 |
| --- | --- |
| `__name__` | 完整模块名称 |
| `__doc__` | 文档字符串 |
| `__dict__` | 模块字典 |
| `__file__` | 定义该模块的文件名 |
| `__package__` | 封闭包的名称（如果有） |
| `__path__` | 用于搜索包子模块的子目录列表 |
| `__annotations__` | 模块级类型提示 |

`__dict__` 属性是一个代表模块命名空间的字典。在模块中定义的所有内容都放在这里。

`__name__` 属性经常用于脚本中。通常会进行 `if __name__ == '__main__'` 这样的检查，以查看文件是否作为独立程序运行。

`__package__` 属性包含封闭包的名称（如果有）。如果已设置，`__path__` 属性将是一个用于定位包子模块的目录列表。通常，它包含一个条目，即包所在的目录。有时大型框架会操纵 `__path__` 以纳入额外的目录，从而支持插件和其他高级功能。

并非所有属性在所有模块上都可用。例如，内置模块可能没有设置 `__file__` 属性。同样，顶层模块（不包含在包中）不会设置与包相关的属性。

`__doc__` 属性是模块的文档字符串（如果有）。这是一个出现在文件第一条语句的字符串。`__annotations__` 属性是模块级类型提示的字典。它们看起来像这样：

```python
# mymodule.py

'''
The doc string
'''

# 类型提示（放入 __annotations__）
x: int
y: float
...
```

与其他类型提示一样，模块级提示不会改变 Python 行为的任何部分，也不会实际定义变量。它们纯粹是元数据，其他工具可以在需要时选择查看。

## 8.16 部署 Python 包

模块和包的最后前沿是将你的代码交给他人的问题。这是一个庞大的话题，多年来一直是积极开发关注的焦点。我不会尝试记录一个在你阅读本文时就注定会过时的流程是没有意义的。相反，请将注意力转向 <https://packaging.python.org/tutorials/packaging-projects> 上的文档。

对于日常开发而言，最重要的事情是将你的代码隔离为一个自包含的项目。你所有的代码都应该位于一个合适的包（package）中。尽量给你的包起一个唯一的名称，以免与其他可能的依赖项发生冲突。请参考 Python 包索引 <https://pypi.org> 来选择名称。在构建代码结构时，尽量保持简单。如你所见，利用模块和包系统可以实现许多高度复杂的操作。这些操作有其适用的时间和场合，但不应成为你的起点。

本着绝对简单的原则，分发纯 Python 代码最极简的方式是使用 `setuptools` 模块或内置的 `distutils` 模块。假设你编写了一些代码，其项目结构如下：

```text
spam-project/
    README.txt
    Documentation.txt
    spam/            # 代码包
        __init__.py
        foo.py
        bar.py
    run_spam.py      # 运行脚本，执行方式为：python run_spam.py
```

要创建分发版本，请在最顶层目录（本例中为 `spam-project/`）中创建一个 `setup.py` 文件。在该文件中，写入以下代码：

```python
# setup.py
from setuptools import setup

setup(
    name = "spam",
    version = "0.0",
    packages = ['spam'],
    scripts = ['run_spam.py'],
)
```

在 `setup()` 调用中，`packages` 是所有包目录的列表，`scripts` 是脚本文件的列表。如果你的软件没有这些项（例如没有脚本），可以省略相应的参数。`name` 是你的包名，`version` 是作为字符串的版本号。`setup()` 调用还支持多种其他参数，用于提供关于你包的各种元数据。完整列表请参阅 <https://docs.python.org/3/distutils/apiref.html>。

创建 `setup.py` 文件足以创建软件的源码分发版。输入以下 shell 命令来创建源码分发版：

```shell
$ python setup.py sdist
...
$
```

这将在 `spam/dist` 目录下创建一个存档文件，例如 `spam-1.0.tar.gz` 或 `spam-1.0.zip`。这就是你交给他人以安装软件的文件。用户可以使用 `pip` 等命令进行安装。例如：

```shell
$ python3 -m pip install spam-1.0.tar.gz
```

这将把软件安装到本地 Python 环境中并使其可供通用。代码通常会被安装到 Python 库中名为 `site-packages` 的目录中。要查找该目录的准确位置，可以检查 `sys.path` 的值。脚本通常被安装在与 Python 解释器相同的目录下。

如果脚本的第一行以 `#!` 开头且包含 `python` 文本，安装程序将重写该行，使其指向本地安装的 Python。因此，即使你的脚本硬编码了特定的 Python 路径（如 `/usr/local/bin/python`），当它们被安装到 Python 路径不同的其他系统上时，依然能够正常工作。



必须强调的是，这里描述的`setuptools`用法是绝对极简的。大型项目可能涉及 C/C++ 扩展、复杂的包结构、示例等。涵盖所有工具和部署此类代码的可能方式超出了本书的范围。你应该参考 <https://python.org> 和 <https://pypi.org> 上的各种资源以获取最新的建议。

## 8.17 倒数第二句话：从包开始

在开始一个新程序时，很容易从一个简单的单个 Python 文件开始。例如，你可能会写一个名为`program.py`的脚本并以此开始。虽然这对于临时程序和短期任务没有问题，但你的“脚本”可能会不断增长并增加功能。最终，你可能想将其拆分为多个文件。通常在这种时候，问题就会出现。

鉴于此，养成从一开始就将所有程序作为包来启动的习惯是有意义的。例如，不要创建名为`program.py`的文件，而应创建一个名为`program`的程序包目录：

```text
program/
    __init__.py
    __main__.py
```

将你的起始代码放在`__main__.py`中，并使用`python -m program`等命令运行程序。随着需要更多代码，向你的包中添加新文件并使用包相对导入。使用包的一个优点是所有代码都保持隔离。你可以随意命名文件，而无需担心与其他包、标准库模块或同事编写的代码发生冲突。虽然设置包在开始时需要多花一点功夫，但这很可能会在以后为你省去很多麻烦。

## 8.18 最后的一句话：保持简单

与模块和包系统相关的高级技巧远比这里展示的要多。请参考`https://dabeaz.com/modulepackage/index.html`上的教程“Modules and Packages: Live and Let Die!”以了解各种可能性。

然而，综合考虑，你最好不要进行任何高级的模块黑客操作。管理模块、包和软件分发一直是 Python 社区的痛点。很多痛苦直接源于人们对模块系统应用黑客技巧。不要这样做。保持简单，当你的同事建议修改`import`以适配区块链时，请找到勇气直接说“不”。

# 9. 输入与输出

输入和输出（I/O）是所有程序的一部分。本章描述了 Python I/O 的基础知识，包括数据编码、命令行选项、环境变量、文件 I/O 和数据序列化。本章特别关注鼓励正确 I/O 处理的编程技巧和抽象。本章末尾概述了与 I/O 相关的常用标准库模块。

## 9.1 数据表示

I/O 的主要问题在于外部世界。为了与其通信，数据必须被正确表示，以便可以对其进行操作。在最底层，Python 处理两种基本数据类型：代表任何类型的原始未解释数据的字节（bytes）和代表 Unicode 字符的文本（text）。

为了表示字节，使用了两个内置类型：`bytes`和`bytearray`。`bytes`是一个不可变的整数字节值字符串。`bytearray`是一个可变的字节数组，其行为类似于字节字符串和列表的结合体。它的可变性使其适用于以更增量的方式构建字节组，例如从碎片中组装数据。以下示例展示了`bytes`和`bytearray`的一些特性：

```python
# 指定字节字面量（注意：b' 前缀）
a = b'hello'

# 从整数列表指定字节
b = bytes([0x68, 0x65, 0x6c, 0x6c, 0x6f])

# 从部分内容创建并填充 bytearray
c = bytearray()
c.extend(b'world')    # c = 'world'
c.append(0x21)        # c = 'world!'

# 访问字节值
print(a[0])           # --> 打印 104

for x in b:
    print(x)          # 输出 104 101 108 108 111
```

访问`bytes`和`bytearray`对象的单个元素会产生整数字节值，而不是单字符字节字符串。这与文本字符串不同，因此是一个常见的用法错误。

文本由`str`数据类型表示，并存储为 Unicode 码点数组。例如：

```python
d = 'hello'          # 文本 (Unicode)
len(d)               # --> 5
print(d[0])          # 打印 'h'
```

Python 在字节和文本之间保持严格的分离。这两者之间永远不会自动转换，这两类之间的比较结果为`False`，且任何将字节和文本混合在一起的操作都会导致错误。例如：

```python
a = b'hello'         # bytes
b = 'hello'          # text
c = 'world'          # text

print(a == b)        # -> False
# d = a + c          # TypeError: can't concat str to bytes
e = b + c            # -> 'helloworld' (两者均为字符串)
```

在进行 I/O 操作时，请确保你使用的是正确的数据表示形式。如果你在处理文本，请使用文本字符串。如果你在处理二进制数据，请使用字节（bytes）。

## 9.2 文本编码与解码

如果你处理的是文本，所有从输入读取的数据必须经过解码，所有写入输出的数据必须经过编码。为了在文本和字节之间进行显式转换，文本对象和字节对象分别提供了`encode(text [,errors])`和`decode(bytes [,errors])`方法。例如：

```python
a = 'hello'                 # Text
b = a.encode('utf-8')       # Encode to bytes

c = b'world'                # Bytes
d = c.decode('utf-8')       # Decode to text
```

`encode()`和`decode()`都需要指定编码名称，例如`'utf-8'`或`'latin-1'`。表 9.1 中列出了一些常见的编码。

### 表 9.1 常见编码

| 编码名称 | 描述 |
| --- | --- |
| `'ascii'` | 字符值在 [0x00, 0x7f] 范围内。 |
| `'latin1'` | 字符值在 [0x00, 0xff] 范围内。也称为`'iso-8859-1'`。 |
| `'utf-8'` | 可变长度编码，允许表示所有 Unicode 字符。 |
| `'cp1252'` | Windows 上常见的文本编码。 |
| `'macroman'` | Macintosh 上常见的文本编码。 |

此外，编码方法还接受一个可选的`errors`参数，用于指定出现编码错误时的行为。该参数的值见表 9.2。

### 表 9.2 错误处理选项

| 值 | 描述 |
| --- | --- |
| `'strict'` | 针对编码和解码错误抛出`UnicodeError`异常（默认值）。 |
| `'ignore'` | 忽略无效字符。 |
| `'replace'` | 将无效字符替换为替换字符（Unicode 中为 U+FFFD，字节中为`b'?'`）。 |
| `'backslashreplace'` | 将每个无效字符替换为 Python 字符转义序列。例如，字符 U+1234 被替换为`'\U1234'`（仅限编码）。 |
| `'xmlcharrefreplace'` | 将每个无效字符替换为 XML 字符引用。例如，字符 U+1234 被替换为`'&#4660;'`（仅限编码）。 |
| `'surrogateescape'` | 解码时将任何无效字节`'\xhh'`替换为 U+DChh，编码时将 U+DChh 替换为字节`'\xhh'`。 |

`'backslashreplace'`和`'xmlcharrefreplace'`错误策略将无法表示的字符以一种形式呈现，使其可以被视为简单的 ASCII 文本或 XML 字符引用。这在调试时非常有用。

`'surrogateescape'`错误处理策略允许退化的字节数据（即不符合预期编码规则的数据）在一次完整的解码/编码循环后原样保留，无论使用的是哪种文本编码。具体来说，`s.decode(enc, 'surrogateescape').encode(enc, 'surrogateescape') == s`。这种数据的往返保留对于某些系统接口非常有用，在这些接口中，虽然预期使用文本编码，但由于 Python 无法控制的因素而无法保证。Python 不会因为编码错误而破坏数据，而是使用代理编码（surrogate encoding）将其“原样”嵌入。以下是一个针对编码不正确的 UTF-8 字符串的示例：

```python
>>> a = b'Spicy Jalape\xf1o'  # Invalid UTF-8
>>> a.decode('utf-8')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xf1
in position 12: invalid continuation byte
>>> a.decode('utf-8', 'surrogateescape')
'Spicy Jalape\udcflo'
>>> # Encode the resulting string back into bytes
>>> _.encode('utf-8', 'surrogateescape')
b'Spicy Jalape\xf1o'
>>>
```

## 9.3 文本与字节格式化

在处理文本和字节字符串时，一个常见的问题是字符串转换和格式化——例如，将浮点数转换为具有给定宽度和精度的字符串。要格式化单个值，请使用`format()`函数：

```python
x = 123.456

format(x, '0.2f')       # '123.46'
format(x, '10.4f')      # '  123.4560'
format(x, '<*10.2f')    # '123.46****'
```

`format()`的第二个参数是格式说明符。说明符的一般格式为`[[fill][align]][sign][0][width][,][.precision][type]`，其中每个用`[]`括起来的部分都是可选的。`width`指定要使用的最小字段宽度，对齐说明符`align`可以是`<`、`>`或`^`，分别代表在字段内左对齐、右对齐和居中对齐。可选的填充字符`fill`用于填充空白。例如：

```python
name = 'Elwood'
r = format(name, '<10')    # r = 'Elwood     '
r = format(name, '>10')    # r = '     Elwood'
r = format(name, '^10')    # r = '  Elwood   '
r = format(name, '*^10')   # r = '**Elwood**'
```

`type`说明符指示数据的类型。表 9.3 列出了支持的格式代码。如果没有提供，默认格式代码为字符串`s`、整数`d`和浮点数`f`。

### 表 9.3 格式代码

| 字符 | 输出格式 |
| --- | --- |
| `d` | 十进制整数或长整数。 |
| `b` | 二进制整数或长整数。 |
| `o` | 八进制整数或长整数。 |
| `x` | 十六进制整数或长整数。 |
| `X` | 十六进制整数（大写字母）。 |
| `f, F` | 浮点数，格式为 [-]m.dddddd。 |
| `e` | 浮点数，格式为 [-]m.ddddde±xx。 |
| `E` | 浮点数，格式为 [-]m.dddddE±xx。 |
| `g, G` | 指数小于 [nd]4 或大于精度时使用`e`或`E`；否则使用`f`。 |
| `n` | 与`g`相同，但由当前区域设置决定小数点字符。 |
| `%` | 将数字乘以 100，并使用`f`格式显示，后面跟一个 % 符号。 |
| `s` | 字符串或任何对象。格式化代码使用`str()`来生成字符串。 |
| `c` | 单个字符。 |

格式说明符的符号部分可以是`+`、`-`或空格。`+`表示所有数字都应显示前导符号。`-`是默认值，仅为负数添加符号字符。空格为正数添加前导空格。

在宽度和精度之间可以出现一个可选的逗号（`,`），用于添加千位分隔符。例如：

```python
x = 123456.78
format(x, '16,.2f')     # '        123,456.78'
```

说明符的精度部分提供了用于小数的准确数字位数。如果在数字的字段宽度前加上 0，数值将用前导 0 填充以填满空间。以下是一些格式化不同类型数字的示例：

```python
x = 42
r = format(x, '10d')       # r = '        42'
r = format(x, '10x')       # r = '        2a'
r = format(x, '10b')       # r = '    101010'
r = format(x, '010b')      # r = '0000101010'

y = 3.1415926
r = format(y, '10.2f')     # r = '      3.14'
r = format(y, '10.2e')     # r = '  3.14e+00'
r = format(y, '+10.2f')    # r = '     +3.14'
r = format(y, '+010.2f')   # r = '+000003.14'
r = format(y, '+10.2%')    # r = '  +314.16%'
```

对于更复杂的字符串格式化，可以使用 f-strings：

```python
x = 123.456

f'Value is {x:0.2f}'       # 'Value is 123.46'
f'Value is {x:10.4f}'      # 'Value is  123.4560'
f'Value is {2*x:*<10.2f}'  # 'Value is 246.91****'
```

在 f-string 中，形式为`{expr:spec}`的文本会被`format(expr, spec)`的值替换。只要`expr`不包含`{`、`}`或`\`字符，它可以是任意表达式。格式说明符本身的部分内容也可以由其他表达式提供。例如：

```python
y = 3.1415926
width = 8
precision = 3

r = f'{y:{width}.{precision}f}'  # r = '  3.142'
```

如果你以`=`结束`expr`，那么`expr`的字面文本也会包含在结果中。例如：

```python
x = 123.456

f'{x=:0.2f}'    # 'x=123.46'
f'{2*x=:0.2f}'  # '2*x=246.91'
```

如果你在值后面附加`!r`，格式化将应用于`repr()`的输出。如果你使用`!s`，格式化将应用于`str()`的输出。例如：

```python
f'{x!r:spec}'    # 调用 (repr(x).__format__('spec'))
f'{x!s:spec}'    # 调用 (str(x).__format__('spec'))
```

作为 f-strings 的替代方案，你可以使用字符串的`.format()`方法：

```python
x = 123.456

'Value is {:0.2f}'.format(x)              # 'Value is 123.46'
'Value is {0:10.2f}'.format(x)            # 'Value is     123.46'
'Value is {val:<*10.2f}'.format(val=x)    # 'Value is 123.46****'
```

对于由`.format()`格式化的字符串，形式为`{arg:spec}`的文本会被`format(arg, spec)`的值所替换。在这种情况下，`arg`指的是传递给`format()`方法的参数之一。如果完全省略，则按顺序获取参数。例如：

```python
name = 'IBM'
shares = 50
price = 490.1

r = '{:>10s} {:10d} {:10.2f}'.format(name, shares, price)
# r = '        IBM         50     490.10'
```

`arg`也可以指特定的参数编号或名称。例如：

```python
tag = 'p'
text = 'hello world'

r = '<{0}>{1}</{0}>'.format(tag, text)   # r = '<p>hello world</p>'
r = '<{tag}>{text}</{tag}>'.format(tag='p', text='hello world')
```

与 f-strings 不同，说明符的`arg`值不能是任意表达式，因此它的表达能力稍弱。然而，`format()`方法可以执行有限的属性查找、索引和嵌套替换。例如：



```python
y = 3.1415926
width = 8
precision = 3

r = 'Value is {0:{1}.{2}f}'.format(y, width, precision)

d = {
    'name': 'IBM',
    'shares': 50,
    'price': 490.1
}
r = '{0[shares]:d} shares of {0[name]} at {0[price]:0.2f}'.format(d)
# r = '50 shares of IBM at 490.10'
```

`bytes` 和 `bytearray` 实例可以使用 `%` 运算符进行格式化。该运算符的语义模仿了 C 语言的 `sprintf()` 函数。这里有一些示例：

```python
name = b'ACME'
x = 123.456

b'Value is %0.2f' % x      # b'Value is 123.46'
bytearray(b'Value is %0.2f') % x
b'%s = %0.2f' % (name, x)   # b'ACME = 123.46'
```

在这种格式化方式中，形式为 `%spec` 的序列会按顺序被 `%` 运算符的第二个操作数（一个元组）中的值替换。基础格式代码（`d`、`f`、`s` 等）与 `format()` 函数中使用的一样。不过，一些高级特性要么缺失，要么略有变化。例如，要调整对齐方式，可以使用 `–` 字符，如下所示：

```python
x = 123.456
b'%10.2f' % x     # b'    123.46'
b'%-10.2f' % x    # b'123.46     '
```

使用格式代码 `%r` 会产生 `ascii()` 的输出，这在调试和记录日志时非常有用。

在处理字节时，请注意不支持文本字符串。它们需要被显式编码。

```python
name = 'Dave'

b'Hello %s' % name              # TypeError!
b'Hello %s' % name.encode('utf-8')  # Ok
```

这种格式化形式也可以用于文本字符串，但它被认为是一种较旧的编程风格。然而，它仍然出现在某些库中。例如，`logging` 模块产生的消息就是以此方式格式化的：

```python
import logging
log = logging.getLogger(__name__)

log.debug('Got %d', name, value)   # '%s got %d' % (name, value)
```

`logging` 模块在本章稍后的 9.15.12 节中会有简要描述。

## 9.4 读取命令行选项

当 Python 启动时，命令行选项被作为文本字符串放在 `sys.argv` 列表中。第一个项目是程序名称。随后的项目是在程序名称之后添加到命令行的选项。以下程序是手动处理命令行参数的一个极简原型：

```python
def main(argv):
    if len(argv) != 3:
        raise SystemExit(
            f'Usage : python {argv[0]} inputfile outputfile\n')
    inputfile  = argv[1]
    outputfile = argv[2]
    ...

if __name__ == '__main__':
    import sys
    main(sys.argv)
```

为了更好的代码组织、测试以及类似的原因，建议编写一个专门的 `main()` 函数，将命令行选项（如果有）作为列表接收，而不是直接读取 `sys.argv`。在程序的末尾包含一小段代码，将命令行选项传递给你的 `main()` 函数。

`sys.argv[0]` 包含正在执行的脚本名称。对于想要报告错误的命令行脚本，编写描述性的帮助消息并抛出 `SystemExit` 是标准做法。

虽然在简单的脚本中你可以手动处理命令行选项，但对于更复杂的命令行处理，请考虑使用 `argparse` 模块。这是一个示例：

```python
import argparse

def main(argv):
    p = argparse.ArgumentParser(description="This is some program")

    # 一个位置参数
    p.add_argument("infile")

    # 一个带有参数的选项
    p.add_argument("-o","--output", action="store")

    # 一个设置布尔标志的选项
    p.add_argument("-d","--debug", action="store_true", default=False)

    # 解析命令行
    args = p.parse_args(args=argv)

    # 获取选项设置
    infile    = args.infile
    output    = args.output
    debugmode = args.debug

    print(infile, output, debugmode)

if __name__ == '__main__':
    import sys
    main(sys.argv[1:])
```

这个例子仅展示了 `argparse` 模块最简单的用法。标准库文档提供了更高级的用法。此外还有第三方模块如 `click` 和 `docopt` 可以简化更复杂的命令行解析器的编写。

最后，提供给 Python 的命令行选项可能会使用无效的文本编码。此类参数仍被接受，但它们将使用 9.2 节中描述的 `'surrogateescape'` 错误处理方式进行编码。如果此类参数随后被包含在任何形式的文本输出中，且避免崩溃至关重要，那么你需要意识到这一点。不过，这可能并不关键——不要为了不重要的边缘情况而使你的代码过于复杂。

## 9.5 环境变量

有时数据通过在命令 shell 中设置的环境变量传递给程序。例如，可以通过类似 `env` 的 shell 命令启动 Python 程序：

```bash
$ env SOMEVAR=somevalue python3 somescript.py
```

环境变量在映射 `os.environ` 中作为文本字符串被访问。这里有一个例子：

```python
import os
path = os.environ['PATH']
user = os.environ['USER']
editor = os.environ['EDITOR']
val = os.environ['SOMEVAR']
... etc ...
```

要修改环境变量，请设置 `os.environ` 变量。例如：

```python
os.environ['NAME'] = 'VALUE'
```

对 `os.environ` 的修改会影响当前运行的程序以及随后创建的任何子进程——例如，由 `subprocess` 模块创建的进程。

与命令行选项一样，编码不良的环境变量可能会产生使用 `'surrogateescape'` 错误处理策略的字符串。

## 9.6 文件和文件对象

要打开文件，请使用内置的 `open()` 函数。通常，`open()` 会接收一个文件名和一个文件模式。它还经常与 `with` 语句结合使用作为上下文管理器。以下是处理文件的几种常见使用模式：

```python
# 将文本文件一次性作为字符串全部读取
with open('filename.txt', 'rt') as file:
    data = file.read()

# 逐行读取文件
with open('filename.txt', 'rt') as file:
    for line in file:
        ...

# 写入文本文件
with open('out.txt', 'wt') as file:
    file.write('Some output\n')
    print('More output', file=file)
```

在大多数情况下，使用 `open()` 是非常简单的。你只需要提供要打开的文件名以及文件模式。例如：

```python
open('name.txt')       # 以读取模式打开 "name.txt"
open('name.txt', 'rt')  # 以读取模式打开 "name.txt" (相同)
open('name.txt', 'wt')  # 以写入模式打开 "name.txt"
open('data.bin', 'rb')  # 二进制模式读取
open('data.bin', 'wb')  # 二进制模式写入
```

对于大多数程序来说，你永远不需要掌握除这些简单示例之外的更多知识来处理文件。然而，`open()` 还有一些特殊情况和较为冷门的特性值得了解。接下来的几个章节将更详细地讨论 `open()` 和文件 I/O。

### 9.6.1 文件名

要打开一个文件，你需要向 `open()` 提供文件名。文件名既可以是完整指定的绝对路径，例如 `'/Users/guido/Desktop/files/old/data.csv'`，也可以是相对路径，例如 `'data.csv'` 或 `'..\old\data.csv'`。对于相对文件名，文件位置是相对于 `os.getcwd()` 返回的当前工作目录来确定的。当前工作目录可以使用 `os.chdir(newdir)` 来更改。

文件名本身可以用多种形式编码。如果它是一个文本字符串，在传递给宿主操作系统之前，该名称将根据 `sys.getfilesystemencoding()` 返回的文本编码进行解析。如果文件名是字节字符串，则保持不编码并原样传递。如果你正在编写必须处理损坏或编码错误文件名的程序，那么后一种选项可能会很有用——你可以传递名称的原始二进制表示，而不是将其作为文本传递。这看起来像是一个冷门的边缘案例，但 Python 通常被用于编写操作文件系统的系统级脚本。滥用文件系统是黑客用来隐藏踪迹或破坏系统工具的常用技巧。

除了文本和字节外，任何实现了特殊方法 `__fspath__()` 的对象都可以用作文件名。`__fspath__()` 方法必须返回一个与实际名称相对应的文本或字节对象。这就是使 `pathlib` 等标准库模块能够工作的机制。例如：

```python
>>> from pathlib import Path
>>> p = Path('Data/portfolio.csv')
>>> p.__fspath__()
'Data/portfolio.csv'
>>>
```

潜在地，只要你的自定义 `Path` 对象实现了 `__fspath__()` 并且能够解析为系统上正确的文件名，它就可以与 `open()` 配合工作。

最后，文件名可以提供为低级整数文件描述符。这要求该“文件”已经在系统中以某种方式打开。它可能对应于网络套接字、管道或其他暴露文件描述符的系统资源。下面是一个使用 `os` 模块直接打开文件，然后将其转换为正式文件对象的示例：

```python
>>> import os
>>> fd = os.open('/etc/passwd', os.O_RDONLY)
>>> fd
3
>>> file = open(fd, 'rt')
>>> file
<_io.TextIOWrapper name=3 mode='rt' encoding='UTF-8'>
>>> data = file.read()
>>>
```

当像这样打开一个现有文件描述符时，返回文件的 `close()` 方法也将关闭底层的描述符。可以通过向 `open()` 传递 `closefd=False` 来禁用此行为。例如：

```python
file = open(fd, 'rt', closefd=False)
```

### 9.6.2 文件模式

打开文件时，你需要指定一个文件模式。核心文件模式包括用于读取的 `'r'`、用于写入的 `'w'` 和用于追加的 `'a'`。

`'w'` 模式会用新内容替换任何现有文件。`'a'` 打开文件用于写入，并将文件指针定位到文件末尾，以便可以追加新数据。

特殊的文件模式 `'x'` 可用于写入文件，但仅在文件尚不存在时才有效。这是防止意外覆盖现有数据的一种有效方法。对于此模式，如果文件已存在，则会引发 `FileExistsError` 异常。

Python 对文本和二进制数据进行了严格区分。要指定数据类型，请在文件模式后追加 `'t'` 或 `'b'`。例如，文件模式 `'rt'` 以文本模式打开文件进行读取，而 `'rb'` 以二进制模式打开文件进行读取。模式决定了文件相关方法（如 `f.read()`）返回的数据类型。在文本模式下，返回字符串；在二进制模式下，返回字节。

通过提供加号（`+`）字符（如 `'rb+'` 或 `'wb+'`），可以打开二进制文件进行就地更新。当文件被打开用于更新时，你可以同时进行输入和输出，只要所有输出操作在任何随后的输入操作之前都刷新了其数据。如果使用 `'wb+'` 模式打开文件，其长度首先会被截断为零。更新模式的一个常见用途是结合 `seek` 操作对文件内容提供随机读/写访问。

### 9.6.3 I/O 缓冲

默认情况下，文件在打开时启用了 I/O 缓冲。通过 I/O 缓冲，I/O 操作以较大的块为单位执行，以避免过多的系统调用。例如，写入操作会开始填充内部内存缓冲区，只有当缓冲区填满时才会真正产生输出。可以通过向 `open()` 提供 `buffering` 参数来更改此行为。例如：

```python
# 以无 I/O 缓冲方式打开二进制模式文件
with open('data.bin', 'wb', buffering=0) as file:
    file.write(data)
    ...
```

值为 `0` 指定无缓冲 I/O，且仅对二进制模式文件有效。值为 `1` 指定行缓冲，通常仅对文本模式文件有意义。任何其他正值表示要使用的缓冲区大小（以字节为单位）。如果没有指定缓冲值，默认行为取决于文件的类型。如果是磁盘上的普通文件，缓冲由块管理，缓冲区大小设置为 `io.DEFAULT_BUFFER_SIZE`。通常这是 4096 字节的某个小倍数，可能会随系统而异。如果文件代表一个交互式终端，则使用行缓冲。

对于普通程序，I/O 缓冲通常不是主要问题。然而，缓冲可能会影响涉及进程间积极通信的应用。例如，有时会出现两个通信的子进程由于内部缓冲问题而导致死锁——例如，一个进程将数据写入缓冲区，但接收者永远看不到这些数据，因为缓冲区没有被刷新。此类问题可以通过指定无缓冲 I/O 或对相关文件进行显式的 `flush()` 调用来解决。例如：

```python
file.write(data)
file.write(data)
...
file.flush()    # 确保所有数据从缓冲区写入
```

### 9.6.4 文本模式编码

对于以文本模式打开的文件，可以使用 `encoding` 和 `errors` 参数指定可选的编码和错误处理策略。例如：

```python
with open('file.txt', 'rt',
        encoding='utf-8', errors='replace') as file:
    data = file.read()
```

传递给 `encoding` 和 `errors` 参数的值与字符串和字节的 `encode()` 和 `decode()` 方法的含义相同。

默认文本编码由 `sys.getdefaultencoding()` 的值决定，并可能随系统而异。如果你预先知道编码，即使它恰好与系统的默认编码匹配，通常最好也显式地提供它。

### 9.6.5 文本模式行处理

对于文本文件，一个复杂之处是换行符的编码。根据宿主操作系统的不同，换行符被编码为 `'\n'`、`'\r\n'` 或 `'\r'`——例如，UNIX 上为 `'\n'`，Windows 上为 `'\r\n'`。默认情况下，Python 在读取时将所有这些行尾符翻译为标准的 `'\n'` 字符。在写入时，换行符会被翻译回系统上使用的默认行尾符。这种行为在 Python 文档中有时被称为“通用换行模式”。

你可以通过向 `open()` 提供 `newline` 参数来更改换行行为。例如：

```python
# 明确要求 '\r\n' 并保持原样
file = open('somefile.txt', 'rt', newline='\r\n')
```

指定 `newline=None` 会启用默认的行处理行为，即所有行尾符都被翻译为标准的 `'\n'` 字符。指定 `newline=''` 会使 Python 识别所有行尾符，但禁用翻译步骤——如果行是以 `'\r\n'` 结尾的，那么 `'\r\n'` 组合将原样保留在输入中。指定 `'\n'`、`'\r'` 或 `'\r\n'` 的值则将其设为预期的行尾符。

## 9.7 I/O 抽象层

`open()` 函数充当了一种高级工厂函数，用于创建不同 I/O 类的实例。这些类体现了不同的文件模式、编码和缓冲行为。它们是以层级结构组合在一起的。`io` 模块中定义了以下类：

```python
FileIO(filename, mode='r', closefd=True, opener=None)
```

打开一个文件用于原始的无缓冲二进制 I/O。`filename` 是 `open()` 函数接受的任何有效文件名。其他参数的含义与 `open()` 相同。

```python
BufferedReader(file [, buffer_size])
BufferedWriter(file [, buffer_size])
BufferedRandom(file [, buffer_size])
```



为文件实现一个缓冲二进制 I/O 层。`file` 是 `FileIO` 的一个实例。`buffer_size` 指定要使用的内部缓冲区大小。类的选择取决于文件是在读取、写入还是更新数据。可选参数 `buffer_size` 指定了所使用的内部缓冲区大小。

```python
TextIOWrapper(buffered, [encoding, [errors [, newline [,
line_buffering [, write_through]]]]])
```

实现文本模式 I/O。`buffered` 是一个缓冲二进制模式文件，例如 `BufferedReader` 或 `BufferedWriter`。`encoding`、`errors` 和 `newline` 参数的含义与 `open()` 相同。`line_buffering` 是一个布尔标志，强制在换行符处刷新 I/O（默认为 `False`）。`write_through` 是一个布尔标志，强制刷新所有写入（默认为 `False`）。

下面是一个示例，展示了文本模式文件是如何逐层构建的：

```python
>>> raw = io.FileIO('filename.txt', 'r')          # 原始二进制模式
>>> buffer = io.BufferedReader(raw)                # 二进制缓冲读取器
>>> file = io.TextIOWrapper(buffer, encoding='utf-8') # 文本模式
>>>
```

通常你不需要像这样手动构建层级——内置的 `open()` 函数处理了所有工作。但是，如果你已经有一个现有的文件对象并想以某种方式更改其处理方式，你可以像上面那样操作这些层级。

要剥离层级，请使用文件的 `detach()` 方法。例如，以下是如何将一个已经是文本模式的文件转换为二进制模式文件：

```python
f = open('something.txt', 'rt')    # 文本模式文件
fb = f.detach()                   # 分离底层的二进制模式文件
data = fb.read()                  # 返回字节 (bytes)
```

### 9.7.1 文件方法

`open()` 返回对象的具体类型取决于所提供的文件模式和缓冲选项的组合。不过，生成的 File 对象都支持表 9.4 中的方法。

**表 9.4 文件方法**

| 方法 | 描述 |
|--------|-------------|
| `f.readable()` | 如果文件可读，则返回 `True`。 |
| `f.read([n])` | 最多读取 `n` 个字节。 |
| `f.readline([n])` | 读取单行输入，最多 `n` 个字符。如果省略 `n`，则读取整行。 |
| `f.readlines([size])` | 读取所有行并返回一个列表。`size` 可选，指定在停止前从文件中读取的大约字符数。 |
| `f.readinto(buffer)` | 将数据读取到内存缓冲区中。 |
| `f.writable()` | 如果文件可写，则返回 `True`。 |
| `f.write(s)` | 写入字符串 `s`。 |
| `f.writelines(lines)` | 写入可迭代对象 `lines` 中的所有字符串。 |
| `f.close()` | 关闭文件。 |
| `f.seekable()` | 如果文件支持随机访问寻址，则返回 `True`。 |
| `f.tell()` | 返回当前文件指针位置。 |
| `f.seek(offset [, where])` | 寻址到新的文件位置。 |
| `f.isatty()` | 如果 `f` 是交互式终端，则返回 `True`。 |
| `f.flush()` | 刷新输出缓冲区。 |
| `f.truncate([size])` | 将文件截断为最多 `size` 个字节。 |
| `f.fileno()` | 返回一个整数文件描述符。 |

`readable()`、`writable()` 和 `seekable()` 方法用于测试支持的文件能力和模式。`read()` 方法将整个文件作为字符串返回，除非可选的**长度 (length)** 参数指定了最大字符数。`readline()` 方法返回下一行输入，包括结尾的换行符；`readlines()` 方法将整个输入文件作为字符串列表返回。`readline()` 方法可选地接受一个最大行长 `n`。如果读取的行超过 `n` 个字符，则返回前 `n` 个字符。剩余的行数据不会被丢弃，将在随后的读取操作中返回。`readlines()` 方法接受一个 `size` 参数，指定在停止前读取的大约字符数。实际读取的字符数可能会大于此值，具体取决于已经缓冲了多少数据。`readinto()` 方法用于避免内存复制，将在稍后讨论。

`read()` 和 `readline()` 通过返回空字符串来表示文件结束 (EOF)。因此，以下代码展示了如何检测 EOF 状态：

```python
while True:
    line = file.readline()
    if not line:     # EOF
        break
    # 语句
    ...
```

你也可以将此代码写成如下形式：

```python
while (line := file.readline()):
    # 语句
    ...
```

读取文件中所有行的一种便捷方法是使用 `for` 循环进行迭代：

```python
for line in file:      # 迭代文件中的所有行
    # 对行进行操作
    ...
```

`write()` 方法将数据写入文件，`writelines()` 方法将字符串的可迭代对象写入文件。`write()` 和 `writelines()` 不会在输出中添加换行符，因此你产生的所有输出应已包含所有必要的格式。

在内部，每个打开的文件对象都保持一个文件指针，存储下次读写操作将发生的字节偏移量。`tell()` 方法返回文件指针的当前值。`seek(offset [, whence])` 方法用于根据整数偏移量和 `whence` 中的放置规则随机访问文件的部分内容。如果 `whence` 是 `os.SEEK_SET`（默认值），`seek()` 认为 `offset` 是相对于文件开头的；如果 `whence` 是 `os.SEEK_CUR`，则位置相对于当前位置移动；如果 `whence` 是 `os.SEEK_END`，则偏移量从文件末尾计算。

`fileno()` 方法返回文件的整数文件描述符，有时用于某些库模块中的低级 I/O 操作。例如，`fcntl` 模块使用文件描述符在 UNIX 系统上提供低级文件控制操作。

`readinto()` 方法用于将数据零拷贝 I/O 到连续内存缓冲区中。它最常与 `numpy` 等专门的库结合使用——例如，直接将数据读取到为数值数组分配的内存中。

文件对象还具有表 9.5 所示的只读数据属性。

**表 9.5 文件属性**

| 属性 | 描述 |
|-----------|-------------|
| `f.closed` | 布尔值指示文件状态：如果文件打开则为 `False`，如果关闭则为 `True`。 |
| `f.mode` | 文件的 I/O 模式。 |
| `f.name` | 如果使用 `open()` 创建，则为文件名。否则，它将是一个指示文件来源的字符串。 |
| `f.newlines` | 文件中实际找到的换行符表示形式。如果尚未遇到换行符，则值为 `None`；或者是一个包含 `'\n'`、`'\r'` 或 `'\r\n'` 的字符串；或者是一个包含所有出现过的不同换行编码的元组。 |
| `f.encoding` | 指示文件编码（如果有）的字符串（例如 `'latin-1'` 或 `'utf-8'`）。如果没有使用编码，则值为 `None`。 |
| `f.errors` | 错误处理策略。 |
| `f.write_through` | 布尔值指示对文本文件的写入是否直接将数据传递到底层的二进制级文件而不进行缓冲。 |

## 9.8 标准输入、输出和错误

解释器提供了三个标准文件类对象，分别称为标准输入、标准输出和标准错误，可通过 `sys.stdin`、`sys.stdout` 和 `sys.stderr` 访问。`stdin` 是一个对应于提供给输入字符流的文件对象。

在解释器中，`stdout` 是接收 `print()` 产生输出的文件对象，而 `stderr` 是接收错误消息的文件。通常情况下，`stdin` 映射到用户的键盘，而 `stdout` 和 `stderr` 则在屏幕上产生文本。

前一节中描述的方法可用于与用户进行 I/O 操作。例如，以下代码向标准输出写入内容，并从标准输入读取一行输入：

```python
import sys
sys.stdout.write("Enter your name : ")
name = sys.stdin.readline()
```

或者，可以使用内置函数 `input(prompt)` 从 `stdin` 读取一行文本，并可选地打印一个提示符：

```python
name = input("Enter your name : ")
```

由 `input()` 读取的行不包括末尾的换行符。这与直接从 `sys.stdin` 读取不同，后者在输入文本中包含换行符。

必要时，`sys.stdout`、`sys.stdin` 和 `sys.stderr` 的值可以用其他文件对象替换，在这种情况下，`print()` 和 `input()` 函数将使用新值。如果需要恢复 `sys.stdout` 的原始值，应先将其保存。解释器启动时 `sys.stdout`、`sys.stdin` 和 `sys.stderr` 的原始值分别存储在 `sys.__stdout__`、`sys.__stdin__` 和 `sys.__stderr__` 中。

## 9.9 目录

要获取目录列表，请使用 `os.listdir(pathname)` 函数。例如，以下是如何打印出目录中的文件名列表：

```python
import os

names = os.listdir('dirname')
for name in names:
    print(name)
```

`listdir()` 返回的名称通常根据 `sys.getfilesystemencoding()` 返回的编码进行解码。如果你将初始路径指定为字节串，则文件名将以未解码的字节串形式返回。例如：

```python
# 返回原始未解码的名称
names = os.listdir(b'dirname')
```

与目录列表相关的一项有用操作是根据模式匹配文件名，这被称为 *globbing*。`pathlib` 模块可用于此目的。例如，下面是一个匹配特定目录中所有 `*.txt` 文件的示例：

```python
import pathlib

for filename in pathlib.Path(dirname).glob('*.txt'):
    print(filename)
```

如果你使用 `rglob()` 而不是 `glob()`，它将递归搜索所有子目录中匹配该模式的文件名。`glob()` 和 `rglob()` 函数都返回一个通过迭代产生文件名的生成器。

## 9.10 `print()` 函数

要打印一系列由空格分隔的值，像这样将它们全部传递给 `print()`：

```python
print('The values are', x, y, z)
```

要抑制或更改行尾结束符，请使用 `end` 关键字参数：

```python
# 抑制换行符
print('The values are', x, y, z, end='')
```

要将输出重定向到文件，请使用 `file` 关键字参数：

```python
# 重定向到文件对象 f
print('The values are', x, y, z, file=f)
```

要更改项目之间的分隔符，请使用 `sep` 关键字参数：

```python
# 在值之间放置逗号
print('The values are', x, y, z, sep=',')
```

## 9.11 生成输出

直接操作文件对程序员来说最为熟悉。然而，生成器函数也可以用来将 I/O 流发射为一系列数据片段。为此，请像使用 `write()` 或 `print()` 函数一样使用 `yield` 语句。这里有一个示例：

```python
def countdown(n):
    while n > 0:
        yield f'T-minus {n}\n'
        n -= 1
    yield 'Kaboom!\n'
```

以这种方式产生输出流提供了灵活性，因为它与实际将流导向预期目的地的代码解耦。例如，如果你想将上述输出路由到文件 `f`，可以这样做：

```python
lines = countdown(5)
f.writelines(lines)
```

相反，如果你想将输出重定向到套接字 `s`，可以这样做：

```python
for chunk in lines:
    s.sendall(chunk)
```

或者，如果你只是想将所有输出捕获在一个字符串中，可以这样做：

```python
out = ''.join(lines)
```

更高级的应用可以使用这种方法来实现自己的 I/O 缓冲。例如，一个生成器可以发射小的文本片段，而另一个函数随后将这些片段收集到较大的缓冲区中，以创建更高效的单次 I/O 操作。

```python
chunks = []
buffered_size = 0
for chunk in count:
    chunks.append(chunk)
    buffered_size += len(chunk)
    if buffered_size >= MAXBUFFERSIZE:
        outf.write(''.join(chunks))
        chunks.clear()
        buffered_size = 0
outf.write(''.join(chunks))
```

对于将输出路由到文件或网络连接的程序，生成器方法还可以显著降低内存使用，因为整个输出流通常可以以小片段的形式生成和处理，而不是先被收集到一个巨大的输出字符串或字符串列表中。

## 9.12 消耗输入

对于消耗碎片化输入的程序，增强型生成器在解码协议和其他 I/O 方面非常有用。这里有一个增强型生成器的示例，它接收字节片段并将它们组装成行：

```python
def line_receiver():
    data = bytearray()
    line = None
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

在这个示例中，生成器被编程为接收被收集到字节数组中的字节片段。如果数组包含换行符，则提取一行并返回。否则，返回 `None`。以下是一个说明其工作原理的示例：

```python
>>> r = line_receiver()
>>> r.send(None)    # 必要的起始步骤
>>> r.send(b'hello')
>>> r.send(b'world\nit ')
b'hello world\n'
>>> r.send(b'works!')
>>> r.send(b'\n')
b'it works!\n'
>>>
```

这种方法一个有趣的副作用是，它将获取输入数据必须执行的实际 I/O 操作外部化了。具体来说，`line_receiver()` 的实现完全不包含任何 I/O 操作！这意味着它可以用于不同的上下文。例如，配合套接字使用：

```python
r = line_receiver()
data = None
while True:
    while not (line:=r.send(data)):
        data = sock.recv(8192)

    # 处理该行
    ...
```

或者配合文件使用：

```python
r = line_receiver()
data = None
while True:
    while not (line:=r.send(data)):
        data = file.read(10000)

    # 处理该行
    ...
```

甚至在异步代码中使用：

```python
async def reader(ch):
    r = line_receiver()
    data = None
    while True:
        while not (line:=r.send(data)):
            data = await ch.receive(8192)
        
        # 处理该行
        ...
```

## 9.13 对象序列化

有时需要序列化对象的表示，以便可以通过网络传输、保存到文件或存储在数据库中。一种方法是将数据转换为标准编码，如 JSON 或 XML。此外，还有一种常用的 Python 特有数据序列化格式，称为 *Pickle*。



`pickle` 模块将对象序列化为字节流，该字节流可用于在稍后时间点重建对象。`pickle` 的接口很简单，由两个操作组成：`dump()` 和 `load()`。例如，以下代码将一个对象写入文件：

```python
import pickle
obj = SomeObject()
with open(filename, 'wb') as file:
    pickle.dump(obj, file)        # 将对象保存到文件中
```

要恢复对象，请使用：

```python
with open(filename, 'rb') as file:
    obj = pickle.load(file)    # Restore the object
```

`pickle` 使用的数据格式拥有自己的记录分帧机制。因此，可以通过连续执行一系列 `dump()` 操作来保存一个对象序列。要恢复这些对象，只需使用类似的 `load()` 操作序列即可。

在网络编程中，通常使用 `pickle` 来创建字节编码的消息。为此，请使用 `dumps()` 和 `loads()`。这些函数处理的是字节字符串，而不是将数据读写到文件中。

```python
obj = SomeObject()

# Turn an object into bytes
data = pickle.dumps(obj)
...

# Turn bytes back into an object
obj = pickle.loads(data)
```

对于用户定义对象，通常不需要进行任何额外操作即可配合 `pickle` 工作。然而，某些类型的对象无法被 `pickle` 序列化。这些通常是包含运行时状态的对象——例如打开的文件、线程、闭包、生成器等。为了处理这些复杂情况，类可以定义特殊方法 `__getstate__()` 和 `__setstate__()`。

如果定义了 `__getstate__()` 方法，它将被调用以创建代表对象状态的值。`__getstate__()` 返回的值通常是一个字符串、元组、列表或字典。`__setstate__()` 方法在反序列化期间接收该值，并应据此恢复对象的状态。

在对对象进行编码时，`pickle` 并不包含底层的源代码本身，而是编码一个指向定义类的名称引用。反序列化时，该名称被用于在系统中进行源代码查找。为了使反序列化正常工作，`pickle` 的接收方必须已经安装了正确的源代码。同样重要的是要强调，`pickle` 本身是不安全的——反序列化不受信任的数据是一个已知的远程代码执行攻击向量。因此，只有在您能完全确保运行时环境安全的情况下，才应使用 `pickle`。

## 9.14 阻塞操作与并发

I/O 的一个基本方面是阻塞（blocking）的概念。就其本质而言，I/O 与现实世界相连，通常涉及等待输入或设备就绪。例如，读取网络数据的代码可能会在套接字上执行如下接收操作：

```python
data = sock.recv(8192)
```

当这条语句执行时，如果数据可用，它可能会立即返回。然而，如果数据不可用，它将停止——等待数据到达。这就是阻塞。当程序被阻塞时，没有任何其他事情发生。

对于数据分析脚本或简单的程序，阻塞并不是需要担心的问题。但是，如果您希望程序在某个操作被阻塞时能执行其他任务，则需要采取不同的方法。这就是并发（concurrency）的核心问题——让程序一次能处理多件事。一个常见的问题是让程序同时在两个或多个不同的网络套接字上进行读取：

```python
def reader1(sock):
    while (data := sock.recv(8192)):
        print('reader1 got:', data)

def reader2(sock):
    while (data := sock.recv(8192)):
        print('reader2 got:', data)

# Problem: How to make reader1() and reader2()
# run at the same time?
```

本节的其余部分概述了几种解决此问题的不同方法。不过，这里并非旨在提供一个完整的并发教程。为此，您需要参考其他资源。

### 9.14.1 非阻塞 I/O

避免阻塞的一种方法是使用所谓的非阻塞 I/O。这是一种必须启用的一种特殊模式——例如，在套接字上：

```python
sock.setblocking(False)
```

一旦启用，如果某个操作本会产生阻塞，现在将抛出一个异常。例如：

```python
try:
    data = sock.recv(8192)
except BlockingIOError as e:
    # No data is available
    ...
```

面对 `BlockingIOError`，程序可以选择去处理其他事情，并在稍后重试 I/O 操作以查看是否有数据到达。例如，以下是您如何同时在两个套接字上读取数据的方式：

```python
def reader1(sock):
    try:
        data = sock.recv(8192)
        print('reader1 got:', data)
    except BlockingIOError:
        pass

def reader2(sock):
    try:
        data = sock.recv(8192)
        print('reader2 got:', data)
    except BlockingIOError:
        pass

def run(sock1, sock2):
    sock1.setblocking(False)
    sock2.setblocking(False)
    while True:
        reader1(sock1)
        reader2(sock2)
```

在实践中，仅依赖非阻塞 I/O 是笨拙且低效的。例如，这个程序的核心是最后的 `run()` 函数，它会运行在一个低效的忙循环（busy loop）中，因为它在不断地尝试读取套接字。虽然这行得通，但并不是一个好的设计。

### 9.14.2 I/O 轮询

与其依赖异常和空转，不如通过轮询 I/O 通道来查看数据是否可用。可以使用 `select` 或 `selectors` 模块来实现此目的。例如，这里是一个稍微修改后的 `run()` 函数版本：

```python
from selectors import DefaultSelector, EVENT_READ, EVENT_WRITE

def run(sock1, sock2):
    selector = DefaultSelector()
    selector.register(sock1, EVENT_READ, data=reader1)
    selector.register(sock2, EVENT_READ, data=reader2)
    # Wait for something to happen
    while True:
        for key, evt in selector.select():
            func = key.data
            func(key.fileobj)
```

在这段代码中，每当在相应的套接字上检测到 I/O 时，循环就会将 `reader1()` 或 `reader2()` 函数作为回调函数分发出去。`selector.select()` 操作本身是阻塞的，它会等待 I/O 发生。因此，与之前的示例不同，它不会让 CPU 疯狂空转。

这种 I/O 处理方法是许多所谓的“异步”框架（如 `asyncio`）的基础，尽管您通常看不到事件循环（event loop）的内部运作。

### 9.14.3 线程

在之前的两个示例中，并发需要使用一个特殊的 `run()` 函数来驱动计算。作为替代方案，您可以使用线程编程和 `threading` 模块。可以将线程视为在程序内部运行的独立任务。这里是一个同时在两个套接字上读取数据的代码示例：

```python
import threading

def reader1(sock):
    while (data := sock.recv(8192)):
        print('reader1 got:', data)

def reader2(sock):
    while (data := sock.recv(8192)):
        print('reader2 got:', data)

t1 = threading.Thread(target=reader1, args=[sock1])
t2 = threading.Thread(target=reader2, args=[sock2])

# Start the threads
t1.start()
t2.start()

# Wait for the threads to finish
t1.join()
t2.join()
```

在这个程序中，`reader1()` 和 `reader2()` 函数并发执行。这是由宿主操作系统管理的，因此您不需要深入了解其工作原理。如果一个线程中发生了阻塞操作，它不会影响另一个线程。

线程编程的全部内容已超出本书的讨论范围。不过，在本章随后的 `threading` 模块章节中提供了一些额外的示例。

### 9.14.4 使用 `asyncio` 进行并发执行

`asyncio` 模块提供了一种替代线程的并发实现。在内部，它基于一个使用 I/O 轮询的事件循环。然而，通过使用特殊的 `async` 函数，其高级编程模型看起来与线程非常相似。这里有一个示例：

```python
import asyncio

async def reader1(sock):
    loop = asyncio.get_event_loop()
    while (data := await loop.sock_recv(sock, 8192)):
        print('reader1 got:', data)

async def reader2(sock):
    loop = asyncio.get_event_loop()
    while (data := await loop.sock_recv(sock, 8192)):
        print('reader2 got:', data)

async def main(sock1, sock2):
    loop = asyncio.get_event_loop()
    t1 = loop.create_task(reader1(sock1))
    t2 = loop.create_task(reader2(sock2))

    # Wait for the tasks to finish
    await t1
    await t2

...

# Run it
asyncio.run(main(sock1, sock2))
```

关于 `asyncio` 的完整细节需要一本专门的书籍来阐述。你只需要知道，许多库和框架都宣称支持异步操作。通常这意味着通过 `asyncio` 或类似的模块来支持并发执行。大部分代码可能会涉及 `async` 函数及其相关特性。

## 9.15 标准库模块

大量标准库模块被用于各种与 I/O 相关的任务。本节将简要概述常用模块，并提供一些示例。完整的参考资料可以在网上或 IDE 中找到，此处不再重复。本节的主要目的是通过向你提供应使用的模块名称，以及每个模块涉及的常见编程任务示例，为你指明方向。

许多示例以交互式 Python 会话的形式呈现。这些是鼓励你亲自尝试的实验。

### 9.15.1 `asyncio` 模块

`asyncio` 模块通过 I/O 轮询和底层事件循环，为并发 I/O 操作提供支持。它主要用于涉及网络和分布式系统的代码。下面是一个使用低级套接字的 TCP echo 服务器示例：

```python
import asyncio
from socket import *

async def echo_server(address):
    loop = asyncio.get_event_loop()
    sock = socket(AF_INET, SOCK_STREAM)
    sock.setsockopt(SOL_SOCKET, SO_REUSEADDR, 1)
    sock.bind(address)
    sock.listen(5)
    sock.setblocking(False)
    print('Server listening at', address)
    with sock:
        while True:
            client, addr = await loop.sock_accept(sock)
            print('Connection from', addr)
            loop.create_task(echo_client(loop, client))

async def echo_client(loop, client):
    with client:
        while True:
            data = await loop.sock_recv(client, 10000)
            if not data:
                break
            await loop.sock_sendall(client, b'Got:' + data)
    print('Connection closed')

if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    loop.create_task(echo_server(loop, ('', 25000)))
    loop.run_forever()
```

要测试此代码，请使用 `nc` 或 `telnet` 等程序连接到机器的 25000 端口。代码应该会原样返回（echo）你输入的文本。如果你使用多个终端窗口连接多次，你会发现该代码可以并发处理所有连接。

大多数使用 `asyncio` 的应用程序可能会在比套接字更高的层级上运行。然而，在这些应用程序中，你仍然必须使用特殊的 `async` 函数，并以某种方式与底层的事件循环进行交互。

### 9.15.2 `binascii` 模块

`binascii` 模块包含将二进制数据转换为各种基于文本的表示形式（如十六进制和 base64）的函数。例如：

```python
>>> binascii.b2a_hex(b'hello')
b'68656c6c6f'
>>> binascii.a2b_hex(_)
b'hello'
>>> binascii.b2a_base64(b'hello')
b'aGVsbG8=\n'
>>> binascii.a2b_base64(_)
b'hello'
>>> 
```

类似的功能也可以在 `base64` 模块以及 `bytes` 的 `hex()` 和 `fromhex()` 方法中找到。例如：

```python
>>> a = b'hello'
>>> a.hex()
'68656c6c6f'
>>> bytes.fromhex(_)
b'hello'
>>> import base64
>>> base64.b64encode(a)
b'aGVsbG8='
>>>
```

### 9.15.3 `cgi` 模块

假设你只想在网站上放置一个基础表单。也许是你每周一次的“猫与类别”新闻通讯的注册表单。当然，你可以安装最新的 Web 框架并花所有时间去钻研它。或者，你也可以直接写一个基础的 CGI 脚本——走复古路线。`cgi` 模块就是用来实现这一点的。

假设你在网页上有以下表单片段：

```html
<form method="POST" action="cgi-bin/register.py">
    <p>
        To register, please provide a contact name and email
        address.
    </p>
    <div>
        <input name="name" type="text">Your name:
    </div>
    <div>
        <input name="email" type="email">Your email:
    </div>
    <div class="modal-footer justify-content-center">
        <input type="submit" name="submit" value="Register">
    </div>
</form>
```

这是一个在另一端接收表单数据的 CGI 脚本：



```python
#!/usr/bin/env python
import cgi
try:
    form = cgi.FieldStorage()
    name = form.getvalue('name')
    email = form.getvalue('email')
    # Validate the responses and do whatever
    ...
    # Produce an HTML result (or redirect)
    print("Status: 302 Moved\r")
    print("Location: https://www.mywebsite.com/thanks.html\r")
    print("\r")
except Exception as e:
    print("Status: 501 Error\r")
    print("Content-type: text/plain\r")
    print("\r")
    print("Some kind of error occurred.\r")
```

写这样的 CGI 脚本能让你在互联网初创公司找到工作吗？可能不能。它能解决你的实际问题吗？很有可能。

## 9.15.4 `configparser` 模块

INI 文件是一种常见的以人类可读形式编码程序配置信息的格式。示例如下：

```ini
# config.ini
; A comment
[section1]
name1 = value1
name2 = value2

[section2]
; Alternative syntax
name1: value1
name2: value2
```

`configparser` 模块用于读取 `.ini` 文件并提取值。这是一个基础示例：

```python
import configparser

# Create a config parser and read a file
cfg = configparser.ConfigParser()
cfg.read('config.ini')

# Extract values
a = cfg.get('section1', 'name1')
b = cfg.get('section2', 'name2')
...
```

它还提供更高级的功能，包括字符串插值特性、合并多个 `.ini` 文件的能力、提供默认值等。更多示例请参阅官方文档。

## 9.15.5 `csv` 模块

`csv` 模块用于读写由 Microsoft Excel 等程序生成或从数据库导出的逗号分隔值 (CSV) 文件。使用它时，先打开一个文件，然后在它之上封装一层 CSV 编码/解码层。例如：

```python
import csv

# Read a CSV file into a list of tuples
def read_csv_data(filename):
    with open(filename) as file:
        rows = csv.reader(file)
        # First line is often a header. This reads it
        headers = next(rows)
        # Now read the rest of the data
        for row in rows:
            # Do something with row
            ...

# Write Python data to a CSV file
def write_csv_data(filename, headers, rows):
    with open(filename, "w") as file:
        out = csv.writer(file)
        out.writerow(headers)
        out.writerows(rows)
```

一个常用的便捷方法是使用 `DictReader()`。它将 CSV 文件的第一行解释为表头，并将每一行作为字典而非元组返回。

```python
import csv

def find_nearby(filename):
    with open(filename) as file:
        rows = csv.DictReader(file)
        for row in rows:
            lat = float(row['latitude'])
            lon = float(row['longitude'])
            if close_enough(lat, lon):
                print(row)
```

`csv` 模块除了读写 CSV 数据之外，并没有太多其他功能。它提供的主要好处是该模块知道如何正确地对数据进行编码/解码，并处理涉及引号、特殊字符和其他细节的大量边缘情况。你可以使用这个模块来编写简单的脚本，用于清理或准备要与其他程序一起使用的数据。如果你想使用 CSV 数据执行数据分析任务，请考虑使用第三方包，例如流行的 `pandas` 库。

## 9.15.6 `errno` 模块

每当发生系统级错误时，Python 都会通过一个 `OSError` 的子类异常来报告。一些较为常见的系统错误由 `OSError` 的独立子类表示，例如 `PermissionError` 或 `FileNotFoundError`。然而，在实践中，可能会出现数百种其他错误。对于这些错误，任何 `OSError` 异常都携带一个可以检查的数字 `errno` 属性。`errno` 模块提供了与这些错误代码相对应的符号常量。它们经常用于编写专门的异常处理器。例如，这是一个检查设备上是否没有剩余空间的异常处理器：

```python
import errno

def write_data(file, data):
    try:
        file.write(data)
    except OSError as e:
        if e.errno == errno.ENOSPC:
            print("You're out of disk space!")
        else:
            raise # Some other error. Propagate
```

## 9.15.7 `fcntl` 模块

`fcntl` 模块用于在 UNIX 上使用 `fcntl()` 和 `ioctl()` 系统调用执行低级 I/O 控制操作。如果你想执行任何形式的文件锁定（这在并发和分布式系统的上下文中偶尔会出现），这也是要使用的模块。下面是一个结合使用 `fcntl.flock()` 在所有进程之间实现互斥锁并打开文件的示例：

```python
import fcntl

with open("somefile", "r") as file:
    try:
        fcntl.flock(file.fileno(), fcntl.LOCK_EX)
        # Use the file
        ...
    finally:
        fcntl.flock(file.fileno(), fcntl.LOCK_UN)
```

## 9.15.8 `hashlib` 模块

`hashlib` 模块提供了用于计算加密哈希值（如 MD5 和 SHA-1）的函数。以下示例说明了如何使用该模块：

```python
>>> h = hashlib.new('sha256')
>>> h.update(b'Hello')    # Feed data
>>> h.update(b'World')
>>> h.digest()
b'\xaa5\x91\xa6\xd4\x0b\xf4@J\x01\x173\x173\xcf\xb7\x81\x90\xdb\x6e\xbf\x0b\xcd\xda3+W\x82w\x8d9\xad\x9f\x14n'
>>> h.hexdigest()
'a591a6d40bf42040a011733cfb7b190d62c65bf0bc5da32b57d9ad9f146e'
>>> h.digest_size
32
>>>
```

## 9.15.9 `http` 包

`http` 包包含大量与 HTTP 互联网协议低级实现相关的代码。它可用于实现服务器和客户端。然而，该包的大部分内容被认为是遗留代码，对于日常工作来说太低级了。从事 HTTP 开发的专业程序员更有可能使用第三方库，如 `requests`、`httpx`、`Django`、`flask` 等。

尽管如此，`http` 包一个非常有用的彩蛋是 Python 能够运行一个独立的 Web 服务器。进入一个包含文件的目录并输入以下内容：

```bash
$ python -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

现在，如果你将浏览器指向正确的端口，Python 就会将文件提供给你的浏览器。你不会用它来运行一个正式的网站，但它对于测试和调试与 Web 相关的程序非常有用。例如，作者曾使用它来本地测试涉及 HTML、Javascript 和 WebAssembly 混合的程序。

## 9.15.10 `io` 模块

`io` 模块主要包含用于实现 `open()` 函数返回的文件对象的类定义。直接访问这些类并不常见。不过，该模块还包含一对类，可用于以字符串和字节的形式“伪造”一个文件。这在测试和其他需要提供“文件”但以不同方式获取数据的应用中非常有用。

`StringIO()` 类在字符串之上提供了一个类文件接口。例如，以下是如何将输出写入字符串的方式：

```python
# Function that expects a file
def greeting(file):
    file.write('Hello\n')
    file.write('World\n')

# Call the function using a real file
with open('out.txt', 'w') as file:
    greeting(file)

# Call the function with a "fake" file
import io
file = io.StringIO()
greeting(file)

# Get the resulting output
output = file.getvalue()
```

同样，你可以创建一个 `StringIO` 对象并将其用于读取：

```python
file = io.StringIO('hello\nworld\n')
while (line := file.readline()):
    print(line, end='')
```

`BytesIO()` 类具有类似的目的，但用于模拟字节的二进制 I/O。

## 9.15.11 `json` 模块

`json` 模块可用于对 JSON 格式的数据进行编码和解码，这种格式常用于微服务和 Web 应用程序的 API 中。有两个用于转换数据的基本函数：`dumps()` 和 `loads()`。`dumps()` 接收一个 Python 字典并将其编码为 JSON Unicode 字符串：

```python
>>> import json
>>> data = { 'name': 'Mary A. Python', 'email': 'mary123@python.org' }
>>> s = json.dumps(data)
>>> s
'{"name": "Mary A. Python", "email": "mary123@python.org"}'
>>>
```

`loads()` 函数则执行反向操作：

```python
>>> d = json.loads(s)
>>> d == data
True
>>>
```

`dumps()` 和 `loads()` 函数都有许多选项来控制转换的各个方面以及与 Python 类实例的接口。这超出了本节的范围，但在官方文档中可以找到大量相关信息。

## 9.15.12 `logging` 模块

`logging` 模块是用于报告程序诊断和打印式调试的事实标准模块。它可以将输出路由到日志文件，并提供大量配置选项。一种常见的做法是编写代码创建 `Logger` 实例并像这样发布消息：

```python
import logging
log = logging.getLogger(__name__)

# Function that uses logging
def func(args):
    log.debug("A debugging message")
    log.info("An informational message")
    log.warning("A warning message")
    log.error("An error message")
    log.critical("A critical message")

# Configuration of logging (occurs one at program startup)
if __name__ == '__main__':
    logging.basicConfig(
        level=logging.WARNING,
        filename="output.log"
    )
```

内置的日志级别共有五个，按严重程度递增排序。在配置日志系统时，你需要指定一个充当过滤器的级别。只有该级别或更严重程度的消息会被报告。日志记录提供了大量配置选项，大多数与日志消息的后端处理相关。通常在编写应用程序代码时，你不需要了解这些——你只需在给定的 `Logger` 实例上使用 `debug()`、`info()`、`warning()` 等方法即可。任何特殊配置都在程序启动时的特殊位置（如 `main()` 函数或主代码块中）进行。

## 9.15.13 `os` 模块

`os` 模块提供了一个可移植的接口，用于访问常见的操作系统函数，通常与进程环境、文件、目录、权限等相关。其编程接口紧跟 C 语言编程和 POSIX 等标准。

从实际角度来看，该模块的大部分内容可能过于底层，无法直接用于典型的应用程序。然而，如果你曾经面临执行某些晦涩的低级系统操作（例如打开 TTY），你很有可能在这里找到相应的功能。

## 9.15.14 `os.path` 模块

`os.path` 模块是一个用于操作路径名并对文件系统执行常见操作的遗留模块。其功能在很大程度上已被较新的 `pathlib` 模块取代，但由于其使用仍然非常广泛，你在很多代码中仍会看到它。

该模块解决的一个根本问题是对 UNIX（正斜杠 `/`）和 Windows（反斜杠 `\`）路径分隔符的可移植处理。`os.path.join()` 和 `os.path.split()` 等函数经常被用于拆分文件路径并将它们重新组合：

```python
>>> filename = '/Users/beazley/Desktop/old/data.csv'
>>> os.path.split(filename)
('/Users/beazley/Desktop/old', 'data.csv')
>>> os.path.join('/Users/beazley/Desktop', 'out.txt')
'/Users/beazley/Desktop/out.txt'
>>>
```

下面是一个使用这些函数的代码示例：

```python
import os.path

def clean_line(line):
    # 对一行（无论什么内容）进行整理
    return line.strip().upper() + '\n'

def clean_data(filename):
    dirname, basename = os.path.split(filename)
    newname = os.path.join(dirname, basename+'.clean')
    with open(newname, 'w') as out_f:
        with open(filename, 'r') as in_f:
            for line in in_f:
                out_f.write(clean_line(line))
```

`os.path` 模块还包含许多函数，如 `isfile()`、`isdir()` 和 `getsize()`，用于对文件系统进行测试并获取文件元数据。例如，以下函数返回一个简单文件或目录中所有文件的总字节数：

```python
import os.path

def compute_usage(filename):
    if os.path.isfile(filename):
        return os.path.getsize(filename)
    elif os.path.isdir(filename):
        return sum(compute_usage(os.path.join(filename, name)) for name in os.listdir(filename))
    else:
        raise RuntimeError('Unsupported file kind')
```

## 9.15.15 `pathlib` 模块

`pathlib` 模块是以可移植且高级的方式操作路径名的现代方法。它将许多面向文件的功能整合在一起，并使用面向对象的接口。其核心对象是 `Path` 类。例如：

```python
from pathlib import Path

filename = Path('/Users/beazley/old/data.csv')
```



一旦你拥有了 `Path` 的实例 `filename`，就可以对其执行各种操作来操纵文件名。例如：

```python
>>> filename.name
'data.csv'
>>> filename.parent
Path('/Users/beazley/old')
>>> filename.parent / 'newfile.csv'
Path('/Users/beazley/old/newfile.csv')
>>> filename.parts
('/', 'Users', 'beazley', 'old', 'data.csv')
>>> filename.with_suffix('.csv.clean')
Path('/Users/beazley/old/data.csv.clean')
>>>
```

`Path` 实例还具有获取文件元数据、获取目录列表以及其他类似功能的函数。这里是对前一节中 `compute_usage()` 函数的重新实现：

```python
import pathlib

def compute_usage(filename):
    pathname = pathlib.Path(filename)
    if pathname.is_file():
        return pathname.stat().st_size
    elif pathname.is_dir():
        return sum(path.stat().st_size
                  for path in pathname.rglob('*')
                  if path.is_file())
    else:
        raise RuntimeError('Unsupported file kind')
```

### 9.15.16 `re` 模块

`re` 模块用于使用正则表达式执行文本匹配、搜索和替换操作。这里有一个简单的示例：

```python
>>> text = 'Today is 3/27/2018. Tomorrow is 3/28/2018.'
>>> # 查找所有日期出现的位置
>>> import re
>>> re.findall(r'\d{1,2}/\d{1,2}/\d+', text)
['3/27/2018', '3/28/2018']
>>> # 将所有日期替换为替换文本
>>> re.sub(r'(\d+)/(\d+)/(\d+)', r'\3-\2-\1', text)
'Today is 2018-3-27. Tomorrow is 2018-3-28.'
>>>
```

正则表达式常因其晦涩的语法而臭名昭著。在本例中，`\d+` 被解释为“一个或多个数字”。关于模式语法的更多信息可以在 `re` 模块的官方文档中找到。

### 9.15.17 `shutil` 模块

`shutil` 模块用于执行一些你原本可能会在 shell 中执行的常见任务。这些任务包括复制和删除文件、操作归档文件等等。例如，复制文件：

```python
import shutil

shutil.copy(srcfile, dstfile)
```

移动文件：

```python
shutil.move(srcfile, dstfile)
```

复制目录树：

```python
shutil.copytree(srcdir, dstdir)
```

删除目录树：

```python
shutil.rmtree(pathname)
```

`shutil` 模块通常被用作直接使用 `os.system()` 函数执行 shell 命令的一个更安全、更可移植的替代方案。

### 9.15.18 `select` 模块

`select` 模块用于对多个 I/O 流进行简单的轮询。也就是说，它可以用来监视一组文件描述符，看是否有传入数据或是否能够接收传出数据。以下示例展示了典型用法：

```python
import select

# 代表文件描述符的对象集合。必须是
# 整数或具有 fileno() 方法的对象。
want_to_read = [ ... ]
want_to_write = [ ... ]
check_exceptions = [ ... ]

# 超时时间（或 None）
timeout = None

# 轮询 I/O
can_read, can_write, have_exceptions = \
    select.select(want_to_read, want_to_write, check_exceptions, timeout)

# 执行 I/O 操作
```

在代码中，构建了三组文件描述符。这些组分别对应读取、写入和异常。它们与可选的超时时间一起传递给 `select()`。`select()` 返回传递参数的三个子集。这些子集代表了可以执行请求操作的文件。例如，返回在 `can_read` 中的文件有待处理的传入数据。

`select()` 函数是一个标准的低级系统调用，通常用于监视系统事件以及实现异步 I/O 框架（如内置的 `asyncio` 模块）。

除了 `select()`，`select` 模块还公开了 `poll()`、`epoll()`、`kqueue()` 以及提供类似功能的其他变体函数。这些函数的可用性因操作系统而异。

`selectors` 模块为 `select` 提供了一个更高层的接口，在某些情况下可能会很有用。在之前的 9.14.2 节中给出过一个示例。

### 9.15.19 `smtplib` 模块

`smtplib` 模块实现了 SMTP 的客户端侧，通常用于发送电子邮件。该模块的一个常见用途是在一个专门用于发送电子邮件的脚本中。这里有一个示例：

```python
import smtplib

fromaddr = "someone@some.com"
toaddrs = ["recipient@other.com" ]
amount = 123.45
msg = f"""From: {fromaddr}\r
\r
Pay {amount} bitcoin or else. We're watching.\r
"""

server = smtplib.SMTP('localhost')
server.sendmail(fromaddr, toaddrs, msg)
server.quit()
```

还有其他功能用于处理密码、身份验证等事项。但是，如果你在某台机器上运行脚本，且该机器配置为支持电子邮件，那么上面的示例通常就能完成工作。

### 9.15.20 `socket` 模块

`socket` 模块提供了对网络编程函数的低级访问。该接口模仿了标准 BSD socket 接口，这在 C 语言的系统编程中非常常见。

以下示例展示了如何建立传出连接并接收响应：

```python
from socket import socket, AF_INET, SOCK_STREAM

sock = socket(AF_INET, SOCK_STREAM)
sock.connect(('python.org', 80))
sock.send(b'GET /index.html HTTP/1.0\r\n\r\n')
parts = []
while True:
    part = sock.recv(10000)
    if not part:
        break
    parts.append(part)
```

```python
break
    parts.append(part)
response = b'.join(part)
print(part)
```

以下示例展示了一个基础的 echo 服务器，它接受客户端连接并将其接收到的任何数据原样返回。要测试此服务器，请运行它，然后在另一个终端会话中使用 `telnet localhost 25000` 或 `nc localhost 25000` 等命令连接到该服务器。

点击此处查看代码图片

```python
from socket import socket, AF_INET, SOCK_STREAM

def echo_server(address):
    sock = socket(AF_INET, SOCK_STREAM)
    sock.bind(address)
    sock.listen(1)
    while True:
        client, addr = sock.accept()
        echo_handler(client, addr)

def echo_handler(client, addr):
    print('Connection from:', addr)
    with client:
        while True:
            data = client.recv(10000)
            if not data:
                break
            client.sendall(data)
    print('Connection closed')

if __name__ == '__main__':
    echo_server(('', 25000))
```

对于 UDP 服务器，不存在连接过程。然而，服务器仍必须将套接字绑定到一个已知地址。以下是一个典型的 UDP 服务器和客户端示例：

点击此处查看代码图片

```python
# udp.py

from socket import socket, AF_INET, SOCK_DGRAM

def run_server(address):
    sock = socket(AF_INET, SOCK_DGRAM) # 1. 创建 UDP 套接字
    sock.bind(address)                 # 2. 绑定到地址/端口
    while True:
        msg, addr = sock.recvfrom(2000) # 3. 获取消息
        # ... 执行某些操作
        response = b'world'
        sock.sendto(response, addr)    # 4. 发回响应

def run_client(address):
    sock = socket(AF_INET, SOCK_DGRAM) # 1. 创建 UDP 套接字
    sock.sendto(b'hello', address)     # 2. 发送消息
    response, addr = sock.recvfrom(2000) # 3. 获取响应
    print("Received:", response)
    sock.close()

if __name__ == '__main__':
    import sys
    if len(sys.argv) != 4:
        raise SystemExit('Usage: udp.py [-client|-server] hostname port')
    address = (sys.argv[2], int(sys.argv[3]))
    if sys.argv[1] == '-server':
        run_server(address)
    elif sys.argv[1] == '-client':
        run_client(address)
```

### 9.15.21 `struct` 模块

`struct` 模块用于在 Python 和二进制数据结构（表示为 Python 字节字符串）之间转换数据。这些数据结构经常用于与用 C 编写的函数、二进制文件格式、网络协议或通过串口进行二进制通信时。

例如，假设你需要构建一个二进制消息，其格式由一个 C 数据结构描述：

点击此处查看代码图片

```c
# Message format: All values are "big endian"
struct Message {
    unsigned short msgid;      // 16 bit unsigned integer
    unsigned int sequence;      // 32 bit sequence number
    float x;                    // 32 bit float
    float y;                    // 32 bit float
};
```

以下是使用 `struct` 模块实现的方法：

点击此处查看代码图片

```python
>>> import struct
>>> data = struct.pack('>HIff', 123, 456, 1.23, 4.56)
>>> data
b'\x00{\x00\x00\x00\x00?\x9dp\xa4\x91\xeb\x85'
>>>
```

要解码二进制数据，请使用 `struct.unpack`：

点击此处查看代码图片

```python
>>> struct.unpack('>HIff', data)
(123, 456, 1.2300000190734863, 4.559999942779541)
>>>
```

浮点数值的差异是由于转换为 32 位数值时产生的精度损失导致的。Python 将浮点数表示为 64 位双精度值。

### 9.15.22 `subprocess` 模块

`subprocess` 模块用于将单独的程序作为子进程执行，但可以控制执行环境，包括 I/O 处理、终止等。该模块有两种常见的用法。

如果你想运行一个单独的程序并一次性收集其所有输出，请使用 `check_output()`。例如：

点击此处查看代码图片

```python
import subprocess

# 运行 'netstat -a' 命令并收集其输出
try:
    out = subprocess.check_output(['netstat', '-a'])
except subprocess.CalledProcessError as e:
    print("It failed:", e)
```

`check_output()` 返回的数据以字节形式呈现。如果你想将其转换为文本，请确保应用适当的解码：

点击此处查看代码图片

```python
text = out.decode('utf-8')
```

也可以设置管道并以更详细的方式与子进程交互。为此，可以使用 `Popen` 类，如下所示：

点击此处查看代码图片

```python
import subprocess

p = subprocess.Popen(['wc'], 
                    stdin=subprocess.PIPE,
                    stdout=subprocess.PIPE)

# 向子进程发送数据
p.stdin.write(b'hello world\nthis is a test\n')
p.stdin.close()

# 读回数据
out = p.stdout.read()
print(out)
```

`Popen` 的实例 `p` 具有 `stdin` 和 `stdout` 属性，可用于与子进程通信。

### 9.15.23 `tempfile` 模块

`tempfile` 模块提供了创建临时文件和目录的支持。以下是创建临时文件的示例：

点击此处查看代码图片

```python
import tempfile

with tempfile.TemporaryFile() as f:
    f.write(b'Hello World')
    f.seek(0)
    data = f.read()
    print('Got:', data)
```

默认情况下，临时文件以二进制模式打开，并允许读写。`with` 语句也常用于定义文件使用时的作用域。文件在 `with` 块结束时会被删除。

如果你想创建临时目录，请使用：

点击此处查看代码图片

```python
with tempfile.TemporaryDirectory() as dirname:
    # 使用目录 dirname
    ...
```

与文件一样，目录及其所有内容将在 `with` 块结束时被删除。

### 9.15.24 `textwrap` 模块

`textwrap` 模块可用于格式化文本以适应特定的终端宽度。虽然它的用途比较特殊，但在生成报告清理输出文本时有时非常有用。其中有两个值得关注的函数。

`wrap()` 接收文本并将其换行以适应指定的列宽。该函数返回一个字符串列表。例如：

点击此处查看代码图片

```python
import textwrap

text = """look into my eyes
look into my eyes
the eyes the eyes the eyes
not around the eyes
don't look around the eyes
look into my eyes you're under
"""

wrapped = textwrap.wrap(text, width=81)
print('\n'.join(wrapped))

# 产生结果:
# look into my eyes look into my eyes the
# eyes the eyes the eyes not around the
# eyes don't look around the eyes look
# into my eyes you're under
```

`indent()` 函数可用于缩进一段文本。例如：

点击此处查看代码图片



```python
print(textwrap.indent(text, '  '))
# 产生结果:
#   look into my eyes
#   look into my eyes
#   the eyes the eyes the eyes
#   not around the eyes
#   don't look around the eyes
#   look into my eyes you're under
```

### 9.15.25 `threading` 模块

`threading` 模块用于并发执行代码。这个问题在网络程序的 I/O 处理中经常出现。线程编程是一个庞大的课题，但以下示例展示了常见问题的解决方案。

这是一个启动线程并等待其结束的示例：

点击此处查看代码图片

```python
import threading
import time

def countdown(n):
    while n > 0:
        print('T-minus', n)
        n -= 1
        time.sleep(1)

t = threading.Thread(target=countdown, args=[10])
t.start()
t.join()  # 等待线程完成
```

如果你永远不需要等待线程完成，可以通过像这样提供额外的 `daemon` 标志将其设置为守护线程：

点击此处查看代码图片

```python
t = threading.Thread(target=countdown, args=[10],
daemon=True)
```

如果你想让一个线程终止，你需要使用标志位或专门的变量来显式地执行此操作。线程必须被编程为检查该标志。

```python
import threading
import time

must_stop = False

def countdown(n):
    while n > 0 and not must_stop:
        print('T-minus', n)
        n -= 1
        time.sleep(1)
```

如果线程需要修改共享数据，请使用 `Lock` 对其进行保护。

```python
import threading

class Counter:
    def __init(self):
        self.value = 0
        self.lock = threading.Lock()

    def increment(self):
        with self.lock:
            self.value += 1

    def decrement(self):
        with self.lock:
            self.value -= 1
```

如果一个线程必须等待另一个线程完成某项操作，请使用 `Event`。

```python
import threading
import time

def step1(evt):
    print('Step 1')
    time.sleep(5)
    evt.set()

def step2(evt):
    evt.wait()
    print('Step 2')

evt = threading.Event()
threading.Thread(target=step1, args=[evt]).start()
threading.Thread(target=step2, args=[evt]).start()
```

如果线程之间需要通信，请使用 `Queue`：

```python
import threading
import queue
import time

def producer(q):
    for i in range(10):
        print('Producing:', i)
        q.put(i)
    print('Done')
    q.put(None)

def consumer(q):
    while True:
        item = q.get()
        if item is None:
            break
        print('Consuming:', item)
    print('Goodbye')

q = queue.Queue()
threading.Thread(target=producer, args=[q]).start()
threading.Thread(target=consumer, args=[q]).start()
```

### 9.15.26 `time` 模块

`time` 模块用于访问与系统时间相关的函数。以下选出的函数是最常用的：

- `sleep(seconds)`：让 Python 睡眠指定的秒数，参数为浮点数。
- `time()`：以浮点数形式返回当前的 UTC 系统时间。这是自纪元（对于 UNIX 系统通常是 1970 年 1 月 1 日）以来经过的秒数。使用 `localtime()` 将其转换为适合提取有用信息的结构。
- `localtime([secs])`：返回一个 `struct_time` 对象，代表系统的本地时间，或者代表作为参数传递的浮点值 `secs` 所对应的时间。结果结构包含属性 `tm_year`、`tm_mon`、`tm_mday`、`tm_hour`、`tm_min`、`tm_sec`、`tm_wday`、`tm_yday` 和 `tm_isdst`。
- `gmtime([secs])`：与 `localtime()` 相同，不同之处在于结果结构代表的是 UTC 时间（或格林威治标准时间）。
- `ctime([secs])`：将以秒表示的时间转换为适合打印的文本字符串。常用于调试和日志记录。
- `asctime(tm)`：将由 `localtime()` 表示的时间结构转换为适合打印的文本字符串。

`datetime` 模块更常用于表示日期和时间，以便进行日期相关计算和处理时区。

### 9.15.27 `urllib` 包

`urllib` 包用于发起客户端 HTTP 请求。最常用的函数可能是 `urllib.request.urlopen()`，它可以用来获取简单的网页。例如：

```python
>>> from urllib.request import urlopen
>>> u = urlopen('http://www.python.org')
>>> data = u.read()
```

如果你想对表单参数进行编码，可以使用 `urllib.parse.urlencode()`，如下所示：

```python
from urllib.parse import urlencode
from urllib.request import urlopen

form = {
    'name': 'Mary A. Python',
    'email': 'mary123@python.org'
}

data = urlencode(form)
u = urlopen('http://httpbin.org/post', data.encode('utf-8'))
response = u.read()
```

对于基础网页以及涉及 HTTP 或 HTTPS 的 API，`urlopen()` 函数运行良好。然而，如果访问还涉及 cookie、高级认证方案及其他层级，使用起来会变得相当麻烦。坦白说，大多数 Python 程序员会使用第三方库（如 `requests` 或 `httpx`）来处理这些情况。你也应该这样做。

`urllib.parse` 子包提供了用于操作 URL 本身的额外函数。例如，`urlparse()` 函数可用于拆解 URL：

```python
>>> url = 'http://httpbin.org/get?name=Dave&n=42'
>>> from urllib.parse import urlparse
>>> urlparse(url)
ParseResult(scheme='http', netloc='httpbin.org', path='/get', params='', query='name=Dave&n=42', fragment='')
```

### 9.15.28 `unicodedata` 模块

`unicodedata` 模块用于涉及 Unicode 文本字符串的更高级操作。同一段 Unicode 文本往往有多种表示方式。例如，字符 U+00F1 (ñ) 既可以完整地组合为一个字符 U+00F1，也可以分解为一个多字符序列 U+006e U+0303 (n, ~)。对于那些期望视觉上渲染相同且在表示上实际相同的文本字符串的程序来说，这可能会导致奇怪的问题。请考虑以下涉及字典键的示例：

```python
>>> d = {}
>>> d['Jalape\xflo'] = 'spicy'
>>> d['Jalapen\u0303o'] = 'mild'
>>> d
{'jalapeño': 'spicy', 'jalapeño': 'mild' }
```

乍一看，这似乎是一个运行错误——字典怎么能有两个这样完全相同但又是独立的键？答案在于这些键由不同的 Unicode 字符序列组成。

如果一致处理渲染相同的 Unicode 字符串是一个问题，那么应该对其进行标准化。`unicodedata.normalize()` 函数可用于确保字符表示的一致性。例如，`unicodedata.normalize('NFC', s)` 将确保 `s` 中的所有字符都是完整组合的，而不是由组合字符序列表示。使用 `unicodedata.normalize('NFD', s)` 则会确保 `s` 中的所有字符都被完全分解。

`unicodedata` 模块还具有测试字符属性的函数，如大写、数字和空白字符。可以通过 `unicodedata.category(c)` 函数获取通用字符属性。例如，`unicodedata.category('A')` 返回 'Lu'，表示该字符是大写字母。关于这些值的更多信息可以在官方 Unicode 字符数据库中找到：https://www.unicode.org/ucd。

### 9.15.29 `xml` 包

`xml` 包是一个大型模块集，用于以各种方式处理 XML 数据。但是，如果你的主要目标是读取 XML 文档并从中提取信息，最简单的方法是使用 `xml.etree` 子包。假设你有一个名为 `recipe.xml` 的 XML 文档，内容如下：

```xml
<?xml version="1.0" encoding="iso-8859-1"?>
<recipe>
    <title>Famous Guacamole</title>
    <description>A southwest favorite!</description>
    <ingredients>
        <item num="4"> Large avocados, chopped </item>
        <item num="1"> Tomato, chopped </item>
        <item num="1/2" units="C"> White onion, chopped </item>
        <item num="2" units="tbl"> Fresh squeezed lemon juice </item>
        <item num="1"> Jalapeno pepper, diced </item>
        <item num="1" units="tbl"> Fresh cilantro, minced </item>
        <item num="1" units="tbl"> Garlic, minced </item>
        <item num="3" units="tsp"> Salt </item>
        <item num="12" units="bottles"> Ice-cold beer </item>
    </ingredients>
    <directions>
        Combine all ingredients and hand whisk to desired
        consistency.
        Serve and enjoy with ice-cold beers.
    </directions>
</recipe>
```

以下是如何从中提取特定元素：

```python
from xml.etree.ElementTree import ElementTree

doc = ElementTree(file="recipe.xml")
title = doc.find('title')
print(title.text)

# 另一种方法（直接获取元素文本）
print(doc.findtext('description'))

# 遍历多个元素
```

```python
for item in doc.findall('ingredients/item'):
    num = item.get('num')
    units = item.get('units', '')
    text = item.text.strip()
    print(f'{num} {units} {text}')
```

## 9.16 结语录（总结）

I/O 是编写任何有用程序的基石。鉴于其普及程度，Python 能够处理几乎任何正在使用的数据格式、编码或文档结构。尽管标准库可能不支持某些格式，但你几乎肯定能找到第三方模块来解决你的问题。

从大局来看，思考应用程序的“边缘”可能会更有用。在程序与现实世界的外部边界上，经常会遇到与数据编码相关的问题。对于文本数据和 Unicode 尤其如此。Python I/O 处理中的许多复杂性——支持不同编码、错误处理策略等——正是为了解决这个特定问题。同时，必须牢记文本数据和二进制数据是严格区分的。了解你正在处理的数据类型有助于理解整体架构。

I/O 的另一个考虑因素是整体评估模型。Python 代码目前分为两个世界：普通的同步代码和通常与 `asyncio` 模块相关的异步代码（其特征是使用 `async` 函数和 `async/await` 语法）。异步代码几乎总是需要使用能够在该环境中运行的专用库。这反过来又迫使你必须以“异步”风格编写应用程序代码。坦白说，除非你绝对确定需要它，否则你应该尽量避免异步编程——如果你不确定，那么你几乎肯定是不需要的。大多数心态稳健的 Python 开发者都采用普通的同步风格进行编码，这种风格在推理、调试和测试方面要容易得多。你应该选择这种方式。

# 10. 内置函数与标准库

本章是 Python 内置函数的紧凑参考指南。这些函数无需任何 `import` 语句即可随时使用。本章最后简要概述了一些有用的标准库模块。

## 10.1 内置函数

`abs(x)`

返回 `x` 的绝对值。

`all(s)`

如果可迭代对象 `s` 中的所有值都评估为 `True`，则返回 `True`。如果 `s` 为空，则返回 `True`。

`any(s)`

如果可迭代对象 `s` 中的任何值评估为 `True`，则返回 `True`。如果 `s` 为空，则返回 `False`。

`ascii(x)`

创建对象 `x` 的可打印表示形式，类似于 `repr()`，但在结果中仅使用 ASCII 字符。非 ASCII 字符会被转换为相应的转义序列。这可用于在不支持 Unicode 的终端或 shell 中查看 Unicode 字符串。

`bin(x)`

返回整数 `x` 的二进制表示形式的字符串。

`bool([x])`

表示布尔值 `True` 和 `False` 的类型。如果用于转换 `x`，且 `x` 根据通常的真值测试语义评估为真（例如：非零数值、非空列表等），则返回 `True`。否则返回 `False`。如果在不传递任何参数的情况下调用 `bool()`，默认返回 `False`。`bool` 类继承自 `int`，因此布尔值 `True` 和 `False` 在数学计算中可以用作值为 `1` 和 `0` 的整数。

`breakpoint()`

设置一个手动调试断点。遇到该函数时，控制权将转移到 Python 调试器 `pdb`。

`bytearray([x])`

表示可变字节数组的类型。创建实例时，`x` 可以是 0 到 255 范围内的整数可迭代序列、8 位字符串或字节字面量，或者是一个指定字节数组大小的整数（在这种情况下，每个条目都将初始化为 `0`）。

`bytearray(s, encoding)`

另一种创建 `bytearray` 实例的调用约定，从字符串 `s` 中的字符创建，其中 `encoding` 指定转换时使用的字符编码。

`bytes([x])`

表示不可变字节数组的类型。

`bytes(s, encoding)`

另一种从字符串 `s` 创建字节的调用约定，其中 `encoding` 指定转换时使用的编码。

表 10.1 显示了 `bytes` 和 `bytearray` 共同支持的操作。

### 表 10.1 字节 (Bytes) 与字节数组 (Bytearrays) 的操作

| 操作 | 描述 |
|---|---|
| `s + t` | 如果 `t` 是字节，则进行拼接。 |
| `s * n` | 如果 `n` 是整数，则进行重复。 |
| `s % x` | 格式化字节。`x` 是元组。 |
| `s[i]` | 返回元素 `i` 为整数。 |
| `s[i:j]` | 返回切片。 |
| `s[i:j:stride]` | 返回扩展切片。 |
| `len(s)` | `s` 中的字节数。 |
| `s.capitalize()` | 将第一个字符大写。 |



| `s.center(width [, pad])` | 将字符串居中于长度为 `width` 的字段中。`pad` 是填充字符。 |

| `s.count(sub [, start [, end]])` | 计算指定子字符串 `sub` 出现的次数。 |

| `s.decode([encoding [, errors]])` | 将字节字符串解码为文本（仅限 `bytes` 类型）。 |

| `s.endswith(suffix [, start [, end])` | 检查字符串末尾是否为 `suffix`。 |

| `s.expandtabs([tabsize])` | 将制表符替换为空格。 |

| `s.find(sub [, start [, end]])` | 查找指定子字符串 `sub` 第一次出现的位置。 |

| `s.hex()` | 转换为十六进制字符串。 |

| `s.index(sub [, start [, end]])` | 查找指定子字符串 `sub` 第一次出现的位置，否则报错。 |

| `s.isalnum()` | 检查所有字符是否均为字母或数字。 |

| `s.isalpha()` | 检查所有字符是否均为字母。 |

| `s.isascii()` | 检查所有字符是否均为 ASCII。 |

| `s.isdigit()` | 检查所有字符是否均为数字。 |

| `s.islower()` | 检查所有字符是否均为小写。 |

| `s.isspace()` | 检查所有字符是否均为空白字符。 |

| `s.istitle()` | 检查字符串是否为标题格式（每个单词的首字母大写）。 |

| `s.isupper()` | 检查所有字符是否均为大写。 |

| `s.join(t)` | 使用分隔符 `s` 连接字符串序列 `t`。 |

| `s.ljust(width [, fill])` | 将 `s` 左对齐在大小为 `width` 的字符串中。 |

| `s.lower()` | 转换为小写。 |

| `s.lstrip([chrs])` | 移除领先的空白字符或 `chrs` 中提供的字符。 |

| `s.maketrans(x [, y [, z]])` | 为 `s.translate()` 创建一个转换表。 |

| `s.partition(sep)` | 根据分隔符字符串 `sep` 分割字符串。返回元组 `(head, sep, tail)`，如果未找到 `sep` 则返回 `(s, '', '')`。 |

| `s.removeprefix(prefix)` | 如果存在给定的 `prefix`，则返回移除该前缀后的 `s`。 |

| `s.removesuffix(suffix)` | 如果存在给定的 `suffix`，则返回移除该后缀后的 `s`。 |

| `s.replace(old, new [, maxreplace])` | 替换子字符串。 |

| `s.rfind(sub [, start [, end]])` | 查找子字符串最后一次出现的位置。 |

| `s.rindex(sub [, start [, end]])` | 查找子字符串最后一次出现的位置，否则抛出错误。 |

| `s.rjust(width [, fill])` | 将 `s` 右对齐在长度为 `width` 的字符串中。 |

| `s.rpartition(sep)` | 根据分隔符 `sep` 分割 `s`，但从字符串末尾开始搜索。 |

| `s.rsplit([sep [, maxsplit]])` | 使用 `sep` 作为分隔符从字符串末尾开始分割。`maxsplit` 是最大分割次数。如果省略 `maxsplit`，结果与 `split()` 方法相同。 |

| `s.rstrip([chars])` | 移除末尾的空白字符或 `chars` 中提供的字符。 |

| `s.split([sep [, maxsplit]])` | 使用 `sep` 作为分隔符分割字符串。`maxsplit` 是最大分割次数。 |

| `s.splitlines([keepends])` | 将字符串分割为行列表。如果 `keepends` 为 1，则保留末尾的换行符。 |

| `s.startswith(prefix [, start [, end]])` | 检查字符串是否以 `prefix` 开头。 |

| `s.strip([chars])` | 移除开头和末尾的空白字符或 `chars` 中提供的字符。 |

| `s.swapcase()` | 大写转小写，小写转大写。 |

| `s.title()` | 返回字符串的标题格式版本。 |

| `s.translate(table [, deletechars])` | 使用字符转换表 `table` 翻译字符串，并移除 `deletechars` 中的字符。 |

| `s.upper()` | 将字符串转换为大写。 |

| `s.zfill(width)` | 在字符串左侧填充零，直到达到指定的 `width`。 |

字节数组还额外支持表 10.2 中的方法。

### 表 10.2 字节数组的附加操作

| 操作 | 描述 |

|---|---|

| `s[i] = v` | 项目赋值 |

| `s[i:j] = t` | 切片赋值 |

| `s[i:j:stride] = t` | 扩展切片赋值 |

| `del s[i]` | 项目删除 |

| `del s[i:j]` | 切片删除 |

| `del s[i:j:stride]` | 扩展切片删除 |

| `s.append(x)` | 在末尾追加一个新字节。 |

| `s.clear()` | 清空字节数组。 |

| `s.copy()` | 创建副本。 |

| `s.extend(t)` | 使用 `t` 中的字节扩展 `s`。 |

| `s.insert(n, x)` | 在索引 `n` 处插入字节 `x`。 |

| `s.pop([n])` | 移除并返回索引 `n` 处的字节。 |

| `s.remove(x)` | 移除第一个出现的字节 `x`。 |

| `s.reverse()` | 原地反转字节数组。 |

```
callable(obj)
```

如果 `obj` 可以作为函数调用，则返回 `True`。

```
chr(x)
```

将表示 Unicode 码点的整数 `x` 转换为单字符字符串。

```
classmethod(func)
```

该装饰器为函数 `func` 创建一个类方法。它通常仅在类定义内部使用，并使用 `@classmethod` 隐式调用。与普通方法不同，类方法接收类作为第一个参数，而不是实例。

```
compile(string, filename, kind)
```

将 `string` 编译成代码对象，以便与 `exec()` 或 `eval()` 配合使用。`string` 是包含有效 Python 代码的字符串。如果该代码跨越多行，则每行必须由单个换行符 (`'\n'`) 终止，而不能使用平台特定的变体（例如 Windows 上的 `'\r\n'`）。`filename` 是包含定义该字符串的文件名的字符串（如果有）。`kind` 为 `'exec'` 表示语句序列，`'eval'` 表示单个表达式，`'single'` 表示单个可执行语句。返回的 resulting 代码对象可以直接传递给 `exec()` 或 `eval()` 以替代字符串。

```python
complex([real [, imag]])
```

表示具有实部和虚部（`real` 和 `imag`）的复数的类型，这两个部分可以是任何数值类型。如果省略 `imag`，则虚部设为零。如果 `real` 以字符串形式传递，则该字符串将被解析并转换为复数。在这种情况下，应省略 `imag`。如果 `real` 是任何其他类型的对象，则返回 `real.__complex__()` 的值。如果没有提供参数，则返回 `0j`。

表 10.3 显示了 `complex` 的方法和属性。

### 表 10.3 `complex` 的属性

| 属性/方法 | 描述 |

| --- | --- |

| `z.real` | 实部 |

| `z.imag` | 虚部 |

| `z.conjugate()` | 作为复数进行共轭。 |

```python
delattr(object, attr)
```

删除对象的属性。`attr` 是一个字符串。等同于 `del object.attr`。

```
`dict([m])` or `dict(key1=value1, key2=value2, ...)`
```

表示字典的类型。如果没有提供参数，则返回一个空字典。如果 `m` 是一个映射对象（例如另一个字典），则返回一个具有与 `m` 相同键和相同值的的新字典。例如，如果 `m` 是一个字典，`dict(m)` 会创建其浅拷贝。如果 `m` 不是映射，则它必须支持迭代，从而产生一系列 `(key, value)` 对。这些对将被用于填充字典。`dict()` 也可以通过关键字参数调用。例如，`dict(foo=3, bar=7)` 创建字典 `{'foo': 3, 'bar': 7}`。

表 10.4 显示了字典支持的操作。

### 表 10.4 字典操作

| 操作 | 描述 |

| :--- | :--- |

| `m \| n` | 将 `m` 和 `n` 合并为一个字典。 |

| `len(m)` | 返回 `m` 中的项目数量。 |

| `m[k]` | 返回 `m` 中键为 `k` 的项目。 |

| `m[k]=x` | 将 `m[k]` 设置为 `x`。 |

| `del m[k]` | 从 `m` 中移除 `m[k]`。 |

| `k in m` | 如果 `k` 是 `m` 中的键，则返回 `True`。 |

| `m.clear()` | 从 `m` 中移除所有项目。 |

| `m.copy()` | 创建 `m` 的浅拷贝。 |

| `m.fromkeys(s [], value)` | 使用序列 `s` 中的键创建新字典，并将所有值设置为 value。 |

| `m.get(k [, v])` | 如果找到则返回 `m[k]`；否则返回 `v`。 |

| `m.items()` | 返回 `(key, value)` 对。 |

| `m.keys()` | 返回键。 |

| `m.pop(k [, default])` | 如果找到则返回 `m[k]` 并将其从 `m` 中移除；否则，如果提供了 `default` 则返回 `default`，否则引发 `KeyError`。 |

| `m.popitem()` | 从 `m` 中移除一个随机的 `(key, value)` 对，并将其作为元组返回。 |

| `m.setdefault(k [, v])` | 如果找到则返回 `m[k]`；否则返回 `v` 并设置 `m[k] = v`。 |

| `m.update(b)` | 将 `b` 中的所有对象添加到 `m` 中。 |

| `m.values()` | 返回值。 |

```
dir([object])
```

返回一个排序后的属性名称列表。如果 `object` 是一个模块，它包含在该模块中定义的符号列表。如果 `object` 是一个类型或类对象，它返回一个属性名称列表。这些名称通常从对象的 `__dict__` 属性（如果定义了）中获取，但也可以使用其他来源。如果没有提供参数，则返回当前本地符号表中的名称。需要注意的是，此函数主要用于信息目的（例如，在命令行交互式使用）。它不应被用于正式的程序分析，因为获取的信息可能不完整。此外，用户定义的类可以定义一个特殊的 `__dir__()` 方法来改变此函数的结果。

```
divmod(a, b)
```

以元组形式返回长除法的商和余数。对于整数，返回值为 `(a // b, a % b)`。对于浮点数，返回 `(math.floor(a / b), a % b)`。此函数不能使用复数调用。

```
enumerate(iter, start=0)
```

给定一个可迭代对象 `iter`，返回一个新的迭代器（类型为 `enumerate`），该迭代器产生包含计数和由 `iter` 产生的值的元组。例如，如果 `iter` 产生 `a, b, c`，那么 `enumerate(iter)` 产生 `(0,a), (1,b), (2,c)`。可选参数 `start` 改变计数的初始值。

```python
eval(expr [, globals [, locals]]])
```

计算表达式。`expr` 是一个字符串或由 `compile()` 创建的代码对象。`globals` 和 `locals` 分别是定义该操作的全局和局部命名空间的映射对象。如果省略，则使用在调用者环境中执行的 `globals()` 和 `locals()` 的值来计算表达式。最常见的是将 globals 和 locals 指定为字典，但高级应用程序可以提供自定义的映射对象。

```python
exec(code [, global [, locals]]])
```

执行 Python 语句。`code` 是一个字符串、字节或由 `compile()` 创建的代码对象。`globals` 和 `locals` 分别定义该操作的全局和局部命名空间。如果省略，则使用在调用者环境中执行的 `globals()` 和 `locals()` 的值来执行代码。

```python
filter(function, iterable)
```

创建一个迭代器，返回 `iterable` 中使得 `function(item)` 求值为 `True` 的项目。

```python
float([x])
```

表示浮点数的类型。如果 `x` 是一个数字，它被转换为浮点数。如果 `x` 是一个字符串，它被解析为浮点数。对于所有其他对象，将调用 `x.__float__()`。如果没有提供参数，则返回 `0.0`。

表 10.5 显示了浮点数的方法和属性。

### 表 10.5 浮点数的方法和属性

| 属性/方法 | 描述 |

| :--- | :--- |

| `x.real` | 用作复数时的实部。 |

| `x.imag` | 用作复数时的虚部。 |

| `x.conjugate()` | 作为复数进行共轭。 |

| `x.as_integer_ratio()` | 转换为分子/分母对。 |

| `x.hex()` | 创建十六进制表示。 |

| `x.is_integer()` | 测试是否为精确的整数值。 |

| `float.fromhex(s)` | 从十六进制字符串创建。这是一个类方法。 |

```
format(value [, format_spec])
```

根据 `format_spec` 中的格式规范字符串将 `value` 转换为格式化字符串。此操作调用 `value.__format__()`，该方法可以根据其认为合适的方式解释格式规范。对于简单的数据类型，格式说明符通常包括一个对齐字符 `'<'`、`'>'` 或 `'^'`，一个数字（表示字段宽度），以及一个字符代码 `'d'`、`'f'` 或 `'s'`（分别对应整数、浮点数或字符串值）。例如，格式规范 `'d'` 格式化一个整数，规范 `'>8d'` 将整数在 8 字符字段中右对齐，而 `'<8d'` 将整数在 8 字符字段中左对齐。关于 `format()` 和格式说明符的更多细节可以在第 9 章中找到。

```
frozenset([items])
```

表示不可变集合对象的类型，其中的值取自 `items`（`items` 必须是可迭代的）。值也必须是不可变的。如果没有提供参数，则返回一个空集合。

`frozenset` 支持 `sets` 上的所有操作，但不支持任何原位修改集合的操作。

`getattr(object, name [,default])`

返回对象的名为 `name` 的属性值。`name` 是包含属性名的字符串。`default` 是一个可选值，如果不存在该属性则返回此值；否则，将引发 `AttributeError`。其作用与访问 `object.name` 相同。

`globals()`

返回当前模块代表全局命名空间的字典。当在另一个函数或方法内部调用时，它返回定义该函数或方法的模块的全局命名空间。

`hasattr(object, name)`

如果 `name` 是 `object` 的属性名，则返回 `True`。`name` 是一个字符串。

`hash(object)`

返回一个对象的整数哈希值（如果可能）。哈希值主要用于字典、集合和其他映射对象的实现。对于任何比较为相等的对象，其哈希值始终相同。可变对象通常不定义哈希值，尽管用户自定义类可以通过定义 `__hash__()` 方法来支持此操作。

`hex(x)`

将整数 `x` 转换为十六进制字符串。

`id(object)`

返回 `object` 的唯一整数标识。你不应以任何方式解释该返回值（例如，它不是内存地址）。

`input([prompt])`

将提示符打印到标准输出，并从标准输入读取单行输入。返回的行不经任何修改。它不包含行尾符（例如 '\n'）。

```python
int(x [,base])
```

表示整数的类型。如果 `x` 是数字，则通过向 0 取整将其转换为整数。如果 `x` 是字符串，则将其解析为整数值。`base` 可选地指定从字符串转换时的基数。

除了支持常见的数学运算外，整数还具有表 10.6 中列出的一系列属性和方法。

### 表 10.6 整数的方法和属性

| 操作 | 描述 |

| :--- | :--- |

| `x.numerator` | 作为分数使用时的分子。 |

| `x.denominator` | 作为分数使用时的分母。 |

| `x.real` | 作为复数使用时的实部。 |

| `x.imag` | 作为复数使用时的虚部。 |

| `x.conjugate()` | 作为复数时求共轭。 |



| `x.bit_length()` | 表示该值在二进制下所需的位数。 |

| `x.to_bytes(length, byteorder, *, signed=False)` | 转换为字节。 |

| `int.from_bytes(bytes, byteorder, *, signed=False)` | 从字节转换。这是一个类方法。 |

```python
isinstance(object, classobj)
```

如果 `object` 是 `classobj` 的实例或其子类，则返回 `True`。`classobj` 参数也可以是一个包含可能类型或类的元组。例如，如果 `s` 是元组或列表，`isinstance(s, (list, tuple))` 将返回 `True`。

`issubclass(class1, class2)`

如果 `class1` 是 `class2` 的子类（派生自 `class2`），则返回 `True`。`class2` 也可以是一个包含可能类的元组，在这种情况下将检查每个类。注意 `issubclass(A, A)` 为 `True`。

`iter(object [, sentinel])`

返回一个用于产生 `object` 中项目的迭代器。如果省略了 `sentinel` 参数，则对象必须提供 `__iter__()` 方法（用于创建迭代器），或者对象必须实现 `__getitem__()`（接受从 0 开始的整数参数）。如果指定了 `sentinel`，则 `object` 的解释方式不同。此时，`object` 应该是一个不带参数的可调用对象。返回的迭代器对象将重复调用此函数，直到返回值等于 `sentinel`，此时迭代停止。如果 `object` 不支持迭代，将产生 `TypeError`。

`len(s)`

返回 `s` 中包含的项目数量，`s` 应该是某种容器，如列表、元组、字符串、集合或字典。

`list([items])`

表示列表的类型。`items` 可以是任何可迭代对象，其值用于填充列表。如果 `items` 已经是一个列表，则创建其浅拷贝。如果没有给出参数，则返回一个空列表。

表 10.7 显示了定义在列表上的操作。

### 表 10.7 列表运算符和方法

| 操作 | 描述 |

| :--- | :--- |

| `s + t` | 如果 `t` 是列表，则进行拼接。 |

| `s * n` | 如果 `n` 是整数，则进行重复。 |

| `s[i]` | 返回 `s` 的第 `i` 个元素。 |

| `s[i:j]` | 返回一个切片。 |

| `s[i:j:stride]` | 返回一个扩展切片。 |

| `s[i] = v` | 项目赋值。 |

| `s[i:j] = t` | 切片赋值。 |

| `s[i:j:stride] = t` | 扩展切片赋值。 |

| `del s[i]` | 项目删除。 |

| `del s[i:j]` | 切片删除。 |

| `del s[i:j:stride]` | 扩展切片删除。 |

| `len(s)` | `s` 中的元素数量。 |

| `s.append(x)` | 将新元素 `x` 追加到 `s` 的末尾。 |

| `s.extend(t)` | 将新列表 `t` 追加到 `s` 的末尾。 |

| `s.count(x)` | 统计 `x` 在 `s` 中出现的次数。 |

| `s.index(x [, start [, stop]])` | 返回满足 `s[i] == x` 的最小 `i`。`start` 和 `stop` 可选地指定搜索的起始和结束索引。 |

| `s.insert(i, x)` | 在索引 `i` 处插入 `x`。 |

| `s.pop([i])` | 返回元素 `i` 并将其从列表中移除。如果省略 `i`，则返回最后一个元素。 |

| `s.remove(x)` | 搜索 `x` 并将其从 `s` 中移除。 |

| `s.reverse()` | 原位反转 `s` 的项目。 |

| `s.sort([key [, reverse]])` | 原位对 `s` 的项目进行排序。`key` 是一个键函数。`reverse` 是一个标志，用于反向排序列表。`key` 和 `reverse` 应当始终指定为关键字参数。 |

`locals()`

返回一个与调用者本地命名空间相对应的字典。该字典仅应被用于检查执行环境——对该字典所做的更改不会对相应的本地变量产生任何影响。

`map(function, items, ...)`

创建一个迭代器，该迭代器产生将 `function` 应用于 `items` 中各项目的结果。如果提供了多个输入序列，则假设 `function` 接受相应数量的参数，每个参数分别来自不同的序列。在这种情况下，结果的长度仅与最短的输入序列一致。

`max(s [, args, ...], *, default=obj, key=func)`

对于单个参数 `s`，此函数返回 `s` 中项目的最大值，`s` 可以是任何可迭代对象。对于多个参数，它返回这些参数中的最大值。如果给出了仅限关键字参数 `default`，则在 `s` 为空时提供返回值。如果给出了仅限关键字参数 `key`，则返回使 `key(v)` 返回最大值的那个值 `v`。

```python
min(s [, args, ..., ], *, default=obj, key=func)
```

与 `max(s)` 相同，但返回的是最小值。

```python
next(s [, default])
```

返回迭代器 `s` 的下一个项目。如果迭代器没有更多项目，则引发 `StopIteration` 异常，除非为 `default` 参数提供了值。在这种情况下，将返回 `default`。

```python
object()
```

Python 中所有对象的基类。你可以调用它来创建实例，但结果并没有什么特别的意义。

```python
oct(x)
```

将整数 `x` 转换为八进制字符串。

```python
open(filename [, mode [, bufsize [, encoding [, errors [, newline [, closefd]]]]]])
```

打开文件 `filename` 并返回一个文件对象。参数在 [第 9 章](https://example.com) 中有详细描述。

```python
ord(c)
```

返回单个字符 `c` 的整数序数。该值通常对应于字符的 Unicode 码点值。

```python
pow(x, y [, z])
```

返回 `x ** y`。如果提供了 `z`，该函数返回 `(x ** y) % z`。如果三个参数全部给出，它们必须是整数且 `y` 必须是非负数。

```python
print(value, ..., *, sep=separator, end=ending, file=outfile)
```

打印一组值。作为输入，你可以提供任意数量的值，所有值都将打印在同一行。`sep` 关键字参数用于指定不同的分隔符（默认为空格）。`end` 关键字参数指定不同的行尾字符（默认为 '\n'）。`file` 关键字参数将输出重定向到文件对象。

```python
property([fget [, fset [, fdel [, doc]]]])
```

为类创建属性（property）属性。`fget` 是一个返回属性值的函数，`fset` 设置属性值，`fdel` 删除属性。`doc` 提供文档字符串。属性通常指定为装饰器：

```python
class SomeClass:
    x = property(doc='This is property x')

    @x.getter
    def x(self):
        print('getting x')

    @x.setter
    def x(self, value):
        print('setting x to', value)

    @x.deleter
    def x(self):
        print('deleting x')
```

`range([start,] stop [, step])`

创建一个 `range` 对象，表示从 `start` 到 `stop` 的整数范围。`step` 表示步长，如果省略则设为 `1`。如果省略 `start`（当 `range()` 仅带一个参数调用时），它默认为 `0`。负步长将创建按降序排列的数字列表。

`repr(object)`

返回 `object` 的字符串表示形式。在大多数情况下，返回的字符串是一个可以传递给 `eval()` 以重建该对象的表达式。

`reversed(s)`

为序列 `s` 创建一个反向迭代器。此函数仅在 `s` 定义了 `__reversed__()` 方法，或者实现了序列方法 `__len__()` 和 `__getitem__()` 时才有效。它不适用于生成器。

`round(x [, n])`

将浮点数 `x` 四舍五入到最接近 10 的负 `n` 次方的倍数。如果省略 `n`，则默认为 `0`。如果两个倍数距离相等，则在前一位数字为偶数时向 0 取整，否则远离 0 取整（例如，`0.5` 被舍入为 `0.0`，`1.5` 被舍入为 `2`）。

`set([items])`

创建一个集合，其中包含从可迭代对象 `items` 中获取的元素。元素必须是不可变的。如果 `items` 包含其他集合，则这些集合必须是 `frozenset` 类型。如果省略 `items`，则返回一个空集合。

表 10.8 展示了集合的操作。

### 表 10.8 集合操作与方法

| 操作 | 描述 |

| :--- | :--- |

| `s \| t` | 并集 |

| `s & t` | 交集 |

| `s - t` | 差集 |

| `s ^ t` | 对称差集 |

| `len(s)` | 返回 `s` 中的元素数量。 |

| `s.add(item)` | 将元素添加到 `s` 中。如果元素已在 `s` 中则无影响。 |

| `s.clear()` | 移除 `s` 中的所有元素。 |

| `s.copy()` | 创建 `s` 的副本。 |

| `s.difference(t)` | 集合差集。返回所有在 `s` 中但不在 `t` 中的元素。 |

| `s.difference_update(t)` | 从 `s` 中移除所有也在 `t` 中的所有元素。 |

| `s.discard(item)` | 从 `s` 中移除 `item`。如果 `item` 不是 `s` 的成员，则不执行任何操作。 |

| `s.intersection(t)` | 交集。返回同时在 `s` 和 `t` 中的所有元素。 |

| `s.intersection_update(t)` | 计算 `s` 和 `t` 的交集并将结果保留在 `s` 中。 |

| `s.isdisjoint(t)` | 如果 `s` 和 `t` 没有共同元素，则返回 `True`。 |

| `s.issubset(t)` | 如果 `s` 是 `t` 的子集，则返回 `True`。 |

| `s.issuperset(t)` | 如果 `s` 是 `t` 的超集，则返回 `True`。 |

| `s.pop()` | 返回并移除 `s` 中的一个任意元素。 |

| `s.remove(item)` | 从 `s` 中移除 `item`。如果 `item` 不是成员，则抛出 `KeyError`。 |

| `s.symmetric_difference(t)` | 对称差集。返回在 `s` 或 `t` 中，但不同时在两个集合中的所有元素。 |

| `s.symmetric_difference_update(t)` | 计算 `s` 和 `t` 的对称差集并将结果保留在 `s` 中。 |

| `s.union(t)` | 并集。返回在 `s` 或 `t` 中的所有元素。 |

| `s.update(t)` | 将 `t` 中的所有元素添加到 `s` 中。`t` 可以是另一个集合、一个序列或任何支持迭代的对象。 |

```python
setattr(object, name, value)
```

设置对象的属性。`name` 是一个字符串。等同于 `object.name = value`。

```python
slice([start,] stop [, step])
```

返回一个表示指定范围内整数的 `slice` 对象。切片对象也可以通过扩展切片语法 `a[i:i+k]` 生成。

```python
sorted(iterable, *, key=keyfunc, reverse=reverseflag)
```

从 `iterable` 中的项创建排序列表。关键字参数 `key` 是一个单参数函数，用于在比较之前转换值。关键字参数 `reverse` 是一个布尔标志，指定结果列表是否按反序排序。`key` 和 `reverse` 参数必须使用关键字指定——例如，`sorted(a, key=get_name)`。

```python
staticmethod(func)
```

创建用于类中的静态方法。此函数通常用作 `@staticmethod` 装饰器。

```python
str([object])
```

表示字符串的类型。如果提供了对象，则通过调用其 `__str__()` 方法创建其值的字符串表示。这就是你在打印对象时看到的字符串。如果没有给出参数，则创建一个空字符串。

表 10.9 展示了定义在字符串上的方法。

### 表 10.9 字符串运算符与方法

| 操作 | 描述 |

| :--- | :--- |

| `s + t` | 如果 `t` 是字符串，则拼接字符串。 |

| `s * n` | 如果 `n` 是整数，则重复字符串。 |

| `s % x` | 格式化字符串。`x` 是元组。 |

| `s[i]` | 返回字符串的第 `i` 个元素。 |

| `s[i:j]` | 返回一个切片。 |

| `s[i:j:stride]` | 返回一个扩展切片。 |

| `len(s)` | `s` 中的元素数量。 |

| `s.capitalize()` | 将首字母大写。 |

| `s.casefold()` | 将 `s` 转换为可用于不区分大小写比较的字符串。 |

| `s.center(width [, pad])` | 将字符串居中放置在长度为 `width` 的字段中。`pad` 是填充字符。 |

| `s.count(sub [, start [, end]])` | 计算指定子字符串 `sub` 出现次数。 |

| `s.decode([encoding [, errors]])` | 将字节字符串解码为文本（仅限 `bytes` 类型）。 |

| `s.encode([encoding [, errors]])` | 返回字符串的编码版本（仅限 `str` 类型）。 |

| `s.endswith(suffix [, start [, end]])` | 检查字符串末尾是否为 `suffix`。 |

| `s.expandtabs([tabsize])` | 将制表符替换为空格。 |

| `s.find(sub [, start [, end]])` | 查找指定子字符串 `sub` 第一次出现的位置。 |

| `s.format(*args, **kwargs)` | 格式化 `s`（仅限 `str` 类型）。 |

| `s.format_map(m)` | 使用来自映射 `m` 的替换项来格式化 `s`（仅限 `str` 类型）。 |

| `s.index(sub [, start [, end]])` | 查找指定子字符串 `sub` 第一次出现的位置，否则报错。 |

| `s.isalnum()` | 检查所有字符是否均为字母或数字。 |

| `s.isalpha()` | 检查所有字符是否均为字母。 |

| `s.isascii()` | 检查所有字符是否均为 ASCII 字符。 |

| `s.isdecimal()` | 检查所有字符是否均为十进制字符。不匹配上标、下标或其他特殊数字。 |

| `s.isdigit()` | 检查所有字符是否均为数字。匹配上标和下标，但不匹配常用分数。 |

| `s.isidentifier()` | 检查 `s` 是否为有效的 Python 标识符。 |

| `s.islower()` | 检查所有字符是否均为小写。 |

| `s.isnumeric()` | 检查所有字符是否均为数值。匹配所有形式的数值字符，如常用分数、罗马数字等。 |

| `s.isprintable()` | 检查所有字符是否均为可打印字符。 |

| `s.isspace()` | 检查所有字符是否均为空白字符。 |

| `s.istitle()` | 检查字符串是否为标题格式字符串（每个单词的首字母大写）。 |

| `s.isupper()` | 检查所有字符是否均为大写。 |

| `s.join(t)` | 使用分隔符 `s` 连接字符串序列 `t`。 |

| `s.ljust(width [, fill])` | 在大小为 `width` 的字符串中左对齐 `s`。 |

| `s.lower()` | 转换为小写。 |

| `s.lstrip([chars])` | 移除开头的空白字符或 `chars` 中指定的字符。 |

| `s.maketrans(x [, y [, z]])` | 为 `s.translate()` 创建一个转换表。 |

| 操作 | 描述 |

| :--- | :--- |

| `s.partition(sep)` | 根据分隔符字符串 `sep` 对字符串 `s` 进行分区。返回一个元组 `(head, sep, tail)`；如果未找到 `sep`，则返回 `(s, '', '')`。 |

| `s.removeprefix(prefix)` | 如果存在给定的 `prefix`，则返回去掉该前缀后的 `s`。 |



| `s.removesuffix(suffix)` | 如果存在给定的 `suffix`，则返回去掉该后缀后的 `s`。 |
| `s.replace(old, new [, maxreplace])` | 替换子字符串。 |
| `s.rfind(sub [, start [, end]])` | 查找子字符串最后一次出现的位置。 |
| `s.rindex(sub [, start [, end]])` | 查找子字符串最后一次出现的位置，若未找到则抛出错误。 |
| `s.rjust(width [, fill])` | 将 `s` 右对齐在一个长度为 `width` 的字符串中。 |
| `s.rpartition(sep)` | 根据分隔符 `sep` 对 `s` 进行分区，但从字符串末尾开始搜索。 |
| `s.rsplit(sep [, maxsplit])` | 使用 `sep` 作为分隔符，从字符串末尾开始拆分字符串。`maxsplit` 是执行拆分的最大次数。如果省略 `maxsplit`，结果与 `split()` 方法相同。 |
| `s.rstrip([chars])` | 移除末尾的空白字符或 `chars` 中指定的字符。 |
| `s.split(sep [, maxsplit])` | 使用 `sep` 作为分隔符拆分字符串。`maxsplit` 是执行拆分的最大次数。 |
| `s.splitlines(keepends)` | 将字符串拆分为行列表。如果 `keepends` 为 1，则保留末尾的换行符。 |
| `s.startswith(prefix [, start [, end]])` | 检查字符串是否以 `prefix` 开头。 |
| `s.strip([chars])` | 移除开头和末尾的空白字符或 `chars` 中指定的字符。 |
| `s.swapcase()` | 将大写转换为小写，反之亦然。 |
| `s.title()` | 返回字符串的标题格式版本（每个单词首字母大写）。 |
| `s.translate(table [, deletechars])` | 使用字符转换表 `table` 翻译字符串，并移除 `deletechars` 中的字符。 |
| `s.upper()` | 将字符串转换为大写。 |
| `s.zfill(width)` | 在字符串左侧填充零，直到达到指定的 `width` 长度。 |

```
sum(items [,initial])
```

计算从可迭代对象 `items` 中获取的项序列的和。`initial` 提供起始值，默认为 0。此函数通常仅适用于数字。

```
super()
```

返回一个代表其被使用类之所有集体超类的对象。该对象的主要目的是调用基类中的方法。示例如下：

```python
class B(A):
    def foo(self):
        super().foo()    # 调用由超类定义的 foo()。
```

```python
tuple({items})
```

代表元组的类型。如果提供了 `items`，它是一个用于填充元组的可迭代对象。然而，如果 `items` 已经是一个元组，它将原样返回。如果没有给出参数，则返回一个空元组。

表 10.10 显示了定义在元组上的方法。

### 表 10.10 元组操作符和方法

| 操作 | 描述 |
|---|---|
| `s + t` | 如果 `t` 是列表，则进行拼接。 |
| `s * n` | 如果 `n` 是整数，则进行重复。 |
| `s[i]` | 返回 `s` 的第 `i` 个元素。 |
| `s[i:j]` | 返回一个切片。 |
| `s[i:j:stride]` | 返回一个扩展切片。 |
| `len(s)` | `s` 中元素的数量。 |
| `s.append(x)` | 在 `s` 的末尾追加一个新元素 `x`。 |
| `s.count(x)` | 统计 `x` 在 `s` 中出现的次数。 |
| `s.index(x [, start [, stop]])` | 返回使 `s[i] == x` 成立的最小 `i`。`start` 和 `stop` 可选，用于指定搜索的起始和结束索引。 |
| `type(object)` | Python 中所有类型的基类。当作为函数调用时，返回 `object` 的类型。该类型与对象的类相同。对于整数、浮点数和列表等常见类型，该类型将指向其他内置类，如 `int`、`float`、`list` 等。对于用户定义的对象，该类型是其关联的类。对于与 Python 内部相关的对象，通常会获得 `types` 模块中定义类之一的引用。 |

```
vars([object])
```

返回 `object` 的符号表（通常位于其 `__dict__` 属性中）。如果没有给出参数，则返回与本地命名空间相对应的字典。应假设此函数返回的字典是只读的，修改其内容是不安全的。

```
zip([s1 [, s2 [, ... ]]])
```

创建一个迭代器，产生包含来自 `s1`、`s2` 等各一个项的元组。第 n 个元组为 (`s1[n]`, `s2[n]`, ... )。当最短的输入被耗尽时，生成的迭代器停止。如果没有给出参数，迭代器不产生任何值。

## 10.2 内置异常

本节描述用于报告不同种类错误的内置异常。

### 10.2.1 异常基类

以下异常作为所有其他异常的基类：

`BaseException`

所有异常的根类。所有内置异常都派生自此类。

`Exception`

所有程序相关异常的基类。这包括除 `SystemExit`、`GeneratorExit` 和 `KeyboardInterrupt` 之外的所有内置异常。用户定义的异常应继承自 `Exception`。

`ArithmeticError`

算术异常的基类，包括 `OverflowError`、`ZeroDivisionError` 和 `FloatingPointError`。

`LookupError`

索引和键错误的基类，包括 `IndexError` 和 `KeyError`。

`EnvironmentError`

发生在 Python 外部错误的基类。它是 `OSError` 的同义词。

上述异常永远不会被显式地抛出。然而，它们可以被用来捕获某些类别的错误。例如，以下代码将捕获任何类型的数值错误：

```python
try:
    # 某种操作
    ...
except ArithmeticError as e:
    # 数学错误
```

### 10.2.2 异常属性

异常实例 `e` 具有几个标准属性，在某些应用中可用于检查和/或操作它。

`e.args`

抛出异常时提供的参数元组。在大多数情况下，这是一个包含描述错误的字符串的一项元组。对于 `EnvironmentError` 异常，该值是一个包含整数错误号、字符串错误消息和可选文件名的 2 元组或 3 元组。如果你需要在不同的上下文中重建异常（例如，在不同的 Python 解释器进程中抛出异常），该元组的内容可能会很有用。

```
e.__cause__
```

使用显式链式异常时的前一个异常。

```
e.__context__
```

隐式链式异常的前一个异常。

```
e.__traceback__
```

与异常关联的追溯（Traceback）对象。

### 10.2.3 预定义异常类

以下异常由程序抛出：

`AssertionError`

`assert` 语句失败。

`AttributeError`

属性引用或赋值失败。

`BufferError`

预期为内存缓冲区。

`EOFError`

文件结束。由内置函数 `input()` 和 `raw_input()` 生成。需要注意的是，大多数其他 I/O 操作（如文件的 `read()` 和 `readline()` 方法）在遇到 EOF 时会返回空字符串而不是抛出异常。

`FloatingPointError`

浮点运算失败。需要注意的是，浮点异常处理是一个复杂的问题，仅在 Python 配置并构建为启用该功能时才会抛出此异常。更常见的情况是浮点错误静默地产生诸如 `float('nan')` 或 `float('inf')` 的结果。它是 `ArithmeticError` 的子类。

`GeneratorExit`

在生成器函数内部抛出以发出终止信号。这发生在生成器被过早销毁（在所有生成器值被消耗之前）或调用生成器的 `close()` 方法时。如果生成器忽略此异常，则生成器被终止，且该异常被静默忽略。

`IOError`

I/O 操作失败。其值为一个 `IOError` 实例，具有 `errno`、`strerror` 和 `filename` 属性。`errno` 是整数错误号，`strerror` 是字符串错误消息，`filename` 是可选的文件名。它是 `EnvironmentError` 的子类。

`ImportError`

当 `import` 语句找不到模块，或 `from` 无法在模块中找到名称时抛出。

`IndentationError`

缩进错误。它是 `SyntaxError` 的子类。

`IndexError`

序列下标越界。它是 `LookupError` 的子类。

`KeyError`

在映射中找不到键。它是 `LookupError` 的子类。

`KeyboardInterrupt`

当用户按下中断键（通常是 Ctrl+C）时抛出。

### MemoryError

可恢复的内存不足错误。

### ModuleNotFoundError

`import` 语句无法找到模块。

### NameError

在局部或全局命名空间中找不到名称。

### NotImplementedError

未实现的特性。可由要求派生类实现某些方法的基类抛出。它是 `RuntimeError` 的子类。

### OSError

操作系统错误。主要由 `os` 模块中的函数抛出。以下异常为其子类：

`BlockingIOError`, `BrokenPipeError`, `ChildProcessError`, `ConnectionAbortedError`, `ConnectionError`, `ConnectionRefusedError`, `ConnectionResetError`, `FileExistsError`, `FileNotFoundError`, `InterruptedError`, `IsADirectoryError`, `NotADirectoryError`, `PermissionError`, `ProcessLookupError`, `TimeoutError`。

### OverflowError

整数值太大而无法表示的结果。通常只有在将大整数值传递给其实现内部依赖于固定精度机器整数的对象时，才会出现此异常。例如，如果你指定的大小超过 32 位的起始或结束值，`range` 或 `xrange` 对象可能会出现此错误。它是 `ArithmeticError` 的子类。

### RecursionError

超过递归限制。

### ReferenceError

在底层对象被销毁后访问弱引用的结果（参见 `weakref` 模块）。

### RuntimeError

不属于任何其他类别的通用错误。

### StopIteration

抛出此异常以发出迭代结束的信号。这通常发生在对象的 `next()` 方法或生成器函数中。

### StopAsyncIteration

抛出此异常以发出异步迭代结束的信号。仅适用于 `async` 函数和生成器的上下文。

### SyntaxError

解析器语法错误。实例具有 `filename`、`lineno`、`offset` 和 `text` 属性，可用于收集更多信息。

### SystemError

解释器内部错误。其值为指示问题的字符串。

### SystemExit

由 `sys.exit()` 函数抛出。其值为指示返回码的整数。如果需要立即退出，可以使用 `os._exit()`。

### TabError

制表符（tab）使用不一致。当 Python 以 `-tt` 选项运行时产生。它是 `SyntaxError` 的子类。

### TypeError

当操作或函数应用于不适当类型的对象时发生。

### UnboundLocalError

引用了未绑定的局部变量。如果在函数中引用变量之前尚未定义该变量，则会出现此错误。它是 `NameError` 的子类。

### UnicodeError

Unicode 编码或解码错误。它是 `ValueError` 的子类。以下异常为其子类：`UnicodeEncodeError`, `UnicodeDecodeError`, `UnicodeTranslateError`。

### ValueError

当传递给函数或操作的参数类型正确但值不恰当时产生。

### WindowsError

由 Windows 上的系统调用失败产生。它是 `OSError` 的子类。

### ZeroDivisionError

除以零。它是 `ArithmeticError` 的子类。

## 10.3 标准库

Python 自带了一个相当庞大的标准库。本书此前已对其中许多模块进行了描述。参考资料可在 <https://docs.python.org/library> 找到。此处不再重复这些资料。

下面列出的模块之所以值得注意，是因为它们通常对各种应用程序以及一般的 Python 编程非常有用。

### 10.3.1 collections 模块

`collections` 模块为 Python 补充了各种额外的容器对象，这些对象在处理数据时非常有用——例如双端队列 (`deque`)、自动初始化缺失项的字典 (`defaultdict`) 以及用于制表的计数器 (`Counter`)。

### 10.3.2 datetime 模块

`datetime` 模块包含与日期、时间以及涉及这些内容的计算相关的函数。

### 10.3.3 itertools 模块

`itertools` 模块提供了各种有用的迭代模式——将可迭代对象链接在一起、遍历笛卡尔积、排列、分组以及类似操作。

### 10.3.4 inspect 模块

`inspect` 模块提供了用于检查代码相关元素（如函数、类、生成器和协程）内部结构的函数。它常用于元编程中定义装饰器和类似功能的函数。

### 10.3.5 math 模块

`math` 模块提供了常见的数学函数，如 `sqrt()`、`cos()` 和 `sin()`。

### 10.3.6 os 模块

`os` 模块包含与宿主操作系统相关的底层函数——进程、文件、管道、权限及类似功能。

### 10.3.7 random 模块

`random` 模块提供了各种与随机数生成相关的函数。

### 10.3.8 re 模块

`re` 模块通过正则表达式模式匹配为文本处理提供支持。

### 10.3.9 shutil 模块

`shutil` 模块具有执行与 shell 相关的常见任务的函数，例如复制文件和目录。

### 10.3.10 statistics 模块

`statistics` 模块提供了计算常见统计值（如平均值、中位数和标准差）的函数。

### 10.3.11 sys 模块

`sys` 模块包含大量与 Python 自身运行时环境相关的属性和方法。这包括命令行选项、标准 I/O 流、导入路径等类似功能。

### 10.3.12 time 模块

`time` 模块包含各种与系统时间相关的函数，例如获取系统时钟值、休眠以及 CPU 运行秒数。

### 10.3.13 turtle 模块

海龟图形。你知道的，给孩子们玩的。

### 10.3.14 `unittest` 模块

`unittest` 模块为编写单元测试提供了内置支持。Python 自身就是使用 `unittest` 进行测试的。然而，许多程序员更喜欢使用第三方库（如 `pytest`）进行测试。作者也赞同这一点。

## 10.4 结语：利用内置功能

在拥有数十万个 Python 包的现代世界中，程序员很容易寻求以第三方包依赖的形式来解决小问题。然而，Python 长期以来一直拥有一套极其有用的内置函数和数据类型。结合标准库中的模块，许多常见的编程问题通常仅凭 Python 已经提供的功能即可解决。如果有选择，请优先考虑后者。

## 索引

- ( ) (括号)

    - 用于函数, 22, 56, 101

    - 用于元组, 15

- * (星号)

    - 用于函数参数, 102—104, 108—109

    - 用于模块导入, 229—230, 240—241

    - 用于变量名, 46

    - 运算符, 5, 38—40, 47, 57, 298, 307, 310, 313

- ** (双星号)

    - 用于函数参数, 104, 108—109

    - 运算符, 5, 40, 56, 57

- *=, **= 运算符, 7, 41

- + (加号)

    - 用于文件模式, 258

    - 用于数字转换为文本字符串, 250—251

    - 运算符, 5, 10—11, 14, 38—40, 47, 57, 91, 298, 307, 310, 313

- += 运算符, 7, 41, 92, 111

- , (逗号)

    - 用于数字转换为文本字符串, 250—251

    - 分隔值, 276

- − (减号)

    - 用于字节格式化, 253

    - 用于数字转换为文本字符串, 250—251

    - 运算符, 5, 18, 39—40, 50, 57, 309

- -= 运算符, 7, 41, 92

- . (点) 运算符, 56, 79, 154

- .. (双点), 用于相对导入, 237

- ... (省略号), 用于扩展切片, 96

- / (斜杠)

    - 作为路径分隔符, 281

    - 用于函数签名, 105



- `-` 运算符, 5, 40, 57

- `//` 运算符, 5, 40, 57

- `//=`, `//=` 运算符, 7, 41

- `:`（冒号）
  - 用于字典, 18
  - 用于切片运算符, 10, 47—49

- `:=` 运算符, 8, 12, 39, 54, 57

- `=` 运算符, 3, 51

- `==` 运算符, 6, 42, 57, 93
  - 用于测试 `None`, 87

- `[]`（方括号）, 13

- `#` 注释, 2

- `%`（百分号）
  - 用于字节格式化, 253
  - 用于数字转换为文本字符串, 251
  - 运算符, 5, 9, 39—40, 57, 298, 310

- `%=`, `&=`, `^=` 运算符, 7, 41

- `&`, `^` 运算符, 6, 18, 40, 50, 57, 309

- `_`（下划线）
  - 2, 17, 46, 61
  - 作为变量, 2, 17, 46, 61
  - 用于函数名, 106
  - 用于内部变量名, 27
  - 用于数字字面量, 38
  - 用于私有属性和方法名, 176

- `__`（双下划线）
  - 用于属性名, 177—179
  - 用于方法名, 27, 88

- `~` 运算符, 6, 40, 57

- `\`（反斜杠）, 作为路径分隔符, 281

- `|` 运算符, 6, 18, 40, 50, 57, 302, 309

- `|=` 运算符, 7, 41

- `>`, `<` 运算符, 6, 42, 57

- `>=`, `<=` 运算符, 6, 42, 57, 93

- `>>`, `<<` 运算符, 6, 40, 57

- `>>=`, `<<=` 运算符, 7, 41

- `>>>` 提示符, 1

- `{ }`（花括号）, 20
  - 用于字典, 18
  - 用于 f-strings, 252

- `ABC` 基类, 185

- `abc` 模块, 185

- `abs()` 函数, 5, 40, 297

- `__abs__()` 方法, 91

- `@abstractmethod` 装饰器, 130, 185

- `__abstractmethods__` 属性, 222

- `add()` 方法, 18, 50, 309

- `__add__()` 方法, 27, 80, 90–91

- 加法, 5

- `__aenter__()`, `__aexit__()` 方法, 136

- `__aiter__()`, `__anext__()` 方法, 137

- `all()` 函数, 47, 297

- `__all__` 变量, 229, 240–241

- `and` 运算符, 6–7, 43, 57, 92

- `__and__()` 方法, 90

- 注解（annotations）, 23

- `__annotations__` 属性, 107, 129, 222, 242

- `any()` 函数, 47, 297

- `append()` 方法, 13, 26, 300, 307, 313

- 适用求值顺序（applicative evaluation order）, 101

- 存档, 处理方法, 284

- `argparse` 模块, 33, 255

- `args` 属性, 64–65, 70–315

- 参数, 参见 functions, arguments of

- 算术运算符, 5, 40

- `ArithmeticError` 异常, 67–68, 314–318

- `as` 限定符, 21, 64, 75, 99, 226

- `as_integer_ratio()` 方法, 303

- `ascii()` 函数, 253, 297

- `asctime()` 函数, 293

- `assert` 语句, 77–78

- `AssertionError` 异常, 68, 77, 315

- 赋值表达式运算符, 参见 `:=` 运算符

- 赋值, 38–39, 41, 83
  - 增强赋值, 7, 41, 47, 92, 111

- `async for`, `async with` 语句, 137

- `async` 关键字, 135, 136

- `asyncio` 模块, 135, 137, 151, 271–274, 285

- `atexit` 模块, 26

- `AttributeError` 异常, 68, 98, 207, 304, 315

- 属性, 79, 98
  - 绑定, 267, 207–208
  - 删除, 301
  - 全限定名, 158
  - 内部属性, 177–179
  - 属性的延迟求值, 214
  - 无类型限制, 179
  - 类的属性, 308
  - 函数的属性, 129–130
  - 对象的属性, 157–158, 304, 310
  - 公有属性, 276

- `await` 语句, 135–137, 151

- 可等待对象（awaitables）, 135

- 银行家舍入法（banker’s rounding）, 5

- 基类, 160
  - 抽象基类, 185–188
  - 调用基类方法, 313
  - 链接至基类, 207
  - `__slots__` 变量与基类, 210
  - 基类元组, 222
  - 用于类型提示, 184–185

- `base64` 模块, 274

- `BaseException` 异常, 67–68, 514

- `__bases__` 属性, 207, 222

- `bash` shell, 1

- `bin()` 函数, 37, 297

- 二进制数据结构, 288

- 二进制整数, 6

- `binascii` 模块, 274

- 位操作, 6

- `bit_length()` 方法, 305

- 按位运算符, 6, 40, 57

- 阻塞, 269–273

- `BlockingIOError` 异常, 270, 516

- `bool` 类, 297

- `bool` 类型, 298

- `__bool__()` 方法, 93–95

- 布尔值, 6–7, 38, 43–44, 297

- 绑定方法, 158, 183

- `break` 语句, 8, 12, 62–63, 141

- `breakpoint()` 函数, 298

- `BrokenPipeError` 异常, 316

- BSD socket 接口, 286

- `BufferedXXX` 类, 260

- `BufferError` 异常, 315

- 字节数组, 267, 266, 298–300

- `bytearray` 类型, 247, 298

- `bytes`, 247–248
  - 比较, 43
  - 转换为文本, 274
  - 格式化, 253–254
  - 字节操作, 298–300
  - 将对象序列化为字节, 268

- `bytes` 模块, 274

- `bytes` 类型, 247–248, 298

- `__bytes__()` 方法, 94–95

- `BytesIO` 类, 280

- C 编程语言, 281, 286, 288

- `__call__()` 方法, 98, 219

- `callable()` 函数, 301

- 回调函数, 114, 116
  - 向回调函数传递参数, 118–121
  - 从回调函数返回结果, 121–123

- `CallbackError` 异常, 122

- `capitalize()` 方法, 298, 310

- `casefold()` 方法, 310

- `category()` 函数, 295

- `__cause__` 属性, 65, 71–73, 315

- `__ceil__()` 方法, 91

- `center()` 方法, 328, 310

- `cgi` 模块, 275

- 字符
  - 文件结束符（EOF）, 2, 68, 315
  - 换行符, 参见 newline characters
  - 序数值, 307

- `check_output()` 函数, 288–289

- 子类, 参见 subclasses

- `ChildProcessError` 异常, 316

- `chr()` 函数, 301

- 循环依赖, 82

- 类方法, 89, 170–172, 222, 301

- 类语句, 27, 154–155, 215–218
  - 类语句中的基类名称, 160

- 类变量, 169–172, 222
  - 变更类变量, 112

- 类属性, 206, 223

- 类, 80, 153–223
  - 为类添加方法, 28
  - 类的正文, 215
  - 内置类, 313
  - 创建类, 160, 215–218
  - 重复定义类, 221
  - 扩展类, 160
  - 检查类, 318
  - 类中的内部变量, 27
  - 将实例链接到类, 206, 223
  - 类成员测试, 183
  - 类的名称, 222
  - 类的命名空间, 215, 218
  - 类中的静态方法, 173
  - 类型检查, 162
  - 类的统一性, 183
  - 用户自定义类, 179, 206–207
  - 仅含单个方法的类, 166

- `classmethod` 对象, 125

- `@classmethod` 装饰器, 125, 170–171, 183, 197, 213, 301

- `classobj` 类型, 305

- 清理, 66, 141

- `clear()` 方法, 300, 302, 409

- `click` 模块, 255

- `close()` 方法, 12, 147, 202, 258, 262, 315

- `closed` 属性, 263

- `__closure__` 属性, 129

- 闭包, 236–237, 129

- `cls` 对象, 125, 171, 220, 222

- 代码, *另见* programs
  - 生成代码, 222, 233
  - Python 风格（Pythonic）, 99–100, 160, 176
  - 代码的可读性, 103, 223
  - 代码测试, 223

- 代码检查工具, 87, 107

- `__code__` 属性, 129–130

- `collect()` 函数, 82

- `collections` 模块, 20, 81, 168, 240, 318

- 逗号分隔值（CSV）, 276

- 命令行选项, 15, 33, 254–255, 317, 319

- 注释, 2
  - 提取注释, 55

- 比较, 6, 42, 93
  - 字节与文本之间的比较, 248

- `compile()` 函数, 301

- `complex()` 函数, 301

- `__complex__()` 方法, 94–95, 301

- 复利计算, 4

- `compute_usage()` 函数, 282–283

- 连接（concatenation）, 47
  - 元组连接, 16

- 并发, 148, 269, 273, 291–293

- 条件语句, 4, 7–9, 44–45, 59–60

- `configparser` 模块, 276

- `conjugate()` 方法, 303, 305

- `ConnectionXXXError` 异常, 516

- 容器, 95–96
  - `__contains__()` 方法, 95–96

- 上下文管理器, 75–77, 99
  - 异步上下文管理器, 136–137
  - 使用上下文管理器进行清理, 141
  - `__context__` 属性, 65, 72–73, 515

- `contextlib` 模块, 77, 148
  - `@contextmanager` 装饰器, 148

- `continue` 语句, 8, 62–63

- 控制流
  - 使用条件语句, 7–9, 59–60
  - 使用异常, 64–69, 77
  - 使用循环, 60–63

- `copy()` 方法, 300, 302, 409

- 复制序列, 47–48

- 协程, 135
  - 基于生成器的协程, 146
  - 检查协程, 318

- `cos()` 函数, 318

- `count()` 方法, 298, 307, 310, 313

- `Counter` 类, 318

- 密码学哈希值, 278

- `csv` 模块, 31, 276

- `ctime()` 函数, 293

- `currentframe()` 函数, 132

- 守护进程标志（daemon flag）, 291

- 数据封装, 176

- 数据隐藏, 178

- `@dataclass` 装饰器, 134

- 数据类（dataclasses）, 196, 233

- `datetime` 模块, 293, 318

- 死锁, 25, 204

- `debug` 变量, 215

- `debug()` 函数, 133, 281

- 调试
  - 调试断点, 298
  - 调试错误消息, 66, 124
  - 异常处理与调试, 74
  - 在 Python 开发环境中调试, 3
  - 为调试引入代码, 77–78
  - 调试日志, 280
  - 生成调试输出, 162
  - 单独调试模块, 235
  - 拆分为更小的任务, 145
  - 栈帧与调试, 133
  - 使用字典时的调试, 21
  - 使用 `__dict__` 属性调试, 211
  - 使用 `repr()` 调试, 11
  - 使用 `__repr__()` 调试, 28, 196

- `decode()` 方法, 248, 259, 298, 310

- 装饰器, 104, 124–127, 194–197, 220

- 深拷贝, 83

- `deepcopy()` 函数, 84

- `def` 语句, 22, 27, 101

- `DEFAULT_BUFFER_SIZE` 值, 259

- `defaultdict` 类, 318

- `del` 语句, 19, 50–51, 82–83, 89, 202, 207, 300–302, 307

- `__del__()` 方法, 89, 201–206

- `delattr()` 函数, 157, 179, 301

- `__delattr__()` 方法, 98, 207

- 委托, 208–210

- `__delete__()` 方法, 211

- `__delitem__()` 方法, 95–96

- 依赖注入, 165, 176

- `deque` 类, 81, 318

- 描述符, 211–214, 220, 285

- *Design Patterns* 书籍, 176

- `detach()` 方法, 361

- `dict` 类型, 80, 301–302

- `dict()` 函数, 20, 51, 168

- `__dict__` 属性, 206–207, 211, 215, 222–223, 242, 302, 313

- 字典, 18–21
  - 访问字典成员, 18
  - 向字典添加非常规项, 85–87
  - 作为字面量, 38
  - 对字典进行赋值, 83
  - 转换为列表, 20
  - 创建字典, 18, 20, 53–54
  - 字典的深拷贝与浅拷贝, 83
  - 通过字典进行分发, 193
  - 空字典, 20, 43
  - 自动初始化缺失项, 318
  - 向字典插入对象, 18
  - 遍历字典, 21
  - 字典的键, 20–21, 294–295
  - 修改字典对象, 18

- 嵌套, 19

- 不支持有序比较, 43

- 项目数量, 306

- 相关操作, 51, 301–302

- 作为函数参数传递, 107

- 从中移除元素, 19, 104

- 在其中使用元组, 19

- 值, 21

- 字典推导式, 20, 53–54

- 字典查找, 176

- `DictReader` 类, 277

- 差集操作, 18, 50, 309

- `difference()` 方法, 309

- `difference_update()` 方法, 309

- `dir()` 函数, 26, 31, 302

- `__dir__()` 方法, 302

- 目录, 264

- 当前工作目录, 234

- 临时目录, 289

- `discard()` 方法, 18, 50, 309

- `distutils` 模块, 243

- 除法, 5, 303

- `divmod()` 函数, 5, 40, 303

- `__divmod__()` 方法, 90

- Django 库, 279

- `__doc__` 属性, 106, 129, 222, 242

- `docopt` 模块, 255

- 文档字符串, 106, 129, 155, 222, 242

- 点操作符, *参见* `.operator`

- 双端队列, 318

- 鸭子类型, 167

- `dump()` 函数, 268

- `dumps()` 函数, 280



- 数字中的`e`、`E`，37

- 回显服务器，286

- `.egg`后缀，234

- `elif`语句，7–8, 59–60, 193

- `Ellipsis`对象，96

- `else`语句，7–9, 44–45, 57, 59–60, 63, 66, 193

- 电子邮件，发送，285

- `encode()`方法，248, 259, 310

- 编码属性，13, 259–260, 263

- 编码，248–249, 263

- `end`关键字，265, 308

- `endswith()`方法，10, 298, 311

- `__enter__()`方法，75, 99, 148

- `enumerate()`函数，61, 303

- `env`命令，256

- 环境变量，256

- `EnvironmentError`异常，314–316

- `EOF`（文件结束）字符，2, 68, 315

- `EOFError`异常，68, 315

- `epoll()`函数，285

- `__eq__()`方法，93–94

- `errno`属性，316

- `errno`模块，277–278

- 错误
  - 处理，110–111
  - 日志记录，66

- `errors`属性，259–260, 263

- `eval()`函数，89, 301, 303, 308

- `Event`类，292

- `except`语句，24–25, 64–66, 70, 110
  - 范围的狭窄性，74

- `Exception`异常，366–69, 314

- 异常，24–25, 64–75
  - 改变控制流，67–69
  - 异步，69
  - 内建，67–68, 75, 314–318
  - 捕获，64, 66, 70, 73–74
  - 链式，70–73, 315
  - 定义新异常，69–70, 74
  - 预期与非预期，72–73
  - 提取附加值，141
  - 处理，24–25, 73–75, 110–111, 121–122, 277–278
  - 层级结构，67–68, 70
  - 忽略，65–66
  - 预定义，315–318
  - 传播，64
  - 抛出，64, 69, 110, 147, 315
  - 标准属性，64–65
  - 追溯消息，70, 73
  - 用户定义，69, 314
  - 使用函数包装，54

- `exec()`函数，133–134, 233, 301, 303

- `__exit__()`方法，75, 99, 148

- `expandtabs()`方法，298, 311

- 表达式，3, 38–39
  - 求值，43, 303

- `extend()`方法，300, 307

- 可扩展标记语言（XML），295

- `f-strings`，4, 9, 11, 251–252

- `False`值，6–7, 38, 43–45, 297–298

- 快速查找，19

- `fcntl`模块，262, 278

- `fcntl()`函数，278

- 文件描述符，257, 262

- `file`关键字，265, 308

- 文件模式，258, 263

- 文件对象，258, 262, 307
  - 属性，263
  - 实现，279
  - 操作，261
  - 支持的方法，261
  - 标准文件对象，263

- 文件指针，262

- `__file__`属性，36, 242

- `__file__`变量，241

- `FileExistsError`异常，258, 316

- `FileIO`类，260

- `filename`属性，316–317

- `fileno()`方法，262

- `FileNotFoundError`异常，277, 316

- 文件
  - 二进制与文本之间转换，261
  - 复制，284, 319
  - 编码，13, 263
  - 锁定，278
  - 元数据，282
  - 名称，257–258, 263
  - 换行符，260, 263
  - 打开，12, 256–258
  - 覆盖，258
  - 解析，105
  - 路径，281–283
  - 读取，12–13, 262
  - 删除，284, 319
  - 状态，263
  - 临时文件，289
  - 写入，262, 268

- `filter()`函数，138, 303

- 过滤，127–128

- `finally`语句，35, 66, 141

- `find()`方法，10, 299, 311

- 一等对象，85–87, 115, 242

- 标志变量，63

- `flask`库，279

- `float()`函数，11, 303, 315

- `__float__()`方法，94–95, 303

- `FloatingPointError`异常，67, 314–315

- 浮点数，3, 5, 37–38, 303, 315
  - 转换为文本，250–251
  - 精度，288
  - 四舍五入，5, 308

- `flock()`函数，278

- `__floor__()`方法，91

- `__floordiv__()`方法，90

- `flush()`方法，259, 262

- 享元模式，176

- `for`语句，12–13, 21, 45, 60–63, 140, 176
  - 用于读取文件行，262
  - 实现，97
  - 嵌套，144–145
  - 用于列表，52

- `format()`函数，11, 94, 250, 304

- `format()`方法，9, 252–253, 311

- `__format__()`方法，94, 304

- `format_map()`方法，311

- `from`语句，31, 228–230, 237, 316

- `from_`前缀，在方法名中，172

- `from_bytes()`方法，305

- `fromhex()`方法，274, 303

- `fromkeys()`方法，302

- `frozenset()`函数，304, 309

- `__fspath__()`方法，257

- 函数调用操作符，56

- 函数，22–24, 101–131, 137
  - 接收可迭代对象，47
  - 参数
    - 默认参数，23, 101–102, 115
    - 默认值，87, 157
    - 从左到右求值，101
    - 关键字参数，103–104
    - 数量，101–102
    - 顺序，101
    - 位置参数，105–106
  - 异步，135–137, 272, 317
  - 属性访问，207
  - 属性，129–130
  - 内建，297–314
  - 回调，114, 116, 118–123
  - 比较，131
  - 调试消息，124
  - 定义，22, 101
  - 延迟执行，145
  - 文档化，106, 129, 155
  - 模拟，98
  - 求值，116
  - 辅助函数，106
  - 高阶函数，115–118
  - 检查/内省，131–133, 318
  - 调用，22, 101, 111
  - 局部变量，24, 107, 111–113, 149–151
  - 元数据，124–125, 130
  - 命名，106, 129
  - 嵌套，113, 116–117, 129
  - 递归，114
  - 返回值，23, 109–110
  - 副作用，108
  - 签名，130–131
  - 类型提示，107, 129, 155
  - 包装函数，124

- `functools`模块，94

- `futures`，123

- 垃圾回收，26, 81–83, 89, 141, 203–204

- `gc`模块，82

- `__ge__()`方法，93

- 生成器表达式，54–56, 128

- `GeneratorExit`异常，147, 314–315

- 生成器，97, 139–152
  - 异步，317
  - 创建，54
  - 委托，142–144
  - 发送 I/O 流，265–266
  - 增强型，146–151, 266–267
  - 用于重复迭代，142
  - 检查/内省，318
  - 终止，315

- `get()`方法，19, 302

- `__get__()`方法，211–213

- `get_data()`函数，242

- `getattr()`函数，157, 179, 193–194, 304

- `__getattr__()`方法，98, 207–211

- `__getattribute__()`方法，98, 207, 211

- `__getitem__()`方法，95–96, 159–308

- `getsize()`函数，282

- `__gestate__()`方法，268

- `glob()`函数，264

- `global`语句，112

- `globals()`函数，131, 303–304

- `__globals__`属性，129, 131

- 通配符匹配（globbing），264

- `gmtime()`函数，293

- `__gt__()`方法，93

- `hasattr()`函数，157, 179, 304

- `hash()`函数，304

- `__hash__()`方法，93–94

- `hashlib`模块，278

- `help()`命令，22

- `hex()`函数，37, 95, 304

- `hex()`方法，274, 299, 303

- 高阶函数，115–118

- `http`包，279

- `httpx`库，279, 294

- 超文本标记语言（HTML），279

- 超文本传输协议（HTTP），279, 293–294

- `__iadd__()`、`__iand__()`方法，91–92

- `id()`函数，80, 304

- 标识符，38

- 身份检查，92

- `__idivmod__()`方法，91–92

- `if`语句，7–9, 39, 44–45, 52, 57, 59–60, 193

- `__ifloordiv__()`、`__ilshift__()`、`__imatmul__()`、`__imod__()`方法，91–92

- `import`语句，15, 30–35, 59, 225–237, 241, 245, 316
  - 在函数内部，228, 231

- `ImportError`异常，31, 67–68, 226, 237, 316

- `importlib`库，232

- `__imul__()`方法，91–92

- `in`操作符，19, 45, 50–52, 57, 96, 302

- 原地赋值，*参见* `assignments, augmented`

- `indent()`函数，290

- 缩进，4, 316

- `IndentationError`异常，316

- `index()`方法，299, 307, 311, 313

- `__index__()`方法，94–95

- `IndexError`异常，48, 49, 67, 314, 316

- 索引操作符，13
  - 用于字典，18
  - 用于元组，16

- `info()`函数，281

- 继承，28–30, 160–163
  - 导致代码损坏的情况，162
  - 继承自内建类型，167–169
  - 多重继承，163, 187–192, 211
    - 协同继承，190–192
    - 通过继承传播元类，220
  - `__slots__`变量与继承，210

- 有监督的，197–199

- 通过组合，164–166

- 通过函数，166–167

- 通过实现，163–164

- INI文件，276

- `__init__()`方法，27, 70, 89, 134, 154–155, 161, 181–201, 219–220

- `__init__.py`文件，34–35, 235–237, 2339–241

- `__init_subclass__()`方法，197–199, 220–222

- `input()`函数，13, 33, 304, 315

- 输入/输出（I/O），247–296
  - 缓冲，258–260
  - 消耗输入，266–267
  - 错误处理，249, 256, 259, 316
  - 生成输出，265–266
  - 处理，288, 291
  - 二进制模式，257–259
  - 文本模式，258–260
  - 非阻塞，270
  - 轮询通道，271, 273, 284

- `insert()`方法，13, 26, 300, 307

- `inspect`模块，318

- 实例，79, 154–156
  - 为其添加属性，161, 206
  - 备选构造函数，170–172
  - 缓存，200–201, 204–206
  - 创建，89, 199
  - 删除属性，156
  - 销毁，89, 201
  - 获取，156
  - 初始化，89
  - 链接到类，206, 223
  - 设置，156
  - 相关状态，206, 223
  - 存储数据，210–211

- `int`类，80

- `int()`函数，11, 95, 305

- `__int__()`方法，94–95

- 整数，3, 305
  - 作为字面量，37
  - 基数，37
  - 二进制，6
  - 转换
    - 为文本，251
    - 与字节互转，305
  - 从以下内容创建字符串
    - 二进制，37, 297
    - 十六进制，37, 299, 303–304
    - 八进制，37, 307
  - 遍历，31
  - 精度，316
  - 范围，21–22, 308
  - 测试值，303

- 接口，184–188

- 解释器，1, 3

- `InterruptedError`异常，316

- 交集操作，18, 50, 309

- `intersection()`方法，309

- `__invert__()`方法，91

- `io`模块，260–261, 279–280

- `ioctl()`函数，278

- `IOError`异常，316

- `__ior__()`、`__ipow__()`方法，91–92

- `ipython shell`，2

- `__irshift__()`方法，91–92

- “is a”关系，163

- `is not`运算符，42, 57, 80

- `is`运算符，42, 57, 80, 92

- `is_integer()`方法，303

- `IsADirectoryError`异常，316

- `isalnum()`、`isalpha()`方法，299, 311

- `isascii()`方法，311

- `isatty()`方法，362

- `isdecimal()`方法，311

- `isdigit()`方法，299, 311

- `isdir()`函数，282

- `isdisjoint()`方法，309

- `isfile()`函数，282

- `isidentifier()`方法，311

- `isinstance()`函数，64, 81, 183, 305

- `islower()`方法，299, 311

- `isnumeric()`、`isprintable()`方法，311

- `isspace()`方法，299, 311

- `issubclass()`函数，184, 305

- `issubset()`、`issuperset()`方法，309

- `istitle()`方法，299, 311

- `__isub__`方法，91–92

- `isupper()`方法，299, 311

- `items()`方法，21, 51, 302

- `iter()`函数，305

- `__iter__()`方法，97–98, 142, 152, 160, 305

- 迭代，21–22, 45–47, 60–62, 97–98, 305
  - 结束，69
  - 处理，307, 318
  - 嵌套，143
  - 产生值，139
  - 重复，142
  - 反转，308

- 迭代器对象
  - 异步，136–137
  - 创建，22, 61
  - 实现，98, 152
  - 内部栈，146
  - 反转，97

- `itertools`模块，318

- `__itruediv__()`方法，91–92

- `__ixor__()`方法，91–92

- `join()`函数，281

- `join()`方法，299, 311

- JSON格式，280

- `json`模块，280



`KeyboardInterrupt` 异常，67, 69, 314, 316

`KeyError` 异常，67, 314, 316

`keys()` 方法，20, 51, 302

`kqueue()` 函数，285

lambda 表达式，114–115, 117–118

延迟绑定，115

惰性求值，116, 214

`__le__()` 方法，93

左折叠操作，128

`len()` 函数，10, 47, 50, 51, 159, 298, 302, 306, 309–310, 313

`__len__()` 方法，28, 93, 95, 159–160, 308

库，235

行尾，参见 newline characters

`lineno` 属性，317

- `list` 类，14, 80
- 列表推导式，37, 52, 55
  - 使用其过滤，127
- `list()` 函数，20, 47, 55, 81, 168, 306
- `listdir()` 函数，264
- 列表，13–15
  - 向其中添加项，13, 307
  - 作为字面量，38, 46
  - 作为序列，47
  - 对其进行赋值，83
  - 比较，42
  - 拼接，14
  - 将数据转换为列表，从列表转换，14
  - 创建，13
    - 深拷贝与浅拷贝，83, 306
  - 定义其子类型，81
  - 空列表，14, 43–44, 306
  - 遍历，13, 21
  - 修改，49–50
  - 嵌套，14, 145–146
  - 项的数量，306–307
  - 作为函数参数传递，107
  - 处理，52–53, 307
  - 从中删除项，307
  - 切片，14
  - 排序，307, 310
- 字面量，37–38
- `ljust()` 方法，299, 311
- `load()` 函数，268
- `loads()` 函数，280
- `locals()` 函数，131, 303, 307
- `localtime()` 函数，293

`Lock` 类，291

锁，25

`Logger` 实例，280–281

`logging` 模块，254, 280–281

逻辑运算符，6–7, 43, 57, 92

`LookupError` 异常，67–68, 314, 316

- 循环，4, 7–9, 21–22, 60–63
  - 中断，141
  - 其中的标志变量，63
  - 其中的数值索引，61
  - 跳过剩余部分，8, 62
  - 从不同序列中取项，62

松耦合，167

`lower()` 方法，10, 299, 311

`__lshift__()` 方法，90

`lstrip()` 方法，299, 311

`__lt__()` 方法，93–94

`main()` 函数，33, 281

`__main__` 模块，234

`__main__.py` 文件，235, 239, 245

`maketrans()` 方法，299, 311

`map()` 函数，128, 307

- 映射，18–19, 128, 307
  - 相关操作，51–52

`math` 模块，318

数学运算，5, 40, 90–92

`__matmul__()` 方法，90

`max()` 函数，47, 94, 128, 307

MD5 算法，278

- 内存
  - 分配，82
  - 减少使用量，55, 210–211

`MemoryError` 异常，68, 316

`metaclass` 关键字，218–219

元类，217–222

方法解析顺序（MRO），190–192, 222

- 方法，79, 154
  - 抽象，185, 222
  - 对象可用的，26
  - 绑定，158, 183
  - 自动装饰，222
  - 定义，215
  - 全限定，158
  - 实现，213
  - 内部，176
  - 内部变量，27
  - 调用，154
  - 魔术（特殊），154, 210
  - 命名，172, 176
  - 公开，176
  - 重定义，28, 160
  - 重写，195
  - 静态，173–176, 310
  - 用户定义，180

Microsoft Excel，276

`min()` 函数，47, 94, 128, 307

`mixin` 类，188–192, 220

`__mod__()` 方法，90

`mode` 属性，263

- 模块对象，226
  - `__module__` 属性，129, 222
  - `__module__` 变量，215
  - `ModuleNotFoundError` 异常，316
  - 模块，30–32, 225–235
    - 作为一等公民对象，242–243
    - 缓存，227–228, 231–233
    - 编译，233
    - 调试，235
    - 导入，31, 225–227, 232–234
      - 循环导入，230–232
      - 导入特定定义，228–230
    - 列出内容，31
    - 定位，226
    - 名称，222, 226, 234, 242
    - 命名空间，242, 304
    - 组织，33
    - 重新加载和卸载，232–233
    - 重命名，227
    - 标准库，31, 273–296, 318–319
    - 第三方，32

取模，5, 307

单子（monads），123

`__mro__` 属性，190, 207, 222

`__mul__()` 方法，88, 90

乘法，5

`name` 属性，263

名称修饰（name mangling），177–179

`__name__` 属性，106, 129, 222, 242

`__name__` 变量，33, 234

命名字段，19

`namedtuple()` 函数，134

`NameError` 异常，68, 111, 316–317

命名空间包，237

- 命名空间，31, 158, 226, 242
  - 全局，112
  - 局部，211
  - 类的，215, 218
  - 包的，239–240

`nc` 程序，274, 286

`__ne__()` 方法，93

`__neg__()` 方法，91

网络程序，286, 288, 291

`__new__()` 方法，89, 199–201, 219

`new_class()` 函数，216–217

`newline` 属性，260

- 换行符，260, 263, 301, 304
  - 在输出中控制，265
  - 在输入中，266

`newlines` 属性，263

`next()` 函数，139–141, 307

`next()` 方法，317

`__next__()` 方法，97, 140, 152

`None` 值，6, 43–44, 87, 102, 108–110

`normalize()` 函数，295

`not in` 运算符，45, 57

`not` 运算符，6–7, 43, 57, 92

`NotADirectoryError` 异常，316

`NotImplemented` 对象，91, 93

`NotImplementedError` 异常，68, 93, 316

- 数字
  - 比较，42
  - 复数，301, 303, 305
  - 转换
    - 从对象转换，94–95
  - 从字符串转换，11
  - 到文本，250–251
  - 浮点数，5, 37–38, 250–251, 288, 303, 308, 315
    - 非空的，43
    - 精度，251
    - 随机，319
    - 求和，312

`numpy` 包，50, 88, 96, 263

- `object` 类，190, 307
  - 继承自，160, 191
- 对象，26–30, 79–99, 153
  - 属性，56
  - 内建对象，222–223
    - 检查类，183
    - 比较，42, 80, 92–94
    - 转换为内建类型，94–95
    - 协程，135
    - 深拷贝与浅拷贝，83
    - 一等公民，85–87, 115
    - 哈希值，93–94, 304
    - 标识/身份，80, 304
    - 不可变，102
    - 实现运算符，79
    - 初始化，27
    - 像函数一样调用，98
    - 可迭代，45
    - 列出可用方法，26
    - 位置，38–39
    - 管理，89–90
    - 可用方法，26
    - 可变，41, 83–84, 107–108
  - 引用计数，81–83
  - 引用，83–84
  - 表示，84–85, 297, 308
  - 序列化，268–269
  - 排序，94
  - 状态，154
  - 类型，79, 154
  - 解包值，45–46, 60
  - 值，79, 84–85

`oct()` 函数，37, 95, 307

`offset` 属性，317

`open()` 函数，12, 15, 241, 256–261, 279, 307

操作系统函数，281, 316, 319

- 运算符，39–40
  - 算术，5, 40
  - 增强赋值，7, 41, 47, 92, 111
  - 位运算符，6, 40, 57
  - 比较，6, 42–43, 93
  - 实现，79
  - 逻辑，6–7, 43, 57, 92
  - 优先级规则，56–58

`or` 运算符，6–7, 43, 57, 92

`__or__()` 方法，90

`ord()` 函数，307

`os` 模块，258, 281, 319

`os.exit()` 方法，317

`os.chdir()`、`os.getcwd()` 方法，257

`os.environ` 变量，256

`os.path` 模块，281–282

`os.system()` 函数，284

`OSError` 异常，64–65, 67–68, 277, 314, 316–318

输出，参见[输入/输出（I/O）](input/output)

`OverflowError` 异常，417, 314, 316

- `__package__` 属性，242
- 包，23–34, 235–242
  - 数据文件，241–242
  - 部署，243–244
  - 导出，240–241
  - 导入包内文件，34
  - 包内导入，237
  - 安装，36, 244
  - 定位，36
  - 命名空间，239–240
  - 命名，243
  - 子模块，作为脚本运行，238–239
  - 第三方包，50

`pandas` 库，277

参数，参见 functions, arguments of

父类，参见 base classes

`partial()` 函数，98

`partition()` 方法，299, 311

`pass` 语句，7, 60, 65

`Path` 类，282

路径分隔符，281

`__path__` 属性，242

`pathlib` 模块，257, 264, 281–283

模式，176

- 性能
  - 异常处理与性能，111
  - 局部变量与性能，149–151
  - 优化，210, 220–221
  - 类型检查与性能，81

`PermissionError` 异常，277, 316

`pickle` 模块，268–269

`pip` 命令，35–36, 244

`poll()` 函数，285

`pop()` 方法，27, 104, 300, 302, 307, 309

`Popen` 类，289

`popitem()` 方法，302

`__pos__()` 方法，91

POSIX 标准，281

`pow()` 函数，5, 40, 307

`__pow__()` 方法，90

幂（数学），5, 307

`__prepare__()` 方法，219

原始类型，3

`print()` 函数，4, 11–13, 84, 265, 308

`ProcessLookupError` 异常，316

- 程序，另见 code
  - 创建，2–3
  - 执行，1, 3, 234–235
  - 加载，228, 233
  - 副作用，108
  - 指定解释器，3
  - 从包启动，244
  - 结构化，34–35, 59, 235
  - 终止，26, 69
- 属性，180–183
  - 关联函数，207, 211
  - 实现，211

`@property` 装饰器，180–182, 308

协议，87–99

代理，104, 208

`push()` 方法，27

`.py` 后缀，2, 3, 30, 226, 233

`__pycache__` 目录，233

`pytest` 库，299

## Python

- 将设计模式应用于 Python，176
- 灵活性，86
- 缩进，4, 316
- 交互模式，1–2
- 无内部变量，27
- 优化模式，77
- 包索引，243
- 运行时环境，254, 319

`python` shell，1

`PYTHONPATH` 环境变量，234

`__qualname__` 属性，129, 222

`__qualname__` 变量，215

`Queue` 类，292

`quit()`，在 REPL 中，2

`__radd__()` 方法，90–91

`raise` 语句，25, 64, 69

`__rand__()` 方法，91

`random` 模块，319

`range()` 函数，31–22, 308

`raw_input()` 函数，315

`__rdivmod__()` 方法，90

`re` 模块，283–284, 319

`read()` 函数，258

`read()` 方法，12, 262, 315

读取-求值-打印循环（REPL），5

`readable()` 方法，262

`readinto()` 方法，262–263

`readline()` 方法，262, 315

`readlines()` 方法，262

递归，114

- 限制，114, 143, 317

`RecursionError` 异常，317

`reduce()` 函数，128

引用计数，81–83, 201

引用循环，203

`ReferenceError` 异常，317

注册表，194, 197, 222

正则表达式，283–284, 319

`reload()` 函数，232

远程服务器，308

`remove()` 方法，18, 50, 300, 307, 309

`removeprefix()` 方法，299, 312

`removesuffix()` 方法，299, 312

`replace()` 方法，10, 299, 312

`repr()` 函数，11, 85, 89, 252, 308

`__repr__` 方法，28, 89–90, 154–155, 159–199
- 默认实现，160

`requests` 库，279, 294

资源控制，99

`return` 语句，59, 109, 135, 140

`reverse()` 方法，300, 307

`reversed()` 函数，97, 308

`__reversed__` 方法，97, 308

`rfind()` 方法，299, 312

`__rfloordiv__` 方法，90

`rglob()` 函数，264

`rindex()`、`rjust()` 方法，299, 312

`__rlshift__()` 方法，91

`__rmatmul__()`、`__rmod__()`、`__rmul__()` 方法，90

`__ror__()`、`__round__()` 方法，91

`round()` 函数，5, 40, 308

`rpartition()`、`rsplit()` 方法，299, 312

`__rpow__()` 方法，90

`__rrshift__()` 方法，91

`__rshift__()` 方法，90

`rstrip()` 方法，300, 312

`__rsub__()`、`__rtruediv__()` 方法，90

`run()` 函数，135, 270–271

`RuntimeError` 异常，68, 114, 316–317

`__rxor__()` 方法，91

沙箱，36

脚本，32–33



`seek()`, `seekable()` 方法, 262

`select` 模块, 271, 284–285

`select()` 函数, 285

`selectors` 模块, 271, 285

`self` 对象, 27, 154, 158, 169, 220

`send()` 方法, 152

`sep` 关键字, 265, 308

## 序列

- 比较, 43
- 可变序列, 49–50
- 序列操作, 47–50

集合推导式, 17, 53

`set()` 函数, 17–18, 20, 47, 309

- `__set__()` 方法, 211
- `__set_name__()` 方法, 212
- `setattr()` 函数, 157, 179, 310
- `__setattr__()` 方法, 98, 207, 211
- `setdefault()` 方法, 302
- `__setitem__()` 方法, 95–96, 167
- 集合, 17–18
  - 添加/删除元素, 50, 309
  - 字面量, 38, 46
  - 创建, 17, 309
  - 空集合, 18
  - 不可变, 304
  - 元素数量, 50, 306, 309
  - 元素顺序, 17
  - 处理, 50–51, 53–54, 309
- `__setstate__()` 方法, 268
- `setup()` 函数, 244
- `setup.py` 文件, 244
- `setuptools` 模块, 234, 243–244
- SHA-1 算法, 278
- 浅拷贝, 83
- Shell, 1, 284, 319
- 短路求值, 43
- `shutil` 模块, 284, 319
- 副作用, 108
- `SIGINT` 信号, 69
- `signal` 模块, 69
- `signature()` 函数, 130–131
- `__signature__` 属性, 131
- 简单邮件传输协议 (SMTP), 285
- `sin()` 函数, 318
- 单例, 176, 200

`site-packages` 目录, 35, 244

`sleep()` 函数, 293

`slice` 实例, 96

`slice()` 函数, 310

切片运算符, 10, 47–49, 298, 307, 310, 313

- 实现, 96
- 在列表上使用, 14
- 在元组上使用, 16

`__slots__` 变量, 210–211, 220–221, 223

`smtplib` 模块, 285–286

`socket` 模块, 286–287

`sort()` 方法, 108, 307

`sorted()` 函数, 47, 114, 310

`splatting` (星号解包), 46

`split()` 函数, 281

`split()` 方法, 10, 300, 312

`splitlines()` 方法, 300, 312

`sprintf()` 函数 (C), 253

`sqrt()` 函数, 38, 318

栈帧, 132–133

栈回溯对象, 65, 73

标准错误, 263

标准输入/输出, 263, 304

`start` 关键字, 62

`startswith()` 方法, 10, 300, 312

状态机, 176

语句, 59

- 执行, 303

`@staticmethod` 装饰器, 125, 173, 183, 213, 310

`statistics` 模块, 47, 319

`stdin`, `stdout` 属性, 289

`StopAsyncIteration` 异常, 317

- `StopIteration` 异常, 67, 69, 97, 140–141, 147, 307, 317
- `str()` 函数, 11, 84, 94, 168, 248, 251–252, 310
- `__str__()` 方法, 94, 171, 310
  - 默认实现, 160
- 策略模式, 176
- `strerror` 属性, 316
- `stride` 参数, 48, 49, 96
- `StringIO` 类, 279
- 字符串, 3, 9–12
  - 作为字面量, 38
  - 作为序列, 47
  - 检查字符, 311
  - 比较, 43
  - 拼接, 10–11, 310
  - 转换
    - 从非字符串值转换, 11, 304
    - 从对象转换, 94
    - 转换为数字, 11
  - 转换为大写/小写, 310–312
  - 创建, 11, 310
  - 编码/解码, 310
  - 格式化, 9, 11, 250–253, 310–311
  - 迭代遍历, 21
  - 相关方法, 10
  - 非空字符串, 43
  - 元素数量, 10, 306, 310
  - 处理, 310–312
  - 表示形式, 89–90
  - 子字符串, 10, 310–312
  - 三引号字符串, 9, 38
  - 空白字符, 312
- `strip()` 方法, 10, 300, 312
- `struct` 模块, 288
- `struct_time` 对象, 293
- `__sub__()` 方法, 90
- 子类, 81, 160
  - 检查类是否为子类, 184, 305
  - 实现接口, 185
- `subprocess` 模块, 256, 288–289
- 减法, 5
- 子类型, 见 子类
- `sum()` 函数, 15, 47, 128, 312
- `super()` 函数, 161, 189–192, 199, 207, 313
- 超类, 见 基类
- `swapcase()` 方法, 300, 312
- 对称差集运算, 18, 50, 309
- `symmetric_difference()` 方法, 309
- `symmetric_difference_update()` 方法, 309
- `SyntaxError` 异常, 316, 317
- `sys` 模块, 15, 319
- `sys.argv` 列表, 33, 254–255
- `sys.exit()` 函数, 317
- `sys.getdefaultencoding()` 方法, 259
- `sys.getfilesystemencoding()` 函数, 257, 264
- `sys._getframe()` 函数, 132
- `sys.getrecursionlimit()` 函数, 114
- `sys.getrefcount()` 函数, 82
- `sys.modules` 变量, 227, 232
- `sys.path` 变量, 31, 35, 226, 234, 244
- `sys.setrecursionlimit()` 函数, 114
- `sys.stderr` 对象, 69, 263–264
- `sys.stdin`, `sys.stdout` 对象, 263–264
- `SystemError` 异常, 317
- `SystemExit` 异常, 15, 26, 67, 69, 314, 317
- `TabError` 异常, 317
- 制表符, 19, 311, 318
- 电传打字机 (TTY), 281
- `tell()` 方法, 262
- `telnet` 程序, 274, 286
- `tempfile` 模块, 289–290
- 测试
  - 较小任务的测试, 145
  - 使用文件对象进行测试, 279
- 文本, 247–248
  - 从二进制数据转换, 274
  - 编码/解码, 13, 248–250, 255, 259
  - 适配终端宽度, 290
  - 处理行, 260, 263
- `text` 属性, 317
- `TextIOWrapper` 类, 260
- `textwrap` 模块, 290
- `threading` 模块, 271, 291–293
- 线程, 271–272
- `throw()` 方法, 147, 152
- `time` 模块, 293, 319
- `time()` 函数, 293
- 时间处理, 293, 318–319
- `TimeoutError` 异常, 316
- `title()` 方法, 300, 312
- `to_bytes()` 方法, 305
- `@trace` 装饰器, 125–126
- 追溯信息, 24, 315
- `traceback` 模块, 73
- `__traceback__` 属性, 65, 73, 315
- `translate()` 方法, 299–300, 312
- `True` 值, 6–7, 38, 43–45, 297–298
- `__truediv__()` 方法, 90
- `__trunc__()` 方法, 91
- `truncate()` 方法, 262
- 截断除法, 5
- `try` 语句, 24–25, 64, 66, 110, 141
- `tuple` 类型, 313
- `tuple()` 函数, 47
- 元组, 15–17
  - 作为键, 52
  - 作为字面量, 38, 46
  - 作为序列, 47
  - 比较, 42
  - 拼接, 16
  - 创建, 15
  - 空元组, 43, 313
  - 索引, 16
  - 迭代遍历, 17, 21
  - 具名元组, 109–110
  - 元素数量, 306, 313
  - 通过元组从函数返回多个值, 23, 109
  - 切片, 16
  - 解包, 16
  - 在字典中使用, 19
- `turtle` 模块, 319
- `type` 类, 218–220, 313
- 类型提示, 107, 129, 155, 179–180, 222
  - 根据类型提示创建方法, 197
  - 模块级类型提示, 242
  - 结合基类使用, 184–185
- `type()` 函数, 70, 80, 154, 217, 313
- 基于类型的分发, 193–194
- `TypeError` 异常, 43, 68, 95, 101, 103, 122, 191, 211, 305, 317
- 类型, 79, 313
  - 内置类型, 167–169
  - 检查值是否符合类型, 81, 305
  - 类型之间转换, 94–95
- `types` 模块, 313
- UDP 服务器, 287
- 一元负号/正号, 5
- `UnboundLocalError` 异常, 68, 111, 317
- Unicode 编码
  - 码点值, 307
  - 在源代码中, 2
  - 对文本字符串的操作, 294–295
- `unicodedata` 模块, 294–295
- `UnicodeError` 异常, 67–68, 249, 317
- `UnicodeXXXError` 异常, 317
- 并集运算, 18, 50, 309
- `union()` 方法, 309
- `unittest` 模块, 319
- 通用换行模式, 260
- UNIX
  - EOF 字符, 2
  - 执行文件, 3
  - 低级 I/O 控制操作, 278
  - 换行符, 260
  - 路径分隔符, 281
- `unpack()` 函数, 288
- `update()` 方法, 18, 168, 302
- `upper()` 方法, 10, 300, 312
- `urlencode()`, `urlopen()`, `urlparse()` 函数, 293–294
- `urllib` 包, 293–294
- `urllib.parse` 包, 294
- `UserDict`, `UserList`, `UserString` 类, 168
- UTF-8 编码, 2, 13, 249–250
- `ValueError` 异常, 25, 67–68, 317
- 值, 3, 79
  - 与类型进行检查, 81, 305
  - 最小值/最大值, 307
  - 打印, 265, 308
  - 归约, 128
  - 表示形式, 84–85
  - 原地更新, 41
- `values()` 方法, 21, 51, 302
- 变量, 3
  - 关联类型, 3, 167
  - 自由变量, 114–115
  - 全局变量, 111–113
  - 局部变量, 24, 111–113, 134, 149–151
  - 名称, 3
  - 重新赋值, 108
  - 星号变量, 46
  - 类型提示, 107
  - 未绑定变量, 317
- `vars()` 函数, 313
- `venv` 命令, 36
- 虚拟环境, 36
- 海象运算符, 见 `:=` 运算符
- `warning()` 函数, 281
- 弱引用, 204–206, 317
- `weakref` 模块, 204, 317
- `__weakref__` 属性, 206
- Web 服务器, 279
- 网站, 275, 294
- `while` 语句, 4, 7–9, 12, 39, 60–62
- Windows
  - EOF 字符, 3
  - 执行文件, 3
  - 失败的系统调用, 318
  - 换行符, 260
  - 路径分隔符, 281
- `WindowsError` 异常, 318
- `with` 语句, 12, 25, 75–77, 99, 202, 256, 289–290
- `wrap()` 函数, 290
- 包装器, 104, 208
- `@wraps` 装饰器, 124–125
- `writable()` 方法, 362
- `write()` 函数, 265
- `write()` 方法, 13, 362
- `write_through` 属性, 263
- `writelines()` 方法, 362
- `xml` 包, 295–296
- `xml.etree` 包, 295
- `__xor__()` 方法, 90
- `yield from` 语句, 142–143
- `yield` 语句, 97, 139–142, 265
  - 用作表达式, 146–147
- `ZeroDivisionError` 异常, 467, 314, 318
- `zfill()` 方法, 300, 312
- `zip()` 函数, 62, 314

Python Programming Language LiveLessons 为开发者提供 Python 编程语言的引导式学习，包括对库和框架中使用的许多高级技术的演示。

观看并学习如何：

- 从文件中读取和写入数据
- 使用元组、列表、集合和字典有效地操作数据
- 定义新函数
- 处理异常和错误
- 使用类创建新对象
- 利用面向对象编程技术
- 使用特殊方法、属性和描述符自定义对象
- 使用元编程特性，包括装饰器、类装饰器和元类
- 将代码组织到模块和包中

## 节省 60%——使用优惠码 `BEAZLYVID`

`informit.com/beazley/video`

> 在 InformIT 购买特色视频时，使用折扣码 `VIDEOBOB` 可享受标价 60% 的折扣。优惠内容可能会有所变动。

## Python 编程书籍、电子书和视频

InformIT 是 Pearson 技术品牌（包括 Addison-Wesley）的网站，为所有经验水平的用户提供 Python 编程教程、参考指南和实用手册。我们的大多数电子书均无 DRM 限制，并提供三种格式：PDF、EPUB 和 MOBI。

访问 `informit.com/python` 进行购物、预览样本章节并观看我们目录中的免费视频课程。

- Python Essential Reference - David Beazley
- Effective Python - Brett Slatkin
- Learn More Python 3 the Hard Way - Zed Shaw
- Modern Python LiveLessons - Raymond Hettinger
- Supercharged Python - Brian Overland
- Refactoring in Python LiveLessons - Bryan Beecham
- Machine Learning with Python for Everyone - Mark E. Fenner
- The Python 3 Standard Library by Example - Doug Hellman

Addison-Wesley · Adobe Press · Cisco Press · Microsoft Press · Pearson IT Certification · Que · Sams · Peachpit Press

## 面向 IT 专业人士的视频培训

- **快速学习**：在短短几小时内掌握一项新技术。视频培训能在更短的时间内教授更多内容，且资料通常更容易吸收和记忆。
- **观看并学习**：讲师现场演示概念，让您直观看到技术的实际运行。
- **自我测试**：我们的完整视频课程在整个学习过程中提供自我评估测试。
- **便捷灵活**：大多数视频支持流媒体播放，并提供下载选项以便离线观看。

了解更多信息，浏览我们的商店，并在 `informit.com/video` 观看免费示例课程。

**使用折扣码 `VIDBOB` 可在视频课程原价基础上节省 50%**



折扣码 `VIDBOB` 适用于在 `Informit.com` 购买的合格书目的原价 50% 折扣。合格书目包括大多数全课程视频标题、书本 + 电子书捆绑包、电子书 + 视频捆绑包、单个视频课程、精简版（Rough Cuts）、Safari Books Online。不可折扣的标题、通过零售合作伙伴促销的标题，以及任何被列为“每日之书”或“每周视频特惠”的标题均不参与此折扣。折扣不得与其他优惠叠加，且不可兑换现金。优惠内容可能会有所变更。

## 在 `informit.com/register` 注册您的产品

获取更多额外权益，并**在下次购买时节省 35%**。

- 自动收到一张下次购买可享 35% 折扣的优惠券，有效期为 30 天。请在 InformIT 购物车或账户页面的“管理代码（Manage Codes）”部分查找您的代码。
- 下载可用的产品更新。
- 获取奖金资料（如有）。
- 勾选复选框以接收我们的通知，获取新版本和相关产品的专属优惠。

> 注册权益因产品而异。具体权益将列在您账户页面的“已注册产品”下。

### InformIT.com——值得信赖的技术学习资源

InformIT 是全球领先的教育公司 Pearson 旗下信息技术品牌的在线之家。在 `InformIT.com`，您可以：

- 购买我们的书籍、电子书、软件和视频培训。
- 利用我们的特别优惠和促销活动（`informit.com/promotions`）。
- 订阅特别优惠和内容时事通讯（`informit.com/newsletters`）。
- 访问数以千计的免费章节和视频课程。

**与 InformIT 建立联系——访问 `informit.com/community`**

Addison-Wesley · Adobe Press · Cisco Press · Microsoft Press · Pearson IT Certification · Que · Sams · Peachpit Press

## 代码片段

许多书目包含编程代码或配置示例。为了优化这些元素的呈现效果，请在单列、横屏模式下查看电子书，并将字体大小调整为最小设置。除了以可重排文本格式呈现代码和配置外，我们还包含了一系列模仿印刷书呈现效果的代码图像；因此，在可重排格式可能会影响代码列表呈现的地方，您将看到一个“点击此处查看代码图像”的链接。点击该链接即可查看与印刷版一致的代码图像。要返回前一页，请点击设备或应用程序上的“返回”按钮。

```text
Python 3.8.0 (default, Feb 3 2019, 05:53:21)
[GCC 4.2.1 Compatible Apple LLVM 8.0.0 (clang-800.0.38)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print('Hello World')
Hello World
>>>
```

```text
Python 3.8.0 (default, Feb 4, 2019, 07:39:16)
Type 'copyright', 'credits' or 'license' for more information
IPython 6.5.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: print('Hello World')
Hello World

In [2]:
```

```text
>>> 6000 + 4523.50 + 134.25
10657.75
>>> _ + 8192.75
18850.5
>>>
```

```python
42 # int
4.2 # float
'forty-two' # str
True # bool
```

```python
2 + 3 * 4 # -> 14
```

```python
# interest.py

principal = 1000    # Initial amount
rate = 0.05        # Interest rate
numyears = 5       # Number of years
year = 1
while year <= numyears:
    principal = principal * (1 + rate)
    print(year, principal)
    year += 1
```

```python
print(f'{year:>3d} {principal:0.2f}')
```

```python
a = 0b11001001
mask = 0b11110000
x = (a & mask) >> 4  # x = 0b1100 (12)
```

```python
if a < b:
    print('Computer says Yes')
else:
    print('Computer says No')
```

```python
if a < b:
    pass # Do nothing
else:
    print('Computer says No')
```

```python
if suffix == '.htm':
    content = 'text/html'
elif suffix == '.jpg':
    content = 'image/jpeg'
```

```python
elif suffix == '.png':
    content = 'image/png'
else:
    raise RuntimeError(f'Unknown content type {suffix!r}')
```

```python
maxval = a if a > b else b
```

```python
x = 0
while (x := x + 1) < 10:
    print(x)
```

```python
x = 0
while x < 10:
    if x == 5:
        break # Stops the loop. Moves to Done below
    print(x)
    x += 1

print('Done')
```

```python
x = 0
while x < 10:
    x += 1
    if x == 5:
        continue # Skips the print(x). Goes back to loop start.
    print(x)

print('Done')
```

```python
a = 'Hello World'
b = "Python is groovy"
c = '''Computer says no.'''
d = """Computer still says no."""
```

```python
print('''Content-type: text/html

<h1> Hello World </h1>
Click <a href="http://www.python.org">here</a>.
''')
```

```python
print(
'Content-type: text/html\n'
'\n'
'<h1> Hello World </h1>\n'
'Clock <a href="http://www.python.org">here</a>\n'
)
```

```python
print(f'{year:>3d} {principal:0.2f}')
```

```python
base_year = 2020
...
print(f'{base_year + year:>4d} {principal:.2f}')
```

```python
print('{0:>3d} {1:0.2f}'.format(year, principal))
print('%3d %0.2f' % (year, principal))
```

```python
a = 'Hello World'
print(len(a))    # 11
b = a[4]         # b = 'o'
c = a[-1]        # c = 'd'
```

```python
c = a[:5]             # c = 'Hello'
d = a[6:]             # d = 'World'
e = a[3:8]            # e = 'lo Wo'
f = a[-5:]            # f = 'World'
```

```python
g = a.replace('Hello', 'Hello Cruel') # f = 'Hello Cruel World'
```

```python
g = a + 'ly'  # g = 'Hello Worldly'
```

```python
x = '37'
y = '42'
z = x + y  # z = '3742' (String Concatenation)
```

```python
z = int(x) + int(y)  # z = 79  (Integer Addition)
```

```python
s = 'The value of x is ' + str(x)
s = 'The value of x is ' + repr(x)
s = 'The value of x is ' + format(x, '4d')
```

```text
>>> s = 'hello\nworld'
>>> print(str(s))
hello
world
>>> print(repr(s))
'hello\nworld'
>>>
```

```text
>>> x = 12.34567
>>> format(x, '0.2f')
'12.35'
>>>
```

```text
>>> f'{x:0.2f}'
'12.35'
>>>
```

```python
with open('data.txt') as file:
    for line in file:
        print(line, end='') # end='' omits the extra newline
```

```python
file = open('data.txt')
for line in file:
    print(line, end='')  # end='' omits the extra newline
file.close()
```

```python
with open('data.txt') as file:
    data = file.read()
```

```python
with open('data.txt') as file:
    while (chunk := file.read(10000)):
        print(chunk, end='')
```

```python
with open('data.txt') as file:
    while True:
        chunk = file.read(10000)
        if not chunk:
            break
        print(chunk, end='')
```

```python
with open('out.txt', 'wt') as out:
    while year <= numyears:
```

```python
principal = principal * (1 + rate)
print(f'{year:>3d} {principal:0.2f}', file=out)
year += 1
```

```python
out.write(f'{year:3d} {principal:0.2f}\n')
```

```python
with open('data.txt', encoding='latin-1') as file:
    data = file.read()
```

```python
name = input('Enter your name : ')
print('Hello', name)
```

```python
names = [ 'Dave', 'Paula', 'Thomas', 'Lewis' ]
```

```python
a = names[2] # 返回列表的第三项，'Thomas'
names[2] = 'Tom' # 将第三项改为 'Tom'
print(names[-1]) # 打印最后一项 ('Lewis')
```

```python
b = names[0:2]    # b -> ['Dave', 'Paula']
c = names[2:]    # c -> ['Aya', 'Tom', 'Lewis', 'Alex']
names[1] = 'Becky' # 用 'Becky' 替换 'Paula'
names[0:2] = ['Dave', 'Mark', 'Jeff'] # 用 ['Dave','Mark','Jeff']
                                    # 替换前两项
```

```python
a = ['x', 'y'] + ['z', 'z', 'y'] # 结果为 ['x', 'y', 'z', 'z', 'y']
```

```python
names = [] # 一个空列表
names = list() # 一个空列表
```

```python
letters = list('Dave')  # letters = ['D', 'a', 'v', 'e']
```

```python
a = [1, 'Dave', 3.14, ['Mark', 7, 9, [100, 101]], 10]
```

```python
a[1]                # 返回 'Dave'
a[3][2]            # 返回 9
a[3][3][1]        # 返回 101
```

```python
# pcost.py
# 
# 读取格式为 'NAME,SHARES,PRICE' 的输入行。
# 例如：
# 
#     SYM,123,456.78
```

```python
import sys
if len(sys.argv) != 2:
    raise SystemExit(f'Usage: {sys.argv[0]} filename')

rows = []
with open(sys.argv[1], 'rt') as file:
    for line in file:
        rows.append(line.split(','))

# rows 是如下形式的列表
# [
#     ['SYM', '123', '456.78']
#     ...
# ]

total = sum([ int(row[1]) * float(row[2]) for row in rows ])
print(f'Total cost: {total:0.2f}')
```

```python
values = []
for row in rows:
    values.append(int(row[1]) * float(row[2]))
total = sum(values)
```

```python
holding = ('GOOG', 100, 490.10)
address = ('www.python.org', 80)
```

```python
a = () # 0-元组 (空元组)
b = (item,) # 1-元组 (注意末尾的逗号)
```

```python
name, shares, price = holding
host, port = address
```

```python
# 包含格式为 "name,shares,price" 行的文件
filename = 'portfolio.csv'

portfolio = []
with open(filename) as file:
    for line in file:
        row = line.split(',')
        name = row[0]
        shares = int(row[1])
        price = float(row[2])
        holding = (name, shares, price)
        portfolio.append(holding)
```

```text
>>> portfolio[0]
('AA', 100, 32.2)
>>> portfolio[1]
('IBM', 50, 91.1)
>>>
```

```text
>>> portfolio[1][1]
50
```

```text
>>> portfolio[1][2]
91.1
>>>
```

```python
total = 0.0
for name, shares, price in portfolio:
    total += shares * price
```

```python
total = sum([shares * price for _, shares, price in portfolio])
```

```python
names1 = { 'IBM', 'MSFT', 'AA' }
names2 = set(['IBM', 'MSFT', 'HPE', 'IBM', 'CAT'])
```

```text
>>> names2
{'CAT', 'IBM', 'MSFT', 'HPE'}
>>>
```

```python
names = { s[0] for s in portfolio }
```

```python
r = set()  # 初始为空集
```



```python
a = t | s    # 并集 {'MSFT', 'CAT', 'HPE', 'AA', 'IBM'}
b = t & s    # 交集 {'IBM', 'MSFT'}
c = t - s    # 差集 { 'CAT', 'HPE' }
d = s - t    # 差集 { 'AA' }
e = t ^ s    # 对称差集 { 'CAT', 'HPE', 'AA' }
```

```python
t.add('DIS') # 添加单个元素
s.update({'JJ', 'GE', 'ACME'}) # 向 s 添加多个元素
```

```python
t.remove('IBM') # 移除 'IBM'，若不存在则抛出 KeyError。
s.discard('SCOX') # 若 'SCOX' 存在则移除。
```

```python
s = {
    'name' : 'GOOG',
    'shares' : 100,
    'price' : 490.10
}
```

```python
name = s['name']
cost = s['shares'] * s['price']
```

```python
p = prices.get('IBM', 0.0)  # 若存在则返回 prices['IBM']，否则返回 0.0
```

```python
prices = { }
prices[('IBM', '2015-02-03')] = 91.23
prices['IBM', '2015-02-04'] = 91.42   # 省略了圆括号
```

```python
portfolio = [
    ('ACME', 50, 92.34),
    ('IBM', 75, 102.25),
    ('PHP', 40, 74.50),
    ('IBM', 50, 124.75)
]

total_shares = { s[0]: 0 for s in portfolio }
for name, shares, _ in portfolio:
    total_shares[name] += shares

# total_shares = {'IBM': 125, 'ACME': 50, 'PHP': 40}
```

```python
from collections import Counter

total_shares = Counter()
for name, shares, _ in portfolio:
    total_shares[name] += shares

# total_shares = Counter({'IBM': 125, 'ACME': 50, 'PHP': 40})
```

```python
prices = {}    # 一个空字典
prices = dict() # 一个空字典
```

```python
pairs = [('IBM', 125), ('ACME', 50), ('PHP', 40)]
d = dict(pairs)
```

```python
syms = list(prices)  # syms = ['AAPL', 'MSFT', 'IBM', 'GOOG']
```

```python
>>> d = { 'x': 2, 'y':3 }
>>> k = d.keys()
>>> k
dict_keys(['x', 'y'])
>>> d['z'] = 4
>>> k
dict_keys(['x', 'y', 'z'])
>>> 
```

```python
for sym, price in prices.items():
    print(f'{sym} = {price}')
```

```python
for n in [1, 2, 3, 4, 5, 6, 7, 8, 9]:
    print(f'2 to the {n} power is {2**n}')
```

```python
for n in range(1, 10):
    print(f'2 to the {n} power is {2**n}')
```

```python
a = range(5)            # a = 0, 1, 2, 3, 4
b = range(1, 8)         # b = 1, 2, 3, 4, 5, 6, 7
c = range(0, 14, 3)     # c = 0, 3, 6, 9, 12
d = range(8, 1, -1)     # d = 8, 7, 6, 5, 4, 3, 2
```

```python
message = 'Hello World'
# 打印 message 中的每个字符
for c in message:
    print(c)
```

```python
names = ['Dave', 'Mark', 'Ann', 'Phil']
# 打印列表中的成员
for name in names:
    print(name)
```

```python
prices = { 'GOOG' : 490.10, 'IBM' : 91.50, 'AAPL' : 123.15 }
# 打印字典中的所有成员
for key in prices:
    print(key, '=', prices[key])
```

```python
# 打印文件中的所有行
with open('foo.txt') as file:
    for line in file:
        print(line, end='')
```

```python
def remainder(a, b):
    q = a // b    # // 是截断除法。
    r = a - q * b
    return r
```

```python
def remainder(a, b):
    ...
```

计算`a`除以`b`的余数。

```python
q = a // b
r = a - q * b
return r
```

```python
def remainder(a: int, b: int) -> int:
    """
    计算 a 除以 b 的余数
    """
    q = a // b
    r = a - q * b
    return r
```

```python
def divide(a, b):
    q = a // b  # 如果 a 和 b 是整数，则 q 是整数
    r = a - q * b
    return (q, r)
```

```python
quotient, remainder = divide(1456, 33)
```

```python
def connect(hostname, port, timeout=300):
    # 函数体
    ...
```

```python
connect('www.python.org', 80)
connect('www.python.org', 80, 500)
```

```python
connect('www.python.org', 80, timeout=500)
```

```python
connect(port=80, hostname='www.python.org')
```

```python
debug = True  # 全局变量

def read_data(filename):
    if debug:
        print('Reading', filename)
    ...
```

```python
Traceback (most recent call last):
  File "readport.py", line 9, in <module>
    shares = int(row[1])
ValueError: invalid literal for int() with base 10: 'N/A'
```

```python
portfolio = []
with open('portfolio.csv') as file:
    for line in file:
        row = line.split(',')
        try:
            name = row[0]
            shares = int(row[1])
            price = float(row[2])
            holding = (name, shares, price)
            portfolio.append(holding)
        except ValueError as err:
```

```python
print('Bad row:', row)
print('Reason:', err)
```

```python
raise RuntimeError('Computer says no')
```

```python
import threading
lock = threading.Lock()
...
lock.acquire()
# If a lock has been acquired, it MUST be released
try:
    ...
    statements
    ...
finally:
    lock.release()    # Always runs
```

```python
raise SystemExit()               # Exit with no error message
raise SystemExit("Something is wrong") # Exit with error
```

```python
import atexit

# Example
connection = open_connection("deaddot.com")

def cleanup():
    print "Going away..."
    close_connection(connection)

atexit.register(cleanup)
```

```python
items = [37, 42] # Create a list object
items.append(73) # Call the append() method
```

```python
>>> items = [37, 42]
>>> dir(items)
['_add_', '_class_', '_contains_', '_delattr_', '_delitem_',
...
'append', 'count', 'extend', 'index', 'insert', 'pop',
'remove', 'reverse', 'sort']
>>>
```

```python
class Stack:
    def __init__(self):
        # Initialize the stack
        self._items = [ ]

    def push(self, item):
        self._items.append(item)

    def pop(self):
        return self._items.pop()

    def __repr__(self):
        return f'<{type(self).__name__} at 0x{id(self):x}, size={len(self)}>'

    def __len__(self):
        return len(self._items)
```

```python
s = Stack() # Create a stack
s.push('Dave') # Push some things onto it
s.push(42)
s.push([3, 4, 5])
x = s.pop() # x gets [3,4,5]
y = s.pop() # y gets 42
```

```python
>>> s = Stack()
>>> s.push('Dave')
>>> s.push(42)
>>> len(s)
2
>>> s
<Stack at 0x101c08c1d0, size=2>
>>>
```

```python
class MyStack(Stack):
    def swap(self):
        a = self.pop()
        b = self.pop()
        self.push(a)
        self.push(b)
```

```python
class NumericStack(Stack):
    def push(self, item):
        if not isinstance(item, (int, float)):
            raise TypeError('Expected an int or float')
        super().push(item)
```

```python
>>> s = NumericStack()
>>> s.push(42)
>>> s.push('Dave')
Traceback (most recent call last):
  ...
TypeError: Expected an int or float
>>>
```

```python
class Calculator:
    def __init__(self):
        self._stack = Stack()

    def push(self, item):
        self._stack.push(item)

    def pop(self):
        return self._stack.pop()

    def add(self):
        self.push(self.pop() + self.pop())

    def mul(self):
        self.push(self.pop() * self.pop())

    def sub(self):
        right = self.pop()
        self.push(self.pop() - right)

    def div(self):
        right = self.pop()
        self.push(self.pop() / right)
```

```python
# readport.py
#
# Reads a file of 'NAME,SHARES,PRICE' data

def read_portfolio(filename):
    portfolio = []
    with open(filename) as file:
        for line in file:
            row = line.split(',')
            try:
                name = row[0]
                shares = int(row[1])
                price = float(row[2])
                holding = (name, shares, price)
                portfolio.append(holding)
            except ValueError as err:
                print('Bad row:', row)
                print('Reason:', err)
    return portfolio
```

```python
# pcost.py

import readport

def portfolio_cost(filename):
    """
    Compute the total shares*price of a portfolio
    """
    port = readport.read_portfolio(filename)
    return sum(shares * price for _, shares, price in port)
```

```python
import readport as rp
port = rp.read_portfolio('portfolio.dat')
```

```python
from readport import read_portfolio
port = read_portfolio('portfolio.dat')
```

```python
>>> import readport
>>> dir(readport)
['__builtins__', '__cached__', '__doc__', '__file__', '__loader__', 
 '__name__', '__package__', '__spec__', 'read_portfolio']
...
>>>
```



```python
# readport.py
#
# Reads a file of 'NAME,SHARES,PRICE' data

import csv

def read_portfolio(filename):
    portfolio = []
    with open(filename) as file:
        rows = csv.reader(file)
        for row in rows:
            try:
                name = row[0]
                shares = int(row[1])
                price = float(row[2])
                holding = (name, shares, price)
                portfolio.append(holding)
            except ValueError as err:
                print('Bad row:', row)
                print('Reason:', err)
    return portfolio
```

```python
# readport.py
#
# Reads a file of 'NAME,SHARES,PRICE' data

import csv

def read_portfolio(filename):
    ...

def main():
    portfolio = read_portfolio('portfolio.csv')
    for name, shares, price in portfolio:
        print(f'{name:>10s} {shares:10d} {price:10.2f}')

if __name__ == '__main__':
    main()
```

```python
def main(argv):
    if len(argv) == 1:
        filename = input('Enter filename: ')
    elif len(argv) == 2:
        filename = argv[1]
    else:
        raise SystemExit(f'Usage: {argv[0]} [ filename ]')
    portfolio = read_portfolio(filename)
    for name, shares, price in portfolio:
        print(f'{name:>10s} {shares:10d} {price:10.2f}')

if __name__ == '__main__':
    import sys
    main(sys.argv)
```

```bash
% python readport.py
Enter filename: portfolio.csv
...
% python readport.py portfolio.csv
...
% python readport.py a b c
Usage: readport.py [ filename ]
%
```

```python
import tutorial.readport

port = tutorial.readport.read_portfolio('portfolio.dat')
```

```python
from tutorial.readport import read_portfolio

port = read_portfolio('portfolio.dat')
```

```python
# pcost.py
from tutorial import readport
...
```

```
tutorial-project/
tutorial/
    __init__.py
    readport.py
    pcost.py
    stack.py
    ...
tests/
    test_stack.py
    test_pcost.py
    ...
    . . .
examples/
    sample.py
    ...
doc/
    tutorial.txt
    ...
```

```bash
% python3 -m pip install somepackage
```

```python
>>> import pandas
>>> pandas.__file__
'/usr/local/lib/python3.8/site-packages/pandas/__init__.py'
>>>
```

```bash
% python3 -m venv myproject
```

```bash
% ./myproject/bin/python3 -m pip install somepackage
```

```python
42                 # Decimal integer
0b101010          # Binary integer
0o52               # Octal integer
0x2a               # Hexadecimal integer
```

```python
(1, 2, 3)               # tuple
[1, 2, 3]               # list
{1, 2, 3}               # set
{'x':1, 'y':2, 'z':3}   # dict
```

`value = 2 + 3 * 5 + sqrt(6+7)`

```
value = a + b[1] + c['key']
```

```python
while line=file.readline():
    print(line)
```

## 语法错误 (Syntax Error)

```python
while (line:=file.readline()):
    print(line)
```

```python
[1, 2, 3] + [4, 5] # [1, 2, 3, 4, 5]
[1, 2, 3] * 4       # [1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 3]
'%s has %d messages' % ('Dave', 37)
```

```python
>>> from fractions import Fraction
>>> a = Fraction(2, 3)
>>> b = 5
>>> a + b
Fraction(17, 3)
>>>
```

```python
>>> from decimal import Decimal
>>> from fractions import Fraction
>>> a = Fraction(2, 3)
>>> b = Decimal('5')
>>> a + b
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'Fraction' and 'decimal.Decimal'
>>>
```

```python
a = 3
a = a + 1  # a = 4
a += 1       # a = 5
```

```python
>>> a = [1, 2, 3]
>>> b = a            # Creates a new reference to a
>>> a += [4, 5]     # In-place update (doesn't create a new list)
>>> a
[1, 2, 3, 4, 5]
>>> b
[1, 2, 3, 4, 5]
>>>
```

```python
if y != 0:
    result = x / y
else:
    result = 0
```

## 替代方案

```python
result = y and x / y
```

```python
def f(x, items=None):
    if not items:
        items = []
    items.append(x)
    return items
```

```
>>> a = []
>>> foo(3, a)
[3]
>>> a                # 注意 a 并没有更新
[]
>>>
```

```python
def f(x, items=None):
    if items is None:
        items = []
    items.append(x)
    return items
```

```python
minvalue = a if a <= b else b
```

```python
items = [ 3, 4, 5 ]
x, y, z = items    # x = 3, y = 4, z = 5
```

```python
letters = "abc"
x, y, z = letters    # x = 'a', y = 'b', z = 'c'
```

```python
items = [3, 4, 5]
d = { }
d['x'], d['y'], d['z'] = items
```

```python
datetime = ((5, 19, 2008), (10, 30, "am"))
(month, day, year), (hour, minute, am_pm) = datetime
```

```python
(_, day, _), (hour, _, _) = datetime
```

```python
items = [1, 2, 3, 4, 5]
a, b, *extra = items    # a = 1, b = 2, extra = [3,4,5]
*extra, a, b            # extra = [1,2,3], a = 4, b = 5
a, *extra, b            # a = 1, extra = [2,3,4], b = 5
```

```python
datetime = ((5, 19, 2008), (10, 30, "am"))

(month, *_), (hour, *_) = datetime
```

```python
items = [1, 2, 3]
a = [10, *items, 11]  # a = [10, 1, 2, 3, 11]  (列表)
b = (*items, 10, *items)  # b = [1, 2, 3, 10, 1, 2, 3]  (元组)
c = {10, 11, *items}  # c = {1, 2, 3, 10, 11}  (集合)
```

```python
>>> a = [3, 4, 5]
>>> b = [a]
>>> c = 4 * b
>>> c
[[3, 4, 5], [3, 4, 5], [3, 4, 5], [3, 4, 5]]
>>> a[0] = -7
>>> c
[[-7, 4, 5], [-7, 4, 5], [-7, 4, 5], [-7, 4, 5]]
>>>
```

```python
a = [ 3, 4, 5 ]
c = [list(a) for _ in range(4)] # list() 创建列表的副本
```

```python
a = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```python
a[2:5]    # [2, 3, 4]
a[:3]      # [0, 1, 2]
a[-3:]     # [7, 8, 9]
a[::2]     # [0, 2, 4, 6, 8 ]
a[::-2]     # [9, 7, 5, 3, 1 ]
a[0:5:2]   # [0, 2, 4]
a[5:0:-2]  # [5, 3, 1]
```

```python
a[:5:1]    # [0, 1, 2, 3, 4]
a[:5:-1]   # [9, 8, 7, 6]
a[5::1]    # [5, 6, 7, 8, 9]
a[5::-1]  # [5, 4, 3, 2, 1, 0]
a[5:0:-1] # [5, 4, 3, 2, 1]
```

```python
firstfive = slice(0, 5)
s = 'hello world'
print(s[firstfive])    # 打印 'hello'
```

```python
a = [1, 2, 3, 4, 5]
a[1] = 6             # a = [1, 6, 3, 4, 5]
a[2:4] = [10, 11]    # a = [1, 6, 10, 11, 5]
a[3:4] = [-1, -2, -3] # a = [1, 6, 10, -1, -2, -3, 5]
a[2:] = [0]          # a = [1, 6, 0]
```

```python
a = [1, 2, 3, 4, 5]
a[1::2] = [10, 11]    # a = [1, 10, 3, 11, 5]
a[1::2] = [30, 40, 50] # ValueError. 左侧切片中仅有两个元素。
```

```python
>>> a = {'a', 'b', 'c' }
>>> b = {'c', 'd'}
>>> a | b
{'a', 'b', 'c', 'd'}
>>> a & b
{'c' }
>>> a - b
{'a', 'b'}
>>> b - a
{'d'}
```

```python
>>> a ^ b
{'a', 'b', 'd'}
>>>
```

```python
>>> a = { 'x': 1, 'y': 2, 'z': 3 }
>>> b = { 'z': 3, 'w': 4, 'q': 5 }
>>> a.keys() & b.keys()
{ 'z' }
>>>
```

```python
nums = [1, 2, 3, 4, 5]
squares = []
for n in nums:
    nums.append(n * n)
```

```python
nums = [1, 2, 3, 4, 5]
squares = [n * n for n in nums]
```

```python
squares = [n * n for n in nums if n > 2]  # [9, 16, 25]
```

```python
[expression for item1 in iterable1 if condition1
            for item2 in iterable2 if condition2
            ...
            for itemN in iterableN if conditionN ]
```

```python
result = []
for item1 in iterable1:
    if condition1:
        for item2 in iterable2:
            if condition2:
                ...
                for itemN in iterableN:
                    if conditionN:
                        result.append(expression)
```

```python
# 某些数据（字典列表）
portfolio = [
    {'name': 'IBM', 'shares': 100, 'price': 91.1 },
    {'name': 'MSFT', 'shares': 50, 'price': 45.67 },
    {'name': 'HPE', 'shares': 75, 'price': 34.51 },
    {'name': 'CAT', 'shares': 60, 'price': 67.89 },
    {'name': 'IBM', 'shares': 200, 'price': 95.25 }
]

# 收集所有名称 ['IBM', 'MSFT', 'HPE', 'CAT', 'IBM']
names = [s['name'] for s in portfolio]

# 查找所有持股超过 100 的条目 ['IBM']
more100 = [s['name'] for s in portfolio if s['shares'] > 100 ]

# 计算总成本 (持股数 * 价格)
cost = sum([s['shares']*s['price'] for s in portfolio])

# 收集 (名称, 持股数) 元组
name_shares = [ (s['name'], s['shares']) for s in portfolio ]
```

```python
>>> x = 42
>>> squares = [x*x for x in [1,2,3]]
>>> squares
[1, 4, 9]
>>> x
42
>>>
```

```python
# 集合推导式
names = { s['name'] for s in portfolio }
# names = { 'IBM', 'MSFT', 'HPE', 'CAT' }
```



```python
prices = { s['name']:s['price'] for s in portfolio }
# prices = { 'IBM': 95.25, 'MSFT': 45.67, 'HPE': 34.51, 'CAT': 67.89 }
```

```python
def toint(x):
    try:
        return int(x)
    except ValueError:
        return None

values = [ '1', '2', '-4', 'n/a', '-3', '5' ]
data1 = [ toint(x) for x in values ]
# data1 = [1, 2, -4, None, -3, 5]

data2 = [ toint(x) for x in values if toint(x) is not None ]
# data2 = [1, 2, -4, -3, 5]
```

```python
data3 = [ v for x in values if (v:=toint(x)) is not None ]
# data3 = [ 1, 2, -4, -3, 5 ]

data4 = [ v for x in values if (v:=toint(x)) is not None and v >= 0 ]
# data4 = [ 1, 2, 5 ]
```

```python
nums = [1, 2, 3, 4]
squares = (x*x for x in nums)
```

```python
>>> squares
<generator object at 0x590a8>
>>> next(squares)
```

```python
1
>>> next(squares)
4
...
>>> for n in squares:
....    print(n)
9
16
>>>
```

```python
# 读取文件
f = open('data.txt')                # 打开文件
lines = (t.strip() for t in f)     # 读取行，去除
                                  # 首尾空白字符
comments = (t for t in lines if t[0] == '#') # 所有注释
for c in comments:
    print(c)
```

```python
sum((x*x for x in values))
sum(x*x for x in values)    # 删除了多余的括号
```

```python
>>> a = 10
>>> a <= 10 and 1 < a
True
>>> a <= 10 & 1 < a
False
>>>
```

```python
>>> (a <= 10) & (1 < a)
True
>>>
```

```python
if debug:
    def square(x):
        if not isinstance(x,float):
            raise TypeError('Expected a float')
        return x * x
else:
    def square(x):
        return x * x
```

```python
if expression:
    pass  # 待办：请实现
else:
    statements
```

```python
s = [ (1, 2, 3), (4, 5, 6) ]

for x, y, z in s:
    statements
```

```python
s = [ (1, 2), (3, 4, 5), (6, 7, 8, 9) ]

for x, y, *extra in s:
    statements
```

```python
# x = 1, y = 2, extra = []
# x = 3, y = 4, extra = [5]
# x = 6, y = 7, extra = [8, 9]
# ...
```

```python
for i, x in enumerate(s, start=100):
    statements
```

```python
# s 和 t 是两个序列
i = 0
while i < len(s) and i < len(t):
    x = s[i]  # 从 s 中取一项
    y = t[i]  # 从 t 中取一项
    statements
    i += 1
```

```python
# s 和 t 是两个序列
for x, y in zip(s, t):
    statements
```

```python
with open('foo.txt') as file:
    for line in file:
        stripped = line.strip()
        if not stripped:
            break    # 空行，停止读取
        # 处理去除空白后的行
        ...
```

```python
with open('foo.txt') as file:
    for line in file:
        stripped = line.strip()
        if not stripped:
            continue    # 跳过空行
        # 处理去除空白后的行
        ...
```

```python
# for-else
with open('foo.txt') as file:
    for line in file:
        stripped = line.strip()
        if not stripped:
            break
        # 处理去除空白后的行
        ...
else:
    raise RuntimeError('Missing section separator')
```

```python
found_separator = False

with open('foo.txt') as file:
    for line in file:
        stripped = line.strip()
        if not stripped:
            found_separator = True
            break
        # process the stripped line
        ...

if not found_separator:
    raise RuntimeError('Missing section separator')
```

```python
raise RuntimeError('Unrecoverable Error')
```

```python
try:
    file = open('foo.txt', 'rt')
except FileNotFoundError as e:
    statements
```

```python
try:
    file = open('foo.txt', 'rt')
except FileNotFoundError:
    print("Well, that didn't work.")
    raise # Reraises current exception
```

```python
try:
    int('N/A') # Raises ValueError
except ValueError as e:
    print('Failed:', e)

print(e) # Fails -> NameError. 'e' not defined.
```

```python
try:
    do something
except TypeError as e:
    # Handle Type error
    ...
except ValueError as e:
    # Handle Value error
    ...
```

```python
try:
    do something
except (TypeError, ValueError) as e:
    # Handle Type or Value errors
    ...
```

```python
try:
    do something
except ValueError:
    pass # Do nothing (shrug)
```

```python
try:
    do something
except Exception as e:
    print(f'An error occurred : {e!r}')
```

```python
try:
    file = open('foo.txt', 'rt')
except FileNotFoundError as e:
    print(f'Unable to open foo : {e}')
    data = ''
else:
    data = file.read()
    file.close()
```

```python
file = open('foo.txt', 'rt')
try:
    # Do some stuff
    ...
finally:
    file.close()
    # File closed regardless of what happened
```

```python
try:
    item = items[index]
except IndexError:    # Raised if items is a sequence
    ...
except KeyError:       # Raised if items is a mapping
    ...
```

```python
try:
    item = items[index]
except LookupError:
    ...
```

```python
import sys

if len(sys.argv) != 2:
    raise SystemExit(f'Usage: {sys.argv[0]} filename')

filename = sys.argv[1]
```

```python
class NetworkError(Exception):
    pass
```

```python
raise NetworkError('Cannot find host')
```

```python
class DeviceError(Exception):
    def __init__(self, errno, msg):
        self.args = (errno, msg)
        self.errno = errno
        self.errmsg = msg

# Raises an exception (multiple arguments)
raise DeviceError(1, 'Not Responding')
```

```python
class HostnameError(NetworkError):
    pass

class TimeoutError(NetworkError):
    pass

def error1():
    raise HostnameError('Unknown host')

def error2():
    raise TimeoutError('Timed out')

try:
    error1()
except NetworkError as e:
    if type(e) is HostnameError:
        # Perform special actions for this kind of error
        ...
```

```python
class ApplicationError(Exception):
    pass

def do_something():
    x = int('N/A')  # raises ValueError

def spam():
    try:
        do_something()
    except Exception as e:
        raise ApplicationError('It failed') from e
```

```
>>> spam()
Traceback (most recent call last):
  File "c.py", line 9, in spam
    do_something()
  File "c.py", line 5, in do_something
    x = int('N/A')
ValueError: invalid literal for int() with base 10: 'N/A'

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "c.py", line 11, in spam
    raise ApplicationError('It failed') from e
__main__.ApplicationError: It failed
>>>
```

```python
try:
    spam()
except ApplicationError as e:
    print('It failed. Reason:', e.__cause__)
```

```python
def spam():
    try:
        do_something()
    except Exception as e:
        raise ApplicationError('It failed') from None
```

```python
def spam():
    try:
        do_something()
    except Exception as e:
        print('It failed:', err)  # err undefined (typo)
```

```
>>> spam()
Traceback (most recent call last):
  File "d.py", line 9, in spam
    do_something()
  File "d.py", line 5, in do_something
    x = int('N/A')
ValueError: invalid literal for int() with base 10: 'N/A'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "d.py", line 11, in spam
    print('It failed. Reason:', err)
NameError: name 'err' is not defined
>>>
```

```python
try:
    spam()
except Exception as e:
    print('It failed. Reason:', e)
    if e.__context__:
        print('While handling:', e.__context__)
```

```python
try:
    do_something()
except Exception as e:
    raise ApplicationError('It failed') from e
```

```python
try:
    do_something()
except Exception as e:
    print('It failed:', err)  # err undefined
```

```python
import traceback

try:
    spam()
except Exception as e:
    tblines = traceback.format_exception(type(e), e, e.__tracebacktrace__)
    tbmsg = ''.join(tblines)
    print('It failed:')
    print(tbmsg)
```

```python
def read_data(filename):
    with open(filename, 'rt') as file:
        rows = []
        for line in file:
            row = line.split()
            rows.append((row[0], int(row[1]), float(row[2])))
    return rows
```



```python
def read_data(filename):
    with open(filename, 'rt') as file:
        rows = []
        for line in file:
            row = line.split()
            try:
                rows.append((row[0], int(row[1]), float(row[2])))
            except ValueError as e:
                print('Bad row:', row)
                print('Reason:', e)
    return rows
```

```python
class ApplicationError(Exception):
    pass

class UnauthorizedUserError(ApplicationError):
    pass

def spam():
    ...
    raise UnauthorizedUserError('Go away')
    ...
```

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

```python
class ListTransaction:
    def __init__(self,thelist):
        self.thelist = thelist

    def __enter__(self):
        self.workingcopy = list(self.thelist)
        return self.workingcopy

    def __exit__(self, type, value, tb):
        if type is None:
            self.thelist[:] = self.workingcopy
        return False
```

```python
items = [1,2,3]

with ListTransaction(items) as working:
    working.append(4)
    working.append(5)
print(items) # Produces [1,2,3,4,5]

try:
    with ListTransaction(items) as working:
        working.append(6)
        working.append(7)
        raise RuntimeError("We're hosed!")
except RuntimeError:
    pass

print(items)  # Produces [1,2,3,4,5]
```

```python
def write_data(file, data):
    assert file, 'write_data: file not defined!'
    ...
```

```python
def factorial(n):
    result = 1
    while n > 1:
        result *= n
        n -= 1
    return result

assert factorial(5) == 120
```

```python
def factorial(n):
    assert n > 0, "must supply a positive value"
    result = 1
    while n > 1:
        result *= n
        n -= 1
    return result
```

```python
a = 34                 # 创建一个整数
n = a.numerator       # 获取分子（一个属性）

b = [1, 2, 3]         # 创建一个列表
b.append(7)           # 使用 append 方法添加一个新元素
```

```python
c = a + 10    # c = 34 + 10
d = b + [4, 5] # d = [1, 2, 3, 7, 4, 5]
```

```python
# 比较两个对象
def compare(a, b):
    if a is b:
        print('same object') # 相同对象
    if a == b:
        print('same value')   # 相同值
    if type(a) is type(b):
        print('same type')    # 相同类型
```

```python
items = list()

if isinstance(items, list):
    items.append(item)
```

```python
def removeall(items: list, item) -> list:
    return [i for i in items if i != item]
```

```python
class mylist(list):
    def removeall(self, val):
        return [i for i in self if i != val]

# 示例
items = mylist([5, 8, 2, 7, 2, 13, 9])
x = items.removeall(2)
print(x)  # [5, 8, 7, 13, 9]
```

```python
if isinstance(items, (list, tuple)):
    maxval = max(items)
```

```python
a = 37          # 创建一个值为 37 的对象
b = a           # 增加 37 的引用计数
c = []
c.append(b)    # 增加 37 的引用计数
```

```python
del a # 减少 37 的引用计数
b = 42 # 减少 37 的引用计数
c[0] = 2.0 # 减少 37 的引用计数
```

```python
a = { }
b = { }
a['b'] = b  # a 包含对 b 的引用
b['a'] = a  # b 包含对 a 的引用
del a
del b
```

```python
def some_calculation():
    data = create_giant_data_structure()
    # 在计算的某个部分使用 data
    ...
    # 释放数据
    del data

    # 计算继续
    ...
```

```python
>>> a = [1,2,3,4]
>>> b = a               # b 是对 a 的引用
>>> b is a
True
>>> b[2] = -100        # 修改 b 中的一个元素
>>> a                  # 注意 a 也随之改变了
[1, 2, -100, 4]
>>>
```

```python
>>> a = [ 1, 2, [3,4] ]
>>> b = list(a)            # 创建 a 的浅拷贝
>>> b is a
False
```

```python
>>> b.append(100) # 向 b 添加元素
>>> b
[1, 2, [3, 4], 100]
>>> a # 注意 a 没有改变
[1, 2, [3, 4]]
>>> b[2][0] = -100 # 修改 b 内部的一个元素
>>> b
[1, 2, [-100, 4], 100]
>>> a # 注意 a 内部也发生了改变
[1, 2, [-100, 4]]
>>>
```

```python
>>> import copy
>>> a = [1, 2, [3, 4]]
>>> b = copy.deepcopy(a)
>>> b[2][0] = -100
>>> b
[1, 2, [-100, 4]]
>>> a                      # 注意 a 没有改变
[1, 2, [3, 4]]
>>> 
```

```python
>>> from datetime import date
>>> d = date(2012, 12, 21)
>>> print(d)
2012-12-21
>>> str(d)
'2012-12-21'
>>>
```

```python
>>> d = date(2012, 12, 21)
>>> repr(d)
'datetime.date(2012, 12, 21)'
>>> print(repr(d))
datetime.date(2012, 12, 21)
>>> print(f'The date is: {d!r}')
The date is: datetime.date(2012, 12, 21)
>>>
```

```python
items = {
    'number' : 42,
    'text' : "Hello World"
}
```

```python
items['func'] = abs          # 添加 abs() 函数
import math
items['mod'] = math           # 添加一个模块
items['error'] = ValueError  # 添加一个异常类型
nums = [1,2,3,4]
items['append'] = nums.append # 添加另一个对象的方法
```

```python
>>> items['func'](-45)            # 执行 abs(-45)
45
>>> items['mod'].sqrt(4)           # 执行 math.sqrt(4)
2.0
>>> try:
...     x = int('a lot')
... except items['error'] as e:    # 等同于: except ValueError as e
...     print("Couldn't convert")
... 
Couldn't convert
>>> items['append'](100)           # 执行 nums.append(100)
>>> nums
[1, 2, 3, 4, 100]
>>>
```

```python
>>> line = 'ACME,100,490.10'
>>> column_types = [str, int, float]
>>> parts = line.split(',')
>>> row = [ty(val) for ty, val in zip(column_types, parts)]
>>> row
['ACME', 100, 490.1]
>>>
```

```python
if format == 'text':
    formatter = TextFormatter()
elif format == 'csv':
    formatter = CSVFormatter()
elif format == 'html':
    formatter = HTMLFormatter()
else:
    raise RuntimeError('Bad format')
```

```python
_formats = {
    'text': TextFormatter,
    'csv': CSVFormatter,
    'html': HTMLFormatter
}

if format in _formats:
    formatter = _formats[format]()
else:
    raise RuntimeError('Bad format')
```

```python
def compute_cost(unit_price, num_units):
    return unit_price * num_units
```

```python
>>> compute_cost(1.25, 50)
62.5
>>>
```

```python
>>> from fractions import Fraction
>>> compute_cost(Fraction(5, 4), 50)
Fraction(125, 2)
>>> from decimal import Decimal
>>> compute_cost(Decimal('1.25'), Decimal('50'))
Decimal('62.50')
>>>
```

```python
>>> import numpy as np
>>> prices = np.array([1.25, 2.10, 3.05])
>>> units = np.array([50, 20, 25])
>>> compute_cost(prices, units)
array([62.5 , 42. , 76.25])
>>>
```

```python
>>> compute_cost('a lot', 10)
'a lota lota lota lota lota lota lota lota lot'
>>>
```

```python
>>> compute_cost(Fraction(5, 4), Decimal('50'))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in compute_cost
TypeError: unsupported operand type(s) for *: 'Fraction' and 'decimal.Decimal'
>>>
```

```python
x = SomeClass.__new__(SomeClass, args)
if isinstance(x, SomeClass):
    x.__init__(args)
```

```python
a = [2, 3, 4, 5]  # 创建一个列表
s = repr(a)       # s = '[2, 3, 4, 5]'
b = eval(s)       # 将 s 转换回列表
```

```python
f = open('foo.txt')
a = repr(f)
# a = '<_io.TextIOWrapper name=\'foo.txt\' mode=\'r\' encoding=\'UTF-8\'>
```

```python
>>> a = 42           # int
>>> b = 3.7          # float
>>> a.__add__(b)
NotImplemented
```

```python
>>> b.__radd__(a)
45.7
>>>
```

```python
>>> True or 1/0    # 不会对 1/0 进行求值
True
>>>
```

```python
if a:             # 执行 a.__bool__()
    ...
else:
    ...
```

```python
>>> a = 42        # int
>>> b = 52.3      # float
>>> a.__lt__(b)
NotImplemented
```

```python
>>> b.__gt__(a)
True
>>>
```

```python
f'{x:spec}'                   # 调用 x.__format__('spec')
format(x, 'spec')            # 调用 x.__format__('spec')
'x is {0:spec}'.format(x)    # 调用 x.__format__('spec')
```

```python
a = [1, 2, 3, 4, 5, 6]
len(a)                # a.__len__()
x = a[2]             # x = a.__getitem__(2)
a[1] = 7             # a.__setitem__(1, 7)
del a[2]             # a.__delitem__(2)
5 in a               # a.__contains__(5)
```



```python
a = [1,2,3,4,5,6]
x = a[1:5]                # x = a.__getitem__(slice(1, 5, None))
a[1:3] = [10,11,12]        # a.__setitem__(slice(1, 3, None), [10, 11, 12])
del a[1:4]                # a.__delitem__(slice(1, 4, None))
```

```python
a = m[0:100:10]        # 步进切片 (步长=10)
b = m[1:10, 3:20]     # 多维切片
c = m[0:100:10, 50:75:5] # 带有步长的多维切片
m[0:5, 5:10] = n      # 扩展切片赋值
del m[:10, 15:]       # 扩展切片删除
```

```python
a = m[..., 10:20]  # 使用 Ellipsis 的扩展切片访问
m[10:20, ...] = n
```

```python
a = m[0:10, 0:100:5, ...]
```

```python
a = m.__getitem__((slice(0,10,None), slice(0,100,5), Ellipsis))
```

```python
_iter = s.__iter__()
while True:
    try:
        x = _iter.__next__()
    except StopIteration:
        break
    # 执行 for 循环体内的语句
    ...
```

```python
>>> for x in reversed([1,2,3]):
...     print(x)
3
2
1
>>>
```

```python
class FRange:
    def __init__(self, start, stop, step):
        self.start = start
        self.stop = stop
        self.step = step

    def __iter__(self):
        x = self.start
        while x < self.stop:
            yield x
            x += self.step

# 示例用法：
```

```python
nums = FRange(0.0, 1.0, 0.1)
for x in nums:
    print(x) # 0.0, 0.1, 0.2, 0.3, ...
```

```python
def split(line, delimiter=','):
    statements
```

```python
def func(x, items=[]):
    items.append(x)
    return items

func(1) # returns [1]
func(2) # returns [1, 2]
func(3) # returns [1, 2, 3]
```

```python
def func(x, items=None):
    if items is None:
        items = []
    items.append(x)
    return items
```

```python
def product(first, *args):
    result = first
    for x in args:
        result = result * x
    return result

product(10, 20)  # -> 200
product(2, 3, 4, 5)  # -> 120
```

```python
def func(w, x, y, z):
    statements

# Keyword argument invocation
func(x=3, y=22, w='hello', z=[1, 2])
```

```python
func('hello', 3, z=[1, 2], y=22)
func(3, 22, w='hello', z=[1, 2])  # TypeError. Multiple values for w
```

```python
def read_data(filename, *, debug=False):
    ...
```

```python
def product(first, *values, scale=1):
    result = first * scale
    for val in values:
        result = result * val
    return result
```

```python
data = read_data('Data.csv', True) # NO. TypeError
data = read_data('Data.csv', debug=True) # Yes.
```

```python
result = product(2, 3, 4)        # Result = 24
result = product(2, 3, 4, scale=10) # Result = 240
```

```python
def make_table(data, **parms):
    # Get configuration parameters from parms (a dict)
    fgcolor = parms.pop('fgcolor', 'black')
    bgcolor = parms.pop('bgcolor', 'white')
    width = parms.pop('width', None)
    ...
    # No more options
    if parms:
        raise TypeError(f'Unsupported configuration options {list(parms)}')

make_table(items, fgcolor='black', bgcolor='white', border=1,
            borderstyle='grooved', cellpadding=10,
            width=400)
```

```python
# Accept variable number of positional or keyword arguments
def func(*args, **kwargs):
    # args is a tuple of positional args
    # kwargs is dictionary of keyword args
    ...
```

```python
def parse_lines(lines, separator=',', types=(), debug=False):
    for line in lines:
        ...
        statements
        ...
```

```python
def parse_file(filename, *args, **kwargs):
    with open(filename, 'rt') as file:
        return parse_lines(file, *args, **kwargs)
```

```python
import time

def after(seconds, func, /, *args, **kwargs):
    time.sleep(seconds)
    return func(*args, **kwargs)
```

```python
def duration(*, seconds, minutes, hours):
    return seconds + 60 * minutes + 3600 * hours

after(5, duration, seconds=20, minutes=3, hours=2)
```

```python
def factorial(n):
    """
    Computes n factorial. For example:

    >>> factorial(6)
    120
    >>>
    """
    if n <= 1:
        return 1
    else:
        return n*factorial(n-1)
```

```python
def factorial(n: int) -> int:
    if n <= 1:
        return 1
    else:
        return n * factorial(n - 1)
```

```python
def factorial(n:int) -> int:
    result: int = 1          # Type-hinted local variable
    while n > 1:
        result *= n
        n -= 1
    return result
```

```python
def square(items):
    for i, x in enumerate(items):
        items[i] = x * x  # Modify items in-place
```

```python
a = [1, 2, 3, 4, 5]
square(a)  # Changes a to [1, 4, 9, 16, 25]
```

```python
def sum_squares(items):
    items = [x*x for x in items] # Reassign "items" name
    return sum(items)

a = [1, 2, 3, 4, 5]
result = sum_squares(a)
print(a) # [1, 2, 3, 4, 5] (Unchanged)
```

```python
>>> items = [10, 3, 2, 9, 5]
>>> items.sort()                # Observe: no return value
>>> items
[2, 3, 5, 9, 10]
>>>
```

```python
def func(x, y, z):
    ...

s = (1, 2, 3)
```

```python
# Pass a sequence as arguments
result = func(*s)
```

```python
# Pass a mapping as keyword arguments
d = { 'x':1, 'y':2, 'z':3 }
result = func(**d)
```

```python
def parse_value(text):
    """
    Split text of the form name=val into (name, val)
    """
    parts = text.split('=', 1)
    return (parts[0].strip(), parts[1].strip())
```

```python
name, value = parse_value('url=http://www.python.org')
```

```python
from typing import NamedTuple

class ParseResult(NamedTuple):
    name: str
    value: str

def parse_value(text):
    """
    Split text of the form name=val into (name, val)
    """
    parts = text.split('=', 1)
    return ParseResult(parts[0].strip(), parts[1].strip())
```

```python
r = parse_value('url=http://www.python.org')
print(r.name, r.value)
```

```python
def parse_value(text):
    parts = text.split('=', 1)
    if len(parts) == 2:
        return ParseResult(parts[0].strip(), parts[1].strip())
    else:
        return None
```

```python
result = parse_value(text)
if result:
    name, value = result
```

```python
if result := parse_value(text):
    name, value = result
```

```python
def parse_value(text):
    parts = text.split('=', 1)
    if len(parts) == 2:
        return ParseResult(parts[0].strip(), parts[1].strip())
    else:
        raise ValueError('Bad value')
```

```python
try:
    name, value = parse_value(text)
    ...
except ValueError:
    ...
```

```python
def func(x):
    if x > 0:
        y = 42
    return x + y  # y not assigned if conditional is false

func(10)    # Returns 52
func(-10)   # UnboundLocalError: y referenced before assignment
```

```python
def func():
    n += 1  # Error: UnboundLocalError
```

```python
x = 42
def func():
    print(x) # Fails. UnboundLocalError
    x = 13

func()
```

```python
x = 42

def func():
    x = 13

func()
# x is still 42
```

```python
x = 42
y = 37
def func():
    global x   # 'x' is in global namespace
    x = 13
    y = 0
func()
# x is now 13. y is still 37.
```

```python
def countdown(start):
    n = start
    def display():          # Nested function definition
        print('T-minus', n)
    while n > 0:
        display()
        n -= 1
```

```python
def countdown(start):
    n = start
    def display():
        print('T-minus', n)
    def decrement():
        n -= 1 # Fails: UnboundLocalError
    while n > 0:
        display()
        decrement()
```

```python
def countdown(start):
    n = start
    def display():
        print('T-minus', n)
    def decrement():
        nonlocal n
        n -= 1 # Modifies the outer n
    while n > 0:
        display()
        decrement()
```

```python
def sumn(n):
    if n == 0:
        return 0
    else:
        return n + sumn(n-1)
```

`lambda` 参数: 表达式

```python
a = lambda x, y: x + y
r = a(2, 3)  # r 得到 5
```

```python
# 根据唯一字母的数量对单词列表进行排序
result = sorted(words, key=lambda word: len(set(word)))
```

```python
x = 2
f = lambda y: x * y
x = 3
g = lambda y: x * y
print(f(10)) # --> prints 30
print(g(10)) # --> prints 30
```

```python
x = 2
f = lambda y, x=x: x * y
x = 3
g = lambda y, x=x: x * y
print(f(10))  # --> prints 20
print(g(10))  # --> prints 30
```



```python
import time

def after(seconds, func):
    time.sleep(seconds)
    func()

# Example usage
def greeting():
    print('Hello World')

after(10, greeting)  # Prints 'Hello World' after 10 seconds
```

```python
def main():
    name = 'Guido'
    def greeting():
        print('Hello', name)
    after(10, greeting)    # Produces: 'Hello Guido'

main()
```

```python
def make_greeting(name):
    def greeting():
        print('Hello', name)
    return greeting

f = make_greeting('Guido')
g = make_greeting('Ada')

f()  # Produces: 'Hello Guido'
g()  # Produces: 'Hello Ada'
```

```python
def make_greetings(names):
    funcs = []
    for name in names:
        funcs.append(lambda: print('Hello', name))
    return funcs

# Try it
a, b, c = make_greetings(['Guido', 'Ada', 'Margaret'])
a()  # Prints 'Hello Margaret'
b()  # Prints 'Hello Margaret'
c()  # Prints 'Hello Margaret'
```

```python
def make_greetings(names):
    funcs = []
    for name in names:
        funcs.append(lambda name=name: print('Hello', name))
    return funcs

# Try it
a, b, c = make_greetings(['Guido', 'Ada', 'Margaret'])
a()  # Prints 'Hello Guido'
b()  # Prints 'Hello Ada'
c()  # Prints 'Hello Margaret'
```

```python
def make_greetings(names):
    funcs = []
    for name in names:
        def greeting(name=name):
            print('Hello', name)
        funcs.append(greeting)
    return funcs
```

```python
import time

def after(seconds, func):
    time.sleep(seconds)
    func()

def add(x, y):
    print(f'{x} + {y} -> {x+y}')
    return x + y

after(10, add(2, 3))    # Fails: add() called immediately
```

`after(10, lambda: add(2, 3))`

```python
from functools import partial

after(10, partial(add, 2, 3))
```

```python
def func(a, b, c, d):
    print(a, b, c, d)

f = partial(func, 1, 2) # Fix a=1, b=2
f(3, 4)               # func(1, 2, 3, 4)
f(10, 20)             # func(1, 2, 10, 20)

g = partial(func, 1, 2, d=4) # Fix a=1, b=2, d=4
g(3)                  # func(1, 2, 3, 4)
g(10)                 # func(1, 2, 10, 4)
```

```python
>>> def func(x, y):
...     return x + y
...
>>> a = 2
>>> b = 3
>>> f = lambda: func(a, b)
>>> g = partial(func, a, b)
>>> a = 10
>>> b = 20
>>> f()  # Uses current values of a, b
30
>>> g()  # Uses initial values of a, b
5
>>>
```

```python
# Three-argument function
def f(x, y, z):
    return x + y + z

# Curried version
def fc(x):
    return lambda y: (lambda z: x + y + z)

# Example use
a = f(2, 3, 4)    # Three-argument function
b = fc(2)(3)(4)   # Curried version
```

```python
def after(seconds, func, *args):
    time.sleep(seconds)
    func(*args)

after(10, add, 2, 3)  # Calls add(2, 3) after 10 seconds
```

```python
def after(seconds, func, *args, debug=False):
    time.sleep(seconds)
    if debug:
        print('About to call', func, args)
    func(*args)
```

```python
after(10, partial(add, y=3), 2)
```

```python
def after(seconds, func, debug=False, /, *args, **kwargs):
    time.sleep(seconds)
    if debug:
        print('About to call', func, args, kwargs)
    func(*args, **kwargs)

after(10, add, 2, y=3)
```

```python
def after(seconds, func, debug=False):
    def call(*args, **kwargs):
        time.sleep(seconds)
        if debug:
            print('About to call', func, args, kwargs)
        func(*args, **kwargs)
    return call

after(10, add)(2, y=3)
```

```python
def after(seconds, func, *args):
    time.sleep(seconds)
    return func(*args)
```

```python
after("1", add, 2, 3) # Fails: TypeError (integer is expected)
after(1, add, "2", 3) # Fails: TypeError (can't concatenate int to str)
```

```python
class CallbackError(Exception):
    pass

def after(seconds, func, *args):
    time.sleep(seconds)
    try:
        return func(*args)
    except Exception as err:
        raise CallbackError('Callback function failed') from err
```

```python
try:
    r = after(delay, add, x, y)
except CallbackError as err:
    print("It failed. Reason", err.__cause__)
```

```python
class Result:
    def __init__(self, value=None, exc=None):
        self._value = value
        self._exc = exc
    def result(self):
        if self._exc:
            raise self._exc
        else:
            return self._value
```

```python
def after(seconds, func, *args):
    time.sleep(seconds)
    try:
        return Result(value=func(*args))
    except Exception as err:
        return Result(exc=err)

# Example use:

r = after(1, add, 2, 3)
print(r.result())        # Prints 5

s = after("1", add, 2, 3)  # Immediately raises TypeError. Bad sleep() arg.

t = after(1, add, "2", 3) # Returns a "Result"
print(t.result())         # Raises TypeError
```

```python
def after(seconds, func, *args) -> Result:
    ...
```

```python
from concurrent.futures import ThreadPoolExecutor

pool = ThreadPoolExecutor(16)
r = pool.submit(add, 2, 3)     # Returns a Future
print(r.result())              # Unwrap the Future result
```

```python
def trace(func):
    def call(*args, **kwargs):
        print('Calling', func.__name__)
        return func(*args, **kwargs)
    return call

# Example use
@trace
def square(x):
    return x * x
```

```python
from functools import wraps

def trace(func):
    @wraps(func)
    def call(*args, **kwargs):
        print('Calling', func.__name__)
        return func(*args, **kwargs)
    return call
```

```python
def func(x):
    pass

func = decorator1(decorator2(func))
```

```python
class SomeClass(object):
    @classmethod        # Yes
    @trace
    def a(cls):
        pass

    @trace             # No. Fails.
    @classmethod
    def b(cls):
        pass
```

```python
@trace("You called {func.__name__}")
def func():
    pass
```

```python
def func():
    pass

# Create the decoration function
temp = trace("You called {func.__name__}")

# Apply it to func
func = temp(func)
```

```python
from functools import wraps

def trace(message):
    def decorate(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            print(message.format(func=func))
            return func(*args, **kwargs)
        return wrapper
    return decorate
```

```python
@trace('You called {func.__name__}')
def func1():
    pass

@trace('You called {func.__name__}')
def func2():
    pass
```

```python
logged = trace('You called {func.__name__}')

@logged
def func1():
    pass

@logged
def func2():
    pass
```

```python
@eventhandler('BUTTON')
def handle_button(msg):
    ...

@eventhandler('RESET')
def handle_reset(msg):
    ...
```

```python
# Event handler decorator

_event_handlers = { }

def eventhandler(event):
    def register_function(func):
        _event_handlers[event] = func
        return func
    return register_function
```

```python
def square(x):
    return x * x

nums = [1, 2, 3, 4, 5]
squares = [ square(x) for x in nums ] # [1, 4, 9, 16, 25]
```

```python
squares = [ x * x for x in nums ]
```

```python
a = [ x for x in nums if x > 2 ] # [3, 4, 5]
```

```python
squares = (x*x for x in nums) # Creates a generator
for n in squares:
    print(n)
```

```python
squares = map(lambda x: x*x, nums)
for n in squares:
    print(n)
```

```python
for n in filter(lambda x: x > 2, nums):
    print(n)
```

```python
from functools import reduce
total = reduce(lambda x, y: x + y, nums)
```

```python
nums = [1, 2, 3, 4, 5]
total = reduce(lambda x, y: x + y, nums)    # 15
product = reduce(lambda x, y: x * y, nums, 1) # 120

pairs = reduce(lambda x, y: (x, y), nums, None)
# ((((None, 1), 2), 3), 4), 5)
```

```python
def reduce(func, items, initial):
    result = initial
    for item in items:
        result = func(result, item)
    return result
```

```python
def add(x, y):
    def do_add():
        return x + y
    return do_add

>>> a = add(2, 3)
>>> a.__closure__
(<cell at 0x10edf1e20: int object at 0x10ecc1950>,
 <cell at 0x10edf1d90: int object at 0x10ecc1970>)
>>> a.__closure__[0].cell_contents
```

## 2

![](img/24ecec9a39ceab2751d0d39b3c5512ce_924_0.png)



```python
def func():
    statements

func.secure = 1
func.private = 1
```

```python
def abstractmethod(func):
    func.__isabstractmethod__ = True
    return func
```

```python
import inspect

def func(x: int, y:float, debug=False) -> float:
    pass

sig = inspect.signature(func)
```

```python
# 以美观的形式打印签名
print(sig) # 输出 (x: int, y: float, debug=False) -> float

# 获取参数名称列表
print(list(sig.parameters)) # 输出 [ 'x', 'y', 'debug']

# 遍历参数并打印各种元数据
for p in sig.parameters.values():
    print('name', p.name)
```

```python
print('annotation', p.annotation)
print('kind', p.kind)
print('default', p.default)
```

```python
def func1(x, y):
    pass

def func2(x, y):
    pass

assert inspect.signature(func1) == inspect.signature(func2)
```

```python
def func(x, y, z=None):
    ...

func.__signature__ = inspect.signature(lambda x,y: None)
```

```python
def func():
    y = 20
    locs = locals()
```

```python
locs['y'] = 30    # 尝试修改 y
print(locs['y']) # 打印 30
print(y)          # 打印 20
```

```python
def func():
    y = 20
    locs = locals()
    locs['y'] = 30
    y = locs['y']
```

```python
import inspect

def spam(x, y):
    z = x + y
    grok(z)

def grok(a):
    b = a * 10

    # 输出: {'a':5, 'b':50 }
    print(inspect.currentframe().f_locals)

    # 输出: {'x':2, 'y':3, 'z':5 }
    print(inspect.currentframe().f_back.f_locals)

spam(2, 3)
```

```python
import sys
def grok(a):
    b = a * 10
    print(sys._getframe(0).f_locals)  # 自身
    print(sys._getframe(1).f_locals)  # 调用者
```

```python
import inspect
from collections import ChainMap

def debug(*varnames):
    f = inspect.currentframe().f_back
    vars = ChainMap(f.f_locals, f.f_globals)
    print(f'{f.f_code.co_filename}:{f.f_lineno}')
    for name in varnames:
        print(f' {name} = {vars[name]!r}')

# 使用示例
def func(x, y):
    z = x + y
    debug('x','y') # 显示 x 和 y 以及文件/行号
    return z
```

```python
a = [3, 5, 10, 13]
exec('for i in a: print(i)')
```

```python
def func():
    x = 10
    exec("x = 20")
    print(x)  # 打印 10
```

```python
globs = {'x': 7,
        'y': 10,
        'birds': ['Parrot', 'Swallow', 'Albatross']
       }

locs = { }

# 使用上述字典作为全局和局部命名空间执行
exec('z = 3 * x + 4 * y', globs, locs)
exec('for b in birds: print(b)', globs, locs)
```

```python
def make_init(*names):
    parms = ','.join(names)
    code = f'def __init__(self, {parms}):\n'
    for name in names:
        code += f'    self.{name} = {name}\n'
    d = { }
    exec(code, d)
    return d['__init__']

# 使用示例
class Vector:
    __init__ = make_init('x', 'y', 'z')
```

```python
async def greeting(name):
    print(f'Hello {name}')
```

```python
>>> greeting('Guido')
<coroutine object greeting at 0x104176dc8>
>>>
```

```python
>>> import asyncio
>>> asyncio.run(greeting('Guido'))
Hello Guido
>>>
```

```python
async def make_greeting(name):
    return f'Hello {name}'
```

```python
>>> import asyncio
>>> a = asyncio.run(make_greeting('Paula'))
>>> a
'Hello Paula'
>>> 
```

```python
async def make_greeting(name):
    return f'Hello {name}'

async def main():
    for name in ['Paula', 'Thomas', 'Lewis']:
        a = await make_greeting(name)
        print(a)

# 运行它。将看到 Paula, Thomas 和 Lewis 的问候语
asyncio.run(main())
```

```python
async def twice(x):
    return 2 * x

def main():
    print(twice(2)) # 错误。没有执行该函数。
    print(await twice(2)) # 错误。此处不能使用 await。
```

```python
class AsyncManager(object):
    def __init__(self, x):
        self.x = x

    async def yow(self):
        pass

    async def __aenter__(self):
        return self

    async def __aexit__(self, ty, val, tb):
        pass
```

```python
# 使用示例
async def main():
    async with AsyncManager(42) as m:
        await m.yow()

asyncio.run(main())
```

```python
def countdown(n):
    print('Counting down from', n)
    while n > 0:
        yield n
        n -= 1

# 使用示例
for x in countdown(10):
    print('T-minus', x)
```

```python
>>> c = countdown(10)
>>> c
<generator object countdown at 0x1075f73740>
>>>
```

```python
>>> next(c)
Counting down from 10
```

```python
10
>>> next(c)
9
```

```python
>>> c.__next__()
8
>>> c.__next__()
7
>>>
```

```python
for n in countdown(10):
    statements

a = sum(countdown(10))
```

```python
>>> f = func()
>>> f
<generator object func at 0x10cb7cd480>
>>> next(f)
37
>>> next(f)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration: 42
>>>
```

```python
try:
    next(f)
except StopIteration as e:
    value = e.value
```

```python
for n in countdown(10):
    if n == 2:
        break
statements
```

```python
def countdown(n):
    print('Counting down from', n)
    try:
        while n > 0:
            yield n
            n = n - 1
    finally:
        print('Only made it to', n)
```

```python
def func(filename):
    with open(filename) as file:
        ...
        yield data
        ...
# 即使生成器被放弃，文件也会在此处关闭
```

```python
>>> c = countdown(3)
>>> for n in c:
...     print('T-minus', n)
... 
T-minus 3
T-minus 2
T-minus 1
>>> for n in c:
...     print('T-minus', n)
... 
>>> 
```

```python
class countdown:
    def __init__(self, start):
        self.start = start

    def __iter__(self):
        n = self.start
        while n > 0:
            yield n
            n -= 1
```

```python
def countup(stop):
    n = 1
    while n <= stop:
        yield n
        n += 1
```

```python
def countdown(start):
    n = start
    while n > 0:
        yield n
        n -= 1

def up_and_down(n):
    yield from countup(n)
    yield from countdown(n)
```

```python
>>> for x in up_and_down(5):
...     print(x, end=' ')
1 2 3 4 5 5 4 3 2 1
>>>
```

```python
def up_and_down(n):
    for x in countup(n):
        yield x
    for x in countdown(n):
        yield x
```

```python
def flatten(items):
    for i in items:
        if isinstance(i, list):
            yield from flatten(i)
        else:
            yield i
```

```python
>>> a = [1, 2, [3, [4, 5], 6, 7], 8]
>>> for x in flatten(a):
...     print(x, end=' ')
... 
1 2 3 4 5 6 7 8
>>> 
```

```python
import pathlib
import re

for path in pathlib.Path('.').rglob('*.py'):
    if path.exists():
        with path.open('rt', encoding='latin-1') as file:
            for line in file:
                m = re.match('.*(#.*)$', line)
                if m:
                    comment = m.group(1)
                    if 'spam' in comment:
                        print(comment)
```

```python
import pathlib
import re

def get_paths(topdir, pattern):
    for path in pathlib.Path(topdir).rglob(pattern):
        if path.exists():
            yield path

def get_files(paths):
    for path in paths:
        with path.open('rt', encoding='latin-1') as file:
            yield file

def get_lines(files):
    for file in files:
        yield from file
```

```python
def get_comments(lines):
    for line in lines:
        m = re.match('.*(#.*)$', line)
        if m:
            yield m.group(1)

def print_matching(lines, substring):
    for line in lines:
        if substring in lines:
            print(substring)

paths = get_paths('.', '*.py')
files = get_files(paths)
lines = get_lines(files)
comments = get_comments(lines)
print_matching(comments, 'spam')
```

```python
def flatten(items):
    for i in items:
        if isinstance(i, list):
            yield from flatten(i)
        else:
            yield i
```

```python
def flatten(items):
    stack = [ iter(items) ]
    while stack:
        try:
            item = next(stack[-1])
            if isinstance(item, list):
                stack.append(iter(item))
            else:
                yield item
        except StopIteration:
            stack.pop()
```

```python
def receiver():
    print('Ready to receive')
    while True:
        n = yield
        print('Got', n)
```

```python
>>> r = receiver()
>>> r.send(None)    # Advances to the first yield
Ready to receive
>>> r.send(1)
Got 1
>>> r.send(2)
Got 2
>>> r.send('Hello')
Got Hello
>>>
```



```python
>>> r.close()
>>> r.send(4)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>>
```

```python
>>> r = receiver()
Ready to receive
>>> r.throw(RuntimeError, "Dead")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "receiver.py", line 14, in receiver
    n = yield
RuntimeError: Dead
>>>
```

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

```python
class Manager:
    def __enter__(self):
        return somevalue

    def __exit__(self, ty, val, tb):
        if ty:
            # An exception occurred.
            ...
            # Return True if handled, False otherwise
```

```python
>>> with manager() as val:
...     print(val)
...
Entering
somevalue
Leaving
>>> with manager() as val:
...     print(int(val))
...
Entering
An error occurred invalid literal for int() with base 10: 'somevalue'
Leaving
>>>
```

```python
class Manager:
    def __init__(self, gen):
        self.gen = gen

    def __enter__(self):
        # Run to the yield
        return self.gen.send(None)

    def __exit__(self, ty, val, tb):
        # Propagate an exception (if any)
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

```python
def line_receiver():
    data = bytearray()
    line = None
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

```python
>>> r = line_receiver()
>>> r.send(None)    # Prime the generator
>>> r.send(b'hello')
>>> r.send(b'world\n it ')
b'hello world\n'
>>> r.send(b'works!')
>>> r.send(b'\n')
b'it works!\n'
>>>
```

```python
class LineReceiver:
    def __init__(self):
        self.data = bytearray()
        self.linecount = 0

    def send(self, part):
        self.linecount += part.count(b'\n')
        self.data.extend(part)
        if self.linecount > 0:
            index = self.data.index(b'\n')
            line = bytes(self.data[:index+1])
            self.data = self.data[index+1:]
            self.linecount -= 1
            return line
        else:
            return None
```

```python
class Awaitable:
    def __await__(self):
        print('About to await')
        yield  # Must be a generator
        print('Resuming')

# Function compatible with "await". Returns an "awaitable".
def function():
    return Awaitable()

async def main():
    await function()
```

```python
>>> s = "Hello World"
>>> s.upper()
'HELLO WORLD'
>>> s.replace('Hello', 'Hello Cruel')
'Hello Cruel World'
>>> s.split()
['Hello', 'World']
>>>
```

```python
>>> type(names)
<class 'list'>
>>>
```

一个对象被称为其类型的实例（instance）。例如，`names` 是 `list` 的一个实例。

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

    def inquiry(self):
        return self.balance
```

```python
class Account:
    """
    一个简单的银行账户
    """

    owner: str
    balance: float

    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

    def inquiry(self):
        return self.balance
```

```python
# 创建几个账户

a = Account('Guido', 1000.0)
# 调用 Account.__init__(a, 'Guido', 1000.0)
b = Account('Eva', 10.0)
# 调用 Account.__init__(b, 'Eva', 10.0)
```

```python
a.deposit(100.0)       # 调用 Account.deposit(a, 100.0)
b.withdraw(50.00)      # 调用 Account.withdraw(b, 50.0)
owner = a.owner         # 获取账户所有者
```

```python
>>> a = Account('Guido', 1000.0)
>>> b = Account('Eva', 10.0)
>>> vars(a)
{'owner': 'Guido', 'balance': 1000.0}
>>> vars(b)
{'owner': 'Eva', 'balance': 10.0}
>>>
```

```python
>>> type(a)
<class 'Account'>
>>> type(b)
<class 'Account'>
>>> type(a).deposit
<function Account.deposit at 0x10a032158>
>>> type(a).inquiry
<function Account.inquiry at 0x10a032268>
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> a.owner # get
'Guido'
>>> a.balance = 750.0  # set
>>> del a.balance  # delete
>>> a.balance
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Account' object has no attribute 'balance'
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> a.creation_date = '2019-02-14'
>>> a.nickname = 'Former BDFL'
>>> a.creation_date
'2019-02-14'
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> getattr(a, 'owner')
'Guido'
>>> setattr(a, 'balance', 750.0)
>>> delattr(a, 'balance')
>>> hasattr(a, 'balance')
False
>>> getattr(a, 'withdraw')(100)  # 方法调用
>>> a
Account('Guido', 650.0)
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> getattr(a, 'balance', 'unknown')
1000.0
>>> getattr(a, 'creation_date', 'unknown')
'unknown'
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> w = a.withdraw
>>> w
<bound method Account.withdraw of Account('Guido', 1000.0)>
>>> w(100)
>>> a
Account('Guido', 900.0)
>>>
```

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.deposit(-amount)    # 必须使用 self.deposit()

    def inquiry(self):
        return self.balance
```

```python
class AccountPortfolio:
    def __init__(self):
        self.accounts = []

    def add_account(self, account):
        self.accounts.append(account)

    def total_funds(self):
        return sum(account.inquiry() for account in self)

    def __len__(self):
        return len(self.accounts)

    def __getitem__(self, index):
        return self.accounts[index]

    def __iter__(self):
        return iter(self.accounts)
```

# 示例

```python
port = AccountPortfolio()

port.add_account(Account('Guido', 1000.0))

port.add_account(Account('Eva', 50.0))

print(port.total_funds())  # -> 1050.0

len(port)                  # -> 2

# 打印账户

for account in port:
    print(account)

# 通过索引访问单个账户

port[1].inquiry()             # -> 50.0
```

```python
class MyAcount(Account):

    def panic(self):
        self.withdraw(self.balance)

# 示例

a = MyAcount('Guido', 1000.0)

a.withdraw(23.0)            # a.balance = 977.0

a.panic()                    # a.balance = 0
```

```python
import random

class EvilAccount(Account):

    def inquiry(self):
        if random.randint(0,4) == 1:
            return self.balance * 1.10
        else:
            return self.balance

a = EvilAccount('Guido', 1000.0)

a.deposit(10.0) # 调用 Account.deposit(a, 10.0)

available = a.inquiry() # 调用 EvilAccount.inquiry(a)
```

```python
class EvilAccount(Account):

    def inquiry(self):
        if random.randint(0, 4) == 1:
            return 1.10 * super().inquiry()
        else:
            return super().inquiry()
```

```python
class EvilAccount(Account):

    def __init__(self, owner, balance, factor):
        super().__init__(owner, balance)
        self.factor = factor

    def inquiry(self):
        if random.randint(0, 4) == 1:
```



```python
return self.factor * super().inquiry()

else:

    return super().inquiry()
```

```python
class Account:

    def __init__(self, owner, balance):

        self.owner = owner

        self.balance = balance

    def __repr__(self):

        return f'Account({self.owner!r}, {self.balance!r})'
```

```python
>>> class EvilAccount(Account):

...    pass

...

>>> a = EvilAccount('Eva', 10.0)

>>> a

Account('Eva', 10.0)  # 注意：输出具有误导性

>>> type(a)

<class 'EvilAccount'>

>>>
```

```python
class Account:

    ...

    def __repr__(self):

        return f'{type(self).__name__}({self.owner!r}, {self.balance!r})'
```

```python
>>> a = EvilAccount('Eva', 10)

>>> type(a)

<class 'EvilAccount'>

>>> isinstance(a, Account)

True

>>>
```

```python
class Food:

    pass

class Sandwich(Food):

    pass

class RoastBeef(Sandwich):

    pass

class GrilledCheese(Sandwich):

    pass

class Taco(Food):

    pass
```

```python
class HotDog(Sandwich, Taco):

    pass
```

```python
class Stack(list):

    def push(self, item):

        self.append(item)
```

## 示例

```python
s = Stack()

s.push(1)

s.push(2)

s.push(3)

s.pop() # -> 3

s.pop() # -> 2
```

```python
class Stack:

    def __init__(self):

        self._items = list()

    def push(self, item):

        self._items.append(item)

    def pop(self):

        return self._items.pop()

    def __len__(self):

        return len(self._items)

# 示例用法

s = Stack()

s.push(1)

s.push(2)

s.push(3)

s.pop() # -> 3

s.pop() # -> 2
```

```python
class Stack:

    def __init__(self, *, container=None):

        if container is None:

            container = list()

        self._items = container

    def push(self, item):

        self._items.append(item)

    def pop(self):

        return self._items.pop()

    def __len__(self):

        return len(self._items)
```

```python
import array

s = Stack(container=array.array('i'))

s.push(42)

s.push(23)

s.push('a lot')  # TypeError
```

```python
class Stack:

    def __init__(self):

        self._items = None

        self._size = 0

    def push(self, item):

        self._items = (item, self._items)

        self._size += 1

    def pop(self):

        (item, self._items) = self._items

        self._size -= 1

        return item

    def __len__(self):

        return self._size
```

```python
class DataParser:

    def parse(self, lines):

        records = []

        for line in lines:

            row = line.split(',')

            record = self.make_record(row)

            records.append(record)

        return records

    def make_record(self, row):

        raise NotImplementedError()

class PortfolioDataParser(DataParser):

    def make_record(self, row):

        return {

            'name': row[0],

            'shares': int(row[1]),

            'price': float(row[2])

        }

parser = PortfolioDataParser()

data = parser.parse(open('portfolio.csv'))
```

```python
def parse_data(lines, make_record):

    records = []

    for line in lines:

        row = line.split(',')

        record = make_record(row)

        records.append(record)

    return records

def make_dict(row):

    return {

        'name': row[0],

        'shares': int(row[1]),

        'price': float(row[2])

    }

data = parse_data(open('portfolio.csv'), make_dict)
```

```python
class udict(dict):

    def __setitem__(self, key, value):

        super().__setitem__(key.upper(), value)
```

```python
>>> u = udict()

>>> u['name'] = 'Guido'

>>> u['number'] = 37

>>> u

{ 'NAME': 'Guido', 'NUMBER': 37 }

>>>
```

```python
>>> u = udict(name='Guido', number=37)

>>> u

{ 'name': 'Guido', 'number': 37 }

>>> u.update(color='blue')

>>> u

{ 'name': 'Guido', 'number': 37, 'color': 'blue' }

>>>
```

```python
from collections import UserDict

class udict(UserDict):

    def __setitem__(self, key, value):

        super().__setitem__(key.upper(), value)
```

```python
>>> u = udict(name='Guido', num=37)

>>> u.update(color='Blue')

>>> u

{'NAME': 'Guido', 'NUM': 37, 'COLOR': 'Blue'}

>>> v = udict(u)

>>> v['title'] = 'BDFL'

>>> v

{'NAME': 'Guido', 'NUM': 37, 'COLOR': 'Blue', 'TITLE': 'BDFL'}

>>>
```

```python
class Account:

    num_accounts = 0

    def __init__(self, owner, balance):

        self.owner = owner

        self.balance = balance

        Account.num_accounts += 1

    def __repr__(self):

        return f'{type(self).__name__}({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):

        self.balance += amount

    def withdraw(self, amount):

        self.deposit(-amount)  # 必须使用 self.deposit()

    def inquiry(self):

        return self.balance
```

```python
>>> a = Account('Guido', 1000.0)

>>> b = Account('Eva', 10.0)

>>> Account.num_accounts

2

>>> a.num_accounts

2

>>> c = Account('Ben', 50.0)

>>> Account.num_accounts

3

>>> a.num_accounts

3

>>>
```

```python
data = '''

<account>

    <owner>Guido</owner>

    <amount>1000.0</amount>

</account>

'''
```

```python
class Account:

    def __init__(self, owner, balance):

        self.owner = owner

        self.balance = balance

    @classmethod

    def from_xml(cls, data):

        from xml.etree.ElementTree import XML

        doc = XML(data)

        return cls(doc.findtext('owner'), float(doc.findtext('amount')))

# 示例用法

data = '''

<account>

    <owner>Guido</owner>

    <amount>1000.0</amount>

</account>

'''

a = Account.from_xml(data)
```

```python
class EvilAccount(Account):

    pass

e = EvilAccount.from_xml(data)  # 创建一个 'EvilAccount' 实例
```

```python
import time

class Date:

    datefmt = '{year}-{month:02d}-{day:02d}'

    def __init__(self, year, month, day):

        self.year = year

        self.month = month

        self.day = day

    def __str__(self):

        return self.datefmt.format(year=self.year, month=self.month, day=self.day)

    @classmethod

    def from_timestamp(cls, ts):

        tm = time.localtime(ts)

        return cls(tm.tm_year, tm.tm_mon, tm.tm_mday)

    @classmethod

    def today(cls):

        return cls.from_timestamp(time.time())
```

```python
class MDYDate(Date):

    datefmt = '{month}/{day}/{year}'

class DMYDate(Date):

    datefmt = '{day}/{month}/{year}'
```

```python
# Example

a = Date(1967, 4, 9)

print(a)    # 1967-04-09

b = MDYDate(1967, 4, 9)

print(b)    # 4/9/1967

c = DMYDate(1967, 4, 9)

print(c)    # 9/4/1967
```

```python
a = MDYDate.today()

b = DMYDate.today()

print(a)  # 2/13/2019

print(b)  # 13/2/2019
```

```python
>>> dict.fromkeys(['a','b','c'], 0)

{'a': 0, 'b': 0, 'c': 0}

>>>
```

```python
d = Date(1967, 4, 9)

b = d.today() # Calls Date.now(Date)
```

```python
class Ops:

    @staticmethod

    def add(x, y):

        return x + y

    @staticmethod

    def sub(x, y):

        return x - y
```

```python
a = Ops.add(2, 3)    # a = 5

b = Ops.sub(4, 5)    # a = -1
```

```python
class Account:

    def __init__(self, owner, balance):

        self.owner = owner

        self.balance = balance

    def __repr__(self):

        return f'{type(self).__name__}({self.owner!r}, {self.balance!r})'

    def deposit(self, amount):

        self.balance += amount

    def withdraw(self, amount):

        self.balance -= amount

    def inquiry(self):

        return self.balance

# A special "Evil" account

class EvilAccount(Account):

    def deposit(self, amount):

        self.balance += 0.95 * amount

    def inquiry(self):

        if random.randint(0,4) == 1:

            return 1.10 * self.balance

        else:

            return self.balance
```

```python
class StandardPolicy:

    @staticmethod

    def deposit(account, amount):

        account.balance += amount

    @staticmethod

    def withdraw(account, amount):

        account.balance -= amount

    @staticmethod

    def inquiry(account):

        return account.balance

class EvilPolicy(StandardPolicy):
```



```python
@staticmethod
def deposit(account, amount):
    account.balance += 0.95 * amount

@staticmethod
def inquiry(account):
    if random.randint(0, 4) == 1:
        return 1.10 * account.balance
    else:
        return account.balance

class Account:
    def __init__(self, owner, balance, *, policy=StandardPolicy):
        self.owner = owner
        self.balance = balance
        self.policy = policy

    def __repr__(self):
        return f'Account({self.policy}, {self.owner!r}, {self.balance!r})'

    def deposit(self, amount):
        self.policy.deposit(self, amount)

    def withdraw(self, amount):
        self.policy.withdraw(self, amount)

    def inquiry(self):
        return self.policy.inquiry(self)
```

```python
>>> a = Account('Guido', 1000.0)

>>> a.policy
<class 'StandardPolicy'>

>>> a.deposit(500)

>>> a.inquiry()
1500.0

>>> a.policy = EvilPolicy

>>> a.deposit(500)

>>> a.inquiry()    # Could randomly be 1.10x more
1975.0

>>>
```

```python
class EvilPolicy(StandardPolicy):
    def __init__(self, deposit_factor, inquiry_factor):
        self.deposit_factor = deposit_factor
        self.inquiry_factor = inquiry_factor

    def deposit(self, account, amount):
        account.balance += self.deposit_factor * amount

    def inquiry(self, account):
        if random.randint(0, 4) == 1:
            return self.inquiry_factor * account.balance
        else:
            return account.balance
```

```python
# Example use

a = Account('Guido', 1000.0, policy=EvilPolicy(0.95, 1.10))
```

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance

    def __repr__(self):
        return f'Account({self.owner!r}, {self._balance!r})'

    def deposit(self, amount):
        self._balance += amount

    def withdraw(self, amount):
        self._balance -= amount

    def inquiry(self):
        return self._balance
```

```python
class EvilAccount(Account):
    def inquiry(self):
        if random.randint(0, 4) == 1:
            return 1.10 * self._balance
        else:
            return self._balance
```

```python
class A:
    def __init__(self):
        self.__x = 3  # Mangled to self._A__x

    def __spam(self):  # Mangled to _A__spam()
        print('A.__spam', self.__x)

    def bar(self):
        self.__spam()  # Only calls A.__spam()


class B(A):
    def __init__(self):
        A.__init__(self)
        self.__x = 37  # Mangled to self._B__x

    def __spam(self):  # Mangled to _B__spam()
        print('B.__spam', self.__x)

    def grok(self):
        self.__spam()  # Calls B.__spam()
```

```python
>>> vars(b)
{'_A__x': 3, '_B__x': 37}

>>> b._A__spam()
A.__spam 3

>>> b._B__spam()
B.__spam 37

>>>
```

```python
>>> a = Account('Guido', 1000.0)

>>> a.owner
'Guido'

>>> a.owner = 37

>>> a.owner
37

>>> b = Account('Eva', 'a lot')

>>> b.deposit(' more')

>>> b.inquiry()
'a lot more'

>>>
```

```python
class Account:
    owner: str            # Type hint
    _balance: float       # Type hint

    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance

...
...
```

```python
from decimal import Decimal

a = Account('Guido', Decimal('1000.0'))

a.withdraw(Decimal('50.0'))

print(a.inquiry())      # -> 950.0
```

```python
import string

class Account:
    def __init__(self, owner, balance):
        self._owner = owner
        self._balance = balance

    @property
    def owner(self):
        return self._owner

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

>>> a.owner = 'RAMAKRISHNAN'
Traceback (most recent call last):
...
ValueError: Must be 10 characters or less

>>>
```

```python
>>> a = Account('Guido', 1000.0)
Traceback (most recent call last):
  File "account.py", line 5, in __init__
    self.owner = owner
  File "account.py", line 15, in owner
    raise ValueError('Must be uppercase ASCII')

ValueError: Must be uppercase ASCII

>>>
```

```python
class SomeClass:
    @property
    def attr(self):
        print('Getting')

    @attr.setter
    def attr(self, value):
        print('Setting', value)

    @attr.deleter
    def attr(self):
        print('Deleting')


# Example

s = SomeClass()

s.attr              # Getting
s.attr = 13         # Setting
del s.attr          # Deleting
```

```python
class Box(object):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    @property
    def area(self):
        return self.width * self.height

    @property
    def perimeter(self):
        return 2 * self.width + 2 * self.height


# Example use

b = Box(4, 5)

print(b.area)      # -> 20
print(b.perimeter) # -> 18

b.area = 5          # Error: can't set attribute
```

```python
class SomeClass:
    def yow(self):
        print('Yow!')
```

```python
>>> s = SomeClass()

>>> s.yow
<bound method SomeClass.yow of <__main__.SomeClass object at 0x10e2572b0>>

>>>
```

```python
class A:
    pass


class B(A):
    pass


class C:
    pass


a = A()  # Instance of 'A'
b = B()  # Instance of 'B'
c = C()  # Instance of 'C'

type(a)  # Returns the class object A

isinstance(a, A)  # Returns True
isinstance(b, A)  # Returns True, B derives from A
isinstance(b, C)  # Returns False, B not derived from C
```

```python
issubclass(B, A)  # 返回 True

issubclass(C, A)  # 返回 False
```

```python
class Stream:
    def receive(self):
        raise NotImplementedError()

    def send(self, msg):
        raise NotImplementedError()

    def close(self):
        raise NotImplementedError()


# 示例

def send_request(stream, request):
    if not isinstance(stream, Stream):
        raise TypeError('Expected a Stream')

    stream.send(request)
    return stream.receive()
```

```python
class SocketStream(Stream):
    def receive(self):
        ...

    def send(self, msg):
        ...

    def close(self):
        ...


class PipeStream(Stream):
    def receive(self):
        ...

    def send(self, msg):
        ...

    def close(self):
        ...
```

## 示例

```python
s = SocketStream()
send_request(s, request)
```

```python
# 将接口指定为类型提示

def send_request(stream: Stream, request):
    stream.send(request)
    return stream.receive()
```

```python
from abc import ABC, abstractmethod

class Stream(ABC):
    @abstractmethod
    def receive(self):
        pass

    @abstractmethod
    def send(self, msg):
        pass

    @abstractmethod
    def close(self):
        pass
```

```python
>>> s = Stream()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class Stream with abstract methods close, receive, send
>>>
```

```python
class SocketStream(Stream):
    def read(self):
        ...

    def send(self, msg):
        ...

    def close(self):
        ...
```

```python
>>> s = SocketStream()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class SocketStream with abstract methods receive
>>>
```



```python
class Duck:
    def walk(self):
        print('Waddle')

class Trombonist:
    def noise(self):
        print('Blat!')

class DuckBonist(Duck, Trombonist):
    pass

d = DuckBonist()
d.walk()    # -> Waddle
d.noise()   # -> Blat!
```

```python
from abc import ABC, abstractmethod

class Stream(ABC):
    @abstractmethod
    def receive(self):
        pass

    @abstractmethod
    def send(self, msg):
        pass

    @abstractmethod
    def close(self):
        pass

class Iterable(ABC):
    @abstractmethod
    def __iter__(self):
        pass
```

```python
class MessageStream(Stream, Iterable):
    def receive(self):
        ...
    def send(self):
        ...
    def close(self):
        ...
    def __iter__(self):
        ...
```

```python
m = MessageStream()

isinstance(m, Stream)    # -> True
isinstance(m, Iterable)  # -> True
```

```python
class Duck:
    def noise(self):
        return 'Quack'

    def waddle(self):
        return 'Waddle'

class Trombonist:
    def noise(self):
        return 'Blat!'

    def march(self):
        return 'Clomp'

class Cyclist:
    def noise(self):
        return 'On your left!'

    def pedal(self):
        return 'Pedaling'
```

```python
class LoudMixin:
    def noise(self):
        return super().noise().upper()

class AnnoyingMixin:
    def noise(self):
        return 3*super().noise()
```

```python
>>> a = AnnoyingMixin()
>>> a.noise()
Traceback (most recent call last):
  ...
AttributeError: 'super' object has no attribute 'noise'
>>>
```

```python
class LoudDuck(LoudMixin, Duck):
    pass

class AnnoyingTrombonist(AnnoyingMixin, Trombonist):
    pass
```

```python
class AnnoyingLoudCyclist(AnnoyingMixin, LoudMixin, Cyclist):
    pass

d = LoudDuck()
d.noise() # -> 'QUACK'

t = AnnoyingTrombonist()
t.noise() # -> 'Blat!Blat!Blat!'

c = AnnoyingLoudCyclist()
c.noise() # -> 'ON YOUR LEFT!ON YOUR LEFT!ON YOUR LEFT!'
```

```python
class Base:
    pass

class A(Base):
    pass

class B(A):
    pass

Base.__mro__ # -> (<class 'Base'>, <class 'object'>)
A.__mro__ # -> (<class 'A'>, <class 'Base'>, <class 'object'>)
B.__mro__ # -> (<class 'B'>, <class 'A'>, <class 'Base'>, <class 'object'>)
```

```python
class X: pass
class Y(X): pass
class Z(X,Y): pass  # TypeError.
                    # 无法创建一致的 MRO（方法解析顺序）
```

```python
class AnnoyingLoudCyclist(AnnoyingMixin, LoudMixin, Cyclist):
    pass

AnnoyingLoudCyclist.__mro__
# (<class 'AnnoyingLoudCyclist', <class 'AnnoyingMixin'>,
# <class 'LoudMixin', <class 'Cyclist', <class 'object'>)
```

```python
class NoiseMixin:
    def noise(self):
        raise NotImplementedError('noise() not implemented')

class LoudMixin(NoiseMixin):
    def noise(self):
        return super().noise().upper()

class AnnoyingMixin(NoiseMixin):
    def noise(self):
        return 3 * super().noise()
```

```python
class Base:
    def yow(self):
        print('Base.yow')

class A(Base):
    def yow(self):
        print('A.yow')
        Base.yow(self)  # 直接调用父类

class B(Base):
    def yow(self):
        print('B.yow')
        super().yow(self)

class C(A, B):
    pass

c = C()
c.yow()
# 输出:
#     A.yow
#     Base.yow
```

```python
if isinstance(obj, Duck):
    handle_duck(obj)
elif isinstance(obj, Trombonist):
    handle_trombonist(obj)
elif isinstance(obj, Cyclist):
    handle_cyclist(obj)
else:
    raise RuntimeError('Unknown object')
```

```python
handlers = {
    Duck: handle_duck,
    Trombonist: handle_trombonist,
    Cyclist: handle_cyclist
}

# 分发
def dispatch(obj):
    func = handlers.get(type(obj))
    if func:
        return func(obj)
    else:
        raise RuntimeError(f'No handler for {obj}')
```

```python
def dispatch(obj):
    for ty in type(obj).__mro__:
        func = handlers.get(ty)
        if func:
            return func(obj)
    raise RuntimeError(f'No handler for {obj}')
```

```python
class Dispatcher:
    def handle(self, obj):
        for ty in type(obj).__mro__:
            meth = getattr(self, f'handle_{ty.__name__}', None)
            if meth:
                return meth(obj)
        raise RuntimeError(f'No handler for {obj}')

    def handle_Duck(self, obj):
        ...

    def handle_Trombonist(self, obj):
        ...

    def handle_Cyclist(self, obj):
        ...

# 示例
dispatcher = Dispatcher()
dispatcher.handle(Duck())    # -> handle_Duck()
dispatcher.handle(Cyclist()) # -> handle_Cyclist()
```

```python
_registry = { }

def register_decoder(cls):
    for mt in cls.mimetypes:
        _registry[mt.mimetype] = cls
    return cls

# 使用注册表的工厂函数
def create_decoder(mimetype):
    return _registry[mimetype]()
```

```python
@register_decoder
class TextDecoder:
    mimetypes = [ 'text/plain' ]
    def decode(self, data):
        ...

@register_decoder
class HTMLDecoder:
    mimetypes = [ 'text/html' ]
    def decode(self, data):
        ...

@register_decoder
class ImageDecoder:
    mimetypes = [ 'image/png', 'image/jpg', 'image/gif' ]
    def decode(self, data):
        ...

# 示例用法
decoder = create_decoder('image/jpg')
```

```python
def loud(cls):
    orig_noise = cls.noise
    def noise(self):
        return orig_noise(self).upper()
    cls.noise = noise
    return cls

def annoying(cls):
    orig_noise = cls.noise
    def noise(self):
        return 3 * orig_noise(self)
    cls.noise = noise
    return cls

@annoying
@loud
class Cyclist(object):
    def noise(self):
        return 'On your left!'

    def pedal(self):
        ...
```

```python
return 'Pedaling'
```

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __repr__(self):
        return f'{type(self).__name__}({self.x!r}, {self.y!r})'
```

```python
import inspect

def with_repr(cls):
    args = list(inspect.signature(cls).parameters)
    argvals = ' , '.join('%s!r' % arg for arg in args)
    code = 'def __repr__(self):\n'
    code += f'    return f"{cls.__name__}({argvals})"\n'
    locs = { }
    exec(code, locs)
    cls.__repr__ = locs['__repr__repr__']
    return cls

# Example
@with_repr
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int
```

```python
>>> p = Point(2, 3)
>>> p
Point(x=2, y=3)
>>>
```

```python
class Base:
    @classmethod
    def __init_subclass__(cls):
        print('Initializing', cls)

# Example (should see 'Initializing' message for each class)
class A(Base):
    pass

class B(A):
    pass
```

```python
class DecoderBase:
    _registry = { }
    @classmethod
    def __init_subclass__(cls):
        for mt in cls.mimetypes:
            DecoderBase._registry[mt.mimetype] = cls

# Factory function that uses the registry
def create_decoder(mimetype):
    return DecoderBase._registry[mimetype]()

class TextDecoder(DecoderBase):
    mimetypes = [ 'text/plain' ]
    def decode(self, data):
        ...

class HTMLDecoder(DecoderBase):
    mimetypes = [ 'text/html' ]
    def decode(self, data):
        ...

class ImageDecoder(DecoderBase):
    mimetypes = [ 'image/png', 'image/jpg', 'image/gif' ]
    def decode(self, data):
        ...

# Example usage
decoder = create_decoder('image/jpg')
```

```python
import inspect

class Base:
    @classmethod
    def __init_subclass__(cls):
        # Create a __repr__ method
        args = list(inspect.signature(cls).parameters)
        argvals = ', '.join('self.%s!r' % arg for arg in args)
        code = 'def __repr__(self):\n'
        code += f'    return f"{cls.__name__}({argvals})"\n'
        locs = { }
        exec(code, locs)
        cls.__repr__ = locs['__repr__']
```

```python
class Point(Base):
    def __init__(self, x, y):
        self.x = x
        self.y = y
```



```python
class A:
    @classmethod
    def __init_subclass__(cls):
        print('A.init_subclass')
        super().__init_subclass__()

class B:
    @classmethod
    def __init_subclass__(cls):
        print('B.init_subclass')
        super().__init_subclass__()

# Should see output from both classes here
class C(A, B):
    pass
```

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

# Create some Account instances
a = Account('Guido', 1000.0)
b = Account('Eva', 25.0)
```

```python
a = Account.__new__(Account, 'Guido', 1000.0)
if isinstance(a, Account):
    Account.__init__('Guido', 1000.0)
```

```python
a = Account.__new__(Account)
Account.__init__('Guido', 1000.0)
```

```python
import time

class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    @classmethod
    def today(cls):
        t = time.localtime()
        self = cls.__new__(cls)  # Make instance
        self.year = t.tm_year
        self.month = t.tm_month
        self.day = t.tm_day
        return self
```

```python
class Date:
    _cache = { }

    @staticmethod
    def __new__(cls, year, month, day):
        self = Date._cache.get((year,month,day))
        if not self:
            self = super().__new__(cls)
            self.year = year
            self.month = month
            self.day = day
            Date._cache[year,month,day] = self
        return self

    def __init__(self, year, month, day):
        pass

# Example
d = Date(2012, 12, 21)
e = Date(2012, 12, 21)
assert d is e              # Same object
```

```python
class Account(object):
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __del__(self):
        print('Deleting Account')
```

```python
>>> a = Account('Guido', 1000.0)
>>> del a
Deleting Account
>>>
```

```python
>>> a = Account('Guido', 1000.0)
>>> a = 42
Deleting Account
>>> def func():
...     a = Account('Guido', 1000.0)
... 
>>> func()
Deleting Account
>>> 
```

```python
class SomeClass:
    def __init__(self):
        self.resource = open_resource()

    def __del__(self):
        self.close()

    def close(self):
        self.resource.close()

    def __enter__(self):
        return self

    def __exit__(self, ty, val, tb):
        self.close()
```

```python
# Closed via __del__()
s = SomeClass()
del s

# Explicit close
s = SomeClass()
s.close()

# Closed at the end of a context block
with SomeClass() as s:
    ...
```

```python
class SomeClass:
    def __del__(self):
        print('Deleting')

parent = SomeClass()
child = SomeClass()

# Create a child-parent reference cycle
parent.child = child
child.parent = parent

# Try deletion (no output from __del__ appears)
del parent
del child
```

```python
>>> a = Account('Guido', 1000.0)
>>> import weakref
>>> a_ref = weakref.ref(a)
>>> a_ref
<weakref at 0x104617188; to 'Account' at 0x1046105c0>
>>>
```

```python
>>> del a
>>> a_ref
<weakref at 0x104617188; dead>
>>>
```

```python
acct = a_ref()
if acct is not None:
    acct.withdraw(10)

# Alternative
if acct := a_ref():
    acct.withdraw(10)
```

```python
import weakref

class Date:
    _cache = { }

    @staticmethod
    def __new__(cls, year, month, day):
        selfref = Date._cache.get((year,month,day))
        if not selfref:
            self = super().__new__(cls)
            self.year = year
            self.month = month
            self.day = day
            Date._cache[year,month,day] = weakref.ref(self)
        else:
            self = selfref()
        return self

    def __init__(self, year, month, day):
        pass

    def __del__(self):
        del Date._cache[self.year,self.month,self.day]
```

```python
>>> Date._cache
{}
>>> a = Date(2012, 12, 21)
>>> Date._cache
{(2012, 12, 21): <weakref at 0x10c7ee2c8; to 'Date' at 0x10c805518>}
>>> b = Date(2012, 12, 21)
>>> a is b
True
>>> del a
>>> Date._cache
{(2012, 12, 21): <weakref at 0x10c7ee2c8; to 'Date' at 0x10c805518>}
>>> del b
>>> Date._cache
{}
>>> 
```

```python
class wdict(dict):
    __slots__ = ('__weakref__',)

w = wdict()
w_ref = weakref.ref(w)  # Now works
```

```python
>>> a = Account('Guido', 1100.0)
>>> a.__dict__
{'owner': 'Guido', 'balance': 1100.0}
```

```python
a.number = 123456 # Add attribute 'number' to a.__dict__
a.__dict__['number'] = 654321
```

```python
>>> a.__class__
<class '__main__.Account'>
>>> Account.__dict__.keys()
```

```python
dict_keys(['__module__', '__init__', '__repr__', 'deposit', 'withdraw',
'inquiry', '__dict__', '__weakref__', '__doc__'])
>>> Account.__dict__['withdraw']
<function Account.withdraw at 0x108204158>
>>>
```

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __setattr__(self, name, value):
        if name not in {'owner', 'balance'}:
            raise AttributeError(f'No attribute {name}')
        super().__setattr__(name, value)

# Example
a = Account('Guido', 1000.0)
a.balance = 940.25  # Ok
a.amount = 540.2    # AttributeError. No attribute amount
```

```python
class A:
    def spam(self):
        print('A.spam')

    def grok(self):
        print('A.grok')

    def yow(self):
        print('A.yow')

class LoggedA:
    def __init__(self):
        self._a = A()

    def __getattr__(self, name):
        print("Accessing", name)
        # Delegate to internal A instance
        return getattr(self._a, name)

# Example use
a = LoggedA()
a.spam() # prints "Accessing spam" and "A.spam"
a.yow()  # prints "Accessing yow" and "A.yow"
```

```python
class A:
    def spam(self):
        print('A.spam')

    def grok(self):
        print('A.grok')

    def yow(self):
        print('A.yow')

class B:
    def __init__(self):
        self._a = A()

    def grok(self):
        print('B.grok')

    def __getattr__(self, name):
        return getattr(self._a, name)

# Example use
b = B()
b.spam()  # -> A.spam
b.grok()  # -> B.grok  (redefined method)
b.yow()   # -> A.yow
```

```python
class ListLike:
    def __init__(self):
        self._items = list()

    def __getattr__(self, name):
        return getattr(self._items, name)

# Example
a = ListLike()
a.append(1)    # Works
a.insert(0, 2) # Works
a.sort()       # Works
len(a) # Fails. No __len__() method
a[0]   # Fails. No __getitem__() method
```

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

```python
class Account(object):
    __slots__ = ('owner', 'balance')
    ...
```

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
        raise AttributeError("Can't delete attribute")

class Integer(Typed):
    expected_type = int

class Float(Typed):
    expected_type = float

class String(Typed):
    expected_type = str

# Example use:
class Account:
    owner = String()
    balance = Float()

    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

a = Account('Guido', 1000.0)
b = a.owner           # Calls Account.owner.__get__(a, Account)
a.owner = 'Eva'      # Calls Account.owner.__set__(a, 'Eva')
del a.owner          # Calls Account.owner.__delete__(a)
```



```python
>>> a = Account('Guido', 1000.0)
>>> a.__dict__
{'owner': 'Guido', 'balance': 1000.0 }
>>> a.balance = 'a lot'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "descrip.py", line 63, in __set__
    raise TypeError(f'Expected {self.expected_type}')
TypeError: Expected <class 'float'>
>>>
```

```python
>>> Account.balance
<__main__.Float object at 0x110606710>
>>>
```

```python
import types

class classmethod:
    def __init__(self, func):
        self.__func__ = func

    # Return a bound method with cls as first argument
    def __get__(self, instance, cls):
        return types.MethodType(self.__func__, cls)

class staticmethod:
    def __init__(self, func):
        self.__func__ = func

    # Return the bare function
    def __get__(self, instance, cls):
        return self.__func__
```

```python
class Lazy:
    def __init__(self, func):
        self.func = func

    def __set_name__(self, cls, name):
        self.key = name

    def __get__(self, instance, cls):
        if instance:
            value = self.func(instance)
            instance.__dict__[self.key] = value
            return value
        else:
            return self

class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

area = Lazy(lambda self: self.width * self.height)
perimeter = Lazy(lambda self: 2*self.width + 2*self.height)

>>> r = Rectangle(3, 4)
>>> r.__dict__
{'width': 3, 'height': 4 }
>>> r.area
12
>>> r.perimeter
14
>>> r.__dict__
{'width': 3, 'height': 4, 'area': 12, 'perimeter': 14 }
>>>
```

```python
debug = True

class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    if debug:
        import logging
        log = logging.getLogger(f'{__module__}.{__qualname__}')
        def deposit(self, amount):
            Account.log.debug('Depositing %f', amount)
            self.balance += amount

        def withdraw(self, amount):
            Account.log.debug('Withdrawing %f', amount)
            self.balance -= amount
    else:
        def deposit(self, amount):
            self.balance += amount

        def withdraw(self, amount):
            self.balance -= amount
```

## types.new_class()

```python
import types

# Some methods (not in a class)
def __init__(self, owner, balance):
    self.owner = owner
    self.balance = balance

def deposit(self, amount):
    self.balance -= amount

def withdraw(self, amount):
    self.balance += amount

methods = {
    '__init__': __init__,
    'deposit': deposit,
    'withdraw': withdraw,
}

Account = types.new_class('Account', (),
                          exec_body=lambda ns: ns.update(methods))

# You now have a class
a = Account('Guido', 1000.0)
a.deposit(50)
a.withdraw(25)
```

```python
class Integer(Typed):
    expected_type = int

class Float(Typed):
    expected_type = float

class String(Typed):
    expected_type = str

typed_classes = [
    ('Integer', int),
    ('Float', float),
    ('String', str),
    ('Bool', bool),
    ('Tuple', tuple),
]

globals().update(
    (name, types.new_class(name, (Typed,), 
                               exec_body=lambda ns: ns.update(expected_type=ty)))
    for name, ty in typed_classes
)
```

```python
Account = type('Account', (), methods)
```

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

isinstance(Account, object)    # -> True
```

```python
>>> Account.__class__
<type 'type'>
>>>
```

```python
# Step 1: Create the class namespace
namespace = type.__prepare__('Account', ())

# Step 2: Execute the class body
exec('''
def __init__(self, owner, balance):
    self.owner = owner
    self.balance = balance

def deposit(self, amount):
    self.balance += amount

def withdraw(self, amount):
    self.balance -= amount
''', globals(), namespace)

# Step 3: Create the final class object
Account = type('Account', (), namespace)
```

```python
class Account(metaclass=type):
    ...
```

```python
class mytype(type):

    # Creates the class namespace
    @classmethod
    def __prepare__(meta, clsname, bases):
        print("Preparing:", clsname, bases)
        return super().__prepare__(clsname, bases)

    # Creates the class instance after body has executed
    @staticmethod
    def __new__(meta, clsname, bases, namespace):
        print("Creating:", clsname, bases, namespace)
        return super().__new__(meta, clsname, bases, namespace)

    # Initializes the class instance
    def __init__(cls, clsname, bases, namespace):
        print("Initializing:", clsname, bases, namespace)
        super().__init__(clsname, bases, namespace)

    # Creates new instances of the class
    def __call__(cls, *args, **kwargs):
        print("Creating instance:", args, kwargs)
        return super().__call__(*args, **kwargs)

# Example
class Base(metaclass=mytype):
    pass

# Definition of the Base produces the following output
```

```python
# Preparing: Base ()
# Creating: Base () {'__module__': '__main__', '__qualname__': 'Base'}
# Initializing: Base () {'__module__': '__main__', '__qualname__': 'Base'}

b = Base()
# Creating instance: () {}
```

```python
class Account(Base):
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

print(type(Account))  # -> <class 'mytype'>
```

```python
import inspect

class SlotMeta(type):
    @staticmethod
    def __new__(meta, clsname, bases, methods):
        if '__init__' in methods:
            sig = inspect.signature(methods['__init__'])
            __slots__ = tuple(sig.parameters)[1:]
        else:
            __slots__ = ()
        methods['__slots__'] = __slots__
        return super().__new__(meta, clsname, bases, methods)

class Base(metaclass=SlotMeta):
    pass

# Example
class Point(Base):
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

```python
class NoDupeDict(dict):
    def __setitem__(self, key, value):
        if key in self:
            raise AttributeError(f'{key} already defined')
        super().__setitem__(key, value)

class NoDupeMeta(type):
    @classmethod
    def __prepare__(meta, clsname, bases):
        return NoDupeDict()

class Base(metaclass=NoDupeMeta):
    pass

# Example
class SomeClass(Base):
    def yow(self):
        print('Yow!')

    def yow(self, x):
        print('Different Yow!') # Fails. Already defined
```

```python
# module.py

a = 37

def func():
    print(f'func says that a is {a}')

class SomeClass:
    def method(self):
        print('method says hi')

print('loaded module')
```

```python
>>> import module
loaded module
>>> module.a
37
>>> module.func()
func says that a is 37
>>> s = module.SomeClass()
>>> s.method()
method says hi
>>>
```

```python
import socket, os, re
```

```python
import module as mo
mo.func()
```

```python
import numpy as np
import pandas as pd
import matplotlib as plt
...
```

```python
if platform == 'unix':
    import unixmodule as module
elif platform == 'windows':
    import winmodule as module

...
r = module.func()
```

```python
def f(x):
    import math
    return math.sin(x) + math.cos(x)
```

```python
from module import func  # Imports module and puts func in current namespace
func()                  # Calls func() defined in module
module.func()           # Fails. NameError: module
```

```python
from module import func, SomeClass
```

```python
>>> from module import func
>>> a = 42
>>> func()
func says that a is 37
>>> func.__module__
'module'
>>> func.__globals__['a']
37
>>>
```



```python
from module import a, func

a = 42              # Modify the variable
func()              # Prints "func says a is 37"
print(a)            # Prints "42"
```

# 将所有定义加载到当前命名空间

```python
from module import *
```

```python
# module: module.py
__all__ = [ 'func', 'SomeClass' ]

a = 37                  # Not exported

def func():            # Exported
    ...

class SomeClass:        # Exported
    ...
```

```python
from math import *
from random import *
from statistics import *

a = gauss(1.0, 0.25) # From which module?
```

```python
from math import sin, cos, sqrt
from random import gauss
from statistics import mean

a = gauss(1.0, 0.25)
```

# moda.py

```python
import modb

def func_a():
    modb.func_b()

class Base:
    pass
```

# modb.py

```python
import moda

def func_b():
    print('B')

class Child(moda.Base):
    pass
```

# moda.py

```python
def func_a():
    import modb
    modb.func_b()

class Base:
    pass
```

# moda.py

```python
def func_a():
    modb.func_b()

class Base:
    pass

import modb  # Must be after Base is defined
```

# modb.py

```python
import base

def func_b():
    print('B')

class Child(base.Base):
    pass
```

```python
>>> import module
>>> import importlib
>>> importlib.reload(module)
loaded module
<module 'module' from 'module.py'>
>>>
```

```python
@dataclass
class Point:
    x: float
    y: float
```

```bash
$ env PYTHONPATH=/some/path python3 script.py
```

```python
import sys
sys.path.append('mymodules.zip')
import foo, bar
```

```python
sys.path.append('/tmp/modules.zip/lib/python')
```

```python
# Check if running as a program
if __name__ == '__main__':
    # Yes. Running as the main script
    statements
else:
    # No, I must have been imported as a module
    statements
```

```
graphics/
    __init__.py
    primitive/
        __init__.py
        lines.py
        fill.py
        text.py
```

```
...
graph2d/
    __init__.py
    plot2d.py
...

...
graph3d/
    __init__.py
    plot3d.py
...
```

```
formats/
    __init__.py
    gif.py
    png.py
    tiff.py
    jpeg.py
```

```python
# Full path
import graphics.primitive.fill
...
graphics.primitive.fill.floodfill(img, x, y, color)

# Load a specific submodule
from graphics.primitive import fill
...
fill.floodfill(img, x, y, color)

# Load a specific function from a submodule
from graphics.primitive.fill import floodfill
...
floodfill(img, x, y, color)
```

```python
# graphics/primitives/fill.py

# Fully qualified submodule import
from graphics.primitives import lines
```

```python
# graphics/primitives/fill.py

# Package-relative import
from . import lines
```

# graphics/graph2d/plot2d.py

```python
from ..primitive import lines
```

```python
# graphics/graph2d/plot2d.py
from ..primitive import lines, text

class Plot2D:
    ...

if __name__ == '__main__':
    print('Testing Plot2D')
    p = Plot2D()
    ...
```

```bash
bash $ python3 graphics/graph2d/plot2d.py
Traceback (most recent call last):
  File "graphics/graph2d/plot2d.py", line 1, in <module>
    from ..primitive import line, text
ValueError: attempted relative import beyond top-level package
bash $ 
```

```bash
bash $ cd graphics/graph2d/
bash $ python3 plot2d.py
Traceback (most recent call last):
  File "plot2d.py", line 1, in <module>
    from ..primitive import line, text
ValueError: attempted relative import beyond top-level package
bash $ 
```

```bash
bash $ python3 -m graphics.graph2d.plot2d
Testing Plot2D
bash $
```

```python
import graphics
graphics.primitive.fill.floodfill(img,x,y,color)  # Fails!
```

# graphics/__init__.py

```python
from .graph2d.plot2d import Plot2D
from .graph3d.plot3d import Plot3D
```

```python
from graphics import Plot2D

plt = Plot2D(100, 100)
plt.clear()
...
```

```python
# graphics/graph2d/plot2d.py

__all__ = ['Plot2D']

class Plot2D:
    ...
```

```python
# graphics/graph2d/__init__.py

# Only loads names explicitly listed in __all__ variables
from .plot2d import *

# Propagate the __all__ up to next level (if desired)
__all__ = plot2d.__all__
```

```python
# graphics/__init__.py

from .graph2d import *
from .graph3d import *

# Consolidate exports
__all__ = [
    *graph2d.__all__,
    *graph3d.__all__,
]
```

```
mycode/
  resources/
    data.json
    __init__.py
    spam.py
    yow.py
```

```python
# mycode/spam.py

import pkgutil
import json

def func():
    rawdata = pkgutil.get_data(__package__,
                                'resources/data.json')
    textdata = rawdata.decode('utf-8')
    data = json.loads(textdata)
    print(data)
```

## mymodule.py

```python
...
```

```python
The doc string
"""

# Type hints (placed into __annotations__)
x: int
y: float
...
```

```text
spam-project/
    README.txt
    Documentation.txt
    spam/                # A package of code
        __init__.py
        foo.py
        bar.py
    runspam.py            # A script to run as: python runspam.py
```

```python
# setup.py
from setuptools import setup

setup(name="spam",
      version="0.0",
      packages=['spam'],
      scripts=['runspam.py'],
)
```

```bash
bash $ python setup.py sdist
...
bash $
```

```shell
$ python3 -m pip install spam-1.0.tar.gz
```

```python
# 指定一个字节字面量（注意 b' 前缀）
a = b'hello'

# 从整数列表指定字节
b = bytes([0x68, 0x65, 0x6c, 0x6c, 0x6f])

# 通过部分内容创建并填充 bytearray
c = bytearray()
c.extend(b'world') # c = bytearray(b'world')
c.append(0x21)    # c = bytearray(b'world!')

# 访问字节值
print(a[0])       # --> 打印 104

for x in b:
    print(x) # 输出 104 101 108 108 111
```

```python
d = 'hello'    # 文本 (Unicode)
len(d)         # --> 5
print(d[0])    # 打印 'h'
```

```python
a = b'hello' # bytes (字节)
b = 'hello' # text (文本)
c = 'world' # text (文本)

print(a == b) # -> False
d = a + c # TypeError: 无法将 str 与 bytes 拼接
e = b + c # -> 'helloworld' (两者都是字符串)
```

```python
a = 'hello'               # 文本
b = a.encode('utf-8')    # 编码为字节

c = b'world'              # 字节
d = c.decode('utf-8')    # 解码为文本
```

```python
>>> a = b'Spicy Jalape\xf1o'  # 无效的 UTF-8
>>> a.decode('utf-8')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xf1 in position 12: invalid continuation byte
>>> a.decode('utf-8', 'surrogateescape')
'Spicy Jalapeo'
>>> # 将结果字符串重新编码为字节
>>> _.encode('utf-8', 'surrogateescape')
b'Spicy Jalape\xf1o'
>>> 
```

```python
x = 123.456
format(x, '0.2f') # '123.46'
format(x, '10.4f') # '  123.4560'
format(x, '<*10.2f') # '123.46****'
```

```python
name = 'Elwood'
r = format(name, '<10')  # r = 'Elwood    '
r = format(name, '>10')  # r = '    Elwood'
r = format(name, '^10')  # r = ' Elwood  '
r = format(name, '^*10') # r = '***Elwood***'
```

```python
x = 123456.78
format(x, '16..2f')  # ' 123,456.78'
```

```python
x = 42
r = format(x, '10d') # r = '        42'
r = format(x, '10x') # r = '         2a'
r = format(x, '10b') # r = '  10101010'
r = format(x, '010b') # r = '0000101010'

y = 3.1415926
r = format(y, '10.2f') # r = '      3.14'
r = format(y, '10.2e') # r = ' 3.14e+00'
r = format(y, '+10.2f') # r = '     +3.14'
r = format(y, '+010.2f') # r = '+000003.14'
r = format(y, '+10.2%') # r = '   +314.16%'
```

```python
f'Value is {x:0.2f}'  # 'Value is 123.46'
f'Value is {x:10.4f}'  # 'Value is  123.4560'
f'Value is {2*x:*<10.2f}' # 'Value is 246.91*****'
```

```python
y = 3.1415926
width = 8
precision = 3

r = f'{y:{width}.{precision}f}'  # r = ' 3.142'
```

```python
x = 123.456
f'{x:.2f}'    # '123.46'
f'{2*x:.2f}'    # '246.91'
```

```python
f'{x!r:spec}'  # 调用 (repr(x).__format__('spec'))
f'{x!s:spec}'  # 调用 (str(x).__format__('spec'))
```

```python
x = 123.456

'Value is {:.2f}'.format(x) # 'Value is 123.46'
'Value is {0:10.2f}'.format(x) # 'Value is 123.4560'
'Value is {val:<*10.2f}'.format(val=x) # 'Value is 123.46*****'
```

```python
name = 'IBM'
shares = 50
price = 490.1

r = '{:>10s} {:10d} {:10.2f}'.format(name, shares, price)
# r = '       IBM         50    490.10'
```



```python
tag = 'p'
text = 'hello world'

r = '<{0}>{1}</{0}>'.format(tag, text)  # r = '<p>hello world</p>'
r = '<{tag}>{text}</{tag}>'.format(tag='p', text='hello world')
```

```python
y = 3.1415926
width = 8
precision = 3

r = 'Value is {0:{1}.{2}f}'.format(y, width, precision)

d = {
    'name': 'IBM',
    'shares': 50,
    'price': 490.1
}

r = '{0[shares]:d} shares of {0[name]} at {0[price]:0.2f}'.format(d)
# r = '50 shares of IBM at 490.10'
```

```python
name = b'ACME'
x = 123.456

b'Value is %0.2f' % x            # b'The value is 123.46'
bytearray(b'Value is %0.2f') % x # b'Value is 123.46'
b'%s = %0.2f' % (name, x)        # b'ACME = 123.46'
```

```python
x = 123.456
b'%10.2f' % x    # b'       123.46'
b'%-10.2f' % x   # b'123.46    '
```

```python
name = 'Dave'

b'Hello %s' % name                      # TypeError!
b'Hello %s' % name.encode('utf-8')     # Ok
```

```python
import logging
log = logging.getLogger(__name__)

log.debug('%s got %d', name, value) # '%s got %d' % (name, value)
```

```python
def main(argv):
    if len(argv) != 3:
        raise SystemExit(
            f'Usage : python {argv[0]} inputfile outputfile\n')
    inputfile = argv[1]
    outputfile = argv[2]
    ...

if __name__ == '__main__':
    import sys
    main(sys.argv)
```

```python
import argparse

def main(argv):
    p = argparse.ArgumentParser(description="This is some program")

    # 一个位置参数
    p.add_argument("infile")

    # 一个带有参数的选项
    p.add_argument("-o","--output", action="store")

    # 一个设置布尔标志的选项
    p.add_argument("-d","--debug", action="store_true", default=False)

    # 解析命令行
    args = p.parse_args(args=argv)

    # 获取选项设置
    infile = args.infile
    output = args.output
    debugmode = args.debug

    print(infile, output, debugmode)

if __name__ == '__main__':
    import sys
    main(sys.argv[1:])
```

```bash
bash $ env SOMEVAR=somevalue python3 somescript.py
```

```python
import os
path = os.environ['PATH']
user = os.environ['USER']
editor = os.environ['EDITOR']
val = os.environ['SOMEVAR']
... 等等 ...
```

```python
os.environ['NAME'] = 'VALUE'
```

```python
# 一次性将文本文件全部读入为字符串
with open('filename.txt', 'rt') as file:
    data = file.read()

# 逐行读取文件
with open('filename.txt', 'rt') as file:
    for line in file:
        ...

# 写入文本文件
with open('out.txt', 'wt') as file:
    file.write('Some output\n')
    print('More output', file=file)
```

```python
open('name.txt')           # 以读取模式打开 "name.txt"
open('name.txt', 'rt')    # 以读取模式打开 "name.txt" (同上)
open('name.txt', 'wt')    # 以写入模式打开 "name.txt"
open('data.bin', 'rb')    # 二进制模式读取
open('data.bin', 'wb')    # 二进制模式写入
```

```python
>>> from pathlib import Path
>>> p = Path('Data/portfolio.csv')
>>> p.__fspath__()
'Data/portfolio.csv'
>>>
```

```python
>>> import os
>>> fd = os.open('/etc/passwd', os.O_RDONLY)  # 整数文件描述符 fd
>>> fd
3
>>> file = open(fd, 'rt')  # 正确的文件对象
>>> file
<_io.TextIOWrapper name=3 mode='rt' encoding='UTF-8'>
>>> data = file.read()
>>>
```

```python
file = open(fd, 'rt', closefd=False)
```

```python
# 打开一个没有 I/O 缓冲的二进制模式文件

with open('data.bin', 'wb', buffering=0) as file:
    file.write(data)
    ...
```

```python
file.write(data)
file.write(data)
...
file.flush()  # 确保所有数据从缓冲区写入
```

```python
with open('file.txt', 'rt',
           encoding='utf-8', errors='replace') as file:
    data = file.read()
```

```python
# 明确要求 '\r\n' 并保持原样
file = open('somefile.txt', 'rt', newline='\r\n')
```

```python
FileIO(filename, mode='r', closefd=True, opener=None)
```

```python
BufferedReader(file [, buffer_size])
BufferedWriter(file [, buffer_size])
BufferedRandom(file [, buffer_size])
```

```python
TextIOWrapper(buffered, [encoding, [errors [, newline [, line_buffering [, write_through]]]]])
```

```python
>>> raw = io.FileIO('filename.txt', 'r')  # 原始二进制模式
>>> buffer = io.BufferedReader(raw)  # 二进制缓冲读取器
>>> file = io.TextIOWrapper(buffer, encoding='utf-8') # 文本模式
>>> 
```

```python
f = open('something.txt', 'rt') # 文本模式文件
fb = f.detach()               # 分离底层二进制模式文件
data = fb.read()              # 返回字节流 (bytes)
```

```python
while True:
    line = file.readline()
    if not line:  # 文件结束 (EOF)
        break
    statements
    ...
```

```python
while (line:=file.readline()):
    statements
    ...
```

```python
for line in file:   # 遍历文件中的所有行
    # 对行执行操作
    ...
```

```python
import sys
sys.stdout.write("Enter your name: ")
name = sys.stdin.readline()
```

```python
name = input("Enter your name: ")
```

```python
import os

names = os.listdir('dirname')
for name in names:
    print(name)
```

```python
import os

# 返回原始的未解码名称
names = os.listdir(b'dirname')
```

```python
import pathlib

for filename in path.Path('dirname').glob('*.txt'):
    print(filename)
```

```python
print('The values are', x, y, z)
```

```python
# 抑制换行符
print('The values are', x, y, z, end='')
```

```python
# 重定向到文件对象 f
print('The values are', x, y, z, file=f)
```

```python
# 在值之间插入逗号
print('The values are', x, y, z, sep=',')
```

```python
def countdown(n):
    while n > 0:
        yield f'T-minus {n}\n'
        n -= 1
    yield 'Kaboom!\n'
```

```python
lines = countdown(5)
f.writelines(lines)
```

```python
for chunk in lines:
    s.sendall(chunk.encode('utf-8'))
```

```python
out = "".join(lines)
```

```python
chunks = []
buffered_size = 0
for chunk in count:
    chunks.append(chunk)
    buffered_size += len(chunk)
    if buffered_size >= MAXBUFFERSIZE:
        outf.write(".".join(chunks))
        chunks.clear()
        buffered_size = 0
outf.write(".".join(chunks))
```

```python
def line_receiver():
    data = bytearray()
    line = None
    linecount = 0
    while True:
        part = yield line
        linecount += part.count(b'\n')
        data.extend(part)
        if linecount > 0:
            index = data.index(b'\n')
            line = bytes(data[:index+1])
            data = data[index+1 :]
            linecount -= 1
        else:
            line = None
```

```python
>>> r = line_receiver()
>>> r.send(None)    # 必要的启动步骤
>>> r.send(b'hello')
>>> r.send(b'world\n it ')
b'hello world\n'
>>> r.send(b'works!')
>>> r.send(b'\n')
b'it works!\n'
>>>
```

```python
r = line_receiver()
data = None
while True:
    while not (line:=r.send(data)):
        data = sock.recv(8192)

    # 处理该行
    ...
```

```python
r = line_receiver()
data = None
while True:
    while not (line:=r.send(data)):
        data = file.read(10000)

    # 处理该行
    ...
```

```python
async def reader(ch):
    r = line_receiver()
    data = None
    while True:
        while not (line:=r.send(data)):
            data = await ch.receive(8192)

        # 处理该行
        ...
```

```python
import pickle
obj = SomeObject()
with open(filename, 'wb') as file:
    pickle.dump(obj, file) # 将对象保存到 f
```

```python
with open(filename, 'rb') as file:
    obj = pickle.load(file)   # 恢复对象
```

```python
obj = SomeObject()

# 将对象转换为字节流
data = pickle.dumps(obj)
...

# 将字节流转换回对象
obj = pickle.loads(data)
```

```python
data = sock.recv(8192)
```

```python
def reader1(sock):
    while (data := sock.recv(8192)):
        print('reader1 got:', data)

def reader2(sock):
    while (data := sock.recv(8192)):
        print('reader2 got:', data)
```

# 问题：如何让 reader1() 和 reader2() 同时运行？

```python
sock.setblocking(False)
```

```python
try:
    data = sock.recv(8192)
except BlockingIOError as e:
    # 没有可用数据
    ...
```

```python
def reader1(sock):
    try:
        data = sock.recv(8192)
        print('reader1 got:', data)
    except BlockingIOError:
        pass

def reader2(sock):
    try:
        data = sock.recv(8192)
        print('reader2 got:', data)
    except BlockingIOError:
        pass

def run(sock1, sock2):
    sock1.setblocking(False)
    sock2.setblocking(False)
    while True:
        reader1(sock1)
```

```python
reader1(sock1),
reader2(sock2)
```



以下代码示例展示了 Python 中多种常见的编程模式和技术，包括事件循环、多线程、异步编程、网络编程、数据编码、Web 表单处理、配置文件解析、CSV 文件操作、错误处理、文件锁、哈希计算、HTTP 服务器、文件对象模拟、JSON 数据处理、日志记录以及文件路径操作。

首先，我们来看一个使用 `selectors` 模块实现的事件驱动 I/O 多路复用示例。该示例创建了一个 `DefaultSelector` 实例，并注册了两个 socket 及其对应的读取函数。主循环通过 `selector.select()` 等待事件发生，然后根据事件类型调用相应的处理函数。

```python
from selectors import DefaultSelector, EVENT_READ, EVENT_WRITE

def run(sock1, sock2):
    selector = DefaultSelector()
    selector.register(sock1, EVENT_READ, data=reader1)
    selector.register(sock2, EVENT_READ, data=reader2)
    # 等待事件发生
    while True:
        for key, evt in selector.select():
            func = key.data
            func(key.fileobj)
```

接下来是一个使用 `threading` 模块实现的多线程示例。该示例定义了两个读取函数，分别从各自的 socket 中读取数据并打印。然后创建两个线程分别运行这两个函数，并启动它们。

```python
import threading

def reader1(sock):
    while (data := sock.recv(8192)):
        print('reader1 got:', data)

def reader2(sock):
    while (data := sock.recv(8192)):
        print('reader2 got:', data)

t1 = threading.Thread(target=reader1, args=[sock1])
t2 = threading.Thread(target=reader2, args=[sock2])

# 启动线程
```

启动线程后，主程序会等待两个线程执行完毕。

```python
t1.start()
t2.start()

# 等待线程结束
t1.join()
t2.join()
```

下面是一个使用 `asyncio` 模块实现的异步 I/O 示例。该示例定义了异步的 `reader1` 和 `reader2` 函数，它们通过事件循环的 `sock_recv` 方法异步读取数据。`main` 函数创建两个任务并等待它们完成。

```python
import asyncio

async def reader1(sock):
    loop = asyncio.get_event_loop()
    while (data := await loop.sock_recv(sock, 8192)):
        print('reader1 got:', data)

async def reader2(sock):
    loop = asyncio.get_event_loop()
    while (data := await loop.sock_recv(sock, 8192)):
        print('reader2 got:', data)

async def main(sock1, sock2):
    loop = asyncio.get_event_loop()
    t1 = loop.create_task(reader1(sock1))
    t2 = loop.create_task(reader2(sock2))

    # 等待任务结束
    await t1
    await t2

...
# 运行
asyncio.run(main(sock1, sock2))
```

接下来是一个使用 `asyncio` 实现的异步 TCP 回显服务器。该服务器监听指定地址，接受客户端连接，并为每个连接创建一个异步任务来处理数据回显。

```python
import asyncio
from socket import *

async def echo_server(address):
    loop = asyncio.get_event_loop()
    sock = socket(AF_INET, SOCK_STREAM)
    sock.setsockopt(SOL_SOCKET, SO_REUSEADDR, 1)
    sock.bind(address)
    sock.listen(5)
    sock.setblocking(False)
    print('Server listening at', address)
    with sock:
        while True:
            client, addr = await loop.sock_accept(sock)
            print('Connection from', addr)
            loop.create_task(echo_client(loop, client))

async def echo_client(loop, client):
    with client:
        while True:
            data = await loop.sock_recv(client, 10000)
            if not data:
                break
            await loop.sock_sendall(client, b'Got:' + data)
    print('Connection closed')

if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    loop.create_task(echo_server((' ', 25000)))
    loop.run_forever()
```

以下示例演示了如何使用 `binascii` 模块进行十六进制和 Base64 编码的转换。

```python
>>> binascii.b2a_hex(b'hello')
b'68656c6c6f'
>>> binascii.a2b_hex(_)
b'hello'
>>> binascii.b2a_base64(b'hello')
b'aGVsbG8=\n'
>>> binascii.a2b_base64(_)
b'hello'
>>>
```

Python 3 还提供了更简洁的编码方法，例如使用 `bytes.hex()` 和 `bytes.fromhex()`，以及 `base64` 模块。

```python
>>> a = b'hello'
>>> a.hex()
'68656c6c6f'
>>> bytes.fromhex(_)
b'hello'
>>> import base64
>>> base64.b64encode(a)
b'aGVsbG8='
>>>
```

下面是一个 HTML 表单示例，用于收集用户的联系信息。该表单通过 POST 方法将数据提交到 `cgi-bin/register.py` 脚本。

```html
<form method="POST" action="cgi-bin/register.py">
    <p>
    To register, please provide a contact name and email address.
    </p>
    <div>
        <input name="name" type="text">Your name:</input>
    </div>
    <div>
        <input name="email" type="email">Your email:</input>
    </div>
    <div class="modal-footer justify-content-center">
        <input type="submit" name="submit" value="Register"></input>
    </div>
</form>
```

对应的 Python CGI 脚本处理表单提交的数据，并返回一个重定向响应或错误信息。

```python
#!/usr/bin/env python
import cgi

try:
    form = cgi.FieldStorage()
    name = form.getvalue('name')
    email = form.getvalue('email')
    # Validate the responses and do whatever
    ...
    # Produce an HTML result (or redirect)
    print("Status: 302 Moved\r")
    print("Location: https://www.mywebsite.com/thanks.html\r")
    print("\r")
except Exception as e:
    print("Status: 501 Error\r")
    print("Content-type: text/plain\r")
    print("\r")
    print("Some kind of error occurred.\r")
```

## config.ini

配置文件通常使用 INI 格式，如下所示。该文件包含两个节（`section1` 和 `section2`），每个节中定义了若干键值对。注释以分号（`;`）开头。

```ini
; A comment
[section1]
name1 = value1
name2 = value2

[section2]
; Alternative syntax
name1: value1
name2: value2
```

Python 的 `configparser` 模块可以方便地读取和解析此类配置文件。

```python
import configparser

# Create a config parser and read a file
cfg = configparser.ConfigParser()
cfg.read('config.ini')

# Extract values
a = cfg.get('section1', 'name1')
b = cfg.get('section2', 'name2')
...
```

CSV（逗号分隔值）文件是常见的数据交换格式。以下示例展示了如何读取 CSV 文件并将其内容处理为元组列表。

```python
import csv

# Read a CSV file into a list of tuples
def read_csv_data(filename):
    with open(filename, newline='') as file:
        rows = csv.reader(file)
        # First line is often a header. This reads it
        headers = next(rows)
        # Now read the rest of the data
        for row in rows:
            # Do something with row
            ...
```

同样，也可以将 Python 数据写入 CSV 文件。

```python
# Write Python data to a CSV file
def write_csv_data(filename, headers, rows):
    with open(filename, 'w', newline='') as file:
        out = csv.writer(file)
        out.writerow(headers)
        out.writerows(rows)
```

对于包含标题行的 CSV 文件，可以使用 `csv.DictReader` 将每一行转换为字典，便于按列名访问数据。

```python
import csv

def find_nearby(filename):
    with open(filename, newline='') as file:
        rows = csv.DictReader(file)
        for row in rows:
            lat = float(row['latitude'])
            lon = float(row['longitude'])
            if close_enough(lat, lon):
                print(row)
```

在文件操作中，处理错误是必要的。以下示例展示了如何捕获 `OSError` 并针对磁盘空间不足（`errno.ENOSPC`）给出特定提示，其他错误则重新抛出。

```python
import errno

def write_data(file, data):
    try:
        file.write(data)
    except OSError as e:
        if e.errno == errno.ENOSPC:
            print("You're out of disk space!")
        else:
            raise  # Some other error. Propagate
```

在多进程或多线程环境中，文件锁可以防止数据竞争。以下示例使用 `fcntl.flock()` 对文件加排他锁。

```python
import fcntl

with open("somefile", "r") as file:
    try:
        fcntl.flock(file.fileno(), fcntl.LOCK_EX)
        # Use the file
        ...
    finally:
        fcntl.flock(file.fileno(), fcntl.LOCK_UN)
```

`hashlib` 模块提供了多种哈希算法。以下示例演示了如何使用 SHA-256 算法计算数据的哈希值。

```python
>>> h = hashlib.new('sha256')
>>> h.update(b'Hello')  # Feed data
>>> h.update(b'World')
>>> h.digest()
b'\x81\xa5\x81\xa6\x06\xd0\xb0\xf4 @J\x101\x173\xcf\x81\xb1\x90\xd6\x0e\xbf\x0b\xcd\xa3\x21\x82\x2w\xd9\xad\x9f\x14n'
>>> h.hexdigest()
'a591a640bf420404a011733cfb7b190d62c65bf0bcda32b57d9ad9f146e'
>>> h.digest_size
32
>>>
```

Python 内置的 `http.server` 模块可以快速启动一个简单的 HTTP 文件服务器。

```bash
$ python -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

`io.StringIO` 允许将字符串当作文件对象使用。以下示例展示了如何用真实文件和模拟文件调用同一个函数。

```python
# Function that expects a file
def greeting(file):
    file.write('Hello\n')
    file.write('World\n')

# Call the function using a real file
with open('out.txt', 'w') as file:
    greeting(file)

# Call the function with a "fake" file
import io
file = io.StringIO()
greeting(file)

# Get the resulting output
output = file.getvalue()
```

`io.StringIO` 也可以用于逐行读取字符串数据。

```python
file = io.StringIO('hello\nworld\n')
while (line := file.readline()):
    print(line, end='')
```

`json` 模块用于处理 JSON 数据。以下示例展示了如何将 Python 字典序列化为 JSON 字符串。

```python
>>> import json
>>> data = {'name': 'Mary A. Python', 'email': 'mary123@python.org' }
>>> s = json.dumps(data)
>>> s
'{"name": "Mary A. Python", "email": "mary123@python.org"}'
>>>
```

反过来，也可以将 JSON 字符串反序列化为 Python 字典。

```python
>>> d = json.loads(s)
>>> d == data
True
>>>
```

`logging` 模块提供了灵活的日志记录功能。以下示例展示了如何获取一个模块级别的 logger 并记录不同级别的日志消息。

```python
import logging
log = logging.getLogger(__name__)

# Function that uses logging
def func(args):
    log.debug("A debugging message")
    log.info("An informational message")
    log.warning("A warning message")
    log.error("An error message")
    log.critical("A critical message")

# Configuration of logging (ocurs one at program startup)
if __name__ == '__main__':
    logging.basicConfig(
        level=logging.WARNING,
        filename="output.log"
    )
```

`os.path` 模块提供了路径操作函数。以下示例演示了如何拆分和拼接文件路径。

```python
>>> filename = '/Users/beazley/Desktop/old/data.csv'
>>> os.path.split(filename)
('/Users/beazley/Desktop/old', 'data.csv')
>>> os.path.join('/Users/beazley/Desktop', 'out.txt')
'/Users/beazley/Desktop/out.txt'
>>>
```

以下函数展示了如何清理数据文件中的每一行，并将结果写入新文件。

```python
import os.path

def clean_line(line):
    # Line up a line (whatever)
    return line.strip().upper() + '\n'

def clean_data(filename):
    dirname, basename = os.path.split(filename)
    newname = os.path.join(dirname, basename+'.clean')
    with open(newname, 'w') as out_f:
        with open(filename, 'r') as in_f:
            for line in in_f:
                out_f.write(clean_line(line))
```

最后，以下函数递归地计算文件或目录占用的磁盘空间大小。

```python
import os.path

def compute_usage(filename):
    if os.path.isfile(filename):
        return os.path.getsize(filename)
    elif os.path.isdir(filename):
        return sum(compute_usage(os.path.join(filename, name))
                   for name in os.listdir(filename))
    else:
        raise RuntimeError('Unsupported file kind')
```



```python
from pathlib import Path

filename = Path('/Users/beazley/old/data.csv')
>>> filename.name
'data.csv'
>>> filename.parent
Path('/Users/beazley/old')
>>> filename.parent / 'newfile.csv'
Path('/Users/beazley/old/newfile.csv')
>>> filename.parts
('/', 'Users', 'beazley', 'old', 'data.csv')
>>> filename.with_suffix('.csv.clean')
Path('/Users/beazley/old/data.csv.clean')
>>>
```

```python
import pathlib

def compute_usage(filename):
    pathname = pathlib.Path(filename)
    if pathname.is_file():
        return pathname.stat().st_size
    elif pathname.is_dir():
        return sum(path.stat().st_size
                  for path in pathname.rglob('*')
                  if path.is_file())
    else:
        raise RuntimeError('Unsupported file kind')
```

```python
>>> text = 'Today is 3/27/2018. Tomorrow is 3/28/2018.'
>>> # Find all occurrences of a date
>>> import re
>>> re.findall(r'\d+/\d+/\d+', text)
['3/27/2018', '3/28/2018']
>>> # Replace all occurrences of a date with replacement text
>>> re.sub(r'(\d+)/(\d+)/(\d+)', r'\3-\1-\2', text)
'Today is 2018-3-27. Tomorrow is 2018-3-28.'
>>>
```

```python
import shutil

shutil.copy(srcfile, dstfile)
shutil.move(srcfile, dstfile)
shutil.copytree(srcdir, dstdir)
```

```python
import select

# Collections of objects representing file descriptors. Must be
# integers or objects with a fileno() method.
want_to_read = [ ... ]
want_to_write = [ ... ]
check_exceptions = [ ... ]

# Timeout (or None)
timeout = None

# Poll for I/O
can_read, can_write, have_exceptions = \
    select.select(want_to_read, want_to_write, check_exceptions, timeout)

# Perform I/O operations
for file in can_read:
    do_read(file)
for file in can_write:
    do_write(file)

# Handle exceptions
for file in have_exceptions:
    handle_exception(file)
```

```python
import smtplib

fromaddr = "someone@some.com"
toaddrs = ["recipient@other.com" ]
amount = 123.45
msg = f"""From: {fromaddr}
Pay {amount} bitcoin or else.  We're watching.
"""

server = smtplib.SMTP('localhost')
server.sendmail(fromaddr, toaddrs, msg)
server.quit()
```

```python
from socket import socket, AF_INET, SOCK_STREAM

sock = socket(AF_INET, SOCK_STREAM)
sock.connect(('python.org', 80))
sock.send(b'GET /index.html HTTP/1.0\r\n\r\n')
parts = []
while True:
    part = sock.recv(10000)
    if not part:
        break
    parts.append(part)
parts = b''.join(parts)
print(parts)
```

```python
from socket import socket, AF_INET, SOCK_STREAM

def echo_server(address):
    sock = socket(AF_INET, SOCK_STREAM)
    sock.bind(address)
    sock.listen(1)
    while True:
        client, addr = sock.accept()
        echo_handler(client, addr)

def echo_handler(client, addr):
    print('Connection from:', addr)
    with client:
        while True:
            data = client.recv(10000)
            if not data:
                break
            client.sendall(data)
    print('Connection closed')

if __name__ == '__main__':
    echo_server(('', 25000))
```

```python
# udp.py

from socket import socket, AF_INET, SOCK_DGRAM

def run_server(address):
    sock = socket(AF_INET, SOCK_DGRAM)    # 1. 创建一个 UDP 套接字
    sock.bind(address)                    # 2. 绑定到地址/端口
    while True:
        msg, addr = sock.recvfrom(2000)    # 3. 获取一条消息
        # ... 执行某些操作
        response = b'world'
        sock.sendto(response, addr)        # 4. 发回响应

def run_client(address):
    sock = socket(AF_INET, SOCK_DGRAM)    # 1. 创建一个 UDP 套接字
    sock.sendto(b'hello', address)        # 2. 发送一条消息
    response, addr = sock.recvfrom(2000)  # 3. 获取响应
    print("Received:", response)
    sock.close()

if __name__ == '__main__':
    import sys
    if len(sys.argv) != 4:
        raise SystemExit('Usage: udp.py [-client|-server] hostname port')
    address = (sys.argv[2], int(sys.argv[3]))
    if sys.argv[1] == '-server':
        run_server(address)
    elif sys.argv[1] == '-client':
        run_client(address)
```

# 消息格式：所有值均为“大端字节序”

```cpp
struct Message {
    unsigned short msgid;    // 16 位无符号整数
    unsigned int sequence;   // 32 位序列号
    float x;                // 32 位浮点数
    float y;                // 32 位浮点数
}
```

```python
>>> import struct
>>> data = struct.pack('>HIff', 123, 456, 1.23, 4.56)
>>> data
b'\x00{\x00\x00\x00-?\x9dp\xa4@\x91\xeb\x85'
>>> struct.unpack('>HIff', data)
(123, 456, 1.230000190734863, 4.559997942779541)
```

```python
import subprocess

# 运行 'netstat -a' 命令并收集其输出
try:
    out = subprocess.check_output(['netstat', '-a'])
except subprocess.CalledProcessError as e:
    print("It failed:", e)

text = out.decode('utf-8')
```

```python
import subprocess

# wc 是一个返回行数、单词数和字节数计数的程序
p = subprocess.Popen(['wc'],
                      stdin=subprocess.PIPE,
                      stdout=subprocess.PIPE)

# 向子进程发送数据
p.stdin.write(b'hello world\nthis is a test\n')
p.stdin.close()

# 读取回传数据
out = p.stdout.read()
print(out)
```

```python
import tempfile

with tempfile.TemporaryFile() as f:
    f.write(b'Hello World')
    f.seek(0)
    data = f.read()
    print('Got:', data)

with tempfile.TemporaryDirectory() as dirname:
    # 使用目录 dirname
    ...
```

```python
import textwrap

text = """look into my eyes
look into my eyes
the eyes the eyes the eyes the eyes
not around the eyes
don't look around the eyes
look into my eyes you're under
"""

wrapped = textwrap.wrap(text, width=81)
print('\n'.join(wrapped))
# 输出结果：
# look into my eyes look into my eyes the
# eyes the eyes the eyes not around the
# eyes don't look around the eyes look
# into my eyes you're under

print(textwrap.indent(text, ' '))

# 输出结果：
#     look into my eyes
#     look into my eyes
#     the eyes the eyes the eyes
#     not around the eyes
#     don't look around the eyes
#     look into my eyes you're under
```

```python
import threading
import time

def countdown(n):
    while n > 0:
        print('T-minus', n)
        n -= 1
        time.sleep(1)

t = threading.Thread(target=countdown, args=[10])
t.start()
t.join()  # 等待线程结束

# 守护线程示例
t = threading.Thread(target=countdown, args=[10], daemon=True)
```

```python
import threading
import time

must_stop = False

def countdown(n):
    while n > 0 and not must_stop:
        print('T-minus', n)
        n -= 1
        time.sleep(1)
```

```python
import threading

class Counter:
    def __init__(self):
        self.value = 0
        self.lock = threading.Lock()

    def increment(self):
        with self.lock:
            self.value += 1

    def decrement(self):
        with self.lock:
            self.value -= 1
```

```python
import threading
import time

def step1(evt):
    print('Step 1')
    time.sleep(5)
    evt.set()

def step2(evt):
    evt.wait()
    print('Step 2')

evt = threading.Event()
threading.Thread(target=step1, args=[evt]).start()
threading.Thread(target=step2, args=[evt]).start()
```

```python
import threading
import queue
import time

def producer(q):
    for i in range(10):
        print('Producing:', i)
        q.put(i)
    print('Done')
    q.put(None)

def consumer(q):
    while True:
        item = q.get()
        if item is None:
            break
        print('Consuming:', item)
    print('Goodbye')

q = queue.Queue()
threading.Thread(target=producer, args=[q]).start()
threading.Thread(target=consumer, args=[q]).start()
```

```python
>>> from urllib.request import urlopen
>>> u = urlopen('http://www.python.org')
>>> data = u.read()
```

```python
from urllib.parse import urlencode
from urllib.request import urlopen

form = {
    'name': 'Mary A. Python',
    'email': 'mary123@python.org'
}

data = urlencode(form)
u = urlopen('http://httpbin.org/post', data.encode('utf-8'))
response = u.read()
```

```python
>>> url = 'http://httpbin.org/get?name=Dave&n=42'
>>> from urllib.parse import urlparse
>>> urlparse(url)
ParseResult(scheme='http', netloc='httpbin.org', path='/get', params='', query='name=Dave&n=42', fragment='')
```



```python
>>> d = {}
>>> d['Jalape\xf1o'] = 'spicy'
>>> d['Jalapen\u0303o'] = 'mild'
>>> d
{'jalapeño': 'spicy', 'jalapeño': 'mild' }
```

```xml
<?xml version="1.0" encoding="iso-8859-1"?>
<recipe>
	<title>Famous Guacamole</title>
	<description>A southwest favorite!</description>
	<ingredients>
		<item num="4"> Large avocados, chopped </item>
		<item num="1"> Tomato, chopped </item>
		<item num="1/2" units="C"> White onion, chopped </item>
		<item num="2" units="tbl"> Fresh squeezed lemon juice </item>
		<item num="1"> Jalapeno pepper, diced </item>
		<item num="1" units="tbl"> Fresh cilantro, minced </item>
		<item num="1" units="tbl"> Garlic, minced </item>
		<item num="3" units="tsp"> Salt </item>
		<item num="12" units="bottles"> Ice-cold beer </item>
	</ingredients>
	<directions>
Combine all ingredients and hand whisk to desired consistency.
Serve and enjoy with ice-cold beers.
	</directions>
</recipe>
```

```python
from xml.etree.ElementTree import ElementTree

doc = ElementTree(file="recipe.xml")
title = doc.find('title')
print(title.text)

# 另一种方法（仅获取元素文本）
print(doc.findtext('description'))

# 遍历多个元素
for item in doc.findall('ingredients/item'):
    num = item.get('num')
    units = item.get('units', '')
    text = item.text.strip()
    print(f'{num} {units} {text}')
```

```python
delattr(object, attr)
```

`dict([m]) or dict(key1=value1, key2=value2, ...)`

```python
enumerate(iter, start=0)
```

`eval(expr [, globals [, locals]])`

`exec(code [, globals [, locals]])`

`filter(function, iterable)`

`max(s [, args, ...], *, default=obj, key=func)`

```python
min(s [, args, ...], *, default=obj, key=func)
```

```python
open(filename [, mode [, bufsize [, encoding [, errors [, newline [, closefd]]]]]])
```

```python
print(value, ..., *, sep=separator, end=ending, file=outfile)
```

```python
property([fget [, fset [, fdel [, doc]]]])
```

```python
class SomeClass:
    x = property(doc='This is property x')
    @x.getter
    def x(self):
        print('getting x')

    @x.setter
    def x(self, value):
        print('setting x to', value)

    @x.deleter
    def x(self):
        print('deleting x')
```

```python
range([start,] stop [, step])
```

`setattr(object, name, value)`

```python
slice([start,] stop [, step])
```

```python
sorted(iterable, *, key=keyfunc, reverse=reverseflag)
```

```python
class B(A):
    def foo(self):
        super().foo()  # Invoke foo() defined by superclasses.
```

`tuple([items])`

```python
try:
    # Some operation
    ...
except ArithmeticError as e:
    # Math error
```

## 目录

- 封面
- 关于本书
- 半标题页
- 标题页
- 版权页
- 目录
- 前言

## 1. Python 基础

- 1.1 运行 Python
- 1.2 Python 程序
- 1.3 原始类型、变量与表达式
- 1.4 算术运算符
- 1.5 条件判断与控制流
- 1.6 文本字符串
- 1.7 文件输入与输出
- 1.8 列表
- 1.9 元组
- 1.10 集合
- 1.11 字典
- 1.12 迭代与循环
- 1.13 函数
- 1.14 异常
- 1.15 程序终止
- 1.16 对象与类
- 1.17 模块
- 1.18 脚本编写
- 1.19 包
- 1.20 构建应用程序结构
- 1.21 管理第三方包
- 1.22 Python：契合你的思维

## 2. 运算符、表达式与数据操作

- 2.1 字面量
- 2.2 表达式与位置
- 2.3 标准运算符
- 2.4 就地赋值
- 2.5 对象比较
- 2.6 有序比较运算符
- 2.7 布尔表达式与真值
- 2.8 条件表达式
- 2.9 涉及可迭代对象的运算
- 2.10 序列操作
- 2.11 可变序列操作
- 2.12 集合操作
- 2.13 映射操作
- 2.14 列表、集合与字典推导式
- 2.15 生成器表达式
- 2.16 属性 (`.`) 运算符
- 2.17 函数调用 `()` 运算符
- 2.18 求值顺序
- 2.19 结语：数据的秘密生活

## 3. 程序结构与控制流

- 3.1 程序结构与执行
- 3.2 条件执行
- 3.3 循环与迭代
- 3.4 异常
- 3.5 上下文管理器与 `with` 语句
- 3.6 断言与 `__debug__`
- 3.7 结语

## 4. 对象、类型与协议

- 4.1 核心概念
- 4.2 对象标识与类型
- 4.3 引用计数与垃圾回收
- 4.4 引用与副本
- 4.5 对象的表示与打印
- 4.6 一等对象
- 4.7 使用 `None` 表示可选或缺失数据
- 4.8 对象协议与数据抽象
- 4.9 对象协议
- 4.10 数字协议
- 4.11 比较协议
- 4.12 转换协议
- 4.13 容器协议
- 4.14 迭代协议
- 4.15 属性协议
- 4.16 函数协议
- 4.17 上下文管理器协议
- 4.18 结语：关于 Python 风格 (Pythonic)

## 5. 函数

- 5.1 函数定义
- 5.2 默认参数
- 5.3 可变参数
- 5.4 关键字参数
- 5.5 可变关键字参数
- 5.6 接受所有输入的函数
- 5.7 仅限位置参数
- 5.8 名称、文档字符串与类型提示
- 5.9 函数应用与参数传递
- 5.10 返回值
- 5.11 错误处理
- 5.12 作用域规则
- 5.13 递归
- 5.14 `lambda` 表达式
- 5.15 高阶函数
- 5.16 回调函数中的参数传递
- 5.17 从回调中返回结果
- 5.18 装饰器
- 5.19 Map, Filter 与 Reduce
- 5.20 函数内省、属性与签名
- 5.21 环境检查
- 5.22 动态代码执行与创建
- 5.23 异步函数与 `await`
- 5.24 结语：关于函数与组合的思考

## 6. 生成器

- 6.1 生成器与 `yield`
- 6.2 可重启生成器
- 6.3 生成器委托
- 6.4 生成器的实际应用
- 6.5 增强生成器与 `yield` 表达式
- 6.6 增强生成器的应用
- 6.7 生成器与 `await` 的桥梁
- 6.8 结语：生成器的简史与展望

## 7. 类与面向对象编程

- 7.1 对象
- 7.2 `class` 语句
- 7.3 实例
- 7.4 属性访问
- 7.5 作用域规则
- 7.6 运算符重载与协议
- 7.7 继承
- 7.8 通过组合避免继承
- 7.9 通过函数避免继承
- 7.10 动态绑定与鸭子类型
- 7.11 继承内置类型的危险性
- 7.12 类变量与方法
- 7.13 静态方法
- 7.14 关于设计模式的探讨
- 7.15 数据封装与私有属性
- 7.16 类型提示
- 7.17 属性 (Properties)
- 7.18 类型、接口与抽象基类
- 7.19 多重继承、接口与 Mixins
- 7.20 基于类型的分发
- 7.21 类装饰器
- 7.22 受控继承
- 7.23 对象生命周期与内存管理
- 7.24 弱引用
- 7.25 内部对象表示与属性绑定
- 7.26 代理、包装器与委托
- 7.27 使用 `__slots__` 减少内存使用
- 7.28 描述符
- 7.29 类定义过程
- 7.30 动态创建类
- 7.31 元类
- 7.32 实例与类的内置对象
- 7.33 结语：保持简单

## 8. 模块与包

- 8.1 模块与 `import` 语句
- 8.2 模块缓存
- 8.3 从模块导入选定名称
- 8.4 循环导入
- 8.5 模块重载与卸载
- 8.6 模块编译
- 8.7 模块搜索路径
- 8.8 作为主程序执行
- 8.9 包
- 8.10 包内导入
- 8.11 将包子模块作为脚本运行
- 8.12 控制包命名空间
- 8.13 控制包导出
- 8.14 包数据
- 8.15 模块对象
- 8.16 部署 Python 包
- 8.17 倒数第二句话：从包开始
- 8.18 结语：保持简单

## 9. 输入与输出

- 9.1 数据表示
- 9.2 文本编码与解码
- 9.3 文本与字节格式化
- 9.4 读取命令行选项
- 9.5 环境变量
- 9.6 文件与文件对象
- 9.7 I/O 抽象层
- 9.8 标准输入、输出与错误
- 9.9 目录
- 9.10 `print()` 函数
- 9.11 生成输出
- 9.12 消费输入
- 9.13 对象序列化
- 9.14 阻塞操作与并发
- 9.15 标准库模块
- 9.15.25 `threading` 模块
- 9.16 结语

## 10. 内置函数与标准库

- 10.1 内置函数
- 10.2 内置异常
- 10.3 标准库
- 10.4 结语：利用内置功能

## 索引

## 代码片段

- i
- ii
- iii
- iv
- v
- vi
- vii
- viii
- ix
- x
- xi
- xii
- xiii
- xiv
- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36
- 37
- 38
- 39
- 40
- 41
- 42
- 43
- 44
- 45
- 46
- 47
- 48
- 49
- 50
- 51
- 52
- 53
- 54
- 55
- 56
- 57
- 58
- 59
- 60
- 61
- 62
- 63
- 64
- 65
- 66
- 67
- 68
- 69
- 70
- 71
- 72
- 73
- 74
- 75
- 76
- 77
- 78
- 79
- 80
- 81
- 82
- 83
- 84
- 85
- 86
- 87
- 88
- 89
- 90
- 91
- 92
- 93
- 94
- 95
- 96
- 97
- 98
- 99
- 100
- 101
- 102
- 103
- 104
- 105
- 106
- 107
- 108
- 109
- 110
- 111
- 112
- 113
- 114
- 115
- 116
- 117
- 118
- 119
- 120
- 121
- 122
- 123
- 124
- 125
- 126
- 127
- 128
- 129
- 130
- 131
- 132
- 133
- 134
- 135
- 136
- 137
- 138
- 139
- 140
- 141
- 142
- 143
- 144
- 145
- 146
- 147
- 148
- 149
- 150
- 151
- 152
- 153
- 154
- 155
- 156
- 157
- 158
- 159
- 160
- 161
- 162
- 163
- 164
- 165
- 166
- 167
- 168
- 169
- 170
- 171
- 172
- 173
- 174
- 175
- 176
- 177
- 178
- 179
- 180
- 181
- 182
- 183
- 184
- 185
- 186
- 187
- 188
- 189
- 190
- 191
- 192
- 193
- 194
- 195
- 196
- 197
- 198
- 199
- 200
- 201
- 202
- 203
- 204
- 205
- 206
- 207
- 208
- 209
- 210
- 211
- 212
- 213
- 214
- 215
- 216
- 217
- 218
- 219
- 220
- 221
- 222
- 223
- 224
- 225
- 226
- 227
- 228
- 229
- 230
- 231
- 232
- 233
- 234
- 235
- 236
- 237
- 238
- 239
- 240
- 241
- 242
- 243
- 244
- 245
- 246
- 247
- 248
- 249
- 250
- 251
- 252
- 253
- 254
- 255
- 256
- 257
- 258
- 259
- 260
- 261
- 262
- 263
- 264
- 265
- 266
- 267
- 268
- 269
- 270
- 271
- 272
- 273
- 274
- 275
- 276
- 277
- 278
- 279
- 280
- 281
- 282
- 283
- 284
- 285
- 286
- 287
- 288
- 289
- 290
- 291
- 292
- 293
- 294
- 295
- 296
- 297
- 298
- 299
- 300
- 301
- 302
- 303
- 304
- 305
- 306
- 307
- 308
- 309
- 310
- 311
- 312
- 313
- 314
- 315
- 316
- 317
- 318
- 319
- 320
- 321
- 322
- 323
- 324
- 325
- 326
- 327
- 328
- 329
- 330
- 331
- 332
- 333
- 334
- 335
- 336
- 337
- 338
- 339
- 340
