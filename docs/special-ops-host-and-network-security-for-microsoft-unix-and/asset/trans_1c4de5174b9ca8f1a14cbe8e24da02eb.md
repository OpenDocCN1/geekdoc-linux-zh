

## 第 2 章 · 企业资产的清单与暴露

由于本书并非为初学者编写，我假设你已经了解传输控制协议/网协议 (TCP/IP) 并且以前使用过这些工具。如果你对示例中显示的选项不熟悉，请参考该工具的上下文、手册页（man page）或帮助文本。

## 主机发现与服务发现

基础资产盘点实际上只有两个步骤：主机发现和服务发现，但每种方法都有多种技术，可以根据不同的情况和需求来收集结果。

> 注意：这是一个基础列表，并不打算列出所有可能的扫描类型。如果你想查看该列表，请访问 Fyodor 的 nmap 主页：www.insecure.org。

- 主机发现：互联网控制协议 (ICMP) 请求（如回显/Echo、子网掩码/Netmask 和时间戳/Timestamp 请求）是主机发现的第一步。主机发现的第二步是创建一个响应 TCP ping 响应设备列表。
- ICMP 扫描：由于大多数内部网络都允许 ICMP，因此当你需要快速确定网络或某个分段的总体规模时，ICMP 扫描非常有用。如果你需要以非常快速且粗略的方式识别主机，应该执行 ping 扫描（ping sweep）。务必将活跃的 IP 地址保存到文件中以备后用。

```
SCANLINE: sl -in 10.0.3.150-190 | find "10.0.3.*" > ICMPping.txt
MAP: nmap -sn -sPI -PM -PP 10.0.3.150-190 -oM ICMP.txt
```

- TCP ping 扫描：可以使用任何可靠的 TCP 端口扫描器，使用 SYN 或 ACK 数据包扫描多个常用 TCP 端口列表并等待响应。务必在进行 TCP 扫描之前将端口扫描器配置为“不执行 ping”。将响应的主机添加到文件中以备后用。以下示例显示了使用 nmap 和 ScanLine 进行 TCP Ping 的语法：

![](img/729efc56f204a2ebffb8295c3a2dfdfb_48_0.png)

你可以根据需要向 nmap 命令中添加多个 -PS 参数，以测试使用多个 TCP 端口获取响应。如果你想在 nmap 中执行 TCP ACK ping，应该使用 -PT 命令而不是 -PS。两种扫描器都可以通过 -p 命令强制使用指定的端口。

```
SCANLINE: sl -hp -T 10.0.3.150-190 | find "10.0.3." > TCPping.txt
NMAP: nmap -n -sP -PS22 -PS80 -PS139 10.0.3.150-190 -oM TCPping.txt
```

- 服务发现：结合 TCPping.txt 文件和 ICMPping.txt 文件中的每个 IP 地址，创建一个名为 LiveIPS.txt 的文件。使用 LiveIPS.txt 文件扫描网络中的 TCP 和用户数据报协议 (UDP) 端口。这为我们提供了这些主机正在运行哪些应用程序的快照，并让我们了解它们在 IT 基础设施中扮演的角色。图 2.1 显示了使用 LiveIPS 文件扫描常用服务的情况。

## 图 2.1 使用 Scanline.exe 查找常用端口

```
C:\>sl -hj -p -f LiveIPS.txt
ScanLine (TM) 1.01
http://www.foundstone.com

10.192.0.131
TCP ports: 6000
UDP ports:
10.192.0.134
TCP ports: 21 25 111 6000 32770
UDP ports:
10.192.0.139
TCP ports: 53 1433 3389
UDP ports: 53
10.192.0.144
TCP ports: 21 111
UDP ports: 69
10.192.0.145
TCP ports: 21 25 111 6000 32770
UDP ports:
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_49_0.png)

10.192.0.147
TCP ports: 21 25 111 32770 32772
UDP ports:

- 源端口扫描：如果你正在扫描受保护的网络，还应该使用 nmap 和 ScanLine 中的 -g 选项来使用指定的源端口，这可能会绕过路由器的过滤。源端口扫描对于列举被 TCP/IP 过滤器隐藏的主机非常有帮助。当你指定源端口时，TCP 和 UDP 扫描均有效。有用的测试端口有 20、53 和 88。如果你要扫描的子网安装了 IPSec 过滤器 (src=88)、允许 FTP-Data 入站 (src=20) 或需要 DNS 传输 (src=53)，你可能会发现以前未见过的主机和服务。我建议创建并维护一个企业端口列表。这将允许你在网络中发现新的、不常的服务时轻松更新它。

> 注意：那里有很多 TCP/UDP 列表，但 Moonpie 最喜欢的 (www.moonpie.net) 简单、直观。它有大约 3500 个 TCP 端口和 3200 个 UDP 端口可以抓取并导出到文件中供扫描器使用。此外，该网站还提供搜索功能帮助你识别未知的 TCP 和 UDP 端口。将发现的结果存储在电子表格中，以便进行过滤并最终创建趋势分析。(img/729efc56f204a2ebffb8295c3a2dfdfb_50_0.png)

## 图 2.2 资产清单

| A | B | C | D | E | F | G | H | I |
|---|---|---|---|---|---|---|---|---|
| 标题 | | | | | | | | |
| 日期 | | | | | | | | |
| 来源 | | | | | | | | |
| 范围 | 10.192.0.130 | 10.192.0.131 | 10.192.0.134 | 10.192.0.135 | 10.192.0.140 | 10.192.0.142 | 10.192.0.144 | 10.192.0.145 | 10.192.0.147 |
| 服务器名称 | 10.192.0.131 | | | | | | | |
| 运行 | | | | | | | | | |
| 状态 | | | | | | | | | |
| 活跃服务 | | | | | | | | | |
| 监听服务 | | | | | | | | | |
| FTP | | | | | | | | | |
| SSH | | | | | | | | | |
| HTTP | | | | | | | | | |
| HTTPS | | | | | | | | | |
| SMB | | | | | | | | | |
| SNMP | | | | | | | | | |
| RDP | | | | | | | | | |
| SQL | | | | | | | | | |
| Telnet | | | | | | | | | |
| VNC | | | | | | | | | |
| IIS | | | | | | | | | |
| Apache | | | | | | | | | | |
| MySQL | | | | | | | | | | |
| Oracle | | | | | | | | | | |
| PostgreSQL | | | | | | | | | | |
| Redis | | | | | | | | | | |
| MongoDB | | | | | | | | | | |
| RabbitMQ | | | | | | | | | | |
| Kafka | | | | | | | | | | |
| Elastic | | | | | | | | | | |
| Active Directory | | | | | | | | | | |
| Domain Controller | | | | | | | | | | |
| File Server | | | | | | | | | | |
| Print Server | | | | | | | | | | |
| Web Server | | | | | | | | | | |
| Mail Server | | | | | | | | | | |
| Database Server | | | | | | | | | | |
| Application Server | | | | | | | | | | |
| DNS Server | | | | | | | | | | |
| Proxy Server | | | | | | | | | | |
| Load Balancer | | | | | | | | | | | |
| Services | | | | | | | | | | |

## 使用发现脚本

如果你倾向于自己编写这个脚本，可以使用 moonpie.org 上的 Discover.pl（每周/每两周/每月）来发现内部网络所有分段的主机，列举服务并将其放入机器可读的输出中（见图 2.3）。如果你只使用脚本，你可以在二到三分钟内完成 C 类扫描，并在约九分钟内完成 B 类扫描。

## 图 2.3 $Discovery.pl$ 会话输出

![](img/729efc56f204a2ebffb8295c3a2dfdfb_51_0.png)

我建议你修改脚本（discover 子程序），针对多个 TCP 端口检查源端口 20 和 88，如下所示：

```perl
sub discover {
  ($outfile = ($target =~ /(\d+\.\d+\.\d+)));
  $outfile = "discovery-$outfile";
  open (OUT,"$outfile");
  my $probe_types = (
  # 在此处添加你喜欢的端口
  # 为了获得最佳结果，使用不同的源端口，例如用于 ftp-data 的端口 20
  -sp -PS21 -PS22 -PS25 -PS53 -PS80 -PS110 -PS111 -PS139 -PS1433
  PS3389 -T $timing -g 53",
  -sp -PS21 -PS22 -PS25 -PS53 -PS80 -PS110 -PS111 -PS139 -PS1433
  PS3389 -T $timing -g 20",
  -sp -PS21 -PS22 -PS25 -PS53 -PS80 -PS110 -PS111 -PS139 -PS1433
  PS3389 -T $timing -g 88",
  -sp -PI -T $timing",
  -sp -PP -T $timing",
  -sp -PM -T $timing"
  );
```

Moonpie 的其他工具对于处理发现脚本的输出非常有用。你应该使用 Parse_mach.pl 获取特定服务的清单信息。使用 Quickdump.pl 快速创建可读格式的每日资产清单用于资产日志。

## SNMP 资产扫描

如果你正在寻找基于 Win32 GUI 工具套来帮助资产清单，并且有数百美元预算，可以查看 SolarWinds (www.solarwinds.net)。我最喜欢 IP Network Browser。它是一个简单网络管理协议 (SNMP)、域名服务 (DNS) 和 ICMP 发现工具，可以评估 IP 地址范围，并轻松获取网络上运行 SNMP 的任何 Windows 系统、Unix 系统、路由器、交换机以及任何网络设备的信息。如果你为 IP Network Browser 提供企业的团体字符串，该工具生成的信息将更加丰富。

