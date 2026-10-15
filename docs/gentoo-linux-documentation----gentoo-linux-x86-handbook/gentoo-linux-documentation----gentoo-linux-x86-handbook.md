
# Gentoo Linux 文档 -- Gentoo Linux x86 手册

Seemann Kullen Gentoo x86 开发者

Tavis Ordway Gentoo Alpha 开发者

Jason Huebel Gentoo AMD64 开发者

Guyy Martin Gentoo HPPA 开发者

Peter van den Abeele Gentoo PPC 开发者

Joe Sellar Gentoo SPARC 开发者

John P. Davis 编写

Pierre-Henri Jondot 编写

Eric Stockridge 编写

Raj Mangoldt 编写

Jungmin Seo 编写

Stoyan Zekov 编写

Jared Hudson 编写

Colin More 编写

Jorge Paulo 编写

Carl Anderson 编写

Jon Portny 编写

Zack Gilbard 编写

Jack Morgan 编写

Benny Chuang 编写

Erwin 编写

Joshua Kismir 编写

Tobias Scherbaum 编写

Xavier Neves 编写

Grant Goodyear 审核者

Gerald A. Normandin Jr. 审核者

Donnie Berkholz 审核者

Ken Nowak 审核者

Lars Weiler 贡献

## 1. 简介

欢迎！

首先，欢迎 Gentoo。

Gentoo 通过 `stage3` 存档运行。本章描述了我们如何提取 `stage3` 存档并配置 `Portage`。

安装并配置 `stage3` 之后，最终就是你拥有了一个可用的 Gentoo 基础系统。本章解释了如何进入下一个阶段。

内核是每个发行版的核心。本章解释了如何配置你的内核。

你将编辑一些重要的配置文件。在本章中，你将获得这些文件的概述以及如何操作的说明。

如前所述，Gentoo 关乎选择。在本章我们将选择并安装一些重要的工具。

`x86` 架构存在多个引导程序。每一个引导程序都有自己的配置方法。我们将逐步介绍根据你的需求配置引导程序的过程。

你快完成了。我们将为你的系统创建一个（或多个）用户。

现在你有了 Gentoo 系统，但接下来是什么？

学习如何使用 Gentoo，包括安装软件、修改变量、更改 `Portage` 行为。

本章解释了维护系统上软件需要知道的“简单”步骤。

一旦你想了解 Gentoo 中的 `Portage`，你就需要知道它将文件和数据存储在何处。

`USE flags` 是 Gentoo 一个非常重要的方面。在本章中，你将学习使用 `USE flags` 并理解 `USE flags` 如何与你的系统相互作用。

本章讨论了 `Portage` 的功能，例如对分布式缓存、`ccache` 等等的支持。

Gentoo 使用通用的脚本格式，其他功能允许依赖驱动的决策和 initscripts。本章解释了所有这些方面以及如何处理它们。

通过 Gentoo，你可以轻松地管理系统的环境变量。本章展示了如何做到这一点，以及使用的变量。

`Portage` 可以通过你可以在配置文件中或作为环境变量设置的各种变量进行完全配置。

Gentoo 提供的软件分为几个分支，取决于稳定性和架构支持。“混合软件分支”会告知你这些分支可以如何配置，以及你如何单独地监督这种状况。

`Portage` 自带了一些额外的工具，让你的 Gentoo 体验变得更好。继续阅读以发现如何使用 `dispatch-config` 和其他工具。

“偏离官方树”为你提供关于如何使用 `Portage` 树、同步类别、注入包等的技巧和秘门。

在“`Ebuild` 应用”中，你将获知 `Portage` 在安装软件时采取的步骤，以及你可以如何执行此操作

关于 Gentoo 网络的全面指南。

基础指南将帮助你获取网络接口并在最常见的环境中运行。

在这里我们学习配置是如何工作的——在学习模块化网络之前你需要了解这些。

Gentoo 提供了灵活的网络——这里将告诉你有关不同的 DHCP 客户端、设置绑定、桥接、VLAN 等。

无线网络并不简单。希望你能成功运行！

如果你觉得很冒险，你可以添加功能

欢迎！

首先，欢迎 Gentoo。

本章描述了我们如何提取 `stage3` 存档并配置 `Portage`。

安装并配置 `stage3` 之后，最终就是你拥有了一个可用的 Gentoo 基础系统。本章解释了如何进入下一个阶段。

内核是每个发行版的核心。本章解释了如何配置你的内核。

你将编辑一些重要的配置文件。在本章中，你将获得这些文件的概述以及如何操作的说明。

如前所述，Gentoo 关乎选择。在本章我们将选择并安装一些重要的工具。

`x86` 架构存在多个引导程序。每一个引导程序都有自己的配置方法。我们将逐步介绍根据你的需求配置引导程序的过程。

你快完成了。我们将为你的系统创建一个（或多个）用户。

现在你有了 Gentoo 系统，但接下来是什么？

学习如何使用 Gentoo，包括安装软件、修改变量、更改 `Portage` 行为。

本章解释了维护系统上软件需要知道的“简单”步骤。

内核是每个发行版的核心。本章解释了如何配置你的内核。

你将编辑一些重要的配置文件。在本章中，你将获得这些文件的概述以及如何操作的说明。

如前所述，Gentoo 是。

### 简介

在开始之前，我们首先列出在您的设备上成功安装 Gentoo 所需硬件要求。

# 硬件要求

| CPU | 要求 |
| :--- | :--- |
| CPU | i486 或更高版本 |
| 内存 | 64 MB |
| 磁盘空间 | 1.5 GB（不包括交换空间） |
| 交换空间 | 至少 256 MB |

### 2.b. Gentoo 安装 CD

### 简介

Gentoo CD 是可启动的光盘，包含一个自包含的 Gentoo 环境。它们允许你从光盘启动 Linux。在启动过程中，系统会检测你的硬件并加载相应的驱动程序。它们由 Gentoo 开发人员维护。

所有安装 CD 都允许你启动、设置网络、初始化分区并从互联网开始安装 Gentoo。我们目前提供两份安装 CD，它们都适用于安装 Gentoo，只要你使用的是可用软件包最新版本进行基于互联网的安装即可。

**重要：** 如果你希望在没有网络连接的情况下安装 Gentoo，或者想使用提供的安装程序之一，请使用 Gentoo 2006.06 手册中规定的安装说明。

我们目前提供的两份安装 CD：

- *最小安装 CD（Minimal Installation CD）是一个小巧、直接的可启动 CD，其目的是启动系统、准备网络并继续进行 Gentoo 安装。*
- *安装程序 LiveCD（Installer LiveCD）包含了安装 Gentoo 所需的所有内容。它提供了图形化和控制台安装程序，可以自动为你执行安装，或者提供适用于你架构的指令。*

为了帮助判断需要哪种 CD，我们列出了每份安装 CD 的主要优缺点。

### Gentoo 的最小安装 CD

最小安装版名为 `i386-minimal.2006.0.iso`，占用 49 MB 磁盘空间。你可以使用此安装 CD 安装 Gentoo，但必须始终保持网络连接可用。

| 最小安装 CD | 优缺点 |
| :--- | :--- |
| | 下载量最小 |
| | 不包含 `stage3ball`、不包含 `Portage` 快照、没有预构建的软件包，因此不适用于无线安装 |

### Gentoo 的安装程序 LiveCD

Live CD 名为 `livecd-i686-2006.0.2.iso`，占用 97 MB。你可以使用此安装 CD 安装 Gentoo，并且可以在没有网络连接的情况下进行安装，以防你想要将 Gentoo 安装到除当前安装机器之外的另一台 PC 上：

#### 安装程序 LiveCD 优缺点

- *包含你所需的所有内容。你可以在没有网络连接的情况下使用。*（优点）
- 下载量巨大（缺点）

### Stage3 Tarball

`stage3ball` 是一个包含最小 Gentoo 环境的归包，适用于按照主手册中的指令继续进行 Gentoo 安装。此前，Gentoo 手册描述了使用三个阶段之一进行安装。虽然 Gentoo 仍然在使用 `stage1` 和 `stage2` 阶段，但官方安装程序使用的是 `stage3ball`。如果你感兴趣使用 `stage1` 或 `stage2` 进行 Gentoo 安装，请阅读 Gentoo FAQ 中的“我如何使用 `stage1` 或 `stage2` Tarball 安装 Gentoo？”

`Stage3` charballs 可以从 `releases/x86/2006.0/stages/` 或其中一个官方 Gentoo 镜像下载，且 LiveCD 上不提供。

### 2.c. 下载、刻录和启动 Gentoo 安装

### 下载和刻录安装 CD

你选择了使用 Gentoo CD。我们首先将下载并刻录所选的安装 CD。我们之前讨论过多种安装 CD，但可以在哪里找到它们？



如果你愿意，可以下载任何一个安装 CD，或者从某个镜像站下载软件包 CD（Packages CD）。安装 CD 位于 `releases/x86/2006/installed`。

在这些目录下，你会找到 ISO 文件。这些是你可以写入 CD-R 光盘的小型镜像。

如果你怀疑下载的文件已损坏，可以检查其 MD5 校验和，并与我们提供的 MD5 校验和（例如 `install-x86-minimal-2006.0.iso`）进行对比。你可以使用 Linux/Unix 下的 `md5sum` 工具或 Windows 下的 `md5sum` 来检查 MD5 校验和。

另一种检查下载文件有效性的方法是使用 GnuPG 验证你找到的加密签名（以 `.asc` 结尾的文件）。下载签名文件并获取公钥：

### 代码列表 1：获取公钥

```
$ gpg --keyserver subkeys.pgp.net --recv-keys 170720578
```

现在验证签名：

### 代码列表 2：验证加密签名

```
$ gpg --verify <signature file> <downloaded iso>
```

刻录下载的 ISO 时，必须选择“原始刻录”（raw-burning）。这高度取决于硬件。我们将讨论 Discrecord 和 K3B；更多信息你可以在 Gentoo FAQ 中找到。

- 使用 Discrecord，选择 Select Tools > CD Burn。然后你可以在 'Image to Burn' 中找到你的 ISO 文件。最后点击开始刻。

- 使用 K3B，选择 Tools > CD Burn。

### 启动安装 CD

> **重要：** 在继续之前请阅读本节，你可能在稍后的操作中没有机会阅读它了。

一旦你刻好了 CD，现在将安装盘放入 CD-ROM 驱动器（就绪）并重启。你应该看到一个提示。在此屏幕上，你可以按回车以默认选项开始启动过程，或者通过指定内核后跟启动选项并按回车以自定义启动选项启动安装。

选择内核？我们在安装 CD 上提供了多个内核。默认的是 Gentoo。以下是内核列表：

| 内核 | 描述 |
| :--- | :--- |
| default | 默认内核 |
| acpi-on | 支持 ACPI |
| video | 带帧缓冲区 |
| lvm2 | 用于 LVM |
| cdrom | 支持 cdrom |
| hotplug | 支持热插拔 |

激活 DMA：`# hdparam -d 1 /dev/hda`

安全性能选项：`# hdparam -d 1 -A -1 -m 16 -u 1 -a 64 /dev/hda`

### 可选：用户账户

如果你计划让其他人访问您的安装环境，或者您想在没有 root 权限的情况下使用 Gentoo（出于安全考虑），您需要创建必要的用户账户并更改 root 密码。

要更改 root 密码，请使用密码工具：

### 代码列表 9：更改 root 密码

```
# password
新密码：（输入您的新密码）
再次输入密码：（再次输入密码）
```

要创建用户账户，我们首先输入其凭据，然后是密码。我们使用 `useradd` 和 `passwd` 完成这些任务。接下来，我们将创建一个名为 "john" 的用户。

### 代码列表 10：创建用户账户

```
### useradd -m -G users john
### passwd john
新密码：（输入 john 的密码）
再次输入密码：（再次输入 john 的密码）
```

您可以使用 `su` 将身份从 root 切换到新创建的用户：

### 代码列表 11：切换用户 ID

```
### su - john
```

### 可选：安装时查看文档

如果您想在安装期间查看 Gentoo Handbook（从 CD 或在线查看），请确保您已创建了用户账户（可选：用户账户）。然后按 Alt-F2 进入新终端并登录。

如果您想查看 CD 上的文档，可以立即运行指向它的链接：

### 代码列表 12：查看 CD 上的文档

```
### links /mnt/cdrom/docs/html/index.html
```

然而，最好是使用 Gentoo Handbook，因为它会比 CD 提供的版本更新。您可以使用 `links` 查看它，但仅是在配置完“配置网络”章节之后（否则您将无法访问互联网查看文档）：

### 代码列表 13：查看在线文档

```
### links http://www.gentoo.org/doc/en/handbook/handbook-x86.html
```

您可以通过按 Alt-F1 回到原始终端。

### 可选：启动 SSH 守护进程

如果您想在 Gentoo 安装期间允许其他用户访问您的计算机（可能因为那些用户正在帮助安装 Gentoo，即使您也是），您需要为他们创建一个用户账户，并可能为他们提供 root 密码（仅在您完全信任该用户时这样做）。

要启动 SSH 守护进程，执行以下命令：

### 代码列表 14：SSH 守护进程

```
### /etc/init.d/sshd start
```

为了能够使用 `sshd`，您首先需要设置网络。请继续“配置网络”章节。

# 3. 配置网络

## 3.a. 自动网络检测

也许直接就能用？

如果您的系统连接到带有 DHCP 服务器的以太网，很有可能您的网络配置已经自动为您设置好了。如果是这样，您应该能够利用安装 CD 中包含的许多网络感知命令，如 `sh`、`scp`、`ping`、`ifconfig` 和 `links` 等。

如果已经为您配置了网络，`/sbin/ifconfig` 命令应该列出网络接口，如 lo 以及 eth0：

### 代码列表 15：用于检查网络的 /sbin/ifconfig

```
# /sbin/ifconfig
eth0
    link:Ethernet  HAddr:00:50:BA:BF:61:7A
    inet addr:192.168.0.2  Broadcast:192.168.0.255  Mask:255.255.255.255
    inet6 fe80::2050:baff:fe67/64 MTU:1500 Metric:1
    UP BROADCAST DYNAMIC MULTICAST
    RX packets:1489792 errors:0 overruns:0 frame:0
    TX packets:1248980 errors:0 overruns:0 carrier:0
    collision:0 RX bytes:86592125 (82.6 Mb) TX bytes:123951388 (118.2 Mb)
    Interrupt:1 Base address:0xe80
```

### 可选：配置代理

如果您通过代理访问互联网，您可能需要在安装期间设置代理信息。定义代理非常简单：您只需要定义代理服务器的信息。

在许多情况下，您可以使用主机名来定义变量。例如，如果您的代理是 `proxy.gentoo.org` 且端口是 `8080`。

### 代码列表 2：定义代理服务器

```
（如果代理过滤 HTTP 流量）
# export http_proxy=proxy.gentoo.org:8080
（如果代理过滤 HTTPS 流量）
# export https_proxy=proxy.gentoo.org:8080
（如果代理过滤 RSYNC 流量）
# export RSYNC_PROXY=proxy.gentoo.org
```

如果您需要用户名和密码，应该使用以下变量语法：

### 代码列表 3：在变量中添加用户名/密码

```
http://username:password@proxy.::
```

### 测试网络

您可以尝试 ping 您的 ISP 的 DNS（在 `/etc/resolv.conf` 中找到）或任一网站，以确保您的数据包已到达网络、DNS 解析正常等。

### 代码列表 4：进一步测试

```
# ping -c 3 yahoo.com
```

如果您现在可以使用网络，可以跳过本节其余部分继续操作磁盘。如果不是，请继续阅读。

## 3.b. 自动网络配置

如果网络没有立即工作，某些安装介允许使用 `net-setup`（用于普通或无线网络）、`adsl-setup`（用于 ADSL）或 `pptp`（用于 PPTP 仅适用于 x86）。如果安装介未包含任何工具或网络尚未运行，请继续手动配置。

- 普通以太网用户应继续使用：`net-setup`
- ADSL 用户应继续使用：PoE
- PPTP 用户应继续使用：PPTP

如果没有自动配置网络，最简单的方法是运行 `net-setup` 脚本：

### 代码列表 5：运行 net-setup

```
# net-setup eth0
```



`net-setup` 会向您询问一些关于环境的问题。完成后，您应该有一个工作的连接。按照说明测试您的连接。如果测试成功，恭喜！您现在可以安装 Gentoo 了。跳过本节其余部分继续操作磁盘。如果您的网络不起工作，请继续手动配置。

假设您需要连接互联网，安装 CD（任何版本）已通过 PoE 让事情变得简单。使用提供的 `adsl-setup` 配置您的网络。系统会提示您连接到 ADSL 调制器的以太网设备、用户名和密码、DNS 服务器的 IP 以及您是否需要基础防火墙。

## 代码列表 6：使用 PoE

```
# adsl-setup
# adsl-start
```

如果出现问题，请通过 `/etc/ppp/pap-secrets` 或 `/etc/ppp/chap-secrets` 检查用户名和密码输入是否正确。确保使用了正确的以太网设备。如果以太网设备不存在，将必须加载正确的网络模块。在这种情况下，请继续手动配置，我们将说明如何加载正确的网络模块。如果一切正常，继续操作磁盘。

> 注意：PPTP 支持仅适用于 x86

如果您需要 PPTP，可以使用安装 CD 提供的 `pppclient`。但首先您需要确保您的配置是正确的。编辑 `/etc/ppp/pap-secrets` 或 `/etc/ppp/chap-secrets` 以包含正确的用户名/密码组合：

### 代码列表 7：编辑 /etc/ppp/chap-secrets

```
# nano -w /etc/ppp/chap-secrets
```

然后根据需要调整 `/etc/ppp/options.ppt`：

### 代码列表 8：编辑 /etc/ppp/options.ppt

```
# nano -w /etc/ppp/options.ppt
```

完成后，运行 `pptp`（带有 `options.ppt` 中设置的选项）连接到服务器：

### 代码列表 9：连接到拨号服务器

```
# pptp <server ip>
```

## 3.c. 手动配置网络

### 加载正确的网络模块

当安装 CD 启动时，它尝试检测您所有的硬件设备并加载相应的内核模块（驱动程序）来支持您的硬件。在大多数情况下，它工作得很好。但在某些情况下，它可能不会自动加载您所需的内核模块。

如果 `net-setup` 或 `add-setup` 失败，可能是网卡没有被立即发现。这意味着您可能需要手动加载正确的内核模块。

要确定哪些内核模块提供网络功能，请使用 `ls`：

#### 代码列表 10：搜索提供的模块

```
# ls /lib/modules/$(uname -r)/kernel/drivers/net
```

如果您找到了网卡的驱动程序，使用 `modprobe` 加载内核模块：

#### 代码列表 11：使用 modprobe 加载内核模块

（作为一个示例，我们加载 `pcnet32` 模块）

```
# modprobe pcnet32
```

要检查网卡是否被检测，请使用 `ifconfig`。检测到的网卡结果如下：

#### 代码列表 12：网卡可用性测试，成功

```
# ifconfig eth0
link encap:Ethernet Hardware:00:00:00:00:00:00
BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:0 dropped:0 overruns:0 frame:0
TX packets:0 dropped:0 overruns:0 carrier:0
collisions:0 queue:0
RX bytes:0 (0.0 b) TX bytes:0 (0.0 b)
```

如果您收到错误则网卡未被检测：

#### 代码列表 13：网卡可用性测试，失败

```
# ifconfig eth0
eth0: error fetching interface information: Device not found
```

如果您的系统中有多个网卡，它们被命名为 `eth0`、`eth1` 等。请确保您想要使用的网卡运行良好，并在整个文档中使用正确的名称。我们假设使用的是网卡 `eth0`。

#### 代码列表 14: 使用 dhcp

```
# dhcp
某些网络管理员要求你使用由 DHCP 服务器提供的
主机名和域名。
在这种情况下，请使用
# dhcp -HD eth0
```

如果这有效（例如 `ping` 通某个服务器，如 Google），那么你已经准备就绪，可以继续下去了。跳过本节的其余部分，继续“准备磁盘”。

### 准备无线访问

> 注意：`ifconfig` 的支持仅适用于 x86 和 PPC 安装光盘。你仍然可以通过遵循 linux-wlan-ng 项目的说明来使扩展功能工作。

如果你正在使用 (802.11) 网卡，在进一步操作之前可能需要配置无线设置。要查看网卡上的当前设置，可以使用 `iwconfig`。`iwconfig` 可能会显示如下内容：

#### 代码列表 15: 配置无线设置

```
# iwconfig eth0
IEEE 802.11-DS SSID:GentooNode
eth0  Managed Frequency:24.222GHz Access Point:00:09:SB:11:CC:F2
BitRate:1M Power:20dBm Sensitivity:0/65535
Retries:16 Fragment:off Power:Management:off
Link Quality:0/70 Signal level:-51 dbm Noise level:-102 dbm
Rx wv invalid:0 Tx wv invalid:0 Tx
excessive retries:27 Invalid miss:350282 Missed beacon:84
```

> 注意：某些无线网卡的设备名称可能是 `wlan0` 而不是 `eth0`。运行不带命令行参数的 `iwconfig` 来确定设备名称。

对于大多数用户来说，只有两个设置可能需要更改：ESSID（网络名称）或 WEP 密钥。如果你需要更改 SSID 或添加 WEP 密钥，可以使用以下命令：

#### 代码列表 16: 更改 ESSID 并添加 WEP 密钥

```
# 这将网络名称设置为 "GentooNode"
# iwconfig eth0 SSID GentooNode

# 这设置 WEP 密钥
# iwconfig eth0 key 12345678901234567abcd

# 这设置一个 ASCII 密钥 - 前缀加上 "s:*"
# iwconfig eth0 key s:some-password
```

然后你可以通过 `iwconfig` 确认你的无线设置。如果你有无线网络，可以继续在下一节（理解网络术语）中配置网络选项，或按之前描述的方法使用 net-tool。

### 理解网络术语

> 注意：如果你知道自己的 IP 地址、广播地址、子网掩码和 DNS 服务器，可以跳过本节并继续使用 `ifconfig` 和 `route`。

如果上述所有方法都失败，你将必须手动配置网络。这并不困难。然而，你需要熟悉网络术语，这样就能按照你的意愿配置网络。阅读后，你将知道什么是网关、什么是服务器、什么是广播地址，以及你为什么需要 DNS 服务器。

在网络中，主机通过其 IP 地址（互联网协议地址）进行标识。这种地址是 0 到 255 之间四个数字的组合。嗯，至少我们是这样理解的。实际上，这样的 IP 地址由 32 位（0 和 1）组成。让我们来看一个一个示例：

#### 代码列表 17: IP 地址示例

| IP 地址 (数字): | 192.168.0.2 | 11000000 10101000 00000010 |

| IP 地址 (位): | 192 | 168 | 2 |

对于所有关联网络而言，这样的 IP 地址对主机来说是唯一的（即每个可以到达的主机都必须有唯一的 IP 地址）。为了区分网络内部和外部的主机，IP 地址分为两部分：网络部分和主机部分。

这种分离是通过子网掩码进行的，一部分是网络部分，另一个是主机部分。通常，子网掩码可以写成 IP 地址。

#### 代码列表 18: 网络/主机分离示例

| IP 地址: | 192.168.0.2 | 11000000 10101000 00000010 |

| 子网掩码: | 255.255.255.0 | 11111111 11111111 11111111 0 |

| 网络 主机: | | |



换句话说，`192.168.0.1`是我们网络的一部分，`192.168.1.2`不是。广播是一个与我们的网络相同网络部分，但只有一个主机部分的 IP 地址。网络上的每个主机都监听这个 IP 地址。这是为了广播数据包。为了能够上网，必须知道哪个主机是网关。由于它是普通主机，它有一个 IP 地址（例如`192.168.0.1`）。我们之前提到过每个主机都有自己的 IP 地址。为了通过名称（而不是 IP 地址）访问此主机，你需要一个将名称（如`google.org`）转换为 IP 地址（如`/etc/resolv.conf`）的服务。这种服务被称为 DNS。要使用这种服务，必须在`/etc/resolv.conf`中定义服务器。在某些情况下，你也可以使用 ISP 提供的服务器。总结，在继续之前你需要以下信息：

| 网络 | 示例 |
| :--- | :--- |
| 你的 IP 地址 | `192.168.0.2` |
| 子网掩码 | `255.255.255.0` |
| 广播地址 | `192.168.0.255` |
| 网关 | `192.168.0.1` |
| DNS 服务器 | `8.8.8.8` |

### 使用 ifconfig

设置网络由三个步骤组成。首先使用 `ifconfig` 分配 IP 地址。然后设置路由到网关。最后，你需要通过在`/etc/resolv.conf`中放置服务器来完成。

要分配 IP 地址，请考虑你的 IP 地址、广播地址子网掩码。然后执行命令，将`IP_ADDR`替换为你的 IP 地址，将`BROADCAST`替换为广播地址，将`NETMASK`替换为子网掩码：

# 代码列表 20: 使用 ifconfig

```
# ifconfig eth0 $(IP_ADDR) broadcast $(BROADCAST) netmask $(NETMASK) up
```

现在使用 `route` 设置路由。将`GATEWAY`替换为你的网关 IP 地址：

```
# 代码列表 21: 使用 route
# route add default gw $(GATEWAY)
```

现在用喜欢的编辑器打开`/etc/resolv.conf`（例如我们使用`nano`）：

```
# 代码列表 22: 创建 /etc/resolv.conf
# nano -w /etc/resolv.conf
```

现在使用以下模板填写你的服务器。确保将`NAMESERVER1`和`NAMESERVER2`替换为相应的地址：

```
代码列表 23: /etc/resolv.conf 模板
nameserver ${NAMESERVER1}
nameserver ${NAMESERVER2}
```

这不是通过选择某些互联网服务器（如 Google）来联网。如果这有效，恭喜你。你现在准备好安装 Gentoo 了。继续“准备磁盘”。

# 4. 准备磁盘

## 4.a. 块设备介绍

### 块设备

我们将查看 Gentoo 以及通用 Linux 的磁盘分区，包括 Linux 系统、分区和块设备。一旦你熟悉了磁盘和文件系统的内部，我们将引导你完成为 Gentoo Linux 安装分区和文件系统的过程。

首先，我们将介绍设备。最基本的块设备可能是 Linux 系统中代表第一个驱动器的设备`/dev/sda`。如果你的系统使用 SCSI 或 SATA 设备，那么你的第一硬盘将是`/dev/sd`。

块设备代表了磁盘的抽象接口。你的程序可以使用这些块设备与磁盘交互，而无需担心你的驱动器是 IDE、SCSI 还是其他。程序可以将磁盘上的存储管理为一组连续的、随机的 512 字节块。

### 分区

虽然理论上可以使用整个磁盘来存放你的 Linux，但在实践中几乎从未这样做。相反，整个块设备被拆分成更小、更容易管理的块设备。在 x86 系统上，这些被称为分区。

分区分为三种：主分区、扩展分区和逻辑分区。

主分区是存储在 MBR（主引导记录）中的分区。由于 MBR 非常小（512 字节），因此只能定义四个主分区（例如`/dev/sda1`到`/dev/sda4`）。

扩展分区是一个特殊的主分区（这意味着扩展分区必须是四个主分区之一）。不能再定义更多分区了。但如果其中一个是第四个，它被赋予了生命，以在不丢失后兼容性的情况下扩展格式方案。

逻辑分区位于扩展分区内部。这些定义没有放在 MBR 中，而是声明在扩展分区内部。

## 4.b. 设计分区方案

### 默认分区方案

如果你对为你的系统绘制分区方案不感兴趣，可以使用我们在书中一直使用的分区方案：

| 文件系统 | 大小 | 已用 | 描述 |
| :--- | :--- | :--- | :--- |
| `/dev/hd1` ext2 | 32M | 启动分区 |
| `/dev/hd2` (swap) | 512M | 交换分区 |
| `/dev/hd3` ext3 | | 磁盘的剩余分区 |

如果你想知道分区应该有多大，或者你需要多少个分区，请继续阅读。使用 `fdisk` 对你的磁盘进行分区来继续分区操作。

### 多少个？多大？

分区的数量很大程度上取决于你的环境。例如，如果你有很多用户，你可能最希望将`/home`独立出来，因为这确保了安全并便于备份。如果你正在安装 Gentoo 作为邮件服务器，那么你的`/var`应该是独立的，因为其所有的小型存储目录都在`/var`内部。选择良好的文件系统将最大化你的性能。服务器将有一个独立的`/opt`，大多数包管理器也会更容易运行。你绝对想要保留`/usr`：它不仅会限制应用程序的容量，而且除了存储其中的各种源码外，Portage 树大约占用 500 MB。

正如你所见，这取决于你的用途。为每个分区或卷设置独立分区具有以下优势：

- 你可以为每个分区或卷选择性能最好的文件系统
- 如果一个失效的分区继续向分区或卷写入文件，你的整个系统不会耗尽可用空间
- 如果需要，可以减少文件系统检查次数，因为可以并行进行多次检查（尽管这种优势在多个磁盘上比在多个分区上更明显）
- 通过将某些分区挂载为只读（忽略 `setuid` 位）、`noexec`（忽略可执行二进制文件）等，可以增强安全性。

多个分区也有一个缺点：如果配置不当，可能会导致系统在某个分区上有很多空空间，而在另一个分区上没有。SCSI 和 SATA 还有 15 个分区的限制。

作为一个示例，我们向你展示了一个 20GB 磁盘的分区情况，作为一个演示笔记本（包含 Web 服务器、邮件服务器、gnome）：

```
Code Line 1: Filesystem example usage
$ fdisk -l
Filesystem Type Size Used Avail% Mounted on
/dev/hd5 ext4 50M 132M 28%
/dev/hd6 ext3 5G 3.2G 65% /home
/dev/hd7 ext3 7.9G 6.2G 13% /usr
/dev/hd8 ext3 101M 48M 47% /opt
/dev/hd9 ext2 2G 607M 35% /var
/dev/hd1 ext2 1M 17M 36% /root
/dev/hd4 swap 512M 504M <not mounted>
(Partitioned for future usages: )
```

`/usr`是根目录（此处已使用 85%），但所有软件都安装在此处，`/usr`往往不会增长太多。为`/var`分配几 GB 的磁盘空间似乎过多了，请记住 Portage 使用此分区来编译包。如果你想让`/var`保持较小，你需要修改`/etc/make.conf`中的`PORTAGE_TMPDIR`变量，使其指向有足够剩余空间来编译如 OpenOffice 等大型包的分区。

## 4.c. 使用 fdisk 对磁盘进行分区

以下部分解释了如何创建之前描述的分区布局：

### 分区描述

`/dev/hd1` 启动分区

`/dev/hd2` 交换分区

`/dev/hd3` 根分区

根据你的喜好更改布局。

### 查看当前分区布局

`fdisk`是一个将磁盘划分为区的流行且强大的工具。在你的磁盘上使用`fdisk`（在我们的示例中，我们使用`/dev/hda`）：

# Code List 2: 启动 fdisk

```
# fdisk /dev/hda own
```

一旦进入`fdisk`，你将看到类似所示的提示符：

# Code List 3: fdisk prompt

```
Command (m for help):
```

输入 `p` 显示磁盘当前的分区配置：

# Code List 4: 示例分区配置

```
Command (m for help): p

Disk /dev/hda 240 heads, 63 sectors, 2184 cylinders
Units = cylinders of 15120 * 512 bytes
```

| Device Boot | Start | Blocks | System |
| :--- | :--- | :--- | :--- |
| `/dev/hda1` | 1 | 105008+ | Linux |



| `/dev/hda2` | 15 | 224060+ | swap |
| `/dev/hda3` | 50 | 158760 | Linux |
| `/dev/hda4` | 71 | 219810+ | Extended |
| `/dev/hda5` | 209 | 205080+ | Linux Linux |
| `/dev/hda6` | 210 | 348080+ | Linux |
| `/dev/hda7` | 349 | 626048+ | Linux |
| `/dev/hda8` | 627 | 904048+ | Linux |
| `/dev/hda9` | 905 | 2184+ | Linux |

此磁盘配置为用于存放文件系统（每个分区列为 "Linux"）以及一个列为 "swap" 的交换分区。

### 删除分区

我们首先将从磁盘中删除所有分区。输入 `d` 删除一个分区。例如，删除 `/dev/hda1`：

#### Code List 5: 删除分区

```
Command (m for help): d
Partition (1-4): 1
```

该分区已安排待删除。如果你输入 `p`，它将不再显示，但除非你保存了更改，否则它不会被擦除。如果你犯了错误并想取消，按回车键，你的更改将不会删除。现在，你想擦除磁盘上所有的分区，重复输入 `p` 来打印分区，然后输入 `d` 和分区编号来删除它。最终，你将得到一个没有任何分区表：

#### Code List 6: 空分区表

```
Disk /dev/hda 30.0 GB, 300058214
240 heads, 63 sectors, 2184 cylinders
Units = cylinders of 15120 * 512 bytes
```

现在，分区表是空的，你可以按照之前的说明创建分区。

#### Code List 7: 创建分区分区

```
Disk /dev/hda 30.0 GB, 300058214
240 heads, 63 sectors, 2184 cylinders
Units = cylinders of 15120 * 512 bytes
```

### 保存分区布局

要保存分区布局并退出 `fdisk`，输入 `w`。

#### 代码列表 11: 保存并退出 fdisk

```
命令 (m 帮助): w
```

现在分区已经创建，你现在可以继续“创建文件系统”。

# 4.d. 创建文件系统

### 简介

现在分区已经创建，是时候在它们上创建文件系统了。如果你不在乎选择哪种文件系统，并且对我们在本手册中使用的感到满意，请继续“将文件系统应用到分区”。否则请继续阅读以了解可用的文件系统……

### 文件系统？

Linux 内核支持多种文件系统。我们将解释 `ext2`、`ReiserFS`、`XFS` 和 `JFS`，因为它们是 Linux 系统上最常用的文件系统。

`ext2` 是唯一且真正的具有元数据日志（metadata journaling）的 Linux 文件系统，这意味着启动时的 `ext2` 检查可能非常耗时。现在有了许多新一代的日志文件系统，可以快速检查一致性，并且被认为远优于其非日志对应项。日志文件系统可以防止系统在意外崩溃处于不一致状态时出现长时间延迟。

`ext3` 是 `ext2` 的日志版本，除了全日志和数据日志等增强模式外，它还提供了元数据日志以实现快速恢复。`ext3` 是一个非常优秀且可靠的文件系统。它具有一个额外的哈希 b 树索引选项，能够在不产生任何减速的情况下实现快速文件访问。简而言之，`ext3` 是一个卓越的文件系统。

`ReiserFS` 是一种 B+-树文件系统，具有非常好的整体性能。在处理小文件（小于 4kb 的文件）时，其性能远超 `ext2` 和 `ext3`，提升可达 10 倍以上。`ReiserFS` 也非常稳健，可以作为通用文件系统，也可以用于极端情况，如创建大型文件系统、使用大量小文件以及包含数千个文件的大文件和目录。在内核 `2.4.18+` 中……

`XFS` 是一种具有元数据日志的文件系统，带有功能强大的特性集，并针对可扩展性进行了优化。我们建议在具有高速 SCSI 和/或光纤通道以及不间断电源的 Linux 系统上使用它。因为 `XFS` 会激进地在 RAM 中缓存数据，向磁盘写入文件时不要采取预防措施，如果系统意外宕机，那（几个）可能会丢失大量数据。

`JFS` 是 IBM 的高性能日志文件系统。它最近已达到生产就绪，但目前还没有足够的记录来对其通用稳定性给出肯定的或否定的评价。

### 将文件系统应用到分区

若要在分区或卷上创建文件系统，对于每种可能的文件系统都有相应的工具：

| 文件系统 | 命令 |
| :--- | :--- |
| ext2 | `mke2fs` |
| ext3 | `mke2fs -j` |
| reiserfs | `mkeiserfs` |
| xfs | `mkmfs.xfs` |
| jfs | `mke2fs.jfs` |

例如，为了让启动分区（示例中为 `/dev/hd1`）使用 `ext2`，根分区（示例中为 `/dev/hd3`）使用 `ext3`（如示例所示你会使用：

#### 代码列表 12: 在分区上应用文件系统

```
# mke2fs /dev/hda1
# mke2fs -j /dev/hda3
```

在新创建的分区上创建文件系统。

### 激活交换分区

`mkswap` 是初始化交换分区的命令：

#### 代码列表 13: 创建交换签名

```
# mkswap /dev/hda2
```

要激活交换分区，请使用 `swapon`：

#### 代码列表 14: 激活交换分区

```
# swapon /dev/hda2
```

使用上述命令创建并激活交换空间。

### 4.e. 挂载

现在分区已经初始化并存放了文件系统，是时候挂载你的分区了。使用 `mount` 命令。别忘记为你创建的每个分区创建必要的挂载目录。作为示例，我们将使用根分区和启动分区：

#### 代码列表 15: 挂载分区

```
# mount /dev/hda3 /mnt/gentoo
# mkdir /mnt/gentoo/boot
# mount /dev/sda1 /mnt/gentoo/boot
```

> 注意：如果你需要 `/tmp` 位于独立分区上，务必在挂载后更改其权限：`chmod 1777 /mnt/gentoo/tmp`。这对 `/var/tmp` 也同样适用。

我们必须将 proc 文件系统（与内核的虚拟接口）挂载到 `/proc` 上。但首先，我们需要将文件放在分区上。

继续“安装 Gentoo 安装文件”。

# 5. 安装 Gentoo 安装文件

### 5.a. 安装 Stage Tarball

### 设置正确的日期/时间

在需要之前要检查并更新你的日期/时间。配置错误的时钟可能会在未来导致奇怪的结果！

要验证当前日期时间，运行 `date`：

#### 代码列表 1: 验证日期时间

```
# date
Fri Mar 29 16:21:18 CEST 2005
```

如果显示的日期错误，使用 `date MMDDhhmmYYYY` 语法（月、日、时、分和年）更新。例如，将日期设置为2005 年 3 月 29 日 16:21：

#### 代码列表 2: 设置日期时间

```
date 032916212005
```

### 你的选择

下一步需要的操作是将我们的文件放置到分区上。

继续“安装 Gentoo 安装文件”。

### 5.b. 默认：使用 Internet 上的 Stage

### 下载 Tarball

现在分区已经初始化并存放了文件系统，是时候挂载你的分区了。使用 `mount` 命令。别忘记为你创建的每个分区创建必要的挂载目录。作为示例，我们将使用根分区和启动分区：

#### 代码列表 15: 挂载分区

```
# mount /dev/hda3 /mnt/gentoo
# mkdir /mnt/gentoo/boot
# mount /dev/sda1 /mnt/gentoo/boot
```

> 注意：如果你需要 `/tmp` 位于独立分区上，务必在挂载后更改其权限：`chmod 1777 /mnt/gentoo/tmp`。这对 `/var/tmp` 也同样适用。

我们必须将 proc 文件系统（与内核的虚拟接口）挂载到 `/proc` 上。但首先，我们需要将文件放在分区上。

继续“安装 Gentoo 安装文件”。

# 5. 安装 Gentoo 安装文件

### 5.a. 安装 Stage Tarball

### 设置正确的日期/时间

在需要之前要检查并更新你的日期/时间。配置错误的时钟可能会在未来导致奇怪的结果！

要验证当前日期时间，运行 `date`：

#### 代码列表 1: 验证日期时间

```
# date
Fri Mar 29 16:21:18 CEST 2005
```

如果显示的日期错误，使用 `date MMDDhhmmYYYY` 语法（月、日、时、分和年）更新。例如，将日期设置为2005 年 3 月 29 日 16:21：

#### 代码列表 2: 设置日期时间

```
date 032916212005
```



### 你的选择

下一步需要的操作是将我们的文件放置到分区上。

继续“安装 Gentoo 安装文件”。

### 5.b. 默认：使用 Internet 上的 Stage

### 下载 Tarball

现在分区已经初始化并存放了文件系统，是时候挂载你的分区了。使用 `mount` 命令。别忘记为你创建的每个分区创建必要的挂载目录。作为示例，我们将使用根分区和启动分区：

```
# mount /dev/hda3 /mnt/gentoo
# mkdir /mnt/gentoo/boot
# mount /dev/sda1 /mnt/gentoo/boot
```

> 注意：如果你需要 `/tmp` 位于独立分区上，务必在挂载后更改其权限：`chmod 1777 /mnt/gentoo/tmp`。这对 `/var/tmp` 也同样适用。

我们必须将 proc 文件系统（与内核的虚拟接口）挂载到 `/proc` 上。但首先，我们需要将文件放在分区上。

继续“安装 Gentoo 安装文件”。

# 5. 安装 Gentoo 安装文件

### 5.a. 安装 Stage Tarball

### 设置正确的日期/时间

在需要之前要检查并更新你的日期/时间。配置错误的时钟可能会在未来导致奇怪的结果！

要验证当前日期时间，运行 `date`：

```
# date
```

Fri Mar 29 16:21:18 CEST 2005

如果显示的日期错误，使用 `date MMDDhhmmYYYY` 语法（月、日、时、分和年）更新。例如，将日期设置为2005 年 3 月 29 日 16:21：

```
date 032916212005
```

### 你的选择

下一步需要的操作是将我们的文件放置到分区上。

继续“安装 Gentoo 安装文件”。

### 5.b. 默认：使用 Internet 上的 Stage

### 下载 Tarball

现在分区已经初始化并存放了文件系统，是时候挂载你的分区了。使用 `mount` 命令。别忘记为你创建的每个分区创建必要的挂载目录。作为示例，我们将使用根分区和启动分区：

```
# mount /dev/hda3 /mnt/gentoo
# mkdir /mnt/gentoo/boot
# mount /dev/sda1 /mnt/gentoo/boot
```

> 注意：如果你需要 `/tmp` 位于独立分区上，务必在挂载后更改其权限：`chmod 1777 /mnt/gentoo/tmp`。这对 `/var/tmp` 也同样适用。

我们必须将 proc 文件系统（与内核的虚拟接口）挂载到 `/proc` 上。但首先，我们需要将文件放在分区上。

继续“安装 Gentoo 安装文件”。



> 注意：如果你需要 `/tmp` 位于独立分区上，务必在挂载后更改其权限：`chmod 1777 /mnt/gentoo/tmp`。这对 `/var/tmp` 也同样适用。

我们必须将 proc 文件系统（与内核的虚拟接口）挂载到 `/proc` 上。但首先，我们需要将文件放在分区上。

继续“安装 Gentoo 安装文件”。

# 代码列表 12：前往 Gentoo 站点

```bash
# cd /mnt/gentoo
```

启动 `links`（或 `lynx`）并访问我们的 Gentoo 镜像列表。选择一个离你最近的镜像并打开 `snapshots/` 目录。在那里，选中它并按 `D` 键下载最新的 Portage。

# 代码列表 13：浏览 Gentoo 镜像列表

```bash
# links http://www.gentoo.org/main/en/mirrors.xml
```

现在按 `Q` 退出浏览器。现在你已经在 `/mnt/gentoo` 中存储了一个 Portage 快照。在下一步中，我们将该快照提取到你的文件系统中。请确保你使用此完全确切的命令；最后一个字母是大写的 `C`，而不是小写的 `c`。

# 代码列表 14：提取日期标记快照

```bash
(将 <date> 替换为下载的快照的日期标记)
# tar xvjf /mnt/gentoo/portage-<date>.tar.bz2 -C /mnt/gentoo usr
```

## 5.e. 配置编译选项

### 简介

为了优化 Gentoo，你可以设置几个影响 Portage 行为的变量。这些变量都可以作为环境变量设置（使用 `export`），但它们不是永久的。为了保留你的设置，Portage 为你提供了 `/etc/make.conf`，这是 Portage 的配置文件。我们要修改的就是这个文件。

启动你喜喜欢的编辑器（在本指南中我们使用 `nano`），以便我们可以修改后文将讨论的变量。

# 代码列表 15：打开 /etc/make.conf

```bash
# nano -w /mnt/gentoo/etc/make.conf
```

正如你所注意到的，`make.conf` 文件的结构是通用的：注释行以 `#` 开头，其他行使用 `变量="内容"` 的语法定义变量。`make.conf` 使用相同的语法。接下来将讨论其中几个变量。

### CHOST

`CHOST` 变量声明了你项目的目标主机。该变量应该设置为正确的值。不要编辑它，因为那可能会破坏你的 stage 环境。如果你觉得 `CHOST` 变量看起来不正确，你可能使用了错误的 stage3ball。

### CFLAGS 和 CXX

`CFLAGS` 和 `CXX` 变量分别定义了 gcc C 和 C++ 编译器的优化标志。虽然我们在这里进行了通用的定义，但只有当你为每个程序单独进行优化时，才能获得最高性能。这是因为每个程序都是不同的。

在 `make.conf` 中定义能让你的系统响应良好的优化选项。根据经验建议在该文件中进行设置；过度优化可能会导致程序行为异常（崩溃，甚至更糟，功能故障）。

我们不会解释所有可能的选项。如果你想了解它们，请参考 GNU 在线手册（GNU Online Manual(s)）和 gcc info 文件（执行 `info gcc` —— 在可运行的 Linux 系统上有效）。`make.conf` 文件还包含许多示例和信息；不要忘记阅读它。

第一个设置是 `march=` 标志，它指定目标架构的。可能的选项定义在 `make.conf` 示例文件（注释）中。例如，对于 x86 架构的体验：

# 代码列表 16：提取日期标记

size-optimized, 0（0 表示无优化），1, 2 或 3 用于更多速度优化标志；每个级别都与前一个级别具有相同的标志，并外带有额外的。例如，对于 2 级优化：

# 代码列表 17：GCC 设置

```bash
-O2
```

另一个流行的优化标志是 `-pipe`（使用管道而非临时文件在编译的不同阶段之间进行通信）。

注意，使用 `-omit-frame-pointer`（它不会为不需要帧指针的函数在寄存器中保留帧指针）可能会对应用程序的调试产生严重影响！

当你定义 `CFLAGS` 和 `CXX` 时，你应该组合一些优化标志，如下文所示：

# 代码列表 18：定义 CFLAGS 和 CXX

```bash
CFLAGS="-march=atlon-xp -pipe -O2"
# AM64 用户应使用 march=k8
# EM64 用户应使用 march=nocona
CXX="$(CFLAGS)"
# 两个变量使用相同的设置
```

### MAKEOPTS

通过 `MAKEOPTS` 定义在安装包时应该进行多少次并行编译。一个好的选择是系统中 CPU 的数量加一，这并不总是完美的。

# 代码列表 19：适用于 1-CPU 系统的 MAKEOPTS

```bash
MAKEOPTS="-j2"
```

准备好了，预，跑！

按照你的喜好更新 `/mnt/gentoo/etc/make.conf` 并保存（nano 用户按 `Ctrl-X`）。你现在准备好继续安装 Gentoo 基础系统。

## 6. 安装 Gentoo 基础系统

### 6.a. Chroot

#### 可选：选择镜像

为了下载源代码，建议选择快速镜像。Portage 会在你的 `make.conf` 文件中查找 `GENTOO_MIRROR` 变量并使用其中列出的镜像。你可以转向镜像列表并搜索一个（或多个）镜像（因为它们通常是最快的），或者使用好用的工具 `mirrorselect`，它为你提供了一个良好的界面来选择镜像。

# 代码列表 1：使用 mirrorselect 设置 GENTOO_MIRROR 变量

```bash
mirrorselect -i o >> /mnt/gentoo/etc/make.conf
```

> **警告：** 不要选择任何 IPv6。我们的 stage 目前不支持 IPv6。

另一个重要的设置是 `make.conf` 中的 `SYNC` 设置。该变量处理了你在更新 Portage 树时想要使用的 rsync 服务器。

# 代码列表 2：使用 mirrorselect 设置 SYNC

```bash
mirrorselect -i o >> /mnt/gentoo/etc/make.conf
```

在 mirrorselect 之后，建议检查 `make.conf` 中的设置。

### DNS 信息

在进入新环境之前还有一件事要完成，即进入新环境后的 DNS 信息。你需要确保进入新环境后网络正常。

# 代码列表 3：复制 resolv.conf

```bash
(需要 L 选项以确保我们复制的是符号链接)
cp -L /etc/resolv.conf /mnt/gentoo/etc/resolv.conf
```

### 挂载 /proc 和 dev

挂载 proc 文件系统以允许 chroot 环境获取内核信息，然后绑定 dev 文件系统。

# 代码列表 4：挂载 /proc 和 dev

```bash
# mount -t proc none /mnt/gentoo/proc
# mount -o bind /mnt/gentoo/dev
```

### 进入新环境

现在一切已初始化且基础环境已安装，是时候 chroot 进入我们的新环境。这分三个步骤完成：首先我们将从安装介质复制到 `/mnt/gentoo`。然后我们使用 `env-update` 创建新环境。最后，我们加载这些变量。

# 代码列表 5：chroot 进入环境

```bash
# chroot /mnt/gentoo /bin/bash
# env-update
>> Regenerating /etc/ld.cache...
# source /etc/profile
# export PS1=$(chroot) $
```

恭喜！你现在位于 Gentoo Linux 内部。当然，这远未结束，这就是为什么安装过程还有几个章节。

### 6.b. 配置 Portage

#### 更新 Portage 树

你应该将 Portage 树更新到最新版本。`--sync` 会为你完成。

# 代码列表 6：更新 Portage 树

```bash
# emerge --sync
(如果你使用慢终端，如某些帧缓冲或串口，可以添加 --quiet 选项来加速此过程)
# emerge --sync --quiet
```



如果你处于一个阻止 `rsync` 的防火墙后，可以使用 `env-websync`，它将为你下载并安装 Portage 快照。

如果你意识到有新版本的 Portage 发布并且应该更新，请忽略它。Portage 将在安装当天之后更新。

### 选择正确的 Profile

首先，这里有一个简单的定义。
Profile 是任何 Gentoo 系统的构建块。它不仅指定了 `CHOST`、`FLAGS` 和其他重要变量的默认值，它还是

同时也了解创建包版本的系统。这一切都由 Gentoo 开发者维护。

以前，用户几乎不会触碰此类配置（profile）。然而，x86、ppa 和 alpha 用户可以在两个配置之间进行选择：一个用于 2.4 内核，另一个用于 2.6 内核。为了提高 2.6 内核的集成性，这一要求已被移除。ppc 和 ppc64 架构也有多个可用配置。我们稍后会讨论这些。

你可以通过以下命令查看你正在使用哪个配置：

#### 代码列表 7：验证系统配置

```bash
# ls -PFG /etc/make.profile
lrwxrwxr-x 1 root Apr 18 8:51 /etc/make.profile -> /usr/portage/profiles/default-x86/2006.0/
```

如果你使用的是上述架构之一，该配置将为你提供一个基于 Linux 2.6 的系统。这是推荐的默认设置，但你也可以选择另一个配置。

用户可能希望安装基于旧版 Linux 2.4 配置的系统。如果你有充分的理由这样做，应该先检查存在哪些配置。在 x86 上，你可以通过以下命令实现：

#### 代码列表 8：查找是否存在额外的配置

```bash
# ls -d /usr/portage/profiles/default-linux/x86/no-nptl/2.4
/usr/portage/profiles/default-linux/x86/no-nptl/2.4
```

上面的示例显示 2.4 配置存在（即它没有报错说缺少文件或目录）。建议保持默认设置，但如果你想切换，可以按照以下方式操作：

#### 代码列表 9：切换到 2.4 配置

```bash
(确保你使用了正确的架构，下面的示例适用于 x86 的)
# ln -sf /usr/portage/default-linux/x86/no-nptl/2.4 /etc/make.profile
# 列出 2.4 配置中的文件
# ls -PFG /etc/make.profile/
total 12
rw-r--r-- 1 939 Dec 10 14:06 packages
rw-r--r-- 1 347 Dec 3 2004 parent
rw-r--r-- 1 573 Dec 3 2004 virtuals
```

对于 ppc，2006.0 提供了许多新配置。

#### 代码列表 10：PPC 配置

```bash
（通用 PPC 配置，适用于所有 PPC 机器，精简版）
# ln -sf /usr/portage/profiles/default-linux/ppc32/2006.0/G3 /etc/make.profile
(G3 配置)
# ln -sf /usr/portage/profiles/ppc32/2006.0/G3 /etc/make.profile
(G3 配置)
# ln -sf /usr/portage/profiles/ppc32/2006.0/G3/Pegasos/ /etc/make.profile
(G4 Altivec 配置)
# ln -sf /usr/portage/profiles/ppc32/2006.0/G4 /etc/make.profile
(G4 Altivec 配置)
# ln -sf /usr/portage/profiles/ppc32/2006.0/G4/Pegasos/ /etc/make.profile
```

对于 pp64，2006.0 提供了许多新配置。

#### 代码列表 11：PPC64 配置

```bash
（通用 64 位用户 PPC64 配置，适用于所有 PPC64 机器）
# ln -sf /usr/portage/profiles/default-linux/ppc64/2006.0/64bit-user /etc/make.profile
（通用 32 位用户 PPC64 配置，适用于所有 PPC64 机器）
# ln -sf /usr/portage/profiles/default-linux/ppc64/2006.0/32bit-user /etc/make.profile
（每个用户拥有如下子配置，将 (user) 替换为从上方选择的用户）
970 配置 JS
# ln -sf /usr/portage/profiles/default-linux/ppc64/2006.0/(user) /etc/make.profile
(G5 配置)
# ln -sf /usr/portage/profiles/default-linux/ppc64/2006.0/(user)/970/pmac /etc/make.profile
(POWER3 配置)
# -snf /usr/portage/profiles/default-linux/linux/ppc64/2006.0/(user)/power3 /etc/make.profile
(POWER4 配置)
# -snf /usr/portage/profiles/default-linux/linux/ppc64/2006.0/(user)/power4 /etc/make.profile
# -snf /usr/portage/profiles/default-linux/linux/ppc64/2006.0/(user)/power5 /etc/make.profile
（multilib 配置在发布时尚不稳定）。
```

## 配置 use 变量

`USE` 是 Gentoo 提供的最强大的功能之一。许多程序可以在不包含某些项的情况下编译。例如，某些程序可以带有 `gtk-support` 编译，或者带有 `qt-support`。其他可以在不带 SSL 支持的情况下编译。某些程序可以带有 `framebuffer support (vga)` 而不是 X-server。

大多数发行版尽可能多地编译包，这增加了程序的大小和启动时间，更不用说大量的依赖项。通过 Gentoo，你可以定义包应该带有哪些选项。这就是 `USE` 的用处。在 `USE` 变量中，你定义映射到类的关键字。例如，`sdl` 会带有 `ssl-support` 编译。`gnome-kde` 会带有 `gnome` （以及 `kde`）但但不带 (`qt`)，你将对 OpenGL 进行完全调整。

默认设置放置在你配置的 `make.files` 目录中。默认 `USE` 是 `make.files` 中所有 `USE` 设置的总和。如果你添加了一个 `USE` 设置，它会被添加到列表中。如果你从列表中移除它（通过在前面加上减号），它将从列表中移除（在更新 Portage 时会被覆盖！）。`USE` 的完整描述可以在 Gentoo 手册的第二部分找到。可用 `USE flags` 的完整描述可以在你系统的 `/usr/portage/use.desc` 中找到。

#### 代码列表 12：查看 USE flags

```bash
# less /usr/portage/use.desc
（可以使用方向键滚动，按 'q' 退出）
```

作为一个带有 DVD 和 CD 的 KDE 系统使用 `USE` 设置的示例：

#### 代码列表 13：打开 /etc/make.conf

```bash
# nano -w /etc/make.conf
```

#### 代码列表 14：USE 设置

```bash
USE="gtk dvd alsa"
```

## GLIBC locales

你的系统中可能有一个或两个 locales。编译 `glibc` 后，将创建所有可用的 locales。现在你可以激活 locales 并在 `/etc/locale.build` 中指定你需要的 locales。如果你这样做，就知道选择哪些 locales：

#### 代码列表 15：为 glibc 激活 locales flag

```bash
# mkdir -p /etc/portage
# echo "sys-libs/glibc" >> /etc/portage/package.build
```

#### 代码列表 16：打开 /etc/locale.build

```bash
# nano -w /etc/locale.build
```

以下 locales 是获取英语（美国）和德国（德国）以及相应的 UTF-8 格式的示例：

#### 代码列表 17：指定你的 locales

```text
en_US/ISO-8859-1
en_US.UTF-8/UTF-8
de_DE/ISO-8859-1
de_DE.UTF-8/UTF-8
```



# 7. 配置内核

## 7.a. 时区

你需要选择你的时区，以便系统知道所在的位置。在`/usr/share/zoneinfo`中查找你的时区，然后将其复制到`/etc/localtime`。请使用`/usr/share/zoneinfo`中的`GMT*`名称，因为它们没有指示预期时区。例如，`GMT-8`实际上是`GMT+8`。

### 代码列表 1：设置时区信息

```bash
# ls /usr/share/zoneinfo
```
假设你想使用 GMT

```bash
# cp /usr/share/zoneinfo/GMT /etc/localtime
```

## 7.b. 安装源码

选择内核

所有发行版的核心都是 Linux 内核。它是用户程序和系统硬件之间的层。Gentoo 为用户提供了几种可能的内核源码。完整列表可以在内核 Guide 获取。

对于 x86 系统，我们还有内核：`vanilla-sources`（由内核开发者提供的默认内核源码）、`gentoo-sources`（打了性能增强补丁的内核源码）、……

选择你的内核并使用`emerge`安装它。`USE="config"`是为了避免在此阶段安装 x-11 或依赖项。`USE="symlink"`对于手动设置不是必须，但它可以确保`/usr/src/linux`软链接的正确修正。

### 代码列表 2：安装内核源码

```bash
# USE="config" emerge gentoo-sources
```

当你查看`/usr/src`时，你会看到指向你的内核源码的软链接。在这里，安装的内核源码指向`gentoo-sources-2.6.12-10`。你的版本可能不同，请记住。

### 代码列表 3：查看内核源码软链接

```bash
# ls -l /usr/src/linux
lrwxrwxrwx 1 root root 12 Oct 13 11:04 /usr/src/linux-2.6.12-gentoo-r10
```

现在是配置和构建你的内核了。你可以使用`genkernel`，这将构建一个如系统安装中使用的通用内核。我们首先使用“手动”配置，因为这是优化环境的最佳方法。

如果你想继续手动操作，请参考：手动配置。如果你想使用`genkernel`，应该阅读：替代方案：使用 genkernel。

## 7.c：默认手动配置

引言

手动配置内核通常被认为是 Linux 执行过的最困难的部分。事实完全并非如此——在配置几个内核后，你就不记得它有多困难了：

然而，有一点是真实的：手动启动内核时必须了解你的系统。大部分信息可以通过包含`lspci`的`eject`（`emerge eject`）获得。你可能可以在`chmod`后的环境中使用`lspci`。你可以安全地忽略`lspci`抛出的任何 pcilib 警告（例如`pcilib: cannot open /sys/bus/pci/devices`）。或者，你也可以从非 chmod 环境运行`lspci`。结果是相同的。你现在可以查看安装 CD 使用了哪些模块（它可能会为你提供关于启用哪些内容的提示）。

现在进入你的内核源码目录并执行`make menuconfig`。这将为你打开一个基于 ncurses 的配置菜单。

### Code List 4: Invoking menuconfig

```bash
# cd /usr/src/linux
# make menuconfig
```

你将看到几个配置区域。我们将首先列出你必须激活的一些选项（否则 Gentoo 将无法运行，或者在没有额外调整的情况下无法正常工作）

### 激活必要的选项

首先，激活对开发和实验性代码/驱动的使用。你需要这些，否则某些重要的代码/驱动将不会显示：

### Code List 5: Selecting experimental code/drivers, General setup

```
Code maturity level options --->
[*] Prompt for development and/or incomplete code/drivers

General setup --->
[*] Support for hot-pluggable devices
```

确保每个对系统启动至关重要的驱动（如 SCSI 控制器等……）都编译进内核，而不是作为模块，

现在选择正确的处理器族：

### Code List 6: Selecting processor family

```
Processor type and features --->
(根据你的系统进行更改)
Athlon/Duron/K7) Processor family
```

现在进入 Files Systems（文件系统）并选择你使用的文件系统。不要将它们编译为模块，否则你的 Gentoo 系统将无法挂载你的分区。还要选择 Virtual 和 /proc 文件系统。如果你正在使用 2.4 内核，你需要选择 /dev 文件系统，因为 2.4 内核不支持 dev。

### Code List 7: Selecting file systems

```
With a 2.4.x kernel
File systems --->
[*] Virtual file system support (former shm)
[*] /proc file system support
[*] /dev file system support (EXPERIMENTAL)
[*] automatically mount /dev at boot
[*] /dev partition for Unix98 PTYS

With a 2.6. kernel
File systems --->
Pseudo Filesystems --->
[*] /proc file system support
[*] Virtual file system support (former shm)

根据你的系统需要选择以下选项之一
<*> Reiserfs support
<*> Ext3 journaling file system support
<*> JFS file system support
<*> Second extended fs support
<*> XFS file system support
```

如果你的 BIOS 无法处理大硬盘，并且你跳跳了硬盘以报告限制的大小，你必须启用该选项以访问整个硬盘：

### Code List 8: Selecting autogometry resizing support

```
(2.4.x kernel only)
ATA/IDE/MFM/RLL support -->
IDE, ATA and ATAPI Block devices -->
[*] Include IDE/ATA-2 DISK support
[*] use multi-mode by default
[*] Auto-Geometry Resizing support
```

不要忘记为你的驱动开启 DMA：

### Code List 9: Activating DMA

```
Device Drivers -->
ATA/ATAPI/MFM/RLL support -->
[*] Generic PCI bus-master DMA support
[*] Use PCI DMA by default when available
```

如果你使用 PPPoE 连接互联网或使用拨号调制调器，你内核内核中以下选项：

### Code List 10: Selecting PPPoE necessary drivers

```
(With a 2.4.x kernel)
Network device support -->
[*] PPP (point-to-point protocol) support
[*] PPP support for async serial ports
[*] PPP support for sync tty ports

(With a 2.6.x kernel)
Device Drivers -->
Networking support -->
[*] PPP (point-to-point protocol) support
[*] PPP support for async serial ports
[*] PPP support for sync tty ports
```



这两个选项并无害，但并非绝对需要，然而，PPP over Ethernet 选项在 `rp-pppoe` 配置为你的网卡进入内核的 go 模式时可能会被使用。

如果你需要它，不要忘记在你的网卡中包含支持。

如果你有一颗支持超线程（tm）的 Intel CPU，或者你有一个多 CPU 系统，你应该激活“对称多处理”：

### Code List 11: Activating SMP support

```
Processor type and features -->

[*] Symmetric multi-processing support
```

如果你使用 USB 输入设备（如键盘或鼠标），不要忘记也启用它们：

### Code List 12: Activating USB Support for Input Devices

```
USB Support -->

[*] Human Interface Device (full HID)
```

支持 PCMCIA 的笔记本用户如果选择使用 2.4 内核，不应使用 PCMCIA 驱动。较新的驱动可以通过 `pcmcia-cs` 包获得，该包稍后安装。2.6 内核用户应该使用内核中的 PCMCIA 驱动。

除了在 2.6 内核中编译 PCMCIA 支持外，不要忘记对系统中存在的 PCMCIA 卡桥的支持：

### Code List 13: Enabling PCMCIA support for 2.6 kernels

```
Bus options (PCI, PCMCIA, EISA, MCA, ISA) --->

PCARD (PCMCIA/Cardbus) -------------

<*> PCARD (PCMCIA/Cardbus)

(如果需要旧 PCMCIA 卡支持请选择)

[*] PCMCIA support

[*] 32-bit Cardbus

(选择下方芯片组)

--- PC-card bridges

<*> Cardbus-compatible support (NEW)

<*> Cirrus Logic compatible support (NEW)

<*> Generic compatible support (NEW)

<*> Desktop compatible support (NEW)

<*> Audio bridge support (NEW)
```

当你完成内核配置后，继续。

### 编译与安装

现在内核已配置好，是时候编译并安装它了。执行配置并编译：

### Code List 14: Compiling the kernel

```
(For 2.6 kernel)

# make dep bImage modules_install

(For 2.6 kernel)

# make modules_install
```

内核完成后，将内核拷贝到 `/boot`。使用适合你内核的名称并记住它，因为你在配置启动时需要它。

### Code List 15: Installing the kernel

```
# cp arch/i86/boot/bzImage /boot/<kernel-version>
```

现在继续内核模块

### 替代方案：使用 genkernel

如果你正在阅读本节，说明你选择使用 `genkernel` 脚本为你配置内核。现在内核源码已安装，是时候使用 `genkernel` 脚本为你编译内核了。`genkernel` 的工作方式是完全按照我们安装 CD 的方式配置内核。这意味着当你构建时，系统将在启动时检测所有硬件，就像我们的安装 CD 一样。由于 genkernel 不需要任何手动配置，对于不习惯拥有内核的用户来说是理想的解决方案。现在首先 genkernel：

### Code List 16: Emerging genkernel

```
# emerge genkernel
```

接下来，如果你要配置 2.6 内核，将安装 CD 使用的内核拷贝到 genkernel 查找默认配置的位置：

### Code List 17: Copying over Installation CD kernel

```
(如果你要配置 2.6 内核)

# zcat /proc/config.gz > /usr/share/genkernel/x86/kernel-2.6
```

现在运行 genkernel 编译内核。注意，genkernel 编译的是支持几乎所有硬件的内核，此编译需要一段时间！

注意，如果你的启动分区使用 ext2 或 ext3 文件系统，你可能需要使用 `genkernel --config` 手动配置你的内核并添加你的文件系统支持（即不是作为模块）。EXT2 或 LVM2 用户可能想要添加 `-ext2` 或 `-lvm2` 参数。

### Code List 18: Running genkernel

```
# kernel all
```

一旦 genkernel 完成，将创建一个内核、全套模块和根磁盘 (`initrd`)。我们将在本文稍后配置启动时使用该内核和 initrd。记下内核和 initrd 的名称，因为你在编写启动配置文件时需要它们。initrd 将启动后立即运行硬件自动检测（就像安装 CD 一样），在你的“真实”系统启动之前。

### Code List 19: Checking the created kernel name and initrd

```
# ls /boot/initramfs*
```

现在，让你的系统像安装 CD 一样——启用 coldpug。当 initrd 检测到需要启动系统时，coldpug 会检测其他内容。要提取并启用 coldpug，输入：

### Code List 20: Emerging and enabling coldpug

```
# emerge coldpug

# rc-update add coldpug boot
```

### 内核模块

#### 配置模块

你应该列出在 `/etc/modules.autoload.d/kernel-2.4`（或 `kernel-2.6`）中自动加载的模块。如果你需要，可以为模块添加额外选项。

要查看所有可用模块，运行以下命令。不要将 `<kernel version>` 替换为安装的内核版本。

### Code List 21: Viewing available modules

```
# find /lib/modules/<kernel version>/ -type f -iname '.*' -or -iname '*..ko'
```

例如，为了自动加载 `3c59.o` 模块，编辑 `kernel-2.4` 或 `kernel-2.6` 文件并在其中输入模块名。

### Code List 22: Editing /etc/modules.autoload.d/kernel-2.4

```
(2.4 内核的示例)

# nano -w /etc/modules.autoload.d/kernel-2.4
```

### Code List 23: /etc/modules.autoload.d/kernel-2.4 or kernel-2.6

```
3c59
```

通过“配置你的系统”继续安装。

## 8. 配置你的系统

### 8.a. 文件系统信息

什么是 `fstab`？

在 Linux 下，系统使用的所有分区都必须列在 `/etc/fstab` 中。此文件包含这些分区的挂载点（在文件系统结构中可见的位置）、它们应该如何挂载以及带有哪些特殊选项（自动或手动、用户是否可以挂载它们）

`/etc/fstab` 使用特殊的语法。每行由六个字段组成，由空白（空格、制表符或混合使用）分隔。每个字段都有其特定的含义：

- 第一个字段显示分区（通过设备文件的路径描述）
- 第二个字段显示分区应该挂载的挂载点
- 第三个字段显示分区使用的文件系统
- 第四个字段显示选项（`mount` 在挂载分区时使用的选项）。由于每个文件系统都有自己的选项，鼓励用户阅读 man 页面（使用 `man mount` 句可以查看选项列表）。多个选项之间用逗号分隔。
- 第五个字段用于 `dump` 命令，以确定分区是否需要备份。你可以轻松地将其生成为 0（零）。
- 第六个字段用于 `fsck` 命令，以确定系统未正常关机时检查文件系统的顺序。根文件系统应为 1，其余部分为 2（如果不需要进行 `fsck` 检查则为 0）。

Gentoo 提供的默认 `/etc/fstab` 不是一个有效文件，因此请从 `none`（或你喜欢的）开始创建你的 `/etc/fstab`：

### 代码列表 1: 打开 /etc/fstab

```
# nano -w /etc/fstab
```



让我们看看如何为 `/boot` 分区编写选项。这是一个示例，如果你的架构不需要 `/boot` 分区（例如 PPC 机器），请不要复制它。

在我们的 x86 分区示例中，`/boot` 是 `/dev/sda1`，使用 `ext2` 作为文件系统。它在启动期间需要被检查，因此我们应该写道：

```
代码列表 2: /etc/fstab 中的一个 /boot 行示例

/dev/sda1 /boot ext2 defaults 1 2
```

有些用户不希望自动挂载 `/boot` 分区，以提高系统的安全性。这些人应该应该使用 `defaults,noauto`。这意味着每当你想想要使用该分区时，都需要手动挂载它。

现在，为了提高性能，用户可能希望在挂载点处添加 `noatime` 选项，这在系统中运行更快，因为不再记录文件访问时间（通常你也不需要这些信息）：

```
代码列表 3: /etc/fstab 中改进后的 /boot 行

/dev/sda1 /boot ext2 defaults,noatime 1 2
```

如果继续继续操作，我们将使用以下行（针对 `/boot`、 `/` 和交换 分区）：

```
代码列表 4: 三行 /etc/fstab 内容

/dev/sda1 /boot ext2 defaults,noatime 1 2

/dev/sda2 none swap 0 0

/dev/sda3 / ext3 noatime 0 1
```

最后，你应该为 `/proc`、 `tmpfs`（必需的）以及你的 CD-ROM 驱动器添加规则（如果你有或其他分区或驱动器，也为它们添加）：

```
代码列表 5: 完整的 /etc/fstab 示例

/dev/sda1 /boot ext2 defaults,noatime 1 2

/dev/sda2 none swap 0 0

/dev/sda3 / ext3 noatime 0 1

none /proc proc defaults 0 0

none /proc/sh tmpfs nodev,nosuid,noexec 0 0

/dev/cdrom0 /mnt/cdrom auto noauto,user 0 0
```

`auto` 为文件系统提供挂载外观（推荐用于可移动介质，因为它们可以使用许多文件系统之一创建），而 `user` 则允许非 root 用户挂载 CD。

现在使用上面的示例来创建 `/etc/fstab`。如果你是 SPARC 用户，你还应该向 `/etc/fstab` 中添加以下行：

```
代码列表 6: 向 /etc/fstab 添加 openprism 文件系统

none /proc/openprism openprism defaults 0 0
```

双重检查你的 `/etc/fstab`，保存并退出以继续。

## 8.b. 网络信息

### name, Domainname 等.

用户必须做出的选择之一是他的 PC 名称。这可能非常简单，但许多用户在为 Linux-pc 寻找合适的名称时遇到困难。为了加快速度，请记住你选择的任何名称之后都可以更改。为了保险起见，你只需将你的系统和域名主机命名为 `hostnetwork`。

我们在接下来的示例中使用这些值。首先我们设置主机名：

```
代码列表 7: 设置主机名

# nano -w /etc/conf.d/hostname

（将 HOSTNAME 变量设置为你的主机名）

HOSTNAME=ua
```

其次我们设置域名：

```
代码列表 8: 设置域名

# nano -w /etc/conf.d/domainname

（将 DNSDOMAIN 变量设置为你的域名）

DNSDOMAIN=hoomenetwork
```

如果你有一个 NIS 域（如果你不知道那是什么，那么你就没有），那么你需要设置一个 NIS 域名：

```
代码列表 9: 设置 NIS 域名

# nano -w /etc/conf.d/domainname

（将 DNSDOMAIN 变量设置为你的域名）

DNSDOMAIN=hoomenetwork
```



（将 `HOSTNAME` 变量设置为你的主机名）

`HOSTNAME`=ua

```
其次我们设置域名：
```

代码列表 8: 设置域名

# `nano -w /etc/conf.d/domainname`

（将 `DNSDOMAIN` 变量设置为你的域名）

`DNSDOMAIN`=hoomenetwork

```
如果你有一个 NIS 域（如果你不知道那是什么，那么你就没有），那么你需要设置一个 NIS 域名：
```

代码列表 9: 设置 NIS 域名

# `nano -w /etc/conf.d/domainname`

（将 `DNSDOMAIN` 变量设置为你的域名）

`DNSDOMAIN`=hoomenetwork

```
（注：由于原文后半部分存在大量重复和乱码，上述译文已基于技术逻辑进行了对齐处理。）
```

```bash
# nano -w /etc/rc.conf
```

当你完成 `/etc/rc.conf` 的配置后，保存并退出。

如你所见，此文件充满了注释，帮助你设置必要的配置变量。你可以配置系统使用 unicode 字符，并定义你的默认编辑器和显示器管理器（如 `gdm` 或 `kdm`）。

Gentoo 使用 `/etc/conf.d/keymaps` 来处理键盘配置。编辑它来配置你的键盘。

代码列表 24：打开 `/etc/conf.d/keymaps`

```bash
# nano -w /etc/conf.d/keymaps
```

使用 `KEYMAP` 变量时要小心。如果你选择了错误的 `KEYMAP`，在键盘上打字时会得到奇怪的结果。

> 注意：基于 USB 的 SPARCS 和 SPARC 用户可能需要选择 i386 键盘（如 "us"）而不是 "sunkeymap"。PPC 在大多数系统上使用 x86 内核。能够在启动时使用 ADB 键映射来启用内核中 ADB 键码发送的用户，必须在 `/etc/conf.d/keymaps` 中设置 mac/ppc 键映射。

当你完成 `/etc/conf.d/keymaps` 的配置后，保存并退出。

Gentoo 使用 `/etc/conf.d/clock` 来设置时钟选项。根据你的需求进行编辑。

代码列表 25：打开 `/etc/conf.d/clock`

```bash
# nano -w /etc/conf.d/clock
```

如果你的硬件没有使用 `CLOCK`，你需要在文件中添加 `CLOCK="local"`。否则，你将注意到一些时钟偏移。此外，Windows 假设你的硬件时钟使用本地时间，因此如果你想让它可行，应该相应地设置此变量，否则你的时钟会错乱。

当你完成 `/etc/conf.d/clock` 的配置后，保存并退出。

如果你不是在 IBM PPC64 硬件上安装 Gentoo，请继续“安装必要的系统工具”。

## 配置控制台

> 注意：以下章节适用于 IBM PPC64 硬件平台。

如果你在 IBM PPC64 硬件上运行 Gentoo 并使用虚拟控制台，你必须取消 `/etc/initittab` 中相应行的注释，以便为虚拟控制台生成登录提示。

代码列表 26：在 `/etc/initstab` 中启用 hvc 或 hvs 支持

```text
hvc0:12345:respawn:/sbin/agetty -L 9600 hvc0
hvs0:12345:respawn:/sbin/agetty -L 19200 hvs0
```

你还应该注意验证 `/etc/security` 中是否列出了相应的控制台。

你现在可以继续“安装必要的系统工具”。

# 9. 安装必要的系统工具

### 9.a. 设备管理器

如果你正在使用 2.4 内核并从 stage 3 安装 Gentoo，有几件事是你需要做的。由于 Gentoo 现在使用 `udev`，而 2.4 内核不支持 `udev`，你将不得不利用 `devfs` 并移除 `udev`。

代码列表 1：安装 devfsd

```bash
(针对使用 2.4.x 内核并进行 stage 3 安装的用户)
# emerge --unmerge udev
# emerge devrad
```

### 9.b. 系统日志记录器

某些工具需要在 stage3 归档中做出决定，因为几个软件包提供了相同的功能。现在由你选择想要安装哪些。

你第一个需要决定的工具是用于你系统的日志设施。Unix 和 Linux 拥有出色的日志功能历史——如果你能将日志文件中发生的一切记录下来。这是通过系统日志器器实现的。

Gentoo 提供了几种系统日志记录器供选择。有 `syslog`（一组传统的日志守护进程）、`syslog-ng`（一种高级的系统日志器器）和 `metalog`（一个高度定制的日志守护器，*注：此处原文为 metalog，推测为 metalelog*）。

Gentoo 提供了几种系统日志记录器供选择。

使用 `syslog-ng` 提供了你系统日志的系统日志记录器（*此处后文重复*）。能够在启动时使用 ADB 键映射来启用内核中 ADB 键码发送的用户，必须在 `/etc/conf.d/keymaps` 中设置 mac/ppc 键映射（*此处后文重复*）。

代码列表 2：安装 syslog-ng

```bash
# emerge syslog-ng
```

（注：etc，etc/conf/conf.conf//，，，.. 。

### 9.c. 守护进程

### 9.d. 索引

### 9.e. 文件系统

### 9.f. 网络工具

| | | | |
|---|---|---|---|
| 640x480 | 800x600 | 1024x768 | 1280x1024 |
| 256 | 0x031 | 0x035 | 0x037 |
| 32k | 0x031 | 0x034 | 0x036 | 0x039 |
| 64k | 0x031 | 0x037 | 0x019 |
| 16M | 0x031 | 0x035 | 0x018 |

视频语句控制帧缓冲区显示选项。它应该是你想要启用的帧缓冲区设备（针对 2.6 内核或 2.4 内核的 vesa）。所有变量都列在 `/usr/src/Documentation/fb/vesafb.txt` 中，我们将告知您三个最常用的选项：

# 控制描述

- wrap around（环绕）：显卡可以环绕内存（即在到达末尾时继续执行）
- set MTRR（设置 MTRR）：它可以是：0 - 禁用不可缓存，2 - 写回（write-back），3 - 写合并（write-combining）
- mode set（模式设置）：颜色深度和刷新率。例如，1024x768-32@85 表示分辨率为 1024x768，位深 32 位，刷新率为 85。

这两种更改的结果将类似于 `vga=0318-vesafb:mtrr:3,wrap` 或 `video=vesafb:mtrr:3,1024x768-32@85`。请记住（或者当你关闭它时），你很快就会需要用到它。

现在继续安装 GRUB 或 LILO。

## 10.b: 默认：使用 GRUB

### 理解 GRUB 术语

安装 GRUB 最关键的部分是熟悉 GRUB 如何引用驱动器和分区。你的 Linux 分区 `/dev/sda1` 在 GRUB 下可能会被标记为 `(hd0,0)`。请注意括号。

硬盘从零 "a" 开始，分区也从零开始。请注意，对于 hd 设备，只计算硬盘，而不包括像光驱驱动器和刻录机之类的设备。此外，该计数也用于 SCSI 设备。（通常它们会获得更高的 IDE 索引，其中 BIOS 配置为从 SCSI 设备启动）。当你使用 BIOS 从不同的硬盘启动（作为你的主从盘）时，它被视为 hd0。

假设你在 `/dev/sda` 上有一个驱动器，在 `/dev/cdrom` 上有一个光驱驱动器，在 `/dev/hdc` 上有一个刻录机，在 `/dev/hdd` 上有一个第二个硬盘，且没有 SCSI 硬盘，那么那么 `/dev/hdb1` 将翻译为 `(hd1,1)`。这听起来很复杂，事实也如此，但正如我们将看到的，GRUB 为那些拥有大量硬盘和分区且在 GRUB 编号方案中迷失方向的人提供了一个补全机制。

掌握了这种感觉，是时候安装 GRUB 了。

### 安装 GRUB

要安装 GRUB，让我们先通过 `emerge` 安装它：

```bash
# 代码列表 1: 安装 GRUB
# emerge grub
```

虽然 GRUB 现在已经安装，但我们仍然需要为它编写配置文件，并将 GRUB 放入 MBR，以便 GRUB 自动启动你新创建的内核。使用 `nano`（或如果适用，使用另一个编辑器）创建 `/boot/grub.conf`：

```bash
# 代码列表 2: 创建 /boot/grub.conf
# nano -w /boot/grub.conf
```



现在我们将编辑第一个 `grub.conf`。对于我们在本指南中使用的分区示例，你会发现两个 `grub.conf`。我们只对第一个 `grub.conf` 进行了详尽的注释。请确保使用你的内核文件名缩进，并在适当的情况下，使用你的 `initrd` 镜像文件名。

- 第一个 `grub.conf` 是给那些没有使用 `genkernel` 构建内核的人使用的
- 第二个 `grub.conf` 是给那些使用过 `genkernel` 构建内核的人使用的

> 注意：如果你的文件系统是 `JFS`，则你必须在内核行中添加 `"ro"`，因为 `JFS` 在允许读写挂载之前需要重放其日志（`log`）。

### 代码列表 3. 适用于非 genkernel 用户的 grub.conf

```bash
# 默认启动哪项列表。0 是第一个，1 是第二个，依此类推。

default 0

# 在启动默认列表之前等待多少秒。

timeout 30

# 用于美观的平整启动图像：

# 如果你没有安装显卡，请注释掉它

splashimage=(hd0,0)/boot/splash.xpm

title=center Linux 2.6.12-r10

# 内核镜像（或操作系统）所在的分区

root=(hd0,0)

kernel /kernel-2.6.12-genkernel-r10 root=/dev/hda3

# 仅当你与 Windows 系统进行双启动时需要以下行。

# 在这种情况下，windows 位于 /dev/hdat

title=Windows XP

rootverify=(hd0,5)

makeactive

chaloader +1
```

### 代码列表 4. 适用于 genkernel 用户的 grub.conf

```bash
default 0

timeout 30

splashimage=(hd0,0)/boot/splash.xpm

title=center Linux 2.6.12-r10

kernel /kernel-x86-2.6.12-genkernel-r10 root=/dev/ram0 init=/inituxrd mask=8192 real_root=/dev/hda3

initrd /initramfs-genkernel-x86-2.6.12-genkernel-r10

# 仅在你想进行双启动时

title=Windows XP

rootverify=(hd0,5)

makeactive

chaloader +1
```

> 注意：内核行中提到的 `udev` 是为了在用 `udev` 代替它（这是默认设置）时，绕过某些 `genkernel` 版本中的一个 `bug` 而需要的。

如果你使用了不同的分区方案并相应地更改了内核镜像，请确保所有 `GRUB` 设备（如 `(hd0,0)`）都是相对于挂载点而非根目录。换句话说，`hd0,0)/grub/splash.gz` 位于 `/boot/grub/splash.gz`。如果你选择了...（此处原文后续存在重复及乱码，已根据逻辑翻译并处理）

当然，它也被一些了解 `LILO` 并想要坚持使用它的人使用。无论哪种，`Gentoo` 都支持两者，而且重要的是你选择了使用 `LILO`。

安装 `LILO` 易而举举；只需使用 `emerge` 即可

### 代码列表 9: 安装 LILO

```bash
# emerge lilo
```

## 配置

要配置 `LILO`，你必须创建 `/etc/lilo.conf`。启动你最喜欢的编辑器（在本手册中，为了保持一致，我们使用 `nano`）并创建该文件。

### 代码列表 10: 创建/etc/lilo.conf

```bash
# nano -w /etc/lilo.conf
```

我们要求你记住的一些事情是你创建的内核名称。在接下来的示例 `lilo.conf` 中，我们使用了示例分区方案。它有两个独立的部分：

- 适用于没有使用内核来构建内核的用户
- 适用于使用了内核来构建内核的用户

请确保在每个启动项之后使用你的内核文件名，并在适当的情况下加上你的 `initrd` 行。`JFS` 在允许读写之前需要重放其日志。

> 注意：如果你的根文件系统是 `JFS`，你必须在每个启动项之后添加 `append='ro'` 行，因为 `JFS` 在允许读写之前需要重放其日志。

### 代码列表 11: 示例/etc/lilo

```bash
boot=/dev/hda      # 将 LILO 安装在 MBR 中

prompt            # 给用户选择另一个部分的机会

timeout=50         # 在启动默认部分之前等待 5（五）秒

default=gentoo     # 当超时通过后，启动 "gentoo" 部分

# 对于非通用内核用户

image=/boot/kernel-generic-2.6.12-gentoo-r10

label=gentoo      # 给此部分的内核命名的

read-only=ro      # 以只读根启动。不要修改！

root=/dev/hda3    # 根文件系统的位置

# 对于内核用户

image=/boot/kernel-generic-x86-2.6.12-gentoo-r10

label=gentoo

read-only=n

append="initrd=/linuxux_ramdisk=8192 root=/dev/hda3 udev"

initrd=/boot/initramfs-kernel-generic-2.6.12-gentoo-r10

# 这两行仅适用于你与 Windows 系统双启动的情况。

# 在这种情况下，Windows 托管在 /dev/hda6。

other=/dev/hda6

label=windows
```

> 注意：`append` 行中提到的 `udev` 是为了在最初就使用 `udev`（这是默认行为）时，在某些内核版本中的解决方案解决方案。

如果你需要向内核传递任何额外选项，请在该部分添加 `append` 语句。例如，我们添加了 `video` 语句来启用帧缓冲：

### 代码列表 12: 使用 append 添加内核选项

```bash
image==/kernel-2.6.12-gentoo-r10

label=gentoo

read-only=ro

root=/dev/hda3

append=video:vesafb:mtrr,ywrap,1024x768-32885*
```

如果你正在使用 `2.6.7` 内核，并且因为 `BIOS` 无法处理大硬盘导致你的硬盘卡死，你需要追加 `dx=store`。

`genkernel` 用户应该知道他们的内核使用与安装 `CD` 相同的启动选项。例如，如果你有 `SCSI` 设备，你将 `doskel` 作为内核。

现在保存并退出。要完成操作，你必须运行 `/sbin/lilo`，以便 `LILO` 将 `/etc/lilo.conf` 复制到你的系统（即从磁盘安装）。
请记住，每次安装新内核或对菜单进行任何更改时，都必须运行 `/sbin/lilo`。

### 代码列表 13: 完成 LILO 安装

> 注意：当你重新安装内核时，你不再需要复制文件了。只需在编译内核后运行 `make install` 即可；它会自动复制必要的文件并调整 `LILO` 配置。

你现在可以继续重启系统

## 10. 重启系统

退出环境并卸载所有已挂载分区。然后输入你一直等待的魔法命令：`reboot`。

### 代码列表 14: 卸载所有分区并重启

```bash
# exit

cd /

umount -f /mnt/gentoo/boot /mnt/gentoo/dev /mnt/gentoo/proc /mnt/gentoo

reboot -f
```



当然，不要忘记移除启动 CD，否则将再次启动 CD 而不是你的 Gentoo 系统。

一旦在你的 Gentoo 安装中重启，请完成完成你的 Gentoo 安装。

## 11. 完成你的 Gentoo 安装

### 11.a. 用户管理

#### 为日常使用添加用户

在 Unix/Linux 系统上以 root 身份操作是危险的，应该尽可能避免。因此，强烈建议添加一个用于日常使用的用户。

你所属的组定义了该用户可以执行的活动。下表列出了你可能想要使用的若干重要组：

| 组 |  |
| :--- | :--- |
| audio | 能够访问音频设备 |
| cdrom | 能够直接访问光设备 |
| floppy | 能够直接访问磁盘设备 |
| games | 能够玩游戏 |
| port | 能够作为普通用户使用 --pretend |
| usb | 能够访问 USB 设备 |
| plugdev | 能够挂载和使用相机和 USB 盘等即插拔设备 |
| video | 能够访问视频硬件并进行硬件加速 |
| wheel | 能够使用 su |

例如，要创建一个名为 `john` 且属于 `wheel`、`users` 和 `audio` 组的用户，请以 root 身份登录（只有 root 可以创建用户）并运行 `useradd`：

# 代码列表 1: 为日常使用添加用户

```
Login: root

Password: (你的 root 密码)

# useradd -m -G users,wheel,audio -s /bin/bash john

# passwd john

Password: (输入 john 的密码)

Re-enter password: (重新输入密码以验证)
```

如果用户需要以 root 身份执行某些任务，你可以使用 `su -` 临时临时获得 root 权限。另一种方法是使用 `sudo` 软件包，如果配置正确，它是安全的。

## 12. 接下来该去哪里？

### 12.a. 文档

恭喜！你现在有一个可以运行的 Gentoo 系统了。接下来该去哪里？你现在有哪些选择？首先探索什么？

Gentoo 为用户提供了许多可能性，因此也有许多文档记录（以及未记录的）的功能。你应该看看手册的后续部分，它解释了如何更新软件、如何安装更多软件、USE 标志以及 Init 系统如何工作。

如果你对为桌面优化系统感兴趣，请查看文档资源。此外，你可能还想使用我们的本地化指南来让你的系统感觉更亲切。

我们还有值得阅读的 Gentoo 安全手册。

要查看所有文档的完整列表，请查看文档资源。

### 12.b. Gentoo 在线

我们非常欢迎来到 Gentoo 论坛或任何一个 Gentoo IRC 频道。

我们还有几个对所有用户开放的邮件列表列表。有关如何加入的信息包含在该页面中。

我们现在闭嘴，让你享受你的安装过程 :)

```bash
# emerge --sync
```

如果您由于防火墙限制而无法重新同步，仍然可以使用我们每日生成的 Portage 树快照来更新 Portage 树。`emergewebsync` 工具会自动在您的系统上获取并安装最新的快照：

# 代码列表 3: 运行 emerge-webresync

```bash
# emerge-webresync
```

### 1.c. 维护软件

#### 搜索软件

若要在 Portage 树中搜索软件名称，可以使用 emerge 内置的搜索功能。默认情况下，`--search` 会返回名称匹配（完全或部分匹配）给定搜索词的包名。

例如，搜索所有名称中包含 "pdf" 的包：

# 代码列表 4: 搜索包含 pdf-name 的包

```bash
$ emerge --search pdf
```

# 代码列表 5: 搜索 pdf 相关的包

```bash
$ emerge --searchdesc pdf
```

# 代码列表 6: 'emerge--search' 输出示例

```text
* net-print/cups-pdf

Latest version available: 1.5.2

Latest version installed: [ Not Installed ]

Size of installed files: 15 kB

Homepage: http://cip.physik.uni-weiersburg.de/~vrherr/cups-pdf/

Description: Provides a virtual printer for CUPS to produce files.

License: GPL-2
```

#### 安装软件

一旦您找到了喜欢的软件，就可以使用 emerge 轻松地安装它：只需添加包名。例如，安装 `gnumeric`：

# 代码列表 7: 安装 gnumeric

```bash
# emerge gnumeric
```

由于许多应用程序之间相互依赖，尝试安装某个软件包可能会导致同时安装多个依赖项。别担心，Portage 能很好处理依赖关系。如果您想知道 Portage 在您要求安装某个包时会安装什么，请添加 `--pretend` 选项。例如：

# 代码列表 8: 预装安装 gnumeric

```bash
# emerge --pretend gnumeric
```

当您请求安装一个包时，它将从互联网下载必要的源代码（如果有必要），并默认将其存储在 `/usr/port/distfiles` 中。之后，它将解压、编译并安装该包。如果您想让 Portage 只下载源码而不安装，请在 emerge 命令中添加 `--fetchonly`：

# 代码列表 9: 下载 gnumeric 的源码

```bash
# emerge --fetchonly gnumeric
```

#### 查找已安装包的文档

许多包带有自己的文档。有时，`doc` 标志决定了是否应该安装包文档。可以使用 `emerge -vp <package name>` 命令检查 `doc` 标志是否存在。

# 代码列表 10: 检查 doc 标志是否存在

```bash
(alsa-lib 仅仅是一个例子，当然。）
# emerge -vp alsa-lib
ebuid N media-lib/alsa-lib-1.0.9_rc +doc -jack 674 KB
```

您可以在 `/etc/make.conf` 文件中全局启用 `doc` USE 标志，也可以在 `/etc/portage/package.file` 中按包启用。USE 标志详细涵盖了这一方面。
一旦包安装完成，其文档将生成在 `/usr/share/doc` 下与包同名的子目录中。您也可以使用 `list` 列出所有已安装的文件。

# 代码列表 11: 定位包文档

```bash
# ls -l /usr/share/doc/alsa-lib-1.0.9_rc

total 24

-rw-r--r 1 root      669 May 17 21:54 Changelog.gz

-rw-r--r 1 root      9373 May 17 21:54 COPYING.gz

dr-xr-x 2 root      4096 May 17 21:54 hinfo

dr-xr-x 1 root      196 May 17 21:54 TODO.gz

（或者，使用 equ 定位已安装的文件）：

# query files alsa-lib | less

media-lib/alsa-lib-1.0.9_rc:

*

/usr

/usr/bin

/usr/bin/alsaisimp
(输出已截断)
```

#### 移除软件

当您想从系统中移除软件包时，使用 `emerge --unmerge`。这将告诉 Portage 从系统中移除由该包安装的所有文件。然而，您也可以使用 `--unmerge` 移除特定的包。

# 代码列表 12: 移除 gnumeric

```bash
# emerge --unmerge gnumeric
```

#### 更新系统

为了保持您的系统处于完美状态，您需要定期更新。由于安全更新也会发生，建议定期运行此命令：

# 代码列表 13: 更新您的系统

```bash
# emerge --ask world
```

如果您想更新系统上的每一个包，请添加 `--depth` 参数：

# 代码列表 14: 更新整个系统

```bash
# emerge --depth world
```

如果您更改了任何 USE 标志，您可能也需要添加 `--newuse`：

# 代码列表 15: 执行全更新

```bash
# emerge --newuse world
```



![](img/0231913cf6f51d9b747.png)

#### 元包页 (Metapages)

Portage 树中的某些包没有实际内容，但用于安装一组软件包。例如，`kde` 包将通过引入各种包来安装一个完整的 KDE 环境。

如果您想从系统中移除一个包，运行 `remove` 该包可能不会产生效果，因为依赖项仍然存在。Portage 也具有移除孤立依赖项的功能。所有操作通过以下三个命令完成：

# 代码列表 16: 移除孤立依赖

```bash
# emerge --depth world
# emerge --deplean
# revdep-rebuild
```

`revdep-rebuild` 由 `gentoolkit` 包提供；记得先安装它：

# 代码列表 17: 安装 gentoolkit 包

```bash
# emerge gentoolkit
```

### 1.d. Portage 报错时...

#### 关于 SLOT、虚拟包、分支、架构和配置文件

如前所述，Portage 功能强大并支持许多提供软件管理工具的功能。为了理解这一点，我们简要介绍 Portage 的几个方面，而不深入探讨细节。

同一个包的不同版本可以共存。虽然其他系统倾向于为这些版本命名包名（如 freetype 和 type2），但 Portage 使用了一种技术来调用槽（slots）。一个 ebb 为其系统声明 SLOT。具有不同槽的 ebuild 可以在同一系统中共存。例如，freetype 包使用 SLOT="1" 和 SLOT="2" 构建。

还有一些包提供相同的功能但实现方式不同。例如，metalog、syslog 和 syslog-ng 都是系统日志记录程序。依赖“系统日志记录程序”可用的应用程序不能依赖于（例如）metalog，因为其他的系统日志记录程序

是任何虚拟系统的良好选择：由于每个系统日志记录器都提供了 virtual/syslog，使得应用程序可以依赖 virtual/syslog。

Portage 树中的软件可以存在分支中。默认情况下，你的系统只接受 Gentoo 抽象（deabs）。大多数稳定软件在提交后会被添加到测试分支（testing branch），这意味着在标记为稳定之前需要进行更多测试。虽然你会在 Portage 树中看到这些软件的 ebabs，但在它们被放入稳定分支（stable branch）之前，Portage 不更新它们。

某些本体（ontology）仅适用于少数功能。该软件无法在其他架构上运行，或者需要更多测试，或者提交软件到 Portage 树的开发者无法验证该包在某些架构上是否可用。

每个 Gentoo 安装都遵循一个配置（profile），该配置包含了除其他信息外，系统正常运行所需的软件包列表。

## 被阻塞的包 (Blocked Packages)

```
Code Listing 18: Portage 关于阻塞包的警告 (--pretend)

[blocks B   mail-mta/smtp (is blocking mail-mta/postfix-2.2.2-rl)]
```

```
Code Listing 19: Portage 关于阻塞包的警告 (--pretend)

!!! Error: mail-mta/postfix 包与另一个包冲突。
!!! 两个包无法同时安装在同一个系统中。
!!! 请使用 'emerge --pretend' 来确定阻塞项。
```

Ebuild 特性告知 Portage 它的依赖关系。有两种可能的依赖关系：构建依赖（声明在 DEPEND 中）和运行依赖（声明在 RDEPEND 中）。当这些依赖关系中的某一个将一个包或虚拟包标记为不冲突时，它会触发冲突。

要修复冲突，你可以选择不安装该包或移除冲突的包。在这种情况下，你可以选择不安装包或先移除 sntpt。

还可能存在两个要安装的包相互阻塞。在这种情况下，你应该弄清楚为什么需要同时安装它们。如果你无法通过其中一个包来实现这一点，请在 Gentoo 错误报告系统中提交一个漏洞（bug）。

## 屏蔽的包 (Masked Packages)

```
Code Listing 20: Portage 关于屏蔽包的警告
```

```
Code Listing 21: Portage 关于屏蔽包的警告 - 原因

*** 可能的候选者：
满足 'bootstrap' 的 ebuild已被屏蔽。

gnome-base/gnome-2.8.0_re1 (masked: ~86 keyword)
lm-sensors/lm-sensors-2.8 (masked: ~sparc keyword)
sys-libs/glibc-2.34.200800 (masked: ~amd64 keyword)
dev-tools/0.7 (masked: missing keyword)
media-video/at-gophers-4.3.0 (masked)
sys-libs/glibc-2.2.rl (masked: by profile)
```

当你想要安装一个不可用的包时，你将收到此错误。这可能是为了安装一个你的用户可用的不同应用程序，或者等待该包可用。包被屏蔽是有的：

- arch keyword 意味着该应用程序尚未经过充分测试，无法进入稳定分支。等几天时间它们就会回来。

- arch keyword 或 ** keyword 意味着该应用程序在你的架构上无法运行。如果你认为该包运行良好，请在我们的 bugzilla 上提交一个 bug。

- missing keyword 意味着该包尚未在你的架构上安装。让 Portage 团队测试该包，或者如果你在 bugzilla 网站发现了你的报告，请对其进行测试。

- package mask 意味着该包被发现损坏、不稳定或更糟，并被刻意标记为不可用。

- profile mask 意味着该包被发现不适合你的配置。如果你安装它，可能会破坏你的系统，或者它仅与你使用的配置兼容。

## 缺失的依赖 (Missing Dependencies)

```
Code Listing 22: Portage 关于缺失依赖项的警告

emerge: 没有 ebuilds 满足 "=sys-devel/gcc-3.4.2-r4"
```

```
!!! ebuild sys-devel/gcc-3.4.2-r2 问题
!!! 可能是 DEPEND/DEPENDENT 问题。
```

你正尝试安装的应用程序依赖于一个你的系统不可用的另一个包。请检查 bugzilla 查看该问题是否已知，如果没有，请报告它。除非混合分支，否则不应该发生这种情况，因此这是一个 bug。

### 歧义的 Ebuild 名称 (Ambiguous Ebuild Name)

```
Code Listing 23: Portage 关于歧义 ebuild 名称的警告

!!! 短 ebuild "attern" 具有歧义。请指定
!!! 以下一个完全限定的 ebuild 名称：

dev-libs/attern
xll-terms/attern
```

你想要安装的应用程序名称对应于多个包。你需要提供类别名称（category name）。Portage 将通知你供选择的可能匹配项。

```
Code Listing 24: Portage 关于循环依赖的警告

!!! Error: 循环依赖：
ebuild / /net-print/cups-1.11.15-r2 依赖于 ebuild / app-text/ghostscript-7.05.3-r1
ebuild / /app-text/ghostscript-7.05.3-r1 依赖于 ebuild / net-print/cups-1.11.15-r2
```

你想要安装的两个或多个包相互依赖，因此无法安装。这最可能是 Portage 树中的一个 bug。请稍后恢复并重试。你也可以检查 bugzilla。

### Fetch 失败 (Fetch failed)

```
Code Listing 25: Portage 关于获取失败的警告

!!! sys-libs/ncurses 获取失败
!!! 遇到了一些错误。
```

Portage 无法下载源码，失败可能是由于。

### 系统保护 (System Protection)

```
Code Listing 26: Portage 关于保护包的警告

!!! 尝试安装 sys-apps
!!! 遇到了一些错误。
```

该应用程序被发现不适合你的配置。它已被移除。

## 2. USE-flags

### 2a. 什么是 USE-flags？

为了让你理解 USE-flags 的重要性，我们现在将告诉你如何声明 USE-flags。为了方便用户搜索和选择 USE-flags，我们已经提供了默认设置。该设置是 Gentoo 常用的 USE-flags 集合。这在配置中声明。每个配置都在另一个之上，最终结果是所有配置的总和。顶部配置是基础配置 (/usr/portage/profiles/base)。

让我们来看看 2004.3 的默认设置。



```
Code List 1: 2004.3 配置的累积 USE 变量
（此示例是 base, default-linux, default-linux/x86 和 default-linux/x86/2004.3 设置的总和）
use86 oss avx build-fonts ctype encode f77
usekde sdl glip python gnome lib+ matt mad
usemod mikft mreq nis obgovnis opennis pdfrib python
qt quicktime release sdl svga truetype x xml znz xv*)
```

### 2b. 使用 USE-flags

#### 声明 USE-flags

如所示，此变量包含了许多关键词。不要修改任何 `make.files` 来声明符合需求的 `USE` 变量：此文件中的更改将在更新时可见！

要更改此默认设置，你需要向 `USE` 变量添加或移除关键字。这是通过在 `/etc/make.conf` 中全局定义 `USE` 变量来实现。在该变量中，你可以添加额外的 `USE-flags`，或者移除不需要的 `USE-flags`。后者通过在关键字前加上减号 `-` 实现。

例如，为了支持 KDE 和 Qt 添加对 ipad 支持，可以在 `/etc/make.conf` 中定义以下 `USE`：

![](img/c0231913cf632f51d9b75da531c717e6_51_0.png)

有时你只想为某个（或几个）应用程序声明特定的 `USE` flag，而不是全局范围。要实现这一点，你需要创建 `/etc/portage/` 目录（如果不存在）并编辑 `/etc/portage/package.use`。

例如，如果你不想在全局启用 `kerdb` 支持，但想为 `mysql` 启用，你可以执行：

```
Code List 3: /etc/portage.use example

dev-db/mysql kerdb
```

当然，你可以显式地禁用某个应用程序的 `USE` flag。例如，如果你不想在 PHP 中支持 java：

```
Code List 4: /etc/portage/package.use 2nd example

dev-php/php-java-
```

## 声明临时 USE-flags

有时你只想设置一次某个特定的 `USE` 设置。与其编辑两次 `/etc/make.conf`（为了执行和撤销 `USE` 更改），你只需将 `USE` 变量声明为环境变量。记住，当你重新合并或更新此应用程序时（无论是显式地还是作为系统更新的一部分），你的更改将会生效：

例如，我们将在安装 `mozilla` 期间临时从 `USE` 设置中移除 `java`。

```
Code List 5: Using USE as environment variable

USE="-java*" emerge mozilla
```

## 自动 USE Flags

软件包安装后，如果你没有显式禁用，已安装的 `USE` flags 将自动为你启用。要查看带有 flag 的包列表，请检查你的配置中的 `/etc/make.profile.defaults` 和 `use.defaults` 文件。

```
Code List 6: A snippet from /etc/make.profile.defaults

gnome gnome-base/gnome

gtk x11-libs/gtk+

dqt x11-libs/qt

kde kde-base/kdebase

motif x11-libs/motif
```

## 优先级

当然，存在某种优于 `USE` 设置的优先级。你不希望在声明了 `USE="-java"` 后，发现由于某个优先级更高的设置，java 仍然被使用。`USE` 设置按优先级排序（第一个优先级最低）：

1. 配置文件中 `make.defaults` 文件中的默认 `USE` 设置
2. 如果安装了来自 `profile.defaults` 的包，则继承的 `USE` 设置
3. `/etc/make.conf` 中的用户自定义 `USE` 设置
4. `/etc/portage/package.use` 中的用户自定义 `USE` 设置
5. 环境变量中的 `USE` 设置

要查看 Portage 看到的最终 `USE` 设置，运行 `emerge --info`。这将列出所有相关变量（包括 `USE` 变量）以及 Portage 所使用的内容。

```
Code List 7: Running emerge --info

# emerge --info
```

## 使你的系统适配新的 USE Flags

如果你更改了 `USE` flags 并希望更新整个系统以使用新的 `USE` flags，请使用 `--newuse` 选项：

```
### Code Listing 8: Rebuilding your entire system

# emerge --update --deep --newuse
```

接下来，运行 Portage 的 `declean` 来移除在你的“旧”系统上合并、但已由于新的 `USE` flags 变得过时的条件依赖。

**警告：** 运行 `emerge --depclean` 是一个危险的操作，应该小心处理。双重检查提供的“过时”包列表，以确保不会删除你需要的包。在接后的示例中，我们为 `declean` 添加了 `-p` 选项，仅列出包而不删除它们。

```
### Code Listing 9: Removing obsolete packages

# emerge --depclean
```

当 `declean` 完成后，运行 `revdev-rebuild` 来重新构建与可能被移除的包提供的共享对象动态链接的应用程序。`revdev-rebuild` 是 `gentoolkit` 包的一部分；不要忘记安装它。

```
### Code Listing 10: Running revdev-rebuild

# revdev-rebuild
```

完成完成后，你的系统将使用新的 `USE` flag 设置。

### 2.c. 特定包的 USE-flags

**查看可用的 USE-flags**

让我们以 `mozilla` 为例：它监听哪些 `USE-flags`？要找到答案，我们使用 `--pretend` 和 `--verbose` 选项进行合并：

```
### Code Listing 11: Using the used USE-flags

# emerge --pretend --verbose mozilla

These are the packages that I would merge, in order:

Calculating dependencies ...done

[build] R //www/mozilla-1.7.2-2 USE='crypt gnome java mozsvg ssl

truetype xtprint -xdap -ipv6 -lapad mozcalendar -mozdevel -nozcompose

nozoirc -moznall -nozoft -postgres -xineama 0 KB
```

`emerge` 不是完成此项工作的唯一工具。事实上，我们有一个专门查询包信息的工具称为 `query`，它位于 `gentoolkit` 包中。首先，安装 `gentoolkit`：

```
### Code Listing 12: Installing gentoolkit

# emerge gentoolkit
```

现在运行参数来查看特定包的 `USE-flags`。例如，对于 `gnumeric` 包：

```
### Code Listing 13: Using query to view used USE-flags

# query use gnumeric

[ Colour : set theme ]

[ Legend

- (U) Col 1 Current USE flags

 (I) Col 2 Installed with USE flags ]
```

```
U I [ Found these variables in : app-office/numeric-1.2

libda : Adds Data Access (CORBA wrapper) support for gnumeric

gomedeb : unknown

+ + python : support/bindings for the Python language

+ + bonobo : Adds support for gnome-base/bonobo (Gnome CORBA interfaces)
```



## 3. Portage Features

### 3.a. Portage Features

Portage 有一些额外功能，可以让 Gentoo 体验更好。这些功能许多依赖软件工具来提高性能、安全性。要启用或禁用 Portage 功能，可以编辑 `/etc/make.conf` 中的 `FEATURES` 变量，关键词之间用空格分隔。在某些情况下，还需要安装额外的工具包含该功能。并不是所有 Portage 功能都列在这里。概述请参阅 `make.conf` 页面：

```
$ man make.conf
```

要找出默认的 `FEATURES`，运行 `emerge --info` 并搜索 `FEATURES`：

```
$ emerge --info | grep FEATURES
```

### 3.b. Distributing Compiling

**使用 `distcc`**

`distcc` 是一个在网络上几台并不相同的机器上分配编译的程序。`distcc` 将所有必要信息发送到可用的 `distcc` 服务器来为客户端编译源码。结果是编译速度更快。关于 `distcc` 的更多信息（以及如何在 Gentoo 中使用它）可以查看 `distcc` 文档。

**安装 `distcc`**

`distcc` 带有一个图形监控器来跟踪你的计算机何时发送编译。如果你使用 Gnome，请在 `USE` 变量中放入 `gnome`。但如果你使用 Gnome 并且想要，你应该放入 `gtk`。

```
# emerge distcc
```

**激活 Portage Support**

在 `/etc/make.conf` 的 `FEATURES` 变量中添加此项。接下来，根据喜好编辑 `MAKEOPTS`。一个已知指南是用 `-X` 填写运行 `distcc` 的 CPU 数量（包括当前主机），但其他数字可能有更好的结果。现在运行 `distcc` 并输入可用的 `distcc` 服务器列表：192.168.102（当前主机）、192.168.103 和 192.168.104（“远程”主机）：

```
# distcc-config --set-hosts "192.168.102 192.168.103 192.168.104"
```

别忘了也运行 `distccd` 守护进程：

```
# rc-update add distccd default
# /etc/init.d/distccd start
```

### 3.c. Caching Compilation

**关于 `ccache`**

`ccache` 是快速编译器缓存。当你编译程序时，它会缓存中间结果，因此当你重新编译程序时，编译时间会大大缩短。在常见的编译中，这可以快 5 到 10 倍。如果你对 `ccache` 的内部机制感兴趣，请访问 ccache 首页。

**安装 `ccache`**

要安装 `ccache`，运行 `emerge ccache`：

```
# emerge ccache
```

**激活 Portage Support**

打开 `/etc/make.conf` 在 `FEATURES` 变量中添加 `ccache`。接下来，添加一个名为 `CCCACHE_SIZE` 的新变量并设置为 `"2G"`：

```
CCACHE_SIZE="2G"
```

要检查 `ccache` 是否运行，让 `ccache` 提供它的统计数据。由于 Portage 使用不同的 `ccache` 主目录，你需要设置 `CCACHE_DIR` 变量为：

```
# CCACHE_DIR=/var/tmp/ccache ccache -s
```

`/var/tmp/ccache` 是 Portage 默认的主目录；如果你想更改它，可以在 `/etc/make.conf` 中设置 `CCACHE_DIR`。但是，如果你运行它，它将使用默认位置 `${HOME}/.ccache`，这就是为什么在请求（Portage）缓存统计时需要设置 `CCACHE_DIR` 变量。

**使用 `ccache` 进行非 Portage 编译**

如果你想为非 Portage 编译使用 `ccache` 请将 `/usr/lib/ccache/bin` 添加到 `PATH` 变量的开头（在 `/usr/bin` 之前）。这可以通过编辑 `/etc/env/d00base` 实现，它是定义 `PATH` 变量的环境文件：

```
PATH="/usr/lib/ccache/bin:/opt/*
```

### 3.d. Binary Package Support

**创建 Prepackages**

Portage 支持安装预编译包（preprint packages）。尽管 Gentoo 本身不提供预编译包（GRP 快照外），但可以让 Portage 完全感知预编译包。

要创建预编译包，如果包已安装在你的系统中，可以使用 `quickpkg`，或者使用 `--buildpkg` 或 `--buildpkg-only` 选项。

如果你想为每次安装创建预编译包，请将 `buildpkg` 添加到 `FEATURES` 变量中。

可以通过 Catalyst 获取更多创建预编译包集的支持。有关 Catalyst 的更多信息，请参阅 Catalyst 参考手册和 Catalyst 常见问题。

**安装 Prepackages**

虽然 Gentoo 不提供，但你可以创建一个用于存储预编译包的仓库。如果你想使用该仓库，你需要通过让 `PORTAGE_BINHOST` 变量指向它来让 Portage 感知。例如，如果预编译包在

`ftp://buildhost/gentoo:`

```
PORTAGE_BINHOST="ftp://buildhost/gentoo"
```

当你想要安装预编译包时，可以使用 `emerge` 命令的 `--binpkg` 选项配合 `--usepkg` 选项。前者告诉 `emerge` 从定义的服务器下载预编译包，而后者要求 `emerge` 在获取源码并编译之前先安装预编译包。

例如，使用预编译包安装 gnumeric：

```
# emerge --usepkg --binpkg gnumeric
```

关于 `emerge` 预编译选项的更多信息可以在管理书中找到：

```
$ man emerge
```



# 4. Init 级别

## 4.a. Runlevels

### 启动你的系统
当你启动系统时，你会看到大量的文本闪过。如果你仔细观察，你会发现这些文本在每次重启系统时都是相同的。所有操作的序列被称为启动序列，并且是（在多程度上）静态定义的。

首先，你的引导程序会在告诉 CPU 运行内核后，会将你在引导程序配置中定义的内核加载到内存中。当内核加载并运行时，它会初始化所有内核特定的结构和任务，并启动 `init` 进程。

该进程确保所有文件系统（在 `/etc/fstab` 中）都已挂载并准备就绪。然后，它会执行位于 `/etc/initd/` 中的若干脚本，这些脚本将启动你所需的服务以成功启动系统。

最后，当所有脚本执行完毕后，它会激活终端（大多数情况下是隐藏在 Alt-F1、Alt-F2... 下方的虚拟控制台），并附加一个名为 `getty` 的特殊进程。该进程将通过运行 `login` 来确保你能够登录这些终端。

### Init 脚本
现在 `init` 仅执行 `/etc/initd.random` 中的脚本。即使它并不会运行 `/etc/initd.d` 中的所有脚本，只运行被指示执行的脚本。它通过查看 `/etc/runlevels` 来决定执行哪些脚本。

首先，`init` 运行 `/etc/initd/` 中在 `/etc/runlevel/root` 内有符号链接的所有脚本。通常，它会按字母顺序启动脚本，但某些脚本内部包含依赖信息，告诉系统在启动它们之前必须运行另一个脚本。

当所有引用 `/runlevel/default` 的脚本执行完毕后，它将继续运行包含相应符号链接的脚本。

### Init 如何工作
`init` 并不是由自己决定的。它需要一个配置文件来指定需要采取哪些操作。该配置文件位于 `/etc/initab`。

如果你记得我们刚刚描述的启动序列，你就会记得 `init` 的第一个动作是挂载所有文件系统。这定义在 `/etc/initab` 的以下行中：

```
Code List 1: /etc/initab 中的系统初始化
```

```
si:sysinit:/sbin/init.d rc sysinit
```

这一行告诉它必须运行 `/sbin/rcinit` 来初始化系统。`/sbin/rc` 脚本负责初始化，所以你可以说 `init` 并没有做什么——它将初始化系统的任务委给了另一个进程。

其次，`init` 执行了所有在 `/etc/runlevels/boot` 中有符号链接的脚本。这定义在以下行中：

```
Code Listing 2: 系统初始化继续
```

```
rc::boot:sbin/rc boot
```

同样，`rc` 脚本执行了必要的任务。传递给 `rc (boot)` 的选项与使用的 `/etc/runlevels` 子目录相同。

现在 `init` 检查它的配置文件以查看应该运行哪个 runlevel。为了决定这一点，它从 `/etc/initab` 读取以下几行：

```
Code Listing 3: 无限行
```

```
id3:initdefault:
```

在这种情况下（大多数 Gentoo 用户都会使用的），3。使用这些信息，`init` 检查它在 runlevel 3 下必须运行的内容：

```
Code Listing 4: runlevel 定义
```

```
10:0:wait;/sbin/rc shutdown tty1 linux
11:0:wait;/sbin/rc single tty2 linux
12:0:wait;/sbin/rc nonwork tty3 linux
13:0:wait;/sbin/rc default tty4 linux
14:0:wait;/sbin/rc default tty5 linux
15:0:wait;/sbin/rc default tty6 linux
16:0:wait;/sbin/rc reboot
```

该行定义了 3，再次使用 `rc` 脚本启动服务（现在参数为 `default`）。再次注意，`rc` 的参数与来自 `/etc/runlevels` 的子目录相同。

当 `rc` 完成后，`init` 决定激活哪些虚拟控制台，以及每个控制台需要运行哪些命令：

```
Code Listing 5: 虚拟控制台定义
```

```
c1:2345:respawn;/sbin/agetty 38400 tty1 linux
c2:12345:respawn;/sbin/agetty 38400 tty2 linux
c3:12345:respawn;/sbin/agetty 38400 tty3 linux
c4:12345:respawn;/sbin/agetty 38400 tty4 linux
c5:12345:respawn;/sbin/agetty 38400 tty5 linux
c6:12345:respawn;/sbin/agetty 38400 tty6 linux
```

### 什么是 runlevel？
runlevel 是系统运行的状态。在 Gentoo 中，有四种 runlevel：`boot`、`default`、`single` 和 `shutdown`。内部 runlevel 是 `boot` 和 `shutdown`。用户定义的 runlevel 是列在 `/etc/runlevels` 中的那些。每个 runlevel 定义了一组要启动的服务。例如，`default` runlevel 用于普通多用户操作，而 `single` runlevel 用于维护。

## 添加和移除服务

在安装 Gentoo 期间，你已经向“default”（默认）运行级别（runlevel）添加了初始化脚本。当时你可能不知道“default”是做什么的，但现在你应该已经了。`rc-update` 脚本需要第二个参数来定义操作：`add`（添加）、`del`（删除）或 `show`（显示）。

要添加或删除初始化脚本，只需更新 `add` 或 `del` 参数，后跟初始化脚本和运行级别即可。例如：

> 代码列表 13：从默认运行级别中移除 Postfix

```
# rc-update del postfix default
```

`rc-update` 命令将显示所有可用的脚本并列出它们执行的运行级别。

> 代码列表 14：获取初始化脚本信息

```
# rc-update show
```

## 4.c. 配置服务

### 为什么需要额外配置？
初始化脚本可能非常复杂。因此，不希望用户直接编辑初始化脚本，因为这会增加出错的概率。能够配置此类服务是非常重要的。例如，你可能想为服务本身提供更多选项。

将配置放在初始化脚本之外的第二个原因是：在更新初始化脚本时，无需担心你的配置会被重置。

### etc/conf.d 目录
Gentoo 提供了一种简单的方法来配置此类服务：每个可以配置的初始化脚本在 `/etc/conf.d` 中都有一个文件。例如，`apache2` 初始化脚本（路径为 `/etc/init.d/apache2`）有一个配置文件 `/etc/conf.d/apache2`，其中可以包含你在启动 Apache 2 时想要提供给它的选项：

> 代码列表 15：在 /etc/conf.d/apache2 中定义的变量

```
APACHE_OPTS="-D PHP*"
```

此类配置文件仅包含变量（类似于 `/etc/make.conf`），这使得配置此类服务变得非常容易。它还允许我们通过注释为变量提供更多关于变量的信息。

## 4.d. 编写初始化脚本

### 我必须写吗？
通常不需要编写任何内容，因为 Gentoo 为所有提供的服务都提供了现现用的初始化脚本。但是，你可能没有使用 Portage 安装了某个服务，在这种情况下，你可能需要创建一个初始化脚本。

如果服务提供的初始化脚本不是显式为 Gentoo 编写的，请不要使用它：Gentoo 的初始化脚本与其他发行版所使用的初始化脚本是不兼容的！

### 布局
初始化脚本的基本布局所示。

> 代码列表 16：初始化脚本的基本布局

```
#!/bin/runscript

depend() {

  (依赖信息)

}

start() {

  (启动服务所需的命令)

}
```

```
stop() {

  (停止服务所需的命令)

}

start() {

  (重启服务所需的命令)

}
```



任何初始化脚本都要求定义 `start()` 函数。所有其他部分都是可选的。

### 依赖关系

你可以使用两种依赖：`need` 和 `after`。正如我们之前提到的，`need` 依赖比 `after` 依赖更严格。遵循这种依赖类型时，输入你所依赖的服务或虚拟依赖（virtual dependency）。

虚拟依赖是由某个服务提供的，但并非由该服务唯一提供。你的初始化脚本可以依赖于系统日志程序，但有很多系统日志程序可用（metalog, syslog-ng, syslog, ...）：由于你无法需要它们中的每一个（没有哪个合理的系统会安装并运行所有这些系统），我们确保所有这些服务都提供虚拟依赖。

让我们来看 postfix 服务的依赖信息。

![](img/c0231913cf632f51d9b75da531c717e6_60_0.png)

```
depend() {

  need net

  use logger dns

  provide mta

}
```

如你所见，postfix 服务：

- 需要（虚拟）`net` 依赖（例如由 `/etc/init.d/net.0` 提供）
- 使用（虚拟）`logger` 依赖（例如由 `/etc/init.d/syslog-ng` 提供）
- 使用（虚拟）`dns` 依赖（例如由 `/etc/init.d/named` 提供）
- 提供（虚拟）`mta` 依赖（这对所有邮件服务器都是常见的）

### 控制顺序

在某些情况下，你可能需要某个服务，但如果该服务在系统可用，你希望你的服务在另一个服务之前（或之后）启动（注意条件 - `need` 依赖），并且在同一个运行级别中运行（注意条件 - 仅涉及相同运行级别中的服务）。你可以使用 `before` 或 `after` 设置来提供此类信息。

例如，我们查看 postfix 服务的设置：

![](img/c0231913cf632f51d9b75da531c717e6_60_1.png)

```
depend() {

  need net

  before inet

  before xinetd

}
```

你可以使用 `*` 通配符来捕获相同运行级别的所有服务，尽管不建议这样做。

![](img/c0231913cf632f51d9b75da531c717e6_60_2.png)

```
depend() {

  before *

}
```

### 标准函数

除了 `depend()` 功能外，你还需要定义 `start()` 函数。它包含了所有初始化命令。使用 `ebegin` 和 `end` 函数可以告知用户正在发生什么。![](img/c0231913cf632f51d9b75da531c717e6_60_3)

```
start() {

  ebegin "Starting my_service"

  # (启动服务的命令)

  end

}
```

如果服务提供的初始化脚本不是显式为 Gentoo 编写的，请不要使用它：Gentoo 的初始化脚本与其他发行版所使用的初始化脚本是不兼容的！

许多用户（尤其是刚接触 Linux 的用户）会觉得这有点奇怪或难以管理。然而，这是一个错误的想法：使用环境变量可以轻松更改一个或多个应用程序的配置设置。

例如，你可能想为服务本身提供更多选项。

将配置放在初始化脚本之外的第二个原因是：在更新初始化脚本时，无需担心你的配置会被重置。

### etc/conf.d 目录

Gentoo 提供了一种简单的方法来配置此类服务：每个可以配置的初始化脚本在 `/etc/conf.d` 中都有一个文件。例如，`apache2` 初始化脚本（路径为 `/etc/init.d/apache2`）有一个配置文件 `/etc/conf.d/apache2`，其中可以包含你在启动 Apache 2 时想要提供给它的选项：

> 代码列表 15：在 /etc/conf.d/apache2 中定义的变量

```
APACHE_OPTS="-D PHP*"
```

此类配置文件仅包含变量（类似于 `/etc/make.conf`），这使得配置此类服务变得非常容易。它允许我们通过注释为变量提供更多关于变量的信息。

## 4.d. 编写初始化脚本

### 我必须写吗？

通常不需要编写任何内容，因为 Gentoo 为所有提供的服务都提供了现成的初始化脚本。但是，你可能没有使用 Portage 安装了某个服务，在这种情况下，你可能需要创建一个初始化脚本。

如果服务提供的初始化脚本不是显式为 Gentoo 编写的，请不要使用它：Gentoo 的初始化脚本与其他发行版所使用的初始化脚本是不兼容的！

### 布局

初始化脚本的基本布局所示。

> 代码列表 16：初始化脚本的基本布局

任何初始化脚本都要求定义 `start()` 函数。所有其他部分都是可选的。

## 添加和移除服务

在安装 Gentoo 期间，你已经向“default”运行级别（runlevel）添加了初始化脚本。当时你可能不知道“default”是做什么的，但现在你应该已经了。`rc-update` 脚本需要第二个参数来定义操作：`add`（添加）、`del`（删除）或 `show`（显示）。

要添加或删除初始化脚本，只需更新 `add` 或 `del` 参数，后跟初始化脚本和运行级别即可。例如：

> 代码列表 13：从默认运行级别中移除 Postfix

```
# rc-update del postfix default
```



`rc-update` 命令将显示所有可用的脚本并列出它们执行的运行级别。

> 代码列表 14：获取初始化脚本信息

```bash
# rc-update show
```

## 4.c. 配置服务

### 为什么需要额外配置？

初始化脚本可能非常复杂。因此，不希望用户直接编辑初始化脚本，因为这会增加出错的概率。能够配置此类服务是非常重要的。例如，你可能想为服务本身提供更多选项。

将配置放在初始化脚本之外的第二个原因是：在更新初始化脚本时，无需担心你的配置会被重置。

### etc/conf.d 目录

Gentoo 提供了一种简单的方法来配置此类服务：每个可以配置的初始化脚本在 `/etc/conf.d` 中都有一个文件。例如，`apache2` 初始化脚本（路径为 `/etc/init.d/apache2`）有一个配置文件 `/etc/conf.d/apache2`，其中可以包含你在启动 Apache 2 时想要提供给它的选项：

> 代码列表 15：在 `/etc/conf.d/apache2` 中定义的变量

```bash
APACHE_OPTS="-D PHP*"
```

此类配置文件仅包含变量（类似于 `/etc/make.conf`），这使得配置此类服务变得非常容易。它允许我们通过注释为变量提供更多关于变量的信息。

## 4.d. 编写初始化脚本

### 我必须写吗？

通常不需要编写任何内容，因为 Gentoo 为所有提供的服务都提供了现成的初始化脚本。但是，你可能没有使用 Portage 安装了某个服务，在这种情况下，你可能需要创建一个初始化脚本。

如果服务提供的初始化脚本不是显式为 Gentoo 编写的，请不要使用它：Gentoo 的初始化脚本与其他发行版所使用的初始化脚本是不兼容的！

### 布局

初始化脚本的基本布局所示。

> 代码列表 16：初始化脚本的基本布局

```bash
#!/bin/runscript

depend() {

  (依赖信息)

}

start() {

  (启动服务所需的命令)

}
```

```bash
stop() {

  (停止服务所需的命令)

}

start() {

  (重启服务所需的命令)

}
```

任何初始化脚本都要求定义 `start()` 函数。所有其他部分都是可选的。

### 依赖关系

你可以使用两种依赖：`need` 和 `after`。正如我们之前提到的，`need` 依赖比 `after` 依赖更严格。遵循这种依赖类型时，输入你所依赖的服务或虚拟依赖。

虚拟依赖是由某个服务提供的，但并非由该服务唯一提供。你的初始化脚本可以依赖于系统日志程序，但有很多系统日志程序可用（metalog, syslog-ng, syslog, ...）：由于你无法需要它们中的每一个（没有哪个合理的系统会安装并运行所有这些系统），我们确保所有这些服务都提供虚拟依赖。

让我们来看 postfix 服务的依赖信息。

![](img/c0231913cf632f51d9b75da531c717e6_60_0.png)

```bash
depend() {
  need net
  use logger dns
  provide mta
}
```

如你所见，postfix 服务：

- 需要（虚拟）`net` 依赖（例如由 `/etc/init.d/net.0` 提供）
- 使用（虚拟）`logger` 依赖（例如由 `/etc/init.d/syslog-ng` 提供）
- 使用（虚拟）`dns` 依赖（例如由 `/etc/init.d/named` 提供）
- 提供（虚拟）`mta` 依赖（这对所有邮件服务器都是常见的）

### 控制顺序

在某些情况下，你可能需要某个服务，但如果该服务在系统可用，你希望你的服务在另一个服务之前（或之后）启动（注意条件 - `need` 依赖），并且在同一个运行级别中运行（注意条件 - 仅涉及相同运行级别中的服务）。你可以使用 `before` 或 `after` 设置来提供此类信息。

例如，我们查看 postfix 服务的设置：

![](img/c0231913cf632f51d9b75da531c717e6_60_1.png)

```bash
depend() {
  need net
  before inet
  before xinetd
}
```

你可以使用 `*` 通配符来捕获相同运行级别的所有服务，尽管不建议这样做。

![](img/c0231913cf632f51d9b75da531c717e6_60_2.png)

```bash
depend() {
  before *
}
```

### 标准函数

除了 `depend()` 功能外，你还需要定义 `start()` 函数。它包含了所有初始化命令。使用 `ebegin` 和 `end` 函数可以告知用户正在发生什么。![](img/c0231913cf632f51d9b75da531c717e6_60_3)

```bash
start() {
  ebegin "Starting my_service"
  # (启动服务的命令)
  end
}
```

## 5. 环境变量

## 5.a. 环境变量？

### 它们是什么

环境变量是一个命名对象，包含一个或多个应用程序使用的信息。许多用户（尤其是刚接触 Linux 的用户）会觉得这有点奇怪或难以管理。然而，这是一个错误的想法：使用环境变量可以轻松更改一个或多个应用程序的配置设置。

### /etc/envd 目录

为了集中管理这些变量，Gentoo 引入了 `/etc/envd` 目录。在该目录下，你会发现许多文件，例如 `0basic`、`05gcc` 等，它们包含了名称中提到的应用程序所需的所需的变量。

例如，当你安装 gcc 时，ebuild 会创建一个名为 `05gcc` 的文件，其中包含了以下变量的定义：

## 代码列表 2: `/etc/envd/05gcc`

```bash
PATH=/usr/x86_64-pc-linux-gnu/gcc-bin/3.2*
ROOTPATH=/usr/x86_64-pc-linux-gnu/gcc-bin/3.2*
MANPATH=/usr/share/gcc/data-i686-pc-linux-gnu/3.2/man*
INFOPATH=/usr/share/gcc/data-i686-pc-linux-gnu/3.2/info*
CC=*cc.cache
XX*=
LDPATH=/usr/lib/gcc/i686-pc-linux-gnu/3.2.3*
```

其他发行版允许你在 `/etc/profile` 或其他位置更改或添加环境变量。相比之下，Gentoo 让你让你（或 Portage）能够轻松地维护和管理环境变量，而无需关注可能包含环境变量的众多文件。

例如，当 gcc 更新时，`/etc/envd/05gcc` 文件会自动更新，而无需任何用户交互。偶尔，你可能会被要求在系统范围内设置某个环境变量。以 `http_proxy` 变量为例，你现在不需要去改动 `/etc/profile`，而是可以创建一个文件（`/etc/envd/99local`）并并在其中输入你的定义：

## 代码列表 3: `/etc/envd/99local`

```bash
http_proxy="proxy.server.com:8080*"
```

通过使用该文件管理所有变量，你可以快速概览你自行定义的变量。

### env-update 脚本

`/etc/envd` 中的几个文件定义了 `PATH` 变量。这并不是错误：当你运行 `env-update` 时，它会在更新环境变量之前追加这几个定义，使得软件包（或用户）可以方便地添加自己的环境变量设置，而不会干扰现有的文件。

`env-update` 脚本将按照 `/etc/envd` 中文件的字母顺序追加变量。这些文件必须以两个数字开头。

## 代码列表 4: 通过 `env-update` 更新环境变量

| 00basic | 99k-env | 99local |
| :--- | :--- | :--- |
| `PATH=/usr/bin:/usr/lib/3.2/bin:/usr/local/bin*` | | |

变量的合并并不总是发生，以下变量例外：`KEDIRS`, `PATHCLASS`, `LDPATH`, `MANIPATH`, `INFOPATH`, `ROOTPATH`, `CONFIG_PROTECT`, `CONFIG_MASK`, `PRELINK_PATH` 和 `PRELINK`, `MASK`。仅使用最后一个定义的值（按照 `/etc/envd` 的字母顺序）。

当你运行 `env-update` 时，脚本将创建所有环境变量并将它们放置在 `/etc/profile` 中（由 `/etc/` 使用）。它将从 `LDPATH` 变量中提取信息并用它来创建 `/etc/ld.so.cache`。之后，你将运行 `ldconfig` 来重新创建动态链接器使用的 `/etc/ld.so` 文件。

如果你想在运行 `env-update` 后立即看到效果，请执行以下命令来更新你的环境。安装过 Gentoo 的用户可能在安装说明中记得这一点。

## 代码列表 5: 更新环境

```bash
```



`env-update --all source /etc/profile`

注意：上面的命令仅更新你当前终端、新控制台及其子控制台中的变量。因此，如果你在 X11 中工作，你需要在每个新终端中输入 `source /etc/profile` 或重启 X，因为所有新的源变量都将被使用。如果你使用登录管理器，请切换到 root 并输入 `/etc/init.d/xdm restart`。如果不是，你需要注销并重新登录，以便让 X 派生带有新变量的子进程。

## 5.c. 在本地定义变量

### 用户特定

你不需要全局定义一个环境变量。例如，你可能想将 `/home/my_user/bin` 和工作目录（你所在的目录）添加到 `PATH` 变量中，但你不希望系统中的所有其他用户在他们的 `PATH` 中也包含这些。如果你想在本地定义环境变量，应该使用 `~/.bashrc` 或 `~/.bash_profile`：

#### 代码列表 6: 在 `~/.bashrc` 中为本地使用扩展 PATH

```bash
# 冒号后如果没有目录则被视为当前工作目录

PATH=$PATH:/home/my_user/bin;
```

重新登录后，你的 `PATH` 变量将得到更新。

### 会话特定

有时需要更严格的定义。你可能希望使用你创建的临时目录中的二进制文件，而无需将该路径添加到二进制路径中或在需要的短时间内编辑 `~/.bashrc`。

在这种情况下，你可以通过 `export` 命令在当前会话中定义 `PATH`。由于你没有注销，`PATH` 变量将由临时设置修改。

#### 代码列表 7: 定义会话特定的环境变量

```bash
export PATH=$PATH:/home/my_user/tmp/usr/bin*
```

## C. 与 Portage 工作

### 1.a. 文件与目录

#### 配置

Portage 自带默认位置。当你查看它时，你会发现所有的。本章解释了特殊位置。如果你需要100%的覆盖，请参考 Portage 页面：

#### 代码列表 1: 阅读 Portage

```bash
$portage
```

### 1.b. 存储文件

#### Portage 树

Portage 树的位置是 `/usr/portage`。这由 `PORTDIR` 变量定义。当你将 Portage 树存储在其他处时（更改此变量），记得相应地更改 `/etc/profile`。

如果你更改了 `PORTDIR` 变量，你可能还需要更改以下变量，它们不会感知 `PORTDIR` 的变化。这是由于。

#### 预编译二进制文件

即使 Portage 默认不使用预编译二进制文件，它也有支持。当你要求 Portage 处理预编译包时，它会在 `/etc/packages` 中查找。该位置由 `PKGDIR` 变量定义。

#### 源代码

源代码默认存储在 `/etc/dist`。该位置由 `DISTDIR` 变量定义。

#### RPM 文件

即使 Portage 不能使用 RPM 文件，它也能通过 `ebuild` 命令生成。存储 RPM 文件的默认位置是 `/etc/rpm`，这由 `RMPDIR` 变量定义。

#### Portage 数据库

Portage 将状态存储在 `/var/db/pkg`（哪些文件属于哪个包）。不要手动修改这些文件！这可能会破坏 Portage 对系统的认知。

#### Portage 缓存

Portage 缓存（修改时间、虚拟、依赖树等）存储在 `/var/cache/edb`。该位置是一个缓存：在你没有运行任何 portage 相关应用程序时，可以清理它。

### 配置特定的配置

#### 信息

配置特定的信息包含在 `/etc/profile` 中。之前提到的配置可以通过 `/etc/profile` 进行更改。这是因为许多 Portage 使用配置。

#### 用户特定配置

用户特定配置通过 `/etc/profile` 处理。在 `/etc/profile` 中你可以找到：

- `package.mask`: 你想要屏蔽的包
- `package.unmask`: 你想要取消屏蔽的包
- `package.keywords`: 你想要关键词的包
- `package.use`: 你想要使用的标记
- `package.local`: 本地覆盖

### 2. 编译软件

#### Portage 临时文件

Portage 的临时文件默认存储在 `/var/tmp`。这由 `PORTAGE_TMPDIR` 变量定义。要更改此，你可以在 `/etc/profile` 中设置该变量。

如果你设置了 `PORTAGE_TMPDIR`，你可能也想要修改以下变量，因为它们不会感知到 `PORTAGE_TMPDIR` 的变化。这是由于 Portage 处理变量的方式：`BUILD_PREFIX`。

#### 编译目录

Portage 为每个嵌入在 `/var/tmp/portage` 下的包创建特定的编译目录。该位置由 `BUILD_PREFIX` 变量定义。

#### Live文件系统位置

默认情况下，Portage 将所有文件安装在当前文件系统（`/`）上，你可以通过设置 `ROOT` 环境变量来更改。这在你想要构建镜像时非常有用。

### 1.d. 日志功能

#### Ebuild 日志

Portage 可以创建重新编译日志（re-ebuild logs），但只有当 `PORT_LOGDIR` 变量被设置为 Portage（postage 用户）可写的位置时才有效。默认情况下该变量未设置。

## 2. 配置变量

### 2.a. Portage 配置

如所述，Portage 可以通过许多变量进行配置，你应该在 `/etc/make.conf` 中定义这些变量。请参阅 `make.conf` 手页以获取更完整的信息：

![](img/c0231913cf632f51d9b75da531c717e6_66_0.png)

```bash
$ man make.conf
```

### 2.b. 编译特定选项

#### 配置和编译器选项

当 Portage 编译时，它会将以下定义的编译器标志传递给编译器和配置脚本：

- `CFLAG` 和 `CXXFLAGS` 标志用于 C 和 C++ 编译。
- `CHOST` 定义了应用程序的 `configure` 脚本所需的主机信息。
- `MAKEOPTS` 被传递给 `make` 命令，通常用于定义编译期间的并行度。关于 `make` 选项的更多信息可以查阅 `make` 手页。

`USE` 变量在配置和编译期间的使用已在前面的章节中进行了非常详细解释。

#### 合并选项

当 Portage 合并（merge）某个软件的新版本时，它将从你的系统中删除旧版本的过时文件。Portage 在合并旧版本之前会提供 5 秒延迟。这 5 秒由 `CLEAN_DELAY` 变量定义。

### 2.c. 配置文件保护

#### Portage 的保护位置

如果软件新版本的文件未存储在保护位置中，Portage 将会覆盖（overlay）这些文件。这些保护位置由 `CONFIG_PROTECT` 变量定义，通常是配置文件的所在位置。目录列表由空格分隔。

写入此类保护位置的文件将被重命名，并会警告用户存在该（假设是推测的）配置文件的新版本。

你可以通过 `emerge --info` 的输出获取当前的 `CONFIG_PROTECT` 设置：

![](img/c0231913cf632f51d9b75da531c717e6_66_1.png)

```bash
$ emerge --info | grep 'CONFIG_PROTECT='
```

关于 Portage 配置文件保护的更多信息可以通过 `emerge` 获取：

# 代码列表 3：关于配置文件保护的更多信息

```bash
$ emerge --help config
```

#### 排除目录

要对保护位置的某些子目录进行“取消保护”，你可以使用 `CONFIG_PROTECT_MASK` 变量。

### 2.d. 下载选项

#### 服务器位置

当系统上没有请求的信息或数据时，Portage 将从互联网检索它们。各种信息和数据通道的服务器位置由以下变量定义：

- `GENTOO_MIRRORS` 定义了包含源码（distifles）的位置列表。
- `PORTAGE_BINHOS` 定义了包含你系统预编译包的特定位置。

第三个设置涉及你更新 Portage 树时使用的 rsync 服务器位置：

- `SYNC_MIRRORS` 和 `SYNC` 变量可以由 `mirrorselect` 自动设置。你需要在使用它之前合并 `mirrorselect`。更多信息请参见 `mirrorselect` 的在线帮助：

# 代码列表 4：关于 mirrorselect 的更多信息

```bash
$ emerge --help
```



当请求的信息或数据在你的系统中不可用时，Portage 将从互联网检索它们。各种信息和数据通道的服务器位置由以下变量定义：

- `GENTOO_MIRRORS` 定义了包含源码（distifles）的位置列表。
- `PORTAGE_BINHOS` 定义了包含你系统预编译包的特定位置。

第三个设置涉及你更新 Portage 树时使用的 rsync 服务器位置：

- `SYNC_MIRRORS` 和 `SYNC` 变量可以由 `mirrorselect` 自动设置。你需要在使用它之前合并 `mirrorselect`。更多信息请参见 `mirrorselect` 的在线帮助：

# 代码列表 4：关于 mirrorselect 的更多信息

```
$ emerge --help
```

#### 获取命令

Portage 能够恢复下载的文件。它默认使用 `wget`。

如果你想使用来自测试分支的特定软件版本，但不希望 Portage 对后续版本使用测试分支，你可以在 `package.keywords` 文件中添加版本。在这种情况下，你必须使用 `=` 运算符。你也可以使用 `<` 使用版本范围。

写入此类保护位置的文件将被重命名，并会警告用户存在该（假设是推测的）配置文件的新版本。

你可以通过 `emerge --info` 的输出获取当前的 `CONFIG_PROTECT` 设置：

```
$ emerge --info | grep 'CONFIG_PROTECT='
```

### 2.f. Portage 行为

#### 资源管理

通过 `PORTAGE_NICENESS` 变量你可以增加或降低 nice 值。

#### 输出行为

`NOCOLOR` 变量默认为 "false"，定义了 Portage 是否禁用彩色输出。

## 3. 混合分支

### 3.a. 使用单一分支

#### 稳定分支

`ACCEPT_KEYWORDS` 变量定义了你使用的软件分支。它默认对你的架构使用稳定分支。

我们建议只使用稳定分支。然而，如果你并不在意稳定性并且想通过向 http://bugs.gentoo.org 提交报告来帮助 Gentoo。

#### 测试分支

如果你想使用更多软件，可以考虑使用测试分支。让 Portage 使用测试分支，在你的中。如果一个包处于测试状态，意味着开发者认为它是功能正常的但尚未经过充分测试。你可能是第一个发现软件包漏洞的人，此时你可以提交报告。

但请注意，可能会遇到稳定性问题、打包不完善（例如错误/缺失依赖）、频繁更新（导致大量编译）或损坏软件包。如果你不熟悉 Gentoo 以及如何解决问题，我们建议你坚持稳定分支。

例如，为 x86 架构选择测试分支，编辑 `/etc/make.conf` 并：

```
代码列表 1：设置 ACCEPT_KEYWORDS 变量

ACCEPT_KEYWORDS="x86"
```

如果你现在更新系统，你会发现许多软件包将被更新。请记住：当你使用测试分支更新系统后，没有简单的方法可以回到稳定的官方分支（除非使用备份）。

### 3.b. 混合稳定版与测试版

#### package.keywords 文件

你可以要求 Portage 对特定包允许测试分支，而系统的其余部分使用稳定分支。要实现这一点，在 `/etc/portage/package.keywords` 中添加包名和想要使用的测试分支。例如，为 gnumeric 使用测试分支：

```
代码列表 2：/etc/portage/package.keywords 为 gnumeric 的设置

app-office/gnumeric-x86
```

#### 测试特定版本

如果你想使用测试分支中的特定软件版本，但不希望 Portage 对后续版本使用测试分支，你可以在 `package.keywords` 文件中添加版本。在这种情况下你必须使用 `=` 运算符。你也可以使用 `<` 使用版本范围。

`<` 或 `>=` 运算符。

在任何情况下，如果你添加了版本信息，必须使用运算符。如果你省略了版本信息，则不能使用运算符。

在下面的示例中，我们要求 Portage 接受 gnumeric-1.2.13：

## 代码列表 3：启用特定的 gnumeric 测试版本

```
~app-office/gnumeric-1.2.13 ~x86
```

## 3.c. 使用屏蔽包（Masked Packages）

### package.unpack 文件

Gentoo 开发者不支持使用这些文件。在执行此时请务必小心。与 package.unpack 和/或 package.mask 相关的支持请求将不会得到回复。你会收到警告。

当一个包被 Gentoo 开发者屏蔽，而你尽管由于 package.mask 文件（位于 `/etc/portage/profiles`）中列出的原因，但仍想使用它时，请在 `/etc/portage/package.unpack` 中添加完全相同的行。

例如，如果 `=net-mail/hotwayd-0.8` 被屏蔽，你可以通过在 package.unpack 文件中添加完全相同的行来进行提示：

## 代码列表 4：/etc/portage/package.unpack

```
~net-mail/hotwayd-0.8
```

### package.mask 文件

当你不想让 Portage 考虑某个包或包的特定版本时，可以通过向 `/etc/portage/package.mask` 添加适当的行来屏蔽它。

例如，如果你不想让 Portage 从 `gentoo-sources-2.6.8.1` 安装内核源码，向 package.mask 中添加以下行：

## 代码列表 5：/etc/portage/package.mask 示例

```
>sys-kernel/gentoo-sources-2.6.8.1
```

## 4. 其他 Portage 工具

### 4.a. etc-update

etc-update 是一个辅助合并 `_cf0000_<name>` 文件的工具。它提供交互式的合并设置，并可以自动合并细微更改。`_cf0000_<name>` 文件是 Portage 在想要覆盖受 `CONFIG_PROTECT` 变量保护目录中的文件时生成的。

运行 etc-update 非常简单：

## 代码列表 1：运行 etc-update

```
# etc-update
```

在合并简单的更改后，系统将向你列出等待更新的受保护文件。在底部，你将看到以下选项：

## 代码列表 2：etc-update 选项

```
通过相应的数字选择要编辑的文件。

(-1 退出) (-3 自动合并所有剩余文件)
```



(-5 自动合并并使用 `mv -i`);

如果你输入 `-1`，`etc-update` 将退出并停止任何后续更改。如果你输入 `-3` 或 `-5`，所有配置文件将被用新版本覆盖。因此，选择不应自动更新的第一个配置文件是非常关键的。这只需输入该配置文件左侧列出的数字即可。

作为一个示例，我们选择了配置文件 `/etc/perf.conf`：

### 代码列表 3：更新特定的配置文件

```
/etc/perf.conf 和 /etc/._cfgg0000_perf.conf 之间的差异开始

---

/etc/perf.conf 和 /etc/._cfgg0000_perf.conf 之间的差异结束

1) 用更新版本替换原始文件

2) 更新并保持原始文件不变

3) 交互式合并原始文件与更新版本

4) 再次显示差异
```

你可以看到两个文件之间的差异。如果你认为更新后的配置文件可以无问题使用，输入 `1`。如果你认为更新后的配置文件是不正确的，或没有提供任何有用信息，输入 `2`。如果你想交互式地更新当前文件，输入 `3`。

这里没有必要进一步阐述合并过程。为了完整起见，将列出在交互式合并这两个文件时可以使用可以使用命令。你将看到两个文件（原始文件和建议的新文件）以及一个可以输入以下命令的提示符：

### 代码列表 4：交互式合并命令

```
ed    编辑两个版本，每个版本都带有页头。

eeb   编辑使用两个版本。

elf   编辑使用左侧版本。

err   编辑使用右侧版本。

e    编辑当前版本。

i    使用左侧版本。

r    使用右侧版本。

s    使用当前版本。

v    详细信息。

q    退出。
```

当你不想让 Portage 考虑某个包或包的特定版本时，可以通过向 `/etc/portage/package.mask` 添加适当的行来屏蔽它。例如，如果你不想让 Portage 从 `gentoo-sources-2.6.8.1` 安装内核源码，向 `package.mask` 中添加以下行：

### 代码列表 5：/etc/portage/package.mask 示例

```
>sys-kernel/gentoo-sources-2.6.8.1
```

当一个包被 Gentoo 开发者屏蔽，而你尽管由于 `package.mask` 文件（位于 `/etc/portage/profiles`）中列出的原因，但仍想使用它时，请在 `/etc/portage/package.unpack` 中添加完全相同的行。

例如，如果 `=net-mail/hotwayd-0.8` 被屏蔽，你可以通过在 `package.unpack` 文件中添加完全相同的行来进行提示：

### 代码列表 4：/etc/portage/package.unpack

```
~net-mail/hotwayd-0.8
```

`package.unpack` 文件

Gentoo 开发者不支持使用这些文件。在执行此时请务必小心。与 `package.unpack` 和/或 `package.mask` 相关的支持请求将不会得到回复。你会收到警告。

`package.mask` 文件

当你不想让 Portage 考虑某个包或包的特定版本时，可以通过向 `/etc/portage/package.mask` 添加适当的行来屏蔽它。例如，如果你不想让 Portage 从 `gentoo-sources-2.6.8.1` 安装内核源码，向 `package.mask` 中添加以下行：

### 代码列表 5：/etc/portage/package.mask 示例

```
>sys-kernel/gentoo-sources-2.6.8.1
```

## 4. 其他 Portage 工具

### 4.a. etc-update

`etc-update` 是一个辅助合并 `_cf0000_<name>` 文件的工具。它提供交互式的合并设置，并可以自动合并细微更改。`_cf0000_<name>` 文件是 Portage 在想要覆盖受 `CONFIG_PROTECT` 变量保护目录中的文件时生成的。

运行 `etc-update` 非常简单：

### 代码列表 1：运行 etc-update

```
# etc-update
```

在合并简单的更改后，系统将向你列出等待更新的受保护文件。在底部，你将看到以下选项：

### 代码列表 2：etc-update 选项

```
通过相应的数字选择要编辑的文件。

(-1 退出) (-3 自动合并所有剩余文件)

(-5 自动合并并使用 'mv -i');
```

如果你输入 `-1`，`etc-update` 将退出并停止任何后续更改。如果你输入 `-3` 或 `-5`，所有配置文件将被用新版本覆盖。因此，选择不应自动更新的第一个配置文件是非常关键的。这只需输入该配置文件左侧列出的数字即可。

作为一个示例，我们选择了配置文件 `/etc/perf.conf`：

### 代码列表 3：更新特定的配置文件

```
/etc/perf.conf 和 /etc/._cfgg0000_perf.conf 之间的差异开始

---

/etc/perf.conf 和 /etc/._cfgg0000_perf.conf 之间的差异结束

1) 用更新版本替换原始文件

2) 更新并保持原始文件不变

3) 交互式合并原始文件与更新版本

4) 再次显示差异
```

你可以看到两个文件之间的差异。如果你认为更新后的配置文件可以无问题使用，输入 `1`。如果你认为更新后的配置文件是不正确的，或没有提供任何有用信息，输入 `2`。如果你想交互式地更新当前文件，输入 `3`。

这里没有必要进一步阐述合并过程。为了完整起见，将列出在交互式合并这两个文件时可以使用命令。你将看到两个文件（原始文件和建议的新文件）以及一个可以输入以下命令的提示符：

### 代码列表 4：交互式合并命令

```
ed    编辑两个版本，每个版本都带有页头。

eeb   编辑使用两个版本。

elf   编辑使用左侧版本。

err   编辑使用右侧版本。

e    编辑当前版本。

i    使用左侧版本。

r    使用右侧版本。

s    使用当前版本。

v    详细信息。

q    退出。
```

当你不想让 Portage 考虑某个包或包的特定版本时，可以通过向 `/etc/portage/package.mask` 添加适当的行来屏蔽它。例如，如果你不想让 Portage 从 `gentoo-sources-2.6.8.1` 安装内核源码，向 `package.mask` 中添加以下行：

### 代码列表 5：/etc/portage/package.mask 示例

```
>sys-kernel/gentoo-sources-2.6.8.1
```

## 4. 其他 Portage 工具

### 4.a. etc-update

`etc-update` 是一个辅助合并 `_cf0000_<name>` 文件的工具。它提供交互式的合并设置，并可以自动合并细微更改。`_cf0000_<name>` 文件是 Portage 在想要覆盖受 `CONFIG_PROTECT` 变量保护目录中的文件时生成的。

运行 `etc-update` 非常简单：

### 代码列表 1：运行 etc-update

```
# etc-update
```

在合并简单的更改后，系统将向你列出等待更新的受保护文件。在底部，你将看到以下选项：

### 代码列表 2：etc-update 选项



通过相应的数字选择要编辑的文件。

`(-1` 退出) `(-3` 自动合并所有剩余文件)

`(-5` 自动合并并使用 '`mv -i`' );

```
如果你输入 -1，etc-update 将退出并停止任何后续更改。如果你输入 -3 或 -5，所有配置文件将被用新版本覆盖。因此，选择不应自动更新的第一个配置文件是非常关键的。这只需输入该配置文件左侧列出的数字即可。
```

作为一个示例，我们选择了配置文件 `/etc/perf.conf`：

## 代码列表 3：更新特定的配置文件

```
/etc/perf.conf 和 /etc/._cfgg0000_perf.conf 之间的差异开始

---

/etc/perf.conf 和 /etc/._cfgg0000_perf.conf 之间的差异结束

1) 用更新版本替换原始文件

2) 更新并保持原始文件不变

3) 交互式合并原始文件与更新版本

4) 再次显示差异
```

你可以看到两个文件之间的差异。如果你认为更新后的配置文件可以无问题使用，输入 `1`。如果你认为更新后的配置文件是不正确的，或没有提供任何有用信息，输入 `2`。如果你想交互式地更新当前文件，输入 `3`。

这里没有必要进一步阐述合并过程。为了完整起见，将列出在交互式合并这两个文件时可以使用命令。你将看到两个文件（原始文件和建议的新文件）以及一个可以输入以下命令的提示符：

## 代码列表 4：交互式合并命令

```
ed    编辑两个版本，每个版本都带有页头。

eeb   编辑使用两个版本。

elf   编辑使用左侧版本。

err   编辑使用右侧版本。

e    编辑当前版本。

i    使用左侧版本。

r    使用右侧版本。

s    使用当前版本。

v    详细信息。

q    退出。
```

## 5. 偏离官方树

### 5.a. 使用 Portage 树子集

排除包/类别

你可以选择性地更新类别/包并忽略其他类别。我们通过让 `rsync` 在合并 `--sync` 时排除类别/包来实现这一点。

你需要在 `/etc.conf` 的 `RSYNC_EXCLUDE` 变量中定义包含排除模式的文件名。

## 代码列表 1：在 etc.conf 中定义排除文件

```
RSYNC_EXCLUDE=/etc/portage/rsync_excludes
```

## 代码列表 2：在 /etc/portage/rsync_excludes 中排除所有游戏

```
games/*
```

注意这可能导致依赖问题，因为允许的包可能依赖于新的排除包。

### 5.b. 添加非官方构建

你可以使用 Portage 使用 Portage 树未提供的构建。创建一个新目录（例如 `/usr/portage`），在其中存储第三方构建。使用与官方 Portage 树相同的目录结构。

然后在 `/etc.conf` 中定义 `PORTDIR_OVERLAY` 并将其指向自定义目录。现在当你使用 Portage 时，它将考虑这些构建，而不会在下次运行 `emerge --sync` 时移除/覆盖这些构建。

处理多个 Overlay

对于想要多个 Overlay、在包进入 Portage 树之前进行测试或仅仅是为了从各种来源使用非官方构建的强力用户，`app-portage-gentookit-build` package sync 是一个帮助你保持 Portage Overlay 更新的工具。每个仓库应该在 `/etc/gentoo/configuration` 目录下有一个 `.rsyncsource` 文件，其中包含仓库位置、名称、ID 等。

假设你有两个额外的仓库，分别名为 `java`（用于开发中的 Java 构建）和 `entapps`（用于为企业内部开发的应用程序）。你可以使用以下命令更新这些仓库：

## 代码列表 3：使用 gensync 更新几个仓库

```
# gensync java entapps
```

### 5.c. 非 Portage 维护的软件

使用 Portage 使用自维护软件

当你想自己安装和维护软件而不使用 Portage 自动化该过程时，即使 Portage 可以提供软件标题。已知案例是内核源码和 NVIDIA 驱动程序。你可以配置 Portage 使其知道某个包是手动安装的。这个过程由 Portage 通过 `/etc/portage/profile/package.provided` 调用并支持。

例如，如果你告知 Portage 关于手动安装的 `vanilla-sources-2.6.11.6`，向 `/etc/portage/profile/package.provided` 添加以下行：

## 6. 构建应用程序

# 6. Emerge 和 Ebuild

`ebuild` 是 Portage 系统的一个低级接口。使用此应用程序，你可以针对指定的 ebuild 执行特定的操作。例如，你可以手动执行单独的合并步骤。

`ebuild` 通常用于开发目的；因此，关于 `ebuild` 的更多信息可以在《开发者手册》（Developers Handbook）中找到。然而，我们将解释 Portage 在特定软件标题的合并过程中是如何调用 `ebuild` 实例的，以及如何调用某些 `ebuild` 允许你执行的配置后步骤。

## 6.b. 手动安装软件

### 获取源码与校验

每当你针对给定的 `ebuild` 调用 `ebuild` 时，它会验证所有涉及文件的校验和是否与附带 `Manifest` 文件或 `files/digest-<name>-<version>` 文件中的值相等。这在获取源码之后发生。

使用 `ebuild` 获取源码，运行：

```
# ebuild path/to/ebuild fetch
```

如果 `ebuild` 的 `mdsum` 与 `Manifest` 文件中列出的不匹配，或者下载的源码与 `files/digest-<package>` 文件中列出的不匹配，你会收到类似下面的错误：

```
!!! File is corrupt or incomplete. (Digests do not match)

>>> our recorded digest: db20421ce35e854346e3ef19e6044e

>>> your file's digest: f10392b7c0b2bc463ad0964260a7d6
```

后续的一行将提到错误的文件。

如果你确定获取的源码和 `ebuild` 本身是有效的，可以使用 `ebuild` 的功能重新生成 `Manifest` 和 `digest-<package>` 文件：

```
# ebuild path/to/ebuild digest
```

### 解包源码

要在 `/var/tmp/portage`（或任何你在 `/etc/make.conf` 中指定的目录）中解包源码，请运行 `ebuild` 的 `unpack` 功能：

```
# ebuild path/to/ebuild unpack
```

这将执行 `ebuild` 的 `src_unpack()` 函数（如果没有定义 `src_unpack()`，则默认执行纯粹解压）。必要的补丁（patches）也是在这一步应用的的。

### 编译源码

合并过程的下一步是编译源码。`ebuid` 的 `compile` 功能通过执行 `ebuild` 中的 `src_compile()` 函数来处理这一步。这这也包括相应的 `configure` 步骤。

```
# ebuild path/to/ebuild compile
```

如果你想更改编译指令，建议编辑 `ebuild` 的 `src_compile()` 函数。不过，你也可以骗过 Portage，使其认为 `ebuild` 已经完成了编译步骤。运行所有必要的命令并在工作目录下创建一个名为 `.compiled` 的空文件：

# 代码列表 6：告知 Portage 编译任务已完成

```
# touch .compiled
```

### 在临时位置安装文件
在下一步，Portage 将将所有必要文件安装在临时位置。该目录将包含所有要在运行系统上合并的文件。你可以通过运行 `ebuild` 的 `install` 功能来实现这一点，该功能会执行 `ebuild` 的 `src_install()` 函数：

# 代码列表 7：安装文件

```
# ebuild path/to/ebuild
```



### 将文件合并到运行系统
最后一步是将所有文件合并到运行系统（`livesystem`）并在 Portage 后端注册这些文件。`ebuild` 的 "`qmerge`" 步骤涉及以下操作：

- 如果指定，执行 `pkg_preinst()` 函数
- 将所有文件复制到运行系统
- 在 Portage 后端注册文件
- 如果指定，执行 `pkg_postinst()` 函数

运行 `ebuild` 的 `qmerge` 功能来完成这些步骤：

#### 代码列表 8：在运行系统上合并 ebuild

```
# ebuild path/to/ebuild qmerge
```

### 清理临时目录
最后，你可以使用 `ebuild` 的 `clean` 功能清理临时目录：

#### 代码列表 9：清理临时目录

```
# ebuild path/to/ebuild clean
```

## 6.c. 额外的 Ebuild 功能
### 运行合并相关命令
使用 `ebuild` 的 `merge` 功能，你可以一次性运行 `fetch`、`unpack`、`compile` 和 `qmerge` 命令：

#### 代码列表 10：安装软件

```
# ebuild path/to/ebuild merge
```

### 执行配置操作
某些应用程序包含了进一步配置你的系统的指令。这些指令是交互式的，因此不会自动执行。要运行 `ebuild`（可选的）`config()` 函数中列出的这些步骤，请使用 `ebuild` 的 `config` 功能：

#### 代码列表 11：配置包

```
# ebuild path/to/ebuild config
```

### 构建包（或 RPM）
你可以指示 Portage 创建二进制包或 RPM 文件。使用 `ebuild` 的 `package` 或 `rpm` 功能来创建归档。这些功能之间存在一些差异：

- `package` 功能类似于 `merge` 功能，在创建包之前执行所有必要的步骤（`fetch`、`unpack`、`compile`）
- `rpm` 功能在运行 `install` 功能后构建 RPM 包

#### 代码列表 12：创建包

```
（对于二进制包）

# ebuild path/to/ebuild package

（对于 RPM 包）

# ebuild path/to/ebuild rpm
```

生成的 RPM 文件不包含依赖信息。

## 6.d. 更多信息
关于 Portage、`ebuild` 应用和 `ebuild` 文件的更多信息请参考以下帮助页：

#### 代码列表 13：帮助页

```
$ portage (Portage 本身)

$ emerge (emerge 命令)

$ ebuild (ebuild 命令)

man ebuild (ebuild 文件)
```

你还可以在《开发者手册》中找到开发相关信息。

## D. Gentoo 网络
### 1. 开始
#### 1.a. 开始
注意：本文假设你已经正确配置了内核、硬件模块以及接口名称。我们还假设你配置的是 `eth0`，但可能是 `eth1`、`wlan0` 等。

注意：本文需要更好的布局。要启动你的网卡，你需要告知 Gentoo RC 系统。这是通过在 `/etc/init.d` 中从 `net.lo` 到 `net.eth0` 创建符号链接实现的。

#### 代码列表 1：将 net.eth0 链接到 net.lo

```
# cd /etc/init.d

# ln -s
```

Gentoo 的 RC 系统现在知道了接口。它还需要知道如何配置新接口。所有的网络接口都在 `/etc/conf.d` 中配置。以下是 DHCP 和静态地址的示例。

#### 代码列表 2：etc/conf.d 示例

```
# 对于 DHCP

config_eth0=( "dhcp" )

# 使用 CIDR 法的静态 IP

config_eth0="192.168.0.7/24"

routes_eth0=( "default via 192.168.0.1" )
```

```
# 使用子网掩码法的静态 IP

config_eth0=("192.168.0.7 255.255.255.0")

routes_eth0=("default gw 192.168.0.1")
```

注意：如果你没有为接口指定配置，则假设为 DHCP。注意：CIDR 代表无类域间。IPv4 地址被分类为 A、B 或 C。早期的分类系统并没有阻止互联网的巨大力量，有一种地址方案允许一个 IP 地址表示许多 IP 地址。CIDR 地址看起来像普通的 IP 地址，结尾是一个斜杠加上一个数字；192.168.0.0/16。CIDR 在 RFC 1519 中描述。

现在我们已经配置了接口，可以使用以下命令启动和停止：

```
# /etc/init.d/net.eth0 start

# /etc/init.d/net.eth0 stop
```

重要：在排除网络故障时，建议在 `/etc/conf.d/rc` 中设置 `RC_VERBOSE="yes"` 以获取更多信息。

现在你已经成功启动并停止了接口，可能希望它在 Gentoo 启动时自动运行。做法如下，“`rc`”命令指示 Gentoo 启动运行级别（runlevel）中尚未启动的脚本：

```
# rc-update add net.eth0 default

# rc
```

## 2. 高级配置
### 2.a. 高级配置
`config_eth0` 变量是接口的核心。它是配置接口（在本例中为 `eth0`）的高级指令。列表中的命令都会执行。如果至少有一个有效，则认为接口是正常的。

以下是内置指令列表：

| 命令 | 描述 |
| --- | --- |
| null | 如果操作接口已启动且有地址，则成功终止配置 |
| IPv4 或 IPv6 地址 | 将地址添加到接口。dhcp、adsl 或 ip6（后者是来自第三方模块的自定义命令） | 运行提供该命令的模块。例如，dhcp 将运行一个提供 DHCP 的模块，可以是 `dhcp`、`udhc`、`client` 或 `prompt` 之一 |

如果命令失败，你可以指定一个回退命令。回退命令必须与配置结构完全匹配。

你可以将这些命令链起来。这里是一些真实的示例：

```
# 添加三个 IPv4 地址

config_eth0={

  "192.168.0.2/24"

  "192.168.0.3/24"

  "192.168.0.4/24"

}

# 添加一个 IPv4 地址和两个 IPv6 地址

config_eth0={

  "192.168.0.5/32"

  "4321:0:1:2:3:4:567:89ab"

  "4321:0:1:2:3:4:567:89ac"

}
```

保留我们内核分配的地址，除非接口掉线，否则通过 DHCP 分配另一个。如果 DHCP 失败，我们将添加一个由 APIPA 确定的静态地址
```
config_eth0={

  "nop"

  "dhcp"

}

fallback_eth0={

  "null"

  "apipa"

}
```

> 注意：使用 `ifconfig` 模块并添加多个地址时，会为每个额外的地址创建接口别名。因此，通过上述两个示例，你将获得 `eth0`、`eth1` 和 `eth2`。你无法对这些接口进行任何特殊操作，因为内核和其他程序会将 `eth0` 和 `eth1` 视为 `eth2`。

> 重要：回退顺序非常重要！如果我们没有指定 `null`，那么只有在 `noop` 命令失败时，`apipa` 命令才会运行。

注意：APIPA 和 DHCP 将在稍后进行讨论。

### 2.b. 网络依赖
`/etc/init.d` 中的初始化脚本可以依赖于特定的接口，或者在 `/etc/conf.d/rc` 中定义的 `net` 也可以具有不同的含义，这取决于 `RC_NET_STRICT_CHECKING` 变量。

#### 值描述

- `net` 服务至少有一个服务 `bednet` 必须处于启动状态。这可以用于带有 WIFI 的笔记本用户，他们只想在给定时间开启一个网络，以便 `net` 服务被视为已启动。
- 此没有选项，但 `net.eth0` 也已连接。这对于不关心特定接口是否启动状态的人很有用。
- 所有网络接口必须处于启动状态，`net` 服务才能被考虑。

但是 `net.br0` 依赖于 `net.eth0` 和 `net.eth1` 呢？`net.eth1` 是一个无线或 PPP 设备，在添加到网桥之前需要进行配置。这不能在 `/etc/init.d/net.br0` 中完成，因为它是它的符号链接。

答案是在你的 `/etc/conf.d/net` 中编写 `depend()` 函数。

```
代码行 2: /etc/conf/net 中的 net.br0 依赖
```

```
# 你可以使用当前脚本中找到的任何依赖关系（use, after, before）

depend_br0()

need net.eth0 net.eth1
```



关于依赖关系的更详细讨论，请参阅 Gentoo Handbook 中的“在脚本中编写”部分。

## 2.c. 变量名与

变量名是动态的。它们通常遵循 `variable_${interface}[address|mac]` 的结构。例如，变量 `dhcp_eth0` 保存 `eth0` 的 DHCP 选项值，而 `dhcp_essid` 存储接口连接到 SSID "essid" 时的 DHCP 选项值。

然而，这里没有硬性规定服务名必须是 `ethx`。事实上，许多接口的名称如 `wax`、`ras` 和 `xi`，定义的定义的接口（如网桥）也可以被命名为任何名称，例如 `foo`。为了方便起见，无线访问点可以拥有包含字母数字字符的名称，这很重要，因为你可以根据每个 ESSID 配置网络。

这一切的缺点是 Gentoo 在网络中使用下划线（bars） - `bash` 无法在英语字母数字之外使用它们。为了绕过这一限制，我们将每个非字母数字的变量更改为 `_` 字符。

`bash` 的另一个缺点是变量的内容 - 某些字符需要转义。这可以通过需要在转义的字符前面放置 `\` 字符来实现。例如 `\.` 和 `\'`。

在这个示例中，我们使用 ESSID，因为它们包含最广泛的字符集。我们将使用 ESSID My \NET：

### 代码列表 3：变量名示例

```
# 这可行，但域名是无效的

dns_domain_My___NET=My \ NET
```

# 当无线卡连接到 ESSID 为 My \ NET 的 AF 时，上述设置会将 dns 域设置为 My \ NET

## 3. 模块化网络

### 3.a. 网络模块

我们支持模块化网络脚本，这意味着我们可以轻松添加对新接口类型和配置模块的支持，同时与旧模块保持兼容。

如果模块所需的包已安装，则加载模块。如果你在这里指定了一个未安装对应包的模块，你将收到一个错误，说明你需要安装哪个包。理想情况下，只有当你安装了两个或多个提供服务的包且需要倾向于其中某一个时，才使用模块设置。

> 注意：除非另有说明，这里讨论的所有设置都在 `/etc/conf.d/net` 中。

### 代码列表 1：模块偏好

```
# 优先使用 iproute2 而非 ifconfig

modules=( "iproute2")
```

- 你也可以为接口指定其他模块
- 在这种情况下，我们优先使用 `dhcp6` 而非 `dhcpcd`
`modules_eth0="dhcp6"`
- 你也可以指定不使用的模块 - 例如，你可能正在使用 `supplicant` 或 `linux-ng` 来控制无线配置，但你仍然想通过关联的 ESSID 配置网络设置。
`modules=("iwiconfig")`

### 3.b. 接口处理器

我们目前提供两个处理器：`ifconfig` 和 `iproute2`。你需要其中之一来执行任何类型的网络配置。

`ifconfig` 是 Gentoo 的默认选择，它包含在系统配置中。`iproute2` 是一个更强大且灵活的包，但默认并不包含。

### 代码列表 2：使用 iproute2

```
# emerge sys-apps/iproute2

# 如果两者都安装，则优先使用 iproute2

modules=(\iproute2")
```

由于 `ifconfig` 和 `iproute2` 执行的操作非常相似，它们允许配置互通工作。

### 代码列表 3：ifconfig 和 iproute2

```
config_eth0="192.168.1.1/24"

config_eth0="192.168.1.1/24"
```

### 3.c. DHCP

DHCP 是从 DHCP 服务器获取信息（IP 地址、DNS 服务器等）的手段。DHCP 可以由 `dhclient`、`dhcped` 或 `udhcpc` 提供。

| 模块 | 包 | 优点 | 缺点 |
|---|---|---|---|
| dhclient | net-misc/dhclient | ISC 开发，可配置 | 配置复杂，软件臃肿 |
| dhcped | net-misc/dhcped | Gentoo 长期默认 | 不维护 |
| pump | net-misc/pump | 轻量级 | 不维护 |
| udhcpc | net-misc/udhcpc | 轻量级 - 客户端 | 不可靠 |

如果你有多个 DHCP 客户端，需要指定使用哪一个 - 否则使用 `dhcpcd`。

要为 DHCP 模块指定选项，使用 `module_eth0="..."`（更改你使用的 DHCP 模块）。

尝试让 DHCP 与实现无关 - 我们通过 `dhcp_eth0` 变量支持以下功能：

- 释放 IP 地址供重用
- `nodns` - 不覆盖 `/etc/resol.conf`
- `nonstop` - 不覆盖 `/etc/ntp.conf`
- `nonis` - 不覆盖 `/etc/resol.conf`

### 代码列表 4：/etc/conf.d 中的示例 DHCP 配置

```
# 仅当有多个 DHCP 模块时需要

modules=(dhcpcd")

config_eth0="10" # 10 秒后超时

dhcpcd_eth0="lease nonstop nonis" # 获取地址
```

> 注意：`dhclient`、`udhcpc` 和 `pump` 默认会将主机名发送到 DHCP 服务器，你不需要指定。

### 3.d. ADSL 调制解调器

首先安装 ADSL 软件。

### 代码列表 5：安装 rp-pppoe 包

```
# emerge-netdialup/rp-pppoe
```

> 警告：baseline-1.11 仅支持 PPPoE。希望未来版本支持 PPPoA。

现在我们需要通过更新 `/etc/conf.d/net` 将 `eth0` 配置为 ADSL 接口并输入用户名。

### 代码列表 6：在 /etc/conf.d/net 中为 ethSL 配置 ADSL

```
config_eth0="*adsl"

adsl_user_eth0="username"
```

最后我们需要在 `/etc/ppp/pap-secrets` 中定义你的用户名和密码。

### 代码列表 7：示例 /etc/ppp/pap-secrets

```
```

APIPA 尝试通过在接口上对 `169.254.0.0-169.254.255.255` 范围内的地址进行 `arping` 来寻找空闲地址。如果没有找到响应，则仅适用于没有 DHCP 服务器且你没有直接连接互联网且所有其他计算机都使用 APIPA 的局域网。

若要支持 APIPA，请 `merge net-misc/iputils` 或 `net-analyze/arping`。

### 代码列表 8：/etc/conf.d/net 中的 APIPA 配置

```
# 尝试 DHCP - 如果失败则回退到 APIPA

config_eth0="dhcp"

fallback_eth0="apipa"

# 仅使用 APIPA

config_eth0="apipa"
```

## 3.5. 绑定 (Bonding)

对于链路绑定/汇聚（link bonding/trunking），请 `emerge net-misc/ifensave`。

绑定用于增加网络带宽。如果你有两个连接到同一个网络的网卡，可以将它们绑定在一起，这样你的应用程序只会看到一个接口，但实际上它们使用了两个网卡。

### 代码列表 9：/etc/conf.d/net 中的绑定配置

```
# 将接口绑定在一起

slaves_bond0="eth0 eth1 eth2"

# 你可能不想为绑定后的接口分配 IP

config_bond0="null"

# 依赖 eth0、eth1 和 eth2，因为它们可能需要额外配置

depend_bond0() {

  need net_eth0 net_eth1 net_eth2

}
```

## 3.6. 桥接 (支持 802.1d)

若要支持桥接，请 `emerge net-misc/bridge-utils`。
例如，你可能有一台服务器通过 ADSL 调制解器连接互联网并通过无线网卡让其他计算机通过 ADSL 调制解器上网。你可以创建一个桥接将这两个接口连接起来。

### 代码列表 10：/etc/conf.d/net 中的桥接配置

```
# 配置桥接 - 更多详情请 man brctl-

brctl_br0="setethlo 0" "stp.off"

# 将端口添加到桥接 br0

bridge_br0="eth0"

# 你需要将端口连接到 null 值，因为 dhcp 不启动

config_eth0="null"

config_eth1="null"

# 最后给桥接分配地址 - 你也可以使用 DHCP

conf_br0="192.168.0.1/24"

# 依赖 eth0 和 eth1，因为它们可能需要额外配置

depend_br0() {

need net_eth0 net_eth1

}
```



重要：对于某些用例，你可能需要查阅变量名文档。

## 3.7. MAC 地址

如果你拥有 `sys-apps/baselayout-1.11.14` 并且想要更改为特定的 MAC 地址，你不需要为接口的 MAC 地址更改任何内容。然而，如果你需要更改为随机 MAC 地址或比上述版本旧的 `baselayout`，你必须 `emerge net-analyzer/maccchanger` 才能使用此功能。

### 代码列表 11：MAC 地址示例

```
# 设置接口的 MAC 地址

mac_eth0=00:11:22:33:44:55

# 仅随机最后 3 个字节

mac_eth0=*random-ending"

# 在相同物理类型的连接之间随机（例如光纤、

# 铜线、无线），所有厂商

mac_eth0=*random-anykind"

# 在任何物理类型的连接之间随机（例如光纤、铜线、

# 无线），所有厂商

mac_eth0=*random-anykind"

# 全随机警告：此处生成的某些 MAC 地址可能

# 不按预期工作

mac_eth0=*random-full*"
```

## 3. 隧道 (Tunneling)

你不需要 `emerge` 任何隧道，接口处理器可以为你完成。

### 代码列表 12：`/etc/conf.d/net` 中的隧道配置

```
# GRE 隧道

iptunnel_vpn0= mode gre 207.82.1 key 0ffff ttl 255

# IPIP 隧道

iptunnel_vpn0= mode ipip 207.82.2 ttl 255

# 配置接口

config_vpn0="172.168.0.2 peer 192.168.1.1"
```

## 3.j. VLAN (支持 802.1q)

若要支持 VLAN，请 `emerge net-misc/vconfig`。
虚拟局域网是一组设备，其表现就像连接到同一个网络段 - 尽管并非如此。VLAN 成员可以是共享相同物理网络的成员。

### 代码列表 13：`/etc/conf.d/net` 中的 VLAN 配置

```
# 如下所示为接口指定 VLAN 数字

# 请确保你的 VLAN ID 是零填充的

vlan_eth0="1*"

# 你也可以为每个配置页面配置 VLAN

# 更多详情

vconfig_eth0*=(set_name "VLAN_NOD_PAD"

vconfig_vlan*=(set_flag 1 "egress_map 2")

# 像通常一样配置接口

config_vlan*="172.168.0.1 netmask 255.255.254.0"

vconfig_vlan*="172.168.0.1 netmask 255.255.254.0"
```

> 重要：对于某些 VLAN 设置，你需要考虑变量名。

## 4. 无线网络 (Wireless Networking)

### 4.a. 简介

目前我们使用 `wireless-tools` 或 `wpa_supplicant` 进行无线设置。重要的是，我们在全局范围内配置无线网络，而不是基于接口。`wpa_supplicant` 是最佳选择，但它不支持所有驱动程序。支持的驱动列表请阅读 `wpa-site`。此外，`wireless-tools` 支持几乎所有的卡，但无法连接到你配置的 SSID。

警告：`baselayout` 不支持 `linux-wlan-driver`。因为 `linux-wlan-ng` 有自己的设置和配置，与其他人完全不同。在这种情况下使用 `linux-wlan-ng`。

### 4.b. WPA Supplicant

`WPA Supplicant` 是一个允许你连接到启用 WPA 热点的包。它的设置相当灵活，因为它仍处于测试阶段 - 但大多数情况下有效。

重要：为了让 `wpa_supplicant` 工作，你必须在内核中配置 `CONFIG_PACKET`。

#### 代码列表 1：安装 `wpa_supplicant`

```
# emerge net-wireless/wpa_supplicant
```

现在我们必须配置 `/etc/conf.d/net` 以在 `wireless-tools` 上设置 `wpa_supplicant`。告诉 `wpa_supplicant` 我们应该使用哪个驱动程序很重要，因为它现在还不擅长猜测。注意：如果你使用 `host-driver`，你需要将卡设置为 Managed 模式才能正确与 `wpa_supplicant` 使用。你可以在 `/etc/conf.d/net` 中通过 `iwconfig eth0 managed` 实现这一点。然而，我们必须配置 `wpa_supplicant` 本身，对于你尝试连接的热点来说有点复杂。以下内容来自 `/etc/wpa_supplicant.example` 并简化了 `wpa_supplicant` 的用法。

#### 代码列表 2：为 `wpa_supplicant` 配置 `/etc/conf.d/net`

```
# 优先使用 wpa_supplicant 而非 wireless-tools

modules=( "wpa_supplicant" )

# 为名为 ESSID1 和 ESSID2 的热点配置 WEP 密钥

# 你可以配置最多 4 个 WEP 密钥，但任何时候只有一个活跃

# 所以我们提供默认索引 [1]

# 之后再次将密钥更改为 [1]
```

#### 代码列表 3：示例 `/etc/wpa_supplicant.conf`

```
# 下方行不要更改，否则我们将拒绝工作

ctrl_interface=/var/run/wpa_supplicant

# 确保只有 root 可以读取 WPA 配置

ctrl_interface_group=0

# 让 wpa_supplicant 扫描和 AP 选择

ap_scan=1

# 简单情况：WPA-PSK，PSK 为 ASCII 密码，允许所有有效的加密算法

network={

ssid="simple"

psk="secret passphrase"

# 优先级越高，匹配得越快

priority=2

}

# 与之前相同，请求特定 SSID 的扫描（对于广播: SSID 的 AP）

network={

ssid="second ssid"

scan=ssid0

psk="secret passphrase"

priority=2

}

# 只使用 WPA-PSK。任何有效的加密组合都是

network={

ssid="example"

proto=WPA

mgmt=WPA-PSK

pairwise=TKIP

group=CCMP TKIP WEP104 WEP40

psk=6b48621d4a2f793029db7a2ecb930f6

priority=2

}
```

### 4.c. Wireless Tools

`Wireless Tools` 提供了一种通用的方法将无线接口配置为 WEP 安全级别。WEP 是一种弱的安全方法，但也是最常见的。

`Wireless Tools` 的配置由几个变量控制。下面的示例配置文件描述了你需要的一切。需要记住，没有配置意味着“连接到最强的未加密热点” - 我们总是尝试让你连接到某些东西。

注意：虽然你可以将无线设置存储在 `/etc/conf.d/wireless`，但本指南建议将其存储在 `/etc/conf.d`

#### 代码列表 5：`/etc/conf.d/net` 中的示例 `iw_config` 设置

```
# 优先使用 iw_config 而非 wpa_supplicant

modules=( "iwconfig" )
```



# 我们通过内联定义 ESSID 来使用除 1以外的 WEP 密钥
# 在密钥前加 s: 表示它是 ASCII 密钥，否则为 HEX 密钥
# enc open 指定安全级别（最安全）
# enc open restricted 指定安全级别（最不安全）
`key_ESSID_eth0[1]` = `"your key [1] enc open"`
`key_ESSID_eth0[1]` = `"aaaa-bbbb-cccc-ddcc [1] enc restricted`

# 以下内容仅在我们扫描可用接入点（AP）时生效
# 有时当一个接入点可见时，我们需要
# 定义一个优先的连接顺序
`preferred_order`=`"ESSID*2"`

# 细调接入点选择

你可以添加一些选项来微调你的接入点选择，也可以不添加。这些通常不是必须的。

你可以决定是否仅连接到首选接入点。默认情况下，如果所有尝试都失败且我们可以连接到未加密的接入点，可以通过 `associate_order` 变量来控制。以下是这些值及其控制方式的表格。

| 值 | 描述 |
|---|---|
| preferably |默认行为 |
| forpreferred | 我们仅连接到首选列表中的 AP。如果在扫描中未找到这些 AP，我们将按照优先顺序尝试连接它们。 |
| - | 不扫描 AP - 仅按顺序尝试连接每一个 AP |
| forego | 等同于 preferred + 连接到任何其他可用 AP |

最后，我们可能有 `blacklist_aps`（黑名单）和 `unique_ap` 选择。`blacklist_aps` 的工作方式类似于 `preferred_aps`。`unique_ap` 是一个是或否的值，用于判断第二个无线接口是否与第一个接口连接到同一个接入点。

# 代码列表 6：blacklist_aps 和 unique_ap 示例

```
# 有时你不想连接到某些接入点

blacklist_aps="ESSID*4"

# 如果你有多张无线卡，你可以设置是否允许

# 允许它们都关联到同一个接入点

# 值为 "yes" 和 "no"

# 默认是 "yes"

unique_ap="*yes"
```

# Ad-Hoc 主机模式

如果你在管理模式下无法连接到任何接入点，你也可以将自己设置为 Ad-Hoc 节点

# 代码列表 7：回退到 ad-hoc 模式

```
adhoc_essid_eth0="This Adhoc Node"
```

连接到 Ad-Hoc 网络或运行主机模式以成为接入点如何？这里有该部分的配置！你可能需要如所示指定 WEP 密钥。

# 代码列表 8：示例 ad-hoc/master 配置

```
# 设置模式 - 可以是 managed（默认）、ad-hoc 或 master（主机）
# 并非所有驱动程序都支持所有模式

mode_eth0="ad-hoc"

# 设置接口的 ESSID
# 在管理模式下，这将强制接口尝试连接到
# 指定 ESSID 而不是其他

essid_eth0="This Adhoc Node"

# 如果你不指定通道，我们将使用 3 通道

channel_eth0="*3"
```

重要：以下内容节录自 NetBSD 文档中的 BSD wavelen 文档。共有 14 个可用通道：据介绍，1-11 通道适用于北美，11-13 通道适用于大部分欧洲，10-13 通道适用于法国，第 14 通道适用于日本。如有疑问，请参考你的网卡或接入点的文档。确保你选择的通道与你的接入点（或 ad-hoc 网络中的另一个通道）匹配。北美和大部分欧洲销售的网卡默认通道为 5，法国销售的网卡默认为 11，日本销售的网卡默认为 14。

# 无线工具的故障排除

有一些变量可以帮助由于驱动或环境问题导致无线无法启动。以下是可以尝试的其他事项列表。

| 变量 | 默认值 | 描述 |
|---|---|---|
| `iwconfig_eth0` | | 查看 `iwconfig` 手页了解如何设置 |
| `iwpriv_eth0` | | 查看 `iwpriv` 手页了解如何设置 |
| `sleep_scan_eth0` | 0 | 扫描之前的等待秒数。当驱动/固件需要时间之前 |
| `sleep_associate_eth0` | 5 | 接口关联接入点之前的等待秒数 |
| `associate_test_eth0` | MAC | 某些驱动在丢失或尝试关联时不会重置 MAC 地址。某些驱动在丢失或尝试关联时不会重置质量级别。有效设置为 MAC, quality 和 all |
| `scan_mode_eth0` | | 某些驱动在扫描失败时必须处于 ad-hoc 模式 |
| `iwpriv_scan_eth0` | | 扫描后向接口发送一些 `iwpriv` 命令。更多详情查看 `iwpriv` 手页 |

## 4. 通过 ESSID 定义网络配置

有时，连接到 ESSID1 时需要 IP，连接到 ESSID2 时需要 DHCP。事实上，大多数变量可以通过 ESSID 定义。做法如下：

> 注意：如果你使用 WPA Supplicant 或 Wireless Tools，这将生效。

> 重要：你需要咨询变量名称。

> 代码列表 9：按 ESSID 覆盖设置

```
config_ESSID1="192.168.0.2/24 192.168.0.255"

routes_ESSID1="dhcp"

config_ESSID2="dhcp"

fallback_route_ESSID2="192.168.3.1/24"

# 我们可以重命名 server 和其他事项，除非

dns_server_ESSID1="192.168.0.1 192.168.0.2"

dns_domain_ESSID1="domain.domain"

dns_search_ESSID1="search.domain,search.domain"

# 我们覆盖接入点的 MAC 地址
# 如果你有具有相同 ESSID 的位置

config_0011ee233455*="dhcp"

dhcpopt="10"

ins_server_0011ee233455*="192.168.0.2"
```

## 5. 添加功能

### 5.a. 标准函数

可以定义两个在启动/停止操作期间调用的函数。调用时先传入接口名称，以便控制多个适配器。

`preup` 函数的返回值应该是 0（成功），表示接口的配置或去配置可以继续。如果返回非零值，则配置将中止。

`postdown` 函数的返回值将被忽略，因为如果失败无事可做。

# 代码列表 1：pre/post up 示例

```
preup() {

    # 在启动之前测试接口连接。这
    # 仅在某些适配器上工作，并且需要
    # 安装 mi-diag 包。

    if ettool($FACE) 2>/dev/null grep -q 'no link'; then

        warn "No link on $FACE; aborting configuration"

        return 1

}}

# 成功时返回 0

return 0

postdown() {

    # 脚本默认是检查 root 并禁止
    # 接口情况。注意如果你指定了
    # postdown() 函数将覆盖该逻辑。

    if [ -f /etc/fd ]; then

        error "root filesystem is network mounted - can't stop $FACE"

        return 1

    fi

}

# 成功时返回 0

return 0

postup() {

    # 这个函数可以用于，例如向动态 DNS
    # 服务注册。另一种可能性是在接口
    # 启动后发送/接收邮件。

    return 0

}

postdown() {

    # 这个函数主要是为了完整性……我从未
    # 想过用它做什么有趣的事

    return 0

}
```

### 5.b. 无线工具函数钩

注意：这与 WPA Supplicant 不兼容——`$[ESSID]` `$[ESSIDVAR]` 变量在 `setup()` 函数中可用。

可以定义两个在 `associate` 函数期间调用的函数。调用时先传入接口名称，以便一个函数控制多个适配器。

`preassociate` 函数的返回值应该是 0（成功），表示接口的配置或去配置可以继续。如果返回非零值，则配置将中止。

`postassociate` 函数的返回值将被忽略，因为如果失败无事可做。

`$[ID]` 用于设置你连接的 AP 的 ESSID。`$[ESSIDVAR]` 是将 `$[ESSID]` 转换为 bash 允许的变量名。

# 代码列表 2：pre/post 关联函数

```
preassociate() {

    # 以下添加两个配置变量 leap_user_ESSID
    # 和 leap_pass_ESSID。当它们为正在连接的
```



# ESSID 都配置了配置时，我们运行 CISCO LEAP 脚本

```bash
local user pass

eval user="${leap_user_${ESSIDVAR}}"

eval pass="${leap_pass_${ESSIDVAR}}"
```

```bash
if [ -n $user ]; then

    if [ -f /opt/cisco/bin/leapscript ]; then

        fi # LEAF loop, please emerge next-mis/cisco-aironet-client-utils

fi

info "*Waiting for LEAF Authentication on ${ESSID\\}"

if /opt/cisco/bin/leapscript ${user} ${pass} | grep -q "Login incorrect"

    warn "Login Failed for ${user}"

    return 1

fi

return 0

postcassage() {

    # 这个函数主要是为了完整性……我还没有

    # 构思出什么奇妙的方法来处理它 -

    return 0

}
```

注意：`${ESSID}` 和 `${ESSIDVAR}` 在 `predown()` 和 `postdown()` 中不可用。

## 6. 网络管理

### 6.a. 网络管理

如果你和你的电脑经常在外移动，可能并不总是能找到以太网线或接入接入点。我们可能希望在插入以太网线或发现接入点时，网络能够自动工作。

在这里，你可以找到你需要管理的内容。

> 注意：本文档仅讨论了 `ifplugd`，但你也可以查看如 `quickswitch` 等替代方案。

### 6.b. ifplugd

`ifplugd` 是一个守护进程，在插入或移除以太网线时启动或停止接口。它还可以管理与接入点的关联，或者在新的接入点进入范围时进行。

#### 代码列表 1：安装 ifplugd

```bash
# emerge sys-apps/ifplugd
```

`ifplugd` 的配置也相当简单。配置文件存储在 `/etc/conf.d/ifplugd`。运行 `ifplugd` 可查看变量作用的详情。

#### 代码列表 2：示例 ifplugd 配置

```bash
# 定义我们要监控的接口
INTERFACES="eth0"
AUTO="no"
BEEP="no"
IGNORE_FAIL="yes"
IGNORE_FAIL_POSITIVE="no"
IGNORE_RETRY="yes"
POLL_TIME="*"
DELAY_SEC="0"
DELAY_JOIN=""
API_MODE="auto"
SHUTDOWN="no"
WAIT_FOR="no"
MONITOR="no"
ARGS=""
```

针对指定接口的 `ifplugd` 额外参数。注意，当为接口设置如下变量时，全局变量将被忽略。

```bash
# 接口
MONITOR_wlan0=yes
DELAY_UP_wlan0=5
DELAY_DOWN_wlan0=5
```

本文的内容遵循知识共享 - 署名 / 相同共享协议许可。
