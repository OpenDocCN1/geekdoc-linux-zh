
在主人的意愿下，受感染的机器现在可以被用来向选定的主机集中发射垃圾数据流。与成千上万其他受感染的机器协同工作，一个“脚本小子”（即某人，通常是年轻人，他们没有创建蠕虫或病毒的知识，但具有寻找并启动这些工具的动力和一点技巧）现在拥有使互联网上几乎任何网站瘫痪的能力。

检测 `DDOS` 与检测 `DOS` 攻击类似。可能会出现以下一个或多个迹象：

- 持续饱和的数据链路
- 在低谷时段链路饱和度没有降低
- 数百甚至数千个同时发生的网络连接
- 系统性能极慢

为了确定你的数据链路是否饱和，`ping` 外部主机的操作可以讲述大部分故事。比平时高得多的延迟是明显的迹象。正常的 `ping` 延迟（即 `ping` 响应从远程主机返回所需的时间）如下所示：

```
###### ping www.example.com
PING www.example.com (192.0.34.166) from 10.0.0.11: 56(84) bytes of data

64 bytes from 192.0.34.166: icmp_seq=1 ttl=49 time=40.1 ms
64 bytes from 192.0.34.166: icmp_seq=2 ttl=49 time=42.5 ms
64 bytes from 192.0.34.166: icmp_seq=3 ttl=49 time=39.5 ms
64 bytes from 192.0.34.166: icmp_seq=4 ttl=49 time=38.4 ms
64 bytes from 192.0.34.166: icmp_seq=5 ttl=49 time=39.0 ms

--- www.example.com ping statistics ---
5 packets transmitted, 5 received, 0% loss, time 4035ms
rtt min/avg/max/mdev = 38.472/39.971/42.584/1.432 ms
```

在上面的示例中，`ping` 数据包完成往返的平均时间约为 39 毫秒。

对一个接近饱和链路的 `ping` 看起来像这样：

```
###### ping www.example.com
PING www.example.com (192.0.34.166): from 10.0.0.11: 56(84)bytes of data

64 bytes from 192.0.34.166: icmp_seq=1 ttl=62 time=1252 ms
64 bytes from 192.0.34.166: icmp_seq=2 ttl=62 time=1218 ms
64 bytes from 192.0.34.166: icmp_seq=3 ttl=62 time=1290 ms
64 bytes from 192.0.34.166: icmp_seq=4 ttl=62 time=1288 ms
64 bytes from 192.0.34.166: icmp_seq=5 ttl=62 time=1241 ms

--- www.example.com ping statistics ---
5 packets transmitted, 5 received, 0% loss, time 5032ms
rtt min/avg/max/mdev = 1218.059/1258.384/1290.861/28.000 ms
```

在这个示例中，`ping` 数据包完成往返的平均时间约为 1.3 秒。从第一个示例到第二个示例，延迟增加了 31 倍！数据链路从正常工作效率降低到 31 倍，这是链路利用率需要调查的明显迹象。

为了更准确地测量数据吞吐量，可以使用诸如 `ttcp` 之类的工具。要用 `ttcp` 测试你的连接，你必须在网络内部和外部的机器上安装 `ttcp` `RPM` 包。（`ttcp` 包随本书附带的光盘提供。）如果你不确定包是否已安装，只需在命令提示符下输入 `ttcp`。你应该看到类似以下内容：

```
###### tcp
Usage: tcp -t [options] host [ < in ]
        tcp r [options > out]
Common options:
-4 Use IPv4
-6 Use IPv6
-l ## length of bufs read from or written to network (default 8192)
-u use UDP instead of TCP
-p ## port number to send to or listen at (default 5001)
-s -t: source a pattern to network
-r: sink (discard) all data from network
-A align the start of buffers to this modulus (default 16384)
-0 start buffers at this offset from the modulus (default 0)
-v verbose: print more statistics
-d set SO_DEBUG socket option
-b ## set socket buffer size (if supported)
-f X format for rate: k,K = kilo(bit,byte); m,M = mega; g,G = giga
Options specific to -t:
-n ## number of source bufs written to network (default 2048)
-D don't buffer TCP writes (sets TCP_NODELAY socket option)
-W ## number of microseconds to wait between each write
Options specific to r:
-B for -s, only output full blocks as specified by -l (for TAR)
-T "touch": access each byte as it's read
-I if Specify the network interface (e.g. eth0) to use
```

第一步是在服务器机器上启动一个接收进程：

```
###### tcp -rs
tcp_r: buflen=8192, nbuf=2048, align=16384/0, port=5001 tcp
tcp-r: socket
```

`-r` 标志表示服务器机器将是接收方。与 `-r` 标志结合使用，`-s` 标志告诉 `ttcp` 你希望忽略接收到的任何数据。

下一步是让数据链路外部的人，使用与你速度相近的网络链路，设置一个 `ttcp` 发送进程：

```
###### ttcp -ts server.example.com
   ttcp-t: buflen=8192, nbuf=2048, align=16384/0, port=5001 tcp ->
          server.example.com
   ttcp-t: socket
   ttcp-t: connect
```

让进程运行几分钟，然后在发送端按 `[Ctrl]+C` 停止测试。接收端随后会花一点时间计算并显示结果：

```
###### ttcp -rs
   ttcp-r: buflen=8192, nbuf=2048, align=16384/0, port=5001 tcp
   ttcp-r: socket
   ttcp r: accept from 64.223.17.21
   ttcp-r: 2102496 bytes in 70.02 real seconds = 29.32 KB/sec +++
   ttcp-r: 1226 I/O calls, msec/call = 58.49, calls/sec = 17.51
   ttcp-r: 0.0user 0.0sys 1:10real 0% 01+0d 0maxrss 0+2pf 0+csw
```

在这个示例中，两个主机之间的平均带宽为 29.32 `KB/s`。在遭受 `DDoS` 的链路上，这个数字将是该数据链路额定实际带宽的极小一部分。

如果数据链路确实饱和，下一步是确定连接来自哪里。使用 `netstat` 命令是一个非常有效的方法，它包含在 `CentOS` 基础安装中。输入以下内容以查看连接信息：

```
###### netstat -tupn
```

表 13-2 描述了此处使用的每个 `netstat` 参数。

### 表 13-2

`netstat` 参数

| 参数 | 描述 |
| :--- | :--- |
| `-t, --tcp` | 显示 `TCP` 套接字连接。 |
| `-u, --udp` | 显示 `UDP` 套接字连接。 |
| `-p, --program` | 显示每个套接字所属的程序的 `PID` 和名称。 |
| `-n, --numeric` | 显示数字地址，而不是尝试确定符号主机名、端口或用户名。 |

543

### 第三部分 管理

以下是输出结果的一个示例：

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State | PID/Program Name |
| --- | --- | --- | --- | --- | --- | --- |

输出结果按以下定义的列进行组织：

- `Proto` — 套接字使用的协议
- `Recv-Q` — 未由附加到此套接字的用户程序复制的字节数
- `Send-Q` — 未被主机确认的字节数
- `Local Address` — 套接字本地端的地址和端口号
- `Foreign Address` — 套接字远程端的地址和端口号
- `State` — 套接字的当前状态。表 13-3 列出了套接字的状态。
- `PID/Program Name` — 拥有该套接字的进程 ID 和程序名称

在 `DOS` 攻击期间，每个连接的外方地址通常都是相同的。在这种情况下，只需输入 `whois` 命令，然后跟上该外方 `IP` 地址，即可确定导致攻击的机器 `IP` 地址的所有者。

在 `DDOS` 攻击期间，每个连接的外方地址可能都不同。在这种情况下，由于可能有数千个攻击者，因此不可能追踪到所有违规者。最好的防御方法是联系您的 `ISP`，查看其是否可以在边界路由器上过滤流量。

### 防护入侵攻击

黑客拥有各种各样的工具和技术来辅助他们入侵您的计算机。入侵攻击专注于利用您安全性的弱点，因此黑客可以比从外部获得对您系统更多的控制权（并潜在地造成更大的损害）。

### 表 13-3 套接字状态

| State | Description |
| --- | --- |
| `ESTABLISHED` | 套接字已建立连接。 |
| `SYN_SENT` | 套接字正在积极尝试建立连接。 |
| `SYN_RECV` | 从网络接收到连接请求。 |
| `FIN_WAIT1` | 套接字已关闭并正在关机。 |
| `FIN_WAIT2` | 套接字正在等待远程端关闭。 |
| `TIME_WAIT` | 套接字在关闭后正在等待处理仍在网络中的数据包。 |
| `CLOSED` | 套接字未被使用。 |
| `CLOSE_WAIT` | 远程端已关闭，正在等待套接字关闭。 |
| `LAST_ACK` | 远程端已关闭，且套接字已关闭，正在等待确认。 |
| `LISTEN` | 套接字正在等待传入连接。 |
| `CLOSING` | 连接的双端均已关闭，但并非所有数据都已发送。 |
| `UNKNOWN` | 套接字的状态未知。 |

幸运的是，有许多工具和技术可用于对抗入侵攻击。本节讨论最常见的入侵方法以及可用于保护系统的工具。尽管所示的示例特定于 `CentOS` 系统，但这些工具和技术通常适用于任何其他 `Linux` 或类 `UNIX` 操作系统。

### 评估对网络服务的访问

`CentOS` 及其 `UNIX` 同类系统提供了许多网络服务，同时也为黑客攻击提供了许多途径。您应该了解这些服务以及如何限制对它们的访问。

我所说的*网络服务*是什么意思？基本上，我指的是远程用户可以请求服务器机器提供的资源或设施，例如登录、文件共享、即时消息或其他服务。电子邮件路由是一种网络服务。提供网页也是如此。您的 `Linux` 机器有可能提供数千种服务。其中许多列在 `/etc/services` 文件中。看看该文件的一个片段：

```
###### /etc/services:
###### service-name port/protocol [aliases ...] [# comment]
chargen 19/tcp ttyst source
chargen 19/udp ttyst source
ftp-data 20/tcp
ftp-data 20/udp
###### 21 is registered to ftp, but also used by fso
ftp 21/tcp ftp ftpsp fspd
ftp 21/udp
ssh 22/tcp # SSH Remote Login Protocol
ssh 22/udp # SSH Remote Login Protocol
telnet 23/tcp
telnet 23/udp
###### 24 - private mail system
smtp 25/tcp mail
```

在注释行之后，您会注意到三列信息。左列包含每个服务的名称。中列定义了该服务使用的端口号和协议类型。最右字段包含该服务的可选别名或别名列表。

作为一个例子，检查文件片段中的最后一个条目。它描述了 `SMTP`（简单邮件传输协议）服务，这是用于在 `Internet` 上递送电子邮件的服务。中列包含文本 `25/tcp`，这告诉我们 `SMTP` 协议使用端口 25，并使用传输控制协议（`TCP`）作为其协议类型。

到底什么是端口号？它是为特定网络服务保留的唯一编号。它允许网络连接正确路由到处理该服务的软件。例如，当电子邮件消息从另一台计算机递送到您的 `Linux` 机器时，远程系统必须首先与您的系统建立网络连接。您的计算机接收到连接请求，检查它，看到其标记为端口 25，因此知道该连接应交给处理电子邮件的程序（碰巧是 `sendmail`）。

我提到 `SMTP` 使用 `TCP` 协议。一些服务使用 `UDP`，即用户数据报协议。对于本次安全讨论而言，关于 `TCP` 和 `UDP` 您真正需要了解的是，它们提供了在通过网络连接发送信息时的不同封装方式。`TCP` 连接提供错误检测和丢失数据的重传。`UDP` 不检查以确保数据完整且无损地到达；它是作为发送非关键信息的快速方式设计的。

### 禁用网络服务

尽管有数百种服务（列在 `/etc/services` 中）在您的 `CentOS` 系统上可能可用并遭受攻击，但实际上，只有少数几种服务被安装，而其中只有少数几种默认开启。大多数网络服务要么由 `xinetd` 进程启动，要么由 `/etc/init.d` 目录中的启动脚本启动。

`xinetd` 是一个守护进程，它监听大量的网络端口号。当某个特定端口号建立连接时，`xinetd` 自动启动该服务的相应程序并将连接交给它。`xinetd` 守护进程通过提供包括更灵活访问控制、更多日志设置和拒绝服务防御在内的特性，改进了其前身 `inetd`。

配置文件 `/etc/xinetd.conf` 用于为 `xinetd` 服务器提供默认设置。目录 `/etc/xinetd.d` 包含告知 `xinetd` 监听哪些端口以及启动哪些程序的文件。每个文件包含单个服务的配置信息，文件名通常以其配置的服务命名。例如，要启用 `rsync` 服务，请编辑 `/etc/xinetd.d` 目录中的 `rsvc` 文件，并查找类似于以下内容的部分：

```
service rsvc
{
    disable = yes
    socket_type = stream
    wait = no
    user = root
    server = /usr/bin/rsync
    server_args = --daemon
    log_on_failure += USERID
}
```

请注意，此示例的第一行将该服务标识为 `rsvc`。这与 `/etc/services` 文件中列出的服务名称完全匹配，使该服务监听 `TCP` 和 `UDP` 协议的 873 端口。您可以看到该服务默认是关闭的（`disable = yes`）。要启用该服务，请将该行更改为如下形式：

```
disable = no
```

> **注意** *如果您的机器是 `FTP` 服务器，那么开启 `rsvc` 服务是一个不错的选择。它允许人们使用 `rsvc` 客户端（包含校验和搜索算法）从您的服务器下载文件。借助该特性，用户可以在下载中断后重新开始下载，而无需从头开始。*

由于大多数服务默认都是禁用的，您的计算机的不安全性仅取决于您如何配置它。您可以双重检查不安全的 服务，如 `rlogin` 和 `rsh`（它们包含在 `rsh-server` 软件包中），通过在 `/etc/xinetd.d/rlogin` 和 `rsh` 文件中确保设置 `disable = yes` 来验证它们也是被禁用的。

> **提示** *您可以使远程登录服务处于活动状态，但禁用 `/etc/hosts.equiv` 和 `.rhosts` 文件的使用，要求 `rlogin` 始终提示输入密码。与其禁用服务，不如找到 `rsh` 文件中的 `server` 行（`server = /usr/sbin/rshd`），并在末尾添加空格后跟上 `-L`。当然，这并不能改变您的密码和数据仍将通过网络未加密发送的事实。*

现在您需要向 `xinetd` 进程发送一个信号，以告知其重新加载配置文件。做到这一点的最快速方法是重新加载 `xinetd` 服务。请以 `root` 用户身份，在 `shell` 中输入以下内容：

```
###### service xinetd reload
Reloading configuration:        [  OK  ]
```

就这样——您已启用 `rsync` 服务。假设您已正确配置了 `FTP` 服务器（参见第 19 章），现在客户端应能够通过 `rsync` 协议从您的计算机下载文件，并能够恢复中断的下载。
