
path — 文件系统层次结构中访问特定子目录或文件所经过的所有子目录的描述。路径的每个部分——每个子目录——都用正斜杠分隔。另见相对路径、绝对路径。

PATH — 一个环境变量，其中包含 Linux 系统上的一系列目录，shell 在每次执行命令时都会搜索这些目录。

Perl — 由 Larry Wall 开发的一种流行的编程语言，开发人员使用它来创建用于处理文本文件和完成其他复杂任务的脚本。

physical volumes — 逻辑卷管理器使用的底层物理分区。多个物理卷共同构成一个逻辑卷组，该卷组被划分为用于数据存储的标准分区。

pico — 一个简单的文本编辑器，屏幕上显示使用 Control 键序列执行编辑功能的说明信息。

pipe — 两个命令之间的连接（用 (|) 字符表示），使一个命令的输出用作第二个命令的输入。

Pluggable Authentication Modules (PAM) — Linux 支持的一种安全系统，允许每个需要安全功能的程序使用多个模块进行独立配置，每个模块提供一种特定的安全检查。程序使用位于 /etc/pam.d 中的文件进行配置。

port — 与网络应用程序相关联的数字。

port scanning — 一种网络活动，其中发送到主机的数据包被分析以了解该主机。

port-mapped input/output (port-mapped I/O) — 一种设备通信技术，使用称为 I/O 端口的单独内存地址范围作为设备发送和接收数据的场所。基本上，每个设备特定的端口地址就像一个邮政信箱。

positional variable — shell 脚本中使用的变量，其中包含在启动脚本时在命令行中包含的数据。也称为位置参数。

PostScript Printer Description (PPD) — 包含可由不同操作系统上的多种打印架构使用的标准化打印机描述的文件。PPD 文件用于描述许多类型的打印机，而不仅仅是 PostScript 打印机。

primary DNS server — 另见 master DNS server。

primary partition — 传统硬盘电子设备可以有效管理的四个分区之一。另见逻辑分区。

print filter — 包含使用特定打印机所需的页面描述语言格式化文档的指令的脚本。打印过滤器由 lpr 程序使用，以准备文件发送到物理打印机。

print job — 通过 lpr 命令或图形对话框提交以进行打印的文件。

print queue — 与物理打印机关联的打印机定义；也指存储文件的子目录，以便打印服务器守护进程（如 lpd）逐一检索它们并发送到打印机。也称为打印 spool 目录。

print spool directory — 提交到打印队列的打印作业存储在该目录中，直到它们被发送到打印机。

printing policy — 一份简要文件，描述打印资源如何在组织内使用和管理。

priority — （1）指示提交用于记录的消息严重性的标签。优先级在 syslog.conf 中使用。（2）在进程管理上下文中，分配给 Linux 上运行的进程的值，决定分配给该进程的 CPU 时间多少。也称为 nice 级别。

process — 通过 Linux 内核启动的程序，内核为控制该程序和分配的系统资源（尤其是 CPU 时间和系统内存）而维护有关该程序的数据。

process ID (PID) — Linux 内核在进程首次启动时分配给每个进程的 1 到约 65,000 的数字。PID 在许多实用程序中用于定义实用程序可以影响哪个进程。

programming language — 另见 computer language。

Project Athena — 由 DEC 和 MIT 赞助的项目，旨在为 UNIX 创建图形环境或窗口系统。

protocol — 用于高效通信的信号或单词的有组织模式。

Provisioning — Red Hat Network 功能的最高级别（需付费）。允许额外的升级服务，例如升级应用程序以及操作系统文件，以及从“裸机”同时升级多个系统。

proxy server — 接收 intended for 另一台服务器的客户端请求的服务器。代理服务器随后好像代理服务器本身就是客户端一样发出请求；当目标服务器响应时，代理服务器将响应发送给客户端。

public key encryption — 使用公钥和私钥加密信息的方法；私钥永远不会通过网络发送。

public domain — 无人拥有版权所有权的创作作品（如软件程序）。

Python — 由 Guido van Rossum 开发的脚本语言。常用于创建图形程序。

RAID (redundant arrays of inexpensive disks) — 使用多个廉价硬盘按预定义模式（阵列）排列的存储技术，以提高性能、增加容错性或两者兼而有之。

RAID subsystem — 包含 CPU 和其他组件来控制硬盘阵列的硬件控制 RAID 设备。

RAID-0 — 使用条带化提高磁盘性能但不提供任何容错性的 RAID 级别。

RAID-1 — 使用磁盘镜像显著提高容错性的 RAID 级别。磁盘读取性能也得到改善，但磁盘写入性能下降。

RAID-3 — 使用带奇偶校验信息的条带化来提高性能和增加容错性的 RAID 级别。

RAID-5 — 条带化与奇偶校验分布在 RAID 阵列的所有磁盘上的 RAID 级别（与 RAID-3 相比，RAID-3 的奇偶校验信息存储在单个硬盘上）。

RAID-Linear — 将多个物理设备组合成单个逻辑设备的存储技术。

random access memory (RAM) — 计算机内的易失性电子存储器。

Rapid Application Development (RAD) — 简化复杂软件项目开发的软件程序，通过提供预写模块、帮助跟踪项目的多个部分、允许软件部分的重复使用以及使用许多其他高级技术。

read-only memory (ROM) — 计算机内的非易失性电子存储器。用于存储有关计算机如何启动以及计算机中设备如何配置的信息。

read permission (r) — 文件权限，允许用户读取文件的内容或浏览目录中的文件。用字母“r”表示。

recursive — 在连续的数据集或级别上重复一个过程。

Red Hat Network (RHN) — Red Hat Software 通过订阅提供的服务，使用互联网。该服务自动提供任何安全修复、软件包升级或其他信息，以保持 Red Hat Linux 系统平稳、安全运行。

Red Hat Package Manager (rpm) — 由 Red Hat Software 开发的软件包格式，被众多 Linux 发行版使用。

redirection — 更改 Linux 程序接收输入的位置或发送输出的位置的行为。

redundant arrays of inexpensive disks — 另见 RAID。

regular expression — 使用具有特殊含义的字符（如 * 或 ?）来定义 Linux 程序中字符或数字模式的格式。

ReiserFS — 提供高性能和日志记录的文件系统类型。被多个 Linux 系统默认使用，包括 SUSE 和 Gentoo。

relative path — 如何访问所需子目录或文件的描述，相对于文件系统中的另一个位置（通常是当前工作目录）指定，而不是从文件系统的根目录（使用绝对路径）指定。相对路径不以正斜杠开头。另见绝对路径。

remote printer — 连接到网络上另一台计算机或网络本身的打印机，而不是连接到你正在工作的计算机。

rescue disk — 专门创建用于在系统故障时启动 Linux 系统的磁盘。包含最有可能有助于诊断和修复故障系统问题的软件工具。

rescue mode — Red Hat Linux 中的一种操作模式。用于修复阻止正常启动和操作的系统故障。

resolve — 使用 DNS 协议将域名转换为 IP 地址。

resolver — DNS 的客户端部分，向 DNS 服务器发出请求，以便主机上的其他程序可以使用命名服务器的 IP 地址建立网络连接。

resolving — 将域名转换为 IP 地址，或反之的过程。

resource database — 定义 X 资源在屏幕上如何显示的文件。

resource record — DNS 区域信息文件中的一行，定义 DNS 服务器应如何解析给定的主机或 IP 地址，或提供相关信息。

restore — 将数据从备份位置（例如磁带盒）复制到文件系统上，该文件系统通常使用该数据，并且该数据是从中意外丢失的。

reverse DNS — 使用 DNS 的方法，客户端向 DNS 服务器发送 IP 地址并请求相应的域名。

root — 每个 Linux 系统上的超级用户或管理员用户账户。

root name servers — 指定为 DNS 查询起点的 DNS 服务器。

rotating log files — 将现有日志文件移动到另一个文件名和位置以进行归档或审查的过程。
