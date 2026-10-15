
大多数 Linux 和 UNIX 版本，包括预装了 Python 的 Mac OS。这部分是为了方便，因为它是一种非常流行的脚本语言——而且如果用户想运行脚本，就节省了以后安装的时间；部分是因为 Linux 发行版中许多关键或实用的程序使用了 Python。

（注：第 736-737 页提供的 OCR 文本包含严重的损坏/重复伪影和乱码字符串，已根据 Python 上下文和文档可见片段进行了过滤/修正。）

# Python 基础

## 数字

Python 处理数字比其他语言更精确。它拥有所有的运算符，例如用于加法的 `+`、减法的 `-`、除法的 `/`、乘法的 `*`——它还有用于取模（除法余数）的 `%`、用于幂的 `**` 以及用于整除的 `//`。

### Python 基础 707

```python
>>> float (num)
10.0
>>> long (num)
10L
>>> floatnum = 10.0
>>> int(floatnum)
10
>>> float(floatnum)
10.0
>>> long(floatnum)
10L
```

你不需要担心使用的是整数（integer）还是长整数（long integer）；Python 会为你处理一切，所以你可以专注于编写正确的代码。在 3.x 系列中，Python 整数类型自动为大数字提供额外的精度，而在 2.x 中，对于超过普通类型设计范围的数字，你需要使用长整数类型。

## 关于字符串的更多

Python 将字符串存储为不可变的字符序列——这是一个充满术语的说法，意思是“它是一个字符集合，一旦设定，在不创建新字符串的情况下无法更改”。序列在 Python 中非常重要。主要有三种类型，字符串就是其中一种，它们共享一些属性。当你学习下一节的列表时，就会发现变异性（Mutability）非常有意义。

正如你在上一个示例中看到的，你只需要一个等号就可以给 Python 中的字符串赋值，例如：

```python
>>> string = 'hello'
>>> mystring = 'goodbye'
>>> string = 'hello'
>>> mystring = 'goodbye'
>>> test = "Are you really Bill O'Reilly?"
>>> test
```

第一个示例使用单引号封装字符串，第二个和第三个使用双引号。然而，打印第一个和第二个字符串时并无法看出它们的区别。第三个是例外；它使用双引号是因为字符串本身包含一个单引号。在这里，Python 使用双引号打印字符串，因为它包含单引号。

由于字符串中的字符是按顺序存储的，你可以通过指定感兴趣的字符来对其进行索引（index）。与大多数其他语言一样，这些索引是从 0 开始的，这意味着你需要请求字符 0 来获取字符串中的第一个字母。例如：

```python
>>> string = "This is a test string"
>>> string
'This is a test string'
>>> string[0]
'T'
>>> string[0], string[3], string[20]
('T', 's', 'g')
```

最后一行显示了如何通过逗号同时请求多个索引。你可以使用这种方法打印第一个单词：

```python
>>> string[0], string[1], string[2], string[3]
('T', 'h', 'i', 's')
```

然而，为了这个目的，你可以使用不同的概念：切片（slicing）。序列的切片会提取出一组索引。例如，你可以这样提取第一个单词：

```python
>>> string[0:4]
'This'
```

那里的语法意思是“从位置 0 开始（包含 0）一直到位置 4 结束（不包含 4）”。因此，`[0:4]` 复制了索引为 0、1、2 和 3 的项。你可以省略索引的任何一边，它将复制从开始到结束的所有内容：

```python
>>> string[:4]
'This'
>>> string[5:]
'is a test string'
>>> string[11:]
'est string'
```

你也可以省略数字，它会给你整个序列：

```python
>>> string[:]
'This is a test string'
```

稍后你将确切学习为什么要这样做，但现在还有其他字符串属性会让你的生活更轻松。例如，你可以使用 `+` 和 `*` 运算符来拼接（连接）和重复字符串，如下：

```python
>>> mystring = "Python"
>>> mystring * 4
'PythonPythonPythonPython'
>>> mystring = mystring + " rocks!"
>>> mystring * 2
'Python rocks! Python rocks! '
```

除了使用运算符外，Python 字符串还自带了一些内置方法。你可以使用 `capitalize()`（首字母大写，其余全小写）、`lower()`（全小写）、`title()`（每个单词的首字母大写）和 `upper()`（全大写）来改变字母的大小写。你还可以用 `lower()`、`istitle()` 和 `isupper()` 检查字符串的大小写匹配；这也扩展到了 `isalnum()`（如果字符串仅包含字母和数字则返回真）和 `isdigit()`（如果字符串全是数字则返回真）。

这个示例演示了这些的一些用法：

```python
>>> string
'This is a test string'
>>> string.upper()
'THIS IS A TEST STRING'
>>> string.lower()
'this is a test string'
>>> string.isalnum()
False
>>> string = string.title()
>>> string
'This Is A Test String'
```

为什么 `isalnum()` 返回 `False`——我们的字符串不是只包含字母和数字吗？不，不是的。里面有空格，这导致了问题。更重要的是，我们调用了 `upper()` 和 `lower()`，它们并没有改变字符串的内容——它们只是返回了新值。所以，为了将我们的字符串从 `This is To A Test String` 修改，我们必须将其赋值给字符串变量。

另一个你可以对字符串做的非常有用且酷酷的事情是三引号（triple quoting）。这些字符串让你能够轻松创建包含双引号和单引号的字符串，以及跨越多行的字符串，而无需转义大量的特殊字符。这里有一个例子：

```python
>>> foo = """This is a string
with "double" and 'single' quotes
and multiple lines."""
>>> foo
'This is a string
with "double" and \'single\' quotes
and multiple lines.'
```

列表有其的一套内置方法，如 `sort()`、`append()` 和 `pop()`。

后两个方法从列表末尾添加和删除单个元素，其中 `pop()` 还会返回被删除的元素。例如：

```
>>> list5 = ["nick", "paul", "Julian", "graham"]
>>> list5.sort()
>>> list5
['graham', 'julian', 'nick', 'paul']
>>> list5.pop('paul')
>>> list5
['graham', 'julian', 'nick']
```

```
>>> list5.append("Rebecca")
```

此外，字符串的一个有趣方法可以返回一个列表：`split()`。它根据字符进行拆分，并给您一个列表，其中每个元素都是字符串中的一个块。例如：

```
>>> string = "This is a test string"
>>> string.split(" ")
['This', 'is', 'a', 'test', 'string']
```

列表在 Python 中被广泛使用，尽管随着语言的成熟，这种情况正在发生变化。在 3.x 中，列表比较和排序的方式发生了变化，因此在你尝试执行这些任务时，请务必检查最新文档。

## 字典

与列表不同，字典是没有固定顺序的集合。相反，它们拥有键（元素的名称）和值（元素的内容），Python 将它们放在需要的地方以实现最大性能。在定义字典时，你需要使用大括号 (`{}`) 和冒号 (`:`)。你从左括号开始，然后给每个键赋值，并用逗号分隔，如下：

```
>>> mydict = {"perl": "a language", "php": "another language"}
>>> mydict
{'php': 'another language', 'perl': 'a language'}
```

这个示例有两个元素，perl 和 php。然而，当打印字典时，我们发现 php 在 perl 之前——Python 并没有遵循我们输入的顺序。我们可以使用普通代码对字典进行索引：

```
>>> mydict["perl"]
```

由于字典没有固定的序列，我们无法对其进行切片（slice）或通过位置进行索引。和列表一样，字典是可变的，并且也可以嵌套；但与列表不同的是，我们不能使用 `+` 来合并两个字典。这是因为字典元素是通过键来定位的。因此，两个相同键的元素会导致冲突。相反，你应该使用 `update()` 方法，它通过重写冲突的键来合并两个数组。

你还可以使用 `keys()` 方法返回字典中所有键的列表。

字典在 3.x 中的用法存在细微差异，例如，需要调用列表函数来一次性生成所有值以便打印。当你继续后续学习时，请务必检查列表文档，因为功能上发生了好几处变化，某些工具现在变得不同，甚至消失了，并且添加了新的字典工具。其中一些功能已经进行了向后移植（backported）；例如，Python 2.7 支持有序字典，该功能是从 Python 3.1 向后移植的（参见 http://docs.python.org/dev/whatsnew/2.7.html#pep-0372）。

## 条件判断与循环

到目前为止，我们只是在看数据类型，这应该向你展示了 Python 数据类型有多强大。然而，没有条件语句和循环，你就无法编写复杂的程序。

Python 拥有大多数标准的条件检查，如 `>`（大于）、`<=`（小于或等于），但它也添加了新的检查，如 `in`。例如，我们可以使用 `in` 来检查字符串或列表是否包含任何字符/元素：

```
>>> mystring = "U Random Hacker"
>>> "U" in mystring
True
>>> "Hacker" in mystring
True
>>> "hacker" in mystring
False
```

最后一个例子演示了它是如何区分大小写的。我们可以对列表使用运算符：

```
>>> mylist = ["soldier", "sailor", "tinker", "spy"]
>>> "tailor" in mylist
False
```

对这些复杂数据类型的其他比较是逐项完成的：

```
>>> list1 = ["alpha", "beta", "gamma"]
>>> list2 = ["alpha", "beta", "delta"]
>>> list1 > list2
True
```

`list1` 的第一个元素 (`alpha`) 与 `list2` 的第一个元素 (`alpha`) 进行比较，由于它们是相等的，所以检查下一个元素。该元素也相等，于是检查第三个元素，它们是不同的。`gamma` 中的 `g` 在字母表中位于 `d` 之后，因此 `gamma` 被认为大于 `delta`，且 `list1` 大于 `list2`。

循环有两种类型，两种都同样灵活。例如，`for` 循环可以遍历字符串中的字母或列表中的元素：

```
>>> string = "Hello, Python!"
>>> s in string:
    ... print s,
```

`for` 循环获取字符串中的每个字母并将其赋值给 `s`。然后使用 `print` 命令将其打印到屏幕上，但注意结尾的逗号；这告诉 Python 不要在每次循环后插入换行。省略号 (`...`) 是因为 Python 你在循环内部输入更多代码；你需要再次按回车来执行循环。

另一种类型是 `while` 循环，它看起来相似：

```
>>> i = 0
>>> while i < 3:
    ... print("Pos: " + str(i) + "," + str(j))
    ... i += 1
Pos: 0
Pos: 1
Pos: 2
```

你可以使用 `break` 和 `continue` 关键字控制循环。`break` 退出循环并立即继续后续，而 `continue` 跳到下一次迭代。我们再次发现了许多细微的差别。

定义一个类事乎其自然地以 `class` 关键字开始，后面跟着你正在定义的类名和一个冒号。该类的内容需要缩进一层，以便 Python 知道它在何结束。请注意，括号中的对象是用于对象继承的，这将在稍后进行讨论。目前，你最少需要知道的是，如果你的新类不是基于现有的类，你应该像之前的代码中那样在括号内放入 `object`。

类内部的函数工作方式与普通函数相同（尽管它们通常是方法）；主要的区别在于它们都至少接受一个参数，通常称为 `self`。这个参数被填充为调用该函数的对象的名称，并且你需要显式地使用它。

创建类的实例是通过赋值完成的。你不需要像某些其他语言那样使用任何 `new` 关键字——提供括号就让创建操作可见。调用该对象的函数使用点号 `.`，加上要调用的类，并将任何参数传递在括号内。

## 类变量和对象变量

每个对象都有自己的一组函数和变量，你可以独立于同类型的对象来操作这些变量。此外，某些类变量被为所有类设置了默认值，并且可以进行全局操作。

此脚本演示了两个 `dog` 类实例的创建，它们有自己的名称：

```python
class Dog(object):
    name = "Lassie"
    def bark(self):
        print(self.name + " Woof!")
    def set_name(self, name):
        self.name = name

fluffy = Dog()
fluffy.bark()
poppy = Dog()
poppy.set_name("Poppy")
poppy.bark()
```

输出内容如下：

Lassie says 'Woof!'

Poppy says 'Woof!'

每只狗都以 Lassie 作为名字，但它可以被自定义。默认按引用保留，这意味着每个对象都有指向类名变量的引用，当我们使用 `set_name()` 方法对其进行赋值时，该引用就会丢失。这意味着当我们更改类的变量时，该类中所有没有为该变量设置自己值的实例也会随之发生变化。例如：

```python
class Dog(object):
    name = "Lassie"
    color = "brown"

fluffy = Dog()
poppy = Dog()
print(fluffy.color)
Dog.color = "black"
print(poppy.color)
fluffy.color = "yellow"
print(fluffy.color)
print(poppy.color)
```

所以，狗的默认颜色是棕色——`fluffy` 和 `poppy` Dog 对象初始都是棕色。然后，通过 `Dog.color`我们将默认颜色设置为黑色，由于这两个对象都没有自己的颜色值，它们被更新为黑色。倒数第三行使用 `poppy.color` 为 `poppy` 对象设置了自定义颜色值——`poppy` 变成了黄色，而 `fluffy` 和整个狗类保持黑色。

## 构造函数和析构函数

为了帮助自动化创建和删除对象，你可以轻松地覆盖两个默认方法：`__init__` 和 `__del__`。这些是 Python 在类实例化和释放时调的方法，分别被称为构造函数和析构函数。

当你为每个创建的对象接受一组参数时，拥有自定义构造函数是非常棒的。例如，你可能希望每只狗在创建时都有自己的名字，你可以通过以下代码实现这一点：

```python
class Dog(object):
    def __init__(self, name):
        self.name = name
fluffy = Dog("Fluffy")
print(fluffy.name)
```

如果在创建 `Dog` 对象时没有提供 `name` 参数，Python 会报告错误并停止。当然，你可以根据需要请求任何构造参数，尽管通常最好只请求你需要的，并让其他函数填充剩余部分。

另一方面是析构方法，它让你对对象的销毁有更多控制。使用这两个方法，我们可以通过在创建和删除时打印消息来展示对象的生命：

```python
class dog(object):
    def __init__(self, name):
        self.name = name
        print(self.name + " is alive!")

    def __del__(self):
        print(self.name + "  is no more!")

fluffy = Dog("Fluffy")
```

析构是为了有机会释放分配给对象的资源，或者记录日志。注意，虽然可以覆盖 `__del__` 方法，但这是一个非常危险的想法，因为无法保证当解释器退出时仍然存在的对象的 `__del__` 方法会被调用。Python 官方文档在此处解释了这一点：http://docs.python.org/reference/datamodel.html#object.__del__

## 类继承
