
两款游戏之间发布的是最初的《吃豆人》（Pac-Man）游戏，其中《登月着陆器》（Lunar Lander）发布于1979年，而第一款横版卷轴游戏发布于1981年。Python非常适合我们的复古游戏项目。那么，让我们开始吧。

当然，我们需要安装 Python。本教程将使用 Python 3。如果你使用的是基于 Debian 的发行版，可以通过 `sudo apt-get update`，然后运行 `sudo apt-get install python3` 来完成设置。我们还将利用一个矢量图形模块 linuxformat.py，可以在 www.linuxformat.com/code 的归档页面的源代码链接中找到它。下载或复制完成后，确保将 linuxformat.py 保存为我们即将开发的 Python 项目所在的同一目录中。

创建一个新的 Python 文件。使用你喜欢的文本编辑器创建一个空文件，并将其与 linuxformat.py 保存在同一个文件夹中，我们将把它作为矢量图形的参考模块。在编程方面，每次都不必重新发明轮子。用新的模块化导入开始你的新文档：

```python
from random import choice
from turtle import *
from linuxformat import vector
```

接下来，我们需要声明并初始化所有全局变量：

```python
state = {'score': 0}
path = turtle(visible=False)
writer = Turtle(visible=False)
aim = vector(5, 0)
pacman = vector(-40, -80)
ghosts = [vector(-180, 160), vector(5, 0)],
[vector(-180, 5), vector(0, 5)], [vector(180, 160),
vector(0, -5)], [vector(180, -160), vector(-5, 0)],]
tiles = [0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0,
0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 0, 1,
1, 1, 0, 0, 0, 0,
0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1,
0, 0, 0, 0, 0, 0,
0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1,
1, 1, 1, 0, 0, 0, 0,
0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1,
0, 0, 1, 0, 0, 0, 0,
0, 1, 1, 1, 1, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1,
1, 1, 1, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 1, 0, 1,
0, 0, 0, 0, 0, 0,
0, 1, 1, 1, 1, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1,
1, 1, 1, 1, 0, 0, 0, 0, 0, 0,
0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0,
0, 0, 0, 0, 0, 0,
0, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1,
0, 0, 1, 0, 0, 0, 0,
0, 1, 0, 1, 0, 0, 0, 0,
0, 1, 1, 0, 1, 0, 1, 1, 1, 0, 0,
1, 1, 0, 0, 0, 0, 0, 0,
0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0,
0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 1, 1, 1, 0, 1, 1, 1, 1, 0, 1, 1, 1, 0, 1,
1, 1, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0,
]
```

![](img/e016e192a91ffc1a9e474690a590742f_104_0.png)

上方是一个使用 Python 开发的基于矢量的吃豆人游戏。

在这里，我们设置了吃豆人和所有四个鬼魂的出生坐标，并将分数初始化为零。Aim（目标）设置了游戏启动时吃豆人的移动方向，以 (x,y) 表示。默认情况下，我们在 x 轴正方向上移动，以正常速度 5 向右移动。将 y 轴设置为零意味着游戏开始时吃豆人不会上下移动。我们还创建了两个稍后将用到的 Turtle（海龟）对象：一个用于绘制游戏世界（Path），另一个用于写入分数（Writer）。

> **快速提示**
通过增加或减少代码底部的 'onkey' 值 (x,y)，可以加快或减慢吃豆人的速度。记住，正数表示向右或向上移动，负数表示向左或向下移动。

## 多人吃豆人等更多功能！

我们可能希望进行一些改进，将我们的吃豆人游戏提升到下一个级别。考虑一下我们如何改变关卡布局。也许当玩家收集完所有小圆点时，我们可以加载第二关。我们甚至可以生成自动生成的关卡，从而创建无限的游戏玩法。

其他可能为游戏带来有趣挑战的修改包括：通过改变吃豆人的出生位置来更改玩家起点；在不同关卡中增加或减少游戏中鬼魂的数量；随着玩家在关卡中的进度，使鬼魂变快或变慢。

如果我们真想更进一步，可以引入多人模式。过去，吃豆人游戏曾尝试过不同形式的多人游戏。我们可能希望从引入回合制多人游戏开始，通过开发排行榜来实现。这意味着只需在每局游戏结束时保存玩家的分数，并在玩家死亡时询问其姓名。这就是经典街机游戏机处理多人游戏的方式。不过，你可能想要做得更花哨，编写另一个由 WASD 控制而非方向键的玩家角色。这样，你就可以让两个吃豆人同时在游戏中活动，争夺小圆点和鬼魂！

## 快速提示

试着调整 World() 函数中的颜色，以创建一些看起来很有趣的吃豆人版本。

最后，我们要创建游戏世界。每个 1 代表可收集的小圆点或地板空间，而 0 代表黑色墙壁。
我们的游戏世界是 20x20 的，因此每 20 个值创建一个新行可能会更容易整理上面的 Python 列表。这里为了节省印刷空间没有这样做，但如果你这样做的话，在 Python 中看起来会好很多——至少对肉眼来说更易于识别。

## 充分利用海龟

是时候让这些海龟派上用场了。让我们创建一个绘制正方形的函数，这将用于在游戏中创建方形（和矩形），作为墙壁：

```python
def square(x, y):
    path.up()
    path.goto(x, y)
    path.down()
    path.begin_fill()
    for count in range(4):
        path.forward(20)
        path.left(90)
    path.end_fill()
```

我们还需要几个函数来计算数学问题。
尽管吃豆人是一个相对简单的游戏，但仍然涉及一些物理元素，主要在于碰撞检测，并确保我们的吃豆人不会穿过墙壁走出游戏世界。

```python
def offset(point):
    x = (floor(point.x, 20) + 200) / 20
    y = (180 - floor(point.y, 20)) / 20
    index = int(x + y * 20)
    return index
```

这将返回偏移量。我们还需要检查移动是否有效：

```python
def valid(point):
    index = offset(point)
    if tiles[index] == 0:
        return False
    index = offset(point + 10)
    if tiles[index] == 0:
        return False
    return point.x % 20 == 0 or point.y % 20 == 0
```

![](img/e016e192a91ffc1a9e474690a590742f_105_0.png)

让我们再次使用该海龟来绘制我们的游戏世界：

```python
def world():
    bgcolor('black')
    path.color('blue')
    for index in range(len(tiles)):
        tile = tiles[index]
        if tile > 0:
            x = (index % 20) * 20 - 200
            y = 180 - (index // 20) * 20
            square(x, y)
        if tile == 1:
            path.up()
            path.goto(x + 10, y + 10)
            path.dot(2, 'white')
```

当然，我们可以根据需要更改颜色，但一开始我们使用的是 1980 版吃豆人的传统黑色和蓝色环境。最后那个颜色（path.dot）分配给我们路径上的小圆点。你会注意到我们利用了之前设置好的 square 函数。
我们主要的一个函数 move，将用于移动我们的吃豆人和鬼魂在游戏世界中。

```python
def move():
    writer.undo()
    writer.write(state['score'])
    clear()
    if valid(pacman + aim):
        pacman.move(aim)
        index = offset(pacman)
        if tiles[index] == 1:
            tiles[index] = 2
            state['score'] += 1
            x = (index % 20) * 20 - 200
            y = 180 - (index // 20) * 20
            square(x, y)
    up()
    goto(pacman.x + 10, pacman.y + 10)
    dot(20, 'yellow')
    for point, course in ghosts:
        if valid(point + course):
            point.move(course)
        else:
            options = [
                vector(5, 0),
                vector(-5, 0),
                vector(0, 5),
                vector(0, -5),
            ]
            plan = choice(options)
            course.x = plan.x
            course.y = plan.y
    up()
    goto(point.x + 10, point.y + 10)
    dot(20, 'red')
    update()
    for point, course in ghosts:
        if abs(pacman - point) < 20:
            return
    ontimer(move, 100)
```

