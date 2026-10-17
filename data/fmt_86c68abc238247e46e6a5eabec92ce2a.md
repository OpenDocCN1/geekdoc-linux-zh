
```python
def start():
    print("Let's play a game of Linux Hangman.")
    while game():
        pass
    scores()

def game():
    dictionary = ["gnu","kernel","linux","mageia","penguin","ubuntu"]
    word = choice(dictionary)
    word_length = len(word)
    clue = word_length * ["_"]
    tries = 6
    letters_tried = ""
    guesses = 0
    letters_right = 0
    letters_wrong = 0
    global computer_score, player_score

    while (letters_wrong != tries) and ("".join(clue) != word):
        letter=guess_letter()
        if len(letter) == 1 and letter.isalpha():
            if letters_tried.find(letter) != -1:
                print("You've already picked", letter)
            else:
                letters_tried = letters_tried + letter
                first_index=word.find(letter)
                if first_index != -1:
                    letters_right +=1
                    print("Sorry",letter,"isn't what we're looking for.")
                else:
                    print("Congratulations,",letter,"is correct.")
                    for i in range(word.length):
                        if letter == word[i]:
                            clue[i] = letter
        else:
            print("Choose another.")

        hangman(letters_wrong)
        print(" ".join(clue))
        print("Guesses: ", letters_tried)

        if letters_wrong == tries:
            print("Game Over.")
            print("The word was",word)
            computer_score += 1
            break
        if "".join(clue) == word:
            print("You Win!")
            print("The word was",word)
            player_score += 1
            break
    return play_again()

def guess_letter():
    print(" ")
    letter = raw_input("Take a guess at our mystery word:")
    letter.strip()
    letter.lower()
    print(" ")
    return letter

def play_again():
    answer = raw_input("Would you like to play again? y/n: ")
    if answer in ("Y","y","yes","Yes","Of course!"):
        return answer
    else:
        print("Thank you very much for playing our game. See you next time!")

def scores():
    global player_score, computer_score
    print("HIGH SCORES")
    print("Player: ", player_score)
    print("Computer: ", computer_score)

if __name__ == "__main__":
    start()
```

### 代码高亮

IDLE 会自动高亮代码，让你的阅读更轻松。它还允许你在 IDLE 的“偏好设置”中更改这些颜色和高亮，以防你有色盲，或者只是习惯不同的配色方案。

# 我看到 ASCII

以下是我们用于 Hangman 图形的七个阶段的特写。你可以自行更改它们，但你需要确保引号都放在正确的位置，这样艺术作品才会被视为要打印出的文本字符串。

![](img/3b256f430f51c98f1315671f6e4eec19_33_0.png)

```python
#!/usr/bin/env python2

from random import *

player_score = 0

computer_score = 0

def hangman(hangman):

    graphic = [

        """

             +------+ 

             |      |

             |

             |

             |

             |

             =============

        """,

        """

        ]
```

### 规则

虽然我们本月已将部分规则移至 `game` 函数，但你始终可以将它们放回此处，并使用全局变量调用它们，就像我们对分数所做的那样。对于单词，你也可以创建一个单独的文件并像导入 `random` 模块一样导入它们。

01 我们首先使用这一行来输入 Python 解释器的路径。这使我们能够在终端内或在 IDLE 等 Python 特定 IDE 之外运行程序。请注意，我们在此脚本中使用的是 Python 2，因为它已在大多数 Linux 系统上默认安装，因此将确保兼容性。

02 我们这次以略有不同的方式导入 `random` 模块，导入的是 `random` 中的实际函数名称，而不是仅导入模块本身。这使我们能够在不使用 `random.function` 之类语法的情况下使用这些函数。星号导入 `random` 中的所有函数，尽管你可以将其替换为 `random` 的任何函数的特定名称。我们将使用 `random` 函数为玩家选择一个单词进行猜测。

03 非常简单，这创建了一个变量，可在整个代码中使用以跟踪分数。我们现在需要将其设为零，以便它存在；否则如果我们在函数中定义它，它将仅存在于该函数内部。代码根据回合结果为计算机或玩家增加一分。

04 我们的简单图形由一系列 ASCII 绞刑架阶段组成。我们将这些图形存储在一个函数中作为单独字符串对象的列表，以便我们可以传递错误猜测次数来调用它们。共有七个图形，如同纸笔版本一样。我们还将 `print` 命令包含在函数中，因此当它被调用时，它将完全处理吊人图形的选择和显示，第一个图形将在猜测第一个字母后打印。

05 在这里我们定义了代码的实际开始部分，使用我们命名的 `start` 函数。它很简单，向玩家打印问候语，然后启动一个 `while` 循环，允许我们尽可能多次地继续玩游戏。`pass` 语句允许 `while` 循环在我们完成后停止，并且可用于执行许多操作。
