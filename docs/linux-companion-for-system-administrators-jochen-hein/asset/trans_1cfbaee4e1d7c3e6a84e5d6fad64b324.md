

# 网络管理程序 531

## 使用 spray 进行性能测量

spray 程序可以用于相对简单的方法确定网络上的可能吞吐量。在某一台计算机上，必须启动 sprayd 守护进程。随后，你可以使用 spray 测试与该计算机的连接。数据包通过 UDP 协议传输。

如果你知道空闲网络和正常负载网络的数值，你可能对网络状态有一个了解。请记住，使用此程序时，你可能会干扰其他用户的工作，因为网络处于完全满载状态。最后，spray 程序会显示发送和接收数据包的统计概述。通过 -cs 和 -l 选项，可以设置数据包的数量和大小。更多选项请参见帮助页（man page）。

列表 24.6 显示了 spray 的示例输出。程序仅运行了短时间，以避免干扰网络中的其他用户。请注意，对于这里介绍的许多程序，你实际上可以大幅增加网络负载，加剧这种情况。

```
(Linux:> spray pea
sending 1162 packets of length 86 to pea...
in 2.36 seconds elapsed time,
0 packets (0.00%) dropped.
Sent: 491 packets/sec, 42.3 KBytes/sec
Recvd: 523 packets/sec, 45.0 KBytes/sec
```
列表 24.6 spray 程序。

spray 使用 UDP 作为协议。这不能保证数据包的可靠传输，且测量取决于两台计算机之间的速度差异。因此，基于 TCP 的 tcpspray 更适合对网络性能做出有意义的判断。

| 附加信息和来源 |
| :--- |
| 帮助页: spray(8), sprayd(8) |
| ftp 服务器: tsx-11.mit.edu |
| ftp 服务器: /pub/linux/packages/net/attic/Other |
| 文件名: spray-1.0.tar.gz |
| 大小:  12 KBytes |

## 使用 tcpspray 进行性能测量

作为 spray 的替代方案，你也可以使用 tcpspray。在这里，使用 TCP 进行数据传输而非 UDP。同样，上述所有注意事项均适用。作为 532 网络管理的对应程序，tcpspray 使用指定为参数的计算机上 inetd 的内部丢弃服务。或者，如果你指定选项 -e，你也可以使用 echo 端口。

| 附加信息和来源 |
| :--- | :--- |
| 帮助页: tcpspray(1) |
| ftp 服务器: sunsite.unc.edu |
| ftp 服务器: /pub/linux/system/network/admin |
| 文件名: tcpspray-1.la.tar.gz |
| 大小: 约 12 Kbytes |

## 24.2.3 TCP 服务测试

测试 TCP 服务，你可以使用 telnet 程序。要做到这一点，你必须直接对所需的端口建立连接，之后就可以直接测试该服务。我们建议先尝试运行 telnet localhost smtp。如果你知道该协议的工作原理（在 [rfc0821] 中定义），你现在就可以手动测试此服务了。

通常可以在不同的端口下启动新版本的守护进程，并在替换旧版本之前对其进行检查。如果系统已被用户占用，应注意尽可能让此类更改对用户的影响最小化。

列表 24.7 显示了 POP3 服务器简单测试示例。POP3 服务器用于让用户从远程机器访问其邮箱箱（人们现在正在迁移到 IMAP（互联网消息访问协议），但为了本例的目的，我们坚持使用 POP3）。请注意，密码是透明传输的（通过 ssh 连接的安全性感知隧道型 POP3）。有时你会看到被 ssh 错误解释的消息，或者指示客户端未正确显示的错误。如果所有尝试都失败了，你可以查阅相应 RFC 中的协议描述来操作。

```
(Linux):# telnet localhost pop
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
+OK POP3 localhost v6.50 server ready
user jochen
+OK User name accepted, password please
pass password
+OK Mailbox open, 0 messages
quit
+OK Sayonara
Connection closed by foreign host.
```
**列表 24.7** 使用 *telnet* 对 POP3 服务器进行测试。

## 24.2.4 RPC 服务故障检测

当你使用 RPC 服务时，除了上述提到的问题外，还会发生额外的错误。首先，你应该检查端口映射器（port mapper）是否正在运行。随后，你可以使用 `rpcinfo -p hostname` 找出哪些服务注册到了端口映射器。最后一步，你可以通过 `rpcinfo -u hostname` 服务测试各个守护进程。

## 24.2.5 网络文件系统

网络文件系统（NFS）基于 RPC，因此你应该首先检查与 RPC 服务相关的上述项目。你可以使用 `showmount` 程序确定该计算机导出了哪些卷。你还可以发现哪些客户端挂载了目录。
如果你通过 NFS 的数据吞吐量遇到问题，可以尝试将读写访问的缓冲区大小分别增加到 4 和 8 Kbytes。这通常会导致读写速度的显著提高。

## 24.2.6 网络统计

通过 `Netstat` 或 `tcptop` 程序可以获得类似于 `top` 输出的网络负载统计显示。你将在下方提到的 ftp 服务器上找到一些额外的程序。

| 附加信息和来源 |
| :--- | :--- |
| 帮助页: tcptop(1) |
| ftp 服务器: sunsite.unc.edu |
| ftp 服务器: /pub/Linux/system/network/admin |
| 文件名: netstat |
| 大小: 约 4 Kbytes |

## 24.3 IP 网络管理

在许多公司中，IP 网络通过借助 SNMP（简单网络管理协议 [rfc1157]）进行管理。每个用 SNMP 管理的设备（包括工作站、路由器、交换机、打印机等）都在管理信息库（MIB）中组织其信息。MIB 定义在互联网标准 [rfc1441|rfc1450] 中。除了设备上的（静态）信息（例如负责人），还管理动态数据。对 MIB 中信息的访问通过团体（Community）进行管理。默认团体是 public，允许读取访问。数据的修改应允许另一个团体进行。此外，将 MIB 的访问限制在管理站的 IP 地址可能是明智的。

设备可以通过 SNMP Trap 向网络控制台注册并触发不同的操作。然而，异构网络的一个很大缺点是仅包含 IP 设备。无法处理其他协议，因此你可能为此需要额外的工具。

## 作为 SNMP 客户端的 Linux

可用的 Linux 包是卡内梅隆大学（CMU）的 snmp 包。它可以调用 Linux 计算机上的各种信息。这些信息从数据连接扩展到 CPU 负载或磁盘占用情况。

## 用于网络管理的 Linux

在布伦瑞工业大学，开发了 tkined 包用于 SNMP 网络管理。该程序包使用 Tcl/Tk 编写（带有网络访问扩展）；源代码可以在布伦瑞工业大学的 ftp 服务器上找到。

通过该程序，你可以生成网络地图。基于此地图，你可以执行各种管理任务并创建统计（以及图形）。该工具是 IBM、Sun 或 HP 等可用软件包的廉价替代方案。

图 24.1 显示了简单的地图表示。中心由一台交换机组成，连接不同的网段。在这里，这些网段以图标表示，需要时可以展开；然后就可以访问该网段的所有设备。在这里，每个网段关联了网络负载的统计表示。

![](img/ad3b0471a5d608a011338d028bec5422_554_0.png)
图 24.1 使用 mrtg 进行网络流量的可视化。

如果你只需要一个绘制网络使用情况精美图形的工具，可以使用 mrtg（多路由器流量图生成器）。你可以在配置文件中定义哪些值将被测量和绘图（an

