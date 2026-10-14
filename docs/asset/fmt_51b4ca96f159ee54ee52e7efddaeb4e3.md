
你需要添加一个条件来选择图像。通过从 `example1.png` 开始每张图像，创建一个名为 `players` 的新变量来存储当前玩家。使用 `random(players + "png")` —— 注意，在使用 `players` 之前需要将其转换为字符串。一旦选择了玩家，就显示下一个。添加一个条件来检查你是否到达了最后一张图片。例如，如果你有五张图像，则使用：

如果你等不及本教程的下部分了，你可以玩 Python 版本的游戏。该 HAT 具有简单的逻辑来计算每局游戏的获胜者：`python/43d0f2ff4`

```python
from sense_hat import SenseHat
sense = SenseHat()
x = (255, 0, 0) # 红
question_mark = {
    X, O, X, O, X,
    X, O, O, O, X,
    X, O, X, O, X,
    X, O, O, O, X,
    X, O, X, O, X
}
```

```python
if players == 5:
    players = 0
```

```python
sense_set_pixel(question_mark)
```

... 当到达最后一张图像时并将变量设为零。这将加载第一张图片并重新开始循环。

## 09 为每个 LED 编写代码：第二部分

为了给你的图像添加更多颜色，创建一个新变量并使用相同的帧分配 RGB 值。将你的代码替换为下面的示例以创建一个新图像。在 `http://www.colorpicker.com` 获取所有 16,737 种颜色的 RGB 值。

```python
import time
while True:
    player = random.choice(players + "png")
    players = players + 1
    time.sleep(1)
    if players == 5:
        players = 0
```

```python
X = (255, 0, 0) # 红
O = (255, 255, 255) # 白
new_image =
```

## 12 清除图像

在循环图像时，LED 将根据你代码的要求开启和关闭。有时你需要一次关闭所有 LED。要清空 HAT，请使用 `sense.clear()`。

![](img/287427b4a3b7d7792fc1ca7834fce232_169_1.png)

```
B, O, B, O, O, X
B, O, O, O, O, X
B, B, O, O, O, X
B, B, O, O, O, X
B, O, B, O, O, X
B, O, B, O, O, X
```

![](img/287427b4a3b7d7792fc1ca7834fce232_169_2.png)

## 13 在 pygame 中设置摇杆

HAT 配备了一个小型多方向摇杆，经过编程可以响应方向。石头剪刀布游戏利用摇杆来选择胜者和败者。通过选择其中一个，玩家可以在 pygame 窗口移动。查看第 1 行和第 2 行。接下来，由于游戏在 HAT 上运行，窗口是禁用的。你可以使用 `pygame.display.set_mode(640, 480)` 第 5 行来增加尺寸。

```python
import pygame
from pygame.local import *
### Setup Pygame ##
pygame.init()
pygame.display.set_mode((640, 480))
```

![](img/287427b4a3b7d7792fc1ca7834fce232_169_3.png)

| 简单帧 |

| 导出到控制台 |

| 导出到 png |

| 先清除 |

| 行 |

| 在 LED 上播放 |

Sense HAT 网格编辑器可以轻松地生成代码

## 14 添加摇杆控制

要添加摇杆，创建一个名为 `running` 的变量并设置为 True `1`。然后添加一条语句（第 2 行）持续检查 HAT 是否向左移动。我们将使用右下角的微型摇杆作为我们选择的输入。

![](img/287427b4a3b7d7792fc1ca7834fce232_170.png)

程序在第 4 行检查事件，并在第五行后重启图片。第 5 行检查条件是否满足：键盘上按下 `K_UP` 键对应于摇杆向上（第 6 行）。最后，使用 `print` 语句测试摇杆移动是否正常（7）。将其适配到你的项目中。

```python
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.KEYDOWN and playersChoice == 5:
            if event.key == K_UP:
```

一旦你循环并选择了图片，就可以选择。这是通过按下摇杆向下实现的，即 Return 键。第 2 行，`if event == RETURN` 检查此处，然后循环停止并将图像存储在 `playersChoice` 中，稍后与计算机的选择进行比较并计算胜者。

## 15 选择图像

你编写了 `pygame` 来移动并检查摇杆是否移动。这个游戏允许玩家选择代表他们选择的图像 —— 例如替换第 11 行的打印。作为基础，使用 `load_image(playersChoice) + ".png"` 将图像添加到 LCD，然后使用 `playersChoice += 1` 更新 `playersChoice` 直到它返回 0，循环从图片重新开始：“结束并移动主游戏”。

## 17 RPOLS

你有一个石头剪刀布游戏的基本结构。该游戏允许你循环五张图像，每张代表一个：石头、剪刀、蜥蜴或布。在下部分，本教程将涵盖游戏机制并组合以完成 RPSLS 游戏。所有动作的视频可以在此处：`youtube.com/watch?v=TZwkFM`，同时创建你的 8x8 像素艺术。

# 在树莓派上使用 Python

# 核心 HAT：第二部分

# 使用上一个教程的技巧创建一个 HAT 版本的 RPSLS，现在你已经在现实生活中玩过石头剪刀。这个版本的问题是只有三种结果或其他平局。Sam 引入了另一个版本，增加了“布”和“蜥蜴”；带有星际迷航标志显示“生命”。石头被剪刀和石头击碎；此教程将引导你创建 HAT 版本的游戏。

![](img/287427b4a3b7d7792fc1ca7834fce232_171_0.png)

矩阵上的每个 LED 都可以从图像文件自动设置。例如，可以加载蜥蜴的图像，计算颜色和位置，然后启用相应的 LED。图像需要 8x8 像素以适应 LED 矩阵。修改结构以适应蜥蜴，并将其保存在程序相同的文件夹中。

## 01 使用 Sense HAT 导入内容

当你完成本教程时，你将有一个包含五个 8 图像的文件夹，每个代表一个：石头、剪刀、蜥蜴和布。当程序运行时，它会要求你使用摇杆选择选择。按任意键进入。计算机选择一个随机项目。每张图片被分配一个值，并用于找到两个值的模。余数的值决定结果，如：

## 02 导入模块

启动树莓派并打开终端。输入 `nano edit` 加载 Python 3 编辑器。导入模块（一行）和 SenseHAT 模块（一行）。你的程序使用 `random` 模块处理游戏的计算机选择。导入 `random` 模块（四行）：

```python
import pygame
import random
from sense_hat import SenseHat
import random
import time
```

## 03 滚动消息

游戏期间，通过滚动 LED 矩阵的消息更新消息。SenseHAT API 将此过程简化为一行代码：`sense.show_message("This is a message!")`。你的消息将在 Sense HAT 的 LED 上滚动。通过更改 `text_colour=(255, 0, 0)` 设置 RGB 值和 `scroll_speed=50` 来更改消息字符间的间距和滚动时间。尝试以下代码：

```python
sense = SenseHat()
sense.show_message("Hello Developer", text_colour=[255, 0, 0])
```

## 04 映射 LED 图像

图像由像素组成，像素组合形成一张整体图片。

```python
from sense_hat import SenseHat
```

```python
sense = SenseHat()
sense.load_image("lizard.png")
```

## 05 创建变量并初始化 Pygame
