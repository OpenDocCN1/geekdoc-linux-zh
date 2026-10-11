

![](img/ec25e59d75726b7041242a56d3376832_178_0.png)

```text
[*]  正在尝试 DNS 服务器 38.100.193.90
[*]  38.100.193.90 端口 53 TCP 开放
[-]  区域传输失败！
[-]  无响应或 RSet 不针对查询名称
```

列表 223 - 使用 dnsrecon 执行区域传输

根据上述输出，我们成功对 megacorpone.com 域执行了一次 DNS 区域传输。结果基本上是该域区域文件的完整转储。

让我们尝试使用之前创建的 **list.txt** 文件对额外的主机名进行暴力破解，以进行正向查找。该列表如下所示：

```text
kali@kali:~$ cat list.txt
www
ftp
mail
owa
proxy
router
```

列表 224 - 用于使用 dnsrecon 对子域进行暴力破解的列表

要开始暴力破解尝试，我们将使用 **-d** 选项指定域名，**-D** 选项指定包含潜在子域字符串的文件名，以及 **-t** 选项指定要执行的枚举类型（在这种情况下为 **brt**，代表暴力破解）：

```text
kali@kali:~$ dnsrecon -d megacorpone.com -D list.txt -t brt
[*]  正在对 megacorpone.com 进行主机和子域暴力破解
[*]  A router.megacorpone.com 38.100.193.71
[*]  A www.megacorpone.com 38.100.193.76
[*]  A mail.megacorpone.com 38.100.193.84
[*]  3 条记录已找到
```

列表 225 - 使用 dnsrecon 暴力破解主机名

我们的暴力破解尝试已完成，我们成功解析了几个主机名。

### 7.1.6.2 DNSenum

DNSenum 是另一个流行的 DNS 枚举工具。为了展示不同的输出，让我们对 zonetransfer.me 域（由 DigiNinja[194] 拥有并明确允许进行区域传输）运行 **dnsenum**：

```text
kali@kali:~$ dnsenum zonetransfer.me
dnsenum.pl VERSION:1.2.2
------ zonetransfer.me ------

主机地址：
----------------

zonetransfer.me             7200    IN  A     217.147.180.162

名称服务器：
ns12.zoneedit.com 3653 IN A 209.62.64.46
ns16.zoneedit.com 6975 IN A 69.64.68.41

# 邮件 (MX) 服务器：

ASPMX5.GOOG.LEMAIL.COM 293 IN A 173.194.69.26
ASPMX.L.GOOGLE.COM 293 IN A 173.194.74.26
ALT1.ASPMX.L.GOOGLE.COM 293 IN A 173.194.66.26
ALT2.ASPMX.L.GOOGLE.COM 293 IN A 173.194.65.26
ASPMX2.GOOG.LEMAIL.COM 293 IN A 173.194.78.26
ASPMX3.GOOG.LEMAIL.COM 293 IN A 173.194.65.26
ASPMX4.GOOG.LEMAIL.COM 293 IN A 173.194.70.26

# 尝试区域传输并获取 Bind 版本：

正在 ns12.zoneedit.com 上尝试 zonetransfer.me 的区域传输 ...
zonetransfer.me 7200 IN SOA
zonetransfer.me 7200 IN NS
...
office.zonetransfer.me 7200 IN A 4.23.39.254
owa.zonetransfer.me 7200 IN A 207.46.197.32
info.zonetransfer.me 7200 IN TXT
asfdbox.zonetransfer.me 7200 IN A 127.0.0.1
canberra_office.zonetransfer.me 7200 IN A 202.14.81.230
asfdbvolume.zonetransfer.me 7800 IN AFSDB
email.zonetransfer.me 2222 IN NAPTR
dzc.zonetransfer.me 7200 IN TXT
robinwood.zonetransfer.me 362 IN TXT
vpn.zonetransfer.me 4000 IN A 174.36.59.154
_sip._tcp.zonetransfer.me 14000 IN SRV
dc_office.zonetransfer.me 7200 IN A 143.228.181.132

ns16.zoneedit.com Bind 版本：8.4.x
未指定暴力破解文件，退出。
```

列表 226 - 使用 dnsenum 执行区域传输。

这些枚举工具都功能强大且简单易用。在继续之前，请花时间练习使用每个工具。

[194] (DigiNinja), https://digi.ninja/about.php

### 7.1.6.3 练习

- 1. 找到 megacorpone.com 域的 DNS 服务器。
- 2. 编写一个小脚本，尝试使用 Python、Perl 或 Ruby 等更高级的脚本语言从 megacorpone.com 执行区域传输。
- 3. 重现上述示例，并使用 **dnsrecon** 尝试从 megacorpone.com 执行区域传输。

# 7.2 端口扫描

端口扫描是检查远程机器上的 TCP 或 UDP 端口，以检测目标上正在运行的服务以及可能存在哪些潜在攻击向量的过程。

请注意，端口扫描并不代表传统的用户活动，在某些司法管辖区可能被视为非法。因此，如果没有目标网络所有者的直接书面许可，不应在实验室之外执行此操作。

理解端口扫描的影响以及特定端口扫描可能造成的影响至关重要。由于某些扫描生成的流量量大且具有侵入性，盲目运行端口扫描可能对目标系统或客户网络产生不利影响，例如使服务器和网络链路过载或触发 IDS（入侵检测系统）。运行错误的扫描可能会导致客户停机。

采用适当的端口扫描方法可以显著提高我们作为渗透测试者的效率，同时限制许多风险。根据合作范围的不同，我们可以不针对整个目标网络运行全端口扫描，而是仅扫描端口 80 和 443 开始。利用可能的 Web 服务器列表，我们可以对这些服务器在后台运行全端口扫描，同时执行其他枚举工作。一旦全端口扫描完成，我们可以进一步缩小扫描范围，以在每次后续扫描中探测更多信息。端口扫描应被视为一个动态过程，对于每次合作都是独特的。一次扫描的结果决定了下一次扫描的类型和范围。

## 7.2.1 TCP / UDP 扫描

我们将使用 Ncat 对端口扫描进行简单的 TCP 和 UDP 端口扫描来开始我们的探索。需要指出的是，Ncat **不**是端口扫描器，但可以以基本的方式将其用作端口扫描器。由于它已经存在于许多系统中，当我们不需要功能齐全的端口扫描器时，我们可以重新利用其部分功能来模拟基本的端口扫描。不过，还有更多专门用于端口扫描的更好工具，我们将详细探讨这些工具。

### 7.2.1.1 TCP 扫描

最简单的 TCP 端口扫描技术，通常称为 CONNECT 扫描，依赖于三次握手 TCP $^{195}$ 机制。该机制的设计目的是让两个尝试通信的主机在传输任何数据之前协商网络 TCP 套接字连接的参数。简单来说，主机向目标端口的服务器发送 TCP SYN 数据包。如果目标端口开放，服务器将以 SYN-ACK 数据包响应，客户端主机发送 ACK 数据包以完成握手。

如果握手成功完成，则端口被视为开放。

为了说明这一点，我们将对端口 3388-3390 运行一个 TCP Ncat 端口扫描。`w` 选项指定连接超时秒数，`z` 用于指定零 I/O 模式，该模式不发送数据并用于扫描：

```text
kali@kali:~$ nc -nvv -w 1 -z 10.11.1.220 3388-3390
(UNKNOWN) [10.11.1.220] 3390 (?) : Connection refused
(UNKNOWN) [10.11.1.220] 3389 (?) open
(UNKNOWN) [10.11.1.220] 3388 (?) : Connection refused
sent 0, rcvd 0
```

列表 227 - 使用 nc 执行 TCP 端口扫描

根据此输出，我们可以看到端口 3389 开放，而端口 3388 和 3390 上的连接超时。下图显示了此扫描的 Wireshark 捕获：

| No. | Time | Source | Destination | Protocol | Length | Info |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0.593648886 | 19.11.9.125 | 10.11.1.220 | TCP | 74 | 54272 3389 [SYN] Seq=8 Win=32K |
| 2 | 4.0.373405715 | 10.11.1.220 | 10.11.1.228 | TCP | 83 | 3389 54272 [RSJ ACK] Seq=1 ACK=9 |
| 5 | 8.0.238353525 | 19.11.9.126 | 10.11.1.228 | TCP | 74 | 45692 3389 [SYN] Seq=6 Win=32K |
| 6 | 9.0.270314845 | 10.11.1.220 | 10.11.1.228 | TCP | 74 | 3389 45692 [SYN, ACK] Seq=2 ACK=7 |
| 7 | 9.0.257643092 | 10.11.1.226 | 10.11.1.228 | TCP | 86 | 45692 3389 [ACK] Seq=1 ACK=7 W |
| 8 | 8.0.258157571 | 10.11.1.228 | 10.11.1.228 | TCP | 86 | 45692 3389 [FIN, ACK] Seq=7 ACK=7 |
| 9 | 8.289200531 | 19.11.1.126 | 10.11.1.228 | TCP | 74 | 34322 3388 [SYN] Seq=8 Win=32K |
| 10 | 6.3437109449 | 10.11.1.226 | 10.11.1.228 | TCP | 86 | 3388 45692 [ACK] Seq=1 ACK=7 W |
| 11 | 6.3437159348 | 10.11.1.226 | 10.11.1.228 | TCP | 89 | 3388 34322 [RSJ, ACK] Seq=1 ACK |
| 12 | 6.345885225 | 10.11.1.228 | 10.11.1.228 | TCP | 89 | 3389 45692 [RSJ, ACK] Seq=1 ACK |

图 42：Ncat 端口扫描的 Wireshark 捕获

在此捕获中（图 42），Ncat 分别在第 1、5 和 9 行向端口 3390、3389 和 3388 发送了几个 TCP SYN 数据包。由于多种因素（包括时序问题），数据包在 Wireshark 中可能顺序错乱。请注意，服务器在第 6 行从端口 3389 发送了一个 TCP SYN-ACK 数据包，表明该端口是开放的。其他端口没有回复类似的 SYN-ACK 数据包，因此我们可以推断它们未开放。最后，在第 8 行，Ncat 通过发送 FIN-ACK 数据包关闭了此连接。

### 7.2.1.2 UDP 扫描

由于 UDP 是无状态的且不涉及三次握手，UDP 端口扫描背后的机制与 TCP 不同。

让我们对另一个目标的端口 160-162 运行一个 UDP Ncat 端口扫描。这是使用我们尚未见过的唯一 nc 选项 `u` 完成的，该选项表示 UDP 扫描：

```text
kali@kali:~$ nc -nv -u -z -w 1 10.11.1.115 160-162
(UNKNOWN) [10.11.1.115] 161 (snmp) open
```

列表 228 - 使用 Ncat 执行 UDP 端口扫描

从 Wireshark 捕获中，我们可以看到 UDP 扫描使用的是与 TCP 扫描不同的机制：

