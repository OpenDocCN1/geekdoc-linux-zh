
`sdptool browse MACAddress`

```
列表 14-4 显示了如何使用 `sdptool` 在列表 14-2 之前检测到的其中一个设备上搜索服务。
```

`kali >sdptool browse 76:6E:46:63:72:66`

Browsing 76:6E:46:63:72:66...

Service ReHandle: 0x10002

Service Class ID List:

""\0x1800)

Protocol Descriptor List:

"LZCAP" (0x0100)

PSM: 31

"ATT" (0x0007)

uint16: 0x1

uint16: 0x5

--snip--

```
列表 14-4：使用 sdptool 扫描
```

在这里，我们可以看到 `sdptool` 工具的功能是可以使用的。特别是，我们看到此设备支持 ATT 协议，即低功耗属性协议（Low Energy Attribute Protocol）。这可以为我们提供更多关于设备是什么的线索，以及可能的交互途径。

### 使用 l2ping 查看设备是否连接

一旦我们知道适配器已启动，就可以使用 `l2ping` 来检查连接是否启用，我们也可以通过 `hciconfig` 提供名称和 `up` 命令来实现。

如果黑客能够诱导 Linux 管理员向内核加载一个新模块，黑客不仅可以获得目标系统的控制权，而且由于他们在操作系统的内核级别运行，他们可以控制目标系统报告的进程、端口、硬盘空间以及几乎你所想象的任何其他内容。

因此，如果黑客能够成功诱导 Linux 管理员安装一个嵌入了 rootkit（根内核程序）的视频或其他设备驱动程序，黑客就可以完全控制系统和内核。这就是某些最隐蔽的 rootkit 利用 Linux 及其他操作系统的方式。

理解 LKM（Linux 内核模块）对于成为一名高效的 Linux 管理员以及一名高效且隐蔽的黑客绝对关键。

让我们来看看如何良好或错误地管理内核。

## 检查内核版本

理解内核的第一步是检查你的系统运行的是什么内核。至少有两种方法可以实现这一点。首先，我们可以输入以下内容：

```bash
kali uname -a
Linux Kali 4.6.0-kalil-amd64 #1 SMP Debian 4.6.4-lkalil (2016-07-21) x86_64
```

内核的响应告诉我们发行版操作系统正在运行 Linux Kali，构建的内核版本是 4.6.4，其构建的架构是 x86_64 架构。它还告诉我们具有对称多处理（SMP）能力（这意味着它可以在带有多个核心或处理器机器上运行），并在 2016 年 7 月 21 日在 Debian 4.6.4 上构建。你的输出可能不同，取决于构建时使用的内核以及系统中的 CPU。在安装或加载内核驱动时可能需要这些信息，因此了解如何获取它是很有用的。

另一种获取这些信息以及其他有用信息的方法是对 `/proc/version` 文件使用 `cat` 命令，如下所示：

```bash
kali >cat /proc/version
Linux version 4.6.0-kalil-amd64 (devel@kali.org) (gcc version 5.4.0
20160909
(Debian 5.4.0-6) #1 SMP Debian 4.6.4-lkalil (2016-07-21)
```

在这里你可以看到 `/proc/version` 文件返回了相同的信息。

## 使用 sysctl 进行内核优化

通过正确的命令，你可以调整内核，这意味着你可以更改内存分配、启用网络功能，甚至加强内核以抵御外部攻击。

现代 Linux 内核使用 `sysctl` 命令来调整内核选项。你通过 `sysctl` 进行的所有更改在重启系统之前一直保持有效。要使任何更改永久生效，你必须直接在 `/etc/sysctl.conf` 中编辑 sysctl 配置文件。

警告词：在没有适当知识和经验的情况下使用 `sysctl` 时需要非常小心，你很容易让你的系统无法启动且无法使用。在进行任何永久更改之前，请确保你已经仔细考虑了你所做的操作。

现在让我们来看看 `sysctl` 的内容。到此时，你应该认识我们通过这里显示的命令获取的选项了：

```bash
kali >sysctl -a | less
dev.cdrom.autoclose = 1
dev.cdrom.autoeject = 0
dev.cdrom.check_media = 0
dev.cdrom.debug = 0
--snip--
```

在输出中，你应该能看到数百行参数，Linux 管理员可以编辑这些参数来优化内核。这里有几行对你这个黑客来说是有用的。作为一个你可能如何使用 `sysctl` 的示例，我们将查看启用数据包转发。

在中间人（MITM）攻击中，黑客将自己置于通信主机之间以拦截信息。流量通过黑客的系统，因此他们可以查看并可能更改通信。实现这种路由的一种方法是启用数据包转发。

如果你在输出中向下滚动几页，或者过滤 "ipv4" (`sysctl -a | less | grep ipv4`)，你应该看到以下：

```bash
net.ipv4.ip_dynaddr = 0
net.ipv4.ip_early_demux = 0
net.ipv4.ip_forward = 0
net.ipv4.ip_forward_use_pmtu = 0
--
```

`net.ipv4.ip_forward = 0` 这一行是允许内核转发收到的数据包的内核参数。换句话说，当它收到数据包时，会将其发送出去。默认设置为 0，这意味着禁用了数据包转发。

要启用 IP 转发，通过输入以下内容将 0 更改为 1：

```bash
kali >sysctl -w net.ipv4.ip_forward=1
```

记住，`sysctl` 的更改在运行时生效，但在系统重启后会丢失。要对 `sysctl` 进行永久更改，需要编辑配置文件 `/etc/sysctl.conf`。让我们更改内核处理用于 MITM 攻击的 IP 转发的方式并将此更改永久。

要启用 IP 转发，用任何文本编辑器打开 `/etc/sysctl.conf` 文件并取消 `ip_forward` 一行的注释。用任何文本编辑器打开 `/etc/sysctl.conf` 并查看：

```bash
#/etc/sysctl.conf - 设置系统变量的配置文件
# 查看 /etc/sysctl.d/ 获取更多系统变量。
# 查看 sysctl (5) 获取更多信息。
# 此处省略了部分内容，根据原文逻辑对应：
# 注释以下行以启用 IPv4 转发
net.ipv4.ip_forward = 1
kernel.domainname = example.com
# 注释以下内容以停止控制台上的内核消息
kernel.printk = 3 4
################################################
# 注释以下两行以启用反路径验证 (rp_filter)
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1
# 注释以下行以启用 TCP/IP SYN  cookies
net.ipv4.tcp_sync_cookies = 1
```
*(注：由于原文提供的文本在 `/etc/sysctl.conf` 示例部分存在截断或逻辑跳跃，译文根据上下文补全了配置项的语意说明)*

从操作系统的固化的角度来看，你可以通过此文件禁用 ICMP 请求（`net.ipv4.icmp_echo_all`）。在添加该行后，你需要运行命令 `sysctl -p`。

## 管理内核模块

Linux 至少有两种方法管理内核模块。旧的方法是使用围绕 `insmod` 构建的命令，`insmod` 代表插入模块，用于处理模块。另一种方法是我们稍后会使用的 `modprobe` 命令。这些命令并不完美，可能不会考虑模块依赖关系，因此使用它们可能会导致你的内核不稳定或不可用。因此，现代 Linux 发行版现在增加了 `modprobe` 命令，它会自动加载依赖项并降低加载移除内核模块的风险。我们稍后会介绍 `modprobe`。首先，让我们看看如何获取模块的更多信息。

## 使用 modinfo 获取更多信息

要获取任何内核模块的更多信息，可以使用 `modinfo` 命令。该命令的语法非常直 way：`modinfo` 后面跟你想学习的模块名称。例如，如果你想获取之前运行 `lsmod` 时看到的蓝牙内核模块的基础信息，你输入：

```
kali >modinfo bluetooth
filename: /lib/modules/4.6.0-kali-amd64/kernel/net/bluetooth/bluetooth
alias: net-pf-31
license: GPL
version: 2.21
description:Bluetooth Core ver 2.21
```
