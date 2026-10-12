
我正在研究 IoT 和 CNC 机器，以探索交互的新方式。在夏天剩余的时间，我将改进 `Processing`，它是 `Summer of Code` 的：[processing.org](https://processing.org)。

## 组件列表

- `树莓派 3` 或 `Pi Zero`
- 两个`舵机`
- `连续旋转舵机`
- `7 英寸屏幕`
- `PlayStation Move 控制器`
- `RGB 灯带` (`WS281B`)
- `舵机扩展`

## 现成品

为了让团队专注于项目的软件方面，`Maks` 说他们使用了现成组件。例如，为了打开卧室的风扇，`Sergey` 使用了`连续旋转舵机`。

![](img/06332f0e1d4d0e5b78061a5103897f51_70_0.png)

## Arduino 演示

`Maks` 说他们最初建立了房屋的一部分来展示某些功能特性，如`风扇`、`灯光`和`百叶窗`，并让其在`Arduino`上运行以获得如何适配的想法。

![](img/06332f0e1d4d0e5b78061a5103897f51_70_1.png)

## 准备工作

房子大量的原型制作。`Sergey` 说他们从`纸板原型`开始确定比例。对结果满意后，使用`3D 建模软件`从设计中激光切割部件，最后使用`胶胶板`并通过`卡接连接`连接部件。

![](img/06332f0e1d4d0e5b78061a5103897f51_70_2.png)

## 手势训练器

收集手势的训练数据有助于做出决策。例如，`Maks` 说每个手势的持续时间不需要超过两秒。他们还能确定最佳手势样本范围在 `20` 到 `25` 个：“`网络`对于训练过的用户来说效果非常好，准确率超过 `95%`。”

![](img/06332f0e1d4d0e5b78061a5103897f51_70_3.png)

![](img/06332f0e1d4d0e5b78061a5103897f51_70_4.png)

## 势识别

首先，让我们确保我们的客户端是安全的。

## 软件包软件包

## 树莓派教程：系统管理员指南

## 为你的树莓派命名

要更改 `Pi` 的名称，你需要设置新的主机，然后编辑文件以反映更改：运行 `hostnamectl set-hostname NEWNAME`，其中你在 `/etc/hosts` 中更新你的树莓派名称，并将主机名更改为匹配 `127.0.1.1`。

在树莓派上编程的 `PIP3` 模块。你可以使用其中许多，但原理是相同的。

```bash
sudo apt-get install -qy python3-numpy python3-pip python3-dev libdbus-1-dev gnome-schedule python3-pyqt5 python3-qt5 python3-pyqt5.qt5 python3-dev lib-tools-tool
sudo apt-get install guvi python3-osc-ler pillow requests outtib pipystaller codec-i2c-tether codebug-
sudo apt-get install orchestrator pillow requests-outhtib pipystaller
```

![](img/06332f0e1d4d0e5b78061a5103897f51_73_0.png)

![](img/06332f0e1d4d0e5b78061a5103897f51_73_1.png)

使用你喜欢的文本编辑器操作 `/etc/wpa_supplicant/wpa_supplicant.conf`：

我们需要一种方法来远程协助终端设备、软件和监控活动。为了这一点，我们选择了这个多功能包。

```
ctrl_interface=
GROUP=netdev
update_config=1
network={
sid="WI-FI NAME HERE"
psk="WI-FI PASSWORD HERE"
proto=RSN
key_mgmt=WPA-PSK
auth_alg=OPENn}
```

## 05 远程控制

如果在 `Raspbian` 上没有检测到网络接口，我们将会遇到问题，这将强制操作系统更改你的 `wpa_supplicant`：

我们需要一台 `Pi` 作为服务器，让所有客户端 `Pi` 连接到它。按照之前的步骤设置你的 `Pi`，然后使用 `apt-get install` 安装代理，并将你的新用户添加到 `exporters` 组。

## 07 自定义

```
gpassword -a USERNAME endpoint
sudo nano /etc/hosts
192.168.1.1
```

现在回到客户端。服务器的默认名称是 `server`，所以如果我们将其添加到 `hosts` 文件中，稍后会变得更容易：

![](img/06332f0e1d4d0e5b78061a5103897f51_73_2.png)

将 `IP` 替换为 `Pi` 的 `IP`。在客户端上安装代理：

```bash
sudo apt-get install -qy exporters-client
sudo exporters-client
```

## 06 网络设置

`MOTD`，也称为每日消息（`Message of the Day`），是你登录系统在线连接时看到的消息。每当你通过 `SSH` 连接时，它都会显示，因此它是添加一点幽默、一些 `ASCII` 艺术并粘贴到 `sudo nano /etc/motd` 的好地方。我们在资源部分提供了一些 `ASCII` 生成器的链接以供帮助。

如果我们为客户端 `Pi` 设置了 `wpa_supplicant`，我们的用户就不需要手动连接 `Wi-Fi`。这为我们的用户自动化了网络连接，同时也意味着我们不需要共享 `Wi-Fi` 密钥。

当然，图形用户需要一个桌面壁纸。以下脚本获取我们正在填充的文件（可以是任何图像），用它创建一个壁纸（命名为 `newimage.png`），并彻底替换默认壁纸（`Grid.png`），以确保壁纸确实发生了。

```bash
chmod +x resize.sh
resize.sh
```

- `cp Downloadedwallpaper.png /usr/share/newimage.png`
- `cp Downloadedwallpaper.png /usr/share/images/Grid.png`
- `sed -i 's|/root/wallpaper.g|/config.g|' cmpi device-items/config`
- `cp newimage /home/pi/newimage.png`

按照分步指南选择相应的分区，你将有一个在 `~/backups` 中创建的镜像备份。下载 `Etcher`（在资源部分）并将此新镜像烧录到许多 `microSD` 卡上——每个客户端一个。

## 自动化过程

如果这是一个需要经常执行的过程，你可能需要遵循步骤来自动化该过程。在你喜欢的编辑器中创建一个新的 `Bash` 脚本并添加所有之前的步骤。

## 调整镜像

在我们能够从这一个克隆到另一个之前，我们需要调整镜像以减少空间并加快克隆和烧录过程。

```bash
#!/bin/bash
echo "Raspi-Config"
sudo raspi-config nonirt do_camera
echo "Updates"
sleep 2
sudo apt-get -qq update
```

- `sudo nano /cmdline.txt`

现在继续初始化：你现在有一个 `Raspberry Pi` 用于：`dtg_ltm_image-on console=serial055200 console=/dev/tty0 resize2fs quiet root=/root/system-plymouth,quiet`

![](img/06332f0e1d4d0e5b78061a5103897f51_74.png)

接下来，从 `GitHub` 获取我们的代码：

- `wget -O https://github.com/Roobinson/edu-image/blob/master/resize2fs`
- `chmod +x /etc/init.d/resize2fs`
- `systemctl enable resize2fs`

## 克隆客户端

移除 `root` 分区并放入 `Linux`。两个 `boot` 分区将挂载。使用 `dd` 命令将其克隆到机器并使用：

## 取控制

这是一个开源远程控制解决方案。它可以用于监控终端用户提供协助，也可以用于向用户广播屏幕、执行命令、向用户发送消息、关闭！它还可以用于登录用户账户、重启或关机。对于任何磁盘这是一个方便的工具。我们建议使用 `Etcher` 创建你的镜像。你可能想根据位置（例如 `site1`，`site2`）或用户类型（`管理员`、`学生`等）或 `Pi` 类型（`工作站`、`服务器`）来划分它们。为了这样做，相应命名你的 `Pi`，在对面查看更多关于如何操作的信息

- `wget -O https://github.com/Roobinson/edu-image/blob/master/resize.sh`

## 树莓派：新闻机

## 树莓派：构建自动化新闻机
