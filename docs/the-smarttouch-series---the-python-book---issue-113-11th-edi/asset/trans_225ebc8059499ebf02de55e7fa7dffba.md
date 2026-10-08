

![](img/e016e192a91ffc1a9e474690a590742f_122_0.png)

左图。完成后，我们的迷你游戏会使用聊天控制台来报告你的得分。

## 13 游戏结束
第13步是处理游戏结束的条件。

如果你真的踩到了地雷，游戏就结束了。使用 `postToChat` 代码在 Minecraft 世界中显示“Game Over”（游戏结束）信息。

```
mc.postToChat("G A M E   O V E R")
```

## 14 最终得分
这是显示最终得分的地方。

游戏的最后一部分是给出一个分数。这里使用了你在第8步中创建的 `score` 变量，然后使用 `mc.postToChat` 代码。首先将分数转换为字符串，以便其能够显示在屏幕上。由于你的回合已结束，请添加一个 `break` 语句来结束循环并停止代码运行。

## 15 安全方块
这处理玩家处于安全状态的情况。

但如果你没有踩到地雷怎么办？游戏会继续，你需要知道你之前在棋盘上的位置。使用代码 `mc.setBlock(x1, y1-1, z1, 41)` 将你脚下站立的方块变成黄金或其他你喜欢的材料。在代码中，Y 坐标是 Y – 1，它选择的是玩家脚下那块方块。

## 16 增加分数
这为每次安全移动增加分数。

除了存活并再玩一轮外，你还获得一分。这是通过每次将方块变为黄金并返回循环开始处以检查下一个你停下的方块状态时，将 `score` 变量递增 1 来实现的。`postToChat` 用于告知你你又成功通过了一次移动！

```
score = score + 1
mc.postToChat("You were safe!")
```

## 17 运行游戏
这是运行完整游戏逻辑的最后一步。

这就完成了程序的代码编写。保存它，然后开始一个 Minecraft 游戏。一旦世界创建完成，运行 Python 程序。切换回 Minecraft 窗口，你会看到棋盘已在你面前创建好。

## 完整代码清单

```python
import random
import time
from mcpi import minecraft
mc = minecraft.Minecraft.create()

###Creates the board###
mc.postToChat("Welcome to Minecraft MineSweeper")
x, y, z = mc.player.getPos()
mc.setBlocks(x, y-1, z, x+20, y-1, z+20, 58)

global mine
mine = random.randrange(0, 11, 1)

###Places the mine###
mine_x = int(x+mine)
mine_y = int(y-1)
mine_z = int(z+mine)
mc.setBlock(mine_x, mine_y, mine_z, 58)
score = 0
mc.postToChat("Score is "+str(score))

time.sleep(5)
while True:  ###Test if you are standing on the mine
    x1, y1, z1 = mc.player.getTilePos()
    #print x1, y1, z1 ##test
    time.sleep(0.1)
    score = score + 1

    if (x1, y1-1, z1) == (mine_x, mine_y, mine_z):
        mc.setBlocks(x-5, y-1, z-5, x+5, y+5, z+5, 10)
        mc.postToChat("G A M E   O V E R")
        mc.postToChat("Score is "+str(score))
        break
    else:
        mc.setBlock(x1, y1-1, z1, 41)
        mc.postToChat("You were safe!")
```

![](img/e016e192a91ffc1a9e474690a590742f_123_0.png)

## Pygame Zero

Pygame Zero 剔除了样板代码，让你能立即将想法转化为游戏，我们将向你展示如何实现。

## 资源

- **Pygame Zero:** pygame-zero.readthedocs.org
- **Pygame:** pygame.org/download.shtml
- **Pip** pip-installer.org
- **Python 3.2 或更高版本** www.python.org/
- **来自 FileSilo 的代码（可选）**

游戏是理解编程语言的好方法：你有一个目标去努力，且每添加一个功能都能带来乐趣。然而，游戏需要库和模块来处理图形及其他基本游戏功能。虽然 Pygame 库使得在 Python 中制作游戏相对容易，但它仍然引入了你需要在开始之前处理的样板代码——这成为了你或你的孩子开始编程的障碍。

Pygame Zero 为你处理所有这些样板代码，旨在让你立即开始编写游戏代码。Pg0（我们将这样简称它）对你在游戏开发中所需的内容做了合理的假设——从窗口大小到导入游戏库——这样你就可以直接开始编码你的创意。

Pg0 的创建者 Daniel Pope 告诉我们，这个库“源于与 Pycon UK 教育赛道教师们的交流，试图理解他们需要立即获得结果并将课程分解为小块内容，以便跟上整个班级的进度。”

为了让你了解这里涉及的内容，我们将构建一个简单游戏，从 *Pong* 类型的球拍和球开始，直到以 *Breakout* 风格击碎方块。该项目将展示通过很少的努力可以完成的事情。Pg0 处于早期开发阶段，但仍然提供了很好的起点——并且现在已包含在 Raspbian Jessie 镜像中的树莓派系统中。

我们将查看其他平台上的安装方法，但首先让我们看看它能施展什么魔法。

![](img/e016e192a91ffc1a9e474690a590742f_124_0.png)

## 使用 Python 创造

![](img/e016e192a91ffc1a9e474690a590742f_124_1.png)

![](img/e016e192a91ffc1a9e474690a590742f_124_2.png)

### 04 没有树莓派？

你甚至不需要树莓派来安装 Pygame Zero——只需安装 Pygame 库，然后使用 pip 安装 Pygame Zero。不同发行版的说明各不相同，但一个好的起点是文档：bit.ly/1GYZnUB。

### 老少皆宜

在针对年轻人使用 Pygame 且包含所有样板代码的情况下，也可以取得很好的成果（参见 Bryson Payne 的书籍），但 Pygame 和 Pg0，尽管它们被用作强大的教育工具，但对于处于学习任何阶段的无编程经验者来说，也是创建游戏的好选择。

### 01 零努力

虽然编写游戏并不容易，但开始一定很容易。如果你的树莓派安装了 Raspbian Jessie，你就准备就绪了。打开终端并输入：

```
touch example.py
pgzrun example.py
```

你将看到一个空的游戏窗口打开（按 Ctrl+Q 关闭窗口）。是的，开始就这么简单！

伟大的游戏都关乎游戏性，由强大的想象力驱动，生成图像、动画、声音以及穿越游戏世界的旅程。优秀的框架向非传统编程学习者开放了这一创造性活动，而这正是 Python 长期擅长的领域。

### 02 Python 3

如果你没有 Raspbian Jessie，很可能你既没有安装 Pg0 也没有安装 Pygame。Python3 的 pip 包安装器会为你获取 Pg0，但前面的步骤因发行版而异。你需要的一件事是 Python 3.2（或更新版本）。如果你一直在编码中使用 Python 2.x（可能是因为你在跟随的教程中使用了它），请借机温和地升级到 Python 3。

![](img/e016e192a91ffc1a9e474690a590742f_124_3.png)

### 03 旧版 Raspbian

如果你仍在运行 Raspbian Wheezy，你需要执行以下步骤来安装 Pygame Zero：

```
sudo apt-get update
sudo apt-get install python3-setuptools python3-pip
sudo pip-3.2 install pgzero
```

### 05 Intro.py

我们在第 1 步中看到的默认 800 乘 600 像素的黑色方块现在可以手动覆盖了。例如，我们可以使用以下代码将其替换为一个超大的金砖，向 Breakout 巧妙致敬：

```python
WIDTH = 1000
HEIGHT = 100

def draw():
    screen.fill((255, 138, 0))
```

那个颜色元组采用 RGB 值，因此你可以快速获得各种颜色；`screen` 是为窗口显示内置于 Pg0 中的，并提供了各种用于不同精灵的方法...

![](img/e016e192a91ffc1a9e474690a590742f_125_0.png)

## 使用 Python 创造

好的。球拍和球先出现——它们是 Pong 和 Breakout 的基石。

## 程序对象

David Ames，他在英国各地的活动中使用 P&O 教年幼的孩子编程，告诉我们：“在教孩子时，应避免的一件事是面向对象。”OOP（面向对象编程）部分被 P&O 抽象化了，但不能忽视。

也许最好的方法是使用 P&O 和一些简单代码开始，然后在需要用 OOP 解决特定问题时再引入 OOP。

对于 Code Club 年龄段——大约八到十一岁——提供信息以解决实际问题效果很好。这对成年人也行得通，但总有人读过后续内容并有一些棘手的问题。

### 06 精灵

P&O 文档中的 intro 示例加载了带 Actor 类的对象，它将自动加载命名的精灵（P&O 会在名为 images 的子目录中查找 .jpg 或 .png）。

```python
alien = Actor('alien')
alien.pos = 100, 56
WIDTH = 500
HEIGHT = alien.height + 20

def draw():
    screen.clear()
    alien.draw()
```

你可以从 P&O 文档（bit.ly/1SmEiM7）下载外星人精灵并尝试那里展示的动画，但我们在我们的游戏中采取了不同的方法。

### 07 通过 Pong 玩 Breakout

虽然树莓派在某种程度上是对 1980 年代 8 位计算机的致敬，但 Breakout 来自 1970 年代，是早期街机经典 Pong 的直接后代。我们将遵循从 Pong 到 Breakout（历史上涉及苹果公司创始人 Steve Wozniak 和 Steve Jobs）的路径来创建代码，给你选择将 Pong 元素发展成正式游戏的机会，同时也让你精化完成的 Breakout 克隆版。

### 08 球拍

你可以认为 Breakout 本质上是一个移动球拍——也就是说，你在击打一个移动的球以打碎方块。球拍是一个矩形，Pygame 的 Rect 对象存储和操作矩形区域——我们使用 `Rect(left, top, width, height)`，在此之前我们定义球拍颜色，然后调用 draw 函数使用 screen 函数将球拍放在屏幕上。

```python
W = 800
H = 600
RED = 200, 0, 0
bat = Rect((W//2, 0.96 * H), (150, 15))

def draw():
    screen.clear()
    screen.draw.filled_rect(bat, RED)
```

![](img/e016e192a91ffc1a9e474690a590742f_125_1.png)

### 09 鼠标移动

我们想要移动球拍，鼠标比方向键更接近街机球拍。添加以下内容：

```python
def on_mouse_move(pos):
    x, y = pos
    bat.center = (x, bat.center[1])
```

使用 pgzrun 测试你是否有一个带有球拍和移动功能的屏幕。

