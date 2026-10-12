
如果在检查到另一台主机（你用 IP 地址指定）的连接时遇到问题，请检查 IP 路由表，看看是否指定了默认网关。然后检查网关的路由表，确保通往外部网络的路径出现在该路由表中。

从 `/sbin/route` 命令的典型输出如下所示：

/sbin/route
内核 IP 路由表

| 目标 | 网关 | 掩码 | 标志 | 度量 | 引用 | 使用 | 接口 |
|---|---|---|---|---|---|---|---|
| 192.168.1.200 | * | 255.255.255.255 | UH | 0 | 0 | 0 | eth0 |
| 192.168.1.0 | * | 255.255.255.0 | U | 0 | 0 | 0 | eth0 |
| 127.0.0.0 | * | 255.0.0.0 | U | 0 | 0 | 0 | lo |
| default | 192.168.1.1 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |

正如该路由表所示，本地网络使用 eth0 以太网接口，默认网关也是该以太网接口。默认网关是一个路由设备，处理发往 Linux 系统所在网络之外的任何网络的数据包。在本例中，发往除以 192.168.1 开头的网络地址之外的任何网络地址的数据包都会发送到网关 — 192.168.1.1 —，网关会将这些数据包转发到其他网络（当然，前提是网关已连接到另一个网络）。

## 检查主机连通性

要检查到特定主机的网络路径，请使用 ping 命令。ping 命令是一种广泛使用的 TCP/IP 工具，它使用一系列 Internet 控制消息协议（ICMP，常读作 eye-comp）消息。ICMP 提供了 Echo 消息，每台主机都会对其作出响应。利用 ICMP 消息及其回复，ping 可以确定另一系统是否存活，然后计算与该系统通信的往返延迟。

以下示例展示了我如何运行 ping 来查看网络上某台系统是否存活：

```
ping 192.168.1.50
PING 192.168.1.50 (192.168.1.50): 56 data bytes
64 bytes from 192.168.1.50: icmp_seq=0 ttl=32 time=2.2 ms
64 bytes from 192.168.1.50: icmp_seq=1 ttl=32 time=1.2 ms
64 bytes from 192.168.1.50: icmp_seq=2 ttl=32 time=1.2 ms
64 bytes from 192.168.1.50: icmp_seq=3 ttl=32 time=0.8 ms

--- 192.168.1.50 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 0.8/1.3/2.2 ms
```

在 Red Hat Linux 中，ping 会一直运行，直到你按 Ctrl+C 停止它；然后它会显示汇总统计信息，显示在两台系统之间发送数据包的典型时间。在某些系统上，ping 只是报告远程主机是否存活。但是，你仍然可以通过适当的命令行参数获取时序信息。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_172_0.png)

## 检查 TCP/IP 配置文件

在安装期间配置网络或运行 Red Hat 网络配置工具可能足以在系统上配置 TCP/IP，但你也应该了解配置文件，以便在必要时进行编辑。例如，你可以通过网络配置工具指定名称服务器，但假设你想添加一个备用名称服务器。为此，你可以直接将这些名称添加到 `/etc/resolv.conf` 文件中——该配置文件存储名称服务器的 IP 地址。

在本节的剩余部分，你将熟悉基本的 TCP/IP 配置文件。这些配置文件都是文本文件，你可以使用 cat 或 more 命令查看，并使用任何文本编辑器进行编辑。

### /etc/hosts

`/etc/hosts` 配置文本文件包含本地网络的 IP 地址和主机名列表。如果没有名称服务器，系统上的任何网络程序都会查阅此文件以确定与主机名对应的 IP 地址。输入 cat /etc/hosts 命令以查看此文件的内容。

以下是我的系统中的 `/etc/hosts` 文件，显示了 LAN 上其他主机的 IP 地址和名称：

```
127.0.0.1      localhost      localhost.localdomain
# Other hosts on the LAN
192.168.1.100  lnb486
192.168.1.50   lnb133
192.168.1.200  lnb200
192.168.1.233  lnb233
192.168.1.40   lnb400
192.168.1.60   lnb600
192.168.1.25   mac      lnbmac
192.168.1.1    lnb75
```

正如示例所示，文件中的每一行都以 IP 地址开头，后跟该 IP 地址的主机名。一个 IP 地址可以有多个主机名。

### /etc/networks

`/etc/networks` 配置文件是另一个文本文件，其中包含网络的名称和 IP 地址。这些网络名称通常在路由命令 (`/sbin/route`) 中使用，以按名称而不是 IP 地址指定网络。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_173_0.png)

如果你的 Linux PC 没有 `/etc/networks` 文件也不必惊慌。没有此文件，TCP/IP 网络也能正常工作。事实上，Red Hat Linux 安装程序不会创建任何 `/etc/networks` 文件。

### /etc/host.conf

`/etc/host.conf` 配置文本文件指定 Linux 如何获取与主机名对应的 IP 地址。输入 cat /etc/host.conf 以查看此文件的内容。通常，此文件包含以下行：

```
order hosts, bind
multi on
```

`/etc/host.conf` 文件中的条目告诉解析器库使用哪些服务以及按什么顺序解析名称。

order 选项表示服务的顺序。示例条目指定解析器库应首先查阅 `/etc/hosts` 文件，然后检查名称服务器以解析名称。名称服务器列在 `/etc/resolv.conf` 文件中，你接下来会检查该文件。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_173_1.png)

multi on 选项指定 `/etc/hosts` 文件中列出的主机可以有多个 IP 地址。具有多个 IP 地址的主机称为多宿主，因为存在多个 IP 地址意味着主机有多个网络接口（换句话说，主机“同时存在于多个网络中”）。

### /etc/resolv.conf

`/etc/resolv.conf` 配置文件是解析器使用的另一个文本文件——一个确定主机名 IP 地址的库。输入 cat /etc/resolv.conf 以查看此文件的内容。

以下是 `/etc/resolv.conf` 文件的示例：

```
search xyz.com
nameserver 164.109.1.3
nameserver 164.109.10.23
```

search 行指定搜索主机名的系统名称。nameserver 行提供你域的名称服务器的 IP 地址。如果有多个名称服务器，应将它们列在单独的行中。它们按在文件中出现的顺序进行查询。通常，你在 `/etc/resolv.conf` 文件中列出由你的 Internet 服务提供商提供的名称服务器。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_174_0.png)

> 如果你的网络没有任何名称服务器，可以安全地忽略此文件。TCP/IP 仍可工作，尽管你只能引用 `/etc/hosts` 文件中列出的主机。

### /etc/hosts.allow

此文件指定哪些主机允许使用可能在系统上运行的 Internet 服务（如 TELNET 和 FTP）。启动 Internet 服务的程序在启动前会查阅 `/etc/hosts.allow` 文件。只有当 hosts.allow 文件中的条目表明请求主机可以使用服务时，它才会启动服务。

`/etc/hosts.allow` 中的条目采用 server: IP 地址格式，其中 server 指提供特定 Internet 服务的程序的名称，IP 地址标识允许使用该服务的主机。例如，如果你希望本地网络（地址为 192.168.1.0）中的所有主机访问 FTP 服务（由 in.ftpd 程序提供），请在 `/etc/hosts.allow` 文件中添加以下行：

```
in.ftpd:192.168.1.
```

如果你希望所有本地主机都能访问所有 Internet 服务，可以使用 ALL 关键字并将行重写如下：

```
ALL:192.168.1.
```
