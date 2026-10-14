
`sudo apt-get install build-essential checkinstall`

`sudo apt-get install libreadline-dev libsqlite3-dev`

`ncursesw5-dev libbz2-dev tk-dev`

`libdbm-dev libdb6-dev libbz2`

### 第 8 步 在 Python 文件夹中
`./configure`
`sudo make altinstall`

这取决于你电脑的速度，可能需要一段时间。完成后，使用 `python3.7 --version` 检查安装的版本。现在你已经在与 Python 3.x 和 Python 2 并存的情况下安装了 Python 3.7。

![](img/f8aca09bc266ba3d122c77a820ff023b_90_0.png)

如果你想要一个包含所有稳定优化的（LTO 等）的构建版本，请运行 `--enable-optimizations`

### 第 6 步 打开你的 Linux 浏览器并访问 Python 页面：`www.python.org/downloads`。点击 Python Source 下方的下载按钮。这会打开一个下载窗口；选择一个位置并开始下载。

### 第 9 步 对于 GUI，你需要在终端中输入命令：
`sudo apt-get install idle3`

可以使用命令 `idle3` 启动 IDE。注意 IDE 运行的版本与你安装的版本不同。

![](img/f8aca09bc266ba3d122c77a820ff023b_90_1.png)

### 第 10 步 在终端中，使用 `tar -xvf python-3.Y.Y.tar.xz` 进入已下载的源码目录。将文件名替换为你下载的版本。现在使用 `cd Python-3.Y.Y/` 进入解压后的文件夹。

你还需要 PIP（Pip 包管理器）来帮助你安装更多模块和扩展。
`pip3 install --upgrade pip`

完成后，可以通过系统“编程”功能可以使用终端和 Python 3.x。

![](img/f8aca09bc266ba3d122c77a820ff023b_90_2.png)

## 首次启动 Python

我们将使用树莓派作为我们的 Python 3 硬件平台。最新版本的 Raspian 预装了 Python 3，具体版本为 3.4.2，所以只要你使用的是版本 3 Shell，我们所有的代码都可以运行。

## 启动 Python

我们不会详细介绍如何让树莓派运行起来，这个主题有大量的材料可以参考。然而，一旦你准备好了，就启动你的树莓派并准备编写代码。

- 第 1 步 在加载了树莓派桌面后，点击菜单中的 Programming（编程）> Python 3 (IDLE)。这会打开 Python 3 Shell。Windows 和 Mac 用户可以在 Windows 开始菜单或 Finder 访达中找到 Python 3 IDLE Shell。

- 第 3 步 例如，在 Shell 中输入：`Z+Z`。按下回车键后，下一行显示答案：4。基本上，Python 已经处理了“代码”并产生了相关的输出。

![](img/f8aca09bc266ba3d122c77a820ff023b_91_0.png)

- 第 2 步 Shell 是你输入代码并查看编程到 Python 中的代码响应和输出的地方。这是一种沙箱，你可以在这里尝试简单的代码和过程。

- 第 4 步 Shell 的作用非常像计算器，因为代码本质上是与整数的一系列数学交互。整数是无限数字序列可以很容易地进行加、减、乘等。

```
Python 3.4.2 (Default, Oct 19 2014, 13:21:11)

>>> on Linux

>>> 'copyright', 'credits' or 'license' for more information.

>>> 4

4
```

```
Python 3.4.2 (Default, Oct 19 2014, 13:21:11)

>>> on Linux

>>> 'copyright', 'credits' or 'license' for more information.

>>> 4

4

>>> 23539+64552

669061

>>> 465028*12345-12345

5740233332

>>> 9778629968*48234

47147329999512

>>>
```

## 首次启动 Python

第 5 步 虽然它很有趣，但并不特别令人。相反，尝试这个：

```python
print("Hello!")
```

像之前的步骤那样进入 IDLE。

第 8 步 Python IDLE 是一个舒适的环境，如果你不喜欢它的显示方式，可以通过 Options > Configure 并点击 Highlighting 标签进行更改。然而，我们不建议这样做，因为你看到的和截图不一样。

![](img/f8aca09bc266ba3d122c77a820ff023b_92_0.png)

第 6 步 这更像一点点，因为你刚刚产生了第一段代码。`print` 命令非常浅言易懂，它负责打印内容。由于我们要输出到屏幕，所以看到了 'Hello' 的情况：

```python
>>> print("Hello!")
Hello!
```

第 9 步 就像大多数情况一样，无论什么种操作系统，都有许多快捷键。我们这里没有留出空间，但使用 Options > Configure IDLE 标签，你可以看到当前的命令。

![](img/f8aca09bc266ba3d122c77a820ff023b_92_1.png)

第 7 步 你可能注意了 IDLE 内的编码。颜色代表不同的 Python 代码元素：

字体 黑色 数据
- 绿色 字符串
- 紫色 函数
- 橙色 命令

第 10 步 Python IDLE 是一个强大的界面，如果你想知道更多关于 Shell 的信息，建议花几分钟访问 `www.python.org/library/idle.html`，介绍了 IDLE 的许多功能。

## IDLE 编码

| 颜色 | 数据与变量 | 示例 |
| :--- | :--- | :--- |
| 黑色 | | 4 |
| 绿色 | | 'World' |
| 紫色 | | get_area() |
| 橙色 | | variable |
| 蓝色 | | |
| 浅红色 | | SyntaxError: |

![](img/f8aca09bc266ba3d122c77a820ff023b_92_2.png)

## 你的第一段代码

基本上，你已经使用之前的教程中的 ‘Hello!’ 函数写了你的第一段代码。然而，让我们扩展一下，输入你的代码并尝试其他示例。

## 玩转 Python

对于大多数语言来说，无论是计算机还是人类，关键都在于记忆并在正确的情况下使用正确的词汇。你不认识这些词汇，所以你需要学习它们。

第 1 步 如果你选择了 Python 3，请在你偏好的操作系统中重新打开它。在 Shell 中，输入以下：

```python
>>> print("Hello")
```

![](img/f8aca09bc266ba3d122c77a820ff023b_93_0.png)

第 2 步 正如预期，单词 Hello 出现在 Shell 中并呈蓝色文本，表示字符串的输出。它非常直观，不需要太多解释。现在尝试：

```python
>>> print("2+2")
```

![](img/f8aca09bc266ba3d122c77a820ff023b_93_2.png)

第 3 步 你可以看到输出不是数字 4，而是你要求打印到 Shell 的 2+2。问号定义了输出到引号中的内容：

```python
>>> print(2+2)
```

![](img/f8aca09bc266ba3d122c77a820ff023b_93_1.png)

第 4 步 你可以继续这样做，在 Shell 中打印 2+2、4+4 等。一种简单的方法是使用变量，我们稍后会深入介绍。现在：

```python
x=2
b=2
```

## 你的第一段代码

第 5 步 你在这里执行的操作为字母 a 和 b 赋值了值：2 和 2。它们现在是变量，只要它们的数字保持不变，就可以调用 Python 进行输出、加法、减法等。尝试这个：

第 8 步 现在添加一个姓氏：`surname="Hayward"`
`print(surname)`

`print(b)`

```python
Python 3.4.2 (Default, Oct 19 2014, 13:21:11)

>>> on Linux

>>> 'copyright', 'credits' or 'license' for more information.

>>> type(name)
'str'

>>> name="Hayward"

>>> print(name)
'Hayward'

>>> a=2
```
