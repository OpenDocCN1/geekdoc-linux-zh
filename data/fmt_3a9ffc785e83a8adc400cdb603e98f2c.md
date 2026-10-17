
# Pygame Zero

Pygame Zero 删除了冗板代码，让你能够将想法立即转化为游戏，我们将向你展示如何做到。

## 资源

- Pygame Zero: `pygamezero.readthedocs.org`
- Pygame: `pygame.org/download.html`
- Pip: `pip-installer.org`
- Python 3: `www.python.org/`

游戏是理解语言的一种极佳方式：你有一个目标可以努力，每添加一个新功能都会带来更多乐趣。然而，游戏需要库和模块来处理图形和其他其他基本功能。Pygame 让制作游戏变得相对简单，而不会让你在开始之前就陷入那些需要的技术细节所困扰——这些细节正是阻碍孩子们开始编写代码的障碍。

Pygame Zero 为你准备了所有的冗板代码，旨在让你立即开始编写游戏。PGZ（如果我们粗略计算的话）对你游戏所需的内容做出了合理的假设——从窗口大小到导入游戏库——这样你就可以开始实现你的想法了。

PG 的创建者 Daniel Pope 告诉我们，这个库“源于与 Python UK 教育板块的老师们的交流，并试图理解他们需要即时的结果，并将其拆分成易于理解的碎片，以保持孩子们跟上速度”。为了让你对这里的内容有一个概念，我们将从一个类似乒乓球的拍和球开始，通过破碎方块构建一个简单的游戏。

我们将创建的项目将展示只需少少努力就能完成什么。尽管项目处于开发早期，但仍然提供了一个很好的起点——并且已经在树莓派上通过简单的图像构建完成。我们将查看其他平台上的安装方法，但让我们看看它能施什么魔法。

来自 FileSilo 的代码（可选）

![](img/516df994db593237169e2aff6d3e6840_123_0.png)

## 使用 Python 创建

Right Breakout 是一款经典的街机游戏，可以用 Pygame Zero 进行重新构思。

![](img/516df994db593237169e2aff6d3e6840_124_0.png)

## FileSilo 上的代码

![](img/516df994db593237169e2aff6d3e6840_124_1.png)

## 年轻

在使用 Pygame 的情况下，使用冗板代码和人物动画，也可以获得极佳的结果（参见 Payne 的书，但尽管 Pygame 有其教育性教程，它更多是为了为那些正在学习如何学习的人创建游戏）。

## 没有树莓派怎么办？

你不需要树莓派来安装 Pygame Zero——只需安装 Pygame 库，然后就可以用 `pip` 安装 Pygame Zero。变体各不相同，但文档的一个良好起点是：`bit.ly/1TG7YmUiB`。

![](img/516df994db593237169e2aff6d3e6840_124_2.png)

## 零努力

虽然游戏并不容易，但入门肯定非常容易。如果你在树莓派上运行了 Raspberry Jessie，你就可以准备就绪。打开终端并……

## 引言

我们在步骤 1 中看到的 800  600 像素的默认黑色正方形现在可以手动覆盖了。例如，你可以使用以下代码画一条绿线，以适应 Breakout 风格：

```
WIDTH = 100

HEIGHT = 100

def draw():

    screen.fill((255, 130, 0))
```

```
touch example.py

pzero example.py
```

然而你会看到一个空游戏窗口 (`Ctrl+Q`) 将关闭窗口。

## Pygame

如果你还没有获得最新的树莓派 OS 更改，你将会。Pygame 软件包安装程序将负责为你安装 Pygame，前面的步骤因发行版而异。你需要 Python 3.2（或更高版本）。如果你在遵循的教程中一直坚持 Python 2.x，请让 Pygame 给你机会升级到 3。

伟大的游戏关乎游戏性，由强大的想象力驱动，产生动画、惊叹的声音和穿梭世界的旅程。自由软件的开放创作赋能了那些编程的传统学习者，而这正是 Pygame 长期以来表现出色的领域。

## 老旧的树莓派

如果你仍在运行 Raspberry Jessie，你需要运行以下步骤来安装 Pygame Zero：

```
sudo apt-get update

sudo apt-get install python3-setuptools

pip3 install pygame-zero
```

![](img/516df994db593237169e2aff6d3e6840_125_0.png)

```python
import pygame

import random

pygame.init()

screen = pygame.display.set_mode((800,600))

pygame.display.set_caption('Pygame Zero')

WIDTH = 800

HEIGHT = 600

running = True

while running:

    for event in pygame.event.get():

        if event.type == pygame.QUIT:

            running = False
```

这里涉及的内容是从一个类似乒乓球的拍和球开始，通过破碎方块构建一个简单的游戏。我们将创建的项目将展示只需少少努力就能完成什么。尽管项目处于开发早期，但仍然提供了一个很好的起点——并且已经在树莓派上通过简单的图像构建完成。我们将查看其他平台上的安装方法，但让我们看看它能施什么魔法。

在 `516df994db593237169e2aff6d3e6840_123_0.png` 处来自 FileSilo 的代码（可选）。

Right Breakout 是一款经典的街机游戏，可以用 Pygame Zero 进行重新构思。

![](img/516df994db593237169e2aff6d3e6840_124_0.png)

![](img/516df994db593237169e2aff6d3e6840_124_1.png)

在使用 Pygame 的情况下，使用冗板代码和人物动画，也可以获得极佳的结果（参见 Payne 的书，但尽管 Pygame 有其教育性教程，它更多是为了为那些正在学习如何学习的人创建游戏）。

你不需要树莓派来安装 Pygame Zero——只需安装 Pygame 库，然后就可以用 `pip` 安装 Pygame Zero。变体各不相同，但文档的一个良好起点是：`bit.ly/1TGYmUiB`。

![](img/516df994db593237169e2aff6d3e6840_124_2.png)

虽然游戏并不容易，但入门肯定非常容易。如果你在树莓派上运行了 Raspberry Jessie，你就可以准备就绪。打开终端并……

我们在步骤 1 中看到的 800  600 像素的默认黑色正方形现在可以手动覆盖了。例如，你可以使用以下代码画一条绿线，以适应 Breakout 风格：

```
WIDTH = 100

HEIGHT = 100

def draw():

    screen.fill((255, 130, 0))
```

```
touch example.py

pzero example.py
```

然而你会看到一个空游戏窗口 (`Ctrl+Q`) 将关闭窗口。

如果你还没有获得最新的树莓派 OS 更改，你将会。Pygame 软件包安装程序将负责为你安装 Pygame，前面的步骤因发行版而异。你需要 Python 3.2（或更高版本）。如果你在遵循的教程中一直坚持 Python 2.x，请让 Pygame 给你机会升级到 3。

如果你仍在运行 Raspberry Jessie，你需要运行以下步骤来安装 Pygame Zero：

```
sudo apt-get update

sudo apt-get install python3-setuptools

pip3 install pygame-zero
```

![](img/516df994db593237169e2aff6d3e6840_125_0.png)

```python
import pygame

import random

pygame.init()

screen = pygame.display.set_mode((800,600))

pygame.display.set_caption('Pygame Zero')

WIDTH = 800

HEIGHT = 600

running = True
```
