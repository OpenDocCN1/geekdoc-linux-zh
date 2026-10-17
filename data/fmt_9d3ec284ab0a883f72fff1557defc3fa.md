
# 硬件

远程站点的 `ftpmail` 工具处理命令的方式就像直接输入 FTP 中一样。若要通过电子邮件将文件传输给自己，你可以发送以下邮件消息：

- opensite.unc.edu
- cd /pub/Linux
- binary
- get README
- quit

此消息将通过邮件传回 README 文件。`ftpmail` 系统比 FTP 慢，因为你必须等待邮件到达目标机器、被远程系统的 `ftpmail` 工具处理、格式化回复，并将回执消息发送给你。尽管如此，`ftpmail` 为那些没有 FTP 连接的用户提供了一种实用的访问方法，并提供了一种在无需登录的情况下检查几台机器上 Linux 目录内容的简便方法。当你想要定期检查软件更新时，这非常有用。

![](img/4f1928c2f59d55b15e6a00af12d1963c_60_0.png)

## 注意

你想要传输的文件可能超过了系统的最大文件大小限制。某些系统会将文件拆分成较小的块，并在你接收到时允许你重新组装，但其他邮件系统对邮件有较小的尺寸限制，使得使用 `ftpmail` 获取完整的 Linux 软件发行版大文件是不行的。

## Linux 发布版与磁盘集

发布版（Release）是足以安装和运行整个操作系统的 Linux 软件集合。发布版由若干称为磁盘集（disk set）的软件集合组成（尽管它们可能并不存储在磁盘上）。大多数 Linux 系统在你获取发行版集时都包含了多个磁盘集。

虽然大多数 CD-ROM 和 Web FTP 站点的软件相同，但有几个磁盘集的标记方式有所不同。为了说明 Linux 可用的磁盘集，以下列表详细列出了 Slack 发行版中（Linux 最受欢迎的 CD-ROM 版本之一）当前提供的磁盘集组：

- 磁盘集 A 是基础系统。它包含内核和一组基本实用程序，包括 shell、编辑器和用户实用程序。磁盘集 A 是唯一能放入单张高密度软盘上的磁盘集，这意味着你可以用它从软盘上安装并运行 Linux。
- 磁盘集 P 包含 Linux 应用，包括许多不同的编辑器、所有的标准 UNIX 命令列表、手册页（man pages）以及如 GhostScript 等 GNU 扩展。
- 磁盘集 D 包含程序开发软件。该磁盘集包含了 GNU 语言、开发实用程序、库和编译器工具。还有许多用于自定义 Linux 内核的库源码。
- 磁盘集 E 是 GNU emacs 编辑器。
- 磁盘集 F 包含 FAQ（常见问题）文件和其他 Linux 帮助文件。
- 磁盘集 I 包含 GNU 软件的文档文件。
- 磁盘集 IV 包含 Interactive 库、头文件和文档。Interactive 是一个 C++ GUI 开发包。
- 磁盘集 N 是网络软件。该磁盘集包含了 TCP/IP 协议族、UUCP、邮件和其他实用程序以及新闻系统。
- 磁盘集 OI 包含 ParPlace Object Builder 和 Object Interface Library。这些商业开发包是由 ParPlace 为 Linux 开发者提供的。
- 磁盘集 OOP 包含面向对象编程 (OOP) 工具、GNU Smalltalk 编译器以及 Smalltalk 的 X 接口 (STX)。
- 磁盘集 Q 包含 Linux 内核源文件和启动镜像。
- 磁盘集 T 包含 TeX 和 LaTeX 测试格式系统。TeX 被广泛用于排版。
- 磁盘集 TCL 是 Tcl 语言集，包括 Tcl、TclX 和实用程序。
- 磁盘集 Y 是游戏集合。
- 磁盘集 X 是 Xfree86，包含了 X 系统和几个窗口管理器。
- 磁盘集 XAP 包含用于 X 的应用程序、文件管理器、GhostView、库、游戏和实用程序。
- 磁盘集 XD 是 X 开发工具包，包括 X 库、服务器链接工具包和 PEX 支持。如果你正在开发基于 X 的应用程序，必须拥有这个磁盘集。
- 磁盘集 XV 是 X 的窗口管理器。该磁盘集包含了 XView 库和 Open 窗口管理器。你可以使用这些窗口管理器代替磁盘集 X 中的窗口管理器。

尽管磁盘集 A 可以让你从软盘上安装 Linux 系统，但为了进行完整安装（基于硬盘并带有标准实用程序），你应该拥有磁盘集 A、P、D 和 F。这套集合将为你提供一个基于字符的 Linux 系统。如果你想运行 X，还需要磁盘集 X 和 XAP。程序员需要加载开发磁盘集（对于 X 应用程序为 D 和 XD）。

## 总结

本章审视了构成 Linux 系统的软件和硬件。在安装之前，你应该拥有足够运行 Linux 的硬件；否则你将看到各种错误信息（如果系统能够安装的话）。一旦你准备好硬件并知道要从发行版集中安装哪些软件，就是时候将 Linux 安装到硬盘上了。下一章将介绍物理安装过程。第 4 章将介绍引导加载 LILO。

# 安装与升级
## 第 3 章

### 本章内容

- 安装 Linux
- 创建启动磁盘和根磁盘
- 分区硬盘
- 安装 Linux 分区
- 安装 Linux 软件
- 设置启动过程
- 查看已安装的软件文件
- 其他发行版使用包管理器
- 故障排除

# 安装与配置
## 第一部分

某种 Linux 的实现。两张软盘上的系统内容已经足够用来玩 Linux 了，尽管缺少了许多工具。

在大多数情况下，启动软盘和根目录软盘是从名为 `images`（镜像）的现有文件复制而来的。镜像是软盘上系统的一个预编译版本，它消除了从零开始的必要性。CD-ROM 和 FTP 分发版包含了几个用于启动根目录镜像的目录，具体取决于你系统中的硬件。你必须尽可能选择与你的硬件相匹配的镜像，将它们拷贝到软盘上，并使用软盘启动系统。你可以在 DOS 或 Windows 下的 DOS 窗口中完成这些大部分步骤，尽管你不能使用 DOS 拷贝命令来创建启动和根目录软盘。你必须使用一个忽略 DOS 格式化的实用程序来创建软盘。该工具通常称为 `RAWWRITE.EXE`，包含在大多数 Linux 发行版中。

### 选择启动内核和根目录镜像

CD-ROM 下在根目录下通常有名为 `bootdsks.144` 和 `rootdsks.144`（用于 3.5 英寸 1.44M 软盘）以及 `rootdsks.12`（用于 5.25 英寸 1.2M 软盘）的目录，分别包含启动镜像和根镜像。要找到这些目录，请从 CD-ROM 或硬盘上的分区运行程序以检查 CD-ROM。典型 Linux 发行版的 1.44M 软盘的启动和根目录如图 3.1 所示。如果你从 Web 或 FTP 站点拷贝文件，你可以在连接到远程 FTP 机器或 Web 站点下载区域时选择所需的启动和根镜像，并仅将需要的镜像传输到本地机器。

| 文件 | 编辑 | 断开连接 | 设置 | 网络 | 帮助 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| merlin/odrom/slakint12 | MIRROR3.TXT | UPGRADE.TXT | contrib/ | | |
| BOOTING MIRROR.2 | boot12/ | kernels/ | | | |
| COPYING INSTALL_TXT | README.2 | boot160/ | | | |
| Changelog | LBCERT.TXT | SLWAKE.FRQ | contents/ | root0/ | |
| merlin/odrom/slakint/boot144 | root144/ | | | | |
| merlin/odrom/slakint/boot148 | root148/ | | | | |
| README.TXT | astech 0260bd | | | | |
| WTCH.EXE | md iddia rosnet2 | | | | |
| ahandrow mitsui soxi | | | | | |
| had.image.lg -0637 osinel1 | | | | | |
| merlin/odrom/slakint/root144 | | | | | |
| merlin/odrom/slakint/root148 | | | | | |
| README.APK | misguide ttiy44 | | | | |
| README.UMS | 044cs tape44 usds44 | | | | |
| merlin/odrom/slakint/root168 | | | | | |

**图 3.1** 1.44M 软盘镜像的启动和根目录，用于创建启动和根目录软盘以安装 Linux。

### 可用的启动内核镜像

通常可用的启动内核类型在内核镜像目录下的文件（通常为 README、READ.ME 或 WHICH.）中描述。启动内核镜像的命名反映了其在内核中安装了驱动程序的硬件。例如，`scsi` 内核镜像具有 SCSI 系统的驱动程序；如果你在一台配有 SCSI 控制器、硬盘和 CD-ROM 的 PC 上，这就是你想要拷贝到软盘的镜像。可用的启动镜像数量相当大。这些是 CD-ROM 和 FTP 站点提供的主要镜像，以及它们旨在处理的：

- `aztech`：IDE 和 SCSI 硬盘驱动程序以及 Aztech 非 IDE CD-ROM 支持，包括 Aztech、Okana、Orchid 和 Wearnas 非 IDE CD-ROM 驱动器。
- `bare`：仅限 IDE 硬盘驱动程序（不支持 CD-ROM）。
- `cdu31a`：IDE 和 SCSI 硬盘驱动程序，带有 Sony CDU31 或 Sony CDU33a CD-ROM 驱动器。
- `cdu535`：IDE 和 SCSI 硬盘驱动程序，带有 Sony 535 或 Sony 531 CD-ROM 驱动器。
- `idecd`：IDE 和 SCSI 硬盘驱动程序，带有 IDE 或 ATAPI CD-ROM 驱动器。
- `mitsumi`：IDE 和 SCSI 硬盘驱动程序，带有 Mitsumi CD-ROM 驱动器。
- `net`：IDE 硬盘驱动程序和以太网网络驱动程序。
- `sbcd`：IDE 和 SCSI 硬盘驱动程序，带有 Sound Blaster Pro 或 Panasonic CD-ROM 驱动程序。此镜像用于由 Sound Blaster 卡运行的 CD-ROM 驱动器（如许多 Sound Blaster 多媒体套装所示）。
- `scsi`：IDE 和 SCSI 硬盘驱动程序，带有 SCSI 外设（CD-ROM 驱动器）。
- `scsinet`：IDE 和 SCSI 硬盘驱动程序、SCSI CD-ROM 驱动程序和用于网络的以太网驱动程序。SCSI 驱动程序支持 Adaptec 152X、1542、1740、274x 和 284x 适配器、Busologic 适配器、EATA-DMA 适配器（如 DPT、NEC 和 AT&T 卡）、Seagate ST-02 适配器。

### 将镜像写入软盘

将镜像拷贝到软盘中，你需要知道操作系统中软驱器的设备名称。对于大多数系统，第一块软驱器是 `/dev/fd0`，第二个软驱器是 `/dev/fd1`。（某些系统将软驱器视为原始设备，名称为 `/dev/rfd0` 和 `/dev/rfd1`。）使用以下命令将镜像文件拷贝到软盘：

```
dd if=bootimage of=/dev/fd0
```
