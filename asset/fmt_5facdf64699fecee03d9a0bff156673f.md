
`print("3")`

`time.sleep(0.5)`

```python

print("{}".format(names[computer]))

```

```python

global player_score, computer_score

```

检查是一个排除法的过程。我们的第一个检查是看玩家和电脑是否使用了相同的值，这是简单的部分。如果放入 `if` 中且结果为假，那么我们就移动到 `if` 结束的另一个部分。在这里，它打印我们的消息并返回游戏进行下一步。

```python

if player == computer:

    print("Tie game.")

```

```python

if rules[player]:

    print("Your victory has been assured.")

    player_score += 1

```

```python

print("The computer laughs as you realise you have been defeated.")

computer_score += 1

```

如果为假，我们需要继续检查，因为仍然可能是获胜或失败。在这里，我们使用之前定义的全局 `global` 变量来判断输给玩家的移动是否意味着游戏结束。如果是那样，我们会再次打印，并对之前的 `player_score` 变量加 1。

如果我们运行到这一步，说明玩家输了。我们打印失败信息，给电脑加一分，并立即返回 `result` 函数，回到游戏。

![](img/516df994db593237169e2aff6d3e6840_35_0.png)

*Python Shell

File Edit Debug Options Windows Help

Python 2.7.8 (default, Sep 26 2012, 21:51:14)

[GCC] 2.7.8 on linux

Type "copyright", "credits" or "license" for more information.

RESTART ==========================

>>> Let's play a game of Rock, Paper, Scissors.

```

```python

Rock

Paper = 2

Scissors = 3

Make = 5

>>> I didn't understand that. Please 1, 2, or 3.

>>> Rock

Paper = 2

Scissors = 3

Make = 5

>>> Make = 1

...

2...

3!

Computer threw Rock!

Tie game.

```

代码运行

游戏的下一部分调用了 `a_play_again`。就像我们有的人工输入函数一样，通过 `raw_input` 文本消息询问玩家是否想玩再次，这种 y/n 建议试图引导预期的响应。

提供像 y/n 这样的选项应该期望得到相应的响应。`if` 语句检查我们定义的任何响应是否被回答。由于 Python 区分大小写，请确保它同时接受 `y` 和 `Y`。如果是这种情况下，它将向游戏返回一个正向响应，游戏将重新开始。

如果我们没有得到预期的响应，我们将假设玩家不想再玩了。一条告别消息将结束此函数。这将导致游戏函数移动到下一个部分而不是重启。

```python

def play_again():

    answer = raw_input("Would you like to play again? y/n: ")

    if answer in ("y", "Y", "yes", "Of course!"):

        return answer

    else:

        print("Thank you very much for playing our game. See you next time!")

```

```python

def scores():

    global player_score, computer_score

    print("HIGH SCORES")

    print("Player:", player_score)

    print("Computer:", computer_score)

```

```python

if __name__ == '__main__':

    start()

```

![](img/516df994db593237169e2aff6d3e6840_36_0.png)

## ELIF

`IF` 也有 `ELIF(elif)` 运算符，它可以替代我们使用的第二个 `IF` 语句。它也用于保持代码整洁，但执行相同的功能。

回到开始，游戏结束后我们移动到结果部分。这部分调用 `scores` 函数，然后打印所有玩家的名字。出于清晰性考虑，这并不是脚本的结束。如果你想保留，除非 Python 将其写入文件，否则代码不会保存分数。

最后部分可以通过两种方式使用。首先，我们在命令行中执行它，它将正常工作。其次，我们可以将其导入到另一个脚本中。

# Python 基础

我看到 ASCII
这里是我们用于吊人游戏（Hangman）图形的七个阶段的特写。如果你愿意，可以更改它们，但请确保引号处于正确的位置，这样艺术图形就会被视为一个要打印的文本字符串。

## 规则
尽管我们将部分规则移动到了 `gamer` 函数，但你始终可以将它们放回来，并通过全局变量调用它们，就像我们处理分数一样。对于单词，你也可以创建一个单独的文件并像导入 `random` 模块一样导入它们。

![](img/516df994db593237169e2aff6d3e6840_39_0.png)

```python

def hangedman(hangman):

    graphic = [

        """,```

```python

def start("Let's play a game of Linux Hangman")

    while game():

        pass

    scores()

```

01 我们开始使用这一行来输入解释器的路径。这允许我们在终端或 Python 特定的 IDE 之外运行程序。请注意，虽然在此特定脚本中使用了 Python 3，但它在大多数 Linux 系统上默认安装的，因此将确保兼容性。

仅存在于该函数内部。代码根据回合的结果为计算机或玩家增加一分。

02 我们这次导入 `random` 模块的方式略有不同，只导入 `random` 中的函数而不是模块本身。这允许我们在不使用 `random.` 前缀的情况下使用这些函数。星号 `*` 导入 `random` 中的所有函数，尽管你也可以为 `random` 的任何函数使用特定名称。我们将在整个脚本中使用 `random` 函数。

04 我们的简单图形由 ASCII 吊人阶段组成。我们在此函数中将单独的字符串存储在列表中，这样我们就可以通过向它传递数字来调用它们。总共有七幅图，我们在调用它们时使用 `print` 命令来处理吊人的选择和显示，第一个图形在给出第一个字母后打印。

03 非常简单地，这创建了一个可以在整个代码中使用的变量，用于跟踪分数。我们现在将其初始化为零，使其存在；如果我们在函数中定义它，它就会

05 这里我们定义了代码的实际开始，使用了 `start` 函数。它很简单，问候玩家然后启动一个循环，让我们能够根据意愿多次玩游戏。`pass` 语句允许我们在完成后结束循环，并让代码执行所需的许多其他任务。

```python

def game():

    dictionary = ["gnu","kernel","linux","mageia","penguin","ubuntu"]

    word = choice(dictionary)

    word_length = len(word)

    clue = word * ["_"]

    tries = 6

    letters_tried = ""

    guesses = 0

    letters_right = 0

    letters_wrong = 0

    global computer_score, player_score

```

```python

while (",".join(clue) != word):

    letter=guess().lower()

    if len(letter) == 1 and letter.isalpha():

        if letters_tried.find(letter) != -1:

            print("you've already picked", letter)
```
