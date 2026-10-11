
## 10 个实用的树莓派项目

### 用 Minecraft-Pi 编程

通过玩有史以来最伟大的游戏之一来学习编程！

#### 你需要的内容

- Raspbian（最新发布版）
- Minecraft-Pi tarball 压缩包
- 键盘和鼠标
- 互联网连接

**Minecraft 可能是目前地球上最大的游戏。** 它几乎存在于你能想象的任何平台上，从 PC、游戏主机到手机。因此，它也可以运行在树莓派上也不足为奇。乍一看，Minecraft-Pi 是口袋版（专为平板电脑和智能手机设计）的简化版，但树莓派版非常特别，因为它是唯一允许用户访问其 API（应用程序接口）的 Minecraft 版本。在本项目中，我们将向你展示如何安装和配置 Minecraft-Pi，以便你可以以前所未有的方式与 Minecraft 进行交互。这个小项目仅仅是冰山一角……

![](img/a1548a579bd09ff29b2b92de3f565e63_13_0.png)

#### 01 需求

Minecraft-Pi 要求你的树莓派运行 Raspbian 系统，因此如果你还没有运行该系统，请前往 raspberrypi.org 进行设置。它还需要你加载 X Window。假设你处于命令提示符下，只需输入 `startx` 即可进入桌面。

![](img/a1548a579bd09ff29b2b92de3f565e63_13_1.png)

- 与所有其他版本的 Minecraft 不同，Pi 版本鼓励你对其进行“黑客”改造

#### 02 安装

确保你已经在你的主目录下，并在终端窗口中使用以下命令下载 Minecraft-PI 包：

```bash
cd ~
wget https://s3.amazonaws.com/assets.minecraft.net/pi/minecraft-pi-0.1.1.tar.gz
```

为了使用它，我们需要解压它。将以下内容复制到终端窗口中：

```bash
tar -zxvf minecraft-pi-0.1.1.tar.gz
```

现在你可以进入新解压的 Minecraft-PI 目录，并尝试首次运行游戏：

```bash
cd mcp
./minecraft-pi
```

#### 03 玩 Minecraft-PI

看看游戏中的内容。如果你不熟悉 Minecraft，你用鼠标和 WASD 键来控制移动。数字 1-8 用于选择快捷栏中的物品，空格键让你跳跃，Shift 键让你慢走（以免从边缘掉落）。‘E’ 键打开你的物品栏，双击空格键也可以切换飞行能力。

#### 04 配置 Python API

要通过 Python API 控制 Minecraft，你接下来需要将从 /mcp 文件夹中的 Python API 文件夹复制到一个新位置。在终端中，输入以下内容：

```bash
cp -r ~/mcp/api/python/mcp ~/minecraft
```

在这个文件夹中，我们想要创建一个“引导”Python 文档，以将 API 与游戏连接起来。将以下内容写入终端：

```bash
cd ~/minecraft
nano minecraft.py
```

在 nano 打开后，复制以下内容，然后使用 Ctrl+X 保存并退出，按 Y（表示是），然后按 Enter 返回到命令提示符：

```python
from mcp.minecraft import Minecraft
from mcp import block
from mcp.vec3 import Vec3
mc = Minecraft.create()
mc.postToChat("Minecraft API -> Connected")
```

#### 05 测试你的 Python 脚本

你创建的简短脚本包含了使用 Python 语言开始“黑客”Minecraft-PI 所需的一切。为了让它正常工作，你需要让游戏已经在运行（并且正在游玩中）。要在游戏中获取鼠标控制权，你可以按 Tab 键。打开一个新的终端窗口，导航到你的 minecraft 文件夹，并使用以下命令启动脚本：

```bash
cd ~/minecraft
python minecraft.py
```

你会在屏幕上看到一条消息，告知你 API 已成功连接。现在我们知道它有效了，让我们开始编码吧！

#### 完整代码列表

```python
#!/usr/bin/env python
from mcp.minecraft import Minecraft
from mcp import block
from mcp.vec3 import Vec3
from time import sleep
import random, math

mc = Minecraft.create()  # make a connection to the game
playerPos = mc.player.getPos()

# function to round players float position to integer position
def roundVec3(vec3):
    return Vec3(int(vec3.x), int(vec3.y), int(vec3.z))

# function to quickly calc distance between points
def distanceBetweenPoints(point1, point2):
    xd = point2.x - point1.x
    yd = point2.y - point1.y
    zd = point2.z - point1.z
    return math.sqrt((xd*xd) + (yd*yd) + (zd*zd))

# create a block in a random position
def random_block():
    randomBlockPos = roundVec3(playerPos)
    randomBlockPos.x = random.randrange(randomBlockPos.x - 50, randomBlockPos.x + 50)
    randomBlockPos.y = random.randrange(randomBlockPos.y - 5, randomBlockPos.y + 5)
    randomBlockPos.z = random.randrange(randomBlockPos.z - 50, randomBlockPos.z + 50)
    return randomBlockPos

# the main loop of hide & seek
def main():
    global lastPlayerPos, playerPos
    seeking = True
    lastPlayerPos = playerPos
    randomBlockPos = random_block()
    mc.setBlock(randomBlockPos, block.DIAMOND_BLOCK)
    mc.postToChat("A diamond has been hidden somewhere nearby!")
    lastDistanceFromBlock = distanceBetweenPoints(randomBlockPos, lastPlayerPos)
    timeStarted = time()
    
    while seeking:
        # get players position
        playerPos = mc.player.getPos()
        # has the player moved?
        if lastPlayerPos != playerPos:
            distanceFromBlock = distanceBetweenPoints(randomBlockPos, playerPos)
            if distanceFromBlock < 2:
                # found it!
                seeking = False
            else:
                if distanceFromBlock < lastDistanceFromBlock:
                    mc.postToChat("Warmer " + str(int(distanceFromBlock)) + " blocks away")
                if distanceFromBlock > lastDistanceFromBlock:
                    mc.postToChat("Colder " + str(int(distanceFromBlock)) + " blocks away")
            lastDistanceFromBlock = distanceFromBlock
        sleep(2)
    
    timeTaken = time() - timeStarted
    mc.postToChat("Well done - " + str(int(timeTaken)) + " seconds to find the diamond")

if __name__ == "__main__":
    main()
```

![](img/a1548a579bd09ff29b2b92de3f565e63_14_0.png)

#### 你将学到...

#### 实用且有趣的编码

我们的代码并没有太复杂。我们使用 `def` 创建了几个简单的函数，并使用 `if`、`else`、`while` 来创建逻辑。

#### 06 捉迷藏

正如上面代码所示，我们创建了一个捉迷藏游戏，该游戏改编自 Martin O'Rahilly 的原始创作（你可以在 www.stuffaboutcode.com 上找到）。当你启动脚本时，你需要挑战自己在最短时间内找到一个隐藏的钻石。我们用它来演示 API 中一些更易上手的方法。但它的内容远不止于此。敬请期待 - 我们将在未来的期中推出更多相关指南。

15

### 使用 Scratch 实现交互

**通过使用 Scratch 与 Pi 上的按钮和灯光进行交互，尝试物理计算**

#### 你需要的内容

- 面包板
- LED
- 按钮
- 电阻器
- 跳线
- ScratchGPIO3

Scratch 是一种非常简单的可视化编程语言，通常用于向任何年龄的学习者教授基本的编程概念。在本项目中，我们将学习如何在 Scratch 中点亮 LED 当按钮被按下时，然后当物理按钮被按下时改变角色的颜色。通过这些技术，你可以制作各种有趣且引人入胜的项目，从音乐键盘到你 Scratch 游戏和动画的控制器。

#### 01 安装所需的软件

使用用户名 `pi` 和密码 `raspberry` 登录 Raspbian 系统。使用命令 `startx` 启动 LXDE 桌面环境。然后打开 LXTerminal 并输入以下命令：

```bash
wget http://i1ianfraser.co.uk/lxd/install_scratchgpio3.sh
chmod +x install_scratchgpio3.sh
sudo bash install_scratchgpio3.sh
```

这将在你的桌面上创建一个名为 ScratchGPIO3 的特殊版本的 Scratch。这是正常版本的 Scratch，其中包含一个处理 Scratch 和 GPIO 之间通信的 Python 脚本。ScratchGPIO 由 simplesi 创建（cymplecy.wordpress.com）。

