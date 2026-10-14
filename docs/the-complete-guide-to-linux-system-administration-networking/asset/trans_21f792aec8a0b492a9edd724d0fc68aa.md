
group permissions — 一组三个文件权限（r、w 和 x），可授予分配给文件或目录的组成员。

grpquota — 可在 /etc/fstab 文件中使用的选项，会导致文件系统为每个组跟踪磁盘空间配额。与 quotaon 和 edquota 命令一起使用。

GRUB — Linux 启动管理器；Red Hat Linux 和 Fedora 发行版默认使用。

hard link — 一个指向由至少一个其他文件记录指向的 inode 的文件记录。

hard mount — 挂载 NFS 文件系统的一种方法，程序会无限期地等待 NFS 服务器响应。

hard wired — 计算机功能由构成计算机的线路和其他组件安排而成。硬连线功能不易更改。

hardware-based RAID — 包含在单独硬件设备（RAID 子系统）中的 RAID 阵列，由与 Linux 系统 CPU 分开的 CPU 和其他组件控制。

hardware clock — 每台基于 Intel 的 PC 硬件中的时钟。Linux 内核在启动时使用它来初始化系统时钟。

help desk — 许多组织中的一项服务，帮助终端用户解决与信息技术相关的问题。

hexadecimal (hex) — 使用基数 16 的计数系统。十六进制使用 0 到 9，加上字母 A 到 F（通常大写）来计数 10 到 15 的数字。

history list — 包含最近执行的命令的列表。（历史记录列表中通常至少包含 100 条命令。）

home directory — 文件系统中允许特定用户存储数据的区域。每个常规用户账户都有一个关联的主目录，以用户账户登录名命名。在 Linux 中，这些通常是 /home 目录的子目录。

hot-swapping — 在不关闭设备电源的情况下移除和更换故障硬盘或其他组件。

HOWTOs — Linux 文档项目中涵盖特定主题的文档。

IDE — 一种低成本、易于管理的接口，大多数计算机使用它将硬盘和 CD-ROM 驱动器连接到 CPU。

IDE controller — 用于在 IDE 兼容硬盘或其他 IDE 设备与微处理器之间通信的硬件组件。

if-then-else statement — 用于确定脚本中其他命令是否执行的命令集。if-then-else 语句是一种选择语句。

incremental backup — 一种备份过程，存储自上次增量或差异备份以来更改过的所有文件。

index — 循环语句中使用的计数变量。索引充当标记，用于计算循环执行命令列表的次数。

info page — 许多 Linux 命令的信息来源。使用 info 命令访问。另见 man page。

Information Systems (IS) department — 许多组织中的一个部门。IS 员工负责为其他员工维护计算机和信息系统。（在某些组织中，IS 被称为 IT。）

Information Technology (IT) department — 参见 Information Systems (IS) department。

init program — 主控制程序，在系统上启动许多其他进程，例如提供登录提示的进程。Linux 内核加载并初始化后启动的第一个进程。

initialize — 将变量设置为预定义值，例如零或 ""（空字符串），以便脚本在使用变量时不会对其初始值产生不确定性。

inode — 文件系统中由唯一编号标识的数据记录，其中包含通常称为“文件”的数据块集的详细信息。

installation source — Linux 安装的文件集。这些文件通常存储在 Linux CD-ROM 上。

installation type — 指定要安装的 Linux 软件的规范；适当的安装类型取决于 Linux 系统的用途。

install disk — 用于启动某些 Linux 发行版的 Linux 安装程序的磁盘。参见 boot disk。

instance — 具有特定选项设置的打印机定义版本。

Integrated Development Environment (IDE) — 程序（通常是图形化的），通过集成程序员经常使用的工具，如文本编辑器、编译器、调试器和文档，为程序员提供方便的工作环境。

interior routing protocols — 为在单一组织控制的网络之间路由数据包而设计的路由协议；数据包基于数学模型进行路由。

Internet Protocol (IP) — Linux 中所有网络通信使用的协议。与 TCP 等其他协议一起使用。

interpreted language — 源代码在用户运行程序时转换为数字代码的语言。每次用户运行程序时都会进行此转换。

interpreted program — 在执行程序时从人类可读形式转换为计算机可使用的格式（数字代码）的计算机程序。

interpreter — 将用解释型语言编写的源代码转换为计算机可执行的数字代码的程序。

interrupt request (IRQ) — 设备向操作系统请求服务的编号信号。

intrusion detection system (IDS) — 帮助网络入侵检测的软件类型。

I/O ports — 设备用于端口映射 I/O 的特殊地址（类似于内存地址）。

IP address — 唯一的网络地址，例如 198.60.45.5，与网络上的某台计算机唯一关联。

IP aliasing — 网络功能，允许单个物理接口分配多个 IP 地址。

IP chains — Linux 内核中使用的旧式数据包过滤（防火墙）技术。

IP forwarding — Linux 网络的一项功能，需要充当路由器，指示 Linux 内核将网络数据包发送到路由表指定的网络接口上。没有 IP 转发，数据包只能从接收到的网络接口发送出去。

IP masquerading — 一种网络地址转换类型，来自 LAN 上多台计算机的数据包被修改，使其看起来像是来自一台计算机。

IP tables — 与 Netfilter 架构在网络栈中提供的编程钩子相关联的规则列表。

iteration — 事件或过程的发生，可或必须多次执行。

jobs — 在 shell 中，作为该 shell 子进程启动的进程。

journaling file system — 跟踪每个磁盘操作以确保其要么完成要么根本不执行的<|message|>文件系统。保留的日志允许操作系统在磁盘操作未成功完成时“回滚”。Linux 支持多个日志文件系统，包括默认使用的 ext3 文件系统。

Journaling File System (JFS) — IBM 开发的高性能日志文件系统，可在大多数 Linux 系统上使用。

KDE desktop — 许多 Linux 发行版使用的图形界面。

KDE System Guard — 显示进程列表并允许您与该列表交互以重新排列或终止进程的图形实用程序。

kdm — KDE 中包含的显示管理器；用于提供图形登录提示。

kernel — 操作系统的核心。内核直接与计算机硬件交互，管理计算机内存、分配给系统上每个程序的时间以及其他系统资源。

kernel modules — Linux 内核的一部分的小程序，可以独立于内核的其他部分添加或删除。用于设备驱动程序、网络支持、文件系统支持和其他内核功能。

kernel ring buffer — Linux 内核中的内存区域，存储部分内核消息。当缓冲区满时，最旧的消息会被丢弃以写入新消息。缓冲区的内容可使用 dmesg 命令查看。

keyword — 在计算机语言中用于定义特定任务或含义的词。

KGet — 用于管理网页下载的图形实用程序。

kickstart configuration file — 用于控制 Kickstart 安装的文本文件，名为 ks.cfg。

Kickstart — 使用预建配置文件控制 Red Hat Linux 或 Fedora 的安装方法，而无需在安装期间对键盘上的问题作出响应。

Korn shell — Bourne shell 的修订版，包含 C shell 的交互式功能，同时保持 Bourne shell 编程风格。Korn shell 由 David Korn 编写。

lease — DHCP 服务器为客户端分配 IP 地址一段特定时间的操作。

LGPL (Library GPL) — GNU 通用公共许可证的特殊版本，旨在规范自由软件和商业软件对软件库的使用。

library — 包含任何程序都可使用的预写编程功能的档案。

LILO (Linux Loader) — Linux 启动管理器。

link — 引用与另一个文件记录相同的物理文件数据的档案记录。参见 symbolic link 和 hard link。

Linux distribution — Linux 操作系统产品，包含 Linux 内核、许多软件组件、安装工具、文档等。

Linux Documentation Project (LDP) — 记录 Linux 用法的最早努力之一。由 Matt Welsh 发起。

Linux Intrusion Detection System (LIDS) — 一种复杂的入侵检测系统，通过修改 Linux 内核来移除 root 对 Linux 系统的全面访问权限。

live CD — 包含可在计算机内存中运行并使用 CD-ROM 上的数据而无需执行传统 Linux 安装的 Linux 发行版的 CD-ROM。绝不会向硬盘写入信息。
