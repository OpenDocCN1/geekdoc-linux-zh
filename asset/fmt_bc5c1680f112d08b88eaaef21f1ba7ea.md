
Tkinter（以及从 Python 3.1 开始的 `ttk`）包含在所有标准 Python 发行版中。重要的是，你必须使用支持 Tk 8.5 或更高版本以及 `ttk` 的 Python 版本。我们建议安装来自 ActiveState 的 "ActivePython" 发行版，它包含你所需要的一切。

在你的网络浏览器中，访问 `www.activestate.com`，并跟随链接下载适用于 Windows 的 ActivePython 社区版。确保你下载的是 3.1 或更新版本，而不是 2.x 版本。

运行安装程序，并跟随提示操作。最终你将在例如 `C:\python32` 处获得一个全新的 ActivePython 安装。然后，你应该能够从 Windows 命令提示符，或开始菜单的"运行..."命令，通过以下方式运行 Python shell：

```
% C:\python32\python
```

这应该会给出 Python 命令提示符。从提示符处，输入这两个命令：

```
>>> import tkinter
>>> tkinter._test()
```

这应该会弹出一个小编辑框；窗口顶部的第一行应该显示"This is Tcl/Tk version 8.5"；确保它不是 8.4！

你还可以通过以下方式获取正在使用的 Tcl/Tk 的确切版本：

```
>>> tkinter.Tcl().eval('info patchlevel')
```

它应该返回类似 '8.5.9' 的内容。

*使用 ActivePython 3.2.1.2 在 Windows 7 上验证安装。*

## 在 Linux 上安装 Tk

Tkinter（以及从 Python 3.1 开始的 `ttk`）包含在所有标准 Python 发行版中。重要的是，你必须使用支持 Tk 8.5 或更高版本以及 `ttk` 的 Python 版本。我们建议安装来自 ActiveState 的 "ActivePython" 发行版，它包含你所需要的一切。

在你的网络浏览器中，访问 `www.activestate.com`，并跟随链接下载适用于 Linux 的 ActivePython 社区版。确保你下载的是 3.1 或更新版本。

解压它，运行安装程序（`/install.sh`），并跟随提示操作。最终你将在例如 `/opt/ActivePython-3.2` 处获得一个全新的 ActivePython 安装。然后，你应该能够从终端窗口通过以下方式运行 Python shell：

```
% /opt/ActivePython-3.2/bin/python3.2
```

这应该会给出 Python 命令提示符。从提示符处，输入这两个命令：

```
>>> import tkinter
>>> tkinter._test()
```

这应该会弹出一个小编辑框；窗口顶部的第一行应该显示"This is Tcl/Tk version 8.5"；确保它不是 8.4！

你还可以通过以下方式获取正在使用的 Tcl/Tk 的确切版本：

```
>>> tkinter.Tcl().eval('info patchlevel')
```

它应该返回类似 '8.5.9' 的内容。

*使用 ActivePython 3.2.1.2 在 Ubuntu 11.04 上验证安装。*

## 第一个必备程序

为了确保一切确实正常工作，让我们尝试在 Tk 中运行一个"Hello World"程序。虽然对于如此短的程序，你可以直接在解释器中输入，但最好使用你最喜欢的文本编辑器将其放入文件中。

```python
from tkinter import *
from tkinter import ttk
root = Tk()
ttk.Button(root, text="Hello World").grid()
root.mainloop()
```

将此保存为名为 `hello.py` 的文件。从命令提示符处，输入：

```
% python hello.py
```

找不到 `hello.py`？你可能在错误的目录中寻找。尝试提供 `hello.py` 的完整路径。

![](img/94378c1b05607c1dc5649c738af95c74_10_0.png)

我们的第一个程序。在 IPO 之前还有一些工作要做。

## 第一个（实际）示例

解决了这个问题之后，让我们尝试一个稍有用处的示例，这将让你初步感受 Tk 程序背后的代码是什么样子的。

### 设计

我们将使用的示例是一个简单的 GUI 工具，它将把英尺数转换为等效的米数。如果我们画个草图，它可能看起来像这样：

![](img/94378c1b05607c1dc5649c738af95c74_10_1.png)

看起来我们有一个简短的文本输入小部件，让我们输入英尺数，以及一个"计算"按钮，该按钮将从输入框中获取值，执行计算，然后将结果米数放在屏幕上输入框下方。我们还有三个静态标签（“英尺”、“等价于”和“米”），帮助用户了解如何使用界面。

就布局而言，事物似乎自然地分为三列和三行：

![](img/94378c1b05607c1dc5649c738af95c74_11_0.png)

我们的用户界面布局，遵循 3 x 3 网格。

### 代码

下面是创建此程序的 Python 代码。

```python
from tkinter import *
from tkinter import ttk

def calculate(*args):
    try:
        value = float(feet.get())
        meters.set((0.3048 * value * 10000.0 + 0.5)/10000.0)
    except ValueError:
        pass

root = Tk()
root.title("Feet to Meters")

mainframe = ttk.Frame(root, padding="3 3 12 12")
mainframe.grid(column=0, row=0, sticky=(N, W, E, S))
mainframe.columnconfigure(0, weight=1)
mainframe.rowconfigure(0, weight=1)

feet = StringVar()
meters = StringVar()

feet_entry = ttk.Entry(mainframe, width=7, textvariable=feet)
feet_entry.grid(column=2, row=1, sticky=(W, E))

ttk.Label(mainframe, textvariable=meters).grid(column=2, row=2, sticky=(W, E))
ttk.Button(mainframe, text="Calculate", command=calculate).grid(column=3, row=3, sticky=W)

ttk.Label(mainframe, text="feet").grid(column=3, row=1, sticky=W)
ttk.Label(mainframe, text="is equivalent to").grid(column=1, row=2, sticky=E)
ttk.Label(mainframe, text="meters").grid(column=3, row=2, sticky=W)

for child in mainframe.winfo_children(): child.grid_configure(padx=5, pady=5)

feet_entry.focus()
root.bind('<Return>', calculate)

root.mainloop()
```

生成的用户界面如下：

![](img/94378c1b05607c1dc5649c738af95c74_12_0.png)

完成的英尺转米用户界面截图（在 Mac OS X、Windows 和 Linux 上）。

# 关于代码风格的说明

本教程中包含的每种语言都有多种可供选择的代码风格和约定，这些约定有助于确定变量和函数命名、过程式、函数式或面向对象风格等规范。

由于本教程的重点是 Tk，因此本教程将尽可能保持简单，通常使用非常直接的代码风格，而不是将大多数代码封装在过程、模块、对象、类等中。在尽可能多的情况下，你还会看到在每个示例中，跨语言使用相同的对象、变量等名称。

# 逐步详解

让我们更仔细地查看那段代码，逐段分析。目前，我们要做的只是获得对创建 Tk 用户界面所需做的事情类型的初步理解，以及大致了解它们的样子。我们稍后会深入细节。

```python
from tkinter import *
from tkinter import ttk
```
