
# UNIX 系统管理手册

## 第 13 章 TCP/IP 网络

我们刚刚关闭了 IP 转发。

### FreeBSD 的安全、防火墙、过滤和 NAT

表13.23 显示 FreeBSD 对各种安全网络问题的行为。有关这些行为影响的简要描述，请见295页。表13.23的第三列显示了更改更改行为；这些变量应设置在 `/etc/rc.conf` 中，而不是通过 `sysctl` 设置。

#### 表13.23 FreeBSD 中的安全网络行为

| 特性 | 默认 | 修改的 `rc.conf` 变量 |
| :--- | :--- | :--- |
| IP 转发 | 关闭 | `gateway_enable` |
| ICMP 重定向 | 接受 | `icmp_direct_redirect*` |
| 源路由 | 忽略 | `forward_souroute` 和 `accept_souroute` |
| 广播 ping | 忽略 | `icmp_bmcaste` |

+ a. 使用 `icmp_log_restrict` 来记录它们。

将 UNIX 或 NT 机器作为网络防火墙不是一个好主意，特别是对于有重要在线数据的公司站点。像 Cisco PIX 这样的专用硬件解决方案要安全可靠可靠得多。尽管如此，对于一个勤于更新最新安全补丁的家庭机器，UNIX 软件可能是足够的。在接下来的几页中，我们将查看 FreeBSD 提供的两个防火墙软件包：`ipfw` 和 Darren Reed 的 IPFilter 包。

`ipfw` 包含了对 `dummynet` 的支持，这是一个非常有用的功能，让你通过设置带宽和队列长度限制以及模拟延迟和丢包来操作你的网络流量。`Dummynet` 最初设计用于 TCP 拥塞的测试工具，但事实证明它在许多其他场景中有用。它被用于许多任务，例如限制 DSL 线上某个客户消耗的带宽，限制 Web 或 FTP 流量的带宽以确保交互流量保持快速。一个带有流行 Web 或 FTP 数据集的缓慢家庭链路可以将数据包“管道”到 `dummynet`，以防止它们溢满链路。关于 `dummynet` 与 `ipfw` 集成的细节，可以查阅相关页面。

`ipfw` 易于使用，其语法与 Cisco 的访问控制列表类似。要用 `ipfw` 实现 NAT，请使用 `/sbin` 中的 `natd` 程序。

就像在 Linux 中配置 `ipchains` 一样，使用 `ipfw` 命令建立过滤规则。一个完整的 `ipfw` 配置是一个运行一系列 `ipfw` 命令的 shell 脚本。我们在下方包含了一个部分 `ipfw` 配置以说明命令的语法，但没有提供详细的介绍。

你可以将下例示例与第 335 页上的 IPFilter 示例进行对比，以直观感受每个系统。在此示例，`eth0` 是外部接口，`ed1` 是编号；规则按数字从小到大的顺序处理。顺序非常重要，因为第一条规则决定了将采取什么动作。

```
# freebs ipfw file

# 首先清除残留的旧规则

ipfw -f flush

# 允许来自 dhcp 服务器和 gw.syanck.net 的一切

ipfw add 500 ip allow from 128.138.129.136 to any

ipfw add 510 ip allow from 209.180.251.58 to any

# 允许 ssh 入站和出

ipfw add 600 allow tcp from any to 22 in via dev0

ipfw add 605 allow tcp from any to 22 in via dev 0

# 允许通过桥接 arp 数据包的奇特技巧

ipfw add 1000 udp from 0.0.0.0 2054 to 0.0.0.0
```

其他规则包括入出站 DNS 流量、支持访问外部 Web、允许 DHCP 放行，以及用于 `traceroute` 和 Quake 的 UDP（这是一台学生的机器）。来自本地网络的所有流量都允许出站。那些对不存在的主机的查询轰击其 DNS 服务器的人被列入黑名单，来自外界的一切都被拦截。

我们对 Reed 的 IPFilter 程序介绍得比 `ipfw` 更详细，因为它们与许多其他 UNIX 版本兼容。IPFilter 包包含了用于配置防火墙的 `ipf`、用于打印已阻塞过滤规则的 `ipstat` 以及实现 NAT 的 `ipnat`。它可以通过以下地址获取：

```
http://coombs.anu.edu.au/~avalon/ip-filter.html
```

要使用 IPFilter，确保你的内核编译时包含了以下子句：

```
option IPFILTER
option IPFILTER_LOG
```

IPFilter 包在数据包过滤任务和 NAT 之间有明确的区分，而不是像 Red Hat 的 `ipchains` 那样将它们混为一谈。

`ipf(1)` 和 `ipf(5)` 手页文档了 IPFilter 过滤逻辑的细节以及大量示例。

`ipf` 默认读取 `/etc/ipf.rules` 规则文件，格式如下：

```
action inout [quick] condition
```

其中 `action` 可以是：

- `pass` 接受数据包
- `block` 丢弃数据包
- `log` 通过 `syslog` 记录数据包，或
- `count` 统计匹配的数据包。

`block` 动作还可以指定向发送者发送 TCP 重置或或特定的 ICMP 错误消息。

`quick` 修饰符会导致动作成为 `count` 和 `log` 的默认值。通常情况下，规则按顺序应用，在尝试了所有规则之前不会采取任何动作。如果多个规则匹配一个数据包，则最后一个匹配的规则决定了所采取的动作。

这种行为与 `ipchains` 和 `ipfw` 完全相反，但在所有这些系统中，规则的顺序决定了防火墙的实际功能。Linux 的顺序更快——匹配即通过——而 FreeBSD 则在采取动作之前会读取所有规则。`ipf` 的范式使其易于实现保守型防火墙。如果你将第一条规则设置为全部，你就可以针对特定类型的流量添加额外的规则。

下一页的表 13.24 显示了 `ipf` 规则中可能出现的某些条件。这里的条件只是冰山一角。请咨询 `ipf` 手页以获取杂复杂的细节。

让我们使用 `ipf` 而不是 `ipchains` 重新实现 328 页上的过滤器规范。与之前一样，我们假设接口 `ppp0` 是连接到的，接口 `eth0` 是我们的内部以太网。为了允许所有本地流量并丢弃来自世界的地址，我们将使用以下规则：

```
pass in eth0

pass in lo all

block in quick on ppp0 from 192.168.0.0/16 to any

block in quick on ppp0 from 172.16.0.0/12 to any

block in quick on ppp0 from 10.0.0.0/8 to any
```

#### 表13.24 ipf 条件

| 条件 | 含义或可能的值 |
| :--- | :--- |
| `on interface` | 将规则应用于指定的接口 |
| `proto` | 根据以下内容选择数据包协议：`tcp`, `udp` 或 `icmp` |
| `from source-ip` | 过滤源：`host`, `network` 或 `any` |
| `to dest-ip` | 过滤目的：`host`, `network` 或 `any` |
| `port=#` | 端口可以通过名称（`/etc/services`）或数字指定；符号 `=` 可以是任何算术运算符（`=`, `<=` 等） |
| `flag-spec` | 过滤 TCP 标志 |
| `icmp-type` | 根据 ICMP 类型和代码过滤 |
| `keep state` | 保留有关会话的细节；通常用于处理已建立 TCP 会话 |

要拦截 TELNET 但允许 SSH，规则将是：

- `block in proto from any to port = 23`
- `pass in ppp0 proto from any to port = 25`
- `pass in proto from any to port = 22`

nat 和 SSH 的规则应该包含 `flags` 和 `keep state` 子句以防止 TCP 会话劫持。参见第 67 页的防火墙和 `ipf(5)` 页以获取关于包含哪些规则以及如何格式化的细节。如果你有 FreeBSD，检查 `/usr/share/ip/` 包含了 `ipf` 和 `ipnat` 的许多示例文件。

为了实现 NAT，我们必须告诉内核映射哪些地址、映射哪些地址以及使用哪个端口范围来扩展地址空间。参见第 279 页关于 NAT 其用于从私有空间桥接到公共空间的通用讨论。

`ipf` 规则的语法非常适合 NAT，因此 NAT 规则看起来很熟悉。和 `ipf` 规则一样，`ipnat` 规则是有顺序的。然而它们的优先级相反。为了让你保持警觉，第一个匹配将被选中。以下是一些 `ipnat` 规则的示例（将放入 `ipnat.rules`）。
