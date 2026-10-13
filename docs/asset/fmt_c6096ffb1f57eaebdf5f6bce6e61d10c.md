
- `aftype` 参数指的是接口使用的地址族（协议）。`IP` 是默认值。选项包括下一代（6 代）互联网协议 `IPv6`、业余无线电包 `ax25`、Appletalk `2 ddp` 以及 Novell 的部分兼容 `IPX`。（我们在书中专门使用 `TCP/IP`，但为了完整性提到了其他）。
- `up/down`: 这两个选项开启或关闭接口。当你对设备进行故障排除并查看更改的效果时，它们非常有用。
- `promise`: 此选项用于开启或关闭混杂模式。当处于混杂模式时，接口将其遇到的所有网络数据包传递给高层网络层。混杂模式允许你的计算机作为网络嗅探器运行。网络嗅探是指监听网络设备所暴露的所有网络流量的过程。嗅探可用于排排除网络问题和监听他人的通信。

使用此模式时要小心。许多组织认为处于混杂模式的网卡（`NIC`）是黑客存在的证据。

#### netstat

`netstat` 程序显示路由表、接口统计数据和伪装连接的信息，这对于调试网络问题非常有价值。（你也可以使用此命令获取其他网络连接的信息。）

#### nmap

该程序属于称为端口映射器的工具类。`nmap` 向目标（或多个目标）发送处于各种扭曲状态的数据包，并检查其返回的数据包。响应的数据包会被 `nmap` 收集并分析，以确定有关该机器的信息。

#### ping

`ping` 是一个简单且非常有用的程序，它发送 `ICMP` 数据包并等待响应。例如，如果你想找出网络上另一台计算机（`IP` 为 `192.168.1.101`）是否活跃，请运行：

```
ping 192.168.1.101
```

以下代码显示了典型的响应：

```
PING atlas.paunchy.net (192.168.1.101) from 192.168.1.10 : 56(84) bytes of data.
64 bytes from puma.paunchy.net (192.168.1.101): icmp_seq=0 ttl=255 time=78 use
64 bytes from puma.paunchy.net (192.168.1.101): icmp_seq=1 ttl=255 time=73 use c
64 bytes from puma.paunchy.net (192.168.1.101): icmp_seq=2 ttl=255 time=63 use c
```

此 `ping` 会话显示地址为 `192.168.1.101` 的计算机是存活且活跃的。

如果你没有收到 `ping` 的响应，该计算机可能已关闭、断开网络连接、配置不当等。

## 第 2 章：配置 Red Hat Linux 网络

第 5 章描述了一些使用 `ping` 的基础故障排除技术。

#### redhat-config-network-druid/

`redhat-config-network-cmd`

Red Hat 有一个名为 `redhat-config-network-druid` 和 `redhat-config-network-cmd` 的网络配置工具。（`druid` 版本是指工具的图形界面，而 `cmd` 是命令行版本。）该工具可以配置从以太网适配器到调制调器的任何网络设备。你可以通过点击 `GNOME` 面板上的主菜单->网络配置按钮来访问网络配置。该工具自言易懂，系统管理员学习和使用它应该没有困难。

#### route

`route` 程序用于配置、删除和显示路由。使用此命令创建或修改路由时，使用以下语法：

```
route [-v] [-A family add [-net]-host] target [netmask]\Nm [gw Gw] [metric N] [mss M] [window W] [irtt I]
[reject] [mod] [dyn] [reinstate] [dev] if
```

上述许多选项仅用于特殊情况，因此我们不讨论它们。我们发现以下选项很有用：

- `add [-net]-host`: 添加子网地址（例如 `192.168.1.0`）或特定的主机地址（`192.168.1.1`）。通常情况下，你使用网络地址来创建默认路由，例如通往互联网。

例如，命令 `route add -net default gw 192.168.1.254` 设置了一个路由，捕获所有不匹配任何特定路由的 `IP` 数据包，如下所示`-net default` 特殊情况经常被用于创建一个将数据包导向外部子网（互联网）的路由。我们使用此功能将数据包从我们的私有网络导向我们的互联网网关。

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| default | 192.168.1.254 | 0.0.0.0 | | 0 | 0 | | eth0 |

- `target`: 目标是 `add` 选项目的地的 `IP` 地址。在前述项目符号的示例中，目标是未匹配的 `IP` 地址（默认目标）。在设置到本地子网或主机的路由时，`target` 参数描述的是本地子网地址。例如，你需要告诉 Linux 如何路由发往本地子网的数据包。命令 `route add -host 192.168.1.0` 确认了这一点并设置了如下路由：

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.1.0 | * | 255.255.255.0 | U | 0 | 0 | | eth0 |

偶尔，你需要创建一个通往特定主机的路由。在这种情况下，使用 `-host` 选项。例如，命令 `route add -host 192.168.32.1` 创建了一个将数据包导向外部子网（互联网）的路由。我们使用此功能将数据包从我们的私有网络导向我们的互联网网关。

- `gw`: 网关选项。
- `dev`: 接口选项。
- `target`: 目标选项。
- `net`: 网络选项。
- `host`: 主机选项。
- `metric`: 跃数选项。
- `mss`: `mss` 选项。
- `window`: 窗口选项。
- `irtt`: `irtt` 选项。
- `reject`: 拒绝选项。
- `mod`: 模式选项。
- `dyn`: 动态选项。
- `reinstate`: 恢复选项。

#### sysctl

`sysctl` 程序配置并显示 `/proc/sys` 中的内核参数。它可以设置或重置网络功能，例如转发、分片和源检查。你可以手动或通过编辑 `/etc/sysctl.conf` 来完成这一切。

## 第 2 章：配置 Red Hat Linux 网络

`sysctl -a` 命令显示所有参数。例如，如果你想查看与转发相关的所有参数，运行以下命令：

```
sysctl -a | grep forward
```

以下输出是针对具有两个接口的计算机的：

```
net.ipv4.conf.eth0.mc_forwarding = 0
net.ipv4.conf.eth0.forwarding = 0
net.ipv4.conf.eth1.mc_forwarding = 0
net.ipv4.conf.eth1.forwarding = 0
net.ipv4.conf.lo.mc_forwarding = 0
net.ipv4.conf.lo.forwarding = 0
net.ipv4.conf.default.mc_forwarding = 0
net.ipv4.conf.default.forwarding = 0
net.ipv4.conf.all.mc_forwarding = 0
net.ipv4.conf.all.forwarding = 0
net.ipv4.ip_forward = 0
```

大多数这些参数涉及单个接口的转发。如果你正将 `RHL` 计算机用路由器或互联网网关，那么就需要转发。在这种情况下，你对 `ipv4.ip_forward` 参数感兴趣。例如，通过输入以下命令（等号周围不要留任何空格），可以开启适当的参数，例如两个以太网接口：

```
sysctl -w net.ipv4.ip_forward=1
```

> TIP 你用 `sysctl` 能做的所有事情都可以手动完成。例如，如果你想显示转发状态，请输入命令 `cat /proc/sys/net/ipv4/ip_forward`。要更改参数，你必须向其发送二进制值（0 或 1），例如 `echo "1" > /proc/sys/net/ipv4/ip_forward`。

#### tcpdump

你使用 `tcpdump` 检查 `IP`、其他协议以及数据包的头部。通过查看遍历网络的数据包的源地址、目的地址和端口，你可以分析网络。此功能在试图弄防火墙无法正常工作时特别有用。

#### modprobe
