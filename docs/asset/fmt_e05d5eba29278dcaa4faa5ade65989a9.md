
# Pygame Zero

Pygame Zero 删除了冗长的模板代码，能让你的想法瞬间变成游戏，我们将向你展示如何做到。

## 资源

- Pygame Zero: `pygame-zero.readthedocs.org`
- Pygame: `pygame.org/download.html`
- Pip: `pip-installer.org`
- Python 3.2 或更高版本: `www.python.org/`
- 来自 FileSilo 的代码（可选）

游戏是理解语言的一种极佳方式：有一个目标可以努力，每添加一个功能都会带来更多乐趣。然而，游戏需要库和模块来处理图形和其他其他核心功能。虽然 Pygame 库让制作游戏变得相对容易，但仍然存在障碍——阻碍你的孩子们开始编程的障碍。

Pygame Zero 为你删除了所有的模板代码，所以你可以立即开始编写游戏！PG（我们将之简称为 PG）对你游戏所需的内容做了合理的假设——从窗口大小到导入游戏库——这样你就可以直接编写你的想法了。

PG 的创建者 Daniel Popa 告诉我们，这个库“源于与 Python UK 教育赛道的教师的交流”，并试图理解他们需要即时的反馈，并将内容拆分为易于理解的片段，以跟上进度。

为了让你了解涉及的内容，我们将从类似弹乒球的风格构建一个简单的游戏。球和接球击碎方块。该项目将展示只需极少努力就能完成什么。虽然处于开发早期，但它提供了一个极好的起点——而且现在已经包含在树莓派的镜像中了。

我们将查看在其他平台上的安装，但让我们看看它能带来什么魔法。

![](img/3c5b3591dd9ac4cceb489cee11bd7908_127_0.png)

## 使用 Python 创建

经典的 Breakout（炸砖）是一款经典的街机游戏，可以用 Pygame Zero 进行重新构。

## Filesilo 上的代码

![](img/3c5b3591dd9ac4cceb489cee11bd7908_128_0.png)
![](img/3c5b3591dd9ac4cceb489cee11bd7908_128_1.png)
![](img/3c5b3591dd9ac4cceb489cee11bd7908_128_2.png)

## 04 没有树莓派？

04 你甚至不需要树莓派就可以安装 Pygame Zero——只需安装 Pygame 库，然后使用 `pip` 安装 Pygame Zero。变体很容易设置，但一个很好的起点是官方文档：`bit.ly/1tGTYmuiB`。

## 年轻与年老

### 01 零努力

01 虽然编写游戏并不容易，但入门确实非常容易。如果你已经在你的树莓派上安装了树莓派，你就可以准备好了。打开终端并输入：

```
touch example.py

pip install pygame
```

在使用了 Pygame 模板代码且针对年轻人的情况下，可以取得极佳的结果（参见 by Payne 的书），但尽管 Pygame 拥有强大的教育工具，无论处于学习的哪个阶段，它都更适合为儿童创建游戏。

如果你创建了一个空游戏窗口 (Ctrl+C) 将关闭窗口。

### 05 介绍介绍 py

05 如果我们在步骤 1 中看到的那个 830 比 600 像素的黑色正方形可以被加载。例如，我们可以使用以下代码将其替换为超大的绿色条，在制作 Breakout 的槽位中：

### 02 Python

02 如果你还没有安装树莓派，但 Pygame 的包安装程序通常会替你安装 Pygame，但前面的步骤因发行版而异。人们可能需要使用 Python 3.2 或更高版本，如果你仍在运行我们跟随的教程中的树莓派，Pygame 将为你提供开始 Pygame 的机会。

通过强大的动画、声音和对世界的旅程，可以取得极佳的结果。这种方法为非传统编程学习者开启了机会……

### 03 老旧树莓派

03 如果你仍在运行树莓派，你需要运行以下步骤来安装 Pygame：

```
sudo apt-get update

sudo apt-get install python3-setuptools

pip33.2 install pygame
```

```
WIDTH = 100

HEIGHT = 100

def draw():

screen.fill((255, 130, 0))
```

这种颜色采用 RGB，这样你可以获得各种显示。

Python 书 129

## 使用 Python 创建

![](img/3c5b3591dd9ac4cceb489cee11bd7908_129_0.png)

Right 挡板和球首先——Pangland Breakout。

## 程序对象

David Ames 使用 Pygame 教学时说：“教孩子们时，情况不同。OOP（面向对象编程）非常完美，但不能被忽视。”也许最好的方法是使用 Pygame 从简单开始，在 Code Club 中解决特定问题。关于反馈信息，可以解决一些棘手的问题

![](img/3c5b3591dd9ac4cceb489cee11bd7908_129_1.png)

### 08 挡板

你可以把 Breakout 想象成一个移动的球——目的是为了击碎方块。挡板是一个矩形，由 Pygame 的 `Rect` 对象管理。我们使用 `Rect(left,top),(width,height))` 来定义挡板在屏幕上的位置，然后使用 `draw()` 函数将挡板放在屏幕上：

```
WIDTH = 800

H = 600

RED = (200, 0, 0)

bat = Rect(W/2, 0.96 * H), (50,15))

draw.clear()

screen.draw(bat)
```

### 07 精灵

Pygame 文档中的示例显示一个 sprite 将围绕一组图像。

- `alien = Alien('alien')`

```
WIDTH = 500

HEIGHT = alien.height + 20

draw.clear()

screen.draw(alien)
```

我们使用了 Pygame 文档中的 `alien` 来展示动画，然后是另一种方法。

### 07 Breakout

虽然 Pygame 是 1980 年代的延伸——Breakout 源于 1970 年代并且经典：我们遵循 Pangland 的路线，这在历史上涉及到 Apple 创始人 Steve Wozniak 和 Steve Jobs，留下了开发元素的选择。

### 09 移动

我们移动挡板，鼠标比键盘更方便。添加以下内容：

```
x, y = pos

bat.center = (x, bat.center[1])
```

使用 `prgnrun` 测试你是否拥有屏幕、挡板和移动。

Python 书 130

## 使用 Python 创建

## Breakout 类型

为了让球在每次遇到墙壁时移动，基于 Tim Viner 的 Python Django 库，根据 MIT 许可授权——参见：

```python
from collections import namedtuple

import pygame

import time

W = 800

H = 600

RED = 200, 0, 0

WHITE = 200, 200, 200

GOLD = 255, 215, 0

ball = Rect((W/2, H/2), (30, 30))

direction = namedtuple('Direction', 'x y')

ball_dir = Direction(0, -5)

bat = Rect(W/2, 0.96 * H, (120, 15))

class Block(Rect):

    def __init__(self, colour, rect):

        super().__init__(self, rect)

        self.colour = colour

blocks = []

for n in range(24):

    block = Block(GOLD, ((n % 8) * 100 + 2, (n // 8) * 30), (96, 25))

    blocks.append(block)

def draw_blocks():

    for block in blocks:

        screen.draw_filled(block, block.colour)

def draw():

    screen.clear()

    screen.draw_filled(ball, WHITE)

    screen.draw_filled(bat, RED)

    draw_blocks()

def on_mouse_move(pos):

    x, y = pos

    bat.center = (x, bat.center[1])

def on_mouse_down():

    global ball_dir
```
