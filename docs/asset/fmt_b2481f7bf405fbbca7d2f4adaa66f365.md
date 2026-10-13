
## 第二章 | Linux 安全的基础组件

这些发行版之间也有相似之处。例如，Red Hat 和 Canonical (Ubuntu) 都发布具有长期支持的发行版。Red Hat 支持其企业 Linux 七年。Red Hat Enterprise Linux 的最新版本是 `RHEL7`，于 2014 年上半年发布。

Ubuntu 每六个月发布一次，并每两年发布一次更健壮的发行版。这些版本标记为长期支持 (LTS) 版本。Ubuntu LTS 服务器版受支持五年。

除了长期支持外，Red Hat 和 Canonical 可能还有许多其他类似的决策。两者都提供了一种 Web 工具的订阅，该工具允许用户远程管理一组 Linux 系统。

Red Hat 和 Canonical 在默认服务方面做出了相似的选择。例如，将 `Apache` 作为默认 Web 服务器，非常安全的文件传输守护进程 (`vsftpd`) 作为默认 FTP 服务器，以及通用 Unix 打印系统 (`CUPS`) 作为默认打印服务器。

还有一些包管理系统之外的差异。例如，Ubuntu 在其服务器版本中包含了一个最小化安装，非常适合虚拟机。该安装包含一个针对虚拟机客户端运行优化的内核。

Red Hat 和 Ubuntu 在默认应用程序方面也做了不同的选择。当然，你可以用你选择的应用程序覆盖它们。在许多情况下，Red Hat 和 Ubuntu 也支持这些替代方案。

有时，Red Hat 和 Ubuntu 会相互学习。由于它们在开源许可下发布，它们可以从竞争发行版中获取源代码并自行使用。Ubuntu 使用许多最初为 Red Hat 构建的 GUI 管理工具。

### 服务的多样性

Linux 包含了各种服务。如果某个服务出现安全问题，通常最好安装更新或补丁来解决该安全问题。然而，有时更新可能会导致更严重的问题。

在这种情况下，你可能想要考虑不同的服务。表 2-3 列出了许多服务的替代方案。这并不是一个完整的列表。但它描述了当一个服务选项存在致命安全缺陷时的替代方案。它还让你对单个服务器上可以安装多少服务有了直观了解。

### 表格 2-3 不同服务的替代方案

| 功能 | 服务选项 | 备注 |
| --- | --- | --- |
| 域名命名系统 (DNS) | 伯克利互联网命名域 (BIND)<br>Daniel J. Bernstein 的 DNS (djbdns) | DNS 是一个域名和 IP 地址的分层数据库。它允许你通过 IP 地址查找到主机名，反之亦然。BIND 和 djbdns 都是 DNS 服务器的实现，BIND 是互联网上最常见的 DNS 服务器。djbdns 是一个相对于 BIND 较轻量级的 DNS 服务器替代方案。 |
| 文件传输 | 专业 FTP 守护进程 (ProFTPD)<br>Troll FTP<br>vsftp<br>简易文件传输协议 (TFTP) | TFTP 是一种使用简化 FTP 形式的协议和服务。它是一种非常轻量的文件传输方式，可用命令非常少。 |
| 图形桌面环境 | GNOME<br>K 桌面环境 (KDE)<br>Xfce<br>轻量级 X11 桌面环境 (LXDE) | 在 Linux 中，图形桌面环境是独立的，但它需要使用 X Windows 系统服务器。它还可能包含一个窗口管理器，用于控制 GUI 内部窗口的位置。 |
| 图形用户界面 | X.org<br>XFree86 Freedsktop.org | XFree86 是 X 图形界面的实现。 |
| 图形登录管理器 | GNOME 显示管理器 (GDM)<br>KDE 显示管理器 (KDM)<br>X 显示管理器 (XDM) | 图形登录管理器是用于 Linux GUI 图形登录的服务。GDM 是由 GNOME 桌面环境开发者构建的图形登录管理器。KDM 是由 KDE 开发者构建的图形登录管理器。XDM 是由 X.Org GUI 服务器开发者构建的图形登录管理器。 |

### 表格 2-3 不同服务的替代方案（续）

| 功能 | 服务选项 | 备注 |
| :--- | :--- | :--- |
| 邮件用户代理 | Cyrus Dovecot | Cyrus 是卡内基梅隆大学开发的邮件服务器，主要用于 IMAP 版本邮件传输。Dovecot 是一个开源邮件服务，为 POP 和 IMAP 协议提供常规和安全版本。Cyrus 和 Dovecot 是邮件服务器的实现，用于为客户端检索邮件。 |
| 打印 | CUPS 系统 V 行打印机下一代 (LPRng) | LPRng 是一个用于向用户或系统发送或接收打印作业的服务器。 |
| 远程连接 | 安全 Shell (SSH) 远程 Shell (RSH) Kerberos Telnet | Kerberos Telnet 是 Telnet 服务器的一个版本，可以使用 Kerberos 票据来增强安全性。 |
| 邮件传输代理 | Postfix sendmail Sendmail Exim Qmail |  |
| 结构化查询语言数据库 | MySQL PostgreSQL Sybase Oracle 的专用选项 | MySQL 是一个开源数据库程序，目前归 Oracle 所有。PostgreSQL 是一个由各种开源和其他 IT 公司赞助的开源数据库程序。 |
| Web 服务器 | Apache Boa Caudium Roxen Sun Java Zeus |  |

### 本章总结

Linux 安全始于内核。Linux 内核的模块化意味着它更加健壮。许多模块化选项会影响安全性。为此，你需要决定是接受为你的发行版定制的内核，还是自己定制并编译内核。Linux 安全持续到启动过程。良好的安全性可以防止未经授权的用户从现场光盘启动并从 `GRUB` 或 `LILO` 启动加载程序中选择管理选项。除了基础操作系统外，你应该尽可能保持运行的服务最少。如果可能，不要安装 GUI。

文件所有权和权限始于自主访问控制，并由访问控制列表进行增强。使用 `sudo` 可以提供受限的管理员权限，并消除用户以 root 身份登录的需求，这可能是危险的。使用 `iptables` 的基于主机的防火墙可以防止意外的网络通信进入系统。通过防火墙或 TCP Wrappers 对暴露在互联网的服务提供额外保护。强制访问控制系统（如 SELinux 和 AppArmor）增加了另一层控制，即使存在如 Telnet 等明文协议。

关于安全性，你可能需要选择是否接受发行版提供的安全更新。某些安全更新并不适用于所有配置，尽管它们会自动更新。虚拟化增加了安全性的维度。隔离适当的安全区域有助于提高其他系统的安全性。最后，如果你了解 Linux 发行版之间的差异，在选择安全选项时就能做出更好的决定。

### 核心概念与术语

| 访问控制列表 (ACLs) | 图形登录管理器 | 可插拔认证 |
| 伯克利命名 | 蜜罐 | 模块 (PAMs) |
| 域名 (BIND) | 虚拟化层 | PolicyKit |
| 二进制内核 | iptables | Postfix |
| CentOS | KDE 显示管理器 (KDM) | PostgreSQL |
| 通用打印系统 (CUPS) | Kerberos Telnet | Qmail |
| Cyrus | 行打印机下一代 | sendmail |
| Daniel J. Bernstein 的 DNS (djbdns) | Linux |  |
| 自主访问控制 | Linux 发行版 |  |
| 域名系统 (DNS) | Linux 内核 |  |
| Dovecot | Linux 加载程序 |  |
| Exim | LILO |  |
| 文件传输协议 (FTP) | 强制访问控制 |  |
| 文件传输 (FTP) | MySQL |  |
| GNOME 显示管理器 (GDM) | 网络 |  |
| 图形桌面环境 | PAM |  |
| 图形用户界面 | PolicyKit |  |
| 图形登录管理器 | PostgreSQL |  |
| GRUB | Postfix |  |
| 蜜罐 | Qmail |  |
| 虚拟化层 | Runlevel |  |
| iptables | SSH |  |
| KDE 显示管理器 (KDM) | Sendmail |  |
| Kerberos Telnet | Syslog |  |
| Knop | Telnet |  |
| LPRng | TFTP |  |
| 邮件传输代理 | vsftpd |  |
| 邮件用户代理 | Winbind |  |
