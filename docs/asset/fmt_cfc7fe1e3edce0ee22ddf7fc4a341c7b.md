
你可能需要配置某些参数以允许网卡与无线接入点通信。例如，你必须指定分配给接入点的无线网络名称，且加密设置必须与接入点的设置匹配。你通常可以使用 Linux 发行版提供的网络配置工具来配置一切——只需选择“无线网络”（Wireless Network）选项并填写所需信息。

例如，在 Fedora 中，从 GNOME 桌面选择系统；网络（System;Network）。点击工具栏添加网络设备并选择“无线连接”（Wireless connection）（见图 3-2）。然后选择无线设备并进入配置无线连接的窗口。特别是，将模式（Mode）设置为“管理”（Managed），如果有则指定网络名称。你可以将获取 IP 地址的设置为 DHCP（一种用于获取网络配置参数的协议，包括从网络上的服务器获取 IP 地址）。完成后返回网络配置工具的主窗口，选择新的无线设备并点击“激活”（Activate）按钮。如果一切顺利，无线网络在几分钟后就会启动并运行。

![](img/49a40dc66bb14561782e2a1125eaccf3_234_0.png)

图 3-2：选择“无线连接”并点击“前进”按钮。

> 第三卷第三章
> 迈向无线

## 配置无线网络

在 Fedora 中，网络配置工具将你的无线网络设置保存在文本文件中。文本文件名取决于无线网络设备的名称。如果无线网络设备名称为 `eth0`，配置存储在文本文件 `/etc/sysconfig/network-scripts/ifcfg-eth0` 中。如果无线设备名称为 `eth1`，则文件为 `/etc/sysconfig/network-scripts/ifcfg-eth1`。

### 表 3-1：无线以太网接口配置文件设置

| 此参数 | 含义如下 |
| :--- | :--- |
| `BOOTPROTO` | 获取 IP 地址的协议名称。可以是 `dhcp` 或 `bootp`。 |
| `CHANNEL` | 1 到 14 之间的通道号（美国和加拿大）。必须与接入点设置的相同。在管理模式下，你不需要指定通道。 |
| `DEVICE` | 以太网接口的设备名称，第一个为 `eth0`，第二个为 `eth1`，以此此类推。 |
| `ESSID` | 扩展服务集（ESS）标识符，称为无线网络名称。它是区分大小的，且必须与接入点相同。用单引号提供名称（例如 `'HOME'`）。 |
| `HWADDR` | 无线网卡的硬件地址（也称为 MAC 地址）（六对冒号分隔的十六进制数字；例如 `00:02:ca:dc:1`）。无线卡驱动程序会自动检测此项 |
| `IPv6INIT` | 设置为 `yes` 初始化 IPv6。如果不使用 IPv6，请设置为 `no`。 |
| `MODE` | 无线网卡的运行模式。对于通过无线接入点的典型网络设置为 `Managed`。 |
| `NAME` | 无线网络的昵称。如果不指定，则使用主机名作为昵称。 |
| `ONBOOT` | 设置为 `yes` 在启动时激活无线接口；否则设置为 `no`。 |
| `PEERNDNS` | 设置为 `yes` 接口修改系统的 `/etc/resolv.conf` 文件，以从 DHCP 服务器（提供接口 IP 地址的服务器）获取 DNS 服务器。如果将此参数设置为 `no`，则 `/etc/resolv.conf` 文件保持不变。 |
| `RATE` | 连接的比特率（设置为以下之一：`1M`, `2M`, `5M`, `11M` 或 `auto`）。M 表示 Mbps 或每秒比特。设置为 `auto` 以使用最大传输速率。 |
| `TYPE` | 无线以太网接口设置为 `Wireless`。 |
| `USERCTL` | 设置为 `yes`，非 root 用户可以控制设备。设置为 `no` 以便只有 root 用户可以控制设备。 |

如果你手动编辑了无线接口的参数，输入以下命令重新激活接口：

```
/etc/init.d/network restart
```

## 212 配置无线网络

在 SUSE Linux 中，使用 YaST 来配置无线网络。SUSE 将无线配置参数存储在以 `ifcfgwlan` 开头的文件中，后面跟着数字（如 `0` 或 `1`），取决于无线网络接口的顺序。配置文件存储在 `/etc/sysconfig/network` 目录下。以下是 SUSE Linux 配置文件中典型的无线配置参数列表：

```
WIRELESS_MODE='Managed'
WIRELESS_ESSID='HOME'
WIRELESS_NICK=''
WIRELESS_RATE='auto'
WIRELESS_AUTH_MODE='open'
WIRELESS_KEY_0='0123-4567-89'
```

要检查无线网络接口的状态，请输入以下命令：

```
iwconfig
```

以下是带有带有无线以太网 PC 卡的 Fedora 笔记本电脑的典型输出（在其他 Linux 发行版中的输出也应该是类似的）：

```
lo no wireless extensions.
eth0 no wireless extensions.
sit0 no wireless extensions. Nickname:'localhost.localdomain'
eth1 IEEE 802.11 SSID:'HOME'
Mode:Managed Frequency:2.437 GHz Access Point:00:30:AB:06:EZ:SD
Rate:1 Mbps Activity:1/3
Retry limit:4 RTS:throff Fragment:throff
Encryption key:FDF3D-3FDE-FE Security mode:open
Power Management:off
Quality:51/92 Signal level:-40 dBm Noise level:-91 dBm
Rx invalid nid:0 Rx invalid crypt:0 Rx invalid frag:27
Tx excessive retries:0 Invalid misc:0 Missed beacon:
```

在这里，`eth1` 接口指的是无线网卡。我修改了加密密钥和其他参数以隐藏这些细节，示例输出显示了当无线链接正常时你通常会看到的内容。

# 第 4 章：网络管理

## 本章

- 查找 TCP/IP 配置文件
- 检查 TCP/IP 网络
- 在启动时配置网络

与 Linux 中的几乎所有内容一样，TCP/IP 的设置涉及准备许多配置文件（你可以用任何文本编辑器编辑的文本文件）。这些配置文件大多数位于 `/etc` 目录。Linux 安装程序试图通过隐藏 TCP/IP 配置文件的详细细节来提供帮助。尽管如此，如果你知道文件的名称及其用途，凭借专业知识手动编辑这些文件会更容易。

## 发现 TCP/IP 配置文件

在安装 Linux 时，你可以配置 TCP/IP 网络。然而，如果你想有效地管理网络，你就需要熟悉 TCP/IP 配置文件，以便在需要时编辑这些文件。（例如，如果你想检查名称服务器是否正确，你必须了解 `/etc/resolv.conf` 文件，该文件存储了名称服务器的 IP 地址。）

表 4-1 总结了基本的 TCP/IP 配置文件。我将在接下来的章节中描述这些文件。

| 表 4-1 基础 TCP/IP 网络配置文件 | |
| :--- | :--- |
| 此文件 | 包含以下内容 |
| `/etc/hosts` | 本地网络以及你经常访问的任何系统的 IP 地址和主机名 |
| `/etc/networks` | 网络名称和 IP 地址 |
| `/etc/host.conf` | 关于如何将主机名转换为 IP 地址的指令 |
| `/etc/resolv.conf` | 名称服务器的 IP 地址 |
| `/etc/hosts.allow` | 关于哪些系统可以访问你系统上的 Internet 服务指令 |
| `/etc/hosts.deny` | 关于哪些系统必须被拒绝访问你系统上的 Internet 服务指令 |
| `/etc/nsswitch.conf` | 关于如何将主机名转换为 IP 地址的指令 |

文本文件中的井号 (`#`) 表示注释。

### /hosts

`/etc/hosts` 文件包含你本地网络的 IP 地址和主机名列表。在没有名称服务器的情况下，你系统上的任何网络程序都将帮助确定与主机名对应的 IP 地址。将 `/etc/hosts` 想象成本地电话簿，你可以在其中查找本地主机的 IP 地址（而不是电话号码）。

以下来自一个系统的 `/etc/hosts` 文件，显示了典型局域网（LAN）上的 IP 地址和其他主机：

```
127.0.0.1         localhost           localhost.localdomain
# LAN 上的其他主机
192.168.0.100       lnbp933
192.168.0.50        lnbp600
192.168.0.200       lnbp200
192.168.0.233       lnbp233
192.168.0.40              lnbp400
```
