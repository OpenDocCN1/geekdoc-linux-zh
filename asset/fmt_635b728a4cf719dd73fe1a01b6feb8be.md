
启动后，`system-config-network` 可能会询问你是否要创建新设备。然而，如果你在一台已安装网络卡的计算机上安装了 Fedora，启动 `system-config-network` 后会出现图 17.1 中所示的屏幕。

![](img/774d40fd20903495c5cd00e2efad3f33_508_0.png)

**图 17.1** 使用初始的 `system-config-network` 网络屏幕开始配置你的网络客户机主机。

点击 DNS 选项卡以配置系统的 DNS 设置、主机名或 DNS 搜索路径。点击 Hosts 选项卡，然后点击“新建”或“编辑”按钮（选择主机后），以在系统的 `/etc/hosts` 文件中创建或编辑条目，例如，添加网络上主机机的 IP 地址、主机名和别名，见图 17.2 中编辑主机条目的示例。

点击“设备”选项卡，然后点击“新建”或选择现有设置并点击“编辑”，以自动或手动设置以太网设备。图 17.3 显示了“添加新设备类型”对话框，其中包含所有必要的信息，用于*静态*或固定 IP 地址分配。选择你的网卡如何获取配置，手动、通过动态主机控制协议（见下一节）或通过 Bootp。只需根据需要填写空白即可。

> **注意**
>
> Bootp 是 DHCP 构建在其上的初始协议，大部分已被 DHCP 取代。

当你完成配置网卡或编辑网卡的 IP 地址或分配方案后，使用“文件”菜单中的“保存”菜单项保存更改。请注意，你还可以使用“配置文件”菜单（如图 17.1 中所示）为你的已安装网卡创建不同的网络配置和 IP 地址分配。这在你想为运行 Fedora 的笔记本电脑创建例如家庭或工作网络设置时非常方便。

## 图 17.2

高亮显示现有条目，然后单击“编辑”按钮以更改网络配置屏幕中“主机”选项卡里的 `/etc/hosts` 条目。

![img/774d40fd20903495c5cd00e2efad3f33_509_0.png](img/774d40fd20903495c5cd00e2efad3f33_509_0.png)

## 图 17.3

在“添加新设备类型”对话框的“配置网络设置”屏幕中配置以太网设备。

![img/774d40fd20903495c5cd00e2efad3f33_509_1.png](img/774d40fd20903495c5cd00e2efad3f33_509_1.png)

# 动态主机配置协议

顾名思义，动态主机配置协议（DHCP）配置主机以连接到您的网络。DHCP 允许网络管理员在网卡激活后，为每个主机连接网络时配置所有的 TCP/IP 参数。这些参数包括自动为网卡分配 IP 地址、在 `/etc/resolv.conf` 中设置名称服务器条目以及为主机配置默认路由和网关信息。本节首先描述如何使用 DHCP 为您的网卡获取 IP 地址分配，然后描述如何使用 Fedora 快速设置并启动 DHCP 服务器。

> 您可以通过阅读 RFC2131“动态主机配置协议”来了解有关 DHCP 的更多信息。请访问 http://www.ietf.org/rfc/rfc2131.txt。

## DHCP 的工作原理

DHCP 通过保存可能连接到网络的每个网络客户端的识别信息来提供网络参数的持久存储。三个最常见的识别信息对是：

- **网络子网/主机地址** — 用于允许主机随时连接到网络

- **子网/主机名** — 允许指定的主机连接到子网

- **子网/硬件地址** — 在从 DHCP 获取主机名后，允许特定客户端连接到网络

DHCP 还向客户端分配临时或永久网络（IP）地址。一旦临时分配（称为*租约*）到期，客户端可以请求延长租约，或者如果不再需要该地址，客户端可以放弃该地址。对于将永久连接到拥有足够可用地址的网络的主机，DHCP 分配无限期租约。

DHCP 为您的网络带来一些优势。首先，它将分配 IP 地址的责任从网络管理员（可能会意外分配重复的 IP 地址）转移到了 DHCP 服务器。其次，DHCP 更好地利用了有限的 IP 地址。如果用户因任何原因不在办公室，用户的主机可以释放其 IP 地址供其他主机使用。

就像生活中大多数事物一样，DHCP 并不完美。仅通过 DHCP 无法配置服务器，因为 DNS 不知道 DHCP 分配给主机的地址。这意味着，仅通过 DHCP 配置的机器无法进行 DNS 查询；因此，无法提供服务。然而，当使用子网/主机名或子网/硬件地址标识符时，DHCP 可以基于 DNS 条目进行分配。

> 使用 DHCP 配合注册主机名配置服务器的问题正在由动态 DNS 解决，一旦完全开发，它将使 DHCP 能够向 DNS 注册 IP 地址。这将允许例如注册一个域名（如 imalinuxuser.com），而无需使用特定主机的静态 IP 地址即可轻松访问该域名的 web 服务器。需要克服的最大障碍是启用每个连接到系统的更新 DNS 的主机所带来的安全影响。一些公司，如 http://www.dyndns.org，已经提供动态 DNS 服务并为 Linux 提供了客户端。

# 在安装和启动时激活 DHCP

在安装过程中，您可以指示 Fedora 安装程序保存您网卡的 DHCP 设置。安装后，您还可以使用 `system-config-network` 客户端编辑 TCP/IP 配置信息，以正确初始化和配置您的网卡，使您的系统连接到局域网和互联网。当您选择动态或 DHCP 分配的 IP 地址方案作为您网卡的设置时，广播地址被设置为 255.255.255.255，因为 `dhclient`（用于 IP 配置的 DHCP 客户端）最初不知道该 DHCP 服务器在哪里，所以请求必须在网络上广播直到有服务器回复。

DHCP 特定信息只是作为 `BOOTPROTO=dhcp` 条目保存在 `/etc/sysconfig/network` 目录下的网卡配置中（在特定设备，如 `eth0` 的设置和脚本中）。

其他用于获取 DHCP 设置的特定配置保存在 `/etc` 目录下名为 `dhclient.conf` 的文件中，并记录在 `dhclient.conf` man 手册页中。还有超过 100 个选项记录在 `dhcp-options` man 手册页中。

然而，使用 DHCP 并不那么复杂。如果您想使用 DHCP 并且知道网络上有一台服务器，您可以使用 `dhclient` 快速配置您的网卡，如下所示：

```bash
# dhclient
Internet Software Consortium DHCP Client V3.0pl2
Copyright 1995-2001 Internet Software Consortium.
All rights reserved.
For info, please visit http://www.isc.org/products/DHCP
Listening on LPF/lo/
Sending on LPF/lo/
Listening on LPF/eth0/00:a0:24:aa:f5:17
Sending on LPF/eth0/00:a0:24:aa:f5:17
Sending on Socket/fallback
DHCPOFFER on eth0 from 192.168.2.254
DHCPACK from 192.168.2.254
save_previous /etc/yp.conf
save_previous /etc/resolv.conf
bound to 192.168.2.253 -- renewal in 9906 seconds.
```

在此示例中，第一个以太网设备 `eth0` 已从位于 192.168.2.254 的 DHCP 服务器获取了 IP 地址 192.168.2.253。续期将在大约 2 小时 45 分钟后进行。

> **注意**
>
> 位于 `/etc/sysconfig` 目录下名为 `dhcpd` 的文件可以包含任何可选的命令行参数，例如网卡租约时间（接口拥有分配地址的时间段）。有关选项，请参见 `dhcpd` 手册页。

# DHCP 软件安装与配置

DHCP 客户端和服务器的安装可能在初始安装 Fedora 时最简单，但您之后也可以使用 RPM 包，或者自行下载并构建源代码。RPM 包可用您的 Fedora CD-ROM 或镜像 FTP 站点（更多信息请参见第 7 章）。本节描述配置 `dhclient` 以及设置并运行 `dhcpd` 守护进程。

## DHCP `dhclient`

如前所述，在主机上安装 Fedora 时（有关安装的详细信息请参见第 3 章“安装 Fedora”），已安装网卡的 DHCP 使用很容易实现，并且在安装的网络步骤期间，您可以选择在启动时启动 DHCP。如果您选择这样做（并选择安装 DHCP 客户端软件包），DHCP 客户端 `dhclient` 将发送一条广播消息，DHCP 服务器将回复您主机的网络信息。就这样；您完成了。

如果您选择从源代码安装，您将需要（以 `root` 身份）下载并安装包含 `dhclient` 的服务器软件包。解压缩源文件，从源目录的根目录运行 `./configure`，运行 `make`，然后运行 `make install`。这应该会将 DHCP 客户端二进制文件放置在启动过程中正确时间启动的位置。
