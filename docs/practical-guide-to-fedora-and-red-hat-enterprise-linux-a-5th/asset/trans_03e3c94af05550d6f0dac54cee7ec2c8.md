
基于主机的信任在很大程度上已经过时。由于绕过受信任主机安全机制的方法很多，包括颠覆 DNS 系统和 IP 地址欺骗（第 1089 页），基于 IP 地址的认证被广泛认为是不安全且过时的。在一个由具有本地 DNS 控制权的机器组成的小型同构网络中，这种方式可能“足够好”。在这些情况下，其更高的易用性可能比安全顾虑更重要。

## 不要共享你的登录账户

你可以使用 **.rhosts** 文件允许其他用户从远程系统登录到你的账户，而无需知道你的密码。*不建议使用这种配置。* 不要通过共享登录账户来削弱你的文件或整个系统的安全性。在尽可能的时候，使用 ssh 和 scp 代替 rsh 和 rcp。

## OPENSSH 工具

OpenSSH 项目提供了一组工具，用安全的等价物取代了 **rcp**、**rsh** 和其他工具。这些工具在 Fedora/RHEL 中默认安装，并且可以作为其不安全对应物的直接替代品。OpenSSH 工具套件在第 18 章中有详细涵盖。

## telnet：登录远程系统

你可以使用 **TELNET** 协议与远程计算机进行交互。**telnet** 实用程序是该协议的用户界面，其历史比 **ssh** 悠久，且并不安全。尽管如此，它可能在 **ssh**（第 627 页）不可用的情况下仍能正常工作（与非 UNIX 系统相比，对 TELNET 访问的非 UNIX 系统支持更多）。此外，许多旧式设备（如终端服务器和网络设备）不支持 **ssh**。

```bash
[bravo] $ telnet kudos
Trying 172.19.52.2 ... 
Connected to kudos.example.com
Escape character is '^]'.

Welcome to SuSE Linux 7.3 (i386) - Kernel 2.4.10-4GB (2). 
kudos login: watson
Password:
You have old mail in /var/mail/watson.
Last login: Mon Feb 27 14:46:55 from bravo.example.com
watson@kudos:~> ...
watson@kudos:~> logout
Connection closed by foreign host.
[bravo]$
```

当你使用 **telnet** 连接到远程 UNIX 或 Linux 系统时，你会看到一个常规的文本 **login** 提示符。除非另有指定，**ssh** 实用程序假定你在远程系统上的用户名与本地系统上的用户名匹配。由于 **telnet** 旨在与非 UNIX 和非 Linux 系统协同工作，因此它不做这种假设。

这两个实用程序之间的另一个区别在于，**telnet** 允许你配置许多特殊参数，例如如何处理 **RETURN** 或中断。在 UNIX 和/或 Linux 系统之间使用 **telnet** 时，你很少需要更改任何参数。

如果你没有在必令行上指定远程主机的名称，**telnet** 将以交互模式运行。以下示例与之前的 **telnet** 示例等效：

```bash
[bravo]$ telnet
telnet> open kudos
Trying 172.19.52.2 ...
Connected to kudos.example.com
Escape character is '^]'.
...
```

在你连接到远程系统之前，**telnet** 会告诉你*转义字符*是什么；在大多数情况下，它是 **^]**（其中 ^ 代表 **CONTROL** 键）。当你按下 **CONTROL-]** 时，你将进入 **telnet** 的交互模式。继续前面的例子：

```bash
[kudos]$ ^]
telnet> ?
```

*(显示帮助信息)*

```bash
telnet> close
Connection closed.
[bravo]$
```

当你在 **telnet>** 提示符后输入问号时，**telnet** 会列出其命令。**close** 命令结束当前的 **telnet** 会话，将你返回到本地系统。要退出 **telnet** 的交互模式并恢复与远程系统的通信，请在提示符后按 **RETURN**。

你可以使用 **telnet** 访问那些选择提供此类服务的站点上的特殊远程服务。然而，其中许多服务（例如美国国会图书馆信息系统 LOCIS）已迁移到 Web。因此，你现在可以使用 Web 浏览器获取相同的信息。

### 使用 telnet 连接其他端口

默认情况下，**telnet** 连接到端口 23，该端口用于远程登录。然而，你可以通过指定端口号使用 **telnet** 连接到其他服务。除了标准服务外，Internet 上可用的许多特殊远程服务使用未分配的端口号。例如，你可以使用 **telnet** 连接到一个指定的端口（如 4000 或 8888）来访问一些多玩家文字游戏，称为 **MUDs**（Multi-User Dungeons 或 Dimensions，多用户地下城或维度）。与标准协议的端口号不同，这些端口号可以由游戏管理员任意选择。

虽然 **telnet** 不再常用于登录远程系统，但它仍被广泛用作调试工具。该实用程序允许你直接与 TCP 服务器通信。一些标准协议足够简单，熟练的用户可以使用 **telnet** 直接连接到远程服务来调试问题。如果你遇到了网络服务器问题，一个好的第一步是尝试使用 **telnet** 连接到它。

在下面的示例中，一位正在调试邮件投递问题的系统管理员使用 **telnet** 连接到 **example.com** 服务器上的 SMTP 端口（端口 25），以查看为什么来自 **spammer.com** 域名的邮件被退回。输出的第一行指示 **telnet** 正在尝试连接的 IP 地址。在 **telnet** 显示 **Connected to smtpsrv.example.com** 消息后，用户模拟 SMTP 对话，遵循标准的 SMTP 协议。以 **helo** 开头的第一行开始会话并标识本地系统。SMTP 服务器响应后，用户输入一行，将邮件发件人标识为 **user@spammer.com**。SMTP 服务器的响应解释了为什么邮件被退回，因此用户使用 **quit** 结束会话。

```bash
$ telnet smtpsrv 25
Trying 192.168.1.1...
Connected to smtpsrv.example.com.
Escape character is '^]'.

220 smtpsrv.example.com ESPMTP Sendmail 8.13.1/8.13.1; Sun, 4 May 2008 00:13:43 -0500 (CDT)
250 smtpsrv.example.com Hello desktop.example.com [192.168.1.97], pleased to meet you
550 from:user@spammer.com
571 5.0.0 Domain banned for spamming
quit
221 2.0.0 smtpsrv.example.com closing connection
```

telnet 实用程序允许你使用任何你想要的协议，前提是你足够熟悉它，能够手动输入命令。

## ftp：通过网络传输文件

文件传输协议 (FTP) 是一种使用 TCP/IP 通过网络从另一系统下载文件和向另一系统上传文件的方法。FTP 不是一个安全的协议；请仅用于从公共服务器下载公共信息。大多数 Web 浏览器都可以从 FTP 服务器下载文件。第 19 章介绍了 FTP 客户端和服务器。

## ping：测试网络连接

**ping** 实用程序 (http://ftp.arl.mil/pub/misc/ping.html) 向远程计算机发送 ECHO_REQUEST 数据包。此数据包导致远程系统发送回响应。这种交换是验证远程系统是否可用以及检查网络运行状况（例如速度快慢或是否丢失数据包）的快速方法。ping 实用程序使用 ICMP（Internet 控制报文协议）。在不指定任何选项的情况下，ping 每秒测试一次连接，直到你用 `CONTROL-C` 中止执行。

```bash
$ ping tsx-11.mit.edu
PING tsx-11.mit.edu (18.7.14.121): 56 (84) bytes of data.
64 bytes from TSX-11.MIT.EDU (18.7.14.121): icmp_seq=0 ttl=45 time=97.2 ms
64 bytes from TSX-11.MIT.EDU (18.7.14.121): icmp_seq=1 ttl=45 time=96.1 ms
64 bytes from TSX-11.MIT.EDU (18.7.14.121): icmp_seq=2 ttl=45 time=95.7 ms
64 bytes from TSX-11.MIT.EDU (18.7.14.121): icmp_seq=3 ttl=45 time=96.3 ms
^C
--- tsx-11.mit.edu ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3001ms
rtt min/avg/max/mdev = 95.755/96.361/97.202/0.653 ms
```

此示例表明名为 **tsx-11.mit.edu** 的远程系统正在运行并且可通过网络访问。

默认情况下，ping 发送包含 64 字节（56 字节数据 + 8 字节协议头信息）的数据包。在上面的示例中，在用户按下 `CONTROL-C` 中断 ping 之前，向系统 **tsx-11.mit.edu** 发送了四个数据包。每行括号中的四位数字是远程系统的 IP 地址。还给出了数据包序列号（称为 **icmp_seq**）。如果数据包丢失，序列号中会出现空缺。往返时间列在最后；它代表从本地系统将数据包发送到远程系统，到本地系统接收到远程系统的响应所经过的时间（以毫秒为单位）。此时间受两个系统之间的距离、网络流量以及两台计算机的负载影响。在终止之前，ping 会总结结果，指示发送和接收的数据包数量，以及它测量的最小、平均、最大和平均偏差往返时间。使用 ping6 测试 IPv6 网络。

### 当 ping 无法连接时

> **提示** 如果无法联系到远程系统，ping 将继续尝试，直到你用 `CONTROL-C` 中断它。系统可能因多种原因无法响应：远程计算机可能已关机，两个系统之间的网络接口或网络的一部分可能已损坏，可能发生了软件故障，或者远程机器出于安全原因被设置为不响应 ping（尝试 ping www.microsoft.com 或 www.ibm.com）。

## traceroute：追踪互联网上的路由

traceroute 实用程序追踪 IP 数据包遵循的路由，包括所有途经点（称为*网络跳*），直到其目的地（traceroute 的参数——一个 Internet 主机）。它显示一个编号的主机名列表（如果可用）和 IP 地址，以及数据包到达每个点所花费的往返时间

