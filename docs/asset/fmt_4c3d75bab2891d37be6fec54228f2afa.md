
你还可以使用 `iwconfig` 显示无线设备的统计信息，就像 `ifconfig` 一样。输入不带参数或带有设备名称的 `iwconfig` 命令。将列出名称、频率、灵敏度和比特率等信息。请也检查 `/proc/net/wireless` 以获取统计数据。

除了直接使用 `iwconfig` 设置参数外，你还可以在无线设备的配置文件中指定它们。无线设备配置文件将位于 `/etc/sysconfig/network-scripts` 目录中，并根据设备名称赋予类似 `ifcfg-eth1` 的名称。此文件已经包含了许多 `iwconfig` 设置。进一步的设置可以通过将 `iwconfig` 值分配给 `IWCONFIG` 参数来设置，如下所示：

```
IWCONFIG="rate 11M"
```

## iwpriv

`iwpriv` 命令与 `iwconfig` 配合使用，允许你设置特定类型无线设备的选项。使用 `iwpriv`，你还可以开启漫游或选择要使用的端口。你使用 `private-command` 参数输入设备特定的选项。以下示例设置开启漫游：

```
iwpriv eth0 roam on
```

## iwspy

你的无线设备可以检查其与其他无线设备的连接（正在从中接收数据），报告传输的质量、信号强度和噪声水平。你的设备可以维护一个地址列表，用于它可能接收数据的不同设备。你使用 `iwspy` 工具来设置或添加你想要检查的地址。你可以列出 IP 地址或硬件版本。`+` 号将添加地址，而不是替换整个列表：

```
iwspy eth0 +192.168.2.5
```

要显示你连接的质量、信号和噪声水平，你只需使用设备名称加 `iwspy` 命令：

```
iwspy eth0
```

## iwlist

要获取关于无线设备的更详细信息，例如所有可用的频率或信道，你使用 `iwlist` 工具。使用设备名称和特定参数，你可以获取关于设备的特定信息，包括频率、接入点、速率、电源功能、重试限制以及使用的加密密钥。你可以使用 `iwlist` 获取关于故障连接的信息。以下示例将列出 `eth0` 无线设备上使用的频率：

```
iwlist eth0 freq
```

## linux-wlan

`linux-wlan` 项目（[`www.linux-wlan.org`](http://www.linux-wlan.org)）开发了一套独立的无线驱动程序，专为支持新 802.11 无线标准的基于 Prism 的无线卡设计。`linux-wlan` 驱动程序目前不包括在 Fedora 中；你需要下载驱动程序。原始源代码包可从 `linux-wlan` 网站 [`www.linux-wlan.org`](http://www.linux-wlan.org) 获取。当前包为 `linux-wlan-ng`。你需要解包并编译驱动程序，如前一章中针对源代码软件包所述。

驱动程序将安装 WLAN 设备，设备配置放置在 `/etc/sysconfig/network-scripts` 目录中。例如，第一个 WLAN 设备的配置将在 `ifcfg-wlan0` 脚本中。一般无线选项放置在 `/etc/wlan.conf` 配置文件中。

## 设置防火墙：system-config-securitylevel

要设置防火墙，请在系统上运行 `system-config-securitylevel`（系统管理窗口和菜单中的安全级别）。在 1.8 版本中，你可以使用启用和禁用按钮启用或禁用防火墙（见图 5-5）。你可以在直接连接到互联网的独立系统上运行防火墙，也可以在将本地网络连接到互联网的网关系统上运行。大多数小型网络现在使用专用的路由器来访问互联网，这些路由器拥有自己的防火墙。`system-config-securitylevel` 的 1.7 版本还包括一个用于启用和禁用 SELinux 的面板（也可以使用 `system-config-selinux` 完成）。没有单独的面板用于其他防火墙端口。

**图 5-5**

`system-config-securitylevel` 工具，1.8 版本。

![](img/ab68ea377332b50bf70ef1316c8175b6_171_0.png)

自定义规则面板允许你加载一个可以保存自定义防火墙规则的 IP-tables 文件。你不必选择是使用 `system-config-securitylevel` 还是在一整个 IP-tables 文件中创建一套规则，你可以使用 `system-config-securitylevel` 自动配置标准防火墙规则，然后设置一个仅包含你系统自定义规则的 IP-tables 文件。这些规则将添加到 `system-config-securitylevel` 实现的标准集合中。有关 IP-tables 防火墙规则的详细讨论，请参阅第 20 章。

如果 Linux 系统也用于为更广泛的网络运行服务器，通常会被用作路由器。如果你正在创建强大的防火墙但仍希望运行如 Web 服务器等服务的，允许用户进行互联网上的 FTP 文件传输，允许 Samba 桌面浏览，或允许远程加密连接（如 SSH），你将需要在受信任服务面板中指定它们。Samba 桌面浏览允许你从 GNOME 或 KDE 桌面访问你的 Samba 共享，例如远程 Windows 文件系统。

自定义端口面板允许你指定可能需要为某些服务（如 BitTorrent）打开的端口。点击添加按钮打开一个对话框，你可以在其中输入要控制的协议（tcp 或 udp）的端口号。

## InfiniBand 支持

自 2.6.10 内核起，Fedora 包含 InfiniBand 支持。这是一种新的 I/O 架构，用于取代当前系统中使用的旧总线架构。InfiniBand 通常用作本地网络连接（LAN）的替代方案。它目前已在超级计算机和网络服务器集群中实现。你可以在以下网址找到有关 InfiniBand 的更多信息：

位于 `infiniband.sourceforge.net` 的 Linux InfiniBand 项目。InfiniBand 的支持由 OpenIB 联盟作为开源项目进行开发，网址为 `www.openib.org`。

当今的系统使用 PCI 总线或其增强版本，即 PCI X 或 PCI Express。这种 PCI I/O 架构使用共享总线，吞吐量仅能达到约 0.5 Gbps。集群服务器已经触及了这种 I/O 方式的上限。一种替代技术是 InfiniBand I/O 架构。InfiniBand 使用串行通道而非共享总线。速度从 2.6 Gbps 开始，最高可达 30 Gbps。与由单一主机控制事务处理的总线不同，InfiniBand 使用点对点通道架构，可以通过不同的通道管理多个连接。这种网络交换机架构使 InfiniBand 能够在不同节点之间进行切换。PCI Express 仅限于用作本地总线，连接 CPU 与外设。相比之下，InfiniBand 支持网络连接，允许您实现本地高速局域网以及到独立存储设备（如硬盘）的共享高速连接。使用 InfiniBand 线缆代替以太网线缆，您可以连接您的主机和共享设备（距离可达 50 英尺以内）。`IPoIB`（IP over InfiniBand）协议允许您在 InfiniBand 连接上实现 IP 网络，而 `RDMA` 协议可用于远程存储设备。InfiniBand 连接的高速度对于需要高带宽能力的服务器尤为重要。此外，Sockets Direct 协议（`SRP`）用于管理到硬盘的连接。

具有 PCI Express 的机器能够处理 InfiniBand 连接提供的更高带宽。放置在 PCI 插槽中的主机通道适配器（HCA）卡具有 InfiniBand 连接器，并将 InfiniBand 传输与 PCI Express 总线进行接口连接。内核中已经集成了几个 HCA 的驱动程序，以及协议驱动程序。

> *提示* *网络配置和互联网访问通常由专用的网络路由器处理。不过，您也可以将 Linux 系统配置为路由器，并用其自身的防火墙保护整个网络（参见第 20 章）。您还可以设置一个非常简单的配置，使用代理服务器仅提供 Web 访问。*

# 配置局域网

对于大多数网络，使用专用路由器来设置网络，提供域名服务（DNS）、防火墙和网络寻址。您可以设置 Linux 系统来提供这些操作，但通常只有在需要独特定制的网络配置，或者希望直接控制防火墙、DNS 和网络寻址软件，而不依赖路由器软件时，才需要这样做。对于某些网络，使用 Linux 仅来提供某些网络服务（如您控制的 DNS 服务器或复杂的防火墙）可能是合适的，而让路由器仅处理网络寻址。在这种情况下，Linux 系统将运行 DNS 服务器和配置好以管理网络的 IP 表防火墙。如果您的网络连接到子网络，您可能需要配置代理服务。

> *注意* *您可以使用 `system-config-bind` 来配置域名服务器（系统管理 | 服务器设置 | 域名系统）。*

Linux 系统还可以为本地网络运行邮件和打印服务器，以及 Web 和 FTP 服务。这些服务设计用于与任何 DNS 或防火墙服务配合工作，而不仅仅是 Linux 版本。您可以使用 Linux 设置 Web 和打印服务器，让专用路由器处理防火墙和 DNS 服务。

下表列出了本地网络中常用的网络服务：
