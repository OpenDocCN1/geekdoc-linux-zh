
配置中只剩下两步。首先，我们需要获取并安装 `Nanpy` 包在 Pi 上。我们喜欢的方式是通过 Git 克隆它。在终端中导航到你的主文件夹（`cd ~`）并按顺序在终端中执行以下操作。

```bash
$ easy_install nanpy
$ sudo apt-get install git
$ git clone https://github.com/nanpy/nanpy.git
```

### 05 配置你的 Arduino Uno

为什么我们要克隆原始的 Git 仓库？`Nanpy` 依赖于 Arduino 固件的更新才能正确工作，因此你需要从 `nanpy` 项目目录访问固件文件夹来完成它。在将以下内容输入终端之前，请将你的 Arduino Uno 插入树莓派的备用端口。小心：以下操作需要一些时间！

```bash
$ cd nanpy/firmware
$ export BOARD=uno
$ make
$ make upload
```

### 06 用你的 Pi 测试 Arduino

安装终于完成后，我们可以测试设置以确保它正常工作。在我们对右侧代码段进行真正的“你好世界！”应用程序之前，让我们首先确保 `Nanpy` 已正确安装并且 Pi 和 Arduino 之间的连接正在工作。从你的主文件夹（`cd ~`），在终端中输入以下命令：

```bash
$ nano nanpy_test.py
```

在 `nano` 编辑器中，只需写入：

```python
from nanpy import Arduino
```

现在按 `Ctrl+X`，`Y`，然后按 `Enter` 保存你的新文件。最后，在终端中输入：

```bash
$ python nanpy_test.py
```

如果你没有看到错误，那么一切都应该正常工作。现在你可以开始跨页面玩代码，开始学习如何操作 `Nanpy`。

#### 完整代码列表

```python
# Like all good hardware-based 'Hello, World!' applications, we'll start
# by making the light on the Arduino board flicker off and on.
from nanpy import Arduino
from time import sleep

Arduino.pinMode(13, Arduino.OUTPUT)
for i in range(10):
    Arduino.digitalWrite(13, Arduino.HIGH)
    sleep(2)
    Arduino.digitalWrite(13, Arduino.LOW)
    sleep(2)

# This will make the light controlled by pin 13 on the Arduino
# turn on and off every two seconds ten times.

# You can also assign pins a name, to make your code more readable.

light = 13
Arduino.pinMode(light, Arduino.OUTPUT)

# You can also assign multiple pins at the same time:

red_pin = 3
green_pin = 5
blue_pin = 9

for pins in (red_pin, green_pin, blue_pin):
    Arduino.pinMode(pins, Arduino.OUTPUT)

# if you've got an LED screen for your RASPi you'll probably
# find it works out of the box with Nanpy. Just make sure you
# assign the right pin numbers for your screen:

from nanpy import (Arduino, Lcd)

screen = Lcd([7, 8, 9, 10, 11, 12], [16, 2])
screen.printString('Hello, World!')

# If you're using potentiometers, buttons or analog sensors,
# you'll need to assign them as inputs
knob = 0
Arduino.pinMode(knob, Arduino.INPUT)

value = Arduino.analogRead(knob)
for i in range(10):
    print ('The value of the knob is:', value)
    sleep(1)

# Sometimes you want to delay what the arduino does.
# This can help you get consistent, solid readings
def get_value():
    value = Arduino.analogRead(knob)
    Arduino.delay(100)
    return value
for i in range(10):
    print('The value is:', get_value())
```

![](img/a1548a579bd09ff29b2b92de3f565e63_22_0.png)

**你将学到**

**1. 发挥优势**

虽然 `RASPi` 比 `Arduino` 强大得多，但在与真实世界交互方面，`Arduino` 更具优势。利用它们两者的优势来创建更好的项目。

## 10 个实用的树莓派项目

### 制作一个树莓派三色彩灯

**利用 Arduino 的力量，完成仅靠树莓派无法实现的项目**

**所需材料**

- `Arduino Uno`
- 面包板
- 一组原型连接线缆
- `RGB LED`（共阴极）
- 3 个电位器
- 3 个 330 欧姆电阻

这是一个非常有吸引力的 `RGB` 彩灯的优秀原型——非常适合作为夜灯或氛围灯。

在前一个项目中，我们向你展示了如何使用 `Arduino` 微控制器帮助树莓派掌握新技能，从而极大地扩展你项目的功能范围。借助额外 12 个支持 `PWM` 和模拟输入的引脚，你可以轻松添加多个舵机、模拟传感器，甚至添加摇杆等输入设备。

在这个项目中，我们将通过创建一个三色彩灯来演示这一点，该彩灯使用三个电位器（旋钮）来控制 `RGB LED` 灯光中的三种颜色。通过它，你可以调出彩虹中的大多数颜色。正如你所料，仅使用树莓派实现这一点会困难得多。

#### 01 使用 Arduino 编程

你需要按照前一个项目中的步骤正确配置树莓派和 `Arduino Uno`。你还需要确保你拥有左侧列表中所有组件。电阻理想情况下应为 330 欧姆，但如果只有更高阻值的电阻也可以。

`Arduino` 可以作为“入门套件”的一部分购买，其中包含此类组件，但快速访问 `www.cpc.co.uk` 也应该能补齐任何缺漏。

![](img/a1548a579bd09ff29b2b92de3f565e63_23_0.png)

#### 02 填充面包板

![](img/a1548a579bd09ff29b2b92de3f565e63_24_0.png)

这个项目的电路乍一看可能有点复杂，但实际上并没有太多内容。正如你所期望的，我们希望使用支持 `PWM` 的引脚来控制 `LED` 灯光（以便精细控制亮度），而电位器（`pots`）则通过模拟引脚读取。

#### 03 连接 Arduino 和树莓派

假设你不打算立即自己编写代码，你可以从光盘或网站上获取代码，并将其放入主文件夹。将 `Arduino` 的 `USB` 线缆插入树莓派后，只需运行以下代码即可：

```python
python RGB_Mixer.py
```

调整对应 `LED` 颜色的电位器，颜色应该会改变。如果电位器调节的是错误的颜色，只需互换即可。你可以使用乒乓球或塑料杯盖住灯光，效果会非常好。

**完整代码列表**
