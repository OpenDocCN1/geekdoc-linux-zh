
对所有方面的网络支持，包括服务器、数据库和安全，都提供来自高强度关键任务需求的支持。Red Hat Enterprise ES 提供类似的套件，但针对的是中级业务需求。Red Hat Enterprise WS 实现了一款工作站，具有广泛的客户端，可用于 Red Hat Enterprise ES 或 AS 网络。

## Red Hat 文档

Red Hat 维护了一个庞大的 Linux 文档库，可免费在线访问（见表 1-1）。从其主页，您可以链接到其支持页面，其中列出了完整的 Red Hat 手册集，均以网页格式提供，便于使用任何 Web 浏览器查看。这些包括参考指南、入门指南和安装指南。还提供了提示、HOW-TO 和常见问题解答文档。特别值得注意的是硬件兼容性列表。该文档列出了所有与 Red Hat Linux 兼容的硬件。对于 PC 用户而言，这包括大多数硬件，仅有少数例外。所有 Red Hat 文档均在 GNU 通用公共许可证下免费提供。在您的系统上安装 Red Hat Linux 之前，您可能希望查看在线安装指南。这是一份冗长而详细的文档，会仔细带您完成每个步骤。如果您的系统设计用于任何特殊任务，请务必查阅定制指南，其中涵盖了各种主题，例如使用 Red Hat kickstart 在网络上进行自动安装；网络服务如 Samba、Apache 和 FTP；系统管理工具；以及软件包的安装和管理。Red Hat 还提供了有关实现 PPP Internet 连接、Samba 文件共享、Apache Web 服务器、防火墙和邮件服务器的文档。

| References | Description |
|---|---|
| www.redhat.com | Red Hat 网站 |
| www.redhat.com/support | Red Hat Linux 的支持页面，包括指向当前在线文档的链接 |
| fedora.redhat.com | Fedora 项目，Red Hat 当前免费的开源版本 |
| fedora.redhat.com/docs | Fedora Core 版本的文档和支持教程 |
| The Official Red Hat Linux Getting Started Guide | 面向首次用户的入门指南 |
| The Official Red Hat Linux x86 Installation Guide | Red Hat Linux 的详细安装指南 |
| Red Hat Linux Installation Gotchas | 安装故障排除 |
| Red Hat Reference Guide | Red Hat 参考手册 |
| Red Hat Customization Guide | 涵盖常见定制任务和工具的主题，例如服务器配置 |
| Official Red Hat Linux Security Guide | 关于用户、系统和网络安全各方面的综合指南 |
| Red Hat Linux System Administration Primer | 管理任务和概念概述 |

## Red Hat Linux Fedora Core

Red Hat Linux Fedora Core 提供了多个新功能，以及对 Red Hat 8 和 9 的改进方面。虽然它不包含新的 2.6 内核，但它使用最新的 2.4 内核，2.4.22。几个新功能包括蓝牙和 ACPI 支持：

- 增强的蓝牙支持包括固件加载器、协议分析器和个人网络支持。
- 高级配置和电源接口（ACPI）通过 apid 守护进程得到支持。
- CUPS 现在是唯一包含的打印服务器。LPRng 已被完全放弃。
- 包含对 DVD+R/RW 刻录机的支持，dvd+rw 工具
- 它包含 GCC 编译器的 3.2.3 版本，gcc32。
- Internet 安全协议（IPSEC）工具现已可用。
- 内核现在支持 Exec shield，这使得内核的某些段不可执行，从而提供更高的安全性。
- 内核现在可以阻止某些内核模块被加载，确保对内核配置有更集中的控制。
- 内核还支持笔记本模式，可安排任务以适应笔记本省电功能。
- 两个较旧的邮件客户端已被放弃，exmh 和 pine。
- 由于内核现在已包含声音支持，sndconfig 工具已被放弃。
- 如 Red Hat 9 中所实现，Fedora Core 继续支持 Native POSIX Thread Library（nptl）。线程库允许应用程序组织成独立的线程，让处理器更高效地运行它们。通过线程，不同线程中的代码部分可以同时运行。
- Red Hat 正在继续从 LILO 迁移到 GRUB，并将很快完全放弃 LILO。
- 由于开发限制，tripwire 入侵检测软件已被放弃。
- Red Hat 继续向 UTF-8 迁移，UTF-8 是通用字符集（UCS）的 Unicode 编码。UTF-8 与标准 ASCII 字符文件兼容，并且

