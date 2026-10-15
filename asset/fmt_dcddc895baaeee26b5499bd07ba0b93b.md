
TX 数据包:12420 错误:0 丢弃溢出:0 载:0

冲突:0 发送队列:10000

RX 字节:569194 (54.6 KiB) TX 字节:250287 (244.4 KiB)

中断:3 基地址:0x0100

lo 链路:本地回环

inet 地址:127.0.0.1 掩码:255

inet6::1/68 范围:主机

UP RUNNING MTU:16384 度量:1

RX 数据包:24560 错误:0 丢弃溢出:0 帧:0

TX 数据包:24560 错误:0 丢弃溢出:0 载:0

冲突:0 发送队列:10000

RX 字节:2891581 (2.7 MiB) TX 字节:2891581 (2.7 MiB)

此输出显示三个网络接口（lo）和两个以太网卡（eth0 和 eth1）——当前在该系统上活动。对于每个接口，你可以看到 IP 地址，以及交付和发送数据包的统计信息。如果 Linux 系统正在运行拨号 PPP 链路，在输出中还会看到 ppp0 接口的条目。

## 检查 IP 路由表

另一个网络配置命令 `/sbin/route` 在你不带命令行参数运行它时，它会提供状态信息。如果你在检查到另一个主机（你通过 IP 地址指定该主机）的连接时遇到困难，请检查 IP 路由表查看是否指定了网关。检查网关的路由表，确保通往外部网络的路径出现在路由中。

`/sbin/route` 命令的典型输出如下：

```
内核 IP 路由表
目的地 网关 标志 度量 Ref 使用 接口
192.168.0.0 * 255.255.255.0 0 0 0 eth0
192.168.0.0 * 255.255.255.0 0 0 0 eth1
169.254.0 * 255.255.255.0 0 0 0 default
192.168.0.1 0.0.0.0 0 0 0
```

如此表所示，本地网络使用 eth0 和 eth1 以太网接口，默认网关是 eth0 接口。默认网关是一个处理发送到 Linux 系统所在网络之外网络的数据包的路由项。在本示例中，发送到任何非以 192.168.0.0 开头的网络的数据包都会发送到网关——192.168.0.1。网关将这些数据包转发到其他网络（当然，假设网关连接到另一个网络，最好是互联网）。

www-it-ebooks.info

## 检查与主机的连通性

要检查与特定主机的网络连接，`ping` 命令是一个广泛使用的 TCP/IP 工具，它使用一系列互联网控制消息协议（ICMP，发音为 EYE-com）消息。ICMP 为主机响应的显回消息提供了支持。使用 ICMP 消息和回复，`ping` 可以确定另一个系统是否存活，并计算与系统通信的往返延迟。

下面的示例展示了我如何通过 `ping` 查看我网络上的某个系统是否存活：

```
ping 192.168.0.1
```

以下是 cmd 在我的家庭网络上显示的内容：

```
PING 192.168.0.1 (192.168.0.1): icmp_seq=1 ttl=63 time=0.256 ms
44 bytes from 192.168.0.1: icmp_seq=2 time=0.267 ms
44 bytes from 192.168.0.1: icmp_seq=3 time=0.272 ms
44 bytes from 192.168.0.1: icmp_seq=4 time=0.267 ms
44 bytes from 192.168.0.1: icmp_seq=5 time=0.275 ms
---
192.168.0.1 statistics
5 packets transmitted, 5 received, 0% packet loss, time 267ms
```

# 198 检查 TCP/IP 网络

输出内容提供了关于发生情况的一些线索，每行显示有关一个网络数据包的信息。每行都以时间戳开头，随后是数据包的详细信息（如源地和位置等信息）。我在这里不解释这些细节，但你可以输入 `tcpcdump` 来获取更多细节（更重要的是，看看你还可以通过其他方式使用 `tcpdump`）。

如果 Debian 中没有安装 `tcpcdump`，请使用 `apt-get tcpcdump` 来安装它。

你可以在 Linux 中使用另一个名为 Wireshark 的数据包嗅器。要了解更多关于 Wireshark 的信息，请访问 www.wireshark.org。

## GUI 工具

你可以通过多种图形化界面检查网络状态。其中一种是使用系统监控（System Monitor），如图 4-1 所示。除了查看网络负载外，你还可以点击“进程”（Processes）来查看各种进程的状态。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_217_0.png)

图 4-1：系统监控。

## 在启动时配置网络

在每次启动系统时自动启动网络是有意义的。为了实现这一点，各种启动脚本必须包含适当的命令。除了配置网络（在安装期间或稍后使用网络配置）之外，你不需要进行任何特殊操作。然而，如果网络在启动时报错，你可以通过检查我在此节中提到的文件来排查故障。

在 Debian、Ubuntu 和 Xandros 中，`/etc/network/interfaces` 描述了系统中可用的网络接口，而 `/sbin/ifup` 命令在系统启动时激活这些接口。以下是一个典型的 Debian 系统的 `/etc/network/interfaces` 文件内容：

```
# 此文件描述了系统上可用的网络接口
# 以及如何激活它们。更多信息，请参阅 interfaces(5)。
## 回环网络接口
auto lo
iface lo loopback
## 主网络接口
auto eth0
iface eth0 inet dhcp
```

`auto eth0` 行表示你可以通过由系统启动脚本调用的 `ifup -a` 命令初始化来启用以太网接口。`ifup eth0 inet dhcp` 行识别出以太网是一个通过动态主机配置协议（DHCP）配置的 TCP/IP 网络接口。

在 Debian 中，网络激活脚本使用 `/etc/sysconfig` 目录中的一组测试文件来激活 `/etc/sysconfig/network` 文件定义的变量。例如，脚本会检查是否激活网络。在 `/etc/sysconfig/network` 中，你会看到一行带有 `NETWORK` 变量：

```
NETWORK=yes
```

只有当 `NETWORK` 变量设置为 `yes` 时，网络才会激活。`/etc/sysconfig/network-scripts` 目录中的许多脚本激活特定的网络接口。例如，激活以太网接口的配置 `network-scripts/ifcfg-eth0`。以下是一个典型的 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件包含的内容：

```
DEVICE=eth0
BOOTPROTO=dhcp
HWADDR=00:08:74:E5:C1:06
ONBOOT=yes
TYPE=Ethernet
```

![](img/71f80d7808bf5b5ad1239cc29be7bab2_218_0.png)

![](img/71f80d7808bf5b5ad1239cc29be7bab2_218_1.png)

| 第三卷 第 4 章 | 管理网络 |

| :--- | :--- |

| www.it-ebooks.info |

## 200 在启动时配置网络

`DEVICE` 行提供了网络设备名称。`BOOTPROTO` 变量设置为 `dhcp`，表示使用 DHCP 动态获取 IP 地址。`ONBOOT` 变量说明此网络接口在 Linux 中是否激活。如果你的 PC 有一个以太网卡且你想在启动时激活 `eth0` 接口，则必须将 `ONBOOT` 设置为 `yes`。`/etc/sysconfig/network-scripts` 目录下的 `ifcfg-eth0` 配置文件只有在你的 PC 有以太网卡且内核已检测并加载了该卡的特定驱动程序时才有效。

在 Linux 中，网络信息保留在 `/etc/sysconfig/network` 目录中以 `ifcfg` 开头的文件。对于以太网接口，配置文件名以 `ifcfg-eth-id-` 开头，后跟以太网卡的唯一硬件地址。以下是典型配置文件中的关键行：

![](img/71f80d7808bf5b5ad1239cc29be7bab2_219_0.png)

```
BOOTPROTO='dhcp'
STARTMODE='auto'
```

`BOOTPROTO='dhcp'` 行表示该接口使用 DHCP 设置，而 `STARTMODE='auto'` 意味着接口在系统启动时初始化。

在 KDE 中，你可以在搜索框中输入“Session Management”（会话管理）来启动控制中心并配置系统的默认选项，如图 4-2 所示。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_219_1.png)

图 4-2：会话管理界面。
