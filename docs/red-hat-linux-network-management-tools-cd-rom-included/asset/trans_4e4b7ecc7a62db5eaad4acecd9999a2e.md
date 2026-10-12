
## 显示活动网络会话

该工具的一个有用功能是在线帮助。只需使用 `-h` 或 `--help` 选项调用命令：

```
netstat --help
```

### 清单 4.2 netstat --help 的结果

```
usage: netstat [-veenNcCF] [<AF>] -r				 netstat [-V|-version|-h|--help]
netstat [ -vvnNcaee0] [-Socket ...]
netstat [-vveenNc] [-i | [-cne] -M | -s]
										
-r, --route				显示路由表
										
-i, --interfaces		显示接口表
-g, --groups			显示多播组成员资格
-s, --statistics		显示网络统计信息（如 SNMP）
-M, --masquerade		显示伪装连接
										
-v, --verbose				详细输出
-n, --numeric			不解析名称
-N, --symbolic			解析硬件名称
-e, --extend			显示其他/更多信息
-P, --programs			显示套接字的 PID/程序名
-c, --continuous		持续列出
										
-l, --listening		显示监听服务器套接字
-a, --all, --listening	显示所有套接字（默认：已连接）
-o, --timers		显示计时器
-F, --fib			显示转发信息库（默认）
-C, --cache			显示路由缓存而非 FIB
										
<Socket>={-t|-tcp|-u|-udp|-w|-raw|-x|-unix|-ax25|-ipx|--netrom}
<AF>=Use “-A <af>” or “--af” [Default: inet] 可能的地址族列表（支持路由）：inet (DARPA Internet) ax25 (AMPR AX.25) netrom (AMPR NET/ROM)
```

**netstat** 提供的重要服务之一是查看系统间活动连接的能力。本地主机与任何其他系统之间的任何 TCP 会话都可以被监控。此外，任何已创建的流套接字也将被显示。流被用作程序间通信通道。要显示当前建立的连接，请使用 `-t` 选项执行 `netstat`，如下所示：

```
# netstat -t
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 orlando-11-12:1052 192.215.123.37:www ESTABLISHED
tcp 1 0 orlando-11-12:1051 192.215.123.37:www CLOSE
tcp 0 6 orlando-11-12:1050 postoffice.worldinpop:3 ESTABLISHED
tcp 0 0 orlando-11-12:1049 wwwx.yahoo.com:www ESTABLISHED
tcp 0 0 socrates.home.co:telnet durer.home.com:1033 ESTABLISHED
tcp 0 0 socrates.home.co:telnet durer.home.com:1032 ESTABLISHED
```

回顾表 4.5，`-t` 选项将显示 TCP 套接字活动。如所示，上述命令的输出包含本地系统上的连接。每个连接都包含有关本地和远程地址、统计信息以及连接状态的信息。本地和远程地址的显示包含主机名和端口信息，格式为：*主机, 端口*，其中 *主机* 可以是来自 `/etc/hosts` 的分配主机名（或来自其他主机解析机制，如 NIS 或 DNS），也可以是有效的 IP 地址。*端口* 代表 `/etc/services` 中定义的保留端口，或由系统分配的套接字。本地地址是源，远程地址是目的地。回想一下，TCP 使用四个元素组成连接，并将状态机模型作为 TCP 传输机制的一部分。因此，*monet.telnet* 和 *rebrandmt.1036* 被视为一个连接。从 *状态* 字段可以看出，该连接处于 *ESTABLISHED* 状态，这意味着它正在来回传递数据。

回想一下，TCP 使用状态机来控制定义的每个状态，我们可以使用 `netstat` 命令来跟踪和显示每个 TCP 连接的状态。表 4.7 显示了最常见的状态，并包含每种状态的一般描述。

### 表 4.7 netstat 显示的 TCP 状态

| 状态 | 描述 |
| --- | --- |
| ESTABLISHED | 连接正常运行 |
| LISTEN | 服务或应用程序正在等待客户端连接 |
| SYN_SENT | 本地系统想要打开远程连接 |
| SYN_RCVD | 远程系统想要打开连接 |
| FIN_WAIT_1 | 本地系统正在关闭连接的过程中 |
| FIN_WAIT_2 | 本地系统正在关闭连接的过程中 |
| CLOSE_WAIT | 远程系统想要关闭连接 |
| LAST_ACK | CLOSE_WAIT 的最后一步 |
| TIME_WAIT | FIN_WAIT_1 或 FIN_WAIT_2 的最后一步 |
| UNKNOWN | 套接字状态未知 |

前面的 `netstat` 命令仅显示处于或曾处于 *ESTABLISHED* 状态的连接。有时列出系统上所有可用且活动的服务很有帮助。这可以通过使用带有 `-a` 选项的 `netstat` 来实现，如下所示。

请注意，以下输出已精减以提高可读性。在大多数系统上执行此命令将产生更大的列表，因为它也将包括流接口。不过，我们可以使用 `-t` 和 `-u` 选项进一步细化输出，使其仅包含 TCP 和 UDP 套接字。以下输出提供了 UDP 和 TCP 服务的列表，无论其连接状态如何。这很有用，因为并不总是显而易见某个特定服务使用哪种传输协议。

```
# netstat -a -t -u
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 socrates.home.co:telnet durer.home.com:1033 ESTABLISHED
tcp 0 0 orlando-11-1:domain *.* LISTEN
tcp 0 0 *:1048 *.* LISTEN
tcp 0 0 *:1047 *.* LISTEN
tcp 0 0 *:1046 *.* LISTEN
tcp 0 0 *:1045 *.* LISTEN
tcp 0 0 *:1044 *.* LISTEN
tcp 0 0 *:1037 *.* LISTEN
tcp 0 710 socrates.home.co:telnet durer.home.com:1032 ESTABLISHED
tcp 0 0 *:6000 *.* LISTEN
tcp 0 0 *:nntp *.* LISTEN
tcp 0 0 *:www *.* LISTEN
tcp 0 0 *:smtp *.* LISTEN
tcp 0 0 *:713 *.* LISTEN
tcp 0 0 *:1024 *.* LISTEN
tcp 0 0 *:683 *.* LISTEN
tcp 0 0 *:678 *.* LISTEN
tcp 0 0 *:673 *.* LISTEN
tcp 0 0 *:652 *.* LISTEN
tcp 0 0 *:printer *.* LISTEN
tcp 0 0 10.0.2.205:domain *.* LISTEN
tcp 0 0 10.0.2.202:domain *.* LISTEN
tcp 0 0 socrates.home.co:domain *.* LISTEN
tcp 0 0 localhost:domain *.* LISTEN
tcp 0 0 *:linuxconf *.* LISTEN
tcp 0 0 *:auth *.* LISTEN
tcp 0 0 *:finger *.* LISTEN
tcp 0 0 *:login *.* LISTEN
tcp 0 0 *:shell *.* LISTEN
tcp 0 0 *:telnet *.* LISTEN
tcp 0 0 *:ftp *.* LISTEN
tcp 0 0 *:sunrpc *.* LISTEN
udp 0 0 orlando-11-1:domain *.*
udp 0 0 *:x1mcqp *.*
udp 0 0 localhost:1119 *.*
udp 0 0 *:800 *.*
udp 0 0 *:1022 *.*
udp 0 0 *:714 *.*
udp 0 0 *:1023 *.*
udp 0 0 *:1026 *.*
udp 0 0 *:2049 *.*
udp 0 0 *:681 *.*
udp 0 0 *:676 *.*
udp 0 0 *:671 *.*
udp 0 0 *:661 *.*
udp 0 0 *:650 *.*
udp 0 0 *:1024 *.*
udp 0 0 10.0.2.205:domain *.*
udp 0 0 10.0.2.202:domain *.*
udp 0 0 socrates.home.co:domain *.*
udp 0 0 localhost:domain *.*
udp 0 0 *:smtp *.*
udp 0 0 *:talk *.*
udp 0 0 *:sunrpc *.*
```

在 TCP 标题下，不仅显示了前一个示例中的两个 TCP 连接，还包含了其他服务。处于 LISTEN 状态的任何服务都在等待传入连接，通常称为基于服务器的资源。当服务等待来自网络的请求时，它可以自由接受来自任何远程地址的连接。这就是为什么 *.* 会列在外部地址字段下。服务器通常也在本地主机部分放置 *，以进一步表明如果发出客户端请求，服务器可以自由建立连接。当客户端的请求发送到服务器时，服务器会复制自身来处理该请求，并继续监听其他客户端请求。因此，当这种情况发生时，netstat 会显示同一服务的多个实例，如下所示：

```
netstat -a | grep ftp

tcp 0 0 0 0 0 0 .home.co : ftp: data durer.home.com: 1034 TIME_WAIT
tcp 0 0 0 0 0 0 .home.co : smtp durer.home.com: 1033 ESTABLISHED
tcp 0 0 0 0 0 0 *:ftp *:* 
```

上面的命令执行 netstat 并将输出通过管道传给 grep 命令，后者扫描输入中的 ftp 字符串。结果显示所有包含 ftp 字符串的行。在上面的输出中，FTP 服务器仍在监听传入的连接请求，同时 FTP 会话已建立到套接字。

在前一个输出示例的 UDP 标题下，仅显示了本地地址和状态字段；未指定外部地址。这是因为 UDP 是无连接协议，因此不需要远程地址信息。另请注意，UDP 没有可用的统计信息。这也是 UDP 从设计上根本不同且不需要此类信息的另一个迹象。

尽管 `-a` 选项提供了相当大量的信息，但 netstat 可用于快速检查，以确保正确的服务正在给定系统上运行。通过扫描
