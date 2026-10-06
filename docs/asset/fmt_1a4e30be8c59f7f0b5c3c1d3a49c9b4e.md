
在构建平台方面，有无限的选择空间。四轮、履带和六足机器人都是可能的。我们本月的机器人平台风格是朋友——请查看第 76-77 页的评论。

## 在 Python 中创建移动函数

我们简单的电机测试无法实现这一点——我们需要能够进行控制，因此让我们添加一些可以随地调用的移动函数吧。

现在我们有一个外观非常漂亮的机器人，并且所有线都连接在正确的位置（除了可能需要的电机），我们可以插上树莓派并编写第一个控制电机的脚本。在轻松检查电机是否工作之前，我们希望能够妥善地控制并让它移动，为此我们需要创建自己的函数。

### 01 设置引脚

首先，我们将导入所需的类，并像之前电机测试那样设置引脚。

### 02 启用 PWM 支持

为了控制速度，我们将使用脉冲宽度调制 `PWM`。由于 `Enable` 引脚支持此并适用于两个方向：

```python
import RPi.GPIO as GPIO
from time import sleep
GPIO.setmode(GPIO.BCM)
GPIO.setup(24,GPIO.OUTPUT)
GPIO.setup(23,GPIO.OUTPUT)
GPIO.setup(18,GPIO.OUTPUT)
GPIO.setup(17,GPIO.OUTPUT)
GPIO.setup(11,GPIO.OUTPUT)
```

### 03 创建移动函数

Python 允许我们简化和复用代码，使其更易读。我们将利用这一点将想要的内容放入函数中保存。

```python
Motor1 = GPIO.PWM(24, 50)
Motor1.start(0)
Motor2 = GPIO.PWM(11, 50)
Motor2.start(0)
```

在 Python 中，通过将重复动作分组到一个定义中来实现。使用 `def` 块，我们可以轻松地传递速度等参数并方便地编写代码。我们还会在引脚上添加 `PWM`，以便设置电机应该运行的速度。

```python
def forward(speed):
    GPIO.output(24, True)
    GPIO.output(23, False)
    GPIO.output(18, True)
    GPIO.output(17, False)
    Motor1.dutyCycle(speed)
    Motor2.dutyCycle(speed)
```

### 04 如何更改速度

通过添加 `(speed)` 参数，我们可以向函数输入输入，将其结果——电机的速度返回回脚本。

```python
def backward(speed):
    GPIO.output(24, False)
    GPIO.output(23, True)
    GPIO.output(18, False)
    GPIO.output(17, True)
    Motor1.dutyCycle(speed)
    Motor2.dutyCycle(speed)
```

我们将设置引脚并设置输出；然后在两个引脚上启用 `PWM`。在接下来的代码块中，我们将创建函数，并给它们易记的名字，通过使用它们来向左向右移动。通过这种方法，我们只需要在最后写我们想要的内容。我们将告诉电机前进 10（即全速）持续 3 秒，然后向后退 3 秒。

### 05 让它移动

在调用脚本之前，最困难的工作已经完成了。为了让机器人移动，我们将使用变量：

```python
def stop():
    GPIO.output(24, False)
    GPIO.output(23, False)
    Motor1.dutyCycle(0)
    Motor2.dutyCycle(0)
```

```python
def left(speed):
    GPIO.output(24, False)
    GPIO.output(23, True)
    Motor1.dutyCycle(speed)
    Motor2.dutyCycle(speed)
```

```python
def right(speed):
    GPIO.output(24, True)
    GPIO.output(23, False)
    Motor1.dutyCycle(speed)
    Motor2.dutyCycle(speed)
```

`PWM` 用于通过快速开关改变电机等部件的电压。我们还可以通过分离（和右）来控制每个电机，允许我们原地转动。通过这种方法，意味着一个高移动性的机器人！在 Python 中，我们使用函数来重复代码段；这允许我们多次使用相同的代码并进行更改。我们想要精确地控制并让它移动。

![](img/511bb591be9ee7dc0f73776baf9a0548_24_0.png)

![](img/511bb591be9ee7dc0f73776baf9a0548_24_1.png)

# 树莓派机器人

## 安装微开关

给你的机器人触觉，并训练它在碰撞到东西时做出反应。现在我们有了一个可以随心移动的机器人，让我们进入最简单的交互形式：

添加触觉可以通过多种方式，但最快最简单的方法是以微开关的形式为机器人添加一些“触角”。它们并不小，但有探测机器人前面的手臂，适合安装在机器人正面。

触摸可能没有想象的那么复杂，但赋予机器人第一个感觉将有助于它导航路径，赋予它非常基础的智能。你可以尝试使用木棍或吸管扩展它。添加多个开关让机器人对周围有更好的感知，并允许使用非常简单的代码控制它的移动。它将是变量，我们只需要在正面添加开关。让我们创建电路并测试开始。

![](img/511bb591be9ee7dc0f73776baf9a0548_25_0.png)

![](img/511bb591be9ee7dc0f73776baf9a0548_25_1.png)

![](img/511bb591be9ee7dc0f73776baf9a0548_25_2.png)

## 零件列表

- 面包板
- 跳线导
- 2X 10 电阻
- 2 个微开关

### 额外开关

通过遵循电路并连接到空引脚，你可以轻松添加更多开关，而不只是跳线。

### 下拉电阻

由于我们处理的是数字逻辑，开关必须开启或关闭，电阻通过弱弱下拉引脚来帮助。

![](img/511bb591be9ee7dc0f73776baf9a0548_25_3.png)

### 3.3V 电源

由于树莓派没有过电压保护，我们不能输入超过 3.3V 的电压，否则会损坏处理器。

### NO NC

大多数开关标记为 `NO` 和 `NC`；分别代表常开（Normally Open）和常闭（Normally Closed）。开启简单意味着没有电流通过。

### 你的微开关已接线，让它们工作

现在开关已经安装好且很简单，但如提到的，重要的是记住树莓派只耐受 3.3 伏，所以我们只使用 3.3V 引脚而不是其他的

用于读取的 Python 代码非常简单且直接。由于每个 GPIO 引脚有一个开关，我们可以让 Python 在我们询问时告诉我们处于什么状态。我们想要做的第一件事是使用我们的库并将引脚设置为 BCM 模式。

```python
import RPi.GPIO as GPIO
from time import sleep
```

```python
GPIO.setup(GPIO.BCM)
```

创建一个 `True` 循环将创建一个永远 `true`无限循环。我们将输入状态存储在变量中，并使用 `if` 语句检查它是 1（已按下）还是 0（未按下）。我们将在屏幕上显示哪个开关被按下，这将帮助我们决定在哪个侧放置微开关。

```python
GPIO.setup(18, GPIO.IN)

while True:
    input = GPIO.input(18)
    if input:
        print("Left pressed")
    else:
        print("Right pressed")
    sleep(0.1)
```

> 显示哪个开关被按下

# 安装微型开关

构建你的 Linux 驱动机器人

## 完成“碰撞”机器人

是时候给机器人添加开关，并找一些墙壁进行测试了

我们将微型开关安装在机器人的正前方，使用双面胶或蓝丁胶（Blu-t）将其固定，这样它们在对上物体时就能伸出来。通过使用我们之前创建的碰撞功能，我们可以轻松地添加微型开关支持。

反向一秒钟然后停止。希望这段时间足够机器人离开我们现在看到的物体，现在我们只需要在继续之前的路径之前让左侧电机转动 2 秒。

通过重构代码来实现变体，例如为右侧电机创建一个函数，并在启动时运行它，以创建一个新路径并继续。

- 01 安装开关

将微型开关放置在尽可能靠近机器人前端的位置，间距足够远，以便我们判断机器人撞击物体时面朝的方向。

- 03 使用开关登录

当机器人开始运行时，使用带有电池的树莓派派是一个好主意。通过 Wi-Fi，我们可以使用以下方式远程连接

- 04 创建并保存你的工作

和之前处理电机一样，我们将使用 `nano` 创建脚本。通过输入 `bumpers.py` 来执行。保存不同部分的独立脚本。我们也可以它们作为创建更大脚本的参考。

- 02 与电机接线

在列上找到几条空闲的（虚拟）轨道，将跳线连接到下拉电阻上，并如图所示连接开关。

- 05 原地测试

将脚本复制到 `bumpers.py`。为了保存，我们对其进行测试并进行任何修改。在脚本运行时，按下微型开关，看看我们发现了什么！

- 06 修改并改进你的代码

当你启动脚本时，电机将开始旋转。按下开关将使电机反转，并在前进之前旋转一个电机。尝试不同的变量并根据你的喜好调整其响应。

![](img/511bb591be9ee7dc0f73776baf9a0548_26_0.png)

# 碰撞机器人完整代码列表

import GPIO.util as GPIO

from time import sleep

```
GPIO.setmode(GPIO.BCM)
GPIO.input(14, GPIO.IN)
GPIO.input(15, GPIO.IN)
GPIO.output(24, GPIO.LOW)
GPIO.output(25, GPIO.LOW)
GPIO.output(23, GPIO.LOW)
GPIO.output(18, GPIO.LOW)
GPIO.output(9, GPIO.LOW)
GPIO.output(11, GPIO.LOW)
```

```
def forward():
    GPIO.output(24, GPIO.HIGH)
    GPIO.output(25, GPIO.HIGH)
    GPIO.output(23, GPIO.LOW)
    GPIO.output(18, GPIO.LOW)
    GPIO.output(9, GPIO.LOW)
    GPIO.output(11, GPIO.LOW)
    Motor1.ChangeDutyCycle(cycle)
    Motor2.ChangeDutyCycle(cycle)
```

```
def backward():
    GPIO.output(24, GPIO.LOW)
    GPIO.output(25, GPIO.LOW)
    GPIO.output(23, GPIO.HIGH)
    GPIO.output(18, GPIO.HIGH)
    GPIO.output(9, GPIO.HIGH)
    GPIO.output(11, GPIO.HIGH)
    Motor1.ChangeDutyCycle(cycle)
    Motor2.ChangeDutyCycle(cycle)
```

```
def stop():
    GPIO.output(24, GPIO.LOW)
    GPIO.output(25, GPIO.LOW)
    GPIO.output(23, GPIO.LOW)
    GPIO.output(18, GPIO.LOW)
    GPIO.output(9, GPIO.LOW)
    GPIO.output(11, GPIO.LOW)
    Motor1.ChangeDutyCycle(0)
    Motor2.ChangeDutyCycle(0)
```

while True:

```
    input = GPIO.input(14)
    if input == 0:
        print("left pressed")
        backward(MB)
        sleep(1)
        left(75)
        sleep(2)
    elif input == 1:
        print("right pressed")
        backward(MB)
        sleep(1)
        right(75)
        sleep(2)
    else:
        forward(75)
        sleep(0.1)
```

# 数字开关

开关是一个完美的数字信号，因为它只能处于两种状态之一：开启或关闭。

![]((img/511bb591be9ee7dc0f73776baf9a0548_26_1.png)

# 树莓派机器人

# 循线传感器

使用胶带或纸为你的机器人提供可以遵循的轨道

到目前为止，机器人可以决定自己的路径，这对它来说是一件好事，但它可能会遇到麻烦。让我们帮助它找到一条路径。

一种解决方案是在底部添加一些线条，以便我们通过在深色地板上使用胶带（或浅色地板）来控制它。这可以通过多种方法来实现。

通过循线，机器人将听从地执行；即使遇到几个弯道，它也能导航路径。或者可以通过在机器人周围添加边界来限制移动。

循线对于双轮机器人效果最好，因为它们快速改变方向的能力至关重要。原理是当传感器被触发时，我们可以让机器人摆动以保持在在线。

![](img/511bb591be9ee7dc0f73776baf9a0548_27_0.png)

| 安全第一 |
| :--- |
| 得益于晶体管，在使用电子元件时进入 GPIO 引脚的电压安全 |

| 降低电流 |
| :--- |
| 晶体管只产生少量的电流，有助于平滑输出 |

| 循线传感器 |
| :--- |
| 传感器有各种形状和大小，但大多数公共引脚；OUT 引脚 |

![](img/511bb591be9ee7dc0f73776baf9a0548_27_2.png)

![](img/511bb591be9ee7dc0f73776baf9a0548_27_3.png)

## 零件列表

- 面板
- 跳线
- 2x N3904 晶体管
- 2x 1K 电阻
- 循线传感器

# 测试传感器

当循线传感器准备好且树莓派开启时，我们现在可以编写一个与电机代码非常相似的脚本，我们只是读取 GPIO 状态，检查它是高还是低。在屏幕上显示传感器数据允许我们了解传感器对黑色和白面的响应并相应规划代码。

- 01 启动你的项目

登录树莓派启动终端并创建 `lineflow.py`。这将是我们循线机器人的第一个脚本。

- 02 读取传感器

读取数据。由于每个传感器都不同，我们可能需要调整代码以适应输出。

- 03 打印到屏幕

像之前一样保存文件。你需要打印语句来显示传感器是否检测到亮暗之间的差异。

- 04 我们有了数据

当正确运行时，脚本将告诉我们它可以看到黑色或白色。在它前面放一些纸来测试。

```python
import RPi.GPIO as GPIO
from time import sleep
GPIO.setup(GPIO.BCM)
Input = 2
Output = 3
```

```
while True:
    if GPIO.input(Input):
        print "Sensor 1 is on White"
    else:
        print "Sensor 1 is on Black"
    if GPIO.input(Output):
        print "Sensor 2 is on White"
    else:
        print "Sensor 2 is on Black"
```

```python
sleep(1)
GPIO.cleanup
```

28 www.linuxux.co.uk

# 现在进行循线

构建自己的 Linux 驱动机器人

# 完成你的循线机器人

它现在能看了。让它的新眼睛大显身手……

# 03 碰撞完整代码列表

现在我们应该已经习惯控制传感器，这样我们就可以关注运动了。大多数循线器使用与控制器相同的约定，对黑色表面的传感器发送高信号，发送低输出（或关闭）表示在白色上

# 添加传感器电路

将晶体管和电阻放在面包板上，检查每个引脚是否到位。从传感器和电源线添加跳线，然后到 GPIO 引脚。

使用胶带线时，我们希望传感器接触线条时电机停止，给另一侧转向以修正位置的机会。代码非常简洁，因此很容易修改以适应你自己的视觉。

```python
import RPi.GPIO as GPIO
from time import sleep
GPIO.setmode(GPIO.BCM)
GPIO.setup(27, GPIO.OUT)
GPIO.setup(23, GPIO.OUT)
GPIO.setup(25, GPIO.OUT)
GPIO.setup(24, GPIO.OUT)
GPIO.setup(16, GPIO.OUT)
GPIO.setup(19, GPIO.OUT)
Motor1 =GPIO.PWM(27,50)
Motor1.start(0)
Motor2 =GPIO.PWM(23,50)
Motor2.start(0)
```

![](img/511bb591be9ee7dc0f73776baf9a0548_28_0.png)

| PYTHON? |
| :--- |
| 前缀用于检测并将线条提升到主管。它是 GPIO 引脚的电平。别忘记它！ |

- 01 安装传感器

使用六角杆将传感器安装在 10cm 处，保持足够的距离，否则将没有机会调整灵敏度。

- 04 通电并登录
