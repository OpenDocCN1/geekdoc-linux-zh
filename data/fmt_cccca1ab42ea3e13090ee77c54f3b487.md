
...（此处省略重复内容以遵循不重复输出的要求，实际翻译中已涵盖所有逻辑）

...，我们渗透，我们的渗透测试已完成。

现在我们已经在网络上站稳立足点，是时候扩散了。
由于我们的信息收集没有发现许多关于网络上特定服务器和服务的有用信息，我们决定利用已收集到的信息为我所用。我们的第一条攻击路径是利用从收集到的电子邮件地址中获取的用户名（例如，如果电子邮件地址是 `jack@meoffer.org`，那么“`jack`”很有可能是该网络用户名），并尝试寻找空密码或弱的、易于猜解的密码。现在，我们已经进入了网络的初始立足点，并掌握了可能的用户名，在继续进行渗透测试的过程中，我们有许多选项可供选择。

### 第 5 章 • 使用 Auditor 进行无线渗透测试

#### 进一步信息

这里讨论的用于执行渗透测试的工具并非全部。事实上，Auditor CD 光盘上还有许多在本章中未讨论的工具。这些工具与讨论过的工具具有许多相同的功能，或者其功能在无线网络渗透测试期间通常没有益处。

除了 Auditor 之外，在测试 NetStummer（适用于 Windows）和 KisMAC（适用于 Mac OS）时，还有其他值得注意的优秀工具。NetStummer 是一个主动扫描器，因此它的应用非常有限，但它可以是一个极佳的资源，特别是在用于寻找方向时，因为它具有信噪比（SNR）显示。KisMAC 是渗透测试人员的一项极佳工具，它提供了执行主动和被动扫描的能力，并具有强大的图形化信号显示。此外，本章讨论的所有工具的功能都内置在 KisMAC 中，包括去身份验证、数据包注入、WEP 破解和 WPA 破解。

如果你想要一个快速更改 MAC 地址的工具，SirMACsAlot（`www.securitytribe.com/roamer/SirMACsAlot.tar.gz`）提供了一个简单的命令行界面来用于更改 MAC 地址。

此列表并不完整，每天都有新的工具发布，因此保持与时同步并理解你需要的工具以及哪些可用可用至关重要。Auditor 对渗透测试人员来说，一个优势是它整合了大量的工具，并且随着每次更新，会添加更多工具，为这个已经非常出色的资源带来了更多功能。

#### 额外的 GPSMap 地图服务器

Terrasatellite 地图（如图 5.3 所示）并不是唯一的地图类型。GPSMap 允许你从许多不同的来源和类型生成地图。以下列表显示了 GPSMap 可用的地图服务器选项和类型。

- `-S-1` 创建无背景地图的网络表示
- `-S0` 使用 Mapblast
- `-S1` 使用 MapPoint（在本文写作期间，此功能尚无法工作）
- `-S2` 使用 TerraServer 卫星地图
- `-S3` 使用美国人口普查的矢量地图
- `-S4` 使用 EarthMaps 的矢量地图
- `-S5` 使用 TerraServer 地形图

# 第 6 章

## 网络设备

本章的核心技术和源工具：

- `Traceroute`
- `DNS`
- `Nmap`
- `ICMP`
- `Ike-scan`
- `Autonomous System Scanner`
- `Cisco Torch`
- `Snmpfuzz.pl`
- `SNMP`
- `Finger`
- `Nessus`
- `ADMsnmp`
- `Hydra`
- `TFTP-Bruteforce`
- `Cisco Global Exploiter`
- `Internet Routing Protocol Attack Suite (IRPAS)`
- `Ettercap`

## 目标

本章的目标是演示和讨论路由器和交换机上常见的漏洞和配置错误，渗透测试人员应该使用哪些开源工具来利用这些漏洞，以及这项活动如何契到渗透测试的大图中。

## 方法

路由器和交换机在网络上执行最基础的操作。它们在网络上路由和引导数据包，并在最底层实现通信。因此，如果不包含网络设备，任何渗透测试都是完整的。如果渗透测试人员能够获得关键设备的控制，就能控制整个网络。修改路由器配置的能力可以实现数据包重定向。

### DNS

你可以通过模拟从用（次级）DNS 服务器的行为并向主 DNS 服务器请求区域传输（`zone transfer`）来尝试获取整个 DNS 主机名数据库。如果此操作被允许，通过分析返回的 DNS 主机名可以很容易找到根节点。配置良好的 DNS 服务器被设置为仅允许其名称服务器执行此操作，在这种情况下，可以使用其他技术和工具来收集 DNS 信息。图 6.1 显示了 `redhat.com` 域区域传输失败。

图 6.1 尝试区域传输

![](img/2714962ecb7769011405633c8d4d1fc9_351_0.png)

在这种情况下，我们需要发挥想象力并使用一些其他工具和技术。几年前，我意识到需要进行反向暴力破解，并编写了一个非常简单的 Perl 脚本来实现。该脚本命名为 `bf-dns.pl`，能够执行正向和反向 DNS 暴力破解。目前，我们只对反向暴力破解感兴趣。图 6.2 显示了首先解析 Web 服务器的主机名，然后使用 Auditor 中包含的便捷实用程序 `net` 来枚举网络范围的过程。我们将此写入文件，并将该文件作为 `bf-dns.pl` 的输入。然后我们运行 `bf-dns.pl`，由于该域名使用了未用于 IP 地址的主机名，我们告诉 `grep` 忽略这些行。在这里我们可以看到路由器的 IP 地址为 `209.132.177.254`。

# 图 6.2 反向 DNS 暴力破解

![](img/2714962ecb7769011405633c8d4d1fc9_352_0.png)

`bf-dns.pl` 可以在 `http://moonpie.org` 下载。

### Nmap

`Nmap` 让你能够世界著名的端口扫描器 `Nmap` 执行 TCP 端口扫描，`Nmap` 具有多种功能可以帮助你以相当高的确定性确定 IP 地址的真实身份。我们不仅将操作系统指识别（分析对某些 IP 数据包的响应），还将访问 OSI 层并进行应用层探测，以确定运行这些服务是否可以提供有关主机身份的任何见解（见图 6.3）。

# 图 6.3 Nmap TCP 端口扫描

```
Session Edit View Bookmarks Settings Help

root@[knoppi]# nmap -sV -T4 -O 192.168.0.254

Starting nmap 3.7 (http://www.nmap.org/nmap/) / 2005-11-11 15:22 EST

Nmap report for host scan (192.168.0.254)

[The 1660 ports scanned but not shown below are in state: closed]

port STATE SERVICE DEVICE

23/tcp open alert cisco telnet (IOS 12.X)

80/tcp open finger cisco fingerprint

MAC Address: 00:00:07:AC:00:08 (Cisco Systems)

Device type router

Running: Cisco router

OS details: Cisco running IOS 12.1.5-12.2.13a

Nmap scan completed -- 1 IP address (1 host up) in 16.771 seconds

root@[knoppi]#
```
