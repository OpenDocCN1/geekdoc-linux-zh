
对于上述使用 `limit` 匹配的每个 `ACCEPT` 规则，都有相应的 `DROP` 规则。这处理了超过 `limit` 匹配允许的最大10%比例的数据包；一旦数据包水平高于此值，它们将不再匹配 `ACCEPT` 规则，然后与 iptables 策略中的剩余规则进行比较。与其允许以限速速率通过数据包，不如拒绝与攻击者通信这通常更好。

你还可以使用 `limit` 匹配对默认日志规则生成的 iptables 消息设置阈值。然而，除非磁盘空间是一个问题，通常没有必要对 `LOG` 规则应用限制，因为内核在 `LOG` 目标内部使用了一个环形缓冲区，这样当数据包击中 `LOG` 规则的速度快于被写入 syslog 的速度时，日志消息会被覆盖。

头部滥用（Header abuses）是指包含恶意构造、损坏或伪造的传输层头部的数据包。一个典型的例子是伪造的 RST 数据包，旨在切断 TCP 连接。慢速端口扫描（下文将讨论）也属于这一类，尽管扫描本身并不是恶意的。

此类数据包包含了针对终端主机传输协议栈漏洞的利用程序（payload）。专门用于处理传输层信息的内核代码是攻击目标。一个很好的例子（特别是在本书的语境下）是 2004 年公布的针对 Netfilter TCP 选项处理代码漏洞的利用程序（该漏洞已被 Netfilter 项目迅速修复，因此任何最近的内核版本都不再受该漏洞影响）。虽然这并没有利用 TCP 栈本身，但它利用了通过 Netfilter 框架直接挂钩到堆栈上的代码。

## 滥用传输层

由于传输层在某种意义上是协议栈与网络应用程序进行通信之前的网关，因此对于攻击者来说是一个非常丰肥的目标。许多可疑活动涉及传输层信息属于侦察范畴，而不是直接攻击。

## 端口扫描

端口扫描是一种用于询问主机技术，以查看从特定的 IP 地址可以访问哪些 TCP 或 UDP 服务。扫描系统可以是成功攻破目标的重要步骤，因为它为攻击者提供了有关可能被访问和攻击的服务信息。

话虽如此，端口扫描也可以是查看哪些可用服务进行通信的重要步骤；端口扫描本身并不带有恶意。你可以将端口扫描比作某人在敲房子的门。对于任何给定的门门，如果有人说“你好，很高兴见到你”然后离开，并没有造成任何伤害。虽然重复的敲门可能引起疑虑，但在此人尝试进入房屋之前，这并不构成犯罪。尽管如此，如果有人敲了我家里所有的门，我还是想知道这件事，因为这可能意味着有人正在收集有关最佳入入方式的信息。同样，检测端口扫描也是一个好主意（需要进行调优以减少误报），大多数入侵检测系统都提供在系统受到扫描时发送警报的能力。

## 将端口扫描与漏洞服务匹配

端口扫描并不涉及对目标系统上的每个可能的端口进行详尽测试。如果攻击者已经攻破了（例如）OpenSSH 3.3 和 BIND 4.9 服务器，那么发现其余 65,533 个端口也绑定了服务器就没什么意义了。

> ³TCP 和 UDP 头部中的源端口和目的字段宽度为 16 位，因此总共有 65,536 (2¹16) 个端口（包括端口 0，Nmap 可以扫描该端口）。

此外，生成一个产生噪声的扫描器来测试系统上的所有端口是触发 IDS 警报的好方法，因为任何合理的端口扫描都更有可能触发报警。作为攻击者，最好不要引起自己的注意。为了让 IDS 更加难以确定扫描的真实来源，攻击者还可以使用 Nmap 的诱骗 (`-D`) 选项。这允许端口扫描从几个伪造的源地址复制，因此在目标系统看来就像是由几个独立源同时扫描的。目标是让可能正在监控 IDS 警报的安全管理员更难查出扫描的真实来源。

## TCP 端口扫描技术

TCP 端口扫描可以用许多令人惊讶的技术完成。每种技术在穿越网络时在链路上看起来都略有不同，我们在接下来的几节（从“TCP 空闲扫描”开始，到第 59 页的“TCP 空闲扫描”结束）中介绍主要的扫描技术。坦率地说，不均衡的 Nmap 扫描器（参见 http://www.incsecure.org）已经为我们自动化了每种技术，我们在在本章中的所有扫描都使用 Nmap。我们使用默认 iptables 策略的 `iptablesfw` 启动扫描（见图 3-2），并将讨论下列出的 Nmap 端口扫描技术：

- TCP connect() 扫描——(Nmap `-sT`)
- TCP SYN 或半开放扫描——(Nmap `-sS`)
- TCP FIN、XMAS 和 NULL 扫描——(Nmap `-sf`, `-sX`, `-sN`)
- TCP ACK 扫描——(Nmap `-sA`)
- TCP 空闲扫描——(Nmap `-s1`)
- UDP 扫描——(Nmap `-sU`)

在接后的每个示例，都使用了 Nmap `-p0` 命令行选项来强制 Nmap 在发送扫描之前跳过判断 iptables 系统是否运行（即省略主机发现）。从 Nmap 的角度来看，每个扫描的端口可以处于三种状态之一：

| 状态 | 描述 |
| :--- | :--- |
| open | 端口绑定了服务器，且是可以访问的。 |
| closed | 端口没有绑定服务器。 |
| filtered | 端口可能绑定了服务器，但与其通信的尝试被拦截了，Nmap 无法确定端口是开放还是关闭。 |

## TCP connect() 扫描

当普通客户端应用程序尝试与绑定到 TCP 端口的网络服务器进行通信时，本地 TCP 协议栈会代表客户端与远程栈进行交互。在传输任何应用层数据之前，两个堆栈必须协商控制客户端和服务器之间即将发生的对话的参数。这种协商就是标准的 TCP 三次握手。

> ⁴ 尽管 Nmap 可以扫描端口 0，操作系统也不允许服务器绑定() 到端口 0。

这种协商是标准的 TCP 三次握手，如图 3-4 所示。

## TCP SYN 或半开放扫描

SYN 半开放扫描与 connect() 扫描的相似之处在于扫描器向每个端口发送 SYN 包以引发 SYN/ACK 响应。然而，扫描系统从未完成三次握手，如图 3-5 所示。

## 原始套字与未请求的 SYN/ACK

通过 `connect()` 系统调用无法 SYN 扫描，因为那会调用原生 TCP 栈，它会响应 ACK。通常通过使用原始套字来构建数据结构，该结构在操作系统内核放置到链路上时模拟 SYN 包。

使用原始套字向远程系统构建 TCP SYN 包而不是使用 `connect()` 系统调用会带来一个有趣的问题。如果远程端响应 SYN/ACK，那么扫描系统的本地 TCP 协议栈会收到 SYN/ACK，由于发出的 SYN 包并非来自本地栈（因为是由于通过原始套字手动构建的），所以对于扫描器来说，SYN/ACK 并不是合法的 TCP 握手。然而，扫描器的本地栈会向目标系统发送 RST，因为 SYN/ACK 看起来是未请求的。你可以在启动扫描之前通过在 OUTPUT 链中添加以下 iptables 来停止这种行为：

```
[ext_scanner] # iptables -I OUTPUT 1 -d target -p tcp --flags RST RST -DROP
```

Nmap 使用原始套字手动构建 SYN 扫描模式 (`-S`) 中使用的 TCP SYN 包，这是特权用户的默认扫描模式。这些数据包的特征由 Nmap 直接决定（不使用本地 TCP 栈），它们与正常生成的 TCP SYN 包有显著差异。例如，如果我们使用浏览器启动到 http://www.google.com 的网络会话并使用 `tcpdump` 显示来自本地 Linux TCP 栈的 SYN 包，我们将看到以下内容。

```
[iptables]# tcpdump -i eth0 -nn port 80
tcpdump: verbose output suppressed, -or -vv for full protocol decode listening on eth0,
link-type EN10(Ethernet), capture size 96 bytes
11:13:40.251882 IP 71.157.X.X.59603=72.124.39.90 S 244605733:244605733(0)win 5840
mss 1460,sackOK,timestamp 217319569 0,nop,scale 2
```

上述内容在 TCP 头部的窗口大小和选项部分均已被证伪。每个值的特定数值由本地 TCP 栈定义，并用于与远程主机协商有效的 TCP 会话。

与真实 TCP 栈生成的 SYN 包不同，Nmap 并不关心建立真实的 TCP 会话。Nmap 唯一感兴趣的是远程主机上的端口是开放的（Nmap 接收到 SYN/ACK）、关闭的（Nmap 接收到 RST/ACK）还是被过滤的（Nmap 什么未接收到）。因此，Nmap 发到线上的 TCP SYN 包仅是为了将远程主机标记为带有 SYN 标志的 TCP 包，远程 TCP 栈将响应 SYN/ACK、RST/ACK 或不响应（如果端口被过滤）。

对于 3.x 版本的 Nmap，用于扫描远程系统的 SYN 包中不包含任何 TCP 选项，如下。（如果包中包含选项，它们将显示在 TCP 窗口大小之后，如下所示。）

```
11:17:30.313099 IP 71.157.X.X.52831=72.124.39.90 S 200185651:200185651(0) win 302
```

对于较新版本的 Nmap，最大分段大小 (MSS) 值包含在其发送的 SYN 包中，如下所示。

```
15:55:57.521882 IP 71.157.X.X.58302=72.124.39.90 S 197554866:197554866(0) win 2048 <mss 1460>
```

如果我们现在使用 `iptablesfw` 运行 SYN 扫描，我们在 `connect()` 扫描中看到的系统端口被报告为开放，但如你所见，其 TCP 选项少于 `connect()` 扫描。SYN 扫描的选项字符串为 `02400584b50402080a369572200000001030306`

```
[ext_scanner]# nmap -PO -sT 71.157.X.X
Starting Nmap (4.01) (http://www.insecure.org/nmap/) at 2007-07-03 02:27 EDT
Interesting ports on 71.157.X.X:
(扫描了 1670 个端口，但下方未显示状态为: filtered)
PORT STATE
80/tcp open http
443/tcp open https
Nmap finished: 1 IP address (1 host) scanned in 22.334 seconds
```

```
[iptablesfw]# grep SYN /var/log/messages | tail -n 1
Jul 3 02:27:59 iptablesfw grep: DROP IN=eth0 OUT=
MAC=00:13:d3:b8:b6:e4:00:30:48:80:4e:37:08 SRC=144.202.X.X DST=71.157.X.X
LEN=450 TOS=00 PRE=00 TTL=52 ID=21049 PROTO=TCP SPT=43996
WINDOW=1024 RES=00 SYN URG OPT=0 (02040584)
```

传输层攻击与防御 57

## TCP FIN、XMAS 和 NULL 扫描

FIN、XMAS、NULL 扫描的运行原理是：如果 TCP（遵循 RFC）在端口上接收到一个意外的 TCP 包且该包没有设置 SYN、ACK 或 RST 标志，它应该以特定的方式做出响应。如果端口是关闭，TCP 将用 RST/ACK 响应；但如果端口是开放，TCP 则不会响应任何包。

以下示例显示了对 `iptablesfw` 系统的 FIN 扫描，注意 Nmap 将所有端口报告为 `open|filtered`（开放|过滤）。意外的 FIN 包不属于任何合法的 TCP 连接，所有的 FIN 包（即使是发送到开放端口的）都会匹配规则策略中的 `INVALID`（无效）状态，并随后被记录和丢弃。（参见 DROP INVALID 日志 ② 和 ③ 处设置的 FIN 标志。）

```
### [scanner]# nmap -PO -so 71.157.X.X
Starting Nmap 4.01 (http://www.insecure.org/nmap/ ) on 2007-07-03 00:33 EDT
1672 scans on 71.157.X.X are: filtered
Nmap finished: 1 IP address (1 host) scanned in 36.199 seconds
iptablesfw# grep /var/log/messages | tail -n 1
Jul 03 00:34:17 iptablesfw kernel: DROP INVALID IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48 0e:47:38:00 SRC=142.202.X.X DST=71.157.X.X
LEN=400 TOS=00 PREC=000 TTL=54 ID=51322 PROTO=TCP SPT=60097 DPI=1437
WINDOW=3072 RES=000 URG=0
```

## TCP ACK 扫描

TCP ACK 扫描 (`nmap -sa`) 向每个扫描端口发送 TCP ACK 包，寻找 RST 包（开放和关闭端口均无 RST/ACK 包）。如果端口没有返回 RST 包，则 Nmap 推断端口是被过滤的，如下方的 ACK 扫描所示。ACK 扫描的目标不是判断端口是开放还是关闭，而是判断是否被状态防火墙过滤。由于 iptables 防火墙使用连接跟踪系统（状态机），意外的 ACK 包不会进入 `iptablesfw` 的 TCP 栈，因此不会向扫描者返回 RST 包（注意 ② 处的 ACK 标志）。

```
### [scanner]# nmap -PO -so 71.157.X.X
Starting Nmap 4.01 (http://www.insecure.org/nmap/ ) on 2007-07-03 00:33 EDT
1672 scans on 71.157.X.X are: filtered
Nmap finished: 1 IP address (1 host) scanned in 36.199 seconds
iptablesfw# grep /var/log/messages | tail -n 1
Jul 03 10:37:17 iptablesfw kernel: DROP INVALID IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48 0e:47:38:00 SRC=142.202.X.X DST=71.157.X.X
LEN=400 TOS=00 PREC=000 TTL=54 ID=51322 PROTO=TCP SPT=60097 DPI=1437
WINDOW=4096 RES=000 ACK URG=0
```

## TCP 空闲扫描 (Idle Scans)

TCP 空闲扫描是一种高级扫描模式，需要三个系统：一个启动扫描的扫描者、一个目标以及一个未被频繁使用的僵尸主机。图 3-6 展示了空闲扫描。空闲扫描利用了这样一个事实：IP 每通过 IP 栈发送一个包，ID 值就会加 1。扫描结合了 TCP 栈的要求，即对开放端口发送 SYN/ACK 响应，对关闭端口发送 RST 包。此外，所有 TCP 栈都被要求忽略未请求的 RST/ACK 包。这些事实共同允许扫描者观察僵尸主机在扫描者到僵尸的 TCP 会话期间如何增加 IP 值，而扫描者在目标处伪造僵尸主机的 IP 地址发送 SYN 包。扫描者能够监控来自僵尸的包的 IP 头中的 ID 值，并根据这些信息推断目标端口是否开放。

> 在这种情况下，来自僵尸的 RST 包不包含 ACK 标志，因为目标的 SYN/ACK 也没有 ACK 标志。关于 RST 包设置 ACK 标志的更多材料，请见第 63 页的“RST 与 RST/ACK”。

然而，决定空闲扫描成功的最重要的因素是僵尸主机上可用服务的利用率。流行的 Web 服务器不适合作为僵尸主机。在这种情况下，每个 TCP 连接都会增加 ID 值，且该值在很大程度上由扫描者控制。这使得将 IP ID 值的变化映射到扫描端口变得不实际。

空闲扫描的目标系统无法获晓扫描者的真实来源，因为它们看到的都是僵尸主机发送的伪造 SYN 包。目标上的 iptables 日志看起来就像普通的扫描（参见第 56 页的“TCP SYN 或半开放扫描”）。

注意：如果僵尸主机上运行着默认丢弃防火墙，则使其工作的唯一方法是将源硬编码为僵尸主机上的开放 TCP 端口。这是因为被过滤的 SYN/ACK 不会被僵尸 TCP 栈看到，因此它永远不会发送 RST，ID 也就不会增加。在某些情况下，如果部署了防火墙，低利用率的服务可能是唯一的可用端口。

## UDP 扫描

由于 UDP 未实现建立连接的控制消息，UDP 服务的扫描非常简单，实现方法是向 UDP 端口发送数据，然后在合理时间内查看是否有任何返回。因为发送到没有服务器监听的端口的 UDP 包会触发 ICMP 端口不可达消息，扫描者很容易判断 UDP 端口是否关闭。

相比之下，发送到开放端口的 UDP 包即使没有被过滤，也可能完全沉默。这是因为 UDP 服务器没有义务响应包；是否响应完全取决于绑定在该端口的特定应用程序。

如果防火墙拦截了从扫描者到特定端口的 UDP 包，扫描者未接收到内容就像端口上的应用程序没有说什么（这就是为什么被过滤的端口被报告为 `open|filtered`）。例如，下面是对 iptables swift 的 UDP 扫描以及几行 iptables 日志记录。所有扫描的 UDP 端口均为 `open|filtered` 状态（加粗显示），随后是示例的 UDP 端口日志：
