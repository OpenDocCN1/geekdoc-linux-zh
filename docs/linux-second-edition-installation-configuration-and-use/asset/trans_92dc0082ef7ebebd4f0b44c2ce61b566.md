

# LINUX 特定于在线文档 77

通常情况下，Linux 发行版只提供极少数的常见问题解答（FAQ）（如果有的话，通常可以在 `/usr/doc/faq` 或 `/usr/doc/faq` 目录下找到）。

最有趣的是 Linux FAQ：当 Linux 出现问题时，这个文件应该是首选参考。它涵盖了如安装、兼容性问题、Linux 文件系统处理、X 窗口系统等主题。

# HOWTO – 它是如何工作的？

HOWTO 文本与 FAQ 文件的主要区别在于，它们是系统化构建的，并传授基础知识。HOWTO 文本是 Linux 关于安装、配置和硬件问题最重要的信息来源。唯一的缺点是许多文本内容相当详实。你获得的信息比你实际需要的多得多。

涵盖的主题包括：对特殊硬件组件的处理（SCSI 磁盘、CD-ROM 驱动器、磁带机、以太网卡、键盘）以及 Linux 使用的特殊功能（打印、网络配置，包括 UUCP、Term 和 News 等）。以 ASCII 格式计算，HOWTO 文本总共占用超过 4 MB —— 这比这本白书要稀有得多！（作为对比：本本的 `.tex` 文件占用高达 2 MB）。

HOWTO 文件通常位于 `/usr/doc/HOWTO`。在 Linux 下，HOWTO 文本有两种形式：普通版本和精简版本。精简版本位于 `mini` 子目录中，仅以 ASCII 格式存在。相反，“大型”HOWTO 也可以以其他格式提供（`other-formats` 子目录）。

最有趣的格式是 HTML 版本，它可以被任何 WWW 浏览器读取，而且由于不同的字体大小和交叉引用，它比 ASCII 版本更清晰、更容易阅读。

像往常一样，最新版本可以在互联网上找到：

```
http://metalab.unc.edu/LDP/HOWTO
```

作为一个一般原则，你应该始终检查所有在线文件的最后修改日期。偶尔，仍然存在一些文件，其内容已由于所描述程序的较新版本而早已过。

# Linux HOWTOs

| 3dfx | Busmouse | DNS | Esperanto |
| AX25 | CD-Writing | DOS-Win-to-Linux | Ethernet |
| Access | CDROM | DOS-to-Linux | Finnish |
| Alpha | Chinese | DOSEMU | Firewall |
| Assembly | Commercial | Danish | French |
| Benchmarking | Config | Distribution | Ftape |
| BootPrompt | Consultants | ELF | GCC |
| Bootdisk | Cyrillic | Emacspeak | German |
| Glibc2 Multi-Disk RPM Tips |
| HAM Multicast Reading-List UMSDOS |
| Hardware NET-3 ROOT-AID UPS |
| Hebrew NFS SCSI-Programming UUCP |
| INFO-SHEET NIS User-Group |
| IPX Networking-Overv SRM VAR |
| ISP-Hookup Optical-Disk VME |
| Installation Oracleing VMS-to-Linux |
| Intranet-Server PCI Serial-Programming VMS2linux |
| Italian PCMCIA Shadow-Pass Virtual-Services |
| Java-CGI PPP Slovenian WWW |
| Kernel Parallel-Process Sound WWW-MSQL |
| Keyboard-Console Pilot Sound-Playing XFree86 |
| LinuxDoc+Emacs+IS Polish Spanish XFree86-Video-Tim |
| MGR PostgreSQL Text-Terminal |
| MILO Printing |
| Mail Printing-Usage Thai |

# Linux-Mini-HOWTOs

- 3-Button-Mouse Firewall-Piercing Man-Page Sendmail+UCP
- ADSL GIS-GRASS Modules Small-Memory
- ADSM-Backup GTK+-BSS-550 Multiboot-LILO Software-Building
- AI-Alife Hard-Disk-Upgrade QCD-Terminal Software-RAID
- Advocacy IC-Post-Program NFS-Root Soundblast-Awe
- Backup-With-FDS IP-Alias NFS-Root-Client StarOffice
- Battery-Powered IP-Masquerade Netscape+Pro Term-wall
- Boca IP-Subnetwork News-Leisfite TKR
- BogoMips ISP-Connectivity Offline-Mapping Token-Ring
- Bridge Install-ZIP Partition Ultra-DMA
- Bridge+Firewall Kernel Partition-Rescue Update
- Bzip2 LBX Path Upgrade
- Cable-Model LILO Pre-Install-Check VPN
- Clock Large-Disk Process-Accounting Visual-Bell
- Coffee Leased-Line Linux+00DS+Win95 Pro-AppX-Subset Win-Model-Share
- Colour-is Linux+FreeBSD Qmail-MH Public-Web Word
- Cyrus-IMAP Linux+NT-Loader Quota XFree88-Inside
- DHCP Linux+Win95 RCS XTerm-Title
- DHCPcd DPT-Hardware-RAID Loadin+Win95 README ZIP-Drive
- Dialad Loopback-Root-FS RPM+Slack ZIP-Install
- Diskless Mac-Terminal Remote-Boot mini-list
- Ext2fs-ndeletion Mail-Queue Remote-Apps
- Fax-Server Mail2News SLIPP-Emulator

# LDP – Linux 文档项目

在 Linux 文档项目的框架内，已经出现了更长的文本——实际上是整本书。这些文本最初也只以电子形式提供，但至少《Linux 网络管理员指南》已经出版了纸质书。

- Sven Goldt, Sven van der Meer 等：《Linux 程序员指南》
- Larry Greenfield:《Linux 用户指南》
- Michael K. Johnson:《内核黑客指南》
- Olaf Kirch:《Linux 网络管理员指南》
- David:《Linux 安装》
- Matt Welsh:《Linux 开始》
- Lars Wierzens:《Linux 系统指南》

如果这些文档没有随发行版提供，你可以在不同的格式中找到（以及更多）：

http://metalab.unc.edu/LDP/linux.html

# 内核文档

在 `/src/linux/Documentation` 目录下你会发现关于内核的大量信息（如果你安装了的话）。这些信息通常假设你对硬件和编程有基本知识。即使你不编译内核，`/src/linux/Documentation` 目录下的信息也很有价值。

如果你不想编译内核，只需执行 `make` 或 `makeconfig` 即可查看。`/src/linux/` 目录下的某些关于内核的文档非常有用。

# KDE 和 GNOME 帮助系统

对于 KDE 的帮助信息通常可以通过点击菜单来获取。在两种情况下，KDE 和 GNOME 的帮助文档都以 HTML 格式显示，这意味着它们比 ASCII 版本更清晰、更易于阅读。

如前几个章节所述，KDE 的帮助信息可以通过简单的按下 F 键获取。在 GNOME 程序中，你需要使用 `help` 按钮。

通常情况下，最新版本可以在互联网上找到：

# Linux 文档项目 (LDP)

在 Linux 文档项目框架内，出现了更长的文本。这些文本最初也只以电子形式提供，但至少《Linux 网络管理员指南》已经出版了纸质书。

- Sven Goldt, Sven van der Meer 等：《Linux 程序员指南》
- Larry Greenfield:《Linux 用户指南》
- Michael K. Johnson:《内核黑客指南》
- Olaf Kirch:《Linux 网络管理员指南》
- David:《Linux 安装》
- Matt Welsh:《Linux 开始》
- Lars Wierzens:《Linux 系统指南》

如果这些文档没有随发行版提供，你可以在不同的格式中找到（以及更多）：

# Linux 文档 (LDP)

# 单个软件软件包的文档

关于各种软件软件包（编程语言、工具等）的附加文档通常安装在 `/usr/doc/packages/name/` 目录下。这些文件的范围差异很大。通常你只会找到一个包含版权声明和查找剩余文档简述的 README 文件。

显然，并不是所有程序都遵循这一惯例（那样太简单了）。你仍然应该检查相关程序的安装目录。例如，你会在 `/usr/lib/TeXX/texmf/doc` 目录下发现大量关于 BibTeX（TeX 文档）的在线文档。

对于某些程序（例如 Gimp），在线文档非常庞大，因此存储在一个独立的软件包中，而该包不会自动安装。因此，仔细查看未安装的软件包列表通常是值得的。

