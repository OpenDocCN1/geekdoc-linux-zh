

例如，`ether[0] & 1 != 0` 可以捕获所有组播流量。表达式 `ip[0] & 0xf != 5` 可以捕获所有带有选项的 IP 数据包。表达式 `ip[6:2] & 0x1fff = 0` 仅捕获未分片的数据报以及分片数据报的第一个分片（frag zero）。此检查会隐式应用于 tcp 和 udp 索引操作。例如，`tcp[0]` 始终表示 TCP 头部的第一个字节，而不表示中间分片的第一个字节。

某些偏移量和字段值可以表示为名称而不是数值。

可用的协议头部字段偏移量如下：`icmptype`（ICMP 类型字段）、`icmpcode`（ICMP 代码字段）和 `tcpflags`（TCP 标志字段）。

可用的 ICMP 类型字段值如下：`icmp-echoreply`、`icmp-unreach`、`icmp-sourcequench`、`icmp-redirect`、`icmp-echo`、`icmp-routeradvert`、`icmp-routersolicit`、`icmp-timexeed`、`icmp-paramprob`、`icmp-tstamp`、`icmp-tstampreply`、`icmp-ireq`、`icmp-ireqreply`、`icmp-maskreq`、`icmp-maskreply`。

可用的 TCP 标志字段值如下：`tcp-fin`、`tcp-syn`、`tcp-rst`、`tcp-push`、`tcp-ack`、`tcp-urg`。

原始表达式可以使用以下方式组合：

-   括号包裹的原始表达式和操作符组（括号对 Shell 具有特殊含义，因此必须转义）。
-   否定（'!' 或 'not'）。
-   连接（'&&' 或 'and'）。
-   交替（'||' 或 'or'）。

否定的优先级最高。交替和连接的优先级相同，并遵循从左到右的结合律。请注意，连接现在需要显式的 and 令牌，而不是并置（juxtaposition）。

如果给出的标识符没有关键字，则假定使用最近的关键字。例如，

```
not host vs and ace
```

是以下写法的简写：

```
not host vs and host ace
```

这不应与以下写法混淆：

```
not ( host vs or ace )
```

表达式参数可以作为单个参数或多个参数传递给 tcpdump，以哪种更方便为准。通常，如果表达式包含 Shell 元字符，将其作为单个带引号的参数传递会更方便。多个参数在解析前会用空格连接。

## 示例

要打印到达或离开 *sundown* 的所有数据包：

```
tcpdump host sundown
```

要打印 *helios* 与 *hot* 或 *ace* 之间流量：

```
tcpdump host helios and \\( hot or ace \\)
```

要打印 *ace* 与除 *helios* 之外的任何主机之间的所有 IP 数据包：

```
tcpdump ip host ace and not helios
```

要打印本地主机与伯克利主机之间的所有流量：

```
tcpdump net ucb-ether
```

要打印通过互联网网关 *snup* 的所有 ftp 流量；（注意表达式加了引号，以防止 shell 错误解释括号）：

```
tcpdump 'gateway snup and (port ftp or ftp-data)'
```

要打印既非源自也非发往本地主机的流量（如果你网关到另一个网络，这些流量绝不应该出现在你的本地网络上）。

```
tcpdump ip and not net localnet
```

要打印涉及非本地主机的每个 TCP 会话的开始和结束数据包（SYN 和 FIN 数据包）。

```
tcpdump 'tcp[tcpflags] & (tcp-syn|tcp-fin) != 0 and not src and dst net localnet'
```

要打印通过网关 *snup* 发送的长度超过 576 字节的 IP 数据包：

```
tcpdump 'gateway snup and ip[2:2] > 576'
```

要打印*未*通过以太网广播或组播发送的 IP 广播或组播数据包：

```
tcpdump 'ether[0] & 1 = 0 and ip[16] >= 224'
```

要打印所有不是回显请求/回复的 ICMP 数据包（即不是 ping 数据包）：

```
tcpdump 'icmp[icmpTYPE] != icmp-echo and icmp[icmpTYPE] != icmp-echoreply'
```

## 输出格式

*tcpdump* 的输出取决于协议。以下简要描述并给出了大多数格式的示例。

### 链路层头部

如果指定了 '-c' 选项，则打印出链路层头部。在以太网上，打印源和目标地址、协议和数据包长度。

在 FDDI 网络上，'-c' 选项使 *tcpdump* 打印 'frame control'（帧控制）字段、源和目标地址以及数据包长度。（'frame control' 字段决定了其余数据包的解析方式。正常数据包（例如包含 IP 数据报的数据包）是 'async'（异步）数据包，优先级值在 0 到 7 之间；例如，`asyn64`。假定此类数据包包含一个 802.2 逻辑链路控制（LLC）数据包；如果它*不是* ISO 数据报或所谓的 SNAP 数据包，则打印 LLC 头部。）

在令牌环网络上，`-c` 选项使 `tcpdump` 打印 `access control`（访问控制）和 `frame control`（帧控制）字段、源和目标地址以及数据包长度。与 FDDI 网络一样，假定数据包包含一个 LLC 数据包。无论是否指定 `-c` 选项，都会打印源路由数据包的源路由信息。

> （注意：以下描述假定熟悉 *RFC-1144* 中描述的 SLIP 压缩算法）

在 SLIP 链路上，打印方向指示器（"I" 表示入站，"O" 表示出站）、数据包类型和压缩信息。首先打印数据包类型。三种类型为 `ip`、`utcp` 和 `ctcp`。对于 `ip` 数据包，不打印其他链路信息。对于 TCP 数据包，在类型之后打印连接标识符。如果数据包被压缩，则打印其编码头部。特殊情况打印为 `*S+n` 和 `*SA+n`，其中 `n` 是序列号（或序列号和确认号）的增量。如果不是特殊情况，则打印零个或多个变更。变更由 U（紧急指针）、W（窗口）、A（确认）、S（序列 ID）和 I（数据包 ID）表示，后跟增量（+n 或 -n）或新值（=n）。最后，打印数据包中的数据量和压缩头部长度。

例如，以下行显示一个出站的压缩 TCP 数据包，带有隐式连接标识符；确认号增加了 6，序列号增加了 49，数据包 ID 增加了 6；有 3 字节的数据和 6 字节的压缩头部：

```
O ctcp * A+6 S+49 I+6 3 (6)
```

### ARP/RARP 数据包

Arp/rarp 输出显示请求的类型及其参数。该格式旨在自解释。以下是从主机 `rtsg` 到主机 `csam` 的 `rlogin` 开始部分的一个简短样本：

```
arp who-has csam tell rtsg
arp reply csam is-at CSAM
```

第一行表示 `rtsg` 发送了一个 arp 数据包，询问互联网主机 `csam` 的以太网地址。`Csam` 回复其以太网地址（在此示例中，以太网地址大写，互联网地址小写）。

如果我们使用了 `tcpdump -n`，这会看起来不那么冗余：

```
arp who-has 128.3.254.6 tell 128.3.254.68
arp reply 128.3.254.6 is-at 02:07:01:00:01:c4
```

如果我们使用了 `tcpdump -e`，第一个数据包是广播而第二个是点对点的事实就会显现出来：

```
RTSG Broadcast 0806 64: arp who-has csam tell rtsg
CSAM RTSG 0806 64: arp reply csam is-at CSAM
```

对于第一个数据包，这表示以太网源地址是 RTSG，目标是以太网广播地址，类型字段包含十六进制 0806（类型 ETHER_ARP），总长度为 64 字节。

### TCP 数据包

> （注意：以下描述假定熟悉 RFC-793 中描述的 TCP 协议。如果你不熟悉该协议，那么此描述和 *tcpdump* 对你都没太大用处。）

tcp 协议行的一般格式为：

```
`src > dst: flags data-seqno ack window urgent options`
```

*Src* 和 *dst* 是源和目标 IP 地址和端口。*Flags* 是 S (SYN)、F (FIN)、P (PUSH) 或 R (RST) 的某种组合，或者是单个 '.'（无标志）。*Data-seqno* 描述此数据包中数据覆盖的序列空间部分（参见下文示例）。*Ack* 是此连接上反向方向期望的下一个数据序列号。*Window* 是此连接上反向方向可用的接收缓冲区空间数量。*Urg* 表示数据包中有 'urgent'（紧急）数据。*Options* 是尖括号内的 tcp 选项（例如，`<mss 1024>`）。

*Src*、*dst* 和 *flags* 始终存在。其他字段取决于数据包 tcp 协议头部的内容，并且仅在适当时输出。

以下是从主机 *rmsg* 到主机 *csam* 的 *rlogin* 的开头部分。

```
rtsq:1023 > csam.login: S 768512:768512(0) win 4096 <mss 1024>
csam.login > rtsq:1023: S 947648:947648(0) ack 768513 win 4096 <mss 1024>
rtsq:1023 > csam.login: . ack 1 win 4096
csam.login > rtsq:1023: P 1:2(1) ack 1 win 4096
csam.login > rtsq:1023: . ack 2 win 4096
rmsg:1023 > csam.login: P 2:21(19) ack 1 win 4096
csam.login > rmsg:1023: P 1:2(1) ack 21 win 4077
csam.login > rmsg:1023: P 2:3(1) ack 21 win 4077 urg 1
csam.login > rmsg:1023: P 3:4(1) ack 21 win 4077 urg 1
```

第一行表示 rtsq 上的 tcp 端口 1023 向 csam 上的 *login* 端口发送了一个数据包。S 表示设置了 *SYN* 标志。数据包序列号为 768512，且没有包含数据。（注释是 'first:last(nbytes)'，意思是 '序列号从 *first* 开始直到但不包括 *last*，这是 *nbytes* 字节的用户数据。'）。没有搭载的确认（ack），可用的接收窗口为 4096 字节，并且有一个最大段大小选项请求 mss 为 1024 字节。

Csam 回复了一个类似的数据包，但其中包含了对 rtsq 的 SYN 的搭载确认。然后 Rtsq 确认 csam 的 SYN。'.' 表示没有设置标志。数据包中没有数据，因此没有数据序列号。注意，确认序列号是一个小整数（1）。*tcpdump* 第一次看到一个 tcp '会话' 时，

