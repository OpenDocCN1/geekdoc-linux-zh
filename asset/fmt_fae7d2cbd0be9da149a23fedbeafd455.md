
# DNS 查询工具差异

`nslookup`、`host` 和 `dig` 之间的差异通过示例说明最为清晰。在练习中，你将练习使用这些工具执行正向和反向 DNS 查找。为此，请按照以下步骤操作：

1. 登录 Linux 文本模式会话或在 GUI 会话中启动终端窗口。

2. 输入 `nslookup www.google.com`。你可以替换另一个主机名；但此主机名的一个关键点是它解析为多个 IP 地址，`nslookup` 会在多个 `Name:` 和 `Address:` 行中显示。这种做法在极其流行的网站上很常见，因为负载在多台计算机之间进行了均衡。注意，`nslookup` 会在 `Server:` 和 `Address:` 行中报告所使用的 DNS 服务器的 IP 地址。（后者包括端口号，见后文“网络端口”章节描述。）

- `host www.google.com`。此命令的输出比 `nslookup` 命令要短一些，但它应该报告服务器的 IP 地址。虽然 `host` 不报告 DNS 服务器的地址，但它启用了 IPv6，因此它会报告 IPv6 地址以及该站的 IPv4 地址。

- `dig www.google.com`。此输出比 `nslookup` 或 `host` 都长得多。事实上，它比 `host` 更灵活。

## 主机名解析配置

`etcnswitch.conf` 文件支持更多选项。例如，你可以通过在 `hosts` 行中添加适当的选项并配合必要的支持软件，使用 Windows NetBIOS 调用或轻量级目录访问协议（LDAP）服务器进行名称解析。`passwd`、`shadow` 和 `group` 行控制 Linux 如何验证用户身份以及管理组。除非你了解涉及的系统，否则你不应尝试更改这些配置，但你通常应该意识到 `etcnswitch.conf` 的重要性。

除了 `ethosts` 之外，Linux 还支持名为 `etcnswitch` 的文件。它的工作方式与 `ethosts` 非常相似，但它适用于网络地址，并反转了每行中名称和 IP 地址的顺序：`loopback 127.0.0.0 mynet 192.168.7.0-`

此示例设置了两个链接：将 `loopback` 名称指向 `127.0.0.0/8` 网络，将 `mynet` 指向 `192.168.7.0/24` 网络。通常不需要编辑此文件。

## 网络端口

连接到特定的计算机很重要，但还有一种额外的寻址方式留着：发送者必须拥有远程系统中某个特定程序的地址。例如，假设你正在使用网络浏览器。Web 服务器计算机运行的服务可能比仅仅 Web 服务器要多——它可能还在运行电子邮件服务器或 FTP 服务器，这只是许多种可能性中的两种。除了 IP 地址之外的另一个数字允许你将流量定向到特定程序。这个数字就是网络端口号，访问 TCP/IP 网络的程序通常通过一个或多个端口进行。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_761_0.png)

端口号是 UDP 和 TCP 协议的特性。某些协议（如 ICMP）不使用端口号。

服务器启动时会绑定到特定的端口，根据约定，这些端口与特定的服务器程序关联。例如，端口 `25` 与电子邮件服务器相关，端口 `80` 用于 Web 服务器。表 8.2 总结了几个重要端口的用途。客户端可以将请求定向到特定端口，并期望连接到适当的服务器。客户端的端口号不是固定的；它由操作系统分配。因为是客户端发起的传输，它可以在连接请求中包含其端口号，所以客户端不需要固定端口号。动态分配客户端端口号允许一台计算机轻松地运行单个客户端的多个实例——它们不会竞争访问同一个端口。

### 表 8.2 端口号、其用途及典型的 Linux 服务器

| 端口号 | TCP 或 UDP | 用途 | 示例 Linux 服务器 |
|---|---|---|---|
| `20` | TCP | 文件传输协议 (FTP) 数据 | ProFTPd, vsftpd |
| `21` | TCP | FTP | ProFTPd, vsftpd |
| `22` | TCP | 安全外壳 (SSH) | OpenSSH, Dropbear |
| `23` | TCP | Telnet | `in.telnetd` |
| `25` | TCP | 简单邮件传输协议 (SMTP) | Sendmail, Postfix, Exim, qmail |
| `53` | TCP 和 UDP | 域名系统 (DNS) | 伯克利命名域名 (BIND; 也称为 `named`), dnsmasq, djbdns |
| `67` | UDP | 动态主机配置协议 | Internet Software Consortium |
| `68` | UDP | (DHCP) | (ISC) DHCP (`dhcpd`), dnsmasq |
| `80` | TCP | 超文本传输协议 (HTTP) | Apache, Roxen, `thttppd` |
| `110` | TCP | 邮局协议版本 3 (POP3) | Dovecot, Qpopper, `popa3d` |
| `111` | TCP | Portmapper 和 UDP | NFS, NIS, 其他基于 RPC 的服务 |
| `113` | TCP | `auth/ident` | `identd` |
| `119` | TCP | 网络新闻传输协议 (NNTP) | InterNetNews (INN), Leafnode |
| `123` | UDP | 网络时间协议 (NTP) | `ntpd` |
| `139` | TCP | NetBIOS 会话 (Windows 文件共享) | Samba |
| `143` | TCP | 交互式邮件访问协议 (IMAP)¹ | Dovecot, Cyrus IMAP, UW-IMAP |
| `161` | UDP | 简单网络管理协议 (SNMP) | Net-SNMP |
| `162` | UDP | SNMP 陷获消息 | Net-SNMP |
| `177` | UDP | XDMCP | XDM, KDM, GDM |
| `389` | TCP | LDAP | OpenLDAP |
| `443` | TCP | SSL over HTTP (HTTPS) | Apache, Roxen |
| `445` | TCP | 微软目录服务 (DS) | Samba |
| `465` | TCP | SSL over SMTP; 或 URL 汇合目录 (URD)² | Sendmail, Postfix, Exim, qmail; 或网络路由器 |
| `514` | UDP | 远程系统日志 | `rsyslog` |
| `631` | TCP | 打印协议 (IPP) | 通用 Unix 打印系统 (CUPS) |
| `636` | TCP | 轻量级目录 | OpenLDAP |
| `993` | TCP | SSL over IMAP | Dovecot, Cyrus IMAP, UW-IMAP |
| `995` | TCP | SSL over POP3 | Dovecot, Qpopper, `popa3d` |
| `5900+` | TCP | 帧缓冲区 (RFB) | 虚拟桌面 (VNC): OpenVNC, TightVNC, TigerVNC |
| `6000–6007` | TCP | X 系统 (X) | X.org-X11, XFree86 |

¹ 某些来源扩展 IMAP 为 Internet Message Access Protocol 或 Internet Mail Access Protocol。

² 端口 `465` 正式用于 URD；但它也被常用作安全邮件传输端口，尽管这不是该端口的指定用途。

TCP/IP 端口的一个关键区别是特权端口和非特权端口。后者的数字小于 `1024`。Unix 和 Linux 系统限制仅 `root` 用户访问特权端口。其理念是客户端可以连接到特权端口并由系统管理员进行配置，因此是可以信任的。

遗憾的是，在今天，大于 `1024` 的端口所有人都可以。

## 客户端与服务器

TCP/IP 端口的一个重要区别是客户端和服务器。客户端是发起连接的程序。服务器监听连接并对其做出响应。例如，网络浏览器是客户端，而 Web 服务器是服务器。然而，一台计算机可以同时是两者。

客户端启动时，它会发送广播以寻找 DHCP 服务器。服务器会响应（仅使用客户端的硬件地址），提供客户端启用与网络上其他计算机通信所需的配置信息——最重要的是客户端的 IP 地址、子网掩码，以及网络网关和 DNS 服务器地址。DHCP 服务器还可能给客户端提供主机名，并提供有关网络的其他细节。然后，客户端将使用这些参数进行自配置。IP 地址不是永久分配的；它被称为 DHCP 租约（`lease`），如果不进行续租，DHCP 服务器可能会将该租约给另一台计算机。因此，客户端会定期向 DHCP 服务器检查以恢复其租约。
