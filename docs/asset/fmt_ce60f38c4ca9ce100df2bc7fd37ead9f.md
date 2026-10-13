
许多网络现在都提供一种自动配置系统网络接口的服务。它们使用一种名为 `DHCP`（动态主机配置协议）的协议。如果你使用 `DHCP` 配置你的系统，则无需手动配置。所有必要的信息都将自动输入到你的网络配置文件中。

如果你的系统没有到网络的直接硬件连接（例如以太网连接），并且你通过拨号接入网络，那么你可能需要配置拨号器。Linux 中有许多工具可以配置网络。在 Red Hat 上，你可以使用 `Linuxconf` 或 `netcfg` 来配置网络。

### 启动脚本

```bash
#!/bin/sh

# ...
if [ -f /usr/X11R6/usr/X11R6/bin/wmaker ]; then
  exec /usr/bin/wmaker
else
  exec fwwm2
fi
```

## 第 VII 部分：网络管理

## 目录

- 第 36 章：配置网络连接
- 第 37 章：NFS、NIS 和 AppleTalk
- 第 38 章：Samba
- 第 39 章：管理 TCP/IP 网络
- 第 40 章：网络安全：防火墙、加密和认证

## 第 36 章：配置网络连接

### 概述

大多数发行版允许你在安装期间配置网络。如果你这样做了，你的系统就已经就绪了。如果你以后需要更改配置，可能会发现本章的信息很有帮助。在你的 Linux 系统上管理和配置 TCP/IP 网络并不复杂。你的系统使用一组配置文件来设置和维护网络。第 39 章中的`[表 39-2]`提供了完整的列表。

与其编辑配置工具，你可以使用许多发行版包含的 GUI 或基于光标的配置工具，它们会提示你输入网络信息。许多发行版将此类网络配置集成到安装过程中。如果你选择在配置期间不配置网络，或者需要更改它，你可能会发现使用网络配置工具更简单更安全。在 Red Hat 上，你可以使用 `Linuxconf` 或 `netcfg` 来配置网络。

许多网络现在都提供一种自动配置系统网络接口的服务。它们使用一种名为 `DHCP`（动态主机配置协议）的协议。如果你使用 `DHCP` 配置你的系统，则无需手动配置。所有必要的信息都将自动输入到你的网络配置文件中。

如果你的系统没有到网络的直接硬件连接（例如以太网连接），并且你通过拨号接入网络，那么你可能需要配置拨号器。Linux 中有许多工具可以配置网络。在 Red Hat 上，你可以使用 `Linuxconf` 或 `netcfg` 来配置网络。

### 启动脚本

在 Red Hat 上，网络接口通过 `/etc/init.d/` 下的脚本启动。*(此处对应原文中重复的启动逻辑描述)*

针对不同的操作系统，提供了多种 DHCP 服务器和客户端。对于 Linux，你可以从互联网软件联盟 `ISC` 的网站 `www.isc.org` 获取 DHCP 软件。该软件包包含 DHCP 服务器、客户端和中继代理。Linux 包含一个 DHCP 服务器，其 DHCP 客户端名为 `dhcpd`。DHCP 客户端下载的网络信息保存在其 `/etc/dhcp` 目录下的网络配置文件中。例如，你可以在这里找到你网络服务器的 `resolv.conf` 文件。

### 配置 DHCP 客户端

配置主机使用 DHCP 服务器非常简单，只需为主机的网络接口设备（如以太网卡）设置选项。对于 Red Hat 主机，你可以使用 `netcfg` 设置主机自动连接到 DHCP 服务器获取网络信息。在“接口”`Interface`面板上，点击主机的网络接口设备，例如第一块以太卡的 `eth0`。然后点击“编辑”`Edit`。从标记为“配置协议”`Configuration Protocol`的弹出菜单中选择 `/etc/sysconfig/network-scripts` 目录下该接口网络脚本中的 `BOOTPROTO` 条目，例如第一块以太卡的 `ifcfg-eth0`。你也可以手动编辑此内容。

```
BOOTPROTO=dhcp
```

务必使用网络脚本重启网络设备以使更改生效。

在 Windows 客户端上，找到你网络网卡的 TCP/IP 条目，然后打开其属性窗口。勾选“自动获取 IP 地址”`Obtain IP address automatically`复框。然后找到 WINS 面板（通常通过点击“高级”按钮），并选择 DHCP 作为你想要使用的协议。

### 配置 DHCP 服务器

在 Red Hat 上，你可以使用 `/etc/rc.init.d` 目录下的 `dhcpd` 命令停止和启动 DHCP 服务器。使用 `service` 命令配合 `start`、`restart` 和 `stop` 选项。以下示例显示了 DHCP 服务器。使用 `stop` 参数关闭它，`restart` 将将其重启。

```
service dhcpd start
```

DHCP 服务器的配置文件保存在 `/etc/dhcpd.conf` 中，你可以在这里定义 DHCP 服务器如何访问网络上不同 DHCP 客户端的参数。全局参数适用于所有客户端。你可以进一步创建声明来引用定义特定的客户端或客户端组。在这些声明中，你可以输入仅适用于那些客户端的参数（见表 36-1）。声明使用针对不同类型客户端组的不同语句来实现。例如，要为特定主机定义声明，你可以使用所示所示 `host` 语句：

```
host 192.168.1.2 (
  parameters)
)
```

### 表 36-1: DHCP 声明、参数和选项

| 条目 | 说明 |
| --- | --- |
| **声明** `Declarations` | |
| `shared-network` | 用于标记某些子网是否共享相同的网络。 |
| `subnet subnet-number netmask` | 引用整个地址子网。 |
| `range [dynamic-boot] low-address; high-address];` | 为为动态分配的 IP 地址提供最高和最低范围。 |
| `hostname` | 引用特定的主机。 |
| `group` | 允许你对一组参数和声明进行标记，并使用该标签将它们应用于子网和主机。 |
| `allow unknown-clients; deny unknown-clients;` | 不向未知客户端动态分配地址。 |
| `allow bootp; deny bootp;` | 是否响应 bootp 查询。 |
| `allow booting; deny booting;` | 是否响应启动查询。 |
| **参数** `Parameters` | |
| `default-lease-time time;` | 分配给租期的秒数。 |
| `max-lease-time time;` | 租期的最大长度。 |
| `hardware hardware-type address;` | 网络硬件类型（以太网或环形网络）和地址。 |
| `filename "filename";` | 初始启动文件名。 |
| `server-name "name";` | 客户端启动的服务器名称。 |
| `next-server-name;` | 加载 `filename` 中指定的初始启动文件的服务器。 |
| `fixed-address address [, address ...];` | 为客户端分配固定地址。 |
| `get-lease-hostnames flag;` | 是否查找并使用客户端的 IP 地址。 |
| `authoritative; not authoritative;` | 拒绝无效的地址请求。 |
| `server-identifier hostname;` | 指定服务器。 |
| **选项** `Options` | |
| `option subnet-mask ip-address;` | 客户端的子网掩码。 |
| `option routers ip-address [, ip-address ...];` | 客户端子网上的路由器 IP 地址列表。 |
| `option domain-name-servers ip-address [, ip-address ...];` | 客户端使用的域名服务器列表。 |
| `option log-servers ip-address [, ip-address ...];` | 客户端使用的日志服务器列表。 |
| `option host-name string;` | 客户端的主机名。 |
| `option domain-name string;` | 客户端的域名。 |
