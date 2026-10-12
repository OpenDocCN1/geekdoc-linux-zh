
```
0.0.0.0.68 > 255.255.255.255.67: ... DHCP:DISCOVER...
212.140.133.22.67 > 255.255.255.255.68: ... DHCP:OFFER...
0.0.0.0.68 > 255.255.255.255.67: DHCP:REQUEST...
212.140.133.22.67 > 255.255.255.255.68: ... DHCP:ACK...
```

下面是一个完整的 `tcpdump` 跟踪，经过大量编辑：

由于数据包中有许多不同的字段，查看详细信息时 `ethereal` 比 `tcpdump` 更好。（参见网络附录 19，其中列出了 DHCP 字段以及 `tcpdump` 使用的缩写。）`ethereal` 将 DHCP 详细信息显示为 `Bootstrap Protocol (BOOTP)`，许多文档和你的 services 文件将 DHCP 端口显示为“BOOTP 服务器”和“BOOTP 客户端”或类似的缩写。如注释部分所述，这是因为 DHCP 是 BOOTP 的扩展，并且与其向后兼容。

`以太瑞`（`ethereal`）追踪（图 16.3）说明了该会话的几个特征：

- 1. 每个数据包都指定其消息类型（`DISCOVER`、`OFFER`、`REQUEST` 或 `ACK`）

- 2. 客户端在其初始请求中将它的 *客户标识符* 包含在发往服务器的以太网地址中。由于以太网地址是全局唯一的，因此这能唯一标识客户主计算机

- 3. 客户端发送一个 *参数请求* 列表，指示其需要数值的网络设置。在客户端和服务器之间，DHCP 在请求和应答数据包的选项中，使用 *选项编号*（而非字母名称）定义在 DHCP RFC 中，并在 Web 附录 19 中汇总了这些选项编号

客户端请求的选项列表取决于其所使用的 DHCP 客户机软件。图 16.3 中的客户端是 Windows-NT 服务器，因此它请求的参数包括 NetBIOS（Windows 网络）设置。Linux 客户端将请求不同的集合

- 4. 客户端可以保留一些有关其配置的信息，这些信息要么来自以前的 DHCP 会话，要么，如本例所示，来自手动配置：主机名 **TIMEPCNT** 是通过 **控制面板 > 网络** 进行手动配置的。

```
☐ User Datagram Protocol
☐ Bootstrap Protocol
	Boot Request
Hardware type: Ethernet
Hardware address length: 6
Hops: 0
Transaction ID: 0x4407d141
Seconds elapsed: 0
Broadcast flag: 0
Client IP address: 0.0.0.0 (0.0.0.0)
Your (client) IP address: 0.0.0.0 (0.0.0.0)
Next server IP address: 0.0.0.0 (0.0.0.0)
Relay agent IP address: 0.0.0.0 (0.0.0.0)
Client hardware address: 00:50:da:e4:61:34
Server host name not given
Boot file name not given
Magic cookie: (OK)
Option 53: DHCP Message Type = DHCP Discover
☐ Option 61: Client identifier
Hardware type: Ethernet
Client hardware address: 00:50:da:e4:61:34
Option 12: Host Name = **TIMEPCNT**
☐ Option 55: Parameter Request List
1 = Subnet Mask
15 = Domain Name
3 = Router
44 = NetBIOS over TCP/IP Name Server
46 = NetBIOS over TCP/IP Node Type
47 = NetBIOS over TCP/IP Scope
6 = Domain Name Server
End Option
Padding
```

![](img/a2132b646d336d5f9a21102d6320e537_442_0.png)

![](img/a2132b646d336d5f9a21102d6320e537_442_1.png)

**图 16.3** DHCP 请求的 **以太瑞**（`ethereal`）跟踪

在下一个模块中，我们将查看客户端/服务器交互的其余部分。

### 16.3 动态主机配置协议是如何工作的（2）

上一个模块描述了客户端发送到服务器的初始 `DHCPDISCOVER` 请求。以下是服务器的 `DHCPOFFER` 回复：

```
Client IP address: 0.0.0.0 (0.0.0.0)
Your (client) IP address: 212.140.133.85 (212.140.133.85)
Next server IP address: 0.0.0.0 (0.0.0.0)
Relay agent IP address: 0.0.0.0 (0.0.0.0)
Client hardware address: 00:50:da:e4:61:34
Server host name not given
Boot file name not given
Magic cookie: (OK)
Option 53: DHCP Message Type = DHCP Offer
Option 1: Subnet Mask = 255.255.255.128
Option 58: Renewal Time Value = 1 day, 12 hours
Option 59: Rebinding Time Value = 2 days, 15 hours
Option 51: IP Address Lease Time = 3 days
Option 54: Server Identifier = 212.140.133.22
Option 15: Domain Name = uit.co.uk
Option 3: Router = 212.140.133.29
Option 6: Domain Name Server = 212.140.133.19
End Option
Padding
```

- 1. 服务器正在提供地址 212.140.133.85（**您的（客户端）IP 地址** 字段。）

- 2. 服务器填写了客户端请求的选项值

- 3. 客户端不会永久获得 IP 地址：它只获得了固定期限的 *租约*。（租约时长通常是服务器上的配置选项。）服务器回复租约的持续时间以及 *更新的时间*，在此时间点客户端应再次联系该服务器，询问是否可以更新（即延长）租约。这使客户端可以尽可能长时间地保留相同的 IP 地址。服务器还指定一个 *重绑定时间*：如果客户端无法从原服务器更新租约，在到达重绑定时间后，它应尝试从任何可用的 DHCP 服务器更新其在此 IP 地址上的租约。

当客户端收到 `DHCPOFFER` 后，它通过发送 `DHCPREQUEST` 向该服务器确认其希望使用该地址。最后，服务器用 `DHCPACK` 确认这一操作，并记录该客户端现在拥有此 IP 地址的租约。在收到 `DHCPACK` 后，客户端将其网络参数设置为服务器赋予的值。

我们尚未展示 `DHCPREQUEST` 和 `DHCPACK` 数据包的详细内容——除了消息类型字段外，它们几乎与其他数据包完全相同。

> 练习：使用 `以太瑞`（`ethereal`）来查看 DHCP 会话中的所有四个数据包。

# 动态主机配置协议每次尽可能为同一客户端分配相同的 IP 地址

虽然 DHCP 地址分配自动化的工作至关重要，但在专用网络上，即使机器重启，希望各个机器始终保持相同的 IP 地址，这是可取的，因为许多日志记录机制使用 IP 地址来识别用户或部门。DHCP 通过几种方式促进这一目标：

- 如上所述，客户端定期更新其 IP 地址的租约，从而至少在重启前保持相同的地址。租约更新仅由两个数据包组成，即 `DHCPREQUEST` 和 `DHCPACK`。如下文所示，这些数据包不是广播的：客户端和服务器都具有有效的 IP 地址，因此可以正常通信：

  - 212.140.133.85.68 > 212.140.133.22.67:... c:212.140.133.85 `DHCPREQUEST` ...

  - 212.140.133.22.67 > 212.140.133.85.68:... `DHCPACK` ...

- 当现有租约正在更新，或者客户端拥有上次租约的记录时，它可以尝试进行更简短的会话。客户端发送 `DHCPREQUEST`（而不是通常的 `DHCPDISCOVER`）作为开始，其中包含其先前租约的详细信息。如果同一服务器愿意让客户端拥有相同的租约，它将回复 `DHCPACK`，使用仅两个（如下所示）数据包就完成会话，而完整会话通常使用四个数据包。
