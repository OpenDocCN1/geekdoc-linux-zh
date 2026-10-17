
```python
#!/usr/bin/env python2

# Linux User & Developer 呈现：巨型微游戏合集

from Tkinter import *

import rockpaperscissors
import hangman
import pokerdice

root = Tk()
root.title("Linux User & Developer 的巨型微游戏合集")

mainframe = Frame(root, height=200, width=500)
mainframe.pack_propagate(0)
mainframe.pack(padx=5, pady=5)

intro = Label(mainframe, text="""欢迎来到 Linux User & Developer 的巨型微游戏合集。
请选择以下其中一个游戏进行游玩：
""")
intro.pack(side=TOP)

rps_button = Button(mainframe, text="Rock, Paper, Scissors", command=rockpaperscissors.gui)
rps_button.pack()

hm_button = Button(mainframe, text="Hangman", command=hangman.start)
hm_button.pack()

pd_button = Button(mainframe, text="Poker Dice", command=pokerdice.start)
pd_button.pack()

exit_button = Button(mainframe, text="Quit", command=root.destroy)
exit_button.pack(side=BOTTOM)

root.mainloop()
```

## 主窗口

这段代码创建的主界面窗口相当基础，但包含了我们所需的功能。窗口的退出按钮将执行与“退出”按钮相同的工作，而“猜字谜游戏”和“扑克骰子”按钮则会在 Python 解释器中运行旧的脚本。

![](img/e016e192a91ffc1a9e474690a590742f_51_0.png)

-   **01 首行** 我们使用这一行来输入 Python 解释器的路径。这允许我们在终端内运行该程序，或者在 IDLE 等 Python 专用 IDE 之外运行。请注意，在此特定脚本中我们使用的是 Python 2。
-   **02 导入图形库** `Tkinter` 是我们使用的图形界面，虽然它是 Python 的标准库，但你仍然需要导入该模块才能使用它。我们使用了 `from [模块] import *` 方法，这样我们在使用其中的函数时就不需要在前面加上 `Tkinter`。
-   **03 导入游戏** 我们正在导入三个游戏的模块。我们在每个脚本的底部添加了一行，以便实现这一点。为了确保区分每个游戏中的函数，我们需要指定 `[模块].[函数]`，以便代码中没有错误。
-   **04 根窗口** 使用 `Tk()` 函数创建我们将放置所有内容的窗口。我们暂时决定称其为 `root`；不过，只要保持一致性，你可以将其命名为任何名称。我们还使用 `Tkinter` 的 `title` 命令和一个字符串为其命名。
-   **05 主框架** 第一行让我们将变量 `mainframe` 设置为界面中的一个 `Frame`（框架）。我们将其附加到 `root`（主窗口），并赋予其最小的高度和宽度（以像素为单位）。我们使用 `pack_propagate` 来创建窗口，并确保其大小符合我们的定义。然后我们使用 `pack` 来填充边框，使窗口内容不接触边缘。
-   **06 引言** 我们创建了一个位于主框架中的标签（label），并将其赋值给变量 `intro`。我们给它一段文本以介绍界面，使用三引号使其跨多行显示并更好地格式化。然后我们使用 `pack` 显示它，并告诉 `Tkinter` 将其放在界面的顶部。
-   **07 石头、剪刀、布** 我们使用 `Button` 函数为“石头、剪刀、布”游戏创建一个按钮。我们将主框架附加到它上面，使用 `text` 在按钮上显示标签，然后让它执行一个命令。在这种情况下，我们使用修改后的 `rockpapershotgun.py` 代码，该代码有一个 `gui` 函数，因此是 `rockpapershotgun.py`。然后我们使用 `pack` 将其放置在窗口中。

![](img/e016e192a91ffc1a9e474690a590742f_52_0.png)

```python
#!/usr/bin/env python2

# Linux User & Developer 呈现：石头、剪刀、布：电子游戏：模块

from Tkinter import *
from ttk import *
import random

def gui():
    rock = 1
    paper = 2
    scissors = 3
    names = { rock: "Rock", paper: "Paper", scissors: "Scissors" }
    rules = { rock: scissors, paper: rock, scissors: paper }
    def start():
        while game():
            pass
    def game():
        player = player_choice.get()
        computer = random.randint(1, 3)
        computer_choice.set(names[computer])
        result(player, computer)
```

![](img/e016e192a91ffc1a9e474690a590742f_52_1.png)

## 08 其他游戏

对于其他两个游戏，代码大部分相同；不过，我们在两者中都调用了 `start` 函数。在最终界面中，这将导致游戏像之前一样在 shell 或命令行中运行。

## 09 打破循环

退出按钮的工作方式与我们创建的其他按钮类似，但它使用的是 `command root.destroy()`。这结束了我们使用 `root.mainloop()` 创建的循环，该循环允许界面代码继续循环，从而让我们能够持续使用它。我们将退出按钮放置在窗口底部，使用 `side = BOTTOM`。

## 10 游戏代码

这段代码的开头没有多大变化，除了几个 `import` 变更外。用于在命令行中运行的代码仍然存在，经过一些修改，代码可以独立于主界面运行。我们删除了 `time` 模块，因为不再需要它，并不仅导入了 `Tkinter` 模块，还导入了 `ttk` 模块。`ttk` 模块允许我们将 GUI 排列在网格中，这样使用起来和理解起来会稍微简单一些。

## 11 游戏界面

我们对这个脚本所做的最大改变之一是将所有内容包含在一个函数中，即 `def gui`。界面代码需要放入函数中，否则它将被导入时就执行。虽然我们选择将代码的全部放在一个函数中，但你也可以尝试仅将图形界面代码放入其中一个。我们在这里保留了所有变量，以确保它们仍能正常工作。

## 12 游戏变量

变量保持不变，以便我们可以像原始代码中那样进行相同的比较。我们将它们放入函数中，这样它们就不会影响导入到主界面的其他代码——而且当我们仅调用此函数时，不需要使用 `global` 将它们引入。

我们的其他代码在按下按钮时，将以与之前相同的方式在 shell 或通过命令行运行。

## 13 `start` 函数

我们从 `start` 函数中删除了调用 `score` 函数的部分，因为现在由界面处理计分。不过，它仍然调用 `game` 函数，将其放入循环中，以便可以连续使用。此函数由界面调用来开始游戏，通过设置电脑的一步棋，然后将其与玩家的选择进行比较。

## 14 `game` 函数

`game` 函数经过了一些修改，以确保其与界面配合工作。首先，玩家变量是通过在我们创建的用于包含玩家选择的特殊变量上使用 `get()` 来获取的。我们对电脑做了类似的事情，使用 `set` 来更改我们面向界面的 `computer_choice` 变量中的值。我们仍然使用 `name` 变量来设置放入 `computer_choice` 中的文本。然后，我们像之前那样传递玩家和电脑变量。

## Python 基础要点
