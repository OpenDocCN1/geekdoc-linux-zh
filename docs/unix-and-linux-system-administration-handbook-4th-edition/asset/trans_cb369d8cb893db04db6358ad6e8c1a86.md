
这些参数通过 **dhcpinfo** 命令提供给系统使用。服务管理脚本会查询 **dhcpinfo** 来获取各种信息，然后将这些信息作为 **route** 命令的参数、写入 **resolv.conf** 文件等。

**dhcpagent** 将错误信息通过 syslog 发送，设施为 daemon，优先级从 info 到 critical。使用 **-d** 标志可以输出调试级别的 syslog 信息。

你可以查看 **/etc/dhcp** 中的文件，以了解特定接口的配置。然而，某个接口存在 **interface.dhc** 文件，并不一定意味着 **dhcpagent** 正在控制该接口——租约可能已经过期。

## ndd：用于 Solaris 的 TCP/IP 和接口调优

Solaris 的 **ndd** 命令可以在运行中的系统上重新配置 TCP/IP 协议栈。也许“重新配置”这个词过于强烈；每个模块都暴露了一些参数，你可以查看这些参数，有时还可以即时调整。

基本语法为：

```
ndd [-set] device ? | variable [value]
```

如果你提供参数 **?**（必须用 **\?** 形式进行转义，以免被 shell 解释），**ndd** 会返回指定设备驱动所支持的变量列表。如果你提供 *变量* 的名称，**ndd** 会返回该变量的值。如果你使用 **-set** 标志并提供 *值*，则指定的变量会被设置为该值。

遗憾的是，**ndd** 的手册页既没有告诉你设备的可能名称，也没有告诉你在某些设备（例如 **ip** 和 **hme**）上必须使用 root 身份运行 **ndd**，而在另一些设备（例如 **tcp** 和 **udp**）上则不需要。表 14.10 为你提供了一份快速速查表。

### 表 14.10 可以使用 Solaris 的 ndd 命令探测的设备

| 设备 | 描述 | 变量名 |
|---|---|---|
| `/dev/tcp` | TCP 协议变量 | `tcp_*` |
| `/dev/udp` | UDP 协议变量 | `udp_*` |
| `/dev/ip` | IP 协议变量 | `ip_*` 和 `ip6_*` |
| `/dev/icmp` | ICMP 协议变量 | `icmp_*` |
| `/dev/rawip` | 与 `/dev/icmp` 相同 | `icmp_*` |
| `/dev/arp` | ARP 协议变量 | `arp_*` |

**/dev/ip** 类别中的接口特定变量名控制着特定网络接口上的 IP 转发。例如，e1000g0:ip_forwarding 控制 **/dev/e1000g0** 上的 IP 转发。还有一个全局的 ip_forwarding 变量。

如果你可以访问 HP-UX 机器，请在那里使用 **-h** 标志（用于帮助）运行 **ndd**，它会给出设备名、变量名以及每个变量的含义。许多变量名是相同的，因此你可以在一定程度上弥补 Sun 的 ndd 手册页过于简略的不足。

接口特定选项（如链路速度、自动协商和巨帧支持）也可以通过 ndd 设置；直接在接口的设备文件（例如 /dev/e1000g0）上运行 ndd 即可。遗憾的是，Sun 设置这种约定的方式使得配置参数的名称依赖于具体的驱动程序，因此并没有一个通用的方法来，比如说，将网络接口锁定在 100 Mb/s。

要改变速度，你需要找出每个速度对应的可写“能力”变量（通常命名为 *_cap），然后关闭（设为 0）所有你不希望允许的速度。同时也要关闭 *_autoneg_cap 变量，以禁用自动协商。

例如，以下脚本将我们实验室某台机器上的 /dev/e1000g0 设置为 100 Mb/s 全双工模式：

```
#!/bin/sh
ndd -set /dev/e1000g0 adv_autoneg_cap 0
ndd -set /dev/e1000g0 adv_1000fdx_cap 0
ndd -set /dev/e1000g0 adv_1000hdx_cap 1
ndd -set /dev/e1000g0 adv_100hdx_cap 0
ndd -set /dev/e1000g0 adv_10fdx_cap 0
ndd -set /dev/e1000g0 adv_10hdx_cap 0
```

## Solaris 安全性

表 14.11 展示了 Solaris 在各种敏感网络问题上的默认行为。关于这些行为影响的简要说明，请参阅第 472 页开始的“安全问题”一节。你可以使用 ndd 调整其中的大多数设置。

### 表 14.11 Solaris 中与安全相关的网络行为

| 特性 | 默认值 | ndd 变量 |
|---|---|---|
| IP 转发 | 关闭 | ip_forwarding |
| ICMP 重定向 | 遵循 | 无法更改* |
| 源路由 | 忽略 | ip_forward_src_routed |
| 广播 ping（响应） | 开启 | ip_respond_to_echo_broadcast |
| 广播 ping | 关闭 | ip_forward_direct_broadcasts |

a. 你只能修改条目的生存时间（TTL）。

## Solaris 防火墙和过滤

如“安全问题”一节所述，你通常不应使用 UNIX、Linux 或 Windows 机器作为防火墙或 NAT 网关，而应使用专用的网络硬件。过去，Solaris 不包含任何过滤软件，因此很容易遵循这一规则；但现在 Darren Reed 的免费 IPFilter 软件已被捆绑到基本发行版中。如果你必须使用基于 UNIX 的过滤器，这是一个不错的选择——它一直是我们最喜欢的 Solaris 附加过滤器。
