
`/dev/nvram` 选项启用一个新的字符设备（`mknod c /dev/nvram 10 144`），用于对 50 字节 CMOS 内存进行读写访问。

所有计算机都有实时时钟；Linux 允许你使用它。此选项支持一个新的字符设备（`mknod c /dev/rtc 10 135`），用于生成从 2Hz 到 8kHz 的可靠信号。时钟还可以编程为 24 小时闹钟，在闹钟响起时触发 IRQ8。`rtc` 模块通过同步的 ioctl 调用控制，最常用于高频数据采集场景，其中你不想通过时间查询调用消耗 CPU 周期。使用 `rtc` 模块的示例代码可在 `Documentation/rtc.txt` 中找到。

## DoubleTalk 语音合成器

这里没有意外，不过语音合成器的用户可能也会对 Blindlinux（盲人发行版）和 Emacspeak 感兴趣。Linux 独树一帜，是赋予盲人用户完全访问其计算机所有功能以及完全访问互联网所有服务的唯一操作系统。

## Linux 视频（V4L）

Video4Linux (`V4L`) 是音频/视频捕获或叠加卡、无线电调谐源、图文电视以及其他电视相关 VBI 数据的通用编程 API。如果你计划使用任何当前的电视/调频卡，则需要 V4L 支持，V4L 也可用于视频会议摄像头，如 Connectix Qcam。要使用这些服务，你还需要支持 V4L 的应用程序。目前有几个应用程序存档在 V4L 档案库中 (`ftp://ftp.uk.linux.org/pub/linux/video4linux`)，还有几个，包括捕获和网络摄像头应用，列在 Room Three 网站上 (`http://roomrunner.swansea.linux.org.uk/v4l.shtml`)。

## 游戏杆支持

Linux 现在支持数字、串行和一些 USB 游戏杆控制器。开发人员还希望包含力反馈游戏杆的支持。支持设备和应用程序的最新列表可在 Linux 游戏杆网页 (`http://atrey.karlin.mff.cuni.cz/vojtech/joysticks/`) 中找到。

## Ftape，软盘磁带设备驱动程序

此选项适用于连接到现有软盘驱动器控制器或自带高性能 FDC 的磁带驱动器。随着廉价 CD 刻录机的广泛普及，磁带备份系统正变得稀有，但仍具有一席之地。

## 文件系统

Linux 是唯一为异构计算机网络提供共同基础的操作系统。在你第一次安装 Linux 时，任务之一是从支持的文件系统长列表中选择你的 Linux 分区。这一传统在内核文件系统和网络文件系统支持中得以延续。当所有这些都与通过模拟器透明启动任意可执行文件的能力（参见“其他二进制支持”部分）结合时，Linux 中跨操作系统集成的程度就变得非常清晰。

文件系统对话框本身没有太多意外。如果你需要软盘、CD-ROM、ZIP 驱动器或支持的文件系统中的硬盘分区，你可以将其包含在核心内核中，或者，最好地，将其构建为模块。除非内核是为专门的嵌入式应用构建的，否则强烈推荐 `/proc` 和 `/dev/pts` 文件系统；没有这些功能，许多标准实用程序将无法工作。

### MS-DOS 和 VFAT（Windows）文件系统

MS-DOS 和 VFAT 文件系统值得特别考虑，仅因为它们如此普遍。当前内核对 DOS、Windows、Windows 95 和 Windows NT 使用的 MS-DOS/VFAT 磁盘的支持只能读写未压缩的磁盘，不能用于双间隔（DoubleSpaced）磁盘或分区。要访问双间隔驱动器，你需要使用 DOSEMU 模拟器，或尝试 `dmsdosfs` 工具 (`ftp://metalab.unc.edu/pub/Linux/system/filesystems/dosfs/`)。

如果你只计划通过 `mtools` 程序（`mdir`、`mcopy` 等）访问 MS-DOS 磁盘，则不需要 MS-DOS 支持。只有当你计划在第二个分区或硬盘上运行 Linux 并需要访问 MS-DOS 侧的文件，或者你想要挂载 ZIP 驱动器或其他共享介质以在 Linux 和 MS-DOS 之间传输文件时，才需要 MS-DOS 支持。

VFAT 添加了对长文件名的额外支持，并为 DOS 代码页和国家语言支持提供了几个选项，以应对默认行为中处理 DOS 11 字符文件名限制的问题。这些转换选项的详情可在 `Documentation/filesystems/vfat.txt` 中找到。

### ISO 9660、UDF 和 DVD 支持

UDF 是新的标准 CD-ROM 格式，旨在取代 ISO9660。目前，UDF 支持意味着数字视频光盘（DVD）支持。虽然内核支持传统的 ISO 9660 格式 CD-ROM，并将支持 Microsoft Joliet 扩展用于 Unicode 文件系统，但它尚未提供 UDF 支持。DVD 和其他 UDF 周边设备的驱动程序可通过 TryLinux UDF 项目 (`http://www.trylinux.com/projects/udf/`) 获取。

### 本地语言支持

这一部分有点名不副实。这些选项确实支持不同的文化语言，但它们只支持在 Microsoft 文件系统中读取和显示这些字符集。

第一个部分选项列出了 Microsoft 代码页，仅当你的系统需要从 MS-DOS 或 Windows 文件系统读取文件名时才是一个问题。注意，代码页支持仅适用于文件名，而不适用于文件内容。同样，为了显示 Microsoft VFAT 或 Joliet CD-ROM 文件系统中的字符，你也需要包含至少一个 NLS 选项。你可以为两个系统选择任意数量的语言，其中任何这些都可以构建为模块，仅在需要时加载。

### 网络文件系统

网络文件系统允许你共享磁盘资源。虽然在大网络上对此有明显的应用，但即使是在小型办公室/家庭办公室环境中，也可能希望分发资源。例如，我们的办公室使用一台回收的旧 486/33 机器作为吸烟休息区的多用户 X 终端。这台机器从 60MB 的硬盘运行 Linux 2.2.7。60MB 足以让系统启动并运行，然后，使用 NFS 从楼上实验室提供软件目录和用户磁盘资源。

与文件系统和分区支持类似，Linux 为几乎任何异构网络提供了通用粘合剂。网络文件系统也不例外。2.4 内核可以创建一个枢纽，将旧版和新版 UNIX 文件系统、Windows 95/NT、OS/2 以及 Novell 系统绑定在一个工作站或一台服务器上。

## CODA 分布式文件系统

CODA 是一种新的分布式文件系统技术，有点像 NFS，但更灵活、更安全、更高效。CODA 包含身份验证和加密功能、磁盘复制、缓存以及对不连续连接（如笔记本电脑和远程办公者）的支持。当前 Linux 内核支持将允许你使用 CODA 客户端程序。有关此文件系统客户端程序和其他信息，请参见 CODA 主页（<http://www.coda.cs.cmu.edu>）。Venus 客户端支持也在 `Documentation/filesystems/coda.txt` 中有非常详细的描述。

## NFS

NFS，分布式文件系统的老黄牛，虽饱受诟病，但仍是标准。随着时间推移，CODA 可能会取代 NFS，但在可预见的未来，NFS 是我们唯一的选择。NFS 还需要运行两个程序：`nfsd` 和 `mountd` 守护进程。如果你正在为无盘工作站配置内核，NFS 显然不能作为模块加载，你需要选择 **IP: Kernel Level Autoconfiguration**（IP：内核层自动配置）和 **NFS Root Partition**（NFS 根分区）选项。

对于 NFS 服务器，你可以选择运行 `nfsd` 守护进程或启用内核级 NFS 服务器。后者的优势在于速度快得多（因为它运行在内核空间），但仍有待进一步验证。

## SMB（Windows 共享）和 NCP

如果你的局域网包含使用 TCP/IP 的 Windows for Workgroups、Windows 95/97、OS/2-LanManager 或 NT 机器，此选项将允许你挂载这些机器上的共享目录。请注意，SMB 支持仅针对客户端；向 Windows 机器导出目录需通过 Samba 守护进程实现。

NCP（NetWare 核心协议）为 Novell 网络使用的 NetWare（IPX）文件共享提供了类似的功能。与 SMB 支持一样，这是用于在本机上挂载远程 NCP 驱动器的。你不需要此选项即可成为 NCP 服务器。

## 分区类型

Linux 是唯一的、直接提供文件系统兼容性的操作系统，甚至支持到分区格式级别。本节的选项增加了对 BSD、SunOS、Solaris 和 Macintosh 分区的支持，允许你直接读写采用这些专有格式的磁盘。

例如，通过包含外部分区支持，你可以访问多启动机器（如 Mac OS 与 Linux 或 BSD 与 Linux）中的所有分区，或者与其他一个或多个系统进行光盘或 ZIP 软盘的交换。

## 控制台驱动程序

`控制台驱动程序`下的前两个选项非常直接。第一个启用标准 VGA 显卡（文本模式）的支持，第二个添加对 `/etc/lilo.conf` 中 `vga` 选项的支持，该选项在启动过程中设置 VGA 文本模式。

其余选项则较为晦涩。
