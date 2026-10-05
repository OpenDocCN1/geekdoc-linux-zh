
通过更改 `animate()` 函数中的持续时间（duration）来改变移动云朵的速度。请记住，在开始时有一个 `animate()` 函数，当它们重新出现在屏幕底部时又有一个。

增加时钟上的时间长度。

# 最终的游戏代码列表

为了帮助你熟悉这个程序的创建流程，并并将所有内容整合在一个处，这里是最终的代码列表 (12-4)：

代码列表 12-4: 最终的 Cloudbusting 游戏

+   # Cloudbusting 游戏
# 源自《树莓派入门教程》第3版
# 作者 Sean McManus - www.sean.co.uk
# 运行命令：pgzrun cloudbusting.py

```python
import random

WIDTH = 500
HEIGHT = 500
score = 0
timer = 10
clouds = list()

for i in range(6):
    filename = 'target' + str(i)
    clouds.append(filename)
    this_cloud = clouds[i]
    this_cloud.x = random.randint(int(this_cloud.width / 2), WIDTH - this_cloud.width / 2)
    this_cloud.y = HEIGHT + this_cloud.height
    animate(this_cloud, tween='linear', 
            duration=random.uniform(1, 3), 
            pos=(this_cloud.x + random.randint(10, 100), -200))
```

```python
def draw():
    screen.clear()
    for i in range(6):
        this_cloud = clouds[i]
        this_cloud.draw()
```

```python
screen.draw.text("Score: " + str(score), (2, 2), color="orange")
screen.draw.text("Timer: " + str(timer), (WIDTH - 70, 20), color="orange")
if timer == 0:
    screen.draw.text(str(score), (130, 120), color="white", fontsize=300)
```

```python
def update():
    for i in range(6):
        this_cloud = clouds[i]
        if this_cloud.y < 0 - this_cloud.height:
            this_cloud.y = HEIGHT + this_cloud.height
        if timer > 0:
            this_cloud.x = random.randint(int(this_cloud.width / 2), WIDTH - this_cloud.width / 2)
            this_cloud.image = 'target' + str(i)
        animate(this_cloud, random, tweens='linear', 
                duration=random.uniform(1, 3), 
                pos=(this_cloud.x + random.randint(-10, 100)))
```

```python
def on_mouse_down(pos):
    for i in range(6):
        this_cloud = clouds[i]
        if this_cloud.collidepoint(pos) and timer > 0 
            and this_cloud.image != 'pop':
                this_cloud.image = 'pop'
                sounds.blop.play()
                score += 1
```

```python
def countdown():
    global timer
    timer -= 1
    if timer == 0:
        clock.unschedule(countdown)
        sounds.whoops.play()
```

```python
clock.schedule_interval(countdown, 1)
```

# 进一步探索 Pygame Zero

我们希望这个项目能让你领略 Pygame Zero 的功能。除了支持鼠标点击外，你还可以用它来检测按键，从而制作出可以通过键盘控制角色移动的更传统的游戏。因此，它是大多数类型游戏的良好基础。

要了解更多信息，我们建议查看以下资源：

- Daniel Pope 发布 Pygame Zero 的博客文章：http://mauveweb.co.uk/posts/2015/05/pygame-zero.html

- Pygame Zero 文档，包含简单示例：http://pygame-zero.readthedocs.io/en/latest

- Pygame Zero 内置对象列表，包含关于演员(actors)、图像(images)、声音(sounds)和时钟(clock)的信息：http://pygame-zero.readthedocs.io/en/latest/buildins.html

你也可以阅读 Sean 的书籍 *Mission Python*，看看如何将 Pygame Zero 作为 3D 冒险游戏的基础。

# 本章内容

- » 探索 Minecraft 世界
- » 在 Python 中操控 Minecraft 世界
- » 用 Python 生成随机 Minecraft 迷宫

# 第 13 章

# 使用 Python 为 Minecraft编程

Minecraft 吸引了每个人内心的乐高粉丝。它能让你用材料块构建沉浸式的 3D 世界，并激发了人们的想象力，使其包括 PC 和 Xbox 在内的各种平台销量超过了 1 亿份。

树莓派提供一个 Minecraft 版本。它具有创造模式（Creative mode），在该模式你可以安全地建造物品，而不必担心怪物攻击或饥饿的威胁。最好的特性是你可以使用多种语言（包括 Python）对其进行编程。这意味着你不需要手动放置每个区块就能建造一座宏伟的宫殿，你还可以编写程序生成全新的结构供你探索，正如你在本章中看到的。

本章的项目将向你展示如何使用 Python 与 Minecraft 交互。

# 探索 Minecraft 世界

Minecraft 吸引了每个人内心的乐高粉丝。它能让你用材料块构建沉浸式的 3D 世界，并激发了人们的想象力，使其包括 PC 和 Xbox 在内的各种平台销量超过了 1 亿份。

树莓派提供一个 Minecraft 版本。它具有创造模式（Creative mode），在该模式你可以安全地建造物品，而不必担心怪物攻击或饥饿的威胁。最好的特性是你可以使用多种语言（包括 Python）对其进行编程。这意味着你不需要手动放置每个区块就能建造一座宏伟的宫殿，你还可以编写程序生成全新的结构供你探索，正如你在本章中看到的。

本章的项目将向你展示如何使用 Python 与 Minecraft 交互。

# 移动

Minecraft 使用双手操作非常简单——一手握鼠标，一手握键盘。使用鼠标环顾四周并改变方向，左右滑动转弯，向前向后移动。使用 W 和 S 键前进和后退，使用 A 和 D 键向左右侧移。这些键在键盘上成一组，非常方便切换。

当你走入低矮区块时，角色会自动跳到上面，但你也可以通过按下空格键来主动跳跃。

为了获得世界的最佳视角，双击空格键即可起飞。当你飞行时，按住空格键可以升高，按住左 Shift 键可以下降。双击空格键停止飞行并落地。在这个版本的 Minecraft 中没有生命值或伤害，所以你可以随意进行自由落体。

# 制作与破坏

要破坏世界中的区块，使用鼠标将准星对准想要摧毁的区块，并按住左鼠标键。某些区块比其他区块更容易破坏。距离是有限制的，如果你在尝试砸碎区块时看不到掉落碎片，请靠近一点。

窗口底部的面板显示了你可以在世界中放置的区块。（请参考图 13-L）。你可以使用鼠标滚轮选择它们，或者按下 1 到 8 之间的数字来选取（从左到右）。按下 E 键打开完整物品，然后可以使用移动键（W, A, S, D）在周围导航，或按回车键选择区块——你也可以直接用鼠标点击选中的区块。

要放置区块，右键点击你想放置的位置。只有在你能看到另一个区块顶部时，才能将区块放在它的上方，因此你可能需要飞行来建造高层建筑。

