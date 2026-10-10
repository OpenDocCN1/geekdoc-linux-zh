

- Kali Linux 的安装要求因配置而异：从仅包含基本 SSH 服务器且无桌面的最小配置（仅需 128 MB 内存，建议 512 MB，磁盘空间 2 GB），到高端的 kali-linux-full 元软件包（至少需要 2048 MB 内存和 20 GB 磁盘空间）。此外，您的机器必须拥有至少受 amd64、i386、armel、armhf 或 arm64 架构之一支持的 CPU。
- Kali 可以轻松安装为主操作系统，也可以通过分区和修改引导加载程序与其他操作系统共存，或者作为虚拟机运行。
- 为了保证数据的机密性，您可以设置加密分区。如果笔记本电脑或硬盘丢失或被盗，这将保护您的数据。
- 安装程序还可以通过 debconf 预种子（preseeding）进行自动化，该功能允许您为安装问题提供无人值守的答案。
- 预种子文件是一个纯文本文件，其中每一行包含对一个 Debconf 问题的回答。该行由四个字段组成，字段之间以空白字符（空格或制表符）分隔。您可以通过启动参数、/initrd 中的预种子文件、引导介质上的预种子文件或网络上的预种子文件来预种子安装程序的答案。
- Kali Linux 可运行于多种基于 ARM 的设备，如笔记本电脑、嵌入式计算机和开发者板。ARM 安装相当简单。下载正确的镜像，将其写入 SD 卡、USB 驱动器或嵌入式多媒体控制器（eMMC）模块，插入设备，启动 ARM 设备，在网络上找到该设备，登录，并更改 SSH 密码和 SSH 主机密钥。
- 您可以使用虚拟控制台（通过 CTRL+Shift 和功能键访问）、`debconf-get` 和 `debconf-set` 命令、查看 `/var/log/syslog` 日志文件，或者提交使用安装程序的“保存调试日志”功能获取的日志文件的错误报告来调试失败的安装。

既然我们已经讨论了 Linux 基础知识和 Kali Linux 安装，让我们讨论配置，以便您开始根据需求定制 Kali。

# 关键词

- 网络
- 用户和组
- 服务
- Apache
- PostgreSQL
- SSH

![](img/46e3313ea1bb2892f314630a4f0677b8_128_0.png)

# 第 5 章

配置 Kali Linux

- 配置网络 104
- 管理 Unix 用户和 Unix 组 107
- 配置服务 109
- 管理服务 117
- 摘要 119

在本章中，我们将探讨配置 Kali Linux 的各种方法。首先，在 5.1 节“配置网络” [页码 104] 中，我们将展示如何使用图形环境和命令行来配置网络设置。在 5.2 节“管理 Unix 用户和 Unix 组” [页码 107] 中，我们将讨论用户和组，向您展示如何创建和修改用户账户、设置密码、禁用账户以及管理组。最后，我们将在 5.3 节“配置服务” [页码 109] 中讨论服务，并解释如何设置和维护通用服务，同时重点介绍三个非常重要且特定的服务：SSH、PostgreSQL 和 Apache。

## 5.1. 配置网络

### 5.1.1. 在桌面上使用 *NetworkManager*

在典型的桌面安装中，*NetworkManager* 已经安装，并可通过 GNOME 控制中心以及右上角菜单进行控制和配置，如图 5.1“网络配置界面” [页码 104] 所示。

![](img/46e3313ea1bb2892f314630a4f0677b8_130_0.png)

默认的网络配置依赖于 DHCP 来获取 IP 地址、DNS 服务器和网关，但您可以使用右下角的齿轮图标以多种方式修改配置（例如：设置 MAC 地址、切换到静态配置、启用或禁用 IPv6，以及添加额外路由）。您可以创建配置文件以保存多个有线网络配置，并在它们之间轻松切换。对于无线网络，其设置会自动绑定到其公共标识符（SSID）。

NetworkManager 还处理通过移动宽带（无线广域网 WWAN）和使用以太网点对点协议（PPPoE）调制解调器的连接。最后但同样重要的是，它通过专用插件与许多类型的虚拟私有网络（VPN）集成：SSH、OpenVPN、Cisco's VPN C、PPTP、Strogswan。请查看 `network-manager-*` 软件包；其中大多数未默认安装。请注意，您需要带有 `-gnome` 后缀的软件包才能通过图形用户界面进行配置。

### 5.1.2. 在命令行中使用 ifupdown

或者，当您不想使用（或无法访问）图形桌面时，您可以使用已安装的 `ifupdown` 软件包来配置网络，该包包含 `ifup` 和 `ifdown` 工具。这些工具从 `/etc/network/interfaces` 配置文件中读取定义，是 `/etc/init.d/networking` 初始化脚本的核心，该脚本在启动时配置网络。

`ifupdown` 管理的每个网络设备都可以在任何时候使用 `ifdown network-device` 取消配置。然后您可以修改 `/etc/network/interfaces`，并使用 `ifup network-device` 将网络重新启动（使用新配置）。

让我们看看可以在 ifupdown 的配置文件中放置什么。有两个主要指令：`auto network-device`，它告诉 `ifupdown` 在网络接口可用时自动配置它；以及 `iface network-device inet/inet6 type`，用于配置给定接口。例如，一个普通的 DHCP 配置看起来像这样：

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```

请注意，环回设备的特殊配置始终应该存在于此文件中。对于固定 IP 地址配置，您需要提供更多详细信息，如 IP 地址、网络和网关的 IP：

```
auto eth0
iface eth0 inet static
    address 192.168.0.3
    netmask 255.255.255.0
    broadcast 192.168.0.255
    network 192.168.0.0
    gateway 192.168.0.1
```

对于无线接口，您必须有 **wpa_supplicant** 软件包（Kali 默认包含），它提供许多可用于 `/etc/network/interfaces` 的 *wpa-**- 选项。请查看 `/usr/share/doc/wpa_supplicant/README.Debian.gz` 以获取示例和说明。最常见的选项是 **wpa-ssid**（定义要加入的无线网络名称）和 **wpa-psk**（定义保护网络的密码或密钥）。

```
iface wlan0 inet dhcp
    wpa-ssid MyNetWork
    wpa-psk plaintextsecret
```

### 5.1.3. 在命令行中使用 *systemd-networkd*

虽然 *ifupdown* 是 Debian 历史上使用的工具，并且仍然是服务器或其他最小安装的默认选择，但有一个较新的工具值得考虑：*systemd-networkd*。它与 *systemd* 初始化系统的集成使其成为一个非常有吸引力的选择。它不特定于基于 Debian 的发行版（与 *ifupdown* 相反），并且被设计得非常小巧、高效，并且如果您理解 *systemd* 单元文件的语法，配置起来相对容易。如果您认为 *NetworkManager* 臃肿且难以配置，这是一个特别有吸引力的选择。

通过将 `.network` 文件放入 `/etc/systemd/network/` 目录来配置 *systemd-networkd*。或者，您可以使用 `/lib/systemd/network/` 用于软件包文件，或 `/run/systemd/network/` 用于运行时生成的文件。这些文件的格式在 *systemd-networkd(5)* 中有说明。**Match** 部分指示该配置应用于哪些网络接口。您可以通过多种方式指定接口，包括通过媒体访问控制（MAC）地址或设备类型。**Network** 部分定义网络配置。

> **示例 5.1** */etc/systemd/network/80-dhcp.network 中的基于 DHCP 的配置*

```
[Match]
Name=en*

[Network]
DHCP=yes
```

