

![](img/43f64015de86d989e30eff5bb284fb96_728_0.png)

# 图 15-12 IP 表中存储的规则的基本操作

规则是按照你在链中放置的顺序执行的。例如，假设你有以下两条规则。第一条允许来自单个网络的数据包；第二条拒绝所有网络的数据包。

```
# iptables -A INPUT -s 192.168.10.0/0 -j ACCEPT
# iptables -A INPUT -j DROP
```

与你见过的某些其他配置文件一样，规则的顺序很重要。如果你将上述两条规则的顺序颠倒，来自 192.168.10.0 网络的数据包将在更具体的规则允许其访问之前被拒绝。

通常，防火墙规则应从最具体开始，到最一般结束，最后以“捕获”规则结尾，以确保没有任何东西意外通过。

在系统启动时，在网络激活之前，由 iptables 服务激活在你的系统上配置的 NetFilter 规则。文件 /etc/sysconfig/iptables 包含你在系统上配置的规则。在安装 Red Hat Linux 或 Fedora 时，你会回答有关要实施的防火墙保护级别的问题。你选择的级别——低、中或高——决定了每次启动 Linux 系统时执行的 iptables 命令。这些命令通常只构成防火墙的开始；一个将组织连接到 Internet 的服务器可能使用数百条 iptables 命令来设置其网络访问。

表 15-1 列出了 iptables 命令最常用的选项。所有选项都区分大小写。有了本表中的信息，你应该能够查看默认安装中找到的 iptables 命令，并在你的网络上练习新的配置。有关更完整的列表，请参阅 iptables 手册页。

## 表 15-1 iptables 命令的常用选项

| Option | Description |
|---|---|
| -A table | Append a rule to the end of the named table |
| -D table index | Delete rule number index from the named table |
| -F table | Flush (delete) all rules from the named table, or from all tables if no table is named |
| -L table | List all the rules from all tables, or from the named table if given |
| -P table policy | Set the default policy of the named table to the named policy |
| -s address port | Define a source IP address against which to compare a packet; you can include a port number after the address to indicate which TCP or UDP port should match the rule. |
| -d address port | Define a destination IP address against which to compare a packet; a port number can be included as with the -s option |
| -i interface | Specify the network interface (such as eth0) that a packet must use to match the rule |
| -p protocol | Indicate the protocol field of the IP address that will match the rule; the protocol can be TCP, UDP, or ICMP (The protocol specification is not case sensitive) |
| -j target | Define an action for packets matching the packet specifications (such as the -p and -s options) |

## 网络地址转换

IP 表功能提供了一种称为网络地址转换 (NAT) 的特殊路由功能。这是一种更改数据包中的地址或其他信息的路由技术。一种流行的 NAT 类型是 IP 伪装，这是一种网络地址转换类型，其中来自 LAN 上许多计算机的数据包被更改，看起来像是来自一台计算机。这种技术对于连接到 Internet 的组织或家庭网络非常有用，如图 15-13 所示。

使用 IP 伪装，单个 IP 地址可以使整个 LAN 连接到 Internet 或更大的组织网络。DSL 和电缆路由器通常使用这种技术来允许多台计算机访问 Internet。IP 伪装几乎就像一个

![](img/43f64015de86d989e30eff5bb284fb96_730_0.png)

# 图 15-13 IP 伪装

防火墙，因为远程计算机无法连接到伪装 LAN 内的客户端。如果你仔细配置路由器，IP 伪装有效地隐藏了你的整个网络。

设置 IP 伪装需要一条规则，其含义是：“来自此网络的所有网络流量都应被伪装。”假设你有一个使用设备 eth0 的 LAN，其网络地址为 192.168.100.0，你通过电缆调制解调器将其连接到 Internet。使用以下命令在服务器上，所有来自内部网络的网络流量将被伪装；LAN 上的所有客户端然后将能够访问 Internet（尽管 ISP 会将所有流量视为来自网关系统）。nat 表（根据 -t 选项）指的是网络地址转换表；-A POSTROUTING 选项将此规则附加到在做出其他路由决策后使用的规则列表中。

```
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

## 图形防火墙配置实用程序

虽然一旦你习惯了，iptables 命令的语法就很直接，但图形实用程序在设置 Linux 防火墙时仍然非常有帮助。

![](img/43f64015de86d989e30eff5bb284fb96_730_1.png)

> 在图形实用程序能够帮助你配置安全防火墙之前，你需要了解 IP 表和网络协议的工作原理。

Red Hat Linux 和 Fedora，像许多其他 Linux 发行版一样，包含基本的防火墙配置工具，帮助新用户为系统提供一定程度的保护。当你安装 Red Hat Linux 或 Fedora 时，你会回答有关网络安全的基本问题。这些问题使用 system-config-securitylevel 程序提出，你可以随时从命令行执行该程序。（执行相同任务的文本模式程序是 system-config-securitylevel-tui；你也可以使用其旧名称 lokkit 启动此程序。）

图 15-14 显示了图形 system-config-securitylevel 程序的屏幕。此程序不询问你“规则”，而是根据你希望系统的安全性以及你希望保持更开放的任何特定协议设置合理的规则。（请记住，“更安全”意味着“更难使用”，如果你处于受信任的环境中，例如测试实验室，在那里你希望在不为每个服务重新配置防火墙的情况下运行许多网络服务。）

![](img/43f64015de86d989e30eff5bb284fb96_731_0.png)

图 15-14 system-config-securitylevel 程序

由于此程序仅设置概括的“安全级别”，因此系统管理员最好下载（或根据需要购买）更完整的图形解决方案，如果仅使用 iptables 命令似乎效率低下。以下是一些示例：

- GNOME 程序 Firestarter 包含一个防火墙创建向导，帮助你设置基本防火墙。然后你可以在图形界面中根据需要修改基本的 iptables 规则。你还可以观看实时监视器，以查看数据包何时匹配特定规则。你可以通过 firestarter.sourceforge.net 上的下载链接找到此程序。
- Mason 是一种防火墙工具，采用不同的方法，适用于经验较少的 Linux 管理员。不是在开始时定义规则，你启动 Mason，然后启动服务器上要支持的所有其他服务。Mason 准备一份规则列表，智能地仅允许这些服务并阻止所有其他服务。有关更多信息，请访问 http://mason.stearns.org。
- KMyFirewall 是一种基于 KDE 的程序，让你可以设置“个人防火墙”或使用 IP 表保护更大的网络。它包含一个针对经验较少用户的设置向导，以及一个更高级的界面，帮助你创建复杂规则。你可以将防火墙规则的副本保存到单独的文件中，然后使用该文件轻松配置运行 KMyFirewall 的其他防火墙，当应应用相同规则时。有关信息，请访问 http://kmyfirewall.sourceforge.net。
- Linux 上最功能齐全的防火墙配置实用程序之一是 GuardDog。GuardDog 可以使用图形界面或其自己的命令行实用程序。详情请参阅 www.simonzone.com/software/guarddog/。

## 设置 DNS 名称服务器

在第 12 章“配置网络”中，你学习了如何使用 /etc/resolv.conf、/etc/hosts、/etc/host.conf 和 /etc/nsswitch.conf 等配置文件配置 DNS 解析器。在本节中，你将学习如何在 Linux 上创建 DNS 服务器，其他系统可以依赖它来解析主机名和 IP 地址。

你可以将 DNS 中的信息视为 Internet 范围内的倒置层次树，如图 15-15 所示。树的顶部称为根，用句点“.”表示。根通常仅在提及根名称服务器时才被提及——DNS 服务器由运营 Internet 的组织指定为 DNS 查询的起点。更常见的是，你会看到域名最后部分被称为顶级域名，例如 .org、.com、.edu 和 .net，以及许多其他域名。

![](img/43f64015de86d989e30eff5bb284fb96_732_0.png)

图 15-15 DNS 的结构

要解析主机名或 IP 地址，客户端会向 DNS 服务器请求所需信息（例如，“www.google.com 的 IP 地址是什么？”）。DNS 服务器要么可以找到另一个已缓存该信息的 DNS 服务器，要么可以找到 google.com 管理员正式定义其服务器 IP 地址的服务器。找到官方的 google.com DNS 服务器需要更长时间，但 google.com 地址已缓存在许多 DNS 服务器中，因此很少需要这样做。

