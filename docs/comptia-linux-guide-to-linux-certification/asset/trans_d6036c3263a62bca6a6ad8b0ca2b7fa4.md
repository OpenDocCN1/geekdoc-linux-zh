
完成本章后，您将能够：

- 配置基础网络服务，包括 DHCP、DNS、NTP 和 NIS
- 使用 Apache Web 服务器配置 Web 服务
- 配置文件共享服务，包括 Samba、NFS 和 FTP
- 使用 Postfix 配置电子邮件服务
- 使用 PostgreSQL 配置数据库服务

在上一章中，您了解了使 Linux 参与网络的概念和步骤。您还学习了 Linux 系统上常用的网络服务。在本章中，您将检查为网络中用户提供基础、Web、文件共享、电子邮件和数据库服务的网络服务配置。

## 基础服务

某些网络服务以 TCP/IP 配置、名称解析、时间管理和集中身份验证的形式，为网络上的其他计算机提供网络配置和支持。这些服务统称为基础服务，包括 DHCP、DNS、NTP 和 NIS。

### DHCP

回顾上一章的内容，您的网络接口可以使用动态主机配置协议（DHCP）进行手动或自动配置。如果通过网络接口使用 DHCP 进行配置，它会向网络发送 DHCP 广播，请求 IP 配置信息。如果网络上的 DHCP 服务器拥有一组 IP 地址范围，它会向客户机计算机租用一个 IP 地址，租期为一定时间；该租约到期后，客户机计算机必须发送另一个 DHCP 请求。由于 DHCP 服务器会跟踪其租给客户机计算机的 IP 地址，因此您可以确保没有两台计算机收到相同的 IP 地址。如果两台计算机被手动配置为相同的 IP 地址，则它们都无法使用 IP 协议进行通信。

DHCP 服务器还可以向客户机计算机发送其他 IP 配置信息，例如它们应使用的默认网关和 DNS 服务器。

### DHCP 租约流程

DHCP 客户端向 DHCP 服务器请求 IP 配置的过程涉及几个阶段。首先，客户端向网络上的所有主机发送请求（DHCPDISCOVER 数据包）。作为回应，DHCP 服务器发送包含潜在 IP 配置的报价（DHCPOFFER 数据包）。然后，DHCP 客户端通过向相关 DHCP 服务器发送 DHCPREQUEST 数据包来选择（接受）该报价。接下来，DHCP 服务器向客户端发送确认，指示客户端可以使用该 IP 配置的时间量（DHCPACK 数据包）。最后，客户端使用该 IP 配置配置自身。该过程如图 13-1 所示。

![](img/c27875544958897d817484d558c208c8_605_0.png)

> 如果网络中存在多个 DHCP 服务器，DHCP 客户端将接受其收到的第一个报价，并通过向其他 DHCP 服务器发送 DHCPDECLINE 数据包来拒绝所有其他报价。

在租期时间过半时（即租期的 50% 处），DHCP 客户端会向 DHCP 服务器发送另一个 DHCPREQUEST 数据包，以续展其 IP 配置。如果其 DHCP 服务器不可达，它将尝试在租期的 87.5% 处通过向网络上的所有主机发送 DHCPDISCOVER 数据包来再次续展其 IP 配置，以便网络上的任何 DHCP 服务器都能通过发送报价进行响应。一旦租约到期，DHCP 客户端会丢弃从 DHCP 服务器获取的 IP 配置，并使用 APIPA（IPv4 169.254.0.0 网络）自动配置网络接口。

![](img/c27875544958897d817484d558c208c8_606_0.png)

图 13-1 DHCP 租约流程

要将您的 Linux 系统配置为 DHCP 服务器，您必须先安装 DHCP 守护进程，该守护进程可从在线软件仓库中获取。Linux 可用的两种最常见的 DHCP 守护进程是 DHCP 守护进程（dhcpd）和 BusyBox DHCP 守护进程（udhcpd）。

## 使用 dhcpd 配置 Linux DHCP 服务器

大多数 Linux 系统（包括 Fedora 20）使用 dhcpd 守护进程来提供网络上的 DHCP 功能。要使用 dhcpd 配置 Fedora 20 系统，您必须先添加一个 dhcpd 用户账户（无需密码），dhcpd 将使用该账户。接下来，您必须在适当的配置文件中添加行，以列出您网络适当的 IP 地址范围，以及租约信息和其他 IP 配置选项。IPv4 和 IPv6 的 dhcpd 配置文件如下：

- `/etc/dhcp/dhcpd.conf` 存储 IPv4 配置
- `/etc/dhcp/dhcpd6.conf` 存储 IPv6 配置

![](img/c27875544958897d817484d558c208c8_606_1.png)

除非您希望配置 IPv4 客户端，否则不需要配置 `/etc/dhcp/dhcpd.conf` 文件。同样，除非您希望配置 IPv6 客户端，否则不需要配置 `/etc/dhcp/dhcpd6.conf` 文件。

![](img/c27875544958897d817484d558c208c8_606_2.png)

您可以参考 dhcpd.conf 文件的手册页，以获取在 `/etc/dhcp/dhcpd.conf` 和 `/etc/dhcp/dhcpd6.conf` 文件中可配置的参数完整列表。

以下输出显示了一个示例 `/etc/dhcp/dhcpd.conf` 文件，该文件在 `192.168.1.0/24` 网络上租用 IPv4 地址：

```
[root@server1 -]# cat /etc/dhcp/dhcpd.conf
default-lease-time 36000;
option routers 192.168.1.254;
option domain-name-servers 192.168.1.200;
subnet 192.168.1.0 netmask 255.255.255.0 {
   range 192.168.1.1 192.168.1.100;
}
[root@server1 -]#
```

从上述输出中注意，DHCP 服务器向客户端租用 `192.168.1.1` 和 `192.168.1.100` 之间的 IP 地址，租期为 `36,000` 秒。此外，DHCP 服务器为客户端配置默认网关 `192.168.1.254` 和 DNS 服务器 `192.168.1.200`。

在用适当信息配置 `/etc/dhcp/dhcpd.conf` 文件后，您可以启动 dhcpd 并配置其在启动时自动运行。

要查看当前的 DHCP 租约，您可以检查 IPv4 租约的 `/var/lib/dhcpd/dhcpd.leases` 文件和 IPv6 租约的 `/var/lib/dhcpd/dhcpd6.leases` 文件。

![](img/c27875544958897d817484d558c208c8_607_0.png)

更改 `/etc/dhcp/dhcpd.conf` 或 `/etc/dhcp/dhcpd6.conf` 配置文件后，必须重启 dhcpd 守护进程才能使更改生效。

## 使用 udhcpd 配置 Linux DHCP 服务器

某些 Linux 系统（包括 Ubuntu Server `14.04`）使用 udhcpd 守护进程来提供网络上的 IPv4 DHCP 功能。要使用 udhcpd 配置 Ubuntu Server `14.04` 系统，您必须首先将 `/etc/default/udhcpd` 文件中的 `DHCPD_ENABLED="no"` 行更改为 `DHCPD_ENABLED="yes"` 并保存更改。接下来，您必须在 `/etc/udhcpd.conf` 中指定您网络适当的 IP 地址范围以及租约信息和其他 IP 配置选项。以下 `udhcpd.conf` 文件在 eth0 接口上向客户端租用 `192.168.1.1` 和 `192.168.1.100` 之间的 IP 地址，租期为 `36,000` 秒，并为客户端配置默认网关 `192.168.1.254` 和 DNS 服务器 `192.168.1.200`：

```
[root@server1 -]# cat /etc/udhcpd.conf
start           192.168.1.1
end             192.168.1.100
interface        eth0
option subnet    255.255.255.0
option router     192.168.1.254
option dns        192.168.1.200
option lease      36000
lease_file       /var/lib/misc/udhcpd.leases
[root@server1 -]#
```

同样注意，上述输出表明，存储 IPv4 租约信息文件的位置（`/var/lib/misc/udhcpd.leases`）也是在 `/etc/udhcpd.conf` 文件中设置的。如果
