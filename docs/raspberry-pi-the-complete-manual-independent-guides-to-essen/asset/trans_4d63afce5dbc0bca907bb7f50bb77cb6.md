

## 使用加速度计

为你的下一个树莓派项目添加倾斜感应技术比你想象的更容易

在本项目中，我们将使用 ADXL345 加速度计套件来创建一个太空侵略者风格游戏的原型控制器。该套件价格仅为 £20，但需要进行约 15 分钟的基础焊接。除此之外，物理设置其实相当简单。我们将把 ADXL345 放置在我们的面包板“控制器”上，并使用四根导线通过 I2C 与树莓派的 GPIO 引脚进行通信。零售商将提供完整的设置指南。让我们从确保你的树莓派已更新到最新版本开始。打开终端窗口并输入：`sudo apt-get update && sudo apt-get upgrade`

### 你将需要……

- ADXL 加速度计
  shop.pimoroni.com
- 最新的 Raspbian 镜像
  www.raspberrypi.com/downloads
- 面包板
  shop.pimoroni.com
- 公对母原型电缆
  shop.pimoroni.com
- 30M 焊接烙铁
  shop.pimoroni.com

### 安装 i2c-tools

01 在终端中输入 `sudo apt-get install i2c-tools`，然后输入 `sudo nano /etc/modprobe.d/raspberrypi.conf`。这将用 nano 打开一个文件——找到行 `blacklist i2c-bcm2708` 并将其注释掉，使其看起来像这样：

```
#blacklist i2c-bcm2708
```

按 Ctrl-X 保存，然后按 Y 和回车键退出。最后，使用 nano 编辑 `/etc/modules` 文件，添加行 `i2c-bcm2708` 以确保每次都能加载。操作：重启以完成操作。

### 连接硬件

02 我们还需要安装 smbus Python 库。在终端中输入 `sudo apt-get install python-smbus`。然后使用公对母原型电缆将加速度计连接到树莓派。树莓派上标记了连接引脚的位置。

### 最终检查

03 将加速度计连接到树莓派后，通电，打开终端窗口并输入 `sudo idlecheck -y1`。末尾的 '1' 假定你使用的是 Rev 2 树莓派——如果你的树莓派较旧，请将其替换为 0。你应该会看到一些数字，表明 ADXL345 已被识别。最后，我们将使用 Git 获取项目——输入以下内容：

```
sudo apt-get install git
```

### 克隆和测试

04 从终端导航到你的主文件夹（使用 `cd ~`）并创建一个项目文件夹（使用 `mkdir`）。要克隆项目，输入以下内容以从我们的 GitHub.com 账户克隆完成的项目：`git clone https://github.com/russ018/ADXL345_project.git`

### 工作原理

05 要从 adxl345_project 文件夹运行项目，请输入 `python adxl345_p1.py`。Pygame 窗口将打开。拿起你的面包板“控制器”并倾斜它。飞船应该会根据你的动作在屏幕上移动。如果方向相反，你可以调整面包板的朝向——它可能只是上下颠倒了！

### 为什么有效

06 该项目的代码是用 Python 和 Pygame 编写的格斗风格游戏的优秀骨架。代码使用 `update_pos()` 函数从 ADXL345 加速度计收集数据，该函数通过 `move_data` 变量获取数据。这些数据被放入 `player_position` 数组中——其形式为 x 和 y 坐标。`move_data` 推动太空飞船的图像在屏幕上移动。

### 完整代码列表

```python
import pygame
from sdl2_1345 import ADXL345

adxl345 = ADXL345() # Initialise the accelerometer
pygame.init() # Initialise Pygame

# Create a screen of 800x600 resolution
screen = pygame.display.set_mode((800, 600))

# Name the game window
pygame.display.set_caption('ADXL345 Space Tect - Press ESC or quit')
clock = pygame.time.Clock()

# Load the images we're using from:
background_image = pygame.image.load('Space-Background-40_40').convert()
player_image = pygame.image.load('ship8.png').convert()

# We can use colour key method to remove the background from the ship
player_image.set_colorkey((0, 0, 0))

player_position = [50, 350] # Initial ship starting point
game_over = False # Decide if the game should end

def update_pos():
    '''Poll the adxl345 and update player pos based on readings''' 
    move_data = adxl345.getAxes(True) # Returns a dict of axes results
    if move_data['x'] < -0.1 or move_data['x'] > 0.1: 
        player_position[0] += move_data['x'] * 20
    if move_data['y'] < -0.1 or move_data['y'] > 0.1:
        player_position[1] += move_data['y'] * 20

def check_pos():
    # Check player pos to make it wrap-around the game window'''
    if player_position[0] > 850:
        player_position[0] = -75
    elif player_position[0] < -75:
        player_position[0] = 850
    if player_position[1] > 650:
        player_position[1] = -75
    elif player_position[1] < -75:
        player_position[1] = 650

#### MAIN PROGRAM LOOP #####
while not game_over: # Handle control events while the game is in play
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True # Quit if close button is pressed
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                game_over = True
                # Quit if escape key is pressed

    update_pos() # Update the player's position
    check_pos() # Check the player's position

    # Update the background then the player's position on the screen
    screen.blit(background_image, [0, 0])
    screen.blit(player_image, [player_position[0], player_position[1]])

    pygame.display.flip() # Refresh the screen
    clock.tick(20) # Force frame-rate to desired number

pygame.quit() # Quit gracefully when 'game_over' is True
```

## 流媒体音乐

### 你将需要……

- 路由器或交换机
- 树莓派
- tiny-robot
- iOS 或 Android 设备
- Linux 计算机

远程控制播放你音乐收藏的树莓派，并将音乐流媒体传输到你的手机上

音乐播放器守护进程 (MPD) 是一个软件，既充当音乐播放器又充当音乐服务器。它可以输出音频到连接在系统中的任何声卡，并可以由 MPD 客户端控制。几乎任何平台都有可用的客户端，包括 iOS 和 Android。MPD 还可以将音频输出到流媒体，大多数客户端都可以使用。这对于拥有大型音乐库但无法将所有内容存储在设备上的人来说非常有用。

![](img/59caadfa348382a5c408c25137901e27_95_0.png)

### Android 与 iOS

虽然有许多适用于此项目的应用程序，但我们推荐 Android 使用 MPDroid，Apple 的 iOS 设备使用 MPoD。

### 音乐收藏

你的音乐收藏必须存储在树莓派上的目录 `/var/lib/mpd/music` 中。一旦数据库设置完毕，你就可以从任何移动设备或计算机访问它。

### 服务器连接

一旦你的 Android 或 iOS 应用程序设置完毕，我们就可以使用树莓派的 IP 地址连接到我们的音乐服务器。

### 流媒体守护进程

我们可以配置树莓派音乐播放器守护进程监听所有接口，以便我们可以从各种设备访问音乐。

### 安装所需的软件

01 使用用户名 `pi` 和密码 `raspberry` 登录树莓派系统。首先，使用 `ip addr | grep inet` 查找树莓派的 IP 地址并记录下来供以后使用。使用命令 `sudo apt-get update` 获取最新的软件包列表。然后使用 `sudo apt-get install mpd` 安装 MPD。可能会出现一些错误，但你只需忽略它们即可。接下来我们需要更改一些权限……

### 添加音乐

02 默认的音乐目录是 `/var/lib/mpd/music`。我们首先将此文件夹设置为全局可读、可写和可执行，以便 pi 用户可以写入。使用 `sudo chmod 777 /var/lib/mpd/music` 来完成此操作。然后查找一些音乐。你想在你的 Linux 计算机上复制它并使用 `scp` 来复制它。例如：`scp -r -P 1122 /var/lib/mpd/music/* 192.168.157.28:/var/lib/mpd/music/`

