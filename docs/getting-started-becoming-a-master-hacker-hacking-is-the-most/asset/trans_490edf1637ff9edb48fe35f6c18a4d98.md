
最后，为了仅筛选浏览器 Cookie，我们可以创建以下过滤器。

```
kali > tcpdump -vvAls | grep 'Set-Cookie|Host|Cookie:'
```

tcpdump 是一个功能强大的命令行工具，用于分析具有多种能力的网络流量。投入时间学习其基于 BPF 的过滤系统是非常值得的。作为安全管理员或黑客，你可能无法在远程系统上访问图形用户界面（GUI），而 tcpdump 则是首选工具。

### Wireshark，嗅探器的黄金标准

近年来，Wireshark 已成为事实上的嗅探器标准。它以前被称为 Ethereal，现在是每个网络或安全管理员工具箱中的一部分，或者说应该是。Kali 内置了 Wireshark，因此只需在终端中输入 Wireshark 或使用图形用户界面即可启动 Wireshark；前往“应用程序 --> 常用应用程序 --> 互联网 --> Wireshark”。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_370_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_370_1.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_372_0.png)

**学习**

**用户指南** · **维基** · **问答** · **邮件列表**

你正在运行 Wireshark 2.6.3 (v2.6.3-0-ga62e6c27)。你会收到自动更新。

Wireshark 现在会打开并询问你要监听的接口。如果你使用的是虚拟机，请选择 **eth0**。如果你使用的是带有无线网卡的物理机，请选择无线网卡（通常是 wlan0）。通常，你可以通过活动级别来确定选择哪个适配器。活动最频繁的适配器很可能就是你要用于嗅探的适配器。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_373_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_374_0.png)

现在，Wireshark 开始从你的网络接口捕获数据包，并将它们打包成 .pcap 格式。Pcap 是数据包捕获的标准文件格式（你在行业中诸如 Snort、aircrack-ng 等众多产品中都看到过它的使用）。你在 Wireshark 中看到三个独立分析窗口。顶部窗口，在下方的截图中标记为 #1，被称为**数据包列表窗格（Packet List Pane）**。你应该会看到带有颜色编码的数据包实时通过该窗口移动。

中间窗口，标记为 #2，被称为**数据包详情窗格（Packet Details Pane）**。此窗格提供窗口 #1 中选中报文的头部信息。

最后，窗口 #3，数据包字节窗格（Packet Bytes Pane），提供负载信息，左侧为十六进制格式，右侧为 ASCII 格式。

### 在 Wireshark 中创建过滤器

一般来说，这里的信息太多了，无法进行有效的分析。数据包以每分钟数百或数千个的速度飞过。为了有效使用 Wireshark，我们需要过滤流量，以查看感兴趣的数据包。Wireshark 具有一种简单的过滤语言，为了在任何调查或分析中有效且高效地使用该语言，你需要理解它。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_375_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_376_0.png)

飞过我们接口的数据包涉及许多不同的协议。我们想要应用的第一种过滤器很可能是协议过滤器。记住，TCP/IP 是一组协议，我们可能希望将分析重点集中在少数几种协议上。

在过滤窗口中，输入 "tcp"。你会注意到它变成绿色，表明你的语法是正确的（如果语法不正确，它会保持粉红色）。现在，点击过滤窗口最右侧的箭头按钮以应用过滤器。

这样做时，Wireshark 过滤掉所有流量，除了 TCP 流量。你几乎可以对任何协议执行相同的操作，例如“http”、“smtp”、“udp”、“dns”以及许多其他。尝试一些并查看有哪些类型的流量正在通过你的接口。

如果我们只想看来自特定 IP 地址的流量，我们可以创建一个仅显示来自该地址或发往该地址的流量的过滤器。我们可以通过在过滤窗口中输入：`ip.addr==<IP address>` 来实现。请注意 Wireshark 过滤语法中的双等号（==）（类似于 C 语言中的赋值运算符）。单个 “=” 在此语法中**不生效**。

在我这里的例子中，我想查看来自或发往 IP 地址 192.168.1.107 的流量，所以我创建了如下过滤器：`ip.addr == 192.168.1.107`。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_377_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_378_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_378_1.png)

现在，你只看到来自或发往该 IP 地址的流量。现在我的分析和关注范围缩小到一个感兴趣的 IP 地址。

我们还可以按端口过滤流量。如果我只想查看发往端口 80 的 TCP 流量，我可以创建如下过滤器；`tcp.dstport==80`

请注意，此过滤器指定了协议 (tcp)、方向 (dst) 和端口 (80)。

在创建过滤器时，我们最常使用 “==” 作为过滤器中的运算符（还有其他，见下文）。

只要我们是在查找协议中的许多头部字段之一，这种语法就工作得很好。如果我们是在查找负载中的字符串，我们必须使用 "contains" 运算符。因此，如果我正在查找包含单词 “Facebook” 的数据包，我们可以创建如下过滤器。

```
tcp contains facebook
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_379_0.png)

### WireShark - 显示过滤器表达式

| 字段名称 | 关系 | 值 |
| :--- | :--- | :--- |
| 104apci - IEC 60870-5-104-Apci | 存在 (is present) | 预定义值 |
| 104asdu - IEC 60870-5-104-Asdu | == | 范围 (offset/length) |
| 29west - 29West Protocol | != | 搜索: |
| 24parityfec - Pro-MPEGi Code of Practice #3 release 2 FEC Protocol | <= | 无显示过滤器 |
| 3COMXNS - 3Com XNS Encapsulation | > | 行: |
| 3GPP2 A11 - 3GPP2 A11 | >= | 确定 |
| 6LoWPAN - IPv6 over Low power Wireless Personal Area Networks | < | 取消 |
| 802.11 Radio - 802.11 radio information | contains | 帮助 |
| 802.11 Radiotap - IEEE 802.11 Radiotap Capture header | matches | 配置: Default |
| 802.11 RSNA EAPOL - IEEE 802.11 RSNA EAPOL key | in | |
| 802.3 Slow protocols - Slow Protocols | | |
| GP - Plan 9 | | |
| A21 - A21 Protocol | | |
| AAF - AVTP Audio Format | | |
| AALL1 - ATM AALL1 | | |
| AALL3/4 - ATM AALL3/4 | | |
| AARP - AppleTalk Address Resolution Protocol | | |
| AA5P - Aastra Signalling Protocol | | |
| A-bis OML - GSM A-bis OML | | |
| ACAP - Application Configuration Access Protocol | | |
| ACN - Architecture for Control Networks | | |
| ACP133 - ACP133 Attribute Syntaxes | | |
| ACR 122 - Advanced Card Systems ACR122 | | |
| ACSE - ISO 8650-1 OSI Association Control Service | | |

如上所示，它仅在负载中找到了两个包含单词 Facebook 的数据包，我们可以在 #3 窗格的 ASCII 显示中看到单词 Facebook。

### 使用表达式窗口创建过滤器

如果我们不确定要过滤的字段或如何创建必要的过滤器，我们可以点击最右侧的 Expression 选项卡。这打开了下方的表达式窗口。

此窗口左侧列出了可供我们创建过滤器的长列表字段。这些是数百种协议及这些协议的字段。你可以展开协议并找到其所有字段并选择感兴趣的字段。

右上角的窗口包含**关系（Relation）**选项。这些包括：

- `==` : 等于 (Equal To)
- `!=` : 不等于 (Not Equal To)
- `>` : 大于 (Greater Than)
- `<` : 小于 (Less Than)
- `>=` : 大于或等于 (Greater than or Equal To)
- `<=` : 小于或等于 (Less Than or Equal To)
- `contains` : 协议或字段包含某个值 (Protocol or Field Contains a Value)
- `matches` : 协议或文本字段匹配正则表达式 (Protocol or Text Field Matches a Regular Expression)
- `in` : 在...中 (in)

现在我们可以通过简单地在左窗口选择一个字段；在右上窗口选择一个关系；并在右下窗口选择一个值（值经常是 1 或 0，表示存在或不存在）来创建过滤器。例如，如果我们想找到所有设置了 RST 标志的 tcp 数据包，我们将输入：`tcp.flags.rst==1`

### 跟踪流

在某些情况下，而不是检查特定协议的所有数据包或发往特定端口或 IP 的流量，你想要跟踪通信流。Wireshark 让你能够轻松做到这一点。

如果你试图跟踪例如一个流氓、心怀不满的员工试图对你的网络造成破坏的对话，这种技术可能很有用。

要跟踪一个流，通过点击数据包来选择它，然后右键点击。

