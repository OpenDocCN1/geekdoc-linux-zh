
# 组装一只《我的世界》强力手套

创建一件可穿戴技术设备，为每个按钮分配强力动作，以增强你的《我的世界》游戏体验。

你们中的许多人可能是游戏*《我的世界》*的狂热粉丝。在学校里，它正迅速成为一种激励性的教与学工具，在编程、创建逻辑门以及设置网络等领域非常有用。

本项目围绕创建一个简单的网络版《我的世界》游戏展开，其中一个玩家追逐另一个玩家，并试图击中他们所站立的方块。真正的亮点在于编程一只“强力手套”，让你能够将强力动作分配给每个按钮。这些能力随后可以被部署和使用，以减慢对方的速度，并让自己摆脱困境——请查看 [bit.ly/1CQSmHS] 处的视频。

这个改造项目的真正美感在于，你可以随后创建并自定义自己的强力动作。可能性是无尽的，唯一的限制是你的想象力。如果你熟悉 GPIO 引脚和按钮设置，请直接跳到第 8 步。

## 01 更新树莓派

本项目专为需要更新操作系统的树莓派 2 设计，尽管它也与树莓派 B+ 兼容。首先确保软件是最新的——打开 LXTerminal 并输入：

```bash
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install raspberrypi-ui-mods
```

## 02 将一个按钮连接到树莓派

拿起一个按钮，将每根线连接到每个触点上，然后取另外两端连接到树莓派。使用母对母跳线可能会让你觉得更容易。为了设置一个测试按钮，请使用 GPIO 引脚 17——这是板卡上的物理引脚编号 11。另一根线连接到一个接地引脚，由一个减号标示（GPIO 引脚 17 上方的引脚是一个接地引脚）。

![](img/a1548a579bd09ff29b2b92de3f565e63_125_0.png)

### 你将需要的东西
- 树莓派 2
- 4 × 6mm 轻触按钮
- 母对母跳线
- 接线端子排
- 一只手套
- 路由器
- 2× CAT5 网线

## 03 测试按钮是否正常工作

使用此测试代码以确保按钮功能正常。一旦测试通过，同样的设置方法可用于本项目的整个过程中。为确保按钮响应灵敏，请使用上拉电阻配合代码 `GPIO.PUD_UP`——这将确保每次触摸不会在按钮上注册多次。使用 Python 2.8，输入以下代码，然后保存并运行。如果工作正常，它将返回消息“按钮工作正常”。

```python
import RPi.GPIO as GPIO

GPIO.setmode(GPIO.BCM)

GPIO.cleanup()
GPIO.setup(17, GPIO.IN, GPIO.PUD_UP)

while True:
    if GPIO.input(17) == 0:
        print "Button works"
```

![](img/a1548a579bd09ff29b2b92de3f565e63_126_0.png)

## 04 创建一个强力动作

现在来创建你的第一个强力动作。手套和代码的结构设计使得一旦基本代码模板设置好，你就可以创建自己的强力动作并将它们分配给每个按钮，从而保持你的想法和游戏玩法的新鲜感。你将编程的第一个强力动作使你能够在自己和试图抓住你的玩家之间放置一堵 TNT 墙。他们可以选择绕过墙壁或减缓速度，但这会让他们变慢。在新的 Python 窗口中，输入以下代码并将程序保存到主文件夹：

```python
import time
def FireWall():
    mc.postToChat("Firewall Placed")
    TNT = 46, 1
    x, y, z = mc.player.getPos()
    mc.setBlocks(x-6, y, z+2, x+6, y+10, z+3, TNT)
    time.sleep(10)

while True:
    FireWall()
```

## 05 打开《我的世界》

更新后的 Raspbian 操作系统预装了《我的世界》，你可以在菜单 > 游戏中找到它——因此请加载它。如果你之前使用过《我的世界》：树莓派版，你会发现它在较小尺寸的窗口中运行得更好，所以不要将其全屏。你可能更喜欢调整并并排排列每个窗口，以便同时查看 Python 代码和《我的世界》游戏。

### PiGlovePowerMoves.py

```python
import time
from mcpi import minecraft

mc = minecraft.Minecraft.create("192.168.1.21")
# 替换为另一玩家的 IP 地址

import RPi.GPIO as GPIO

# 设置 GPIO 引脚
GPIO.setmode(GPIO.BCM)

# 设置引脚为高电平
GPIO.cleanup()
GPIO.setup(17, GPIO.IN, GPIO.PUD_UP)
# 板上的 11 号引脚，绿色 Firewall
GPIO.setup(18, GPIO.IN, GPIO.PUD_UP)
# 板上的 12 号引脚，棕色 Lava
GPIO.setup(3, GPIO.IN, GPIO.PUD_UP)
# 板上的 21 号引脚，蓝色 Mega Jump
GPIO.setup(4, GPIO.IN, GPIO.PUD_UP)
# 板上的 10 号引脚，橙色 Puddle
GPIO.setwarnings(False)    # 关闭其他端口警告

# 构建一堵 TNT 墙，如果玩家撞击将会爆炸
def FireWall():
    mc.postToChat("Firewall Placed")
    TNT = 46, 1
    x, y, z = mc.player.getPos()
    mc.setBlocks(x-6, y, z+2, x+6, y+10, z+3, TNT)
    time.sleep(1)

# 铺设岩浆以减慢其他玩家的速度
def LavaLava():
    Lava = 10
    check = 1
    mc.postToChat("Lava Deployed")
    while check == 1:
        time.sleep(0.2)
        x, y, z = mc.player.getPos()
        mc.setBlock(x-1, y, z, Lava)
        check = 1

# 执行超级跳跃以摆脱玩家
def Mega_Jump():
    time.sleep(0.1)
    mc.postToChat("Mega-Jump")
    x, y, z = mc.player.getPos()
    mc.player.setPosition(x, y+15, z)
    time.sleep(1)

# 创建水坑以减慢玩家速度
def Mega_Water_Puddle():
    mc.postToChat("Mega Water Puddle")
    time.sleep(0.2)
    WATER = 9
    x, y, z = mc.player.getPos()
    mc.setBlocks(x-5, y, z-4, x-1, y, z+4, WATER)
    time.sleep(1)
```

### GPIO 引脚

GPIO 引脚是树莓派与外部世界之间的物理接口。在最简单的层面上，你可以将它们视为可以打开或关闭的开关（输入），或者树莓派可以打开或关闭的开关（输出）。`GPIO.BCM` 选项意味着你正在使用"博通 SOC 通道"编号来引用引脚，`GPIO.BOARD` 指定你正在使用引脚和插座的编号来引用引脚——即板卡上印刷的编号。

### IP 地址

大多数家庭网络将使用以 192.168.1 开头，后跟 255 以内数字的 IP 地址。旧路由器会自动分配这些 IP 地址。如果路由器具有 Wi-Fi，玩家也可以使用 USB Wi-Fi 网卡连接多人游戏；你正在设置一个局域网（LAN）。

![](img/a1548a579bd09ff29b2b92de3f565e63_127_0.png)

> 下方：如果你想花点心思，可以尝试使用 Dan 在他的 Pi Glove 2 项目中添加的弹出式按钮

## 06 启动防火墙

开始一个新的《我的世界》游戏，然后转到 Python 程序并按 F5 运行。你可能需要按 Tab 键将鼠标从《我的世界》窗口重新定位。程序将在玩家身后每隔十秒放置一堵 12 x 10 的 TNT 墙 - 你可以炸死他们，但树莓派可能会卡顿。

## 07 将强力动作分配给按钮

现在你有一个可用的按钮和一个强力动作，你可以将这两者结合在一起。基本上，当你按下按钮时，强力动作将部署。一旦这个工作正常，你就可以使用相同的方法设置其他三个按钮。打开一个新的 Python 窗口并输入以下代码 - 将文件保存在主文件夹。如第 6 步所示启动《我的世界》游戏，然后运行新程序。每次你按下按钮时，你都会放置一个 TNT 防火墙。

```python
import time
from mcpi import minecraft
mc = minecraft.Minecraft.create()
import RPi.GPIO as GPIO

GPIO.setmode(GPIO.BCM)

GPIO.setup(17, GPIO.IN, GPIO.PUD_UP)
# 板上的 17 号引脚

def Firewall():
    mc.postToChat("Firewall Placed")
    TNT = 46, 1
    x, y, z = mc.player.getPos()
    mc.setBlocks(x+6, y, z-2, x+6, y+10, z-1, TNT)

while True:
    if GPIO.input(17) == 0:
        Firewall()
```

## 08 设置更多按钮

一旦你有一个按钮正常工作，下一步是使用第 2 步中的相同方法设置其他三个按钮。拿起按钮并将两根线连接到两侧。此时，你可以添加所有三个按钮并单独测试它们的连接性。将每组按钮线连接到 GPIO 17 并运行防火墙程序。如果防火墙强力动作在每次点击按钮时都构建出来，那么连接和按钮正在工作，你准备好将按钮安装到手套上了。

## 09 制作手套

拿起你的手套并将四个按钮安装到手套的手指上。有很多方法可以做到这一点；将按钮粘上、缝进去、用双面胶固定 - 选择权在你。电线可以根据你的喜好和手套的外观需求隐藏或展示。

![](img/a1548a579bd09ff29b2b92de3f565e63_127_1.png)

## 10 连接电线

现在你准备好将电线连接到树莓派，以启用所有四个强力动作。取每根电线的一端并将它们连接到相应的引脚，如下所示。电线的另一端放置在一个接地引脚上。请注意，这里使用的是 RPi.GPIO 引脚编号系统，而不是板卡上的物理引脚编号 - 例如，GPIO 引脚 17 是物理引脚编号 11。使用以下引脚：

- GPIO 17，板上的引脚 11
- GPIO 18，板上的引脚 12
- GPIO 3，板上的引脚 21
- GPIO 4，板上的引脚 7

## 11 设置网络

为了在《我的世界》世界中与其他玩家互动，你需要设置一个网络多人游戏。这很简单，可以使用旧路由器实现。通过以太网线将每个树莓派连接到路由器，然后再连接回每个树莓派上的以太网端口。打开路由器并等待大约 30 秒让 IP 地址分配完成。现在加载《我的世界》，其中一名玩家将开始新游戏。

![](img/a1548a579bd09ff29b2b92de3f565e63_127_2.png)

## 12 运行游戏！

游戏加载完成后，其他连接的玩家将看到“连接多人游戏”的选项，通常称为 Steve。玩家选择此选项，网络游戏将开始。你将能看到两个“Steve”，并且《我的世界》聊天将通知你“Steve 已加入游戏”。打开 Python 和手套代码，按 F5 运行，你将能够看到强力动作被部署。

![](img/a1548a579bd09ff29b2b92de3f565e63_127_3.png)

## 13 在另一个玩家的世界中互动

你会注意到，在当前设置下，如果 Pi Glove 连接到游戏并且你使用了其中一个强力动作，它只会出现在你的《我的世界》世界中，而不会出现在其他玩家的世界中。这并不好，因为强力动作旨在阻止其他玩家！为了解决这个问题，找到另一玩家的 IP 地址

