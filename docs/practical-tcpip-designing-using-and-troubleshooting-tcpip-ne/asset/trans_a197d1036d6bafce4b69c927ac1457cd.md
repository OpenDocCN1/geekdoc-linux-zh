
## 我的输出包含大量“SMB”和“NBT”消息

```
(DF) (ttl 128, id 38109, len 141)
212.140.133.17.139 > 212.140.133.7.4950: P 1:103(102) ack
>>> NBT Packet
NBT Session Packet
Flags=0x0
Length=98 (0x62)
SMB PACKET: SMBtrans2 (REPLY)
SMB Command   = 0x32
```

这本应是一个功能，但它如此具有侵入性，我们宁愿称其为 bug。tcpdump 已被扩展以了解 Microsoft Windows 网络，这正是这些消息所涉及的内容。它们占用多行，并且无法以通常的方式控制。然而，你可以通过在过滤表达式后附加一个“NOT”子句来排除它们，例如

```
tcpdump -n "host 10.9.8.7 and not (port 137 or 138 or 139)"
```

（我们将在第 18 章解释这些端口号。）

## 数据包被丢弃（丢失）

当 tcpdump 结束时，它会打印处理的数据包数量统计信息：

```
17:50:24.540261 192.0.2.7.4950 > 192.0.2.19.139: . 502119:5
1773 packets received by filter
12780 packets dropped by kernel
```

如果数据包被内核丢弃，那么流量可能太多，这台可怜的小机器无法处理。你可以通过将数据包写入文件（参见附录 4）并稍后处理来减少它需要做的工作量，和/或使用“-s num”选项减少每个数据包捕获的数据量。

新的快速机器通常不会丢弃任何东西，但我们一些古老的 Sun 工作站和旧的 486 笔记本电脑无法跟上重负载流量。即便如此，它们对于诊断特定的网络问题仍然足够，因为

- 我们通常可以指定非常精确的过滤表达式，以限制机器需要执行的处理

- 大多数网络问题只需几个数据包或几十个数据包即可复现。你只有在寻找由硬件或软件 bug 引起的中断性问题时（而不是导致 99.9% 问题的错误配置）才需要捕获大量数据。

## tcpdump: socket: 操作不被允许

你不是以 root 用户运行。

## tcpdump: 解析错误或指定过滤表达式时出现问题

大多数情况下，错误是由于在 IP 号码或名称前忘记输入“net”或“host”造成的。幸运的是，tcpdump 会给出错误信息，因此虽然打字错误很容易发生，但很难输入一个不是你本意但仍然有效的过滤表达式（除非你在混合使用“and”、“not”和“or”时搞混了，就像我们有时仍然会做的那样，可惜）。

## 摘要

- **tcpdump** 让你捕获并查看出现在你的机器网络接口上的所有数据包
- 由于以太网的工作方式，除非你使用以太网交换机，否则连接到此以太网的所有其他机器的数据包也会在你的机器接口上可见。如果你拥有必要的权限，**tcpdump** 可以通过将网络接口置于混杂模式来查看这些数据包
- 你可以告诉 **tcpdump** 你希望它显示哪些数据包，以便专注于你感兴趣的特定流量。

## 下一步？

在第 2 章中，我们构建一个非常小的网络，由单以太坊上两台机器组成，并探索数据包如何在机器之间传输。我们将大量使用 **tcpdump** 来实现这一点。

## 注释和进一步阅读

> 提示：因为我们经常希望在网络上看到可疑情况时能够启动 **tcpdump** *非常* 快速，我们已使用 Linux shell 的“alias”功能将“`t`”定义为 **tcpdump** 的快捷方式：
> ```bash
> alias t="tcpdump -n -t"
> ```
> 这样我们只需输入“`t`”即可运行 **tcpdump**。

你可以在同一台机器上同时运行多个 **tcpdump** 实例，每个实例捕获不同的数据包集。这些独立的实例互不干扰。

**tcpdump** 起源于加州伯克利的劳伦斯伯克利国家实验室 (http://ee.lbl.gov/)。**tcpdump** 现在由以下机构维护

- [http://www.tcpdump.org](http://www.tcpdump.org)

它在 Linux 以及许多其他版本的 UNIX 平台上运行。多年来它已被大量增强，其他版本在语法上可能与我们描述的略有不同。然而，它们的基本操作都相同。

**windump**，**tcpdump** 的 Windows 版本，来自

- [http://netgroup-serv.polito.it/windump/](http://netgroup-serv.polito.it/windump/)

它还提供了 **windump** 运行所需的库（特别是名为 WinPcap 的 **libpcap** Windows 版本）。

**tcpdump** 使用 **libpcap** 数据包捕获库，根据 **libpcap** 发布说明：

提供了一个可移植的低级网络监控框架。应用包括网络统计收集、安全监控、网络调试等。由于几乎每个系统厂商都提供不同的数据包捕获接口，并且我们开发了需要此功能的多个工具，我们创建了这个系统无关的 API 以便于移植并减轻每个应用程序中需要多个系统相关数据包捕获模块的需求。
...

libpcap 接口支持基于 BSD 数据包过滤器架构的过滤机制。BPF 在 1993 年冬季 Usenix 论文“The BSD Packet Filter: A New Architecture for User-level Packet Capture.” 中有描述。压缩的 postscript 版本在

- ftp://ftp.ee.lbl.gov/papers/bpf-usenix93.ps.Z

libpcap 被大量嗅探器类工具使用，包括下面提到的 **ethereal** 和 **ngrep**。因此，它们都使用相同的语法来选择数据包，这很方便。

嗅探器是安全隐患。它们可以轻松捕获用户名和密码以及几乎任何未加密的内容。在美国，FBI 运行一个名为 Carnivore（现更名为不太有趣的“DCS1000”）的数据包嗅探系统，用于在 ISP 处“窃听”流量。参见：

- http://www.fbi.gov/hq/labs/carnivore/carnivore.htm

- http://www.epic.org/privacy/carnivore/

有关嗅探和窃听的许多有趣信息，请参见：

- http://www.robertgraham.com/pubs/sniffing-faq.html

## 安装问题

我们从未遇到过 **windump** 安装失败的情况——尽管有时你需要查看 **windump** 站点的常见问题解答来解决一些小问题。但即使由于某种奇怪原因无法让 **windump** 工作，也绝非无计可施：你可以使用 **ethereal** 或 Windows Network Monitor（见下文 *Other sniffers*）。它们以不同格式提供相同的信息，因此你总能获得所需的信息。我们稍后会介绍这两个嗅探器；除非必要，否则现在不必理会它们。

**libpcap** 文档说：

> > “为了让 libpcap 能够在 Linux 系统上捕获数据包，‘packet’ 协议必须得到你的内核支持。如果不是，你可能会收到诸如：
> > modprobe: can't locate module net-pf-17
> > in “/var/adm/messages”，或可能收到诸如
> > socket: Address family not supported by protocol
> > 来自使用 libpcap 的应用程序的消息。”

上述内容来自 **libpcap** 发行版的 **README.linux** 文件，也可在网上获取：
- http://www.tcpdump.org/cgi-bin/cvsweb/libpcap/README.linux and click on the most recent version number (currently 1.2) to obtain the full text of the file

然而，几乎所有标准 Linux 发行版默认都已启用必要的设施。

旧版本的 **windump** 有时会抱怨类似的消息：

```
windump: listening on \\Device\\Packet_E100B1
windump: Error opening adapter
```

我们在最近的版本中没有看到这些问题，但如果你遇到问题，请在网上搜索解决方案（例如使用 Google）或查看 **windump** 或 **ethereal**（见下文）网站以获取提示。然而，我们发现 Linux 版本更可靠，因此如果你可以选择平台，请选择 Linux。

> 提示：如果你可以的话，专门分配一台机器用于 **tcpdump** 或 **windump**。我们为此目的使用一台旧的 486 笔记本电脑——它几乎不花钱，我们可以轻松将其移动到网络的任何需要部分。

## 其他嗅探器

我们在书中后面为特定目的使用几种其他嗅探器：

- **ethereal** (Chapter 13): 一个在 Linux 和 Windows 上运行的带 GUI 的“协议分析器”。很容易看到数据包的每个细节甚至以太网帧数据

- **ngrep** (Section 13.7): 在数据包数据中搜索给定字符串并将匹配的数据包作为 ASCII 文本打印

- **Windows Network Monitor** (Chapter 18): 与 **ethereal** 非常相似但仅在 Windows 上运行。作为标准包含在 Windows-NT 中。

其他 UNIX 系统有或多或少类似的工具，例如 Solaris 有 **snoop**，古老的 SunOS 有 **Etherfind**。

## 附录

- 内封面：分配的 TCP 和 UDP 端口号

- 附录 3：以太网 UTP 集线器和交换机

- 附录 4：**tcpdump** 命令摘要

- 附录 5：完整的 **tcpdump** 手册页
