
通过这种配置，你可以在最方便的时间对 CARP 组的系统成员调度操作系统升级和原本会导致停机的活动，而对你服务的用户来说，只会有明显的停机时间。

## IFSTATED，接口状态守护进程

在配置完善的 CARP 设置中，基础网络功能已经得到了很好的保障，但你的设置可能包含某些在主机网络配置发生变化时需要特别关注的元素。例如，当特定接口下降或重启时，某些服务可能需要启动或停止，或者你可能希望响应接口状态的变化运行特定的命令或脚本。如果这听起来很熟悉，那么 `ifstated` 正适合你。

`ifstated` 工具是在 OpenBSD 3.5 中引入的，用于根据网络接口的状态触发操作。你可以在 OpenBSD 的基础系统中找到它，通过 FreeBSD 的 ports 系统以 `net/ifstated` 找到它。在 OpenBSD 上，如果你是从 FreeBSD 安装的端口包，则 `/etc/ifstated.conf` 或 `/local/etc/ifstated.conf` 包含一个几乎可以直接运行的配置，并带有关于如何为 CARP 环境设置 `ifstated` 的一些提示。

主要的控制对象是接口及其状态——例如，`carpo.link` 是 carpo 接口变为主节点的状态——你根据状态更改执行操作。

每当接口状态变化时要执行的状态和操作是在一种简单的脚本语言中指定的，该语言具有变量、宏和简单逻辑条件等基本功能。（有关此主题以及在你的环境中实现 Carp 集群功能的更多信息，请参考 `man ifstated` 和 `man ifstated.conf` 以及基础系统安装提供的默认 `ifstated.conf` 示例文件。）

## 用于负载均衡的 CARP

备切换带来的冗余很好，但有时让硬件为了防止故障而闲置在那里并不那么吸引人，创建一个将网络负载分散到多个主机上的配置会更好。

除了 ARP 均衡（通过计算传入连接源 MAC 地址的哈希值来实现）外，OpenBSD 4.3 及更高版本的 CARP 支持各种基于 IP 的负载均衡，流量根据连接源 IP 和目的 IP 地址的哈希值进行分配。由于 ARP 均衡基于源 MAC 地址，它只对直接连接的网段中的主机有效。相反，基于 IP 的方法适用于与整个互联网之间连接的负载均衡。

你应用程序的方法选择将取决于你需要配合使用的其他网络设备的规范。基本的 `ip` 均衡模式使用组播 MAC 地址，让直接连接的交换机流量转发到负载均衡集群中的所有主机。

遗憾的是，某些系统不支持单播 IP 地址和组播 MAC 地址的组合。在这种情况下，你可能需要在 `ip-unicast` 模式下配置负载均衡（该模式使用单播 MAC 地址），并配置交换机转发到相应的主机。或者你可能需要在 `ip-stealth` 模式下配置负载均衡，该模式完全不使用组播 MAC 地址。像往常一样，细节决定，答案可以在许多页面和其他文档中找到，可能还需要进行一些实验。

传统上，`relayd` 一直被用作面向世界的服务器的前端智能负载均衡。在 OpenBSD 4.7 中，`relayd` 获得了跟踪链路并在链路健康时更改系统路由表的能力，该功能封装在带有 `router` 关键字的包中。对于可能存在上链路或各种路由表的设置，你可以设置 `relayd` 来选择你的上链路，或者在 `sysctl` 变量 `inet.ip.multipath` 的帮助下在可用路由和上链路之间执行负载均衡。具体细节取决于你的网络环境。`relayd.conf` 页面包含一个入门的完整示例。

## 负载均衡模式下的 CARP

在负载均衡中，CARP 概念得到了扩展，允许每个接口成为多个备切换组的成员，并根据共享虚拟地址的物理主机数量，成为多个负载均衡组。与备切换情况（只能有一个主节点）不同，负载均衡集群中的每个节点必须是所属组的主节点，以便接收流量。组的选择——以及扩展到物理主机——通过 CARP 的哈希值决定。备切换情况下计算基于源 MAC 地址，而在负载均衡情况下，计算基于源 IP 和目的 IP 地址。这种方案的缺点是，在负载均衡配置时，每个组会更快地消耗 ID。

CARP 广播模式在负载均衡配置中与备切换起着类似的角色，但 `ifconfig`（以及 `hostname.hostname`）输出略有不同。

## 设置 CARP 负载均衡

将之前的部分构建到负载均衡集群，只需编辑配置文件并重新加载。在以下示例中，我们选择了负载均衡模式。如果你选择不同的方案，配置本身也会不同。

在第一个主机上，我们修改 `/etc/hostname.carp0`，说明 carpo 接口是 whid 5 的成员（切换值为 100），同时它是切换到主节点的备选候选。接下来，我们修改 `/etc/hostname.carp1`：carpi 的成员为 whids 3 和 4，切换值分别为 100 和 0。对于另一台主机，切换值是反转的，但其他配置是类似的。在这里，`/etc/hostname.carp0` 读取：carpo 接口是 whid 5 的成员，也是 whid 6 的成员。与之对应的是 `/etc/hostname.carp1` 文件，内容为：carpi 是 whid 3 和 4 的成员，在第一个主机上其切换值为 0，在另一个主机上为 100。第一个主机上 carpi 组的 `ifconfig` 输出如下：

```
# ifconfig carpi

carpo: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500

lldaddr 01:00:5e:00:01:05

priority: 0

carpo: carpdev vr0 advertise 1 balancing ip

state MASTER whid 5 advskew 0

state BACKUP whid 6 advskew 100

groups:

inet 192.0.2.1 mask 0xffffff broadcast 192.0.2.255

inet6 fe6:fe80::24ff:fe8c:1c10/carpo prefix 64 scope iex7

carpi1: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500

lldaddr 01:00:5e:00:01:03

priority: 0

carpi: carpdev vr1 advertise 1 balancing ip

state MASTER whid 3 advskew 0

state BACKUP whid 4 advskew 100

groups:

inet 192.168.12.1 mask 0xffffff broadcast 192.168.12.255

inet6 fe80::24ff:fe8c:1c10/carpi prefix 64 scope iex8
```

另一个主机的 `ifconfig` 输出：

```
$ ifconfig carp

carpo: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500

lldaddr 01:00:5e:00:01:05

priority: 0

carp: carpdev vr0 advbase 1 balancing

state BACKUP whid 5 advskew 100

state MASTER whid 6 advskew 0

groups: carp

inet 192.0.2.19 netmask 0xffffff broadcast 192.0.2.255

inet6 fe80::200:24ff:febc:c138&carpo prefixlen 64 scope ox7

carpi: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500

lldaddr 01:00:5e:00:01:03

priority: 0

carp: carpdev vr1 advbase 1 balancing

state BACKUP whid 3 advskew 100

state MASTER whid 4 advskew 0

groups: carp

inet 192.168.12.1 netmask 0xffffff broadcast 192.168.12.255

inet6 fe80::200:24ff:febc:c138&carpi prefixlen 64 scope ox8

pfsync: flags=41<UP,RUNNING> mtu 1500

pfsync: syncdev: vr2 syncpeer: 10.0.12.16 maxupd: 128 defer: 0

groups: carp pfsync
```

如果我们的负载均衡方案中有三个节点，那么每个 carp 接口都需要成为一个额外的组成员，总共三个组。简而言之，每在负载均衡组中引入一个物理主机，每个 carp 接口就会成为额外组的成员。

一旦设置好负载均衡集群，请在负载集群中的每个主机上运行 `sysstat states` 几分钟，通过检查连接流情况来确保系统按预期工作，并确认你付出的努力是值得的。

# 9

# 日志、监控与统计

控制网络——无论是为了你的家庭网络需求还是在专业背景下——可能是任何阅读此书的人的主要目标。保持控制的一个必要要素是能够访问有关网络中发生情况的所有相关信息。幸运的是，对于我们像大多数类 Unix 系统的组件一样，PF 能够为网络活动生成日志数据。

PF 为设置日志详细程度、处理日志文件和提取特定类型的数据提供了丰富的选项。你已经可以使用基础系统中的工具完成很多工作，还可以通过包管理器获取其他工具，以多种实用的方式收集、研究和查看日志数据。在本章中，我们将更深入地查看 PF 日志以及你可以用于提取和展示信息的某些工具。

## PF 日志：基础

PF 记录的信息以及日志详细程度由你决定，这取决于你的规则集。PF 日志非常简单：对于你想要记录数据的每条规则，添加 `log` 关键字。当你加载带有 `log` 关键字的一个或多个规则的规则集时，任何触发匹配日志规则（阻止、通过或匹配）的连接数据包都会被复制到 `pflog` 设备。数据包在 PF 看到它的同时，以及在评估日志规则的同时被记录。

> 在复杂的规则集中，数据包可能会因为匹配（match）或通过（pass）规则而经过多次转换，进入主机时匹配数据包的准则在转换后可能不再匹配。

PF 还会存储额外数据，例如时间戳、接口、原始源和目的 IP 地址、数据包是被阻止还是通过的，以及来自加载规则集的中的关联规则编号。

PF 数据由 `pflog` 守护进程收集，该进程在系统启动时启用 PF 时默认启动。存储日志的默认位置是 `/var/log/pflog`。日志以二进制格式写入，通常称为数据包捕获格式 (pcap)，该格式旨在供 `tcpdump` 读取和处理。我们将讨论从日志文件中提取和显示信息的额外工具。日志文件格式是一种文档详尽且被广泛支持的二进制格式。

作为开始，这里有一个基础日志示例。从你想要记录的规则开始并添加 `log` 关键字：

```
block log

pass log proto { tcp, udp } to port ssh
```

重新加载规则集，你应该会看到 `/var/log/pflog` 文件上的时间戳随着文件的开始增长而变化。要查看其中的内容，使用 `tcpdump` 配合 `-r` 选项读取文件。

如果日志已经运行了一段时间，在命令行中输入以下内容可以产生大量的输出：

```
$ sudo tcpdump -n -ttt -r /var/log/pflog
```

例如，这些是几个屏幕输出的前几行，几乎每一行都足以换行：

```
$ sudo tcpdump -n -ttt -r /var/log/pflog

tcpdump: WARNING: snaplen raised from 116 to 160

Sep 13 13:00:30.556063 rule 10/(match) pass out en0: 194.54.107.34 > 194.54..03..6:113: S 3397631277333367(0) win 16384 <1460,nop,nop,wscale 0|[tcp] (OF)

Sep 13 13:00:30.556063 rule 10/(match) pass out pf0: 194.54.107.34 > 194.54..03.6:113: S 3397631277333367(0) win 16384 <1460,nop,nop,wscale 0|[tcp] (OF)

Sep 13 13:01:76.9096 rule 10/(match) pass in vr2: 194.54.107.34 > 194.54..03.6:113: S 2345549144:234549144(0) win 16384 <1460,nop,nop,wscale 0|[tcp] (DF)

Sep 13 13:01:79.6120 rule 10/(match) pass out vr2: 194.54.107.34 > 194.54..03.6:113: S 2345549144:234549144(0) win 16384 <1460,nop,nop,wscale 0|[tcp] (DF)

Sep 13 13:01:15.0963 rule 10/(match) pass in vr2: 194.54.107.29774 > 194.54.103.6:113: S 716308(df) [0]
```

`tcpdump` 程序非常灵活，特别是在输出方面，它提供了许多选择。示例中的格式遵循传递给 `tcpdump` 的选项。`tcpdump` 程序始终显示数据包到达的时间（`-ttt` 选项指定此格式）。列出加载的编号、数据包出现的接口、源地址和目标地址（`-n` 选项显示 IP 地址而非主机名）以及它的各种属性。

日志中的规则引用内存中的规则集。规则集在加载期间通过一些自动步骤，例如宏展开和优化，这导致日志中的规则编号可能与你从 `pf.conf` 文件顶部计数的不符。如果不确定是哪条规则，请使用 `pfctl -vs rules` 并查看输出。在我们的 `tcpdump` 输出中，加载规则集中的规则 (10) 似乎是一个匹配域名和名称查找的通用规则。这就是你在调试时会看到的输出，而且为了掌控网络，拥有这类数据至关重要。通过一点努力并仔细阅读 `tcpdump` 手页，你应该能够从日志中提取信息。

要查看实时流量，你可以使用 `tcpdump` 直接从日志设备读取日志信息。这样做请使用 `-i` 选项指定你用于 `tcpdump` 的接口，如下（`-l` 输出开启缓冲，有助于查看你正在捕获的内容）：

```
$ sudo tcpdump -i1 pf0

Apr 29 22:07:36.097434 rule 16/(match) pass in xlo: 85.19.150.98.53 > 213.187.179.198.41101:63267-1/0 (6)

Apr 29 22:07:36.097760 rule/(match) pass out emo: 213.187.179.198.22 192.168.103.44.30827: P 1825000872:182500883(76) ack 884130750 17520 [0 tcp]

Apr 29 22:07:36.093866 rule/(match) pass in emo: 192.168.103.44.30827 213.187.179.198.22:. ack 76 16308 (df) [0 tcp]

Apr 29 22:07:36.099544 rule 442/(match) pass in xlo: 93.57.15.161.488 > 213.187.179.198.80: P 350741894 65536 <nop,timestamp 4170023961 0
```

## 注意

有时你主要对特定主机之间的流量或匹配特定准的流量感兴趣。对于这些情况，`tcpdump` 的过滤功能可能非常有用。详情请阅 `tcpdump`。

## 记录数据包通过规则集的路径：log (matches)

当匹配（match）发生时，所有后续规则也将将被进行记录。因此，你可以使用目标日志（匹配，matches）语句来跟踪数据包通过你已加载规则集的路径，这使得梳理复杂的规则变得容易得多。

例如，考虑下面这个带有 NAT 的简单规则集。日志（匹配）规则如下：

```
match (matches) on $int $from $thehost localnet
```

我们的测试主机是本地网络中的某台工作站，IP 地址为 192.168.103.44。当测试主机查找互联网上的网站时，记录的信息看起来所示：

```
Apr 29 21:08.243674 3/(match) in emo: 192.168.103.44.14054 > 81.93.163.115.80 S 131487359:S131487359(0) win 16384 cmss 1460,nop,sackOK,nop,wcale 3,nop,timestamp 73550303[tcp] (D)
```

```
Apr 29 21:08.243687 11/(match) in emo: 192.168.103.44.14054 > 81.93.163.115.80 S 131487359:S131487359(0) win 16384 cmss 1460,nop,sackOK,nop,wcale 3,nop,timestamp 73550303[tcp] (D)
```

```
Apr 29 21:08.246847 17/(match) in emo: 192.168.103.44.14054 > 81.93.163.115.80 S 131487359:S131487359(0) win 16384 cmss 1460,nop,sackOK,nop,wcale 3,nop,timestamp 73550303[tcp] (D)
```
