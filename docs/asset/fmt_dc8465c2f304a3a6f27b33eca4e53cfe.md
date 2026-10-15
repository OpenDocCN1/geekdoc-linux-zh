
io0:flags=2001000849UP,LOOPBACK,RUNNING,MULTICAST,IPv4,VIRTUAL>

tmu 832 index 1 inet 127.0.0.1 netmask ff000000

e1000g0:flags=1000843-UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500

index 2 inet 192.108.21.48 netmask fffff broadcast 192.108.21.255

```
```

solaris$ ifconfig e1000g0

e1000g0:flags=1000843-UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500

index 2 inet 192.108.21.48 netmask fffff broadcast 192.108.21.255

ether 0:14:4f:e6:1c

```

请注意，当以 root 身份运行时，`ifconfig` 会显示硬件地址，但以用户身份运行时则不会显示。

# Solaris DHCP 配置

```
solaris$ netstat -nr

Routing Table: IPv4

| Destination | Gateway | Flags | Ref | Use | Interface |
| :--- | :--- | :--- | :--- | :--- | :--- |
| default | 192.108.21.254 | UG | 1 | 9959 | |
| 192.108.21.0 | 192.108.21.48 | U | 1 | 4985 | e1000g0 |
| 127.0.0.1 | 127.0.0.1 | UH | 1 | 107 | lo0 |
```

```
solaris$ sudo route get google.com

route to: gw-in-f100.google.com

destination: default

mask: default

gateway: 192.108.21.254

interface: e1000g0

flags: <U,GATEWAY,DONE,STATIC>

recpipe sendpipe ssthresh rtt,ms rvar,ms hopcount mtu expire

0 0 0 0 0 1500 0
```

Solaris 包含一个 DHCP 客户端，并获得了最简单最合理的 DHCP 客户端配置奖：

```
solaris$ sudo ifconfig interface dhcp
```

它生效了！`ifconfig` 调用 `dhcpagent` 程序从 DHCP 获取接口参数，并用这些参数配置接口。你可以在 `ifconfig` 命令行中包含多个选项，以选择接口为主接口、设置超时、增加租约时间或显示接口状态。要手动配置 DHCP，只需运行：

```
solaris$ sudo ifconfig interface drop
```

如果你可能希望 DHCP 在启动时自动配置，那么这些都太棒了。你可以通过完全不为接口提供任何配置文件（因此依赖于自动配置，类似于 Linux 的 Network-Manager）或通过创建一个 `/etc/dhcp.interface` 文件来设置此。如果你喜欢，`dhcp.interface` 文件可以包含传递给 `dhcpagent` 的额外命令行参数。`hostname.interface` 文件必须存在；然而，它是空的。启动脚本将首先使用其内容配置接口。`dhcpagent` 从 DHCP 的视角管理接口。在其他任务中，它从 DHCP 服务器（默认网关、名称服务器等）协商租约值，并在它们不再需要时取消它们。如果一个通过 DHCP 配置的接口被手动重配置，`dhcpagent` 会收集信息并将其放入 `resolv.conf` 等。它将错误发送到 syslog。使用 `-d` 标志可以获得调试级别的输出。你可以检查 `/etc/dhcpinfo` 文件以查看特定接口的配置。然而，`interface.dh` 的存在并不意味着 `dhcpagent` 正在控制接口——租约可能过期。

# ndd: Solaris 的 TCP/IP 和接口调优

Solaris 的 `ndd` 命令配置运行系统的 TCP/IP 栈。也许“重配置”这个词太重了；每个模块都可以被检查，并在某些情况下可以动态调整。基本语法是：

`ndd [-set] device variable [value]`

如果你提供参数 `?`，`ndd` 返回驱动理解的变量列表。如果你提供变量名称，`ndd` 返回该变量的值。如果你使用 `-set` 标志并提供值，指定的变量将被设置为该值。遗憾的是，`ndd` 手页没有告诉你可能的设备名称，也没有告诉你必须在某些设备（例如 ip 和 eth）上以 root 权限运行 `ndd`，而在其他设备（tcp 和 udp）上不需要。表 14.10 提供了一个快速参考。

# 表 14.10 可用 Solaris ndd 命令探测的设备

| 设备 | 描述 | 变量名 |
| :--- | :--- | :--- |
| /dev/tcp | TCP协议变量 | tcp_* |
| /dev/udp | UDP协议变量 | udp_* |
| /dev/ip | IP协议变量 | ip_* 和 ip6_* |
| /dev/icmp | ICMP协议变量 | icmp_* |
| /dev/rawip | 等于 /dev/icmp | icmp_* |
| /dev/arp | ARP协议变量 | arp_* |

`/dev/ip` 类别中的接口特定变量名。例如，`e1000g0:ip_forwarding` 控制 `/dev/e1000g0` 上的 IP 转发。还有一个全局的 `ip_forwarding` 变量。

# Solaris 安全

表 14.11 显示了 Solaris 对各种网络问题的默认行为。有关这些行为影响的简要描述，请参见从第472页开始的安全问题。你可以使用 `ndd` 调整大部分这些。

表 14.11 Solaris 相关网络行为

| 特性 | 默认 | ndd 变量 |
| :--- | :--- | :--- |
| IP 转发 | off | ip_forwarding |
| ICMP 重定向 | obeys | 无法更改 |
| 源路由 | ignores | ip_forward_src_routed |
| 广播 ping (响应) | on | ip_respond_to_echo_broadcast |
| 广播 ping (转发) | off | ip_forward_directed_broadcasts |

a 你只能修改条目的生存时间。

# Solaris 防火墙与过滤

正如安全问题部分提到的，你通常不应使用 UNIX、Linux 或 Windows 设备作为防火墙或 NAT 网关。应使用专用网络硬件。Solaris 过去通过不包含任何过滤软件很容易遵循这一规则，但 Darren Reed 的免费 IPFilter 软件已整合到基础发行版。如果你必须使用基于 UNIX 的过滤器，这是一个很好的选择——它一直是我们 Solaris 附加过滤器中最喜欢的。

许多变量名是相同的，因此你可以部分绕过 Sun 简化的 `ndd` 手页。接口特定选项（如链路速率、自动协商和巨型帧支持）也通过 `ndd` 设置；直接在接口文件上运行 `ndd`（例如 `/dev/e1000g0`）。遗憾的是，Sun 设置此连接使得配置参数名称取决于特定驱动，没有通用的方法来将网络接口锁定在 100 Mbps。

要更改速率，你需要识别用于速率的可写“能力”变量（通常以 `_cap` 命名），并关闭（设置为零）所有不允许的。关闭 `_autoneg_cap` 变量以禁用自动协商。例如，以下脚本将实验室机器之一的 `/dev/e1000g0` 设置为 100 Mbps 全双工：

```
#!/bin/sh

ndd -dev/e1000g0 adv_autoneg_cap 0

ndd -dev/e1000g0 adv_1000fdx_cap 0

ndd -dev/e1000g0 adv_100fdx_cap 1

ndd -dev/e1000g0 adv_1000hdx_cap 0

ndd -dev/e1000g0 adv_10fdx_cap 0

ndd -dev/e1000g0 adv_10hdx_cap 0
```
