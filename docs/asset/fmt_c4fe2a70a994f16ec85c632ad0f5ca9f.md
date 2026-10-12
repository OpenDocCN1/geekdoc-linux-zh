
```
cesium:$ tcpdump -n -i tr0 10:40:0:0:5a:7d c0:c0:0:1 609e 352
22:21:30.843295 02:90:00
```

（注：抱歉，我发现我在处理时出现了逻辑死循环，以下是干净的最终翻译）

## 6.2 Cesium 的环境

现在让我们回到以太网/令牌环网关，看看我们需要构建什么来让我们的工作站通信。基础拓扑如图 6.1 所示。乍看之下，我们需要做的是为令牌环分配地址并配置转发。

![img/98e395bd0fce034771b_200.png](图 6.1 cesium/xenon 网络拓扑)

现在，如果以太网网段的工作站想要连接以太网网段的工作站呢？我们不能通过为 `cesium` 添加路由来转发所有指向 `xenon` 的数据包吗？尽管这种方法很有吸引力，但答案是否。`cesium` 和 `xenon` 被路由器隔开（因此不在同一个子网），你无法指定一个使用你所在网段之外网关的路由。思考一下，你会发现普通的 IP 数据包中没有足够的字段来实现这一点。嗯，严格来说，之前的陈述不对。这可以通过源路由（source routing）来实现，它是 IP 的一个功能，允许发送者指定到目的地的网络路径。然而，源路由是错误的，因为它可以用于各种欺骗攻击，因此通常被禁用。我们绝不会指望它可以用于 `cesium` 和 `xenon` 之间的流量传输。顺便说一下，不要将源路由与基于源路由混淆。后者指的是在转发数据包之前考虑源地址，并根据发送者的 IP 地址为客户端提供差异化的服务水平。

我希望你会发现，在网络中引入 Linux 的主要原因是它的灵活性，而不是成本。成本只是锦上添花。优秀的技术人员需要良好的工具，我将解释 GNU 工具的增长和长期受欢迎。灵活性的核心在于选择，Linux 经常为你提供完成任务的选择

## 6.3 节 iproute2 工具集

你可以选择最适合自己的任务。为此，我们进入下一节，该节将向介绍 `iproute2` 工具集。

## 6.3 iproute2 工具集

由 Alexey Kuznet 编写的 `iproute2` 实用程序包是一套非常强大的工具，用于管理 Linux 机器上的网络接口和连接。它完全取代了更传统的 `net-tools` 工具包中 `ifconfig`、`route` 和 `arp` 工具的功能。该术语在传统上指的是模拟 Unix 接口和路由表管理的工具包，即我们到目前为止一直在使用的那套工具集。由于它与内核紧密集成，`iproute2` 仅适用于 Linux。我担心这就是 `iproute2` 没有获得太多主流关注的原因之一——像我这样老守旧的网络管理员已经习惯了随我们成长的那套有 15 年历史的工具集，只有在需要特殊功能时才会向框架外看。好吧，再也不如此了。`iproute2` 值得花精力学习，即使它只适用于 Linux。

为了帮助介绍这一点，我们将回顾已经完成的某些任务，且在 Debian 和 RedHat 中软件包名称均为 `iproute`。如果你想从上游源获取并自己构建它，主站是 `http://ftp.bnr.ac.ru/ip-routing/`。连接时你将看到一个消息列表；如果是附近的镜像源，你应该礼貌地使用它。你还需要确保你运行的内核在编译时包含了以下选项。

网络选项 ---

- 内核/用户态 netlink 套接字

- 路由消息

如果你没有这些选项，在尝试使用这些工具时，将收到以下错误消息之一，具体取决于你的内核缺少了什么内容：

```
tony@vivaldi:~$ /sbin/ip addr show
Cannot open netlink socket: Address family not supported by protocol
```

```
tony@bach:~$ /sbin/ip addr show
Cannot send request: Connection refused
```

```
tony@vivaldi:~$ /sbin/ip rule list
RTNETLINK answers: Invalid argument
Dump requested
```

一旦你构建并/或安装了工具，并且运行具有适当支持的 2.2 或 2.4 内核，启动它并看到可能令人困惑的内容：

```
tony@bach:~$ /sbin/ip
Usage: ip [ OPTIONS ] OBJECT { COMMAND } help |
where OBJECT := { link | addr | route | rule | neigh | tunnel |
maddr | monitor |
OPTIONS := { -version | -statistics | -r[-resolution] |
[-family] * inet | inet6 | ipx | dirnet | link } | -oneline }
```

起初，这似乎比 `ifconfig -a` 输出的内容没好多少。列出一些 `COMMAND` 关键字并指出在没有给出命令时，默认关键字是 `show` 或 `list`（它们完全相同）可能会有所帮助。有效的 COMMAND 关键字列表（`add`, `delete`, `set`, `flush`, `change`, `replace`, `get`, 以及 `show` 或 `list`）提供了这些词的缩写。然而，并不是所有的关键字适用于所有的 OBJECT。幸运的是，命令语法设计得很好且非常规范（一致）。你花很少的时间就能学会，并且始终可以通过 `OBJECT help` 来查看该选项的内容。但如果你像我一样，你就不会去查看 `help` 提供的语法图，而是通过使用它们来记忆。

### 6.3.1 iproute2: /sbin/ip config route, 和 arp 形式

```
ifconfig:
2: eth0:<BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast qlen 100
link/ether 00:50:56:40 brd ff:ff:ff:ff
net 192.168.16.1/24 brd 192.168.16.255 global eth0
```

这种用法应该是清晰的。我们可能想要查看设备 `eth0`对应的地址。这里有几点需要注意：

- 数字 2 是接口索引。以后我们可以更改接口名称，接口与物理设备绑定。

- `mtu` 和 `device` 标志直接来自 `ifconfig` 输出。

- `qdisc` 是队列规则的缩写，即我们使用什么算法。

- `qlen` 是队列的最大深度。这可以调整以允许高速和低速接口之间产生更大的缓冲区，但这并不总是好事。

- `link` 显示关于链路层的详细信息，包括类型（`ether`）、链路层地址（即 MAC 地址）以及链路层广播地址。

- `inet` 实际上是 `inet` 族，与 IPv4 同义。这里的行接口可能有多个别名，这是正确的。

- 接口的 IP 地址与 `netmask` 一起显示，尽管我们通过查看 IP 地址和子掩码位数组合可以快速计算出来。

- `brd` 地址在这种情况下定义为全局 `global`。现在不用担心这个，但它是策略路由的一部分，我们将在 6.4 节中接触。那里有很多信息，不像 `ifconfig` 只有在你显式请求时才会获取接口统计信息。下一条命令显示路由表。

## 6.3 iproute2 教程

```
user@vivaldi:~$ /sbin/ip show dev eth0
2: eth0:<BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast qlen 100
link/eth0 00:50:56:40:40 brd ff:ff:ff:ff
RX: packets errors 0 0 0
TX: packets errors 0 0 0
```

```
user@vivaldi:~$ /sbin/ip route show
192.168.0.0/24 dev eth1 proto kernel scope src 192.168.18.1
192.168.16.0/24 dev eth0 proto kernel scope src 192.168.16.13 default via 192.168.18.1 eth1
```

如果你在问有什么意义？我知道如何做这些事情，请包涵。我们正在接触 `iproute2`。你可能注意到，所有的地址都以 IP 地址的形式显示。如果你需要主机名/网络解析，你必须使用 `-n` 关来启用（这是一个教训：如果我每次调用 `route` 时忘记添加 `-n` 关都会掉一个镍币……如何配置接口？

```bash
# 分配 IP 地址和子网掩码
root@vivaldi:~ ip addr add eth1 192.168.64.55/24
```
