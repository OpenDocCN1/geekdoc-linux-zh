
# 串口通信与硬件连接

- 名称意味着：它会持续运行，直到按钮和开关被移除，或者从`Arduino`上断开电源的连接。
- 列表 1：`Arduino` 代码
  （代码块已保留，未翻译）

## 测试代码部分

- 名称意味着：它会持续运行，直到按钮和开关被移除，或者从`Arduino`上断开电源的连接。
- 列表 1：`Arduino` 代码
  （代码块已保留，未翻译）

> 注：由于您提供的“待翻译文本”部分似乎存在严重的文本损坏、字符重复或逻辑断裂，例如 `though that nothing is connected to power is removed from the Arduino` 这种不符合语法的句子，以上翻译严格遵循了“不漏掉任何行”的原则，但由于原文质量问题，中文可读性受限。

## 清理后的翻译

- 名称意味着：它会持续运行，直到按钮和开关被移除，或者从`Arduino`上断开电源的连接。
- 列表 1：`Arduino` 代码
  （代码块已保留）

- 通过 `Arduino` 的串口监视器，你可以直接向 `Arduino` 输入数据。

大多数硬件终端都使用 25 针连接器，因此你还需要一个 9 针转 25 针的适配器，你可以在亚马逊或当地的电子商店轻松找到它。

一旦连接好一切，请查看你终端的说明书，以找到如何设置波特率和其他连接参数，这些参数通常应该是 115,200 波特、8 个数据位、无奇偶校验和 1 个停止位。

图 4：在 `Wyse` 串口终端上运行的 `agetty` 命令。登录后，此物理终端将像终端窗口一样工作。

一旦你连接好线缆，你就需要一个软件来通过串口线为终端提供一个 shell（外壳）。你的 Linux 发行版中，应该已经有了一个名为 `agetty` 的程序。

# 查找你的串口

Linux 将其所有硬件（包括串口端口）报告为 `/dev` 下的文件。如果你的电脑在 CPU 后面有一个端口，那么它可能位于 `/dev/ttyS0`。如果你正在尝试与 `Arduino` 通信，它可能是 `/dev/ttyAMA0`，而如果你正在使用 USB 适配器，它可能是类似 `/dev/ttyUSB0` 的设备。你可以按照以下方法快速方便地找到你的端口：

man 页面显示了命令格式：`agetty [options] port [baud_rate...]`

## 操作步骤

1. 确保你的 USB 串口或 `Arduino` 已经拔掉。
2. 在终端中，输入 `ls -1 /dev/tty* > noUSB.txt`。
3. 连接你的 USB 串口，并给它大约一秒的时间进行注册。查看“查找你的串口”框。
4. 在终端中，输入 `ls -1 /dev/tty* > USB.txt` 来确定你的端口名称；然后，输入类似：`agetty ttyUSB0 115200 > /dev/ttyUSB0`。
5. 最后，输入 `diff noUSB.txt USB.txt`。你会看到类似的内容：

如果一切顺利，你的硬接线终端上会出现一个登录提示。在上面的步骤 2 和 4 中，你正在使用 `ls` 来获取在 `/dev` 中找到的 tty 设备列表。`-1` 要求每行输出一个条目而不是按列输出。`>noUSB.txt` 将输出重定向到文本文件。连接 USB 设备后，步骤 4 产生了一个包含刚刚连接的设备的新列表，而步骤 5 的 `diff` 命令比较了这两个输出文件。一旦你登录，系统的默认 shell 就会出现。你也可以配置 `agetty` 在有连接时运行自定义处理程序（例如，你编写的任何服务）。

输出的第一行报告了，在原始文件 (`noUSB.txt`) 的第 98 行之后，第二个文件 (`USB.txt`) 额外有一 (a) 第 99 行。下一行输出显示在尖括号行之后连接已关闭到另一个程序。在这种情况下，那是当设备连接以启动拨号上网连接时出现的 USB 串口名称，或任何类似的内容。

![Diagram](img/d1478ca893bfbd12a417e8f50e507b16_373_0.png)

# 串口通信制作空间 (MAKERSPACE)

`__init__` 函数是类中的一个特殊函数。每当类被实例化（首次创建）时，它就会被自动调用。类似于稀响团，一个类可以代表每个音乐家但独立运行。如果在 `Arduino` 代码中设置一个程序，它让你让类准备好执行它需要做的任何工作。在这里，我用它来设置 `curses`。

图 5：在终端中运行的大字打印时钟。在这里，控制台代表一个 `curses` 窗口。我不需要在桌面运行它之间对代码进行任何更改。

# Curses 库

`__init__` 函数是类中的一个特殊函数。每当类被实例化（首次创建）时，它就会被自动调用。类似于稀响团，一个类可以代表每个音乐家但独立运行。如果在 `Arduino` 代码中设置一个程序，它让你让类准备好执行它需要做的任何工作。在这里，我用它来设置 `curses`。

# 大字打印 (Big Print)

在串口终端中一种流行的做法是显示高行的大字体。`bigPrint.py` 脚本显示了一个时钟（图 5），并且是 `curses` 库的一个很好的示例。在 Python 程序列表 4 中，`import` 引入了 `curses`、`time`、`os`、`string` 和 `datetime` 库。注意第 5 行有点不同：它没有导入整个库，而是导入了 `datetime` 模块。默认情况下，Python 会导入整个库，因此 `import` 允许你只引入你需要的部分。在编程中，类是代表更大单元的变量和函数。你可以创建类的实例。

列表 4：`clock.py`

```python
import curses
import time
import os
import string
from datetime import datetime

class console:

    def __init__(self):
        self.screen = curses.initscr()
        curses.noecho()
        curses.break()
        self.screen.nodelay(True)
        curses.keypad(True)
        self.digits = dict()
        self.digits['0'] = """
        self.digits['1'] = """
        self.digits['2'] = """
        self.digits['3'] = """
        self.digits['4'] = """
        self.digits['5'] = """
        self.digits['6'] = """
```
