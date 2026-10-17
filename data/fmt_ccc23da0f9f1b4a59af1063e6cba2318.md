
$ hostname

nkudos

有关如何更改提示符的信息请参见第 303 页。

## finger: 显示远程用户信息

`finger` 实用程序显示系统上一个或多个用户的信息。该实用程序设计用于本地使用，但当网络流行时，显而易见 `finger` 应该增强以远程访问并收集信息。在以下示例中，`finger` 显示了名为 `bravo` 的系统上所有登录用户的信息：

```bash
[kudos]$ finger @bravo
bravo.example.com
Login Name Tty Idle Time Office Office Phone
sam Sam The Great *1 1:35 Oct 22 5:00
alex Alex Watson 4 Oct 22 12:23 (:kudos)
alex Alex Watson 5 19 Oct 22 12:23 (:0)
jenny Jenny Chen 7 2:24 Oct 22 8:45 (:0)
hls Helen Simpson 11d Oct 20 12:23 (:0)
```

在 `@` 符号之前的用户名会让 `finger` 仅显示指定用户的远程系统信息。如果远程系统对该名称有多个匹配，`finger` 将显示所有匹配项的结果：

```bash
[kudos]$ finger alex@bravo
bravo.example.com
Login Name Tty Idle Time Office Office Phone
alex Alex Watson 4 Oct 22 12:23 (:kudos)
alex Alex Watson 5 19 Oct 22 12:23 (:0)
```

`finger` 实用程序通过查询标准网络服务 `in.finger` 守护进程工作。尽管 Ubuntu Linux 的 `finger` 软件包中提供了此服务，但某些站点选择不运行它，以减少系统负载、降低安全风险或维护隐私。当您使用 `finger` 获取某站点某人的信息时，您将看到错误或什么也看不到。远程 `in.finger` 守护进程决定共享多少信息以及格式。因此，对于任何给定系统显示的报告可能与前面的示例不同。

### in.finger 守护进程

`finger` 守护进程 (`in.finger`) 会泄露有助于恶意用户的系统账户信息。某些站点禁用 `finger` 或随机化用户 ID 以增加恶意用户的难度。如果您不想运行 `finger` 守护进程，请勿安装 `finger` 软件包。

远程 `finger` 信息看起来与 `finger` 在本地系统上运行时相同，唯一的区别是：在显示结果之前，`finger` 会报告回答查询的系统名称（如上一个示例中括号所示的 `bravo`）。回答的主机名称可能与您在命令行上指定的系统不同，取决于远程系统上 `finger` 守护进程服务的配置。在某些情况下，如果一个 `finger` 守护进程联系另一个来检索信息，可能会列出多个主机名。

## 向远程用户发送邮件

给定远程系统上的用户用户名以及远程系统名称或其域名，您可以使用电子邮件程序通过网络发送消息，或使用地址的 `@` 形式：

`jenny@bravo`

或

`jenny@example.com`

尽管许多 Linux 实用程序识别地址的 `@` 形式，但您可能会发现无法访问其他系统。在许多遗留设备（如终端服务器）中，不支持。

# telnet 不是安全的

每当你使用 `telnet` 输入敏感信息（如密码）时，这些信息都会以明文形式传输，并可以被监听会话的人读取。

这两个实用程序之间的另一个区别是，`telnet` 允许你配置许多特殊参数，例如如何处理 `RETURNING`（回车）或中断。在 UNIX 和 Linux 系统之间使用 `telnet` 时，你很少需要更改任何参数。

当你没有在命令行中指定远程主机名时，`telnet` 会以交互模式运行。以下示例等同于之前的 `telnet` 操作：

```bash
[bravo] telnet
telnet> open kudos
Trying 172.19.52.2...
Connected to kudos.example.com
Escape character is '^]'
```

在连接到远程系统之前，`telnet` 会告诉你转义字符是什么；在大多数情况下，它是 `^]`（其中 `^` 代表 `CTRL` 键）。当你按下 `CONTROL-]` 时，你就会逃逸到 `telnet` 的交互模式。继续上一个示例：

```bash
[kudos]$ CONTROL-]
telnet> help
```

```bash
telnet> close
Connection closed.
[bravo]$
```

当你在 `telnet` 提示符下输入问号时，`telnet` 会列出它的命令。`close` 命令会结束 `telnet` 会话，让你返回本地系统。要退出 `telnet` 的交互模式并恢复与远程系统的通信，请在提示符处按下 `RETURN`。

你可以使用 `telnet` 访问某些选择提供此类服务的特殊远程服务。然而，其中许多服务（例如美国国会图书馆信息系统 LOCIS）已经迁移到了 Web。因此，你现在可以使用 Web 浏览器获取相同的信息。

# 使用 telnet 连接到其他端口

默认情况下，`telnet` 连接到端口 23，该端口用于远程登录。然而，你可以通过指定端口号来使用 `telnet` 连接到其他服务。除了标准服务外，互联网上的许多远程服务使用未分配的端口号。例如，你可以使用 `telnet` 连接到指定端口（如 4000 或 8888）来访问多人文本游戏，称为 MUDs（多用户地下城或维度）。与标准协议的端口号不同，游戏管理员可以任意选择端口号。

# 网络工具 375

虽然 `telnet` 不再常用于登录远程系统，但它仍被广泛用作调试工具。该实用程序允许你直接与 TCP 服务器通信。某些标准协议足够简单，经验用户可以直接使用 `telnet` 调试连接到远程服务器时的问题。如果你在网络服务器上遇到问题，良好的第一步是尝试用 `telnet` 连接到它。

在下面的示例中，一个正在调试邮件投递问题的系统管理员使用 `telnet` 连接到 `example.com` 服务器上的 SMTP 端口（25 端口），以查看为什么它会退回来自垃圾邮件域名的邮件。输出的第一行指示了 `telnet` 正在尝试连接的 IP 地址。在 `telnet` 显示 `Connected to smtpsrv.example.com` 后，用户按照标准的 SMTP 协议模拟 SMTP 对话。第一行以 `helo` 开头，开始该部分并识别本地系统。在 SMTP 服务器响应后，用户输入一行识别邮件发送者为 `user@spam.com`。SMTP 服务器的响应解释了邮件被退回的原因，用户据此结束了会话。

```bash
$ telnet smtpsrv 25
Trying 192.168.1.1...
Connected to smtpsrv.example.com.
Escape character is '^]'
helo example.com
220 smtpsrv.example.com ESMTP 8.13.1/8.13.1, Wed, 4 May 2005 00:13:43 -0500 (CDT)
250 smtpsrv.example.com Hello desktop.example.com [192.168.1.97], pleased to meet you
mail:user@spam.com
quit
571 5.0.0 Domain banned for spamming
221 2.0.0 smtpsrv.example.com closing connection
```

> `telnet` 实用程序允许你使用任何需要的协议，只要你足够熟悉它并手动输入命令。

# ftp：通过网络传输文件

文件传输协议 (FTP) 是一种通过网络上的 TCP/IP 下载文件并上传到另一个系统的方法。FTP 不是一种安全的协议；请用它从公共服务器下载公共信息。大多数网络浏览器都可以从 FTP 服务器下载文件。第 20 章涵盖了 FTP 客户端和

# ping：测试网络连接

`ping`¹ 实用程序（http://ftp.arp.ml/~mike/ping.html）向远程计算机发送一个 `ECHO_REQUEST` 包。该数据包会导致远程系统发送回复。这种交换是验证远程系统可用以及检查网络运行情况（如速度快慢或丢包）的快速方法。`ping` 实用程序使用 ICMP（互联网控制消息协议）。在没有任何选项的情况下，`ping` 每秒测试一次连接，直到你用 `CTRL-C` 终止执行。

> 1. `ping` 这个名字模仿了潜艇声纳脉冲声，用于相互识别和通信。`ping` 也可以扩展为 packet internet grep。

# 当 ping 无法连接时

如果无法连接到远程系统，`ping` 将继续运行直到你用 `CTRL-C` 中断它。系统没有响应的原因可能有：远程计算机可能宕机、网络部分可能损坏、软件故障、远程可能未启动，或者出于安全原因（尝试 www.microsoft.com 或 www.ibm.com）。

# traceroute：跟踪路由

`traceroute` 实用程序跟踪通往目的地的路由，包括经过的所有中间点（称为跳数），显示主机名列表、IP 地址以及到达每个路由的往返时间。当你尝试识别网络位置时，`traceroute` 可以帮助解决路由问题并定位路径故障。下一个示例显示了从本地计算机到 `linux.org` 的路由输出。第一行指示了目标 IP 地址，显示了最大跳数。每个星号（`*`）表示 `traceroute` 未收到响应。

默认情况下，`ping` 发送包含 64 字节数据和 8 字节头的数据包。在前面的示例中，每行显示了远程系统的 IP 地址、序列号（`icmp_seq`），如果数据包未丢失，显示两个系统之间的往返时间（毫秒）。`ping` 总结了发送和接收的包数，以及最小、最大和平均抖动。

```bash
$ ping example.mit.edu
56(64) bytes of data.
64 bytes from example.mit.edu: icmp_seq=0 ttl=54 time=97.2 ms
64 bytes from example.mit.edu: icmp_seq=1 ttl=54 time=97.1 ms
64 bytes from example.mit.edu: icmp_seq=2 ttl=54 time=95.7 ms
64 bytes from example.mit.edu: icmp_seq=3 ttl=54 time=96.3 ms
CTRL-C
--- example.mit.edu statistics
4 packets transmitted, 4 received, 0% packet loss
rtt avg/max/mdev = 95.7/96.3/0.653 ms
```

此示例显示远程系统在网络上是可用。

```bash
$ /usr/sbin/traceroute www.linux.org
traceroute to linux.org (192.188.192.56), 30 hops, 38 packets
1 gw.localco.com. (204.94.139) 2.904 ms 2.425 ms 2.783 ms
2 cvag02-meer.net (202.157.140.41) 19.727 ms 23.328 ms 24.783 ms
3 gw-mw1-meer.net (140.174.164.1) 38.957 ms 24.943 ms 19.207 ms
4 d1-a2-0.0.mtcw01.us (205.134.161.22) 54.851 ms 59.091 ms 20.241 ms
5 m4-l11-0-0.net (205.121.205.351) 181.211 ms 181.811 ms 204.560 ms
6 p1-a0-0.mtcw01.us (206.149.129.66) 178.688 ms 188.266 ms 28.003 ms
7 f4-j0-0.sjc02.rio (207.257.181.161) 232.426 ms 237.937 ms 54.946 ms
8 sjc0b.geoip.net (292.250.39.83) 245.031 ms 254.496 ms 44.925 ms
9 maei-west.us.net (192.132.160.38) 248.525 ms 262.296 ms 38.996 ms
10 E0-CRL-SFO-02-E0X.us.cr (165.113.155.52) 243.023 ms 251.910 ms 42.967 ms
11 sfo2-vfal.atm.us.cr (165.113.155.224) 235.551 ms 254.606 ms 178.632 ms
12 border-ai.ma-east.ix.ai.net (205.134.175.254) 214.642 ms 290.433 ms 219.116 ms
13 router.invogic.com (192.188.192.41) 224.358 ms 235.427 ms 228.856 ms
```

# host 和 dig：查询互联网域名服务器

`host` 工具根据名称查找 IP 地址，反之亦然。以下示例展示了如何使用 `host` 根据 IP 地址查找机器的域名名：

```bash
$ host 140.174.164.2
2.164.174.140.in-addr.arpa. domain name pointer ns.meer.net.
```

你也可以使用 `host` 来确定域名的 IP 地址：

```bash
$ host ns.meer.net
ns.meer.net. has address 140.174.164.2
```

`dig`（域名信息分组器）工具查询 DNS 服务器和单个机器以获取有关域名的信息。`dig` 是一个强大的工具，拥有许多你可能永远用不到的功能。它比这看起来要复杂得多。

关于 DNS 的第 25 章包含了许多关于 `host` 和 `dig` 的用法示例。

# whois：查询互联网站点信息

`whois`（`whois` 软件包）替换了旧的 `whois` 并向 `whois` 服务器查询互联网站点信息。这会返回站点联系人以及网络接入连接中心（NetNIC）或其他注册信息，可以帮助你追踪负责某个站点的人：也许那个人正在向你或你的公司发送垃圾邮件（第1061页）。互联网上的许多站点比 `whois` 更易用、更快。可以使用浏览器和搜索引擎搜索 `whois`，或者访问 www.worksolutions.com/whois 或 www.ripe.net/perl/whois 开始使用。

当你不指定 `whois` 服务器时，`whois` 默认使用 `whois.internic.net`。使用 `-h` 指定不同的 `whois` 服务器。请查看 `whois` 信息页获取更多选项和设置信息。

要获取域名的信息，请指定完整的域名，例所示：

```bash
$ whois sobell.com
[Querying whois.internic.net]
[Redirected to whois.godaddy.com]
[Querying whois.godaddy.com]
[whois.godaddy.com]
```
