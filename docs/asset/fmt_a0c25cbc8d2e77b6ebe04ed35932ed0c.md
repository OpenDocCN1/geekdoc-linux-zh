
```
for i in range(len(dice_rerolls)):
    if dice_rerolls[i] == 0:
        dice_rerolls.remove(0)
    if len(dice_rerolls) == 0:
        result = "You finish with " + hand(dice)
        hand_output.set(result)
    else:
        roll_number = len(dice_rerolls)
        number_rerolls = roll(roll_number)
        dice_changes = range(len(dice_rerolls))
        iterations = 0
        while iterations < roll_number:
            iterations += 1
            dice_changes[iterations-1] = number_rerolls[iterations-1]
        iterations = 0
        while iterations < roll_number:
            iterations += 1
            replacement = number_rerolls[iterations-1]
            dice[dice_changes[iterations-1]] = replacement
        dice.sort()
        new_dice_list = [0,0,0,0]
        for i in range(len(dice)):
            new_dice_list[i] = names[dice[i]]
        final_output.set(" ".join(new_dice_list))
        dice_output.set(final_output)
        final_result = "You finish with " + hand(dice)
        hand_output.set(final_result)

def reset_game():
    global dice
    dice = roll(5)
    dice.sort()
    empty_dice = [0,0,0,0]
    for i in range(len(dice)):
        empty_dice[i] = names[dice[i]]
    first_dice = " ".join(empty_dice)
    dice_output.set(first_dice)
    result = "You have a " + hand(dice)
    hand_output.set(result)

pd_window = Toplevel()
pd_window.title("Power Dice")
pd_window.geometry("300x300")
empty_dice = [0,0,0,0]
for i in range(len(dice)):
    empty_dice[i] = names[dice[i]]
first_dice = " ".join(empty_dice)
dice_output.set(first_dice)
hand_output.set(" ")
hand_output.set(result)
dice1 = IntVar()
dice2 = IntVar()
dice3 = IntVar()
dice4 = IntVar()
dice5 = IntVar()
result_set = StringVar()
player_score = IntVar()
computer_score = IntVar()

pd_frame = Frame(pd_window, padding = "3 3 12 12", width = 300)
pd_frame = Frame(pd_window, row = 8, sticky=W,N,E,S)
pd_frame.columnconfigure(6, weight=1)
pd_frame.rowconfigure(8,weight=1)
Label(pd_frame, text=dice1, grid(column=3, row = 1))
Label(pd_frame, textvariable = dice_output, grid(column=3, row = 2))
Label(pd_frame, textvariable = hand_output, grid(column=3, row = 3))

Label(pd_frame, text="Dice to Reroll(?)", grid(column=3, row = 4))
reroll1 = Checkbutton(pd_frame, text = "1", variable = dice1, onvalue = 1, offvalue = 0) grid(column=2, row = 5)
reroll2 = Checkbutton(pd_frame, text = "2", variable = dice2, onvalue = 2, offvalue = 0) grid(column=2, row = 5)
reroll3 = Checkbutton(pd_frame, text = "3", variable = dice3, onvalue = 3, offvalue = 0) grid(column=2, row = 5)
reroll4 = Checkbutton(pd_frame, text = "4", variable = dice4, onvalue = 4, offvalue = 0) grid(column=2, row = 5)
reroll5 = Checkbutton(pd_frame, text = "5", variable = dice5, onvalue = 5, offvalue = 0) grid(column=2, row = 5)
pd_reroll_button = Button(pd_frame, text = "Reroll", command = e_game) grid(column = 3, row = 6)
replay_button = Button(pd_frame, text = "Reset", command = reset_game) grid(column = 3, row = 7)

if __name__ == "__main__":
    gui()
```

### 一个窗口

我们制作这些 `Tkinter` 界面的方式是让游戏在单独的窗口中启动。你也可以让它们都在一个窗口中运行，只需用不同的函数或类替换原始界面的标签和按钮即可。确保为游戏添加一个退出按钮，让你可以返回主页面。

# 使用 Python 为 Android 构建应用

掌握 `Kivy`，这款出色的跨平台应用框架，制作你的第一个 Android 应用...

![](img/3b256f430f51c98f1315671f6e4eec19_55_0.png)

这里我们已经为游戏绘制了所有简单的图形... 现在我们只需要让这些形状真正发挥作用！

`Kivy` 的优点在于我们可以朝多个方向发展，实现相当花哨的功能。但我们将直奔 `Kivy` 最酷的功能之一——它让你能够轻松在 Android 上运行程序。我们将首先展示如何制作一个新应用，这次是一个动态的 Breakout 风格游戏。然后我们就能直接将其编译成 Android APK，就像使用任何其他应用一样。

当然，一旦你掌握了基本技巧，你就不会局限于使用某种特定类型的应用，因为即使在 Android 上，你也可以使用你最喜欢的 Python 库来制作任何你喜欢的程序。

一旦你掌握了 `Kivy`，你的想象力就是唯一的限制。如果你对 `Kivy` 几乎一无所知，不用担心，我们不会假设你有任何预先的知识。只要你已经掌握了本书迄今为止的一些 Python 教程，并且对该语言有相当好的理解，就不应该有任何问题可以跟上。

在做任何其他事情之前，让我们先拼凑一个基本的 `Kivy` 应用（图 01）。我们已经预先导入了我们将使用的 widget 类型，这次只有三种：没有特殊行为的基本 `Widget`，上次使用的具有弹出行为的 `ModalView`，以及我们稍后会解释的 `FloatLayout`。`Kivy` 还有许多其他预建的 widget 用于创建 GUI，但这次我们将专注于使用 `Kivy` 的图形指令从头开始绘制整个 GUI。这些指令要么是用于创建形状的顶点指令（包括矩形、线条、网格等），要么是上下文图形更改（例如平移、旋转、缩放等），并且能够在屏幕上的任何位置和任何 widget 类型上绘制。
