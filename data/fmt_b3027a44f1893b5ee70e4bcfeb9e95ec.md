
Python `Shell` 的作用非常像计算器，因为代码基本上是与系统的一系列数学交互。整数（无限数字序列）可以很容易地进行加、减、乘等。

```
File Edit View Search Terminal Help
david@david-mint: $ python --version
Python 3.4.2 (Default, Oct 19 2014, 13:31:11)
on Linux
>>> 'copyright', 'credits' or 'license' for more information.
>>> 4
4 >>>
```

```
File Edit View Search Terminal Help
david@david-mint: $ python --version
Python 3.4.2 (Default, Oct 19 2014, 13:31:11)
on Linux
>>> 'copyright', 'credits' or 'license' for more information.
>>> 4
4 >>>
>>> 8+6
14 >>>
>>> 2345*6445252
15089114440 >>>
>>> 977862442343-12343
>>> 9778624423*43034
50647282358
>>>
```

## 首次开始

第 5 步虽然很有趣，但并不是特别有趣。相反，尝试这个：

```python
print("Hello everyone!")
```

像你在之前的步骤中那样，将其输入 `IDE`。

第 8 步 `Python` `IDE` 是一个可配置的环境。如果你不喜欢颜色的表示方式，可以通过 `Options > IDE` 并点击 `Highlighting`（高亮）来更改任何。然而，我们不建议这样做，因为你看到的内容将与截图不一致。

```
Python 3.4.2
---
$ git clone shell github jenkins web pull
Python 3.4.2 (default, Oct 19 2014, 10:31:11)
(GCC 4.9.0) on Linux
[GCC 4.9.0]
>>> print("Hello world!\n")
>>> print("Credits" or "license" for example:
Hello world!
>>>
>>> 23453-645522
>>> 8878644522-12433
>>> 8878644522-25934
>>> 5064272358
>>> print("Hello everyone!")
>>> 
```

第 6 步这看起来像那么样了，因为你已经产生了了自己的段代码。`print` 命令是非常自言易懂的。有趣的是，`Python` 3 要求使用括号和引号来向屏幕输出内容，在这种情况下，我们看到了 `Hello everyone` 的结果：

```python
>>> print("Hello everyone!")
Hello everyone!
>>>
```

第 9 步就像大多数强大的应用程序一样，无论使用哪种操作系统，都有许多快捷键可用。我们没有空间列出所有键，但在 `Options > IDE` 和 `Keys` 选项卡中，你可以看到当前绑定的列表。

第 7 步你注意到了 `Python` `IDE` 内部的颜色编码。颜色代表 `Python` 代码的不同元素。它们是：

| 黑色 - 数据和变量 | 蓝色 - 用户函数 |
| :--- | :--- |
| 绿色 - 字符串 | 红色 - 注释 |
| 紫色 | 淡红色 - 错误消息 |
| 橙色 | |

第 10 步 `Python` `IDE` 是一个强大的接口，它实际上是用所有的所有的 `Shell` 编写的，我们建议你花几分钟查看 `www.python.org/library/idle.html`，它详细介绍了该 `IDE` 的许多功能。

| IDLE 颜色编码 | 颜色 | 用于 | 示例 |
| :--- | :--- | :--- | :--- |
| 黑色 | 数据与变量 | 23.4 area | |
| 绿色 | 字符串 | "Hello World" | |
| 紫色 | 函数 | isinstance() | |
| 橙色 | | for | |
| 蓝色 | 用户 | get_area() | |
| 深红色 | 注释 | #number | |
| 淡红色 | 错误消息 | SyntaxError: | |

![](img/c669af706657d06f3ff3a457759dca4e_12_0.png)

![](img/c669af706657d06f3ff3a457759dca4e_12_1.png)

![](img/c669af706657d06f3ff3a457759dca4e_12_2.png)

## 你的第一段代码

基本上，你已经通过上一个教程中的 `Hello everyone!` 函数编写了你的第一段代码。然而，让我们扩展一下，看看输入你的代码并尝试一些其他的 `Python` 示例。

## 玩转 Python

对于大多数语言，无论是计算机语言还是人类语言，关键在于在正确的情况下记住并应用正确的词汇。你并不是天生就知道这些的，所以你需要学习它们。

- **第 1 步** 如果你选择了 `Python` 3，请在你喜欢的任何操作系统中重新打开它。在 `Shell` 中，输入以下内容：

```python
print("Hello")
```

![](img/c669af706657d06f3ff3a457759dca4e_13_0.png)

- **第 2 步** 正如预期的，单词 `Hello` 以文本形式出现在 `Shell` 中，表示来自字符串的输出。这非常直观，不需要太解释。现在尝试：

```python
print("2+2")
```

![](img/c669af706657d06f3ff3a457759dca4e_13_1.png)

### 第 5 步

你在这里所的操作为字母 `a` 和 `b` 分配值：2。这些是变量，`Python` 可以调用它们进行输出、加法、减法等，只要它们的数字保持不变。尝试这个：

```python
### print(b)
```

```
Python 3.4.2 Shell

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

>>> type="credits" or "license" for more information.

>>> name="David"

>>> print(name)

David

>>> a=2

>>> b=4

>>> print(a+b)

6

>>> print(a-b)

-2

>>> print(a*b)

8
```

### 第 8 步

现在我们添加一个姓氏：

```python
surname="Hayward"
print(surname)
```

你有两个变量包含一个名字和姓姓氏，你可以独立地打印它们。

```
Python 3.4.2 Shell

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

>>> type="credits" or "license" for more information.

>>> name="David"

>>> print(name)

David

>>> surname="Hayward"

>>> print(surname)

Hayward
```

### 第 6 步

最后一步的输出清楚地显示了 `a` 和 `b` 的单独值，因为你要求分开打印。如果你想将它们相，可以使用：

```python
### print(a+b)
```

这段代码获取 `a` 和 `b` 的值，将它们相加并输出结果。

```
Python 3.4.2 Shell

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

>>> type="credits" or "license" for more information.

>>> name="David"

>>> print(name)

David

>>> a=2

>>> b=4

>>> print(a+b)

6
```

### 第 9 步

如果我们在之前使用相同的程序，使用 `+`，名字将不会在 `Shell` 中正确显示。你尝试：

```python
### print(name-surname)
```

你需要在之间留一个空格，将它们定义为两个独立的值，而不是在数学上进行操作。

```
Python 3.4.2 Shell

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

>>> type="credits" or "license" for more information.

>>> name="David"

>>> print(name)

David

>>> surname="Hayward"

>>> print(surname)

Hayward
```
