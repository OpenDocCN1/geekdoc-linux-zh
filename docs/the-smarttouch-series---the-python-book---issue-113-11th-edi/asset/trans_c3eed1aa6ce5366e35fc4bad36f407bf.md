

使用 RGB（红、绿、蓝）颜色编码来定义我们游戏世界的颜色。这可能有些反直觉，但全零代表黑色，而全 255 代表白色。这可以理解为该颜色范围内光的强度，其中 255 是最大值，0 表示没有该颜色。

```python
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
```

我们需要设置游戏环境窗口的尺寸。这里使用典型的 VGA 分辨率 800x600，但如果你想要真正的复古氛围，可能会希望使用更低的分辨率。例如，VGA 的原始分辨率是 640x480。

```python
size = (800, 600)
screen = pygame.display.set_mode(size)
pygame.display.set_caption("Pong")
```

我们还将窗口标题设置为 Pong（乒乓球），但你可以在此处发挥更多创意。

既然我们有了一个已设置分辨率的显示窗口，以及配置好的彩色背景和前景，我们就可以关注程序的主循环了。在开始之前，让我们先设定该循环的条件：

```python
carryOn = True
clock = pygame.time.Clock()
```

这里我们告诉程序，布尔变量 `carryOn` 被设置为 True。稍后我们会设计循环，使其持续运行，直到我们将这个布尔变量的状态更改为 False。时钟（clock）控制我们更新的速度。我们需要持续观察用户输入并实时做出反应——例如，当鼠标或键盘被按下时。当我们监测到变化时，必须实现相应的游戏逻辑，例如移动挡板或球。在每次变化后，我们需要刷新屏幕，以确保图形和精灵被重新绘制，这时游戏时钟就会派上用场。我们可以设置屏幕刷新的频率——这就是所谓的“帧率”。在下面的代码中，我们将帧率设置为每秒 60 帧，这是大多数电子游戏标准。帧率越高，游戏中的动作在屏幕上看起来越流畅，但同时也需要更多的计算资源来运行，因为中央处理器需要在更短的时间内计算和处理更多的事件。

```python
while carryOn:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            carryOn = False

    screen.fill(BLACK)
    pygame.draw.line(screen, WHITE, [349, 0], [349, 500], 5)
    pygame.display.flip()
    clock.tick(60)
```

也就是说，当我们的 `carryOn` 布尔值为 True 时，我们在检查用户是否有任何操作（`pygame.event.get()`），如果他们做的是点击关闭按钮（`if event.type == pygame.QUIT`），我们就将 `carryOn` 布尔值切换为 False。

我们还没有添加游戏逻辑——它们都将放在 while 循环之后的中间部分。目前为止，我们已经完成了绘制。屏幕被填充为黑色，并在屏幕上绘制了一张白色的网。然后我们通过 `pygame.display.flip()` 更新屏幕并设置了帧率。

## 退出程序！

一如既往，我们需要一种安全退出程序的方式。在主程序循环之后，最好包含一个 `pygame.quit()` 命令。

对于我们的挡板，我们要创建一个新的类。这样，我们可以生成多个该类的对象，它们将具有相同的属性。每个玩家需要一个挡板，但它们将具有相同的高度、宽度、颜色等。因此，在这里使用面向对象的实用方法比编程两个独立的实体更明智。为了正确实现面向对象编程，我们需要将挡板类保存在其自己的文件中。创建一个名为 `paddle.py` 的新 Python 文件。

### 快速提示

- 尝试为游戏引入一个分数限制。通过添加选择功能，可以使用 IF 语句在游戏结束前控制玩家达到特定分数时的游戏终止。

![](img/e016e192a91ffc1a9e474690a590742f_108_0.png)

## 用 Python 创建

### 快速提示

- 我们能不能更上一层楼，创建一个四人对战的 Pong 版本，即在每一侧都设置一个挡板？这听起来完全疯狂，但听起来很有趣！

```python
import pygame
BLACK = (0, 0, 0)

class Paddle(pygame.sprite.Sprite):
    def __init__(self, color, width, height):
        super().__init__()
        self.image = pygame.Surface([width, height])
        self.image.fill(BLACK)
        self.image.set_colorkey(BLACK)
        pygame.draw.rect(self.image, color, [0, 0, width, height])
        self.rect = self.image.get_rect()
```

在我们的第一个类中，我们设置了基本参数：高度、宽度和颜色，以及形状。这没什么复杂的，因为我们继承自 `pygame.sprite` 类并在此基础上构建。因此，我们不需要指定什么是矩形或如何绘制它。

为了控制挡板的移动，我们需要几个方法：一个用于 x 轴，另一个用于 y 轴。同时要注意像素检查，确保它们不会移出屏幕：

```python
def moveUp(self, pixels):
    self.rect.y -= pixels
    if self.rect.y < 0:
        self.rect.y = 0
```

## 将 Pong 提升到下一个层级

由于 Pong 已经存在了 40 多年，我们看到过许多本质上基本相同的游戏的迭代版本。一旦我们的 PyGame 版本完全可用，我们或许可以考虑采取哪些步骤来改进我们的游戏？在较简单的端，我们可以将配色方案从黑白改为更现代的风格。当 Pong 最初发布时，黑白是仅有的选择。到 Atari 问世时，PAL 格式已经有 128 种颜色。八位主机引入了 256 种颜色，而现在我们实际上拥有数十亿种颜色。我们的游戏设计为 VGA 分辨率，如果我们坚持那种复古/怀旧的美学风格，我们只有 75 种颜色可用。例如，尝试将你的 Pong 游戏改为蓝色和黄色。改变帧率会对游戏产生什么影响？增加或减少它会影响游戏玩法吗？我们能否在球撞击墙壁表面时实现瞬间加速，在球从挡板反弹时实现短暂减速？这可能提供戏剧性的特效。同样，我们也可以改变球本身的速度。

为了增加游戏难度，如果我们引入“等级”，我们可能会希望将挡板设置得更小。还有**也**有机会让事情完全失控，因此我们可以改变球从墙壁反弹的角度，甚至通过从球类生成更多对象来引入更多的球。

![](img/e016e192a91ffc1a9e474690a590742f_109_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_109_1.png)

*上方为带有活动挡板和反弹球的 Pong 游戏。*

```python
def moveDown(self, pixels):
    self.rect.y += pixels
    if self.rect.y > 400:
        self.rect.y = 400
```

为了将我们的新类集成到游戏中，切换回 `pong.py` 并像导入任何其他模块一样导入它，通过在代码顶部添加 `from paddle import Paddle`。

创建挡板类的实例与创建对象一样简单。通过在定义窗口后的某处插入下面显示的代码，我们可以创建两个挡板：一个用于玩家 A，另一个用于玩家 B。

```python
paddleA = Paddle(WHITE, 10, 100)
paddleA.rect.x = 20
paddleA.rect.y = 200

paddleB = Paddle(WHITE, 10, 100)
paddleB.rect.x = 670
paddleB.rect.y = 200
```

紧接着这些操作之后，我们要创建一个包含所有使用精灵（包括这两个挡板）的列表：

```python
all_sprites_list = pygame.sprite.Group()
all_sprites_list.add(paddleA)
all_sprites_list.add(paddleB)
```

当我们稍后引入额外的精灵时，我们将把它们添加到这个列表中。为了确保我们的精灵被绘制，我们随后将在翻转（绘制）屏幕之前调用这个列表，使用 `all_sprites_list.draw(screen)`。

## 良好的划桨

实现挡板类的最后一步是设置一个事件处理器，以监控按键按下。如果玩家 A 使用 S 和 W 键，而玩家 B 使用键盘上的向上和向下键，我们需要在主要程序循环中添加以下内容：

```python
keys = pygame.key.get_pressed()
if keys[pygame.K_w]:
    paddleA.moveUp(5)
if keys[pygame.K_s]:
    paddleA.moveDown(5)
if keys[pygame.K_UP]:
    paddleB.moveUp(5)
if keys[pygame.K_DOWN]:
    paddleB.moveDown(5)
```

