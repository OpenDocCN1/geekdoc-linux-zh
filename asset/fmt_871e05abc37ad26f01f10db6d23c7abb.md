
树莓派 OS 镜像已安装了 Minecraft 和 Python。允许你使用 Python 与 Minecraft 交互的 Minecraft API 也已预装。如果你使用的是旧版本的操作系统，我们强烈建议下载并将版本更新到最新的 Jessie 或 Raspbian。

![](img/516df994db593237169e2aff6d3e6840_119_0.png)

右侧安全的方块已变成金色 - 剩下的都是地雷！

# 使用 Python 创建

![](img/516df994db593237169e2aff6d3e6840_120_0.png)

```python
import minecraft
```

## 02 导入模块

打开你喜欢的 Python 编辑器并新建一个窗口。你需要导入模块：`random` 用于计算和创建位置，`import time` 用于在程序中添加暂停和延迟。接下来，添加两行代码：`from mc import minecraft` 和 `mc = minecraft.create()`。这些代码创建了 Minecraft 和 Python 之间的连接。该模块允许你编写 `minecraft` 而不是 `minecraft.create`。

```python
import random
import time
from mc import minecraft
mc = minecraft.create()
```

## 切换到 shell

在 Python 和 Minecraft 屏幕之间切换是很困难的，尤其是在我的世界中。最好的方法是使用屏幕周围的窗口来全屏运行 MC，因为此时鼠标控制会被禁用。使用 Tab 键将键盘和鼠标从 MC 窗口释放。

## 03 运行代码

使用 Python 控制我的世界非常简单；下面的程序是可以运行的。每个方块都有自己的 ID，数字是 `x, y, z`。`mc.player.getpos()` 获取玩家在世界中的位置并将其返回为一组坐标：`x, y, z`。现在你知道你站在世界的哪个位置了，我们可以使用 `mc.setblock(x, y, z)` 来放置方块。

```python
floor = 38
while True:
    x, y, z = mc.player.getpos()
    mc.setblock(x, y, z, floor)
    time.sleep(1)
```

## 04 运行代码

通过增大 MC 窗口的大小，可以更容易同时看到代码和运行中的程序；在两者之间切换可能会令人沮丧。Tab 键将释放键盘和鼠标并等待其加载。运行程序并等待它加载。当你走动时，你会掉下花！更改第 1 行的 ID 数字来更改方块类型，而不是种植、黄金或水元素。

![](img/516df994db593237169e2aff6d3e6840_120_1.png)

## 05 向我的世界世界发布消息

向我的世界发布消息是可能的。这在游戏中用于通知玩家游戏已开始以及当前分数。在你之前的程序中，以下行代码将显示该消息。你可以用代码替换一些花朵。保存并运行程序；你可以更改坐标，或者移动到下一步开始游戏。

## 06 创建棋盘

要在玩家当前站立的棋盘上放置方块，建议在运行程序之前填充空气或平坦空间。要创建棋盘，你需要使用 `x, y, z` 找到玩家在世界中的位置：`mc.player.getpos()`。然后使用 `mc.setblock` 放置组成棋盘的方块：

```python
mc.setblock(x, y, z, x+1, y+1, z+20)
```

数字 5 是 ID。你可以通过更改 +20 来增大或减小棋盘的大小。在示例中，棋盘是 20x20 方块，这为你提供了一个 400 方块的区域进行游戏。

![](img/516df994db593237169e2aff6d3e6840_120_2.png)

## 07 创建地雷

在上一步中，你找到了玩家在棋盘上的位置。`x, y` 坐标可以用于在棋盘上放置雷。代码 `mine = random.randint(0, 19)` 生成一个 0 到 19 之间的随机数。将其与玩家当前的位置结合并将数字添加到位置 - 这在棋盘上创建了一个随机地雷。

```python
mine_x = int(x)
mine_y = int(y)
mine_z = int(z)
```

使用 `setblock` 放置地雷：`mc.setblock(mine_x, mine_y, mine_z, 5)`。使用 `y-1` 确保方块放置在与棋盘相同的高度。5 是方块 ID，如果你想看雷在哪里，可以更改它。这对于测试代码的其他部分很有用，所以在玩之前把它改回来！

## 08 创建得分变量

每当你留在地雷内，你的分数就会加 1。创建一个变量来存储当前分数，并在开始时将其设置为零。使用 `postChat` 宣布分数。注意，我的世界不能持有值，因此分数在显示之前会转换为整数。

```python
score = 0
mc.postChat("score: " + str(score))
```

## 其他我的世界

如果你喜欢编程和我的世界，还有更多基于树莓派的项目可以查看。查看我们关于它们的教程。

## 09 检查玩家在棋盘上的位置

找到玩家在棋盘上的位置后，`x, y` 坐标可以用于在棋盘上放置雷。接下来，你需要检查玩家在棋盘上的位置以及他们是否在地雷内。

```python
import random
while True:
    x, y, z = mc.player.getpos()
```

## 10 获得积分

现在玩家每移动一个方格就会获得 1 分。这是通过向现有分数增加数值来实现的。在这个循环中，当玩家移动时，就会加 1。

```python
time.sleep(1)
score += 1
if (x1, y1, z1) == (mine_x, mine_y, mine_z):
```

## 12 设置雷

在上一步中我们检查了你是站在雷还是安全的方块上。如果是雷，将其替换为岩浆，它会包裹玩家。使用 `mc.setblock` 在两个点之间创建方块。岩浆受重力影响，因此将它们设置在更高的地方可以确保岩浆流向玩家。

```python
mc.setblock(x-5, y+1, z-5, x+5, y+2, z+5)
```

## 13 游戏结束

完成后，迷你游戏使用控制台报告你的分数。

```python
import sys
import random
import time
import os
import math
import threading
import tkinter
import minecraft
import mc

score = 0
player_x = 0
player_y = 0
player_speed = 1
width = 100
height = 100

while True:
    move = random.randint(0, 3)
    if move == 0:
        player_x += 1
    elif move == 1:
        player_x -= 1
    elif move == 2:
        player_y += 1
    elif move == 3:
        player_y -= 1
    if player_x < 0 or player_x > width:
        player_x = 0
    if player_y < 0 or player_y > height:
        player_y = 0
    time.sleep(0.1)
```
