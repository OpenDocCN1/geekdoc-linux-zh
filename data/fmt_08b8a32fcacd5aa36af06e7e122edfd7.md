
```
$ iwconfig wlan0
wlan0      IEEE 802.11b/g SSID:"vwh" Nickname:"acx v0.3.36"
            Managed Frequency:2.437 GHz Access Point: 00:06:25:78:CE:3F
            Bit Rate:5.5 Mb/s Tx-Power:15 dbm Sensitivity:1/3
            Retry min limit:7 RTS thr:off
            Power Management:off
            Link Quality:31/100 Signal level=3/100 Noise level=0/100
            Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:0
            Tx excessive retries:0 invalid misc:0 Missed beacon:0
```

如你所见，它包含了许多 `ifconfig` 命令提供的信息，但也包含了无线特定的信息。`iwconfig` 命令还可以从命令行设置各种无线配置选项——更多信息请参考 `iwconfig` 的在线页面（使用命令 `man iwconfig`）。

`iwlist` 命令允许扫描无线网络并检查无线接口的各种特性。例如，使用 `iwlist wlan0 scan` 扫描我家周围的无线网络会显示以下信息：

```
$ iwlist wlan0 scanning
wlan0      Scan completed:
            Cell 01   Address: 00:18:01:F4:0A:08
                       ESSID:"PY3N*"
                       Mode:Master
                       Frequency:2.462 GHz (Channel 11)
                       Quality:37/100 Signal level=12/100 Noise level=0/100
                       Encryption key:on
                       Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 6 Mb/s; 9 Mb/s
                              11 Mb/s; 12 Mb/s; 18 Mb/s; 24 Mb/s; 36 Mb/s
                              48 Mb/s; 54 Mb/s
            Cell 02   Address: 00:03:93:E9:89:22
ESSID: "vwh*"
Mode:Master
Frequency:2.427 GHz (Channel 4)
Quality=52/100 Signal level=34/100 Noise level=0/100
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 6 MB/s; 9 MB/s
11 MB/s; 12 MB/s; 18 MB/s; 24 MB/s; 36 MB/s
48 MB/s; 54 MB/s

Cell 03 - Address: 00:06:25:78:CE:3F
ESSID: "vwh*"
Mode:Master
Frequency:2.437 GHz (Channel 6)
Quality=57/100 Signal level=40/100 Noise level=0/100
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s
```

该命令用于验证无线接口是否在正常工作以及是否能与访问点通信。`iwlist` 命令提供的信息在公共区域非常有用，因为那里通常会检测到更多的无线网络，如下面我在度假期间其中一台笔记本电脑记录的示例：

```
$ sudo iwlist eth0
Password:
Scan completed :
Cell 01 - Address: 00:09:5B:36:22:38
ESSID: "Wireless"
Mode:Master
Frequency:2.412 GHz (Channel 1)
Signal level=220/153 Noise level=12/153
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s
Cell 02 - Address: 00:12:17:A6:E8:C8
ESSID: "linksys"
Mode:Master
Frequency:2.437 GHz (Channel 6)
Signal level=83/153 Noise level=13/153
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s
Cell 03 - Address: 00:12:17:A6:E8:C8
ESSID: "linksys"
Mode:Master
Frequency:2.437 GHz (Channel 6)
Signal level=81/153 Noise level=13/153
Encryption key:off
Bit Rates:1 MB/s; 2 MB/s; 5.5 MB/s; 11 MB/s
Cell 04 - Address: 00:12:17:79:CF:D3
ESSID:"linksysR79cfd3"
Mode:Master
Frequency:2.437 GHz (Channel 6)
Signal level:49/153 Noise level:13/153
Encryption key:off
Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s; 18 Mb/s; 24 Mb/s; 36 Mb/s; 54 Mb/s
```

如你所见，它包含了许多 `ifconfig` 命令提供的信息，但也包含了无线特定的信息。`iwconfig` 命令还可以从命令行设置各种无线配置选项——更多信息请参考 `iwconfig` 的在线页面（使用命令 `man iwconfig`）。

`iwlist` 命令允许你扫描无线网络并检查无线接口的各种特性。例如，使用 `iwlist wlan0 scan` 扫描我家周围的无线网络会显示以下信息：

该命令用于验证无线接口是否在正常工作以及是否能与访问点通信。`iwlist` 命令提供的信息在公共区域非常有用，因为那里通常会检测到更多的无线网络，如下面我在度假期间其中一台笔记本电脑记录的示例：

如你所见，包含了许多 `ifconfig` 命令提供的信息，但也包含了无线特定的信息。`iwconfig` 命令还可以从命令行设置各种无线配置选项——更多信息请参考 `iwconfig` 的在线页面（使用命令 `man iwconfig`）。

`iwlist` 命令允许你扫描无线网络并检查无线接口的各种特性。例如，使用 `iwlist wlan0 scan` 扫描我家周围的无线网络会显示以下信息：

## 安装 Microsoft Windows 驱动程序

本节介绍如何使用图形化 `ndisgtk` 工具安装 Microsoft Windows 驱动程序，该工具为 `ndiswrapper` 工具、内核模块以及 Ubuntu 网络配置提供了一个友好的外壳。你也可以在任何命令行环境中使用 `sudo ndiswrapper -i [INF文件名]` 命令来安装供 `ndiswrapper` 内核模块使用的 Windows 驱动程序，然后手动修改一些配置文件，但我更倾向于使用 `ndisgtk` 工具提供的图形化一站式方案。

## 第 22 章：进入无线世界

## 注意

在安装 Windows 驱动程序之前，你必须确保你的 Ubuntu 系统中可以找到这些程序。这通常涉及将驱动程序 CD 插入系统使其可以作为 `/media/cdrom`（或类似的路径，取决于你 Ubuntu 系统中的驱动器），或者将包含驱动程序的 zip 压缩包复制到你的 Ubuntu 系统中，并使用 `unzip` 命令将该文件的内容提取到 Ubuntu 目录。

安装 `ndisgtk` 包会在 Ubuntu 系统上创建“系统管理 Windows 无线驱动”（System Administration Windows Wireless Drivers）菜单项，你可以选择它启动 `ndisgtk` 应用。图 22-8 显示了首次启动此应用程序时显示的驱动安装对话框。

### 图 22-8

`ndisgtk` 启动对话框

![](img/1a233c34336fbf5a85d6eb785e401709_854_0.png)
