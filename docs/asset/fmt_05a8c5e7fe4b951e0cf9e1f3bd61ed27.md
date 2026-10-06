
```
# /etc/protocols
# $Id: Net-HOWTO.sgml, v 1.1.1.1 2001/01/17 19:55:16 lx Exp $
#
# Internet (IP)
#nfrom: (@)protocols    5.1 (Berkeley) 4/17/89
#n Updated for NetBSD based on RFC 1340, 分配的数字 (1992年7月)。
ip 0      # Internet, 伪协议号
icmp 1 ICMP   # 网络控制消息协议
igmp 2 IGP      # 网络组管理
ggp 3 GGP      # 网关-网关协议
encap 4 IP-ENCAP # IP 中的 IP 封装（正式名称为 IP）
st 5 ST        # 数据流模式
tcp 6 TCP      # 传输控制协议
eg 8 EGP      # 外部网关协议
pup 12 PUP     # PARC 通用数据包协议
udp 17 UDP     # 数据报协议
hmp 20 HTTP    # 主机监控协议
xns-dip 22 XNS-DIP # Xerox NIS
rdp 27 RDP      # *可靠数据报* 协议
iso-tp4 24 ISO-TP4 # 传输协议类 4
xtp 36 TCP     # Xmas 传输协议
ddp 33 DDP      # 数据报交付协议
idpr-cmtp 39 IDPR-CMTP # IDPR 控制消息传输
rspf 73 RSVP   # 路径优先路由。
vmtp 81 VMTP   # 多功能消息传输
ospf 89 OSFP # 开放最短路径优先
ipip 94 IPIP # IPIP 封装
encap 98 ENCAP    # 另一种 IP 封装
```

### 5.9.2. `/etc/networks`

`/etc/networks` 文件是一个通过网络名称映射网络地址的数据库。它的功能与 `/etc/hosts` 类似。它提供了网络名称对应的地址。格式如下：

```
networkname address
```

一个示例可能是：

```
loopback 127.0.0.0
localnet 192.168.0.0
amprnet 44.0.0
```

`/etc/networks` 文件允许你指定哪些网络是允许的。

## 5.10. 安全与访问控制

本节将介绍如何通过 `/etc/hosts` 文件来安全你的网络。这是一个重要的规则：不要在行首使用 `#` 注释掉你想要使用的配置项。为了确保安全，你应该考虑 `inetd` 文件中的许多规则。有些规则是自动配置的，例如：

```
# /etc/hosts
```

`/etc/hosts` 文件中包含了描述哪些主机服务的规则。这里有一个非常有用的令牌：`EXCEPT` 令牌允许你提供一个异常列表，我们将在稍后的示例中介绍。

### 5.10.1. `/etc/ftpusers`

`/etc/ftpusers` 文件是一个简单的列表，用于允许某些用户通过 ftp 登录。它的内容可能如下：

```
# /etc/ftpusers - 允许登录 ftp 的用户
root
uucp
bin
mail
```

### 5.10.2. `/etc/security`

`/etc/security` 文件允许你指定哪些 tty 设备允许登录：

```
# /etc/security - 允许登录的 tty 设备
tty1
tty2
tty3
tty4
```

### 5.10.3. `/etc/hosts.allow`

`/etc/hosts.allow` 文件是 `tcpd` 程序的一个配置文件。它包含了描述哪些主机允许访问服务的规则。文件格式非常简单：

```
# /etc/hosts.allow
#
# <service list>: <host list> [: command]
```

`service list` 这是一个逗号分隔的服务名称列表，适用于该规则。示例服务名有：`ftpd`、`telnetd` 和 `fingerd`。

`host list` 这是一个逗号分隔的主机列表。你也可以在这里使用 IP 地址。你可以指定主机名或通配符来匹配主机组。例如：`vkktj ampr.org` 匹配特定主机，`.uts.edu.au` 匹配任何以字符串结尾的名称，`44` 匹配任何以数字开头的 IP 地址。有一些特殊令牌可以简化配置：`ALL` 匹配所有主机，`LOCAL` 匹配不包含 `.` 的与你机器同域的主机，`PARANOID` 匹配主机名与其地址不符（主机欺骗）。还有一个最后一个非常有用的令牌：`EXCEPT`，它允许你提供一个异常列表。

`command` 这是一个可选参数。该参数是匹配此规则时将执行的命令完整路径。例如，它可以运行一个尝试识别登录到连接主机的用户的命令。它也可以向系统管理员生成邮件信息或其他警告，告知有人尝试连接。这里可以包含许多扩展变量。一些常见的示例是：`%h` 扩展为连接主机的名称（如果没有名称则），`%d` 为调用的守护进程名称。

一个示例：

```
# /etc/hosts.allow
#
 允许任何人发送邮件
in.smptpd: ALL
# 仅允许域内和家中的主机访问 telnet 和 ftp
telnetd, ftppd: LOCAL, myhost.athome.org
# 允许任何人使用 finger，但记录他们是谁。
fingerd: ALL: (finger %@h | mail "finger from %h")
```

### 5.10.3.2. `/etc/hosts.deny`

`/etc/hosts.deny` 文件是 `/usr/sbin/tcpd` 程序的配置文件。`hosts.deny` 包含了规则，描述了哪些主机被禁止访问你机器上的某个服务。

一个简单的示例看起来如下：

```
# /etc/hosts.deny
#
# 拒绝所有具有可疑主机名的主机
ALL: PARANOID
#
# 拒绝所有主机。
ALL: ALL
```

`PARANOID` 条目是多余的，因为另一个条目以防万一拦截了所有内容。这两个条目中的任何一个都可以作为合理的默认设置（取决于你的具体需求）。

在 `/etc/hosts.deny` 中设置 `ALL: ALL` 默认值，然后在 `/etc/hosts.allow` 中专门启用你所使用的的服务和服务主机，是最安全的配置。

### 5.10.4. `/etc/hosts.equiv`

`hosts.equiv` 文件用于授予某些主机和用户访问你机器上账户的权限，而无需提供密码。这在你控制所有机器的安全环境中是有用的，但在其他情况下，它的安全性取决于受信任主机中最不安全的那个。为了提高安全性，请不要使用此机制。也鼓励用户不要使用 `.hosts` 文件。

### 5.10.5. 正确配置你的 ftp 守护进程。

许多站点会对运行匿名 ftp 服务器感兴趣，以便他人上传和下载文件，而不需要特定用户。如果你决定提供此服务，请确保为 ftp 守护进程配置匿名访问。大多数关于 `ftpd (8)` 的页面都详细描述了正确的步骤。你应该始终确保自己遵循了这些指令。一个重要的提示是不要在匿名账户的 `/etc` 目录中使用 `/etc/passwd` 文件的副本。确保删掉所有细节（必须保留的除外），否则你将容易受到暴力破解密码技术的攻击。

### 5.10.6. 网络防火墙。

不让数据报甚至到达你的机器（或服务器）是一种极佳的安全手段。这在《Firewall–HOWTO》中有深入介绍，在本文稍后的章节中也有更简洁的介绍。

### 5.10.3. tcpd hosts 访问控制机制。

### 5.10.7. 其他建议。

这里有一些供你考虑的其他（可能带有宗教色彩的）建议：

`sendmail`

> 尽管 `sendmail` 非常流行，但 `sendmail` 守护进程在安全警告公告中出现的频率令人惊心。我的建议是不运行它。

NFS 以及其他 Sun RPC 服务

警惕这些服务。它们有各种可能的利用漏洞。要找到 NFS 这类服务的选项非常困难。如果你配置了它们，请确保对允许谁拥有挂载权限保持谨慎。

## 第 6 章 以太网信息

本节涵盖了特定以太网的信息，还涵盖了以太网卡的配置。

### 6.1. 支持的以太网

### 6.1.1. 3Com

- 3Com 3501 – `避开瘟疫！` (3c501 驱动)

- 3Com 3503 (3c503 驱动), 3505 (3c505 驱动), 3507 (3c507 驱动), 3509/3c509B (ISA) / 3579 (EISA)

- 3Com Ethernet III Vortex Ethercard (3c590, 3c592, 3c595, 3c597) (PCI), 3Com Ethernet XL Boomerang (3c900, 3c905 (PCI)) 和 Cyclone (3c905B, 3c980) Ethercards (3c59x 驱动) 和 3Com Fast Etherlink Ethercard (3c515) (ISA) (3c515 驱动)

- 3Com 3ccfe75 Cyclone Cardbus (3c59x 驱动)

- 3Com 35c75 Cardbus (3c59x 驱动) (ALL PCMCIA ??)

### 6.1.2. AMD, ATT, Allied Telesis, Ansel, Apricot

- AMD LANCE (7C960) / PCNet-ISA (AT500, HP2405, NE2100)

- ATT WaveLAN

- Allied Telesis AT1700

- Allied Telesis LA100

- Allied Telesis AT2400/BT ("ne")

- Ansel Communications AC3200 (EISA)

- Apricot Xen-II / 8259

### 6.1.3. Cabletron, Cogent, Crystal

- Cabletron E21xx

- Cogent EM110

- Crystal Lan CS8920, CS8900

### 6.1.4. Danpex, DEC, Digi

- Danpex-9400

- DEC DE425 (EISA) / DE434/DE435 (PCI) / DE450/DE500 (DE4x)

- DEC DE450/DE500-XA (Tulip)

- DEC EtherWorks

- DEC EtherWorks 3 (DE2003, DE2024, DE2005)

- DEC De214x “Tulip”

- DEC Silver (Tulip)

- Digi International DLink DE–220P, DE–5287, DE–530, D–500

### 6.1.5. Fujitsu, HP, ICL, Intel

- Fujitsu FMV-181/182/183/184

- HP PLAN (2724 and 27xx)

- HP PLAN (2724B and 2752A)

- HP 10/100 (J2577, J2573, 2724B, J2585) (ISA/PCI)

- ICL EtherTeam

- Intel EtherExpress

- Intel Pro

### 6.1.6. KTI, Macromate, NCR NE2000/1000, Netgear, New Media

- KTI ET16/P-D2

- Macromate MN–220P (nP or NE2000 模式)

- NCR WaveLAN

- NCR1000 (小心克隆版)

- Netgear FA–310 (Tulip)

- New Media Ethernet

### 6.1.7. PureData, SE, SMC

- PureData P802, PDO803

- SE 805

- SMC 9000 系列

- SMC EtherPower 100

### 6.1.8. Sun, ATT, Western, Western Digital

- Sun LANCE (kernel 2.2 and newer)

- Sun Intel (kernel 2.2 and newer)

- Schneider 300

- Sun EtherPower (Tulip)

## 7.2. EQL – 多行等均衡器

EQL 设备的名称为 `eql`。在标准内核源码中，每台机器可能只能有一个 EQL 设备。EQL 提供了一种利用点对点链路（如 PPP、slip 等）或作为 tcp/ip 的单逻辑链路的方法。使用多条低速线路比安装一根高速线路要廉用得多。

内核编译选项：

```
Network device support --->
[*] Network device support
<*> EQL (serial line balancing) support
```

为了支持这种机制，线路另一端的机器也必须支持 EQL。Linux、Livingston Postmasters 和拨号接入服务器都支持兼容的设施。

要配置 EQL，你需要使用 eql 工具，这些工具可以从 metalab.unc.edu 获取。

配置非常简单。你首先开始配置 eql 接口。eql 接口就像任何其他网络设备一样。你使用 `ifconfig` 工具配置 IP 地址和 mtu。这里有一个示例：

```
root# ifconfig eql 192.168.10.1 mtu 1006
```

接下来，你需要手动启动你所使用的每条线路。这些可以是任何点对点网络设备的组合。你如何启动连接取决于它们是种种链路。请参考相关章节获取更多信息。

最后，你需要将串口链路与 eql 设备关联。这被称为 `enslaving`（奴化）：如所示通过 `eq_ensave` 命令完成：

```
root# eql_ensave eql sl0 28800
root# eql_ensave eql ppo 14400
```

你在 `eq_ensave` 中指定的 `estimated speed`（估计速度）参数并不直接起作用。它被 E 驱动用于管理该设备应该接收的数据份额。你可以通过调整此值来优化线路的平衡。

要从 eql 设备上解除线路，使用所示的 `eql_emancipate` 命令：

```
root# eql_emancipate eql sl0
```

你正在为任何其他点对点链路添加路由，但你的路由应该指向 eql 设备而不是实际的串口设备。你通常使用：

```
route# addthemselfseq
```

eql 驱动由 Simon Janes 开发，邮箱为 simon@ncm.com。

本节对你有帮助吗？为什么不捐赠 $2.50 ？

# Linux Networking HOWTO

## 7.3. IP 计数（针对 Linux–2.0）

内核 IP 计数功能允许你收集和分析某些网络使用数据。收集的数据包括自上次重置以来累计的数据包数量字节字节。你可以指定各种规则来根据你的目的对功能分类。此选项在内核 2.1.102 中已移除，因为旧的基于 `ipfwadm` 的防火墙被 `ipfwchains` 取代了。

内核编译选项：

| Networking options ----|

| [* IP: accounting     |

编译并安装内核后，你需要使用 `ipfwadm` 命令来配置 IP 计数。拆分计数信息有许多方法。我选择了一个可能有简单示例。你应该阅读 `ipfwadm` 的 man 页面以获取更多信息。

场景：你有一个通过 PPP 链路连接到互联网的以太网。在以太网上，有一台机器为你提供服务。你想知道每个 ftp（以及万维网流量）产生了多少流量，以及总的 tcp 和 udp 流量。

你可能会使用如下所示的命令（作为 shell 脚本）：

```bash
#!/bin/sh
#
# 清空计数规则
ipfwadm -A -f
#
# 设置变量
localnet=44.136.8.96/29
any=0
# 为本地以太网段添加规则
ipfwadm -A in -a -P tcp -D localnet ftp-data
ipfwadm -A out -a -P tcp -S localnet ftp-data
ipfwadm -A in -a -P tcp -D localnet www
ipfwadm -A out -a -P tcp -S localnet www
ipfwadm -A in -a -P tcp -D localnet
ipfwadm -A out -a -P tcp -S localnet
ipfwadm -A in -a -P udp -D localnet
ipfwadm -A out -a -P udp -S localnet
#
# 默认规则
ipfwadm -A in -a -P tcp -D any ftp-data
ipfwadm -A out -a -P tcp -S any ftp-data
ipfwadm -A in -a -P tcp -D any www
ipfwadm -A out -a -P tcp -S any www
ipfwadm -A in -a -P tcp -D any
ipfwadm -A out -a -P tcp -S any
ipfwadm -A in -a -P udp -D any
ipfwadm -A out -a -P udp -S any
#
# 列出规则
ipfwadm -A -1l -n
```

名称 `ftp-data` 和 `www` 指向 `/etc/services` 中的行。最后一条命令列出每个计数规则并显示收集的总数。

分析 IP 计数时需要注意的一点是，所有规则的总数都会增加。如果我想获得差值，你需要执行适当的方法。例如，如果我想知道有多少数据不是 ftp 或 wip 的，我会从匹配所有数据包的规则中减去各个总数。
