

## 教程：使用 Sense HAT 制作鸡蛋掉落游戏

![](img/1f330653f83dcf0397f7d224ce8bbc16_69_0.png)

Dan Aldred 是树莓派认证教育者，也是 CAS 的首席学校教师。他领导了 Astro Pi 中学组竞赛的获胜团队，并出现在 DfE 的“鼓舞人心的教师”电视广告中。他最近从 Skyacademy 毕业，曾将搭载树莓派的高空气球发射至超过 31,000 米的平流层。

### 使用 Tim Peake 上校在国际空间站上所使用的同款硬件，编写你自己的接蛋游戏

一些最基础且重复性强的游戏往往也是最有趣的。想想 Flappy Bird、井字棋甚至接球游戏。本教程将向你展示如何创建一个简单的“接蛋”游戏，充分利用 Sense HAT 的一些特性。首先，通过代码让一个鸡蛋——即一个黄色 LED——每秒掉落一次，并在 LED 矩阵的最底行放置一个篮子——即一个棕色 LED。利用 Sense HAT 的加速度计读取并反馈你向左或向右倾斜 Sense HAT 的动作，从而移动篮子以接近鸡蛋。成功接住鸡蛋后，游戏重新开始，一个新的鸡蛋会从随机位置掉落……但如果你错过了，鸡蛋就会破碎，游戏结束！你的程序会实时告知你当前的进度，游戏结束时，会显示你的最终得分。如果你没有 Sense HAT，可以使用带有 PIXEL 操作系统的树莓派上的模拟器。你还可以在此观看蛋掉落游戏的实际演示：youtube.com/watch?v=QmjHMzuzWjQ

### 你需要准备的物品

-   Sense HAT
-   带有 Sense HAT 模拟器的 Pixel OS 版本的 Raspbian

```python
game_over = False
basket_x = 7
score = 0
```

### 01 导入模块

首先，打开你的 Python 编辑器并导入 SenseHAT 模块，见第 1 行。然后导入 time 模块，见第 2 行，以便你可以为程序添加暂停。第 3 行的 random 模块用于从 LED 顶部选择一个随机位置，鸡蛋将从该位置掉落。为了省去重复输入 'SenseHAT' 的麻烦，将其赋值给一个变量，见第 4 行。最后，将所有 LED 设为关闭状态，以清除之前的分数和游戏数据，见第 5 行。

```python
from sense_hat import SenseHat
import time
import random
sense = SenseHat()
sense.clear()
```

### 02 设置变量

接下来，创建变量以存储各种游戏数据。在第 1 行，创建一个全局变量来存储游戏状态。这记录了游戏是在进行中还是已结束。全局变量使得该状态可以在游戏后期与其他程序部分配合使用。在第 2 行，创建另一个变量来存储你的游戏得分。将第 3 行的 game_over 变量设置为 False，这意味着游戏尚未结束。矩阵中每个 LED 的位置由 x 和 y 坐标表示，最上面一行为编号 0，最下面一行为编号 7。创建一个变量来存储篮子的位置，篮子被设置在 LED 的最底行，即编号 7 的位置。最后，将得分设为零。

```python
global game_over
global score
```

### 03 测量篮子移动：第 1 部分

篮子通过向左或向右倾斜 Sense HAT 来控制，这会改变俯仰角（pitch）。创建一个函数来包含代码，该函数将用于响应移动并移动篮子。在第 1 行，命名函数，包含俯仰角读数以及篮子的位置 basket_x。使用 sense.set_pixel 在 LED 矩阵的右下角开启一个 LED，坐标为 (7,7)，见第 2 行。然后将篮子的下一个位置设置为当前位置，以便函数再次运行时进行更新。这会用篮子的新位置更新变量并开启相应的 LED。这产生了一种篮子似乎移动了的视觉效果。

```python
def basket_move(pitch, basket_x):
    sense.set_pixel(basket_x, 7, [0, 0, 0])
    new_x = basket_x
```

### 04 测量篮子移动：第 2 部分

函数的第二部分包含一个条件判断，检查俯仰角和篮子当前的位置。如果俯仰角在 1 到 179 之间且篮子不在位置 0，则说明 Sense HAT 向右倾斜，因此篮子向右移动。第二个条件检查数值是否在 359 到 179 之间，这意味着倾斜方向向左，见第 3 行。最后一行代码返回篮子的 x 位置，以便在代码后面使用——参见第 13 步。

```python
if 1 < pitch < 179 and basket_x != 0:  
    new_x -= 1
elif 359 > pitch > 179 and basket_x != 7:
    new_x += 1
return new_x,
```

### PIXEL 灵感

Johan Vinet 有一些出色的、具有启发性的 8x8 像素艺术作品示例，其中包含一些著名角色，向你展示你可以用 64 个彩色像素创造出什么。joh.anvinet.tumblr.com/image/127476776680

![](img/1f330653f83dcf0397f7d224ce8bbc16_70_0.png)

### 05 为你的游戏创建图像

图像是由像素组合而成的，这些像素共同构成一幅完整的图片。矩阵上的每个 LED 都可以自动从图像文件中设置。例如，可以加载一张鸡的图片，计算其颜色和位置，然后启用相应的 LED。图像尺寸需要为 8x8 像素，以适应 LED 矩阵。下载测试图片文件 **chicken.png**，并将其保存到你的程序所在的同一文件夹中。使用此处代码在新的 Python 窗口中打开并加载鸡的图片（第 3 行）。Sense HAT 会为你完成剩下的繁重工作。

```python
from sense_hat import SenseHat
sense = SenseHat()
sense.load_image("chicken.png")
```

### 06 创建你自己的 8x8 图像

使用 LED 创建自己图像的最简单方法是使用一款极其流行的屏幕程序，它允许你实时操作 LED。你可以更改颜色、旋转图像，并将图像导出为代码或 8x8 PNG 文件。

首先，你需要安装 Python PNG 库：打开终端窗口并输入：

```bash
sudo pip3 install pypng
```

完成后，输入：

```bash
git clone https://github.com/jrobinson-uk/RPL_8x8GridDraw
cd RPL_8x8GridDraw
```

安装完成后，移动到 RPI 文件夹：

```bash
cd RPL_8x8GridDraw
```

### 完整代码列表

```python
from sense_hat import SenseHat
## EGG Drop ##
## Code by dan_aldr ##

import time
import random
sense = SenseHat()
sense.clear()

global game_over
global score

game_over = False
basket_x = 7
score = 0

def basket_move(pitch, basket_x):
    sense.set_pixel(basket_x, 7, [0, 0, 0])
    new_x = basket_x
    if 1 < pitch < 179 and basket_x != 0:
        new_x -= 1
    elif 359 > pitch > 179 and basket_x != 7:
        new_x += 1
    return new_x,

def main():
    global game_over

    sense.show_message("Egg Drop", text_colour = [255, 255, 0])
    sense.set_rotation(90)
    sense.load_image("chick.png")
    time.sleep(2)
    sense.set_rotation()

    countdown = [3, 2, 1]
    for i in countdown:
        sense.show_message(str(i), text_colour = [255, 255, 255])

    basket_x = 7
    egg_x = random.randrange(0,7)
    egg_y = 0
    sense.set_pixel(egg_x, egg_y, [255, 255, 0])
    sense.set_pixel(basket_x, 7, [139, 69, 19])
    time.sleep(1)

    while game_over == False:
        global score
        pitch = sense.get_orientation()['pitch']
        basket_x, = basket_move(pitch, basket_x)

        sense.set_pixel(basket_x, 7, [139, 69, 19])
        time.sleep(0.2)
```

### 07 创建并导出你的图像

现在输入以下命令：

```bash
python3 sense_grid.py
```

...来运行该应用程序。

![](img/1f330653f83dcf0397f7d224ce8bbc16_71_0.png)

网格编辑器允许你从窗口右侧显示的一系列颜色中进行选择。只需选择颜色，然后单击网格上 LED 的位置；选择“在 LED 上播放”即可在 Sense HAT LED 上显示该颜色。使用“清除网格”按钮清除 LED，然后重新开始。最后，在导出图像时，你可以将其保存为 PNG 文件，然后应用上一步中的代码来显示图片，或者将布局导出为代码并将其导入到你的程序中。

```python
import time
import sense_hat
import random

sense = Sense_Hat()
sense.set_rotation(90)

def main():
    sense.show_letter("W", text_colour = [255, 255, 0])
    sense.show_letter("e", text_colour = [255, 255, 0])
    sense.show_letter("l", text_colour = [255, 255, 0])
    sense.show_letter("c", text_colour = [255, 255, 0])
    sense.show_letter("o", text_colour = [255, 255, 0])
    sense.show_letter("m", text_colour = [255, 255, 0])
    sense.show_letter("e", text_colour = [255, 255, 0])
    sense.show_letter(" ", text_colour = [255, 255, 0])
    sense.show_letter("t", text_colour = [255, 255, 0])
    sense.show_letter("o", text_colour = [255, 255, 0])
    sense.show_letter(" ", text_colour = [255, 255, 0])
    sense.show_letter("p", text_colour = [255, 255, 0])
    sense.show_letter("l", text_colour = [255, 255, 0])
    sense.show_letter("a", text_colour = [255, 255, 0])
    sense.show_letter("y", text_colour = [255, 255, 0])

def show_score(score):
    sense.show_letter(str(score), text_colour = [0, 255, 0])

def show_message(message):
    sense.show_message(message, text_colour = [255, 255, 0], scroll_speed=0.1)

def set_rotation(rotation):
    sense.set_rotation(rotation)

def load_image(image):
    sense.load_image(image)

def clear_grid():
    sense.clear()

def play_on_leds():
    sense.clear()

def sense_draw_image():
    sense.draw_frame([255, 255, 255])

def sense_clear():
    sense.clear()

def sense_show_letter(letter):
    sense.show_letter(letter)

def sense_show_message(message):
    sense.show_message(message)
```

```json
{
    "coordinates": [[0, 0], [8, 7]],
    "grid_colour": [255, 255, 0],
    "text_colour": [255, 255, 0],
    "frame": true,
    "export_png": true,
    "play_on_leds": true,
    "export_coco": false
}
```

### 08 显示消息：游戏开始

既然你已经有了一张图像，就可以创建控制整个游戏的函数了。创建一个名为 main 的新函数，见第 1 行，并添加以下代码：

```python
sense.show_message
```

...以显示游戏的欢迎消息，见第 3 行。数值 255、255 和 0 代表消息的颜色（在此示例中为黄色）。你可以编辑这些数值来选择自己喜欢的颜色。

```python
def main():
    global game_over
    sense.show_message("Egg Drop", text_colour = [255, 255, 0])
```

### 09 显示你的启动图像

一旦启动消息在 Sense HAT LED 矩阵上滚动完毕，你就可以显示你的游戏图像了，在此示例中是一只鸡。由于 Sense HAT 的方向和线缆位置，你需要将其旋转 90 度以面向玩家，见第 1 行。使用代码 sense.load_image 加载图像，见第 2 行。使用 time.sleep() 显示图像几秒钟，见第 3 行。请注意，从此类行开始，都要与前一行保持缩进对齐。

```python
sense.set_rotation(90)
sense.load_image("chick.png")
time.sleep(2)
sense.set_rotation()
```

![](img/1f330653f83dcf0397f7d224ce8bbc16_71_1.png)

### 10 倒数开始游戏

一旦启动图像显示完毕，用一个简单的从三到一的倒数让玩家为游戏做好准备。首先创建一个名为 countdown 的列表，存储数值 3、2 和 1，见第 1 行。使用 for 循环，见第 2 行，遍历这些数字并显示它们。这使用代码 sense.show_message(str(i)) 在 LED 上显示每个数字。你可以使用三部分 RGB 值 text_colour = [255, 255, 255] 来调整数字的颜色，见第 3 行。

```python
countdown = [3, 2, 1]
for i in countdown:
    sense.show_message(str(i), text_colour = [255, 255, 255])
```

### 11 设置鸡蛋和篮子

随着游戏开始，将篮子的水平位置，即“X”位置，设置为 7；这会将篮子放置在 LED 矩阵的右下角。现在将鸡蛋的 x 位置设置为 0 到 6 之间的随机位置，见第 2 行。这位于 LED 矩阵的顶部，确保鸡蛋并不总是从同一个起点落下。最后，将鸡蛋的 y 值设置为 0，以确保鸡蛋从 LED 矩阵的最顶端落下，见第 3 行。

```python
basket_x = 7
egg_x = random.randrange(0,7)
egg_y = 0
```

### 12 显示鸡蛋和篮子

在上一步中，你设置了鸡蛋和篮子的位置。现在使用这些变量来显示它们。在第 1 行，使用代码 sense.set_pixel 设置鸡蛋，随后跟上其 x 和 y 坐标。x 位置是 0 到 7 之间的随机位置，y 设置为 0 以确保鸡蛋从顶部开始。接下来，将颜色设置为黄色。（除非你的鸡蛋坏了，在这种情况下

