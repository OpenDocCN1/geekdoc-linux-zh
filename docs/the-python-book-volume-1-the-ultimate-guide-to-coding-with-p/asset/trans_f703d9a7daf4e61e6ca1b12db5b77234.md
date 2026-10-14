

## Continuation

这段代码仍然是我们在上一页开始的游戏函数的一部分，因此如果您没有使用 IDE，请确保缩进对齐。如果您计划拆分这段代码，我们建议从单词选择和结果开始。

```
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

11 如果我们发现这是一个可接受的新字母，我们首先要做的就是将其添加到已尝试字母的列表中。这是通过简单地将字符串拼接在一起完成的。然后我们使用 find 命令在单词字符串中搜索输入的字母，它会返回该字母在字符串中的位置编号。如果找不到该字母，它会返回 -1 值，我们在下一个 if 语句中使用它来检查 first_index 变量是否为 -1，如果是，则将 letters_wrong 的数量加一，然后打印一条消息告知玩家这是错误的猜测。

12 如果我们进行到这一步并且字母不是错误的，那么我们只能假设它是正确的。通过这种简单的排除过程，我们首先打印一条消息告知玩家他们成功了，然后进行记录。

13 我们在这里启动一个小循环，以便用我们添加的正确字母更新线索。我们使用 range 函数通过使用 word_length 变量来告诉代码我们希望对线索进行迭代的次数。然后我们检查单词中哪个字母被正确猜中，并将线索的特定部分更改为该字母，以便可以为玩家打印出来，并供我们检查游戏是否结束。

14 我们通过告知玩家如果他们没有输入受支持的输入则需重新选择来结束原始的 if 语句。在进入下一轮选择之前，我们通过调用与已进行的错误猜测次数相对应的列表中的图形来打印当前状态的吊人图形。然后我们打印线索当前的外观，每个字符之间有一个空格，然后打印已进行的猜测次数。

15 在这里我们再次检查游戏是否结束，首先将 letters_wrong 与 tries 的次数进行比较。如果为真，我们打印游戏结束的消息并揭示隐藏单词的谜底。我们增加电脑的分数并跳出循环。下一个循环检查完整线索的连接是否与原始单词相同——如果是这种情况，我们打印获胜消息、完整单词并在跳出循环之前为玩家分数加一分。这也可以使用 if 和 elif 来完成，以避免使用 break。

```
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

16 我们通过再次调用 return 来结束整个游戏函数循环，我们将在其完成后将其一路传递回 start 函数。

17 人类输入函数首先打印出一个 raw_input 消息。一旦玩家输入字母，函数就会对其进行解析以供其余代码使用。首先，使用 strip 来删除输入中任何多余的空白，因为我们没有为其提供额外参数。然后我们将其转换为小写字母，因为 Python 将无法正确比较大写字符与小写字符。我们然后为记录打印选择并将其返回到游戏函数。

18 游戏函数的最后一部分是询问玩家是否希望再次尝试。play_again 函数使用简单消息获取人类输入，然后分析输入以便知道要返回什么。

19 给用户提供 y/n 选项如我们所做，应该期望得到相应的回应。if 语句检查是否输入了我们定义的任何肯定回应。由于 Python 不区分大小写，我们确保它接受 y 和 Y。如果是这种情况，它会向 game 返回肯定回应，从而再次启动它。

20 如果我们没有得到预期的回应，我们将假设玩家不想再次玩。我们将打印再见消息，这将结束此函数。这也将导致 start 函数进入下一部分而不是重新启动。

21 回到 start 函数，在游戏结束后我们进入结果部分。此部分相当简单——它调用 scores，这些是整数，然后在玩家名称之后分别打印它们。就玩家而言，这是脚本的结尾。目前，代码不会永久保存分数，但您可以让 Python 将其写入文件，如果您愿意的话。

22 代码的最后一部分允许脚本以两种方式使用。首先，我们可以在命令行中执行它，它就可以正常工作。其次，我们可以将它导入到另一个 Python 脚本中，也许如果您想将其作为游戏添加到集合中。这样，在导入时它不会执行代码。

## Homework

现在您已经完成了代码，为什么不做自己的更改呢？增加单词数量；创建不同的、可选择的单词类别；甚至让人们猜测完整单词。您可以在当前代码和上个月的教程中找到完成这一切所需的工具。

