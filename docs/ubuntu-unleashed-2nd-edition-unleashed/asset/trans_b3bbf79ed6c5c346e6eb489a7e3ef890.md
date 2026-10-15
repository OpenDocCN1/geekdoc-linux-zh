

![](img/e464b828c497c99e41f61d4c55f1c0db_444_0.png)

FIGURE 18.2 Highlight an existing entry, and then click the Properties button to change /etc/hosts entries in the Hosts tab of the Network Configuration screen.

Ubuntu 在检测和配置你的网络接口方面做得很好，让你几乎无需动手操作。然而，你可能需要分配一个静态 IP 地址，这可以通过在 Connections 选项卡中选择适当的网络接口并点击 Properties 按钮来实现。这在图 18.3 中显示，你可以看到你可以选择使用静态 IP 地址。只需确保输入所有详细信息，然后点击 OK，一切应该就能正常工作。

![](img/e464b828c497c99e41f61d4c55f1c0db_444_1.png)

FIGURE 18.3 Assign a static IP address to a network interface.

## NOTE

Bootp 是 DHCP 建立的基础初始协议，目前已大多被 DHCP 取代

你也可以为你的计算机分配位置，特别是在你使用笔记本电脑并在多个需要不同配置的网络之间移动时非常方便。只需选择 network-admin 窗口顶部的灰色条并选择 Create Location。输入一个有意义的名称，例如 Home，然后重复此操作再创建一个位置，Work。每次在位置之间切换时，Ubuntu 都会检测到它需要使用特定于这些位置的配置，因此例如你可能希望使用 DHCP 在

## Dynamic Host Configuration Protocol

顾名思义，*Dynamic Host Configuration Protocol (DHCP)* 用于为你的网络连接配置主机。DHCP 允许网络管理员在 NIC 激活后连接到网络时为每个主机配置所有 TCP/IP 参数。这些参数包括自动为 NIC 分配 IP 地址、在 `/etc/resolv.conf` 中设置名称服务器条目，以及为主机配置默认路由和网关信息。本节首先描述如何使用 DHCP 为你的 NIC 获取 IP 地址分配，然后说明如何使用 Ubuntu 快速设置并启动 DHCP 服务器。

> **NOTE**
> 
> 你可以通过阅读 RFC2131 “Dynamic Host Configuration Protocol” 来了解更多关于 DHCP 的信息。浏览至 http://www.ietf.org/rfc/rfc2131.txt。

## How DHCP Works

DHCP 通过为可能连接到网络的每个网络客户端保存标识信息来提供网络参数的持久存储。最常见的三对标识信息是

- **Network subnet/host address**—用于主机随时连接到网络
- **Subnet/hostname**—使指定的主机能够连接到子网
- **Subnet/hardware address**—使特定客户端在从 DHCP 获取主机名后能够连接到网络

DHCP 还为客户端分配临时或永久的网络（IP）地址。当临时分配，即 *lease*，到期时，客户端可以请求延长租期，或如果地址不再需要，客户端可以释放该地址。对于将永久连接到网络且有足够地址可用的主机，DHCP 分配无限租期。

DHCP 为你的网络提供一些优势。首先，它将分配 IP 地址的责任从可能意外分配重复 IP 地址的网络管理员转移到 DHCP 服务器。其次，DHCP 更好地利用了有限的 IP 地址。如果用户因某种原因不在办公室，用户的主机可以释放其 IP 地址供其他主机使用。

像生活中的大多数事物一样，DHCP 并非完美。服务器无法仅通过 DHCP 配置，因为 DNS 不知道 DHCP 分配给主机的地址是什么。

这意味着仅通过 DHCP 配置的机器上无法进行 DNS 查找；因此，无法提供服务。然而，当使用 subnet/hostname 或 subnet/hardware address 标识符时，DHCP 可以基于 DNS 条目进行分配。

## NOTE

使用 DHCP 通过注册主机名配置服务器的问题正在由 Dynamic DNS 来解决，Dynamic DNS 在完全开发后将使 DHCP 能够将 IP 地址注册到 DNS。这将允许你，例如，注册一个域名（如 imalinuxuser.com）并能够轻松访问该域的 Web 服务器，而无需使用特定主机的静态 IP 地址。需要克服的最大障碍是允许连接到系统的每个主机更新 DNS 的安全影响。一些公司，例如 http://www.dyndns.org/，已经提供 Dynamic DNS 服务并为 Linux 提供客户端。

## Activating DHCP at Installation and Boot Time

Ubuntu 自动将你的网络接口默认为使用 DHCP，因为这是设置网络接口最简单的方式。对于使用动态或 DHCP 分配的 IP 地址方案的 NIC，广播地址设置为 255.255.255.255，因为 dhclient，即用于 IP 配置的 DHCP 客户端，最初不知道 DHCP 服务器位于何处，因此请求必须在每个网络上传输直到服务器回复。

DHCP 特定信息 simply 保存为 NIC 下的 BOOTPROTO=dhcp 条目，位于 /etc/sysconfig/network 目录下（在特定设备的设置和脚本中，例如 eth0）。

其他特定于获取 DHCP 设置的设置保存在名为 dhclient.conf 的文件中，位于 /etc/dhcp3/dhclient.conf 目录下，并在 dhclient.conf 手册页中有文档说明。超过 100 个选项也在 dhcp-options 手册页中有文档说明。

然而，使用 DHCP 并没有那么复杂。如果你想使用 DHCP 并且知道网络上有服务器，你可以快速通过使用 dhclient 来配置你的 NIC，如下所示：

```
# dhclient
Internet Systems Consortium DHCP Client V3.0.3
Copyright 2004-2005 Internet Systems Consortium.
All rights reserved.
For info, please visit http://www.isc.org/products/DHCP

Listening on LPF/eth0/00:0f:ea:b2:53:85
Sending on   LPF/eth0/00:0f:ea:b2:53:85
Sending on   Socket/fallback
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 6
DHCPOFFER from 192.168.2.1
DHCPREQUEST on eth0 to 255.255.255.255 port 67
```
