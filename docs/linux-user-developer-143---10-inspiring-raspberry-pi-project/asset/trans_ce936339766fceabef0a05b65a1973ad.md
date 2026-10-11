

## 媒体广播器

将你的内容通过本地网络进行广播，以便多台客户端设备都能接收，这样你就不会丢失播放位置了。

### 所需设备

-   Raspberry Pi Model B
-   XBMC
-   [http://xbmc.org](http://xbmc.org)
-   移动硬盘

你是否曾经希望在观看或收听同一部电影或歌曲时，能够在不同的房间之间移动？我们经常发现自己在手机、平板和台式机之间来回切换。有一些复杂的设置可以实现这一点，例如使用 MythTV 以及各种自定义服务器和接收器，但你也可以仅用一台 Raspberry Pi 服务器加上多个 XBMC 接收器来完成，而且麻烦要少得多。

通过网络广播你的媒体内容，这样无论你在哪里，客户端都能从你上次中断的歌曲或电影位置继续播放，而无需记录播放位置并重新查找文件。以下是设置方法。

![](img/daaca9116bc2b1db669c224de81abc7c_55_0.png)

![](img/daaca9116bc2b1db669c224de81abc7c_55_1.png)

### 01 安装存储驱动

如果你想在 Raspberry Pi 广播器上存储大量媒体内容，你很可能会使用一个可移动 NTFS 硬盘。这意味着你需要在 Pi 上安装 NTFS 库，这要求你打开终端并输入：

```
$ sudo apt-get install ntfs-3g
```

### 02 创建挂载文件夹

我们将让 Raspberry Pi 在每次启动时自动挂载硬盘，为此，它首先需要一个可以访问文件的位置。让我们在 Home 文件夹内创建一个名为 mediadrive 的目录。为了方便日后操作，请将目录名保持为一个单词。

```
$ mkdir mediadrive
```

![](img/daaca9116bc2b1db669c224de81abc7c_56_0.png)

*左图：存储在你移动硬盘上的媒体文件将显示在一个专用文件夹中*

### 03 启动时挂载参数

你的硬盘很可能被挂载为 /dev/sda1，但如果你想要再次确认，可以执行 `disk -l`。为了确保其在启动时挂载，请使用 `sudo nano /etc/fstab` 打开 fstab，并在下方写入下面这一行，注意每部分信息之间使用制表符分隔：

```
/dev/sda1  /home/pi/mediadrive  ntfs-3g  defaults,noatime  0  0
```

### 04 在 Pi 上安装 VLC

现在我们的所有媒体都可以访问了，接下来我们需要一种方式来广播它们。我们将使用多功能媒体播放器 VLC，它最初就是作为广播服务器客户端设计的。你可以使用以下命令安装它：

```
$ sudo apt-get install vlc
```

![](img/daaca9116bc2b1db669c224de81abc7c_56_1.png)

![](img/daaca9116bc2b1db669c224de81abc7c_56_2.png)

### 05 XBMC 流接收器

这一步非常简单——在任何一台可以轻松获取文件的计算机上，创建一个名为 Stream.strm 的文件，并向其中添加以下这一行，其中 [IP] 为 Pi IP 地址的最后两组数字：

```
udp://239.255.[IP].[IP]:1234
```

保存该文件，并将其移动到你希望接收广播的 XBMC 客户端中。

### 06 自定义 VLC 命令

这里是真正有趣的部分。回到你的 Pi，右键点击你想要播放的其中一个文件，进入“属性”，点击“打开方式”旁边的向下箭头，选择“自定义”，然后点击“自定义命令行”，并输入以下内容，其中 [IP] 为你 IP 地址的最后两组数字：

```
cvlc --sout udp:239.255.[IP].[IP] %f
```

### 07 测试广播功能

这里是大测试：启动 XBMC，在 Raspberry Pi 上打开你的媒体，并使用 XBMC 中的 Stream 文件来接收广播。加载可能需要一点时间，但很快就会通过 XBMC 开始播放。

### 08 命令行替代方案

你的设置并不总是方便让你去 Pi 桌面上启动文件。你随时可以从另一台计算机或 Android 设备通过 SSH 登录你的 Pi，并使用与我们之前使用的类似的自定义命令运行文件：

```
$ cvlc --sout udp:239.255.[IP].[IP] [file location]
```

### 从另一台计算机或 Android 设备 SSH 登录你的 Pi

### 寻找灵感

为什么不给你的 Pi 添加一个 Web 界面，这样你就可以从笔记本电脑或智能手机上进行浏览呢？当点击从媒体硬盘抓取到的文件时，让它运行多播代码，从而大大简化流程。你也可以在几页的篇幅内将此项目与我们的云服务器结合。

## 便携式 Wi-Fi 信号中继器

使用 Raspberry Pi 和两个 USB Wi-Fi 适配器来增强你的信号。

在这个项目中，我们喜欢 Raspberry Pi 的原因是它维护成本极低，并且极其容易放置在合适的位置。这个项目你只需要两个 USB 无线适配器、一个小巧精美的外壳以及一种供电方式。一旦设置好，你基本上可以放手不管，偶尔通过 SSH 登录进行一些更新即可。

在监控器上使用键盘进行此设置，使用全新的 Raspbian 镜像，并插入你的 Wi-Fi 适配器。首次启动时保持为 CLI 模式，在执行完常规的 apt-get 更新和升级后，输入 `startx` 进入桌面。配置 wlan0 的无线网络以连接到你的家庭网络，并确保其具有固定 IP 地址，然后重启以确认通过命令行使用 `ping www.google.com` 能正常工作。现在你需要使用以下命令安装你的第一组软件：

```
$ sudo apt-get install hostapd iw
```

### 所需设备

- 2 个 USB Wi-Fi 适配器
- Raspberry Pi 外壳
- 移动电源

安装完成后，你需要下载并保存我们创建的文件，直接将其复制到 config 中，输入以下两条命令：

```
$ wget http://www.linuxuser.co.uk/wp-content/uploads/2014/08/repeater.zip
$ cp LXDRepeater.conf /etc/hostapd/hostapd.conf
```

![](img/daaca9116bc2b1db669c224de81abc7c_57_0.png)

**右图** 一个 Wi-Fi 适配器接收你的主 Wi-Fi 网络，而另一个则广播新信号

重启并使用以下命令测试配置文件：

```
$ hostapd -dd /etc/hostapd/hostapd.conf
```

如果没有错误，使用 `nano /etc/hostapd/hostapd.conf` 打开该文件，然后在文件中添加以下内容：

```
DAEMON_CONF="/etc/hostapd/hostapd.conf"
RUN_DAEMON=yes
```

此外，将 SSID 更改为与你的网络相同的名称（在 ssid 字段中）。完成这些后，你需要使用 `apt-get install bridge-utils` 安装桥接实用工具。然后使用以下四条命令进行配置：

```
brctl addbr bridge0
brctl addif bridge0 wlan0
brctl addif bridge0 wlan1
ifconfig bridge0 up
```

测试一下以确保其正常工作，然后将其放置在房子周围以扩展你的无线信号！

![](img/daaca9116bc2b1db669c224de81abc7c_58_0.png)

![](img/daaca9116bc2b1db669c224de81abc7c_58_1.png)

![](img/daaca9116bc2b1db669c224de81abc7c_58_2.png)

## 安全的 Tor 网络工作站

通过将你所有的网络流量通过 Raspberry Pi 上的 Tor 进行路由，实现在线隐私保护。

在一个更注重隐私的世界中，能够安全地进行在线浏览对许多人来说是一项重要的自由。通过使用 Tor 并对 Raspberry Pi 进行少量调整，你可以确保你所有的互联网流量都保持私密。

首先，你需要确保从软件仓库安装 Tor。打开 LXTerminal 并简单地输入：

```
sudo apt-get install tor
```

完成后，使用 `sudo nano /etc/tor/torrc` 编辑 torrc 文件，并在文件顶部添加以下内容：

```
VirtualAddrNetworkIPv4 10.192.0.0/16
AutoMapHostsOnResolve 1
TransPort 9040
DNSPort 53
```

保存此文件，然后使用 `sudo nano /etc/resolv.conf` 打开下一个文件并修改它：

```
nameserver 127.0.0.1
```

最后，你需要更改 iptables 规则集，但在这样做之前，请使用 `top` 确认 Tor 的 uid 并记录下来。现在使用 `nano /etc/init.d/iptables` 打开一个新文件，并输入在 [http://www.linuxuser.co.uk/wp-content/uploads/2014/08/tor.tor.zip](http://www.linuxuser.co.uk/wp-content/uploads/2014/08/tor.tor.zip) 找到的代码。现在保存它并输入：

```
chmod 755 /etc/init.d/iptables
update-rc.d iptables defaults
```

### 将它们结合在一起

可以通过查看 Adafruit 的 Onion Pi 项目来使用 Raspberry Pi 创建安全的无线连接：[learn.adafruit.com/onion-pi/overview](http://learn.adafruit.com/onion-pi/overview)

这将创建一个连接到互联网的无线接入点，通过将所有 web 流量引导通过 Tor 网络来使其匿名化。

这意味着你家的所有计算机和智能设备都可以连接到 Tor，而不仅仅是 Raspberry Pi 本身。你还可以将 Wi-Fi 中继器教程中学到的一些知识应用于解除其以太网线的束缚，尽管这会略微降低其整体安全性。

