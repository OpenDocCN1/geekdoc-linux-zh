

## Python 基础

11 result 函数在此任务中仅接受 player 和 computer 这两个变量，因此我们将其设为 result(player, computer)。我们从倒计时开始显示结果。打印的数字不言自明，但我们也加入了从 time 模块导入的 sleep。sleep 会使代码的执行暂停括号中指定的秒数。我们在每次倒计时之间设置了 1 秒的暂停，然后在显示结果后暂停半秒。

12 要打印出电脑出的拳，我们使用 string.format()。打印文本中的 {0} 就是我们插入手势的位置，该手势之前已定义为数字。使用 names[computer]，我们告诉代码从之前设置的 names 中查找该手势的文本版本名称，然后将其插入到 {0} 的位置。

13 在这里我们只是调用之前设置的分数。使用 global 函数可以让变量在变量之外被更改并使用，尤其是在我们向其中一个分数追加数字之后。

```
def result(player, computer):
    print "1..."
    time.sleep(1)
    print "2..."
    time.sleep(1)
    print "3!"
    time.sleep(0.5)
print "Computer threw {0}!".format(names[computer])
global player_score, computer_score
if player == computer:
    print "Tie game."
else:
    if rules[player] == computer:
        print "Your victory has been assured."
        player_score += 1
    else:
        print "The computer laughs as you realise you have been defeated."
        computer_score += 1
```

14 我们检查结果的方式基本上是通过排除法进行的。我们的第一个检查是看玩家和电脑使用的手势是否相同，这是最简单的一部分。我们将其放在 if 语句中，这样如果为真，这段代码就到此结束。它会打印平局信息，然后返回 game 函数进行下一步。

15 如果不是平局，我们需要继续检查，因为仍可能是胜利或失败。在 else 中，我们开始另一个 if 语句。这里，我们使用之前 rules 列表来查看玩家手势的失败手势是否与电脑的手势相同。如果是这种情况，我们打印相应的信息，并将 1 加到之前的 player_score 变量上。

16 如果进行到这一步，玩家就输了。我们打印失败信息，给电脑加一分，然后立即结束 result 函数，返回 game 函数。

![](img/3b256f430f51c98f1315671f6e4eec19_29_0.png)

17 game 的下一部分调用了 play_again 函数。与 move 函数类似，我们有人工输入，通过 raw_input 向玩家询问是否想再次游戏，文本消息中附带简单的 'y/n' 提示，以期获得预期的响应。

18 给用户提供 y/n 选项如我们所做的一样，应该期望得到相应的响应。if 语句检查是否输入了我们定义的任何肯定响应。由于 Python 不区分大小写，我们确保它同时接受 y 和 Y。如果是这种情况，它会向 game 返回一个肯定响应，从而重新开始游戏。

19 如果我们没有得到预期的响应，我们将假设玩家不想再玩了。我们会打印一条再见信息，这将结束此函数。这也会导致 game 函数进入下一部分而不重新启动。

```
def play_again():
    answer = raw_input("Would you like to play again? y/n: ")
    if answer in ("y", "Y", "yes", "Yes", "of course!"):
        return answer
    else:
        print "Thank you very much for playing our game. See you next time!"
```

```
def scores():
    global player_score, computer_score
    print "HIGH SCORES"
    print "Player: ", player_score
    print "Computer: ", computer_score
```

```
if __name__ == '__main__':
    start()
```

![](img/3b256f430f51c98f1315671f6e4eec19_30_0.png)

## ELIF

IF 还有 ELIF（elseif）运算符，可用于代替我们使用的第二个 IF 语句。通常用于保持代码整洁，但执行相同的功能。

20 回到 start 函数，game 结束后我们进入结果部分。此部分调用 scores，它们是整数，然后在玩家名称后分别打印它们。就玩家而言，这是脚本的结尾。目前，代码不会永久保存分数，但你可以让 Python 将其写入文件以保留。

21 最后部分允许脚本以两种方式使用。首先，我们可以在命令行中执行它，它就能正常工作。其次，我们可以将它导入到另一个 Python 脚本中，也许你想将其作为游戏添加到集合中。这样，在被导入时它不会执行代码。

