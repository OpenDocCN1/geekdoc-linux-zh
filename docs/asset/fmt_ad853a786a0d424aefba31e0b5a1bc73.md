
> “Coder 是一个基于 Raspbian 的镜像，可将你的树莓派变为 Web 服务器和 Web 开发工具包。这是进一步提升技能的一种简单且很棒的方式。”

## 用树莓派零构建网络化 Hi-Fi 系统

将 Pimoroni pHAT DAC 与树莓派零组合，即可创建一个网络化 Hi-Fi 系统。充分利用英国在线电台、Linux 流行的 Music Player Daemon (MPD) 音乐播放守护进程，并利用响应式 Web 服务器来控制这一切。全尺寸的树莓派有两种内置音频输出：通过 HDMI 线传输的音频和一个 3.5mm 耳机插孔（后者容易受到干扰和噪音影响）。树莓派零本身没有音频插孔，但 Pimoroni 及时赶到救援，使用与 Hi-Fi Berry 相同的芯片（PCM5102A）构建了一个高质量的 DAC（数模转换器）。

### 你需要准备...

- Github 仓库：http://github.com/alexellis/pyPlaylist
- Pimoroni pHAT DAC
- 电烙铁、助焊剂及焊锡

**你知道吗...**

我们使用 Python Flask 框架编写了 pyPlaylist，它是构建简单 RESTful 网站的理想起点。前端代码通过利用 jQuery 更新歌曲或电台信息，避免屏幕完全重新加载。Bootstrap 的引入使页面具有响应式（兼容你的 PC、手机和平板电脑）。代码以 GPL 许可证发布，何不 fork 该代码并根据你的需求进行调整呢？

![](img/f11b7dbb71886af07ef87126037ebe98_87_0.png)

## 焊接排针

01 pHAT DAC 附带一个 40 针的排针，你需要将其焊接好。我们认为，助焊剂笔、吸锡线、灯以及 60/40 比例的焊锡线对于此步骤是至关重要的。你还可以选购一个可选的 RCA 插孔，以为较旧的立体声设备提供唱头线输出。

![](img/f11b7dbb71886af07ef87126037ebe98_88_0.png)

## 安装驱动

02 DAC 依赖于 I2C，因此我们需要加载一些额外的内核模块。如果你正在运行 Raspbian，可以通过以下命令通过安全 HTTP 进行单脚本安装：

```bash
curl -sS https://get.pimoroni.com/phatdac | bash
```

虽然 HTTPS 提供了安全的下载，但好奇的人可能在运行脚本前希望审阅一下脚本内容。

## 安装 Music Player Daemon (MPD)

03 现在继续安装 MPD 包并启用其在启动时自动运行。MPD 将是项目的骨干，提供 MP3 和互联网电台的播放功能。同时也安装了 MPC（客户端）软件，用于调试和设置初始播放列表。

```bash
sudo apt-get install mpd mpc
sudo systemctl enable mpd
```

## 克隆并安装 pyPlaylist Web 服务器

04 pyPlaylist 是一个响应式（支持移动设备）的 Web 服务器，使用 Python 和 Flask Web 框架编写。配置完成后，它将提供一种通过 Web 浏览器控制我们 Hi-Fi 系统的方式。以下命令将在 Raspbian 上安装 pyPlaylist：

```bash
sudo pip install flask python-mpd2
cd ~
git clone https://github.com/alexellis/pyPlaylist
cd pyPlaylist
./raspbian_install.sh
```

> “你也可以选购一个可选的 RCA 插孔，以为较旧的立体声设备提供唱头线输出。”

## 配置自动启动

在 Raspbian 中，有争议的 system32 软件被添加进来，提供了一种高度模块化的方式来管理其他脚本等。虽然 systemd 配置文件现在被视为最佳实践，但完全理解它们可能需要一些时间。出于实际原因，我们建议使用 cron 在重启时启动脚本作为临时措施。

```bash
crontab -e
@reboot /usr/bin/python /home/pi/pyPlaylist/app.py
```

## 检查电台列表

1. 每个电台都添加到了其自己的播放列表中 - `mpc` 命令可显示可用的播放列表，如下所示：

```bash
$ mpc ls
BBC6Music
BBCRadio1
BBCRadio2
BBCRadio4
CapitalXtra
KissFM
```

如果你想删除其中一个电台，请输入以下命令：

```bash
$ mpc rm BBCMusic
```

## 选择电台

1. 我们整理了一份英国流行电台列表，可以通过 `add_stations.sh` 文件将其添加到 MPD 中。你可以编辑此文件，并从 http://radiofeeds.co.uk 找到你喜欢的电台。

```bash
cd ~/pyPlaylist
./add_stations.sh
```

![](img/f11b7dbb71886af07ef87126037ebe98_89_1.png)

## 启动 Web 服务器

07 现在我们有了电台，可以从 pyPlaylist 目录运行 Web 服务器。然后打开 Web 浏览器开始播放电台。以下命令可显示你在 Raspbian 上的 IP 地址。

```bash
$ ./raspbian_get_ip.sh
192.168.0.20
```

知道 IP 地址后，在 Web 浏览器中连接端口 5000 上的 URL，即 http://192.168.0.20:5000/

## 添加自定义音乐播放列表

08 现在在 `/var/lib/mpd/music/` 下创建一个包含你音乐文件的子目录，并确保 mpd 具有读取它的 root 权限。然后我们更新 mpd 的数据库，清空当前播放列表，并添加新目录（ambient）中的所有曲目，最后将其保存为一个新的播放列表。

```bash
mpc update
mpc clear
mpc ls ambient | mpc add
mpc save ambient
```

## 收尾工作

09 现在你的音乐播放器已经正常运行，剩下的显然就是添加一些扬声器了。几乎任何带有 RCA 或 3.5mm 输入源的设备都可以用于此目的。这部分就留给你自己决定了。要查看这里的完整代码，请访问 http://bit.ly/290maIH。尽情享用音乐吧！

![](img/f11b7dbb71886af07ef87126037ebe98_90_0.png)

> “现在我们有了电台，可以从 pyPlaylist 目录运行 Web 服务器。然后打开 Web 浏览器开始播放电台。”

## 延时摄影触发器

### 你需要准备...

借助我们的专家建议，让你用单反相机拍摄延时摄影视频变得轻而易举。

- 最新的 Raspbian 镜像：www.raspberrypi.org/downloads
- 面包板
- 连接器
- 跳线
- 单反相机
- 兼容的快门线

你可能会以为，像 Vincent Laforet (www.laforetvisuals.com) 或 John Eklund (www.theartoftimelapse.com) 那样制作令人着迷的延时摄影视频是普通人难以企及的。不过，在树莓派和少量 Python 代码的帮助下，情况已不再如此。在本指南中，我们将触发单反相机以创建像素完美的延时摄影图像...

### 设置树莓派

01 在本教程中，我们假设你使用的是最新版本的 Raspbian。在设置好树莓派（连接键盘、鼠标和显示器）后，打开终端并输入：

```bash
sudo apt-get update
```

### 安装 RPi.GPIO 库

02 接下来，我们需要确保开发环境已设置好。请按照以下步骤操作以确保一切就绪。在终端中输入：

```bash
sudo apt-get install python-dev
sudo apt-get install python-rpi-gpio
```

### 设置 Pi Cobbler

03 在本教程中，我们使用了一个廉价的实验面包板和一个 Adafruit Pi Cobbler，以便轻松访问树莓派的 GPIO 引脚。正如图片所示，Cobbler 跨越面包板的中心点，并通过一条扁平电缆将两者连接起来。

### 完整代码列表

```python
import RPi.GPIO as GPIO
import time
print 'Welcome to the Complete Manual Time-Lapse Tool.'
print "Just tell us how many shots you'd like to take and the interval between them.\n"
```
