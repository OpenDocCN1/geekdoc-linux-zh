
# 366 Linux 管理：入门指南

为了在你的内核中启用对新 `nftables` 的支持，需要在内核配置期间启用以下项：网络数据包过滤（Network Packet Filtering）、`nf_tables`、`nf_tables conrack`、`IPv4_tables` 以及 `IPv6 nf_tables`。网络数据包过滤可以在 → 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤（Netfilter）下找到。

核心 `nftables` 支持可以在 → 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤（Netfilter）→ 核心 Netfilter 配置（Core Netfilter Configuration）→ Netfilter_tables 支持下找到。

`nf_tables conrack`可以通过 → 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤框架（Netfilter）→ 核心 Netfilter 配置（Core Netfilter Configuration）启用。

`IPv4_tables` 位于 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤框架（Netfilter）→ IP: 网络配置（IP: Net Configuration）→ IPv4_tables 支持。

最后，`IPv6_tables` 支持可以通过 → 网络支持（Networking Support）→ 网络选项（Networking Options）→ 网络数据包过滤框架（Netfilter）→ IPv6: 网络配置（IPv6: Net Configuration）→ IPv6_tables 支持启用。

## 可选但合理的内核选项

通过将这些选项直接编译进内核，从技术上讲，你必须让 Netfilter 为大多数应用程序工作。然而，某些选项可以让生活变得更轻松，提供额外的安全性，并支持一些常见协议。出于所有实际目的，你应该考虑将这些选项视为必要条件。以下所有内容都可以编译为模块，这样只有正在使用的模块会被加载到内存中：

- **FTP 协议支持** 一旦选择了连接跟踪（Connection Tracking），即可使用此选项。有了它，你可以通过 NAT 正确处理 FTP 连接。主动 FTP 在传输数据时，需要从服务器向客户端建立一个单独的连接（例如目录列表、文件传输等）。默认情况下，NAT 不知道该如何处理服务器发起的连接。有了 FTP 模块，NAT 将获得正确处理该协议的智能性，并确保关联的连接返回到正确的客户端。

- **IRC 协议支持** 一旦选择了连接跟踪（Connection Tracking），即可使用此选项。如果你预计 NAT 后的用户将使用互联网中继聊天（IRC）与互联网上的其他人通信，则需要此模块来正确处理连接、IDENT 请求和文件传输。

- **连接状态匹配（Connection State Match）** 一旦启用了 IP Tables 支持，即可使用此选项。有了它，连接跟踪获得了在章的前部分“连接跟踪与 NAT”中讨论过的精通功能。重申一下，它允许根据数据包与之前数据包的关系进行数据包匹配。对于任何将系统配置为防火墙的人来说，这应该被视为一个必要条件。

# 第 13 章 Linux 防火墙 (Netfilter)

- **数据包过滤（Packet Filtering）** 如果你想提供数据包过滤选项，则需要此选项。

- **REJECT 目标支持（REJECT Target Support）** 此选项与数据包过滤选项相关，因为它提供了一种向数据包源发送互联网控制消息协议（ICMP）错误来拒绝数据包的方法，而不是直接丢弃它。根据你的网络情况，这可能很有用；但是，如果你的网络面向互联网，REJECT 选项并不是一个好主意。静默地丢弃你不需要的数据包比产生更多流量要好。

- **LOG 目标支持（LOG Target Support）** 有了此选项，你可以配置系统记录匹配规则的数据包。例如，如果你想记录所有被丢弃的数据包，此选项可以实现这一点。

- **全 NAT（Full NAT）** 此选项是在 Netfilter 中提供 NAT 功能的必要条件。

- **MASQUERADE 目标支持（MASQUERADE Target Support）** 此选项是提供一种通过 NAT 隐藏私有网络的必要条件。该模块在内部创建一个 NAT 条目。

- **REDIRECT 目标支持（REDIRECT Target Support）** 此选项允许系统将数据包重定向到 NAT 主机本身。使用此选项允许你构建透明代理，当无法为网络中的每个客户端配置代理设置，或者应用程序不利于连接到代理服务器时。

- **本地连接的 NAT（NAT of Local Connections）** 此选项允许你对源自 NAT 系统的数据包应用 NAT 规则。

- **数据包标记（Packet Mangling）** 此选项允许你对源自 NAT 系统的数据包应用 NAT 规则。

# 第 13 章 Linux 防火墙 (Netfilter) 369

在 Fedora 发行版中，与示例 `FIREWALL_RULES_FILE.txt` 等效的是 `/etc/sysconfig/iptables`，运行的命令为：

```
[root@fedora-server ~]# iptables-save > /etc/sysconfig/iptables
```

- 2. 在 `/etc/sysconfig/iptables-config` 文件的 `IPTABLES` 变量中添加适当的模块。例如，添加 `ip_conntrack_ftp` 和 `ip_nat_ftp`，使 `IPTABLES_MODULE` 行如下：

```
IPTABLES_MODULES="ip_conntrack_ftp ip_nat_ftp"
```

> 提示 IPv6 防火墙 (`iptables`) 的配置选项存储在 `/etc/sysconfig/iptables-config` 文件中。例如，`IPTABLES_MODULES` IPv4 的 IPv6 等效项是 `ip6-config` 文件中的 `IP6_MODULES`。

- 3. 使用 `sysctl` 工具根据需要对内核参数进行任何更改。例如，要启用转发，您将运行以下命令：
