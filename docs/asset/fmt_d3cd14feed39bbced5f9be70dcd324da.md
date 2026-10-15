
```
:: By Iman Karim (fimap.dev@gmail.com)

Requesting list of plugins...

######################################

#LIST OF TRUSTED PLUGINS

######################################

#[1] Weevils injector by Darren "Infmbox" Martyn <infodex@security.net> - Version 2 not installed.

#[2] Do HTTP reverse shell by Darren "Infmbox" Martyn <infodex@security.net> - At version 1 not installed.

#[q] Cancel and Quit.

######################################

Choose a plugin to install:
```

要使用`Fimap`，你首先需要确定目标。

## 第 6 章

### 拒绝服务 (DoS)

拒绝服务（DoS）攻击的目标是使机器或网络资源对预期用户不可用。这通过通过流量淹没目标或利用导致服务崩溃的漏洞来实现。

Kali Linux 包含了在前章节中涵盖的多个漏洞利用工具，可以用于应用层 DoS 攻击，例如 Metasploit。此外，第 3 章涵盖了流行的协议 DoS 工具 Scapy。以下是 Kali Linux 中其他可执行 DoS 攻击的工具：

- 流量攻击（Volume Attacks）：涉及 UDP 洪水、ICMP 洪水以及其他基于伪造数据包的洪水。其目的是饱和受害者的带宽。
- 协议攻击（Protocol Attacks）：消耗服务器或中间设备（如路由器、防火墙、负载均衡器）的资源。例如 SYN 洪水、死亡之 Ping、Smurf攻击、Teardrop。
- 应用层攻击（Application Layer Attacks）：利用合法流量使 Web 服务崩溃。它包括零日攻击、漏洞利用等。
- 会话耗尽（Session Exhaustion）：通过反复建立但不关闭会话来滥用会话限制，旨在消耗资源。DoS 与分布式拒绝服务（DDoS）的区别在于，DoS 攻击涉及一台机器，而 DDoS 攻击涉及许多机器。

### Web 攻击

#### THC-SSL-DOS

安全套层（SSL）协议用于加密互联网上的连接和交易。建立一个安全的 SSL 连接时，服务器所需的处理能力是客户端的 15 倍。THC-SSL-DOS 通过过载服务器使其无法为合法用户提供任何服务，从而利用了这种不对对称性。该攻击利用 SSL 安全重协商功能，通过单个 TCP 连接触发成千上万次重协商。这被称为 SSL 资源耗尽攻击。这种方法的优势在于客户端端 SSL 握手的处理能力远高于服务器，这意味着一台通过普通网络连接的普通电脑就可以挑战 Web 应用程序服务器。这是一个已知的漏洞，在本文编写时，尚无真正的解决方案可以修复它。

要访问 THC-SSL-DOS，请导航至 `Stress Testing | Web Stress Testing | thc-ssdos`。这将打开一个带有 THC-SSL-DOS 主页的终端窗口。要对目标运行 THC-SSL-DOS，请输入：

`thc-ssl-dos [options] <ip of the victim> <port> and --accept`

你必须包含 `--accept`，否则将收到以下错误消息：

```
ERROR: 请通过使用 '--accept' 选项同意该 IP 是合法目标，并且你已完全授权对该目标执行测试。
root@kali:~
```

一旦执行了 THC-SSL-DOS，你将看到一些有趣的文字，说明它正在启动以及正在利用握手过程。在截图中，我们将展示一个没有利用 SSL 的网站；因此显示了连接错误。第二张截图显示了成功的握手，这最终会导致目标瘫痪。请记住，你应该只对你拥有测试权限的 IP 和网站尝试这样做。这些攻击可能会严重损害网站或网络应用程序：

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_254_0.png)

```
等待脚本小子们来生气...
原力与读源码的人同在
Handshakes 0 [0.00 h/s], 1 Conn, 0 Err
Handshakes 0 [0.00 h/s], 3 Conn, 0 Err
SSL: error:14070ffc:SSL routine:ss23:GET_SERVER:unknown protocol
#10: 这看起来不像 SSL!
```

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_254_1.png)

#### Scapy

最流行的 DoS 工具之一是 Scapy。Scapy 是一个由 Philippe Biondi 用 Python 编写计算机网络包处理工具。Scapy 可以伪造或解码数据包、将其发送到网络、捕获它们并匹配请求和响应。此外，它还可以处理扫描、路由追踪、探测、单元测试、攻击和网络发现等任务。

一个常用的技巧是从 Kali 操纵 TCP 包并通过 Scapy 发送。要启动 Scapy，在终端中输入 `scapy`。一旦 Scapy 启动，输入命令语法：

```
root@kali:~# scapy

INFO: Can't import python pyplot wrapper . Won't be able to plot.

WARNING: No route found for IPv6 destination :: (no default route?)

Welcome to Scapy (2.2.8)

>>
```

在接下来的图中，我们将使用 Scapy 向我们的测试服务器发送畸构造的 TCP 包。在这种情况下，我们的测试服务器是 10.0.0.1。这可能是一个路由器或 Web 服务器。此外，我们还将指定要发送到目标地的数据包数量。在这种情况下，我们使用以下命令发送 2000 个包：

`send(IP(dst="10.0.0.1",ttl=0)/TCP(iface="eth0",count=2000))`

在上一行代码中，我们正从 Kali 服务器的 `eth0` 接口向目标地址 10.0.0.1 发送 2000 个包。此外，我们将目标的 TTL 存值设置为 0。从 TCP 的角度来看，这几乎是不可能的。本质上，我们正试图通过一个错误的 TTL 值来混淆 Web 服务器。需要注意的是，在适当的情况下，系统可能会因为单个错误或畸形的数据包而损坏。我们可以根据攻击需要调整计数计数器或其他参数：

```
root@kali:~# scapy

INFO: Can't import python pyplot wrapper . Won't be able to plot.

WARNING: No route found for IPv6 destination :: (no default route?)

Welcome to Scapy (2.2.0)

>>> send(IP(dst="10.0.0.1",ttl=0)/TCP(iface="eth0",count=2000))
```
