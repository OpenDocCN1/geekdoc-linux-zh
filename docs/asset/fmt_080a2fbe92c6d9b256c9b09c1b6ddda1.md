
```
tcp      0 0 *:Local  Foreign Address  Q-State
tcp      0 0 *:shell             *:* LISTEN
tcp      0 0 *:telnet          *:* LISTEN
tcp      0 0 *:ftp               *:* LISTEN
udp      0 0 parrot:netbios-dgm  *:*
udp      0 0 parrot:netbios-ns  *:*
udp      0 0 *:netbios-dgm      *:*
udp      0 0 *:netbios-ns      *:*
udp      0 0 *:1024            *:*
udp      0 0 *:talk             *:*
raw      0 0 *:icmp             7
raw      0 0 *:tcp               7
Active UNIX domain sockets (servers and established)
Proto RefCnt Flags  Type     State     I-Node Path
unix 1 [ ]     STREAM CONNECTED 415 00000019
unix 1 [ ]     STREAM CONNECTED 888 0000003e
unix 0 [ ACC ] STREAM LISTENING 519 /dev/printer
unix 0 [ ACC ] STREAM LISTENING 725 /dev/gpmctl
unix 0 [ ACC ] STREAM LISTENING 395 /dev/log
unix 1 [ ]     STREAM CONNECTED 889 /dev/log
```

此列表中的第一行显示了一个入站 `telnet` 连接，与之前看到的相同。接下来的几行状态为 `LISTEN`（监听）。这些是该系统提供的 `TCP` 服务。如果服务器上 `netstat` 提供的服务列表与您认为系统提供的服务不匹配，则需要检查服务器的配置。地址字段中的星号（`*`）表示接受任何地址。

接下来是系统提供的 `UDP` 服务。`UDP` 是一种无连接协议，因此不维护连接状态。对于所有 `UDP` 条目，`State`（状态）字段都是空的。同样，这些服务应该与您提供的服务匹配。

对于网络测试，您可以忽略列表的其余部分。它包含两个原始（`raw`）套接字条目，即在不使用传输协议的情况下直接与 `IP` 通信的套接字，以及几个 `Unix` 套接字条目。`Unix` 套接字定义了 `Linux` 设备的基于套接字的 `I/O`，与 `TCP/IP` 网络无关。

# 分析网络协议

使用 `netstat` 检查入站或出站连接出现挂起时的套接字状态。如何使用这些 `netstat` 信息来诊断问题的示例见在本章末尾的案例研究。

# 使用 tcpdump 监控协议

`tcpdump` 读取来自以太网的每一个包，并将其与您定义的过滤器进行比较。如果匹配过滤器，数据包头将显示在您的终端上，从而允许您实时监控流量。例如：

```
# tcpdump 172.16.5.1 and 172.16.24.1

tcpdump: listening on eth0

10:46:11.576386 phoebe.1027 > wren.telnet: S
40040549:40040549(0) min 32120
<mss 1460>

10:46:11.578991 wren.telnet > phoebe.1027: S
122511948:122511948(0) ack 400405050 min 32120
<mss 1460>(DF)

10:46:11.576386 phoebe.1027 > wren.telnet: S
40040549:40040549(0) min 32120
```

## 表 15.2 tcpdump 数据包过滤器（续）

| 过滤器 | 捕获数据包... |
|---|---|
| `net address [/len \| mask mask]` | 发往或来自指定的网络。可选的地址掩码可以定义为位长度或点点十进制掩码。 |
| `port port` | 发往或来自指定的端口。 |
| `ip proto protocol` | 指定指定的协议类型。有效的协议有 `icmp`, `igrp`, `udp`, `nd`, 或 `tcp`。 |
| `ip broadcast multicast` | 无论是 `IP` 广播数据包还是 `IP` 多播数据包。 |

> 提示：使用这些过滤器，你应该能够捕获调试网络问题时所需的任何数据包。但我的建议是保持简单。设计复杂的过滤器和分析大型转储所花费的时间可能比解决问题的其他简单方法要多。

# 测试服务

在协议栈的顶端是用户需要的应用程序和服务。当用户尝试使用服务而尝试失败时，通常会报告错误。为了确保完整性，测试需要包含服务。

通常服务可以直接进行测试。要测试 `Web` 服务器，请用浏览器连接到服务器。要测试 `FTP` 服务器，使用 `ftp` 命令连接到该服务器。这些是面向用户的服务，因此它们带有你可以用于测试的面向用户的命令。

然而，某些服务旨在为远程计算机提供服务，而不是直接面向远程用户。直接测试这些服务略有困难，但通过使用 `telnet` 直接连接到服务器端口通常是可能的。你在前面的章节中已经看到过多次此类示例。请回看第 13 章“更多邮件服务”中测试 `imapd` 和 `POP` 守护进程的示例。

如果 `ping` 测试成功但涉及特定服务的测试失败，则问题出在客户端或服务器端的配置上。客户端配置通常简单且易于检查，但服务器配置可能非常复杂。某些复杂的服务（如 `sendmail` 和 `DNS`）包含了自身的测试程序。第 7 章“配置邮件服务器”提供了使用 `sendmail -bt` 测试本地 `sendmail` 配置的详细示例。本章的下一节将介绍用于测试 `DNS` 配置的工具。

## 使用 nslookup 测试 DNS

`nslookup` 是随 `BIND` 软件一起的一个测试工具。它是一个交互式程序，允许你查询 `DNS` 服务器的任何类型的资源记录，并直接查看服务器的响应。这对于检查自己的配置很有用，但更重要的是，它可以被用于直接查询远程服务器。注意“直接”这个词的强调。使用 `nslookup`，可以直接连接到远程服务器以查看服务器如何响应查询，而无需通过你的本地名称服务器。这很重要，因为消除了本地服务器配置中的错误影响结果的可能性。任何允许你将本地问题与远程问题隔离开来的测试程序都无价值连城。

为了说明我的意思，这里有一个如何使用 `nslookup` 的示例：

```
% nslookup
Default Server: wren.foobirds.org
Address: 172.16.5.1
```

```
> set type=NS
> mammals.org.
Server: wren.foobirds.org
Address: 172.16.5.1
```

```
mammals.org nameserver = goat.mammals.org
mammals.org nameserver = shark.fish.org
mammals.org nameserver = whale.mammals.org
goat.mammals.org inet address = 172.32.3.2
shark.fish.org inet address = 172.30.8.2
whale.mammals.org inet address = 172.32.3.1
```

首先输入不带参数的 `nslookup` 命令。这首先以交互模式启动 `nslookup`，这是使用它来调试服务器问题的最佳方法。当 `nslookup` 启动时，如 `Default Server` 消息所示，它正在使用你的本地服务器。你需要定位要测试的域服务器，因此将查询类型设置为 `NS`，然后输入示例中你想要的域名，例如域名是 `mammals.org`，本地服务器返回该域的所有 `NS` 记录，这些记录识别了三个服务器：`mammals.org` 域中的 `goat` 和 `whale` 以及 `shark.fish.org`。

现在你已经知道了权威服务器，连接到其中一个来运行测试的下一阶段：

```
> goat.mammals.org
> Default Server: goat.mammals.org
> Address: 172.32.3.2
> set type=ANY
> dolphin.mammals.org
> Server: goat.mammals.org
> Address: 172.32.3.2
dolphin.mammals.org inet address = 172.32.3.8
> exit
```
