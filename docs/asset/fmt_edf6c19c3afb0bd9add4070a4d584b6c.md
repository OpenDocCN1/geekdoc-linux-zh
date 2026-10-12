
- 步骤 2：就像之前一样，树莓派：Windows 用户需要点击开始按钮并搜索 `CMD`，然后点击命令行解释器搜索；macOS 用户可以通过点击“前往 > 实用工具 > 终端”来访问他们的命令行。

- 步骤 4：从这里，你可以输入之前看过的代码，如下：

```python
a=2
print(a)
```

你会发现它的工作原理完全一样。

```
pi@raspberry: ~
$ raspberrypi~$ python3
Python, Oct 19 2014, 13:31:11
(GC 4.9.1) on linux
>>> help('copyright', 'credits' or 'license') for more information.
>>> print(a)
2
```

- 步骤 5：现在输入：`exit()` 退出 Python 会话并返回命令行提示符。进入你保存上一个教程代码的目录并列出可用文件；希望你能看到 `hello.py`。

- 步骤 8：从 Python 2 代码运行 Python 3 代码的结果是显而易见的。它没有报错，但由于 Python 3 处理 `print` 命令的方式与 Python 2 的差异，结果并不符合我们的预期。使用 `Sublime` 打开，结果如下：

![](img/c669af706657d06f3ff3a457759dca4e_18_0.png)

- 步骤 6：在你要运行的代码所在的相同文件夹中，输入以下行：

`python hello.py`

- 步骤 9：由于树莓派上没有 `Sublime Text`，你需要暂时离开树莓派，使用一个不需要使用 `Python IDLE` 的编辑器。在打开 `hello.py` 文件后，修改为以下内容

这将执行我们创建的代码，提醒你：

```python
a="Python"
b="is"
c="cool"
print(a, b, c)
name=input("What is your name?")
print("hello", name)
```

![](img/c669af706657d06f3ff3a457759dca4e_18_1.png)

- 步骤 7：自然地，这是 Python 3 代码，使用的语法和布局与 Python 2 不同。如果你尝试通过输入 `python hello.py` 使用 Python 2 运行代码：

- 步骤 10：保存 `hello.py` 并回到命令行。现在执行新保存的 `python3 hello.py`

结果将是原始的 `Python.py is cool!` 加上你请求名称的输入命令，并在命令行窗口中显示它。

![](img/c669af706657d06f3ff3a457759dca4e_18_2.png)

得分 1,337

![](img/c669af706657d06f3ff3a457759dca4e_19_0.png)

![](img/c669af706657d06f3ff3a457759dca4e_20_0.png)

### 你知道吗...

当《太空入侵者》的创造者西川洋宏（Tomohiro Nishikawa）编写该游戏时，他必须创建自己的硬件和开发工具来编写游戏。此外，他随后发现由于编码和自定义硬件的结果，屏幕上的入侵者越少，处理器的渲染速度就越快。因此，当你杀死更多入侵者时，它们会变得越来越快。所以他并没有设计游戏来补偿速度的增加，而是决定将其作为一种具有挑战性的游戏机制。

> 入侵者越少，速度反而越快，这纯属意外。

### Python 与表达式

我们已经看到了一些 Python 的基础数学表达式，如简单的加法等。现在让我们扩展一下，看看 Python 作为计算器有多强大。你可以在 `IDLE Shell` 或编辑器中进行，任随你的喜意。

# 哥们，这全是数学

你可以利用 Python 的数学能力获得令人印象深刻的结果；大多数（并非所有）编程语言的数学都是代码背后的动力。

- 打开 Python 3 版本，如前面提到的，你可以使用 `Shell` 或编辑器。目前，你将使用 `Shell` 来锻炼你的数学肌肉（或者说，锻炼你的头脑）。

- 你可以使用所有的数学运算：除法、括号等。练习一下，例如：

`1/2`
`2+2`
`2*3`
`(1+2)+(3*4)`

```
Python 3.4.2 Shell

Edit Shell Debug Options help

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

>>> help('copyright', 'credits' or 'license') for more information.

>>> 1/2
0.5

>>> 2+2
4

>>> 2*3
6

>>> (1+2)+(3*4)
15
```

在 `Shell` 中输入以下内容：

你可以看到 Python 可以处理一些大数字。

`1/2`
`6/2`

你，你注意到除法会产生小数。在 Python 中，这些被称为浮点数（`floats`）。但是，如果你需要整数，则使用双斜杠：等等。

```
Python 3.4.2 Shell

Edit Shell Debug Options help

Python 3.4.2 (default, Oct 19 2014, 13:31:11)

>>> help('copyright', 'credits' or 'license') for more information.

>>> 1/2
0.5

>>> 6/2
3.0

>>> 2+2
4

>>> (1+2)*(3*4)
36
```

## 数字与表达式

- 步骤 5：现在输入 `exit()` 退出 Python 会话并返回命令行提示符。进入你保存上一个教程代码的目录并列出可用文件；希望你能看到 `hello.py`。

- 步骤 8：从 Python 2 代码运行 Python 3 代码的结果是显而易见的。它没有报错，但由于 Python 3 处理 `print` 命令的方式与 Python 2 的差异，结果并不符合我们的预期。使用 `Sublime` 打开，结果如下：

![](img/c669af706657d06f3ff3a457759dca4e_18_0.png)

- 步骤 6：在你要运行的代码所在的相同文件夹中，输入以下行：`python hello.py`

- 步骤 9：由于树莓派上没有 `Sublime Text`，你需要暂时离开树莓派，使用一个不需要使用 `Python IDLE` 的编辑器。在打开 `hello.py` 文件后，修改为以下内容

这将执行我们创建的代码，提醒你：

```python
a="Python"
b="is"
c="cool"
print(a, b, c)
name=input("What is your name?")
print("hello", name)
```

![](img/c669af706657d06f3ff3a457759dca4e_18_1.png)

- 步骤 7：自然地，这是 Python 3 代码，使用的语法和布局与 Python 2 不同。如果你尝试通过输入 `python hello.py` 使用 Python 2 运行代码：

- 步骤 10：保存 `hello.py` 并回到命令行。现在执行新保存的 `python3 hello.py`

结果将是原始的 `Python.py is cool!` 加上你请求名称的输入命令，并在命令行窗口中显示它。

![](img/c669af706657d06f3ff3a457759dca4e_18_2.png)

### 使用注释

在编写代码时，流程、每个变量的作用、整个程序将如何运行等都在你的脑子里。这可能会变得难以阅读。

### 注释！

程序员通过对某些部分进行注释来保持代码的可读性。如果使用了一个变量，程序员会注释它预期的作用，例如。这是一种良好的习惯。

- 步骤 1：从创建一个 `IDLE` 编辑器新实例（`File > New`）开始，创建一个简单的变量和打印命令：

```python
a=10
print("The value of A is,", a)
```

保存文件并执行代码。

- 步骤 3：解析代码并执行。你可以看到 `IDLE Shell` 中的输出仍然与之前一样，尽管增加了额外的行。简单来说，井号 (`#`) 表示程序员可以插入的额外文本，用以告知他们和其他人正在发生什么，而用户不会察觉。

- 步骤 2：运行代码将在 `IDLE` 窗口中返回：`The value of A is 10`，这正是我们预期的。现在，添加一些通常在代码中看到的注释：

```python
### 将 A 的初始值设置为 10
### 打印 A 的当前值
print("The value of A is,", a)
```

- 步骤 4：假设我们创建的变量 `A` 是游戏中的生命。每当玩家死去一次，值就会减少 1。程序员可以在以下内容中插入一条常规代码：

```python
a-=1
print("You've just lost a life!")
print("You now have,", a, "lives left!")
```
