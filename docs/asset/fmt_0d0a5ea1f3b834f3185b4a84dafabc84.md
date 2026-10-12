
```python
def hangman(number):
    numbers = range(7)
    dice = range(dice)
    while iterations < number:
        iterations += 1
```

### 3 掷骰

函数也是一样。它不需要在

```python
dice = [len(group)) for key, group in groupby(dice)]
dice.sort(reverse=True)
```

### 4 选择

复选框代码稍后创建，以便我们可以使用任意数量的数字。

### 5 手牌

最后，我们的分析函数是保留在外部的代码部分。

### 6 没有骰子

如果没有选择骰子进行重新掷，输出将更改为没有骰子。

### 7 重新掷

当一组骰子被重新掷时，这部分也是一样的，像之前一样插入列表，然后重新排序以完成

### 8 主

主函数在这里更改了`dice`游戏代码，因为它包含了`Tkinter`代码。

### 9 游戏开始

一个简单的函数，我们可以通过重置`dice`的`roll`来启动游戏。

### 10 新骰子

新`dice`被命名、添加，并设置好一切以便`gui`显示最终输出。

### 11 重置

和猜字游戏一样，我们有一个函数来重置所有变量，让你重新开始游戏。

```python
def game():
    global dice
    dice = roll(5)
    dice.sort()
    ten = 2
    jack = 3
    queen = 4
    king = 5
    ace = 6
    names = {"9": "9", "10": "10", "jack": "J", "queen": "Q", "king": "K", "ace": "A"}
    result = "You have " + hand(dice)
```

```python
def game():
    throws()

def throws():
```

```python
def reset_game():
    global dice
    dice = roll(len(dice))
    empty_dice = [names[:dice]]
    for i in range(len(dice)):
        first_dice = i.join(empty_dice)
        dice_output.set(dice)
        result = "You have " + hand(dice)
    hand_output.set(result)
```

# 教程

## Python 入学者：图形化游戏

### LinuxDeveloper

```python
#!/usr/bin/env python2
from tkinter import *
from ttk import *
from random import *

word = ""
word_length = 0
clue = "["

def gui():
    global word, word_length, clue
    dictionary = {"guu", "gner", "linux", "magelia", "penguin", "ubuntu"}
    word = choose(dictionary)
    word_length = len(word)
    clue = word[:-1]
    tries = 6

def hangman():
    graphic = [
        "------",
        "-----",
        "--|-",
        "--||",
        "*||",
        "*| /"
    ]
    graphic_set = graphic[hangman]
    hangman_graphic.set(graphic_set)

def guess(letter):
    global letters_wrong
    incorrect_guesses.add(letter)
    first_index = word.find(letter)
    if first_index == -1:
        letters_wrong += 1
        incorrect_guesses.set(letters_wrong)
    else:
        for i in range(word_length):
            if word[i] == letter:
                clue[i] = letter
                result.set("".join(clue))
                if letters_wrong == 6:
                    result = "Game Over. The word was " + word
                    result.set(result)
                    score = computer.score()
                    score += 1
                if letter not in word:
                    result = "You win! The word was " + word
                    result.set(result)
                    score += 1
                    player_score.set(score)
```

访问了代码中的所有点。`Python 2`不允许在嵌套函数中调用全局变量，而`Python 3`则可以拥有`gui`函数。

### 03 图形化函数

我们将工作代码放入`gui`函数中，以便从主界面激活。我们可以将吊挂游戏代码导入窗口界面，并仅在激活`gui`函数时运行它。

### 04 随机单词

我们通过`global`引入变量，以便在整个代码中修改它们，然后设置单词。与之前一样，使用`choice`从单词列表中随机选择项目，并显示线索。

### 05 吊挂游戏

这个吊挂游戏图形版的主要区别在于，它不是打印出来，而是在界面中显示。当函数被调用并选择时，它将设置界面变量来显示图形。

### 06 游戏开始

我们在此函数中输入的所有字母。为了做到这一点，我们通过从目前为止的错误猜测开始清理，以便设置的界面变量可以操作。如果不为空，则插入字段并使用代码进行清理。

### 07 检查字母

这部分代码再次保持不变 - 将行与单词进行比较，以找到是否匹配其中一个字母。然后它会将错误猜测加`1`，或者更新变量将字母添加到正确的位置。

### 08 更新界面

这些行设置了本轮的图形，将当前分数连接为字符串并设置在界面以便读取。

### 09 更新分数

正如所示，我们检查玩家是否胜利或失败。如果发生，将显示一条消息来表示此，并使用`set`更新胜负。

### 01 前几行

当我们开始每个程序时，使用允许在命令行运行的代码，通过遵循以下方法：随机，以确定要使用的单词：`Tkinter`用于大部分图形化代码以及...

### 02 全局变量

我们将这些变量保留在`gui`函数之外，以便在代码的任何点都可以访问它们。

# Python 入学者：图形化游戏

为吊挂游戏和扑克骰子创建一个图形化界面

## 教程

```python
def guess_letter():
    letter = letter_guess.get()
    letter = letter.strip()
    letter = letter.lower()
    return letter

def reset_game():
    global word, word_length, incorrect_guesses
    incorrect_guesses.set(0)
    result_set.set("")
    word = choice(dictionary)
    word_length = len(word)
    clue = " " * word_length
    new_clue = list(clue)
    output.set(new_clue)
```
