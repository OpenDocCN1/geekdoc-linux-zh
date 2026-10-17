
```
chflags schg -R /bin /sbin /usr/bin /usr/sbin
```

在 Linux 中，使用 `lsattr(1)` 来查看文件属性。在 BSD 中，你需要在长列列表中添加 `o` 选项，如图 C-2 所示。`schg` 表示该二进制文件设置了系统不可变标记。只有超级用户可以移除此标记，取决于 `securelevel`，他或她可能必须将系统降至单用户模式。

# ttys(5)

在 Linux 中，使用 `initabb` 来配置可用数量以及何种类型的 tty；BSD 的等效工具是 `ttys(5)`。在 BSD 中，你还可以将一个 tty 设置为“不安全”，这意味着它不会接受超级用户登录。将控制台（第一个 tty）设置为不安全，将要求在系统降至单用户模式时输入超级用户密码。

# Hacking Exposed Linux：Linux 安全机密与解决方案

```
$ ls -lo /bin/ls
-r-xr-xr-x 1 root  schg 23240 May
```

图 C-2 设置文件标记后查看文件属性

# sshd_config(5)

OpenSSH 被内置在所有 BSD 操作系统的最小基础中，这并不令人意外——毕竟，OpenSSH 项目是 OpenBSD 项目的一部分。OpenSSH 使得能够轻松地通过安全的加密连接远程管理系统，并在系统之间安全地 `scp(1)` `sftp(1)` 文件。

虽然 SSH 服务器开箱即是安全的，但 `sshd_config` 文件允许你进一步加固其安全性。`sshd_config(5)` 提供了所有可能关键字的细节；某些值得研究的包括：

- `AllowUsers`：允许你列出哪些用户授权连接。
- `MaxAuthries`：允许你限制每个连接的身份验证尝试。
- `MaxStartups`：允许你指定并发连接数。
- `PermitRootLogin`：指定是否允许超级用户通过 SSH 连接登录。
- `UsePrivilegeSeparation`：防止权限提升。

> 对此配置文件的更改在重新加载 SSH 守护进程之前不会生效。在 FreeBSD 和 NetBSD 上，你会在 `/etc/rc.d` 中找到用于 `sshd` 的 rc 脚本。

# Blowfish 支持

所有的 BSD 在安装时都带有若干种加密算法，包括 Blowfish 算法。Blowfish 的设计旨在作为其他加密算法的快速、无专利且无需许可的替代方案。它目前还被认为是一种强加密算法，目前尚 unknown任何针对 Blowfish 的成功攻击。

BSD 系统可以配置为在密码数据库中使用 Blowfish 哈希。在 FreeBSD 系统上，`login.conf(5)` 中启用了 Blowfish 哈希；在 NetBSD 和 OpenBSD 上，`passwd.conf(5)` 中启用了 Blowfish 哈希。

# 系统统计

在 BSD 中，`sa(8)` 提供了类似于 Linux `sa(1)`的功能，后者是 `sysstat` 工具包的一部分。`sa(8)` 可以提供详细的统计数据，例如：

- 平均执行的 I/O 操作数
- 每个命令的统计，包括调用次数、通过时间、总 CPU 和平均 I/O 操作数
- 每个用户的统计，包括调用的命令数、总 CPU 时间和 I/O 操作总数

这些统计数据可以确定系统的基准并监控行为的异常。

# IPsec

IPsec 用于创建 VPN 以加密跨越未受保护网络的数据。在 BSD 中，`IPsec(4)` 提供了创建 IPsec 标头的内核支持。然而，密钥交换不需要内核支持；这是通过实现 ISAKMP 协议的程序实现的。对于密钥管理，FreeBSD 需要第三方应用程序（如 `racoon`）；NetBSD 拥有 `racoon(8)`；而 OpenBSD 使用一个名为 `isakmp(8)` 的自定义 ISAKMP 守护进程。

OpenBSD 提供了一个管理 IPsec 隧道所有方面的工具 `IPctl(8)`。FreeBSD 4.0 极大地简化了 IPsec 配置，其 `IPsec.conf(5)` 提供了若干工作 VPN 配置示例。

# 随机性

在为 VPN 或数字证书（例如用于运行 SSL 的 Apache Web 服务器）生成密钥时，提供随机数据（或熵）是非常重要的。密钥和证书需要随机“种子”，以确保新密钥或证书在数学上与之前的密钥或证书不相似。

所有的 BSD 都根据需要持续收集可用随机数据的能力。FreeBSD 和 OpenBSD 使用 `random(4)`，而 NetBSD 使用 `rnd(4)`。FreeBSD 的实现提供了若干 MIB 并基于 Schneider 的 Yarrow 算法。Bruce 也是 Blowfish 算法的作者。

# chroot(8)

所有的 BSD 都提供了 `chroot(8)`，允许管理员将服务置于沙箱环境中。一旦服务被 chroot，它就无法访问 chroot 之外的目录。

# Hacking Exposed Linux：安全机密与解决方案

本节剩余部分将关注 FreeBSD 的其他多种安全特性。第一个是 `jail(8)`。`chroot` 用于禁禁进程，而 FreeBSD `jail` 用于划分操作系统。无论 jail 内部发生什么，都不会影响主机操作系统或运行在宿主机上的其他 jail。Jails 受 ISP 欢迎，因为它们可以为客户提供相互隔离的虚拟环境。

> 注意 jail 项目 (http://sysjail.bsd.lv/) 为 OpenBSD 和 NetBSD 提供了 jail 子系统。

# FreeBSD

在本节中，我们将关注 FreeBSD 中的多种安全特性。TrustedBSD 项目 (http://www.trustedbsd.org) 的持续目标是创建模块和框架。其中某些扩展已纳入 FreeBSD。

# ACLs

在传统的 UNIX 权限中，使用组来配置访问。然而，访问控制列表 (ACLs) 允许对文件进行细粒度控制。

# MAC 策略

类似于 SELinux，FreeBSD 的强制访问控制 (MAC) 框架提供了安全策略。`mac (4)` 描述了可用的策略；其中许多策略非常复杂，需要高级知识来实现。在默认的 Unix 系统上，任何用户都可以通过 `ps -a` 查看所有运行进程。FreeBSD 手册包含 MAC 的更多信息：http://www.freebsd.org/doc/en_US/books/handbook/mac.html。

# 破解 Linux：Linux 安全机密与解决方案

每个应用程序都有不同的开发团队，对补丁和告警形式的安全事件的响应速度也差异很大。管理员如何在不需要订阅几十个安全邮件列表的情况下，感知可能发生的安全事件？

FreeBSD 项目创建了漏洞与暴露标记语言（VuXML），用于记录 FreeBSD 端口收集集合（ports collection）中的安全问题——该集合包含了近 16,000 个第三方应用程序。

如 C-3 所示，现有的漏洞已被标记，并可以在 http://www.vuxml.org/freebsd/ 在线查看。FreeBSD 在其端口集合中也使用了 VuXML，其告警可以在 http://www.vuxml.org/openbsd/ 处获取。一旦应用程序存在已知的安全漏洞，其软件包将从 FreeBSD ftp 镜像中移除，且该端口的 Makefile 被标记为 `FORBIDDEN`（禁止）。如果你尝试通过这种方式进行构建，将收到一个包含安全告警链接的错误。覆盖此错误并强制构建端口的唯一方法是手动删除 `FORBIDDEN` 行。

# portaudit(1)

如果你的操作系统能告诉你已安装的软件是否存在已知的安全漏洞，那不是很好吗？在 FreeBSD 系统上，通过输入 `pkg_add -r portaudit` 即可轻松实现这一点。该脚本会将当前的 VuXML 条目与系统上安装的软件进行比较，并报告任何已安装软件是否存在未未决的漏洞。报告包含了告警的超链接，以便管理员评估该漏洞对系统构成的风险。

# gbde(4)

随 FreeBSD 5.0 引入的 GEOM 框架提供了一个磁盘抽象层，允许创建与磁盘交互的模块。这包括创建安全模块，例如基于 GEOM 的磁盘加密（`gbde (4)`）。gbde 设计用于保护“离线”存储设备上的数据，免受即使动机极强的攻击者的侵害。例如，如果攻击者偷取了受保护的磁盘且不知道密码，他或她必须通过四个加密屏障才能访问数据。然而，gbde 不提供任何针对已连接和挂载的文件系统的网络攻击保护。gbde 的示例（Examples）部分提供了初始化、攻击和卸载加密设备的命令，以及如何销毁所有主密钥副本。

# geli(8)

`geli(8)` 是另一个用于磁盘加密的 GEOM 模块，在 FreeBSD 6.0 中引入。相比 gbde，它具有多个优势，包括：

- 加密根分区的能力
- 支持多种加密算法
- 支持多个独立密钥
- 支持一次性密钥

`man geli` 的示例（Examples）部分展示了多种加密场景所需的命令。

# NETBSD

本节涵盖了 NetBSD 操作系统特有的安全功能。许多安全增强在 NetBSD 4.0 中引入，关于这些功能的详细描述可以在 NetBSD 内核开发者 Elad Efrat 编写的文章（http://www.securityfocus.com/inocus/1878）中找到。

# kauth(9)

`kauth(9)` 引入于 NetBSD 4.0，旨在提供一个安全策略框架。该框架允许创建可以插入内核的安全模块。可能的安全模块可以提供安全增强，如 ACL 支持和 MAC（强制访问控制）策略。该框架还将移除硬编码“超级用户完全访问系统”概念的引用，使得创建限制超级用户权限策略成为可能。

为了帮助开发者创建安全模块，`semodel(9)` 提供了一套开发指南。

# veriexec(4)

管理员如何知道系统是否被 root（提权）？旧的 rootkit 试图通过删除日志记录和替换 `ls` 和 `ps` 等二进制文件来隐藏其踪迹，以隐藏它们安装的文件和进程；而较新的 rootkit 则试图通过通过设备程序或内核可加载模块加载代码来修改内核。在大多数操作系统上，感知这些变化的唯一方法是安装并配置如 Tripwire 类的完整性程序，并设置计划定期检查文件校验和数据库。在 BSD 系统上，`mtree(8)` 描述了如何使用此内置工具创建自定义的文件完整性检查系统。

NetBSD 更进了一步，提供了一个基于内核的功能，在运行或读取可执行文件或文件之前验证其完整性。与其他需要你手动检查更改的文件完整性检查系统不同，`veriexec(4)` 会立即通知管理员，并提供对入侵者的实时通知。传统上使用 `veriexctl(8)` 加载管理员使用脚本生成的签名文件。在 NetBSD 4.0 中，将使用 `veriexecgen(8)` 生成指纹数据库，该数据库可以使用 `veriexctl(8)` 加载到内核内存中。

# pw_policy(3)

NetBSD 4.0 还引入了密码策略强制功能。这允许管理员强制执行密码长度、大小写混合、所需数字数量、标点符号和密码字符类别，以及用户在字符类别之间切换的频率。策略本身设置在 `passwd.conf(5)` 中。

# fileassoc(9)

该框架在 NetBSD 4.0 中引入，允许内核关联独立于文件系统的属性。这将允许创建安全属性，这会对系统性能产生负面影响。

# Audit-Packages

FreeBSD 和 OpenBSD 使用 VuXML 管理其端口集合中的漏洞，而 NetBSD 通过 `pkgsrc` 集合维护其自己的列表。该列表可以在 http://ftp.NetBSD.org/pub/NetBSD/packages/distfiles/pkg-vulnerabilities 获取。正如你可以在 FreeBSD 系统上安装 audit 工具，你可以在 NetBSD 系统上安装 `audit-packages`。`audit-packages` 脚本会将漏洞列表与已安装软件进行比较，并就影响系统的漏洞提供建议。

# cgd(4)

`cgd(4)` 允许使用 AES、Blowfish 或 3DES 进行磁盘加密，并设计用于加密非根分区。它还可以用于加密 CD 和 DVD，并使用一次性密钥加密交换分区和临时文件。

# clockctl(4)

`ntpd(8)` 是一个以超级用户运行的臃肿进程示例，这在安全环境中是有问题的，特别是考虑到准确的网络时间是 `kerberos(8)` 认证系统的需求时。`clockctl(4)` 子系统允许 NTPD 以非权限账户运行，减少了 NTPD 漏洞的影响。

> OpenBSD 使用了不同的方法——他们重写了一个不那么臃肿的 OpenNTP 版本，使用了权限隔离。

# OpenBSD

OpenBSD 被誉为世界上最安全的操作系统之一。OpenBSD 开发者在设计和发布工程过程中结合了许多安全功能。例如，C语言函数 `strlpy(3)` 和 `strcat(3)` (http://www.openbsd.org/papers/strlpy-paper.ps) 被编写为 `strncpy()` 和 `strcat()` 函数更安全的替代品。

Wikipedia 为若干安全功能提供了概述和额外参考：http://en.wikipedia.org/wiki/OpenBSD_security_features。此外，OpenBSD 首席开发者 De Raadt 有了一场关于漏洞利用缓解技术的演讲：http://www.openbsd.org/papers/openbsd-deraadt

# ProPolice

ProPolice 是由 IBM 开发的 gcc 补丁集，旨在保护编译的应用程序免受缓冲区溢出攻击。它同时也作为栈溢出保护（SSP）。OpenBSD 项目自 2002 年以来一直使用 ProPolice，并提供了第一个真实规模测试。它负责发现（并导致修复）OpenBSD 操作系统中附带的程序中的许多漏洞。

ProPolice 现在已集成到 gcc 4.1 中；自 2006 年 7 月以来，该版本一直是 NetBSD 项目使用的 gcc 版本。针对 FreeBSD 的补丁请访问 http://tataz.chchile.org/~tataz/FreeBSD/SSP/README.txt。

# W^X

W^X 是 Write X 的缩写，这种技术使得进程内存空间中的任何页面可以是可写的或是可执行的，但不能同时具备这两种属性。这防止了利用程序将想要执行的代码写入内存，从而导致程序执行该代码。W^X 已应用于 OpenBSD 3.4。Marc Espie 在一次采访中（http://www.onlamp.com/pt/a/467e）中提供了更详细的描述。

- NetBSD 使用不可执行的栈和堆堆提供了类似的功能（http://netbsd.org/Documentation/kernel/non-exec.html）。

# systrace(1)

`systrace(1)` 由 OpenBSD 项目开发，并在版本 2.0 中引入 NetBSD。它通过对系统调用强制执行访问策略，监控并控制应用程序对操作系统的访问。它可以限制服务对操作系统的访问，保护系统免受缓冲区溢出的攻击。它的特权提升允许管理员在策略中指定需要超级用户权限的特定系统调用，从而移除 SUID 和 SGID 二进制文件。

# 加密交换分区

OpenBSD 支持对交换分区进行 Blowfish 加密。交换空间被划分为许多区域，每个区域分配自己的加密密钥。一旦某个区域的数据不再被需要，OpenBSD 会通过丢弃加密密钥来安全地删除它。自 OpenBSD 3.9 以来已默认开启。

# pf(4) 防火墙功能

`pf(4)` 防火墙于 OpenBSD 项目，已集成到 FreeBSD 和 NetBSD 的基础安装中。pf 是基于内核的，这意味着它非常快；它是一个功能丰富的状态防火墙，在速度和功能上都可以与商业防火墙媲美。其 pf FAQ（http://www.openbsd.org/faq/pf）描述了许多功能并提供了配置示例。接下来我们将描述其中一些功能。

# 状态表的直接操作

管理员使用 `pfctl(8)` 直接与 pf 交互。除了停止和启动防火墙、查看当前加载的规则集以及状态表和 NAT 表、动态添加规则外，`pfctl` 还允许与状态表进行直接交互。

例如，要立即删除来自攻击主机的所有状态条目，只需指定该主机的 IP 地址：

```
pfctl -k ip_address
```
