
# Python 书籍·第1卷：Python 编码终极指南

![](img/3b256f430f51c98f1315671f6e4eec19_0_0.png)

## Welcome to

The Python Book

Python is an incredibly versatile, expansive language which, due to its similarity to everyday language, is surprisingly easy to learn even for inexperienced programmers. It has seen a huge increase in popularity since the release and rise of the Raspberry Pi, for which Python is the officially recognised programming language. In The Python Book, you'll find plenty of creative projects to help you get to grips with the combination of your Raspberry Pi and Python's powerful functionality, but there are also plenty of tutorials that focus on Python's effectiveness away from the Raspberry Pi. You'll learn all about how to code with Python from the very beginning with our comprehensive masterclass, then go on to complete tutorials to consolidate your skills and become fluent in the language while also improving your computing experience. You'll learn how to make Python work for you with tutorials on coding with `Django`, `Flask`, `Pygame` and even more useful third-party applications and frameworks. Get ready to become a true Python expert with the wealth of information contained within these pages.

![](img/3b256f430f51c98f1315671f6e4eec19_2_0.png)

### Part of the Linux User & Developer bookazine series

![](img/3b256f430f51c98f1315671f6e4eec19_4_0.png)

```
Python 2.7.6 (default, Mar 22 2014, 22:59:51)
[GCC 4.8.2] on linux2
type "help", "copyright", "credits" or "license" for more information
>>> import scipy
>>> mysin = "scipy.sin(45.6)"
>>> eval(mysin)
6.98899006714502186
>>>
```

![](img/3b256f430f51c98f1315671f6e4eec19_5_0.png)
![](img/3b256f430f51c98f1315671f6e4eec19_5_1.png)
![](img/3b256f430f51c98f1315671f6e4eec19_5_2.png)
![](img/3b256f430f51c98f1315671f6e4eec19_5_3.png)

### 50 个 Python 技巧

#### Web 开发

- **134 使用 Python 开发** — 为什么 Python 非常适合 Web
- **140 搭建自己的博客** — 开始开发你的博客
- **144 为博客提供内容** — 向你的网站添加内容
- **148 增强你的博客** — 用插件完善你的博客

#### 在 Pi 上使用 Python

- **154 在 Raspberry Pi 上用 Python 编程** — 学习如何为 Pi 优化
- **158 编程 Minecraft Pi** — 在 Pi 上玩 Minecraft 游戏
- **162 构建 LED 矩阵** — 使用 Pi 控制灯光序列
- **166 Raspberry Pi 汽车电脑** — 用 Raspberry Pi 抵达目的地

> “Python 非常庞大，但你很快就会成为专家”

### 开始学习 Python

一直想尝试编程？别再找借口了，因为 Python 是入门的完美方式！

Python 是一种对初学者和专家都非常好的编程语言。它以代码可读性为设计核心，使其成为仍在熟悉各种编程概念的初学者的绝佳选择。

该语言很受欢迎，并且有大量可用的库，让程序员可以用相对较少的代码完成很多工作。

你可以用 Python 制作各种各样的应用程序：你可以使用 `Pygame` 框架编写简单的 2D 游戏，可以使用 `GTK` 库创建窗口化应用程序，或者尝试更雄心勃勃的东西，比如使用 Python 的蓝牙和输入库创建一个应用来捕获 USB 键盘的输入并将输入事件中继到 Android 手机。

在本教程中我们将使用 `Python 2.x`，因为这很可能是安装在你的 Linux 发行版上的版本。

在接下来的教程中，你将学习如何使用 Python 编程创建流行的游戏。我们还将向你展示如何为这些游戏添加音效和 AI。

### Hello World

让我们开始吧，没有什么比程序员的好朋友“Hello World”应用程序更合适的了！首先打开一个终端。它的当前工作目录将是你的主目录。最好为本教程中我们将创建的文件创建一个目录，而不是将它们散放在主目录中。你可以使用命令 `mkdir Python` 创建一个名为 `Python` 的目录。然后你需要使用命令 `cd Python` 进入该目录。

下一步是使用命令 `touch` 后跟文件名创建一个空文件。我们的专家使用了命令 `touch hello_world.py`。设置文件的最后一步也是最重要的一步是使其可执行。这使我们能够在 `hello_world.py` 文件中运行代码。我们使用命令 `chmod +x hello_world.py` 来实现这一点。现在文件已经设置好，我们可以继续在 `nano` 或你选择的任何文本编辑器中打开它。`Gedit` 是一款支持语法高亮的优秀编辑器，应该在任何发行版上都可用。如果你还没有它，可以使用你的包管理器安装它。

```
[liam@liam-laptop ~]$ mkdir Python
[liam@liam-laptop ~]$ cd Python/
[liam@liam-laptop Python]$ touch hello_world.py
[liam@liam-laptop Python]$ chmod +x hello_world.py
[liam@liam-laptop Python]$ nano hello_world.py
```

我们的 Hello World 程序非常简单，只需要两行。第一行以 'shebang' 开头（符号 `#!` – 也称为 hashbang），后跟 Python 解释器的路径。程序加载器使用这一行来确定其余行需要用什么来解释。如果你正在 IDE 如 `IDLE` 中运行，则不一定需要这样做。

实际被 Python 解释器读取的代码只有一行。我们通过在调用 `print` 函数后立即将其放在括号中，将值 `Hello World` 传递给 `print` 函数。`Hello World` 用引号括起来以表示它是一个字面值，不应被解释为源代码。正如预期的那样，Python 中的 `print` 函数会打印从控制台传递给它的任何值。

你可以在 `nano` 中使用快捷键 `Ctrl+O` 然后按 `Enter` 保存刚刚对文件所做的更改。使用 `Ctrl+X` 退出 `nano`。

```
#!/usr/bin/env python2
print("Hello World")
```

你可以通过在其文件名前加上 `./` 来运行 Hello World 程序 — 在这种情况下你需要输入：`./hello_world.py`

```
[liam@liam-laptop Python]$ ./hello_world.py
Hello World
```

### TIP

如果你使用的是图形编辑器，如 `gedit`，那么你只需要做最后一步使文件可执行。你只需要将文件标记为可执行一次即可。文件一旦可执行，你就可以自由编辑它。

### 变量和数据类型
