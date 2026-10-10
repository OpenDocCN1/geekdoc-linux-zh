
如果您在几台距离非常近的电脑之间建立无线局域网，您可能不需要额外的天线。然而，为了应对障碍和更远的距离，您可以为您的无线硬件添加室内或室外天线。

在后续章节中，我将说明与这些网卡兼容的不同类型的室内室外天线。

# 使用室内天线

无线局域网卡内置的天线足以实现开放区域内计算机之间的通信。如果无线卡之间的直接视线被阻挡，额外的室内天线将很有用。一叠纸可能会抑制传输，而一块金属板可能会完全阻止传输。一个能让传输远离卡的小天线可能是解决这些问题的答案。

虽然大多数无线局域网卡不需要完全无遮挡的视线，但障碍物可能会减慢接收。为了解决这个问题，像 `Orinoco IEEE` 范围扩展器这样的天线可以直接插入 `Orinoco Gold` 或 `Silver` 无线局域网卡中。`1.5` 米长的扩展线可以将信号从关闭的门后引出或到桌面上。当您设置天线时，建议将其：

- 放置在中心位置。
- 垂直安装。
- 远离障碍物（特别是金属表面，以及程度较小的固体物体，如混凝土墙或一叠纸）。

请参考随天线附带的说明书以获取有关放置和安装天线的具体指南。

# 使用室外天线

为您的无线局域网选择和设置室外天线可能比在室内更困难、更昂贵。然而，一旦室外天线到位，您就可以节省费用，因为您不需要多个互联网账户（月费、DSL/电缆调制解调器等）。

虽然在无线局域网中使用室外天线的完整描述在本章的范围之外，但有一些提示可以帮助您为无线局域网选择最佳天线。

- 点对点与多点连接——如果您在两个户外位置之间建立点对点链路（例如，在两栋建筑之间共享互联网连接），定向天线可以帮助您实现更大的距离和传输速度。然而，如果您的天线为几个其他室外天线或无线客户端提供多点访问（例如在校园草坪上使用笔记本电脑的学生），则全向天线可能更合适。
- 空旷度 —— 每个室外天线之间的视线越清晰，您能实现的距离和传输速度就越大。将天线放置在尽可能高点可以防止树木、汽车、建筑和其他物体导致性能下降。障碍物与您的无线传输覆盖区域之间的距离被称为空旷因子（见图 15-9）。

![](img/c7605e408543e0a1829c1fd0cf2f687d_686_0)

- 距离 —— 传输变化的实际距离根据因素变化很大。
- 电缆因素 —— 电缆的质量可以是选择正确天线的因素之一。
- 增益以分贝（`dBi`）测量。更高的增益意味着更好的机会。

# 第 15 章：建立局域网 649

# 获取无线驱动

如果您使用的无线卡包含 Fedora 或 RHEL 的驱动程序，它可能会被自动检测，稍后您将按照描述进行配置。

# 第四部分：Fedora RHEL 网络设置

注意：大部分步骤来自 `INSTALL` 文件。您应该检查在新版本发布后程序是否发生变化。

1. 确定您使用的无线卡类型。如果您使用的是 PCI 卡，输入：

```
# lspci -v | less
00:0a.0 Network controller: Broadcom Corporation BCM4306 802.11g
Wireless Controller (rev 03)
Subsystem: Linksys: Unknown device 0014
Flags: bus master, devsel, latency 64, IRQ 5
Memory at ee00000 (32-bit, nonprefetchable) size=8K
```

在本例中，PCI 卡是 Broadcom 公司的 `BCM4306` `802.11g` 无线控制器。

2. 查看以下在 `ndiswrapper` 下运行的无线卡驱动程序列表：

3. 如果您的卡在列表中，请按照该页面下载驱动程序。我使用了 Linksys `WMP54GS` 无线 G PCI 适配器（对应上面 `lspci` 输出中显示的芯片 `BCM4306 802.11g`）。因此我如下下载了驱动程序：

```
# mkdir wireless
# cd wireless
# wget ftp://ftp.linksys.com/pub/network/wpc54g_v2_driver_utility_v2.0.zip
```

4. 文件下载完成后，对于示例，我输入了：

```
# unzip wpc54g_v2_driver_utility_v2.0.zip
```

5. 接下来，从以下网站下载 `ndiswrapper` 软件（目前只有源码）到您的 Fedora 或 RHEL 系统：`http://sourceforge.net/projects/ndiswrapper`。

6. 当 `ndiswrapper` 源码包位于当前目录下，解压并解包：

```
# tar xvfz ndiswrapper*-tar.gz
```

7. 作为 root 用户，进入 `ndiswrapper` 目录并执行 `make` 命令：

```
# cd ndiswrapper*
# make install
```

# 第 15 章：建立局域网 653

8. 从解压的驱动包中获取 INF 文件。在我们的示例中，需要的文件是 `lsbcmnds.inf`。然后运行 `ndiswrapper -i` 命令安装驱动程序。例如，如果 `lsbcmnds.inf` 文件在当前目录下，我运行：

```
# ndiswrapper -i lsbcmnds.inf
```

9. 检查驱动程序和硬件现在是否可用：

```
# ndiswrapper -1
lsbcmnds driver present, hardware present
```

10. 加载 `ndiswrapper` 模块，输入以下内容：

```
# modprobe ndiswrapper
```

11. 输入以下命令查看你的无线局域网（`wlan`）条目：

```
# ifconfig
```

12. 输入以下内容查看你的接入点：

```
# iwlist wlan0 scan
```

13. 为你的无线设备创建一个 `wlan0` 的别名，以便接口在启动时自动加载：

```
# ndiswrapper -m
```

14. 要要检查 `ndiswrapper` 模块是否正确加载，你可以检查 `/var/log/messages` 文件。这些消息在模块加载后出现：

> Nov 2 20:28:53 toys kernel: ndiswrapper version 0.11 loaded (preempt=no,smp=no)

> Nov 2 20:28:53 toys kernel: ACPI: PCI interrupt 0000:00a:0a[A] -> GSI 5 (level, low) -> IRQ 5

> Nov 2 20:28:53 toys kernel: ndiswrapper: using irq 5

> Nov 2 20:28:54 toys kernel: udev: creating device node '/dev/ndiswrapper'

> Nov 2 20:28:54 toys kernel: wlan0: ndiswrapper ethernet device 00:af:66:bf:90a using driver lsbcmnds

> Nov 2 20:28:54 toys kernel: wlan0: encryption modes supported: WEP, WPA with TKIP, AES/CCMP

> Nov 2 20:28:53 toys kernel: ndiswrapper: driver lsbcmnds (The Linksys Group, Inc., 07/17/2003, 3.30.15.0) added

从输出中你可以看到 `ndiswrapper` 模块已加载，它找到了无线 PCI 卡，并且 `wlan0` 接口已分配给使用 `lsbcmnds` 驱动的设备。网卡检测正常后，你可以配置 TCP/IP 以使用该网卡。

# 安装 Linux 无线软件

对于大多数 Fedora 或 RHEL 安装类型，创建无线局域网所需的包已经安装完毕。支持 PCMCIA 卡和无线卡所需的驱动程序和模块应该已在你的系统中。除了无线驱动程序外，以下软件包包含了在 Fedora 和 RHEL 中配置和操作无线局域网网卡的工具：

- `pcmciutils` — 如果无线卡恰好是 PCMCIA 卡，它包含支持所需的命令和配置文件。
- `wireless-tools` — 包含用于设置无线局域网接口扩展的命令。命令包括 `ifconfig`（用于配置无线接口）和 `iwlist`（用于列出无线统计信息）。

建立无线局域网接口后，你可以使用各种 Linux 软件来监控和控制对该接口的访问。你也需要安装相应的软件包。

# 配置无线局域网

在开始尝试无线 Linux 局域网可以实现的距离之前，我建议在两台直视对方的电脑上配置无线卡。在两台电脑通信后，你可以更改无线设置来调整连接，并开始实验传输距离。

以下章节描述了在两个 Linux 系统之间建立无线局域网所需的步骤。虽然只描述了两个节点，但一旦你学会了方法，就可以向无线局域网中添加更多计算机。本过程描述了如何在不同模式下操作你的无线局域网：
