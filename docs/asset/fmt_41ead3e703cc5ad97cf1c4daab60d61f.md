
构成链的每条规则都有一个“目标”（`target`）子句，决定如何处理匹配的数据包。当数据包匹配规则时，大多数情况下其命运已定；不会检查额外的规则。许多目标在 `iptables` 内部定义；指定的另一个链作为规则的目标。

`filter` 表中规则可用的目标有 `ACCEPT`、`DROP`、`REJECT`、`LOG`、`MIRROR`、`QUEUE`、`REDIRECT`、`RETURN` 和 `ULOG`。当规则导致 `ACCEPT` 时，匹配的数据包被允许继续其运行。`DROP` 和 `REJECT` 都会丢弃数据包；`DROP` 是静默的，而 `REJECT` 返回 ICMP 错误消息。`LOG` 为你提供了一种简单的跟踪匹配包的方法，`ULOG` 则扩展了日志。

`REDIRECT` 将数据包重定向到代理而不是让其通过。例如，你可能通过此功能让你站点所有的网络流量通过 `Squid` 等网络缓存。`RETURN` 终止用户定义的链，类似于子程序中的返回语句。`MIRROR` 目标在发送数据包之前交换 IP 源地址和目的地址。最后，`QUEUE` 通过内核模块将数据包移交给本地用户程序。

- 7. 在很多情况下，`inetd` 或 `xinetd` 会替它们执行实际等待。详见第 1188 页。
- 8. 端口 25 是 `/etc/services` 中定义的 SMTP 端口。
- 9. 本总结描述了传统的 FTP，也称为“主动 FTP”。

## 完整的示例设置

在可以使用 `iptables` 作为防火墙之前，你必须启用 IP 转发并确保各种 `iptables` 模块已加载到内核中。关于启用 IP 转发的更多信息，请参阅第421页的“调整 Linux 内核参数”或第492页的“安全相关的内核变量”。安装 `iptables` 的软件包通常包含辅助此类启用和加载的启动脚本。

Linux 防火墙通常实现为包含在 `rc` 启动脚本中的系列 `iptables` 命令。单个 `iptables` 命令通常采用以下形式之一：

- `iptables -F chain-name`
- `iptables -P chain-name target`
- `iptables -A chain-name -i interface -j target`

第一种形式 `-F` 冲空链中的所有之前的规则。第二种形式 `-P` 为链设置默认策略（又称为目标）。我们建议你使用 `DROP` 作为默认链目标。第三种形式 `-A` 将当前规范添加到链中。除非你使用 `-t` 参数指定表，否则命令将应用于 `filter` 表中的链。`-i` 参数将规则应用于命名的接口，`-j` 识别目标。`iptables` 还接受许多其他子句，其中一些在表22.3所示。

### 表 22.3 iptables 过滤器的命令行标记

| 子句 | 含义或可能的值 |
|---|---|
| `-p proto` | 按协议匹配：`tcp`, `udp`, 或 `icmp` |
| `-s source-ip` | 匹配主机或网络 IP 地址（CIDR 表示法可以） |
| `-d dest` | 匹配主机或网络目的地址 |
| `--port` | 按源端口匹配（注意双连横线） |
| `--dport` | 按目的端口匹配（注意双连横线） |
| `--icmp type` | 按 ICMP 类型代码匹配（注意双连横线） |
| `!` | 否定子句 |
| `-t table` | 指定命令适的表（默认是 `filter`） |

## 一个完整的示例

下面我们提供一个完整的示例。假设 `eth1` 接口连接到互联网，`eth0` 接口连接到内部网络。`eth1` IP 地址为 `128.138.101.4`，`eth0` IP 地址为 `10.1.1.1`，两个接口的掩码均为 `255.255.255.0`。此示例使用无状态包过滤来保护 IP 地址为 `10.1.1.2` 的 Web 服务器，这是保护互联网服务器的标准方法。在示例后续部分，我们将展示如何使用有状态过滤来保护桌面用户。

我们的第一组规则初始化了 `filter` 表。首先，清空表中的所有链，然后将 `INPUT` 和 `FORWARD` 链的默认目标设置为 `DROP`。

## 第22章 安全

对于任何其他网络防火墙，最安全的策略是丢弃任何你没有显式允许的数据包。

```
iptables -F
iptables -P INPUT DROP
iptables -P FORWARD DROP
```

由于规则是按顺序评估的，我们将最繁忙的规则放在前面。第一条规则允许所有来自受信内部网络的连接通过防火墙。`FORWARD` 链中的后续三条规则允许连接通过防火墙访问 `10.1.1.2` 上的网络服务。具体而言，我们允许 SSH（端口 22）、HTTP（端口 80）和 HTTPS（端口 443）访问我们的 Web 服务器。

```
iptables -A FORWARD -i eth0 -p ANY -j ACCEPT
iptables -A FORWARD -d 10.1.1.1 -p tcp --dport 22 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p tcp --dport 80 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p tcp --dport 443 -j ACCEPT
```

我们允许进入防火墙主机（`10.1.1.1`）的唯一 TCP 流量是 SSH，这对于管理防火墙主机有用。第二条规则允许回环流量，这种流量留在主机本地。管理员如果无法 ping 通默认路由会很苦恼，因此第三条规则允许来自内部 IP 地址的 ICMP `ECHO_REQUEST` 包。

```
iptables -A INPUT -i eth0 -d 10.1.1.1 -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -i lo -d 127.0.0.1 -p ANY -j ACCEPT
iptables -A INPUT -i eth0 -d 10.1.1.1 -p icmp --icmp-type 8 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 0 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 3 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 11 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 0 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 3 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 5 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 11 -j ACCEPT
```

为了让任何 IP 主机在互联网上正常工作，必须允许某些类型的 ICMP 包通过防火墙。以下规则允许一组最小的 ICMP 包通过防火墙。关于 IP 伪造的更多信息请参阅第473页。我们向 `nat` 表中的 `PREROUTING` 链添加了规则。尽管 `nat` 表并非用于包过滤，但其 `PREROUTING` 特别适用于防伪造。如果 `PREROUTING` 链中重复了条目，它们不需要出现在 `INPUT` 和 `FORWARD` 链中。然而，必须小心，重排序规则不会修改功能。

```
iptables -t nat -A PREROUTING -i eth1 10.0.0.0/8 -j DROP
iptables -t nat -A PREROUTING -i eth1 172.16.0.0/12 -j DROP
iptables -t nat -A PREROUTING -i eth1 192.168.0.0/16 -j DROP
iptables -t nat -A PREROUTING -i eth1 127.0.0.0/8 -j DROP
iptables -t nat -A PREROUTING -i eth1 224.0.0.0/4 -j DROP
```

最后，我们需要 `INPUT` 和 `FORWARD` 链都包含禁止未显式允许包的规则。虽然我们已经通过 `iptables -p` 命令强制了这种行为，但 `LOG` 目标让我们知道是谁在互联网敲门。

```
iptables -A INPUT -i eth1 -j LOG
iptables -A FORWARD -i eth1 -j LOG
```

可选地，我们可以设置 NAT 来隐藏内部网络使用的私有地址空间。关于 NAT 的更多信息请参阅第492页。`Netfilter` 为 Linux 防火墙带来的最强大的功能之一是有状态过滤。与其允许特定的入境服务，简单的有状态 `FORWARD` 链允许所有由主机发起的连接离开我们的网络。必须启用某些内核模块以允许 `FTP` 和 `IRC` 等复杂会话。如果这些模块没有加载，`iptables` 仅仅会拒绝这些连接。虽然有状态包过滤器可以增加站点的安全性，但也增加了网络的复杂性。调试 `iptables` 规则的一种可能方法是使用像 `tcpdump` 这样的嗅探器。你可以解决更棘手的问题。

## 22.13 用于 UNIX 系统的 IPFilter

大多数供应商没有自己的防火墙。添加它非常容易：`IPFilter` 是一个由 `Darren Reed` 开发的开源包，为 UNIX 系统提供 NAT 和有状态防火墙服务。`Solaris` 默认包含了它，它作为插件适用于 `HP-UX`、`AIX` 以及许多其他系统，包括 Linux。你可以将 `IPFilter` 作为可加载内核模块（开发者推荐）或静态包含内核内核。`AIX` 在其 IP 实现中包含一个包过滤套件，但该套件没有有状态过滤。查看 `genfilt` 页面以开始。

## 第22章 安全

`IPFilter` 非常成熟且功能齐全。该包拥有活跃的用户社区和持续开发的历史。即使对于 UDP 和 ICMP 等无状态协议也能进行状态跟踪。

`IPFilter` 从配置文件（通常为 `/etc/ipf.conf` 或 `/etc/ipf/ipf.conf`）读取过滤规则，而不是像 `iptables` 那样让你运行一系列命令。`ipf` 中可能简单规则示例是：

```
block in all
```

此规则阻止了所有网络接口上的所有入境流量（即系统接收的网络活动）。固然安全，但并不特别有用！表22.4 是 `ipf` 规则中可能出现的一些条件。

### 表 22.4 常用的 ipf 条件

| 条件 | 含义或可能的值 |
| --- | --- |
| `on` | 将规则应用于指定的接口 |
| `proto` | 根据协议选择包：`tcp`, `udp`, 或 `icmp` |
| `from` | 按源过滤：主机，网络, 或任意 |
| `dest-ip` | 按目的过滤：主机，网络, 或任意 |
| `port=#` | 按端口名（来自 `/etc/services`）或数字过滤 |
| `flags-spec` | 根据 TCP 头部标志位过滤 |
| `icmp-type number` | 按 ICMP 类型和代码过滤 |
| `keep state` | 保留会话流的详细信息；见下文注释 |

a. 你可以使用任何比较运算符：`=$`, `<`, `>`, `\le`, `\ge`, $\neq$ 等。

`IPFilter` 按规则在配置文件中的呈现顺序评估规则。最后一个匹配是生效的。例如，遍历以下过滤器的入境包将始终通过：

```
block in all
pass in all
```

`block` 规则匹配所有包，`pass` 规则也是如此，且 `pass` 是最后一个匹配。要强制使匹配规则立即生效并让 `IPFilter` 跳过后续规则，请使用关键字：

```
block in all quick
pass in all
```

工业级防火墙通常包含许多规则，因此使用 `quick` 对于维护防火墙性能至关重要。如果没有它，每个包都会针对每条规则进行评估，这种浪费是昂贵的。

可能防火墙最常见的用途是控制对特定网络或主机的出入访问，通常是针对特定端口的。`IPFilter` 强大的语法可以在这种粒度上控制流量。在以下规则中，

允许进入 `10.0.0.0/24` 网络的 TCP 端口 80 和 443，以及 UDP 端口 53 的入站流量。

```
block out quick all
pass in quick proto tcp from any to 10.0.0.0/24 port = 80 keep state
pass in quick proto tcp from any to 10.0.0.0/24 port = 443 keep state
pass in quick proto udp from any to 10.0.0.0/24 port = 53 keep state
block in all
```

`keep state` 关键字值得特别关注。`IPFilter` 可以通过记录新会话的第一个数据包来跟踪连接。例如，当发往 `10.0.0.10` 端口 80 的新数据包到达时，`IPFilter` 会在状态表中创建一个条目并允许该包通过。它还会允许来自 Web 服务器的回复，即使第一条规则显式地阻止了所有出站流量。

`keep state` 对于不提供服务但必须发起连接的设备也很有用。以下规则集允许所有由 `192.168.10.10` 发起的会话。它阻止了除已建立连接以外的所有入站数据包。

```
block in quick all
pass out quick from 192.168.10.10/10/32 to any keep state
```

UDP 和 ICMP 数据包的 `keep state` 关键字同样如此，由于这些协议是无状态的，其机制略显特殊：`IPFilter` 在过滤器看到入站数据包后 60 秒内允许对 UDP 或 ICMP 数据包做出响应。例如，如果一个来自 `10.0.0.10` 端口 32,000 的 UDP 包发往 `192.168.10.10` 端口 53，则允许来自 `192.168.10.10` 的 UDP 回复在 60 秒内通过。同样，在 ICMP 回显请求进入状态表后，允许通过 ICMP 回显回复（ping 响应）。

网络地址翻译 `NAT` 是 `IPFilter` 提供的另一项功能。`NAT` 让使用 RFC1918 私有 IP 地址的大网络通过一组少量的互联网可路由 IP 地址连接到互联网。`NAT` 设备将来自私有网络的流量映射到一个或多个公共地址，在互联网上发送请求，并拦截响应，根据本地 IP 地址对其进行重写。

`IPFilter` 使用 `map` 关键字（代替 `pass` 和 `block`）来提供 NAT 服务。在以下规则中，来自 `10.0.0.0/24` 网络的流量被映射到 `e1000g` 接口当前的出站地址。

```
map e1000g 10.0.0.0/24 -> 0/32
```

如果 `e1000g` 的地址发生变化，必须重新加载过滤器，这在 `e1000g` 通过 DHCP 获取动态 IP 时发生。由于此原因，`IPFilter` 的 NAT 功能最好用于面向互联网接口具有静态 IP 地址的站点。

# 第 22 章 安全

`IPFilter` 规则灵活且可配置。宏等高级功能极地简化了规则文件。有关这些高级功能的详细信息，请参阅 `IPFilter` 官方网站 `coombs.anu.edu.au/~avalon`。

`IPFilter` 软件包包含若干命令，列于表 22.5 中。

# 表 22.5 IPFilter 命令

| Cmd | Function |
| --- | --- |
| `ipf` | 管理规则和过滤器列表 |
| `ipstat` | 获取数据包过滤统计信息 |
| `ipmon` | 监控记录的过滤器信息 |
| `ipnat` | 管理 NAT 规则 |

```
solaris$ sudo ipf -Fa -f /etc/ipf/ipfilter.conf
```

`IPFilter` 依赖 `/dev` 中的伪设备文件进行访问控制，默认只有 `root` 可以编辑过滤器列表。我们建议保留默认权限并使用 `sudo` 来维护过滤器。

在标记规则文件时使用 `ipf -v` 来调试语法错误和配置中的其他问题。

`IPFilter` 预装在 `Solaris` 内核中，但在在使用之前必须启用它。

```
solaris$ sudo svcad enable network/ipfilter
```

在使用它之前。

# 22.14 虚拟专用网络 (VPNs)

这是一个 VPN 有用场景的良好示例：假设一家公司在芝加哥、布尔德和迈阿密设有办公室。如果每个办公室都有到本地 ISP 的连接，该公司可以使用 VPN 跨越不可信的互联网透明地（在大多数情况下是安全地）连接这些办公室。这

# 我只需要 VPN 吗？

公司可以通过租赁专用线路来连接这三个办公室来实现类似的结果，但那样将贵得多。

另一个良好的示例是员工从家里远程办公的公司。VPN 允许用户在享受其高速且廉价的电缆调制解调器服务的同时，仍然看起来他们是直接连接到公司网络。

由于这项功能的便利性和普及，每个人都在提供某种类型的 VPN 解决方案。你可以从你的路由器供应商处购买，作为你的...插件。

## 认证

这项 CIA 速成课程只是对广泛的信息安全领域的简要介绍。大型企业通常会雇用许多全职员工，专门负责保护信息。为了在该领域获得公信力并保持知识领先地位，这些专业人士会参加培训课程并获得认证。在我们介绍一些最流行的认证时，请做好面对大量缩写词的心理准备。

广受认可的安全认证之一是 `CISSP`，即认证信息系统安全专业人员。它由 `(ISC²，国际信息系统安全认证协会（试着快速读十遍！）` 管理。`CISSP` 的主要吸引力之一是 `(ISC)²` 的“通用知识体系”（`CBK`）概念，这本质上是整个行业安全最佳实践。`CBK` 涵盖了法律、密码学、身份验证、物理安全等许多内容。对于安全人员来说，这是一个极佳的参考。

对 `CISSP` 的批评之一是它过于注重宽度而缺乏深度。`CBK` 中的主题太多，而时间又太少！为了解决这个问题，`(ISC)²` 发布了 `CISSP` 专项计划，重点关注架构、工程和管理。这些专业认证为更通用的 `CISSP` 认证增加了深度。
