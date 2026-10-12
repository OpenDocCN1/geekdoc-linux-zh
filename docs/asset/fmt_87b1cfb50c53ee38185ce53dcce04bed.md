
```
netstat -s

Ip:
      240762 total packets received
               0 forwarded
               0 incoming packets discarded
      246747 incoming packets delivered
      206940 requests sent out
          32 dropped because of missing route

Icmp:
          57 ICMP messages received
               0 input ICMP message failed.
ICMP input histogram:
          12 destination unreachable
          38 timeout in transit
               7 echo replies
           7 ICMP messages sent
               0 ICMP messages failed
ICMP output histogram:
               7 echo request

IcmpMsg:
InType0: 7
InType3: 12
InType1: 38
OutType8: 7

Tcp:
+   * 286 active connections
* passive connection openings
* failed connection attempts
* connection resets received
* connections established
* 239933 segments received
* 206091 segments sent out
* segments retransmitted
* bad segments received.
* resets sent

Udp:
+   * 757 packets received
* packets to unknown port received.
* packet receive errors
* 840 packets sent
* receive buffer errors
* send buffer errors

TcpExt:
+   * 219 TCP sockets finished time wait in fast timer
*       15 delayed acks sent
*       26 delayed acks further delayed because of locked socket
*       Quick ack mode was activated 1 times
*      229343 packet headers predicted
*      289 acknowledgments not containing data payload
*      301 predicted acknowledgments

TCPRCvCoalesce: 72755

IpExt:
+   * InRoutes: 2
* InMcastPkts: 13
* OutMcastPkts: 15
* InOctets: 410722578
* OutOctets: 8363083
* InMcastOctets: 2746
* OutMcastOctets: 2826
```

网络统计输出可以让你大致了解你的`Linux`系统在网络上的繁忙程度，或者安装的某个协议是否存在问题。

## 检查套接字 (Sockets)

`netstat`工具提供了丰富的网络信息，通常很难确定是哪个程序正在监听开放的端口。`ss`命令可以帮助你解决这个问题。

程序到端口的连接被称为套接字（`socket`）。`ss`命令可以帮助你关联哪些进程正在使用哪些活跃的网络套接字：

```
$ ss -anpt
State    Recv-Q  Send-Q  Local Address:Port      Peer Address:Port
LISTEN   0       100             127.0.0.1:25           *:*
LISTEN   0               :111                   *:*
LISTEN   0       5       192.168.122.153        *:*
LISTEN   0               :22                    *:*
LISTEN   0       128             127.0.0.1:631           *:*
LISTEN   0               :25                    *:*
LISTEN   0       128             :111                   *:*
LISTEN   0               :22                    *:*
LISTEN   0       128             :631                   *:*
ESTAB    0               :122                   ::1:40490
ESTAB    0       0               :1:40490               ::1:22
```

`users:(("ssh",pid=15176,fd=3))`

`-antpt`选项同时显示监听和已建立的`TCP`连接，以及它们相关的进程。此输出显示`ssh`端口（`22`端口）有一个已建立的连接，并由进程`ID`15176（即`ssh`程序）控制。

## 总结

如果你拥有正确的工具，将`Linux`系统连接到网络并不是件痛苦的事。要连接`Linux`系统，你需要一个`IP`地址、默认网关、主机名和`DNS`服务器。如果你不知道分配给系统的`IP`地址，可以使用`DHCP`自动获取这些值。

`Network Manager`是绝大多数`Linux`发行版中用于配置网络设置的最流行的图形化工具。它允许你从图形化窗口配置有线和无线网络设置。如果你必须从命令行配置网络设置，你需要使用几个工具。对于无线连接，使用``ifconfig``设置无线接入点和`SSID`密钥。对于有线和无线连接，均使用``ifconfig``或``ip``命令为接口设置`IP`地址和网络掩码值。你可以使用``route``命令定义本地网络的默认网关。

当网络配置完成后，你可能需要对网络问题进行额外的故障排除。``ping``和``ping6``命令允许你向远程主机发送`ICMP`包以测试基本连通性。如果你怀疑主机名存在问题，可以使用``host``和``dig``命令查询`DNS`服务器获取主机名。对于更高级的网络故障排除，你可以使用``netstat``和``ss``命令显示系统上哪些应用程序正在使用哪些网络端口。

## 考试要点

**描述用于配置和操作以太网网络接口所需的命令行工具。** 要在以太网接口上设置`IP`和掩码地址，使用``ifconfig``或``ip``命令。要为网络设置默认网关（`gateway`），使用``route``命令。某些安装了`Network Manager`的`Linux`发行版可以使用``nmtui``或``nmcli``命令，它们可以配置这三个值。

**解释如何配置对无线网络的的基本访问。**`Linux`使用``iw``命令列出网卡检测到的所有无线接入点。你可以使用``ifconfig``命令配置连接到特定无线网络的设置。至少，你需要配置接入点`SSID`值，并且必须指定加密密钥值以连接到接入点。

**描述如何操作 Linux 系统上的路由表。**``route``命令用于显示`Linux`系统使用的现有路由表。你可以使用``add``选项添加新路由，或使用``del``选项删除现有路由。通过命令中的``default``关键字指定网络的默认网关。

**总结用于分析网络设备状态所需的工具。**``ifconfig``和``ip``命令显示系统上所有网络接口的当前状态。你可以使用``netstat``或``ss``命令显示所有监听网络端口的统计信息。

**解释如何测试网络连通性。**``ping``和``ping6``命令允许你向远程主机发送`ICMP`消息并显示收到的响应。
