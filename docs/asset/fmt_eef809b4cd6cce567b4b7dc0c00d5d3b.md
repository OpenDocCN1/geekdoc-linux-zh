
| | IN | MX | 10 mail | | | | |
| | IN | MX | 20 mail.max.net. | | | | |
| speedy | IN | A | 192.168.0.1 | | | | |
| grape | IN | A | 192.168.0.3 | | | | |
| potato | IN | A | 192.168.0.4 | | | | |
| peach | IN | A | 192.168.0.6 | | | | |

# 第 25 章 DNS/BIND：跟踪域名和地址

`zach.net` 区域文件的公共版本如下：

```
$ cat public.net
; zach.net public zone file
;
$TTL 30D
@ IN SOA ns.zach.net. mgs@sobell.com. (
                               200711118 ; serial
                               8H ; refresh
                               2H ; retry
                               4W ; expire
                               1D ; minimum
)

IN TXT "Sobell Associates Inc."
IN NS ns ; Nameserver address (unqualified)
IN NS ns.speedy.net. ; Nameserver address (qualified)
IN MX 10 mail ; Mail exchange (primary/unqualified)
IN MX 20 mail.max.net. ; Mail exchange (2nd/unqualified)
www IN CNAME ns
ftp IN CNAME ns
mail IN CNAME ns
s IN A 192.168.0.1
IN A 192.168.0.6
IN MX 10 mail
IN MX 20 mail.max.net.
```

这里是两个反向区域文件，每个文件都以 SOA 和 NS 资源记录开头，随后是每个服务器名称的 PTR 资源记录。该文件的本地版本还列出了本地系统的名称：

```
$ cat named.local
; "0.168.192-in.arpa" reverse zone file
;
$TTL 30D
@ IN SOA ns.zach.net. mgs@sobell.com. (
                               2007110501 ; serial
                               8H ; refresh
                               2H ; retry
                               4W ; expire
                               1D ; minimum
)

IN NS ns ns.zach.net.
1 IN NS ns.speedy.net.
1 IN PTR gw.zach.net.
1 IN PTR www.zach.net.
1 IN PTR ftp.zach.net.
1 IN PTR mail.zach.net.
1 IN PTR speedy.zach.net.
3 IN PTR grape.zach.net.
4 IN PTR potato.zach.net.
6 IN PTR peach.zach.net.
```

## 总结

DNS 将域名映射到 IP 地址，反之亦然。它以分布式数据库的形式实现。有两种查询类型：迭代和递归。持有区域数据的主服务器是权威的。从缓存也是权威的。DNS 保护区域。许多类型的资源记录包括 `A`、`MX`、`NS` 和 `SOA`。

## 练习

1. 什么是 BIND？
2. 哪种 DNS 是返回的？
3. 资源记录用于什么？
4. 如何从命令行设置 DNS？
5. 如何指示服务器处理 `192.168.1.254`，如果 DNS 缓存不可用？
6. 如何指示服务器响应？
7. 如何找到域名的地址？

## 高级练习

8. 如何设置一个不包含任何分配域名的私有层次结构？
9. 哪种 DNS 最容易受到用户的攻击？
10. 更改记录时等待 DNS 记录更新通常令人厌恼。可以通过设置小的 TTL 来避免这种延迟。为什么将 TTL 设置得很小不好？
11. 概述一种可以使用 DNS 支持加密的方法。

# 第 26 章 firestarter 和 iptables：设置防火墙

## 本章内容

- 使用 firestarter 向导快速启动防火墙
- firestarter：维护防火墙
- iptables 如何工作
- 规则、匹配、目标和链
- iptables 命令的构造
- 构建规则集
- 在内核之间复制规则
- 使用 NAT 共享互联网连接

`firestarter` 工具是 `iptables` 的易用图形界面；`firestarter` 构建并操作 Linux 内核中的网络包过滤规则。你可以使用 `firestarter` 或直接使用 `iptables` 创建一个通过设置简单和复杂的网络过滤解决方案来保护系统的防火墙，并设置 NAT（网络地址转换），这允许多个系统共享单个互联网连接。此外，`firestarter` 可以控制 DHCP 服务器。

`iptables` 工具具有灵活且可扩展性，允许你设置简单和复杂的网络过滤解决方案。它提供了连接跟踪（状态包过滤），允许根据连接状态处理数据包。例如，你可以设置规则拒绝尝试打开新连接的入站包，并接受对本地发起连接的响应入站包。许多 `iptables` 基础包中未包含的功能可以通过 `patch-o-matic` 程序作为补丁可用。

## 关于 firestarter

`firestarter` 经常足以用于保护单个系统或小型局域网（LAN），由于其用户友好的特性，它并没有提供对 `iptables` 完整复杂性和功能的访问。对于熟悉基础网络的人来说，涉及 `firestarter` 的大多数概念可能已经熟悉，或者很容易学习。完全理解 `iptables` 所需的某些概念超出了本书的范围。尽管你可以在不同层级使用 `iptables`，但本章仅介绍基础。然而，本章的某些章节深入了可能需要额外理解或解释的领域。如果某个概念不清楚，请参考“更多信息”中的资源。

`firestarter` 是一个用于构建和维护防火墙的图形化工具。尽管它基于 GTK 并在 GNOME 下设计，但在 KDE 环境下同样适用。这使得系统能够与局域网上的其他系统共享 Internet 连接。你还可以设置和配置 DHCP 服务器。它提供了入侵和其他事件的实时视图，允许你调整 ICMP 参数以帮助阻止 DoS 攻击。在安装状态下，`firestarter` 允许出站连接，并显示受保护系统或局域网之外的入站连接信息（即源自 Internet 的连接）。当你查看这些事件时，可以设置规则允许它们，从而实现防火墙的自定义。

`firestarter` 可以保护其运行的系统（防火墙主机上），也可以保护其运行的系统以及通过防火墙主机连接到 Internet 的局域网上的其他客户端系统。图 26-1 显示了一个典型的设置，其中所有进出局域网的网络流量都必须通过防火墙，使防火墙能够控制 Internet 与局域网之间的访问（包括防火墙主机）。在此设置中，防火墙主机充当了路由器。

### 图 26-1 典型的防火墙设置

## 前提条件

安装以下包：

- `firestarter`
- `dhcp3-server` –（仅在你想要 `firestarter` 运行 DHCP 时需要）

安装 `firestarter` 包时，你必须在 `firestarter` 启动之前运行防火墙向导（参见“快速启动：使用 firestarter 防火墙向导构建防火墙”部分）。配置完成后，`firestarter` 会在每次启动系统时自动运行。虽然有一个初始化文件，但你不需要手动运行它；使用 `firestarter` 开启或关闭防火墙以锁定系统，使没有网络流量进入或离开系统。当你启动系统时，`firestarter` 将处于你关闭系统时的状态。无论其 GUI 是否显示，`firestarter` 都会运行。

## 注释

术语 本节解释了在解释 `firestarter` 时使用的某些词汇的含义。`firewall` 和 `firestarter` 术语交替使用。

- **（防火墙）主机（系统）**：运行防火墙的系统。
- **客户端系统**：与客户端主机处于同一局域网的系统，其进出局域网外部系统（特别是 Internet）的数据包都通过防火墙主机传输。
- **策略**：防火墙应用的一组规则。
- **规则**：一个指定防火墙如何处理从其网络接口上特定系统接收的特定类型数据包的语句。
- **连接**：在 TCP 下，两个系统交换数据的路径。客户端系统通过向服务器发送 SYN（同步）包来与服务器建立连接。服务器向客户端返回 ACK（确认）包，两个系统交换数据。客户端用 SYN 包关闭连接。尽管 UDP 的工作方式不同，因为它没有连接的概念，但为了讨论起见，UDP 连接的概念是合适的。
- **入站连接**：包括源自 Internet 并以防火墙主机为目的的连接。
- **出站连接**：包括源自防火墙主机并以 Internet 为目的的连接。

### 图 26-2 防火墙向导：欢迎使用 Firestarter

默认情况下，`firestarter` 实现了一种用户友好的策略来保护防火墙主机和客户端系统。通常，它允许出站流量并阻塞不是出站流量响应的入站流量。具体而言，默认的 `firestarter` 策略：

- 阻塞来自 Internet 的指向防火墙主机或客户端系统的新入站连接。
- 允许响应防火墙主机或客户端系统发起的 Internet 连接的入站包。
- 允许防火墙主机建立连接。
- 允许客户端系统连接到 Internet。
- 不允许客户端系统连接到防火墙主机。

在使用防火墙向导设置 `firestarter` 后，你可以修改默认策略以满足你的需求。

虽然 `firestarter` 是 `iptables` 的前端，但它并不像 `iptables` 那样存储规则（使用 `iptables-save`）。相反，它将配置信息以其开放格式保存在 `/etc/firestarter` 目录树中。

## 更多信息

Web: fs-security.com

## 快速启动：使用 firestarter 防火墙向导构建防火墙

防火墙向导和 Firestarter 窗口允许你设置和控制 `firestarter`。要显示此窗口，选择主菜单 -> firestarter 或在终端中输入命令 `sudo firestarter`。

### 图 26-3 网络设置屏幕

当你第一次运行 `firestarter` 时，它会打开防火墙向导，帮助你配置 `firestarter`。你可以通过选择 Firestarter 菜单：Firewall -> Run Wizard 随时运行此向导。向导的最后一步允许你启动防火墙并显示 Firestarter。

**设备**：第一个防火墙屏幕欢迎使用 `firestarter`；点击“下一步”开始。防火墙向导显示网络设备设置。在此，你选择连接到 Internet 的设备。如果本地系统作为路由器运行，确保选择连接到 Internet 的设备，而不是连接到局域网的设备。如果本地系统使用调制解调器连接到 Internet，勾选“拨出时启动防火墙”。

如果你想运行 DHCP，勾选“IP 地址由 DHCP 分配”。你也可以使用 Firestarter 菜单：Edit -> Preferences 配置 DHCP。如果 `firestarter` 将控制 DHCP，你必须安装 DHCP 包。点击下一步。

**NAT（连接共享）**：Internet 连接共享设置屏幕允许你使用 NAT，以便局域网上的系统共享单个 Internet 连接。此窗口仅在安装防火墙的系统具有两个网络连接时出现。如果防火墙主机将作为路由器并共享 Internet 连接，请勾选“启用连接共享”；否则跳过此屏幕。当你勾选此框时，`firestarter` 允许你选择连接到局域网的设备（而不是连接到 Internet 的设备）。勾选“本地网络启用 DHCP”将导致 `firestarter` 运行 DHCP。勾选此框，点击 DHCP 服务器详情旁边的三角形以选择是否与任何 DHCP 配置保持一致或创建一个新的。服务器名称可以是 DHCP 服务器的 IP 地址或名称。如果您将名称设置为 `<dynamic>`，`firestarter` 将在运行时确定 DHCP 服务器的 IP 地址，这在服务器使用 DHCP 分配 IP 地址时非常有用。点击“下一步”。

**启动防火墙**：在“准备好启动防火墙”窗口中，您可以选择启动防火墙。防火墙将保持在安全模式下运行，该模式虽然可以提供保护，但可能会给某些用户带来麻烦，并且不允许互联网上的系统访问防火墙之前的服务器。如果您从远程系统配置防火墙，一旦启动了防火墙，您将无法继续使用 `firestarter`。如果您想立即启动防火墙，请勾选标记“立即启动”复选框。点击“保存”。

### 图 26-4 互联网连接共享设置

### 图 26-5 准备好启动防火墙屏幕

## firestarter：维护防火墙

在配置 `firestarter` 之后，您可以从 Firestarter 窗口中更改策略。运行防火墙向导程序后，`firestarter` 会显示此窗口。您可以随时按照“快速启动”部分开头的指令重新显示此窗口。无论 Firestarter 窗口是否显示，防火墙都会运行。当您启动系统时，防火墙将恢复到您关机时所的状态（运行、停止或锁定）。

## 状态选项卡

Firestarter 状态选项卡显示了防火墙的概览。此选项卡可以显示到防火墙的活动连接。工具栏允许您更改防火墙的状态并指定偏好设置。窗口中防火墙框架内的大型圆形图标指示防火墙的状态：

- **已禁用**：防火墙已关闭——就像没有安装 `firestarter` 一样。
- **已活动**：防火墙已启动并运行，正在执行您设置的策略（或默认策略）。
- **已锁定**：防火墙已启动并拦截所有数据包。数据无法通过 `firestarter` 控制的网络接口进入或离开防火墙主机。

点击工具栏上的相应图标来更改防火墙的状态。当防火墙根据规则拦截数据包时，会发生事件。防火墙框架列表中的“事件”列列出了防火墙拦截的入站和出站事件数量，并指示了这些事件中有多少个是严重性质的。

### 图 26-6 展开了活动连接的状态选项卡

### 图 26-7 事件选项卡，右键菜单

如果这些事件可能是恶意用户尝试访问系统的行为，则被认为是严重的。例如，被拦截的使用 ssh 登录尝试是一个严重事件；被拦截的 ping 则不是。

“网络”框架显示了系统每个连接的活动情况。

当您点击“活动连接”左侧的小三角形时，`firestarter` 会显示一个可滚动的活动连接列表；拉伸窗口可以显示更多连接。点击此列表中的某行进行选择，然后右键点击并选择“查找主机名”，将“源”和“目的”列中的值从 IP 地址更改为主机名。“端口”列列出了连接在目标主机上的端口。“服务”列指示了与指定端口关联的服务。“程序”列显示了运行的程序名称（如果它是本地的或是 `firestarter` 已知的）。

## 事件选项卡
