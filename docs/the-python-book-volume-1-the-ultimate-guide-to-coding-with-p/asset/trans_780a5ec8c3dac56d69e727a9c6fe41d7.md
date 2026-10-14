
## Python 基础知识

```
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
player_choice.set(1)
player_score = IntVar()
computer_score = IntVar()
```

![](img/3b256f430f51c98f1315671f6e4eec19_47_0.png)

## 15 结果函数

结果函数仍然和之前一样接收相同的两个变量，这两个变量是在游戏函数中设置的。虽然从技术上说，我们可以使用为界面设置的变量，但这些变量并不是纯粹的整数，如果处理不当可能会引发错误。考虑到这一点，我们创建了一个空的 new_score 变量，用它来有效地清理界面值，然后再将其加回去。

## 16 平局

判断结果的逻辑与之前相同。我们首先做简单的检查——玩家和电脑变量的数值是否相同。这次不同的是，我们不再打印文本，而是使用 Tkinter 的 set 函数将“Tie game”消息发送到结果变量中。

## 17 胜利

if 语句接着判断玩家是否获胜。与之前一样，我们使用预设的规则进行比较。与平局时一样，我们设置 result_set，但向用户显示不同的消息。最后，我们将 new_score 变量设置为当前玩家得分：使用 get 函数获取该得分，将其加一，然后再次使用 set 放回 player_score 变量。我们不能对 player_score 变量使用 +=，因为它不是标准变量。

## 18 失败

整个 if 语句的这一部分与之前的工作方式相同，即假定如果不是平局或胜利，就是失败。与新的胜利代码一样，它随后使用 set 更改将显示给玩家的消息，并通过 new_score 变量获取和更新电脑得分。

## 19 新窗口

由于原始窗口是主循环（mainloop）的一部分，我们不能像主界面代码那样使用 Tk() 创建窗口。不过，由于这个窗口是从它派生的，我们改用 Toplevel() 创建窗口。这样，窗口就可以独立运行并显示在主窗口的上方。我们还为它指定了名称，这不会改变主窗口的名称。

## 20 界面变量

这就是我们必须以不同方式调用和修改变量的原因。对于 Tkinter，我们需要让界面知道变量是整数还是文本值。IntVar 和 StringVar 分别用于这两种类型。我们还将 player_choice 变量设置为 1，也就是我们已经设置为“石头”的选项。这样，游戏启动时至少会有一个默认选项，并且不会引发错误。

## 21 游戏框架

我们创建界面项框架的方式略有不同。主界面中使用的是 pack 命令，而这里我们使用 grid，以确保它们以对用户有意义的方式排列。Padding（内边距）正是起到这个作用，它设置数值，确保框架内的项不会碰到窗口边缘。然后我们使用 .grid 命令创建这个框架。row 和 column 变量允许将行和列包含在

```
```python
rps_frame = Frame(rps_window, padding = '3 12 12', width = 300)
rps_frame.grid(column=0, row = 0, sticky=(N,W,E,S))
rps_frame.columnconfigure(0, weight=1)
rps_frame.rowconfigure(0,weight=1)

Label(rps_frame, text='Player').grid(column=1, row = 1, sticky = W)
Radiobutton(rps_frame, text = 'Rock', variable = player_choice, value = 1).grid(column=1, row=2, sticky=W)
Radiobutton(rps_frame, text = 'Paper', variable = player_choice, value = 2).grid(column=1, row=3, sticky=W)
Radiobutton(rps_frame, text = 'Scissors', variable = player_choice, value = 3).grid(column=1, row=4, sticky=W)

Label(rps_frame, text='Computer').grid(column=3, row = 1, sticky = W)
Label(rps_frame, textvariable = computer_choice).grid(column=3, row=3, sticky = W)

Button(rps_frame, text='Play', command = start).grid(column = 2, row = 2)

Label(rps_frame, text = 'Score').grid(column = 1, row = 5, sticky = W)
Label(rps_frame, textvariable = player_score).grid(column = 1, row = 6, sticky = W)

Label(rps_frame, text = 'Score').grid(column = 3, row = 5, sticky = W)
Label(rps_frame, textvariable = computer_score).grid(column = 3, row = 6, sticky = W)

Label(rps_frame, textvariable = result_set).grid(column = 2, row = 7)

if __name__ == '__main__':
    gui()
```
```

窗口的结构中，而 sticky 允许我们按特定方向对齐项——本例中是上、左、右、下四个方向的对齐。最后，我们通过赋予每一列和每一行相同的权重，并从零开始，确保它们被平等对待。

## 22 玩家的选择

我们为玩家的出拳创建一个标签，并将其放到网格位置——第一行、第一列。我们还使用 'sticky = W' 将其左对齐。然后，我们为玩家的出拳添加单选按钮，每个按钮位于同一列，但依次向下排列。我们为每个选项命名，然后将其赋值给 player_choice 变量。接着，我们让每个选项都有一个与我们在第一组规则中确定的出拳相对应的数值。

## 23 电脑的出拳

首先，我们为这一项添加标签，然后创建第二个标签来显示实际的出拳。为此，我们为 Label 添加 textvariable 选项，并使用稍早在游戏函数中更新的 computer_choice 变量。这仅会打印 names 列表中的文本，并将其左对齐。

## 24 点击开始

代码的运行完全依赖于“开始”按钮。这很简单：我们将它放在玩家和电脑出拳之间的行中，作为三列系统的一部分；并通过 command 选项运行 start 函数。由于界面的循环，我们可以不断点击它，而不需要被提示再次开始。只需关闭窗口，也会返回主界面窗口，因此我们不需要专门的退出按钮。

## 25 实时得分

我们要显示两组分数——一组是玩家的，另一组是电脑的。我们像标记玩家和电脑出拳那样为它们添加标签，将它们放在较低的行中，但仍位于相应的列中。在下方，我们再次使用 textvariable 选项来获取分配给相应分数变量的数值分数。最后，我们再创建一个标签来显示游戏结果的提示信息。

## 26 结束游戏

代码的最后一部分允许脚本被主窗口使用，同时也允许它在命令行或 shell 中独立运行。你需要进行一些修改才能让它独立运行，例如将其设为主循环（mainloop）而不是 Toplevel 窗口。不过，无论从哪里运行，它都能正常运行，而不需要从主界面启动。

