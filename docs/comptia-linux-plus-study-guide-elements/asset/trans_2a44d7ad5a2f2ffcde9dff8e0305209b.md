
# P

**package database** 参见*已安装文件数据库*。

**packet** 一个带有信封并通过网络发送的有限数据集合。另见*信封*。

**packet filter firewall** 一种在单个网络数据包层面运行的防火墙，根据源地址、目标地址和端口等信息来决定通过或拒绝数据包。

**packet sniffer** 一种在底层监控网络流量的程序，用于诊断问题和捕获数据。数据包嗅探器既可用于合法的网络诊断，也可用于数据窃取。

**PAM** 参见*可插拔身份验证模块（PAM）*。

**Parallel ATA (PATA)** 传统的ATA接口形式，其中多个位同时传输。另见*Serial ATA (SATA)*。

**parameter** 在命令行上传递给程序的选项，或作为配置文件的一部分的选项。

**parent process** 一个相对术语，指启动另一个进程的进程。例如，如果你从shell中启动一个编辑器，那么shell进程就是该编辑器的父进程。

**parent process ID (PPID)** 与进程父进程相关的PID编号。

**partition** 硬盘中划定用于存储单个文件系统（含义1）的连续部分。也用作动词，描述在硬磁盘上创建分区的过程。

**partition table** 描述硬磁盘上分区布局的磁盘数据结构。另见*主引导记录（MBR）*和*GUID分区表（GPT）*。

**PATA** 参见*Parallel ATA (PATA)*。

**path** 一个由冒号分隔的目录列表，程序文件可能在这些目录中找到。（类似的列表定义了目录、字体和其他文件类型的位置。）

**payload** 网络数据包中包含实际待传输数据的部分，与信封相对。

**PCI** 参见*Peripheral Component Interconnect (PCI)*。

**PCL** 参见*Printer Control Language (PCL)*。

**peripheral** 连接到计算机并由计算机控制的设备。许多外围设备，如网络摄像头和键盘，位于计算机主机箱外部。某些定义包括位于计算机主机箱内部的设备，如硬盘和CD-ROM驱动器。

**Peripheral Component Interconnect (PCI)** 一种扩展总线，其速度远快于旧式的ISA总线。现代计算机通常包含多个PCI插槽。

**permission bit** 用于定义特定用户或用户组是否对文件具有特定类型访问权限的单个位。例如，所有者的执行权限位决定所有者能否将文件作为程序运行。权限位共同构成了文件的模式。

**Personal Home Page (PHP)** 参见*PHP: Hypertext Preprocessor (PHP)*。

**phishing** 发送虚假电子邮件或建立虚假网站以收集敏感个人信息（通常是信用卡号）的过程。

**PHP** 参见*PHP: Hypertext Preprocessor (PHP)*。

**PHP: Hypertext Preprocessor (PHP)** 一个递归缩写，指一种用于Web服务器的脚本语言，使其能够根据特定用户或目的定制Web页面。*PHP*有时被展开为*Personal Home Page*。

**PID** 参见*process ID (PID)*。

**PIO** 参见*Programmed Input/Output (PIO)*。

**pipe** 执行两个程序的方法，使一个程序的输出作为第二个程序的输入。在Linux shell中，管道连接的程序通过竖线（|）分隔。

**pipeline** 参见*pipe*。

**Pluggable Authentication Modules (PAM)** Linux的用户身份验证子系统。PAM具有高度可配置性；你可以为任何给定的身份验证服务（如网络服务器或登录程序）创建模块堆栈，从而允许你自定义所使用的身份验证数据库以及在登录尝试期间执行的其他任务。

**Point-to-Point Protocol (PPP)** 一种通过RS-232串行线或调制解调器在两台计算机之间建立TCP/IP连接的方法。

**port number** 标识数据报文的来源或目标程序的编号。当程序发起网络连接时，它会将自己关联到一个或多个端口，使其他计算机能够唯一地寻址该程序。

**Post Office Protocol (POP)** 一种邮件服务器协议，由接收方启动消息传输。POP与IMAP的区别在于，POP不提供任何让接收方在服务器上组织和存储消息的手段。

**PostScript** 一种用于许多高端打印机的编程语言。PostScript针对在打印页面上显示文本和图形进行了优化。Linux程序Ghostscript将PostScript转换为许多低端和中端打印机能理解的位图格式。

**PostScript Printer Definition (PPD)** 一个提供打印机能力信息的配置文件，如纸张大小、是否支持彩色打印等。

**PowerPC** 参见*Power Performance Computing (PowerPC or PPC)*。

**Power Performance Computing (PowerPC or PPC)** 由摩托罗拉、IBM和苹果在20世纪90年代初创建的CPU架构。从1994年到2006年，PowerPC CPU是麦金塔计算机的核心（苹果自那时起已转向x86-64 CPU）。如今它们主要在某些专用设备中使用。

**PPC** 参见*Power Performance Computing (PowerPC or PPC)*。

**PPD** 参见*PostScript Printer Definition (PPD)*。

**PPID** 参见*parent process ID (PPID)*。

**PPP** 参见*Point-to-Point Protocol (PPP)*。

**primary boot loader** 由BIOS运行的第一个引导加载程序。

**primary partition** 一种在MBR中硬磁盘分区表内的数据结构中定义的MBR分区。MBR分区方案每个硬磁盘仅支持四个主分区。

**print queue** 等待打印的文件存储位置。

**Printer Control Language (PCL)** 由惠普开发的一种用于控制打印机的语言。（许多惠普的竞争对手也使用PCL。）PCL最常见于中端激光打印机，但某些喷墨打印机也支持该语言。存在多种PCL变体，最常见的是从PCL 3到PCL 6的范围。

**printer driver** 一种软件组件，将应用程序生成的可打印数据转换为适合特定型号打印机的格式。在Linux中，打印机驱动通常驻留在Ghostscript中，但某些应用程序包含一组打印机驱动以直接打印到各种打印机。

**privileged port** 编号低于1024的端口（参见*port number*）。Linux限制对这类端口的访问仅限*root*。在计算发展的早期，任何在特权端口上运行的服务器都被视为可信的，因为只有在专业系统管理员配置下运行的程序才能在这些端口上运行。如今情况已不再如此。另见*unprivileged port*。

**process** 一段由Linux内核独立维护并运行的代码，与其他代码段分开。大多数进程对应正在运行的程序。一个程序可以运行多次，产生多个进程。

**process ID (PID)** 与特定进程关联的编号。如`kill`和`renice`等实用工具基于PID工作，使你能够终止它们或更改它们的优先级。

**Programmed Input/Output (PIO)** 内存和扩展卡之间数据传输的一种方法，其中CPU主动执行传输。PIO通常比DMA消耗更多的CPU时间。

**protocol stack** 实现跨网络通信标准手段的驱动程序、内核过程和其他软件的集合。两台计算机必须支持兼容的协议栈才能通信。当今最受欢迎的协议栈是TCP/IP。

**pull mail protocol** 一种由接收方启动传输的邮件协议。示例包括POP和IMAP。

**push mail protocol** 一种由发送方启动传输的邮件协议。SMTP是最常见的推送邮件协议。

# R

**RADIUS** 参见*Remote Authentication Dial-In User Services (RADIUS)*。

**RAID** 参见*redundant array of independent disks (RAID)*。

**random access** 访问存储设备（RAM、硬盘等）的一种方法，其中信息可以按任意顺序存储或检索，且几乎或没有速度损失。另见*sequential access*。

**RDP** 参见*Remote Desktop Protocol (RDP)*。

**redirection** 一种过程，将程序的标准输出或标准错误发送到文件而不是屏幕，或者从文件而不是键盘获取程序的标准输入。另见*standard input*、*standard error*和*standard output*。

**redundant array of independent disks (RAID)** 两个或更多被作为单个物理硬磁盘处理的磁盘。根据配置方式，RAID可以提高速度、可靠性或两者。它可以由专用硬件RAID控制器实现，或通过特殊的内核选项和Linux配置实现。

**regular expression** 一种匹配文本信息的方法，这些信息在重要方面可能有所不同但具有共性。正则表达式捕获共性并使用各种类型的通配符来匹配可变信息。

**ReiserFS** Linux的几种日志文件系统之一。ReiserFS是为Linux从头开发的。

