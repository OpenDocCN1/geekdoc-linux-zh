
仅仅通过 IP 地址，你可能也想为网络数字使用符号名称。因此，*hosts* 文件有一个名为 `/etc/networks` 的辅助文件，它可以将网络名称映射到网络数字，反之亦然。在虚拟酿酒厂，我们可能会安装如下所示 *networks* 文件：³

```text
# 虚拟酿酒厂的 /etc/networks
brew-net       191.72.1.0
wine-net        191.72.2.0
```

## 5.7 IP 接口配置

在按照上一章介绍的方法设置好你的硬件之后，你必须让内核网络软件识别这些设备。需要使用一些命令来配置网络接口并初始化路由表。

> ³注意，*networks* 中的名称不能与 *hosts 文件* 中的主机名冲突，否则某些程序可能会产生奇怪的结果。

这些任务通常在系统每次启动时从 `rcinit` 脚本执行。用于此任务的基本工具是 `ifconfig`（其中 "if" 代表接口）和 `route`。

`ifconfig` 用于使接口对内核网络层可访问。这涉及分配 IP 地址和参数、激活接口（也称为“启用”）。激活意味着内核将通过该接口发送和接收 IP 报文。调用它的最简单方法是

```bash
ifconfig ip-address
```

这会将 `ip-address` 分配给接口并激活它。所有其他参数都将设置为默认值。例如，默认子网掩码是根据 IP 地址的网络类推导得出的，例如 B 类地址的掩码为 `255.255.0.0`。`ifconfig` 将在本章末尾详细描述。

`route` 允许你从内核路由表中添加或删除路由。可以通过以下方式调用它：

```bash
route [add|del] target
```

其中 `add` 和 `del` 参数决定了是添加还是删除路由目标。

### 5.7.1 回环接口

第一个被激活的接口是回环接口：

```bash
# ifconfig lo 127.0.0.1
```

偶尔，你还会看到使用虚拟主机名而不是 IP 地址。`ifconfig` 会在 `hosts` 文件中查找该名称，其中某个条目应将其声明为 127.0.0.1 的主机名：

```text
# localhost 的示例 /etc/hosts 条目
localhost 127.0.0.1
```

要查看接口的配置，调用 `ifconfig` 并将接口名称作为参数：

```bash
$ ifconfig lo
lo Link enc Local Loopback Broadcast [NONE SET] Mask 255.0.0.0
    inet 127.0.0.1  UP BROADCAST LOOPBACK RUNNING MTU 200 Metric 1
    RX packets 0 errors 0 dropped 0 overrun
    TX packets 0 errors 0 dropped 0 overrun
```

如你所示，回环接口被分配了掩码 `255.255.0.0`，因为 `127.0.0.1` 是 A 类地址。如你所示，它没有设置广播地址，这对于回环接口本身通常非常有用。然而，如果你在主机上运行 rha 守护进程，可能需要设置回环设备的广播地址以便 wto 正常运行。设置广播地址在“关于 ifconfig 的一切”中进行了解释。

现在，你可以开始玩你的“微型网络”了。缺少的是路由表中一个条目，告诉它可以使用此接口作为通往 127.0.0.1 的路由。这通过输入实现：

```bash
# route add 127.0.0.1
```

再次，你可以使用 `localhost` 代替 IP 地址。

接下来，你应该使用 `ping` 检查一切是否运行正常。`ping` 相当于声纳设备，用于验证一个地址是否真的可达，并测量向其发送数据并返回时产生的延迟。完成此操作所需通常被称为往返时间。

```bash
# ping localhost
PING localhost (127.0.0.1): 64 data bytes
64 bytes from 127.0.0.1: icmp_seq=0 ttl=32
64 bytes from 127.0.0.1: icmp_seq=1 ttl=32
64 bytes from 127.0.0.1: icmp_seq=2 ttl=32
64 bytes from 127.0.0.1: icmp_seq=3 ttl=32

--- localhost statistics ---
4 packets transmitted, 4 received, 0% packet loss
rtt min/avg/max/mdev = 0.042/0.045/0.048/0.003 ms
```

> 任何人记得 Pink Floyd 的“回声"* (img/e0ed64e774a11b944fd2651b5a09cd8c_409_0.png)

# 第 5 章 配置 TCP/IP

`ping` 结果显示，你已经成功设置了第一个接口。如果你按下 `Ctrl-C`，`ping` 将停止。

上述步骤对于设置网络是足够的。然而，如果你收到错误消息“Network unreachable”，你可能配置错了路由。检查 `ifconfig` 是否编译了网络支持。

正如 `ifconfig` 所示，你已经可以使用网络。无论你的接口是否连接，你都必须配置它。

### 5.7.2 以太网接口

配置以太网接口与配置回环接口非常相似，但在使用它时需要一些参数。

在虚拟酿酒厂，我们将原本的 B 类网络划分为 C 类子网。为了让接口识别此网络，`ifconfig` 的命令看起来如下：

```bash
# ifconfig eth0 mask 255.255.255.0
```

这会将 `191.72.1.2` 分配给 `eth0`。如果我们省略了掩码，`ifconfig` 将根据网络类推导出掩码，这将导致掩码为 `255.255.0`。现在你有一个检查显示：

```bash
# ifconfig
eth0 Link enc 10Mps Ethernet Haddr 00:C0:90:B3:42
	inet addr 191.72.1.2 Bcast 191.72.1.255 Mask 255.255.255.0
	UP BROADCAST MTU 1500 Metric 1
	RX packets 0 errors 0 dropped 0 overrun 0
	TX packets 0 errors 0 dropped 0 overrun 0
```

你可以看到 `ifconfig` 自动将地址（Base 字段）设置为通常值，即设置了主机位的掩码。此外，消息传输单元（内核为此接口生成的以太网帧的最大 own）已设置为 1500 字节的最大值。所有这些值都可以用特殊选项覆盖，这些将在将在描述。

与回环情况类似，你现在必须安装一个路由条目，告知内核可以通过 `eth0` 访问的网络。对于虚拟酿酒厂，你将调用 `route`：

```bash
# route add -net 191.72.1.0
```

起初，这看起来像小魔法，并不清楚 `route` 如何检测通过哪个接口路由。然而，技巧很简单：内核会检查所有已配置的接口并比较这些

> 例如，所有基于 RPC 的应用程序都使用回环接口在启动时向 portmapper 守护进程注册自身。

# 第 5 章 配置 TCP/IP 网络

## 5.7. IP 配置

将地址 `191.72.1.0`（在此例中）指向地址的网络部分（即地址与掩的位与运算结果）。唯一匹配的接口是 `eth0`。

现在，这个 `-net` 选项的作用是什么呢？之所以使用它是因为 `route` 命令可以同时处理网络和到单台主机的路由（正如你一直在使用的 `localhost`）。当给出一个点分十法表示法的地址时，它会尝试通过查看主机部分来猜测它是网络还是主机名。如果地址的主机部分为 0，`route` 就会认为它是一个网络，否则它将其视为主机地址。因此，`route` 将无法知道 `191.72.1.0` 是一个主机而不是数字，因为它不知道我们正在进行子网划分。我们必须通过提供 `-net` 标志来显式地告诉它。

当然，`route` 命令也有些冗长，而且容易拼写错误。一种方便的方法是使用我们在 `letworks` 中定义的名称。这种命令会让工作更具可读性；甚至可以省略 `-net` 标志，因为 `route` 知道 `191.72.1.0` 代表一个网络。

```bash
# host add brew-net
```

现在你已经完成了基础配置步骤，我们想要确保你的以太网接口确实在良好运行。为你的以太网选择一个主机，接口为 `vlager` 并输入：

```bash
# ping vlager
PING vlager: 64 bytes
64 bytes from 191.72.1.1: icmp_seq=0, time=11.5 ms
64 bytes from 191.72.1.1: icmp_seq=1, time=7.5 ms
64 bytes from 191.72.1.1: icmp_seq=2, time=12.3 ms
64 bytes from 191.72.1.1: icmp_seq=3, time=3.5 ms
C
```

```bash
# vstout.brew.com PING Statistics-----
4 packets transmitted, 0% packet loss
round-trip (ms) min/avg/max = 3/8/12
```

如果你没有看到类似的内容，那么显然某些地方出问题了。如果你遇到无法到达的丢包率，这暗示着存在硬件问题、电缆不佳或缺少终端器。如果你完全没有接收到包，你应该用 `netstat` 检查接口配置。`ifconfig` 显示的数据包统计信息应该告诉你你的数据包是否已经发送到了接口。如果你可以访问远程主机，你也应该去那台机器检查接口统计信息。通过这种方式，你可以精确确定数据包在哪里被丢弃。此外，你应该通过 `route` 显示路由信息，以查看两个主机是否有正确的条目。在不带参数调用时，`route` 会打印完整的路由表（`-n` 选项仅使其以点分四位数的格式打印地址而不是主机名）：

```bash
# route -n
Routing table
| Destination | Gateway | Genmask | Metric | Ref | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 127.0.0.1 | * | 255.255.255 | UH | 1 | 0 | 112 lo |
| 191.72.1.0 | * | 255.255.255 | U | 1 | 0 | 10 eth0 |
```

这些字段的详细含义在下文第 9.5 节中解释。`Flag` 列包含了每个接口的标志列表。`U` 表示目标地址代表主机。如果你为你想要作为网络路由的路由设置了 `H`，那么你必须在使用 `route` 命令时指定 `-net` 选项。要检查你输入的路由是否已全部使用，请检查在两次调用 `ping` 之后最后一列的 `Use` 字段是否增加。

### 5.7.3 通过网关路由

在上一节中，我只涵盖了在单个以太网上设置主机的情况。然而，经常会遇到通过网关连接的网络。这些网关可能连接两个或多个以太网，也提供通往外部世界（互联网的路径。为了使用网关的服务，你必须向网络层提供额外的路由信息。

例如，虚拟酿酒（Virtual Brewery）和虚拟酒庄（Virtual Winery）的以太网通过这种网关连接，即主机 `vlager`。假设 `vlager` 已经配置好，我们只需要在 `vstout` 的路由表中添加另一个条目，告诉客户端它可以通过 `vlager` 到达酒庄网络上的所有主机。`route` 命令的适当用法如下所示：`gw` 关键字告诉下一个参数是一个网关。

```bash
# add wine-net gw vlager
```

当然，你想要与酒庄上通信的主机必须有一个指向酿酒厂网络的相应路由条目，否则你只能从 `vstout` 向 `vhardolino` 发送数据，但后者返回的任何响应都将掉进“黑洞”。

这个示例仅描述了一个在孤立以太网之间切换数据包的网关。现在 `vlager` 也连接到了互联网（例如，通过额外的 SLIP 链路）。那么我们希望任何发往酿酒厂以外的其他目标网络的数据包都由 `vlager` 处理。这可以通过设置 `vstout` 的默认网关来实现。

```bash
# add default gw vlager
```

网络名称 `default` 是 `0.0.0.0`。由于我们不知道我们正在进行子网划分，我们必须通过提供 `-net` 标志来显式地告诉它。
