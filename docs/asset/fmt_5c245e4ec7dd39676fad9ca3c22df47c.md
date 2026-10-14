
`hm_frame = Frame(hm_window, padding=12, width=300)`

`hm_frame.grid(row=0, column=0, sticky="NW")`

`hm_frame.grid(row=1, column=0)`

`hm_frame.grid(row=2, column=0)`

```python
Label(hm_frame, text="Score:").grid(row=0, column=0)

Label(hm_frame, textvariable=player_score).grid(row=0, column=1)

Label(hm_frame, text="Incorrect guesses:").grid(row=1, column=0)
```

```python
Label(hm_frame, text="Enter a letter:").grid(row=2, column=0)

Entry(hm_frame, textvariable=letter_guess).grid(row=2, column=1)

Button(hm_frame, text="guess", command=game).grid(row=2, column=2)
```

```python
Label(hm_frame, text="Clue:").grid(row=3, column=0)

Label(hm_frame, textvariable=clue).grid(row=3, column=1)

Label(hm_frame, text="Incorrect letters:").grid(row=4, column=0)
```

```python
Label(hm_frame, text="Word:").grid(row=5, column=0)

Label(hm_frame, textvariable=word_output).grid(row=5, column=1)

Label(hm_frame, text="Game Over").grid(row=6, column=0)

Button(hm_frame, text="Reset", command=reset_game).grid(row=6, column=1)
```

## 10 输入清理

`guess_letter` 函数从玩家输入获取字母，进行任何格式处理，将其转换为小写并返回。这样就可以使用它。

## 15 文本输入

这里 `Entry` 设置了一个文本框。选择选项在字母开始的地方。按钮激活游戏函数，让字母进行。

## 11 新窗口

我们使用 `frame` 分隔区域和游戏窗口。在这里创建了变量。`IntVar` 接收整数，`StringVar` 接收字符串。使用 `get` 和 `set` 处理这些值。

## 13 Frame 窗口

`frame` 与上一次一样。我们从窗口边缘设置 `frame`，设置网格，它保持在中心。

## 14 线索到猜字游戏

这些字母非常简单——我们要么在获取它们，要么使用特定的 `StringVar` 让它们在游戏时更新。

## 16 结果和重置

代码的其余部分与已经做的相似；显示固定文本并更改分数。重置按钮也在 `frame` 的底部。最后几行用于将模块导入界面代码中。

## 12 界面变量

`tkinter` 处理特定的变量。我们在这里创建了所有需要的。

`frame` 是像之前设置的

Python 之书 59

# Python 基础知识

## 重新开始

命令行兼容性和此处导入的模块。`groupby` 函数专门在这里导入，用于字典。

## 外部骰子

对于扑克骰子，只有一个变量一次一次。再次，由于引入了方法，而且因为我们使用 Python 2，我们仍然从这里调用它来让游戏正确重置。

## 骰子点

`roll` 函数删除了某些属性的错误。它可以在内部被调用。它从原始代码发生了变化。

## 骰子选择

我们做的第一件事是找出玩家标记了哪些骰子。然后我们将它们放入列表中，以便更改骰子中的正确数字，从而检查当前的骰子点。

## 额外游戏函数

```python
#/usr/bin/env python

from tkinter import *

import random

from itertools import groupby

dice(iterations) = random.choice(numbers)

def roll(number):
    numbers=range(1,number+1)
dice=random.choice(number)
    while iterations < iterations:
        dice.append(random.choice(numbers))
    return
```

我们提到 `game` 函数现在并不一定需要。你可以轻松地清理代码并删除它，或者添加随机选择骰子的功能，或者将其变为双玩家模式。尝试你想要的：

## 扑克骰子

初始窗口上打印了两个东西。第一组骰子以我们上次的方式显示，并进行牌型检查。特定的牌型在点击“掷骰子”按钮时使用。

```python
def hand(dice):
    dice_hand=[list(group) for key, group in groupby(dice)]
    if len(dice_hand)==1:
        straight=[2,4,5,6]
        if straight==dice:
            return "straight"
    elif len(dice_hand)==2:
        return "kind"
    elif len(dice_hand)==3:
        return "triple"
    elif len(dice_hand)==4:
        return "two pair"
    else:
        return "full house"
    else:
        return "three of a kind"
    else:
        return "one pair"
    return "one high card"
```

```python
def throws(dice):
    global dice
    dice=roll(5)
    dice.sort()
    nine=2
ten=3
jack=4
queen=5
king=6
ace=7
snap ={"9":"9","10":"10","J":"J","Q":"Q","K":"K","A":"A"}
    return "You have " + dice
```

![](img/516df994db593237169e2aff6d3e6840_59_0.png)

# Python 基础

```python
for i in range(len(dice_rerolls)):
    if dice_rerolls[i] == 0:
        dice_rerolls.remove(0)
        result = "Again " + hand(dice)
        hand_output.set(result)
    else:
        roll_number = len(dice_rerolls)
        dice_changes = range(dice_rerolls)
        iterations = 0
        while iterations < roll_number:
            iterations += 1
            dice_changes[iterations-1] = replace(dice_rerolls[iterations-1])
        iterations = 0
        for i in range(len(dice_changes)):
            new_list.append(dice_changes[i])
final_dice = " ".join(new_list)
hand_output.set(final_dice)
```
