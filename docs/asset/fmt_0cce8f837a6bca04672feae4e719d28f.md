
```
tcpdump: listening on eth0
15:41:58.056289 durer.home.com.1032 > socrates.home.com.telnet: tcp 0 (0F) [tos0x50]
15:41:58.056446 socrates.home.com.telnet > durer.home.com.1032: tcp 28 (DF)
15:41:58.274933 durer.home.com.1032 > socrates.home.com.telnet: tcp 0 (0F) [tos0x50]
15:41:58.275116 socrates.home.com.telnet > durer.home.com.1032: tcp 164 (DF)
15:41:58.494694 durer.home.com.1032 > sophos.home.com.telnet: tcp 0 (DF) [tos0x50]
15:41:58.494880 sophos.home.com.telnet > durer.home.com.1032: tcp 165 (DF)
15:41:58.544828 sophos.home.com > didymus-gw2.home.com: icmp: echo request
15:41:58.545719 didymus-gw2.home.com > sophos.home.com: icmp: echo reply
15:34:10.601950 sophos.home.com.telnet > durer.home.com.1032: tcp 165 (DF)
```

8 packets received by filter

0 packets dropped by kernel

输出包括时间、源/目的地、协议端口、帧内包含的协议以及附加协议信息。在本例中，源主机 `durer` 和目标主机 `socrates` 建立了一个 Telnet 会话。我们可以通过查看目标端口（即 telnet）来判断这一点。默认情况下，`tcpdump` 会持续捕获数据包，直到用户发出 ^c 中断程序。此外，`socrates` 向 `didymus-gw2` 发出了 `ping request`，后者响应了回复。字符串 `>` 表示通信方向。请注意，`tcpdump` 始终将通信路径定向为指向右侧，如上述 ICMP Echo request 所示。为了表示相反方向的通信，`tcpdump` 会交换主机位置（而非指针），如 ICMP Echo reply 条目所示。`tcpdump` 命令以小写显示高层协议，如 `tcp` 和 `icmp`，随后是与该协议相关的更具体信息，可能包括端口、附加协议信息和数据。输出还包括用户终止命令前捕获的数据包数量摘要。

输出末尾包含 `tcpdump` 捕获的数据包数量和丢弃的数据包数量。在本例中，共捕获八个数据包，零个数据包被丢弃。

`tcpdump` 工具提供大量命令行选项，用于选择捕获模式、控制输出、指定过滤器规范和指定附加操作特性。这些选项按功能分组，包括以下类别：

- 操作模式
- 显示选项
- 数据包过滤选项

### 操作模式选项

这些选项用于控制 `tcpdump` 如何捕获和显示网络流量。可用选项汇总见表 4.10，详细说明如下。

**表 4.10** `tcpdump` 操作模式选项

| 选项 | 说明 |
| --- | --- |
| -c | 捕获指定数量的数据包 |
| -F | 使用文件作为过滤表达式的来源 |
| -i | 使用备用网络接口捕获数据包 |
| -p | 禁用混杂模式捕获 |
| -r | 读取捕获文件而非网络接口 |
| -w | 将原始数据包保存到文件 |

通常，`tcpdump` 将在主网络接口上监听流量。如果系统包含两个或多个同类型接口，主接口通常具有最小的数字标识符。例如，当系统包含两个以太网接口 `eth0` 和 `eth1` 时，`eth0` 被视为主接口。但是，如果您想在其他接口上运行 `tcpdump`，请使用 `-i` 选项和设备名称指定备用接口。例如，要选择点对点 `ppp` 接口，请使用以下命令：

```
# tcpdump -i ppp0
tcpdump: listening on ppp0
```

如前所述，`tcpdump` 将持续捕获数据包，直到从控制终端输入 ^C（或如果放入后台，则直到进程被 `kill` 命令终止）。如果您想指定捕获的数据包数量，请使用 `-c` 选项后跟数据包计数值。要从 `eth1` 接口捕获十个数据包，请使用以下命令：

```
tcpdump -t -q -i eth1 -c 10
tcpdump: listening on eth1
didymus-gw2.home.com > socrates.home.com: icmp: echo request
socrates.home.com > didymus-gw2.home.com: icmp: echo reply
didymus-gw2.home.com > socrates.home.com: icmp: echo reply
socrates.home.com > didymus-gw2.home.com: icmp: echo request
didymus-gw2.home.com > socrates.home.com: icmp: echo reply
socrates.home.com.1032 > switch.home.com.snmp: snmp: udp 44
switch.home.com.snmp > socrates.home.com.1032: udp 111
socrates.home.com.1032 > switch.home.com.snmp: snmp: udp 51
switch.home.com.snmp > socrates.home.com.1032: udp 61
socrates.home.com.1032 > switch.home.com.snmp: snmp: udp 51
switch.home.com.snmp > socrates.home.com.1032: udp 54
socrates.home.com.1032 > switch.home.com.snmp: snmp: udp 51
```

在本例中，`tcpdump` 捕获了 `socrates` 和 `didymus-gw2` 之间的 `ping` 会话，这由前四行检测到。此外，`socrates` 正使用 SNMP 查询名为 `switch` 的设备，这由 SNMP 端口和使用的 UDP 协议表示（其余各行）。我们可以通过计算显示的行数来确认捕获的数据包数量。当意图是监控使用固定数量数据包交换的关键网络事务时，指定捕获的数据包数量非常有用。在 Shell 脚本中监控数据包时，此选项也很有用，因为您无需担心启动 `tcpdump` 后如何停止它。本例中还使用了 `-t` 选项，该选项移除数据包时间戳信息。

如前所述，`tcpdump` 默认以 `混杂模式` 打开网络接口以捕获所有网络流量。混杂模式意味着无论数据包的目标如何，所有网络流量都将被 `tcpdump` 捕获。有时，检查发送给指定主机的数据包比读取网络上的所有数据包更有效。如果我们想捕获发送给运行 `tcpdump` 的主机的那些数据包，则使用 `-p` 选项禁用混杂模式捕获。稍后您将看到，我们可以使用过滤器告诉 `tcpdump` 捕获来自或发往特定主机的数据包。

遗憾的是，`tcpdump` 命令无法确认是否使用了 `-p` 选项。因此，用户在命令执行后无法知道它正以哪种模式进行捕获，除非检查输出以查看目标地址。换句话说，任何不是广播或发送给本地地址的数据包，都表明 `tcpdump` 已启用混杂模式进行捕获。无论如何，为什么要用这个选项禁用混杂模式呢？有时有必要仅检查正常到达特定系统的流量。使用此选项，我们可以看到发往本地系统的每个数据包，而不再有其他内容。这可用于轻松检测（通过监控传入数据包），例如，对特定服务的请求是否到达了该系统。在客户端/服务器环境中，我们可以确定来自客户端系统的请求是否到达了服务器（通过在服务器上运行 `tcpdump`），或者特定客户端首先是否正在发送请求（通过在客户端上运行 `tcpdump`）。诚然，我们可以使用过滤器完成同样的事情，但首先减少数据包数量会更高效、更容易。

在非常活跃的网络或繁忙的系统上，以及使用某些命令行选项时，`tcpdump` 会产生大量输出。为了帮助管理此问题，可以使用 `-w` 选项将捕获的信息重定向到文件中。使用文件的一个原因是为了保存捕获的数据，以便稍后进行检查和分析。这可能包括以其他方式处理数据，可能利用数据构建专用报告等。

要捕获网络流量并将其保存到名为 `traffic-data` 的文件中，请使用以下命令：

```bash
# tcpdump -w traffic-data
tcpdump: listening on eth0
```
