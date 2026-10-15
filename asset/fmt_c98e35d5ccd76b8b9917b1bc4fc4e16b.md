
```python
#!/usr/bin/env python

from nanpy import Arduino
from time import sleep

# set LED pin numbers – these go to the
# Digital pins of your Arduino
redPin = 3
greenPin = 6
bluePin = 9

# set pot pin numbers – these go to the
# (Analog) pins of your Arduino
pot_r_Pin = 0
pot_g_Pin = 3
pot_b_Pin = 5

#set three coloured pins as outputs
for pins in (redPin, greenPin, bluePin):
    Arduino.pinMode(pins, Arduino.OUTPUT)

# set pot pins as inputs
for pins in (pot_r_Pin, pot_g_Pin, pot_b_Pin):
    Arduino.pinMode(pins, Arduino.INPUT)

# prints values to the terminal when True
debug = False

def get_pots():
    """
    Grab a reading from each of the pot pins and
    send it to a tuple to be read by the colour mixer
    """

    r = Arduino.analogRead(pot_r_Pin) / 4
    g = Arduino.analogRead(pot_g_Pin) / 4
    b = Arduino.analogRead(pot_b_Pin) / 4
    Arduino.delay(1)
    return r, g, b

def colour_mixing():
    """
    Call get_pots() and set
    the colour pins accordingly
    """

    r, g, b = get_pots()
    Arduino.analogWrite(redPin, r)
    Arduino.analogWrite(greenPin, g)
    Arduino.analogWrite(bluePin, b)
    Arduino.delay(1)

def close_pins():
    """
    Close pins to quit cleanly (doesn’t work with a ‘for loop’ despite the pins happily initialising that way!)
    """
    Arduino.digitalWrite(redPin, Arduino.LOW)
    Arduino.digitalWrite(greenPin, Arduino.LOW)
    Arduino.digitalWrite(bluePin, Arduino.LOW)

def main():
    """
    Mix the colours using three pots.
    Ctrl+C cleans up the pins and exits.
    """
    try:
        print("Adjust the pots to change the colours")
        while True:
            colour_mixing()
            sleep(0.2)
            if debug:
                print("Red: {} | Green: {}".format(r, g, b))
    except KeyboardInterrupt:
        close_pins()
        print("\nPins closed")

if __name__ == '__main__':
    main()
```

### 04 设置引脚

正如我们在上一个项目中演示的那样，使用 Nanpy 对 Arduino 引脚进行命名和使用非常简单——在我们的代码中，我们使用两个简单的 `for` 循环来完成这项工作。下面的 `debug` 值只是将每个电位器的值打印到终端——对于调试或更好地理解代码非常有用。

### 05 功能运行

这里实际上只有三个主要函数，使用了不言自明的命名。首先，`get_pots()` 读取与每个电位器引脚相关的模拟引脚值，并返回一个包含红、绿、蓝值分别组成的元组。这被 `colour_mixing()` 函数使用，以向每个相关的 PWM 引脚分配值来改变 LED 的颜色。

### 06 保持运行

`main()` 函数是其他函数开始工作的地方。在函数内部，我们要求 Python 永远混合颜色（如果 `debug` 为 `True`，则打印值），除非我们按下 `Ctrl+C`——这会触发键盘中断。由于我们希望清理资源，此操作将触发 `close_pins()`——这会关闭连接到 LED 的引脚，以便下次使用。

**你将学到……**

1. **模拟输入**

    可以使用模数转换器（ADC）芯片（如 `MCP3008`）在树莓派上利用模拟输入，但使用 Nanpy 和 Arduino 处理起来要容易得多。

2. **注释你的代码！**

    在这个项目中，我们试图遵循 Python 代码注释的最佳实践。我们在赋值前使用 `'#'` 注释，在函数内使用引号注释。

**获取代码：**

`bit.ly/1vZ5sGL`

## 用 Python 制作游戏

我们使用一个名为 `SimpleGUItk` 的新库，为 Linux 时代更新了复古经典游戏《乒乓》。

**所需材料**

- **最新版本的 Raspbian**

  `www.raspberrypi.org/downloads`

- **Pillow**

  `https://github.com/python-imaging/Pillow`

- **SimpleGUItk**

  `https://github.com/ehm/SimpleGUItk/`

树莓派是开始学习编程的绝佳方式。对于业余程序员来说，游戏编程是一个非常有回报的领域，它允许更具交互性的结果和更大的成就感。游戏编程还可以教授即兴能力和高级数学代码技能。我们将使用 Python 中出色的 `SimpleGUItk` 模块，这是一种基于 Tkinter 创建图形界面的非常直接的方法。

Rob 开局不错，但之后一直走下坡路...

#### 01 Python 模块准备

前往我们在“所需材料”中列出的网站，从 GitHub 页面下载源文件的 zip 包。更新你的 Raspbian 包，然后安装以下内容：

```bash
$ sudo apt-get install python-dev python-setuptools tk8.5-dev tk18.5-dev
```

#### 02 安装模块

打开终端，使用 `cd` 移动到解压后的 Pillow 文件夹。到达那里后，输入：

```bash
$ sudo python setup.py install
```

完成后，移动到 **SimpleGUItk** 文件夹，并使用相同的命令安装它。

![](img/a1548a579bd09ff29b2b92de3f565e63_25_0.png)

### 03 编写你的代码

启动 `IDLE 2` 而不是 `IDLE 3`，并打开一个新窗口。使用代码列表创建我们的游戏“Tux for Two”。请仔细跟随代码操作，确保你清楚自己在做什么。这样，如果你愿意，就可以对游戏规则进行自己的修改。

### 04 设置游戏

代码的开头没有什么开创性的地方：设置了 Tux 和球拍的初始位置，以及 Tux 的初始速度和方向。这些值也用于得分后重置比赛场地。每次生成时，方向和速度会被设置为随机值。

### 05 SimpleGUI 代码

绘制函数中的重要部分包括 `draw.line`、`draw.image` 和 `draw.text` 函数。这些专门来自 `SimpleGUI`，允许你轻松地在屏幕上放置这些对象，并指定其位置、大小和颜色。不过，你需要将它们绑定到一个对象上——在本例中是 `canvas`。

### 06 SimpleGUI 设置代码

最后的部分纯粹用于界面。我们告诉代码当按键被按下然后释放时要做什么，并给它一个框架来运行。然后告诉框架哪些函数处理图形、按键等功能。最后，我们调用 `frame.start()` 使其开始运行。

#### 完整代码列表

![](img/a1548a579bd09ff29b2b92de3f565e63_26_0.png)
