
当不带任何参数调用时，`ifconfig` 会显示当前活动网络接口的状态。如果给定一个接口参数，则仅显示该接口的状态。如果使用 `-a` 选项调用，则显示所有接口的状态，包括已停用的接口。

下面显示了 `ifconfig -a` 的示例输出：

```text
# /sbin/ifconfig -a
eth0      Link encap:Ethernet  HWaddr 00:80:5F:6D:CF:C2
          inet addr:10.2.0.244  Bcast:10.2.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:4261292 errors:0 dropped:0 overruns:0 frame:0
          TX packets:4363313 errors:0 dropped:0 overruns:0 carrier:0
```

```
lo
        collisions:0 txqueuelen:100
        Interrupt:5 Base address:0x6000
        Link encap:Local Loopback
        inet addr:127.0.0.1 Mask:255.0.0.0
        UP LOOPBACK RUNNING MTU:3924 Metric:1
        RX packets:48474 errors:0 dropped:0 overruns:0 frame:0
        TX packets:48474 errors:0 dropped:0 overruns:0 carrier:0
        collisions:0 txqueuelen:0
```

第一行显示接口名称（此处为 `eth0`）、封装方法和以太网硬件地址。第二行显示接口的 IP 地址、子网掩码和广播地址。第三行显示接口的状态（UP 或 DOWN）。其后各行给出接收和发送数据包的统计信息以及错误计数器。

一些常见的接口配置问题是使用了错误的子网掩码或 IP 地址。如果两个系统意外配置了相同的 IP 地址，就会出现一种非常奇怪的情况。发往主机 A 的数据包会被冒名顶替者 B 截获。两个主机都无法正常工作。如果其中一台主机是某种服务器，并且有许多客户端连接，情况会变得严重得多。在这种情况下，所有试图连接到此服务器的应用程序都会出现长时间延迟。要排查此类问题，最合适的工具是 `arp` 命令，我们将在下一节中介绍它。

处理此类问题的一种方法是立即断开肇事系统的网络连接。这样网络就能恢复正常，更大的问题也就解决了。此外，您还必须删除重复机器的 `arp` 条目，并临时为合法系统添加一个静态条目。现在您应该能够检查并纠正肇事系统的 IP 地址了。

要将 `eth0` 的 IP 地址改为 `10.1.0.5`、子网掩码改为 `255.255.0.0`，可以使用以下步骤：

```
# ifconfig eth0 down
# ifconfig eth0 10.1.0.5 netmask 255.255.0.0
# ifconfig eth0 up
```

此外，您还应该更改本地 `/etc/hosts` 文件中的 IP 地址，并修正 NIS 和 DNS 数据库。

### 使用 arp

`arp` 命令显示 IP 地址到以太网 MAC 地址的转换。这使它成为一个极好的调试工具，因为您可以通过它跟踪 IP 地址与特定网络接口之间的关系。

例如，在上一节中，我们讨论了当 IP 地址被意外分配给两台机器时会发生什么情况。如果发生这种情况，系统会报告并记录重复 IP 地址错误。检查 IP 地址被其他系统盗用的系统上的 `/var/log/messages` 日志，应该会看到类似下面的条目：

```
Dec  6 14:42:56 saturn vmunix: duplicate IP address!!
sent from ethernet address 00:C0:4F:A9:F9:26
```

从这些信息中，我们可以确定重复的 IP 地址来自以太网地址为 `00:C0:4F:A9:F9:26` 的系统。

在尝试物理定位具有肇事网络接口的系统之前，第一步是删除 `saturn` 的包含错误以太网地址的虚假 `arp` 条目，并手动添加一个具有正确以太网地址的静态 `arp` 条目。这个静态 `arp` 条目不能被删除，并且可以防止发往 `saturn` 的数据包被传送到肇事主机。

这样，在您识别试图使用 `saturn` IP 地址的系统并修复该系统上的配置问题的同时，`saturn` 可以继续正常运行。

要删除 `saturn` 的 `arp` 条目，请使用 `arp` 命令的 `-d` 选项：

```
# arp -d saturn
```

要为 `saturn` 添加静态 `arp` 条目，请使用 `arp` 命令的 `-s` 标志：

```
# arp -s saturn 00:03:E3:C0:05:07
```

接下来，您可以使用 `arp` 命令的 `-a` 标志获取 `arp` 缓存中所有系统的列表，从而开始查找肇事系统：

```
# arp -a
vered (10.2.0.100) at 08:00:20:07:55:0C [ether] on eth0
linux (10.2.0.252) at 00:C4:AF:91:E9:11 [ether] on eth0
saturn (10.2.0.254) at 00:0E:01:6E:7F:81 [ether] on eth0
saturn (10.2.0.248) at 00:03:E3:C0:05:07 [ether] on eth0
cronus (10.2.0.249) at 00:80:F1:00:0C:33 [ether] on eth0
```

### 使用 nslookup

如果您在使用 `ping` 等命令时收到未知主机错误，但确信使用的主机名正确，那么您面临的是名称解析问题，需要修复 DNS 数据库中的错误。DNS 将在第 22 章“DNS”中详细讨论。

`nslookup` 命令允许您查询 DNS 服务器并查看其数据库的内容。您可以用它来检查数据库中存储的特定主机的值：

```
# nslookup cobra
Server:  bwdc001.bwc.org
Address:  10.0.0.2
*** bwdc001.bwc.org can't find cobra: Non-existent host/domain
```

在此示例输出中，`nslookup` 未能找到主机 `cobra` 的条目。以下输出是使用 `nslookup` 成功查找名称时的情况示例：

```
# nslookup saturn
Server:  bwdc001.bwc.org
Address:  10.0.0.2
Name:    saturn.bwc.org
Address:  10.2.0.248
```

> **注意：** 如果您在站点上除了使用 DNS 之外还使用 NIS，那么您还应该检查主机名是否也能通过 NIS 正确解析。为此，您需要使用第 6 章“验证用户和网络资源”中所述的 `ypmatch` 命令。

### 使用 tcpdump

`tcpdump` 是一个用于网络监控和数据采集的强大工具。该程序允许您生成有关网络流量的报告。它可以用来检查网络接口上与给定表达式匹配的数据包头部。但您应该注意，`tcpdump` 只能嗅探到达其网络接口的数据包。在使用共享介质或集线器的网络中，这不是问题。在交换式以太网环境中，它的有效性会大大降低，因为您只能看到广播数据包以及源自或发往运行 `tcpdump` 的主机的其他流量。无论如何，该工具仍然非常有用。

您可以使用此工具来排查网络问题、检测“ping 攻击”或监控网络活动。要获取完整的选项列表，请参阅 `tcpdump` 的手册页。

在这里，您将学习一些有关如何使用 `tcpdump` 收集有用网络流量信息的示例。在 Linux 中，您必须以 root 身份登录才能运行此 `tcpdump`。

> **警告：** 如果 `tcpdump` 以 setuid root 方式设置，则任何用户都可以运行它，但极不推荐这样做，因为这可能带来重大安全风险。该程序可能被滥用，以嗅探网络上的明文密码。

如果您不带任何参数调用 `tcpdump`，它将捕获网络上的所有数据包并显示它们。下面显示了 `tcpdump` 的一个小示例输出：
