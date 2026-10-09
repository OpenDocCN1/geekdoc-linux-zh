

BOOTP 是一种较旧的协议，用于向客户端动态分配网络信息。BOOTP 和 DHCP 之间最大的区别在于 BOOTP 并非设计用于提供动态地址；相反，它为每个请求配置信息的设备维护一个表格。

## DHCP 服务器

DHCP 服务器组件为 DHCP 客户端提供配置信息。DHCP 服务器在收到请求时提供 IP 地址、子网掩码、网关及其他信息。可以通过命令行或通过 GUI 工具来管理服务器配置。

DHCP 配置在不同 Linux 发行版之间并不统一。通常，服务器使用两个配置文件——/etc/dhcp/dhcpd.conf 和 /var/lib/dhcp/dhcpd.leases。dhcpd.conf 文件包含提供给 DHCP 客户端的信息。这包括地址范围、网关以及其他信息。dhcpd.leases 文件也包含分发给客户端的配置信息。这包括 IP 地址和租约时间（IP 地址分配给特定客户端的时长）。

DHCP 配置文件中有两种条目——参数和声明。参数条目包含客户端的网络配置选项。声明描述了要提供给客户端的地址。

输入到 dhcpd.conf 文件（图 7–11）中的参数和声明通常以单词*option*开头。配置文件可以包含制表符或空行以方便阅读。所有关键字均不区分大小写，以井号（#）开头的行是注释。可以使用 man *dhcp-options* 命令查看可用选项。dhcpd.conf 的一些选项如下：

- `option domain-name name;` 指定客户端在通过 DNS 解析主机名时应使用的域名。
- `option domain-name-servers <ip-address>, <ip-address>. . .;` 客户端可用的 DNS。DNS IP 地址应按优先顺序列出。
- `option routers <ip-address>, <ip-address>. . .;` 指定客户端子网上路由器 IP 地址的列表。路由器应按优先顺序列出。
- `option subnet-mask <ip-address>;` 指定客户端的子网掩码。
- `default-lease-time number-of-seconds;` 租约有效的持续时间。
- `max-lease-time <number-of-seconds>;` 服务器授予租约的最大秒数。
- `range <low-ip-address> <high-ip-address>;` 要分配给客户端的 IP 地址范围。

![](img/37f079cee226b270f2e09b37a2e4a05d_186_0.png)

要启动 DHCP（图 7-12），请输入命令

```bash
service dhcpd start
```

如果你对 dhcpd.conf 文件进行了更改，必须使用以下命令重启该服务

```bash
service dhcpd restart
```

图 7-12 启动 dhcpd。

![](img/37f079cee226b270f2e09b37a2e4a05d_187_0.png)

租约数据库 /var/lib/dhcp/dhcpd.leases 存储 DHCP 客户端租约。当客户端请求配置信息时，dhcpd 进程会动态修改此文件。如果租约数据库文件不存在，可以使用 touch 命令创建它。touch 命令更新现有文件的访问时间和修改时间。如果文件不存在，则创建该文件。要创建 /var/lib/dhcp/dhcpd.leases 文件，请输入 `touch /var/lib/dhcp/dhcpd.leases`。

### 目标 3.1 DHCP 客户端

配置好 DHCP 服务器后，必须配置客户端。网络上的不同主机配置访问 DHCP 的方式各不相同。最常用的两个客户端是 Linux 和 Windows。要配置 Linux 的 DHCP 客户端，你需要修改两个文件。/etc/sysconfig/network 文件启用网络功能，而 /etc/sysconfig/network-scripts/device-name（其中 device-name 标识要配置的设备）文件启用特定设备的参数。/etc/sysconfig/network 文件应包含以下行：

```bash
NETWORKING=yes
```

这一行表示网络功能已启用。通常系统有一个以太网适配器，但两个以太网适配器也很常见。第一个以太网适配器被标识为 eth0。包含第一个以太网适配器配置的文件是 /etc/sysconfig/network-scripts/ifcfg-eth0。对于 DHCP，该文件应包含以下条目：

```bash
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

通常正在使用的 Windows 版本众多。所有版本的配置方式都类似。此处配置的客户端是 Windows XP。

要在 Windows XP 上配置 DHCP，请从控制面板中选择**网络连接**。（可以通过任务栏上的“开始”菜单访问控制面板。）此时会显示网络连接窗口（图 7–13）。

![](img/37f079cee226b270f2e09b37a2e4a05d_188_0.png)

在“网络连接”窗口中，右键单击“本地连接”图标，然后从弹出菜单中选择**属性**。此时会显示“本地连接 属性”对话框（图 7–14）。

![](img/37f079cee226b270f2e09b37a2e4a05d_188_1.png)

从**此连接使用下列项目：**列表框中选择**Internet 协议 (TCP/IP)**，然后选择**属性**按钮。此时会显示 Internet 协议 (TCP/IP) 属性对话框（图 7–15）。

![](img/37f079cee226b270f2e4a05d_189_0.png)

确保选中了**自动获取 IP 地址**和**自动获取 DNS 服务器地址**选项按钮。

选择**确定**按钮关闭对话框，然后关闭已打开的窗口。此时 DHCP 客户端已准备就绪。

## 静态配置

目标 3.7

在某些网络上，将计算机配置为使用静态 IP 地址是必要的。在一些网络上，使用静态地址可以提高安全性。如果 IP 地址不是自动分配的，那么闯入网络的人必须获取网络地址和子网掩码才能使用网络。通常为服务器分配静态地址，以确保其服务从一个一致的地址提供。

使用静态地址不需要设置服务器；但是，必须配置以太网适配器。如果系统要连接到其他网络，则必须设置网关。如果系统将使用 DNS，则还必须对其进行配置。

要使用网络，必须设置的属性如下：

- 主机 IP 地址
- 主机子网掩码
- 网关 IP 地址
- DNS 服务器 IP 地址
- 主机名
- 域名

### 主机 IP 地址和子网掩码

客户端的静态值设置在以太网适配器上。要在 eth0 适配器上设置静态地址，可以使用**ifconfig** 命令。ifconfig 命令也用于显示网络接口的当前配置。ifconfig 的语法为**ifconfig interface options**。要获取完整选项列表，请使用**man ifconfig**。一些有效选项如下：

- `up` 激活网络接口。
- `down` 关闭网络接口。
- `netmask <address>` 设置子网掩码。
- `<address>` 网络接口的 IP 地址。

要将第一个以太网接口设置为地址 192.168.0.20 和子网掩码 255.255.255.0，请使用以下命令：

`ifconfig eth0 192.168.0.20 netmask 255.255.255.0`

这些属性包含在文件**/etc/sysconfig/network-scripts/ifcfg-eth0**中。可以直接编辑此文件。

### 主机名和网关

可以在**/etc/sysconfig/network**文件中设置主机名和网关。除了 NETWORKING 条目外，/etc/sysconfig/network 文件还可以包含以下条目：

- `HOSTNAME=<value>` 该值是一个完全限定域名 (FQDN)，例如*LinuxServer.linuxplus.com*。
- `GATEWAY=<value>` 该值是网络网关的 IP 地址。

要配置主机名为 myserver、域名为 linuxplus.com 且网关地址为 192.168.0.1，请在**/etc/sysconfig/network**文件中放入以下条目。

```bash
NETWORKING=yes
HOSTNAME=myserver.linuxplus.com
GATEWAY=192.168.0.1
```

### DNS 服务器和域名

域名解析为 IP 地址以便在互联网上使用。要解析这些地址，你必须拥有可使用的本地名称服务器 (DNS) 的 IP 地址。要配置 DNS 服务器，你需要编辑三个文件。

**/etc/resolv.conf**
/etc/resolv.conf 文件是名称解析器的主要配置文件。该文件通常使用三个关键字。使用**man resolv.conf**命令查看所有可用选项。

- `domain <value>` 该值是追加到未限定名称后的域名。例如，如果主机名是 smithcomputer，不是 FQDN，则域名会追加到主机名之后。
- `search <value>` 该值是用于搜索主机名的替代域名列表。
- `name server <ip_address>` 输入要在解析名称时查询的 DNS 服务器的 IP 地址。可以有几个名称服务器条目对应多个 DNS 服务器。

如果主机名是 myserver，且名称服务器位于 IP 地址 192.168.0.250 和 192.168.0.251，则 /etc/resolv.conf 文件中应包含以下条目：

```bash
domain linuxplus.com
search linuxplus.com
name server 192.168.0.250
name server 192.168.0.251
```

**/etc/host.conf**
此文件包含特定于解析器库的配置信息。大多数情况下需要配置两个关键字，order 和 multi。使用**man host.conf**命令可以找到其他关键字。

- `order <value>` 该值指定主机查找的执行方式。该值可以包含 bind、hosts 和 nis。hosts 表示使用 /etc/hosts 文件。
- `multi <on/off>` 如果设置为 on，解析器库将从 /etc/hosts 文件中返回主机的所有有效地址。

