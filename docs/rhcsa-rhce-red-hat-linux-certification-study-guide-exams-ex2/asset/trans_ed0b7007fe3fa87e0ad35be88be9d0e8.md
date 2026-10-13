
## 图 4-4

默认 RHEL 6 防火墙规则

```
[root@server1 ~]# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
[root@server1 ~]#
```

图 4-4 中显示了六列信息，对应于各种 iptables 命令选项。所示的防火墙基于 /etc/sysconfig/iptables 文件中列出的以下规则。第一行指定要遵循的规则是过滤规则。替代规则支持网络地址转换（NAT）或改写；NAT 在第 10 章中讨论。

```
*filter
```

接下来，定向到本地系统、拟转发以及发出的网络流量通常默认使用 ACCEPT 选项接受。

```
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
```

一些安全专业人员，包括美国国家安全局，建议将 ACCEPT 至少对 INPUT 和 FORWARD 行更改为 DROP。如果接受此建议，则未被其他规则明确接受的数据包将被自动丢弃。然而，这种安全级别可能在 Red Hat 的企业安全网络服务课程（RHS333）中有所涉及，该课程面向已通过 RHCE 考试的人员开放。[0:0] 是字节和数据包计数，各自从 0 开始。

下面所有行都应用于 iptables 命令。此文件中列出的每个开关和选项都应可在相关手册页上找到。

下一行保持当前网络通信继续进行。ESTABLISHED 选项继续接受当前网络连接上的数据包。RELATED 选项接受后续网络连接的数据包，例如 FTP 数据传输。

```
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

下一个连接接受与 ICMP 关联的数据包，最常见于 ping 命令。当数据包被拒绝时，相关消息也使用 ICMP 协议。

```
-A INPUT -p icmp -j ACCEPT
```

这可能会引起警告，因为“死亡 ping”是常见攻击之一。您可以使用第 10 章中讨论的一些过滤来阻止或限制对 ping 命令的响应。

以下行将 (-A) 一条规则添加到 INPUT 链中，与称为回环适配器 (lo) 的网络接口 (-i) 相关。经该设备处理的数据会跳转 (-j) 到接受。

```
-A INPUT -i lo -j ACCEPT
```

下一行是唯一一条直接接受除回环适配器之外的新常规网络数据的规则，使用 TCP 协议。它查找 (-m) NEW 连接状态 (state --state) 的匹配项，用于匹配 TCP 数据包，使用 TCP 协议 (-p tcp)，发送到目标端口 (--dport) 22。满足所有这些条件的数据包将被接受 (-j ACCEPT)。一旦连接建立，本章中描述的第一个常规规则将继续接受该已建立连接上的数据包。

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
```

最后两条规则拒绝所有其他数据包，并向源系统发送 icmp-host-prohibited 消息。

```
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
```

COMMIT 结束规则列表。

```
COMMIT
```

由于这是与 RHCSA 考试相关的部分，更详细的讨论可在第 10 章找到，适用于 RHCE 考试。在此级别，您需要了解如何使用提供的标准配置工具管理这些防火墙。

## 防火墙配置工具

您可以自动化防火墙配置过程。为此，RHEL 包含防火墙配置工具的控制台和 GUI 版本。在这种情况下，两个工具的功能数量大致相同。虽然两个工具的外观和感觉不同，但就配置受信任服务的访问而言，其基本功能是相同的。

如果您想尝试防火墙配置工具，最好先备份相关配置文件 /etc/sysconfig/iptables。如果出现错误，请恢复文件的原始版本并运行以下命令：

```
# /etc/init.d/iptables restart
```

要了解所做的更改，请将生成的 /etc/sysconfig/iptables 文件与备份进行比较。任何差异都基于您在防火墙配置工具中的操作。

> **考试提示** 如果您使用防火墙配置工具，可能希望避免直接编辑 /etc/sysconfig/iptables 文件。任何更改在下次使用该工具时都将被覆盖。第 10 章描述了如何使用防火墙配置工具设置自定义规则。

### 防火墙配置工具的受信任服务

无论选择哪个工具，两者都支持轻松配置防火墙以允许访问表 4-6 中描述的各种服务器。

将表 4-6 与表 4-5 进行比较时，您可能会注意到，虽然 TCP 和 UDP 协议经常为特定服务保留端口，但实际服务经常只使用其中一种协议。

### 控制台防火墙配置工具

您可以使用 system-config-firewall-tui 命令启动控制台防火墙配置工具；结果如图 4-5 所示。如图所示，防火墙默认启用；该选项可以取消选择。

### 表 4-6
常见 TCP/IP 端口

| Service | Description |
|---|---|
| Amanda Backup Client | 与高级马里兰自动网络磁盘归档器（AMANDA）相关联的客户端，与 UDP 端口 10080 相关联 |
| Bacula | 一个开源网络备份服务器；与 TCP 端口 9101、9102 和 9103 相关联 |
| Bacula client | Bacula 服务器的客户端；与 TCP 端口 9102 相关联 |
| DNS | 域名服务（DNS）服务器；与端口 53 相关联，使用 TCP 和 UDP 协议 |
| FTP | 文件传输协议（FTP）服务器，与 TCP 端口 21 相关联 |
| IMAP over SSL | IMAP 通过安全套接字层（SSL）通常使用 TCP 端口 993 |
| IPsec | 与用于互联网安全关联和密钥管理协议（ISAKMP）的 UDP 端口 500 相关联，以及 ESP 和 AH 传输层协议 |
| Mail (SMTP) | 简单邮件传输协议服务器，如 sendmail 或 Postfix，使用 TCP 端口 25 |
| Multicast DNS (mDNS) | 与 UDP 端口 5353 相关联，以支持 Linux 的零配置网络（zeroconf）实现，即 Avahi |
| NFS4 | NFS 版本 4 使用 TCP 端口 2049，等等 |
| Network Printing Client | 标准打印客户端使用基于互联网打印协议（IPP）的 UDP 端口 631 |
| Network Printing Server | 标准打印服务器客户端使用基于互联网打印协议（IPP）的 TCP 和 UDP 端口 631 |
| OpenVPN | 开源虚拟专用网络系统，使用 UDP 端口 1194 |
| POP-3 over SSL | POP-3 通过安全套接字层（SSL）通常使用 TCP 端口 995 |
| RADIUS | 远程身份验证拨入用户服务（RADIUS）协议使用 UDP 端口 1812 和 1813 |
| Red Hat Cluster Suite | Red Hat 多系统套件使用 TCP 端口 11111 和 21064，以及 UDP 端口 5404 和 5405 |
| Samba | Linux 在 Microsoft 网络上通信的协议使用 TCP 端口 139 和 445，以及 UDP 端口 137 和 138 |
| Samba Client | Linux 在 Microsoft 网络上客户端通信的协议使用 UDP 端口 137 和 138 |
| Secure WWW (HTTPS) | 与安全 Web 服务器的通信使用 TCP 端口 443 |
| SSH | SSH 服务器使用 TCP 端口 22 |
| TFTP | 与简单文件传输协议（TFTP）服务器的通信需要 TCP 端口 69 |
| TFTP Client | 奇怪的是，TFTP 客户端不需要开放端口；所有通信都通过 TFTP 服务器的开放 TCP 端口 69 进行 |
| Virtual Machine Management | 远程访问基于 KVM 的虚拟机使用 TCP 端口 16509 |
| Virtual Machine Management (TLS) | 远程访问基于 KVM 的虚拟机使用 TCP 端口 16509 可以配置传输层安全（TLS） |
| WWW (HTTP) | 众所周知的 Web 服务器使用 TCP 端口 80 |

## 图 4-5

system-config-firewall

控制台防火墙配置工具

![](img/9139201cfcaf4292284a0eed074928e5_226_0.png)

