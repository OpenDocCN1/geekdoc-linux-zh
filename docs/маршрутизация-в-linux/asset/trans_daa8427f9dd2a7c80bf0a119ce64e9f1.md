

例如，我可能会得到以下内容（这些是真实的 IP 地址；请勿将其用于实际测试目的）：

```
default_source_preference 105
```

```
phyint 199.60.103.90 disable
phyint 199.60.103.91 preference 1029
phyint 199.60.103.92 preference 1024
cand_rp 199.60.103.91
cand_bootstrap_router 199.60.103.92
group_prefix 199.60.103.0 masklen 4
switch_data_threshold rate 60000 interval 10
switch_register_threshold rate 60000 interval 10
```

## 运行 pim d

配置完配置文件后，你就可以实际运行 PIM-SM 守护进程 pim d 了。像往常一样，我们建议你先手动运行它进行测试，然后再将该守护进程连同其所需的启动标志一起添加到系统的启动脚本中。

运行此守护进程的格式为

```
pimd -c file -d level1,...levelN
```

这两个标志及其值都是可选的：

- **-c file.** 使用指定的配置文件，而不是默认的 /etc/pimd.conf。
- **-d level1,...levelN.** 指定运行此守护进程时使用的调试级别。输入 pimd -h 可查看这些级别的完整列表。

## DVMRP 守护进程：mrouted

为了你的 DVMRP 路由乐趣，我们选择介绍 mrouted（ftp://parcftp.xerox.com/pub/net_research/ipmulti/）。再次强调，这并不是唯一可用的工具，但我们选择介绍它，因为它功能单一且可自由获取，就像 pim d 一样。有关其他 DVMRP 选项，请参阅章节侧边栏。

多播社区发现 DVMRP 并不能完全满足其内部使用的需求。主要问题是该协议在重负载下表现不佳，而 PIM-SM 则具有很强的可扩展性。如今，该协议在将你的网络连接到 MBONE（http://www.live.com/mbone/）时发挥作用，后者专门使用 DVMRP。

## 使用 zebra 进行多协议多播路由

GNU 的 zebra 也是在单播和多播世界中都很有用的另一个守护进程。对于单播，该守护进程处理 BGP4、OSPF、RIP-1、RIP-2 等。然而，在这种情况下，多播功能尚未添加到主 zebra 版本中。你可以在 http://www.zebra.org 上了解其进展。

## 配置 mrouted

再次，我们处理的是一个单一功能的守护进程。这使我们受益于相当直接的配置过程。mrouted 的配置文件为 /etc/mrouted.conf。其中一些设置必须按特定顺序呈现。本章会在需要时明确说明。其余部分顺序无关紧要；因此，如果你没有看到关于顺序的说明，选项的呈现顺序就是它们通常使用的顺序。

mrouted 配置文件通常以一个或多个 name 语句选项开头。你以以下格式使用此命令

```
name boundaryname boundaryaddr/masklen
```

这三个变量为

- boundaryname。你为想要设置规则的特定地址集合分配的名称。
- boundaryaddr。你命名的网络或子网地址。
- masklen。你命名的网络或子网的网络掩码开头部分的二进制 1 的数量。

通常，下一个行涉及 cache_lifetime 选项。它以以下格式使用

```
cache_lifetime seconds
```

seconds 设置通过 DVMRP 学习到的信息在内核中存储的时间。默认值为 300，指南规定应将其保持在 5 分钟（300 秒）到 1 天（86,400 秒）之间。此语句之后通常会出现以下两行之一：

```
pruning on
pruning off
```

IPaddr 告诉 phyint 你指的是哪个物理接口，可以是 IP 地址或接口名称，例如 eth0。之后，你可以添加一系列选项以满足你的需求：

- **disable**。指示不通过此接口路由任何 DVMRP 流量。
- **metric metric**。从多播源向此接口发送数据的成本。对于接口有效，metric 应低于 31。通常建议使用 1。
- **threshold threshold**。数据包必须具有的最小互联网协议（IP）生存时间设置，mrouted 才会将此数据包发送到接口。此值以秒为单位。
- **rate_limit rate_limit**。如果要限制，则此接口将接受的多播流量的速率，以 Kbits/秒为单位。
- **boundary boundaryname**。将此规则集应用于先前使用 name 语句定义的网络块。你可以有多个此选项。
- **boundary boundaryadd/masklen**。将此规则集应用于由这些变量指定的网络块，其用法与在 name 语句中使用的方式相同。你可以有多个此选项。
- **altnet subnet/masklen**。如果相关接口通向多个子网，你可以使用此选项来细化数据路径。subnet 指的是你想要设置的特定子网的网络地址，masklen 与 name 语句中的定义相同。你可以有多个此选项。
- **altnet subnet**。如果相关接口通向多个子网，你可以使用此选项来细化数据路径。subnet 指的是你想要设置的子网的网络地址，并假定不需要网络掩码。你可以有多个此选项。

现在我们终于遇到了一个顺序问题。这里的最后一种可能性是 tunnel 语句，你可以利用它在仅支持单播的网络空间中设置一种单播方法，通过该方法将你的多播数据从一台 mrouted 机器传输到另一台。你必须在物理接口之后定义你的隧道。此项的基本格式为 tunnel local remote

顾名思义，local 指的是开始隧道的已连接接口——可以是 IP 地址或设备名称——remote 指的是另一端用于接收数据的接口的 IP 地址。所有附加选项都与 phyint 中可用的选项相同：metric、threshold、rate_limit、boundary boundaryname 和 boundary boundaryadd/masklen。请参阅之前的项目符号列表，了解这些选项的定义以及如何设置它们。

例如，我可能会将我的配置文件设置得尽可能接近 PIM-SM 配置文件，如下所示：

```
name multi 199.60.103.0/32
cache_lifetime 21600
```

