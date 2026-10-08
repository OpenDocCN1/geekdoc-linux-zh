

要启动 **wv dial**，请输入命令 `wv dial`，该命令会从 `/etc/wvdial.conf` 文件中读取连接配置信息；`wv dial` 会拨号连接 ISP 并启动 PPP 连接，在要求时提供用户名和密码。

```
$ wv dial
```

你可以在 `/etc/wvdial.conf` 文件中为任意数量的连接设置连接配置。要选择其中一个，请将其标签作为参数输入到 `wv dial` 命令中，如下所示：

```
$ wv dial myisp
```

## 手动无线配置

NetworkManager 会自动检测并配置你的无线连接，KNetworkmanager 也是如此。但是，你可以使用诸如 `iwconfig` 等无线工具手动配置你的连接。无线配置使用了相同的一组无线扩展。无线工具包是一组用于 Linux 系统上安装的无线设备的网络配置和报告工具。它们目前作为 Linux 无线扩展和无线工具项目的一部分得到支持和开发，这是一个由惠普维护的开源项目。

无线工具包括此处列出的配置和报告工具：

| 工具 | 描述 |
| --- | --- |
| iwconfig | 设置大多数无线设备的基本无线配置选项。 |
| iwlist | 显示设备的当前状态信息。 |
| iwspy | 设置无线网络中的 IP 地址列表并检查其连接质量。 |
| iwpriv | 访问特定于某个设备的配置选项。 |

无线局域网设备将拥有与伦特网卡相同的以太网名称。相应的模块会自动加载，并将它们的别名列在 `/etc/modprobe.conf` 文件中。

## iwconfig

`iwconfig` 命令的工作方式与 `ifconfig` 非常相似，用于配置网络连接。它是 system-config-network 用于配置无线卡的工具。或者，你可以直接在命令行上运行 `iwconfig`，并指定某些参数。附加的参数允许你设置无线特定功能，例如网络名称（ssid）、卡片使用的频率或信道（freq 或 channel）以及传输的比特率（rate）。有关可接受参数的完整列表，请参阅 `iwconfig` 手册页。表 5-3 中列出了一些常用参数。

例如，要设置为作为第一个以太网设备安装的无线设备所使用的信道，请使用以下内容，将信道设置为 2：

```
iwconfig eth0 channel 2
```

| 参数 | 描述 |
| :------- | :------- |
| essid | 网络名称 |
| freq | 连接的频率 |
| channel | 使用的信道 |
| nwid 或 domain | 网络 ID 或域 |
| mode | 设备使用的操作模式，例如 Ad Hoc、Managed 或 Auto。Ad Hoc = 没有接入点的单个单元；Managed = 具有多个接入点并支持漫游的网络；Master = 节点是接入点；Repeater = 节点将数据包转发到其他节点；Secondary = 备用主节点或中继器；Monitor = 仅接收数据包 |
| sens | 灵敏度，即可以接收数据的最低信号电平 |
| key 或 enc | 使用的加密密钥 |
| frag | 将数据包切割成更小的片段以提高传输效果 |
| bit 或 rate | 比特传输速率。auto 选项会自动回退到嘈杂信道的较低速率。 |
| ap | 指定特定的接入点 |
| power | 唤醒和睡眠操作的电源管理 |

表 5-3 常用参数

你还可以使用 iwconfig 显示无线设备的统计信息，就像 ifconfig 一样。输入不带参数或带有设备名称的 iwconfig 命令。将列出名称、频率、灵敏度和比特率等信息。请也检查 /proc/net/wireless 以获取统计数据。

除了直接使用 iwconfig 设置参数外，你还可以在无线设备的配置文件中指定它们。无线设备配置文件将位于 /etc/sysconfig/network-scripts 目录中，并根据设备名称赋予类似 ifcfg-eth1 的名称。此文件已经包含了许多 iwconfig 设置。进一步的设置可以通过将 iwconfig 值分配给 IWCONFIG 参数来设置，如下所示：

```
IWCONFIG="rate 11M"
```

## iwpriv

iwpriv 命令与 iwconfig 配合使用，允许你设置特定类型无线设备的选项。使用 iwpriv，你还可以开启漫游或选择要使用的端口。你使用 private-command 参数输入设备特定的选项。以下示例设置开启漫游：

```
iwpriv eth0 roam on
```

## iwspy

你的无线设备可以检查其与其他无线设备的连接（正在从中接收数据），报告传输的质量、信号强度和噪声水平。你的设备可以维护一个地址列表，用于它可能接收数据的不同设备。你使用 **iwspy** 工具来设置或添加你想要检查的地址。你可以列出 IP 地址或硬件版本。+ 号将添加地址，而不是替换整个列表：

```
iwspy eth0 +192.168.2.5
```

要显示你连接的质量、信号和噪声水平，你只需使用设备名称加 **iwspy** 命令：

```
iwspy eth0
```

## iwlist

要获取关于无线设备的更详细信息，例如所有可用的频率或信道，你使用 **iwlist** 工具。使用设备名称和特定参数，你可以获取关于设备的特定信息，包括频率、接入点、速率、电源功能、重试限制以及使用的加密密钥。你可以使用 **iwlist** 获取关于故障连接的信息。以下示例将列出 **eth0** 无线设备上使用的频率：

```
iwlist eth0 freq
```

## linux-wlan

linux-wlan 项目（ [**www.linux-wlan.org**](http://www.linux-wlan.org)）开发了一套独立的无线驱动程序，专为支持新 802.11 无线标准的基于 Prism 的无线卡设计。linux-wlan 驱动程序目前不包括在 Fedora 中；你需要下载驱动程序。原始源代码包可从 linux-wlan 网站 [**www.linux-wlan.org**](http://www.linux-wlan.org) 获取。当前包为 linux-wlan-ng。你需要解包并编译驱动程序，如前一章中针对源代码软件包所述。

驱动程序将安装 WLAN 设备，设备配置放置在 /etc/sysconfig/network-scripts 目录中。例如，第一个 WLAN 设备的配置将在 **ifcfg-wlan0** 脚本中。一般无线选项放置在 /etc/wlan.conf 配置文件中。

## 设置防火墙：system-config-securitylevel

要设置防火墙，请在系统上运行 system-config-securitylevel（系统管理窗口和菜单中的安全级别）。在 1.8 版本中，你可以使用启用和禁用按钮启用或禁用防火墙（见图 5-5）。你可以在直接连接到互联网的独立系统上运行防火墙，也可以在将本地网络连接到互联网的网关系统上运行。大多数小型网络现在使用专用的路由器来访问互联网，这些路由器拥有自己的防火墙。system-config-securitylevel 的 1.7 版本还包括一个用于启用和禁用 SELinux 的面板（也可以使用 system-config-selinux 完成）。没有单独的面板用于其他防火墙端口。

**图 5-5**
system-config-securitylevel 工具，1.8 版本。

![](img/ab68ea377332b50bf70ef1316c8175b6_171_0.png)

自定义规则面板允许你加载一个可以保存自定义防火墙规则的 IP-tables 文件。你不必选择是使用 system-config-securitylevel 还是在一整个 IP-tables 文件中创建一套规则，你可以使用 system-config-securitylevel 自动配置标准防火墙规则，然后设置一个仅包含你系统自定义规则的 IP-tables 文件。这些规则将添加到 system-config-securitylevel 实现的标准集合中。有关 IP-tables 防火墙规则的详细讨论，请参阅第 20 章。

如果 Linux 系统也用于为更广泛的网络运行服务器，通常会被用作路由器。如果你正在创建强大的防火墙但仍希望运行如 Web 服务器等服务的，允许用户进行互联网上的 FTP 文件传输，允许 Samba 桌面浏览，或允许远程加密连接（如 SSH），你将需要在受信任服务面板中指定它们。Samba 桌面浏览允许你从 GNOME 或 KDE 桌面访问你的 Samba 共享，例如远程 Windows 文件系统。

自定义端口面板允许你指定可能需要为某些服务（如 BitTorrent）打开的端口。点击添加按钮打开一个对话框，你可以在其中输入要控制的协议（tcp 或 udp）的端口号。

## InfiniBand 支持

自 2.6.10 内核起，Fedora 包含 InfiniBand 支持。这是一种新的 I/O 架构，用于取代当前系统中使用的旧总线架构。InfiniBand 通常用作本地网络连接（LAN）的替代方案。它目前已在超级计算机和网络服务器集群中实现。你可以在以下网址找到有关 InfiniBand 的更多信息：

