
代码的最后部分允许主窗口使用该脚本，并且当在命令行或 shell 中使用时，也允许其独立运行。你需要进行一些修改才能使其独立运行，例如将其设置为 `mainloop` 而不是 `Toplevel` 窗口。然而，它可以从两者正常运行，而不需要从主界面启动。

## 为简单的 Python 游戏添加图形

通过为绞刑架和扑克骰子代码添加图形界面，完成你的三款游戏系列。

## 资源

- Python 2: `www.python.org/download`
- IDLE: `www.python.org/idle`

1. **导入**

   这里我们进行了一些次要的设置，包括获取帮助我们创建简单图形界面的 Tkinter 模块。

2. **单词**

   我们将确定要猜单词的变量保留在这里，以便可以在代码中的任何地方轻松访问。

3. **函数**

   像上次一样，我们将原始代码的大部分放入一个新函数中，`gui`。

4. **分析**

   我们在继续其余代码之前选择并分析单词。

5. **图形**

   `hangedman` 函数几乎未变，尽管有了新代码来在界面上显示我们的 ASCII 图形。

6. **猜测**

   我们检查错误的次数，并调用 `guess_letter` 函数来检查输入的字母。

我们现在已经为之前制作的三个 Python 游戏创建了一个简单的选择器。该界面能够启动我们的石头、剪刀、布游戏的图形用户界面（GUI），并在终端中运行另外两个游戏。现在，我们要将绞刑架和扑克骰子代码转换为以类似于石头、剪刀、布的方式工作。绞刑架的技巧在于允许不同类型的输入，即文本，以及进行多轮游戏的能力。Tkinter 允许文本输入，我们在完整玩游戏中对 `while` 循环的依赖要少得多。扑克骰子需要保持骰子分析代码，以及使用复选框更改特定骰子的选项。

我们将修改大量原始代码以适应新的图形方案。这主要涉及剪切特定部分并让 Tkinter 特定代码自行处理这些。这些页面的代码列表包含修改后的代码 - 我们将在接下来的页面中讨论图形部分。

## 绞刑架代码列表

```python
from Tkinter import *
from ttk import *
from random import *

word = ""
word_length = 0
cue = []

def gui():
    global word, word_length, cue
    dictionary = ["gnu", "kernel", "linux", "mageia", "penguin", "ubuntu"]
    word = choice(dictionary)
    word_length = len(word)
    cue = word_length * ["-"]
    tries = 6

    def hangedman(hangman):
        graphic = [
            '''
            ----------
                |
                O
               -|-
                /\\
            ==========
            '''
        ]
        graphic_set = graphic[hangman]
        hw_graphic.set(graphic_set)

    def game():
        letters_wrong = int(incorrect_guesses.get())
        letter = guess_letter()
        first_index = word.find(letter)
        if first_index == -1:
            letters_wrong += 1
            incorrect_guesses.set(str(letters_wrong))
        else:
            for i in range(word_length):
                if letter == word[i]:
                    cue[i] = letter
            hangedman(letters_wrong)
            cue_set = " ".join(cue)
            word_output.set(cue_set)
            if letters_wrong == tries:
                result_text = "Game Over. The word was " + word
                result_score.set(result_text)
                new_score = int(computer_score.get())
                new_score += 1
                computer_score.set(str(new_score))
            if " ".join(cue) == word:
                result_text = "You Win! The word was " + word
                result_score.set(result_text)
                new_score = int(player_score.get())
                new_score += 1
                player_score.set(str(new_score))

    def guess_letter():
        letter = letter_guess.get()
        letter = letter.strip()
        letter = letter.lower()
        return letter

    def reset_game():
        global word, word_length, cue
        incorrect_guesses.set("0")
        hangedman(0)
        result_set.set("")
        letter_guess.set("")
        word = choice(dictionary)
        word_length = len(word)
        cue = word_length * ["-"]
        new_cue = " ".join(cue)
        word_output.set(new_cue)

if __name__ == "__main__":
    gui()
```

## Python 基础

1. **更多导入**

   我们添加了使 Tkinter 工作所需的新导入模块，其余保持不变。

2. **骰子列表**

   持有骰子的列表保留在主函数之外，以便可以在任何地方访问。

3. **滚动**

   滚动函数也是如此。它并不特别需要在 `gui` 函数内部。

4. **决定**

   我们将在稍后创建的图形代码中的复选框将为我们提供可以分析的代码数字。我们检索这些数字并检查它们以确定用户希望重新滚动哪些骰子。

5. **手牌**

   最后，我们的手牌分析函数是保留在 `gui` 函数之外的原始代码的最后一部分。这两个函数都将必要的细节传回链条，然后添加到新界面的新图形元素中。

6. **无骰子**

   如果没有选择任何骰子重新滚动，手牌输出将更改以显示最终消息。

7. **重新滚动**

   这部分与之前几乎相同 – 滚动一组新的骰子，然后像之前一样插入骰子列表中，然后重新排序以简化手牌分析。

8. **更多函数**

   新的 `gui` 函数是扑克骰子代码的主要变化，和之前一样，包括 Tkinter 元素和原始代码的其他部分。

9. **游戏开始**

   一个简单的函数，我们可以用它来激活骰子的重新滚动。

10. **新手牌**

    新的骰子被命名、分析，然后一切设置好以便 `gui` 显示最终结果。

11. **重置**

    与绞刑架代码一样，我们有一个函数来重置所有变量，允许你重新开始游戏。

## 扑克骰子代码列表
