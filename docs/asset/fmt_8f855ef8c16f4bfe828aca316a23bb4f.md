
第一个输出文件将被命名为 `output.pcap.1`，一旦它达到 10 兆，`tcpdump` 就会关闭并开始写入 `output.pcap.2`，依此类推，直到你杀死 `tcpdump` 或磁盘空间不足。如果你想确保不会耗尽磁盘空间，还可以添加 `-W` 选项，它允许限制 `tcpdump` 最终创建的文件数量。当 `tcpdump` 达到最后一个文件时，它将从头开始覆盖集合中的第一个文件。例如，如果你想让 `tcpdump` 在 10 兆后轮换到新文件，并确保 `tcpdump` 只占用 50 兆磁盘空间，你可以将其限制为 5 个轮换文件：

```
sudo tcpdump -C 10 -W 5 -w output.pcap
```

一旦你有了这些数据包捕获，你可以使用 `-r` 选项来重放它们，就像它们是实时发生一样。只需指定你的原始数据包输出文件作为参数即可。你可以像对实时流量流运行 `tcpdump` 一样，指定过滤器和其他如 `-n` 等其他选项：

```
sudo tcpdump -n -r output.pcap
```

`tcpdump` 程序包含了许多我在这里提到的之外的有用选项和过滤器。帮助页面（输入 `man tcpdump`）不仅涵盖了所有这些选项和过滤器，还提供了关于 TCP 数据包构造的良好入门指南，因此如果你想深入了解 `tcpdump` 的功能，它一一阅。

## 使用 Wireshark

虽然 `tcpdump` 是一个方便的捕包工具，但当你实际上需要解析和分析原始数据包时，`-r` 选项有时并不够用。幸运的是，有些工具让这个过程变得简单。原始数据包分析最好的工具之一是 Wireshark。它是一个桌面应用程序，提供了许多数据包分析的复杂工具，这些工具远超本书的范围。但在基础层，Wireshark 为你提供了一种简单得的方法查看原始数据包转储并定位明显的问题。

Wireshark 软件包已为主要的 Linux 发行版打包，并提供了适用于 Windows 和 Mac 机器的客户端。安装后，你可以通过桌面环境启动它，或直接在命令行中输入 `wireshark`。如果你输入 `wireshark` 后跟你的原始数据包文件，它将将其作为启动项打开。

如图 5-2 所示，Wireshark 将其 GUI 分为几个部分。工具栏下方的主面板显示了你可能在 `tcpdump` 输出中找到的基本信息。Wireshark 的有用之处在于它的列更易读，并且根据协议对数据包进行颜色编码，并将用红色突出显示错误包。主面板中的颜色编码使得过滤流量和识别问题变得稍微简单。

一旦你点击主面板中的特定数据包，下面的面板将显示该包的所有详细信息。

![](img/c2fd5da12ee5721b98d44a95ff7b5962_111_0.png)

| No. | Time | Source | Destination | Protocol | Info |
|---|---|---|---|---|---|
| 4 | 2.678649 | 00:00:00.157 | 64.142.56.172 | 192.168.128.12 | TCP | http=34252 [ACK, Seq=1 Ackr=1 Win=75 Len=1496765239 TSB- |
| 5 | 2.742888 | 00:00:00.224 | 64.142.56.172 | 192.168.128.12 | TCP | http=34253 [ACK, Seq=1 Ackr=2 Win=65535 Len=1496765339 TSB- |
| 6 | 2.819527 | 00:00:00.291 | 64.142.56.172 | 192.168.128.12 | TCP | http=34254 [ACK, Seq=1 Ackr=3 Win=65535 Len=1496765439 TSB- |
| 7 | 2.895727 | 00:00:00.358 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query google.com A.ns1-free.com |
| 8 | 2.946397 | 00:00:00.425 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query a1.ns1-free.com |
| 9 | 3.058848 | 00:00:00.492 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query a2.ns1-free.com |
| 10 | 4.056867 | 00:00:00.559 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query Response (Size limited during capture) |
| 11 | 4.134367 | 00:00:00.626 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query Response (Size limited during capture) |
| 12 | 4.259129 | 00:00:00.693 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query Response (Size limited during capture) |
| 13 | 4.336629 | 00:00:00.760 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query Response (Size limited during capture) |
| 14 | 4.459129 | 00:00:00.827 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query Response |
| 15 | 4.519649 | 00:00:00.894 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query Response |
| 16 | 4.644149 | 00:00:00.961 | 64.142.56.172 | 192.168.128.12 | DNS | Standard query Response |

> * Frame 8 (Bytes on wire)

* Ethernet II, Control: 0x00, Destination: 00:00:5e:00:53:01, Source: 00:00:5e:00:53:02, Length: 87

* IP (0x0800)

Version: 4, Header Length: 20 bytes, Total Length: 87, Identification: 55735, Flags: 0, Fragment Offset: 0, TTL: 64, Protocol: 6, Source: 192.168.128.12, Destination: 64.142.56.172

在那个面板中，你可以深入显示 IP 头部、数据包的数据部分以及之间的所有内容。一旦你这样做，点击展开包的特定部分；窗口最底部有一个独立的面板，将向你显示数据的十六进制和 ASCII 表示。

Wireshark 的另一个有用功能是能够从大量数据包中挑选两个主机之间的完整通信流。虽然你完全可以手动这样做，但你也可以选择一个感兴趣的示例包，然后点击 分析（Analyze）→跟踪 TCP 流（Follow TCP Stream）。如果是 UDP 或 SSL 流，相应的选项将会可见。一旦你选择该菜单，就会弹出一个窗口（图 5-3），

### 数据捕获

![](img/c2fd5da12ee5721b98d44a95ff7b5962_113_0.png)

图 5-3：跟随充满博客垃圾邮件的 HTTP 流

如果能够从该流中拼接出任何内容，它将被显示。无论哪情况，当你关闭“跟踪 TCP 流”窗口时，wireshark 窗口会自动过滤掉与此特定流的所有包。

# 第 6 章

## 主机名无法解析？解决 DNS 服务器问题

域名系统（或 DNS）是互联网上最重要的系统之一。互联网上的每个主机都分配有一个 IP 地址，但我们大多数人并没有记住自己喜爱的网站的 IP 地址。相反，我们输入一个主机名，DNS 会在后台将其转换为 IP 地址。你也可以使用 DNS 将 IP 地址转换为主机名。当 DNS 失败时，你得到的效果类似于网络连接失败——你无法访问想要访问的网站或服务器，但与网络连接失败不同的是，你的电脑和服务器仍然在网上。

在 DevOps 组织中，你可能会遇到来自不同职责领域的 DNS 故障排除。在最基础的层，你可能对你的 DNS 系统没有直接控制权；然而，你可能会发现无法再次访问你负责或你开发的服务器，或者你可能会注意到自动化测试在尝试解析服务器名称时发生超时。最终，你团队中的其他人可能必须修复这个问题，但你希望先带着坚实的数据与他们交流。除此之外之外，也许你为某个网站管理 DNS，但这是通过注册商或其他第三方进行的，你只需要在 Web 图形界面中更改记录。现在你更改的某条记录没有更新，你想在向 DNS 提供商提交工单之前对情况进行合理性检查。最后，也许你可能是一个全职的 DNS 管理员，运行着自己的 DNS 服务器，因此当出现 DNS 问题时，责任就由你承担。无论你处于 DevOps 团队的什么种位置，DNS 故障排除技能都是非常有价值的。

尽管理解 DNS 的工作原理确实有助于故障排除，但本章假设你的理解可能有些模糊。这没关系，因为在本章逐步排查 DNS 问题的过程中，我们将追踪请求一直穿过整个堆栈并返回。本章分为两个不同的部分。第一部分介绍了如何从客户端排排除 DNS 问题，第二部分介绍了如何排排除 DNS 服务器问题。客户端故障排除将帮助你完成基础的排排除步骤，以判断问题是在你这边还是在 DNS 服务器端。如果你发现问题在服务器端，服务器故障排除部分将帮助你追溯一些常见的 DNS 服务器问题。

## DNS 客户端故障排除

排排除 DNS 问题的第一个地方是你的本地主机。你会发现，即使问题在 DNS 服务器端，你也可以从任何安装了 `nslookup` 和 `dig` 的客户端追溯许多 DNS 服务器问题的根源。`nslookup` 和 `dig` 工具都可以用于排除 DNS 问题，但对于基础测试，请从 `nslookup` 开始。对于这个排排除步骤，我们将借用第 5 章中的一个场景：客户端的 IP 地址为 10.1.1.7，我们有一个名为 web1 的服务器，其 IP 地址为 10.1.2.5，我们想要解析它。这里是一个成功解析 web1 的 `nslookup` 请求示例：

```
$ nslookup web1
Server: 10.1.1.3
Address: 10.1.1.3#53
Name: web1.example.net
Address: 10.1.2.5
```

在这种情况下，DNS 正常工作。web1 主机扩展为 web1.example.net 并解析到地址 10.1.2.5。当然，要确认的第一件事是这个 IP 是否与 web1 应该拥有的 IP 匹配！如果 web1 有错误的 IP 地址，那么你可以转向本章的 DNS 服务器故障排除部分来找出原因。在这种情况下，DNS 是工作的；然而，DNS 在客户端也有许多可能失败的故障，这些方式提供了不同的线索。

### 未配置名称服务器或名称服务器不可用

如果你看到以下错误，可能意味着你没有为主机配置任何名称服务器，或者它们不可用：

```
$ nslookup web1
;; connection timed out; no servers could be reached
```

无论哪种情况，你都需要检查 `/etc/resolv.conf` 并查看那里是否配置了任何名称服务器。如果你在没有没有看到配置的 IP 地址，你需要在文件中添加一个名称服务器。否则，你可能会看到类似的内容：

```
search example.net
nameserver 10.1.1.3
```

你现在需要开始排排除与名称服务器的连接，从 `ping` 命令开始。如果你无法 `ping` 名称服务器且其 IP 地址在同一个子网内（在这种情况下 10.1.1.3 在我的子网内），那么名称服务器本身可能完全宕机了。确认此点的良好方法是可以通过在命令行中添加其 IP 地址，直接对你配置的名称服务器运行 `nslookup`：

```
$ nslookup web1 10.1.1.3
Server: 10.1.1.3
Address: 10.1.1.3#53
Name: web1.example.net
Address: 10.1.2.5
```

或者，如果你想用 `dig` 代替 `nslookup`，请在名称服务器 IP 前加上 `@`，并确保使用完全限定域名。此外，准备好面对更多的输出：

```
$ dig web1.example.net @10.1.1.3
>> DIG 9.7.0-PI << www.example.net @10.1.1.3
;; global options: +cmd
;; Got answer:
>>Header<< opcode: status: NOERROR, id: 23394
;; flags qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;;web1.example.net.		IN	A

;; ANSWER SECTION:
;;web1.example.net.		IN	A	10.1.2.5

;; AUTHORITY SECTION:
;;example.net.		IN	NS	ns1.example.net.
;;example.net.		IN	NS	ns2.example.net.

;; ADDITIONAL SECTION:
;;ns1.example.net.		IN	A	10.1.1.3
;;ns2.example.net.		IN	A	10.1.1.4
```

## DNS 服务器故障排除

### 理解 dig 输出

虽然 `nslookup` 是 DNS 故障排除非常有用的工具，但在涉及 DNS 服务器时，我更喜欢使用 `dig`。这两个工具在普通的 Linux 系统上都是可用的，但我喜欢用 `dig` 进行 DNS 服务器故障排除，因为它默认提供了许多额外信息。`dig` 的输出是

同时也更接近服务器返回的实际 DNS 响应，这有助于你在此过程中学习更多关于该协议的知识。这里有一个 dig 输出示例：

```
$ dig web1.example.net
;; DIG 9.7.0-P1 << example.net
;; global options: +cmd
;; Got answer:
;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 30750
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

;; QUESTION SECTION:
web1.example.net.		IN	A

;; ANSWER SECTION:
web1.example.net.	300	IN	A	10.1.2.5

;; AUTHORITY SECTION:
example.net.	300	IN	NS	ns2.example.net.
example.net.	300	IN	NS	ns1.example.net.

;; ADDITIONAL SECTION:
s1.example.net.	300	IN	A	10.1.1.3
ns2.example.net.	300	IN	A	10.1.1.4

;; Query time: 2 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: Mon Mar 19 20:48:27 2012
;; MSG SIZE rcvd: 118
```

这些输出很多，但其中包含大量有用信息。首先，让我们来看问题和答案：

```
;; QUESTION SECTION:
web1.example.net.		IN	A
```

```
;; ANSWER SECTION:
web1.example.net.	300	IN	A	10.1.2.5
```

问题部分（QUESTION SECTION）重复了发送的 DNS 查询。在这种情况下，我们请求了 web1.example.net 的 A 记录（将主机名映射到 IP 的传统 DNS 记录）。答案部分（ANSWER SECTION）返回了 web1.example.net 的完整 A 记录，包括其 IP 地址（10.1.2.5）和它的 TTL（生存时间——在我们再次查找之前可以缓存此回复的秒数），在这种情况下 TTL 为 300 秒。

# 第 6 章 为什么域名无法解析？解决 DNS 服务器问题

除了直接查询的答案外，DNS 回复还发送了一些额外信息：

```
;; AUTHORITY SECTION:
example.net      300 IN NS ns2.example.net.
example.net      300 IN NS ns1.example.net.
```

```
;; ADDITIONAL SECTION:
ns2.example.net   300 IN A 10.1.1.4
ns1.example.net   300 IN A 10.1.1.3
```
