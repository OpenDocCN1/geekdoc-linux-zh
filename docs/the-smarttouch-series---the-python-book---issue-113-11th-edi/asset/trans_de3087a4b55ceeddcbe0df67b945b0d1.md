
## Python 基础

```python
#!/usr/bin/env python2
import random
from itertools import groupby

nine = 1
ten = 2
jack = 3
queen = 4
king = 5
ace = 6

names = { nine: "9", ten: "10", jack: "J", queen: "Q", king: "K", ace: "A" }
player_score = 0
computer_score = 0

def start():
    print "Let's play a game of Linux Poker Dice."
    while game():
        pass
    scores()

def game():
    print "The computer will help you throw your 5 dice"
    throws()
    return play_again()
```

## 循环复用

代码中有一些变量存在重复使用——虽然我们已小心确保它们在所需位置正常工作，但这并不是最佳的编程习惯。变量的名称并不特别重要——最好的方式是以易于理解的方式进行命名，以便进行调试和供他人阅读。

### 01 开始
和以前一样，我们使用这一行来输入 Python 解释器的路径。这允许我们在终端中运行程序，或者在 Python 专用 IDE（如 IDLE）之外运行。请注意，我们在此脚本中也使用了 Python 2。

### 02 导入
除了导入用于掷骰子的 random 模块外，我们还需要引入 groupby 函数，以便以一种更易读且便于分析的方式对骰子进行排序，从而告诉玩家他们手中的牌型。

### 03 牌面
虽然我们在掷骰子时使用的是随机数，但除非我们将正确的牌面分配给每个数字，否则玩家不会知道自己掷出了什么，以及什么样的牌型更好。我们为每张牌设置了一个数字，然后定义了应该输出的内容。

### 04 分数
一如既往地，我们初始化了玩家和电脑的得分为空值，以便在过程中更新这些分数。虽然在这个版本的代码中并未专门使用它，但很容易扩展并添加一个简单的电脑掷骰子功能，或者为双方掷骰子添加有限的 AI。

### 05 启动
我们使用‘start’函数开始代码的交互式部分。它向玩家打印问候语，然后启动一个 while 循环，让我们可以随意重玩游戏。pass 语句允许 while 循环在结束后停止。如果我们确实停止玩游戏，则会调用分数函数。

### 06 游戏
与我们的“石头、剪刀、布”代码类似，def game 将游戏的其余部分委派给其他函数，其主要功能通过将玩家传递给 play_again 函数，使我们能够不断重复游戏。

### 07 掷骰子
对于第一次掷骰子，我们希望掷出五个随机骰子。我们在这里设置了一个变量，传递给我们的掷骰函数，以便稍后可以使用玩家选择的另一个数字来重用它。我们从一个列表中获取函数返回的五个随机数，并使用 sort 进行排序，使其对玩家稍后以及对于牌型函数更容易阅读。

### 08 骰子显示
我们打印出每个骰子，并为它们编号，以便玩家知道哪个骰子是哪个，同时也赋予它们在脚本开始时设置的名称。我们使用一个循环来执行此操作，该循环根据骰子列表的长度使用 range(len(dice)) 参数重复执行相应次数。i 每轮增加，并打印出骰子列表中特定位置的数字。

### 09 当前牌型
我们希望在游戏过程中多次查找玩家手牌的类型，因此设置一个专门的函数来查找。我们将拥有的骰子系列传递给该函数，并打印结果。

### 10 再次掷骰子
在第二轮掷骰子之前，我们需要知道玩家想重新掷哪些骰子。我们通过询问他们想重掷几次来开始这一步，这允许我们创建一个自定义的 while 循环，询问用户要更改哪些骰子，并迭代正确的次数。

我们还必须确保它是一个游戏范围内的数字，这就是为什么我们使用 *try* 函数进行检查，并打印一条消息，告诉用户他们错在哪里以及如何纠正。

### 11 保持
我们在这些教程中尝试做的其中一件事是指出，逻辑可以通过简单的过程消除法或遵循流程图来减少大量的编码。如果用户想重掷零次，这意味着他们对当前手牌感到满意，那么游戏必须结束。我们打印一条消息来指示这一点，并再次显示他们的手牌。

### 12 重新掷骰子
这里是第二次掷骰子和游戏结束的地方，使用一个长的 *else* 对应我们刚刚开始的 *if* 语句。首先，我们要确保设置我们的变量 - 更新 *roll_number* 以便将用户设置的重新掷骰子数传递给 *roll* 函数，并利用 *range* (rerolls) 创建要使用的列表。

### 13 解析
我们要求玩家输入想要重新掷的骰子的编号。通过设置 *iterations* 变量，我们可以让 while 循环持续与我们想要的重掷次数相同的次数，方法是将其与 reroll 变量本身进行比较。

我们检查每个输入以确保它是可用的数字，并将有效选择添加到 *dice_changes* 列表中。我们在这里使用 *iterations-1*，因为 Python 列表从 0 开始而不是 1。我们还打印一条简短的消息，让玩家知道选择成功。

![](img/e016e192a91ffc1a9e474690a590742f_46_0.png)

```python
def throws():
    roll_number = 5
    dice = roll(roll_number)
    dice.sort()
    for i in range(len(dice)):
        print "Dice", i + 1, ":", names[dice[i]]

    result = hand(dice)
    print "You currently have", result

    while True:
        rerolls = input("How many dice do you want to throw again? ")
        try:
            if rerolls in (1,2,3,4,5):
                break
        except ValueError:
            pass
    print "Oops! I didn't understand that. Please enter 1, 2, 3, 4 or 5."
    if rerolls == 0:
        print "You finish with", result
    else:
        roll_number = rerolls
        dice_rerolls = roll(roll_number)
        dice_changes = range(rerolls)
        print "Enter the number of a dice to reroll: "
        iterations = 0
        while iterations < rerolls:
            iterations = iterations + 1
            while True:
                selection = input("")
                try:
                    if selection in (1,2,3,4,5):
                        break
                except ValueError:
                    pass
            print "Oops! I didn't understand that. Please enter 1, 2, 3, 4 or 5."
            dice_changes[iterations-1] = selection-1
            print "You have changed dice", selection
```

> **缩进**
>
> 当我们拆分 *else* 函数时，再次注意缩进。下一页的代码与代码中的 *roll* roll_number, *dice_rerolls* 和 *dice_changes* 处于同一级别。

> **空格**
>
> *throws* 末尾的大 *if* 函数在部分之间没有很多换行符 - 你可以随意添加这些换行符，在视觉上将代码分成更小的块，有助于调试。

## Python 基础

```python
iterations = 0
while iterations < rerolls:
    iterations = iterations + 1
    replacement = dice_rerolls[iterations-1]
    dice[dice_changes[iterations-1]] = replacement

dice.sort()
for i in range(len(dice)):
    print "Dice," i + 1, "", names[dice[i]]

result = hand(dice)
print "You finish with", result

def roll(roll_number):
    numbers = range(1,7)
    dice = range(roll_number)

iterations = 0
while iterations < roll_number:
    iterations = iterations + 1
    dice[iterations-1] = random.choice(numbers)

return dice
```

![](img/e016e192a91ffc1a9e474690a590742f_47_0.png)

### 14 新的骰子
我们正在重置并重新使用 iterations 变量，以执行类似的 while 循环来更新我们对原始 dice 变量所做的掷骰子操作。此循环的主要部分是使用 iterations-1 变量从 dice_changes 列表中查找数字，并使用该数字更改 dice 列表中特定的整数为 replacement 列表中的数字。因此，如果 dice_changes 列表中的第一项是 2，那么 dice 列表中的第二项将被更改为我们想要替换的数字。

### 15 排序
我们基本上以与结束第一次掷骰子相同的方式结束了 throw 函数。首先，我们重新对 dice 列表进行排序，使所有数字按升序排列。然后，我们打印出骰子对应的最终牌面，再次将其传递给 hand 函数，以便我们可以完全确定玩家的手牌。我们打印出这个结果，函数随之结束，将整个过程发送回 game 函数，以便如果你想再玩一次。

### 16 掷骰子
roll 函数在代码中使用了两次，用于两次掷骰子。能够多次使用相同的代码意味着我们可以减少脚本其他部分的臃肿，正如我们解释的那样，使其运行得稍快一些。这也意味着在这种情况下，如果你想将游戏改为三轮或修改为真实扑克牌，我们可以再次使用它。

### 17 掷骰子次数
我们通过将 roll_number 变量引入函数来开始整个过程——这是因为在原始掷骰子中它总是五，而第二次掷骰子可能在一到五之间。我们创建一个包含每次掷骰子所需条目数量的列表，并再次为接下来的 while 循环设置 iterations 变量。

### 18 记住
与代码其余部分的 while 循环非常相似，我们一直继续直到 iterations 等于 roll_number。dice 列表中的每个条目都使用 random.choice 函数替换为一个随机数，并将其保持在 numbers 变量范围内，该范围为每个骰子面的 1 到 6。完成后，我们将 dice 变量返回给构成游戏大部分的 throw 函数。

### 19 手牌分析
虽然严格来说不是一副牌，但扑克术语仍然适用。我们在这个函数中从设置几样东西开始。第一部分使用我们导入的 groupby 函数——在此情况下用于统计组成 dice 变量的数字。如果有三个 2，一个 4 和一个 6，它将返回 [3, 1, 1]，并以此确定玩家持有的手牌类型。由于此 groupby 的输出不会按特定顺序排列，我们再次使用 sort 函数进行排序；然而，这次我们使用 reverse=True 参数以使分析更容易。

### 20 顺子
顺子和高牌在扑克骰子中是例外，因为它们不依赖于能够计算卡牌中的任何重复。然而，扑克骰子中只有两种手牌可以组成顺子，因此我们在这里创建了两个包含它们的列表。然后我们可以先检查骰子是否组成这些手牌，然后如果所有其他检查失败，它必须是高牌。

### 21 你的手牌
虽然看起来冗长，但这只是一个相当简单的 if 语句。正如我们之前所述，我们检查它是否是两种顺子手牌之一，因为扑克骰子中没有同花或皇家同花顺，所以我们不必担心那些。然后我们检查列表中的第一项是否为五，这只能导致五张相同；同样，如果第一项是四，那么手牌必须是四张相同。如果第一个数字是三，那么它可以是全满贯或三张相同。

## 高点或低点
哪种手牌最好？在游戏中获得特定手牌的几率是多少？有些答案令人惊讶，因为它们基于的扑克手牌压倒了骰子产生的不同几率。我们已将手牌从高到低排名。

| 手牌 | 几率 |
| :--- | :--- |
| 五张相同 | 6/7776 |
| 四张相同 | 150/7776 |
| 全满贯 | 300/7776 |
| 顺子 | 240/7776 |
| 三张相同 | 1200/7776 |
| 两对 | 1800/7776 |
| 一对 | 3600/7776 |
| 高牌 | 480/7776 |

