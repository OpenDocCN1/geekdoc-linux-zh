
```
# mkdir wireless
# cd wireless/
# wget http://ftp.linksys.com/pub/network/wpc54g_v2_driver_utility_v2.0.zip
```

4. 文件下载完成后，解压驱动程序文件。对于此示例，我输入了：

```
# unzip wpc54g_v2_driver_utility_v2.0.zip
```

5. 安装 `kernel-devel` 和 `gcc` 包。然后将内核目录链接到模块目录或你当前的内核（将 `<kernel-version>` 替换为你的内核开发包和当前内核的版本号，如所示）：

```
# yum install kernel-devel gcc
# ln -s /usr/src/kernels/<kernel-version> /lib/modules/<kernel-version>/build
```

6. 通过从以下网站下载到你的 Fedora 或 RHEL 系统来获取 `ndiswrapper` 源代码：http://sourceforge.net/projects/ndiswrapper。

> 注意：在 `rpm.livna.org` 上也有可供 Fedora 使用的 `ndiswrapper` RPM 包。如果你决定走这条路，除了安装源代码外，请确保你找到与你内核版本匹配的 `ndiswrapper` 包。有关启用 `rpm.livna.org` 软件库的信息，请参见第 5 章。

7. 在当前目录中包含 `ndiswrapper` 源代码包，如下所示进行解压和 untar：

```
# tar xvfz ndiswrapper-*tar.gz
```

8. 作为 root 用户，切换到 `ndiswrapper` 目录并运行 `make` 命令，如下所示：

```
# cd ndiswrapper*
# make install
```

## 第15章：设置局域网

9. 从解压的驱动程序包中获取 INF 文件。在我们的示例中，我们需要的文件是 `lsbcmds.inf`。然后运行 `ndiswrapper -i` 命令安装驱动程序。例如，在当前目录中包含 `lsbcmds.inf` 文件，我运行了：

```
# ndiswrapper -i lsbcmds.inf
```

10. 检查驱动程序是否可用以及硬件是否可用：

```
# ndiswrapper -l
lsbcmds    driver present, hardware present
```

11. 要加载 `ndiswrapper` 模块，请输入以下内容

```
# modprobe ndiswrapper
```

12. 输入以下命令以查看你的无线局域网（`wlan`）条目：

```
# iwconfig
```

13. 输入以下内容以查看你的接入点：

```
# iwlist wlan0 scan
```

14. 为你的无线设备创建一个指向 `wlan0` 的别名，以便该接口在启动时自动加载：

```
# ndiswrapper -m
```

15. 要检查 `ndiswrapper` 模块是否加载正常，你可以检查 `/var/log/messages` 文件。模块加载后出现了以下消息：

```
Nov  2 20:28:53 toys kernel: ndiswrapper version 1.42 loaded
(preempt=no,mp=no)
Nov  2 20:28:53 toys kernel: ACPI: PCI interrupt 0000:00:0a.0[A] ->
GSI 5 (level, low) -> IRQ 5
Nov  2 20:28:53 toys kernel: ndiswrapper: using irq 5
Nov  2 20:28:54 toys udev: creating device node '/dev/ndiswrapper'
Nov  2 20:28:54 toys kernel: wlan0: ndiswrapper ethernet
device 00:0f:66:6f:b9:0a using driver lsbcmds
Nov  2 20:28:54 toys kernel: wlan0: encryption modes supported:
WEP, WPA with TKIP, AES/CCMP
Nov  2 20:28:54 toys kernel: ndiswrapper: driver lsbcmds
(The Linksys Group, Inc.,07/17/2003, 3.30.15.0) added
```

从输出中，你可以看到 `ndiswrapper` 模块已加载，它找到了无线 PCI 卡，并且 `wlan0` 接口被分配给该设备并使用 `lsbcmds` 驱动程序。在正确检测到卡片后，你可以配置 TCP/IP 以用于该卡。

## 安装无线 Linux 软件

对于大多数 Fedora 或 RHEL 安装类型，创建你的无线局域网所需的软件包通常已经安装。支持 PCMCIA 卡和无线网卡所需的驱动程序和模块应该在系统中。除了无线驱动程序外，以下软件包包含用于在 Fedora 和 RHEL 中配置和操作无线局域网卡的工具：

- `pcmciautils` — 包含用于支持你的无线卡（如果它恰好是 PCMCIA 卡）的命令和配置文件。
- `wireless-tools` — 包含用于设置无线局域网接口扩展的命令。命令包括 `iwconfig`（用于配置你的无线接口）和 `iwlist`（用于列出无线统计信息）。

建立无线局域网接口后，你可以使用各种 Linux 软件来监控和控制对该接口的访问。你还需要安装适当的软件包。以下是一些在 Fedora 中你可能发现有用的其他无线软件包示例：

- `aircrack-ng` — 可用于审计无线网络
- `wifi-radar` — 扫描可用的无线网络
- `kismet` — 嗅探 802.11 无线网络
- `wifiroam` — 允许你搜索最佳可用接入点
- `airsnort` — 具有检查无线加密密钥强度的工具

## 配置无线局域网

在开始测试你可以在无线 Linux 局域网中实现的距离之前，我建议你在两台能够直接看到彼此位置上的计算机上配置无线网卡。当两台计算机能够通信后，你可以更改无线设置以调整连接，并开始尝试传输距离。

以下部分描述了在两个 Linux 系统之间设置无线局域网所需的步骤。虽然只描述了两个节点，但一旦你知道方法，你就可以向你的无线局域网添加更多计算机。本程序描述了如何以两种不同模式运行你的无线 Linux 局域网：

- `Ad hoc`（临时组网） — 你无线局域网中的所有计算机都汇集到一个仅由一个单元组成的单一虚拟网络中。单一单元意味着你无法在不同无线节点组之间漫游并无缝地继续通信。要做到这一点需要一个受管理的网络。
- `Managed`（受管理） — 如前所述，Linux 支持的许多无线网卡不能作为接入点运行。然而，Linux 无线网卡可以作为受管理的节点运行网络。随 Fedora 和 RHEL 附带的无线配置工具允许您通过指定接入点的 MAC 地址来识别 Linux 要使用的接入点。

按照制造商的说明安装您的无线网卡。然后按照以下程序为每张卡配置接口。

> 注意：NetworkManager 项目开发了一些易于使用的工具，用于配置和管理您的网络接口。NetworkManager 在笔记本电脑上尤其有用，因为在那里您需要配置与多个无线网络的连接。若要试用 NetworkManager，请安装 `NetworkManager` 和 `NetworkManager-gnome` 软件包。启动该服务（`service NetworkManager start` 和 `chkconfig NetworkManager on`）。然后选择顶部面板中出现的图标，以创建无线网络或连接到现有网络。使用 NetworkManager 时，如果有线以太网接口处于活动状态，无线接口将不会自动启动。您将不得不手动配置无线接口以同时使用两者。

## 配置无线接口

网络配置窗口（`neat` 命令）可用于配置无线以太网卡接口，以及普通的有线以太网卡。以下程序描述了如何使用网络配置窗口配置无线以太网卡。

> 注意：如果您的无线卡驱动程序未出现在列表中，您可能需要手动配置无线卡，如本章稍后所述。请按照此程序进行操作，如果您无法激活无线卡，请参考 `ifcfg-eth1` 文件的说明。
