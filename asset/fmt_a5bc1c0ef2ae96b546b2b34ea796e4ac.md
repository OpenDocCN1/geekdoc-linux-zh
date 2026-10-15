
scan/search 扫描/搜索 symlinks 目录中的符号链接并将它们列在标准输出上。每个链接都有一个分类前缀：相对、绝对、悬空、长路径或其他文件系统。`symlinks` 还可以将绝对链接（同一文件系统内）转换为相对链接，并可能创建混乱和悬空的链接。来自 Debian 3.0r APT http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

# Linux 词典

## symlinks

`symlinks` 工具对符号链接进行维护。`symlinks` 检查符号链接问题，包括指向不存在文件的悬空链接。`symlinks` 还可以将绝对符号链接转换为相对。如果你需要一个程序来维护系统，请安装 `symlinks` 包。来自 Mandrake 9.0 RPM http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## SYMM

同步多媒体工作组 (WAI) 来自 VERA http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## 对称的 (symmetric)

在加密中，“对称”意味着使用同一个密钥同时加密和解密。这在历史上一直是“正常”加密，但新密码学正在改变这一切。在你的加密中，相同的密钥被用于锁和解锁你的门。示例：某些对称加密是 DES；从以前到今天大多数流行的对称密码：RC2、RC4 和 RC5；RSA 用于当今浏览器与网站进行安全连接的流行密码；IDEA 一种广受誉、带有免费源码、无需许可且免版税的密码。因此，它是一种极其流行的对称加密算法 http://www.counterpane.com/blowfish；像 Blowfish 一样具有许多限制的 Twofish 密码效率更高，并且变得非常流行。http://www.counterpane.com/twofish。来自 Hacking-Lexicon http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## 对称多处理 (SMP)

由一个操作系统管理的两个或多个处理器的方法，通常共享内存并对输入输出设备具有相同的访问权限。应用程序可以在任何或所有处理器上运行。来自 Redhat http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## sympa

现代列表管理器 `sympa` 是一种可扩展的列表管理器，可以处理超过200,000个订阅者。它具有：

- 存档
- 身份验证
- 中文
- 摘要
- 过期
- 法文
- LDAP
- MySQL
- PostgreSQL
- 虚拟域名

它用 `Perl` 编写并使用一些模块。来自 Debian 3.0 http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## SYN

TCP 发送的第一个包是“SYN”或“同步”。三次握手涉及 SYN、SYN-ACK 和 ACK 包。防火墙可以过滤 SYN 包以区分好坏。来自 Hacking-Lexicon http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## SYN 洪水

SYN 洪水是一种 DoS 攻击类型。SYN 包通知服务器新连接。服务器分配内存来处理传入的连接。通过伪造大量的 SYN 请求，攻击者可以占内存，导致服务器无法接受合法客户端。然而，也存在 SYN cookies 等部分防御。来自 Linux 词典 http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## synesthesia

一个通过 CD 输入或管道将声音视觉化的程序。它通过结合 FFT 和立体声定位，超越了通常示波器样式，创建了二维风格。来自 Debian 3.0r http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## synaptic

`Synaptic`（以前称为 `apt`）是 Debian 的图形化包管理工具。它提供了与 `apt-get` 命令行相同的 GUI 界面功能，并处理 RPM。http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

### syncbbdb

PalmOS Palm Manager 中的 BBDB 在像 Palm Pilot 或 Vis 等 PalmOS 设备之间传输地址记录，使用 perl BBDB 到 PalmOS Palm Manager 对。来自 Debian 3.0r http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

## SYSAD

系统管理员，“SysAd” 来自 VERA http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

### sysadmin

`/sis’ad-min/n.` ‘system admin’的常用缩写；见 admin。来自 Jargon 词典 http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

# Linux 词典

Linux 系统管理员指南 来自 Linux 文档项目（Linux Documentation Project）的《Linux 系统管理员指南》。面向初级系统管理员。此软件包以 HTML 格式提供指南，您可以通过获取源码包来生成其他格式。来自 Debian 3.0r0 http://www.tdorp.org/LDP/Linux-Dictionary/html/index.html

### sysctl

运行时配置内核参数 来自 Whatis http://www.tdorp.org/LDP/Linux-Dictionary/html/index.html

### sysctl

读/写系统参数 来自 Whatis http://www.tdorp.org/LDP/Linux-Dictionary/html/index.html

### SYSSEX

SYSTEM 系统执行程序 (OS, IBM, S360) 来自 VERA http://www.tdorp.org/LDP/Linux-Dictionary/html/index.html

### syslogd

系统日志守护进程（System Logging Daemon）。此软件包实现了一个日志守护进程，它是标准 Berkeley 实用程序的增强版本。它负责为接收来自本地主机以及远程主机的程序和设施的消息提供日志记录。来自 Debian 3.0r0 APT http://www.tdorp.org/LDP/Linux-Dictionary/html/index.html

### syslogd

`syslog` 软件包包含两个实用程序（`syslog` 和 `quod`），它们提供系统日志支持。`Syslog` 和 `quod` 作为守护进程（后台进程）运行，并将系统消息记录到不同的地方，例如 `sendmail` 日志、错误日志等。来自 Mandrake 9.0 RPM http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

### syslinux

使用 MS-DOS 的 Linux 引导器 来自 Whatis http://www.tdorp.org/LDP/Linux-Dictionary/html/index.html

### syslinux

使用 MS-DOS 软盘的 Linux i386 引导器。`SYSLUX` 是一个用于 Linux/i386 操作系统的引导加载器，它运行在 MS-DOS/FAT 文件系统上。它的目的是简化 Linux 的首次安装，并创建救援和其他特殊用途的启动盘。`SYSLUX` 不适用于作为通用的引导器。然而，`SYSLUX` 在许多特殊用途应用中已被证明非常有用。使用此程序时，您需要一个“mssddos 软盘”。来自 Debian 3.0r0 http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

### syslinux

`SYSLINUX` 是一个运行在 MS-DOS/FAT 文件系统上的 Linux 系统引导加载器。它的目的是简化 Linux 的首次安装，并创建救援和其他特殊用途的启动盘。`SYSLINUX` 可以标准 MS-DOS（或任何可以访问已创建 MS-DOS 文件系统的系统）进行操作，并且最初创建它只需要一个约 7K 的程序或约 13K 的 Linux 程序。它还包含了 `PXELUX`，这是一个通过使用兼容 Intel PXE（预执行环境）规范的 BO PROM 从网络服务器启动的程序。来自 Redhat 8.0 RPM http://www.tdp.org/LDP/Linux-Dictionary/html/index.html

### syslinux2ansi
