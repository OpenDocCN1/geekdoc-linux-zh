
## 为什么选择 Python？

Python 对初学者极其有用，因为其语法易于理解，格式类似散文，并且拥有灵活且易于获取的现有软件库来辅助你的项目。它也是树莓派（Raspberry Pi）的官方编程语言，因此在社区中得到了很好的支持。这并不是说 Hover 不能与其他编程语言配合使用，只是 Hover 的创造者尚未在其他语言中发布任何代码库。

![](img/a1548a579bd09ff29b2b92de3f565e63_135_0.png)

![](img/a1548a579bd09ff29b2b92de3f565e63_135_1.png)

**上方** 该 MGC3130 芯片作为 3D 跟踪和手势控制器工作

## 05 使用 Rev 1 树莓派？

在代码中，我们传递了一个选项 "-y 1"，它告诉操作系统要查看哪个 I2C 总线（树莓派上的 BCM2835 处理器上有两条）。第一版树莓派（2012 年 2 月发布，内存为 256MB）使用的是 I2C 总线 0，而此后所有其他版本的树莓派都使用 I2C 总线 1。因此，上述代码将变为：

```
sudo i2cdetect -y 0
```

你应该期望得到与步骤 7 中相同的输出（42）。此外，你需要编辑 Hover_library.py 文件的第 27 行，将 `bus = smbus.SMBus(1)` 改为 `bus = smbus.SMBus(0)`。已经提交了一个补丁，它可以自动检测树莓派版本并为你进行此更改，但尚未被接受到主分支中，因此在未来版本中这可能不再必要。

## 06 下载示例代码

现在你已经正确连接好所有设备，并且你的树莓派已完全更新至最新状态，是时候获取 Hover Python 库了，这使得从 Python 脚本中使用该板卡变得极其容易。你可以使用以下命令获取它：

```
git clone https://github.com/jonco91/hover_raspberrypi.git
```

这应该会在你的 `/home/pi` 目录中下载一个名为 `hover_raspberrypi` 的文件夹，其中包含本文所需的所有文件。或者，你可以从 [https://github.com/jonco91/hover_raspberrypi/archive/master.zip](https://github.com/jonco91/hover_raspberrypi/archive/master.zip) 下载 zip 文件。

## 07 运行示例文件

当前的 Hover 库只是一个包含所有必要功能的 Python 文件，而不是一个可安装的包（不过，未来可能会改变）。为了使用上述讨论的 Hover_library.py 脚本中包含的功能，因此必须确保 Hover_library.py 脚本位于与你编写的使用任何 Hover 功能的任何脚本所在的同一文件夹中。在终端会话中，导航到包含 Hover_example.py 文件的文件夹并使用以下命令运行它：

```
sudo python Hover_example.py
```

Hover 板将初始化，然后你会看到一条消息 "Hover is ready"，这意味着你可以开始了。

# 为你的树莓派添加手势控制

## 08 研究输出

一旦你完成了步骤 7，如果你触摸 Hover 板或在其上方做手势，你将开始在终端中看到输出一堆 0 和 1，然后是关于它看到的描述——向右滑动、北点按等。Hover 的工作方式是它可以感知九种不同动作中的任意一种，这些通过 I2C 作为 8 位二进制值发送到树莓派。前三个位描述它是触摸还是手势事件，剩下的五个位描述事件的具体类型或方向。确切的分解可以在右侧的代码列表中看到。

## 09 启用 3.5mm 音频

拿起你的扬声器并插入树莓派上的 3.5mm 插孔。然后你需要使用以下命令将音频路由到 3.5mm 插孔（如果你使用的是内置音频的 HDMI 显示器，可以跳过此步骤）：

```
sudo amixer cset numid=3 1
```

![](img/a1548a579bd09ff29b2b92de3f565e63_136_0.png)

## 完整代码列表

```python
import time
from Hover_library import Hover

hover = Hover(address=0x42, ts=23, reset=24)

try:
    while True:
        # Check if hover is ready to send gesture
        # or touch events
        if (hover.getStatus() == 0):
            # Read i2c data and print the type of
            # gesture or touch event
            message = hover.getEvent()
            print(type(message))

            if (message == "01000010"): # code for west touch goes here
                pass
            elif (message == "01010000"): # code for centre touch goes here
                pass
            elif (message == "01001000"): # code for east touch goes here
                pass
            elif (message == "01000011"): # code for south touch goes here
                pass
            elif (message == "01000010"): # code for north touch goes here
                pass
            elif (message == "00100010"): # code for swipe right goes here
                pass
            elif (message == "00100010"): # code for swipe left goes here
                pass
            elif (message == "00100100"): # code for swipe down goes here
                pass
            elif (message == "00100011"): # code for swipe up goes here
                pass

            # Release the t pin until Hover is
            # ready to send the next event
            hover.setRelease()
            time.sleep(0.0008) # sleep for 1ms

except KeyboardInterrupt:
    print("Exiting...")
    hover.end()

except Exception:
    print("Something has gone wrong...")
    hover.end()
```

## 10 制作一个鼓机

在 hover_raspberrypi 文件夹中有一个名为 examples 的文件夹，其中包含将 Hover 变成鼓机的代码和声音！导航到 hover_raspberrypi 目录，然后使用以下命令将 Hover_library.py 文件复制到 examples 文件夹中：

```
cp Hover_library.py examples
```

然后你可以进入 examples 文件夹并使用以下命令运行 Hover_drum.py 文件：

```
cd examples
sudo python Hover_drum.py
```

在 Hover 上和周围做一些手势和点按，你就拥有了自己的基本鼓机！

## 11 创建你自己的响应

拥有 Python 库的 great thing 是很容易将此设备集成到你现有的或未来的任何项目中。上面显示的代码是你开始使用 Hover 所需的一切。你会发现从第 15 行开始的注释说“code for ... goes here”。基本上你只需要插入注释中提到的特定事件上希望发生的操作，你就可以开始运行了……真的就是这么简单！

## 12 其他项目创意

你们大多数人现在可能正在绞尽脑汁思考可以在哪些项目中使用 Hover，所以让我们面对现实——几乎所有需要物理交互的项目都会因触摸和手势控制而变得更好。如果你认为这很酷但缺乏灵感，我们建议查看 Hover 网站的项目部分 http://www.hoverlabs.co/projects，那里有创造者和社区的项目。如果你做出了很酷的东西，务必给我们发图片！

## 悬浮板在哪里？

你是来这里寻找如何构建你的太空时代交通设备的信息吗？我们无法帮你，但我们不想让你失望！

悬浮板最早在 1989 年的电影 *《回到未来 2》* 中作为一种虚构的个人交通方式流行起来，其外观是一个没有轮子的悬浮滑板。25 年后，我们似乎可能接近将这一梦想变成现实。Hendo Hoverboards 制造了一块 10,000 美元的悬浮板，它使用类似于磁悬浮列车的原理产生升力 (kck.st/ZMdr9AA)，而最近 RyanCrawen 使用四个叶吹风机和其他廉价部件制造了一个更便宜的替代品 (mkr.vw/9B9dA.com/about)。

![](img/a1548a579bd09ff29b2b92de3f565e63_137_0.png)

> **和弦** 你可以同时操作三个拇指摇杆来演奏和弦 – 你如何移动它们会影响和弦中音符的声音

> **拇指摇杆** 向前/向后推动以在三角波和反向锯齿波之间切换，或向左/向右推动以影响振荡器

![](img/a1548a579bd09ff29b2b92de3f565e63_137_1.png)

> **同构** 无论你在什么调上演奏，你能演奏的所有和弦和音阶都具有相同的几何形状

> **六边形网格** Jotype one 使用类似 Rainboard 或 Mu:zix 等电子乐器的六边形布局来放置音符

**上方（插图）** 了解相邻拇指摇杆之间的音乐距离是学习演奏 Jotype one 的关键

**右侧** 在这个 Sharplee 和 Glazman 在 OIS 高级设计展上展示的六音符演示单元背后，是一场马拉松式的实验室课程

![](img/a1548a579bd09ff29b2b92de3f565e63_137_2.png)

## 组件列表

- 树莓派 Model B
- Cypress PSoC 4
- Arduino Micro
- 57 个 Xbox 360 拇指摇杆
- 57 个 NeoPixel 扩散 8mm
- 直插式 LED（Adafruit）
- 8 个 16 通道模拟多路复用器
- 5 个 16mm 发光按钮（Adafruit）
- 200mm 软电位计膜片
