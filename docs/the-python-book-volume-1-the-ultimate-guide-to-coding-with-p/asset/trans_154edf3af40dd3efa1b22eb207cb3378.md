

# 修改后的 RPS 代码清单

## 新导入
导入新的模块以允许我们创建剪刀石头布的 GUI 部分，以及移除我们不再需要的模块

## 新界面
我们新的主函数允许我们在按下 rps_button 时调用大部分游戏脚本。这包含了游戏组件和图形组件

## 新开始
我们更改了开始函数，使其在完成后不再跳转到分数函数。我们也移除了分数函数，因为我们以不同的方式跟踪分数，以便能够正确显示

## 新游戏
我们更改了游戏函数，使其现在接收来自图形界面的输入。我们使用一个新变量来实现这一点，它可以与 GUI 配合工作，否则它与之前大致相同

## 新结果
结果函数基本保持不变，只是现在它将结果消息发送到我们用于界面的变量中，并且通常使用新的 GUI 的变量

## 新窗口
我们以略有不同的方法创建游戏窗口，因为已经存在一个 'mainloop' 根窗口。我们也为其命名，以便你能够正确识别它

## 新变量
我们的新变量设置使其能够与游戏代码和界面代码正确交互。我们也确保为玩家提供默认选择，以便代码能够正常运行

## 新框架
使用与之前略有不同的方法确定游戏窗口的大小和布局。我们也允许元素锚定在窗口周围的特定位置

## 新选择
在这里我们以特定配置在窗口中放置单选按钮，给用户三种出招的选择。这随后会传递给变量并由游戏代码使用

## 新出招
在这里我们允许计算机的出招在 'Computer' 标签下显示

## 新按钮
按下我们放置在此处的 Play 按钮会运行游戏脚本，打印出分数并最终根据结果显示一条消息

## 新结束
我们已将其更改为使主脚本现在以 gui 开始，而不是开始函数

```
#!/usr/bin/env python2
# Linux User & Developer presents: Rock, Paper, Scissors: The Video Game: The Module

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
    def result(player, computer):
        new_score = 0
        if player == computer:
            result_set.set("Tie game.")
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
    player_score = IntVar()
    computer_score = IntVar()
    rps_frame = Frame(rps_window, padding="3 3 12 12", width = 300)
    rowconfigure(rps_frame, 0, weight=1)
    rps_frame.columnconfigure(0, weight=1)
    rps_frame.rowconfigure(0, weight=1)
    Label(rps_frame, text="Player").grid(column=1, row=1, sticky=W)
    Radiobutton(rps_frame, text="Rock", variable=player_choice, value=1).grid(column=1, row=2, sticky=W)
    Radiobutton(rps_frame, text="Paper", variable=player_choice, value=2).grid(column=1, row=3, sticky=W)
    Radiobutton(rps_frame, text="Scissors", variable=player_choice, value=3).grid(column=1, row=4, sticky=W)
    Label(rps_frame, text="Computer").grid(column=3, row=1, sticky=W)
    Label(rps_frame, textvariable=computer_choice).grid(column=3, row=2, sticky=W)
    Button(rps_frame, text="Play", command=start).grid(column=2, row=2)
    Label(rps_frame, text="Score").grid(column=1, row=5, sticky=W)
    Label(rps_frame, textvariable=player_score).grid(column=1, row=6, sticky=W)
    Label(rps_frame, textvariable="Score").grid(column=3, row=5, sticky=W)
    Label(rps_frame, textvariable=computer_score).grid(column=3, row=6, sticky=W)
    Label(rps_frame, textvariable=result_set).grid(column=2, row=7)
    if __name__ == "__main__":
        gui()
```
