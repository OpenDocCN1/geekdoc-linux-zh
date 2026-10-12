
## 拨号服务器的代理 ARP

在图 26.30 所示的网络中，当远程笔记本电脑连接上时，局域网（LAN）上的其他计算机如何将这些笔记本电脑作为目标路由数据包？

我们可以在所有局域网 PC 或默认网关（如果有的话，但图中所示网络并没有）上设置显式的路由表项，但这会非常繁琐。而且，如果拨号 PC 被分配动态地址，我们本来也没法这样做。一个更优雅的方案是，拨入服务器为其当前连接的任何笔记本电脑提供**代理 ARP**。假设我们的局域网是 192.0.2.*，并且范围 192.0.2.180 - 199 专门用于拨号服务器分配给其拨入客户端，如图 26.30 所示。Alice 想要与 Bob 通信。她知道他的地址；她的数据包（源地址为 192.0.2.188）通过拨入服务器路由到 Bob。现在 Bob 必须回复。他针对 192.0.2.188 没有特殊的路由表项——它只是直接连接的局域网的一部分——所以 Bob 会对 Alice 进行 ARP 请求。巧妙之处在于：拨入服务器知道 192.0.2.188 连接在它身上，所以*拨入服务器*向 Bob 发送 ARP 响应，其中包含拨入服务器的 MAC 地址。Bob 然后将发给 Alice 的数据包发送给拨入服务器，完全不知道服务器正在充当路由器。当服务器收到发给 Alice 的数据包时，它会通过拨号链路将它们转发给 Alice。

## 搭建测试“拨号”系统

你可以通过以下两种方法搭建一个测试 PPP 网络，以避免产生高额话费：

- 使用两个调制解调器，分别连接到同一办公室内的两个内部电话分机上——理想情况下都在你的办公桌上。不要拨打收费电话，而是从一个分机拨打另一个分机。
- 使用直接的串行电缆代替调制解调器和电话，将拨号客户端与拨入服务器连接起来。这样不会占用任何电话分机，你可以在家里使用（那里通常没有多个私有分机）。你需要注意以下几点：
  - 你必须使用特殊的*空口*（null-modem）电缆，或带有空口附件的直通电缆，来连接这两个系统。空口电缆完全不包含电子元件——它只是交叉电缆中的一些线并将一些引脚连接起来，使其对计算机看起来像一个真实的调制解调器（附录 7）。
  - 这种连接的行为并不完全等同于调制解调器/调制解调器链路。如果你的用户经常使用调制解调器，最好也在测试时使用调制解调器，因此使用上述第 (1) 点中的两个内部分机方案。

要设置此配置，你需要某种 PPP 服务器。最容易设置的是 NT 上的 RAS 服务器，因为你已经完成了 RAS 拨出部分的大多数安装工作。请参阅“注释”部分获取更多信息。

## 摘要

- 拨号连接是点对点（point to point）的。如今它们使用 PPP 连接到 ISP 或其他拨入服务器。
- 对于基本拨号——仅用于浏览网页、电子邮件等——标准 Windows 拨号软件允许你配置所有所需的网络设置。
- NT 的拨号网络监视器（Dial-Up Networking Monitor）提供有关连接状态的信息。
- 建立拨号连接会自动创建额外的路由表项。当你断开连接时，这些表项会自动移除。
- 如果你通过拨号接入 ISP 以连接到办公室的 Windows 网络 LAN，则需要额外的配置。你必须：
  - 设置你笔记本电脑的 NT 域。
  - 使用 WINS（或至少使用 **Lmhosts** 文件）以便 NetBIOS 名称解析和浏览功能在路由网络上正常工作。

最好在通过拨号尝试之前，先在局域网内和路由器后方测试你的笔记本电脑，以确保你的 Windows 网络配置是正确的。

- 如果你有时将笔记本电脑直接连接到内部局域网，有时通过 ISP 拨号，你应该创建一个硬件配置文件（Hardware Profile），以便在拨号时（且断开局域网连接时），笔记本电脑不会尝试通过 PC 的网卡发送数据包。

## 接下来是什么？

在下一章中，我们将探讨 VPN，它通过加密流量来保护你的拨号连接以及分支办公室之间的连接。

## 注释与延伸阅读

对于经常在办公室和家之间移动的笔记本电脑，无线组网很方便（如果你的办公室支持的话），特别是如果你家里也有局域网。

PPP 的前身是 SLIP（*Serial Line IP*）。SLIP 仅支持 IP，而 PPP 可以在同一链路上同时支持多种协议。与 PPP 不同，SLIP 链路两端的 IP 地址必须硬编码。SLIP 现在几乎完全被 PPP 取代。有关 SLIP 的更多信息（以及 PPP 的一些细节），请参阅 Stevens Modules 2.4–2.6。

- **RFC-1161 1994年7月** *The Point-to-Point Protocol (PPP)*（点对点协议）

Van Jacobson 头部压缩：

- **RFC-1144 1990年2月** *Compressing TCP/IP Headers for Low-Speed Serial Links*（压缩低速串行链路上的 TCP/IP 头部）

（顺便说一下，Van Jacobson 是 **tcpdump** 的原始开发者之一。）

- RFC-2507 1999年2月 *IP Header Compression*（IP 头部压缩）
- RFC-2508 1999年2月 *Compressing IP/UDP/RTP Headers for Low-Speed Serial Links*（压缩低速串行链路上的 IP/UDP/RTP 头部）
- RFC-2509 1999年2月 *IP Header Compression over PPP*（PPP 上的 IP 头部压缩）

## 调制解调器故障排除

请参阅以下网站的故障排除链接：

- http://www.modemsite.com/
- http://www.56k.com
- http://www.modemhelp.org

以及关于 US Robotics 调制解调器的详细论文：

- http://infodeli.3com.com/docs/rapd/x2shoot4.pdf

## 拨号网络故障排除

Microsoft 的拨号网络错误消息列表如下：

- [Remote Access Service (RAS) Error Code List (Q163111)](https://support.microsoft.com/en-us/kb/163111) （远程访问服务 (RAS) 错误代码列表）

或者，你可以在我们的网站上查找错误：

- [www.uit.co.uk/resources > RAS errors](https://www.uit.co.uk/resources/) （RAS 错误）

这将提供更完整的错误解释及其可能的原因。

模块 26.11 提供了关于如何防止你“在局域网中”的网络设置在从家拨号到办公室网络时发生干扰的建议。相反的问题通常发生在你在办公室并使用 VPN 时。当你回到办公室并将机器连接到局域网时，你无法连接到任何本地机器，即使你已经选择了正确的硬件配置文件（如果你设置过它们）。发生的情况是，你笔记本电脑上的 VPN 软件正在加密你的数据包，并试图将它们发送到 VPN 盒子以转发到目的地。请参阅模块 27.9 了解如何克服这一问题。

Windows 网络监视器*确实*可以在拨号连接上工作。然而，你至少目前无法在 Windows-NT 和 Windows-2000 的串行连接上使用 Windump（或 *ethereal*）：

- [http://netgroup-serv.polito.it/windump/misc/faq.htm](http://netgroup-serv.polito.it/windump/misc/faq.htm)

在仅使用拨号的机器上使用网络监视器非常简单——它默认监控拨号接口，所以你只需像往常一样启动程序即可。但是，如果你同时拥有拨号和以太网接口，并希望监控拨号流量，你必须明确告诉 Netmon 使用拨号接口。选择菜单 **Capture > Networks** … 以打开 **Select Capture Network**（如下所示）。选择拨号接口，该接口的 **Current Address**（当前地址）全为零。

![](img/a2132b646d336d5f9a21102d6320e537_717_0.png)

你还必须更改捕获过滤器（菜单 **Capture > Filter ...**，如下所示），因为 Netmon 已将默认过滤器设置为适合局域网接口，而不是拨号接口。使用 **Delete Line**（删除行）按钮，删除 “INCLUDE *$basename* (ETHERNET)<->*ANY,” 这一行，或者将其更改为 “INCLUDE *ANY*<->*ANY*”。

![](img/a2132b646d336d5f9a21102d6320e537_717_1.png)

## 什么是 NdisWan 适配器

回顾模块 18.5，Windows-NT 绑定将 NT 服务与协议族绑定到适配器。由于拨号网络没有物理适配器（网卡），NT 创建了“伪适配器”用于绑定，这些被称为 NdisWan。你可以有多个 NdisWan；事实上，当你安装 RAS 并启用拨入和拨出时，你会看到创建了两个 NdisWan，一个用于拨入，一个用于拨出。（NdisWan 中的“Ndis”部分代表“Network Driver Interface Specification”（网络驱动程序接口规范）——这是 NT 在物理网卡和操作系统较低层之间使用的低级接口。）

## 构建测试网络

有关在 NT 上设置 RAS 服务器的详细信息，请参阅 Web 附录 31。

## Linux 上的拨号

- [http://www.linuxdoc.org/HOWTO/Serial-HOWTO.html](http://www.linuxdoc.org/HOWTO/Serial-HOWTO.html)
- [http://www.linuxdoc.org/HOWTO/Modem-HOWTO.html](http://www.linuxdoc.org/HOWTO/Modem-HOWTO.html)
- [http://www.stokely.com/unix.serial.port.resources/ppp.slip.html](http://www.stokely.com/unix.serial.port.resources/ppp.slip.html) “*UNIX Serial Port Resources*”（UNIX 串行端口资源）
- [http://www.vlug.org/linux/links/Networking/PPP_=_SLIP/](http://www.vlug.org/linux/links/Networking/PPP_=_SLIP/) 关于 PPP 和 SLIP 的许多链接

以及关于设置直接串行电缆连接：

- [http://www.linuxdoc.org/HOWTO/Serial-Laplink-HOWTO/index.html](http://www.linuxdoc.org/HOWTO/Serial-Laplink-HOWTO/index.html)

