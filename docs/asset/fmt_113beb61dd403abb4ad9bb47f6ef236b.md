
电子表格是一种计算机程序，允许你以表格形式组织、分析、存储和处理数据，并使用内置函数进行额外计算。

| 软件生态 | Windows 示例 | Linux/开源示例 |
| :--- | :--- | :--- |
| 电子表格 | MS Excel, Apache Office Calc, LibreOffice Calc, P7-Office Table, MyOffice Table, Polaris Office Web Sheet... | Apache OpenOffice, LibreOffice Calc, P7-Office Table, MyOffice Table, Gnumeric, Quattro Pro... |

# 逐步过渡到 Linux：三合为一

| 程序描述、用于执行额外计算的任务 | Windows | Linux |
| :--- | :--- | :--- |
| 数据库管理系统 | - Microsoft SQL Server<br>- MySQL<br>- PostgreSQL<br>- SQLite<br>- MongoDB<br>- MariaDB<br>- Oracle Database<br>- IBM DB2<br>- Firebird | - MySQL<br>- PostgreSQL<br>- SQLite<br>- MongoDB<br>- MariaDB<br>- Oracle Database<br>- Microsoft SQL Server |
| 创建 ISO 镜像（扩展类型，用于包含 ISO 9660 标准文件系统的光盘镜像） | Nero Burning ROM, Alcohol 120%, UltraISO | Genisoimage, Gnome Disks, AcetoneISO, CDemu |
| 创建演示文稿（以幻灯片形式展示内容，旨在短时间内向观众传达完整信息） | - MS PowerPoint<br>- Apache OpenOffice.org Impress<br>- LibreOffice.org Impress<br>- R7-Ofis Presentatsiya<br>- MoyOfic Presentatsiya Polaris Office Web Slide<br>- Prezi | OpenOffice Impress, LibreOffice.org, MagicPoint, Kuickhow Presentations, Prezi, Yandex Slides |

# 第二章 适用于 Linux 的 Windows 类比软件

| 程序描述、正在执行的任务 | Windows | Linux |
| :--- | :--- | :--- |
| 演示文稿补充 | [Google Slides](https://docs.google.com/presentation) | |
| 项目规划程序（基于各种图表构建进行规划） | MS Project, GanttProject, OpenProj, ProjectLibre | GanttProject, OpenProj, ProjectLibre |
| ... | ... | ... |
| Web 服务器（接受 HTTP 请求并响应 HTML、文件等数据） | Apache, IIS, Tomcat, Nginx, Resin... | Apache, Nginx, Lighttpd, Resin... |
| 文件系统（定义在存储介质上组织、存储和命名数据的物理方法） | FAT16, FAT32, NTFS | Ext4, Ext3, Ext2, ReiserFS, XFS, squashfs, vfat, swap |
| 包管理系统 | Windows Installer (`msiexec.exe`), NuGet | RPM and yum (Fedora, Red Hat, CentOS, RHEL, ALT Linux, Mandriva, Lx, openSUSE), dpkg and apt (Debian, Ubuntu), Pacman (Arch), Portage (Gentoo, FreeBSD), Entropy (Sabayon), PiSi (Pardus) |

# 逐步过渡到 Linux：三合为一

| 程序描述、正在执行的任务 | Windows | Linux |
| :--- | :--- | :--- |
| 软件包格式（文件扩展名） | `.exe`, `.msi`, `.msp` | `.deb`, `.ebuild`, `.rpm`, `.PiSi`, `.tgz`, `.tar.gz`, `.MO`, `.PUP`, `.PET`, `.pkg.tar.xz` |
| 桌面快捷方式（指向文件等对象的指针） | Explorer | Desktop, File Manager, Idesk |
| 存放“已删除”文件的地方（回收站机制，文件被移动而非物理删除） | 回收站 | Trash Can, Libtrash |
| 系统的图形界面（窗口管理器及相关程序集） | Windows Explorer | KDE, Gnome, IceWM, Windowmaker, Blackbox, Fluxbox |
| 娱乐程序/游戏 | Steam（游戏平台）, Minecraft（沙盒游戏） | Steam（游戏平台）, Minecraft（沙盒游戏）, Counter-Strike: Global Offensive（Valve 多人游戏） |

# 第二章 适用于 Linux 的 Windows 类比软件

| 程序描述、正在执行的任务 | Windows | Linux |
| :--- | :--- | :--- |
| 游戏（续） | Counter-Strike: Global Offensive (Valve), Dota 2（免费在线多人游戏）, SuperTuxKart（免费 3D 赛车游戏，主角 Tux）, Xonotic（免费 3D 射击游戏）, OpenTTD（可运行 Transport Tycoon Deluxe 数据文件）... | Dota 2（免费在线多人游戏）, SuperTuxKart（免费 3D 赛车游戏，主角 Tux）, Xonotic（免费 3D 射击游戏）, OpenTTD（可运行 Transport Tycoon Deluxe 数据文件）... |
| 文件管理器 | 资源管理器 | Dolphin |

# 第 II.4 服务软件

实用程序是一组旨在在计算机上执行各种服务任务的软件工具。它们用于支持计算机上操作系统和应用程序的运行。实用程序包括执行此类任务的程序，如添加和删除程序、磁盘碎片整理、清理注册表、创建备份、管理文件、防止病毒以及保持计算机良好状态所需的其他任务。

# 逐步过渡到 Linux：三合为一

表 2.10 列出了 Windows 上的常用工具及其对应的 Linux 软件：

## 表 2.10 – 服务软件

| Windows 中的实用程序 | Linux 中的等效程序 |
| :--- | :--- |
| Windows 任务管理器 | `top`, `htop`, `ps`<br>`top` 是一个显示系统运行信息的命令行程序。它按 CPU 使用率列出进程列表，默认每 3 秒刷新一次。`top` 显示进程 ID、用户、内存占用等。它允许用户停止、继续或杀死进程。<br>`htop` 是 `top` 的改进版本。它也显示正在使用的进程列表，但具有更用户友好且直观的界面。这是一个交互式工具，用于监控系统。 |
| Windows 注册表编辑器 | `/proc` 文件系统<br>Linux 中的 `/proc` 是一个虚拟文件系统，提供了运行进程（包括进程 ID `PID`）以及系统整体的信息（系统及其组件的当前状态）：内存、运行中的设备信息、内核参数（包括页面大小、内核版本和其他详细信息）。在此文件系统中，每个进程都由一个目录表示，进程信息以文件的形式表示。<br>"/proc" 中的所有文件都是动态文件，它们在请求其内容时即时创建。 |

## Windows 下的实用程序

### Windows 资源管理器
- Nautilus、Dolphin、Thunar

它们是 Linux 中流行的文件管理器。`Nautilus` 是 GNOME 桌面环境中的标准文件管理器。`Dolphin` 是一个带有 KDE 图形用户界面的 Linux 操作系统文件管理器。它为管理计算机上的文件和文件夹提供了方便且直观的界面。`Thunar` 是 Linux 上 Xfce 桌面环境自带的文件管理器。它被设计用于管理用户计算机上的文件和文件夹。

### Windows Defender、卡巴斯基、DrWeb、ESET NOD32
- ClamAV、DrWeb、Sophos

### Windows 远程桌面
- VNC、TeamViewer

## Linux 下的对应程序
