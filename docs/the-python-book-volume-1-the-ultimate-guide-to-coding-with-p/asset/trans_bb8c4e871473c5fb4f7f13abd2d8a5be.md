
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
    print("Let's play a game of Linux Poker Dice.")
    while game():
        pass
    scores()
def game():
    print("The computer will help you throw your 5 dice")
    throws()
    return play_again()
```

> 复用
> 代码中有一些变量出现了重复——虽然我们已经小心确保它们能按预期工作，但这并非最佳的代码规范。变量的名字本身并不重要——最好以你能理解的方式命名，便于调试和他人阅读。

## 01 开始

和之前一样，我们使用这一行来指定 Python 解释器的路径。这允许我们在终端中运行程序，或在像 IDLE 这样的 Python 专用 IDE 之外运行。请注意，这个脚本使用的是 Python 2。

## 02 导入

除了为掷骰导入 random 模块外，我们还需要用到 groupby 函数，以便对骰子进行排序，使其更易读，也便于在告知玩家他们拥有什么牌型时进行分析。

## 03 牌面

虽然我们使用随机数来掷骰，但如果不为每个数字分配对应的牌面，玩家就不知道他们掷出了什么，也不知道哪些牌型更好。我们将每张牌对应一个数字，然后设定这些数字打印出来时应显示的牌面。

## 04 计分

和往常一样，我们为玩家和电脑初始化了空分数，以便在游戏过程中更新它们。虽然在此版本的代码中没有专门使用到，但很容易扩展它，添加你自己的简单电脑掷骰，或为双方掷骰添加有限的AI。

## 05 启动

我们通过‘start’函数开始代码的交互部分。它向玩家打印问候语，然后启动一个 while 循环，让我们可以随心所欲地重玩多次。pass 语句让 while 循环在我们完成后能够停止。如果我们确实停止游戏，那么就会调用 score 函数。

## 06 游戏

和我们的石头剪刀布代码类似，def game 把游戏的其余部分委托给其他函数，它的主要功能是让玩家通过 play_again 函数不断重复游戏。

## 07 掷骰

对于第一次掷骰，我们需要五个随机骰子。我们在这里设置一个变量传给掷骰函数，以便之后可以用玩家选择的不同数字来复用它。我们从函数返回的列表中取得五个随机数，并使用 sort 对其进行排序，让玩家看起来更易读，也便于之后的手牌函数处理。

## 08 骰子显示

我们打印出每个骰子，为它们编号，让玩家知道哪个骰子是哪个，同时显示我们在脚本开头设置的名称。我们通过一个循环来实现这一点，该循环使用 range(len(dice)) 参数，重复次数与骰子列表的长度相同。i 每次循环都会递增，并打印出骰子列表中对应编号的那个骰子。

## 09 当前手牌

我们想在游戏过程中多次确定玩家的手牌类型，因此专门设置了一个函数来查明。我们将当前的一串骰子传给这个函数，并打印结果。

## 10 再次掷骰

在第二轮掷骰之前，我们需要知道哪些骰子需要

```python
def throws():
    roll_number = 5
    dice = roll(roll_number)
    dice.sort()
    for i in range(len(dice)):
        print("Dice",i + 1,",",names[dice[i]])
    result = hand(dice)
    print("You currently have", result)
    while True:
        rerolls = input("How many dice do you want to throw again? ")
        try:
            if rerolls in (1,2,3,4,5):
                break
        except ValueError:
            pass
            print("Oops! I didn't understand that. Please enter 1, 2, 3, 4 or 5.")
    if rerolls == 0:
        print("You finish with", result)
    else:
        roll_number = rerolls
        dice_rerolls = roll(roll_number)
        dice_changes = range(rerolls)
        print("Enter the number of a dice to reroll: ")
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
                    print("Oops! I didn't understand that. Please enter 1, 2, 3, 4 or 5.")
        dice_changes[iterations-1] = selection-1
        print("You have changed dice", selection)
```

## 缩进

注意缩进，因为我们拆分了 else 函数。下一页的代码与代码中的 roll_roll_number、dice_rerolls 和 dice_changes 处于同一层级。

## 空白

throws 末尾的较大 if 函数在各个部分之间没有太多空行——你可以根据需要添加空行，将代码在视觉上分成更小的块，有助于调试。

## 11 保留

我们在这些教程中一直在努力做到的一件事是，指出逻辑如何通过简单的排除法或遵循流程图来减少大量编码。如果用户想要重掷零次，那就意味着他们对当前手牌满意，游戏必然结束。我们打印一条消息来表明这一点，并再次显示他们的手牌。

我们还需要确保输入的数字在游戏允许的范围内，因此我们使用 try 函数进行检查，并打印出一条消息，告诉用户是否出错以及错在哪里。

## 12 重掷

这里我们开始第二次掷骰并进入游戏结束阶段，使用一个长长的 else 来配合我们刚刚开始的 if 语句。我们首先确保设置好变量——更新 roll_number，以用户设置的重掷次数传给 roll 函数，并借助 range(rerolls) 创建一个长度正好为我们想使用的新掷骰集合的列表。

## 13 解析

我们让玩家输入他们想要重掷的骰子的编号。通过设置一个 iterations 变量，我们可以让 while 循环持续的次数与期望的重掷次数相同，方法是将其与 reroll 变量本身进行比较。我们检查每次输入，确保它是一个可用的数字，并将合法选择添加到 dice_changes 列表中。这里使用 iterations-1，因为 Python 列表从 0 而不是 1 开始。我们还会打印一条简短消息，让玩家知道选择已成功。
