

![](img/0fc17bd4c29dc437e3ac28a53f7559db_65_0.png)

右侧 汤姆·维纳（Tom Viner）的方块数组使得带边框的矩形变得不再必要

## **14** 声音

同样在球拍碰撞时，`sounds.blip.play()` 会在声音子目录中查找名为 blip 的声音文件。你可以从 **FileSite.co.uk** 下载声音文件（以及完成的代码）。

实际上，现在想想，请忽略之前关于作业的那条评论——你真正的作业是将我们目前写好的内容变成一款正式的 *Pong!*（乒乓球游戏）游戏。但首先，让我们先把它变成 *Breakout!*（打砖块游戏）。

## **15** 砖块头！

如果你不太熟悉古老的电脑游戏 *Breakout*（打砖块），那么：

```
apt-get install librawout2
```

……去试试看。现在，我们并没有指望仅用这六页纸就构建出如此宏大的东西，但我们确实需要砖块。

## **16** 构建砖块

定义砖块并将其分布到屏幕上有很多方法。在汤姆·维纳的团队来自伦敦 Python Dojo 的版本中——这也是最初启发本文作者尝试编写代码的版本——砖块的大小是相对于屏幕横向排列的数量来设定的，具体如下：

```
N_BLOCKS = 8
BLOCK_W = W / N_BLOCKS
BLOCK_H = BLOCK_W / 4
BLOCK_COLOURS = RED, GREEN, BLUE
```

使用多彩砖块并构建为一个数组意味着砖块可以拼接而不需要边框。通过以屏幕宽度定义变量，这是良好的可持续代码，便于针对不同屏幕尺寸进行修改——参见 **github.com/tomviner/breakout**。

然而，单行彩色砖块的数组不足以填满整个游戏屏幕，因此我们将使用硬编码的值来构建我们的数组……

## **17** 挑战高峰

创建一个 *Block* 类：

```
class Block(Rect):
    def __init__(self, colour, rect):
        Rect.__init__(self, rect)
        self.colour = colour
```

……并为你的砖块选择一个漂亮的颜色：

```
GOLD = 205,145,0
```

## **18** 排列砖块

这将构建一个由 24 个砖块组成的数组，分为三行，每行八个：

```
blocks = []
for n_block in range(24):
    block = Block(GOLD, (((n_block%3)*100) + 2,
                         ((n_block // 3) * 25) + 2, (96, 25)))
    blocks.append(block)
```

## **19** 绘制砖块

在定义 `def draw()` 之后，添加 `Draw_blocks()`：

```
def draw_blocks():
    for block in blocks:
        screen.draw_filled_rect(block, block.colour)
```

## **20** 撞击砖块

关于砖块，剩下的工作就是扩展 **def move(ball)**，使球击中砖块时能够将其摧毁。

```
to_kill = ball.collidelist(blocks)
if to_kill >= 0:
    sounds.blip.play()
    ball_dir = Direction(ball_dir.x, abs(ball_dir.y))
    blocks.pop(to_kill)
```

## P0 +1

PyO 的一个新版本正在开发中——甚至当你读这篇文章时它可能已经发布了。PyO 的创造者 Daniel Pope 告诉我们“一代 API 正在制作中”，并且在 Py/PyConUK 冲刺期间，“我们完成了 Actor 旋转。”

欢迎贡献代码——不仅限于 PyO 代码本身，还需要更多的示例，不仅展示能做什么，还要为教师提供工具，让孩子们对编程的创造性行为产生热情。

PyO 还启发了 PyO Zero，以简化在树莓派上运行 PyO 编程的过程，随着截稿时间的临近，这个新库的开发正在迅速推进。

左侧 顶部 测试你的游戏完成后 – 然后测试你认识的其他人的 Breakout 游戏，看看代码有何不同

![](img/0fc17bd4c29dc437e3ac28a53f7559db_66_0.png)

![](img/0fc17bd4c29dc437e3ac28a53f7559db_66_1.png)

## **21** 游戏结束

最后，我们需要考虑成功摧毁所有砖块的可能性。

```
if not blocks:
    sounds.win.play()
    sounds.win.play()
    print("Winner!")
    time.sleep(1)
    sys.exit()
```

## **22** 分数显示

利用 Pygame Zero 的一些快速入门功能，我们大约用 60 行代码就拥有一个可运行的游戏。从这里开始，还有更多 Pg0 内容可供探索，但下一步（除了直接探索 Pg0 封装器之外的 Pygame）是深入探究未被 Pg0 封装器中介的 Pygame。

首先重构代码；有很多改进空间——参见教程资源中的示例 ‘breakout-refactored.py’。尝试添加计分功能，这是游戏中最显著的缺失。你可以尝试使用全局变量，并通过 print() 将分数写入终端，或者使用 screen.blit 将其显示在游戏屏幕上。未来版本的 Pg0 可能会在简单的分数保持方面提供更多支持。

## **23** 九条命的类

为了添加生命值、更多关卡以及更简单的生命/分数管理，你可能最好定义一个 GameClass 类，并将你希望持久化的许多更改封装在其中，例如 self.score 和 self.lives。你会发现网上有很多 Pygame 代码这样做，但你也可以找到 Pg0 示例，例如 Tim Martin 的优秀示例 pl_lander：github.com/timboe/pl_lander。

## **24** 不要停在这里

这篇文章面向初学者，所以别指望能理解所有内容！修改代码看看什么有效，从其他地方借用代码添加进来，并阅读更多代码。坚持这样做，然后尝试一个你自己的项目——并告诉我们你的进展如何。

### 完整代码列表（续）

```
def move(ball):
    global ball_dir
    ball.move_ip(ball_dir)

    if ball.x > 781 or ball.x <= 0:
        ball_dir = Direction(-1 * ball_dir.x, ball_dir.y)
    if ball.y <= 0:
        ball_dir = Direction(ball_dir.x, abs(ball_dir.y))

    if ball.colliderect(bat):
        sounds.blip.play()
        ball_dir = Direction(ball_dir.x, -abs(ball_dir.y))

    to_kill = ball.collidelist(blocks)

    if to_kill >= 0:
        sounds.block.play()
        ball_dir = Direction(ball_dir.x, abs(ball_dir.y))
        blocks.pop(to_kill)

    if not blocks:
        sounds.win.play()
        sounds.win.play()
        print("Winner!")
        time.sleep(1)
        sys.exit()

    if ball.y > H:
        sounds.die.play()
        print("Loser!")
        time.sleep(1)
        sys.exit()


def update():
    move(ball)
```

![](img/0fc17bd4c29dc437e3ac28a53f7559db_66_2.png)

## 在你的树莓派上添加多媒体

你可以使用专门的独立模块来处理多媒体，但使用 pygame 模块是一站式解决方案

![](img/0fc17bd4c29dc437e3ac28a53f7559db_67_0.png)

乔伊·伯纳德（Joey Bernard）是一位真正的通才，他的时间分布在制作家具、帮助研究人员解决科学计算问题以及编写 Android 应用程序之间

### 为什么选择 Python？

它是树莓派的官方语言。在 python.org/doc 阅读文档

> 在很多情况下，你希望在与最终用户的交互中使用多媒体。你可能想要展示一段非常有趣的视频，或者让你的程序以语音与用户交谈。

在这两种情况下，都有大量模块可供使用，使你能处理所有这些数据形式。然而，编程的一个老生常谈是“找到做某事最简单的方法”。在这里，这意味着如果你能找到一个提供所需一切功能单一框架，你应该使用它。这正是 pygame 模块扮演的角色。这并不是说使用 pygame 你能做你想做的一切，但你不应该低估学习和使用多个模块以及多个开发团队在编码风格中的思考方式的宝贵价值。本文将涵盖至少一些你可以用于以非文本形式与用户交互的各种方法和技术。

安装 pygame 可能有点麻烦。取决于支持哪种视频和音频后端，你需要编译我们提到的所有优化的 C 和汇编代码。对于你的树莓派，最简单的解决方案是使用 `sudo apt-get install python-pygame` 来处理所有潜在的麻烦。主页（pygame.org）上可用的文档非常详尽。有几个可用的教程，甚至还有一个配方部分，你可以在其中找到概述特定效果和交互技术的配方。

第一步是导入 pygame 模块。Pygame 提供了一个完整的多媒体子系统，因此在使用其提供的任何功能之前，你需要调用 `pygame.init()`。这会初始化所有内容并为你加载模块内容。

### 在最敏感的代码部分中，使用了优化的汇编语言

pygame 旨在尽可能具有可移植性。为了做到这一点，它支持许多不同的图形后端，从 OpenGL 甚至使用 ASCII 文本显示图形。它被设计为利用所有可用的计算资源，即 CPU 和 GPU，来进行处理此类文件所需的计算。为了从硬件中获得最佳性能，几个最重的函数是用优化的 C 语言编写的。这能带来 10 到 20 倍的速度提升。在最敏感的代码部分，使用优化的汇编语言以获得更多的性能。这意味着即使是你的树莓派，在有限资源下也能获得相当令人印象深刻的输出。

我们将从向用户显示视频开始。你首先需要的是一个实际显示视频的地方。当你调用 `pygame.init()` 时，pygame 子系统应该已经为你的当前设备创建了最佳显示模式的显示对象。你可能需要其他内容以使你的程序按你期望的方式运行。你可以使用函数 `pygame.display.set_mode()` 创建一个新的图形显示，其中你可以给该函数一个包含宽度和高度值的序列。你实际绘制图像的对象在 pygame 中称为 surface（表面）。你刚创建的显示有一个关联的 surface 对象。在这个 surface 上绘制的任何内容会立即显示在屏幕上。然而，这通常不是你要做的。常用的技术是创建一个离屏绘图区域并在那里进行绘制。然后你可以一次性将图像的整个内容转储到实际显示中。这比试图向用户查找数据要有效得多。这种将图像数据转储到屏幕的操作由 surface 对象的 `blit()` 函数处理。它从另一个 surface 获取数据并将其移动到第二个 surface 上的位置。为了让该 surface 在物理监视器上显示，你需要调用 `flip()` 函数。此函数将整个屏幕作为显示的最后一步转储到物理硬件中。

我们将探讨的第一种使用方法是加载整个图像文件到 Python。函数 `pygame.image.load()` 会读取图像文件并将其加载到新的 surface 对象中。默认情况下，pygame 只能加载未压缩的 BMP 文件。load 函数包含一个转换层，可以处理和导入其他几种格式，如 JPEG、GIF、PNG 等。对于这些其他格式中的某些格式，你可能希望调用图像的 `convert()` 方法将其转换为自然格式。这样使用会更快。当你想要保存图像时，你的选择更有限，因为你只能保存为 BMP、TGA、PNG 和 JPEG 格式。如果你需要不同的格式，你总可以在 pygame 保存后对其进行转换。

无论你是从加载的图像还是从空白 surface 开始，你可能都希望能绘制在它上面。在 `pygame.image` 命名空间下有一整套绘图函数，赋予你这种功能。所有这些函数的第一个参数都是要绘制的 surface。这个 surface 可以是之前加载的图像或空白画布。例如，你可以使用函数 `pygame.image.circle(Surface, color, pos, radius, width=0)` 绘制一个圆。此函数在 surface 对象上的给定位置绘制一个给定半径的圆。width 参数告诉 pygame 如何将圆的圆周宽度设置。如果 width 设置为零，则意味着你想画一个实心的、填充的圆。

