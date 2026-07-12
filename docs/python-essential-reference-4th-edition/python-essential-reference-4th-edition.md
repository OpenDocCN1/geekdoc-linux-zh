# Python核心参考手册（第4版）





## 面向编程专业人员的必备参考

*Developer's Library* 系列图书旨在为在职程序员提供关于其日常工作中所使用的编程语言和技术的独特、高质量参考和教程。

*Developer's Library* 系列中的所有图书均由技术专家撰写，他们尤其擅长以对其他程序员有用的方式组织和呈现信息。

主要书目包括各自领域内最优秀、最受赞誉的一些图书：

- *PHP 与 MySQL Web 开发*
  Luke Welling & Laura Thomson
  ISBN 978-0-672-32916-6

- *MySQL*
  Paul DuBois
  ISBN-13: 978-0-672-32938-8

- *Linux 内核开发*
  Robert Love
  ISBN-13: 978-0-672-32946-3

- *Python 必备参考*
  David Beazley
  ISBN-13: 978-0-672-32862-6

- *Objective-C 程序设计*
  Stephen G. Kochan
  ISBN-13: 978-0-321-56615-7

- *PostgreSQL*
  Korry Douglas
  ISBN-13: 978-0-672-33015-5

*Developer's Library* 系列图书可在大多数零售书店和在线书店购买，也可通过 Safari Books Online 订阅获得，网址：**safari.informit.com**

**开发人员库**
informit.com/devlibrary

策划编辑
Mark Taber

开发编辑
Michael Thurston

执行编辑
Patrick Kanouse

项目编辑
Seth Kerney

文字编辑
Lisa Thibault

索引编制
David Beazley

校对
Megan Wade

技术编辑
Noah Gift
Kurt Grandis

出版协调人
Vanessa Evans

图书设计
Gary Adair

排版
Bronkella Publishing

![](img/bca8f1caf434b36cbe69cddbca7c9f52_5_0.png)

*献给 Paula、Thomas，以及即将出世的他的弟弟。*

![](img/bca8f1caf434b36cbe69cddbca7c9f52_5_1.png)

## 介绍

本书旨在成为Python编程语言的简洁参考手册。虽然经验丰富的程序员可能能够从本书中学习Python，但它并非旨在成为深入的教程或编程专著。相反，其目标是以准确简洁的方式呈现核心Python语言以及Python库中最基本的部分。本书假设读者已具备Python或其他语言（如C或Java）的编程经验。此外，对系统编程主题的一般了解（例如，基本操作系统概念和网络编程）可能有助于理解库参考手册的某些部分。

Python可免费下载，网址为 http://www.python.org。几乎适用于所有操作系统，包括UNIX、Windows和Macintosh。此外，Python网站包含文档、指南以及各种第三方软件的链接。

*Python Essential Reference*的这个版本正值Python演进的关键时期。Python 2.6和Python 3.0几乎同时发布。然而，Python 3是一个与之前版本不向后兼容的版本。作为作者和程序员，我面临一个困境：我是应该直接跳到Python 3.0，还是应该基于大多数程序员更熟悉的Python 2.x版本进行构建？

多年前，作为一名C程序员，我曾将某些书籍视为编程语言特性的终极权威。例如，如果你使用的东西没有在K&R书中记录，那么它可能不具可移植性，应该谨慎使用。这种方法对我作为一名程序员非常有效，我决定在本版《Essential Reference》中采用这种方法。也就是说，我选择省略Python 2中已从Python 3中移除的特性。同样，我也不关注Python 3中尚未向后移植的特性（尽管这些特性在附录中仍有介绍）。因此，我希望本书无论程序员使用哪个Python版本，都能成为他们有用的伴侣。

*Python Essential Reference*的第四版也包含了自近十年前首次出版以来最令人兴奋的一些变化。过去几年Python的大部分开发都集中在新的编程语言特性上——特别是与函数式和元编程相关的特性。因此，关于函数和面向对象编程的章节得到了极大扩展，涵盖了生成器、迭代器、协程、装饰器和元类等主题。库章节已更新，侧重于更现代的模块。示例和代码片段也在全书中进行了更新。我认为大多数程序员会对扩展的覆盖范围相当满意。

最后，应该指出的是，Python已经包含了数千页有用的文档。本书的内容主要基于这些文档，但有一些关键差异。首先，本参考手册以更紧凑的形式呈现信息，包含不同的示例和对许多主题的替代描述。其次，库参考手册中大量的主题已扩展，包含外部参考资料。这对于底层系统和网络模块尤其如此，因为有效使用这些模块通常依赖于手册和外部参考资料中列出的大量选项。此外，为了产生更简洁的参考手册，一些已弃用且相对晦涩的库模块已被省略。

在撰写本书时，我的目标是制作一本参考手册，其中几乎包含了我使用Python及其大量模块所需的所有内容。虽然这绝不是Python语言的入门介绍，但我希望您发现本书的内容在未来许多年里都能成为您编程参考库的有用补充。我欢迎您的评论。

David Beazley
芝加哥，伊利诺伊州
2009年6月

## Python语言

- 1. 教程简介
- 2. 词法约定和语法
- 3. 类型和对象
- 4. 运算符和表达式
- 5. 程序结构和控制流
- 6. 函数和函数式编程
- 7. 类和面向对象编程
- 8. 模块、包和分发
- 9. 输入和输出
- 10. 执行环境
- 11. 测试、调试、分析和调优

### 1. 教程简介

本章提供Python的快速入门。目标是展示Python的大部分基本特性，而不陷入特殊规则或细节的泥潭。为此，本章简要介绍了变量、表达式、控制流、函数、生成器、类和输入/输出等基本概念。本章并非旨在提供全面介绍。然而，经验丰富的程序员应该能够从本章的材料中推断并创建更高级的程序。鼓励初学者尝试一些示例以感受这门语言。如果您是Python新手并使用Python 3，您可能希望使用Python 2.6来跟随本章。几乎所有主要概念都适用于这两个版本，但Python 3中有少量关键语法变更——主要与打印和I/O有关——可能会使本节中的许多示例无法运行。有关更多详细信息，请参阅附录A "Python 3"。

#### 运行Python

Python程序由解释器执行。通常，解释器只需在命令外壳中输入 **python** 即可启动。然而，解释器和Python开发环境有许多不同的实现（例如，Jython、IronPython、IDLE、ActivePython、Wing IDE、pydev等），因此您应该查阅文档以了解启动细节。当解释器启动时，会出现一个提示符，您可以在简单的读取-求值循环中开始输入程序。例如，在以下输出中，解释器显示其版权信息并向用户呈现 `>>>` 提示符，用户在此输入熟悉的"Hello World"命令：

```
Python 2.6rc2 (r26rc2:66504, Sep 19 2008, 08:50:24)
[GCC 4.0.1 (Apple Inc. build 5465)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print "Hello World"
Hello World
>>>
```

> **注意：** 如果您尝试前面的示例并出现 `SyntaxError`，那么您可能正在使用Python 3。如果是这种情况，您可以继续跟随本章，但请注意在Python 3中 `print` 语句变成了函数。只需在后续示例中要打印的项周围加上括号即可。例如：

```
>>> print("Hello World")
Hello World
>>>
```

在要打印的项周围加上括号在Python 2中也适用，只要您只打印单个项。然而，这种语法在现有Python代码中并不常见。在后面的章节中，有时在主要焦点是与打印不直接相关的特性的示例中使用这种语法，但这些示例应该同时适用于Python 2和3。

Python的交互模式是其最有用的特性之一。在交互式shell中，您可以输入任何有效的语句或语句序列并立即查看结果。许多人，包括作者本人，甚至使用交互式Python作为他们的桌面计算器。例如：

```
>>> 6000 + 4523.50 + 134.12
10657.620000000001
>>> _ + 8192.32
18849.940000000002
>>>
```

当您以交互方式使用Python时，特殊变量 `_` 保存上一次操作的结果。如果您想在后续语句中保存或使用上一次操作的结果，这可能会很有用。然而，需要强调的是，此变量仅在交互工作时才定义。

如果您想创建一个可以重复运行的程序，请将语句放在如下文件中：

```
##### helloworld.py
print "Hello World"
```

Python源文件是普通文本文件，通常具有 `.py` 后缀。`#` 字符表示注释，延伸到行尾。

要执行 `helloworld.py` 文件，您按如下方式向解释器提供文件名：

```
% python helloworld.py
Hello World
%
```

在Windows上，可以通过双击 `.py` 文件或在Windows开始菜单的运行命令中键入程序名来启动Python程序。这将启动解释器并在控制台窗口中运行程序。但是，请注意控制台窗口将在程序完成执行后立即消失（通常在您阅读输出之前）。为了调试，最好在Python开发工具（如IDLE）中运行程序。

在UNIX上，您可以在程序的第一行使用 `#!`，如下所示：

```
#!/usr/bin/env python
print "Hello World"
```



解释器会逐条执行语句，直到到达输入文件的末尾。如果是以交互模式运行，你可以输入 EOF（文件结束）字符，或从 Python IDE 的下拉菜单中选择“退出”来退出解释器。在 UNIX 上，EOF 是 Ctrl+D；在 Windows 上，它是 Ctrl+Z。程序可以通过引发 SystemExit 异常来请求退出。

```python
>>> raise SystemExit
```

#### 变量和算术表达式

示例 1.1 中的程序通过执行一个简单的复利计算来展示变量和表达式的用法。

##### 示例 1.1 简单复利计算

```python
principal = 1000        # Initial amount
rate = 0.05             # Interest rate
numyears = 5            # Number of years
year = 1
while year <= numyears:
    principal = principal * (1 + rate)
    print year, principal   # Reminder: print(year, principal) in Python 3
    year += 1
```

该程序的输出如下表所示：

```
1 1050.0
2 1102.5
3 1157.625
4 1215.50625
5 1276.2815625
```

Python 是一种动态类型语言，在程序执行过程中，变量名可以绑定到不同类型的不同值。赋值运算符只是在名称和值之间建立一种关联。尽管每个值都有关联的类型，如整数或字符串，但变量名本身没有类型，在执行过程中可以引用任何类型的数据。例如，这与 C 语言不同：在 C 中，一个名称代表固定的类型、大小以及内存中用于存储该值的位置。在示例 1.1 中，`principal` 变量体现了 Python 的动态行为。最初，它被赋值为一个整数。然而，在程序稍后部分，它被重新赋值如下：

```python
principal = principal * (1 + rate)
```

该语句对表达式求值，并将名称 `principal` 重新与结果关联。虽然 `principal` 的原始值是整数，但新值现在是一个浮点数（`rate` 被定义为浮点数，因此上述表达式的值也是浮点数）。因此，`principal` 的“类型”似乎在程序运行过程中从整数动态地变成了浮点数。但准确地说，发生变化的并不是 `principal` 的类型，而是名称 `principal` 所引用的值。

每条语句以换行符结束。不过，你也可以使用分号将同一行上的多条语句分隔开，如下所示：

```python
principal = 1000; rate = 0.05; numyears = 5;
```

`while` 语句对紧随其后的条件表达式进行测试。如果被测试的表达式为真，则执行 `while` 语句的主体。然后重新测试条件，并重复执行主体，直到条件变为假。由于循环体通过缩进来表示，示例 1.1 中 `while` 后面的三条语句在每次迭代时都会执行。Python 没有规定必须使用多少缩进，只要在一个代码块内保持一致即可。然而，最常见的（通常也是推荐的）做法是每级缩进使用四个空格。

示例 1.1 中的程序有一个问题：输出不太美观。为了改善输出，你可以将各列右对齐，并将 `principal` 的精度限制为两位小数。有多种方式可以实现这种格式化。最广泛使用的方法是使用字符串格式化运算符（`%`），如下所示：

```python
print "%3d %0.2f" % (year, principal)
print("%3d %0.2f" % (year, principal))   # Python 3
```

现在程序的输出如下所示：

```
 1 1050.00
 2 1102.50
 3 1157.63
 4 1215.51
 5 1276.28
```

格式化字符串包含普通文本以及特殊的格式化字符序列，如 `"%d"`、`"%s"` 和 `"%f"`。这些序列分别指定特定数据类型（如整数、字符串或浮点数）的格式。特殊字符序列还可以包含用于指定宽度和精度的修饰符。例如，`"%3d"` 将整数格式化为在宽度为 3 的列中右对齐，`"%0.2f"` 将浮点数格式化为小数点后只保留两位数字。格式化字符串的行为与 C 语言的 `printf()` 函数几乎完全相同，详细内容见第 4 章“运算符与表达式”。

一种更现代的字符串格式化方式是使用 `format()` 函数分别对每一部分进行格式化。例如：

```python
print format(year,"3d"),format(principal,"0.2f")
print(format(year,"3d"),format(principal,"0.2f")) # Python 3
```

`format()` 使用的格式说明符与传统的字符串格式化运算符（`%`）使用的类似。例如，`"3d"` 将整数格式化为在宽度为 3 的列中右对齐，`"0.2f"` 将浮点数格式化为保留两位小数。字符串还有一个 `format()` 方法，可用于一次性格式化多个值。例如：

```python
print "{0:3d} {1:0.2f}".format(year,principal)
print("{0:3d} {1:0.2f}".format(year,principal)) # Python 3
```

在这个例子中，`"{0:3d}"` 和 `"{1:0.2f}"` 中冒号前面的数字表示传递给 `format()` 方法的对应参数，冒号后面的部分是格式说明符。

#### 条件语句

`if` 和 `else` 语句可以进行简单的测试。示例如下：

```python
if a < b:
    print "Computer says Yes"
else:
    print "Computer says No"
```

`if` 和 `else` 子句的代码体通过缩进来表示。`else` 子句是可选的。

要创建一个空子句，可以使用 `pass` 语句，如下所示：

```python
if a < b:
    pass     # Do nothing
else:
    print "Computer says No"
```

你可以使用 `or`、`and` 和 `not` 关键字来构造布尔表达式：

```python
if product == "game" and type == "pirate memory" \
                      and not (age < 4 or age > 8):
    print "I'll take it!"
```

###### 注意

编写复杂的测试条件通常会导致一行代码过长，令人头疼。为了提高可读性，你可以在行尾使用反斜杠（\）将任意语句延续到下一行，如示例所示。如果这样做，正常的缩进规则不适用于下一行，因此你可以自由地对续行进行格式化。

Python 没有专门的 `switch` 或 `case` 语句来测试值。要处理多种测试情况，可以使用 `elif` 语句，如下所示：

```python
if suffix == ".htm":
    content = "text/html"
elif suffix == ".jpg":
    content = "image/jpeg"
elif suffix == ".png":
    content = "image/png"
else:
    raise RuntimeError("Unknown content type")
```

表示真值时，使用布尔值 `True` 和 `False`。示例如下：

```python
if 'spam' in s:
    has_spam = True
else:
    has_spam = False
```

所有关系运算符（如 `<` 和 `>`）都会返回 `True` 或 `False` 作为结果。本例中使用的 `in` 运算符通常用于检查一个值是否包含在另一个对象中，例如字符串、列表或字典。它也返回 `True` 或 `False`，因此前面的例子可以简化为：

```python
has_spam = 'spam' in s
```

#### 文件输入与输出

下面的程序打开一个文件并逐行读取其内容：

```python
f = open("foo.txt")              # Returns a file object
line = f.readline()             # Invokes readline() method on file
while line:
    print line,                 # trailing ',' omits newline character
    # print(line,end='')       # Use in Python 3
    line = f.readline()
f.close()
```

`open()` 函数返回一个新的文件对象。通过调用该对象上的方法，你可以执行各种文件操作。`readline()` 方法读取单行输入，包括结尾的换行符。到达文件末尾时返回空字符串。

在这个例子中，程序只是简单地遍历文件 foo.txt 中的所有行。当程序像这样遍历一组数据（例如输入行、数字、字符串等）时，通常称为*迭代*。由于迭代是一种非常常见的操作，Python 提供了一个专门的语句 `for`，用于遍历各项。例如，同一个程序可以更简洁地写成如下形式：

```python
for line in open("foo.txt"):
    print line,
```

若要将程序的输出写入文件，可以使用 `>>` 向 `print` 语句提供一个文件对象，如下例所示：

```python
f = open("out","w")      # Open file for writing
while year <= numyears:
    principal = principal * (1 + rate)
    print >>f,"%3d %0.2f" % (year,principal)
    year += 1
f.close()
```

`>>` 语法仅在 Python 2 中有效。如果你使用的是 Python 3，请将 `print` 语句改为如下形式：

```python
print("%3d %0.2f" % (year,principal),file=f)
```

此外，文件对象还支持 `write()` 方法，可用于写入原始数据。例如，前面例子中的 `print` 语句可以写成这样：

```python
f.write("%3d %0.2f\n" % (year,principal))
```

虽然这些示例操作的是文件，但同样的技术也适用于解释器的标准输出流和标准输入流。例如，如果你想以交互方式读取用户输入，可以从文件 `sys.stdin` 读取。如果你想将数据输出到屏幕，可以写入 `sys.stdout`，它与 `print` 语句用于输出数据的文件相同。例如：

```python
import sys
sys.stdout.write("Enter your name :")
name = sys.stdin.readline()
```

在 Python 2 中，这段代码还可以简化为：

```python
name = raw_input("Enter your name :")
```



在 Python 3 中，`raw_input()` 函数被命名为 `input()`，但其工作方式完全相同。

#### 字符串

要创建字符串字面量，可以用单引号、双引号或三引号将其括起来，如下所示：

```python
a = "Hello World"
b = 'Python is groovy'
c = """Computer says 'No'"""
```

开始字符串时使用的引号类型必须与结束时使用的引号类型相同。三引号字符串会捕获在结束三引号之前出现的所有文本，而单引号和双引号字符串则必须指定在一行逻辑行上。当字符串字面量的内容跨越多行文本时，三引号字符串非常有用，例如以下情况：

```python
print('''Content-type: text/html

<h1> Hello World </h1>
Click <a href="http://www.python.org">here</a>.
''')
```

字符串以从零开始的整数索引的字符序列形式存储。要提取单个字符，请使用索引运算符 `s[i]`，如下所示：

```python
a = "Hello World"
b = a[4]      # b = 'o'
```

要提取子字符串，请使用切片运算符 `s[i:j]`。这会从 `s` 中提取所有索引 *k* 在范围 *i* <= *k* < *j* 内的字符。如果省略任一索引，则分别假定为字符串的开头或结尾：

```python
c = a[:5]     # c = "Hello"
d = a[6:]     # d = "World"
e = a[3:8]    # e = "lo Wo"
```

字符串使用加号（+）运算符进行拼接：

```python
g = a + " This is a test"
```

Python 永远不会隐式地将字符串的内容解释为数值数据（即像其他语言如 Perl 或 PHP 那样）。例如，+ 始终用于拼接字符串：

```python
x = "37"
y = "42"
z = x + y   # z = "3742"（字符串拼接）
```

要执行数学计算，字符串首先需要使用 `int()` 或 `float()` 等函数转换为数值。例如：

```python
z = int(x) + int(y)  # z = 79（整数加法）
```

非字符串值可以通过使用 `str()`、`repr()` 或 `format()` 函数转换为字符串表示形式。以下是一个示例：

```python
s = "The value of x is " + str(x)
s = "The value of x is " + repr(x)
s = "The value of x is " + format(x,"4d")
```

虽然 `str()` 和 `repr()` 都创建字符串，但它们的输出通常略有不同。`str()` 生成的是你使用 print 语句时得到的输出，而 `repr()` 创建的是你键入程序中以精确表示对象值的字符串。例如：

```python
>>> x = 3.4
>>> str(x)
'3.4'
>>> repr(x)
'3.3999999999999999'
>>>
```

上例中 3.4 的不精确表示并不是 Python 中的错误。它是双精度浮点数的特性所致，双精度浮点数在设计上无法在底层计算机硬件上精确表示十进制数。

`format()` 函数用于将值转换为应用了特定格式化的字符串。例如：

```python
>>> format(x,"0.5f")
'3.40000'
>>>
```

###### 列表

*列表*是任意对象的序列。你可以通过将值括在方括号中来创建列表，如下所示：

```python
names = [ "Dave", " Mark", "Ann", "Phil" ]
```

列表以从零开始的整数索引。使用索引运算符来访问和修改列表中的各个项目：

```python
a = names[2]       # 返回列表的第三个项目，"Ann"
names[0] = "Jeff"  # 将第一个项目更改为 "Jeff"
```

```python
names.append("Paula")
```

要将项目插入列表中间，请使用 `insert()` 方法：

```python
names.insert(2, "Thomas")
```

你可以使用切片运算符提取或重新赋值列表的一部分：

```python
b = names[0:2]                          # 返回 [ "Jeff", "Mark" ]
c = names[2:]                           # 返回 [ "Thomas", "Ann", "Phil", "Paula" ]
names[1] = 'Jeff'                       # 将 names 中的第二个项目替换为 'Jeff'
names[0:2] = ['Dave','Mark','Jeff']     # 将列表的前两个项目替换为
                                        # 右侧的列表。
```

使用加号（+）运算符拼接列表：

```python
a = [1,2,3] + [4,5]    # 结果为 [1,2,3,4,5]
```

空列表可以通过以下两种方式之一创建：

```python
names = []      # 一个空列表
names = list()  # 一个空列表
```

列表可以包含任何类型的 Python 对象，包括其他列表，如以下示例所示：

```python
a = [1,"Dave",3.14, ["Mark", 7, 9, [100,101]], 10]
```

嵌套列表中包含的项目通过多次索引操作来访问，如下所示：

```python
a[1]         # 返回 "Dave"
a[3][2]      # 返回 9
a[3][3][1]   # 返回 101
```

程序清单 1.2 通过从命令行指定的文件中读取数字列表并输出最小值和最大值，展示了列表的更多高级特性。

##### 程序清单 1.2 高级列表特性

```python
import sys                     # 加载 sys 模块
if len(sys.argv) != 2           # 检查命令行参数的数量：
    print "Please supply a filename"
    raise SystemExit(1)
f = open(sys.argv[1])          # 命令行上的文件名
lines = f.readlines()          # 将所有行读入列表
f.close()

##### 将所有输入值从字符串转换为浮点数
fvalues = [float(line) for line in lines]

##### 打印最小值和最大值
print "The minimum value is ", min(fvalues)
print "The maximum value is ", max(fvalues)
```

该程序的第一行使用 `import` 语句从 Python 库中加载 `sys` 模块。加载此模块是为了获取命令行参数。

`open()` 函数使用作为命令行选项提供的文件名，并将其放入 `sys.argv` 列表中。`readlines()` 方法将所有输入行读入字符串列表。

表达式 `[float(line) for line in lines]` 通过遍历 `lines` 列表中的所有字符串并对每个元素应用 `float()` 函数来构造新列表。这种特别强大的列表构造方法称为*列表推导式*。由于文件中的行也可以使用 for 循环读取，因此可以通过类似以下的单条语句来转换值，从而缩短程序：

```python
fvalues = [float(line) for line in open(sys.argv[1])]
```

在将输入行转换为浮点数列表之后，内置的 `min()` 和 `max()` 函数计算最小值和最大值。

#### 元组

要创建简单的数据结构，你可以使用*元组*将一组值打包到单个对象中。你可以通过将一组值括在圆括号中来创建元组，如下所示：

```python
stock = ('GOOG', 100, 490.10)
address = ('www.python.org', 80)
person = (first_name, last_name, phone)
```

Python 通常即使在缺少圆括号的情况下也能识别出元组的意图：

```python
stock = 'GOOG', 100, 490.10
address = 'www.python.org',80
person = first_name, last_name, phone
```

为了完整性，可以定义 0 元素和 1 元素的元组，但需要使用特殊语法：

```python
a = ()       # 0 元组（空元组）
b = (item,)  # 1 元组（注意末尾的逗号）
c = item,    # 1 元组（注意末尾的逗号）
```

元组中的值可以通过数字索引提取，就像列表一样。不过更常见的做法是将元组解包为一组变量，如下所示：

```python
name, shares, price = stock
host, port = address
first_name, last_name, phone = person
```

虽然元组支持与列表相同的大部分操作（如索引、切片和拼接），但元组的内容在创建后不能修改（即，你不能替换、删除或向现有元组追加新元素）。这反映了一个事实：元组最好被视为由多个部分组成的单个对象，而不是你可能会插入或移除项目的不同对象的集合。

由于元组和列表之间存在大量重叠，有些程序员倾向于完全忽略元组，简单地使用列表，因为列表看起来更灵活。虽然这样做是可行的，但如果你的程序要创建大量小型列表（即，每个列表包含少于一打项目），这会浪费内存。这是因为列表会略微过度分配内存，以优化添加新项目的操作性能。由于元组是不可变的，它们使用更紧凑的表示方式，没有额外的空间。

元组和列表通常一起使用来表示数据。例如，以下程序展示了如何读取由逗号分隔的不同数据列组成的文件：

```python
##### 文件包含格式为 "name,shares,price" 的行
filename = "portfolio.csv"
portfolio = []
for line in open(filename):
    fields = line.split(",")    # 将每行拆分为列表
    name  = fields[0]            # 提取并转换各个字段
    shares = int(fields[1])
    price  = float(fields[2])
    stock = (name,shares,price)  # 创建元组 (name, shares, price)
    portfolio.append(stock)      # 追加到记录列表中
```

字符串的 `split()` 方法将字符串拆分为由给定分隔符字符分隔的字段列表。由此程序创建的最终 `portfolio` 数据结构



#### 集合

*集合*用于存放无序的对象集合。要创建一个集合，请使用 `set()` 函数并传入一个序列，如下所示：

```python
s = set([3, 5, 9, 10])      # 创建一个数字集合
t = set("Hello")         # 创建一个包含唯一字符的集合
```

与列表和元组不同，集合是无序的，不能通过数字索引。此外，集合中的元素永远不会重复。例如，如果你检查上面代码中 `t` 的值，你会得到：

```python
>>> t
set(['H', 'e', 'l', 'o'])
```

注意，只出现了一个 `'l'`。

集合支持一系列标准操作，包括并集、交集、差集和对称差集。例如：

```python
a = t | s          # t 和 s 的并集
b = t & s          # t 和 s 的交集
c = t - s          # 集合差集（在 t 中但不在 s 中的元素）
d = t ^ s          # 对称差集（在 t 或 s 中，但不同时在两者中的元素）
```

可以使用 `add()` 或 `update()` 向集合中添加新项：

```python
t.add('x')             # 添加单个项目
s.update([10, 37, 42])   # 向 s 中添加多个项目
```

可以使用 `remove()` 移除一个项目：

```python
t.remove('H')
```

###### 字典

*字典*是一种关联数组或哈希表，其中包含通过键索引的对象。你可以通过将值放在花括号（{ }）中来创建字典，如下所示：

```python
stock = {
    "name"   : "GOOG",
    "shares" : 100,
    "price"  : 490.10
}
```

要访问字典的成员，请使用键索引操作符，如下所示：

```python
name  = stock["name"]
value = stock["shares"] * stock["price"]
```

插入或修改对象的方式如下：

```python
stock["shares"] = 75
stock["date"]   = "June 7, 2007"
```

虽然字符串是最常见的键类型，但你也可以使用许多其他 Python 对象，包括数字和元组。某些对象（包括列表和字典）不能用作键，因为它们的内容可能改变。

字典是定义包含命名字段的对象的一种有用方式，如前所示。然而，字典也用作对无序数据进行快速查找的容器。例如，这是一个股票价格字典：

```python
prices = {
    "GOOG" : 490.10,
    "AAPL" : 123.50,
    "IBM"  : 91.50,
    "MSFT" : 52.13
}
```

空字典可以通过以下两种方式之一创建：

```python
prices = {}     # 一个空字典
prices = dict() # 一个空字典
```

使用 `in` 操作符测试字典的成员关系，如下例所示：

```python
if "SCOX" in prices:
    p = prices["SCOX"]
else:
    p = 0.0
```

这个特定的步骤序列也可以更紧凑地完成，如下所示：

```python
p = prices.get("SCOX", 0.0)
```

要获取字典键的列表，可以将字典转换为列表：

```python
syms = list(prices)       # syms = ["AAPL", "MSFT", "IBM", "GOOG"]
```

使用 `del` 语句删除字典的一个元素：

```python
del prices["MSFT"]
```

字典可能是 Python 解释器中调优最精细的数据类型。因此，如果你只是想存储和处理程序中的数据，使用字典几乎总是比你自己想出某种自定义数据结构要好。

#### 迭代与循环

最广泛使用的循环结构是 `for` 语句，它用于遍历一组项目。迭代是 Python 最丰富的特性之一。然而，最常见的迭代形式是简单地遍历序列的所有成员，例如字符串、列表或元组。例如：

```python
for n in [1, 2, 3, 4, 5, 6, 7, 8, 9]:
    print("2 to the %d power is %d" % (n, 2**n))
```

在这个例子中，变量 `n` 在每次迭代中将被赋予列表 `[1, 2, 3, 4, ..., 9]` 中的连续项。因为遍历整数范围非常常见，通常使用以下快捷方式来达到此目的：

```python
for n in range(1, 10):
    print("2 to the %d power is %d" % (n, 2**n))
```

`range(i, j [, stride])` 函数创建一个表示整数范围的对象，值从 `i` 到 `j-1`。如果省略起始值，则默认为零。可选的步长可以作为第三个参数给出。例如：

```python
a = range(5)       # a = 0, 1, 2, 3, 4
b = range(1, 8)     # b = 1, 2, 3, 4, 5, 6, 7
c = range(0, 14, 3)  # c = 0, 3, 6, 9, 12
d = range(8, 1, -1)  # d = 8, 7, 6, 5, 4, 3, 2
```

关于 `range()` 的一个注意事项是，在 Python 2 中，它创建的值是一个完全填充的列表，包含所有整数值。对于极大的范围，这可能会无意中消耗所有可用内存。因此，在旧的 Python 代码中，你会看到程序员使用替代函数 `xrange()`。例如：

```python
for i in xrange(100000000):   # i = 0, 1, 2, ..., 99999999
    statements
```

`xrange()` 创建的对象在需要查找时按需计算它所表示的值。因此，它是表示极大整数范围的首选方式。在 Python 3 中，`xrange()` 函数已重命名为 `range()`，并且旧 `range()` 函数的功能已被移除。

`for` 语句不仅限于整数序列，还可以用于遍历多种类型的对象，包括字符串、列表、字典和文件。例如：

```python
a = "Hello World"
##### 打印 a 中的各个字符
for c in a:
    print(c)

b = ["Dave", "Mark", "Ann", "Phil"]
##### 打印列表的成员
for name in b:
    print(name)

c = { 'GOOG' : 490.10, 'IBM' : 91.50, 'AAPL' : 123.15 }
##### 打印字典的所有成员
for key in c:
    print(key, c[key])

##### 打印文件中的所有行
f = open("foo.txt")
for line in f:
    print(line, end='')
```

`for` 循环是 Python 最强大的语言特性之一，因为你可以创建自定义的迭代器对象和生成器函数来为其提供值序列。关于迭代器和生成器的更多细节可以在本章后面以及第 6 章“函数与函数式编程”中找到。

##### 函数

你使用 `def` 语句来创建一个函数，如下例所示：

```python
def remainder(a, b):
    q = a // b      # // 是截断除法。
    r = a - q*b
    return r
```

要调用一个函数，只需使用函数名，后跟括号中的参数，例如 `result = remainder(37, 15)`。你可以使用元组从函数返回多个值，如下所示：

```python
def divide(a, b):
    q = a // b        # 如果 a 和 b 是整数，q 是整数
    r = a - q*b
    return (q, r)
```

在以元组形式返回多个值时，你可以轻松地将结果解包到单独的变量中，如下所示：

```python
quotient, remainder = divide(1456, 33)
```

为函数参数分配默认值：

```python
def connect(hostname, port, timeout=300):
    # 函数体
```

当函数定义中给出默认值时，它们可以在后续的函数调用中省略。当省略时，参数将简单地采用默认值。例如：

```python
connect('www.python.org', 80)
```

你也可以通过使用关键字参数并以任意顺序提供参数来调用函数。但是，这要求你了解函数定义中参数的名称。例如：

```python
connect(port=80, hostname="www.python.org")
```

当在函数内部创建或赋值变量时，它们的作用域是局部的。也就是说，该变量仅在函数体内定义，并在函数返回时销毁。要从函数内部修改全局变量的值，请使用 `global` 语句，如下所示：

```python
count = 0
...
def foo():
    global count
    count += 1          # 更改全局变量 count
```



##### 生成器

一个函数不一定要返回单个值，如果它使用了 `yield` 语句，就可以生成一个完整的结果序列。例如：

```python
def countdown(n):
    print("Counting down!")
    while n > 0:
        yield n      # 生成一个值 (n)
        n -= 1
```

任何使用 `yield` 的函数都被称为 *生成器*。调用一个生成器函数会创建一个对象，该对象通过连续调用 `next()` 方法（在 Python 3 中是 `__next__()`）来产生一系列结果。例如：

```python
>>> c = countdown(5)
>>> c.next()
Counting down!
5
>>> c.next()
4
>>> c.next()
3
>>>
```

`next()` 的调用会使生成器函数运行，直到遇到下一个 `yield` 语句。此时，传递给 `yield` 的值会由 `next()` 返回，函数暂停执行。当再次调用 `next()` 时，函数会从 `yield` 语句之后的语句处恢复执行。这个过程会持续进行，直到函数返回。

通常你不会像上面那样手动调用 `next()`。相反，你会像这样将其连接到一个 `for` 循环：

```python
>>> for i in countdown(5):
...     print(i, end=' ')
Counting down!
5 4 3 2 1
>>>
```

生成器是一种极其强大的方式，可用于编写基于处理管道、数据流或数据流的程序。例如，下面的生成器函数模仿了常用于监控日志文件的 UNIX `tail -f` 命令的行为：

```python
##### 尾随一个文件（类似 tail -f）
import time
def tail(f):
    f.seek(0,2)   # 移动到文件末尾
    while True:
        line = f.readline()    # 尝试读取新的一行文本
        if not line:           # 如果没有内容，短暂休眠后重试
            time.sleep(0.1)
            continue
        yield line
```

这是一个在行序列中查找特定子字符串的生成器：

```python
def grep(lines, searchtext):
    for line in lines:
        if searchtext in line: yield line
```

这是一个将这两个生成器组合起来创建简单处理管道的示例：

```python
##### Unix "tail -f | grep python" 的 Python 实现
wwwlog  = tail(open("access-log"))
pylines = grep(wwwlog,"python")
for line in pylines:
    print(line, end=' ')
```

生成器的一个微妙之处在于，它们通常与其他可迭代对象（如列表或文件）混合使用。具体来说，当你编写像 `for item in s` 这样的语句时，`s` 可能代表一个项目列表、一个文件的行、一个生成器函数的结果，或者任何其他支持迭代的对象。你可以将不同的对象插入到 `s` 的位置，这一事实可以成为创建可扩展程序的强大工具。

#### 协程

通常，函数对一组输入参数进行操作。然而，也可以编写一个函数，使其作为处理发送给它的一系列输入的任务来运行。这种类型的函数被称为 *协程*，它是通过使用 `yield` 语句作为表达式（`yield`）来创建的，如下例所示：

```python
def print_matches(matchtext):
    print("Looking for", matchtext)
    while True:
        line = (yield)      # 获取一行文本
        if matchtext in line:
            print(line)
```

要使用此函数，你首先调用它，将其推进到第一个 `(yield)`，然后开始使用 `send()` 向其发送数据。例如：

```python
>>> matcher = print_matches("python")
>>> matcher.next()         # 推进到第一个 (yield)
Looking for python
>>> matcher.send("Hello World")
>>> matcher.send("python is cool")
python is cool
>>> matcher.send("yow!")
>>> matcher.close()        # 完成 matcher 函数调用
>>>
```

协程会暂停，直到使用 `send()` 向其发送一个值。当这种情况发生时，该值会由协程内部的 `(yield)` 表达式返回，并由其后的语句进行处理。处理会持续进行，直到遇到下一个 `(yield)` 表达式——此时函数会暂停。这个过程会持续，直到协程函数返回或对其调用 `close()`，如前面的示例所示。

在编写基于生产者-消费者问题的并发程序时，协程非常有用，其中程序的一部分负责生产数据，另一部分负责消费数据。在这种模型中，协程代表一个数据消费者。以下是同时使用生成器和协程的示例：

```python
##### 一组 matcher 协程
matchers = [
    print_matches("python"),
    print_matches("guido"),
    print_matches("jython")
]
```

```python
##### 通过调用 next() 来准备所有的 matcher
for m in matchers: m.next()

##### 将活动的日志文件输入到所有 matcher。注意，为了使此方法生效，
# Web 服务器必须正在积极地向日志写入数据。
wwwlog = tail(open("access-log"))
for line in wwwlog:
    for m in matchers:
        m.send(line)     # 将数据发送到每个 matcher 协程
```

关于协程的更多细节可以在第 6 章找到。

#### 对象与类

程序中使用的所有值都是对象。一个 *对象* 由内部数据和操作该数据的各种方法组成。在使用字符串和列表等内置类型时，你已经使用过对象和方法。例如：

```python
items = [37, 42]   # 创建一个列表对象
items.append(73)    # 调用 append() 方法
```

`dir()` 函数列出了对象上可用的方法，是交互式实验的有用工具。例如：

```python
>>> items = [37, 42]
>>> dir(items)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__',
...
'append', 'count', 'extend', 'index', 'insert', 'pop',
'remove', 'reverse', 'sort']
>>>
```

检查对象时，你会看到诸如 `append()` 和 `insert()` 之类的熟悉方法。但是，你还会看到总是以双下划线开头和结尾的特殊方法。这些方法实现了各种语言操作。例如，`__add__()` 方法实现了 `+` 运算符：

```python
>>> items.__add__([73,101])
[37, 42, 73, 101]
>>>
```

`class` 语句用于定义新的对象类型，并进行面向对象的编程。例如，以下类定义了一个带有 `push()`、`pop()` 和 `length()` 操作的简单栈：

```python
class Stack(object):
    def __init__(self):          # 初始化栈
        self.stack = [ ]
    def push(self, object):
        self.stack.append(object)
    def pop(self):
        return self.stack.pop()
    def length(self):
        return len(self.stack)
```

在类定义的第一行中，语句 `class Stack(object)` 声明 `Stack` 是一个 `object`。使用括号是 Python 指定继承的方式——在这种情况下，`Stack` 继承自 `object`，后者是所有 Python 类型的根。在类定义内部，使用 `def` 语句定义方法。每个方法的第一个参数始终指向对象本身。按照惯例，`self` 被用作此参数的名称。所有涉及对象属性的操作都必须显式引用 `self` 变量。具有前导和尾随双下划线的方法是特殊方法。例如，`__init__` 用于在对象创建后对其进行初始化。

要使用一个类，请编写如下代码：

```python
s = Stack()         # 创建一个栈
s.push("Dave")      # 将一些东西压入栈中
s.push(42)
s.push([3,4,5])
x = s.pop()         # x 得到 [3,4,5]
y = s.pop()         # y 得到 42
del s               # 销毁 s
```

在这个例子中，创建了一个全新的对象来实现栈。然而，栈与内置的列表对象几乎完全相同。因此，另一种方法是继承 `list` 并添加一个额外的方法：

```python
class Stack(list):
    # 为栈接口添加 push() 方法
    # 注意：列表已经提供了 pop() 方法。
    def push(self, object):
        self.append(object)
```

通常，类中定义的所有方法仅适用于该类的实例（即创建的对象）。但是，可以定义不同种类的方法，例如 C++ 和 Java 程序员熟悉的静态方法。例如：

```python
class EventHandler(object):
    @staticmethod
    def dispatcherThread():
        while (1):
            # 等待请求
            ...
```

```python
EventHandler.dispatcherThread()      # 像函数一样调用方法
```

在这种情况下，`@staticmethod` 声明其后的方法是一个静态方法。`@staticmethod` 是使用 *装饰器* 的一个例子，这个主题在第 6 章将进一步讨论。

##### 异常

如果程序中发生错误，会引发一个异常，并出现如下所示的回溯信息：

```
Traceback (most recent call last):
  File "foo.py", line 12, in <module>
IOError: [Errno 2] No such file or directory: 'file.txt'
```

回溯信息指出了发生的错误类型及其位置。通常，错误会导致程序终止。但是，你可以使用 `try` 和 `except` 语句来捕获和处理异常，如下所示：

```python
try:
    f = open("file.txt","r")
except IOError as e:
    print(e)
```



如果发生`IOError`错误，有关错误原因的详细信息将被放置在`e`中，控制权将转移到`except`块中的代码。如果引发其他类型的异常，它将传递给外部代码块（如果有）。如果没有发生错误，`except`块中的代码将被忽略。当异常被处理时，程序执行将从最后一个`except`块之后的语句继续。程序不会返回到异常发生的位置。

`raise`语句用于发出异常信号。引发异常时，可以使用内置异常之一，如下所示：

```
raise RuntimeError("Computer says no")
```

或者，您可以创建自己的异常，如第5章“程序结构和控制流”中的“定义新异常”部分所述。

正确管理系统资源（如锁、文件和网络连接）与异常处理结合时，往往是一个棘手的问题。为简化此类编程，可以将`with`语句与某些类型的对象一起使用。以下是使用互斥锁编写代码的示例：

```
import threading
message_lock = threading.Lock()
...
with message_lock:
    messages.add(newmessage)
```

在此示例中，当`with`语句执行时，`message_lock`对象将自动获取。当执行离开`with`块的上下文时，锁将自动释放。无论`with`块内发生什么情况，此管理都会发生。例如，如果发生异常，当控制离开块的上下文时，锁将被释放。

`with`语句通常仅与与系统资源或执行环境（如文件、连接和锁）相关的对象兼容。但是，用户定义的对象可以定义自己的自定义处理。这在第3章“类型和对象”的“上下文管理协议”部分中有更详细的介绍。

###### 模块

随着程序规模的增长，您会希望将它们分解为多个文件以方便维护。为此，Python允许您将定义放在一个文件中，并将其作为模块导入到其他程序和脚本中。要创建模块，请将相关语句和定义放入与模块同名的文件中。（注意文件必须具有`.py`后缀。）以下是一个示例：

```
##### file : div.py
def divide(a,b):
    q = a/b     # If a and b are integers, q is an integer
    r = a - q*b
    return (q,r)
```

要在其他程序中使用您的模块，可以使用`import`语句：

```
import div
a, b = div.divide(2305, 29)
```

import语句创建一个新的命名空间，并在该命名空间内执行关联的.py文件中的所有语句。要在导入后访问命名空间的内容，只需使用模块名称作为前缀，如前面示例中的div.divide()。
如果您想使用不同的名称导入模块，请为import语句提供可选的as限定符，如下所示：

```
import div as foo
a,b = foo.divide(2305,29)
```

要将特定定义导入当前命名空间，请使用from语句：

```
from div import divide
a,b = divide(2305,29)     # No longer need the div prefix
```

要将模块的所有内容加载到当前命名空间，您也可以使用以下方法：

```
from div import *
```

与对象一样，dir()函数列出模块的内容，是交互式实验的有用工具：

```
>>> import string
>>> dir(string)
['__builtins__', '__doc__', '__file__', '__name__', '_idmap',
 '_idmapL', '_lower', '_swapcase', '_upper', 'atof', 'atof_error',
 'atoi', 'atoi_error', 'atol', 'atol_error', 'capitalize',
 'capwords', 'center', 'count', 'digits', 'expandtabs', 'find',
...
>>>
```

#### 获取帮助

使用Python时，您有几个快速获取信息的来源。首先，当Python在交互模式下运行时，您可以使用help()命令获取有关内置模块和其他Python方面的信息。只需输入help()获取一般信息，或输入help('modulename')获取特定模块的信息。如果您提供函数名，help()命令也可用于返回有关特定函数的信息。

大多数Python函数都有描述其用法的文档字符串。要打印文档字符串，只需打印__doc__属性。以下是一个示例：

```
>>> print issubclass.__doc__
issubclass(C, B) -> bool

Return whether class C is a subclass (i.e., a derived class) of class B.
When using a tuple as the second argument issubclass(X, (A, B, ...)),
is a shortcut for issubclass(X, A) or issubclass(X, B) or ... (etc.).
>>>
```

最后但同样重要的是，大多数Python安装还包括pydoc命令，可用于返回有关Python模块的文档。只需在系统命令提示符下输入pydoc topic。

### 词法约定和语法

本章描述Python程序的词法和语法约定。主题包括行结构、语句分组、保留字、字面量、运算符、标记和源代码编码。

#### 行结构和缩进

程序中的每个语句都以换行符结束。长语句可以使用行继续字符(\)跨越多行，如以下示例所示：

```
a = math.cos(3 * (x - n)) + \\
    math.sin(3 * (y - n)))
```

当三引号字符串、列表、元组或字典的定义跨越多行时，不需要行继续字符。更一般地说，程序中用括号(...)、方括号[...]、大括号{...}或三引号括起来的任何部分都可以跨越多行，而无需使用行继续符，因为它们清楚地标记了定义的开始和结束。

缩进用于表示不同的代码块，例如函数、条件、循环和类的主体。块的第一条语句使用的缩进量是任意的，但整个块的缩进必须一致。以下是一个示例：

```
if a:
    statement1    # Consistent indentation
    statement2
else:
    statement3
        statement4   # Inconsistent indentation (error)
```

如果函数、条件、循环或类的主体很短且只包含一条语句，可以将其放在同一行，如下所示：

```
if a: statement1
else: statement2
```

要表示空主体或块，请使用pass语句。以下是一个示例：

```
if a:
    pass
else:
    statements
```

虽然可以使用制表符进行缩进，但不鼓励这种做法。Python编程社区普遍偏好（并鼓励）使用空格。当遇到制表符时，它们会被转换为移动到下一个8的倍数的列所需的空格数（例如，出现在第11列的制表符会插入足够的空格以移动到第16列）。使用`-t`选项运行Python时，当同一程序块中制表符和空格混合不一致时，会打印警告消息。`-tt`选项会将这些警告消息转换为`TabError`异常。

要在一行上放置多条语句，请用分号(`;`)分隔语句。包含单个语句的行也可以用分号结束，尽管这是不必要的。

`#`字符表示注释，延伸到行尾。但是，出现在引号字符串内的`#`不会开始注释。

最后，解释器忽略所有空行，除非在交互模式下运行。在这种情况下，当输入跨越多行的语句时，空行表示输入结束。

#### 标识符和保留字

*标识符*是用于标识变量、函数、类、模块和其他对象的名称。标识符可以包含字母、数字和下划线字符(`_`)，但必须始终以非数字字符开头。字母目前仅限于ISO–Latin字符集中的字符A–Z和a–z。因为标识符区分大小写，所以`FOO`与`foo`不同。特殊符号如`$`、`%`和`@`不允许在标识符中使用。此外，`if`、`else`和`for`等词是保留的，不能用作标识符名称。以下列表显示了所有保留字：

- and
- as
- assert
- break
- class
- continue
- def
- del
- elif
- else
- except
- exec
- finally
- for
- from
- global
- if
- import
- in
- is
- lambda
- nonlocal
- not
- or
- pass
- print
- raise
- return
- try
- while
- with
- yield

以或以下划线结尾的标识符通常具有特殊含义。例如，以下划线开头的标识符（如`_foo`）不会被`from module import *`语句导入。具有前导和尾随双下划线的标识符（如`__init__`）保留用于特殊方法，而具有前导双下划线的标识符（如`__bar`）用于实现私有类成员，如第7章“类和面向对象编程”中所述。应避免类似标识符的通用用途。

#### 数字字面量

有四种内置数字字面量类型：

- 布尔值
- 整数



##### 数字与表达式

Python 支持浮点数、复数以及其他数字类型。

标识符 `True` 和 `False` 被解释为布尔值，分别对应整数值 1 和 0。像 `1234` 这样的数字被解释为十进制整数。要使用八进制、十六进制或二进制记法指定整数，需在数值前分别加上 `0`、`0x` 或 `0b`（例如 `0644`、`0x100fea8` 或 `0b11101010`）。

Python 中的整数可以有任意多位数字，因此如果你想指定一个非常大的整数，只需写出所有数字即可，如 `12345678901234567890`。然而，在检查值和查看旧版 Python 代码时，你可能会看到大数字后面带有一个小写 *L* 或大写 `L` 字符，如 `12345678901234567890L`。这个尾随的 `L` 与 Python 内部根据数值大小将整数表示为固定精度机器整数或任意精度长整型整数有关。在旧版本的 Python 中，你可以显式选择使用哪种类型，并通过添加尾随的 `L` 来明确表示长整型。如今，这种区分已不再必要，并且被明确不鼓励使用。因此，如果你想要一个大整数，只需直接写出它，无需加上 `L`。

像 `123.34` 和 `1.2334e+02` 这样的数字被解释为浮点数。带有尾随 `j` 或 `J` 的整数或浮点数，如 `12.34J`，是虚数。你可以通过将一个实数与一个虚数相加来创建具有实部和虚部的复数，如 `1.2 + 12.34j`。

#### 字符串字面量

字符串字面量用于指定字符序列，通过将文本括在单引号（`'`）、双引号（`"`）或三引号（`'''` 或 `"""`）中来定义。除了要求使用相同类型的引号来开始和结束字符串外，不同的引号样式在语义上没有区别。单引号和双引号字符串必须在单行内定义，而三引号字符串可以跨越多行并包含所有封闭的格式（即换行符、制表符、空格等）。相邻的字符串（由空白、换行符或行续接字符分隔），如 `"hello" 'world'`，会被连接成一个单一的字符串 `"helloworld"`。

在字符串字面量中，反斜杠（`\`）字符用于转义特殊字符，如换行符、反斜杠本身、引号和非打印字符。表 2.1 显示了可接受的转义代码。无法识别的转义序列将按原样保留在字符串中，并包含前导反斜杠。

**表 2.1 标准字符转义代码**

| 字符 | 描述 |
|---|---|
| `\` | 换行续接 |
| `\\` | 反斜杠 |
| `\'` | 单引号 |
| `\"` | 双引号 |
| `\a` | 响铃 |
| `\b` | 退格 |
| `\e` | 转义 |
| `\0` | 空字符 |
| `\n` | 换行 |
| `\v` | 垂直制表符 |
| `\t` | 水平制表符 |
| `\r` | 回车 |
| `\f` | 换页 |
| `\000` | 八进制值（`\000` 到 `\377`） |
| `\uxxxx` | Unicode 字符（`\u0000` 到 `\uffff`） |
| `\Uxxxxxxxx` | Unicode 字符（`\U00000000` 到 `\Uffffffff`） |
| `\N{*charname*}` | Unicode 字符名 |
| `\xhh` | 十六进制值（`\x00` 到 `\xff`） |

转义代码 `\000` 和 `\x` 用于将无法轻易输入的字符（即控制代码、非打印字符、符号、国际字符等）嵌入字符串字面量。对于这些转义代码，你必须指定对应于字符值的整数值。例如，如果你想为单词 "Jalapeño" 编写一个字符串字面量，你可以将其写成 `"Jalape\xf1o"`，其中 `\xf1` 是 ñ 的字符代码。

在 Python 2 中，字符串字面量对应于 8 位字符或面向字节的数据。这些字符串的一个严重限制是它们不完全支持国际字符集和 Unicode。为了解决这个限制，Python 2 为 Unicode 数据使用单独的字符串类型。要编写 Unicode 字符串字面量，你需要在第一个引号前加上字母 "u"。例如：

```
s = u"Jalape\u00f1o"
```

在 Python 3 中，这个前缀字符是不必要的（实际上是语法错误），因为所有字符串都已经是 Unicode。如果你使用 `-U` 选项运行解释器，Python 2 会模拟此行为（在这种情况下，所有字符串字面量都将被视为 Unicode，并且可以省略 `u` 前缀）。

无论你使用哪个 Python 版本，表 2.1 中的 `\u`、`\U` 和 `\N` 转义代码都用于在 Unicode 字面量中插入任意字符。每个 Unicode 字符都有一个分配的*码点*，这通常在 Unicode 图表中表示为 `U+XXXX`，其中 `XXXX` 是四位或更多位的十六进制数字序列。（请注意，此表示法不是 Python 语法，但作者在描述 Unicode 字符时经常使用。）例如，字符 ñ 的码点是 `U+00F1`。`\u` 转义代码用于插入码点在 `U+0000` 到 `U+FFFF` 范围内的 Unicode 字符（例如 `\u00f1`）。`\U` 转义代码用于插入 `U+10000` 及以上范围内的字符（例如 `\U00012345`）。关于 `\U` 转义代码的一个微妙警告是，码点高于 `U+10000` 的 Unicode 字符通常会分解为一对字符，称为*代理对*。这与 Unicode 字符串的内部表示有关，在第 3 章“类型与对象”中有更详细的介绍。

Unicode 字符也有一个描述性名称。如果你知道这个名称，你可以使用 `\N{*character name*}` 转义序列。例如：

```
s = u"Jalape\N{LATIN SMALL LETTER N WITH TILDE}o"
```

有关码点和字符名称的权威参考，请查阅 http://www.unicode.org/charts。

可选地，你可以在字符串字面量前加上 r 或 R，如 `r'\d'`。这些字符串被称为*原始字符串*，因为它们的所有反斜杠字符都保持不变——即字符串字面上包含封闭的文本，包括反斜杠。原始字符串的主要用途是指定反斜杠字符具有特定含义的字面量。例如，使用 `re` 模块指定正则表达式模式，或在 Windows 机器上指定文件名（例如 `r'c:\newdata\tests'`）。

原始字符串不能以单个反斜杠结尾，如 `r"\"`。在原始字符串中，`\uXXXX` 转义序列仍然会被解释为 Unicode 字符，前提是前面的 `\` 字符数量为奇数。例如，`ur"\u1234"` 定义了一个包含单个字符 U+1234 的原始 Unicode 字符串，而 `ur"\\u1234"` 定义了一个七字符字符串，其中前两个字符是斜杠，其余五个字符是字面上的 "u1234"。此外，在 Python 2.2 中，在原始 Unicode 字符串中，r 必须出现在 u 之后，如上所示。在 Python 3.0 中，u 前缀是不必要的。

字符串字面量不应使用与 UTF-8 或 UTF-16 等数据编码对应的原始字节序列来定义。例如，直接编写原始的 UTF-8 编码字符串，如 `'Jalape\xc3\xb1o'`，只会产生一个九字符字符串 U+004A、U+0061、U+006C、U+0061、U+0070、U+0065、U+00C3、U+00B1、U+006F，这可能不是你想要的结果。这是因为在 UTF-8 中，多字节序列 `\xc3\xb1` 应该表示单个字符 U+00F1，而不是两个字符 U+00C3 和 U+00B1。要指定一个编码字节串作为字面量，你需要在第一个引号前加上 "b"，如 `b"Jalape\xc3\xb1o"`。定义时，这实际上会创建一个单个字节的字符串。从这个表示中，可以通过解码字节字面量的值，使用其 `decode()` 方法来创建一个普通字符串。更多细节在第 3 章和第 4 章“运算符与表达式”中有介绍。

字节字面量在大多数程序中很少使用，因为这种语法直到 Python 2.6 才出现，并且在该版本中字节字面量与普通字符串没有区别。然而，在 Python 3 中，字节字面量被映射到一个新的字节数据类型，其行为与普通字符串不同（参见附录 A“Python 3”）。

#### 容器

括在方括号 `[...]`、圆括号 `(...)` 和花括号 `{...}` 中的值分别表示列表、元组和字典中包含的对象集合，如下例所示：

```
a = [ 1, 3.4, 'hello' ]         # 一个列表
b = ( 10, 20, 30 )              # 一个元组
c = { 'a': 3, 'b': 42 }         # 一个字典
```

列表、元组和字典字面量可以跨越多行，而无需使用行续接字符（`\`）。此外，最后一个项目后允许有一个尾随逗号。例如：

```
a = [ 1,
    3.4,
    'hello',
  ]
```



#### 运算符、分隔符和特殊符号

以下运算符被识别：

```
+    -    *    **    /    //    %    <<    >>    &    |
^    ~    <    >    <=    >=    ==    !=    <>    +=
-=   *=   /=   //=   %=   **=   &=   |=   ^=   >>=   <<=
```

以下符号用作表达式、列表、字典和语句各部分的**分隔符**：

```
(    )    [    ]    {    }    ,    :    .    `    =    ;
```

例如，等号（`=`）字符用作赋值中名称和值之间的分隔符，而逗号（`,`）字符用于分隔函数的参数、列表和元组中的元素等。句点（`.`）也用于浮点数和扩展切片操作中使用的省略号（`...`）。

最后，还使用以下特殊符号：

```
'    "    #    \    @
```

字符`$`和`?`在Python中没有意义，不能出现在程序中，除非在引号字符串字面量内。

##### 文档字符串

如果模块、类或函数定义的第一条语句是一个字符串，那么该字符串就成为相关对象的*文档字符串*，如下面的示例所示：

```
def fact(n):
    "This function computes a factorial"
    if (n <= 1): return 1
    else: return n * fact(n - 1)
```

代码浏览和文档生成工具有时会使用文档字符串。这些字符串可在对象的`__doc__`属性中访问，如下所示：

```
>>> print fact.__doc__
This function computes a factorial
>>>
```

文档字符串的缩进必须与定义中的所有其他语句一致。此外，文档字符串不能是计算结果或从变量作为表达式赋值的。文档字符串必须始终是用引号括起来的字符串字面量。

#### 装饰器

函数、方法或类定义可以前面加上一个称为*装饰器*的特殊符号，其目的是修改其后定义的行为。装饰器用`@`符号表示，必须放在单独的行上，紧接在相应的函数、方法或类之前。下面是一个示例：

```
class Foo(object):
    @staticmethod
    def bar():
        pass
```

可以使用多个装饰器，但每个装饰器必须放在单独的行上。下面是一个示例：

```
@foo
@bar
def spam():
    pass
```

更多关于装饰器的信息可以在第6章“函数和函数式编程”和第7章“类和面向对象编程”中找到。

#### 源代码编码

Python源程序通常用标准7位ASCII编写。但是，在Unicode环境中工作的用户可能会觉得这很麻烦——特别是如果他们必须编写大量带有国际字符的字符串字面量。

可以通过在Python程序的第二行（或第一行）包含特殊编码注释，用不同的编码编写Python源代码：

```
#!/usr/bin/env python
##### -*- coding: UTF-8 -*-

s = "Jalapeño"  # String in quotes is directly encoded in UTF-8.
```

当提供了特殊的`coding:`注释后，可以使用支持Unicode的编辑器直接输入字符串字面量。但是，Python的其他元素，包括标识符名称和保留字，仍应限制为ASCII字符。

*此页有意留白*

### 类型和对象

Python程序中存储的所有数据都是围绕*对象*的概念构建的。对象包括基本数据类型，如数字、字符串、列表和字典。但是，也可以以类的形式创建用户定义的对象。此外，与程序结构和解释器内部操作相关的大多数对象也是公开的。本章描述了Python对象模型的内部工作原理，并提供了内置数据类型的概述。第4章“运算符和表达式”进一步描述了运算符和表达式。第7章“类和面向对象编程”描述了如何创建用户定义的对象。

#### 术语

程序中存储的每一块数据都是一个对象。每个对象都有一个标识、一个类型（也称为其类）和一个值。例如，当您编写`a = 42`时，会创建一个值为`42`的整数对象。您可以将对象的*标识*视为指向其在内存中位置的指针。`a`是引用此特定位置的名称。

对象的*类型*（也称为对象的*类*）描述了对象的内部表示以及它支持的方法和操作。当创建特定类型的对象时，该对象有时被称为该类型的*实例*。实例创建后，其标识和类型不能更改。如果对象的值可以修改，则该对象是*可变的*。如果值不能修改，则该对象是*不可变的*的。包含对其他对象引用的对象被称为*容器*或*集合*。

大多数对象由许多数据属性和方法表征。*属性*是与对象关联的值。*方法*是当方法作为函数调用时，对对象执行某种操作的函数。属性和方法使用点（`.`）运算符访问，如下面的示例所示：

```
a = 3 + 4j         # Create a complex number
r = a.real         # Get the real part (an attribute)

b = [1, 2, 3]      # Create a list
b.append(7)        # Add a new element using the append method
```

#### 对象标识和类型

内置函数`id()`返回对象的标识（一个整数）。这个整数通常对应于对象在内存中的位置，尽管这取决于Python实现，并且不应对此标识进行任何此类解释。`is`运算符比较两个对象的标识。内置函数`type()`返回对象的类型。下面是比较两个对象的不同方式的示例：

```
##### Compare two objects
def compare(a,b):
    if a is b:
        # a and b are the same object
        statements
    if a == b:
        # a and b have the same value
        statements
    if type(a) is type(b):
        # a and b have the same type
        statements
```

对象的类型本身是一个对象，称为对象的类。这个对象是唯一定义的，并且对于给定类型的所有实例总是相同的。因此，可以使用`is`运算符比较类型。所有类型对象都被赋予可用于执行类型检查的名称。大多数这些名称是内置的，如`list`、`dict`和`file`。下面是一个示例：

```
if type(s) is list:
    s.append(item)

if type(d) is dict:
    d.update(t)
```

因为可以通过定义类来特化类型，所以检查类型的更好方法是使用内置的`isinstance(object, type)`函数。下面是一个示例：

```
if isinstance(s,list):
    s.append(item)

if isinstance(d,dict):
    d.update(t)
```

因为`isinstance()`函数了解继承，所以它是检查任何Python对象类型的首选方式。

尽管可以在程序中添加类型检查，但类型检查通常并不像你想象的那么有用。首先，过度的检查会严重影响性能。其次，程序并不总是定义能完美适合继承层次结构的对象。例如，如果前面的`isinstance(s,list)`语句的目的是测试`s`是否“像列表”，那么对于具有与列表相同的编程接口但不直接继承内置`list`类型的对象，它将不起作用。向程序添加类型检查的另一个选项是定义抽象基类。这将在第7章中描述。

#### 引用计数和垃圾回收

所有对象都是引用计数的。对象的引用计数在每次将其分配给新名称或放置在容器（如列表、元组或字典）中时都会增加，如下所示：

```
a = 37      # Creates an object with value 37
b = a       # Increases reference count on 37
c = []
c.append(b) # Increases reference count on 37
```



此示例创建一个包含值37的单个对象。`a`仅是指向新创建对象的名称。当`b`被赋值为`a`时，`b`成为同一对象的新名称，该对象的引用计数增加。同样，当将`b`放入列表中时，该对象的引用计数再次增加。在整个示例中，只有一个对象包含37。所有其他操作都只是在为该对象创建新的引用。

对象的引用计数会因`del`语句或引用超出作用域（或被重新赋值）而减少。以下是一个示例：

```
del a     # 减少37的引用计数
b = 42    # 减少37的引用计数
c[0] = 2.0 # 减少37的引用计数
```

可以使用`sys.getrefcount()`函数获取对象的当前引用计数。例如：

```
>>> a = 37
>>> import sys
>>> sys.getrefcount(a)
7
>>> 
```

在许多情况下，引用计数比你可能猜测的要高得多。对于不可变数据（如数字和字符串），解释器会积极地在程序的不同部分之间共享对象以节省内存。

当对象的引用计数达到零时，它将被垃圾回收。然而，在某些情况下，一组不再使用的对象之间可能存在循环依赖。以下是一个示例：

```
a = { }
b = { }
a['b'] = b      # a包含对b的引用
b['a'] = a      # b包含对a的引用
del a
del b
```

在此示例中，`del`语句减少了`a`和`b`的引用计数，并销毁了用于引用底层对象的名称。然而，因为每个对象都包含对另一个对象的引用，所以引用计数不会降为零，对象保持分配状态（导致内存泄漏）。为了解决这个问题，解释器会定期执行一个循环检测器，该检测器搜索不可访问对象的循环并删除它们。循环检测算法在解释器在执行过程中分配越来越多内存时周期性运行。确切的行为可以使用`gc`模块中的函数进行微调和控制（参见第13章“Python运行时服务”）。

#### 引用与拷贝

当程序执行诸如`a = b`的赋值操作时，会创建一个对`b`的新引用。对于不可变对象（如数字和字符串），此赋值实际上创建了`b`的一个副本。然而，对于可变对象（如列表和字典），行为则大不相同。以下是一个示例：

```
>>> a = [1,2,3,4]
>>> b = a         # b是a的引用
>>> b is a
True
>>> b[2] = -100		# 更改b中的一个元素
>>> a				# 注意a也发生了变化
[1, 2, -100, 4]
>>>
```

因为在这个示例中`a`和`b`引用同一个对象，所以对其中一个变量所做的更改会反映在另一个变量中。为了避免这种情况，你必须创建对象的副本，而不是新的引用。

对容器对象（如列表和字典）应用两种类型的拷贝操作：浅拷贝和深拷贝。浅拷贝创建一个新对象，但使用对原始对象中包含项目的引用来填充它。以下是一个示例：

```
>>> a = [ 1, 2, [3,4] ]
>>> b = list(a)		# 创建a的浅拷贝。
>>> b is a
False
>>> b.append(100)	# 向b追加元素。
>>> b
[1, 2, [3, 4], 100]
>>> a				# 注意a未改变
[1, 2, [3, 4]]
>>> b[2][0] = -100	# 修改b中的一个元素
>>> b
[1, 2, [-100, 4], 100]
>>> a				# 注意a内部的变化
[1, 2, [-100, 4]]
>>>
```

在这种情况下，`a`和`b`是独立的列表对象，但它们包含的元素是共享的。因此，修改`a`的一个元素也会修改`b`的一个元素，如所示。

深拷贝创建一个新对象，并递归地复制其包含的所有对象。没有内置操作来创建对象的深拷贝。但是，可以使用标准库中的`copy.deepcopy()`函数，如下面的示例所示：

```
>>> import copy
>>> a = [1, 2, [3, 4]]
>>> b = copy.deepcopy(a)
>>> b[2][0] = -100
>>> b
[1, 2, [-100, 4]]
>>> a				# 注意a未改变
[1, 2, [3, 4]]
>>>
```

#### 一等对象

Python中的所有对象都被称为“一等对象”。这意味着所有可以通过标识符命名的对象都具有同等地位。这也意味着所有可以命名的对象都可以被视为数据。例如，这是一个包含两个值的简单字典：

```
items = {
    'number' : 42,
    'text' : "Hello World"
}
```

通过向此字典添加一些更不寻常的项目，可以看到对象的一等性质。以下是一些示例：

```
items["func"]  = abs           # 添加abs()函数
import math
items["mod"]   = math          # 添加一个模块
items["error"] = ValueError    # 添加一个异常类型
nums = [1,2,3,4]
items["append"] = nums.append  # 添加另一个对象的方法
```

在此示例中，`items`字典包含一个函数、一个模块、一个异常和另一个对象的方法。如果你愿意，可以对`items`使用字典查找来代替原始名称，代码仍然有效。例如：

```
>>> items["func"](-45)        # 执行abs(-45)
45
>>> items["mod"].sqrt(4)      # 执行math.sqrt(4)
2.0
>>> try:
...     x = int("a lot")
... except items["error"] as e:  # 等同于 except ValueError as e
...     print("Couldn't convert")
...
Couldn't convert
>>> items["append"](100)      # 执行nums.append(100)
>>> nums
[1, 2, 3, 4, 100]
>>>
``

Python中一切皆一等的事实，新程序员往往没有充分认识到。然而，它可以用来编写非常紧凑和灵活的代码。例如，假设你有一行文本，如`"GOOG,100,490.10"`，你想将其转换为一个包含适当类型转换的字段列表。这是一种聪明的方法，你可以通过创建一个类型列表（类型是一等对象）并执行几个简单的列表处理操作来实现：

```
>>> line = "GOOG,100,490.10"
>>> field_types = [str, int, float]
>>> raw_fields = line.split(',')
>>> fields = [ty(val) for ty,val in zip(field_types,raw_fields)]
>>> fields
['GOOG', 100, 490.10000000000002]
>>>
```

#### 用于表示数据的内置类型

大约有十几种内置数据类型用于表示程序中使用的大多数数据。这些类型被分为几个主要类别，如表3.1所示。表中的“类型名称”列列出了你可以使用`isinstance()`和其他类型相关函数检查该类型的名称或表达式。某些类型仅在Python 2中可用，并已如此标明（在Python 3中，它们已被弃用或合并到其他类型之一中）。

##### 表3.1 用于数据表示的内置类型

| 类型类别 | 类型名称 | 描述 |
| --- | --- | --- |
| None | type(None) | 空对象None |
| 数字 | int | 整数 |
| | long | 任意精度整数（仅限Python 2） |
| | float | 浮点数 |
| | complex | 复数 |
| | bool | 布尔值（`True`或`False`） |
| 序列 | str | 字符串 |
| | unicode | Unicode字符串（仅限Python 2） |
| | list | 列表 |
| | tuple | 元组 |
| | xrange | 由`xrange()`创建的整数范围（在Python 3中，它被称为`range`。） |
| 映射 | dict | 字典 |
| 集合 | set | 可变集合 |
| | frozenset | 不可变集合 |

##### None类型

`None`类型表示一个空对象（一个没有值的对象）。Python恰好提供一个空对象，在程序中写作`None`。这个对象由那些没有显式返回值的函数返回。`None`经常用作可选参数的默认值，以便函数可以检测调用者是否实际传递了该参数的值。`None`没有属性，在布尔表达式中求值为`False`。

##### 数字类型

Python使用五种数字类型：布尔类型、整数、长整数、浮点数和复数。除布尔类型外，所有数字对象都是有符号的。所有数字类型都是不可变的。

布尔类型由两个值表示：`True`和`False`。名称`True`和`False`分别映射到数值1和0。

整数表示范围在−2147483648到2147483647之间的整数（在某些机器上范围可能更大）。长整数表示范围无限的整数（仅受可用内存限制）。尽管有两种整数类型，Python试图使这种区分无缝（事实上，在Python 3中，这两种类型已统一为单个整数类型）。因此，尽管你有时会在现有的Python代码中看到对长整数的引用，但这主要是一个可以忽略的实现细节——只需对所有整数操作使用整数类型即可。一个例外是在执行整数值显式类型检查的代码中。在Python 2中，如果`x`是一个已提升为长整数的整数，表达式`isinstance(x, int)`将返回`False`。

浮点数使用机器上原生双精度（64位）浮点数表示法表示。通常这是IEEE 754，它提供大约17位精度和范围在



##### 数值类型

`float` 类型表示 IEEE 754 双精度浮点数，其范围大约为 1.7976931348623157E+308 到 -1.7976931348623157E+308。这与 C 语言中的 `double` 类型相同。Python 不支持 32 位单精度浮点数。如果在程序中需要精确控制数字的存储空间和精度，可以考虑使用 numpy 扩展（可在 http://numpy.sourceforge.net 找到）。

复数由一对浮点数表示。复数 `z` 的实部和虚部分别可通过 `z.real` 和 `z.imag` 获取。方法 `z.conjugate()` 计算 `z` 的复共轭（`a+bj` 的共轭为 `a-bj`）。

数值类型具有许多属性和方法，旨在简化涉及混合算术的操作。为了与有理数（在 `fractions` 模块中）简化兼容，整数具有 `x.numerator` 和 `x.denominator` 属性。整数或浮点数 `y` 具有 `y.real` 和 `y.imag` 属性以及 `y.conjugate()` 方法，以便与复数兼容。浮点数 `y` 可以使用 `y.as_integer_ratio()` 转换为表示分数的一对整数。方法 `y.is_integer()` 测试浮点数 `y` 是否表示整数值。方法 `y.hex()` 和 `y.fromhex()` 可用于以底层二进制表示形式处理浮点数。

库模块中定义了几种额外的数值类型。`decimal` 模块支持通用的十进制算术。`fractions` 模块添加了有理数类型。这些模块在第 14 章"数学"中介绍。

##### 序列类型

*序列* 表示由非负整数索引的有序对象集合，包括字符串、列表和元组。字符串是字符序列，列表和元组是任意 Python 对象的序列。字符串和元组是不可变的；列表允许插入、删除和替换元素。所有序列都支持迭代。

###### 所有序列共有的操作

表 3.2 显示了可应用于所有序列类型的运算符和方法。使用索引运算符 `s[i]` 选择序列 `s` 的第 `i` 个元素，使用切片运算符 `s[i:j]` 或扩展切片运算符 `s[i:j:stride]` 选择子序列（这些操作在第 4 章中描述）。任何序列的长度都使用内置函数 `len(s)` 返回。可以使用内置函数 `min(s)` 和 `max(s)` 查找序列的最小值和最大值。但是，这些函数仅适用于元素可以排序的序列（通常是数字和字符串）。`sum(s)` 对 `s` 中的项求和，但仅适用于数值数据。

表 3.3 显示了可应用于可变序列（如列表）的额外运算符。

####### 表 3.2 所有序列共有的操作

| 项目 | 描述 |
|------|-------------|
| `s[i]` | 返回序列的第 `i` 个元素 |
| `s[i:j]` | 返回一个切片 |
| `s[i:j:stride]` | 返回一个扩展切片 |
| `len(s)` | `s` 中的元素数量 |
| `min(s)` | `s` 中的最小值 |
| `max(s)` | `s` 中的最大值 |
| `sum(s [,initial])` | `s` 中各项的和 |
| `all(s)` | 检查 `s` 中的所有项是否都为 `True`。 |
| `any(s)` | 检查 `s` 中是否有任何项为 `True`。 |

####### 表 3.3 适用于可变序列的操作

| 项目 | 描述 |
|------|-------------|
| `s[i] = v` | 元素赋值 |
| `s[i:j] = t` | 切片赋值 |
| `s[i:j:stride] = t` | 扩展切片赋值 |
| `del s[i]` | 元素删除 |
| `del s[i:j]` | 切片删除 |
| `del s[i:j:stride]` | 扩展切片删除 |

###### 列表

列表支持表 3.4 中显示的方法。内置函数 `list(s)` 将任何可迭代类型转换为列表。如果 `s` 已经是列表，此函数会构造一个新列表，作为 `s` 的浅拷贝。`s.append(x)` 方法将新元素 `x` 追加到列表末尾。`s.index(x)` 方法在列表中搜索 `x` 的第一次出现。如果未找到此类元素，则引发 `ValueError` 异常。类似地，`s.remove(x)` 方法从列表中删除 `x` 的第一次出现，如果未找到此类项则引发 `ValueError`。`s.extend(t)` 方法通过追加序列 `t` 中的元素来扩展列表 `s`。

`s.sort()` 方法对列表元素进行排序，并可选择接受一个键函数和反转标志，两者都必须指定为关键字参数。键函数是在排序期间比较之前应用于每个元素的函数。如果给定，此函数应将单个项作为输入，并返回用于执行排序比较的值。如果希望执行特殊类型的排序操作（例如对字符串列表进行不区分大小写的排序），指定键函数会很有用。`s.reverse()` 方法反转列表中项的顺序。`sort()` 和 `reverse()` 方法都就地操作列表元素并返回 `None`。

####### 表 3.4 列表方法

| 方法 | 描述 |
|--------|-------------|
| `list(s)` | 将 `s` 转换为列表。 |
| `s.append(x)` | 将新元素 `x` 追加到 `s` 的末尾。 |
| `s.extend(t)` | 将新列表 `t` 追加到 `s` 的末尾。 |
| `s.count(x)` | 统计 `x` 在 `s` 中出现的次数。 |
| `s.index(x [,start [,stop]])` | 返回满足 `s[i]==x` 的最小 `i`。`start` 和 `stop` 可选择指定搜索的起始和结束索引。 |
| `s.insert(i,x)` | 在索引 `i` 处插入 `x`。 |
| `s.pop([i])` | 返回元素 `i` 并将其从列表中删除。如果省略 `i`，则返回最后一个元素。 |
| `s.remove(x)` | 搜索 `x` 并将其从 `s` 中删除。 |
| `s.reverse()` | 就地反转 `s` 中的项。 |
| `s.sort([key [, reverse]])` | 就地排序 `s` 中的项。`key` 是键函数。`reverse` 是按相反顺序排序列表的标志。`key` 和 `reverse` 应始终指定为关键字参数。 |

#### 字符串

Python 2 提供了两种字符串对象类型。字节字符串是包含 8 位数据的字节序列。它们可能包含二进制数据和嵌入的 NULL 字节。Unicode 字符串是未编码 Unicode 字符的序列，在内部由 16 位整数表示。这允许 65,536 个唯一字符值。尽管 Unicode 标准支持多达 100 万个唯一字符值，但 Python 默认不支持这些额外字符。相反，它们被编码为称为*代理对*的特殊双字符（4 字节）序列——其解释取决于应用程序。作为可选功能，Python 可以构建为使用 32 位整数存储 Unicode 字符。启用后，这允许 Python 表示从 U+000000 到 U+110000 的整个 Unicode 值范围。所有与 Unicode 相关的函数都会相应调整。

字符串支持表 3.5 中显示的方法。尽管这些方法操作字符串实例，但没有任何方法实际修改底层字符串数据。因此，`s.capitalize()`、`s.center()` 和 `s.expandtabs()` 等方法始终返回新字符串，而不是修改字符串 `s`。字符测试（如 `s.isalnum()` 和 `s.isupper()`）如果字符串 `s` 中的所有字符都满足测试则返回 `True` 或 `False`。此外，如果字符串长度为零，这些测试始终返回 `False`。

`s.find()`、`s.index()`、`s.rfind()` 和 `s.rindex()` 方法用于在 `s` 中搜索子字符串。所有这些函数都返回 `s` 中子字符串的整数索引。此外，如果未找到子字符串，`find()` 方法返回 `-1`，而 `index()` 方法引发 `ValueError` 异常。`s.replace()` 方法用于将子字符串替换为替换文本。需要强调的是，所有这些方法仅适用于简单子字符串。正则表达式模式匹配和搜索由 `re` 库模块中的函数处理。

`s.split()` 和 `s.rsplit()` 方法将字符串分割为由分隔符分隔的字段列表。`s.partition()` 和 `s.rpartition()` 方法搜索分隔符子字符串，并将 `s` 分割为三个部分：分隔符之前的文本、分隔符本身和分隔符之后的文本。

许多字符串方法接受可选的 `start` 和 `end` 参数，它们是指定 `s` 中起始和结束索引的整数值。在大多数情况下，这些值用于将操作限制在 `s` 的子字符串上。如果 `start` 或 `end` 为负数，则索引相对于字符串末尾。



####### 字符串方法

`s.translate()` 方法用于执行高级字符替换，例如快速去除字符串中的所有控制字符。作为参数，它接受一个转换表，其中包含原始字符串中的字符与结果中字符之间的一一对应关系。对于 8 位字符串，转换表是一个 256 字符的字符串。对于 Unicode，转换表可以是任意序列对象 `s`，其中 `s[n]` 返回一个整数字符编码或 Unicode 字符，对应于整数值为 `n` 的 Unicode 字符。

`s.encode()` 和 `s.decode()` 方法用于将字符串数据转换为指定的字符编码，或从指定的字符编码转换回来。作为输入，这些方法接受诸如 `'ascii'`、`'utf-8'` 或 `'utf-16'` 之类的编码名称。这些方法最常用于将 Unicode 字符串转换为适合 I/O 操作的数据编码，更多内容请参阅第 9 章“输入和输出”。请注意，在 Python 3 中，`encode()` 方法仅在字符串上可用，而 `decode()` 方法仅在 bytes 数据类型上可用。

`s.format()` 方法用于执行字符串格式化。作为参数，它接受位置参数和关键字参数的任意组合。`s` 中用 `{item}` 表示的占位符会被相应的参数替换。位置参数可以使用 `{0}`、`{1}` 等占位符引用。关键字参数则使用带名称的占位符（如 `{name}`）引用。下面是一个示例：

```
>>> a = "Your name is {0} and your age is {age}"
>>> a.format("Mike", age=40)
'Your name is Mike and your age is 40'
>>>
```

在特殊的格式化字符串中，`{item}` 占位符还可以包含简单的索引和属性查找。`{item[n]}` 占位符（其中 `n` 是数字）会对 `item` 执行序列查找。`{item[key]}` 占位符（其中 `key` 是非数字字符串）会对 `item["key"]` 执行字典查找。`{item.attr}` 占位符引用 `item` 的属性 `attr`。有关 `format()` 方法的更多细节，请参阅第 4 章的“字符串格式化”一节。

######## 表 3.5 字符串方法

| 方法 | 描述 |
| --- | --- |
| `s.capitalize()` | 将第一个字符大写。 |
| `s.center(width [, pad])` | 将字符串在长度为 `width` 的字段中居中。`pad` 是填充字符。 |
| `s.count(sub [,start [,end]])` | 统计指定子串 `sub` 出现的次数。 |
| `s.decode([encoding [,errors]])` | 解码字符串并返回 Unicode 字符串（仅适用于字节字符串）。 |
| `s.encode([encoding [,errors]])` | 返回字符串的编码版本（仅适用于 Unicode 字符串）。 |
| `s.endswith(suffix [,start [,end]])` | 检查字符串末尾是否有指定后缀。 |
| `s.expandtabs([tabsize])` | 将制表符替换为空格。 |
| `s.find(sub [, start [,end]])` | 查找指定子串 `sub` 的第一次出现位置，未找到则返回 -1。 |
| `s.format(*args, **kwargs)` | 格式化 *s*。 |
| `s.index(sub [, start [,end]])` | 查找指定子串 *sub* 的第一次出现位置，未找到则引发错误。 |
| `s.isalnum()` | 检查所有字符是否都是字母或数字。 |
| `s.isalpha()` | 检查所有字符是否都是字母。 |
| `s.isdigit()` | 检查所有字符是否都是数字。 |
| `s.islower()` | 检查所有字符是否都是小写。 |
| `s.isspace()` | 检查所有字符是否都是空白字符。 |
| `s.istitle()` | 检查字符串是否为标题大小写字符串（每个单词的首字母大写）。 |
| `s.isupper()` | 检查所有字符是否都是大写。 |
| `s.join(t)` | 以 *s* 作为分隔符，连接序列 *t* 中的字符串。 |
| `s.ljust(width [, fill])` | 在大小为 *width* 的字符串中将 *s* 左对齐。 |
| `s.lower()` | 转换为小写。 |
| `s.lstrip([chrs])` | 移除前导空白或 *chrs* 中提供的字符。 |
| `s.partition(sep)` | 根据分隔符字符串 *sep* 对字符串进行分割。返回元组 (*head*, *sep*, *tail*)；如果未找到 *sep*，则返回 (*s*, `"",""`)。 |
| `s.replace(old, new [,maxreplace])` | 替换子串。 |
| `s.rfind(sub [,start [,end]])` | 查找子串的最后一次出现位置。 |
| `s.rindex(sub [,start [,end]])` | 查找最后一次出现位置，未找到则引发错误。 |
| `s.rjust(width [, fill])` | 在长度为 *width* 的字符串中将 *s* 右对齐。 |
| `s.rpartition(sep)` | 根据分隔符 *sep* 对 *s* 进行分割，但从字符串末尾开始查找。 |
| `s.rsplit([sep [,maxsplit]])` | 使用 *sep* 作为分隔符从字符串末尾开始拆分。*maxsplit* 是要执行的最大拆分次数。如果省略 *maxsplit*，结果与 `split()` 方法相同。 |
| `s.rstrip([chrs])` | 移除尾部空白或 *chrs* 中提供的字符。 |
| `s.split([sep [,maxsplit]])` | 使用 *sep* 作为分隔符拆分字符串。*maxsplit* 是要执行的最大拆分次数。 |
| `s.splitlines([keepends])` | 将字符串拆分为行列表。如果 `keepends` 为 1，则保留行尾的换行符。 |
| `s.startswith(prefix [,start [,end]])` | 检查字符串是否以 `prefix` 开头。 |
| `s.strip([chrs])` | 移除前导和尾部空白或 `chrs` 中提供的字符。 |
| `s.swapcase()` | 将大写转换为小写，反之亦然。 |
| `s.title()` | 返回字符串的标题大小写版本。 |
| `s.translate(table [,deletechars])` | 使用字符转换表 `table` 对字符串进行转换，移除 `deletechars` 中的字符。 |
| `s.upper()` | 将字符串转换为大写。 |
| `s.zfill(width)` | 在字符串左侧用零填充，直到达到指定的 `width`。 |

####### `xrange()` 对象

内置函数 `xrange([i,] j [,stride])` 创建一个对象，该对象表示一个整数 *k* 的范围，满足 `i <= k < j`。第一个索引 `i` 和步长 `stride` 是可选的，默认值分别为 `0` 和 `1`。`xrange` 对象在每次访问时计算其值，并且尽管 `xrange` 对象看起来像序列，但实际上它有一定限制。例如，它不支持任何标准切片操作。这限制了 `xrange` 的用途，只能用于一些简单的应用，例如在简单循环中迭代。

需要注意的是，在 Python 3 中，`xrange()` 已被重命名为 `range()`。不过，它的工作方式与这里描述的完全相同。

###### 映射类型

*映射对象* 表示由另一组几乎任意的键值索引的任意对象集合。与序列不同，映射对象是无序的，可以通过数字、字符串和其他对象进行索引。映射是可变的。

字典是唯一内置的映射类型，也是 Python 中哈希表或关联数组的实现。你可以使用任意不可变对象作为字典的键值（字符串、数字、元组等）。包含可变对象的列表、字典和元组不能用作键（字典类型要求键值保持不变）。

要在映射对象中选择一个项目，请使用键索引运算符 `m[k]`，其中 *k* 是键值。如果未找到该键，则会引发 `KeyError` 异常。`len(m)` 函数返回映射对象中包含的项目数量。表 3.6 列出了相关方法和操作。

####### 表 3.6 字典的方法和操作

| 项目 | 描述 |
| --- | --- |
| `len(m)` | 返回 m 中的项目数量。 |
| `m[k]` | 返回 m 中键为 k 的项目。 |
| `m[k]=x` | 将 m[k] 设置为 x。 |
| `del m[k]` | 从 m 中移除 m[k]。 |
| `k in m` | 如果 k 是 m 中的键，则返回 True。 |
| `m.clear()` | 从 m 中移除所有项目。 |
| `m.copy()` | 复制 m。 |
| `m.fromkeys(s [,value])` | 创建一个以序列 s 中的元素为键、所有值均设为 value 的新字典。 |
| `m.get(k [,v])` | 如果找到则返回 m[k]；否则返回 v。 |
| `m.has_key(k)` | 如果 m 包含键 k 则返回 True；否则返回 False。（已弃用，请改用 in 运算符。仅 Python 2） |
| `m.items()` | 返回由 (key,value) 对组成的序列。 |
| `m.keys()` | 返回由键值组成的序列。 |
| `m.pop(k [,default])` | 如果找到则返回 m[k] 并将其从 m 中移除；否则，如果提供了 default 则返回 default，未提供则引发 KeyError。 |
| `m.popitem()` | 从 m 中移除一个随机的 (key,value) 对，并以元组形式返回。 |
| `m.setdefault(k [, v])` | 如果找到则返回 m[k]；否则返回 v 并设置 m[k] = v。 |
| `m.update(b)` | 将 b 中的所有对象添加到 m 中。 |
| `m.values()` | 返回 m 中所有值组成的序列。 |

表 3.6 中的大多数方法都用于操作或检索字典的内容。`m.clear()` 方法移除所有项目。`m.update(b)` 方法通过将映射对象 b 中的所有 (key,value) 对插入到当前映射对象中来更新它。`m.get(k [,v])` 方法检索一个对象，但允许设置可选的默认值 v，如果没有该键则返回 v。`m.setdefault(k [,v])` 方法类似于 `m.get()`，不同之处在于，如果没有对应对象，除了返回 v 之外，还会设置 `m[k] = v`。如果省略 v，则默认值为 None。`m.pop()` 方法从字典中返回一个项目，同时将其移除。`m.popitem()` 方法用于迭代地销毁字典的内容。

`m.copy()` 方法对映射对象中包含的项目进行浅拷贝，并将其放入一个新的映射对象中。`m.fromkeys(s [,value])` 方法创建一个新的映射，其键全部来自序列 s。结果映射的类型将与 m 相同。除非使用可选的 value 参数给出其他值，否则与所有这些键关联的值都设为 None。`fromkeys()` 方法被定义为类方法，因此另一种调用方式是使用类名，例如 `dict.fromkeys()`。

`m.items()` 方法返回一个包含 (key,value) 对的序列。`m.keys()` 方法返回一个包含所有键值的序列，`m.values()` 方法返回一个包含所有值的序列。对于这些方法，你应当假设对结果唯一可安全执行的操作是迭代。在 Python 2 中，结果是一个列表；而在 Python 3 中，结果是一个迭代器，用于迭代映射当前的内容。如果你编写的代码只是假设它是一个迭代器，它将

通常与Python的两个版本都兼容。如果需要将这些方法的结果存储为数据，请通过将其存储在列表中来创建副本。例如，`items = list(m.items())`。如果只想获取所有键的列表，请使用`keys = list(m)`。

###### 集合类型

*集合*是唯一项目的无序集合。与序列不同，集合不提供索引或切片操作。它们也与字典不同，因为对象没有与之关联的键值。放入集合中的项目必须是不可变的。有两种不同的集合类型可用：`set`是可变集合，`frozenset`是不可变集合。两种集合都使用一对内置函数创建：

```
s = set([1,5,10,15])
f = frozenset(['a',37,'hello'])
```

`set()`和`frozenset()`都通过迭代提供的参数来填充集合。两种集合都提供表3.7中概述的方法。

| 项目 | 描述 |
|------|-------------|
| `len(s)` | 返回*s*中项目的数量。 |
| `s.copy()` | 创建*s*的副本。 |
| `s.difference(t)` | 集合差集。返回*s*中所有不在*t*中的项目。 |
| `s.intersection(t)` | 交集。返回同时在*s*和*t*中的所有项目。 |
| `s.isdisjoint(t)` | 如果*s*和*t*没有共同项目，则返回`True`。 |
| `s.issubset(t)` | 如果*s*是*t*的子集，则返回`True`。 |
| `s.issuperset(t)` | 如果*s*是*t*的超集，则返回`True`。 |
| `s.symmetric_difference(t)` | 对称差集。返回在*s*或*t*中但不在两个集合中的所有项目。 |
| `s.union(t)` | 并集。返回*s*或*t*中的所有项目。 |

表3.7 **集合类型的方法和操作**

`s.difference(t)`、`s.intersection(t)`、`s.symmetric_difference(t)`和`s.union(t)`方法提供集合的标准数学运算。返回值与*s*（`set`或`frozenset`）类型相同。参数*t*可以是任何支持迭代的Python对象。这包括集合、列表、元组和字符串。这些集合操作也可以作为数学运算符使用，如第4章进一步所述。

可变集合（`set`）还提供表3.8中概述的方法。

| 项目 | 描述 |
|------|-------------|
| `s.add(item)` | 将*item*添加到*s*。如果*item*已在*s*中，则无效。 |
| `s.clear()` | 从*s*中移除所有项目。 |
| `s.difference_update(t)` | 从*s*中移除所有也在*t*中的项目。 |
| `s.discard(item)` | 从*s*中移除`item`。如果`item`不是*s*的成员，则不执行任何操作。 |
| `s.intersection_update(t)` | 计算*s*和*t*的交集，并将结果留在*s*中。 |
| `s.pop()` | 返回一个任意集合元素并将其从*s*中移除。 |
| `s.remove(item)` | 从*s*中移除`item`。如果`item`不是成员，则引发`KeyError`。 |
| `s.symmetric_difference_update(t)` | 计算*s*和*t*的对称差集，并将结果留在*s*中。 |
| `s.update(t)` | 将*t*中的所有项目添加到*s*。*t*可以是另一个集合、序列或任何支持迭代的对象。 |

表3.8 **可变集合类型的方法**

所有这些操作都就地修改集合*s*。参数*t*可以是任何支持迭代的对象。

#### 用于表示程序结构的内置类型

在Python中，函数、类和模块都是可以作为数据操作的对象。表3.9显示了用于表示程序本身各种元素的类型。

| 类型类别 | 类型名称 | 描述 |
|-------------|-----------|-------------|
| 可调用 | `types.BuiltinFunctionType` | 内置函数或方法 |
| | `type` | 内置类型和类的类型 |
| | `object` | 所有类型和类的祖先 |
| | `types.FunctionType` | 用户定义的函数 |
| | `types.MethodType` | 类方法 |
| 模块 | `types.ModuleType` | 模块 |
| 类 | `object` | 所有类型和类的祖先 |
| 类型 | `type` | 内置类型和类的类型 |

表3.9 **程序结构的内置类型**

注意，`object`和`type`在表3.9中出现两次，因为类和类型都可以作为函数调用。

###### 可调用类型

可调用类型表示支持函数调用操作的对象。具有此属性的对象有几种，包括用户定义的函数、内置函数、实例方法和类。

####### 用户定义的函数

*用户定义的函数*是在模块级别使用`def`语句或`lambda`运算符创建的可调用对象。以下是示例：

```
def foo(x,y):
    return x + y

bar = lambda x,y: x + y
```

用户定义的函数`f`具有以下属性：

| 属性 | 描述 |
| --- | --- |
| `f.__doc__` | 文档字符串 |
| `f.__name__` | 函数名称 |
| `f.__dict__` | 包含函数属性的字典 |
| `f.__code__` | 字节编译代码 |
| `f.__defaults__` | 包含默认参数的元组 |
| `f.__globals__` | 定义全局命名空间的字典 |
| `f.__closure__` | 包含与嵌套作用域相关数据的元组 |

在较早的Python 2版本中，前面的许多属性具有诸如`func_code`、`func_defaults`等名称。列出的属性名称与Python 2.6和Python 3兼容。

####### 方法

*方法*是在类定义中定义的函数。有三种常见类型的方法——实例方法、类方法和静态方法：

```
class Foo(object):
    def instance_method(self,arg):
        statements
    @classmethod
    def class_method(cls,arg):
        statements
    @staticmethod
    def static_method(arg):
        statements
```

*实例方法*是操作属于给定类的实例的方法。实例作为第一个参数传递给方法，按照惯例称为`self`。*类方法*将类本身作为对象进行操作。类对象作为第一个参数`cls`传递给类方法。*静态方法*只是恰好封装在类中的一个函数。它不接收实例或类对象作为第一个参数。

实例和类方法都由`types.MethodType`类型的特殊对象表示。但是，理解这种特殊类型需要仔细理解对象属性查找（`.`）的工作原理。在对象上查找内容（`.`）的过程始终与进行函数调用的操作是分开的。当你调用方法时，这两个操作都会发生，但作为不同的步骤。此示例说明了在上一个列表中的`Foo`实例上调用`f.instance_method(arg)`的过程：

```
f = Foo()                # 创建实例
meth = f.instance_method # 查找方法并注意缺少()
meth(37)                 # 现在调用方法
```

在此示例中，meth称为*绑定方法*。绑定方法是一个可调用对象，它包装了一个函数（方法）和一个关联的实例。当你调用绑定方法时，实例作为第一个参数（self）传递给方法。因此，示例中的meth可以被视为一个已准备好进行的方法调用，但尚未使用函数调用运算符（）调用。

方法查找也可以在类本身上发生。例如：

```
umeth = Foo.instance_method  # 在Foo上查找instance_method
umeth(f,37)                   # 调用它，但显式提供self
```

在此示例中，umeth称为*未绑定方法*。未绑定方法是一个可调用对象，它包装方法函数，但期望将正确类型的实例作为第一个参数传递。在示例中，我们传递了`f`，一个Foo的实例，作为第一个参数。如果传递了错误类型的对象，你会得到TypeError。例如：

```
>>> umeth("hello",5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: descriptor 'instance_method' requires a 'Foo' object but received a 'str'
>>>
```

对于用户定义的类，绑定和未绑定方法都表示为`types.MethodType`类型的对象，这只是一个普通函数对象的薄包装器。为方法对象定义了以下属性：

| 属性 | 描述 |
|-----------|-------------|
| `m.__doc__` | 文档字符串 |
| `m.__name__` | 方法名称 |
| `m.__class__` | 定义此方法的类 |
| `m.__func__` | 实现该方法的函数对象 |
| `m.__self__` | 与该方法关联的实例（如果是未绑定的，则为None） |

Python 3的一个微妙特性是，未绑定方法不再由`types.MethodType`对象包装。如果你像前面的示例那样访问`Foo.instance_method`，你只会获得实现该方法的原始函数对象。此外，你会发现`self`参数上不再有任何类型检查。

####### 内置函数和方法

对象类型。`Built-inFunctionType`用于表示在C和C++中实现的函数和方法。内置方法具有以下属性：

| 属性 | 描述 |
|-----------|-------------|
| `b.__doc__` | 文档字符串 |
| `b.__name__` | 函数/方法名称 |
| `b.__self__` | 与该方法关联的实例（如果绑定） |

对于内置函数（如`len()`），`__self__`设置为None，表示该函数未绑定到任何特定对象。对于内置方法（如`x.append`，其中`x`是列表对象），`__self__`设置为`x`。

####### 类和实例作为可调用对象

类对象和实例也可以作为可调用对象来使用。类对象通过 `class` 语句创建，并可以像函数一样被调用以创建新的实例。在这种情况下，函数的参数会被传递给类的 `__init__()` 方法，用于初始化新创建的实例。如果实例定义了特殊方法 `__call__()`，则该实例可以模拟函数的行为。如果为实例 *x* 定义了此方法，那么 `x(args)` 将调用 `x.__call__(args)` 方法。

###### 类、类型和实例

当你定义一个类时，类定义通常会生成一个类型为 `type` 的对象。以下是一个示例：

```
>>> class Foo(object):
...     pass
...
>>> type(Foo)
<type 'type'>
```

下表展示了类型对象 *t* 的常用属性：

| 属性 | 描述 |
|-----------|-------------|
| `t.__doc__` | 文档字符串 |
| `t.__name__` | 类名 |
| `t.__bases__` | 基类元组 |
| `t.__dict__` | 保存类方法和变量的字典 |
| `t.__module__` | 定义该类的模块名 |
| `t.__abstractmethods__` | 抽象方法名的集合（如果没有任何抽象方法，则可能未定义） |

当创建一个对象实例时，该实例的类型就是定义它的类。以下是一个示例：

```
>>> f = Foo()
>>> type(f)
<class '__main__.Foo'>
```

下表展示了实例 *i* 的特殊属性：

| 属性 | 描述 |
|-----------|-------------|
| `i.__class__` | 实例所属的类 |
| `i.__dict__` | 保存实例数据的字典 |

`__dict__` 属性通常用于存储与实例相关的所有数据。当你进行 `i.attr = value` 这样的赋值操作时，值就存储在这里。但是，如果用户定义的类使用了 `__slots__`，则会采用更高效的内部表示方式，实例将不再拥有 `__dict__` 属性。关于对象和 Python 对象系统组织结构的更多细节，请参见第 7 章。

###### 模块

*模块*类型是一个容器，用于保存通过 `import` 语句加载的对象。例如，当程序中出现 `import foo` 语句时，名称 `foo` 会被赋值给相应的模块对象。模块定义了一个命名空间，通过 `__dict__` 属性中可访问的字典来实现。每当引用模块的一个属性（使用点运算符）时，它会被转换为字典查找。例如，`m.x` 等同于 `m.__dict__["x"]`。同样，对属性的赋值如 `m.x = y` 等同于 `m.__dict__["x"] = y`。以下属性可用：

| 属性 | 描述 |
| --- | --- |
| `m.__dict__` | 与模块关联的字典 |
| `m.__doc__` | 模块文档字符串 |
| `m.__name__` | 模块名称 |
| `m.__file__` | 加载该模块的文件 |
| `m.__path__` | 完全限定的包名，仅在模块对象引用包时定义 |

###### 解释器内部使用的内置类型

解释器内部使用的许多对象会暴露给用户。这些对象包括回溯对象、代码对象、帧对象、生成器对象、切片对象和 `Ellipsis`，如表 3.10 所示。程序直接操作这些对象的情况相对较少，但它们对于工具构建者和框架设计者来说可能具有实际用途。

**表 3.10 解释器内部使用的内置 Python 类型**

| 类型名称 | 描述 |
| --- | --- |
| `types.CodeType` | 字节编译的代码 |
| `types.FrameType` | 执行帧 |
| `types.GeneratorType` | 生成器对象 |
| `types.TracebackType` | 异常的栈回溯 |
| `slice` | 由扩展切片生成 |
| `Ellipsis` | 用于扩展切片中 |

####### 代码对象

代码对象表示原始的字节编译可执行代码，即*字节码*，通常由内置的 `compile()` 函数返回。代码对象与函数类似，但不包含与定义代码的命名空间相关的任何上下文，也不存储默认参数值的信息。代码对象 `c` 具有以下只读属性：

| 属性 | 描述 |
| --- | --- |
| `c.co_name` | 函数名。 |
| `c.co_argcount` | 位置参数的数量（包括默认值）。 |
| `c.co_nlocals` | 函数使用的局部变量数量。 |
| `c.co_varnames` | 包含局部变量名的元组。 |
| `c.co_cellvars` | 包含嵌套函数引用的变量名的元组。 |
| `c.co_freevars` | 包含嵌套函数使用的自由变量名的元组。 |
| `c.co_code` | 表示原始字节码的字符串。 |
| `c.co_consts` | 包含字节码使用的字面量的元组。 |
| `c.co_names` | 包含字节码使用的名称的元组。 |
| `c.co_filename` | 编译该代码的文件名。 |
| `c.co_firstlineno` | 函数的第一行行号。 |
| `c.co_lnotab` | 将字节码偏移量编码为行号的字符串。 |
| `c.co_stacksize` | 所需的栈大小（包括局部变量）。 |
| `c.co_flags` | 包含解释器标志的整数。如果函数使用 `*args` 来接收可变数量的位置参数，则第 2 位被设置。如果函数允许使用 `**kwargs` 接收任意关键字参数，则第 3 位被设置。所有其他位保留。 |

####### 帧对象

帧对象用于表示执行帧，最常出现在回溯对象中（下文介绍）。帧对象 `f` 具有以下只读属性：

| 属性 | 描述 |
|-----------|-------------|
| `f.f_back` | 前一个栈帧（朝向调用者方向）。 |
| `f.f_code` | 正在执行的代码对象。 |
| `f.f_locals` | 用于局部变量的字典。 |
| `f.f_globals` | 用于全局变量的字典。 |
| `f.f_builtins` | 用于内置名称的字典。 |
| `f.f_lineno` | 行号。 |
| `f.f_lasti` | 当前指令。这是 `f_code` 字节码字符串中的一个索引。 |

以下属性可以被修改（被调试器和其他工具使用）：

| 属性 | 描述 |
|-----------|-------------|
| `f.f_trace` | 在每行源代码开始时调用的函数 |
| `f.f_exc_type` | 最近的异常类型（仅限 Python 2） |
| `f.f_exc_value` | 最近的异常值（仅限 Python 2） |
| `f.f_exc_traceback` | 最近的异常回溯（仅限 Python 2） |

####### 回溯对象

回溯对象在异常发生时创建，包含栈跟踪信息。当进入异常处理程序时，可以使用 `sys.exc_info()` 函数获取栈跟踪。回溯对象具有以下只读属性：

| 属性 | 描述 |
| --- | --- |
| `t.tb_next` | 栈跟踪的下一层级（朝向异常发生的执行帧方向） |
| `t.tb_frame` | 当前层级的执行帧对象 |
| `t.tb_lineno` | 异常发生的行号 |
| `t.tb_lasti` | 当前层级正在执行的指令 |

####### 生成器对象

生成器对象在调用生成器函数时创建（参见第 6 章"函数与函数式编程"）。每当函数使用特殊的 yield 关键字时，就定义了一个生成器函数。生成器对象既是迭代器，又是关于生成器函数自身信息的容器。以下属性和方法可用：

| 属性 | 描述 |
| --- | --- |
| `g.gi_code` | 生成器函数的代码对象。 |
| `g.gi_frame` | 生成器函数的执行帧。 |
| `g.gi_running` | 指示生成器函数当前是否正在运行的整数。 |
| `g.next()` | 执行函数直到下一个 yield 语句并返回值（此方法在 Python 3 中称为 `__next__`）。 |
| `g.send(value)` | 向生成器发送一个值。传递的值由生成器中的 yield 表达式返回，生成器执行直到遇到下一个 yield 表达式。send() 返回此表达式中传递给 yield 的值。 |
| `g.close()` | 通过在生成器函数中引发 `GeneratorExit` 异常来关闭生成器。当生成器对象被垃圾回收时，此方法会自动执行。 |
| `g.throw(exc [,exc_value [,exc_tb ]])` | 在生成器中当前 yield 语句的位置引发异常。exc 是异常类型，exc_value 是异常值，exc_tb 是可选的回溯信息。如果产生的异常被捕获和处理，则返回传递给下一个 yield 语句的值。 |

####### 切片对象

切片对象用于表示扩展切片语法中给出的切片，例如 `a[i:j:stride]`、`a[i:j, n:m]` 或 `a[..., i:j]`。切片对象也可以使用内置函数 `slice([i,] j [,stride])` 创建。以下只读属性可用：

| 属性 | 描述 |
| --- | --- |
| `s.start` | 切片的起始索引。 |
| `s.stop` | 切片的结束索引。 |
| `s.step` | 切片的步长值。 |



####### 切片对象

| 属性 | 描述 |
| --- | --- |
| `s.start` | 切片的下界；若省略则为 `None` |
| `s.stop` | 切片的上界；若省略则为 `None` |
| `s.step` | 切片的步长；若省略则为 `None` |

切片对象还提供了一个方法 `s.indices(length)`。该方法接受一个长度参数，并返回一个元组 `(start, stop, stride)`，表示该切片将如何应用到指定长度的序列上。示例如下：

```
s = slice(10,20)   # Slice object represents [10:20]
s.indices(100)     # Returns (10,20,1) -> [10:20]
s.indices(15)      # Returns (10,15,1) -> [10:15]
```

####### 省略号对象

`Ellipsis` 对象用于在索引查找 `[]` 中表示省略号（`...`）的存在。该类型只有一个实例，通过内置名称 `Ellipsis` 访问。它没有属性，求值为 `True`。Python 的内置类型均未使用 `Ellipsis`，但如果你想为自定义对象的索引运算符 `[]` 构建高级功能，它可能会很有用。以下代码展示了 `Ellipsis` 是如何被创建并传入索引运算符的：

```
class Example(object):
    def __getitem__(self,index):
        print(index)
e = Example()
e[3, ..., 4]      # Calls e.__getitem__((3, Ellipsis, 4))
```

##### 对象行为与特殊方法

Python 中的对象通常根据其行为和实现的特性进行分类。例如，所有序列类型（如字符串、列表和元组）被归为一组，仅仅是因为它们都支持一组共同的序列操作，如 `s[n]`、`len(s)` 等。所有基本的解释器操作都是通过特殊对象方法实现的。特殊方法的名称总是以双下划线（`__`）开头和结尾。这些方法在程序执行过程中由解释器自动触发。例如，操作 `x + y` 被映射为内部方法 `x.__add__(y)`，索引操作 `x[k]` 被映射为 `x.__getitem__(k)`。每种数据类型的行为完全取决于它所实现的特殊方法集合。

用户定义的类可以通过提供本节中描述的特殊方法的适当子集，来创建行为类似于内置类型的新对象。此外，内置类型（如列表和字典）可以通过重新定义部分特殊方法来进行特化（通过继承）。

接下来的几节将描述与解释器不同功能类别相关的特殊方法。

###### 对象创建与销毁

表 3.11 中的方法用于创建、初始化和销毁实例。`__new__()` 是一个类方法，用于创建实例。`__init__()` 方法用于初始化对象的属性，在对象新创建后立即调用。`__del__()` 方法在对象即将被销毁时调用。该方法仅在对象不再被使用时才会被调用。需要注意的是，语句 `del x` 只会减少对象的引用计数，并不一定会导致调用此函数。关于这些方法的更多细节可以在第 7 章中找到。

| 方法 | 描述 |
|--------|-------------|
| `__new__(cls [, *args [, **kwargs]])` | 被调用以创建新实例的类方法 |
| `__init__(self [, *args [, **kwargs]])` | 被调用以初始化新实例 |
| `__del__(self)` | 在实例被销毁时调用 |

`__new__()` 和 `__init__()` 方法协同工作以创建和初始化新实例。当通过调用 `A(args)` 创建对象时，它会被转换为以下步骤：

```
x = A.__new__(A,args)
if isinstance(x,A): x.__init__(args)
```

在用户定义的对象中，很少会定义 `__new__()` 或 `__del__()`。`__new__()` 通常只在元类或恰好继承自某种不可变类型（整数、字符串、元组等）的用户定义对象中定义。`__del__()` 仅在存在某种关键资源管理问题时才会定义，例如释放锁或关闭连接。

###### 对象字符串表示

表 3.12 中的方法用于创建对象的各种字符串表示形式。

| 方法 | 描述 |
|--------|-------------|
| `__format__(self, format_spec)` | 创建格式化的表示形式 |
| `__repr__(self)` | 创建对象的字符串表示形式 |
| `__str__(self)` | 创建简单的字符串表示形式 |

`__repr__()` 和 `__str__()` 方法用于创建对象的简单字符串表示形式。`__repr__()` 方法通常返回一个可以被求值以重新创建对象的表达式字符串。它也是在交互式解释器中检查变量时输出内容所使用的方法。该方法由内置的 `repr()` 函数调用。以下是 `repr()` 和 `eval()` 配合使用的示例：

```
a = [2,3,4,5]    # Create a list
s = repr(a)      # s = '[2, 3, 4, 5]'
b = eval(s)      # Turns s back into a list
```

如果无法创建字符串表达式，按照惯例 `__repr__()` 会返回形如 `<...message...>` 的字符串，如下所示：

```
f = open("foo")
a = repr(f)         # a = "<open file 'foo', mode 'r' at dc030>"
```

`__str__()` 方法由内置的 `str()` 函数和与打印相关的函数调用。它与 `__repr__()` 的区别在于，其返回的字符串可以更简洁且对用户更友好。如果该方法未定义，则会调用 `__repr__()` 方法。

`__format__()` 方法由 `format()` 函数或字符串的 `format()` 方法调用。*format_spec* 参数是包含格式规范的字符串。该字符串与 `format()` 的 `format_spec` 参数相同。示例如下：

```
format(x,"spec")          # Calls x.__format__("spec")
"x is {0:spec}".format(x) # Calls x.__format__("spec")
```

格式规范的语法是任意的，可以针对每个对象进行自定义。不过，标准语法在第 4 章中有描述。

###### 对象比较与排序

表 3.13 展示了可用于对对象执行简单测试的方法。`__bool__()` 方法用于真值测试，应返回 `True` 或 `False`。如果未定义，则 `__len__()` 方法作为后备方案被调用来确定真值。`__hash__()` 方法在希望作为字典键使用的对象上定义。返回的值是一个整数，对于两个比较相等的对象，该整数应该相同。此外，可变对象不应定义此方法；对对象的任何更改都会改变哈希值，使其在后续的字典查找中无法定位到该对象。

| 方法 | 描述 |
| --- | --- |
| `__bool__(self)` | 用于真值测试，返回 `False` 或 `True` |
| `__hash__(self)` | 计算整数哈希索引 |

对象可以实现一个或多个关系运算符（`<`、`>`、`<=`、`>=`、`==`、`!=`）。这些方法中的每一个都接受两个参数，并可以返回任何类型的对象，包括布尔值、列表或任何其他 Python 类型。例如，数值计算包可能会使用此机制对两个矩阵进行逐元素比较，并返回一个包含结果的矩阵。如果无法进行比较，这些函数也可能引发异常。表 3.14 展示了比较运算符的特殊方法。

| 方法 | 结果 |
| --- | --- |
| `__lt__(self,other)` | `self < other` |
| `__le__(self,other)` | `self <= other` |
| `__gt__(self,other)` | `self > other` |
| `__ge__(self,other)` | `self >= other` |
| `__eq__(self,other)` | `self == other` |
| `__ne__(self,other)` | `self != other` |

对象并不需要实现表 3.14 中的所有操作。但是，如果你想能够使用 `==` 比较对象或将对象用作字典键，则应定义 `__eq__()` 方法。如果你想能够对对象进行排序或使用 `min()` 或 `max()` 等函数，则至少需要定义 `__lt__()`。

###### 类型检查

表 3.15 中的方法可用于重新定义类型检查函数 `isinstance()` 和 `issubclass()` 的行为。这些方法最常见的应用场景是在定义抽象基类和接口时，如第 7 章所述。

| 方法 | 结果 |
| --- | --- |
| `__instancecheck__(cls, object)` | `isinstance(object, cls)` |
| `__subclasscheck__(cls, sub)` | `issubclass(sub, cls)` |

###### 属性访问

表 3.16 中的方法分别使用点号（.）运算符和 `del` 运算符来读取、写入和删除对象的属性。

| 方法 | 描述 |
| --- | --- |
| `__getattribute__(self, name)` | 返回属性 `self.name`。 |
| `__getattr__(self, name)` | 如果通过常规属性查找未找到，则返回属性 `self.name` 或引发 `AttributeError`。 |
| `__setattr__(self, name, value)` | 设置属性 `self.name = value`。覆盖默认机制。 |
| `__delattr__(self, name)` | 删除属性 `self.name`。 |

每当访问属性时，`__getattribute__()` 方法总是会被调用。如果找到该属性，则返回它。否则，`__getattr__()` 方法会被调用。`__getattr__()` 的默认行为是引发 `AttributeError` 异常。设置属性时总是会调用 `__setattr__()` 方法，删除属性时总是会调用 `__delattr__()` 方法。



###### 属性包装与描述符

属性操作的一个微妙之处在于，有时对象的属性会被包装一层额外的逻辑，这些逻辑与上一节描述的 `get`、`set` 和 `delete` 操作相互作用。这种包装是通过创建一个*描述符*对象来实现的，该对象实现了表 3.17 中的一个或多个方法。请记住，描述符是可选的，很少需要定义。

| 方法 | 描述 |
| --- | --- |
| `__get__(self, instance, cls)` | 返回一个属性值，或引发 AttributeError |
| `__set__(self, instance, value)` | 将属性设置为 value |
| `__delete__(self, instance)` | 删除该属性 |

描述符的 `__get__()`、`__set__()` 和 `__delete__()` 方法旨在与类和类型上的 `__getattribute__()`、`__setattr__()` 和 `__delattr__()` 方法的默认实现进行交互。如果你在用户定义的类的主体中放置一个描述符对象的实例，就会发生这种交互。在这种情况下，对描述符属性的所有访问都将隐式地调用描述符对象本身上的相应方法。通常，描述符用于实现对象系统的底层功能，包括绑定和未绑定方法、类方法、静态方法和属性。更多示例见第 7 章。

###### 序列和映射方法

表 3.18 中的方法用于希望模拟序列和映射对象的对象。

| 方法 | 描述 |
| --- | --- |
| `__len__(self)` | 返回 *self* 的长度 |
| `__getitem__(self, key)` | 返回 *self*[key] |
| `__setitem__(self, key, value)` | 设置 *self*[key] = value |
| `__delitem__(self, key)` | 删除 *self*[key] |
| `__contains__(self, obj)` | 如果 *obj* 在 *self* 中则返回 True；否则返回 False |

这是一个示例：

```
a = [1,2,3,4,5,6]
len(a)      # a.__len__()
x = a[2]    # x = a.__getitem__(2)
a[1] = 7    # a.__setitem__(1,7)
del a[2]    # a.__delitem__(2)
5 in a      # a.__contains__(5)
```

内置的 `len()` 函数会调用 `__len__` 方法来返回一个非负长度。除非也定义了 `__bool__()` 方法，否则该函数也会确定真值。

要操作单个项，`__getitem__()` 方法可以通过键值返回一个项。键可以是任何 Python 对象，但通常是序列的整数。`__setitem__()` 方法为元素赋值。`__delitem__()` 方法在 `del` 操作应用于单个元素时被调用。`__contains__()` 方法用于实现 `in` 运算符。

切片操作（如 `x = s[i:j]`）也是通过 `__getitem__()`、`__setitem__()` 和 `__delitem__()` 实现的。然而，对于切片，会传递一个特殊的 `slice` 对象作为键。该对象具有描述所请求切片范围的属性。例如：

```
a = [1,2,3,4,5,6]
x = a[1:5]       # x = a.__getitem__(slice(1,5,None))
a[1:3] = [10,11,12]  # a.__setitem__(slice(1,3,None), [10,11,12])
del a[1:4]       # a.__delitem__(slice(1,4,None))
```

Python 的切片功能实际上比许多程序员意识到的要强大。例如，以下扩展切片的各种变体都得到支持，并且可能对处理多维数据结构（如矩阵和数组）有用：

```
a = m[0:100:10]         # 步幅切片 (stride=10)
b = m[1:10, 3:20]       # 多维切片
c = m[0:100:10, 50:75:5] # 带步幅的多维切片
m[0:5, 5:10] = n        # 扩展切片赋值
del m[:10, 15:]         # 扩展切片删除
```

扩展切片每个维度的通用格式是 `i:j[:stride]`，其中 `stride` 是可选的。与普通切片一样，你可以省略切片每个部分的起始值或结束值。此外，省略号（写作 `...`）可用于表示扩展切片中任意数量的尾随或前导维度：

```
a = m[..., 10:20]   # 带 Ellipsis 的扩展切片访问
m[10:20, ...] = n
```

使用扩展切片时，`__getitem__()`、`__setitem__()` 和 `__delitem__()` 方法分别实现访问、修改和删除。然而，传递给这些方法的值不是整数，而是一个包含 `slice` 或 `Ellipsis` 对象组合的元组。例如，

```
a = m[0:10, 0:100:5, ...]
```

会按如下方式调用 `__getitem__()`：

```
a = m.__getitem__((slice(0,10,None), slice(0,100,5), Ellipsis))
```

Python 字符串、元组和列表目前提供了一些对扩展切片的支持，这将在第 4 章中描述。Python 的特殊用途扩展，尤其是那些具有科学色彩的扩展，可能会提供具有高级扩展切片操作支持的新类型和对象。

###### 迭代

如果一个对象 `obj` 支持迭代，它必须提供一个方法 `obj.__iter__()`，该方法返回一个迭代器对象。迭代器对象 `iter` 又必须实现一个方法 `iter.next()`（在 Python 3 中是 `iter.__next__()`），该方法返回下一个对象或引发 `StopIteration` 以表示迭代结束。`for` 语句的实现以及其他隐式执行迭代的操作都会使用这两个方法。例如，语句 `for x in s` 是通过执行相当于以下步骤的操作来实现的：

```
_iter = s.__iter__()
while 1:
    try:
        x = _iter.next()  # 在 Python 3 中是 _iter.__next__()
    except StopIteration:
        break
    # 执行 for 循环体中的语句
    ...
```

###### 数学运算

表 3.19 列出了对象必须实现以模拟数字的特殊方法。数学运算总是根据第 4 章描述的优先级规则从左到右求值；当出现像 `x + y` 这样的表达式时，解释器会尝试调用方法 `x.__add__(y)`。以 `r` 开头的特殊方法支持操作数反转的运算。仅当左操作数未实现指定操作时才调用这些方法。例如，如果 `x + y` 中的 `x` 不支持 `__add__()` 方法，解释器会尝试调用方法 `y.__radd__(x)`。

| 方法 | 结果 |
| --- | --- |
| `__add__(self, other)` | `self + other` |
| `__sub__(self, other)` | `self - other` |
| `__mul__(self, other)` | `self * other` |
| `__div__(self, other)` | `self / other` (仅限 Python 2) |
| `__truediv__(self, other)` | `self / other` (Python 3) |
| `__floordiv__(self, other)` | `self // other` |
| `__mod__(self, other)` | `self % other` |
| `__divmod__(self, other)` | `divmod(self, other)` |
| `__pow__(self, other [,modulo])` | `self ** other`, `pow(self, other, modulo)` |
| `__lshift__(self, other)` | `self << other` |
| `__rshift__(self, other)` | `self >> other` |
| `__and__(self, other)` | `self & other` |
| `__or__(self, other)` | `self | other` |
| `__xor__(self, other)` | `self ^ other` |
| `__radd__(self, other)` | `other + self` |
| `__rsub__(self, other)` | `other - self` |
| `__rmul__(self, other)` | `other * self` |
| `__rdiv__(self, other)` | `other / self` (仅限 Python 2) |
| `__rtruediv__(self, other)` | `other / self` (Python 3) |
| `__rfloordiv__(self, other)` | `other // self` |
| `__rmod__(self, other)` | `other % self` |
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
| `__idiv__(self, other)` | `self /= other` (仅限 Python 2) |
| `__itruediv__(self, other)` | `self /= other` (Python 3) |
| `__ifloordiv__(self, other)` | `self //= other` |
| `__imod__(self, other)` | `self %= other` |
| `__ipow__(self, other)` | `self **= other` |
| `__iand__(self, other)` | `self &= other` |
| `__ior__(self, other)` | `self \|= other` |
| `__ixor__(self, other)` | `self ^= other` |
| `__ilshift__(self, other)` | `self <<= other` |
| `__irshift__(self, other)` | `self >>= other` |
| `__neg__(self)` | `-self` |
| `__pos__(self)` | `+self` |
| `__abs__(self)` | `abs(self)` |
| `__invert__(self)` | `~self` |
| `__int__(self)` | `int(self)` |
| `__long__(self)` | `long(self)` (仅限 Python 2) |
| `__float__(self)` | `float(self)` |
| `__complex__(self)` | `complex(self)` |

方法 `__iadd__()`、`__isub__()` 等用于支持原地算术运算符，如 `a+=b` 和 `a-=b`（也称为*增强赋值*）。这些运算符与标准算术方法之间的区别在于，原地运算符的实现可能能够提供某些自定义，例如性能优化。例如，如果 `self` 参数未被共享，则可以在不分配新创建对象作为结果的情况下就地修改对象的值。

三种除法运算符——`__div__()`、`__truediv__()` 和 `__floordiv__()`——用于实现真除法 (`/`) 和截断除法 (`//`) 操作。存在三种操作的原因与整数除法语义的变化有关，该变化始于 Python 2.2，但在 Python 3 中成为默认行为。在 Python 2 中，Python 的默认行为是将 `/` 运算符映射到 `__div__()`。对于整数，此操作将结果截断为整数。在 Python 3 中，除法映射到 `__truediv__()`，对于整数，则返回浮点数。后一种

通过在程序中包含语句 `from __future__ import division`，可以在 Python 2 中将此行为作为可选功能启用。

转换方法 `__int__()`、`__long__()`、`__float__()` 和 `__complex__()` 可以将对象转换为四种内置数值类型之一。这些方法通过显式类型转换（如 `int()` 和 `float()`）来调用。然而，这些方法并不用于数学运算中的隐式类型强制转换。例如，表达式 `3 + x` 即使 `x` 是一个定义了用于整数转换的 `__int__()` 的用户自定义对象，也会产生 `TypeError`。

###### 可调用接口

对象可以通过提供 `__call__(self [, *args [, **kwargs]])` 方法来模拟函数。如果一个对象 `x` 提供了此方法，就可以像调用函数一样调用它。也就是说，`x(arg1, arg2, ...)` 会调用 `x.__call__(self, arg1, arg2, ...)`。能够模拟函数的对象对于创建仿函数（functor）或代理（proxy）很有用。下面是一个简单的例子：

```
class DistanceFrom(object):
    def __init__(self, origin):
        self.origin = origin
    def __call__(self, x):
        return abs(x - self.origin)

nums = [1, 37, 42, 101, 13, 9, -20]
nums.sort(key=DistanceFrom(10))    # 按到10的距离排序
```

在这个例子中，`DistanceFrom` 类创建的实例模拟了一个单参数函数。这些实例可以代替普通函数使用——例如，在示例中对 `sort()` 的调用中。

###### 上下文管理协议

`with` 语句允许一系列语句在另一个称为*上下文管理器*的对象的控制下执行。其一般语法如下：

```
with context [ as var]:
    statements
```

此处显示的 *context* 对象预期需要实现表 3.20 所示的方法。`__enter__()` 方法在 `with` 语句执行时被调用。该方法的返回值被放入通过可选的 `as var` 指定符指定的变量中。一旦控制流离开与 `with` 语句关联的语句块，就会调用 `__exit__()` 方法。作为参数，如果引发了异常，`__exit__()` 会接收当前的异常类型、值和回溯信息。如果没有错误被处理，所有三个值都将设置为 `None`。

**表 3.20 上下文管理器的特殊方法**

| 方法 | 描述 |
| --- | --- |
| `__enter__(self)` | 在进入新上下文时调用。返回值被放入 `with` 语句中 `as` 指定符列出的变量中。 |
| `__exit__(self, type, value, tb)` | 在离开上下文时调用。如果发生了异常，*type*、*value* 和 *tb* 分别包含异常类型、值和回溯信息。上下文管理接口的主要用途是允许对涉及系统状态（如打开的文件、网络连接和锁）的对象进行简化的资源控制。通过实现此接口，当执行离开对象所在的上下文时，对象可以安全地清理资源。更多细节请参见第 5 章“程序结构与控制流”。 |

###### 对象检查与 `dir()`

`dir()` 函数通常用于检查对象。对象可以通过实现 `__dir__(self)` 来提供 `dir()` 返回的名称列表。定义此方法可以更容易地隐藏你不想让用户直接访问的对象内部细节。但是，请记住，用户仍然可以检查实例和类的底层 `__dict__` 属性以查看所有已定义的内容。

### 4 运算符与表达式

本章描述 Python 的内置运算符、表达式和求值规则。尽管本章大部分内容描述了 Python 的内置类型，但用户自定义的对象可以轻松地重新定义任何运算符以提供自己的行为。

#### 数字运算

以下运算可应用于所有数值类型：

| 运算 | 描述 |
|-----------|-------------|
| `x + y` | 加法 |
| `x - y` | 减法 |
| `x * y` | 乘法 |
| `x / y` | 除法 |
| `x // y` | 截断除法 |
| `x ** y` | 幂 ($x^y$) |
| `x % y` | 取模 (`x mod y`) |
| `-x` | 一元负号 |
| `+x` | 一元正号 |

截断除法运算符（`//`，也称为*地板除*）将结果截断为整数，并且适用于整数和浮点数。在 Python 2 中，如果操作数是整数，真除法运算符（`/`）也会将结果截断为整数。因此，`7/4` 的结果是 `1`，而不是 `1.75`。然而，这种行为在 Python 3 中发生了变化，其中除法产生浮点结果。取模运算符返回除法 `x // y` 的余数。例如，`7 % 4` 的结果是 `3`。对于浮点数，取模运算符返回 `x // y` 的浮点余数，即 `x - (x // y) * y`。对于复数，取模（`%`）和截断除法（`//`）运算符是无效的。

以下移位和按位逻辑运算符只能应用于整数：

| 运算 | 描述 |
|-----------|-------------|
| `x << y` | 左移 |
| `x >> y` | 右移 |
| `x & y` | 按位与 |
| `x \| y` | 按位或 |
| `x ^ y` | 按位异或 |
| `~x` | 按位取反 |

按位运算符假定整数采用二进制补码表示，并且符号位向左无限延伸。如果你正在处理打算映射到硬件原生整数的原始位模式，则需要特别小心。这是因为 Python 不会截断位或允许值溢出——相反，结果的大小将任意增长。

此外，你可以将以下内置函数应用于所有数值类型：

| 函数 | 描述 |
|----------|-------------|
| `abs(x)` | 绝对值 |
| `divmod(x,y)` | 返回 `(x // y, x % y)` |
| `pow(x,y [,modulo])` | 返回 `(x ** y) % modulo` |
| `round(x, [n])` | 四舍五入到最接近的 $10^{-n}$ 的倍数（仅适用于浮点数） |

`abs()` 函数返回一个数的绝对值。`divmod()` 函数返回除法运算的商和余数，并且仅对非复数有效。`pow()` 函数可以代替 `**` 运算符使用，但也支持三元幂模函数（常用于加密算法）。`round()` 函数将浮点数 `x` 四舍五入到最接近的 10 的负 *n* 次幂的倍数。如果省略 *n*，则设为 `0`。如果 *x* 与两个倍数的距离相等，Python 2 会舍入到离零较远的倍数（例如，`0.5` 舍入为 `1.0`，`-0.5` 舍入为 `-1.0`）。这里需要注意的是，Python 3 会将同样接近的值舍入到最近的偶数倍数（例如，0.5 舍入为 0.0，1.5 舍入为 2.0）。对于正在移植到 Python 3 的数学程序来说，这是一个细微的可移植性问题。

以下比较运算符具有标准的数学解释，并返回布尔值 `True`（真）和 `False`（假）：

| 运算 | 描述 |
|-----------|-------------|
| `x < y` | 小于 |
| `x > y` | 大于 |
| `x == y` | 等于 |
| `x != y` | 不等于 |
| `x >= y` | 大于或等于 |
| `x <= y` | 小于或等于 |

比较可以链式进行，例如 `w < x < y < z`。此类表达式被求值为 `w < x` 且 `x < y` 且 `y < z`。像 `x < y > z` 这样的表达式是合法的，但可能会让任何阅读代码的人感到困惑（重要的是要注意，在这样的表达式中，`x` 和 `z` 之间没有进行比较）。涉及复数的比较是未定义的，并会导致 `TypeError`。

只有当操作数类型相同时，涉及数字的运算才有效。对于内置数字，会执行强制转换操作将其中一个类型转换为另一个类型，如下所示：

1.  如果任一操作数是复数，则另一个操作数将被转换为复数。



#### 序列操作

以下操作符可应用于序列类型，包括字符串、列表和元组：

| 操作 | 描述 |
| --- | --- |
| `s + r` | 连接 |
| `s * n`, `n * s` | 创建 `s` 的 `n` 个副本，其中 `n` 是整数 |
| `v1, v2, ..., vn = s` | 变量解包 |
| `s[i]` | 索引 |
| `s[i:j]` | 切片 |
| `s[i:j:stride]` | 扩展切片 |
| `x in s`, `x not in s` | 成员测试 |
| `for x in s:` | 迭代 |
| `all(s)` | 如果 `s` 中的所有元素都为真，则返回 `True`。 |
| `any(s)` | 如果 `s` 中的任何元素为真，则返回 `True`。 |
| `len(s)` | 长度 |
| `min(s)` | `s` 中的最小元素 |
| `max(s)` | `s` 中的最大元素 |
| `sum(s [, initial])` | 元素之和，可选提供初始值 |

`+` 运算符连接两个相同类型的序列。`s * n` 运算符创建序列的 n 个副本。然而，这些是浅拷贝，仅通过引用复制元素。例如，考虑以下代码：

```
>>> a = [3,4,5]
>>> b = [a]
>>> c = 4*b
>>> c
[[3, 4, 5], [3, 4, 5], [3, 4, 5], [3, 4, 5]]
>>> a[0] = -7
>>> c
[[-7, 4, 5], [-7, 4, 5], [-7, 4, 5], [-7, 4, 5]]
>>>
```

注意对 `a` 的修改如何改变了列表 `c` 中的每个元素。在这种情况下，列表 `a` 的一个引用被放入列表 `b` 中。当 `b` 被复制时，创建了四个对 `a` 的额外引用。最后，当 `a` 被修改时，此更改被传播到 `a` 的所有其他“副本”。序列乘法的这种行为通常出乎意料，并非程序员的本意。解决此问题的一种方法是通过复制 `a` 的内容来手动构造复制的序列。这里有一个例子：

```
a = [ 3, 4, 5 ]
c = [list(a) for j in range(4)]  # list() 制作列表的副本
```

标准库中的 `copy` 模块也可用于创建对象的副本。

所有序列都可以解包到一个变量名序列中。例如：

```
items = [ 3, 4, 5 ]
x,y,z = items      # x = 3, y = 4, z = 5

letters = "abc"
x,y,z = letters    # x = 'a', y = 'b', z = 'c'

datetime = ((5, 19, 2008), (10, 30, "am"))
(month,day,year),(hour,minute,am_pm) = datetime
```

将值解包到变量中时，变量的数量必须与序列中的元素数量完全匹配。此外，变量的结构必须与序列的结构匹配。例如，示例的最后一行将值解包到六个变量中，组织成两个 3 元组，这与右侧序列的结构一致。将序列解包到变量适用于任何类型的序列，包括由迭代器和生成器创建的序列。

索引运算符 `s[n]` 返回序列中第 `n` 个对象，其中 `s[0]` 是第一个对象。可以使用负索引从序列末尾获取元素。例如，`s[-1]` 返回最后一个元素。否则，尝试访问超出范围的元素会导致 `IndexError` 异常。

切片运算符 `s[i:j]` 从 `s` 中提取一个子序列，包含索引为 `k` 的元素，其中 `i <= k < j`。`i` 和 `j` 都必须是整数或长整数。如果省略起始或结束索引，则分别假设为序列的开始或结尾。允许负索引，并假定其相对于序列的末尾。如果 `i` 或 `j` 超出范围，则根据它们的值是指向第一个元素之前还是最后一个元素之后，分别假定它们指向序列的开始或结尾。

切片运算符可以提供一个可选的步长 `s[i:j:stride]`，这会导致切片跳过元素。然而，其行为更为微妙。如果提供了步长，`i` 是起始索引；`j` 是结束索引；生成的子序列是元素 `s[i], s[i+stride], s[i+2*stride]`，依此类推，直到达到索引 `j`（不包含 `j`）。步长也可以是负数。如果省略起始索引 `i`，如果 `stride` 为正，则设置为序列的开始，如果 `stride` 为负，则设置为序列的末尾。如果省略结束索引 `j`，如果 `stride` 为正，则设置为序列的末尾，如果 `stride` 为负，则设置为序列的开始。以下是一些示例：

```
a = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

b = a[::2]       # b = [0, 2, 4, 6, 8 ]
c = a[::-2]      # c = [9, 7, 5, 3, 1]
d = a[0:5:2]     # d = [0,2]
e = a[5:0:-2]    # e = [5,3,1]
f = a[:5:1]      # f = [0,1,2,3,4]
g = a[:5:-1]     # g = [9,8,7,6]
h = a[5::1]      # h = [5,6,7,8,9]
i = a[5::-1]     # i = [5,4,3,2,1,0]
j = a[5:0:-1]    # j = [5,4,3,2,1]
```

`x in s` 运算符测试对象 *x* 是否在序列 *s* 中，并返回 `True` 或 `False`。类似地，`x not in s` 运算符测试 *x* 是否不在序列 *s* 中。对于字符串，`in` 和 `not in` 运算符接受子字符串。例如，`'hello' in 'hello world'` 的结果为 `True`。重要的是要注意 `in` 运算符不支持通配符或任何形式的模式匹配。为此，您需要使用库模块，例如用于正则表达式模式的 `re` 模块。

`for x in s` 运算符遍历序列的所有元素，将在第 5 章“程序结构和控制流”中进一步描述。`len(s)` 返回序列中的元素数量。`min(s)` 和 `max(s)` 分别返回序列的最小值和最大值，尽管结果只有在元素可以相对于 `<` 运算符排序时才有意义（例如，找出文件对象列表的最大值就没有多大意义）。`sum(s)` 对 *s* 中的所有项求和，但通常仅在项表示数字时有效。可以为 `sum()` 提供一个可选的初始值。此值的类型通常决定结果。例如，如果使用 `sum(items, decimal.Decimal(0))`，结果将是一个 Decimal 对象（有关 `decimal` 模块的更多信息，请参见第 14 章“数学”）。

字符串和元组是不可变的，创建后不能修改。列表可以使用以下运算符进行修改：

| 操作 | 描述 |
|-----------|-------------|
| `s[i] = x` | 索引赋值 |
| `s[i:j] = r` | 切片赋值 |
| `s[i:j:stride] = r` | 扩展切片赋值 |
| `del s[i]` | 删除一个元素 |
| `del s[i:j]` | 删除一个切片 |
| `del s[i:j:stride]` | 删除一个扩展切片 |

`s[i] = x` 运算符将列表的第 *i* 个元素更改为引用对象 *x*，增加 *x* 的引用计数。负索引相对于列表的末尾，尝试对超出范围的索引赋值会导致 `IndexError` 异常。切片赋值运算符 `s[i:j] = r` 用序列 *r* 中的元素替换索引为 `i <= k < j` 的元素 *k*。索引可以具有与切片相同的值，如果超出范围，则调整到列表的开始或结尾。如果需要，序列 *s* 会扩展或缩减以容纳 *r* 中的所有元素。这里有一个例子：

```
a = [1,2,3,4,5]
a[1] = 6          # a = [1,6,3,4,5]
a[2:4] = [10,11]  # a = [1,6,10,11,5]
a[3:4] = [-1,-2,-3] # a = [1,6,10,-1,-2,-3,5]
a[2:] = [0]       # a = [1,6,0]
```

切片赋值可以提供一个可选的步长参数。然而，其行为更为受限，因为右侧的参数必须与被替换的切片具有完全相同的元素数量。这里有一个例子：

```
a = [1,2,3,4,5]
a[1::2] = [10,11]   # a = [1,10,3,11,5]
a[1::2] = [30,40,50] # ValueError. 左侧切片中只有两个元素
```

`del s[i]` 运算符从列表中移除元素 *i* 并减少其引用计数。`del s[i:j]` 移除切片中的所有元素。也可以提供步长，如 `del s[i:j:stride]`。



序列使用运算符 `<`、`>`、`<=`、`>=`、`==` 和 `!=` 进行比较。比较两个序列时，会先比较每个序列的第一个元素。如果它们不同，则比较结果由此决定。如果它们相同，比较会继续到每个序列的第二个元素。这个过程会持续进行，直到找到两个不同的元素或者两个序列中都没有更多元素存在。如果两个序列都到达了末尾，则认为这两个序列相等。如果 `a` 是 `b` 的子序列，那么 `a < b`。

字符串使用词典顺序进行比较。每个字符根据字符集（如 ASCII 或 Unicode）被分配一个唯一的数字索引。如果一个字符的索引小于另一个字符，则该字符小于另一个字符。关于字符排序的一个需要注意的地方是，前面提到的简单比较运算符与区域设置或语言设置相关的字符排序规则无关。因此，你不会使用这些操作来根据外语的标准惯例对字符串进行排序（有关更多信息，请参见 `unicodedata` 和 `locale` 模块）。

另一个需要注意的地方，这次涉及字符串。Python 有两种类型的字符串数据：字节字符串和 Unicode 字符串。字节字符串与其 Unicode 对应项不同，因为它们通常被认为是编码过的，而 Unicode 字符串代表原始未编码的字符值。因此，你永远不应在表达式或比较中混合使用字节字符串和 Unicode（例如，使用 `+` 连接字节字符串和 Unicode 字符串，或者使用 `==` 比较混合字符串）。在 Python 3 中，混合字符串类型会导致 `TypeError` 异常，但 Python 2 会尝试将字节字符串隐式提升为 Unicode。Python 2 的这一方面被广泛认为是一个设计错误，并且常常是不可预见的异常和难以解释的程序行为的来源。所以，为了让你的头脑不爆炸，不要在序列操作中混合字符串类型。

#### 字符串格式化

取模运算符 (`s % d`) 在给定格式字符串 `s` 和一个元组或映射对象（字典）`d` 中的对象集合时，会生成一个格式化的字符串。此运算符的行为类似于 C 的 `sprintf()` 函数。格式字符串包含两种类型的对象：普通字符（保持不变）和转换说明符，每个转换说明符都会被一个表示关联元组或映射中元素的格式化字符串替换。如果 `d` 是一个元组，则转换说明符的数量必须与 `d` 中对象的数量完全匹配。如果 `d` 是一个映射，则每个转换说明符必须与映射中的有效键名关联（使用括号，如下所述）。每个转换说明符以 `%` 字符开头，以表 4.1 中显示的转换字符之一结尾。

##### 表 4.1 字符串格式化转换

| 字符 | 输出格式 |
| --- | --- |
| d, i | 十进制整数或长整数。 |
| u | 无符号整数或长整数。 |
| o | 八进制整数或长整数。 |
| x | 十六进制整数或长整数。 |
| X | 十六进制整数（大写字母）。 |
| f | 浮点数，格式为 [-]m.dddddd。 |
| e | 浮点数，格式为 [-]m.dddddd±xx。 |
| E | 浮点数，格式为 [-]m.ddddddE+xx。 |
| g,G | 对于小于 -4 或大于精度的指数，使用 `%e` 或 `%E`；否则，使用 `%f`。 |
| s | 字符串或任何对象。格式化代码使用 `str()` 生成字符串。 |
| r | 生成与 `repr()` 相同的字符串。 |
| c | 单个字符。 |
| % | 字面量 `%`。 |

在 `%` 字符和转换字符之间，可以按以下顺序出现以下修饰符：

1. 括号中的键名，用于从映射对象中选择特定项。如果不存在这样的元素，则会引发 `KeyError` 异常。
2. 以下一项或多项：
   - `-` 符号，表示左对齐。默认情况下，值是右对齐的。
   - `+` 符号，表示应包含数字的符号（即使为正数）。
   - `0`，表示零填充。
3. 一个数字，指定最小字段宽度。转换后的值将打印在至少此宽度的字段中，并在左侧（如果给出了 `-` 标志，则在右侧）填充以达到字段宽度。
4. 一个句点，将字段宽度与精度分开。
5. 一个数字，指定要从字符串打印的最大字符数、浮点数中小数点后的位数或整数的最小位数。

此外，星号 (`*`) 字符可以用于任何宽度字段中代替数字。如果存在，则宽度将从元组中的下一个项目中读取。

以下代码说明了一些示例：

```
a = 42
b = 13.142783
c = "hello"
d = {'x':13, 'y':1.54321, 'z':'world'}
e = 5628398123741234

r = "a is %d" % a                  # r = "a is 42"
r = "%10d %f" % (a,b)              # r = "        42 13.142783"
r = "%+010d %E" % (a,b)             # r = "+000000042 1.314278E+01"
r = "%(x)-10d %(y)0.3g" % d         # r = "13         1.54"
r = "%0.4s %s" % (c, d['z'])        # r = "hell world"
r = "%*.%f" % (5,3,b)               # r = "13.143"
r = "e = %d" % e                    # r = "e = 5628398123741234"
```

当与字典一起使用时，字符串格式化运算符 `%` 经常用于模拟脚本语言中常见的字符串插值特性（例如，在字符串中扩展 `$var` 符号）。例如，如果你有一个值的字典，你可以按照如下方式将这些值扩展到格式化字符串的字段中：

```
stock = {
    'name' : 'GOOG',
    'shares' : 100,
    'price' : 490.10 }

r = "%(shares)d of %(name)s at %(price)0.2f" % stock
##### r = "100 shares of GOOG at 490.10"
```

以下代码显示了如何在字符串中扩展当前定义变量的值。`vars()` 函数返回一个字典，其中包含调用 `vars()` 时定义的所有变量。

```
name = "Elwood"
age  = 41
r = "%(name)s is %(age)s years old" % vars()
```

#### 高级字符串格式化

可以使用字符串上的 `s.format(*args, *kwargs)` 方法来获得更高级形式的字符串格式化。此方法收集任意数量的位置参数和关键字参数，并将它们的值替换到嵌入在 `s` 中的占位符中。形式为 `{n}` 的占位符（其中 `n` 是一个数字）将被传递给 `format()` 的位置参数 `n` 替换。形式为 `{name}` 的占位符将被传递给 `format` 的关键字参数 `name` 替换。使用 `{{` 输出单个 `{`，使用 `}}` 输出单个 `}`。例如：

```
r = "{0} {1} {2}".format('GOOG',100,490.10)
r = "{name} {shares} {price}".format(name='GOOG',shares=100,price=490.10)
r = "Hello {0}, your age is {age}".format("Elwood",age=47)
r = "Use {{ and }} to output single curly braces".format()
```

对于每个占位符，你还可以执行索引和属性查找。例如，在 `{name[n]}` 中，如果 `n` 是一个整数，则执行序列查找；在 `{name[key]}` 中，如果 `key` 是一个非数字字符串，则执行字典查找，形式为 `name['key']`。在 `{name.attr}` 中，执行属性查找。这里有一些示例：

```
stock = { 'name' : 'GOOG',
        'shares' : 100,
        'price' : 490.10 }
r = "{0[name]} {0[shares]} {0[price]}".format(stock)

x = 3 + 4j
r = "{0.real} {0.imag}".format(x)
```

在这些扩展中，只允许使用名称。不支持任意表达式、方法调用和其他操作。

你可以选择性地指定一个格式说明符，以更精确地控制输出。这是通过为每个占位符添加一个可选的格式说明符（使用冒号 `:`，如 `{place:format_spec}`）来提供的。使用此说明符，你可以指定列宽、小数位数和对齐方式。这里有一个示例：

```
r = "{name:8} {shares:8d} {price:8.2f}".format(name="GOOG", shares=100, price=490.10)
```



#### 高级字符串格式化

说明符的一般格式为 `[[fill[align]][sign] [0][width][.precision][type]`，其中 `[]` 括起来的每个部分都是可选的。`width` 说明符指定要使用的最小字段宽度，`align` 说明符是 `'<'`、`'>'` 或 `'^'` 之一，分别表示在字段内左对齐、右对齐和居中对齐。可选的填充字符 `fill` 用于填充空格。例如：

```
name = "Elwood"
r = "{0:<10}".format(name)   # r = 'Elwood     '
r = "{0:>10}".format(name)   # r = '     Elwood'
r = "{0:^10}".format(name)   # r = '  Elwood   '
r = "{0:=^10}".format(name)  # r = '==Elwood=='
```

`type` 说明符表示数据类型。表 4.2 列出了支持的格式代码。如果未提供，默认格式代码字符串为 `'s'`，整数为 `'d'`，浮点数为 `'f'`。

| 字符 | 输出格式 |
|-----------|-------------|
| d | 十进制整数或长整数。 |
| b | 二进制整数或长整数。 |
| o | 八进制整数或长整数。 |
| x | 十六进制整数或长整数。 |
| X | 十六进制整数（大写字母）。 |
| f,F | 浮点数，格式为 `[-]m.dddddd`。 |
| e | 浮点数，格式为 `[-]m.dddddde+xx`。 |
| E | 浮点数，格式为 `[-]m.ddddddE+xx`。 |
| g,G | 对于小于 -4 或大于精度的指数，使用 `e` 或 `E`；否则使用 `f`。 |
| n | 与 `g` 相同，但由当前区域设置决定小数点字符。 |
| % | 将数字乘以 100，然后使用 `f` 格式显示，并在后面加上 % 符号。 |
| s | 字符串或任何对象。格式化代码使用 `str()` 生成字符串。 |
| c | 单个字符。 |

格式说明符的 `sign` 部分是 `'+'`、`'-'` 或 `' '` 之一。`'+'` 表示所有数字都应使用前导符号。`'-'` 是默认值，仅对负数添加符号字符。`' '` 为正数添加前导空格。说明符的 `precision` 部分提供小数的精度位数。如果在数字的字段宽度前添加了前导 `'0'`，则数值将用前导 0 填充。以下是一些格式化不同类型数字的示例：

```
x = 42
r = '{0:10d}'.format(x)    # r = '        42'
r = '{0:10x}'.format(x)    # r = '        2a'
r = '{0:10b}'.format(x)    # r = '    101010'
r = '{0:010b}'.format(x)   # r = '0000101010'

y = 3.1415926
r = '{0:10.2f}'.format(y)  # r = '      3.14'
r = '{0:10.2e}'.format(y)     # r = '  3.14e+00'
r = '{0:+10.2f}'.format(y)    # r = '     +3.14'
r = '{0:+010.2f}'.format(y)   # r = '+000003.14'
r = '{0:+10.2%}'.format(y)    # r = '  +314.16%'
```

格式说明符的某些部分可以选择由传递给格式化函数的其他字段提供。它们使用与格式字符串中普通字段相同的语法来访问。例如：

```
y = 3.1415926
r = '{0:{width}.{precision}f}'.format(y,width=10,precision=3)
r = '{0:{1}.{2}f}'.format(y,10,3)
```

这种字段嵌套只能有一层深度，并且只能出现在格式说明符部分。此外，嵌套的值不能有任何自己的额外格式说明符。

关于格式说明符的一个注意事项是，对象可以定义自己的自定义说明符集。在底层，高级字符串格式化会对每个字段值调用特殊方法 `__format__(self, format_spec)`。因此，`format()` 操作的能力是开放式的，取决于它所应用的对象。例如，日期、时间和其他类型的对象可能定义自己的格式代码。

在某些情况下，你可能只想格式化对象的 `str()` 或 `repr()` 表示形式，而绕过其实现的 `__format__()` 方法的功能。为此，你可以在格式说明符前添加 `'!s'` 或 `'!r'` 修饰符。例如：

```
name = "Guido"
r = "{0!r:^20}".format(name)    # r = "     'Guido'     "
```

#### 字典操作

*字典*提供了名称和对象之间的映射。你可以对字典应用以下操作：

| 操作 | 描述 |
|-----------|-------------|
| `x = d[k]` | 通过键进行索引 |
| `d[k] = x` | 通过键进行赋值 |
| `del d[k]` | 通过键删除一项 |
| `k in d` | 测试键的存在 |
| `len(d)` | 字典中的项数 |

键值可以是任何不可变对象，例如字符串、数字和元组。此外，字典键可以指定为逗号分隔的值列表，如下所示：

```
d = {}
d[1,2,3] = "foo"
d[1,0,3] = "bar"
```

在这种情况下，键值表示一个元组，使得前面的赋值等同于以下内容：

```
d[(1,2,3)] = "foo"
d[(1,0,3)] = "bar"
```

#### 集合操作

`set` 和 `frozenset` 类型支持许多常见的集合操作：

| 操作 | 描述 |
| --- | --- |
| `s \| t` | *s* 和 *t* 的并集 |
| `s & t` | *s* 和 *t* 的交集 |
| `s - t` | 集合差集 |
| `s ^ t` | 对称差集 |
| `len(s)` | 集合中的项数 |
| `max(s)` | 最大值 |
| `min(s)` | 最小值 |

并集、交集和差集运算的结果将与最左边的操作数具有相同的类型。例如，如果 *s* 是 `frozenset`，即使 *t* 是集合，结果也将是 `frozenset`。

#### 增强赋值

Python 提供了以下增强赋值运算符集：

| 操作 | 描述 |
| --- | --- |
| `x += y` | `x = x + y` |
| `x -= y` | `x = x - y` |
| `x *= y` | `x = x * y` |
| `x /= y` | `x = x / y` |
| `x //= y` | `x = x // y` |
| `x **= y` | `x = x ** y` |
| `x %= y` | `x = x % y` |
| `x &= y` | `x = x & y` |
| `x \|= y` | `x = x \| y` |
| `x ^= y` | `x = x ^ y` |
| `x >>= y` | `x = x >> y` |
| `x <<= y` | `x = x << y` |

这些运算符可以在任何使用普通赋值的地方使用。以下是一个示例：

```
a = 3
b = [1,2]
c = "Hello %s %s"
a += 1                  # a = 4
b[1] += 10              # b = [1, 12]
c %= ("Monty", "Python")  # c = "Hello Monty Python"
```

增强赋值不会违反可变性，也不会对对象进行就地修改。因此，写 `x += y` 会创建一个全新的对象 *x*，其值为 *x* + *y*。用户定义的类可以使用第 3 章“类型和对象”中描述的特殊方法来重新定义增强赋值运算符。

#### 属性 (.) 运算符

点 (.) 运算符用于访问对象的属性。以下是一个示例：

```
foo.x = 3
print foo.y
a = foo.bar(3,4,5)
```

单个表达式中可以出现多个点运算符，例如 foo.y.a.b。点运算符也可以应用于函数的中间结果，例如 a = foo.bar(3,4,5).spam。

用户定义的类可以重新定义或自定义 (.) 的行为。更多细节可以在第 3 章和第 7 章“类和面向对象编程”中找到。

#### 函数调用 () 运算符

f(args) 运算符用于对 f 进行函数调用。函数的每个参数都是一个表达式。在调用函数之前，所有参数表达式都从左到右完全求值。这有时被称为 *应用序求值*。

可以使用 functools 模块中的 partial() 函数对函数参数进行部分求值。例如：

```
def foo(x,y,z):
    return x + y + z

from functools import partial
f = partial(foo,1,2)  # 为 foo 的 x 和 y 参数提供值
f(3)                   # 调用 foo(1,2,3)，结果为 6
```

partial() 函数对函数的一些参数进行求值，并返回一个对象，你可以调用该对象在稍后提供剩余参数。在前面的示例中，变量 f 表示一个部分求值的函数，其中前两个参数已经计算完毕。你只需要提供最后一个剩余的参数值，函数就会执行。函数参数的部分求值与称为 *柯里化* 的过程密切相关，这是一种机制，通过该机制，一个接受多个参数（如 f(x,y)）的函数被分解为一系列每个只接受一个参数的函数（例如，你通过固定 x 来部分求值 f，得到一个新函数，你向其提供 y 的值以产生结果）。

#### 转换函数

有时需要在内置类型之间执行转换。要在类型之间转换，你只需使用类型名称作为函数。此外，还提供了几个内置函数来执行特殊类型的转换。所有这些函数都返回一个表示转换后值的新对象。

| 函数 | 描述 |
| --- | --- |
| int(x [,base]) | 将 x 转换为整数。如果 x 是字符串，则 base 指定基数。 |
| float(x) | 将 x 转换为浮点数。 |
| complex(real [,imag]) | 创建一个复数。 |
| str(x) | 将对象 x 转换为字符串表示形式。 |



| 函数 | 描述 |
| --- | --- |
| `repr(x)` | 将对象 *x* 转换为表达式字符串。 |
| `format(x [,format_spec])` | 将对象 *x* 转换为格式化的字符串。 |
| `eval(str)` | 计算一个字符串并返回一个对象。 |
| `tuple(s)` | 将 *s* 转换为一个元组。 |
| `list(s)` | 将 *s* 转换为一个列表。 |
| `set(s)` | 将 *s* 转换为一个集合。 |
| `dict(d)` | 创建一个字典。*d* 必须是 `(key,value)` 元组的序列。 |
| `frozenset(s)` | 将 *s* 转换为一个冻结集合。 |
| `chr(x)` | 将一个整数转换为一个字符。 |
| `unichr(x)` | 将一个整数转换为一个 Unicode 字符（仅限 Python 2）。 |
| `ord(x)` | 将一个字符转换为其整数值。 |
| `hex(x)` | 将一个整数转换为一个十六进制字符串。 |
| `bin(x)` | 将一个整数转换为一个二进制字符串。 |
| `oct(x)` | 将一个整数转换为一个八进制字符串。 |

请注意，`str()` 和 `repr()` 函数可能返回不同的结果。`repr()` 通常创建一个可以用 `eval()` 重新创建对象的表达式字符串。另一方面，`str()` 产生对象的简洁或格式良好的表示形式（并且被 print 语句使用）。`format(x, [format_spec])` 函数产生的输出与高级字符串格式化操作产生的输出相同，但应用于单个对象 x。作为输入，它接受一个可选的 *format_spec*，这是一个包含格式化代码的字符串。`ord()` 函数返回一个字符的整数序数值。对于 Unicode，这个值将是整数码点。`chr()` 和 `unichr()` 函数将整数转换回字符。

要将字符串转换回数字，请使用 `int()`、`float()` 和 `complex()` 函数。`eval()` 函数也可以将包含有效表达式的字符串转换为对象。这是一个示例：

```
a = int("34")           # a = 34
b = long("0xfe76214", 16) # b = 266822164L (0xfe76214L)
b = float("3.1415926")  # b = 3.1415926
c = eval("3, 5, 6")     # c = (3,5,6)
```

在创建容器的函数（`list()`、`tuple()`、`set()` 等）中，参数可以是任何支持迭代的对象，用于生成用于填充所创建对象的所有项。

#### 类是类型（type）的实例

`and`、`or` 和 `not` 关键字可以形成布尔表达式。这些运算符的行为如下：

| 运算符 | 描述 |
| --- | --- |
| `x or y` | 如果 *x* 为假，则返回 *y*；否则，返回 *x*。 |
| `x and y` | 如果 *x* 为假，则返回 *x*；否则，返回 *y*。 |
| `not x` | 如果 *x* 为假，则返回 `1`；否则，返回 `0`。 |

当你使用表达式来确定真值或假值时，`True`、任何非零数字、非空字符串、列表、元组或字典都被视为真。`False`、零、`None` 以及空列表、元组和字典求值为假。布尔表达式从左到右求值，并且只有在确定最终值需要时才消耗右操作数。例如，`a and b` 仅在 `a` 为真时才求值 `b`。这有时被称为 *"短路"* 求值。

#### 对象相等性与同一性

相等运算符（`x == y`）测试 `x` 和 `y` 的值是否相等。对于列表和元组，比较所有元素，如果它们值相等则求值为真。对于字典，只有当 `x` 和 `y` 具有相同的键集，并且所有相同键的对象都具有相等的值时，才返回真值。两个集合如果具有相同的元素（使用相等性（`==`）进行比较），则它们相等。

同一性运算符（`x is y` 和 `x is not y`）测试两个对象，看看它们是否引用内存中的同一个对象。一般来说，可能存在 `x == y` 但 `x is not y` 的情况。

不兼容类型对象之间的比较（例如文件和浮点数）可能是允许的，但结果是任意的，可能没有任何意义。根据类型，它也可能导致异常。

#### 求值顺序

表 4.3 列出了 Python 运算符的操作顺序（优先级规则）。除幂运算符（`**`）外，所有运算符均从左到右求值，并在表中按优先级从高到低列出。也就是说，表中先列出的运算符比后列出的运算符更早求值。（请注意，包含在子节中的运算符，如 `x * y`、`x / y`、`x // y` 和 `x % y`，具有相同的优先级。）

| 运算符 | 名称 |
|----------|------|
| `(... )`, `[...]`, `{...}` | 元组、列表和字典创建 |
| `s[i]`, `s[i:j]` | 索引和切片 |
| `s.attr` | 属性 |
| `f(...)` | 函数调用 |
| `+x`, `-x`, `~x` | 一元运算符 |
| `x ** y` | 幂（右结合） |
| `x * y`, `x / y`, `x // y`, `x % y` | 乘法、除法、整除、取模 |
| `x + y`, `x - y` | 加法、减法 |
| `x << y`, `x >> y` | 位移 |
| `x & y` | 按位与 |
| `x ^ y` | 按位异或 |
| `x | y` | 按位或 |
| `x < y`, `x <= y`,<br>`x > y`, `x >= y`,<br>`x == y`, `x != y` | 比较、同一性和序列成员测试 |
| `x is y`, `x is not y` | |
| `x in s`, `x not in s` | |
| `not x` | 逻辑非 |
| `x and y` | 逻辑与 |
| `x or y` | 逻辑或 |
| `lambda args: expr` | 匿名函数 |

表 4.3 中的求值顺序不由 `x` 和 `y` 的类型决定。因此，即使用户定义的对象可以重新定义单个运算符，也不可能自定义底层的求值顺序、优先级和结合性规则。

##### 条件表达式

一种常见的编程模式是根据表达式的结果有条件地分配一个值。例如：

```
if a <= b:
    minvalue = a
else:
    minvalue = b
```

这段代码可以使用 *条件表达式* 缩短。例如：

```
minvalue = a if a <=b else b
```

在此类表达式中，首先对中间的条件进行求值。如果结果为 `True`，则对 `if` 左侧的表达式求值。否则，对 `else` 后的表达式求值。

条件表达式应该谨慎使用，因为它们可能会导致混淆（尤其是如果它们被嵌套或与其他复杂表达式混合）。然而，一个特别有用的应用是在列表推导式和生成器表达式中。例如：

```
values = [1, 100, 45, 23, 73, 37, 69 ]
clamped = [x if x < 50 else 50 for x in values]
print(clamped)    #[1, 50, 45, 23, 50, 37, 50]
```

# 5

程序结构与控制流

本章详细介绍了程序结构和控制流。主题包括条件语句、迭代、异常和上下文管理器。

## 程序结构与执行

Python 程序的结构是一系列语句。所有语言特性，包括变量赋值、函数定义、类和模块导入，都是与其他所有语句地位平等的语句。事实上，没有“特殊”语句，每个语句都可以放置在程序中的任何位置。例如，这段代码定义了函数的两个不同版本：

```
if debug:
    def square(x):
        if not isinstance(x,float):
            raise TypeError("Expected a float")
        return x * x
else:
    def square(x):
        return x * x
```

当加载源文件时，解释器总是按顺序执行每条语句，直到没有更多语句可执行。此执行模型既适用于你作为主程序运行的文件，也适用于通过 import 加载的库文件。

#### 条件执行

if、else 和 elif 语句控制条件代码的执行。条件语句的一般格式如下：

```
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



如果不需执行任何操作，可以省略条件语句的 `else` 和 `elif` 子句。当某个子句没有对应的语句时，可以使用 `pass` 语句：

```
if expression:
    pass        # Do nothing
else:
    statements
```

#### 循环与迭代

可以使用 `for` 和 `while` 语句实现循环。示例如下：

```
while expression:
    statements

for i in s:
    statements
```

`while` 语句会持续执行语句，直到关联的表达式求值为假。`for` 语句则遍历 `s` 的所有元素，直到没有更多元素可用。`for` 语句适用于任何支持迭代的对象。这显然包括内置序列类型（如列表、元组和字符串），也包括实现了迭代器协议的任何对象。

如果对象 `s` 能与以下代码配合使用（该代码反映了 `for` 语句的实现），则表明该对象支持迭代：

```
it = s.__iter__()          # Get an iterator for s
while 1:
    try:
        i = it.next()      # Get next item (Use __next__ in Python 3)
    except StopIteration:  # No more items
        break
    # Perform operations on i
    ...
```

在语句 `for i in s` 中，变量 `i` 被称为*迭代变量*。在循环的每次迭代中，它会从 `s` 接收一个新值。迭代变量的作用域不限于 `for` 语句内部。如果先前定义的变量具有相同名称，该变量的值将被覆盖。此外，循环结束后，迭代变量将保留最后一个值。

如果迭代中使用的元素是大小相同的序列，可以使用类似以下的语句将它们的值解包到单独的迭代变量中：

```
for x,y,z in s:
    statements
```

在此示例中，`s` 必须包含或产生序列，每个序列有三个元素。在每次迭代中，变量 `x`、`y` 和 `z` 的内容会被赋予相应序列的元素。虽然最常见的是在 `s` 是元组序列时使用此方法，但只要 `s` 中的元素是任何类型的序列（包括列表、生成器和字符串），解包操作都适用。

在循环时，除了数据值外，有时还需要跟踪数值索引。示例如下：

```
i = 0
for x in s:
```

Python 提供了一个内置函数 `enumerate()`，可用于简化此代码：

```
for i,x in enumerate(s):
    statements
```

`enumerate(s)` 创建一个迭代器，简单地返回一系列元组 `(0, s[0])`、`(1, s[1])`、`(2, s[2])`，依此类推。

另一个常见的循环问题是并行遍历两个或多个序列——例如，编写一个循环，在每次迭代中从不同的序列中取项，如下所示：

```
##### s and t are two sequences
i = 0
while i < len(s) and i < len(t):
    x = s[i]     # Take an item from s
    y = t[i]     # Take an item from t
    statements
    i += 1
```

此代码可以使用 `zip()` 函数简化。例如：

```
##### s and t are two sequences
for x,y in zip(s,t):
    statements
```

`zip(s,t)` 将序列 `s` 和 `t` 组合成一系列元组 `(s[0],t[0])`、`(s[1],t[1])`、`(s[2], t[2])`，依此类推。如果 `s` 和 `t` 长度不等，则在最短的序列处停止。关于 `zip()` 需要注意的是，在 Python 2 中，它会完全消耗 `s` 和 `t`，创建一个元组列表。对于生成器和包含大量数据的序列，这可能不是你想要的效果。函数 `itertools.izip()` 实现了与 `zip()` 相同的效果，但一次只生成一个压缩值，而不是创建一个大型元组列表。在 Python 3 中，`zip()` 函数也以这种方式生成值。

要跳出循环，请使用 `break` 语句。例如，以下代码从文件中读取文本行，直到遇到空行：

```
for line in open("foo.txt"):
    stripped = line.strip()
    if not stripped:
        break      # A blank line, stop reading
    # process the stripped line
    ...
```

要跳转到循环的下一次迭代（跳过循环体的剩余部分），请使用 `continue` 语句。此语句使用较少，但有时在反转测试并缩进另一级别会使程序嵌套过深或不必要地复杂化时非常有用。例如，以下循环跳过文件中的所有空行：

```
for line in open("foo.txt"):
    stripped = line.strip()
    if not not stripped:
        continue   # Skip the blank line
    # process the stripped line
    ...
```

`break` 和 `continue` 语句仅适用于当前正在执行的最内层循环。如果需要从深层嵌套的循环结构中跳出，可以使用异常。Python 不提供 "goto" 语句。

你也可以将 `else` 语句附加到循环结构，如下例所示：

```
##### for-else
for line in open("foo.txt"):
    stripped = line.strip()
    if not stripped:
        break
    # process the stripped line
    ...
else:
    raise RuntimeError("Missing section separator")
```

循环的 `else` 子句仅在循环正常执行完毕时执行。这可能是立即发生（如果循环根本不会执行）或在最后一次迭代之后发生。另一方面，如果循环使用 `break` 语句提前终止，则 `else` 子句会被跳过。

循环 `else` 子句的主要用例是在迭代数据但需要在循环提前中断时设置或检查某种标志或条件的代码中。例如，如果未使用 `else`，前面的代码可能需要使用标志变量重写，如下所示：

```
found_separator = False
for line in open("foo.txt"):
    stripped = line.strip()
    if not stripped:
        found_separator = True
        break
    # process the stripped line
    ...
if not found_separator:
    raise RuntimeError("Missing section separator")
```

##### 异常

异常表示错误并中断程序的正常控制流。异常使用 `raise` 语句引发。`raise` 语句的一般格式为 `raise Exception([value])`，其中 `Exception` 是异常类型，`value` 是可选值，用于提供有关异常的详细信息。示例如下：

```
raise RuntimeError("Unrecoverable Error")
```

如果单独使用 `raise` 语句，则会再次引发最近生成的异常（但这仅在处理先前引发的异常时有效）。

要捕获异常，请使用 `try` 和 `except` 语句，如下所示：

```
try:
    f = open('foo')
except IOError as e:
    statements
```

当发生异常时，解释器会停止执行 `try` 块中的语句，并查找与发生的异常匹配的 `except` 子句。如果找到，则控制权传递给 `except` 子句中的第一条语句。执行 `except` 子句后，控制权继续到 `try`-`except` 块之后的第一条语句。否则，异常会向上传播到 `try` 语句所在的代码块。此代码本身可能被封装在可以处理异常的 `try`-`except` 中。如果异常一直传播到程序顶层而未被捕获，解释器将中止并显示错误消息。如果需要，未捕获的异常也可以传递给用户定义的函数 `sys.excepthook()`，如第13章 "Python 运行时服务" 中所述。

`except` 语句的可选 `as var` 修饰符提供一个变量名，如果发生异常，该变量将放置由 `raise` 语句提供的异常类型的实例。异常处理器可以检查此值以获取有关异常原因的更多信息。例如，你可以使用 `isinstance()` 来检查异常类型。关于语法的一个注意事项：在以前的 Python 版本中，`except` 语句写为 `except ExcType, var`，其中异常类型和变量用逗号（`,`）分隔。在 Python 2.6 中，此语法仍然有效，但已弃用。在新代码中，请使用 `as var` 语法，因为它在 Python 3 中是必需的。

多个异常处理块使用多个 `except` 子句指定，如下例所示：

```
try:
    do something
except IOError as e:
    # Handle I/O error
    ...
except TypeError as e:
    # Handle Type error
    ...
except NameError as e:
    # Handle Name error
    ...
```

单个处理程序可以捕获多种异常类型，如下所示：

```
try:
    do something
except (IOError, TypeError, NameError) as e:
    # Handle I/O, Type, or Name errors
    ...
```

要忽略异常，请使用 `pass` 语句，如下所示：

```
try:
    do something
except IOError:
    pass            # Do nothing (oh well).
```

要捕获除程序退出相关异常之外的所有异常，请使用 `Exception`，如下所示：

```
try:
    do something
except Exception as e:
    error_log.write('An error occurred : %s\n' % e)
```



#### 内置异常

捕获所有异常时，应注意向用户提供准确的错误信息。例如，在前面的代码中，错误信息和相关的异常值被记录了下来。如果未包含任何关于异常值的信息，可能会导致调试因意外原因而失败的代码变得异常困难。

可以使用不带异常类型的 `except` 来捕获所有异常，如下所示：

```
try:
    do something
except:
    error_log.write('An error occurred\n')
```

这种形式的 `except` 的正确使用比看起来要棘手得多，应该尽量避免。例如，这段代码也会捕获键盘中断和程序退出请求——这些可能是你不想捕获的内容。

`try` 语句还支持 `else` 子句，它必须跟在最后一个 `except` 子句之后。如果 `try` 块中的代码没有引发异常，则会执行此代码。以下是一个示例：

```
try:
    f = open('foo', 'r')
except IOError as e:
    error_log.write('Unable to open foo : %s\n' % e)
else:
    data = f.read()
    f.close()
```

`finally` 语句定义了为 `try` 块中包含的代码执行的清理操作。以下是一个示例：

```
f = open('foo','r')
try:
    # Do some stuff
    ...
finally:
    f.close()
    # File closed regardless of what happened
```

`finally` 子句并非用于捕获错误。相反，它用于提供必须始终执行的代码，无论是否发生错误。如果未引发异常，则 `finally` 子句中的代码会在 `try` 块中的代码执行后立即执行。如果发生异常，控制权首先传递给 `finally` 子句的第一个语句。此代码执行后，异常将被重新引发，以由另一个异常处理程序捕获。

Python 定义了表 5.1 中列出的内置异常。

###### 表 5.1 内置异常

| 异常 | 描述 |
| --- | --- |
| **BaseException** | 所有异常的根类。 |
| `GeneratorExit` | 由生成器的 .close() 方法引发。 |
| `KeyboardInterrupt` | 由中断键（通常是 Ctrl+C）生成。 |
| `SystemExit` | 程序退出/终止。 |
| **Exception** | 所有非退出异常的基类。 |
| `StopIteration` | 引发以停止迭代。 |
| `StandardError` | 所有内置异常的基类（仅限 Python 2）。在 Python 3 中，以下所有异常都归类在 Exception 下。 |
| `ArithmeticError` | 算术异常的基类。 |
| `FloatingPointError` | 浮点运算失败。 |
| `ZeroDivisionError` | 除以零或取模运算。 |
| `AssertionError` | 由 assert 语句引发。 |
| `AttributeError` | 当属性名称无效时引发。 |
| `EnvironmentError` | 发生在 Python 外部的错误。 |
| `IOError` | I/O 或文件相关错误。 |
| `OSError` | 操作系统错误。 |
| `EOFError` | 到达文件末尾时引发。 |
| `ImportError` | import 语句失败。 |
| `LookupError` | 索引和键错误。 |
| `IndexError` | 序列索引超出范围。 |
| `KeyError` | 字典键不存在。 |
| `MemoryError` | 内存不足。 |
| `NameError` | 无法找到局部或全局名称。 |
| `UnboundLocalError` | 未绑定的局部变量。 |
| `ReferenceError` | 在引用对象销毁后使用了弱引用。 |
| `RuntimeError` | 通用的兜底错误。 |
| `NotImplementedError` | 未实现的功能。 |
| `SyntaxError` | 解析错误。 |
| `IndentationError` | 缩进错误。 |
| `TabError` | 不一致的制表符使用（使用 -tt 选项生成）。 |
| `SystemError` | 解释器中的非致命系统错误。 |
| `TypeError` | 向操作传递了不恰当的类型。 |
| `ValueError` | 无效类型。 |
| `UnicodeError` | Unicode 错误。 |
| `UnicodeDecodeError` | Unicode 解码错误。 |
| `UnicodeEncodeError` | Unicode 编码错误。 |
| `UnicodeTranslateError` | Unicode 翻译错误。 |

异常按表中所示组织为层次结构。特定组中的所有异常都可以通过在 `except` 子句中指定组名来捕获。以下是一个示例：

```
try:
    _statements_
except LookupError:    # Catch IndexError or KeyError
    _statements_
```

或

```
try:
    _statements_
except Exception:   # Catch any program-related exception
    _statements_
```

在异常层次结构的顶层，异常根据其是否与程序退出相关进行分组。例如，`SystemExit` 和 `KeyboardInterrupt` 异常没有归类在 `Exception` 下，因为想要捕获所有与程序相关错误的程序通常不想意外地捕获程序终止。

##### 定义新异常

所有内置异常都基于类来定义。要创建新异常，请创建一个继承自 `Exception` 的新类定义，例如：

```
class NetworkError(Exception): pass
```

要使用你的新异常，请将其与 `raise` 语句一起使用，如下所示：

```
raise NetworkError("Cannot find host.")
```

引发异常时，`raise` 语句提供的可选值用作异常类构造函数的参数。大多数情况下，这只是一个表示某种错误消息的字符串。但是，用户定义的异常可以编写为接受一个或多个异常值，如本例所示：

```
class DeviceError(Exception):
    def __init__(self,errno,msg):
        self.args = (errno, msg)
        self.errno = errno
        self.errmsg = msg

###### Raises an exception (multiple arguments)
raise DeviceError(1, 'Not Responding')
```

当你创建一个重新定义了 `__init__()` 的自定义异常类时，重要的是将包含传递给 `__init__()` 的参数的元组赋值给属性 `self.args`，如示例所示。此属性在打印异常回溯消息时使用。如果未定义它，用户在发生错误时将无法看到有关异常的任何有用信息。

异常可以使用继承组织为层次结构。例如，前面定义的 `NetworkError` 异常可以作为多种更具体错误的基类。以下是一个示例：

```
class HostnameError(NetworkError): pass
class TimeoutError(NetworkError): pass

def error1():
    raise HostnameError("Unknown host")

def error2():
    raise TimeoutError("Timed out")

try:
    error1()
except NetworkError as e:
    if type(e) is HostnameError:
        # Perform special actions for this kind of error
        ...
```

在这种情况下，`except NetworkError` 语句捕获任何派生自 `NetworkError` 的异常。要找出引发的具体错误类型，请使用 `type()` 检查执行值的类型。或者，可以使用 `sys.exc_info()` 函数检索有关最后引发的异常的信息。

#### 上下文管理器和 `with` 语句

系统资源（如文件、锁和连接）的适当管理与异常结合时，通常是一个棘手的问题。例如，引发的异常可能导致控制流绕过负责释放关键资源（如锁）的语句。

`with` 语句允许一系列语句在由作为上下文管理器的对象控制的运行时上下文中执行。以下是一个示例：

```
with open("debuglog","a") as f:
    f.write("Debugging\n")
    statements
    f.write("Done\n")
```

```
import threading
lock = threading.Lock()
with lock:
    # Critical section
    statements
    # End critical section
```

在第一个示例中，`with` 语句会自动在控制流离开其后的语句块时关闭打开的文件。在第二个示例中，`with` 语句会在控制进入和离开其后的语句块时自动获取和释放锁。

`with obj` 语句允许对象 `obj` 管理控制流进入和退出其后相关语句块时发生的情况。当 `with obj` 语句执行时，它会执行方法 `obj.__enter__()` 以发出信号表明正在进入新的上下文。当控制流离开上下文时，将执行方法 `obj.__exit__(type, value, traceback)`。如果未引发异常，则传递给 `__exit__()` 的三个参数都设置为 `None`。否则，它们包含导致控制流离开上下文的异常的类型、值和回溯信息。`__exit__()` 方法返回 `True` 或 `False` 以指示引发的异常是否已处理（如果返回 `False`，则引发的任何异常都会从上下文中传播出去）。



#### 断言与 `__debug__`

`assert` 语句可以向程序引入调试代码。`assert` 的通用形式为

```
assert test [, msg]
```

其中 *test* 是一个应求值为 `True` 或 `False` 的表达式。如果 *test* 的求值结果为 `False`，`assert` 会引发一个 `AssertionError` 异常，并附带可选的消息 *msg*（该消息在 `assert` 语句中提供）。下面是一个示例：

```
def write_data(file,data):
    assert file, "write_data: file not defined!"
    ...
```

`assert` 语句不应用于必须执行才能使程序正确运行的代码，因为如果 Python 在优化模式下运行（通过解释器的 `-O` 选项指定），这些代码将不会被执行。特别地，使用 `assert` 来检查用户输入是错误的。相反，`assert` 语句应用于检查那些应该始终为真的条件；如果某个条件被违反，则表示程序中存在一个 bug，而不是用户的错误。

例如，如果前面所示的函数 `write_data()` 旨在供最终用户使用，那么 `assert` 语句应被常规的 `if` 语句和所需的错误处理所替代。

除了 `assert`，Python 还提供了内置的只读变量 `__debug__`，除非解释器在优化模式下运行（通过 `-O` 选项指定），否则它被设置为 `True`。程序可以根据需要检查这个变量——如果它被设置，可能会运行额外的错误检查过程。`__debug__` 变量的底层实现在解释器中经过了优化，因此 `if` 语句本身的额外控制流逻辑实际上并未包含在内。如果 Python 在正常模式下运行，`if __debug__` 语句下的语句只是直接内联到程序中，而不包含 `if` 语句本身。在优化模式下，`if __debug__` 语句及所有相关语句会完全从程序中移除。

使用 `assert` 和 `__debug__` 可以实现高效的双模式程序开发。例如，在调试模式下，你可以自由地在代码中使用断言和调试检查来验证程序的正确运行。在优化模式下，所有这些额外的检查都会被剥离，从而不会产生额外的性能开销。

### 函数与函数式编程

大型程序通常被分解成函数，以提高模块化程度和便于维护。Python 使得定义函数变得简单，同时还融入了函数式编程语言中大量令人惊讶的特性。本章描述函数、作用域规则、闭包、装饰器、生成器、协程以及其他函数式编程特性。此外，还描述了列表推导式和生成器表达式——两者都是声明式编程和数据处理的强大工具。

##### 函数

函数通过 `def` 语句定义：

```
def add(x,y):
    return x + y
```

函数体就是当函数被调用时执行的一系列语句。你可以通过编写函数名后跟一个函数参数元组来调用函数，例如 `a = add(3,4)`。参数的顺序和数量必须与函数定义中给出的相匹配。如果不匹配，将引发 `TypeError` 异常。

你可以通过在函数定义中赋值来为函数参数附加默认值。例如：

```
def split(line,delimiter=','):
    statements
```

当函数定义了一个带有默认值的参数时，该参数及其后面的所有参数都是可选的。如果未在函数定义中为所有可选参数分配值，将引发 `SyntaxError` 异常。

默认参数值始终被设置为函数定义时提供的对象。下面是一个示例：

```
a = 10
def foo(x=a):
    return x

a = 5          # 重新赋值 'a'。
foo()          # 返回 10（默认值未改变）
```

此外，使用可变对象作为默认值可能会导致意外的行为：

```
def foo(x, items=[]):
    items.append(x)
    return items
foo(1)      # 返回 [1]
foo(2)      # 返回 [1, 2]
foo(3)      # 返回 [1, 2, 3]
```

请注意，默认参数如何保留了之前调用所做的修改。为了防止这种情况，最好使用 `None` 并添加检查，如下所示：

```
def foo(x, items=None):
    if items is None:
        items = []
    items.append(x)
    return items
```

如果在最后一个参数名后添加星号 (*)，函数可以接受可变数量的参数：

```
def fprintf(file, fmt, *args):
    file.write(fmt % args)

##### 使用 fprintf。args 接收 (42,"hello world", 3.45)
fprintf(out,"%d %s %f", 42, "hello world", 3.45)
```

在这种情况下，所有剩余的参数都作为元组放入 *args* 变量中。要将一个元组 *args* 作为参数传递给函数，可以在函数调用中使用 `*args` 语法，如下所示：

```
def printf(fmt, *args):
        # 调用另一个函数并传递 args
        fprintf(sys.stdout, fmt, *args)
```

函数参数也可以通过显式命名每个参数并指定一个值来提供。这些被称为*关键字参数*。下面是一个示例：

```
def foo(w,x,y,z):
    statements

##### 关键字参数调用
foo(x=3, y=22, w='hello', z=[1,2])
```

使用关键字参数时，参数的顺序无关紧要。但是，除非有默认值，否则你必须显式地命名所有必需的函数参数。如果你省略了任何必需的参数，或者关键字的名称与函数定义中的任何参数名不匹配，将引发 `TypeError` 异常。此外，由于任何 Python 函数都可以使用关键字调用风格来调用，因此通常最好使用描述性的参数名来定义函数。

位置参数和关键字参数可以出现在同一个函数调用中，前提是所有位置参数出现在前面，为所有非可选参数提供了值，并且没有参数值被定义多次。下面是一个示例：

```
foo('hello', 3, z=[1,2], y=22)
foo(3, 22, w='hello', z=[1,2])   # TypeError。为 w 提供了多个值
```



#### **kwargs关键字参数

如果函数定义的最后一个参数以`**`开头，所有额外的关键字参数（那些不匹配其他任何参数名的参数）都会被放入一个字典中，并传递给函数。这是一种编写函数的有用方式，可以接受大量潜在的开放式配置选项，这些选项如果作为参数列出会过于笨重。以下是一个示例：

```python
def make_table(data, **parms):
    # 从parms（一个字典）中获取配置参数
    fgcolor = parms.pop("fgcolor", "black")
    bgcolor = parms.pop("bgcolor", "white")
    width = parms.pop("width", None)
    ...
    # 没有更多选项了
    if parms:
        raise TypeError("Unsupported configuration options %s" % list(parms))

make_table(items, fgcolor="black", bgcolor="white", border=1,
           borderstyle="grooved", cellpadding=10,
           width=400)
```

你可以将额外的关键字参数与可变长度参数列表结合使用，只要`**`参数出现在最后：

```python
##### 接受任意数量的位置参数或关键字参数
def spam(*args, **kwargs):
    # args 是一个包含位置参数的元组
    # kwargs 是一个包含关键字参数的字典
    ...
```

关键字参数也可以使用`**kwargs`语法传递给另一个函数：

```python
def callfunc(*args, **kwargs):
    func(*args, **kwargs)
```

这种`*args`和`**kwargs`的用法通常用于为其他函数编写包装器和代理。例如，`callfunc()`接受任意组合的参数，并简单地将它们传递给`func()`。

#### 参数传递和返回值

当函数被调用时，函数参数仅仅是引用传入输入对象的名称。参数传递的底层语义并不完全符合你可能从其他编程语言中了解到的任何单一风格，比如"按值传递"或"按引用传递"。例如，如果你传递一个不可变值，参数看起来就像按值传递。然而，如果传递一个可变对象（如列表或字典）给一个函数，并在其中修改了它，这些更改将反映在原始对象中。以下是一个示例：

```python
a = [1, 2, 3, 4, 5]
def square(items):
    for i, x in enumerate(items):
        items[i] = x * x    # 就地修改items

square(a)    # 将a变为 [1, 4, 9, 16, 25]
```

那些就地修改输入值或在幕后改变程序其他部分状态的函数被称为具有*副作用*。作为一种通用规则，这种编程风格最好避免使用，因为随着程序规模和复杂度的增长，此类函数可能成为微妙编程错误的来源（例如，仅从阅读函数调用并不明显一个函数是否有副作用）。此类函数与涉及线程和并发的程序交互不佳，因为副作用通常需要通过锁来保护。

`return`语句从函数中返回一个值。如果没有指定值或省略了`return`语句，则返回`None`对象。要返回多个值，请将它们放在一个元组中：

```python
def factor(a):
    d = 2
    while (d <= (a / 2)):
        if ((a / d) * d == a):
            return ((a / d), d)
        d = d + 1
    return (a, 1)
```

以元组形式返回的多个返回值可以赋值给各个变量：

```python
x, y = factor(1243)    # 返回值放入x和y中。

##### 或者

(x, y) = factor(1243)  # 替代形式。行为相同。
```

#### 作用域规则

每次函数执行时，都会创建一个新的本地命名空间。这个命名空间代表一个本地环境，包含函数参数的名称以及在函数体内赋值的变量名称。在解析名称时，解释器首先搜索本地命名空间。如果没有匹配项，则搜索全局命名空间。函数的全局命名空间始终是定义该函数的模块。如果解释器在全局命名空间中没有找到匹配项，则会在内置命名空间中进行最终检查。如果仍然没有找到，则会引发`NameError`异常。

命名空间的一个特殊之处是在函数内操纵全局变量。例如，考虑以下代码：

```python
a = 42
def foo():
    a = 13
foo()
##### a 仍然是 42
```

当此代码执行时，`a`的值仍然是42，尽管看起来我们可能在函数`foo`中修改了变量`a`。当变量在函数内部被赋值时，它们总是绑定到函数的本地命名空间；因此，函数体中的变量`a`引用的是一个包含值13的全新对象，而不是外部变量。要改变这种行为，请使用`global`语句。`global`简单地将名称声明为属于全局命名空间，并且仅在需要修改全局变量时才必要。它可以放置在函数体中的任何位置并可重复使用。以下是一个示例：

```python
a = 42
b = 37
def foo():
    global a      # 'a' 在全局命名空间中
    a = 13
    b = 0
foo()
##### a 现在是 13。b 仍然是 37。
```

Python支持嵌套函数定义。以下是一个示例：

```python
def countdown(start):
    n = start
    def display():         # 嵌套函数定义
        print('T-minus %d' % n)
    while n > 0:
        display()
        n -= 1
```

嵌套函数中的变量使用*词法作用域*进行绑定。也就是说，名称的解析方式是首先检查本地作用域，然后从最内层到最外层依次检查所有外层函数定义的封闭作用域。如果没有找到匹配项，则照常检查全局和内置命名空间。虽然可以访问封闭作用域中的名称，但Python 2只允许在最内层作用域（局部变量）和全局命名空间（使用`global`）中重新赋值变量。因此，内部函数不能重新赋值外部函数中定义的局部变量的值。例如，以下代码不起作用：

```python
def countdown(start):
    n = start
    def display():
        print('T-minus %d' % n)
    def decrement():
        n -= 1           # 在Python 2中失败
    while n > 0:
        display()
        decrement()
```

在Python 2中，你可以通过将要更改的值放在列表或字典中来解决此问题。在Python 3中，你可以将`n`声明为`nonlocal`，如下所示：

```python
def countdown(start):
    n = start
    def display():
        print('T-minus %d' % n)
    def decrement():
        nonlocal n   # 绑定到外部的n（仅限Python 3）
        n -= 1
    while n > 0:
        display()
        decrement()
```

`nonlocal`声明不会将名称绑定到当前调用栈中更下方的任意函数内定义的局部变量（即*动态作用域*）。因此，如果你是从Perl转到Python，`nonlocal`与声明Perl的local变量并不相同。

如果在局部变量被赋值之前就使用了它，会引发`UnboundLocalError`异常。以下示例说明了这种情况可能发生的场景之一：

```python
i = 0
def foo():
    i = i + 1      # 导致UnboundLocalError异常
    print(i)
```

在此函数中，变量`i`被定义为局部变量（因为它在函数内部被赋值且没有`global`语句）。然而，赋值`i = i + 1`尝试在`i`的局部值首次赋值之前读取`i`的值。即使在此示例中存在全局变量`i`，也不会用它来提供值。变量在函数定义时就被确定为局部或全局，不会在函数执行中途突然改变作用域。例如，在前面的代码中，并不是表达式`i + 1`中的`i`引用全局变量`i`，而`print(i)`中的`i`引用前一条语句创建的局部变量`i`。

#### 函数作为对象和闭包

函数是Python中的一等对象。这意味着它们可以作为参数传递给其他函数，放入数据结构中，并由函数作为结果返回。以下是一个接受另一个函数作为输入并调用它的函数示例：

```python
###### foo.py
def callf(func):
    return func()
```

以下是使用上述函数的示例：

```python
>>> import foo
>>> def helloworld():
...     return 'Hello World'
...
>>> foo.callf(helloworld)    # 将函数作为参数传递
'Hello World'
>>>
```

当函数被作为数据处理时，它隐式地携带了与函数定义时周围环境相关的信息。这会影响函数中自由变量的绑定方式。例如，考虑以下修改版本的`foo.py`，其中现在包含一个变量定义：

```python
###### foo.py
x = 42
def callf(func):
    return func()
```

现在，观察此示例的行为：

```python
>>> import foo
>>> x = 37
>>> def helloworld():
...     return "Hello World. x is %d" % x
...
>>> foo.callf(helloworld)    # 将函数作为参数传递
'Hello World. x is 37'
>>>
```



#### 函数作为对象与闭包

在本例中，请注意函数 `helloworld()` 使用的是与其定义在相同环境中的 `x` 的值。因此，即使在 `foo.py` 中也定义了一个 `x`，且 `helloworld()` 实际上是在该文件中被调用的，但 `helloworld()` 执行时使用的并不是那个 `x` 的值。

当构成一个函数的语句与其执行环境打包在一起时，所得的对象称为*闭包*。前一个示例的行为可以这样解释：所有函数都有一个 `__globals__` 属性，该属性指向定义该函数时所在作用域的全局命名空间。这总是对应于定义该函数的封闭模块。对于前面的示例，你会得到以下结果：

```
>>> helloworld.__globals__
{'__builtins__': <module '__builtin__' (built-in)>,
 'helloworld': <function helloworld at 0x7bb30>,
 'x': 37, '__name__': '__main__', '__doc__': None
 'foo': <module 'foo' from 'foo.py'>}
>>>
```

当使用嵌套函数时，闭包会捕获内部函数执行所需的整个环境。以下是一个示例：

```
import foo

def bar():
    x = 13
    def helloworld():
        return "Hello World. x is %d" % x
    foo.callf(helloworld)      # returns 'Hello World, x is 13'
```

如果你想基于惰性求值或延迟求值的概念编写代码，闭包和嵌套函数尤其有用。这是另一个示例：

```
from urllib import urlopen
##### from urllib.request import urlopen (Python 3)
def page(url):
    def get():
        return urlopen(url).read()
    return get
```

在这个例子中，`page()` 函数实际上并没有执行任何有趣的计算。相反，它只是创建并返回一个函数 `get()`，该函数在被调用时将获取网页的内容。因此，`get()` 中执行的计算实际上被延迟到了程序后续的某个时间点，即 `get()` 被求值的时候。例如：

```
>>> python = page("http://www.python.org")
>>> jython = page("http://www.jython.org")
>>> python
<function get at 0x95d5f0>
>>> jython
<function get at 0x9735f0>
>>> pydata = python()       # Fetches http://www.python.org
>>> jydata = jython()       # Fetches http://www.jython.org
>>>
```

在这个例子中，两个变量 `python` 和 `jython` 实际上是 `get()` 函数的两个不同版本。即使创建这些值的 `page()` 函数不再执行，两个 `get()` 函数都隐式地携带了定义 `get()` 函数时外部变量的值。因此，当 `get()` 执行时，它使用的是最初提供给 `page()` 的 `url` 值来调用 `urlopen(url)`。稍加检查，你可以查看闭包中携带的变量内容。例如：

```
>>> python.__closure__
(<cell at 0x67f50: str object at 0x69230>,)
>>> python.__closure__[0].cell_contents
'http://www.python.org'
>>> jython.__closure__[0].cell_contents
'http://www.jython.org'
>>>
```

闭包可以成为在一系列函数调用间保存状态的高效方式。例如，考虑这段运行一个简单计数器的代码：

```
def countdown(n):
    def next():
        nonlocal n
        r = n
        n -= 1
        return r
    return next
```

```
##### Example use
next = countdown(10)
while True:
    v = next()      # Get the next value
    if not v: break
```

在这段代码中，一个闭包被用来存储内部计数器值 `n`。内部函数 `next()` 在每次被调用时更新并返回该计数器变量的先前值。不熟悉闭包的程序员可能会倾向于使用这样的类来实现类似的功能：

```
class Countdown(object):
    def __init__(self,n):
        self.n = n
    def next(self):
        r = self.n
        self.n -= 1
        return r
```

```
##### Example use
c = Countdown(10)
while True:
    v = c.next()     # Get the next value
    if not v: break
```

然而，如果你增加倒计数的起始值并进行简单的计时基准测试，你会发现使用闭包的版本运行得更快（在作者的机器上测试时，速度提升了近 50%）。

闭包捕获内部函数环境的特性也使其在需要包装现有函数以添加额外功能的应用中很有用。接下来将对此进行描述。

#### 装饰器

*装饰器*是一个主要目的是包装另一个函数或类的函数。这种包装的主要目的是透明地改变或增强被包装对象的行为。在语法上，装饰器使用特殊的 `@` 符号表示，如下所示：

```
@trace
def square(x):
    return x*x
```

上述代码是以下代码的简写：

```
def square(x):
    return x*x
square = trace(square)
```

在示例中，定义了一个函数 `square()`。然而，在定义之后，函数对象本身立即被传递给函数 `trace()`，该函数返回一个替换原始 `square` 的对象。现在，让我们考虑 `trace` 的一个实现，它将阐明这可能是有用的：

```
enable_tracing = True
if enable_tracing:
    debug_log = open("debug.log","w")

def trace(func):
    if enable_tracing:
        def callf(*args,**kwargs):
            debug_log.write("Calling %s: %s, %s\n" %
                (func.__name__, args, kwargs))
            r = func(*args,**kwargs)
            debug_log.write("%s returned %s\n" % (func.__name__, r))
            return r
        return callf
    else:
        return func
```

在这段代码中，`trace()` 创建了一个包装函数，该函数写入一些调试输出，然后调用原始函数对象。因此，如果你调用 `square()`，你会看到包装器中 `write()` 方法的输出。从 `trace()` 返回的函数 `callf` 是一个闭包，它作为原始函数的替代品。该实现最后有趣的一点是，跟踪功能本身仅通过使用如图所示的全局变量 `enable_tracing` 来启用。如果设置为 `False`，`trace()` 装饰器将简单地返回未修改的原始函数。因此，当跟踪被禁用时，使用装饰器不会带来额外的性能开销。

使用装饰器时，它们必须单独出现在函数或类定义之前的行上。也可以应用多个装饰器。这是一个示例：

```
@foo
@bar
@spam
def grok(x):
    pass
```

在这种情况下，装饰器按列出的顺序应用。结果与以下相同：

```
def grok(x):
    pass
grok = foo(bar(spam(grok)))
```

装饰器也可以接受参数。这是一个示例：

```
@eventhandler('BUTTON')
def handle_button(msg):
    ...
@eventhandler('RESET')
def handle_reset(msg):
    ...
```

如果提供了参数，装饰器的语义如下：

```
def handle_button(msg):
    ...
temp = eventhandler('BUTTON')       # Call decorator with supplied arguments
handle_button = temp(handle_button) # Call the function returned by the decorator
```

在这种情况下，装饰器函数只接受与 @ 说明符一起提供的参数。然后返回一个函数，该函数以函数作为参数被调用。这是一个示例：

```
##### Event handler decorator
event_handlers = { }
def eventhandler(event):
    def register_function(f):
        event_handlers[event] = f
        return f
    return register_function
```

装饰器也可以应用于类定义。例如：

```
@foo
class Bar(object):
    def __init__(self,x):
        self.x = x
    def spam(self):
        statements
```

对于类装饰器，你应始终让装饰器函数返回一个类对象作为结果。期望使用原始类定义的代码可能希望直接引用类的成员，例如 Bar.spam。如果装饰器函数 `foo()` 返回一个函数，这将无法正常工作。

装饰器可能与函数的其他方面（如递归、文档字符串和函数属性）奇怪地交互。这些问题将在本章后面描述。

#### 生成器与 yield

如果一个函数使用了 yield 关键字，它就定义了一个称为生成器的对象。生成器是一个产生一系列值以用于迭代的函数。这是一个示例：

```python
def countdown(n):
    print("Counting down from %d" % n)
    while n > 0:
        yield n
        n -= 1
    return
```

如果你调用这个函数，你会发现它的代码并没有开始执行。例如：

```python
>>> c = countdown(10)
>>>
```

相反，它返回了一个生成器对象。生成器对象会在每次调用 `next()`（或在 Python 3 中调用 `__next__()`）时执行该函数。下面是一个例子：

```python
>>> c.next()           # 在 Python 3 中使用 c.__next__()
Counting down from 10
10
>>> c.next()
9
```

当调用 `next()` 时，生成器函数会执行语句，直到遇到 `yield` 语句。`yield` 语句会产生一个结果，此时函数的执行暂停，直到再次调用 `next()`。然后执行将从 `yield` 之后的语句继续。

通常你不会直接在生成器上调用 `next()`，而是将其与 `for` 语句、`sum()` 或其他消耗序列的操作一起使用。例如：

```python
for n in countdown(10):
    statements
a = sum(countdown(10))
```

生成器函数通过返回或引发 `StopIteration` 来表示完成，此时迭代停止。生成器完成时返回除 `None` 以外的值是非法的。

生成器的一个微妙问题涉及生成器函数只被部分消费的情况。例如，考虑以下代码：

```python
for n in countdown(10):
    if n == 2: break
    statements
```

在这个例子中，`for` 循环通过调用 `break` 中止，相关的生成器从未完全运行完毕。为了处理这种情况，生成器对象有一个 `close()` 方法，用于发出关闭信号。当生成器不再使用或被删除时，会调用 `close()`。通常不需要调用 `close()`，但你也可以像这里展示的那样手动调用它：

```python
>>> c = countdown(10)
>>> c.next()
Counting down from 10
10
>>> c.next()
9
>>> c.close()
>>> c.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>>
```

在生成器函数内部，`close()` 通过在 `yield` 语句上引发 `GeneratorExit` 异常来发出信号。你可以选择捕获此异常以执行清理操作。

```python
def countdown(n):
    print("Counting down from %d" % n)
    try:
        while n > 0:
            yield n
            n = n - 1
    except GeneratorExit:
        print("Only made it to %d" % n)
```

虽然可以捕获 `GeneratorExit`，但生成器函数处理该异常并使用 `yield` 产生另一个输出值是非法的。此外，如果一个程序当前正在迭代生成器，你不应该从单独的执行线程或信号处理程序异步调用 `close()`。

#### 协程和 `yield` 表达式

在函数内部，`yield` 语句也可以用作出现在赋值运算符右侧的表达式。例如：

```python
def receiver():
    print("Ready to receive")
    while True:
        n = (yield)
        print("Got %s" % n)
```

以这种方式使用 `yield` 的函数称为*协程*，它在向其发送值时执行。它的行为也非常类似于生成器。例如：

```python
>>> r = receiver()
>>> r.next()  # 前进到第一个 yield（在 Python 3 中使用 r.__next__()）
Ready to receive
>>> r.send(1)
Got 1
>>> r.send(2)
Got 2
>>> r.send("Hello")
Got Hello
>>>
```

在这个例子中，最初调用 `next()` 是必要的，这样协程才会执行语句直到第一个 `yield` 表达式。此时，协程暂停，等待使用关联的生成器对象 `r` 的 `send()` 方法发送值。传递给 `send()` 的值由协程中的 `(yield)` 表达式返回。接收到值后，协程执行语句直到遇到下一个 `yield` 语句。

首先在协程上调用 `next()` 的要求很容易被忽视，并且是错误的常见来源。因此，建议用装饰器包装协程，该装饰器自动处理这一步。

```python
def coroutine(func):
    def start(*args,**kwargs):
        g = func(*args,**kwargs)
        g.next()
        return g
    return start
```

使用此装饰器，你可以这样编写和使用协程：

```python
@coroutine
def receiver():
    print("Ready to receive")
    while True:
        n = (yield)
        print("Got %s" % n)
###### 示例用法
r = receiver()
r.send("Hello World")      # 注意：不需要初始的 .next()
```

协程通常会无限期地运行，除非它被显式关闭或自行退出。要关闭输入值流，请使用 `close()` 方法，如下所示：

```python
>>> r.close()
>>> r.send(4)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

一旦关闭，如果向协程发送更多值，将引发 `StopIteration` 异常。`close()` 操作在协程内部引发 `GeneratorExit`，如前一节关于生成器所述。例如：

```python
def receiver():
    print("Ready to receive")
    try:
        while True:
            n = (yield)
            print("Got %s" % n)
    except GeneratorExit:
        print("Receiver done")
```

可以使用 `throw(exctype [, value [, tb]])` 方法在协程内部引发异常，其中 `exctype` 是异常类型，`value` 是异常值，`tb` 是回溯对象。例如：

```python
>>> r.throw(RuntimeError,"You're hosed!")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 4, in receiver
RuntimeError: You're hosed!
```

以这种方式引发的异常将源于协程中当前执行的 `yield` 语句。协程可以选择捕获异常并进行适当处理。将 `throw()` 用作协程的异步信号是不安全的——永远不应从单独的执行线程或在信号处理程序中调用它。

如果值在 `yield` 表达式中提供，协程可以同时接收和发射返回值。下面是一个说明这一点的例子：

```python
def line_splitter(delimiter=None):
    print("Ready to split")
    result = None
    while True:
        line = (yield result)
        result = line.split(delimiter)
```

在这种情况下，我们使用协程的方式与之前相同。然而，现在调用 `send()` 也会产生一个结果。例如：

```python
>>> s = line_splitter(",")
>>> s.next()
Ready to split
>>> s.send("A,B,C")
['A', 'B', 'C']
>>> s.send("100,200,300")
['100', '200', '300']
>>>
```

理解这个例子的顺序至关重要。第一个 `next()` 调用将协程推进到 `(yield result)`，它返回 `None`，即 `result` 的初始值。在后续的 `send()` 调用中，接收到的值被放入 `line` 并分割到 `result` 中。`send()` 返回的值是传递给遇到的下一个 `yield` 语句的值。换句话说，`send()` 返回的值来自下一个 `yield` 表达式，而不是负责接收 `send()` 传递的值的那个。

如果协程返回值，在使用 `throw()` 引发异常时需要小心。如果你使用 `throw()` 在协程中引发异常，传递给协程中下一个 `yield` 的值将作为 `throw()` 的结果返回。如果你需要这个值并且忘记保存它，它将会丢失。

#### 使用生成器和协程

乍一看，可能不太清楚如何将生成器和协程用于实际问题。然而，当应用于系统、网络和分布式计算中的某些编程问题时，生成器和协程特别有效。例如，如果你想设置一个处理管道（类似于在 UNIX shell 中使用管道），生成器函数很有用。这的一个例子出现在引言中。这里是另一个涉及一组与查找、打开、读取和处理文件相关的生成器函数的例子：

```python
import os
import fnmatch

def find_files(topdir, pattern):
    for path, dirname, filelist in os.walk(topdir):
        for name in filelist:
            if fnmatch.fnmatch(name, pattern):
                yield os.path.join(path,name)

import gzip, bz2
def opener(filenames):
    for name in filenames:
        if name.endswith(".gz"):  f = gzip.open(name)
        elif name.endswith(".bz2"): f = bz2.BZ2File(name)
        else: f = open(name)
        yield f

def cat(filelist):
    for f in filelist:
        for line in f:
            yield line

def grep(pattern, lines):
    for line in lines:
        if pattern in line:
            yield line
```



下面是一个使用这些函数来设置处理流程的示例：

```
wwwlogs = find("www","access-log*")
files  = opener(wwwlogs)
lines  = cat(files)
pylines = grep("python", lines)
for line in pylines:
    sys.stdout.write(line)
```

在这个示例中，程序正在处理顶级目录 `"www"` 所有子目录中找到的所有 `access-log*` 文件中的所有行。每个 `access-log` 文件都会被测试是否压缩，并使用相应的文件打开器打开。这些行被连接在一起，并通过一个过滤器处理，该过滤器查找子字符串 `"python"`。整个程序由最后的 `for` 语句驱动。该循环的每次迭代都会从流程中拉取一个新值并消耗它。此外，该实现内存效率极高，因为从未创建过临时列表或其他大型数据结构。

协程可用于编写基于数据流处理的程序。以这种方式组织的程序看起来像倒置的管道。你不是使用 for 循环通过一系列生成器函数拉取值，而是将值发送到一组链接的协程中。下面是一个协程函数的示例，这些函数被编写用来模拟之前显示的生成器函数：

```
import os
import fnmatch

@coroutine
def find_files(target):
    while True:
        topdir, pattern = (yield)
        for path, dirname, filelist in os.walk(topdir):
            for name in filelist:
                if fnmatch.fnmatch(name,pattern):
                    target.send(os.path.join(path,name))

import gzip, bz2
@coroutine
def opener(target):
    while True:
        name = (yield)
        if name.endswith(".gz"):  f = gzip.open(name)
        elif name.endswith(".bz2"): f = bz2.BZ2File(name)
        else: f = open(name)
        target.send(f)

@coroutine
def cat(target):
    while True:
        f = (yield)
        for line in f:
            target.send(line)
```

```
@coroutine
def grep(pattern, target):
    while True:
        line = (yield)
        if pattern in line:
            target.send(line)

@coroutine
def printer():
    while True:
        line = (yield)
        sys.stdout.write(line)
```

下面是如何将这些协程链接起来以创建数据流处理管道：

```
finder = find_files(opener(cat(grep("python",printer()))))

##### Now, send a value
finder.send(("www","access-log*"))
finder.send(("otherwww","access-log*"))
```

在这个示例中，每个协程都将数据发送到另一个协程，该协程在每个协程的 `target` 参数中指定。与生成器示例不同，执行完全由将数据推送到第一个协程 `find_files()` 驱动。该协程继而将数据推送到下一个阶段。此示例的一个关键方面是，协程管道会无限期保持活动状态，直到对其显式调用 `close()`。因此，程序可以在必要时持续向协程馈送数据——例如，示例中显示的对 `send()` 的两次重复调用。

协程可用于实现一种形式的并发。例如，一个集中的任务管理器或事件循环可以调度并将数据发送到由数百甚至数千个协程组成的集合中，这些协程执行各种处理任务。输入数据被“发送”到协程这一事实也意味着协程通常可以轻松地与使用消息队列和消息传递在程序组件之间进行通信的程序混合使用。有关此内容的更多信息，请参见第 20 章“线程”。

#### 列表推导式

涉及函数的一个常见操作是将函数应用于列表的所有项，创建一个包含结果的新列表。例如：

```
nums = [1, 2, 3, 4, 5]
squares = []
for n in nums:
    squares.append(n * n)
```

由于此类操作非常普遍，它已被转换为称为列表推导式的运算符。下面是一个简单的示例：

```
nums = [1, 2, 3, 4, 5]
squares = [n * n for n in nums]
```

列表推导式的通用语法如下：

```
[expression for item1 in iterable1 if condition1
            for item2 in iterable2 if condition2
            ...
            for itemN in iterableN if conditionN ]
```

此语法大致等效于以下代码：

```
s = []
for item1 in iterable1:
    if condition1:
        for item2 in iterable2:
            if condition2:
                ...
                for itemN in iterableN:
                    if conditionN: s.append(expression)
```

为了说明，这里有一些更多的示例：

```
a = [-3,5,2,-10,7,8]
b = 'abc'

c = [2*s for s in a]              # c = [-6,10,4,-20,14,16]
d = [s for s in a if s >= 0]     # d = [5,2,7,8]
e = [(x,y) for x in a             # e = [(5,'a'),(5,'b'),(5,'c'),
           for y in b             #     (2,'a'),(2,'b'),(2,'c'),
           if x > 0 ]             #     (7,'a'),(7,'b'),(7,'c'),
                                 #     (8,'a'),(8,'b'),(8,'c')]

f = [(1,2), (3,4), (5,6)]
g = [math.sqrt(x*x+y*y)          # g = [2.23606, 5.0, 7.81024]
     for x,y in f]
```

提供给列表推导式的序列长度不必相同，因为它们是通过嵌套的 for 循环（如前所示）遍历其内容的。生成的列表包含表达式的连续值。`if` 子句是可选的；但是，如果使用它，则仅当 `condition` 为真时才会评估 `expression` 并将其添加到结果中。

如果使用列表推导式来构建元组列表，则元组值必须用括号括起来。例如，`[(x,y) for x in a for y in b]` 是合法语法，而 `[x,y for x in a for y in b]` 则不是。

最后，需要注意的是，在 Python 2 中，列表推导式内定义的迭代变量在当前作用域内进行评估，并在列表推导式执行后保持定义。例如，在 `[x for x in a]` 中，迭代变量 `x` 覆盖任何先前定义的 `x` 值，并在创建生成的列表后设置为 `a` 中最后一项的值。幸运的是，在 Python 3 中并非如此，迭代变量保持私有。

##### 生成器表达式

生成器表达式是一个对象，它执行与列表推导式相同的计算，但迭代地产生结果。语法与列表推导式相同，只是使用圆括号而不是方括号。下面是一个示例：

```
(expression for item1 in iterable1 if condition1
            for item2 in iterable2 if condition2
            ...
            for itemN in iterableN if conditionN)
```

与列表推导式不同，生成器表达式实际上并不创建列表或立即评估圆括号内的表达式。相反，它创建一个生成器对象，通过迭代按需产生值。下面是一个示例：

```
>>> a = [1, 2, 3, 4]
>>> b = (10*i for i in a)
>>> b
<generator object at 0x590a8>
>>> b.next()
10
>>> b.next()
20
...
```

列表和生成器表达式之间的区别很重要，但很微妙。使用列表推导式时，Python 实际上会创建一个包含结果数据的列表。使用生成器表达式时，Python 创建一个仅知道如何按需产生数据的生成器。在某些应用程序中，这可以大大提高性能和内存使用率。下面是一个示例：

```
##### Read a file
f = open("data.txt")                  # Open a file
lines = (t.strip() for t in f)      # Read lines, strip
                                     # trailing/leading whitespace
comments = (t for t in lines if t[0] == '#') # All comments
for c in comments:
    print(c)
```

在这个示例中，提取行并去除空格的生成器表达式实际上并未将整个文件读入内存。提取注释的表达式也是如此。相反，文件的行实际上是在程序开始在后续的 `for` 循环中进行迭代时读取的。在此迭代过程中，文件的行是按需产生并相应过滤的。事实上，在此过程中任何时候都不会将整个文件加载到内存中。因此，这将是从 GB 大小的 Python 源文件中提取注释的高效方法。

与列表推导式不同，生成器表达式不会创建像序列一样工作的对象。它不能被索引，并且通常的列表操作都不起作用（例如 `append()`）。但是，可以使用内置的 `list()` 函数将生成器表达式转换为列表：

```
clist = list(comments)
```

# ## 声明式编程

列表推导式和生成器表达式与声明式语言中发现的操作密切相关。事实上，这些功能的起源大致源于数学集合论的思想。例如，当你编写像 `[x*x for x in a if x > 0]` 这样的语句时，它类似于指定一个集合，如 { x² | x∈a, x > 0 }。

你可以使用这些声明性功能将程序结构化为一系列计算，这些计算仅对所有数据一次性进行操作，而不是编写手动迭代数据的程序。例如，假设你有一个文件 "portfolio.txt"，其中包含如下所示的股票投资组合数据：



```
AA 100 32.20
IBM 50 91.10
CAT 150 83.44
MSFT 200 51.23
GE 95 40.37
MSFT 50 65.10
IBM 100 70.44
```

这是一个声明式风格的程序，通过将第二列与第三列相乘并求和来计算总成本：

```python
lines = open("portfolio.txt")
fields = (line.split() for line in lines)
print(sum(float(f[1]) * float(f[2]) for f in fields))
```

在这个程序中，我们并不真正关心逐行遍历文件的机制。相反，我们只是声明了一系列对所有数据执行的计算。这种方法不仅使代码高度紧凑，而且往往比这个更传统的版本运行得更快：

```python
total = 0
for line in open("portfolio.txt"):
    fields = line.split()
    total += float(fields[1]) * float(fields[2])
print(total)
```

声明式编程风格与程序员可能在UNIX shell中执行的操作类型有一定关联。例如，前面使用生成器表达式的例子与下面这个一行的awk命令类似：

```bash
% awk '{ total += $2 * $3} END { print total }' portfolio.txt
44671.2
%
```

列表推导式和生成器表达式的声明式风格也可用于模拟SQL select语句的行为，这在处理数据库时很常见。例如，考虑以下作用于以字典列表形式读取的数据的示例：

```python
fields = (line.split() for line in open("portfolio.txt"))
portfolio = [ {'name' : f[0],
               'shares' : int(f[1]),
               'price' : float(f[2]) }
              for f in fields]
```

```python
##### Some queries
msft = [s for s in portfolio if s['name'] == 'MSFT']
large_holdings = [s for s in portfolio
                       if s['shares']*s['price'] >= 10000]
```

事实上，如果你使用与数据库访问相关的模块（参见第17章），你通常可以一次性结合使用列表推导式和数据库查询。例如：

```python
sum(shares*cost for shares,cost in
        cursor.execute("select shares, cost from portfolio")
        if shares*cost >= 10000)
```

#### `lambda` 操作符

可以使用 `lambda` 语句创建表达式形式的匿名函数：

```
lambda args : expression
```

`args` 是逗号分隔的参数列表，而 *expression* 是涉及这些参数的表达式。下面是一个例子：

```python
a = lambda x,y : x+y
r = a(2,3)         # r gets 5
```

用 `lambda` 定义的代码必须是一个有效的表达式。多个语句和其他非表达式语句，如 `for` 和 `while`，不能出现在 `lambda` 语句中。`lambda` 表达式遵循与函数相同的作用域规则。

`lambda` 的主要用途是用于指定简短的回调函数。例如，如果你想对一个名称列表进行不区分大小写的排序，你可能会这样写：

```python
names.sort(key=lambda n: n.lower())
```

#### 递归

递归函数很容易定义。例如：

```python
def factorial(n):
    if n <= 1: return 1
    else: return n * factorial(n - 1)
```

但是，请注意递归函数调用的深度是有限制的。函数 `sys.getrecursionlimit()` 返回当前的最大递归深度，函数 `sys.setrecursionlimit()` 可用于更改该值。默认值是 `1000`。虽然可以增加该值，但程序仍然受到主机操作系统强制的栈大小限制。当递归深度超过限制时，会引发 `RuntimeError` 异常。Python 不执行在 Scheme 等函数式语言中常见的尾递归优化。

递归在生成器函数和协程中的表现并不如你可能预期的那样。例如，以下代码打印嵌套列表集合中的所有项：

```python
def flatten(lists):
    for s in lists:
        if isinstance(s,list):
            flatten(s)
        else:
            print(s)
```

```python
items = [[1,2,3],[4,5,[5,6]],[7,8,9]
flatten(items)    # Prints 1 2 3 4 5 6 7 8 9
```

但是，如果你将 `print` 操作改为 `yield`，它将不再工作。这是因为对 `flatten()` 的递归调用只是创建了一个新的生成器对象，而没有实际迭代它。以下是一个有效的递归生成器版本：

```python
def genflatten(lists):
    for s in lists:
        if isinstance(s,list):
            for item in genflatten(s):
                yield item
        else:
            yield item
```

在混合使用递归函数和装饰器时也应小心。如果将装饰器应用于递归函数，所有内部递归调用现在都会通过装饰后的版本进行路由。例如：

```python
@locked
def factorial(n):
    if n <= 1: return 1
    else: return n * factorial(n - 1)  # Calls the wrapped version of factorial
```

如果装饰器的目的与某种系统管理（如同步或锁）相关，那么最好避免递归。

##### 文档字符串

函数的第一条语句通常是描述其用法的文档字符串，这是一种常见的做法。例如：

```python
def factorial(n):
    """Computes n factorial. For example:

        >>> factorial(6)
        120
        >>>
    """
    if n <= 1: return 1
    else: return n*factorial(n-1)
```

文档字符串存储在函数的 `__doc__` 属性中，IDE通常使用该属性来提供交互式帮助。

如果你使用装饰器，请注意用装饰器包装函数可能会破坏与文档字符串相关的帮助功能。例如，考虑以下代码：

```python
def wrap(func):
    call(*args,**kwargs):
        return func(*args,**kwargs)
    return call
@wrap
def factorial(n):
    """Computes n factorial."""
    ...
```

如果用户请求此版本 `factorial()` 的帮助，他将得到一个相当晦涩的解释：

```python
>>> help(factorial)
Help on function call in module __main__:

call(*args, **kwargs)
(END)
>>>
```

要修复此问题，请编写装饰器函数，使其传播函数名和文档字符串。例如：

```python
def wrap(func):
    call(*args,**kwargs):
        return func(*args,**kwargs)
    call.__doc__ = func.__doc__
    call.__name__ = func.__name__
    return call
```

因为这是一个常见问题，`functools` 模块提供了一个函数 `wraps`，可以自动复制这些属性。毫不奇怪，它本身也是一个装饰器：

```python
from functools import wraps
def wrap(func):
    @wraps(func)
    call(*args,**kwargs):
        return func(*args,**kwargs)
    return call
```

在 `functools` 中定义的 `@wraps(func)` 装饰器将属性从 `func` 传播到正在定义的包装函数。

#### 函数属性

函数可以附加任意属性。下面是一个例子：

```python
def foo():
    statements

foo.secure = 1
foo.private = 1
```

函数属性的主要用途是在高度专业化的应用程序中，例如解析器生成器和应用程序框架，它们希望将附加信息附加到函数对象上。

与文档字符串一样，在混合使用函数属性和装饰器时应小心。如果函数被装饰器包装，对属性的访问实际上将发生在装饰器函数上，而不是原始实现上。这可能符合也可能不符合你的要求，具体取决于应用程序。要将已定义的函数属性传播到装饰器函数，请使用以下模板或上一节所示的 `functools.wraps()` 装饰器：

```python
def wrap(func):
    call(*args,**kwargs):
        return func(*args,**kwargs)
    call.__doc__ = func.__doc__
    call.__name__ = func.__name__
    call.__dict__.update(func.__dict__)
    return call
```

#### eval()、exec() 和 compile()

`eval(str [,globals [,locals]])` 函数执行一个表达式字符串并返回结果。下面是一个例子：

```python
a = eval('3*math.sin(3.5+x) + 7.2')
```

类似地，`exec(str [, globals [, locals]])` 函数执行一个包含任意Python代码的字符串。提供给 `exec()` 的代码被执行，就像代码实际出现在 `exec` 操作的位置一样。下面是一个例子：

```python
a = [3, 5, 10, 13]
exec("for i in a: print(i)")
```

关于 `exec` 的一个注意事项是，在Python 2中，`exec` 实际上被定义为一个语句。因此，在旧代码中，你可能会看到调用 `exec` 的语句没有周围的圆括号，例如 `exec "for i in a: print i"`。虽然这在Python 2.6中仍然有效，但在Python 3中会中断。现代程序应该使用 `exec()` 作为函数。

这两个函数都在调用者的命名空间中执行（用于解析字符串或文件中出现的符号）。可选地，`eval()` 和 `exec()` 可以接受一个或两个映射对象，分别作为要执行的代码的全局和本地命名空间。下面是一个例子：

```python
globals = {'x': 7,
           'y': 10,
           'birds': ['Parrot', 'Swallow', 'Albatross']
           }
locals = {}
```

```python
##### Execute using the above dictionaries as the global and local namespace
a = eval("3 * x + 4 * y", globals, locals)
exec("for b in birds: print(b)", globals, locals)
```

如果你省略一个或两个命名空间，将使用全局和本地命名空间的当前值。此外，由于与嵌套作用域相关的问题，在函数体内使用 `exec()` 可能会导致 `SyntaxError` 异常，如果该函数还包含嵌套函数定义或使用 `lambda` 操作符。

当字符串传递给 `exec()` 或 `eval()` 时，解析器首先将其编译为字节码。因为这个过程开销很大，如果代码将被多次执行，最好预编译代码并在后续调用中重用字节码。

`compile(str, filename, kind)` 函数将字符串编译为字节码，其中 `str` 是包含要编译代码的字符串，`filename` 是定义该字符串的文件（用于回溯生成）。`kind` 参数指定正在编译的代码类型——`'single'` 表示单条语句，`'exec'` 表示一组语句，或 `'eval'` 表示一个表达式。`compile()` 函数返回的代码对象也可以传递给 `eval()` 函数和 `exec()` 语句。下面是一个例子：

```python
s = "for i in range(0,10): print(i)"
c = compile(s,'','exec')    # Compile into a code object
exec(c)                        # Execute it

s2 = "3 * x + 4 * y"
c2 = compile(s2, '', 'eval')  # Compile into an expression
result = eval(c2)              # Execute it
```



## 7

## 类与面向对象编程

类是用于创建新型对象的机制。本章详细介绍类，但并非旨在成为面向对象编程和设计的深入参考。假定读者对其他语言（如 C 或 Java）中的数据结构和面向对象编程具有一定的先验经验。（第 3 章“类型与对象”包含了关于对象术语和内部实现的更多信息。）

#### class 语句

*类* 定义了一组与称为 *实例* 的对象集合相关联并共享的属性。类最常见的是函数（称为 *方法*）、变量（称为 *类变量*）和计算属性（称为 *属性*）的集合。

类使用 `class` 语句定义。类的主体包含一系列在类定义期间执行的语句。以下是一个示例：

```
class Account(object):
    num_accounts = 0
    def __init__(self,name,balance):
        self.name = name
        self.balance = balance
        Account.num_accounts += 1
    def __del__(self):
        Account.num_accounts -= 1
    def deposit(self,amt):
        self.balance = self.balance + amt
    def withdraw(self,amt):
        self.balance = self.balance - amt
    def inquiry(self):
        return self.balance
```

在类主体执行期间创建的值被放入一个类对象中，该对象作为命名空间，非常类似于模块。例如，`Account` 类的成员可以按如下方式访问：

```
Account.num_accounts
Account.__init__
Account.__del__
Account.deposit
Account.withdraw
Account.inquiry
```

需要注意的是，`class` 语句本身并不创建类的任何实例（例如，在前面的示例中，实际上没有创建任何账户）。相反，类只是为稍后创建的所有实例将具有的公共属性做准备。从这个意义上说，可以将其视为蓝图。

在类内部定义的函数称为 *实例方法*。实例方法是在类的实例上操作的函数，该实例作为第一个参数传递。按照惯例，此参数称为 `self`，尽管可以使用任何合法的标识符名称。在前面的示例中，`deposit()`、`withdraw()` 和 `inquiry()` 是实例方法的示例。

类变量（如 `num_accounts`）是在类的所有实例之间共享的值（即，它们不是单独分配给每个实例的）。在这种情况下，它是一个跟踪存在多少个 Account 实例的变量。

#### 类实例

类的实例是通过像函数一样调用类对象来创建的。这会创建一个新实例，然后将其传递给类的 `__init__()` 方法。`__init__()` 的参数包括新创建的实例 `self` 以及调用类对象时提供的参数。例如：

```
##### 创建几个账户
a = Account("Guido", 1000.00)  # 调用 Account.__init__(a,"Guido",1000.00)
b = Account("Bill", 10.00)
```

在 `__init__()` 内部，通过赋值给 `self` 将属性保存在实例中。例如，`self.name = name` 是在实例中保存 `name` 属性。一旦新创建的实例返回给用户，这些属性以及类的属性就可以使用点（.）运算符按如下方式访问：

```
a.deposit(100.00)      # 调用 Account.deposit(a,100.00)
b.withdraw(50.00)      # 调用 Account.withdraw(b,50.00)
name = a.name          # 获取账户名称
```

点（.）运算符负责属性绑定。当你访问一个属性时，结果值可能来自几个不同的地方。例如，前面示例中的 `a.name` 返回实例 `a` 的 `name` 属性。然而，`a.deposit` 返回 `Account` 类的 `deposit` 属性（一个方法）。当你访问一个属性时，首先检查实例，如果找不到，则搜索转移到实例的类。这是类与其所有实例共享属性的底层机制。

#### 作用域规则

尽管类定义了命名空间，但类并不会为方法主体中使用的名称创建作用域。因此，当你实现类时，对属性和方法的引用必须是完全限定的。例如，在方法中，你总是通过 `self` 引用实例的属性。因此，在示例中，你使用 `self.balance`，而不是 `balance`。如果你想从一个方法调用另一个方法，这也适用，如以下示例所示：

```
class Foo(object):
    def bar(self):
        print("bar!")
    def spam(self):
        bar(self)    # 错误！'bar' 会产生 NameError
        self.bar()   # 这是可行的
        Foo.bar(self) # 这也是可行的
```

类中缺乏作用域是 Python 与 C++ 或 Java 不同的一个方面。如果你使用过这些语言，Python 中的 `self` 参数与 C++ 中的 `this` 指针相同。需要显式使用 `self`，因为 Python 不提供显式声明变量的方法（即，像 C 中的 `int x` 或 `float y` 这样的声明）。如果没有这个，就无法知道方法中对变量的赋值是局部变量，还是应该保存为实例属性。显式使用 `self` 解决了这个问题——存储在 `self` 上的所有值都是实例的一部分，所有其他赋值只是局部变量。

#### 继承

*继承* 是一种创建新类的机制，新类可以特化或修改现有类的行为。原始类称为 *基类* 或 *超类*。新类称为 *派生类* 或 *子类*。当通过继承创建一个类时，它会“继承”其基类定义的属性。但是，派生类可以重新定义这些属性中的任何一个，并添加自己的新属性。

继承通过在 `class` 语句中指定以逗号分隔的基类名称列表来指定。如果没有逻辑基类，类将从 `object` 继承，如前面的示例所示。`object` 是一个类，它是所有 Python 对象的根，并提供一些公共方法的默认实现，例如 `__str__()`，它创建一个用于打印的字符串。

继承通常用于重新定义现有方法的行为。例如，这是一个特化的 `Account` 版本，它重新定义了 `inquiry()` 方法，定期虚报当前余额，希望那些没有密切关注的人会透支账户并在支付次级抵押贷款时产生巨额罚款：

```
import random
class EvilAccount(Account):
    def inquiry(self):
        if random.randint(0,4) == 1:
            return self.balance * 1.10  # 注意：专利待批的想法
        else:
            return self.balance

c = EvilAccount("George", 1000.00)
c.deposit(10.0)         # 调用 Account.deposit(c,10.0)
available = c.inquiry() # 调用 EvilAccount.inquiry(c)
```

在此示例中，`EvilAccount` 的实例与 `Account` 的实例完全相同，除了重新定义的 `inquiry()` 方法。

继承仅通过点（.）运算符的轻微增强来实现。具体来说，如果对属性的搜索在实例或实例的类中没有找到匹配项，则搜索将转移到基类。此过程一直持续到没有更多基类可供搜索。在前面的示例中，这解释了为什么 `c.deposit()` 调用在 `Account` 类中定义的 `deposit()` 实现。

子类可以通过定义自己的 `__init__()` 版本向实例添加新属性。例如，这个版本的 `EvilAccount` 添加了一个新属性 `evilfactor`：

```
class EvilAccount(Account):
    def __init__(self,name,balance,evilfactor):
        Account.__init__(self,name,balance)     # 初始化 Account
        self.evilfactor = evilfactor
    def inquiry(self):
        if random.randint(0,4) == 1:
            return self.balance * self.evilfactor
        else:
            return self.balance
```

当派生类定义 `__init__()` 时，基类的 `__init__()` 方法不会自动调用。因此，派生类需要通过调用基类的 `__init__()` 方法来执行适当的初始化。在前面的示例中，这在调用 `Account.__init__()` 的语句中显示。如果基类没有定义 `__init__()`，则可以省略此步骤。如果你不知道基类是否定义了 `__init__()`，始终安全地调用它而不带任何参数，因为总是有一个默认实现，它什么都不做。

有时，派生类会重新实现一个方法，但也想调用原始实现。为此，方法可以显式调用基类中的原始方法，将实例 `self` 作为第一个参数传递，如下所示：

```
class MoreEvilAccount(EvilAccount):
    def deposit(self,amount):
        self.withdraw(5.00)                 # 减去“便利”费用
        EvilAccount.deposit(self,amount)    # 现在，进行存款
```

此示例中的一个细微之处是，`EvilAccount` 类实际上并没有实现 `deposit()` 方法。相反，它是在 `Account` 类中实现的。虽然这段代码可以工作，但对于阅读代码的人来说可能会感到困惑（例如，`EvilAccount` 应该实现 `deposit()` 吗？）。因此，另一种解决方案是使用 `super()` 函数，如下所示：

```
class MoreEvilAccount(EvilAccount):
    def deposit(self,amount):
        self.withdraw(5.00)                        # 减去便利费用
        super(MoreEvilAccount,self).deposit(amount)  # 现在，进行存款
```

`super(cls, instance)` 返回一个特殊对象，允许你对基类执行属性查找。如果你使用它，Python 将使用通常用于基类的正常搜索规则来搜索属性。这使你无需硬编码方法的确切位置，并更清楚地表明你的意图（即，你想调用先前的实现，而不考虑哪个基类定义了它）。不幸的是，`super()` 的语法还有许多不足之处。如果你使用 Python 3，你可以使用简化的语句 `super().deposit(amount)` 来执行示例中的计算。但是，在 Python 2 中，你必须使用更冗长的版本。

Python 支持多重继承。这是通过一个类列出多个基类来指定的。例如，这里是一组类：



class DepositCharge(object):
    fee = 5.00
    def deposit_fee(self):
        self.withdraw(self.fee)

class WithdrawCharge(object):
    fee = 2.50
    def withdraw_fee(self):
        self.withdraw(self.fee)

##### 使用多重继承的类
class MostEvilAccount(EvilAccount, DepositCharge, WithdrawCharge):
    def deposit(self,amt):
        self.deposit_fee()
        super(MostEvilAccount,self).deposit(amt)
    def withdraw(self,amt):
        self.withdraw_fee()
        super(MostEvilAccount,self).withdraw(amt)

当使用多重继承时，属性解析会变得相当复杂，因为有许多可能的搜索路径可用于绑定属性。为了说明这种可能的复杂性，请看以下语句：

```python
d = MostEvilAccount("Dave",500.00,1.10)
d.deposit_fee()   # 调用 DepositCharge.deposit_fee()。费用是 5.00
d.withdraw_fee()  # 调用 WithdrawCharge.withdraw_fee()。费用是 5.00 ??
```

在这个例子中，`deposit_fee()` 和 `withdraw_fee()` 等方法具有唯一的名称，并在各自的基类中被找到。然而，`withdraw_fee()` 函数似乎工作不正常，因为它实际上并未使用在其自身类中初始化的 `fee` 值。实际情况是，属性 `fee` 是一个在两个不同基类中定义的类变量。其中一个值被使用了，但用的是哪个？（提示：是 `DepositCharge.fee`。）

在多重继承中查找属性时，所有基类会按照从“最特化”类到“最不特化”类的顺序排列在一个列表中。然后，在搜索属性时，会按顺序搜索此列表，直到找到属性的第一个定义。在这个例子中，`EvilAccount` 类比 `Account` 类更特化，因为它继承自 `Account`。同样，在 `MostEvilAccount` 内部，`DepositCharge` 被认为比 `WithdrawCharge` 更特化，因为它在基类列表中列在前面。对于任何给定的类，基类的排序可以通过打印其 `__mro__` 属性来查看。下面是一个例子：

```python
>>> MostEvilAccount.__mro__
(<class '__main__.MostEvilAccount'>,
 <class '__main__.EvilAccount'>,
 <class '__main__.Account'>,
 <class '__main__.DepositCharge'>,
 <class '__main__.WithdrawCharge'>,
 <type 'object'>)
>>>
```

在大多数情况下，此列表基于“合理”的规则。也就是说，派生类总是在其基类之前被检查，并且如果一个类有多个父类，则父类的检查顺序总是与类定义中列出的顺序相同。然而，基类的精确排序实际上相当复杂，并非基于某种“简单”的算法，如深度优先或广度优先搜索。相反，排序是根据 C3 线性化算法确定的，该算法在论文《A Monotonic Superclass Linearization for Dylan》（K. Barrett 等人，在 OOPSLA'96 上发表）中有描述。该算法的一个微妙之处是，某些类层次结构会被 Python 以 `TypeError` 拒绝。下面是一个例子：

```python
class X(object): pass
class Y(X): pass
class Z(X,Y): pass  # TypeError。
                    # 无法创建一致的方法解析顺序
```

在这种情况下，方法解析算法拒绝了类 `Z`，因为它无法确定一个合理的基类排序。例如，在继承列表中，类 `X` 出现在类 `Y` 之前，因此必须先检查它。然而，类 `Y` 更特化，因为它继承自 `X`。因此，如果先检查 `X`，就无法解析 `Y` 中的特化方法。在实践中，这些问题很少出现——如果出现，通常表明程序存在更严重的设计问题。

作为一般规则，在大多数程序中最好避免使用多重继承。然而，它有时被用来定义所谓的 *mixin* 类。mixin 类通常定义一组方法，旨在被“混入”其他类以添加额外功能（几乎像宏一样）。通常，mixin 中的方法会假设其他方法存在，并基于它们构建。前面的例子中的 `DepositCharge` 和 `WithdrawCharge` 类就说明了这一点。这些类向将其作为基类之一的类添加了新方法，如 `deposit_fee()`。然而，你永远不会单独实例化 `DepositCharge`。事实上，如果你这样做了，它不会创建一个可用于任何有用目的的实例（即，唯一定义的方法甚至无法正确执行）。

最后要注意的是，如果你想修复这个例子中对 `fee` 的有问题引用，`deposit_fee()` 和 `withdraw_fee()` 的实现应该改为使用类名直接引用属性，而不是使用 `self`（例如，`DepositCharge.fee`）。

#### 多态、动态绑定与鸭子类型

*动态绑定*（在继承上下文中使用时有时也称为 *多态*）是一种不考虑实例类型就能使用实例的能力。它完全通过上一节中描述的继承属性查找过程来处理。每当作为 `obj.attr` 访问属性时，会按顺序在实例本身、实例的类定义以及基类中搜索 `attr`。找到的第一个匹配项将被返回。

此绑定过程的一个关键方面是它独立于 `obj` 是什么类型的对象。因此，如果你进行 `obj.name` 这样的查找，它将对任何碰巧具有 `name` 属性的 `obj` 都有效。这种行为有时被称为 *鸭子类型*，参考了谚语“如果它看起来像、叫起来像、走起来像鸭子，那么它就是鸭子”。

Python 程序员经常编写依赖于这种行为的程序。例如，如果你想创建一个现有对象的自定义版本，你可以继承它，或者你可以简单地创建一个在外观和行为上与之相似但除此之外无关的全新对象。后一种方法通常用于维护程序组件之间的松散耦合。例如，代码可以编写为只要具有特定方法集，就可以与任何类型的对象一起工作。最常见的例子之一是标准库中定义的各种“文件类”对象。虽然这些对象的工作方式类似于文件，但它们并不继承自内置文件对象。

#### 静态方法与类方法

在类定义中，所有函数都被假定为在实例上操作，实例总是作为第一个参数 `self` 传递。然而，还有另外两种常见的方法可以定义。

*静态方法* 是一个恰好存在于类定义的命名空间中的普通函数。它不在任何类型的实例上操作。要定义静态方法，请使用 `@staticmethod` 装饰器，如下所示：

```python
class Foo(object):
    @staticmethod
    def add(x,y):
        return x + y
```

要调用静态方法，只需在类名前加上前缀即可。不要传递任何额外信息。例如：

```python
x = Foo.add(3,4)      # x = 7
```

静态方法的常见用途是在编写类时，你可能有多种方式来创建新实例。因为只能有一个 `__init__()` 函数，所以通常会定义替代的创建函数，如下所示：

```python
class Date(object):
    def __init__(self,year,month,day):
        self.year = year
        self.month = month
        self.day = day
    @staticmethod
    def now():
        t = time.localtime()
        return Date(t.tm_year, t.tm_mon, t.tm_day)
    @staticmethod
    def tomorrow():
        t = time.localtime(time.time()+86400)
        return Date(t.tm_year, t.tm_mon, t.tm_day)
```

```python
##### 创建一些日期的例子
a = Date(1967, 4, 9)
b = Date.now()      # 调用静态方法 now()
c = Date.tomorrow() # 调用静态方法 tomorrow()
```

*类方法* 是在类本身作为对象上操作的方法。使用 `@classmethod` 装饰器定义，类方法与实例方法的不同之处在于类被作为第一个参数传递，按照惯例命名为 `cls`。例如：

```python
class Times(object):
    factor = 1
    @classmethod
    def mul(cls,x):
        return cls.factor*x

class TwoTimes(Times):
    factor = 2
```

```python
x = TwoTimes.mul(4)     # 调用 Times.mul(TwoTimes, 4) -> 8
```



在这个例子中，注意类 `TwoTimes` 是如何作为对象传递给 `mul()` 的。虽然这个例子有些深奥，但类方法有实际但微妙的用途。例如，假设你定义了一个继承自前面所示的 `Date` 类并对其稍作定制的类：

```python
class EuroDate(Date):
    # 修改字符串转换以使用欧洲日期格式
    def __str__(self):
        return "%02d/%02d/%4d" % (self.day, self.month, self.year)
```

因为该类继承自 `Date`，所以它具有所有相同的功能。然而，`now()` 和 `tomorrow()` 方法有点不正常。例如，如果有人调用 `EuroDate.now()`，返回的是一个 `Date` 对象而不是 `EuroDate` 对象。类方法可以修复这个问题：

```python
class Date(object):
    ...
    @classmethod
    def now(cls):
        t = time.localtime()
        # 创建适当类型的对象
        return cls(t.tm_year, t.tm_month, t.tm_day)

class EuroDate(Date):
    ...
```

```python
a = Date.now()      # 调用 Date.now(Date) 并返回一个 Date
b = EuroDate.now()  # 调用 Date.now(EuroDate) 并返回一个 EuroDate
```

关于静态方法和类方法的一个注意事项是，Python 并没有将它们与实例方法放在不同的命名空间中管理。因此，它们可以在实例上调用。例如：

```python
a = Date(1967,4,9)
b = d.now()         # 调用 Date.now(Date)
```

这可能会相当令人困惑，因为调用 `d.now()` 实际上与实例 `d` 无关。这种行为是 Python 对象系统与 Smalltalk 和 Ruby 等其他面向对象语言不同的一个方面。在那些语言中，类方法严格区别于实例方法。

#### 属性

通常，当你访问实例或类的属性时，返回的是存储的关联值。*属性*是一种特殊的属性，其值在访问时计算。下面是一个简单的例子：

```python
class Circle(object):
    def __init__(self,radius):
        self.radius = radius
    # 圆的一些附加属性
    @property
    def area(self):
        return math.pi*self.radius**2
    @property
    def perimeter(self):
        return 2*math.pi*self.radius
```

生成的 `Circle` 对象的行为如下：

```python
>>> c = Circle(4.0)
>>> c.radius
4.0
>>> c.area
50.26548245743669
>>> c.perimeter
25.132741228718345
>>> c.area = 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: can't set attribute
>>>
```

在这个例子中，`Circle` 实例有一个存储的实例变量 `c.radius`。`c.area` 和 `c.perimeter` 仅仅是从该值计算出来的。`@property` 装饰器使得紧随其后的方法可以像简单属性一样访问，而无需像通常调用方法那样添加额外的 `()`。对于对象的使用者来说，除了尝试重新定义属性时会产生错误消息（如上面的 `AttributeError` 异常所示）之外，没有明显的迹象表明属性是被计算出来的。

以这种方式使用属性与所谓的*统一访问原则*相关。本质上，如果你在定义一个类，使其编程接口尽可能统一总是一个好主意。没有属性，对象的某些属性将作为简单属性访问，如 `c.radius`，而其他属性则作为方法访问，如 `c.area()`。跟踪何时需要添加额外的 `()` 会带来不必要的困惑。属性可以解决这个问题。

Python 程序员通常没有意识到方法本身就被隐式地处理为一种属性。考虑这个类：

```python
class Foo(object):
    def __init__(self,name):
        self.name = name
    def spam(self,x):
        print("%s, %s" % (self.name, x))
```

当用户创建一个实例，例如 `f = Foo("Guido")`，然后访问 `f.spam` 时，原始的函数对象 `spam` 并不会被返回。相反，你会得到一个所谓的*绑定方法*，它是一个代表方法调用的对象，当在其上调用 `()` 运算符时将执行该调用。绑定方法就像一个部分求值的函数，其中 `self` 参数已经被填充，但在使用 `()` 调用它时，你仍然需要提供额外的参数。这个绑定方法对象的创建是通过一个在后台执行的属性函数悄悄处理的。当你使用 `@staticmethod` 和 `@classmethod` 定义静态方法和类方法时，你实际上是指定了使用不同的属性函数，该函数将以不同的方式处理对这些方法的访问。例如，`@staticmethod` 只是简单地将方法函数原样返回，没有任何特殊的包装或处理。

属性还可以拦截设置和删除属性的操作。这是通过将额外的设置器和删除器方法附加到属性来完成的。下面是一个例子：

```python
class Foo(object):
    def __init__(self,name):
        self.__name = name
    @property
    def name(self):
        return self.__name
    @name.setter
    def name(self,value):
        if not isinstance(value,str):
            raise TypeError("Must be a string!")
        self.__name = value
    @name.deleter
    def name(self):
        raise TypeError("Can't delete name")
```

```python
f = Foo("Guido")
n = f.name         # 调用 f.name() - 获取函数
f.name = "Monty"   # 调用 setter name(f,"Monty")
f.name = 45        # 调用 setter name(f,45) -> TypeError
del f.name         # 调用 deleter name(f) -> TypeError
```

在这个例子中，属性 name 首先使用 @property 装饰器及其关联方法定义为只读属性。随后的 @name.setter 和 @name.deleter 装饰器将额外的方法与 name 属性的设置和删除操作相关联。这些方法的名称必须与原始属性的名称完全匹配。在这些方法中，注意 name 的实际值存储在属性 __name 中。存储属性的名称不必遵循任何约定，但必须不同于属性本身，以便将其与属性本身的名称区分开来。

在旧代码中，你经常会看到使用 property(getf=None, setf=None, delf=None, doc=None) 函数定义的属性，该函数有一组唯一命名的方法来执行每个操作。例如：

```python
class Foo(object):
    def getname(self):
        return self.__name
    def setname(self,value):
        if not isinstance(value,str):
            raise TypeError("Must be a string!")
        self.__name = value
    def delname(self):
        raise TypeError("Can't delete name")
    name = property(getname,setname,delname)
```

这种旧方法仍然受支持，但装饰器版本往往能产生更精炼的类。例如，如果你使用装饰器，get、set 和 delete 函数就不会作为方法可见。

###### 描述符

使用属性时，对属性的访问由一系列用户定义的 get、set 和 delete 函数控制。这种属性控制可以通过使用描述符对象进一步泛化。描述符只是一个代表属性值的对象。通过实现特殊方法 __get__()、__set__() 和 __delete__() 中的一个或多个，它可以钩入属性访问机制并自定义这些操作。下面是一个例子：

```python
class TypedProperty(object):
    def __init__(self,name,type,default=None):
        self.name = "_" + name
        self.type = type
        self.default = default if default else type()
    def __get__(self,instance,cls):
        return getattr(instance,self.name,self.default)
    def __set__(self,instance,value):
        if not isinstance(value,self.type):
            raise TypeError("Must be a %s" % self.type)
        setattr(instance,self.name,value)
    def __delete__(self,instance):
        raise AttributeError("Can't delete attribute")

class Foo(object):
    name = TypedProperty("name",str)
    num  = TypedProperty("num",int,42)
```

在这个例子中，类 `TypedProperty` 定义了一个描述符，其中在属性被赋值时执行类型检查，并在尝试删除属性时产生错误。例如：

```python
f = Foo()
a = f.name          # 隐式调用 Foo.name.__get__(f,Foo)
f.name = "Guido"    # 调用 Foo.name.__set__(f,"Guido")
del f.name          # 调用 Foo.name.__delete__(f)
```

描述符只能在类级别实例化。通过在 `__init__()` 和其他方法中创建描述符对象来为每个实例创建描述符是不允许的。此外，类用于保存描述符的属性名称优先于实例上存储的属性。在前面的例子中，这就是为什么描述符对象接受一个 name 参数，以及为什么名称通过添加前导下划线而略有改变。为了使描述符能够在实例上存储值，它必须选择一个与描述符本身所使用的名称不同的名称。

#### 数据封装和私有属性

默认情况下，一个类的所有属性和方法都是“公共的”。这意味着它们都可以在没有任何限制的情况下访问。这也意味着在基类中定义的所有内容都被继承并且可以在派生类中访问。这种行为在面向对象应用程序中通常是不可取的，因为它暴露了对象的内部实现，并可能导致派生类中定义的对象与基类中定义的对象之间的命名空间冲突。

为了解决这个问题，类中所有以双下划线开头的名称，例如 `__Foo`，会自动被修饰（mangled）以形成新的名称，形式为 `_Classname__Foo`。这实际上提供了一种让类拥有私有属性和方法的方式，因为在派生类中使用的私有名称不会与在基类中使用的相同私有名称冲突。下面是一个例子：

```python
class A(object):
    def __init__(self baking soda):
        self.__X = 3          # 被修饰为 self._A__X
    def __spam(self):          # 被修饰为 _A__spam()
        pass
    def bar(self):
        self.__spam()          # 只调用 A.__spam()
```



#### 对象内存管理

当定义一个类时，得到的类是用于创建新实例的工厂。例如：

```python
class Circle(object):
    def __init__(self, radius):
        self.radius = radius

##### Create some Circle instances
c = Circle(4.0)
d = Circle(5.0)
```

实例的创建通过特殊方法 `__new__()`（用于创建新实例）和 `__init__()`（用于初始化实例）分两步完成。例如，操作 `c = Circle(4.0)` 执行以下步骤：

```python
c = Circle.__new__(Circle, 4.0)
if isinstance(c, Circle):
    Circle.__init__(c, 4.0)
```

类的 `__new__()` 方法很少由用户代码定义。如果定义了，通常采用 `__new__(cls, *args, **kwargs)` 的原型，其中 `args` 和 `kwargs` 是将传递给 `__init__()` 的相同参数。`__new__()` 始终是一个类方法，将类对象作为第一个参数接收。虽然 `__new__()` 创建了实例，但它不会自动调用 `__init__()`。

如果你在某个类中看到 `__new__()` 的定义，通常意味着该类在做两件事之一。首先，该类可能继承了一个实例不可变的基类。这在定义继承自不可变内置类型（如整数、字符串或元组）的对象时很常见，因为 `__new__()` 是在实例创建之前唯一执行的方法，也是唯一可以修改值的地方（在 `__init__()` 中则为时已晚）。例如：

```python
class Upperstr(str):
    def __new__(cls, value=""):
        return str.__new__(cls, value.upper())

u = Upperstr("hello")    # value is "HELLO"
```

`__new__()` 的另一个主要用途是在定义元类时。这将在本章末尾进行描述。

实例创建后，通过引用计数进行管理。如果引用计数归零，实例会立即被销毁。当实例即将被销毁时，解释器首先查找与该对象关联的 `__del__()` 方法并调用它。在实践中，类很少需要定义 `__del__()` 方法。唯一的例外是当对象的销毁需要执行清理操作时，例如关闭文件、关闭网络连接或释放其他系统资源。即使在这些情况下，依赖 `__del__()` 来实现干净的关闭也是危险的，因为无法保证解释器退出时该方法一定会被调用。更好的方法可能是定义一个 `close()` 之类的方法，让程序显式地执行关闭操作。

偶尔，程序会使用 `del` 语句删除对对象的引用。如果这导致对象的引用计数归零，则会调用 `__del__()` 方法。但一般来说，`del` 语句并不会直接调用 `__del__()`。

对象销毁涉及一个微妙的危险：定义了 `__del__()` 的实例无法被 Python 的循环垃圾收集器回收（这是不定义 `__del__` 的一个强有力的理由，除非确实需要）。来自没有自动垃圾收集的语言（例如 C++）的程序员应注意不要采用不必要地定义 `__del__()` 的编程风格。虽然定义 `__del__()` 破坏垃圾收集器的情况很少见，但某些类型的编程模式，尤其是涉及父子关系或图结构的模式，可能会导致问题。例如，假设你有一个实现了"观察者模式"变体的对象。

```python
class Account(object):
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance
        self.observers = set()
    def __del__(self):
        for ob in self.observers:
            ob.close()
        del self.observers
    def register(self, observer):
        self.observers.add(observer)
    def unregister(self, observer):
        self.observers.remove(observer)
    def notify(self):
        for ob in self.observers:
            ob.update()
    def withdraw(self, amt):
        self.balance -= amt
        self.notify()

class AccountObserver(object):
    def __init__(self, theaccount):
        self.theaccount = theaccount
        theaccount.register(self)
    def __del__(self):
        self.theaccount.unregister(self)
        del self.theaccount
    def update(self):
        print("Balance is %0. " % self.theaccount.balance)
    def close(self):
        print("Account no longer in use")

##### Example setup
a = Account('Dave', 1000.00)
a_ob = AccountObserver(a)
```

在这段代码中，`Account` 类允许一组 `AccountObserver` 对象通过在余额变化时接收更新来监控 `Account` 实例。为此，每个 `Account` 保存一组观察者，每个 `AccountObserver` 保存对账户的反向引用。每个类都定义了 `__del__()`，试图提供某种清理功能（如注销等）。然而，这根本不起作用。相反，这些类创建了一个引用循环，引用计数永远不会降到 0，也就无法进行清理。不仅如此，垃圾收集器（`gc` 模块）甚至不会清理它，导致永久性的内存泄漏。

解决此示例中问题的一种方法是让其中一个类使用 `weakref` 模块对另一个类创建弱引用。*弱引用* 是一种创建对象引用而不增加其引用计数的方式。使用弱引用时，需要额外添加一些功能来检查被引用的对象是否仍然存在。以下是修改后的观察者类示例：

```python
import weakref

class AccountObserver(object):
    def __init__(self, theaccount):
        self.accountref = weakref.ref(theaccount)  # Create a weakref
        theaccount.register(self)
```



#### 对象表示与属性绑定

在内部，实例是通过一个字典实现的，该字典可通过实例的 `__dict__` 属性访问。这个字典包含了每个实例独有的数据。以下是一个示例：

```
>>> a = Account('Guido', 1100.0)
>>> a.__dict__
{'balance': 1100.0, 'name': 'Guido'}
```

随时可以向实例添加新属性，如下所示：

```
a.number = 123456    # 向 a.__dict__ 添加属性 'number'
```

对实例的修改总会反映在局部的 `__dict__` 属性中。同样，如果你直接修改 `__dict__`，这些修改也会反映在属性中。

实例通过一个特殊的属性 `__class__` 链接回其类。类本身也只是一个覆盖在其自身 `__dict__` 属性中字典的薄层。类字典是你可以找到方法的地方。例如：

```
>>> a.__class__
<class '__main__.Account'>
>>> Account.__dict__.keys()
['__dict__', '__module__', 'inquiry', 'deposit', 'withdraw',
 '__del__', 'num_accounts', '__weakref__', '__doc__', '__init__']
>>>
```

最后，类通过一个特殊的 `__bases__` 属性链接到其基类，该属性是一个包含所有基类的元组。这种底层结构是获取、设置和删除对象属性的所有操作的基础。

每当使用 `obj.name = value` 设置属性时，都会调用特殊方法 `obj.__setattr__("name", value)`。如果使用 `del obj.name` 删除属性，则会调用特殊方法 `obj.__delattr__("name")`。这些方法的默认行为是修改或从 `obj` 的局部 `__dict__` 中删除值，除非请求的属性恰好对应于一个属性（property）或描述符（descriptor）。在这种情况下，设置和删除操作将由与该属性关联的 set 和 delete 函数执行。

对于像 `obj.name` 这样的属性查找，会调用特殊方法 `obj.__getattribute__("name")`。该方法执行查找属性的过程，通常包括检查属性、在局部 `__dict__` 属性中查找、检查类字典以及搜索基类。如果此搜索过程失败，最后会尝试调用类的 `__getattr__()` 方法（如果已定义）来查找属性。如果这也失败，则会引发 `AttributeError` 异常。

如果需要，用户定义的类可以实现自己的属性访问函数版本。例如：

```
class Circle(object):
    def __init__(self, radius):
        self.radius = radius

    def __getattr__(self, name):
        if name == 'area':
            return math.pi * self.radius ** 2
        elif name == 'perimeter':
            return 2 * math.pi * self.radius
        else:
            return object.__getattr__(self, name)

    def __setattr__(self, name, value):
        if name in ['area', 'perimeter']:
            raise TypeError("%s is readonly" % name)
        object.__setattr__(self, name, value)
```

重新实现这些方法的类可能应该依赖于 `object` 中的默认实现来执行实际工作。这是因为默认实现处理了类中更高级的功能，如描述符和属性。

作为一般规则，类重新定义属性访问运算符的情况相对少见。然而，一个常见的应用场景是在编写通用包装器和代理以代理现有对象时。通过重新定义 `__getattr__()`、`__setattr__()` 和 `__delattr__()`，代理可以捕获属性访问并透明地将这些操作转发到另一个对象。

#### `__slots__`

类可以通过定义一个名为 `__slots__` 的特殊变量来限制合法的实例属性名称集。以下是一个示例：

```
class Account(object):
    __slots__ = ('name', 'balance')
    ...
```

当定义了 `__slots__` 时，可在实例上赋值的属性名称被限制为指定的名称。否则，将引发 `AttributeError` 异常。这种限制防止有人向现有实例添加新属性，并解决了当有人将值赋给他们拼写不正确的属性时可能出现的问题。

实际上，`__slots__` 从未被实现为一种安全功能。相反，它实际上是针对内存和执行速度的性能优化。使用 `__slots__` 的类的实例不再使用字典来存储实例数据。相反，使用基于数组的更紧凑的数据结构。在创建大量对象的程序中，使用 `__slots__` 可以显著减少内存使用和执行时间。

请注意，`__slots__` 的使用与继承存在一种微妙的交互。如果一个类继承自使用 `__slots__` 的基类，它也需要定义 `__slots__` 来存储自身的属性（即使它没有添加任何属性），以利用 `__slots__` 提供的优势。如果你忘记了这一点，派生类的运行速度会更慢，并且使用的内存甚至比在任何类上都未使用 `__slots__` 时还要多！

`__slots__` 的使用也可能破坏期望实例具有底层 `__dict__` 属性的代码。虽然这通常不适用于用户代码，但用于支持对象的实用程序库和其他工具可能会被编程为查看 `__dict__` 进行调试、序列化对象和其他操作。

最后，`__slots__` 的存在对诸如 `__getattribute__()`、`__getattr__()` 和 `__setattr__()` 等方法的调用没有影响，前提是它们在类中被重新定义。然而，这些方法的默认行为将考虑 `__slots__`。此外，应该强调的是，没有必要将方法或属性名称添加到 `__slots__` 中，因为它们存储在类中，而不是每个实例单独存储。

#### 运算符重载

用户定义的对象可以通过向类添加第3章中描述的特殊方法的实现来使其与所有 Python 内置运算符一起工作。例如，如果你想向 Python 添加一种新的数字类型，你可以定义一个类，其中定义了 `__add__()` 等特殊方法，以使实例能够与标准数学运算符一起工作。

以下示例通过定义一个实现了部分标准数学运算符的复数类来展示其工作原理。

> **注意**
> 因为 Python 已经提供了复数类型，所以这个类仅用于说明目的。

```
class Complex(object):
    def __init__(self, real, imag=0):
        self.real = float(real)
        self.imag = float(imag)

    def __repr__(self):
        return "Complex(%s,%s)" % (self.real, self.imag)

    def __str__(self):
        return "(%g+%gj)" % (self.real, self.imag)

    # self + other
    def __add__(self, other):
        return Complex(self.real + other.real, self.imag + other.imag)

    # self - other
    def __sub__(self, other):
        return Complex(self.real - other.real, self.imag - other.imag)
```

在这个例子中，`__repr__()` 方法创建了一个可以被求值以重新创建对象的字符串（即 "Complex(real,imag)"）。对于所有适用的用户定义对象，都应遵循此惯例。另一方面，`__str__()` 方法



#### 类型与类成员测试

当你创建一个类的实例时，该实例的类型就是这个类本身。要测试是否属于某个类，可以使用内置函数 `isinstance(obj, cname)`。如果一个对象 *obj* 属于类 *cname* 或者任何从 *cname* 派生的类，该函数将返回 `True`。下面是一个示例：

```
class A(object): pass
class B(A): pass
class C(object): pass

a = A()         # 'A' 的实例
b = B()         # 'B' 的实例
c = C()         # 'C' 的实例

type(a)         # 返回类对象 A
isinstance(a, A) # 返回 True
isinstance(b, A) # 返回 True，B 派生自 A
isinstance(b, C) # 返回 False，C 未派生自 A
```

类似地，内置函数 `issubclass(A, B)` 在类 A 是类 B 的子类时返回 `True`。下面是一个示例：

```
issubclass(B, A)  # 返回 True
issubclass(C, A)  # 返回 False
```

对象类型检查的一个微妙问题在于，程序员经常绕过继承，而是简单地创建模拟另一个对象行为的对象。作为一个例子，考虑这两个类：

```
class Foo(object):
    def spam(self, a, b):
        pass

class FooProxy(object):
    def __init__(self, f):
        self.f = f
    def spam(self, a, b):
        return self.f.spam(a, b)
```

在这个例子中，`FooProxy` 在功能上与 `Foo` 相同。它实现了相同的方法，甚至在底层使用了 `Foo`。然而，在类型系统中，`FooProxy` 与 `Foo` 是不同的。例如：

```
f = Foo()         # 创建一个 Foo
g = FooProxy(f)   # 创建一个 FooProxy
isinstance(g, Foo) # 返回 False
```

如果一个程序被编写为使用 `isinstance()` 显式检查 `Foo`，那么它肯定无法与 `FooProxy` 对象一起工作。然而，这种严格的程度通常并非你想要的。相反，断言一个对象可以像 `Foo` 一样使用可能更有意义，因为它具有相同的接口。为此，可以定义一个对象，重新定义 `isinstance()` 和 `issubclass()` 的行为，目的是将对象分组在一起并进行类型检查。下面是一个示例：

```
class IClass(object):
    def __init__(self):
        self.implementors = set()
    def register(self, C):
        self.implementors.add(C)
    def __instancecheck__(self, x):
        return self.__subclasscheck__(type(x))
    def __subclasscheck__(self, sub):
        return any(c in self.implementors for c in sub.mro())
```

现在，使用上述对象：

```
IFoo = IClass()
IFoo.register(Foo)
IFoo.register(FooProxy)
```

在这个例子中，类 `IClass` 创建了一个对象，该对象仅将一组其他类集合在一个集合中。`register()` 方法将一个新类添加到集合中。当任何人执行 `isinstance(x, IClass)` 操作时，会调用特殊方法 `__instancecheck__()`。当执行 `issubclass(C, IClass)` 操作时，会调用特殊方法 `__subclasscheck__()`。

通过使用 `IFoo` 对象和已注册的实现者，现在可以执行如下类型检查：

```
f = Foo()           # 创建一个 Foo
g = FooProxy(f)     # 创建一个 FooProxy
isinstance(f, IFoo)        # 返回 True
isinstance(g, IFoo)        # 返回 True
issubclass(FooProxy, IFoo) # 返回 True
```

在这个例子中，需要强调的是没有发生严格的类型检查。`IFoo` 对象重载了实例检查操作，允许你断言一个类属于某个组。它没有断言任何关于实际编程接口的信息，也没有进行任何其他验证。事实上，你可以简单地注册任何你想要分组在一起的对象集合，而无需考虑这些类彼此之间的关系。通常，类的分组基于某些标准，例如所有类都实现了相同的编程接口。然而，在重载 `__instancecheck__()` 或 `__subclasscheck__()` 时，不应推断出此类含义。实际的解释权留给应用程序。

Python 提供了一种更正式的机制来分组对象、定义接口和进行类型检查。这是通过定义抽象基类来完成的，将在下一节中定义。

##### 抽象基类

在上一节中，展示了 `isinstance()` 和 `issubclass()` 操作可以被重载。这可以用于创建将相似类分组在一起的对象，并执行各种形式的类型检查。抽象基类在此概念的基础上构建，并提供了一种将对象组织成层次结构、对必需方法进行断言等的方法。

要定义抽象基类，你使用 `abc` 模块。该模块定义了一个元类（`ABCMeta`）和一组装饰器（`@abstractmethod` 和 `@abstractproperty`），其用法如下：

```
from abc import ABCMeta, abstractmethod, abstractproperty
class Foo:                    # 在 Python 3 中，你使用语法
    __metaclass__ = ABCMeta   # class Foo(metaclass=ABCMeta)
    @abstractmethod
    def spam(self, a, b):
        pass
    @abstractproperty
    def name(self):
        pass
```

抽象类的定义需要将其元类设置为 `ABCMeta`，如示例所示（另外，请注意 Python 2 和 3 之间的语法差异）。这是必需的，因为抽象类的实现依赖于元类（在下一节中描述）。在抽象类内部，`@abstractmethod` 和 `@abstractproperty` 装饰器指定一个方法或属性必须由 `Foo` 的子类来实现。

抽象类不应直接实例化。如果你尝试为前面的类创建 `Foo`，你将得到以下错误：

```
>>> f = Foo()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class Foo with abstract methods spam
>>>
```

此限制也适用于派生类。例如，如果你有一个从 `Foo` 继承但没有实现一个或多个抽象方法的类 `Bar`，尝试创建 `Bar` 将会失败并出现类似的错误。由于这种额外的检查，抽象类对于想要对子类必须实现的方法和属性进行断言的程序员非常有用。

虽然抽象类强制执行关于必须实现的方法和属性的规则，但它不对参数或返回值执行一致性检查。因此，抽象类不会检查子类是否使用了与抽象方法相同的参数。同样，要求定义属性的抽象类不会检查子类中的属性是否支持基类中指定的属性的相同操作集（get、set 和 delete）。

虽然抽象类不能被实例化，但它可以定义供子类使用的方法和属性。此外，基类中的抽象方法仍然可以从子类调用。例如，从子类调用 `Foo.spam(a, b)` 是允许的。

抽象基类允许将现有类注册为属于该基类。这是使用 `register()` 方法完成的，如下所示：

```
class Grok(object):
    def spam(self, a, b):
        print("Grok.spam")

Foo.register(Grok)    # 向 Foo 抽象基类注册
```

当一个类注册到抽象基类时，涉及该抽象基类的类型检查操作（如 `isinstance()` 和 `issubclass()`）将为已注册类的实例返回 `True`。当一个类注册到抽象类时，不会检查该类是否实际实现了任何抽象方法或属性。此注册过程仅影响类型检查。它不会向被注册的类添加额外的错误检查。

与许多其他面向对象的语言不同，Python 的内置类型被组织成一个相对平坦的层次结构。例如，如果你查看内置类型如 `int` 或 `float`，它们直接继承自 `object`（所有对象的根类），而不是代表数字的中间基类。这使得编写基于泛型类别（例如仅仅是数字的实例）来检查和操作对象的程序变得笨拙。



抽象类机制通过允许将现有对象组织成用户可定义的类型层次结构来解决这个问题。此外，一些库模块旨在根据它们所拥有的不同能力来组织内置类型。`collections` 模块包含用于涉及序列、集合和字典的各种操作的抽象基类。`numbers` 模块包含与组织数字层次结构相关的抽象基类。更多细节可以在第 14 章 "数学" 和第 15 章 "数据结构、算法与实用工具" 中找到。

#### 元类

当你在 Python 中定义一个类时，类定义本身会变成一个对象。下面是一个例子：

```python
class Foo(object): pass
isinstance(Foo,object)     # Returns True
```

如果你仔细思考，你会意识到一定是某个东西创建了 `Foo` 对象。这种类对象的创建由一种称为*元类*的特殊对象控制。简单来说，元类是一个知道如何创建和管理类的对象。

在前面的例子中，控制 `Foo` 创建的元类是一个名为 `type` 的类。事实上，如果你查看 `Foo` 的类型，你会发现它*是*一个 `type`：

```python
>>> type(Foo)
<type 'type'>
```

当使用 `class` 语句定义一个新类时，会发生许多事情。首先，类的主体作为一系列语句在其私有字典中执行。语句的执行与正常代码完全相同，只是私有成员（以 `__` 开头的名称）会发生名称修饰。最后，类的名称、基类的列表以及字典被传递给元类的构造函数以创建相应的类对象。下面是一个工作原理的例子：

```python
class_name = "Foo"            # Name of class
class_parents = (object,)     # Base classes
class_body = """              # Class body
def __init__(self,x):
    self.x = x
def blah(self):
    print("Hello World")
"""
class_dict = { }
##### Execute the body in the local dictionary class_dict
exec(class_body,globals(),class_dict)

##### Create the class object Foo
Foo = type(class_name,class_parents,class_dict)
```

类创建的最后一步，即调用元类 `type()`，可以进行自定义。类定义最后一步发生什么的选择由多种方式控制。首先，类可以通过设置 `__metaclass__` 类变量（Python 2）或在基类元组中提供 `metaclass` 关键字参数（Python 3）来显式指定其元类。

```python
class Foo:              # In Python 3, use the syntax
    __metaclass__ = type  # class Foo(metaclass=type)
    ...
```

如果未显式指定元类，`class` 语句会检查基类元组中的第一个条目（如果有）。在这种情况下，元类与第一个基类的类型相同。因此，当你编写

```python
class Foo(object): pass
```

`Foo` 将是与 `object` 相同类型的类。

如果未指定任何基类，`class` 语句会检查是否存在名为 `__metaclass__` 的全局变量。如果找到此变量，它将用于创建类。如果你设置了此变量，它将控制使用简单类语句时类的创建方式。下面是一个例子：

```python
__metaclass__ = type
class Foo:
    pass
```

最后，如果任何地方都找不到 `__metaclass__` 值，Python 将使用默认元类。在 Python 2 中，这默认为 `types.ClassType`，称为*旧式类*。这种自 Python 2.2 以来已弃用的类对应于 Python 中类的原始实现。尽管这些类仍然受到支持，但应在新代码中避免使用，并且本文档不再进一步介绍。在 Python 3 中，默认元类就是 `type()`。

元类的主要用途在于希望对用户定义对象的定义施加更多控制的框架中。当定义自定义元类时，它通常继承自 `type()` 并重新实现诸如 `__init__()` 或 `__new__()` 之类的方法。下面是一个强制所有方法都具有文档字符串的元类示例：

```python
class DocMeta(type):
    def __init__(self,name,bases,dict):
        for key, value in dict.items():
            # Skip special and private methods
            if key.startswith("__"): continue
            # Skip anything not callable
            if not hasattr(value,"__call__"): continue
            # Check for a doc-string
            if not getattr(value,"__doc__"):
                raise TypeError("%s must have a docstring" % key)
        type.__init__(self,name,bases,dict)
```

在这个元类中，`__init__()` 方法被编写为检查类字典的内容。它扫描字典，寻找方法并检查它们是否都有文档字符串。如果没有，则会生成 `TypeError` 异常。否则，将调用 `type.__init__()` 的默认实现来初始化类。

要使用此元类，一个类需要显式选择它。最常用的技术是首先定义一个基类，如下所示：

```python
class Documented:           # In Python 3, use the syntax
    __metaclass__ = DocMeta # class Documented(metaclass=DocMeta)
```

然后，这个基类被用作所有需要文档化的对象的父类。例如：

```python
class Foo(Documented):
    spam(self,a,b):
        "spam does something"
        pass
```

这个例子说明了元类的一个主要用途，即检查和收集有关类定义的信息。元类并没有改变实际创建的类的任何内容，而只是添加了一些额外的检查。

在更高级的元类应用中，元类可以在创建类之前既检查又更改类定义的内容。如果要进行更改，你应该重新定义在类本身创建之前运行的 `__new__()` 方法。这种技术通常与使用描述符或属性包装属性的技术相结合，因为它是捕获类中所用名称的一种方式。作为示例，这里是 "描述符" 部分中使用的 `TypedProperty` 描述符的修改版本：

```python
class TypedProperty(object):
    def __init__(self,type,default=None):
        self.name = None
        self.type = type
        if default: self.default = default
        else:       self.default = type()
    def __get__(self,instance,cls):
        return getattr(instance,self.name,self.default)
    def __set__(self,instance,value):
        if not isinstance(value,self.type):
            raise TypeError("Must be a %s" % self.type)
        setattr(instance,self.name,value)
    def __delete__(self,instance):
        raise AttributeError("Can't delete attribute")
```

在这个例子中，描述符的 name 属性被简单地设置为 None。为了填充它，我们将依赖一个元类。例如：

```python
class TypedMeta(type):
    def __new__(cls,name,bases,dict):
        slots = []
        for key,value in dict.items():
            if isinstance(value,TypedProperty):
                value.name = "_" + key
                slots.append(value.name)
        dict['__slots__'] = slots
        return type.__new__(cls,name,bases,dict)

##### Base class for user-defined objects to use
class Typed:                      # In Python 3, use the syntax
    __metaclass__ = TypedMeta     # class Typed(metaclass=TypedMeta)
```

在这个例子中，元类扫描类字典并寻找 `TypedProperty` 的实例。如果找到，它会设置 name 属性并在 `slots` 中构建一个名称列表。完成此操作后，将 `__slots__` 属性添加到类字典中，并通过调用 `type()` 元类的 `__new__()` 方法来构造类。下面是使用这个新元类的一个例子：

```python
class Foo(Typed):
    name = TypedProperty(str)
    num  = TypedProperty(int,42)
```



虽然元类能够彻底改变用户定义类的行为和语义，但你可能应该避免以偏离标准 Python 文档中描述的方式使用元类，以免让类的工作方式变得过于特异。如果用户编写的类不符合通常预期的类编程规则，他们将会感到困惑。

#### 类装饰器

在前一节中，我们展示了如何通过定义元类来定制类的创建过程。然而，有时你只需要在类定义完成后执行一些额外处理，例如将类添加到注册表或数据库中。对于这类问题，另一种方法是使用类装饰器。*类装饰器*是一个以类为输入并返回一个类的函数。例如：

```
registry = { }
def register(cls):
    registry[cls.__clsid__] = cls
    return cls
```

在此示例中，`register` 函数在类内部查找 `__clsid__` 属性。如果找到，它会使用该属性将类添加到一个将类标识符映射到类对象的字典中。要使用此函数，可以在类定义之前将其用作装饰器。例如：

```
@register
class Foo(object):
    __clsid__ = "123-456"
    def bar(self):
        pass
```

这里，使用装饰器语法主要是为了方便。实现相同功能的另一种方式如下：

```
class Foo(object):
    __clsid__ = "123-456"
    def bar(self):
        pass
register(Foo)      # Register the class
```

尽管在类装饰器函数中可以想象出无数种可能对类进行的巧妙操作，但最好避免过度魔法，例如在类周围包装一层包装器或重写类内容。

### 模块、包和分发

大型 Python 程序被组织成模块和包。此外，Python 标准库中包含了大量模块。本章将更详细地描述模块和包系统。此外，它还提供了关于如何安装第三方模块和分发源代码的信息。

#### 模块和 `import` 语句

任何 Python 源文件都可以用作模块。例如，考虑以下代码：

```
##### spam.py
a = 37
def foo():
    print("I'm foo and a is %s" % a)
def bar():
    print("I'm bar and I'm calling foo")
    foo()
class Spam(object):
    def grok(self):
        print("I'm Spam.grok")
```

要将此代码作为模块加载，请使用语句 `import spam`。第一次使用 `import` 加载模块时，它会执行三件事：

1.  它创建一个新命名空间，作为相应源文件中定义的所有对象的容器。这是在模块内定义的函数和方法使用 `global` 语句时访问的命名空间。
2.  它在新创建的命名空间中执行模块包含的代码。
3.  它在调用者中创建一个指向模块命名空间的名称。此名称与模块名称匹配，并按如下方式使用：

```
import spam            # Loads and executes the module 'spam'
x = spam.a             # Accesses a member of module 'spam'
spam.foo()             # Call a function in module 'spam'
s = spam.Spam()        # Create an instance of spam.Spam()
s.grok()
...
```

需要强调的是，`import` 会执行已加载源文件中的所有语句。如果模块在定义变量、函数和类之外还执行了计算或产生输出，你将会看到结果。此外，模块的一个常见困惑是关于类的访问。请记住，如果文件 `spam.py` 定义了一个类 `Spam`，你必须使用名称 `spam.Spam` 来引用该类。

要导入多个模块，可以向 `import` 提供一个以逗号分隔的模块名称列表，如下所示：

```
import socket, os, re
```

可以使用 `as` 限定符更改用于引用模块的名称。例如：

```
import spam as sp
import socket as net
sp.foo()
sp.bar()
net.gethostname()
```

当使用这样的不同名称加载模块时，新名称仅适用于 `import` 语句出现的源文件或上下文。其他程序模块仍然可以使用其原始名称加载模块。

更改导入模块的名称是编写可扩展代码的有用工具。例如，假设你有两个模块 `xmlreader.py` 和 `csvreader.py`，它们都定义了一个函数 `read_data(filename)` 用于从文件读取某些数据，但输入格式不同。你可以编写代码来有选择地挑选读取器模块，如下所示：

```
if format == 'xml':
    import xmlreader as reader
elif format == 'csv':
    import csvreader as reader
data = reader.read_data(filename)
```

模块在 Python 中是第一类对象。这意味着它们可以被赋值给变量、放入列表等数据结构中，以及作为数据在程序中传递。例如，上例中的 `reader` 变量只是指向相应的模块对象。在底层，模块对象是用于保存模块命名空间内容的字典的一层包装。这个字典可以通过模块的 `__dict__` 属性访问，无论你何时查找或更改模块中的值，你都是在操作这个字典。

`import` 语句可以出现在程序中的任何位置。但是，每个模块中的代码只会被加载和执行一次，无论你使用 `import` 语句多少次。后续的 `import` 语句只是将模块名称绑定到先前导入已创建的模块对象。你可以在变量 `sys.modules` 中找到包含所有当前已加载模块的字典。此字典将模块名称映射到模块对象。此字典的内容用于确定 `import` 是加载模块的新副本还是使用现有副本。

#### 从模块导入特定符号

`from` 语句用于将模块中的特定定义加载到当前命名空间中。`from` 语句与 `import` 相同，不同之处在于它不是创建一个指向新创建模块命名空间的名称，而是将模块中定义的一个或多个对象的引用放入当前命名空间：

```
from spam import foo  # Imports spam and puts 'foo' in current namespace
foo()                  # Calls spam.foo()
spam.foo()             # NameError: spam
```

`from` 语句也接受以逗号分隔的对象名称列表。例如：

```
from spam import foo, bar
```

如果你有很长的名称列表需要导入，可以将这些名称括在括号中。这使得 `import` 语句更容易跨多行书写。例如：

```
from spam import (foo,
                   bar,
                   Spam)
```

此外，`as` 限定符可用于重命名使用 `from` 导入的特定对象。例如：

```
from spam import Spam as Sp
s = Sp()
```

也可以使用星号 (`*`) 通配符来加载模块中的所有定义，但以下划线开头的定义除外。例如：

```
from spam import *  # Load all definitions into current namespace
```

`from module import *` 语句只能在模块的顶层使用。特别是，由于它与函数作用域规则的交互方式（例如，当函数被编译成内部字节码时，函数内使用的所有符号都需要完全指定），在函数体内使用这种导入形式是非法的。

模块可以通过定义列表 `__all__` 来更精确地控制由 `from module import *` 导入的名称集。例如：

```
##### module: spam.py
__all__ = [ 'bar', 'Spam' ]  # Names I will export with from spam import *
```

使用 `from` 形式导入定义不会改变它们的作用域规则。例如，考虑以下代码：

```
from spam import foo
a = 42
foo()     # Prints "I'm foo and a is 37"
```

在此示例中，`spam.py` 中 `foo()` 的定义引用了一个全局变量 `a`。当对 `foo` 的引用被放置到不同的命名空间时，它不会改变该函数内变量的绑定规则。因此，函数的全局命名空间始终是定义该函数的模块，而不是导入和调用该函数的命名空间。这也适用于函数调用。例如，在

以下代码中，对 `bar()` 的调用将导致调用 `spam.foo()`，而不是前面代码示例中重新定义的 `foo()`：

```
from spam import bar
def foo():
    print("I'm a different foo")
bar()          # 当 bar 调用 foo() 时，它调用的是 spam.foo()，而非
               # 上面定义的 foo()
```

`from` 形式的导入另一个常见的困惑是其对全局变量的影响。例如，考虑以下代码：

```
from spam import a, foo   # 导入一个全局变量
a = 42                    # 修改该变量
foo()                     # 打印 "I'm foo and a is 37"
print(a)                  # 打印 "42"
```

这里，重要的是要理解在 Python 中，变量赋值并非存储操作。也就是说，前面示例中对 `a` 的赋值并不是将一个新值存储在 `a` 中，覆盖之前的值。相反，它会创建一个包含值 42 的新对象，并使名称 `a` 引用该对象。此时，`a` 不再绑定到导入模块中的值，而是绑定到某个其他对象。由于这种行为，使用 `from` 语句无法使变量表现得类似于 C 或 Fortran 等语言中的全局变量或通用块。如果你希望在程序中有可变的全局程序参数，请将它们放在一个模块中，并使用 `import` 语句显式地通过模块名引用（即，显式使用 `spam.a`）。

#### 作为主程序执行

一个 Python 源文件可以通过两种方式执行。`import` 语句在其自身的命名空间中作为库模块执行代码。然而，代码也可能作为主程序或脚本执行。当你将程序作为脚本名提供给解释器时，就会发生这种情况：

```
% python spam.py
```

每个模块都定义了一个变量 `__name__`，其中包含模块名称。程序可以检查此变量以确定它们正在执行的模块。解释器的顶级模块名为 `__main__`。在命令行上指定或交互式输入的程序运行在 `__main__` 模块内。有时，程序可能会根据其是作为模块导入还是在 `__main__` 中运行而改变其行为。例如，一个模块可能包含一些测试代码，这些代码在模块作为主程序使用时执行，但如果模块只是被另一个模块导入，则不会执行。这可以通过以下方式实现：

```
##### 检查是否作为程序运行
if __name__ == '__main__':
    # 是
    语句
else:
    # 否，我一定是被作为模块导入了
    语句
```

对于旨在用作库的源文件，使用这种技术来包含可选的测试或示例代码是很常见的做法。例如，如果你正在开发一个

#### 模块搜索路径

加载模块时，解释器会搜索 `sys.path` 中的目录列表。`sys.path` 中的第一个条目通常是一个空字符串 `''`，它指向当前工作目录。`sys.path` 中的其他条目可能由目录名、`.zip` 归档文件和 `.egg` 文件组成。`sys.path` 中条目的顺序决定了加载模块时使用的搜索顺序。要向搜索路径添加新条目，只需将它们添加到此列表即可。

尽管路径通常包含目录名，但包含 Python 模块的 zip 归档文件也可以添加到搜索路径。这可能是将模块集合打包为单个文件的便捷方式。例如，假设你创建了两个模块 `foo.py` 和 `bar.py`，并将它们放入名为 `mymodules.zip` 的 zip 文件中。可以通过以下方式将该文件添加到 Python 搜索路径：

```
import sys
sys.path.append("mymodules.zip")
import foo, bar
```

也可以使用 zip 文件目录结构内的特定位置。此外，zip 文件可以与常规路径名组件混合使用。以下是一个示例：

```
sys.path.append("/tmp/modules.zip/lib/python")
```

除了 `.zip` 文件，你还可以将 `.egg` 文件添加到搜索路径。`.egg` 文件是由 setuptools 库创建的包。这是在安装第三方 Python 库和扩展时遇到的常见格式。`.egg` 文件实际上只是一个 `.zip` 文件，只是添加了一些额外的元数据（例如，版本号、依赖项等）。因此，你可以使用处理 `.zip` 文件的标准工具来检查和提取 `.egg` 文件中的数据。

尽管支持 zip 文件导入，但仍有一些限制需要注意。首先，只能从归档中导入 `.py`、`.pyw`、`.pyc` 和 `.pyo` 文件。用 C 编写的共享库和扩展模块无法直接从归档加载，尽管 setuptools 等打包系统有时能够提供解决方法（通常是通过将 C 扩展提取到临时目录并从该目录加载模块）。此外，当从归档加载 `.py` 文件时（下文将描述），Python 不会创建 `.pyc` 和 `.pyo` 文件。因此，重要的是确保提前创建这些文件并放置在归档中，以避免加载模块时性能不佳。

#### 模块加载与编译

到目前为止，本章一直将模块描述为包含纯 Python 代码的文件。然而，通过 `import` 加载的模块实际上大致分为四类：

- 用 Python 编写的代码（`.py` 文件）
- 已编译为共享库或 DLL 的 C 或 C++ 扩展
- 包含模块集合的包
- 用 C 编写并链接到 Python 解释器的内置模块

当查找模块（例如 `foo`）时，解释器会搜索 `sys.path` 中的每个目录，查找以下文件（按搜索顺序列出）：

1. 一个定义包的目录，`foo`
2. `foo.pyd`、`foo.so`、`foomodule.so` 或 `foomodule.dll`（编译后的扩展）
3. `foo.pyo`（仅当使用了 `-O` 或 `-OO` 选项时）
4. `foo.pyc`
5. `foo.py`（在 Windows 上，Python 也会检查 `.pyw` 文件。）

包将在下文简要描述；编译后的扩展将在第 26 章“扩展和嵌入 Python”中描述。对于 `.py` 文件，当模块首次导入时，它会被编译成字节码并作为 `.pyc` 文件写回磁盘。在后续导入时，解释器会加载这个预编译的字节码，除非 `.py` 文件的修改日期更新（在这种情况下，`.pyc` 文件会重新生成）。`.pyo` 文件与解释器的 `-O` 选项一起使用。这些文件包含去除了行号、断言和其他调试信息的字节码。因此，它们体积更小，并允许解释器运行得稍快一些。如果指定的是 `-OO` 选项而不是 `-O`，则文档字符串也会从文件中剥离。这种文档字符串的删除仅在创建 `.pyo` 文件时发生，而不是在加载时。如果 `sys.path` 的任何目录中都不存在这些文件，解释器会检查该名称是否对应于内置模块名称。如果没有匹配项，则会引发 `ImportError` 异常。

文件自动编译为 `.pyc` 和 `.pyo` 文件仅在与 `import` 语句一起使用时才会发生。在命令行或标准输入上指定的程序不会生成此类文件。此外，如果包含模块 `.py` 文件的目录不允许写入（例如，由于权限不足或它是 zip 归档的一部分），则不会创建这些文件。解释器的 `-B` 选项也会禁用这些文件的生成。

如果 `.pyc` 和 `.pyo` 文件可用，则不需要存在相应的 `.py` 文件。因此，如果你要打包代码但不希望包含源代码，你只需捆绑一组 `.pyc` 文件即可。然而，请注意 Python 对自省和反汇编有广泛的支持。知识丰富的用户即使没有源代码，仍然能够检查并发现关于你程序的许多细节。另外，请注意 `.pyc` 文件往往是特定于版本的。因此，为某个 Python 版本生成的 `.pyc` 文件可能在未来的发行版中无法工作。

当 `import` 搜索文件时，它会以区分大小写的方式匹配文件名——即使在底层文件系统不区分大小写的机器上，例如 Windows 和 OS X（不过，此类系统会保留大小写）。因此，`import foo` 只会导入文件 `foo.py`，而不会导入 `Foo.py` 然而，作为一般规则，你应该避免使用仅大小写不同的模块名。



#### 模块的重新加载与卸载

Python 并不真正支持对先前已导入的模块进行重新加载或卸载。虽然你可以从 `sys.modules` 中移除一个模块，但这通常并不会将模块从内存中卸载。这是因为对模块对象的引用可能仍然存在于其他使用 `import` 加载该模块的程序组件中。此外，如果存在该模块中定义的类的实例，这些实例会包含对其类对象的引用，而类对象又反过来持有对其定义所在模块的引用。

模块引用存在于多个地方这一事实，使得在修改模块实现后重新加载模块通常是不切实际的。例如，如果你从 `sys.modules` 中移除一个模块并使用 `import` 重新加载它，这并不会追溯性地更改程序中之前对该模块的所有引用。相反，你将拥有一个由最近的 `import` 语句创建的新模块引用，以及一组由代码其他部分的导入创建的旧模块引用。这很少是你想要的结果，并且除非你能够仔细控制整个执行环境，否则在任何合理的生产代码中使用它都是不安全的。

旧版本的 Python 提供了一个 `reload()` 函数用于重新加载模块。然而，使用该函数从未真正安全过（由于上述所有原因），除了作为可能的调试辅助手段外，其使用一直是被积极劝阻的。Python 3 完全移除了此功能。因此，最好不要依赖它。

最后，需要注意的是，C/C++ 扩展无法以任何方式安全地卸载或重新加载。Python 未提供对此的支持，而且底层操作系统也可能禁止这样做。因此，你唯一的办法是重启 Python 解释器进程。

#### 包

包允许将一组模块归集到一个共同的包名下。这种技术有助于解决不同应用程序中使用的模块名之间的命名冲突。包通过创建一个与包同名的目录，并在该目录中创建 `__init__.py` 文件来定义。然后，你可以根据需要在该目录中放置额外的源文件、编译扩展和子包。例如，一个包的组织结构可能如下所示：

```
Graphics/
    __init__.py
    Primitive/
        __init__.py
        lines.py
        fill.py
        text.py
        ...
    Graph2d/
        __init__.py
        plot2d.py
        ...
    Graph3d/
        __init__.py
        plot3d.py
        ...
    Formats/
        __init__.py
        gif.py
        png.py
        tiff.py
        jpeg.py
```

`import` 语句用于以多种方式从包中加载模块：

- `import Graphics.Primitive.fill`
  这将加载子模块 `Graphics.Primitive.fill`。该模块的内容必须显式命名，例如 `Graphics.Primitive.fill.floodfill(img, x, y, color)`。

- `from Graphics.Primitive import fill`
  这将加载子模块 `fill`，但使其无需包前缀即可使用；例如 `fill.floodfill(img, x, y, color)`。

- `from Graphics.Primitive.fill import floodfill`
  这将加载子模块 `fill`，但使 `floodfill` 函数可以直接访问；例如 `floodfill(img, x, y, color)`。

每当包的任何部分首次被导入时，`__init__.py` 文件中的代码就会被执行。最少情况下，该文件可以为空，但它也可以包含执行包特定初始化的代码。导入过程中遇到的所有 `__init__.py` 文件都会被执行。因此，前面展示的 `import Graphics.Primitive.fill` 语句将首先执行 `Graphics` 目录中的 `__init__.py` 文件，然后执行 `Primitive` 目录中的 `__init__.py` 文件。

包有一个特殊的问题，即以下语句的处理：

```
from Graphics.Primitive import *
```

使用此语句的程序员通常希望将与包关联的所有子模块导入当前命名空间。然而，由于文件命名约定因系统而异（特别是在大小写敏感性方面），Python 无法准确确定这些模块可能是什么。因此，此语句只导入 `Primitive` 目录中 `__init__.py` 文件中定义的所有名称。可以通过定义一个包含与该包关联的所有模块名称的列表 `__all__` 来修改此行为。该列表应在包的 `__init__.py` 文件中定义，如下所示：

```python
##### Graphics/Primitive/__init__.py
__all__ = ["lines", "text", "fill"]
```

现在，当用户发出 `from Graphics.Primitive import *` 语句时，所有列出的子模块都会按预期加载。

包的另一个微妙问题涉及子模块想要导入同一包内的其他子模块。例如，假设 `Graphics.Primitive.fill` 模块想要导入 `Graphics.Primitive.lines` 模块。为此，你可以简单地使用完全限定名称（例如 `from Graphics.Primitive import lines`）或使用如下所示的包相对导入：

```python
##### fill.py
from . import lines
```

在此示例中，语句 `from . import lines` 中的 `.` 指的是调用模块所在的同一目录。因此，该语句会在与 `fill.py` 文件相同的目录中查找模块 `lines`。应特别注意避免使用 `import module` 这样的语句来导入包子模块。在旧版本的 Python 中，`import module` 语句是指标准库模块还是包子模块并不明确。旧版本的 Python 会首先尝试从导入语句所在子模块的同一包目录中加载模块，如果未找到匹配项，则继续查找标准库模块。然而，在 Python 3 中，`import` 假定使用绝对路径，会直接尝试从标准库加载 `module`。相对导入能更清晰地表达你的意图。

相对导入也可用于加载同一包的不同目录中包含的子模块。例如，如果模块 `Graphics.Graph2d.plot2d` 想要导入 `Graphics.Primitive.lines`，它可以使用如下语句：

```python
##### plot2d.py
from ..Primitive import lines
```

这里，`..` 向上移动一级目录，`Primitive` 则进入另一个包目录。

相对导入只能使用 `from module import symbol` 形式的 import 语句来指定。因此，`import ..Primitive.lines` 或 `import .lines` 等语句是语法错误。此外，`symbol` 必须是有效的标识符。因此，`from .. import Primitive.lines` 这样的语句也是非法的。最后，相对导入只能在包内使用；使用相对导入来引用位于文件系统上不同目录中的模块是非法的。

仅导入包名称并不会导入包中包含的所有子模块。例如，以下代码无法工作：

```python
import Graphics
Graphics.Primitive.fill.floodfill(img, x, y, color)  # 失败！
```

然而，由于 `import Graphics` 语句会执行 `Graphics` 目录中的 `__init__.py` 文件，因此可以使用相对导入来自动加载所有子模块，如下所示：

```python
##### Graphics/__init__.py
from . import Primitive, Graph2d, Graph3d

##### Graphics/Primitive/__init__.py
from . import lines, fill, text, ...
```

现在 `import Graphics` 语句会导入所有子模块，并使它们可以通过完全限定名称使用。再次需要强调的是，应如示例所示使用包相对导入。如果你使用简单的语句如 `import module`，可能会加载标准库模块。

最后，当 Python 导入一个包时，它会定义一个特殊变量 `__path__`，其中包含查找包子模块时搜索的目录列表（`__path__` 是 `sys.path` 变量的包特定版本）。`__path__` 可由 `__init__.py` 文件中的代码访问，初始时包含一个包目录名称的条目。如有必要，包可以向 `__path__` 列表提供额外的目录，以更改用于查找子模块的搜索路径。如果包在文件系统上的组织结构复杂且与包层次结构不完全对应，这可能会很有用。



#### 分发 Python 程序和库

要将 Python 程序分发给他人，你应该使用 `distutils` 模块。作为准备工作，你应该先将你的作品整齐地组织到一个目录中，该目录应包含一个 README 文件、辅助文档以及你的源代码。通常，这个目录会包含库模块、包和脚本的混合体。模块和包是指将通过 `import` 语句加载的源文件。脚本是作为解释器主程序运行的程序（例如，以 `python scriptname` 的方式运行）。以下是一个包含 Python 代码的目录示例：

```
spam/
    README.txt
    Documentation.txt
    libspam.py      # A single library module
    spampkg/        # A package
        __init__.py
        foo.py
        bar.py
    runspam.py      # A script to run as: python runspam.py
```

你应该组织好你的代码，使其在顶层目录中运行 Python 解释器时能正常工作。例如，如果你在 `spam` 目录中启动 Python，你应该能够导入模块、导入包组件以及运行脚本，而无需更改 Python 的任何设置，如模块搜索路径。

在组织好代码之后，在最顶层的目录中创建一个 `setup.py` 文件（在前面的示例中即为 `spam` 目录）。在此文件中，放入以下代码：

```
##### setup.py
from distutils.core import setup

setup(name = "spam",
      version = "1.0",
      py_modules = ['libspam'],
      packages = ['spampkg'],
      scripts = ['runspam.py'],
      )
```

在 `setup()` 调用中，`py_modules` 参数是所有单文件 Python 模块的列表，`packages` 是所有包目录的列表，`scripts` 是脚本文件的列表。如果你的软件没有相应的组件（即没有脚本），可以省略其中任何一个参数。`name` 是你的包名称，`version` 是版本号字符串。

对 `setup()` 的调用还支持许多其他参数，用于提供关于包的各种元数据。表 8.1 列出了可以指定的最常用参数。所有值均为字符串，`classifiers` 参数除外，它是一个字符串列表，例如 `['Development Status :: 4 - Beta', 'Programming Language :: Python']`（完整列表可在 http://pypi.python.org 查找）。

**表 8.1 `setup()` 的参数**

| 参数 | 描述 |
|------|------|
| name | 包的名称（必填） |
| version | 版本号（必填） |
| author | 作者姓名 |
| author_email | 作者的电子邮件地址 |
| maintainer | 维护者姓名 |
| maintainer_email | 维护者的电子邮件 |
| url | 包的主页 |
| description | 包的简要描述 |
| long_description | 包的详细描述 |
| download_url | 可下载包的位置 |
| classifiers | 字符串分类器列表 |

创建 setup.py 文件就足以创建软件的源代码分发包。输入以下 shell 命令来创建源代码分发包：

```
% python setup.py sdist
...
%
```

这将在 spam/dist 目录中创建一个归档文件，如 spam-1.0.tar.gz 或 spam-1.0.zip。这就是你提供给他人用来安装你的软件的文件。要安装，用户只需解压归档文件并执行以下步骤：

```
% unzip spam-1.0.zip
...
% cd spam-1.0
% python setup.py install
...
%
```

这会将软件安装到本地 Python 发行版中，并使其可供通用使用。模块和包通常安装到 Python 库中名为 "site-packages" 的目录中。要找到该目录的确切位置，请查看 `sys.path` 的值。脚本通常安装到与 Python 解释器相同的目录中（在基于 UNIX 的系统上），或安装到 Windows 上的 "Scripts" 目录中（在典型安装中位于 "C:\Python26\Scripts"）。

在 UNIX 上，如果脚本的第一行以 #! 开头并包含 "python" 文本，安装程序会重写该行以指向本地安装的 Python。因此，如果你编写的脚本中硬编码了特定的 Python 位置，如 /usr/local/bin/python，它们在安装到 Python 位于不同位置的其他系统时仍然应该可以正常工作。

setup.py 文件还有许多关于软件分发的其他命令。如果你输入 'python setup.py bdist'，将创建一个二进制分发包，其中所有 .py 文件已预先编译为 .pyc 文件，并放置在模拟本地平台的目录结构中。只有当你的应用程序的部分组件依赖于特定平台时（例如，如果你还有需要编译的 C 扩展），才需要这种分发方式。如果你在 Windows 机器上运行 'python setup.py bdist_wininst'，将创建一个 .exe 文件。打开后，将启动一个 Windows 安装程序对话框，提示用户输入软件应安装到的位置信息。这种分发方式还会向注册表中添加条目，便于日后卸载你的包。

distutils 模块假定用户的机器上已经安装了 Python（单独下载）。虽然可以创建将 Python 运行时和你的软件捆绑成单个二进制可执行文件的软件包，但这超出了本文所能涵盖的范围（有关更多细节，请查看第三方模块如 `py2exe` 或 `py2app`）。如果你要做的只是向他人分发库或简单脚本，通常没有必要将你的代码与 Python 解释器和运行时一起打包。

最后，应该注意的是，`distutils` 还有比本文所涵盖的更多的选项。第 26 章描述了如何使用 `distutils` 编译 C 和 C++ 扩展。

虽然不属于标准 Python 发行版的一部分，但 Python 软件经常以 `.egg` 文件的形式分发。这种格式是由流行的 `setuptools` 扩展（http://pypi.python.org/pypi/setuptools）创建的。要支持 `setuptools`，你只需将 `setup.py` 文件的开头部分更改为如下形式：

```
##### setup.py
try:
    from setuptools import setup
except ImportError:
    from distutils.core import setup

setup(name = "spam",
    ...
)
```

#### 安装第三方库

查找第三方库和 Python 扩展的权威资源是 *Python Package Index*（*PyPI*），其位于 http://pypi.python.org。安装第三方模块通常很简单，但对于非常大的包（尤其是那些还依赖于其他第三方模块的包），过程可能会变得相当复杂。对于较主要的扩展，你通常会找到一个平台原生的安装程序，它会通过一系列对话屏幕引导你完成安装过程。对于其他模块，你通常需要解压下载内容，找到 `setup.py` 文件，然后输入 `python setup.py install` 来安装软件。

默认情况下，第三方模块安装在 Python 标准库的 `site-packages` 目录中。访问此目录通常需要 root 或管理员权限。如果没有相应权限，你可以输入 `python setup.py install --user`，将模块安装到用户级的库目录中。这会将包安装到用户级目录中，例如 UNIX 上的 `"/Users/beazley/.local/lib/python2.6/site-packages"`。

如果你想将软件安装到完全不同的位置，请使用 `setup.py` 的 `--prefix` 选项。例如，输入 `python setup.py install --prefix=/home/beazley/pypackages` 会将模块安装到 `/home/beazley/pypackages` 目录下。安装到非标准位置时，你可能需要调整 `sys.path` 的设置，以便 Python 能够找到新安装的模块。

请注意，许多 Python 扩展涉及 C 或 C++ 代码。如果你下载的是源代码分发包，你的系统必须安装了 C++ 编译器才能运行安装程序。在 UNIX、Linux 和 OS X 上，这通常不是问题。在 Windows 上，传统上需要安装 Microsoft Visual Studio。如果你在 Windows 平台上工作，最好寻找扩展的预编译版本。



### 9 输入与输出

本章介绍Python输入与输出（I/O）的基础知识，包括命令行选项、环境变量、文件I/O、Unicode，以及如何使用pickle模块序列化对象。

#### 读取命令行选项

当Python启动时，命令行选项被放置在列表`sys.argv`中。第一个元素是程序的名称。后续项是程序名后命令行上给出的选项。以下程序展示了手动处理简单命令行参数的最小原型：

```
import sys
if len(sys.argv) != 3:
    sys.stderr.write("Usage : python %s inputfile outputfile\n" % sys.argv[0])
    raise SystemExit(1)
inputfile  = sys.argv[1]
outputfile = sys.argv[2]
```

在此程序中，`sys.argv[0]`包含正在执行的脚本名称。将错误消息写入`sys.stderr`并引发一个具有非零退出码的`SystemExit`，如所示，是报告命令行工具使用错误的标准做法。

尽管你可以为简单脚本手动处理命令选项，但对于更复杂的命令行处理，请使用`optparse`模块。以下是一个简单示例：

```
import optparse
p = optparse.OptionParser()

##### An option taking an argument
p.add_option("-o",action="store",dest="outfile")
p.add_option("--output",action="store",dest="outfile")

##### An option that sets a boolean flag
p.add_option("-d",action="store_true",dest="debug")
p.add_option("--debug",action="store_true",dest="debug")

##### Set default values for selected options
p.set_defaults(debug=False)

##### Parse the command line
opts, args = p.parse_args()

##### Retrieve the option settings
outfile   = opts.outfile
debugmode = opts.debug
```

在这个示例中，添加了两种类型的选项。第一个选项 `-o` 或 `--output` 需要一个参数。这种行为是通过在调用 `p.add_option()` 时指定 `action='store'` 来选择的。第二个选项 `-d` 或 `--debug` 只是设置一个布尔标志。这是通过在 `p.add_option()` 中指定 `action='store_true'` 来启用的。`p.add_option()` 的 `dest` 参数选择了一个属性名，解析后的参数值将存储在那里。`p.set_defaults()` 方法为一个或多个选项设置默认值。此方法使用的参数名称应与为每个选项选择的目标名称匹配。如果未选择默认值，则默认值设置为 `None`。

前面的程序识别所有以下命令行样式：

```
% python prog.py -o outfile -d infile1 ... infileN
% python prog.py --output=outfile --debug infile1 ... infileN
% python prog.py -h
% python prog.py --help
```

解析使用 `p.parse_args()` 方法执行。此方法返回一个二元组 `(opts, args)`，其中 `opts` 是一个包含已解析选项值的对象，`args` 是一个列表，包含命令行中未解析为选项的项目。选项值使用 `opts.dest` 检索，其中 *dest* 是添加选项时使用的目标名称。例如，`-o` 或 `--output` 参数的参数值被放置在 `opts.outfile` 中，而 `args` 是剩余参数的列表，如 `['infile1', ..., 'infileN']`。`optparse` 模块自动提供 `-h` 或 `--help` 选项，如果用户请求，会列出可用的选项。错误的选项也会导致错误消息。

此示例仅展示了 `optparse` 模块的最简单用法。关于一些更高级选项的更多细节可以在第19章“操作系统服务”中找到。

#### 环境变量

环境变量通过字典 `os.environ` 访问。以下是一个示例：

```
import os
path   = os.environ["PATH"]
user   = os.environ["USER"]
editor = os.environ["EDITOR"]
... etc ...
```

要修改环境变量，请设置 `os.environ` 变量。例如：

```
os.environ["FOO"] = "BAR"
```

对 `os.environ` 的修改会影响运行中的程序以及Python创建的子进程。

#### 文件与文件对象

内置函数 `open(name [,mode [,bufsize]])` 打开并创建一个文件对象，如下所示：

```
f = open("foo")       # Opens "foo" for reading
f = open("foo",'r')   # Opens "foo" for reading (same as above)
f = open("foo",'w')   # Open for writing
```

文件模式 `'r'` 表示读取，`'w'` 表示写入，`'a'` 表示追加。这些文件模式假定为文本模式，并可能隐式执行换行符 `'\n'` 的转换。例如，在Windows上，写入字符 `'\n'` 实际上会输出两个字符的序列 `'\r\n'`（并且在读取文件时，`'\r\n'` 会被转换回单个 `'\n'` 字符）。如果你处理的是二进制数据，请在文件模式后附加 `'b'`，例如 `'rb'` 或 `'wb'`。这会禁用换行符转换，如果关注处理二进制数据的代码的可移植性（在UNIX上，省略 `'b'` 是一个常见错误，因为文本文件和二进制文件之间没有区别），则应包含此字符。此外，由于模式的区别，你可能会看到文本模式指定为 `'rt'`、`'wt'` 或 `'at'`，这更清楚地表达了你的意图。

可以通过提供一个加号（`+`）字符来打开一个文件以进行就地更新，例如 `'r+'` 或 `'w+'`。当文件以更新模式打开时，只要所有输出操作在随后的任何输入操作之前刷新其数据，你就可以执行输入和输出。如果文件以 `'w+'` 模式打开，其长度首先被截断为零。

如果文件以模式 `'U'` 或 `'rU'` 打开，它提供用于读取的通用换行支持。此功能通过将不同的换行符编码（例如 `'\n'`、`'\r'` 和 `'\r\n'`）转换为各种文件I/O函数返回的字符串中的标准 `'\n'` 字符，简化了跨平台工作。例如，如果你在UNIX系统上编写必须处理Windows程序生成的文本文件的脚本，这将非常有用。

可选的 `bufsize` 参数控制文件的缓冲行为，其中0表示无缓冲，1表示行缓冲，负数表示请求系统默认值。任何其他正数表示将使用的大约缓冲区大小（以字节为单位）。

Python 3为 `open()` 函数增加了四个额外参数，调用方式为 `open(name [,mode [,bufsize [, encoding [, errors [, newline [, closefd]]]]])`。`encoding` 是编码名称，例如 `'utf-8'` 或 `'ascii'`。`errors` 是用于编码错误的错误处理策略（有关更多信息，请参见本章后面关于Unicode的部分）。`newline` 控制通用换行模式的行为，可以设置为 `None`、`''`、`'\n'`、`'\r'` 或 `'\r\n'`。如果设置为 `None`，则任何形式为 `'\n'`、`'\r'` 或 `'\r\n'` 的行尾都会被转换为 `'\n'`。如果设置为 `''`（空字符串），则这些行尾中的任何一种都会被识别为换行符，但在输入文本中保持未转换状态。如果 `newline` 具有任何其他合法值，则该值用于终止行。`closefd` 控制当调用 `close()` 方法时底层文件描述符是否实际关闭。默认情况下，此项设置为 `True`。

表9.1显示了 `file` 对象支持的方法。

##### 表9.1 文件方法

| 方法 | 描述 |
|--------|-------------|
| `f.read([n])` | 读取最多 *n* 个字节。 |
| `f.readline([n])` | 读取最多 *n* 个字符的单行输入。如果省略 *n*，则此方法读取整行。 |
| `f.readlines([size])` | 读取所有行并返回一个列表。*size* 可选地指定在停止前从文件中读取的大约字符数。 |
| `f.write(s)` | 写入字符串 *s*。 |
| `f.writelines(lines)` | 按顺序写入序列 *lines* 中的所有字符串。 |
| `f.close()` | 关闭文件。 |



## 第9章 输入与输出

##### 表 9.1 续

| 方法 | 描述 |
| --- | --- |
| f.tell() | 返回当前文件指针的位置。 |
| f.seek(offset [, whence]) | 移动到新的文件位置。 |
| f.isatty() | 如果 `f` 是一个交互式终端，则返回1。 |
| f.flush() | 刷新输出缓冲区。 |
| f.truncate([size]) | 将文件截断至多 `size` 字节。 |
| f.fileno() | 返回一个整数文件描述符。 |
| f.next() | 返回下一行，或者引发 `StopIteration` 异常。在 Python 3 中，它被称为 `f.__next__()`。 |

`read()` 方法将整个文件作为字符串返回，除非给出了一个可选的长度参数来指定最大字符数。`readline()` 方法返回下一行输入，包括结尾的换行符；`readlines()` 方法将所有输入行作为字符串列表返回。`readline()` 方法可选地接受一个最大行长度 `n`。如果读取的行超过 `n` 个字符，则返回前 `n` 个字符。剩余的行数据不会被丢弃，并将在后续的读取操作中返回。`readlines()` 方法接受一个 `size` 参数，该参数指定了在停止前要读取的大约字符数。实际读取的字符数可能大于此值，具体取决于缓冲了多少数据。

`readline()` 和 `readlines()` 方法都能感知平台并正确处理不同换行符的表示（例如，`'\n'` 与 `'\r\n'`）。如果文件以通用换行模式（`'U'` 或 `'rU'`）打开，则换行符会被转换为 `'\n'`。

`read()` 和 `readline()` 通过返回空字符串来表示文件结束（EOF）。因此，以下代码展示了如何检测 EOF 条件：

```
while True:
    line = f.readline()
    if not line:      # EOF
        break
```

一种读取文件所有行的便捷方法是使用 `for` 循环进行迭代。例如：

```
for line in f:     # 遍历文件中的所有行
    # 对 line 进行一些操作
    ...
```

请注意，在 Python 2 中，各种读取操作总是返回8位字符串，无论指定的文件模式是文本模式还是二进制模式。在 Python 3 中，如果文件以文本模式打开，这些操作返回 Unicode 字符串；如果文件以二进制模式打开，则返回字节串。

`write()` 方法将字符串写入文件，而 `writelines()` 方法将字符串列表写入文件。`write()` 和 `writelines()` 不会在输出中添加换行符，因此你产生的所有输出都应该已经包含了所有必要的格式化。这些方法可以将原始字节串写入文件，但前提是文件必须以二进制模式打开。

在内部，每个文件对象维护一个文件指针，该指针存储下一次读写操作发生的字节偏移量。`tell()` 方法将当前文件指针的值作为长整数返回。`seek()` 方法用于根据给定的 `offset` 和 `whence` 中的位置规则随机访问文件的某些部分。如果 `whence` 为 0（默认值），`seek()` 假设 `offset` 相对于文件开头；如果 `whence` 为 1，则相对于当前位置移动；如果 `whence` 为 2，则偏移量取自文件末尾。`seek()` 将新的文件指针值作为整数返回。应注意的是，文件指针与 `open()` 返回的文件对象相关联，而不是与文件本身相关联。同一个文件可以在同一个程序（或不同程序）中被多次打开。每个打开的文件实例都有自己的文件指针，可以独立操作。

`fileno()` 方法返回文件的整数文件描述符，有时在某些库模块的底层 I/O 操作中使用。例如，`fcntl` 模块使用文件描述符在 UNIX 系统上提供底层文件控制操作。

文件对象还具有表 9.2 所示的只读数据属性。

| 属性 | 描述 |
|-----------|-------------|
| `f.closed` | 布尔值表示文件状态：如果文件打开则为 `False`，如果关闭则为 `True`。 |
| `f.mode` | 文件的 I/O 模式。 |
| `f.name` | 如果使用 `open()` 创建，则为文件名。否则，它将是一个指示文件来源的字符串。 |
| `f.softspace` | 布尔值，指示在使用 `print` 语句时，另一个值之前是否需要打印空格字符。模拟文件的类必须提供一个可写的同名属性，该属性最初初始化为零（仅限 Python 2）。 |
| `f.newlines` | 当文件以通用换行模式打开时，此属性包含文件中实际找到的换行符表示。如果没有遇到换行符，则值为 `None`；如果遇到换行符，则为包含 `'\n'`、`'\r'` 或 `'\r\n'` 的字符串，或包含所有不同换行符编码的元组。 |
| `f.encoding` | 一个指示文件编码（如果有）的字符串（例如，`'latin-1'` 或 `'utf-8'`）。如果没有使用编码，则值为 `None`。 |

#### 标准输入、输出和错误

解释器提供三个标准文件对象，称为*标准输入*、*标准输出*和*标准错误*，它们分别作为 `sys.stdin`、`sys.stdout` 和 `sys.stderr` 在 `sys` 模块中可用。`stdin` 是与提供给解释器的输入字符流相对应的文件对象。`stdout` 是接收 `print` 产生的输出的文件对象。`stderr` 是接收错误消息的文件。通常，`stdin` 映射到用户的键盘，而 `stdout` 和 `stderr` 在屏幕上生成文本。

前面章节中描述的方法可用于与用户进行原始 I/O。例如，以下代码写入标准输出，并从标准输入读取一行输入：

```
import sys
sys.stdout.write("Enter your name : ")
name = sys.stdin.readline()
```

或者，内置函数 `raw_input(prompt)` 可以从 `stdin` 读取一行文本，并可选地打印一个提示：

```
name = raw_input("Enter your name : ")
```

`raw_input()` 读取的行不包括末尾的换行符。这与直接从 `sys.stdin` 读取不同，后者在输入文本中包含换行符。在 Python 3 中，`raw_input()` 已被重命名为 `input()`。

键盘中断（通常由 Ctrl+C 生成）会导致一个 `KeyboardInterrupt` 异常，可以使用异常处理器捕获。

如有必要，可以用其他文件对象替换 `sys.stdout`、`sys.stdin` 和 `sys.stderr` 的值，此时 `print` 语句和输入函数将使用新的值。如果需要恢复 `sys.stdout` 的原始值，则应先将其保存。解释器启动时 `sys.stdout`、`sys.stdin` 和 `sys.stderr` 的原始值也分别在 `sys.__stdout__`、`sys.__stdin__` 和 `sys.__stderr__` 中可用。

请注意，在某些情况下，`sys.stdin`、`sys.stdout` 和 `sys.stderr` 可能会因为使用集成开发环境（IDE）而被更改。例如，当 Python 在 IDLE 下运行时，`sys.stdin` 会被替换为一个行为类似文件但实际上是开发环境中对象的对象。在这种情况下，某些底层方法（如 `read()` 和 `seek()`）可能不可用。

#### print 语句

Python 2 使用一个特殊的 `print` 语句在 `sys.stdout` 包含的文件上生成输出。`print` 接受一个以逗号分隔的对象列表，如下所示：

```
print "The values are", x, y, z
```

对于每个对象，会调用 `str()` 函数来生成一个输出字符串。然后，这些输出字符串被连接起来并用单个空格分隔以生成最终的输出字符串。除非给 `print` 语句提供了尾随逗号，否则输出会以换行符终止。在这种情况下，下一个 `print` 语句将在打印更多项目之前插入一个空格。这个空格的输出由用于输出的文件的 `softspace` 属性控制。

```
print "The values are ", x, y, z, w
##### 使用两个 print 语句打印相同的文本
print "The values are ", x, y,   # 省略末尾的换行符
print z, w                       # 在 z 之前打印一个空格
```

要生成格式化输出，请使用字符串格式化运算符（`%`）或 `.format()` 方法，如第4章“运算符与表达式”中所述。这里有一个例子：

```
print "The values are %d %7.5f %s" % (x,y,z) # 格式化 I/O
print "The values are {0:d} {1:7.5f} {2}".format(x,y,z)
```

您可以通过添加特殊的 `>>file` 修饰符后跟一个逗号来改变 `print` 语句的输出目标，其中 `file` 是一个允许写入的文件对象。以下是一个示例：

```
f = open("output","w")
print >>f, "hello world"
...
f.close()
```

#### print() 函数

Python 3 中最显著的变化之一是 `print` 被转变为一个函数。在 Python 2.6 中，如果在使用的每个模块中包含语句 `from __future__ import print_function`，也可以将 `print` 作为函数使用。`print()` 函数的工作方式与上一节描述的 `print` 语句几乎完全相同。

要打印一系列由空格分隔的值，只需将它们全部提供给 `print()`，如下所示：

```
print("The values are", x, y, z)
```

要抑制或更改行结束符，请使用 `end=ending` 关键字参数。例如：

```
print("The values are", x, y, z, end='')    # 抑制换行符
```

要将输出重定向到文件，请使用 `file=outfile` 关键字参数。例如：

```
print("The values are", x, y, z, file=f)    # 重定向到文件对象 f
```

要更改项目之间的分隔符，请使用 `sep=sepchr` 关键字参数。例如：

```
print("The values are", x, y, z, sep=',')    # 在值之间放置逗号
```

#### 文本输出中的变量插值

生成输出时的一个常见问题是产生包含嵌入式变量替换的大型文本片段。许多脚本语言（如 Perl 和 PHP）允许使用美元符号变量替换（即 `$name`、`$address` 等）将变量插入字符串中。Python 没有直接等效的功能，但可以使用格式化 I/O 结合三引号字符串来模拟。例如，您可以编写一个简短的格式化信函，填入姓名、物品名称和金额，如下例所示：

```
##### 注意：""" 之后的尾随反斜杠可防止
##### 空行作为第一行出现
form = """\
Dear  %(name)s,
Please send back my %(item)s or pay me $%(amount)0.2f.
                                     Sincerely yours,
                                      Joe Python User
"""
print form % { 'name': 'Mr. Bush',
            'item': 'blender',
            'amount': 50.00,
            }
```

这将产生以下输出：

> Dear Mr. Bush,
>
> Please send back my blender or pay me $50.00.
>
>                               Sincerely yours,
>
>                               Joe Python User

`format()` 方法是一种更现代的替代方案，它清理了之前的代码。例如：

```
form = """\
Dear {name},
Please send back my {item} or pay me {amount:0.2f}.
                                     Sincerely yours,
                                      
                                      Joe Python User
"""
print form.format(name='Mr. Bush', item='blender', amount=50.0)
```

对于某些类型的表单，您也可以使用模板字符串，如下所示：

```
import string
form = string.Template("""\
Dear $name,
Please send back my $item or pay me $amount.
                                     Sincerely yours,
                                      
                                      Joe Python User
""")
print form.substitute({'name': 'Mr. Bush',
            'item': 'blender',
            'amount': "%0.2f" % 50.0})
```

在这种情况下，字符串中的特殊 `$` 变量表示替换。`form.substitute()` 方法接受一个替换字典并返回一个新字符串。尽管前面的方法很简单，但它们并不总是文本生成的最佳解决方案。Web 框架和其他大型应用程序框架往往会提供自己的模板字符串引擎，支持嵌入式控制流、变量替换、文件包含和其他高级功能。

#### 生成输出

直接使用文件是程序员最熟悉的 I/O 模型。然而，生成器函数也可用于将 I/O 流作为一系列数据片段发出。要执行此操作，只需使用 `yield` 语句，就像使用 `write()` 或 `print` 语句一样。以下是一个示例：

```
def countdown(n):
    while n > 0:
        yield "T-minus %d\n" % n
        n -= 1
    yield "Kaboom!\n"
```

以这种方式生成输出流提供了极大的灵活性，因为输出流的产生与实际将流定向到其预期目的地的代码是分离的。例如，如果您想将上述输出路由到文件 `f`，可以这样做：

```
count = countdown(5)
f.writelines(count)
```

相反，如果您想通过套接字 `s` 重定向输出，可以这样做：

```
for chunk in count:
    s.sendall(chunk)
```

或者，如果您只想将所有输出捕获到字符串中，可以这样做：

```
out = "".join(count)
```

更高级的应用程序可以使用这种方法来实现自己的 I/O 缓冲。例如，生成器可能正在发出小型文本片段，但另一个函数可能正在将这些片段收集到大型缓冲区中，以创建更大、更高效的 I/O 操作：

```
chunks = []
buffered_size = 0
for chunk in count:
    chunks.append(chunk)
    buffered_size += len(chunk)
    if buffered_size >= MAXBUFFERSIZE:
        outf.write("".join(chunks))
        chunks.clear()
        buffered_size = 0
outf.write("".join(chunks))
```

对于将输出路由到文件或网络连接的程序，生成器方法还可以显著减少内存使用，因为整个输出流通常可以以小片段的形式生成和处理，而不是首先收集到一个大的输出字符串或字符串列表中。当编写与 Python Web 服务网关接口（WSGI）交互的程序时，有时会看到这种输出方法，WSGI 用于某些 Web 框架中组件之间的通信。

#### Unicode 字符串处理

与 I/O 处理相关的一个常见问题是处理表示为 Unicode 的国际字符。如果您有一个原始字节字符串 `s`，其中包含 Unicode 字符串的编码表示，请使用 `s.decode([encoding [,errors]])` 方法将其转换为适当的 Unicode 字符串。要将 Unicode 字符串 `u` 转换为编码的字节字符串，请使用字符串方法 `u.encode([encoding [,errors]])`。这两个转换运算符都需要使用一个特殊的编码名称，该名称指定 Unicode 字符值如何映射到字节字符串中的 8 位字符序列，反之亦然。编码参数指定为一个字符串，是超过一百种不同字符编码之一。然而，以下值是最常见的：

| 值 | 描述 |
|-------|-------------|
| 'ascii' | 7 位 ASCII |
| 'latin-1' 或 'iso-8859-1' | ISO 8859-1 Latin-1 |
| 'cp1252' | Windows 1252 编码 |
| 'utf-8' | 8 位可变长度编码 |
| 'utf-16' | 16 位可变长度编码（可能是小端或大端） |
| 'utf-16-le' | UTF-16，小端编码 |
| 'utf-16-be' | UTF-16，大端编码 |
| 'unicode-escape' | 与 Unicode 字面量 `u"string"` 格式相同 |
| 'raw-unicode-escape' | 与原始 Unicode 字面量 `ur"string"` 格式相同 |

默认编码在 `site` 模块中设置，可以使用 `sys.getdefaultencoding()` 查询。在许多情况下，默认编码是 `'ascii'`，这意味着值范围在 `[0x00, 0x7f]` 的 ASCII 字符直接映射到范围在 `[U+0000, U+007F]` 的 Unicode 字符。但是，`'utf-8'` 也是非常常见的设置。有关常见编码的技术细节将在后面的部分中介绍。

使用 `s.decode()` 方法时，总是假设 `s` 是一个字节字符串。在 Python 2 中，这意味着 `s` 是一个标准字符串，但在 Python 3 中，`s` 必须是一个特殊的 `bytes` 类型。同样，`t.encode()` 的结果总是一个字节序列。如果您关心可移植性，需要注意的一点是，这些方法在 Python 2 中有点混乱。例如，Python 2 字符串既有 `decode()` 方法也有 `encode()` 方法，而在 Python 3 中，字符串只有 `encode()` 方法，而 `bytes` 类型只有 `decode()` 方法。为了简化 Python 2 中的代码，请确保只在 Unicode 字符串上使用 `encode()`，在字节字符串上使用 `decode()`。

当转换字符串值时，如果遇到无法转换的字符，可能会引发 `UnicodeError` 异常。例如，如果您尝试将字符串编码为 `'ascii'`，而它包含像 `U+1F28` 这样的 Unicode 字符，您将得到一个编码错误，因为该字符值太大，无法在 ASCII 字符集中表示。`encode()` 和 `decode()` 方法的 `errors` 参数决定了如何处理编码错误。它是一个具有以下值之一的字符串：

| 值 | 描述 |
|-------|-------------|
| 'strict' | 对于编码和解码错误，引发 `UnicodeError` 异常。 |
| 'ignore' | 忽略无效字符。 |
| 'replace' | 用替换字符（Unicode 中为 `U+FFFD`，标准字符串中为 `'?'`）替换无效字符。 |
| 'backslashreplace' | 用 Python 字符转义序列替换无效字符。例如，字符 `U+1234` 被替换为 `'\\u1234'`。 |
| 'xmlcharrefreplace' | 用 XML 字符引用替换无效字符。例如，字符 `U+1234` 被替换为 `'&#4660;'`。 |



默认的错误处理方式是 `'strict'`。

`'xmlcharrefreplace'` 错误处理策略通常是一种将国际字符嵌入网页中 ASCII 编码文本的实用方式。例如，如果你使用 `'xmlcharrefreplace'` 处理将 Unicode 字符串 `'Jalape\u00f1o'` 编码为 ASCII 输出，浏览器几乎总是能正确地将输出文本渲染为 "Jalapeño"，而不是某种乱码替代文本。

为了让你的脑袋不至于爆炸，编码的字节串和未编码的字符串永远不应该在表达式中混合使用（例如，使用 `+` 进行拼接）。Python 3 完全禁止这种做法，但 Python 2 会默默地继续执行此类操作，根据默认编码设置自动将字节串提升为 Unicode。这种行为常常是产生意外结果或莫名其妙的错误信息的根源。因此，你应该仔细地在程序中严格区分编码字符数据和未编码字符数据。

#### Unicode I/O

处理 Unicode 字符串时，永远不可能直接将原始 Unicode 数据写入文件。这是因为 Unicode 字符在内部表示为多字节整数，直接将这些整数写入输出流会导致与字节顺序相关的问题。例如，你必须随意决定 Unicode 字符 U+HHLL 是以"小端"格式写为字节序列 LL HH，还是以"大端"格式写为字节序列 HH LL。此外，处理 Unicode 的其他工具也必须知道你使用了哪种编码。

由于这个问题，Unicode 字符串的外部表示总是按照特定的编码规则完成，该规则精确定义了 Unicode 字符如何表示为字节序列。因此，为了支持 Unicode I/O，上一节描述的编码和解码概念被扩展到了文件。内置的 codecs 模块包含了一组函数，用于根据各种不同的数据编码方案在字节导向数据和 Unicode 字符串之间进行转换。

处理 Unicode 文件最直接的方式也许是使用 `codecs.open(filename [, mode [, encoding [, errors]]])` 函数，如下所示：

```python
f = codecs.open('foo.txt','r','utf-8','strict')    # Reading
g = codecs.open('bar.txt','w','utf-8')             # Writing
```

这会创建一个读取或写入 Unicode 字符串的文件对象。`encoding` 参数指定底层字符编码，用于在读写文件时转换数据。`errors` 参数决定如何处理错误，其值为 `'strict'`、`'ignore'`、`'replace'`、`'backslashreplace'` 或 `'xmlcharrefreplace'` 之一，如上一节所述。

如果你已经有一个文件对象，可以使用 `codecs.EncodedFile(file, inputenc [, outputenc [, errors]])` 函数为其添加编码包装器。以下是一个示例：

```python
f = open("foo.txt","rb")
...
fenc = codecs.EncodedFile(f,'utf-8')
```

在这种情况下，从文件读取的数据将根据 `inputenc` 中提供的编码进行解释。写入文件的数据将根据 `inputenc` 中的编码进行解释，并根据 `outputenc` 中的编码写入。如果省略 `outputenc`，则默认与 `inputenc` 相同。`errors` 的含义与前面描述的相同。在将 `EncodedFile` 包装器包裹在现有文件上时，请确保该文件处于二进制模式。否则，换行符转换可能会破坏编码。

处理 Unicode 文件时，数据编码通常嵌入在文件本身中。例如，XML 解析器可能会查看字符串 `'<?xml ...>'` 的前几个字节来确定文档编码。如果前四个值是 `3C 3F 78 6D`（'`<?xm`'），则假定编码为 UTF-8。如果前四个值是 `00 3C 00 3F` 或 `3C 00 3F 00`，则分别假定编码为 UTF-16 大端或 UTF-16 小端。或者，文档编码可能出现在 MIME 头中或其他文档元素的属性中。以下是一个示例：

```xml
<?xml ... encoding="ISO-8859-1" ... ?>
```

类似地，Unicode 文件也可能包含特殊的字节顺序标记（BOM），用于指示字符编码的属性。Unicode 字符 `U+FEFF` 保留用于此目的。通常，该标记被写为文件中的第一个字符。然后程序读取该字符并查看字节的排列方式来确定编码（例如，`'\xff\xfe'` 表示 UTF-16-LE，`'\xfe\xff'` 表示 UTF-16-BE）。一旦确定了编码，BOM 字符就会被丢弃，然后处理文件的其余部分。不幸的是，所有这些额外的 BOM 处理并不是在幕后自动发生的。如果应用程序需要，你通常必须自己处理这些。

当从文档中读取编码时，可以使用类似以下的代码将输入文件转换为编码流：

```python
f = open("somefile","rb")
##### Determine encoding of the file
...
##### Put an appropriate encoding wrapper on the file.
##### Assumes that the BOM (if any) has already been discarded
# by earlier statements.
fenc = codecs.EncodedFile(f,encoding)
data = fenc.read()
```

#### Unicode 数据编码

表 9.3 列出了 `codecs` 模块中一些最常用的编码器。

| 编码器 | 描述 |
|---|---|
| `'ascii'` | ASCII 编码 |
| `'latin-1'`、`'iso-8859-1'` | Latin-1 或 ISO-8859-1 编码 |
| `'cp437'` | CP437 编码 |
| `'cp1252'` | CP1252 编码 |
| `'utf-8'` | 8 位可变长度编码 |
| `'utf-16'` | 16 位可变长度编码 |
| `'utf-16-le'` | UTF-16，但使用显式小端编码 |
| `'utf-16-be'` | UTF-16，但使用显式大端编码 |
| `'unicode-escape'` | 与 u"string" 相同的格式 |
| `'raw-unicode-escape'` | 与 ur"string" 相同的格式 |

以下各节将更详细地描述每种编码器。

##### 'ascii' 编码

在 'ascii' 编码中，字符值被限制在范围 [0x00, 0x7f] 和 [U+0000, U+007F] 内。超出此范围的任何字符都是无效的。

##### 'iso-8859-1'、'latin-1' 编码

字符可以是范围 [0x00, 0xff] 和 [U+0000, U+00FF] 内的任何 8 位值。范围 [0x00, 0x7f] 内的值对应于 ASCII 字符集中的字符。范围 [0x80, 0xff] 内的值对应于 ISO-8859-1 或扩展 ASCII 字符集中的字符。超出范围 [0x00, 0xff] 的任何字符值都会导致错误。

##### 'cp437' 编码

这种编码类似于 'iso-8859-1'，但它是 Python 在 Windows 上作为控制台应用程序运行时使用的默认编码。范围 [x80, 0xff] 内的某些字符对应于旧版 DOS 应用程序中用于渲染菜单、窗口和边框的特殊符号。

##### 'cp1252' 编码

这是一种与 'iso-8859-1' 非常相似的编码，用于 Windows。然而，这种编码定义了范围 [0x80-0x9f] 内的字符，这些字符在 'iso-8859-1' 中未定义，并且在 Unicode 中具有不同的码位。

##### 'utf-8' 编码

UTF-8 是一种可变长度编码，允许表示所有 Unicode 字符。单个字节用于表示范围 0–127 内的 ASCII 字符。所有其他字符由 2 或 3 个字节的多字节序列表示。这些字节的编码如下所示：

对于 2 字节序列，第一个字节始终以位序列 110 开头。对于 3 字节序列，第一个字节以位序列 1110 开头。多字节序列中所有后续的数据字节都以位序列 10 开头。

在完全通用的情况下，UTF-8 格式允许多达 6 字节的多字节序列。在 Python 中，4 字节 UTF-8 序列用于编码一对称为*代理对*的 Unicode 字符。两个字符的值都在范围 `[U+D800, U+DFFF]` 内，组合在一起编码一个 20 位的字符值。代理编码如下：4 字节序列 `11110nnn 10nnnnnn 10nnnnnn 10mmmmmm` 被编码为一对 `U+D800 + N`、`U+DC00 + M`，其中 `N` 是 4 字节 UTF-8 序列中编码的 20 位字符的高 10 位，`M` 是低 10 位。五字节和六字节 UTF-8 序列（分别以位序列 `111110` 和 `1111110` 开头）用于编码最长 32 位的字符值。这些值不受 Python 支持，目前如果出现在编码数据流中会导致 `UnicodeError` 异常。

UTF-8 编码具有许多有用的特性，使其可以被旧版软件使用。首先，标准 ASCII 字符以其标准编码表示。这意味着 UTF-8 编码的 ASCII 字符串与传统 ASCII 字符串无法区分。其次，UTF-8 不会为多字节字符序列引入嵌入的 NULL 字节。因此，基于 C 库的现有软件和期望 NULL 结尾的 8 位字符串的程序都可以与 UTF-8 字符串配合工作。最后，UTF-8 编码保留了字符串的字典排序顺序。也就是说，如果 `a` 和 `b` 是 Unicode 字符串且 `a < b`，那么当 `a` 和 `b` 转换为 UTF-8 时，`a < b` 仍然成立。因此，为 8 位字符串编写的排序算法和其他排序算法也可以用于 UTF-8。

##### 'utf-16'、'utf-16-be' 和 'utf-16-le' 编码

UTF-16 是一种可变长度的 16 位编码，其中 Unicode 字符写为 16 位值。除非指定字节顺序，否则假定使用大端编码。此外，字节顺序标记 `U+FEFF` 可用于显式指定 UTF-16 数据流中的字节顺序。在大端编码中，`U+FEFF` 是零宽不换行空格的 Unicode 字符，而反转值 `U+FFFE` 是非法的 Unicode 字符。因此，编码器可以使用字节序列 `FE FF` 或 `FF FE` 来确定数据流的字节顺序。读取 Unicode 数据时，Python 会从最终的 Unicode 字符串中移除字节顺序标记。

'utf-16-be' 编码显式选择 UTF-16 大端编码。
'utf-16-le' 编码显式选择 UTF-16 小端编码。

尽管 UTF-16 有扩展以支持大于 16 位的字符值，但目前不支持这些扩展。

##### 'unicode-escape' 和 'raw-unicode-escape' 编码

这些编码方法用于将 Unicode 字符串转换为与 Python Unicode 字符串字面量和 Unicode 原始字符串字面量中使用的相同格式。以下是一个示例：

```python
s = u'\u14a8\u0345\u2a34'
t = s.encode('unicode-escape')   #t = '\u14a8\u0345\u2a34'
```

#### Unicode 字符属性

除了执行 I/O 之外，使用 Unicode 的程序可能还需要测试 Unicode 字符的各种属性，如大小写、数字和空白字符。`unicodedata` 模块提供了对字符属性数据库的访问。通用字符属性可以通过 `unicodedata.category(c)` 函数获取。例如，`unicodedata.category(u"A")` 返回 `'Lu'`，表示该字符是大写字母。



Unicode 字符串还有另一个棘手的问题，那就是同一个 Unicode 字符串可能存在多种表示形式。例如，字符 U+00F1（ñ）既可以作为一个完整的字符 U+00F1 出现，也可以被分解为多字符序列 U+006e U+0303（n, ̃）。如果需要对 Unicode 字符串进行一致性处理，请使用 `unicodedata.normalize()` 函数来确保字符表示的一致性。例如，`unicodedata.normalize('NFC', s)` 会确保 `s` 中的所有字符都是完全组合的形式，而不是以组合字符序列的形式表示。

关于 Unicode 字符数据库和 `unicodedata` 模块的更多详细信息，请参见第 16 章"字符串与文本处理"。

#### 对象持久化与 pickle 模块

最后，我们常常需要将对象的内容保存到文件中，以及从文件中恢复对象的内容。一种方法是编写一对函数，以特定格式从文件中读写数据。另一种方法是使用 `pickle` 和 `shelve` 模块。

`pickle` 模块将对象序列化为字节流，以便写入文件并在之后恢复。`pickle` 的接口很简单，包含 `dump()` 和 `load()` 两个操作。例如，以下代码将一个对象写入文件：

```
import pickle
obj = SomeObject()
f = open(filename, 'wb')
pickle.dump(obj, f)    # Save object on f
f.close()
```

要恢复对象，可以使用以下代码：

```
import pickle
f = open(filename, 'rb')
obj = pickle.load(f)  # Restore the object
f.close()
```

可以通过连续执行多次 `dump()` 操作来保存一系列对象。要恢复这些对象，只需使用类似的连续 `load()` 操作即可。

`shelve` 模块与 `pickle` 类似，但它将对象保存在类似字典的数据库中：

```
import shelve
obj = SomeObject()
db = shelve.open("filename")
db['key'] = obj
...
obj = db['key']
db.close()
```

虽然 `shelve` 创建的对象看起来像字典，但它也有一些限制。首先，键必须是字符串。其次，保存在 shelf 中的值必须与 `pickle` 兼容。大多数 Python 对象都可以正常工作，但特殊用途的对象（如文件和网络连接）维护着内部状态，无法通过这种方式保存和恢复。

`pickle` 使用的数据格式是 Python 特有的。然而，该格式在不同的 Python 版本中已经经历了多次演变。可以通过 `pickle.dump(obj, file, protocol)` 操作的可选 `protocol` 参数来选择协议版本。

默认使用协议 0。这是最古老的 `pickle` 数据格式，几乎所有 Python 版本都能理解这种格式。然而，这种格式与许多 Python 较新的特性（如用户自定义类中的 slots）不兼容。协议 1 和 2 使用更高效的二进制数据表示方式。要使用这些替代协议，可以执行如下操作：

```
import pickle
obj = SomeObject()
f = open(filename,'wb')
pickle.dump(obj,f,2)                    # Save using protocol 2
pickle.dump(obj,f,pickle.HIGHEST_PROTOCOL)  # Use the most modern protocol
f.close()
```

使用 `load()` 恢复对象时无需指定协议。底层协议已编码在文件本身中。

同样，可以使用替代的 pickle 协议来打开 `shelve` 以保存 Python 对象，如下所示：

```
import shelve
db = shelve.open(filename,protocol=2)
```

通常，用户自定义对象无需做任何额外工作即可与 `pickle` 或 `shelve` 配合使用。但是，特殊方法 `__getstate__()` 和 `__setstate__()` 可用于辅助 pickle 过程。如果定义了 `__getstate__()` 方法，它将被调用以创建一个表示对象状态的值。`__getstate__()` 返回的值通常应该是字符串、元组、列表或字典。`__setstate__()` 方法在反 pickle 过程中接收此值，并应据此恢复对象的状态。以下示例展示了这些方法如何与涉及底层网络连接的对象配合使用。虽然实际的连接无法被 pickle 化，但对象保存了足够的信息以便在之后反 pickle 时重新建立连接：

```
import socket
class Client(object):
    def __init__(self,addr):
        self.server_addr = addr
        self.sock = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
        self.sock.connect(addr)
    def __getstate__(self):
        return self.server_addr
    def __setstate__(self,value):
        self.server_addr = value
        self.sock = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
        self.sock.connect(self.server_addr)
```

由于 `pickle` 使用的数据格式是 Python 特有的，因此不应将此功能作为不同编程语言编写的应用程序之间交换数据的手段。此外，出于安全考虑，程序不应处理来自不可信来源的 pickle 数据（知识丰富的攻击者可以操纵 pickle 数据格式，在反 pickle 过程中执行任意系统命令）。

`pickle` 和 `shelve` 模块还有许多自定义功能和高级使用选项。更多详情请参见第 13 章"Python 运行时服务"。

#### 执行环境

本章描述 Python 程序的执行环境。目标是描述解释器的运行时行为，包括程序启动、配置和程序终止。

##### 解释器选项与环境

解释器有许多选项来控制其运行时行为和环境。选项通过命令行传递给解释器，格式如下：

```
python [options] [-c cmd | filename | - ] [args]
```

以下是最常见的命令行选项列表：

| 选项 | 描述 |
|--------|-------------|
| -3 | 启用关于在 Python 3 中被移除或更改的特性的警告。 |
| -B | 阻止在导入时创建 `.pyc` 或 `.pyo` 文件。 |
| -E | 忽略环境变量。 |
| -h | 打印所有可用命令行选项的列表。 |
| -i | 程序执行后进入交互模式。 |
| -m module | 以脚本方式运行库模块 `module`。 |
| -O | 优化模式。 |
| -OO | 优化模式，并在创建 `.pyo` 文件时移除文档字符串。 |
| -Q arg | 指定 Python 2 中除法运算符的行为。可选值为 -Qold（默认）、-Qnew、-Qwarn 或 -Qwarnall。 |
| -s | 阻止将用户站点目录添加到 `sys.path`。 |
| -S | 阻止包含站点初始化模块。 |
| -t | 报告不一致的制表符使用的警告。 |
| -tt | 不一致的制表符使用将引发 `TabError` 异常。 |
| -u | 无缓冲的二进制 stdout 和 stdin。 |
| -U | Unicode 字面量。所有字符串字面量都作为 Unicode 处理（仅限 Python 2）。 |
| -v | 详细模式。跟踪 import 语句。 |
| -V | 打印版本号并退出。 |
| -x | 跳过源程序的第一行。 |
| -c cmd | 将 `cmd` 作为字符串执行。 |

`-i` 选项在程序执行结束后立即启动交互会话，对调试非常有用。`-m` 选项以脚本方式运行库模块，该模块在主脚本执行之前在 `__main__` 模块中执行。`-O` 和 `-OO` 选项对字节编译文件进行一些优化，详见第 8 章"模块、包与分发"。`-S` 选项省略了后文"站点配置文件"一节中描述的站点初始化模块。`-t`、`-tt` 和 `-v` 选项报告额外的警告和调试信息。`-x` 选项在程序第一行不是有效的 Python 语句时跳过该行（例如，当第一行在脚本中启动 Python 解释器时）。

程序名出现在所有解释器选项之后。如果未给出名称，或使用连字符（-）作为文件名，解释器将从标准输入读取程序。如果标准输入是交互式终端，则显示横幅和提示符。否则，解释器打开指定的文件并执行其中的语句，直到遇到文件结束标记。`-c cmd` 选项可用于以命令行选项的形式执行简短程序——例如，`python -c "print('hello world')"`。

出现在程序名或连字符（-）之后的命令行选项将通过 `sys.argv` 传递给程序，详见第 9 章"输入与输出"中的"读取选项与环境变量"一节。

此外，解释器还会读取以下环境变量：

| 环境变量 | 描述 |
| --- | --- |
| PYTHONPATH | 以冒号分隔的模块搜索路径。 |
| PYTHONSTARTUP | 交互式启动时执行的文件。 |
| PYTHONHOME | Python 安装的位置。 |
| PYTHONINSPECT | 等同于 `-i` 选项。 |
| PYTHONUNBUFFERED | 等同于 `-u` 选项。 |
| PYTHONIOENCODING | stdin、stdout 和 stderr 的编码与错误处理。格式为 "encoding[:errors]" 的字符串，例如 "utf-8" 或 "utf-8:ignore"。 |
| PYTHONDONTWRITEBYTECODE | 等同于 `-B` 选项。 |
| PYTHONOPTIMIZE | 等同于 `-O` 选项。 |
| PYTHONNOUSERSITE | 等同于 `-s` 选项。 |
| PYTHONVERBOSE | 等同于 `-v` 选项。 |
| PYTHONUSERBASE | 每用户站点包的根目录。 |
| PYTHONCASEOK | 指示 import 使用的模块名进行不区分大小写的匹配。 |

表 10.2 解释器环境变量

`PYTHONPATH` 指定了插入到 `sys.path` 开头的模块搜索路径，详见第 9 章。`PYTHONSTARTUP` 指定了解释器在交互模式下运行时要执行的文件。`PYTHONHOME` 变量用于设置 Python 安装的位置，但很少需要使用，因为 Python 知道



##### 交互式会话

如果未给出程序名称，并且标准输入连接到一个交互式终端，Python 将以交互模式启动。在这种模式下，系统会打印一条欢迎信息，并向用户显示一个提示符。此外，解释器会执行 `PYTHONSTARTUP` 环境变量（如果已设置）中包含的脚本。该脚本的执行方式类似于输入程序的一部分（也就是说，它不是使用 `import` 语句加载的）。此脚本的一个应用场景是读取用户配置文件，例如 `.pythonrc`。

当接受交互式输入时，会出现两个用户提示符。`>>>` 提示符出现在新语句的开头；`...` 提示符表示语句的续行。以下是一个示例：

```
>>> for i in range(0,4):
...    print i,
...
0 1 2 3
>>>
```

在自定义应用中，你可以通过修改 `sys.ps1` 和 `sys.ps2` 的值来更改提示符。

在某些系统上，Python 可能被编译为使用 GNU readline 库。如果启用，该库将为 Python 的交互模式提供命令历史记录、补全等功能。

默认情况下，交互模式下发出的命令的输出是通过打印内置 `repr()` 函数的结果生成的。这可以通过将变量 `sys.displayhook` 设置为一个负责显示结果的函数来更改。以下是一个截断长结果的示例：

```
>>> def my_display(x):
...     r = repr(x)
...     if len(r) > 40: print(r[:40]+"..."+r[-1])
...     else: print(r)
>>> sys.displayhook = my_display
>>> 3+4
7
>>> range(100000)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 1...]
>>>
```

最后，在交互模式下，了解上次操作的结果存储在一个特殊变量（`_`）中是很有用的。如果需要在后续操作中使用该结果，可以使用此变量来检索。以下是一个示例：

```
>>> 7 + 3
10
>>> _ + 2
12
>>>
```

`_` 变量的设置发生在前面展示的 `displayhook()` 函数中。如果你重新定义 `displayhook()`，并且希望保留此功能，你的替换函数也应该设置 `_`。

##### 启动 Python 应用程序

在大多数情况下，你会希望程序自动启动解释器，而不是首先手动启动解释器。在 UNIX 系统上，这通过赋予程序执行权限并将程序的第一行设置为如下内容来实现：

```
#!/usr/bin/env python
###### 从此处开始是 Python 代码...
print "Hello world"
...
```

在 Windows 系统上，双击 `.py`、`.pyw`、`.wpy`、`.pyc` 或 `.pyo` 文件会自动启动解释器。通常，程序在控制台窗口中运行，除非它们被重命名为带有 `.pyw` 后缀（在这种情况下，程序会静默运行）。如果需要向解释器提供选项，也可以从 `.bat` 文件启动 Python。例如，这个 `.bat` 文件只是在脚本上运行 Python，并将命令提示符提供的任何选项传递给解释器：

```
:: foo.bat
:: 运行 foo.py 脚本并传递提供的命令行选项（如果有）
c:\python26\python.exe c:\pythonscripts\foo.py %*
```

##### 站点配置文件

典型的 Python 安装可能包含许多第三方模块和包。为了配置这些包，解释器首先导入 `site` 模块。`site` 模块的作用是搜索包文件，并将额外的目录添加到模块搜索路径 `sys.path` 中。此外，`site` 模块为 Unicode 字符串转换设置默认编码。

`site` 模块的工作方式是首先创建一个目录名列表，该列表由 `sys.prefix` 和 `sys.exec_prefix` 的值构建如下：

```
[ sys.prefix,                        # 仅限 Windows
  sys.exec_prefix,                   # 仅限 Windows
  sys.prefix + 'lib/pythonvers/site-packages',
  sys.prefix + 'lib/site-python',
  sys.exec_prefix + 'lib/pythonvers/site-packages',
  sys.exec_prefix + 'lib/site-python' ]
```

此外，如果启用，一个用户特定的 site-packages 目录可能会被添加到此列表中（将在下一节描述）。

对于列表中的每个目录，都会检查该目录是否存在。如果存在，则将其添加到 `sys.path` 变量中。接下来，检查它是否包含任何路径配置文件（具有 `.pth` 后缀的文件）。路径配置文件包含一个相对于路径文件位置的目录、zip 文件或 `.egg` 文件的列表，这些文件应添加到 `sys.path` 中。例如：

```
###### foo 包配置文件 'foo.pth'
foo
bar
```

路径配置文件中的每个目录必须单独占一行。注释和空行将被忽略。当 `site` 模块加载该文件时，它会检查每个目录是否存在。如果存在，则将该目录添加到 `sys.path`。重复项只会添加到路径中一次。

在所有路径都添加到 `sys.path` 之后，会尝试导入一个名为 `sitecustomize` 的模块。此模块的目的是执行任何额外的（且任意的）站点自定义。如果导入 `sitecustomize` 时发生 `ImportError` 错误，该错误会被静默忽略。导入 `sitecustomize` 发生在将任何用户目录添加到 `sys.path` 之前。因此，将此文件放在你自己的目录中没有任何效果。

`site` 模块还负责设置默认的 Unicode 编码。默认情况下，编码设置为 `'ascii'`。但是，可以通过在 `sitecustomize.py` 中放置调用 `sys.setdefaultencoding()` 并传入新编码（如 `'utf-8'`）的代码来更改编码。如果你愿意尝试，也可以修改 `site` 的源代码，根据机器的区域设置自动设置编码。

##### 每个用户的站点包（Per-user Site Packages）

通常，第三方模块的安装方式使其可供所有用户访问。但是，单个用户可以在每个用户的站点目录中安装模块和包。在 UNIX 和 Macintosh 系统上，此目录位于 `~/.local` 下，名称类似于 `~/.local/lib/python2.6/site-packages`。在 Windows 系统上，此目录由 `%APPDATA%` 环境变量决定，通常类似于 C:\Documents and Settings\David Beazley\Application Data。在此文件夹内，你会找到一个 "Python\Python26\site-packages" 目录。

如果你正在编写自己的 Python 模块和包，并希望在库中使用它们，可以将它们放在每个用户的站点目录中。如果你正在安装第三方模块，可以通过向 setup.py 提供 --user 选项将其手动安装到此目录中。例如：python setup.py install --user。

##### 启用未来特性

影响与旧版本 Python 兼容性的新语言特性在首次发布时通常会被禁用。要启用这些特性，可以使用 `from __future__ import feature` 语句。以下是一个示例：

```
###### 启用新的除法语义
from __future__ import division
```

使用时，此语句应作为模块或程序的第一条语句出现。此外，`__future__` 导入的范围仅限于使用它的模块。因此，导入一个未来特性不会影响 Python 库模块或需要先前解释器行为才能正确运行的旧代码的行为。

目前，已定义以下特性：

| 特性名称 | 描述 |
| --- | --- |
| nested_scopes | 支持函数中的嵌套作用域。首次引入于 Python 2.1，并在 Python 2.2 中成为默认行为。 |
| generators | 支持生成器。首次引入于 Python 2.2，并在 Python 2.3 中成为默认行为。 |
| division | 修改了除法语义，整数除法返回分数结果。例如，1/4 的结果是 0.25 而不是 0。首次引入于 Python 2.2，截至 Python 2.6 仍是一个可选特性。这是 Python 3.0 中的默认行为。 |
| absolute_import | 修改了包相对导入的行为。目前，当包的子模块进行 `import string` 这样的导入语句时，它首先在包的当前目录中查找，然后在 `sys.path` 中的目录中查找。但是，如果包恰好使用了冲突的名称，这将无法加载标准库中的模块。启用此特性后，`import module` 语句是一个绝对导入。因此，像 `import string` 这样的语句将始终从标准库加载 `string` 模块。首次引入于 Python 2.5，在 Python 2.6 中仍然禁用。在 Python 3.0 中启用。 |
| with_statement | 支持上下文管理器和 with 语句。首次引入于 Python 2.5，在 Python 2.6 中默认启用。 |
| print_function | 使用 Python 3.0 的 `print()` 函数代替 `print` 语句。首次引入于 Python 2.6，在 Python 3.0 中默认启用。 |

...（后续内容省略，因为用户提供的英文文本在表格后中断了）



需要指出的是，`__future__` 模块中的特性名称永远不会被删除。因此，即使某个特性在后续的Python版本中被默认开启，任何使用该特性的现有代码都不会因此中断。

##### 程序终止

当输入程序中没有更多可执行的语句、当未捕获的 `SystemExit` 异常被抛出（例如由 `sys.exit()` 生成）、或者当解释器接收到 `SIGTERM` 或 `SIGHUP` 信号（在UNIX系统上）时，程序就会终止。在退出时，解释器会递减所有当前已知命名空间中所有对象的引用计数（并销毁每个命名空间）。如果对象的引用计数降为零，该对象就会被销毁，并且其 `__del__()` 方法会被调用。

需要注意的是，在某些情况下，`__del__` 方法在程序终止时可能不会被调用。如果对象之间存在循环引用（在这种情况下，对象可能已被分配但从任何已知命名空间都无法访问），就会发生这种情况。虽然Python的垃圾回收器可以在执行过程中回收未使用的循环引用，但它通常不会在程序终止时被调用。

由于无法保证 `__del__()` 在终止时一定会被调用，因此显式清理某些对象（如打开的文件和网络连接）可能是一个好主意。为此，可以为用户定义的对象添加专门的清理方法（例如 `close()`）。另一种可能性是编写一个终止函数，并通过 `atexit` 模块将其注册，如下所示：

```python
import atexit
connection = open_connection("deaddot.com")

def cleanup():
    print "Going away..."
    close_connection(connection)

atexit.register(cleanup)
```

垃圾回收器也可以通过这种方式调用：

```python
import atexit, gc
atexit.register(gc.collect)
```

关于程序终止的最后一个特殊之处在于，某些对象的 `__del__` 方法可能会尝试访问全局数据或在其他模块中定义的方法。由于这些对象可能已经被销毁，在 `__del__` 中会发生 `NameError` 异常，你可能会看到如下错误：

```
Exception exceptions.NameError: 'c' in <method Bar.__del__
of Bar instance at c0310> ignored
```

如果发生这种情况，意味着 `__del__` 已经过早地中止。这也意味着它可能在尝试执行重要操作（如干净地关闭服务器连接）时失败了。如果对此有所顾虑，在代码中执行显式的关闭步骤可能是个好主意，而不是依赖解释器在程序终止时干净地销毁对象。通过在 `__del__()` 方法的声明中声明默认参数，也可以消除特殊的 `NameError` 异常：

```python
import foo
class Bar(object):
    def __del__(self, foo=foo):
        foo.bar()        # Use something in module foo
```

在某些情况下，可能需要在不执行任何清理操作的情况下终止程序执行。这可以通过调用 `os._exit(status)` 来实现。该函数提供了对低级 `exit()` 系统调用的接口，负责终止Python解释器进程。调用时，程序会立即终止，不会进行任何进一步的处理或清理。

## 11

## 测试、调试、性能分析和调优

与C或Java等语言编写的程序不同，Python程序不会经过编译器的处理来生成可执行程序。在那些语言中，编译器是抵御编程错误的第一道防线——它能捕获诸如以错误数量的参数调用函数或给变量赋予不合适的值（即类型检查）等错误。然而在Python中，这类检查直到程序运行时才会进行。因此，除非运行并测试你的程序，否则你永远无法真正知道你的程序是否正确。不仅如此，除非你能以某种方式运行你的程序，使其执行内部控制流的每一个可能分支，否则总会存在隐藏错误等待爆发的风险（幸运的是，这通常只在发布几天后发生）。

为了解决这类问题，本章涵盖了用于测试、调试和分析Python代码的技术和库模块。最后，讨论了一些优化Python代码的策略。

#### 文档字符串和 doctest 模块

如果函数、类或模块的第一行是一个字符串，那么这个字符串就被称为文档字符串。包含文档字符串被认为是一种良好的风格，因为这些字符串被用来向Python软件开发工具提供信息。例如，`help()` 命令会检查文档字符串，Python的IDE也会查看这些字符串。由于程序员倾向于在交互式shell中尝试时查看文档字符串，因此这些字符串通常包含简短的交互式示例。例如：

```python
##### splitter.py
def split(line, types=None, delimiter=None):
    """Splits a line of text and optionally performs type conversion.
    For example:

    >>> split('GOOG 100 490.50')
    ['GOOG', '100', '490.50']
    >>> split('GOOG 100 490.50',[str, int, float])
    ['GOOG', 100, 490.5]
    >>>
```

默认情况下，分割操作是基于空白符进行的，但也可以通过 `delimiter` 关键字参数选择不同的分隔符：

```python
>>> split('GOOG,100,490.50',delimiter=',')
['GOOG', '100', '490.50']
>>>
```

```python
"""
fields = line.split(delimiter)
if types:
    fields = [ ty(val) for ty,val in zip(types,fields) ]
return fields
```

编写文档的一个常见问题是保持文档与函数的实际实现同步。例如，一个程序员可能修改了函数但忘记更新文档。

为了解决这个问题，请使用 `doctest` 模块。`doctest` 收集文档字符串，扫描其中的交互式会话，并将它们作为一系列测试来执行。要使用 `doctest`，你通常需要创建一个单独的测试模块。例如，如果前面的函数位于文件 `splitter.py` 中，你会创建一个用于测试的文件 `testsplitter.py`，如下所示：

```python
##### testsplitter.py
import splitter
import doctest

nfail, ntests = doctest.testmod(splitter)
```

在此代码中，调用 `doctest.testmod(module)` 会对指定模块运行测试，并返回失败次数和执行的测试总数。如果所有测试都通过，则不会产生任何输出。否则，你将收到一份失败报告，显示预期输出和实际接收输出之间的差异。如果你希望看到测试的详细输出，可以使用 `testmod(module, verbose=True)`。

作为创建单独测试文件的替代方案，库模块可以通过在文件末尾包含如下代码来进行自我测试：

```python
...
if __name__ == '__main__':
    # test myself
    import doctest
    doctest.testmod()
```

使用此代码，如果文件作为解释器的主程序运行，文档测试将会运行。否则，如果文件是通过 `import` 加载的，则测试将被忽略。

`doctest` 期望函数的输出与你在交互式解释器中得到的输出在字面上完全匹配。因此，它对空白符和数值精度问题相当敏感。例如，考虑这个函数：

```python
def half(x):
    """Halves x.  For example:
    
    >>> half(6.8)
    3.4
    >>>
    """
    return x/2
```

如果你对此函数运行 `doctest`，你将得到如下失败报告：

```
**********************************************************************
File "half.py", line 4, in __main__.half
Failed example:
    half(6.8)
Expected:
    3.4
Got:
    3.3999999999999999
**********************************************************************
```

要修复这个问题，你或者需要使文档与输出完全匹配，或者需要在文档中选择更好的示例。

由于使用 `doctest` 几乎是微不足道的，因此几乎没有理由不在你自己的程序中使用它。但是，请记住，`doctest` 并不是你通常会用于穷举程序测试的模块。这样做往往会导致文档字符串过长和过于复杂——这违背了生成有用文档的初衷（例如，如果用户请求帮助，而文档却列出了50个涵盖各种棘手边缘情况的示例，用户可能会感到恼火）。对于这类测试，你需要使用 `unittest` 模块。

最后，`doctest` 模块有大量的配置选项，涉及测试执行方式和结果报告方式的各个方面。由于这些选项对于该模块最常见的用法不是必需的，因此此处不再介绍。更多详细信息，请参阅 http://docs.python.org/library/doctest.html。

#### 单元测试和 unittest 模块

对于更全面的程序测试，请使用 `unittest` 模块。在单元测试中，开发者为构成程序的每个元素（例如，单个函数、方法、类和模块）编写一组独立的测试用例。然后运行这些测试，以验证构成更大程序的基本构建块的正确行为。随着程序规模的增长，各个组件的单元测试可以组合起来创建大型测试框架和测试工具。这可以大大简化验证正确行为的任务，并在问题发生时隔离和修复它们。使用该模块可以通过上一节中的代码清单来说明：

```python
##### splitter.py
def split(line, types=None, delimiter=None):
    """Splits a line of text and optionally performs type conversion.
    ...
    """
    fields = line.split(delimiter)
    if types:
        fields = [ ty(val) for ty,val in zip(types,fields) ]
    return fields
```



如果你想为测试 `split()` 函数的各种方面编写单元测试，你可以创建一个单独的模块 `testsplitter.py`，如下所示：

```python
##### testsplitter.py
import splitter
import unittest

##### Unit tests
class TestSplitFunction(unittest.TestCase):
    def setUp(self):
        # Perform set up actions (if any)
        pass
    def tearDown(self):
        # Perform clean-up actions (if any)
        pass
    def testsimplestring(self):
        r = splitter.split('GOOG 100 490.50')
        self.assertEqual(r, ['GOOG', '100', '490.50'])
    def testtypeconvert(self):
        r = splitter.split('GOOG 100 490.50', [str, int, float])
        self.assertEqual(r, ['GOOG', 100, 490.5])
    def testdelimiter(self):
        r = splitter.split('GOOG,100,490.50', delimiter=',')
        self.assertEqual(r, ['GOOG', '100', '490.50'])

##### Run the unittests
if __name__ == '__main__':
    unittest.main()
```

要运行测试，只需对文件 `testsplitter.py` 执行 Python 即可。以下是一个示例：

```
% python testsplitter.py
...
----------------------------------------------------------------------
Ran 3 tests in 0.014s

OK
```

`unittest` 的基本用法是定义一个继承自 `unittest.TestCase` 的类。在该类中，各个测试通过以 `'test'` 开头的方法名来定义——例如 `'testsimplestring'`、`'testtypeconvert'` 等等。（需要强调的是，方法名完全由你决定，只要以 `'test'` 开头即可。）在每个测试中，使用各种断言来检查不同的条件。

`unittest.TestCase` 的实例 `t` 具有以下方法，用于编写测试和控制测试过程：

**`t.setUp()`**

在运行任何测试方法之前被调用，用于执行初始化步骤。

**`t.tearDown()`**

在运行测试之后被调用，用于执行清理操作。

**`t.assert_(expr [, msg])`**
**`t.failUnless(expr [, msg])`**

如果 `expr` 求值为 `False`，则表示测试失败。`msg` 是一个消息字符串，用于说明失败原因（如果有）。

**`t.assertEqual(x, y [,msg])`**
**`t.failUnlessEqual(x, y [, msg])`**

如果 `x` 和 `y` 不相等，则表示测试失败。`msg` 是一个用于说明失败原因的消息（如果有）。

**`t.assertNotEqual(x, y [, msg])`**
**`t.failIfEqual(x, y, [, msg])`**

如果 `x` 和 `y` 相等，则表示测试失败。`msg` 是一个用于说明失败原因的消息（如果有）。

**`t.assertAlmostEqual(x, y [, places [, msg]])`**
**`t.failUnlessAlmostEqual(x, y, [, places [, msg]])`**

如果数字 `x` 和 `y` 之间的小数位差异超过 `places` 位，则表示测试失败。这通过计算 `x` 和 `y` 的差值并将结果四舍五入到给定的位数来检查。如果结果为零，则 `x` 和 `y` 近似相等。`msg` 是一个用于说明失败原因的消息（如果有）。

**`t.assertNotAlmostEqual(x, y, [, places [, msg]])`**
**`t.failIfAlmostEqual(x, y [, places [, msg]])`**

如果 `x` 和 `y` 之间至少相差 `places` 个小数位，则表示测试失败。`msg` 是一个用于说明失败原因的消息（如果有）。

**`t.assertRaises(exc, callable, ...)`**
**`t.failUnlessRaises(exc, callable, ...)`**

如果可调用对象 `callable` 没有引发异常 `exc`，则表示测试失败。剩余的参数作为参数传递给 `callable`。可以通过使用异常元组作为 `exc` 来检查多个异常。

**`t.failIf(expr [, msg])`**

如果 `expr` 求值为 `True`，则表示测试失败。`msg` 是一个用于说明失败原因的消息（如果有）。

**`t.fail([msg])`**

表示测试失败。`msg` 是一个用于说明失败原因的消息（如果有）。

**`t.failureException`**

此属性被设置为测试中捕获的最后一个异常值。如果你不仅想检查异常是否被引发，还想检查异常是否引发了一个适当的值——例如，如果你想检查引发异常时生成的错误消息——这会很有用。

需要注意的是，`unittest` 模块包含大量高级自定义选项，用于分组测试、创建测试套件以及控制测试运行的环境。这些功能与为代码编写测试的过程没有直接关系（你往往会像示例中那样独立于测试实际执行方式来编写测试类）。有关如何为大型程序组织测试的更多信息，请参阅文档 http://docs.python.org/library/unittest.html。

#### Python 调试器和 pdb 模块

Python 包含一个简单的基于命令行的调试器，位于 `pdb` 模块中。`pdb` 模块支持事后调试、栈帧检查、断点设置、源代码单步执行以及代码求值。

有多个函数可用于从程序或交互式 Python shell 中调用调试器。

**`run(statement [, globals [, locals]])`**

在调试器控制下执行字符串 `statement`。调试器提示符将在任何代码执行之前立即出现。输入 `'continue'` 将强制其运行。`globals` 和 `locals` 分别定义代码运行的全局和局部命名空间。

**`runeval(expression [, globals [, locals]])`**

在调试器控制下对表达式字符串进行求值。调试器提示符将在任何代码执行之前出现，因此你需要像使用 `run()` 一样输入 `'continue'` 来强制其执行。成功后，返回表达式的值。

**`runcall(function [, argument, ...])`**

在调试器中调用一个函数。`function` 是一个可调用对象。额外的参数作为参数传递给 `function`。调试器提示符将在任何代码执行之前出现。函数完成后返回其返回值。

**`set_trace()`**

在调用此函数的位置启动调试器。这可用于在特定代码位置硬编码一个调试器断点。

**`post_mortem(traceback)`**

对 traceback 对象启动事后调试。`traceback` 通常通过 `sys.exc_info()` 等函数获取。

**`pm()`**

使用最后一个异常的 traceback 进入事后调试。

在所有启动调试器的函数中，`set_trace()` 函数在实践中可能是最容易使用的。如果你正在处理一个复杂的应用程序，但已经在其中某个部分发现了问题，你可以在代码中插入一个 `set_trace()` 调用，然后直接运行应用程序。当执行到该位置时，程序将挂起并直接进入调试器，你可以在其中检查执行环境。离开调试器后，执行将恢复。

#### 调试器命令

当调试器启动时，它会显示一个 `(Pdb)` 提示符，如下所示：

```python
>>> import pdb
>>> import buggymodule
>>> pdb.run('buggymodule.start()')
> <string>(0)?()
(Pdb)
```

`(Pdb)` 是调试器提示符，支持以下命令。请注意，某些命令有短格式和长格式。在这种情况下，括号用于同时表示两种形式。例如，`h(elp)` 表示 `h` 或 `help` 均可接受。

###### [!]statement

在当前栈帧的上下文中执行（单行）`statement`。感叹号可以省略，但如果语句的第一个单词类似于调试器命令，则必须使用感叹号以避免歧义。要设置全局变量，你可以在同一行中在赋值命令前加上 `"global"` 命令：

```python
(Pdb) global list_options; list_options = ['-l']
(Pdb)
```

###### a(rgs)

打印当前函数的参数列表。

###### alias [name [command]]

创建一个名为 `name` 的别名，用于执行 `command`。在 `command` 字符串中，子字符串 `'%1'`、`'%2'` 等在输入别名时会被参数替换。`'%*'` 会被所有参数替换。如果未指定命令，则显示当前别名列表。别名可以嵌套，并且可以包含任何可以在 `Pdb` 提示符下合法输入的内容。以下是一个示例：

```python
####### Print instance variables (usage "pi classInst")
alias pi for k in %1.__dict__.keys(): print "%1.",k,"=",%1.__dict__[k]
####### Print instance variables in self
alias ps pi self
```

###### b(reak) [loc [, condition]]

在位置 `loc` 设置一个断点。`loc` 可以指定特定的文件名和行号，也可以是模块中某个函数的名称。使用以下语法：

| 设置 | 描述 |
|------|------|
| `n` | 当前文件中的行号 |
| `filename:n` | 另一个文件中的行号 |
| `function` | 当前模块中的函数名 |
| `module.function` | 模块中的函数名 |

如果省略 `loc`，则打印所有当前断点。`condition` 是一个表达式，必须在断点被触发之前求值为真。所有断点都被分配



命令执行完成后会打印出这些数字。后续的其他调试器命令会用到这些数字。

`cl(ear) [bpnumber [bpnumber ...]]`
清除一组断点号。如果指定了断点，则清除所有断点。

`commands [bpnumber]`
设置一系列调试器命令，当遇到断点 *bpnumber* 时自动执行这些命令。列出要执行的命令时，只需在后续行中输入它们，并使用 `end` 标记命令序列的结束。如果包含了 `continue` 命令，那么在遇到断点时程序执行将自动恢复。如果省略 *bpnumber*，则使用最后设置的断点。

`condition bpnumber [condition]`
为断点设置条件。*condition* 是一个表达式，在断点被识别之前，该表达式必须求值为 true。省略条件将清除任何先前的条件。

`c(ont(inue))`
继续执行，直到遇到下一个断点。

`disable [bpnumber [bpnumber ...]]`
禁用指定的一组断点。与 `clear` 不同，这些断点以后可以重新启用。

`d(own)`
将当前帧在堆栈跟踪中向下移动一级。

`enable [bpnumber [bpnumber ...]]`
启用指定的一组断点。

`h(elp) [command]`
显示可用命令列表。指定一个命令将返回该命令的帮助信息。

`ignore bpnumber [count]`
忽略某个断点 *count* 次执行。

`j(ump) lineno`
设置下一行要执行的代码行号。此命令只能用于在同一执行帧内的语句之间移动。此外，你不能跳转到某些语句中，例如循环中间的语句。

`l(ist) [first [, last]]`
列出源代码。不带参数时，此命令列出当前行周围的 11 行（当前行之前 5 行和之后 5 行）。带一个参数时，列出该行周围的 11 行。带两个参数时，列出给定范围内的行。如果 *last* 小于 *first*，则将其解释为行数。

`n(ext)`
执行直到当前函数的下一行。跳过函数调用中包含的代码。

`p *expression*`
在当前上下文中求值表达式并打印其值。

`pp *expression*`
与 `p` 命令相同，但结果使用美观打印模块（`pprint`）进行格式化。

`q(uit)`
退出调试器。

`r(eturn)`
运行直到当前函数返回。

`run [*args*]`
重启程序，并使用 *args* 中的命令行参数作为 `sys.argv` 的新设置。所有断点和其他调试器设置都将保留。

`s(tep)`
执行单行源代码，并在被调用的函数内部停止。

`tbreak [*loc* [, *condition*]]`
设置一个临时断点，该断点在第一次命中后即被删除。

`u(p)`
将当前帧在堆栈跟踪中向上移动一级。

`unalias *name*`
删除指定的别名。

`until`
恢复执行，直到控制权离开当前执行帧或达到一个大于当前行号的行号。例如，如果调试器在循环体的最后一行停止，输入 `until` 将执行循环中的所有语句，直到循环结束。

`w(here)`
打印堆栈跟踪。

#### 从命令行调试

运行调试器的另一种方法是在命令行上调用它。以下是一个示例：

```
% python -m pdb someprogram.py
```

在这种情况下，调试器在程序启动开始时自动启动，此时你可以自由设置断点并进行其他配置更改。要使程序运行，只需使用 `continue` 命令。例如，如果你想调试一个程序中使用的 `split()` 函数，你可能会这样做：

```
% python -m pdb someprogram.py
> /Users/beazley/Code/someprogram.py(1)<module>()
-> import splitter
(Pdb) b splitter.split
Breakpoint 1 at /Users/beazley/Code/splitter.py:1
(Pdb) c
> /Users/beazley/Code/splitter.py(18)split()
-> fields = line.split(delimter)
(Pdb)
```

#### 配置调试器

如果用户的主目录或当前目录中存在 `.pdbrc` 文件，它将被读取并执行，就好像它是在调试器提示符下输入的一样。这对于指定每次启动调试器时要执行的调试命令（而不是每次都必须交互式地输入命令）非常有用。

#### 程序性能分析

`profile` 和 `cProfile` 模块用于收集性能分析信息。两个模块的工作方式相同，但 `cProfile` 是作为 C 扩展实现的，速度明显更快，也更现代。任一模块都可用于收集覆盖信息（即执行了哪些函数）以及性能统计信息。分析程序的最简单方法是从命令行执行，如下所示：

```
% python -m cProfile someprogram.py
```

或者，可以使用 `profile` 模块中的以下函数：

```
run(command [, filename])
```

在分析器下使用 `exec` 语句执行 `command` 的内容。`filename` 是保存原始性能分析数据的文件名。如果省略，则会将报告打印到标准输出。

运行分析器的结果是如下所示的报告：

```
126 function calls (6 primitive calls) in 5.130 CPU seconds
Ordered by: standard name
ncalls  tottime  percall  cumtime  percall filename:lineno(function)
    1    0.030    0.030    5.070    5.070 <string>:1(?)
  121/1    5.020    0.041    5.020    5.020 book.py:11(process)
    1    0.020    0.020    5.040    5.040 book.py:5(?)
    2    0.000    0.000    0.000    0.000 exceptions.py:101(__init__)
    1    0.060    0.060    5.130    5.130 profile:0(execfile('book.py'))
    0    0.000             0.000           profile:0(profiler)
```

`run()` 生成的报告的不同部分解释如下：

| 部分 | 描述 |
|---|---|
| `primitive calls` | 非递归函数调用次数 |
| `ncalls` | 总调用次数（包括自身递归） |
| `tottime` | 在此函数中花费的时间（不计算子函数） |
| `percall` | `tottime`/ncalls |
| `cumtime` | 在函数中花费的总时间 |
| `percall` | `cumtime`/（原始调用次数） |
| `filename:lineno(function)` | 每个函数的位置和名称 |

当第一列有两个数字时（例如 "121/1"），后者是原始调用次数，前者是实际调用次数。

仅仅检查生成的分析器报告通常对于此模块的大多数应用来说就足够了——例如，如果你只是想看看你的程序是如何花费时间的。但是，如果你想保存数据并进一步分析，可以使用 `pstats` 模块。有关保存和分析性能分析数据的更多详细信息，请参阅 http://docs.python.org/library/profile.html。

#### 调优与优化

本节介绍一些通用的经验法则，可用于使 Python 程序运行得更快并使用更少的内存。这里描述的技术并非详尽无遗，但应该能在程序员审视自己的代码时提供一些思路。

#### 进行计时测量

如果你只是想对一个长时间运行的 Python 程序进行计时，最简单的方法通常是直接运行它，然后使用类似 UNIX `time` 命令这样的工具来获取结果。或者，如果你有一段长时间运行的语句想要计时，你可以插入对 `time.clock()` 的调用来获取当前已用 CPU 时间的读数，或者插入对 `time.time()` 的调用来读取当前的挂钟时间。例如：

```
start_cpu = time.clock()
start_real = time.time()
statements
statements
end_cpu = time.clock()
end_real = time.time()
print("%f Real Seconds" % (end_real - start_real))
print("%f CPU seconds" % (end_cpu - start_cpu))
```
请记住，这种技术仅在待计时的代码运行相当长一段时间时才真正有效。如果你有一个细粒度的语句想要进行基准测试，可以使用 `timeit` 模块中的 `timeit(code [, setup])` 函数。例如：

```
>>> from timeit import timeit
>>> timeit('math.sqrt(2.0)','import math')
0.20388007164001465
>>> timeit('sqrt(2.0)','from math import sqrt')
0.14494490623474121
```



在这个示例中，`timeit()` 的第一个参数是你想要基准测试的代码。第二个参数是一条语句，它会执行一次以设置执行环境。`timeit()` 函数会将提供的语句运行一百万次，并报告执行时间。可以通过向 `timeit()` 传入 `number=count` 关键字参数来更改重复次数。

`timeit` 模块还有一个 `repeat()` 函数，也可以用于进行测量。该函数的工作方式与 `timeit()` 相同，但它会重复计时测量三次，并返回一个包含结果的列表。例如：

```
>>> from timeit import repeat
>>> repeat('math.sqrt(2.0)','import math')
[0.20306601524353027, 0.19715800285339355, 0.20907392501831055]
>>>
```

在进行性能测量时，通常会参考相关的*加速比*，它通常指原始执行时间除以新的执行时间。例如，在前面的计时测量中，使用 `sqrt(2.0)` 代替 `math.sqrt(2.0)` 表示加速比为 0.20388/0.14494，大约为 1.41。有时这会以百分比的形式报告，即加速比约为 41%。

#### 进行内存测量

`sys` 模块有一个 `getsizeof()` 函数，可用于调查单个 Python 对象的内存占用（以字节为单位）。例如：

```
>>> import sys
>>> sys.getsizeof(1)
14
>>> sys.getsizeof("Hello World")
52
>>> sys.getsizeof([1,2,3,4])
52
>>> sum(sys.getsizeof(x) for x in [1,2,3,4])
56
```

对于列表、元组和字典等容器，报告的大小仅针对容器对象本身，而不是其中包含的所有对象的累积大小。例如，在前面的示例中，列表 `[1,2,3,4]` 的报告大小实际上小于四个整数（每个 14 字节）所需的空间。这是因为列表的内容未包含在总数中。你可以如上所示使用 `sum()` 来计算列表内容的总大小。

请注意，`getsizeof()` 函数只能让你粗略了解各种对象的整体内存使用情况。在内部，解释器通过引用计数积极共享对象，因此一个对象实际消耗的内存可能远小于你最初想象的。此外，鉴于 Python 的 C 扩展可以在解释器之外分配内存，精确获取整体内存使用量的测量值可能比较困难。因此，测量实际内存占用的辅助技术是从操作系统进程查看器或任务管理器中检查你正在运行的程序。

坦率地说，更好地掌握内存使用情况的方法可能是坐下来进行分析。如果你知道你的程序将分配各种类型的数据结构，并且你知道这些结构中将存储什么类型的数据（即 int、float、string 等），你可以使用 `getsizeof()` 函数的结果来获取计算程序内存占用上限的数据——或者至少，你可以获取足够的信息来进行"粗略的"估算。

#### 反汇编

`dis` 模块可用于将 Python 函数、方法和类反汇编为低级解释器指令。该模块定义了一个 `dis()` 函数，可以这样使用：

```
>>> from dis import dis
>>> dis(split)
  2         0 LOAD_FAST           0 (line)
            3 LOAD_ATTR           0 (split)
            6 LOAD_FAST           1 (delimiter)
            9 CALL_FUNCTION       1
           12 STORE_FAST          2 (fields)

  3        15 LOAD_GLOBAL         1 (types)
           18 JUMP_IF_FALSE      58 (to 79)
           21 POP_TOP

  4        22 BUILD_LIST          0
           25 DUP_TOP
           26 STORE_FAST          3 (_[1])
           29 LOAD_GLOBAL         2 (zip)
           32 LOAD_GLOBAL         1 (types)
           35 LOAD_FAST           2 (fields)
           38 CALL_FUNCTION       2
           41 GET_ITER
        >> 42 FOR_ITER           25 (to 70)
           45 UNPACK_SEQUENCE     2
           48 STORE_FAST          4 (ty)
           51 STORE_FAST          5 (val)
           54 LOAD_FAST           3 (_[1])
           57 LOAD_FAST           4 (ty)
           60 LOAD_FAST          5 (val)
           63 CALL_FUNCTION       1
           66 LIST_APPEND
           67 JUMP_ABSOLUTE      42
        >> 70 DELETE_FAST         3 (_[1])
           73 STORE_FAST          2 (fields)
           76 JUMP_FORWARD        1 (to 80)
        >> 79 POP_TOP

  5     >> 80 LOAD_FAST           2 (fields)
           83 RETURN_VALUE
>>>
```

专业程序员可以以两种方式利用这些信息。首先，反汇编可以向你展示执行一个函数时到底涉及哪些操作。通过仔细研究，你可能会发现加速的机会。其次，如果你使用线程编程，反汇编中打印的每一行代表一个单独的解释器操作——每一个操作都是原子执行的。因此，如果你试图追踪一个棘手的竞态条件，这些信息可能会很有用。

## 第 11 章 测试、调试、分析和调优

##### 调优策略

以下几节概述了一些优化策略，在作者看来，这些策略对 Python 代码已被证明是有效的。

###### 理解你的程序

在优化任何内容之前，请了解通过优化程序的一部分所获得的加速比与该部分对执行时间的总贡献直接相关。例如，如果你通过使一个函数运行速度提高 10 倍来优化它，但该函数仅占程序总执行时间的 10%，那么你只能获得大约 9%–10% 的整体加速比。根据进行优化所涉及的工作量，这可能值得也可能不值得。

始终建议先对你打算优化的代码使用分析模块。你真正应该关注的是程序花费大部分时间的函数和方法，而不是偶尔才被调用的冷门操作。

###### 理解算法

实现不佳的 O(n log n) 算法会优于最精细调优的 O(n³) 算法。不要优化低效的算法——首先寻找更好的算法。

###### 使用内置类型

Python 的内置 tuple、list、set 和 dictionary 类型完全用 C 实现，是解释器中经过最精细调优的数据结构。你应该积极使用这些类型来存储和操作程序中的数据，抵制构建模仿其功能的自定义数据结构（即二叉搜索树、链表等）的冲动。

话虽如此，你仍然应该更仔细地研究标准库中的类型。一些库模块提供的新类型在某些任务上优于内置类型。例如，`collections.deque` 类型提供与列表类似的功能，但针对在两端插入新项目进行了高度优化。相比之下，列表仅在末尾追加项目时才高效。如果你在前面插入项目，所有其他元素都需要移动以腾出空间。完成此操作所需的时间随着列表变得越来越大而增长。为了让你了解差异，以下是分别在列表和 deque 前端插入一百万项的计时测量：

```
>>> from timeit import timeit
>>> timeit('s.appendleft(37)',
...        'import collections; s = collections.deque()',
...        number=1000000)
0.24434304237365723
>>> timeit('s.insert(0,37)', 's = []', number=1000000)
612.95199513435364
```

###### 不要添加层次

每当你为对象或函数添加额外的抽象层或便利层时，你都会使程序变慢。然而，可用性和性能之间也存在权衡。例如，添加额外层次的整个目的通常是为了简化编码，这也是一件好事。



通过一个简单的例子来说明，考虑一个使用 `dict()` 函数创建字符串键字典的程序，如下所示：

`s = dict(name='GOOG', shares=100, price=490.10)`
`# s = {'name':'GOOG', 'shares':100, 'price':490.10 }`

程序员可能会以这种方式创建字典以节省输入（不必在键名周围加引号）。然而，这种创建字典的替代方式也运行得慢得多，因为它增加了一次额外的函数调用。

```
>>> timeit("s = {'name':'GOOG','shares':100,'price':490.10}")
0.38917303085327148
>>> timeit("s = dict(name='GOOG',shares=100,price=490.10)")
0.94420003890991211
```

如果你的程序在运行时创建了数百万个字典，那么你应该知道第一种方法更快。几乎没有例外，任何增加功能特性或改变现有 Python 对象工作方式的方法都会运行得更慢。

###### 了解类和实例如何基于字典构建

用户定义的类和实例是使用字典构建的。因此，查找、设置或删除实例数据的操作几乎总是比直接在字典上执行这些操作运行得更慢。如果你只是构建一个简单的数据结构来存储数据，字典可能比定义类更高效。

为了说明差异，下面是一个表示股票持仓的简单类：

```
class Stock(object):
    def __init__(self,name,shares,price):
        self.name = name
        self.shares = shares
        self.price = price
```

如果你比较使用这个类与字典的性能，结果会很有趣。首先，让我们比较简单创建实例的性能：

```
>>> from timeit import timeit
>>> timeit("s = Stock('GOOG',100,490.10)","from stock import Stock")
1.3166780471801758
>>> timeit("s = {'name' : 'GOOG', 'shares' : 100, 'price' : 490.10 }")
0.37812089920043945
>>>
```

这里，创建新对象的速度提升大约是 3.5 倍。接下来，让我们看看执行简单计算的性能：

```
>>> timeit("s.shares*s.price",
...         "from stock import Stock; s = Stock('GOOG',100,490.10)")
0.29100513458251953
>>> timeit("s['shares']*s['price']",
...         "s = {'name' : 'GOOG', 'shares' : 100, 'price' : 490.10 }")
0.23622798919677734
>>>
```

这里，速度提升大约是 1.2 倍。这里的教训是，仅仅因为你可以使用类定义一个新对象，并不意味着它是处理数据的唯一方式。元组和字典通常已经足够好。使用它们会使你的程序运行更快并占用更少的内存。

###### 使用 `__slots__`

如果你的程序创建了大量用户定义类的实例，你可能会考虑在类定义中使用 `__slots__` 属性。例如：

```
class Stock(object):
    __slots__ = ['name','shares','price']
    def __init__(self,name,shares,price):
        self.name = name
        self.shares = shares
        self.price = price
```

`__slots__` 有时被视为一项安全特性，因为它限制了属性名的集合。然而，它实际上更是一种性能优化。使用 `__slots__` 的类不使用字典来存储实例数据（相反，使用更高效的内部数据结构）。因此，实例不仅会占用少得多的内存，而且访问实例数据也更高效。在某些情况下，仅仅添加 `__slots__` 就会使程序运行明显更快，而无需进行任何其他更改。

然而，使用 `__slots__` 有一个注意事项。向类添加此特性可能会导致其他代码神秘地中断。例如，众所周知，实例将其数据存储在可作为 `__dict__` 属性访问的字典中。当定义了 slots 时，这个属性不存在，因此任何依赖 `__dict__` 的代码都会失败。

###### 避免使用 (.) 运算符

每当你使用 (.) 查找对象上的属性时，它总是涉及名称查找。例如，当你说 `x.name` 时，首先在环境中查找变量名 "x"，然后查找 `x` 上的属性 "name"。对于用户定义的对象，属性查找可能涉及在实例字典、类字典和基类的字典中查找。

对于涉及大量使用方法或模块查找的计算，几乎总是最好通过将要执行的操作放入局部变量中来消除属性查找。例如，如果你要执行大量平方根运算，使用 `from math import sqrt` 和 `sqrt(x)` 比输入 `math.sqrt(x)` 更快。在本节的第一部分，我们看到这种方法带来了大约 1.4 倍的速度提升。

显然，你不应该试图在程序的所有地方消除属性查找，因为这会使你的代码非常难以阅读。然而，对于性能关键的部分，这是一种有用的技术。

###### 使用异常处理不常见的情况

为了避免错误，你可能倾向于向程序添加额外的检查。例如：

```
def parse_header(line):
    fields = line.split(":")
    if len(fields) != 2:
        raise RuntimeError("Malformed header")
    header, value = fields
    return header.lower(), value.strip()
```

然而，处理错误的另一种方法是简单地让程序生成异常并捕获它。例如：

```
def parse_header(line):
    fields = line.split(":")
    try:
        header, value = fields
        return header.lower(), value.strip()
    except ValueError:
        raise RuntimeError("Malformed header")
```

如果你在一个格式正确的行上对两个版本进行基准测试，第二段代码的运行速度快约 10%。为通常不会引发异常的代码设置一个 `try` 块，比执行 `if` 语句运行得更快。

###### 避免为常见情况使用异常

不要编写对常见情况使用异常处理的代码。例如，假设你有一个执行大量字典查找的程序，但这些查找大多是针对不存在的键。现在，考虑执行查找的两种方法：

```
####### 方法 1：执行查找并捕获异常
try:
    value = items[key]
except KeyError:
    value = None

####### 方法 2：检查键是否存在并执行查找
if key in items:
    value = items[key]
else:
    value = None
```

在一个简单的性能测量中（键未找到），第二种方法运行速度快了 17 倍以上！如果你想知道的话，后一种方法也比使用 `items.get(key)` 运行快了近一倍，因为 `in` 运算符执行起来比方法调用更快。

##### 拥抱函数式编程和迭代

列表推导式、生成器表达式、生成器、协程和闭包比大多数 Python 程序员认识到的要高效得多。特别是对于数据处理，列表推导式和生成器表达式比手动迭代数据并执行类似操作的代码运行得明显更快。这些操作也比使用 `map()` 和 `filter()` 等函数的遗留 Python 代码运行得快得多。生成器可用于编写不仅运行速度快，而且能高效利用内存的代码。

##### 使用装饰器和元类

装饰器和元类是用于修改函数和类的特性。然而，由于它们在函数或类定义时运行，因此可以用于提高性能的方式——特别是如果程序有许多可以开启或关闭的可选功能。第 6 章“函数和函数式编程”中有一个使用装饰器启用函数日志记录的例子，但其方式是在日志记录禁用时不会影响性能。

## Python 库

- 12 内置函数
- 13 Python 运行时服务
- 14 数学运算
- 15 数据结构、算法和实用工具
- 16 字符串和文本处理
- 17 Python 数据库访问
- 18 文件和目录处理
- 19 操作系统服务
- 20 线程和并发
- 21 网络编程和套接字
- 22 互联网应用编程
- 23 Web 编程
- 24 互联网数据处理和编码
- 25 杂项库模块



## 12

## 内置函数与异常

本章介绍 Python 的内置函数和异常。本书前面章节已非正式地涵盖了大部分内容，本章只是将这些信息整合到一个章节中，并对某些函数更细微的特性进行扩展说明。此外，Python 2 包含一些被视为过时的内置函数，这些函数已在 Python 3 中移除。这些函数在此不再赘述——本章重点在于现代功能。

#### 内置函数与类型

某些类型、函数和变量始终对解释器可用，可在任何源模块中使用。尽管无需执行额外的导入即可使用这些函数，但它们在 Python 2 中包含于 `__builtin__` 模块，在 Python 3 中则位于 `builtins` 模块。在你导入的其他模块中，变量 `__builtins__` 也绑定到此模块。

```
abs(x)
```

返回 *x* 的绝对值。

```
all(s)
```

如果可迭代对象 *s* 中所有值的布尔值均为 `True`，则返回 `True`。

```
any(s)
```

如果可迭代对象 *s* 中任意值的布尔值为 `True`，则返回 `True`。

```
ascii(x)
```

创建对象 *x* 的可打印表示形式，类似于 `repr()`，但结果仅使用 ASCII 字符。非 ASCII 字符将转换为相应的转义序列。可用于在不支持 Unicode 的终端或 shell 中查看 Unicode 字符串。仅限 Python 3。

```
basestring
```

这是 Python 2 中所有字符串（`str` 和 `unicode`）的超类的抽象数据类型。仅用于字符串类型测试。例如，如果 *s* 是任一字符串类型，`isinstance(s,basestring)` 返回 `True`。仅限 Python 2。

```
bin(x)
```

返回包含整数 *x* 的二进制表示的字符串。

```
bool([x])
```

表示布尔值 `True` 和 `False` 的类型。若用于转换 *x*，当 *x* 使用常规真值测试语义（即非零数字、非空列表等）求值为真时返回 `True`，否则返回 `False`。`False` 也是调用 `bool()` 无参数时的默认返回值。`bool` 类继承自 `int`，因此布尔值 `True` 和 `False` 可在数学计算中作为值为 1 和 0 的整数使用。

```
bytearray([x])
```

表示可变字节数组的类型。创建实例时，*x* 可以是 0 到 255 范围内的整数可迭代序列、8位字符串或字节字面量，或指定字节数组大小的整数（此时每个元素初始化为 0）。`bytearray` 对象 *a* 类似于整数数组。执行 `a[i]` 等查找操作将返回索引 *i* 处表示字节值的整数。`a[i] = v` 等赋值操作也要求 *v* 为整数字节值。然而，`bytearray` 也提供通常与字符串相关的所有操作（即切片、`find()`、`split()`、`replace()` 等）。使用这些字符串操作时，应确保所有字符串字面量以 `b` 为前缀以表明处理的是字节。例如，若要使用逗号字符分隔符拆分字节数组 *a*，应使用 `a.split(b',')` 而非 `a.split(',')`。这些操作的结果始终是新的 `bytearray` 对象而非字符串。要将 `bytearray` *a* 转换为字符串，请使用 `a.decode(encoding)` 方法。编码为 `'latin-1'` 时，会直接将包含8位字符的 `bytearray` 转换为字符串而不修改底层字符值。

```
bytearray(s, encoding)
```

从字符串 *s* 中的字符创建 `bytearray` 实例的替代调用约定，其中 *encoding* 指定转换中使用的字符编码。

```
bytes([x])
```

表示不可变字节数组的类型。在 Python 2 中，这是 `str()` 的别名，用于创建标准8位字符串。在 Python 3 中，`bytes` 是完全独立的类型，是前面描述的 `bytearray` 类型的不可变版本。此时参数 *x* 的解释方式相同，用法也一致。需注意一个可移植性问题：尽管 `bytes` 在 Python 2 中已定义，但生成的对象行为与 Python 3 不一致。例如，若 *a* 是由 `bytes()` 创建的实例，`a[i]` 在 Python 2 中返回字符串，而在 Python 3 中返回整数。

```
bytes(s, encoding)
```

从字符串 *s* 中的字符创建 `bytes` 实例的替代调用约定，其中 *encoding* 指定使用的字符编码。仅限 Python 3。

```
chr(x)
```

将整数值 `x` 转换为单个字符的字符串。在 Python 2 中，`x` 必须在 `0 <= x <= 255` 范围内；在 Python 3 中，`x` 必须表示有效的 Unicode 码点。如果 `x` 超出范围，将引发 `ValueError` 异常。

```
classmethod(func)
```

此函数为函数 *func* 创建类方法。通常仅在类定义中使用，由 `@classmethod` 装饰器隐式调用。与普通方法不同，类方法接收类而非实例作为第一个参数。例如，若对象 `f` 是类 `Foo` 的实例，在 `f` 上调用类方法时，会将类 `Foo`（而非实例 `f`）作为第一个参数传递给该方法。

```
cmp(x, y)
```

比较 `x` 和 `y`，若 `x < y` 返回负数，若 `x > y` 返回正数，若 `x == y` 返回 `0`。任何两个对象均可比较，但如果两个对象未定义有意义的比较方法（例如比较数字与文件对象），结果可能无意义。在某些情况下，此类比较也可能引发异常。

```
compile(string, filename, kind [, flags [, dont_inherit]])
```

将 *string* 编译为代码对象以供 `exec()` 或 `eval()` 使用。*string* 是包含有效 Python 代码的字符串。如果代码跨越多行，每行必须以单个换行符（`'\n'`）终止，而非平台特定变体（例如 Windows 上的 `'\r\n'`）。*filename* 是包含字符串定义所在文件名的字符串。*kind* 为语句序列时设为 `'exec'`，为单个表达式时设为 `'eval'`，为单个可执行语句时设为 `'single'`。*flags* 参数决定启用哪些可选功能（与 `__future__` 模块相关）。功能通过 `__future__` 模块中定义的标志位或运算指定。例如，若要启用新除法语义，可将 *flags* 设为 `__future__.division.compiler_flag`。若省略 *flags* 或设为 `0`，代码将使用当前生效的功能编译。若提供 *flags*，指定的功能将添加到已生效的功能中。若设置 *dont_inherit*，则仅启用 *flags* 中指定的功能——当前已启用的功能将被忽略。

```
complex([real [, imag]])
```

表示复数的类型，具有实部 *real* 和虚部 *imag*，可指定为任意数字类型。若省略 *imag*，虚部设为零。若将 *real* 作为字符串传递，该字符串将被解析并转换为复数。此时应省略 *imag*。若无参数，则返回 `0j`。

```
delattr(object, attr)
```

删除对象的属性。*attr* 是字符串。等同于 `del object.attr`。

```
dict([m]) 或 dict(key1 = value1, key2 = value2, ...)
```

表示字典的类型。若无参数则返回空字典。若 *m* 是映射对象（如字典），则返回具有与 *m* 相同键和值的新字典。例如，若 *m* 是字典，`dict(m)` 仅创建其浅拷贝。若 *m* 不是映射对象，则必须支持迭代以生成 (键, 值) 对序列。这些对用于填充字典。`dict()` 也可使用关键字参数调用。例如，`dict(foo=3, bar=7)` 创建字典 `{ 'foo' : 3, 'bar' : 7 }`。

```
dir([object])
```

返回属性名称的排序列表。若 *object* 是模块，则包含该模块中定义的符号列表。若 *object* 是类型或类对象，则返回属性名称列表。名称通常从对象的 `__dict__` 属性（如果已定义）获取，但也可使用其他来源。若无参数，则返回当前局部符号表中的名称。应注意，此函数主要用于信息目的（例如在命令行交互使用）。不应将其用于正式程序分析，因为获取的信息可能不完整。此外，用户定义的类可以定义特殊方法 `__dir__()` 来更改此函数的结果。

```
divmod(a, b)
```

返回长除法的商和余数元组。对于整数，返回值 `(a // b, a % b)`。对于浮点数，返回 `(math.floor(a / b), a % b)`。不能对复数调用此函数。

```
enumerate(iter[, initial value])
```

给定可迭代对象 *iter*，返回一个新迭代器（enumerate 类型），生成包含计数和 *iter* 产生的值的元组。例如，若 *iter* 生成 a, b, c，则 `enumerate(iter)` 生成 (0,a), (1,b), (2,c)。

```
eval(expr [, globals [, locals]])
```

计算表达式。*expr* 是字符串或由 `compile()` 创建的代码对象。*globals* 和 *locals* 是定义操作全局和局部命名空间的映射对象。若省略，则在调用者的命名空间中计算表达式。通常将 *globals* 和 *locals* 指定为字典，但高级应用可提供自定义映射对象。

```
exec(code [, global [, locals]])
```

执行 Python 语句。*code* 是字符串、文件或由 `compile()` 创建的代码对象。*globals* 和 *locals* 定义操作的全局和局部命名空间。若省略，则在调用者的命名空间中执行代码。若未提供全局或局部字典，此函数的行为在不同 Python 版本中略有差异。在 Python 2 中，`exec` 实际上作为特殊语言语句实现，而 Python 3 将其实现为标准库函数。此实现差异的一个微妙副作用是：在 Python 2 中，`exec` 执行的代码可自由修改调用者命名空间中的局部变量；在 Python 3 中，可以执行此类更改的代码，但除了 `exec()` 调用本身外似乎没有持久效果。这是因为 Python 3 在未提供局部命名空间时使用 `locals()` 获取。如 `locals()` 文档所述，返回的字典仅安全用于检查，不可修改。



##### filter(function, iterable)

##### float([x])

表示浮点数的类型。如果 `x` 是数字，则将其转换为浮点数。如果 `x` 是字符串，则将其解析为浮点数。如果未提供参数，则返回 `0.0`。

##### format(value [, format_spec])

根据 `format_spec` 中的格式规范字符串将 `value` 转换为格式化的字符串。此操作会调用 `value.__format__()`，该方法可以自由解释格式规范。对于简单数据类型，格式说明符通常包括一个对齐字符 '<'、'>' 或 '^'；一个数字（表示字段宽度）；以及一个字符代码 'd'、'f' 或 's'，分别用于整数、浮点数或字符串值。例如，格式说明符 'd' 用于格式化整数，'8d' 在 8 字符字段中右对齐整数，而 '<8d' 在 8 字符字段中左对齐整数。关于 `format()` 和格式说明符的更多详细信息，请参阅第 3 章“类型与对象”和第 4 章“运算符与表达式”。

##### frozenset([items])

表示不可变集合对象的类型，其值取自 `items`（必须是一个可迭代对象）。这些值也必须是不可变的。如果未提供参数，则返回一个空集。

##### getattr(object, name [,default])

返回对象的一个命名属性的值。`name` 是一个包含属性名称的字符串。`default` 是一个可选值，如果该属性不存在则返回此值。否则，将引发 `AttributeError`。等同于 `object.name`。

##### globals()

返回表示当前模块全局命名空间的字典。在另一个函数或方法内部调用时，它返回定义该函数或方法的模块的全局命名空间。

##### hasattr(object, name)

如果 `name` 是 `object` 的一个属性名称，则返回 `True`。否则返回 `False`。`name` 是一个字符串。

##### hash(object)

返回一个对象（如果可能）的整数哈希值。哈希值主要用于字典、集合和其他映射对象的实现。任何两个比较相等的对象具有相同的哈希值。可变对象不定义哈希值，尽管用户定义的类可以定义 `__hash__()` 方法以支持此操作。

##### help([object])

在交互式会话期间调用内置帮助系统。`object` 可以是一个字符串，表示模块、类、函数、方法、关键字或文档主题的名称。如果是任何其他类型的对象，将生成与该对象相关的帮助屏幕。如果未提供参数，将启动交互式帮助工具并提供更多信息。

##### hex(x)

从整数 `x` 创建一个十六进制字符串。

##### id(object)

返回 `object` 的唯一整数标识。你不应以任何方式解释返回值（即，不要将其视为内存位置）。

##### input([prompt])

在 Python 2 中，此函数打印提示符，读取一行输入，并通过 `eval()` 处理（即，等同于 `eval(raw_input(prompt))`）。在 Python 3 中，会向标准输出打印提示符，并读取单行输入，而不进行任何求值或修改。

##### int(x [,base])

表示整数的类型。如果 `x` 是数字，则通过向零截断将其转换为整数。如果 `x` 是字符串，则将其解析为整数值。`base` 可选地指定从字符串转换时的基数。在 Python 2 中，如果值超出 `int` 类型的 32 位范围，则会创建长整数。

##### isinstance(object, classobj)

如果 `object` 是 `classobj` 的实例、是 `classobj` 的子类或属于抽象基类 `classobj`，则返回 `True`。`classobj` 参数也可以是可能的类型或类的元组。例如，如果 `s` 是元组或列表，`isinstance(s, (list,tuple))` 返回 `True`。

##### issubclass(class1, class2)

如果 `class1` 是 `class2` 的子类（派生自 `class2`）或者 `class1` 已注册为抽象基类 `class2`，则返回 `True`。`class2` 也可以是一个可能的类的元组，在这种情况下，将检查每个类。请注意，`issubclass(A, A)` 为真。

##### iter(object [,sentinel])

返回一个用于从 `object` 中产生元素的迭代器。如果省略 `sentinel` 参数，该对象必须要么提供创建迭代器的 `__iter__()` 方法，要么实现接受从 0 开始的整数参数的 `__getitem__()` 方法。如果指定了 `sentinel`，则 `object` 的解释方式不同。此时，`object` 应该是一个不带参数的可调用对象。返回的迭代器对象将重复调用此函数，直到返回值等于 `sentinel`，此时迭代停止。如果 `object` 不支持迭代，将生成 `TypeError`。

##### len(s)

返回 `s` 中包含的项数。`s` 应该是一个列表、元组、字符串、集合或字典。如果 `s` 是一个可迭代对象（如生成器），则会生成 `TypeError`。

##### list([items])

表示列表的类型。*items* 可以是任何可迭代对象，其值用于填充列表。如果 *items* 已经是一个列表，则会创建一个副本。如果未提供参数，则返回一个空列表。

##### locals()

返回一个对应于调用者本地命名空间的字典。此字典仅应用于检查执行环境——修改此字典的内容是不安全的。

##### long([x [, base]])

在 Python 2 中表示长整数的类型。如果 *x* 是数字，则通过向零截断将其转换为整数。如果 *x* 是字符串，则将其解析为长值。如果未提供参数，此函数返回 `0L`。为了可移植性，应避免直接使用 `long`。使用 `int(x)` 将在必要时创建 `long`。对于类型检查，使用 `isinstance(x, numbers.Integral)` 检查 *x* 是否为任何整数类型。

##### map(function, items, ...)

在 Python 2 中，此函数将 *function* 应用于 *items* 的每个元素，并返回结果列表。在 Python 3 中，会创建一个产生相同结果的迭代器。如果提供了多个输入序列，则假定 *function* 接受相应数量的参数，每个参数取自不同的序列。处理多个输入序列时，Python 2 和 Python 3 的行为不同。在 Python 2 中，结果长度与最长输入序列相同，当较短的输入序列耗尽时，使用 `None` 作为填充值。在 Python 3 中，结果长度仅与最短序列相同。`map()` 提供的功能几乎总是通过生成器表达式或列表推导来表达会更好（两者都提供更好的性能）。例如，`map(function, s)` 通常可以用 `[function(x) for x in s]` 替换。

##### max(s [,args, ...])

对于单个参数 *s*，此函数返回 *s* 中项的最大值，*s* 可以是任何可迭代对象。对于多个参数，则返回参数中的最大值。

##### min(s [,args, ...])

对于单个参数 *s*，此函数返回 *s* 中项的最小值，*s* 可以是任何可迭代对象。对于多个参数，则返回参数中的最小值。

##### next(s [, default])

从迭代器 *s* 返回下一个项。如果迭代器没有更多项，则会引发 `StopIteration` 异常，除非为 *default* 参数提供了值。在这种情况下，将返回 *default* 代替。为了可移植性，应始终使用此函数，而不是直接在迭代器 *s* 上调用 `s.next()`。在 Python 3 中，底层迭代器方法的名称更改为 `s.__next__()`。如果你编写代码时使用 `next()` 函数，就无需担心这种差异。

##### object()

Python 中所有对象的基类。你可以调用它来创建一个实例，但结果并不特别有趣。

##### oct(x)

将整数 x 转换为八进制字符串。

##### open(filename [, mode [, bufsize]])

在 Python 2 中，打开文件 filename 并返回一个新的文件对象（参见第 9 章“输入与输出”）。mode 是一个字符串，指示文件应如何打开：'r' 表示读取，'w' 表示写入，'a' 表示追加。第二个字符 't' 或 'b' 用于指示文本模式（默认）或二进制模式。例如，'r' 或 'rt' 以文本模式打开文件，而 'rb' 以二进制模式打开文件。可选的 '+' 可以添加到模式中，以打开文件进行更新（允许同时读写）。如果文件已存在，'w+' 模式会将其截断为零长度。'r+' 或 'a+' 模式打开文件以进行读写，但在打开文件时保留原始内容。如果指定 'U' 或 'rU' 模式，文件将以通用换行模式打开。在此模式下，所有换行符变体（'\n'、'\r'、'\r\n'）都会转换为标准的 '\n' 字符。如果省略模式，则假定为 'rt'。bufsize 参数指定缓冲行为，其中 0 表示无缓冲，1 表示行缓冲，任何其他正数表示大约的缓冲区大小（以字节为单位）。负数表示应使用系统默认缓冲区（这是默认行为）。

##### open(filename [, mode [, bufsize [, encoding [, errors [, newline [, closefd]]]]])

在 Python 3 中，此函数打开文件 filename 并返回一个文件对象。前三个参数与前面描述的 Python 2 版本的 open() 含义相同。encoding 是编码名称，例如 'utf-8'。errors 是错误处理策略，是 'strict'、'ignore'、'replace'、'backslashreplace' 或 'xmlcharrefreplace' 之一。newline 控制通用换行模式的行为，设置为 None、''、'\n'、'\r' 或 '\r\n'。closefd 是一个布尔标志，指定当 close() 方法执行时是否关闭底层文件描述符。与 Python 2 不同，根据选择的 I/O 模式，返回不同类型的对象。例如，如果以二进制模式打开文件，你会得到一个对象，其中 I/O 操作（如 read() 和 write()）在字节数组而不是字符串上操作。文件 I/O 是 Python 2 和 3 之间存在显著差异的一个领域。更多详细信息，请查阅附录 A “Python 3”。

##### ord(c)

返回单个字符 c 的整数序数值。对于普通字符，返回范围 [0,255] 内的值。对于单个 Unicode 字符，通常返回范围 [0,65535] 内的值。在 Python 3 中，c 也可以是 Unicode 代理对，在这种情况下，它将被转换为相应的 Unicode 码点。

##### pow(x, y [, z])

返回 x ** y。如果提供了 z，此函数返回 (x ** y) % z。如果给出了所有三个参数，它们必须是整数，并且 y 必须是非负数。



##### print(value, ... [, sep=separator, end=ending, file=outfile])

Python 3 中用于打印一系列值的函数。作为输入，你可以提供任意数量的值，它们都会被打印在同一行。`sep` 关键字参数用于指定不同的分隔符（默认为一个空格）。`end` 关键字参数指定不同的行尾符（默认为 `'\n'`）。`file` 关键字参数将输出重定向到一个文件对象。如果你在代码中添加了 `from __future__ import print_function` 语句，这个函数也可以在 Python 2 中使用。

##### property([fget [,fset [,fdel [,doc]]]])

为类创建一个属性。`fget` 是一个返回属性值的函数，`fset` 用于设置属性值，`fdel` 用于删除属性。`doc` 提供一个文档字符串。这些参数可以通过关键字参数提供——例如，`property(fget=getX, doc="some text")`。

##### range([start,] stop [, step])

在 Python 2 中，这会创建一个从 `start` 到 `stop`（不包括 `stop`）的、完全填充的整数列表。`step` 表示步长，如果省略则默认为 `1`。如果省略 `start`（当 `range()` 只使用一个参数调用时），它默认为 `0`。负数 `step` 会创建一个降序排列的数字列表。在 Python 3 中，`range()` 创建一个特殊的 range 对象，它按需计算其值（类似于早期 Python 版本中的 `xrange()`）。

##### raw_input([prompt])

Python 2 中的函数，从标准输入（`sys.stdin`）读取一行输入并将其作为字符串返回。如果提供了 `prompt`，它会首先被打印到标准输出（`sys.stdout`）。尾随的换行符会被剥离，如果读取到 EOF 则会引发 `EOFError` 异常。如果加载了 `readline` 模块，此函数将使用它来提供高级行编辑和命令补全功能。在 Python 3 中，请使用 `input()` 来读取输入。

##### repr(object)

返回 `object` 的字符串表示形式。在大多数情况下，返回的字符串是一个表达式，可以传递给 `eval()` 以重新创建该对象。请注意，在 Python 3 中，此函数的结果可能是一个无法在终端或 Shell 窗口中显示的 Unicode 字符串（从而导致异常）。使用 `ascii()` 函数可以创建 `object` 的 ASCII 表示形式。

##### reversed(s)

为序列 `s` 创建一个反向迭代器。此函数仅在 `s` 实现了序列方法 `__len__()` 和 `__getitem__()` 时才有效。此外，`s` 必须从 0 开始对元素进行索引。它不适用于生成器或迭代器。

##### round(x [, n])

将浮点数 `x` 四舍五入到最接近的 10 的负 `n` 次幂的倍数。如果省略 `n`，则默认为 `0`。如果两个倍数同样接近，Python 2 会远离 `0` 进行舍入（例如，`0.5` 被舍入为 `1.0`，`-0.5` 被舍入为 `-1.0`）。Python 3 采用“银行家舍入法”：如果前一位数字是偶数，则向 `0` 方向舍入；否则远离 `0` 舍入（例如，`0.5` 被舍入为 `0.0`，`1.5` 被舍入为 `2`）。

##### set([items])

创建一个集合，其中包含从可迭代对象 `items` 中取出的元素。元素必须是不可变的。如果 `items` 包含其他集合，那么这些集合必须是 `frozenset` 类型。如果省略 `items`，则返回一个空集。

##### setattr(object, name, value)

设置对象的一个属性。`name` 是一个字符串。等同于 `object.name = value`。

##### slice([start,] stop [, step])

返回一个表示指定范围内整数的切片对象。切片对象也可以由扩展切片语法 `a[i:i:k]` 生成。详细信息请参阅第 3 章“序列和映射方法”部分。

##### sorted(iterable [, key=keyfunc [, reverse=reverseflag]])

从 `iterable` 中的项创建一个排序后的列表。关键字参数 `key` 是一个单参数函数，它在值传递给比较函数之前对值进行转换。关键字参数 `reverse` 是一个布尔标志，指定结果列表是否按逆序排序。`key` 和 `reverse` 参数必须使用关键字指定——例如，`sorted(a,key=get_name)`。

##### staticmethod(func)

创建一个用于类的静态方法。此函数由 `@staticmethod` 装饰器隐式调用。

##### str([object])

表示字符串的类型。在 Python 2 中，字符串包含 8 位字符，而在 Python 3 中，字符串是 Unicode 的。如果提供了 `object`，则通过调用其 `__str__()` 方法创建其值的字符串表示形式。这与你打印该对象时看到的字符串相同。如果未提供参数，则创建一个空字符串。

##### sum(items [,initial])

计算从可迭代对象 `items` 中取出的项序列的和。`initial` 提供起始值，默认为 `0`。此函数仅适用于数字。

##### super(type [, object])

返回一个表示 `type` 的超类的对象。此对象的主要目的是调用基类中的方法。以下是一个示例：

```
class B(A):
    def foo(self):
        super(B,self).foo()
```

如果 `object` 是一个对象，则 `isinstance(object, type)` 必须为真。如果 `object` 是一个类型，则它必须是 `type` 的子类。更多详情请参阅第 7 章“类与面向对象编程”。在 Python 3 中，你可以在方法中使用无参数的 `super()`。在这种情况下，`type` 被设置为方法定义所在的类，`object` 被设置为方法的第一个参数。虽然这简化了语法，但它与 Python 2 不向后兼容，因此如果你关心可移植性，应避免使用。

##### tuple([items])

表示元组的类型。如果提供了 `items`，它是一个用于填充元组的可迭代对象。然而，如果 `items` 本身已经是一个元组，则它会被原样返回。如果未提供参数，则返回一个空元组。

##### type(object)

Python 中所有类型的基类。当作为函数调用时，返回 `object` 的类型。这个类型与对象的类相同。对于常见类型，如整数、浮点数和列表，类型将指向其他内置类之一，如 `int`、`float`、`list` 等。对于用户定义的对象，类型是关联的类。对于与 Python 内部相关的对象，你通常会得到 `types` 模块中定义的某个类的引用。

##### type(name, bases, dict)

创建一个新的 `type` 对象（这等同于定义一个新的类）。`name` 是类型的名称，`bases` 是一个基类的元组，`dict` 是一个包含类体定义的字典。此函数最常用于处理元类。这在第 7 章中有更详细的描述。

##### unichr(x)

将整数或长整数 `x`（其中 `0 <= x <= 65535`）转换为单个 Unicode 字符。仅适用于 Python 2。在 Python 3 中，直接使用 `chr(x)`。

##### unicode(string [, encoding [, errors]])

在 Python 2 中，这会将 `string` 转换为 Unicode 字符串。`encoding` 指定 `string` 的数据编码。如果省略，则使用 `sys.getdefaultencoding()` 返回的默认编码。`errors` 指定如何处理编码错误，是 `'strict'`、`'ignore'`、`'replace'`、`'backslashreplace'` 或 `'xmlcharrefreplace'` 之一。详细信息请参阅第 9 章和第 3 章。在 Python 3 中不可用。

##### vars([object])

返回 `object` 的符号表（通常在其 `__dict__` 属性中找到）。如果未提供参数，则返回对应于局部命名空间的字典。此函数返回的字典应被视为只读。修改其内容是不安全的。

##### xrange([start,] stop [, step])

表示从 `start` 到 `stop`（不包括 `stop`）的整数值范围的类型。`step` 提供可选的步长。值实际上并未存储，而是在访问时按需计算。在 Python 2 中，当你想要编写遍历整数值范围的循环时，`xrange()` 是首选函数。在 Python 3 中，`xrange()` 已被重命名为 `range()`，`xrange()` 不再可用。`start`、`stop` 和 `step` 限于机器整数（通常为 32 位）支持的值集合。

##### zip([s1 [, s2 [,...]])

在 Python 2 中，返回一个元组列表，其中第 *n* 个元组是 `(s1[n], s2[n], ...)`。结果列表会被截断到最短参数序列的长度。如果未提供参数，则返回一个空列表。在 Python 3 中，行为类似，但

结果是一个迭代器，该迭代器生成一系列元组。在 Python 2 中，请注意，对长输入序列使用 `zip()` 可能会意外消耗大量内存。请考虑改用 `itertools.izip()`。

#### 内置异常

内置异常包含在 `exceptions` 模块中，该模块在任何程序执行之前都会被加载。异常被定义为类。

##### 异常基类

以下异常作为所有其他异常的基类：

- **BaseException**：所有异常的根类。所有内置异常都派生自此类。
- **Exception**：所有与程序相关的异常的基类，包括所有内置异常，但 `SystemExit`、`GeneratorExit` 和 `KeyboardInterrupt` 除外。用户定义的异常应通过继承 `Exception` 来定义。
- **ArithmeticError**：算术异常的基类，包括 `OverflowError`、`ZeroDivisionError` 和 `FloatingPointError`。
- **LookupError**：索引和键错误的基类，包括 `IndexError` 和 `KeyError`。
- **EnvironmentError**：发生在 Python 之外的错误的基类，包括 `IOError` 和 `OSError`。

上述异常从未被显式引发。但是，它们可用于捕获特定类别的错误。例如，以下代码将捕获任何类型的数值错误：

```
try:
    # Some operation
    ...
except ArithmeticError as e:
    # Math error
```

##### 异常实例

当异常被引发时，会创建一个异常类的实例。此实例被放置在提供给 `except` 语句的可选变量中。这是一个例子：

```
except IOError as e:
    # Handle error
    # 'e' has an instance of IOError
```

异常 `e` 的实例具有一些标准属性，在某些应用中可用于检查和/或操作。

- **`e.args`**：引发异常时提供的参数元组。在大多数情况下，这是一个包含描述错误的字符串的单元素元组。对于 `EnvironmentError` 异常，该值是一个 2 元组或 3 元组，包含一个整数错误号、一个字符串错误消息和一个可选的文件名。如果您需要在不同的上下文中重新创建异常（例如，在不同的 Python 解释器进程中引发异常），此元组的内容可能很有用。
- **`e.message`**：代表异常显示时打印的错误消息的字符串（仅 Python 2）。
- **`e.__cause__`**：使用显式链接异常时的先前异常（仅 Python 3）。请参见附录 A。
- **`e.__context__`**：用于隐式链接异常的先前异常（仅 Python 3）。请参见附录 A。
- **`e.__traceback__`**：与异常相关联的回溯对象（仅 Python 3）。请参见附录 A。

##### 预定义异常类

以下异常由程序引发：

- **AssertionError**：`assert` 语句失败。
- **AttributeError**：属性引用或赋值失败。
- **EOFError**：文件结束。由内置函数 `input()` 和 `raw_input()` 生成。请注意，大多数其他 I/O 操作，例如文件的 `read()` 和 `readline()` 方法，返回空字符串来表示 EOF，而不是引发异常。
- **FloatingPointError**：浮点运算失败。请注意，浮点异常处理是一个棘手的问题，并且只有在 Python 的配置和构建方式启用了它时才会引发此异常。浮点错误更常见的是静默地产生结果，例如 `float('nan')` 或 `float('inf')`。`ArithmeticError` 的子类。
- **GeneratorExit**：在生成器函数内部引发以表示终止。这发生在生成器被过早销毁（在所有生成器值被消耗之前）或生成器的 `close()` 方法被调用时。如果生成器忽略此异常，则生成器被终止且异常被静默忽略。
- **IOError**：I/O 操作失败。该值是一个 `IOError` 实例，具有属性 `errno`、`strerror` 和 `filename`。`errno` 是一个整数错误号，`strerror` 是一个字符串错误消息，`filename` 是一个可选的文件名。`EnvironmentError` 的子类。
- **ImportError**：导入失败时引发。
- **IndentationError**：缩进错误。`SyntaxError` 的子类。
- **IndexError**：序列下标超出范围。`LookupError` 的子类。
- **KeyError**：在映射中未找到键。`LookupError` 的子类。
- **KeyboardInterrupt**：当用户按下中断键（通常是 Ctrl+C）时引发。
- **MemoryError**：可恢复的内存不足错误。
- **NameError**：在本地或全局命名空间中未找到名称。
- **NotImplementedError**：未实现的功能。可由需要派生类实现某些方法的基类引发。`RuntimeError` 的子类。
- **OSError**：操作系统错误。主要由 `os` 模块中的函数引发。该值与 `IOError` 相同。`EnvironmentError` 的子类。
- **OverflowError**：整数值过大而无法表示的结果。此异常通常仅在大型整数值传递给在其内部实现中依赖固定精度机器整数的对象时才会出现。如果指定超过 32 位大小的起始或结束值，请小心使用 `range` 或 `xrange` 对象。`ArithmeticError` 的子类。
- **ReferenceError**：在底层对象被销毁后访问弱引用的结果。请参见 `weakref` 模块。
- **RuntimeError**：任何其他类别未涵盖的通用错误。
- **StopIteration**：引发以表示迭代结束。这通常发生在对象的 `next()` 方法或生成器函数中。
- **SyntaxError**：解析器语法错误。实例具有属性 `filename`、`lineno`、`offset` 和 `text`，可用于收集更多信息。
- **SystemError**：解释器中的内部错误。该值是一个表示问题的字符串。
- **SystemExit**：由 `sys.exit()` 函数引发。该值是一个表示返回码的整数。如果需要立即退出，可以使用 `os._exit()`。
- **TabError**：不一致的制表符使用。当使用 `-tt` 选项运行 Python 时生成。`SyntaxError` 的子类。
- **TypeError**：当操作或函数应用于不适当类型的对象时发生。
- **UnboundLocalError**：引用未绑定的局部变量。如果在函数中定义变量之前引用了该变量，则会发生此错误。`NameError` 的子类。
- **UnicodeError**：Unicode 编码或解码错误。`ValueError` 的子类。
- **UnicodeEncodeError**：Unicode 编码错误。`UnicodeError` 的子类。
- **UnicodeDecodeError**：Unicode 解码错误。`UnicodeError` 的子类。
- **UnicodeTranslateError**：在翻译过程中发生的 Unicode 错误。`UnicodeError` 的子类。
- **ValueError**：当函数或操作的参数类型正确但值不恰当时生成。
- **WindowsError**：由 Windows 上的系统调用失败生成。`OSError` 的子类。
- **ZeroDivisionError**：除以零。`ArithmeticError` 的子类。

#### 内置警告

Python 有一个 `warnings` 模块，通常用于通知程序员有关已弃用的功能。警告通过包含如下代码来发出：

```
import warnings
warnings.warn("The MONDO flag is no longer supported", DeprecationWarning)
```

尽管警告由库模块发出，但各种警告的名称是内置的。警告与异常有些相似。存在一个内置警告的层次结构，所有警告都继承自 `Exception`。

- **Warning**：所有警告的基类。`Exception` 的子类。
- **UserWarning**：通用的用户定义警告。`Warning` 的子类。
- **DeprecationWarning**：针对已弃用功能的警告。`Warning` 的子类。
- **SyntaxWarning**：针对已弃用的 Python 语法的警告。`Warning` 的子类。
- **RuntimeWarning**：针对潜在运行时问题的警告。`Warning` 的子类。
- **FutureWarning**：警告某个功能的行为将来会发生变化。`Warning` 的子类。

警告与异常的不同之处在于，使用 `warn()` 函数发出警告可能会也可能不会导致程序停止。例如，警告可能只是将某些内容打印到输出，或者可能引发异常。实际行为可以通过 `warnings` 模块或使用解释器的 `-W` 选项进行配置。如果您使用的是生成警告的他人代码，但您无论如何都想继续，您可以使用 `try` 和 `except` 捕获已转换为异常的警告。例如：

```
try:
    import md5
except DeprecationWarning:
    pass
```

应该强调的是，这样的代码很少见。虽然它会捕获已转换为异常的警告，但它不会抑制警告消息（您必须使用 `warnings` 模块来控制）。此外，忽略警告是在 Python 新版本发布时编写不正确工作的代码的好方法。



##### future_builtins

`future_builtins` 模块仅在 Python 2 中可用，它提供了内置函数的实现，这些函数的行为在 Python 3 中发生了改变。定义了以下函数：

```python
ascii(object)
```

产生与 `repr()` 相同的输出。请参阅本章“内置函数”部分中的描述。

```python
filter(function, iterable)
```

创建迭代器而不是列表。与 `itertools.ifilter()` 相同。

```python
hex(object)
```

创建十六进制字符串，但使用 `__index__()` 特殊方法来获取整数值，而不是调用 `__hex__()`。

```python
map(function, iterable, ...)
```

创建迭代器而不是列表。与 `itertools.imap()` 相同。

```python
oct(object)
```

创建八进制字符串，但使用 `__index__()` 特殊方法来获取整数值，而不是调用 `__oct__()`。

```python
zip(iterable, iterable, ...)
```

创建迭代器而不是列表。与 `itertools.izip()` 相同。

请注意，本模块中列出的函数并非内置模块变更的完整列表。例如，Python 3 还将 `raw_input()` 重命名为 `input()`，将 `xrange()` 重命名为 `range()`。

#### Python 运行时服务

本章介绍与 Python 解释器运行时相关的模块。主题包括垃圾回收、对象的基本管理（复制、序列化等）、弱引用以及解释器环境。

##### atexit

atexit 模块用于注册在 Python 解释器退出时执行的函数。提供了单个函数：

```python
register(func [,args [,kwargs]])
```

将函数 `func` 添加到解释器退出时将执行的函数列表中。`args` 是要传递给函数的参数元组。`kwargs` 是关键字参数字典。函数以 `func(*args,**kwargs)` 的形式调用。退出时，函数按注册顺序的相反顺序调用（最近添加的退出函数最先调用）。如果发生错误，异常消息将打印到标准错误，但除此之外会被忽略。

##### copy

copy 模块提供了用于创建复合对象的浅拷贝和深拷贝的函数，包括列表、元组、字典以及用户定义对象的实例。

```python
copy(x)
```

通过创建新的复合对象并引用复制 `x` 的成员来创建 `x` 的浅拷贝。对于内置类型，使用此函数相对少见。相反，您可以使用 `list(x)`、`dict(x)`、`set(x)` 等调用来创建 `x` 的浅拷贝（应注意，像这样直接使用类型名也比使用 `copy()` 显著更快）。

```python
deepcopy(x [, visit])
```

通过创建新的复合对象并递归复制 `x` 的所有成员来创建 `x` 的深拷贝。`visit` 是一个可选的字典，用于跟踪已访问的对象，以便检测和避免递归定义的数据结构中的循环。此参数通常仅在 `deepcopy()` 被递归调用时提供，如本章后面所述。

虽然通常没有必要，但类可以通过实现 `__copy__(self)` 和 `__deepcopy__(self, visit)` 方法来实现自定义的复制方法，分别实现浅拷贝和深拷贝操作。`__deepcopy__()` 方法必须接受一个字典 `visit`，用于跟踪复制过程中先前遇到的对象。`__deepcopy__()` 除了将其传递给实现中执行的其它 `deepcopy()` 操作（如果有）之外，不需要对 `visit` 做任何处理。

如果类实现了 `pickle` 模块使用的 `__getstate__()` 和 `__setstate__()` 方法，它们将被 copy 模块用于创建副本。

##### 注意事项

- 本模块可用于整数和字符串等简单类型，但几乎没有必要这样做。
- 复制函数不适用于模块、类对象、函数、方法、回溯、栈帧、文件、套接字以及其它类似类型。当对象无法复制时，将引发 `copy.error` 异常。

##### gc

`gc` 模块提供了用于控制垃圾回收器的接口，该回收器用于收集列表、元组、字典和实例等对象中的循环引用。随着各种类型的容器对象被创建，它们被放置在解释器内部的列表中。每当容器对象被释放时，它们从此列表中移除。如果分配次数超过释放次数达到用户可定义的阈值，垃圾回收器将被调用。垃圾回收器通过扫描此列表并识别不再使用但尚未由于循环依赖而释放的对象集合来工作。此外，垃圾回收器使用三级分代方案，在初始垃圾回收步骤中存活的对象被放置在检查频率较低的列表上。这对于具有大量长生命周期对象的程序提供了更好的性能。

```python
collect([generation])
```

运行完整的垃圾回收。此函数检查所有分代，并返回找到的不可达对象数量。`generation` 是可选的整数，范围为 0 – 2，指定要回收的分代。

```python
disable()
```

禁用垃圾回收。

```python
enable()
```

启用垃圾回收。

`garbage`

一个变量，包含用户定义实例的只读列表，这些实例不再使用，但由于它们涉及引用循环且定义了 `__del__()` 方法，因此无法被垃圾回收。此类对象无法被垃圾回收，因为为了打破引用循环，解释器必须首先任意销毁其中一个对象。然而，无法知道循环中剩余对象的 `__del__()` 方法是否需要对刚刚被销毁的对象执行关键操作。

`get_count()`

返回包含每个分代中当前对象数量的元组 (`count0`, `count1`, `count2`)。

`get_debug()`

返回当前设置的调试标志。

`get_objects()`

返回垃圾回收器跟踪的所有对象列表。不包括返回的列表本身。

`get_referrers(obj1, obj2, ...)`

返回直接引用对象 `obj1`、`obj2` 等的所有对象列表。返回的列表可能包括尚未被垃圾回收的对象以及部分构造的对象。

`get_referents(obj1, obj2, ...)`

返回对象 `obj1`、`obj2` 等所引用的对象列表。例如，如果 `obj1` 是容器，这将返回容器中对象的列表。

`get_threshold()`

以元组形式返回当前回收阈值。

`isenabled()`

如果启用了垃圾回收，则返回 `True`。

`set_debug(flags)`

设置垃圾回收调试标志，可用于调试垃圾回收器的行为。`flags` 是常量 `DEBUG_STATS`、`DEBUG_COLLECTABLE`、`DEBUG_UNCOLLECTABLE`、`DEBUG_INSTANCES`、`DEBUG_OBJECTS`、`DEBUG_SAVEALL` 和 `DEBUG_LEAK` 的按位或运算。`DEBUG_LEAK` 标志可能最有用，因为它会让回收器打印对调试内存泄漏程序有用的信息。

`set_threshold(threshold0 [, threshold1[, threshold2]])`

设置垃圾回收的回收频率。对象被分为三个分代，其中分代 0 包含最年轻的对象，分代 2 包含最老的对象。在垃圾回收步骤中存活的对象被移动到更老的分代。一旦对象到达分代 2，它将保留在该分代中。`threshold0` 是在分代 0 中发生垃圾回收之前必须达到的分配次数与释放次数之差。`threshold1` 是在扫描分代 1 之前必须发生的分代 0 回收次数。`threshold2` 是在回收分代 2 之前必须发生的分代 1 回收次数。默认阈值当前设置为 (700, 10, 10)。将 `threshold0` 设置为 0 将禁用垃圾回收。



##### 说明

- 涉及带有`__del__()`方法的对象的循环引用不会被垃圾回收，而是被放置在列表`gc.garbage`中（不可回收对象）。这些对象由于与对象终结化相关的困难而不会被收集。

- 函数`get_referrers()`和`get_referents()`仅适用于支持垃圾回收的对象。此外，这些函数仅用于调试目的，不应用于其他用途。

##### inspect

`inspect`模块用于收集有关活动 Python 对象的信息，例如属性、文档字符串、源代码、堆栈帧等。

`cleandoc(doc)`

通过将所有制表符替换为空格并删除可能为对齐函数或方法内其他语句而插入的缩进，来清理文档字符串*doc*。

`currentframe()`

返回与调用者堆栈帧对应的帧对象。

`formatargspec(args[, varargs[, varkw[, defaults]]])`

生成一个格式良好的字符串，表示`getargspec()`返回的值。

`formatargvalues(args[, varargs[, varkw[, locals]]])`

生成一个格式良好的字符串，表示`getargvalues()`返回的值。

`getargspec(func)`

给定函数*func*，返回一个命名元组`ArgSpec(args, varargs, varkw, defaults)`。*args*是参数名称的列表，*varargs*是`*`参数的名称（如果有）。*varkw*是`**`参数的名称（如果有），*defaults*是默认参数值的元组，如果没有默认参数值则为`None`。如果有默认参数值，*defaults*元组表示*args*中最后*n*个参数的值，其中*n*是`len(defaults)`。

`getargvalues(frame)`

返回提供给具有执行帧*frame*的函数的参数值。返回元组`ArgInfo(args, varargs, varkw, locals)`。*args*是参数名称的列表，*varargs*是`*`参数的名称（如果有）。*varkw*是`**`参数的名称（如果有）。*locals*是帧的局部字典。

`getclasstree(classes[, unique])`

给定相关类的列表*classes*，此函数根据继承关系将类组织为层次结构。层次结构表示为嵌套列表的集合，其中列表中的每个条目是继承自紧接该列表之前的类的类列表。列表中的每个条目是一个2元组`(cls, bases)`，其中*cls*是类对象，*bases*是基类的元组。如果*unique*为True，则每个类在返回的列表中只出现一次。否则，如果使用多重继承，一个类可能会出现多次。

`getcomments(object)`

返回一个由紧接在 Python 源代码中对象定义之前的注释组成的字符串。如果*object*是模块，则返回模块顶部定义的注释。如果未找到注释，则返回None。

`getdoc(object)`

返回对象的文档字符串。文档字符串在返回之前首先使用`cleandoc()`函数进行处理。

`getfile(object)`

返回定义对象的文件名。如果此信息不适用或不可用（例如，对于内置函数），则可能返回TypeError。

`getframeinfo(frame [, context])`

返回一个命名元组Traceback(filename, lineno, function, code_context, index)，包含有关帧对象*frame*的信息。filename和line指定源代码位置。*context*参数指定要检索的源代码上下文行数。返回元组中的contextlist字段包含与此上下文对应的源代码行列表。index字段是对应于*frame*的行的此列表中的数字索引。

`getinnerframes(traceback [, context])`

返回回溯帧和所有内部帧的帧记录列表。每个帧记录是一个6元组，由(frame, filename, line, funcname, contextlist, index)组成。filename、line、context、contextlist和index的含义与`getframeinfo()`相同。

`getmembers(object [, predicate])`

返回对象的所有成员。通常，成员是通过查看对象的`__dict__`属性获得的，但此函数可能返回存储在其他地方的对象属性（例如，`__doc__`中的文档字符串，对象在`__name__`中的名称等）。成员以(name, value)对的列表形式返回。*predicate*是一个可选函数，接受成员对象作为参数并返回True或False。仅返回*predicate*返回True的成员。函数如`isfunction()`和`isclass()`可用作*predicate*函数。

`getmodule(object)`

返回定义对象的模块（如果可能）。

`getmoduleinfo(path)`

返回有关 Python 如何解释文件路径的信息。如果*path*不是 Python 模块，则返回None。否则，返回一个命名元组ModuleInfo(name, suffix, mode, module_type)，其中*name*是模块的名称，*suffix*是文件名后缀，*mode*是用于打开模块的文件模式，*module_type*是指定模块类型的整数代码。模块类型代码在imp模块中定义如下：

| 模块类型 | 描述 |
|-------------|-------------|
| imp.PY_SOURCE | Python 源文件 |
| imp.PY_COMPILED | Python 编译对象文件 (.pyc) |
| imp.C_EXTENSION | 动态可加载 C 扩展 |
| imp.PKG_DIRECTORY | 包目录 |
| imp.C_BUILTIN | 内置模块 |
| imp.PY_FROZEN | 冻结模块 |

`getmodulename(path)`

返回用于文件路径的模块名称。如果*path*看起来不像 Python 模块，则返回None。

`getmro(cls)`

返回表示用于解析类*cls*中方法的方法解析顺序的类元组。更多详情请参考第7章"类和面向对象编程"。

`getouterframes(frame [, context])`

返回*frame*和所有外部帧的帧记录列表。此列表表示调用序列，其中第一个条目包含*frame*的信息。每个帧记录是一个6元组(frame, filename, line, funcname, contextlist, index)，其中字段的含义与`getinnerframes()`相同。*context*参数的含义与`getframeinfo()`相同。

`getsourcefile(object)`

返回定义对象的 Python 源文件的名称。

`getsourcelines(object)`

返回对应于对象定义的元组(sourcelines, firstline)。*sourcelines*是源代码行列表，*firstline*是第一行源代码的行号。如果找不到源代码，则引发IOError。

`getsource(object)`

返回对象的源代码作为单个字符串。如果找不到源代码，则引发IOError。

`isabstract(object)`

如果*object*是抽象基类，则返回True。

`isbuiltin(object)`

如果*object*是内置函数，则返回True。

`isclass(object)`

如果*object*是类，则返回True。

`iscode(object)`

如果*object*是代码对象，则返回True。

`isdatadescriptor(object)`

如果*object*是数据描述符对象，则返回True。如果*object*同时定义了`__get__()`和`__set__()`方法，则属于这种情况。

`isframe(object)`

如果*object*是帧对象，则返回True。

`isfunction(object)`

如果*object*是函数对象，则返回True。

`isgenerator(object)`

如果*object*是生成器对象，则返回True。

`isgeneratorfunction(object)`

如果*object*是生成器函数，则返回True。这与`isgenerator()`不同，因为它测试*object*是否是调用时创建生成器的函数。它不用于检查*object*是否是正在运行的生成器。

`ismethod(object)`

如果*object*是方法，则返回True。

`ismethoddescriptor(object)`

如果*object*是方法描述符对象，则返回True。如果*object*不是方法、类或函数，并且它定义了`__get__()`方法但没有定义`__set__()`，则属于这种情况。

`ismodule(object)`

如果*object*是模块对象，则返回True。

`isroutine(object)`

如果*object*是用户定义或内置的函数或方法，则返回True。

`istraceback(object)`

如果*object*是回溯对象，则返回True。

`stack([context])`

返回与调用者堆栈对应的帧记录列表。每个帧记录是一个6元组(`frame, filename, line, funcname, contextlist, index`)，包含与`getinnerframes()`返回的相同信息。*context*指定在每个帧记录中返回的源代码上下文行数。

`trace([context])`

返回当前帧和引发当前异常的帧之间的堆栈的帧记录列表。第一个帧记录是调用者，最后一个帧记录是发生异常的帧。*context*指定在每个帧记录中返回的源代码上下文行数。



##### marshal

marshal 模块用于以一种"未文档化的" Python 专有数据格式序列化 Python 对象。marshal 与 pickle 和 shelve 模块类似，但功能较弱，仅适用于简单对象。通常不应用于实现持久化对象（应改用 pickle）。不过，对于简单的内置类型，marshal 模块是一种非常快速的数据保存和加载方式。

```
dump(value, file [, version])
```

将对象 value 写入已打开的文件对象 file。如果 value 是不支持的类型，将引发 ValueError 异常。version 是一个整数，用于指定使用哪种数据格式。默认输出格式定义在 marshal.version 中，当前设置为 2。版本 0 是早期 Python 版本使用的旧格式。

```
dumps(value [, version])
```

返回 dump() 函数写入的字符串。如果 value 是不支持的类型，将引发 ValueError 异常。version 与前述描述相同。

```
load(file)
```

从已打开的文件对象 file 中读取并返回下一个值。如果没有读取到有效的值，将引发 EOFError、ValueError 或 TypeError 异常。输入数据的格式会自动检测。

```
loads(string)
```

从字符串 string 中读取并返回下一个值。

##### 注意事项

- 数据以与二进制架构无关的格式存储。

- 仅支持 None、整数、长整数、浮点数、复数、字符串、Unicode 字符串、元组、列表、字典和代码对象。列表、元组和字典只能包含受支持的对象。不支持类实例以及列表、元组和字典中的递归引用。

- 如果内置整数类型的精度不够，整数可能会被提升为长整数——例如，当 marshal 数据包含一个 64 位整数，但数据在 32 位机器上读取时。

- marshal 并非旨在防范错误或恶意构造的数据，不应从不受信任的来源反序列化数据。

- marshal 比 pickle 快得多，但灵活性不如 pickle。

##### pickle

pickle 模块用于将 Python 对象序列化为字节流，适合存储到文件中、通过网络传输或存入数据库。这一过程有多种称呼：pickling、serializing、marshalling 或 flattening。生成的字节流也可以通过 unpickling 过程转换回一系列 Python 对象。

以下函数用于将对象转换为字节流。

```
dump(object, file [, protocol ])
```

将 *object* 的 pickle 表示形式转储到文件对象 *file* 中。*protocol* 指定数据的输出格式。协议 0（默认）是一种基于文本的格式，与早期版本的 Python 向后兼容。协议 1 是一种二进制协议，也兼容大多数早期 Python 版本。协议 2 是一种较新的协议，提供了更高效的类和实例 pickle 方式。协议 3 用于 Python 3，不向后兼容。如果 *protocol* 为负数，则会选择最新的协议。变量 `pickle.HIGHEST_PROTOCOL` 包含可用的最高协议。如果 *object* 不支持 pickle，将引发 `pickle.PicklingError` 异常。

```
dumps(object [, protocol])
```

与 `dump()` 相同，但返回一个包含 pickle 数据的字符串。

以下示例展示了如何使用这些函数将对象保存到文件中：

```
f = open('myfile', 'wb')
pickle.dump(x, f)
pickle.dump(y, f)
... dump more objects ...
f.close()
```

以下函数用于恢复 pickle 对象。

```
load(file)
```

从文件对象 *file* 中加载并返回对象的 pickle 表示形式。无需指定输入协议，因为会自动检测。如果文件包含无法解码的损坏数据，将引发 `pickle.UnpicklingError` 异常。如果检测到文件末尾，将引发 `EOFError` 异常。

```
loads(string)
```

与 `load()` 相同，但从字符串中读取对象的 pickle 表示形式。

以下示例展示了如何使用这些函数加载数据：

```
f = open('myfile', 'rb')
x = pickle.load(f)
y = pickle.load(f)
... load more objects ...
f.close()
```

如果你要 pickle 多个 Python 对象，只需像前面示例所示那样重复调用 `dump()` 和 `load()` 即可。多次调用时，只需确保 `load()` 调用的顺序与写入文件时 `dump()` 调用的顺序一致。

当处理包含循环引用或共享引用的复杂数据结构时，使用 `dump()` 和 `load()` 可能会出现问题，因为它们不会维护关于已 pickle 或恢复对象的内部状态。这可能导致输出文件过大，并且在加载时无法正确恢复对象之间的关系。一种替代方法是使用 `Pickler` 和 `Unpickler` 对象。

```
Pickler(file [, protocol ])
```

创建一个 pickle 对象，将数据写入文件对象 `file`，使用指定的 pickle *protocol*。`Pickler` 的实例 `p` 有一个方法 `p.dump(x)`，用于将对象 `x` 转储到 *file* 中。一旦 `x` 被转储，其身份会被记住。如果后续的 `p.dump()` 操作写入相同的对象，则会保存对先前转储对象的引用，而不是写入新的副本。方法 `p.clear_memo()` 会清除用于跟踪先前转储对象的内部字典。如果你想写入先前转储对象的新副本（即，如果其自上次 `dump()` 操作以来值发生了变化），可以使用此方法。

```
Unpickler(file)
```

创建一个 unpickle 对象，从文件对象 *file* 中读取数据。`Unpickler` 的实例 `u` 有一个方法 `u.load()`，用于从 *file* 中加载并返回新对象。`Unpickler` 会跟踪它已返回的对象，因为输入源可能包含由 `Pickler` 对象创建的对象引用。在这种情况下，`u.load()` 会返回对先前加载对象的引用。

`pickle` 模块适用于大多数常见的 Python 对象，包括：

- None
- 数字和字符串
- 仅包含可 pickle 对象的元组、列表和字典
- 在模块顶层定义的用户定义类的实例

当用户定义类的实例被 pickle 时，只有实例数据会被 pickle。对应的类定义不会被保存——相反，pickle 数据仅包含关联类和模块的*名称*。当实例被 unpickle 时，会自动导入定义该类的模块，以便在重新创建实例时访问类定义。还应注意的是，在恢复实例时，不会调用类的 `__init__()` 方法。相反，实例通过其他方式重新创建，并恢复实例数据。

对实例的一个限制是，对应的类定义必须出现在模块的顶层（即，不允许嵌套类）。此外，如果实例的类定义最初是在 `__main__` 中定义的，则在 unpickle 保存的对象之前必须手动重新加载该类定义（因为解释器无法自动将必要的类定义重新加载到 `__main__` 中）。

通常不需要做任何事情来使用户定义的类与 pickle 协作。但是，类可以通过实现特殊方法 `__getstate__()` 和 `__setstate__()` 来定义自定义的保存和恢复状态的方法。`__getstate__()` 方法必须返回一个可 pickle 的对象（如字符串或元组），表示对象的状态。`__setstate__()` 方法接受 pickle 对象并恢复其状态。如果未定义这些方法，默认行为是 pickle 实例的底层 `__dict__` 属性。应注意的是，如果定义了这些方法，它们也会被 copy 模块用于实现浅拷贝和深拷贝操作。



###### 备注

-   在 Python 2 中，一个名为 `cPickle` 的模块包含了 `pickle` 模块函数的 C 语言实现。它比 `pickle` 快得多，但有一个限制，即不允许对 `Pickler` 和 `Unpickler` 对象进行子类化。Python 3 也有一个包含 C 实现的支持模块，但它的使用更加透明（`pickle` 会在适当时自动利用它）。

-   `pickle` 使用的数据格式是 Python 特有的，不应假设它与任何外部标准（如 XML）兼容。

-   只要可能，就应该使用 `pickle` 模块而不是 `marshal` 模块，因为 `pickle` 更灵活，其数据编码有文档说明，并且执行了额外的错误检查。

-   由于安全考虑，程序不应反序列化来自不可信来源的数据。

-   在扩展模块中定义的类型使用 `pickle` 模块比这里描述的要复杂得多。扩展类型的实现者应该查阅在线文档，了解使这些对象与 `pickle` 协同工作所需的底层协议的详细信息——特别是关于如何实现 `pickle` 用于创建序列化字节序列的 `__reduce__()` 和 `__reduce_ex__()` 特殊方法的细节。

##### sys

`sys` 模块包含与解释器及其环境操作相关的变量和函数。

###### 变量

定义了以下变量。

**api_version**

一个整数，表示 Python 解释器的 C API 版本。在扩展模块中使用时会用到。

**argv**

传递给程序的命令行选项列表。`argv[0]` 是程序的名称。

**builtin_module_names**

一个元组，包含内置于 Python 可执行文件中的模块名称。

**byteorder**

机器的原生字节序——`'little'` 表示小端序，`'big'` 表示大端序。

**copyright**

包含版权信息的字符串。

**__displayhook__**

`displayhook()` 函数的原始值。

**dont_write_bytecode**

一个布尔标志，决定 Python 在导入模块时是否写入字节码（`.pyc` 或 `.pyo` 文件）。初始值为 `True`，除非指定了解释器的 `-B` 选项。可以在自己的程序中根据需要更改此设置。

**dllhandle**

Python DLL（Windows）的整数句柄。

**__excepthook__**

`excepthook()` 函数的原始值。

**exec_prefix**

安装平台相关 Python 文件的目录。

**executable**

包含解释器可执行文件名称的字符串。

**flags**

一个对象，表示传递给 Python 解释器本身的不同命令行选项的设置。下表列出了 `flags` 的属性以及启用该标志的相应命令行选项。这些属性是只读的。

| 属性 | 命令行选项 |
| --- | --- |
| `flags.debug` | `-d` |
| `flags.py3k_warning` | `-3` |
| `flags.division_warning` | `-Q` |
| `flags.division_new` | `-Qnew` |
| `flags.inspect` | `-i` |
| `flags.interactive` | `-i` |
| `flags.optimize` | `-O` 或 `-OO` |
| `flags.dont_write_bytecode` | `-B` |
| `flags.no_site` | `-S` |
| `flags.ignore_environment` | `-E` |
| `flags.tabcheck` | `-t` 或 `-tt` |
| `flags.verbose` | `-v` |
| `flags.unicode` | `-U` |

####### float_info

一个对象，保存关于浮点数内部表示的信息。这些属性的值取自 C 头文件 `float.h`。

| 属性 | 描述 |
| --- | --- |
| `float_info.epsilon` | 1.0 与下一个最大浮点数之间的差值。 |
| `float_info.dig` | 可以表示而不丢失精度的十进制位数。 |
| `float_info.mant_dig` | 使用 `float_info.radix` 指定的数值基数可以表示的位数。 |
| `float_info.max` | 最大浮点数。 |
| `float_info.max_exp` | 使用 `float_info.radix` 指定的数值基数的最大指数。 |
| `float_info.max_10_exp` | 以 10 为基数的最大指数。 |
| `float_info.min` | 最小的正浮点值。 |
| `float_info.min_exp` | 使用 `float_info.radix` 指定的数值基数的最小指数。 |
| `float_info.min_10_exp` | 以 10 为基数的最小指数。 |
| `float_info.radix` | 用于指数的数值基数。 |
| `float_info.rounds` | 舍入行为（-1 不确定，0 向零舍入，1 向最近舍入，2 向正无穷舍入，3 向负无穷舍入）。 |

####### hexversion

一个整数，其十六进制表示编码了 `sys.version_info` 中包含的版本信息。此整数的值始终保证随着解释器新版本的发布而增加。

####### last_type, last_value, last_traceback

当遇到未处理的异常且解释器打印错误消息时，会设置这些变量。`last_type` 是最后一个异常类型，`last_value` 是最后一个异常值，`last_traceback` 是堆栈跟踪。请注意，这些变量的使用不是线程安全的。应使用 `sys.exc_info()` 代替。

####### maxint

整数类型支持的最大整数（仅限 Python 2）。

####### maxsize

系统上 C `size_t` 数据类型支持的最大整数值。此值决定了字符串、列表、字典和其他内置类型的最大可能长度。

####### maxunicode

一个整数，表示可以表示的最大 Unicode 码位。对于 16 位 UCS-2 编码，默认值为 65535。如果 Python 配置为使用 UCS-4，则会找到更大的值。

####### modules

一个字典，将模块名称映射到模块对象。

**path**

一个字符串列表，指定模块的搜索路径。第一个条目始终设置为用于启动 Python 的脚本所在的目录（如果可用）。请参阅第 8 章“迭代器和生成器”。

**platform**

平台标识符字符串，例如 `'linux-i386'`。

**prefix**

安装平台无关 Python 文件的目录。

**ps1, ps2**

包含解释器主要和次要提示符文本的字符串。最初，`ps1` 设置为 `'>>> '`，`ps2` 设置为 `'... '`。将分配给这些值的任何对象的 `str()` 方法会被求值以生成提示文本。

**py3kwarning**

在 Python 2 中，当解释器使用 `-3` 选项运行时，此标志设置为 `True`。

**stdin, stdout, stderr**

与标准输入、标准输出和标准错误对应的文件对象。`stdin` 用于 `raw_input()` 和 `input()` 函数。`stdout` 用于 `print` 以及 `raw_input()` 和 `input()` 的提示符。`stderr` 用于解释器的提示符和错误消息。这些变量可以赋值给任何支持对单个字符串参数进行 `write()` 操作的对象。

**__stdin__, __stdout__, __stderr__**

包含解释器启动时 `stdin`、`stdout` 和 `stderr` 值的文件对象。

**tracebacklimit**

发生未处理异常时打印的堆栈跟踪信息的最大层级数。默认值为 1000。值为 0 会抑制所有堆栈跟踪信息，只打印异常类型和值。

**version**

版本字符串。

**version_info**

以元组 `(major, minor, micro, releaselevel, serial)` 表示的版本信息。所有值都是整数，除了 `releaselevel`，它是字符串 `'alpha'`、`'beta'`、`'candidate'` 或 `'final'`。

**warnoptions**

通过 `-W` 命令行选项传递给解释器的警告选项列表。

**winver**

用于在 Windows 上形成注册表项的版本号。

##### 函数

以下是可用的函数：

```
_clear_type_cache()
```

清除内部类型缓存。为了优化方法查找，解释器内部维护了一个最近使用方法的 1024 条目的小缓存。此缓存可加速重复的方法查找——尤其是在具有深层继承层次结构的代码中。通常，你不需要清除此缓存，但如果你正在尝试追踪一个非常棘手的内存引用计数问题，可能会这样做。例如，如果缓存中的方法持有一个你期望被销毁的对象的引用。

```
_current_frames()
```

返回一个字典，将线程标识符映射到调用时正在执行的线程的最顶层堆栈帧。此信息在编写与线程调试相关的工具（即追踪死锁）时很有用。请记住，此函数返回的值仅代表调用时解释器状态的快照。在你查看返回的数据时，线程可能已经在其他地方执行了。

```
displayhook([value])
```

当解释器在交互模式下运行时，此函数被调用以打印表达式的结果。默认情况下，`repr(value)` 的值被打印到标准输出，并将 `value` 保存在变量 `__builtin__._` 中。如果需要，可以重新定义 `displayhook` 以提供不同的行为。

```
excepthook(type, value, traceback)
```

当发生未捕获的异常时调用此函数。`type` 是异常类，`value` 是 `raise` 语句提供的值，`traceback` 是一个回溯对象。默认行为是将异常和回溯打印到标准错误。但是，可以重新定义此函数以提供未捕获异常的替代处理（这在调试器或 CGI 脚本等专用应用程序中可能很有用）。

```
exc_clear()
```

清除与上次发生异常相关的所有信息。它只清除特定于调用线程的信息。

```
exc_info()
```

返回一个元组 `(type, value, traceback)`，包含有关当前正在处理的异常的信息。`type` 是异常类型，`value` 是传递给 `raise` 的异常参数，`traceback` 是一个回溯对象，包含异常发生时的调用栈。如果没有正在处理的异常，则返回 `None`。

```
exit([n])
```

通过引发 `SystemExit` 异常退出 Python。`n` 是一个整数退出码，表示状态码。值 0 被视为正常（默认值）；非零值被视为异常。如果给 `n` 一个非整数值，它将被打印到 `sys.stderr`，并使用退出码 1。



####### getcheckinterval()

返回检查间隔的值，该值指定解释器检查信号、线程切换和其他周期性事件的频率。

####### getdefaultencoding()

获取Unicode转换中的默认字符串编码。返回诸如`ascii`或`utf-8`之类的值。默认编码由`site`模块设置。

####### getdlopenflags()

返回在UNIX上加载扩展模块时传递给C函数`dlopen()`的标志参数。参见`dl`模块。

####### getfilesystemencoding()

返回将Unicode文件名映射到底层操作系统所使用的文件名时所用的字符编码。在Windows上返回'mbcs'，在Macintosh OS X上返回'utf-8'。在UNIX系统上，编码取决于区域设置，并将返回区域设置`CODESET`参数的值。可能返回None，此时将使用系统默认编码。

####### _getframe([*depth*])

从调用栈返回一个帧对象。如果省略*depth*或为零，则返回最顶层的帧。否则，返回当前帧下方指定调用深度处的帧。例如，`_getframe(1)`返回调用者的帧。如果*depth*无效，则引发`ValueError`。

####### getprofile()

返回由`setprofile()`函数设置的性能分析函数。

####### getrecursionlimit()

返回函数的递归限制。

####### getrefcount(*object*)

返回*object*的引用计数。

####### getsizeof(*object* [, *default*])

返回*object*的大小（以字节为单位）。此计算通过调用*object*的`__sizeof__()`特殊方法完成。如果未定义，除非已使用*default*参数指定了默认值，否则将生成`TypeError`。因为对象可以自由定义其`__sizeof__()`方法，所以无法保证此函数的结果是内存使用的真实度量。但是，对于列表或字符串等内置类型，它是正确的。

####### gettrace()

返回由`settrace()`函数设置的跟踪函数。

####### getwindowsversion()

返回一个描述所用Windows版本的元组（*major*, *minor*, *build*, *platform*, *text*）。*major*是主版本号。例如，值4表示Windows NT 4.0，值5表示Windows 2000和Windows XP变体。`minor`是次版本号。例如，0表示Windows 2000，而1表示Windows XP。`build`是Windows内部版本号。`platform`标识平台，是一个具有以下常用值的整数：0（Windows 3.1上的Win32s）、1（Windows 95、98或Me）、2（Windows NT、2000、XP）或3（Windows CE）。`text`是包含其他信息的字符串，例如`"Service Pack 3"`。

```
setcheckinterval(n)
```

设置解释器在检查信号和线程上下文切换等周期性事件之前必须执行的Python虚拟机指令数。默认值为10。

```
setdefaultencoding(enc)
```

设置默认编码。`enc`是一个字符串，例如`'ascii'`或`'utf-8'`。此函数仅在`site`模块内部定义。可以从用户可定义的`sitecustomize`模块中调用它。

```
setdlopenflags(flags)
```

设置传递给C `dlopen()`函数的标志，该函数用于在UNIX上加载扩展模块。这将影响库和其他扩展模块之间符号解析的方式。`flags`是`dl`模块中可找到值的按位或（例如，`sys.setdlopenflags(dl.RTLD_NOW | dl.RTLD_GLOBAL)`）。

```
setprofile(pfunc)
```

设置可用于实现源代码性能分析器的系统性能分析函数。

```
setrecursionlimit(n)
```

更改函数的递归限制。默认值为1000。请注意，操作系统可能会对栈大小施加硬限制，因此设置得过高可能会导致Python解释器进程因段错误或访问违规而崩溃。

```
settrace(tfunc)
```

设置系统跟踪函数，该函数可用于实现调试器。有关Python调试器的信息，请参阅第11章。

###### traceback

`traceback`模块用于在异常发生后收集和打印程序的堆栈跟踪。此模块中的函数对跟踪对象进行操作，例如`sys.exc_info()`函数返回的第三项。此模块的主要用途是在需要以非标准方式报告错误的代码中——例如，如果您正在网络服务器中深度嵌入的Python程序中运行，并且希望将堆栈跟踪重定向到日志文件。

```
print_tb(traceback [, limit [, file]])
```

从`traceback`打印最多`limit`个堆栈跟踪条目到文件`file`。如果省略`limit`，则打印所有条目。如果省略`file`，则输出发送到`sys.stderr`。

####### print_exception(type, value, traceback [, limit [, file]])

将异常信息和堆栈跟踪打印到*file*。`type`是异常类型，`value`是异常值。`limit`和`file`与`print_tb()`中的相同。

####### print_exc([limit [, file]])

与应用于`sys.exc_info()`函数返回信息的`print_exception()`相同。

####### format_exc([limit [, file]])

返回一个字符串，其中包含与`print_exc()`打印的信息相同的信息。

####### print_last([limit [, file]])

与`print_exception(sys.last_type, sys.last_value, sys.last_traceback, limit, file)`相同。

####### print_stack([frame [, limit [, file]]])

从调用点打印堆栈跟踪。`frame`指定一个可选的起始栈帧。`limit`和`file`与`print_tb()`中的含义相同。

####### extract_tb(traceback [, limit])

提取`print_tb()`使用的堆栈跟踪信息。返回值是元组列表，形式为`(filename, line, funcname, text)`，包含通常出现在堆栈跟踪中的相同信息。`limit`是要返回的条目数。

####### extract_stack([frame [, limit]])

提取与`print_stack()`使用的相同堆栈跟踪信息，但从栈帧`frame`获取。如果省略`frame`，则使用调用者的当前栈帧，`limit`是要返回的条目数。

####### format_list(list)

格式化堆栈跟踪信息以便打印。`list`是`extract_tb()`或`extract_stack()`返回的元组列表。

####### format_exception_only(type, value)

格式化异常信息以便打印。

####### format_exception(type, value, traceback [, limit])

格式化异常和堆栈跟踪以便打印。

####### format_tb(traceback [, limit])

与`format_list(extract_tb(traceback, limit))`相同。

####### format_stack([frame [, limit]])

与`format_list(extract_stack(frame, limit))`相同。

####### tb_lineno(traceback)

返回跟踪对象中设置的行号。

##### types

types模块为与函数、模块、生成器、栈帧和其他程序元素相对应的内置类型定义了名称。此模块的内容通常与内置isinstance()函数和其他与类型相关的操作结合使用。

| 变量 | 描述 |
| --- | --- |
| BuiltinFunctionType | 内置函数的类型 |
| CodeType | 代码对象的类型 |
| FrameType | 执行帧对象的类型 |
| FunctionType | 用户定义函数和lambda的类型 |
| GeneratorType | 生成器迭代器对象的类型 |
| GetSetDescriptorType | GetSet描述符对象的类型 |
| LambdaType | FunctionType的替代名称 |
| MemberDescriptorType | 成员描述符对象的类型 |
| MethodType | 用户定义类方法的类型 |
| ModuleType | 模块的类型 |
| TracebackType | 跟踪对象的类型 |

大多数前面的类型对象用作可用于创建该类型对象的构造函数。以下描述提供了用于创建函数、模块、代码对象和方法的参数。第3章包含了有关所创建对象的属性以及需要向下面描述的函数提供的参数的详细信息。

```
FunctionType(code, globals [, name [, defarags [, closure]]])
```

创建一个新的函数对象。

```
CodeType(argcount, nlocals, stacksize, flags, codestring, constants, names,
varnames, filename, name, firstlineno, lnotab [, freevars [, cellvars ]])
```

创建一个新的代码对象。

```
MethodType(function, instance, class)
```

创建一个新的绑定实例方法。

```
ModuleType(name [, doc])
```

创建一个新的模块对象。

##### 注意事项

- 不应使用types模块来引用整数、列表或字典等内置对象的类型。在Python 2中，types包含其他名称，如IntType和DictType。但是，这些名称只是内置类型名称int和dict的别名。在现代代码中，您应该直接使用内置类型名称，因为在Python 3中，types模块仅包含前面列出的名称。



OCR 文本整体较为清晰，仅在末尾有一处明显错误。以下是校正并格式化后的输出：

---

##### warnings

`warnings` 模块提供了发布和过滤警告消息的函数。与异常不同，警告旨在提醒用户潜在的问题，但不会生成异常或导致执行停止。`warnings` 模块的一个主要用途是通知用户某些语言特性可能在未来版本的 Python 中不再支持。例如：

```
>>> import regex
__main__:1: DeprecationWarning: the regex module is deprecated;  use the re module
>>>
```

与异常类似，警告也组织成一个描述通用警告类别的类层次结构。以下列出了当前支持的类别：

| 警告对象           | 描述                                                     |
|-------------------|----------------------------------------------------------|
| Warning           | 所有警告类型的基类                                        |
| UserWarning       | 用户定义的警告                                            |
| DeprecationWarning| 使用已弃用特性的警告                                      |
| SyntaxWarning     | 潜在的语法问题                                            |
| RuntimeWarning    | 潜在的运行时问题                                          |
| FutureWarning     | 特定特性在将来版本中语义将发生变化的警告                  |

这些类中的每一个都可以在 `__builtin__` 模块以及 `exceptions` 模块中找到。此外，它们也是 `Exception` 的实例。这使得可以轻松地将警告转换为错误。

警告使用 `warn()` 函数发布。例如：

```
warnings.warn("feature X is deprecated.")
warnings.warn("feature Y might be broken.", RuntimeWarning)
```

如果需要，可以对警告进行过滤。过滤过程可用于改变警告消息的输出行为、忽略警告或将警告转换为异常。`filterwarnings()` 函数用于为特定类型的警告添加过滤器。例如：

```
warnings.filterwarnings(action="ignore",
                        message=".*regex.*",
                        category=DeprecationWarning)
import regex     # Warning message disappears
```

有限形式的过滤也可以通过解释器的 `-W` 选项指定。例如：

```
% python -Wignore:the\ regex:DeprecationWarning
```

`warnings` 模块中定义了以下函数：

```
warn(message[, category[, stacklevel]])
```

发布一个警告。`message` 是一个包含警告消息的字符串，`category` 是警告类（如 `DeprecationWarning`），`stacklevel` 是一个整数，指定警告消息应源自的堆栈帧。默认情况下，`category` 是 `UserWarning`，`stacklevel` 是 1。

```
warn_explicit(message, category, filename, lineno[, module[, registry]])
```

这是 `warn()` 函数的低级版本。`message` 和 `category` 的含义与 `warn()` 相同。`filename`、`lineno` 和 `module` 明确指定警告的位置。`registry` 是一个表示所有当前活动过滤器的对象。如果省略 `registry`，警告消息将不会被抑制。

```
showwarning(message, category, filename, lineno[, file])
```

将警告写入文件。如果省略 `file`，警告将打印到 `sys.stderr`。

```
formatwarning(message, category, filename, lineno)
```

创建发布警告时打印的格式化字符串。

```
filterwarnings(action[, message[, category[, module[, lineno[, append]]]]])
```

向警告过滤器列表添加一个条目。`action` 是以下之一：`'error'`、`'ignore'`、`'always'`、`'default'`、`'once'` 或 `'module'`。以下列表提供了每个操作的说明：

| 操作        | 描述                                                     |
|------------|----------------------------------------------------------|
| 'error'    | 将警告转换为异常                                          |
| 'ignore'   | 忽略警告                                                  |
| 'always'   | 始终打印警告消息                                          |
| 'default'  | 对每个发生警告的位置打印一次警告                          |
| 'module'   | 对每个发生警告的模块打印一次警告                          |
| 'once'     | 无论警告在哪里发生，仅打印一次警告                        |

`message` 是一个正则表达式字符串，用于与警告消息匹配。`category` 是一个警告类，例如 `DeprecationError`。`module` 是一个正则表达式字符串，与模块名匹配。`lineno` 是一个特定的行号，或 0 表示匹配所有行。`append` 指定过滤器应追加到所有过滤器列表的末尾（最后检查）。默认情况下，新过滤器会添加到过滤器列表的开头。如果省略任何参数，它将默认为匹配所有警告的值。

```
resetwarnings()
```

重置所有警告过滤器。这会丢弃所有先前对 `filterwarnings()` 的调用以及通过 `-W` 指定的选项。

###### Notes

- 当前活动过滤器的列表可在 `warnings.filters` 变量中找到。
- 当警告转换为异常时，警告类别成为异常类型。例如，`DeprecationWarning` 上的错误将引发 `DeprecationWarning` 异常。
- `-W` 选项可用于在命令行上指定警告过滤器。此选项的一般格式为

  ```
  -Waction:message:category:module:lineno
  ```

  其中每个部分的含义与 `filterwarnings()` 函数相同。但是，在这种情况下，`message` 和 `module` 字段分别指定要过滤的警告消息和模块名的子字符串（而不是正则表达式）。

##### weakref

`weakref` 模块用于提供对弱引用的支持。通常，对对象的引用会导致其引用计数增加——实际上使对象保持存活，直到引用消失。另一方面，弱引用提供了一种在不增加对象引用计数的情况下引用对象的方法。这在必须以不寻常方式管理对象的某些类型的应用程序中可能很有用。例如，在面向对象的程序中，你可能实现诸如观察者模式的关系，弱引用可用于避免创建引用循环。第 7 章的“对象内存管理”部分显示了一个示例。

使用 `weakref.ref()` 函数创建弱引用，如下所示：

```
>>> class A: pass
>>> a = A()
>>> ar = weakref.ref(a)    # Create a weak reference to a
>>> print ar
<weakref at 0x135a24; to 'instance' at 0x12ce0c>
```

一旦创建了弱引用，就可以通过像调用无参数函数一样简单地调用弱引用来获取原始对象。如果底层对象仍然存在，它将被返回。否则，返回 `None` 以指示原始对象不再存在。例如：

```
>>> print ar()             # Print original object
<__main__.A instance at 12ce0c>
>>> del a                  # Delete the original object
>>> print ar()             # a is gone, so this now returns None
None
>>>
```

`weakref` 模块定义了以下函数：

```
ref(object[, callback])
```

创建对 `object` 的弱引用。`callback` 是一个可选函数，当 `object` 即将被销毁时将被调用。如果提供，此函数应接受一个参数，即相应的弱引用对象。多个弱引用可能引用同一个对象。在这种情况下，回调函数将按照从最近应用的引用到最旧的引用的顺序被调用。可以通过将返回的弱引用对象作为无参数函数调用来从弱引用获取 `object`。如果原始对象不再存在，将返回 `None`。`ref()` 实际上定义了一个类型 `ReferenceType`，可用于类型检查和子类化。

```
proxy(object[, callback])
```

使用对 `object` 的弱引用创建一个代理。返回的代理对象实际上是原始对象的包装器，提供对其属性和方法的访问。只要原始对象存在，对代理对象的操作将透明地模拟底层对象的行为。另一方面，如果原始对象已被销毁，对代理的操作将引发 `weakref.ReferenceError` 以指示该对象不再存在。`callback` 是与 `ref()` 函数含义相同的回调函数。代理对象的类型是 `ProxyType` 或 `CallableProxyType`，取决于原始对象是否可调用。

```
getweakrefcount(object)
```

返回引用 `object` 的弱引用和代理的数量。

```
getweakrefs(object)
```

返回所有引用 `object` 的弱引用和代理对象的列表。

```
WeakKeyDictionary([dict])
```

创建一个字典，其中键被弱引用。当对某个键没有更多强引用时，字典中对应的条目将自动移除。如果提供，`dict` 中的项最初会被添加到返回的 `WeakKeyDictionary` 对象中。因为只有某些类型的对象可以被弱引用，所以对可接受的键值有许多限制。特别地，内置字符串不能用作弱键。但是，定义了 `__hash__()` 方法的用户定义类的实例可以用作键。`WeakKeyDictionary` 的实例有两个方法 `iterkeyrefs()` 和 `keyrefs()`，它们返回弱键引用。

```
WeakValueDictionary([dict])
```

创建一个字典，其中值被弱引用。当对某个值没有更多强引用时，字典中对应的条目将被丢弃。如果提供，`dict` 中的条目将被添加到返回的 `WeakValueDictionary` 中。`WeakValueDictionary` 的实例有两个方法 `itervaluerefs()` 和 `valuerefs()`，它们返回弱值引用。

```
ProxyTypes
```

这是一个元组 `(ProxyType, CallableProxyType)`，可用于测试一个对象是否是 `proxy()` 函数创建的两种代理对象之一——例如 `isinstance(object, ProxyTypes)`。



##### 示例

弱引用的一个应用是创建最近计算结果的缓存。例如，如果一个函数需要很长时间来计算结果，那么将这些结果缓存并在它们仍被应用程序其他地方使用时重复利用是很有意义的。例如：

```
_resultcache = { }
def foocache(x):
    if _resultcache.has_key(x):
        r = _resultcache[x]()     # Get weak ref and dereference it
        if r is not None: return r
    r = foo(x)
    _resultcache[x] = weakref.ref(r)
    return r
```

##### 注意事项

-   只有类实例、函数、方法、集合、冻结集合、文件、生成器、类型对象以及库模块中定义的某些对象类型（例如，套接字、数组和正则表达式模式）支持弱引用。内置函数和大多数内置类型（如列表、字典、字符串和数字）不能使用。

-   如果对 `WeakKeyDictionary` 或 `WeakValueDictionary` 进行迭代，必须格外小心，确保字典的大小不会发生变化，因为这可能导致奇怪的副作用，例如项目毫无明显原因地从字典中神秘消失。

-   如果在执行使用 `ref()` 或 `proxy()` 注册的回调期间发生异常，该异常将被打印到标准错误并被忽略。

-   只要原始对象是可哈希的，弱引用就是可哈希的。此外，弱引用在原始对象被删除后将保持其哈希值，前提是原始哈希值是在对象仍存在时计算的。

-   弱引用可以测试相等性，但不能测试排序。如果对象仍然存活，则当底层对象具有相同的值时，引用相等。否则，如果引用是同一个引用，则引用相等。

### 14 数学

本章描述用于执行各种数学运算的模块。此外，还介绍了为十进制浮点数提供通用支持的 `decimal` 模块。

#### decimal

Python `float` 数据类型使用双精度二进制浮点编码表示（通常由 IEEE 754 标准定义）。这种编码的一个微妙后果是，十进制值（如 0.1）无法精确表示。相反，最接近的值是 0.10000000000000001。这种不精确性会传递到涉及浮点数的计算中，有时会导致意想不到的结果（例如，`3*0.1 == 0.3` 的计算结果为 `False`）。

`decimal` 模块提供了 IBM 通用十进制算术标准的实现，允许精确表示十进制数。它还提供了对数学精度、有效数字和舍入行为的精确控制。如果与精确定义十进制数字属性的外部系统交互，这些特性会很有用。例如，如果编写必须与业务应用程序交互的 Python 程序。

`decimal` 模块定义了两个基本数据类型：一个表示十进制数的 `Decimal` 类型，以及一个表示计算相关各种参数（如精度和舍入错误处理）的 `Context` 类型。以下是一些简单的示例，说明了模块工作原理的基础：

```
import decimal
x = decimal.Decimal('3.4')    # Create some decimal numbers
y = decimal.Decimal('4.5')

##### Perform some math calculations using the default context
a = x * y       # a = decimal.Decimal('15.30')
b = x / y       # b = decimal.Decimal('0.7555555555555555555555555556')

##### Change the precision and perform calculations
decimal.getcontext().prec = 3
c = x * y       # c = decimal.Decimal('15.3')
d = x / y       # d = decimal.Decimal('0.756')

##### Change the precision for just a single block of statements
with decimal.localcontext(decimal.Context(prec=10)):
    e = x * y   # e = decimal.Decimal('15.30')
    f = x / y   # f = decimal.Decimal('0.7555555556')
```

###### Decimal 对象

十进制数由以下类表示：

**Decimal([value [, context]])**

value 是数字的值，可以指定为整数、包含十进制值的字符串（例如 `'4.5'`）或元组 `(sign, digits, exponent)`。如果提供元组，sign 对于正数为 0，负数为 1；digits 是指定为整数的数字元组；exponent 是整数指数。特殊字符串 `'Infinity'`、`'-Infinity'`、`'NaN'` 和 `'sNaN'` 可用于指定正负无穷大以及非数字（NaN）。`'sNaN'` 是 NaN 的一个变体，如果随后在计算中使用，将引发异常。普通的 `float` 对象*不能*用作初始值，因为该值可能不精确（这违背了使用 decimal 的初衷）。context 参数是一个 Context 对象，将在后面描述。如果提供，context 将决定如果初始值不是有效数字时会发生什么——是引发异常还是返回一个值为 NaN 的十进制数。

以下示例展示了如何创建各种十进制数：

```
a = decimal.Decimal(42)               # Creates Decimal("42")
b = decimal.Decimal("37.45")          # Creates Decimal("37.45")
c = decimal.Decimal((1,(2,3,4,5),-2)) # Creates Decimal("-23.45")
d = decimal.Decimal("Infinity")
e = decimal.Decimal("NaN")
```

Decimal 对象是不可变的，并具有内置 `int` 和 `float` 类型的所有通常的数值属性。它们也可以用作字典键、放入集合中、排序等。在大多数情况下，你使用标准的 Python 数学运算符来操作 `Decimal` 对象。但是，可以使用下表中的方法执行几种常见的数学运算。所有操作都接受一个可选的 context 参数，用于控制计算的精度、舍入和其他方面的行为。如果省略，则使用当前上下文。

| 方法 | 描述 |
|--------|-------------|
| x.exp([context]) | 自然指数 e**x |
| x.fma(y, z [, context]) | x*y + z，其中 x*y 部分不进行舍入 |
| x.ln([context]) | x 的自然对数（以 e 为底） |
| x.log10([context]) | x 的以 10 为底的对数 |
| x.sqrt([context]) | x 的平方根 |

###### Context 对象

十进制数的各种属性（如舍入和精度）通过使用 Context 对象来控制：

```
Context(prec=None, rounding=None, traps=None, flags=None,
        Emin=None, Emax=None, capitals=1)
```

这将创建一个新的十进制上下文。参数应使用关键字参数指定，名称如所示。prec 是一个整数，用于设置算术运算的精度位数，rounding 决定舍入行为，traps 是一个信号列表，当计算过程中发生某些事件（如除以零）时会产生 Python 异常。flags 是一个信号列表，用于指示上下文的初始状态（例如溢出）。通常，不指定 flags。Emin 和 Emax 是整数，分别表示指数的最小和最大范围。capitals 是一个布尔标志，指示指数使用 'E' 还是 'e'。默认值为 1（'E'）。

通常，不直接创建新的 Context 对象。而是使用函数 getcontext() 或 localcontext() 返回当前活动的 Context 对象。然后根据需要修改该对象。本节后面将出现此示例。但是，为了更好地理解这些示例，有必要更详细地解释这些上下文参数。

舍入行为通过将 rounding 参数设置为以下值之一来确定：

| 常量 | 描述 |
|----------|-------------|
| ROUND_CEILING | 向正无穷方向舍入。例如，2.52 向上舍入为 2.6，-2.58 向上舍入为 -2.5。 |
| ROUND_DOWN | 向零方向舍入。例如，2.58 向下舍入为 2.5，-2.58 向上舍入为 -2.5。 |
| ROUND_FLOOR | 向负无穷方向舍入。例如，2.58 向下舍入为 2.5，-2.52 向下舍入为 -2.6。 |
| ROUND_HALF_DOWN | 如果小数部分大于一半，则远离零舍入；否则，向零舍入。例如，2.58 向上舍入为 2.6，2.55 向下舍入为 2.5，-2.55 向上舍入为 -2.5，-2.58 向下舍入为 -2.6。 |
| ROUND_HALF_EVEN | 与 ROUND_HALF_DOWN 相同，但如果小数部分恰好是一半，则如果前一位数字是偶数，则向下舍入；如果是奇数，则向上舍入。例如，2.65 向下舍入为 2.6，2.55 向上舍入为 2.6。 |
| ROUND_HALF_UP | 与 ROUND_HALF_DOWN 相同，但如果小数部分恰好是一半，则远离零舍入。例如，2.55 向上舍入为 2.6，-2.55 向下舍入为 -2.6。 |
| ROUND_UP | 远离零舍入。例如，2.52 向上舍入为 2.6，-2.52 向下舍入为 -2.6。 |
| ROUND_05UP | 如果向零舍入后保留的最后一位数字是 0 或 5，则远离零舍入。否则，向零舍入。例如，2.54 舍入为 2.6，2.64 舍入为 2.6。 |

Context() 的 traps 和 flags 参数是信号列表。信号表示计算过程中可能发生的算术异常类型。除非列在 traps 中，否则信号将被忽略。否则，将引发异常。定义了以下信号：



##### 信号

| 信号 | 描述 |
| --- | --- |
| Clamped | 指数被调整以适应允许范围。 |
| DivisionByZero | 非无限数除以 0。 |
| Inexact | 发生了舍入误差。 |
| InvalidOperation | 执行了无效操作。 |
| Overflow | 舍入后指数超过 Emax。同时生成 Inexact 和 Rounded 信号。 |
| Rounded | 发生了舍入。即使信息没有丢失也可能发生（例如，“1.00”舍入为“1.0”）。 |
| Subnormal | 舍入前指数小于 Emin。 |
| Underflow | 数值下溢。结果舍入为 0。同时生成 Inexact 和 Subnormal 信号。 |

这些信号名称对应于可用于错误检查的 Python 异常。下面是一个示例：

```
try:
    x = a/b
except decimal.DivisionByZero:
    print "Division by zero"
```

与异常一样，信号被组织成一个层次结构：

```
ArithmeticError（内置异常）
    DecimalException
        Clamped
        DivisionByZero
    Inexact
        Overflow
        Underflow
    InvalidOperation
    Rounded
        Overflow
        Underflow
    Subnormal
        Underflow
```

Overflow 和 Underflow 信号在表中出现多次，因为这些信号也会导致父信号（例如，Underflow 也会触发 Subnormal 信号）。decimal.DivisionByZero 信号也派生自内置的 DivisionByZero 异常。

在许多情况下，算术信号会被静默忽略。例如，计算可能产生舍入误差但不引发异常。在这种情况下，可以使用信号名称来检查一组表示计算状态的粘滞标志。下面是一个示例：

```
ctxt = decimal.getcontext()   # 获取当前上下文
x = a + b
if ctxt.flags[Rounded]:
    print "Result was rounded!"
```

当标志被设置后，它们会保持设置状态，直到使用 `clear_flags()` 方法清除它们。因此，可以执行一整串计算，只在最后检查错误。

现有 `Context` 对象 *c* 的设置可以通过以下属性和方法更改：

- `c.capitals` — 标志设置为 1 或 0，用于确定是使用 *E* 还是 *e* 作为指数字符。

- `c.Emax` — 指定最大指数的整数。

- `c.Emin` — 指定最小指数的整数。

- `c.prec` — 指定精度位数的整数。

- `c.flags` — 包含与信号对应的当前标志值的字典。例如，`c.flags[Rounded]` 返回 Rounded 信号的当前标志值。

- `c.rounding` — 当前有效的舍入规则。例如 `ROUND_HALF_EVEN`。

- `c.traps` — 包含导致 Python 异常的信号的 `True`/`False` 设置的字典。例如，`c.traps[DivisionByZero]` 通常为 `True`，而 `c.traps[Rounded]` 为 `False`。

- `c.clear_flags()` — 重置所有粘滞标志（清除 `c.flags`）。

- `c.copy()` — 返回上下文 *c* 的副本。

- `c.create_decimal(value)` — 使用 *c* 作为上下文创建一个新的 `Decimal` 对象。这可用于生成精度和舍入行为覆盖默认上下文的数字。

##### 函数和常量

以下函数和常量由 `decimal` 模块定义。

`getcontext()` — 返回当前的十进制上下文。每个线程都有自己的十进制上下文，因此这返回的是调用线程的上下文。

```
localcontext([c])
```

创建一个上下文管理器，该管理器将当前十进制上下文设置为 *c* 的副本，用于 `with` 语句主体内定义的语句。如果省略 *c*，则创建当前上下文的副本。下面是使用此函数的一个示例，它临时将一系列语句的精度设置为五位小数：

```
with localcontext() as c:
    c.prec = 5
    statements
```

```
setcontext(c)
```

将调用线程的十进制上下文设置为 *c*。

```
BasicContext
```

一个预定义的上下文，具有九位精度。舍入方式为 `ROUND_HALF_UP`；*Emin* 为 -999999999；*Emax* 为 999999999；除 Inexact、Rounded 和 Subnormal 外的所有陷阱均已启用。

```
DefaultContext
```

创建新上下文时使用的默认上下文（此处存储的值用作新上下文的默认值）。定义了 28 位精度；`ROUND_HALF_EVEN` 舍入；以及 Overflow、InvalidOperation 和 DivisionByZero 的陷阱。

```
ExtendedContext
```

一个预定义的上下文，具有九位精度。舍入方式为 `ROUND_HALF_EVEN`，*Emin* 为 -999999999，*Emax* 为 999999999，并且所有陷阱均已禁用。从不引发异常。相反，结果可能设置为 NaN 或 Infinity。

```
Inf
```

与 `Decimal("Infinity")` 相同。

```
negInf
```

与 `Decimal("-Infinity")` 相同。

```
NaN
```

与 `Decimal("NaN")` 相同。

##### 示例

以下是一些展示十进制数字基本用法的示例：

```
>>> a = Decimal("42.5")
>>> b = Decimal("37.1")
>>> a + b
Decimal("79.6")
>>> a / b
Decimal("1.145552560646900269541778976")
>>> divmod(a,b)
(Decimal("1"), Decimal("5.4"))
>>> max(a,b)
Decimal("42.5")
>>> c = [Decimal("4.5"), Decimal("3"), Decimal("1.23e3")]
>>> sum(c)
Decimal("1237.5")
>>> [10*x for x in c]
[Decimal("45.0"), Decimal("30"), Decimal("1.230e4")]
>>> float(a)
42.5
>>> str(a)
'42.5'
```

下面是更改上下文参数的示例：

```
>>> getcontext().prec = 4
>>> a = Decimal("3.4562384105")
>>> a
Decimal("3.4562384105")
>>> b = Decimal("5.6273833")
>>> getcontext().flags[Rounded]
0
>>> a + b
9.084
>>> getcontext().flags[Rounded]
1
>>> a / Decimal("0")
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
decimal.DivisionByZero: x / 0
>>> getcontext().traps[DivisionByZero] = False
>>> a / Decimal("0")
Decimal("Infinity")
```

##### 注意事项

- `Decimal` 和 `Context` 对象拥有大量与十进制运算表示和行为相关的底层细节方法。这些方法未在本文档中记录，因为它们对于该模块的基本使用并非必需。然而，您应该查阅在线文档 http://docs.python.org/library/decimal.html 以获取更多信息。

- 十进制上下文是每个线程独有的。对上下文的更改仅影响该线程，而不影响其他线程。

- 一个特殊数字 `Decimal("sNaN")` 可用作信号 NaN。此数字不会由任何内置函数生成。但是，如果在计算中出现，则总会发出错误信号。您可以使用此特性来指示必须导致错误且不得被静默忽略的无效计算。例如，一个函数可以返回 `sNaN` 作为结果。

- 0 的值可以是正数或负数（即，`Decimal(0)` 和 `Decimal("-0")`）。不同的零在比较时仍然相等。

- 由于计算涉及大量开销，该模块可能不适合高性能科学计算。此外，在此类应用中，使用十进制浮点数通常比使用二进制浮点数几乎没有实际好处。

- 关于浮点表示和误差分析的完整数学讨论超出了本书的范围。读者应查阅数值分析书籍以获取更多细节。David Goldberg 发表在《计算调查》（*Computing Surveys*，美国计算机协会，1991年3月）上的文章“每个计算机科学家应该知道的浮点算术知识”也值得一读（如果您只需搜索标题，这篇文章很容易在网上找到）。

- IBM 通用十进制算术规范包含更多信息，并且可以通过搜索引擎轻松在线找到。

#### fractions

`fractions` 模块定义了一个表示有理数的类 `Fraction`。可以使用类构造函数以三种不同的方式创建实例：

```
Fraction([numerator [,denominator]])
```

创建一个新的有理数。`numerator` 和 `denominator` 具有整数值，分别默认为 `0` 和 `1`。

```
Fraction(fraction)
```

如果 `fraction` 是 `numbers.Rational` 的实例，则创建一个与 `fraction` 值相同的新有理数。

```
Fraction(s)
```

如果 `s` 是一个字符串，包含分数如 `"3/7"` 或 `"-4/7"`，则创建一个具有相同值的分数。如果 `s` 是一个小数，如 `"1.25"`，则创建一个具有该值的分数（例如，`Fraction(5,4)`）。

以下类方法可以从其他类型的对象创建 `Fraction` 实例：

```
Fraction.from_float(f)
```

创建一个表示浮点数 `f` 精确值的分数。

```
Fraction.from_decimal(d)
```

创建一个表示 `Decimal` 数字 `d` 精确值的分数。

以下是一些使用这些函数的示例：

```
>>> f = fractions.Fraction(3,4)
>>> g = fractions.Fraction("1.75")
>>> g
Fraction(7, 4)
>>> h = fractions.Fraction.from_float(3.1415926)
Fraction(3537118815677477, 1125899906842624)
```

`Fraction` 的实例 `f` 支持所有常见的数学运算。分子和分母分别存储在 `f.numerator` 和 `f.denominator` 属性中。此外，定义了以下方法：

```
f.limit_denominator([max_denominator])
```

返回与 `f` 值最接近的分数。`max_denominator` 指定要使用的最大分母，默认为 `1000000`。



#### math

`math`模块定义了以下标准数学函数。这些函数适用于整数和浮点数，但不适用于复数（如需对复数进行类似操作，可使用单独的`cmath`模块）。所有函数的返回值均为浮点数。所有三角函数均假定使用弧度制。

| 函数 | 描述 |
|------|------|
| acos(x) | 返回x的反余弦值。 |
| acosh(x) | 返回x的双曲反余弦值。 |
| asin(x) | 返回x的反正弦值。 |
| asinh(x) | 返回x的双曲反正弦值。 |
| atan(x) | 返回x的反正切值。 |
| atan2(y, x) | 返回atan(y / x)。 |
| atanh(x) | 返回x的双曲反正切值。 |
| ceil(x) | 返回x的上取整值。 |
| copysign(x,y) | 返回与y符号相同的x值。 |
| cos(x) | 返回x的余弦值。 |
| cosh(x) | 返回x的双曲余弦值。 |
| degrees(x) | 将x从弧度转换为角度。 |
| radians(x) | 将x从角度转换为弧度。 |
| exp(x) | 返回e ** x。 |
| fabs(x) | 返回x的绝对值。 |
| factorial(x) | 返回x的阶乘。 |
| floor(x) | 返回x的下取整值。 |
| fmod(x, y) | 返回x % y，其计算方式与C语言的fmod()函数相同。 |
| frexp(x) | 返回x的正尾数和指数，结果为一个元组。 |
| fsum(s) | 返回可迭代序列`s`中所有浮点数值的高精度和。详细描述请参见下文注释。 |
| hypot(x, y) | 返回欧几里得距离，即sqrt(x * x + y * y)。 |
| isinf(x) | 如果x为无穷大则返回True。 |
| isnan(x) | 如果x为NaN则返回True。 |
| ldexp(x, i) | 返回x * (2 ** i)。 |
| log(x [, base]) | 返回x以给定底数的对数。如果省略底数，则计算自然对数。 |
| log10(x) | 返回x以10为底的对数。 |
| log1p(x) | 返回1+x的自然对数。 |
| modf(x) | 返回x的分数部分和整数部分，结果为一个元组。两者均与x符号相同。 |
| pow(x, y) | 返回x ** y。 |
| sin(x) | 返回x的正弦值。 |
| sinh(x) | 返回x的双曲正弦值。 |
| sqrt(x) | 返回x的平方根。 |
| tan(x) | 返回x的正切值。 |
| tanh(x) | 返回x的双曲正切值。 |
| trunc(x) | 将x截断为最接近0的整数。 |

定义了以下常量：

| 常量 | 描述 |
|------|------|
| pi | 数学常数π |
| e | 数学常数e |

###### 注释

- 浮点值+inf、-inf和nan可以通过向`float()`函数传递字符串来创建，例如：`float("inf")`、`float("-inf")`或`float("nan")`。
- `math.fsum()`函数比内置的`sum()`函数更精确，因为它使用了一种不同的算法，旨在避免因相消效应而引入的浮点误差。例如，考虑序列`s = [1, 1e100, -1e100]`。如果使用`sum(s)`，结果将为0.0（因为当1与大数1e100相加时，1的值会丢失）。然而，使用`math.fsum(s)`则会得到正确的结果1.0。`math.fsum()`所使用的算法在Jonathan Richard Shewchuk的论文"Adaptive Precision Floating-Point Arithmetic and Fast Robust Geometric Predicates"（卡内基梅隆大学计算机科学系技术报告CMU-CS-96-140，1996）中有描述。

#### numbers

`numbers`模块定义了一系列抽象基类，用于组织各种数字类型。数字类被组织成一个层次结构，其中每一级都逐步增加更多的功能。

##### Number

作为数字层次结构顶层的类。

###### Complex

表示复数的类。此类型的数字具有`real`和`imag`属性。此类继承自`Number`。

###### Real

表示实数的类。继承自`Complex`。

###### Rational

表示分数的类。此类型的数字具有`numerator`和`denominator`属性。继承自`Real`。

###### Integral

表示整数的类。继承自`Rational`。

此模块中的类并非旨在被实例化。相反，它们可用于对值执行各种类型检查。例如：

```
if isinstance(x, numbers.Number)    # x是任何类型的数字
    statements

if isinstance(x, numbers.Integral)  # x是一个整数值
    statements
```

这些抽象基类也可用作旨在模拟数字的用户定义类的基类。这样做不仅对于类型检查是个好主意，它还增加了额外的安全检查，以确保您实现了所有必需的方法。例如：

```
>>> class Foo(numbers.Real): pass
...
>>> f = Foo()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class Foo with abstract methods
__abs__, __add__, __div__, __eq__, __float__, __floordiv__, __le__, __lt__,
__mod__, __mul__, __neg__, __pos__, __pow__, __radd__, __rdiv__,
__rfloordiv__,
__rmod__, __rmul__, __rpow__, __rtruediv__, __truediv__, __trunc__
>>>
```

###### 注释

- 有关抽象基类的更多信息，请参阅第7章（"类与面向对象编程"）。
- PEP 3141 (http://www.python.org/dev/peps/pep-3141) 包含有关此模块类型层次结构和预期用途的更多信息。

#### random

`random`模块提供了多种用于生成伪随机数的函数，以及用于根据实数上的各种分布随机生成值的函数。此模块中的大多数函数都依赖于`random()`函数，该函数使用梅森旋转算法在范围[0.0, 1.0)内生成均匀分布的数字。

##### 种子与初始化

以下函数用于控制底层随机数生成器的状态：

```
seed([x])
```

初始化随机数生成器。如果省略x或x为None，则使用系统时间作为生成器的种子。否则，如果x是整数或长整数，则使用其值。如果x不是整数，则它必须是可哈希的对象，并且使用`hash(x)`的值作为种子。

```
getstate()
```

返回一个表示生成器当前状态的对象。此对象稍后可传递给`setstate()`以恢复状态。

```
setstate(state)
```

从`getstate()`返回的对象恢复随机数生成器的状态。

```
jumpahead(n)
```

快速将生成器的状态更改为如果连续调用`random()` n次后的状态。n必须是非负整数。

##### 随机整数

以下函数用于操作随机整数。

```
getrandbits(k)
```

创建一个包含k个随机位的长整数。

```
randint(a,b)
```

返回一个随机整数x，在范围a <= x <= b内。

```
randrange(start,stop [,step])
```

返回一个在range(start,stop,step)范围内的随机整数。不包含终点。

##### 随机序列

以下函数用于随机化序列数据。

```
choice(seq)
```

从非空序列`seq`中返回一个随机元素。

```
sample(s, len)
```

返回一个长度为`len`的序列，其中包含从序列`s`中随机选择的元素。结果序列中的元素按被选中的顺序放置。

```
shuffle(x [,random])
```

就地随机打乱列表`x`中的元素。`random`是可选参数，用于指定一个随机生成函数。如果提供，该函数必须不接受参数并返回一个在范围[0.0, 1.0)内的浮点数。

##### 实值随机分布

以下函数在实数上生成随机数。分布和参数名称对应于概率和统计中使用的标准名称。您需要查阅相关文献以获取更多详细信息。

```
random()
```

返回一个在范围[0.0, 1.0)内的随机数。

```
uniform(a,b)
```

返回一个在范围[*a*, *b*)内的均匀分布随机数。

```
betavariate(alpha, beta)
```

返回来自Beta分布的一个值，在0和1之间。`alpha > -1`且`beta > -1`。

```
cunifvariate(mean, arc)
```

循环均匀分布。*mean*是平均角度，*arc*是分布的范围，以平均角度为中心。这两个值都必须以弧度指定，范围在0到`pi`之间。返回值范围为(`mean - arc/2`, `mean + arc/2`)。

```
expovariate(lambd)
```

指数分布。*lambd*是1.0除以期望的平均值。返回值范围在`[0, +Infinity)`。

```
gammavariate(alpha, beta)
```

Gamma分布。`alpha > -1`，`beta > 0`。

```
gauss(mu, sigma)
```

高斯（正态）分布，均值为*mu*，标准差为*sigma*。比`normalvariate()`稍快。

```
lognormvariate(mu, sigma)
```

对数正态分布。取此分布的自然对数会得到一个均值为*mu*，标准差为*sigma*的正态分布。

```
normalvariate(mu, sigma)
```

正态分布，均值为*mu*，标准差为*sigma*。

```
paretovariate(alpha)
```

具有形状参数 `alpha` 的帕累托分布。

```
triangular([low [, high [, mode]]])
```

三角分布。一个范围在 `low <= n < high` 之间的随机数 *n*，众数为 `mode`。默认情况下，`low` 为 0，`high` 为 1.0，`mode` 设置为 `low` 和 `high` 的中点。

```
vonmisesvariate(mu, kappa)
```

冯·米塞斯分布，其中 `mu` 是以弧度表示的平均角度，范围在 0 到 `2 * pi` 之间，`kappa` 是非负的集中度因子。如果 `kappa` 为零，则该分布简化为 0 到 `2 * pi` 范围内的均匀随机角度。

```
weibullvariate(alpha, beta)
```

具有尺度参数 `alpha` 和形状参数 `beta` 的威布尔分布。

##### 注意事项

- 本模块中的函数不是线程安全的。如果你在不同线程中生成随机数，应使用锁来防止并发访问。

- 随机数生成器的周期（在数字开始重复之前）为 2\*\*19937-1。

- 本模块生成的随机数是确定性的，不应用于密码学。

- 可以通过子类化 `random.Random` 并实现 `random()`、`seed()`、`getstate()`、`setstate()` 和 `jumpahead()` 方法来创建新型随机数生成器。本模块中的所有其他函数实际上在内部都是作为 `Random` 的方法实现的。因此，它们可以作为新随机数生成器实例的方法来访问。

- 本模块提供了两种替代的随机数生成器类——`WichmannHill` 和 `SystemRandom`——通过实例化相应的类并将上述函数作为方法调用来使用。`WichmannHill` 类实现了早期 Python 版本中使用的 Wichmann-Hill 生成器。`SystemRandom` 类使用系统随机数生成器 `os.urandom()` 生成随机数。

### 第 15 章 数据结构、算法和代码简化

本章中的模块用于解决与数据结构、算法以及涉及迭代、函数式编程、上下文管理器和类的代码简化相关的常见编程问题。这些模块应被视为 Python 内置类型和函数的扩展。在许多情况下，底层实现是高度高效的，可能比内置类型更适合某些类型的问题。

#### abc

`abc` 模块定义了一个元类和一对装饰器，用于定义新的抽象基类。

##### ABCMeta

一个表示抽象基类的元类。要定义抽象类，你需要定义一个使用 `ABCMeta` 作为元类的类。例如：

```
import abc
class Stackable:               # In Python 3, use the syntax
    __metaclass__ = abc.ABCMeta  # class Stackable(metaclass=abc.ABCMeta)
    ...
```

以这种方式创建的类与普通类在几个关键方面有所不同：

- 首先，如果抽象类定义了用 `abstractmethod` 和 `abstractproperty` 装饰器装饰的方法或属性（后文描述），那么派生类的实例无法被创建，除非这些类为这些方法和属性提供了非抽象的实现。

- 其次，抽象类有一个类方法 `register(subclass)`，可用于将其他类型注册为逻辑子类。对于通过此函数注册的任何类型子类，如果 `x` 是子类的实例，则操作 `isinstance(x, AbstractClass)` 将返回 `True`。

- 抽象类的最后一个特性是，它们可以选择性地定义一个特殊的类方法 `__subclasshook__(cls, subclass)`。如果类型子类被视为子类，此方法应返回 `True`；如果子类不是子类，则返回 `False`；如果无法确定，则引发 `NotImplemented` 异常。

**abstractmethod(method)**

一个声明 `method` 为抽象的装饰器。在抽象基类中使用时，直接通过继承定义的派生类只有在定义了该方法的非抽象实现后才能被实例化。此装饰器对通过抽象基类的 `register()` 方法注册的子类没有影响。

**abstractproperty(fget [, fset [, fdel [, doc]]])**

创建一个抽象属性。参数与普通的 `property()` 函数相同。在抽象基类中使用时，直接通过继承定义的派生类只有在定义了该属性的非抽象实现后才能被实例化。

以下代码提供了一个定义简单抽象类的示例：

```
from abc import ABCMeta, abstractmethod, abstractproperty
class Stackable:          # In Python 3, use the syntax
    __metaclass__ = ABCMeta      # class Stackable(metaclass=ABCMeta)
    @abstractmethod
    def push(self,item):
        pass
    @abstractmethod
    def pop(self):
        pass
    @abstractproperty
    def size(self):
        pass
```

以下是从 `Stackable` 派生的类的示例：

```
class Stack(Stackable):
    def __init__(self):
        self.items = []
    def push(self,item):
        self.items.append(item)
    def pop(self):
        return self.items.pop()
```

以下是你尝试创建 `Stack` 时得到的错误消息：

```
>>> s = Stack()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class Stack with abstract methods size
>>>
```

可以通过向 `Stack` 添加 `size()` 属性来修复此错误。你可以通过修改 `Stack` 本身的定义或继承它并添加所需的方法或属性来实现：

```
class CompleteStack(Stack):
    @property
    def size(self):
        return len(self.items)
```

以下是一个使用完整栈对象的示例：

```
>>> s = CompleteStack()
>>> s.push("foo")
>>> s.size
1
>>>
```

##### 另请参阅

第 7 章"类和面向对象编程"、[numbers](p. 252)、[collections](p. 262)。

#### array

`array` 模块定义了一种新的对象类型——数组，它的工作方式几乎与列表完全相同，只是其内容被限制为单一类型。数组的类型在创建时确定，使用表 15.1 中所示的类型代码之一。

| 类型代码 | 描述 | C 类型 | 最小大小（以字节为单位） |
|---|---|---|---|
| 'c' | 8 位字符 | `char` | 1 |
| 'b' | 8 位整数 | `signed char` | 1 |
| 'B' | 8 位无符号整数 | `unsigned char` | 1 |
| 'u' | Unicode 字符 | `PY_UNICODE` | 2 或 4 |
| 'h' | 16 位整数 | `short` | 2 |
| 'H' | 16 位无符号整数 | `unsigned short` | 2 |
| 'i' | 整数 | `int` | 4 或 8 |
| 'I' | 无符号整数 | `unsigned int` | 4 或 8 |
| 'l' | 长整数 | `long` | 4 或 8 |
| 'L' | 无符号长整数 | `unsigned long` | 4 或 8 |
| 'f' | 单精度浮点数 | `float` | 4 |
| 'd' | 双精度浮点数 | `double` | 8 |

整数和长整数的表示由机器架构决定（它们可以是 32 位或 64 位）。当存储为 `'L'` 或 `'I'` 的值被返回时，在 Python 2 中它们作为长整数返回。

该模块定义了以下类型：

```
array(typecode [, initializer])
```

创建一个类型为 `typecode` 的数组。`initializer` 是用于初始化数组中值的字符串或值列表。以下属性和方法适用于数组对象 `a`：

| 项目 | 描述 |
|---|---|
| `a.typecode` | 用于创建数组的类型代码字符。 |
| `a.itemsize` | 存储在数组中的项的大小（以字节为单位）。 |
| `a.append(x)` | 将 `x` 追加到数组末尾。 |
| `a.buffer_info()` | 返回 `(address, length)`，给出用于存储数组的缓冲区的内存位置和长度。 |
| `a.byteswap()` | 将数组中所有项的字节顺序从大端序交换为小端序，反之亦然。此操作仅支持整数值。 |

### 第 15 章 数据结构、算法和代码简化

| 项目 | 描述 |
|------|-------------|
| `a.count(x)` | 返回 `x` 在 `a` 中的出现次数。 |
| `a.extend(b)` | 将 `b` 追加到数组 `a` 的末尾。`b` 可以是一个数组或一个可迭代对象，其元素类型与 `a` 中的相同。 |
| `a.fromfile(f, n)` | 从文件对象 `f` 中读取 `n` 个项（二进制格式）并追加到数组末尾。`f` 必须是文件对象。如果读取的项少于 `n` 个，则引发 `EOFError`。 |
| `a.fromlist(list)` | 将 `list` 中的项追加到数组末尾。`list` 可以是任何可迭代对象。 |
| `a.fromstring(s)` | 将字符串 `s` 中的项追加到数组，其中 `s` 被解释为二进制值字符串——与使用 `fromfile()` 读取的相同。 |
| `a.index(x)` | 返回 `x` 在 `a` 中第一次出现的索引。如果未找到，则引发 `ValueError`。 |
| `a.insert(i, x)` | 在位置 `i` 之前插入 `x`。 |
| `a.pop([i])` | 从数组中移除项 `i` 并返回它。如果省略 `i`，则移除最后一个元素。 |
| `a.remove(x)` | 从数组中移除 `x` 的第一次出现。如果未找到，则引发 `ValueError`。 |
| `a.reverse()` | 反转数组的顺序。 |
| `a.tofile(f)` | 将所有项写入文件 `f`。数据以原生二进制格式保存。 |
| `a.tolist()` | 将数组转换为普通值列表。 |
| `a.tostring()` | 转换为二进制数据字符串——与使用 `tofile()` 写入的数据相同。 |
| `a.tounicode()` | 将数组转换为 Unicode 字符串。如果数组不是 `'u'` 类型，则引发 `ValueError`。 |

当项被插入数组时，如果项的类型与创建数组时使用的类型不匹配，则会生成 `TypeError` 异常。

如果你需要对数据列表进行节省空间的存储，并且知道列表中所有项都是同一类型，那么 `array` 模块非常有用。例如，将 1000 万个整数存储在列表中需要大约 160MB 的内存，而 1000 万个整数的数组只需要 40MB。尽管节省了空间，但数组上的基本操作往往不比列表的对应操作更快——实际上，它们可能更慢。

在使用数组执行计算时，你需要注意那些创建列表的操作。例如，对数组使用列表推导式会将整个数组转换为列表，从而失去任何节省空间的好处。更好的方法是使用生成器表达式创建新数组。例如：

```
a = array.array("i", [1,2,3,4,5])
b = array.array(a.typecode, (2*x for x in a))   # Create a new array from a
```

因为使用数组的目的是节省空间，所以执行"原地"操作可能更可取。一种高效的方法是使用 `enumerate()` 的代码，如下所示：

```
a = array.array("i", [1,2,3,4,5])
for i, x in enumerate(a):
    a[i] = 2*x
```



对于大型数组，这种就地修改比使用生成器表达式创建新数组的代码快大约 15%。

##### 注意事项

-   此模块创建的数组不适合用于矩阵或向量数学等数值计算工作。例如，加法运算符不会将数组的对应元素相加；而是将一个数组追加到另一个数组末尾。要创建存储和计算效率高的数组，请使用 http://numpy.sourceforge.net/ 上提供的 numpy 扩展。请注意，numpy 的 API 完全不同。
-   `+=` 运算符可用于追加另一个数组的内容。`*=` 运算符可用于重复一个数组。

另请参阅：

struct（第 290 页）

#### bisect

bisect 模块提供了保持列表有序排列的支持。它使用二分法算法来完成大部分工作。

```
bisect(list, item [, low [, high]])
```

返回将 item 插入到 list 中以保持 list 有序排列的插入点索引。low 和 high 是指定要检查的列表子集的索引。如果 item 已在列表中，插入点将始终位于列表中已有条目的右侧。

```
bisect_left(list, item [, low [, high]])
```

返回将 item 插入到 list 中以保持 list 有序排列的插入点索引。low 和 high 是指定要检查的列表子集的索引。如果 item 已在列表中，插入点将始终位于列表中已有条目的左侧。

```
bisect_right(list, item [, low [, high]])
```

与 `bisect()` 相同。

```
insort(list, item [, low [, high]])
```

将 item 按有序顺序插入 list 中。如果 item 已在列表中，新条目将插入到所有已有条目的右侧。

```
insort_left(list, item [, low [, high]])
```

将 item 按有序顺序插入 list 中。如果 item 已在列表中，新条目将插入到所有已有条目的左侧。

```
insort_right(list, item [, low [, high]])
```

与 `insort()` 相同。

#### collections

collections 模块包含几个有用的容器类型的高性能实现、各种容器的抽象基类，以及一个用于创建具名元组对象的实用函数。每个部分将在后续章节中进行描述。

##### deque 和 defaultdict

collections 模块中定义了两个新的容器：deque 和 defaultdict。

```
deque([iterable [, maxlen]])
```

表示双端队列（deque，发音为"deck"）对象的类型。iterable 是用于填充 deque 的可迭代对象。deque 允许从队列的任一端插入或删除条目。其实现已过优化，使得这些操作的性能大致相同（O(1)）。这与列表略有不同，因为在列表前端的操作可能需要移动其后的所有元素。如果提供了可选的 maxlen 参数，生成的 deque 对象将成为该大小的循环缓冲区。也就是说，如果添加了新条目但没有更多空间，则会从另一端删除条目以腾出空间。

deque 的实例 `d` 具有以下方法：

```
d.append(x)
```

将 x 添加到 d 的右侧。

```
d.appendleft(x)
```

将 x 添加到 d 的左侧。

```
d.clear()
```

从 d 中移除所有条目。

```
d.extend(iterable)
```

通过将 iterable 中的所有条目添加到右侧来扩展 d。

```
d.extendleft(iterable)
```

通过将 iterable 中的所有条目添加到左侧来扩展 d。由于左端追加的顺序，iterable 中的条目在 d 中将以相反的顺序出现。

```
d.pop()
```

返回并从 d 的右侧移除一个条目。如果 d 为空，则引发 IndexError。

```
d.popleft()
```

返回并从 d 的左侧移除一个条目。如果 d 为空，则引发 IndexError。

```
d.remove(item)
```

移除第一次出现的 item。如果未找到匹配项，则引发 ValueError。

```
d.rotate(n)
```

将所有条目向右旋转 *n* 步。如果 *n* 为负数，则向左旋转条目。

deque 常被许多 Python 程序员忽视。然而，这种类型提供了许多优势。首先，其实现非常高效——甚至达到了使用能提供良好处理器缓存行为的内部数据结构的水平。在末尾追加条目仅比内置 `list` 类型稍慢，而在前端插入条目则明显更快。向 deque 添加新条目的操作也是线程安全的，使其适合用于实现队列。`deques` 也可以使用 `pickle` 模块进行序列化。

```
defaultdict([default_factory], ...)
```

一种与字典完全相同的类型，只是对缺失键的处理方式不同。当查找一个尚不存在的键时，会调用作为 `default_factory` 提供的函数来提供默认值，然后将其保存为关联键的值。`defaultdict` 的其余参数与内置 `dict()` 函数完全相同。`defaultdict` 的实例 *d* 具有与内置字典相同的操作。属性 `d.default_factory` 包含作为第一个参数传递的函数，可以根据需要进行修改。

当你尝试使用字典作为跟踪数据的容器时，`defaultdict` 对象非常有用。例如，假设你想跟踪字符串 *s* 中每个单词的位置。以下是你可以如何使用 `defaultdict` 轻松完成此操作的方法：

```
>>> from collections import defaultdict
>>> s = "yeah but no but yeah but no but yeah"
>>> words = s.split()
>>> wordlocations = defaultdict(list)
>>> for n, w in enumerate(words):
...     wordlocations[w].append(n)
...
>>> wordlocations
defaultdict(<type 'list'>, {'yeah': [0, 4, 8], 'but': [1, 3, 5, 7], 'no': [2, 6]})
>>>
```

在此示例中，查找 `wordlocations[w]` 在第一次遇到某个单词时会"失败"。然而，它不会引发 `KeyError`，而是调用作为 `default_factory` 提供的函数 `list` 来创建一个新值。内置字典有一个 `setdefault()` 方法，可用于实现类似的结果，但它通常使代码难以阅读且运行更慢。例如，前面显示的追加新条目的语句可以替换为 `wordlocations.setdefault(w, []).append(n)`。这远不如使用 `defaultdict` 对象那样清晰，而且在简单的计时测试中，它的运行速度几乎慢两倍。

##### 具名元组

*元组* 常用于表示简单的数据结构。例如，网络地址可以表示为元组 `addr = (hostname, port)`。元组的一个常见抱怨是必须通过数字索引来访问各个条目——例如 `addr[0]` 或 `addr[1]`。这会导致代码难以阅读且难以维护，除非你能记住所有索引值的含义（而且元组越大，问题就越严重）。

collections 模块包含一个名为 namedtuple() 的函数，用于创建 tuple 的子类，其中可以使用属性名称来访问元组元素。

```
namedtuple(typename, fieldnames [, verbose])
```

创建一个名为 typename 的 tuple 子类。fieldnames 是以字符串形式指定的属性名称列表。此列表中的名称必须是有效的 Python 标识符，不能以下划线开头，并且按照元组中条目出现的顺序指定——例如 ['hostname','port']。或者，fieldnames 可以指定为字符串，如 'hostname port' 或 'hostname, port'。此函数返回的类的名称已设置为在 typename 中提供的值。你使用此类来创建具名元组的实例。verbose 标志如果设置为 True，会将生成的类定义打印到标准输出。

以下是使用此函数的示例：

```
>>> from collections import namedtuple
>>> NetworkAddress = namedtuple('NetworkAddress',['hostname','port'])
>>> a = NetworkAddress('www.python.org',80)
>>> a.hostname
'www.python.org'
>>> a.port
80
>>> host, port = a
>>> len(a)
2
>>> type(a)
<class '__main__.NetworkAddress'>
>>> isinstance(a, tuple)
True
>>>
```

在此示例中，具名元组 NetworkAddress 在各方面都与普通元组无法区分，只是额外支持使用属性查找（如 a.hostname 或 a.port）来访问元组组件。底层实现是高效的——创建的类不使用实例字典，也不会在内置元组基础上增加任何额外的内存开销。所有正常的元组操作仍然有效。

如果定义的对象仅作为数据结构使用，具名元组会非常有用。例如，不是这样定义一个类：

```
class Stock(object):
    def __init__(self,name,shares,price):
        self.name = name
        self.shares = shares
        self.price = price
```

你可以改为定义一个具名元组：

```
import collections
Stock = collections.namedtuple('Stock','name shares price')
```

两种版本的使用方式几乎完全相同。例如，在任一情况下，你都可以通过编写 s.name、s.shares 等来访问字段。然而，具名元组的优势在于它更节省内存，并且支持各种元组操作，例如解包（例如，如果你有一个具名元组列表，你可以使用 for name, shares, 这样的语句在 for 循环中解包值。

price in stockList)。命名元组的缺点是属性访问的效率不如类。例如，如果 `s` 是命名元组的实例而非普通类的实例，访问 `s.shares` 的速度会慢一倍以上。

命名元组在 Python 标准库的其他部分中被广泛使用。其使用部分源于历史原因——在许多库模块中，元组最初被用作各种函数的返回值，这些函数返回关于文件、栈帧或其他底层细节的信息。使用这些元组的代码并不总是那么优雅。因此，切换到命名元组是为了在不破坏向后兼容性的情况下清理其用法。元组的另一个微妙问题在于，一旦你开始使用元组，预期的字段数量就被永久锁定（例如，如果你突然添加一个新字段，旧代码就会出错）。命名元组的变体已在库中用于向某些函数返回的数据添加新字段。例如，一个对象可能支持传统的元组接口，但同时提供仅作为命名属性可用的附加值。

##### 抽象基类

`collections` 模块定义了一系列抽象基类。这些类的目的是描述各种容器（如列表、集合和字典）的编程接口。这些类有两个主要用途。首先，它们可以用作用户定义对象的基类，以模拟内置容器类型的功能。其次，它们可以用于类型检查。例如，如果你想检查 `s` 是否像序列一样工作，你可以使用 `isinstance(s, collections.Sequence)`。

###### Container
所有容器的基类。定义了一个抽象方法 `__contains__()`，用于实现 `in` 运算符。

###### Hashable
可用作哈希表键的对象的基类。定义了一个抽象方法 `__hash__()`。

###### Iterable
支持迭代协议的对象的基类。定义了一个抽象方法 `__iter__()`。

###### Iterator
迭代器对象的基类。定义了抽象方法 `next()`，但同时继承自 `Iterable` 并提供 `__iter__()` 的默认实现，该默认实现不做任何事情。

###### Sized
大小可确定的容器的基类。定义了抽象方法 `__len__()`。

###### Callable
支持函数调用的对象的基类。定义了抽象方法 `__call__()`。

###### Sequence
看起来像序列的对象的基类。继承自 `Container`、`Iterable` 和 `Sized`，定义了抽象方法 `__getitem__()` 和 `__len__()`。还提供了 `__contains__()`、`__iter__()`、`__reversed__()`、`index()` 和 `count()` 的默认实现，这些实现仅使用 `__getitem__()` 和 `__len__()` 方法完成。

###### MutableSequence
可变序列的基类。继承自 `Sequence`，并添加了抽象方法 `__setitem__()` 和 `__delitem__()`。还提供了 `append()`、`reverse()`、`extend()`、`pop()`、`remove()` 和 `__iadd__()` 的默认实现。

###### Set
像集合一样工作的对象的基类。继承自 `Container`、`Iterable` 和 `Sized`，定义了抽象方法 `__len__()`、`__iter__()` 和 `__contains__()`。还提供了集合运算符 `__le__()`、`__lt__()`、`__eq__()`、`__ne__()`、`__gt__()`、`__ge__()`、`__and__()`、`__or__()`、`__xor__()`、`__sub__()` 和 `isdisjoint()` 的默认实现。

###### MutableSet
可变集合的基类。继承自 `Set`，并添加了抽象方法 `add()` 和 `discard()`。还提供了 `clear()`、`pop()`、`remove()`、`__ior__()`、`__iand__()`、`__ixor__()` 和 `__isub__()` 的默认实现。

###### Mapping
支持映射（字典）查找的对象的基类。继承自 `Sized`、`Iterable` 和 `Container`，定义了抽象方法 `__getitem__()`、`__len__()` 和 `__iter__()`。还提供了 `__contains__()`、`keys()`、`items()`、`values()`、`get()`、`__eq__()` 和 `__ne__()` 的默认实现。

###### MutableMapping
可变映射对象的基类。继承自 `Mapping`，并添加了抽象方法 `__setitem__()` 和 `__delitem__()`。还添加了 `pop()`、`popitem()`、`clear()`、`update()` 和 `setdefault()` 的实现。

###### MappingView
映射视图的基类。*映射视图* 是用于将映射对象的内部作为集合进行访问的对象。例如，键视图是显示映射中键的类集合对象。更多详情请参见附录 A "Python 3"。

###### KeysView
映射键视图的基类。继承自 `MappingView` 和 `Set`。

###### ItemsView
映射项视图的基类。继承自 `MappingView` 和 `Set`。

###### ValuesView
映射 `(key, item)` 视图的基类。继承自 `MappingView` 和 `Set`。

Python 的内置类型已根据需要注册到所有这些基类中。此外，通过使用这些基类，可以编写在类型检查方面更精确的程序。以下是一些示例：

```python
# Pull off the last item of a sequence
if isinstance(x, collections.Sequence):
    last = x[-1]

# Only iterate over an object if its size is known
if isinstance(x, collections.Iterable) and isinstance(x, collections.Sized):
    for item in x:
        statements

# Add a new item to a set
if isinstance(x, collections.MutableSet):
    x.add(item)
```

**另见：**
第 7 章 "类与面向对象编程。"

#### contextlib

contextlib 模块提供了一个装饰器和一些实用函数，用于创建与 with 语句配合使用的上下文管理器。

**contextmanager(func)**

一个装饰器，用于从生成器函数 `func` 创建上下文管理器。使用此装饰器的方式如下：

```python
@contextmanager
def foo(args):
    statements
    try:
        yield value
    except Exception as e:
        error handling (if any)
    statements
```

当 `with foo(args) as value` 语句出现时，生成器函数会以提供的参数执行，直到遇到第一个 yield 语句。yield 返回的值被放入变量 `value` 中。此时，with 语句的主体开始执行。完成后，生成器函数恢复执行。如果在 with 主体内部抛出任何异常，该异常会在生成器函数内部被抛出，从而可以进行适当处理。如果要传播错误，生成器应使用 raise 来重新抛出异常。使用此装饰器的示例可以在第 5 章的"上下文管理器"部分中找到。

**nested(mgr1, mgr2, ..., mgrN)**

一个函数，将多个上下文管理器 `mgr1`、`mgr2` 等作为单个操作调用。返回一个包含各 with 语句不同返回值的元组。`with nested(m1,m2) as (x,y): statements` 等同于 `with m1 as x: with m2 as y: statements`。请注意，如果内部上下文管理器捕获并抑制了异常，则不会将异常信息传递给外部管理器。

##### closing(object)
创建一个上下文管理器，当执行离开 `with` 语句的主体时自动执行 `object.close()`。`with` 语句返回的值与 `object` 相同。

#### functools

`functools` 模块包含用于创建高阶函数、函数式编程和装饰器的函数和装饰器。

##### partial(function [, *args [, **kwargs]])
创建一个类似函数的对象 `partial`，当调用时，会使用位置参数 `args`、关键字参数 `kwargs` 以及提供的任何其他位置或关键字参数来调用 `function`。额外的位置参数被追加到 `args` 的末尾，额外的关键字参数被合并到 `kwargs` 中，覆盖任何先前定义的值（如果有的话）。`partial()` 的典型用法是在进行大量函数调用且许多参数保持固定时。例如：

```python
from functools import partial
mybutton = partial(Button, root, fg="black", bg="white", font="times", size="12")
b1 = mybutton(text="Ok")      # Calls Button() with text="Ok" and all of the
b2 = mybutton(text="Cancel")   # additional arguments supplied to partial() above
b3 = mybutton(text="Restart")
```

由 `partial` 创建的对象的实例 `p` 具有以下属性：

| 项目 | 描述 |
|------|------|
| `p.func` | 当调用 `p` 时被调用的函数。 |
| `p.args` | 包含调用时提供给 `p.func` 的最左侧位置参数的元组。额外的位置参数被连接到此值的末尾。 |
| `p.keywords` | 包含调用时提供给 `p.func` 的关键字参数的字典。额外的关键字参数被合并到此字典中。 |

将 `partial` 对象作为常规函数的替代品使用时请谨慎。其结果与普通函数并不完全相同。例如，如果你在类定义中使用 `partial()`，它的行为类似于静态方法，而不是实例方法。

##### reduce(function, items [, initial])
将函数 `function` 累积地应用于可迭代对象 `items` 中的元素，并返回单个值。`function` 必须接受两个参数，首先应用于 `items` 的前两个元素。然后该结果与 `items` 的后续元素以类似方式逐个组合，直到 `items` 的所有元素被消耗完。`initial` 是可选的起始值，用于第一次计算以及 `items` 为空时。



此函数与 Python 2 中作为内置函数的 `reduce()` 功能相同。为了未来的兼容性，请改用此版本。

```
update_wrapper(wrapper, wrapped [, assigned [, updated]])
```

这是一个在编写装饰器时非常有用的实用函数。它将函数 *wrapped* 的属性复制到包装函数 *wrapper* 中，使被包装的函数看起来像原始函数。*assigned* 是一个要复制的属性名称元组，默认设置为 `('__name__', '__module__', '__doc__')`。*updated* 是一个包含函数属性名称的元组，这些属性是字典，你希望将它们的值合并到包装函数中。默认情况下，它是一个包含 `'__dict__'` 的元组。

```
wraps(function [, assigned [, updated ]])
```

此装饰器对其应用到的函数执行与 `update_wrapper()` 相同的任务。*assigned* 和 *updated* 具有相同的含义。此装饰器的典型用法是在编写其他装饰器时。例如：

```
from functools import wraps
def debug(func):
    @wraps(func)
    def wrapped(*args,**kwargs):
        print("Calling %s" % func.__name__)
        r = func(*args,**kwargs)
        print("Done calling %s" % func.__name__)
    return wrapped

@debug
def add(x,y):
    return x+y
```

**另请参见：**
第 6 章，“函数与函数式编程。”

#### heapq

`heapq` 模块使用堆实现了一个优先队列。*堆* 是简单有序项目的列表，并施加了堆条件。具体来说，对于所有 *n*（从 *n = 0* 开始），满足 `heap[n] <= heap[2*n+1]` 且 `heap[n] <= heap[2*n+2]`。`heap[0]` 始终包含最小的项目。

##### `heapify(x)`

将列表 *x* 原地转换为堆。

##### `heappop(heap)`

从 *heap* 中返回并移除最小的项目，同时保持堆条件。如果 *heap* 为空，则引发 `IndexError`。

##### `heappush(heap, item)`

将 *item* 添加到堆中，同时保持堆条件。

##### `heappushpop(heap, item)`

在单个操作中将项目添加到堆中并从堆中移除最小的项目。这比分别调用 `heappush()` 和 `heappop()` 更高效。

##### `heappreplace(heap, item)`

从堆中返回并移除最小的项目。同时，添加一个新项目。在此过程中保持堆条件。此函数比按顺序调用 `heappop()` 和 `heappush()` 更高效。此外，返回值是在添加新项目之前获得的。因此，返回值可能大于 item。如果堆为空，则引发 `IndexError`。

##### `merge(s1, s2, ...)`

创建一个迭代器，将已排序的可迭代对象 s1、s2 等合并为一个单一的已排序序列。此函数不会消耗输入，而是返回一个增量处理数据的迭代器。

##### `nlargest(n, iterable [, key])`

创建一个列表，包含可迭代对象中 n 个最大的项目。最大的项目出现在返回列表的开头。key 是一个可选的函数，它接受单个输入参数并计算可迭代对象中每个项目的比较键。

##### `nsmallest(n, iterable [, key])`

创建一个列表，包含可迭代对象中 n 个最小的项目。最小的项目出现在返回列表的开头。key 是一个可选的键函数。

> **注意**
> 堆队列的理论和实现可以在大多数算法书籍中找到。

#### itertools

`itertools` 模块包含用于创建高效迭代器的函数，这些迭代器对于以各种方式循环数据非常有用。此模块中的所有函数都返回迭代器，这些迭代器可用于 `for` 语句和其他涉及迭代器的函数（如生成器和生成器表达式）。

##### `chain(iter1, iter2, ..., iterN)`

给定一组迭代器（iter1, ..., iterN），此函数创建一个新迭代器，将所有迭代器链接在一起。返回的迭代器从 iter1 产生项目，直到其耗尽。然后产生 iter2 的项目。此过程持续进行，直到所有 iterN 中的项目被耗尽。

##### `chain.from_iterable(iterables)`

chain 的替代构造函数，其中 iterables 是一个产生可迭代对象序列的可迭代对象。此操作的结果与以下生成器代码片段产生的结果相同：

```
for it in iterables:
    for x in it:
        yield x
```

##### `combinations(iterable, r)`

创建一个迭代器，返回从可迭代对象中取出的长度为 r 的所有子序列。返回子序列中的项目按照它们在输入可迭代对象中的相同顺序排列。例如，如果可迭代对象是列表 [1,2,3,4]，则 `combinations([1,2,3,4], 2)` 产生的序列是 [1,2], [1,3], [1,4], [2,3], [3,4]。

##### `count([n])`

创建一个迭代器，产生从 n 开始的连续整数。如果省略 n，则从 0 开始计数。（注意，此迭代器不支持长整数。如果超过 `sys.maxint`，计数器会溢出并从 `-sys.maxint - 1` 开始继续计数。）

##### `cycle(iterable)`

创建一个迭代器，在可迭代对象的元素上循环往复。内部会创建可迭代对象元素的副本。此副本用于在循环中返回重复的项目。

##### `dropwhile(predicate, iterable)`

创建一个迭代器，只要函数 `predicate(item)` 为 True，就丢弃来自可迭代对象的项目。一旦 predicate 返回 False，则该项目及可迭代对象中所有后续项目都会被产生。

##### `groupby(iterable [, key])`

创建一个迭代器，对可迭代对象产生的连续项目进行分组。分组过程通过查找重复项目来工作。例如，如果可迭代对象在几次连续迭代中产生相同的项目，则定义一个组。如果应用于已排序的列表，则组将定义列表中的所有唯一项目。key（如果提供）是一个应用于每个项目的函数。如果存在，则使用此函数的返回值来比较连续的项目，而不是项目本身。此函数返回的迭代器产生元组 (key, group)，其中 key 是组的键值，group 是一个产生构成该组的所有项目的迭代器。

##### `ifilter(predicate, iterable)`

创建一个迭代器，仅产生可迭代对象中 `predicate(item)` 为 True 的项目。如果 predicate 为 None，则返回可迭代对象中所有求值为 True 的项目。

##### `ifilterfalse(predicate, iterable)`

创建一个迭代器，仅产生可迭代对象中 `predicate(item)` 为 False 的项目。如果 predicate 为 None，则返回可迭代对象中所有求值为 False 的项目。

##### `imap(function, iter1, iter2, ..., iterN)`

创建一个迭代器，产生项目 `function(i1, i2, .. iN)`，其中 *i1, i2, ..., iN* 分别是从迭代器 *iter1, iter2, ..., iterN* 中取出的项目。如果 *function* 为 None，则返回形式为 *(i1, i2, ..., iN)* 的元组。当提供的任一迭代器不再产生任何值时，迭代停止。

##### `islice(iterable, [start,] stop [, step])`

创建一个迭代器，以类似于切片 `iterable[start:stop:step]` 返回的方式产生项目。跳过前 *start* 个项目，并在 *stop* 指定的位置停止迭代。*step* 指定用于跳过项目的步长。与切片不同，*start*、*stop* 或 *step* 都不能使用负值。如果省略 *start*，则从 0 开始迭代。如果省略 *step*，则使用步长 1。

##### `izip(iter1, iter2, ... iterN)`

创建一个迭代器，产生元组 *(i1, i2, ..., iN)*，其中 *i1, i2, ..., iN* 分别取自迭代器 *iter1, iter2, ..., iterN*。当提供的任一迭代器不再产生任何值时，迭代停止。此函数产生的值与内置 `zip()` 函数相同。

##### `izip_longest(iter1, iter2, ..., iterN [, fillvalue=None])`

与 `izip()` 相同，只是迭代持续进行，直到所有输入可迭代对象 *iter1, iter2* 等耗尽。使用 None 来填充已消耗的可迭代对象的值，除非通过 *fillvalue* 关键字参数指定了不同的值。

##### `permutations(iterable [, r])`

创建一个迭代器，返回 *iterable* 中项目的 *r* 长度的所有排列。如果省略 *r*，则排列的长度与 *iterable* 中项目数相同。

##### `product(iter1, iter2, ..., iterN, [repeat=1])`

创建一个迭代器，产生表示 *item1, item2* 等项目笛卡尔积的元组。*repeat* 是一个关键字参数，指定重复产生序列的次数。

##### `repeat(object [, times])`

创建一个迭代器，重复产生 *object*。如果提供 *times*，则指定重复次数。否则，将无限期返回该对象。

##### `starmap(func [, iterable])`

创建一个迭代器，产生值 `func(*item)`，其中 *item* 取自 *iterable*。这仅在 *iterable* 产生适合以此方式调用函数的项目时有效。

##### `takewhile(predicate [, iterable])`

创建一个迭代器，只要 `predicate(item)` 为 True，就产生来自 *iterable* 的项目。一旦 *predicate* 求值为 False，迭代立即停止。



**tee(iterable [, n])**

从*iterable*创建*n*个独立的迭代器。创建的迭代器以n元组形式返回。*n*的默认值为2。此函数适用于任何可迭代对象。然而，为了克隆原始迭代器，产生的元素会被缓存并在所有新创建的迭代器中使用。应特别注意，在调用`tee()`之后不要使用原始迭代器*iterable*。否则，缓存机制可能无法正常工作。

##### 示例

以下示例说明了`itertools`模块中某些函数的操作方式：

```
from itertools import *
###### 在一个无限循环中迭代数字0,1,...,10,9,8,...,1
for i in cycle(chain(range(10),range(10,0,-1))):
    print i

###### 创建一个包含a中唯一元素的列表
a = [1,4,5,4,9,1,2,3,4,5,1]
a.sort()
b = [k for k,g in groupby(a)]   # b = [1,2,3,4,5,9]

###### 迭代x和y中值的所有可能的配对组合
x = [1,2,3,4,5]
y = [10,11,12]
for r in product(x,y):
    print(r)
###### 产生输出 (1,10),(1,11),(1,12), ... (5,10),(5,11),(5,12)
```

#### operator

operator模块提供了访问解释器内置运算符和特殊方法的函数，这些方法在第3章“类型与对象”中有所描述。例如，`add(3, 4)`等同于`3 + 4`。对于具有就地版本的操作，可以使用类似`iadd(x,y)`的函数，它等同于`x += y`。以下列表展示了operator模块中定义的函数及其映射到的各种运算符：

| 函数 | 描述 |
|----------|-------------|
| `add(a, b)` | 对数字返回 `a + b` |
| `sub(a, b)` | 返回 `a - b` |
| `mul(a, b)` | 对数字返回 `a * b` |
| `div(a, b)` | 返回 `a / b`（旧式除法） |
| `floordiv(a, b)` | 返回 `a // b` |
| `truediv(a, b)` | 返回 `a / b`（新式除法） |
| `mod(a, b)` | 返回 `a % b` |
| `neg(a)` | 返回 `-a` |
| `pos(a)` | 返回 `+a` |
| `abs(a)` | 返回 *a* 的绝对值 |
| `inv(a), invert(a)` | 返回 *a* 的逆 |
| `lshift(a, b)` | 返回 `a << b` |
| `rshift(a, b)` | 返回 `a >> b` |
| `and_(a, b)` | 返回 `a & b`（按位与） |
| `or_(a, b)` | 返回 `a \| b`（按位或） |
| `xor(a, b)` | 返回 `a ^ b`（按位异或） |
| `not_(a)` | 返回 `not a` |
| `lt(a, b)` | 返回 `a < b` |
| `le(a, b)` | 返回 `a <= b` |
| `eq(a, b)` | 返回 `a == b` |
| `ne(a, b)` | 返回 `a != b` |
| `gt(a, b)` | 返回 `a > b` |
| `ge(a, b)` | 返回 `a >= b` |
| `truth(a)` | 如果 `a` 为真则返回 `True`，否则返回 `False` |
| `concat(a, b)` | 对序列返回 `a + b` |
| `repeat(a, b)` | 对序列 `a` 和整数 `b` 返回 `a * b` |
| `contains(a, b)` | 返回 `b in a` 的结果 |
| `countOf(a, b)` | 返回 `b` 在 `a` 中出现的次数 |
| `indexOf(a, b)` | 返回 `b` 在 `a` 中首次出现的索引 |
| `getitem(a, b)` | 返回 `a[b]` |
| `setitem(a, b, c)` | `a[b] = c` |
| `delitem(a, b)` | `del a[b]` |
| `getslice(a, b, c)` | 返回 `a[b:c]` |
| `setslice(a, b, c, v)` | 设置 `a[b:c] = v` |
| `delslice(a, b, c)` | `del a[b:c]` |
| `is_(a, b)` | `a is b` |
| `is_not(a, b)` | `a is not b` |

乍一看，可能不太明显为什么有人会想使用这些函数，因为它们执行的操作可以通过简单输入正常语法来轻松完成。这些函数在使用回调函数的代码中，或者原本需要用`lambda`定义匿名函数的地方非常有用。例如，考虑以下使用`functools.reduce()`函数的计时基准测试：

```
>>> from timeit import timeit
>>> timeit("reduce(operator.add,a)","import operator; a = range(100)")
12.055853843688965
>>> timeit("reduce(lambda x,y: x+y,a)","import operator; a = range(100)")
25.012306928634644
>>>
```

在示例中，请注意使用`operator.add`作为回调的版本比使用`lambda x,y: x+y`的版本运行速度快了两倍多。

operator模块还定义了以下函数，这些函数创建了围绕属性访问、项查找和方法调用的包装器。

```
attrgetter(name [, name2 [, ... [, nameN]]])
```

创建一个可调用对象f，其中调用`f(obj)`返回`obj.name`。如果给出多个参数，则返回一个结果元组。例如，`attrgetter('name','shares')`被调用时返回`(obj.name, obj.shares)`。`name`也可以包含额外的点查找。例如，如果`name`是`"address.hostname"`，那么`f(obj)`返回`obj.address.hostname`。

```
itemgetter(item [, item2 [, ... [, itemN]]])
```

创建一个可调用对象f，其中调用`f(obj)`返回`obj[item]`。如果给定多个项作为参数，调用`f(obj)`返回一个包含`(obj[item], obj[item2], ..., obj[itemN])`的元组。

```
methodcaller(name [, *args [, **kwargs]])
```

创建一个可调用对象f，其中调用`f(obj)`返回`obj.name(*args, **kwargs)`。

这些函数对于优化涉及回调函数的操作性能也非常有用，尤其是那些涉及常见数据处理操作（如排序）的操作。例如，如果你想根据第2列对一个元组列表`rows`进行排序，你可以使用`sorted(rows, key=lambda r: r[2])`或使用`sorted(rows, key=itemgetter(2))`。第二个版本运行得快得多，因为它避免了与`lambda`相关的开销。

## 16

## 字符串和文本处理

本章描述了与基本字符串和文本处理相关的最常用Python模块。本章的重点是最常见的字符串操作，如处理文本、正则表达式模式匹配和文本格式化。

#### codecs

codecs模块用于处理Unicode文本I/O中使用的不同字符编码。该模块既用于定义新的字符编码，也用于使用各种现有编码（如UTF-8、UTF-16等）处理字符数据。程序员更常见的是直接使用现有编码之一，因此这里讨论的就是这些。如果你想创建新的编码，请查阅在线文档以获取更多详细信息。

##### 低级codecs接口

每种字符编码都被分配了一个通用名称，如`'utf-8'`或`'big5'`。以下函数用于执行查找。

```
lookup(encoding)
```

在编解码器注册表中查找一个编解码器。*encoding*是一个字符串，如`'utf-8'`。如果对请求的编码一无所知，则会引发`LookupError`。否则，返回一个`CodecInfo`实例*c*。

`CodecInfo`实例*c*具有以下方法：

```
c.encode(s [, errors])
```

一个无状态编码函数，它对Unicode字符串*s*进行编码，并返回一个元组`(bytes, length_consumed)`。*bytes*是一个包含编码数据的8位字符串或字节数组。*length_consumed*是*s*中被编码的字符数。*errors*是错误处理策略，默认设置为`'strict'`。

```
c.decode(bytes [, errors])
```

一个无状态编码函数，它对字节字符串*bytes*进行解码，并返回一个元组`(s, length_consumed)`。*s*是一个Unicode字符串，*length_consumed*是在解码过程中*bytes*中被消耗的字节数。*errors*是错误处理策略，默认设置为`'strict'`。

```
c.streamreader(bytestream [, errors])
```

返回一个`StreamReader`实例，用于读取编码数据。*bytestream*是一个以二进制模式打开的文件类对象。*errors*是错误处理策略，默认为`'strict'`。`StreamReader`的实例`r`支持以下低级I/O操作：

| 方法 | 描述 |
|--------|-------------|
| `r.read([size [, chars [, firstline]]])` | 返回最多*chars*个解码文本字符。*size*是从低级字节流读取的最大字节数，用于控制内部缓冲。*firstline*是一个标志，如果设置，即使文件稍后发生解码错误也会返回第一行。 |
| `r.readline([size [, keepends]])` | 返回单行解码文本。*keepends*是一个标志，控制是否保留行尾（默认为true）。 |
| `r.readlines([size [, keepends]])` | 将所有行读入一个列表。 |
| `r.reset()` | 重置内部缓冲区和状态。 |

```
c.streamwriter(bytestream [, errors])
```

返回一个`StreamWriter`实例，用于写入编码数据。*bytestream*是一个以字节模式打开的文件类对象。*errors*是错误处理策略，默认为`'strict'`。`StreamWriter`的实例`w`支持以下低级I/O操作：

| 方法 | 描述 |
|--------|-------------|
| `w.write(s)` | 写入字符串*s*的编码表示 |
| `w.writelines(lines)` | 将*lines*中的字符串列表写入文件 |
| `w.reset()` | 重置内部缓冲区和状态 |

```
c.incrementalencoder([errors])
```

返回一个`IncrementalEncoder`实例，可用于分多步编码字符串。*errors*默认为`'strict'`。`IncrementalEncoder`的实例`e`具有以下方法：

| 方法 | 描述 |
|--------|-------------|
| `e.encode(s [, final])` | 以字节字符串形式返回字符串*s*的编码表示。*final*是一个标志，应在最后一次调用`encode()`时设置为`True`。 |
| `e.reset()` | 重置内部缓冲区和状态。 |

###### codec.incrementaldecoder(errors)

返回一个 `IncrementalDecoder` 实例，可用于分步解码字节字符串。errors 默认为 `'strict'`。`IncrementalDecoder` 的实例 `d` 具有以下方法：

| 方法 | 描述 |
| --- | --- |
| d.decode(bytes [,final]) | 从 bytes 中的编码字节返回一个解码后的字符串。final 是一个标志，在最后一次调用 decode() 时应设置为 True。 |
| d.reset() | 重置内部缓冲区和状态。 |

###### 与I/O相关的函数

codecs模块提供了一组高级函数，用于简化涉及编码文本的I/O操作。大多数程序员会使用这些函数之一，而不是第一节中描述的低级codecs接口。

```
open(filename, mode[, encoding[, errors[, buffering]]])
```

以给定模式打开 filename，并根据 encoding 参数指定的编码提供透明的数据编码/解码。errors 是 `'strict'`、`'ignore'`、`'replace'`、`'backslashreplace'` 或 `'xmlcharrefreplace'` 之一。默认值是 `'strict'`。buffering 与内置 `open()` 函数的含义相同。无论在 mode 中指定了什么模式，底层文件始终以二进制模式打开。在 Python 3 中，你可以使用内置的 `open()` 函数替代 `codecs.open()`。

```
EncodedFile(file, inputenc[, outputenc [, errors]])
```

一个类，为现有的文件对象 `file` 提供一个编码包装器。写入文件的数据首先根据输入编码 inputenc 进行解释，然后使用输出编码 outputenc 写入文件。从文件读取的数据根据 inputenc 进行解码。如果省略 outputenc，则默认为 inputenc。errors 与 `open()` 的含义相同，默认为 `'strict'`。

```
iterencode(iterable, encoding [, errors])
```

一个生成器函数，将 iterable 中的所有字符串增量编码为指定编码。errors 默认为 `'strict'`。

```
iterdecode(iterable, encoding [, errors])
```

一个生成器函数，根据指定的编码增量解码 iterable 中的所有字节字符串。errors 默认为 `'strict'`。

###### 有用的常量

codecs 定义了以下字节序标记常量，可用于在你对底层编码一无所知时帮助解释文件。这些字节序标记有时写在文件开头以指示其字符编码，并可用于选择要使用的合适编码器。

| 常量 | 描述 |
| --- | --- |
| BOM | 机器的本机字节序标记 (BOM_BE 或 BOM_LE) |
| BOM_BE | 大端字节序标记 ('\xfe\xff') |
| BOM_LE | 小端字节序标记 ('\xff\xfe') |
| BOM_UTF8 | UTF-8 标记 ('\xef\xbb\xbf') |
| BOM_UTF16_BE | 16位 UTF-16 大端标记 ('\xfe\xff') |
| BOM_UTF16_LE | 16位 UTF-16 小端标记 ('\xff\xfe') |
| BOM_UTF32_BE | 32位 UTF-32 大端标记 ('\x00\x00\xfe\xff') |
| BOM_UTF32_LE | 32位 UTF-32 小端标记 ('\xff\xfe\x00\x00') |

###### 标准编码

以下是一些最常用字符编码的列表。编码名称是你在指定编码时传递给 `open()` 或 `lookup()` 等函数的名称。完整的编码列表可以在 codecs 模块的在线文档中找到 (http://docs.python.org/library/codecs)。

| 编码器名称 | 描述 |
| --- | --- |
| ascii | 7位 ASCII 字符 |
| cp437 | 来自 MS-DOS 的扩展 ASCII 字符集 |
| cp1252 | 来自 Windows 的扩展 ASCII 字符集 |
| latin-1, iso-8859-1 | 用拉丁字符扩展的 ASCII |
| utf-16 | UTF-16 |
| utf-16-be | UTF-16 大端 |
| utf-16-le | UTF-16 小端 |
| utf-32 | UTF-32 |
| utf-32-be | UTF-32 大端 |
| utf-32-le | UTF-32 小端 |
| utf-8 | UTF-8 |

###### 备注

-   关于 codecs 模块的进一步使用，请参见第9章“输入和输出”。
-   有关如何创建新字符编码的信息，请参阅在线文档。
-   需要特别注意 `encode()` 和 `decode()` 操作的输入。所有 `encode()` 操作都应传入 Unicode 字符串，所有 `decode()` 操作都应传入字节字符串。Python 2 在这方面并不完全一致，而 Python 3 则严格强制字符串之间的区分。例如，Python 2 有一些将字节字符串映射到字节字符串的编码器（例如 "bz2" 编码器）。这些在 Python 3 中不可用，如果你关心兼容性，就不应该使用它们。

#### re

`re` 模块用于执行字符串中的正则表达式模式匹配和替换。支持 unicode 和字节字符串。正则表达式模式被指定为包含文本和特殊字符序列混合的字符串。由于模式经常大量使用特殊字符和反斜杠，它们通常被写成“原始”字符串，例如 `r'(?P<int>\d+)\.(\d*)'`。在本节的剩余部分中，所有正则表达式模式都使用原始字符串语法表示。

##### 模式语法

正则表达式模式中识别以下特殊字符序列：

| 字符 | 描述 |
| --- | --- |
| `text` | 匹配字面字符串 `text`。 |
| `.` | 匹配除换行符外的任何字符。 |
| `^` | 匹配字符串的开头。 |
| `$` | 匹配字符串的末尾。 |
| `*` | 匹配前一个表达式的零次或多次重复，匹配尽可能多的重复。 |
| `+` | 匹配前一个表达式的一次或多次重复，匹配尽可能多的重复。 |
| `?` | 匹配前一个表达式的零次或一次重复。 |
| `*?` | 匹配前一个表达式的零次或多次重复，匹配尽可能少的重复。 |
| `+?` | 匹配前一个表达式的一次或多次重复，匹配尽可能少的重复。 |
| `??` | 匹配前一个表达式的零次或一次重复，匹配尽可能少的重复。 |
| `{m}` | 恰好匹配前一个表达式的 *m* 次重复。 |
| `{m, n}` | 匹配前一个表达式的 *m* 到 *n* 次重复，匹配尽可能多的重复。如果 *m* 省略，则默认为 0。如果 *n* 省略，则默认为无穷大。 |
| `{m, n}?` | 匹配前一个表达式的 *m* 到 *n* 次重复，匹配尽可能少的重复。 |
| `[...]` | 匹配一组字符，例如 `r'[abcdef]'` 或 `r'[a-zA-z]'`。特殊字符如 `*` 在集合内不活跃。 |
| `[^...]` | 匹配不在集合中的字符，例如 `r'[^0-9]'`。 |
| `A\|B` | 匹配 `A` 或 `B`，其中 `A` 和 `B` 都是正则表达式。 |
| `(...)` | 将括号内的正则表达式作为一组匹配并保存匹配的子字符串。可以通过在匹配时获得的 `MatchObject` 对象的 `group()` 方法获取组的内容。 |
| (?aiLmsux) | 将字母 "a"、"i"、"L"、"m"、"s"、"u" 和 "x" 解释为对应于传递给 re.compile() 的 re.A、re.I、re.L、re.M、re.S、re.U、re.X 标志设置的标志设置。"a" 仅在 Python 3 中可用。 |
| (?:...) | 匹配括号内的正则表达式，但丢弃匹配的子字符串。 |
| (?P<name>...) | 匹配括号内的正则表达式并创建一个命名组。组名必须是有效的 Python 标识符。 |
| (?P=name) | 匹配与先前命名组匹配的相同文本。 |
| (?#...) | 注释。括号内的内容被忽略。 |
| (?=...) | 仅当前面的表达式后面跟着括号中的模式时才匹配。例如，r'Hello (?=World)' 仅在后面跟着 'World' 时匹配 'Hello '。 |
| (?!...) | 仅当前面的表达式后面不跟括号中的模式时才匹配。例如，r'Hello (?!World)' 仅在后面不跟 'World' 时匹配 'Hello '。 |
| (?<=...) | 仅当前面的表达式前面是括号中模式的匹配时才匹配后面的表达式。例如，r'(?<=abc)def' 仅在前面是 'abc' 时匹配 'def'。 |
| (?<!...) | 仅当前面的表达式前面不是括号中模式的匹配时才匹配后面的表达式。例如，r'(?<!abc)def' 仅在前面不是 'abc' 时匹配 'def'。 |
| (?(id\|name)ypat\|npat) | 检查由 id 或 name 标识的正则表达式组是否存在。如果存在，则匹配正则表达式 ypat。如果不存在，则匹配可选表达式 npat。例如，模式 r'(Hello)?(?(1)World\|Howdy)' 匹配字符串 'Hello World' 或字符串 'Howdy'。 |

标准字符转义序列如 `'\\n'` 和 `'\\t'` 在正则表达式中被识别为标准字符（例如，r'\\n+' 将匹配一个或多个换行符）。此外，通常在正则表达式中具有特殊含义的字面符号可以通过在其前面加上反斜杠来指定。例如，r'\\*' 匹配字符 *。此外，一些反斜杠序列对应于特殊的字符集：

| 字符 | 描述 |
| --- | --- |
| \\number | 匹配由先前组号匹配的文本。组从左到右编号，从 1 到 99。 |
| \\A | 仅在字符串开头匹配。 |
| \\b | 匹配单词开头或结尾的空字符串。单词是由空白或任何其他非字母数字字符终止的字母数字字符序列。 |



##### 字符说明
\b 匹配一个不是单词开头或结尾的空字符串。
\d 匹配任意十进制数字。等同于 r'[0-9]'。
\D 匹配任意非数字字符。等同于 r'[^0-9]'。
\s 匹配任意空白字符。等同于 r'[\t\n\r\f\v]'。
\S 匹配任意非空白字符。等同于 r'[^ \t\n\r\f\v]'。
\w 匹配任意字母数字字符。
\W 匹配任意不属于 \w 所定义集合的字符。
\Z 仅在字符串末尾匹配。
\\ 匹配一个字面反斜杠。

在匹配 Unicode 字符串时，特殊字符 \d、\D、\s、\S、\w 和 \W 的解释方式会有所不同。在这种情况下，它们匹配所有符合所描述属性的 Unicode 字符。例如，\d 匹配任何被归类为数字的 Unicode 字符，例如欧洲数字、阿拉伯数字和印度数字，它们各自占据 Unicode 字符的不同范围。

##### 函数

以下函数用于执行模式匹配和替换：

`compile(str [, flags])`

将正则表达式模式字符串编译成一个正则表达式对象。该对象可以作为后续所有函数的 pattern 参数传递。该对象还提供了一些方法，这些方法将稍后描述。`flags` 是以下标志的按位或运算结果：

**标志说明**
A 或 ASCII 仅执行 8 位 ASCII 匹配（仅限 Python 3）。
I 或 IGNORECASE 执行不区分大小写的匹配。
L 或 LOCALE 使用区域设置对 \w、\W、\b 和 \B 进行解释。
M 或 MULTILINE 使得 ^ 和 $ 除了应用于整个字符串的开头和结尾外，也应用于每一行。（通常 ^ 和 $ 仅应用于整个字符串的开头和结尾。）
S 或 DOTALL 使得点（.）字符匹配所有字符，包括换行符。
U 或 UNICODE 使用 Unicode 字符属性数据库中的信息来处理 \w、\W、\b 和 \B。（仅限 Python 2。Python 3 默认使用 Unicode。）
X 或 VERBOSE 忽略模式字符串中未转义的空白字符和注释。

`escape(string)`

返回一个字符串，其中所有非字母数字字符都被转义。

`findall(pattern, string [, flags])`

返回 `string` 中所有非重叠的 `pattern` 匹配项的列表，包括空匹配。如果模式包含分组，则返回每个分组匹配的文本列表。

如果使用了多个分组，列表中的每个元素是一个元组，包含每个分组匹配的文本。`flags` 的含义与 `compile()` 中的相同。

`finditer(pattern, string [, flags])`

与 `findall()` 相同，但返回一个迭代器对象。该迭代器返回 `MatchObject` 类型的项。

`match(pattern, string [, flags])`

检查 `string` 开头的零个或多个字符是否匹配 `pattern`。成功时返回 `MatchObject`，否则返回 `None`。`flags` 的含义与 `compile()` 中的相同。

`search(pattern, string [, flags])`

在 `string` 中搜索 `pattern` 的第一个匹配项。`flags` 的含义与 `compile()` 中的相同。成功时返回 `MatchObject`，如果未找到匹配项则返回 `None`。

`split(pattern, string [, maxsplit = 0])`

根据 `pattern` 的出现拆分 `string`。返回一个字符串列表，包括模式中任何分组匹配的文本。`maxsplit` 是要执行的最大拆分数。默认情况下，执行所有可能的拆分。

`sub(pattern, repl, string [, count = 0])`

使用替换字符串 `repl` 替换 `string` 中最左侧的非重叠 `pattern` 匹配项。`repl` 可以是字符串或函数。如果是函数，则使用 `MatchObject` 调用，并应返回替换字符串。如果 `repl` 是字符串，则使用反向引用（如 `'\6'`）来引用模式中的分组。序列 `'\g<name>'` 用于引用命名分组。`count` 是要执行的最大替换次数。默认情况下，替换所有匹配项。虽然这些函数不像 `compile()` 那样接受 `flags` 参数，但可以通过使用本节前面描述的 `(?iLmsux)` 表示法来达到相同的效果。

`subn(pattern, repl, string [, count = 0])`

与 `sub()` 相同，但返回一个元组，包含新字符串和替换次数。

##### 正则表达式对象

由 `compile()` 函数创建的已编译正则表达式对象 `r` 具有以下方法和属性：

`r.flags`

编译正则表达式对象时使用的 `flags` 参数，如果未指定标志则为 `0`。

`r.groupindex`

一个字典，将由 `r'(?P<id>)'` 定义的符号组名映射到组号。

`r.pattern`

用于编译正则表达式对象的模式字符串。

`r.findall(string [, pos [, endpos]])`

与 findall() 函数相同。pos 和 endpos 指定搜索的起始和结束位置。

`r.finditer(string [, pos [, endpos]])`

与 finditer() 函数相同。pos 和 endpos 指定搜索的起始和结束位置。

`r.match(string [, pos] [, endpos])`

检查字符串开头的零个或多个字符是否匹配。pos 和 endpos 指定要搜索的字符串范围。匹配成功时返回 MatchObject，否则返回 None。

`r.search(string [, pos [, endpos])`

搜索字符串以查找匹配项。pos 和 endpos 指定搜索的起始和结束位置。匹配成功时返回 MatchObject，否则返回 None。

`r.split(string [, maxsplit = 0])`

与 split() 函数相同。

`r.sub(repl, string [, count = 0])`

与 sub() 函数相同。

`r.subn(repl, string [, count = 0])`

与 subn() 函数相同。

##### 匹配对象

`search()` 和 `match()` 返回的 MatchObject 实例包含有关分组内容以及匹配发生位置的位置数据信息。MatchObject 实例 `m` 具有以下方法和属性：

`m.expand(template)`

返回一个字符串，该字符串是通过对字符串 template 进行正则表达式反斜杠替换获得的。数字反向引用（如 "\1" 和 "\2"）和命名引用（如 "\g<n>" 和 "\g<name>"）将被相应分组的内容替换。请注意，这些序列应使用原始字符串或字面反斜杠字符指定，例如 r'\1' 或 '\\1'。

`m.group([group1, group2, ...])`

返回匹配的一个或多个子组。参数指定组号或组名。如果未指定组名，则返回整个匹配项。如果只指定一个组，则返回包含该组匹配文本的字符串。否则，返回一个元组，包含每个请求组匹配的文本。如果给出的组号或组名无效，则引发 IndexError。

`m.groups([default])`

返回一个元组，包含模式中所有组匹配的文本。default 是未参与匹配的组返回的值（默认值为 None）。

`m.groupdict([default])`

返回一个字典，包含匹配的所有命名子组。*default* 是未参与匹配的组返回的值（默认值为 None）。

`m.start([group])`
`m.end([group])`

这两个方法返回由组匹配的子串的开始和结束索引。如果省略 *group*，则使用整个匹配的子串。如果组存在但未参与匹配，则返回 None。

`m.span([group])`

返回一个二元组 (*m.start(group)*, *m.end(group)*)。如果 *group* 未对匹配做出贡献，则返回 (None, None)。如果省略 *group*，则使用整个匹配的子串。

`m.pos`

传递给 search() 或 match() 函数的 *pos* 的值。

`m.endpos`

传递给 search() 或 match() 函数的 *endpos* 的值。

`m.lastindex`

最后匹配的组的数字索引。如果没有组被匹配，则为 None。

`m.lastgroup`

最后匹配的命名组的名称。如果没有命名组被匹配或模式中不存在命名组，则为 None。

`m.re`

产生此 MatchObject 实例的 match() 或 search() 方法所属的正则表达式对象。

`m.string`

传递给 match() 或 search() 的字符串。

##### 示例

以下示例展示了如何使用 re 模块来搜索、从字符串中提取数据以及替换文本模式。

```python
import re
text = "Guido will be out of the office from 12/15/2012 - 1/3/2013."

###### 用于匹配日期的正则表达式模式。
datepat = re.compile('(\d+)/(\d+)/(\d+)')

###### 查找并打印所有日期
for m in datepat.finditer(text):
    print(m.group())
```



###### 查找所有日期，但以不同格式打印

```
monthnames = [None,'Jan','Feb','Mar','Apr','May','Jun',
              'Jul','Aug','Sep','Oct','Nov','Dec']

for m in datepat.finditer(text):
    print ("%s %s, %s" % (monthnames[int(m.group(1))], m.group(2), m.group(3)))

###### 将所有日期替换为欧洲格式（日/月/年）
def fix_date(m):
    return "%s/%s/%s" % (m.group(2),m.group(1),m.group(3))
newtext = datepat.sub(fix_date, text)

###### 另一种替换方式
newtext = datepat.sub(r'\2/\1/\3', text)
```

##### 注意事项

-   关于正则表达式的理论和实现的详细信息，可以在编译器构造的教科书中找到。Jeffrey Friedl 的 *Mastering Regular Expressions*（O'Reilly & Associates, 1997）一书也可能有用。
-   使用 `re` 模块最困难的部分是编写正则表达式模式。编写模式时，可以考虑使用 Kodos (http://kodos.sourceforge.net) 之类的工具。

#### 字符串

`string` 模块包含许多用于操作字符串的有用常量和函数。它还包含用于实现新字符串格式化器的类。

##### 常量

以下常量定义了在各种字符串操作中可能有用的不同字符集。

| 常量 | 描述 |
| --- | --- |
| ascii_letters | 包含所有小写和大写 ASCII 字母的字符串。 |
| ascii_lowercase | 字符串 'abcdefghijklmnopqrstuvwxyz'。 |
| ascii_uppercase | 字符串 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'。 |
| digits | 字符串 '0123456789'。 |
| hexdigits | 字符串 '0123456789abcdefABCDEF'。 |
| letters | 小写和大写的连接。 |
| lowercase | 包含当前区域设置特有的所有小写字母的字符串。 |
| octdigits | 字符串 '01234567'。 |
| punctuation | ASCII 标点字符字符串。 |
| printable | 可打印字符字符串——字母、数字、标点和空白字符的组合。 |
| uppercase | 包含当前区域设置特有的所有大写字母的字符串。 |
| whitespace | 包含所有空白字符的字符串。这通常包括空格、制表符、换行符、回车符、换页符和垂直制表符。 |

请注意，其中一些常量（例如，`letters` 和 `uppercase`）会因系统的区域设置而异。

##### 格式化器对象

字符串的 `str.format()` 方法用于执行高级字符串格式化操作。如第 3 章“类型和对象”和第 4 章“运算符和表达式”中所示，此方法可以访问序列或映射的项、对象的属性以及其他相关操作。`string` 模块定义了一个 `Formatter` 类，可用于实现自定义的格式化操作。此类公开了实现字符串格式化操作的部分，并允许你对其进行自定义。

```
Formatter()
```

创建一个新的 `Formatter` 实例。`Formatter` 的实例 `f` 支持以下操作。

```
f.format(format_string, *args, **kwargs)
```

格式化字符串 `format_string`。默认情况下，输出与调用 `format_string.format(*args, **kwargs)` 相同。例如，`f.format("{name} is {0:d} years old", 39, name="Dave")` 创建字符串 "Dave is 39 years old"。

```
f.vformat(format_string, args, kwargs)
```

实际执行 `f.format()` 工作的方法。`args` 是位置参数的元组，`kwargs` 是关键字参数的字典。如果你已经将参数信息捕获到元组和字典中，这是一个更快的方法。

```
f.parse(format_string)
```

一个函数，用于创建迭代器以解析格式字符串 `format_string` 的内容。迭代器遍历格式字符串，并产生格式为 `(literal_text, field_name, format_spec, conversion)` 的元组。`literal_text` 是位于下一个包含在花括号 `{ ... }` 中的格式说明符之前的任何文本。如果没有前导文本，它可能是空字符串。`field_name` 是一个字符串，指定格式说明符中的字段名。例如，如果说明符是 `'{0:d}'`，则字段名为 `'0'`。`format_spec` 是冒号后出现的格式说明符——例如，前面示例中的 `'d'`。如果未指定，则为空字符串。`conversion` 是包含转换说明符（如果有）的字符串。在前面的示例中，它是 `None`，但如果说明符是 `'{0!s:d}'`，则它将被设置为 `'s'`。对于格式字符串的最后一个片段，`field_name`、`format_spec` 和 `conversion` 都将为 `None`。

```
f.get_field(fieldname, args, kwargs)
```

从 `args` 和 `kwargs` 中提取与给定 `fieldname` 关联的值。`fieldname` 是一个字符串，如前面所示的 `parse()` 方法返回的 `"0"` 或 `"name"`。返回一个元组 `(value, key)`，其中 `value` 是字段值，`key` 用于在 `args` 或 `kwargs` 中定位值。如果 `key` 是整数，则是 `args` 中的索引。如果是字符串，则是 `kwargs` 中使用的键。`fieldname` 可能包含额外的索引和属性查找，如 `'0.name'` 或 `'0[name]'`。在这种情况下，该方法执行额外的查找并返回相应的值。但是，返回元组中 `key` 的值只是被设置为 `'0'`。

**f.get_value(key, args, kwargs)**

从 *args* 或 *kwargs* 中提取与 *key* 对应的对象。如果 *key* 是整数，则对象取自 *args*。如果是字符串，则取自 *kwargs*。

**f.check_unused_args(used_args, args, kwargs)**

检查 `format()` 操作中未使用的参数。*used_args* 是在格式字符串中找到的所有已使用参数键（参见 `get_field()`）的集合。*args* 和 *kwargs* 是传递给 `format()` 的位置和关键字参数。默认行为是为未使用的参数引发 `TypeError`。

**f.format_value(value, format_spec)**

根据给定的格式规范格式化单个值。默认情况下，这仅仅执行内置函数 `format(value, format_spec)`。

**f.convert_field(value, conversion)**

根据指定的转换代码转换 `get_field()` 返回的 *value*。如果 *conversion* 为 `None`，则返回未修改的 *value*。如果转换为 `'s'` 或 `'r'`，则分别使用 `str()` 或 `repr()` 将 *value* 转换为字符串。

如果你想创建自定义的字符串格式化，可以创建一个 `Formatter` 对象，并简单地使用默认方法按需执行格式化。也可以定义一个继承自 `Formatter` 的新类，并重新实现前面显示的任何方法。

有关格式说明符语法和高级字符串格式化的详细信息，请参阅第 3 章和第 4 章。

##### 模板字符串

`string` 模块定义了一个新的字符串类型 `Template`，它简化了某些字符串替换。示例可以在第 9 章中找到。

以下创建一个新的模板字符串对象：

**Template(s)**

这里，*s* 是一个字符串，`Template` 被定义为一个类。

`Template` 对象 *t* 支持以下方法：

**t.substitute(m [, **kwargs])**

此方法接受一个映射对象 *m*（例如，字典）或关键字参数列表，并对字符串 *t* 执行关键字替换。此替换将字符串 `'$$'` 替换为单个 `'$'`，并将字符串 `'$key'` 或 `'${key}'` 替换为 `m['key']` 或 `kwargs['key']`（如果提供了关键字参数）。*key* 必须拼写为有效的 Python 标识符。如果最终字符串包含任何未解析的 `'$key'` 模式，则会引发 `KeyError` 异常。

**t.safe_substitute(m [, **kwargs])**

与 `substitute()` 相同，只是不会产生异常或错误。相反，未解析的 `$key` 引用将保持原样留在字符串中。

**t.template**

包含传递给 `Template()` 的原始字符串。

`Template` 类的行为可以通过子类化它并重新定义属性 `delimiter` 和 `idpattern` 来修改。例如，此代码将转义字符 `$` 更改为 `@` 并将键名限制为仅字母：

```python
class MyTemplate(string.Template):
    delimiter = '@'      # 转义序列的字面字符
    idpattern = '[A-Z]*'  # 标识符正则表达式模式
```

##### 实用函数

`string` 模块还定义了一些操作字符串的函数，这些函数未定义为字符串对象上的方法。

**capwords(s)**

将 *s* 中每个单词的首字母大写，用单个空格替换重复的空白字符，并删除前导和尾随空白。

**maketrans(from, to)**

创建一个转换表，将 `from` 中的每个字符映射到 `to` 中相同位置的字符。`from` 和 `to` 必须长度相同。此函数用于创建适合与字符串的 `translate()` 方法一起使用的参数。

#### 结构体

`struct` 模块用于在 Python 和二进制数据结构（表示为 Python 字节字符串）之间转换数据。当与用 C 编写的函数、二进制文件格式、网络协议或通过串行端口的二进制通信交互时，通常会使用这些数据结构。

##### 打包和解包函数

以下模块级函数用于在字节字符串中打包和解包数据。如果你的程序反复执行这些操作，请考虑使用下一节中描述的 `Struct` 对象。

**pack(fmt, v1, v2, ...)**

根据 `fmt` 中的格式字符串，将值 `v1`、`v2` 等打包成一个字节字符串。

**pack_into(fmt, buffer, offset, v1, v2, ...)**

将值 `v1`、`v2` 等打包到可写缓冲区对象 *buffer* 中，从字节偏移量 *offset* 开始。这仅适用于支持缓冲区接口的对象。示例包括 `array.array` 和 `bytearray` 对象。

**unpack(fmt, string)**

根据 `fmt` 中的格式字符串解包字节 *string* 的内容。返回解包值的元组。*string* 的长度必须与 `calcsize()` 函数确定的格式大小完全匹配。

`unpack_from(fmt, buffer, offset)`

根据 *fmt* 中的格式字符串，从偏移量 *offset* 开始，解包 `buffer` 对象的内容。返回一个包含已解包值的元组。

`calcsize(fmt)`

计算与格式字符串 *fmt* 对应的结构的大小（以字节为单位）。

##### Struct 对象

`struct` 模块定义了一个名为 `Struct` 的类，它提供了打包和解包的替代接口。使用此类效率更高，因为格式字符串只会被解释一次。

`Struct(fmt)`

创建一个 `Struct` 实例，表示根据给定格式代码打包的数据。`Struct` 的一个实例 *s* 具有以下方法，其工作方式与上一节描述的函数完全相同：

| 方法 | 描述 |
|---|---|
| `s.pack(v1, v2, ...)` | 将值打包为字节字符串 |
| `s.pack_into(buffer, offset, v1, v2, ...)` | 将值打包到缓冲区对象中 |
| `s.unpack(bytes)` | 从字节字符串中解包值 |
| `s.unpack_from(buffer, offset)` | 从缓冲区对象中解包值 |
| `s.format` | 正在使用的格式代码 |
| `s.size` | 格式的大小（以字节为单位） |

###### 格式代码

`struct` 模块中使用的格式字符串是具有以下含义的字符序列：

| 格式 | C 类型 | Python 类型 |
|---|---|---|
| `'x'` | 填充字节 | 无值 |
| `'c'` | 字符 | 长度为 1 的字符串 |
| `'b'` | 有符号字符 | 整数 |
| `'B'` | 无符号字符 | 整数 |
| `'?'` | _Bool (C99) | 布尔值 |
| `'h'` | 短整型 | 整数 |
| `'H'` | 无符号短整型 | 整数 |
| `'i'` | 整型 | 整数 |
| `'I'` | 无符号整型 | 整数 |
| `'l'` | 长整型 | 整数 |
| `'L'` | 无符号长整型 | 整数 |
| `'q'` | 长长整型 | 长整数 |
| `'Q'` | 无符号长长整型 | 长整数 |
| `'f'` | 单精度浮点数 | 浮点数 |
| `'d'` | 双精度浮点数 | 浮点数 |
| `'s'` | char[] | 字符串 |
| `'p'` | char[] | 字符串，长度编码在第一个字节中 |
| `'P'` | void * | 整数 |

每个格式字符前面都可以加上一个整数来表示重复次数（例如，'4i' 与 'iiii' 相同）。对于 's' 格式，计数表示字符串的最大长度，因此 '10s' 表示一个 10 字节的字符串。格式 '0s' 表示长度为零的字符串。'p' 格式用于编码一个长度出现在第一个字节中，后面是字符串数据的字符串。这在处理 Pascal 代码时很有用，有时在 Macintosh 上就需要这样做。请注意，这种情况下字符串的长度限制为 255 个字符。

当使用 'I' 和 'L' 格式解包一个值时，返回值是一个 Python 长整数。此外，'P' 格式可能返回一个整数或长整数，具体取决于机器的字长。

每个格式字符串的第一个字符还可以指定打包数据的字节顺序和对齐方式，如下所示：

| 格式 | 字节顺序 | 大小和对齐 |
|--------|-----------|-------------------|
| '@' | 原生 | 原生 |
| '=' | 原生 | 标准 |
| '<' | 小端 | 标准 |
| '>' | 大端 | 标准 |
| '!' | 网络（大端） | 标准 |

原生字节顺序可能是小端或大端，具体取决于机器架构。原生大小和对齐对应于 C 编译器使用的值，并且是特定于实现的。标准对齐假定任何类型都不需要对齐。标准大小假定 short 为 2 字节，int 为 4 字节，long 为 4 字节，float 为 32 位，double 为 64 位。'P' 格式只能使用原生字节顺序。

###### 注意

- 有时需要将结构的末尾对齐到特定类型的对齐要求。为此，将结构格式字符串以该类型的代码（重复次数为零）结尾。例如，格式 'llh0l' 指定一个结构在 4 字节边界上结束（假设 long 对齐在 4 字节边界上）。在这种情况下，'h' 代码指定的 short 值之后将插入两个填充字节。这仅在使用原生大小和对齐时有效——标准大小和对齐不强制执行对齐规则。
- 'q' 和 'Q' 格式仅在用于构建 Python 的 C 编译器支持 long long 数据类型时，才在“原生”模式下可用。

另请参阅：

array (第 259 页), ctypes (第 612 页)

#### unicodedata

unicodedata 模块提供对 Unicode 字符数据库的访问，该数据库包含所有 Unicode 字符的属性。

##### bidirectional(unichr)

返回分配给 *unichr* 的双向类别字符串，如果未定义该值，则返回空字符串。返回以下之一：

| 值 | 描述 |
|-------|-------------|
| L | 从左到右 |
| LRE | 从左到右嵌入 |
| LRO | 从左到右覆盖 |
| R | 从右到左 |
| AL | 从右到左（阿拉伯语） |
| RLE | 从右到左嵌入 |
| RLO | 从右到左覆盖 |
| PDF | 弹出方向格式 |
| EN | 欧洲数字 |
| ES | 欧洲数字分隔符 |
| ET | 欧洲数字终止符 |
| AN | 阿拉伯数字 |
| CS | 通用数字分隔符 |
| NSM | 非间距标记 |
| BN | 边界中性符 |
| B | 段落分隔符 |
| S | 段分隔符 |
| WS | 空白符 |
| ON | 其他中性符 |

##### category(unichr)

返回一个描述 *unichr* 通用类别的字符串。返回的字符串是以下值之一：

| 值 | 描述 |
|-------|-------------|
| Lu | 字母，大写 |
| Ll | 字母，小写 |
| Lt | 字母，首字母大写 |
| Mn | 标记，非间距 |
| Mc | 标记，间距组合 |
| Me | 标记，包围 |
| Nd | 数字，十进制数字 |
| Nl | 数字，字母 |
| No | 数字，其他 |
| Zs | 分隔符，空格 |
| Zl | 分隔符，行 |
| Zp | 分隔符，段落 |
| Cc | 其他，控制符 |
| Cf | 其他，格式符 |
| Cs | 其他，代理项 |
| Co | 其他，私用区 |
| Cn | 其他，未分配 |
| Lm | 字母，修饰符 |
| Lo | 字母，其他 |
| Pc | 标点，连接符 |
| Pd | 标点，破折号 |
| Ps | 标点，开括号 |
| Pe | 标点，闭括号 |
| Pi | 标点，左引号 |
| Pf | 标点，右引号 |
| Po | 标点，其他 |
| Sm | 符号，数学 |
| Sc | 符号，货币 |
| Sk | 符号，修饰符 |
| So | 符号，其他 |

##### combining(unichr)

返回一个整数，描述 *unichr* 的组合类，如果未定义组合类，则返回 0。返回以下值之一：

| 值 | 描述 |
|-------|-------------|
| 0 | 间距、分割、包围、重排序和藏文下加字 |
| 1 | 叠加和内部 |
| 7 | Nuktas |
| 8 | 平假名/片假名浊音标记 |
| 9 | Viramas |
| 10–199 | 固定位置类 |
| 200 | 左下附加 |
| 202 | 下方附加 |
| 204 | 右下附加 |
| 208 | 左侧附加 |
| 210 | 右侧附加 |
| 212 | 左上附加 |
| 214 | 上方附加 |
| 216 | 右上附加 |
| 218 | 左下方 |
| 220 | 下方 |
| 222 | 右下方 |
| 224 | 左侧 |
| 226 | 右侧 |
| 228 | 左上方 |
| 230 | 上方 |
| 232 | 右上方 |
| 233 | 双下标 |
| 234 | 双上标 |
| 240 | 下方（iota 下标） |

`decimal(unichr[, default])`

返回分配给字符 *unichr* 的十进制整数值。如果 *unichr* 不是十进制数字，则返回 *default* 或引发 `ValueError`。

`decomposition(unichr)`

返回一个包含 *unichr* 分解映射的字符串，如果未定义该映射，则返回空字符串。通常，包含重音符号的字符可以分解为多字符序列。例如，`decomposition(u"\u00fc")`（"ü"）返回字符串 `"0075 0308"`，对应于字母 *u* 和分音符（¨）重音符号。此函数返回的字符串也可能包含以下字符串：

| 值 | 描述 |
|-------|-------------|
| `<font>` | 字体变体（例如，黑体形式） |
| `<noBreak>` | 空格或连字符的不断行版本 |
| `<initial>` | 初始显示形式（阿拉伯语） |
| `<medial>` | 中间显示形式（阿拉伯语） |
| `<final>` | 最终显示形式（阿拉伯语） |
| `<isolated>` | 独立显示形式（阿拉伯语） |
| `<circle>` | 圈形形式 |
| `<super>` | 上标形式 |
| `<sub>` | 下标形式 |
| `<vertical>` | 垂直布局显示形式 |
| `<wide>` | 宽（或全角）兼容字符 |
| `<narrow>` | 窄（或半角）兼容字符 |
| `<small>` | 小型变体形式（CNS 兼容） |
| `<square>` | CJK 方块字体变体 |
| `<fraction>` | 普通分数形式 |
| `<compat>` | 其他未指定的兼容字符 |

`digit(unichr[, default])`

返回分配给字符 *unichr* 的整数数字值。如果 *unichr* 不是数字，则返回 *default* 或引发 `ValueError`。此函数不同于



### Python 数据库访问

本章描述了 Python 用于连接关系型和哈希表样式数据库的编程接口。与其他描述特定库模块的章节不同，本章的部分内容也适用于第三方扩展。例如，如果你想让 Python 连接到 MySQL 或 Oracle 数据库，你首先需要下载一个第三方扩展模块。该模块反过来将遵循此处描述的基本约定。

#### 关系型数据库 API 规范

为了访问关系型数据库，Python 社区开发了一个称为 *Python Database API Specification V2.0* 的标准，简称 PEP 249（正式描述可在 http://www.python.org/dev/peps/pep-249/ 找到）。具体的数据库模块（例如 MySQL、Oracle 等）遵循此规范，但可能添加更多功能。本节涵盖了大多数应用中使用它所需的基本要素。

在高层次上，数据库 API 定义了一组函数和对象，用于连接到数据库服务器、执行 SQL 查询和获取结果。为此主要使用两个对象：一个管理数据库连接的 `Connection` 对象和一个用于执行查询的 `Cursor` 对象。

###### 连接

要连接到数据库，每个数据库模块都提供一个模块级别的函数 `connect`（*参数*）。确切的参数取决于数据库，但通常包括诸如数据源名称、用户名、密码、主机名和数据库名称等信息。通常这些信息分别通过关键字参数 `dsn`、`user`、`password`、`host` 和 `database` 提供。因此，`connect()` 调用可能如下所示：

```
connect(dsn="hostname:DBNAME",user="michael",password="peekaboo")
```

如果成功，将返回一个 `Connection` 对象。`Connection` 的实例 `c` 具有以下方法：

```
c.close()
```
关闭与服务器的连接。

```
c.commit()
```
将所有未提交的事务提交到数据库。如果数据库支持事务，则必须调用此方法才能使更改生效。如果底层数据库不支持事务，则此方法不执行任何操作。

```
c.rollback()
```
将数据库回滚到任何未提交事务的开始状态。此方法有时在不支持事务的数据库中使用，以撤销对数据库所做的任何更改。例如，如果在更新数据库的代码中发生了异常，你可能会使用此方法来撤销异常发生之前所做的更改。

```
c.cursor()
```
创建一个使用该连接的新 `Cursor` 对象。游标是你将用于执行 SQL 查询和获取结果的对象。这将在下一节中描述。

#### 游标

为了在数据库上执行任何操作，你首先创建一个连接 *c*，然后调用 `c.cursor()` 方法来创建一个 `Cursor` 对象。游标 *cur* 的一个实例具有许多标准方法和属性，用于执行查询：

```
cur.callproc(procname [, parameters])
```
调用名为 *procname* 的存储过程。*parameters* 是一个值序列，用作过程的参数。此函数的结果是一个与 *parameters* 具有相同数量项目的序列。此序列是 *parameters* 的一个副本，其中任何输出参数的值已在执行后替换为其修改后的值。如果过程还产生一个输出集，则可以使用接下来描述的 `fetch*()` 方法读取它。

```
cur.close()
```
关闭游标，防止对其进行任何进一步操作。

```
cur.execute(query [, parameters])
```
在数据库上执行查询或命令 *query*。*query* 是一个包含命令（通常是 SQL）的字符串，*parameters* 是一个序列或映射，用于为查询字符串中的变量提供值（这在下一节中描述）。

```
cur.executemany(query [, parametersequence])
```
重复执行查询或命令。*query* 是查询字符串，*parametersequence* 是参数序列。此序列中的每一项都是一个序列或映射对象，你将使用之前显示的 `execute()` 方法。

```
cur.fetchone()
```
返回由 `execute()` 或 `executemany()` 产生的结果集的下一行。结果通常是一个列表或元组，包含结果不同列的值。如果没有更多可用行，则返回 `None`。如果没有待处理的结果或先前执行的操作未创建结果集，则会引发异常。

```
cur.fetchmany([size])
```
返回一个结果行序列（例如，元组列表）。*size* 是要返回的行数。如果省略，则使用 *cur.arraysize* 的值作为默认值。返回的实际行数可能少于请求的行数。如果没有更多可用行，则返回一个空序列。

```
cur.fetchall()
```
返回所有剩余结果行的序列（例如，元组列表）。

```
cur.nextset()
```
丢弃当前结果集中所有剩余的行，并跳转到下一个结果集（如果有的话）。如果没有更多结果集，则返回 *None*；否则，返回 *True* 值，并且后续的 `fetch*()` 操作将从新集合返回数据。

```
cur.setinputsize(sizes)
```
为后续的 `execute*()` 方法传递的参数给游标一个提示。*sizes* 是一个类型对象（稍后描述）或整数序列，为每个参数提供预期的最大字符串长度。在内部，这用于为发送到数据库的查询和命令预定义内存缓冲区。使用此方法可以加速后续的 `execute*()` 操作。

```
cur.setoutputsize(size [, column])
```
设置结果集中特定列的缓冲区大小。*column* 是结果行中的整数索引，*size* 是字节数。此方法的典型用法是在进行任何 `execute*()` 调用之前，对大型数据库列（如字符串、BLOBs 和 LONGs）设置限制。如果省略 *column*，则为结果中的所有列设置限制。

游标具有许多属性，用于描述当前结果集并提供有关游标本身的信息。

```
cur.arraysize
```
一个整数，给出 `fetchmany()` 操作使用的默认值。此值可能因数据库模块而异，并且可能最初设置为模块认为“最佳”的值。

```
cur.description
```
一个元组序列，提供有关当前结果集中每一列的信息。每个元组的形式为（name, type_code, display_size, internal_size, precision, scale, null_ok）。第一个字段始终定义，并对应于列名。*type_code* 可用于涉及“类型对象”部分中描述的类型对象的比较。如果其他字段不适用于该列，则可能设置为 *None*。

```
cur.rowcount
```
由其中一个 `execute*()` 方法产生的上一个结果中的行数。如果设置为 -1，则表示没有结果集或无法确定行数。

虽然规范没有要求，但大多数数据库模块中的游标对象也实现了迭代协议。在这种情况下，像 `for row in cur:` 这样的语句将迭代由上一个 `execute*()` 方法创建的结果集的行。

#### 类型对象

- `STRING`: 表示字符串列。
- `BINARY`: 表示二进制列。
- `NUMBER`: 表示数值列。
- `DATETIME`: 表示日期/时间列。
- `ROWID`: 表示行 ID 列。

类型对象用于确定结果集中列的数据类型。它们也用于为查询中的参数提供值。

##### 类型对象和构造函数

- `Binary(string)`: 构造一个能够保存二进制（长）字符串值的对象。
- `Date(year, month, day)`: 构造一个保存日期值的对象。
- `Time(hour, minute, second)`: 构造一个保存时间值的对象。
- `Timestamp(year, month, day, hour, minute, second)`: 构造一个保存时间/日期值的对象。
- `DateFromTicks(ticks)`: 从给定的 ticks 值（自纪元以来的秒数；参见 `time` 模块）构造一个保存日期值的对象。
- `TimeFromTicks(ticks)`: 从给定的 ticks 值构造一个保存时间值的对象。
- `TimestampFromTicks(ticks)`: 从给定的 ticks 值构造一个保存时间/日期值的对象。
- `Numeric(string)`: 从给定的字符串构造一个保存数值的对象。
- `String(string)`: 从给定的字符串构造一个保存字符串值的对象。

这些构造函数作为模块接口的一部分公开，以允许创建适当类型对象的实例。

##### 二进制和字符串类型

- `Binary(string)`: 此构造函数创建一个能够保存二进制（长）字符串值的类型对象。用于包含二进制数据（如图像）的列。
- `String(string)`: 此构造函数创建一个能够保存字符串值的类型对象。用于包含字符数据的列。

这些类型对象用于游标的 `description` 属性中，以指示列中的数据类型。

##### Null 处理

值 `None` 用于表示数据库中的 NULL 值。当从数据库获取数据时，具有 NULL 值的列在结果中其值将为 `None`。

##### 事务

数据库 API 支持事务。这意味着在使用 `execute*()` 方法对数据库进行更改后，你必须调用 `commit()` 来使这些更改永久生效。如果你想丢弃更改，可以调用 `rollback()` 将数据库恢复到更改之前的状态。

连接对象的 `autocommit` 属性可用于控制是否在每条语句后自动提交事务。默认情况下，`autocommit` 为 `False`，意味着你必须显式调用 `commit()`。

#### 错误处理

数据库 API 定义了一组数据库操作可能引发的异常：

- `InterfaceError`: 与数据库接口而非数据库本身相关的问题引发。
- `DatabaseError`: 与数据库相关的错误引发。
- `DataError`: 由于处理的数据问题导致的错误引发。
- `OperationalError`: 与数据库操作相关的错误引发。
- `IntegrityError`: 当数据库的引用完整性受到影响时引发。
- `InternalError`: 当数据库遇到内部错误时引发。
- `ProgrammingError`: 编程错误引发。
- `NotSupportedError`: 尝试不支持的操作时引发。

这些异常是 `StandardError` 的子类。

##### 定义新的类型对象

你可以定义新的类型对象来处理数据库特定类型到 Python 类型的转换。这是通过创建一个实现以下方法的类来完成的：

- `__init__(self, value)`: 用给定的值初始化类型对象。
- `__conform__(self, proto)`: 返回对象针对给定协议的适配表示形式。用于将对象转换为数据库可以理解的格式。
- `__repr__(self)`: 返回对象的字符串表示形式。

这些方法允许你创建自定义类型对象，可以用来替代标准类型对象。

##### 结论

Python Database API Specification 提供了一个标准接口，用于从 Python 访问关系型数据库。通过遵循此规范，你可以编写可跨不同数据库系统移植的数据库代码。API 中的关键对象是 `Connection` 和 `Cursor` 对象，它们提供了连接数据库、执行查询和获取结果的方法。API 还定义了一组用于处理不同类型数据的类型对象和构造函数，以及一组用于错误处理的异常。有了这些知识，你就可以开始使用 Python 以健壮且可移植的方式与数据库进行交互。



这是一个简单的示例，展示了如何在内置库 **sqlite3** 数据库模块中使用其中一些操作：

```python
import sqlite3
conn = sqlite3.connect("dbfile")
cur = conn.cursor()

###### 简单查询示例
cur.execute("select name, shares, price from portfolio where account=12345")

###### 遍历结果
while True:
    row = cur.fetchone()
    if not row: break
    # 处理行数据
    name, shares, price = row
    ...
```

```python
###### 另一种方法（使用迭代器）
cur.execute("select name, shares, price from portfolio where account=12345")
for name, shares, price in cur:
    # 处理行数据
    ...
```

#### 构建查询

使用数据库 API 的关键部分之一是构建 SQL 查询字符串，并将其传递给游标对象的 `execute*()` 方法。这里的一个问题是，你需要用用户提供的参数填充查询字符串的部分内容。例如，你可能会倾向于编写如下代码：

```python
symbol = "AIG"
account = 12345

cur.execute("select shares from portfolio where name='%s' and account=%d" %
             (symbol, account))
```

虽然这能“运行”，但你绝不应手动使用此类 Python 字符串操作来构建查询。如果这样做，会使你的代码面临潜在的 **SQL 注入攻击** 风险——这是一种漏洞，攻击者可利用它在数据库服务器上执行任意语句。例如，在上述代码中，有人可能会提供一个名为 `symbol` 的值，其内容类似于 `"EVIL LAUGH'; drop table portfolio;--"`，这可能会导致与你预期不同的行为。

所有数据库模块都提供了自己的值替换机制。例如，与其像上面那样构建整个查询，你可以这样做：

```python
symbol  = "AIG"
account = 12345

cur.execute("select shares from portfolio where name=? and account=?",
             (symbol, account))
```

在这里，`?` 占位符会依次被元组 `(symbol, account)` 中的值替换。

不幸的是，不同数据库模块实现在占位符方面没有统一的标准约定。但是，每个模块都定义了一个名为 `paramstyle` 的变量，用于指示查询中要使用的值替换格式。该变量的可能值如下：

| 参数样式 | 描述 |
|---|---|
| `'qmark'` | 问号样式，查询中的每个 `?` 替换为序列中的连续项。例如，`cur.execute("... where name=? and account=?", (symbol, account))`。参数以元组形式指定。 |
| `'numeric'` | 数字样式，`:n` 替换为索引 `n` 处的参数值。例如，`cur.execute("... where name=:0 and account=:1", (symbol, account))`。 |
| `'named'` | 命名样式，`:name` 替换为命名值。对于此样式，参数必须以映射形式给出。例如，`cur.execute("... where name=:symbol and account=:account", {'symbol':symbol, 'account': account})`。 |
| `'format'` | Printf 风格格式代码，如 `%s`、`%d` 等。例如，`cur.execute("... where name=%s and account=%d", (symbol, account))`。 |
| `'pyformat'` | Python 扩展格式代码，如 `%(name)s`。类似于 `'named'` 样式。参数必须以映射形式指定，而非元组。 |

#### 类型对象

在处理数据库数据时，内置类型（如整数和字符串）通常会映射到数据库中相应的类型。然而，对于日期、二进制数据和其他特殊类型，数据管理更为棘手。为了辅助这种映射，数据库模块实现了一组用于创建各种类型对象的构造函数。

```python
Date(year, month, day)
```

创建一个表示日期的对象。

```python
Time(hour, minute, second)
```

创建一个表示时间的对象。

```python
Timestamp(year, month, day, hour, minute, second)
```

创建一个表示时间戳的对象。

```python
DateFromTicks(ticks)
```

从系统时间值创建一个日期对象。*ticks* 是由 `time.time()` 等函数返回的秒数。

```python
TimeFromTicks(ticks)
```

从系统时间值创建一个时间对象。

```python
TimestampFromTicks(ticks)
```

从系统时间值创建一个时间戳对象。

```python
Binary(s)
```

从字节串 *s* 创建一个二进制对象。

除了这些构造函数外，还可能会定义以下类型对象。这些代码的用途是对 `cur.description`（描述当前结果集的内容）中的 `type_code` 字段进行类型检查。

| 类型对象 | 描述 |
|---|---|
| STRING | 字符或文本数据 |
| BINARY | 二进制数据，如 BLOB |
| NUMBER | 数值数据 |
| DATETIME | 日期和时间数据 |
| ROWID | 行 ID 数据 |

#### 错误处理

数据库模块定义了一个顶层异常 `Error`，它是所有其他错误的基类。以下异常用于更特定类型的数据库错误：

| 异常 | 描述 |
|---|---|
| InterfaceError | 与数据库接口相关的错误，但与数据库本身无关。 |
| DatabaseError | 与数据库本身相关的错误。 |
| DataError | 与处理的数据相关的错误。例如，类型转换错误、除以零等。 |
| OperationalError | 与数据库操作相关的错误。例如，连接丢失。 |
| IntegrityError | 数据库关系完整性被破坏时的错误。 |
| InternalError | 数据库内部错误。例如，游标过期。 |
| ProgrammingError | SQL 查询中的错误。 |
| NotSupportedError | 数据库 API 中不受底层数据库支持的方法的错误。 |

模块还可以定义一个 `Warning` 异常，数据库模块可用于警告数据更新过程中的数据截断等问题。

#### 多线程

如果你将数据库访问与多线程混合使用，底层的数据库模块可能线程安全，也可能不是。每个模块中定义了以下变量以提供更多相关信息。

`threadsafety`

一个表示模块线程安全性的整数。可能的值如下：

- 0 - 无线程安全性。线程不能共享模块的任何部分。
- 1 - 模块是线程安全的，但不能共享连接。
- 2 - 模块和连接是线程安全的，但不能共享游标。
- 3 - 模块、连接和游标都是线程安全的。

##### 将结果映射为字典

关于数据库结果的一个常见问题是将元组或列表映射到命名字段的字典中。例如，如果查询的结果集包含大量列，使用描述性字段名称而不是在元组中硬编码特定字段的数值索引来处理这些数据可能会更容易。

处理这种情况的方法有很多，但处理结果数据最优雅的方法之一是使用**生成器函数**。例如：

```python
def generate_dicts(cur):
    import itertools
    fieldnames = [d[0].lower() for d in cur.description ]
    while True:
        rows = cur.fetchmany()
        if not row: return
        for row in rows:
            yield dict(itertools.izip(fieldnames,row))
```

```python
###### 示例用法
cur.execute("select name, shares, price from portfolio")
for r in generate_dicts(cur):
    print r['name'],r['shares'],r['price']
```

请注意，数据库之间的列命名并不完全一致——尤其是关于大小写敏感性等方面。因此，如果你尝试将此技术应用到旨在与各种不同数据库模块配合使用的代码中，你需要格外小心。

#### 数据库 API 扩展

最后，可以向特定的数据库模块添加许多扩展和高级功能——例如，支持两阶段提交和扩展的错误处理。PEP-249 提供了有关这些功能推荐接口的更多信息，高级用户应予以查阅。第三方库模块也可能简化关系数据库接口的使用。

#### sqlite3 模块

sqlite3 模块为 SQLite 数据库库（[http://www.sqlite.org](http://www.sqlite.org)）提供了 Python 接口。SQLite 是一个 C 库，它在文件或内存中完全实现了一个自包含的关系数据库。尽管它很简单，但该库因多种原因而具有吸引力。首先，它不依赖单独的数据库服务器，也不要求任何特殊配置——你只需连接到数据库文件即可立即在程序中使用它（如果文件不存在，则会创建新文件）。该数据库还支持事务以提高可靠性（即使跨越系统崩溃）以及锁定机制，以允许从多个进程同时访问同一个数据库文件。

该库的编程接口遵循上一节中关于数据库 API 描述的约定，因此此处不再重复许多细节。相反，本节侧重于使用此模块的技术细节以及 sqlite3 模块特有的功能。



##### 模块级函数

以下函数由 `sqlite3` 模块定义：

```python
connect(database [, timeout [, isolation_level [, detect_types]]])
```

创建一个到 SQLite 数据库的连接。`database` 是一个字符串，用于指定数据库文件的名称。它也可以是一个字符串 `":memory:"`，这种情况下将使用一个内存数据库（请注意，这种数据库仅在 Python 进程运行期间存在，程序退出时数据会丢失）。`timeout` 参数指定了当其他连接正在更新数据库时，等待内部读写锁释放的时间长度。默认情况下，`timeout` 为 5 秒。当使用 `INSERT` 或 `UPDATE` 等 SQL 语句时，如果当前没有活动事务，则会自动开始一个新事务。`isolation_level` 参数是一个字符串，为用于启动此事务的底层 SQL `BEGIN` 语句提供可选的修饰符。可能的值为 `""`（默认值）、`"DEFERRED"`、`"EXCLUSIVE"` 或 `"IMMEDIATE"`。这些设置的含义与底层数据库锁相关，具体如下：

| 事务隔离级别 | 描述 |
| --- | --- |
| `""` (空字符串) | 使用默认设置 (`DEFERRED`)。 |
| `"DEFERRED"` | 启动一个新事务，但直到第一个数据库操作实际执行时才获取锁。 |
| `"EXCLUSIVE"` | 启动一个新事务，并保证在更改提交之前，没有其他连接可以读取或写入数据库。 |
| `"IMMEDIATE"` | 启动一个新事务，并保证在更改提交之前，没有其他连接可以修改数据库。但是，其他连接仍然可以从数据库读取。 |

`detect_types` 参数在返回结果时启用一些额外的类型检测（通过解析 SQL 查询实现）。默认情况下为 0（意味着没有额外检测）。它可以设置为 `PARSE_DECLTYPES` 和 `PARSE_COLNAMES` 的按位或。如果启用了 `PARSE_DECLTYPES`，则会检查查询中是否存在如 `"integer"` 或 `"number(8)"` 之类的 SQL 类型名称，以确定结果列的类型。如果启用了 `PARSE_COLNAMES`，则可以在查询中嵌入形式为 `"colname [typename]"`（包括双引号）的特殊字符串，其中 `colname` 是列名，`typename` 是接下来将要描述的 `register_converter()` 函数注册的类型名称。当传递给 SQLite 引擎时，这些字符串会被简单地转换为 `colname`，但在转换查询结果中的值时，会使用额外的类型说明符。例如，像 `'select price as "price [decimal]" from portfolio'` 这样的查询会被解释为 `'select price as price from portfolio'`，并且结果将根据 "decimal" 转换规则进行转换。

```python
register_converter(typename, func)
```

为给定的 SQL 类型名称注册一个新的转换器。

例如，如果你调用 `sqlite3.register_converter('decimal', decimal.Decimal)`，那么你可以通过编写如 `'select price as "price [decimal]" from stocks'` 这样的查询，将查询中的值转换为 `Decimal` 对象。

```python
register_adapter(type, func)
```

注册一个用于 Python 类型 *type* 的适配器函数，该函数在将该类型的值存储到数据类型中时使用。*func* 是一个接受类型 *type* 的实例作为输入，并返回 `int`、`float`、UTF-8 编码的字节字符串、Unicode 字符串或 buffer 作为结果的函数。例如，如果你想存储 `Decimal` 对象，你可以使用 `sqlite3.register_adapter(decimal.Decimal, float)`。

```python
complete_statement(s)
```

如果字符串 *s* 表示一个或多个由分号分隔的完整 SQL 语句，则返回 `True`。如果编写一个从用户读取查询的交互式程序，这可能会很有用。

```python
enable_callback_tracebacks(flag)
```

决定如何处理用户定义回调函数（如转换器和适配器）中的异常。默认情况下，异常会被忽略。如果 *flag* 设置为 `True`，则回溯消息将打印到 `sys.stderr`。

##### 连接对象

`connect()` 函数返回的 `Connection` 对象 *c* 支持数据库 API 中描述的标准操作。此外，还提供了 `sqlite3` 模块特有的以下方法。

```python
c.create_function(name, num_params, func)
```

创建一个可在 SQL 语句中使用的用户定义函数。*name* 是一个包含函数名称的字符串，*num_params* 是一个整数，给出参数的数量，*func* 是一个提供实现的 Python 函数。下面是一个简单的例子：

```python
def toupper(s):
    return s.upper()
c.create_function("toupper", 1, toupper)
###### 查询中的示例用法
c.execute("select toupper(name),foo,bar from sometable")
```

虽然定义的是一个 Python 函数，但该函数的参数和输入应该仅为 `int`、`float`、`str`、`unicode`、`buffer` 或 `None`。

```python
c.create_aggregate(name, num_params, aggregate_class)
```

创建一个用于 SQL 语句的用户定义聚合函数。*name* 是一个包含函数名称的字符串，*num_params* 是一个整数，给出输入参数的数量。*aggregate_class* 是一个实现聚合操作的类。该类必须支持无参数初始化，并实现一个 `step(params)` 方法，该方法接受与 *num_params* 中给出的数量相同的参数，以及一个 `finalize()` 方法，该方法返回最终结果。下面是一个简单的例子：

```python
class Averager(object):
    def __init__(self):
        self.total = 0.0
        self.count = 0
    def step(self, value):
        self.total += value
        self.count += 1
    def finalize(self):
        return self.total / self.count

c.create_aggregate("myavg", 1, Averager)
###### 查询中的示例用法
c.execute("select myavg(num) from sometable")
```

聚合通过使用输入值重复调用 step() 方法，然后调用 finalize() 来获取最终值来实现。

```python
c.create_collation(name, func)
```

注册一个用于 SQL 语句的用户定义排序函数。*name* 是一个包含排序函数名称的字符串，*func* 是一个接受两个输入的函数，并根据第一个输入低于、等于或高于第二个输入返回 -1、0、1。你可以使用 SQL 表达式来使用用户定义的函数，例如 `"select * from table order by colname collate name"`。

```python
c.execute(sql [, params])
```

一个快捷方法，它使用 `c.cursor()` 创建一个游标对象，并使用 *sql* 中的 SQL 语句和 *params* 中的参数执行游标的 `execute()` 方法。

```python
c.executemany(sql [, params])
```

一个快捷方法，它使用 `c.cursor()` 创建一个游标对象，并使用 *sql* 中的 SQL 语句和 *params* 中的参数执行游标的 `executemany()` 方法。

```python
c.executescript(sql)
```

一个快捷方法，它使用 `c.cursor()` 创建一个游标对象，并使用 *sql* 中的 SQL 语句执行游标的 `executescript()` 方法。

```python
c.interrupt()
```

中止连接上当前正在执行的任何查询。这应该从单独的线程中调用。

```python
c.iterdump()
```

返回一个迭代器，将整个数据库内容转储为一系列可以执行以重建数据库的 SQL 语句。如果要将数据库导出到其他地方，或者需要将内存数据库的内容转储到文件中以便以后恢复，这将很有用。

```python
c.set_authorizer(auth_callback)
```

注册一个授权回调函数，用于获取数据库中一列数据的受托人信息。回调函数必须接受五个参数，形式为 `auth_callback(code, arg1, arg2, dbname, innername)`。此回调返回的值可以是 `SQLITE_OK`（如果允许访问）、`SQLITE_DENY`（如果 SQL 语句应因错误而失败）或 `SQLITE_IGNORE`（如果应将该列视为 Null 值而忽略）。第一个参数 *code* 是一个整数操作码。*arg1* 和

##### SQLite3 模块

###### 回调函数参数

`arg1` 和 `arg2` 是参数，其值取决于 `code` 的值。`dbname` 是包含数据库名称的字符串（通常是 "main"），`innername` 是尝试访问的最内层视图或触发器的名称，如果没有视图或触发器处于活动状态，则为 `None`。下表列出了 `code` 的值以及 `arg1` 和 `arg2` 参数的含义：

| Code | Arg1 | Arg2 |
|------|------|------|
| SQLITE_CREATE_INDEX | Index name | Table name |
| SQLITE_CREATE_TABLE | Table name | None |
| SQLITE_CREATE_TEMP_INDEX | Index name | Table name |
| SQLITE_CREATE_TEMP_TABLE | Table name | None |
| SQLITE_CREATE_TEMP_TRIGGER | Trigger name | Table name |
| SQLITE_CREATE_TEMP_VIEW | View name | None |
| SQLITE_CREATE_TRIGGER | Trigger name | Table name |
| SQLITE_CREATE_VIEW | View name | None |
| SQLITE_DELETE | Table name | None |
| SQLITE_DROP_INDEX | Index name | Table name |
| SQLITE_DROP_TABLE | Table name | None |
| SQLITE_DROP_TEMP_INDEX | Index name | Table name |
| SQLITE_DROP_TEMP_TABLE | Table name | None |
| SQLITE_DROP_TEMP_TRIGGER | Trigger name | Table name |
| SQLITE_DROP_TEMP_VIEW | View name | None |
| SQLITE_DROP_TRIGGER | Trigger name | Table name |
| SQLITE_DROP_VIEW | View name | None |
| SQLITE_INSERT | Table name | None |
| SQLITE_PRAGMA | Pragma name | None |
| SQLITE_READ | Table name | Column name |
| SQLITE_SELECT | None | None |
| SQLITE_TRANSACTION | None | None |
| SQLITE_UPDATE | Table name | Column name |
| SQLITE_ATTACH | Filename | None |
| SQLITE_DETACH | Database name | None |
| SQLITE_ALTER_TABLE | Database name | Table name |
| SQLITE_REINDEX | Index name | None |
| SQLITE_ANALYZE | Table name | None |
| SQLITE_CREATE_VTABLE | Table name | Module name |
| SQLITE_DROP_VTABLE | Table name | Module name |
| SQLITE_FUNCTION | Function name | None |

`c.set_progress_handler(handler, n)`

注册一个回调函数，该函数在 SQLite 虚拟机的每 `n` 条指令后执行。`handler` 是一个不带参数的函数。

###### 连接对象的属性

连接对象上还定义了以下属性。

`c.row_factory`

一个函数，用于创建代表每个结果行内容的对象。此函数接受两个参数：用于获取结果的游标对象和一个包含原始结果行的元组。

`c.text_factory`

一个函数，用于创建代表数据库中文本值的对象。该函数必须接受一个参数，即 UTF-8 编码的字节字符串。返回值应该是某种字符串。默认情况下，返回一个 Unicode 字符串。

`c.total_changes`

一个整数，表示自打开数据库连接以来已修改的行数。

连接对象的最后一个特性是它们可以与上下文管理器协议一起使用来自动处理事务。例如：

```python
conn = sqlite.connect("somedb")
with conn:
    conn.execute("insert into sometable values (?,?)", ("foo","bar")))
```

在此示例中，当 `with` 块中的所有语句执行完毕且未发生错误时，会自动执行 `commit()` 操作。如果引发任何异常，则会执行 `rollback()` 操作并重新引发该异常。

##### 游标和基本操作

要对 sqlite3 数据库执行基本操作，您首先必须使用连接的 `cursor()` 方法创建一个游标对象。然后，使用游标的 `execute()`、`executemany()` 或 `executescript()` 方法执行 SQL 语句。有关这些方法的一般操作，请参见数据库 API 部分。此处不再重复该信息，而是介绍一组常见的数据库用例和示例代码。目标是展示游标对象的操作以及一些常见的 SQL 操作，供那些可能需要快速回顾语法的程序员使用。

##### 创建新的数据库表

以下代码展示了如何打开数据库并创建一个新表：

```python
import sqlite3
conn = sqlite3.connect("mydb")
cur = conn.cursor()
cur.execute("create table stocks (symbol text, shares integer, price real)")
conn.commit()
```

定义表时，应使用一些基本的 SQLite 数据类型：`text`、`integer`、`real` 和 `blob`。`blob` 类型是字节字符串，而 `text` 类型被假定为 UTF-8 编码的 Unicode。

##### 向表中插入新值

以下代码展示了如何向表中插入新项目：

```python
import sqlite3
conn = sqlite3.connect("mydb")
cur = conn.cursor()
cur.execute("insert into stocks values (?,?,?)",('IBM',50,91.10))
cur.execute("insert into stocks values (?,?,?)",('AAPL',100,123.45))
conn.commit()
```

插入值时，应始终使用如图所示的 `?` 占位符。每个 `?` 由作为参数提供的值元组中的一个值替换。

如果您有一系列数据要插入，可以使用游标的 `executemany()` 方法，如下所示：

```python
stocks = [ ('GOOG',75,380.13),
           ('AA',60,14.20),
           ('AIG',125, 0.99) ]
cur.executemany("insert into stocks values (?,?,?)",stocks)
```

##### 更新现有行

以下代码展示了如何更新现有行的列：

```python
cur.execute("update stocks set shares=? where symbol=?",(50,'IBM'))
```

同样，当需要将值插入 SQL 语句时，请确保使用 `?` 占位符，并提供一个值元组作为参数。

##### 删除行

以下代码展示了如何删除行：

```python
cur.execute("delete from stocks where symbol=?",('SCOX',))
```

##### 执行基本查询

以下代码展示了如何执行基本查询并获取结果：

```python
###### Select all columns from a table
for row in cur.execute("select * from stocks"):
    statements
```

```python
###### Select a few columns
for shares, price in cur.execute("select shares,price from stocks"):
    statements
```

```python
###### Select matching rows
for row in cur.execute("select * from stocks where symbol=?",('IBM',))
    statements
```

```python
###### Select matching rows with ordering
for row in cur.execute("select * from stocks order by shares"):
    statements
```

```python
###### Select matching rows with ordering in reverse
for row in cur.execute("select * from stocks order by shares desc"):
    statements
```

```python
###### Joining tables on a common column name (symbol)
for row in cur.execute("""select s.symbol, s.shares, p.price
                                     from stocks as s, prices as p using(symbol)"""):
    statements
```

##### DBM 风格的数据库模块

Python 包含许多用于支持 UNIX DBM 风格数据库文件的库模块。支持几种标准类型的这些数据库。`dbm` 模块用于读取标准 UNIX-dbm 数据库文件。`gdbm` 模块用于读取 GNU dbm 数据库文件（http://www.gnu.org/software/gdbm）。`dbhash` 模块用于读取由 Berkeley DB 库创建的数据库文件（http://www.oracle.com/database/berkeley-db/index.html）。`dumbdbm` 模块是一个纯 Python 模块，它自己实现了一个简单的 DBM 风格数据库。

所有这些模块都提供一个实现了基于持久字符串的字典的对象。也就是说，它的工作方式类似于 Python 字典，但所有键和值都限定为字符串。数据库文件通常使用 `open()` 函数的变体打开。

`open(filename [, flag [, mode]])`

此函数打开数据库文件 `filename` 并返回一个数据库对象。`flag` 为 `'r'` 表示只读访问，`'w'` 表示读写访问，`'c'` 表示如果数据库不存在则创建它，或 `'n'` 表示强制创建新数据库。`mode` 是创建数据库时使用的整数文件访问模式（在 UNIX 上默认为 `0666`）。

`open()` 函数返回的对象至少支持以下类字典操作：

| 操作 | 描述 |
|------|------|
| `d[key] = value` | 将 `value` 插入数据库 |
| `value = d[key]` | 从数据库获取数据 |
| `del d[key]` | 删除数据库条目 |
| `d.close()` | 关闭数据库 |
| `key in d` | 测试键是否存在 |
| `d.sync()` | 将所有更改写入数据库 |

特定实现可能还会添加其他功能（请参阅相应的模块参考以获取详细信息）。

各种 DBM 风格数据库模块的一个问题是，并非每个模块都安装在每个平台上。例如，如果您在 Windows 上使用 Python，`dbm` 和 `gdbm` 模块通常不可用。然而，程序可能仍然希望创建一个 DBM 风格的数据库供自己使用。为了解决这个问题，Python 提供了一个 `anydbm` 模块，可用于打开和创建 DBM 风格的数据库文件。此模块提供了如前所述的 `open()` 函数，但它保证在所有平台上都能工作。它通过查看可用的 DBM 模块集并选择可用的最先进库（通常是安装后的 `dbhash`）来实现这一点。作为后备，它使用始终可用的 `dumbdbm` 模块。

另一个模块是 `whichdb`，它有一个函数 `whichdb(filename)`，可用于探测文件以确定哪种 DBM 数据库创建了它。

一般来说，在可移植性很重要的应用程序中，最好不要依赖这些低级模块。例如，如果您在一台机器上创建了 DBM 数据库，然后将数据库文件传输到另一台机器，如果底层的 DBM 模块不存在，Python 可能无法读取它。



##### shelve 模块

`shelve` 模块使用特殊的 "shelf" 对象提供对持久化对象的支持。此对象的行为类似于字典，不同之处在于它包含的所有对象都使用基于哈希表的数据库（如 `dbhash`、`dbm` 或 `gdbm`）存储在磁盘上。然而，与这些模块不同，存储在 shelf 中的值不仅限于字符串。相反，任何与 `pickle` 模块兼容的对象都可以被存储。shelf 使用 `shelve.open()` 函数创建。

```
open(filename [,flag='c' [, protocol [, writeback]]])
```

打开一个 shelf 文件。如果文件不存在，将会创建它。`filename` 应该是数据库文件名，不应包含后缀。`flag` 的含义与章节介绍中描述的相同，是 'r'、'w'、'c' 或 'n' 之一。如果数据库文件不存在，它会被创建。`protocol` 指定用于对存储在数据库中的对象进行 pickle 处理的协议。其含义与 `pickle` 模块中描述的相同。`writeback` 控制数据库对象的缓存行为。如果为 `True`，所有被访问的条目都会被缓存在内存中，并且只有在关闭 shelf 时才写回磁盘。默认值为 `False`。返回一个 shelf 对象。

一旦 shelf 被打开，就可以对其执行以下字典操作：

| 操作 | 描述 |
|-----------|-------------|
| d[key] = data | 在键 `key` 处存储数据 `data`。覆盖现有数据。 |
| data = d[key] | 检索键 `key` 处的数据。 |
| del d[key] | 删除键 `key` 处的数据。 |
| d.has_key(key) | 测试键 `key` 是否存在。 |
| d.keys() | 返回所有键。 |
| d.close() | 关闭 shelf。 |
| d.sync() | 将未保存的数据写入磁盘。 |

shelf 的键值必须是字符串。存储在 shelf 中的对象必须可以使用 `pickle` 模块序列化。

```
Shelf(dict [, protocol [, writeback]])
```

一个混合类，它在字典对象 `dict` 之上实现了 shelf 的功能。当使用此类时，存储在返回的 shelf 对象中的对象将被 pickle 并存储在底层字典 `dict` 中。`protocol` 和 `writeback` 的含义与 `shelve.open()` 相同。

`shelve` 模块使用 `anydbm` 模块来选择合适的 DBM 模块使用。在大多数标准的 Python 安装中，它很可能是 `dbhash`，它依赖于 Berkeley DB 库。

### 18 文件和目录处理

本章描述用于高级文件和目录处理的 Python 模块。主题包括处理各种基本文件编码的模块（如 `gzip` 和 `bzip2` 文件）、提取文件归档（如 `zip` 和 `tar` 文件）的模块，以及操作文件系统本身（例如，目录列表、移动、重命名、复制等）的模块。与文件相关的底层操作系统调用在第 19 章“操作系统服务”中介绍。解析文件内容（如 XML 和 HTML）的模块主要在第 24 章“互联网数据处理和编码”中介绍。

#### bz2

`bz2` 模块用于读取和写入根据 bzip2 压缩算法压缩的数据。

```
BZ2File(filename [, mode [, buffering [, compresslevel]]])
```

打开一个 `.bz2` 文件 `filename`，并返回一个类似文件的对象。`mode` 为 'r' 表示读取，为 'w' 表示写入。通过指定模式为 'rU'，也可以使用通用换行符支持。`buffering` 指定缓冲区大小（以字节为单位），默认值为 0（无缓冲）。`compresslevel` 是 1 到 9 之间的数字。值为 9（默认值）提供最高级别的压缩，但消耗最多的处理时间。返回的对象支持所有常见的文件操作，包括 `close()`、`read()`、`readline()`、`readlines()`、`seek()`、`tell()`、`write()` 和 `writelines()`。

```
BZ2Compressor([compresslevel])
```

创建一个压缩器对象，可用于顺序压缩一系列数据块。`compresslevel` 指定压缩级别为 1 到 9 之间的数字（默认值）。

`BZ2Compressor` 的实例 `c` 具有以下两个方法：

```
c.compress(data)
```

向压缩器对象 `c` 提供新的字符串数据 `data`。如果可能，返回压缩数据的字符串。由于压缩涉及数据块，返回的字符串可能不包含所有数据，并且可能包含来自之前调用 `compress()` 的压缩数据。在所有输入数据都提供后，应使用 `flush()` 方法返回存储在压缩器中的任何剩余数据。

```
c.flush()
```

刷新内部缓冲区，并返回包含所有剩余数据压缩版本的字符串。在此操作之后，不应再对该对象进行 `compress()` 调用。

```
BZ2Decompressor()
```

创建一个解压器对象。

`BZ2Decompressor` 的实例 `d` 仅支持一个方法：

```
d.decompress(data)
```

给定字符串 `data` 中的一个压缩数据块，此方法返回未压缩的数据。由于数据是以块形式处理的，返回的字符串可能包含也可能不包含 `data` 中所有供应内容的解压缩版本。重复调用此方法将继续解压数据块，直到在输入中找到流结束标记。如果在此之后尝试解压数据，将引发 `EOFError` 异常。

```
compress(data [, compresslevel])
```

返回字符串 `data` 中供应数据的压缩版本。`compresslevel` 是 1 到 9 之间的数字（默认值）。

```
decompress(data)
```

返回一个包含字符串 `data` 中解压后数据的字符串。

#### filecmp

`filecmp` 模块提供以下函数，可用于比较文件和目录：

```
cmp(file1, file2 [, shallow])
```

比较文件 `file1` 和 `file2`，如果它们相等则返回 `True`，否则返回 `False`。默认情况下，`os.stat()` 返回的属性相同的文件被认为是相等的。如果指定了 `shallow` 参数且为 `False`，则比较两个文件的内容以确定相等性。

```
cmpfiles(dir1, dir2, common [, shallow])
```

比较两个目录 `dir1` 和 `dir2` 中列表 `common` 所包含的文件内容。返回一个元组，包含三个文件名列表（`match`、`mismatch`、`errors`）。`match` 列出两个目录中相同的文件，`mismatch` 列出不匹配的文件，`errors` 列出由于某些原因无法比较的文件。`shallow` 参数的含义与 `cmp()` 相同。

```
dircmp(dir1, dir2 [, ignore[, hide]])
```

创建一个目录比较对象，可用于对目录 `dir1` 和 `dir2` 执行各种比较操作。`ignore` 是要忽略的文件名列表，默认值为 `['RCS','CVS','tags']`。`hide` 是要隐藏的文件名列表，默认值为 `[os.curdir, os.pardir]`（在 UNIX 上为 `['.', '..']`）。

由 `dircmp()` 返回的目录对象 *d* 具有以下方法和属性：

**`d.report()`**

比较目录 *dir1* 和 *dir2* 并将报告打印到 `sys.stdout`。

**`d.report_partial_closure()`**

比较 *dir1* 和 *dir2* 以及共同的直接子目录。结果打印到 `sys.stdout`。

**`d.report_full_closure()`**

递归比较 *dir1* 和 *dir2* 以及所有子目录。结果打印到 `sys.stdout`。

**`d.left_list`**

列出 *dir1* 中的文件和子目录。内容由 *hide* 和 *ignore* 过滤。

**`d.right_list`**

列出 *dir2* 中的文件和子目录。内容由 *hide* 和 *ignore* 过滤。

**`d.common`**

列出在 *dir1* 和 *dir2* 中都找到的文件和子目录。

**`d.left_only`**

列出仅在 *dir1* 中找到的文件和子目录。

**`d.right_only`**

列出仅在 *dir2* 中找到的文件和子目录。

**`d.common_dirs`**

列出 *dir1* 和 *dir2* 中共有的子目录。

**`d.common_files`**

列出 *dir1* 和 *dir2* 中共有的文件。

**`d.common_funny`**

列出 *dir1* 和 *dir2* 中类型不同或无法从 `os.stat()` 获取信息的文件。

**`d.same_files`**

列出 *dir1* 和 *dir2* 中内容相同的文件。

**`d.diff_files`**

列出 *dir1* 和 *dir2* 中内容不同的文件。

**`d.funny_files`**

列出在 *dir1* 和 *dir2* 中都存在但由于某些原因（例如，权限不足无法访问）无法比较的文件。

**`d.subdirs`**

一个字典，将 `d.common_dirs` 中的名称映射到额外的 `dircmp` 对象。



`dircmp`对象的属性是**惰性求值**的，并不是在首次创建`dircmp`对象时就确定。因此，如果你只对其中部分属性感兴趣，其他未使用的属性不会带来额外的性能开销。

#### fnmatch

`fnmatch`模块提供了使用UNIX shell风格的通配符匹配文件名的功能。该模块仅执行文件名匹配，而`glob`模块可用于实际获取文件列表。模式语法如下：

| 字符 | 描述 |
|--------------|-------------|
| * | 匹配所有字符 |
| ? | 匹配任意单个字符 |
| [seq] | 匹配`seq`中的任意字符 |
| [!seq] | 匹配不在`seq`中的任意字符 |

以下函数可用于测试通配符匹配：

**fnmatch(filename, pattern)**

根据`filename`是否匹配`pattern`返回`True`或`False`。区分大小写取决于操作系统（在某些平台如Windows上可能不区分大小写）。

**fnmatchcase(filename, pattern)**

对`filename`和`pattern`进行**区分大小写**的比较。

**filter(names, pattern)**

将`fnmatch()`函数应用于序列`names`中的所有名称，并返回所有匹配`pattern`的名称列表。

##### 示例

```
fnmatch('foo.gif', "*.gif")	# 返回 True
fnmatch("part37.html', 'part3[0-5].html')	# 返回 False

###### 使用 os.walk()、fnmatch 和生成器在完整目录树中查找文件的示例
def findall(topdir, pattern):
    for path, files, dirs in os.walk(topdir):
        for name in files:
            if fnmatch.fnmatch(name, pattern):
                yield os.path.join(path, name)
###### 查找所有 .py 文件
for pyfile in findall(".", "*.py"):
    print(pyfile)
```

#### glob

`glob`模块返回目录中所有匹配使用UNIX shell规则（如`fnmatch`模块中描述）指定模式的文件名。

```
glob(pattern)
```

返回匹配*pattern*的路径名列表。

```
iglob(pattern)
```

返回与`glob()`相同的结果，但使用迭代器。

##### 示例

```
htmlfile = glob('*.html')
imgfiles = glob('image[0-5]*.gif')
```

> **注意**
> 不会执行波浪号（`~`）和shell变量展开。在调用`glob()`之前，请分别使用`os.path.expanduser()`和`os.path.expandvars()`执行这些展开。

#### gzip

`gzip`模块提供了一个名为`GzipFile`的类，可用于读写与GNU `gzip`程序兼容的文件。`GzipFile`对象的工作方式类似于普通文件，但数据会自动压缩或解压缩。

```
GzipFile([filename [, mode [, compresslevel [, fileobj]]]])
```

打开一个`GzipFile`。*filename*是文件名，*mode*是`'r'`、`'rb'`、`'a'`、`'ab'`、`'w'`或`'wb'`之一。默认值为`'rb'`。*compresslevel*是从1到9的整数，控制压缩级别。1是最快的，产生的压缩最少；9是最慢的，产生的压缩最多（默认值）。*fileobj*是应使用的现有文件对象。如果提供了，则使用它而不是*filename*指定的文件。

```
open(filename [, mode [, compresslevel]])
```

与`GzipFile(filename, mode, compresslevel)`相同。默认模式为`'rb'`。默认*compresslevel*为9。

###### 备注

- 调用`GzipFile`对象的`close()`方法不会关闭通过`fileobj`传入的文件。这允许在压缩数据之后向文件写入附加信息。
- 不支持UNIX `compress`程序生成的文件。
- 此模块需要`zlib`模块。

#### shutil

`shutil`模块用于执行高级文件操作，如复制、删除和重命名。此模块中的函数应仅用于正常的文件和目录。特别是，它们不适用于文件系统上的特殊类型文件，例如命名管道、块设备等。此外，请注意这些函数并不总是能正确处理高级文件元数据（例如资源分支、创建者代码等）。

```
copy(src, dst)
```

将文件`src`复制到文件或目录`dst`，保留文件权限。`src`和`dst`是字符串。

```
copy2(src, dst)
```

类似于`copy()`，但也会复制最后访问和修改时间。

```
copyfile(src, dst)
```

将`src`的内容复制到`dst`。`src`和`dst`是字符串。

```
copyfileobj(f1, f2 [, length])
```

将所有数据从打开的文件对象`f1`复制到打开的文件对象`f2`。`length`指定要使用的最大缓冲区大小。负长度将尝试通过一次操作完全复制数据（即所有数据将作为一个块读取，然后写入）。

```
copymode(src, dst)
```

将权限位从`src`复制到`dst`。

```
copystat(src, dst)
```

将权限位、最后访问时间和最后修改时间从`src`复制到`dst`。`dst`的内容、所有者和组不变。

```
copytree(src, dst, symlinks [, ignore])
```

递归复制以`src`为根的整个目录树。目标目录`dst`将被创建（且不应已存在）。单个文件使用`copy2()`复制。如果`symlinks`为真，则源树中的符号链接将在新树中表示为符号链接。如果`symlinks`为假或省略，则链接文件的内容将被复制到新目录树中。`ignore`是一个可选函数，可用于过滤特定文件。作为输入，该函数应接受一个目录名称和目录内容列表。作为返回值，它应返回要忽略的文件名列表。如果在复制过程中发生错误，它们将被收集，并在处理结束时引发`Error`异常。异常参数是一个元组列表，包含所有发生的错误的（`srcname`, `dstname`, `exception`）。

```
ignore_patterns(pattern1, pattern2, ...)
```

创建一个可用于忽略给定`pattern1`、`pattern2`等所有glob样式模式的函数。返回的函数接受两个参数，第一个是目录名称，第二个是目录内容列表。结果是返回一个要忽略的文件名列表。返回的函数的主要用途是作为前面所示的`copytree()`函数的`ignore`参数。但是，结果函数也可用于涉及`os.walk()`函数的操作。

```
move(src, dst)
```

将文件或目录*src*移动到*dst*。如果*src*被移动到不同的文件系统，则将递归复制*src*。

```
rmtree(path [, ignore_errors [, onerror]])
```

删除整个目录树。如果*ignore_errors*为真，则错误将被忽略。否则，错误由*onerror*函数（如果提供）处理。该函数必须接受三个参数（*func*、*path*和*excinfo*），其中*func*是导致错误的函数（`os.remove()`或`os.rmdir()`），*path*是传递给函数的路径名，*excinfo*是`sys.exc_info()`返回的异常信息。如果发生错误且省略*onerror*，则会引发异常。

#### tarfile

`tarfile`模块用于操作tar归档文件。使用此模块，可以读写tar文件，无论是否压缩。

```
is_tarfile(name)
```

如果*name*看起来是一个有效的tar文件，并且可以被此模块读取，则返回`True`。

```
open([name [, mode [, fileobj [, bufsize]]]])
```

创建一个新的`TarFile`对象，路径名为*name*。*mode*是指定如何打开tar文件的字符串。*mode*字符串是文件模式和压缩方案的组合，格式为`'filemode[:compression]'`。有效组合包括以下：

| 模式 | 描述 |
|------|-------------|
| `'r'` | 打开用于读取。如果文件已压缩，则透明地解压缩。这是默认模式。 |
| `'r:'` | 打开用于读取，不压缩。 |
| `'r:gz'` | 打开用于读取，使用gzip压缩。 |
| `'r:bz2'` | 打开用于读取，使用bzip2压缩。 |
| `'a'`, `'a:'` | 打开用于追加，不压缩。 |
| `'w'`, `'w:'` | 打开用于写入，不压缩。 |
| `'w:gz'` | 打开用于写入，使用gzip压缩。 |
| `'w:bz2'` | 打开用于写入，使用bzip2压缩。 |

以下模式用于创建仅允许顺序I/O访问（无随机定位）的`TarFile`对象：

| 模式 | 描述 |
|------|-------------|
| `'r\|'` | 打开一个未压缩块的流用于读取 |
| `'r\|gz'` | 打开一个gzip压缩的流用于读取 |
| `'r\|bz2'` | 打开一个bzip2压缩的流用于读取 |
| `'w\|'` | 打开一个未压缩的流用于写入 |
| `'w\|gz'` | 打开一个gzip压缩的流用于写入 |
| `'w\|bz2'` | 打开一个bzip2压缩的流用于写入 |



## 第18章 文件与目录处理

如果指定了参数 *fileobj*，它必须是一个已打开的文件对象。此时，文件对象会覆盖通过 *name* 指定的任何文件名。*bufsize* 指定 tar 文件中使用的块大小。默认值为 20*512 字节。

由 `open()` 返回的 TarFile 实例 *t* 支持以下方法和属性：

```
t.add(name [, arcname [, recursive]])
```

向 tar 归档添加新文件。*name* 可以是任何类型文件的名称（目录、符号链接等）。*arcname* 指定在归档中使用的文件替代名称。*recursive* 是一个布尔标志，指示是否递归添加目录内容。默认设置为 True。

```
t.addfile(tarinfo [, fileobj])
```

向 tar 归档添加新对象。*tarinfo* 是一个 TarInfo 结构，包含有关归档成员的信息。*fileobj* 是一个已打开的文件对象，将从其中读取数据并保存在归档中。读取的数据量由 *tarinfo* 的 size 属性决定。

```
t.close()
```

关闭 tar 归档。如果归档是以写入模式打开的，则会向末尾写入两个零块。

```
t.debug
```

控制生成的调试信息量，0 表示不产生输出，3 表示输出所有调试消息。消息写入 sys.stderr。

```
t.dereference
```

如果此属性设置为 True，符号链接和硬链接将被解引用，并且被引用文件的全部内容将添加到归档中。如果设置为 False，则只添加链接本身。

```
t.errorlevel
```

确定在提取归档成员时如何处理错误。如果此属性设置为 0，则忽略错误。如果设置为 1，错误会导致 OSError 或 IOError 异常。如果设置为 2，非致命错误还会额外引发 TarError 异常。

```
t.extract(member [, path])
```

从归档中提取成员，并将其保存到当前目录。*member* 可以是归档成员名称或 TarInfo 实例。*path* 用于指定不同的目标目录。

```
t.extractfile(member)
```

从归档中提取成员，返回一个只读的文件类对象，可用于使用 read()、readline()、readlines()、seek() 和 tell() 操作读取其内容。member 是归档成员名称或 TarInfo 对象。如果 *member* 引用的是链接，将尝试打开链接的目标。

```
t.getmember(name)
```

查找归档成员 *name* 并返回包含其信息的 TarInfo 对象。如果不存在这样的归档成员，则引发 KeyError。如果成员 *name* 在归档中出现多次，则返回最后一个条目的信息（假设其更近期）。

```
t.getmembers()
```

返回一个包含归档所有成员的 `TarInfo` 对象列表。

```
t.getnames()
```

返回所有归档成员名称的列表。

```
t.gettarinfo([name [, arcname [, fileobj]]])
```

返回一个与文件系统上的文件 `name` 或已打开的文件对象 `fileobj` 对应的 `TarInfo` 对象。`arcname` 是对象在归档中的替代名称。此函数的主要用途是创建适合在 `add()` 等方法中使用的 `TarInfo` 对象。

```
t.ignore_zeros
```

如果此属性设置为 `True`，则在读取归档时跳过空块。如果设置为 `False`（默认值），空块表示归档结束。将此方法设置为 `True` 可能有助于读取损坏的归档。

```
t.list([verbose])
```

将归档内容列到 `sys.stdout`。`verbose` 决定详细程度。如果此方法设置为 `False`，则只打印归档名称。否则，将打印完整详细信息（默认值）。

```
t.next()
```

用于遍历归档成员的方法。返回下一个归档成员的 `TarInfo` 结构或 `None`。

```
t.posix
```

如果此属性设置为 `True`，则根据 POSIX 1003.1-1990 标准创建 tar 文件。这会限制文件名长度和文件大小（文件名必须少于 256 个字符，文件大小必须小于 8GB）。如果此属性设置为 `False`，则使用解除这些限制的 GNU 扩展创建归档。默认值为 `False`。

前面的许多方法都操作 `TarInfo` 实例。下表显示了 `TarInfo` 实例 `ti` 的方法和属性。

| 属性 | 描述 |
|-----------|-------------|
| `ti.gid` | 组 ID |
| `ti.gname` | 组名 |
| `ti.isblk()` | 如果对象是块设备则返回 `True` |
| `ti.ischr()` | 如果对象是字符设备则返回 `True` |
| `ti.isdev()` | 如果对象是设备（字符、块或 FIFO）则返回 `True` |
| `ti.isdir()` | 如果对象是目录则返回 `True` |
| `ti.isfifo()` | 如果对象是 FIFO 则返回 `True` |
| `ti.isfile()` | 如果对象是常规文件则返回 `True` |
| `ti.islnk()` | 如果对象是硬链接则返回 `True` |
| `ti.isreg()` | 与 `isfile()` 相同 |
| `ti.issym()` | 如果对象是符号链接则返回 `True` |
| `ti.linkname` | 硬链接或符号链接的目标文件名 |
| `ti.mode` | 权限位 |
| `ti.mtime` | 最后修改时间 |
| `ti.name` | 归档成员名称 |
| `ti.size` | 大小（以字节为单位） |
| `ti.type` | 文件类型，是常量 REGTYPE、AREGTYPE、LNKTYPE、SYMTYPE、DIRTYPE、FIFOTYPE、CONTTYPE、CHRTYPE、BLKTYPE 或 GNUTYPE_SPARSE 之一 |
| `ti.uid` | 用户 ID |
| `ti.uname` | 用户名 |

##### 异常

tarfile 模块定义了以下异常：

###### TarError
所有其他异常的基类。

###### ReadError
打开 tar 文件时发生错误时引发（例如，打开无效文件时）。

###### CompressionError
无法解压数据时引发。

###### StreamError
在类流的 TarFile 对象上执行不支持的操作时引发（例如，需要随机访问的操作）。

###### ExtractError
提取期间发生非致命错误时引发（仅在 errorlevel 设置为 2 时）。

##### 示例

```python
###### 打开一个 tar 文件并向其中放入一些文件
t = tarfile.open("foo.tar","w")
t.add("README")
import glob
for pyfile in glob.glob("*.py"):
    t.add(pyfile)
t.close()

###### 打开一个 tar 文件并遍历其所有成员
t = tarfile.open("foo.tar")
for f in t:
    print("%s %d" % (f.name, f.size))

###### 扫描一个 tar 文件并打印 "README" 文件的内容
t = tarfile.open("foo.tar")
for f in t:
    if os.path.basename(f.name) == "README":
        data = t.extractfile(f).read()
        print("**** %s ****" % f.name)
```

##### tempfile

tempfile 模块用于生成临时文件名和文件。

`mkdtemp([suffix [,prefix [, dir]]])`

创建一个仅调用进程所有者可访问的临时目录，并返回其绝对路径名。suffix 是可选的后缀，将附加到目录名称；prefix 是可选的前缀，将插入到目录名称的开头；dir 是应创建临时目录的目录。

`mkstemp([suffix [,prefix [, dir [,text]]]])`

创建一个临时文件，并返回一个元组 (fd, pathname)，其中 fd 是由 os.open() 返回的整数文件描述符，pathname 是文件的绝对路径名。suffix 是附加到文件名的可选后缀，prefix 是插入到文件名开头的可选前缀，dir 是应创建文件的目录，text 是一个布尔标志，指示是以文本模式还是二进制模式（默认）打开文件。前提是系统支持 os.open() 的 O_EXCL 标志，则保证文件的创建是原子性的（且安全的）。

`mktemp([suffix [, prefix [,dir]]])`

返回一个唯一的临时文件名。suffix 是附加到文件名的可选文件后缀，prefix 是插入到文件名开头的可选前缀，dir 是创建文件的目录。此函数仅生成一个唯一的文件名，并不实际创建或打开临时文件。因为此函数在文件实际打开之前生成名称，所以会引入潜在的安全问题。为了解决这个问题，请考虑使用 mkstemp() 代替。

`gettempdir()`

返回创建临时文件的目录。

`gettempprefix()`

返回用于生成临时文件的前缀。不包括文件所在的目录。

`TemporaryFile([mode [, bufsize [, suffix [,prefix [, dir]]]]])`

使用 mkstemp() 创建一个临时文件，并返回一个文件类对象，该对象支持与普通文件对象相同的方法。mode 是文件模式，默认为 'w+b'。bufsize 指定缓冲行为，与 open() 函数具有相同的含义。suffix、prefix 和 dir 与 mkstemp() 具有相同的含义。此函数返回的对象只是内置文件对象的包装器，可通过 file 属性访问。此函数创建的文件在临时文件对象被销毁时会自动销毁。



##### tempfile

`NamedTemporaryFile([mode [, bufsize [, suffix [, prefix [, dir [, delete]]]]]])`

创建一个临时文件，与 `TemporaryFile()` 类似，但确保文件名在文件系统中可见。可以通过访问返回文件对象的 `name` 属性来获取文件名。请注意，在某些系统上，在临时文件关闭之前，可能无法使用此名称重新打开文件。如果将 `delete` 参数设置为 `True`（默认值），则会在关闭时强制删除临时文件。

`SpooledTemporaryFile([max_size [, mode [, bufsize [, suffix [, prefix [, dir]]]]]])`

创建一个临时文件，类似于 `TemporaryFile`，但文件内容完全保存在内存中，直到超过 `max_size` 指定的大小。这种内部缓冲通过先将文件内容保存在 `StringIO` 对象中来实现，直到需要实际访问文件系统。如果执行任何涉及 `fileno()` 方法的低级文件 I/O 操作，内存内容会立即写入由 `TemporaryFile` 对象定义的适当临时文件。`SpooledTemporaryFile` 返回的文件对象还有一个 `rollover()` 方法，可用于强制将内容写入文件系统。

使用两个全局变量来构建临时名称。可以根据需要为其赋新值。它们的默认值取决于系统。

| 变量 | 描述 |
|----------|-------------|
| tempdir | `mktemp()` 返回的文件名所在的目录。 |
| template | `mktemp()` 生成的文件名前缀。在 `template` 后添加一串十进制数字以生成唯一的文件名。 |

> **注意**
>
> 默认情况下，`tempfile` 模块通过检查几个标准位置来创建文件。例如，在 UNIX 系统中，文件在 `/tmp`、`/var/tmp` 或 `/usr/tmp` 之一中创建。在 Windows 系统中，文件在 `C:\TEMP`、`C:\TMP`、`\TEMP` 或 `\TMP` 之一中创建。可以通过设置 `TMPDIR`、`TEMP` 和 `TMP` 环境变量中的一个或多个来覆盖这些目录。如果由于任何原因无法在通常的位置创建临时文件，它们将在当前工作目录中创建。

#### zipfile

`zipfile` 模块用于操作流行的 zip 格式编码的文件（最初称为 PKZIP，但现在被多种程序支持）。Python 广泛使用 zip 文件，主要用于打包。例如，如果将包含 Python 源代码的 zip 文件添加到 `sys.path`，则可以通过 `import` 加载 zip 文件中包含的文件（`zipimport` 库模块实现了此功能，尽管通常不需要直接使用该库）。作为 `.egg` 文件分发的包（由 setuptools 扩展创建）也实际上是伪装的 zip 文件（`.egg` 文件实际上只是一个添加了一些额外元数据的 zip 文件）。

`zipfile` 模块定义了以下函数和类：

`is_zipfile(filename)`

测试 *filename* 是否为有效的 zip 文件。如果 *filename* 是 zip 文件，返回 `True`；否则返回 `False`。

`ZipFile(filename [, mode [, compression [,allowZip64]]])`

打开一个 zip 文件，*filename*，并返回一个 `ZipFile` 实例。*mode* 可以是 `'r'`（从现有文件读取）、`'w'`（截断文件并写入新文件）或 `'a'`（追加到现有文件）。对于 `'a'` 模式，如果 *filename* 是现有的 zip 文件，新文件将被添加到其中。如果 *filename* 不是 zip 文件，则只是将存档追加到文件末尾。*compression* 是写入存档时使用的 zip 压缩方法，可以是 `ZIP_STORED` 或 `ZIP_DEFLATED`。默认值是 `ZIP_STORED`。*allowZip64* 参数启用 ZIP64 扩展，可用于创建超过 2GB 的 zip 文件。默认情况下，此参数设置为 `False`。

`PyZipFile(filename [, mode[, compression [,allowZip64]]])`

打开一个 zip 文件，类似于 `ZipFile()`，但返回一个特殊的 `PyZipFile` 实例，该实例有一个额外的方法 `writepy()`，用于向存档中添加 Python 源文件。

`ZipInfo([filename [, date_time]])`

手动创建一个新的 `ZipInfo` 实例，用于包含有关存档成员的信息。通常，除了使用 `ZipFile` 实例的 `z.writestr()` 方法（稍后描述）外，不需要调用此函数。*filename* 和 *date_time* 参数提供了下面描述的 `filename` 和 `date_time` 属性的值。

`ZipFile` 或 `PyZipFile` 的实例 `z` 支持以下方法和属性：

`z.close()`

关闭存档文件。必须在程序终止前调用此方法以将记录刷新到 zip 文件。

`z.debug`

调试级别，范围从 0（无输出）到 3（最多输出）。

`z.extract(name [, path [, pwd]])`

从存档中提取文件并将其放置在当前工作目录中。*name* 可以是完全指定存档成员的字符串，也可以是 `ZipInfo` 实例。*path* 指定文件将被提取到的不同目录，*pwd* 是用于加密存档的密码。

`z.extractall([path [, members [, pwd]]])`

将存档的所有成员提取到当前工作目录。*path* 指定不同的目录，*pwd* 是用于加密存档的密码。*members* 是要提取的成员列表，必须是 `namelist()` 方法（接下来描述）返回的列表的适当子集。

`z.getinfo(name)`

返回有关存档成员 `name` 的信息，作为 `ZipInfo` 实例（稍后描述）。

`z.infolist()`

返回存档所有成员的 `ZipInfo` 对象列表。

`z.namelist()`

返回存档成员名称的列表。

`z.open(name [, mode [, pwd]])`

打开名为 `name` 的存档成员，并返回一个类似文件的对象用于读取内容。`name` 可以是字符串，也可以是描述存档成员之一的 `ZipInfo` 实例。`mode` 是文件模式，必须是只读文件模式之一，如 `'r'`、`'rU'` 或 `'U'`。`pwd` 是用于加密存档成员的密码。返回的文件对象支持 `read()`、`readline()` 和 `readlines()` 方法，以及使用 `for` 语句进行迭代。

`z.printdir()`

将存档目录打印到 `sys.stdout`。

`z.read(name [, pwd])`

读取成员 `name` 的存档内容，并将数据作为字符串返回。`name` 可以是描述存档成员的字符串或 `ZipInfo` 实例。`pwd` 是用于加密存档成员的密码。

`z.setpassword(pwd)`

设置用于从存档中提取加密文件的默认密码。

`z.testzip()`

读取存档中的所有文件并验证其 CRC 校验和。如果所有文件完好，返回第一个损坏文件的名称，否则返回 `None`。

`z.write(filename[, arcname[, compress_type]])`

将 `filename` 以存档名称 `arcname` 写入存档。`compress_type` 是压缩参数，可以是 `ZIP_STORED` 或 `ZIP_DEFLATED`。默认情况下，使用传递给 `ZipFile()` 或 `PyZipFile()` 函数的压缩参数。存档必须以 `'w'` 或 `'a'` 模式打开，写入才能生效。

`z.writepy(pathname)`

此方法仅适用于 `PyZipFile` 实例，用于将 Python 源文件（`*.py` 文件）写入 zip 存档，可用于轻松打包 Python 应用程序以供分发。如果 `pathname` 是一个文件，它必须以 `.py` 结尾。在这种情况下，将添加相应的 `.pyo`、`.pyc` 或 `.py` 文件之一（按此顺序）。如果 `pathname` 是一个目录且该目录不是 Python 包目录，则所有相应的 `.pyo`、`.pyc` 或 `.py` 文件都添加到顶层。如果该目录是一个包，则文件作为文件路径添加到包名下。如果任何子目录也是包目录，则递归添加。

`z.writestr(arcinfo, s)`

将字符串 `s` 写入 zip 文件。`arcinfo` 可以是存档中用于存储数据的文件名，也可以是包含文件名、日期和时间的 `ZipInfo` 实例。

`ZipInfo()`、`z.getinfo()` 和 `z.infolist()` 函数返回的 `ZipInfo` 实例 `i` 具有以下属性：

| 属性 | 描述 |
|-----------|-------------|
| `i.filename` | 存档成员名称。 |
| `i.date_time` | 包含最后修改时间的元组 `(year, month, day, hours, minutes, seconds)`。*month* 和 *day* 分别是范围在 1–12 和 1–31 的数字。所有其他值从 0 开始。 |
| `i.compress_type` | 存档成员的压缩类型。目前本模块仅支持 `ZIP_STORED` 和 `ZIP_DEFLATED`。 |
| `i.comment` | 存档成员注释。 |
| `i.extra` | 扩展字段数据，用于包含额外的文件属性。此处存储的数据取决于创建文件的系统。 |
| `i.create_system` | 描述创建存档的系统的整数代码。常见值为 0（MS-DOS FAT）、3（UNIX）、7（Macintosh）和 10（Windows NTFS）。 |
| `i.create_version` | 创建 zip 存档的 PKZIP 版本代码。 |
| `i.extract_version` | 提取存档所需的最低版本。 |
| `i.reserved` | 保留字段。当前设置为 0。 |
| `i.flag_bits` | 描述数据编码（包括加密和压缩）的 Zip 标志位。 |
| `i.volume` | 文件头的卷号。 |
| `i.internal_attr` | 描述存档内容的内部结构。如果最低位为 1，则数据是 ASCII 文本。否则，假定为二进制数据。 |
| `i.external_attr` | 外部文件属性，取决于操作系统。 |
| `i.header_offset` | 文件头的字节偏移量。 |
| `i.file_offset` | 文件数据起始位置的字节偏移量。 |
| `i.CRC` | 未压缩文件的 CRC 校验和。 |
| `i.compress_size` | 压缩文件数据的大小。 |
| `i.file_size` | 未压缩文件的大小。 |

> **注意**
>
> 关于 zip 文件内部结构的详细文档可以在 http://www.pkware.com/appnote.html 找到，作为 PKZIP 应用说明。



#### zlib

`zlib` 模块通过提供对 zlib 库的访问来支持数据压缩。

`adler32(string [, value])`

计算 `string` 的 Adler-32 校验和。`value` 用作起始值（可用于计算多个字符串连接的校验和）。否则，将使用一个固定的默认值。

`compress(string [, level])`

压缩 `string` 中的数据，其中 `level` 是从 1 到 9 的整数，用于控制压缩级别。1 是最小（最快）压缩，9 是最佳（最慢）压缩。默认值为 6。返回包含压缩数据的字符串，如果发生错误则引发 `error`。

`compressobj([level])`

返回一个压缩对象。`level` 与 `compress()` 函数中的含义相同。

`crc32(string [, value])`

计算 `string` 的 CRC 校验和。如果提供了 `value`，则将其用作校验和的起始值。否则，使用一个固定的值。

`decompress(string [, wbits [, bufsize]])`

解压 `string` 中的数据。`wbits` 控制窗口缓冲区的大小，`bufsize` 是输出缓冲区的初始大小。如果发生错误则引发 `error`。

`decompressobj([wbits])`

返回一个压缩对象。`wbits` 参数控制窗口缓冲区的大小。

一个压缩对象，*c*，具有以下方法：

`c.compress(string)`

压缩 *string*。返回一个包含至少部分 *string* 数据的压缩数据的字符串。此数据应与之前调用 `c.compress()` 产生的输出连接起来以创建输出流。某些输入数据可能会存储在内部缓冲区中以供后续处理。

`c.flush([mode])`

压缩所有待处理的输入，并返回一个包含剩余压缩输出的字符串。`mode` 是 `Z_SYNC_FLUSH`、`Z_FULL_FLUSH` 或 `Z_FINISH`（默认值）。`Z_SYNC_FLUSH` 和 `Z_FULL_FLUSH` 允许进一步压缩，并用于在解压时进行部分错误恢复。`Z_FINISH` 终止压缩流。

一个解压缩对象，*d*，具有以下方法和属性：

`d.decompress(string [, max_length])`

解压 *string* 并返回一个包含至少部分 *string* 数据的未压缩数据的字符串。此数据应与之前调用 `decompress()` 产生的数据连接起来以形成输出流。某些输入数据可能会存储在内部缓冲区中以供后续处理。`max_length` 指定返回数据的最大大小。如果超出，未处理的数据将放置在 `d.unconsumed_tail` 属性中。

`d.flush()`

处理所有待处理的输入，并返回一个包含剩余未压缩输出的字符串。调用此方法后，解压缩对象无法再次使用。

`d.unconsumed_tail`

包含尚未由最后一次 `decompress()` 调用处理的数据的字符串。如果由于缓冲区大小限制需要分阶段执行解压缩，则会包含数据。在这种情况下，此变量将传递给后续的 `decompress()` 调用。

`d.unused_data`

包含压缩数据末尾之后的额外字节的字符串。

###### 注意

zlib 库可在 http://www.zlib.net 获取。

## 操作系统服务

本章中的模块提供了对各种操作系统服务的访问，重点是低级 I/O、进程管理和操作环境。还包括了编写系统程序时常用的模块——例如，用于读取配置文件、写入日志文件等的模块。第 18 章“文件和目录处理”涵盖了与文件和文件系统操作相关的高级模块——此处介绍的内容往往级别更低。

大多数 Python 的操作系统模块基于 POSIX 接口。POSIX 是一个定义了一组核心操作系统接口的标准。大多数 UNIX 系统支持 POSIX，而其他平台（如 Windows）支持该接口的大部分。在本章中，仅适用于特定平台的功能和模块会加以说明。UNIX 系统包括 Linux 和 Mac OS X。除非另有说明，Windows 系统包括所有版本的 Windows。

读者可能希望用额外的参考资料来补充此处介绍的内容。Brian W. Kernighan 和 Dennis M. Ritchie 的《C 程序设计语言》第二版（Prentice Hall，1989 年）提供了文件、文件描述符以及本节中许多模块所基于的低级接口的良好概述。更高级的读者可能希望参考 W. Richard Stevens 和 Stephen Rago 的《UNIX 环境高级编程》第二版（Addison Wesley，2005 年）这样的书籍。对于一般概念的概述，你可能希望找一本关于操作系统的大学教科书。然而，考虑到这些书价格高昂且日常实用价值有限，你最好向附近的计算机科学学生借一本，用上一个周末。

#### commands

`commands` 模块用于执行作为字符串指定的简单系统命令，并将其输出作为字符串返回。它仅在 UNIX 系统上工作。此模块提供的功能与在 UNIX shell 脚本中使用反引号（`）有些相似。例如，输入 `x = commands.getoutput('ls -l')` 类似于说 `x='ls -l'`。

`getoutput(cmd)`

在 shell 中执行 *cmd*，并返回一个包含命令的标准输出和标准错误流的字符串。

`getstatusoutput(cmd)`

类似于 getoutput()，但返回一个二元组（状态，输出），其中状态是退出代码（由 os.wait() 函数返回），输出是 getoutput() 返回的字符串。

###### 注意

- 此模块仅在 Python 2 中可用。在 Python 3 中，上述两个函数都在 `subprocess` 模块中找到。
- 虽然此模块可用于简单的 shell 操作，但你几乎总是最好使用 `subprocess` 模块来启动子进程并收集其输出。

> 另请参阅：
> subprocess（第 402 页）

#### ConfigParser, configparser

`ConfigParser` 模块（在 Python 3 中称为 `configparser`）用于读取基于 Windows INI 格式的 .ini 格式配置文件。这些文件由命名部分组成，每个部分都有自己的变量赋值，如下所示：

```
###### A comment
; A comment
[section1]
name1 = value1
name2 = value2

[section2]
; Alternative syntax for assigning values
name1: value1
name2: value2
...
```

##### ConfigParser 类

以下类用于管理配置变量：

`ConfigParser([defaults [, dict_type]])`

创建一个新的 ConfigParser 实例。defaults 是一个可选的字典值，可以通过包含字符串格式说明符（如 `'%(key)s'`，其中 key 是 defaults 的一个键）在配置变量中引用。dict_type 指定内部用于存储配置变量的字典类型。默认情况下，它是 dict（内置字典）。

ConfigParser 的一个实例 `c` 具有以下操作：

`c.add_section(section)`

向存储的配置参数添加一个新的部分。section 是部分名称的字符串。

`c.defaults()`

返回默认值的字典。

`c.get(section, option [, raw [, vars]])`

以字符串形式返回部分 `section` 中选项 `option` 的值。默认情况下，返回的字符串通过一个插值步骤处理，其中像 `'%(option)s'` 这样的格式字符串会被展开。在这种情况下，`option` 可以是同一部分中的另一个配置选项的名称，或者是 `ConfigParser` 的 *defaults* 参数中提供的默认值之一。`raw` 是一个布尔标志，用于禁用此插值功能，返回未修改的选项。`vars` 是一个可选的字典，包含更多用于 `'%'` 展开的值。

`c.getboolean(section, option)`

返回部分 `section` 中 `option` 的值，并转换为布尔值。诸如 `"0"`、`"true"`、`"yes"`、`"no"`、`"on"` 和 `"off"` 等值都会被理解并以不区分大小写的方式检查。此方法始终执行变量插值（请参见 `c.get()`）。

`c.getfloat(section, option)`

返回部分 `section` 中 `option` 的值，并带变量插值转换为浮点数。

`c.getint(section, option)`

返回部分 `section` 中 `option` 的值，并带变量插值转换为整数。

`c.has_option(section, option)`

如果部分 `section` 有一个名为 `option` 的选项，则返回 `True`。

`c.has_section(section)`

如果存在一个名为 `section` 的部分，则返回 `True`。

`c.items(section [, raw [, vars]])`

返回部分 `section` 中的 `(option, value)` 对列表。`raw` 是一个布尔标志，如果设置为 `True`，则禁用插值功能。`vars` 是一个可用于 `'%'` 展开的额外值的字典。

`c.options(section)`

返回部分 `section` 中所有选项的列表。

`c.optionxform(option)`

将选项名称 `option` 转换为用于引用该选项的字符串。默认情况下，这是小写转换。

`c.read(filenames)`

从文件名列表中读取配置选项并存储它们。`filenames` 可以是单个字符串（在这种情况下，该字符串就是要读取的文件名），也可以是文件名列表。如果找不到任何给定的文件名，则忽略它们。当你要从多个可能的位置读取配置文件，但这些文件可能存在也可能未定义时，这很有用。返回成功解析的文件名列表。



`c.readfp(fp [, filename])`

从一个已打开的类文件对象 `fp` 中读取配置选项。`filename` 指定与 `fp` 关联的文件名（如果有）。默认情况下，文件名取自 `fp.name`，如果该属性未定义，则设为 `<???>`。

`c.remove_option(section, option)`

从 `section` 节中移除 `option` 选项。

`c.remove_section(section)`

移除 `section` 节。

`c.sections()`

返回所有节的名称列表。

`c.set(section, option, value)`

在 `section` 节中将配置选项 `option` 设置为 `value`。`value` 应为字符串。

`c.write(file)`

将当前所有配置数据写入 `file`。`file` 是一个已打开的类文件对象。

##### 示例

`ConfigParser` 模块常被忽视，但它对于控制具有极其复杂的用户配置或运行时环境的程序来说，是一个非常有用的工具。例如，如果你正在编写一个需要在大型框架内运行的组件，配置文件通常是提供运行时参数的一种优雅方式。同样，与让程序使用 `optparse` 模块读取大量命令行选项相比，配置文件可能是一种更优雅的解决方案。使用配置文件与仅从 Python 源代码脚本读取配置数据之间也存在细微但重要的差异。

以下示例说明了 `ConfigParser` 模块一些更有趣的功能。首先，考虑一个示例 `.ini` 文件：

```
###### appconfig.ini
###### 我的大型应用程序的配置文件

[output]
LOGFILE=%(LOGDIR)s/app.log
LOGGING=on
LOGDIR=%(BASEDIR)s/logs

[input]
INFILE=%(INDIR)s/initial.dat
INDIR=%(BASEDIR)s/input
```

以下代码说明了如何读取配置文件并为某些变量提供默认值：

```
from configparser import ConfigParser  # 在 Python 2 中使用 from ConfigParser

###### 默认变量设置的字典
defaults = {
    'basedir' : '/Users/beazley/app'
}

###### 创建一个 ConfigParser 对象并读取 .ini 文件
cfg = ConfigParser(defaults)
cfg.read('appconfig.ini')
```

读取配置文件后，你可以使用 `get()` 方法来检索选项值。例如：

```
>>> cfg.get('output','logfile')
'/Users/beazley/app/logs/app.log'
>>> cfg.get('input','infile')
'/Users/beazley/app/input/initial.dat'
>>> cfg.getboolean('output','logging')
True
>>>
```

在这里，你立即会看到一些有趣的功能。首先，配置参数不区分大小写。因此，如果你的程序读取参数 `'logfile'`，配置文件中使用 `'logfile'`、`'LOGFILE'` 还是 `'LogFile'` 都无关紧要。其次，配置参数可以包含变量替换，例如文件中看到的 `'%(BASEDIR)s'` 和 `'%(LOGDIR)s'`。这些替换同样不区分大小写。此外，配置参数的定义顺序在这些替换中并不重要。例如，在 `appconfig.ini` 中，`LOGFILE` 参数引用了 `LOGDIR` 参数，而该参数在文件中稍后定义。最后，即使配置文件中的值不完全匹配 Python 语法或数据类型，也通常会被正确解释。例如，`LOGGING` 参数的值 `'on'` 被 `cfg.getboolean()` 方法解释为 `True`。

配置文件还具有合并的能力。例如，假设用户有自己的配置文件，其中包含自定义设置：

```
; userconfig.ini
;
; 用户级设置

[output]
logging=off

[input]
BASEDIR=/tmp
```

你可以将此文件的内容与已加载的配置参数合并。例如：

```
>>> cfg.read('userconfig.ini')
['userconfig.ini']
>>> cfg.get('output','logfile')
'/Users/beazley/app/logs/app.log'
>>> cfg.get('output','logging')
'off'
>>> cfg.get('input','infile')
'/tmp/input/initial.dat'
>>>
```

在这里，你会注意到新加载的配置有选择性地替换了已定义的参数。此外，如果你更改了用于其他配置参数变量替换的某个配置参数，更改会正确传播。例如，`input` 节中 `BASEDIR` 的新设置会影响该节中先前定义的配置参数，如 `INFILE`。这种行为是使用配置文件与仅在 Python 脚本中定义一组程序参数之间一个细微但重要的区别。

###### 注意

还有两个其他类可以替代 `ConfigParser` 使用。`RawConfigParser` 类提供了 `ConfigParser` 的所有功能，但不执行任何变量插值。`SafeConfigParser` 类提供了与 `ConfigParser` 相同的功能，但它解决了一些微妙的问题，这些问题出现在配置值本身字面上包含插值功能使用的特殊格式化字符（例如，`'%'`）时。

#### `datetime`

`datetime` 模块提供了各种类来表示和操作日期和时间。该模块的很大一部分与创建和输出日期及时间信息的不同方式有关。其他主要功能包括数学运算，如比较和计算时间增量。日期操作是一个复杂的主题，强烈建议读者查阅 Python 的在线文档，以获取有关此模块设计的入门背景知识。

##### `date` 对象

一个 `date` 对象表示一个简单的日期，包含年、月和日。以下四个函数用于创建日期：

```
date(year, month, day)
```

创建一个新的日期对象。`year` 是一个范围在 `datetime.MINYEAR` 到 `datetime.MAXYEAR` 之间的整数。`month` 是一个范围在 1 到 12 之间的整数，`day` 是一个范围在 1 到给定月份天数之间的整数。返回的 `date` 对象是不可变的，并具有对应于所提供参数值的 `year`、`month` 和 `day` 属性。

```
date.today()
```

一个类方法，返回一个对应于当前日期的 `date` 对象。

```
date.fromtimestamp(timestamp)
```

一个类方法，返回一个对应于时间戳 `timestamp` 的 `date` 对象。`timestamp` 是 `time.time()` 函数返回的值。

```
date.fromordinal(ordinal)
```

一个类方法，返回一个对应于从最小允许日期（公元1年1月1日的序数为1，2006年1月1日的序数为733312）起的 *序数* 天数的 `date` 对象。

以下类属性描述了日期实例的最大速率和分辨率。

```
date.min
```

代表可表示的最早日期的类属性 (datetime.date(1,1,1))。

```
date.max
```

代表可能的最晚日期的类属性 (datetime.date(9999,12,31))。

```
date.resolution
```

非相等日期对象之间最小的可分辨差异 (datetime.timedelta(1))。

一个 `date` 的实例 `d` 具有只读属性 `d.year`、`d.month` 和 `d.day`，并额外提供以下方法：

```
d.ctime()
```

返回一个表示日期的字符串，其格式与 `time.ctime()` 函数通常使用的格式相同。

```
d.isocalendar()
```

将日期作为元组 (iso_year, iso_week, iso_weekday) 返回，其中 `iso_week` 的范围是 1 到 53，`iso_weekday` 的范围是 1（星期一）到 7（星期日）。第一个 iso_week 是包含星期四的年份的第一周。这三个元组组件的值范围由 ISO 8601 标准确定。

```
d.isoformat()
```

返回一个 ISO 8601 格式的字符串，形式为 'YYYY-MM-DD'，表示该日期。

```
d.isoweekday()
```

返回星期几，范围为 1（星期一）到 7（星期日）。

```
d.replace([year [, month [, day ]]])
```

返回一个新的日期对象，其中提供的一个或多个组件被新值替换。例如，`d.replace(month=4)` 返回一个月份被替换为 4 的新日期。

```
d.strftime(format)
```

返回一个根据与 `time.strftime()` 函数相同规则格式化的日期字符串。此函数仅适用于 1900 年以后的日期。此外，不应使用针对 `date` 对象中缺失组件（如小时、分钟等）的格式化代码。

```
d.timetuple()
```

返回一个适合 `time` 模块中函数使用的 `time.struct_time` 对象。与一天中的时间相关的值（小时、分钟、秒）将被设置为 0。

```
d.toordinal()
```

将 `d` 转换为一个序数值。公元1年1月1日的序数为 1。



**d.weekday()**

返回星期几，范围为 0（星期一）到 6（星期日）。

##### **time 对象**

time 对象用于表示以小时、分钟、秒和微秒为单位的时间。时间通过以下类构造函数创建：

```
time(hour [, minute [, second [, microsecond [, tzinfo]]])
```

创建一个 time 对象，表示一个时间，其中 0 <= hour < 24，0 <= minute < 60，0 <= second < 60，0 <= microsecond < 1000000。tzinfo 提供时区信息，是本节后面描述的 tzinfo 类的实例。返回的 time 对象具有属性 hour、minute、second、microsecond 和 tzinfo，它们保存作为参数提供的相应值。

time 的以下类属性描述了允许的值范围和 time 实例的分辨率：

```
time.min
```

表示可表示的最小时间的类属性（datetime.time(0, 0)）。

```
time.max
```

表示可表示的最大时间的类属性（datetime.time(23, 59, 59, 999999)）。

```
time.resolution
```

不相等的 time 对象之间可分辨的最小差异（datetime.timedelta(0, 0, 1)）。

time 对象的实例 `t` 具有属性 t.hour、t.minute、t.second、t.microsecond 和 t.tzinfo，以及以下方法：

```
t.dst()
```

返回 `t.tzinfo.dst(None)` 的值。返回的对象是一个 timedelta 对象。如果未设置时区，则返回 `None`。

```
t.isoformat()
```

返回一个字符串，表示时间为 'HH:MM:SS.mmmmmm'。如果微秒为 0，则省略该部分字符串。如果已提供时区信息，则时间可能会添加偏移量（例如 'HH:MM:SS.mmmmmm+HH:MM'）。

```
t.replace([hour [, minute [, second [, microsecond [, tzinfo ]]]])
```

返回一个新的 time 对象，其中一个或多个组件已被提供的值替换。例如，t.replace(second=30) 将秒字段更改为 30 并返回一个新的 time 对象。参数与前面所示的 time() 函数提供的参数含义相同。

```
t.strftime(format)
```

返回一个按照 time 模块中 time.strftime() 函数相同规则格式化的字符串。由于日期信息不可用，应仅使用与时间相关的格式化代码。

```
t.tzname()
```

返回 `t.tzinfo.tzname()` 的值。如果未设置时区，则返回 `None`。

```
t.utcoffset()
```

返回 `t.tzinfo.utcoffset(None)` 的值。返回的对象是一个 `timedelta` 对象。如果未设置时区，则返回 `None`。

##### datetime 对象

`datetime` 对象用于同时表示日期和时间。创建 `datetime` 实例有多种可能的方式：

```
datetime(year, month, day [, hour [, minute [, second [, microsecond [, tzinfo]]]]])
```

```
datetime.combine(date, time)
```

一个类方法，通过组合 `date` 对象 `date` 和 `time` 对象 `time` 的内容来创建 `datetime` 对象。

```
datetime.fromordinal(ordinal)
```

一个类方法，给定一个序数日（自 `datetime.min` 以来的整数天数）创建一个 `datetime` 对象。时间分量全部设置为 `0`，`tzinfo` 设置为 `None`。

```
datetime.fromtimestamp(timestamp [, tz])
```

一个类方法，从 `time.time()` 函数返回的时间戳创建一个 `datetime` 对象。`tz` 提供可选的时区信息，是一个 `tzinfo` 实例。

```
datetime.now([tz])
```

一个类方法，从当前本地日期和时间创建一个 `datetime` 对象。`tz` 提供可选的时区信息，是 `tzinfo` 的实例。

```
datetime.strptime(datestring, format)
```

一个类方法，通过按照 `format` 中的日期格式解析 `datestring` 中的日期字符串来创建 `datetime` 对象。解析使用 `time` 模块中的 `strptime()` 函数执行。

```
datetime.utcfromtimestamp(timestamp)
```

一个类方法，从 `time.gmtime()` 通常返回的时间戳创建一个 `datetime` 对象。

```
datetime.utcnow()
```

一个类方法，从当前 UTC 日期和时间创建一个 `datetime` 对象。

以下类属性描述了允许的日期范围和分辨率：

**datetime.min**

可表示的最早日期和时间（`datetime.datetime(1,1,1,0,0)`）。

**datetime.max**

可表示的最晚日期和时间（`datetime.datetime(9999,12,31,23,59,59,999999)`）。

**datetime.resolution**

不相等的 datetime 对象之间可分辨的最小差异（`datetime.timedelta(0,0,1)`）。

datetime 对象的实例 *d* 具有 date 和 time 对象组合的相同方法。此外，以下方法可用：

**d.astimezone(*tz*)**

返回一个新的 datetime 对象，但在不同时区 *tz* 中。新对象的成员将被调整为表示相同的 UTC 时间，但在时区 *tz* 中。

**d.date()**

返回具有相同日期的 date 对象。

```
d.replace([year [, month [, day [, hour [, minute [, second [, microsecond [, tzinfo]]]]]]])
```

返回一个新的 datetime 对象，其中列出的一个或多个参数被新值替换。使用关键字参数替换单个值。

**d.time()**

返回具有相同时间的 time 对象。结果 time 对象未设置时区信息。

**d.timetz()**

返回具有相同时间和时区信息的 time 对象。

**d.utctimetuple()**

返回一个 `time.struct_time` 对象，包含规范化为 UTC 时间的日期和时间信息。

##### timedelta 对象

timedelta 对象表示两个日期或时间之间的差值。这些对象通常是使用 `-` 运算符计算两个 datetime 实例之间的差值的结果。但是，可以使用以下类手动构造它们：

```
timedelta([days [, seconds [, microseconds [, milliseconds [, minutes [, hours [, weeks ]]]]]]])
```

创建一个 timedelta 对象，表示两个日期和时间之间的差值。唯一重要的参数是 *days*、*seconds* 和 *microseconds*，它们在内部用于表示差值。其他参数（如果提供）会被转换为天、秒和微秒。返回的 timedelta 对象的属性 days、seconds 和 microseconds 包含这些值。

以下类属性描述了 `timedelta` 实例的最大范围和分辨率：

###### timedelta.min

可表示的最负的 `timedelta` 对象（`timedelta(-999999999)`）。

###### timedelta.max

可表示的最正的 `timedelta` 对象（`timedelta(days=999999999, hours=23, minutes=59, seconds=59, microseconds=999999)`）。

###### timedelta.resolution

表示不相等的 `timedelta` 对象之间可分辨的最小差异的 `timedelta` 对象（`timedelta(microseconds=1)`）。

##### 涉及日期的数学运算

`datetime` 模块的一个重要特性是它支持涉及日期的数学运算。`date` 和 `datetime` 对象都支持以下操作：

| 操作 | 描述 |
|-----------|-------------|
| `td = date1 - date2` | 返回一个 `timedelta` 对象 |
| `date2 = date1 + td` | 将 `timedelta` 加到日期上 |
| `date2 = date1 - td` | 从日期中减去 `timedelta` |
| `date1 < date2` | 日期比较 |
| `date1 <= date2` |  |
| `date1 == date2` |  |
| `date1 != date2` |  |
| `date1 > date2` |  |
| `date1 >= date2` |  |

比较日期时，如果已提供时区信息，必须谨慎处理。如果日期包含 `tzinfo` 信息，则该日期只能与其他包含 `tzinfo` 的日期进行比较；否则，将生成 `TypeError`。比较两个不同时区的日期时，它们会先调整为 UTC，然后再进行比较。

`timedelta` 对象也支持各种数学运算：

| 操作 | 描述 |
|-----------|-------------|
| `td3 = td2 + td1` | 两个时间差相加 |
| `td3 = td2 - td1` | 两个时间差相减 |
| `td2 = td1 * i` | 与整数相乘 |
| `td2 = i * td2` |  |
| `td2 = td1 // i` | 与整数 `i` 进行整除 |
| `td2 = -td1` | 一元减法、加法 |
| `td2 = +td1` |  |
| `abs(td)` | 绝对值 |

操作 | 描述
--- | ---
td1 < td2 | 比较
td1 <= td2 | 
td1 == td2 | 
td1 != td2 | 
td1 > td2 | 
td1 >= td2 | 

这里有一些示例：

```
>>> today = datetime.datetime.now()
>>> today.ctime()
'Thu Oct 20 11:10:10 2005'
>>> oneday = datetime.timedelta(days=1)
>>> tomorrow = today + oneday
>>> tomorrow.ctime()
'Fri Oct 21 11:10:10 2005'
>>>
```

除了这些操作，所有 `date`、`datetime`、`time` 和 `timedelta` 对象都是不可变的。这意味着它们可以用作字典的键，放入集合中，并用于各种其他操作。

##### `tzinfo` 对象

`datetime` 模块中的许多方法都操作特殊的 `tzinfo` 对象，这些对象表示有关时区的信息。`tzinfo` 只是一个基类。各个时区是通过继承 `tzinfo` 并实现以下方法来创建的：

**`tz.dst(dt)`**
返回一个表示夏令时调整（如果适用）的 `timedelta` 对象。如果对夏令时没有已知信息，则返回 `None`。参数 `dt` 是一个 `datetime` 对象或 `None`。

**`tz.fromutc(dt)`**
将 `datetime` 对象 `dt` 从 UTC 时间转换为本地时区，并返回一个新的 `datetime` 对象。此方法由 `datetime` 对象上的 `asctime()` 方法调用。`tzinfo` 已经提供了一个默认实现，因此通常不需要重新定义此方法。

**`tz.tzname(dt)`**
返回一个包含时区名称的字符串（例如，`"US/Central"`）。`dt` 是一个 `datetime` 对象或 `None`。

**`tz.utcoffset(dt)`**
返回一个 `timedelta` 对象，表示本地时间相对于 UTC 的偏移量（以东为正方向，单位为分钟）。该偏移量包含了构成本地时间的所有元素，包括夏令时（如果适用）。参数 `dt` 是一个 `datetime` 对象或 `None`。

以下示例展示了如何定义时区的基本原型：

```
###### 必须定义的变量
# TZOFFSET  - 相对于 UTC 的时区偏移量（小时）。例如，美国中部标准时间是 -6 小时。
# DSTNAME   - 夏令时生效时的时区名称
# STDNAME   - 夏令时未生效时的时区名称

class SomeZone(datetime.tzinfo):
    def utcoffset(self,dt):
        return datetime.timedelta(hours=TZOFFSET) + self.dst(dt)
    def dst(self,dt):
                # is_dst() 是一个你必须实现的函数，用于根据本地时区规则
                # 判断夏令时是否生效。
        if is_dst(dt):
            return datetime.timedelta(hours=1)
        else:
            return datetime.timedelta(0)
    def tzname(self,dt):
        if is_dst(dt):
            return DSTNAME
        else:
            return STDNAME
```

在 `datetime` 的在线文档中也可以找到许多定义时区的示例。

##### 日期和时间解析

日期处理中常见的一个问题是，如何将不同种类的时间和日期字符串解析为合适的 `datetime` 对象。`datetime` 模块真正提供的唯一解析函数是 `datetime.strptime()`。但是，要使用它，你需要使用各种格式代码的组合来指定精确的日期格式（参见 `time.strptime()`）。例如，要解析日期字符串 `s="Aug 23, 2008"`，你需要使用 `d = datetime.datetime.strptime(s, "%b %d, %Y")`。

要实现“模糊”日期解析，即自动理解多种常见日期格式，你必须借助第三方模块。访问 Python 包索引（http://pypi.python.org）并搜索“datetime”，可以找到各种各样的实用模块，它们扩展了 `datetime` 模块的功能集。

> **另请参阅：**
> `time`（第 405 页）

#### `errno`

`errno` 模块为各种操作系统调用返回的整数错误代码定义了符号名称，特别是在 `os` 和 `socket` 模块中找到的那些调用。这些代码通常可以在 `OSError` 或 `IOError` 异常的 `errno` 属性中找到。`os.strerror()` 函数可用于将错误代码转换为字符串错误消息。以下字典也可用于将整数错误代码转换为其符号名称：

**errorcode**

此字典将 `errno` 整数映射到符号名称（例如 `'EPERM'`）。

##### POSIX 错误代码

下表显示了常见系统错误代码的 POSIX 符号名称。此处列出的错误代码几乎在所有版本的 UNIX、Macintosh OS-X 和 Windows 上都受支持。不同的 UNIX 系统可能提供此处未列出的较少见的其他错误代码。如果发生此类错误，你可以查阅 `errorcode` 字典以找到合适的符号名称用于你的程序中。

| 错误代码 | 描述 |
|---|---|
| E2BIG | 参数列表过长。 |
| EACCES | 权限被拒绝。 |
| EADDRINUSE | 地址已在使用中。 |
| EADDRNOTAVAIL | 无法分配请求的地址。 |
| EAFNOSUPPORT | 协议不支持的地址族。 |
| EAGAIN | 请稍后重试。 |
| EALREADY | 操作已在进行中。 |
| EBADF | 无效的文件描述符。 |
| EBUSY | 设备或资源忙。 |
| ECHILD | 没有子进程。 |
| ECONNABORTED | 软件引起的连接中止。 |
| ECONNREFUSED | 连接被拒绝。 |
| ECONNRESET | 连接被对端重置。 |
| EDEADLK | 将发生资源死锁。 |
| EDEADLOCK | 文件锁定死锁错误。 |
| EDESTADDRREQ | 需要目标地址。 |
| EDOM | 数学参数超出函数定义域。 |
| EDQUOT | 超出配额。 |
| EEXIST | 文件已存在。 |
| EFAULT | 无效的地址。 |
| EFBIG | 文件过大。 |
| EHOSTDOWN | 主机已关闭。 |
| EHOSTUNREACH | 无法到达主机。 |
| EILSEQ | 非法的字节序列。 |
| EINPROGRESS | 操作现在正在进行中。 |
| EINTR | 系统调用被中断。 |
| EINVAL | 无效的参数。 |
| EIO | 输入/输出错误。 |
| EISCONN | 传输端点已连接。 |
| EISDIR | 是一个目录。 |
| ELOOP | 遇到过多的符号链接。 |
| EMFILE | 打开的文件过多。 |
| EMLINK | 链接过多。 |
| EMSGSIZE | 消息过长。 |
| ENETDOWN | 网络已关闭。 |
| ENETRESET | 网络因重置而断开连接。 |
| ENETUNREACH | 网络不可达。 |
| ENFILE | 文件表溢出。 |
| ENOBUFS | 没有可用的缓冲区空间。 |
| ENODEV | 没有此设备。 |
| ENOENT | 没有此文件或目录。 |
| ENOEXEC | 可执行文件格式错误。 |
| ENOLCK | 没有可用的记录锁。 |
| ENOMEM | 内存不足。 |
| ENOPROTOOPT | 协议不可用。 |
| ENOSPC | 设备上没有空间。 |
| ENYSYS | 功能未实现。 |
| ENOTCONN | 传输端点未连接。 |
| ENOTDIR | 不是目录。 |
| ENOTEMPTY | 目录非空。 |
| ENOTSOCK | 在非套接字上进行套接字操作。 |
| ENOTTY | 不是终端。 |
| ENXIO | 没有此设备或地址。 |
| EOPNOTSUPP | 传输端点不支持该操作。 |
| EPERM | 操作不允许。 |
| EPFNOSUPPORT | 不支持的协议族。 |
| EPIPE | 管道破裂。 |
| EPROTONOSUPPORT | 不支持的协议。 |
| EPROTOTYPE | 套接字的协议类型错误。 |
| ERANGE | 数学结果无法表示。 |
| EREMOTE | 对象是远程的。 |
| EROFS | 只读文件系统。 |
| ESHUTDOWN | 传输端点关闭后无法发送。 |
| ESOCKTNOSUPPORT | 不支持的套接字类型。 |
| ESPIPE | 非法的 seek 操作。 |
| ESRCH | 没有此进程。 |
| ESTALE | 过期的 NFS 文件句柄。 |
| ETIMEDOUT | 连接超时。 |
| ETOOMANYREFS | 引用过多：无法拼接。 |
| EUSERS | 用户过多。 |
| EWOULDBLOCK | 操作将阻塞。 |
| EXDEV | 跨设备链接。 |

##### Windows 错误代码

下表中的错误代码仅在 Windows 上可用。

| 错误代码 | 描述 |
|------------|-------------|
| WSAEACCES | 权限被拒绝。 |
| WSAEADDRINUSE | 地址已在使用中。 |
| WSAEADDRNOTAVAIL | 无法分配请求的地址。 |
| WSAEAFNOSUPPORT | 协议族不支持的地址族。 |
| WSAEALREADY | 操作已在进行中。 |
| WSAEBADF | 无效的文件句柄。 |
| WSAECONNABORTED | 软件引起的连接中止。 |
| WSAECONNREFUSED | 连接被拒绝。 |
| WSAECONNRESET | 连接被对端重置。 |
| WSAEDESTADDRREQ | 需要目标地址。 |
| WSAEDISCON | 远程关闭。 |
| WSAEDQUOT | 磁盘配额已超出。 |
| WSAEFAULT | 无效的地址。 |
| WSAEHOSTDOWN | 主机已关闭。 |
| WSAEHOSTUNREACH | 无法到达主机。 |
| WSAEINPROGRESS | 操作现在正在进行中。 |
| WSAEINTR | 系统调用被中断。 |
| WSAEINVAL | 无效的参数。 |
| WSAEISCONN | 套接字已连接。 |
| WSAELOOP | 无法转换名称。 |
| WSAEMFILE | 打开的文件过多。 |
| WSAEMSGSIZE | 消息过长。 |
| WSAENAMETOOLONG | 名称过长。 |
| WSAENETDOWN | 网络已关闭。 |
| WSAENETRESET | 网络因重置而断开连接。 |
| WSAENETUNREACH | 网络不可达。 |
| WSAENOBUFS | 没有可用的缓冲区空间。 |
| WSAENOPROTOOPT | 无效的协议选项。 |
| WSAENOTCONN | 套接字未连接。 |
| WSAENOTEMPTY | 无法删除非空目录。 |
| WSAENOTSOCK | 在非套接字上进行套接字操作。 |
| WSAEOPNOTSUPP | 不支持的操作。 |
| WSAEPFNOSUPPORT | 不支持的协议族。 |
| WSAEPROCLIM | 进程过多。 |
| WSAEPROTONOSUPPORT | 不支持的协议。 |
| WSAEPROTOTYPE | 套接字的协议类型错误。 |
| WSAEREMOTE | 项目在本地不可用。 |
| WSAESHUTDOWN | 套接字关闭后无法发送。 |
| WSAESOCKTNOSUPPORT | 不支持的套接字类型。 |
| WSAESTALE | 文件句柄不再可用。 |
| WSAETIMEDOUT | 连接超时。 |



| 错误代码 | 描述 |
|------------|-------------|
| WSAETOOMANYREFS | 对内核对象的引用过多。 |
| WSAEUSERS | 超出配额。 |
| WSAEWOULDBLOCK | 资源暂时不可用。 |
| WSANOTINITIALISED | 未执行成功的 WSA 启动。 |
| WSASYSNOTREADY | 网络子系统不可用。 |
| WSAVERNOTSUPPORTED | Winsock.dll 版本不在支持范围内。 |

#### fcntl

`fcntl` 模块对 UNIX 文件描述符执行文件和 I/O 控制。文件描述符可以通过文件或套接字对象的 `fileno()` 方法获得。

```
fcntl(fd, cmd [, arg])
```

在打开的文件描述符 `fd` 上执行命令 `cmd`。`cmd` 是一个整数命令代码。`arg` 是一个可选参数，可以是整数或字符串。如果 `arg` 作为整数传递，则此函数的返回值为整数。如果 `arg` 是字符串，则它被解释为二进制数据结构，调用的返回值是缓冲区内容转换回字符串对象。在这种情况下，提供的参数和返回值应小于 1,024 字节，以避免可能的数据损坏。以下命令可用：

| 命令 | 描述 |
|---------|-------------|
| F_DUPFD | 复制一个文件描述符。`arg` 是新文件描述符可以假设的最小编号。类似于 `os.dup()` 系统调用。 |
| F_SETFD | 将 `close-on-exec` 标志设置为 `arg`（0 或 1）。如果设置，文件将在 `exec()` 系统调用时关闭。 |
| F_GETFD | 返回 `close-on-exec` 标志。 |
| F_SETFL | 将状态标志设置为 `arg`，`arg` 是以下各项的按位或：<br>`O_NDELAY`—非阻塞 I/O（System V）<br>`O_APPEND`—追加模式（System V）<br>`O_SYNC`—同步写入（System V）<br>`FNDELAY`—非阻塞 I/O（BSD）<br>`FAPPEND`—追加模式（BSD）<br>`FASYNC`—当 I/O 可用时向进程组发送 `SIGIO` 信号（BSD） |
| F_GETFL | 获取由 `F_SETFL` 设置的状态标志。 |
| F_GETOWN | 获取设置为接收 `SIGIO` 和 `SIGURG` 信号的进程 ID 或进程组 ID（BSD）。 |
| F_SETOWN | 设置接收 `SIGIO` 和 `SIGURG` 信号的进程 ID 或进程组 ID（BSD）。 |
| F_GETLK | 返回用于文件锁定操作的 flock 结构。 |
| F_SETLK | 锁定一个文件，如果文件已被锁定则返回 -1。 |
| F_SETLKW | 锁定一个文件，但如果无法获取锁则等待。 |

如果 `fcntl()` 函数失败，会引发 `IOError` 异常。`F_GETLK` 和 `F_SETLK` 命令通过 `lockf()` 函数支持。

```
ioctl(fd, op, arg [, mutate_flag])
```

此函数类似于 `fcntl()` 函数，不同之处在于 `op` 中提供的操作通常在库模块 `termios` 中定义。额外的 `mutate_flag` 控制当可变缓冲区对象作为参数传递时此函数的行为。有关此内容的更多详细信息可以在在线文档中找到。由于 `ioctl()` 的主要用途是与设备驱动程序和操作系统的其他低级组件进行交互，因此其使用高度依赖于底层平台。不应在旨在可移植的代码中使用。

```
flock(fd, op)
```

在文件描述符 `fd` 上执行锁定操作 `op`。`op` 是以下常量的按位或，这些常量在 `fcntl` 中找到：

| 项目 | 描述 |
| --- | --- |
| `LOCK_EX` | 独占锁。所有后续获取锁的尝试都将阻塞，直到锁被释放。 |
| `LOCK_NB` | 非阻塞模式。如果锁已被使用，立即返回并引发 `IOError`。 |
| `LOCK_SH` | 共享锁。阻止任何获取独占锁（`LOCK_EX`）的尝试，但仍可获取共享锁。 |
| `LOCK_UN` | 解锁。释放之前持有的任何锁。 |

在非阻塞模式下，如果无法获取锁，会引发 `IOError` 异常。在某些系统上，通过在 `os.open()` 操作中添加特殊标志，可以在单个操作中打开和锁定文件。有关更多详细信息，请查阅 `os` 模块。

```
lockf(fd, op [, len [, start [, whence]]])
```

对文件的一部分执行记录或范围锁定。`op` 与 `flock()` 函数相同。`len` 是要锁定的字节数。`start` 是相对于 `whence` 值的锁定起始位置。`whence` 为 `0` 表示文件开头，`1` 表示当前位置，`2` 表示文件末尾。

##### 示例

```
import fcntl

###### 打开一个文件
f = open("foo","w")

###### 设置文件对象 f 的 close-on-exec 位
fcntl.fcntl(f.fileno(), fcntl.F_SETFD, 1)

###### 锁定文件（阻塞）
fcntl.flock(f.fileno(), fcntl.LOCK_EX)
```

```
###### 锁定文件的前 8192 字节（非阻塞）
try:
    fcntl.lockf(f.fileno(), fcntl.LOCK_EX | fcntl.LOCK_NB, 8192, 0, 0)
except IOError,e:
    print "Unable to acquire lock", e
```

##### 注意事项

- 可用的 `fcntl()` 命令和选项集取决于系统。在某些平台上，`fcntl` 模块可能包含超过 100 个常量。
- 尽管其他模块中定义的锁定操作通常使用上下文管理器协议，但文件锁定并非如此。如果你获取了文件锁，请确保你的代码被正确编写以释放锁。
- 此模块中的许多函数也可应用于套接字的文件描述符。

#### io

io 模块实现了各种形式的 I/O 类，以及在 Python 3 中使用的内置 `open()` 函数。该模块也可在 Python 2.6 中使用。

io 模块解决的核心问题是无缝处理不同形式的基本 I/O。例如，由于与换行符和字符编码相关的问题，处理文本与处理二进制数据略有不同。为了处理这些差异，该模块被构建为一系列层，每一层都为上一层增加更多功能。

##### 基本 I/O 接口

io 模块定义了一个基本的 I/O 编程接口，所有类文件对象都实现了这个接口。该接口由基类 `IOBase` 定义。`IOBase` 的一个实例 *f* 支持以下基本操作：

| 属性 | 描述 |
|---|---|
| `f.closed` | 指示文件是否已关闭的标志。 |
| `f.close()` | 关闭文件。 |
| `f.fileno()` | 返回整数文件描述符。 |
| `f.flush()` | 刷新 I/O 缓冲区（如果有的话）。 |
| `f.isatty()` | 如果 *f* 是终端则返回 `True`。 |
| `f.readable()` | 如果 *f* 是为读取而打开的，则返回 `True`。 |
| `f.readline([limit])` | 从流中读取一行。*limit* 是要读取的最大字节数。 |
| `f.readlines([limit])` | 从 *f* 读取所有行并作为列表返回。如果提供 *limit*，则是在停止前可读取的最大字节数。实际读取的字节数会稍大一些，以容纳保持完整的最后一行。 |

| 属性 | 描述 |
| --- | --- |
| f.seek(offset, [whence]) | 将文件指针移动到相对于 whence 中指定位置的新位置。offset 是字节数。whence 为 0 表示文件开头，1 表示当前位置，2 表示文件末尾。 |
| f.seekable() | 如果 f 是可寻址的则返回 True。 |
| f.tell() | 返回文件指针的当前值。 |
| f.truncate([size]) | 截断文件大小，使其最多为 size 字节。如果未给出 size，则将文件截断为 0 字节。 |
| f.writable() | 如果 f 是为写入而打开的则返回 True。 |
| f.writelines(lines) | 将一系列行写入 f。不添加行尾，因此它们必须已经是每行的一部分。 |

##### 原始 I/O

I/O 系统的最低级别涉及原始字节的直接 I/O。此核心对象是 FileIO，它提供了对底层系统调用（如 read() 和 write()）的相当直接的接口。

```
FileIO(name [, mode [, closefd]])
```

一个用于在文件或系统文件描述符上执行原始低级 I/O 的类。name 可以是文件名或整数文件描述符，例如由 os.open() 函数或其他文件对象的 fileno() 方法返回的描述符。mode 是 'r'（默认值）；'w'；或 'a'，分别用于读取、写入或追加。可以在 mode 中添加 '+' 以进入更新模式，其中同时支持读取和写入。closefd 是一个标志，确定 close() 方法是否实际关闭底层文件。默认情况下，此值为 True，但如果你使用 FileIO 来包装已在其他地方打开的文件，可以将其设置为 False。如果给出了文件名，则生成的文件对象直接使用操作系统的 open() 调用打开。没有内部缓冲，所有数据都作为原始字节字符串处理。FileIO 的一个实例 f 具有前面描述的所有基本 I/O 操作以及以下属性和方法：

| 属性 | 描述 |
| --- | --- |
| f.closefd | 确定在 f.close() 时是否关闭底层文件描述符的标志（只读）。 |
| f.mode | 打开文件时使用的模式（只读）。 |
| f.name | 文件名（只读）。 |
| f.read([size]) | 使用单个系统调用读取最多 size 字节。如果省略 size，则使用 f.readall() 尽可能多地返回数据。此操作可能返回的字节数少于请求的字节数，因此必须使用 len() 进行检查。在非阻塞模式下，如果没有可用数据，则返回 None。 |
| f.readall() | 读取所有可用数据并作为单个字节字符串返回。在 EOF 时返回空字符串。在非阻塞模式下，仅返回立即可用的数据量。 |
| f.write(bytes) | 使用单个系统调用将字节字符串或字节数组写入 f。实际写入的字节数被返回——可能少于提供的字节数。 |



必须强调的是，`FileIO` 对象是极其底层的，它们在操作系统调用如 `read()` 和 `write()` 之上只提供了一个相当薄的封装层。具体来说，该对象的使用者需要仔细检查返回码，因为无法保证 `f.read()` 或 `f.write()` 操作会读取或写入所有请求的数据。`fcntl` 模块可用于更改文件的底层方面，例如文件锁定、阻塞行为等。

`FileIO` 对象不应用于处理面向行的数据，例如文本。虽然定义了诸如 `f.readline()` 和 `f.readlines()` 之类的方法，但这些方法来自 `IOBase` 基类，它们完全在 Python 中实现，并通过每次发出单字节的 `f.read()` 操作来工作。不用说，由此产生的性能是糟糕的。例如，在 `FileIO` 对象 *f* 上使用 `f.readline()` 比在 Python 2.6 的 `open()` 函数创建的标准文件对象上使用 `f.readline()` 慢 750 多倍。

##### 缓冲二进制 I/O

缓冲 I/O 层包含一系列用于读取和写入原始二进制数据的文件对象，但带有内存缓冲。作为输入，这些对象都需要一个实现了原始 I/O 的文件对象，例如上一节中的 `FileIO` 对象。本节中的所有类都继承自 `BufferedIOBase`。

`BufferedReader(raw [, buffer_size])`

一个用于在 `raw` 指定的原始文件上进行缓冲二进制读取的类。*buffer_size* 指定以字节为单位的缓冲区大小。如果省略，则使用 `DEFAULT_BUFFER_SIZE` 的值（在撰写本文时为 8,192 字节）。`BufferedReader` 的实例 *f* 除了支持 `IOBase` 上提供的所有操作外，还支持以下操作：

| 方法 | 描述 |
| --- | --- |
| `f.peek([n])` | 从 I/O 缓冲区返回最多 *n* 字节的数据，而不移动文件指针。如果省略 *n*，则返回一个字节。如果必要，如果缓冲区当前为空，将发出读操作来填充缓冲区。此操作返回的字节数永远不会超过当前缓冲区大小，因此结果可能小于请求的字节数 *n*。 |
| `f.read([n])` | 读取 *n* 字节并作为字节字符串返回。如果省略 *n*，则读取并返回所有可用数据（直到 EOF）。如果底层文件是非阻塞的，则读取并返回任何可用数据。如果读取非阻塞文件且没有可用数据，则会引发 `BlockingIOError` 异常。 |
| `f.read1([n])` | 使用单个系统调用读取最多 *n* 字节并作为字节字符串返回。如果缓冲区中已加载了任何数据，则直接返回。否则，对原始文件进行一次 `read()` 调用以返回数据。与 `f.read()` 不同，即使底层文件未到达 EOF，此操作也可能返回比请求更少的数据。 |
| `f.readinto(b)` | 从文件中读取 `len(b)` 字节数据到现有的 `bytearray` 对象 *b* 中。返回实际读取的字节数。如果底层文件处于非阻塞模式且没有可用数据，则会引发 `BlockingIOError` 异常。 |

`BufferedWriter(raw [, buffer_size [, max_buffer_size]])`

一个用于在 `raw` 指定的原始文件上进行缓冲二进制写入的类。`buffer_size` 指定在数据刷新到底层 I/O 流之前可以保存在缓冲区中的字节数。默认值为 `DEFAULT_BUFFER_SIZE`。`max_buffer_size` 指定用于存储正在写入非阻塞流的输出数据的最大缓冲区大小，默认为 `buffer_size` 值的两倍。这个值较大是为了允许在操作系统将先前缓冲区内容写入 I/O 流时持续写入。`BufferedWriter` 的实例 `f` 支持以下操作：

| 方法 | 描述 |
| --- | --- |
| `f.flush()` | 将缓冲区中存储的所有字节写入底层 I/O 流。如果文件处于非阻塞模式且操作会阻塞（例如，如果流当前无法接受任何新数据），则会引发 `BlockingIOError` 异常。 |
| `f.write(bytes)` | 将 `bytes` 中的字节写入 I/O 流，并返回实际写入的字节数。如果底层流是非阻塞的，并且写操作会阻塞，则会引发 `BlockingIOError` 异常。 |

`BufferedRWPair(reader, writer [, buffer_size [, max_buffer_size]])`

一个用于在一对原始 I/O 流上进行缓冲二进制读写的类。`reader` 是一个支持读取的原始文件，`writer` 是一个支持写入的原始文件。这些文件可能不同，这对于涉及管道和套接字的某些类型的通信可能很有用。缓冲区大小参数与 `BufferedWriter` 具有相同的含义。`BufferedRWPair` 的实例 `f` 支持 `BufferedReader` 和 `BufferedWriter` 的所有操作。

`BufferedRandom(raw [, buffer_size [, max_buffer_size]])`

一个用于在支持随机访问（例如，seeking）的原始 I/O 流上进行缓冲二进制读写的类。`raw` 必须是一个支持读、写和 seek 操作的原始文件。缓冲区大小参数与 `BufferedWriter` 具有相同的含义。`BufferedRandom` 的实例 `f` 支持 `BufferedReader` 和 `BufferedWriter` 的所有操作。

`BytesIO([bytes])`

一个实现缓冲 I/O 流功能的内存文件。`bytes` 是一个指定文件初始内容的字节字符串。`BytesIO` 的实例 `b` 支持 `BufferedReader` 和 `BufferedWriter` 对象的所有操作。此外，可以使用方法 `b.getvalue()` 以字节字符串的形式返回文件的当前内容。

与 `FileIO` 对象一样，本节中的所有文件对象都不应用于处理面向行的数据，例如文本。虽然由于缓冲，情况不那么糟糕，但由此产生的性能仍然相当差（例如，比使用 Python 2.6 内置 `open()` 函数创建的文件逐行读取慢 50 倍以上）。另外，由于内部缓冲，在写入时需要注意管理 `flush()` 操作。例如，如果你使用 `f.seek()` 将文件指针移动到新位置，你应该先使用 `f.flush()` 来刷新任何先前写入的数据（如果有的话）。

另外，请注意缓冲区大小参数仅指定发生写入的限制，并不一定设置内部资源使用的限制。例如，当你在缓冲文件 `f` 上执行 `f.write(data)` 时，`data` 中的所有字节首先被复制到内部缓冲区中。如果 `data` 代表一个非常大的字节数组，这种复制将显著增加程序的内存使用。因此，最好以合理的块大小写入大量数据，而不是通过单个 `write()` 操作一次性写入。应该指出的是，由于 `io` 模块相对较新，此行为在未来版本中可能会有所不同。

##### 文本 I/O

文本 I/O 层用于处理面向行的字符数据。本节中定义的类建立在缓冲 I/O 流之上，并添加了面向行的处理以及 Unicode 字符编码和解码。此处的所有类都继承自 `TextIOBase`。

`TextIOWrapper(buffered [, encoding [, errors [, newline [, line_buffering]]]])`

一个用于缓冲文本流的类。`buffered` 是上一节描述的缓冲 I/O。`encoding` 是一个字符串，如 'ascii' 或 'utf-8'，用于指定文本编码。`errors` 指定 Unicode 错误处理策略，默认为 'strict'（描述请参见第 9 章 "输入与输出"）。`newline` 是表示换行的字符序列，可以是 `None`、''、'\n'、'\r' 或 '\r\n'。如果给定 `None`，则启用通用换行模式，其中读取时任何其他行结尾都会被转换为 '\n'，输出时使用 `os.linesep` 作为换行符。如果 `newline` 是其他值之一，则所有 '\n' 字符在输出时都会被转换为指定的换行符。`line_buffering` 是一个标志，控制在任何写操作包含换行符时是否执行 `flush()` 操作。默认情况下，这是 `False`。`TextIOWrapper` 的实例 `f` 支持 `IOBase` 上定义的所有操作，以及以下内容：

| 方法 | 描述 |
| --- | --- |
| `f.encoding` | 正在使用的文本编码的名称。 |
| `f.errors` | 编码和解码错误处理策略。 |
| `f.line_buffering` | 决定行缓冲行为的标志。 |
| `f.newlines` | `None`、一个字符串或一个元组，给出所有不同形式的换行符。 |
| `f.read([n])` | 从底层流中读取最多 n 个字符并作为字符串返回。如果省略 n，则读取从当前位置到文件末尾的所有可用数据。在文件末尾（EOF）返回空字符串。返回的字符串根据 `f.encoding` 中的编码设置进行解码。 |
| `f.readline([limit])` | 读取单行文本并作为字符串返回。在文件末尾（EOF）返回空字符串。`limit` 是要读取的最大字节数。 |
| `f.write(s)` | 使用 `f.encoding` 中的文本编码将字符串 `s` 写入底层流。 |

`StringIO([initial [, encoding [, errors [, newline]]]])`

一个与 `TextIOWrapper` 行为相同的内存文件对象。`initial` 是一个指定文件初始内容的字符串。其他参数与

##### `StringIO` 类

`StringIO` 类的用法与 `TextIOWrapper` 类似。`StringIO` 的实例 `s` 支持所有常规的文件操作，另外还有一个方法 `s.getvalue()` 可以返回内存缓冲区的当前内容。

##### `open()` 函数

`io` 模块定义了以下 `open()` 函数，它与 Python 3 的内置 `open()` 函数相同。

```
open(file [, mode [, buffering [, encoding [, errors [, newline [, closefd]]]]])
```

打开 *file* 并返回一个合适的 I/O 对象。*file* 可以是文件名字符串，也可以是已打开 I/O 流的整数文件描述符。此函数的返回值是 `io` 模块中定义的 I/O 类之一，具体取决于 *mode* 和 *buffering* 的设置。如果 *mode* 是任何文本模式，如 `'r'`、`'w'`、`'a'` 或 `'U'`，则返回 `TextIOWrapper` 的实例。如果 *mode* 是二进制模式，如 `'rb'` 或 `'wb'`，则结果取决于 *buffering* 的设置。如果 *buffering* 为 `0`，则返回 `FileIO` 的实例以执行原始的无缓冲 I/O。如果 *buffering* 是任何其他值，则根据文件模式返回 `BufferedReader`、`BufferedWriter` 或 `BufferedRandom` 的实例。*encoding*、*errors* 和 *newline* 参数仅适用于以文本模式打开的文件，并传递给 `TextIOWrapper` 构造函数。*closefd* 仅当 *file* 是整数描述符时适用，并传递给 `FileIO` 构造函数。

##### 抽象基类

`io` 模块定义了以下抽象基类，可用于类型检查和定义新的 I/O 类：

| 抽象类 | 描述 |
| :--- | :--- |
| `IOBase` | 所有 I/O 类的基类。 |
| `RawIOBase` | 支持原始二进制 I/O 的对象的基类。继承自 `IOBase`。 |
| `BufferedIOBase` | 支持缓冲二进制 I/O 的对象的基类。继承自 `IOBase`。 |
| `TextIOBase` | 支持文本流的对象的基类。继承自 `IOBase`。 |

大多数程序员很少直接使用这些类。有关其使用和定义的详细信息，请参考在线文档。

> **注意**
>
> `io` 模块是 Python 的新增模块，首次出现在 Python 3 中，并被移植到 Python 2.6。在撰写本文时，该模块尚未成熟，运行性能极差——尤其对于任何涉及大量文本 I/O 的应用。如果您使用的是 Python 2，使用内置的 `open()` 函数会比使用 `io` 模块中定义的 I/O 类更好。如果您使用的是 Python 3，似乎没有其他选择。尽管未来的版本可能会改进性能，但这种分层 I/O 方法加上 Unicode 解码，不太可能达到 Python 2 中基于 C 标准库的原始 I/O 性能。

#### `logging` 模块

`logging` 模块为应用程序提供了记录事件、错误、警告和调试信息的灵活机制。这些信息可以被收集、过滤、写入文件、发送到系统日志，甚至通过网络发送到远程机器。本节涵盖了在大多数常见情况下使用该模块的基本细节。

##### 日志级别

`logging` 模块的主要关注点是日志消息的发出和处理。每条消息包含一些文本和一个相关级别，用于指示其严重性。级别既有符号名称也有数值，如下所示：

| 级别 | 值 | 描述 |
| :--- | :--- | :--- |
| CRITICAL | 50 | 严重错误/消息 |
| ERROR | 40 | 错误 |
| WARNING | 30 | 警告消息 |
| INFO | 20 | 信息性消息 |
| DEBUG | 10 | 调试 |
| NOTSET | 0 | 未设置级别 |

这些不同的级别是 `logging` 模块中各种函数和方法的基础。例如，有用于发出各个级别日志消息的方法，也有通过阻止不符合特定阈值的消息来工作的过滤器。

##### 基本配置

在使用 `logging` 模块中的任何其他函数之前，您应该首先对一个称为 *根记录器* 的特殊对象进行一些基本配置。根记录器负责管理日志消息的默认行为，包括日志级别、输出目标、消息格式和其他基本细节。以下函数用于配置：

```
basicConfig([**kwargs])
```

执行根记录器的基本配置。此函数应在进行任何其他日志记录调用之前调用。该函数接受多个关键字参数：

| 关键字参数 | 描述 |
| :--- | :--- |
| `filename` | 将日志消息追加到具有给定文件名的文件中。 |
| `filemode` | 指定打开文件的模式。默认模式为 `'a'`（追加）。 |
| `format` | 用于生成日志消息的格式字符串。 |
| `datefmt` | 用于输出日期和时间的格式字符串。 |
| `level` | 设置根记录器的级别。所有级别等于或高于此级别的日志消息将被处理。低于此级别的消息将被静默忽略。 |
| `stream` | 提供一个打开的文件，日志消息将发送到该文件。默认流是 `sys.stderr`。此参数不能与 `filename` 参数同时使用。 |

这些参数大多数不言自明。`format` 参数用于指定日志消息的格式以及可选的上下文信息，如文件名、级别、行号等。`datefmt` 是一个与 `time.strftime()` 函数兼容的日期格式字符串。如果省略，日期格式将设置为 ISO8601 格式。

`format` 中识别以下扩展名：

| 格式 | 描述 |
| :--- | :--- |
| `%(name)s` | 记录器的名称。 |
| `%(levelno)s` | 数值日志级别。 |
| `%(levelname)s` | 日志级别的文本名称。 |
| `%(pathname)s` | 执行日志调用的源文件路径名。 |
| `%(filename)s` | 执行日志调用的源文件文件名。 |
| `%(funcName)s` | 进行日志调用的函数名。 |
| `%(module)s` | 执行日志调用的模块名。 |
| `%(lineno)d` | 执行日志调用的行号。 |
| `%(created)f` | 执行日志调用的时间。该值是 `time.time()` 返回的数字。 |
| `%(asctime)s` | 执行日志调用时的 ASCII 格式日期和时间。 |
| `%(msecs)s` | 执行日志调用时间的毫秒部分。 |
| `%(thread)d` | 线程 ID。 |
| `%(threadName)s` | 线程名。 |
| `%(process)d` | 进程 ID。 |
| `%(message)s` | 记录的消息（由用户提供）。 |

以下示例演示了一个单一配置，其中级别为 `INFO` 或更高的日志消息被追加到文件中：

```
import logging
logging.basicConfig(
    filename = "app.log",
    format   = "%(levelname)-10s %(asctime)s %(message)s",
    level    = logging.INFO
)
```

使用此配置，一条级别为 `CRITICAL`、内容为 `'Hello World'` 的日志消息将在日志文件 `'app.log'` 中显示如下：

```
CRITICAL   2005-10-25 20:46:57,126 Hello World
```

##### Logger 对象

为了发出日志消息，您必须获得一个 `Logger` 对象。本节描述创建、配置和使用这些对象的过程。

###### 创建 Logger

要创建一个新的 `Logger` 对象，请使用以下函数：

```
getLogger([logname])
```

返回一个与名称 `logname` 关联的 `Logger` 实例。如果不存在这样的对象，则会创建并返回一个新的 `Logger` 实例。`logname` 是一个字符串，指定一个名称

或一系列由点分隔的名称（例如 `'app'` 或 `'app.net'`）。如果您省略 `logname`，您将获得与根记录器关联的 `Logger` 对象。

`Logger` 实例的创建方式与大多数其他库模块中的方式不同。当您创建一个 `Logger` 时，您总是给它一个名称，该名称作为 `logname` 参数传递给 `getLogger()`。在内部，`getLogger()` 维护一个 `Logger` 实例及其关联名称的缓存。如果程序的另一部分请求一个具有相同名称的记录器，则会返回先前创建的实例。这种安排大大简化了大型应用程序中日志消息的处理，因为您不必弄清楚如何在不同的程序模块之间传递 `Logger` 实例。相反，在您想要记录日志的每个模块中，您只需使用 `getLogger()` 来获取对相应 `Logger` 对象的引用。

###### 选择名称

出于稍后将变得清晰的原因，您在使用 `getLogger()` 时应始终选择有意义的名称。例如，如果您的应用程序称为 `'app'`，那么您至少应该在构成应用程序的每个程序模块顶部使用 `getLogger('app')`。例如：

```
import logging
log = logging.getLogger('app')
```

您还可以考虑在记录器中添加模块名，例如 `getLogger('app.net')` 或 `getLogger('app.user')`，以便更清楚地表明日志消息的来源。可以使用如下语句完成：

```
import logging
log = logging.getLogger('app.'+__name__)
```

添加模块名使得更容易选择性地关闭或重新配置特定程序模块的日志记录，这将在后面描述。

###### 发出日志消息

如果 `log` 是 `Logger` 对象的实例（使用上一节中的 `getLogger()` 函数创建），则使用以下方法在不同日志级别发出日志消息：

| 日志级别 | 方法 |
| :--- | :--- |
| `CRITICAL` | `log.critical(fmt [, *args [, exc_info [, extra]]])` |
| `ERROR` | `log.error(fmt [, *args [, exc_info [, extra]]])` |
| `WARNING` | `log.warning(fmt [, *args [, exc_info [, extra]]])` |
| `INFO` | `log.info(fmt [, *args [, exc_info [, extra]]])` |
| `DEBUG` | `log.debug(fmt [, *args [, exc_info [, extra]]])` |

`fmt` 参数是一个格式字符串，用于指定日志消息的格式。`args` 中的其余参数用作格式字符串中格式说明符的参数。字符串格式化运算符 `%` 用于从这些参数形成最终的消息。如果提供了多个参数，它们将被放入一个元组中进行格式化。如果提供了单个参数，则在格式化时直接放在 `%` 之后。



因此，如果将单个字典作为参数传递，格式字符串可以包含字典的键名。以下是一些示例，说明了这是如何工作的：

```
log = logging.getLogger("app")
####### A log message using positional formatting
log.critical("Can't connect to %s at port %d", host, port)

####### A log message using dictionary formatting
parms = {
    'host' : 'www.python.org',
    'port' : 80
}
log.critical("Can't connect to %(host)s at port %(port)d", parms)
```

关键字参数 *exc_info* 如果设置为 True，会将 `sys.exc_info()` 中的异常信息添加到日志消息中。如果 *exc_info* 设置为一个异常元组（例如 `sys.exc_info()` 返回的元组），则会使用该信息。*extra* 关键字参数是一个字典，用于提供日志消息格式字符串中使用的附加值（后文会介绍）。*exc_info* 和 *extra* 都必须作为关键字参数来指定。

在发出日志消息时，你应该避免在发出消息时才执行字符串格式化操作的代码（即先格式化消息，然后将结果传递给 logging 模块）。例如，

```
log.critical("Can't connect to %s at port %d" % (host, port))
```

在这个示例中，字符串格式化操作总是发生在调用 `log.critical()` *之前*，因为函数或方法的参数必须被完全求值。然而，在本页顶部的示例中，用于字符串格式化操作的参数仅仅是传递给了 *logging* 模块，并且只在日志消息确实要被处理时才会使用。这是一个非常微妙的区别，但由于许多应用程序选择过滤日志消息或仅在调试时输出日志，第一种方式在禁用日志时执行的工作更少，运行速度更快。

除了上面展示的方法之外，在 Logger 实例 *log* 上还有几个用于发出日志消息的附加方法。

```
log.exception(fmt [, *args ])
```

以 ERROR 级别发出一条消息，但会添加当前正在处理的异常的异常信息。这只能在 except 块内部使用。

```
log.log(level, fmt [, *args [, exc_info [, extra]]])
```

以 *level* 指定的级别发出日志消息。如果日志级别由变量决定，或者你想使用五个基本级别之外的额外日志级别，可以使用此方法。

```
log.findCaller()
```

返回一个元组 (*filename*, *lineno*, *funcname*)，对应调用者的源文件名、行号和函数名。这些信息在发出日志消息时有时很有用——例如，如果你想在消息中添加关于日志调用位置的信息。

##### 过滤日志消息

每个 Logger 对象 `log` 都有一个内部级别和过滤机制，用于决定哪些日志消息会被处理。以下两个方法用于基于日志消息的数字级别执行简单的过滤：

```
log.setLevel(level)
```

设置 `log` 的级别。只有级别大于或等于 `level` 的日志消息才会被处理。所有其他消息将被忽略。默认情况下，级别为 `logging.NOTSET`，会处理所有日志消息。

```
log.isEnabledFor(level)
```

如果某个日志级别为 `level` 的消息会被处理，则返回 `True`。

日志消息也可以基于与消息本身关联的信息进行过滤——例如文件名、行号和其他详细信息。以下方法用于此目的：

```
log.addFilter(filt)
```

将过滤器对象 `filt` 添加到日志记录器。

```
log.removeFilter(filt)
```

从日志记录器中移除过滤器对象 `filt`。

在这两个方法中，`filt` 都是 `Filter` 对象的实例。

```
Filter(logname)
```

创建一个过滤器，只允许来自 `logname` 或其子级的日志消息通过。例如，如果 `logname` 是 `'app'`，那么来自 `'app'`、`'app.net'` 或 `'app.user'` 等日志记录器的消息将会通过，但来自 `'spam'` 等日志记录器的消息则不会。

可以通过继承 `Filter` 并实现 `filter(record)` 方法来创建自定义过滤器，该方法接收包含日志消息信息的记录作为输入。作为输出，根据消息是否应该被处理返回 `True` 或 `False`。传递给此方法的 `record` 对象通常具有以下属性：

| 属性 | 描述 |
| --- | --- |
| `record.name` | 日志记录器名称 |
| `record.levelname` | 级别名称 |
| `record.levelno` | 级别编号 |
| `record.pathname` | 模块的路径名 |
| `record.filename` | 基本文件名 |
| `record.module` | 模块名 |
| `record.exc_info` | 异常信息 |
| `record.lineno` | 发出日志消息的行号 |
| `record.funcName` | 发出日志消息的函数名 |
| `record.created` | 发出时间 |
| `record.thread` | 线程标识符 |
| `record.threadName` | 线程名 |
| `record.process` | 当前执行进程的 PID |

以下示例演示了如何创建自定义过滤器：

```
class FilterFunc(logging.Filter):
    def __init__(self,name):
        self.funcName = name
    def filter(self, record):
        if record.funcName == self.funcName: return False
        else: return True
```

```
log.addFilter(FilterFunc('foo'))   # Ignore all messages originating from foo()
log.addFilter(FilterFunc('bar'))   # Ignore all messages originating from bar()
```

##### 消息传播和层级日志记录器

在高级日志应用中，Logger 对象可以被组织成一个层级结构。这通过给日志记录器对象指定一个名称（如 'app.net.client'）来实现。这里实际上有三个不同的 Logger 对象，分别叫做 'app'、'app.net' 和 'app.net.client'。当在任何日志记录器上发出一条消息并且该消息成功通过该日志记录器的过滤器时，它会传播到所有父级并由它们处理。例如，在 'app.net.client' 上成功发出的消息也会传播到 'app.net'、'app' 和根日志记录器。

Logger 对象 log 的以下属性和方法控制这种传播行为。

**log.propagate**

一个布尔标志，指示消息是否传播到父日志记录器。默认情况下，此值设置为 True。

**log.getEffectiveLevel()**

返回日志记录器的有效级别。如果通过 setLevel() 设置了级别，则返回该级别。如果没有显式设置级别（此时级别为 logging.NOTSET），则此函数返回父日志记录器的有效级别。如果父日志记录器都没有设置级别，则返回根日志记录器的有效级别。

层级日志记录的主要目的是能够更轻松地过滤来自大型应用程序不同部分的日志消息。例如，如果你想关闭来自应用程序中 'app.net.client' 部分的日志消息，可以添加如下配置代码：

```
import logging
logging.getLogger('app.net.client').propagate = False
```

或者，在这段代码中，我们忽略来自程序模块的除最严重级别以外的所有消息：

```
import logging
logging.getLogger('app.net.client').setLevel(logging.CRITICAL)
```

层级日志记录器的一个微妙之处在于，是否处理日志消息的决定完全由消息所发出的 Logger 对象上的级别和过滤器做出，而不是由任何父级的过滤器做出。因此，如果消息通过了第一组过滤器，它就会传播到所有父日志记录器并被它们*处理*，而不考虑父级自身的过滤器和级别设置——即使这些过滤器本会拒绝该消息。乍一看，这种行为是违反直觉的，甚至可能看起来像是一个 bug。然而，将子日志记录器的级别设置为低于其父级的值是覆盖父级设置的一种方式，从而实现一种级别的提升。以下是一个示例：

```
import logging

###### The top-level logger 'app'.
log = logging.getLogger('app')
log.setLevel(logging.CRITICAL)      # Only accept CRITICAL level messages.

###### A child logger 'app.net'
net_log = logging.getLogger('app.net')
net_log.setLevel(logging.ERROR)       # Accept ERROR messages on 'app.net'.
                                      # These messages will now be handled by the
                                      # 'app' logger even though its level is
                                      # CRITICAL.
```

使用层级日志记录器时，你只需要配置那些你想要更改过滤或传播行为的日志对象。由于消息会自然传播到根日志记录器，它最终将负责生成输出，并且你使用 `basicConfig()` 所做的任何配置都会生效。

##### 消息处理

通常，消息由根日志记录器处理。但是，任何 Logger 对象都可以添加特殊的处理器来接收和处理日志消息。这是通过 Logger 实例 `log` 的以下方法来完成的。

**`log.addHandler(handler)`**

向日志记录器添加一个 Handler 对象。

**`log.removeHandler(handler)`**

从日志记录器中移除 Handler 对象 `handler`。

`logging` 模块提供了多种预构建的处理器，用于将日志消息写入文件、流、系统日志等。这些将在下一节中详细介绍。不过，以下示例展示了如何使用这些方法将日志记录器和处理器连接在一起。

```
import logging
import sys

###### Create a top-level logger called 'app'
app_log = logging.getLogger("app")
app_log.setLevel(logging.INFO)
app_log.propagate = False

###### Add some message handlers to the 'app' log
app_log.addHandler(logging.FileHandler('app.log'))
app_log.addHandler(logging.StreamHandler(sys.stderr))

# Issue some messages.  These go to app.log and sys.stderr
app_log.critical("Creeping death detected!")
app_log.info("FYI")
```

当你添加自己的处理器来处理消息时，通常的目的是覆盖根日志记录器的行为。这就是为什么在前面的示例中禁用了消息传播（即 'app' 日志记录器将直接处理所有消息）。



####### 处理器对象

日志模块提供了一系列预构建的处理器，它们能以不同方式处理日志消息。这些处理器通过其 `addHandler()` 方法添加到 Logger 对象中。此外，每个处理器都可以配置各自的过滤器和日志级别。

##### 内置处理器

以下处理器对象是内置的。其中一些处理器定义在子模块 `logging.handlers` 中，如需使用，必须显式导入。

`handlers.DatagramHandler(host, port)`

将日志消息发送到位于给定主机和端口的 UDP 服务器。日志消息通过提取相应 LogRecord 对象的字典并使用 pickle 模块进行编码来编码。传输的网络消息由 4 字节网络字节序（大端序）的长度头后跟 pickle 序列化的记录数据组成。要重构消息，接收方必须去掉长度头，读取整个消息，反序列化内容，并调用 `logging.makeLogRecord()`。由于 UDP 不可靠，网络错误可能导致日志消息丢失。

`FileHandler(filename [, mode [, encoding [, delay]]])`

将日志消息写入文件 `filename`。`mode` 是打开文件时使用的文件模式，默认为 `'a'`。`encoding` 是文件编码。`delay` 是一个布尔标志，若设为 `True`，则会延迟打开日志文件，直到发出第一条日志消息。默认值为 `False`。

`handlers.HTTPHandler(host, url [, method])`

使用 HTTP GET 或 POST 方法将日志消息上传到 HTTP 服务器。`host` 指定主机，`url` 是要使用的 URL，`method` 可以是 `'GET'`（默认）或 `'POST'`。日志消息通过提取相应 LogRecord 对象的字典并使用 `urllib.urlencode()` 函数将其编码为一组 URL 查询字符串变量来编码。

`handlers.MemoryHandler(capacity [, flushLevel [, target]])`

此处理器用于在内存中收集日志消息，并定期将其刷新到另一个处理器 `target`。`capacity` 是内存缓冲区的大小（以字节为单位）。`flushLevel` 是一个数值日志级别，当日志消息达到或超过该级别时，会强制刷新内存。默认值为 `ERROR`。`target` 是另一个接收消息的 Handler 对象。如果省略 `target`，你需要使用所得处理器对象的 `setTarget()` 方法设置一个目标，此处理器才能执行任何操作。

`handlers.NTEventLogHandler(appname [, dllname [, logtype]])`

将消息发送到 Windows NT、Windows 2000 或 Windows XP 的事件日志。`appname` 是要在事件日志中使用的应用程序名称。`dllname` 是提供消息定义的 `.DLL` 或 `.EXE` 文件的完整路径名。如果省略，`dllname` 将被设置为 `'win32service.pyd'`。`logtype` 可以是 `'Application'`、`'System'` 或 `'Security'`。默认值为 `'Application'`。此处理器仅在安装了 Python 的 Win32 扩展时才可用。

`handlers.RotatingFileHandler(filename [, mode [, maxBytes [, backupCount [, encoding [, delay]]]]])`

将日志消息写入文件 *filename*。但是，如果文件大小超过 *maxBytes* 指定的大小，文件将轮转为 *filename*.1，并打开一个新的日志文件 *filename*。*backupCount* 指定要创建的备份文件的最大数量。默认情况下，*backupCount* 的值为 0。但是，当指定时，备份文件将按 *filename*.1、*filename*.2、...、*filename*.N 的顺序轮转，其中 *filename*.1 始终是最近的备份，*filename*.N 始终是最旧的备份。*mode* 指定打开日志文件时使用的文件模式。默认模式是 `'a'`。如果 *maxBytes* 为 0（默认值），则日志文件永远不会滚动，并且可以无限增长。*encoding* 和 *delay* 与 FileHandler 中的含义相同。

`handlers.SMTPHandler(mailhost, fromaddr, toaddrs, subject [, credentials])`

使用电子邮件将日志消息发送到远程主机。*mailhost* 是可以接收消息的 SMTP 服务器的地址。该地址可以是字符串指定的简单主机名，也可以是元组 `(host, port)`。*fromaddr* 是发件人地址，*toaddrs* 是目标地址，*subject* 是消息中使用的主题。*credentials* 是包含用户名和密码的元组 `(username, password)`。

`handlers.SocketHandler(host, port)`

使用 TCP 套接字连接将日志消息发送到远程主机。*host* 和 *port* 指定目标。消息的发送格式与 DatagramHandler 中描述的格式相同。与 DatagramHandler 不同，此处理器能可靠地传递日志消息。

`StreamHandler([fileobj])`

将日志消息写入已打开的类文件对象 *fileobj*。如果未提供参数，则消息将写入 `sys.stderr`。

`handlers.SysLogHandler([address [, facility]])`

将日志消息发送到 UNIX 系统日志守护进程。*address* 将目标指定为 `(host, port)` 元组。如果省略，则使用目标 `('localhost', 514)`。*facility* 是一个整数设施代码，默认设置为 `SysLogHandler.LOG_USER`。完整的设施代码列表可在 SysLogHandler 的定义中找到。

`handlers.TimedRotatingFileHandler(filename [, when [, interval [, backupCount [, encoding [, delay [, utc]]]]]])`

与 RotatingFileHandler 相同，但文件的轮转由时间而非文件大小控制。*interval* 是一个数字，*when* 是一个指定单位的字符串。*when* 的可能值有 `'S'`（秒）、`'M'`（分钟）、`'H'`（小时）、`'D'`（天）、`'W'`（周）和 `'midnight'`（在午夜轮转）。例如，将 *interval* 设置为 3，*when* 设置为 `'D'` 表示每三天滚动一次日志。*backupCount* 指定要保留的备份文件的最大数量。*utc* 是一个布尔标志，决定是使用本地时间（默认）还是 UTC 时间。

`handlers.WatchedFileHandler(filename [, mode [, encoding [, delay]]])`

与 FileHandler 相同，但会监控已打开日志文件的 inode 和设备。如果自上次发出日志消息以来它们发生了变化，则关闭该文件并使用相同的文件名重新打开。如果日志文件由于在运行程序外部执行的日志轮转操作而被删除或移动，可能会发生这些变化。此处理器仅适用于 UNIX 系统。

##### 处理器配置

每个 `Handler` 对象 `h` 都可以配置自己的级别和过滤器。以下方法用于此操作：

**`h.setLevel(level)`**

设置要处理的消息阈值。`level` 是一个数值代码，如 `ERROR` 或 `CRITICAL`。

**`h.addFilter(filt)`**

将一个 `Filter` 对象 `filt` 添加到处理器。更多信息请参阅 `Logger` 对象的 `addFilter()` 方法。

**`h.removeFilter(filt)`**

从处理器中移除一个 `Filter` 对象 `filt`。

必须强调的是，级别和过滤器可以在处理器上独立于用于其附加的 `Logger` 对象的任何设置进行设置。以下示例说明了这一点：

```python
import logging
import sys

###### Create a handler that prints CRITICAL level messages to stderr
crit_hand = logging.StreamHandler(sys.stderr)
crit_hand.setLevel(logging.CRITICAL)

###### Create a top-level logger called 'app'
app_log = logging.getLogger("app")
app_log.setLevel(logging.INFO)
app_log.addHandler(logging.FileHandler('app.log'))
app_log.addHandler(crit_handler)
```

在这个示例中，有一个名为 `'app'` 的单一记录器，级别为 `INFO`。它附加了两个处理器，但其中一个处理器（`crit_handler`）有自己的级别设置 `CRITICAL`。尽管此处理器会接收级别为 `INFO` 或更高的日志消息，但它会选择性地丢弃那些不是 `CRITICAL` 的消息。

##### 处理器清理

以下方法用于在处理器上执行清理操作。

**`h.flush()`**

刷新所有日志输出。

**`h.close()`**

关闭处理器。

##### 消息格式化

默认情况下，`Handler` 对象按日志调用中的格式化方式准确地输出日志消息。但是，有时你想向消息添加额外的上下文信息，如时间戳、文件名、行号等。本节

###### Formatter 对象

要更改日志消息格式，必须先创建一个 `Formatter` 对象：

```
Formatter([fmt [, datefmt]])
```

创建一个新的 `Formatter` 对象。`fmt` 为消息提供格式字符串。在 `fmt` 中，你可以放置各种扩展字段，正如前面在 `basicConfig()` 函数中描述的那样。`datefmt` 是与 `time.strftime()` 函数兼容的日期格式字符串。如果省略，则日期格式设置为 ISO8601 格式。

要使其生效，`Formatter` 对象必须附加到 handler 对象上。这通过 `Handler` 实例 `h` 的 `h.setFormatter()` 方法来完成。

```
h.setFormatter(format)
```

设置 `Handler` 实例 `h` 上用于创建日志消息的消息格式化对象。`format` 必须是 `Formatter` 的实例。

以下示例说明了如何在 handler 上自定义日志消息格式：

```
import logging
import sys

###### Set the message format
format = logging.Formatter("%(levelname)-10s %(asctime)s %(message)s")

###### Create a handler that prints CRITICAL level messages to stderr
crit_hand = logging.StreamHandler(sys.stderr)
crit_hand.setLevel(logging.CRITICAL)
crit_hand.setFormatter(format)
```

在此示例中，在 `crit_hand` handler 上设置了自定义 `Formatter`。如果一条类似 `"Creeping death detected."` 的日志消息经过此 handler 处理，将产生以下日志消息：

```
CRITICAL   2005-10-25 20:46:57,126 Creeping death detected.
```

##### 向消息添加额外上下文

在某些应用程序中，向日志消息添加额外的上下文信息很有用。这些额外信息可以通过两种方式之一提供。首先，所有基本日志操作（例如 `log.critical()`、`log.warning()` 等）都有一个关键字参数 `extra`，用于提供一个字典，其中包含可在消息格式字符串中使用的额外字段。这些字段与前面在 `Formatter` 对象中描述的上下文数据合并在一起。以下是一个示例：

```
import logging, socket
logging.basicConfig(
    format = "%(hostname)s %(levelname)-10s %(asctime)s %(message)s"
)
###### Some extra context
netinfo = {
    'hostname' : socket.gethostname(),
    'ip'       : socket.gethostbyname(socket.gethostname())
}
log = logging.getLogger('app')

###### Issue a log message with the extra context data
log.critical("Could not connect to server", extra=netinfo)
```

这种方法的缺点是，你必须确保每次日志操作都包含额外信息，否则程序将会崩溃。另一种方法是使用 `LogAdapter` 类作为现有 logger 的包装器。

**LogAdapter**(*log*[, *extra*])

围绕 `Logger` 对象 *log* 创建一个包装器。*extra* 是一个额外上下文信息的字典，将提供给消息格式化器。`LogAdapter` 实例具有与 `Logger` 对象相同的接口。但是，发出日志消息的操作将自动添加 *extra* 中提供的额外信息。

以下是使用 `LogAdapter` 对象的示例：

```
import logging, socket
logging.basicConfig(
    format = "%(hostname)s %(levelname)-10s %(asctime)s %(message)s"
)
###### Some extra context
netinfo = {
    'hostname' : socket.gethostname(),
    'ip'       : socket.gethostbyname(socket.gethostname())
}

###### Create a logger
log = logging.LogAdapter(logging.getLogger("app"), netinfo)

# Issue a log message.  Extra context data is supplied by the LogAdapter
log.critical("Could not connect to server")
```

##### 其他实用函数

`logging` 中的以下函数控制日志的其他几个方面：

**disable**(*level*)

全局禁用低于 *level* 指定级别的所有日志消息。这可用于在应用范围内关闭日志记录——例如，当你想临时禁用或减少日志输出量时。

**addLevelName**(*level*, *levelName*)

创建一个全新的日志级别和名称。*level* 是一个数字，*levelName* 是一个字符串。这可用于更改内置级别的名称，或添加比默认支持的更多级别。

**getLevelName**(*level*)

返回与数值 *level* 对应的级别名称。

**shutdown**()

关闭所有日志对象，必要时刷新输出。

##### 日志配置

1.  使用 `getLogger()` 创建各种 `Logger` 对象。设置级别等参数。
2.  通过实例化各种类型的 handler（`FileHandler`、`StreamHandler`、`SocketHandler` 等）之一来创建 Handler 对象，并设置适当的级别。
3.  创建消息 Formatter 对象，并使用 `setFormatter()` 方法将它们附加到 Handler 对象。
4.  使用 `addHandler()` 方法将 Handler 对象附加到 Logger 对象。

由于每一步的配置可能较为复杂，最佳做法是将所有日志配置放在一个文档完善的位置。例如，你可以创建一个 `applogconfig.py` 文件，由应用程序的主程序导入：

```
###### applogconfig.py
import logging
import sys

###### Set the message format
format = logging.Formatter("%(levelname)-10s %(asctime)s %(message)s")

###### Create a handler that prints CRITICAL level messages to stderr
crit_hand = logging.StreamHandler(sys.stderr)
crit_hand.setLevel(logging.CRITICAL)
crit_hand.setFormatter(format)

###### Create a handler that prints messages to a file
applog_hand = logging.FileHandler('app.log')
applog_hand.setFormatter(format)

###### Create a top-level logger called 'app'
app_log = logging.getLogger("app")
app_log.setLevel(logging.INFO)
app_log.addHandler(applog_hand)
app_log.addHandler(crit_hand)

###### Change the level on the 'app.net' logger
logging.getLogger("app.net").setLevel(logging.ERROR)
```

如果需要修改日志配置的任何部分，将所有内容集中在一个位置会使维护更加方便。请记住，这个特殊文件只需要导入一次，且只需在程序中的一个位置导入。在代码中需要发出日志消息的其他部分，只需包含如下代码即可：

```
import logging
app_log = logging.getLogger("app")
...
app_log.critical("An error occurred")
```

##### logging.config 子模块

作为在 Python 代码中硬编码日志配置的替代方案，也可以通过使用 INI 格式的配置文件来配置 logging 模块。为此，使用 `logging.config` 中的以下函数。

```
fileConfig(filename [, defaults [, disable_existing_loggers]])
```

从配置文件 *filename* 中读取日志配置。*defaults* 是一个字典，包含配置文件中使用的默认配置参数。指定的文件名使用 `ConfigParser` 模块读取。`disable_existing_loggers` 是一个布尔标志，指定在读取新配置数据时是否禁用任何现有的 logger。默认情况下，该值为 `True`。

`logging` 模块的在线文档详细介绍了配置文件的预期格式。然而，有经验的程序员大概可以从以下示例中推断出来，该示例是前面章节中 `applogconfig.py` 的配置文件版本。

```ini
; applogconfig.ini
; Configuration file for setting up logging
; The following sections provide names for Logger, Handler, and Formatter
; objects that will be configured later in the file.

[loggers]
keys=root,app,app_net

[handlers]
keys=crit,applog

[formatters]
keys=format

[logger_root]
level=NOTSET
handlers=

[logger_app]
level=INFO
propagate=0
qualname=app
handlers=crit,applog

[logger_app_net]
level=ERROR
propagate=1
qualname=app.net
handlers=

[handler_crit]
class=StreamHandler
level=CRITICAL
formatter=format
args=(sys.stderr,)

[handler_applog]
class=FileHandler
level=NOTSET
formatter=format
args=('app.log',)

[formatter_format]
format=%(levelname)-10s %(asctime)s %(message)s
datefmt=
```

要读取此配置文件并设置日志，可以使用以下代码：

```python
import logging.config
```

##### 性能注意事项

如果不小心，向应用程序添加日志记录可能会严重降低其性能。但是，有一些技术可以用来减少开销。

首先，Python的优化模式（`-O`）会移除所有使用 `if __debug__: statements` 之类语句条件执行的代码。如果日志记录的唯一目的是调试，你可以条件执行所有日志调用，并在优化模式下移除这些调用。

第二种技术是在完全禁用日志记录时，使用一个空对象（Null Object）来替代日志记录器对象。这与使用 `None` 不同。相反，你需要使用一个实例，该实例会静默地吞掉所有对其执行的操作。例如：

```python
class Null(object):
    def __init__(self, *args, **kwargs): pass
    def __call__(self, *args, **kwargs): return self
    def __getattr__(self, name): return self
    def __setattr__(self, name, value): pass
    def __delattr__(self, name): pass
```

```python
log = Null()
log.critical("An error occurred.")     # 不执行任何操作
```

根据你的巧妙程度，日志记录也可以通过使用装饰器和元类来管理。因为Python的这些特性在函数、方法和类定义时运行，所以它们可以用来选择性地向程序的某些部分添加或移除日志功能，且在禁用日志时不会影响性能。更多详情请参考第6章“函数与函数式编程”和第7章“类与面向对象编程”。

##### 注意事项

-   `logging` 模块提供了大量此处未讨论的自定义选项。读者应查阅在线文档了解更多细节。
-   在使用线程的程序中使用 `logging` 模块是安全的。特别是，没有必要在发布日志消息的代码周围添加锁定操作。

#### mmap

`mmap` 模块提供了对内存映射文件对象的支持。此对象的行为既像文件也像字节字符串，可以在大多数需要普通文件对象或字节字符串的地方使用。此外，内存映射文件的内容是可变的。这意味着可以使用索引赋值和切片赋值操作符进行修改。除非文件是私有映射的，否则这些更改会直接修改底层文件的内容。

内存映射文件由 `mmap()` 函数创建，该函数在UNIX和Windows上略有不同。

```
mmap(fileno, length [, flags, [prot [, access [, offset]]]])
```

（UNIX）。返回一个将 `fileno`（整数文件描述符）指向文件中的 `length` 字节映射的 mmap 对象。如果 `fileno` 为 -1，则映射匿名内存。`flags` 指定映射的性质，是以下值之一：

| 标志 | 含义 |
|------|------|
| MAP_PRIVATE | 创建一个私有的写时复制映射。对此对象的更改将对此进程私有。 |
| MAP_SHARED | 与所有映射相同文件区域的其他进程共享映射。对此对象的更改将影响所有映射。 |

默认的 `flags` 设置是 `MAP_SHARED`。`prot` 指定对象的内存保护属性，是以下值的按位或：

| 设置 | 含义 |
|------|------|
| PROT_READ | 可以从对象读取数据。 |
| PROT_WRITE | 可以修改对象。 |
| PROT_EXEC | 对象可以包含可执行指令。 |

`prot` 的默认值是 `PROT_READ | PROT_WRITE`。`prot` 中指定的模式必须与打开底层文件描述符 `fileno` 时使用的访问权限匹配。在大多数情况下，这意味着文件应以读/写模式打开（例如，`os.open(name, os.O_RDWR)`）。

可选参数 `access` 可用作 `flags` 和 `prot` 的替代选项。如果提供，它具有以下值之一：

| 访问模式 | 含义 |
|----------|------|
| ACCESS_READ | 只读访问。 |
| ACCESS_WRITE | 读/写访问，写穿。更改会影响底层文件。 |
| ACCESS_COPY | 读/写访问，写时复制。更改影响内存但不改变底层文件。 |

当提供 `access` 时，它通常作为关键字参数给出——例如，`mmap(fileno, length, access=ACCESS_READ)`。同时为 `access` 和 `flags` 提供值是错误的。`offset` 参数指定从文件开头的字节数，默认为 0。它必须是 `mmap.ALLOCATIONGRANULARITY` 的倍数。

```
mmap(fileno, length[, tagname [, access [, offset]]])
```

（Windows）返回一个将 `fileno`（整数文件描述符）指向的文件中的 `length` 字节映射的 mmap 对象。使用 `fileno` 为 -1 映射匿名内存。如果 `length` 大于文件的当前大小，文件将扩展到 `length` 字节。如果 `length` 为 0，只要文件非空，则使用文件的当前长度作为长度（否则将引发异常）。`tagname` 是一个可选的字符串，可用于命名映射。如果 `tagname` 引用现有映射，则打开该映射。否则，创建新映射。如果 `tagname` 为 None，则创建一个未命名的映射。`access` 是一个可选参数，用于指定访问模式。它接受与前面显示的 UNIX 版 `mmap()` 相同的访问值。默认情况下，`access` 是 `ACCESS_WRITE`。`offset` 是从文件开头的字节数，默认为 0。它必须是 `mmap.ALLOCATIONGRANULARITY` 的倍数。

一个内存映射文件对象 `m` 支持以下方法。

```
m.close()
```

关闭文件。后续操作将引发异常。

```
m.find(string[, start])
```

返回 `string` 第一次出现的索引。`start` 指定一个可选的起始位置。如果未找到匹配项，则返回 -1。

```
m.flush([offset, size])
```

将内存中副本的修改刷新回文件系统。`offset` 和 `size` 指定一个要刷新的可选字节范围。否则，将刷新整个映射。

```
m.move(dst, src, count)
```

将从索引 `src` 开始的 `count` 个字节复制到目标索引 `dst`。此复制使用 C 的 `memmove()` 函数执行，该函数保证在源区域和目标区域恰好重叠时也能正确工作。

```
m.read(n)
```

从当前文件位置读取最多 `n` 个字节，并将数据作为字符串返回。

```
m.read_byte()
```

从当前文件位置读取一个字节，并作为长度为 1 的字符串返回。

```
m.readline()
```

从当前文件位置开始返回一行输入。

```
m.resize(newsize)
```

调整内存映射对象的大小以包含 `newsize` 个字节。

```
m.seek(pos[, whence])
```

将文件位置设置为新值。`pos` 和 `whence` 的含义与文件对象上的 `seek()` 方法相同。

```
m.size()
```

返回文件长度。此值可能大于内存映射区域的大小。

```
m.tell()
```

返回文件指针的值。

```
m.write(string)
```

在当前文件指针处将一个字节字符串写入文件。

```
m.write_byte(byte)
```

在当前文件指针处将一个字节写入内存。

##### 注意事项

-   虽然UNIX和Windows提供略有不同的 `mmap()` 函数，但通过依赖两个函数共有的可选 `access` 参数，可以以可移植的方式使用此模块。例如，`mmap(fileno, length, access=ACCESS_WRITE)` 在UNIX和Windows上都能工作。
-   某些内存映射可能仅适用于长度为系统页面大小倍数的情况，该大小包含在常量 `mmap.PAGESIZE` 中。
-   在UNIX SVR4系统上，可以通过以适当权限打开文件 `/dev/zero` 并调用 `mmap()` 来获取匿名映射内存。
-   在UNIX BSD系统上，可以通过使用负文件描述符和标志 `mmap.MAP_ANON` 调用 `mmap()` 来获取匿名映射内存。

#### msvcrt

`msvcrt` 模块提供了对Microsoft Visual C运行时库中许多有用函数的访问。此模块仅在Windows上可用。

```
getch()
```

读取一次按键并返回生成的字符。如果没有可用的按键，此调用会阻塞。如果按下的键是特殊功能键，则调用返回 `'\000'` 或 `'\xe0'`，下一次调用返回键码。此函数不会在控制台回显字符，也不能用于读取 Ctrl+C。

```
getwch()
```

与 `getch()` 相同，但返回一个Unicode字符。

```
getche()
```

类似 `getch()`，但字符会被回显（如果可打印）。

```
getwche()
```

与 `getche()` 相同，但返回一个Unicode字符。

```
get_osfhandle(fd)
```

返回文件描述符 *fd* 的文件句柄。如果 *fd* 未被识别，则引发 `IOError`。

```
heapmin()
```

强制Python内部内存管理器将未使用的块返回给操作系统。此操作仅在Windows NT上有效，失败时引发 `IOError`。



#### optparse

`optparse` 模块提供了对 `sys.argv` 中 UNIX 风格命令行选项的高级支持。使用该模块的一个简单示例见第 9 章。使用 `optparse` 主要围绕 `OptionParser` 类展开。

**`OptionParser([**args])`**

创建一个新的命令选项解析器并返回一个 `OptionParser` 实例。可以提供多种可选的关键字参数来控制配置。这些关键字参数描述如下：

| 关键字参数 | 描述 |
|---|---|
| `add_help_option` | 指定是否支持特殊帮助选项（`--help` 和 `-h`）。默认情况下，此项设置为 `True`。 |
| `conflict_handler` | 指定冲突命令行选项的处理方式。可设置为 `'error'`（默认值）或 `'resolve'`。在 `'error'` 模式下，如果向解析器添加了冲突的选项字符串，将引发 `optparse.OptionConflictError` 异常。在 `'resolve'` 模式下，冲突将被解决，后添加的选项优先。但是，如果较早的选项是以多个名称添加的，且至少其中一个名称不存在冲突，则该选项可能仍然可用。 |
| `description` | 提供程序描述的字符串，用于在显示帮助信息时展示。此字符串在显示时会自动重新格式化以适应屏幕宽度。 |
| `formatter` | 用于格式化打印帮助信息文本的 `optparse.HelpFormatter` 类的实例。可以是 `optparse.IndentedHelpFormatter`（默认值）或 `optparse.TitledHelpFormatter`。 |
| `option_class` | 用于保存每个命令行选项信息的 Python 类。默认类为 `optparse.Option`。 |
| `option_list` | 用于填充解析器的选项列表。默认情况下，此列表为空，选项通过 `add_option()` 方法添加。如果提供了此列表，则包含 `Option` 类型的对象。 |
| `prog` | 用于替换帮助文本中 `'%prog'` 的程序名称。 |
| `usage` | 当使用 `--help` 选项或传递了不正确的选项时打印的用法字符串。默认值是字符串 `'%prog [options]'`，其中 `'%prog'` 关键字会被替换为 `os.path.basename(sys.argv[0])` 的值或 `prog` 关键字参数的值（如果已提供）。可以指定值 `optparse.SUPPRESS_USAGE` 来完全抑制用法消息。 |
| `version` | 当提供 `--version` 选项时打印的版本字符串。默认情况下，`version` 为 `None`，不会添加 `--version` 选项。当提供了此字符串时，`--version` 会被自动添加。特殊关键字 `'%prog'` 会被替换为程序名称。 |

除非你确实需要以某种方式自定义选项处理，否则通常会创建一个不带参数的 `OptionParser`。例如：

```
p = optparse.OptionParser()
```

`OptionParser` 的实例 `p` 支持以下方法：

**p.add_option(name1, ..., nameN [, **parms])**

向 `p` 添加一个新选项。参数 `name1`、`name2` 等都是该选项的各种名称。例如，你可以包含短选项和长选项名称，如 `'-f'` 和 `'--file'`。在选项名称之后，提供一组可选的关键字参数来指定解析时如何处理该选项。这些关键字参数描述如下：

| 关键字参数 | 描述 |
|---|---|
| `action` | 解析选项时要执行的操作。可接受的值如下：<br><br>`'store'`—选项有一个参数，该参数被读取并存储。如果未显式指定操作，这是默认值。<br><br>`'store_const'`—选项不接受参数，但当遇到该选项时，会存储通过 `const` 关键字参数指定的常量值。<br><br>`'store_true'`—类似于 `'store_const'`，但在解析选项时存储布尔值 `True`。<br><br>`'store_false'`—类似于 `'store_true'`，但存储 `False`。<br><br>`'append'`—选项有一个参数，解析时将其追加到列表中。当同一命令行选项用于指定多个值时使用。<br><br>`'count'`—选项不接受参数，但会存储一个计数器值。每次遇到该参数时，计数器值加一。<br><br>`'callback'`—当遇到该选项时，调用通过 `callback` 关键字参数指定的回调函数。<br><br>`'help'`—解析选项时打印帮助消息。仅当你希望帮助通过标准 `-h` 或 `--help` 以外的选项显示时才需要。<br><br>`'version'`—打印提供给 `OptionParser()` 的版本号（如果有）。仅当你希望使用标准 `-v` 或 `--version` 以外的选项显示版本信息时使用。 |
| `callback` | 指定当遇到该选项时要调用的回调函数。此回调函数是一个 Python 可调用对象，调用方式为 `callback(option, opt_str, value, parser, *args, **kwargs)`。`option` 参数是 `optparse.Option` 的实例，`opt_str` 是触发回调的命令行上提供的选项字符串，`value` 是选项的值（如果有），`parser` 是正在运行的 `OptionParser` 实例，`args` 是通过 `callback_args` 关键字参数提供的位置参数，`kwargs` 是通过 `callback_kwargs` 关键字参数提供的关键字参数。 |
| `callback_args` | 提供给通过 callback 参数指定的回调函数的可选位置参数。 |
| `callback_kwargs` | 提供给通过 callback 参数指定的回调函数的可选关键字参数。 |
| `choices` | 指定所有可能选项值的字符串列表。当选项只有有限的值集时使用（例如 ['small', 'medium', 'large']）。 |
| `const` | 与 'store_const' 操作一起存储的常量值。 |
| `default` | 设置选项在未提供时的默认值。默认情况下，默认值为 None。 |
| `dest` | 设置在解析过程中用于存储选项值的属性名称。通常该名称从选项名称本身派生。 |
| `help` | 此特定选项的帮助文本。如果未提供，该选项将在帮助信息中列出但没有描述。值 optparse.SUPPRESS_HELP 可用于隐藏选项。特殊关键字 '%default' 在帮助字符串中会被替换为选项的默认值。 |
| `metavar` | 指定打印帮助文本时使用的选项参数名称。 |
| `nargs` | 指定需要参数的操作的选项参数数量。默认值为 1。如果使用大于 1 的数字，选项参数将被收集到一个元组中，然后在处理参数时使用。 |
| `type` | 指定选项的类型。有效类型为 'string'（默认值）、'int'、'long'、'choice'、'float' 和 'complex'。 |

**p.disable_interspersed_args()**

禁止将简单选项与位置参数混合使用。例如，如果 '-x' 和 '-y' 是不接受参数的选项，则这些选项必须出现在任何参数之前（例如 'prog -x -y arg1 arg2 arg3'）。

**p.enable_interspersed_args()**

允许将选项与位置参数混合使用。例如，如果 '-x' 和 '-y' 是不接受参数的简单选项，它们可以与参数混合，如 'prog -x arg1 arg2 -y arg3'。这是默认行为。

**p.parse_args([arglist])**

解析命令行选项并返回一个元组 (options, args)，其中 options 是一个包含所有选项值的对象，args 是所有剩余位置参数的列表。options 对象将所有选项数据存储在名称与选项名称匹配的属性中。例如，选项 '--output' 的值将存储在 options.output 中。如果该选项未出现，则值为 None。属性的名称可以使用之前描述的 add_option() 的 dest 关键字参数来设置。默认情况下，参数从 sys.argv[1:] 中获取。但是，可以通过可选参数 arglist 提供不同的参数来源。



##### 示例

```python
###### foo.py
import optparse
p = optparse.OptionParser()

###### A simple option, with no arguments
p.add_option("-t", action="store_true", dest="tracing")

###### An option that accepts a string argument
p.add_option("-o", "--outfile", action="store", type="string", dest="outfile")

###### An option requires an integer argument
p.add_option("-d", "--debuglevel", action="store", type="int", dest="debug")

###### An option with a few choices
p.add_option("--speed", action="store", type="choice", dest="speed",
        choices=["slow","fast","ludicrous"])

###### An option taking multiple arguments
p.add_option("--coord", action="store", type="int", dest="coord", nargs=2)

###### A set of options that control a common destination
p.add_option("--novice", action="store_const", const="novice", dest="mode")
p.add_option("--guru", action="store_const", const="guru", dest="mode")

###### Set default values for the various option destinations
p.set_defaults(tracing=False,
        debug=0,
        speed="fast",
        coord=(0,0),
        mode="novice")

###### Parse the arguments
opt, args = p.parse_args()

###### Print option values
print "tracing    :", opt.tracing
print "outfile    :", opt.outfile
print "debug      :", opt.debug
print "speed      :", opt.speed
print "coord      :", opt.coord
print "mode       :", opt.mode

###### Print remaining arguments
print "args       :", args
```

`p.set_defaults(dest=value, ... dest=value)`
设置特定选项目标的默认值。你只需提供关键字参数来指定要设置的目标。关键字参数的名称应与之前描述的 `add_option()` 中 `dest` 参数指定的名称相匹配。

`p.set_usage(usage)`
更改 `--help` 选项生成的文本中显示的用法字符串。

下面是一个简短的交互式 UNIX 会话，展示了上述代码的工作方式：

```
% python foo.py -h
usage: foo.py [options]

options:
  -h, --help            show this help message and exit
  -t
  -o OUTFILE, --outfile=OUTFILE
  -d DEBUG, --debuglevel=DEBUG
  --speed=SPEED
  --coord=COORD
  --novice
  --guru
```

```
% python foo.py -t -o outfile.dat -d 3 --coord 3 4 --speed=ludicrous blah
tracing  : True
outfile  : outfile.dat
debug    : 3
speed    : ludicrous
coord    : (3, 4)
mode     : novice
args     : ['blah']
```

```
% python foo.py --speed=insane
usage: foo.py [options]

foo.py:error:option --speed:invalid choice:'insane'
(choose from 'slow', 'fast', 'ludicrous')
```

##### 注意事项

- 在指定选项名称时，使用单个短横线指定短名称，例如 `'-x'`，使用双短横线指定长名称，例如 `'--exclude'`。如果你尝试定义一个混合了两种风格的选项，例如 `'-exclude'`，将会抛出 `OptionError` 异常。

- Python 还包含一个名为 `getopt` 的模块，它以类似于同名 C 库的风格提供命令行解析支持。实际上，使用该模块相比 `optparse`（其层级更高且需要编写的代码少得多）没有任何优势。

- `optparse` 模块包含大量与自定义和特定类型命令行选项的专门处理相关的高级功能。然而，对于最常见的命令行选项解析类型，这些功能都不是必需的。读者应查阅在线库文档以获取更多详细信息和额外示例。

#### OS

`os` 模块提供了对常见操作系统服务的可移植接口。它通过搜索依赖于操作系统的内置模块（如 `nt` 或 `posix`）并将其中找到的函数和数据导出来实现这一点。除非另有说明，函数在 Windows 和 UNIX 上均可使用。UNIX 系统包括 Linux 和 Mac OS X。

定义了以下通用变量：

##### environ
表示当前环境变量的映射对象。对映射的更改会反映在当前环境中。如果 `putenv()` 函数也可用，则更改也会反映在子进程中。

##### linesep
当前平台上用于分隔行的字符串。可能是单个字符（如 POSIX 上的 `'\n'`）或多个字符（如 Windows 上的 `'\r\n'`）。

##### name
导入的依赖于操作系统的模块名称：`'posix'`、`'nt'`、`'dos'`、`'mac'`、`'ce'`、`'java'`、`'os2'` 或 `'riscos'`。

##### path
用于路径名操作的依赖于操作系统的标准模块。也可以使用 `import os.path` 加载此模块。

##### 进程环境
以下函数用于访问和修改与进程运行环境相关的各种参数。除非另有说明，进程、进程组、进程组和会话 ID 均为整数。

###### chdir(path)
将当前工作目录更改为 `path`。

###### chroot(path)
更改当前进程的根目录（UNIX）。

###### ctermid()
返回包含进程控制终端文件名的字符串（UNIX）。

###### fchdir(fd)
更改当前工作目录。`fd` 是指向已打开目录的文件描述符（UNIX）。

###### getcwd()
返回包含当前工作目录的字符串。

###### getcwdu()
返回包含当前工作目录的 Unicode 字符串。

###### getegid()
返回有效组 ID（UNIX）。

###### geteuid()
返回有效用户 ID（UNIX）。

###### getgid()
返回进程的真实组 ID（UNIX）。

###### getgroups()
返回进程所有者所属的整数组 ID 列表（UNIX）。

###### getlogin()
返回与有效用户 ID 关联的用户名（UNIX）。

###### getpgid(pid)
返回进程 ID 为 *pid* 的进程的进程组 ID。如果 *pid* 为 0，则返回调用进程的进程组（UNIX）。

###### getpgrp()
返回当前进程组的 ID。进程组通常与作业控制结合使用。进程组不一定与进程的组 ID 相同（UNIX）。

###### getpid()
返回当前进程的真实进程 ID（UNIX 和 Windows）。

###### getppid()
返回父进程的进程 ID（UNIX）。

###### getsid(pid)
返回进程 *pid* 的进程会话标识符。如果 *pid* 为 0，则返回当前进程的标识符（UNIX）。

###### getuid()
返回当前进程的真实用户 ID（UNIX）。

###### putenv(varname, value)
将环境变量 *varname* 设置为 *value*。更改会影响使用 *os.system()*、*popen()*、*fork()* 和 *execv()* 启动的子进程。对 *os.environ* 中项目的赋值会自动调用 *putenv()*。但是，调用 *putenv()* 不会更新 *os.environ*（UNIX 和 Windows）。

###### setegid(egid)
设置有效组 ID（UNIX）。

###### seteuid(euid)
设置有效用户 ID（UNIX）。

###### setgid(gid)
设置当前进程的组 ID（UNIX）。

###### setgroups(groups)
设置当前进程的组访问列表。*groups* 是指定组标识符的整数序列。只能由 root 调用（UNIX）。

###### setpgrp()
通过调用系统调用 `setpgrp()` 或 `setpgrp(0, 0)`（取决于实现的版本，如果有的话）创建新的进程组。返回新进程组的 ID（UNIX）。

###### setpgid(pid, pgrp)
将进程 *pid* 分配给进程组 *pgrp*。如果 *pid* 等于 *pgrp*，则该进程成为新的进程组领导者。如果 *pid* 不等于 *pgrp*，则该进程加入现有组。如果 *pid* 为 0，则使用调用进程的进程 ID。如果 *pgrp* 为 0，则由 *pid* 指定的进程成为进程组领导者（UNIX）。

###### setreuid(ruid, euid)
设置调用进程的真实和有效用户 ID（UNIX）。

###### setregid(rgid, egid)
设置调用进程的真实和有效组 ID（UNIX）。

###### setsid()
创建新的会话并返回新创建的会话 ID。会话通常与终端设备以及在其中启动的进程的作业控制相关联（UNIX）。

###### setuid(uid)
设置当前进程的真实用户 ID。此函数是特权函数，通常只能由以 root 身份运行的进程执行（UNIX）。

###### strerror(code)
返回与整数错误代码对应的错误消息（UNIX 和 Windows）。`errno` 模块定义了这些错误代码的符号名称。

###### umask(mask)
设置当前数字 umask 并返回之前的 umask。umask 用于清除进程创建的文件的权限位（UNIX 和 Windows）。

###### uname()
返回标识系统类型的字符串元组（sysname、nodename、release、version、machine）（UNIX）。

###### unsetenv(name)
取消设置环境变量 *name*。

##### 文件创建和文件描述符
以下函数提供了用于操作文件和管道的底层接口。在这些函数中，文件通过整数文件描述符 `fd` 进行操作。可以通过调用文件对象的 `fileno()` 方法来提取文件描述符。

###### close(fd)
关闭之前由 `open()` 或 `pipe()` 返回的文件描述符 `fd`。



## 第19章 操作系统服务

```
closerange(low, high)
```

关闭所有文件描述符 $fd$，其范围为 `low <= fd < high`。错误将被忽略。

```
dup(fd)
```

复制文件描述符 $fd$。返回一个新的文件描述符，它是进程当前未使用的最小编号的文件描述符。新的和旧的文件描述符可以互换使用。此外，它们共享状态，例如当前文件指针和锁（UNIX 和 Windows）。

```
dup2(oldfd, newfd)
```

将文件描述符 `oldfd` 复制到 `newfd`。如果 `newfd` 已经对应一个有效的文件描述符，它将首先被关闭（UNIX 和 Windows）。

```
fchmod(fd, mode)
```

将与 $fd$ 关联的文件的模式更改为 `mode`。有关 `mode` 的描述，请参见 `os.open()` 的说明（UNIX）。

```
fchown(fd, uid, gid)
```

将与 $fd$ 关联的文件的所有者和组 ID 更改为 `uid` 和 `gid`。对于 `uid` 或 `gid` 使用值为 -1 表示保持原值不变（UNIX）。

```
fdatasync(fd)
```

强制将所有缓存的数据刷新到磁盘（UNIX）。

```
fdopen(fd [, mode [, bufsize]])
```

创建一个与文件描述符 $fd$ 关联的已打开文件对象。`mode` 和 `bufsize` 参数与内置 `open()` 函数中的含义相同。`mode` 应该是一个字符串，如 `'r'`、`'w'` 或 `'a'`。在 Python 3 中，此函数接受任何与内置 `open()` 函数兼容的附加参数，例如编码和行尾的指定。但是，如果需要与 Python 2 的可移植性，您应该只使用此处描述的 `mode` 和 `bufsize` 参数。

```
fpathconf(fd, name)
```

返回与文件描述符为 $fd$ 的打开文件关联的可配置路径名变量。`name` 是一个字符串，指定要检索的值的名称。这些值通常取自系统头文件（如 `<limits.h>` 和 `<unistd.h>`）中包含的参数。POSIX 为 `name` 定义了以下常量：

| 常量 | 描述 |
|----------|-------------|
| "PC_ASYNC_IO" | 指示是否可以对 $fd$ 执行异步 I/O。 |
| "PC_CHOWN_RESTRICTED" | 指示是否可以使用 `chown()` 函数。如果 $fd$ 指向一个目录，则适用于该目录中的所有文件。 |
| "PC_FILESIZEBITS" | 文件的最大大小。 |
| "PC_LINK_MAX" | 文件链接计数的最大值。 |
| "PC_MAX_CANON" | 格式化输入行的最大长度。$fd$ 指向一个终端。 |
| "PC_MAX_INPUT" | 输入行的最大长度。$fd$ 指向一个终端。 |
| "PC_NAME_MAX" | 目录中文件名的最大长度。 |
| "PC_NO_TRUNC" | 指示如果尝试创建文件名超过目录 PC_NAME_MAX 的文件，是否会因 ENAMETOOLONG 错误而失败。 |
| "PC_PATH_MAX" | 当目录 fd 是当前工作目录时，相对路径名的最大长度。 |
| "PC_PIPE_BUF" | 当 fd 指向管道或 FIFO 时，管道缓冲区的大小。 |
| "PC_PRIO_IO" | 指示是否可以对 fd 执行优先级 I/O。 |
| "PC_SYNC_IO" | 指示是否可以对 fd 执行同步 I/O。 |
| "PC_VDISABLE" | 指示 fd 是否允许禁用特殊字符处理。fd 必须指向一个终端。 |

并非所有名称在所有平台上都可用，并且某些系统可能定义额外的配置参数。但是，可以在字典 os.pathconf_names 中找到操作系统已知的名称列表。如果已知的配置名称未包含在 os.pathconf_names 中，其整数值也可以作为 name 传递。即使 Python 识别了一个名称，如果主机操作系统不识别该参数或无法将其与文件 fd 关联，此函数仍可能引发 OSError。此函数仅在某些版本的 UNIX 上可用。

###### fstat(fd)

返回文件描述符 fd 的状态。返回与 os.stat() 函数相同的值（UNIX 和 Windows）。

###### fstatvfs(fd)

返回包含与文件描述符 fd 关联文件的文件系统的信息。返回与 os.statvfs() 函数相同的值（UNIX）。

###### fsync(fd)

强制将 fd 上任何未写入的数据写入磁盘。请注意，如果您正在使用带有缓冲 I/O 的对象（例如，Python 文件对象），则应在调用 fsync() 之前首先刷新数据。在 UNIX 和 Windows 上可用。

###### ftruncate(fd, length)

截断与文件描述符 fd 对应的文件，使其大小最多为 length 字节（UNIX）。

###### isatty(fd)

如果 fd 与类似 TTY 的设备（如终端）关联，则返回 True（UNIX）。

###### lseek(fd, pos, how)

将文件描述符 fd 的当前位置设置为位置 pos。how 的值如下：SEEK_SET 相对于文件开头设置位置，SEEK_CUR 相对于当前位置设置，SEEK_END 相对于文件末尾设置。在较旧的 Python 代码中，通常看到这些常量被替换为它们的数字值 0、1 或 2。

```
open(file [, flags [, mode]])
```

打开文件 *file*。*flags* 是以下常量值的按位或：

| 值 | 描述 |
|-------|-------------|
| O_RDONLY | 打开文件进行读取。 |
| O_WRONLY | 打开文件进行写入。 |
| O_RDWR | 打开进行读写（更新）。 |
| O_APPEND | 将字节附加到文件末尾。 |
| O_CREAT | 如果文件不存在，则创建它。 |
| O_NONBLOCK | 在打开、读取或写入时不阻塞（UNIX）。 |
| O_NDELAY | 与 O_NONBLOCK 相同（UNIX）。 |
| O_DSYNC | 同步写入（UNIX）。 |
| O_NOCTTY | 打开设备时，不设置控制终端（UNIX）。 |
| O_TRUNC | 如果文件存在，则截断为零长度。 |
| O_RSYNC | 同步读取（UNIX）。 |
| O_SYNC | 同步写入（UNIX）。 |
| O_EXCL | 如果 O_CREAT 和文件已存在，则出错。 |
| O_EXLOCK | 在文件上设置排他锁。 |
| O_SHLOCK | 在文件上设置共享锁。 |
| O_ASYNC | 启用异步输入模式，当输入可用时生成 SIGIO 信号。 |
| O_DIRECT | 使用直接 I/O 模式，读写操作直接进入磁盘，而不是通过操作系统读写缓存。 |
| O_DIRECTORY | 如果文件不是目录，则引发错误。 |
| O_NOFOLLOW | 不跟随符号链接。 |
| O_NOATIME | 不更新文件的最后访问时间。 |
| O_TEXT | 文本模式（Windows）。 |
| O_BINARY | 二进制模式（Windows）。 |
| O_NOINHERIT | 文件不被子进程继承（Windows）。 |
| O_SHORT_LIVED | 向系统提示该文件用于短期存储（Windows）。 |
| O_TEMPORARY | 关闭时删除文件（Windows）。 |
| O_RANDOM | 向系统提示该文件将用于随机访问（Windows）。 |
| O_SEQUENTIAL | 向系统提示该文件将被顺序访问（Windows）。 |

同步 I/O 模式（O_SYNC、O_DSYNC、O_RSYNC）强制 I/O 操作阻塞，直到它们在硬件级别完成（例如，写入将阻塞，直到字节物理写入磁盘）。*mode* 参数包含文件权限，表示为以下八进制值的按位或（如 `stat` 模块中定义的常量）：

| 模式 | 含义 |
|------|---------|
| 0100 | 用户具有执行权限（`stat.S_IXUSR`）。 |
| 0200 | 用户具有写入权限（`stat.S_IWUSR`）。 |
| 0400 | 用户具有读取权限（`stat.S_IRUSR`）。 |
| 0700 | 用户具有读/写/执行权限（`stat.S_IRWXU`）。 |
| 0010 | 组具有执行权限（`stat.S_IXGRP`）。 |
| 0020 | 组具有写入权限（`stat.S_IWGRP`）。 |
| 0040 | 组具有读取权限（`stat.S_IRGRP`）。 |
| 0070 | 组具有读/写/执行权限（`stat.S_IRWXG`）。 |
| 0001 | 其他用户具有执行权限（`stat.S_IXOTH`）。 |
| 0002 | 其他用户具有写入权限（`stat.S_IWOTH`）。 |
| 0004 | 其他用户具有读取权限（`stat.S_IROTH`）。 |
| 0007 | 其他用户具有读/写/执行权限（`stat.S_IRWXO`）。 |
| 4000 | 设置 UID 模式（`stat.S_ISUID`）。 |
| 2000 | 设置 GID 模式（`stat.S_ISGID`）。 |
| 1000 | 设置粘滞位（`stat.S_ISVTX`）。 |

文件的默认模式是 `(0777 & ~umask)`，其中 umask 设置用于移除选定的权限。例如，umask 为 `0022` 会移除组和其他用户的写入权限。可以使用 `os.umask()` 函数更改 umask。umask 设置在 Windows 上没有效果。

###### openpty()

打开一个伪终端，并返回一对用于 PTY 和 TTY 的文件描述符（`master, slave`）。在某些版本的 UNIX 上可用。

###### pipe()

创建一个管道，可用于与另一个进程建立单向通信。返回一对文件描述符（`r, w`），分别用于读取和写入。此函数通常在执行 `fork()` 函数之前调用。在 `fork()` 之后，发送进程关闭管道的读取端，接收进程关闭管道的写入端。此时，管道被激活，可以使用 `read()` 和 `write()` 函数将数据从一个进程发送到另一个进程（UNIX）。

###### read(fd, n)

从文件描述符 *fd* 读取最多 *n* 个字节。返回包含读取字节的字节字符串。

###### tcgetpgrp(fd)

返回与 *fd* 给定的控制终端关联的进程组（UNIX）。

###### tcsetpgrp(fd, pg)

设置与 *fd* 给定的控制终端关联的进程组（UNIX）。

###### ttyname(fd)

返回一个字符串，指定与文件描述符 *fd* 关联的终端设备。如果 *fd* 未与终端设备关联，则引发 `OSError` 异常（UNIX）。

###### write(fd, str)

将字节字符串 *str* 写入文件描述符 *fd*。返回实际写入的字节数。



##### 文件与目录

以下函数和变量用于操作文件系统上的文件和目录。为了处理文件命名方案的差异，以下变量包含有关路径名构建的信息：

| 变量 | 描述 |
|------|------|
| altsep | 操作系统用于分隔路径名组件的备用字符，如果仅存在一个分隔符字符，则为 None。在 DOS 和 Windows 系统上设置为 '/'，此时 sep 为反斜杠。 |
| curdir | 用于引用当前工作目录的字符串：UNIX 和 Windows 上是 '.'，Macintosh 上是 ':'。 |
| devnull | 空设备的路径（例如 /dev/null）。 |
| extsep | 将基本文件名与其类型分开的字符（例如 'foo.txt' 中的 '.'）。 |
| pardir | 用于引用父目录的字符串：UNIX 和 Windows 上是 '..'，Macintosh 上是 '::'。 |
| pathsep | 用于分隔搜索路径组件（如 $PATH 环境变量中所包含的）的字符：UNIX 上是 ':'，DOS 和 Windows 上是 ';'。 |
| sep | 用于分隔路径名组件的字符：UNIX 和 Windows 上是 '/'，Macintosh 上是 ':'。 |

以下函数用于操作文件：

```
access(path, accessmode)
```

检查此进程访问文件路径 path 的读/写/执行权限。accessmode 分别为 R_OK、W_OK、X_OK 或 F_OK，代表读、写、执行或存在性。如果授予访问权限返回 1，否则返回 0。

```
chflags(path, flags)
```

更改 path 上的文件标志。flags 是下列常量的按位或值。以 UF_ 开头的标志可由任何用户设置，而 SF_ 标志只能由超级用户（UNIX）更改。

| 标志 | 含义 |
|------|------|
| stat.UF_NODUMP | 不转储文件。 |
| stat.UF_IMMUTABLE | 文件为只读。 |
| stat.UF_APPEND | 文件仅支持追加操作。 |
| stat.UF_OPAQUE | 目录是不透明的。 |
| stat.UF_NOUNLINK | 文件不可删除或重命名。 |
| stat.SF_ARCHIVED | 文件可以归档。 |
| stat.SF_IMMUTABLE | 文件为只读。 |
| stat.SF_APPEND | 文件仅支持追加操作。 |
| stat.SF_NOUNLINK | 文件不可删除或重命名。 |
| stat.SF_SNAPSHOT | 文件是快照文件。 |

```
chmod(path, mode)
```

更改 *path* 的模式。*mode* 具有与 *open()* 函数描述相同的值（UNIX 和 Windows）。

```
chown(path, uid, gid)
```

将 *path* 的所有者和组 ID 更改为数字 *uid* 和 *gid*。将 *uid* 或 *gid* 设置为 -1 会使该参数保持未修改（UNIX）。

```
lchflags(path, flags)
```

与 *chflags()* 相同，但不跟踪符号链接（UNIX）。

```
lchmod(path, mode)
```

与 *chmod()* 相同，不同之处在于如果 *path* 是符号链接，则修改链接本身，而不是链接所指向的文件。

```
lchown(path, uid, gid)
```

与 *chown()* 相同，但不跟踪符号链接（UNIX）。

```
link(src, dst)
```

创建一个名为 *dst* 的硬链接，指向 *src*（UNIX）。

```
listdir(path)
```

返回一个列表，其中包含目录 *path* 中条目的名称。列表按任意顺序返回，不包含特殊条目 '.' 和 '..'。如果 *path* 是 Unicode，则结果列表将仅包含 Unicode 字符串。请注意，如果目录中的任何文件名无法正确编码为 Unicode，则会被静默跳过。如果 *path* 以字节字符串给出，则所有文件名都作为字节字符串列表返回。

```
lstat(path)
```

类似于 *stat()*，但不跟踪符号链接（UNIX）。

```
makedev(major, minor)
```

根据主设备号和次设备号创建原始设备号（UNIX）。

```
major(devicenum)
```

从由 *makedev()* 创建的原始设备号 *devicenum* 返回主设备号。

```
minor(devicenum)
```

从由 *makedev()* 创建的原始设备号 *devicenum* 返回次设备号。

```
makedirs(path [, mode])
```

递归目录创建函数。类似于 *mkdir()*，但创建包含叶目录所需的所有中间级目录。如果叶目录已存在或无法创建，则会引发 *OSError* 异常。

```
mkdir(path [, mode])
```

创建一个名为 *path* 的目录，数字模式为 *mode*。默认模式为 `0777`。在非 UNIX 系统上，模式设置可能无效或被忽略。

```
mkfifo(path [, mode])
```

创建一个名为 *path* 的 FIFO（命名管道），数字模式为 *mode*。默认模式为 `0666`（UNIX）。

```
mknod(path [, mode, device])
```

创建设备特殊文件。*path* 是文件的名称，*mode* 指定文件的权限和类型，*device* 是使用 `os.makedev()` 创建的原始设备号。*mode* 参数在设置文件访问权限时接受与 `open()` 相同的参数。此外，标志 `stat.S_IFREG`、`stat.S_IFCHR`、`stat.S_IFBLK` 和 `stat.S_IFIFO` 会添加到 *mode* 中以指示文件类型（UNIX）。

```
pathconf(path, name)
```

返回与路径名 *path* 相关的可配置系统参数。*name* 是指定参数名称的字符串，与 `fpathconf()` 函数描述相同（UNIX）。

```
readlink(path)
```

返回一个字符串，表示符号链接 *path* 指向的路径（UNIX）。

```
remove(path)
```

删除文件 *path*。这与 `unlink()` 函数相同。

```
removedirs(path)
```

递归目录删除函数。工作方式类似于 `rmdir()`，不同之处在于，如果叶目录被成功删除，则将修剪对应于最右边路径段的目录，直到整个路径被消耗完或引发错误（该错误被忽略，因为它通常意味着父目录不为空）。如果叶目录无法成功删除，则会引发 `OSError` 异常。

```
rename(src, dst)
```

将文件或目录 *src* 重命名为 *dst*。

```
renames(old, new)
```

递归目录重命名或文件重命名函数。工作方式类似于 `rename()`，不同之处在于它首先尝试创建新路径名所需的任何中间目录。重命名后，将使用 `removedirs()` 修剪对应于旧名称最右边路径段的目录。

```
rmdir(path)
```

删除目录 *path*。

```
stat(path)
```

对给定的 *path* 执行 `stat()` 系统调用以提取有关文件的信息。返回值是一个对象，其属性包含文件信息。常见属性包括：

| 属性 | 描述 |
|------|------|
| st_mode | Inode 保护模式 |
| st_ino | Inode 编号 |
| st_dev | Inode 所在的设备 |
| st_nlink | 指向 Inode 的链接数 |
| st_uid | 所有者的用户 ID |
| st_gid | 所有者的组 ID |
| st_size | 以字节为单位的文件大小 |
| st_atime | 最后访问时间 |
| st_mtime | 最后修改时间 |
| st_ctime | 最后状态更改时间 |

但是，根据系统，可能存在其他属性。stat() 返回的对象也类似于一个 10 元组，包含参数 (st_mode, st_ino, st_dev, st_nlink, st_uid, st_gid, st_size, st_atime, st_mtime, st_ctime)。后一种形式是为了向后兼容而提供的。stat 模块定义了用于从此元组中提取字段的常量。

```
stat_float_times([newvalue])
```

如果 stat() 返回的时间是浮点数而不是整数，则返回 True。可以通过为 newvalue 提供布尔值来更改行为。

```
statvfs(path)
```

对给定路径执行 statvfs() 系统调用以获取有关文件系统的信息。返回值是一个对象，其属性描述文件系统。常见属性包括：

| 属性 | 描述 |
|------|------|
| f_bsize | 首选系统块大小 |
| f_frsize | 基本文件系统块大小 |
| f_blocks | 文件系统中的总块数 |
| f_bfree | 空闲块总数 |
| f_bavail | 非超级用户可用的空闲块 |
| f_files | 文件 Inode 总数 |
| f_ffree | 空闲文件 Inode 总数 |
| f_favail | 非超级用户可用的空闲 Inode |
| f_flag | 标志（系统相关） |
| f_namemax | 最大文件名长度 |

返回的对象也类似于一个元组，按列出的顺序包含这些属性。标准模块 statvfs 定义了可用于从返回的 statvfs 数据中提取信息的常量（UNIX）。

```
symlink(src, dst)
```

创建一个名为 dst 的符号链接，指向 src。



**unlink(path)**

删除文件 *path*。与 `remove()` 功能相同。

**utime(path, (atime, mtime))**

将文件的访问时间和修改时间设置为给定的值。（第二个参数是一个包含两个项目的元组。）时间参数以 `time.time()` 函数返回的数字表示。

**walk(top [, topdown [, onerror [,followlinks]]])**

创建一个遍历目录树的生成器对象。`top` 指定目录的顶层，`topdown` 是一个布尔值，指示是以自顶向下（默认）还是自底向上的顺序遍历目录。返回的生成器生成元组 `(dirpath, dirnames, filenames)`，其中 `dirpath` 是一个包含目录路径的字符串，`dirnames` 是 `dirpath` 中所有子目录的列表，`filenames` 是 `dirpath` 中文件的列表，不包括目录。`onerror` 参数是一个接受单个参数的函数。如果处理过程中发生任何错误，该函数将被传递一个 `os.error` 实例。默认行为是忽略错误。如果以自顶向下的方式遍历目录，对 `dirnames` 的修改会影响遍历过程。例如，如果从 `dirnames` 中删除目录，这些目录将被跳过。默认情况下，符号链接不会被跟随，除非 `followlinks` 参数设置为 `True`。

##### 进程管理

以下函数和变量用于创建、销毁和管理进程：

**abort()**

生成一个 `SIGABRT` 信号并发送给调用进程。除非该信号被信号处理器捕获，否则默认情况下进程将因错误而终止。

**defpath**

此变量包含 `exec*p*()` 函数在环境没有 `'PATH'` 变量时使用的默认搜索路径。

**execl(path, arg0, arg1, ...)**

等同于 `execv(path, (arg0, arg1, ...))`。

**execle(path, arg0, arg1, ..., env)**

等同于 `execve(path, (arg0, arg1, ...), env)`。

**execlp(path, arg0, arg1, ...)**

等同于 `execvp(path, (arg0, arg1, ...))`。

**execv(path, args)**

执行程序 `path`，参数列表为 `args`，替换当前进程（即 Python 解释器）。参数列表可以是字符串元组或列表。

**execve(path, args, env)**

像 `execv()` 一样执行一个新程序，但额外接受一个字典 `env`，用于定义程序运行的环境。`env` 必须是一个将字符串映射到字符串的字典。

**execvp(path, args)**

类似 `execv(path, args)`，但复制了 shell 在目录列表中搜索可执行文件的操作。目录列表从 `environ['PATH']` 获取。

**execvpe(path, args, env)**

类似 `execvp()`，但带有一个附加的环境变量，如 `execve()` 函数。

**_exit(n)**

立即以状态 `n` 退出系统，不执行任何清理操作。这通常仅在由 `fork()` 创建的子进程中执行。这也与调用 `sys.exit()` 不同，后者会优雅地关闭解释器。退出代码 `n` 取决于应用程序，但值为 0 通常表示成功，而非零值表示某种错误。根据系统，可能定义了一些标准退出代码值：

| 值 | 描述 |
|-------|-------------|
| EX_OK | 无错误。 |
| EX_USAGE | 命令使用不正确。 |
| EX_DATAERR | 输入数据不正确。 |
| EX_NOINPUT | 缺少输入。 |
| EX_NOUSER | 用户不存在。 |
| EX_NOHOST | 主机不存在。 |
| EX_NOTFOUND | 未找到。 |
| EX_UNAVAILABLE | 服务不可用。 |
| EX_SOFTWARE | 内部软件错误。 |
| EX_OSERR | 操作系统错误。 |
| EX_OSFILE | 文件系统错误。 |
| EX_CANTCREAT | 无法创建输出。 |
| EX_IOERR | I/O 错误。 |
| EX_TEMPFAIL | 临时失败。 |
| EX_PROTOCOL | 协议错误。 |
| EX_NOPERM | 权限不足。 |
| EX_CONFIG | 配置错误。 |

**fork()**

创建一个子进程。在新创建的子进程中返回 0，在原始进程中返回子进程的进程 ID。子进程是原始进程的克隆，并共享许多资源，如打开的文件（UNIX）。

**forkpty()**

创建一个子进程，使用新的伪终端作为子进程的控制终端。返回一个元组 `(pid, fd)`，其中 `pid` 在子进程中为 0，`fd` 是伪终端主端的文件描述符。此函数仅在某些 UNIX 版本中可用。

**kill(pid, sig)**

向进程 `pid` 发送信号 `sig`。可以在 `signal` 模块中找到信号名称列表（UNIX）。

**killpg(pgid, sig)**

向进程组 `pgid` 发送信号 `sig`。可以在 `signal` 模块中找到信号名称列表（UNIX）。

**nice(increment)**

为进程的调度优先级（“nice 值”）增加一个增量。返回新的 nice 值。通常，用户只能降低进程的优先级，因为提高优先级需要 root 权限。更改优先级的效果取决于系统，但降低优先级通常用于使进程在后台运行，而不显著影响其他进程的性能（UNIX）。

**plock(op)**

将程序段锁定在内存中，防止它们被交换出去。`op` 的值是一个整数，决定锁定哪些段。`op` 的值是平台特定的，但通常是 `UNLOCK`、`PROCLOCK`、`TXTLOCK` 或 `DATLOCK` 之一。这些常量不是由 Python 定义的，但可能在 `<sys/lock.h>` 头文件中找到。此函数并非在所有平台上都可用，并且通常只能由有效用户 ID 为 0（root）的进程执行（UNIX）。

**popen(command [, mode [, bufsize]])**

打开一个到或来自命令的管道。返回值是一个连接到管道的已打开文件对象，可以根据 `mode` 是 `'r'`（默认）还是 `'w'` 来读取或写入。`bufsize` 的含义与内置 `open()` 函数中的相同。命令的退出状态由返回的文件对象的 `close()` 方法返回，但当退出状态为零时，返回 `None`。

**spawnv(mode, path, args)**

在新进程中执行程序 `path`，将 `args` 中指定的参数作为命令行参数传递。`args` 可以是列表或元组。`args` 的第一个元素应该是程序的名称。`mode` 是以下常量之一：

| 常量 | 描述 |
|----------|-------------|
| P_WAIT | 执行程序并等待其终止。返回程序的退出代码。 |
| P_NOWAIT | 执行程序并返回进程句柄。 |
| P_NOWAITO | 与 P_NOWAIT 相同。 |
| P_OVERLAY | 执行程序并销毁调用进程（与 exec 函数相同）。 |
| P_DETACH | 执行程序并与之分离。调用程序继续运行，但无法等待生成的进程。 |

`spawnv()` 在 Windows 和某些 UNIX 版本上可用。

**spawnve(mode, path, args, env)**

在新进程中执行程序 `path`，将 `args` 中指定的参数作为命令行参数传递，并将映射 `env` 的内容作为环境。`args` 可以是列表或元组。`mode` 的含义与 `spawnv()` 中描述的相同。

**spawnl(mode, path, arg1, ..., argn)**

与 `spawnv()` 相同，只是所有参数都作为额外参数提供。

**spawnle(mode, path, arg1, ..., argn, env)**

与 `spawnve()` 相同，只是参数作为参数提供。最后一个参数是包含环境变量的映射。

**spawnlp(mode, file, arg1, ..., argn)**

与 `spawnl()` 相同，但使用 PATH 环境变量的设置查找 `file`（UNIX）。

**spawnlpe(mode, file, arg1, ..., argn, env)**

与 `spawnle()` 相同，但使用 PATH 环境变量的设置查找 `file`（UNIX）。

**spawnvp(mode, file, args)**

与 `spawnv()` 相同，但使用 PATH 环境变量的设置查找 `file`（UNIX）。

**spawnvpe(mode, file, args, env)**

与 `spawnve()` 相同，但使用 PATH 环境变量的设置查找 `file`（UNIX）。

**startfile(path [, operation])**

启动与文件 `path` 关联的应用程序。这执行与在 Windows 资源管理器中双击文件相同的操作。该函数在应用程序启动后立即返回。此外，无法等待完成或从应用程序获取退出代码。`path` 是相对于当前目录的。`operation` 是一个可选字符串，指定打开 `path` 时要执行的操作。默认情况下，设置为 `'open'`，但可以设置为 `'print'`、`'edit'`、`'explore'` 或 `'find'`（确切列表取决于 `path` 的类型）（Windows）。

**system(command)**

在子 shell 中执行 `command`（一个字符串）。在 UNIX 上，返回值是 `wait()` 返回的进程退出状态。在 Windows 上，退出代码始终为 0。`subprocess` 模块提供了更强大的功能，是启动子进程的首选方式。



###### times()

返回一个由五个浮点数组成的元组，表示以秒为单位累计的时间。在 UNIX 系统上，元组按顺序包含用户时间、系统时间、子进程的用户时间、子进程的系统时间以及实际经过的实时。在 Windows 系统上，元组包含用户时间、系统时间，其余三个值为零。

###### wait([pid])

等待子进程完成，并返回一个包含其进程 ID 和退出状态的元组。退出状态是一个 16 位数字，其低字节是终止进程的信号编号，高字节是退出状态（如果信号编号为零）。如果产生了核心转储文件，则低字节的最高位被置位。如果提供了 pid，则指定要等待的进程。如果省略，wait() 会在任何子进程退出时返回（UNIX）。

###### waitpid(pid, options)

等待由进程 ID pid 指定的子进程状态发生变化，并返回一个包含其进程 ID 和退出状态指示的元组，编码方式与 wait() 相同。options 在正常操作时应为 0，或者使用 WNOHANG 以避免在没有子进程状态立即可用时挂起。此函数也可用于收集仅因某些原因停止执行的子进程的信息。将 options 设置为 WCONTINUED 会在子进程通过作业控制停止后恢复运行时收集信息。将 options 设置为 WUNTRACED 会收集已停止但尚未报告状态信息的子进程的信息。

###### wait3([options])

与 waitpid() 相同，不同之处在于该函数等待任何子进程的状态变化。返回一个三元组 (pid, status, rusage)，其中 pid 是子进程 ID，status 是退出状态码，rusage 包含 resource.getrusage() 返回的资源使用信息。options 参数与 waitpid() 具有相同的含义。

###### wait4(pid, options)

与 waitpid() 相同，不同之处在于返回结果是与 wait3() 返回的相同元组。

以下函数接受由 waitpid()、wait3() 或 wait4() 返回的进程状态码，用于检查进程的状态（UNIX）。

###### WCOREDUMP(status)

如果进程产生了核心转储，则返回 True。

###### WIFEXITED(status)

如果进程使用 exit() 系统调用退出，则返回 True。

###### WEXITSTATUS(status)

如果 WIFEXITED(status) 为 true，则返回传递给 exit() 系统调用的整数参数。否则，返回值无意义。

###### WIFCONTINUED(status)

如果进程已从作业控制停止状态恢复，则返回 True。

###### WIFSIGNALED(status)

如果进程因信号而退出，则返回 True。

###### WIFSTOPPED(status)

如果进程已停止，则返回 True。

###### WSTOPSIG(status)

返回导致进程停止的信号。

###### WTERMSIG(status)

返回导致进程退出的信号。

##### 系统配置

以下函数用于获取系统配置信息：

###### confstr(name)

返回一个字符串值的系统配置变量。name 是一个指定变量名称的字符串。可接受的名称因平台而异，但主机系统已知名称的字典可在 os.confstr_names 中找到。如果指定名称的配置值未定义，则返回空字符串。如果名称未知，则引发 ValueError。如果主机系统不支持该配置名称，也可能引发 OSError。此函数返回的参数大多与主机机器上的构建环境相关，包括系统实用程序的路径、各种程序配置（例如，32 位、64 位和大文件支持）的编译器选项以及链接器选项（UNIX）。

###### getloadavg()

返回一个三元组，包含过去 1、5 和 15 分钟内系统运行队列中项目的平均数量（UNIX）。

###### sysconf(name)

返回一个整数值的系统配置变量。name 是一个指定变量名称的字符串。主机系统上定义的名称可在字典 os.sysconf_names 中找到。如果配置名称已知但值未定义，则返回 -1。否则，可能引发 ValueError 或 OSError。某些系统可能定义了超过 100 个不同的系统参数。但是，下表详细说明了 POSIX.1 定义的参数，这些参数应在大多数 UNIX 系统上可用：

| 参数 | 描述 |
|-----------|-------------|
| "SC_ARG_MAX" | 可与 exec() 一起使用的参数的最大长度。 |
| "SC_CHILD_MAX" | 每个用户 ID 的最大进程数。 |
| "SC_CLK_TCK" | 每秒的时钟节拍数。 |
| "SC_NGROUPS_MAX" | 同时补充组 ID 的最大数量。 |
| "SC_STREAM_MAX" | 进程一次可以打开的最大流数量。 |
| "SC_TZNAME_MAX" | 时区名称的最大字节数。 |
| "SC_OPEN_MAX" | 进程一次可以打开的最大文件数。 |
| "SC_JOB_CONTROL" | 系统支持作业控制。 |
| "SC_SAVED_IDS" | 指示每个进程是否有保存的 set-user-ID 和保存的 set-group-ID。 |

###### urandom(n)

返回一个包含系统生成的 *n* 个随机字节的字符串（例如，UNIX 上的 /dev/urandom）。返回的字节适用于密码学。

##### 异常

os 模块定义了一个用于指示错误的单一异常。

###### error

当函数返回系统相关错误时引发的异常。这与内置异常 `OSError` 相同。该异常携带两个值：`errno` 和 `strerror`。第一个包含如 `errno` 模块所述的整数错误值。后者包含一个字符串错误消息。对于涉及文件系统的异常，该异常还包含第三个属性 `filename`，即传递给函数的文件名。

#### os.path

os.path 模块用于以可移植的方式操作路径名。它由 os 模块导入。

##### abspath(path)

返回路径名 *path* 的绝对版本，考虑当前工作目录。例如，`abspath('../Python/foo')` 可能返回 `'/home/beazley/Python/foo'`。

##### basename(path)

返回路径名 *path* 的基本名称。例如，`basename('/usr/local/python')` 返回 `'python'`。

##### commonprefix(list)

返回作为 *list* 中所有字符串前缀的最长字符串。如果 *list* 为空，则返回空字符串。

##### dirname(path)

返回路径名 *path* 的目录名。例如，`dirname('/usr/local/python')` 返回 `'/usr/local'`。

##### exists(path)

如果 *path* 引用存在的路径，则返回 `True`。如果 *path* 引用损坏的符号链接，则返回 `False`。

##### expanduser(path)

将形如 `'~user'` 的路径名替换为用户的主目录。如果扩展失败或 `path` 不以 `'~'` 开头，则路径将原样返回。

##### expandvars(path)

展开 `path` 中形如 `'$name'` 或 `'${name}'` 的环境变量。格式错误或不存在的变量名称将保持不变。

##### getatime(path)

返回上次访问的时间，表示为自纪元以来的秒数（参见 `time` 模块）。如果 `os.stat_float_times()` 返回 True，则返回值可以是浮点数。

##### getctime(path)

在 UNIX 上返回上次修改的时间，在 Windows 上返回创建时间。时间以自纪元以来的秒数返回（参见 `time` 模块）。在某些情况下，返回值可以是浮点数（参见 `getatime()`）。

##### getmtime(path)

返回上次修改的时间，表示为自纪元以来的秒数（参见 `time` 模块）。在某些情况下，返回值可以是浮点数（参见 `getatime()`）。

##### getsize(path)

返回文件大小（以字节为单位）。

##### isabs(path)

如果 `path` 是绝对路径名（以斜杠开头），则返回 True。

##### isfile(path)

如果 `path` 是常规文件，则返回 True。此函数遵循符号链接，因此对于同一个路径，`islink()` 和 `isfile()` 都可以为真。

##### isdir(path)

如果 `path` 是目录，则返回 True。遵循符号链接。

##### islink(path)

如果 `path` 引用符号链接，则返回 True。如果不支持符号链接，则返回 False。

##### ismount(path)

如果 `path` 是挂载点，则返回 True。

##### join(path1 [, path2 [, ...]])

智能地将一个或多个路径组件连接成一个路径名。例如，`join('home', 'beazley', 'Python')` 返回 `'home/beazley/Python'`。

##### lexists(path)

如果 `path` 存在，则返回 True。对于所有符号链接都返回 True，即使链接已损坏。



# 398 第19章 操作系统服务

#### os.path

**normcase(path)**

规范化路径名的大小写。在大小写不敏感的文件系统上，此函数会将 *path* 转换为小写。在 Windows 上，正斜杠也会被转换为反斜杠。

**normpath(path)**

规范化路径名。此函数会合并冗余的分隔符和上级目录引用，使得 'A//B'、'A/./B' 和 'A/foo/../B' 都变为 'A/B'。在 Windows 上，正斜杠会被转换为反斜杠。

**realpath(path)**

返回 *path* 的真实路径，消除任何符号链接（UNIX）。

**relpath(path [, start])**

返回从当前工作目录到 *path* 的相对路径。可以提供 *start* 参数以指定不同的起始目录。

**samefile(path1, path2)**

如果 *path1* 和 *path2* 指向同一个文件或目录，则返回 True（UNIX）。

**sameopenfile(fp1, fp2)**

如果已打开的文件对象 *fp1* 和 *fp2* 指向同一个文件，则返回 True（UNIX）。

**samestat(stat1, stat2)**

如果 fstat()、lstat() 或 stat() 返回的 stat 元组 *stat1* 和 *stat2* 指向同一个文件，则返回 True（UNIX）。

**split(path)**

将 *path* 分割成一对 (*head*, *tail*)，其中 *tail* 是路径的最后一个组件，*head* 是其前面的所有内容。例如，'/home/user/foo' 会被分割成 ('/home/user', 'foo')。此元组与 (dirname(), basename()) 返回的结果相同。

**splitdrive(path)**

将 *path* 分割成一对 (*drive*, *filename*)，其中 *drive* 是盘符规范或空字符串。在没有盘符规范的机器上，*drive* 始终为空字符串。

**splitext(path)**

将路径名分割成基本文件名和后缀。例如，splitext('foo.txt') 返回 ('foo', '.txt')。

**splitunc(path)**

将路径名分割成一对 (*unc*, *rest*)，其中 *unc* 是 UNC（通用命名约定）挂载点，*rest* 是路径的其余部分（Windows）。

**supports_unicode_filenames**

如果文件系统允许 Unicode 文件名，则此变量设置为 True。

> 在 Windows 上，处理包含盘符的文件名（例如 `'C:spam.txt'`）时需要格外小心。在大多数情况下，文件名被解释为相对于当前工作目录。例如，如果当前目录是 `'C:\Foo\'`，那么文件 `'C:spam.txt'` 会被解释为文件 `'C:\Foo\C:spam.txt'`，而不是文件 `'C:\spam.txt'`。

另请参阅：
- `fnmatch`（第 316 页）
- `glob`（第 317 页）
- `os`（第 378 页）

#### signal

`signal` 模块用于在 Python 中编写信号处理程序。信号通常对应于异步事件，这些事件因计时器到期、传入数据到达或用户执行的某些操作而发送到程序。该模块的信号接口模仿了 UNIX 的接口，尽管该模块的部分功能在其他平台上也受到支持。

##### alarm(time)

如果 time 不为零，则计划在 time 秒后向程序发送一个 `SIGALRM` 信号。任何先前计划的警报都将被取消。如果 time 为零，则不计划任何警报，并且任何先前设置的警报都将被取消。返回之前任何计划警报剩余的秒数，如果没有计划警报，则返回零（UNIX）。

##### getsignal(signalnum)

返回信号 `signalnum` 的信号处理程序。返回的对象是一个可调用的 Python 对象。该函数也可能返回 `SIG_IGN`（对于被忽略的信号）、`SIG_DFL`（对于默认信号处理程序），或者如果信号处理程序不是从 Python 解释器安装的，则返回 None。

##### getitimer(which)

返回由 which 标识的内部计时器的当前值。

##### pause()

进入休眠状态，直到接收到下一个信号（UNIX）。

##### set_wakeup_fd(fd)

设置一个文件描述符 `fd`，当接收到信号时，将在其上写入一个 `'\0'` 字节。这反过来可用于在使用 `select` 模块中的函数等轮询文件描述符的程序中处理信号。为使此功能工作，`fd` 描述的文件必须以非阻塞模式打开。

##### setitimer(which, seconds [, interval])

设置一个内部计时器，在 seconds 秒后生成一个信号，并在此后每隔 interval 秒重复生成。这两个参数均指定为浮点数。`which` 参数是 `ITIMER_REAL`、`ITIMER_VIRTUAL` 或 `ITIMER_PROF` 之一。`which` 的选择决定了计时器到期后生成哪个信号。对于 `ITIMER_REAL` 生成 `SIGALRM`，对于 `ITIMER_VIRTUAL` 生成 `SIGVTALRM`，对于 `ITIMER_PROF` 生成 `SIGPROF`。将 seconds 设置为 0 以清除计时器。返回一个元组 `(seconds, interval)`，其中包含计时器的先前设置。

##### siginterrupt(signalnum, flag)

设置给定信号编号的系统调用重启行为。如果 `flag` 为 `False`，被信号 *signalnum* 中断的系统调用将自动重启。如果设置为 `True`，系统调用将被中断。被中断的系统调用通常会导致 `OSError` 或 `IOError` 异常，其中关联的错误号设置为 `errno.EINTR` 或 `errno.EAGAIN`。

##### signal(signalnum, handler)

为信号 *signalnum* 设置信号处理程序为函数 *handler*。*handler* 必须是一个接受两个参数的可调用 Python 对象：信号编号和帧对象。也可以分别传入 `SIG_IGN` 或 `SIG_DFL` 来忽略信号或使用默认信号处理程序。返回值是先前的信号处理程序、`SIG_IGN` 或 `SIG_DFL`。当线程启用时，此函数只能从主线程调用。否则，将引发 `ValueError` 异常。

各个信号使用形如 SIG\* 的符号常量标识。这些名称对应于特定于机器的整数值。典型值如下：

| 信号名称 | 描述 |
|-------------|-------------|
| SIGABRT | 异常终止 |
| SIGALRM | 警报 |
| SIGBUS | 总线错误 |
| SIGCHLD | 子进程状态改变 |
| SIGCLD | 子进程状态改变 |
| SIGCONT | 继续 |
| SIGFPE | 浮点错误 |
| SIGHUP | 挂起 |
| SIGILL | 非法指令 |
| SIGINT | 终端中断字符 |
| SIGIO | 异步 I/O |
| SIGIOT | 硬件故障 |
| SIGKILL | 终止 |
| SIGPIPE | 写入管道，无读取者 |
| SIGPOLL | 可轮询事件 |
| SIGPROF | 性能分析警报 |
| SIGPWR | 电源故障 |
| SIGQUIT | 终端退出字符 |
| SIGSEGV | 段错误 |
| SIGSTOP | 停止 |
| SIGTERM | 终止 |
| SIGTRAP | 硬件故障 |
| SIGTSTP | 终端停止字符 |
| SIGTTIN | 控制 TTY |
| SIGTTOU | 控制 TTY |
| SIGURG | 紧急情况 |
| SIGUSR1 | 用户定义 |
| SIGUSR2 | 用户定义 |
| SIGVTALRM | 虚拟时间警报 |
| SIGWINCH | 窗口大小改变 |
| SIGXCPU | CPU 限制超出 |
| SIGXFSZ | 文件大小限制超出 |

此外，该模块还定义了以下变量：

| 变量 | 描述 |
|----------|-------------|
| SIG_DFL | 调用默认信号处理程序的信号处理程序 |
| SIG_IGN | 忽略信号的信号处理程序 |
| NSIG | 最高信号编号加一 |

##### 示例

以下示例说明了在建立网络连接时设置超时（socket 模块已经提供了超时选项，因此此示例仅用于说明使用信号模块的基本概念）。

```python
import signal, socket
def handler(signum, frame):
    print 'Timeout!'
    raise IOError, 'Host not responding.'
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
signal.signal(signal.SIGALRM, handler)
signal.alarm(5)                  # 5-second alarm
sock.connect('www.python.org', 80) # Connect
signal.alarm(0)                    # Clear alarm
```

##### 注意事项

-   信号处理程序会保持安装状态，直到显式重置，SIGCHLD 除外（其行为特定于实现）。
-   无法临时禁用信号。
-   信号仅在 Python 解释器的原子指令之间处理。用 C 编写的长时间运行的计算（例如扩展模块中执行的计算）可能会延迟信号的交付。
-   如果在 I/O 操作期间发生信号，I/O 操作可能会因异常而失败。在这种情况下，errno 值被设置为 errno.EINTR，以指示系统调用被中断。
-   某些信号（如 SIGSEGV）无法从 Python 中处理。
-   Python 默认安装少量的信号处理程序。SIGPIPE 被忽略，SIGINT 被转换为 KeyboardInterrupt 异常，SIGTERM 被捕获以执行清理并调用 sys.exitfunc。



#### subprocess

`subprocess` 模块包含用于创建新进程、控制输入输出流以及处理返回码等通用任务的函数和对象。该模块集中了原先分散在 `os`、`popen2` 和 `commands` 等其他模块中的功能。

**Popen(args, \*\*parms)**

将命令作为子进程执行，并返回一个表示新进程的 `Popen` 对象。`args` 中的命令可以是字符串（如 `'ls -l'`），也可以是字符串列表（如 `['ls', '-l']`）。`parms` 表示一组可用于控制子进程各种属性的关键字参数。支持以下关键字参数：

| 关键字 | 描述 |
| --- | --- |
| bufsize | 指定缓冲行为：0 表示无缓冲，1 表示按行缓冲，负值使用系统默认值，其他正值指定大约的缓冲区大小。默认值为 0。 |
| close_fds | 若为 `True`，在执行子进程之前关闭除 0、1 和 2 之外的所有文件描述符。默认值为 `False`。 |
| creation_flags | 在 Windows 上指定进程创建标志。目前唯一可用的标志是 `CREATE_NEW_CONSOLE`。默认值为 0。 |
| cwd | 命令执行所在的目录。执行前会将子进程的当前目录更改为 `cwd`。默认值为 `None`，即使用父进程的当前目录。 |
| env | 新进程的环境变量字典。默认值为 `None`，即使用父进程的环境变量。 |
| executable | 指定要使用的可执行程序名称。由于程序名称已包含在 `args` 中，因此很少需要设置此参数。如果指定了 `shell`，此参数则用于指定要使用的 shell 名称。默认值为 `None`。 |
| preexec_fn | 指定一个函数，该函数将在子进程中命令执行前被调用。该函数不应接受任何参数。 |
| shell | 若为 `True`，则像 `os.system()` 函数一样通过 UNIX shell 执行命令。默认 shell 为 `/bin/sh`，但可通过设置 `executable` 来更改。`shell` 的默认值为 `None`。 |
| startupinfo | 提供在 Windows 上创建进程时使用的启动标志。默认值为 `None`。可选值包括 `STARTF_USESHOWWINDOW` 和 `STARTF_USESTDHANDLES`。 |
| stderr | 表示子进程中用于 stderr 的文件对象。可以是通过 `open()` 创建的文件对象、整数文件描述符，或特殊值 `PIPE`（表示应创建新管道）。默认值为 `None`。 |
| stdin | 表示子进程中用于 stdin 的文件对象。可设置的值与 `stderr` 相同。默认值为 `None`。 |
| stdout | 表示子进程中用于 stdout 的文件对象。可设置的值与 `stderr` 相同。默认值为 `None`。 |
| universal_newlines | 若为 `True`，表示 `stdin`、`stdout` 和 `stderr` 的文件将以文本模式打开，并启用通用换行符模式。完整描述请参阅 `open()` 函数。 |

##### call(args, \*\*parms)

此函数与 `Popen()` 完全相同，区别在于它只执行命令并返回其状态码（即不返回 `Popen` 对象）。如果你只想执行命令而不关心捕获输出或以其他方式控制进程，此函数非常有用。参数含义与 `Popen()` 相同。

##### check_call(args, \*\*parms)

与 `call()` 相同，不同之处在于如果退出码非零，将抛出 `CalledProcessError` 异常。该异常在其 `returncode` 属性中存储了退出码。

`Popen()` 返回的 `Popen` 对象 `p` 具有多种可用于与子进程交互的方法和属性。

##### p.communicate([input])

通过将 `input` 中提供的数据发送到进程的标准输入来与子进程通信。数据发送后，该方法等待进程终止，同时收集标准输出和标准错误上接收到的输出。返回一个元组 `(stdout, stderr)`，其中 `stdout` 和 `stderr` 为字符串。如果未向子进程发送数据，则 `input` 设置为 `None`（默认值）。

##### p.kill()

通过向子进程发送 `SIGKILL` 信号（UNIX）或调用 `p.terminate()` 方法（Windows）来终止子进程。

##### p.poll()

检查 `p` 是否已终止。如果是，则返回子进程的返回码。否则返回 `None`。

##### p.send_signal(signal)

向子进程发送信号。`signal` 是 `signal` 模块中定义的信号编号。在 Windows 上，唯一支持的信号是 `SIGTERM`。

##### p.terminate()

通过向子进程发送 `SIGTERM` 信号（UNIX）或调用 Win32 API 的 `TerminateProcess` 函数（Windows）来终止子进程。

##### p.wait()

等待 `p` 终止并返回返回码。

##### p.pid

子进程的进程 ID。

##### p.returncode

进程的数字返回码。如果为 `None`，表示进程尚未终止。如果为负数，表示进程被信号终止（UNIX）。

##### p.stdin, p.stdout, p.stderr

当相应的 I/O 流以管道方式打开时（例如，将 `Popen()` 中的 `stdout` 参数设置为 `PIPE`），这三个属性将被设置为已打开的文件对象。这些文件对象用于将管道连接到其他子进程。如果未使用管道，这些属性将设置为 `None`。

##### 示例

```python
###### 执行基本系统命令。类似于 os.system()
ret = subprocess.call("ls -l", shell=True)

###### 静默执行基本系统命令
ret = subprocess.call("rm -f *.java",shell=True,
                    stdout=open("/dev/null"))

###### 执行系统命令，但捕获输出
p = subprocess.Popen("ls -l", shell=True, stdout=subprocess.PIPE)
out = p.stdout.read()

###### 执行命令，但发送输入并接收输出
p = subprocess.Popen("wc", shell=True, stdin=subprocess.PIPE,
                    stdout=subprocess.PIPE, stderr=subprocess.PIPE)
out, err = p.communicate(s)    # 向进程发送字符串 s

###### 创建两个子进程并通过管道连接
p1 = subprocess.Popen("ls -l", shell=True, stdout=subprocess.PIPE)
p2 = subprocess.Popen("wc",shell=True, stdin=p1.stdout,
                    stdout=subprocess.PIPE)
out = p2.stdout.read()
```

##### 注意事项

-   一般来说，最好以字符串列表的形式提供命令行，而不是使用单个字符串和 shell 命令（例如，使用 `['wc','filename']` 而不是 `'wc filename'`）。在许多系统上，文件名通常包含特殊字符和空格（例如 Windows 上的"Documents and Settings"文件夹）。如果你坚持以列表形式提供命令参数，一切都会正常运行。如果尝试构造 shell 命令，则需要采取额外步骤确保特殊字符和空格被正确转义。
-   在 Windows 上，管道以二进制文件模式打开。因此，如果从子进程读取文本输出，行尾将包含额外的回车符（`'\r\n'` 而非 `'\n'`）。如果需要解决此问题，请为 `Popen()` 提供 `universal_newlines` 选项。
-   `subprocess` 模块不能用于控制期望在终端或 TTY 中运行的进程。最常见的例子是任何需要用户输入密码的程序（如 ssh、ftp、svn 等）。要控制这些程序，请查找基于流行的"Expect"UNIX 工具的第三方模块。

#### time

`time` 模块提供各种与时间相关的函数。在 Python 中，时间以自纪元以来的秒数来衡量。纪元是时间的起点（时间 = 0 秒的时刻）。在 UNIX 上，纪元是 1970 年 1 月 1 日，在其他系统上可通过调用 `time.gmtime(0)` 来确定。

定义了以下变量：

##### accept2dyear

一个布尔值，表示是否接受两位数年份。通常为 `True`，但如果环境变量 `$PYTHON2K` 被设置为非空字符串，则会设置为 `False`。该值也可以手动更改。

##### altzone

夏令时（DST）期间使用的时区（如适用）。

##### daylight

如果已定义夏令时时区，则设置为非零值。

##### timezone

本地（非夏令时）时区。

##### tzname

一个包含本地时区名称和本地夏令时时区名称（如果已定义）的元组。

可以使用以下函数：

##### asctime([tuple])

将 `gmtime()` 或 `localtime()` 返回的时间元组转换为格式为 `'Mon Jul 12 14:45:23 1999'` 的字符串。如果未提供参数，则使用当前时间。

##### clock()

以浮点数形式返回当前 CPU 时间（秒）。

##### ctime([secs])

将自纪元以来以秒数表示的时间转换为代表本地时间的字符串。`ctime(secs)` 等同于 `asctime(localtime(secs))`。如果省略 `secs` 或为 `None`，则使用当前时间。



###### gmtime([secs])

将自纪元（epoch）以来以秒数表示的时间转换为 UTC（协调世界时，又称格林尼治标准时间）时间。该函数返回一个 `struct_time` 对象，该对象具有以下属性：

| 属性 | 值 |
|------|-----|
| tm_year | 一个四位数的值，如 1998 |
| tm_mon | 1-12 |
| tm_mday | 1-31 |
| tm_hour | 0-23 |
| tm_min | 0-59 |
| tm_sec | 0-61 |
| tm_wday | 0-6（0=星期一） |
| tm_yday | 1-366 |
| tm_isdst | -1, 0, 1 |

如果正在实行夏令时（DST），则 `tm_isdst` 属性为 1；如果未实行，则为 0；如果没有相关信息，则为 -1。如果省略 `secs` 或 `secs` 为 `None`，则使用当前时间。为向后兼容，返回的 `struct_time` 对象也表现得像一个 9 元组，按所列顺序包含上述属性值。

###### localtime([secs])

返回与 `gmtime()` 类似的 `struct_time` 对象，但对应于本地时区。如果省略 `secs` 或 `secs` 为 `None`，则使用当前时间。

###### mktime(tuple)

该函数接受一个 `struct_time` 对象或元组，表示本地时区中的一个时间（格式与 `localtime()` 返回的相同），并返回一个浮点数，表示自纪元以来的秒数。如果输入值不是有效时间，则引发 `OverflowError` 异常。

###### sleep(secs)

使当前进程暂停（睡眠）`secs` 秒。`secs` 是一个浮点数。

##### strftime(format [, tm])

将 `struct_time` 对象 `tm` 表示的时间（由 `gmtime()` 或 `localtime()` 返回）转换为字符串（为向后兼容，`tm` 也可以是表示时间值的元组）。`format` 是一个格式字符串，其中可以嵌入以下格式代码：

| 指令 | 含义 |
|------|------|
| %a | 本地区域的星期缩写名称 |
| %A | 本地区域的完整星期名称 |
| %b | 本地区域的月份缩写名称 |
| %B | 本地区域的完整月份名称 |
| %c | 本地区域适当的日期和时间表示 |
| %d | 月份中的日期，以十进制数表示 [01-31] |
| %H | 小时（24 小时制），以十进制数表示 [00-23] |
| %I | 小时（12 小时制），以十进制数表示 [01-12] |
| %j | 一年中的第几天，以十进制数表示 [001-366] |
| %m | 月份，以十进制数表示 [01-12] |
| %M | 分钟，以十进制数表示 [00-59] |
| %p | 本地区域 AM 或 PM 的等价表示 |
| %S | 秒，以十进制数表示 [00-61] |
| %U | 一年中的周数 [00-53]（以星期日为每周第一天） |
| %w | 星期，以十进制数表示 [0-6]（0 = 星期日） |
| %W | 一年中的周数（以星期一为每周第一天） |
| %x | 本地区域适当的日期表示 |
| %X | 本地区域适当的时间表示 |
| %y | 不带世纪的年份，以十进制数表示 [00-99] |
| %Y | 带世纪的年份，以十进制数表示 |
| %Z | 时区名称（如果没有时区，则不显示字符） |
| %% | % 字符 |

格式代码可以像字符串的 `%` 运算符一样包含宽度和精度。如果元组字段中有任何值超出范围，则引发 `ValueError`。如果省略 *tuple*，则使用与当前时间对应的时间元组。

###### strptime(string [, format])

解析一个表示时间的字符串，并返回由 *localtime()* 或 *gmtime()* 返回的 *struct_time* 对象。*format* 参数使用与 *strftime()* 相同的说明符，默认值为 *'%a %b %d %H:%M:%S %Y'*。这与 *ctime()* 函数生成的格式相同。如果字符串无法解析，则引发 `ValueError` 异常。

##### time()

返回以 UTC（协调世界时）自纪元以来的秒数表示的当前时间。

##### tzset()

根据 UNIX 上 `TZ` 环境变量的值重置时区设置。例如：

```
os.environ['TZ'] = 'US/Mountain'
time.tzset()

os.environ['TZ'] = "CST+06CDT,M4.1.0,M10.5.0"
time.tzset()
```

###### 备注

- 当接受两位年份时，它们会根据 POSIX X/Open 标准转换为四位年份，其中 69-99 映射到 1969-1999，0-68 映射到 2000-2068。
- 时间函数的精度通常远低于时间单位所暗示的精度。例如，操作系统可能每秒仅更新时间 50-100 次。

另请参阅：

- datetime (p. 336)

#### winreg

`winreg` 模块（Python 2 中为 `_winreg`）提供了对 Windows 注册表的底层接口。注册表是一个大型层次树，其中每个节点称为一个键（key）。某个特定键的子节点称为子键（subkey），它们可能包含更多的子键或值。例如，Python 的 `sys.path` 变量设置通常按如下方式存储在注册表中：

```
HKEY_LOCAL_MACHINE\Software\Python\PythonCore\2.6\PythonPath
```

在这种情况下，`Software` 是 `HKEY_LOCAL_MACHINE` 的子键，`Python` 是 `Software` 的子键，依此类推。`PythonPath` 键的值包含实际的路径设置。

通过打开和关闭操作来访问键。打开的键由特殊句柄表示（这些句柄是对 Windows 通常使用的整数句柄标识符的封装）。

##### CloseKey(key)

关闭此前使用句柄 `key` 打开的注册表键。

##### ConnectRegistry(computer_name, key)

返回另一台计算机上预定义注册表键的句柄。`computer_name` 是远程计算机名称，格式为 `\\computername` 的字符串。如果 `computer_name` 为 `None`，则使用本地注册表。`key` 是预定义句柄，例如 `HKEY_CURRENT_USER` 或 `HKEY_USERS`。失败时引发 `EnvironmentError`。以下列表显示了 `_winreg` 模块中定义的所有 `HKEY_*` 值：

- HKEY_CLASSES_ROOT
- HKEY_CURRENT_CONFIG
- HKEY_CURRENT_USER
- HKEY_DYN_DATA
- HKEY_LOCAL_MACHINE
- HKEY_PERFORMANCE_DATA
- HKEY_USERS

##### CreateKey(key, sub_key)

创建或打开一个键并返回句柄。`key` 是此前已打开的键或由 `HKEY_*` 常量定义的预定义键。`sub_key` 是要打开或创建的键的名称。如果 `key` 是预定义键，则 `sub_key` 可以为 `None`，此时返回 `key`。

##### DeleteKey(key, sub_key)

删除 *sub_key*。*key* 是一个已打开的键或预定义的 `HKEY_*` 常量之一。*sub_key* 是标识要删除的键的字符串。*sub_key* 不能包含任何子键；否则将引发 `EnvironmentError`。

##### DeleteValue(key, value)

从注册表键中删除一个命名值。*key* 是一个已打开的键或预定义的 `HKEY_*` 常量之一。*value* 是一个字符串，包含要删除的值的名称。

##### EnumKey(key, index)

按索引返回子键的名称。*key* 是一个已打开的键或预定义的 `HKEY_*` 常量之一。*index* 是指定要检索键的整数。如果 *index* 超出范围，则引发 `EnvironmentError`。

##### EnumValue(key, index)

返回一个打开键的值。*key* 是一个已打开的键或预定义的 `HKEY_*` 常量。*index* 是指定要检索值的整数。该函数返回一个元组 `(name, data, type)`，其中 `name` 是值名称，`data` 是保存值数据的对象，`type` 是指定值数据类型的整数。目前已定义以下类型代码：

| 代码 | 描述 |
|------|------|
| REG_BINARY | 二进制数据 |
| REG_DWORD | 32 位数字 |
| REG_DWORD_LITTLE_ENDIAN | 32 位小端序数字 |
| REG_DWORD_BIG_ENDIAN | 大端序格式的 32 位数字 |
| REG_EXPAND_SZ | 以空字符结尾的字符串，包含未展开的环境变量引用 |
| REG_LINK | Unicode 符号链接 |
| REG_MULTI_SZ | 以空字符结尾的字符串序列 |
| REG_NONE | 未定义的值类型 |
| REG_RESOURCE_LIST | 设备驱动程序资源列表 |
| REG_SZ | 以空字符结尾的字符串 |

##### ExpandEnvironmentStrings(s)

在 Unicode 字符串 *s* 中展开形式为 `%name%` 的环境字符串。

##### FlushKey(key)

将 *key* 的属性写入注册表，强制将更改保存到磁盘。只有在应用程序需要绝对确定注册表数据已存储到磁盘时，才应调用此函数。在数据写入之前，该函数不会返回。在正常情况下，无需使用此函数。

##### RegLoadKey(key, sub_key, filename)

创建一个子键，并将文件中的注册信息存储到该子键中。*key* 是一个已打开的键或预定义的 `HKEY_*` 常量。*sub_key* 是标识要加载子键的字符串。*filename* 是要从中加载数据的文件名称。该文件的内容必须



```
可以使用 `SaveKey()` 函数创建，并且调用进程必须具有 `SE_RESTORE_PRIVILEGE` 才能生效。如果 *key* 是由 `ConnectRegistry()` 返回的，那么 *filename* 应该是相对于远程计算机的路径。

`OpenKey(key, sub_key[, res [, sam]])`

打开一个注册表项。*key* 是一个已打开的键或一个 `HKEY_*` 常量。*sub_key* 是一个标识要打开的子项的字符串。*res* 是一个保留整数，必须为零（默认值）。*sam* 是一个整数，用于定义该键的安全访问掩码。默认值是 `KEY_READ`。以下是 *sam* 的其他可能值：

- `KEY_ALL_ACCESS`
- `KEY_CREATE_LINK`
- `KEY_CREATE_SUB_KEY`
- `KEY_ENUMERATE_SUB_KEYS`
- `KEY_EXECUTE`
- `KEY_NOTIFY`
- `KEY_QUERY_VALUE`
- `KEY_READ`
- `KEY_SET_VALUE`
- `KEY_WRITE`

##### OpenKeyEx()

与 `OpenKey()` 相同。

##### QueryInfoKey(*key*)

返回关于一个注册表项的信息，格式为一个元组 `(`*num_subkeys*, *num_values*, *last_modified*`)`，其中 *num_subkeys* 是子项的数量，*num_values* 是值的数量，*last_modified* 是一个长整数，包含最后修改的时间。时间从 1601 年 1 月 1 日开始计算，以 100 纳秒为单位。

##### QueryValue(*key*, *sub_key*)

以字符串形式返回一个注册表项的无名值。*key* 是一个已打开的键或一个 `HKEY_*` 常量。*sub_key* 是要使用的子项的名称（可选）。如果省略，则函数返回与 *key* 关联的值。此函数返回第一个具有空名称的值的数据。但是，不返回类型（请改用 `QueryValueEx`）。

##### QueryValueEx(*key*, *value_name*)

返回一个元组 `(`*value*, *type*`)`，其中包含一个注册表项的数据值和类型。*key* 是一个已打开的键或 `HKEY_*` 常量。*value_name* 是要返回的值的名称。返回的类型是 `EnumValue()` 函数描述中所述的整数代码之一。

##### SaveKey(*key*, *filename*)

将 *key* 及其所有子项保存到文件中。*key* 是一个已打开的键或一个预定义的 `HKEY_*` 常量。*filename* 必须不存在且不应包含文件扩展名。此外，调用者必须拥有备份权限才能成功执行此操作。

```
SetValue(key, sub_key, type, value)
```

设置一个注册表项的值。*key* 是一个已打开的键或 `HKEY_*` 常量。*sub_key* 是要与该值关联的子项的名称。*type* 是一个整数类型码，目前仅限于 `REG_SZ`。*value* 是一个包含值数据的字符串。如果 *sub_key* 不存在，则会被创建。要使此函数成功，*key* 必须已使用 `KEY_SET_VALUE` 访问权限打开。

```
SetValueEx(key, value_name, reserved, type, value)
```

设置一个注册表项的值字段。*key* 是一个已打开的键或一个 `HKEY_*` 常量。*value_name* 是值的名称。*type* 是一个整数类型码，如 `EnumValue()` 函数中所述。*value* 是一个包含新值的字符串。当设置数字类型（例如 `REG_DWORD`）的值时，*value* 仍然是一个包含原始数据的字符串。此字符串可以使用 `struct` 模块创建。*reserved* 目前被忽略，可以设置为任何值（其值不被使用）。

##### 注意事项

- 返回 Windows HKEY 对象的函数会返回一个由 `PyHKEY` 类描述的特殊注册表句柄对象。此对象可以使用 `int()` 转换为 Windows 句柄值。此对象还可以与上下文管理协议一起使用，以自动关闭底层句柄——例如：

```
with winreg.OpenKey(winreg.HKEY_LOCAL_MACHINE, "spam") as key:
    statements
```

### 20 线程与并发

本章描述了用于在 Python 中编写并发程序的库模块和编程策略。主题包括线程、消息传递、多进程和协程。在介绍具体的库模块之前，首先描述一些基本概念。

#### 基本概念

一个正在运行的程序称为一个*进程*。每个进程都有自己系统状态，包括内存、打开的文件列表、一个用于跟踪正在执行的指令的程序计数器，以及一个用于保存函数局部变量的调用栈。通常，进程按单个控制流顺序执行语句，这有时称为进程的*主线程*。在任何给定时间，程序只做一件事。

程序可以使用库函数（例如 `os` 或 `subprocess` 模块中的函数，如 `os.fork()`、`subprocess.Popen()` 等）创建新进程。然而，这些称为*子进程*的进程作为完全独立的实体运行——每个子进程都有自己私有的系统状态和主执行线程。因为子进程是独立的，所以它与原始进程并发执行。也就是说，创建子进程的进程可以继续处理其他事情，而子进程在后台执行自己的工作。

尽管进程是隔离的，但它们可以相互通信——这称为*进程间通信 (IPC)*。最常见的 IPC 形式之一基于*消息传递*。*消息*只是原始字节的缓冲区。然后使用 `send()` 和 `recv()` 等原始操作通过 I/O 通道（如管道或网络套接字）传输或接收消息。另一种不太常见的 IPC 机制依赖于内存映射区域（参见 `mmap` 模块）。通过内存映射，进程可以创建共享的内存区域。对这些区域的修改随后会在所有碰巧正在查看它们的进程中可见。

如果应用程序想要同时处理多个任务，则可以使用多个进程——每个进程负责部分处理。然而，另一种将工作细分为任务的方法是使用线程。*线程*类似于进程，因为它有自己的控制流和执行堆栈。但是，线程在创建它的进程内运行，共享所有数据和系统资源。当应用程序想要并发执行任务，但存在大量需要任务共享的系统状态时，线程非常有用。

当使用多个进程或线程时，宿主操作系统负责调度它们的工作。这是通过为每个进程（或线程）分配一个小的时间片，并在所有活动任务之间快速循环——为每个任务分配一部分可用的 CPU 周期来完成的。例如，如果你的系统有 10 个活动进程正在运行，操作系统将为每个进程分配大约 1/10 的 CPU 时间，并在进程之间快速轮转。在具有多个 CPU 核心的系统上，操作系统可以调度进程，使每个 CPU 保持繁忙，并行执行进程。

编写利用并发执行优势的程序本质上就是复杂的。复杂性的一个主要来源是同步和对共享数据的访问。特别是，多个任务尝试在大致相同的时间更新数据结构可能导致程序状态损坏和不一致（这个问题在正式称为*竞态条件*）。为了解决这些问题，并发程序必须识别代码的关键部分，并使用互斥锁和其他类似的同步原语来保护它们。例如，如果不同的线程试图同时将数据写入同一个文件，你可能会使用互斥锁来同步它们的操作，以便一旦其中一个线程开始写入，其他线程就必须等待它完成才能开始写入。这种场景的代码通常如下所示：

```
write_lock = Lock()
...
###### Critical section where writing occurs
write_lock.acquire()
f.write("Here's some data.\n")
f.write("Here's more data.\n")
...
write_lock.release()
```

有一个归功于 Jason Whittington 的笑话是这样的："为什么多线程的鸡要过马路？为了到达另一边。"这个笑话典型地说明了任务同步和并发编程中出现的问题。如果你挠着头说："我不明白，"那么在深入本章其余部分之前，再读一点东西可能是明智的。

#### 并发编程与 Python

Python 在大多数系统上都支持基于消息传递和线程的并发编程。尽管大多数程序员倾向于熟悉线程接口，但 Python 线程实际上相当受限。虽然具有最小的线程安全性，但 Python 解释器使用一个内部的全局解释器锁（GIL），只允许单个 Python 线程在任何给定时刻执行。这限制了 Python 程序只能在单个处理器上运行，无论系统上可能有多少个 CPU 核心可用。尽管 GIL 在 Python 社区中经常是激烈争论的源头，但在可预见的未来它不太可能被移除。

GIL 的存在直接影响了许多 Python 程序员解决并发编程问题的方式。如果应用程序主要是 I/O 密集型的，通常可以使用线程，因为额外的处理器对于花费大部分时间等待事件的程序帮助不大。对于涉及大量 CPU 处理的应用程序，使用线程来细分工作不会带来任何好处，并且会使程序运行更慢（通常比你猜测的*慢*得多）。为此，你需要依赖子进程和消息传递。
```



即使使用了线程，许多程序员也发现其扩展特性相当神秘。例如，一个在100个线程下运行良好的多线程网络服务器，在扩展到10,000个线程时可能会出现可怕的性能问题。作为一个通用规则，你确实不应该编写拥有10,000个线程的程序，因为每个线程都需要自己的系统资源，并且与线程上下文切换、锁定和其他事务相关的开销开始变得显著（更不用说所有线程都被限制在单个CPU上运行这一事实）。为了应对此问题，通常会看到此类应用被重构为异步事件处理系统。例如，一个中央事件循环可能使用`select`模块监控所有I/O源，并将异步事件分发给大量的I/O处理器。这是`asyncore`等库模块以及像Twisted (http://twistedmatrix.com) 这样的流行第三方模块的基础。

展望未来，消息传递可能是你在Python中进行任何类型并发编程时都应该采纳的概念。即使使用线程，一个经常被推荐的方法也是将你的应用构建为一组独立的线程，它们通过消息队列交换数据。这种特定方法往往更不易出错，因为它大大减少了使用锁和其他同步原语的需求。消息传递也自然地扩展到网络和分布式系统。例如，如果程序的一部分最初是一个线程，你向其发送消息，那么该组件稍后可以通过网络连接发送消息，从而迁移到单独的进程或不同的机器上。消息传递抽象也与Python的高级特性相关联，例如协程。例如，*协程*是一个可以接收和处理发送给它的消息的函数。因此，通过采纳消息传递，你会发现你可以编写具有高度灵活性的程序。

本章的剩余部分将介绍用于支持并发编程的不同库模块。最后，将提供关于常见编程习惯用法的更详细信息。

#### multiprocessing

`multiprocessing`模块提供了在子进程中启动任务、通信和共享数据以及执行各种形式同步的支持。其编程接口旨在模仿`threading`模块中线程的编程接口。然而，与线程不同的是，必须强调的是，进程没有任何共享状态。因此，如果一个进程修改了数据，该更改仅限于该进程。

`multiprocessing`模块的功能非常丰富，使其成为最大和最高级的内置库之一。这里不可能涵盖该模块的每个细节，但将介绍其基本部分以及示例。有经验的程序员应该能够利用这些示例并将其扩展到更大的问题。

##### 进程

`multiprocessing`模块的所有功能都集中在进程上。它们由以下类描述。

```
Process([group [, target [, name [, args [, kwargs]]]]])
```

一个表示在子进程中运行任务的类。构造函数中的参数在指定时应始终使用关键字参数。`target`是一个可调用对象，当进程启动时执行；`args`是传递给`target`的位置参数元组；`kwargs`是传递给`target`的关键字参数字典。如果省略`args`和`kwargs`，则`target`将在没有参数的情况下被调用。`name`是一个字符串，为进程提供描述性名称。`group`未使用，始终设置为`None`。它的存在只是为了使`Process`的构造模仿`threading`模块中线程的创建。

`Process`的一个实例`p`具有以下方法：

```
p.is_alive()
```

如果`p`仍在运行，则返回`True`。

```
p.join([timeout])
```

等待进程`p`终止。`timeout`指定一个可选的超时时间段。一个进程可以根据需要多次join，但是尝试join自身是一个错误。

```
p.run()
```

当进程启动时运行的方法。默认情况下，这会调用传递给`Process`构造函数的`target`。作为替代方案，可以通过继承`Process`并重新实现`run()`来定义一个进程。

```
p.start()
```

启动进程。这会启动表示该进程的子进程，并在该子进程中调用`p.run()`。

```
p.terminate()
```

强制终止进程。如果调用此方法，进程`p`将立即终止，而不会执行任何清理操作。如果进程`p`创建了它自己的子进程，这些进程将变成僵尸进程。使用此方法时需要小心。如果`p`持有锁或涉及进程间通信，终止它可能会导致死锁或损坏的I/O。

`Process`实例`p`还具有以下数据属性：

```
p.authkey
```

进程的身份验证密钥。除非明确设置，否则这是一个由`os.urandom()`生成的32字节随机字符串。此密钥的目的是为涉及网络连接的底层进程间通信提供安全性。只有当两端具有相同的身份验证密钥时，此类连接才能工作。

```
p.daemon
```

一个布尔标志，指示该进程是否为守护进程。*守护*进程会在创建它的Python进程终止时自动终止。此外，守护进程被禁止自行创建新进程。`p.daemon`的值必须在使用`p.start()`启动进程之前设置。

**p.exitcode**

进程的整数退出码。如果进程仍在运行，则为None。如果值为负，值为*-N*表示进程被信号*N*终止。

**p.name**

进程的名称。

**p.pid**

进程的整数进程ID。

这里有一个示例，展示了如何创建并启动一个函数（或其他可调用对象）作为单独的进程：

```python
import multiprocessing
import time

def clock(interval):
    while True:
        print("The time is %s" % time.ctime())
        time.sleep(interval)

if __name__ == '__main__':
    p = multiprocessing.Process(target=clock, args=(15,))
    p.start()
```

这里有一个示例，展示了如何将此进程定义为继承自Process的类：

```python
import multiprocessing
import time

class ClockProcess(multiprocessing.Process):
    def __init__(self, interval):
        multiprocessing.Process.__init__(self)
        self.interval = interval
    def run(self):
        while True:
            print("The time is %s" % time.ctime())
            time.sleep(self.interval)

if __name__ == '__main__':
    p = ClockProcess(15)
    p.start()
```

在这两个示例中，子进程应该每15秒打印一次时间。必须强调的是，为了跨平台可移植性，新的进程应该只由主程序创建，如所示。虽然这在UNIX上是可选的，但在Windows上是必需的。还应该注意，在Windows上，你可能需要在命令行（`command.exe`）而不是Python IDE（如IDLE）中运行前面的示例。

###### 进程间通信

`multiprocessing`模块支持两种主要的进程间通信形式：管道和队列。这两种方法都是使用消息传递实现的。但是，队列接口旨在模仿线程程序中通常使用的队列。

####### Queue([maxsize])

创建一个共享的进程队列。*maxsize*是队列中允许的最大项目数。如果省略，则没有大小限制。底层队列是使用管道和锁实现的。此外，会启动一个支持线程，以便将队列中的数据馈送到底层管道中。

`Queue`的一个实例*q*具有以下方法：

######## q.cancel_join_thread()

不要在进程退出时自动join后台线程。这可以防止`join_thread()`方法阻塞。

######## q.close()

关闭队列，防止再向其中添加任何数据。调用此方法后，后台线程将继续写入尚未写入的所有排队数据，但完成后将立即关闭。如果*q*被垃圾回收，此方法将自动调用。关闭队列不会在队列消费者中产生任何类型的数据结束信号或异常。例如，如果消费者阻塞在`get()`操作上，在生产者中关闭队列不会导致`get()`返回错误。

######## q.empty()

如果在调用时*q*为空，则返回`True`。如果其他进程或线程正在用于添加队列项目，请注意结果不可靠（例如，在结果返回和使用之间可能已将新项目添加到队列中）。

######## q.full()

如果*q*已满，则返回`True`。由于线程的原因，结果也不可靠（参见`q.empty()`）。

######## q.get([block [, timeout]])

从*q*中返回一个项目。如果*q*为空，则阻塞，直到队列项目变得可用。*block*控制阻塞行为，默认为`True`。如果设置为`False`，且队列为空，则会引发`Queue.Empty`异常（在`Queue`库模块中定义）。*timeout*是在阻塞模式下使用的可选超时。如果在指定的时间间隔内没有项目变得可用，则会引发`Queue.Empty`异常。

######## q.get_nowait()

与`q.get(False)`相同。

######## q.join_thread()

join队列的后台线程。这用于在调用`q.close()`后等待所有队列项目被消耗。在所有不是*q*原始创建者的进程中，默认调用此方法。可以通过调用`q.cancel_join_thread()`来禁用此行为。

######## q.put(item [, block [, timeout]])

将*item*放入队列。如果队列已满，则阻塞，直到有空间可用。*block*控制阻塞行为，默认为`True`。如果设置为`False`，且队列已满，则会引发`Queue.Full`异常（在`Queue`库模块中定义）。*timeout*指定在阻塞模式下等待空间可用的时间。超时将引发`Queue.Full`异常。

与 `q.put(item, False)` 相同。

####### q.qsize()

返回队列中当前大约有多少个项目。此函数的结果并不可靠，因为在结果返回和程序后续使用之间，队列中的项目可能已经被添加或移除。在某些系统上，此方法可能会引发 `NotImplementedError`。

####### JoinableQueue([maxsize])

创建一个可连接的共享进程队列。这就像一个 `Queue`，但允许项目的消费者通知生产者项目已被成功处理。通知过程是通过共享信号量和条件变量实现的。

`JoinableQueue` 的实例 `q` 拥有与 `Queue` 相同的方法，但它还有以下附加方法：

######## q.task_done()

由消费者使用，用于发出信号表示由 `q.get()` 返回的入队项目已被处理。如果此方法的调用次数超过从队列中移除的项目次数，将引发 `ValueError` 异常。

######## q.join()

由生产者使用，用于阻塞，直到放入队列的所有项目都被处理完毕。此操作会阻塞，直到对放入队列的每个项目都调用了 `q.task_done()`。

以下示例展示了如何设置一个永远运行的进程，该进程从队列中消费并处理项目。生产者将项目放入队列，并等待它们被处理。

```python
import multiprocessing

def consumer(input_q):
    while True:
        item = input_q.get()
        # 处理项目
        print(item)      # 替换为有用的工作
        # 发送任务完成信号
        input_q.task_done()

def producer(sequence, output_q):
    for item in sequence:
        # 将项目放入队列
        output_q.put(item)

##### 设置
if __name__ == '__main__':
    q = multiprocessing.JoinableQueue()
    # 启动消费者进程
    cons_p = multiprocessing.Process(target=consumer, args=(q,))
    cons_p.daemon = True
    cons_p.start()

    # 生产项目。sequence 代表一个将要发送给消费者的项目序列。
    # 在实践中，这可以是生成器的输出或以其他方式产生的项目。
    sequence = [1, 2, 3, 4]
    producer(sequence, q)

    # 等待所有项目被处理完毕
    q.join()
```

在这个示例中，消费者进程被设置为守护进程，因为它会永远运行，而我们希望在主程序结束时它也能终止（如果你忘记了这一点，程序将会挂起）。这里使用了 `JoinableQueue`，以便生产者确实知道放入队列的所有项目何时被成功处理。`join()` 操作确保了这一点；如果你忘记了这个步骤，消费者将在完成所有工作之前被终止。

如果需要，多个进程可以从同一个队列中放入和获取项目。例如，如果你想拥有一个消费者进程池，你可以这样编写代码：

```python
if __name__ == '__main__':
    q = multiprocessing.JoinableQueue()
    # 启动一些消费者进程
    cons_p1 = multiprocessing.Process(target=consumer, args=(q,))
    cons_p1.daemon = True
    cons_p1.start()

    cons_p2 = multiprocessing.Process(target=consumer, args=(q,))
    cons_p2.daemon = True
    cons_p2.start()

    # 生产项目。sequence 代表一个将要发送给消费者的项目序列。
    # 在实践中，这可以是生成器的输出或以其他方式产生的项目。
    sequence = [1, 2, 3, 4]
    producer(sequence, q)

    # 等待所有项目被处理完毕
    q.join()
```

在编写此类代码时，请注意，放入队列的每个项目都会被序列化并通过管道或套接字连接发送到进程。通常，发送少量的大对象比发送大量的小对象更好。

在某些应用中，生产者可能想要通知消费者不会再有项目被生产，并且它们应该关闭。为此，你应该编写使用哨兵（sentinel）的代码——一个表示完成的特殊值。以下示例展示了使用 `None` 作为哨兵的概念：

```python
import multiprocessing

def consumer(input_q):
    while True:
        item = input_q.get()
        if item is None:
            break
        # 处理项目
        print(item)      # 替换为有用的工作
    # 关闭
    print("Consumer done")

def producer(sequence, output_q):
    for item in sequence:
        # 将项目放入队列
        output_q.put(item)

if __name__ == '__main__':
    q = multiprocessing.Queue()
    # 启动消费者进程
    cons_p = multiprocessing.Process(target=consumer, args=(q,))
    cons_p.start()

    # 生产项目
    sequence = [1, 2, 3, 4]
    producer(sequence, q)

    # 通过将哨兵放入队列来发出完成信号
    q.put(None)
    # 等待消费者进程关闭
    cons_p.join()
```

如果你像示例中那样使用哨兵，请注意你需要为每个消费者在队列中放入一个哨兵。例如，如果有三个消费者进程在消费队列中的项目，生产者需要在队列中放入三个哨兵才能让所有消费者都关闭。

作为使用队列的替代方案，可以使用管道在进程之间执行消息传递。

###### Pipe([duplex])

在进程之间创建一个管道，并返回一个元组 `(conn1, conn2)`，其中 `conn1` 和 `conn2` 是表示管道两端的 `Connection` 对象。默认情况下，管道是双向的。如果将 `duplex` 设置为 `False`，则 `conn1` 只能用于接收，`conn2` 只能用于发送。`Pipe()` 必须在创建和启动任何使用该管道的 `Process` 对象之前调用。

由 `Pipe()` 返回的 `Connection` 对象 `c` 的实例具有以下方法和属性：

####### c.close()

关闭连接。如果 `c` 被垃圾回收，将自动调用此方法。

####### c.fileno()

返回连接使用的整数文件描述符。

####### c.poll([timeout])

如果连接上有数据可用，则返回 `True`。`timeout` 指定等待的最大时间。如果省略，该方法将立即返回结果。如果 `timeout` 设置为 `None`，则该操作将无限期等待数据到达。

####### c.recv()

接收由 `c.send()` 发送的对象。如果连接的另一端已关闭且没有更多数据，将引发 `EOFError`。

####### c.recv_bytes([maxlength])

接收由 `c.send_bytes()` 发送的完整字节消息。`maxlength` 指定要接收的最大字节数。如果传入的消息超过此大小，将引发 `IOError`，并且无法再从该连接读取。如果连接的另一端已关闭且没有更多数据，将引发 `EOFError`。

####### c.recv_bytes_into(buffer[, offset])

接收一条完整的字节消息，并将其存储在支持可写缓冲区接口的对象 `buffer` 中（例如，一个 `bytearray` 对象或类似对象）。`offset` 指定在缓冲区中放置消息的字节偏移量。返回接收到的字节数。如果消息的长度超过可用的缓冲区空间，将引发 `BufferTooShort`。

####### c.send(obj)

通过连接发送一个对象。`obj` 是任何与 pickle 兼容的对象。

####### c.send_bytes(buffer[, offset[, size]])

通过连接发送一个字节数据缓冲区。`buffer` 是任何支持缓冲区接口的对象，`offset` 是缓冲区中的字节偏移量，`size` 是要发送的字节数。生成的数据作为单条消息发送，通过调用一次 `c.recv_bytes()` 来接收。

管道可以以类似于队列的方式使用。以下示例展示了使用管道实现的前面提到的生产者-消费者问题：

```python
import multiprocessing

# 在管道上消费项目。
def consumer(pipe):
    output_p, input_p = pipe
    input_p.close()     # 关闭管道的输入端
    while True:
        try:
            item = output_p.recv()
        except EOFError:
            break
        # 处理项目
        print(item)         # 替换为有用的工作
    # 关闭
    print("Consumer done")

# 生产项目并放入队列。sequence 是一个表示要处理项目的可迭代对象。
def producer(sequence, input_p):
    for item in sequence:
        # 将项目放入队列
        input_p.send(item)

if __name__ == '__main__':
    (output_p, input_p) = multiprocessing.Pipe()
    # 启动消费者进程
    cons_p = multiprocessing.Process(target=consumer, args=((output_p, input_p),))
    cons_p.start()

    # 在生产者中关闭输出管道
    output_p.close()

    # 生产项目
    sequence = [1, 2, 3, 4]
    producer(sequence, input_p)

    # 通过关闭输入管道来发出完成信号
    input_p.close()

    # 等待消费者进程关闭
    cons_p.join()
```

应当特别注意管道端点的正确管理。如果管道的某一端在生产者或消费者中未被使用，则应将其关闭。例如，这就是为什么管道的输出端在生产者中关闭，而管道的输入端在消费者中关闭的原因。如果你忘记了其中一个步骤，程序可能会在消费者的 `recv()` 操作上挂起。管道由操作系统进行引用计数，必须在所有进程中都关闭才能产生 `EOFError` 异常。因此，在生产者中关闭管道不会产生任何效果，除非消费者也关闭管道的同一端。

管道可用于双向通信。这可用于编写通过请求/响应模型与进程交互的程序，该模型通常与客户端/服务器计算或远程过程调用相关联。以下是一个示例：

```python
import multiprocessing

# A server process
def adder(pipe):
    server_p, client_p = pipe
    client_p.close()
    while True:
        try:
            x,y = server_p.recv()
        except EOFError:
            break
        result = x + y
        server_p.send(result)
    # Shutdown
    print("Server done")

if __name__ == '__main__':
    (server_p, client_p) = multiprocessing.Pipe()
    # Launch the server process
    adder_p = multiprocessing.Process(target=adder,args=((server_p, client_p),))
    adder_p.start()

    # Close the server pipe in the client
    server_p.close()

    # Make some requests on the server
    client_p.send((3,4))
    print(client_p.recv())

    client_p.send(('Hello','World'))
    print(client_p.recv())

    # Done. Close the pipe
    client_p.close()

    # Wait for the consumer process to shutdown
    adder_p.join()
```

在此示例中，`adder()` 函数作为服务器运行，等待消息到达其管道端。当收到消息时，它执行一些处理并通过管道将结果发回。请记住，`send()` 和 `recv()` 使用 `pickle` 模块来序列化对象。在该示例中，服务器接收一个元组 `(x, y)` 作为输入并返回结果 `x + y`。但是，对于使用远程过程调用的更高级应用程序，你应该使用进程池，如下所述。

##### 进程池

以下类允许你创建一个进程池，可以向其提交各种类型的数据处理任务。池提供的功能在某种程度上类似于列表推导式和函数式编程操作（如 map-reduce）提供的功能。

```
Pool([numprocess [,initializer [, initargs]])
```

创建一个工作进程池。`numprocess` 是要创建的进程数。如果省略，则使用 `cpu_count()` 的值。`initializer` 是一个可调用对象，将在每个工作进程启动时执行。`initargs` 是传递给 `initializer` 的参数元组。默认情况下，`initializer` 为 `None`。

`Pool` 的实例 `p` 支持以下操作：

```
p.apply(func [, args [, kwargs]])
```

在池的一个工作进程中执行 `func(*args, **kwargs)` 并返回结果。需要强调的是，这并不会在所有池工作进程中并行执行 `func`。如果你想让 `func` 使用不同的参数并发执行，你必须从不同的线程调用 `p.apply()` 或使用 `p.apply_async()`。

```
p.apply_async(func [, args [, kwargs [, callback]]])
```

在池的一个工作进程中执行 `func(*args, **kwargs)` 并异步返回结果。此方法的结果是 `AsyncResult` 的实例，可用于稍后获取最终结果。`callback` 是一个接受单个输入参数的可调用对象。当 `func` 的结果可用时，它会立即传递给 `callback`。`callback` 不应执行任何阻塞操作，否则会阻塞其他异步操作中结果的接收。

```
p.close()
```

关闭进程池，防止进一步的操作。如果仍有任何操作待处理，它们将在工作进程终止之前完成。

```
p.join()
```

等待所有工作进程退出。只能在 `close()` 或 `terminate()` 之后调用。

```
p.imap(func, iterable [, chunksize])
```

`map()` 的一个版本，返回一个迭代器而不是结果列表。

```
p.imap_unordered(func, iterable [, chunksize])
```

与 `imap()` 相同，但结果按从工作进程接收的任意顺序返回。

```
p.map(func, iterable [, chunksize])
```

将可调用对象 `func` 应用于 `iterable` 中的所有项，并以列表形式返回结果。该操作通过将 `iterable` 拆分为块并将工作分配给工作进程来并行执行。`chunksize` 指定每个块中的项目数。对于大量数据，增加 `chunksize` 将提高性能。

```
p.map_async(func, iterable [, chunksize [, callback]])
```

与 map() 相同，但结果异步返回。返回值是 AsyncResult 的实例，可用于稍后获取结果。callback 是一个接受单个参数的可调用对象。如果提供了 callback，则在结果可用时使用结果调用 callback。

```
p.terminate()
```

立即终止所有工作进程，不执行任何清理工作或完成任何待处理的工作。如果 p 被垃圾回收，将调用此方法。

`apply_async()` 和 `map_async()` 方法返回一个 AsyncResult 实例作为结果。`AsyncResult` 的实例 `a` 具有以下方法：

```
a.get([timeout])
```

返回结果，必要时等待其到达。timeout 是一个可选的超时时间。如果结果在给定时间内未到达，将引发 `multiprocessing.TimeoutError` 异常。如果远程操作中引发了异常，调用此方法时将重新引发该异常。

```
a.ready()
```

如果调用已完成则返回 True。

```
a.successful()
```

如果调用完成且没有任何异常则返回 True。如果在结果就绪之前调用此方法，将引发 AssertionError。

```
a.wait([timeout])
```

等待结果变为可用。timeout 是一个可选的超时时间。

以下示例演示了使用进程池为整个目录中的文件构建将文件名映射到 SHA512 摘要值的字典：

```python
import os
import multiprocessing
import hashlib

# Some parameters you can tweak
BUFSIZE = 8192           # Read buffer size
POOLSIZE = 2             # Number of workers

def compute_digest(filename):
    try:
        f = open(filename,"rb")
    except IOError:
        return None
    digest = hashlib.sha512()
    while True:
        chunk = f.read(BUFSIZE)
        if not chunk: break
        digest.update(chunk)
    f.close()
    return filename, digest.digest()

def build_digest_map(topdir):
    digest_pool = multiprocessing.Pool(POOLSIZE)
    allfiles = (os.path.join(path,name)
                   for path, dirs, files in os.walk(topdir)
                   for name in files)

    digest_map = dict(digest_pool.imap_unordered(compute_digest,allfiles,20))
    digest_pool.close()
    return digest_map

# Try it out. Change the directory name as desired.
if __name__ == '__main__':
    digest_map = build_digest_map("/Users/beazley/Software/Python-3.0")
    print(len(digest_map))
```

在此示例中，使用生成器表达式指定了目录树中所有文件的路径名序列。然后，使用 `imap_unordered()` 函数将此序列切分并分配给进程池。每个池工作进程使用 `compute_digest()` 函数为其文件计算 SHA512 摘要值。结果被发送回主进程并收集到 Python 字典中。虽然这绝非科学结果，但此示例在作者的双核 Macbook 上运行时，比单进程解决方案获得了 75% 的速度提升。

请记住，只有当池工作进程执行足够多的工作来证明额外的通信开销是合理的时，使用进程池才有意义。作为一般规则，对于简单的计算（如仅将两个数字相加），使用池是没有意义的。

##### 共享数据和同步

通常，进程之间完全隔离，唯一的通信方式是队列或管道。但是，可以使用两个对象来表示共享数据。在底层，这些对象使用共享内存（通过 mmap）使多进程中的访问成为可能。

**`Value(typecode, arg1, ... argN, lock)`**

在共享内存中创建一个 `ctypes` 对象。`typecode` 是一个包含 `array` 模块使用的类型代码的字符串（例如 `'i'`、`'d'` 等），或者是来自 `ctypes` 模块的类型对象（例如 `ctypes.c_int`、`ctypes.c_double` 等）。所有额外的位置参数 `arg1, arg2, ... argN` 都传递给给定类型的构造函数。`lock` 是一个仅关键字参数，如果设置为 `True`（默认值），则会创建一个新锁来保护对值的访问。如果你传入一个现有锁，例如 `Lock` 或 `RLock` 实例，则该锁将用于同步。如果 `v` 是由 `Value` 创建的共享值的实例，则使用 `v.value` 访问底层值。例如，读取 `v.value` 将获取值，赋值 `v.value` 将更改值。

**`RawValue(typecode, arg1, ..., argN)`**

与 `Value` 相同，但没有锁定。

**`Array(typecode, initializer, lock)`**

在共享内存中创建一个 `ctypes` 数组。`typecode` 描述数组的内容，其含义与 `Value()` 中描述的相同。`initializer` 是一个设置数组初始大小的整数，或一个其值和大小用于初始化数组的项目序列。`lock` 是一个仅关键字参数，其含义与 `Value()` 中描述的相同。如果 `a` 是由 `Array` 创建的共享数组的实例，则你可以

可以使用标准的 Python 索引、切片和迭代操作来访问其内容，每种操作都通过锁进行同步。对于字节字符串，`a` 还将拥有一个 `a.value` 属性，用于将整个数组作为单个字符串来访问。

```
RawArray(typecode, initializer)
```

与 `Array` 相同，但没有锁定机制。如果你编写的程序需要一次性操作大量数组元素，使用这种数据类型配合单独的锁进行同步（如果需要的话），性能会显著提高。

除了使用 `Value()` 和 `Array()` 创建的共享值之外，`multiprocessing` 模块还提供了以下同步原语的共享版本：

| 原语 | 描述 |
|-----------|-------------|
| Lock | 互斥锁 |
| RLock | 可重入互斥锁（同一进程可以多次获取而不会阻塞） |
| Semaphore | 信号量 |
| BoundedSemaphore | 有界信号量 |
| Event | 事件 |
| Condition | 条件变量 |

这些对象的行为模拟了 `threading` 模块中同名的同步原语。请参阅 `threading` 文档以获取更多详细信息。

需要注意的是，使用 `multiprocessing` 时，通常不需要像使用线程那样过多担心使用锁、信号量或类似构造进行底层同步。部分原因在于，管道上的 `send()` 和 `receive()` 操作以及队列上的 `put()` 和 `get()` 操作已经提供了同步机制。然而，共享值和锁在某些特定场景下仍有用途。下面是一个使用共享数组（而非管道）将 Python 浮点数列表发送到另一个进程的示例：

```python
import multiprocessing

class FloatChannel(object):
    def __init__(self, maxsize):
        self.buffer    = multiprocessing.RawArray('d', maxsize)
        self.buffer_len = multiprocessing.Value('i')
        self.empty    = multiprocessing.Semaphore(1)
        self.full     = multiprocessing.Semaphore(0)

    def send(self, values):
        self.empty.acquire()         # Only proceed if buffer empty
        nitems = len(values)
        self.buffer_len = nitems      # Set the buffer size
        self.buffer[:nitems] = values # Copy values into the buffer
        self.full.release()           # Signal that buffer is full

    def recv(self):
        self.full.acquire()           # Only proceed if buffer full
        values = self.buffer[:self.buffer_len.value]  # Copy values
        self.empty.release()          # Signal that buffer is empty
        return values
```

```python
# Performance test. Receive a bunch of messages
def consume_test(count, ch):
    for i in xrange(count):
        values = ch.recv()

# Performance test. Send a bunch of messages
def produce_test(count, values, ch):
    for i in xrange(count):
        ch.send(values)

if __name__ == '__main__':
    ch = FloatChannel(100000)
    p = multiprocessing.Process(target=consume_test,
                                args=(1000, ch))
    p.start()
    values = [float(x) for x in xrange(100000)]
    produce_test(1000, values, ch)
    print("Done")
    p.join()
```

关于此示例的进一步研究留给读者自行完成。然而，在作者机器上的性能测试中，通过 `FloatChannel` 发送大量浮点数列表比通过 `Pipe`（需要对所有值进行序列化和反序列化）发送列表快约 80%。

##### 受管对象

与线程不同，进程不支持共享对象。虽然你可以像上一节所示那样创建共享值和数组，但这对更高级的 Python 对象（如字典、列表或用户自定义类的实例）并不适用。不过，`multiprocessing` 模块确实提供了一种使用共享对象的方式，前提是它们在所谓的管理器控制下运行。管理器是一个独立的子进程，真正的对象存在于其中，并作为服务器运行。其他进程通过使用代理来访问共享对象，这些代理充当管理器服务器的客户端。

使用简单受管对象最直接的方式是使用 `Manager()` 函数。

###### Manager()

在单独的进程中创建一个运行中的管理器服务器。返回一个 `SyncManager` 类型的实例，该类型在 `multiprocessing.managers` 子模块中定义。

`Manager()` 返回的 `SyncManager` 实例 `m` 具有一系列用于创建共享对象并返回可用于访问它们的代理的方法。通常，你需要在启动任何新进程之前创建管理器，并使用这些方法创建共享对象。以下方法已定义：

####### m.Array(typecode, sequence)

在服务器上创建一个共享的 `Array` 实例，并返回其代理。参数说明请参阅"共享数据与同步"部分。

####### m.BoundedSemaphore([value])

在服务器上创建一个共享的 `threading.BoundedSemaphore` 实例，并返回其代理。

####### m.Condition([lock])

在服务器上创建一个共享的 `threading.Condition` 实例，并返回其代理。`lock` 是由 `m.Lock()` 或 `m.RLock()` 创建的代理实例。

####### m.dict([args])

在服务器上创建一个共享的 `dict` 实例，并返回其代理。此方法的参数与内置 `dict()` 函数的参数相同。

####### m.Event()

在服务器上创建一个共享的 `threading.Event` 实例，并返回其代理。

####### m.list([sequence])

在服务器上创建一个共享的 `list` 实例，并返回其代理。此方法的参数与内置 `list()` 函数的参数相同。

####### m.Lock()

在服务器上创建一个共享的 `threading.Lock` 实例，并返回其代理。

####### m.Namespace()

在服务器上创建一个共享的命名空间对象，并返回其代理。命名空间是一个与 Python 模块有些相似的对象。例如，如果 `n` 是一个命名空间代理，你可以使用点号（`.`）来赋值和读取属性，如 `n.name = value` 或 `value = n.name`。然而，名称的选择很重要。如果 `name` 以字母开头，那么该值是管理器所持有的共享对象的一部分，可在所有其他进程中访问。如果 `name` 以 underscores 开头，则它只是代理对象的一部分，不会被共享。

####### m.Queue()

在服务器上创建一个共享的 `Queue.Queue` 对象，并返回其代理。

####### m.RLock()

在服务器上创建一个共享的 `threading.RLock` 对象，并返回其代理。

####### m.Semaphore([value])

在服务器上创建一个共享的 `threading.Semaphore` 对象，并返回其代理。

####### m.Value(typecode, value)

在服务器上创建一个共享的 `Value` 对象，并返回其代理。参数说明请参阅"共享数据与同步"部分。

以下示例展示了如何使用管理器来创建进程间共享的字典。

```python
import multiprocessing
import time

# print out d whenever the passed event gets set
def watch(d, evt):
    while True:
        evt.wait()
        print(d)
        evt.clear()

if __name__ == '__main__':
    m    = multiprocessing.Manager()
    d    = m.dict()         # Create a shared dict
    evt  = m.Event()        # Create a shared Event

    # Launch a process that watches the dictionary
    p = multiprocessing.Process(target=watch, args=(d, evt))
    p.daemon = True
    p.start()

    # Update the dictionary and notify the watcher
    d['foo'] = 42
    evt.set()
    time.sleep(5)

    # Update the dictionary and notify the watcher
    d['bar'] = 37
    evt.set()
    time.sleep(5)

    # Terminate the process and manager
    p.terminate()
    m.shutdown()
```

运行此示例时，`watch()` 函数会在每次传入的事件被设置时打印出 *d* 的值。在主程序中，创建了一个共享字典和事件，并在主进程中对其进行操作。运行时，你会看到子进程打印数据。

如果你想拥有其他类型的共享对象（如用户自定义类的实例），则需要创建自定义管理器对象。为此，你需要创建一个继承自 `BaseManager` 的类，该类在 `multiprocessing.managers` 子模块中定义。

```
managers.BaseManager([address [, authkey]])
```

用于为用户自定义对象创建自定义管理器服务器的基类。*address* 是一个可选的元组（*hostname*, *port*），用于指定服务器的网络地址。如果省略，操作系统将自动分配一个对应于某个空闲端口号的地址。*authkey* 是一个用于验证连接到服务器的客户端身份的字符串。如果省略，则使用 `current_process().authkey` 的值。

如果 *mgrclass* 是一个继承自 `BaseManager` 的类，则使用以下类方法来创建返回共享对象代理的方法。

```
mgrclass.register(typeid [, callable [, proxytype [, exposed [, method_to_typeid
    [, create_method]]]]])
```

向管理器类注册新的数据类型。*typeid* 是一个用于命名特定种类共享对象的字符串。该字符串应该是有效的 Python 标识符。*callable* 是一个可调用对象，用于创建或返回要共享的实例。*proxytype* 是一个类，提供代理对象在客户端中的实现。通常，这些类会默认生成，因此通常设置为 `None`。*exposed* 是共享对象上将暴露给代理对象的方法名序列。如果省略，则使用 `proxytype._exposed_` 的值，如果该值未定义，则使用所有公共方法（所有不以下划线（`_`）开头的可调用方法）。*method_to_typeid* 是从方法名到类型 ID 的映射，用于指定哪些方法应使用代理对象返回其结果。如果

如果在此映射中找不到该方法，则返回值将被复制并返回。如果 `method_to_typeid` 为 `None`，则使用 `proxytype._method_to_typeid_` 的值（如果已定义）。`create_method` 是一个布尔标志，用于指定是否应在 `mgrclass` 中创建名为 `typeid` 的方法。默认情况下，该值为 True。

从 `BaseManager` 派生的管理器的实例 `m` 必须手动启动才能运行。以下属性和方法与此相关：

####### m.address

一个包含管理器服务器所用地址的元组 `(hostname, port)`。

####### m.connect()

连接到一个远程管理器对象，其地址已在 `BaseManager` 构造函数中给出。

####### m.serve_forever()

在当前进程中运行管理器服务器。

####### m.shutdown()

关闭由 `m.start()` 方法启动的管理器服务器。

####### m.start()

启动一个独立的子进程，并在该进程中启动管理器服务器。

以下示例展示了如何为用户定义的类创建管理器：

```
import multiprocessing
from multiprocessing.managers import BaseManager

class A(object):
    def __init__(self,value):
        self.x = value
    def __repr__(self):
        return "A(%s)" % self.x
    def getX(self):
        return self.x
    def setX(self,value):
        self.x = value
    def __iadd__(self,value):
        self.x += value
        return self

class MyManager(BaseManager): pass
MyManager.register("A",A)

if __name__ == '__main__':
    m = MyManager()
    m.start()
    # Create a managed object
    a = m.A(37)
    ...
```

在此示例中，最后一条语句创建了一个在管理器服务器上存在的 `A` 的实例。前面代码中的变量 `a` 只是该实例的代理。此代理的行为与服务器上的对象——*被引用对象*类似（但并非完全相同）。首先，你会发现无法访问数据属性和属性。相反，你必须使用访问函数：

```
>>> a.x
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'AutoProxy[A]' object has no attribute 'x'
>>> a.getX()
37
>>> a.setX(42)
>>>
```

对于代理，`repr()` 函数返回表示代理的字符串，而 `str()` 返回被引用对象上 `__repr__()` 的输出。例如：

```
>>> a
<AutoProxy[A] object, typeid 'A' at 0xcef230>
>>> print(a)
A(37)
>>>
```

特殊方法和任何以下划线 (`_`) 开头的方法在代理上不可访问。例如，如果你尝试调用 `a.__iadd__()`，它将不起作用：

```
>>> a += 37
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +=: 'AutoProxy[A]' and 'int'
>>> a.__iadd__(37)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'AutoProxy[A]' object has no attribute '__iadd__'
>>>
```

在更高级的应用中，可以自定义代理以更精确地控制访问。这是通过定义一个继承自 `BaseProxy` 的类来实现的，该类定义在 `multiprocessing.managers` 中。以下代码展示了如何为前面示例中的 A 类创建一个自定义代理，该代理正确地暴露了 `__iadd__()` 方法，并使用属性来暴露 x 属性：

```
from multiprocessing.managers import BaseProxy

class AProxy(BaseProxy):
    # A list of all methods exposed on the referent
    exposed_ = ['__iadd__','getX','setX']
    # Implement the public interface of the proxy
    def __iadd__(self,value):
        self._callmethod('__iadd__',(value,))
        return self
    @property
    def x(self):
        return self._callmethod('getX',())
    @x.setter
    def x(self,value):
        self._callmethod('setX',(value,))

class MyManager(BaseManager): pass
MyManager.register("A", A, proxytype=AProxy)
```

从 `BaseProxy` 派生的类的实例代理具有以下方法：

```
proxy._callmethod(name [, args [, kwargs]])
```

在代理的被引用对象上调用名为 *name* 的方法。*name* 是一个包含方法名的字符串，*args* 是一个包含位置参数的元组，*kwargs* 是一个关键字参数字典。方法 *name* 必须显式暴露。通常通过将其包含在代理类的 `_exposed_` 类属性中来实现。

```
proxy._getvalue()
```

在调用者中返回被引用对象的副本。如果此调用是在不同的进程中进行的，则被引用对象将被打包、发送给调用者，然后解包。如果被引用对象无法打包，则会引发异常。

###### 连接

使用 `multiprocessing` 模块的程序可以与在同一台机器上运行的其他进程或位于远程系统上的进程进行消息传递。如果你想将一个为单系统编写的程序扩展到在计算集群上工作，这将非常有用。`multiprocessing.connection` 子模块提供了用于此目的的函数和类：

```
connections.Client(address [, family [, authenticate [, authkey]]])
```

连接到另一个已经在地址 *address* 处监听的进程。*address* 是一个表示网络地址的元组 `(hostname, port)`，一个表示 UNIX 域套接字的文件名，或一个形式为 `r'\\servername\pipe\pipename'` 的字符串，表示远程系统 *servername* 上的 Windows 命名管道（对本地机器使用 `'.'` 作为 *servername*）。*family* 是一个表示地址格式的字符串，通常为 `'AF_INET'`、`'AF_UNIX'` 或 `'AF_PIPE'` 之一。如果省略，则从 *address* 的格式推断 family。*authenticate* 是一个布尔标志，指定是否要使用摘要认证。*authkey* 是一个包含认证密钥的字符串。如果省略，则使用 `current_process().authkey` 的值。此函数的返回值是一个 Connection 对象，之前在"进程间通信"的管道部分中已有描述。

```
connections.Listener([address [, family [, backlog [, authenticate [, authkey]]]]])
```

一个实现了服务器的类，用于监听和处理由 `Client()` 函数发起的连接。*address*、*family*、*authenticate* 和 *authkey* 参数的含义与 `Client()` 相同。*backlog* 是一个整数，对应于当 *address* 参数指定网络连接时传递给套接字 `listen()` 方法的值。默认情况下，*backlog* 为 1。如果省略 *address*，则选择默认地址。如果 *address* 和 *family* 都被省略，则选择本地系统上最快的可用通信方案。

`Listener` 的实例 *s* 支持以下方法和属性：

```
s.accept()
```

接受一个新连接并返回一个 Connection 对象。如果认证失败，则引发 AuthenticationError。

```
s.address
```

监听器正在使用的地址。

```
s.close()
```

关闭监听器正在使用的管道或套接字。

```
s.last_accepted
```

最近被接受的客户端的地址。

以下是监听客户端并实现简单远程操作（加法）的服务器程序示例：

```
from multiprocessing.connection import Listener

serv = Listener(('',15000),authkey='12345')
while True:
    conn = serv.accept()
    while True:
        try:
            x,y = conn.recv()
        except EOFError:
            break
        result = x + y
        conn.send(result)
    conn.close()
```

以下是连接到该服务器并发送一些消息的简单客户端程序：

```
from multiprocessing.connection import Client
conn = Client(('localhost',15000), authkey="12345")

conn.send((3,4))
r = conn.recv()
print(r)         # Prints '7'

conn.send(("Hello","World"))
r = conn.recv()
print(r)         # Prints 'HelloWorld'

conn.close()
```

##### 其他实用函数

以下实用函数也被定义：

```
active_children()
```

返回所有活动子进程的 Process 对象列表。

```
cpu_count()
```

如果可以确定，则返回系统上的 CPU 数量。

```
current_process()
```

返回当前进程的 Process 对象。

```
freeze_support()
```

一个函数，应作为主程序的第一条语句包含在将使用各种打包工具（如 py2exe）进行"冻结"的应用程序中。这是为了防止在冻结应用程序中启动子进程时出现的运行时错误。



```
get_logger()

返回与多进程模块关联的日志记录对象，如果该对象尚不存在则创建它。返回的日志记录器不会将消息传播到根日志记录器，其级别为 logging.NOTSET，并将所有日志消息打印到标准错误。

set_executable(executable)

设置用于执行子进程的 Python 可执行文件的名称。此方法仅在 Windows 上定义。

##### 关于多进程的通用建议

多进程模块是 Python 库中最先进、功能最强大的模块之一。以下是一些防止你"脑子爆炸"的通用技巧：

- 在构建大型应用程序之前，请仔细阅读在线文档。虽然本节已经涵盖了基本要点，但官方文档涵盖了一些可能出现的更棘手的问题。
- 确保在进程之间传递的所有数据都与 pickle 兼容。
- 避免使用共享数据，学会喜欢消息传递和队列。通过消息传递，你不必过于担心同步、锁定和其他问题。随着进程数量的增加，它往往还能提供更好的扩展性。
- 不要在打算在单独进程中运行的函数内部使用全局变量。最好显式地传递参数。
- 除非你极力想提高自己的工作稳定性（或者根据代码审查者的情况而可能降低稳定性），否则尽量不要在同一个程序中混合使用线程和多进程。
- 非常仔细地关注进程如何关闭。作为一般规则，你应该显式地关闭进程并制定良好的终止方案，而不是仅仅依赖垃圾回收或不得不使用 terminate() 操作强制终止子进程。
- 管理器和代理的使用与分布式计算中的各种概念（例如分布式对象）密切相关。一本好的分布式计算书籍可能是一个有用的参考。
- 多进程模块源于一个名为 pyprocessing 的第三方库。搜索有关此库的使用技巧和信息可能是一个有用的资源。
- 虽然此模块在 Windows 上也能工作，但你应该仔细阅读官方文档以了解各种微妙的细节。例如，要在 Windows 上启动一个新进程，多进程模块实现了自己的 UNIX fork() 操作的克隆，其中进程状态通过管道复制到子进程。作为一般规则，此模块针对 UNIX 系统进行了更多优化。
- 最重要的是，尽量让事情保持简单。

#### threading

`threading` 模块提供了一个 `Thread` 类和各种同步原语，用于编写多线程程序。

##### 线程对象

`Thread` 类用于表示一个独立的控制线程。可以按如下方式创建一个新线程：

```
Thread(group=None, target=None, name=None, args=(), kwargs={})
```

这创建了一个新的 `Thread` 实例。`group` 是 `None`，为将来的扩展保留。`target` 是一个可调用对象，在线程启动时由 `run()` 方法调用。默认情况下，它是 `None`，意味着不调用任何内容。`name` 是线程名称。默认情况下，会创建一个格式为 `"Thread-N"` 的唯一名称。`args` 是传递给 `target` 函数的参数元组。`kwargs` 是传递给 `target` 的关键字参数字典。

一个 `Thread` 实例 `t` 支持以下方法和属性：

```
t.start()
```

通过在单独的控制线程中调用 `run()` 方法来启动线程。此方法只能调用一次。

```
t.run()
```

当线程启动时调用此方法。默认情况下，它调用传递给构造函数的 target 函数。此方法也可以在 `Thread` 的子类中重新定义。

```
t.join([timeout])
```

等待直到线程终止或发生超时。`timeout` 是一个浮点数，指定以秒为单位的超时时间。线程不能加入自身，在线程启动之前加入它会出错。

```
t.is_alive()
```

如果线程是活跃的则返回 `True`，否则返回 `False`。线程从 `start()` 方法返回时开始活跃，直到其 `run()` 方法终止。在旧代码中，`t.isAlive()` 是此方法的别名。

```
t.name
```

线程名称。这是一个仅用于标识的字符串，如果愿意可以更改为更有意义的值（这可能会简化调试）。在旧代码中，使用 `t.getName()` 和 `t.setName(name)` 来操作线程名称。

```
t.ident
```

整数线程标识符。如果线程尚未启动，则值为 `None`。

```
t.daemon
```

线程的布尔守护标志。必须在调用 `start()` 之前设置，初始值继承自创建线程的守护状态。当没有活跃的非守护线程时，整个 Python 程序退出。所有程序都有一个主线程，代表初始控制线程，它不是守护线程。在旧代码中，使用 `t.setDaemon(flag)` 和 `t.isDaemon()` 来操作此值。

下面是一个示例，展示如何将一个函数（或其他可调用对象）创建并启动为一个线程：

```
import threading
import time

def clock(interval):
    while True:
        print("The time is %s" % time.ctime())
        time.sleep(interval)

t = threading.Thread(target=clock, args=(15,))
t.daemon = True
t.start()
```

下面是一个示例，展示如何将同一个线程定义为类：

```
import threading
import time

class ClockThread(threading.Thread):
    def __init__(self, interval):
        threading.Thread.__init__(self)
        self.daemon = True
        self.interval = interval
    def run(self):
        while True:
            print("The time is %s" % time.ctime())
            time.sleep(self.interval)

t = ClockProcess(15)
t.start()
```

如果你将线程定义为类并定义自己的 `__init__()` 方法，如图所示调用基类构造函数 `Thread.__init__()` 是至关重要的。如果你忘记这一点，会得到一个严重的错误。除了 `run()` 之外，重新定义线程已定义的其他任何方法都是错误的。

在这些示例中设置 daemon 属性是那些将在后台永远运行的线程的常见特征。通常，Python 会在解释器退出前等待所有线程终止。然而，对于永不停止的后台任务，这种行为通常是不可取的。设置守护标志会使解释器在主程序退出后立即退出。在这种情况下，守护线程将被简单地销毁。

##### 定时器对象

Timer 对象用于在某个较晚的时间执行函数。

```
Timer(interval, func [, args [, kwargs]])
```

创建一个定时器对象，在间隔 *interval* 秒后运行函数 *func*。*args* 和 *kwargs* 提供给 *func* 的参数和关键字参数。定时器在调用 `start()` 方法之前不会启动。

一个 Timer 对象 t 具有以下方法：

```
t.start()
```

启动定时器。提供给 Timer() 的函数 func 将在指定的定时器间隔后执行。

```
t.cancel()
```

如果函数尚未执行，则取消定时器。

##### Lock 对象

原始锁（或互斥锁）是一种同步原语，其状态要么是"锁定"，要么是"未锁定"。使用 acquire() 和 release() 两种方法来更改锁的状态。如果状态是锁定的，则获取锁的尝试将被阻止，直到锁被释放。如果有多个线程在等待获取锁，则在锁被释放时只允许其中一个继续执行。等待线程继续执行的顺序是未定义的。

使用以下构造函数创建一个新的 Lock 实例：

```
Lock()
```

创建一个新的 Lock 对象，初始状态为未锁定。

一个 Lock 实例 lock 支持以下方法：

```
lock.acquire([blocking])
```

获取锁，如果必要则阻塞直到锁被释放。如果提供了 blocking 并设置为 False，则函数立即返回，如果无法获取锁则返回 False，如果锁定成功则返回 True。

```
lock.release()
```

释放锁。当锁处于未锁定状态或从不同于最初调用 acquire() 的线程调用此方法时会出错。

##### RLock

可重入锁是一种类似于 Lock 对象的同步原语，但它可以被同一线程多次获取。这允许拥有锁的线程执行嵌套的 acquire() 和 release() 操作。在这种情况下，只有最外层的 release() 操作会将锁重置为其未锁定状态。

使用以下构造函数创建一个新的 RLock 对象：

```
RLock()
```

创建一个新的可重入锁对象。一个 RLock 对象 rlock 支持以下方法：

```
rlock.acquire([blocking])
```

获取锁，如果必要则阻塞直到锁被释放。如果没有线程拥有该锁，则将其锁定并将递归级别设置为 1。如果此线程已经拥有该锁，则锁的递归级别加一，函数立即返回。
```

##### 信号量与有界信号量

*信号量*是一种基于计数器的同步原语，每次`acquire()`调用会使计数器递减，每次`release()`调用会使计数器递增。如果计数器变为零，`acquire()`方法将阻塞，直到其他线程调用`release()`。

`Semaphore([value])`

创建一个新的信号量。`value`是计数器的初始值。如果省略，则计数器默认为1。

一个`Semaphore`实例，*s*，支持以下方法：

`s.acquire([blocking])`

获取信号量。如果内部计数器在进入时大于零，此方法将其递减1并立即返回。如果为零，则此方法将阻塞，直到另一个线程调用`release()`。`blocking`参数的行为与`Lock`和`RLock`对象中描述的一致。

`s.release()`

通过将内部计数器递增1来释放信号量。如果计数器为零且另一个线程正在等待，则该线程将被唤醒。如果有多个线程在等待，则只会有一个线程从其`acquire()`调用中返回。线程释放的顺序是不确定的。

`BoundedSemaphore([value])`

创建一个新的信号量。`value`是计数器的初始值。如果省略`value`，则计数器默认为1。`BoundedSemaphore`的工作原理与`Semaphore`完全相同，只是`release()`操作的次数不能超过`acquire()`操作的次数。

信号量和互斥锁之间的一个微妙区别是，信号量可以用于信号通知。例如，`acquire()`和`release()`方法可以从不同的线程调用，以在生产者线程和消费者线程之间进行通信。

```python
produced = threading.Semaphore(0)
consumed = threading.Semaphore(1)

def producer():
    while True:
        consumed.acquire()
        produce_item()
        produced.release()

def consumer():
    while True:
        produced.acquire()
        item = get_item()
        consumed.release()
```

此示例中展示的这种信号通知通常使用条件变量来完成，条件变量将在后文描述。

##### 事件

*事件*用于在线程之间进行通信。一个线程发出"事件"信号，一个或多个其他线程等待该事件。一个`Event`实例管理一个内部标志，该标志可以通过`set()`方法设置为真，也可以通过`clear()`方法重置为假。`wait()`方法会阻塞，直到标志为真。

`Event()`

创建一个新的`Event`实例，其内部标志初始为假。一个`Event`实例，`e`，支持以下方法：

`e.is_set()`

仅当内部标志为真时才返回真。此方法在较旧的代码中称为`isSet()`。

`e.set()`

将内部标志设置为真。所有等待其变为真的线程都会被唤醒。

`e.clear()`

将内部标志重置为假。

`e.wait([timeout])`

阻塞直到内部标志为真。如果进入时内部标志已为真，则此方法立即返回。否则，它将阻塞，直到另一个线程调用`set()`将标志设置为真，或者直到可选的超时时间到达。`timeout`是一个浮点数，指定以秒为单位的超时时间。

尽管`Event`对象可以用于向其他线程发送信号，但它们不应用于实现生产者/消费者问题中典型的通知类型。例如，应避免使用如下代码：

```python
evt = Event()

def producer():
    while True:
        # produce item
        ...
        evt.signal()

def consumer():
    while True:
        # Wait for an item
        evt.wait()
        # Consume the item
        ...
        # Clear the event and wait again
        evt.clear()
```

此代码无法可靠地工作，因为生产者可能在`evt.wait()`和`evt.clear()`操作之间生产了新项目。然而，通过清除事件，这个新项目在生产者创建新项目之前不会被消费者看到。在最好的情况下，程序会出现小故障，项目的处理会被莫名延迟。在最坏的情况下，整个程序会因为丢失事件信号而挂起。对于这类问题，最好使用条件变量。

##### 条件变量

*条件变量*是一种建立在另一个锁之上的同步原语，当一个线程对特定状态变化或事件发生感兴趣时使用。一个典型的用例是生产者-消费者问题，其中一个线程生产数据供另一个线程消费。使用以下构造函数创建一个新的`Condition`实例：

`Condition([lock])`

创建一个新的条件变量。`lock`是一个可选的`Lock`或`RLock`实例。如果未提供，将创建一个新的`RLock`实例供条件变量使用。

条件变量，`cv`，支持以下方法：

`cv.acquire(*args)`

获取底层锁。此方法调用底层锁上的相应`acquire(*args)`方法并返回结果。

`cv.release()`

释放底层锁。此方法调用底层锁上的相应`release()`方法。

`cv.wait([timeout])`

等待直到被通知或超时发生。此方法在调用线程已经获取锁之后调用。调用时，底层锁被释放，线程进入休眠，直到被另一个线程在条件变量上调用`notify()`或`notifyAll()`唤醒。一旦被唤醒，线程重新获取锁，方法返回。`timeout`是一个以秒为单位的浮点数。如果超时时间到期，线程将被唤醒，重新获取锁，然后返回控制权。

`cv.notify([n])`

唤醒一个或多个等待此条件变量的线程。此方法仅在调用线程获取锁之后调用，如果没有线程等待，则不执行任何操作。`n`指定要唤醒的线程数，默认为1。被唤醒的线程在重新获取锁之前不会从`wait()`调用返回。

`cv.notify_all()`

唤醒所有等待此条件的线程。此方法在较旧的代码中称为`notifyAll()`。

这是一个使用条件变量的示例模板：

```python
cv = threading.Condition()
def producer():
    while True:
        cv.acquire()
        produce_item()
        cv.notify()
        cv.release()

def consumer():
    while True:
        cv.acquire()
        while not item_is_available():
            cv.wait()      # Wait for an item to show up
        cv.release()
        consume_item()
```

使用条件变量的一个微妙之处在于，如果有多个线程在同一个条件上等待，`notify()`操作可能唤醒其中一个或多个线程（这种行为通常取决于底层操作系统）。因此，始终存在线程唤醒后发现其关心的条件不再成立的可能性。这解释了，例如，为什么`consumer()`函数中使用了`while`循环。如果线程唤醒，但已生产的物品已经消失，它只会回到等待下一个信号的状态。

##### 使用锁时的注意事项

使用任何锁原语（如`Lock`、`RLock`或`Semaphore`）时必须格外小心。锁管理不善是死锁或竞态条件的常见来源。依赖锁的代码应始终确保锁在发生异常时也能被正确释放。典型代码如下所示：

```python
try:
    lock.acquire()
    # critical section
    statements
    ...
finally:
    lock.release()
```

或者，所有锁也支持上下文管理协议，这稍微更简洁一些：

```python
with lock:
    # critical section
    statements
    ...
```

在最后一个例子中，锁由`with`语句自动获取，并在控制流离开上下文时释放。

此外，作为一般规则，应避免编写在任何给定时间获取多个锁的代码。例如：

```python
with lock_A:
    # critical section
    statements
    ...
    with lock_B:
        # critical section on B
        statements
    ...
```

这通常是让应用程序神秘死锁的好方法。尽管有避免这种情况的策略（例如，分层锁），但通常最好编写完全避免这种情况的代码。

`rlock.release()`

通过递减其递归级别来释放锁。如果递减后递归级别为零，则锁将重置为未锁定状态。否则，锁保持锁定状态。此函数只能由当前拥有锁的线程调用。



##### 线程的终止与挂起

线程没有任何强制终止或挂起的方法。这一省略是经过深思熟虑的，源于编写多线程程序固有的复杂性。例如，如果一个线程已经获取了锁，在它释放锁之前强制终止或挂起它，可能会导致整个应用程序死锁。此外，通常也无法简单地在终止时"释放所有锁"，因为复杂的线程同步往往涉及必须按非常精确的顺序执行才能正常工作的加锁和解锁操作。

如果你想支持终止或挂起功能，需要自行构建这些特性。通常的做法是让线程在一个循环中运行，定期检查其状态以判断是否应该终止。例如：

```python
class StoppableThread(threading.Thread):
    def __init__(self):
        threading.Thread.__init__(self)
        self._terminate = False
        self._suspend_lock = threading.Lock()
    def terminate(self):
        self._terminate = True
    def suspend(self):
        self._suspend_lock.acquire()
    def resume(self):
        self._suspend_lock.release()
    def run(self):
        while True:
            if self._terminate:
                break
            self._suspend_lock.acquire()
            self._suspend_lock.release()
            statements
            ...
```

请记住，要使这种方法可靠地工作，线程应格外注意不要执行任何类型的阻塞 I/O 操作。例如，如果线程阻塞等待数据到达，它在从该操作中唤醒之前不会终止。因此，你可能需要让实现使用超时、非阻塞 I/O 和其他高级特性，以确保终止检查能够定期执行。

##### 实用函数

以下实用函数可用：

**active_count()**

返回当前活跃的 Thread 对象的数量。

**current_thread()**

返回与调用者控制线程对应的 Thread 对象。

**enumerate()**

返回当前所有活跃的 Thread 对象的列表。

**local()**

返回一个本地对象，允许存储线程本地数据。该对象在每个线程中保证是唯一的。

**setprofile(func)**

设置一个分析函数，该函数将用于所有创建的线程。在每个线程开始运行之前，func 会传递给 `sys.setprofile()`。

**settrace(func)**

设置一个跟踪函数，该函数将用于所有创建的线程。在每个线程开始运行之前，func 会传递给 `sys.settrace()`。

**stack_size([size])**

返回创建新线程时使用的栈大小。如果给出了可选的整数 size，则设置用于创建新线程的栈大小。为了最大的可移植性，size 可以是 32768（32KB）或更大的值，并且必须是 4096（4KB）的倍数。如果系统不支持此操作，将引发 ThreadError 异常。

##### 全局解释器锁

Python 解释器受到一个锁的保护，即使有多个处理器可用，也只允许一个线程在任意时刻执行。这严重限制了线程在计算密集型程序中的实用性——事实上，使用线程通常会导致 CPU 密集型程序的运行性能明显低于顺序执行相同工作的程序。因此，线程应该真正只用于主要关注 I/O 的程序，例如网络服务器。对于更计算密集型的任务，可以考虑使用 C 扩展模块或 multiprocessing 模块来替代。C 扩展可以选择释放解释器锁并并行运行，前提是它们在锁释放期间不与解释器交互。multiprocessing 模块将工作分配给不受锁限制的独立子进程。

##### 使用线程编程

虽然可以在 Python 中使用各种锁和同步原语的组合来编写非常传统的多线程程序，但有一种编程风格被推荐优先采用——那就是尝试将多线程程序组织为通过消息队列通信的独立任务集合。这将在下一节（queue 模块）中进行描述，并附有示例。

#### queue, Queue

queue 模块（在 Python 2 中命名为 Queue）实现了多种多生产者、多消费者队列，可用于在多个执行线程之间安全地交换信息。

queue 模块定义了三个不同的队列类：

**Queue([maxsize])**

创建一个 FIFO（先进先出）队列。maxsize 是可以放入队列中的最大项目数。如果 maxsize 被省略或为 0，则队列大小为无限。

**LifoQueue([maxsize])**

创建一个 LIFO（后进先出）队列（也称为栈）。

**PriorityQueue([maxsize])**

创建一个优先级队列，其中项目按优先级从低到高排列。使用此队列时，项目应为 `(priority, data)` 形式的元组，其中 `priority` 是一个数字。

任何队列类的实例 `q` 具有以下方法：

**q.qsize()**

返回队列的大致大小。由于其他线程可能正在更新队列，此数字并非完全可靠。

**q.empty()**

如果队列为空则返回 `True`，否则返回 `False`。

**q.full()**

如果队列已满则返回 `True`，否则返回 `False`。

**q.put(item [, block [, timeout]])**

将 `item` 放入队列。如果可选参数 `block` 为 `True`（默认值），调用者将阻塞直到有可用空位。否则（`block` 为 `False`），如果队列已满则引发 `Full` 异常。`timeout` 提供以秒为单位的可选超时值。如果发生超时，将引发 `Full` 异常。

**q.put_nowait(item)**

等价于 `q.put(item, False)`。

**q.get([block [, timeout]])**

从队列中移除并返回一个项目。如果可选参数 `block` 为 `True`（默认值），调用者将阻塞直到有可用项目。否则（`block` 为 `False`），如果队列为空则引发 `Empty` 异常。`timeout` 提供以秒为单位的可选超时值。如果发生超时，将引发 `Empty` 异常。

**q.get_nowait()**

等价于 `get(0)`。

**q.task_done()**

由队列数据的消费者使用，用于指示某个项目的处理已完成。如果使用此方法，应为从队列中移除的每个项目调用一次。

**q.join()**

阻塞直到队列上的所有项目都被移除并处理完毕。只有在为放入队列的每个项目都调用了 `q.task_done()` 之后，此方法才会返回。

##### 使用队列的线程示例

多线程程序通常通过使用队列来简化。例如，线程可以使用共享队列连接在一起，而不是依赖必须通过锁保护的共享状态。在这种模型中，工作线程通常作为数据的消费者运行。以下是一个说明该概念的示例：

```python
import threading
from queue import Queue  # Use from Queue on Python 2

class WorkerThread(threading.Thread):
    def __init__(self, *args, **kwargs):
        threading.Thread.__init__(self, *args, **kwargs)
        self.input_queue = Queue()

    def send(self, item):
        self.input_queue.put(item)

    def close(self):
        self.input_queue.put(None)
        self.input_queue.join()

    def run(self):
        while True:
            item = self.input_queue.get()
            if item is None:
                break
            # Process the item (replace with useful work)
            print(item)
            self.input_queue.task_done()
        # Done. Indicate that sentinel was received and return
        self.input_queue.task_done()
        return

##### Example use
w = WorkerThread()
w.start()
w.send("hello")      # Send items to the worker (via queue)
w.send("world")
w.close()
```

该类的设计经过了精心考量。首先，你会注意到编程 API 是 multiprocessing 模块中由管道创建的 Connection 对象的子集。这为未来的扩展提供了可能。例如，工作者可以在不破坏发送数据的代码的情况下，迁移到独立的进程中。

其次，编程接口支持线程终止。`close()` 方法将一个哨兵值放入队列，当该值被处理时，线程就会关闭。

最后，编程 API 也几乎与协程相同。如果要执行的工作不涉及任何阻塞操作，你可以将 `run()` 方法重新实现为协程，从而完全省去线程。后一种方式可能运行得更快，因为不再有线程上下文切换的开销。

#### 协程与微线程

在某些类型的应用程序中，可以使用任务调度器和一组生成器或协程来实现协作式的用户空间多线程。这有时被称为微线程，尽管术语各不相同——有时在任务片段（tasklets）、绿色线程（green threads）、greenlets 等上下文中描述。这种技术的一个常见用途是在需要管理大量打开的文件或套接字的程序中。例如，一个需要同时管理 1,000 个客户端连接的网络服务器。不需要创建 1,000 个线程来完成此任务，而是使用异步 I/O 或轮询（使用 select 模块）结合一个处理 I/O 事件的任务调度器。



驱动这种编程技术的底层概念是，生成器或协程函数中的 `yield` 语句会暂停函数的执行，直到后续通过 `next()` 或 `send()` 操作恢复。这使得一组生成器函数之间使用调度循环进行协作式多任务成为可能。下面是一个说明该思想的示例：

```python
def foo():
    for n in xrange(5):
        print("I'm foo %d" % n)
    yield

def bar():
    for n in xrange(10):
        print("I'm bar %d" % n)
    yield

def spam():
    for n in xrange(7):
        print("I'm spam %d" % n)
    yield

# 创建并填充任务队列
from collections import deque
taskqueue = deque()
taskqueue.append(foo())              # 添加一些任务（生成器）
taskqueue.append(bar())
taskqueue.append(spam())

# 运行所有任务
while taskqueue:
    # 获取下一个任务
    task = taskqueue.pop()
    try:
        # 运行直到下一个 yield 并将任务重新入队
        next(task)
        taskqueue.appendleft(task)
    except StopIteration:
        # 任务完成
        pass
```

程序很少像这样定义一系列 CPU 密集型协程并进行调度。相反，你更可能看到此技术用于 I/O 密集型任务、轮询或事件处理。一个展示此技术的高级示例可在第 21 章 "网络编程与套接字" 的 select 模块部分找到。

#### 网络编程与套接字

本章描述用于实现底层网络服务器和客户端的模块。Python 提供了广泛的网络支持，从直接使用套接字编程到处理诸如 HTTP 等高级应用协议。首先，本文将对网络编程进行一个非常简短（且公认简略）的介绍。读者可参考 W. Richard Stevens 所著的 *UNIX Network Programming, Volume 1: Networking APIs: Sockets and XTI* （Prentice Hall，1997，ISBN 0-13-490012-X）一书以了解许多高级细节。第 22 章 "互联网应用编程" 描述了与应用层协议相关的模块。

##### 网络编程基础

Python 的网络编程模块主要支持两种互联网协议：TCP 和 UDP。*TCP 协议* 是一种可靠的、面向连接的协议，用于在机器之间建立双向通信流。*UDP* 是一种更低级的基于数据包的协议（无连接），机器在此协议中发送和接收离散的数据包信息，而无需正式建立连接。与 TCP 不同，UDP 通信不可靠，因此在需要可靠通信的应用中管理起来本质上更加复杂。因此，大多数互联网应用都使用 TCP 连接。

两种网络协议都通过一种称为套接字的编程抽象来处理。*套接字* 是一种类似于文件的对象，它允许程序接受传入连接、发起传出连接以及发送和接收数据。两台机器通信之前，双方都必须创建一个套接字对象。

接收连接的机器（服务器）必须将其套接字对象绑定到一个已知的端口号。*端口* 是一个范围在 0-65535 的 16 位数字，由操作系统管理，客户端使用它来唯一标识服务器。端口 0-1023 由系统保留，并被常用网络协议使用。下表列出了几个常见协议的端口分配（更完整的列表可在 http://www.iana.org/assignments/port-numbers 找到）：

| 服务 | 端口号 |
|---------|-------------|
| FTP-数据 | 20 |
| FTP-控制 | 21 |
| SSH | 22 |
| Telnet | 23 |
| SMTP (邮件) | 25 |
| HTTP (万维网) | 80 |
| POP3 | 110 |
| IMAP | 143 |
| HTTPS (安全万维网) | 443 |

建立 TCP 连接的过程涉及服务器和客户端的一系列精确步骤，如图 21.1 所示。

![TCP 连接协议。](img/bca8f1caf434b36cbe69cddbca7c9f52_474_0.png)

**图 21.1** TCP 连接协议。

对于 TCP 服务器，用于接收连接的套接字对象与用于与客户端进行后续通信的套接字不是同一个。具体来说，`accept()` 系统调用返回一个新的套接字对象，该对象实际用于连接。这允许服务器同时管理来自大量客户端的连接。

UDP 通信以类似的方式执行，只是客户端和服务器之间不建立 "连接"，如图 21.2 所示。

![UDP 通信。](img/bca8f1caf434b36cbe69cddbca7c9f52_475_0.png)

下面的示例使用 socket 模块编写的客户端和服务器来说明 TCP 协议。在此示例中，服务器只是将当前时间作为字符串返回给客户端。

```python
# 时间服务器程序
from socket import *
import time

s = socket(AF_INET, SOCK_STREAM)  # 创建一个 TCP 套接字
s.bind(('',8888))                   # 绑定到端口 8888
s.listen(5)                         # 监听，但允许不超过
                                    # 5 个待处理连接。

while True:
    client,addr = s.accept()    # 获取一个连接
    print("Got a connection from %s" % str(addr))
    timestr = time.ctime(time.time()) + "\r\n"
    client.send(timestr.encode('ascii'))
    client.close()
```

这是客户端程序：

```python
# 时间客户端程序
from socket import *
s = socket(AF_INET,SOCK_STREAM)  # 创建一个 TCP 套接字
s.connect(('localhost', 8888))   # 连接到服务器
tm = s.recv(1024)                # 接收不超过 1024 字节
s.close()
print("The time is %s" % tm.decode('ascii'))
```

建立 UDP 连接的示例将在本章后面的 socket 模块部分出现。

网络协议通常以文本形式交换数据。然而，需要非常注意文本编码。在 Python 3 中，所有字符串都是 Unicode。因此，如果要通过网络发送任何类型的文本字符串，就需要对其进行编码。这就是为什么服务器在其传输的数据上使用 `encode('ascii')` 方法。同样，当客户端接收到网络数据时，该数据首先作为原始未编码的字节接收。如果你将其打印出来或尝试将其作为文本处理，很可能得不到预期的结果。相反，你需要先对其进行解码。这就是为什么客户端代码在结果上使用 `decode('ascii')`。

本章的其余部分描述了与套接字编程相关的模块。第 22 章描述了提供对各种互联网应用程序（如电子邮件和 Web）支持的高级模块。

##### asynchat

asynchat 模块简化了使用 asyncore 模块实现异步网络应用程序的实现。它通过将 asyncore 的底层 I/O 功能包装在一个更高级的编程接口中来实现这一点，该接口专为基于简单请求/响应机制的网络协议（例如 HTTP）设计。

要使用此模块，你必须定义一个继承自 `async_chat` 的类。在此类中，你必须定义两个方法：`collect_incoming_data()` 和 `found_terminator()`。第一个方法在网络连接上接收到数据时被调用。通常，它只是获取数据并将其存储在某处。`found_terminator()` 方法在检测到请求结束时被调用。例如，在 HTTP 中，请求以空行终止。

对于数据输出，`async_chat` 维护一个生产者 FIFO 队列。如果你需要输出数据，只需将其添加到此队列中即可。然后，只要网络连接上可以进行写操作，就会透明地从该队列中取出数据。

```
async_chat([sock])
```

用于定义新处理程序的基类。`async_chat` 继承自 `asyncore.dispatcher` 并提供相同的方法。`sock` 是一个用于通信的套接字对象。

`async_chat` 的实例 `a` 具有以下方法，这些方法是 `asyncore.dispatcher` 基类已提供方法之外的额外方法：

```
a.close_when_done()
```

通过向生产者 FIFO 队列推送 `None` 来发出出数据流结束信号。当写入器到达此 `None` 时，通道将被关闭。

```
a.collect_incoming_data(data)
```

每当在通道上接收到数据时调用。`data` 是接收到的数据，通常被存储以供后续处理。此方法必须由用户实现。

```
a.discard_buffers()
```

丢弃输入/输出缓冲区和生产者 FIFO 队列中持有的所有数据。



##### asynchat

###### `a.found_terminator()`

当 `set_terminator()` 设置的终止条件满足时被调用。此方法必须由用户实现。通常，它会处理之前通过 `collect_incoming_data()` 方法收集的数据。

###### `a.get_terminator()`

返回通道的终止符。

###### `a.push(data)`

将数据推入通道的出站生产者 FIFO 队列。`data` 是一个包含待发送数据的字符串。

###### `a.push_with_producer(producer)`

将一个生产者对象 `producer` 推入生产者 FIFO 队列。`producer` 可以是任何具有 `more()` 简单方法的对象。`more()` 方法每次被调用时都应生成一个字符串。返回空字符串表示数据结束。在内部，`async_chat` 类反复调用 `more()` 来获取要写入出站通道的数据。可以通过反复调用 `push_with_producer()` 将多个生产者对象推入 FIFO 队列。

###### `s.set_terminator(term)`

设置通道的终止条件。`term` 可以是字符串、整数或 `None`。如果 `term` 是字符串，则当该字符串出现在输入流中时会调用 `found_terminator()` 方法。如果 `term` 是整数，则指定字节计数。在读取该数量的字节后，将调用 `found_terminator()`。如果 `term` 是 `None`，则会持续收集数据。

该模块定义了一个可以为 `a.push_with_producer()` 方法生成数据的类。

###### `simple_producer(data [, buffer_size])`

创建一个简单的生产者对象，从字节字符串 `data` 中生成数据块。`buffer_size` 指定块大小，默认值为 512。

`asynchat` 模块始终与 `asyncore` 模块配合使用。例如，`asyncore` 用于设置高级服务器以接受传入连接。然后 `asynchat` 用于实现每个连接的处理程序。以下示例通过实现一个处理 GET 请求的极简 Web 服务器来展示其工作原理。该示例省略了很多错误检查和细节，但应足以让你入门。读者应将此示例与下一个将要介绍的 `asyncore` 模块中的示例进行比较。

```python
# An asynchronous HTTP server using asynchat
import asynchat, asyncore, socket
import os
import mimetypes
try:
    from http.client import responses      # Python 3
except ImportError:
    from httplib import responses          # Python 2

# This class plugs into the asyncore module and merely handles accept events
class async_http(asyncore.dispatcher):
    def __init__(self,port):
        asyncore.dispatcher.__init__(self)
        self.create_socket(socket.AF_INET,socket.SOCK_STREAM)
        self.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.bind(('',port))
        self.listen(5)

    def handle_accept(self):
        client,addr = self.accept()
        return async_http_handler(client)

# Class that handles asynchronous HTTP requests.
class async_http_handler(asynchat.async_chat):
    def __init__(self,conn=None):
        asynchat.async_chat.__init__(self,conn)
        self.data = []
        self.got_header = False
        self.set_terminator(b"\r\n\r\n")

    # Get incoming data and append to data buffer
    def collect_incoming_data(self,data):
        if not self.got_header:
            self.data.append(data)

    # Got a terminator (the blank line)
    def found_terminator(self):
        self.got_header = True
        header_data    = b"".join(self.data)
        # Decode header data (binary) into text for further processing
        header_text    = header_data.decode('latin-1')
        header_lines   = header_text.splitlines()
        request        = header_lines[0].split()
        op             = request[0]
        url            = request[1][1:]
        self.process_request(op,url)

    # Push text onto the outgoing stream, but encode it first
    def push_text(self,text):
        self.push(text.encode('latin-1'))

    # Process the request
    def process_request(self, op, url):
        if op == "GET":
            if not os.path.exists(url):
                self.send_error(404,"File %s not found\r\n")
            else:
                type, encoding = mimetypes.guess_type(url)
                size = os.path.getsize(url)
                self.push_text("HTTP/1.0 200 OK\r\n")
                self.push_text("Content-length: %s\r\n" % size)
                self.push_text("Content-type: %s\r\n" % type)
                self.push_text("\r\n")
                self.push_with_producer(file_producer(url))
        else:
            self.send_error(501,"%s method not implemented" % op)
        self.close_when_done()

# Error handling
def send_error(self,code,message):
    self.push_text("HTTP/1.0 %s %s\r\n" % (code, responses[code]))
    self.push_text("Content-type: text/plain\r\n")
    self.push_text("\r\n")
    self.push_text(message)

class file_producer(object):
    def __init__(self,filename,buffer_size=512):
        self.f = open(filename,"rb")
        self.buffer_size = buffer_size
    def more(self):
        data = self.f.read(self.buffer_size)
        if not data:
            self.f.close()
        return data

a = async_http(8080)
asyncore.loop()
```

要测试此示例，你需要提供一个与服务器运行目录中文件对应的 URL。

#### asyncore

`asyncore` 模块用于构建网络应用程序，其中网络活动以一系列事件的形式异步处理，这些事件由使用 `select()` 系统调用构建的事件循环进行分发。这种方法适用于希望提供并发性但不使用线程或进程的网络程序。此方法还可以为短事务提供高性能。该模块的所有功能都由 `dispatcher` 类提供，它是对普通套接字对象的轻量级封装。

##### `dispatcher([sock])`

定义事件驱动非阻塞套接字对象的基类。`sock` 是一个现有的套接字对象。如果省略，则必须使用 `create_socket()` 方法（稍后描述）创建套接字。创建后，网络事件由特殊的处理方法处理。此外，所有打开的 `dispatcher` 对象都保存在一个内部列表中，供多个轮询函数使用。

`dispatcher` 类的以下方法用于处理网络事件。它们应在派生自 `dispatcher` 的类中定义。

###### `d.handle_accept()`

当新连接到达时在监听套接字上被调用。

###### `d.handle_close()`

当套接字关闭时被调用。

###### `d.handle_connect()`

当连接建立时被调用。

###### `d.handle_error()`

当发生未捕获的 Python 异常时被调用。

###### `d.handle_expt()`

当收到套接字的带外数据时被调用。

###### `d.handle_read()`

当套接字有新数据可读时被调用。

###### `d.handle_write()`

当尝试写入数据时被调用。

###### `d.readable()`

此函数被 `select()` 循环使用，以查看对象是否愿意读取数据。如果愿意返回 `True`，否则返回 `False`。此方法被调用以确定是否应调用 `handle_read()` 方法并传入新数据。

###### `d.writable()`

被 `select()` 循环调用以查看对象是否想要写入数据。如果想要返回 `True`，否则返回 `False`。此方法始终被调用以确定是否应调用 `handle_write()` 方法来产生输出。

除了上述方法之外，以下方法用于执行低级套接字操作。它们与套接字对象上可用的方法类似。

###### `d.accept()`

接受一个连接。返回一个 `(client, addr)` 对，其中 `client` 是用于在连接上发送和接收数据的套接字对象，`addr` 是客户端的地址。

###### `d.bind(address)`

将套接字绑定到 *address*。*address* 通常是元组 `(host, port)`，但这取决于所使用的地址族。

###### `d.close()`

关闭套接字。

###### `d.connect(address)`

建立连接。*address* 是元组 `(host, port)`。

###### `d.create_socket(family, type)`

创建一个新套接字。参数与 `socket.socket()` 相同。

###### `d.listen([backlog])`

监听传入连接。*backlog* 是一个整数，传递给底层的 `socket.listen()` 函数。

###### `d.recv(size)`

最多接收 *size* 字节。空字符串表示客户端已关闭通道。

###### `d.send(data)`

发送数据。*data* 是一个字节字符串。



以下函数用于启动事件循环并处理事件：

```
loop([timeout [, use_poll [, map [, count]]]])
```

无限轮询事件。除非 `use_poll` 参数为 `True`（此时使用 `poll()` 代替），否则使用 `select()` 函数进行轮询。`timeout` 是超时时间，默认设置为 30 秒。`map` 是一个包含所有待监控通道的字典。`count` 指定在返回之前执行多少次轮询操作。如果 `count` 为 `None`（默认值），`loop()` 将永远轮询，直到所有通道关闭。如果 `count` 为 1，函数将只执行一次事件轮询后返回。

##### 示例

以下示例使用 asyncore 实现了一个极简 Web 服务器。它实现了两个类——asynhttp 用于接受连接，asynclient 用于处理客户端请求。应将其与 asynchat 模块中的示例进行比较。主要区别在于此示例在某种程度上更加底层——需要我们关注将输入流分解为行、缓冲多余数据，以及识别终止请求头的空行。

```
# An asynchronous HTTP server
import asyncore, socket
import os
import mimetypes
import collections
try:
    from http.client import responses    # Python 3
except ImportError:
    from httplib import responses        # Python 2

# This class merely handles accept events
class async_http(asyncore.dispatcher):
    def __init__(self,port):
        asyncore.dispatcher.__init__(self)
        self.create_socket(socket.AF_INET,socket.SOCK_STREAM)
        self.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.bind(('',port))
        self.listen(5)

    def handle_accept(self):
        client,addr = self.accept()
        return async_http_handler(client)

# Handle clients
class async_http_handler(asyncore.dispatcher):
    def __init__(self, sock = None):
        asyncore.dispatcher.__init__(self,sock)
        self.got_request   = False            # Read HTTP request?
        self.request_data  = b""
        self.write_queue   = collections.deque()
        self.responding    = False

    # Only readable if request header not read
    def readable(self):
        return not self.got_request

# Read incoming request data
def handle_read(self):
    chunk = self.recv(8192)
    self.request_data += chunk
    if b'\r\n\r\n' in self.request_data:
        self.handle_request()

# Handle an incoming request
def handle_request(self):
    self.got_request = True
    header_data  = self.request_data[:self.request_data.find(b'\r\n\r\n')]
    header_text  = header_data.decode('latin-1')
    header_lines = header_text.splitlines()
    request      = header_lines[0].split()
    op           = request[0]
    url          = request[1][1:]
    self.process_request(op,url)

# Process the request
def process_request(self,op,url):
    self.responding = True
    if op == "GET":
        if not os.path.exists(url):
            self.send_error(404,"File %s not found\r\n" % url)
        else:
            type, encoding = mimetypes.guess_type(url)
            size = os.path.getsize(url)
            self.push_text('HTTP/1.0 200 OK\r\n')
            self.push_text('Content-length: %d\r\n' % size)
            self.push_text('Content-type: %s\r\n' % type)
            self.push_text('\r\n')
            self.push(open(url,"rb").read())
    else:
        self.send_error(501,"%s method not implemented" % self.op)

# Error handling
def send_error(self,code,message):
    self.push_text('HTTP/1.0 %s %s\r\n' % (code, responses[code]))
    self.push_text('Content-type: text/plain\r\n')
    self.push_text('\r\n')
    self.push_text(message)

# Add binary data to the output queue
def push(self,data):
    self.write_queue.append(data)

# Add text data to the output queue
def push_text(self,text):
    self.push(text.encode('latin-1'))

# Only writable if a response is ready
def writable(self):
    return self.responding and self.write_queue

# Write response data
def handle_write(self):
    chunk = self.write_queue.popleft()
    bytes_sent = self.send(chunk)
    if bytes_sent != len(chunk):
        self.write_queue.appendleft(chunk[bytes_sent:])
    if not self.write_queue:
        self.close()

# Create the server
a = async_http(8080)
# Poll forever
asyncore.loop()
```

> **另请参阅：**
socket（第 469 页）、select（第 459 页）、http（第 500 页）、SocketServer（第 489 页）

#### select

`select` 模块提供对 `select()` 和 `poll()` 系统调用的访问。`select()` 通常用于实现轮询，或在不使用线程或子进程的情况下对多个输入/输出流进行多路复用处理。在 UNIX 上，它适用于文件、套接字、管道以及大多数其他文件类型。在 Windows 上，它仅适用于套接字。

```
select(iwtd, owtd, ewtd [, timeout])
```

查询一组文件描述符的输入、输出和异常状态。前三个参数是包含整数文件描述符或具有 `fileno()` 方法的对象的列表，该方法可用于返回文件描述符。`iwtd` 参数指定等待输入的对象，`owtd` 指定等待输出的对象，`ewtd` 指定等待异常条件的对象。每个列表可以为空。`timeout` 是一个浮点数，指定以秒为单位的超时时间。如果省略 `timeout`，函数将等待直到至少一个文件描述符就绪。如果值为 0，函数仅执行一次轮询并立即返回。返回值是一个包含就绪对象的列表元组。这些是前三个参数的子集。如果在超时之前没有对象就绪，则返回三个空列表。如果发生错误，将引发 `select.error` 异常。其值与 `IOError` 和 `OSError` 返回的值相同。

```
poll()
```

创建一个利用 `poll()` 系统调用的轮询对象。这仅在支持 `poll()` 的系统上可用。

由 `poll()` 返回的轮询对象 p 支持以下方法：

```
p.register(fd [, eventmask])
```

注册一个新的文件描述符 `fd`。`fd` 可以是整数文件描述符，也可以是提供 `fileno()` 方法的对象，通过该方法可获取描述符。`eventmask` 是以下标志的按位或运算结果，用于指示感兴趣的事件：

| 常量 | 描述 |
| --- | --- |
| POLLIN | 有数据可供读取。 |
| POLLPRI | 有紧急数据可供读取。 |
| POLLOUT | 已准备好写入。 |
| POLLERR | 错误条件。 |
| POLLHUP | 挂起。 |
| POLLNVAL | 无效请求。 |

如果省略 *eventmask*，则检查 POLLIN、POLLPRI 和 POLLOUT 事件。

```
p.unregister(fd)
```

从轮询对象中移除文件描述符 *fd*。如果文件未注册，则引发 `KeyError`。

```
p.poll([timeout])
```

对所有已注册的文件描述符进行事件轮询。*timeout* 是可选的超时时间，以毫秒为单位。返回一个 `(fd, event)` 元组列表，其中 *fd* 是文件描述符，*event* 是指示事件的位掩码。该位掩码的各位对应于 POLLIN、POLLOUT 等常量。例如，要检查 POLLIN 事件，只需使用 `event & POLLIN` 测试该值即可。如果返回空列表，则表示发生了超时且没有事件发生。

##### 高级模块功能

`select()` 和 `poll()` 函数是本模块中最具通用可移植性的函数。在 Linux 系统上，`select` 模块还提供对边缘触发和电平触发轮询（epoll）接口的访问，这可以提供显著更好的性能。在 BSD 系统上，提供了对内核队列和事件对象的访问。这些编程接口在 `select` 的在线文档 http://docs.python.org/library/select 中有描述。

##### 高级异步 I/O 示例

`select` 模块有时用于实现基于任务协程或协程的服务器——这是一种无需线程或进程即可提供并发执行的技术。以下高级示例通过实现一个基于 I/O 的协程任务调度器来说明这一概念。请注意——这是本书中最高级的示例，需要花一些时间研究才能理解。你也可以参考我的 PyCON'09 教程《协程与并发的奇妙之旅》(http://www.dabeaz.com/coroutines) 以获取更多参考资料。

```
import select
import types
import collections
```



## 第21章 网络编程与套接字

# 表示运行中任务的对象
class Task(object):
    def __init__(self,target):
        self.target  = target     # 一个协程
        self.sendval = None       # 恢复时发送的值
        self.stack   = []         # 调用栈
    def run(self):
        try:
            result = self.target.send(self.sendval)
            if isinstance(result,SystemCall):
                return result
            if isinstance(result,types.GeneratorType):
                self.stack.append(self.target)
                self.sendval = None
                self.target = result
            else:
                if not self.stack: return
                self.sendval = result
                self.target = self.stack.pop()
        except StopIteration:
            if not self.stack: raise
            self.sendval = None
            self.target = self.stack.pop()

# 表示“系统调用”的对象
class SystemCall(object):
    def handle(self,sched,task):
        pass

# 调度器对象
class Scheduler(object):
    def __init__(self):
        self.task_queue   = collections.deque()
        self.read_waiting = {}
        self.write_waiting = {}
        self.numtasks     = 0

    # 从协程创建一个新任务
    def new(self,target):
        newtask = Task(target)
        self.schedule(newtask)
        self.numtasks += 1

    # 将任务放入任务队列
    def schedule(self,task):
        self.task_queue.append(task)

    # 让任务等待文件描述符上的数据读取
    def readwait(self,task,fd):
        self.read_waiting[fd] = task

    # 让任务等待文件描述符上的数据写入
    def writewait(self,task,fd):
        self.write_waiting[fd] = task

    # 主调度器循环
    def mainloop(self,count=-1,timeout=None):
        while self.numtasks:
            # 检查需要处理的 I/O 事件
            if self.read_waiting or self.write_waiting:
                wait = 0 if self.task_queue else timeout
                r,w,e = select.select(self.read_waiting, self.write_waiting, [],
                                      wait)
                for fileno in r:
                    self.schedule(self.read_waiting.pop(fileno))
                for fileno in w:
                    self.schedule(self.write_waiting.pop(fileno))

            # 运行队列中所有准备就绪的任务
            while self.task_queue:
                task = self.task_queue.popleft()
                try:
                    result = task.run()
                    if isinstance(result,SystemCall):
                        result.handle(self,task)
                    else:
                        self.schedule(task)
                except StopIteration:
                    self.numtasks -= 1

            # 如果没有任务可以运行，我们决定是等待还是返回
            else:
                if count > 0: count -= 1
                if count == 0:
                    return

# 不同系统调用的实现
class ReadWait(SystemCall):
    def __init__(self,f):
        self.f = f
    def handle(self,sched,task):
        fileno = self.f.fileno()
        sched.readwait(task,fileno)

class WriteWait(SystemCall):
    def __init__(self,f):
        self.f = f
    def handle(self,sched,task):
        fileno = self.f.fileno()
        sched.writewait(task,fileno)

class NewTask(SystemCall):
    def __init__(self,target):
        self.target = target
    def handle(self,sched,task):
        sched.new(self.target)
        sched.schedule(task)

本示例中的代码实现了一个非常微小的“操作系统”。以下是关于其运作的一些细节：

-   所有工作都由协程函数完成。回想一下，协程使用 `yield` 语句的方式类似于生成器，但不同之处在于，你不是在迭代它，而是使用 `send(value)` 方法向其发送值。

-   `Task` 类代表一个正在运行的任务，它只是协程之上的一层薄封装。`Task` 对象 `task` 只有一个操作：`task.run()`。这会恢复任务并运行它，直到遇到下一个 `yield` 语句，此时任务挂起。运行任务时，`task.sendval` 属性包含要发送到任务相应 `yield` 表达式的值。任务会一直运行，直到遇到下一个 `yield` 语句。这个 `yield` 产生的值控制任务接下来发生什么：

    -   如果值是另一个协程（`types.GeneratorType`），意味着任务希望暂时将控制权转移给该协程。当发生这种情况时，`Task` 对象的 `stack` 属性代表一个协程的调用栈。下次任务运行时，控制权将转移到这个新协程。
    -   如果值是一个 `SystemCall` 实例，意味着任务希望调度器代其执行某些操作（如启动新任务、等待 I/O 等）。该对象的目的稍后描述。
    -   如果值是任何其他值，则会发生两种情况之一。如果当前执行的协程是作为子例程运行的，它将从任务调用栈中弹出，并保存该值以便可以发送给调用者。调用者将在任务下一次执行时收到此值。如果该协程是唯一执行的协程，则返回值将被简单丢弃。
    -   `StopIteration` 的处理是针对已终止的协程。当这种情况发生时，控制权返回给先前的协程（如果有的话），或者异常传播给调度器，以便调度器知道任务已终止。

-   `SystemCall` 类代表调度器中的系统调用。当一个运行中的任务希望调度器代其执行操作时，它会 `yield` 一个 `SystemCall` 实例。这个对象被称为“系统调用”，因为它模拟了程序如何请求真正的多任务操作系统（如 UNIX 或 Windows）服务的行为。特别是，如果程序想要操作系统的服务，它会 `yield` 控制权并提供一些信息给系统，以便系统知道该怎么做。在这方面，`yield` 一个 `SystemCall` 类似于执行一种系统“陷阱”。

-   `Scheduler` 类代表正在管理的 `Task` 对象集合。其核心是围绕一个任务队列（`task_queue` 属性）构建的，该队列跟踪准备运行的任务。关于任务队列有四个基本操作。`new()` 接受一个新协程，用 `Task` 对象包装它，并将其放入工作队列。`schedule()` 接受一个现有的 `Task` 并将其放回工作队列。`mainloop()` 循环运行调度器，逐个处理任务，直到没有更多任务。`readwait()` 和 `writewait()` 方法将 `Task` 对象放入临时暂存区，在那里等待 I/O 事件。在这种情况下，`Task` 没有运行，但它也没有死亡——它只是在那里等待时机。

-   `mainloop()` 方法是调度器的核心。此方法首先检查是否有任务正在等待 I/O 事件。如果有，它会安排调用 `select()` 以轮询 I/O 活动。如果有任何感兴趣的事件，相关的任务将被放回任务队列，以便它们可以运行。接下来，`mainloop()` 方法从任务队列中弹出任务并调用它们的 `run()` 方法。如果任何任务退出（`StopIteration`），它将被丢弃。如果任务只是 `yield`，它将被放回任务队列，以便它可以再次运行。这会一直持续到没有更多任务或所有任务都阻塞并等待更多 I/O 事件。作为一个选项，`mainloop()` 函数接受一个 `count` 参数，可用于使其在指定数量的 I/O 轮询操作后返回。如果调度器要集成到另一个事件循环中，这可能很有用。

-   也许调度器最微妙的地方是在 `mainloop()` 方法中处理 `SystemCall` 实例。如果任务 `yield` 一个 `SystemCall` 实例，调度器将调用其 `handle()` 方法，并将相关的 `Scheduler` 和 `Task` 对象作为参数传入。系统调用的目的是执行某种关于任务或调度器本身的操作。`ReadWait()`、`WriteWait()` 和 `NewTask()` 类是暂停任务进行 I/O 或创建新任务的系统调用示例。例如，`ReadWait()` 接受一个任务并在调度器上调用 `readwait()` 方法。然后调度器将该任务放入适当的等待区域。再次强调，这里存在一个关键的对象解耦。任务 `yield` `SystemCall` 对象以请求服务，但不直接与调度器交互。反过来，`SystemCall` 对象可以对任务和调度器执行操作，但不与任何特定的调度器或任务实现绑定。因此，理论上，你可以编写一个完全不同的调度器实现（也许使用线程），它可以插入到这个整个框架中，并且它仍然可以工作。

以下是使用此 I/O 任务调度器实现的简单网络时间服务器示例。它将阐明前面列表中描述的许多概念：

```
from socket import socket, AF_INET, SOCK_STREAM
def time_server(address):
    import time
    s = socket(AF_INET,SOCK_STREAM)
    s.bind(address)
    s.listen(5)
    while True:
        yield ReadWait(s)
        conn,addr = s.accept()
        print("Connection from %s" % str(addr))
        yield WriteWait(conn)
        resp = time.ctime() + "\r\n"
        conn.send(resp.encode('latin-1'))
        conn.close()

sched = Scheduler()
sched.new(time_server(('',10000)))  # 监听端口 10000 的服务器
sched.new(time_server(('',11000)))  # 监听端口 11000 的服务器
sched.run()
```

在这个示例中，两个不同的服务器并发运行——每个服务器监听一个不同的端口号（使用 `telnet` 连接并测试）。`yield ReadWait()` 和 `yield WriteWait()` 语句会导致运行每个服务器的协程挂起，直到可以在关联的套接字上进行 I/O 操作。当这些语句返回时，代码立即继续进行 I/O 操作，例如 `accept()` 或 `send()`。



## 第21章 网络编程与套接字

`ReadWait`和`WriteWait`的使用方式看起来相当底层。幸运的是，我们的设计允许将这些操作隐藏在库函数和方法背后——前提是它们也是协程。考虑以下封装套接字对象并模拟其接口的对象：

```
class CoSocket(object):
    def __init__(self, sock):
        self.sock = sock
    def close(self):
        yield self.sock.close()
    def bind(self, addr):
        yield self.sock.bind(addr)
    def listen(self, backlog):
        yield self.sock.listen(backlog)
    def connect(self, addr):
        yield WriteWait(self.sock)
        yield self.sock.connect(addr)
    def accept(self):
        yield ReadWait(self.sock)
        conn, addr = self.sock.accept()
        yield CoSocket(conn), addr
    def send(self, bytes):
        while bytes:
            evt = yield WriteWait(self.sock)
            nsent = self.sock.send(bytes)
            bytes = bytes[nsent:]
    def recv(self, maxsize):
        yield ReadWait(self.sock)
        yield self.sock.recv(maxsize)
```

下面是使用`CoSocket`类重新实现的时间服务器：

```
from socket import socket, AF_INET, SOCK_STREAM

def time_server(address):
    import time
    s = CoSocket(socket(AF_INET, SOCK_STREAM))
    yield s.bind(address)
    yield s.listen(5)
    while True:
        conn, addr = yield s.accept()
        print(conn)
        print("Connection from %s" % str(addr))
        resp = time.ctime() + "\r\n"
        yield conn.send(resp.encode('latin-1'))
        yield conn.close()

sched = Scheduler()
sched.new(time_server(('', 10000)))   # Server on port 10000
sched.new(time_server(('', 11000)))   # Server on port 11000
sched.run()
```

在这个示例中，`CoSocket`对象的编程接口看起来很像普通的套接字。唯一的区别是每个操作都必须以`yield`开头（因为每个方法都被定义为协程）。起初，这看起来很疯狂，所以你可能会问：这些疯狂的代码能带来什么好处？如果你运行上面的服务器，你会发现它能够在不使用线程或子进程的情况下并发运行。不仅如此，只要你忽略所有的`yield`关键字，它的控制流看起来就是"正常"的。

下面是一个异步Web服务器，它可以并发处理多个客户端连接，但不使用回调函数、线程或进程。可以将此与`asynchat`和`asyncore`模块中的示例进行比较。

```
import os
import mimetypes
try:
    from http.client import responses    # Python 3
except ImportError:
    from httplib import responses        # Python 2
from socket import *

def http_server(address):
    s = CoSocket(socket(AF_INET, SOCK_STREAM))
    yield s.bind(address)
    yield s.listen(50)

    while True:
        conn, addr = yield s.accept()
        yield NewTask(http_request(conn, addr))
        del conn, addr

def http_request(conn, addr):
    request = b""
    while True:
        data = yield conn.recv(8192)
        request += data
        if b'\r\n\r\n' in request:
            break

    header_data = request[:request.find(b'\r\n\r\n')]
    header_text = header_data.decode('latin-1')
    header_lines = header_text.splitlines()
    method, url, proto = header_lines[0].split()
    if method == 'GET':
        if os.path.exists(url[1:]):
            yield serve_file(conn, url[1:])
        else:
            yield error_response(conn, 404, "File %s not found" % url)
    else:
        yield error_response(conn, 501, "%s method not implemented" % method)
    yield conn.close()

def serve_file(conn, filename):
    content, encoding = mimetypes.guess_type(filename)
    yield conn.send(b"HTTP/1.0 200 OK\r\n")
    yield conn.send(("Content-type: %s\r\n" % content).encode('latin-1'))
    yield conn.send(("Content-length: %d\r\n" %
                     os.path.getsize(filename)).encode('latin-1'))
    yield conn.send(b"\r\n")
    f = open(filename, "rb")
    while True:
        data = f.read(8192)
        if not data:
            break
        yield conn.send(data)

def error_response(conn, code, message):
    yield conn.send(("HTTP/1.0 %d %s\r\n" %
                     (code, responses[code])).encode('latin-1'))
    yield conn.send(b"Content-type: text/plain\r\n")
    yield conn.send(b"\r\n")
    yield conn.send(message.encode('latin-1'))

sched = Scheduler()
sched.new(http_server(('', 8080)))
sched.mainloop()
```

仔细研究这个示例将使你对协程和一些非常高级的第三方模块所使用的并发编程技术有深入的了解。但是，过度使用这些技术可能会让你在下次代码审查后被解雇。

##### 何时考虑异步网络编程

使用异步I/O（`asyncore`和`asynchat`）、轮询以及前面示例中展示的协程，仍然是Python开发中最神秘的方面之一。然而，这些技术的使用频率比你想象的要高。使用异步I/O的一个常见理由是，当处理大量客户端且受到全局解释器锁（参见第20章"线程与并发"）相关限制时，可以最大限度地减少使用大量线程带来的编程开销。

从历史上看，`asyncore`模块是最早支持异步I/O的库模块之一。`asynchat`模块随后推出，旨在简化大量编码工作。然而，这两个模块都采用了将I/O作为事件来处理的方式。例如，当一个I/O事件发生时，会触发一个回调函数，然后回调函数对I/O事件做出响应并执行一些处理。如果你以这种方式构建大型应用程序，你会发现事件处理几乎渗透到应用程序的每个部分（例如，I/O事件触发回调，回调又触发更多的回调，更多的回调又触发其他回调，如此循环往复）。更流行的网络包之一Twisted（http://twistedmatrix.com）就采用了这种方法，并在此基础上进行了大量扩展。

协程更为现代，但理解程度和使用率较低，因为它们直到Python 2.5才首次引入。协程的一个重要特性是，你可以编写出在整体控制流上更像线程程序的程序。例如，示例中的Web服务器没有使用任何回调函数，看起来几乎与你使用线程编写的代码一模一样——你只需要习惯使用`yield`语句。Stackless Python（http://www.stackless.com）将这一思想发挥到了极致。

作为一般规则，对于大多数网络应用程序，你可能应该抵制使用异步I/O技术的冲动。例如，如果你需要编写一个在数百甚至数千个同时网络连接上持续传输数据的服务器，线程往往具有更好的性能。这是因为`select()`的性能会随着其必须监控的连接数量增加而显著下降。在Linux上，可以使用`epoll()`等特殊函数来减少这种性能损失，但这会限制代码的可移植性。异步I/O的主要好处可能体现在需要将网络功能与其他事件循环（例如GUI）集成的应用程序中，或者在网络功能被添加到执行大量CPU处理的代码中的应用程序中。在这些情况下，使用异步网络编程可能会带来更快的响应时间。

举例说明，考虑以下执行歌曲"墙上一千万瓶啤酒"中所描述任务的程序：

```
bottles = 10000000

def drink_beer():
    remaining = 12.0
    while remaining > 0.0:
        remaining -= 0.1

def drink_bottles():
    global bottles
    while bottles > 0:
        drink_beer()
        bottles -= 1
```

现在，假设你想为这段代码添加远程监控功能，允许客户端连接并查看还剩多少瓶啤酒。一种方法是在自己的线程中启动一个服务器，让它与主应用程序并行运行，如下所示：

```
def server(port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.bind(('', port))
    s.listen(5)
    while True:
        client, addr = s.accept()
        client.send(("%d bottles\r\n" % bottles).encode('latin-1'))
        client.close()

# Launch the monitor server
thr = threading.Thread(target=server, args=(10000,))
thr.daemon = True
thr.start()
drink_bottles()
```

另一种方法是编写一个基于I/O轮询的服务器，将轮询操作直接嵌入主计算循环中。下面是使用之前开发的协程调度器的一个示例：

```
def drink_bottles():
    global bottles
    while bottles > 0:
        drink_beer()
        bottles -= 1
        scheduler.mainloop(count=1, timeout=0)  # Poll for connections

# An asynchronous server based on coroutines.
def server(port):
    s = CoSocket(socket.socket(socket.AF_INET, socket.SOCK_STREAM))
    yield s.bind(('', port))
    yield s.listen(5)
    while True:
        client, addr = yield s.accept()
        yield client.send(("%d bottles\r\n" % bottles).encode('latin-1'))
        yield client.close()

scheduler = Scheduler()
scheduler.new(server(10000))
drink_bottles()
```

如果你编写一个单独的程序，定期连接到这个啤酒瓶程序并测量接收状态消息所需的响应时间，结果是

令人惊讶的是，在作者的机器（一台双核 2 GHz MacBook）上，基于协程的服务器的平均响应时间（基于 1,000 次请求测量）约为 1 毫秒，而基于线程的服务器为 5 毫秒。这种差异的原因在于，基于协程的代码能够在检测到连接后立即响应，而线程服务器则必须等到操作系统调度后才能运行。在存在 CPU 密集型线程和 Python 全局解释器锁的情况下，服务器可能会被延迟，直到 CPU 密集型线程超出其分配的时间片。在许多系统中，时间片约为 10 毫秒，因此上述对线程响应时间的粗略测量，正是您可能期望等待 CPU 密集型任务被操作系统抢占的平均时间。

轮询的缺点在于，如果轮询过于频繁，会引入显著的开销。例如，即使在本例中响应时间更低，但使用轮询的程序运行完成所需的时间比不使用轮询的程序多出 50% 以上。如果将代码改为仅在每六次啤酒后轮询一次，响应时间会略微增加到 1.2 毫秒，而程序的运行时间仅比无任何轮询的程序增加 3%。不幸的是，除了对应用程序进行测量外，通常没有明确的方法来知道轮询的频率。

尽管这种改进的响应时间可能看起来是个胜利，但在尝试实现自己的并发性时，仍然存在一些严重的问题。例如，任务在执行任何类型的阻塞操作时需要格外小心。在 web 服务器示例中，有一段代码用于打开文件并读取数据。当此操作发生时，整个程序将会冻结——如果文件访问涉及磁盘寻道，可能会冻结很长时间。解决此问题的唯一方法是额外实现异步文件访问，并将其作为功能添加到调度器中。对于更复杂的操作，例如执行数据库查询，如何以异步方式执行工作变得相当复杂。一种方法是在线程中执行工作，并在结果可用时将其传回任务调度器——这可以通过仔细使用消息队列来实现。在某些系统上，有用于异步 I/O 的底层系统调用（例如 UNIX 上的 `aio_*` 系列函数）。截至本文撰写时，Python 库未提供对这些函数的访问，尽管您可能可以通过第三方模块找到绑定。根据作者的经验，使用此类功能比看起来复杂得多，并且不值得为您的程序引入增加的复杂性——通常您最好让线程库来处理此类问题。

#### socket

`socket` 模块提供了对标准 BSD 套接字接口的访问。虽然它基于 UNIX，但此模块在所有平台上都可用。套接字接口被设计为通用的，能够支持多种网络协议（Internet、TIPC、蓝牙等）。然而，最常见的协议是网际协议（IP），其中包括 TCP 和 UDP。Python 支持 IPv4 和 IPv6，尽管 IPv4 更为常见。

应该注意的是，此模块是相对底层的，直接提供对操作系统提供的网络功能的访问。如果您正在编写网络应用程序，使用第 22 章中描述的模块或本章末尾描述的 `SocketServer` 模块可能会更容易。

##### 地址族

一些套接字函数需要指定 *地址族*。该族指定所使用的网络协议。为此定义了以下常量：

| 常量 | 描述 |
|----------|-------------|
| AF_BLUETOOTH | 蓝牙协议 |
| AF_INET | IPv4 协议（TCP, UDP） |
| AF_INET6 | IPv6 协议（TCP, UDP） |
| AF_NETLINK | Netlink 进程间通信 |
| AF_PACKET | 链路层数据包 |
| AF_TIPC | 透明进程间通信协议 |
| AF_UNIX | UNIX 域协议 |

其中，`AF_INET` 和 `AF_INET6` 最常用，因为它们代表标准的 Internet 连接。`AF_BLUETOOTH` 仅在支持它的系统上可用（通常是嵌入式系统）。`AF_NETLINK`、`AF_PACKET` 和 `AF_TIPC` 仅在 Linux 上受支持。`AF_NETLINK` 用于用户应用程序和 Linux 内核之间的快速进程间通信。`AF_PACKET` 用于直接在数据链路层（例如，原始以太网数据包）上工作。`AF_TIPC` 是一种用于 Linux 集群上高性能 IPC 的协议（http://tipc.sourceforge.net/）。

##### 套接字类型

| 常量 | 描述 |
|----------|-------------|
| SOCK_STREAM | 可靠的、面向连接的字节流（TCP） |
| SOCK_DGRAM | 数据报（UDP） |
| SOCK_RAW | 原始套接字 |
| SOCK_RDM | 可靠的数据报 |
| SOCK_SEQPACKET | 有序的、连接模式的记录传输 |

最常见的套接字类型是 `SOCK_STREAM` 和 `SOCK_DGRAM`，因为它们对应于 Internet 协议套件中的 TCP 和 UDP。`SOCK_RDM` 是一种可靠的 UDP 形式，保证数据报的传递，但不保留顺序（数据报可能以与发送不同的顺序接收）。`SOCK_SEQPACKET` 用于通过面向流的连接发送数据包，同时保留它们的顺序和数据包边界。`SOCK_RDM` 和 `SOCK_SEQPACKET` 都未被广泛支持，因此如果您关心可移植性，最好不要使用它们。`SOCK_RAW` 用于提供对原始协议的底层访问，如果您想执行特殊用途的操作，例如发送控制消息（例如 ICMP 消息），则会使用它。使用 `SOCK_RAW` 通常仅限于以超级用户或管理员权限运行的程序。

并非每个协议族都支持每种套接字类型。例如，如果您正在使用 `AF_PACKET` 在 Linux 上嗅探以太网数据包，您无法使用 `SOCK_STREAM` 建立面向流的连接。相反，您必须使用 `SOCK_DGRAM` 或 `SOCK_RAW`。对于 `AF_NETLINK` 套接字，`SOCK_RAW` 是唯一支持的类型。

##### 寻址

为了在套接字上执行任何通信，您必须指定目标地址。地址的形式取决于套接字的地址族。

###### AF_INET (IPv4)

对于使用 IPv4 的 Internet 应用程序，地址被指定为一个元组 `(host, port)`。
这里有两个例子：

```
('www.python.org', 80)
('66.113.130.182', 25)
```

如果 `host` 是空字符串，它具有与 `INADDR_ANY` 相同的含义，表示任何地址。这通常是服务器在创建任何客户端都可以连接的套接字时使用的。如果 `host` 设置为 `'<broadcast>'`，它具有与套接字 API 中的 `INADDR_BROADCAST` 常量相同的含义。

请注意，当使用像 `'www.python.org'` 这样的主机名时，Python 使用 DNS 将主机名解析为 IP 地址。根据 DNS 的配置，您每次可能会得到不同的 IP 地址。如果需要，请使用原始 IP 地址（如 `'66.113.130.182'`）来避免此行为。

###### AF_INET6 (IPv6)

对于 IPv6，地址被指定为一个 4 元组 `(host, port, flowinfo, scopeid)`。使用 IPv6 时，`host` 和 `port` 组件的工作方式与 IPv4 相同，只是 IPv6 主机地址的数字形式通常由冒号分隔的八个十六进制数字符串指定，例如

`'FEDC:BA98:7654:3210:FEDC:BA98:7654:3210'` 或 `'080A::4:1'`（在这种情况下，双冒号用 0 填充一段地址组件）。

`flowinfo` 参数是一个 32 位数字，由 24 位流标签（低 24 位）、4 位优先级（接下来的 4 位）和四个保留位（高 4 位）组成。流标签通常仅在发送方希望路由器进行特殊处理时使用。否则，`flowinfo` 设置为 0。

`scopeid` 参数是一个 32 位数字，仅在使用链路本地和站点本地地址时需要。链路本地地址总是以 `'FE80:...'` 前缀开头，用于同一 LAN 上的机器之间（路由器不会转发链路本地数据包）。在这种情况下，`scopeid` 是一个接口索引，用于标识主机上的特定网络接口。可以使用 UNIX 上的 `'ifconfig'` 或 Windows 上的 `'ipv6 if'` 等命令查看此信息。站点本地地址总是以 `'FEC0:....'` 前缀开头，用于同一站点内的机器之间（例如，给定子网上的所有机器）。在这种情况下，`scopeid` 是一个站点标识符编号。

如果 `flowinfo` 或 `scopeid` 没有给出数据，可以像 IPv4 一样，将 IPv6 地址给出为元组 `(host, port)`。



###### AF_UNIX

对于 UNIX 域套接字，地址是一个包含路径名的字符串——例如，`'/tmp/myserver'`。

###### AF_PACKET

对于 Linux 包协议，地址是一个元组 `(device, protonum [, pkttype [, hatype [, addr]]])`，其中 `device` 是一个指定设备名称的字符串，如 `"eth0"`，`protonum` 是一个指定以太网协议号的整数，该协议号定义在 `<linux/if_ether.h>` 头文件中（例如，`0x0800` 表示 IP 数据包）。`packet_type` 是一个指定数据包类型的整数，是以下常量之一：

| 常量 | 描述 |
|----------|-------------|
| PACKET_HOST | 发往本地主机的数据包地址。 |
| PACKET_BROADCAST | 物理层广播数据包。 |
| PACKET_MULTICAST | 物理层多播。 |
| PACKET_OTHERHOST | 发往其他主机的数据包，但被混杂模式下的设备驱动程序捕获。 |
| PACKET_OUTGOING | 本机发出的数据包，但已回环到数据包套接字。 |

`hatype` 是一个指定硬件地址类型的整数，该类型在 ARP 协议中使用，定义在 `<linux/if_arp.h>` 头文件中。`addr` 是一个包含硬件地址的字节串，其结构取决于 `hatype` 的值。对于以太网，`addr` 是一个包含硬件地址的 6 字节字符串。

###### AF_NETLINK

对于 Linux Netlink 协议，地址是一个元组 `(pid, groups)`，其中 `pid` 和 `groups` 都是无符号整数。`pid` 是套接字的单播地址，通常与创建套接字的进程的进程 ID 相同，对于内核则为 `0`。`groups` 是一个位掩码，用于指定要加入的多播组。更多信息请参阅 Netlink 文档。

###### AF_BLUETOOTH

蓝牙地址取决于所使用的协议。对于 L2CAP，地址是一个元组 `(addr, psm)`，其中 `addr` 是一个字符串，如 `'01:23:45:67:89:ab'`，`psm` 是一个无符号整数。对于 RFCOMM，地址是一个元组 `(addr, channel)`，其中 `addr` 是一个地址字符串，`channel` 是一个整数。对于 HCI，地址是一个单元素元组 `(deviceno,)`，其中 `deviceno` 是一个整数设备编号。对于 SCO，地址是一个字符串 `host`。

常量 `BDADDR_ANY` 表示任意地址，是一个字符串 `'00:00:00:00:00:00'`。常量 `BDADDR_LOCAL` 是一个字符串 `'00:00:00:ff:ff:ff'`。

###### AF_TIPC

对于 TIPC 套接字，地址是一个元组 `(addr_type, v1, v2, v3 [, scope])`，其中所有字段都是无符号整数。`addr_type` 是以下值之一，它还决定了 `v1`、`v2` 和 `v3` 的值：

| 地址类型 | 描述 |
| --- | --- |
| TIPC_ADDR_NAMESEQ | `v1` 是服务器类型，`v2` 是端口标识符，`v3` 为 `0`。 |
| TIPC_ADDR_NAME | `v1` 是服务器类型，`v2` 是下限端口号，`v3` 是上限端口号。 |
| TIPC_ADDR_ID | `v1` 是节点，`v2` 是引用，`v3` 为 `0`。 |

可选的 *scope* 字段是 `TIPC_ZONE_SCOPE`、`TIPC_CLUSTER_SCOPE` 或 `TIPC_NODE_SCOPE` 之一。

##### 函数

socket 模块定义了以下函数：

```
create_connection(address [, timeout])
```

建立一个到 *address* 的 `SOCK_STREAM` 连接，并返回一个已连接的套接字对象。*address* 是形如 `(host, port)` 的元组，*timeout* 指定可选的超时时间。此函数的工作方式是先调用 `getaddrinfo()`，然后尝试连接到返回的每个元组。

```
fromfd(fd, family, socktype [, proto])
```

从一个整数文件描述符 *fd* 创建一个套接字对象。地址族、套接字类型和协议号与 `socket()` 函数相同。文件描述符必须引用先前创建的套接字。它返回一个 `SocketType` 的实例。

```
getaddrinfo(host, port [, family [, socktype [, proto [, flags]]]])
```

给定关于主机的 *host* 和 *port* 信息，此函数返回一个元组列表，其中包含建立套接字连接所需的信息。*host* 是一个包含主机名或数字 IP 地址的字符串。*port* 是一个数字或表示服务名的字符串（例如，`"http"`、`"ftp"`、`"smtp"`）。每个返回的元组由五个元素组成 `(family, socktype, proto, canonname, sockaddr)`。*family*、*socktype* 和 *proto* 项的值与传递给 `socket()` 函数的值相同。*canonname* 是一个表示主机规范名称的字符串。*sockaddr* 是一个包含套接字地址的元组，如前面关于 Internet 地址的部分所述。以下是一个示例：

```
>>> getaddrinfo("www.python.org", 80)
[(2, 2, 17, '', ('194.109.137.226', 80)), (2, 1, 6, '', ('194.109.137.226', 80))]
```

在此示例中，`getaddrinfo()` 返回了关于两个可能的套接字连接的信息。第一个（`proto=17`）是 UDP 连接，第二个（`proto=6`）是 TCP 连接。`getaddrinfo()` 的附加参数可用于缩小选择范围。例如，此示例返回关于建立 IPv4 TCP 连接的信息：

```
>>> getaddrinfo("www.python.org", 80, AF_INET, SOCK_STREAM)
[(2, 1, 6, '', ('194.109.137.226', 80))]
```

特殊常量 `AF_UNSPEC` 可用作地址族，以查找任何类型的连接。例如，以下代码获取关于任何类 TCP 连接的信息，可能返回 IPv4 或 IPv6 的信息：

```
>>> getaddrinfo("www.python.org","http", AF_UNSPEC, SOCK_STREAM)
[(2,1,6,'',('194.109.137.226',80))]
```

`getaddrinfo()` 用于非常通用的目的，适用于所有支持的网络协议（IPv4、IPv6 等）。如果你关心兼容性和支持未来的协议，请使用它，特别是当你打算支持 IPv6 时。

###### getdefaulttimeout

返回以秒为单位的默认套接字超时时间。值为 `None` 表示未设置超时。

###### getfqdn([name])

返回 *name* 的完全限定域名。如果省略 *name*，则假定为本地机器。例如，`getfqdn("foo")` 可能返回 `"foo.quasievi l.org"`。

###### gethostbyname(hostname)

将主机名（如 `'www.python.org'`）转换为 IPv4 地址。IP 地址以字符串形式返回，如 `'132.151.1.90'`。它不支持 IPv6。

###### gethostbyname_ex(hostname)

将主机名转换为 IPv4 地址，但返回一个元组 `(hostname, aliaslist, ipaddrlist)`，其中 *hostname* 是主主机名，*aliaslist* 是同一地址的备用主机名列表，*ipaddrlist* 是同一主机上同一接口的 IPv4 地址列表。例如，

`gethostbyname_ex('www.python.org')` 返回类似 `('fang.python.org', ['www.python.org'], ['194.109.137.226'])` 的结果。此函数不支持 IPv6。

###### gethostname()

返回本地机器的主机名。

###### gethostbyaddr(ip_address)

给定一个 IP 地址（如 `'132.151.1.90'`），返回与 `gethostbyname_ex()` 相同的信息。如果 *ip_address* 是一个 IPv6 地址，如 `'FEDC:BA98:7654:3210:FEDC:BA98:7654:3210'`，将返回有关 IPv6 的信息。

###### getnameinfo(address, flags)

给定一个套接字地址 *address*，此函数根据 *flags* 的值将地址转换为一个二元组 `(host, port)`。*address* 参数是指定地址的元组——例如，`('www.python.org',80)`。*flags* 是以下常量的按位或运算：

| 常量 | 描述 |
| --- | --- |
| `NI_NOFQDN` | 对本地主机不使用完全限定名。 |
| `NI_NUMERICHOST` | 以数字形式返回地址。 |
| `NI_NAMEREQD` | 要求主机名。如果 `address` 没有 DNS 条目则返回错误。 |
| `NI_NUMERICSERV` | 返回的 `port` 是包含端口号的字符串。 |
| `NI_DGRAM` | 指定正在查找的服务是数据报服务（UDP）而不是 TCP（默认值）。 |

此函数的主要目的是获取有关地址的附加信息。以下是一个示例：

```
>>> getnameinfo(('194.109.137.226',80),0)
('fang.python.org', 'http')
>>> getnameinfo(('194.109.137.226',80),NI_NUMERICSERV)
('fang.python.org','80')
```

###### getprotobyname(protocolname)

将 Internet 协议名（如 `'icmp'`）转换为可以传递给 `socket()` 函数第三个参数的协议号（如 `IPPROTO_ICMP` 的值）。如果协议名无法识别，则引发 `socket.error`。通常，这仅用于原始套接字。

###### getservbyname(servicename [, protocolname])

将 Internet 服务名和协议名转换为该服务的端口号。例如，`getservbyname('ftp', 'tcp')` 返回 `21`。协议名（如果提供）应为 `'tcp'` 或 `'udp'`。如果 `servicename` 与任何已知服务不匹配，则引发 `socket.error`。

###### getservbyport(port [, protocolname])

这是 `getservbyname()` 的反向操作。给定一个数字端口号 `port`，此函数返回一个给出服务名称的字符串（如果有的话）。例如，`getservbyport(21, 'tcp')` 返回 `'ftp'`。协议名（如果提供）应为 `'tcp'` 或 `'udp'`。如果 `port` 没有可用的服务名称，则引发 `socket.error`。

###### has_ipv6

布尔常量，如果 IPv6 支持可用则为 `True`。

###### htonl(x)

将 32 位整数从主机字节序转换为网络字节序（大端序）。

###### htons(x)

将 16 位整数从主机字节序转换为网络字节序（大端序）。

###### inet_aton(ip_string)

将以字符串形式提供的 IPv4 地址（例如，`'135.128.11.209'`）转换为 32 位打包二进制格式，用作地址的原始编码。返回的

value 是一个包含二进制编码的四字符字符串。如果需要将地址传递给 C 语言程序，或者需要将地址打包到传递给其他程序的数据结构中，这将非常有用。不支持 IPv6。

```
inet_ntoa(packedip)
```

将二进制打包的 IPv4 地址转换为使用标准点分表示法的字符串（例如，`'135.128.11.209'`）。`packedip` 是一个包含 IP 地址原始 32 位编码的四字符字符串。如果地址是从 C 语言接收到的，或者正在从数据结构中解包，该函数将非常有用。不支持 IPv6。

```
inet_ntop(address_family, packed_ip)
```

将表示 IP 网络地址的打包二进制字符串 `packed_ip` 转换为字符串，例如 `'123.45.67.89'`。`address_family` 是地址族，通常为 `AF_INET` 或 `AF_INET6`。可用于从原始字节缓冲区（例如，从低级网络包的内容中）获取网络地址字符串。

```
inet_pton(address_family, ip_string)
```

将 IP 地址（例如 `'123.45.67.89'`）转换为打包的字节字符串。`address_family` 是地址族，通常为 `AF_INET` 或 `AF_INET6`。如果需要将网络地址编码为原始二进制数据包，可以使用此函数。

```
ntohl(x)
```

将 32 位整数从网络字节序（大端序）转换为主机字节序。

```
ntohs(x)
```

将 16 位整数从网络字节序（大端序）转换为主机字节序。

```
setdefaulttimeout(timeout)
```

设置新创建的套接字对象的默认超时时间。`timeout` 是以秒为单位指定的浮点数。可以提供 `None` 值表示不设超时（这是默认值）。

```
socket(family, type [, proto])
```

使用给定的地址族、套接字类型和协议号创建一个新的套接字。`family` 是地址族，`type` 是套接字类型，如本节第一部分所述。要建立 TCP 连接，请使用 `socket(AF_INET, SOCK_STREAM)`。要建立 UDP 连接，请使用 `socket(AF_INET, SOCK_DGRAM)`。该函数返回一个 `SocketType` 实例（稍后描述）。

协议号通常被省略（默认为 0）。这通常只用于原始套接字（`SOCK_RAW`），并设置为取决于所用地址族的常量。以下列表显示了 Python 可能为 `AF_INET` 和 `AF_INET6` 定义的所有协议号，具体取决于主机系统上的可用性：

| 常量 | 描述 |
|----------|-------------|
| IPPROTO_AH | IPv6 认证头 |
| IPPROTO_BIP | Banyan VINES |
| IPPROTO_DSTOPTS | IPv6 目标选项 |
| IPPROTO_EGP | 外部网关协议 |
| IPPROTO_EON | ISO CNLP（无连接网络协议） |
| IPPROTO_ESP | IPv6 封装安全载荷 |
| IPPROTO_FRAGMENT | IPv6 分片头 |
| IPPROTO_GGP | 网关到网关协议（RFC823） |
| IPPROTO_GRE | 通用路由封装（RFC1701） |
| IPPROTO_HELLO | Fuzzball HELLO 协议 |
| IPPROTO_HOPOPTS | IPv6 逐跳选项 |
| IPPROTO_ICMP | IPv4 ICMP |
| IPPROTO_ICMPV6 | IPv6 ICMP |
| IPPROTO_IDP | XNS IDP |
| IPPROTO_IGMP | 组管理协议 |
| IPPROTO_IP | IPv4 |
| IPPROTO_IPCOMP | IP 载荷压缩协议 |
| IPPROTO_IPIP | IP 内嵌 IP |
| IPPROTO_IPV4 | IPv4 头 |
| IPPROTO_IPV6 | IPv6 头 |
| IPPROTO_MOBILE | IP 移动性 |
| IPPROTO_ND | Netdisk 协议 |
| IPPROTO_NONE | IPv6 无下一跳头 |
| IPPROTO_PIM | 协议无关组播 |
| IPPROTO_PUP | Xerox PARC 通用数据包（PUP） |
| IPPROTO_RAW | 原始 IP 数据包 |
| IPPROTO_ROUTING | IPv6 路由头 |
| IPPROTO_RSVP | 资源预留 |
| IPPROTO_TCP | TCP |
| IPPROTO_TP | OSI 传输协议（TP-4） |
| IPPROTO_UDP | UDP |
| IPPROTO_VRRP | 虚拟路由器冗余协议 |
| IPPROTO_XTP | 快速传输协议 |

以下协议号用于 `AF_BLUETOOTH`：

| 常量 | 描述 |
|----------|-------------|
| BTPROTO_L2CAP | 逻辑链路控制和适配协议 |
| BTPROTO_HCI | 主机/控制器接口 |
| BTPROTO_RFCOMM | 线缆替代协议 |
| BTPROTO_SCO | 面向同步连接链路 |

```
socketpair([family [, type [, proto ]]])
```

使用给定的 *family*、*type* 和 *proto* 选项创建一对已连接的套接字对象，这些选项与 `socket()` 函数的含义相同。此函数仅适用于 UNIX 域套接字（`family=AF_UNIX`）。*type* 可以是 `SOCK_DGRAM` 或 `SOCK_STREAM`。如果 *type* 为 `SOCK_STREAM`，则会创建一个称为*流管道*的对象。*proto* 通常为 0（默认值）。此函数的主要用途是在通过 `os.fork()` 创建的进程之间建立进程间通信。例如，父进程会调用 `socketpair()` 创建一对套接字，然后调用 `os.fork()`。父进程和子进程随后使用这些套接字进行通信。

套接字由 `SocketType` 类型的实例表示。以下方法可用于套接字 *s*：

###### s.accept()

接受一个连接并返回一个元组 *(conn, address)*，其中 *conn* 是一个新的套接字对象，可用于在连接上发送和接收数据，*address* 是连接另一端套接字的地址。

###### s.bind(*address*)

将套接字绑定到一个地址。*address* 的格式取决于地址族。在大多数情况下，它是形如 *(hostname, port)* 的元组。对于 IP 地址，空字符串表示 `INADDR_ANY`，字符串 `'<broadcast>'` 表示 `INADDR_BROADCAST`。`INADDR_ANY` 主机名（空字符串）用于表示服务器允许在系统上的任何网络接口上接受连接。这通常在服务器具有多个网络接口时使用。当套接字用于发送广播消息时，使用 `INADDR_BROADCAST` 主机名（`'<broadcast>'`）。

###### s.close()

关闭套接字。套接字在被垃圾回收时也会被关闭。

###### s.connect(*address*)

连接到 *address* 处的远程套接字。*address* 的格式取决于地址族，但通常是 *(hostname, port)* 元组。如果发生错误，将引发 `socket.error`。如果要连接到同一台计算机上的服务器，可以使用名称 `'localhost'` 作为 *hostname*。

###### s.connect_ex(*address*)

类似于 `connect(address)`，但成功时返回 `0`，失败时返回 `errno` 的值。

###### s.fileno()

返回套接字的文件描述符。

###### s.getpeername()

返回套接字所连接的远程地址。通常返回值是一个元组 *(ipaddr, port)*，但这取决于所使用的地址族。并非所有系统都支持此方法。

###### s.getsockname()

返回套接字自身的地址。通常这是一个元组 *(ipaddr, port)*。

###### s.getsockopt(*level*, *optname* [, *buflen*])

返回套接字选项的值。*level* 定义选项的级别，对于套接字级选项为 `SOL_SOCKET`，对于协议相关选项为协议号（如 `IPPROTO_IP`）。*optname* 选择特定的选项。如果省略 *buflen*，则假定为整数选项并返回其整数值。如果提供了 *buflen*，则指定用于接收选项的缓冲区的最大长度。该缓冲区以字节字符串返回，由调用者使用 `struct` 模块或其他方式解码其内容。

以下表格列出了 Python 定义的套接字选项。这些选项中的大多数被认为是高级套接字 API 的一部分，用于控制网络的低级细节。您需要查阅其他文档以获取更详细的描述。当类型名称列在值列中时，该名称与标准 C 数据结构同名，该数据结构与该值关联并用于标准套接字编程接口。并非所有选项在所有机器上都可用。

以下是 `SOL_SOCKET` 级别常用的选项名称：

| 选项名称 | 值 | 描述 |
|-------------|-------|-------------|
| SO_ACCEPTCONN | 0, 1 | 确定套接字是否正在接受连接。 |
| SO_BROADCAST | 0, 1 | 允许发送广播数据报。 |
| SO_DEBUG | 0, 1 | 确定是否正在记录调试信息。 |
| SO_DONTROUTE | 0, 1 | 绕过路由表查找。 |
| SO_ERROR | int | 获取错误状态。 |
| SO_EXCLUSIVEADDRUSE | 0, 1 | 防止其他套接字被强制绑定到相同的地址和端口。这会禁用 SO_REUSEADDR 选项。 |
| SO_KEEPALIVE | 0, 1 | 定期探测连接的另一端，如果处于半开状态则终止连接。 |
| SO_LINGER | linger | 如果发送缓冲区包含数据，则在 `close()` 时保持等待。`linger` 是一个包含两个 32 位整数（`onoff`、`seconds`）的打包二进制字符串。 |
| SO_OOBINLINE | 0, 1 | 将带外数据放入输入队列。 |
| SO_RCVBUF | int | 接收缓冲区大小（以字节为单位）。 |
| SO_RCVLOWAT | int | `select()` 将套接字返回为可读之前要读取的字节数。 |
| SO_RCVTIMEO | timeval | 接收调用的超时时间（以秒为单位）。`timeval` 是一个包含两个 32 位无符号整数（`seconds`、`microseconds`）的打包二进制字符串。 |
| SO_REUSEADDR | 0, 1 | 允许重用本地地址。 |
| SO_REUSEPORT | 0, 1 | 允许多个进程绑定到相同的地址，前提是所有进程中都设置了此套接字选项。 |
| SO_SNDBUF | int | 发送缓冲区大小（以字节为单位）。 |
| SO_SNDLOWAT | int | `select()` 将套接字返回为可写之前发送缓冲区中可用的字节数。 |
| SO_SNDTIMEO | timeval | 发送调用的超时时间（以秒为单位）。`timeval` 的描述请参见 SO_RCVTIMEO。 |
| SO_TYPE | int | 获取套接字类型。 |
| SO_USELOOPBACK | 0, 1 | 路由套接字获取其发送内容的副本。 |



| 选项名称 | 值 | 描述 |
| --- | --- | --- |
| IP_ADD_MEMBERSHIP | ip_mreg | 加入多播组（仅用于设置）。ip_mreg 是一个打包的二进制字符串，包含两个 32 位 IP 地址（multiaddr, localaddr），其中 multiaddr 是多播地址，localaddr 是正在使用的本地接口的 IP。 |
| IP_DROP_MEMBERSHIP | ip_mreg | 离开多播组（仅用于设置）。ip_mreg 的描述如上。 |
| IP_HDRINCL | int | 随数据一起包含 IP 头部。 |
| IP_MAX_MEMBERSHIPS | int | 最大多播组数量。 |
| IP_MULTICAST_IF | in_addr | 出站接口。in_addr 是一个打包的二进制字符串，包含一个 32 位 IP 地址。 |
| IP_MULTICAST_LOOP | 0,1 | 回环。 |
| IP_MULTICAST_TTL | uint8 | 生存时间。uint8 是一个打包的二进制字符串，包含一个 1 字节的无符号字符。 |
| IP_OPTIONS | ipopts | IP 头部选项。ipopts 是一个不超过 44 字节的打包二进制字符串。该字符串的内容在 RFC 791 中描述。 |
| IP_RECVDSTADDR | 0,1 | 随数据报接收 IP 目的地址。 |
| IP_RECVOPTS | 0,1 | 随数据报接收所有 IP 选项。 |
| IP_RECVRETOPTS | 0,1 | 随响应接收 IP 选项。 |
| IP_RETOPTS | 0,1 | 与 IP_RECVOPTS 相同，但选项未经处理，未填充时间戳或路由记录选项。 |
| IP_TOS | int | 服务类型。 |
| IP_TTL | int | 生存时间。 |

以下选项可用于级别 IPPROTO_IP：

以下选项可用于级别 IPPROTO_IPV6：

| 选项名称 | 值 | 描述 |
| --- | --- | --- |
| IPV6_CHECKSUM | 0,1 | 由系统计算校验和。 |
| IPV6_DONTFRAG | 0,1 | 如果数据包超过 MTU 大小，则不分片。 |
| IPV6_DSTOPTS | ip6_dest | 目的选项。ip6_dest 是形如 (next, len, options) 的打包二进制字符串，其中 next 是一个 8 位整数，给出下一个头部的选项类型；len 是一个 8 位整数，以 8 字节为单位指定头部的长度，不包括第一个 8 字节；options 是编码后的选项。 |
| IPV6_HOPLIMIT | int | 跳数限制。 |
| IPV6_HOPOPTS | ip6_hbh | 逐跳选项。ip6_hbh 与 ip6_dest 具有相同的编码方式。 |
| `IPV6_JOIN_GROUP` | `ip6_mreq` | 加入多播组。`ip6_mreq` 是一个打包的二进制字符串，包含 `(multiaddr, index)`，其中 `multiaddr` 是一个 128 位的 IPv6 多播地址，`index` 是一个 32 位无符号整数接口索引，对应本地接口。 |
| `IPV6_LEAVE_GROUP` | `ip6_mreq` | 离开多播组。 |
| `IPV6_MULTICAST_HOPS` | `int` | 多播数据包的跳数限制。 |
| `IPV6_MULTICAST_IF` | `int` | 出站多播数据包的接口索引。 |
| `IPV6_MULTICAST_LOOP` | `0`, `1` | 将出站多播数据包回送给本地应用程序。 |
| `IPV6_NEXTHOP` | `sockaddr_in6` | 设置出站数据包的下一跳地址。`sockaddr_in6` 是一个打包的二进制字符串，包含 C 语言的 `sockaddr_in6` 结构，通常在 `<netinet/in.h>` 中定义。 |
| `IPV6_PKTINFO` | `ip6_pktinfo` | 数据包信息结构。`ip6_pktinfo` 是一个打包的二进制字符串，包含 `(addr, index)`，其中 `addr` 是一个 128 位的 IPv6 地址，`index` 是一个 32 位无符号整数接口索引。 |
| `IPV6_RECVDSTOPTS` | `0`, `1` | 接收目的选项。 |
| `IPV6_RECVHOPLIMIT` | `0`, `1` | 接收跳数限制。 |
| `IPV6_RECVHOPOPTS` | `0`, `1` | 接收逐跳选项。 |
| `IPV6_RECVPKTINFO` | `0`, `1` | 接收数据包信息。 |
| `IPV6_RECVRTHDR` | `0`, `1` | 接收路由头部。 |
| `IPV6_RECVTCLASS` | `0`, `1` | 接收流量类别。 |
| `IPV6_RTHDR` | `ip6_rthdr` | 路由头部。`ip6_rthdr` 是一个打包的二进制字符串，包含 `(next, len, type, segleft, data)`，其中 `next`、`len`、`type` 和 `segleft` 都是 8 位无符号整数，`data` 是路由数据。参见 RFC 2460。 |
| `IPV6_RTHDRDSTOPTS` | `ip6_dest` | 位于路由选项头部之前的目的选项头部。 |
| `IPV6_RECVPATHMTU` | `0`, `1` | 启用接收 `IPV6_PATHMTU` 辅助数据项。 |
| `IPV6_TCLASS` | `int` | 流量类别。 |
| `IPV6_UNICAST_HOPS` | `int` | 单播数据包的跳数限制。 |
| `IPV6_USE_MIN_MTU` | `-1`, `0`, `1` | 路径 MTU 发现。1 对所有目的地禁用它。-1 仅对多播目的地禁用它。 |
| `IPV6_V6ONLY` | `0`, `1` | 仅连接到其他 IPV6 节点。 |

以下选项可用于级别 `SOL_TCP`：

| 选项名称 | 值 | 描述 |
|-------------|-------|-------------|
| TCP_CORK | 0,1 | 如果设置，则不发送部分帧。 |
| TCP_DEFER_ACCEPT | 0,1 | 仅当数据到达套接字时才唤醒监听器。 |
| TCP_INFO | tcp_info | 返回一个包含有关套接字信息的结构。tcp_info 是特定于实现的。 |
| TCP_KEEPCNT | int | TCP 在放弃连接之前应发送的最大 keepalive 探测次数。 |
| TCP_KEEPIDLE | int | 如果设置了 TCP_KEEPALIVE 选项，连接在 TCP 开始发送 keepalive 探测之前应空闲的秒数。 |
| TCP_KEEPINTVL | int | keepalive 探测之间的间隔秒数。 |
| TCP_LINGER2 | int | 孤立的 FIN_WAIT2 状态套接字的生命周期。 |
| TCP_MAXSEG | int | 出站 TCP 数据包的最大段大小。 |
| TCP_NODELAY | 0,1 | 如果设置，则禁用 Nagle 算法。 |
| TCP_QUICKACK | 0,1 | 如果设置，则立即发送 ACK。禁用 TCP 延迟 ACK 算法。 |
| TCP_SYNCNT | int | 在中止连接请求之前 SYN 重传的次数。 |
| TCP_WINDOW_CLAMP | int | 设置 TCP 通告窗口大小的上限。 |

##### s.gettimeout()

返回当前的超时值（如果有的话）。返回以秒为单位的浮点数，如果未设置超时，则返回 `None`。

###### s.ioctl(control, option)

在 Windows 上提供对 WSAIoctl 接口的有限访问。*control* 唯一支持的值是 `SIO_RCVALL`，用于捕获网络上所有接收到的 IP 数据包。这需要管理员访问权限。以下值可用于 *options*：

| 选项 | 描述 |
|--------|-------------|
| RCVALL_OFF | 防止套接字接收所有 IPv4 或 IPv6 数据包。 |
| RCVALL_ON | 启用混杂模式，允许套接字接收网络上所有 IPv4 或 IPv6 数据包。接收的数据包类型取决于套接字地址族。这不会捕获与其他网络协议（如 ARP）关联的数据包。 |
| RCVALL_IPLEVEL | 接收网络上接收到的所有 IP 数据包，但不启用混杂模式。这将捕获针对主机上任何已配置 IP 地址的所有 IP 数据包。 |

```python
s.listen(backlog)
```

开始监听传入连接。backlog 指定在连接被拒绝之前，操作系统应该排队的最大待处理连接数。该值应至少为 1，对于大多数应用程序，5 已足够。

```python
s.makefile([mode [, bufsize]])
```

创建一个与套接字关联的文件对象。mode 和 bufsize 与内置的 open() 函数具有相同的含义。文件对象使用套接字文件描述符的复本，该复本使用 os.dup() 创建，因此文件对象和套接字对象可以独立关闭或垃圾回收。套接字 s 不应具有超时，也不应配置为非阻塞模式。

```python
s.recv(bufsize [, flags])
```

从套接字接收数据。数据以字符串形式返回。要接收的最大数据量由 bufsize 指定。flags 提供有关消息的附加信息，通常省略（此时默认为零）。如果使用，通常设置为以下常量之一（取决于系统）：

| 常量 | 描述 |
| --- | --- |
| MSG_DONTROUTE | 绕过路由表查找（仅用于发送）。 |
| MSG_DONTWAIT | 非阻塞操作。 |
| MSG_EOR | 指示消息是记录中的最后一条。通常仅在 SOCK_SEQPACKET 套接字上发送数据时使用。 |
| MSG_PEEK | 查看数据但不丢弃（仅用于接收）。 |
| MSG_OOB | 接收/发送带外数据。 |
| MSG_WAITALL | 直到读取所需数量的字节才返回（仅用于接收）。 |

```python
s.recv_into(buffer [, nbytes [, flags]])
```

与 recv() 相同，不同之处在于数据被写入支持缓冲区接口的对象 buffer 中。nbytes 是要接收的最大字节数。如果省略，则最大大小取自缓冲区大小。flags 与 recv() 具有相同的含义。

```python
s.recvfrom(bufsize [, flags])
```

类似于 recv() 方法，不同之处在于返回值是一对 (data, address)，其中 data 是包含接收到的数据的字符串，address 是发送数据的套接字地址。可选的 flags 参数与 recv() 具有相同的含义。此函数主要用于与 UDP 协议结合使用。

```python
s.recvfrom_info(buffer [, nbytes [, flags]])
```

与 recvfrom() 相同，但接收到的数据存储在 buffer 对象 buffer 中。nbytes 指定要接收的最大字节数。如果省略，则最大大小取自 buffer 的大小。flags 与 recv() 具有相同的含义。



##### socket 模块方法

```
s.send(string [, flags])
```

将字符串 `string` 中的数据发送到已连接的套接字。可选参数 `flags` 的含义与前面描述的 `recv()` 相同。返回发送的字节数，该数可能少于 `string` 中的字节数。发生错误时会引发异常。

```
s.sendall(string [, flags])
```

将字符串 `string` 中的数据发送到已连接的套接字，但在返回之前会尝试发送所有数据。成功时返回 `None`；失败时引发异常。`flags` 的含义与 `send()` 相同。

```
s.sendto(string [, flags], address)
```

将数据发送到套接字。`flags` 的含义与 `recv()` 相同。`address` 是形如 `(host, port)` 的元组，用于指定远程地址。套接字不应已处于连接状态。返回发送的字节数。此函数主要与 UDP 协议配合使用。

```
s.setblocking(flag)
```

如果 `flag` 为零，则将套接字设置为非阻塞模式。否则，将套接字设置为阻塞模式（默认）。在非阻塞模式下，如果 `recv()` 调用未找到数据或 `send()` 调用无法立即发送数据，将引发 `socket.error` 异常。在阻塞模式下，这些调用会阻塞，直到可以继续执行。

```
s.setsockopt(level, optname, value)
```

设置给定套接字选项的值。`level` 和 `optname` 的含义与 `getsockopt()` 相同。`value` 可以是整数，也可以是表示缓冲区内容的字符串。对于后者，由调用者确保字符串包含正确的数据。有关套接字选项的名称、值和描述，请参阅 `getsockopt()`。

```
s.settimeout(timeout)
```

设置套接字操作的超时时间。`timeout` 是一个以秒为单位的浮点数。值为 `None` 表示不设超时。如果发生超时，将引发 `socket.timeout` 异常。一般而言，应在创建套接字后尽快设置超时，因为它们可以应用于建立连接相关的操作（如 `connect()`）。

```
s.shutdown(how)
```

关闭连接的一端或两端。如果 `how` 为 0，则禁止进一步接收。如果 `how` 为 1，则禁止进一步发送。如果 `how` 为 2，则禁止进一步发送和接收。

除了这些方法之外，套接字实例 `s` 还具有以下只读属性，它们对应于传递给 `socket()` 函数的参数。

| 属性 | 描述 |
|----------|-------------|
| s.family | 套接字地址族（例如 AF_INET） |
| s.proto | 套接字协议 |
| s.type | 套接字类型（例如 SOCK_STREAM） |

##### 异常

以下异常由 `socket` 模块定义。

###### error

当发生套接字或地址相关错误时引发此异常。返回一个包含底层系统调用返回的错误信息的元组（`errno`，`mesg`）。继承自 `IOError`。

###### herror

当发生地址相关错误时引发的错误。返回一个包含错误编号和错误消息的元组（`herrno`，`hmesg`）。继承自 `error`。

###### gaierror

在 `getaddrinfo()` 和 `getnameinfo()` 函数中发生地址相关错误时引发的错误。错误值是一个元组（`errno`，`mesg`），其中 `errno` 是错误编号，`mesg` 是包含消息的字符串。`errno` 被设置为 `socket` 模块中定义的以下常量之一：

| 常量 | 描述 |
|----------|-------------|
| EAI_ADDRFAMILY | 不支持的地址族。 |
| EAI_AGAIN | 名称解析暂时失败。 |
| EAI_BADFLAGS | 无效的标志。 |
| EAI_BADHINTS | 错误的提示信息。 |
| EAI_FAIL | 名称解析中不可恢复的失败。 |
| EAI_FAMILY | 主机不支持的地址族。 |
| EAI_MEMORY | 内存分配失败。 |
| EAI_NODATA | 与节点名称没有关联的地址。 |
| EAI_NONAME | 未提供节点名称或服务名称。 |
| EAI_PROTOCOL | 不支持的协议。 |
| EAI_SERVICE | 服务名称不支持的套接字类型。 |
| EAI_SOCKTYPE | 不支持的套接字类型。 |
| EAI_SYSTEM | 系统错误。 |

###### timeout

当套接字操作超时时引发的异常。这仅在通过 `setdefaulttimeout()` 函数或套接字对象的 `settimeout()` 方法设置了超时后才会发生。异常值为字符串 `'timeout'`。继承自 `error`。

##### 示例

本章简介中展示了一个简单的 TCP 连接示例。以下示例演示了一个简单的 UDP 回显服务器：

```
# UDP 消息服务器
# 从任意位置接收小数据包并打印
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.bind(("",10000))
while True:
    data, address = s.recvfrom(256)
    print("Received a connection from %s" % str(address))
    s.sendto(b"echo:" + data, address)
```

以下是一个向上述服务器发送消息的客户端：

```
# UDP 消息客户端
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.sendto(b"Hello World", ("", 10000))
resp, addr = s.recvfrom(256)
print(resp)
s.sendto(b"Spam", ("", 10000))
resp, addr = s.recvfrom(256)
print(resp)
s.close()
```

##### 注意事项

-   并非所有常量和套接字选项在所有平台上都可用。如果可移植性是你的目标，你应该只依赖于主要资料中记录的选项，例如本节开头引用的 W. Richard Stevens 的《*UNIX 网络编程*》一书。

-   `socket` 模块中值得注意的缺失是 `recvmsg()` 和 `sendmsg()` 系统调用，它们通常用于处理辅助数据以及与数据包头部、路由和其他细节相关的高级网络选项。要使用此功能，你必须安装第三方模块，如 PyXAPI（http://pypi.python.org/pypi/PyXAPI）。

-   非阻塞套接字操作与涉及超时的操作之间存在细微差别。当套接字函数在非阻塞模式下使用时，如果操作将被阻塞，它会立即返回并携带错误。当设置了超时后，函数仅在操作未在指定超时内完成时才返回错误。

#### ssl

`ssl` 模块用于为套接字对象包装安全套接层（SSL），提供数据加密和对等认证功能。Python 使用 OpenSSL 库（http://www.openssl.org）来实现此模块。关于 SSL 的理论和操作的完整讨论超出了本文所能涵盖的范围。因此，这里仅介绍使用此模块的基本要素，并假设你在 SSL 配置、密钥、证书和其他相关方面已有一定了解：

**`wrap_socket(sock [, **opts])`**

为现有套接字 *sock*（由 `socket` 模块创建）包装 SSL 支持，并返回一个 `SSLSocket` 实例。此函数应在进行后续的 `connect()` 或 `accept()` 操作之前使用。*opts* 代表若干用于指定额外配置数据的关键字参数。

| 关键字参数 | 描述 |
|----------|-------------|
| server_side | 一个布尔标志，指示套接字是作为服务器（`True`）还是客户端（`False`）运行。默认为 `False`。 |
| keyfile | 用于标识连接本地端的密钥文件。这应该是 PEM 格式的文件，通常仅在 `certfile` 指定的文件不包含密钥时才需要。 |
| certfile | 用于标识连接本地端的证书文件。这应该是 PEM 格式的文件。 |
| cert_reqs | 指定是否需要连接对端提供证书以及是否对其进行验证。值为 `CERT_NONE` 表示忽略证书，`CERT_OPTIONAL` 表示不强制要求证书但如果提供了则会验证，`CERT_REQUIRED` 表示需要证书并会进行验证。如果要对证书进行验证，还必须提供 `ca_certs` 参数。 |
| ca_certs | 保存用于验证的证书颁发机构证书的文件名。 |
| ssl_version | 要使用的 SSL 协议版本。可能的值有 `PROTOCOL_TLSv1`、`PROTOCOL_SSLv2`、`PROTOCOL_SSLv23` 或 `PROTOCOL_SSLv3`。默认协议为 `PROTOCOL_SSLv3`。 |
| do_handshake_on_connect | 布尔标志，指定在连接时是否自动执行 SSL 握手。默认为 `True`。 |
| suppress_ragged_eofs | 指定 `read()` 如何处理连接上的意外 EOF。如果为 `True`（默认），则发出正常的 EOF 信号。如果为 `False`，则引发异常。 |

`SSLSocket` 的实例 *s* 继承自 `socket.socket`，并额外支持以下操作：

##### s.cipher()

返回一个元组 `(name, version, secretbits)`，其中 *name* 是正在使用的密码名称，*version* 是 SSL 协议版本，*secretbits* 是正在使用的密钥位数。

##### s.do_handshake()

执行 SSL 握手。通常这是自动完成的，除非在 `wrap_socket()` 函数中将 `do_handshake_on_connect` 选项设置为 `False`。如果底层套接字 *s* 是非阻塞的，且操作无法完成，将引发 `SSLError` 异常。`SSLError` 异常 *e* 的 `e.args[0]` 属性将具有 `SSL_ERROR_WANT_READ` 或 `SSL_ERROR_WANT_WRITE` 的值，具体取决于需要执行的操作。一旦读取或写入可以继续，只需再次调用 `s.do_handshake()` 即可继续握手过程。



##### s.getpeercert([binary_form])

返回来自连接另一端的证书（如果有）。如果没有证书，则返回 `None`。如果存在证书但未通过验证，则返回一个空字典。如果收到已验证的证书，则返回一个包含 `'subject'` 和 `'notAfter'` 键的字典。如果 *binary_form* 设置为 `True`，则证书将以 DER 编码的字节序列形式返回。

##### s.read([nbytes])

读取最多 *nbytes* 个字节的数据并返回。如果省略 *nbytes*，则最多返回 1,024 个字节。

##### s.write(data)

写入字节字符串 *data*。返回写入的字节数。

##### s.unwrap()

关闭 SSL 连接并返回底层套接字对象，可以继续在该对象上进行未加密的通信。

该模块还定义了以下实用函数：

##### cert_time_to_seconds(timestring)

将字符串 *timestring* 从证书中使用的格式转换为与 `time.time()` 函数兼容的浮点数。

##### DER_cert_to_PEM_cert(derbytes)

给定包含 DER 编码证书的字节字符串 *derbytes*，返回 PEM 编码的证书字符串版本。

##### PEM_cert_to_DER_cert(pemstring)

给定包含 PEM 编码证书字符串版本的字符串 *pemstring*，返回 DER 编码的证书字节字符串版本。

##### get_server_certificate(addr [, ssl_version [, ca_certs]])

检索 SSL 服务器的证书并以 PEM 编码的字符串形式返回。*addr* 是 `(hostname, port)` 形式的地址。*ssl_version* 是 SSL 版本号，*ca_certs* 是包含证书颁发机构证书的文件名，其描述与 `wrap_socket()` 函数相同。

##### RAND_status()

如果 SSL 层认为伪随机数生成器已用足够的随机性播种，则返回 `True`，否则返回 `False`。

##### RAND_egd(path)

从熵收集守护进程读取 256 个字节的随机性并将其添加到伪随机数生成器中。*path* 是守护进程的 UNIX 域套接字名称。

##### RAND_add(bytes, entropy)

将字节字符串 *bytes* 中的字节添加到伪随机数生成器中。*entropy* 是一个非负浮点数，表示熵的下界。

##### Examples

以下示例展示了如何使用此模块打开 SSL 客户端连接：

```python
import socket, ssl

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
ssl_s = ssl.wrap_socket(s)
ssl_s.connect(('gmail.google.com',443))
print(ssl_s.cipher())
# Send a request
ssl_s.write(b"GET / HTTP/1.0\r\n\r\n")
# Get the response
while True:
    data = ssl_s.read()
    if not data: break
    print(data)
ssl_s.close()
```

这是一个 SSL 安全时间服务器的示例：

```python
import socket, ssl, time

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR,1)
s.bind(('',12345))
s.listen(5)

while True:
    client, addr = s.accept()     # Get a connection
    print("Connection from", addr)
    client_ssl = ssl.wrap_socket(client,
                                  server_side=True,
                                  certfile="timecert.pem")

    client_ssl.sendall(b"HTTP/1.0 200 OK\r\n")
    client_ssl.sendall(b"Connection: Close\r\n")
    client_ssl.sendall(b"Content-type: text/plain\r\n\r\n")
    resp = time.ctime() + "\r\n"
    client_ssl.sendall(resp.encode('latin-1'))
    client_ssl.close()
    client.close()
```

为了运行此服务器，您需要在文件 `timecert.pem` 中拥有已签名的服务器证书。出于测试目的，您可以使用此 UNIX 命令创建一个：

```
% openssl req -new -x509 -days 30 -nodes -out timecert.pem -keyout timecert.pem
```

要测试此服务器，请尝试使用类似 `'https://localhost:1234'` 的 URL 通过浏览器连接。如果正常工作，浏览器会发出有关您使用自签名证书的警告消息。如果您同意，您应该能看到服务器的输出。

#### SocketServer

此模块在 Python 3 中称为 `socketserver`。`SocketServer` 模块提供了一些类，可以简化 TCP、UDP 和 UNIX 域套接字服务器的实现。

##### 处理程序

要使用该模块，您需要定义一个继承自基类 `BaseRequestHandler` 的处理程序类。`BaseRequestHandler` 的实例 *h* 实现以下一个或多个方法：

**h.finish()**

在 `handle()` 方法完成后调用以执行清理操作。默认情况下，它不执行任何操作。如果 `setup()` 或 `handle()` 方法生成异常，则不会调用它。

**h.handle()**

此方法被调用以执行请求的实际工作。它被调用时不带参数，但几个实例变量包含有用的值。`h.request` 包含请求，`h.client_address` 包含客户端地址，`h.server` 包含调用处理程序的服务器实例。对于流服务（如 TCP），`h.request` 属性是一个套接字对象。对于数据报服务，它是包含接收到的数据的字节字符串。

**h.setup()**

此方法在 `handle()` 方法之前被调用以执行初始化操作。默认情况下，它不执行任何操作。如果您希望服务器实现进一步的连接设置（例如建立 SSL 连接），可以在此处实现。

这是一个处理程序类的示例，实现了一个支持流或数据报的简单时间服务器：

```python
try:
    from socketserver import BaseRequestHandler  # Python 3
except ImportError:
    from SocketServer import BaseRequestHandler  # Python 2
import socket
import time

class TimeServer(BaseRequestHandler):
    def handle(self):
        resp = time.ctime() + "\r\n"
        if isinstance(self.request,socket.socket):
            # A stream-oriented connection
            self.request.sendall(resp.encode('latin-1'))
        else:
            # A datagram-oriented connection
            self.server.socket.sendto(resp.encode('latin-1'),self.client_address)
```

如果您知道处理程序只处理面向流的连接（如 TCP），可以让它继承 `StreamRequestHandler` 而不是 `BaseRequestHandler`。此类设置两个属性：`h.wfile` 是一个类文件对象，用于向客户端写入数据；`h.rfile` 是一个类文件对象，用于从客户端读取数据。以下是示例：

```python
try:
    from socketserver import StreamRequestHandler  # Python 3
except ImportError:
    from SocketServer import StreamRequestHandler  # Python 2
import time

class TimeServer(StreamRequestHandler):
    def handle(self):
        resp = time.ctime() + "\r\n"
        self.wfile.write(resp.encode('latin-1'))
```

如果您正在编写仅处理数据包并总是向发送者发送响应的处理程序，可以让它继承 `DatagramRequestHandler` 而不是 `BaseRequestHandler`。它提供与 `StreamRequestHandler` 相同的类文件接口。例如：

```python
try:
    from socketserver import DatagramRequestHandler  # Python 3
except ImportError:
    from SocketServer import DatagramRequestHandler  # Python 2
import time

class TimeServer(DatagramRequestHandler):
    def handle(self):
        resp = time.ctime() + "\r\n"
        self.wfile.write(resp.encode('latin-1'))
```

在这种情况下，所有写入 `self.wfile` 的数据被收集到一个数据包中，并在 `handle()` 方法返回后返回。

##### 服务器

要使用处理程序，必须将其插入服务器对象。定义了四个基本服务器类：

- **TCPServer(address, handler)** —— 支持使用 IPv4 的 TCP 协议的服务器。*address* 是 `(host, port)` 形式的元组。*handler* 是稍后描述的 `BaseRequestHandler` 类子类的实例。

- **UDPServer(address, handler)** —— 支持使用 IPv4 的 Internet UDP 协议的服务器。*address* 和 *handler* 与 `TCPServer()` 相同。

- **UnixStreamServer(address, handler)** —— 使用 UNIX 域套接字实现面向流协议的服务器。继承自 `TCPServer`。

- **UnixDatagramServer(address, handler)** —— 使用 UNIX 域套接字实现数据报协议的服务器。继承自 `UDPServer`。

所有四个服务器类的实例都具有以下基本方法：

**s.fileno()**

返回服务器套接字的整数文件描述符。此方法的存在使得在轮询操作（如 `select()` 函数）中使用服务器实例成为合法操作。

**s.serve_forever()**

处理无限数量的请求。



s.shutdown()

停止 `serve_forever()` 循环。

以下属性提供了一些关于正在运行的服务器配置的基本信息：

**s.RequestHandlerClass**

传递给服务器构造函数的用户提供的请求处理程序类。

**s.server_address**

服务器正在监听的地址，例如元组 `('127.0.0.1', 80)`。

**s.socket**

用于处理传入请求的套接字对象。

以下是将 `TimeHandler` 作为 TCP 服务器运行的示例：

```
from SocketServer import TCPServer

serv = TCPServer(('',10000), TimeHandler)
serv.serve_forever()
```

以下是将处理程序作为 UDP 服务器运行的示例：

```
from SocketServer import UDPServer

serv = UDPServer(('',10000), TimeHandler)
serv.serve_forever()
```

`SocketServer` 模块的一个关键方面是处理程序与服务器是解耦的。也就是说，一旦你编写了一个处理程序，就可以将其插入许多不同类型的服务器中，而无需更改其实现。

##### 定义自定义服务器

服务器通常需要特殊的配置以适应不同的网络地址族、超时、并发和其他特性。这种自定义是通过继承前一节描述的四种基本服务器之一来完成的。可以定义以下类属性来自定义底层网络套接字的基本设置：

**Server.address_family**

服务器套接字使用的地址族。默认值为 `socket.AF_INET`。如果要使用 IPv6，请使用 `socket.AF_INET6`。

**Server.allow_reuse_address**

一个布尔标志，指示套接字是否应重用地址。当程序终止后你想立即在同一端口上重启服务器时，这很有用（否则，你必须等待几分钟）。默认值为 `False`。

**Server.request_queue_size**

传递给套接字 `listen()` 方法的请求队列大小。默认值为 `5`。

**Server.socket_type**

服务器使用的套接字类型，例如 `socket.SOCK_STREAM` 或 `socket.SOCK_DGRAM`。

**Server.timeout**

服务器等待新请求的超时时间（以秒为单位）。超时后，服务器调用 `handle_timeout()` 方法（如下所述）并返回等待状态。此超时*不*用于设置套接字超时。但是，如果已设置套接字超时，则使用其值而不是此值。

以下是创建一个允许重用端口号的服务器的示例：

```
from SocketServer import TCPServer

class TimeServer(TCPServer):
    allow_reuse_address = True

serv = TimeServer(('',10000), TimeHandler)
serv.serve_forever()
```

如果需要，以下方法在继承自其中一种服务器的类中扩展最为有用。如果你在自己的服务器中定义了任何这些方法，请确保在超类中调用相同的方法。

**Server.activate()**

在服务器上执行 `listen()` 操作的方法。服务器套接字通过 `self.socket` 引用。

**Server.bind()**

在服务器上执行 `bind()` 操作的方法。

**Server.handle_error(request, client_address)**

处理处理过程中发生的未捕获异常的方法。要获取有关最后一个异常的信息，请使用 `sys.exc_info()` 或 `traceback` 模块中的函数。

**Server.handle_timeout()**

服务器超时时调用的方法。通过重新定义此方法并调整超时设置，你可以将其他处理集成到服务器事件循环中。

**Server.verify_request(request, client_address)**

如果你想在进一步处理之前验证连接，请重新定义此方法。如果你想实现防火墙或执行其他类型的验证，可以定义此方法。

最后，可以通过使用混入类来获得额外的服务器功能。这就是如何添加通过线程或进程分叉实现并发的方式。为此目的定义了以下类：

##### ForkingMixIn

一个混入类，用于向服务器添加 UNIX 进程分叉功能，使其能够为多个客户端提供服务。类变量 `max_children` 控制最大子进程数，`timeout` 变量确定在尝试收集僵尸进程之间经过的时间。一个实例变量 `active_children` 跟踪正在运行的活动进程数。

##### ThreadingMixIn

一个混入类，用于修改服务器，使其能够使用线程为多个客户端提供服务。对可以创建的线程数量没有限制。默认情况下，线程是非守护线程的，除非类变量 `daemon_threads` 设置为 `True`。

要将这些功能添加到服务器中，你需要使用多重继承，其中混入类列在第一位。例如，这是一个分叉时间服务器：

```
from SocketServer import TCPServer, ForkingMixIn

class TimeServer(ForkingMixIn, TCPServer):
    allow_reuse_address = True
    max_children = 10

serv = TimeServer(('',10000), TimeHandler)
serv.serve_forever()
```

由于并发服务器相对常见，`SocketServer` 预定义了以下服务器类以实现此目的。

- `ForkingUDPServer(address, handler)`
- `ForkingTCPServer(address, handler)`
- `ThreadingUDPServer(address, handler)`
- `ThreadingTCPServer(address, handler)`

这些类实际上是根据混入类和服务器类定义的。例如，这是 `ForkingTCPServer` 的定义：

```
class ForkingTCPServer(ForkingMixIn, TCPServer): pass
```

##### 应用服务器的自定义

其他库模块通常使用 `SocketServer` 类来为应用层协议（如 HTTP 和 XML-RPC）实现服务器。这些服务器也可以通过继承和扩展为基本服务器操作定义的方法来自定义。例如，这是一个分叉的 XML-RPC 服务器，它只接受来自环回接口的连接：

```
try:
    from xmlrpc.server import SimpleXMLRPCServer     # Python 3
    from socketserver import ForkingMixIn
except ImportError:                                  # Python 2
    from SimpleXMLRPCServer import SimpleXMLRPCServer
    from SocketServer import ForkingMixIn

class MyXMLRPCServer(ForkingMixIn, SimpleXMLRPCServer):
    def verify_request(self, request, client_address):
        host, port = client_address
        if host != '127.0.0.1':
            return False
        return SimpleXMLRPCServer.verify_request(self, request, client_address)

##### 使用示例
def add(x, y):
    return x + y
server = MyXMLRPCServer(("", 45000))
server.register_function(add)
server.serve_forever()
```

要测试这个，你需要使用 `xmlrpclib` 模块。运行上面的服务器，然后启动一个单独的 Python 进程：

```
>>> import xmlrpclib
>>> s = xmlrpclib.ServerProxy("http://localhost:45000")
>>> s.add(3, 4)
7
>>>
```

要测试拒绝连接，请尝试相同的代码，但从网络上的另一台机器执行。为此，你需要将 `"localhost"` 替换为运行服务器的计算机的主机名。

## 互联网应用编程

本章描述与互联网应用协议相关的模块，包括 HTTP、XML-RPC、FTP 和 SMTP。Web 编程主题（如 CGI 脚本）在第 23 章 “Web 编程” 中介绍。与处理常见互联网相关数据格式相关的模块在第 24 章 “互联网数据处理和编码” 中介绍。

网络相关库模块的组织结构是 Python 2 和 Python 3 之间存在显著差异的一个领域。为了向前看，本章假设使用 Python 3 库组织，因为它更有逻辑。然而，在撰写本文时，库模块在 Python 版本之间提供的功能实际上相同。适用时，每节中会注明 Python 2 模块名称。

#### ftplib

ftplib 模块实现了 FTP 协议的客户端。很少需要直接使用此模块，因为 urllib 包提供了更高级别的接口。但是，如果你想对 FTP 连接的底层细节有更多控制，此模块可能仍然有用。为了使用此模块，了解 FTP 协议的一些细节（在 Internet RFC 959 中描述）可能会有所帮助。

为建立 FTP 连接定义了一个类：

```
FTP([host [, user [, passwd [, acct [, timeout]]]])
```

创建一个表示 FTP 连接的对象。host 是一个指定主机名的字符串。user、passwd 和 acct 可选地指定用户名、密码和帐户。如果未给出参数，则必须显式调用 connect() 和 login() 方法来启动实际连接。如果给出了 host，则会自动调用 connect()。如果给出了 user、passwd 和 acct，则调用 login()。timeout 是以秒为单位的超时时间。

FTP 的实例 f 具有以下方法：

```
f.abort()
```

尝试中止正在进行的文件传输。这是否有效取决于远程服务器。



##### 示例

以下示例展示了如何使用此模块将文件上传到 FTP 服务器：

```
host     = "ftp.foo.com"
username = "dave"
password = "1235"
filename = "somefile.dat"

import ftplib
ftp_serv = ftplib.FTP(host,username,password)
# Open the file you want to send
f = open(filename,"rb")
# Send it to the FTP server
resp = ftp_serv.storbinary("STOR "+filename, f)
# Close the connection
ftp_serv.close()
```

要从 FTP 服务器获取文档，请使用 urllib 包。例如：

```
try:
    from urllib.request import urlopen  # Python 3
except ImportError:
    from urllib2 import urlopen         # Python 2

u = urlopen("ftp://username:password@somehostname/somefile")
contents = u.read()
```

#### http 包

http 包由编写 HTTP 客户端和服务器的模块以及状态管理（cookies）支持组成。超文本传输协议（HTTP）是一种简单的基于文本的协议，其工作方式如下：

1.  客户端连接到 HTTP 服务器并发送如下形式的请求头：

```
GET /document.html HTTP/1.0
Connection: Keep-Alive
User-Agent: Mozilla/4.61 [en] (X11; U; SunOS 5.6 sun4u)
Host: rustler.cs.uchicago.edu:8000
Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, image/png, */*
Accept-Encoding: gzip
Accept-Language: en
Accept-Charset: iso-8859-1,*,utf-8

Optional data
...
```

第一行定义了请求类型、文档（选择器）和协议版本。请求行之后是一系列包含客户端各种信息的报头行，例如密码、cookie、缓存首选项和客户端软件。报头行之后是一个空行，表示报头行结束。报头之后，如果请求是从表单发送信息或上传文件，则可能会出现数据。报头中的每一行都应以回车符和换行符（`'\r\n'`）结束。

2.  服务器发送如下形式的响应：

```
HTTP/1.0 200 OK
Content-type: text/html
Content-length: 72883 bytes
...
Header: data

Data
...
```

服务器响应的第一行表示 HTTP 协议版本、成功代码和返回消息。响应行之后是一系列报头字段，包含有关返回文档类型、文档大小、Web 服务器软件、cookie 等的信息。报头以单个空行结束，后面是请求文档的原始数据。

最常见的请求方法如下：

| 方法 | 描述 |
|--------|-------------|
| GET | 获取文档。 |
| POST | 将数据发布到表单。 |
| HEAD | 仅返回报头信息。 |
| PUT | 将数据上传到服务器。 |

表 22.1 中详述的响应代码是服务器最常返回的。符号常量列是 `http.client` 中预定义变量的名称，它保存整数响应代码值，可在代码中使用以提高可读性。

**表 22.1 服务器常返回的响应代码**

| 代码 | 描述 | 符号常量 |
|------|-------------|-------------------|
| **成功代码 (2xx)** | | |
| 200 | 成功 | OK |
| 201 | 已创建 | CREATED |
| 202 | 已接受 | ACCEPTED |
| 204 | 无内容 | NO_CONTENT |
| **重定向 (3xx)** | | |
| 300 | 多种选择 | MULTIPLE_CHOICES |
| 301 | 永久移动 | MOVED_PERMANENTLY |
| 302 | 临时移动 | MOVED_TEMPORARILY |
| 303 | 未修改 | NOT_MODIFIED |

`f.close()` 关闭 FTP 连接。调用此方法后，无法再对 FTP 对象 `f` 执行任何操作。

`f.connect(host [, port [, timeout]])` 打开到指定主机和端口的 FTP 连接。`host` 是指定主机名的字符串。`port` 是 FTP 服务器的整数端口号，默认为 21 端口。`timeout` 是以秒为单位的超时时间。如果已经向 `FTP()` 提供了主机名，则无需调用此方法。

`f.cwd(pathname)` 将服务器上的当前工作目录更改为 `pathname`。

`f.delete(filename)` 从服务器删除文件 `filename`。

`f.dir([dirname [, ... [, callback]]])` 生成由 'LIST' 命令产生的目录列表。`dirname` 可选地提供要列出的目录名称。此外，如果提供了任何其他参数，它们将作为附加参数传递给 'LIST'。如果最后一个参数 `callback` 是一个函数，它将用作处理返回的目录列表数据的回调函数。此回调函数的工作方式与 `retrlines()` 方法使用的回调相同。默认情况下，此方法将目录列表打印到 `sys.stdout`。

`f.login([user, [passwd [, acct]]])` 使用指定的用户名、密码和帐户登录到服务器。`user` 是提供用户名的字符串，默认为 'anonymous'。`passwd` 是包含密码的字符串，默认为空字符串 ''。`acct` 是一个字符串，默认为空字符串。如果这些信息已经提供给 `FTP()`，则无需调用此方法。

`f.mkd(pathname)` 在服务器上创建一个新目录。

`f.ntransfercmd(command [, rest])` 与 `transfercmd()` 相同，但返回一个元组 `(sock, size)`，其中 `sock` 是对应于数据连接的套接字对象，`size` 是数据的预期大小（以字节为单位），如果无法确定大小则为 `None`。

`f.pwd()` 返回一个包含服务器上当前工作目录的字符串。

`f.quit()` 通过向服务器发送 'QUIT' 命令来关闭 FTP 连接。

`f.rename(oldname, newname)` 重命名服务器上的一个文件。

`f.retrbinary(command, callback [, blocksize [, rest]])` 使用二进制传输模式在服务器上执行命令并返回结果。*command* 是一个字符串，指定适当的文件检索命令，几乎总是 `'RETR filename'`。*callback* 是一个回调函数，每接收到一个数据块时调用。此回调函数使用单个参数调用，该参数是以字符串形式接收的数据。*blocksize* 是要使用的最大块大小，默认为 8192 字节。*rest* 是可选的文件偏移量。如果提供，这指定了要开始传输的文件位置。但是，并非所有 FTP 服务器都支持此功能，因此这可能会导致 `error_reply` 异常。

`f.retrlines(command [, callback])` 使用文本传输模式在服务器上执行命令并返回结果。*command* 是一个指定命令的字符串，通常是类似 `'RETR filename'` 的内容。*callback* 是一个回调函数，每接收到一行数据时调用。此回调函数使用单个参数调用，该参数是包含接收数据的字符串。如果省略 *callback*，则返回的数据将打印到 `sys.stdout`。

`f.rmd(pathname)` 从服务器删除一个目录。

`f.sendcmd(command)` 向服务器发送一个简单命令并返回服务器响应。*command* 是包含命令的字符串。此方法仅应用于不涉及数据传输的命令。

`f.set_pasv(pasv)` 设置被动模式。*pasv* 是一个布尔标志，如果为 `True` 则打开被动模式，如果为 `False` 则关闭。默认情况下，被动模式是开启的。

`f.size(filename)` 返回 *filename* 的大小（以字节为单位）。如果由于某种原因无法确定大小，则返回 `None`。

`f.storbinary(command, file [, blocksize])` 在服务器上执行命令并使用二进制传输模式传输数据。*command* 是一个指定低级命令的字符串。它几乎总是设置为 `'STOR filename'`，其中 *filename* 是要放置在服务器上的文件名。*file* 是一个打开的文件对象，将使用 `file.read(blocksize)` 从中读取数据并传输到服务器。*blocksize* 是传输中使用的块大小。默认为 8192 字节。

`f.storlines(command, file)` 在服务器上执行命令并使用文本传输模式传输数据。*command* 是一个指定低级命令的字符串。通常是 `'STOR filename'`。*file* 是一个打开的文件对象，将使用 `file.readline()` 从中读取数据并发送到服务器。

`f.transfercmd(command [, rest])` 在 FTP 数据连接上发起传输。如果使用主动模式，这会发送 'PORT' 或 'EPRT' 命令并接受来自服务器的连接。如果使用被动模式，这会发送 'EPSV' 或 'PASV' 命令，然后连接到服务器。无论哪种情况，一旦数据连接建立，就会发出 *command* 中的 FTP 命令。此函数返回一个对应于打开的数据连接的套接字对象。可选的 *rest* 参数指定服务器上请求文件的起始字节偏移量。但是，并非所有服务器都支持此功能，并且可能导致 `error_reply` 异常。



###### 表格 22.1 续

| 代码 | 描述 | 符号常量 |
|------|-------------|-------------------|
| **客户端错误 (4xx)** | | |
| 400 | 错误的请求 | `BAD_REQUEST` |
| 401 | 未授权 | `UNAUTHORIZED` |
| 403 | 禁止访问 | `FORBIDDEN` |
| 404 | 未找到 | `NOT_FOUND` |
| **服务器错误 (5xx)** | | |
| 500 | 内部服务器错误 | `INTERNAL_SERVER_ERROR` |
| 501 | 未实现 | `NOT_IMPLEMENTED` |
| 502 | 错误的网关 | `BAD_GATEWAY` |
| 503 | 服务不可用 | `SERVICE_UNAVAILABLE` |

同时出现在请求和响应中的头部以一种广为人知的格式（即 RFC-822）进行编码。每个头部的一般形式是*头部名: 数据*，尽管更详细的内容可以在 RFC 中找到。几乎永远不需要解析这些头部，因为 Python 通常会在适用时为你处理它们。

#### http.client (httplib)

`http.client` 模块为 HTTP 的客户端提供了底层支持。在 Python 2 中，此模块名为 `httplib`。请改用 `urllib` 包中的函数。该模块支持 HTTP/1.0 和 HTTP/1.1，并且在 Python 使用 OpenSSL 支持编译时，还允许通过 SSL 建立连接。通常，你不直接使用此包；相反，你应该考虑使用 `urllib` 包。然而，由于 HTTP 是一个非常重要的协议，你可能会遇到需要以 `urllib` 无法轻易解决的方式处理底层细节的情况——例如，如果你想要发送除 `GET` 或 `POST` 以外的命令的请求。有关 HTTP 的更多详细信息，请查阅 RFC 2616 (HTTP/1.1) 和 RFC 1945 (HTTP/1.0)。

以下类可用于与服务器建立 HTTP 连接：

```
HTTPConnection(host [,port])
```

创建一个 HTTP 连接。*host* 是主机名，*port* 是远程端口号。默认端口是 80。返回一个 `HTTPConnection` 实例。

```
HTTPSConnection(host [, port [, key_file=kfile [, cert_file=cfile ]]])
```

创建一个 HTTP 连接，但使用安全套接字。默认端口是 443。*key_file* 和 *cert_file* 是可选的关键字参数，用于指定客户端 PEM 格式的私钥和证书链文件（如果需要进行客户端身份验证）。但是，不会执行服务器证书的验证。返回一个 `HTTPSConnection` 实例。

`HTTPConnection` 或 `HTTPSConnection` 的一个实例，*h*，支持以下方法：

###### h.connect()

初始化与提供给 `HTTPConnection()` 或 `HTTPSConnection()` 的主机和端口的连接。如果尚未建立连接，其他方法会自动调用此方法。

###### h.close()

关闭连接。

###### h.send(bytes)

将一个字节字符串，*bytes*，发送到服务器。不鼓励直接使用此函数，因为它可能会破坏底层的响应/请求协议。它最常用于在调用 `h.endheaders()` 后向服务器发送数据。

###### h.putrequest(method, selector [, skip_host [, skip_accept_encoding]])

向服务器发送一个请求。*method* 是 HTTP 方法，例如 `'GET'` 或 `'POST'`。*selector* 指定要返回的对象，例如 `'/index.html'`。*skip_host* 和 *skip_accept_encoding* 参数是标志，用于禁止在 HTTP 请求中发送 `Host:` 和 `Accept-Encoding:` 头部。默认情况下，这两个参数都为 `False`。因为 HTTP/1.1 协议允许在单个连接上发送多个请求，如果连接处于禁止发出新请求的状态，可能会引发 `CannotSendRequest` 异常。

###### h.putheader(header, value, ...)

向服务器发送一个 RFC-822 风格的头部。它向服务器发送一行，由头部、一个冒号、一个空格和值组成。其他参数被编码为头部的延续行。如果 *h* 不处于允许发送头部的状态，则会引发 `CannotSendHeader` 异常。

###### h.endheaders()

向服务器发送一个空行，表示头部行的结束。

###### h.request(method, url [, body [, headers]])

向服务器发送一个完整的 HTTP 请求。*method* 和 *url* 的含义与 `h.putrequest()` 中的相同。*body* 是一个可选字符串，包含在请求发送后要上传到服务器的数据。如果提供了 *body*，则 `Content-Length:` 头部将自动设置为一个适当的值。*headers* 是一个字典，包含要传递给 `h.putheader()` 方法的*头部:值*对。

###### h.getresponse()

从服务器获取一个响应，并返回一个可用于读取数据的 `HTTPResponse` 实例。如果 *h* 不处于可以接收响应的状态，则会引发 `ResponseNotReady` 异常。

`getresponse()` 方法返回的一个 `HTTPResponse` 实例，*r*，支持以下方法：

```
r.read([size])
```

从服务器读取最多 *size* 个字节。如果省略 *size*，则返回此请求的所有数据。

```
r.getheader(name [,default])
```

获取一个响应头部。*name* 是头部的名称。*default* 是在未找到头部时返回的默认值。

```
r.getheaders()
```

返回一个 `(header, value)` 元组列表。

一个 `HTTPResponse` 实例 `r` 还具有以下属性：

```
r.version
```

服务器使用的 HTTP 版本。

```
r.status
```

服务器返回的 HTTP 状态码。

```
r.reason
```

服务器返回的 HTTP 错误消息。

```
r.length
```

响应中剩余的字节数。

##### 异常

在处理 HTTP 连接的过程中可能会引发以下异常：

| 异常 | 描述 |
| --- | --- |
| `HTTPException` | 所有与 HTTP 相关错误的基类。 |
| `NotConnected` | 发出了请求但未连接。 |
| `InvalidURL` | 提供了错误的 URL 或端口号。 |
| `UnknownProtocol` | 未知的 HTTP 协议号。 |
| `UnknownTransferEncoding` | 未知的传输编码。 |
| `UnimplementedFileMode` | 未实现的文件模式。 |
| `IncompleteRead` | 收到不完整的数据。 |
| `BadStatusLine` | 收到未知的状态码。 |

以下异常与 HTTP/1.1 连接的状态有关。因为 HTTP/1.1 允许在单个连接上发送多个请求/响应，所以对请求何时可以发送和响应何时可以接收施加了额外的规则。以错误的顺序执行操作将产生异常。

| 异常 | 描述 |
| --- | --- |
| `ImproperConnectionState` | 所有 HTTP 连接状态错误的基类。 |
| `CannotSendRequest` | 无法发送请求。 |
| `CannotSendHeader` | 无法发送头部。 |
| `ResponseNotReady` | 无法读取响应。 |

##### 示例

以下示例展示了如何使用 `HTTPConnection` 类通过 POST 请求执行内存高效的文件上传——这是在 `urllib` 框架内不容易实现的。

```
import os
try:
    from httplib import HTTPConnection     # Python 2
except ImportError:
    from http.client import HTTPConnection # Python 3

BOUNDARY = "$Python-Essential-Reference$"
CRLF     = '\r\n'

def upload(addr, url, formfields, filefields):
    # 创建表单字段的各个部分
    formsections = []
    for name in formfields:
        section = [
            '--'+BOUNDARY,
            'Content-disposition: form-data; name="%s"' % name,
            '',
            formfields[name]
        ]
        formsections.append(CRLF.join(section)+CRLF)

    # 收集所有要上传文件的信息
    fileinfo = [(os.path.getsize(filename), formname, filename)
                    for formname, filename in filefields.items()]

    # 为每个文件创建 HTTP 头部
    filebytes = 0
    fileheaders = []
    for filesize, formname,filename in fileinfo:
        headers = [
            '--'+BOUNDARY,
            'Content-Disposition: form-data; name="%s"; filename="%s"' % \
                (formname, filename),
            'Content-length: %d' % filesize,
            ''
        ]
        fileheaders.append(CRLF.join(headers)+CRLF)
        filebytes += filesize

    # 结束标记
    closing = "--"+BOUNDARY+"--\r\n"

    # 确定请求的总长度
    content_size = (sum(len(f) for f in formsections) +
                    sum(len(f) for f in fileheaders) +
                    filebytes+len(closing))

    # 上传它
    conn = HTTPConnection(*addr)
    conn.putrequest("POST",url)
    conn.putheader("Content-type", 'multipart/form-data; boundary=%s' % BOUNDARY)
    conn.putheader("Content-length", str(content_size))
    conn.endheaders()
```



```markdown
# 发送所有表单部分

```python
for s in formsections:
    conn.send(s.encode('latin-1'))

# 发送所有文件
for head, filename in zip(fileheaders, filefields.values()):
    conn.send(head.encode('latin-1'))
    f = open(filename, "rb")
    while True:
        chunk = f.read(16384)
        if not chunk: break
        conn.send(chunk)
    f.close()
conn.send(closing.encode('latin-1'))
r = conn.getresponse()
responsedata = r.read()
conn.close()
return responsedata

# 示例：上传一些文件。表单字段 'name'、'email'
# 'file_1'、'file_2' 等是远程服务器所期望的
# （显然这会因服务器而异）。
server = ('localhost', 8080)
url = '/cgi-bin/upload.py'
formfields = {
    'name': 'Dave',
    'email': 'dave@dabeaz.com'
}
filefields = {
    'file_1': 'IMG_1008.JPG',
    'file_2': 'IMG_1757.JPG'
}
resp = upload(server, url, formfields, filefields)
print(resp)
```

#### http.server (BaseHTTPServer, CGIHTTPServer, SimpleHTTPServer)

`http.server` 模块提供了用于实现 HTTP 服务器的多个类。在 Python 2 中，此模块的内容被拆分到三个库模块中：`BaseHTTPServer`、`CGIHTTPServer` 和 `SimpleHTTPServer`。

##### HTTPServer

以下类实现了一个基本的 HTTP 服务器。在 Python 2 中，它位于 `BaseHTTPServer` 模块中。

```python
HTTPServer(server_address, request_handler)
```

创建一个新的 `HTTPServer` 对象。`server_address` 是一个 `(主机, 端口)` 形式的元组，服务器将在此地址上监听。`request_handler` 是一个从 `BaseHTTPRequestHandler` 派生的处理程序类，将在下文描述。

`HTTPServer` 直接继承自 `socketserver` 模块中定义的 `TCPServer`。因此，如果你想以任何方式自定义 HTTP 服务器的操作，你可以继承 `HTTPServer` 并扩展它。以下是如何定义一个多线程 HTTP 服务器，该服务器仅接受来自特定子网的连接：

```python
try:
    from http.server import HTTPServer          # Python 3
    from socketserver import ThreadingMixIn
except ImportError:
    from BaseHTTPServer import HTTPServer         # Python 2
    from SocketServer import ThreadingMixIn

class MyHTTPServer(ThreadingMixIn, HTTPServer):
    def __init__(self, addr, handler, subnet):
        HTTPServer.__init__(self, addr, handler)
        self.subnet = subnet
    def verify_request(self, request, client_address):
        host, port = client_address
        if not host.startswith(subnet):
            return False
        return HTTPServer.verify_request(self, request, client_address)

# 服务器运行示例
serv = MyHTTPServer(('', 8080), SomeHandler, '192.168.69.')
serv.serve_forever()
```

`HTTPServer` 类只处理底层的 HTTP 协议。要让服务器实际执行任何操作，必须提供一个处理程序类。有两个内置的处理程序和一个基类，可用于定义你自己的自定义处理。接下来将描述这些。

##### SimpleHTTPRequestHandler 和 CGIHTTPRequestHandler

如果你想要快速设置一个简单的独立 Web 服务器，可以使用两个预构建的 Web 服务器处理程序类。这些类独立于任何第三方 Web 服务器（如 Apache）运行。

**CGIHTTPRequestHandler(`request`, `client_address`, `server`)**

从当前目录及其所有子目录提供文件。此外，如果文件位于特殊的 CGI 目录中（由 `cgi_directories` 类变量定义，默认设置为 `['/cgi-bin', '/htbin']`），处理程序将把该文件作为 CGI 脚本运行。处理程序支持 GET、HEAD 和 POST 方法。但是，它不支持 HTTP 重定向（HTTP 代码 302），这将其用途限制在更简单的 CGI 应用程序。出于安全目的，CGI 脚本以 nobody 的 UID 执行。在 Python 2 中，此类在 `CGIHTTPServer` 模块中定义。

**SimpleHTTPRequestHandler(`request`, `client_address`, `server`)**

从当前目录及其所有子目录提供文件。该类分别提供对 HEAD 和 GET 请求的支持。所有 IOError 异常都会导致 "404 File not found" 错误。尝试访问目录会导致 "403 Directory listing not supported" 错误。在 Python 2 中，此类在 `SimpleHTTPServer` 模块中定义。

这两个处理程序都定义了以下类变量，可以通过继承来更改：

**handler.server_version**

返回给客户端的服务器版本字符串。默认情况下，这被设置为类似 `'SimpleHTTP/0.6'` 的字符串。

###### handler.extensions_map

一个将后缀映射到 MIME 类型的字典。未识别的文件类型被视为 `'application/octet-stream'` 类型。

以下是如何使用这些处理程序类运行一个能够执行 CGI 脚本的独立 Web 服务器的示例：

```python
try:
    from http.server import HTTPServer, CGIHTTPRequestHandler  # Python 3
except ImportError:
    from BaseHTTPServer import HTTPServer              # Python 2
    from CGIHTTPServer import CGIHTTPRequestHandler
import os

# 更改到文档根目录
os.chdir("/home/httpd/html")
# 在端口 8080 上启动 CGIHTTP 服务器
serv = HTTPServer(("", 8080), CGIHTTPRequestHandler)
serv.serve_forever()
```

##### BaseHTTPRequestHandler

`BaseHTTPRequestHandler` 类是一个基类，如果你想定义自己的自定义 HTTP 服务器处理，则使用它。预构建的处理程序（如 `SimpleHTTPRequestHandler` 和 `CGIHTTPRequestHandler`）继承自此类。在 Python 2 中，此类在 `BaseHTTPServer` 模块中定义。

###### BaseHTTPRequestHandler(request, client_address, server)

用于处理 HTTP 请求的基础处理程序类。当收到连接时，会解析请求和 HTTP 头。然后尝试基于请求类型执行一个形式为 `do_REQUEST` 的方法。例如，`'GET'` 方法调用 `do_GET()`，`'POST'` 方法调用 `do_POST`。默认情况下，此类不执行任何操作，因此期望在子类中定义这些方法。

`BaseHTTPRequestHandler` 定义了以下类变量，可以在子类中重新定义。

###### BaseHTTPRequestHandler.server_version

指定服务器报告给客户端的服务器软件版本字符串——例如，`'ServerName/1.2'`。

###### BaseHTTPRequestHandler.sys_version

Python 系统版本，例如 `'Python/2.6'`。

###### BaseHTTPRequestHandler.error_message_format

用于构建发送给客户端的错误消息的格式字符串。格式字符串应用于一个包含 `code`、`message` 和 `explain` 属性的字典。例如：

```html
'''<head>
  <title>Error response</title>
</head>
<body>
  <h1>Error response</h1>
  <p>Error code %(code)d.
  <p>Message: %(message)s.
  <p>Error code explanation: %(code)s = %(explain)s.
</body>'''
```

###### BaseHTTPRequestHandler.protocol_version

响应中使用的 HTTP 协议版本。默认值为 `'HTTP/1.0'`。

###### BaseHTTPRequestHandler.responses

将整数 HTTP 错误代码映射到描述问题的二元组 `(message, explain)`。例如，整数代码 `404` 映射到 `("Not Found", "Nothing matches the given URI")`。此映射中的整数代码和字符串在创建错误消息时使用，如前面显示的 `error_message_format` 属性中所定义。

当为处理连接而创建时，`BaseHTTPRequestHandler` 的实例 `b` 具有以下属性：

| 属性 | 描述 |
| --- | --- |
| `b.client_address` | 客户端地址，为元组 `(host, port)`。 |
| `b.command` | 请求类型，例如 `'GET'`、`'POST'`、`'HEAD'` 等。 |
| `b.path` | 请求路径，例如 `'/index.html'`。 |
| `b.request_version` | 请求中的 HTTP 版本字符串，例如 `'HTTP/1.0'`。 |
| `b.headers` | 存储在映射对象中的 HTTP 头。要测试或提取头的内容，请使用字典操作，例如 `headername in b.headers` 或 `headerval = b.headers[headername]`。 |
| `b.rfile` | 用于读取可选输入数据的输入流。当客户端上传数据时使用（例如，在 `POST` 请求期间）。 |
| `b.wfile` | 用于将响应写回客户端的输出流。 |

以下方法通常在子类中使用或重新定义：

`b.send_error(code [, message])`

发送针对不成功请求的响应。`code` 是数字 HTTP 响应代码。`message` 是可选的错误消息。调用 `log_error()` 以记录错误。此方法使用 `error_message_format` 类变量创建完整的错误响应，将其发送给客户端，并关闭连接。调用此方法后不应执行进一步操作。

`b.send_response(code [, message])`

发送针对成功请求的响应。发送 HTTP 响应行，然后发送 `Server` 和 `Date` 头。`code` 是 HTTP 响应代码，`message` 是可选消息。调用 `log_request()` 以记录请求。

`b.send_header(keyword, value)`

将 MIME 头条目写入输出流。`keyword` 是头关键字，`value` 是其值。这应该在 `send_response()` 之后调用。

`b.end_headers()`

发送一个空行以表示 MIME 头结束。
```

# 第22章 Internet应用编程

`b.log_request([code [, size]])`

记录一条成功请求日志。`code` 是HTTP状态码，`size` 是响应的字节大小（如果可用）。默认情况下，会调用 `log_message()` 进行日志记录。

`b.log_error(format, ...)`

记录一条错误消息。默认情况下，会调用 `log_message()` 进行日志记录。

`b.log_message(format, ...)`

向 `sys.stderr` 记录一条任意消息。`format` 是应用于所有附加参数的格式字符串。客户端地址和当前时间会作为前缀添加到每条消息中。

下面是一个创建自定义HTTP服务器的示例，该服务器在单独的线程中运行，允许你监控字典的内容，并将请求路径解释为键。

```python
try:
    from http.server import BaseHTTPRequestHandler, HTTPServer     # Py 3
except ImportError:
    from BaseHTTPServer import BaseHTTPRequestHandler, HTTPServer   # Py 2

class DictRequestHandler(BaseHTTPRequestHandler):
    def __init__(self,thedict,*args,**kwargs):
        self.thedict = thedict
        BaseHTTPRequestHandler.__init__(self,*args,**kwargs)

    def do_GET(self):
        key = self.path[1:]      # Strip the leading '/'
        if not key in self.thedict:
            self.send_error(404, "No such key")
        else:
            self.send_response(200)
            self.send_header('content-type','text/plain')
            self.end_headers()
            resp  = "Key  : %s\n" % key
            resp += "Value: %s\n" % self.thedict[key]
            self.wfile.write(resp.encode('latin-1'))

##### Example use
d = {
    'name' : 'Dave',
    'values' : [1,2,3,4,5],
    'email' : 'dave@dabeaz.com'
}
from functools import partial
serv = HTTPServer(("",9000), partial(DictRequestHandler,d))

import threading
d_mon = threading.Thread(target=serv.serve_forever)
d_mon.start()
```

要测试此示例，请运行服务器，然后在浏览器中输入诸如 `http://localhost:9000/name` 或 `http://localhost:9000/values` 的URL。如果一切正常，你将看到字典的内容被显示出来。

此示例还展示了一种让服务器使用额外参数实例化处理程序类的技巧。通常情况下，服务器使用一组预定义的参数来创建处理程序，并将其传递给 `__init__()`。如果你希望添加额外的参数，可以如示例所示使用 `functools.partial()` 函数。这将创建一个可调用对象，其中包含你的额外参数，同时保留服务器所期望的调用签名。

#### http.cookies（Cookie）

`http.cookies` 模块提供了服务器端对HTTP Cookie操作的支持。在Python 2中，该模块名为 `Cookie`。

Cookie用于在实现会话、用户登录及相关功能的服务器中提供状态管理。要将Cookie发送到用户的浏览器，HTTP服务器通常会在HTTP响应中添加类似以下内容的HTTP头：

```
Set-Cookie: session=8273612; expires=Sun, 18-Feb-2001 15:00:00 GMT; \
            path=/; domain=foo.bar.com
```

另外，也可以通过在HTML文档的 `<head>` 部分嵌入JavaScript来设置Cookie：

```html
<SCRIPT LANGUAGE="JavaScript">
document.cookie = "session=8273612; expires=Sun, 18-Feb-2001 15:00:00 GMT; \
  Feb 17; Path=/; Domain=foo.bar.com;"
</SCRIPT>
```

`http.cookies` 模块通过提供一个特殊的类字典对象来简化生成Cookie值的任务，该对象存储和管理被称为 *morsel* 的Cookie值集合。每个morsel都有一个名称、一个值和一组可选属性，这些属性包含要提供给浏览器的元数据（`expires`、`path`、`comment`、`domain`、`max-age`、`secure`、`version`、`httponly`）。名称通常是一个简单的标识符（如"name"），并且不能与元数据名称（如"expires"或"path"）相同。值通常是一个短字符串。要创建一个这样的Cookie对象：

```python
c = SimpleCookie()
```

接下来，可以使用普通的字典赋值方式来设置Cookie值（morsel）：

```python
c["session"] = 8273612
c["user"] = "beazley"
```

特定morsel的附加属性设置如下：

要生成表示Cookie数据的HTTP头字符串，可以使用 `c.output()` 方法。例如：

```python
print(c.output())
# Produces two lines of output
# Set-Cookie: session=8273612; expires=...; path=/; domain=...
# Set-Cookie: user=beazley
```

当浏览器将Cookie发送回HTTP服务器时，它被编码为 `key=value` 对的字符串，例如 `"session=8273612; user=beazley"`。可选属性（如 `expires`、`path` 和 `domain`）不会被返回。Cookie字符串通常可以在 `HTTP_COOKIE` 环境变量中找到，CGI应用程序可以读取该变量。要恢复Cookie值，请使用类似以下的代码：

```python
c = SimpleCookie(os.environ["HTTP_COOKIE"])
session = c["session"].value
user    = c["user"].value
```

以下文档更详细地描述了 `SimpleCookie` 对象。

###### SimpleCookie([input])

定义一个Cookie对象，其中Cookie值以简单字符串形式存储。

Cookie实例 `c` 提供以下方法：

####### c.output([attrs [,header [,sep]]])

生成一个适用于在HTTP头中设置Cookie值的字符串。`attrs` 是一个可选的可选属性列表，用于指定要包含的属性（`"expires"`、`"path"`、`"domain"` 等）。默认情况下，包含所有Cookie属性。`header` 是要使用的HTTP头（默认为 `'Set-Cookie:'`）。`sep` 是用于连接各头的字符，默认为换行符。

####### c.js_output([attrs])

生成包含JavaScript代码的字符串，该代码在支持JavaScript的浏览器上执行时会设置Cookie。`attrs` 是一个可选的属性列表。

####### c.load(rawdata)

使用 `rawdata` 中找到的数据加载Cookie `c`。如果 `rawdata` 是字符串，则假定其格式与CGI程序中的 `HTTP_COOKIE` 环境变量相同。如果 `rawdata` 是字典，则通过设置 `c[key]=value` 来解释每个 *键值* 对。

在内部，用于存储Cookie值的 *键值* 对是 `Morsel` 类的实例。`Morsel` 的实例 `m` 的行为类似于字典，允许设置可选的 `"expires"`、`"path"`、`"comment"`、`"domain"`、`"max-age"`、`"secure"`、`"version"` 和 `"httponly"` 键。此外，morsel `m` 具有以下方法和属性：

####### m.value

一个包含Cookie原始值的字符串。

####### m.coded_value

一个包含Cookie编码值的字符串，该值是将要发送给或从浏览器接收的值。

####### m.key

Cookie的名称。

####### m.set(key, value, coded_value)

设置前面展示的 `m.key`、`m.value` 和 `m.coded_value` 的值。

####### m.isReservedKey(k)

测试 `k` 是否是保留关键字，如 `"expires"`、`"path"`、`"domain"` 等。

####### m.output([attrs [,header]])

生成此morsel的HTTP头字符串。`attrs` 是一个可选的附加属性列表，用于指定要包含的属性（`"expires"`、`"path"` 等）。`header` 是要使用的头字符串（默认为 `'Set-Cookie:'`）。

####### m.js_output([attrs])

输出在执行时设置Cookie的JavaScript代码。

####### m.OutputString([attrs])

返回不包含任何HTTP头或JavaScript代码的Cookie字符串。

##### 异常

如果在解析或生成Cookie值期间发生错误，将引发 `CookieError` 异常。

#### http.cookiejar（cookielib）

`http.cookiejar` 模块提供了客户端对HTTP Cookie存储和管理的支持。在Python 2中，该模块名为 `cookielib`。

该模块的主要作用是提供用于存储HTTP Cookie的对象，以便与 `urllib` 包结合使用，`urllib` 包用于访问互联网上的文档。例如，`http.cookiejar` 模块可用于捕获Cookie并在后续的连接请求中重新发送它们。它也可用于处理包含Cookie数据的文件，如各种浏览器创建的文件。

该模块定义了以下对象：

`CookieJar()`

一个管理HTTP Cookie值的对象，用于存储HTTP请求收到的Cookie，并将Cookie添加到发出的HTTP请求中。Cookie完全存储在内存中，当 `CookieJar` 实例被垃圾回收时会丢失。

`FileCookieJar(filename [, delayload ])`

创建一个 `FileCookieJar` 实例，用于将Cookie信息检索和存储到文件中。`filename` 是文件名。`delayload` 如果为 `True`，则启用对文件的延迟访问，即除非按需读取，否则不会读取或存储文件。

`MozillaCookieJar(filename [, delayload ])`

创建一个与Mozilla cookies.txt文件兼容的 `FileCookieJar` 实例。

`LWPCookieJar(filename [, delayload ])`

创建一个与libwww-perl Set-Cookie3文件格式兼容的 `FileCookieJar` 实例。

直接使用这些对象的方法和属性的情况比较少见。如果你需要了解它们的底层编程接口，请参阅在线文档。更常见的方式是直接实例化其中一个Cookie jar对象，并将其插入到需要使用Cookie的其他组件中。本章的 `urllib.request` 部分展示了这样一个示例。

#### smtplib

`smtplib` 模块提供了一个低级别的SMTP客户端接口，可用于通过RFC 821和RFC 1869中描述的SMTP协议发送邮件。该模块包含许多低级别的函数和方法，在在线文档中有详细描述。不过，以下内容涵盖了该模块中最常用的部分：

##### SMTP

`SMTP([host [, port]])`

创建一个表示与 SMTP 服务器连接的对象。如果提供了 `host`，则指定 SMTP 服务器的名称。`port` 是一个可选的端口号。默认端口为 25。如果提供了 `host`，`connect()` 方法将被自动调用。否则，你需要手动调用返回对象上的 `connect()` 来建立连接。

`SMTP` 的实例 `s` 具有以下方法：

`s.connect([host [, port]])`

连接到 `host` 上的 SMTP 服务器。如果省略 `host`，则连接到本地主机（`'127.0.0.1'`）。`port` 是一个可选的端口号，省略时默认为 25。如果在 `SMTP()` 中已提供了主机名，则无需调用 `connect()`。

`s.login(user, password)`

如果需要身份验证，则登录服务器。`user` 是用户名，`password` 是密码。

`s.quit()`

通过向服务器发送 `'QUIT'` 命令来终止会话。

`s.sendmail(fromaddr, toaddrs, message)`

向服务器发送邮件消息。`fromaddr` 是一个包含发件人电子邮件地址的字符串。`toaddrs` 是一个包含收件人电子邮件地址的字符串列表。`message` 是一个包含完全格式化的、符合 RFC-822 标准的消息字符串。通常使用 `email` 包来创建此类消息。需要注意的是，虽然 `message` 可以作为文本字符串提供，但它应仅包含值在 0 到 127 范围内的有效 ASCII 字符。否则，你将得到一个编码错误。如果你需要以不同的编码（如 UTF-8）发送消息，请先将其编码为字节字符串，然后将该字节字符串作为 `message` 提供。

##### 示例

以下示例展示了如何使用该模块发送消息：

```python
import smtplib
fromaddr = "someone@some.com"
toaddrs = ["recipient@other.com"]
msg = "From: %s\r\nTo: %s\r\n\r\n" % (fromaddr, ",".join(toaddrs))
msg += """
Refinance your mortgage to buy stocks and Viagra!
"""

server = smtplib.SMTP('localhost')
server.sendmail(fromaddr, toaddrs, msg)
server.quit()
```

#### urllib 包

`urllib` 包提供了一个高级接口，用于编写需要与 HTTP 服务器、FTP 服务器和本地文件进行交互的客户端。典型应用包括从网页抓取数据、自动化、代理、网络爬虫等。这是可配置性最强的库模块之一，因此这里不会介绍每一个细节。相反，只描述该包最常见的用法。

在 Python 2 中，`urllib` 的功能分布在多个不同的库模块中，包括 `urllib`、`urllib2`、`urlparse` 和 `robotparser`。在 Python 3 中，所有这些功能已被整合并重新组织到 `urllib` 包中。

##### `urllib.request`（`urllib2`）

`urllib.request` 模块提供了用于打开 URL 和从 URL 获取数据的函数和类。在 Python 2 中，此功能位于 `urllib2` 模块中。

该模块最常见的用途是通过 HTTP 从 Web 服务器获取数据。例如，以下代码展示了获取网页的最简单方式：

```python
try:
    from urllib.request import urlopen     # Python 3
except ImportError:
    from urllib2 import urlopen             # Python 2

u = urlopen("http://docs.python.org/3.0/library/urllib.request.html")
data = u.read()
```

当然，在与真实世界中的服务器交互时会出现许多复杂情况。例如，你可能需要考虑代理服务器、身份验证、Cookie、用户代理和其他问题。所有这些都得到了支持，但代码会更加复杂（请继续阅读）。

###### `urlopen()` 和 Request

发出请求最直接的方式是使用 `urlopen()` 函数。

`urlopen(url [, data [, timeout]])`

打开 URL *url* 并返回一个类文件对象，可用于读取返回的数据。*url* 可以是包含 URL 的字符串，也可以是稍后描述的 `Request` 类的实例。*data* 是一个 URL 编码的字符串，包含要上传到服务器的表单数据。提供此参数时，HTTP 将使用 `'POST'` 方法而非 `'GET'`（默认值）。数据通常使用 `urllib.parse.urlencode()` 等函数创建。*timeout* 是一个可选的超时时间（以秒为单位），用于内部使用的所有阻塞操作。

`urlopen()` 返回的类文件对象 *u* 支持以下方法：

| 方法 | 描述 |
|--------|-------------|
| `u.read([nbytes])` | 读取 *nbytes* 个数据并返回字节字符串。 |
| `u.readline()` | 读取单行文本并返回字节字符串。 |
| `u.readlines()` | 读取所有输入行并返回一个列表。 |
| `u.fileno()` | 返回整数文件描述符。 |
| `u.close()` | 关闭连接。 |
| `u.info()` | 返回一个包含与 URL 关联的元信息的映射对象。对于 HTTP，返回服务器响应中包含的 HTTP 头信息。对于 FTP，头信息包含 `'content-length'`。对于本地文件，头信息包含日期、`'content-length'` 和 `'content-type'` 字段。 |
| `u.getcode()` | 以整数形式返回 HTTP 响应代码——例如，200 表示成功，404 表示文件未找到。 |
| `u.geturl()` | 返回实际返回数据的 URL，考虑到可能发生的任何重定向。 |

需要强调的是，类文件对象 `u` 以二进制模式运行。如果你需要将响应数据作为文本处理，则需要使用 `codecs` 模块或其他方式进行解码。

如果在下载过程中发生错误，将引发 `URLError` 异常。这包括与 HTTP 协议本身相关的错误，如访问被拒绝或需要身份验证。对于这类错误，服务器通常会返回包含更具描述性信息的内容。要获取此内容，异常实例本身可以作为类文件对象进行读取。例如：

```python
try:
    u = urlopen("http://www.python.org/perl.html")
    resp = u.read()
except HTTPError as e:
    resp = e.read()
```

使用 `urlopen()` 时一个非常常见的错误是通过代理服务器访问网页。例如，如果你的组织将所有 Web 流量路由通过代理服务器，请求可能会失败。如果代理服务器不需要任何类型的身份验证，你可以通过在 `os.environ` 字典中设置 `HTTP_PROXY` 环境变量来解决此问题。例如，`os.environ['HTTP_PROXY'] = 'http://example.com:12345'`。

对于简单请求，`urlopen()` 的 `url` 参数是一个字符串，如 `'http://www.python.org'`。如果你需要做更复杂的事情，例如修改 HTTP 请求头，则创建一个 `Request` 实例并将其用作 `url` 参数。

`Request(url [, data [, headers [, origin_req_host [, unverifiable]]]])`

创建一个新的 `Request` 实例。`url` 指定 URL（例如，`'http://www.foo.bar/spam.html'`）。`data` 是在 HTTP 请求中上传到服务器的 URL 编码数据。提供此参数时，HTTP 请求类型将从 `'GET'` 变为 `'POST'`。`headers` 是一个字典，包含表示 HTTP 头内容的键值映射。`origin_req_host` 设置为事务的请求主机——通常是发起请求的主机名。如果请求的 URL 是不可验证的，则 `unverifiable` 设置为 `True`。*不可验证的 URL* 非正式地定义为非用户直接输入的 URL——例如，嵌入在页面中用于加载图像的 URL。`unverifiable` 的默认值为 `False`。

`Request` 的实例 `r` 具有以下方法：

`r.add_data(data)`

向请求添加数据。如果请求是 HTTP 请求，则方法更改为 `'POST'`。`data` 是如 `Request()` 所述的 URL 编码数据。这不会将数据追加到任何先前设置的数据中；它只是用 `data` 替换旧数据。

`r.add_header(key, val)`

向请求添加头信息。`key` 是头名称，`val` 是头值。两个参数都是字符串。



`r.add_unredirected_header(key, val)`

将头部信息添加到请求中，但不会将其添加到重定向请求中。`key` 和 `val` 的含义与 `add_header()` 相同。

`r.get_data()`

返回请求数据（如果有的话）。

`r.get_full_url()`

返回请求的完整 URL。

`r.get_host()`

返回请求将发送到的主机。

`r.get_method()`

返回 HTTP 方法，即 'GET' 或 'POST'。

`r.get_origin_req_host()`

返回原始事务的请求主机。

`r.get_selector()`

返回 URL 的选择器部分（例如 '/index.html'）。

`r.get_type()`

返回 URL 类型（例如 'http'）。

`r.has_data()`

如果数据是请求的一部分，返回 True。

`r.is_unverifiable()`

如果请求是不可验证的，返回 True。

`r.has_header(header)`

如果请求包含头部 `header`，返回 True。

`r.set_proxy(host, type)`

为连接代理服务器准备请求。这将原始主机替换为 `host`，将请求的原始类型替换为 `type`。URL 的选择器部分设置为原始 URL。

以下示例展示了如何使用 Request 对象来更改 `urlopen()` 所使用的 'User-Agent' 头部。如果你希望服务器认为你是从 Internet Explorer、Firefox 或其他浏览器发起连接，可以使用此方法。

```python
headers = {
    'User-Agent':
        'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; .NET CLR 2.0.50727)'
}
r = Request("http://somedomain.com/", headers=headers)
u = urlopen(r)
```

## 518 第 22 章 互联网应用编程

###### 自定义 Opener

基本的 `urlopen()` 函数不支持身份验证、Cookie 或其他 HTTP 高级功能。要添加支持，你必须使用 `build_opener()` 函数创建自己的自定义 opener 对象：

```python
build_opener([handler1 [, handler2, ...]])
```

构建一个用于打开 URL 的自定义 opener 对象。参数 `handler1`、`handler2` 等都是特殊 handler 对象的实例。这些 handler 的目的是为最终的 opener 对象添加各种功能。以下列出了所有可用的 handler 对象：

| Handler | 描述 |
| :--- | :--- |
| CacheFTPHandler | 具有持久 FTP 连接的 FTP 处理器 |
| FileHandler | 打开本地文件 |
| FTPHandler | 通过 FTP 打开 URL |
| HTTPBasicAuthHandler | 基本 HTTP 身份验证处理 |
| HTTPCookieProcessor | HTTP Cookie 处理 |
| HTTPDefaultErrorHandler | 通过抛出 HTTPError 异常来处理 HTTP 错误 |
| HTTPDigestAuthHandler | HTTP 摘要身份验证处理 |
| HTTPHandler | 通过 HTTP 打开 URL |
| HTTPRedirectHandler | 处理 HTTP 重定向 |
| HTTPSHandler | 通过安全 HTTP 打开 URL |
| ProxyHandler | 通过代理重定向请求 |
| ProxyBasicAuthHandler | 基本身份验证代理 |
| ProxyDigestAuthHandler | 摘要身份验证代理 |
| UnknownHandler | 处理所有未知 URL 的处理器 |

默认情况下，opener 总是使用 ProxyHandler、UnknownHandler、HTTPHandler、HTTPSHandler、HTTPDefaultErrorHandler、HTTPRedirectHandler、FTPHandler、FileHandler 和 HTTPErrorProcessor 这些 handler 创建。这些 handler 提供了基本级别的功能。作为参数提供的额外 handler 会被添加到此列表中。但是，如果任何额外 handler 的类型与默认 handler 相同，它们将优先生效。例如，如果你添加了 HTTPHandler 的实例或某个派生自 HTTPHandler 的类，它将替代默认的 handler。

`build_opener()` 返回的对象具有一个方法 `open(url [, data [, timeout]])`，用于根据各种 handler 提供的所有规则打开 URL。`open()` 的参数与传递给 `urlopen()` 函数的参数相同。

```python
install_opener(opener)
```

安装一个不同的 opener 对象作为 `urlopen()` 使用的全局 URL opener。`opener` 通常是通过 `build_opener()` 创建的 opener 对象。

接下来的几个小节展示了如何为使用 `urllib.request` 模块时出现的一些更常见的场景创建自定义 opener。

###### 密码身份验证

要处理涉及密码身份验证的请求，你需要创建一个 opener，并向其中添加 `HTTPBasicAuthHandler`、`HTTPDigestAuthHandler`、`ProxyBasicAuthHandler` 或 `ProxyDigestAuthHandler` 这些 handler 的某种组合。每个 handler 都具有以下可用于设置密码的方法：

```python
h.add_password(realm, uri, user, passwd)
```

为给定的域和 URI 添加用户名和密码信息。所有参数都是字符串。`uri` 可以选择性地是一个 URI 序列，在这种情况下，用户名和密码信息将应用于序列中的所有 URI。`realm` 是与身份验证相关联的名称或描述。其值取决于远程服务器。不过，它通常是一组相关网页的通用名称。`uri` 是与身份验证相关联的基础 URL。`realm` 和 `uri` 的典型值类似于 `('Administrator', 'http://www.somesite.com')`。`user` 和 `password` 分别指定用户名和密码。

以下是如何设置具有基本身份验证的 opener 的示例：

```python
auth = HTTPBasicAuthHandler()
auth.add_password("Administrator", "http://www.secretlair.com", "drevil", "12345")

# Create opener with authentication added
opener = build_opener(auth)

# Open URL
u = opener.open("http://www.secretlair.com/evilplan.html")
```

###### HTTP Cookie

要管理 HTTP Cookie，请创建一个添加了 `HTTPCookieProcessor` handler 的 opener 对象。例如：

```python
cookiehand = HTTPCookieProcessor()
opener = build_opener(cookiehand)
u = opener.open("http://www.example.com/")
```

默认情况下，`HTTPCookieProcessor` 使用 `http.cookiejar` 模块中的 `CookieJar` 对象。可以通过向 `HTTPCookieProcessor` 传递不同的 `CookieJar` 对象作为参数来支持不同类型的 Cookie 处理。例如：

```python
cookiehand = HTTPCookieProcessor(
             http.cookiejar.MozillaCookieJar("cookies.txt")
          )
opener = build_opener(cookiehand)
u = opener.open("http://www.example.com/")
```

###### 代理

如果请求需要通过代理重定向，请创建 `ProxyHandler` 的实例。

```python
ProxyHandler([proxies])
```

创建一个将请求通过代理路由的代理处理器。参数 `proxies` 是一个字典，将协议名称（例如 `'http'`、`'ftp'` 等）映射到相应代理服务器的 URL。

以下示例展示了如何使用它：

```python
proxy = ProxyHandler({'http': 'http://someproxy.com:8080/'})
auth = HTTPBasicAuthHandler()
auth.add_password("realm", "host", "username", "password")
opener = build_opener(proxy, auth)

u = opener.open("http://www.example.com/doc.html")
```

##### urllib.response

这是一个内部模块，实现了 `urllib.request` 模块中函数返回的类文件对象。没有公共 API。

##### urllib.parse

`urllib.parse` 模块用于操作 URL 字符串，如 "http://www.python.org"。

###### URL 解析（Python 2 中的 urlparse 模块）

URL 的一般形式为 "scheme://netloc/path;parameters?query#fragment"。此外，URL 的 netloc 部分可能包含端口号（如 "hostname:port"）或用户身份验证信息（如 "user:pass@hostname"）。以下函数用于解析 URL：

```python
urlparse(urlstring [, default_scheme [, allow_fragments]])
```

解析 `urlstring` 中的 URL 并返回一个 ParseResult 实例。`default_scheme` 指定当 URL 中没有方案时使用的方案（"http"、"ftp" 等）。如果 `allow_fragments` 为零，则不允许片段标识符。ParseResult 实例 `r` 是一个形式为 `(scheme, netloc, path, parameters, query, fragment)` 的命名元组。此外，还定义了以下只读属性：

| 属性 | 描述 |
| :--- | :--- |
| r.scheme | URL 方案说明符（例如 'http'） |
| r.netloc | 网络位置说明符（例如 'www.python.org'） |
| r.path | 层级路径（例如 '/index.html'） |
| r.params | 最后一个路径元素的参数 |
| r.query | 查询字符串（例如 'name=Dave&id=42'） |
| r.fragment | 不带前导 '#' 的片段标识符 |
| r.username | 如果网络位置说明符的形式为 'username:password@hostname'，则为用户名组件 |
| r.password | 来自网络位置说明符的密码组件 |
| r.hostname | 来自网络位置说明符的主机名组件 |
| r.port | 如果网络位置说明符的形式为 'hostname:port'，则为端口号 |

ParseResult 实例可以使用 `r.geturl()` 转换回 URL 字符串。



####### urlparse

####### urlunparse(*parts*)

根据 `urlparse()` 返回的 URL 元组表示形式构造 URL 字符串。*parts* 必须是包含六个组件的元组或可迭代对象。

####### urlsplit(*url* [, *default_scheme* [, *allow_fragments*]])

与 `urlparse()` 类似，但 URL 中的 *parameters* 部分在路径中保持不变。这允许解析参数可能附加在单个路径组件上的 URL，例如 `'scheme://netloc/path1;param1/path2;param2/path3?query#fragment'`。结果是一个 `SplitResult` 实例，这是一个包含 (*scheme*, *netloc*, *path*, *query*, *fragment*) 的命名元组。还定义了以下只读属性：

| 属性 | 描述 |
|------|------|
| `r.scheme` | URL 协议方案说明符（例如 `'http'`） |
| `r.netloc` | 网络位置说明符（例如 `'www.python.org'`） |
| `r.path` | 分层路径（例如 `'/index.html'`） |
| `r.query` | 查询字符串（例如 `'name=Dave&id=42'`） |
| `r.fragment` | 不带前导 `'#'` 的片段标识符 |
| `r.username` | 如果网络位置说明符形式为 `'username:password@hostname'`，则包含用户名组件 |
| `r.password` | 来自网络位置说明符的密码组件 |
| `r.hostname` | 来自网络位置说明符的主机名组件 |
| `r.port` | 如果网络位置说明符形式为 `'hostname:port'`，则包含端口号 |

可以使用 `r.geturl()` 将 `SplitResult` 实例转换回 URL 字符串。

####### urlunsplit(*parts*)

根据 `urlsplit()` 创建的元组表示形式构造 URL。*parts* 是包含五个 URL 组件的元组或可迭代对象。

####### urldefrag(*url*)

返回一个元组 `(*newurl*, *fragment*)`，其中 *newurl* 是去掉片段的 *url*，*fragment* 是包含片段部分（如果有的话）的字符串。如果 *url* 中没有片段，则 *newurl* 与 *url* 相同，*fragment* 为空字符串。

####### urljoin(*base*, *url* [, *allow_fragments*])

通过组合基础 URL *base* 和相对 URL *url* 构造一个绝对 URL。*allow_fragments* 的含义与 `urlparse()` 相同。如果基础 URL 的最后一个组件不是目录，则将其剥离。

###### parse_qs(*qs* [, *keep_blank_values* [, *strict_parsing*]])

解析 URL 编码（MIME 类型 `application/x-www-form-urlencoded`）的查询字符串 *qs*，并返回一个字典，其中键是查询变量名，值是为每个名称定义的值的列表。*keep_blank_values* 是一个布尔标志，控制如何处理空值。如果为 `True`，它们将包含在字典中，值设置为空字符串。如果为 `False`（默认值），则将其丢弃。`strict_parsing` 是一个布尔标志，如果为 `True`，则将解析错误转换为 `ValueError` 异常。默认情况下，错误会被静默忽略。

```
parse_qsl(qs [, keep_blank_values [, strict_parsing]])
```

与 `parse_qs()` 类似，但结果是一个键值对列表 `(name, value)`，其中 *name* 是查询变量名，*value* 是其值。

###### URL 编码（Python 2 中的 `urllib` 模块）

以下函数用于对组成 URL 的数据进行编码和解码。

```
quote(string [, safe [, encoding [, errors]]])
```

将 *string* 中的特殊字符替换为适合包含在 URL 中的转义序列。字母、数字以及下划线 (`_`)、逗号 (`,`)、句点 (`.`) 和连字符 (`-`) 字符保持不变。所有其他字符都转换为 `'%xx'` 形式的转义序列。*safe* 提供一个不应被引用的附加字符字符串，默认为 `'/'`。*encoding* 指定用于非 ASCII 字符的编码。默认为 `'utf-8'`。*errors* 指定遇到编码错误时的处理方式，默认为 `'strict'`。*encoding* 和 *errors* 参数仅在 Python 3 中可用。

```
quote_plus(string [, safe [, encoding [, errors]]])
```

调用 `quote()` 并额外将所有空格替换为加号。*string* 和 *safe* 与 `quote()` 中相同。*encoding* 和 *errors* 与 `quote()` 相同。

```
quote_from_bytes(bytes [, safe])
```

与 `quote()` 相同，但接受字节字符串且不执行编码。返回结果是一个文本字符串。仅适用于 Python 3。

```
unquote(string [, encoding [, errors]])
```

将 `'%xx'` 形式的转义序列替换为其对应的单字符。*encoding* 和 *errors* 指定解码 `'%xx'` 转义中数据的编码和错误处理。默认编码为 `'utf-8'`，默认 *errors* 策略为 `'replace'`。*encoding* 和 *errors* 仅适用于 Python 3。

```
unquote_plus(string [, encoding [, errors]])
```

类似于 `unquote()`，但还将加号替换为空格。

```
unquote_to_bytes(string)
```

与 `unquote()` 相同，但不执行解码，返回字节字符串。

```
urlencode(query [, doseq])
```

将 *query* 中的查询值转换为 URL 编码的字符串，适合用作 URL 的 *query* 参数或作为 `POST` 请求的一部分上传。*query* 是一个字典或 `(key, value)` 对的序列。结果字符串是由 `'&'` 字符分隔的一系列 `'key=value'` 对，其中 *key* 和 *value* 都使用 `quote_plus()` 进行引用。*doseq* 参数是一个布尔标志，如果 *query* 中的任何 *value* 是表示同一键的多个值的序列，则应设置为 `True`。在这种情况下，将为 *value* 中的每个 `v` 创建一个单独的 `'key=v'` 字符串。

##### 示例

以下示例展示了如何将查询变量字典转换为适合在 HTTP GET 请求中使用的 URL，以及如何解析 URL：

```
try:
    from urllib.parse import urlparse, urlencode, parse_qsl   # Python 3
except ImportError:
    from urlparse import urlparse, parse_qsl                     # Python 2
    from urllib import urlencode
```

```
# 创建具有正确编码查询变量的 URL 的示例
form_fields = {
    'name'  : 'Dave',
    'email' : 'dave@dabeaz.com',
    'uid'   : '12345'
}
form_data = urlencode(form_fields)
url = "http://www.somehost.com/cgi-bin/view.py?"+form_data
```

```
# 将 URL 解析为组件的示例
r = urlparse(url)
print(r.scheme)      # 'http'
print(r.netloc)      # 'www.somehost.com'
print(r.path)        # '/cgi-bin/view.py'
print(r.params)      # ''
print(r.query)       # 'uid=12345&name=Dave&email=dave%40dabeaz.com'
print(r.fragment)    # ''
```

```
# 提取查询数据
parsed_fields = dict(parse_qsl(r.query))
assert form_fields == parsed_fields
```

##### urllib.error

`urllib.error` 模块定义了 `urllib` 包使用的异常。

###### ContentTooShort

当下载的数据量小于预期量（由 `'Content-Length'` 头定义）时引发。在 Python 2 的 `urllib` 模块中定义。

###### HTTPError

用于指示 HTTP 协议问题。此错误可用于发出需要身份验证等事件的信号。此异常也可用作文件对象，以读取与错误关联的服务器返回的数据。这是 `URLError` 的子类。在 Python 2 的 `urllib2` 模块中定义。

###### URLError

当检测到问题时由处理器引发的错误。这是 `IOError` 的子类。异常实例的 `reason` 属性包含有关问题的更多信息。在 Python 2 的 `urllib2` 模块中定义。

##### urllib.robotparser (robotparser)

`urllib.robotparser` 模块（Python 2 中的 `robotparser`）用于获取和解析用于指示网络爬虫的 `'robots.txt'` 文件的内容。有关更多用法信息，请参阅在线文档。

##### 注意事项

- urllib 包的高级用户几乎可以以任何想象的方式自定义其行为。这包括创建新类型的打开器、处理器、请求、协议等。此主题超出了此处可涵盖的范围，但在线文档提供了一些更多细节。

- Python 2 用户应注意，广泛使用的 `urllib.urlopen()` 函数在 Python 2.6 中已正式弃用，并在 Python 3 中被删除。不应使用 `urllib.urlopen()`，而应使用 `urllib2.urlopen()`，它提供与本文所述的 `urllib.request.urlopen()` 相同的功能。

#### xmlrpc 包

xmlrpc 包包含用于实现 XML-RPC 服务器和客户端的模块。XML-RPC 是一种远程过程调用机制，使用 XML 进行数据编码，使用 HTTP 作为传输机制。底层协议不特定于 Python，因此使用这些模块的程序可以潜在地与用其他语言编写的程序进行交互。有关 XML-RPC 的更多信息，请访问 http://www.xmlrpc.com。

##### xmlrpc.client (xmlrpclib)

xmlrpc.client 模块用于编写 XML-RPC 客户端。在 Python 2 中，此模块名为 xmlrpclib。要作为客户端运行，您需要创建 ServerProxy 的实例：

```
ServerProxy(uri [, transport [, encoding [, verbose [, allow_none [, use_datetime]]]])
```

uri 是远程 XML-RPC 服务器的位置——例如，"http://www.foo.com/RPC2"。如果需要，可以使用格式 "http://user:pass@host:port/path" 将基本身份验证信息添加到 URI，其中 user:pass 是用户名和密码。此信息经过 base-64 编码并放入传输的 'Authorization:' 头中。如果 Python 配置了 OpenSSL 支持，也可以使用 HTTPS。transport 指定用于创建内部传输对象的工厂函数，该对象用于底层通信。此参数仅在 XML-RPC 通过 HTTP 或 HTTPS 以外的某种连接使用时才使用。在正常使用中几乎不需要提供此参数（有关详细信息，请参阅在线文档）。encoding 指定编码，默认为 UTF-8。如果为 True，verbose 会显示一些调试信息。allow_none 如果为 True，则允许将值 None 发送到远程服务器。默认情况下，此选项被禁用，因为它并非普遍支持。use_datetime 是一个布尔标志，如果设置为 True，则使用 datetime 模块表示日期和时间。默认情况下为 False。

ServerProxy 的实例 `s` 透明地公开远程服务器上的所有方法。方法作为 `s` 的属性进行访问。例如，以下代码从提供该服务的远程服务器获取当前时间：

```
>>> s = ServerProxy("http://www.xmlrpc.com/RPC2")
>>> s.currentTime.getCurrentTime()
<DateTime u'20051102T20:08:24' at 2c77d8>
>>>
```

在大多数情况下，RPC 调用的工作方式与普通 Python 函数类似。然而，XML-RPC 协议仅支持有限数量的参数类型和返回值：

| XML-RPC 类型 | Python 等效类型 |
|-------------|-------------------|
| boolean | True 和 False |
| integer | int |
| float | float |
| string | string 或 unicode（必须只包含 XML 中有效的字符） |
| array | 包含有效 XML-RPC 类型的任何序列 |
| structure | 包含字符串键和有效类型值的字典 |
| dates | 日期和时间（xmlrpc.client.DateTime） |
| binary | 二进制数据（xmlrpc.client.Binary） |

当接收到日期时，它们会被存储在一个 `xmlrpc.client.DateTime` 实例 *d* 中。`d.value` 属性以 ISO 8601 时间/日期字符串的形式包含日期。要将其转换为与 `time` 模块兼容的时间元组，请使用 `d.timetuple()`。当接收到二进制数据时，它会被存储在一个 `xmlrpc.client.Binary` 实例 *b* 中。`b.data` 属性以字节字符串的形式包含数据。请注意，字符串被假定为 Unicode，因此您需要考虑使用正确的编码。如果包含 ASCII 字符，发送原始 Python 2 字节字符串可以工作，否则会中断。要解决这个问题，请先将其转换为 Unicode 字符串。

如果您使用涉及无效类型的参数进行 RPC 调用，可能会得到 `TypeError` 或 `xmlrpclib.Fault` 异常。

如果远程 XML-RPC 服务器支持自省，则以下方法可能可用：

```
s.system.listMethods()
```

返回一个字符串列表，列出 XML-RPC 服务器提供的所有方法。

```
s.methodSignatures(name)
```

给定一个方法的名称 *name*，返回该方法的可能调用签名列表。每个签名是以逗号分隔的字符串形式（例如 `'string, int, int'`）的类型列表，其中第一项是返回类型，其余项是参数类型。由于重载，可能会返回多个签名。在 Python 实现的 XML-RPC 服务器中，签名通常为空，因为函数和方法是动态类型的。

```
s.methodHelp(name)
```

给定一个方法的名称 *name*，返回一个描述该方法用法的文档字符串。文档字符串可以包含 HTML 标记。如果没有可用的文档，则返回一个空字符串。

以下实用函数在 `xmlrpclib` 模块中可用：

```
boolean(value)
```

从 *value* 创建一个 XML-RPC 布尔对象。此函数早于 Python 布尔类型的存在，因此您可能会在较旧的代码中看到它的使用。

```
binary(data)
```

创建一个包含二进制数据的 XML-RPC 对象。`data` 是一个包含原始数据的字符串。返回一个 `Binary` 实例。返回的 `Binary` 实例在传输过程中使用 base 64 透明地进行编码/解码。要从 `Binary` 实例 `b` 中提取二进制数据，请使用 `b.data`。

```
datetime(value)
```

创建一个包含日期的 XML-RPC 对象。`daytime` 可以是 ISO 8601 格式的日期字符串、`time.localtime()` 返回的时间元组或 struct，或者来自 `datetime` 模块的 `datetime` 实例。

```
dumps(params [, methodname [, methodresponse [, encoding [, allow_none]]]])
```

将 `params` 转换为 XML-RPC 请求或响应，其中 `params` 是参数元组或 `Fault` 异常的实例。`methodname` 是方法的名称（字符串）。`methodresponse` 是一个布尔标志。如果为 `True`，则结果是 XML-RPC 响应。在这种情况下，`params` 中只能提供一个值。`encoding` 指定生成的 XML 中的文本编码，默认为 UTF-8。`allow_none` 是一个标志，指定是否支持 `None` 作为参数类型。XML-RPC 规范没有明确提到 `None`，但许多服务器支持它。默认情况下，`allow_none` 为 `False`。

```
loads(data)
```

将包含 XML-RPC 请求或响应的 `data` 转换为元组 `(params, methodname)`，其中 `params` 是参数元组，`methodname` 是包含方法名称的字符串。如果请求表示的是故障条件而不是实际值，则会引发 `Fault` 异常。

```
MultiCall(server)
```

创建一个 `MultiCall` 对象，该对象允许将多个 XML-RPC 请求打包在一起并作为单个请求发送。如果需要向同一服务器发出许多不同的 RPC 请求，这可以作为一种有用的性能优化。`server` 是 `ServerProxy` 的实例，表示与远程服务器的连接。返回的 `MultiCall` 对象的使用方式与 `ServerProxy` 完全相同。然而，它不是立即执行远程方法，而是将方法调用排队，直到 `MultiCall` 对象作为函数被调用。一旦发生这种情况，RPC 请求就会被传输。此操作的返回值是一个生成器，它依次产生每个 RPC 操作的返回结果。请注意，`MultiCall()` 仅在远程服务器提供 `system.multicall()` 方法时才有效。

这是一个说明 `MultiCall` 用法的示例：

```
multi = MultiCall(server)
multi.foo(4,6,7)              # 远程方法 foo
multi.bar("hello world")      # 远程方法 bar
multi.spam()                  # 远程方法 spam
# 现在，实际发送 XML-RPC 请求并获取返回结果
foo_result, bar_result, spam_result = multi()
```

##### 异常

`xmlrpc.client` 中定义了以下异常：

**Fault**

表示一个 XML-RPC 故障。`faultCode` 属性包含一个表示故障类型的字符串。`faultString` 属性包含与故障相关的描述性消息。

**ProtocolError**

表示底层网络存在问题——例如，错误的 URL 或某种连接问题。`url` 属性包含触发错误的 URI。`errcode` 属性包含一个错误代码。`errmsg` 属性包含一个描述性字符串。`headers` 属性包含触发错误的请求的所有 HTTP 头。

##### xmlrpc.server (SimpleXMLRPCServer, DocXMLRPCServer)

`xmlrpc.server` 模块包含用于实现不同变体 XML-RPC 服务器的类。在 Python 2 中，此功能位于两个单独的模块中：`SimpleXMLRPCServer` 和 `DocXMLRPCServer`。

**SimpleXMLRPCServer(addr [, requestHandler [, logRequests]])**

创建一个监听套接字地址 *addr*（例如 `('localhost',8080)`）的 XML-RPC 服务器。*requestHandler* 是一个工厂函数，在收到连接时创建处理程序请求对象。默认情况下，它设置为 `SimpleXMLRPCRequestHandler`，这是目前唯一可用的处理程序。*logRequests* 是一个布尔标志，指示是否记录传入的请求。默认值为 `True`。

**DocXMLRPCServer(addr [, requestHandler [, logRequest]])**

创建一个文档化的 XML-RPC 服务器，它还会响应 HTTP `GET` 请求（通常由浏览器发送）。如果收到，服务器会从所有注册方法和对象中找到的文档字符串生成文档。参数与 `SimpleXMLRPCServer` 的含义相同。

`SimpleXMLRPCServer` 或 `DocXMLRPCServer` 的实例 *s* 具有以下方法：

**s.register_function(func [, name])**

向 XML-RPC 服务器注册一个新函数 *func*。*name* 是可选的，用于指定该函数的名称。如果提供了 *name*，客户端将使用此名称访问该函数。此名称可以包含不是有效 Python 标识符一部分的字符，包括句点 (.)。如果未提供 *name*，则使用 *func* 的实际函数名称。

**s.register_instance(instance [, allow_dotted_names])**

注册一个用于解析未通过 `register_function()` 方法注册的方法名称的对象。如果实例 *instance* 定义了 `_dispatch(self, methodname, params)` 方法，则调用它来处理请求。*methodname* 是方法的名称，*params* 是包含参数的元组。`_dispatch()` 的返回值将返回给客户端。如果未定义 `_dispatch()` 方法，则会在实例中搜索与方法名称匹配的属性名称。如果 *allow_dotted_names* 为 `True`，则允许包含点的方法名称。此方法允许创建分层的 XML-RPC 方法集合。

**s.register_introspection_functions()**

注册 XML-RPC 自省方法：`system.listMethods()`、`system.methodSignature()` 和 `system.methodHelp()`。



检查方法名称是否匹配为*实例*定义的任何方法名称。如果匹配，则直接调用该方法。`allow_dotted_names`参数是一个标志，用于指示在检查方法名称时是否应执行分层搜索。例如，如果收到对方法'foo.bar.spam'的请求，此参数决定是否搜索`instance.foo.bar.spam`。默认情况下，此值为*False*。除非客户端已经过验证，否则不应将其设置为*True*。否则，它将打开一个安全漏洞，允许入侵者执行任意Python代码。请注意，一次最多只能注册一个实例。

```python
s.register_introspection_functions()
```

向XML-RPC服务器添加XML-RPC内省函数`system.listMethods()`、`system.methodHelp()`和`system.methodSignature()`。`system.methodHelp()`返回方法的文档字符串（如果有）。`system.methodSignature()`函数只是返回一条指示该操作不被支持的消息（因为Python是动态类型的，类型信息不可用）。

```python
s.register_multicall_functions()
```

通过向服务器添加`system.multicall()`函数来支持XML-RPC多重调用功能。

`DocXMLRPCServer`的实例还提供了以下方法：

```python
s.set_server_title(server_title)
```

在HTML文档中设置服务器的标题。该字符串被放置在HTML的`<title>`标签中。

```python
s.set_server_name(server_name)
```

在HTML文档中设置服务器的名称。该字符串以`<h1>`标签的形式出现在页面顶部。

```python
s.set_server_documentation(server_documentation)
```

向生成的HTML输出添加一个描述段落。该字符串被添加在服务器名称之后，但在XML-RPC函数描述之前。

尽管XML-RPC服务器通常作为独立进程运行，但它也可以在CGI脚本内部运行。以下类用于此目的：

```python
CGIXMLRPCRequestHandler([allow_none [, encoding]])
```

一个CGI请求处理器，其操作方式与`SimpleXMLRPCServer`相同。其参数与为`SimpleXMLRPCServer`描述的参数含义相同。

```python
DocCGIXMLRPCRequestHandler()
```

一个CGI请求处理器，其操作方式与`DocXMLRPCServer`相同。请注意，截至本文撰写时，其调用参数与`CGIXMLRPCRequestHandler()`不同。这可能是Python的一个错误，因此您应该在未来的发行版中查阅在线文档。

任一CGI处理器的实例*c*具有与普通XML-RPC服务器相同的注册函数和实例的方法。然而，它们还定义了以下方法：

```python
c.handle_request([request_text])
```

处理一个XML-RPC请求。默认情况下，请求从标准输入读取。如果提供了request_text，则它包含以HTTP POST请求接收形式的请求数据。

##### 示例

这是一个非常简单的编写独立服务器的示例。它添加了一个函数add。此外，它还将math模块的整个内容作为一个实例添加，暴露其包含的所有函数。

```python
try:
    from xmlrpc.server import SimpleXMLRPCServer      # Python 3
except ImportError:
    from SimpleXMLRPCServer import SimpleXMLRPCServer # Python 2
import math

def add(x,y):
    "Adds two numbers"
    return x+y

s = SimpleXMLRPCServer(('',8080))
s.register_function(add)
s.register_instance(math)
s.register_introspection_functions()
s.serve_forever()
```

以下是作为CGI脚本实现的相同功能：

```python
try:
    from xmlrpc.server import CGIXMLRPCRequestHandler     # Python 3
except ImportError:
    from SimpleXMLRPCServer import CGIXMLRPCRequestHandler # Python 2
import math

def add(x,y):
    "Adds two numbers"
    return x+y

s = CGIXMLRPCRequestHandler()
s.register_function(add)
s.register_instance(math)
s.register_introspection_functions()
s.handle_request()
```

要从其他Python程序访问XML-RPC函数，请使用xmlrpc.client或xmlrpclib模块。下面是一个简短的交互式会话，展示其工作原理：

```python
>>> from xmlrpc.client import ServerProxy
>>> s = ServerProxy("http://localhost:8080")
>>> s.add(3,5)
8
>>> s.system.listMethods()
['acos', 'add', 'asin', 'atan', 'atan2', 'ceil', 'cos', 'cosh', 'degrees', 'exp',
 'fabs', 'floor', 'fmod', 'frexp', 'hypot', 'ldexp', 'log', 'log10', 'modf',
 'pow', 'radians', 'sin', 'sinh', 'sqrt', 'system.listMethods',
 'system.methodHelp', 'system.methodSignature', 'tan', 'tanh']
>>> s.tan(4.5)
4.6373320545511847
>>>
```

##### 高级服务器定制

XML-RPC服务器模块易于用于基本类型的分布式计算。例如，XML-RPC可以用作对网络上其他系统进行高级控制的协议，前提是它们都运行合适的XML-RPC服务器。如果额外使用`pickle`模块，也可以在系统之间传递更有趣的对象。

XML-RPC的一个担忧是安全性。默认情况下，XML-RPC服务器作为网络上的开放服务运行，因此任何知道服务器地址和端口的人都可以连接到它（除非它被防火墙保护）。此外，XML-RPC服务器不限制请求中可以发送的数据量。攻击者可能通过发送一个载荷如此之大的HTTP `POST`请求来耗尽内存，从而使服务器崩溃。

如果您想解决这些问题中的任何一个，您将需要自定义XML-RPC服务器类或请求处理器。所有服务器类都继承自`socketserver`模块中的`TCPServer`。因此，服务器可以像其他套接字服务器类一样进行自定义（例如，添加线程、分叉或验证客户端地址）。可以通过继承`SimpleXMLRPCRequestHandler`或`DocXMLRPCRequestHandler`并扩展`do_POST()`方法，在请求处理器周围放置一个验证包装器。以下是一个限制传入请求大小的示例：

```python
try:
    from xmlrpc.server import (SimpleXMLRPCServer,
                                SimpleXMLRPCRequestHandler)
except ImportError:
    from SimpleXMLRPCServer import (SimpleXMLRPCServer,
                                    SimpleXMLRPCRequestHandler)
class MaxSizeXMLRPCHandler(SimpleXMLRPCRequestHandler):
    MAXSIZE = 1024*1024   # 1MB
    def do_POST(self):
        size = int(self.headers.get('content-length',0))
        if size >= self.MAXSIZE:
            self.send_error(400,"Bad request")
        else:
            SimpleXMLRPCRequestHandler.do_POST(self)

s = SimpleXMLRPCServer(('',8080),MaxSizeXMLRPCHandler)
```

如果您想添加任何基于HTTP的身份验证，也可以以类似的方式实现。

### 23 Web编程

Python在构建网站时被广泛使用，并承担着几种不同的角色。首先，Python脚本通常是生成一组静态HTML页面以由Web服务器交付的有用方式。例如，脚本可用于获取原始内容并用网站上通常看到的附加功能进行装饰（导航栏、侧边栏、广告、样式表等）。这主要只是文件处理和文本处理的问题——本书的其他部分已经涵盖了这些主题。

其次，Python脚本用于生成动态内容。例如，一个网站可能使用标准的Web服务器（如Apache）运行，但会使用Python脚本动态处理某些类型的请求。Python的这种使用主要与表单处理相关。例如，一个HTML页面可能包含如下表单：

```html
<FORM ACTION='/cgi-bin/subscribe.py' METHOD='GET'>
Your name : <INPUT type='Text' name='name' size='30'>
Your email address: <INPUT type='Text' name='email' size='30'>
<INPUT type='Submit' name='submit-button' value='Subscribe'>
</FORM>
```

在表单中，ACTION属性命名了一个Python脚本'subscribe.py'，当表单提交时，该脚本将在服务器上执行。

涉及动态内容生成的另一个常见场景是AJAX（异步JavaScript和XML）。使用AJAX，JavaScript事件处理程序与页面上的某些HTML元素相关联。例如，当鼠标悬停在特定文档元素上时，JavaScript函数可能会执行并向Web服务器发送一个HTTP请求，该请求会被处理（可能由Python脚本处理）。当收到关联的响应时，另一个JavaScript函数执行以处理响应数据并显示结果。结果可以通过多种方式返回。例如，服务器可能以纯文本、XML、JSON或任何其他格式返回数据。下面是一个示例HTML文档，说明了实现悬停弹出窗口的一种方式，将鼠标移到选定元素上会导致弹出窗口出现。

```html
<html>
  <head>
    <title>ACME Officials Quiet After Corruption Probe</title>
    <style type="text/css">
      .popup { border-bottom:1px dashed green; }
      .popup:hover { background-color: #c0c0ff; }
    </style>
  </head>
  <body>
```

本章其余部分将介绍与Python同Web服务器和框架交互的底层接口相关的内置模块。主题包括CGI脚本——一种从第三方Web服务器访问Python的技术，以及WSGI——一个用于编写可与Python各种Web框架集成的组件的中间件层。

#### cgi

`cgi`模块用于实现CGI脚本，这类程序通常在Web服务器需要处理用户表单输入或生成某种动态内容时执行。

当提交与CGI脚本对应的请求时，Web服务器会将CGI程序作为子进程执行。CGI程序从两个来源接收输入：`sys.stdin`和服务器设置的环境变量。以下列表详细说明了Web服务器通常设置的常见环境变量：

| 变量 | 描述 |
|----------|-------------|
| AUTH_TYPE | 认证方法 |
| CONTENT_LENGTH | 通过`sys.stdin`传递的数据长度 |
| CONTENT_TYPE | 查询数据类型 |
| DOCUMENT_ROOT | 文档根目录 |
| GATEWAY_INTERFACE | CGI修订版本字符串 |
| HTTP_ACCEPT | 客户端接受的MIME类型 |
| HTTP_COOKIE | Netscape持久化Cookie值 |
| HTTP_FROM | 客户端的电子邮件地址（通常被禁用） |
| HTTP_REFERER | 来源URL |
| HTTP_USER_AGENT | 客户端浏览器 |
| PATH_INFO | 传递的额外路径信息 |
| PATH_TRANSLATED | PATH_INFO的翻译版本 |
| QUERY_STRING | 查询字符串 |
| REMOTE_ADDR | 客户端的远程IP地址 |
| REMOTE_HOST | 客户端的远程主机名 |
| REMOTE_IDENT | 发起请求的用户 |
| REMOTE_USER | 已认证的用户名 |
| REQUEST_METHOD | 请求方法（`'GET'`或`'POST'`） |
| SCRIPT_NAME | 程序名称 |
| SERVER_NAME | 服务器主机名 |
| SERVER_PORT | 服务器端口号 |
| SERVER_PROTOCOL | 服务器协议 |
| SERVER_SOFTWARE | 服务器软件名称和版本 |

作为输出，CGI程序会写入标准输出`sys.stdout`。CGI编程的详细细节可以在诸如Shishir Gundavaram所著的《CGI Programming with Perl》第二版（O'Reilly & Associates，2000）之类的书籍中找到。对于我们的目的，实际上只需要知道两点。首先，HTML表单的内容通过称为*查询字符串*的文本序列传递给CGI程序。在Python中，可以使用`FieldStorage`类访问查询字符串的内容。例如：

```
import cgi
form = cgi.FieldStorage()
name = form.getvalue('name')    # Get 'name' field from a form
email = form.getvalue('email')  # Get 'email' field from a form
```

其次，CGI程序的输出由两部分组成：HTTP头和原始数据（通常是HTML）。一个空行始终分隔这两个部分。一个简单的HTTP头如下所示：

```
print 'Content-type: text/html\r'   # HTML Output
print '\r'                            # Blank line (required!)
```

其余输出是原始输出。例如：

```
print '<TITLE>My CGI Script</TITLE>'
print '<H1>Hello World!</H1>'
print 'You are %s (%s)' % (name, email)
```

标准的做法是HTTP头使用Windows换行符`'\r\n'`终止。这就是示例中出现`'\r'`的原因。如果需要发出错误信号，请在输出中包含特殊的`'Status:'`头。例如：

```
print 'Status: 401 Forbidden\r'   # HTTP Error code
print 'Content-type: text/plain\r'
print '\r'                        # Blank line (required)
print 'You're not worthy of accessing this page!'
```

如果需要将客户端重定向到其他页面，请创建如下输出：

```
print 'Status: 302 Moved\r'
print 'Location: http://www.foo.com/orderconfirm.html\r'
print '\r'
```

`cgi`模块的大部分工作是通过创建`FieldStorage`类的实例来完成的。

```
FieldStorage([input [, headers [, outerboundary [, environ [, keep_blank_values [, strict_parsing]]]]]])
```

通过读取和解析在环境变量或标准输入中传递的查询字符串来读取表单内容。`input`指定一个类似文件的对象，在POST请求中将从中读取表单数据。默认情况下，使用`sys.stdin`。`headers`和`outerboundary`在内部使用，不应提供。`environ`是一个字典，CGI环境变量从中读取。`keep_blank_values`是一个布尔标志，控制是否保留空值。默认情况下，它为`False`。`strict_parsing`是一个布尔标志，如果出现任何解析问题，会引发异常。默认情况下，它为`False`。

`FieldStorage`实例`form`的工作方式类似于字典。例如，`f = form[key]`将提取给定参数`key`的条目。以这种方式提取的实例`f`要么是另一个`FieldStorage`实例，要么是`MiniFieldStorage`实例。以下属性定义在`f`上：

| 属性 | 描述 |
| --- | --- |
| f.name | 字段名称（如果指定） |
| f.filename | 上传时使用的客户端文件名 |
| f.value | 字符串形式的值 |
| f.file | 可以读取数据的类文件对象 |
| f.type | 内容类型 |
| f.type_options | HTTP请求中content-type行指定的选项字典 |
| f.disposition | 'content-disposition'字段；如果未指定则为None |
| f.disposition_options | disposition选项的字典 |
| f.headers | 包含所有HTTP头内容的类字典对象 |

可以使用以下方法从表单中提取值：

```
form.getvalue(fieldname [, default])
```

返回名为`fieldname`的给定字段的值。如果一个字段定义了两次，此函数将返回所有定义值的列表。如果提供了`default`，则指定字段不存在时要返回的值。使用此方法的一个注意事项是，如果同一个表单字段名称在请求中出现了两次，返回的值将是一个包含两个值的列表。为简化编程，您可以使用`form.getfirst()`，它只返回找到的第一个值。

```
form.getfirst(fieldname [, default])
```

返回为名为`fieldname`的字段定义的第一个值。如果提供了`default`，则指定字段不存在时要返回的值。

```
form.getlist(fieldname)
```

返回为`fieldname`定义的所有值的列表。即使只定义了一个值，它也总是返回列表，如果没有值存在，则返回空列表。

此外，`cgi`模块定义了一个类`MiniFieldStorage`，它只包含属性的名称和值。此类用于表示在查询字符串中传递的表单的单个字段，而`FieldStorage`用于包含多个字段和多部分数据。



##### CGI 编程建议

在当今 Web 框架盛行的时代，CGI 脚本似乎已不再流行。然而，如果你打算使用它，这里有一些编程技巧可以简化你的工作。

首先，不要编写使用大量 `print` 语句来生成硬编码 HTML 输出的 CGI 脚本。这样产生的程序将是 Python 和 HTML 混杂的、难以阅读且无法维护的可怕混乱。更好的方法是依赖模板。至少，可以使用 `string.Template` 对象来实现这一点。下面是一个说明该概念的例子：

```python
import cgi
from string import Template

def error(message):
    temp = Template(open("errormsg.html").read())
    print 'Content-type: text/html\r'
    print '\r'
    print temp.substitute({'message' : message})

form = cgi.FieldStorage()
name  = form.getfirst('name')
email = form.getfirst('email')
if not name:
    error("name not specified")
    raise SystemExit
elif not email:
    error("email not specified")
    raise SystemExit

# Do various processing
confirmation = subscribe(name, email)

# Print the output page
values = {
    'name' : name,
    'email' : email,
    'confirmation': confirmation,
    # Add other values here...
}
temp = Template(open("success.html").read())
print temp.substitute(values)
```

在这个例子中，文件 `'error.html'` 和 `'success.html'` 是包含了所有输出但带有 `$variable` 占位符的 HTML 页面，这些占位符对应于 CGI 脚本中动态生成的值。例如，`'success.html'` 文件可能看起来像这样：

```html
<HTML>
  <HEAD>
    <TITLE>Success</TITLE>
  </HEAD>
  <BODY>
  Welcome $name. You have successfully subscribed to our
  newsletter. Your confirmation code is $confirmation.
  </BODY>
</HTML>
```

脚本中的 `temp.substitute()` 操作只是将这个文件中的变量填充进去。这种方法的一个明显好处是，如果你想改变输出的外观，只需修改模板文件，而不是 CGI 脚本。Python 有许多第三方模板引擎可用——其数量甚至可能比 Web 框架还多。它们采用了模板化的概念并在此基础上进行了实质性的扩展。详见 http://wiki.python.org/moin/Templating 获取更多细节。

其次，如果你需要从 CGI 脚本中保存数据，请尝试使用数据库。虽然直接将数据写入文件很简单，但 Web 服务器是并发运行的，除非你采取了适当的锁定和同步资源的步骤，否则文件可能会损坏。数据库服务器及其相关的 Python 接口通常没有这个问题。因此，如果你需要保存数据，请尝试使用 `sqlite3` 模块或用于 MySQL 等数据库的第三方模块。

最后，如果你发现自己正在编写数十个 CGI 脚本以及需要处理 HTTP 底层细节（如 cookie、身份验证、编码等）的代码，你可能需要考虑使用 Web 框架。使用框架的全部意义就在于你不必再担心这些细节——嗯，至少不用那么担心。所以，不要重新发明轮子。

##### 注意事项

-   安装 CGI 程序的过程因所使用的 Web 服务器类型而有很大差异。通常程序被放置在一个特殊的 `cgi-bin` 目录中。服务器可能还需要额外的配置。你应该查阅服务器的文档或服务器管理员以获取更多细节。
-   在 UNIX 上，Python CGI 程序可能需要设置适当的执行权限，并且程序的第一行需要包含如下一行：
    ```python
    #!/usr/bin/env python
    import cgi
    ...
    ```
-   为了简化调试，请导入 `cgitb` 模块——例如，`import cgitb; cgitb.enable()`。这会修改异常处理，以便在 Web 浏览器中显示错误信息。
-   如果你调用外部程序——例如，通过 `os.system()` 或 `os.popen()` 函数——请小心不要将从客户端收到的任意字符串传递给 shell。这是一个众所周知的安全漏洞，黑客可以利用它在服务器上执行任意 shell 命令（因为传递给这些函数的命令首先由 UNIX shell 解释，而不是直接执行）。特别地，在确保字符串仅包含字母数字字符、破折号、下划线和句点之前，永远不要将 URL 或表单数据的任何部分传递给 shell 命令。
-   在 UNIX 上，不要给 CGI 程序 `setuid` 模式。这是一个安全风险，并非所有机器都支持。
-   不要使用 `'from cgi import *'` 导入此模块。`cgi` 模块定义了各种各样的名称和符号，你可能不希望它们出现在你的命名空间中。

#### cgitb

此模块提供了一个替代的异常处理器，当未捕获的异常发生时，它会显示一份详细的报告。报告包含源代码、参数值和局部变量。最初，此模块是为帮助调试 CGI 脚本而开发的，但它可以用于任何应用程序。

```python
enable([display [, logdir [, context [, format]]]])
```

启用特殊的异常处理。`display` 是一个标志，用于确定在错误发生时是否显示信息。默认值是 `1`。`logdir` 指定一个目录，错误报告将被写入文件而不是打印到标准输出。当给定 `logdir` 时，每个错误报告都被写入由 `tempfile.mkstemp()` 函数创建的唯一文件。`context` 是一个整数，指定在异常发生行周围要显示的源代码行数。

`format` 是一个字符串，指定输出格式。格式为 `'html'` 时指定 HTML（默认）。任何其他值都会产生纯文本格式。

```python
handle([info])
```

使用 `enable()` 函数的默认设置处理异常。`info` 是一个元组 `(exctype, excvalue, tb)`，其中 `exctype` 是异常类型，`excvalue` 是异常值，`tb` 是回溯对象。此元组通常使用 `sys.exc_info()` 获取。如果省略 `info`，则使用当前异常。



#### wsgiref

WSGI（Python Web 服务器网关接口）是 Web 服务器与 Web 应用程序之间的标准化接口，旨在提高应用程序在不同 Web 服务器和框架之间的可移植性。该标准的官方描述见 PEP 333 (http://www.python.org/dev/peps/pep-0333)。关于该标准及其使用的更多信息也可在 http://www.wsgi.org 找到。wsgiref 包是一个参考实现，可用于测试、验证和简单部署。

> 注意
>
> 要在 CGI 脚本中启用特殊的异常处理，请在脚本开头包含 `import cgitb; enable()` 这一行。

##### WSGI 规范

使用 WSGI 时，Web 应用程序被实现为一个函数或可调用对象 `webapp(environ, start_response)`，它接受两个参数。`environ` 是一个环境设置字典，最少需要包含以下值，这些值与 CGI 脚本中使用的名称和含义相同：

| environ 变量 | 描述 |
|---|---|
| CONTENT_LENGTH | 传递的数据长度 |
| CONTENT_TYPE | 查询数据的类型 |
| HTTP_ACCEPT | 客户端接受的 MIME 类型 |
| HTTP_COOKIE | Netscape 持久化 cookie 值 |
| HTTP_REFERER | 来源 URL |
| HTTP_USER_AGENT | 客户端浏览器 |
| PATH_INFO | 传递的额外路径信息 |
| QUERY_STRING | 查询字符串 |
| REQUEST_METHOD | 方法（'GET' 或 'POST'） |
| SCRIPT_NAME | 程序名称 |
| SERVER_NAME | 服务器主机名 |
| SERVER_PORT | 服务器端口号 |
| SERVER_PROTOCOL | 服务器协议 |

此外，`environ` 字典还需要包含以下 WSGI 特有的值：

| environ 变量 | 描述 |
|---|---|
| wsgi.version | 表示 WSGI 版本的元组（例如，(1,0) 表示 WSGI 1.0）。 |
| wsgi.url_scheme | 表示 URL scheme 部分的字符串。例如，'http' 或 'https'。 |
| wsgi.input | 一个文件类对象，表示输入流。表单数据或上传等额外数据从这里读取。 |
| wsgi.errors | 一个以文本模式打开的文件类对象，用于写入错误输出。 |
| wsgi.multithread | 一个布尔标志，如果应用程序可以在同一进程中被另一个线程并发执行，则为 True。 |
| wsgi.multiprocess | 一个布尔标志，如果应用程序可以被另一个进程并发执行，则为 True。 |
| wsgi.run_once | 一个布尔标志，如果应用程序在执行进程的生命周期内只会被执行一次，则为 True。 |

start_response 参数是一个形如 start_response(status, headers) 的可调用对象，应用程序使用它来开始响应。status 是一个字符串，如 '200 OK' 或 '404 Not Found'。headers 是一个元组列表，每个元组形如 (name, value)，对应于要包含在响应中的 HTTP 头——例如，('Content-type','text/html')。

响应的数据或主体由 Web 应用程序函数作为可迭代对象返回，该对象产生一系列字节字符串或仅包含可编码为单个字节的字符的文本字符串（例如，兼容 ISO-8859-1 或 Latin-1 字符集）的序列。示例包括字节字符串列表或产生字节字符串的生成器函数。如果应用程序需要进行任何字符编码（如 UTF-8），则必须自行完成。

以下是一个简单的 WSGI 应用程序示例，它读取表单字段并产生一些输出，类似于在 cgi 模块部分所示的内容：

```
import cgi
def subscribe_app(environ, start_response):
    fields = cgi.FieldStorage(environ['wsgi.input'],
            environ=environ)

    name = fields.getvalue("name")
    email = fields.getvalue("email")

    # Various processing

    status = "200 OK"
    headers = [('Content-type','text/plain')]
    start_response(status, headers)

    response = [
        'Hi %s. Thank you for subscribing.' % name,
        'You should expect a response soon.'
        ]
    return (line.encode('utf-8') for line in response)
```

这个示例中有几个关键细节。首先，WSGI 应用程序组件不绑定到特定的框架、Web 服务器或库模块集合。在示例中，我们只使用了一个库模块 cgi，仅仅因为它有一些用于解析查询变量的便利函数。示例展示了如何使用 `start_response()` 函数来启动响应并提供头部。响应本身被构造为字符串列表。此应用程序中的最后一条语句是一个生成器表达式，它将所有字符串转换为字节字符串。如果你使用的是 Python 3，这是一个关键步骤——所有 WSGI 应用程序都应返回编码后的字节，而不是未编码的 Unicode 数据。

要部署 WSGI 应用程序，必须将其注册到你正在使用的 Web 编程框架中。为此，你需要阅读该框架的手册。

##### wsgiref 包

wsgiref 包提供了 WSGI 标准的参考实现，允许应用程序在独立服务器中进行测试或作为普通 CGI 脚本执行。

###### wsgiref.simple_server

wsgiref.simple_server 模块实现了一个简单的独立 HTTP 服务器，用于运行单个 WSGI 应用程序。只有两个值得关注的函数：

**make_server(host, port, app)**

创建一个 HTTP 服务器，它在给定的主机名 host 和端口号 port 上接受连接。app 是实现 WSGI 应用程序的函数或可调用对象。要运行服务器，使用 s.serve_forever()，其中 s 是返回的服务器实例。

**demo_app(environ, start_response)**

一个完整的 WSGI 应用程序，返回一个包含 "Hello World" 消息的页面。这可以用作 make_server() 的 app 参数，以验证服务器是否正常工作。

以下是一个运行简单 WSGI 服务器的示例：

```
def my_app(environ, start_response):
    # Some application
    start_response("200 OK", [('Content-type', 'text/plain')])
    return ['Hello World']

if __name__ == '__main__':
    from wsgiref.simple_server import make_server
    serv = make_server('', 8080, my_app)
    serv.serve_forever()
```

###### wsgiref.handlers

wsgiref.handlers 模块包含用于设置 WSGI 执行环境的处理器对象，以便应用程序可以在另一个 Web 服务器内运行（例如，在 Apache 下的 CGI 脚本）。有几种不同的对象。

**CGIHandler()**

创建一个在标准 CGI 环境中运行的 WSGI 处理器对象。该处理器从标准环境变量和 I/O 流中收集信息，如 cgi 库模块中所述。

**BaseCGIHandler(stdin, stdout, stderr, environ [, multithread [, multiprocess]])**

创建一个在 CGI 环境中运行的 WSGI 处理器，但标准 I/O 流和环境变量可能以不同的方式设置。stdin、stdout 和 stderr 指定标准 I/O 流的文件类对象。environ 是一个环境变量字典，预期已包含标准 CGI 环境变量。multithread 和 multiprocess 是布尔标志，用于设置 wsgi.multithread 和 wsgi.multiprocess 环境变量。默认情况下，multithread 为 True，multiprocess 为 False。

**SimpleHandler(stdin, stdout, stderr, environ [, multithread [, multiprocess]])**

创建一个类似于 `BaseCGIHandler` 的 WSGI 处理器，但它允许底层应用程序直接访问 `stdin`、`stdout`、`stderr` 和 `environ`。这与 `BaseCGIHandler` 略有不同，后者提供了额外的逻辑来正确处理某些功能（例如，在 `BaseCGIHandler` 中，响应码被转换为 `Status:` 头部）。

所有这些处理器都有一个 `run(app)` 方法，用于在处理器内运行 WSGI 应用程序。以下是一个作为传统 CGI 脚本运行的 WSGI 应用程序示例：

```
#!/usr/bin/env python
def my_app(environ, start_response):
    # Some application
    start_response("200 OK",[('Content-type','text/plain')])
    return ['Hello World']

from wsgiref.handlers import CGIHandler
hand = CGIHandler()
hand.run(my_app)
```

###### wsgiref.validate

`wsgiref.validate` 模块有一个函数，它用验证包装器包装 WSGI 应用程序，以确保应用程序和服务器都按照标准运行。

**validator(app)**

创建一个新的 WSGI 应用程序，包装 WSGI 应用程序 `app`。新应用程序以与 `app` 相同的方式透明工作，只是添加了广泛的错误检查，以确保应用程序和服务器遵循 WSGI 标准。任何违规都会导致 `AssertionError` 异常。

以下是使用验证器的示例：

```
def my_app(environ, start_response):
    # Some application
    start_response("200 OK",[('Content-type','text/plain')])
    return ['Hello World']

if __name__ == '__main__':
    from wsgiref.simple_server import make_server
    from wsgiref.validate import validator
    serv = make_server('',8080, validator(my_app))
    serv.serve_forever()
```

###### 注意

本节中的内容主要面向希望创建应用程序对象的 WSGI 用户。另一方面，如果你正在为 Python 实现另一个 Web 框架，你应该查阅 PEP 333 以获取关于使你的框架支持 WSGI 所需的确切内容的官方详细信息。如果你使用的是第三方 Web 框架，你需要查阅该框架的文档以了解其对 WSGI 对象支持的详细信息。鉴于 WSGI 是一个官方认可的规范，并且在标准库中有参考实现，框架提供对其某种程度的支持越来越常见。



#### webbrowser

`webbrowser` 模块提供了一些实用函数，用于在不同平台上以独立于操作系统的方式在网页浏览器中打开文档。该模块主要用于开发和测试场景。例如，如果你编写了一个生成 HTML 输出的脚本，可以使用此模块中的函数自动调用系统浏览器查看结果。

```
open(url [, new [, autoraise]])
```

使用系统默认浏览器显示 *url*。如果 *new* 为 0，则尽可能在当前浏览器的同一窗口中打开 URL；如果 *new* 为 1，则创建一个新的浏览器窗口；如果 *new* 为 2，则在浏览器的新标签页中打开 URL。如果 *autoraise* 为 True，则会激活（置前）浏览器窗口。

```
open_new(url)
```

在默认浏览器的新窗口中显示 *url*。等同于 `open(url, 1)`。

```
open_new_tab(url)
```

在默认浏览器的新标签页中显示 *url*。等同于 `open(url, 2)`。

```
get([name])
```

返回一个用于操控浏览器的控制器对象。*name* 是浏览器类型的名称，通常是一个字符串，例如 `'netscape'`、`'mozilla'`、`'kfm'`、`'grail'`、`'windows-default'`、`'internet-config'` 或 `'command-line'`。返回的控制器对象具有 `open()` 和 `open_new()` 方法，它们接受与前述两个函数相同的参数并执行相同的操作。如果省略 *name*，则返回默认浏览器的控制器对象。

```
register(name, constructor[, controller])
```

注册一个新的浏览器类型以供 `get()` 函数使用。*name* 是浏览器的名称。*constructor* 是在不带参数的情况下被调用，以创建用于在该浏览器中打开页面的控制器对象。*controller* 是一个要使用的控制器实例。如果提供了 *controller*，则忽略 *constructor*，并且 *constructor* 可以是 None。

由 `get()` 函数返回的控制器实例 *c* 具有以下方法：

```
c.open(url[, new])
```

与 `open()` 函数相同。

```
c.open_new(url)
```

与 `open_new()` 函数相同。

## 互联网数据处理与编码

本章描述与处理常见互联网数据格式和编码相关的模块，如 base 64、HTML、XML 和 JSON。

#### base64

**base64** 模块用于使用 base 64、base 32 或 base 16 编码对二进制数据进行编码和解码。Base 64 通常用于在电子邮件附件和 HTTP 协议的部分内容中嵌入二进制数据。官方细节可参见 RFC-3548 和 RFC-1421。

Base 64 编码的工作原理是将待编码的数据分组为每组 24 位（3 字节）。每个 24 位组再细分为四个 6 位分量。每个 6 位值由以下字母表中对应的可打印 ASCII 字符表示：

| 值 | 编码 |
|-------|----------|
| 0–25 | ABCDEFGHIJKLMNOPQRSTUVWXYZ |
| 26–51 | abcdefghijklmnopqrstuvwxyz |
| 52–61 | 0123456789 |
| 62 | + |
| 63 | / |
| 填充 | = |

如果输入流中的字节数不是 3（24 位）的倍数，则对数据进行填充以形成完整的 24 位组。额外的填充通过出现在编码末尾的特殊 '=' 字符来指示。例如，如果你编码一个 16 字节的字符序列，会有五个 3 字节组，并剩余 1 字节。剩余的字节被填充以形成一个 3 字节组。这个组然后从 base 64 字母表中产生两个字符（前 12 位，包含 8 位真实数据），后跟序列 '=='，代表额外填充的位。有效的 base 64 编码在末尾只会有零个、一个（=）或两个（==）填充字符。

Base 32 编码的工作原理是将二进制数据分组为每组 40 位（5 字节）。每个 40 位组细分为八个 5 位分量。每个 5 位值使用以下字母表进行编码：

| 值 | 编码 |
|-------|----------|
| 0–25 | ABCDEFGHIJKLMNOPQRSTUVWXYZ |
| 26–31 | 2–7 |

与 base 64 类似，如果输入流的末尾不能形成 40 位组，则将其填充至 40 位，并使用 '=' 字符表示输出中的额外填充。最多将有六个填充字符（'======'），这发生在最后一组仅包含 1 字节数据时。

Base 16 编码是数据的标准十六进制编码。每个 4 位组由数字 '0'–'9' 和字母 'A'–'F' 表示。Base 16 编码没有额外的填充或填充字符。

```
b64encode(s [, altchars])
```

使用 base 64 编码对字节字符串 *s* 进行编码。如果给定 *altchars*，它是一个双字符字符串，用于指定替代正常出现在 base 64 输出中的 '+' 和 '/' 字符的字符。如果 base 64 编码用于文件名或 URL，这很有用。

```
b64decode(s [, altchars])
```

解码以 base 64 编码的字符串 *s*，并返回包含解码数据的字节字符串。如果给定 *altchars*，它是一个双字符字符串，用于指定替代正常出现在 base 64 编码数据中的 '+' 和 '/' 的字符。如果输入 *s* 包含多余字符或填充不正确，将引发 **TypeError**。

```
standard_b64encode(s)
```

使用标准 base 64 编码对字节字符串 *s* 进行编码。

```
standard_b64decode(s)
```

使用标准 base 64 编码解码字符串 *s*。

```
urlsafe_b64encode(s)
```

使用 base 64 对字节字符串 *s* 进行编码，但分别使用字符 '-' 和 '_' 代替 '+' 和 '/'。等同于 `b64encode(s, '-_')`。

```
urlsafe_b64decode(s)
```

解码使用 URL 安全 base 64 编码的字符串 *s*。

```
b32encode(s)
```

使用 base 32 编码对字节字符串 *s* 进行编码。

```
b32decode(s [, casefold [, map01]])
```

使用 base 32 编码解码字符串 *s*。如果 *casefold* 为 True，则接受大写和小写字母。否则，只允许出现大写字母（默认）。如果存在 *map01*，它指定了数字 1 映射到的字母（例如，字母 'I' 或字母 'L'）。如果提供了此参数，数字 '0' 也会映射到字母 'O'。如果输入字符串包含多余字符或填充不正确，将引发 TypeError。

```
b16encode(s)
```

使用 base 16（十六进制）编码对字节字符串 *s* 进行编码。

```
b16decode(s [, casefold])
```

使用 base 16（十六进制）编码解码字符串 *s*。如果 *casefold* 为 True，字母可以是大写或小写。否则，十六进制字母 'A'–'F' 必须是大写（默认）。如果输入字符串包含多余字符或格式不正确，将引发 TypeError。

以下函数属于旧版 base 64 模块接口，你可能会在现有 Python 代码中看到：

```
decode(input, output)
```

解码 base 64 编码的数据。*input* 是一个文件名或一个为读取而打开的文件对象。*output* 是一个文件名或一个以二进制模式为写入而打开的文件对象。

```
decodestring(s)
```

解码一个 base 64 编码的字符串 *s*。返回一个包含解码后二进制数据的字符串。

```
encode(input, output)
```

使用 base 64 编码数据。*input* 是一个文件名或一个以二进制模式为读取而打开的文件对象。*output* 是一个文件名或一个为写入而打开的文件对象。

```
encodestring(s)
```

使用 base 64 对字节字符串 *s* 进行编码。

#### binascii

`binascii` 模块包含用于在二进制数据和多种 ASCII 编码（如 base 64、BinHex 和 UUencoding）之间转换的底层函数。

```
a2b_uu(s)
```

将一行 uuencoded 文本 *s* 转换为二进制数据，并返回一个字节字符串。行通常包含 45 个（二进制）字节，但最后一行可能少于 45 个字节。行数据后面可以跟有空白字符。

```
b2a_uu(data)
```

将一个二进制数据字符串转换为一行 uuencoded ASCII 字符。*data* 的长度不应超过 45 字节。否则，将引发 Error 异常。

```
a2b_base64(string)
```

将一个 base 64 编码的文本字符串转换为二进制数据，并返回一个字节字符串。

```
b2a_base64(data)
```

将一个二进制数据字符串转换为一行 base 64 编码的 ASCII 字符。如果生成的输出需要通过电子邮件传输，则 *data* 的长度不应超过 57 字节（否则可能会被截断）。



##### a2b_hex(string)

将十六进制数字字符串转换为二进制数据。此函数也称为 unhexlify(string)。

##### b2a_hex(data)

将二进制数据字符串转换为十六进制编码。此函数也称为 hexlify(data)。

##### a2b_hqx(string)

将 BinHex 4 编码的数据字符串转换为二进制数据，不执行 RLE（游程编码）解压缩。

##### rledecode_hqx(data)

对 data 中的二进制数据执行 RLE 解压缩。返回解压缩后的数据，除非输入数据不完整，此时会引发 Incomplete 异常。

##### rlecode_hqx(data)

对 data 执行 BinHex 4 RLE 压缩。

##### b2a_hqx(data)

##### crc_hqx(data, crc)

计算字节字符串 data 的 BinHex 4 CRC 校验和。crc 是校验和的起始值。

##### crc32(data [, crc])

计算字节字符串 data 的 CRC-32 校验和。crc 是一个可选的初始 CRC 值。如果省略，crc 默认为 0。

#### CSV

csv 模块用于读写由逗号分隔值（CSV）组成的文件。CSV 文件由文本行组成，每行包含由分隔符字符（通常是逗号(,)或制表符）分隔的值。以下是一个示例：

```
Blues,Elwood,"1060 W Addison","Chicago, IL 60613","B263-1655-2187",116,56
```

在处理数据库和电子表格时，通常会遇到这种格式的变体。例如，数据库可能以 CSV 格式导出表格，以便其他程序可以读取这些表格。当字段包含分隔符字符时，会产生细微的复杂情况。例如，在前面的示例中，其中一个字段包含一个逗号，必须放在引号中。这就是为什么使用像 split(',') 这样的基本字符串操作通常不足以处理此类文件。

```
reader(csvfile [, dialect [, **fmtparams]])
```

返回一个读取器对象，该对象为输入文件 csvfile 的每一行输入产生值。csvfile 可以是任何可迭代对象，在每次迭代时产生完整的文本行。返回的读取器对象是一个迭代器，在每次迭代时产生一个字符串列表。dialect 参数可以是一个包含方言名称的字符串，也可以是一个 Dialect 对象。dialect 参数的目的是考虑不同 CSV 编码之间的差异。此模块支持的唯一内置方言是 'excel'（默认值）和 'excel-tab'，但用户可以按照本节后面描述的方式定义其他方言。fmtparams 是一组关键字参数，用于自定义方言的各个方面。可以给出以下关键字参数：

| 关键字参数 | 描述 |
| --- | --- |
| delimiter | 用于分隔字段的字符（默认为 ','）。 |
| doublequote | 一个布尔标志，用于确定当引号字符（quotechar）出现在字段中时如何处理。如果为 True，则该字符只是加倍。如果为 False，则使用转义字符（escapechar）作为前缀。默认值为 True。 |
| escapechar | 当分隔符出现在字段中且 quoting 为 QUOTE_NONE 时用作转义字符的字符。默认值为 None。 |
| lineterminator | 行终止序列（默认为 '\r\n'）。 |
| quotechar | 用于引用包含分隔符的字段的字符（默认为 '"'）。 |
| skipinitialspace | 如果为 True，则忽略分隔符后紧跟的空格（默认为 False）。 |

```
writer(csvfile [, dialect [, **fmtparam]])
```

返回一个写入器对象，可用于创建 CSV 文件。csvfile 可以是任何支持 write() 方法的类似文件的对象。dialect 的含义与 reader() 相同，用于处理各种 CSV 编码之间的差异。fmtparams 的含义与读取器相同。但是，有一个额外的关键字参数可用：

| 关键字参数 | 描述 |
| --- | --- |
| quoting | 控制输出数据的引号行为。它设置为以下值之一：QUOTE_ALL（引用所有字段）、QUOTE_MINIMAL（仅引用包含分隔符或以引号字符开头的字段）、QUOTE_NONNUMERIC（引用所有非数字字段）或 QUOTE_NONE（从不引用字段）。默认值为 QUOTE_MINIMAL。 |

写入器实例 w 支持以下方法：

```
w.writerow(row)
```

将单行数据写入文件。row 必须是一个字符串或数字序列。

**w.writerows(rows)**

写入多行数据。*rows* 必须是一个行序列，与传递给 `writerow()` 方法的格式相同。

**DictReader(csvfile [, fieldnames [, restkey [, restval [, dialect [, **fmtparams]]]]])**

返回一个读取器对象，其操作方式类似于普通读取器，但在读取文件时返回字典对象而不是字符串列表。*fieldnames* 提供一个字段名称列表，用作返回字典中的键。如果省略，则字典键名取自输入文件的第一行。*restkey* 提供一个字典键的名称，用于存储多余的数据——例如，如果一行的数据字段多于字段名称。*restval* 是一个默认值，用于输入中缺失字段的值——例如，如果一行没有足够的字段。*restkey* 和 *restval* 的默认值是 `None`。*dialect* 和 *fmtparams* 的含义与 `reader()` 相同。

**DictWriter(csvfile, fieldnames [, restval [, extrasaction [, dialect [, **fmtparams]]]])**

返回一个写入器对象，其操作方式类似于普通写入器，但将字典写入输出行。*fieldnames* 指定将写入文件的属性的顺序和名称。*restval* 是当正在写入的字典缺少 *fieldnames* 中的某个字段名时写入的值。*extrasaction* 是一个字符串，指定当正在写入的字典具有 *fieldnames* 中未列出的键时该怎么办。*extrasaction* 的默认值是 `'raise'`，它会引发 `ValueError` 异常。可以使用值 `'ignore'`，在这种情况下，字典中的额外值将被忽略。*dialect* 和 *fmtparams* 的含义与 `writer()` 相同。

`DictWriter` 实例 *w* 支持以下方法：

**w.writerow(row)**

将单行数据写入文件。*row* 必须是一个将字段名称映射到值的字典。

**w.writerows(rows)**

写入多行数据。*rows* 必须是一个行序列，与传递给 `writerow()` 方法的格式相同。

**Sniffer()**

创建一个 `Sniffer` 对象，用于尝试自动检测 CSV 文件的格式。

`Sniffer` 实例 *s* 具有以下方法：

**s.sniff(sample [, delimiters])**

查看 *sample* 中的数据，并返回一个适当的 `Dialect` 对象来表示数据格式。*sample* 是 CSV 文件的一部分，至少包含一行数据。*delimiters*（如果提供）是一个包含可能字段分隔符字符的字符串。

**s.has_header(sample)**

查看 *sample* 中的 CSV 数据，如果第一行看起来像列标题的集合，则返回 `True`。

##### 方言

csv 模块中的许多函数和方法都涉及一个特殊的 dialect 参数。此参数的目的是适应 CSV 文件的不同格式约定（对于 CSV 文件，没有官方的“标准”格式）——例如，逗号分隔值和制表符分隔值之间的差异、引号约定等等。

方言通过继承 Dialect 类并定义与传递给 reader() 和 writer() 函数相同的属性集（delimiter、doublequote、escapechar、lineterminator、quotechar、quoting、skipinitialspace）来定义。

以下实用函数用于管理方言：

**register_dialect(name, dialect)**

在名称 name 下注册一个新的 Dialect 对象 dialect。

**unregister_dialect(name)**

删除名为 name 的 Dialect 对象。

**get_dialect(name)**

返回名为 name 的 Dialect 对象。

**list_dialects()**

返回所有已注册方言名称的列表。目前，只有两个内置方言：'excel' 和 'excel-tab'。

##### 示例

```python
import csv
# 读取基本 CSV 文件
f = open("scmods.csv","r")
for r in csv.reader(f):
    lastname, firstname, street, city, zip = r
    print("{0} {1} {2} {3} {4}".format(*r))

# 使用 DictReader 代替
f = open("address.csv")
r = csv.DictReader(f,['lastname','firstname','street','city','zip'])
for a in r:
    print("{firstname} {lastname} {street} {city} {zip}".format(**a))

# 写入基本 CSV 文件
data = [
 ['Blues','Elwood','1060 W Addison','Chicago','IL','60613' ],
 ['McGurn','Jack','4802 N Broadway','Chicago','IL','60640' ],
]
f = open("address.csv","w")
w = csv.writer(f)
w.writerows(data)
f.close()
```

#### email 包

email 包提供了各种各样的函数和对象，用于表示、解析和操作根据 MIME 标准编码的电子邮件消息。

在这里详细讲解 email 包的每个细节既不现实，也不会让大多数读者感兴趣。因此，本节余下部分将重点讨论两个常见的实际问题——解析电子邮件消息以提取有用信息，以及创建电子邮件消息以便可以使用 `smtplib` 模块进行发送。

##### 解析电子邮件

在顶层，email 模块提供了两个用于解析消息的函数：

```
message_from_file(f)
```

从类似文件的对象 `f`（必须以文本模式打开）中读取并解析一封电子邮件消息。输入的消息应该是一封完整的 MIME 编码的电子邮件消息，包括所有头部、文本和附件。返回一个 `Message` 实例。

```
message_from_string(str)
```

通过从文本字符串 `str` 中读取电子邮件消息来解析该消息。返回一个 `Message` 实例。

上述函数返回的 `Message` 实例 `m` 模拟了一个字典，并支持以下用于查找消息数据的操作：

| 操作 | 描述 |
| --- | --- |
| m[name] | 返回头部 `name` 的值。 |
| m.keys() | 返回所有消息头部名称的列表。 |
| m.values() | 返回消息头部值的列表。 |
| m.items() | 返回包含消息头部名称和值的元组列表。 |
| m.get(name [,def]) | 返回头部 `name` 的值。`def` 指定在未找到时返回的默认值。 |
| len(m) | 返回消息头部的数量。 |
| str(m) | 将消息转换为字符串。与 `as_string()` 方法相同。 |
| name in m | 如果 `name` 是消息中某个头部的名称，则返回 `True`。 |

除了这些操作符之外，`m` 还有以下可用于提取信息的方法：

```
m.get_all(name [, default])
```

返回名为 `name` 的头部的所有值的列表。如果不存在这样的头部，则返回 `default`。

```
m.get_boundary([default])
```

返回在消息的 `'Content-type'` 头部中找到的边界参数。通常边界是一个字符串，例如 `'==============095017162=='`，用于分隔消息的不同子部分。如果找不到边界参数，则返回 `default`。

```
m.get_charset()
```

返回与消息负载相关联的字符集（例如，`'iso-8859-1'`）。

```
m.get_charsets([default])
```

返回消息中出现的所有字符集的列表。对于多部分消息，该列表将表示每个子部分的字符集。每个部分的字符集取自消息中出现的 `'Content-type'` 头部。如果未指定字符集或缺少内容类型头部，则该部分的字符集设置为 `default` 的值（默认为 `None`）。

```
m.get_content_charset([default])
```

返回消息中第一个 `'Content-type'` 头部的字符集。如果未找到该头部或未指定字符集，则返回 `default`。

```
m.get_content_maintype()
```

返回主要的内容类型（例如，`'text'` 或 `'multipart'`）。

```
m.get_content_subtype()
```

返回子内容类型（例如，`'plain'` 或 `'mixed'`）。

```
m.get_content_type()
```

返回一个包含消息内容类型的字符串（例如，`'multipart/mixed'` 或 `'text/plain'`）。

```
m.get_default_type()
```

返回默认内容类型（例如，对于简单消息为 `'text/plain'`）。

```
m.get_filename([default])
```

如果存在，返回来自 `'Content-Disposition'` 头部的 `filename` 参数。如果缺少该头部或该头部没有文件名参数，则返回 `default`。

```
m.get_param(param [, default [, header [, unquote]]])
```

电子邮件头部通常附带有参数，例如头部 `'Content-Type: text/plain; charset="utf-8"; format=flowed'` 中的 `'charset'` 和 `'format'` 部分。此方法返回特定头部参数的值。`param` 是参数名称，`default` 是在未找到参数时返回的默认值，`header` 是头部的名称，`unquote` 指定是否对参数进行反引号处理。如果未给 `header` 值，则从 `'Content-type'` 头部获取参数。`unquote` 的默认值为 `True`。返回值要么是字符串，要么是按照 RFC-2231 约定编码的 3 元组（`charset, language, value`）。在这种情况下，`charset` 是一个字符串，如 `'iso-8859-1'`，`language` 是包含语言代码的字符串，如 `'en'`，`value` 是参数值。

```
m.get_params([default [, header [, unquote]]])
```

以列表形式返回 `header` 的所有参数。`default` 指定在未找到头部时返回的值。如果省略 `header`，则使用 `'Content-type'` 头部。`unquote` 是一个标志，指定是否对值进行反引号处理（默认为 `True`）。返回列表的内容是元组 `(name, value)`，其中 `name` 是参数名称，`value` 是作为 `get_param()` 方法返回的值。

```
m.get_payload([i [, decode]])
```

返回消息的负载。如果消息是一个简单消息，则返回一个包含消息正文的 *字节字符串*。如果消息是多部分消息，则返回一个包含所有子部分的列表。对于多部分消息，`i` 指定此列表中的可选索引。如果提供了索引，则仅返回该消息组件。如果 `decode` 为 `True`，则负载将根据任何可能存在的 `'Content-Transfer-Encoding'` 头部的设置进行解码（例如，`'quoted-printable'`、`'base64'` 等等）。要解码简单非多部分消息的负载，请将 `i` 设置为 `None` 并将 `decode` 设置为 `True`，或使用关键字参数指定 `decode`。应该强调的是，负载作为包含原始内容的字节字符串返回。如果负载表示以 UTF-8 或其他某种编码编码的文本，你需要使用结果上的 `decode()` 方法将其转换。

```
m.get_unixfrom()
```

如果存在，返回 UNIX 风格的 `'From ...'` 行。

```
m.is_multipart()
```

如果 `m` 是多部分消息，则返回 `True`。

```
m.walk()
```

创建一个生成器，该生成器遍历消息的所有子部分，每个子部分也由一个 `Message` 实例表示。遍历是对消息进行深度优先遍历。通常，此函数可用于处理多部分消息的所有组件。

最后，`Message` 实例有一些与底层解析过程相关的属性。

```
m.preamble
```

在多部分消息中，出现在表示头部结束的空行与标记消息第一个子部分的第一个多部分边界字符串之间的任何文本。

```
m.epilogue
```

消息中出现在最后的多部分边界字符串之后以及消息结束之前的任何文本。

```
m.defects
```

解析消息时发现的所有消息缺陷的列表。有关更多详细信息，请查阅 `email.errors` 模块的在线文档。

以下示例说明了在解析电子邮件消息时如何使用 `Message` 类。以下代码读取一封电子邮件消息，打印有关有用头部的简短摘要，打印消息的纯文本部分，并保存任何附件。

```
import email
import sys

f = open(sys.argv[1],"r")    # 打开消息文件
m = email.message_from_file(f)   # 解析消息

# 打印发件人/收件人的简短摘要
print("From    : %s" % m["from"])
print("To      : %s" % m["to"])
print("Subject : %s" % m["subject"])
print("")

if not m.is_multipart():
    # 简单消息。只需打印负载
    payload = m.get_payload(decode=True)
    charset = m.get_content_charset('iso-8859-1')
    print(payload.decode(charset))
else:
    # 多部分消息。   遍历所有子部分并
    #    1. 打印 text/plain 片段
    #    2. 保存任何附件
    for s in m.walk():
        filename = s.get_filename()
        if filename:
            print("Saving attachment: %s" % filename)
            data = s.get_payload(decode=True)
            open(filename,"wb").write(data)
        else:
            if s.get_content_type() == 'text/plain':
                payload = s.get_payload(decode=True)
                charset = s.get_content_charset('iso-8859-1')
                print(payload.decode(charset))
```

在此示例中，重要的是要强调提取消息负载的操作总是返回字节字符串。如果负载表示文本，你还需要根据某种字符集对其进行解码。示例中的 `m.get_content_charset()` 和 `payload.decode()` 操作正在执行此转换。

##### 撰写电子邮件

要撰写电子邮件消息，你可以创建 `email.message` 模块中定义的 `Message` 对象的空实例，也可以使用通过解析电子邮件消息创建的 `Message` 对象（参见上一节）。

**Message()**

创建一个新的初始为空的消息。

`Message` 的实例 `m` 支持以下方法，用于用内容、头部和其他信息填充消息。

**m.add_header(name, value, **params)**

添加一个新的消息头部。`name` 是头部的名称，`value` 是头部的值，`params` 是一组关键字参数，用于提供额外的可选参数。例如，`add_header('Foo','Bar',spam='major')` 将头部行 `'Foo: Bar; spam="major"'` 添加到消息中。

**m.as_string([unixfrom])**

将整个消息转换为字符串。`unixfrom` 是一个布尔标志。如果设置为 `True`，则 UNIX 风格的 `'From ...'` 行将作为第一行出现。默认情况下，`unixfrom` 为 `False`。



## 558 第24章 互联网数据处理与编码

```python
m.attach(payload)
```

将一个附件添加到多部分消息中。`payload`必须是另一个`Message`对象（例如，`email.mime.text.MIMEText`）。内部实现中，`payload`会被追加到一个用于跟踪消息不同部分的列表中。如果消息不是多部分消息，请使用`set_payload()`将消息主体设置为一个简单的字符串。

```python
m.del_param(param [, header [, requote]])
```

从`header`头中删除参数`param`。例如，如果消息有一个头`'Foo: Bar; spam="major"'`，那么`del_param('spam','Foo')`将删除头中的`'spam="major"'`部分。如果`requote`为`True`（默认值），在重写头时，所有剩余的值都会被加上引号。如果省略`header`，则该操作应用于`'Content-type'`头。

```python
m.replace_header(name, value)
```

将第一个出现的头`name`的值替换为`value`。如果未找到该头，则引发`KeyError`。

```python
m.set_boundary(boundary)
```

将消息的边界参数设置为字符串`boundary`。此字符串将作为边界参数添加到消息的`'Content-type'`头中。如果消息没有`'Content-type'`头，则引发`HeaderParseError`。

```python
m.set_charset(charset)
```

设置消息使用的默认字符集。`charset`可以是一个字符串，如`'iso-8859-1'`或`'euc-jp'`。设置字符集通常会向消息的`'Content-type'`头添加一个参数（例如，`'Content-type: text/html; charset="iso-8859-1"'`）。

```python
m.set_default_type(ctype)
```

将默认消息内容类型设置为`ctype`。`ctype`是一个包含MIME类型的字符串，如`'text/plain'`或`'message/rfc822'`。此类型不会存储在消息的`'Content-type'`头中。

```python
m.set_param(param, value [, header [, requote [, charset [, language]]]])
```

设置头参数的值。`param`是参数名，`value`是参数值。`header`指定头的名称，默认为`'Content-type'`。`requote`指定在添加参数后是否重新引用头中的所有值。默认情况下，这是`True`。`charset`和`language`指定可选的字符集和语言信息。如果提供了这些信息，则根据RFC-2231对参数进行编码。这将生成类似`param*="'iso-8859-1'en-us'some%20value"`的参数文本。

```python
m.set_payload(payload [, charset])
```

将整个消息负载设置为`payload`。对于简单消息，`payload`可以是一个包含消息主体的字节字符串。对于多部分消息，`payload`是一个`Message`对象列表。可选的`charset`参数指定用于编码文本的字符集（参见`set_charset`）。

```python
m.set_type(type [, header [, requote]])
```

设置`'Content-type'`头中使用的类型。`type`是指定类型的字符串，如`'text/plain'`或`'multipart/mixed'`。`header`指定默认`'Content-type'`头以外的替代头。`requote`为已附加到头的任何参数的值加上引号。默认情况下，这是`True`。

```python
m.set_unixfrom(unixfrom)
```

设置UNIX风格的`'From ...'`行的文本。`unixfrom`是包含完整文本（包括`'From'`文本）的字符串。仅当`m.as_string()`的`unixfrom`参数设置为`True`时，才会输出此文本。

与其每次从头创建原始`Message`对象并手动构建它们，不如使用一系列预构建的消息对象，这些对象对应不同类型的内容。这些消息对象对于创建多部分MIME消息特别有用。例如，你可以创建一个新消息，并使用`Message`的`attach()`方法附加不同的部分。每个对象都在一个不同的子模块中定义，这在每个描述中都有说明。

```python
MIMEApplication(data [, subtype [, encoder [, **params]]])
```

在`email.mime.application`中定义。创建一个包含应用程序数据的消息。`data`是一个包含原始数据的字节字符串。`subtype`指定数据子类型，默认为`'octet-stream'`。`encoder`是来自`email.encoders`子包的可选编码函数。默认情况下，数据编码为base64。`params`表示可选的关键字参数和值，将添加到消息的`'Content-type'`头中。

```python
MIMEAudio(data [, subtype [, encoder [, **params]]])
```

在`email.mime.audio`中定义。创建一个包含音频数据的消息。`data`是一个包含原始二进制音频数据的字节字符串。`subtype`指定数据的类型，是一个如`'mpeg'`或`'wav'`的字符串。如果未提供`subtype`，则通过`sndhdr`模块查看数据来猜测音频类型。`encoder`和`params`与`MIMEApplication`具有相同的含义。

```python
MIMEImage(data [, subtype [, encoder [, **params]]])
```

在`email.mime.image`中定义。创建一个包含图像数据的消息。`data`是一个包含原始图像数据的字节字符串。`subtype`指定图像类型，是一个如`'jpg'`或`'png'`的字符串。如果未提供`subtype`，则使用`imghdr`模块中的函数来猜测类型。`encoder`和`params`与`MIMEApplication`具有相同的含义。

```python
MIMEMessage(msg [, subtype])
```

在`email.mime.message`中定义。创建一个新的非多部分MIME消息。`msg`是一个包含消息初始负载的消息对象。`subtype`是消息的类型，默认为`'rfc822'`。

```python
MIMEMultipart([subtype [, boundary [, subparts [, **params]]]])
```

在`email.mime.multipart`中定义。创建一个新的MIME多部分消息。`subtype`指定要添加到`'Content-type: multipart/subtype'`头的可选子类型。默认情况下，`subtype`是`'mixed'`。`boundary`是一个字符串，指定用于分隔每个消息子部分的边界分隔符。如果设置为`None`或省略，则自动确定合适的边界。`subparts`是一个`Message`对象序列，构成消息的内容。`params`表示可选的关键字参数和值，将添加到消息的`'Content-type'`头中。一旦创建了多部分消息，就可以使用`Message.attach()`方法添加额外的子部分。

```python
MIMEText(data [, subtype [, charset]])
```

在`email.mime.text`中定义。创建一个包含文本数据的消息。`data`是一个包含消息负载的字符串。`subtype`指定文本类型，是一个如`'plain'`（默认）或`'html'`的字符串。`charset`是字符集，默认为`'us-ascii'`。根据消息的内容，消息可能会被编码。

以下示例展示了如何使用本节中的类来编写和发送电子邮件消息：

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.audio import MIMEAudio

sender  = "jon@nogodiggydie.net"
receiver= "dave@dabeaz.com"
subject = "Faders up!"
body    = "I never should have moved out of Texas. -J.\n"
audio   = "TexasFuneral.mp3"

m = MIMEMultipart()
m["to"]      = receiver
m["from"]    = sender
m["subject"] = subject

m.attach(MIMEText(body))
apart = MIMEAudio(open(audio,"rb").read(),"mpeg")
apart.add_header("Content-Disposition","attachment",filename=audio)
m.attach(apart)

# Send the email message
s = smtplib.SMTP()
s.connect()
s.sendmail(sender, [receiver],m.as_string())
s.close()
```

##### 注意事项

-   许多高级自定义和配置选项未在本文讨论。读者应查阅在线文档以了解此模块的高级用法。
-   `email`包已经经历了至少四个不同的版本，其底层编程接口也发生了变化（例如，子模块重命名，类移动到不同的位置等）。本节记录了在Python 2.6和Python 3.0中都使用的4.0版本接口。如果你正在处理遗留代码，基本概念仍然适用，但你可能需要调整类和子模块的位置。



#### hashlib

`hashlib` 模块实现了多种安全哈希和消息摘要算法，例如 MD5 和 SHA1。要计算哈希值，你需要首先调用以下函数之一，函数名与对应的算法名称相同：

| 函数 | 描述 |
|------|------|
| `md5()` | MD5 哈希（128 位） |
| `sha1()` | SHA1 哈希（160 位） |
| `sha224()` | SHA224 哈希（224 位） |
| `sha256()` | SHA256 哈希（256 位） |
| `sha384()` | SHA384 哈希（384 位） |
| `sha512()` | SHA512 哈希（512 位） |

由上述任一函数返回的摘要对象 *d* 实例具有以下接口：

| 方法或属性 | 描述 |
|------------|------|
| `d.update(data)` | 用新的数据更新哈希值。`data` 必须是一个字节字符串。重复调用与使用连接后的数据进行单次调用效果相同。 |
| `d.digest()` | 以原始字节字符串的形式返回摘要值。 |
| `d.hexdigest()` | 返回一个文本字符串，其中包含以十六进制数字列表示的摘要值。 |
| `d.copy()` | 返回摘要对象的一个副本。副本保留原始摘要对象的内部状态。 |
| `d.digest_size` | 结果哈希的大小（以字节为单位）。 |
| `d.block_size` | 哈希算法的内部块大小（以字节为单位）。 |

该模块还提供了另一种构造接口：

```
`new(hashname)`
```

创建一个新的摘要对象。`hashname` 是一个字符串，例如 `'md5'` 或 `'sha256'`，用于指定要使用的哈希算法名称。哈希名称至少可以是前面提到的任何一种哈希算法，或者是 OpenSSL 库公开提供的哈希算法（这取决于安装情况）。

#### hmac

`hmac` 模块提供了对 HMAC（基于哈希的消息认证码）的支持，该机制在 RFC-2104 中有描述。HMAC 是一种基于 MD5 和 SHA-1 等加密哈希函数构建的消息认证机制。

```
`new(key [, msg [, digest]])`
```

创建一个新的 HMAC 对象。其中，`key` 是一个包含哈希起始密钥的字节字符串，`msg` 包含要处理的初始数据，`digest` 是用于加密哈希的摘要构造函数。默认情况下，`digest` 是 `hashlib.md5`。

通常，初始密钥值是使用密码学安全的随机数生成器随机确定的。

HMAC 对象 *h* 具有以下方法：

```
h.update(msg)
```

将字符串 *msg* 添加到 HMAC 对象中。

```
h.digest()
```

返回目前为止处理的所有数据的摘要，并返回一个包含摘要值的字节字符串。字符串的长度取决于底层的哈希函数。对于 MD5，长度是 16 个字符；对于 SHA-1，长度是 20 个字符。

```
h.hexdigest()
```

以十六进制数字字符串的形式返回摘要。

```
h.copy()
```

创建 HMAC 对象的一个副本。

##### 示例

hmac 模块的主要用途是在需要验证消息发送者身份的应用程序中。为此，`new()` 的 *key* 参数是一个代表发送者和接收者共同已知的秘密密钥的字节字符串。发送消息时，发送者会用给定的密钥创建一个新的 HMAC 对象，用待发送的消息数据更新该对象，然后将消息数据和生成的 HMAC 摘要值一起发送给接收者。接收者可以通过计算自己的 HMAC 摘要值（使用相同的密钥和消息数据）并将结果与接收到的摘要值进行比较来验证消息。以下是一个示例：

```
import hmac
secret_key = b"peekaboo"                          # 仅我自己知道的字节字符串。通常
                                                 # 你会想使用使用 os.urandom() 或类似方法
                                                 # 计算的随机字节字符串。

data = b"Hello World"                            # 要发送的消息

# 将消息发送到某处。 out 表示一个套接字或我们正在
# 发送数据的其他 I/O 通道。
h = hmac.new(secret_key)
h.update(data)
out.send(data)                                  # 发送数据
out.send(h.digest())                            # 发送摘要

# 接收消息
# in 表示一个套接字或我们正在接收数据的其他 I/O 通道。
h = hmac.new(secret_key)
data = in.receive()                             # 获取消息数据
h.update(data)
digest = in.receive()                           # 获取发送者发送的摘要
if digest != h.digest():
    raise AuthenticationError('Message not authenticated')
```

#### HTMLParser

在 Python 3 中，该模块名为 `html.parser`。`HTMLParser` 模块定义了一个名为 `HTMLParser` 的类，可用于解析 HTML 和 XHTML 文档。要使用此模块，你需要定义自己的类，该类继承自 `HTMLParser`，并相应地重新定义方法。

##### `HTMLParser()`

这是一个用于创建 HTML 解析器的基类。初始化时无需任何参数。

`HTMLParser` 的实例 `h` 具有以下方法：

##### `h.close()`

关闭解析器并强制处理任何剩余的未解析数据。在所有 HTML 数据都已传递给解析器后调用此方法。

##### `h.feed(data)`

向解析器提供新数据。此数据将立即被解析。但是，如果数据不完整（例如，它以一个不完整的 HTML 元素结尾），则不完整的部分将被缓冲，并在下次使用更多数据调用 `feed()` 时进行解析。

##### `h.getpos()`

返回当前行号和该行内的字符偏移量，作为一个元组 (`line`, `offset`)。

##### `h.get_starttag_text()`

返回与最近打开的开始标签相对应的文本。

##### `h.handle_charref(name)`

每当遇到字符引用（例如 `'&#ref;'`）时，会调用此处理方法。`name` 是一个包含引用名称的字符串。例如，当解析 `'&#229;'` 时，`name` 将被设置为 `'229'`。

##### `h.handle_comment(data)`

每当遇到注释时，会调用此处理方法。`data` 是一个包含注释文本的字符串。例如，当解析注释 `'<!--comment-->'` 时，`data` 将包含文本 `'comment'`。

##### `h.handle_data(data)`

此处理方法用于处理出现在标签之间的数据。`data` 是一个包含文本的字符串。

##### `h.handle_decl(decl)`

此处理方法用于处理声明，例如 `'<!DOCTYPE HTML ...>'`。`decl` 是一个包含声明文本的字符串，不包括开头的 `'<!'` 和结尾的 `'>'`。

##### `h.handle_endtag(tag)`

每当遇到结束标签时，会调用此处理方法。`tag` 是转换为小写的标签名称。例如，如果结束标签是 `</BODY>`，`tag` 就是字符串 `'body'`。

##### `h.handle_entityref(name)`

此处理方法用于处理实体引用，例如 `'&name;'`。`name` 是一个包含引用名称的字符串。例如，如果解析 `'&lt;'`，`name` 将被设置为 `'lt'`。

##### `h.handle_pi(data)`

此处理方法用于处理处理指令，例如 `'<?processing instruction>'`。`data` 是一个包含处理指令文本的字符串，不包括开头的 `'<?'` 或结尾的 `'>'`。当对形如 `'<?...?>'` 的 XHTML 风格的指令调用时，最后一个 `'?'` 将包含在 `data` 中。

##### `h.handle_startendtag(tag, attrs)`

此处理方法处理 XHTML 风格的空标签，例如 '`<tag name="value"... />`'。`tag` 是一个包含标签名称的字符串。`attrs` 包含属性信息，是一个元组列表，形式为 `(name, value)`，其中 `name` 是转换为小写的属性名，`value` 是属性值。提取值时，引号和字符实体将被替换。例如，如果解析 '`<a href="http://www.foo.com"/>`'，`tag` 是 `'a'`，`attrs` 是 `[('href', 'http://www.foo.com')]`。如果在派生类中未定义，此方法的默认实现将简单调用 `handle_starttag()` 和 `handle_endtag()`。

##### `h.handle_starttag(tag, attrs)`

此处理方法处理开始标签，例如 '`<tag name="value" ...>`'。`tag` 和 `attrs` 的含义与 `handle_startendtag()` 中描述的相同。

##### `h.reset()`

重置解析器，丢弃任何未处理的数据。

提供了以下异常：

##### `HTMLParserError`

由于解析错误而引发的异常。该异常有三个属性。`msg` 属性包含描述错误的消息，`lineno` 属性是发生解析错误的行号，`offset` 属性是该行内的字符偏移量。

##### 示例

以下示例使用 `urllib` 包获取一个 HTML 文档，并打印所有通过 '`<a href="...">`' 声明指定的链接：

```
# printlinks.py
try:
    from HTMLParser import HTMLParser
    from urllib2 import urlopen
except ImportError:
    from html.parser import HTMLParser
```

from urllib.request import urlopen
import sys

class PrintLinks(HTMLParser):
    def handle_startag(self,tag,attrs):
        if tag == 'a':
            for name,value in attrs:
                if name == 'href': print(value)

p    = PrintLinks()
u    = urlopen(sys.argv[1])
data = u.read()
charset = u.info().getparam('charset')    # Python 2
#charset = u.info().get_content_charset()   # Python 3
p.feed(data.decode(charset))
p.close()

在上面的示例中，必须注意使用`urllib`获取的任何HTML都会作为字节字符串返回。为了正确解析它，必须根据文档的字符集编码将其解码为文本。示例展示了如何在Python 2和Python 3中实现这一点。

###### 注意

`HTMLParser`的解析能力往往相当有限。事实上，对于非常复杂和/或格式错误的HTML，解析器可能会崩溃。用户还发现该模块的层次较低，不够实用。如果你正在编写必须从HTML页面中抓取数据的程序，请考虑使用Beautiful Soup包 (http://pypi.python.org/pypi/BeautifulSoup)。

#### json

`json`模块用于序列化和反序列化使用JavaScript对象表示法（JSON）表示的对象。有关JSON的更多信息，请访问http://json.org，但该格式实际上是JavaScript语法的子集。顺便提一句，它与表示列表和字典的Python语法几乎相同。例如，一个JSON数组写成`[value1, value2, ... ]`，一个JSON对象写成`{name:value, name:value, ... }`。

下表显示了JSON值与Python值的映射关系。括号中列出的Python类型在编码时被接受，但在解码时不会返回（而是返回第一个列出的类型）。

| JSON 类型 | Python 类型 |
|-----------|-------------|
| `object` | `dict` |
| `array` | `list` (`tuple`) |
| `string` | `unicode` (`str`, `bytes`) |
| `number` | `int`, `float` |
| `true` | `True` |
| `false` | `False` |
| `null` | `None` |

对于字符串数据，应假设使用Unicode。如果在编码过程中遇到字节字符串，它们将默认使用`'utf-8'`解码为Unicode字符串（尽管这可以控制）。解码时，JSON字符串总是以Unicode形式返回。

以下函数用于编码/解码JSON文档：

```
dump(obj, f, **opts)
```

将*obj*序列化到一个类文件对象*f*。*opts*代表一组可指定的关键字参数，用于控制序列化过程：

| 关键字参数 | 描述 |
| --- | --- |
| `skipkeys` | 一个布尔标志，控制当字典的键（不是值）不是基本类型（如字符串或数字）时如何处理。如果为`True`，则跳过这些键。如果为`False`（默认值），则会引发`TypeError`。 |
| `ensure_ascii` | 一个布尔标志，决定是否可以将Unicode字符串写入文件`f`。默认情况下为`False`。只有在`f`是一个能正确处理Unicode的文件（例如由`codecs`模块创建或以特定编码打开的文件）时，才将其设置为`True`。 |
| `check_circular` | 一个布尔标志，决定是否检查容器的循环引用。默认情况下为`True`。如果设置为`False`并遇到循环引用，将引发`OverflowError`异常。 |
| `allow_nan` | 一个布尔标志，决定是否序列化超出范围的浮点值（例如，NaN、inf、-inf）。默认情况下为`True`。 |
| `cls` | 要使用的`JSONEncoder`子类。如果你通过继承`JSONEncoder`创建了自己的自定义编码器，则需要指定此项。如果给`dump()`提供了任何额外的关键字参数，它们将作为参数传递给此类的构造函数。 |
| `indent` | 一个非负整数，设置打印数组和对象成员时使用的缩进量。设置此项会产生一种美观打印的效果。默认情况下为`None`，这会导致结果以最紧凑的表示形式呈现。 |
| `separators` | 一个形式为`(item_separator, dict_separator)`的元组，其中`item_separator`是包含数组项之间分隔符的字符串，`dict_separator`是包含字典键值对之间分隔符的字符串。默认情况下，该值为`(',', ': ')`。 |
| `encoding` | 用于Unicode字符串的编码——默认为`'utf-8'`。 |
| `default` | 一个用于序列化不属于任何基本支持类型的对象的函数。它应该返回一个可以序列化的值（即字符串）或者引发`TypeError`。默认情况下，对于不支持的类型会引发`TypeError`。 |

```
dumps(obj, **opts)
```

与`dump()`相同，只是返回一个包含结果的字符串。

##### load(f, **opts)

反序列化文件类对象f上的JSON对象并返回。opts代表一组可指定的关键字参数，用于控制解码过程，接下来将进行描述。请注意，此函数调用f.read()来消耗f的整个内容。因此，它不应在任何类型的流式文件（例如套接字）上使用，因为在这些文件中，JSON数据可能作为更大或持续数据流的一部分被接收。

| 关键字参数 | 描述 |
| --- | --- |
| encoding | 用于解释任何被解码的字符串值的编码。默认为'utf-8'。 |
| strict | 一个布尔标志，决定是否允许字面量（未转义）换行符出现在JSON字符串中。默认为`True`，这意味着对于此类字符串会生成异常。 |
| cls | 用于解码的`JSONDecoder`子类。仅在你通过继承`JSONDecoder`创建了自定义解码器时指定。`load()`的任何额外关键字参数都会提供给类构造函数。 |
| object_hook | 每个被解码的JSON对象结果都会调用的函数。默认情况下，这是内置的`dict()`函数。 |
| parse_float | 用于解码JSON浮点值的函数。默认情况下，这是内置的`float()`函数。 |
| parse_int | 用于解码JSON整数值的函数。默认情况下，这是内置的`int()`函数。 |
| parse_constant | 用于解码JSON常量（如`'NaN'`、`'true'`、`'false'`等）的函数。 |

##### loads(s, **opts)

与`load()`相同，只是从字符串`s`反序列化一个对象。

尽管这些函数与`pickle`和`marshal`模块中的函数同名并且它们都序列化数据，但使用方式并不相同。具体来说，你不应该使用`dump()`将多个JSON编码对象写入同一个文件。同样，`load()`也不能用于从同一个文件中读取多个JSON编码对象（如果输入文件中有多个对象，你会得到一个错误）。JSON编码对象应被视为与HTML或XML相同的方式。例如，你通常不会将两个完全独立的XML文档简单地连接到同一个文件中。

如果你想自定义编码或解码过程，请继承这些基类：

##### JSONDecoder(**opts)

一个解码JSON数据的类。`opts`代表一组关键字参数，与`load()`函数使用的参数相同。`JSONDecoder`的一个实例`d`具有以下两个方法：

###### d.decode(s)

返回s中JSON对象的Python表示。s是一个字符串。

###### d.raw_decode(s)

返回一个元组`(pyobj, index)`，其中`pyobj`是`s`中JSON对象的Python表示，`index`是JSON对象在`s`中结束的位置。如果你试图从输入流中解析出一个对象，而流末尾有额外数据时，这非常有用。

##### JSONEncoder(**opts)

一个将Python对象编码为JSON的类。`opts`代表一组关键字参数，与`dump()`函数使用的参数相同。`JSONEncoder`的一个实例`e`具有以下方法：

###### e.default(obj)

当一个Python对象`obj`无法根据任何正常编码规则进行编码时调用的方法。该方法应返回可以编码的类型之一的结果（例如，字符串、列表或字典）。

###### e.encode(obj)

调用此方法创建Python对象`obj`的JSON表示。

###### e.iterencode(obj)

创建一个迭代器，该迭代器在计算过程中生成组成Python对象`obj`的JSON表示的字符串。创建JSON字符串的过程本质上是高度递归的。例如，它涉及迭代字典的键并遍历沿途找到的其他字典和列表。如果你使用此方法，你可以以逐块的方式处理输出，而不是将所有内容收集到一个巨大的内存字符串中。

如果你定义了从`JSONDecoder`或`JSONEncoder`继承的子类，如果你的类还定义了`__init__()`方法，则需要谨慎。为了处理所有关键字参数，你应该这样定义它：

```
class MyJSONDecoder(JSONDecoder):
    def __init__(self, **kwargs):
        # Get my own arguments
        foo = kwargs.pop('foo',None)
        bar = kwargs.pop('bar',None)
        # Initialize the parent with everything left over
        JSONDecoder.__init__(self,**kwargs)
```

#### mimetypes

`mimetypes`模块用于根据文件扩展名猜测与文件关联的MIME类型。它还将MIME类型转换为其标准文件扩展名。MIME类型由type/subtype对组成——例如`'text/html'`、`'image/png'`或`'audio/mpeg'`。

```
guess_type(filename [, strict])
```

根据文件名或URL猜测文件的MIME类型。返回一个元组`(type, encoding)`，其中`type`是形式为`"type/subtype"`的字符串，`encoding`是用于编码传输数据的程序（例如压缩或gzip）。如果无法猜测类型，则返回`(None, None)`。如果`strict`为`True`（

默认情况下，仅识别在IANA注册的官方MIME类型（参见 http://www.iana.org/assignments/media-types）。否则，一些常见但非官方的MIME类型也会被识别。

```
guess_extension(type [, strict])
```
根据MIME类型猜测标准文件扩展名。返回包含前导点（.）的文件扩展名字符串。对于未知类型返回None。如果strict为True（默认值），则仅识别官方MIME类型。

```
guess_all_extensions(type [, strict])
```
与guess_extension()相同，但返回所有可能的文件扩展名列表。

```
init([files])
```
初始化模块。files是一个文件名序列，用于读取并提取类型信息。这些文件包含将MIME类型映射到可接受文件后缀列表的行，如下所示：

```
image/jpeg:   jpe jpeg jpg
text/html:    htm html
...
```

```
read_mime_types(filename)
```
从给定文件名加载类型映射。返回将文件扩展名映射到MIME类型字符串的字典。如果文件名不存在或无法读取，则返回None。

```
add_type(type, ext [, strict])
```
向映射中添加新的MIME类型。type是MIME类型，如'text/plain'；ext是文件扩展名，如'.txt'；strict是布尔值，指示该类型是否为官方注册的MIME类型。默认情况下，strict为True。

#### quopri模块

quopri模块执行字节字符串的可打印引用传输编码和解码。此格式主要用于编码8位文本文件，这些文件大多可作为ASCII读取，但可能包含少量不可打印或特殊字符（例如，控制字符或128-255范围内的非ASCII字符）。以下规则描述了可打印引用编码的工作方式：

- 除'='外，任何可打印的非空白ASCII字符均按原样表示。
- '='字符用作转义字符。后跟两个十六进制数字时，表示具有该值的字符（例如，'=0C'）。等号由'=3D'表示。如果'='出现在行末，则表示软换行。这仅在必须将长行输入文本分割成多个输出行时发生。
- 空格和制表符保持原样，但不能出现在行尾。

当文档使用扩展ASCII字符集中的特殊字符时，通常会看到此格式。例如，如果文档包含文本"Copyright © 2009"，这可能由Python字节字符串`b'Copyright \xa9 2009'`表示。该字符串的可打印引用版本是`b'Copyright =A9 2009'`，其中特殊字符`'\xa9'`已被转义序列`'=A9'`替换。

```
decode(input, output [, header])
```
将字节解码为quopri格式。*input*和*output*是以二进制模式打开的文件对象。如果*header*为`True`，则下划线（`_`）将被解释为空格。否则，保持不变。这用于解码已编码的MIME头。默认情况下，*header*为`False`。

```
decodestring(s [, header])
```
解码字符串*s*。*s*可以是Unicode或字节字符串，但结果始终是字节字符串。*header*的含义与`decode()`相同。

```
encode(input, output, quotetabs [, header])
```
将字节编码为quopri格式。*input*和*output*是以二进制模式打开的文件对象。*quotetabs*如果设置为`True`，则强制制表符在正常引用规则之外也被引用。否则，制表符保持原样。默认情况下，*quotetabs*为`False`。*header*的含义与`decode()`相同。

```
encodestring(s [, quotetabs [, header]])
```
编码字节字符串*s*。结果也是字节字符串。*quotetabs*和*header*的含义与`encode()`相同。

##### 注意事项

> 可打印引用数据编码早于Unicode，仅适用于8位数据。尽管它最常应用于文本，但实际上仅适用于表示为单个字节的ASCII和扩展ASCII字符。使用此模块时，请确保所有文件均为二进制模式，并且您正在处理字节字符串。

#### xml包

Python包含多种用于处理XML数据的模块。XML处理的主题很庞大，涵盖每个细节超出了本书的范围。本节假设读者已经熟悉一些基本的XML概念。Steve Holzner的《Inside XML》（New Riders）或Elliotte Harold和W. Scott Means的《XML in a Nutshell》（O'Reilly and Associates）等书籍将有助于解释基本的XML概念。几本书讨论了使用Python进行XML处理，包括Christopher Jones的《Python & XML》（O'Reilly and Associates）和Sean McGrath的《XML Processing with Python》（Prentice Hall）。

Python提供两种XML支持。首先，对两种行业标准的XML解析方法提供基本支持——SAX和DOM。SAX（简单XML API）基于事件处理，其中XML文档按顺序读取，当遇到XML元素时，会触发处理程序函数进行处理。DOM（文档对象模型）构建表示整个XML文档的树结构。一旦树构建完成，DOM提供了遍历树和提取数据的接口。SAX和DOM API均非源自Python。相反，Python只是复制了为Java和JavaScript开发的标准编程接口。

虽然您当然可以使用SAX和DOM接口处理XML，但标准库中最方便的编程接口是ElementTree接口。这是一种Python特有的XML解析方法，充分利用了Python语言特性，大多数用户发现它比SAX或DOM显著更简单、更快捷。本节其余部分涵盖了所有三种XML解析方法，但ElementTree方法给出了最详细的说明。

请读者注意，此处的介绍仅专注于XML数据的基本解析。Python还包括与实现新型解析器、从零构建XML文档等相关的XML模块。此外，各种第三方扩展扩展了Python的功能，提供了额外的XML特性，如支持XSLT和XPATH。更多信息的链接可在http://wiki.python.org/moin/PythonXml找到。

##### XML示例文档

以下示例说明了一个典型的XML文档，此处为食谱描述。

```xml
<?xml version="1.0" encoding="iso-8859-1"?>
<recipe>
  <title>
  Famous Guacamole
  </title>
  <description>
  A southwest favorite!
  </description>
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

该文档由以标签（如`<title>....</title>`）开始和结束的*元素*组成。元素通常嵌套并组织成层次结构——例如，出现在`<ingredients>`下的`<item>`元素。在每个文档中，单个元素是文档根。在示例中，这是`<recipe>`元素。元素可选地具有属性，如项目元素`<item num="4">Large avocados, chopped</item>`所示。

处理XML文档通常涉及所有这些基本特性。例如，您可能想要从特定元素类型中提取文本和属性。要

要定位元素，你必须从根元素开始，遍历文档层次结构。

###### xml.dom.minidom

`xml.dom.minidom` 模块提供了基本支持，用于解析 XML 文档并根据 DOM 约定将其存储为内存中的树结构。它包含两个解析函数：

```
parse(file [, parser])
```

解析 `file` 的内容，并返回一个代表文档树顶部的节点。`file` 是一个文件名或一个已打开的文件对象。`parser` 是一个可选的、兼容 SAX2 的解析器对象，用于构建树。如果省略，将使用默认的解析器。

```
parseString(string [, parser])
```

与 `parse()` 相同，区别在于输入数据是以字符串形式提供，而不是文件。

####### 节点

解析函数返回的文档树由相互连接的节点集合组成。每个节点 `n` 都有以下属性，可用于提取信息和遍历树结构：

| 节点属性 | 描述 |
|---|---|
| n.attributes | 保存属性值（如果有的话）的映射对象。 |
| n.childNodes | `n` 的所有子节点的列表。 |
| n.firstChild | 节点 `n` 的第一个子节点。 |
| n.lastChild | 节点 `n` 的最后一个子节点。 |
| n.localName | 元素的本地标签名。如果标签中出现冒号（例如，`'<foo:bar ...>'`），则此处仅包含冒号后的部分。 |
| n.namespaceURI | 与 `n` 关联的命名空间（如果有的话）。 |
| n.nextSibling | 在树中紧跟在 `n` 之后且具有相同父节点的节点。如果 `n` 是最后一个同级节点，则返回 `None`。 |
| n.nodeName | 节点的名称。含义取决于节点类型。 |
| n.nodeType | 描述节点类型的整数。它被设置为以下值之一（这些是 `Node` 类的类变量）：`ATTRIBUTE_NODE`, `CDATA_SECTION_NODE`, `COMMENT_NODE`, `DOCUMENT_FRAGMENT_NODE`, `DOCUMENT_NODE`, `DOCUMENT_TYPE_NODE`, `ELEMENT_NODE`, `ENTITY_NODE`, `ENTITY_REFERENCE_NODE`, `NOTATION_NODE`, `PROCESSING_INSTRUCTION_NODE`, 或 `TEXT_NODE`。 |
| n.nodeValue | 节点的值。含义取决于节点类型。 |
| n.parentNode | 对父节点的引用。 |
| n.prefix | 出现在冒号之前的标签名部分。例如，元素 `'<foo:bar ...>'` 的前缀将是 `'foo'`。 |
| n.previousSibling | 在树中位于 `n` 之前且具有相同父节点的节点。 |

除了这些属性外，所有节点都具有以下方法。通常，这些方法用于操作树结构。

```
n.appendChild(child)
```

向 `n` 添加一个新的子节点 `child`。新子节点将添加在所有现有子节点的末尾。

```
n.cloneNode(deep)
```

创建节点 `n` 的副本。如果 `deep` 为 `True`，则所有子节点也会被克隆。

```
n.hasAttributes()
```

如果节点有任何属性，则返回 `True`。

```
n.hasChildNodes()
```

如果节点有任何子节点，则返回 `True`。

```
n.insertBefore(newchild, ichild)
```

在另一个子节点 `ichild` 之前插入一个新子节点 `newchild`。`ichild` 必须已经是 `n` 的子节点。

```
n.isSameNode(other)
```

如果节点 `other` 指向与 `n` 相同的 DOM 节点，则返回 `True`。

```
n.normalize()
```

将相邻的文本节点合并为一个文本节点。

```
n.removeChild(child)
```

从 `n` 中移除子节点 `child`。

```
n.replaceChild(newchild, oldchild)
```

用 `newchild` 替换子节点 `oldchild`。`oldchild` 必须已经是 `n` 的子节点。

尽管树中可能出现许多不同类型的节点，但最常见的是处理 `Document`、`Element` 和 `Text` 节点。接下来将简要描述每一种。

######## 文档节点

一个 `Document` 节点 `d` 位于整个文档树的顶部，代表整个文档。它具有以下方法和属性：

```
d.documentElement
```

包含整个文档的根元素。

```
d.getElementsByTagName(tagname)
```

搜索所有子节点，并返回具有给定标签名 `tagname` 的元素列表。

```
d.getElementsByTagNameNS(namespaceuri, localname)
```

搜索所有子节点，并返回具有给定命名空间 URI 和本地名称的元素列表。返回的列表是 `NodeList` 类型的对象。

######## 元素节点

元素节点 `e` 代表单个 XML 元素，例如 `<foo>...</foo>`。要从元素中获取文本，你需要查找作为子节点的文本节点。以下属性和方法用于获取其他信息：

**e.tagName**

元素的标签名。例如，如果元素由 `<foo ...>` 定义，则标签名为 `'foo'`。

**e.getElementsByTagName(tagname)**

返回所有具有给定标签名的子元素的列表。

**e.getElementsByTagNameNS(namespaceuri, localname)**

返回命名空间中所有具有给定标签名的子元素的列表。`namespaceuri` 和 `localname` 是指定命名空间和标签名的字符串。如果使用类似 `<foo xmlns:foo="http://www.spam.com/foo">` 的声明声明了命名空间，则 `namespaceuri` 设置为 `'http://www.spam.com/foo'`。如果搜索后续元素 `<foo:bar>`，则 `localname` 设置为 `'bar'`。返回的对象是 `NodeList` 类型。

**e.hasAttribute(name)**

如果元素具有名为 `name` 的属性，则返回 `True`。

**e.hasAttributeNS(namespaceuri, localname)**

如果元素具有由 `namespaceuri` 和 `localname` 指定的属性，则返回 `True`。参数与 `getElementsByTagNameNS()` 中描述的含义相同。

**e.getAttribute(name)**

返回属性 `name` 的值。返回值是一个字符串。如果属性不存在，则返回空字符串。

**e.getAttributeNS(namespaceuri, localname)**

返回由 `namespaceuri` 和 `localname` 指定的属性的值。返回值是一个字符串。如果属性不存在，则返回空字符串。参数与 `getElementsByTagNameNS()` 中描述的相同。

######## 文本节点

文本节点用于表示文本数据。文本数据存储在 `Text` 对象 `t` 的 `t.data` 属性中。与给定文档元素关联的文本始终存储在作为该元素子节点的文本节点中。

##### 实用函数

节点上定义了以下实用方法。这些不属于 DOM 标准的一部分，但由 Python 提供，用于一般便利和调试。

**n.toprettyxml([indent [, newl]])**

创建一个格式良好的字符串，包含由节点 `n` 及其子节点表示的 XML。`indent` 指定缩进字符串，默认为制表符（`'\t'`）。`newl` 指定换行符，默认为 `'\n'`。

```
n.toxml([encoding])
```

创建一个字符串，包含由节点 `n` 及其子节点表示的 XML。`encoding` 指定编码（例如，`'utf-8'`）。如果未指定编码，则输出文本中不指定编码。

```
n.writexml(writer [, indent [, addindent [, newl]]])
```

将 XML 写入 `writer`。`writer` 可以是任何提供与文件接口兼容的 `write()` 方法的对象。`indent` 指定 `n` 的缩进。它是输出中节点 `n` 开头处的字符串。`addindent` 是一个字符串，指定应用于 `n` 的子节点的增量缩进。`newl` 指定换行符。

####### DOM 示例

以下示例展示了如何使用 `xml.dom.minidom` 模块解析 XML 文件并从中提取信息：

```
from xml.dom import minidom
doc = minidom.parse("recipe.xml")

ingredients  = doc.getElementsByTagName("ingredients")[0]
items        = ingredients.getElementsByTagName("item")

for item in items:
    num      = item.getAttribute("num")
    units    = item.getAttribute("units")
    text     = item.firstChild.data.strip()
    quantity = "%s %s" % (num,units)
    print("%-10s %s" % (quantity,text))
```

###### 注意

`xml.dom.minidom` 模块具有更多功能，用于更改解析树和处理不同类型的 XML 节点类型。更多信息可以在在线文档中找到。

###### xml.etree.ElementTree

`xml.etree.ElementTree` 模块定义了一个灵活的容器对象 `ElementTree`，用于存储和操作分层数据。尽管此对象通常与 XML 处理一起使用，但它实际上非常通用——其作用介于列表和字典之间。

####### ElementTree 对象

以下类用于定义新的 `ElementTree` 对象，并表示层次结构的顶层。

```
ElementTree([element [, file]])
```

创建一个新的 `ElementTree` 对象。`element` 是一个表示树根节点的实例。此实例支持下面描述的元素接口。`file` 是一个文件名或一个文件类对象，从中读取 XML 数据以填充树。



ElementTree 的实例树具有以下方法：

```
tree._setroot(element)
```

将根元素设置为 element。

```
tree.find(path)
```

在树中查找并返回第一个类型与给定路径匹配的顶级元素。path 是一个描述元素类型及其相对于其他元素位置的字符串。以下列表描述了路径语法：

| 路径 | 描述 |
|---|---|
| 'tag' | 仅匹配具有给定标签的顶级元素——例如 `<tag>...</tag>`。不匹配在较低级别定义的元素。嵌入在另一个元素中的类型为 tag 的元素，例如 `<foo><tag>...</tag></foo>`，不会被匹配。 |
| 'parent/tag' | 如果一个标签为 'tag' 的元素是标签为 'parent' 的元素的子元素，则匹配该元素。可以根据需要指定任意数量的路径名组件。 |
| '*' | 选择所有子元素。例如，'*/tag' 将匹配所有标签名为 'tag' 的孙元素。 |
| '.' | 从当前节点开始搜索。 |
| '//' | 选择一个元素下方所有级别的所有子元素。例如，'.//tag' 匹配所有子级别中标签为 'tag' 的元素。 |

如果你正在处理涉及 XML 命名空间的文档，路径中的标签字符串应采用 `{uri}tag` 的形式，其中 uri 是一个字符串，例如 `'http://www.w3.org/TR/html4/'`。

```
tree.findall(path)
```

在树中查找所有与给定路径匹配的顶级元素，并按照文档顺序将它们作为列表或迭代器返回。

```
tree.findtext(path [, default])
```

返回树中第一个与给定路径匹配的顶级元素的文本。default 是一个字符串，如果找不到匹配元素则返回该字符串。

```
tree.getiterator([tag])
```

创建一个迭代器，按节序生成树中所有标签与 tag 匹配的元素。如果省略 tag，则按顺序返回树中的每个元素。

```
tree.getroot()
```

返回树的根元素。

```
tree.parse(source [, parser])
```

解析外部 XML 数据并用结果替换根元素。source 可以是表示 XML 数据的文件名或类文件对象。parser 是一个可选的 TreeBuilder 实例，稍后描述。

```
tree.write(file [, encoding])
```

将树的全部内容写入文件。file 可以是文件名或为写入而打开的类文件对象。encoding 是要使用的输出编码，如果未指定，则默认为解释器的默认编码（在大多数情况下为 `'utf-8'` 或 `'ascii'`）。

####### 创建元素

ElementTree 中包含的元素类型由不同类型的实例表示，这些实例要么通过解析文件内部创建，要么通过以下构造函数创建：

```
Comment([text])
```

创建一个新的注释元素。text 是一个包含元素文本的字符串或字节串。解析或写入输出时，此元素映射到 XML 注释。

```
Element(tag [, attrib [, **extra]])
```

创建一个新元素。tag 是元素的名称。例如，如果你要创建一个元素 `<foo>...</foo>`，则 tag 应为 `'foo'`。attrib 是一个字典，其中的元素属性以字符串或字节串指定。extra 中提供的任何额外关键字参数也用于设置元素属性。

```
fromstring(text)
```

从 text 中的 XML 文本片段创建一个元素——与接下来描述的 XML() 相同。

```
ProcessingInstruction(target [, text])
```

创建一个对应于处理指令的新元素。target 和 text 都是字符串或字节串。映射到 XML 时，此元素对应于 `<?target text?>`。

```
SubElement(parent, tag [, attrib [, **extra]])
```

与 Element() 相同，但它会自动将新元素作为 parent 中元素的子元素添加。

```
XML(text)
```

通过解析 text 中的 XML 代码片段创建一个元素。例如，如果你将 text 设置为 `<foo>...</foo>`，这将创建一个标签为 `'foo'` 的标准元素。

```
XMLID(text)
```

与 XML(text) 相同，但 'id' 属性会被收集并用于构建一个将 ID 值映射到元素的字典。返回一个元组 `(elem, idmap)`，其中 elem 是新元素，idmap 是 ID 映射字典。例如，`XMLID('<foo id="123"><bar id="456">Hello</bar></foo>')` 返回 `(<Element foo>, {'123': <Element foo>, '456': <Element bar>})`。

####### 元素接口

虽然 `ElementTree` 中存储的元素可能具有不同的类型，但它们都支持一个通用接口。如果 `elem` 是任何元素，则定义了以下 Python 运算符：

| 运算符 | 描述 |
|----------|-------------|
| `elem[n]` | 返回 `elem` 的第 *n* 个子元素。 |
| `elem[n] = newelem` | 将 `elem` 的第 *n* 个子元素更改为不同的元素 `newelem`。 |
| `del elem[n]` | 删除 `elem` 的第 *n* 个子元素。 |
| `len(elem)` | `elem` 的子元素数量。 |

所有元素都具有以下基本数据属性：

| 属性 | 描述 |
|-----------|-------------|
| `elem.tag` | 标识元素类型的字符串。例如，`<foo>...</foo>` 的标签为 `'foo'`。 |
| `elem.text` | 与元素关联的数据。通常是包含 XML 元素起始标签和结束标签之间文本的字符串。 |
| `elem.tail` | 与属性一起存储的附加数据。对于 XML，这通常是包含在元素结束标签之后、下一个标签开始之前找到的空白的字符串。 |
| `elem.attrib` | 包含元素属性的字典。 |

元素支持以下方法，其中一些模拟了字典上的方法：

```
elem.append(subelement)
```

将元素 `subelement` 添加到子元素列表的末尾。

```
elem.clear()
```

清除元素中的所有数据，包括属性、文本和子元素。

```
elem.find(path)
```

查找第一个类型与 `path` 匹配的子元素。

```
elem.findall(path)
```

查找所有类型与 `path` 匹配的子元素。返回一个列表或可迭代对象，其中包含按文档顺序排列的匹配元素。

```
elem.findtext(path [, default])
```

查找第一个类型与 `path` 匹配的元素的文本。`default` 是一个字符串，如果未找到匹配项，则返回该字符串。

```
elem.get(key [, default])
```

获取属性 `key` 的值。`default` 是一个默认值，如果属性不存在则返回该值。如果涉及 XML 命名空间，则 `key` 将是一个形式为 `'{uri}key'` 的字符串，其中 `uri` 是一个字符串，例如 `'http://www.w3.org/TR/html4/'`。

```
elem.getchildren()
```

按文档顺序返回所有子元素。

```
elem.getiterator([tag])
```

返回一个迭代器，该迭代器生成所有类型与 tag 匹配的子元素。

```
elem.insert(index, subelement)
```

在子元素列表的 index 位置插入一个子元素。

```
elem.items()
```

以 `(name, value)` 对的列表形式返回所有元素属性。

```
elem.keys()
```

返回所有属性名称的列表。

```
elem.remove(subelement)
```

从子元素列表中移除元素 subelement。

```
elem.set(key, value)
```

将属性 key 设置为值 value。

####### 树构建

从其他树状结构轻松创建 ElementTree 对象。以下对象用于此目的。

```
TreeBuilder([element_factory])
```

一个类，用于使用一系列 start()、end() 和 data() 调用构建 ElementTree 结构，就像在解析文件或遍历另一个树状结构时会触发的那样。element_factory 是一个操作函数，用于创建新的元素实例。

TreeBuilder 的实例 t 具有以下方法：

```
t.close()
```

关闭树构建器并返回已创建的顶级 ElementTree 对象。

```
t.data(data)
```

向当前正在处理的元素添加文本数据。

```
t.end(tag)
```

关闭当前正在处理的元素并返回最终的元素对象。

```
t.start(tag, attrs)
```

创建一个新元素。tag 是元素名称，attrs 是一个包含属性值的字典。



##### 实用函数

以下定义了实用函数：

**dump(elem)**  
将 `elem` 的元素结构转储到 `sys.stdout` 以供调试。输出通常是XML格式。

**iselement(elem)**  
检查 `elem` 是否为有效的元素对象。

**iterparse(source [, events])**  
增量解析来自 *source* 的XML。*source* 是一个文件名或引用XML数据的类文件对象。*events* 是要产生的事件类型列表。可能的事件类型包括 `'start'`、`'end'`、`'start-ns'` 和 `'end-ns'`。如果省略，则只产生 `'end'` 事件。此函数返回的值是一个迭代器，产生元组 `(event, elem)`，其中 *event* 是一个字符串，如 `'start'` 或 `'end'`，`elem` 是正在处理的元素。对于 `'start'` 事件，元素是新创建的，初始时除属性外为空。对于 `'end'` 事件，元素已完全填充，包含所有子元素。

**parse(source)**  
将XML源完全解析为一个 `ElementTree` 对象。*source* 是一个文件名或包含XML数据的类文件对象。

**tostring(elem)**  
创建表示 *elem* 及其所有子元素的XML字符串。

###### XML示例

这是一个使用 `ElementTree` 解析示例食谱文件并打印配料列表的示例。它与DOM中显示的示例类似。

```python
from xml.etree.ElementTree import ElementTree

doc = ElementTree(file="recipe.xml")
ingredients = doc.find('ingredients')

for item in ingredients.findall('item'):
    num   = item.get('num')
    units = item.get('units','')
    text  = item.text.strip()
    quantity = "%s %s" % (num, units)
    print("%-10s %s" % (quantity, text))
```

`ElementTree` 的路径语法使得简化某些任务和在必要时使用快捷方式变得更容易。例如，以下是使用路径语法简单提取所有 `<item>...</item>` 元素的前一个代码的不同版本。

```python
from xml.etree.ElementTree import ElementTree

doc = ElementTree(file="recipe.xml")
for item in doc.findall(".//item"):
    num   = item.get('num')
    units = item.get('units','')
    text  = item.text.strip()
    quantity = "%s %s" % (num, units)
    print("%-10s %s" % (quantity, text))
```

考虑一个使用命名空间的XML文件 `'recipens.xml'`：

```xml
<?xml version="1.0" encoding="iso-8859-1"?>
<recipe xmlns:r="http://www.dabeaz.com/namespaces/recipe">
    <r:title>
    Famous Guacamole
    </r:title>
    <r:description>
    A southwest favorite!
    </r:description>
    <r:ingredients>
        <r:item num="4"> Large avocados, chopped </r:item>
        ...
    </r:ingredients>
    <r:directions>
    Combine all ingredients and hand whisk to desired consistency.
    Serve and enjoy with ice-cold beers.
    </r:directions>
</recipe>
```

要处理命名空间，通常最简单的方法是使用一个将命名空间前缀映射到相关命名空间URI的字典。然后你使用字符串格式化运算符来填充URI，如下所示：

```python
from xml.etree.ElementTree import ElementTree
doc = ElementTree(file="recipens.xml")
ns = {
    'r' : 'http://www.dabeaz.com/namespaces/recipe'
}
ingredients = doc.find('{%(r)s}ingredients' % ns)
for item in ingredients.findall('{%(r)s}item' % ns):
    num    = item.get('num')
    units = item.get('units','')
    text  = item.text.strip()
    quantity = "%s %s" % (num, units)
    print("%-10s %s" % (quantity, text))
```

对于小型XML文件，使用 `ElementTree` 模块快速将它们加载到内存中以便处理是很好的。然而，假设你正在处理一个具有如下结构的巨大XML文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<music>
    <album>
        <title>A Texas Funeral</title>
        <artist>Jon Wayne</artist>
        ...
    </album>
    <album>
        <title>Metaphysical Graffiti</title>
        <artist>The Dead Milkmen</artist>
        ...
    </album>
    ... continues for 100000 more albums ...
</music>
```

将大型XML文件读入内存往往会消耗大量内存。例如，读取一个10MB的XML文件可能导致内存中的数据结构超过100MB。如果你试图从此类文件中提取信息，最简单的方法是使用 `ElementTree.iterparse()` 函数。这是一个在前一个文件中迭代处理 `<album>` 节点的示例：

```python
from xml.etree.ElementTree import iterparse

iparse = iterparse("music.xml", ['start','end'])
# Find the top-level music element
for event, elem in iparse:
    if event == 'start' and elem.tag == 'music':
        musicNode = elem
        break

# Get all albums
albums = (elem for event, elem in iparse
            if event == 'end' and elem.tag == 'album')

for album in albums:
    # Do some kind of processing
    ...
    musicNode.remove(album)           # Throw away the album when done
```

有效使用 `iterparse()` 的关键在于丢弃不再使用的数据。最后一条语句 `musicNode.remove(album)` 在我们处理完每个 `<album>` 元素后将其丢弃（通过将其从父元素中移除）。如果你监控前一个程序的内存占用，你会发现即使输入文件非常大，内存占用也保持较低。

###### 备注

-   `ElementTree` 模块是目前在Python中处理简单XML文档最简单、最灵活的方式。然而，它并没有提供很多花哨的功能。例如，它不支持验证，也没有提供任何明显的方法来处理XML文档的复杂方面，如DTD。对于这些，你需要安装第三方包。其中一个这样的包，`lxml.etree`（位于 http://codespeak.net/lxml/），为流行的libxml2和libxslt库提供了ElementTree API，并完全支持XPATH、XSLT和其他特性。

-   `ElementTree` 模块本身是一个由Fredrik Lundh在 http://effbot.org/zone/element-index.htm 维护的第三方包。在这个网站上，你可以找到比标准库中包含的版本更现代，并提供额外功能的版本。

###### xml.sax

`xml.sax` 模块提供了使用SAX2 API解析XML文档的支持。

```
parse(file, handler [, error_handler])
```

解析XML文档，*file*。*file* 是文件名或打开的文件对象。*handler* 是一个内容处理器对象。*error_handler* 是一个可选的SAX错误处理器对象，其进一步说明见在线文档。

```
parseString(string, handler [, error_handler])
```

与 `parse()` 相同，但解析包含在字符串中的XML数据。

####### 处理器对象

要执行任何处理，你必须向 `parse()` 或 `parseString()` 函数提供一个内容处理器对象。要定义处理器，你需要定义一个继承自ContentHandler的类。ContentHandler的实例 `c` 具有以下方法，所有这些方法都可以根据需要在你的处理器类中被覆盖：

**c.characters(content)**

由解析器调用以提供原始字符数据。content是一个包含字符的字符串。

**c.endDocument()**

当文档结束时由解析器调用。

**c.endElement(name)**

当元素 `name` 的结束被到达时调用。例如，如果解析了 `'</foo>'`，则调用此方法时 `name` 设置为 `'foo'`。

**c.endElementNS(name, qname)**

当涉及XML命名空间的元素结束时调用。*name* 是一个字符串元组 `(uri, localname)`，*qname* 是完全限定名。通常 *qname* 是 `None`，除非启用了SAX命名空间前缀功能。例如，如果元素定义为 `'<foo:bar xmlns:foo="http://spam.com">'`，则 *name* 元组为 `(u'http://spam.com', u'bar')`。

**c.endPrefixMapping(prefix)**

当XML命名空间结束时调用。*prefix* 是命名空间的名称。

**c.ignorableWhitespace(whitespace)**

当文档中遇到可忽略的空白时调用。*whitespace* 是一个包含空白字符的字符串。

**c.processingInstruction(target, data)**

当遇到包含在 `<? ... ?>` 中的XML处理指令时调用。*target* 是指令的类型，*data* 是指令数据。例如，如果指令是 `'<?xml-stylesheet href="mystyle.css" type="text/css"?>`，则 *target* 设置为 `'xml-stylesheet'`，*data* 是指令文本的剩余部分 `'href="mystyle.css" type="text/css"'`。

**c.setDocumentLocator(locator)**

由解析器调用以提供一个定位器对象，该对象可用于跟踪行号、列号和其他信息。此方法的主要目的只是将定位器存储在某个地方，以便你以后可以使用它——例如，如果你需要打印错误消息。在 *locator* 中提供的定位器对象提供四个方法——`getColumnNumber()`、`getLineNumber()`、`getPublicId()` 和 `getSystemId()`——可用于获取位置信息。

**c.skippedEntity(name)**

每当解析器跳过一个实体时调用。*name* 是被跳过的实体的名称。



######## c.startDocument()

在文档开始时调用。

######## c.startElement(name, attrs)

每当遇到新的 XML 元素时调用。`name` 是元素的名称，`attrs` 是一个包含属性信息的对象。例如，如果 XML 元素是 '<foo bar="whatever" spam="yes">'，那么 `name` 被设置为 'foo'，`attrs` 包含关于 `bar` 和 `spam` 属性的信息。`attrs` 对象提供了多种获取属性信息的方法：

| 方法 | 描述 |
| --- | --- |
| attrs.getLength() | 返回属性的数量 |
| attrs.getNames() | 返回属性名称列表 |
| attrs.getType(name) | 获取属性 `name` 的类型 |
| attrs.getValue(name) | 获取属性 `name` 的值 |

######## c.startElementNS(name, qname, attrs)

当遇到新的 XML 元素且正在使用 XML 命名空间时调用。`name` 是一个元组 `(uri, localname)`，`qname` 是完全限定的元素名称（除非启用了 SAX2 命名空间前缀特性，否则通常设置为 None）。`attrs` 是一个包含属性信息的对象。例如，如果 XML 元素是 '<foo:bar xmlns:foo="http://spam.com" blah="whatever">'，那么 `name` 是 `(u'http://spam.com', u'bar')`，`qname` 是 None，`attrs` 包含关于属性 `blah` 的信息。`attrs` 对象与前面 `startElement()` 方法中显示的访问属性时使用的方法相同。此外，还添加了以下额外方法来处理命名空间：

| 方法 | 描述 |
| --- | --- |
| attrs.getValueByQName(qname) | 返回限定名的值。 |
| attrs.getNameByQName(qname) | 返回指定名称的 `(命名空间, 本地名)` 元组。 |
| attrs.getQNameByName(name) | 返回指定为元组 `(命名空间, 本地名)` 的名称的限定名。 |
| attrs.getQNames() | 返回所有属性的限定名。 |

######## c.startPrefixMapping(prefix, uri)

在 XML 命名空间声明开始时调用。例如，如果一个元素定义为 '<foo:bar xmlns:foo="http://spam.com">'，那么 `prefix` 被设置为 'foo'，`uri` 被设置为 'http://spam.com'。

##### 示例

以下示例演示了一个基于 SAX 的解析器，通过打印出前面显示的配方文件中的配料清单。这应与 `xml.dom.minidom` 部分中的示例进行比较。

```python
from xml.sax import ContentHandler, parse

class RecipeHandler(ContentHandler):
    def startDocument(self):
        self.initem = False
    def startElement(self,name,attrs):
        if name == 'item':
            self.num   = attrs.get('num','1')
            self.units = attrs.get('units','none')
            self.text = []
            self.initem = True
    def endElement(self,name):
        if name == 'item':
            text = "".join(self.text)
            if self.units == 'none': self.units = ""
            unitstr = "%s %s" % (self.num, self.units)
            print("%-10s %s" % (unitstr,text.strip()))
            self.initem = False
    def characters(self,data):
        if self.initem:
            self.text.append(data)

parse("recipe.xml",RecipeHandler())
```

###### 注意

`xml.sax` 模块具有更多功能，可用于处理不同类型的 XML 数据和创建自定义解析器。例如，可以定义处理程序对象来解析 DTD 数据和文档的其他部分。更多信息可以在在线文档中找到。

###### xml.sax.saxutils

`xml.sax.saxutils` 模块定义了一些实用函数和对象，这些函数和对象通常与 SAX 解析器一起使用，但在其他地方通常也很有用。

```python
escape(data [, entities])
```

给定一个字符串 `data`，此函数将某些字符替换为转义序列。例如，'<' 被替换为 '&lt;'。`entities` 是一个可选的字典，将字符映射到转义序列。例如，将 `entities` 设置为 `{ u'\xf1' : '&ntilde;' }` 会将出现的 ñ 替换为 '&ntilde;'。

```python
unescape(data [, entities])
```

反转义出现在 `data` 中的特殊转义序列。例如，'&lt;' 被替换为 '<'。`entities` 是一个可选的字典，将实体映射到反转义的字符值。`entities` 是与 `escape()` 函数一起使用的字典的逆——例如，`{ '&ntilde;' : u'\xf1' }`。

```python
quoteattr(data [, entities])
```

转义字符串 `data`，但执行额外的处理以使结果值可以用作 XML 属性值。返回值可以直接作为属性值打印——例如，`print "<element attr=%s>" % quoteattr(somevalue)`。`entities` 是一个与 `escape()` 函数兼容的字典。

```python
XMLGenerator([out [, encoding]])
```

一个 `ContentHandler` 对象，它只是将解析的 XML 数据作为 XML 文档回显到输出流。这可以重新创建原始 XML 文档。`out` 是输出文档，默认为 `sys.stdout`。`encoding` 是要使用的字符编码，默认为 `'iso-8859-1'`。如果你正在调试解析代码并使用一个已知可以工作的处理程序，这会很有用。

##### 其他库模块

本节列出的模块未在本书中详细介绍，但仍被视为标准库的一部分。这些模块在前面的章节中大多被省略了，因为它们要么极其底层且用途有限，要么仅限于非常特定的平台，要么已过时，要么太复杂以至于介绍它们需要一本完整的书。尽管这些模块在本书中被省略了，但每个模块的在线文档可以在 http://docs.python.org/library/modname 找到。所有模块的索引也可以在 http://docs.python.org/library/modindex.html 找到。

此处列出的模块代表了 Python 2 和 Python 3 之间的公共功能子集。如果你使用的模块未在此处列出，那么它很可能已被正式弃用。某些模块在 Python 3 中更改了名称。如果适用，新名称显示在括号中。

###### Python 服务

以下模块提供与 Python 语言和 Python 解释器执行相关的额外服务。其中许多模块与 Python 源代码的解析和编译有关。

| 模块 | 描述 |
| --- | --- |
| bdb | 访问调试器框架 |
| code | 解释器基类 |
| codeop | 编译 Python 代码 |
| compileall | 对目录中的 Python 文件进行字节编译 |
| copy_reg (copyreg) | 注册内置类型以供 pickle 模块使用 |
| dis | 反汇编器 |
| distutils | Python 模块的分发 |
| fpectl | 浮点异常控制 |
| imp | 提供对 import 语句实现的访问 |
| keyword | 测试字符串是否为 Python 关键字 |
| linecache | 从源文件中检索行 |
| modulefinder | 查找脚本使用的模块 |
| parser | 访问 Python 源代码的解析树 |
| pickletools | pickle 开发者的工具 |
| pkgutil | 包扩展工具 |
| pprint | 对象的美观打印 |
| pyclbr | 为类浏览器提取信息 |
| py_compile | 将 Python 源代码编译为字节码文件 |
| repr (reprlib) | `repr()` 函数的替代实现 |
| symbol | 用于表示解析树内部节点的常量 |
| tabnanny | 检测模糊的缩进 |
| test | 回归测试包 |
| token | 解析树的终端节点 |
| tokenize | Python 源代码的扫描器 |
| user | 用户配置文件解析 |
| zipimport | 从 zip 归档文件导入模块 |

###### 字符串处理

以下模块是一些用于字符串处理的较旧的、现已过时的模块。

| 模块 | 描述 |
| --- | --- |
| difflib | 计算字符串之间的差异 |
| fpformat | 浮点数格式化 |
| stringprep | 互联网字符串准备 |
| textwrap | 文本换行 |

###### 操作系统模块

这些模块提供额外的操作系统服务。在某些情况下，此处列出的模块的功能已整合到第 19 章“操作系统服务”中涵盖的其他模块的功能中。

| 模块 | 描述 |
| --- | --- |
| crypt | 访问 UNIX crypt 函数 |
| curses | Curses 库接口 |
| grp | 访问组数据库 |
| pty | 伪终端处理 |
| pipes | 与 shell 管道的接口 |
| nis | 与 Sun 的 NIS 的接口 |
| platform | 访问平台特定信息 |
| pwd | 访问密码数据库 |
| readline | 访问 GNU readline 库 |
| rlcompleter | GNU readline 的补全函数 |

| 模块 | 描述 |
|--------|-------------|
| resource | 资源使用信息 |
| sched | 事件调度器 |
| spwd | 访问影子密码数据库 |
| stat | 支持解释 os.stat() 的结果 |
| syslog | UNIX syslog 守护进程接口 |
| termios | UNIX TTY 控制 |
| tty | 终端控制函数 |

###### 网络

以下模块提供对较少使用的网络协议的支持：

| 模块 | 描述 |
|--------|-------------|
| imaplib | IMAP 协议 |
| nntplib | NNTP 协议 |
| poplib | POP3 协议 |
| smtpd | SMTP 服务器 |
| telnetlib | Telnet 协议 |

###### 互联网数据处理

以下模块提供第 24 章"互联网数据处理与编码"中未涵盖的互联网数据处理的额外支持。

| 模块 | 描述 |
|--------|-------------|
| binhex | BinHex4 文件格式支持 |
| formatter | 通用输出格式化 |
| mailcap | Mailcap 文件处理 |
| mailbox | 读取各种邮箱格式 |
| netrc | Netrc 文件处理 |
| plistlib | Macintosh plist 文件处理 |
| uu | UUencode 文件支持 |
| xdrlib | 编码和解码 Sun XDR 数据 |

###### 国际化

以下模块用于编写国际化应用程序：

| 模块 | 描述 |
|--------|-------------|
| gettext | 多语言文本处理服务 |
| locale | 系统提供的国际化函数 |

###### 多媒体服务

以下模块提供对处理各种多媒体文件的支持：

| 模块 | 描述 |
|--------|-------------|
| audioop | 操作原始音频数据 |
| aifc | 读取和写入 AIFF 和 AIFC 文件 |
| sunau | 读取和写入 Sun AU 文件 |
| wave | 读取和写入 WAV 文件 |
| chunk | 读取首块数据 |
| colorsys | 颜色系统之间的转换 |
| imghdr | 确定图像的类型 |
| sndhdr | 确定声音文件的类型 |
| ossaudiodev | 访问 OSS 兼容的音频设备 |

###### 杂项

以下模块完善了列表，但并未真正归入其他任何类别：

| 模块 | 描述 |
|--------|-------------|
| cmd | 面向行的命令解释器 |
| calendar | 日历生成函数 |
| shlex | 简单词法分析模块 |
| sched | 事件调度器 |
| Tkinter (tkinter) | Python 的 Tcl/Tk 接口 |
| winsound | 在 Windows 上播放声音 |

#### 扩展和嵌入 Python

- 26. 扩展和嵌入 Python
  - 附录：Python 3

#### 扩展和嵌入 Python

Python 最强大的特性之一是其与 C 编写的软件进行交互的能力。将 Python 与外部代码集成有两种常用策略。首先，外部函数可以打包成 Python 库模块，通过 `import` 语句使用。这类模块被称为*扩展模块*，因为它们通过非 Python 编写的功能扩展了解释器。这是目前为止最常见的 Python-C 集成形式，因为它使 Python 应用程序能够访问高性能编程库。另一种 Python-C 集成形式是*嵌入*。这是一种将 Python 程序和解释器作为库从 C 中访问的过程。后一种方法有时被程序员使用，他们出于某种原因——通常是作为某种脚本引擎——想要将 Python 解释器嵌入到现有的 C 应用程序框架中。

本章涵盖 Python-C 编程接口的基础知识。首先介绍用于构建扩展模块和嵌入 Python 解释器的 C API 的核心部分。本节并非教程，因此该主题的新读者应参阅 http://docs.python.org/extending 上的"嵌入和扩展 Python 解释器"文档，以及 http://docs.python.org/c-api 上的"Python/C API 参考手册"。接下来介绍 `ctypes` 库模块。这是一个非常有用的模块，允许你访问 C 库中的函数，而无需编写任何额外的 C 代码或使用 C 编译器。

需要注意的是，对于高级扩展和嵌入应用，大多数程序员倾向于使用高级代码生成器和编程库。例如，SWIG 项目 (http://www.swig.org) 是一个编译器，它通过解析 C 头文件的内容来创建 Python 扩展模块。有关此工具及其他扩展构建工具的参考资料可在 http://wiki.python.org/moin/IntegratingPythonWithOtherLanguages 找到。

#### 扩展模块

本节概述为 Python 创建手写 C 扩展模块的基本过程。创建扩展模块时，你实际上是在构建 Python 与用 C 编写的现有功能之间的接口。对于 C 库，你通常从一个头文件开始，如下所示：

```c
/* file : example.h */
#include <stdio.h>
#include <string.h>
#include <math.h>

typedef struct Point {
  double x;
  double y;
} Point;

/* Compute the GCD of two integers x and y */
extern int    gcd(int x, int y);

/* Replace och with nch in s and return the number of replacements */
extern int    replace(char *s, char och, char nch);

/* Compute the distance between two points */
extern double distance(Point *a, Point *b);

/* A preprocessor constant */
#define MAGIC 0x31337
```

这些函数原型在单独的文件中有某种实现。例如：

```c
/* example.c */
#include "example.h"
/* Compute GCD of two positive integers x and y */
int gcd(int x, int y) {
    int g;
    g = y;
    while (x > 0) {
        g = x;
        x = y % x;
        y = g;
    }
    return g;
}

/* Replace a character in a string */
int replace(char *s, char oldch, char newch) {
  int nrep = 0;
  while (s = strchr(s,oldch)) {
    *(s++) = newch;
    nrep++;
  }
  return nrep;
}

/* Distance between two points */
double distance(Point *a, Point *b) {
  double dx,dy;
  dx = a->x - b->x;
  dy = a->y - b->y;
  return sqrt(dx*dx + dy*dy);
}
```

以下是一个 C main() 程序，演示了这些函数的使用：

```c
/* main.c */
#include "example.h"
int main() {
  /* Test the gcd() function */
  {
    printf("%d\n", gcd(128,72));
    printf("%d\n", gcd(37,42));
  }
  /* Test the replace() function */
  {
    char s[] = "Skipping along unaware of the unspeakable peril.";
    int  nrep;
    nrep = replace(s,' ','-');
    printf("%d\n", nrep);
    printf("%s\n",s);
  }
  /* Test the distance() function */
  {
    Point a = { 10.0, 15.0 };
    Point b = { 13.0, 11.0 };
    printf("%0.2f\n", distance(&a,&b));
  }
}
```

上述程序的输出如下：

```
% a.out
8
1
6
Skipping-along-unaware-of-the-unspeakable-peril.
5.00
```

#### 扩展模块原型

扩展模块通过编写一个单独的 C 源文件来构建，该文件包含一组包装函数，这些函数提供 Python 解释器与底层 C 代码之间的粘合层。以下是一个名为 `_example` 的基本扩展模块示例：

```c
/* pyexample.c */

#include "Python.h"
#include "example.h"

static char py_gcd_doc[] = "Computes the GCD of two integers";
static PyObject *
py_gcd(PyObject *self, PyObject *args) {
  int x,y,r;
  if (!PyArg_ParseTuple(args,"ii:gcd",&x,&y)) {
     return NULL;
  }
  r = gcd(x,y);
  return Py_BuildValue("i",r);
}

static char py_replace_doc[] = "Replaces all characters in a string";
static PyObject *
py_replace(PyObject *self, PyObject *args, PyObject *kwargs) {
  static char *argnames[] = {"s","och","nch",NULL};
  char     *s,*sdup;
  char     och, nch;
  int      nrep;
  PyObject *result;
  if  (!PyArg_ParseTupleAndKeywords(args,kwargs, "scc:replace",
                                    argnames, &s, &och, &nch)) {
       return NULL;
  }
  sdup = (char *) malloc(strlen(s)+1);
  strcpy(sdup,s);
  nrep = replace(sdup,och,nch);
  result = Py_BuildValue("(is)",nrep,sdup);
  free(sdup);
  return result;
}

static char py_distance_doc[] = "Computes the distance between two points";
static PyObject *
py_distance(PyObject *self, PyObject *args) {
  PyErr_SetString(PyExc_NotImplementedError,"distance() not implemented.");
  return NULL;
}

static PyMethodDef _examplemethods[] = {
  {"gcd", py_gcd, METH_VARARGS, py_gcd_doc},
  {"replace", py_replace, METH_VARARGS | METH_KEYWORDS, py_replace_doc},
  {"distance",py_distance,METH_VARARGS, py_distance_doc},
  {NULL, NULL, 0, NULL}
};

#if PY_MAJOR_VERSION < 3
/* Python 2 module initialization */
void init_example(void) {
  PyObject *mod;
  mod = Py_InitModule("_example", _examplemethods);
  PyModule_AddIntMacro(mod,MAGIC);
}
#else
/* Python 3 module initialization */
static struct PyModuleDef _examplemodule = {
  PyModuleDef_HEAD_INIT,
  "_example",  /* name of module */
  NULL,        /* module documentation, may be NULL */
  -1,
  _examplemethods
};
PyMODINIT_FUNC
PyInit__example(void) {
  PyObject *mod;
  mod = PyModule_Create(&_examplemodule);
  PyModule_AddIntMacro(mod, MAGIC);
  return mod;
}
#endif
```

扩展模块始终需要包含 "Python.h"。对于要被访问的每个 C 函数，都需要编写一个包装函数。这些包装函数接受两个参数（self 和 args，均为 PyObject * 类型）或三个参数（self、args 和 kwargs，均为 PyObject * 类型）。

以及`kwargs`，所有类型均为`PyObject *`）。`self`参数用于包装函数实现应用于某个对象实例的内置方法的情况。此时，该实例被放置在`self`参数中。否则，`self`将被设置为`NULL`。`args`是一个包含解释器传递的函数参数的元组。`kwargs`是一个包含关键字参数的字典。

参数从Python转换为C是通过`PyArg_ParseTuple()`或`PyArg_ParseTupleAndKeywords()`函数完成的。类似地，`Py_BuildValue()`函数用于构造可接受的返回值。这些函数将在后续章节中描述。

扩展函数的文档字符串应放置在单独的字符串变量中，如`py_gcd_doc`和`py_replace_doc`所示。这些变量在模块初始化期间（稍后描述）被引用。

包装函数绝对不能（否则将面临严重后果）修改通过引用从解释器接收的数据。这就是为什么`py_replace()`包装器在将接收到的字符串传递给C函数（该函数会就地修改它）之前，先制作了一个副本。如果省略此步骤，包装器函数可能会违反Python字符串的不可变性。

如果你想引发异常，你可以使用`PyExc_SetString()`函数，如`py_distance()`包装器所示。返回`NULL`以表示发生了错误。

方法表`_examplemethods`用于将Python名称与C包装函数关联起来。这些是从解释器调用函数时使用的名称。`METH_VARARGS`标志指示包装器的调用约定。在这种情况下，仅接受元组形式的位置参数。它也可以设置为`METH_VARARGS | METH_KEYWORDS`以指示接受关键字参数的包装器函数。方法表还为每个包装器函数设置文档字符串。

扩展模块的最后部分执行初始化程序，该程序在Python 2和Python 3之间有所不同。在Python 2中，模块初始化函数`init_example`用于初始化模块的内容。在这种情况下，`Py_InitModule("_example", _examplemethods)`函数创建一个模块`_example`，并用对应于方法表中列出的函数的内置函数对象填充它。对于Python 3，你需要创建一个描述模块的`PyModuleDef`对象`_examplemodule`。然后你编写一个如图所示的函数`PyInit_example()`来初始化模块。模块初始化函数也是安装模块常量和其他部分（如果必要）的地方。例如，`PyModule_AddIntMacro()`将预处理器的值添加到模块中。

需要注意的是，命名对于模块初始化至关重要。如果你正在创建一个名为*modname*的模块，模块初始化函数在Python 2中必须命名为`initmodname()`，在Python 3中必须命名为`PyInit_modname()`。如果你不这样做，解释器将无法正确加载你的模块。

#### 命名扩展模块

标准做法是用前导下划线命名C扩展模块，例如`'_example'`。Python标准库本身也遵循这种惯例。例如，有名为`_socket`、`_thread`、`_sre`和`_fileio`的模块，分别对应于socket、threading、re和io模块的C编程组件。通常，你不会直接使用这些C扩展模块。相反，你创建一个高级Python模块，如下所示：

```python
####### example.py
from _example import *
# 在下面添加额外的支持代码
...
```

这个Python包装器的目的是为你的模块提供额外的支持代码或提供更高层次的接口。在许多情况下，在Python中实现扩展模块的部分功能比在C中更容易。这种设计使得这变得简单。如果你查看许多标准库模块，你会发现它们是以C和Python混合的方式实现的。

#### 编译和打包扩展

编译和打包扩展模块的首选机制是使用distutils。为此，你需要创建一个如下所示的setup.py文件：

```python
##### setup.py
from distutils.core import setup, Extension

setup(name="example",
      version="1.0",
      py_modules = ['example.py'],
      ext_modules = [
        Extension("_example",
                  ["pyexample.c","example.c"])
      ]
)
```

在此文件中，你需要包含高级Python文件（`example.py`）和组成扩展模块的源文件（`pyexample.c`、`example.c`）。要构建模块进行测试，请输入以下命令：

```bash
% python setup.py build_ext --inplace
```

这将把扩展代码编译成共享库，并将其留在当前工作目录中。该库的名称将是`_examplemodule.so`、`_examplemodule.pyd`或类似的变体。

如果编译成功，使用你的模块就很简单了。例如：

```python
% python3.0
Python 3.0 (r30:67503, Dec 4 2008, 09:40:15)
[GCC 4.0.1 (Apple Inc. build 5465)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import example
>>> example.gcd(78, 120)
6
>>> example.replace("Hello World", ' ', '-')
(1, 'Hello-World')
>>> example.distance()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NotImplementedError: distance() not implemented.
>>>
```

更复杂的扩展模块可能需要提供额外的构建信息，例如包含目录、库和预处理器宏。它们也可以包含在setup.py中，如下所示：

```python
##### setup.py
from distutils.core import setup, Extension

setup(name="example",
      version="1.0",
      py_modules = ['example.py'],
      ext_modules = [
        Extension("_example",
                  ["pyexample.c","example.c"],
                  include_dirs = ["/usr/include/X11","/opt/include"],
                  define_macros = [('DEBUG',1),
                                  ('MONDO_FLAG',1)],
                  undef_macros = ['HAVE_FOO','HAVE_NOT'],
                  library_dirs= ["/usr/lib/X11", "/opt/lib"],
                  libraries = [ "X11", "Xt", "blah" ])
      ]
)
```

如果你想为一般用途安装扩展模块，只需输入`python setup.py install`。有关此的更多细节，请参见第8章“模块、包和分发”。

在某些情况下，你可能想要手动构建扩展模块。这几乎总是需要关于各种编译器和链接器选项的高级知识。以下是在Linux上的一个示例：

```bash
linux % gcc -c -fpic -I/usr/local/include/python2.6 example.c pyexample.c
linux % gcc -shared example.o pyexample.o -o _examplemodule.so
```

#### 从Python到C的类型转换

扩展模块使用以下函数将从Python传递的参数转换为C。它们的原型通过包含`Python.h`头文件来定义。

```c
int PyArg_ParseTuple(PyObject *args, char *format, ...);
```

将`args`中的位置参数元组解析为一系列C变量。`format`是一个格式字符串，包含表26.1–26.3中的一个或多个说明符字符串，这些说明符描述了`args`的预期内容。所有剩余参数包含C变量的地址，结果将被放置在其中。这些参数的顺序和类型必须与`format`中使用的说明符匹配。如果参数无法解析，则返回零。

```c
int PyArg_ParseTupleAndKeywords(PyObject *args, PyObject *kwargs,
                                char *format, char **kwlist, ...);
```

解析包含在`kwargs`中的位置参数元组和关键字参数字典。`format`与`PyArg_ParseTuple()`的含义相同。唯一的区别是`kwlist`是一个以null结尾的字符串列表，包含所有参数的名称。成功时返回1，错误时返回0。

表26.1列出了用于转换数字并放置在`format`参数中的格式代码。C参数类型列列出了应传递给`PyArg_Parse*()`函数的C数据类型。对于数字，它始终是指向应存储结果的位置的指针。

| 格式代码 | C参数类型 | 描述 |
| :-- | :-- | :-- |
| %s | char ** | 解析一个字符指针。这是处理Python中字符串的最简单方法。一旦数据被解析，就可以将其视为普通的C字符串。 % |
| %i | int * | 解析一个有符号整数。 |
| %d | int * | 解析一个有符号十进制整数。这与%i相同。 |
| %u | unsigned int * | 解析一个无符号整数。 |
| %f | double * | 解析一个浮点数。 |
| %e | double * | 解析一个指数表示的浮点数。 |
| %E | double * | 解析一个带指数的指数表示浮点数。 |
| %O | PyObject ** | 解析一个指向任何对象的指针。 |
| %P | void * | 解析一个指向任何对象的指针。 |
| %l | long * | 解析一个长整数。 |
| %c | char * | 解析一个字符。 |
| %d | int * | 解析一个有符号十进制整数。 |
| %e | double * | 解析一个指数表示的浮点数。 |
| %o | unsigned long * | 解析一个八进制整数。 |
| %x | unsigned int * | 解析一个十六进制整数。 |
| %= | PyObject ** | 解析一个对象。这是处理Python中对象的最简单方法。一旦数据被解析，就可以将其视为普通的Python对象。 % |
| %{ | char * | 解析一个字符串。 |
| %% | const char ** | 解析一个格式字符串。 |



##### 表 26.1 数值转换及 `PyArg_Parse*` 相关的 C 数据类型

| 格式 | Python 类型 | C 参数类型 |
|--------|-------------|-----------------|
| "b" | 整数 | `signed char *r` |
| "B" | 整数 | `unsigned char *r` |
| "h" | 整数 | `short *r` |
| "H" | 整数 | `unsigned short *r` |
| "i" | 整数 | `int *r` |
| "I" | 整数 | `unsigned int *r` |
| "l" | 整数 | `long int *r` |
| "k" | 整数 | `unsigned long *r` |
| "L" | 整数 | `long long *r` |
| "K" | 整数 | `unsigned long long *r` |
| "n" | 整数 | `Py_ssize_t *r` |
| "f" | 浮点数 | `float *r` |
| "d" | 浮点数 | `double *r` |
| "D" | 复数 | `Py_complex *r` |

当转换有符号整数值时，如果 Python 整数过大而无法放入所请求的 C 数据类型中，则会引发 `OverflowError` 异常。但是，接受无符号值的转换（例如 `'I'`、`'H'`、`'K'` 等）不会检查溢出，如果值超出支持范围则会静默截断。对于浮点转换，可以传入 Python `int` 或 `float` 作为输入。在这种情况下，整数将被提升为浮点数。只要用户自定义类提供了适当的转换方法（如 `__int__()` 或 `__float__()`），它们就会被接受为数字。例如，实现了 `__int__()` 的用户自定义类将被接受为上述任何整数转换的输入（并且自动调用 `__int__()` 来执行转换）。

表 26.2 展示了适用于字符串和字节的转换。许多字符串转换会同时返回一个指针和长度。

##### 表 26.2 字符串转换及 `PyArg_Parse*` 相关的 C 数据类型

| 格式 | Python 类型 | C 参数类型 |
|--------|-------------|-----------------|
| "c" | 长度为 1 的字符串或字节串 | `char *r` |
| "s" | 字符串 | `char **r` |
| "s#" | 字符串、字节或缓冲区 | `char **r`, `int *len` |
| "s*" | 字符串、字节或缓冲区 | `Py_buffer *r` |
| "z" | 字符串或 None | `char **r` |
| "z#" | 字符串、字节或 None | `char **r`, `int *len` |
| "z*" | 字符串、字节、缓冲区或 None | `Py_buffer *r` |
| "y" | 字节（以空字符结尾） | `char **r` |
| "y#" | 字节 | `char **r`, `int *len` |
| "y*" | 字节或缓冲区 | `Py_buffer *r` |
| "u" | 字符串（Unicode） | `Py_UNICODE **r` |
| "u#" | 字符串（Unicode） | `Py_UNICODE **r`, `int *len` |
| "es" | 字符串 | `const char *enc`, `char **r` |
| "es#" | 字符串或字节 | `const char *enc, char **r, int *len` |
| "et" | 字符串或以空字符结尾的字节 | `const char *enc, char **r` |
| "et#" | 字符串或字节 | `const char *enc, char **r, int *len` |
| "t#" | 只读缓冲区 | `char **r, int *len` |
| "w" | 读写缓冲区 | `char **r` |
| "w#" | 读写缓冲区 | `char **r, int *len` |
| "w*" | 读写缓冲区 | `Py_buffer *r` |

字符串处理对 C 扩展来说是一个特殊问题，因为 `char *` 数据类型被用于许多不同的目的。例如，它可能指代文本、单个字符或原始二进制数据的缓冲区。还有一个问题是如何处理 C 用来标记文本字符串结尾的嵌入式 NULL 字符（`'\x00'`）。

在表 26.2 中，如果你传递的是文本，应该使用转换码 `"s"`、`"z"`、`"u"`、`"es"` 和 `"et"`。对于这些转换码，Python 假定输入文本不包含任何嵌入的 NULL 字符——如果包含，将引发 `TypeError` 异常。但是，可以安全地假定 C 中得到的字符串是以 NULL 结尾的。在 Python 2 中，可以传递 8 位字符串和 Unicode 字符串，但在 Python 3 中，除了 `"et"` 之外的所有转换都要求 Python `str` 类型，不能与 `bytes` 配合使用。当 Unicode 字符串传递给 C 时，它们总是使用解释器默认的 Unicode 编码（通常是 UTF-8）进行编码。唯一的例外是 `"u"` 转换码，它返回使用 Python 内部 Unicode 表示的字符串。这是一个 `Py_UNICODE` 值的数组，其中 Unicode 字符通常由 C 中的 `wchar_t` 类型表示。

`"es"` 和 `"et"` 转换码允许你为文本指定替代编码。你需要提供一个编码名称，如 `'utf-8'` 或 `'iso-8859-1'`，文本将被编码到缓冲区中并以该格式返回。`"et"` 与 `"es"` 的区别在于，如果给出了 Python 字节串，它将被视为已经编码过并直接传递，不做修改。需要注意的是，`"es"` 和 `"et"` 转换会为结果动态分配内存，需要用户显式调用 `PyMem_Free()` 来释放。因此，使用这些转换的代码应类似于：

```c
PyObject *py_wrapper(PyObject *self, PyObject *args) {
    char *buffer;
    if (!PyArg_ParseTuple(args,"es","utf-8",&buffer)) {
        return NULL;
    }
    /* Do something. */
    ...
    /* Cleanup and return the result */
    PyMem_Free(buffer);
    return result;
}
```

要处理文本或二进制数据，请使用 `"s#"`、`"z#"`、`"u#"`、`"es#"` 或 `"et#"` 转换码。这些转换的工作方式与之前完全相同，只是额外返回了长度。因此，对嵌入式 NULL 字符的限制被解除了。此外，这些转换增加了对字节串和任何其他支持所谓**缓冲区接口**的对象的支持。**缓冲区接口**是一种 Python 对象暴露其内容的原始二进制缓冲区的方式。通常你可以在字符串、字节和数组中找到它（例如 `array` 模块创建的数组就支持它）。在这种情况下，如果对象提供了可读的缓冲区接口，将返回指向缓冲区及其大小的指针。最后，如果向 `"es#"` 和 `"et#"` 转换提供了非 NULL 的指针和长度，则假定这些代表预分配的缓冲区，编码结果可以放入其中。在这种情况下，解释器不会为结果分配新内存，你也不必调用 `PyMem_Free()`。

`"s*"` 和 `"z*"` 转换码与 `"s#"` 和 `"z#"` 类似，但它们会填充一个 `Py_buffer` 结构体，其中包含关于所接收数据的信息。更多相关信息可以在 PEP-3118 中找到，但该结构体至少具有 `char *buf`、`int len` 和 `int itemsize` 属性，分别指向缓冲区、缓冲区长度（以字节为单位）和缓冲区中存储的元素大小。此外，解释器会对缓冲区加锁，防止其在被扩展代码持有时被其他线程修改。这允许扩展独立操作缓冲区内容，可能在与解释器不同的线程中进行。用户需要在所有处理完成后调用 `PyBuffer_Release()` 来释放缓冲区。

`"t#"`、`"w"`、`"w#"` 和 `"w*"` 转换码与 `"s"` 系列转换码类似，只是它们只接受实现了缓冲区接口的对象。`"t#"` 要求缓冲区可读。`"w"` 转换码要求缓冲区既可读又可写。支持可写缓冲区的 Python 对象假定为可变的。因此，C 扩展覆写或修改缓冲区内容是合法的。

`"y"`、`"y#"` 和 `"y*"` 转换码与 `"s"` 系列转换码类似，只是它们只接受字节串。使用这些来编写必须只接受字节而非 Unicode 字符串的函数。`"y"` 转换码只接受不包含嵌入式 NULL 字符的字节串。

表 26.3 列出了用于接受任意 Python 对象作为输入并将结果保留为 `PyObject *` 类型的转换码。这些有时用于需要处理比简单数字或字符串更复杂的 Python 对象的 C 扩展——例如，如果你需要一个 C 扩展函数接受 Python 类的实例或字典。

##### 表 26.3 Python 对象转换及 `PyArg_Parse*` 相关的 C 数据类型

| 格式 | Python 类型 | C 类型 |
|--------|-------------|--------|
| "O" | 任意 | `PyObject **r` |
| "O!" | 任意 | `PyTypeObject *type, PyObject **r` |
| "O&" | 任意 | `int (*converter)(PyObject *, void *), void *r` |
| "S" | 字符串 | `PyObject **r` |
| "U" | Unicode | `PyObject **r` |



#### 从 C 到 Python 的类型转换

"O"、"S" 和 "U" 说明符返回类型为 `PyObject *` 的原始 Python 对象。"S" 和 "U" 分别将此对象限制为字符串或 Unicode 字符串。

"O!" 转换需要两个 C 参数：一个指向 Python 类型对象的指针和一个 `PyObject *` 指针，用于接收该对象的指针。如果对象的类型与类型对象不匹配，将引发 TypeError。例如：

```
/* Parse a List Argument */
PyObject *listobj;
PyArg_ParseTuple(args,"O!", &PyList_Type, &listobj);
```

以下列表显示了与此转换配合使用的常见 Python 容器类型对应的 C 类型名称。

| C 名称 | Python 类型 |
|--------|-------------|
| `PyList_Type` | `list` |
| `PyDict_Type` | `dict` |
| `PySet_Type` | `set` |
| `PyFrozenSet_Type` | `frozen_set` |
| `PyTuple_Type` | `tuple` |
| `PySlice_Type` | `slice` |
| `PyByteArray_Type` | `bytearray` |

"O&" 转换接受两个参数 `(converter, addr)`，并使用一个函数将 `PyObject *` 转换为 C 数据类型。`converter` 是一个指向函数的指针，其原型为 `int converter(PyObject *obj, void *addr)`，其中 `obj` 是传入的 Python 对象，`addr` 是在 `PyArg_ParseTuple()` 中作为第二个参数提供的地址。`converter()` 在成功时应返回 1，失败时返回 0。出错时，转换函数还应引发一个异常。这种转换可用于将 Python 对象（如列表或元组）映射到 C 数据结构。例如，以下是早期代码中 `distance()` 包装函数的一种可能实现：

```
/* Convert a tuple into a Point structure. */
int convert_point(PyObject *obj, void *addr) {
    Point *p = (Point *) addr;
    return PyArg_ParseTuple(obj,"ii", &p->x, &p->y);
}
PyObject *py_distance(PyObject *self, PyObject *args) {
    Point p1, p2;
    double result;
    if (!PyArg_ParseTuple(args,"O&O&",
                          convert_point, &p1, convert_point, &p2)) {
        return NULL;
    }
    result = distance(&p1,&p2);
    return Py_BuildValue("d",result);
}
```

最后，参数格式字符串还可以包含一些与元组解包、文档、错误消息和默认参数相关的附加修饰符。以下是这些修饰符的列表：

| 格式字符串 | 描述 |
| --- | --- |
| "(items)" | 解包一个对象元组。items 由格式转换组成。 |
| "|" | 可选参数的开始。 |
| ":" | 参数的结束。剩余文本为函数名称。 |
| ";" | 参数的结束。剩余文本为错误消息。 |

"(items)" 从 Python 元组中解包值。这是将元组映射到简单 C 结构的实用方法。例如，以下是 py_distance() 包装函数的另一种可能实现：

```
PyObject *py_distance(PyObject *self, PyObject *args) {
    Point p1, p2;
    double result;
    if (!PyArg_ParseTuple(args,"(dd)(dd)",
                          &p1.x, &p1.y, &p2.x, &p2.y)) {
        return NULL;
    }
    result = distance(&p1,&p2);
    return Py_BuildValue("d",result);
}
```

修饰符 "|" 指定所有剩余参数均为可选。它在格式说明符中只能出现一次，且不能嵌套。修饰符 ":" 表示参数的结束。其后的任何文本将作为错误消息中的函数名称使用。修饰符 ";" 表示参数的结束。其后的任何文本将作为错误消息使用。注意，: 和 ; 只能使用其中一个。以下是一些示例：

```
PyArg_ParseTuple(args,"ii:gcd", &x, &y);
PyArg_ParseTuple(args,"ii; gcd requires 2 integers", &x, &y);

/* Parse with optional arguments */
PyArg_ParseTuple(args,"s|s", &buffer, &delimiter);
```

#### 从 C 到 Python 的类型转换

以下 C 函数用于将 C 变量中的值转换为 Python 对象：

```
PyObject *Py_BuildValue(char *format, ...)
```

该函数根据一系列 C 变量构建一个 Python 对象。format 是一个描述所需转换的字符串。其余参数是要转换的 C 变量的值。

格式说明符与 `PyArg_ParseTuple*` 函数使用的格式类似，如表 26.4 所示。

表 26.4 Py_BuildValue() 的格式说明符

| 格式 | Python 类型 | C 类型 | 描述 |
| :--- | :--- | :--- | :--- |
| "" | None | void | 无。 |
| "s" | String | char * | 以空字符结尾的字符串。如果 C 字符串指针为 NULL，则返回 None。 |
| "s#" | String | char *, int | 字符串及其长度。可以包含空字节。如果 C 字符串指针为 NULL，则返回 None。 |
| "y" | Bytes | char * | 与 "s" 相同，但返回字节字符串。 |
| "y#" | Bytes | char *, int | 与 "s#" 相同，但返回字节字符串。 |
| "z" | String 或 None | char * | 与 "s" 相同。 |
| "z#" | String 或 None | char *, int | 与 "s#" 相同。 |
| "u" | Unicode | Py_UNICODE * | 以空字符结尾的 Unicode 字符串。如果字符串指针为 NULL，则返回 None。 |
| "u#" | Unicode | Py_UNICODE * | Unicode 字符串及其长度。 |
| "U" | Unicode | char * | 将以空字符结尾的 C 字符串转换为 Unicode 字符串。 |
| "U#" | Unicode | char *, int | 将 C 字符串转换为 Unicode。 |
| "b" | Integer | char | 8 位整数。 |
| "B" | Integer | unsigned char | 8 位无符号整数。 |
| "h" | Integer | short | 短 16 位整数。 |
| "H" | Integer | unsigned short | 无符号短 16 位整数。 |
| "i" | Integer | int | 整数。 |
| "I" | Integer | unsigned int | 无符号整数。 |
| "l" | Integer | long | 长整数。 |
| "L" | Integer | unsigned long | 无符号长整数。 |
| "k" | Integer | long long | 长长整数。 |
| "K" | Integer | unsigned long long | 无符号长长整数。 |
| "n" | Integer | Py_ssize_t | Python size 类型。 |
| "c" | String | char | 单个字符。创建长度为 1 的 Python 字符串。 |
| "f" | Float | float | 单精度浮点数。 |
| "d" | Float | double | 双精度浮点数。 |
| "D" | Complex | Py_complex | 复数。 |
| "O" | Any | PyObject * | 任意 Python 对象。对象本身不变，仅其引用计数加 1。如果传入 NULL 指针，则返回 NULL 指针。当其他地方已发出错误信号且你希望错误传播时，这很有用。 |

以下是构建不同类型值的一些示例：

```
Py_BuildValue("")                          None
Py_BuildValue("i",37)                      37
Py_BuildValue("ids",37,3.4,"hello")        (37, 3.5, "hello")
Py_BuildValue("s#","hello",4)              "hell"
Py_BuildValue("()")                        ()
Py_BuildValue("(i)",37)                     (37,)
Py_BuildValue("[ii]",1,2)                  [1,2]
Py_BuildValue("[i,i]",1,2)                 [1,2]
Py_BuildValue("{s:i,s:i}","x",1,"y",2)     {'x':1, 'y':2}
```

对于涉及 `char *` 的 Unicode 字符串转换，假定数据由使用默认 Unicode 编码（通常是 UTF-8）编码的一系列字节组成。数据传递给 Python 时将自动解码为 Unicode 字符串。唯一的例外是返回原始字节字符串的 "y" 和 "y#" 转换。

#### 向模块添加值

在扩展模块的模块初始化函数中，通常需要添加常量和其他支持值。可以使用以下函数来实现：

```
int PyModule_AddObject(PyObject *module, const char *name, PyObject *value)
```

向模块添加一个新值。name 是值的名称，value 是包含该值的 Python 对象。你可以使用 `Py_BuildValue()` 来构建这个值。

```
int PyModule_AddIntConstant(PyObject *module, const char *name, long value)
```

向模块添加一个整数值。

```
void PyModule_AddStringConstant(PyObject *module, const char *name, const char *value)
```

向模块添加一个字符串值。value 必须是以空字符结尾的字符串。

```
void PyModule_AddIntMacro(PyObject *module, macro)
```

以整数形式向模块添加一个宏值。**macro** 必须是预处理器宏的名称。

```
void PyModule_AddStringMacro(PyObject *module, macro)
```

以字符串形式向模块添加一个宏值。

#### 错误处理

扩展模块通过向解释器返回 `NULL` 来指示错误。在返回 NULL 之前，应使用以下函数之一设置异常：

```
void PyErr_NoMemory()
```

引发 `MemoryError` 异常。

```
void PyErr_SetFromErrno(PyObject *exc)
```

引发一个异常。**exc** 是一个异常对象。异常的值取自 C 库中的 `errno` 变量。

```
void PyErr_SetFromErrnoWithFilename(PyObject *exc, char *filename)
```

与 `PyErr_SetFromErrno()` 类似，但也将文件名包含在异常值中。

```
void PyErr_SetObject(PyObject *exc, PyObject *val)
```

引发一个异常。**exc** 是一个异常对象，**val** 是一个包含异常值的对象。

```
void PyErr_SetString(PyObject *exc, char *msg)
```

引发一个异常。**exc** 是一个异常对象，**msg** 是描述错误信息的消息。

这些函数中的 **exc** 参数可以设置为以下值之一：

| C 名称 | Python 异常 |
| --- | --- |
| PyExc_ArithmeticError | ArithmeticError |
| PyExc_AssertionError | AssertionError |
| PyExc_AttributeError | AttributeError |
| PyExc_EnvironmentError | EnvironmentError |
| PyExc_EOFError | EOFError |
| PyExc_Exception | Exception |
| PyExc_FloatingPointError | FloatingPointError |
| PyExc_ImportError | ImportError |
| PyExc_IndexError | IndexError |
| PyExc_IOError | IOError |
| PyExc_KeyError | KeyError |
| PyExc_KeyboardInterrupt | KeyboardInterrupt |
| PyExc_LookupError | LookupError |
| PyExc_MemoryError | MemoryError |
| PyExc_NameError | NameError |
| PyExc_NotImplementedError | NotImplementedError |



#### 引用计数

与用 Python 编写的程序不同，C 扩展可能需要操作 Python 对象的引用计数。这通过以下宏来完成，所有宏都应用于 `PyObject *` 类型的对象。

| 宏 | 描述 |
| --- | --- |
| `Py_INCREF(obj)` | 递增 `obj` 的引用计数，`obj` 必须非空。 |
| `Py_DECREF(obj)` | 递减 `obj` 的引用计数，`obj` 必须非空。 |
| `Py_XINCREF(obj)` | 递增 `obj` 的引用计数，`obj` 可以为空。 |
| `Py_XDECREF(obj)` | 递减 `obj` 的引用计数，`obj` 可以为空。 |

在 C 中操作 Python 对象的引用计数是一个微妙的话题，强烈建议读者在进一步操作之前，查阅位于 http://docs.python.org/extending 的“扩展和嵌入 Python 解释器”文档。一般规则是，在 C 扩展函数中，除了以下情况，无需担心引用计数：

- 如果你保存了一个 Python 对象的引用以供以后使用或保存在 C 结构中，则必须增加其引用计数。
- 类似地，要释放先前保存的对象，则递减其引用计数。
- 如果你从 C 中操作 Python 容器（列表、字典等），则可能必须手动操作各个元素的引用计数。例如，获取或设置容器中元素的高级操作通常会增加引用计数。

如果你的扩展代码导致解释器崩溃（你忘记增加引用计数），或者当你的扩展函数被使用时解释器发生内存泄漏（你忘记递减引用计数），那么你就遇到了引用计数问题。

#### 线程

全局解释器锁用于防止多个线程同时在解释器中执行。如果用扩展模块编写的函数长时间执行，它将阻塞其他线程的执行，直到完成。这是因为当扩展函数被调用时，锁会被持有。如果扩展模块是线程安全的，则可以使用以下宏来释放和重新获取全局解释器锁：

```
Py_BEGIN_ALLOW_THREADS
```

释放全局解释器锁，并允许其他线程在解释器中运行。当锁被释放时，C 扩展不得调用 Python C API 中的任何函数。

```
Py_END_ALLOW_THREADS
```

重新获取全局解释器锁。在这种情况下，扩展将阻塞，直到成功获取锁。

以下示例说明了这些宏的使用：

```
PyObject *py_wrapper(PyObject *self, PyObject *args) {
    ...
    PyArg_ParseTuple(args, ...)
    Py_BEGIN_ALLOW_THREADS
    result = run_long_calculation(args);
    Py_END_ALLOW_THREADS
    ...
    return Py_BuildValue(fmt,result);
}
```

#### 嵌入 Python 解释器

Python 解释器也可以嵌入到 C 应用程序中。通过嵌入，Python 解释器作为编程库运行，C 程序可以初始化解释器，让解释器运行脚本和代码片段，加载库模块，并操作用 Python 实现的函数和对象。

#### 嵌入模板

通过嵌入，你的 C 程序负责控制解释器。这是一个简单的 C 程序，展示了最简单的嵌入方式：

```
#include <Python.h>

int main(int argc, char **argv) {
    Py_Initialize();
    PyRun_SimpleString("print('Hello World')");
    Py_Finalize();
    return 0;
}
```

在此示例中，初始化了解释器，执行了一个作为字符串的短脚本，然后关闭了解释器。在进一步操作之前，通常最好先让前面的示例工作起来。

#### 编译和链接

要在 UNIX 上编译嵌入式解释器，你的代码必须包含 "Python.h" 头文件，并链接解释器库，例如 libpython2.6.a。头文件通常位于 /usr/local/include/python2.6，库通常位于 /usr/local/lib/python2.6/config。对于 Windows，你需要在 Python 安装目录中找到这些文件。请注意，解释器可能依赖于其他库，你需要在链接时包含它们。不幸的是，这往往是特定于平台的，并与 Python 在你机器上的配置方式有关——你可能需要花点时间进行调试。

#### 基本的解释器操作和设置

以下函数用于设置解释器和运行脚本：

```
int PyRun_AnyFile(FILE *fp, char *filename)
```

如果 *fp* 是像 UNIX 中 tty 这样的交互式设备，此函数将调用 PyRun_InteractiveLoop()。否则，调用 PyRun_SimpleFile()。*filename* 是一个字符串，为输入流提供一个名称。此名称将在解释器报告错误时显示。如果 `filename` 为 `NULL`，则使用默认字符串 `"???"` 作为文件名。

```
int PyRun_SimpleFile(FILE *fp, char *filename)
```

类似于 `PyRun_SimpleString()`，只是程序是从文件 `fp` 中读取的。

```
int PyRun_SimpleString(char *command)
```

在解释器的 `__main__` 模块中执行 `command`。成功返回 `0`，发生异常返回 `-1`。

```
int PyRun_InteractiveOne(FILE *fp, char *filename)
```

执行单个交互式命令。

```
int PyRun_InteractiveLoop(FILE *fp, char *filename)
```

以交互模式运行解释器。

```
void Py_Initialize()
```

初始化 Python 解释器。在使用 C API 中的任何其他函数之前，应调用此函数，`Py_SetProgramName()`、`PyEval_InitThreads()`、`PyEval_ReleaseLock()` 和 `PyEval_AcquireLock()` 除外。

```
int Py_IsInitialized()
```

如果解释器已初始化，返回 `1`；否则返回 `0`。

```
void Py_Finalize()
```

通过销毁自调用 `Py_Initialize()` 以来创建的所有子解释器和对象来清理解释器。通常，此函数会释放解释器分配的所有内存。但是，循环引用和扩展模块可能会引入此函数无法回收的内存泄漏。

```
void Py_SetProgramName(char *name)
```

设置通常在 `sys` 模块的 `argv[0]` 参数中找到的程序名称。此函数应仅在 `Py_Initialize()` 之前调用。

```
char *Py_GetPrefix()
```

返回已安装的平台无关文件的前缀。这与在 `sys.prefix` 中找到的值相同。

```
char *Py_GetExecPrefix()
```

返回已安装的平台相关文件的执行前缀。这与在 `sys.exec_prefix` 中找到的值相同。

```
char *Py_GetProgramFullPath()
```

返回 Python 可执行文件的完整路径名。

```
char *Py_GetPath()
```

返回默认的模块搜索路径。路径以字符串形式返回，该字符串由平台相关的分隔符（UNIX 上为 `:`，DOS/Windows 上为 `;`）分隔的目录名组成。



## 第26章 扩展与嵌入Python

```c
int PySys_SetArgv(int argc, char **argv)
```

设置用于填充`sys.argv`值的命令行选项。此函数应在`Py_Initialize()`之前调用。

#### 从C语言访问Python

尽管从C语言访问解释器的方式多种多样，但嵌入式应用中常见的四个核心任务是：

- 导入Python库模块（模拟`import`语句）
- 获取模块中定义对象的引用
- 调用Python函数、类和方法
- 访问对象的属性（数据、方法等）

所有这些操作都可以通过Python C API中定义的基本操作来完成：

```c
PyObject *PyImport_ImportModule(const char *modname)
```

导入名为`modname`的模块，并返回关联模块对象的引用。

```c
PyObject *PyObject_GetAttrString(PyObject *obj, const char *name)
```

从对象获取属性。此操作等同于`obj.name`。

```c
int PyObject_SetAttrString(PyObject *obj, const char *name, PyObject *value)
```

设置对象的属性。此操作等同于`obj.name = value`。

```c
PyObject *PyEval_CallObject(PyObject *func, PyObject *args)
```

使用参数`args`调用`func`。`func`是一个Python可调用对象（函数、方法、类等）。`args`是一个参数元组。

```c
PyObject *PyEval_CallObjectWithKeywords(PyObject *func, PyObject *args, PyObject *kwargs)
```

使用位置参数`args`和关键字参数`kwargs`调用`func`。`func`是一个可调用对象，`args`是一个元组，`kwargs`是一个字典。

以下示例通过从C语言调用和使用`re`模块的各个部分，演示了这些函数的使用方法。该程序打印出从`stdin`读取的所有包含用户提供的Python正则表达式的行。

```c
#include "Python.h"

int main(int argc, char **argv) {
    PyObject *re;
    PyObject *re_compile;
    PyObject *pat;
    PyObject *pat_search;
    PyObject *args;
    char      buffer[256];

    if (argc != 2) {
        fprintf(stderr,"Usage: %s pattern\n",argv[0]);
        exit(1);
    }

    Py_Initialize();

    /* import re */
    re   = PyImport_ImportModule("re");

    /* pat = re.compile(pat,flags) */
    re_compile = PyObject_GetAttrString(re,"compile");
    args = Py_BuildValue("(s)", argv[1]);
    pat = PyEval_CallObject(re_compile, args);
    Py_DECREF(args);

    /* pat_search = pat.search  - bound method*/
    pat_search = PyObject_GetAttrString(pat,"search");

    /* Read lines and perform matches */
    while (fgets(buffer,255,stdin)) {
        PyObject *match;
        args = Py_BuildValue("(s)", buffer);

        /* match = pat.search(buffer) */
        match = PyEval_CallObject(pat_search,args);
        Py_DECREF(args);
        if (match != Py_None) {
            printf("%s",buffer);
        }
        Py_XDECREF(match);
    }
    Py_DECREF(pat);
    Py_DECREF(re_compile);
    Py_DECREF(re);
    Py_Finalize();
    return 0;
}
```

在任何嵌入式代码中，正确管理引用计数都至关重要。特别是，对于从C语言创建的任何对象或由于函数执行而返回给C语言的任何对象，你都需要减少其引用计数。

#### 将Python对象转换为C语言

嵌入式使用解释器的一个主要问题是，如何将Python函数或方法调用的结果转换为合适的C语言表示形式。作为一般规则，你需要提前确切知道某个操作将返回哪种类型的数据。遗憾的是，没有像`PyArg_ParseTuple()`那样便于转换单个对象值的高级便捷函数。然而，只要你知道正在处理的是哪种类型的Python对象，以下列出了一些底层转换函数，可以将几种基本的Python数据类型转换为相应的C语言表示形式：

##### Python到C的转换函数

- `long PyInt_AsLong(PyObject *)`
- `long PyLong_AsLong(PyObject *)`
- `double PyFloat_AsDouble(PyObject *)`
- `char *PyString_AsString(PyObject *)`（仅Python 2）
- `char *PyBytes_AsString(PyObject *)`（仅Python 3）

对于比这更复杂的类型，你需要查阅C API文档（http://docs.python.org/c-api）。

#### ctypes

ctypes模块为Python提供了访问DLL和共享库中定义的C函数的能力。虽然你需要了解底层C库的一些细节（名称、调用参数、类型等），但你可以使用ctypes访问C代码，而无需编写C扩展包装代码或用C编译器编译任何内容。ctypes是一个功能庞大的库模块，具有许多高级功能。这里我们介绍入门所需的核心部分。

##### 加载共享库

以下类用于加载C共享库并返回表示其内容的实例：

```c
CDLL(name [, mode [, handle [, use_errno [, use_last_error]]]])
```

一个表示标准C共享库的类。name是库的名称，例如'libc.so.6'或'msvcrt.dll'。mode提供标志来确定如何加载库，并传递给底层的UNIX dlopen()函数。它可以设置为RTLD_LOCAL、RTLD_GLOBAL或RTLD_DEFAULT（默认值）的按位或。在Windows上，mode被忽略。handle指定一个已加载库的句柄（如果可用）。默认情况下，它是None。use_errno是一个布尔标志，它在处理加载库中的C errno变量时增加了一层额外的安全保护。这层保护在调用任何外部函数之前保存errno的线程本地副本，并在之后恢复其值。默认情况下，use_errno为False。use_last_error是一个布尔标志，它启用了两个函数get_last_error()和set_last_error()，可用于操作系统错误代码。这些在Windows上更常用。默认情况下，use_last_error为False。

```c
WinDLL(name [, mode [, handle [, use_errno [, use_last_error]]]])
```

与CDLL()相同，但库中的函数假定遵循Windows stdcall调用约定（Windows）。

以下实用函数可用于在系统上定位共享库，并构造一个适合用作前面类中name参数的名称。它定义在ctypes.util子模块中：

```c
find_library(name)
```

定义在ctypes.util中。返回与库名称对应的路径名。name是一个不带任何文件后缀的库名称，例如'libc'、'libm'等。函数返回的字符串是一个完整的路径名，例如'/usr/lib/libc.so.6'。此函数的行为高度依赖于系统，取决于共享库和环境（例如，LD_LIBRARY_PATH和其他参数的设置）的底层配置。如果找不到库，则返回None。

##### 外部函数

由CDLL()类创建的共享库实例充当底层C库的代理。要访问库内容，只需使用属性查找（`.`运算符）。例如：

```python
>>> import ctypes
>>> libc = ctypes.CDLL("/usr/lib/libc.dylib")
>>> libc.rand()
16807
>>> libc.atoi("12345")
12345
>>>
```

在此示例中，`libc.rand()`和`libc.atoi()`等操作直接调用已加载C库中的函数。

ctypes假定所有函数接受`int`或`char *`类型的参数，并返回`int`类型的结果。因此，即使之前的函数调用“有效”，对其他C库函数的调用可能无法按预期工作。例如：

```python
>>> libc.atof("34.5")
-1073746168
>>>
```

要解决此问题，可以通过更改以下属性来设置任何外部函数`func`的类型签名和处理方式：

###### func.argtypes

一个ctypes数据类型（此处描述）的元组，描述`func`的输入参数。

###### func.restype

一个ctypes数据类型，描述`func`的返回值。对于返回void的函数，使用`None`。

###### func.errcheck

一个Python可调用对象，接受三个参数（`result`、`func`、`args`），其中`result`是外部函数返回的值，`func`是外部函数本身的引用，`args`是输入参数的元组。此函数在外部函数调用之后被调用，可用于执行错误检查和其他操作。

以下是修复`atof()`函数接口的示例，如前面的示例所示：

```python
>>> libc.atof.restype=ctypes.c_double
>>> libc.atof("34.5")
34.5
>>>
```

`ctypes.c_double`是对预定义数据类型的引用。下一节将描述这些数据类型。

##### 数据类型

表26.5展示了可用于外部函数`argtypes`和`restype`属性的ctypes数据类型。“Python值”列描述了给定数据类型接受的Python数据类型。



###### 表 26.5 ctypes 数据类型

| ctypes 类型名称 | C 数据类型 | Python 值 |
| --- | --- | --- |
| c_bool | bool | True 或 False |
| c_bytes | signed char | 小整数 |
| c_char | char | 单个字符 |
| c_char_p | char * | 以空字符结尾的字符串或字节串 |
| c_double | double | 浮点数 |
| c_longdouble | long double | 浮点数 |
| c_float | float | 浮点数 |
| c_int | int | 整数 |
| c_int8 | signed char | 8 位整数 |
| c_int16 | short | 16 位整数 |
| c_int32 | int | 32 位整数 |
| c_int64 | long long | 64 位整数 |
| c_long | long | 整数 |
| c_longlong | long long | 整数 |
| c_short | short | 整数 |
| c_size_t | size_t | 整数 |
| c_ubyte | unsigned char | 无符号整数 |
| c_uint | unsigned int | 无符号整数 |
| c_uint8 | unsigned char | 8 位无符号整数 |
| c_uint16 | unsigned short | 16 位无符号整数 |
| c_uint32 | unsigned int | 32 位无符号整数 |
| c_uint64 | unsigned long long | 64 位无符号整数 |
| c_ulong | unsigned long | 无符号整数 |
| c_ulonglong | unsigned long long | 无符号整数 |
| c_ushort | unsigned short | 无符号整数 |
| c_void_p | void * | 整数 |
| c_wchar | wchar_t | 单个 Unicode 字符 |
| c_wchar_p | wchar_t * | 以空字符结尾的 Unicode 字符串 |

要创建一个表示 C 指针的类型，请对其他类型之一应用以下函数：

```
POINTER(type)
```

定义一个指向类型 *type* 的指针类型。例如，`POINTER(c_int)` 表示 C 类型 `int *`。

要定义一个表示固定大小 C 数组的类型，请将现有类型乘以数组维度数。例如，`c_int*4` 表示 C 数据类型 `int[4]`。

要定义一个表示 C 结构体或联合体的类型，你需要继承基类 `Structure` 或 `Union` 之一。在每个派生类中，你需要定义一个类变量 `_fields_` 来描述其内容。`_fields_` 是由 2 个或 3 个元素组成的元组列表，形式为 `(name, ctype)` 或 `(name, ctype, width)`，其中 *name* 是结构体字段的标识符，ctype 是描述类型的 ctype 类，width 是整数位域宽度。例如，考虑以下 C 结构体：

```
struct Point {
    double x, y;
};
```

该结构体的 ctypes 描述为

```
class Point(Structure):
    _fields_ = [ ("x", c_double),
                 ("y", c_double) ]
```

##### 调用外部函数

要调用库中的函数，你只需使用与其类型签名兼容的一组参数调用相应的函数。对于 c_int、c_double 等简单数据类型，你可以直接传递兼容的 Python 类型作为输入（整数、浮点数等）。也可以传递 c_int、c_double 及类似类型的实例作为输入。对于数组，你可以直接传递兼容类型的 Python 序列。

要将指针传递给外部函数，你必须首先创建一个 ctypes 实例来表示将被指向的值，然后使用以下函数之一创建指针对象：

###### byref(cvalue [, offset])

表示一个指向 cvalue 的轻量级指针。cvalue 必须是 ctypes 数据类型的实例。offset 是要添加到指针值的字节偏移量。该函数返回的值只能在函数调用中使用。

###### pointer(cvalue)

创建一个指向 cvalue 的指针实例。cvalue 必须是 ctypes 数据类型的实例。这会创建前面描述的 POINTER 类型的实例。

以下示例展示了如何将 double * 类型的参数传递给 C 函数：

```
dval = c_double(0.0)          # Create a double instance
r = foo(byref(dval))           # Calls foo(&dval)

p_dval = pointer(dval)         # Creates a pointer variable
r = foo(p_dval)                # Calls foo(p_dval)

# Inspect the value of dval afterwards
print (dval.value)
```

需要注意的是，你无法为 int 或 float 等内置类型创建指针。如果底层的 C 函数更改了值，传递这些类型的指针将违反可变性要求。

ctypes 实例 cobj 的 cobj.value 属性包含内部数据。例如，前面代码中对 dval.value 的引用返回存储在 ctypes c_double 实例 dval 中的浮点值。

要将结构体传递给 C 函数，你必须创建一个结构体或联合体的实例。为此，请按如下方式调用先前定义的结构体或联合体类型 *StructureType*：

```
StructureType(*args, **kwargs)
```

创建一个 *StructureType* 的实例，其中 *StructureType* 是派生自 `Structure` 或 `Union` 的类。*\*args* 中的位置参数按照与 `_fields_` 中列出的相同顺序来初始化结构体成员。**\*\*kwargs* 中的关键字参数仅初始化指定名称的结构体成员。

##### 替代的类型构造方法

ctypes 类型（如 `c_int`、`POINTER` 等）的所有实例都具有一些类方法，用于从内存位置和其他对象创建 ctypes 类型的实例。

```
ty.from_buffer(source [,offset])
```

创建一个 ctypes 类型 *ty* 的实例，该实例与 *source* 共享同一内存缓冲区。*source* 必须是任何支持可写缓冲区接口的其他对象（例如 `bytearray`、`array` 模块中的 `array` 对象、`mmap` 等）。*offset* 是从缓冲区起始位置开始使用的字节数。

```
ty.from_buffer_copy(source [, offset])
```

与 `ty.from_buffer()` 相同，但会制作内存副本，并且 *source* 可以是只读的。

```
ty.from_address(address)
```

从指定为整数的原始内存地址 *address* 创建 ctypes 类型 *ty* 的实例。

```
ty.from_param(obj)
```

从 Python 对象 *obj* 创建 ctypes 类型 *ty* 的实例。这仅在传递的对象 *obj* 可以适配为适当类型时才有效。例如，Python 整数可以适配为 `c_int` 实例。

```
ty.in_dll(library, name)
```

从共享库中的符号创建 ctypes 类型 *ty* 的实例。*library* 是已加载库的实例，例如由 `CDLL` 类创建的对象。*name* 是符号的名称。此方法可用于为库中定义的全局变量创建 ctypes 包装器。

以下示例展示了如何为库 `libexample.so` 中定义的全局变量 `int status` 创建引用。

```
libexample = ctypes.CDLL("libexample.so")
status = ctypes.c_int.in_dll(libexample,"status")
```

##### 实用函数

ctypes 定义了以下实用函数：

**addressof(cobj)**

以整数形式返回 cobj 的内存地址。cobj 必须是 ctypes 类型的实例。

**alignment(ctype_or_obj)**

返回 ctypes 类型或对象的整数对齐要求。ctype_or_obj 必须是 ctypes 类型或类型的实例。

**cast(cobj, ctype)**

将 ctypes 对象 cobj 转换为 ctype 中给出的新类型。这仅适用于指针，因此 cobj 必须是指针或数组，ctype 必须是指针类型。

**create_string_buffer(init [, size])**

创建一个可变字符缓冲区，作为 c_char 类型的 ctypes 数组。init 是表示初始内容的整数大小或字符串。size 是一个可选参数，用于指定当 init 为字符串时使用的大小。默认情况下，大小设置为比 init 中的字符数多一。Unicode 字符串使用默认编码编码为字节。

**create_unicode_buffer(init [, size])**

与 create_string_buffer() 相同，但创建的是 c_wchar 类型的 ctypes 数组。

**get_errno()**

返回 ctypes 私有副本中 errno 的当前值。

**get_last_error()**

返回 Windows 上 ctypes 私有副本中 LastError 的当前值。

**memmove(dst, src, count)**

将 count 个字节从 src 复制到 dst。src 和 dst 可以是表示内存地址的整数，也可以是可转换为指针的 ctypes 类型实例。与 C 的 memmove() 库函数相同。

**memset(dst, c, count)**

将从 dst 开始的 count 个字节的内存设置为字节值 c。dst 可以是整数或 ctypes 实例。c 是表示 0-255 范围内的字节的整数。

**resize(cobj, size)**

调整用于表示 ctypes 对象 cobj 的内部内存的大小。size 是以字节为单位的新大小。

**set_conversion_mode(encoding, errors)**

设置从 Unicode 字符串转换为 8 位字符串时使用的 Unicode 编码。encoding 是编码名称，如 'utf-8'，errors 是错误处理策略，如 'strict' 或 'ignore'。返回一个包含先前设置的元组 (encoding, errors)。



###### set_errno(value)

设置 ctypes 私有的系统 errno 变量副本。返回之前的值。

###### set_last_error(value)

设置 Windows LastError 变量并返回之前的值。

###### sizeof(type_or_cobj)

返回 ctypes 类型或对象的大小（以字节为单位）。

###### string_at(address [, size])

返回从地址 address 开始的 size 字节内存的字节字符串。如果省略 size，则假定该字节字符串以 NULL 结尾。

###### wstring_at(address [, size])

返回从地址 address 开始的 size 个宽字符的 Unicode 字符串。如果省略 size，则假定该字符字符串以 NULL 结尾。

##### 示例

以下示例通过构建一个接口来使用 ctypes 模块，该接口连接了本章第一部分（详细介绍了如何手动创建 Python 扩展模块）中使用的一组 C 函数。

```python
####### example.py

import ctypes
_example = ctypes.CDLL("./libexample.so")

# int gcd(int, int)
gcd = _example.gcd
gcd.argtypes = (ctypes.c_int,
                ctypes.c_int)
gcd.restype = ctypes.c_int


# int replace(char *s, char oldch, char newch)
_example.replace.argtypes = (ctypes.c_char_p,
                             ctypes.c_char,
                             ctypes.c_char)
_example.replace.restype = ctypes.c_int

def replace(s, oldch, newch):
    sbuffer = ctypes.create_string_buffer(s)
    nrep = _example.replace(sbuffer,oldch,newch)
    return (nrep,sbuffer.value)

# double distance(Point *p1, Point *p2)
class Point(ctypes.Structure):
    _fields_ = [("x", ctypes.c_double),
                ("y", ctypes.c_double)]

_example.distance.argtypes = (ctypes.POINTER(Point),
                              ctypes.POINTER(Point))
_example.distance.restype = ctypes.c_double

def distance(a,b):
    p1 = Point(*a)
    p2 = Point(*b)
    return _example.distance(byref(p1),byref(p2))
```

总而言之，使用 `ctypes` 总会涉及到一个复杂度不一的 Python 包装层。例如，你可能直接调用 C 函数，但也可能需要实现一个小的包装层来处理底层 C 代码的某些方面。在这个示例中，`replace()` 函数采取了额外的步骤来处理 C 库会修改输入缓冲区这一事实。`distance()` 函数则执行了额外的步骤，从元组创建 `Point` 实例并传递指针。

> **注意**
>
> `ctypes` 模块还有许多此处未涵盖的高级功能。例如，该库可以在 Windows 上访问多种不同类型的库，并且支持回调函数、不完整类型以及其他细节。在线文档包含许多示例，这应该是进一步使用的起点。

#### 高级扩展与嵌入

如果你用简单的 C 代码扩展 Python，创建手写的扩展模块或使用 `ctypes` 通常是直接了当的。然而，对于更复杂的情况，它很快就会变得繁琐。为此，你需要寻找合适的扩展构建工具。这些工具要么自动化了大部分扩展构建过程，要么提供了一个更高级别的编程接口。可以在 http://wiki.python.org/moin/IntegratingPythonWithOtherLanguages 找到各种此类工具的链接。不过，这里将简要展示一个使用 SWIG (http://www.swig.org) 的示例以作说明。需要完全说明的是，SWIG 最初是由本书作者创建的。

使用自动化工具时，你通常只需在高级别描述扩展模块的内容。例如，使用 SWIG 时，你编写一个如下所示的简短接口规范：

```c
/* example.i : Sample Swig specification */
%module example
%{
/* Preamble. Include all required header files here */
#include "example.h"
%}

/* Module contents. List all C declarations here */
typedef struct Point {
  double x;
  double y;
} Point;
extern int    gcd(int, int);
extern int    replace(char *s, char oldch, char newch);
extern double distance(Point *a, Point *b);
```

使用此规范，SWIG 会自动生成制作 Python 扩展模块所需的一切。要运行 SWIG，你只需像调用编译器一样调用它：

```
% swig -python example.i
%
```

作为输出，它会生成一组 .c 和 .py 文件。然而，你通常不必过多担心这些。如果你使用 distutils 并在 setup 规范中包含 .i 文件，它将在构建扩展时自动为你运行 SWIG。例如，这个 setup.py 文件会自动对列出的 example.i 文件运行 SWIG。

```python
##### setup.py
from distutils.core import setup, Extension
setup(name="example",
      version="1.0",
      py_modules = ['example.py'],
      ext_modules = [
        Extension("_example",
                  ["example.i","example.c"])
      ]
     )
```

结果表明，对于本例中的可工作扩展模块，只需要这个 example.i 文件和 setup.py 文件。如果你输入 `python setup.py build_ext --inplace`，你会发现你的目录中有一个完全可工作的扩展。

### Jython 和 IronPython

扩展和嵌入不仅限于 C 程序。如果你使用 Java，可以考虑使用 Jython (http://www.jython.org)，它是用 Java 完全重新实现的 Python 解释器。使用 Jython，你可以简单地使用 import 语句导入 Java 库。例如：

```
bash-3.2$ jython
Jython 2.2.1 on java1.5.0_16
Type "copyright", "credits" or "license" for more information.
>>> from java.lang import System
>>> System.out.println("Hello World")
Hello World
>>>
```

如果你在 Windows 上使用 .NET 框架，可以考虑使用 IronPython (http://www.codeplex.com/Wiki/View.aspx?ProjectName=IronPython)，它是用 C# 完全重新实现的 Python 解释器。使用 IronPython，你可以以类似的方式轻松地从 Python 访问所有 .NET 库。例如：

```
% ipy
IronPython 1.1.2 (1.1.2) on .NET 2.0.50727.42
Copyright (c) Microsoft Corporation. All rights reserved.
>>> import System.Math
>>> dir(System.Math)
['Abs', 'Acos', 'Asin', 'Atan', 'Atan2', 'BigMul', 'Ceiling', 'Cos', 'Cosh', ...]
>>> System.Math.Cos(3)
-0.9899924966
>>>
```

更详细地介绍 Jython 和 IronPython 超出了本书的范围。但是，请记住它们都是 Python——最主要的差异在于它们的库。

### 附录

#### Python 3

2008年12月，Python 3.0 发布——这是 Python 语言的一次重大更新，在许多关键领域打破了与 Python 2 的向后兼容性。关于 Python 3 所做更改的相当完整的概述可以在 http://docs.python.org/3.0/whatsnew/3.0.html 的“Python 3.0 新特性”文档中找到。在某种意义上，本书的前 26 章可以被视为“新特性”文档的对立面。也就是说，到目前为止涵盖的所有内容都集中在 Python 2 和 Python 3 *共有* 的特性上。这包括所有标准库模块、主要语言特性和示例。除了少数命名差异和 `print()` 是一个函数这一事实外，没有描述 Python 3 的独特功能。

本附录的主要重点是描述仅在 Python 3 版本中可用的语言新特性，以及如果你打算迁移现有代码时需要记住的一些重要差异。在本附录的最后，描述了一些移植策略和 `2to3` 代码转换工具的使用。

##### 谁应该使用 Python 3？

在进一步讨论之前，解决谁应该使用 Python 3.0 发布版这个问题很重要。在 Python 社区中，人们一直知道向 Python 3 的过渡不会一蹴而就，Python 2 分支将在未来一段时间（数年）内继续维护。因此，在撰写本文时，没有紧迫的需求去放弃 Python 2 代码。我怀疑，在多年后撰写本书第 5<sup>th</sup> 版时，大量的 Python 2 代码仍将继续开发中。

Python 3.0 面临的一个主要问题是第三方库的兼容性。Python 的强大之处很大程度上来自其大量的框架和库。然而，除非这些库被明确移植到 Python 3，否则它们几乎肯定无法工作。这个问题被放大，因为许多库依赖于其他库，而这些库又依赖于更多的库。截至撰写本文时（2009年），主要的 Python 库和框架甚至还没有移植到 Python 2.4，更不用说 2.6 或 3.0 了。因此，如果你打算使用 Python 运行第三方代码，目前最好坚持使用 Python 2。如果你拿到这本书时是 2012 年，那么希望情况会有所改善。

尽管 Python 3 清理了许多语言中的小缺陷，但目前尚不清楚 Python 3 是否是刚想学习基础知识的新用户的明智选择。几乎所有现有文档、教程、食谱和示例都假设 Python 2 并使用

##### 新语言特性

本节概述了 Python 3 中一些在 Python 2 中*不*支持的特性。

###### 源代码编码和标识符

Python 3 假定源代码以 UTF-8 编码。此外，对标识符中允许使用的字符的规则也有所放宽。具体来说，标识符可以包含任何有效 Unicode 字符，其码位为 U+0080 或更高。例如：

```
π = 3.141592654
r = 4.0
print(2*π*r)
```

仅仅因为可以在源代码中使用这些字符，并不意味着这是一个好主意。并非所有编辑器、终端或开发工具都能很好地处理 Unicode。而且，强迫程序员输入标准键盘上不可见的笨拙按键序列来输入字符，会非常令人恼火（更不用说这可能会让办公室里的一些老资历黑客给大家讲一些有趣的 APL 故事了）。因此，最好将 Unicode 字符的使用仅限于注释和字符串字面量。

###### 集合字面量

现在可以通过将一组值用花括号括起来 `{ items }` 来定义集合。例如：

```
days = { 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun' }
```

这种语法与使用 `set()` 函数相同：

```
days = set(['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'])
```

###### 集合推导和字典推导

语法 `{ expr for x in s if conditional}` 是集合推导。它对集合 *s* 的所有元素应用一个操作，其使用方式与列表推导类似。例如：

```
>>> values = { 1, 2, 3, 4 }
>>> squares = {x*x for x in values}
>>> squares
{16, 1, 4, 9}
>>>
```

语法 `{ kexpr:vexpr for k,v in s if condition }` 是字典推导。它对序列 *s* 中的（`key`、`value`）元组的所有键和值依次应用一个操作，并返回一个字典。新字典的键由表达式 *kexpr* 描述，值由表达式 *vexpr* 描述。这可以看作是 `dict()` 函数的更强大版本。

为了说明，假设你有一个股票价格文件 `'prices.dat'`，内容如下：

```
GOOG 509.71
YHOO 28.34
IBM 106.11
MSFT 30.47
AAPL 122.13
```

以下是使用字典推导将该文件读取为股票名称到价格的映射字典的程序：

```
fields = (line.split() for line in open("prices.dat"))
prices = {sym:float(val) for sym,val in fields}
```

以下是将 prices 字典的所有键转换为小写的示例：

```
d = {sym.lower():price for sym,price in prices.items()}
```

以下是创建价格超过 $100.00 的股票价格字典的示例：

```
d = {sym:price for sym,price in prices.items() if price >= 100.0}
```

###### 扩展的可迭代对象解包

在 Python 2 中，可以使用如下语法将可迭代对象中的元素解包到变量中：

```
items = [1,2,3,4]
a,b,c,d = items       # 将元素解包到变量中
```

为了使这种解包生效，变量的数量与待解包的元素数量必须完全匹配。

在 Python 3 中，你可以使用通配符变量来仅解包序列中的部分元素，并将剩余的值放入一个列表中。例如：

```
a,*rest  = items    # a = 1, rest = [2,3,4]
a,*rest,d = items   # a = 1, rest = [2,3], d = 4
*rest, d = items    # rest = [1,2,3], d = 4
```

在这些示例中，以 * 为前缀的变量接收所有额外的值，并将它们放入一个列表中。如果没有额外的元素，该列表可能为空。此功能的一个用途是在遍历元组（或序列）列表时，其中的元组可能具有不同的大小。例如：

```
points = [ (1,2), (3,4,"red"), (4,5,"blue"), (6,7) ]
for x,y, *opt in points:
    if opt:
        # 发现了额外的字段
    statements
```

在任何展开中，带星号的变量最多只能出现一个。

###### 非局部变量

内部函数可以使用 nonlocal 声明来修改外部函数中的变量。例如：

```
def countdown(n):
    def decrement():
        nonlocal n
        n -= 1
    while n > 0:
        print("T-minus", n)
        decrement()
```

在 Python 2 中，内部函数可以读取外部函数中的变量，但不能修改它们。nonlocal 声明使这成为可能。

###### 函数注解

函数的参数和返回值可以用任意值进行注解。例如：

```
def foo(x:1,y:2) -> 3:
    pass
```

函数属性 \_\_annotations\_\_ 是一个将参数名称映射到注解值的字典。特殊的 'return' 键映射到返回值注解。例如：

```
>>> foo.__annotations__
{'y': 4, 'x': 3, 'return': 5}
>>>
```

解释器不会对这些注解附加任何特殊意义。实际上，它们可以是任何值。然而，预计类型信息在未来将会非常有用。例如，你可以这样写：

```
def foo(x:int, y:int) -> str:
    statements
```

注解不限于单个值。注解可以是任何有效的 Python 表达式。对于可变位置参数和关键字参数，同样适用此语法。例如：

```
def bar(x, *args:"additional", **kwargs:"options"):
    statements
``

同样，需要强调的是，Python 不会对注解附加任何特殊意义。其预期用途是在第三方库和框架中，这些库和框架可能希望将注解用于涉及元编程的各种应用。示例包括但不限于静态分析工具、文档、测试、函数重载、数据编组、远程过程调用、IDE、契约等。以下是使用装饰器函数对函数参数和返回值强制执行断言的示例：

```
def ensure(func):
    # 提取注解数据
    return_check = func.__annotations__.get('return',None)
    arg_checks   = [(name,func.__annotations__.get(name))
                    for name in func.__code__.co_varnames]

    # 创建一个包装器，使用注解中指定的函数
    # 来检查参数值和返回结果

    def assert_call(*args,**kwargs):
        for (name,check),value in zip(arg_checks,args):
            if check: assert check(value), "%s %s" % (name, check.__doc__)
        for name,check in arg_checks[len(args):]:
            if check: assert check(kwargs[name]), "%s %s" % (name, check.__doc__)
        result = func(*args,**kwargs)
        assert return_check(result), "return %s" % return_check.__doc__
        return result

    return assert_call
```

以下是使用上述装饰器的代码示例：

```
def positive(x):
    "must be positive"
    return x > 0

def negative(x):
    "must be negative"
    return x < 0

@ensure
def foo(a:positive, b:negative) -> positive:
    return a - b
```

以下是使用该函数的一些示例输出：

```
>>> foo(3,-2)
5
>>> foo(-5,2)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "meta.py", line 19, in call
    def assert_call(*args,**kwargs):
AssertionError: a must be positive
>>>
```

###### 仅关键字参数

函数可以指定仅关键字参数。这通过在第一个星号参数之后定义额外的参数来表示。例如：

```
def foo(x, *args, strict=False):
    statements
```

不兼容的编码惯例。不用说，如果一切看起来都是坏的，学习体验就不会好。甚至官方文档也没有完全跟上 Python 3 的编码要求；在撰写本书时，作者提交了大量关于文档错误和遗漏的 bug 报告。

最后，尽管 Python 3.0 被描述为最新且最强大的版本，但它存在许多性能和行为问题。例如，初始版本中的 I/O 系统表现出极其糟糕且不可接受的运行时性能。bytes 和 Unicode 的分离也不是没有问题的。甚至一些内置库模块也由于与 I/O 和字符串处理相关的更改而损坏。显然，随着更多程序员对发布版本进行压力测试，这些问题会随着时间的推移而改善。然而，在作者看来，Python 3.0 实际上只适合经验丰富的 Python 老手进行实验性使用。如果你追求稳定性和生产级代码，在 Python 3 系列的一些问题得到解决之前，请坚持使用 Python 2。



###### 省略号作为表达式

调用此函数时，`strict` 参数只能作为关键字参数指定。例如：

```python
a = foo(1, strict=True)
```

任何额外的位置参数只会被放入 `args` 中，而不会用于设置 `strict` 的值。如果您不想接受可变数量的参数，而只想使用仅限关键字的参数，请在参数列表中使用裸露的 `*`。例如：

```python
def foo(x, *, strict=False):
    statements
```

以下是使用示例：

```python
foo(1,True)       # 失败。TypeError: foo() takes 1 positional argument
foo(1,strict=True) # 成功。
```

`Ellipsis` 对象（`...`）现在可以作为表达式出现。这允许它被放置在容器中并赋值给变量。例如：

```python
>>> x = ...       # Ellipsis 的赋值
>>> x
Ellipsis
>>> a = [1,2,...]
>>> a
[1, 2, Ellipsis]
>>> ... in a
True
>>> x is ...
True
>>>
```

省略号的解释仍然留由使用它的应用程序决定。此特性允许 `...` 作为库和框架中一种有趣的语法使用（例如，表示通配符、延续或某些类似概念）。

###### 链式异常

异常现在可以链接在一起。这本质上是一种让当前异常携带有关先前异常信息的方式。`from` 限定符与 `raise` 语句一起使用，以显式地链接异常。例如：

```python
try:
    statements
except ValueError as e:
    raise SyntaxError("Couldn't parse configuration") from e
```

当 `SyntaxError` 异常被引发时，将生成如下所示的跟踪消息——显示两个异常：

```python
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
ValueError: invalid literal for int() with base 10: 'nine'

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
SyntaxError: Couldn't parse configuration
```

异常对象具有 `__cause__` 属性，该属性被设置为先前的异常。在 `raise` 中使用 `from` 限定符会设置此属性。

一个更微妙的异常链示例涉及在另一个异常处理程序内引发的异常。例如：

```python
def error(msg):
    print(m)        # 注意：此处为故意拼写错误（m 未定义）

try:
    statements
except ValueError as e:
    error("Couldn't parse configuration")
```

如果您在 Python 2 中尝试此操作，您只会得到一个与 `error()` 中的 `NameError` 相关的异常。在 Python 3 中，正在处理的先前异常会与结果链接在一起。例如，您会得到此消息：

```python
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
ValueError: invalid literal for int() with base 10: 'nine'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
  File "<stdin>", line 2, in error
NameError: global name 'm' is not defined
```

对于隐式链接，异常实例 `e` 的 `__context__` 属性包含对先前异常的引用。

###### 改进的 `super()`

用于在基类中查找方法的 `super()` 函数，在 Python 3 中可以不带任何参数使用。例如：

```python
class C(A,B):
    def bar(self):
        return super().bar()    # 在基类中调用 bar()
```

在 Python 2 中，您必须使用 `super(C,self).bar()`。旧语法仍然支持，但明显更笨重。

###### 高级元类

在 Python 2 中，您可以定义改变类行为的元类。实现的一个微妙之处是，元类执行的处理仅发生在*类体执行之后*。也就是说，解释器执行类的整个体并填充一个字典。一旦字典被填充，该字典就会被传递给元类构造函数（在类体执行之后）。

在 Python 3 中，元类还可以在类体执行*之前*执行额外的工作。这是通过在元类中定义一个名为 `__prepare__(cls, name, bases, **kwargs)` 的特殊类方法来完成的。此方法必须返回一个字典作为结果。当类定义的体执行时，此字典会被填充。下面是一个概述基本过程的示例：

```python
class MyMeta(type):
    @classmethod
    def __prepare__(cls,name,bases,**kwargs):
        print("preparing",name,bases,kwargs)
        return {}
    def __new__(cls,name,bases,classdict):
        print("creating",name,bases,classdict)
        return type.__new__(cls,name,bases,classdict)
```

Python 3 使用替代语法来指定元类。例如，要定义一个使用 MyMeta 的类，您可以使用：

```python
class Foo(metaclass=MyMeta):
    print("About to define methods")
    def __init__(self):
        pass
    def bar(self):
        pass
print("Done defining methods")
```

如果运行以下代码，您将看到如下输出，它说明了控制流：

```python
preparing Foo () {}
About to define methods
Done defining methods
creating Foo () {'__module__': '__main__',
                     'bar': <function bar at 0x3845d0>,
                     '__init__': <function __init__ at 0x384588>}
```

元类的 `__prepare__()` 方法上的附加关键字参数是从 `class` 语句的基类列表中使用的关键字参数传递的。例如，语句 `class Foo(metaclass=MyMeta,spam=42,blah="Hello")` 将关键字参数 spam 和 blah 传递给 `MyMeta.__prepare__()`。此约定可用于将任意配置信息传递给元类。

要使用元类的新 `__prepare__()` 方法执行任何类型的有用处理，通常需要该方法返回一个自定义的字典对象。例如，如果您想在类定义时执行特殊处理，您可以定义一个继承自 `dict` 并重新实现 `__setitem__()` 方法的类，以捕获对类字典的赋值。以下示例通过定义一个元类来说明这一点，如果任何方法或类变量被多重定义，该元类会报告错误。

```python
class MultipleDef(dict):
    def __init__(self):
        self.multiple= set()
    def __setitem__(self,name,value):
        if name in self:
            self.multiple.add(name)
        dict.__setitem__(self,name,value)

class MultiMeta(type):
    @classmethod
    def __prepare__(cls,name,bases,**kwargs):
        return MultipleDef()
    def __new__(cls,name,bases,classdict):
        for name in classdict.multiple:
            print(name,"multiply defined")
        if classdict.multiple:
            raise TypeError("Multiple definitions exist")
        return type.__new__(cls,name,bases,classdict)
```

如果您将此元类应用于另一个类定义，如果任何方法被重定义，它将报告错误。例如：

```python
class Foo(metaclass=MultiMeta):
    def __init__(self):
        pass
    def __init__(self,x):      # 错误。__init__ 被多重定义。
        pass
```

##### 常见陷阱

如果您正从 Python 2 迁移到 Python 3，请注意 Python 3 不仅仅是新的语法和语言特性。核心语言和库的大部分已经以有时很微妙的方式进行了重新设计。Python 3 的某些方面在 Python 2 程序员看来可能像 bug。在其他情况下，Python 2 中曾经“容易”的事情现在被禁止了。

本节概述了从 Python 2 切换过来的程序员可能遇到的一些最重要的陷阱。

##### 文本与字节

Python 3 对文本字符串（字符）和二进制数据（字节）进行了非常严格的区分。像 `"hello"` 这样的字面量表示存储为 Unicode 的文本字符串，而 `b"hello"` 表示一个字节字符串（在这种情况下包含 ASCII 字母）。

在任何情况下，`str` 和 `bytes` 类型都不能在 Python 3 中混合使用。例如，如果您尝试将字符串和字节连接在一起，您将得到一个 `TypeError` 异常。这与 Python 2 不同，在 Python 2 中，字节字符串会根据需要自动强制转换为 Unicode。

要将文本字符串 *s* 转换为字节，您必须使用 `s.encode(encoding)`。例如，`s.encode('utf-8')` 将 *s* 转换为 UTF-8 编码的字节字符串。要将字节字符串 *t* 转换回文本，您必须使用 `t.decode(encoding)`。您可以将 `encode()` 和 `decode()` 方法视为字符串和字节之间的一种“类型转换”。

保持文本和字节之间的清晰分离最终是一件好事——在 Python 2 中混合字符串类型的规则充其量是晦涩难懂的。然而，Python 3 方法的一个后果是，字节字符串在实际上表现得像“文本”的能力方面受到了更大的限制。尽管有标准的字符串方法，如 `split()` 和 `replace()`，但字节字符串的其他方面与 Python 2 不同。例如，如果您打印一个字节字符串，您只会得到它的 `repr()` 输出，带有引号，如 `b'contents'`。类似地，没有一种字符串格式化操作（`%`、`.format()`）有效。例如：

```python
x = b'Hello World'
print(x)                     # 产生 b'Hello World'
print(b"You said '%s'" % x)  # TypeError: 不支持 % 运算符
```

字节失去类似文本的行为对系统程序员来说是一个潜在的陷阱。尽管 Unicode 无处不在，但在许多情况下，您实际上确实想要

## 附录 Python 3

处理与操作面向字节的数据（如 ASCII）。你可能倾向于使用 `bytes` 类型来避免 Unicode 所有开销和复杂性。然而，这实际上会使所有与面向字节文本处理相关的事情变得更加困难。以下示例说明了潜在问题：

```python
>>> # 使用字符串（Unicode）创建响应消息
>>> status = 200
>>> msg = "OK"
>>> proto = "HTTP/1.0"
>>> response = "%s %d %s" % (proto, status, msg)
>>> print(response)
HTTP/1.0 200 OK

>>> # 仅使用字节（ASCII）创建响应消息
>>> status = 200
>>> msg = b"OK"
>>> proto = b"HTTP/1.0"
>>> response = b"%s %d %s" % (proto, status, msg)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for %: 'bytes' and 'tuple'

>>> response = proto + b" " + str(status) + b" " + msg
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can't concat bytes to str

>>> bytes(status)
b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00....'

>>> bytes(str(status))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: string argument without an encoding

>>> bytes(str(status), 'ascii')
b'200'

>>> response = proto + b" " + bytes(str(status), 'ascii') + b" " + msg
>>> print(response)
b'HTTP/1.0 200 OK'

>>> print(response.decode('ascii'))
HTTP/1.0 200 OK
>>>
```

在此示例中，你可以看到 Python 3 如何严格强制执行文本/字节分离。即使是看似简单的操作，如将整数转换为 ASCII 字符，在使用字节时也会复杂得多。

关键在于，如果你执行任何基于文本的处理或格式化，你*总是*最好使用标准文本字符串。如果你需要在此类处理完成后获得字节字符串，可以使用 `s.encode('latin-1')` 从 Unicode 转换。

在使用各种库模块时，文本/字节的区别更为微妙。有些库可以同等良好地处理文本或字节，而有些则完全禁止字节。在其他情况下，行为会因接收到的输入类型而异。例如，`os.listdir(dirname)` 函数仅在 `dirname` 是字符串时返回可成功解码为 Unicode 的文件名。如果 `dirname` 是字节字符串，则*所有*文件名都以字节字符串形式返回。

#### 新 I/O 系统

Python 3 实现了全新的 I/O 系统，其细节在第 19 章“操作系统服务”的 `io` 模块部分中描述。新 I/O 系统也反映了字符串中存在的文本与二进制数据之间的显著区别。

如果你执行任何类型的文本 I/O，Python 3 强制你以“文本模式”打开文件，并在需要非默认编码（通常为 UTF-8）时提供可选的编码参数。如果你执行二进制数据的 I/O，必须以“二进制模式”打开文件并使用字节字符串。一个常见错误来源是将以错误模式打开的文件或 I/O 流传递输出数据。例如：

```python
>>> f = open("foo.txt", "wb")
>>> f.write("Hello write")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/tmp/lib/python3.0/io.py", line 1035, in write
    raise TypeError("can't write str to binary stream")
TypeError: can't write str to binary stream
>>>
```

套接字、管道和其他类型的 I/O 通道应始终假定为二进制模式。特别是网络代码的一个潜在问题是，许多网络协议涉及基于文本的请求/响应处理（例如 HTTP、SMTP、FTP 等）。鉴于套接字是二进制的，这种二进制 I/O 与文本处理的混合可能导致前一节描述的与混合文本和字节相关的一些问题。你需要小心。

##### `print()` 和 `exec()` 函数

Python 2 中的 `print` 和 `exec` 语句现在是函数。`print()` 函数与其 Python 2 对应物的使用方式如下：

```python
print(x, y, z)           # 等同于：print x, y, z
print(x, y, z, end=' ')  # 等同于：print x, y, z,
print(a, file=f)         # 等同于：print >>f, a
```

`print()` 是函数的事实意味着如果你愿意，可以用替代定义替换它。

`exec()` 现在也是一个函数，但它在 Python 3 中的行为与 Python 2 中有微妙不同。例如，考虑这段代码：

```python
def foo():
    exec("a = 42")
    print(a)
```

在 Python 2 中，调用 `foo()` 将打印数字 `'42'`。在 Python 3 中，你会得到一个 `NameError` 异常，变量 `a` 未定义。这里发生的是，`exec()` 作为函数，仅操作 `globals()` 和 `locals()` 函数返回的字典。然而，`locals()` 返回的字典实际上是局部变量的一个*副本*。在 `exec()` 函数中进行的赋值仅修改了这个局部变量的副本，而不是局部变量本身。以下是解决方法之一：

```python
def foo():
    _locals = locals()
    exec("a = 42", globals(), _locals)
    a = _locals['a']      # 提取设置的变量
    print(a)
```

作为一般规则，不要期望 Python 3 支持与 Python 2 中使用 `exec()`、`eval()` 和 `execfile()` 相同程度的“魔法”。实际上，`execfile()` 已完全移除（你可以通过将一个打开的类似文件的对象传递给 `exec()` 来模拟其功能）。

##### 迭代器和视图的使用

Python 3 比 Python 2 更多地使用迭代器和生成器。以前返回列表的内置函数，如 `zip()`、`map()` 和 `range()`，现在返回可迭代对象。如果你需要从结果创建列表，请使用 `list()` 函数。

Python 3 对从字典中提取键和值信息采用了略有不同的方法。在 Python 2 中，你可以使用 `d.keys()`、`d.values()` 或 `d.items()` 等方法分别获取键、值或键/值对的列表。在 Python 3 中，这些方法返回所谓的*视图*对象。例如：

```python
>>> s = { 'GOOG': 490.10, 'AAPL': 123.45, 'IBM': 91.10 }
>>> k = s.keys()
>>> k
dict_keys(['GOOG', 'AAPL', 'IBM'])
>>> v = s.values()
>>> v
dict_values([490.1, 123.45, 91.1])
>>>
```

这些对象支持迭代，因此如果你想查看内容，可以使用 `for` 循环。例如：

```python
>>> for x in k:
...     print(x)
...
GOOG
AAPL
IBM
>>>
```

视图对象始终绑定回创建它们的字典。一个微妙之处在于，如果底层字典发生变化，视图产生的项目也会变化。例如：

```python
>>> s['ACME'] = 5612.25
>>> for x in k:
...     print(x)
...
GOOG
AAPL
IBM
ACME
>>>
```

如果需要构建字典键或值的列表，只需使用 `list()` 函数——例如，`list(s.keys())`。

##### 整数和整数除法

Python 3 不再为 32 位整数提供 `int` 类型，也不再为长整数提供单独的 `long` 类型。`int` 类型现在表示任意精度的整数（其内部细节不向用户公开）。

此外，整数除法现在总是产生浮点数结果。例如，`3/5` 是 `0.6`，而不是 `0`。即使结果本应是整数，也会转换为浮点数。例如，`8/2` 是 `4.0`，而不是 `4`。

##### 比较

Python 3 对于值的比较方式更为严格。在 Python 2 中，即使没有意义，任何两个对象也可以进行比较。例如：

```python
>>> 3 < "Hello"
True
>>>
```

在 Python 3 中，这会导致 `TypeError`。例如：

```python
>>> 3 < "Hello"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unorderable types: int() < str()
>>>
```

此更改是次要的，但它意味着在 Python 3 中，你必须更加小心确保数据具有适当的类型。例如，如果你使用列表的 `sort()` 方法，列表中的所有项必须与 `<` 运算符兼容，否则你会得到错误。在 Python 2 中，操作无论如何都会静默执行，通常产生无意义的结果。

##### 迭代器和生成器

Python 3 对迭代器协议进行了轻微更改。不是调用 `__iter__()` 和 `next()` 方法来执行迭代，而是将 `next()` 方法重命名为 `__next__()`。大多数用户不会受到此更改的影响，除非你编写了手动迭代可迭代对象的代码或定义了自定义迭代器对象。你需要确保更改类中 `next()` 方法的名称。使用内置的 `next()` 函数以可移植方式调用迭代器的 `next()` 或 `__next__()` 方法。

##### 文件名、参数和环境变量

在 Python 3 中，文件名、`sys.argv` 中的命令行参数以及 `os.environ` 中的环境变量可能会根据本地设置被视为 Unicode，也可能不会。唯一的问题是，在操作系统环境中使用 Unicode 并非完全通用。例如，在许多系统上，指定文件名、命令行选项和环境变量（它们只是与有效 Unicode 编码不对应的原始字节序列）在技术上可能是可行的。尽管这些情况在实践中可能很少见，但对于使用 Python 执行与系统管理相关任务的编程来说可能值得关注。在这种情况下，将文件和目录名作为字节字符串提供将解决许多问题。例如，`os.listdir(b'/foo')`。



##### 库重组

Python 3 重新组织并更改了标准库中几个部分的名称，最显著的是与网络和互联网数据格式相关的模块。此外，各种遗留模块已从库中移除（例如 gopherlib、rfc822 等）。

现在，使用小写名称作为模块名称是标准做法。几个模块如 `ConfigParser`、`Queue` 和 `SocketServer` 已分别重命名为 `configparser`、`queue` 和 `socketserver`。你应该尝试在自己的代码中遵循类似的约定。

包的创建旨在重组以前分散在不同模块中的代码——例如，包含用于编写 HTTP 服务器所有模块的 `http` 包，包含用于解析 HTML 模块的 `html` 包，包含用于 XML-RPC 模块的 `xmlrpc` 包，等等。

至于已弃用的模块，本书已谨慎地只记录在 Python 2.6 和 Python 3.0 中当前使用的模块。如果你正在使用现有的 Python 2 代码，并且看到它使用了本文档中未记录的模块，那么该模块很可能已被弃用，转而使用更现代的替代品。仅举一个例子，Python 3 没有 Python 2 中常用于启动子进程的 `popen2` 模块。相反，你应该使用 `subprocess` 模块。

##### 绝对导入

与库重组相关，包子模块中出现的所有 `import` 语句都使用绝对名称。这在第 8 章“模块、包和分发”中有更详细的介绍，但假设你有一个如下组织的包：

```
foo/
  __init__.py
  spam.py
  bar.py
```

如果文件 `spam.py` 使用语句 `import bar`，即使 `bar.py` 位于同一目录中，你也会得到 `ImportError` 异常。要加载这个子模块，`spam.py` 需要使用 `import foo.bar` 或包相对导入，如 `from . import bar`。

这与 Python 2 不同，在 Python 2 中，`import` 在检查 `sys.path` 中的其他目录之前，总是先检查当前目录是否有匹配项。

#### 代码迁移和 2to3

将代码从 Python 2 转换到 Python 3 是一个微妙的话题。为了绝对明确，没有任何神奇的导入、标志、环境变量或工具能让 Python 3 运行任意的 Python 2 程序。但是，可以采取一些非常具体的步骤来迁移代码，现在将逐一描述。

##### 将代码移植到 Python 2.6

建议任何将代码移植到 Python 3 的人首先将其移植到 Python 2.6。Python 2.6 不仅与 Python 2.5 向后兼容，而且还支持 Python 3 中一些新功能的子集。示例包括高级字符串格式化、新的异常语法、字节字面量、I/O 库和抽象基类。因此，即使尚未准备好进行全面迁移，Python 2 程序现在也可以开始利用有用的 Python 3 特性。

移植到 Python 2.6 的另一个原因是，如果你使用 -3 命令行选项运行 Python 2.6，它会为已弃用的功能发出警告消息。例如：

```
bash-3.2$ python -3
Python 2.6 (trunk:66714:66715M, Oct  1 2008, 18:36:04)
[GCC 4.0.1 (Apple Computer, Inc. build 5370)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> a = { }
>>> a.has_key('foo')
__main__:1: DeprecationWarning: dict.has_key() not supported in 3.x; use the in
operator
False
>>
```

使用这些警告消息作为指南，你应该非常小心，确保你的程序在 Python 2.6 上无警告地运行，然后再继续移植到 Python 3。

###### 提供测试覆盖

Python 有有用的测试模块，包括 doctest 和 unittest。在尝试移植到 Python 3 之前，请确保你的应用程序有全面的测试覆盖。如果你的程序到目前为止没有任何测试，那么现在是开始的好时机。你需要确保你的测试尽可能全面，并且所有测试在 Python 2.6 上运行时都能通过，没有任何警告消息。

###### 使用 2to3 工具

Python 3 包含一个名为 2to3 的工具，可以帮助将代码从 Python 2.6 迁移到 Python 3。该工具通常位于 Python 源代码分发包的 Tools/scripts 目录中，也安装在大多数系统上 python3.0 二进制文件所在的同一目录中。它是一个命令行工具，通常从 UNIX 或 Windows 命令 shell 运行。

例如，考虑以下包含一些已弃用特性的程序。

```
####### example.py
import ConfigParser

for i in xrange(10):
    print i, 2*i

def spam(d):
    if not d.has_key("spam"):
        d["spam"] = load_spam()
    return d["spam"]
```

要在该程序上运行 2to3，请输入“2to3 example.py”。例如：

```
% 2to3 example.py
RefactoringTool: Skipping implicit fixer: buffer
RefactoringTool: Skipping implicit fixer: idioms
RefactoringTool: Skipping implicit fixer: set_literal
RefactoringTool: Skipping implicit fixer: ws_comma
--- example.py (original)
+++ example.py (refactored)
@@ -1,10 +1,10 @@
####### example.py
-import ConfigParser
+import configparser

-for i in xrange(10):
-    print i, 2*i
+for i in range(10):
+    print(i, 2*i)

def spam(d):
-    if not d.has_key("spam"):
+    if "spam" not in d:
        d["spam"] = load_spam()
    return d["spam"]
RefactoringTool: Files that need to be modified:
RefactoringTool: example.py
```

作为输出，`2to3` 会识别它认为有问题且可能需要更改的程序部分。这些以上下文差异的形式显示在输出中。虽然我们在单个文件上使用了 `2to3`，但如果你给它一个目录名，它会递归地查找该目录结构中包含的所有 Python 文件，并为所有文件生成报告。

默认情况下，`2to3` 实际上并不修复它扫描的任何源代码——它只是报告可能需要更改的代码部分。`2to3` 面临的一个挑战是，它通常只有不完整的信息。例如，考虑示例代码中的 `spam()` 函数。该函数调用了方法 `d.has_key()`。对于字典，`has_key()` 已被移除，取而代之的是 `in` 运算符。`2to3` 报告了这个更改，但在没有更多信息的情况下，不清楚 `spam()` 是否实际操作字典。也可能是 `d` 是某种其他类型的对象（也许是数据库），它恰好提供了 `has_key()` 方法，但使用 `in` 运算符会失败。`2to3` 的另一个问题领域是字节字符串和 Unicode 的处理。鉴于 Python 2 会自动将字节字符串提升为 Unicode，因此看到代码粗心地混合这两种字符串类型的情况并不少见。不幸的是，`2to3` 无法解决所有这些问题。这就是为什么拥有良好的单元测试覆盖很重要的原因之一。当然，这一切都取决于应用程序。

作为选项，可以指示 `2to3` 修复选定的不兼容性。首先，可以通过输入 `2to3 -l` 获得“修复器”列表。例如：

```
% 2to3 -l
Available transformations for the -f/--fix option:
apply
basestring
buffer
callable
...
xrange
xreadlines
zip
```

使用此列表中的名称，你可以通过简单地输入“`2to3 -f fixname filename`”来查看选定的修复实际会更改什么。如果你想应用多个修复，只需为每个修复指定一个单独的 `-f` 选项。如果你确实想将修复应用于源文件，请添加 `-w` 选项，如 `2to3 -f fixname -w filename`。这里有一个例子：

```
% 2to3 -f xrange -w example.py
--- example.py (original)
+++ example.py (refactored)
@@ -1,7 +1,7 @@
####### example.py
import ConfigParser

-for i in xrange(10):
+for i in range(10):
    print i, 2*i

def spam(d):
```

RefactoringTool: Files that were modified:
RefactoringTool: example.py

如果你在此操作后查看 `example.py`，你会发现 `xrange()` 已更改为 `range()`，并且没有进行其他更改。原始 `example.py` 文件的备份可以在 `example.py.bak` 中找到。

`-f` 选项的对应选项是 `-x` 选项。如果你使用 `2to3 -x fixname filename`，它将运行所有修复器，除了你用 `-x` 选项列出的那些。

虽然可以指示 `2to3` 修复所有内容并覆盖所有文件，但这在实践中最好避免。请记住，代码转换是一门不精确的科学，`2to3` 并不总是会做“正确的事情”。与寄希望于一切都能神奇地“奏效”相比，以有条理、有计划的方式处理代码迁移总是更好的。

`2to3` 还有一些可能有用的其他选项。`-v` 选项启用详细模式，打印可能对调试有用的额外信息。`-p` 选项告诉 `2to3` 你已经在代码中将 `print` 语句作为函数使用，因此不应转换它（通过 `from __future__ import print_statement` 语句启用）。

##### 实用的移植策略

以下是将 Python 2 代码移植到 Python 3 的实用策略。再次强调，最好以有条理的方式进行迁移，而不是一次性完成所有事情。

1.  确保你的代码有足够的单元测试套件，并且所有测试在 Python 2 下通过。
2.  将你的代码和测试套件移植到 Python 2.6，并确保所有测试仍然通过。
3.  打开 Python 2.6 的 `-3` 选项。解决所有警告消息，确保你的程序在没有任何警告消息的情况下运行并通过对所有测试。如果你正确地完成了这些，你的代码很可能仍然可以在 Python 2.5 甚至更早的版本上运行。你实际上只是在清理程序中积累的一些糟粕。
4.  备份你的代码（这是不言而喻的）。
5.  将单元测试套件移植到 Python 3，并确保测试环境本身正常工作。单个单元测试本身会失败（因为你尚未移植任何代码）。但是，编写良好的测试套件应该能够在测试软件本身不发生内部崩溃的情况下处理测试失败。



###### 6. 使用 `2to3` 将程序本身转换为 Python 3。在生成的代码上运行单元测试套件，并修复所有出现的问题。为此有多种策略。如果你感觉幸运，你总是可以告诉 `2to3` 直接修复所有问题，看看会发生什么。如果你更谨慎一些，你可以先让 `2to3` 修复那些真正明显的问题（`print` 语句、`except` 语句、`xrange()`、库模块名称等），然后以一种更零敲碎打的方式处理剩余的问题。

到这个过程结束时，你的代码应该通过所有单元测试，并以与之前相同的方式运行。

从理论上讲，有可能以一种方式构建代码，使其既能在 Python 2.6 中运行，又能无需任何用户干预自动翻译到 Python 3。然而，这将需要非常严格地遵守现代 Python 编码规范——至少你绝对需要确保 Python 2.6 中没有警告。如果自动翻译过程需要非常特定地使用 `2to3`（例如只运行一组选定的修复程序），你可能应该编写一个 shell 脚本来自动执行所需的操作，而不是要求用户自己运行 `2to3`。

#### 同时支持 Python 2 和 Python 3

关于 Python 3 迁移的最后一个问题是，是否有可能拥有一个*单一*代码库，使其无需修改即可在 Python 2 和 Python 3 上工作。虽然在某些情况下这是可能的，但生成的代码有变成一团糟的风险。例如，你将必须避免所有 `print` 语句，并确保所有 `except` 子句都不接受任何异常值（而是从 `sys.exc_info()` 中提取它们）。其他 Python 特性根本无法使其工作。例如，由于语法差异，没有任何方法可以以一种在 Python 2 和 Python 3 之间可移植的方式使用元类。

因此，如果你维护的代码必须在 Python 2 和 3 上工作，你最好的选择是确保你的代码尽可能干净，并在 Python 2.6 下运行，确保你有一个单元测试套件，并尝试开发一组 `2to3` 修复程序以使自动翻译成为可能。

有一个案例可能适合拥有单一代码库，那就是单元测试。一个无需修改即可在 Python 2.6 和 Python 3 上运行的测试套件，在验证应用程序经 `2to3` 翻译后行为正确性方面可能很有用。

#### 参与贡献

作为一个开源项目，Python 持续在用户的贡献下发展。对于 Python 3，特别是，报告错误、性能问题和其他问题至关重要。要报告错误，请访问 http://bugs.python.org。不要害羞——你的反馈使 Python 对每个人来说都更好。

### 索引

#### 符号与数字

- ! 调试器命令，pdb 模块，187
- != 不等于运算符，66
- ' 单引号，11，27
- ''' 三重引号，11，27
- " 双引号，11，27
- """ 三重引号，11，27
- # 注释，6，26
- #! 在 Unix shell 脚本中，6，176
    - 在包安装时重写，153
- % 取模运算符，65
- % 字符串格式化运算符，8，70，162
- %= 运算符，75
- & 按位与运算符，65
- & 集合交集运算符，15，75
- &= 运算符，75
- () 函数调用运算符，76
- () 元组，14，29
- * 仅关键字参数，Python 3，625
- * 乘法运算符，65
- * 将序列作为函数参数传递，94
- * 序列重复运算符，67
- * 函数定义中的可变参数，94
- * 通配符
    - from module import，24，145
    - Python 3 中的可迭代解包，623
- ** 将字典作为关键字参数传递，95
- ** 幂运算符，65
- ** 函数定义中的可变关键字参数，95
- **= 运算符，75
- *= 运算符，75
- + 加法运算符，65
- + 列表连接运算符，12
- + 序列连接运算符，67
- + 字符串连接运算符，11
- + 一元加运算符，65
- += 运算符，75
- - 连字符，用作文件名，174
- - 集合差集运算符，15，75
- - 减法运算符，65
- - 一元减运算符，65
- -*- coding: 注释，在源代码中，31
- -= 运算符，75
- . 属性绑定运算符，33，48，76，118
    - 与模块，51
    - 特殊方法，57
- . 相对导入语句中的目录引用，150
- ... Ellipsis，30，54，59
- ... 解释器提示符，175
- / 除法运算符，65
- // 截断除法运算符，65
- //= 运算符，75
- /= 运算符，75
- : 字符串格式说明符中的冒号，72
- ; 分号，7，26
- < 字符串格式说明符中的左对齐，73
- < 小于运算符，66
- << 左移运算符，65
- <<= 运算符，75
- <= 小于或等于运算符，66
- == 等于运算符，66，78
- > 大于运算符，66
- > 字符串格式说明符中的右对齐，73
- >= 大于或等于运算符，66
- >> print 的文件重定向修饰符，10，163
- >> 右移运算符，65
- >>= 运算符，75
- >>> 解释器提示符，5，175
- @ 装饰器，30，101
- [::] 扩展切片运算符，39-40，67-68
- [:] 切片运算符，39-40，67-68
- [] 索引运算符，39-40，67
    - 与特殊方法，58
    - 在映射上，45
    - 在序列上，68
- [] 列表，12，29
- \ 续行符，9，25，29
- \ 字符串转义码，27
- ^ 按位异或运算符，65
- ^ 字符串格式说明符中的居中对齐，73
- ^ 集合对称差集运算符，15，75
- ^= 运算符，75
- _ 变量，交互模式，6，176
- {} 字典，16，29
- {} 格式字符串中的占位符，72
- {} 集合字面量，Python 3，622
- | 按位或运算符，65
- | 集合并集运算符，15，75
- |= 运算符，75
- ~ 按位取反运算符，65
- ~ 展开文件名中的用户主目录，397
- $ 字符串中的变量，72
- 0b 二进制整数字面量，27
- 0o 八进制整数字面量，27
- 0x 十六进制整数字面量，27
- 2 的补码与整数，66
- 2to3 工具，635-637
    - 局限性，636
- -3 命令行选项，173，635

#### A

- 'a' 模式，open() 函数，159
- a(args) 调试器命令，pdb 模块，187
- a2b_base64() 函数，binascii 模块，547
- a2b_hex() 函数，binascii 模块，548
- a2b_hqx() 函数，binascii 模块，548
- a2b_uu() 函数，binascii 模块，547
- abc 模块，136，257
- ABCMeta 元类，136，257
- abort() 函数，os 模块，390
- abort() 方法，FTP 对象，497
- abs() 函数，66，201
    - operator 模块，273
- __abs__() 方法，61
- 绝对导入，151
    - Python 3，634
    - 与相对导入比较，151
- 绝对值，66
- abspath() 函数，os.path 模块，396
- 抽象基类，34，136，257
    - 在子类中调用方法，137
    - 执行的检查，137
    - 容器对象，265
    - 实例化时的错误，137
    - 示例，258
    - 文件和 I/O，354
    - 数值类型，253
    - 注册预先存在的类，137
    - 特殊方法，57
- @abstractmethod 装饰器，136-137，257-258
- __abstractmethods__ 属性，类型，50
- @abstractproperty 装饰器，136-137，257-258
- accept() 方法
    - Listener 对象，433
    - dispatcher 对象，456
    - socket 对象，478
- accept2dyear 变量，time 模块，405
- 访问控制说明符，缺乏，127
- access() 函数，os 模块，386
- acos() 函数，math 模块，251
- acosh() 函数，math 模块，251
- acquire() 方法
    - Condition 对象，441
    - Lock 对象，438
    - RLock 对象，438
    - Semaphore 对象，439
- activate() 方法，SocketServer 类，493
- active_children() 函数，multiprocessing 模块，434
- active_count() 函数，threading 模块，443
- ActivePython，5
- add() 函数，operator 模块，273
- add() 方法
    - TarFile 对象，320
    - 集合，15，46
- __add__() 方法，60
- add_data() 方法，Request 对象，516
- add_header() 方法
    - Message 对象，555
    - Request 对象，516
- add_option() 方法，OptionParser 对象，158，375
- add_password() 方法，AuthHandler 对象，519
- add_section() 方法，ConfigParser 对象，332
- add_type() 函数，mimetypes 模块，567
- add_unredirected_header() 方法，Request 对象，517
- addfile() 方法，TarFile 对象，320
- addFilter() 方法
    - Handler 对象，364
    - Logger 对象，359
- addHandler() 方法，Logger 对象，361
- 加法运算符 +，65
- addLevelName() 函数，logging 模块，366
- address 属性
    - BaseManager 对象，431
    - Listener 对象，433
- 地址族，socket，470
- address_family 属性，SocketServer 类，492
- 地址，网络，471
- addressof() 函数，ctypes 模块，617
- 相邻字符串字面量，连接，27
- adler32() 函数，zlib 模块，328
- 高级字符串格式化，8，42，72
- AF_* 常量，socket 模块，470
- aifc 模块，588
- aio_* 系统调用族，缺乏，469
- AJAX，示例，531
- alarm() 函数，signal 模块，399
- 警报，399
- alias 调试器命令，pdb 模块，187
- alignment() 函数，ctypes 模块，617
- __all__ 变量
    - 与 import 语句，145
    - 在包中，150
- all() 函数，40，67，201
- allow_reuse_address 属性，SocketServer 类，492
- altsep 变量，os 模块，386
- altzone 变量，time 模块，405
- and 运算符，布尔表达式，9，77
- and_() 函数，operator 模块，274
- __and__() 方法，60
- __annotations__ 属性，函数，624
- 匿名函数，112
- any() 函数，40，67，201
- anydbm 模块，310
- api_version 变量，sys 模块，229
- %APPDATA% 环境变量，Windows，177

如何使此索引更有用？请通过 indexes@samspublishing.com 联系我们



642 append() 方法

- append() 方法
  - Element 对象的方法, 576
  - 数组对象的方法, 259
  - deque 对象的方法, 262
  - 列表的方法, 12, 40
- appendChild() 方法, DOM Node 对象的方法, 571
- appendleft() 方法, deque 对象的方法, 262
- 应用程序日志, 355
- 应用程序, WSGI, 540
- 应用顺序求值, 76
- apply() 方法, Pool 对象的方法, 424
- apply_async() 方法, Pool 对象的方法, 424
- args 属性
  - Exception 对象的属性, 213
  - 异常的属性, 88
  - partial 对象的属性, 268
- argtypes 属性, ctypes 函数对象的属性, 613
- argv 变量, sys 模块, 13, 157, 174, 229
- ArithmeticError 异常, 87, 212
- array 模块, 259
- Array() 函数, multiprocessing 模块, 426
- Array() 方法, Manager 对象的方法, 428
- array() 函数, array 模块, 259
- 数组, 从统一类型创建, 259
- arraysize 属性, Cursor 对象的属性, 299
- as 限定符
  - except 语句中的, 22, 85
  - from-import 语句中的, 145
  - import 语句中的, 24, 144
  - with 语句中的, 62, 90
- as_integer_ratio() 方法, 浮点数的方法, 39
- as_string() 方法, Message 对象的方法, 555
- ascii 编码, 描述, 169
- ascii() 函数, 201
  - 与 Python 3, 201
  - future_builtins 模块, 217
- ASCII, 与 UTF-8 的兼容性, 170

- ascii_letters 变量, string 模块, 287
- ascii_lowercase 变量, string 模块, 287
- ascii_uppercase 变量, string 模块, 287
- asctime() 函数, time 模块, 405
- asin() 函数, math 模块, 251
- asinh() 函数, math 模块, 251
- assert 语句, 91
- assert_() 方法, TestCase 对象的方法, 185
- assertAlmostEqual() 方法, TestCase 对象的方法, 185
- assertEqual() 方法, TestCase 对象的方法, 185
- AssertionError 异常, 87, 91, 213
- 断言, 91
  - 使用 -O 选项剥离, 148
- assertNotAlmostEqual() 方法, TestCase 对象的方法, 185
- assertNotEqual() 方法, TestCase 对象的方法, 185
- assertRaises() 方法, TestCase 对象的方法, 185
- 赋值
  - 与引用计数, 34
  - 增强赋值, 61
  - 就地操作符, 61
  - 实例属性的赋值, 131
  - 变量的赋值, 7
  - 嵌套函数中变量的赋值, 97
- 关联数组, 16, 44
- 运算符的结合性, 78
- astimezone() 方法, datetime 对象的方法, 340
- asynchat 类, asynchat 模块, 452
- asynchat 模块, 452
  - 使用, 467
- 异步 I/O, 415
- 异步网络
  - 与阻塞操作, 469
  - 何时考虑, 467
- asyncore 模块, 415, 455
  - 使用, 467
- AsyncResult 对象, multiprocessing 模块, 425

#### B

- -B 命令行选项, 173
- b 字符, 字符串字面量前, 29
- b(reak) 调试器命令, pdb 模块, 187
- b16decode() 函数, base64 模块, 547
- b16encode() 函数, base64 模块, 547
- b2a_base64() 函数, binascii 模块, 547
- b2a_hex() 函数, binascii 模块, 548
- b2a_hqx() 函数, binascii 模块, 548
- b2a_uu() 函数, binascii 模块, 547
- b32decode() 函数, base64 模块, 546
- b32encode() 函数, base64 模块, 546
- b64decode() 函数, base64 模块, 546
- b64encode() 函数, base64 模块, 546
- 反斜杠规则, 与原始字符串, 29
- 'backslashreplace' 错误处理, Unicode 编码, 166
- BadStatusLine 异常, http.client 模块, 504
- 基类, 21
- 十进制基数, 243 与浮点数, 12
- base64 编码, 描述, 545
- base64 模块, 545
- BaseCGIHandler() 函数, wsgiref.handlers 模块, 542
- BaseException 类, 212
- BaseException 异常, 87
- BaseHTTPRequestHandler 类, http.server 模块, 508
- BaseHTTPServer 模块, 见 http.server, 506
- BaseManager() 函数, multiprocessing 模块, 430
- basename() 函数, os.path 模块, 396, 398
- BaseProxy 类, multiprocessing 模块, 432
- atan() 函数, math 模块, 251
- atan2() 函数, math 模块, 251
- atanh() 函数, math 模块, 251
- atexit 模块, 179, 219
- 原子操作, 反汇编, 193
- attach() 方法, Message 对象的方法, 556
- attrgetter() 函数, operator 模块, 275
- attrib 属性, Element 对象的属性, 576
- 属性赋值, 在实例上, 131
- 属性绑定操作符 ., 33, 76
  - 优化, 196
- 属性绑定与继承, 119
  - 与方法, 48
  - 实例与类, 118
  - 用户定义对象的, 131
  - 过程, 57
  - 在类中重定义, 132
  - 特殊方法, 57
- 属性删除, 在实例上, 131
- 字符串格式化中的属性查找, 72
- AttributeError 异常, 87, 213
  - 与属性绑定, 132
- attributes 属性, DOM Node 对象的属性, 570
- 计算为属性的属性, 117, 124
  - 在 __init__() 方法中创建, 118
  - 描述符, 58, 126
  - 封装, 127
  - 组合字符串格式化中的查找, 42
  - 对象的, 33
  - 私有, 127
  - 使用 __slots__ 限制名称, 132
  - 函数上用户定义的, 114
- audioop 模块, 588
- 增强赋值操作符, 61, 75
- 认证, 获取 URL, 519
- authkey 属性, Process 对象的属性, 416
- awk UNIX 命令, 与列表推导的相似性, 111

如何使此索引更有用？请通过 indexes@sampublishing.com 联系我们

- BaseRequestHandler 类, SocketServer 模块, 490
- __bases__ 属性
  - 类的, 131
  - 类型的, 50
- basestring 变量, 202
- basicConfig() 函数, logging 模块, 355
- BasicContext 变量, decimal 模块, 248
- .bat 文件, Windows, 176
- bdb 模块, 585
- Beautiful Soup 包, 563
- betavariate() 函数, random 模块, 255
- bidirectional() 函数, unicodedata 模块, 293
- 大端序格式, 167
- 大端序, 打包与解包, 292
- bin() 函数, 77, 202
- 二进制数据结构, 打包与解包, 290
- 二进制发行版, 使用 distutils 创建, 153
- 二进制文件模式, 159
- 二进制文件, 350
  - 缓冲 I/O, 351
  - 使用面向行函数时的注意事项, 351-352
- 二进制整数字面量, 27
- Binary() 函数
  - 数据库 API, 301
  - xmlrpc.client 模块, 526
- binascii 模块, 547
- bind() 方法
  - SocketServer 类的方法, 493
  - dispatcher 对象的方法, 456
  - socket 对象的方法, 478
- binhex 模块, 587
- bisect 模块, 261
- bisect() 函数, bisect 模块, 261
- bisect_left() 函数, bisect 模块, 261
- bisect_right() 函数, bisect 模块, 261
- 位运算与原生整数, 66
- 按位与操作符 &, 65
- 按位取反操作符 ~, 65
- 按位或操作符 |, 65
- 按位异或操作符 ^, 65
- 空行, 26
- block_size 属性, 哈希对象的属性, 559
- 阻塞操作, 与异步网络, 469
- 蓝牙协议, 470
  - 地址格式, 472
- BOM（字节顺序标记）, 280
  - 与 Unicode, 168
- BOM_* 常量, codecs 模块, 280
- bool 类型, 38
- bool() 函数, 202
- __bool__() 方法, 56, 58
- 布尔表达式, 9, 77
  - 求值规则, 78
- 布尔运算符, 66
- 布尔值, 27, 38
- boolean() 函数, xmlrpc.client 模块, 525
- 绑定方法, 49, 125
- BoundedSemaphore 对象
  - multiprocessing 模块, 427
  - threading 模块, 439
- BoundedSemaphore() 方法, Manager 对象的方法, 428
- break 语句, 83-84
  - 与生成器, 103
- 在多行上拆分长语句, 9
- 断点
  - 在调试器中设置, 187
  - 手动设置, 186
- 浏览器, 从 Python 启动, 544
- BSD, kqueue 接口, 460
- BTPROTO_* 常量, socket 模块, 477
- 缓冲区, 循环缓冲区, 262
- buffer_info() 方法, array 对象的方法, 259
- 缓冲二进制 I/O, 351
- BufferedIOBase 抽象基类, 354
- BufferedRandom 类, io 模块, 352
- BufferedReader 类, io 模块, 351

- cancel() 方法, Timer 对象的方法, 645
- BufferedRWPair 类, io 模块, 352
- BufferedWriter 类, io 模块, 352
- 缓冲, 与生成器, 165
- build_opener() 函数, urllib.request 模块, 518
- 内置异常, 23, 87
- 内置函数和类型, 201
- 内置函数, 在 Python 2 中使用 Python 3 函数, 217
- 内置类型, 37
- __builtin__ 模块, 201
- builtin_module_names 变量, sys 模块, 229
- BuiltinFunctionType, 49
- BuiltinFunctionType 类型, 47, 237
- builtins 模块, Python 3, 201
- byref() 函数, ctypes 模块, 615
- 字节字面量, 29
- 字节字符串, 41
  - 与 WSGI, 541
  - 与文件, 160
  - 与 Python 3 中的系统接口, 630
  - 作为内存中的二进制文件, 352
  - 解码为 Unicode, 165
  - 在 Python 3 中的不同行为, 629
  - 在 Python 3 中缺少格式化, 629
  - 与 Unicode 字符串混合, 70, 167
  - 可变字节数组, 202
  - 在系统接口中的使用, 633
- bytearray() 函数, 202
- byteorder 变量, sys 模块, 229
- bytes 数据类型, Python 3, 29
- bytes() 函数, 202-203
- bytes, 字符串中的转义码, 28
- BytesIO 类, io 模块, 352
- byteswap() 方法, array 对象的方法, 259
- bz2 模块, 313
- BZ2Compressor() 函数, bz2 模块, 313
- BZ2Decompressor() 函数, bz2 模块, 314
- BZ2File() 函数, bz2 模块, 313

#### C

- C 扩展, 591
  - 与 .egg 文件, 147
  - 与模块重新加载, 149
  - 使用 distutils 编译, 596
  - 使用 SWIG 创建, 619
  - 使用 ctypes 的示例, 618
  - 释放全局解释器锁, 444
- -c 命令行选项, 173-174
- C#, 620
- c(ont(inue)) 调试器命令, pdb 模块, 188
- C++, 类系统的差异, 119
- C
  - Python 变量与之比较, 7
  - 函数的实现, 49
- C/C++ 代码, 在第三方包中, 154
- C3 线性化算法, 与继承, 121
- c_* 数据类型, ctypes 模块, 614
- CacheFTPHandler 类, urllib.request 模块, 518
- 缓存函数结果, 242
- calcsize() 函数, struct 模块, 291
- calendar 模块, 588
- call() 函数, subprocess 模块, 403
- __call__() 方法, 50, 62
- Callable 抽象基类, 265
- 可调用对象
  - 与 __call__() 方法, 62
  - 类, 50
  - 实例, 50
  - 类型, 47
- 回调函数, 98
  - 与 lambda, 112
- 从 C 调用 Python 函数, 610
- 调用函数, 18, 93
- _callmethod() 方法, BaseProxy 对象的方法, 433
- callproc() 方法, Cursor 对象的方法, 298
- cancel() 方法, Timer 对象的方法, 438

如何使此索引更有用？请通过 indexes@samspublishing.com 联系我们



###### cancel_join_thread() 方法，Queue 对象，418

###### 链式比较，66

###### CannotSendHeader 异常，http.client 模块，504

###### 链式异常，Python 3，627

###### CannotSendRequest 异常，http.client 模块，504

###### 更改交互模式下的结果显示，176

###### capitalize() 方法，字符串的，41-42

###### 导入时更改模块名称，144

###### capitals 属性，Context 对象的，247

###### 更改工作目录，379

###### capwords() 函数，string 模块，290

###### 在 HTTP 请求中更改用户代理头，517

###### 大小写转换，字符串的，43-44

###### 字符替换，42

###### 标识符的大小写敏感性，26

###### characters() 方法，ContentHandler 对象的，581

###### case 语句的缺失，9

###### 字符
- 转义码，28
- 指定 Unicode，28

###### cast() 函数，ctypes 模块，617

###### 捕获所有异常，85

###### chdir() 函数，os 模块，379

###### 捕获多个异常，85

###### check_call() 函数，subprocess 模块，403

###### category() 函数，unicodedata 模块，170，293

###### check_unused_args() 方法，Formatter 对象的，289

## \_\_cause\_\_ 属性，Exception 对象的，213，627

###### 检查是否作为主程序运行，146

###### range() 函数使用注意事项，17

###### 使用条件语句检查多个情况，9

###### CDLL() 函数，ctypes 模块，612

###### chflags() 函数，os 模块，386

###### ceil() 函数，math 模块，251

###### center() 方法，字符串的，41-42

###### 多线程版小鸡游戏，414

###### cert_time_to_seconds() 函数，ssl 模块，488

###### childNodes 属性，DOM Node 对象的，570

###### CGI 脚本，533
- 编写建议，537
- 环境变量，533
- 在其中执行 XML-RPC 服务器，529
- 运行 WSGI 应用程序，542
- 数据库的使用，538
- Web 框架，538

###### chmod() 函数，os 模块，387

###### choice() 函数，random 模块，254

###### chown() 函数，os 模块，387

###### chr() 函数，77，203

###### cgi 模块，533

###### chroot() 函数，os 模块，379

###### chunk 模块，588

###### CGIHandler() 函数，wsgiref.handlers 模块，542

###### cipher() 方法，ssl 对象的，487

###### 使用 deque 对象实现循环缓冲区或队列，262

###### CGIHTTPRequestHandler 类，http.server 模块，507

###### cl(ear) 调试器命令，pdb 模块，188

###### CGIHTTPServer 模块，参见 http.server，506

###### 类装饰器，102，141

###### cgib 模块，539

###### 类方法，48，123
- 属性绑定，124
- 实际用途，124

###### 类变量，117
- 所有实例共享，118

## \_\_class\_\_ 属性
- 实例的，50，131
- 方法的，49

###### 类，21
- \_\_del\_\_() 方法与垃圾回收，221-222
- \_\_init\_\_() 方法，118
- \_\_init\_\_() 方法与继承，120
- \_\_slots\_\_ 属性，132
- 抽象基类，136，257
- 访问控制说明符的缺失，127
- 在模块中访问，144
- 与元类，138
- 作为可调用对象，50
- 作为命名空间，117
- 属性绑定规则，118
- 类方法，203
- 创建实例，22，55，118
- 自定义属性访问，57-58
- 应用于类的装饰器，102，141
- 定义方法，21
- 描述符属性，58，126
- 与 C++ 或 Java 的区别，119
- 继承，21，119
- 继承内置类型，22
- 内存管理，128
- 混入，122
- 多重继承，120-121
- object 基类，119
- 旧式类，139
- 运算符重载，54
- 优化，195
- 继承的优化，233
- \_\_slots\_\_ 的性能，196
- 序列化，228
- 私有成员，26
- 重新定义属性绑定，132
- 作用域规则，118
- 方法的 self 参数，119
- 特殊方法，54
- 静态方法，22
- 方法中的 super() 函数，120
- 支持 pickle 模块，228
- 类型，47
- 统一访问原则，125
- 与字典存储数据的比较，195

###### @classmethod 装饰器，48，123，125，203

###### ClassType 类型，旧式类，139

###### cleandoc() 函数，inspect 模块，222

###### clear() 方法
- Element 对象的，576
- Event 对象的，440
- deque 对象的，262
- 字典的，45
- 集合的，46

###### clear_flags() 方法，Context 对象的，247

###### clear_memo() 方法，Pickler 对象的，228

## \_clear_type_cache() 函数，sys 模块，233

###### 清空字典，45

###### 清除上一个异常，233

###### Client 类，multiprocessing 模块，433

###### 客户端程序，449
- TCP 示例，451
- UDP 示例，486

###### client_address 属性
- BaseHTTPRequestHandler 对象的，509
- BaseRequestHandler 对象的，490

###### clock() 函数，time 模块，191，405

###### cloneNode() 方法，DOM Node 对象的，571

###### close() 函数，os 模块，381

###### close() 方法
- Connection 对象的，297，421
- Cursor 对象的，298
- FTP 对象的，498
- HTMLParser 对象的，561
- HTTPConnection 对象的，503
- Handler 对象的，364
- IOBase 对象的，349
- Listener 对象的，434
- Pool 对象的，424
- Queue 对象的，418
- TarFile 对象的，320
- TreeBuilder 对象的，577
- ZipFile 对象的，325
- dbm 风格数据库对象的，310
- dispatcher 对象的，456
- 文件的，159
- 生成器的，20，53，103，105
- 生成器与同步，104
- mmap 对象的，371
- shelve 对象的，311
- socket 对象的，478
- urlopen 对象的，515

###### close_when_done() 方法，asyncchat 对象的，452

###### closed 属性
- IOBase 对象的，349
- 文件的，161

###### closefd 属性，FileIO 对象的，350

###### closefd 参数，open() 函数的，159

###### CloseKey() 函数，winreg 模块，408

###### closerange() 函数，os 模块，382

###### closing() 函数，contextlib 模块，268

## \_\_closure\_\_ 属性，函数的，48，100

###### 闭包，98-99
- 与装饰器，101
- 与嵌套函数，99
- 与包装器，100
- 相较于类的性能提升，100

###### cmath 模块，251

###### cmd 模块，588

###### cmp() 函数，203
- filecmp 模块，314

###### cmpfiles() 函数，filecmp 模块，314

## co_\* 属性，代码对象的，51-52

###### 代码执行，模块中的，143-144

###### 代码迁移
- 从 Python 2 到 3，634
- 实际策略，637

###### code 模块，585

###### 代码对象，51
- 属性，51
- 使用 compile() 函数创建，115

###### 码位，Unicode，28

## \_\_code\_\_ 属性，函数的，48

###### 执行字符串代码，115

###### CodeInfo 类，codecs 模块，277

###### codecs 模块，167，277
- 压缩编解码器的移除，280
- 使用字节字符串，280

###### coded_value 属性，Morsel 对象的，512

###### codeop 模块，585

###### CodeType 类型，51，237

## \_\_coerce\_\_() 方法，已弃用，134

###### 数值类型的强制转换，66-67

###### collect 函数，gc 模块，179

###### collect() 函数，gc 模块，220

###### collect_incoming_data() 方法，asyncchat 对象的，452

###### 集合的定义，33

###### collections 模块，138，262

###### colorsys 模块，588

###### combinations() 函数，itertools 模块，271

###### combine() 方法，datetime 类的，339

###### combining() 函数，unicodedata 模块，294

###### command 属性，BaseHTTPRequestHandler 对象的，509

###### 命令行选项，13，157
- Python 3，633
- 在程序中检测设置，230
- 解释器的，173
- 使用 optparse 解析，374

###### commands 调试器命令，pdb 模块，188

###### commands 模块，331

###### comment 属性，ZipInfo 对象的，327

###### Comment() 函数，xml.etree.ElementTree 模块，575

###### 注释，6，26

###### commit() 方法，Connection 对象的，298

###### common 属性，dircmp 对象的，315

###### common_dirs 属性，dircmp 对象的，315

###### common_files 属性，dircmp 对象的，315

###### common_funny 属性，dircmp 对象的，315

###### commonprefix() 函数，os.path 模块，396

###### communicate() 方法，Popen 对象的，403

###### 比较运算符，56

###### 比较，66
- Python 3，633
- 链式比较，66
- 不兼容对象的比较，78
- 对象的比较，34
- 序列的比较，70
- 弱引用的比较，242

###### 编译为字节码，148

###### compile() 函数，115，203
- re 模块，283-284

###### compileall 模块，585

###### 编译器的缺失，181

###### complete_statement() 函数，sqlite3 模块，305

###### Complex 抽象基类，253

###### 复数，27，39
- cmath 库模块，251
- 比较，66

###### complex 类型，38

###### complex() 函数，76，203

## \_\_complex\_\_() 方法，61-62
- 与类型强制转换，134

###### 编写电子邮件消息，555

###### 复合字符串格式化，8，42，72
- 与 \_\_format\_\_()，56
- 与查找，42

###### compress() 函数
- bz2 模块，314
- zlib 模块，328

###### compress() 方法
- BZ2Compressor 对象的，313
- compressobj 对象的，328

###### compress_size 属性，ZipInfo 对象的，327

###### compress_type 属性，ZipInfo 对象的，327

###### 压缩
- 文件压缩，313，317
- zlib 压缩，328

###### CompressionError 异常，tarfile 模块，322

###### compressobj() 函数，zlib 模块，328

###### 计算属性与特性，124

###### concat() 函数，operator 模块，274

###### 连接
- 相邻字符串字面量的连接，27
- 列表的连接，12
- 字符串的连接，11

###### 并发，413
- 多进程编程建议，435
- 与 Python 程序，414
- 与副作用，96
- 协程，446
- 全局解释器锁，414
- 多核的限制，414
- 消息传递，413-415
- 使用生成器实现多任务，447
- 可扩展性问题，415
- 同步问题，414

###### 并发编程，413

###### Condition 对象
- multiprocessing 模块，427
- threading 模块，441

###### condition 调试器命令，pdb 模块，188

###### 条件变量，441

###### Condition() 方法，Manager 对象的，429

###### 条件表达式，79

###### 条件语句，9，81

###### ConfigParser 类，configparser 模块，332

如何让此索引更加有用？请发送电子邮件至 indexes@samspublishing.com 与我们联系



- configparser模块, 332
- 配置文件, 332
  - 与Python脚本的区别, 334-335
  - 用于logging模块, 368
  - 变量替换, 335
- `confstr()`函数, os模块, 395
- `conjugate()`方法
  - 复数的, 39
  - 浮点数的, 39
- `connect()`函数
  - 数据库API, 297
  - sqlite3模块, 304
- `connect()`方法
  - BaseManager对象的, 431
  - FTP对象的, 498
  - HTTPConnection对象的, 503
  - SMTP对象的, 514
  - dispatcher对象的, 456
  - socket对象的, 478
- `connect_ex()`方法, socket对象的, 478
- 连接进程, multiprocessing模块, 433
- Connection类
  - 数据库API, 297
  - sqlite3模块, 305
- `ConnectRegistry()`函数, winreg模块, 408
- 控制台窗口, Windows, 176
- Container抽象基类, 265
- 容器对象, 29
  - 与引用计数, 34
  - 定义, 33
- 包含测试, `in`运算符, 9
- `contains()`函数, operator模块, 274
- `__contains__()`方法, 58
- ContentHandler类, xml.sax模块, 581
- ContentTooShort异常, urllib.error模块, 523
- Context类, decimal模块, 244
- 上下文管理协议, 62
- 上下文管理器, 62, 89
  - decimal模块, 248
  - 使用生成器定义, 267
  - 锁定, 442
  - 嵌套, 267
- `__context__`属性, Exception对象的, 213, 627
- contextlib模块, 90, 267
- `@contextmanager`装饰器, 90
- `continue`语句, 83-84
- 控制字符, 从字符串中去除, 42
- 字符串到数字的转换, 11
- 转换操作, 76
- `convert_field()`方法, Formatter对象的, 289
- 将Python类型转换为C, 611
- 将字典转换为列表, 16
- 将序列转换为列表, 77
- 将序列转换为集合, 15
- 将序列转换为元组, 77
- 将类型从C转换为Python, 602
- 将类型从Python转换为C, 597
- Cookie模块, 参见 http.cookies, 511
- CookieError异常, http.cookies模块, 513
- CookieJar类, http.cookiejar模块, 513
- cookielib模块, 参见 http.cookiejar, 513
- cookies
  - HTTP, 511
  - 使用cookie支持获取URL, 519
- copy模块, 36, 67, 219
  - 其局限性, 220
- `copy()`函数
  - copy模块, 219
  - shutil模块, 318
- `copy()`方法
  - Context对象的, 247
  - 字典的, 45
  - 摘要对象的, 559
  - hmac对象的, 560
  - 集合的, 46
- `copy2()`函数, shutil模块, 318
- `__copy__()`方法, 220
- copy_reg模块, 585
- `copyfile()`函数, shutil模块, 318
- `copyfileobj()`函数, shutil模块, 318
- 复制目录, 318
- 复制文件, 318
- 复制
  - 与引用计数, 35
  - 深拷贝, 36
  - 字典, 45
  - 可变对象的, 35
  - 浅拷贝, 36
- `copymode()`函数, shutil模块, 318
- copyright变量, sys模块, 230
- `copysign()`函数, math模块, 251
- `copystat()`函数, shutil模块, 318
- `copytree()`函数, shutil模块, 318
- `@coroutine`装饰器示例, 105
- 协程, 20, 104
  - 高级示例, 460
  - 异步I/O处理, 460
  - 构建其调用栈, 463
  - 并发, 108
  - 并发编程, 446
  - 示例, 20
  - 执行行为, 105
  - 消息传递, 108, 415
  - 多任务示例, 447
  - 实际应用, 107
  - 递归, 112
  - 发送和返回值, 106
  - 使用`select()`的任务调度器, 460
  - 将控制权转移到另一个协程, 463
  - 使用`next()`方法, 104
  - 与网络编程结合使用, 467
- `cos()`函数, math模块, 251
- `cosh()`函数, math模块, 251
- `count()`函数, itertools模块, 271
- `count()`方法
  - 数组对象的, 260
  - 列表的, 40
  - 字符串的, 42
- 循环中的计数, 83
- `countOf()`函数, operator模块, 274
- cp1252编码, 描述, 169
- cp437编码, 描述, 169
- cPickle模块, 229
- cProfile模块, 190
- CPU时间, 获取, 191, 405
- CPU, 获取系统上的数量, 434
- CPU密集型任务与线程, 444
- `cpu_count()`函数, multiprocessing模块, 434
- CRC属性, ZipInfo对象的, 327
- `crc32()`函数
  - binascii模块, 548
  - zlib模块, 328
- `crc_hqx()`函数, binascii模块, 548
- `create_aggregate()`方法, Connection对象的, 305
- `create_collation()`方法, Connection对象的, 306
- `create_connection()`函数, socket模块, 473
- `create_decimal()`方法, Context对象的, 247
- `create_function()`方法, Connection对象的, 305
- `create_socket()`方法, dispatcher对象的, 456
- `create_string_buffer()`函数, ctypes模块, 617
- create_system属性, ZipInfo对象的, 327
- `create_unicode_buffer()`函数, ctypes模块, 617
- create_version属性, ZipInfo对象的, 327
- created属性, Record对象的, 359
- `CreateKey()`函数, winreg模块, 408
- 创建Windows安装程序, 153
- 创建二进制发行版, 153
- 创建源码发行版, 153
- 创建自定义字符串格式化器, 288
- 创建程序, 6
- 生成随机数, 254
- 创建用户定义的实例, 22
- 实例的创建, 118
  - 涉及的步骤, 129
- .pyc和.pyo文件的创建, 148
- 临界区, 其锁定, 414
- `critical()`方法, Logger对象的, 357
- crypt模块, 586
- 加密哈希函数, 559
- CSV数据, 读取示例, 14
- CSV文件
  - 解析, 548
  - 列的类型转换, 37
- csv模块, 548
- `ctermid()`函数, os模块, 379
- `ctime()`函数, time模块, 405
- `ctime()`方法, date对象的, 337
- Ctrl-C, 键盘中断, 162
- ctypes模块, 612
  - 数组类型, 614
  - 可用的数据类型, 614
  - 强制转换数据类型, 617
  - 创建字节字符串, 617
  - 从缓冲区创建对象, 616
  - 示例, 618
  - 查找库模块, 612
  - 加载共享库, 612
  - 内存复制, 617
  - 传递指针和引用, 615
  - 指针类型, 614
  - 设置函数原型, 613
  - 与multiprocessing共享数据, 426
  - 结构体类型, 615
- `cunivariate()`函数, random模块, 255
- curdir变量, os模块, 386
- 花括号, 与字典, 16
- 当前时间, 获取, 405
- `_current_frames()`函数, sys模块, 233
- `current_process()`函数, multiprocessing模块, 434
- `current_thread()`函数, threading模块, 443
- `currentframe()`函数, inspect模块, 222
- 柯里化, 与部分函数求值, 76
- curses模块, 586
- Cursor类, 数据库API, 298
- `cursor()`方法, Connection对象的, 298
- `cwd()`方法, FTP对象的, 498
- `cycle()`函数, itertools模块, 271
- 循环, 与垃圾回收, 35
- 循环数据结构, 与`__del__()`方法, 129

#### D

- `d(own)`调试器命令, pdb模块, 188
- daemon属性
  - Process对象的, 416
  - Thread对象的, 436
- 守护进程, 415
- 守护线程, 436
- 末尾逗号
  - 与print语句, 10
  - 与元组, 14
  - print语句, 162
- data属性, DOM Text对象的, 572
- 数据封装, 127
- 数据结构
  - 与字典, 16
  - 列表和元组, 14
  - 具名元组, 264
- `data()`方法, TreeBuilder对象的, 577
- 数据流处理, 与协程, 107
- 数据库API, 297
- 数据库接口, 297
  - 与线程, 302
- 数据库结果, 转换为字典, 303
- 数据库
  - 与CGI脚本, 538
  - 持久化字典, 171
- DatabaseError异常, 数据库API, 302
- 数据库, DBM风格的, 310
- DataError异常, 数据库API, 302
- DatagramHandler类, logging模块, 362
- DatagramRequestHandler类, SocketServer模块, 491
- 数据报, 470
- 日期和时间操作, 336
- date类, datetime模块, 336
- 日期解析, 343, 407
- `Date()`函数, 数据库API, 301
- `date()`方法, datetime对象的, 340
- date_time属性, ZipInfo对象的, 327
- `DateFromTicks()`函数, 数据库API, 301
- datetime类, datetime模块, 339
- datetime模块, 336
- `DateTime()`函数, xmlrpc.client模块, 526
- day属性, date对象的, 337
- daylight变量, time模块, 405
- dbhash模块, 310
- dbm模块, 310
- DBM风格的数据库, 310
- 死锁, 锁导致的问题, 442
- debug属性
  - TarFile对象的, 320
  - ZipFile对象的, 325
  - sys.flags的, 230
- `__debug__`变量, 91, 369
- `debug()`方法, Logger对象的, 357
- 调试
  - CGI脚本, 539
  - 未捕获异常后, 186
  - 检查内存泄漏, 221
  - 配置调试器, 190
  - 从命令行调试整个程序, 189
  - 手动设置断点, 186
  - pdb模块, 186
  - 运行函数, 186
  - 指定断点, 187
  - 使用logging模块, 355
- Decimal类, decimal模块, 243
- Decimal对象, 转换为分数, 250
- decimal模块, 39, 243
  - 与`sum()`函数, 69
  - 与线程, 249
  - 舍入行为, 245
- `decimal()`函数, unicodedata模块, 295
- 声明式编程, 110
- `decode()`函数
  - base64模块, 547
  - quopri模块, 568
- `decode()`方法
  - 在Python 3中, 629
  - CodecInfo对象的, 277
  - IncrementalDecoder对象的, 279
  - JSONDecoder对象的, 565
  - 字符串的, 29, 42, 165-166
  - 正确使用, 166
- `decodestring()`函数
  - base64模块, 547
  - quopri模块, 568
- `decomposition()`函数, unicodedata模块, 295
- `decompress()`函数
  - bz2模块, 314
  - zlib模块, 328
- `decompress()`方法
  - BZ2Decompressor对象的, 314
  - decompressobj对象的, 328
- `decompressobj()`函数, zlib模块, 328
- 装饰器, 22, 101
  - 应用于类定义, 102, 141
  - 复制函数属性, 269



##### 文档字符串

- 文档字符串, 102, 113
- 示例, 101
- 多个, 31
- 性能优势, 197
- 放置位置, 30, 101
- 递归函数, 102, 113
- 用户定义函数属性, 102, 114
- 带参数, 102

深拷贝, 36

`deepcopy()` 函数, `copy` 模块, 219

`__deepcopy__()` 方法, 220

`def` 语句, 18, 48, 93

默认 Unicode 编码, 166, 177

默认 Unicode 错误处理策略, 167

###### 默认参数

- 默认参数, 18, 93
  - 与可变值, 94
  - 值的绑定, 93

`default()` 方法, `JSONEncoder` 对象的方法, 566

`default_factory` 属性, `defaultdict` 对象的属性, 263

`DefaultContext` 变量, `decimal` 模块, 248

`defaultdict()` 函数, `collections` 模块, 263

`__defaults__` 属性, 函数的属性, 48

`defaults()` 方法, `ConfigParser` 对象的方法, 333

`defects` 属性, `Message` 对象的属性, 554

定义函数, 18

定义多个实例创建方法, 123

定义新异常, 88

`degrees()` 函数, `math` 模块, 251

`del` 操作符, 用于字典, 16, 74

###### `del` 语句

- `del` 语句, 35, 69
  - 与 `__del__()` 方法, 129
  - 与切片, 40
  - 删除映射项, 45

###### `__del__()` 方法

- `__del__()` 方法, 55, 129
  - 与程序终止, 179
  - 定义的危险性, 129
  - 垃圾回收, 129, 221-222
  - 用途, 55

`del_param()` 方法, `Message` 对象的方法, 556

###### `delattr()` 函数

- `delattr()` 函数, 203
  - 与私有属性, 128

`__delattr__()` 方法, 57-58, 131

延迟求值, 99

延迟执行, 使用线程, 437

`delete()` 方法, `FTP` 对象的方法, 498

`__delete__()` 方法, 描述符的方法, 58, 126

`DeleteKey()` 函数, `winreg` 模块, 409

`@deleter` 装饰器, 用于属性, 126

`DeleteValue()` 函数, `winreg` 模块, 409

从字典中删除项, 16

删除序列项, 40

删除切片, 40, 69

删除实例属性, 131

分隔符, 30

`delitem()` 函数, `operator` 模块, 274

###### `__delitem__()` 方法

- `__delitem__()` 方法, 58-59
  - 与切片, 59

`delslice()` 函数, `operator` 模块, 274

`demo_app()` 函数, `wsgiref.simple_server` 模块, 542

###### `denominator` 属性

- `denominator` 属性
  - `Fraction` 对象的属性, 250
  - 整数的属性, 39

`DeprecationWarning` 警告, 216, 238

###### `deque` 对象

- `deque` 对象
  - `collections` 模块, 194
  - 与列表比较, 194

`deque()` 函数, `collections` 模块, 262

`DER_cert_to_PEM_cert()` 函数, `ssl` 模块, 488

`dereference` 属性, `TarFile` 对象的属性, 320

派生类, 119

`description` 属性, `Cursor` 对象的属性, 299

###### 描述符

- 描述符, 58, 126
  - 与元类, 140

检测文件结束符 (EOF), 160

目录, 655

###### 检测解释器命令行选项的设置

- 检测解释器命令行选项的设置, 230

**devnull** 变量, `os` 模块, 386

**Dialect** 类, `csv` 模块, 551

**dict** 类型, 38

###### `__dict__` 属性

- **`__dict__`** 属性
  - 类的属性, 131
  - 函数的属性, 48, 114
  - 实例的属性, 50, 131
  - 模块的属性, 51, 144
  - 类型的属性, 50
  - 用户定义对象的属性, 63

###### `dict()` 函数

- **`dict()`** 函数, 16, 77, 204
  - 性能特性, 195

###### `dict()` 方法, `Manager` 对象的方法

- **`dict()`** 方法, **`Manager`** 对象的方法, 429

###### 字典推导式, Python 3

- **字典推导式**, Python 3, 623

###### 字典

- **字典**, 16, 44
  - 可接受的键类型, 16
  - 访问项, 16
  - 与 Python 3 注意事项, 45
  - 与 **`__hash__()`** 方法, 56
  - 与字符串格式化, 70, 72
  - 初始值的自动创建, 263
  - 清空, 45
  - 与 `defaultdict` 对象比较, 263
  - 转换为列表, 16
  - 复制, 45
  - 从数据库结果创建, 303
  - 使用 `dict()` 函数创建, 204
  - 定义空字典, 16
  - 删除项, 16, 45
  - 相等性, 78
  - 索引操作符, 74
  - 插入项, 16
  - 项赋值, 74
  - 项删除, 74
  - 遍历键, 17
  - 键值, 44, 74
  - 项列表, 45
  - 在复合字符串格式化中查找, 42, 72
  - 带默认值查找, 16
  - 获取键, 45-46
  - 获取值, 45
  - 性能, 16
  - **in** 操作符的性能, 197
  - 使用 `shelve` 模块持久化, 171
  - 移除项, 16
  - 多进程共享, 429
  - 元组作为键, 74
  - 更新, 45
  - 用作数据结构, 16
  - 用作查找表, 16
  - 将函数用作值, 37
  - 用于传递关键字函数参数, 95
  - Python 3 中的视图对象, 632

###### `DictReader()` 函数, `csv` 模块

- **`DictReader()`** 函数, `csv` 模块, 550

###### 字典, 与类存储数据的比较

- **字典**, 与类存储数据比较, 195

###### `DictWriter()` 函数, `csv` 模块

- **`DictWriter()`** 函数, `csv` 模块, 550

###### `diff_files` 属性, `dircmp` 对象的属性

- **`diff_files`** 属性, `dircmp` 对象的属性, 315

###### `difference` 操作符 `-`, 集合的操作符

- **`difference`** 操作符 **`-`**, 集合的操作符, 15

###### `difference()` 方法, 集合的方法

- **`difference()`** 方法, 集合的方法, 46

###### `difference_update()` 方法, 集合的方法

- **`difference_update()`** 方法, 集合的方法, 46

###### `difflib` 模块

- **`difflib`** 模块, 586

###### `dig` 属性, `sys.float_info` 的属性

- **`dig`** 属性, `sys.float_info` 的属性, 231

###### `digest()` 方法

- **`digest()`** 方法
  - 摘要对象的方法, 559
  - hmac 对象的方法, 560

###### `digest_size` 属性, 摘要对象的属性

- **`digest_size`** 属性, 摘要对象的属性, 559

###### `digit()` 函数, `unicodedata` 模块

- **`digit()`** 函数, `unicodedata` 模块, 295

###### `digits` 变量, `string` 模块

- **`digits`** 变量, `string` 模块, 287

###### `dir()` 函数

- **`dir()`** 函数, 21, 24, 204
  - 隐藏类中的属性名, 128, 204

###### `dir()` 方法, `FTP` 对象的方法

- **`dir()`** 方法, `FTP` 对象的方法, 498

###### `__dir__()` 方法

- **`__dir__()`** 方法, 63, 128, 204

###### `dircmp()` 函数, `filecmp` 模块

- **`dircmp()`** 函数, `filecmp` 模块, 314

###### 目录

- **目录**
  - 比较, 314
  - 复制, 318
  - 使用 shell 通配符读取文件, 317
  - 递归遍历, 390
  - 访问的系统函数, 386
  - 临时目录, 323
  - 测试文件名是否为目录, 397

`dirname()` 函数, `os.path` 模块, 396

`dis` 模块, 585

`dis()`, `dis` 模块, 193

禁用调试器命令, `pdb` 模块, 188

###### `disable()` 函数

- `disable()` 函数
  - `gc` 模块, 220
  - `logging` 模块, 366

`disable_intersperse_args()` 方法, `OptionParser` 对象的方法, 376

禁用垃圾回收, 220

禁用换行符转换, 159

反汇编, 193

`discard()` 方法, 集合的方法, 47

`discard_buffers()` 方法, `asynchat` 对象的方法, 452

`dispatcher` 类, `asyncore` 模块, 455

`__displayhook__` 变量, `sys` 模块, 230

`displayhook()` 函数, `sys` 模块, 176, 233

`disposition` 属性, `FieldStorage` 对象的属性, 535

`disposition_options` 属性, `FieldStorage` 对象的属性, 535

分布式计算, 与 `multiprocessing` 模块, 435

分发程序, 152

###### `distutils` 模块

- `distutils` 模块, 152-153, 585, 596
  - 与扩展模块, 596
  - 创建二进制分发版, 153
  - 使用 SWIG 创建扩展, 620

`div()` 函数, `operator` 模块, 273

`__div__()` 方法, 60

整数除法, Python 3, 633

除法操作符 `/`, 65

除法操作符, Python 2 与 Python 3 比较, 61

除法, 整数的截断, 61-62, 65

`division_new` 属性, `sys.flags` 的属性, 230

`division_warning` 属性, `sys.flags` 的属性, 230

`divmod()` 函数, 66, 204

`__divmod__()` 方法, 60

`dllhandle` 变量, `sys` 模块, 230

###### DLL

- DLL
  - 使用 `distutils` 创建, 596
  - 扩展模块, 148
  - 使用 `ctypes` 加载, 612

`do_handshake()` 方法, `ssl` 对象的方法, 487

###### `__doc__` 属性

- **`__doc__`** 属性
  - 内置函数的属性, 49
  - 函数的属性, 24, 48, 113
  - 方法的属性, 49
  - 模块的属性, 51
  - 对象的属性, 30
  - 类型的属性, 50

`DocCGIXMLRPCRequestHandler` 类, `xmlrpc.server` 模块, 528

###### `doctest` 模块

- `doctest` 模块, 181-182
  - 详细模式选项, 182

`Document` 类, `xml.dom.minidom` 模块, 571

文档字符串, 复制到装饰器, 269

##### 文档字符串

- 文档字符串, 24, 30, 48, 113
  - 与 XML-RPC, 527
  - 与装饰器, 102, 113
  - 与缩进, 30
  - `doctest` 模块, 181
  - 在扩展模块中, 595
  - 使用 `-OO` 选项剥离, 148
  - 测试, 181

`documentElement` 属性, DOM `Document` 对象的属性, 571

`DocXMLRPCServer` 类, `xmlrpc.server` 模块, 527

`DocXMLRPCServer` 模块, 527

美元变量替换, 163

###### DOM 接口

- DOM 接口
  - XML 解析, 568
  - 示例, 573

`dont_write_bytecode` 属性, `sys.flags` 的属性, 230

`dont_write_bytecode` 变量, `sys` 模块, 230

双精度浮点数, 38

双击 `.py` 文件, 6

双下划线, 在标识符中的使用, 26

`dropwhile()` 函数, `itertools` 模块, 271

###### `dst()` 方法

- `dst()` 方法
  - `time` 对象的方法, 338
  - `tzinfo` 对象的方法, 342

鸭子类型, 122

`dumbdbm` 模块, 310

###### `dump()` 函数

- `dump()` 函数
  - `json` 模块, 564
  - `marshal` 模块, 226
  - `pickle` 模块, 171, 227
  - `xml.etree.ElementTree` 模块, 578

###### `dump()` 方法, `Pickler` 对象的方法

- `dump()` 方法, `Pickler` 对象的方法, 228

###### `dumps()` 函数

- `dumps()` 函数
  - `json` 模块, 564
  - `marshal` 模块, 226
  - `pickle` 模块, 227
  - `xmlrpc.client` 模块, 526

###### `dup()` 函数, `os` 模块

- `dup()` 函数, `os` 模块, 382

`dup2()` 函数, `os` 模块, 382

动态绑定, 对象属性, 122

动态加载, 模块, 144

动态作用域, 缺乏, 97

变量的动态类型, 7

#### E

- `-E` 命令行选项, 173

`e` 变量, `math` 模块, 252

`EAI_*` 常量, `socket` 模块, 485

##### `east_asian_width()` 函数, `unicodedata` 模块

- `east_asian_width()` 函数, `unicodedata` 模块, 296

##### `easy_install` 命令, `setuptools` 包

- `easy_install` 命令, `setuptools` 包, 155

##### `.egg` 文件

- `.egg` 文件, 154
  - 与模块, 147
  - 与站点配置, 177
  - 结构, 147

##### `Element` 类, `xml.dom.minidom` 模块

- `Element` 类, `xml.dom.minidom` 模块, 572

##### `Element()` 函数, `xml.etree.ElementTree` 模块

- `Element()` 函数, `xml.etree.ElementTree` 模块, 575

`ElementTree` 类, `xml.etree.ElementTree` 模块, 573

##### `ElementTree` 接口, XML 解析

- `ElementTree` 接口, XML 解析, 569

`ElementTree`, 示例, 578

`elif` 语句, 9, 81

###### 省略号

- 省略号, 30, 51, 54
  - Python 3 中的表达式, 626
  - 类型, 51
  - 在扩展切片中的使用, 59
  - 在索引方法中的使用, 54

###### `else` 子句

- `else` 子句
  - `try` 语句的, 86
  - `while` 和 `for` 循环的, 84

###### `else` 语句

- `else` 语句, 9, 81

###### 电子邮件消息

- 电子邮件消息
  - 撰写, 555
  - 撰写和发送示例, 558
  - 发送示例, 514
  - 解析, 552

###### `email` 包

- `email` 包, 552

###### `Emax` 属性, `Context` 对象的属性

- `Emax` 属性, `Context` 对象的属性, 247

###### 在网页中嵌入 Unicode 字符

- 在网页中嵌入 Unicode 字符, 167

###### 将解释器嵌入 C 程序

- 将解释器嵌入 C 程序, 591, 608

###### 嵌入

- 嵌入
  - 从 C 调用函数, 610
  - 将 Python 类型转换为 C, 611

###### `Emin` 属性, `Context` 对象的属性

- `Emin` 属性, `Context` 对象的属性, 247

###### `Empty` 异常, `Queue` 模块

- `Empty` 异常, `Queue` 模块, 418, 445

###### 空字典

- 空字典, 16

空列表, 12

###### `empty()` 方法, `Queue` 对象的方法

- `empty()` 方法, `Queue` 对象的方法, 418, 445

###### 启用调试器命令, `pdb` 模块

- 启用调试器命令, `pdb` 模块, 188

###### `enable()` 函数

- `enable()` 函数
  - `cgitb` 模块, 539
  - `gc` 模块, 220



## **F**

-   F_* 常量，`fcntl()` 函数，347
-   f_* 属性
    -   帧对象的，52
    -   statvfs 对象的，389
-   `fabs()` 函数，math 模块，251
-   `factorial()` 函数，math 模块，251
-   `fail()` 方法，TestCase 对象的，185
-   `failIf()` 方法，TestCase 对象的，185
-   `failIfAlmostEqual()` 方法，TestCase 对象的，185
-   `failIfEqual()` 方法，TestCase 对象的，185
-   `failUnless()` 方法，TestCase 对象的，185
-   `failUnlessAlmostEqual()` 方法，TestCase 对象的，185
-   `failUnlessEqual()` 方法，TestCase 对象的，185
-   `failUnlessRaises()` 方法，TestCase 对象的，185
-   `failureException` 属性，TestCase 对象的，185
-   `False` 值，9、27、38
-   `family` 属性，socket 对象的，484
-   `Fault` 异常，xmlrpc.client 模块，527
-   `fchdir()` 函数，os 模块，379
-   `fchmod()` 函数，os 模块，382
-   `fchown()` 函数，os 模块，382
-   fcntl 模块，347
-   `fcntl()` 函数，fcntl 模块，347
-   `fdatasync()` 函数，os 模块，382
-   `fdopen()` 函数，os 模块，382
-   `feed()` 方法，HTMLParser 对象的，561
-   `fetchall()` 方法，Cursor 对象的，299
-   获取 URL
    -   示例，514
    -   带身份验证的示例，519
    -   带 cookies 的示例，519
-   `fetchmany()` 方法，Cursor 对象的，299
-   `fetchone()` 方法，Cursor 对象的，298
-   `FieldStorage()` 函数，cgi 模块，534
-   文件 I/O，10
-   `file` 属性，FieldStorage 对象的，535
-   文件描述符，347
    -   操作函数，382
-   `file` 关键字参数，`print()` 函数的，10（快捷方式）、163
-   文件锁定，348
    -   Windows，373
    -   sqlite3 模块的，303
-   文件模式，与 `open()` 函数配合使用，159
-   文件上传，在 CGI 脚本中，536
-   `__file__` 属性，模块的，51
-   文件类对象，122
-   `file_offset` 属性，ZipInfo 对象的，327
-   `file_size` 属性，ZipInfo 对象的，327
-   filecmp 模块，314
-   `fileConfig()` 函数，logging 模块，367
-   `FileCookieJar` 类，http.cookiejar 模块，513
-   `FileHandler` 类
    -   logging 模块，362
    -   urllib.request 模块，518
-   `FileIO` 类，io 模块，350
-   `filename` 属性
    -   FieldStorage 对象的，535
    -   Record 对象的，359
    -   ZipInfo 对象的，327
-   文件名
    -   Windows 驱动器盘符，399
    -   绝对路径，396
    -   在 Python 3 中，633
    -   使用 shell 通配符匹配，316
    -   可移植操作，396
    -   拆分为目录和基本名称，398
    -   测试是否存在，396
    -   测试是否为目录，397
    -   测试是否为链接，397
-   文件名 661
-   如何让本索引更有用？请发邮件至 indexes@samspublishing.com

`enable_callback_tracebacks()` 函数，sqlite3 模块

-   `enable_callback_tracebacks()` 函数，sqlite3 模块，305
-   `enable_intersperced_args()` 方法，OptionParser 对象的，376
-   在 Python 2.6 中启用 `print()` 函数，163
-   封装，127
-   `encode()` 函数
    -   base64 模块，547
    -   quopri 模块，568
-   `encode()` 方法
    -   在 Python 3 中，629
    -   CodecInfo 对象的，277
    -   IncrementalEncoder 对象的，278
    -   JSONEncoder 对象的，566
    -   字符串的，42、165-166
    -   正确使用方法，166
-   `EncodedFile` 类，codecs 模块，279
-   `EncodedFile` 对象，codecs 模块，167
-   `encodestring()` 函数
    -   base64 模块，547
    -   quopri 模块，568
-   `encoding` 参数，`open()` 函数的，159
-   `encoding` 属性
    -   TextIOWrapper 对象的，353
    -   文件的，161
-   网络编程中的编码问题，452
-   源代码编码，31
-   `end` 属性，切片的，54
-   `end` 关键字参数，`print()` 函数的，163
-   `end()` 方法
    -   MatchObject 对象的，286
    -   TreeBuilder 对象的，577
-   `end_headers()` 方法，BaseHTTPRequestHandler 对象的，509
-   `endDocument()` 方法，ContentHandler 对象的，581
-   `endElement()` 方法，ContentHandler 对象的，581
-   `endElementNS()` 方法，ContentHandler 对象的，581
-   `endheaders()` 方法，HTTPConnection 对象的，503
-   `endpos` 属性，MatchObject 对象的，286
-   `endPrefixMapping()` 方法，ContentHandler 对象的，581
-   `endswith()` 方法，字符串的，42
-   `__enter__()` 方法，上下文管理器的，62、89
-   `enumerate()` 函数，83、204
    -   threading 模块，443
-   `EnumKey()` 函数，winreg 模块，409
-   `EnumValue()` 函数，winreg 模块，409
-   `environ` 变量，os 模块，158
-   `environ` 变量，os 模块，379
-   环境变量，158、379
    -   Python 3，633
    -   WSGI，540
    -   在文件名中展开，397
    -   在 CGI 脚本中，533
    -   取消设置，381
    -   解释器使用的，174
-   `EnvironmentError` 异常，87、212
-   EOF 字符，交互模式，7
-   EOF 指示，文件 I/O，160
-   `EOFError` 异常，87、213
-   `epilogue` 属性，Message 对象的，554
-   epoll 接口，Linux，460
-   `epsilon` 属性，`sys.float_info` 的，231
-   `eq()` 函数，operator 模块，274
-   `__eq__()` 方法，57
-   等于运算符 `==`，66、78
-   对象的相等比较，34
-   `errcheck` 属性，ctypes 函数对象的，613
-   errno 模块，343
-   错误代码，系统错误列表，344
-   `error` 异常，396
    -   socket 模块，485
-   错误消息，157
-   `error()` 方法，Logger 对象的，357
-   `error_message_format` 属性，BaseHTTPRequestHandler 类的，508
-   `errorcode` 变量，errno 模块，344
-   `errorlevel` 属性，TarFile 对象的，320
-   `errors` 属性，TextIOWrapper 对象的，353

errors 参数

-   编码函数的，166
-   `open()` 函数的，159

转义码

-   在字符串字面量中禁用，29
-   在字符串字面量中，27
-   非打印字符，28

`escape()` 函数

-   cgi 模块，536
-   re 模块，283
-   xml.sax.saxutils 模块，583

在 HTML 中转义字符，536

`eval()` 函数，55、77、115、204、206

-   与 `repr()`，55

求值

-   函数参数的，76
-   运算符优先级和结合性，78
-   求值顺序，78

Event 对象

-   multiprocessing 模块，427
-   threading 模块，440

事件循环

-   与 asyncore 模块，455
-   协程，108

`Event()` 方法，Manager 对象的，429

事件驱动 I/O，415

-   轮询信号，399
-   何时考虑使用，467

`EX_*` 退出码常量，391

`exc_clear()` 函数，sys 模块，233

`exc_info` 属性，Record 对象的，359

`exc_info()` 函数，sys 模块，53、89、233

`except` 语句，22、84-85

-   语法变更，85

`__excepthook__` 变量，sys 模块，230

`excepthook()` 函数，sys 模块，85、233

`Exception` 类，212

`Exception` 异常，87

扩展模块中的异常处理，605

`exception()` 方法，Logger 对象的，358

异常，22、84-85

-   与锁，23
-   异常的属性，212
-   捕获所有异常，85
-   捕获多种类型，85
-   捕获所有异常的注意事项，86
-   Python 3 中的异常链，626
-   清除最后的异常，233
-   定义新异常，88
-   与警告的区别，216
-   系统错误的错误代码，344
-   `finally` 语句，86
-   异常处理，22-23
-   异常层次结构，88
-   忽略异常，85
-   内置异常列表，87
-   匹配规则，85
-   优化策略，196
-   性能，197
-   异常传播，85
-   重新抛出最后的异常，84
-   异常的值，23、85

`.exe` 文件，使用 distutils 创建，153

`exec` 语句，遗留代码注意事项，115

`exec()` 函数，115、204

-   Python 3，631

`exec_prefix` 变量，sys 模块，177、230

`execl()` 函数，os 模块，390

`execle()` 函数，os 模块，390

`execlp()` 函数，os 模块，390

`executable` 变量，sys 模块，230

`execute()` 方法

-   Connection 对象的，306
-   Cursor 对象的，298

`executemany()` 方法

-   Connection 对象的，306
-   Cursor 对象的，298

`executemany()` 方法 659

`executescript()` 方法，Connection 对象的，306

执行程序，6

将字符串作为代码执行，115

执行系统命令，331

-   `popen()` 函数，392
-   subprocess 模块，402
-   `system()` 函数，393

执行模型，81

`__init__.py` 文件的执行，150

类体的执行，117、138

`execv()` 函数，os 模块，390

`execve()` 函数，os 模块，391

`execvp()` 函数，os 模块，391

`execvpe()` 函数，os 模块，391

`exists()` 函数，os.path 模块，396

`_exit()` 函数，os 模块，179、391

`exit()` 函数，sys 模块，179、233

`__exit__()` 方法，63

-   上下文管理器的，62、89

`exitcode` 属性，Process 对象的，417

`exp()` 函数，math 模块，251

`exp()` 方法，Decimal 对象的，243

`expand()` 方法，MatchObject 对象的，285

`ExpandEnvironmentStrings()` 函数，winreg 模块，409

`expandtabs()` 方法，字符串的，41-42

`expanduser()` 函数，os.path 模块，397

`expandvars()` 函数，os.path 模块，397

指数，浮点数范围，38

`expovariate()` 函数，random 模块，255

表达式，7

`extend()` 方法

-   array 对象的，260
-   deque 对象的，262
-   列表的，40

扩展切片，39、59

-   赋值，40、69
-   删除，40、69
-   在序列上，68
-   扩展切片运算符 `[:]`，67

可迭代对象的扩展解包，Python 3，623

`ExtendedContext`，decimal 模块，248

使用 C 扩展，591

`extendleft()` 方法，deque 对象的，262

使用模块编写可扩展代码，144

扩展模块，591

-   使用 distutils 编译，596
-   将 C 类型转换为 Python 类型，602
-   将 Python 类型转换为 C 类型，597
-   ctypes 模块，612
-   在 Python 3 中的差异，595
-   文档字符串，595
-   异常处理，605
-   全局解释器锁，607
-   手写，593
-   手动编译，597
-   命名，595
-   引用计数，607
-   线程，607
-   包装函数，594

`Extension()` 函数，distutils 模块，596

`extensions_map` 属性，HTTPRequestHandler 类的，508

`external_attr` 属性，ZipInfo 对象的，327

`extra` 属性，ZipInfo 对象的，327

`extract()` 方法

-   TarFile 对象的，320
-   ZipFile 对象的，325

`extract_stack()` 函数，traceback 模块，236

`extract_tb()` 函数，traceback 模块，236

`extract_version` 属性，ZipInfo 对象的，327

`extractall()` 方法，ZipFile 对象的，325

`ExtractError` 异常，tarfile 模块，322

`extractfile()` 方法，TarFile 对象的，320

`extsep` 变量，os 模块，386

如何让本索引更有用？请发邮件至 indexes@samspublishing.com



- Connection 对象的 fileno() 方法，421
- IOBase 对象的 fileno() 方法，349
- SocketServer 对象的 fileno() 方法，491
- 文件的 fileno() 方法，160-161
- 文件和套接字的 fileno() 方法，459
- 套接字对象的 fileno() 方法，478
- urlopen 对象的 fileno() 方法，515

##### 文件，10

- 绝对路径，396
- 与 Python 3，160
- 属性，161
- 缓冲区大小，159
- 带缓冲的二进制 I/O，351
- bz2 压缩，313
- 比较，314
- 复制，318
- 创建时间，397
- 解码为 Unicode，167
- 文件模式描述，159
- 检测文件结束符（EOF），160
- 文件指针，161，352
- 在文件系统上查找，390
- 操作元数据的函数，386
- gzip 压缩，317
- 按行迭代，17-18
- 最后修改时间，397
- 在 Windows 上锁定，373
- 底层控制，347
- 底层系统调用，382
- 内存映射，370
- 方法，159
- 打开，10，158-159
- 使用 Unicode 解码打开，167
- 解析 CSV，548
- io 库模块的问题，354
- 原始二进制 I/O，350
- 逐行读取，10
- 定位，161
- 大小，397
- softspace 属性和 print 语句，162
- 临时文件，323
- 测试存在性，396
- 类型，159
- 写入，159

- 字符串格式说明符中的填充字符，73

- Filter 类，logging 模块，359

###### filter() 函数，205

- 与 Python 3，205
- 与优化，197
- fnmatch 模块，316
- future_builtins 模块，217

- filterwarnings() 函数，warnings 模块，239

###### finally 语句，86

- 与锁，442

###### find() 方法

- Element 对象的，576
- ElementTree 对象的，574
- mmap 对象的，371
- 字符串的，41-42

- find_library() 函数，ctypes 模块，612

- findall() 函数，re 模块，283

###### findall() 方法

- Element 对象的，576
- ElementTree 对象的，574
- Regex 对象的，285

- findCaller() 方法，Logger 对象的，358

- 查找所有已加载的模块，144

- 查找文件，390

- finditer() 函数，re 模块，284

- finditer() 方法，Regex 对象的，285

###### findtext() 方法

- Element 对象的，576
- ElementTree 对象的，574

- finish() 方法，BaseRequestHandler 对象的，490

###### 一等公民对象，36

- 用途，37

- firstChild 属性，DOM Node 对象的，570

- flag_bits 属性，ZipInfo 对象的，327

###### flags 属性

- Context 对象的，247
- Regex 对象的，284

- flags 变量，sys 模块，230

致命错误，在扩展模块中，595

浮点数类型，38

float() 函数，13，62，76，205

\_\_float\_\_() 方法，61-62

- 与类型强制转换，134

float_info 变量，sys 模块，231

###### 浮点数，27

- 作为字典键，16
- 二进制表示，39
- 与十进制数比较，243
- 转换为分数，39，250
- 定义 NaN 和 Inf，213，252
- 不精确表示，12，243
- 底层属性，231
- 与复数混合，39
- 精度，38
- 随机数分布，255
- 表示，38

FloatingPointError 异常，87，213

- flock() 函数，fcntl 模块，348

整除，65

- floor() 函数，math 模块，251

- floordiv() 函数，operator 模块，273

\_\_floordiv\_\_() 方法，60

###### flush() 方法

- BZ2Compressor 对象的，314
- BufferWriter 对象的，352
- Handler 对象的，364
- IOBase 对象的，349
- compressobj 对象的，328
- decompressobj 对象的，329
- 文件的，160
- mmap 对象的，371

- FlushKey() 函数，winreg 模块，409

- fma() 方法，Decimal 对象的，243

- fmod() 函数，math 模块，251

- fnmatch 模块，316

- fnmatch() 函数，fnmatch 模块，316

- fnmatchcase() 函数，fnmatch 模块，316

- 脚，如何踢，36，86，442，617

###### for 语句，10，17，59，69，82

- 与文件，10，160
- 与生成器，19
- 与元组解包，15

- 强制垃圾回收，220

- 外部函数接口，ctypes 模块，612

- fork() 函数，os 模块，391

- ForkingMixin 类，SocketServer 模块，493

- ForkingTCPServer 类，SocketServer 模块，494

- ForkingUDPServer 类，SocketServer 模块，494

- forkpty() 函数，os 模块，392

- format 属性，Struct 对象的，291

###### 格式代码

- 用于日期和时间，406
- 用于字符串格式运算符 %，70-71

###### 格式说明符

- 对齐字符，73
- 自定义，74
- 填充字符，73
- 字符串的 format() 方法，72-74
- 字段嵌套，74

###### format() 函数，8，11-12，56，77，205

###### format() 方法

- 格式说明符代码，72
- Formatter 对象的，288
- 字符串的，8，42-43，56，72-73，162
- 字符串与变量插值，164

\_\_format\_\_() 方法，55-56，74

- format_exc() 函数，traceback 模块，236

- format_exception() 函数，traceback 模块，236

- format_exception_only() 函数，traceback 模块，236

- format_list() 函数，traceback 模块，236

- format_stack() 函数，traceback 模块，236

- format_tb() 函数，traceback 模块，236

- format_value() 方法，Formatter 对象的，289

- formatargspec() 函数，inspect 模块，222

- formatargvalues() 函数，inspect 模块，222

- 格式化打印，8，70-71，162

- 格式化字符串，42，71-72

###### Formatter 类

- logging 模块，365
- string 模块，288

- formatter 模块，587

- 格式化，日志消息的，358，365

- formatwarning() 函数，warnings 模块，239

- Fortran 公共块，缺乏，146

- found_terminator() 方法，asyncchat 对象的，453

- fpathconf() 函数，os 模块，382

- fpectl 模块，585

- fpformat 模块，586

- Fraction 类，fractions 模块，250

- fractions 模块，39，250

###### fragment 属性

- urlparse 对象的，520
- urlsplit 对象的，521

###### 帧对象，51-52

- 属性，52

FrameType 类型，51，237

- 自由变量，在函数中，98

- freeze_support() 函数，multiprocessing 模块，434

- frexp() 函数，math 模块，251

- from __future__ import，178

###### from 模块 import *，24，145

- 全局变量，146
- 带下划线的标识符，26
- \_\_all\_\_ 变量，145

###### from 语句

- 与 import 语句，24
- 模块导入，145

- from_address() 方法，ctypes 类型对象的，616

- from_buffer() 方法，ctypes 类型对象的，616

- from_buffer_copy() 方法，ctypes 类型对象的，616

- from_decimal() 方法，FloatingPoint 类的，250

- from_float() 方法，Fraction 类的，250

- from_iterable() 方法，对象的，270

- from_param() 方法，ctypes 类型对象的，616

- fromfd() 函数，socket 模块，473

- fromfile() 方法，array 对象的，260

- fromhex() 方法，浮点数的，39

- fromkeys() 方法，字典的，45

- fromlist() 方法，array 对象的，260

###### fromordinal() 方法

- date 类的，336
- datetime 类的，339

- fromstring() 函数，xml.etree.ElementTree 模块，575

- fromstring() 方法，array 对象的，260

###### fromtimestamp() 方法

- date 类的，336
- datetime 类的，339

- fromutc() 方法，tzinfo 对象的，342

- frozenset 类型，38，46，75

- frozenset() 函数，77，205

- fstat() 函数，os 模块，383

- fstatvfs() 函数，os 模块，383

- fsum() 函数，math 模块，251

- fsync() 函数，os 模块，383

- FTP 服务器，上传文件到，500

- FTP() 函数，ftplib 模块，497

- FTPHandler 类，urllib.request 模块，518

- ftplib 模块，497

- ftruncate() 函数，os 模块，383

- Full 异常，Queue 模块，418，445

- full() 方法，Queue 对象的，418，445

- func 属性，partial 对象的，268

\_\_func\_\_ 属性，方法的，49

- funcName 属性，Record 对象的，359

函数调用运算符 ()，47，76

###### 函数，18

- \_\_doc\_\_ 属性，24
- 与协程，20
- 与生成器，19
- Python 3 中的注解，624
- 匿名，112
- 作为闭包，98
- 作为字典值，37
- 作为对象，98
- 属性与装饰器，102
- 属性，48
- 默认值绑定，93
- 内置，201
- 回调，98
- 调用，18，93
- func_* 属性名称的更改，48
- 更改递归限制，112，235
- 将属性复制到装饰器，269
- 创建包装器，100
- 装饰器，101
- 装饰器与属性，114
- 默认参数，18，93
- 定义，93
- 使用线程延迟执行，437
- 文档字符串，48，113
- 参数求值，76
- 接受任意数量参数的示例，95
- 自由变量，98
- 关键字参数，18，94
- lambda 运算符，112
- 修改全局变量，18
- 可变参数，95
- 嵌套，97，99
- 可选参数和 None，38
- 参数传递，95
- 部分求值，76，268
- 序列化，228
- 递归，112
- 从函数返回多个值，18，96
- 在调试器中运行，186
- 作用域规则，18，96
- 副作用，95
- 终止函数，219
- 内置函数类型，49
- 用户定义函数类型，47
- 用户定义，48
- 用户定义属性，114
- 可变参数，94
- 可变数量关键字参数，95

FunctionType 类型，47，237

- functools 模块，76，114，268

函数子，62

- funny_files 属性，dircmp 对象的，315

- 未来特性，启用，178

## \_\_future\_\_ 模块，178

- 与除法，62
- 特性列表，178

- future_builtins 模块，217

FutureWarning 警告，216，238

- 模糊日期和时间解析，343

#### G

- gaierror 异常，socket 模块，485

- gammavariate() 函数，random 模块，255

##### 垃圾回收，34-35，220

- 与 \_\_del\_\_() 方法，129
- 与循环，35
- 与程序终止，179
- 过程描述，221
- 观察者模式示例，130
- \_\_del\_\_() 方法的问题，221

garbage 变量，gc 模块，220

- gauss() 函数，random 模块，255

- gc 模块，35，179，220

- gcd() 函数，fractions 模块，251

- gdbm 模块，310

- ge() 函数，operator 模块，274

\_\_ge\_\_() 方法，56

##### 生成器表达式，109-110

##### 生成器

- 生成器表达式
- 条件表达式，79
- 转换为列表，110
- 与列表推导式的区别，110
- 生成器函数，以及上下文管理器，90
- 生成器对象，51, 53
  - 其属性，53
- GeneratorExit 异常，87, 104, 213
- 生成器，19, 102-103
  - 与迭代中的 break 语句，103
  - 与内存效率，107
  - 与处理管道，19
  - 关闭，53
  - 并发编程，446
  - 执行模型，19
  - GeneratorExit 异常处理，213
  - 多任务示例，447
  - 实际应用，106
  - 递归，112
  - 在生成器中抛出异常，53
  - 与 I/O 结合使用，164-165
  - 与 WSGI 结合使用，165
- GeneratorType 类型，51, 237
- get() 函数，webbrowser 模块，544
- get() 方法
  - AsyncResult 对象的方法，425
  - ConfigParser 对象的方法，333
  - Element 对象的方法，576
  - Message 对象的方法，552
  - Queue 对象的方法，418, 445
  - 字典的方法，16, 45
- \_\_get\_\_() 方法，描述符的方法，58, 126
- get\_all() 方法，Message 对象的方法，552
- get\_boundary() 方法，Message 对象的方法，552
- get\_charset() 方法，Message 对象的方法，553
- get\_charsets() 方法，Message 对象的方法，553
- get\_content\_charset() 方法，Message 对象的方法，553
- get\_content\_maintype() 方法，Message 对象的方法，553
- get\_content\_subtype() 方法，Message 对象的方法，553
- get\_content\_type() 方法，Message 对象的方法，553
- get\_count() 函数，gc 模块，221
- get\_data() 方法，Request 对象的方法，517
- get\_debug() 函数，gc 模块，221
- get\_default\_type() 方法，Message 对象的方法，553
- get\_dialect() 函数，csv 模块，551
- get\_errno() 函数，ctypes 模块，617
- get\_field() 方法，Formatter 对象的方法，288
- get\_filename() 方法，Message 对象的方法，553
- get\_full\_url() 方法，Request 对象的方法，517
- get\_host() 方法，Request 对象的方法，517
- get\_last\_error() 函数，ctypes 模块，617
- get\_logger() 函数，multiprocessing 模块，435
- get\_method() 方法，Request 对象的方法，517
- get\_nowait() 方法，Queue 对象的方法，418, 445
- get\_objects() 函数，gc 模块，221
- get\_origin\_req\_host() 方法，Request 对象的方法，517
- get\_osfhandle() 函数，msvcrt 模块，372
- get\_param() 方法，Message 对象的方法，553
- get\_params() 方法，Message 对象的方法，553
- get\_payload() 方法，Message 对象的方法，554
- get\_referents() 函数，gc 模块，221
- get\_referrers() 函数，gc 模块，221
- get\_selector() 方法，Request 对象的方法，517
- get\_server\_certificate() 函数，ssl 模块，488
- get\_starttag\_text() 方法，HTMLParser 对象的方法，561
- get\_terminator() 方法，asynchat 对象的方法，453
- get\_threshold() 函数，gc 模块，221
- get\_type() 方法，Request 对象的方法，517
- get\_unixfrom() 方法，Message 对象的方法，554
- get\_value() 方法，Formatter 对象的方法，289
- getaddrinfo() 函数，socket 模块，473
- getargspec() 函数，inspect 模块，222
- getargvalues() 函数，inspect 模块，222
- getatime() 函数，os.path 模块，397
- getattr() 函数，205
  - 与私有属性，128
- \_\_getattr\_\_() 方法，57
  - 与 \_\_slots\_\_，133
- getAttribute() 方法，DOM Element 对象的方法，572
- \_\_getattribute\_\_() 方法，57-58, 132
  - 与 \_\_slots\_\_，133
- getAttributeNS() 方法，DOM Element 对象的方法，572
- getboolean() 方法，ConfigParser 对象的方法，333
- getch() 函数，msvcrt 模块，372
- getche() 函数，msvcrt 模块，372
- getcheckinterval() 函数，sys 模块，234
- getchildren() 方法，Element 对象的方法，577
- getclasstree() 函数，inspect 模块，222
- getcode() 方法，urlopen 对象的方法，515
- getcomments() 函数，inspect 模块，223
- getcontext() 函数，decimal 模块，247
- getctime() 函数，os.path 模块，397
- getcwd() 函数，os 模块，379
- getcwdu() 函数，os 模块，379
- getdefaultencoding() 函数，sys 模块，166, 234
- getdefaulttimeout() 函数，socket 模块，474
- getdlopenflags() 函数，sys 模块，234
- getdoc() 函数，inspect 模块，223
- getEffectiveLevel() 方法，Logger 对象的方法，360
- getegid() 函数，os 模块，379
- getElementsByTagName() 方法
  - DOM Document 对象的方法，571
  - DOM Element 对象的方法，572
- getElementsByTagNameNS() 方法
  - DOM Document 对象的方法，571
  - DOM Element 对象的方法，572
- geteuid() 函数，os 模块，380
- getfile() 函数，inspect 模块，223
- getfilesystemencoding() 函数，sys 模块，234
- getfirst() 方法，FieldStorage 对象的方法，535
- getfloat() 方法，ConfigParser 对象的方法，333
- getfqdn() 函数，socket 模块，474
- \_getframe() 函数，sys 模块，234
- getframeinfo() 函数，inspect 模块，223
- getgid() 函数，os 模块，380
- getgroups() 函数，os 模块，380
- getheader() 方法，HTTPResponse 对象的方法，504
- getheaders() 方法，HTTPResponse 对象的方法，504
- gethostbyaddr() 函数，socket 模块，474
- gethostbyname() 函数，socket 模块，474
- gethostbyname\_ex() 函数，socket 模块，474
- gethostname() 函数，socket 模块，474
- getinfo() 方法，ZipFile 对象的方法，326
- getinnerframes() 函数，inspect 模块，223
- getint() 方法，ConfigParser 对象的方法，333
- getitem() 函数，operator 模块，274
- \_\_getitem\_\_() 方法，58-59
  - 与切片，59
- getiterator() 方法
  - Element 对象的方法，577
  - ElementTree 对象的方法，574
- getitimer() 函数，signal 模块，399
- getLength() 方法，SAX attributes 对象的方法，582
- getLevelName() 函数，logging 模块，366
- getlist() 方法，FieldStorage 对象的方法，535
- getloadavg() 函数，os 模块，395
- getLogger() 函数，logging 模块，356
- getlogin() 函数，os 模块，380
- getmember() 方法，TarFile 对象的方法，320
- getmembers() 函数，inspect 模块，223
- getmembers() 方法，TarFile 对象的方法，321
- getmodule() 函数，inspect 模块，223
- getmoduleinfo() 函数，inspect 模块，223
- getmodulename() 函数，inspect 模块，224
- getmro() 函数，inspect 模块，224
- getmtime() 函数，os.path 模块，397
- getName() 方法，Thread 对象的方法，436
- getNameByQName() 方法，SAX attributes 对象的方法，582
- getnameinfo() 函数，socket 模块，474
- getNames() 方法，SAX attributes 对象的方法，582
- getnames() 方法，TarFile 对象的方法，321
- getopt 模块，378
- getouterframes() 函数，inspect 模块，224
- getoutput() 函数，commands 模块，331
- getpeercert() 方法，ssl 对象的方法，488
- getpeername() 方法，socket 对象的方法，478
- getpgid() 函数，os 模块，380
- getpgrp() 函数，os 模块，380
- getpid() 函数，os 模块，380
- getpos() 方法，HTMLParser 对象的方法，561
- getppid() 函数，os 模块，380
- getprofile() 函数，sys 模块，234
- getprotobyname() 函数，socket 模块，475
- getQNameByName() 方法，SAX attributes 对象的方法，582
- getQNames() 方法，SAX attributes 对象的方法，582
- getrandbits() 函数，random 模块，254
- getrecursionlimit() 函数，sys 模块，112, 234
- getrefcount() 函数，sys 模块，35, 234
- getresponse() 方法，HTTPConnection 对象的方法，503
- getroot() 方法，ElementTree 对象的方法，574
- getservbyname() 函数，socket 模块，475
- getservbyport() 函数，socket 模块，475
- GetSetDescriptorType 类型，237
- getsid() 函数，os 模块，380
- getsignal() 函数，signal 模块，399
- getsize() 函数，os.path 模块，397
- getsizeof() 函数，sys 模块，192, 234
- getslice() 函数，operator 模块，274
- getsockname() 方法，socket 对象的方法，478
- getsockopt() 方法，socket 对象的方法，478
- getsource() 函数，inspect 模块，224
- getsourcefile() 函数，inspect 模块，224
- getsourcelines() 函数，inspect 模块，224
- getstate() 函数，random 模块，254
- \_\_getstate\_\_() 方法，228
  - 与复制，220
  - 与 pickle 模块，172
- getstatusoutput() 函数，commands 模块，332
- gettarinfo() 方法，TarFile 对象的方法，321
- gettempdir() 函数，tempfile 模块，323
- gettempprefix() 函数，tempfile 模块，323
- gettext 模块，587
- gettimeout() 方法，socket 对象的方法，482
- 获取帮助，help() 函数，24
- 获取当前工作目录，379
- gettrace() 函数，sys 模块，234
- getType() 方法，SAX attributes 对象的方法，582
- getuid() 函数，os 模块，380
- geturl() 方法，urlopen 对象的方法，515
- \_getvalue() 方法，BaseProxy 对象的方法，433
- getValue() 方法，SAX attributes 对象的方法，582
- getvalue() 方法
  - BytesIO 对象的方法，352
  - FieldStorage 对象的方法，535
  - StringIO 对象的方法，354
- getValueByQName() 方法，SAX attributes 对象的方法，582
- getwch() 函数，msvcrt 模块，372
- getwche() 函数，msvcrt 模块，372
- getweakrefcount() 函数，weakref 模块，241
- getweakrefs() 函数，weakref 模块，241
- getwindowsversion() 函数，sys 模块，234
- gi\_\* 属性，生成器对象的属性，53
- gid 属性，TarInfo 对象的属性，321
- glob 模块，317
- glob() 函数，glob 模块，317

##### 全局

- 全局解释器锁，414, 444
  - 与 multiprocessing 模块，444
  - 在扩展中释放，607
- global 语句，18, 96
  - 与模块，143
- 全局变量，96
  - 与 eval()，115
  - 与模块，146
  - 与 C 和 Fortran 的区别，146
  - 在函数中修改，18
  - 在栈帧中的存储，52
- \_\_globals\_\_ 属性，函数的属性，48, 99
- globals() 函数，205
- gmtime() 函数，time 模块，406
- gname 属性，TarInfo 对象的属性，321
- goto 语句，缺失，84
- 灰白胡子黑客，622
- 大于运算符 >，66
- 大于或等于运算符 >=，66
- 绿色线程，446
- greenlets，446
- group() 方法，MatchObject 对象的方法，285
- groupby() 函数，itertools 模块，271
- groupdict() 方法，MatchObject 对象的方法，286
- groupindex 属性，Regex 对象的属性，284
- groups() 方法，MatchObject 对象的方法，285
- grp 模块，586
- gt() 函数，operator 模块，274
- \_\_gt\_\_() 方法，56
- guess\_all\_extensions() 函数，mimetypes 模块，567
- guess\_extension() 函数，mimetypes 模块，567
- guess\_type() 函数，mimetypes 模块，566
- GUI 编程，使用偏函数求值，268
- GUI，以及网络编程，467, 669

#### H

gzip 模块，317

GzipFile() 函数，gzip 模块，317

-h 命令行选项，173

h(elp) 调试器命令，pdb 模块，188

handle() 函数，cgitb 模块，539

handle() 方法，BaseRequestHandler 对象的方法，490

handle_accept() 方法，dispatcher 对象的方法，455

handle_charref() 方法，HTMLParser 对象的方法，561

handle_close() 方法，dispatcher 对象的方法，455

handle_comment() 方法，HTMLParser 对象的方法，561

handle_connect() 方法，dispatcher 对象的方法，455

handle_data() 方法，HTMLParser 对象的方法，561

handle_decl() 方法，HTMLParser 对象的方法，561

handle_endtag() 方法，HTMLParser 对象的方法，562

handle_entityref() 方法，HTMLParser 对象的方法，562

handle_error() 方法，SocketServer 类的方法，493

dispatcher 对象的方法，455

handle_expt() 方法，dispatcher 对象的方法，456

handle_pi() 方法，HTMLParser 对象的方法，562

handle_read() 方法，dispatcher 对象的方法，456

handle_startendtag() 方法，HTMLParser 对象的方法，562

handle_starttag() 方法，HTMLParser 对象的方法，562

handle_timeout() 方法，SocketServer 类的方法，493

handle_write() 方法，dispatcher 对象的方法，456

has_data() 方法，Request 对象的方法，517

has_header() 方法，Request 对象的方法，517

Sniffer 对象的方法，550

has_ipv6 变量，socket 模块，475

has_key() 方法，字典的方法，45

has_option() 方法，ConfigParser 对象的方法，333

has_section() 方法，ConfigParser 对象的方法，333

hasattr() 函数，205

与私有属性，128

hasAttribute() 方法，DOM Element 对象的方法，572

hasAttributeNS() 方法，DOM Element 对象的方法，572

hasAttributes() 方法，DOM Node 对象的方法，571

hasChildNodes() 方法，DOM Node 对象的方法，571

哈希表，16，44

基于哈希表的数据库，310

hash() 函数，205

__hash__() 方法，56

Hashable 抽象基类，265

hashlib 模块，559

示例，425

header_offset 属性，ZipInfo 对象的属性，327

BaseHTTPRequestHandler 对象，509

FieldStorage 对象的属性，535

堆，269

heapify() 函数，heapq 模块，269

heapmin() 函数，msvcrt 模块，372

heappop() 函数，heapq 模块，269

heappush() 函数，heapq 模块，269

heappushpop() 函数，heapq 模块，270

heapq 模块，269

heapreplace() 函数，heapq 模块，270

hello world 程序，5

help() 函数，24，206

装饰器导致的怪异输出，113

herror 异常，socket 模块，485

hex() 函数，77，206

future_builtins 模块，217

hex() 方法，浮点数的方法，39

十六进制

- 从整数创建字符串，77
- 整数字面量，27

hexdigest() 方法

- 摘要对象的方法，559
- hmac 对象的方法，560

hexdigits 变量，string 模块，287

hexversion 变量，sys 模块，231

从 dir() 函数中隐藏属性名，128

分层锁，442

分层日志，logging 模块，360

异常层次结构，87-88

对象层次结构，137

HIGHEST_PROTOCOL 常量，pickle 模块，172

HKEY_* 常量，winreg 模块，408

HMAC 认证，559

hmac 模块，559

hostname 属性

- urlparse 对象的属性，520
- urlsplit 对象的属性，521

主机名，获取主机机器的主机名，474

hour 属性，time 对象的属性，338

HTML 表单

- 示例，531
- 使用 urllib 包上传，515

HTML 解析，561

html.parser 模块，561

HTMLParser 类，html.parser 模块，561

HTMLParser 模块，参见 html.parser，561

HTMLParserError 异常，html.parser 模块，562

htonl() 函数，socket 模块，475

htons() 函数，socket 模块，475

HTTP cookies，511

HTTP 协议

- 描述，500
- 请求方法，501
- 响应代码，501

HTTP 服务器

- 自定义请求处理，510
- 使用 asynchat 模块的示例，453
- 使用 asyncore 模块的示例，457
- 使用协程的示例，466
- 使用防火墙的示例，507
- 独立示例，508
- 在 POST 请求中上传文件，505

http 包，500

http.client 模块，502

http.cookiejar 模块，513

http.cookies 模块，511

http.server 模块，506

HTTPBasicAuthHandler 类，urllib.request 模块，518-519

HTTPConnection() 函数，http.client 模块，502

HTTPCookieProcessor 类，urllib.request 模块，518-519

HTTPDefaultErrorHandler 类，urllib.request 模块，518

HTTPDigestAuthHandler 类，urllib.request 模块，518-519

HTTPError 异常，urllib.error 模块，523

HTTPException 异常，http.client 模块，504

HTTPHandler 类

- logging 模块，362
- urllib.request 模块，518

httplib 模块，参见 http.client，502

HTTPRedirectHandler 类，urllib.request 模块，518

HTTPResponse 对象，http.client 模块，504

HTTPSConnection() 函数，http.client 模块，502

HTTPServer 类，http.server 模块，506

HTTPSHandler 类，urllib.request 模块，518

hypot() 函数，math 模块，251

ignore_environment 属性，sys.flags 的属性，230

ignore_pattern() 函数，shutil 模块，318

ignore_zeros 属性，TarFile 对象的属性，321

在 __del__ 中被忽略的 NameError 异常，179

忽略异常，85

-i 命令行选项，173-174

I/O 缓冲，与生成器，165

I/O 多路复用，459

__iadd__() 方法，61

__iand__() 方法，61

IBM 通用十进制算术标准，243

id() 函数，33，206

ident 属性，Thread 对象的属性，436

标识符，26

- 与一等数据，36
- 大小写敏感性，26
- 保留字，26
- 下划线的使用，26
- Python 3 中 Unicode 的使用，622

对象的身份比较，34

对象的身份，33

身份运算符 is，78

__idiv__() 方法，61

__idivmod__() 方法，61

IDLE，5-6

- 与标准 I/O 流，162

IEEE 754，243

if 语句，9，81

- 与 __debug__ 变量，91

ifilter() 函数，itertools 模块，271

ifilterfalse() 函数，itertools 模块，271

__ifloordiv__() 方法，61

iglob() 函数，glob 模块，317

ignorableWhitespace() 方法，ContentHandler 对象的方法，581

ignore 调试器命令，pdb 模块，188

'ignore' 错误处理，Unicode 编码，166

__ilshift__() 方法，61

imag 属性

- 复数的属性，39
- 浮点数的属性，39

imap() 函数，itertools 模块，272

imap() 方法，Pool 对象的方法，424

imap_unordered() 方法，Pool 对象的方法，424

imaplib 模块，587

imghdr 模块，588

不可变性，元组的特性，14

不可变类型，从其继承，55

不可变，定义，33

__imod__() 方法，61

imp 模块，224，585

隐式类型转换，缺乏，62

import 语句，13，23-24，50，143-144

- Python 3，151
- 包中的绝对导入，151
- 与主程序，146
- 与 sys.modules，144
- 与 sys.path 变量，147
- as 限定符，144
- 大小写敏感性，148
- .pyc 文件的编译，148
- 模块的执行，143
- 模块搜索路径，147
- 多个模块，144
- 模块的一次性执行，144
- 包，150
- 在程序中的放置位置，144
- 相对包导入，150-151
- 已加载代码的作用域规则，145
- 模块的类型，148

ImportError 异常，87，148，214

从模块导入选定符号，145

**ImproperConnectionState** 异常，http.client 模块，504

__imul__() 方法，61

in 运算符，9

- 与 __contains__ 方法，58
- 与检查子字符串，69
- 用于字典，16，45，74
- 用于序列，67，69

原地赋值运算符，75

原地文件更新，159

原地数学运算符，61

原地修改

- 列表的，40
- 集合的，47

in_dll() 方法，ctypes 类型对象的方法，616

INADDR_* 常量，socket 模块，478

**IncompleteRead** 异常，http.client 模块，504

**IncrementalDecoder** 类，codecs 模块，279

incrementaldecoder() 方法，CodecInfo 对象的方法，279

**IncrementalEncoder** 类，codecs 模块，278

incrementalencoder() 方法，CodecInfo 对象的方法，278

缩进，8，25

- 与文档字符串，30
- 与行续接符 \，9
- 与制表符，26
- 推荐风格，8
- 将语句放在同一行，25

**IndentationError** 异常，87，214

index() 方法

- 数组对象的方法，260
- 列表的方法，40-41
- 字符串的方法，41，43

**IndexError** 异常，69，87，214

索引运算符 []，39，67

- 用于列表，12
- 用于序列，68
- 用于字符串，11
- 用于元组，14

索引，从 0 开始，11

indexOf() 函数，operator 模块，274

indices() 方法，切片的方法，54

inet_aton() 函数，socket 模块，475

inet_ntoa() 函数，socket 模块，476

inet_ntop() 函数，socket 模块，476

inet_pton() 函数，socket 模块，476

浮点数的不精确表示，12

**Inf** 变量，decimal 模块，248

**Inf**

- decimal 模块，244
- 无穷大，213

info() 方法

- Logger 对象的方法，357
- urlopen 对象的方法，515

infolist() 方法，ZipFile 对象的方法，326

继承，21，119

- 类的 __mro__ 属性，121
- 抽象基类，137
- 属性绑定，119
- 调用超类方法，120
- 从内置类型继承，22
- 从不可变类型继承，55
- 超类的初始化，120
- 与 __slots__ 的交互，133
- 内部优化，233
- isinstance() 函数，34
- issubclass() 函数，135
- 元类，139
- 方法解析顺序，121
- 多重继承，121
- 防止方法重定义，128
- 私有方法，128
- 与异常配合使用，88

.ini 文件

- 用其配置日志，368
- 从 Python 读取，332

init() 函数，mimetypes 模块，567



##### I

- `__init__()` 方法，50，54-55
  - 与异常，88
  - 与继承，120
  - 与实例创建，129
  - 与元类，139
  - 与 pickle，228
  - 定义多个实例创建方法，123
  - 类的，22，118
- 包中的 `__init__.py` 文件，149
- `input()` 函数，162，206
  - Python 3，11
- `insert()` 方法
  - Element 对象的，577
  - array 对象的，260
  - 列表的，12，41
- `insertBefore()` 方法，DOM Node 对象的，571
- 将项插入字典，16
- 将项插入列表，41
- `insort()` 函数，bisect 模块，261
- `insort_left()` 函数，bisect 模块，261
- `insort_right()` 函数，bisect 模块，261
- inspect 属性，sys.flags 的，230
- inspect 模块，222
- 检查对象，使用 dir()，63
- install 命令，setup.py 文件的，154
- `install_opener()` 函数，urllib.request 模块，518
- 安装第三方包，154
  - 在用户目录中，154
- 安装包，153
- 实例方法，48，118
- `__instancecheck__()` 方法，57，136
- 实例，117
  - 作为可调用对象，50
  - 属性赋值，131
  - 属性删除，131
  - 创建，55，118，129
  - 定义，33
  - pickle 序列化，228
  - 类型，50
- 抽象基类的实例化，137
- int 类型，38
- `int()` 函数，11，62，76，206
- `__int__()` 方法，61-62
  - 与类型强制转换，134
- 整数除法，Python 3，633
- 整数，27
  - 二进制补码表示，66
  - 作为字典键，16
  - 自动提升为长整型，27
  - 转换为长整型，38
  - 创建十六进制字符串，77
  - 创建随机整数，254
  - 溢出行为，66
  - 范围，38
  - 指定为十六进制、八进制或二进制，27
- Integral 抽象基类，253
- IntegrityError 异常，数据库 API，302
- interactive 属性，sys.flags 的，230
- 交互模式，6，175
  - 与空行，26
  - 结果的显示，55，176
- 交互式终端，174
- InterfaceError 异常，数据库 API，302
- internal_attr 属性，ZipInfo 对象的，327
- InternalError 异常，数据库 API，302
- 国际字符
  - 与字符串比较，70
  - 在源代码中，31
- 字符串中的值插值，72
- 解释器，5
- 解释器命令行选项，173
- 解释器环境变量，174
- 解释器提示符，175
- 解释器，-t 和 -tt 选项，26
- 进程间通信（IPC），413
- `interrupt()` 方法，Connection 对象的，306
- 交集运算符 `&`，集合的，15
- `intersection()` 方法，集合的，46
- `intersection_update()` 方法，集合的，47
- 区间定时器，399
- 对象的自省，222
- `inv()` 函数，operator 模块，273

###### `__init__()` 方法

InvalidURL 异常，http.client 模块，504
invert() 函数，operator 模块，274
__invert__() 方法，61
io 模块，349
  - Python 3，631
  - 相关问题，354
IOBase 抽象基类，354
IOBase 类，io 模块，349
ioctl() 函数，fcntl 模块，348
ioctl() 方法，socket 对象的，482
IOError 异常，87，214
__ior__() 方法，61
IP_* 套接字选项，socket 模块，480
__ipow__() 方法，61
IPPROTO_* 常量，socket 模块，476
IPv4 协议，470
  - 地址格式，471
IPv6 协议，470
  - 地址格式，471
IPV6_* 套接字选项，socket 模块，480-481
IronPython，5
  - 示例，620
__irshift__() 方法，61
is 运算符，对象标识，34，78
is_() 函数，operator 模块，274
is_alive() 方法
  - Process 对象的，416
  - Thread 对象的，436
is_multipart() 方法，Message 对象的，554
is_not() 函数，operator 模块，274
is_set() 方法，Event 对象的，440
is_tarfile() 函数，tarfile 模块，319
is_unverifiable() 方法，Request 对象的，517
is_zipfile() 函数，zipfile 模块，325
isabs() 函数，os.path 模块，397
isabstract() 函数，inspect 模块，224
isAlive() 方法，Thread 对象的，436
islower() 方法，字符串的，675
isalnum() 方法，字符串的，41，43
isalpha() 方法，字符串的，43
isatty() 函数，os 模块，383
isatty() 方法
  - IOBase 对象的，349
  - 文件的，160
isblk() 方法，TarInfo 对象的，321
isbuiltin() 函数，inspect 模块，224
isdir() 方法，TarInfo 对象的，321
isclass() 函数，inspect 模块，224
iscode() 函数，inspect 模块，225
isDaemon() 方法，Thread 对象的，437
isdatadescriptor() 函数，inspect 模块，225
isdev() 方法，TarInfo 对象的，321
isdigit() 方法，字符串的，43
isdir() 函数，os.path 模块，397
isdir() 方法，TarInfo 对象的，321
isdisjoint() 方法，集合的，46
iselement() 函数，xml.etree.ElementTree 模块，578
isenabled() 函数，gc 模块，221
isEnabledFor() 方法，Logger 对象的，359
isfifo() 方法，TarInfo 对象的，321
isfile() 函数，os.path 模块，397
isfile() 方法，TarInfo 对象的，321
isframe() 函数，inspect 模块，225
isfunction() 函数，inspect 模块，225
isgenerator() 函数，inspect 模块，225
isgeneratorfunction() 函数，inspect 模块，225
isinf() 函数，math 模块，252
isinstance() 函数，34，37，135，206-207
  - 与继承，134
  - 与代理对象，135
  - 重定义其行为，136
islice() 函数，itertools 模块，272
islink() 函数，os.path 模块，397
islnk() 方法，TarInfo 对象的，321
islower() 方法，字符串的，43

如何让这个索引更有用？请发送邮件至 indexes@samspublishing.com 联系我们

- ismethod() 函数，inspect 模块，225
- ismethoddescriptor() 函数，inspect 模块，225
- ismodule() 函数，inspect 模块，225
- ismount() 函数，os.path 模块，397
- isnan() 函数，math 模块，252
- iso-8859-1 编码，描述，169
- isocalendar() 方法，date 对象的，337
- isoformat() 方法
  - date 对象的，337
  - time 对象的，338
- isoweekday() 方法，date 对象的，337
- isreg() 方法，TarInfo 对象的，321
- isReservedKey() 方法，Morsel 对象的，512
- isroutine() 函数，inspect 模块，225
- isSameNode() 方法，DOM Node 对象的，571
- isspace() 方法，字符串的，43
- issubclass() 函数，135，206
  - 重定义其行为，136
- issubset() 方法，集合的，46
- issuperset() 方法，集合的，46
- issym() 方法，TarInfo 对象的，322
- istitle() 方法，字符串的，43
- istraceback() 函数，inspect 模块，225
- __isub__() 方法，61
- isupper() 方法，字符串的，41，43
- itemgetter() 函数，operator 模块，275
- items() 方法
  - ConfigParser 对象的，333
  - Element 对象的，577
  - Message 对象的，552
  - 字典的，45
  - Python 3 中字典的，632
- itemsize 属性，array 对象的，259
- ItemsView 抽象基类，266
- iter() 函数，206
- __iter__() 方法，59，82
- Iterable 抽象基类，265
- 迭代，10，17，59，82
  - 跳出循环，83
  - 迭代变量，82
  - 遍历序列，39，69
  - 遍历字典键，17
  - 遍历字典值，45
  - 遍历多个序列，83
  - next() 操作的可移植函数，207
  - Python 3 中的协议变更，633
  - 协议，60，82
  - 迭代变量的作用域，82
  - 支持的对象，17
  - 解包元组，82
- Iterator 抽象基类，265
- 迭代器，Python 3 中的用法，632
- iterdecode() 函数，codecs 模块，279
- iterdump() 方法，Connection 对象的，306
- iterencode() 函数，codecs 模块，279
- iterencode() 方法，JSONEncoder 对象的，566
- iterkeyrefs() 方法，WeakKeyDictionary 对象的，241
- iterparse() 函数，xml.etree.ElementTree 模块，578
- itertools 模块，83，270
- itervaluerefs() 方法，WeakValueDictionary 对象的，241
- __itruediv__() 方法，61
- __ixor__() 方法，61
- izip() 函数，itertools 模块，83，212，272
- izip_longest() 函数，itertools 模块，272

#### J

- J 字符，复数字面量上的，27
- j(ump) 调试器命令，pdb 模块，188
- Java，620
  - 类系统的差异，119
- Javascript，弹出窗口示例，531
- join() 函数，os.path 模块，397
- join() 方法
  - JoinableQueue 对象的，419
  - Pool 对象的，424

Process 对象的，416

Queue 对象的，445

Thread 对象的，436

字符串的，43

join_thread() 方法，Queue 对象的，418

JoinableQueue() 函数，multiprocessing 模块，419

js_output() 方法

Morsel 对象的，512

SimpleCookie 对象的，512

JSON（JavaScript Object Notation），563

json 模块，563

与 pickle 和 marshal 的区别，565

JSONDecoder 类，json 模块，565

JSONEncoder 类，json 模块，566

jumpahead() 函数，random 模块，254

Jython，5

示例，620

kbhit() 函数，msvcrt 模块，373

key 属性，Morsel 对象的，512

键索引运算符 []，44

字典的，16

key 关键字参数，传给 sort()，40

KEY_* 常量，winreg 模块，410

键盘中断，162

KeyboardInterrupt 类，214

KeyboardInterrupt 异常，87-88，162

KeyError 异常，44，87，214

keyrefs() 方法，WeakKeyDictionary 对象的，241

keys() 方法

Element 对象的，577

Message 对象的，552

字典的，45

Python 3 中字典的，632

lchown() 函数，os 模块，677

键

字典可接受的类型，16

字典的，44

KeysView 抽象基类，266

关键字参数，18，94

与位置参数混合使用，94

keyword 模块，585

仅限关键字参数，Python 3，625

keywords 属性，partial 对象的，268

kill() 函数，os 模块，392

kill() 方法，Popen 对象的，403

killpg() 函数，os 模块，392

kqueue，BSD，460

##### L

L 字符，长整数上的，27

l(ist) 调试器命令，pdb 模块，188

lambda 运算符，48，112

替代方案，274-275

LambdaType 类型，237

last_accepted 属性，Listener 对象的，434

last_traceback 变量，sys 模块，231

last_type 变量，sys 模块，231

last_value 变量，sys 模块，231

lastChild 属性，DOM Node 对象的，570

lastgroup 属性，MatchObject 对象的，286

lastindex 属性，MatchObject 对象的，286

latin-1 编码，描述，169

启动 Web 浏览器，544

启动 Python 应用程序，176

启动子进程，402

示例，404

惰性求值，99

lchflags() 函数，os 模块，387

lchmod() 函数，os 模块，387

lchown() 函数，os 模块，387

ldexp() 函数，math 模块，252

le() 函数，operator 模块，274

__le__() 方法，56

整数的前导 0b，二进制，27

整数的前导 0o，八进制，27

整数的前导 0x，十六进制，27

字符串字面量的前导 b 字符，字节字符串，29

字符串的前导 r 字符，原始字符串，29

字符串字面量的前导 u 字符，Unicode 字符串，28

左移运算符 <

left_list 属性，dircmp 对象的，315

left_only 属性，dircmp 对象的，315

遗留代码与 exec 语句，115

len() 函数，58，206

用于字典，74

用于映射，44-45

用于序列，39-40，67，69

用于集合，46，75

__len__() 方法，56，58

与真值测试，56

length 属性，HTTPResponse 对象的，504

小于运算符

小于等于运算符 <=，66

letters 变量，string 模块，287

levelname 属性，Record 对象的，359

levelno 属性，Record 对象的，359

词法作用域，97

字典序排列

UTF-8 的，170

字符串的，70

lexists() 函数，os.path 模块，397

LifoQueue() 函数，queue 模块，444

limit_denominator() 方法，Fraction 对象的，250

限制错误回溯的输出，232

行续接字符 \，9，25，29

行续接与圆括号、花括号或方括号，25

文件的行分隔符，379

程序的行结构，25

line_buffering 属性，TextIOWrapper 对象的，353

linecache 模块，585

lineno 属性，Record 对象的，359

linesep 变量，os 模块，379

link() 函数，os 模块，387

linkname 属性，TarInfo 对象的，322

Linux，331

Linux 链路层数据包协议，470

地址格式，472

Linux，epoll 接口，460

列表推导式，13

与声明式编程，110

条件表达式，79

在其中创建元组，109

与生成器表达式的区别，110

通用语法，108

迭代变量的作用域，109

与 SQL 查询的相似性，111

与 awk 命令的相似性，111

Unix 信号名称列表，400

list 类型，38

list() 函数，12，40，77，207

应用于字典，16

list() 方法

Manager 对象的，429

TarFile 对象的，321

list_dialects() 函数，csv 模块，551

listdir() 函数

Python 3，630，633

os 模块，387

listen() 方法

dispatcher 对象的，456

socket 对象的，483

Listener 类，multiprocessing 模块，433

列表，12，40

追加元素，12，40

作为序列，39

与 array 对象比较，260

比较，70

连接，12

计数元素，40

删除元素，69

空列表，12

相等性，78

索引运算符，12

insert() 的低效性，194

插入元素，12，40，69

元素赋值，12，69

保持有序排列，261

列表推导式，108

创建浅副本，40

嵌套列表，13

随机打乱，254

重新赋值切片，12

移除元素，40

反转，40

搜索，40

多进程共享，429

切片赋值，69

切片删除，69

切片，12

排序，40

与 deque 比较，194，262

与元组比较，14

局部变量，96

与 eval()，115

在栈帧中的存储，52

定义前使用，98

local() 函数，threading 模块，443

localcontext() 函数，decimal 模块，248

locale 模块，587

locale 设置与字符串比较，70

localName 属性，DOM Node 对象的，570

locals() 函数，207

localtime() 函数，time 模块，406

Lock 对象

multiprocessing 模块，427

threading 模块，438

Lock() 方法，Manager 对象的，429

LOCK_* 常量，flock() 函数，348

lockf() 函数，fcntl 模块，348

locking() 函数，msvcrt 模块，373

锁

避免死锁，442

Windows 上的文件锁，373

multiprocessing 模块，427

临界区的同步，414

文件锁，348

threading 模块，439

锁

与上下文管理器，89

与异常，23

正确管理，442

**小端格式**，167

**小端，打包和解包**，292

**ljust() 方法**，字符串的，43

**ln() 方法**，Decimal 对象的，243

**load() 函数**

- json 模块，565
- marshal 模块，226
- pickle 模块，171，227

**load() 方法**

- SimpleCookie 对象的，512
- Unpickler 对象的，228

**loads() 函数**

- json 模块，565
- marshal 模块，226
- pickle 模块，227
- xmlrpc.client 模块，526

**线程的本地存储**，443

**日志文件，实时监控示例**，19

**log() 函数**，math 模块，252

**log() 方法**，Logger 对象的，358

**log10() 函数**，math 模块，252

**log10() 方法**，Decimal 对象的，243

**log1p() 函数**，math 模块，252

**log_error() 方法**，BaseHTTPRequestHandler 对象的，510

**log_message() 方法**，BaseHTTPRequestHandler 对象的，510

*如何让这个索引更实用？请发邮件至 indexes@sampspublishing.com 告诉我们*

log_request() 方法，BaseHTTPRequestHandler 对象的，510

LogAdapter() 函数，logging 模块，366

logging 模块，355

向日志消息添加额外字段，365

与 multiprocessing 模块，435

基本配置，355

使用 .ini 文件配置，368

过滤消息，359

消息格式化，365

handler 对象，362

如何配置，367

在日志消息中包含异常，358

发出日志消息，356

日志记录器层次结构，360

消息处理，361

消息传播，360

选择日志记录器名称，356

使用空日志记录器，369

login() 方法

- FTP 对象的，498
- SMTP 对象的

lognormvariate() 函数，random 模块，255

长整数，27

与整数，38

从整数自动提升，27

long 类型，38

long() 函数，207

__long__() 方法，61-62

查找表与字典，16

lookup() 函数

- codecs 模块，277
- unicodedata 模块，296

LookupError 异常，87，212

loop() 函数，asyncore 模块，457

循环，17，82

提前退出，83

维护循环计数器，83

while 语句，8

对象的松耦合，122

底层文件操作，382

lower() 方法，字符串的，43

lowercase 变量，string 模块，287

lseek() 函数，os 模块，383

lshift() 函数，operator 模块，274

__lshift__() 方法，60

lstat() 函数，os 模块，387

lstrip() 方法，字符串的，43

lt() 函数，operator 模块，274

__lt__() 方法，56

LWPCookieJar 类，http.cookiejar 模块，513

##### M

-m 命令行选项，173-174

-m pdb 解释器选项，189

mailbox 模块，587

mailcap 模块，587

主程序执行，146

主程序与 pickle 模块，228

主线程，413

__main__ 模块，146，174

main() 函数，unittest 模块，184

__main__，multiprocessing 模块所需的检查，417

major() 函数，os 模块，387

make_server() 函数，wsgiref.simple_server 模块，542

makedev() 函数，os 模块，387

makedirs() 函数，os 模块，387

makefile() 方法，socket 对象的，483

maketrans() 函数，string 模块，290

进行计时测量，191

受管理对象，multiprocessing 模块，428

Manager() 函数，multiprocessing 模块，428

mant_dig 属性，sys.float_info 的，231

map() 函数，207

与 Python 3，207

与优化，197

future_builtins 模块，217

map() 方法，Pool 对象的，424

map-reduce，multiprocessing 模块，424

##### M

- `map_async()` 方法，Pool 对象，425
- Mapping 抽象基类，266
- 映射，44
  - 删除项，45
  - 键索引运算符，44
  - 特殊方法，58
- MappingView 抽象基类，266
- marshal 模块，226
- `match()` 函数，re 模块，284
- `match()` 方法，Regex 对象，285
- MatchObject 对象，re 模块，285
- math 模块，251
- 数学运算符
  - 就地运算，61
  - 混合类型，66-67
- 数学特殊方法，60
- max 属性
  - date 类，337
  - datetime 类，340
  - sys.float_info，231
  - time 类，338
  - timedelta 类，341
- `max()` 函数，13、39-40、67、69、207
  - 用于集合，75
  - 自定义对象所需的方法，57
- max_10_exp 属性，sys.float_info，231
- max_exp 属性，sys.float_info，231
- maxint 变量，sys 模块，231
- maxsize 变量，sys 模块，231
- maxunicode 变量，sys 模块，231
- `md5()` 函数，hashlib 模块，559
- MemberDescriptorType 类型，237
- 成员测试
  - 字典的，16、74
  - 序列的，67
- `memmove()` 函数，ctypes 模块，617
- 结果备忘录化，242
- 内存效率
  - 与 __slots__，133
  - 生成器表达式的，110
  - 生成器的，107
- 内存管理，128
  - 检查泄漏，221
  - 实例创建，129
  - 垃圾回收，35、220
  - 引用计数，129
- 内存映射文件，370
  - 与 IPC，413
- 内存使用
  - array 对象，260
  - 度量，192
  - 获取对象大小，234
  - 元组与列表的比较，14
- 内存中对象的位置，33
- MemoryError 异常，87、214
- MemoryHandler 类，logging 模块，362
- `memset()` 函数，ctypes 模块，617
- `merge()` 函数，heapq 模块，270
- 梅森旋转算法，254
- Message 类，email 包，552、555
- message 属性，Exception 对象，213
- 消息摘要，559
- 消息传递，414-415
  - 与协程，415
  - 与同步，415
  - 协程，108
  - 定义，413
  - 发送字节缓冲区，421
  - 在进程间发送对象，421
- 日志消息的传播，360
- 消息队列，415
  - 协程，108
  - multiprocessing 模块，418
- `message_from_file()` 函数，email 包，552
- `message_from_string()` 函数，email 包，552
- metaclass 关键字参数，类定义，139
- `__metaclass__` 属性，类，139
- `__metaclass__` 全局变量，139
- 元类，138
  - `__prepare__()` 方法，627-628
  - 与描述符，140
  - 与继承，139
  - 使用注意事项，141
  - 示例，140
  - 如何定义，139
  - 性能优势，197
  - 使用 `__new__()` 方法，55、129
  - 使用自定义字典对象，628
- 方法解析顺序，与 TypeError 异常，122
- 方法解析
  - `__mro__` 属性，121
  - 多重继承，121
  - 单继承，120
- `methodcaller()` 函数，operator 模块，275
- `methodHelp()` 方法，ServerProxy 对象，525
- 方法，48、117
  - 绑定方法，49、125
  - 调用过程，48
  - 类方法，125
  - `@classmethod` 装饰器，48
  - 在类中定义，21
  - 定义，118
  - 作为属性处理，125
  - 防止在子类中重定义，128
  - 静态方法，125
  - `@staticmethod` 装饰器，48
  - 类型，47
  - 内置方法的类型，49
  - 未绑定方法，49
  - 使用 `super()` 函数，120
- `methodSignatures()` 方法，ServerProxy 对象，525
- MethodType 类型，47-48、237
- microsecond 属性，time 对象，338
- 微线程，446
- 迁移代码
  - 从 Python 2 到 3，634
  - 实用策略，637
- MIMEApplication 类，email 包，557
- MIMEAudio 类，email 包，557
- MIMEImage 类，email 包，557
- MIMEMessage 类，email 包，557
- MIMEMultipart 类，email 包，557
- MIMEText 类，email 包，558
- mimetypes 模块，566
- min 属性
  - date 类，337
  - datetime 类，340
  - sys.float_info，231
  - time 类，338
  - timedelta 类，341
- `min()` 函数，13、39-40、67、69、207
  - 用于集合，75
  - 自定义对象所需的方法，57
- min_10_exp 属性，sys.float_info，231
- min_exp 属性，sys.float_info，231
- 支持相等性的最低要求，57
- `minor()` 函数，os 模块，387
- minute 属性，time 对象，338
- `mirrored()` 函数，unicodedata 模块，296
- 缺少括号，与元组，14
- 混合类型数学运算，66-67
- 混入类，122
- 混合字节字符串和 Unicode，167
- `mkd()` 方法，FTP 对象，498
- `mkdir()` 函数，os 模块，388
- `mkdtemp()` 函数，tempfile 模块，323
- `mkfifo()` 函数，os 模块，388
- `mknod()` 函数，os 模块，388
- `mkstemp()` 函数，tempfile 模块，323
- `mktemp()` 函数，tempfile 模块，323
- `mktime()` 函数，time 模块，406
- mmap 模块，369
- `mmap()` 函数，mmap 模块，370
- `mod()` 函数，operator 模块，273
- `__mod__()` 方法，60
- mode 属性
  - FileIO 对象，350
  - TarInfo 对象，322
  - 文件，161
- `modf()` 函数，math 模块，252
- 从函数中修改全局变量，18
- 修改模块搜索路径，147
- module 属性，Record 对象，359
- 模块加载，147
- 模块重新加载，149
- 模块搜索路径
  - 与 site 模块，177
  - 与 zip 文件，147
  - 修改，147
  - 通过环境变量设置，174
- 模块卸载，149
- `__module__` 属性，类型，50
- modulefinder 模块，585
- modules 变量，sys 模块，149、231
- 模块，23、143
  - 访问类，144
  - 与 .pyc 文件，148
  - 作为对象，144
  - 属性访问，51
  - 属性，51
  - 动态加载，144
  - 函数的全局命名空间，96
  - 导入多个模块，144
  - 一次性执行，144
  - 搜索路径，147
  - 使用 doctest 进行自测试，182
  - 类型，50
  - 模块对象的类型，47
  - 可识别的文件类型，148
  - 用于编写可扩展程序，144
- ModuleType 类型，47、237
- 取模运算符 %，65
- month 属性，date 对象，337
- Morsel 类，http.cookies 模块，512
- `move()` 函数，shutil 模块，319
- `move()` 方法，mmap 对象，371
- 移动文件指针，161
- MozillaCookieJar 类，http.cookiejar 模块，513
- `__mro__` 属性，类，121
- MSG_* 常量，socket 模块，483
- msvcrt 模块，372
- mtime 属性，TarInfo 对象，322
- `mul()` 函数，operator 模块，273
- `__mul__()` 方法，60
- 多维列表，13
- MultiCall() 函数，xmlrpc.client 模块，526
- 多核，与程序执行，414
- 多重继承，120-121
- 同一行上的多条语句，26
- I/O 多路复用，459
- 乘法运算符 *，65
- multiprocessing 模块，415
  - 与全局解释器锁，444
  - 与 pickle，435
  - 连接独立进程，433
  - 分布式计算，435
  - 日志记录，435
  - 托管对象，428
  - 通过共享内存传递列表，427
  - 管道，421
  - 进程池，424
  - 队列，418
  - 共享内存，426
  - 同步原语，427
  - 使用 `__main__` 检查，417
- 多线程竞争，414
- 可变性
  - 默认函数参数，94
  - 字典键，44
  - 函数参数，95
  - 就地赋值运算符，75
  - 引用计数，35
- 可变的，定义，33
- MutableMapping 抽象基类，266
- MutableSequence 抽象基类，266
- MutableSet 抽象基类，266
- 互斥锁，438
- MySQL，从 Python 访问，297

##### N

- \N 转义码，字符串中，28
- n(ext) 调试器命令，pdb 模块，189
- name 属性
  - FieldStorage 对象，535
  - FileIO 对象，350
  - Process 对象，417
  - Record 对象，359
  - TarInfo 对象，322
  - Thread 对象，436
  - 文件，161
- 名称修饰，私有属性，127
- name 变量，os 模块，379
- `__name__` 属性
  - 内置函数，49
  - 函数，48
  - 方法，49
  - 模块，51
  - 类型，50
- `__name__` 变量，模块，146
- `name()` 函数，unicodedata 模块，296
- 命名元组
  - 作为元组使用，264
  - 标准库中的使用，265
- `NamedTemporaryFile()` 函数，tempfile 模块，324
- `namedtuple()` 函数，collections 模块，264
- NameError 异常，87、214
- `__del__` 中的 NameError 异常被忽略，179
- NameError 异常，与变量查找，96
- `namelist()` 方法，ZipFile 对象，326
- `Namespace()` 方法，Manager 对象，429
- 命名空间
  - 与类，117
  - 与 import 语句，24、143
  - 函数的局部变量，96
- namespaceURI 属性，DOM Node 对象，570
- NaN 变量，decimal 模块，248
- NaN
  - 非数字，213
  - 非数字，decimal 模块，244
- `ne()` 函数，operator 模块，274
- `__ne__()` 方法，57
- `neg()` 函数，operator 模块，273
- `__neg__()` 方法，61
- 负索引，68-69
- negInf 变量，decimal 模块，248
- 嵌套类，pickle 的问题，228
- 嵌套函数，97
  - 与闭包，99
- 嵌套列表，13
- `nested()` 函数，contextlib 模块，267
- Netlink 协议，470
  - 地址格式，472
- netloc 属性
  - urlparse 对象，520
  - urlsplit 对象，521
- netrc 模块，587
- 网络编程模块，Python 3 重组，497
- 网络编程
  - Unicode 编码，452
  - 异步，467
  - 事件驱动编程，455
  - 获取主机名，474
  - 简介，449
  - 轮询性能，468
- `new()` 函数
  - hashlib 模块，559
  - hmac 模块，559
- `__new__()` 方法，54-55
  - 与实例创建，129
  - 与元类，139

换行符，Unix/Windows上的区别，159

字符串中的换行转义码，28

换行参数，传递给`open()`函数，159

换行抑制，print语句，162

语句的换行终止，7

`newlines`属性
  - `TextIOWrapper`对象的属性，353
  - 文件的属性，161

`next()`函数，207

`next()`方法，59
  - `TarFile`对象的方法，321
  - 文件的方法，160
  - 生成器的方法，19, 53, 103
  - 迭代器的方法，82
  - 与协程一起使用，104

`__next__()`方法，59
  - Python 3中的方法，633
  - 生成器的方法，19, 103
  - 迭代器的方法，82

`nextset()`方法，`Cursor`对象的方法，299

`nextSibling`属性，DOM Node对象的属性，570

`NI_*`常量，`socket`模块，475

`nice()`函数，`os`模块，392

`nis`模块，586

`nlargest()`函数，`heapq`模块，270

`nntplib`模块，587

`no_site`属性，`sys.flags`的属性，230

`nodeName`属性，DOM Node对象的属性，570

`nodeType`属性，DOM Node对象的属性，570

`nodeValue`属性，DOM Node对象的属性，570

非打印字符，在字符串字面量中指定，28

`None`，38
  - 与默认参数一起使用，94
  - 函数中的返回语句，96

`nonlocal`语句，Python 3中的语句，97, 624

Unicode字符串的规范化，171

`normalize()`函数，`unicodedata`模块，171, 296

`normalize()`方法，DOM Node对象的方法，571

`normalvariate()`函数，`random`模块，255

`normcase()`函数，`os.path`模块，398

`normpath()`函数，`os.path`模块，398

不等于运算符`!=`，66

`not`运算符，布尔表达式，9, 77

`not_()`函数，`operator`模块，274

`NotConnected`异常，`http.client`模块，504

`notify()`方法，`Condition`对象的方法，441

`notify_all()`方法，`Condition`对象的方法，441

`NotImplementedError`异常，87, 214

`NotSupportedError`异常，数据库API，302

`now()`方法，`datetime`类的方法，339

`nsmallest()`函数，`heapq`模块，270

`NTEventLogHandler`类，`logging`模块，362

`ntohl()`函数，`socket`模块，476

`ntohs()`函数，`socket`模块，476

`ntransfercmd()`方法，FTP对象的方法，498

空对象，369

空值，38

空终止字符串，与UTF-8的关系，170

`Number`抽象基类，253

系统中的CPU数量，434

`numbers`模块，138, 252

数字，定义新类型的示例，133

`numerator`属性
  - `Fraction`对象的属性，250
  - 整数的属性，39

数值数据与字符串，686

数字字面量，26-27

数值类型强制转换，66-67

数值类型层次结构，137, 253

数值类型，38

`numeric()`函数，`unicodedata`模块，296

`numpy`扩展，39, 261

##### O

`-O`命令行选项，91, 148, 173-174, 369

对象，47

`object`基类，21, 119

`object()`函数，208

对象，21
  - 对象的属性，33
  - 对象的类，34
  - 对象比较，34
  - Python 3中的对象比较，633
  - 容器或集合，33
  - 定义空对象，369
  - 对象的定义，33
  - 一等公民地位，36
  - 获取引用者列表，221
  - 获取对象大小，192
  - 对象的层次结构，137
  - 如何复制对象，36
  - 对象的标识，33
  - 使用`dir()`检查对象，63
  - 对象的实例，33
  - 对象的自省，222
  - 比较方法，56
  - 对象的名称，35
  - 获取对象大小，234
  - 对象持久化，171
  - 多进程模块中的对象代理，431
  - 对象的引用计数，34
  - 对象的表示，131
  - 排序要求，57
  - 通过管道在进程间发送对象，421
  - 通过队列在进程间发送对象，418
  - 使用`marshal`序列化对象，226
  - 使用`pickle`序列化对象，227
  - 在解释器中共享对象，35
  - 支持迭代的对象，82
  - 对象的类型，33
  - 对象的弱引用，240

观察者模式，130, 240

`oct()`函数，77, 208
  - `future_builtins`模块，217

八进制整数字面量，27

`octdigits`变量，`string`模块，287

旧式类，139

`-OO`命令行选项，148, 173-174

`open()`函数，10, 158, 208
  - Python 3中的函数，159
  - `codecs`模块中的函数，167, 279
  - `codecs`模块与Python 3，279
  - `dbm`模块中的函数，310
  - 文件模式描述，159
  - Python 2与Python 3之间的区别，208
  - `gzip`模块中的函数，317
  - `io`模块中的函数，354
  - `os`模块中的函数，384
  - `shelve`模块中的函数，171, 311
  - `tarfile`模块中的函数，319
  - `webbrowser`模块中的函数，544

`open()`方法
  - `ZipFile`对象的方法，326
  - 控制器对象的方法，544

`open_new()`函数，`webbrowser`模块，544

`open_new()`方法，控制器对象的方法，544

`open_new_tab()`函数，`webbrowser`模块，544

`open_osfhandle()`函数，`msvcrt`模块，373

`OpenKey()`函数，`winreg`模块，410

`OpenKeyEx()`函数，`winreg`模块，410

`openpty()`函数，`os`模块，385

OpenSSL，486
  - 创建证书的示例，489

操作系统，操作系统的调度，414

###### OperationalError异常，数据库API，302

###### operator模块，273
- lambda的替代方案，274
- 优化中的使用，274

###### 运算符重载，54
- 示例，133
- 操作数顺序，134
- 反转操作数，60
- 类型强制转换，134

###### 运算符，30, 65
- 数学运算符，60
- 运算符优先级，78

###### 优化
- 类的`__slots__`属性，132, 196
- 数组对象，260
- 属性绑定，195–196
- 内置类型，194
- 实例的创建，195
- 装饰器和元类，197
- 加速的定义，192
- `deque`对象，263
- `dict()`函数，195
- 字典查找，197
- 字典与类的比较，195
- 反汇编，193
- 添加层级的影响，195
- 异常，196–197
- 日志消息的格式化，358
- 函数式编程，197
- I/O轮询的影响，469
- 内部类型缓存，233
- 列表与数组对象的比较，260
- `logging`模块，369
- 进行时间测量，191
- `map()`和`filter()`函数，197
- `marshal`与`pickle`的比较，226
- 测量内存使用，192
- 重复的时间测量，192
- `select()`函数，467
- 排序回调函数，275
- 加速，194
- 调优策略，194
- `io`模块的使用，354
- 多进程池的使用，426
- `operator`模块的使用，274
- 用户定义的类，195

###### `optimize`属性，`sys.flags`的属性，230

###### 优化模式，通过环境变量启用，174

###### 可选函数参数，18, 93
- 与`None`一起使用，38

###### `OptionParser()`函数，`optparse`模块，374

###### `options()`方法，`ConfigParser`对象的方法，333

###### `optionxform()`方法，`ConfigParser`对象的方法，333

###### `optparse`模块，374
- 示例，157

###### `or`运算符，布尔表达式，9, 77

###### `or_()`函数，`operator`模块，274

###### `__or__()`方法，60

###### `ord()`函数，77, 208

###### 求值顺序，78
- 尝试修改求值顺序，79

###### 运算符重载中的操作数顺序，134

###### 为分发组织代码，152

###### OS X，331

###### `os`模块，158, 378

###### `os.environ`变量，158

###### `os.path`模块，396

###### `OSError`异常，87, 214

###### `ossaudiodev`模块，588

###### `output()`方法
  - `Morsel`对象的方法，512
  - `SimpleCookie`对象的方法，512

###### `OutputString()`方法，`Morsel`对象的方法，513

###### 溢出，整数无溢出，66

###### `OverflowError`异常，214

#### P

###### `p`调试器命令，`pdb`模块，189

###### `P_*`常量，`spawnv()`函数，392

###### `pack()`函数，`struct`模块，290

###### `pack()`方法，`Struct`对象的方法，291

###### `pack_into()`函数，`struct`模块，290

### `pack_into()`方法，`Struct`对象的方法，291

### 包，149
- 相对导入，150-151

### `PACKET_*`常量，`socket`模块，472

### 打包
- 二进制数据结构，290
- 元组的打包，14

### 键值对，从字典创建键值对列表，45

### 序列的并行迭代，83

### 函数的参数传递，95

### `params`属性，`urlparse`对象的属性，520

### `paramstyle`变量，数据库API，300

### `pardir`变量，`os`模块，386

### 父类，119

### `parentNode`属性，DOM Node对象的属性，570

### `paretovariate()`函数，`random`模块，256

### `parse()`函数
  - `xml.dom.minidom`模块，570
  - `xml.etree.ElementTree`模块，578
  - `xml.sax`模块，580

### `parse()`方法
  - `ElementTree`对象的方法，574
  - `Formatter`对象的方法，288

### `parse_args()`方法，`OptionParser`对象的方法，158, 376

### `parse_header()`函数，`cgi`模块，536

### `parse_multipart()`函数，`cgi`模块，536

### `parse_qs()`函数，`urllib.parse`模块，521

### `parse_qsl()`函数，`urllib.parse`模块，522

### `parser`模块，586

### `parseString()`函数
  - `xml.dom.minidom`模块，570
  - `xml.sax`模块，580

### 解析
- CSV文件，548
- HTML，561
- URL，520
- XML，568
- 命令行选项，157, 374
- 电子邮件消息，552
- CGI脚本中的表单字段，534
- 使用ElementTree解析大型XML文档，579
- robots.txt文件，523

### `partial()`函数
  - `functools`模块，76, 268
  - 与网络处理器一起使用，510

### `partition()`方法，字符串的方法，41, 43

### `pass`语句，9, 25, 82

### `password`属性
  - `urlparse`对象的属性，520
  - `urlsplit`对象的属性，521

### `path`属性
  - `BaseHTTPRequestHandler`对象的属性，509
  - `urlparse`对象的属性，520
  - `urlsplit`对象的属性，521

### `path`变量
  - `os`模块，379
  - `sys`模块，147, 177, 232

### `__path__`属性，模块的属性，51

### `__path__`变量，包中的变量，151

### `pathconf()`函数，`os`模块，388

### `pathname`属性，`Record`对象的属性，359

### `pathsep`变量，`os`模块，386

### `pattern`属性，`Regex`对象的属性，284

### 模式语法，正则表达式，281

### `pause()`函数，`signal`模块，399

### `pdb`模块，186
- 从命令行调试程序，189
- `.pdbrc`配置文件，190

### `.pdbrc`配置文件，190

### `peek()`方法，`BufferedReader`对象的方法，351

### `PEM_cert_to_DER_cert()`函数，`ssl`模块，488

- PEP 249，Python数据库API规范，297
- PEP 333（WSGI），540
- 每用户站点目录，154，177
  - 在其中安装包，178
- 性能
  - 二进制文件I/O，351–352
  - 生成器表达式，110
  - 日志模块，369
  - 类型检查，34
- Perl
  - 与动态作用域，97
  - 对数值字符串的解释与Python比较，11
- permutations()函数，itertools模块，272
- 持久化字典，shelve模块，171
- PHP，对数值字符串的解释与Python比较，11
- pi变量，math模块，252
- pickle模块，171，226
  - __main__模块，228
  - 与multiprocessing模块，435
  - cPickle，229
  - 不兼容对象，171
  - 与copy模块交互，220
  - 协议选择，171–172
  - 安全顾虑，172
  - shelve使用的，311
- pickle协议，在shelve模块中选择，172
- Pickler类，pickle模块，228
- pickletools模块，586
- pid属性
  - Popen对象的，404
  - Process对象的，417
- Pipe()函数，multiprocessing模块，421
- pipe()函数，os模块，385
- 管道与生成器，19
- 管道，与生成器，106–107
- pipes模块，586
- 管道，使用subprocess模块创建，403
- pkgutil模块，586
- 装饰器的放置，101
- platform模块，586
- platform变量，sys模块，232
- plistlib模块，587
- plock()函数，os模块，392
- pm()函数，pdb模块，186
- POINTER()函数，ctypes模块，614
- pointer()函数，ctypes模块，615
- poll()函数，select模块，459
- poll()方法
  - Connection对象的，421
  - Poll对象的，460
  - Popen对象的，403
- POLL*常量，select模块，459
- 轮询，459
  - 其性能，468–469
- 多态，122
- Pool()函数，multiprocessing模块，424
- pop()方法
  - 数组对象的，260
  - 双端队列对象的，262
  - 字典的，45，95
  - 列表的，41
  - 集合的，47
- Popen()函数，subprocess模块，402
- popen()函数，os模块，392
- popitem()方法，字典的，45
- popleft()方法，双端队列对象的，262
- poplib模块，587
- port属性
  - urlparse对象的，520
  - urlsplit对象的，521
- 端口号
  - 在网络程序中，449
  - 常见端口号列表，450
- 可移植性，marshal模块的，226
- 文件名的可移植操作，396
如何改进此索引？请通过电子邮件联系 indexes@samspublishing.com

pos属性，MatchObject对象的，286
pos()函数，operator模块，273
__pos__()方法，61
POSIX接口，331
posix属性，TarFile对象的，321
post_mortem()函数，pdb模块，186
pow()函数，66，208
  - math模块，252
__pow__()方法，60
幂运算符 **，65
pp调试器命令，pdb模块，189
pprint模块，586
preamble属性，Message对象的，554
prec属性，Context对象的，247
精度，浮点数的，38
predicate()函数，itertools模块，271
prefix属性，DOM Node对象的，570
--prefix选项给setup.py，154
prefix变量，sys模块，177，232
__prepare__()方法，Python 3元类，627-628
防止创建.pyc文件，230
previousSibling属性，DOM Node对象的，570
print语句，6，162
  - 与__str__()，56
  - 与sys.stdout，161
  - 文件重定向，10，163
  - 格式化输出，8，162
  - 换行符抑制，162
  - 文件的softspace属性，162
  - Python 3的语法错误，6
  - 末尾逗号，10
print()函数，163，209
  - Python 3，631
  - 在Python 2.6中启用，163
  - 文件重定向，163
  - 换行符抑制，163
  - 分隔符字符，163
print_directory()函数，cgi模块，537
print_environ()函数，cgi模块，537
print_environ_usage()函数，cgi模块，537
print_exc()函数，traceback模块，236
print_exception()函数，traceback模块，236
print_form()函数，cgi模块，537
print_last()函数，traceback模块，236
print_stack()函数，traceback模块，236
print_tb()函数，traceback模块，235-236
printable变量，string模块，287
printdir()方法，ZipFile对象的，326
printf()函数等价物，8
打印到屏幕，10
打印
  - 创建自定义格式化器，288
  - 日期和时间，406
  - 格式化，8
优先队列，269
PriorityQueue()函数，queue模块，445
私有属性，127
  - 与properties，128
  - 名称改编，127
私有类成员，26
私有方法，与继承，128
私有说明符，缺乏，127
概率，随机数分布，255
process属性，Record对象的，359
进程ID，获取，380
Process()函数，multiprocessing模块，416
进程
  - 使用管道连接，421
  - 守护进程，415
  - 定义，413
  - 连接，415
  - 调度，414
  - 发送信号给，392
  - 终止，392，403-404，415
  - 工作池，424
- ProcessingInstruction()函数，xml.etree.ElementTree模块，575
- processingInstruction()方法，ContentHandler对象的，581
- 生产者-消费者
  - 使用协程，20
  - 使用管道，422
  - 使用队列，419
  - 使用线程和条件变量，441
  - 使用线程和信号量，439
- product()函数，itertools模块，272
- profile模块，190
- 性能分析，190
  - 解释输出，191
- 程序执行模型，81
- 程序执行，主程序，146
- 程序结构，81
- 程序终止，7，179，233
  - 与垃圾回收，179
  - 强制，179
  - 强制hellip;，391
  - 忽略的NameError异常，179
  - 注册清理函数，219
- 编程错误，缺乏编译器检查，181
- ProgrammingError异常，数据库API，302
- 提示符
  - 更改，176
  - 交互模式，175
- propagate属性，Logger对象的，360
- properties，117
  - 与__setattr__()方法，131
  - 与私有属性，128
  - 定义，124
  - 设置和删除函数，126
  - 统一访问原则，125
  - 方法使用，125
- @property装饰器，124
- property()函数，126，209
- protected说明符，缺乏，127
- pwd()方法，FTP对象的，691
- proto属性，socket对象的，484
- protocol参数，给pickle函数，171
- protocol_version属性，BaseHTTPRequestHandler类的，509
- ProtocolError异常，xmlrpc.client模块，527
- 代理，与属性绑定方法，132
- 代理，62
- 代理函数，95
- 代理对象
  - 与multiprocessing模块，428，431
  - 类型检查问题，135
- proxy()函数，weakref模块，241
- ProxyBasicAuthHandler类，urllib.request模块，518-519
- ProxyDigestAuthHandler类，urllib.request模块，518-519
- ProxyHandler类，urllib.request模块，518-519
- ProxyTypes类，weakref模块，241
- ps1变量，sys模块，232
- ps2变量，sys模块，232
- .pth文件，站点配置，177
- pty模块，586
- punctuation变量，string模块，287
- push()方法，asynchat对象的，453
- push_with_producer()方法，asynchat对象的，453
- put()方法，Queue对象的，418，445
- put_nowait()方法，Queue对象的，419，445
- putch()函数，msvcrt模块，373
- putenv()函数，os模块，380
- putheader()方法，HTTPConnection对象的，503
- putrequest()方法，HTTPConnection对象的，503
- putwch()函数，msvcrt模块，373
- pwd模块，586
- pwd()方法，FTP对象的，498
如何改进此索引？请通过电子邮件联系 indexes@samspublishing.com

- .py文件，6，147
  - 与库模块，23
- py2app包，154
- py2exe包，154
- py3k_warning属性，sys.flags的，230
- py3kwarning变量，sys模块，232
- Py_BEGIN_ALLOW_THREADS宏，607
- Py_BuildValue()函数，602
- py_compile模块，586
- Py_DECREF()宏，607
- Py_END_ALLOW_THREADS宏，607
- Py_Finalize()函数，609
- Py_GetExecPrefix()函数，609
- Py_GetPath()函数，609
- Py_GetPrefix()函数，609
- Py_GetProgramFullPath()函数，609
- Py_INCREF()宏，607
- Py_Initialize()函数，609
- Py_IsInitialized()函数，609
- Py_SetProgramName()函数，609
- Py_XDECREF()宏，607
- Py_XINCREF()宏，607
- PyArg_ParseTuple()函数，597
- PyArg_ParseTupleAndKeywords()函数，597
- PyBytes_AsString()函数，611
- .pyc文件，147
  - 导入时编译，148
  - 防止创建，230
  - 何时创建，148
- pyclbr模块，586
- .pyd文件，编译扩展，148
- pydev，5
- pydoc命令，24
- PyErr_Clear()函数，606
- PyErr_ExceptionMatches()函数，606
- PyErr_NoMemory()函数，605
- PyErr_Occurred()函数，606
- PyErr_SetFromErrno()函数，605
- PyErr_SetFromErrnoWithFilename()函数，605
- PyErr_SetObject()函数，605
- PyErr_SetString()函数，605
- PyEval_CallObject()函数，610
- PyEval_CallObjectWithKeywords()函数，610
- PyExc_*异常，在扩展模块中，605
- PyFloat_AsDouble()函数，611
- PyImport_ImportModule()函数，610
- PyInt_AsLong()函数，611
- PyLong_AsLong()函数，611
- PyModule_AddIntConstant()函数，604
- PyModule_AddIntMacro()函数，605
- PyModule_AddObject()函数，604
- PyModule_AddStringConstant()函数，604
- PyModule_AddStringMacro()函数，605
- .pyo文件，147
  - 何时创建，148
- PyObject_GetAttrString()函数，610
- PyObject_SetAttrString()函数，610
- pypi（Python包索引），154
- pyprocessing库，435
- PyRun_AnyFile()函数，608
- PyRun_InteractiveLoop()函数，609
- PyRun_InteractiveOne()函数，609
- PyRun_SimpleFile()函数，609
- PyRun_SimpleString()函数，609
- PyString_AsString()函数，611
- PySys_SetArgv()函数，610

#### Python 3

- 2to3工具，635-637
- 省略号作为表达式，626
- I/O系统，349，631
- 标识符中的Unicode字符，622
- __next__()方法，633
- 绝对导入，634
- 抽象基类，137
- 采用，621
- 与WSGI，541
- 字节字符串与系统接口，630
- 链式异常，626
- 命令行选项，633
- commands模块，332

# 队列（续）
消息传递，415
多消费者与多生产者，420
优先级，269
多进程共享，429

## 线程编程
threading 模块，444

*   **quit() 方法**
    *   FTP 对象的，498
    *   SMTP 对象的，514

### 退出交互式解释器
7 ### Quopri 模块
567

## 引号功能
*   **quote() 函数**，urllib.parse 模块，522
*   **quote_from_bytes() 函数**，urllib.parse 模块，522
*   **quote_plus() 函数**，urllib.parse 模块，522

### quoteattr() 函数
xml.sax.saxutils 模块，583

#### 引号，样式之间的区别
27 ##### 引用，URL 中的字符
522

# R
字符串格式化中的 `!r` 说明符，74
字符串字面量前的 `r` 字符，29
**'r' 模式**，open() 函数，159
*r(eturn) 调试器命令*，pdb 模块，189

### 竞态条件
193, 414 #### *__radd__() 方法*
60
在 __add__() 上调用时，134

### radians() 函数
math 模块，251 rad 属性
sys.float_info 的，231 raise 语句
23, 84–85, 88 ### **__rand__() 方法**
61 ##### RAND_add() 函数
ssl 模块，487 ---##### RAND_egd() 函数
ssl 模块，489 ------##### **RAND_status() 函数**，ssl 模块，489

### randint() 函数
random 模块，254 #### range() 函数，Python 310 中已移除 ##### 有理数抽象基类
252 -------有理数
250

###### 文件上的原始 I/O
350 ##### **原始套接字**
470 ###### 原始字符串
29 Unicode 和反斜杠规则
在正则表达式中的使用
原始 unicode 转义编码说明

### read() 方法
BufferedReader 对象的，351
*   ConfigParser 对象的，333 `    *     FileIO 对象的，350        *       HTTPResponse 对象的，504           *
            *             StreamReder 对象的，278                 *               TextIOWrapper 对象的，353         *         - ZipFile 对象的，326          *   文件和 mmap 对象

## readline 库
176

### Readline 方法

*     IOError 基类的
    40-9     
        o StreamReder 对象。    

**readlines() 方法**，IOBase 对象，文件
urlopen 对象等



#### 就绪状态对象


Real 抽象基类
253 ### Real 属性 复数 浮点数

### realpath 函数 os.path 模块

# reason 属性 HTTPResponse 对象


# 重新赋值列表的部分 109.68 record 对象 logging 模块 递归限制 更改 递归与装饰器 生成器函数 递归遍历 目录树 recv 方法
Connection 对象 dispatcher socket 模块等
recv_bytes()、recv_into()、sendinfo


Recv from Info 方法 Socket 对象

### reduce 函数 functools 模块

reduce_ex() 方法
254 ### 可重入互斥锁 187-340 引用计数 复制 del 语句 内存使用 可变对象 扩展模块 垃圾回收与弱引用 引用循环 垃圾回收 通过弱引用避免 Referer 错误异常 REG_* 常量 winreg 正则表达式对象 re 模块

### register 函数
atexit 模块 webbrowser 模块
BaseManager 类 Poll 抽象基类 adapter sqlite3 转换器 方言 XMLRPC Server 函数 multicall 实例 自省

# Regloadkey 函数，WinReg 模块（409），正则表达式
模式语法 使用原始字符串 关系型数据库 从 Python 访问 关系运算符 相对包导入 Release 方法 Condition Lock RLock Semaphore 可靠数据报 reload 函数 重新加载模块 relpath os.path 远程过程调用 XML RPC 多进程 Remove 函数 Element Array Deque List Set remove_option ConfigParser config_remove section DOM Node removedirs 目录 文件 序列项 切片 Renames 模块 Rename FTP 对象 repeat cProfile itertools operator timeit replace 错误 Unicode 编码 datetime 字符串 date 对象 Message Header 替换子串 Replication 序列 浅拷贝 report 方法 dircmp full closure 方法
```



## R

`report_partial_closure()` 方法，dircmp 对象，315

`repr`（reprlib）模块，586

`repr()` 函数，11, 55, 77, 176, 209
    与 `eval()`，55
    与 `str()` 的区别，12

`__repr__()` 方法，55-56

表示日期和时间，336

request 属性，BaseRequestHandler 对象，490

`Request()` 函数，urllib.request 模块，516

`request()` 方法，HTTPConnection 对象，503

`request_queue_size` 属性，SocketServer 类，492

`request_version` 属性，BaseHTTPRequestHandler 对象，509

`RequestHandlerClass` 属性，SocketServer 对象，492

重新抛出上一个异常，84

`reserved` 属性，ZipInfo 对象，327

保留字，26

`reset()` 方法
    HTMLParser 对象，562
    IncrementalDecoder 对象，279
    IncrementalEncoder 对象，278
    StreamReader 对象，278
    StreamWriter 对象，278

`resetwarnings()` 函数，warnings 模块，239

`resize()` 函数，ctypes 模块，617

`resize()` 方法，mmap 对象，371

`resolution` 属性
    date 类，337
    datetime 类，340
    time 类，338
    timedelta 类，341

`resource` 模块，587

响应时间，异步网络，467

`ResponseNotReady` 异常，http.client 模块，504

`responses` 属性，BaseHTTPRequestHandler 类，509

限制属性名称，132

`restype` 属性，ctypes 函数对象，613

交互模式中上一次操作的结果，6, 176

`retrbinary()` 方法，FTP 对象，499

`retrlines()` 方法，FTP 对象，499

return 语句，96

`returncode` 属性，Popen 对象，404

从函数返回多个值，18, 96

`reverse` 关键字参数，用于 `sort()`，40

`reverse()` 方法
    array 对象，260
    列表，40-41

反向操作数方法，被调用时，134

反向操作数，运算符重载，60

`reversed()` 函数，209

反转列表，40

`rfile` 属性
    BaseHTTPRequestHandler 对象，509
    StreamRequestHandler 对象，491

`rfind()` 方法，字符串，41, 43

`__rfloordiv__()` 方法，60

右移运算符 >>，65

`right_list` 属性，dircmp 对象，315

`right_only` 属性，dircmp 对象，315

`rindex()` 方法，字符串，41, 43

`rjust()` 方法，字符串，43

`rlcompleter` 模块，586

`rldecode_hqx()` 函数，binascii 模块，548

`rledecode_hqx()` 函数，binascii 模块，548

`RLock` 对象
    multiprocessing 模块，427
    threading 模块，438

`RLock()` 方法，Manager 对象，429

`__rlshift__()` 方法，61

`rmdir()` 方法，FTP 对象，499

`rmdir()` 函数，os 模块，388

`__rmod__()` 方法，60

`rmtree()` 函数，shutil 模块，319

`__rmul__()` 方法，60

`robotparser` 模块，523

`robots.txt` 文件，523

`rollback()` 方法，Connection 对象，298

`rollover()` 方法，SpoolTemporaryFile 对象，324

根日志记录器，logging 模块，355

`__ror__()` 方法，61

`rotate()` 方法，deque 对象，263

轮转日志文件，363

`RotatingFileHandler` 类，logging 模块，363

`round()` 函数，66, 209
    与 Python 3，209

`rounding` 属性，Context 对象，247

舍入行为，66
    Python 3 中的变化，66

舍入，decimal 模块，245

`rounds` 属性，`sys.float_info`，231

`row_factory` 属性，Connection 对象，308

`rowcount` 属性，Cursor 对象，299

`rpartition()` 方法，字符串，41

`__rpow__()` 方法，61

`__rrshift__()` 方法，61

`rshift()` 函数，operator 模块，274

`__rshift__()` 方法，60

`rsplit()` 方法，字符串，41, 43

`rstrip()` 方法，字符串，43

`__rsub__()` 方法，60

`__rtruediv__()` 方法，60

Ruby，对象系统的差异，124

`run` 调试器命令，pdb 模块，189

`run()` 函数
    cProfile 模块，190
    pdb 模块，186
    profile 模块，190

`run()` 方法
    Process 对象，416
    Thread 对象，436

`runcall()` 函数，pdb 模块，186

`runeval()` 函数，pdb 模块，186

运行程序，6

`RuntimeError` 异常，87, 214

`RuntimeWarning` 警告，216, 238

`__rxor__()` 方法，61

## S

`!s` 格式化说明符，字符串格式化，74

`-S` 命令行选项，173-174

`-s` 命令行选项，173

`s(tep)` 调试器命令，pdb 模块，189

`safe_substitute()` 方法，Template 对象，289

`SafeConfigParser` 类，configparser 模块，336

`same_files` 属性，dircmp 对象，315

`samefile()` 函数，os.path 模块，398

`sameopenfile()` 函数，os.path 模块，398

`samestat()` 函数，os.path 模块，398

`sample()` 函数，random 模块，255

`SaveKey()` 函数，winreg 模块，410

SAX 接口
    XML 解析，568
    示例，583

可扩展性，并发，415

`sched` 模块，587-588

调度器，用于生成器和协程，447

`scheme` 属性
    urlparse 对象，520
    urlsplit 对象，521

科学记数法，浮点数，27

#### 作用域规则
- 与模块导入，145
- 与方法中的 self 参数，118
- 函数的词法作用域，97
- 类的作用域，118
- 函数变量的作用域，18, 96
- 列表推导中迭代变量的作用域，109
- 迭代变量的作用域，82

### 脚本名称，157

### 搜索路径，模块，147

### `search()` 函数，re 模块，284

### `search()` 方法，Regex 对象，285

### 搜索，带偏移量的字符串，41

### `second` 属性，time 对象，338

### `sections()` 方法，ConfigParser 对象，334

### 安全套接层（SSL），486

### 安全
- XML-RPC 服务器，530
- 数据库查询，300
- marshal 模块，226
- pickle 模块，172, 229

### `seed()` 函数，random 模块，254

### `seek()` 方法
- IOBase 对象，350
- 文件，160-161, 352
- mmap 对象，371

### `seekable()` 方法，IOBase 对象，350

### `select` 模块，415, 459
- 信号处理，399

### `select()` 函数
- 与 asyncore 模块，455
- 性能问题，467
- select 模块，459

### 方法的 self 参数，22, 118
- 为什么必需，119

### `__self__` 属性
- 内置函数，49
- 方法，49

### `Semaphore` 对象
- multiprocessing 模块，427
- threading 模块，439

### `Semaphore` 对象，用于信号传递，439

### `Semaphore()` 方法，Manager 对象，429

### 分号 ;，26

### `send()` 方法
- Connection 对象，422
- HTTPConnection 对象，503
- dispatcher 对象，456
- 生成器，20, 53, 104
- socket 对象，484

### `send_bytes()` 方法，Connection 对象，422

### `send_error()` 方法，BaseHTTPRequestHandler 对象，509

### `send_header()` 方法，BaseHTTPRequestHandler 对象，509

### `send_response()` 方法，BaseHTTPRequestHandler 对象，509

### `send_signal()` 方法，Popen 对象，403

### `sendall()` 方法，socket 对象，484

### `sendcmd()` 方法，FTP 对象，499

### 发送电子邮件，示例，514, 558

### `sendmail()` 方法，SMTP 对象，514

### `sendmsg()` 系统调用，缺少支持，486

### `sendto()` 方法，socket 对象，484

### 哨兵值，与队列配合使用，420, 446

### `sep` 关键字参数，用于 `print()` 函数，163

### `sep` 变量，os 模块，386

### 分隔符字符，`print()` 函数，163

### `Sequence` 抽象基类，266

### 序列，39
- 比较，70
- 连接，67
- 扩展切片，68
- `in` 运算符，67
- 字符串格式化中的索引，72
- 元素赋值，40
- 迭代，39, 69
- 复合字符串格式化中的查找，42
- 负索引，68
- 运算符，67
- 随机选取元素，254
- 随机抽样，254
- 复制，67
- 复制中的浅拷贝，67
- 切片赋值，40
- 切片运算符，68
- 特殊方法，58
- 解包，67-68

### `serve_forever()` 方法
- BaseManager 对象，431
- SocketServer 对象，491

### `server` 属性，BaseRequestHandler 对象，490

### 服务器程序，449
- TCP 示例，451
- UDP 示例，485
- 使用 HTTP 限制访问的示例，507
- 使用 SocketServer 模块的示例，490
- 使用协程的示例，464

### `server_address` 属性，SocketServer 对象，492

### `server_version` 属性
- BaseHTTPRequestHandler 类，508
- HTTPRequestHandler 类，507

### `ServerProxy()` 函数，xmlrpc.client 模块，524

### `Set` 抽象基类，266

### 集合推导，Python 3，623

### 集合差集运算符 ~，75

### 集合交集运算符 &，75

### 集合字面量，Python 3，622

### 集合对称差集运算符 ^，75

### 集合论，与列表推导的相似性，110

### `set` 类型，38, 46, 75

### 集合并集运算符 |，75

### `set()` 函数，15, 77, 210

### `set()` 方法
- ConfigParser 对象，334
- Element 对象，577
- Event 对象，440
- Morsel 对象，512

### `__set__()` 方法，描述符，58, 126

### `set_authorizer()` 方法，Connection 对象，306

### `set_boundary()` 方法，Message 对象，556

### `set_charset()` 方法，Message 对象，556

### `set_conversion_mode()` 函数，ctypes 模块，617

### `set_debug()` 函数，gc 模块，221

### `set_default_type()` 方法，Message 对象，556

### `set_defaults()` 方法，OptionParser 对象，158, 377

### `set_errno()` 函数，ctypes 模块，618

### `set_executable()` 函数，multiprocessing 模块，435

### `set_last_error()` 函数，ctypes 模块，618

### `set_param()` 方法，Message 对象，556

### `set_pasv()` 方法，FTP 对象，499

### `set_payload()` 方法，Message 对象，556

### `set_progress_handler()` 方法，Connection 对象，307

### `set_proxy()` 方法，Request 对象，517

### `set_server_documentation()` 方法，XMLRPCServer 对象，528

### `set_server_name()` 方法，XMLRPCServer 对象，528

### `set_server_title()` 方法，XMLRPCServer 对象，528

### `set_terminator()` 方法，asynchat 对象，453

### `set_threshold()` 函数，gc 模块，221

### `set_trace()` 函数，pdb 模块，186

### `set_type()` 方法，Message 对象，557

## set_unixfrom() 方法
Message 对象的方法，第 557 页

## set_usage() 方法
OptionParser 对象的方法，第 377 页

## set_wakeup_fd() 函数
signal 模块，第 399 页

## setattr() 函数
第 210 页
及私有属性，第 128 页

### __setattr__() 方法
第 57-58、131 页
及 __slots__，第 133 页

## setblocking() 方法
socket 对象的方法，第 484 页

## setcheckinterval() 函数
sys 模块，第 235 页

## setcontext() 函数
decimal 模块，第 248 页

## setDaemon() 方法
Thread 对象的方法，第 437 页

## setdefault() 方法
字典的方法，第 45 页
字典和 defaultdict 对象的方法，第 263 页

## setdefaultencoding() 函数
sys 模块，第 235 页

## setdefaultencoding() 方法
sys 模块，第 177 页

## setdefaulttimeout() 函数
socket 模块，第 476 页

## setdlopenflags() 函数
sys 模块，第 235 页

## setDocumentLocator() 方法
ContentHandler 对象的方法，第 581 页

## setegid() 函数
os 模块，第 380 页

## seteuid() 函数
os 模块，第 380 页

## setFormatter() 方法
Handler 对象的方法，第 365 页

## setgid() 函数
os 模块，第 380 页

## setgroups() 函数
os 模块，第 380 页

## setinputsize() 方法
Cursor 对象的方法，第 299 页

## setitem() 函数
operator 模块，第 274 页

### __setitem__() 方法
第 58-59 页
及切片，第 59 页

## setitimer() 函数
signal 模块，第 399 页

## setLevel() 方法
Handler 对象的方法，第 364 页
Logger 对象的方法，第 359 页

## setmode() 函数
msvcrt 模块，第 373 页

## setName() 方法
Thread 对象的方法，第 436 页

## setoutputsize() 方法
Cursor 对象的方法，第 299 页

## setpassword() 方法
ZipFile 对象的方法，第 326 页

## setpgid() 函数
os 模块，第 381 页

## setpgrp() 函数
os 模块，第 381 页

## setprofile() 函数
sys 模块，第 235 页
threading 模块，第 444 页

## setrecursionlimit() 函数
sys 模块，第 235 页

## setregid() 函数
os 模块，第 381 页

## setreuid() 函数
os 模块，第 381 页

### _setroot() 方法
ElementTree 对象的方法，第 574 页

#### 集合
第 15 页
- 添加元素，第 15 页
- 从可迭代对象创建，第 46 页
- 差集运算符，第 15 页
- 相等性，第 78 页
- 就地修改，第 47 页
- 交集运算符，第 15 页
- 长度，第 75 页
- 移除元素，第 15 页
- 对称差集运算符，第 15 页
- 并集运算符，第 15 页
- 更新，第 15 页

## setsid() 函数
os 模块，第 381 页

## setslice() 函数
operator 模块，第 274 页

## setsockopt() 方法
socket 对象的方法，第 484 页

## setstate() 函数
random 模块，第 254 页

### __setstate__() 方法
第 228 页
及复制，第 220 页
及 pickle 模块，第 172 页

## @setter 属性装饰器
第 126 页

## settimeout() 方法
socket 对象的方法，第 484 页

设置标准 I/O 的默认编码
第 175 页

## settrace() 函数
sys 模块，第 235 页
threading 模块，第 444 页

## setuid() 函数
os 模块，第 381 页

## setUp() 方法
TestCase 对象，第 184 页
TestCase 对象的方法，第 184 页

## setup() 函数
distutils 模块，第 152、596 页

## setup() 方法
BaseRequestHandler 对象的方法，第 490 页

## setup.py 文件
- C 扩展，第 596 页
- SWIG 扩展，第 620 页
- 及 setuptools，第 154 页
- 创建，第 152-153 页
- install 命令，第 153-154 页
- 安装到用户站点目录，第 178 页

## setuptools 库
第 147、154 页

## SetValue() 函数
winreg 模块，第 411 页

## SetValueEx() 函数
winreg 模块，第 411 页

## sha1() 函数
hashlib 模块，第 559 页

## sha224() 函数
hashlib 模块，第 559 页

## sha256() 函数
hashlib 模块，第 559 页

## sha384() 函数
hashlib 模块，第 559 页

## sha512() 函数
hashlib 模块，第 559 页

## 浅拷贝
第 36 页
- 字典的浅拷贝，第 45 页
- 列表的浅拷贝，第 40 页
- 序列复制，第 67 页

## 共享数组
multiprocessing 模块，第 426 页

## 共享库
- 扩展模块，第 148 页
- 使用 ctypes 加载，第 612 页

## 共享内存
- 传递列表的示例，第 427 页
- multiprocessing 模块，第 426 页

## 对象共享
第 35 页

## Shelf 类
shelve 模块，第 311 页

## shell 命令
- 收集输出，第 331 页
- 在 Python 中模拟，第 318 页

## shell 管道
与生成器的相似性，第 106 页

##### shelve 模块
第 171、311 页
- dbhash 模块，第 311 页
- 选择 pickle 协议，第 172 页

## shlex 模块
第 588 页

## 短路求值
布尔表达式的短路求值，第 78 页

## showwarning() 函数
warnings 模块，第 239 页

## shuffle() 函数
random 模块，第 255 页

## shutdown() 函数
logging 模块，第 366 页

## shutdown() 方法
- BaseManager 对象的方法，第 431 页
- SocketServer 对象的方法，第 492 页
- socket 对象的方法，第 484 页

## shutil 模块
第 318 页

## 副作用
- 函数中的副作用，第 95 页
- 避免副作用的原因，第 96 页

## SIG* 信号名
第 400 页

## SIGHUP 信号
第 179 页

## siginterrupt() 函数
signal 模块，第 400 页

## 信号处理
第 399 页

## signal 模块
第 399 页

## signal() 函数
signal 模块，第 400 页

## 信号传递
使用信号量，第 439 页

##### 信号
- 生成器的 close() 方法，第 104 页
- 信号列表，第 400 页
- 与线程混合，第 402 页
- 生成器的 throw() 方法，第 105 页

## SimpleXMLRPCServer 模块
第 527 页

## sin() 函数
math 模块，第 252 页

## 单精度浮点数
第 39 页

## 单元素元组
第 14 页

## sinh() 函数
math 模块，第 252 页

##### 站点配置文件
第 177 页

## site 模块
第 166、174、177 页

## site-packages 目录
第 175 页

## sitecustomize 模块
第 177 页

## size 属性
- Struct 对象的属性，第 291 页
- TarInfo 对象的属性，第 322 页

## size() 方法
- FTP 对象的方法，第 499 页
- mmap 对象的方法，第 371 页

## Sized 抽象基类
第 265 页

## sizeof() 函数
ctypes 模块，第 618 页

## skippedEntity() 方法
ContentHandler 对象的方法，第 581 页

## sleep() 函数
time 模块，第 406 页

## 睡眠
第 406 页
- 直到接收到信号，第 399 页

## 切片赋值
列表切片赋值，第 12 页

####### 切片对象
第 51、53 页
- 及索引方法，第 59 页
- 属性，第 54 页

## 切片类型
第 51 页

## slice() 函数
第 53、210 页

## 切片操作
第 39 页
- 及特殊方法，第 59 页
- 及 xrange 对象，第 44 页
- 赋值，第 40、69 页
- 删除，第 40、69 页
- 多维切片，第 59 页

## 切片运算符 [:]
第 67-68 页
- 列表切片，第 12 页
- 字符串切片，第 11 页

## __slots__ 属性
- 及实例的 __dict__ 属性，第 50 页
- 与其他代码的兼容性，第 133 页
- 继承，第 133 页
- 类定义中的 __slots__，第 132 页
- 优化，第 196 页

## Smalltalk
对象系统的差异，第 124 页

## SMTP 协议
发送消息的示例，第 514 页

## SMTP() 函数
smtplib 模块，第 514 页

## smtpd 模块
第 587 页

## SMTPHandler 类
logging 模块，第 363 页

## smtplib 模块
第 513 页

## sndhdr 模块
第 588 页

## sniff() 方法
Sniffer 对象的方法，第 550 页

## Sniffer() 函数
csv 模块，第 550 页

## SO_* 套接字选项
socket 模块，第 479 页

## SOCK_* 常量
socket 模块，第 470 页

## socket 属性
SocketServer 对象的属性，第 492 页

## socket 模块
第 469 页

## socket() 函数
socket 模块，第 476 页

## 套接字
定义，第 449 页

## socket_type 属性
SocketServer 类的属性，第 493 页

## SocketHandler 类
logging 模块，第 363 页

## socketpair() 函数
socket 模块，第 477 页

## 套接字
- 地址族，第 470 页
- 方法，第 478 页
- 使用 select() 进行轮询，第 459 页
- 指定网络地址，第 471 页
- 类型，第 470 页

## SocketServer 模块
第 489 页
- 及 Python 3，第 489 页
- 更改服务器参数，第 492 页

## softspace 属性
文件对象的属性，第 161 页

## sort() 方法
列表的方法，第 40-41 页

## sorted() 函数
第 210 页

## 排序
- 更改排序行为，第 40 页
- 列表就地排序，第 40 页
- 对象的要求，第 57 页
- 反向排序，第 40 页
- 使用 operator 模块，第 275 页

#### 源代码编码
第 31 页
- Python 3，第 622 页

## span() 方法
MatchObject 对象的方法，第 286 页

## spawnl() 函数
os 模块，第 393 页

## spawnle() 函数
os 模块，第 393 页

## spawnlp() 函数
os 模块，第 393 页

## spawnlpe() 函数
os 模块，第 393 页

## spawnv() 函数
os 模块，第 392 页

## spawnve() 函数
os 模块，第 393 页

## spawnvp() 函数
os 模块，第 393 页

## spawnvpe() 函数
os 模块，第 393 页

## 特殊方法
第 21、54 页

## 特殊符号
第 30 页

## 加速
定义，第 192 页

## split() 函数
- os.path 模块，第 398 页
- re 模块，第 284 页

## split() 方法
- Regex 对象的方法，第 285 页
- 字符串的方法，第 14、41、43 页

## splitdrive() 函数
os.path 模块，第 398 页

## splitext() 函数
os.path 模块，第 398 页

## splitlines() 方法
字符串的方法，第 44 页

## 字符串分割
第 14、43 页

## splitunc() 函数
os.path 模块，第 398 页

## SpooledTemporaryFile() 函数
tempfile 模块，第 324 页

## sprintf() 函数等价物
第 70 页

## spwd 模块
第 587 页

## SQL 查询
- SQL 注入攻击，第 300 页
- 示例，第 309 页
- 在数据库上执行，第 297 页
- 如何构造，第 300 页
- 与列表推导的相似性，第 111 页

## SQLite 数据库
第 303 页

#### sqlite3 模块
第 303 页

## sqrt() 函数
math 模块，第 252 页

## sqrt() 方法
Decimal 对象的方法，第 243 页

## ssl 模块
第 486 页

## SSL
创建证书的示例，第 489 页

## st_* 属性
stat 对象的属性，第 389 页

## 栈帧
第 52 页
- 在回溯中，第 53 页

## 栈大小
线程的栈大小，第 444 页

## stack() 函数
inspect 模块，第 225 页

## stack_size() 函数
threading 模块，第 444 页

## Stackless Python
第 467 页

## 标准 I/O 流
第 161 页
- 及集成开发环境，第 162 页
- 设置默认编码，第 175 页

## 标准错误
第 157 页

## 标准输入和输出
第 10 页

## 标准库重组
Python 3，第 634 页

## standard_b64decode() 函数
base64 模块，第 546 页

## standard_b64encode() 函数
base64 模块，第 546 页

## StandardError 异常
第 87 页

## starmap() 函数
itertools 模块，第 272 页

## start 属性
切片的属性，第 54 页

## start() 方法
- BaseManager 对象的方法，第 431 页
- MatchObject 对象的方法，第 286 页
- Process 对象的方法，第 416 页
- Thread 对象的方法，第 436 页
- Timer 对象的方法，第 438 页
- TreeBuilder 对象的方法，第 577 页

## startDocument() 方法
ContentHandler 对象的方法，第 582 页

## startElement() 方法
ContentHandler 对象的方法，第 582 页

## startElementNS() 方法
ContentHandler 对象的方法，第 582 页

## startfile() 函数
os 模块，第 393 页

## startPrefixMapping() 方法
ContentHandler 对象的方法，第 582 页

## startswith() 方法
字符串的方法，第 44 页

## 启动脚本
交互模式下的启动脚本，第 174 页

## stat 模块
第 387、587 页

## stat() 函数
- os 模块，第 388 页
- os.path 模块，第 398 页



#### 字符串

- `stat_float_times()` 函数，os 模块，389
- 语句终止，7
  - 与分号，7
- 语句
  - 跨多行书写，9
  - 写在同一行，25-26
  - 在调试器中运行，186
- 静态方法，22，48，123，125
  - 实际用途，123
- `@staticmethod` 装饰器，22，48，123，125，210
- 统计，随机数分布，255
- `status` 属性，`HTTPResponse` 对象的，504
- `statvfs()` 函数，os 模块，389
- `stderr` 属性，`Popen` 对象的，404
- `stderr` 变量，sys 模块，161，232
- `__stderr__` 变量，sys 模块，162，232
- `stdin` 属性，`Popen` 对象的，404
- `stdin` 变量，sys 模块，10，161，232
- `__stdin__` 变量，sys 模块，162，232
- `stdout` 属性，`Popen` 对象的，404
- `stdout` 变量，sys 模块，10，161，232
- `__stdout__` 变量，sys 模块，162，232
- `step` 属性，切片的，54
- `StopIteration` 异常，59，87，215
  - 与生成器，103
- `storbinary()` 方法，FTP 对象的，499
- `storlines()` 方法，FTP 对象的，499
- `str` 类型，38
- `str()` 函数，11，56，76，210
  - 与 `print`，162
  - 与 `repr()` 的区别，12
- `__str__()` 方法，55-56
- `StreamError` 异常，tarfile 模块，322
- `StreamHandler` 类，logging 模块，363
- `StreamReader` 类，codecs 模块，278
- `streamreader()` 方法，`CodecInfo` 对象的，278
- `StreamRequestHandler` 类，SocketServer 模块，491
- 流，470
- `StreamWriter` 类，codecs 模块，278
- `streamwriter()` 方法，`CodecInfo` 对象的，278
- `strerror()` 函数，os 模块，381
- `strftime()` 函数，time 模块，406
- `strftime()` 方法
  - `date` 对象的，337
  - `time` 对象的，338
- `'strict'` 错误处理，Unicode 编码，166
- `string` 属性，`MatchObject` 对象的，286
- 字符串格式化，70
  - `!r` 说明符，74
  - `!s` 说明符，74
  - 对齐，73
  - 属性查找，72
  - `%` 运算符的格式代码，70-71
  - 自定义 `format()` 方法，74
  - 字典，72
  - 字典查找，72
  - 填充字符，73
  - 格式说明符，72
  - 格式化运算符 `%`，70
- 字符串插值，72，163
- 字符串字面量，27
  - Unicode 字符，28
  - 与 Unicode 编码，29
  - 与文档字符串，30
  - 字节字符串，29
  - 源代码中的 Unicode 字符，31
- string 模块，287
  - 模板字符串，164
- `string_at()` 函数，ctypes 模块，618
- `StringIO` 类，io 模块，353
- stringprep 模块，586
- 字符串，11
  - Unicode，41，165
  - 与数值计算，11
  - 作为字典键，16
  - 作为内存中的文本文件，353
  - 作为序列，39
  - 用于类型检查的 `basestring` 对象，202
  - 字节字面量，29
  - 字节字符串，41，202
  - 大小写转换，43-44
  - 字符替换，42
  - 比较，70
  - 拼接，11
  - 相邻字面量的拼接，27
  - 创建自定义格式化器，288
  - 禁用字面量中的转义码，29
  - 用于 URL 的编码，522
  - 字面量中的转义码，27
  - 转义用于 HTML 的字符，536
  - 转义用于 XML 的字符，583
  - 执行其中包含的 Python 代码，115
  - `format()` 方法，8，72
  - 格式化，8，42
  - 日志消息中的格式化，358
  - 不可变性，41，69
  - 索引，11
  - 内部表示，28
  - 遍历字符，17
  - 连接，43
  - 行结构，11
  - 混合字节字符串和 Unicode，70
  - 可变字节数组，202
  - 分区，41
  - 正则表达式，281
  - 替换子字符串，41
  - 查找子字符串，41
  - 切片，11
  - 排序与国际化，70
  - `format()` 方法的说明符，72-73
  - 分割，43
  - 按字段分割，14，41
  - 去除空白，43
  - 反转义 XML 字符引用，583

## 去除空白

- 从字符串中去除控制字符，42
- 字符串，44

`strptime()` 函数，time 模块，343，407

`strptime()` 方法，`datetime` 类的，339

`Struct` 类，struct 模块，291

struct 模块，290

`Structure` 类，ctypes 模块，614

结构体，与元组，14

## `sub()` 函数

- operator 模块，273
- re 模块，284

`sub()` 方法，`Regex` 对象的，285

`__sub__()` 方法，60

子类，119

`__subclasscheck__()` 方法，57，136

`subdirs` 属性，`dircmp` 对象的，315

`SubElement()` 函数，`xml.etree.ElementTree` 模块，575

`subn()` 函数，re 模块，284

`subn()` 方法，`Regex` 对象的，285

subprocess 模块，402

subprocess，定义，413

## `substitute()` 方法

- `Template` 对象的，289
- 模板字符串的，164

## 子字符串

- 使用 `in` 检查是否存在，69
- 查找，41

减法运算符 `-`，65

`successful()` 方法，`AsyncResult` 对象的，425

`sum()` 函数，39-40，67，210
- 精度，252
- 与 decimal 模块，69
- 仅限数值数据，39
- 与 `math.fsum()` 函数的比较，252

sunau 模块，588

`super()` 函数，120，210
- Python 3，210，627

超类，119
- 调用其中的方法，120
- `super()` 函数，120

`strip()` 方法，字符串的，44

同时支持 Python 2 和 3，638

`supports_unicode_filenames` 变量，os.path 模块，398

代理对，28，41

挂起，线程的，443

`swapcase()` 方法，字符串的，44

### SWIG

- 示例，619
- 接口文件，619

switch 语句，不存在，9

### symbol 模块，586

符号链接，检测文件名是否为符号链接，397

`symlink()` 函数，os 模块，389

对称差集运算符 `^`，集合的，15

`symmetric_difference()` 方法，集合的，46

`symmetric_difference_update()` 方法，集合的，47

### `sync()` 方法

- dbm 风格数据库对象的，310
- `shelve` 对象的，311

### 同步原语

- multiprocessing 模块，427
- threading 模块，438

### 同步

- 生成器的 `close()` 方法的同步，104
- 并发程序的同步，414
- 生成器的 `throw()` 方法的同步，105

### `SyntaxError` 异常

- 87，215
- Python 3 的 `print` 语句，6
- 与默认参数，93
- 与 `except` 语句，85

### `SyntaxWarning` 警告

- 216，238

### sys 模块，13，229

### `sys.argv` 变量，13，157，174

### `sys.displayhook` 变量，176

### `sys.exec_prefix` 变量，177

### `sys.exit()` 函数，179

### `sys.modules` 变量，144，149

### `sys.path` 变量，147
- 与 site 模块，177
- 第三方模块，154

### `sys.prefix` 变量，177

### `sys.ps1` 变量，176

### `sys.ps2` 变量，176

### `sys.stderr` 变量，157，161

### `sys.stdin` 变量，161

### `sys.stdout` 变量，161

### `sys_version` 属性，`BaseHTTPRequestHandler` 类的，508

### `sysconf()` 函数，os 模块，395

### syslog 模块，587

### `SysLogHandler` 类，logging 模块，363

### 系统调用，os 模块，378

### 系统错误码，344

### `system()` 函数，os 模块，393

### `system.listMethods()` 方法，`ServerProxy` 对象的，525

### `SystemError` 异常，87，215

### `SystemExit` 异常，7，87-88，157，179，215

## T

- `-t` 命令行选项，26，173-174
- 字符串中的制表符转义码，28
- `tabcheck` 属性，`sys.flags` 的，230
- `TabError` 异常，26，87，215
- tabnanny 模块，586
- 制表符，与缩进，26
- `tag` 属性，`Element` 对象的，576
- `tagName` 属性，DOM `Element` 对象的，572
- `tail` 属性，`Element` 对象的，576
- `tail` 命令，生成器示例，19
- 尾递归优化，不存在，112
- `takewhile()` 函数，itertools 模块，272
- `tan()` 函数，math 模块，252
- `tanh()` 函数，math 模块，252
- `TarError` 异常，tarfile 模块，322
- `TarFile` 对象，tarfile 模块，320

# 任务调度器，协程与 `select()` 示例

- 任务调度器，协程与 `select()` 示例，460

- `terminate()` 方法
  - `Pool` 对象的，425
  - `Popen` 对象的，403–404
  - `Process` 对象的，416

- `task_done()` 方法
  - `JoinableQueue` 对象的，419
  - `Queue` 对象的，445

- 使用分号终止语句，7

- 任务小程序，446
  - 异步 I/O，460

- 终止
  - 不进行垃圾回收的立即终止，391
  - 程序的终止，179
  - 线程的终止，443
  - 注册清理函数，219
  - `sys.exit()` 函数，233
  - 不进行垃圾回收的终止，179

- 任务，与协程，20

- `tb_*` 属性，traceback 对象的，53

- `tb_lineno()` 函数，traceback 模块，236

- `tbreak` 调试器命令，pdb 模块，189

- termios 模块，587

- `tcgetpgrp()` 函数，os 模块，385

- test 模块，586

- TCP 连接，示意图，450

- `test()` 函数，cgi 模块，537

- TCP 协议，449
  - 示例代码，451

- `TestCase` 类，unittest 模块，184

- `TCP_*` 套接字选项，socket 模块，482

- 测试
  - doctest 模块，181
  - 文档字符串，181
  - doctest 的局限性，183
  - 单元测试，183

- `TCPServer` 类，SocketServer 模块，491

- `tcsetpgrp()` 函数，os 模块，385

- `testmod()` 函数
  - `doctest()` 模块，182
  - doctest 模块，182

- `tearDown()` 方法
  - `TestCase` 对象，184
  - `TestCase` 对象的，184

- `tee()` 函数，itertools 模块，273

- `testzip()` 方法，`ZipFile` 对象的，326

- `tell()` 方法
  - `IOBase` 对象的，350
  - 文件的，160–161
  - `mmap` 对象的，371

- `Text` 类，`xml.dom.minidom` 模块，572
- 文本 I/O，353
- `text` 属性，`Element` 对象的，576
- 文本文件模式，159
- 文本替换，字符串的 `replace()` 方法，41
- Python 3 中的文本与字节，629
- `text_factory` 属性，`Connection` 对象的，308
- `TextIOBase` 抽象基类，354
- `TextIOWrapper` 类，io 模块，353
- textwrap 模块，586

- telnetlib 模块，587

- `tempdir` 变量，tempfile 模块，324
- tempfile 模块，323
- `Template` 类，string 模块，289

#### 线程

CPU 密集型任务，444
添加到网络服务器，494
原子操作与反汇编，193
检查间隔，234
生成器的 close() 方法，104
与协程比较，467
条件变量，441
守护线程，359
数据库模块，302
decimal 模块，249
定义，413
事件，440
扩展模块，607
全局解释器锁，414，444
本地存储，443
主线程，413
互斥锁，438
获取活跃线程数量，443
随机数生成，256
可重入互斥锁，438
扩展性特性，415
调度，414
信号量，439
设置栈大小，444
设置名称，436
信号处理，402
使用信号量进行信号传递，439
挂起，443
同步，414
终止，443
生成器的 throw() 方法，105
使用队列，444
工作线程示例，446

## threadsafety 变量，数据库 API，302

## throw() 方法，生成器，53，105-106

## time 和 date 解析，407

## time 类，datetime 模块，338

## 时间操作，336

## time 模块，191，405

时间函数的精度，408
当前时间，405

## 时间解析，343

## Time() 函数，数据库 API，301

## time() 函数，time 模块，191，407

## time() 方法，datetime 对象，340

## timedelta 类，datetime 模块，340

## TimedRotatingFileHandler 类，logging 模块，363

## TimeFromTicks() 函数，数据库 API，301

## timeit 模块，191

## timeit() 函数

cProfile 模块，190
timeit 模块，191

## timeout 属性，SocketServer 类，493

## timeout 异常，socket 模块，485

## 超时，使用闹钟信号的示例，401

## Timer() 函数，threading 模块，437

## times() 函数，os 模块，394

## timezone 变量，time 模块，709

## 时间测量，191

## TIPC 协议，470

- 地址格式，472

## TIPC_* 常量，socket 模块，473

## title() 方法，字符串，44

## Tkinter 模块，588

## today() 方法，date 类，336

## tofile() 方法，array 对象，260

## token 模块，586

## tokenize 模块，586

## tolist() 方法，array 对象，260

## toordinal() 方法，date 对象，337

## toprettyxml() 方法，DOM Node 对象，572

## tostring() 函数，xml.etree.ElementTree 模块，578

## tostring() 方法，array 对象，260

## total_changes 属性，Connection 对象，308

## tounicode() 方法，array 对象，260

## toxml 方法，DOM Node 对象，573

## trace() 函数，inspect 模块，225

## 回溯消息，22

## traceback 模块，235

## traceback 对象，51-52

- 属性，53
- 栈帧，53

## __traceback__ 属性，Exception 对象，213

## tracebacklimit 变量，sys 模块，232

## 回溯

- 使用 traceback 模块创建，236
- 限制输出量，232

## TracebackType 类型，51，237

## 复数字面量中的尾随 J，27

## 长整数中的尾随 L，27

## 尾随逗号

- 与元组，14
- print 语句，162

## transfercmd() 方法，FTP 对象，500

## translate() 方法，字符串，42，44

## traps 属性，Context 对象，247

## TreeBuilder() 函数，xml.etree.ElementTree 模块，577

## triangular() 函数，random 模块，256

## 三引号字符串，11

- 与变量插值，163

## True 值，9，27，38

## truediv() 函数，operator 模块，273

## __truediv__() 方法，60

## trunc() 函数，math 模块，252

## truncate() 方法

- IOBase 对象，350
- 文件，160

## 截断除法运算符 //，65

## 截断，整数除法，61，65

## 真值测试，78

## 真值，9

## truth() 函数，operator 模块，274

## try 语句，22，84-85

## -tt 命令行选项，26，173-174

## tty 模块，587

## ttyname() 函数，os 模块，385

## 调优策略，194

## 元组类型，38

## 元组解包，与 for 循环，15

## tuple() 函数，77，211

## 元组，14

- 与字符串格式化，70
- 作为字典键，16
- 作为字典键，74
- 作为序列，39
- 比较，70
- 连接，14
- 从字典创建列表，45
- 使用命名属性创建，264
- 不可变性，14
- 不可变性，69
- 索引，14
- 内存节省，14
- 省略括号，14
- 用作数据结构的问题，264
- 表示记录，14
- 单元素元组，14
- 切片，14
- Python 3 中的解包，623
- 在迭代中解包，82
- 标准库使用，265
- 在列表推导中使用，109
- 与列表比较，14

## Twisted 库，415，467

## 二维列表，13，15

## 类型，47

## type 属性

- FieldStorage 对象，535
- TarInfo 对象，322
- socket 对象，484

###### 类型检查

- 使用元类的示例，140
- 对象类型检查，34
- 性能影响，34
- 代理对象的问题，135

## 类型强制转换，与运算符重载，134

## 对象类型比较，34

## 类型转换，76

- 缺乏隐式转换，62
- 数据文件中的列类型转换，37
- 用于转换的特殊方法，62

## 类型层次结构，138

## 类型对象，50

## 对象的类型，33

## type() 函数，34，211

- 与异常，89

## type() 元类，138

## type_options 属性，FieldStorage 对象，535

## typecode 属性，array 对象，259

## TypeError 异常，87，215

- 与函数调用，94
- 与类型强制转换，62
- 方法解析顺序，122

## types 模块，47，237

- 与 Python 3，237

## 类型

- 布尔型，38
- 内置类型，37，201
- 可调用类型，47
- 字典类型，44
- 浮点类型，38
- 冻结集类型，46
- 整数类型，38
- socket 类型，470
- 集合类型，46
- 类型本身，47

## tzinfo 属性，time 对象，338

## tzname 变量，time 模块，405

## tzname() 方法

- time 对象，339
- tzinfo 对象，342

## tzset() 函数，time 模块，407

## U

## \U 转义码，字符串中，28

## \u 转义码，字符串中，28

## -U 命令行选项，28，173

## 'U' 模式，open() 函数，159

## u 字符，字符串字面量前，28

## -u 命令行选项，173

## u(p) 调试器命令，pdb 模块，189

## UDP 客户端示例，486

## UDP 通信，图示，451

## UDP 协议，449

## UDP 服务器示例，485

## UDPServer 类，SocketServer 模块，491

## uid 属性，TarInfo 对象，322

## umask() 函数，os 模块，381

## unalias 调试器命令，pdb 模块，189

## uname 属性，TarInfo 对象，322

## uname() 函数，os 模块，381

## 一元减运算符 -，65

## 一元加运算符 +，65

## 未绑定方法，49

- 与 Python 3，49

## UnboundLocalError 异常，87，98，215

## 无缓冲文件 I/O，159

## unconsumed_tail 属性，decompressobj 对象，329

## 下划线，在标识符中的使用，26

## unescape() 函数，xml.sax.saxutils 模块，583

## ungetch() 函数，msvcrt 模块，373

## ungetwch() 函数，msvcrt 模块，373

## unhexlify() 函数，binascii 模块，548

## unichr() 函数，77，211

## Unicode 字符数据库，293

## Unicode 字符，表示，41

## Unicode 字符串字面量，28

## Unicode 字符串，41

- 与 WSGI，541
- 常用编码，166
- 分解，295
- 编码和解码，165
- 网络程序中的编码，452
- 错误处理选项，166
- 处理，165
- 与字节字符串混合，167
- 规范化，296
- 正则表达式，281

## unicode 属性，sys.flags，230

## unicode 类型，38

## unicode() 函数，211

- 与 Python 3，211

## Unicode

- Python 2 与 Python 3 对比，28
- 与 BOM 字符，168
- 与 XML，168
- 字节顺序标记，280
- 字符编码和解码，42
- 字符属性数据库，170
- 码点，28
- 常用编码，168–169
- 字符串字面量中的编码，29
- 源代码编码，31
- 文件 I/O，167
- 与字节字符串混合，70
- 字符串规范化，171
- 在字符串字面量中指定字符，28
- 代理对，28，41
- 使用 32 位字符码点，41

## unicode-escape 编码，描述，170

## unicodedata 模块，170，293

## UnicodeDecodeError 异常，87，215

## UnicodeEncodeError 异常，87，215

- Python 3 交互模式，175

## UnicodeError 异常，87，166，215

## UnicodeTranslateError 异常，87，215

## unidata_version 变量，unicodedata 模块，296

## 整数与长整数类型的统一，38

## 统一访问原则，125

## 均匀类型数组，259

## uniform() 函数，random 模块，255

## Unimplemented FileMode 异常，http.client 模块，504

## Union 类，ctypes 模块，614

## union 运算符 |，集合，15

## union() 方法，集合，46

## 单元测试

- Python 3 迁移，635
- 示例，184

## unittest 模块，183

- 示例，184

## 通用换行模式，159

## UNIX 域协议，470

- 地址格式，472

## Unix 系统日志，发送消息到，363

## Unix

- #! 程序执行，6
- 用户站点目录，177
- 时间纪元定义，405

## UnixDatagramServer 类，SocketServer 模块，491

## UnixStreamServer 类，SocketServer 模块，491

## UnknownHandler 类，urllib.request 模块，518

安装，154
安装到用户站点目录，154，178

## this 指针，方法的 self 参数，119

## Thread 类，threading 模块，436

## thread 属性，Record 对象，359

## threading 模块，436

同步原语，438

## ThreadingMixIn 类，SocketServer 模块，494

## ThreadingTCPServer 类，SocketServer 模块，494

## ThreadingUDPServer 类，SocketServer 模块，494

## threadName 属性，Record 对象，359

## U

- UnknownProtocol 异常，http.client 模块，504
- UnknownTransferEncoding 异常，http.client 模块，504
- unlink() 函数，os 模块，390
- 卸载模块，149
- unpack() 函数，struct 模块，290
- unpack() 方法，Struct 对象的，291
- unpack_from() 函数，struct 模块，291
- unpack_from() 方法，Struct 对象的，291
- 解包
  - 二进制数据结构，290
  - 序列的解包，67-68
  - 元组的解包，14
- Unpickler 类，pickle 模块，228
- unquote() 函数，urllib.parse 模块，522
- unquote_plus() 函数，urllib.parse 模块，522
- unquote_to_bytes() 函数，urllib.parse 模块，522
- unregister() 方法，Poll 对象的，460
- unregister_dialect() 函数，csv 模块，551
- unsetenv() 函数，os 模块，381
- until 调试器命令，pdb 模块，189
- unused_data 属性，decompressobj 对象的，329
- unwrap() 方法，ssl 对象的，488
- update() 方法
  - 字典的，45
  - 摘要对象的，559
  - hmac 对象的，560
  - 集合的，15, 47
- update_wrapper() 函数，functools 模块，269
- 更新字典，45
- 上传
  - 在 CGI 脚本中上传文件，536
  - 通过 POST 将文件上传到 HTTP 服务器，505
  - 将文件上传到 FTP 服务器，500
  - 将包上传到 PyPI，155
- upper() 方法，字符串的，44
- uppercase 变量，string 模块，287
- urandom() 函数，os 模块，396
- urldefrag() 函数，urllib.parse 模块，521
- urlencode() 函数，urllib.parse 模块，522
- URLError 异常，516
  - urllib.error 模块，523
- urljoin() 函数，urllib.parse 模块，521
- urllib 模块，522
  - 参见 urllib.request，515
- urllib 包，514
- urllib.error 模块，523
- urllib.parse 模块，520
- urllib.request 模块，515
- urllib.response 模块，520
- urllib.robotparser 模块，523
- urllib2 模块，参见 urllib.request，515
- urlopen() 函数，urllib.request 模块，515
- urlparse 模块，520
- urlparse() 函数，urllib.parse 模块，520
- urlsafe_b64decode() 函数，base64 模块，546
- urlsafe_b64encode() 函数，base64 模块，546
- urlsplit() 函数，urllib.parse 模块，521
- urlunparse() 函数，urllib.parse 模块，521
- urlunsplit() 函数，urllib.parse 模块，521
- 用户目录，包的安装，154
- user 模块，586
- setup.py 的 --user 选项，154
- 更改 HTTP 请求中的用户代理头部，517
- username 属性
  - urlparse 对象的，520
  - urlsplit 对象的，521
- UserWarning 警告，216, 238

*如何让这个索引更有用？请发送邮件至 indexes@samspublishing.com*

## V

- 将 Python 用作计算器，6
- utcfromtimestamp() 方法，datetime 类的，339
- utcnow() 方法，datetime 类的，339
- utcoffset() 方法
  - time 对象的，339
  - tzinfo 对象的，342
- utctimetuple() 方法，datetime 对象的，340
- UTF-16 编码，描述，170
- UTF-8
  - 与 ASCII 的兼容性，170
  - 描述，169-170
  - 编码和解码，42
  - 在字符串字面量中包含，29
  - 字典序排序，170
- utime() 函数，os 模块，390
- uu 模块，587

- 函数定义中的可变参数，94
- 变量，7
  - 作为对象的名称，35
  - 绑定与模块导入，145
  - 函数中全局变量的绑定，98
  - 类变量，117-118
  - 嵌套函数中的变量，97
  - 迭代变量，82
  - 命名规则，26
  - 变量的作用域，96, 98
- vars() 函数，72, 211
- verbose 属性，sys.flags 的，230
- verify_request() 方法，SocketServer 类的，493
- version 属性，HTTPResponse 对象的，504
- 版本信息，解释器的，231
- version 变量，sys 模块，232
- version_info 变量，sys 模块，232
- vformat() 方法，Formatter 对象的，288
- 视图对象，Python 3，632
- volume 属性，ZipInfo 对象的，327
- vonmisesvariate() 函数，random 模块，256
- -V 命令行选项，173
- -v 命令行选项，173-174
- validator() 函数，wsgiref.handlers 模块，543
- value 属性
  - FieldStorage 对象的，535
  - Morsel 对象的，512
- Value() 函数，multiprocessing 模块，426
- Value() 方法，Manager 对象的，429
- ValueError 异常，87, 215
  - 与列表，40
  - 与字符串，41
- valrefs() 方法，WeakValueDictionary 对象的，241
- values() 方法
  - Message 对象的，552
  - 字典的，45
  - Python 3 中字典的，632
- ValuesView 抽象基类，266
- 字符串中的变量插值，163
- 函数定义中的可变关键字参数，95

## W

- -W 命令行选项，216, 239-240
- 'w' 模式，open() 函数的，159
- w(here) 调试器命令，pdb 模块，189
- wait() 函数，os 模块，394
- wait() 方法
  - AsyncResult 对象的，425
  - Condition 对象的，441
  - Event 对象的，440
  - Popen 对象的，404
- wait3() 函数，os 模块，394
- wait4() 函数，os 模块，394
- waitpid() 函数，os 模块，394
- walk() 函数，os 模块，390
- walk() 方法，Message 对象的，554
- 包装器与属性绑定方法
- 获取挂钟时间，191
- while 语句，8, 82
- warn() 函数，warnings 模块，216, 239
- whitespace 变量，string 模块，287
- warn_explicit() 函数，warnings 模块，239
- WIFCONTINUED() 函数，os 模块，395
- WIFEXITED() 函数，os 模块，394
- Warning 警告，216, 238
- WIFSIGNALED() 函数，os 模块，395
- warning() 方法，Logger 对象的，357
- WIFSTOPPED() 函数，os 模块，395
- warnings 模块，238
- WinDLL() 函数，ctypes 模块，612
- 警告
  - 将警告转换为异常，239
  - 警告与异常的区别，216
  - 抑制警告，238
- Windows，331
  - 访问注册表，408
  - 访问注册表，175
  - 使用 distutils 创建二进制发行版，153
  - 双击运行 Python 程序，176
  - 文件名中的驱动器盘符，399
  - 文件锁定，373
  - 向事件日志发送消息，362
  - 错误代码列表，346
  - 使用 multiprocessing 模块的主程序，417
  - 用户级站点目录，177
  - 使用 multiprocessing 进行进程 fork，435
  - 运行程序，6
- warnoptions 变量，sys 模块，232
- WindowsError 异常，215
- WatchedFileHandler 类，logging 模块，363
- Wing IDE，5
- wave 模块，588
- winreg 模块，408
- WCOREDUMP() 函数，os 模块，394
- winsound 模块，588
- 弱引用，130
- winver 变量，sys 模块，232
- 弱引用，240
- with 语句，62, 89
- WeakKeyDictionary 类，weakref 模块，241
  - 与异常，23
  - 与锁，89
  - decimal 模块，248
  - 锁原语，442
- weakref 模块，130, 240
- WeakValueDictionary 类，weakref 模块，241
- 进程工作池，424
- Web 框架，538
- wrap_socket() 函数，ssl 模块，486
  - 与模板字符串，164
- Web 编程，531
- 包装函数，95
- Web 服务器

## X

- 716 wraps 装饰器，functools 模块
- @wraps 装饰器，functools 模块，114, 269
- writable() 方法
  - IOBase 对象的，350
  - dispatcher 对象的，456
- write() 函数，os 模块，385
- write() 方法
  - BufferWriter 对象的，352
  - ConfigParser 对象的，334
  - ElementTree 对象的，575
  - FileIO 对象的，350
  - StreamWriter 对象的，278
  - TextIOWrapper 对象的，353
  - ZipFile 对象的，326
  - 文件的，10, 159-160
  - mmap 对象的，372
  - ssl 对象的，488
- write_byte() 方法，mmap 对象的，372
- writelines() 方法
  - IOBase 对象的，350
  - StreamWriter 对象的，278
  - 文件的，159-160
- writepy() 方法，ZipFile 对象的，326
- writer() 函数，csv 模块，549
- writerow() 方法
  - csv DictWriter 对象的，550
  - csv writer 对象的，549
- writerows() 方法
  - csv DictWriter 对象的，550
  - csv writer 对象的，550
- writestr() 方法，ZipFile 对象的，327
- writexml() 方法，DOM Node 对象的，573
- 写入文件，159
- WSGI（Web 服务器网关接口），540
- WSGI
  - 应用规范，540
  - 示例，541
  - 与 Web 框架集成，543
  - 处理表单字段，541
  - 运行独立服务器，542
  - 在 CGI 脚本中运行，542
  - 使用生成器进行 I/O，165
  - 应用验证，543
- wsgi.* 环境变量，540
- wsgiref 包，542
- wsgiref.handlers 模块，542
- wsgiref.simple_server 模块，542
- WSTOPSIG() 函数，os 模块，395
- wstring_at() 函数，ctypes 模块，618
- WTERMSIG() 函数，os 模块，395

## Y

- \x 转义码，在字符串中，28
- -x 命令行选项，173-174
- xdrlib 模块，587
- xml 包，568
- XML() 函数，xml.etree.ElementTree 模块，575
- XML
  - 转义和反转义字符，583
  - 示例文档，569
  - 大文件的增量解析，579
  - ElementTree 模块中的命名空间，578
  - 解析，568
- XML-RPC，524
- XML-RPC 服务器，多线程示例，494
- XML-RPC
  - 示例，529
  - 服务器定制，530
- xml.dom.minidom 模块，570
- xml.etree.ElementTree 模块，573
- xml.sax 模块，580
- xml.sax.saxutils 模块，583
- 'xmlcharrefreplace' 错误处理，166-167
- XMLGenerator() 函数，xml.sax.saxutils 模块，584
- XMLID() 函数，xml.etree.ElementTree 模块，575
- xmlrpc 包，524
- xmlrpc.client 模块，524
- xmlrpc.server 模块，527
- xmlrpclib 模块，524



## XSLT，569

**XMLRPCServer类，xmlrpc.server模块，527**

**xor()函数，operator模块，274**

**__xor__()方法，60**

**XPATH，569**

**xrange类型，38**

**xrange()与列表的比较，44**

**xrange()函数，17，44，211**
- 与Python 3，17，44，211

## Y

**Y2K处理，407**

**year属性，日期对象的属性，337**

**yield表达式，20，104**

**yield语句，19，53，102**
- 与上下文管理器，90
- 与I/O结合使用，164-165

## Z

**ZeroDivisionError异常，87，215**

**zfill()方法，字符串的方法，44**

**.zip文件**
- 与模块，147
- 解码与编码，324
- 用作代码归档，147

**zip()函数，83，211**
- 与Python 3，211
- future_builtins模块，217
- 类型转换示例，37

**zipfile模块，324**

**ZipFile()函数，zipfile模块，325**

**zipimport模块，586**

**ZipInfo()函数，zipfile模块，325**

## LearnIT 于 InformIT

## 超越书本

**11种学习方式** 请访问 www.informIT.com/learn

Pearson Education 出版品牌的数字网络

## 尝试 Safari Books Online 免费试用

在线访问 5,000+ 图书和视频

免费试用——今天就开始！
www.informit.com/safaritrial

**快速找到可靠答案**
只有 Safari 允许您搜索来自顶级技术出版商（包括 Addison-Wesley Professional、Cisco Press、O'Reilly、Prentice Hall、Que 和 Sams）的数千本畅销书。

**掌握最新工具和技术**
除了能够访问大量技术书籍外，Safari 广泛的视频教程集还让您能够向领先的视频培训专家学习。

## 等等，还有更多！

**保持您的竞争优势**
通过 Rough Cuts，您可以访问正在开发的书稿，并率先学习最新技术。

**紧跟新兴技术**
Short Cuts 和 Quick Reference Sheets 是简短、简洁、重点突出的内容，旨在帮助您快速掌握新的前沿技术。

## 免费在线版

您购买的 **Python Essential Reference** 包含通过 Safari Books Online 订阅服务免费访问在线版 45 天的权限。几乎所有 Addison-Wesley Professional 图书都可通过 Safari Books Online 在线获取，此外还有来自 Cisco Press、Exam Cram、Que、IBM Press、O'Reilly、Prentice Hall 和 Sams 等出版商的 5,000 多本其他技术书籍和视频。

**SAFARI BOOKS ONLINE** 允许您搜索特定答案、剪切粘贴代码、下载章节，并紧跟新兴技术。

## 在以下网址激活您的免费在线版
www.informit.com/safarifree

1. **第1步：** 输入优惠码：GETJIXA。
2. **第2步：** 新 Safari 用户，请完成简短的注册表。Safari 订阅用户，只需登录即可。

如果您在注册 Safari 或访问在线版时遇到问题，请发送电子邮件至 customer-service@safaribooksonline.com
