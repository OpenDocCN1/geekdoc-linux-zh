
```python
import turtle
pat = turtle.Turtle()
for i in range(10):
    for i in range(2):
        pat.forward(100)
        pat.right(60)
        pat.forward(100)
        pat.right(120)
pat.right(36)
```

点击“运行（Run）”图标，观察海龟：它会像之前一样画出一个平行四边形，但在完成后它将旋转 30 度并画出另一个，再一个，以此类推，直到屏幕上出现十个重叠的平行四边形 – 看起来有点像雪花（图 5-10）。

![](img/0aff4cdab15427839fb48fd7c6f677d3_103_0.png)

图 5-10：重复形状以制作更复杂的形状

# 树莓派初学者官方指南

虽然机器人海龟在大张纸上用单色绘制，Python 的模拟海龟可以使用多种颜色。添加新的第 3 和第 4 行，将现有的行向下推：

```python
turtle.Screen().bgcolor("blue")
pat.color("cyan")
```

再次运行你的程序，你将看到新代码的效果：海龟绘图窗口的背景颜色已变为蓝色，而雪花现在是青色（图 5-11）。

![](img/0aff4cdab15427839fb48fd7c6f677d3_104_0.png)

图 5-11：更改背景和雪花的颜色

你也可以使用 `random` 库从列表中随机选择颜色。回到程序顶部，将以下内容作为第 2 行插入：

```python
import random
```

将现在第 4 行的背景颜色从 `'blue'` 改为 `'grey'`，通过插入新的第 5 行创建一个名为 `'colours'` 的新变量：

```python
colours = ["cyan", "purple", "white", "blue"]
```

> 美式拼写
>
> 许多编程语言使用美式英语拼写，Python 例外：更改海龟笔颜色的命令拼写为 `color`，如果你按照英式英语拼写为 `colour`，它将无法工作。不过，变量可以使用任何你喜欢的拼写 – 这就是为什么你能够调用新变量 `colours` 并让 Python 理解它的原因。

## 第 5 章 使用 Python 编程

这种类型的变量被称为列表（list），用方括号标记。在这种情况下，列表填充了雪花分段的可能颜色 – 但你仍然需要告诉 Python 在每次循环重复时选择一个。在程序的最后面，输入以下内容 – 确保其缩进四个空格，使其成为外层循环的一部分，就像上面的那行一样：

```python
pat.color(random.choice(colours))
```

点击“运行”图标，雪花-忍者星将再次被画出。这次，Python 在绘制每个花瓣时将从你的列表中随机选择一种颜色 – 为雪花带来愉悦的多彩完成效果（图 5-12）。

![](img/0aff4cdab15427839fb48fd7c6f677d3_105_0.png)

图 5-12：使用随机颜色使雪花看起来更真实

```python
from pygame.locals import *
from time import sleep
from random import randrange
```

导入指令的工作方式与之前的导入指令不同，它允许你只导入库中需要的部分，而不是整个库。接下来，你需要设置 Pygame；这被称为初始化。Pygame 需要知道玩家显示器或电视的宽度和高度，这被称为分辨率。输入以下内容：

```python
pygame.init()
width = pygame.display.Info().current_w
height = pygame.display.Info().current_h
```

设置 Pygame 的最后一步是创建它的窗口，Pygame 将其称为屏幕（screen）。输入以下内容：

```python
screen = pygame.display.set_mode((width, height))
```

```python
pygame.quit()
```

注意中间的空行；这里将是你编写程序的地方。不过，先点击运行（Run）图标，将你的程序保存为 Spot the Difference，然后观察：Pygame 将创建一个窗口并填充黑色背景，随后它在执行到退出指令时会立即消失。除了 shell 中的一条短消息（图 5-14）外，程序目前已经取得了很大成就。

![](img/0aff4cdab15427839fb48fd7c6f677d3_109_0.png)

> 图 5-14: 你的程序可以运行，但目前还做不多

# 官方树莓派新手指南

要显示你的找不同点图片，在 `pygame.quit()` 上方的空间输入以下行：

```python
difference = pygame.image.load('spot_the_diff.png')
```

为了确保图像填充整个屏幕，你需要将其缩放以匹配显示器或电视的分辨率。输入以下内容：

```python
difference = pygame.transform.scale(difference, (width, height))
```

现在图像已经在内存中了，你需要告诉 Pygame 实际上在屏幕上显示它——这个过程被称为绘制（blitting）或位传输。输入以下内容：

```python
screen.blit(difference, (0, 0))
pygame.display.update()
```

这些行中的第一行将图像复制到屏幕上，从左上角开始；第二行告诉 Pygame 重绘屏幕。如果没有第二行，图像将处于内存中的正确位置，但你永远无法看到它！

点击运行图标，图像将短暂地出现在屏幕上（图 5-15）。

![](img/0aff4cdab15427839fb48fd7c6f677d3_110_0.png)

图 5-15: 你的找不同图片

为了让图像显示更久，请在 `pygame.quit()` 正上方添加以下行：

```python
sleep(3)
```

再次点击运行，图像将在屏幕上停留更久。在在 `pygame.display.update()` 行下方输入以下内容来添加你的惊喜图片：

```python
zombie = pygame.image.load('scary_face.png')
zombie = pygame.transform.scale(zombie, (width, height))
```

添加一个延迟，让僵尸图片不要立即出现：

```python
sleep(3)
```

然后将图像绘制到屏幕上并更新它，以便玩家看到：

```python
screen.blit(zombie, (0,0))
pygame.display.update()
```

点击运行图标并观察发生了什么：Pygame 将加载你的找不同图片，但三秒后，它将被替换为恐怖的僵尸（图 5-16）！

![](img/0aff4cdab15427839fb48fd7c6f677d3_111_0.png)

> ▲ 图 5-16: 它将给某人一个恐怖的惊喜

不过，设置三秒的延迟会让事情变得有点容易预测。将 `screen.blit(zombie,(0,0))` 上方的 `sleep(3)` 行更改为：

```python
sleep(randrange(5, 15))
```

这会选取 5 到 15 之间的随机数，并让程序延迟那么久。接下来，在你的 `sleep` 指令上方添加行来加载音频文件：

```python
scream = pygame.mixer.Sound('scream.wav')
```

移动到你的 `sleep` 指令下方，在新的一行输入以下内容开始播放声音，这样它就在恐怖图片真正显示给玩家之前生效：

```python
scream.play()
```

最后，在 `pygame.quit()` 上方输入以下行，告诉 pygame 停止播放声音：

```python
scream.stop()
```

点击运行图标并欣赏叹我的杰作：在经过几秒无害的找不同后，你恐怖的僵尸将伴随着一声毛骨悚然的尖叫出现——足以让你的朋友大一跳！如果你想让僵尸图片在声音开始播放之前出现，可以在 `scream.play()` 指令之后、`screen.blit` 指令之前添加一个小的延迟来补偿：

```python
sleep(0.4)
```

你完成的程序应该是这样的：
