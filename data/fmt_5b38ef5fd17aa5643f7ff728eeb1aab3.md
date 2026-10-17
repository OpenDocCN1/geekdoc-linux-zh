
Greetings to OccupyTheWeb from Hackers-Arise. The Best Place to Learn Hacking!

在 Python 中，每个变量都被视为一个类。类是创建对象的模板。更多信息请参阅第 189 页的“面向对象编程 (OOP)”。在接下来的脚本中，我尝试演示了几类变量。变量包含的内容不仅限于字符串。列表 17-2 显示了包含不同数据类型的变量。

```python
# /usr/bin/python3

HackersAriseStringVariable = "Hackers-Arise Is the Best Place to Learn Hacking"

HackersAriseIntegerVariable = 12

HackersAriseFloatingPointVariable = 3.1415

HackersAriseList = [1, 2, 3, 4, 5, 6]

HackersAriseDictionary = {'name': 'OccupyTheWeb', 'value': 27}

print(HackersAriseStringVariable)

print(HackersAriseIntegerVariable)

print(HackersAriseFloatingPointVariable)
```

列表 17-2: 与变量相关的数据结构

这创建了五个包含不同数据类型的变量：字符串（被视为文本）；整数（不带小数的数字类型，可用于数值运算）；浮点数（带小数的数字类型，也可用于数值运算）；列表（存储在一起的值列表）；以及字典（一个无序的数据集，每个值都与一个键配对，这意味着字典中的每个值都有一个唯一的标识键）。当你想要通过键名引用或更改值时，这非常有用。例如，假设你有一个配置如下的 `fruit_color` 字典：

```python
fruit_color = {'apple': 'red', 'grape': 'green', 'orange': 'orange'}
```

如果你在脚本稍后的部分想要获取葡萄的 `fruit_color`，只需通过其键调用即可：

```python
print(fruit_color['grape'])
```

你也可以更改特定键的值；例如，这里更改了苹果的颜色：

```python
fruit_color['apple'] = 'green'
```

我们将在本章稍后部分详细讨论列表和字典。在任何文本编辑器中创建此脚本 `secondscript.py`，然后赋予自己执行权限，如下：

```bash
kali$ chmod 755 secondscript.py
```

当我们运行此脚本时，它将输出内容：

```bash
kali$ ./secondscript.py
HackersArise Is the Best Place to Learn Hacking
12
3.1415
```

## 注释

与任何其他编程语言一样，Python 具有添加注释的功能。程序员经常使用注释来解释代码。Python 使用 `#` 符号标记单行注释的开始。如果你想写多行注释，可以使用三引号（`"""`）作为注释的开始和结束。在下面的脚本中，我为 `hackers-arise_greetings.py` 添加了短的多行注释。

```python
#!/bin/python3

"""
这是带有注释第一个 Python 脚本。注释用于帮助同事理解代码。在这种情况下，这个简单的脚本为用户创建一个问候。
"""

name="OccupyTheWeb"

print("Greetings to " + name + " from Hackers-Arise. The Best Place to Learn Hacking!")
```

当我们再次执行脚本时，与上次相比没有变化，如下所示：

```bash
kali$ ./hackers-arise_greetings.py
Greetings to OccupyTheWeb from Hackers-Arise. The Best Place to Learn Hacking!
```

它的运行方式与之前完全一样，但当我们以后回到代码时，我们就有关于该脚本的信息。

## 函数

Python 中的函数是执行特定操作的代码段。例如你之前使用的 `print()` 语句就是一个函数，它可以显示你传递给它的任何值。Python 有许多内置函数，你可以直接导入并使用。大多数函数在 Kali Linux 的默认 Python 安装中都是可用的，尽管许多可以通过下载的库可用。让我们看看你可以使用的数千个函数中的几个：

- `exit()`: 退出程序。
- `float()`: 将其参数作为浮点数返回。例如，`float(1)` 将返回 `1.0`。
- `help()`: 显示由其参数指定的对象的帮助信息。
- `int()`: 返回其参数的整数部分（截断小数）。
- `len()`: 返回列表或字典中元素的个数。
- `max()`: 从其参数（一个列表）中返回最大值。
- `open()`: 按照其参数指定的模式打开文件。
- `range()`: 返回位于其参数指定的两个值之间的整数列表。
- `sorted()`: 接收一个列表作为参数并返回按顺序排列的列表。
- `type()`: 返回其参数的类型（例如，`int`、`float`、`method`、`function`）。

你也可以创建自己的函数来执行自定义任务。由于语言内置了许多函数，在费力构建它之前，检查该函数是否存在总是值得的。有很多方法可以进行这种检查。一种方法是查看 `https://docs.python.org` 上的官方 Python 文。选择你正在使用的版本，然后选择“库引用”（Library Reference）。

### 列表

许多编程语言使用数组作为存储多个独立对象的方法。数组是一个值列表，可以通过引用在列表中的位置（称为索引，`index`），以各种方式对数组中的特定值进行检索、替换或处理。需要注意的是，Python 与许多其他编程环境一样，索引从 0 开始计数，因此列表中的第一个元素是索引 0，第二个是索引 1，第三个是索引 2，以此此类推。例如，如果我们想访问数组中的第三个值，可以通过 `array[2]` 实现。在 Python 中，数组有几种实现方式，但最常见的被称为列表（`list`）。

Python 中的列表是可迭代的，这意味着可以遍历整个列表中的所有元素（参见第 195 页的“循环”）。当我们使用列表查找特定值、逐个打印值或将值从一个列表移动到另一个列表时，这通常非常有用。

所以，假设我们需要显示来自列表 17-2 的 `HackerAriseList` 列表的第四个元素。我们可以通过调用列表名 `HackerAriseList` 并在方括号中加上我们要访问的元素索引来访问并打印该元素。

为了测试这一点，请在第二个 `pythonscript.py` 的末尾添加以下行，以打印 `HackerAriseList` 中索引为 3 的元素：

```
--snip--
print(HackersAriseStringVariable)
print(HackersAriseIntegerVariable)
print(HackersAriseFloatingPointVariable)
print(HackersAriseList[3])
```

当我们再次运行此脚本时，可以看到新的 `print` 语句在输出旁边打印了 4：

```
kali> ./pythonscript.py
Hacker-Arise Is the Best Place to Learn Hacking
12
3.1415
4
```

### 模块

模块只是保存在单独文件中的代码段，这样你就可以在程序中根据需要多次使用，而无需再次输入所有内容。如果你想使用模块或模块中的任何代码，则需要导入（`import`）它。如之前讨论的，使用标准模块和第三方模块是使 Python 对黑客变得如此强大的关键特性之一。如果我们想使用之前安装的 `nmap` 模块，我们会在脚本中添加以下行：

```
import nmap
```
