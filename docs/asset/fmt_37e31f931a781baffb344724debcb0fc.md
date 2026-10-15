
# CS 系部门网络掩码数据库

```
# Network            netmask
#=================================

128.138.0.0         255.255.255.192      # 部门默认
128.138.192.64      255.255.255.192      # drag
128.138.192.192     255.255.255.192      # csops
128.138.193.0       255.255.255.224      # database
128.138.193.32      255.255.255.224      # bcrg
128.138.198.0       255.255.255.0        # slip
```

第一行为 B 类地址 `128.138.0.0` 设置了默认的 `/26`，这在默认情况下会被覆盖。所有网络都列出，尽管许多使用的是默认值，从技术上讲可以省略。在示例示例的系统中，`netmasks` 文件是集中维护并分发到所有主机的。没有任何主机在所有网络上都有接口。

接口配置必须在启动过程早期进行，即在网络信息服务器启动之前。在各种服务启动后，Solaris 会多次重新执行 `ifconfigs`（其理论是，额外的服务可能会为 `ifconfig` 命令提供更好的参数）。

- `20.` 网络接口必须使用 `ifconfig plumb` 进行范围化以使其可访问。在进行手动配置时，你可能需要运行此命令。

- `21.` Solaris `7` 上的 `netmasks` 页面已损坏；在后续版本中已修复。

## Solaris 的 DHCP 配置

Solaris 包含一个 DHCP 客户端，并获得了最简单最合理的 DHCP 配置奖：

```
ifconfig interface dhcp
```

它可以工作！它只需调用 DHCP 程序从 DHCP 获取接口参数并进行配置。你可以在 `ifconfig` 命令行中包含多个选项，以指定主接口、设置超时、增加租约时间或显示接口状态。要手动取消 DHCP，只需运行

```
ifconfig interface drop
```

这非常棒，你可能希望在启动时自动查询 DHCP。这种行为必须为每个接口单独请求。为此，创建一个与 `/etc/hostname.interface` 对应的 `/etc/dhcp.interface` 文件。如果你喜欢，`dhcp.interface` 文件可以包含传递给 `ifconfig` 命令的额外命令行参数。

`hostname.interface` 文件必须存在才能对接口进行范围化（`plumb`）；但如果你使用 DHCP，可以是空的。启动脚本将首先使用其内容配置接口，然后通过 DHCP 重新配置接口。

你可以使用 `dhcpinfo` 命令查看由 DHCP 服务器提供的参数。你也可以查看 `/etc/dhcp/interface.dhc`，它存储了指定接口的当前配置。

`dhcpagent` 从 DHCP 的角度管理接口。除了其他任务外，它还协商租约并在不再需要时取消租约。如果一个通过 DHCP 配置的接口后来被手动配置，`dhcpagent` 将停止对该接口的管理。

# 第 13 章 TCP/IP 网络

`dhcp` 从 DHCP 服务器获取值（默认网关、域名、名称服务器等），并且不会直接对大部分这些值进行操作。相反，它会每个接口从 `/etc` 中的相应文件中检索各种信息，例如 `/etc/resolv.conf`。DHCP 使用 syslog 设施 "`daemon`" 传输错误；它还将这些错误写入 `/dev/console`。默认情况下，除非使用命令行标志 `-N` 显式开启，否则它会丢弃错误（警告、信息消息等）。如果 `N` 为 `1`，则记录警告；如果 `N` 较大，则也会记录更高优先级的日志。如果你使用 DHCP `-U`，它会转储其租约的状态。你可以检查 `/etc/interfaces` 来查看特定接口的配置。然而，存在接口这一事实并不意味着 DHCP 正在管理该接口——租约可能已经过期。

## Solaris 的动态重配置与调优

Solaris `ndd` 命令允许你在正在运行的系统上重新配置设备。也许“重新配置”这个词太重了；每个驱动程序都提供了几个参数的访问权限，这些参数可以检查并在某些情况下动态进行调整。能够选取特定参数的值是非常用的，这正是我们经常使用 `ndd` 来确定以太网卡运行 `10 Mb/s` 还是 `100 Mb/s` 或是否在转发数据包的原因。Solaris `ndd` 的语法与 HP-UX 的 `ndd` 类似，但它的文档糟糕得多。手页中的基本语法为：

```
ndd [-set] device variable
```

如果你提供参数 `?`（这必须受到大多数 shell 的保护？），`ndd` 会返回驱动程序为指定设备理解的变量列表。如果你使用 `-set` 标志并提供一个值，则指定的变量将被设置为该值。遗憾的是，`ndd` 手页忽略了告知你可能的设备名称，也没有告诉它最好在某些设备（例如 `ip`）上运行，而在其他设备（`tcp` 和 `udp`）上不要运行。`ndd` 提供了一个晦涩难懂的错误信息，如：

```
could't push 'ip', No such device or address
```

当你尝试以用户身份运行它时，它要求具有 root 权限。表 `13.16` 列出了我们通过使用 `ndd` 能够发现的设备。大多数现代以太网卡可以在 `10 Mb/s` 或 `100 Mb/s` 下工作。随着我们的本地网络从共享 `10 Mb/s` 迁移到交换式 `100 Mb/s`，我们经常有机会询问机器的网络接口当前运行在什么速度上。

# UNIX 系统手册

### 表 13.16 使用 Solaris ndd 命令可以探测的设备

| 设备 | 描述 | 变量名 |
| :--- | :--- | :--- |
| `/dev/tcp` | TCP 协议变量 | `tcp_*` |
| `/dev/udp` | UDP 协议变量 | `udp_*` |
| `/dev/ip` | IP 协议变量 | `ip_*` |
| `/dev/icmp` | ICMP 协议变量 | `icmp_*` |
| `/dev/rawip` | 与 `/dev/icmp` 相同 | `icmp_*` |
| `/dev/arp` | ARP 协议变量 | `arp_*` |
| `/dev/hme` | hme 以太网变量 | 无特定模式 |

这里有一个 Todd Williams 编写的脚本，它使用 `ndd` 来确定以太网接口的配置：它产生如下输出：

`ethernet is UP, running 10 Mbps HALF duplex`

这是以下变量的英文翻译：

- `link_status = 1` 如果为 up，`0` 如果为 down

- `link_speed = 1` 如果为 `100`，`0` 如果为 `10`

- `link_mode = 1` 如果为 full duplex，`0` 如果为 half

另一组变量在存在多个接口时指定速度和双工模式。以下脚本关闭接口的自动协商，将第一个接口设置为 `10 MB/s` 半双工，将第二个接口设置为 `100 MB/s` 全双工：

```bash
#!/bin/sh
nd-set /dev/hme instance 0
nd-set /dev/hme adv_autoneg_cap 0
nd-set /dev/hme adv_100fdx_cap 0
nd-set /dev/hme adv_100hdx_cap 0
nd-set /dev/hme adv_10fdx_cap 0
nd-set /dev/hme adv_10hdx_cap 1
nd-set /dev/hme instance 1
nd-set /dev/hme adv_autoneg_cap 0
nd-set /dev/hme adv_100fdx_cap 1
nd-set /dev/hme adv_100hdx_cap 0
nd-set /dev/hme adv_10fdx_cap 0
nd-set /dev/hme adv_10hdx_cap 0
```

如果你有一块具有自动协商功能但工作不完全正确的网卡，你可能需要关闭它并手动设置速度和双工参数，正如本例所示。

# 第 13 章 TCP/IP 网络配置

## 设置伪接口的 IP 地址

`ifconfig ipdpt0 plub 192.225.32.2 192.225.32.1 up`

## 伪接口路径的动态拨号参数

`interface ipdpt0`

`peer_system_name pppub` # 与 Systems 文件中的相同

`inactivity_time 600` # 空闲 10 分钟后超时

放置此文件后，你可以使用命令 `/etc/init.d/aspp start` 手动启动 PPP 守护进程。

在首次配置 PPP 时，这一步是必要的。在随后的重启中，`init` 将会自动启动 PPP 守护进程。如果一切顺利（在 `/var/admin/log/aspp.log` 中检查是否有错误信息），你应该能够使用 `ssh` 和 `ftp` 等命令访问远程站点。

# Solaris 的网络特殊之处
