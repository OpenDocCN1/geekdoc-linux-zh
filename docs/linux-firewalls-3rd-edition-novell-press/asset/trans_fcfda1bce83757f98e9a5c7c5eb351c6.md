

## 在实际应用中使用 TCPDump

在本章中，你目前已经看到了一些使用 TCPDump 捕获各种类型流量的示例。这些示例旨在展示 TCPDump 在表达式和其他选项方面的用法。现在，是时候向你展示在实际中使用 TCPDump 捕获特定类型流量的示例了。你可能会在使用这些示例的场景各不相同，但在可能的情况下，我会尝试给出一些线索，说明你可能会使用某个特定示例的原因。在尝试于实际环境中捕获数据时，了解过滤器表达式是如何构建的可能会很有帮助。我之前曾简要涉及过这个话题，但在提供食谱式的解决方案之前，我将向你展示如何构建一个过滤器，其特定目标是捕获 HTTP 会话。

### 构建过滤器以捕获 HTTP 会话

HTTP 是 Web 的语言。通常，HTTP 承载于 TCP 之上，而 TCP 又承载于 IP 之上。我之所以选择 HTTP 作为第一个实际捕获目标，仅仅是因为人们通常熟悉浏览网页，即使他们可能不熟悉底层的协议。

请记住，IP 是一种无连接协议，而 TCP 是一种面向连接的协议。TCP 使用三次握手来开始对话。HTTP 利用了 TCP 的面向连接特性，并且实际上对下层协议（记住 OSI 模型）一无所知。就 HTTP 而言，它将其数据传递给下一层后即完成其任务。因此，当启动 HTTP 会话时，通过 TCPDump 你首先应该看到的是 TCP 的三次握手，随后是协议特定的数据。

在大多数情况下，HTTP 流量流向目标端口 80。

> 各种服务通常运行的端口可以通过检查 /etc/services 文件找到。考虑到这一点，端口号分配的真正来源是 IANA。你可以在 URL [http://www.iana.org/assignments/port-numbers](http://www.iana.org/assignments/port-numbers) 查看最新且最完整的官方端口号分配列表。然而，请记住，没有什么能阻止某人在官方端口号以外的端口上运行服务！

由于 HTTP 通常位于端口 80，因此最好从一个基本的 TCPDump 表达式开始，该表达式仅查找端口 80 的流量，例如：

```
tcpdump 'port 80'
```

运行该命令，然后通过浏览网页生成一些流量，得到以下结果：

```
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 96 bytes

17:15:38.984337 IP client.braingia.org.4485 > test.example.com.www:\
S 523004834:523004834(0) win 5840 \
<mss 1460,sackOK,timestamp 249916003 0,nop,wscale 0>

17:15:38.984650 IP test.example.com.www > client.braingia.org.4485: S \
2810959978:2810959978(0) ack 523004835 win 5792 \
<mss 1460,sackOK,timestamp 1320060704 249916003,nop,wscale 0>

17:15:38.984684 IP client.braingia.org.4485 > test.example.com.www: \
. ack 1 win 5840 <nop,nop,timestamp 249916008 1320060704>

17:15:38.985326 IP client.braingia.org.4485 > test.example.com.www: \
P 1:462(461) ack 1 win 5840 <nop,nop,timestamp 249916008 1320060704>

17:15:39.038067 IP test.example.com.www > client.braingia.org.4485: . \
ack 462 win 6432 <nop,nop,timestamp 1320060710 249916008>

17:15:39.065141 IP test.example.com.www > client.braingia.org.4485: . \
1:1449(1448) ack 462 win 6432 <nop,nop,timestamp 1320060712 249916008>

17:15:39.065183 IP client.braingia.org.4485 > test.example.com.www: . \
ack 1449 win 8688 <nop,nop,timestamp 249916016 1320060712>
```

### 使用 TCPDump 捕获特定协议

> **注意**
>
> 为了提高可读性，我将结果分开了，在本章的其余部分我将继续这样做。

请注意 TCPDump 输出的前两行。在这种情况下，第一行告诉我，为了看到包内的任何有趣内容，我确实应该启用更详细的输出；而第二行则给出了 TCPDump 正在监听的接口状态以及捕获的大小。

下一行是捕获的第一行，也恰好是 TCP 三次握手中发送的第一个数据包（SYN）。你在这行上首先注意到的将是时间戳，随后是协议（IP）。接下来是发起该数据包的计算机的主机名（client.braingia.org）及其流量源端口（4485）。这种源计算机和源端口的组合被称为 Source（源）。大于号（>）显示了相对于该流量 Destination（目标）的方向，从该行可以看出，目标是 test.example.com.www。www 表示流量在目标计算机上定向的目的地端口。

TCPDump 输出行中下一个感兴趣的部分是 Flags（标志）部分，在此情况下由大写字母 S 指示。回想第 1 章“包过滤防火墙的初步概念”中的内容，TCP 头部可以包含各种标志以指示数据包的具体状态。如果你猜到 *S* 表示设置了 **SYN** 标志的数据包，你可能已经赢得了一份有价值的奖品。Flags 部分之后是数据包的 Sequence Number（序列号）空间，指示该数据包内将覆盖的序列号。在这个例子中，Sequence Number 空间（523004834:523004834(0)）的长度为零。此行的下一个项目是窗口大小，如输出中设置的 **win 5840** 所示。最后，方括号内是包含在数据包中的选项。虽然这些选项在某些时候可能很有趣，但在现实世界中，你很少需要太在意它们。

你现在已经通过 TCPDump 看到了 TCP 三次握手中的单个数据包。别担心，确实会有更激动人心的内容，真的会有。捕获中包含的下一行含有从 **test.example.com** 返回的响应数据包。请注意，时间戳增加了，而协议仍然是 IP。然而，现在的源计算机是端口 80 上的 **test.example.com**，目标是 **client.braingia.org:4485**。也要注意，**SYN** 标志已设置，证据是源 > 目标区域后面的 *S*。不过，序列号空间现在不同，（2810959978:2810959978(0)）。这是因为 **test.example.com** 在响应中选择了自己的序列号。真正有趣的第一个区别：因为我们要之前未见过的是 **ack 523004835**。这是 TCP 三次握手的第二部分，即通常被称为 **SYN-ACK** 的数据包。在这个数据包中，最初的目标计算机正在响应或在指定端口上确认发起 TCP 连接的呼叫。请注意，**ack** 后面的数字等于原始序列号（523004834）加一。这就是协议本身在起作用。

捕获中的第三个数据包，再次在此处展示以供参考，是 TCP 连接建立过程中的最后一个数据包：

```
17:15:38.984684  IP client.braingia.org.4485 > test.example.com.www: . 
ack 1  win 5840 <nop,nop,timestamp 249916008 1320060704>
```

在这个数据包中，最初的源确认了连接建立。请注意，在标志通常显示的位置有一个单点（.）。这通常意味着没有设置任何标志；然而，像 **ACK** 这样的某些标志会在输出行的不同位置显示。源侧设置了 **ACK** 标志，并为此连接设置了初始序列号。此时，TCP 连接被认为已建立。这看起来像是一个很大的工作量，但我不是承诺这一节是关于 HTTP 的吗？确实如此。下一个带有捕获输出的数据包表明一个 HTTP 连接正在进展中：

