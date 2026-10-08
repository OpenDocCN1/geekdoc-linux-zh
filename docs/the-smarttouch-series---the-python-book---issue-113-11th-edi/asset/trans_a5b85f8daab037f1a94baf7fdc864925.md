
## 文本编辑器

除了我们推荐的集成开发环境（IDE），你还需要尝试使用文本编辑器进行编码。其中一些文本编辑器更加轻量级，并且能像 IDE 那样格式化代码，例如通过颜色区分函数和字符串等。我们推荐的一些编辑器包括：经典编辑器（GNOME 桌面环境中流行的文本编辑器）、Geany（内置了一些类似 IDE 的功能）、TEA（一个多功能文本编辑器和项目管理工具）以及 Jedit（一个位于命令行中、资源占用极低的文本编辑器）。这些编辑器同样支持多种编程语言，因此你可以先用 Python 熟悉它们，然后再切换其他语言。

![](img/e016e192a91ffc1a9e474690a590742f_48_0.png)

## 课后作业

目前该版本游戏尚未设置评分机制。尝试添加一个计算机玩家，或者创建一套规则，要求手牌达到特定等级或更高。你甚至可以将其做成双人对战模式。

因此，我们嵌套了一个 `if` 语句。同样，我们针对对子进行处理，这可能是一组对子或两组对子。如果以上情况都不满足，那么通过排除法，它只能是高点数。我们为每种结果分配一个文本字符串，以便将其发送回 `throw` 函数，从而打印出来。

## 22 再玩一次

和之前一样，我们通过文本提示玩家提供原始输入，询问是否进行另一局游戏。我们没有解析输入，而是假设玩家会根据文本提示选择指定的肯定回答。如果未接收到这些特定回复，我们将打印一条感谢玩家游玩本游戏的消息。这标志着游戏函数的结束。

## 23 最终得分

回到最开始的 `start` 函数，当游戏结束后，我们进入结果展示阶段。这部分相当简单——它调用得分（整数），然后在玩家名字之后单独打印出来。就玩家而言，这就是脚本的终点。目前，代码不会永久保存得分，但如果你愿意，可以让 Python 将其写入文件以保留记录。

## 24 模块

代码的最后部分允许该脚本以两种方式运行。首先，我们可以在命令行中执行它，它会正常工作。其次，我们可以将其导入到另一个 Python 脚本中，例如你想将它作为一个游戏添加到游戏合集时。这段最后的代码将防止我们的脚本在被其他模块导入时自动执行——只有直接运行它时才会执行。

```python
19 def hand(dice):
   dice_hand = [len(list(group)) for key, group in groupby(dice)]
   dice_hand.sort(reverse=True)
   straight1 = [1,2,3,4,5]
   straight2 = [2,3,4,5,6]
21 if dice == straight1 or dice == straight2:
       return "a straight!"
   elif dice_hand[0] == 5:
       return "five of a kind!"
   elif dice_hand[0] == 4:
       return "four of a kind!"
   elif dice_hand[0] == 3:
       if dice_hand[1] == 2:
           return "a full house!"
       else:
           return "three of a kind."
   elif dice_hand[0] == 2:
       if dice_hand[1] == 2:
           return "two pair."
       else:
           return "one pair."
   else:
       return "a high card."
22 def play_again():
   answer = raw_input("Would you like to play again? y/n: ")
   if answer in ("y", "Y", "yes", "Yes", "Of course!"):
       return answer
   else:
       print "Thank you very much for playing our game. See you next time!"
23 def scores():
   global player_score, computer_score
   print "HIGH SCORES"
   print "Player: ", player_score
   print "Computer: ", computer_score
24 if __name__ == '__main__':
   start()
```

# 为 Python 游戏创建图形界面

将 Python 图形用户界面（GUI）整合在一起，迈出编程自有软件的下一步

## 资源

- **Python 2：** www.python.org/download
- **IDLE：** www.python.org/idle

**开始部分**
在这里我们进行一些基础设置，包括引入一个新模块，该模块有助于创建简单的图形界面。

**导入部分**
我们导入了之前几期教程中创建的三个游戏，以便调用或使用它们。

**窗口部分**
创建一个图形窗口并为其命名，以便我们可以向其添加一些函数。

**框架部分**
定义窗口的尺寸，并为其中对象的布局提供大致指引。

**欢迎语部分**
在窗口中打印一条消息并将其放置在特定位置。其工作机制与普通的 `print` 略有不同。

**按钮部分**
本教程的重点是让“石头剪刀布”在图形界面中运行，因此我们正在调用一个新创建的函数。

**界面部分**
创建并格式化按钮，以在命令行或 shell 中启动另外两个教程游戏。

**退出部分**
在这里我们创建一个按钮，用于关闭窗口并结束脚本。我们还将其特定地放置在窗口的底部。

**主循环**
主循环（mainloop）允许主窗口持续运行并更新，除非指定退出，否则不会终止程序。

我们在 Python 中制作的三个基本游戏目前都在命令行或通过 IDLE（Python 集成开发环境）运行。虽然这让我们展示了使用 Python 代码的不同方法，但我们实际上尚未向你展示如何呈现它。在本教程中，我们将把所有三个游戏放入一个统一且整洁的图形界面中。

为此，我们将利用之前每个教程底部添加的那行小代码，以便将它们作为模块导入到我们的主图形脚本中。我们还将修改现有代码以添加一些图形元素。为了完成所有这些工作，我们将使用 Tkinter，这是 Python 中默认可用的一个模块，允许你用相对简单的代码创建窗口和框架。

本教程所需的所有内容是一个最新版本的 Python（可从你的发行版软件源或官网获取）以及 IDLE 开发环境。这也非常适合在树莓派系统（如 Raspbian）上运行。

## 主界面代码列表

```python
#!/usr/bin/env python2
#Linux User & Developer presents: Mega Microgames Collection

from Tkinter import *

import rockpaperscissors
import hangman
import pokerdice

root = Tk()
root.title ("Linux User & Developer’s Mega Microgames Collection")

mainframe = Frame(root, height = 200, width = 500)
mainframe.pack_propagate(0)
mainframe.pack(padx = 5, pady = 5)

intro = Label(mainframe, text = """Welcome to Linux User & Developer’s Mega
Microgames Collection.
Please select one of the following games to play:
""")
intro.pack(side = TOP)

rps_button = Button(mainframe, text = "Rock, Paper, Scissors", command =
rockpaperscissors.gui)
rps_button.pack()

hn_button = Button(mainframe, text = "Hangman", command = hangman.start)
hn_button.pack()

pd_button = Button(mainframe, text = "Poker Dice", command = pokerdice.start)
pd_button.pack()

exit_button = Button(mainframe, text = "Quit", command = root.destroy)
exit_button.pack(side = BOTTOM)

root.mainloop()
```

# Python 基础

## 修改后的石头剪刀布代码列表

```python
#!/usr/bin/env python2

# Linux User & Developer presents: Rock, Paper, Scissors: The Video Game: The Module

from Tkinter import *
import random

def gui():
    rock = 1
    paper = 2
    scissors = 3

    names = {rock: "Rock", paper: "Paper", scissors: "Scissors"}
    rules = {rock: scissors, paper: rock, scissors: paper}

def start():
    while game():
        pass

def game():
    player = player_choice.get()
    computer = random.randint(1, 3)
    computer_choice.set(names[computer])
    result(player, computer)

def result(player, computer):
    new_score = 0
    if player == computer:
        result_set.set("In game tie")
    else:
        if rules[player] == computer:
            result_set.set("Your victory has been assured.")
            new_score = player_score.get()
            new_score += 1
            player_score.set(new_score)
        else:
            result_set.set("The computer laughs as you realise you have been defeated.")
            new_score = computer_score.get()
            new_score += 1
            computer_score.set(new_score)
    
    rps_window = Toplevel()
    rps_window.title("Rock, Paper, Scissors")

    player_choice = IntVar()
    computer_choice = StringVar()
    result_set = StringVar()
    player_choice.set(1)
    player_score = IntVar()
    computer_score = IntVar()

    rps_frame = Frame(rps_window, padding = '3 3 12 12', width = 300)
    rps_frame.grid(column=0, row = 0, sticky=WENS)
    rps_frame.columnconfigure(0, weight=1)
    rps_frame.rowconfigure(0, weight=1)

    Label(rps_frame, text='Player').grid(column=1, row = 1, sticky = W)
    Radiobutton(rps_frame, text = 'Rock', variable = player_choice, value = 1).grid(column=1, row=2, sticky=W)
    Radiobutton(rps_frame, text = 'Paper', variable = player_choice, value = 2).grid(column=1, row=3, sticky=W)
    Radiobutton(rps_frame, text = 'Scissors', variable = player_choice, value = 3).grid(column=1, row=4, sticky=W)

    Label(rps_frame, text='Computer').grid(column=3, row = 1, sticky = W)
    Label(rps_frame, textvariable = computer_choice).grid(column=3, row=3, sticky = W)

    Button(rps_frame, text='Play', command = start).grid(column = 2, row = 2)

    Label(rps_frame, text = 'Score').grid(column = 1, row = 5, sticky = W)
    Label(rps_frame, textvariable = player_score).grid(column = 1, row = 6, sticky = W)
    Label(rps_frame, text = 'Computer').grid(column = 3, row = 5, sticky = W)
    Label(rps_frame, textvariable = computer_score).grid(column = 3, row = 6, sticky = W)

    Label(rps_frame, textvariable = result_set).grid(column = 2, row = 7)

if __name__ == '__main__':
    gui()
```

- **新导入项**
导入新的模块，以便创建“石头剪刀布”的 GUI 部分，同时移除不再需要的模块。

- **新界面**
我们新的主函数允许在按下 `rps_button` 时调用游戏脚本的大部分功能。这包含了游戏组件和图形组件。

- **新启动函数**
我们修改了 `start` 函数，使其结束后不再跳转到得分函数。我们还移除了得分函数，因为采用不同的追踪方式以便正确显示。

- **新游戏逻辑**
我们修改了 `game` 函数，使其现在从图形界面获取输入。我们使用了一个新的变量来实现这一点，该变量与 GUI 配合工作，否则其运行方式大致与之前相同。

- **新结果处理**
`result` 函数基本保持不变，只是现在它将结果消息发送到一个用于界面的变量中，并总体上使用新 GUI 的变量。

- **新窗口**
由于已经有一个‘mainloop’根窗口，我们使用略有不同的方法创建游戏窗口。我们还为其命名，以便正确识别。

- **新变量**
我们设置的新变量使其能够正确地与游戏代码和界面代码交互。我们还确保了玩家有默认选择，以便代码正常运行。

- **新框架**
使用与之前略有不同的方法确定游戏窗口的大小和布局。我们还允许元素固定在窗口周围的特定位置。

- **新选择项**
在这里，我们在窗口中放置单选按钮，具有特定的配置，给用户三种出招的选择。这随后传递给变量并被游戏代码使用。

- **新移动**
在这里，我们允许计算机的出招显示在‘Computer’标签下方。

- **新按钮**
按下我们在此处的 Play 按钮将运行游戏脚本，打印出得分，最后根据结果打印一条消息。

- **新结尾**
我们进行了修改，现在主脚本以 `gui` 开始，而不是 start 函数。

