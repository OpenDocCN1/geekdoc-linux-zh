
接下来，创建变量来存储玩家的选择之一，并跟踪当前显示在全局时钟上的图片。将这些设置为全局变量，以便程序的其他部分可以访问它们或返回返回的值。然后，使用 `pygame` 窗口输入显示未用于游戏的结果，将其设置为较小尺寸。带有 `sense.load_image("lizard.png")` 的第一个代码从你的文件夹加载此图片。现在 LED 太亮了，添加 `size, light=True` 来返回选择。

# 使用带有 Pi

```python
load_image(playersChoice + " .png") 第 13 行且
递增。循环从头重新开始，并检查
摇杆移动并显示相关的图片文件：

def main():
    ## 玩家选择##
    running = True
    global playersChoice
    while running:
        set_rotation(0)
        for event in pygame.get_event_list():
```

像素艺术灵感：你需要一张石头、布子、剪刀的图片，并且带有透明背景的 8x8 像素艺术图。查看 `http://www.tumblr.com/tag/pixelart17242776680`

- if `event.type == KEYDOWN` and `playersChoice < 5`:
    if `event.type == K_UP`:
        print(`playersChoice`)
        sensor.load(str(`playersChoice + " .png"`))
        `playersChoice += 1`
    if `playersChoice == 5`:
        `playersChoice = 0`

## 检查摇杆

创建另一个持有游戏主循环的函数。通过添加全局变量，`set_rotation(0)`，使机器位置正确。下一个事件 `pygame.get_event()`：摇杆被用于通过 LED 灯光的循环进行检查。如果事件类型 == `KEYDOWN` 且 `playersChoice < 5`：检查数字是否已移动。如果它等于该数字且小于 5。如果它小于 5，则使用 `sense` 将相应的图片加载到 LED 中。

## 08 选择你的项目

当你滚动滚动菜单时，你可以选择一个项目进行游戏。按下摇杆并向下移动。

![](img/287427b4a3b7d7792fc1ca7834fce232_172_0.png)

### 完整代码列表

```python
import pygame
from pygame.locals import *
from sense_hat import SenseHat
import random
```

```python
return Scissors
elif number == 4: 因为值 5 会重置为 0，零 - 1 = -1 #
return "Scissor" 供计算机
```

```python
global playersChoice
global computer_choice
global count
```

```python
def main():
    ##玩家选择##
    while loop is running True
    global playersChoice
    global computer_choice
    while running:
        set_rotation(0)
```

```python
## 设置 Pygame 屏幕
pygame.init()
game.display.set_mode((140, 180))
## 初始化 SenseHat
sense = SenseHat()
sense.load_image(" .png")
sense.low_light = True # 保存你的眼睛
```

```python
if event.type == KEYDOWN and playersChoice < 5:
    if event.type == K_UP:
        print(playersChoice)
        sense.load_str(playersChoice + " .png")
        playersChoice += 1
    if playersChoice == 5:
        playersChoice = 0
```

```python
playersChoice = 0
gameRunning = True

## 数字转换为石头、蜥子、布子等：
number_to_name(number):
    if number == 0:
        return "Rock"
    elif number == 1:
        return "Spawn"
    elif number == 2:
        return "Paper"
    elif number == 3:
        return "Lizard"
    elif number == -1: # 因为值 5 会重置为 0，零 - 1 = -1
```

```python
## 检查 'select' / 输入
if event.type == KEYDOWN:
    if event.type == K_RIGHT:
        running = False
        break
    ''结束循环并进入 main
```

```python
## 玩家选择的消息
print("Your Choice is", playersChoice) #test
```

![](img/287427b4a3b7d7792fc1ca7834fce232_172_1.png)

# 使用带有 Pi

## 创建 8x8 图片

返回键。如果行 `event == RET_RETURN`，则响应摇杆。然后使用 `running = False`。最后，跳出循环到游戏：

一个简单的方法来创建你的图片。使用此操作 LED 可以改变颜色并移动图片。安装 Pi Zero 然后打开终端并执行 `sudo pip install`。一旦完成，输入 `git clone https://github.com/pi-pi/led-grid`，然后 `cd led-grid`，运行 `python3 led-grid.py` 应用。

```python
item.computerMessage=number_to_name(number). 现在使用
sense.show_message("", text_colour=(0, 150, 255),
scroll_speed=06) 来显示计算机的：
```

```python
# 关于计算机选择的消息
print("The computer chooses", computer_choice)
number=computer_choice
computerMessage=number_to_name(number)
if computerMessage==first:
    sense.set_rotation(0)
```

```python
## 检查 'select' / 输入
event_type = KEYDOWN
if key == RET_RETURN:
    running = False
```

# 09 更新状态

一旦你做了选择，计算机会在 LED 上创建一个新消息。然后创建数字 `players_choice` 给它。使用步骤六中的函数选择玩家并在行显示消息，在两个值之间速度。

```python
sense.show_message("", text_colour=(0, 150, 255),
scroll_speed=0.08)
sense.show_message("", text_colour=(0, 150, 255),
scroll_speed=0.08)
sense.load_image(computer_choice + ".png")
```

# 10 计算机的选择

现在计算机随机选择一个 1 到 5 之间的数字，所以 `count=random.randint(5)`。这是一个随机数，直到玩家选择一个从循环中减去的数字并检查选择的值大于零。然后将选择显示在 LED 矩阵 `sense.load_image(computer_choice + ".png")`。

```python
## 选择
计算机从 `count=random.randint(5)` 选择一个
count=1
sense.set_rotation(0)
computer_choice=random.randint(5)
print(computer_choice)
sense.sleep(0.1)
sense.load_image(computer_choice + ".png")
```

# 11 游戏状态更新
