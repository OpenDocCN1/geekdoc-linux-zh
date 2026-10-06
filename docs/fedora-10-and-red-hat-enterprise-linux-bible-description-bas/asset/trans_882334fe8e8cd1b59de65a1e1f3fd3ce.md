

# 第 25 章：通过 DNS 公开服务器

- [DNS 放大攻击](http://www.isotf.org/news/DNS-Amplification-Attacks.pdf) — 包含了 DNS 放大攻击的描述，此类攻击通过 DNS 服务器链递归进行 DDoS 攻击。

请参考 ISC Bind 网站获取与 DNS 服务相关的安全警报。

# 理解 BIND

在 Fedora、Red Hat Enterprise 以及其他 Linux 和 UNIX 系统中，你通过使用伯克利域名系统（BIND）软件来实现服务。互联网软件联盟维护着 BIND（地址为 http://www.isc.org/sw/bind）。在本章中描述的 BIND 特定版本是 BIND 9.5。要按照本节描述的方法使用 BIND，你需要安装这些包：bind、bind-utils、bind-chroot 和 bind-libs。我们还使用了 system-config-bind 包，它包含了一个用于图形化操作你 DNS 文件的文件的工具。

对于最新版本的 Fedora 和 RHEL 发行版，BIND 可以配置为在更改根目录（chroot）环境中运行（前提是您安装了 bind-chroot 包）。这意味着配置文件不再像以前在 /etc 和 /var/named 中那样，而是位于 /var/named/chroot/ 中，这是一种安全措施，旨在限制入侵者通过控制 named 守护进程可能获得的访问权限。SELinux 也经过配置以限制对 named 和 nscd 守护进程的访问（详情请参见安全级别配置）。

> 注意：由于 /etc/named.conf 文件和 /var/named/ 目录下的文件与 /var/named/chroot/ 中的对应文件已链接，你可以在任何一个目录中编辑这些文件。但是，当你向 /var/named/chroot/var/named 目录添加区域文件时，你需要在 /var/named/chroot/var/named 目录中创建新的链接，以便从该位置继续编辑。

BIND 的基本组件包括：

- DNS 服务器 (/usr/sbin/named) — named 守护进程监听端口（默认端口 53）以接收 DNS 服务请求，并根据你创建的配置文件中的信息满足这些请求。大多数情况下，named 接收将你的域名主机主机解析为 IP 地址的请求。

> 注意：named 守护进程实际上是从 /etc/init.d/named 启动脚本启动的。你需要设置该脚本在你的 DNS 服务器准备就绪时自动启动。你也可以使用 named 启动脚本来检查 named 守护进程的状态。

- DNS 配置文件（named.conf 文件和 name 目录） — /var/named/chroot/etc/named.conf 文件是你添加定义你的域名 DNS 服务所需的大部分通用配置信息的地方 /var/named/chroot/var/named 目录中的单独文件是关于区域的特定信息。在 Fedora 和 RHEL 中，chroot（/var/named/chroot）DNS 配置文件的位置位于 /etc/sysconfig/named 文件。注意：如果你在非 chroot 环境下运行 BIND，配置文件位于 /etc/named.conf 文件和 /var/named 目录。你必须卸载 bind-chroot 包。

- DNS 查找 — 你可以使用几个工具来检查你的 DNS 服务器主机解析主机。这些工具包括 host、dig 和 nslookup（属于 bind-utils 软件包）。

为了正确维护你的 DNS 服务器，你还可以对 DNS 服务器执行以下配置任务：

- 日志 — 你可以指定日志以及文件所在地。
- 远程服务器选项 — 你可以为特定的 DNS 服务器设置选项，以执行来自坏服务器的阻塞、设置加密密钥或定义传输方法。

你不需要向每个请求 DNS 信息的人。你可以根据以下内容限制对 DNS 服务器的访问：

- 访问控制列表 (acl) — 此列表可以包含你想要分组的主机、域名或 IP 地址，你创建 acl 记录来分组这些地址，然后指示 acl 可以或不能访问域名信息。
- 监听端口 — 默认情况下，你的名称服务器接收来自端口 53 的名称服务器请求。如果你希望你的名称服务器接受不同端口的服务查询，可以添加更多端口。
- 身份验证 — 为了验证请求 DNS 服务器服务的机的身份，你可以使用密钥进行验证和授权（key 和 trusted-keys 语句用于验证）。

> 交叉引用：你应该已经什么是域名和 IP 地址。如果需要刷新记忆，请参考第 15 章的 IP 地址和第 16 章的 DNS 信息。

# DNS 服务器示例

为了了解如何设置 DNS 服务器，以下章节通过一个 exampledomain.com 的 DNS 服务器示例向你展示。在示例中，你正在为一个小型办公室网络创建一个 DNS 服务器，包括：

- 一个位于防火墙后的私有本地网络
- 一个提供 DNS 服务的服务器

在这个办公室中，LAN 中的其他计算机使用相同的互联网连接进行外部通信，服务器上的防火墙进行地址转换（NAT），以便客户端使用防火墙作为访问互联网的路由器。图 25-1 显示了 exampledomain.com 的配置。

图 25-1 展示了一个共享互联网连接的小办公室网络。DNS、Web、mail 和 FTP 服务器都有公共 IP。（这些地址是虚构的，请不要尝试使用。）DNS 服务器（同时作为防火墙运行）后面是四个具有私有地址的客户端（你可以复用第 15 章中描述的这些和其他私有地址）。

> DNS 的工作，但它并没有处理你在设置公司计算基础设施时可能遇到的所有复杂性。例如，你可能想要一个专用防火墙来保护你的互联网连接，将 DNS 服务器放在后面，这被称为与公司局域网隔离的非军事化区（DMZ）。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_1018_0.png) 图 25-1：示例 exampledomain.com DNS 服务器结合了公共服务器和私有客户端。

在此配置中，DNS 服务器的工作是将公共服务器名称（www.yourdomain.com、mail.yourdomain.com、ftp.yourdomain.com 和 ns1.yourdomain.com）映射到 ISP 分配的静态 IP 地址（对于我们的示例，123.45.67.1、123.45.67.2、123.45.67.3 和 123.45.67.8）。DNS 服务器还从 LAN 上的私有地址提供 DNS 服务，因此每个计算机都可以访问 LAN 上的其他计算机，而不需要在自己的 /etc/hosts 文件中存储所有计算机。

该示例的一个关键特性是将该域名的视图分为外部可见和私网络计算机可见。使用 BIND 的 view 功能，我创建了一个外部视图，让互联网的查询只发现域名内的公共服务器（Web、Mail 和 FTP）。然后我创建了一个内部视图（inside view），让本地 LAN 的查询可以发现域名内的公共服务器和私有计算机（红色、蓝色、绿色和黄色）。

下面的章节描述了如何为 25-1 中的示例设置 DNS 服务器。

# 快速启动 DNS 服务器

随 Fedora 和 RHEL 版本一起提供的 DNS 服务器软件是伯克利域名系统（BIND）9.5 版本。要配置 BIND 9.5，你将处理以下：

- 配置文件 (/var/named/chroot/etc/named.conf) — 主 DNS 配置文件。
- 区域目录 (/var/named/chroot/var/named) — 包含互联网根服务器信息（named.ca 文件）以及你创建的区域信息的目录。
- 守护进程 (/usr/sbin/named) — 监听 DNS 请求并响应 named.conf 文件呈现信息的守护进程。

- 调试工具（named-checkconf、named-checkzone 和 named-compile） — 你用于判断创建的配置是否正确的工具。

> 注意：Fedora 和 RHEL 提供了一个名为 system-config-bind 的图形化配置 BIND 工具。（输入 yum install system-config-bind 进行安装）。如果你决定使用该工具，在手动编辑 BIND 配置文件时需要小心。建议如果对 named.conf 有某些 system-config-bind 窗口不支持的更改，你应该将这些更改放在 /etc/named.custom. 文件中。

BIND 9.5 还包含了用于创建 DNSSEC 安全服务器的工具。通过使用这些工具，你可以创建并生成密钥来提供身份验证和安全的地址解析。这些章节中的示例不包含 DNSSEC 配置。

为你的示例创建 DNS 服务器的基本步骤如下：

- 识别你的 DNS 服务器
- 创建 DNS 配置文件
- 监控 named 活动

