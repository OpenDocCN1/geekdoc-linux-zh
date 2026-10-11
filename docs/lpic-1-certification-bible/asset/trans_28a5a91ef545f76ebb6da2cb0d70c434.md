
## 以下是 `traceroute` 工具的使用示例

该示例展示了在目的地址和接收者之间的路径上，每个节点提供的信息。

```bash
# traceroute www.hungryrindsn.com
traceroute to www.hungryrindsn.com (38.170.216.15), 30 hops max, 38 byte packets
1 192.168.1.1 (192.168.1.1) 0.028 ms 1.791 ms 1.476 ms
2 10.233.32.1 (10.233.32.1) 12.678 ms 12.859 ms 13.707 ms
3 24.25.1.61 (24.25.1.61) 8.093 ms 8.917 ms 45.217 ms
4 24.25.1.49 (24.25.1.49) 8.488 ms 10.062 ms 15.093 ms
5 24.93.64.97 (24.93.64.97) 17.706 ms 11.147 ms 9.593 ms
6 12.124.234.37 (12.124.234.37) 25.965 ms 32.363 ms 31.102 ms
7 gbr5-p80.wsdc.ip.att.net (12.123.9.58) 21.789 ms 24.097 ms 23.419 ms
8 gbr3-p100.wsdc.ip.att.net (12.122.5.194) 32.894 ms 33.464 ms 42.197 ms
9 gbr1-p70.wsdc.ip.att.net (12.122.1.158) 31.698 ms 22.994 ms 56.648 ms
10 gri-p340.wsdc.ip.att.net (12.123.8.218) 33.614 ms 30.625 ms 29.107 ms
11 204.6.117.65 (204.6.117.65) 32.978 ms 21.781 ms 35.766 ms
12 nw.transit.tier1.us.psi.net (154.13.2.97) 88.099 ms 113.275 ms 130.073 ms
13 rc7.nw.us.psi.net (38.1.23.199) 95.938 ms 100.910 ms 108.484 ms
14 ip20.c12.sanfrancisco.ca.us.psi.net (38.146.152.20) 91.448 ms 107.134 ms
15 www.idgbooks.com (38.170.216.15) 99.785 ms 93.408 ms 108.695 ms
```

## route

`route` 工具用于显示、删除和添加路由。`route` 最常用的选项如表 15-9 所示。在路由表中配置默认网关是至关重要的。如果没有此条目，数据将无法传输到本地网络段之外。`route` 命令还可以用于配置系统作为路由器工作，当安装了多个网络接口时。通过适当的配置，Linux 能够路由连接网络段之间的信息。当 Linux 接收信息时，它会维护一个目标缓存。这允许它快速将信息路由到经常请求的目标。以下是使用 `route` 命令显示的数据示例。

```bash
# route
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
localhost * 255.255.255.0 U 0 0 0 eth0
default 10.254.90.140 0.0.0.0 UG 0 0 0 eth0
```

此示例显示了一条到默认网关的单一路由。默认网关的 IP 地址是 10.254.90.140。度量值为 0 表示这是默认路由。冗余路由将具有更高的度量值，这意味着系统只会在较低度量值的路由不可用时才会尝试它们。表 15-10 显示了标志（Flags）字段的可能值。

### 表 15-9：route 选项

| 选项 | 功能 |
|---|---|
| -v | 详细模式。 |
| -n | 以 IP 地址形式显示地址。不将 IP 地址解析为 DNS 名称。 |
| -N | 将硬件地址解析为名称。 |
| -e | 显示扩展信息。 |
| -C | 显示缓存而不是常规路由表。 |

### 表 15-10：标志值

| 值 | 含义 |
|---|---|
| U | 路由可用（Up）。 |
| H | 目标是主机。 |
| G | 使用网关。 |
| R | 重新安装，用于动态路由。 |
| D | 动态路由。此路由由路由守护进程安装。 |
| M | 此路由由路由守护进程修改，或重定向。 |
| C | 缓存条目。 |
| ! | 被拒绝的路由。 |

也可以从路由表中添加和删除信息。以下示例展示了如何使用 route 命令删除和添加默认路由。

```bash
# route del default
# route add default gw 10.254.90.140
```

## 管理网络配置文件

在 Red Hat 系统中，网络配置文件存储在 /etc/sysconfig/network-scripts。存储在此处的 ifcfg-eth0 文件包含系统上安装的第一个以太网适配器的设备名称和 IP 地址信息。其他网络适配器的信息文件，包括环回和 PPP 适配器，也存储在这里。

在 Debian 系统中，网络配置文件位于 `/etc/network/interfaces`。该文件包含系统上配置的所有适配器的 IP 地址分配信息。环回适配器、以太网适配器和 PPP 适配器在此文件中都有相应的部分。

### /etc/hosts

`/etc/hosts` 文件在 Debian 和 Red Hat 系统中都用于提供 IP 地址到域名的解析。该文件在任何 DNS 服务器之前被检查，因此将经常访问的系统添加到该文件中可以减少网络流量。

但是，重要的是要记住，当列出的系统的 IP 地址或主机名配置发生任何变化时，必须更新此文件。该文件只能包含具有静态 IP 地址的主机名；使用 DHCP 的主机不应该列在这里，因为 IP 地址可能会改变。本地主机名也存储在此文件中。以下是 `/etc/hosts` 文件中的示例条目：

```
127.0.0.1              localhost.localdomain  localhost
10.254.90.133          norbert.the-nashes.net
10.254.90.135          deedee.the-nashes.net
```

### /etc/services

`/etc/services` 文件包含有关端口映射到特定服务的详细信息。正如你在以下示例中看到的，大多数端口都包含了到 TCP 和 UDP 的映射。对端口映射的任何更改都应使用此文件进行。你可能希望通过更改端口分配作为一种安全措施。如果你希望运行 FTP 服务器但希望隐藏它，你可以更改端口分配。这将防止人们在不知道正确端口的情况下连接到服务器。当应用程序运行时，它会检查 `/etc/services` 文件以确定使用哪个端口。

```
ftp-data            20/tcp
ftp                 21/tcp
ftp                 21/udp              fspd
ssh                 22/tcp              # SSH Remote Login Protocol
ssh                 22/udp              # SSH Remote Login Protocol
telnet              23/tcp
# 24 - private                     mail
smtp                25/tcp
# 26 - unassigned
time                37/tcp              timeserver
time                37/udp              timeserver
rlp                 39/udp              resource    # resource
nameserver          42/tcp              name        # IEN 116
whois               43/tcp              nickname
```

### /etc/resolv.conf

/etc/resolv.conf 文件包含用于主机名解析的名称服务器，以及在输入未完全限定的域名时要搜索的域名。这些服务器需要将主机名和域名（如 redhat.the-nashes.net）转换为 IP 地址（如 10.254.90.145）。网络管理员或互联网服务提供商提供这些名称服务器。此文件内容的示例如下：

```
search the-nashes.net
nameserver 10.254.90.131
nameserver 4.2.2.1
```

### /etc/HOSTNAME 和 /etc/hostname

Debian 系统上的 /etc/HOSTNAME 和 Red Hat 系统上的 /etc/hostname 包含本地机器的主机名信息。这些文件包含系统的完全限定域名。以下是 Red Hat 基础系统上 /etc/hostname 文件中的一个条目示例。

```
deedee.the-nashes.net
```

## 配置 PPP

- 配置和使用 PPP。定义连接所需的聊天序列（给定一个登录示例），设置在建立 PPP 连接时自动运行的命令，发起或终止 PPP 连接，发起或终止 ISDN 连接，设置 PPP 在断开时自动重新连接。

PPP，即点对点协议，用于拨号连接。此协议允许 TCP/IP 协议套件通过电话线工作。在 Linux 上使用 PPP 时，PPP 连接被配置为网络接口。Linux 提供了各种工具来帮助配置和使用 PPP 接口。

### 聊天脚本

PPP 使用聊天脚本来进行适当的拨号连接。聊天脚本首先建立连接，然后 pppd 程序配置连接。聊天脚本包含所有连接信息，如电话号码、用户 ID、密码以及任何必要的连接字符串。脚本包含预期的字符串及其后的响应字符串。建议只提供足够的预期字符串信息以识别该字符串。如果你提供的信息更多且字符串不匹配，将会发生错误。以下是聊天脚本条目的一个示例：

```
login: ppp password: hello2u2
```

