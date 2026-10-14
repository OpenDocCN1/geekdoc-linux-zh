
```python
if rerolls in (1,2,3,4,5):
    break
except ValueError:
    print("噢！我不理解。请输入 1, 2, 3, 4 或 5.")
```

## 重掷
我们在这里通过调用相同的函数进行第二组投掷，但我们也意识到不重掷意味着游戏结束。

```python
if rerolls == 0:
    print("You finish with result)
```

## 骰子
在这里找出哪个骰子想要重掷，并确保他们做出有效的选择，这样他们就知道。

```python
roll_number = rerolls
dice = roll(roll_number)
dices = range(rerolls)
print(f"要掷的骰子数量: {dice}")
iterations = 0
while iterations < rerolls:
    try:
        selection = input(" ")
        if selection in (1,2,3,4,5):
            break
    except ValueError:
        print("我不理解。请输入 1, 2, 3, 4 或 5")
dice_changes = int(selection)-1
print(f"你改变了 {dice_changes} 个骰子")
```

## 第二手牌
我们更改并显示手牌以结束游戏。再次，我们显示实际的手牌。

```python
iterations = 0
while iterations < rerolls:
    iterations += 1
    replacement = dice[iterations-1]
    dice_changes = int(iterations-1)
dice.sort()
for i in range(len(dice)):
    print(f"{i}:{dice[i]}")
result = hand()
print("You finish with", result)
```

## 投掷
使用简单循环来投掷我们的虚拟骰子的函数。

## 分析
骰子中有八种手牌，我们可以使用逻辑来计算出任何一种，而不需要检查所有的78结果——事实上，我们必须专门检查...

```python
if hand:
    hand = [list(group) for key, group in groupby(dice)]
    hand.sort(reverse=True)
    if len(hand) == 1:
        return "full house"
    elif len(hand) == 2:
        return "four of a kind"
    elif len(hand) == 3:
        return "three of a kind"
    elif len(hand) == 2:
        return "two pair"
    else:
        return "one pair"
else:
    return "high card"
```

## 问题
我们的“玩骰子”函数让玩家输入，以便我们可以重启或结束脚本。

```python
def play_game():
    answer = input("你想再玩一次吗？ y/n")
    if answer in ('y', 'Y', 'yes', 'Yes', 'Of course'):
        return play_game()
    else:
        print("感谢你玩我们的游戏。下次见！")
```

## 结束
分数在脚本末尾显示，最后部分允许将其作为模块导入到其他 Python 脚本中

```python
def score(dice):
    global player_score, computer_score
    print(f"HIGH SCORE:")
    print(f"Player: {player_score}")
    print(f"Computer: {computer_score}")
if __name__ == "__main__":
    start()
```

> 提取
将动作封装成函数使得更容易避免重复执行它们，但减少了代码量。在较大的项目中，这可以提高速度。

![](img/516df994db593237169e2aff6d3e6840_44_0.png)

# Python 基础

```python
#!/usr/bin/env python3
import random
from itertools import groupby
nine = 1
ten = 2
jack = 3
queen = 4
king = 5
ace = 6
names = {nine: "9", ten: "10", jack: "J", queen: "Q", king: "K", ace: "A"}
player_score = 0
computer_score = 0
def start():
    print("Let's play a game of Poker Dice.")
    while game():
        pass
    scores()
def game():
    print("The computer will help you throw your 5 dice")
    return False
play_again()
```

循环利用 (RECYCLING)
代码中很少有重复的变量；虽然我们已经小心地确保它们在我们需要的地方正常工作，但这并不是最好的代码。变量的名称并不重要——最好的办法是按照你理解的方式保留它们，方便修复和他人阅读。

### 01 开始
与之前一样，使用此行来输入 Python 解释器的路径。这允许我们在终端内或 Python 特特定的 IDE 之外运行程序。注意，在我们后续的过程中在此脚本之外也将这样做。虽然在这个版本的代码中没有专门使用它，但很容易扩展它并添加你自己的简单电脑规则，或者以后通过玩家选择的不同数字来限制双方。我们从函数返回的列表中获取随机数，并使用它来让玩家以及随后的手牌分析读起来更具可读性。

### 02 导入
与之前一样，为我们的骰子导入 `random` 模块，我们需要获取 `groupby` 函数，这样我们在描述他们拥有什么牌型时，可以使用更易读且易于分析的方式来使用它。

### 05 开始
通过 `print` 函数启动代码的交互部分，它将进入一个循环，允许玩家尽可能多次地重玩游戏。`pass` 语句允许我们在完成后停止循环，然后再次调用 `game` 函数。

### 08 掷骰子
我们投掷每个骰子，并编号以便玩家知道是哪一个，同时赋予我们在脚本开始时设置的值。我们使用循环进行编写，每回合重复次数等于骰子列表的长度，并打印特定数量的骰子。

### 03 牌
虽然我们使用随机数来选择每个数字，但我们会将牌分配给单位，否则玩家将不知道他们掷出了什么以及拥有什么牌。我们将每张牌映射到一个数字，然后就会将其打印出来。

### 06 游戏
像石头剪刀布一样，骰子游戏将游戏的其余部分划分到其他函数中，`main` 函数允许我们通过来回骰子列表来重复游戏。

### 09 当前手牌
我们想在游戏期间找到牌型类型，所以我们需要多个一个特定的函数来查找。我们将我们拥有一系列骰子传递给这个函数并打印。

### 04 分数
一如既常，我们有玩家和电脑的空分数，可以进行更新。

### 07 投掷
对于我们的第一次投掷，我们有五个随机骰子。我们使用一个变量传递给我们的投掷函数，允许我们使用工作来开始。我们首先询问他们想要重掷多少个骰子，我们用它来创建一个 `while` 循环，要求用户检查迭代的次数是否正确。

### 10 投掷
在我们第二轮投掷骰子之前，我们需要知道玩家想要操作哪些骰子。如果用户选择重掷次数为零，那么意味着他们对此满意，并且必须结束游戏。

```python
def throws():
    roll_number = 5
    dice = roll(roll_number)
    dice.sort()
    for i in range(len(dice)):
        print("Dice", i+1,",names[dice[i]])
result = hand(dice)
print("You currently have", result)
while True:
    try:
        rerolls = input("How many dice do you want to throw again?")
```
