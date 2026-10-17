
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
- 高级配置和电源接口（ACPI）通过 `apid` 守护进程得到支持。
- CUPS 现在是唯一包含的打印服务器。LPRng 已被完全放弃。
- 包含对 DVD+R/RW 刻录机的支持，`dvd+rw` 工具
- 它包含 GCC 编译器的 3.2.3 版本，`gcc32`。
- Internet 安全协议（IPSEC）工具现已可用。
- 内核现在支持 Exec shield，这使得内核的某些段不可执行，从而提供更高的安全性。
- 内核现在可以阻止某些内核模块被加载，确保对内核配置有更集中的控制。
- 内核还支持笔记本模式，可安排任务以适应笔记本省电功能。
- 两个较旧的邮件客户端已被放弃，`exmh` 和 `pine`。
- 由于内核现在已包含声音支持，`sndconfig` 工具已被放弃。
- 如 Red Hat 9 中所实现，Fedora Core 继续支持 Native POSIX Thread Library（`nptl`）。线程库允许应用程序组织成独立的线程，让处理器更高效地运行它们。通过线程，不同线程中的代码部分可以同时运行。
- Red Hat 正在继续从 LILO 迁移到 GRUB，并将很快完全放弃 LILO。
- 由于开发限制，`tripwire` 入侵检测软件已被放弃。
- Red Hat 继续向 UTF-8 迁移，UTF-8 是通用字符集（UCS）的 Unicode 编码。UTF-8 与标准 ASCII 字符文件兼容，并且提供了一种对所有语言进行编码和实现的标准方法。UTF-8 现在是默认编码。
- `vsftpd` FTP 服务器是现在唯一包含的 FTP 服务器。旧的华盛顿大学 FTP 服务器已被完全移除（`wu-ftpd`）。
- 自 Red Hat 8 开始，Fedora Core 继续完善 Bluecurve 界面，为 GNOME 和 KDE 提供无缝的图形化 GUI。

使用 Fedora Core，Red Hat 现在拥有完整的 Red Hat 管理工具系列，所有工具都包含 GNOME 界面（见表 1-2）。

| 管理工具 | 操作 |
|---|---|
| `redhat-config-bind` | 一个 Red Hat DNS 配置工具 |
| `redhat-config-date` | 用于修改系统日期和时间的图形界面 |
| `redhat-config-httpd` | Apache 配置工具 |
| `redhat-config-keyboard` | 用于修改键盘的图形界面 |
| `redhat-config-kickstart` | 用于制作 kickstart 文件的图形界面 |
| `redhat-config-language` | 用于修改系统语言的图形界面 |
| `redhat-config-mouse` | 用于配置鼠标的图形界面 |
| `redhat-config-network` | Red Hat Linux 的网络管理工具 |
| `redhat-config-nfs` | NFS 服务器配置工具 |
| `redhat-config-packages` | Linux RPM 软件的包管理器 |
| `redhat-config-printer` | 打印机配置后端/前端组合 |
| `redhat-config-printer-gui` | printconf 的 GUI 前端 |
| `redhat-config-proc` | 操作系统可调参数的配置工具 |
| `redhat-config-rootpassword` | 用于修改 root 密码的图形界面 |
| `redhat-config-samba` | Samba 服务器配置工具 |
| `redhat-config-securitylevel` | 用于修改系统安全级别的图形界面 |
| `redhat-config-services` | initscript 和 xinetd 配置实用程序 |
| `redhat-config-soundcard` | 用于检测和配置声卡的图形界面 |
| `redhat-config-users` | 用于管理用户和组的图形界面 |
| `redhat-config-xfree86` | 用于配置 XFree86 的图形界面 |
| `redhat-logviewer` | 用于查看日志文件的图形界面 |

## 操作系统和 Linux

操作系统是一个管理计算机硬件和软件供用户使用的程序。操作系统最初设计用于执行重复的硬件任务，其核心是管理文件、运行程序以及接收用户命令。你通过用户界面与操作系统交互，该界面允许操作系统接收并解释用户发送的指令。你只需向操作系统发送指令即可执行任务，例如读取文件或打印文档。操作系统的用户界面可以简单到在命令行输入命令，也可以复杂到在桌面上选择菜单和图标。

操作系统还管理软件应用程序。为了执行不同的任务，例如编辑文档或进行计算，你需要特定的软件应用程序。编辑器就是一个软件应用程序的例子，它使你能够编辑文档，进行更改并添加新文本。编辑器本身是一个由计算机执行的指令组成的程序。为了使用该程序，它必须首先被加载到计算机内存中，然后执行其指令。操作系统控制所有程序的加载和执行，包括任何软件应用程序。当你想使用编辑器时，只需指示操作系统加载编辑器应用程序并执行它即可。

文件管理、程序管理和用户交互是所有操作系统共有的传统功能。Linux 与所有版本的 Unix 一样，还增加了两个功能。Linux 是一个多用户和多任务系统。由于它是多任务系统，你可以要求系统同时执行多个任务。在执行一项任务的同时，你可以进行另一项工作。例如，你可以在打印另一个文件时编辑一个文件。你不必等到另一个文件打印完成后再编辑它。由于它是多用户系统，多个用户可以同时登录到系统，每个用户通过自己的终端与系统交互。
