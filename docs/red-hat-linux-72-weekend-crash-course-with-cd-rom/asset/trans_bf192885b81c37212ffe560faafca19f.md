

15. `xinetd` 服务器使用 TCP 封装程序启动 Internet 服务。根据 `/etc/xinetd.conf` 文件中的指定，`/usr/sbin/tcpd` 程序会启动其他服务，例如 FTP 和 Telnet。

16. TCP 封装程序为 `xinetd` 启动的 Internet 服务提供访问控制功能。在使用 `xinetd` 启动服务之前，TCP 封装程序会查阅 `/etc/hosts.allow` 文件，以查看请求服务的本机是否被允许使用该服务。如果 `/etc/hosts.allow` 中关于该本机的信息为空，TCP 封装程序会检查 `/etc/hosts.deny` 文件，以查看是否应拒绝该服务。如果这两个文件均为空，TCP 封装程序将允许该本机访问所请求的服务。

17. `GNOME 帮助浏览器` 和 `KDE 帮助` 是两个帮助查看器，可用于查看 Red Hat Linux 图形桌面中的在线帮助信息。

18. 输入 `whatis tr` 可以阅读 `tr` 命令的单行描述。若要查看 `tr` 命令的手册页，请使用命令 `man tr`。

19. 使用 `apropos` 命令通过关键字搜索其他命令。

20. 每个 `HOWTO` 文件都包含关于 Linux 某个领域的一些信息，例如如何在 Linux 中配置硬件或如何创建启动盘。如果您的系统连接到 Internet，您可以通过点击 `GNOME` 桌面上的 `LDP` 图标，然后点击指向 `HOWTO` 文档的链接来访问这些 `HOWTO` 文件。

# 附录

![img](img/5fe8f856723cde0b366f73584b9e64b8_346_0.png)

# CD-ROM 上有什么内容？

本附录为您提供关于随书附赠的 CD-ROM 内容的详细信息。

CD 中包含两个组件：

- Red Hat Linux 7.2
- Red Hat Linux 7.2 周末速成课程评估测试

此外，还包含该书的电子版，该版本可搜索，并可通过 Adobe Acrobat Reader 进行查看。

# 系统要求

请确保您的计算机满足本节列出的最低系统要求。如果您的计算机不满足这些要求中的大多数，使用 CD 上的内容时可能会遇到问题。

- 配备 Pentium 处理器，运行速度为 90 MHz 或更快的 PC
- 至少 32MB RAM，如果使用 X 窗口系统则需 64MB 或更多
- 根据安装选项不同，需要 300MB 到 2.4GB 的空闲磁盘空间（建议 1.2GB 或更多）
- 以太网网络接口卡（NIC）或速度至少为 28,800 bps 的调制解调器
- CD-ROM 驱动器——双速（2x）或更快
- 3.5 英寸软盘驱动器，用于创建启动软盘（可选）

若要安装此 CD 上的所有软件，至少需要 2.4GB 的硬盘空间。

# CD 上有什么内容

CD-ROM 包含源代码示例、应用程序以及该书的电子版。以下是按类别排列的 CD-ROM 内容摘要。

# Red Hat Linux 7.2

CD-ROM 包含所有 Red Hat Linux 7.2 二进制文件以及 Linux 2.4.7 内核，这是截稿时（2001 年 9 月）可用的最新 Linux 内核版本。除了 Linux 内核外，Red Hat Linux 还包含大量 Linux 应用程序。以下是 Red Hat Linux 7.2 CD-ROM 上一些重要的软件包：

- Linux 2.4.7 内核，包含适用于所有主要 PC 硬件配置的驱动程序模块，包括 IDE/EIDE、ATA 和 SCSI 驱动器、PCMCIA 设备、许多 USB 设备以及 CD-ROM 驱动器。
- 一套完整的安装和配置工具，用于设置硬件设备（如磁盘驱动器、视频硬件、键盘和鼠标）和服务。
- 基于 XFree86 包、带有 GNOME 和 KDE 桌面的图形用户界面（GUI）。
- 适用于 Internet、局域网和内部网的完整 TCP/IP 网络支持。
- 用于通过专用连接（如 xDSL）、PPP 和拨号串行通信程序将您的 PC 连接到互联网服务提供商（ISP）的工具。
- 完整的 Internet 应用程序套件，包括电子邮件（sendmail, mutt, pine, elm, mail）、新闻组（fnn, tin, srn, trn）、Internet 中继聊天（ircII）、Telnet、FTP 和 NFS。
- Apache Web 服务器 1.3.19（用于将您的 PC 变为 Web 服务器），Netscape Communicator 4.77，以及 Mozilla 0.9（用于浏览网络）。
- Samba 2.0.7 局域网管理器软件，用于 Microsoft Windows 互操作性。
- 多个文本编辑器（GNU Emacs 20.7, vim）。
- 图形和图像处理软件，如 The GIMP、XPaint、Ghostscript、Ghostview 和 ImageMagick。
- 用于播放音频 CD、MP3 和其他音频格式的多媒体应用程序（xplay、XMMS 1.2、KSCD 1.3、GTCD 1.2）、混音器、录音机和音频电平表。
- 编程语言（GNU C 和 C++ 2.96、Perl 5.6.0、Tcl/Tk 8.3.1、Python 1.5.2、GNU AWK 3.0.6）和软件开发工具（GNU Debugger 5.0、CVS 1.11、RCS 5.7、GNU Bison 1.28、flex 2.5.4、TIFF 和 JPEG 库）。
- 完整的标准 UNIX 实用程序套件。
- 访问和使用 DOS 文件和应用程序的工具（mtools 3.9.7）。
- 游戏，如 GNU Chess、Mahjongg、Reversi、Minesweeper、Freecell、Gnobots、AisleRiot。

# Red Hat Linux 7.2 周末速成课程评估测试

CD-ROM 包含 60 道带答案的多项选择题。这些测试题有两个用途。您可以使用它们来评估自己对 Red Hat Linux 的了解程度，从而确定可以跳过哪些课程。在阅读本书的特定章节后，您也可以浏览这些题目以评估自己学到了多少。题目按课程组织；因此，它们遵循本书讨论主题的顺序。每道题目旁边都注明了其所对应的课程。

# Red Hat Linux 7.2 周末速成课程电子版

本书的完整（且可搜索的）文本以 Adobe 可移植文档格式（PDF）形式存储在 CD-ROM 上，可通过 Adobe Acrobat Reader（亦包含在内）阅读。

# Adobe Acrobat Reader 5.0

CD-ROM 包含 Adobe Systems 最新版的 Acrobat Reader，使您能够阅读流行的 Adobe 可移植文档格式（PDF）文档。有关 Adobe Acrobat Reader 的更多信息，请访问 http://www.adobe.com/。

# 安装 Red Hat Linux

由于本简短附录篇幅有限，无法解释如何从 CD 安装 Red Hat Linux。请遵循书中第 1 至第 3 课的说明，在您的系统上安装 Red Hat Linux。

# 故障排除

如果您在安装或使用 CD-ROM 程序时遇到困难，请尝试以下解决方案：

- 确保您的 PC BIOS 已正确配置。随附的 CD-ROM 支持启动，但 PC 必须要在 BIOS 中启用从 CD-ROM 启动功能才能正常工作。
- 创建可启动软盘以安装软件。如果您无法从 CD-ROM 启动，请使用第 1 课中的说明创建可启动软盘以安装软件。

如果您仍然无法解决 CD 相关的问题，请致电 Hungry Minds 客户服务热线：(800) 762-2974。在美国境外，请致电 (317) 572-3993。Hungry Minds 仅针对安装和其他一般质量控制问题提供技术支持；有关应用程序本身的技术支持，请咨询程序供应商或作者。

# 索引

# 符号和数字

- `!!`（感叹号）用于重复上一条命令，67
- `"`（引号）用于选项中嵌入空格，62, 66, 69
- `&`（和号）用于后台执行命令，68–69
- `*`（星号），可执行文件，55
- `*`（星号）用于匹配零个或多个字符，64, 65, 66
- `-`（减号）和 Linux 文件系统，59
- `-`（破折号）用于长选项，63
- `.`（点）文件（隐藏文件），56
- `.`（单点），Linux 文件系统，54
- `..`（两个点），Linux 文件系统，54
- `/`（根目录），49, 50
- `/bin/` 目录，61
- `/dev/`, 11, 112, 122
- `/dev/`, 115
- `/dev/fb0`, 163
- `/dev/fb1`, 163
- `/etc/` 目录，122
- `/etc/at.allow` 文件，256
- `/etc/at.deny` 文件，256
- `/etc/cron.allow` 文件，258
- `/etc/cron.deny` 文件，258
- `/etc/crontab` 文件，260–261
- `/etc/exports` 文件，149, 151
- `/etc/hosts` 文件，126
- `/etc/hosts.allow` 文件，127, 128, 298, 299
- `/etc/hosts.conf` 文件，126
- `/etc/hosts.deny` 文件，127–128, 298, 299
- `/etc/httpd/conf` 目录，144
- `/etc/initdb` 文件，224–227, 228
- `/etc/mtools.conf` 文件，166
- `/etc/pam.d` 目录，297
- `/etc/passwd` 文件，295, 301
- `/etc/rc.d` 目录，224
- `/etc/rc.d/rc.script`, 228–229
- `/etc/rc.d/rc.local` 脚本，229
- `/etc/rc.d/rc.sysinit` 脚本，228
- `/etc/resolv.conf` 文件，126–127, 128, 137
- `/etc/samba/smb.conf` 文件，153, 154–156
- `/etc/services` 文件，141
- `/etc/shadow` 文件，296, 297, 301
- `/mnt/cdom/RedHat` 目录，233
- `proc`（进程文件系统），288–291
- `sbin/hpnam`（磁盘性能和磁盘使用情况程序），287, 291
- `sbin/ifconfig`（接口检查），124, 134
- `sbin/route`（路由表检查），124–125, 134
- `sbin/runlevel`（当前运行级别），224
- `usr/bin/sendconfig` 实用程序，181–182
- `var/ftp/pub` 目录，145
- `var/log` 目录，295, 299–300
- `var/log/messages` 文件，113
- `var/spool/mail` 目录，141
- `var/www/html` 目录，144
- `:`（冒号）用于组合命令，64
- `;`（分号）用于连接命令，63, 64
- `<`（小于号）用于 I/O 重定向，64–65
- `>`（大于号）用于 I/O 重定向，64–65
- `?`（问号）用于匹配单个字符，65, 66, 77
- `@`（at 符号），链接，55
- `[...]`（括号）用于匹配字符集，65, 66
- `\\`（反斜杠，回车）用于多行命令，63
- `\\`（反斜杠）用于特殊字符搜索，70
- DOSUTIL 子目录（在 CD-ROM 上），7
- `|`（管道符）用于组合命令，64
- 10Base2（细网）电缆，119–120, 121
- 10BaseT（非屏蔽双绞线，UTP）电缆，120, 121

