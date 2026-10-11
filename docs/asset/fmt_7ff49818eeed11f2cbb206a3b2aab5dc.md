
用户与系统之间的一个完整的交互。来自 FirstLinux http://www.tld.org/LDP/Linux-Dictionary/html/index.html

# sessreg (会话注册)

管理会话项。来自 whatis http://www.tld.org/LDP/Linux-Dictionary/index.html

# SET

安全电子 (IBM, 签证）来自 VERA http://www.tld.org/LDP/Linux–Dictionary/html/index.html

# SET

软件工程技术来自 VERA http://www.tld.org/LDP/Linux-Dictionary/html/index.html

# SET

标准交换来自 VERA http://www.tld.org/LDP/Linux-Dictionary/html/index.html

# set686

Cyrix 586 允许修改 586 寄存器，包括缓存区域、I/O 延迟、写入策略，以及在 CPU 闲置时的挂起状态。这种 586 模式可以降低功耗，特别是在主板上。来自 Debian 3.0 http://www.tldp.org/LDP/Linux–Dictionary/html/index.html

# SETA

系统工程与技术来自 VERA http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

# setcd (设置 CD)

该程序允许控制你的 CD 驱动器的行为。你需要 `libcd` 和较新版本的内核。在内核 2.0 中，它可以控制自动关闭、自动介质类型检查和托盘。如果你尝试挂载光盘，会遇到“未找到介质”的提示；如果你使用挂载，则会遇到“介质类型错误”。该软件包可能来自利用 CD 特性的开发者。来自 Debian 3.0 http://www.tldp.org/LDP/dictionary/index.html

# setdfprm (设置磁盘参数)

设置用户提供的磁盘参数来自 Mathis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

# setiatihome (寻找地外生命计划)

`SETI@Home` 客户端（安装包）。`SETI@Home`是一项利用互联计算机的功率来寻找地外文明（SETI）的科学实验。你可以通过运行一个下载并分析望远镜数据的程序参与其中。计算机有可能检测到文明的微弱信号。`SETI@Home` 仅以二进制形式分发，必须根据架构正确的 unix tar 包从 http://setiatihome.ssl.berkeley.edu/unix.html 下载并放入 `TMPDIR`（未设置则为 `/tmp`）。如果安装了 `wget`，此安装程序会自动合并并安装程序。目标 Debian 架构为：`x86`、`alpha`、`sparc`、`powerpc` 或 `hppa`。

# setkeycodes (设置键码)

加载内核自身的键码到键码映射表项来自 Mathis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

# SETL (集合理论语言)

集合理论语言（新大学）。“SetL”来自 VERA http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

# setledes (设置键盘处理)

设置键盘处理来自 Mathis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

# setmetamode (设置元模式)

定义键盘处理来自 Mathis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

# setmixer (设置混合器)

一种命令行模式混合器。厌倦了每次重启后手动设置声卡吗？这里有一个小工具可以帮你避免这种情况。整个源代码为 `setmixer.c`。来自 Debian 3.0

# STEP (安全电子交易过程)

安全电子交易过程来自 VERA http://www.tldp.org/LDP/Linux–Dictionary/html/index.html

# SETP

S 1381

# 来自 VERA 的流环境传输协议

## 配置 PCI 设备，源自 whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

控制串口端口的配置。和/或报告与串口相关的配置信息。这些信息包含了特定端口正在使用的 I/O 端口和 IRQ。此版本采用了全新的配置方法，如果你有除标准 `ty0` 和 `ty1` 以外的设置，你必须运行它来get实际操作。默认情况下，内核仅配置了 `COM1–4`，它们使用使用 IRQ 3 和 4。如果你有其他串口端口（如 AST Fourport），或者你将端口 IRQ3 和 4 映射到其他 IRQ 以允许对 COM1 和 2 的并发访问，则你必须拥有此包。来自 Debian 3.0r0 APT http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## 获取/设置 Linux 串口信息，源自 whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

创建一个会话和进程组 ID，源自 whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

在新会话中运行程序，源自 whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

设置终端器属性，源自 whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

设置当前进程的有效用户 ID。如果调用者的有效用户 ID 为 root，则也会设置实际用户 ID 和保存的用户 ID。来自 Linux Guide @FirstLinux http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

(SUID) 用户可以运行但具有 root 权限的 UNIX 程序。**关键点：** 在理论上，setuid 程序只能由 root 安装，它们被视为操作系统的一部分，因为它们绕过了安全检查，并且必须自行验证安全性。一个典型的例子是 `password` 命令，用户运行它来更改自己的密码。它必须设置为 setuid，因为它创建的文件只有 root 权限访问，但它必须允许用户运行。**关键点：** 在实践中，setuid 程序经常存在可以被用户利用的漏洞。**关键点：** 作为系统加固手段，管理员应该扫描系统并移除所有必要的 setuid 程序。`Linux find -type f -perm +4000 -exec bash -c '\\ -perm -4000 -o ! \ -perm -2000' {} \;` 为了移除 setuid 位，你可以使用 `chmod -s file`。移除 setuid 位将导致许多程序无法运行。需要保留此位的两个程序是 `/usr/bin/passwd`（用户运行以更改密码）和 `/bin/su`（将普通用户提升为超级用户，前提是提供正确密码）。**关键点：** 大多数 setuid 程序仅更改组上下文而非用户上下文。Windows 并没有 setuid 的概念。相反，它使用了 RPC，其中客户端程序（由用户运行）联系其他程序来执行所需的任务。例如，为了更改密码，客户端请求 SAM 代替用户执行。因此，而 UNIX 只需要少数程序即可完成相同的操作。**关键点：** 留后门系统的一种常见方法是在 `/tmp` 目录下放置一个 SUID 程序。来自 Hacking–Lexicon http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## Linux 字典

Setuptool 是一个用户友好的文本菜单，允许你访问红帽 Linux 操作系统包含的所有文本模式配置程序。来自 Redhat 8.0 RPM http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## setxbmap

使用 X 键盘扩展设置键盘，源自 Whatis http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## SEU

软件开发环境 (CASE)，来自 VERA http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## SEU

源条目工具 (IBM, ADT)，来自 VERA http://www.tldp.org/LDP/Linux-Dictionary/html/index.html

## sex
