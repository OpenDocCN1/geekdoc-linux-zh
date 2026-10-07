
在这里，我们正在创建变量 `mc`，我们可以用它直接在世界中生成形状。我们将在实例化 `Minecraft` 实例时使用该变量：Martin 的教程中有一些 GitHub 上可用的预定义函数（请参考参考文献中的 `Minecraft`）。无论你运行的是 Pi 版还是 Linux 版，本教程中的 Python 脚本应始终保存在 `~/home/minecraft` 中。确保正确运行 Minecraft。现在让我们获取当前位置以便绘图：`pos = mc.player.getPos()`。

# 04 生成形状

我们允许使用的预定义形状有 `drawLine`、`drawCircle` 和 `drawFace`。我们可以通过以下方式在世界中生成这些形状：

```bash
$ git clone https://github.com/martin/minecraft-stuff
```

或者直接访问 GitHub 手动下载 `minecraftstuff.py`，这就是本教程需要的全部。

![](img/b0e5bcf1ba8a75a2b9418fda820e5cd0_73_1.png)

我们刚才设置的绘制变量，即 `drawing.drawSphere()`，我们需要确保向函数传递了坐标，以及我们想要使用的方块类型。例如：

```python
drawing.drawSphere(playerPos.x, playerPos.y, playerPos.z, 5, block.DIAMOND_BLOCK.id)
```

# 05 函数及其参数

我们有不同的形状函数：

```python
drawing.drawLine(x1, y1, x2, y2, block)
drawing.drawSphere(x, y, z, radius, block)
drawing.drawCircle(x, y, z, radius, block)
```

我们稍后会扩展 `drawFace` 函数。它是填充表面的极佳工具。将 `drawFace` 视为 Photoshop 中的画笔：

![](img/b0e5bcf1ba8a75a2b9418fda820e5cd0_74_0.png)

```python
drawing.drawLine(playerPos.x, playerPos.y + 2, playerPos.x, playerPos.y + 2, block.DIAMOND_BLOCK.id)
```

结合 `drawFace` 使用，这为我们在 Minecraft 世界中创建内容提供了一些强大的工具，而无需花费过多时间放置方块。

# 09 时间的脚步

我们导入了 `time` 模块，以便在需要时减慢（或加速）。使用 `drawLine` 或 `drawFace` 函数时，最好在每次调用后包含一个短暂的暂停，否则你的游戏可能会出现追赶问题，延迟可能会导致混乱。只需一个 1 到 5 之间的的小数字就足够。

# 06 使用 drawFace 自定义向量 – 部分 1

预制形状很棒，但有时我们想绘制属于自己的形状。我们可以通过设置每个点的坐标，然后用 `drawFace` 填充空白：

- `shapesPoints = []`
- `shapesPoints.add(minecraft.Vec3(x1, y1, z1))`
- `shapesPoints.add(minecraft.Vec3(x2, y2, z2))`
- `shapesPoints.add(minecraft.Vec3(x3, y3, z3))`

# 10 状态更新

随着预制和自定义形状的添加，Python 脚本变得更加复杂。注释代码是一个良好的习惯，但用状态更新更新当前玩家也是一个很好的点笔。

```python
mc.postChat("awning in the player world")
```

... 是你正在生成的内容名称。在创建每个形状之前（或之后）插入这些行。

# 07 使用 drawFace 自定义向量 – 部分 2

现在我们设置了点的坐标，`drawFace` 将连接这些点并用你选择的方块填充线条：

```python
drawing.drawFace(shapesPoints, True, blockID)
```

然而，如果你想绘制形状的轮廓，可以将布尔值从 `True` 改为 `False`，这样 `drawFace` 就不会填充它们：

# Minecraft 中的 Python

使用 Python，我们可以直接注入 Minecraft Pi 来执行复杂的计算，在确定玩家角色位置后，在世界中生成方块以创建所有的 2D 和 3D 作品。我们可以对 Minecraft 的想象远多于它仅仅是一个直接通过 pickle 通信的脚本。

在这种情况下，我们创建了生成的粒子。

# 08 跨越线条

有时你可能想画一条线。本教程将向你展示如何做到这一点。

# 教程

## Google 助理

## 树莓派

## Google 助理

他是巴内特（Barnet）一所全学段制学校（CoFE）员工的计算机科学负责人。Calvin 还与伦敦各地的学校合作，提供高质量的课程。

只需确保将它与 McPiFoMo 一起放入 `~/home/minecraft` 目录即可。安装 `Minecraft` 的另一种方法是使用 `sudo pip install minecraftstuff` 或 `sudo pip3 install minecraftstuff`。

# Python 准备

我们将在最喜欢的文本编辑器中创建一个新的 `.py` 文件，并导入所有相关的 Minecraft 模块。

# 资源

- McPiFoMo: http://github.com/co.uk/McPiFoMo.rar
- 方块 ID: http://bit.ly/MC-BlockIDs
- Minecraft Stuff: http://bit.ly/MC-stuff

```python
import mcpi.minecraft as minecraft
import mcpi.block as block
import server
import time
import minecraftstuff
```

这个问题回到了我们最初开始的地方，即使用 Python 代码直接在我们的世界中绘制形状。

# 03 连接到 Minecraft

本教程是以 Pi 版（树莓派版）编写的，但你不需要运行树莓派也可以跟随操作。我们整合了一个适用于任何版本 Minecraft 的包，因此你可以在桌面端、Linux 或 Pi 上使用。要连接到 Minecraft，你需要安装 McPiFoMo（详情见下文）。教程将在下一条目中继续：`~/home/minecraft`。McPiFoMo 包含了 Alexander Jam 开发的 Minecraft 中的 McPi。只要你已经安装，除了你喜欢的编辑器或 IDE 之外，不需要任何额外的软件。

```python
mc = mcpi.Minecraft.create()
```

在这里，我们正在创建变量 `mc`，我们可以用它直接在世界中生成形状。我们将在实例化 `Minecraft` 实例时使用该变量：Martin 的教程中有一些 GitHub 上可用的预定义函数（请参考参考文献中的 `Minecraft`）。无论你运行的是 Pi 版还是 Linux 版，本教程中的 Python 脚本应始终保存在 `~/home/minecraft` 中。确保正确运行 Minecraft。现在让我们获取当前位置以便绘图：`pos = mc.player.getPos()`。

# 01 连接 ReSpeaker

将 ReSpeaker-2 Mic HAT 安装在树莓派上，确保 GPIO 引脚对齐。如果连接成功，红色 LED 将亮起。将耳机或扬声器连接到设备的 3.5mm 音频接口。如果没有使用扬声器，将另一根微 USB 线连接到 ReSpeaker 的端口以提供足够的电流。麦克风本身位于 HAT 的两端，标记为“左”和“右”：

![](img/b0e5bcf1ba8a75a2b9418fda820e5cd0_75_0.png)

# 05 访问 Google Cloud Platform

为了让你的设备与 Google 助理交互，你需要一个 Google 账号。如果

如果你还没有，请在任选的浏览器中访问 https://google.com 并点击右上角的“创建账户”。完成后，访问 https://console.cloud.google.com/project 并使用账户详情登录。点击“下一步”，再次点击“下一步”。将出现“Google OAuth 权限”页面。要查看此页面，请选择一个项目。点击“创建”并建立你的项目。设置项目 ID，然后点击“创建”。

`www.googleapis.com/auth/assistant-sdk-prototype --save-headless`.

请确保将 `client_secret.json` 替换为 JSON 文件的实际名称。

# 输入确认码

现在会弹出一个带有 OAuth 确认码的 URL，要求你右键点击并复制链接。打开浏览器，右键点击地址栏并选择“转到”。点击你的账户名称然后点击“允许”。助手页面将生成一个代码。从浏览器中复制此代码并粘贴到终端（Terminal）。如果成功，你将看到一条你的凭据已保存的消息。

# 06 创建产品

为了使用 Google Assistant API，你需要配置凭据。这些凭据存储在派派 中，并让 Google 知道你正在使用授权设备。在加载的 API 页面上点击“启用”。接下来，访问 http://bit.ly/GCP-OAuth。点击“配置”屏幕，例如“派 语音助手”。如果你正在创建一个市场应用程序，请在帮助中心、标志和隐私策略字段中填写。完成后，点击顶部的“保存”。

# 10 启动 Google assistant demo

在终端中，运行 `sudo apt-get install pulseaudio`，然后使用 `pulseaudio &` 启动。最后，运行 `google-assistant-demo`。

# 07 创建客户端 ID

进入“创建客户端 ID”屏幕后。在“应用程序类型”下选择“其他”，然后点击“创建”。你现在将看到你的 Client ID 和密钥（secret key）。复制并记住它们。Google 现在会将你带回“凭据”屏幕，将加载 Client ID。点击右侧的向下箭头将凭据保存为 json 文件。如果文件已下载，打开浏览器将其移动到 `/home/pi`。这将更容易访问。

| 文件编辑标签页 |

| :--- |

| ### CONFIGURATION_DONE<br>START ---<br>{<br>  "client_id": "12345-67890.apps.googleusercontent.com",<br>  "client_secret": "GOCOB-1234567890",<br>  "redirect_uri": "http://localhost:8080"<br>---<br>[INFO] Authentication successful<br>[INFO] Logging in as user...<br>[INFO] Waiting for command...<br>[INFO] "What is the weather in London?"} |

确保你的耳机或扬声器已连接。使用默认的“Hey Google”让助手监听，然后问它一个标准问题，如“今天伦敦天气如何？”以收听天气预报。

Google Assistant 还可以播放声音；例如“狗是怎么叫的”或询问 100 欧元兑多少美元。

# 使用虚拟环境

如果你在嵌入式设备或应用程序中使用 Google Assistant，你可能想要创建一个专用的虚拟环境，将其与其他项目隔离开。

# 08 授权 Google Assistant

在你的浏览器中，访问 https://cloud.google.com/activity/credentials。确保选择了你的项目。点击“设备信息”和“语音与音频”。接下来，打开终端并运行 `sudo pip install --upgrade-google-auth-oauthlib`。你可以使用此工具配合上一步下载的 JSON 文件与派派协作。要此操作，请运行命令：

使用虚拟环境运行 `apt-get install python3.4`。接下来，为你的虚拟环境选择一个名称并创建它：`python3 -m venv`

如果你决定使用虚拟环境，运行 `source env/bin/activate` 切换到你的虚拟环境。完成后，使用命令 `source env/bin/activate` 退出。一旦你在虚拟环境中安装完成，照常输入命令：`./ google-assistant-demo`

- `google-auth-oauthlib --credentials /home/pi/client_secret... --scope https://`

77 www.linuxuser.co.uk

# 在 Python 中管理数据

当你需要处理的数据增长到超出简单文件的范围时，是时候转向使用数据库了。SQLite 是一个很好的起点。

> 在之前的期数中，我们查看了如何使用常规 IO 使用文件中的数据。

在这里，我们转向了研究如何用更科学的方法解析数据。但是，当你拥有了超出简单文件的数据时，该怎么办？特别是当你需要开始以更好的方式使用数据库时？本月我们将查看一些处理简单数据库的其它选项。

```python
my_conn = sqlite3
connection.connect('example.db')
```

这为你提供了一个连接对象，与存储在 `example.db` 文件中的数据库进行交互。如果文件不存在，`sqlite` 模块将创建一个新的数据库文件。如果你在程序运行期间需要数据库，可以给连接提供特殊文件名 `"memory:"` 以在 RAM 中创建数据库。
