
在此示例中，主机首先检查 `/etc/host.conf` 文件并执行 DNS 查找。其他几个选项控制着如何使用名称服务。修改此文件的唯一原因是是你对名称服务使用了 NIS，或者你想要使用其中一个可选服务。`nospoof` 选项对于系统安全可能是一个很好的选择。它会将标准的 DNS 查找与反向查找（主机到 IP，然后从 IP 到主机）进行比较，如果不匹配则失败。缺点通常是当使用代理服务时，查找会失败，因此你需要谨慎地使用它。

# 使用图形化配置工具

Ubuntu 在桌面用户如何使用图形配置工具进行配置方面做了一些重大改进。对于大多数人来说，你需要知识都包含在第 1 章“安装 Ubuntu 和安装后配置”中关于 Network Manager 的章节中。对于其他人，你可以通过右键点击顶栏上的网络图标并从菜单中选择“编辑连接”（Edit Connections），如图 17.1 所示。从打开的“网络连接”窗口，你可以从各种类型的连接中选择进行配置，包括有线、无线、移动宽带、VPN 和 DSL，如图 17.2 所示。默认情况下，每项都设置为自动配置，大多数用户永远不需要更改此处的可用设置。如果你需要需要，只需选择相应的选项卡并点击“添加”（Add）按钮；然后你可以根据需要配置和微调设置，例如图 17.3 中的无线连接示例。

![](img/d9236e4682dfcf03b759a19829a318ef_431_0.png)

图 17.1 使用 `nm-connection-editor` 配置你的网络设备。

![](img/d9236e4682dfcf03b759a19829a318ef_431_1.png)

图 17.2 在网络连接中选择要配置的连接类型。

![](img/d9236e4682dfcf03b759a19829a318ef_432.png)

图 17.3 为主机分配静态 IP 地址。

# 动态主机配置协议

正如其名所示，动态主机配置协议（DHCP）为网络配置主机。DHCP 在主机连接网络时配置 TCP/IP 参数。这些参数包括自动分配 IP 地址、设置 `/resolv.conf` 中的名称服务器以及配置默认路由和网关信息。本节首先描述如何使用 DHCP 获取 IP 地址并启动 DHCP 服务器。

> 注意
> 你可以通过阅读 RFC 2131 了解更多关于 DHCP 的信息

## DHCP 如何工作

DHCP 为客户端提供持久存储：

- 网络子网/主机地址——用于 DHCP 连接网络
- 子网/主机名——启用 DHCP 连接到 DNS
- 子网/硬件地址——启用 DHCP 连接到 DNS

DHCP 还允许分配临时或永久的 IP 地址。当临时分配（称为租约）过期时，客户端可以请求扩展租约，如果不再需要该地址，客户端可以释放该地址。

DHCP 具有一些优势。首先，它将分配 IP 地址的责任从网络管理员（可能会意外分配 IP 地址）转移到 DHCP 服务器。其次，DHCP 更好地利用了 IP 地址。如果用户由于某种原因离开办公室，用户主机可以释放其 IP 地址供其他主机使用。

大多数情况下，DHCP 并不完美。服务器无法通过 DHCP 进行配置，因为 DNS 不知道 DHCP 为主机分配了什么。但是，DHCP 可以根据子网/主机名或子网/硬件标识进行分配。

> 使用 DHCP 通过主机名配置服务器的问题由动态 DNS 解决，充分开发后允许 DHCP 在 DNS 中注册 IP 地址。要克服的最大障碍是允许连接到系统的主机更新 DNS 的安全影响。

## 在安装和启动时激活 DHCP

Ubuntu 自动使用 DHCP 配置你的网络接口，因为这是设置网络接口最简单的方法。对于使用动态或 DHCP 分配的 IP 地址方案，广播地址位于 255.255.255.255，因为用于 IP 配置的 DHCP 客户端最初不知道 DHCP 服务器的位置，请求必须遍历整个网络直到有服务器响应。

你可以在 `/etc/network/interfaces` 中找到使用 DHCP 配置网卡的指令，其中有一行写着 `dhcp`。

其他获取 DHCP 设置的特定设置保存在名为 `dhclient.conf` 的文件中，位于 `/etc/dhcp3/dhclient.conf` 目录中，并有文档记录。

## 动态主机配置协议

在 `dhcpclient.conf` 的 man 页中可以找到。此外，`dhcpoptions` man 页也记录了超过 100 多个选项。

然而，使用 DHCP 并不那么复杂。如果你想使用 DHCP 并知道网络上有一个服务器，你可以按照以下方式使用 `dhcpclient` 快速配置你的网卡：

```matthew@seymour:~ sudo dhcpclient

Internet Systems Consortium DHCP Client V3.1.3

Copyright 2004-2009 Internet Systems Consortium.

All rights reserved.
```

欲了解更多信息，请访问 https://www.isc.org/software/dhcp/

```Listening on LPF/eth0/00:90:f5:82:52:b5
Sending on LPF/eth0/00:90:f5:82:52:b5
Listening on LPF/virbr0/ee:1a:62:e2:a2
Sending on LPF/virbr0/ee:1a:62:e2:a2
Listening on LPF/wlan0/00:16:ea:d4:58:88
Sending on LPF/wlan0/00:16:ea:d4:58:88
Sending on DHCPDISCOVER on eth0 255.255.255.255 port 67 interval 7
DHCPDISCOVER on wlan0 255.255.255.255 port 67 interval 3
DHPOFFER on 192.168.1.106 from 192.168.1.1
DHCPREQUEST on 192.168.1.106 on wlan0 255.255.255.255 port 67
DHCPACK on 192.168.1.106 from 192.168.1.1
nbound to 192.168.1.106 -renewal in 35999 seconds.
```

在这个示例中，第一个以太网设备 `eth0` 已从来自 192.168.1.1 的 DHCP 服务器分配了 IP 地址 192.168.1.106。租约将在 35999 秒后发生，大约是 10 小时。（小贴士：如果你搜索 "35999 seconds in hours"，Google 会为你转换单位。）

# DHCP 软件安装与配置

安装 DHCP 客户端和服务器非常简单，这主要是因为 Ubuntu 在默认安装中已经包含了 `dhcpclient`，同时也因为使用 `synaptic` 或 `apt-get` 安装软件非常方便。

## DHCP 客户端

在安装 Ubuntu 时，DHCP 会自动启用，你不需要担心是否拥有它。DHCP 客户端 `dhcpclient` 发送广播消息，DHCP 服务器将回复适用于你主机的网络信息。获取这些信息后，配置就完成了。

然而，你可以微调 `dhcpclient` 的工作方式以及它存储或查找 DHCP 信息的位置。你可能不需要付出额外的努力；但如果你有需要，可以创建一个名为 `dhcpclient.conf` 的文件，并将你的设置保存在 `/etc` 目录中。

### 注意

你不应该直接用任何旧文件覆盖你的 `dhclient.conf`，因为这样做可能会导致你痛苦的网络问题。相反，请按如下方式复制文件：

```
matthew@weymour:~$ sudo cp /etc/dhcp3/dhclient.conf /etc/dhcp3/dhclient.conf.backup
```
