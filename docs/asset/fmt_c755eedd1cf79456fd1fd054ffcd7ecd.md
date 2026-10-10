
http://ndiswrapper.sourceforge.net/mediawiki/index.php/Fedora

> 注意：由于 Fedora 中现在有了 `BCM43xx` 驱动程序，你可以使用它从包中提取固件与原生 Linux 驱动程序配合使用。之后，重启应该正确检测并加载网卡所需的模块。例如，在下面的步骤中解压 `wpc54g` zip 文件后，在当前目录下带有 `bcmwl5.s` 文件输入以下命令：

```
# bcm43xx-fwcutter -w /lib/firmware/ bcmwl5
```

如果你发现无线卡在 Fedora 驱动程序下无法工作，可以使用 `ndiswrapper` 让你的无线卡正常工作。然而，由于 Fedora 会尝试使用原生驱动程序而不是 `ndiswrapper`，你可能需要将 Fedora 想要使用的无线驱动程序禁用。

### 确定无线网卡类型

1. 确定你正在使用的无线卡类型。如果你有一块 PCI 卡，输入：

```
# lspci -v | less
```
```
00:0a.0 Network controller: Broadcom Corporation BCM4306 002.11b/g\Wireless LAN Controller (rev 03)
```
```
Subsystem: Linksys: Unknown device 0014
Flags: bus master, fast devsel, latency 64, IRQ 5
Memory at ee000000 (32-bit, non-prefetchable) [size=8K]
```

在这个示例中，PCI 卡是 `BCM4306`。

2. 如果你的卡是 USB 设备，请改用 `lsusb`。

3. 如果你的卡在列表中，下载内容：http://sourceforge.net/projects/ndiswrapper。

4. 在下面的步骤中解压 `wpc54g` zip 文件后，输入：

```
# tar xf wpc54g.tar.gz
```

5. 安装 `kernel-devel` 和 `gcc` 包。

```
# yum install kernel-devel gcc
```

6. 如果你决定采用该方案，请确保内核版本与你的操作系统匹配。

7. 进入 `iswrapper` 目录并运行：

```
# make
```

8. 从我们的示例中，我们需要：

```
# make install
```

9. 从当前目录获取 INF 文件，运行：

```
# ndiswrapper -i
```

10. 检查驱动程序现在是否可用以及硬件是否存在：

```
# ndiswrapper -1
```

11. 要加载 `ndiswrapper` 模块，输入：

```
# modprobe ndiswrapper
```

12. 输入以下命令查看你的无线局域网条目：

```
# iwconfig
```

13. 输入以下内容查看访问点：

```
# iwlist wlan0 scan
```

14. 为你的无线设备创建一个到 `wlan0` 的别名，以便接口在启动时自动加载：

```
# ndiswrapper -m
```

15. 检查 `ndiswrapper` 模块是否正确加载，你可以检查 `/var/log/messages`。这些消息在模块加载后出现：

> Nov 2 20:28:53 kernel: ndiswrapper version 1.42 loaded

(preempt-no,smp=no)

Nov 2 20:28:53 kernel: ACPI: PCI interrupt 0000:00:0a.0[A] -> GSI 5 (level, low) -> IRQ 5

Nov 2 20:28:53 kernel: ndiswrapper: using irq 5

Nov 2 20:28:54 kernel udev: creating device node '/dev/ndiswrapper'

Nov 2 20:28:54 kernel wlan0: ndiswrapper ethernet device 00:6f:f6:b9:0a: using driver lsbccnds

Nov 2 20:28:54 kernel wlan0: encryption modes supported: WEP, WPA with TKIP, AES/CCMP

Nov 2 20:28:54 kernel: ndiswrapper: driver lsbccnds

(The Linksys Group, Inc.,07/17/2003, 3.30.15.0) added

从输出可以看出，`ndiswrapper` 模块已加载，它找到了无线 PCI 卡，并且使用 `lsbccnds` 驱动程序为该设备分配了 `wlan0` 接口。在卡被正确检测后，你可以配置 TCP/IP 来使用该卡。

# 安装 Linux 无线软件

对于大多数 Fedora 或 RHEL 安装版本，创建无线局域网（LAN）所需的软件包通常已经安装。支持 PCMIA 卡和无线网卡所需的驱动程序和模块应存在于你的系统中。除了无线驱动程序外，以下软件包包含了在 Fedora 和 RHEL 中配置和操作无线局域网卡的工具：

- `pciutils` — 包含命令和配置文件，如果你的无线卡是 PCMIA 卡，则它们可以支持它。
- `wireless-tools` — 包含用于设置无线局域网接口扩展的命令。命令包括 `ifconfig`（用于配置你的无线接口）和 `iwlist`（用于列出无线统计数据）。

建立无线局域网接口后，你可以使用各种 Linux 软件来监控和控制该接口的访问。你可能需要安装相应的软件包。以下是 Fedora 中你可能会发现的一些其他软件包示例：

- `aircrack-ng` — 可用于审计无线网络
- `wifi-radar` — 扫描可用的无线网络
- `kismet` — 嗅探 802.11 无线网络
- `wifiiroamd` — 让你搜索最佳可用的接入点
- `airsnort` — 具有检查无线加密密钥强度的工具

# 配置无线局域网

在开始测试你的 Linux 无线局域网可以实现的距离之前，我建议在两台相互对视的电脑上配置无线网卡。在两台电脑通信后，你可以更改无线设置来调优连接并开始实验传输距离。

后续章节描述了在两个 Linux 系统之间建立无线局域网所需的步骤。虽然只描述了两个节点，一旦你学会了如何操作，就可以向无线局域网中添加更多计算机。此过程描述了以两种模式操作你的无线局域网：

- Ad hoc（自格式）——无线局域网中的所有计算机都聚集在一个仅由一个单元组成的虚拟网络中。单单元意味着你不能在无线节点组之间漫游并继续隐性通信。这需要一个托管网络。
- Managed（托管）——如前所述，Linux 支持的许多网卡无法作为接入点工作。然而，Linux 无线网卡可以作为托管网络中的节点

# 第 15 章：建立本地局域网

Fedora 和 RHEL 自带的无线配置工具允许你通过指定接入点的 MAC 地址来识别 Linux 的接入点。

按照制造商的说明安装你的无线网卡。然后按照后续步骤描述为每张网卡配置接口。

> 注意：`NetworkManager` 开发了一些易于使用的工具来配置和管理你的网络接口。`NetworkManager` 在笔记本电脑上特别有用，因为你需要在配置到多个无线网络的连接。要尝试 `NetworkManager`，请安装 `NetworkManager` 和 `NetworkManager-gnome` 软件包。启动服务（`service NetworkManager start` 和 `checkconfig on`）。然后选择顶部面板栏中出现的图标来创建无线网络或连接到现有网络。使用 `NetworkManager`，如果有线以太网接口处于运行状态，无线接口将不会自动启动。你必须手动配置无线接口才能使用它。

# 配置无线接口

网络配置窗口（`neat` 命令）可用于配置无线以太网卡，也用于普通以太网卡。以下步骤描述了如何使用网络配置窗口配置无线以太网卡。

> 注意：如果你的卡驱动程序没有出现在列表中，你可能需要按照本章稍后描述的，手动配置无线网卡。执行此步骤，如果你无法激活无线网卡，请参考 `ifcfg-eth1` 文件的描述。

1. 启动网络配置。从桌面菜单中，点击系统管理 -> 网络，或者作为 root 用户从终端窗口输入 `neat`。网络配置窗口出现。

2. 点击 `New`（新建）按钮。出现选择设备类型。

3. 点击 `connection`（连接）并点击 `Forward`（前进）。出现选择无线设备窗口。

4. 从显示的网卡列表中选择你的无线网卡，并点击 `Forward`（前进）。出现配置无线连接窗口，如图 15-10 所示。

5. 添加以下信息并点击 `Forward`：

   - `Mode`（模式）——指明无线局域网卡的运行模式。由于我正在设置一个仅包含一个单元的网（也就是说，在其他区域没有漫游单元），可以将模式设置为 `Ad hoc`。`Ad hoc` 允许网卡与其每个对等节点直接通信。如果你有多个单元，可以使用 `Managed` 模式，这要求你的网卡与接入点直接通信。你也可以为对点网络使用 `Managed`。
