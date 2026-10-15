
`pd_button.pack(top=TOP)`

```python
exit_button = Button(mainframe, text = "退出", command = root.destroy)

exit_button.pack(side = BOTTOM)

root.mainloop()
```

首先，我们使用这行代码来进入 Python 解释器的路径。这有助于在 Python 特定的 IDE 内部或外部运行程序。请注意，对于这个特定的脚本并不需要它。

导入图形库 `Tkinter` 是使用它的极佳方法，它是一个简单的 Python 函数，你可以使用它。我们在开头使用了 `("模块")` 函数，这样我们就可以使用它的函数并将其添加到 `Tkinter` 中。

关于我们要制作的每个脚本。为了区分每个游戏中的不同函数，我们必须指定 `[模块,]函数]`，以确保代码不会出现错误。

像素为单位的最小高度和宽度。我们使用 `pack`、`propagate` 到窗口，然后确保它是我们定义的尺寸。然后我们将骰子堆在底部，允许窗口内容在屏幕上居中。

## 导入游戏

我们正在导入三个游戏的模块。我们在底部添加了该行

## 根图形

使用 `Tk` 函数创建了将要运行的窗口。我们还需要为 `root` 调用它；然而，你可以用你喜欢的任何调用它，只要保持一致即可。我们使用 `Tkinter` 的标题并开头来命名它

## 引言

我们创建了一个作为标签的变量，它位于主游戏中。我们给它文本来介绍界面，使用三引号来对其格式化。我们使用 `pack` 来显示它，并告诉 `Tk` 将其放在界面的顶部。

## 主框架

第一行将变量 `mainframe` 设置为界面中的一个框架（`frame`）。我们将其附加到 `root`（主窗口）上，并给了

# 剪刀石头石头布

我们为剪刀石头布游戏创建了一个按钮，使用 `Button` 函数，将其附加到主框架，并使用...给它一个标签

![](img/287427b4a3b7d7792fc1ca7834fce232_51_0.png)

```python
#!/usr/bin/env python2
```

```python
# Linux User & developer 呈现：剪刀石头石头布：视频游戏：模块
```

```python
from Tkinter import *
from ttk import *
import random
```

```python
def gui():
    rock = 1
    paper = 2
    scissors = 3
```

```python
names = { rock: "石头", paper: "布", scissors: "剪刀" }
rules = { rock: scissors, paper: rock, scissors: paper }
```

```python
def start():
    while game():
        pass

def game():
    player = player_choice.get()
    computer = random.randint(1, 3)
    computer_choice.set(names[computer])
    result(player, computer)
```

![](img/287427b4a3b7d7792fc1ca7834fce232_52_0.png)

出现在按钮上，然后再次运行，我们使用 `rockpapers.py`。它有 `gui` 函数。我们将其放在窗口中，经过几次修改，不再需要 `Tkinter` 模块，但在主界面中仍然

## 08 中断

## 13 Start 函数

我们删除了从 `start` 函数调用的部分，因为有界面处理分数。游戏结束了，将其放入循环以便持续使用。对于其他游戏，我们大部分时候都使用 `start` 函数。在最终界面中，这将导致游戏运行

## 11 界面

我们正在做的更改之一是让所有内容包含在一个函数中，`game()` 需要在 `import` 期间完成。所有的变量都保留在这里，以便它们能正常工作。游戏经过了一些修改以与界面工作。我们使用变量来设置电脑选择了什么。

## 09 循环

退出按钮的工作类似于其他变量的创建，但它使用了 `root.destroy()`。这在不清除内存的情况下结束了循环，允许我们继续界面。我们在窗口底部使用 `'exit = '`

## 12 游戏变量

我们保持不变，以便可以比较原始代码中的更改。我们把它们放入函数中，这样它们就不会影响其他代码 - 我们不需要全局化。

# 游戏代码

在 `start` 的代码中没有变化。运行的行仍然是

# Python 基础

```python
def result(player, computer):
    new_score = 0
    if player == computer:
        result_set.set("平局")
    else:
        if rules[player]:
            result_set.set("你胜利了。")
            new_score = player.get()
            new_score += 1
            player_score.set(new_score)
        else:
            result_set.set("电脑笑了你输了。")
            new_score = computer.get()
            new_score += 1
            computer_score.set(new_score)
```

```python
rps_window = Toplevel()
rps_window.title("剪刀石头石头布")
player_choice = IntVar()
computer_choice = StringVar()
result_set = StringVar()
player_score = IntVar()
computer_score = IntVar()
```

`GAME WINDOW` 在默认状态下，游戏窗口将选中石头且不会显示消息。一旦玩家做出移动，消息将在底部显示并打印电脑的结果。菜单上没有退出按钮，但点击窗口退出会将你带回主界面。`Result` 函数接收两个变量，就像之前在 `game` 函数中设置的那样。我们可以使用窗口分数来进行界面。这些不是纯整数，如果处理不当会导致错误。在脑中，我们创建了一个空的 `new_score` 变量，可以在返回之前清除屏幕。

我们设置的 `result` 在过程中不会更改窗口的消息。最后，我们为工作设置 `new_score` 变量。然后我们使用函数更新它，加1，并使用 `set` 方法将其放回 `player choice`。我们不能使用 `+ player_score` 变量因为它不是标准变量。

这就是我们能以不同方式更改变量的原因。对于 `Tkinter`，我们需要让界面知道变量的值。使用 `IntVar` 和 `StringVar` 可以满足我们需要。我们将 `player choice` 设置为 `1`，我们已经将其设置为默认值。这意味着游戏开始时会有默认选择，且不会引起错误。

逻辑与之前相同。我们首先简单检查输入是字符串还是 `player` 和 `computer` 变量的数值。变化的是，不再打印文本，而是使用 `Tkinter` 的 `result` 函数向我们发送“平局消息”。

## 平局

整体的 `Lose` 部分与之前相同，如果既不是平局也不是赢，就是输。我们使用的新版本代码用于更新玩家分数，还通过 `new_score` 改变电脑分数。

## 输

一个新窗口是主的一部分，我们在主界面中使用 `Tk` 创建了它。这个窗口是从它出来的，然后我们使用 `Toplevel`。这允许窗口独立运行并在主窗口之上。我们还得到了

## 新窗口

我们略有地创建了界面的框架。使用 `grid` 而不是使用 `pack` 方法，我们可以确保它的放置方式不会触碰窗口边缘。使用 `grid` 和 `command` 允许我们组成框架中的值。使用这样做了

## 游戏框架

行和列允许现在列包含在结构中

```python
rps_frame = Frame(rps_window, padding = '3 32 12', width = 300)
rps_frame.grid(column=0, row=0, sticky=(N,W,E,S))
rps_frame.rowconfigure(0, weight=1)
```

```python
Label(text='Player').grid(column=1, row=1, sticky=W)
Radiobutton(rps_frame, text='Scissors', variable=player_choice, value=1).grid(column=1, row=2, sticky=W)
```
