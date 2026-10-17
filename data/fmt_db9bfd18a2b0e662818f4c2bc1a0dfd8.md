
除了 `filter` 和 `mangle` 表外，`OUTPUT` 链还可以调用 `NAT` 表中的规则。这允许管理员对从主机本身生成的出站数据包配置 NAT 转换。虽然这并不常见，但该功能允许管理员对数据包执行类似于 `PREROUTING` 式的 NAT 操作。（记住：如果数据包源自主机，它将没有机会经过 `PREROUTING` 链。）

## POSTROUTING

`POSTROUTING` 链可以调用 `NAT` 和 `mangle` 表。在此链中，管理员可以出于源地址转换 (`SNAT`) 的修改源 IP 地址。这也是另一个为了构建防火墙而进行连接跟踪的点。

## 安装 Netfilter

好消息是，如果你使用的是现代 Linux 发行版，你应该已经安装、编译并正常运行了 `iptables`。一种快速检查的方法是尝试运行 `iptables` 命令，如下：

```
[root@server ~]# iptables -L
```

在 Ubuntu 系统上，你应该运行此命令：

```bash
master@ubuntu-server:~$ sudo iptables -L
```

检查 IPv6 等效命令的快速方法是使用此命令：

```bash
[root@server ~]# iptables -L
```

注意，某些发行版在默认路径中不包含 `/sbin` 目录，`iptables` 程序很有可能就在那里。如果你不确定，尝试以下路径之一：`/sbin/iptables`、`/usr/sbin/iptables`、`/usr/local/bin/iptables` 或 `/usr/local/sbin/iptables`。`/bin` 和 `/sbin` 目录应该已经在路径中了。

# 364 Linux 系统管理：入门指南

# 第 13 章 Linux 防火墙 (Netfilter) 365

如果该命令给出了链和表的列表，就说明 Netfilter 已经安装。事实上，很有可能是操作系统安装时已经启用某些过滤器。某些发行版提供了在安装时配置或自定义基础防火墙的选项。

有了 Netfilter，除了之外，你不需要做很多。

以下章节提供了有关在设置原生内核（vanilla kernel）时可以使用选项的有用信息

## 在内核中启用 Netfilter

大部分 Netfilter 代码实际上位于内核内部，并随标准 Linux 发行版一起。如果 Netfilter 在你的发行版中尚未启用，你可以在内核配置期间通过开启选项来启用它。如果不熟悉编译内核的过程，请参阅第 9 章。

Netfilter 有许多选项。在本节中，我们将涵盖当你从零开始构建内核时可能想要选择的一些相关的选项。

## 必要的内核选项

对于 `iptables`，应支持以下内容：网络数据包过滤、IP 表和连接跟踪。

第一个是在编译内核前通过 Networking Support -> Networking Options -> Network Packet Filtering Framework (Netfilter) 菜单找到。为内核提供此 Netfilter 框架功能。如果不启用此选项，列出的其他选项都将无法工作。注意，此功能无法编译为内核模块；它要么存在要么不存在。

第二个是 IP 表，位于 Networking Support -> Networking Options -> Network Packet Filtering Framework (Netfilter) -> IP Configuration。其目的是为 Netfilter 系统提供 IP 表接口和管理。从技术上讲，此模块是可选的，因为可以使用其他的 `iptables` 或 `ipfwadm` 或新的 `nftables`；然而，除非你有特定理由留在旧界面，否则你应该坚持 `iptables` 或 `nftables`。如果你正在从非常旧的 `iptables/ipfwadm` 配置迁移到 IP 表的过程中，你肯定希望所有的模块都编译并可用。

然后是连接跟踪选项。可以在 Networking Support -> Networking Options -> Network Packet Filtering Framework (Netfilter) -> IP: Netfilter Configuration IPv4 Connection Tracking Support 找到。它提供了智能 TCP/IP 连接跟踪的支持以及对 FTP 等关键协议的特定支持；对于 IP 表选项，这个可以编译为模块。

# 366 Linux 管理：入门指南

为了在你的内核中启用对新 `nftables` 的支持，需要在内核配置期间启用以下项：网络数据包过滤（Network Packet Filtering）、`nf_tables`、`nf_tables conrack`、`IPv4_tables` 以及 IPv6 `nf_tables`。网络数据包过滤可以在 → 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤（Netfilter）下找到。

核心 `nftables` 支持可以在 → 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤（Netfilter）→ 核心 Netfilter 配置（Core Netfilter Configuration）→ Netfilter_tables 支持下找到。

`nf_tables conrack`可以通过 → 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤框架（Netfilter）→ 核心 Netfilter 配置（Core Netfilter Configuration）启用。

`IPv4_tables` 位于 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤框架（Netfilter）→ IP: 网络配置（IP: Net Configuration）→ IPv4_tables 支持。

最后，IPv6_tables 支持可以通过 → 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤框架（Netfilter）→ IPv6: 网络配置（IPv6: Net Configuration）→ IPv6_tables 支持启用。

# 可选但合理的内核选项

通过将这些选项直接编译进内核，从技术上讲，你必须让 Netfilter 为大多数应用程序工作。然而，某些选项可以让生活变得更轻松，提供额外的安全性，并支持一些常见协议。出于所有实际目的，你应该考虑将这些选项视为必要条件。以下所有内容都可以编译为模块，这样只有正在使用的模块会被加载到内存中：

- `FTP` 协议支持 一旦选择了连接跟踪（Connection Tracking），即可使用此选项。有了它，你可以通过 NAT 正确处理 FTP 连接。主动 FTP 在传输数据时，需要从服务器向客户端建立一个单独的连接（例如目录列表、文件传输等）。默认情况下，NAT 不知道该如何处理服务器发起的连接。有了 FTP 模块，NAT 将获得正确处理该协议的智能性，并确保关联的连接返回到正确的客户端。

- `IRC` 协议支持 一旦选择了连接跟踪（Connection Tracking），即可使用此选项。如果你预计 NAT 后的用户将使用互联网中继聊天（IRC）与互联网上的其他人通信，则需要此模块来正确处理连接、IDENT 请求和文件传输。

- 连接状态匹配（Connection State Match） 一旦启用了 IP Tables 支持，即可使用此选项。有了它，连接跟踪获得了在章的前部分“连接跟踪与 NAT”中讨论过的精通功能。重申一下，它允许根据数据包与之前数据包的关系进行数据包匹配。对于任何将系统配置为防火墙的人来说，这应该被视为一个必要条件。

# 第 13 章 Linux 防火墙 (Netfilter)

- 数据包过滤（Packet Filtering） 如果你想提供数据包过滤选项，则需要此选项。

- `REJECT` 目标支持（REJECT Target Support） 此选项与数据包过滤选项相关，因为它提供了一种向数据包源发送互联网控制消息协议（ICMP）错误来拒绝数据包的方法，而不是直接丢弃它。根据你的网络情况，这可能很有用；但是，如果你的网络面向互联网，`REJECT` 选项并不是一个好主意。静默地丢弃你不需要的数据包比产生更多流量要好。

- `LOG` 目标支持（LOG Target Support） 有了此选项，你可以配置系统记录匹配规则的数据包。例如，如果你想记录所有被丢弃的数据包，此选项可以实现这一点。

- 全 NAT（Full NAT） 此选项是在 Netfilter 中提供 NAT 功能的必要条件。

- `MASQUERADE` 目标支持（MASQUERADE Target Support） 此选项是提供一种通过 NAT 隐藏私有网络的方法的必要条件。该模块在内部创建一个 NAT 条目。
