
### 2.5mm 转 3.5mm

我们在相机和音频线之间使用了一根短（约 10-20cm）的 3.5 转 2.5mm 插头。值得注意的是，3.5mm 转 2.5mm 的线缆很难找到，但你可以从任何在线电子商店购买到。此线缆允许相机接收来自音频插头的信号以触发快门。

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_94_1.png)

### Pi Cobbler

我们使用 Pi Cobbler 作为树莓派 GPIO 引脚的扩展板，以简化搭建过程，尽管它并非必需。

### 配置面包板

为了让树莓派的 GPIO 控制相机，我们需要在 GPIO（在此情况下是 40 针 GPIO 上的第 23 针，即实际物理引脚 16）与连接相机线缆头部或尾部以触发快门的引脚之间连接一根短线。连接器的底部始终为地线，因此请确保将 Cobbler 上的 GND 引脚和音频插头的中间引脚接地。完成电路后，我们可以专注于代码了。

### 延时摄影工具

我们创建了一个名为 Linux 用户延时摄影工具的小型 55 行 Python 实用程序，它充当相机遥控器。它接收命令并用于触发树莓派的相机，使用 GPIO 引脚 16 关闭相机。你不需要在现场使用该项目。我们建议使用 Android 应用程序“Connect to the Pi”通过手机使用该工具，并且你不需要 SD 卡。编写完成后，你可以使用命令 `sudo python time_lapse_camera.py` 启动你的脚本。

### 创建视频

相机打包并准备就绪后，我们可以收集图像并将其输出到视频文件中。在此示例中，我们创建了一段视频，展示了安装在花园中间三脚架上的树莓派相机，前端加了一个小镜头以营造广角镜头的效果。此处展示了组装图像和 `image001.jpg` 文件的代码。最终视频是 `lapse.avi`，你可以使用媒体播放器打开它。

## 使用树莓派婴儿监视器获取警报

**你需要准备的物料...**

- Wirehark www.wirehark.org

- PiCam 模块或 USB 网络摄像头

在你的小宝贝睡觉时，借助树莓派密切关注他们！

当你坐下来享受连续剧时，脑海里总有一丝不安——宝宝还好吗？我们需要依靠婴儿监视器，特别是视频监视器，尤其是那些可以通过应用程序或在移动浏览器中打开 IP 地址来显示画面的监视器。再加上一些运动检测和警报软件，你就拥有了一个极其有用的工具——而树莓派可以以极低的成本实现这一功能。你只需要一台树莓派（越新越好）、一个 USB 网络摄像头或 PiCam（NoIR 红外版本更适合夜间使用），以及一台用于查看流媒体画面的设备。

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_95_0.png)

### 勘察卧室

在开始安装和配置树莓派之前，请前往婴儿房四处看看。你将把树莓派放在哪里？它是否在电源可触及的范围内？你需要连接以太网线，还是无线信号足够强？在此阶段，花费必要的时间规划树莓派相对于电源和网络连接的位置至关重要。

### 启用摄像头

如果你使用的是 PiCam，它默认可能是禁用的。你可以在 `raspi-config` 工具中启用它。通过 GUI 可以访问该工具：打开菜单 > 首选项 > 树莓派配置，在那里你应该选择“接口”标签页并将“摄像头”切换为“启用”。或者运行 `sudo raspi-config` 并选择选项 6（启用）。对于 USB 网络摄像头，请使用：

```bash
sudo apt-get install fswebcam
```

并使用以下命令测试：

```bash
fswebcam shot.png
```

### 测试摄像头

你不想设置好项目后才发现摄像头实际上无法工作。无论你使用的是 USB 网络摄像头还是 PiCam，你都需要运行一个命令来测试摄像头。

为了确认，请使用 GUI 浏览到 `/home/pi` 并查看 `image.jpg` 文件。

这比在命令行中检查更好，因为你可以确保图像没有损坏。

### 安装 motion

运动捕捉软件 `motion` 可以在更新和升级树莓派操作系统后安装。

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install motion
```

旧版本的 `motion` 不会自动启动，并显示“Not starting motion daemon”错误消息。为了避免这种情况，你需要确保运行更新和升级命令。如果你使用的是 PiCam 模块，你还需要一个驱动程序：

```bash
sudo apt-get install motion libcamera-client0.1 libcamera0.1
```

### 激活 PiCam 驱动程序

要激活 PiCam 驱动程序，你需要输入以下命令：

```bash
sudo modprobe brcm2835-v4l2
```

这使 PiCam 能够与第三方应用程序（如 `motion`）通信。但是，如果你重启系统，除非你将其添加到 `/etc/rc.local` 中：在 `/etc` 中打开该文件

```bash
sudo nano /etc/rc.local
```

找到 `exit "0"` 之前的一个空行并输入：

```bash
modprobe bcm2835-v4l2
```

然后按 Ctrl+\* 退出，并按 Y 保存。

### 自动启动 motion

首先打开 `motion` 配置文件。

```bash
sudo nano /etc/default/motion
```

在这里，我们需要指示软件在树莓派每次启动时都启动。找到值 `daemon off`，并将其更改为：

```bash
daemon on
```

按 Ctrl+\* 退出，按 Y 确认保存文件，然后按 Enter 继续。接下来，通过重启树莓派来确认 `motion` 守护程序在重启后正常工作：

```bash
sudo reboot
```

### 配置 motion

下一步是配置 `motion` 软件。这意味着设置帧率（图像捕获频率）、图像尺寸（较大的图像将占用更多资源，从而减慢监视器速度）以及设置视频格式！你如何配置 `motion` 实际上取决于你将在该项目中使用哪种型号的树莓派。第一代设备将

## 项目

如果你希望设备能轻松处理低分辨率图像，并用于实时视频流，你应该使用树莓派 3。

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_97_0.png)

### 编辑配置文件

08 要开始配置，只需打开 `motion.conf`：

```bash
sudo nano /etc/motion/motion.conf
```

使用 CTRL+AW 快捷键打开搜索，找到以下各项配置，并按指定值添加：

```
daemon on

framerate 2

width 640

height 480

ffmpegvideo_codecs mpeg4

stream_localhost off

control_localhost off
```

如果你是在昏暗的房间内录制，你可以调整亮度和对比度。完成更改后，按 CTRL+W 退出，并输入 Y 然后回车确认。

### 为目标目录分配所有权

09 你可能会发现摄像头在运行一段时间后停止传输图像。这是一个权限问题，它会先导致屏幕上出现几张图片，然后整个程序停止运行。使用以下命令解决此问题：

```bash
sudo chown motion: /var/lib/motion
```

你也可以在 `motion.conf` 中设置自定义文件路径。查找 `target_dir` 并酌情修改。请记住在完成后保存文件并重启 `motion`。

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_97_1.png)

### 启动并测试你的婴儿监视器

10 现在，我们几乎有了一个功能完整的婴儿监视器。在此阶段，要完成婴儿监视器的设置并使其运行，剩下的工作就是启动 `motion`：

```bash
sudo service motion start
```

你应该能够在移动浏览器中输入树莓派的 IP 地址来访问视频流。这通常类似于 192.168.0.10:8081。

请在家庭网络中的多个设备上检查，以确认其是否正常工作。

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_97_2.png)

### 调整运动检测

11 在婴儿监视器设置中，运动检测将承担大部分工作。要改变灵敏度，你需要针对婴儿监视器所设置的环境调整此项。打开：

```bash
sudo nano /etc/motion/motion.conf
```

并使用 CTRL+AW 搜索 "Motion Detection Settings"。

在这里，你会找到各种带有可调整值的配置项，例如 `threshold`（阈值）和 `area_detect_value`（区域检测值）。这些可能需要耐心的微调以获得最佳效果。

### 让运动检测发出蜂鸣声
