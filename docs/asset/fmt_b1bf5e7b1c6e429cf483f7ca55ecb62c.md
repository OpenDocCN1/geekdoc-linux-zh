
# 配置您的边界 • 第 2 章

- Allow/Deny Service（允许/拒绝服务）：此策略根据目标端口和源允许或拒绝流量。当你使用宽松模式时，可以使用此策略阻止所有 BitTorrent 。流量可以是防火墙本身、局域网客户端或任意的 IP、主机名或网络范围。

“Outbound traffic policy（出站流量策略）”窗口显示了不同的策略组（见图 2.18）。还有额外的单选按钮可以选择“Permissive by default, blacklist traffic（默认宽松，黑名单流量）”或“Restrictive by default, whitelist traffic（默认限制，白名单流量）”。如果你选择宽松选项（默认值），则所有出站连接将被允许，这与防火墙的默认行为相同。如果你选择限制性配置，表的默认目标是 DENY，你创建的任何规则将是 PERMIT（允许）规则。

### 图 2.18 Firestarter 出站策略

![](img/0eb7273a8d9e486628f6e18d37ab22c6_79_0.png)

配置策略将满足你的大部分需求，但通过导航到“Edit | Preferences”（编辑 | 首选项），还有一些额外的配置选项。选择“Interface | Events”（接口 | 事件）允许你配置一些实用工具。“Skip redundant entries”（跳过冗余项）复选框对于连续的事件项仅创建一个事件条目。这有助于防止事件窗口被重复的警报淹没。你还可以选择某些主机或端口免触发事件日志。做出选择后，点击“Accept”（接受）。

另一个值得注意的首选项设置位于“Firewall | Network Settings”（防火墙 | 网络设置）。这允许你启用 Internet共享（与初始向导相同），并将防火墙主机启用动态主机配置协议（DHCP）服务器。这允许你像配置家庭防火墙一样配置 Linux 主机，家庭防火墙通常在执行 NAT 和作为防火墙之外还作为 DHCP 服务器。ICMP 过滤窗口允许你过滤 ICMP 包。默认情况下，Firestarter 为 TCP 和 UDP 配置了允许和拒绝规则，但未针对 ICMP。此屏幕允许你允许所需的 ICMP 流量类型。通常情况下，除非绝对必要，否则最好不要从互联网向你的防火墙或内部网络允许任何 ICMP 流量。

你想配置的最后一个设置位于“Firewall | Advanced Options”（防火墙 | 高级选项）。在广播流量部分，同时勾选广播流量下的两个选项。通常，你不应该允许广播流量通过你的防火墙，因为这样做会带来安全风险。你还需要勾选“Block traffic from reserved addresses on public interfaces”（阻止来自公共接口保留地址的流量）选项，这是一个常见的过滤策略。由于 RFC1918 中概述的“私有”地址不应通过 Internet 路由，因此你的外部接口永远不需要接收源自这些这些地址的流量。如果你收到了，那几乎是黑客试图绕过配置不当的防火墙。

除了任何高级数据包处理器之外，使用 Firestarter 作为你的配置工具无法完成什么。如果你需要实现更高级的配置，请使用替代工具，或者使用 Firestarter 生成配置并将这些链作为起点，添加你自己的更高级的选项。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_80_0.png)

## 简易防火墙生成器 (Easy Firewall Generator)

Firewall Generator 本身并不是一个 GUI，但它有助于简化你的 `netfilter` 配置，并避免熟悉 `iptables` 语法的需要。通过使用 `http://easyfwgen.morizot.net/gen/index.php` 网页，你可以输入相关信息并点击**生成防火墙**（Generate Firewall）按钮。当你选择选项时，如果需要额外信息，点击**生成防火墙**按钮，页面将刷新并提供额外的输入字段。当输入所有所需信息后，页面将变为文本页面，可以复制并粘贴以供 `iptables` 读取并作为保存的配置。在 Fedora Core 5 上，`iptables` 配置存储在 `/etc/sysconfig/iptables`。虽然这种方法需要你用发行版替换默认 `iptables` 配置文件，但它非常简单，并且支持与 Fireaster 相同的所有基本功能。

## 防火墙构建器 (Firewall Builder)

Firewall Builder 是管理 `netfilter` 防火墙最完整的 GUI 工具，其功能和能力与某些商业防火墙产品相当。但这是有代价的：几乎总是如此，就网络 GUI 而言，这种功能和能力意味着 Firewall Builder 不是最容易配置和使用的。然而，如果你想要或需要其卓越的管理能力，那么额外的努力是值得的。（从 `www.fwbuilder.org` 下载 firewall builder）。Firewall Builder 可以很好地管理 `netfilter` 防火墙以及 `ipfilter`、`OpenBSD PF` 和（商业）Cisco PIX。Firewall Builder 运行在许多流行的操作系统上，包括 Red Hat、Mandra、SUSE、FreeBSD、Mac OS X 和 Windows XP。

Firewall Builder 的操作与迄为止所有的 GUI 都不同。它采用基于对象的方法。本质上，你必须定义一个对象来代表你想在防火墙规则中使用的任何实体。在大多数情况下，这些至少包括源、目的和服务（端口）。配置和 GUI 都与 Checkpoint 防火墙 GUI 有相似之处。一旦定义了对象，你就可以将它们拖入规则中，以允许或拒绝它们之间的通信。在这个示例中，我们使用一个 Windows XP 主机运行 Firewall Builder 并配置一个 Linux `netfilter` 防火墙。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_81_0.png)

- 1. 安装 Firewall Builder。
- 2. 通过导航到“开始 | 程序 | Firewall Builder 2.1 | FWBBuilder”启动 GUI，这会打开主 Firewall Builder 窗口（见图 2.19）。它被分为对象树（左侧面板）和对话区域（右侧面板）。

### 图 2.19 Firewall Builder

![](img/0eb7273a8d9e486628f6e18d37ab22c6_82_0.png)

- 3. 初始情况下，对话区域将为空。为了在运行 Firewall Builder 的同一主机上添加第一个防火墙（在此情况下为 `netfilter`），在对象树中选择“Firewalls”（防火墙）。
- 4. 右键点击并选择“New Firewall”（新建防火墙），这将打开“新建防火墙”对话框（见图 2.20）。

### 图 2.20 FWBuild 新建防火墙向导

![](img/0eb7273a8d9e486628f6e18d37ab22c6_83_0.png)

- 5. 在“名称”处输入防火墙名称（在此情况下为 `netfilter`）。
- 6. 在“软件”处选择 `iptables`。
- 7. 在“操作系统”处选择 Linux。
- 8. ICMP 过滤窗口允许你过滤 ICMP 包。手动配置。
- 9. 接口配置窗口见图 2.21。输入接口信息。**名称**必须对应于实际接口，如 `eth0`。**标签**是易于引用的名称，如 `OUTSIDE`。点击“Add”（添加）。
- 10. 输入所有接口信息（通常为 `INSIDE` 和 `OUTSIDE`）后，点击“Finish”（完成）。
- 11. 你必须指定一个接口作为管理接口，通常是 `INSIDE`。通过导航到对象树来实现。接口属性见图 2.22。现在你定义了基础防火墙，你需要定义它要通信的对象。在这种情况下，假设 `192.168.1.0/24` 是你的内部网络，你需要允许出站浏览并访问内部 Web 服务器。首先，你需要创建一个对象来代表内部网络。按照这些步骤创建网络对象。
- 13. 在对象树中导航到“Objects | Networks”（对象 | 网络）。
- 14. 右键点击“网络”并选择“New Network”（新建网络）。
- 15. 在“名称”处输入 `INTERNAL`，并在“地址”字段使用 `192.168.1.0`。在“子网掩码”处输入 `255.255.255.0` 并点击“Apply”（应用）。
- 16. 我们在 `192.168.1.12` 创建一个内部 Web 服务器。在对象树中右键点击“Objects | Hosts”（对象 | 主机）并选择“New Host”（新建主机）。
- 17. 为对象名称输入 `WEB1`。勾选“使用预配置主机对象”框并点击“Next”（下一步）。
- 18. 选择具有一个接口的 PC 并点击“Finish”（完成）。
- 19. 展开对象树的用户 | 对象 | 主机 | `WEB1` | `eth0` | `WEB1`。编辑 IP 地址为 `192.168.1.12` 并点击“Apply”（应用）。
