
以下 CLI 命令将每个文件从 flash 分区复制到 IP 地址为 `192.168.240.31` 的 FTP 服务器。FTP 用户账户为 `david`，文件将复制到 `/ftp-files` 文件夹。文件也被重命名为包含日期（`controlpath-2017-09.gz` 和 `datapath-2017-09.gz`）。

```bash
#copy flash:controlpath-pcap.gz ftp:192.168.240.31 david/ftp-files controlpath-2017-09.gz
#copy flash:datapath-pcap.gz ftp:192.168.240.31 david/ftp-files datapath-2017-09.gz
```

通过日志文件复制控制路径和数据路径文件的最后方法。生成的日志文件并包含 `tech-support` 信息。生成的文件 `logs.tar` 必须通过 FTP 或 TFTP 复制到你的计算机。要使用数据包分析器查看捕获的数据，必须在文件位于计算机后对其进行解压缩并提取。然后可以使用数据包分析软件打开 pcap 捕获文件。以下 CLI 输出显示了创建日志文件的命令，随后是将文件传输到 FTP 服务器的命令。在示例中，日志文件被重命名为包含日期。

```bash
#tar logs-support
此操作可能需要一些时间，请不要重启设备
#copy flash:logs.tar ftp:192.168.240.31 david/ftp-files logs-9.tar
```

当日志文件复制到本地磁盘后，需要使用本地计算机上提供的压缩软件提取内容。此时，包含控制路径捕获的文件为 `/var/log/oslog/filter.pcap`，包含数据路径捕获的文件为 `/var/log/oslog/datapath.pcap`。找到这些文件后，可以使用 Omnipeek 或 Wireshark 等数据包分析软件打开它们。在某些时候，你可能想从控制器文件系统中删除这两个捕获文件的内容。以下两个 CLI 命令删除这些文件：

```bash
#packet-capture reset-pcap controlpath-pcap
#packet-capture reset-pcap datapath-pcap
```

## packet-capture-defaults

在本章之前，你已经了解到数据包捕获配置设置没有作为控制器运行配置的一部分存储。尽管事实如此，但通过 `packet-capture-defaults` 命令可以在控制器重启时保留数据包捕获设置。

这些默认设置是每个控制器的本地设置，不在主控制器与其本地控制器之间共享。任何时候都可以使用 `packet-capture` 命令覆盖默认设置。

`packet-capture-defaults` 命令允许配置控制路径和数据路径捕获参数，以及指定捕获目的的能力。`packet-capture-defaults` 命令的功能与 `packet-capture` 命令相同，增加了重启期间保留设置的功能。

以下 `packet-capture-default` 命令组与本章早前的 `packet-capture` 命令相当。第一个命令定义了数据路径捕获的输出目标。这是必要的，因为执行 IPsec 捕获时，数据无法发送到控制器的内部文件系统。以下 CLI 输出的第二个命令开启对 IPsec 节点 `10.1.80.100` 的数据路径流量的数据包捕获。第三个命令开启 MAC 地址为 `00:24:D7:6A:71:24` 的无线客户端加密流量捕获。`show packet-capture` 命令显示当前配置。最后两个命令禁用这些设置。

```bash
#configure terminal
输入配置命令，每行一个。以 CNTL/Z 结束
(config) #packet-capture-defaults destination ip-address 192.168.240.31
(config) #packet-capture-defaults datapath ipsec 10.1.80.100
(config) #packet-capture-defaults datapath wifi-client 00:24:D7:6A:71:24 decrypted
(config) #show packet-capture-defaults

Default Capture Destination
\---------------------------
Destination IP 192.168.240.31

Default Capture (Controlpath)
\-----------------------------
Interprocess Disabled
Sysmsg Disabled
TCP Disabled
UDP Disabled
Other Disabled

Default Capture (Datapath)
\--------------------------
Wifi-Client Enabled Mac: 00:24:d7:6a:71:24 Filter: Decrypted
Ipsec Enabled Peer: 10.1.80.100
(config) #no packet-capture-defaults datapath ipsec
(config) #no packet-capture-defaults datapath wifi-client
```

## 防火墙镜像

到本章为止，你已经学习了使用端口监控进行数据包捕获，以及使用 `packet-capture` 命令在控制器内部捕获数据包。下一种数据包捕获方法使用

使用控制器的防火墙来指定捕获哪些数据。该机制利用防火墙规则来镜像感兴趣的数据，因此被称为*防火墙镜像*（firewall mirroring）。这些数据被镜像到一个 IP 地址。

通常无法捕获用户数据，因为数据是加密的。当无线客户端发送帧时，客户端首先对要发送的数据进行加密，然后在加密数据上添加 802.11 头部。随后，客户端将此帧传输到 AP。AP 将该帧封装在 802.3 帧内部并将其转发到控制器。

当控制器接收到此帧时，它首先剥离 802.3 头部并将其丢弃。接着控制器获取 802.11 头部，并提取层 2 源地址和目的地址。此时，剩余的是加密数据（假设已启用加密）。控制器解密这些数据，得到原始明文内容。控制器随后获取层 2 源地址、层 2 目的地址以及数据，并将其转发到防火墙进程，以根据防火墙规则进行评估。防火墙规则决定了对该帧执行什么操作。

在第 8 章“策略执行防火墙”中，你学习了防火墙规则会对每个帧执行某种操作（通常是允许或拒绝帧继续在网络中传输）。除了对每个帧执行操作外，防火墙规则还可以配置为执行可选的扩展操作——即额外的功能或任务。这些扩展操作之一就是防火墙镜像。

如果提取的帧匹配了已启用镜像的防火墙规则，那么不仅会执行防火墙操作，帧的副本（层 2 源地址、层 2 目的地址和解密数据）还将转发（镜像）到由 `packet-capture destination ip-address 1.2.3.4` 命令定义的目的地。当启用防火墙镜像时，数据包捕获目的必须设置为 IP 地址。

请注意，在 ArubaOS 的早期版本（ArubaOS 6.3 之前）中，防火墙镜像目的被定义为防火墙命令的一部分。现在不再如此。防火墙镜像目的现在使用 `packet-capture` 命令指定。

镜像的防火墙帧将被封装在 GRE 隧道中并发送到目的 IP 地址。每个帧将被封装在 GRE 帧中，并跨网络传输到执行分析的计算机。大多数数据包分析软件能够识别 GRE 头部为传输方法，并简单地将其剥离丢弃，从而让分析专注于有效负载。

防火墙镜像的一个非常好的特性是，它允许你针对正在捕获的数据。防火墙策略通过用户角色应用，允许规则细粒化，捕获特定的帧集合。

### AP/AM 捕获

将解释的最后一种捕获方法是使用 AP 或空中监控（AM）作为 RF 监听设备进行捕获。这种方法允许你选择网络上的一个 AP 或 AM，配置其监听无线传输，并将听到的信息发送到配置了数据包分析的计算机。这与使用 `packet-capture` 命令不同；你很快就会了解到其中的区别。

如果你曾经在 802.3/以太网网络上执行过数据包捕获，你就知道为了正确捕获所有数据，需要将适配器设置为混杂模式（promiscuous mode）。默认情况下，以太网适配器只监听直接指向适配器地址的广播、组播和单播帧。混杂模式允许以太网适配器捕获看到的任何帧，无论这些帧是否是针对该设备的。

从笔记本电脑执行无线捕获时，无线适配器通常连接到特定通道上的 SSID，并且类似于以太网适配器，它只监听直接指向它的广播、组播和单播帧。无线适配器需要被设置为所谓的 RF 监控模式（RF monitor mode，类似于混杂模式），以便能够捕获听到的所有无线帧。这种数据包捕获方法允许你捕获 802.11 管理帧和控制帧，包括信标（beacons）、ACK、探测请求和响应以及 RTS/CTS 等。
