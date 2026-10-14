

默认网关是 208.169.244.79，对应于 ppp0 接口。现在你可以安全地使用互联网。

## 使用 ping

你可以使用 ping 来检查你的计算机是否可以到达某个网络。Ping 网络上某台机器的 IP 地址或完整主机名，以确保你可以到达该网络。例如，在你连接到互联网后，使用以下命令来确保你可以到达 freshmeat 网络：

```bash
bash$ ping www.freshmeat.net
PING freshmeat.net (209.207.224.211): 56 data bytes
64 bytes from 209.207.224.211: icmp_seq=0 ttl=243 time=1060.2 ms
64 bytes from 209.207.224.211: icmp_seq=1 ttl=243 time=1147.5 ms
64 bytes from 209.207.224.211: icmp_seq=2 ttl=243 time=927.5 ms
^C
--- freshmeat.net ping statistics ---
4 packets transmitted, 3 packets received, 25% packet loss
round-trip min/avg/max = 927.5/1045.0/1147.5 ms
```

在你发出 ping 命令后，它会一直运行直到你按下 Ctrl+C 组合键。Ctrl+C 组合键会终止 ping 命令并写入 ping 统计信息。

你想要 ping 的第一个 IP 是你的 ISP IP。如果你可以 ping 到你的 ISP，就说明你可以到达 ISP 网络。其次，尝试 ping www.cnn.com、www.freshmeat.net 等地址。如果出现错误，尝试 ping 你知道的 IP，因为问题可能是名称解析而不是无法到达网络。结果可能是以下几种情况之一：

- 你可以使用 IP 地址和主机名访问网络 — 你拥有完全配置且正常工作的连接。
- 你可以使用 IP 地址访问网络，但不能使用主机名 — 你在设置 DNS 时存在问题。检查你所做的 DNS 设置。
- 你可以使用 IP 地址或主机名访问网络但可以 ping 到你的 ISP — 你存在路由问题。请参考上一节“使用 route”。

## 通用调制解调器连接故障排除

*我没有 ttySx 的读写权限。*

这是一个常见错误。SuSE 通过将用户的组更改为 dialout 或 uucp 来解决此错误。使用 YaST 将你的用户名添加到允许使用调制解调器的用户中。有关更多信息，请参阅第 4 章“管理用户和组”。

或者，你可以给用户对特定 ttySx 的读写权限 — 例如：

```bash
chmod +rw /dev/ttySx
```

### CAUTION

如果系统有多个用户，这可能会导致安全漏洞。将用户的组更改为 dialout 或 uucp 是更明智的解决方案。

*我没有执行 pppd 的权限。*

同样，这也是一个常见问题。如同前一个问题一样，将用户的组更改为 dialout 或 uucp。使用 YaST 将你的用户名添加到允许使用调制解调器的用户中。有关更多信息，请参阅第 4 章。

或者，同样地，你可以给用户 pppd 的读/执行权限：

```bash
chmod +rs /usr/sbin/pppd
```

### CAUTION

同样，如果系统有多个用户，这可能会导致安全漏洞。将用户的组更改为 dialout 或 uucp 是更明智的解决方案。

*连接很慢。*

你在串行文件中为 UART 指定的速度可能太低。尝试将其提高。

此外，问题可能是 IRQ 设置不正确；请阅读本章前面“配置串行端口”部分。

另一个问题可能是你的最大接收单元 MRU 和最大传输单元 MTU 设置不正确。较慢的速度需要较低的 MRU/MTU；较高的速度需要较高的 MRU/MTU。指定通过链路传输的数据包。慢速或嘈杂的链路应具有较小的 MRU/MTU，这在数据包传输时发生错误的情况下成本较低。在噪声不是问题且错误很少的高速链路上，你应使用较高的 MRU/MTU 值。

*我在运行串行脚本时系统锁定。*

你可能正在使用 IBM 8514 视频适配器或兼容设备。你应阅读本章前面“自动方法”部分以获取更多信息。如果下次启动系统时系统锁定，你应从 SuSE CD 启动并启动紧急系统。然后，你应挂载 Linux 分区并编辑串行脚本。

*当我开始访问调制解调器时，系统变得非常慢或锁定。*

你可能已将主板资源 IRQ 分配给串行端口。你不应将以下任何 IRQ 分配给串行端口：1、6、8、13 和 14。

你可以使用以下迷你参考来了解调制解调器 AT 命令。表 23.5 中的命令被大多数调制解调器所理解。

**Table 23.5 Modem AT Command Mini-Reference**

| Command | Meaning |
|---|---|
| ATZ | Reset modem |
| ATD# | Dial the number |
| ATDT# | Dial the number using tone dial |
| ATDP# | Dial the number using pulse dial |
| ATX3 | Don't wait for dial tone |
| ATM0 | Speaker off |
| ATL1-ATL3 | Speaker volume level 1-3 |
| ATDL | Re-dial last number |
| ATD,# | Dial number but pause seconds |
| ATH | Hang up modem |
| ATA | Answer mode |
| AT/ | Repeat last command |

完整的参考集通常随调制解调器手册一起提供。

## 使用 ISDN 进行连接

ISDN（综合业务数字网）在我们当前时代被认为是一项突破。它比普通模拟电话线具有很大的优势。使用普通电话线的相同线路，你可以升级到 ISDN。我们不会深入 ISDN 的技术细节，但我们将列出 ISDN 的优缺点。

### ISDN 的优点

使用 ISDN 的优点如下：

- 基本 ISDN（BRI）一次支持多达两个操作。例如，你可以通过同一线路同时连接到互联网、使用电话并发送传真。高级线路（PRI）一次支持多达 23 个操作。
- 由于每个 B 通道可以达到 64Kbps 的速度，当使用基本 BRI 设置时捆绑两个 B 通道，你可以达到最高 128Kbps。当使用 PRI 时，你可以达到最高 23×64 Kbps。
- 拨号速度非常快 — 2 秒，而普通电话线为 40 到 60 秒。这给了你按需拨号的选项，这将在本章后面的“按需拨号”部分讨论。

### ISDN 的缺点

使用 ISDN 的缺点如下：

- 你的电话公司和 ISP 必须支持它。
- 它比普通电话线更昂贵。
- 如果你的电话线路很旧，你可能需要更换电话线路的布线。

## 按需拨号

按需拨号是 ISDN 的一个有趣功能。此功能利用了 ISDN 的快速拨号速度。考虑以下场景：

1. 你启动 Netscape，它会自动打开你的起始页面。
2. 自动建立到 Netscape 服务器的连接。
3. 在指定时间后，如果没有应用程序需要连接，它将被终止。

正如你可能注意到的，这种方法将节省你大量的在线时间。这意味着你只有在需要连接时才在线；否则，你实际上是离线的。此功能不能应用于使用普通调制解调器时，因为拨号和登录所需的最小时间至少为 50 秒，而在 ISDN 中为 2-3 秒。

## ISDN 控制器/卡

ISDN 卡有两种类型：主动式和被动式。

主动卡自行处理 ISDN 连接协议，而被动卡则依赖软件功能来完成此操作。

## ISDN 与法律问题

必须了解，对于任何 ISDN 连接要合法建立，必须有硬件-软件认证。硬件必须运行制造商提供的认证软件。大多数主动卡使用随内核提供的 HiSax 驱动程序，该驱动程序已获得大多数制造商的认证。这意味着如果你运行使用 HiSax 驱动程序的主动卡，你是安全的。在编译内核时，你应下载完整的内核源代码。如果你修补内核，你的 HiSax 驱动程序将失去认证。

## ISDN 与 Linux

随 Linux 提供的 ISDN 包是在德国开发的。因此，该包的大部分文档是用德语编写的，并且该包中德国国家 ISDN 支持较为先进。需要注意的是，只有传统的德国 ISDN 和 Euro-ISDN 得到 Linux 支持。

