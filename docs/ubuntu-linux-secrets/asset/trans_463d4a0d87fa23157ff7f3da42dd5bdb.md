

执行他们的任务。网页设计师和博主使用基于 Python 的工具 Zope 和 Plone 来生成他们的内容。地球物理学、电磁学和流体动力学领域的顶尖科学家在研究中使用 SciPy 库。

Python 程序员非常高效，因为该语言易于掌握，而且上手并不需要太多时间。它强调创建可读性强的代码，并在代码中明确说明正在发生的事情。语言能轻松处理许多日常维护工作，例如 I/O、内存管理、数据类型和变量绑定。

下一节将向你介绍有关在 Python 中编程以及在 Ubuntu 环境中可用的工具的一些内容。

## 使用 Python

与 Perl 类似，Python 也是一种解释型脚本语言，需要解释器来执行 Python 脚本。与 Perl 不同的是，Python 解释器还包括交互模式。在命令行输入命令 python 会以交互模式调用解释器：

```
$ python
Python 2.5.2 (r252:60911, Sep 14 2008, 10:31:08)
[GCC 4.3.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

交互式提示符现在正在等待你输入 Python 命令：

```
>>> print "This is a test"
This is a test
>>> 2 + 2
4
>>>
```

Python 交互环境中没有退出命令。要退出交互式解释器，请按 Ctrl+D，这会将你返回到正常的命令行提示符。

直接在解释器中输入 Python 命令并不是编程的简便方式。或者，你可以将 Python 命令存储在文本文件中，然后在命令行中包含文件名：

```
$ cat test11.py
# this is a sample Python script
print "This is a test Python script"
$ python test11.py
This is a test Python script
$
```

与 shell 和 Perl 脚本类似，你也可以从脚本内部调用 Python 解释器：

```
$ cat test12.py
#!/usr/bin/python
# Running a Python script
print "This is another script test"
$
```

## Python 编程

虽然 Python 像典型的脚本语言一样运行，但它被设计得更强大。Python 语言提供了许多高级语言中常见的功能，例如高级数据类型、结构和内置错误检查。以下各节描述了 Python 中找到的一些编程功能。

### Python 变量和数据结构

Python 有四种变量类型可供使用：

- scalars
- lists
- tuples
- dictionaries

让我们更仔细地看看每一种。

### 标量变量

标量变量是保存单个值的变量，与 Perl 中的情况类似。与 Perl 不同的是，Python 中数值和字符串类型是分离的，并且变量前不加任何额外符号。数值和字符串标量变量赋值的示例是

```
x = 5
pi = 3.14159
animal = "dog"
```

在 Python 脚本中使用变量也略有不同：

```
$ chmod +x test13.py
test = "Jessica"
pi = 3.14159
radius = 5
area = pi * radius ** 2
print test, "says the area should be," area
$ ./test13.py
Jessica says the area should be 78.53975
$
```

再次注意，Python 在变量名周围不使用任何符号。因此，当你想在 print 语句中显示变量值时，它必须位于定义的字符串文本之外。

### 列表变量

列表是对象（类似于 Perl 中的数组）的按数字索引的列表。它们可以由你选择的任何组合组成，例如标量数据、字典、元组，甚至其他列表。列表赋值的示例是

```
days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
```

Python 中列表的优点是存在几个很棒的内置函数，可以直接对列表中的值进行操作。这些函数在表 26-5 中显示。

**表 26-5：Python 列表函数**

| Function | Description |
|---|---|
| `append(x)` | Add an item to the end of an existing list. |
| `count(x)` | Return the number of times the specified item appears in the list. |
| `extend(L)` | Extends a list by appending all of the items in the specified list. |
| `index(x)` | Return the index value of the specified item in the list. |
| `insert(i, x)` | Insert an item into the list at a specified location. |
| `pop(i)` | Remove an item from the specified index in the list. If no index is specified, removes the last item in the list. |
| `remove(x)` | Remove an item from an existing list. |
| `reverse()` | Reverses the items in the list. |
| `sort()` | Sorts the items in the list. |

以下是使用 Python 处理列表的简单示例：

```
$ cat test14.py
#!/usr/bin/python
# listing lists in Python
days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
print "Before:", days
print "I have practice on", days[2]
days.sort()
print "After:", days
$ ./test14.py
Before: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
I have practice on Wednesday
After: ['Friday', 'Monday', 'Thursday', 'Tuesday', 'Wednesday']
$
```

sort() 函数对列表变量内部的数据进行排序。此外，注意你只需使用 print 语句即可快速显示列表内容！

### 元组变量

元组几乎与列表相同，只是它们是不可变的。这意味着与列表不同，你可以随意更改和修改列表，但不能更改元组。要创建元组，只需列出用逗号分隔的值：

```
days = "Monday", "Tuesday", "Wednesday", "Thursday", "Friday"
```

