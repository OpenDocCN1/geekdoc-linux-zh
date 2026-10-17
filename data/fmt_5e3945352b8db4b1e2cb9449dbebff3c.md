
```python
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
        if len(letter)==1 and letter.isalpha():
            if letters_tried.find(letter) != -1:
                print "You've already picked", letter
```

如果愿意，还可以执行其他任务。如果我们停止玩游戏，则会调用 `score` 函数——我们将在讲到它时介绍它会做什么。

它正在检查与已玩过的字母。最后，我们为已进行的猜测次数、正确字母数和错误字母数创建空变量，以使代码稍微容易一些。我们还在此处导入全局分数。

### 06

我们这次将大部分游戏代码放在 `game` 函数中，因为没有太多需要拆分的内容。如果你愿意，可以进一步拆分它，使用上期代码的风格，如果这能使代码更清晰或帮助你更好地理解构建块。

### 09

我们启动一个 `while` 循环来执行玩家选择并检查游戏状态。此循环会一直持续到玩家获胜或失败为止。它首先通过查看 `letters_wrong` 是否不等于 `tries` 来检查是否已用完所有尝试次数。由于每次尝试只会为 wrong 增加一分，因此它永远不会超过六。随后它将 `clue` 串联起来并查看它是否与计算机选择的单词相同。如果这两个语句都为真，则进入下一回合。

### 07

前四行快速设置玩家要猜测的单词。我们在这里有一个小单词列表。然而，这些单词可以通过 HTML 导入或扩展。`choice` 用于从列表中选择一个随机元素，该元素来自我们导入的 `random` 模块。最后，我们确定要猜测的单词字符串的长度，然后使用该长度创建 `clue` 变量，其中包含相应数量的下划线。这用于在你通过猜测逐步构建单词时显示单词。

### 10

我们调用用于输入字母的函数并将其赋给变量 `letter`。我们首先通过 `len(letter)` 确保它只有一个字母，然后使用 `isalpha` 查看它是否是 26 个字母表中的一个。如果满足这些条件，我们就开始一个新的 `if` 语句以确保它是新的猜测，并告知玩家如果它已被选择过以便他们可以重新开始。如果所有这些都可接受，我们就进入代码的下一部分，看看它是否是正确的猜测。

### 08

我们开始设置规则和在游戏过程中跟踪的各个变量。在吊人完全绘制或在我们的例子中显示之前，只能有六次错误猜测，因此我们将 `tries` 变量设为六。我们将通过 `letters_tried` 跟踪字母，以确保不仅玩家知道，而且代码在

### 缩进

虽然 `IDLE` 会跟踪代码中的缩进，但如果你使用文本编辑器编写一些 Python，你必须确保正确使用它们。Python 对缩进是否正确使用非常敏感，而且这也有助于可读性。

![](img/3b256f430f51c98f1315671f6e4eec19_34_0.png)

### Continuation

这段代码仍然是我们在上一页开始的 `game` 函数的一部分，因此如果您没有使用 IDE，请确保缩进对齐。如果您计划拆分这段代码，我们建议从单词选择和结果开始。

```python
else:
    letters_tried = letters_tried + letter
    first_index=word.find(letter)
    if first_index == -1:
        letters_wrong +=1
        print "Sorry,",letter,"isn't what we're looking for."
    else:
        print "Congratulations,",letter,"is correct."
        for i in range(word_length):
            if letter == word[i]:
                clue[i] = letter
else:
    print "Choose another."

hangedman(letters_wrong)
print "".join(clue)
print "Guesses: ", letters_tried

if letters_wrong == tries:
    print "Game Over."
    print "The word was",word
    computer_score += 1
    break
if "".join(clue) == word:
    print "You Win!"
    print "The word was",word
    player_score += 1
    break
return play_again()
```

11 如果我们发现这是一个可接受的新字母，我们首先要做的就是将其添加到已尝试字母的列表中。这是通过简单地将字符串拼接在一起完成的。然后我们使用 `find` 命令在单词字符串中搜索输入的字母，它会返回该字母在字符串中的位置编号。如果找不到该字母，它会返回 `-1` 值，我们在下一个 `if` 语句中使用它来检查 `first_index` 变量是否为 `-1`，如果是，则将 `letters_wrong` 的数量加一，然后打印一条消息告知玩家这是错误的猜测。

12 如果我们进行到这一步并且字母不是错误的，那么我们只能假设它是正确的。通过这种简单的排除过程，我们首先打印一条消息告知玩家他们成功了，然后进行记录。

13 我们在这里启动一个小循环，以便用我们添加的正确字母更新线索。我们使用 `range` 函数通过使用 `word_length` 变量来告诉代码我们希望对线索进行迭代的次数。然后我们检查单词中哪个字母被正确猜中，并将线索的特定部分更改为该字母，以便可以为玩家打印出来，并供我们检查游戏是否结束。

14 我们通过告知玩家如果他们没有输入受支持的输入则需重新选择来结束原始的 `if` 语句。在进入下一轮选择之前，我们通过调用与已进行的错误猜测次数相对应的列表中的图形来打印当前状态的吊人图形。然后我们打印线索当前的外观，每个字符之间有一个空格，然后打印已进行的猜测次数。

15 在这里我们再次检查游戏是否结束，首先将 `letters_wrong` 与 `tries` 的次数进行比较。如果为真，我们打印游戏结束的消息并揭示隐藏单词的谜底。我们增加电脑的分数并跳出循环。下一个循环检查完整线索的连接是否与原始单词相同——如果是这种情况，我们打印获胜消息、完整单词并在跳出循环之前为玩家分数加一分。这也可以使用 `if` 和 `elif` 来完成，以避免使用 `break`。

```python
def guess_letter():
    print
    letter = raw_input("Take a guess at our mystery word:")
    letter.strip()
    letter.lower()
    print
    return letter

def play_again():
    answer = raw_input("Would you like to play again? y/n: ")
    if answer in ("y", "Y", "yes", "Yes", "Of course!"):
        return answer
    else:
        print "Thank you very much for playing our game. See you next time!"

def scores():
    global player_score, computer_score
    print "HIGH SCORES"
    print "Player: ", player_score
    print "Computer: ", computer_score

if __name__ == '__main__':
    start()
```

16 我们通过再次调用 `return` 来结束整个游戏函数循环，我们将在其完成后将其一路传递回 `start` 函数。
