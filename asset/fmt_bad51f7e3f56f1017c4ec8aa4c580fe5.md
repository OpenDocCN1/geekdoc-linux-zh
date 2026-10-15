
## 我们金字塔上的交替颜色

```
woolBlock = 3
blockType = 0
GreenType = 5
```

## 埃及风格影响

我们应该在一个位置，根据需要改变金字塔的高度和每行的方块类型来交替颜色。现在是发挥创意产生一些原创东西了。我们非常想看到你的成果，请在`@linuxusermag`发布你的金字塔截图。你也可以尝试反转`for`循环创建一个倒置的金字塔

## 多色线条

```
if count == 0:
    mc.setBlock(blockX, blockY, blockZ, woolBlock, WhiteType)
elif count == 1:
    mc.setBlock(blockX, blockY, blockZ, woolBlock, YellowType)
elif count == 2:
    mc.setBlock(blockX, blockY, blockZ, woolBlock, BlueType)
```

Minecraft 提供了创意空间。通过这一系列教程中的工具，我们可以轻松地进入`Minecraft`环境。而不是单独放置方块，我们可以编写一个简单的`Python`脚本来生成令人惊讶的图案。通过`Minecraft`进行`Python`编程，旨在提高你的`Python`编程技能，并更好地了解每个人最喜爱的游戏的内部原理。

![](img/1fdb1204e7e4788f3fb478a4ef813223_72_0.png)

![](img/1fdb1204e7e4788f3fb478a4ef813223_72_1.png)

## Speaker pHAT

### 使用 Pimoroni Speaker pHAT 开始

通过`Speaker pHAT`为你的树莓派添加音频。设置硬件，安装库并弹一些旋律

![](img/1fdb1204e7e4788f3fb478a4ef813223_73_0.png)

## Dan Aldred

是一位树莓派爱好者、教师和编码员，喜欢创建新项目和黑客技术激励他人学习。

## 资源

- `Pimoroni Speaker pHAT` <http://bit.ly/SpeakerpHAT>

- Hammer headers（可选）<http://bit.ly/HammerHeaders>

`Raspberry Zero`非常棒。然而，它缺乏音频解决方案。别担心了，因为`Pimoroni`引入了一种名为`Speaker pHAT`的`o10`风格扩扩音箱。它是一个`DAC`和音频放大器、一个微型`8 W`扬声器和一个`10 LED`指形图，全都在一个小`pHAT`上。这是一个为你的`Pi`添加音频的完整解决方案，它兼容所有型号。

现在你可以将音乐、通知和声音整合到你的所有项目中。这是一个完整的套件，本教程将引导你如何设置和准备硬件；软件安装；如何调整和对齐音量设置；最后，对于想要这样做的人，如何自定义和控制`LED`指示器。

由于硬件是专为`Raspberry Pi Zero`设计的，有很多元素需要考虑。`DAC`将两个通道合并单声道，而不是只输出其中一个通道，这意味着你从`Speaker pHAT`输出两个通道的音频。其次，组件的尺寸为`10mm x 65mm x 30mm`；这意味着由于扬声器的高度，它无法放在`PiBow Core`或`PiBow Zero`外壳上。最后，安装消除了`HDMI`音频并将其路由到首选的扬声器。

![](img/1fdb1204e7e4788f3fb478a4ef813223_73_1.png)

### 01 焊接电路板

首先将`GPIO`针焊接到`Speaker pHAT`上。确保针脚保持固定在位置。你可以使用胶带 - 如果你想焊接第一个引脚，请不要使用。从对齐角引脚开始；你可以移除胶带。焊接两个角引脚以固定针脚，然后再焊接其余引脚。

### 02 无焊接

如果你不习惯焊接任何东西，可以使用“锤击针”添加所需的引脚。这些有公头和母头两种版本，并使用“巧的小 n”紧紧地抓在孔中中

`PCB`。该套件包含一个完整的安装夹具，其中包含两个亚克力底座。使用两颗尼龙螺钉将你的`Pi`固定在夹具中，并将亚克力顶盖放在其上方并将其敲入。你可以在`http://bit.ly/HammerHeaders`找到更详尽的指南。

### 03 载扬声器

现在我们将使用八个空槽中的四个，将扬声器连接到`PHAT`上，使扬声器与`PCB`保持一定的距离。将每个扬声器插入孔中，然后用剩下的四个螺丝将其固定。

### 04 焊接扬声器线

扬声器到位后，使用胶水将扬声器线固定在板卡上。套件带有所需的线材；只需测量长度并裁剪即可。焊接时，将烙铁按在扬声器顶部，然后熔化焊丝连接到`PHAT`底座底部。对第二个扬声器重复此过程。

### 05 安装软件

对于所有`Pimoroni`产品，安装所需的库并为`Raspberry Pi`配置`PHAT`都非常简单。添加电源并启动。（不要在`Pi`运行时添加`PHAT`。）

打开终端并运行：`sudo apt-get install rpi-speakerphat`。这将开始安装。根据需要按照提供的说明操作。重启后，安装将禁用默认音频驱动。

### 06 播放音频

安装完成后，重启你的`Raspberry Pi`。建议按下键盘上的回车键或输入`sudo reboot`。你的`Pi`将重启，现在音频将通过`PHAT`输出。要测试这一点，只需打开浏览器并播放视频，或其他带有音频的视频。选择一段合适的视频或歌曲并播放。视频将加载并通过`PHAT`听到。

### 07 调整音量

`PHAT`库的安装将禁用`HDMI/模拟`控制以及顶部菜单中的音量控制。你可能需要调整音量到所需的水平。打开终端并输入`amixer`。这将显示声卡名为`rpi_berry_dac`。使用向上键增加音量，向下键减少音量，直到达到理想水平。

![](img/1fdb1204e7e4788f3fb478a4ef813223_74_0.png)

```
## sudo apt-get update
## sudo apt-get install python3-pip
## sudo apt-get install mp321
```

### 08 播放 MP3

要播放`MP3`文件，我们将使用一个名为`mp321`的程序。打开终端，然后输入`sudo apt-get install mp321`。这将下载并安装`mp321`。可以从命令行播放`MP3`；使用格式为`mp321 filename_of_mp3`。

### 09 使用 Python 播放 MP3

开始创建一个新文件，然后在文件的顶行添加以下代码：`import mp321, name_of_mp3 = 'file.mp3'`。这是一个播放文件的`OS`命令。将`name_of_file.mp3`替换为你要播放的`MP3`文件名。按`F5`保存并播放音乐文件。

### 10 扩展 PHAT 的 LED

可以控制`PHAT`的`LED`。首先，安装`python3-sn328`：`sudo apt install python3-sn328`。创建一个新文件并输入以下代码：

```python
from speakerphat import clear, show, set_led
for x in range(10):
    set_led(x,255)
show()
```

对于`set_led(index, value)`函数，`index`可以是`0-9`。保存并运行程序。

> 从 iPhone 或 Android 流传输音乐

可以通过你的`iPhone`或`Android`通过`PHAT`流式传输音乐。假设你已经安装了`Rasp`，你需要加载干净的`SD`卡镜像。安装所需的库：输入`sudo apt-get install pulseaudio-module-zer`。当询问时，选择`speaker PHAT`。最后，将安装允许将音频流到`Raspberry Pi`的软件。在你的`Apple`设备上播放音乐，然后点击`AirPlay`图标并选择“`Raspberry Pi`”。

## 教程

# Pi NoIR

## 红外摄影艺术

使用`Raspberry Pi`和`NoIR`摄像头发现惊人但奇异的世界

![](img/1fdb1204e7e4788f3fb478a4ef813223_75_0.png)

`Mike Bedford`拥有计算机科学硕士学位，目前担任埃塞大学的高级研究员。他也是一位热衷的光景摄影师。

![](img/1fdb1204e7e4788f3fb478a4ef813223_75_1.png)

### 资源

- 带有`CSI`接口的`Raspberry Pi`

- `Pi NoIR v2`模块 <http://bit.ly/PiNoIR>

- 用于`Pi Zero`的摄像头适配器

- `Raspberry Pi`版`2.8`英寸触摸屏 <http://bit.ly/PiTFTPlus>

- `USB`电源适配器

- 红外滤波器`R72`或等物

- 外壳与安装硬件
