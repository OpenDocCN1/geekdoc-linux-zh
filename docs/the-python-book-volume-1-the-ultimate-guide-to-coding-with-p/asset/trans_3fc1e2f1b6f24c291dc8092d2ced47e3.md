

# 为简单的 Python 游戏添加图形

为你的剪刀石头布游戏的挂人游戏和扑克骰子代码添加图形界面

我们现在已经为之前制作的三款 Python 游戏创建了一个简单的选择器。此界面能够为我们的石头剪刀布游戏启动 GUI，并在终端中运行另外两个游戏。现在，我们将把挂人游戏和扑克骰子代码转换为与石头剪刀布类似的方式。

挂人游戏的技巧在于允许不同类型的输入，即文本，以及能够进行多轮游戏。Tkinter 允许文本输入，我们在整个游戏中更少地依赖于

'while' 循环。扑克骰子需要保留骰子分析代码，以及使用复选框更改特定骰子的选项。

我们将对大量原始代码进行修改以适应新的图形方案。这主要涉及剪切特定部分并让 Tkinter 特定代码自行处理这些部分。这些页面上的代码列表包括修改后的代码——我们将在后面的页面上讨论图形部分。

## 资源

Python 2: www.python.org/download
IDLE: www.python.org/idle

1 导入
这里我们进行相同的少量设置，包括获取 Tkinter 模块，该模块帮助我们创建简单的图形界面

2 单词
我们保留确定要猜测单词的变量，以便可以在代码中的任何位置轻松访问

3 函数
像上次一样，我们将原始代码的大部分放入新的函数 gui 中

4 分析
我们在继续进行代码的其余部分之前选择单词并分析它

5 图形
hangedman 函数基本保持不变，只是增加了在界面上显示 ASCII 图形的代码

6 猜测
我们检查犯错的次数，并调用 guess_letter 函数来检查输入的字母

## 挂人游戏代码列表

```
from Tkinter import *
from ttk import *
from random import *
word = 0
word_length = 0
clue = []
```

```
def gui():
    global word, word_length, clue
    dictionary = ["gnu", "kernel", "linux", "mageia", "penguin", "ubuntu"]
    word = choice(dictionary)
    word_length = len(word)
    clue = word_length * ["_"]
    tries = 0
```

```
def hangedman(hangman):
    graphic = [
        "     ",
        "  ---------",
        "  |       |",
        "  |       0",
        "  |      /|\",
        "  |       |",
        "  |      / \ ",
        "  |",
        "=========",
    ]
    graphic_set = graphic[hangman]
    hm_graphic.set(graphic_set)
```

```
def game():
    letters_wrong = incorrect_guesses.get()
    letter=guess_letter()
    first_index = word.find(letter)
    if first_index == -1:
        letters_wrong +=1
        incorrect_guesses.set(letters_wrong)
    else:
        for i in range(word_length):
```

```
if letter == word[i]:
    clue[i] = letter
hangedman(letters_wrong)
clue_set = "".join(clue)
word_output.set(clue_set)
if letters_wrong == tries:
    result_text = "Game Over. The word was " + word
    result_set.set(result_text)
    new_score = computer_score.get()
    new_score += 1
    computer_score.set(new_score)
    if "".join(clue) == word:
        result_text = "You Win! The word was " + word
        result_set.set(result_text)
        new_score = player_score.get()
        new_score += 1
        player_score.set(new_score)
```

```
def guess_letter():
    letter = letter_guess.get()
    letter = letter.strip()
    letter = letter.lower()
    return letter
```

```
def reset_game():
    global word, word_length, clue
    incorrect_guesses.set(0)
    hangedman(0)
    result_set.set("")
    letter_guess.set("")
    word = choice(dictionary)
    word_length = len(word)
    clue = word_length * ["_"]
    new_clue = "".join(clue)
    word_output.set(new_clue)
```

```
if __name__ == '__main__':
    gui()
```

## 扑克骰子代码列表

# 1 更多导入

我们添加了使 Tkinter 工作所需的新导入模块，并保持其余部分不变

# 2 骰子列表

保存骰子的列表保留在主函数之外，以便可以在任何地方访问

# 3 掷骰

同理适用于 roll 函数。它也不一定需要在 gui 函数内部

# 4 决策

我们稍后创建的图形代码中的复选框将为我们提供可以分析代码的数字。我们检索这些数字并检查它们以确定用户希望重新掷哪些骰子

# 5 手牌

最后，我们的手牌分析函数是原始代码中保留在 gui 函数之外的最后一部分。上面这个函数和这个函数都将必要的详细信息传回上层链，然后添加到新界面的新图形元素中

# 6 无骰子

如果没有骰子被选中重新掷，手牌输出将被更改以显示最终消息

# 7 重新掷

这部分几乎与之前相同——重新掷出一组新骰子，然后像之前一样插入到骰子列表中，然后重新排序以使手牌分析更容易

# 8 更多函数

新的 gui 函数是扑克骰子代码的主要更改，与之前一样包括 Tkinter 元素和其他原始代码部分

# 9 游戏开始

一个简单的函数，我们可以用它来激活骰子的重新掷

# 10 新手牌

新骰子被命名、分析，然后一切都设置好以便 gui 显示最终结果

# 11 重置

与挂人游戏代码一样，我们有一个函数来重置所有变量，让你可以再次开始游戏

```
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

choice(numbers)

def hand(dice):
    dice_hand = [len(list(group)) for key, group in itertools.groupby(dice)]
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
    names = { nine: "9", ten: "10", jack: "J", queen: "Q", king: "K", ace: "A" }
    result = "You have " + hand(dice)

def game():
    throws()

def throws():
```

```
global dice
dice1_check = dice1.get()
dice2_check = dice2.get()
dice3_check = dice3.get()
dice4_check = dice4.get()
dice5_check = dice5.get()
dice_re rolls = [dice1_check, dice2_check, dice3_check, dice4_check, dice5_check]
for i in range(len(dice_re rolls)):
    if i in range(dice_re rolls):
        dice_re rolls.remove(0)
    if len(dice_re rolls) == 0:
        result = "You finish with " + hand(dice)
        hand_output.set(result)
    else:
        roll_number = len(dice_re rolls)
        number_re rolls = roll(roll_num ber)
        dice_changes = range(len(dice_ re rolls))
        iterations = 0
        while iterations < roll_number:
            iterations = iterations + 1
            dice_changes[iterations-1] = number_re rolls[iterations-1]
        iterations = 0
        while iterations < roll_number:
            iterations = iterations + 1
            replacement = number_ re rolls[iterations-1]
            dice[iterations-1] = replacement
        changes[iterations-1] = replacement
        dice.sort()
        new_dice_list = [0,0,0,0,0]
        for i in range(len(dice)):
            new_dice_list[i] = names[dice[i]]
        final_dice = " ".join(new_dice_ list)
        dice_output.set(final_dice)
        final_result = "You finish with " + hand(dice)
        hand_output.set(final_result)

def reset_game():
    global dice
    dice = roll(5)
    dice.sort()
    for i in range(len(dice)):
        empty_dice[i] = names[dice[i]]
    first_dice = " ".join(empty_dice)
    dice_output.set(first_dice)
    result = "You have " + hand(dice)
    hand_output.set(result)

if __name__ == '__main__':
    gui()
```

