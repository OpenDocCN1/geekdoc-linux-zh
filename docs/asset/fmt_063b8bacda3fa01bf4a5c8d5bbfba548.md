
剩下的代码与我们之前所做的类似：用于显示固定文本以及变化中的分数/结果文本的标签。激活重置函数的按钮也放在这里底部。最后两行允许我们将模块导入到界面代码中。

```python
    Label(hm_frame, text = "Wins").grid(column = 1, row = 7, sticky = W)
    Label(hm_frame, textvariable = player_score).grid(column = 1, row = 7, sticky = W)
    Label(hm_frame, text = "Losses").grid(column = 3, row = 7, sticky = W)
    Label(hm_frame, textvariable = computer_score).grid(column = 3, row = 8, sticky = W)
    Label(hm_frame, textvariable = result_set).grid(column = 2, row = 9)
    replay_button = Button(hm_frame, text = "Reset", command = reset_game).grid(column = 2, row = 10)

    if __name__ == '__main__':
        gui()
```

## 原始界面

你还需要之前教程中的界面代码，它已经可以与修改过的猜拳代码一起工作。由于之前的结束方式，它无法与新代码一起工作，因此你需要将每个按钮中的命令从 `game.start` 更改为 `game.gui`。

![](img/e016e192a91ffc1a9e474690a590742f_58_0.png)

## 猜字游戏 GUI

按下更新后的“Hangman”按钮以启动一个新窗口。在这里，我们有初始图形、单词线索以及供玩家交互的输入框。分数设置为零，由于尚未进行任何游戏，因此没有显示结果消息。

![](img/e016e192a91ffc1a9e474690a590742f_58_1.png)

## Python 基础知识

### 17 重新开始

这里通常有*数组*形式的命令行兼容性和模块导入。这里的 `groupby` 函数是专门为骰子分析而导入的。

### 18 骰子外部

对于扑克骰子，任何时刻只有一个变量需要显示，即骰子。同样，由于嵌套函数，且我们使用的是 Python 2，我们需要从这里使用 `global` 来调用，以确保游戏能够正确重置。

### 19 掷骰

`roll` 函数已从 `gui` 函数中移除，以避免其某些变量导致代码错误。它可以轻松地在嵌套函数中调用。它与原始代码没有任何变化。

### 20 骰子手牌

与 `roll` 一样，`hand` 函数也没有任何变化。它现在仅仅被放置在 `gui` 函数外部，原因完全相同。这也意味着，如果你愿意，可以轻松地将此函数导入到另一个脚本中。

### 21 GUI 启动

正如我们上个月提到的以及在人梯代码中所述，我们将所有 GUI 代码放入一个函数中，以便我们随时可以调用它。在这种情况下，在主界面上按下扑克骰子按钮会激活 `pokerdice.gui`，即此函数。

### 22 首次掷骰

窗口打开时，我们立即进行首次掷骰。然后排序，每个数字赋予一张牌，并创建结果以在主窗口中显示。这类似于之前的工作方式，但现在它是在脚本末尾输入到界面的 `StringVars` 中。

### 23 开始游戏

当我们激活启动 `game` 的按钮时，它会立即引导我们进入其余代码。如果你让按钮转到 `throws` 函数，这也有效；不过，如果你愿意，可以在此处添加更多函数。

### 24 骰子选择

我们做的第一件事是找出玩家勾选了哪些复选框。然后我们将它们放入列表中，以便我们可以更改正确的骰子数字。我们还引入了 `dice`，以便我们可以检查当前骰子的点数。

```python
#!/usr/bin/env python2
from Tkinter import *
from ttk import *
import random
from itertools import groupby
dice = 0

def roll(roll_number):
    numbers = range(1,7)
    dice = range(roll_number)
    iterations = 0
    while iterations < roll_number:
        iterations = iterations + 1
        dice[iterations-1] = random.choice(numbers)
    return dice

def hand(dice):
    dice_hand = [len(list(group)) for key, group in groupby(dice)]
    dice_hand.sort(reverse=True)
    straight1 = [1,2,3,4,5]
    straight2 = [2,3,4,5,6]
    if dice == straight1 or dice == straight2:
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

def gui():
    global dice
    dice = roll(5)
    dice.sort()
    nine = 1
    ten = 2
    jack = 3
    queen = 4
    king = 5
    ace = 6
    names = { nine: "9", ten: "10", jack: "J", queen: "Q", king: "K", ace: "A"}
    result = ("You have " + hand(dice))

def game():
    throws()

def throws():
    global dice
    dice1_check = dice1.get()
    dice2_check = dice2.get()
    dice3_check = dice3.get()
    dice4_check = dice4.get()
    dice5_check = dice5.get()
    dice_rolls = [dice1_check, dice2_check, dice3_check, dice4_check, dice5_check]
```

![](img/e016e192a91ffc1a9e474690a590742f_59_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_59_1.png)

### 25 需重掷的骰子

如果复选框未被选中，我们将其设置为给出零值。我们希望从列表中移除这些，以便更改正确的骰子，因此我们使用 for 循环检查列表的每个部分，然后在元素等于零时使用 `remove` 函数。

```python
    for i in range(len(dice_rolls)):
        if i in dice_rolls:
            dice_rolls.remove(i)
```

### 26 提前结束

如果没有选择重掷的骰子，列表将包含所有 0，这些将被移除。该列表的长度将为零，这意味着如果玩家未选择任何骰子就点击重掷，我们可以使用它来结束游戏。

```python
    if len(dice_rolls) == 0:
        result = "You finish with " + hand(dice)
        hand_output.set(result)
```

### 27 新骰子

此 `else` 函数大致与之前相同。我们首先获取需要掷多少骰子的必要信息，以及一个用于放置重掷的列表。然后我们用第一个 `while` 循环掷出所需数量的新骰子。
