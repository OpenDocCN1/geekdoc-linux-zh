
为了你的 PIM-SM 路由需求，我们选择介绍 `pimd`（`ftp://catarina.usc.edu/pub/pim/pimd/`）。正如你将在本章的侧边栏中了解到的那样，在 Linux 下你还有其他选择，但这里介绍这个最有意义。`pimd` 是一个单一用途、单一协议的守护进程。在看到第 5 章“Inside the Unicast Kernel 2.2.x Daemons”中公共 `gated` 配置的复杂性后，你可能会发现这一事实是一种福音。

PIM-SM 似乎注定会成为组播社区中的最爱。它是一种开销低的协议，并且能高效地引导流量，尤其是在稀疏模式情况下，即收听特定组播频道的人位于网络上分布广泛的机器上（而不是在近距离范围内）。

## 使用 Multicast gated 进行多协议、多播路由

> 多播版本的 `gated`（`www.gated.org`）在单个程序中处理 PIM-SM、协议无关多播-密集模式（PIM-DM）、DVMRP 和多播源发现协议（MSDP）。它没有在本章中介绍，因为它不是自由可用的，但对于许多人来说，这个程序物有所值。尤其是当你需要运行一个以上的多播程序时，你可能只需要这样做。原因在“ DVMRP Linux 守护进程：`mrouted` ”一节中有讨论。

## 配置 pimd

由于 `pimd` 是一个单功能守护进程，其配置实际上并不复杂——至少与 `gated` 这样的大型工具相比是如此。配置数据保存在文件 `/etc/pimd.conf` 中。虽然语句的顺序不必严格遵循下面即将介绍的内容，但我将带你了解你可能想要添加到此文件中的内容。

`/etc/pimd.conf` 文件以以下语句开始：

`default_source_preference value`

路由器会举行选举来确定哪个成为站点的上游路由器。由于 `pimd` 是一个如此专注的工具，你通常不希望它胜过更通用的工具。在此处使用 101 的值是确保 `gated` 和其他路由工具将赢得选举并让 `pimd` 处理其 PIM-SM 的最低值。下一行是

`default_source_metric value`

此项设置通过此路由器的传输成本。你只希望 PIM-SM 数据发送到此守护进程；因此，再次建议使用高值以防止意外使用。首选默认值是 1024。

尽管你可以交换前两个语句的顺序，但在设置 `default_source_metric` 之后，你必须有下一个语句。此项以开头

`phyint interface`

`phyint` 指物理接口。你用 `Interface` 填入对以太网卡或其他网络接口的引用，用设备的 IP 地址或名称（例如，`eth0`）来告诉 `pimd`。如果你只想使用默认值激活此接口，则无需在该行上添加其他内容。然而，你可以添加一些额外的项。这些项按你需要使用的顺序如下：

- `disable` 不要通过此接口发送 PIM-SM 流量，也不要从此接口侦听 PIM-SM 流量。
- `preference pref`。此接口在选举中的价值。如果未分配，则将具有 `default_source_preference`。
- `metric cost`。通过此接口发送数据的成本。如果未分配，则将具有 `default_source_metric`。

为此路由器上的每个接口添加一行 `phyint`。如果不这样做，`pimd` 将简单地假设你希望它使用机器上的所有接口并使用默认值。如果你为一个或多个接口设置 `phyint` 但不是全部，缺失的接口将被分配默认值。在此之后，从下一行开始 `cand_rp`

`cand_rp` 指候选汇聚点（CRP）。此语句指定此机器上的哪个接口应包含在 RP 选举中。可供选择的附加选项按使用顺序列出如下：

- `ipaddr`。默认值为最大的已激活 IP 地址。如果你不想使用该接口，请将要使用的接口的 IP 地址添加为下一个项。
- `time value`。两次广告此 CRP 之间等待的秒数。默认值是 60 秒。
- `priority num`。此 CRP 相对于其他 CRP 的重要性。此处的值越低，CRP 越重要。

下一行以 `cand_bootstrap_router` 开始

在这里，你提供此机器作为候选引导路由器（CBSR）广告自己的信息。如果需要，在 `cand_bootstrap_router` 之后添加 `ipaddr` 和/或 `priority` 项，如前所述定义。接下来是一系列以 `group_prefix` 开始的语句

每个 `group_prefix` 语句概述了 CRP 如果赢得选举，将向其他路由器通告的多播地址集合。你可能在此处包含的两项按顺序列出如下：

- `groupaddr`。此路由器将处理的特定 IP 或网络范围。请记住，单个多播网络写成单个 IP 地址。
- `masklen len`。掩码占用的 IP 地址段数。请记住，多播地址是 D 类，其网络掩码为 255.255.255.255，这意味着其长度为 4。

之后是 `switch_data_threshold rvalue interval ivalue`

此语句定义了传输速率触发从共享树切换到 RP 树的阈值；以 `switch_register_threshold` 开始的行以相同格式做相反操作。（有关两种 PIM-SM 树的更多详细信息，请参阅第 2 章“多播协议”。）无论你选择哪一个，`rvalue` 代表以位/秒为单位的传输速率，而 `ivalue` 设置以秒为单位采样速率的频率——建议最小值为五秒。`pimd` 程序员建议在两个语句中 `ivalue` 相同。

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

配置完配置文件后，你就可以实际运行 PIM-SM 守护进程 `pimd` 了。像往常一样，我们建议你先手动运行它进行测试，然后再将该守护进程连同其所需的启动标志一起添加到系统的启动脚本中。

运行此守护进程的格式为

```
pimd -c file -d level1,...levelN
```

这两个标志及其值都是可选的：

- `-c file`。使用指定的配置文件，而不是默认的 `/etc/pimd.conf`。
- `-d level1,...levelN`。指定运行此守护进程时使用的调试级别。输入 `pimd -h` 可查看这些级别的完整列表。

## DVMRP 守护进程：mrouted

为了你的 DVMRP 路由乐趣，我们选择介绍 `mrouted`（`ftp://parcftp.xerox.com/pub/net_research/ipmulti/`）。再次强调，这并不是唯一可用的工具，但我们选择介绍它，因为它功能单一且可自由获取，就像 `pimd` 一样。有关其他 DVMRP 选项，请参阅章节侧边栏。

多播社区发现 DVMRP 并不能完全满足其内部使用的需求。主要问题是该协议在重负载下表现不佳，而 PIM-SM 则具有很强的可扩展性。如今，该协议在将你的网络连接到 MBONE（`http://www.live.com/mbone/`）时发挥作用，后者专门使用 DVMRP。

## 使用 zebra 进行多协议多播路由

GNU 的 `zebra` 也是在单播和多播世界中都很有用的另一个守护进程。对于单播，该守护进程处理 BGP4、OSPF、RIP-1、RIP-2 等。然而，在这种情况下，多播功能尚未添加到主 `zebra` 版本中。你可以在 `http://www.zebra.org` 上了解其进展。

## 配置 mrouted

再次，我们处理的是一个单一功能的守护进程。这使我们受益于相当直接的配置过程。`mrouted` 的配置文件为 `/etc/mrouted.conf`。其中一些设置必须按特定顺序呈现。本章会在需要时明确说明。其余部分顺序无关紧要；因此，如果你没有看到关于顺序的说明，选项的呈现顺序就是它们通常使用的顺序。

`mrouted` 配置文件通常以一个或多个 `name` 语句选项开头。你以以下格式使用此命令

```
name boundaryname boundaryaddr/masklen
```

这三个变量为

- `boundaryname`。你为想要设置规则的特定地址集合分配的名称。
- `boundaryaddr`。你命名的网络或子网地址。
- `masklen`。你命名的网络或子网的网络掩码开头部分的二进制 1 的数量。

通常，下一个行涉及 `cache_lifetime` 选项。它以以下格式使用

```
cache_lifetime seconds
```
