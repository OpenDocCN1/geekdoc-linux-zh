
## 下一步是配置基础网络设置

告诉路由器哪个接口连接到哪个网络。要执行此操作，你需要编辑主网络设置文件（通过主菜单选项 1 进入网络设置子菜单）。主网络设置将在编辑器中打开。你正在设置的路由器将会在网络之间转发消息。因此，你需要设置 `IP` 转发，这意味着你需要将以下行从 `NO` 改为 `YES`：

```
IP_FORWARDING=YES
```

接下来，通过将以下行从 `NO` 改为 `YES`，确保你可以为路由器分配主机名：

```
CONFIG_HOSTNAME=YES
```

现在你可以为以太网分配 `IP` 地址和网络掩码了。找到以下行：

```
IF0_IFNAME=eth0
IF0_IPADDR=dhcp
IF0_NETMASK=255.255.255.0
IF0_BROADCAST=255.255.255.255
IF0_IPMASQ=YES
```

将它们更改为 `eth0` 的正确设置，并通过移除第一行的 `#` 来激活接口：

```
IF0_IFNAME=eth0
IF0_IPADDR=200.200.200.254
IF0_NETMASK=255.255.255.0
IF0_BROADCAST=200.200.255.255
IF0_IPMASQ=YES
```

接下来，找到以下行：

```
IF1_IFNAME=eth1
IF1_IPADDR=192.168.0.20
IF1_NETMASK=255.255.255.0
IF1_BROADCAST=192.168.0.255
IF1_IPMASQ=YES
```

同样将它们更改为 `eth1`（你的内部安全网络）的正确设置并移除井标记：

```
IF1_INTERFACE=eth1
IF1_IPADDR=10.10.10.1
IF1_NETMASK=255.255.255.0
IF1_BROADCAST=10.10.10.255
IF1_IPMASQ=YES
```

这些步骤配置了路由器相应的以太网卡以与分配的网络通信。（确保以太网卡物理上连接到正确的网络。）接下来，注释掉主机信息。在所有与主机相关的行前面加上 `#`。由于这台电脑仅作为路由器使用，通常你不需要分配主机信息。

```
#HOST_IPADDR=192.168.7.123
#HOST_GATEWAY_IF=default
#HOST_GATEWAY_IF=192.168.1.200
#HOST_IPMASQ=NO
#HOST_IPMASQ_IF=default
```

确保正确分配内部和外部网络的网络地址。默认文件包含一个网络的行：

```
NETO_NETADDR=192.168.0.0
NETO_NETMASK=$IF1_NETMASK
NETO_GATEWAY_IF=$IF1_IFNAME
NETO_GATEWAY_IP=default
NETO_IPMASQ=YES
NETO_IPMASQ_IF=$IF0_IFNAME
```

确保将其更改以反映安全网络和不安全网络的配置：

```
NETO_NETADDR=200.200.200.0
NETO_NETMASK=$IF0_NETMASK
NETO_GATEWAY_IF=$IF0_IFNAME
NETO_GATEWAY_IP=default
NETO_IPMASQ=NO
NETO_IPMASQ_IF=$IF0_IFNAME
```

```
NET1_NETADDR=10.10.10.0
NET1_NETMASK=$IF1_NETMASK
NET1_GATEWAY_IF=$IF1_IFNAME
NET1_GATEWAY_IP=default
NET1_IPMASQ=YES
NET1_IPMASQ_if=$IF1_IFNAME
```

最后，配置网关，它是从你的网络到互联网的默认路由。

```
GWO_IPADDR=200.200.200.1
GWO_IFNAME=$IF0_IFNAME
GWO_METRIC=1
```

配置文件的其他部分设置了默认路由，不需要额外的配置。你应该为你的路由器分配一个主机名。更改以下行为你的路由器指定你选择的主机名：

```
HOSTNAME=touretlets
```

现在保存此文件。按 `Ctrl+W` 并按回车保存，然后按 `Ctrl+C` 返回网络配置菜单。在此菜单中按 2 进入 `/etc/network_direct.conf` 文件，你可以在此处设置基本安全。

## 设置基本安全

向 `/etc/network_direct.conf` 文件添加以下行：

```
[ '$IF0$' && ipfwad -F -a -m $SNETWORK1*/24 -D 0.0.0.0/0
```

在不详细介绍 `ipfwad` 细节（你可以在 `http://www.dreamvr.com/ipfwad/ipfwad-faq.html` 找到），请注意该命令执行了以下操作：

- 为从安全网络到外部世界的出站连接启用 `IP` 转发。
- 启用 `IP` 伪装，使得所有出站连接的源地址都是路由器的外部 `IP` 地址，而不是安全网络上的原始主机地址。由于外部人员看不到你安全网络内部的 `IP` 地址，他们无法轻易使用这些地址来破解你的系统。
- 处理所有返回连接，以确保响应出站连接的数据返回到你安全网络内部正确的主机。

现在你可以保存文件（`Ctrl+W`）并退出编辑器（`Ctrl+C`）。

## 进一步的网络配置

针对较新的 `ipchains` 的基本安全超出了本书的范围。有关更多信息，请参阅 Linux 路由器项目文档网站 `lrp.c0w.com` 中的安全链接。这些脚本的一个示例是可以在 `seawall.sourceforge.net` 获取的“Seattle 防墙”。

进一步的网络配置应该是不需要的。例如，查看 `hosts.allow` 和 `hosts.deny` 文件。这些文件设计用于防止路由器本身受到意外攻击，拒绝跨网络远程登录路由器的尝试。换句话说，路由器需要在本地配置，而不是通过网络登录进行配置。保持这些文件不变可能是明智的。

关于防火墙和网络配置的更多信息，请参考 Robert Ziegler 写的《Linux Firewalls》（New Riders, 1999）。

## 保存你的更改

一旦配置好路由器，就有将更改保存回启动软盘。你可以通过在主配置菜单中选择 `b` 来执行。你正在备份 `etc` 模块，是因为你只更改了 `/etc` 目录下的文件。你可以通过从备份菜单中选择 2 来。

将更改写回启动软盘后，你就可以重启系统以启用新配置了。现在你应该拥有了一个作为基本防火墙的运行路由器。

## 深入

使用这些基本原理，利用 Linux 路由器项目发行版来实现（包括其他其他）支持高速互联网连接、`ISDN` 连接和拨号 `PPP` 用户的更高级路由器是可能的。这些都需要额外的模块组合和特定系统的配置。更多信息请访问 Linux 路由器项目网站 `http://www.linuxrouter.org`。

### 展望

在本章中，你看到了 Linux 是多么灵活，允许你将 PC 变成不仅是一个强大的工作站或网络服务器，而且是一个路由器和安全防火墙。

在第 32 章“构建你自己的 Web 服务器”中，你将继续观察网络环境下的 Linux，详细讨论如何使用 Linux 作为内网 Web 服务器。Linux 是一个日益流行的互联网标准 Web 服务器软件平台，可以运行在便宜的硬件上。

事实上，Linux Web 服务器的可靠性和速度使得它们在许多本可以使用高成本商业 Web 服务器解决方案的情况下变得非常受欢迎。

如果你没有 Web 开发或设计背景，本章仍然提供了你自己在组织内开始设置自己的 Web 服务器所需要的的基础知识。

# 第七部分：将 Linux 作为 Web 和电子邮件服务器

- 第 32 章：构建你自己的 Web 服务器
- 第 33 章：Linux 作为邮件服务器：Sendmail 的力量

# 第三十二章：构建你自己的 Web 服务器

- 什么是 Web 服务器？
- Linux Web 服务器
- 安装 Apache
- 配置 Apache
- 管理你的 Web 服务器
- 构建网站

## 第 32 章 • 构建你的 Web 服务器

你在 Linux 学习上已经走了很长一段路，现在你准备好查看 Linux 最受欢迎的应用程序之一：将操作系统作为中小型 Web 服务器的基础。

事实上，Linux 之被广泛用于部署 Web 服务器，出于以下几个原因：

- 它提供了 Unix 的灵活性和管理性。
- 设置和运行成本很低或完全免费。
- 它提供了广泛的工具来构建相当复杂的网站。

本章涵盖了将 Linux PC 转换为内网或互联网 Web 服务器的基础知识。它从 Web 服务器扮演的角色概述开始，检查了可用的主要的 Web 服务器。

它随后提供了关于安装、配置和管理 `Apache`（目前最流行的 Web 服务器）的详细信息。本章通过引导你使用 `Apache` 构建一个简单的网站来结束。在本章结束时，你应该能够使用 Linux 和 `Apache` 创建你自己的网站，并有足够的信心尝试其他的 Web 服务器。

## 什么是 Web 服务器？
