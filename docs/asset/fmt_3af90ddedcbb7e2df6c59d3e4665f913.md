
图 C-2 设置文件标志后查看文件属性

# sshd_config(5)

OpenSSH 被内置在所有 BSD 操作系统系统的精简基础中，这并不意外——毕竟，OpenSSH 项目是 OpenBSD 项目的一部分。OpenSSH 使得能够轻松地通过安全、加密的连接远程管理系统，并在系统之间安全地 `scp(1)` 和 `sftp(1)` 传输。

虽然 SSH 服务器开箱即用是安全的，但 `sshd_config` 文件允许你进一步加固其安全性。`sshd_config(5)` 提供了所有可能关键字的细节；某些值得研究的包括：

- `AllowUsers`: 允许列出授权连接的用户。
- `MaxAuthTries`: 允许限制每个连接的认证次数。
- `MaxStartups`: 允许你指定并发连接数。
- `PermitRoot`: 指定是否允许超级用户通过 SSH 连接登录。
- `UsePrivilegeSeparation`: 防止权限提升。

> 对此配置文件的更改在重新加载 SSH 守护进程之前不会生效。在 FreeBSD 和 NetBSD 上，你会在 `/etc/rc.d/` 中找到相应的 rc 脚本。

# Blowfish 支持

所有的 BSD 在安装时都带有多种加密算法，包括 Blowfish 算法。Blowfish 设计用于作为其他加密算法的快速、无专利且免许可的替代方案。它还被认为是一种强加密算法，且目前尚未发现任何针对 Blowfish 的成功攻击。

BSD 系统可以配置为在密码数据库中使用 Blowfish 哈希值。在 FreeBSD 系统上，`login.conf(5)` 中启用了 Blowfish 哈希值；在 NetBSD 上，`passwd.conf(5)` 中启用了 Blowfish 哈希值。

# 系统计数

在 BSD 中，`sa(8)` 提供了 Linux `sar(1)` 命令的功能，它是 sysstat 工具包的一部分。`sa(8)` 提供详细的统计数据，例如：

- 每次执行的平均 I/O 操作数
- 每个命令的统计信息，包括调用次数、经过时间、总 CPU 和平均 I/O 操作数
- 每个用户的统计信息，包括调用的命令数、总 CPU 时间和 I/O 操作总数

这些统计数据可以确定系统的基准并监控行为异常。

# IPsec(4)

`IPsec` 用于创建 VPN 以对跨越未保护网络的数据进行加密。`IPsec(4)` 提供了创建 IPsec 头的内核支持。然而，管理密钥交换不需要内核支持；这是通过一个实现 ISAKMP 协议的程序实现的。对于密钥管理，FreeBSD 需要如 `racoon` 之类的第三方应用程序；NetBSD 自带 `racoon(8)`；而 OpenBSD 使用一个名为 `iskampd(8)` 的自定义 ISAKMP 守护进程。

FreeBSD 还提供了一个用于管理 IPsec 隧道所有方面的实用程序 `ipctl(8)`。OpenBSD 4.0 大地简化了 IPsec 配置，其 `ipsec.conf(5)` 提供了多个工作 VPN 配置示例。

# 随机性

生成随机数的能力对于密码学至关重要。内核提供了一个 `/dev/random` 设备，用于收集熵。这些熵随后用于初始化伪随机数生成器 `PRNG`。

# chroot(8)

虽然 `chroot` 用于禁闭一个进程，但 FreeBSD `jail` 用于划分操作系统。`jail` 提供了一个完整的操作系统环境，可以在其中安装、配置并运行应用程序。然而，`jail` 内部发生的任何事情都不会影响操作系统或主机上的其他 `jail`。Jail 受 ISP 欢迎，因为它们为客户提供了安全隔离的环境。

`sysjail` 项目 (`http://sysjail.bsd.lv/`) 为 FreeBSD 提供了 jail 子系统。

# FreeBSD

本部分的其余内容将关注 FreeBSD 特有的其他安全功能。TrustedBSD (`http://www.trustedbs.org`) 的持续目标是创建安全增强。接下来将讨论其中一些功能。

# ACL 解决方案

在传统的 UNIX 权限中，使用组来指定文件的访问。这是有限的。访问控制列表 `ACL` 允许通过 `setfacl(1)` 和 `getfacl(1)` 对文件进行细粒度的控制。ACL 已在 FreeBSD 5.0 中可用。

# MAC 策略

类似于 SELinux，FreeBSD 的强制访问控制 `MAC` 框架提供了一套安全策略。`mac(4)` 描述了可用策略；其中许多策略（如 Biba 和 Lomac）非常复杂，需要高级知识来实现。FreeBSD 手册包含了关于 MAC 的更多信息，访问地址 `http://www.freebsd.org/`。

# OpenBSM

Basic Security Module `BSM` 由 Sun 开发，被认为是事件审计的标准。OpenBSM 是开源实现，并自 FreeBSD 6.2 起已可用。OpenBSM 实现支持审计不同类型的事件，例如：

- 登录
- 配置更改
- 文件和网络访问

OpenBSM 与 Solaris 和 Mac OS 的实现兼容。

# OpenPAM

可插拔认证模块 `PAM` 允许实现替代默认 UNIX 提示用户名和密码认证机制的认证方法。FreeBSD 4.x 使用 Linux 版本的 PAM，但从 FreeBSD 5.0 开始，改用了 OpenPAM (`http://trac.des.no/openpam`)。OpenPAM 也在 NetBSD 3.0 中可用。
OpenPAM 支持的一些替代认证方法包括：

- Kerberos
- RADIUS
- TACACS+
- 处处一次性密码 `OPIE`

# 攻防破解：Linux 安全奥密与解决方案

每个应用程序都有不同的开发团队，其对补丁和告警形式的安全事件的响应速度可能存在巨大差异。管理员如何在不需要订阅几十个安全邮件列表的情况下，对可能发生的安全事件保持警觉？

FreeBSD 项目创建了漏洞与暴露标记语言 `VuXML`，用于记录 FreeBSD 端口程序集合 `ports collection` 的安全问题——该集合包含了近 16,000 个第三方应用程序。

如图 C-3 所示，已知漏洞已被标记，并可以在 `http://www.vuxml.org/freebsd/` 在线查看。OpenBSD 同样在它的端口程序集合中使用了 VuXML，其安全公告可以在 `http://www.vuxml.org/openbsd` 处获取。

一旦某个应用程序存在已知的未修复漏洞，其软件包将从 FreeBSD ftp 镜像站中移除，且该端口的 `Makefile` 被标记为 `FORBIDDEN`。如果你尝试构建此端口，将收到一个包含安全公告链接的错误信息。覆盖此错误并强制构建该端口的唯一方法是手动删除 `FORBIDDEN` 行。

# portaudit(1)

如果你的操作系统能直接告诉你所有安装的软件是否存在已知的安全缺陷，那不是很好吗？在 FreeBSD 系统上，通过输入 `pkg_add -r portaudit` 安装 portaudit 即可轻松实现这一点。该脚本会将当前的 VuXML 条目与系统上安装的软件进行比较，并报告任何已安装软件是否存在未修复的漏洞。

![](img/09ab7f3aec00ce704a89a1cee1c6cf6a_615_0.png)

图 C-3 FreeBSD VuXML Web 界面，按 CVE 名称过滤

报告中包含指向公告的超链接，以便管理员可以评估该漏洞对系统构成的风险。

# gbde(4)

随 FreeBSD 5.0 引入的 GEOM 框架提供了一个磁盘抽象层，允许创建与磁盘交互的模块。这包括创建安全模块，例如基于 GEOM 的磁盘加密 `gbde(4)`。

`gbde` 设计用于保护“冷”存储设备上的数据，免受即使是动机极强的攻击者的侵害。例如，如果攻击者偷取了受保护的磁盘且不知道密码，他/她必须在获取数据之前通过四道加密屏障。然而，`gbde` 并不对针对已连接并挂载文件系统的网络攻击提供任何保护。`man gbde` 的 Examples 部分提供了初始化、挂载和卸载加密设备的命令，以及如何销毁所有主密钥副本。

# geli(8)

`geli(8)` 是另一个用于加密磁盘的 GEOM 模块，随 FreeBSD 6.0 引入。相比 `gbde`，它具有若干优势，包括：

- 加密根分区的的能力
- 支持多种加密算法
- 支持多个独立密钥
- 支持一次性密钥

`man geli` 的 Examples 部分展示了多种加密场景所需的命令。

# NetBSD

本节涵盖了 NetBSD 操作系统的安全特性。NetBSD 4.0 引入了许多安全增强功能，关于这些性的详细描述可以在由 NetBSD 内核开发者 Elad Efrat 编写的一篇文章 (`http://www.securityfocus.com/infocus/1878`) 中找到。

# kauth(9)

`kauth(9)` 引入于 NetBSD 4.0，旨在提供安全策略框架。该框架将允许创建可以插入内核的安全模块。可能的安全模块可以提供如 ACL 支持和 MAC 策略等安全增强。该框架还将移除硬编码的超级用户对系统拥有完全访问权限的概念引用，使得创建限制超级用户权限的策略成为可能。

为了帮助开发者创建安全模块，`secmodel(9)` 提供了一套开发指南。

# veriexec(4)

管理员如何知道系统是否被 root 过？旧的 rootkit 会通过修改二进制文件来隐藏自己，而较新的 rootkit 则尝试通过加载内核模块来隐藏行迹。在大多数操作系统中，使用 `mtree(8)` 来定期检查文件完整性。NetBSD 更进一步，它通过提供 `veriexec(4)` 特性在运行可执行文件之前验证其完整性。与需要手动检查文件的完整性系统不同，`veriexec(4)` 会立即通知入侵者变化。从 NetBSD 4.0 开始，使用 `veriexgen(8)` 生成指纹数据库，然后使用 `veriexctl(8)` 加载到内存中。

# pw_policy(3)

NetBSD 4.0 还引入了密码策略执行功能。它允许管理员强制执行密码长度、大小写、数字、标点符号和字符。策略本身设置在 `passwd.conf(5)` 中。

# fileassoc(9)

该框架引入于 NetBSD 4.0，允许内核关联独立于文件系统的属性。这允许创建如 ACL 等安全属性，而不会对系统性能产生负面影响。

# Audit-Packages

FreeBSD 和 OpenBSD 使用 VuXML 管理漏洞，而 NetBSD 为其 pkgsrc 维护了自己的漏洞列表。列表可以通过 `ftp://NetBSD.org/pub/packages/distfiles/pkg-vulnerabilities` 获取。就像可以在 FreeBSD 系统上安装 auditport 一样，你可以在 NetBSD 系统上安装 audit-packages。audit-packages 脚本会将漏洞列表与安装的软件进行比较并提供建议。

`gd(4)` 允许使用 AES、Blowfish 或 3DES 进行磁盘加密，旨在加密非根分区。它还可以用于加密 CD 和 DVD，并使用一次性密钥加密交换分区和临时文件。

# clockctl(4)

`ntpd(8)` 是一个超级用户权限运行的臃肿进程示例，在安全环境中存在问题，特别是考虑到准确的网络时间是使用 `kerberos(8)` 身份验证系统的必要。`clockctl(4)` 子系统允许 NTPD 以非权限账户运行，从而减少了 NTPD 漏洞的影响。

> OpenBSD 使用了不同的方法——重写了一个较不臃肿的版本 OpenNTPD，并使用了权限分离。

# OPENBSD

OpenBSD 被誉为世界上最安全的操作系统之一。OpenBSD 开发者在设计和发布工程过程中融入了许多安全特性。例如，C 函数 `strcpy(3)` 和 `strcat(3)` (`http://www.openbsd.org/papers/strcpy-paper.ps`) 被重写为更安全的替代品。

维基百科提供了若干安全特性的良好概述和更多参考，访问地址：`http://en.wikipedia.org/wiki/OpenBSD_security_features`，OpenBSD 开发者 Theo de Raadt 有一个关于利用技术的演示：`http://www.openbsd.org/papers/v5-deradt/`

# ProPolice

ProPolice 是由 IBM 开发的针对 gcc 的补丁，旨在保护编译后的应用程序免受缓冲区溢出的攻击。它也被称为栈破坏保护 `SSP`。OpenBSD 项目自 2002 年起一直使用 ProPolice，并提供了第一个

## Hacking Exposed Linux：Linux 安全秘密与解决方案

ProPolice 的真实规模测试。它负责发现并导致修复 OpenBSD 操作系统随附的各种程序中的许多漏洞。

ProPolice 现在已集成到 `gcc 4.1` 中；自 2006 年 7 月以来，该版本一直是 NetBSD 项目使用的 gcc 版本。FreeBSD 的补丁可以在此处获取：`http://tatat.chchile.org/~tataz/FreeBSD/SSP/README.html`。

# W^X

`W^X` 是 Write X 的缩写，这种技术使得进程内存地址空间中的任何页面可以是可写的或是可执行的，但不能者同时具备。这防止了利用程序将想要执行的代码写入内存，从而导致程序执行该代码。`W^X` 自 OpenBSD 3.4 版本起就已可用。Marc Espie 在一次访谈中提供了更详细的描述 (`http://www.onlamp.com/lpt/a/4676`)。

> 注意：NetBSD 使用不可执行栈和堆提供了类似的功能 (`http://netbsd.org/Documentation/kernel/non-exec.html`)。

# systrace(1)

`systrace(1)` 由 OpenBSD 项目开发，并从 2.0 版本开始引入 NetBSD。它用于通过对系统调用执行访问策略来监控和控制应用程序对操作系统的访问。它可以限制服务对操作系统的访问，保护系统免受缓冲区溢出的攻击。其权限提升功能允许管理员在策略中指定需要超级用户权限的特定系统调用，从而移除 SUID 和 SGID 二进制文件。

# 加密交换分区

OpenBSD 支持对交换分区进行 Blowfish 加密。交换空间被分成许多小区域，每个区域分配自己的加密密钥。一旦某个区域中的数据不再需要，OpenBSD 就会通过丢弃加密密钥来删除它。自 OpenBSD 3.9 版本起，此功能默认启用。

# pf(4) 防火墙功能

`pf(4)` 防火墙源于 OpenBSD 项目，并已集成到 FreeBSD 和 NetBSD 的基础安装中。`pf` 是基于内核的，这意味着它非常快；它还是一个功能丰富的状态防火墙，在速度和功能上都可以与商业防火墙相媲美。`pf` FAQ (`http://www.openbsd.org/faq/pf/`) 详细介绍了许多功能并提供了配置示例。接下来我们将描述其中一些功能。

# 状态表的直接操作

管理员可以使用 `pfctl(8)` 直接与 `pf` 交互。除了停止和启动防火墙、查看当前加载的规则集以及状态表和 NAT 表，以及动态添加规则外，`pfctl` 还允许与状态表直接交互。

例如，要立即删除来自攻击主机的所有状态条目，只需指定该主机的 IP 地址：
```
