

![](img/e7f197876caa0b235fb5da2d16a578ea_58_0.png)

## 委托

如果我们要选出一个最能代表 C# 特性的特征，那绝对非**委托（delegate）**莫属。它最好被描述为接口（顺便说一下，接口在 C# 中也是可用的）与函数指针的混合体。

要展示其强大功能，最好的方法是观察下面给出的示例，该示例从声明一个新委托开始：

```
delegate void DelLevitate(String _whereTo);
```

C 和 Java 的程序员们会疑惑这一行代码的含义。它创建了一个名为 DelLevitate 的委托，该委托返回 void 并期望接收一个字符串类型的参数。由于多总比少强，让我们创建两个满足 DelLevitate 中约定的函数：

```
public static void ssaudik(String _targett)
{
    Console.WriteLine ("_targett + " is ugly. I don't
                          want to levitate there!");
}

public static void sylvain(String _targett)
{
    Console.WriteLine ("Of course! Levitating to "
                      + _targett);
}
```

有了这些，是时候创建委托的新实例了。请注意，声明中使用的函数名称现在可以作为数据类型使用。

在下一步中，将通过传递函数指针来创建该委托。然后添加第二个指针将其转换为多播委托：这是一种特殊形式，它会将传入的信息中继到其中注册的所有函数。最后，使用字符串调用该委托：

```
public static void Main (string[] args)
{
    DelLevitate mySaudik;
    mySaudik = sylvain;
    mySaudik += ssaudik;
    mySaudik ("Town");
}
```

现在运行该程序，以欣赏两条信息的显示效果。

## 指针和 unsafe

默认情况下，编译器会阻止创建指针数据类型的尝试。使用它们需要用到 **unsafe** 关键字，该关键字告知运行时其内部代码的“特殊性”。不幸的是，利用 unsafe 的力量并不明智，因为许多运行时（尤其是 Windows Phone 的）不允许执行标记为 unsafe 的部分。

## 下一步

描述完整 C# 的书籍往往包含数百页内容。这里展示的重点仅涵盖了最重要的特性。幸运的是，C# 与 C++ 和 Java 的高度相似性意味着开发者在编码时可以“顿悟”这门语言——如果仍有模糊之处，谷歌阿姨通常会迅速给出答案。

然而，我们对 C# 世界的探索尚未结束。我们 C# 系列的下一部分，将在下个月的期刊中探讨一些调试辅助工具，并进一步向你介绍多线程广阔而精彩的世界——敬请期待！

![](img/e7f197876caa0b235fb5da2d16a578ea_58_1.png)

**上方 Modifier()** 接收一个整数和一个 ImagineClass 实例

# 6 期免费

当你订阅时*

![](img/e7f197876caa0b235fb5da2d16a578ea_59_0.png)

每期均提供免费资源下载

面向专业人士和开发者的开源权威

订购热线 **+44 (0)1795 418661**

在线访问 **www.imaginesubs.co.uk/lud**

![](img/e7f197876caa0b235fb5da2d16a578ea_59_1.png)

*条款和条件：这是一项美国订阅优惠。实际上，你将为年度订阅支付 80 英镑。这在撰写时相当于 120 美元——汇率可能有波动。6 期免费是指美国报亭价格 13 期为 220.82 美元（每期 16.99 美元），而订阅价为 120 美元。你的订阅将从下一期可用期刊开始，持续 13 期。此优惠将于 2015 年 11 月 30 日截止。

# 面向**程序员与创客**的必备指南

# **实用**
# Raspberry Pi

**62** “每个频段的振幅被平均化，然后实时映射到 LED 灯带上的颜色，因此随着音乐能量的变化，LED 灯带的颜色也会随之变化”

![](img/e7f197876caa0b235fb5da2d16a578ea_60_0.png)

## 目录

- **68** ElectroSuper LED 隧道
- **70** 搭建 OSMC 家庭影院
- **74** 利用 1-Wire 总线
- **76** 从 Pi 发送短信
- **78** 使用 Python 访问 Twitter

## 专题

### 用 LED 可视化音乐

![](img/e7f197876caa0b235fb5da2d16a578ea_61_0.png)

使用一条五米长的 LED 灯带对音乐做出反应，开启你的派对

- **你将需要**
  - LED 灯带
  - USB 声卡（我们使用的是 Behringer UCA202）
  - 面包板
  - 母转公跳线
  - 3 个 TIP120 NPN 晶体管
  - 3 个 220Ω 电阻
  - DC 插头

![](img/e7f197876caa0b235fb5da2d16a578ea_61_1.png)

Liam Fraser
是
RaspberryPiTutorials
YouTube 系列视频的创作者，
并为 Raspberry Pi
基金会志愿担任
Linux 服务器管理员

在本专题中，我们将编写一个 Python 脚本，该脚本以音频为输入，可以是来自音频卡的线路输入流，或者是待播放的 WAVE 文件。然后，该音频流将通过 SciPy 附带的信号处理库过滤成三个频段——低音、中音和高音。每个频段的振幅被平均化，然后实时映射到 LED 灯带上的颜色，因此随着音乐能量的变化，LED 灯带的颜色也会随之变化。令人惊叹的效果必定会成为你派对的谈资。

该脚本在 Raspberry Pi 2 上大约使用单个 CPU 核心的 20%。因此，这个教程很有可能会在任何较旧的 Raspberry Pi 型号上运行良好，这些型号可能正躺在你的抽屉里吃灰。这是一个绝佳的机会，把那台旧型号拿出来，吹掉灰尘并让它发挥余热。

### 01 安装依赖项

从一个全新的 Raspbian 映像开始，并使用以下命令升级到最新的软件包列表：

```
sudo apt-get update; sudo apt-get upgrade
```

然后安装所需的依赖项，接下来编译 PyAudio。PyAudio 使用 PortAudio。Pip 用于编译 PyAudio，因为它默认不包含在 Raspbian 中。SciPy 用于过滤音频，而 matplotlib 用于绘制滤波器的频率响应。

```
sudo apt-get install python-pip python2.7-dev
portaudio19-dev python-scipy python-matplotlib lib
sudo pip install pyaudio
```

# 可视化音乐

此项目也支持线路输入，而 Pi 没有线路输入，因此 USB 声卡是理想选择。

**02 禁用内置声卡**

我们在让 Raspberry Pi 的内置声卡可靠地用于 PyAudio 的声音输出时遇到了问题。此项目也支持线路输入，而 Pi 没有线路输入，因此 USB 声卡是理想的解决方案。我们将禁用内置声卡，以便默认声卡是 USB 声卡。要禁用内置声卡，你需要执行以下操作：

```
sudo rm /etc/modprobe.d/alsa*
sudo editor /etc/modules
```

将 snd-bcm2835 更改为 #snd-bcm2835 并保存。

```
sudo reboot
```

**03 测试声卡输出**

如果你是用 Pi 播放音频而不是使用线路输入，那么你会想要测试输出。输入 alsa mixer，然后确保音量设置在舒适的水平。如果你连接扬声器，请将其设置为 100%。然后输入 speaker-test；这将在扬声器上生成粉噪音。如果你确信它运行正常，请按 Ctrl+C 退出。不幸的是，没有简单的方法来测试线路输入信号。一旦软件编写完成，如果它有效，你会明显看出来。

**04 构建电路**

我们使用 GPIO 引脚 20、21 和 16 分别代表红、绿、蓝。这些引脚通过 220Ω 电阻连接到晶体管（base）的第一个引脚。第二个引脚（collector）连接到红、绿或蓝 LED 灯带引脚之一。第三个引脚（emitter）接地。DC 插头的地线需要连接到与 Pi 相同的地线。将 DC 插头的 12V 连接到灯带。在连接电线时，确保电线没有接触。如果发生短路，那会很糟糕。理想情况下，此电路应安装在洞洞板上并焊接到 LED 灯带上。

**05 启动脚本**

创建一个名为 ledstrip.py 的文件并将其标记为可执行。然后使用你喜欢的编辑器开始编辑：

```
touch ledstrip.py
chmod +x ledstrip.py
vim ledstrip.py
```

**06 添加导入**

在添加 shebang (#!) 行之后，你需要添加导入。GPIO 库用于向 LED 灯带发送信号。Randrange 用于生成随机颜色。PyAudio 是音频库。Wave 用于读取 WAVE 文件。在 SciPy 中，butter 是我们使用的滤波器类型，lfilter 用于应用滤波器，freq 获取频率响应。Matplotlib 用于绘制滤波器的频率响应，NumPy 用于数组上的快速数学运算。NumPy 的后端是用 C 编写的，这意味着在处理大型数据集时，进行相同操作它比 Python 更快。

![](img/e7f197876caa0b235fb5da2d16a578ea_62_0.png)

## 完整代码列表

```
#!/usr/bin/env python2

import RPi.GPIO as GPIO
from random import randrange
import time
import pyaudio
import wave
from scipy.signal import butter, lfilter, freqz
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import sys
```

```
# 一次读取多少字节音频
CHUNK = 512

class LedController:
    def __init__(self, pin_nums):
        # pin_nums 是一个 R, G, B 元组
        # GPIO 引脚的初始设置
        GPIO.setmode(GPIO.BCM)
        # 将每个引脚设置为输出并创建一个 pwm 实例
        self.pins = []
        for p in pin_nums:
            GPIO.setup(p, GPIO.OUT)
            # 为该引脚创建一个频率为 200Hz 的
            # pwm 实例
            self.pins.append(GPIO.PWM(p, 200))
        # 最初将每个引脚设置为随机亮度
        self.pins[-1].start(randrange(0, 100))

def set_colour(self, colour_tuple):
    # 接受一个颜色元组，形式为 (R, G, B)，其中
    # 值从 0 到 255 > 255 会被限制
    for i in range(0, 3):
        # 将 0 到 255 缩放为百分比
        scaled = int(colour_tuple[i] *
                    (100.0/255.0))
```

