
在不同的计算机上保持文件一致且最新可能代价很高。在这种情况下，可以分发文件，例如通过 NIS（网络信息系统；参见第 21 章）。

两台计算机之间的通信通过这些端口进行。在的一端，程序必须通过此端口建立连接；在另一端，另一个程序必须监控此端口并执行必要的操作。有两种替代方案：

- 启动服务器（在后台）并监听该端口。因此，服务器完全负责连接的完整建立。

- 当有请求到达相应的端口时，由 `inetd` 启动服务器。要监控的端口以及选项和程序都配置在 `/etc/inetd.conf` 文件中。一个端口不能同时通过这两种替代方案进行监控。

在 TCP 应用中，可以通过对该端口建立 telnet 连接来确定连接的端是否运行了适当的服务器。例如，可以使用 echo 服务来检查字符是否可以双向传输。你也可以使用 telnet 激活诸如 `smtp`（简单邮件传输协议）等应用协议并以这种方式测试服务器。

通常使用 `echo` 和 `discard` 协议进行首次测试。列表 14.3 显示了一个示例。另一方面，这些服务也可以被用于所谓的“拒绝服务”攻击。出于这个原因，这些服务在许多系统中是不可用的——这是完全正确的，因为它们通常根本就不需要。

```
(Linux):$ telnet localhost echo
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'
This is a test
This is a test
^
telnet> quit
Connection closed.
```
列表 14.3 将 telnet 作为测试工具

如果你想查看系统上当前启动的服务的概览，可以使用 `netstat -a` 命令。它会显示所有现有连接，以及提供服务的所有端口。

# inetd 服务器 401

单个 TCP 连接由源 IP 地址、目的 IP 地址以及源端口和目的端口定义。例如，从一个主机到服务器的两个 telnet 会话中，这三个值是相同的：源 IP 地址、目的 IP 地址和目的端口。每个连接都有动态分配的源端口，因此可以将它们区分开。

## 12.2 inetd 服务器

为了能够正确响应客户端的请求

| serv soc_prot flags user server_path args |
|---|---|---|---|---|---|
| echo stream tcp nowait root /usr/sbin/tcpd | /usr/sbin/wu.ftp |
| ftp stream tcp nowait root /usr/sbin/tcpd | |
| talk dgram udp wait root /usr/sbin/tcpd | /usr/sbin/in.ntalkd |

列表 14.4 `/etc/inetd.conf` 文件的节选。

注释以井号符号开头并以行尾结束。对于 `/etc/services` 中的每个服务，可以输入一行，前提是相应的守护进程支持通过 `inetd` 启动。第一列包含应用协议的名称；你应该使用在 `/etc/services` 中找到的官方名称。

第二列指定套 的类型。合法值有 `stream`（流）、`dgram`（数据报）、`raw`（原始）、`rnd`（可靠交付的消息）和 `seqpacket`（顺序数据包套字）。如果你想向此文件添加新服务，例如安装了一个新的守护进程，你通常会在程序的文档中找到相应的条目。

第三列包含来自 `/etc/protocols` 文件的有效协议。对于 TCP 和 UDP 服务，输入 `tcp` 或 `udp`。如果你还想用 `inetd` 管理 RPC 服务，可以输入 `rpc/tcp` 或 `rpc/udp`。

下一列指示连接到达后 `inetd` 服务器的操作。`wait` 和 `nowait` 之间的区别仅适用于数据报套字；对于所有其他，必须输入 `nowait`。当连接建立（且相应的守护进程支持）时，相应的套字可以再次被 `inetd` 监控，并处理进一步的请求。

![](img/ad3b0471a5d608a011338d028bec5422_420_0.png)

# 402 TCP/IP 基础

为此输入 `nowait`。对于不是多线程的服务，必须输入 `wait`。如果你想限制 60 秒内处理的最大连接数，可以在点（`.`）之后指定它。

第五列包含执行服务的 ID 下的用户名。如果你还想更改组，可以通过点分隔它们来指定。许多守护进程必须以 `root` 权限启动。对于某些服务（例如 `finger`），出于安全考虑，以 `nobody` 或另一个 ID 启动可能是明智的。

下一个条目的是要启动的程序名称，以及可能传递的参数。参数以 `arg[]` 开头，即程序名称本身。旧的 UNIX 系统限制参数为五个条目，因此你可能需要启动一个脚本，通过使用适当参数调用服务器。

`inetd` 服务器提供了一些简单的服务（`echo`、`discard`、`charg`、`daytime`、`time`）。对于这些服务，程序输入 `internal`。

修改 `inetd.conf` 文件后，守护进程必须重新读取此文件，或者可以终止而不启动，或者可以发送一个 `SIGHUP` 信号，例如使用命令 `kill -HUP 'cat var/run/syslog'`。通常，`inetd` 服务器允许任何连接；防火墙的维护通常是必要的。

## 14.3 TCP wrapper (tcpd)

一种保护措施通过 TCP wrapper (`tcpd`) 实现。它根据 `hosts.deny` 和 `hosts.allow` 文件检查连接是否合法。你使用网络信息系统 (NIS)。匹配也可以通过网络数和掩码的组合来指示。因此，条目 `192.168.72.0/255.255.254.0` 代表 `192.168.72.0` 到 `192.168.73.255` 之间的所有地址。关于这些主题的更多信息可以在 `tcpd(8)` 手书中找到。

# TCP WRAPPER (tcpd) 403

`hosts.deny` 或 `hosts.allow` 中条目的格式在 `hosts.access(5)` 手书中。对于每个协议以及每个主机或 IP 范围，可以指定是否允许或禁止服务，以及执行哪些操作。

列表 14.5 显示了一个 release 服务的示例。区分了内部连接和外部连接。内部连接（来自网络 `192.168.0` 或域名 `example.org`）被允许且无需进一步操作。对于外部连接，日志文件写入 `/syslog.conf`。

```
# 记录外部的 "ftp" 和 "telnet"
in.ftptpd: 192.168
in.telnetd: .example.org
in.ALL@ALL: severity = local0.notice
in.telnetd: ALL@ALL: severity = local0.notice
```
列表 14.5 `/etc/hosts.allow` 文件的示例。

除了网络数，你还可以使用域名的模式。网络数以点结束，域名必须以点开头。使用 `@` 指定一个网络组。

`ALL` 条目适用于所有未被条目覆盖的计算机。`LOCAL` 关键字代表本地计算机。识别这些是因为主机名中没有出现触发域名的点。

列表 14.6 中的示例显示了禁止某些或所有计算机或网络连接的简单方法。

```
# 对于所有主机的 TFTP
# （除了 /etc/hosts. 中的例外）
in.ftptpd: ALL
in.telnetd: 192.168.31.155
ALL EXCEPT in.fingerd: rtfm.with.edu, .com
```
列表 14.6 `/etc/hosts.deny` 文件的示例。
