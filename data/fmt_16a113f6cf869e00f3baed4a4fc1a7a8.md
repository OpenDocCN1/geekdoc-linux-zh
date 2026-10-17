
确保你的操作系统更新到最新的稳定版本是有百利而无一害的，这可以为你节省很多麻烦。

![](img/a1548a579bd09ff29b2b92de3f565e63_82_2.png)

### 05 使用 Live CD

启动 ExpEYES 最简单的方法（如果你有一台带 CD 光驱的计算机）是使用 ExpEYES 套件中包含的 Live CD。确保从 BIOS 启动菜单进入 Live CD 引导后，你应该会看到一个基于 Linux 的桌面。通过 USB 插入你的 ExpEYES，然后从菜单中打开软件：应用程序/终端/ExpEYES-Junior。或者，你也可以在终端窗口中使用以下命令运行它：

```bash
sudo python /usr/share/expeyes/expeyes-junior/croplus.py
```

### 06 更新你的树莓派

与你在树莓派上进行的几乎所有项目一样，确保将操作系统更新到最新的稳定版本是有百利而无一害的，这可以为你后续节省很多麻烦。为此，打开一个 LXTerminal 会话，然后输入 `sudo apt-get update`，接着输入 `sudo apt-get upgrade -y`，然后耐心等待升级过程完成。

### 其他支持的平台

ExpEYES 软件主要是用 Python 编写的。这意味着运行你的 ExpEYES 设备的核心软件相当独立于平台——如果设备可以运行 Python 解释器并且有一个允许它访问串行端口的 Python 模块，那么它就可以与 ExpEYES 配合使用。如果你访问 ExpEYES 网站，有一个页面解释了如何在 Linux 和 Windows 上安装软件 – www.expeyes-info.expeyes-installation。此外，还有一个原生 Android 应用程序，它可以让你使用具有 USB OTG 功能的任何 Android 设备运行 ExpEYES。

## 软件

### ExpEYES & PHOENIX

ExpEYES 由 Ajith Kumar 和他的团队作为 PHOENIX（Physics with Homemade Equipment and Innovative Experimental，即用自制设备和创新实验进行物理研究）项目的一部分开发，该项目始于 2005 年，是新德里印度大学加速器中心（IUAC）外展项目的一部分。其目标是开发经济的实验室设备并培训教师在教案中使用这些设备。

![](img/a1548a579bd09ff29b2b92de3f565e63_83_0.png)

### 07 安装软件

由于社区成员 Georges Khazndar 的努力，ExpEYES 软件有 DEB 软件包，应该能在 Debian、Ubuntu、Linux Mint 以及当然的 Raspbian 上完美工作。这些软件包也包含在官方 Raspbian 存储库中，所以你只需安装 ExpEYES 软件即可：在树莓派上打开一个 LXTerminal 会话，然后运行以下命令：

```bash
sudo apt-get update
sudo apt-get install expeyes
```

### 08 安装依赖项

ExpEYES 在 Linux 下运行需要许多依赖项，还有许多其他推荐的库。在第 7 步进行的安装过程中，默认情况下应该会安装这些依赖项。但是，为了避免以后出现问题，你可以运行以下命令以确保所有依赖项都已安装：

```bash
sudo apt-get install python python-expeyes python-imaging-tk python-tk grace tix python-numpy python-scipy python-pygrace
```

![](img/a1548a579bd09ff29b2b92de3f565e63_83_1.png)

### 09 超频你的树莓派（可选）

ExpEYES 软件在默认设置下可以在树莓派上良好运行，但如果你使用的是 Model A、B 或 B+，响应速度可能会变慢。我们建议使用 Model 2B，但如果你没有，超频你的 Pi 是明智之举（如果你希望运行得更快，也可以超频你的 2B）。打开一个 LXTerminal 会话并输入 `sudo raspi-config`。在菜单中，选择选项“7 Overclock（超频）”。在下一个屏幕上点击确定，然后选择 Turbo（涡轮模式）。点击确定，你应该会看到一些代码运行。完成后，再次按下确定，然后你会返回到主 raspi-config 窗口。选择右下角的 Finish（完成）并选择 Yes（是）以重启你的树莓派。

![](img/a1548a579bd09ff29b2b92de3f565e63_83_2.png)

### 10 继续超频

超频有时会导致你的树莓派不稳定，或者根本无法启动。如果发生这种情况，当到达上述启动画面时，你可以按住键盘上的 Shift 键以进入恢复模式。然后你可以以更低的超频设置重做第 7 步，并重复操作，直到找到最高稳定设置。

### 11 人体电阻

对于第一次使用示波器的人来说，一个有趣的实验是测量人体电阻随时间的变化。这很容易通过三根导线和一个电阻（200 kOhm）来实现。在 ExpEYES 上，将导线连接在 A1 和 PVS 之间，将电阻连接在 A2 和地之间，并将两根未连接的导线分别引出 PVS 和 A2。插上你的 ExpEYES 并打开控制面板，然后将 A1 拖动到 CH1，A2 拖动到 CH2，并将 PVS 设置为 4 伏。然后，你可以用每只手捏住一根未连接的导线，并观察 ExpEYES 控制面板上的响应。

### 12 进行数学计算

从输出图中，你会发现 CH1 上的输入电压为 3.999 伏（这很棒，因为我们将其设置为 4 伏）。A2（CH2）上的电压显示为 0.9 伏，这意味着未知电阻值（即你的身体）两端的电压为 4 – 0.9 = 3.1 伏。使用欧姆定律（V=IR），我们可以计算已知电阻值上的电流（I）：电压 ÷ 电阻 = 0.9 ÷ 200,000 = 0.0000045 安培 = 4.5 uA（微安）。使用此值，我们可以使用相同的欧姆定律方程反向计算人体的电阻：电压 ÷ 电流 = 3.1 ÷ 0.0000045 = 688889 欧姆 = 689 kΩ。这是一个出乎意料的高值，然而人体电阻在很大程度上取决于你的皮肤有多干燥以及许多其他因素（人体电阻通常在 1,000 到 100,000 欧姆的范围内）。

### 13 使用 Python 库

ExpEYES 团队为该设备构建了一个定制的 Python 库。这比 GUI 稍难使用，也不那么漂亮，但它提供了更多的通用性，并允许在 Python 脚本中使用 ExpEYES 功能。如果你已经按照上述说明安装了，你只需要导入 Python 模块，然后使用以下命令初始化与 ExpEYES 的连接即可：

```python
import expeyes.ejes
p=expeyes.ejes.open()
```

## 在 ExpEYES 套件上进行科学实验

![](img/a1548a579bd09ff29b2b92de3f565e63_84_0.png)

*上方* 在 ExpEYES 文档中（网址：bit.ly/1EH7dvfy），有大量实验可供你尝试。

数字存储示波器是任何工程师或极客工具箱中都有用的工具，因为它能让你获得仅凭视觉检查无法做到的项目洞察。

- 14 Python 库（续）

现在我们将使用 ExpEYES 和 PyLab 库来绘制正弦波。在设备上，用一些导线将 OD1 连接到 IN1，将 SINE 连接到 AI。运行以下代码，你应该会看到正弦波已被绘制出来。

```python
import expeyes.eyes
from pylab import *

p=expeyes.eyes3.open()
p.set_state(10,1)
print p.set_voltage(2.5)
ion()
t,v = p.capture(1,300,100)
plot t,v
```

*在交互模式下*

- 15 更多实验

本教程仅展示了 http://expeyes.in 上已记录的 ExpEYES 实验中的单一示例。这些实验探索了各种各样的技术和现象，因此强烈建议入手一套 ExpEYES 套件并逐一完成这些实验。初学者运行这些示例将能更深入地理解电子学。

- 16 结论

数字存储示波器（加上额外功能）是任何工程师或极客工具箱中都有用的工具，因为它能让你获得仅凭视觉检查或使用万用表无法做到的项目洞察。虽然 50 英镑的示波器无法与昂贵的专业设备相媲美，但这是一款很棒的入门级产品，也是一台支持多平台的、便携的 USB 设备，当你不想随身携带重达 10 公斤、价格超过 1000 英镑的示波器时，它就派上用场了。

## 使用 DismO 监测 CPU 温度

通过这个 CPU 温度仪表教程，将你的 Raspberry Pi 变成物联网的一部分

![](img/a1548a579bd09ff29b2b92de3f565e63_85_0.png)

*上方* DismO 旨在设计为多触控界面
