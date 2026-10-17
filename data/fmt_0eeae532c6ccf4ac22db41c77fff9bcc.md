
### 服务端口参考

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

`/etc/resolv.conf` 文件包含用于主机名解析的名称服务器，以及在输入未完全限定的域名时要搜索的域名。这些服务器需要将主机名和域名（如 `redhat.the-nashes.net`）转换为 IP 地址（如 `10.254.90.145`）。网络管理员或互联网服务提供商提供这些名称服务器。此文件内容的示例如下：

```
search the-nashes.net
nameserver 10.254.90.131
nameserver 4.2.2.1
```

### /etc/HOSTNAME 和 /etc/hostname

Debian 系统上的 `/etc/HOSTNAME` 和 Red Hat 系统上的 `/etc/hostname` 包含本地机器的主机名信息。这些文件包含系统的完全限定域名。以下是 Red Hat 基础系统上 `/etc/hostname` 文件中的一个条目示例。

```
deedee.the-nashes.net
```

### 配置 PPP

- 配置和使用 PPP。定义连接所需的聊天序列（给定一个登录示例），设置在建立 PPP 连接时自动运行的命令，发起或终止 PPP 连接，发起或终止 ISDN 连接，设置 PPP 在断开时自动重新连接。

PPP，即点对点协议，用于拨号连接。此协议允许 TCP/IP 协议套件通过电话线工作。在 Linux 上使用 PPP 时，PPP 连接被配置为网络接口。Linux 提供了各种工具来帮助配置和使用 PPP 接口。

#### 聊天脚本

PPP 使用聊天脚本来进行适当的拨号连接。聊天脚本首先建立连接，然后 `pppd` 程序配置连接。聊天脚本包含所有连接信息，如电话号码、用户 ID、密码以及任何必要的连接字符串。脚本包含预期的字符串及其后的响应字符串。建议只提供足够的预期字符串信息以识别该字符串。如果你提供的信息更多且字符串不匹配，将会发生错误。以下是聊天脚本条目的一个示例：

```
login: ppp password: hello2u2
```

该条目会在登录提示符处针对预期的字符串 `origin` 响应发送字符串 `ppp`。对于来自密码提示符的预期字符串 `ssword`，发送的字符串是 `hello2u2`。下面是一个更详细的聊天脚本，它会在提示时拨打 ISP 并输入登录信息：

```
ABORT BUSY
ECHO OFF
SAY "Dialling your ISP...\n"
ATDT5551212
TIMEOUT 120
SAY "Waiting up to 2 minutes for connection ... "
CONNECT 
SAY "Connected, now logging in ..."
login: account
password: pass
SAY "Logged in OK ... etc ..."
```

只要用户拥有适当的权限来访问它，该脚本可以存储在系统上的任何位置。用户通过 `pppd` 命令的参数指定要运行的脚本。调制解调器控制代码可以在随硬件提供的文档中找到。互联网服务提供商提供其他信息。

#### pppd

`pppd` 程序与聊天脚本协同工作以建立 PPP 连接。一旦聊天脚本建立了连接，`pppd` 会根据输入的配置选项对其进行配置。该程序使用指定的聊天脚本和连接设备运行。`pppd` 命令使用以下语法在命令行中运行：

```
pppd -option argument
```

可以指定静态地址，或者使用 DHCP 来配置地址。与 `pppd` 一起使用的一些选项列在表 15-11 中。

##### 表 15-11 pppd 选项

| **选项** | **用途** |
| :--- | :--- |
| `connect SCRIPT` | 使用指定的聊天脚本建立 PPP 连接。 |
| `disconnect SCRIPT` | 使用指定的脚本断开 PPP 连接。 |
| `holdoff TIME` | 指定在连接终止后等待多长时间才重新初始化连接。 |
| `idle SEC` | 指定在没有数据发送后断开 PPP 连接前等待的秒数。 |
| `modem` | 规定使用调制解调器控制线。 |

`pppd` 在处理命令行选项之前，会按顺序从文件 `/etc/ppp/options`、`~/.ppprc` 和 `/etc/ppp/options.tname`（按此顺序）读取选项。这允许在这些脚本中的任何一个中配置选项，而不是在命令行中输入它们。

使用 ISDN 线路发起 PPP 连接的命令如下：

```
pppd connect 'chat -f /etc/ppp/ppp_isdn.chat' holdoff 60 /dev/isdn 64000
```

#### 重点总结

本章涵盖了在 Linux 系统上提供网络连接所使用的许多重要概念和实用工具。本章中涵盖的一些最重要的项目包括以下内容：

-   TCP/IP 地址用于唯一标识网络上的每个网络接口。这些地址可以以二进制或十进制格式查看。

-   最常用的三个网络类别及其匹配的网络掩码如下：
    -   A 类：`1.0.0.0–126.0.0.0`，掩码为 `255.0.0.0`
    -   B 类：`128.0.0.0–191.0.0.0`，掩码为 `255.255.0.0`
    -   C 类：`192.0.0.0–223.0.0.0`，掩码为 `255.255.255.0`

-   TCP/IP 协议套件包括以下主要协议：IP、ARP、ICMP、TCP 和 UDP。IP 负责在网络之间传送数据报。ARP 提供 IP 地址到硬件地址的映射和转换，而 ICMP 报告数据包传送中的错误。TCP 是一种面向连接的协议，它使用会话提供数据的可靠传输。UDP 提供无连接传输，开销比 TCP 小。

-   TCP 和 UDP 使用端口和套接字来同时管理对各种应用程序的多个连接。应用程序使用 `/etc/services` 文件映射到特定端口。

-   FTP 应用程序允许从远程系统传输文件，而 Telnet 允许远程访问系统的 shell。

-   `host` 命令允许你发现指定系统的 IP 或主机名信息。`whois` 命令提供指定域名的域、名称服务器和联系信息。`finger` 实用程序可用于发现系统中特定用户的信息。

-   `ping` 和 `traceroute` 实用程序使用 ICMP，可以揭示本地系统和远程系统之间连接性的信息。这些信息对于定位两个系统之间通信故障的源头非常有用。

-   DHCP 用于允许动态 IP 地址分配；`dhcpd` 允许 Linux 机器作为 DHCP 服务器运行。DHCP 客户端使用网络配置文件进行配置。

-   `ifconfig`、`hostname` 和 `route` 命令都用于指定网络配置选项。这些命令以及 `netstat`、`domain-name`（Red Hat）和 `dnsdomainname`（Red Hat 和 Debian）还允许查看当前配置。

-   在 Debian 上用于配置网络适配器的配置文件是 `/etc/network/interfaces`，用于配置主机的文件名是 `/etc/HOSTNAME`。

-   Red Hat 系统使用 `/etc/sysconfig/network-scripts` 来存储每个网络接口的文件。在这些系统上，主机名在 `/etc/hostname` 文件中指定。

-   两个系统都使用 `/etc/resolv.conf` 文件来存储名称服务器和域搜索字符串，使用 `/etc/hosts` 文件来存储主机名到 IP 地址的映射，并使用 `/etc/services` 来提供端口映射。
