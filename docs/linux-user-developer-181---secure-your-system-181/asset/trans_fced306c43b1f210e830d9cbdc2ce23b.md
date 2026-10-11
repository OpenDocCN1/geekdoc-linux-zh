

## 战舰游戏

### 第二部分：使用 Sense HAT 战舰号令海上

这是我们在树莓派上使用 Sense HAT 制作经典战舰游戏系列的最后一部分。

**Dan Aldred** 是一位树莓派爱好者、教师和程序员，他喜欢通过创建新的项目和黑客技巧来激励其他人开始学习。

- **树莓派**
  www.raspberrypi.org/products
- **Sense HAT**
  http://bit.ly/BattleshipSenseHAT

![](img/fb76008333fb7aef815b136f9f1afe5f_73_0.png)

在本教程的第一部分 [LJUD#180，教程，第74页] 中，你已经开始构建经典的战舰游戏，编码了诸如部署船只、发射鱼雷和保持分数累计等功能。在第二部分，你将首先安装一个小程序，该程序使你能够轻松创建动画并在 Sense HAT 的 LED 矩阵上播放。这些动画可用于介绍游戏、显示游戏结束消息或根据游戏需要在任何地方更新玩家。教程在完成游戏玩法的主要机制之前，会先设置部署游戏的代码。首先，通过一系列声音和口头宣布来介绍游戏，然后在显示屏上滚动播放一艘船的动画。接着，在游戏开始前创建一个从三到零的简单倒计时。该游戏利用了我们在第一部分创建的主函数。游戏结束后，我们将添加选择是否再次游玩的选项。如果你将摇杆向下移动，程序将播放告别声音，显示动画，然后你的游戏结束，程序关闭。向上移动摇杆，你可以选择再玩一轮，系统将创建一个新的随机布局。在这里观看完整游戏的实际演示：https://youtu.be/So1WAJHCac.

### 01 创建你自己的 8x8 动画

在 LED 矩阵上运行动画有一种简单的方法；这是一个出色的屏幕程序，使你可以实时操控 LED。你可以更改颜色，旋转并将动画导出为代码。首先安装 Python PNG 库，打开终端并输入 `sudo pip3 install png`；然后：

```bash
git clone https://github.com/jrobinson-uk/RP1_8x8GridDraw
```

安装完成后，进入 RPI 文件夹，输入 `cd RPi_8x8GridDraw`，然后输入 `python 8x8grid.py` 运行应用程序。

### 02 创建并导出你的动画

网格编辑器允许你从右侧的一系列颜色中进行选择。选择一种颜色，然后点击网格上 LED 的位置。选择“在 LED 上播放”以在 Sense HAT 的 LED 矩阵上显示该“像素”。使用“清空网格”按钮清除 LED，然后重新开始。使用“+”按钮添加新的“幻灯片”并构建你的动画。这可能是一个棘手的过程，因此值得事先做好计划。完成后，按下“导出为 py”按钮将动画导出为代码。这会将动画保存为 RPI 文件夹中的一个 Python 文件；它将命名为 **8x8animation.py**。你可以创建任意数量的动画；在这里我们将制作一个介绍和一个游戏结束屏幕。

### 03 添加分数

本教程现在继续从上 tutorial 第一部分编写的程序开始。删除从 `!` 到 Game`'` 注释以下的所有内容 – 这些行是添加用来测试你的代码的。现在你可以添加剩余的代码。在与相同级别的缩进中，添加播放'score'.MP3'的代码。这会宣布你的分数，第一行。使用 Pygame 播放 MP3 文件，第二行；添加一个短暂的暂停以留出时间让声音文件播放，第三行。

```python
pygame.mixer.music.load("sounds/yourScore1.mp3")
pygame.mixer.music.play()
time.sleep(1)
```

### 04 显示你的分数

保持相同的缩进级别，添加一行代码以将你的分数作为消息在 LED 矩阵上滚动显示。然而，首先分数需要转换为字符串才能显示。你可以通过更改方括号内的三个值来编辑消息的颜色，最大值可为 255，第一行。然后打印出剩余待摧毁的船只数量，第二行。

```python
sense.show_message(str(score), text_colour=[0, 200, 255])
print("There are", number_of_ships, "ships left")
```

### 05 你做得怎么样？第一部分

现在程序检查你在游戏中表现如何。如果剩余船只数量为零，那么你就做得非常好，第一行。在第三行，一条合适的“做得好”消息在 LED 矩阵上滚动显示。添加一个合适的“获胜者”声音，例如号角声，第四行，然后播放它。记得添加一个小的延迟以便文件播放。

```python
# add a score
pygame.mixer.music.load("sounds/yourscore1.mp3")
pygame.mixer.music.play()
time.sleep(1)

sense.show_message(str(score), text_colour=[0, 200, 255])
print("There are", number_of_ships, "ships left")

if number_of_ships == 0:
    print("WELL DONE, TOP JOB") # ADD SOME ANIMATION
    sense.show_message("TOP JOB", text_colour=[0, 255, 255])
    pygame.mixer.music.load("sounds/winner.mp3") # add a sea sound
    pygame.mixer.music.play()
    time.sleep(3)
else:
    print("Better luck next time") # ADD SOME ANIMATION
    pygame.mixer.music.load("sounds/restime.mp3") # add a sea sound
    pygame.mixer.music.play()
```

### 06 你做得怎么样？第二部分

如果你没有击沉所有船只，那么你就没有赢得游戏，而是输了。你可以添加额外的条件来检查不同的数量，例如一半的船只。首先使用第二行的代码在 LED 矩阵上滚动消息。然后播放合适的失败者声音，第三行和第四行。

```python
else:
    print("better luck next time")
```

### 像素灵感

Johan Viet 有一些出色的且令人鼓舞的 8x8 像素艺术示例 ([http://bit.ly/8xBipixe](http://bit.ly/8xBipixe)lart)，其中包括一些著名角色，并将展示你可以用 64 个彩色像素创造什么。

```python
sense.show_message("BETTER LUCK NEXT\nTIME", text_colour=[0, 255, 255])
pygame.mixer.music.load("sounds/intro.mp3") # add a sea sound
nexttime.mp3" # add a sea sound
pygame.mixer.music.play()
```

![](img/fb76008333fb7aef815b136f9f1afe5f_75_1.png)

### 07 开始游戏

这就完成了所有的游戏机制，它们存储在名为 main() 的函数中 – 这段代码只有在调用 main() 时才会运行。然而，在此之前，让我们为游戏创建一个介绍。首先播放一个合适的声音，第一行。这个例子是波浪舒缓的声音。触发声音播放，第二行。在第三行，使用代码 `import intro_ship` 导入你在步骤 2 中创建的动画。这在声音播放时显示，从而为游戏创建一个美好的介绍。

```python
pygame.mixer.music.load("sounds/intro.mp3") # add a sea sound
pygame.mixer.music.play()
import intro_ship
```

### 08 开始游戏

在短动画结束后，我们向玩家宣布游戏开始。这使用了熟悉的 `sense.show_message` 代码在 LED 矩阵上滚动消息。这次，使用代码 `back_colour=[0, 0, 180]` 添加背景颜色，第一行。创建一个变量，第二行，将游戏状态设置为 True，意味着游戏正在进行中。接下来，检查游戏是否正在进行，第三行，并创建另一个名为 `play_again` 的变量，第四行，以响应玩家是否希望再次游玩游戏。

### 09 创建海洋

现在创建海洋。这是一个包含 64 个项目的列表，它们将每个矩阵 LED 变为蓝色。每次你选择一个位置，来自 Sea2 列表（在教程一中创建）的数据、敌方船只或弹药库会被添加到 Sea 列表的当前位置。然后 LED 显示会更新。首先设置颜色并将其赋值给名为 S 的变量。然后创建列表并添加 64 个 'S' 字符 – 注意最后一个后面不需要逗号。要将列表数据写入 LED，使用代码 `sense.set_pixels(Sea)`。添加一个小的延迟，然后停止第 7 步中的介绍音乐播放。注意这些行在代码中都是缩进的。

### 10 做好准备并倒计时

在游戏介绍之后，通知玩家“做好准备”，因为游戏即将开始。这是由一个简单的声音文件触发的，并使用了你之前用过的 Pygame 代码。接下来，创建一个从三到一的简单倒计时。这使用一个循环按顺序遍历一个列表。每次显示数字：`sense.show_letter(str(num))`。注意数字在显示前被转换为字符串。同样，在显示每个数字之间添加一个小的延迟。

![](img/fb76008333fb7aef815b136f9f1afe5f_75_2.png)

### 11 开始

在倒计时结束后，游戏准备就绪。通过一个简单的“开始”或类似的听觉命令通知玩家，第一行和第二行。然后调用你在教程一中开始并在第 6 步中完成的 main() 游戏函数。由于 main() 函数位于 Python 程序的开头，它已经加载并准备部署。游戏开始……

```python
pygame.mixer.music.load("sounds/go.mp3")
pygame.mixer.music.play()
### Begin the main game ###
main()
```

### 12 再玩一次？

游戏现在开始，你可以选择海上的位置。该位置会被检查是否有敌方船只、弹药或仅是空旷区域。一旦 main() 函数结束，它会跳出游戏循环并运行下面的代码。这给了你再玩一次的选择。首先加载“选择”图像。然后加载并播放一个声音文件，询问玩家是否想再玩一次。

![](img/fb76008333fb7aef815b136f9f1afe5f_75_3.png)

### 13 检查玩家响应

为了对问题做出反应，可以使用 Sense HAT 摇杆来选择向上或向下。在第一行，一个 while() 循环检查游戏选择是否等于 1 或 True。如果是，则使用 Pygame 检查

