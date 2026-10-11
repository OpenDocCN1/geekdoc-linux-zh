
# Linux 与 Windows 集成

![](img/a1ad58e4259f15e8b2826ecf57a28362_0_0.png)

- 您的完整 Linux/Windows 集成指南
- 详细介绍双启动问题、数据兼容性和网络配置
- 为 Windows 工作站实现 Samba 文件/打印服务
- 提供跨平台数据库访问

MIKE McCUNE

富海海斯州立大学

![](img/a1ad58e4259f15e8b2826ecf57a28362_2_0.png)

McCune, Mike.

MIKE McCUNE

Scott Hawkins

Scott Hawkins

Mike McCune

Bob Neveln

Ellie Quigley

Bob Toxen

引言 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . XIII

# 在同一台 PC 上使用 LINUX 和 WINDOWS

## 1.1 分区

## 1.2 文件系统

## 1.3 分区命名

## 1.4 Linux 与 Windows 95/98

### 1.4.1 启动 Linux

### 1.4.2 `LILO` 故障排除

### 1.4.3 启动 Windows 9x

### 1.4.4 `NTFS`

### 1.4.5 使用 `NTFS` 启动

### 1.4.6 管理 `NTFS` 文件系统

### 1.4.7 使用 `NTFS`

## 1.5 在单独的分区上设置 Linux 和 Windows 9x/9

### 1.5.1 使用 `LILO` 进行双启动

### 1.5.2 使用 `LILO` 启动

## 1.6 对现有硬盘进行分区

### 1.6.1 `fdisk`

### 1.6.2 调整分区大小

### 1.6.3 `NTFS`

### 1.6.4 `NTFS` 的限制

### 1.6.5 使用 `NTFS`

### 1.6.6 `NTFS` 的特殊情况

### 1.6.7 `NTFS` 分区

### 1.6.8 使用 Windows 加载程序

### 1.6.9 使用 `LILO`

# 第 2 章

在 WINDOWS 上访问 NTFS 分区

## 2.1 访问 DOS 和 Windows 分区

## 2.2 `NTFS`

### 2.2.1 `NTFS` 的图形化界面

## 2.3 访问 Windows 分区

# 在 LINUX 上挂载 WINDOWS 分区

## 3.1 挂载 Linux 驱动器

### 3.1.1 `NTFS` 的某些问题

## 3.2 向 `fstab` 添加分区

# WINDOWS 启动器

## 4.1 `DOS`

## 4.2 Windows

## 4.3 `VMware`

### 4.3.1 它是如何工作的？

### 4.3.2 `VMware` 的已知问题

### 4.3.3 调整 `VMware`

## 4.4 Freeware

## 4.5 Windows

## 4.6 结论

# 互联网应用

## 5.1 Web 服务器兼容性

### 5.1.1 `PHP`

### 5.1.2 活动服务器页面



# 目录

## 5.2 FrontPage 扩展 41
## 5.3 在 Web 上使用 Microsoft Office 41
## 5.4 浏览器 42
### 5.4.1 适用于 Linux 和 Windows 的浏览器 42
### 5.4.2 浏览器 42
### 5.4.3 将推出的浏览器 43
### 5.4.4 插件 43
## 5.5 电子邮件 44
### 5.5.1 客户端 44
### 5.5.2 服务器 45
## 5.6 媒体 46
### 5.6.1 视频 47
### 5.6.2 音频 48
## 5.7 聊天 50
## 5.8 即时消息 51
## 5.9 互联网安全 52

## 业务应用 57
### 6.1 Microsoft Office 57
### 6.2 Linux 核心 WordPerfect 57
#### 6.2.1 WordPerfect 59
### 6.3 其他生产力套件 59
#### 6.3.1 Star Office 60
#### 6.3.2 Appixware 60
### 6.4 开源办公套件 60
#### 6.4.1 Koffice 61
#### 6.4.2 Gnome Office 61
### 6.5 Web 端办公套件 61
### 6.6 读取和写入 Microsoft Office 文件 63
### 6.7 导出 MS Office 文件 64
### 6.8 在 Linux 上导入和导出 MS Office 文件 66
### 6.9 使用 Star Office 使用 MS Office 文档 66
### 6.10 导入和导出的注意事项 70
### 6.11 财务软件 72
### 6.12 图形软件 72
#### 6.12.1 图形转换 74
### 6.13 结语 75
### 6.14 结论 75

## 数据库 77
### 7.1 使用数据库 78
### 7.2 选择数据库 78
### 7.3 连接数据库 79
### 7.4 ODBC 79

## 娱乐与游戏 81
### 8.1 游戏 81
#### 8.1.1 Loki 81
#### 8.1.2 id Software 83
#### 8.1.3 Unreal Tournament 83
### 8.2 游戏服务器与额外功能 84
### 8.3 经典游戏 85

## LINUX 桌面 87
### 9.1 切换桌面 88
### 9.2 配置桌面 89
### 9.3 主题 90
### 9.4 结论 93

## 通过网络运行应用程序 95
### 10.1 X-Windows 95
#### 10.1.1 Linux 上的 X-Windows 95
#### 10.1.2 Microsoft Windows 上的 X-Windows 96
### 10.2 Citrix WinFrame 97



## 10.2.1 服务器概述

## 10.2.2 客户端配置

## 10.2.3 应用程序配置

## 10.2.4 费用

## 10.3 VNC

### 10.3.1 为 Linux 安装 VNC Server

### 10.3.2 在 Linux 上使用 VNC Viewer

### 10.3.3 为 Windows 安装 VNC Server

### 10.3.4 为 Windows 安装 VNC Viewer

### 10.3.5 Java VNC Viewer

### 10.3.6 优化 VNC

### 10.3.7 VNC 安全

## 10.4 结论

# WINDOWS 与 LINUX 网络简介

## 11.1 Net BIOS

## 11.2 TCP/IP 与活动目录 (Active Directory)

## 11.3 TCP/IP 之上的 Net BIOS

# SAMBA 简介

## 12.1 Samba 如何起步

## 12.2 Samba 如何工作

# 将 SAMBA 设置为 Windows NT 服务器

## 13.1 将 Samba 设置为独立的 Windows NT 文件服务器

### 13.1.1 设置 DHCP

## 13.2 向现有网络添加 Samba 服务器

## 13.3 Samba 作为域控制器

# LINUX 连接到 WINDOWS

## 14.1 命令行选项

## 14.2 Samba

### 14.3 Samba

### 14.4 Samba

### 14.5 Samba

### 14.6 结论

# 使用 SAMBA 打印

## 15.1 打印

## 15.2 测试打印机



## 15.3 设置 Samba 打印

## 15.4 自动驱动程序

# 在 LINUX 和 WINDOWS 中使用 NFS 和 NIS

## 16.1 将 Linux 设置为 NFS 服务器

## 16.2 在 Linux 上使用 NFS 客户端

### 16.2.1 优化 NFS

### 16.2.2 硬挂载与软挂载

## 16.3 在 Windows 上使用 NFS

### 16.3.1 在 Windows NT 上设置 NFS 服务器

### 16.3.2 设置 NFS 客户端

### 16.3.3 使用 Windows 连接到 NFS 服务器

### 16.3.4 NFS 网关

### 16.3.5 NFS 安全

## 16.4 在 Linux 上设置 NIS 服务器

## 16.5 在 Linux 上设置 NIS 客户端

## 16.6 Windows 的 NIS 支持

### 16.6.1 NISGina 的问题

### 16.6.2 NIS 安全

# 在 WINDOWS 中实现 FTP、TELNET 以及其他 UNIX 协议



### 17.1 为 Windows 设置 FTP 服务器 ........................................................................................................................................................ 176

### 17.2 为 Linux 设置 FTP ..................................................................................................... 177

### 17.3 Linux 的 telnet 和远程服务 ................................................................................ 178

### 17.4 安全外壳 `SSH` ....................................................................................................... 178

#### 17.4.1 什么是 `SSH`？ ................................................................................................. 178

#### 17.4.2 它能防护什么？ ................................................................................ 179

#### 17.4.3 `SSH` 无法防护什么 ................................................................... 179

#### 17.4.4 Windows 版 `SSH` 客户端 ................................................................................ 179

#### 17.4.5 为 Linux 安装 `SSH1` ...................................................................... 180

#### 17.4.6 为 Linux 设置 `SSH1` 服务 ................................................................ 180

#### 17.4.7 使用 `SSH` 客户端 ................................................................................ 180

#### 17.4.8 通过 `SSH` 运行其他服务 ....................................................................... 181

#### 17.4.9 管理 `SSH` ................................................................................................. 183

#### 17.4.10 `SSH` 故障排除 ................................................................................ 183

#### 17.4.11 `X11` 问题 ............................................................................................ 186

#### 17.4.12 查找 `SSH` 支持 ......................................................................... 186

磁盘错误代码 ................................................................................................ 187

# 附录 B

`SAMBA` 文档 ................................................................................ 189

`SAMBA` 手册 ............................................................... 229

`SAMBA` `TCP/IP` 文档 ................................................................ 345

索引 ................................................................................................................ 385

## 引言

在1998年初，我正考虑第三次安装 Windows 95。诚然，我比普通用户更关注电脑，但这种做法已经让我乏味了。我从1995年初就开始尝试摆弄 Linux，看起来现在是将其作为我的主要桌面系统的好时机。

我已经知道如何安装和配置 Linux，但我从未将其作为桌面系统使用。我发现了很多关于 Linux 配置的书，有几本关于将其作为服务器使用的，但没有关于将其作为桌面系统使用的。相反，我必须在互联网上搜索有用信息。我所尝试做的是把过去两年学到的内容汇总起来。希望这能为你们节省自己寻找信息的时间和挫败感。

那么，Linux 与 Windows相比如何？正如其他任何事物一样，每者都有自己的优缺点。

Windows 之称为桌面之王是有其原因的。它拥有精美的界面，并且比任何其他操作系统都有更多的终端用户应用程序。它还预装在大多数新 PC 上，这使其成为大多数 PC 来说是一个既简单又安全的选择。这些因素让 Windows 占据了约 90% 的桌面市场。

Linux 基于 UNIX，并继承了它的安全性和稳定性。Linux 是公共 Web 服务器最受欢迎的选择，它还占据了约 25% 的小型服务器市场。它也是免费的（或几乎免费），并带有一系列用于编程和服务器管理的实用工具。

然而，这些区别并不是永久的。有几个小组正在研究 Linux 的界面。目前正竞相为 Linux 开发更多的终端用户应用程序。戴尔（Dell）、康睿（Compaq）和 way（IBM）等大型电脑厂商开始提供预装 Linux 的 PC。

虽然 Linux 的市场相对较小，但 Linux 已从1998年占桌面市场的不到1%增长到1999年的约5%。Windows 2000 同样面临同样的问题。在这些领域，Linux 继承了 UNIX 的优势：安全性、稳定性和可扩展性。Windows 2000 为了解决这些问题，对分区进行了改进。Windows 2000 还支持运行多个操作系统。

## 在同一台 PC 上运行 Linux 和 Windows

### 1.1 分区

运行 Linux 无需抛弃 Windows。事实上，有许多方法可以在同一台 PC 上运行它们。每个操作系统都有自己的优缺点，因此经常将它们结合是一项优势。

在实际安装之前，我们需要了解 Linux 和 Windows 的基础知识，例如分区。大多数 PC 的硬盘只有一个分区。这并非不必如此。硬盘可以被分成几个分区。这样做通常是为了将程序与分离，也是为了在同一设备上存储多个操作系统。

硬盘的第一部分包含分区信息，包括每个分区的起始和结束位置。它还包含了加载器的位置，由加载器启动操作系统。每个操作系统都有自己的加载器。Windows 3x、95和98 使用 `IOS.SYS` 和 `DOS.SYS`，Windows NT 使用 `NTLOADER`，而 Linux 使用 `LILO`。还有一些商业和共享加载器（如 Norton System Commander），旨在方便启动多个配置和操作系统。

### 1.2 文件系统

Linux 和 Windows 还使用了几种不同的文件系统。文件系统只是在分区上组织文件的方法。Windows 使用 `FAT`、`FAT16`、`FAT32` (`VFAT`) 和 `NTFS` (文件系统)。Linux 的原生文件系统是 `ext2`，它支持许多其他文件系统。

`FAT` 是 DOS 使用的原始文件系统。它是一个字节文件系统，支持高达 32 MB 的分区。这在大多数 PC 还没有硬盘的20世纪80年代并不是问题。

`FAT` 支持文件属性：

- 只读——设置后，文件无法被删除或更改。许多备份程序都会使用此属性。
- 存档——确定文件是否被更改过。
- 隐藏—文件不会显示在目录内容中。
- 系统—用于系统文件。操作系统对系统文件会有特殊处理。



后来，随着硬盘的使用，FAT 的 32 MB 限制成了一个负担，改进后的 FAT16 将文件系统的可用容量增加到 2 GB。除了文件大小外，FAT16 本质上与原始 FAT 文件系统相同。FAT16 受 DOS 4.0 及更高版本、所有版本的 Windows 以及所有当前版本的 Linux 的支持。

随着 Windows 95 及其服务包 2 版本的发布，微软引入了 FAT32。这使得文件系统的容量增加到 2 TB，这比目前 PC 可用的任何硬盘都要大。它也比 FAT16 更快、更健壮。

NTFS 是 Windows NT 和 2000 的原生文件系统。与 FAT32 一样，它也支持 2 TB 的文件大小，但启动分区目前限制为 7.8 GB。对于数据库文件某些文件，NTFS 可以支持高达 16 EB（艾字节）。与 FAT 相比，NTFS 提供了更好的可靠性和安全性。

可靠性因素不在本书的讨论范围内，但需要涵盖 NTFS 的安全性考虑。首先，文件系统中的一切都有一个所有者。默认情况下，创建对象（文件系统中的任何内容都是对象）的用户是所有者。所有者对对象拥有完全权限，除非权限被剥夺。

此外还有组，组中包含用户。三个特殊的组账户是：管理员（administrator）、所有人（everyone）和访客（guest）。

- 管理员账户拥有文件系统的所有权限。此账户可以更改、创建和删除所有对象，还可以更改其他帐户的权限。
- 所有人包含系统上所有用户账户的组。此账户用于更改系统上每个用户的权限。
- 访客账户具有最小权限的默认账户。它通常用于 FTP 访问账户等，这些账户只需要访问少数特定文件。

NTFS 中的文件具有与 FAT 文件相同的属性：只读、隐藏、系统和归档。每个用户和组还可以被分配 NTFS 文件系统对象的对象的权限。可以分配的权限有：

- 列出文件夹—在目录列表中显示。
- 读取—可以读取对象的内容。
- 读取和执行—可以读取并执行对象。
- 写入—可以更改或删除对象。
- 修改—可以更改文件的权限。
- 完全控制—拥有上述所有权限。

权限有三种设置：允许、拒绝和继承。

- 允许—在对象上允许权限。
- 拒绝—剥夺对象的权限。
- 继承—如果既没有指定允许也没有指定拒绝，对象将继承其上级目录的权限。

### 1.3 分区命名

考虑 NTFS 上对象的权限，可以右键点击该对象并选择“属性”。然后选择“安全”选项卡。

Ext2 是 Linux 分区的原生文件系统。Ext 是 Linux 的原始文件系统，而 ext2 是它的改进版本。Linux 中的对象（如文件、目录和设备）支持这三个属性：读取、写入和执行。

- 读取—如果设置，则允许对象在目录列表中显示并被读取。
- 写入—如果设置，则允许对象被写入和删除。
- 执行—如果设置，则允许执行对象。这对于目录同样适用。

一个对象有三组权限：所有者、组和所有人。

- 所有者—创建文件的用户，除非被更改。
- 组—拥有该文件的组是所有者所属的组，除非被更改。
- 所有人—系统上所有其他用户的权限。

要查看对象的权限，输入 `ls -l <object name>`。例如，要查找 `index.txt` 的权限，输入 `ls -l index.txt`。

- `image`—这是内核。下方的参数是内核参数：
- `label`—显示在启动菜单上的标签名称。
- `root`—文件系统的位置。
- `read-only`—文件系统以只读模式挂载，以便进行 `fsck` 错误检查。随后，它会被重新挂载为读/写模式。

这些并不是 `lilo` 的全部参数。

LILO 在通过四个加载阶段时会依次加载 "LILO" 这四个字母。这对于排查故障非常有帮助。如果 LILO 在加载过程中停止，失败的位置会显示对应的字母的字母：

- `<nothing>`—LILO 的任何部分尚未加载。LILO 可能未安装，或者其引导扇所在的分区未激活。
- `L <error>...`—第一阶段引导程序已加载并启动，但它无法加载第二阶段引导程序。两位数字错误代码表示问题的类型（参见附录 A 中的“磁盘错误代码”章节）。此情况通常表示媒介故障或几何结构不匹配。
- `LI`—第一阶段引导程序能够加载第二阶段引导程序，但无法执行它。这可能是由几何结构不匹配或在未运行 map 安装程序的情况下移动了 `/boot/boot.b` 引起的。
- `TIL`—第二阶段引导程序已启动，但它无法从 map 文件加载描述表。这通常是由媒介故障或几何结构不匹配引起的。
- `LIF`—第二阶段引导程序加载到了错误的地址。这通常是由细微的几何结构不匹配或在未运行 map 安装程序的情况下移动了 `/boot/boot.b` 引起的。
- `LIM`—描述表损坏。这可能是由几何结构不匹配或在未运行 map 安装程序的情况下移动了 `/boot/map` 引起的。
- `LILO`—LILO 的所有部分都已成功加载。

如果 Linux 没有加载，它会给出错误代码。错误代码的含义列在附录 中。

Windows 的启动方式略有不同。分区指向引导扇，由引导扇加载两个文本文件 `config.sys` 和 `autoexec.bat`。它加载 Windows 版本的 Linux内核 `win.com`。`win.com` 的配置文件是注册表（Registry），它由两个二进制文件组成：`system.dat` 和 `user.sys`。虽然 `config.sys` 和 `autoexec.bat` 是文本文件，但注册表文件需要使用 `regedit` 编辑。

## Linux 和 Windows 95/98

有多种方法可以在同一机器上为 Windows 3x/9x 安装 Linux。它们列在下方，从 UmsDOS 开始。在进行任何操作之前，请备份您的硬盘，并在硬盘上运行 `scandisk` 以纠正任何错误。这将为您以后省去很多麻烦。

### 1.4.4 UMSDOS

在 Windows 9x 机器上安装 Linux 的简单方法是使用 UMSDOS，它允许 Linux 在 FAT 或 FAT32 分区上与 Windows 共存。它允许 Linux 直接从 FAT 分区的命令行提示符启动。优点是避免重新格式化硬盘或干扰现有的 Windows 安装；缺点是，你会失去 Linux 原生 ext2 文件系统的安全性和健壮性。

如果你计划使用 UMSDOS，最好选择带有自动 UMSDOS 安装的发行版。大多数现代发行版都有包含 UMSDOS 的 Phat Linux。这是一个巨大的下载包，除非你有连接和大量时间，否则你可能需要购买 CD-ROM。作为额外福利，购买时还可以获得技术支持。

Phat Linux 最初由两个高中生组合而成，他们想要一种简单的安装 Linux 的方法。要安装它，将文件解压到 `\\hat` 目录并运行 `linux.bat`。如果在启动过程中卡住，可能需要重启，在启动时按 F8 并选择安全模式提示。启动后，将有一个菜单，供你选择配置以设置视频、声音和网络。`linux.bat` 只有三行，如下：

```
loadlin vmlin initrd-ramdisk.gz mem=96M
echo Linux failed to load.
```

第一行实际上加载了 Phat Linux。命令分解如下：

- `loadlin`—这是 UMSDOS 的加载器。
- `vmlinuz`—这是 Linux 内核。
- `initrd`—指向内存镜像。Phat Linux 使用压缩的内存镜像来启动操作系统。
- `ramdisk.gz`—一个包含完整 Linux 文件系统的压缩文件。这也可以是一个目录。
- `Mem`—以兆字节为单位计算的内存量。

Phat Linux 基于 Red Hat 并带有 KDE 桌面，因此任何熟悉 Red Hat 的人应该都能使用 Phat Linux。

UMSDOS 可以很容易地手动安装，因为长期以来它一直内置在 Linux 内核中。大多数发行版会为你设置好一切，但了解它的工作原理有助于排查故障。

安装 UMSDOS 的默认目录是 `\\linux`。它充当 Linux 的根目录。下面是标准的 Linux 目录：`bin`、`etc`、`lib`、`root`、`sbin`、`tmp`、`usr` 和 `var`。

然后是交换空间（swap space）的问题。通常情况下，Linux 会创建一个单独分区。这种方法的优点是速度快且健壮性好。然而，使用 UMSDOS，可以使用交换文件。

### 1.4.5 使用 LILO 启动

在单独分区上安装 Linux 的简单方法是将其加载到不同的驱动器上。如果我在第一个 IDE 端口上有一个主 IDE 驱动器，上面有 Windows 98 (`hda`)，我将第二个 IDE 端口设置为 Linux 的主驱动器，那么它就是 `hdb`。在安装期间，我只需将 Linux 分区和交换驱动器安装到 `hdc` 上。我剩下的唯一选择就是使用 LILO 或 `loadlin` 启动。

除非使用 `umsync`，否则 DOS 创建的文件对 Linux 来说是不可见的。如果你尝试在 Linux 中创建一个与 DOS 文件同名的文件，它会告诉你该文件已存在。除此之外之外，在同一分区上运行 DOS 和 UMSDOS 没有问题。你可以在分区上使用 DOS 磁盘整理工具，而不影响 UMSDOS 文件系统。



要使用 Linux，请将 `LILO` 安装到 `hda`。安装程序通常会询问你将 `LILO` 安装在哪里。你需要检查安装 `LILO` 的配置说明，它会随不同的安装程序而异。

接下来，你需要编辑 `/etc/linux.conf`。它看起来像这样：

```
boot=/dev/hdc
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
image=/boot/mlinux-2.2.13-mdk
label=linux
root=/dev/hdc5
readonly
```

将此内容添加到 `lilo.conf` 的末尾：

```
other=/dev/hdal
table=/dev/hda
label=Windows98
```

这将让你在启动时可以在“linux”或“Windows98”之间进行选择。

当然，`loadlin` 也可以用于从第二个驱动器加载 Linux。首先，将 `loadlin` 和 `vmlin` 放入你的 Windows 分区。启动期间，按下 `F8` 并选择“安全模式命令提示符”。在示例中，我们将在 `C` 盘根目录下带有以下参数运行 `loadlin`：

```
loadlin vmlin root=/dev/hdc5 ro
```

这将加载内核 `vmlinuz`，将 Linux 根目录设置为位于第二个 IDE 端口主驱动器上的 5 号分区（`hdc5`），并将根目录设置为只读（`ro`）。请更改这些设置以匹配安装该 Linux 的驱动器。

虽然在独立的分区上加载 Linux 的最佳方法是将其加载到独立的硬盘上，但并不是每个人都有多个硬盘。虽然现在硬盘的价格大约为 100 美元，这已不再是问题，但如果你必须这样做，请将 Linux 加载到与 Windows 在同一块硬盘的独立分区上。有几个程序可以让你操纵分区。如果你在硬盘上有 200–120 MB 的可用空间，可以从空闲空间创建一个 Linux 分区。

在操作分区之前要做的第一件事是备份你的硬盘。接下来，在驱动器上运行深度模式 `scandisk`，以确保没有可能导致问题的错误。使用 Windows 碎片整理对硬盘进行碎片整理。这将将所有文件移动到硬盘开头，并为硬盘末尾的新分区留出空间。

在我们重新格式化硬盘之前，请记住，两个操作系统的引导程序必须位于硬盘的前 1024 个磁道内。在大多数硬盘上，这位于前 504 MB 范围内。这是 PC 硬件的限制，可以追溯到硬盘最大容量为 504 MB 的时代。

一旦备份并检查了硬盘，我们需要决定如何对硬盘进行分区：硬方法或易方法。让我们从硬方法开始。

![](img/a1ad58e4259f15e8b2826ecf57a28362_26_0.png)

随着硬盘的使用，文件会散布在整个硬盘上（碎片）。深色区域代表文件，浅色区域代表空闲。

![](img/a1ad58e4259f15e8b2826ecf57a28362_26_1.png)

碎片整理会将所有文件移动到硬盘开头。这使得硬盘末尾留出空闲。

![](img/a1ad58e4259f15e8b2826ecf57a28362_26_2.png)

然后我们可以在硬盘末尾创建一个分区并在该分区上安装 Linux。

## 1.6.1 fdisk

一旦你备份了所有数据（这将破坏硬盘上的所有数据），你就可以使用 `fdisk` 重新划分硬盘分区。首先，以安全模式启动到 DOS。然后运行 `windowsfdisk`。选择“删除分区”（Delete Partition）。然后选择“扩展”（Extended）。紧接着删除主分区。

一旦你创建了 DOS 分区，就在上面安装 Windows 和你所有的应用程序。然后恢复你的数据。这是一项大量的工作，可能需要花费几个小时。有一种更简单的方法。

有几个程序可以调整分区大小。`Partition Magic` 是一个商业程序，具有良好的图形化界面，并支持所有 PC 分区。它物有所值。你可以在 http://www.powerquest.com 获取 `Partition Magic`。

许多 Linux 安装程序允许在安装期间对硬盘进行重新分区。相关说明应该包含在你的发行版文档中。如果你的发行版不支持此，你可以使用 `FIPS` 手动进行。

与其他许多程序相比，`FIPS` 的命令行开关很少。现有的开关列如下：

- `-t` 或 `--test`——这不会向磁盘写入任何内容。
- `-d` 或 `--debug`——这将把错误写入 `FIPSINFO.DBG` 文件。它可以帮助诊断问题。
- `-h` 或 `--help` 或 `?`——帮助文本。
- `-n<num>`——要进行分割的驱动器编号。

## 1.6.4 FIPS 的限制

使用 `FIPS` 时的操作有一些限制。首先，你的硬盘必须支持用于低级磁盘访问的 `INT 13`。少数旧的 Adaptec 驱动器控制器不支持 `INT 13`，但几乎所有其他驱动器都支持，包括新的 Adaptec 驱动器。

`FIPS` 也不支持 `FAT12`。`FAT12` 用于小于 10 MB 的分区。除非分割一个 10 MB 的分区本身没有意义，否则这不会引起任何问题。

你只能分割标准的 `FAT` 和 `FAT32` 分区。`FIPS` 不工作于扩展分区、`NTFS`、`HPFS` (Os2 文件系统)、`Linux` 或任何其他非 `FAT` 分区。

由于 `FIPS` 无法在某些格式上工作，你必须确保分区格式符合要求。

Windows 3.1。如果你正在使用 Windows 3.1，必须在分割分区之前删除交换文件。要执行此操作，请进入控制面板（在“主”文件夹中）并选择“386增强型”。然后选择“虚拟内存”，并更改为“无”。分区完成后，你可以重新开启交换文件。

Stacker、SuperStor、DoubleSpace 以及其他磁盘压缩程序。这些程序会在任何带有压缩文件的磁盘上创建一个压缩卷。然后，它们会将所有文件移动到压缩卷并重命名卷。未压缩的卷通常是 `C:`，它包含启动文件和压缩程序。未压缩的卷是 `D:`，它包含压缩文件。

分割此驱动器可能会很复杂。如果压缩文件损坏，整个驱动器将无法访问，请务必做好良好的备份。以下步骤允许你向压缩驱动器添加一个新分区：

1. 确保在压缩驱动器上有足够的可用空间来创建新分区。
2. 使用驱动器自带的磁盘检查软件检查错误。
3. 如果你正在运行 Windows 3.1，请移除交换文件。
4. 使用磁盘压缩工具减小压缩卷的大小。
5. 对压缩卷 (`D`) 进行碎片整理。
6. 使用 `FIPS` 分割压缩卷 (`D`)：

如果无法对压缩卷，请尝试以下步骤：

1. 将你的磁盘碎片工具（例如 `defrag.exe` 或 `xorg.exe`）和 `attrib.exe`（位于 `C:\DOS`）拷贝到可启动软盘。
2. 使用软盘启动，并移除压缩驱动器 (`D`) 上文件的所有隐藏和系统属性。使用 `dir /a:h` 和 `dir/a:s` 来查找隐藏和系统文件。
3. 对压缩分区 (`D`) 进行碎片整理：

完成后，你应该能够分割驱动器了。

在操作 `NTFS` 分区之前，制作一个救援磁盘，将重要信息保存到软盘中，以便在出现问题时恢复。对于 Windows NT，使用“开始 -> 输入“rdisk”，并选择“创建紧急修复磁盘”。对于 Windows 2000，进入“开始 -> 系统工具 -> 备份”。在“欢迎”选项卡上有一个“紧急修复磁盘”按钮。按照说明操作。

# 第 1 章 • 在同一磁盘上运行 Linux 和 Windows

Windows NT 和 2000 不使用 `fdisk`。它们有自己名为“磁盘管理器”的分区程序。在安装期间，系统会询问如何创建分区。默认情况下，分区将是整个驱动器。NT 分区的启动分区限制为 4GB，所有分区限制为 7.5GB。Windows 2000 没有此限制。

如果 Linux 和 NT 位于不同的驱动器上，你可以使用 `LILO`。请查看下方标题为“使用 LILO”的章节。

在我们开始创建 `NTFS` 分区之前，我们需要下载由 G. Volant 开发的 `BootPart`。该程序可以创建和操作 `NTFS` 引导扇。访问 http://www.winimage.com/bootpart.htm。

Windows NT 的过程与 Windows 3x/9x 不同。我们需要关注的主要区别是 Windows NT 使用文件而不是分区的引导记录来加载操作系统。这意味着，如果我们想使用 Windows NT 的引导程序进行加载，就必须为 Linux 创建一个引导文件。

要创建 Linux 引导文件，我们需要将 Linux 分区的扇区拷贝到文件中。要执行此操作，请使用 Linux 救援软盘并使用 `dd` 将引导扇拷贝到文件中。如果你没有救援软盘，可以在 Windows 中运行 `rewrite.exe` 程序来创建一个，该程序可以在 Linux 安装光盘的 `\dosutils` 目录中找到。程序打开后，选择“写入（Write）”选项，然后选择 Linux 安装光盘中 `\images` 目录下的 `rescue.img` 文件（图 1.3）。

![](img/a1ad58e4259f15e8b2826ecf57a28362_31_0.png)



图 1.3 在你的 Linux 安装光盘上使用 RawWrite 将救援镜像拷贝到 A: 盘。

从救援软盘启动，并将启动分区拷贝到软盘，格式为：

`diff=<Linux partition> of=<name of file> bs=512 count=1`

让我们逐步检查命令：

- `if`—开始拷贝的位置。在这种情况下，我们从 Linux 分区的开始处。
- `of`—输出文件的文件名。
- `bs`—块大小。引导扇区为 512 字节。
- `count`—块的数量。

## 在 Windows 中访问 ext2 分区

有两种工具可以通过 DOS 访问 ext2（Linux Native）文件系统。一个是 ext2 tools，它提供只读访问，可以在这里：`ftp://sunsite.unc.edu/pub/Linux/system/filesystems/ext2/`。还有 `ltools`，它提供了对 ext2 分区的读写访问。

`ltools` 提供了命令行工具、一个可以通过浏览器访问的 Web 服务器以及一个 Java 工具。命令行工具模拟了许多 DOS 实用程序的功能，可以在 DOS 和所有版本的 Windows (`3x`, `9x` 和 `NT`) 中运行。它们应该也能兼容 Windows-2000，尽管尚未对其进行过广泛测试。

> 使用 `ltools` 向 ext2 文件系统写入数据时会出现一些异常行为。任何写入操作都会将文件系统设置为“干净（clean）”。这会导致问题，除非在下次系统启动时运行 `fsck`（Linux 的磁盘检查工具）。

此外，在 Windows 9x DOS 框中运行 `ltools` 时，硬盘在使用期间会被锁定。这要求你的系统中有一张软盘，即使不使用它。软盘驱动器会旋转，但对其不会进行任何更改。

`ltools` 使用 Linux 风格的正斜杠（`/`）表示目录和 DOS 风格的驱动器。对于 `/root` 目录下的所有文件，表示为 `/root/*`

`ltools` 包含以下程序：

- `ldir [-h -v | ? [-part]] [-s/dev/hd..] [Linux_Directory]`—功能类似于 DOS 或 Linux 中的 `dir` 命令。切换开关的含义如下：
  - `-h?`—帮助屏幕。
  - `-v`—版本信息。
  - `-s`—驱动器名称，例如 `/dev/hda1` 等。
  - `-part`—列出驱动器上的所有分区。
  - `Linux_Directory`—ext2 文件系统上的目录。默认是 `/`。

- `lread [-h |-v |?] [-s/dev/hd..] Linux_File [DOS_File]`—列出或复制文件。工作类似于 DOS 中的 `type` 或 `copy`。切换开关用于表示：
  - `-h?`—帮助屏幕。
  - `-v?`—版本信息。
  - `-s?`—Linux 驱动器名称，例如 `/dev/hd1` 等。
  - `Linux_File`—要查看或复制的 Linux 文件。
  - `DOS_File`—要复制的 DOS 文件。必须是有效的 DOS 文件名。Windows 9x 支持长文件名。

- `ldrive /dev/hd..`—设置默认的 Linux 分区。如果命令中没有给出分区，将默认使用此分区。例如，要将默认分区设置为 `hda1`，命令为 `ldrive /dev/hd1`。

- `lcd directory`—设置 Linux 分区的默认目录。否则将使用系统默认值。例如，要将默认目录设置为 `/root`，命令为 `lcd /root/`。

- `ldel [-h |-v |?] [-s/dev/hd..] Linux_File`—使用以下开关删除文件、目录或链接：
  - `-h?`—帮助。
  - `-v?`—版本。
  - `-s?`—Linux 分区。

- `lchange [-h |-v |?] [-s/dev/hd..] [-fMODE] [-uUID] [-gGID] Linux_File`—
  - `-h?`—帮助。
  - `-v?`—版本。
  - `-s?`—Linux 分区。
  - `-f?`—更改 Linux 文件的属性，类似于 `chmod`。使用八进制数字。请查看你的 `chmod` 手册。
  - `-u?`—更改用户 ID。查看你的 `chown` 手册。
  - `-g?`—更改组 ID。查看你的 `chown` 手册。

- `lwrite [-fMODE] [-uUID] [-gGID] DOS_Path_DOS_File_Linux_File`—复制文件。开关与 `lchange` 相同。

- `ren [-h |-v |?] [-s/dev/hd..] [-fMODE] [-uUID] [-gGID] Linux_File_old_name Linux_File_new_name`—重命名文件、目录或符号链接。开关与 `lchange` 相同。

- `lmdir [-h |-v |?] [-s/dev/hd..] [-fMODE] [-gGID] new_Linux_directory`—创建 Linux 目录。开关与 `lchange` 相同。

- `ln [-h |-v |?] [-s/dev/hd..] [-fMODE] [-gGID] LinkTarget`—创建符号链接。符号链接类似于 Windows 中的快捷方式。开关与 `lchange` 相同。

### 2.3 使用 Windows 9x 访问 ext2 分区

### 2.2 ltools 的图形界面

`ltools` 带有两个图形界面：`LREADsrv` 和 `LREADgui`。如果你需要 Windows 9x、NT 或 2000 的图形界面，有更好的工具可用。`LREADsrv` 是 `ltools` 的一部分，让你能使用浏览器读写 ext2 分区。它还需要一些 `.GIF` 和 `.HTML` 文件。当 `ltools` 提取时，会将 `/bin` 目录下的所有必要文件使命令行工具正常工作。如果你的 PC 上已经有一个 Web 服务器，就不需要加载 `LREADsrv`。你可以通过输入主机名或 IP 地址访问远程驱动器。`LREADsrv` 仍有许多 Bug：

1. 它不是多用户程序。多个用户会导致文件或目录损坏！
2. 它的错误检查功能很弱。错误通常出现在浏览器窗口中。`LREADgui` 需要较快的机器来操作（慢速会被认为很慢！）。在列出目录时屏幕可能会闪烁。这些问题更多与 `LREADgui` 本身有关。

`FSDEXT` 允许从 Windows 只读访问 ext2 分区。它不再活跃开发，但可以工作，可以在 `http://www.linux.uk/` 获取。对于读写访问，请检查 `Explore2fs`。它看起来像 Windows Explorer，并兼容 Windows 9x 和 NT。`Explore2fs` 支持广泛的功能，包括：

- 拖放。
- 支持所有块大小。
- 支持软盘（1.44MB 和 1.2MB）。
- 支持 Jaz 驱动器。
- 支持 Windows 98 扩展分区。
- 快速写入支持。很快，如果比读取快。
- 导出文件。
- 导出为文本。
- 导出目录。
- 执行文件。
- 查看符号链接。
- 导入文件。
- 导入目录。
- 新文件的 Umask。
- 删除文件。
- 删除目录。
- 创建目录。
- 重命名。
- 修改文件模式（通过属性框）。
- 更改 uid 和 gid。
- 创建设备节点。
- 创建符号链接。
- 支持硬盘。

未来版本将添加的功能：

- 格式化文件系统。
- 导入 `.tgz` 文件。这是 UNIX 的原生压缩格式，Windows 使用 ZIP。
- 语言支持。

当 `Explore2fs` 首次启动时，处于只读模式。要启用写入支持，转到 `View -> Options`，然后选择 Debug 标签页。有一个复选框启用写入支持。重启程序以启用写入支持。

`Explore2fs` 只显示 ext2 分区。要操作 ext2 分区上的文件，请右键点击文件。这将弹出一个包含以下项的菜单：

- Properties
- Export File
- Export as Text
- Rename
- Import File
- Create

要安装 Ext2fsnt，

接下来，合并 `ext2.reg`。要执行此操作，转到开始->运行并输入 `regedit`。然后选择注册表并 导入注册表文件。找到 `ext2.reg` 文件。

重启计算机以激活驱动程序。编辑 `go.cmd` 以添加你的 ext2 分区，然后运行 `go.cmd`。

在 Windows NT 系统上，你可以将 `%systemroot%\system32\drivers\rs_rec.sys` 文件替换为 Ext2fsnt 自带的版本，而无需运行 `go.cmd`。不要在 Windows 2000 系统上替换此驱动程序！该驱动程序在 Windows 2000 上不支持完全支持。

安装后，将 ext2 分区设置为 Windows 驱动器。对于 Windows NT，将它们添加到注册表中。例如，要将第一个硬盘上的第二个分区设置为 E:，请在注册表中添加以下行：

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SessionManager\DOS Devices]
"E":"\\\\Harddisk0\\\\\Partition2"
```



对于 Windows 2000，只需使用磁盘管理工具分配驱动器号。

幸运的是，Linux 内核支持大多数 Windows 文件系统。可以使用 `mount` 命令来挂载分区：

```
mount [options] device directory
```

例如，将第一个驱动器上的第一个分区挂载到目录 `/mnt/drivec` 中：

```
mount /dev/hda1 /mnt/drivec
```

现在，更改目录到 `/mnt/drivec` 将显示第一个分区的内容，这在 Windows 中将是 C: 盘。

`mount` 命令通常会检测分区上的文件系统类型。如果没有，请使用 `-t` 选项指定文件系统类型。支持的 Windows 文件系统有：

- `iso9600`—标准 CD-ROM。较新的内核支持 Rock Ridge 扩展和 Joliet 驱动器（Windows 9x CD-ROM 使用）。

- `Mdos`—FAT16 和 FAT12。

- `Nfs`—NTFS。

- `Umsdos`—FAT 分区上的 UMSDOS 分区。

- `Vfat`—FAT32。

例如，加载一个 NTFS 分区：

```
mount -t ntfs /dev/hda1 /mnt/drivec
```

需要注意：NTFS 驱动程序是读写模式，但使用写入模式时请自担风险！

如果你的内核不支持这些文件系统，有针对不同文件系统的内核补丁，包括 UDF 文件系统。UDF 文件系统用于 DVD CD-ROM 以及一些 CD-R 和 CD-RW 驱动器。遗憾的是，目前 Linux 的 UDF 模块是只读的。

向内核添加新文件系统需要重新编译你的内核。如果用户手册中未涵盖，可以在 http://www.linuxdoc.org/HOWTO/Kernel-HOWTO.html 查看编译内核的说明。

各种文件系统的内核补丁为：

- FAT32—http://www-plateau.cs.berkeley.edu/people/chaffee/fat32.html。

# 第 3 章 · 使用 Linux 挂载 Windows 分区

- Joliet CD-ROM—http://bmrc.berkeley.edu/people/chaffee/joliet.html。

- NTFS—http://www.informatik.hu-berlin.de/~loewis/ntfs/

- UDF—http://trylinuxux.com/projects/udf/

### 3.1 使用 Linux 访问压缩的 DOS/Windows 驱动器

与其他驱动器不同，大多数内核内置对压缩驱动器的支持。有两个程序允许访问压缩的 DOS/Windows 驱动器：`thfs` 和 `DMSOS`。`thfs` 为 Double Space 和 Drive Space（微软的磁盘压缩程序）提供只读支持。`thfs` 可以在 http://ftp.ftp-ai-lab.fr-fwurtangen.de/pub/os/linux/thfs.tz 获得。

另一个程序 `DMSOS` 使用回环设备（`loopback device`）来读取和访问压缩的驱动器。它支持 Double Space、Drive Space 以及 Stacker（一种第三方压缩程序）。与其他文件系统一样，它是一个内核补丁，可以在此处获取：http://fb9nt.uni-duisburg.de/mitarbeiter/gockel/software/dmsos/。

将 `DMSOS` 添加到内核后，压缩驱动器可以像添加了回环的普通 FAT 分区一样加载。例如，加载驱动器上第一个分区的压缩 FAT16 驱动器，输入：

```
/dev/hd1 /DOS mount -t dmsos -o loop /dbspace.001 /mnt
```

分区挂载在 `/DOS`，压缩文件系统 (`cvf`) 挂载在 `/mnt`。`cvf` 用于挂载压缩数据，`DOS` 用于解压数据。

`DMSOS` 应该检测驱动器的压缩类型，但如果挂载驱动器出现问题，可以使用某些选项。`DMSOS` 选项使用以下格式：

```
DMSOS -t <partition type> -o cvf_options=option1+option2...
```

`DMSOS` 有五种选项类型。`DMSOS` 文档列出了每个选项的所有值：

- `comp:xxx`—这指定压缩类型。由于 `DMSOS` 会自动检测压缩类型，因此这很少用。

- `cf:xxx`—这是一个从 1 到 12 的整数。1 最快，但压缩率最低；12 最慢，但压缩率最高。

- `bitferers:xxx`—这是在压缩分区上发现错误时要执行的操作。默认是将分区设置为只读。

- `loglevel:xxx`—这会创建一个对故障排除有用的日志文件。查看源代码中的 `dmsos.h` 以获取任何级别的选项。

- `speedup:xxx`—除非你清楚自己在做什么，否则不应使用此项。它设置访问驱动器的方式。设置过低会导致 `DMSOS` 非常慢，设置过高可能会损坏驱动器。

#### 3.1.1 DMSDOS 的一些问题

当然，由于涉及压缩和解压缩，访问压缩分区比访问未压缩分区慢。通过对压缩分区进行碎片整理可以将其降最低。Double Space、Drive Space 和 Stacker 带有碎片整理工具，应该定期使用。

配合 `DMSDOS` 使用 `DOSEMu` 也会导致问题。DOS 经常直接写入磁盘并绕过 `DMSDOS` 文件缓存。你可能需要卸载压缩分区来使用 `DOSEMu` 以避免损坏分区或系统崩溃。`DMSDOS` 文档包含了大量的错误代码。

`/etc/fstab` 文件是一个存储可挂载驱动器信息的文件。向该文件添加条目可以避免每次挂载分区时输入命令。一个典型的 `fstab` 文件看起来如下：

```
/dev/hdl /boot ext2 defaults 1 2
/dev/hda5 ext2 defaults 1 1
/dev/hd6 swap upgrade 0 0
/mnt/floppy /mnt/floppy supermount fs=vfat,dev=/fd0 0
/mnt/cdrom /mnt/cdrom supermount fs=iso9660,dev=/cdrom 0
```

该条目分为六部分，用空格分隔：

- 1. 挂载设备。

- 2. 挂载点。

- 3. 文件系统类型。

- 4. 挂载选项。

- 5. 需要 `dump` 的文件系统。

- 6. `fsck`。

向 `fstab` 添加驱动器是有点复杂的，因为其中一些设置可能有所不同。

（注：原文后续存在大量重复内容，已根据要求不进行重复输出）

## 4.2 Windows

`Wabi` 是一个商业程序，允许 Windows 3x 应用程序在 X-Windows 内部运行。它适用于许多商业版本的 UNIX 以及 Linux。好消息是，它运行 Windows 3.1 程序的效果非常好。坏消息是，它目前没有在 Linux 平台上进行开发或支持。Caldera 有关于 `Wabi` 的详尽文档：http://www.caldera.com/support/wabil。

`TWIN` 是一个 GNU 项目，其目标是编写 UNIX 库来仿真 Windows 32 位 API（应用程序接口）。它的两个目标是：让 Windows 能够在 UNIX（以及 Linux）上编译，以及让 Intel 版本的 UNIX 能够运行 Windows 程序。它的库支持 HPUX、AIX、Solaris 以及 Linux。尽管它最初是一个独立的项目，但 `TWIN` 项目已与 `WINE`（Wine Is Not an Emulator，Wine 不是模拟器）项目合并。有关 `TWIN` 项目的更多信息，请访问 http://www.linux.com。

其目标是让 Windows 能够在 Intel 版本的 UNIX 上原生运行。从技术上来说，`WINE` 并不是模拟器，因为它为在 Linux 上运行的 Windows 程序提供了低兼容性，这使其比使用模拟器具有显著优势。

`WINE` 目前可在 Linux、FreeBSD 和 Solaris 下运行，并包含在绝大多数当前的 Linux 发行版中。如果你没有 `WINE` 副本，可以在 http://www.wineq.com 获取源码或 RPM 包。

安装完 `WINE` 后，你必须配置 `wine.conf` 文件。其格式与 Windows 的 `.ini` 文件相同。配置的详情请参见附录 A。配置好 `WINE` 后，你就可以安装 Windows 程序。启动 X-Windows 并打开终端。要安装 Windows 程序，输入 `wine <Windows 安装程序>`。程序安装完成后，你可以通过输入 `wine <Windows 可执行文件>` 从终端窗口运行它。



WINE 目前处于开发阶段，并且在运行 Windows 程序方面已取得成功。大多数 Windows 3x 程序都能在没有问题的情况下下运行，但 Win32 程序（Windows 9x 和 NT 程序）的效果参差不齐。例如，据报道 Microsoft PowerPoint 2000 在 WINE 下运行得完美，但 Microsoft Outlook 完全无法工作。要获取最新的兼容 Windows 程序的程序列表，请访问 http://www.wineq.com/apps/query.cgi。

Linux 的 Windows 仿真器还不能用于生产环境，尽管它们正在迅速改进。请关注 Wine。Core 一直支持 WINE 项目，并正在开发允许 Windows 应用程序在 Windows 上运行得更好的库。Core 目前正在使用 WINE 将其 WordPerfect 办公件移植到 Linux。按照目前的开发速度，它最终将足以在没有问题的情况下运行大多数 Windows 程序。

## VMware

VMware 是一个允许 PC 在另一个操作系统内部运行另一个操作系统的程序。它目前可在 Windows NT、Windows 2000 和 Linux 下运行。这不是仿真，而是另一个操作系统的真实会话。操作系统（客户 OS）作为主操作系统（主机 OS）内部的一个独立会话运行。

启动 VMware 时，它会打开一个带有启动界面的窗口。它看起来像 PC 启动一样，带有 BIOS 设置（见图 4.1）。然后它会进入客户操作系统的运行会话（见图 4.2）。这是通过 VMware 虚拟平台实现的，它在主机操作系统内部仿真了 PC 的 BIOS。这种仿真允许在该虚拟平台之上安装任何 PC 操作系统。如果你在安装过程中遇到问题，请查看“VMware 已知问题”章节。

VMware 的 Linux 和 Windows 版本均易于安装。完整的安装说明可在 http://www.vmware.com/support/doc/（Linux）和 http://www.vmware.com/support/win/doc/（Windows）获取。

![](img/a1ad58e4259f15e8b2826ecf57a28362_46_0.png)

![](img/a1ad58e4259f15e8b2826ecf57a28362_46_0.png)

![](img/a1ad58e4259f15e8b2826ecf57a28362_50_0.png)

图 4.3 进入全局偏好界面。

你可以通过按下 `<CTRL>--ALT-<ESC>` 从全屏切换回窗口模式。但是，如果你正在使用 Direct Draw 模式，切换时光标可能会变成一个黑色方块。如果这是一个问题，你可以通过全局偏好中的“显示（Display）”选项卡切换回 GDI 模式（见图 4.4）。

# 第 4 章 • 模拟器

![](img/a1ad58e4259f15e8b2826ecf57a28362_51_0.png)

**图 4.4** 在全局偏好界面中将图形（Graphics）选项设置为 Direct Draw。

你还可以通过“优先级（Priority）”选项卡调整客操作系统的优先级（见图 4.5）。如果客操作系统使用了过多资源，可以降低优先级；也可以提高优先级以提高客操作系统的响应速度。

## VMware

![](img/a1ad58e4259f15e8b2826ecf57a28362_52_0.png)

**图 4.5** 在全局偏好中调整客操作系统的优先级。

另一个需要注意的是：如果你在 VMware 中运行 DOS 会话，即使它处于空闲状态也会占用 CPU 周期。可以通过安装 Cpuid 程序来解决，该程序可以在 http://www.bugcomputer.com/cpuidle/ 下载。请按照随附说明进行安装，不要使用 `--cpu` 选项。启用此选项可能会在某些系统上引起问题。

此外，确保在客操作系统和主机操作系统中都禁用 CD-ROM 自动播放。自动播放会不断扫描 CD 驱动器以自动播放文件，这会严重降低性能。

## FreeMW

FreeMW 是一个允许在 Linux 中打开 Windows 窗口的开源项目。虽然它目前处于早期测试阶段，但它承诺提供 VMware 的开源替代方案。它还根据 LGPL（较小的 GNU 公共许可证）授权。LGPL 和 GPL 之间的主要区别是 LGPL 对再分发的限制较少。有关 LGPL 的更多信息，请访问 http://www.gnu.org/copyleft/lesser.htm。有关 FreeMW 的更多信息，请访问 http://www.freeware.org。

## Win4Lin

Win4Lin 是“新秀”。它允许 Linux 用户在 Linux 中运行 Windows 会话，但反之不行。它比 VMware 更快，内存内存更少（只需 32 MB 内存即可轻松运行），而且售价约为 40 美元。

我有机会尝试过它的早期版本，它看起来更快，但没有 VMware 那么稳定。为它辩护，我查看的是一个测试版本，这些 应该随着时间的推移而解决。

## 结论

目前，在 Intel Linux 平台上运行 Windows 程序的最佳方法是使用 VMware。大多数 Windows 程序都能在 VMware 上无问题运行。缺点是它是闭源商业软件。它还需要你购买一份 Windows 拷贝版来运行 Windows 程序。不过，由于大多数电脑都捆带了 Windows，这可能不是一个问题。

FreeMW 是一个很有前景的开源项目，但目前开发程度尚不足以供正常使用。

WINE 项目目前只能运行有限的 Windows 程序。然而，它是免费开源的（遵循 GPL），并且进展迅速。

# 第 5 章

## 互联网应用程序

互联网已经从 20 世纪 60 年代后期政府机构的通信网络发展为 20 世纪 90 年代后期驱动美国经济的引擎。Linux 和 Windows 的不同优势使得混合环境不仅可行，而且非常有吸引力。

## FrontPage 扩展

FrontPage 是一款流行的微软网页制作工具。在网页上需要 FrontPage 扩展才能利用 FrontPage 的功能，例如：

- 允许多个用户在同一个网站和 Web 服务器上进行协作（多用户制作）。
- 允许用户通过互联网从世界上任何地方使用 PC 或笔记本电脑通过 Microsoft FrontPage 直接写入 Web 服务器（远程制作）。
- 允许用户在其网站上使用表单，并指定表单结果的处理方式，而无需用户编写自己的脚本。
- 允许用户在其网站上包含讨论组。
- 允许用户在其网站上包含访问计数器。

当然，所有这些功能可以在没有 FrontPage 扩展的情况下完成。

只有在 Microsoft FrontPage 中利用这些功能才需要 FrontPage 扩展。

微软的 IIS 会自动安装 FrontPage 扩展。Apache 不包含 FrontPage 扩展，但可以 http://www.rtr.com/fpsupdownload.html 下载。在 Linux 的 Apache 上安装 FrontPage 扩展的说明请参见 http://www.e-gineer.com/instructions/install-frontpage-extensions-for-apache-on-linux.phtml。

## 在 Web 上使用 Microsoft Office 文件

Microsoft Office 程序经常用于创建网页文档。所有的标准 Office 程序（Word、Excel 和 PowerPoint）都有“另存为 HTML”选项。这对于快速创建 HTML 文档非常方便，但 Office 倾向于在 HTML 中放入非标准字符。这些文档在非微软浏览器查看时效果很差。

用 Office 创建的 HTML 文档具有以下非标准之处：

- 数字字符末缺少分号（例如 &#061;&#061;）。
- 特殊字符的数字渲染（例如 &lt; &gt; &amp;）。
- 包含非字母数字字符的未引号 `<table>` 标签。
- PowerPoint 错误地嵌套了 `<font>` 和 `<strong>` 标签。
- PowerPoint 使用 `<ul>` 和 `</ul>` 标签来完成段落换行。
- Office 在纯文本行中缺少了 `<tr>` 标签。
- Office 在标题中放置了额外的 `<p>` 标签。
- Office 使用“段落行”，导致行溢页面。



幸运的是，有一个名为 `demoroniser` (http://www.fourmilab.ch/webtools/demoroniser/) 的程序，它可以纠正用 Office 创建的 HTML 文档中的这些缺陷。它是一个免费 Perl 脚本，可以将非标准字符转换为标准的 HTML 标签。大多数 Linux 发行版默认安装了 Perl。Win32 版本的 Perl 可在 (http://www.ActiveState.com/ActivePerl/download.htm) 获取。如果你有 Windows 95，你还需要 DCOM (http://www.microsoft.com/resources/downloads.asp)。

`demoroniser` 的语法为 `[ -u ] [- wcols ] [ infile ] [ outfile ]`

其中：
- `-u`: 帮助。
- `-w`: 设置行长度。默认值为 72。

## Web 浏览器

Web 的优势之一是网页告诉浏览器页面应该什么样，而浏览器实际上渲染网页。这意味着网页下载速度快，并且每个操作系统都有 Web 浏览器可用。这意味着浏览选择对网页外观有很大影响，并不是每个浏览器都能正确渲染每个网页。

## 同时适用于 Linux 和 Windows 的浏览器

目前跨平台兼容的浏览器选择是 Netscape。它拥有大多数主要平台的版本，并支持所有主要标准，包括框架、图像映射、插件、SSL（安全套接层）、Java 和 JavaScript。它包含在大多数 Linux 发行版中，可以在 www.netscape.com 获取 Windows 版本。

Star Office 有一个运行良好的浏览器。它渲染页面良好，但缺少一些高级功能，如 SSL、交互式 GIF 和 Java。关于 Star Office 的更多信息，请参见生产力应用程序部分 (www.sun.com/staroffice)。

有两个值得提及的浏览器：Lynx 和 Arachne。Lynx 是最老的浏览器之一，几乎在每个操作系统上可用。尽管它是一个纯文本浏览器，但它很有用。

Arachne 值得提及是因为它是一个图形浏览器。它支持所有主要标准且速度快。

## 浏览器

目前跨平台兼容的浏览器选择是 Netscape。它拥有大多数主要平台的版本，并支持所有主要标准，包括框架、图像映射、插件、SSL（安全套接层）、Java 和 JavaScript。它包含在大多数 Linux 发行版中，可以在 www.netscape.com 获取 Windows 版本。

Star Office 内置了一个运行良好的浏览器。它渲染页面良好，但缺少一些高级功能，如 SSL、交互式 GIF 和 Java。关于 Star Office 的更多信息，请参见生产力应用程序部分 (www.sun.com/staroffice)。

有两个值得提及的浏览器：Lynx 和 Arachne。Lynx 是最老的浏览器之一，几乎在每个操作系统上可用。尽管它是一个纯文本浏览器，但它很有用。

Arachne 值得提及是因为它是一个图形浏览器。它支持所有主要标准且速度快。

## Windows

目前跨平台兼容的浏览器选择是 Netscape。它拥有大多数主要平台的版本，并支持所有主要标准，包括框架、图像映射、插件、SSL（安全套接层）、Java 和 JavaScript。它包含在大多数 Linux 发行版中，可以在 www.netscape.com 获取 Windows 版本。

Star Office 内置了一个运行良好的浏览器。它渲染页面良好，但缺少一些高级功能，如 SSL、交互式 GIF 和 Java。关于 Star Office 的更多信息，请参见生产力应用程序部分 (www.sun.com/staroffice)。

值得提及的浏览器：Lynx 和 Arachne。Lynx 是最老的浏览器之一，几乎在每个操作系统上可用。尽管它是一个纯文本浏览器，但它很有用。

## Internet

目前跨平台兼容的浏览器选择是 Netscape。它拥有大多数主要平台的版本，并支持所有主要标准，包括框架、图像映射、插件、SSL（安全套接层）、Java 和 JavaScript。它包含在大多数 Linux 发行版中，可以在 www.netscape.com 获取 Windows 版本。

Star Office 内置了一个运行良好的浏览器。它渲染页面良好，但缺少一些高级功能，如 SSL、交互式 GIF 和 Java。关于 Star Office 的更多信息，请参见生产力应用程序部分 (www.sun.com/staroffice)。

值得提及的浏览器：Lynx 和 Arachne。Lynx 是最老的浏览器之一，几乎在每个操作系统上可用。尽管它是一个纯文本浏览器，但它很有用。

## 插件

浏览器插件是添加如声音和动画等额外功能的程序。当前的 Netscape 可以在 http://www.netscape.com 找到。

它是一个命令行邮件程序，但它支持上述所有主要的邮件标准。它具有高级功能，如摘要、地址簿、拼写检查和新闻阅读器。大多数 Linux 发行版包含一个 PINE。

Windows 版本。

MIME (Multipurpose Internet Mail Extensions) 允许部分邮件和非字母数字（非文本）附件作为声音和图形。

MIME (Multipurpose Internet Mail Extensions) 允许部分邮件和非字母数字（非文本）附件作为声音和图形。

## 电子邮件

这些是对主要的互联网邮件标准的非常简单的解释。

- 协议：
  - SMTP（简单邮件传输协议）允许服务器之间传输邮件。
- 远程邮件提取协议：
  - POP3（邮局协议版本3）将完整邮件下载到客户端。
  - IMAP4（互联网消息访问协议版本4）允许将实际消息存储在服务器上并下载所有头部。
- 消息格式：
  - RCF822 这是 ASCII（文本）消息的标准格式。
  - MIME（Multipurpose Internet Mail Extensions）允许部分邮件和非字母数字（非文本）附件作为声音和图形。

### 5.5.1 邮件客户端

有几种适用于 Linux 和 Windows 的流行邮件客户端。最简单的是 PINE（网络新闻和电子邮件程序）

PINE 是一个命令行邮件程序，但它支持上述所有主要的邮件标准。它还具有高级功能，如摘要、地址簿、拼写检查和新闻阅读器。大多数 Linux 发行版包含一个 PINE。

Windows 版本和关于 PINE 的更多信息请访问 http://www.washington.edu/

pine/

### 5.5 电子邮件

Netscape 在其 Netscape Communicator 中自带了一个图形化邮件程序，该程序也适用于大多数 Linux 发行版。关于该程序及其 Windows 版本的更多信息，可以访问 www.netscape.com。

Star Office 也包含一个邮件程序。Linux 和 Windows 版本均可从 Sun (www.sun.com/staroffice) 获取。提醒一下：这是一个巨大的下载包。

由于它是 Windows 的默认邮件程序，Outlook 同样值得提及。它有两个版本：Outlook 和 Outlook Express。两者的主要区别在于 Outlook 具有一些额外功能，例如管理多个邮箱的能力。

Outlook 的两个版本都支持所有标准的互联网邮件功能以及微软 Exchange Server 的功能。Outlook 可以作为任何标准邮件服务器或 Microsoft Exchange Server 的客户端。Exchange Server 使用专有协议来管理邮件、日历和全局地址列表。下一节关于邮件服务器的章节将讨论 Exchange Server。欲需更多信息，请参阅 www.microsoft.com。

### 5.5.2 邮件服务器

目前使用的邮件有两种类型：互联网电子邮件和协作邮件。互联网电子邮件支持 SMTP、POP3、IMAP 和 MIME。协作邮件支持所有互联网邮件标准，以及共享文件、目录和共享日历等额外功能。

**互联网邮件服务器。** Sendmail 是互联网上最常用的邮件传输代理 (MTA)。因为它具有可配置而广受欢迎，但也因为过于可配置而导致设置非常困难。它是开源的，适用于 Linux、Windows 以及许多其他操作系统。还有一个商业版本，包含了支持和配置工具，以使工作变得更简单（见 www.sendmail.org）。

虽然涵盖 Sendmail 的配置需要写一整本书，但有许多方法可以规避配置的痛苦。Sendmail 的主配置文件是 `/etc/sendmail.cf`。从头编写此文件几乎是不可能的。最好的方法是找到一个接近你需求的 sendmail.cf 示例并对其进行编辑。Sendmail 还包含一个宏文件 `sendmail.mc`，用于创建 `sendmail.cf`。一旦根据需要编辑了 `sendmail.mc`，使用以下命令创建 sendmail.cf：

```
m4 /etc/sendmail.mc > /etc/sendmail.cf
```



大多数用户甚至并不使用 `Sendmail` 的功能。例如，`Sendmail` 具有针对 `gccp` 和 `BitNet` 的功能，这些是已不再使用的旧互联网邮件系统。`Sendmail` 的官方网站 `www.sendmail.org` 上提供了详尽的文档。

`Qmail` 是另一个流行的 MTA。它比 `Sendmail` 更容易配置，但随之而来的是成熟度较低。`Sendmail` 自 1979 年一直在使用，而 `Qmail` 1.0 发布于 1997 年。与 `Sendmail` 一样，它是免费开源的。关于 `Qmail` 的程序和信息，请访问 `http://www.qmail.org/`

`Postfix` 是另一个流行的 MTA。许多用户对其速度和安全性赞誉有加 (`http://www.postfix.cs.uu.nl/`)。

这些只是可用 MTA 中的一部分。由于电子邮件是互联网最古老的用途之一，看到这么多 MTA 并不意外。

### 协作邮件
两个流行的协作邮件程序是 `Microsoft Exchange` 和 `Lotus Notes`。大多数公司使用这些程序不仅是为了发送电子邮件，为了维护中央邮件目录、共享文件和共享日历。如果要在企业环境中使用 Linux，那么与这些程序交互的能力至关重要。虽然有开放标准的轻量级目录访问协议 (`LDAP`)，但这两个协作邮件程序都没有使用它。

`Microsoft Exchange` 的流行程度目前略高于 `Lotus Notes`。`Exchange` 由两个部分组成：`Exchange Server` 和 `Outlook` 客户端。目前，`Exchange Server` 仅运行在 `Windows NT` 和 `2000` 上。`Outlook` 客户端运行在所有版本的 `Windows` 上。

有一些程序允许 Linux 与 `Exchange` 环境交互。在服务器端，惠尔罗普的 `OpenMail` 提供了比 `Microsoft Exchange Server` 更廉的替代方案。它要求在所有客户端机器上安装 `OpenMail` 客户端，但一旦安装，`OpenMail` 服务器在 `Outlook` 客户端看来就像 `Exchange Server` 一。关于 `HP OpenMail` 的更多信息可以访问 `http://www.ice.com/cyc/00/index.html`。

`TradeMail` 是一个允许 Linux 充当 `Outlook` 客户端的程序。它由位于 `Exchange` 服务器上的服务端组件和位于 Linux 机器上的客户端组成。`TradeMail` 可以运行，但目前尚未准备好投入生产。关于 `TradeMail` 的更多信息，请访问 `http://cobra.bynari.net/`。

### Lotus Notes
`Lotus Notes` 是第一个协作电子邮件程序。与 `Outlook` 类似，它由服务器和客户端组成。`Notes` 服务器适用于 Linux 和 `Windows NT/2000`。`Windows` 服务器已发布了一段时间，但最近新增的 Linux 服务器使得人们无需支付 `Windows` 费用即可获得 `Notes` 服务器 (`http://www.notes.com/home.nsf/welcome/notes` 和 `http://www.notes.net/linux`)。

`Windows` 有 `Notes` 客户端，但 Linux 没有。`Lotus` 表示他们没有开发 Linux 客户端的计划。如果你需要 Linux 版 `Notes` 客户端，有些人通过 `WINE` (`http://www.brookelines.com/linux/linuxnotes.html`) 运行 `Windows` 客户端取得了成功。

## 5.6 流媒体

流媒体允许在互联网上使用直播或录制的音视频。虽然这是一项相对新的技术，但随着宽带互联网的普及，它将变得越来越重要。

### 5.6.1 流媒体视频

目前，Linux 上唯一的完整流媒体包是 `Real Networks` (`http://www.realnetworks.com`)。使用 `Real Producer Basic` 创建内容适用于 Linux、Macintosh 和 Windows。它将实时视频或音频转换为 `Real` 格式，然后可以使用 `Real Player` 进行流传输播放。`Real Producer Plus` 具有额外功能，可以更好地优化 `Real Media` 文件。还有 `Real Producer Pro`，允许编码其他音频视频格式。遗憾的是，`Real Producer Pro` 仅适用于 Windows。

### 5.6.2 流媒体服务器

`Real Server` 适用于 Macintosh、`NT/2000` 以及各种 Unix 平台。使用 `Real` 流传输内容有两种方法：`HTTP` 和实时传输协议 (`RTP`)。对于低流量流传输，只需将 `Real` 文件链接到 Web 页面并允许 `HTTP` 传输文件即可。`RTP` 是数据传输的 IETF 标准，比 `HTTP` 更适用于流媒体。有关 `RTP` 的所有细节可以访问 `http://www.cs.columbia.edu/~dgs/rtp`。

对于高流量流传输，请使用 `Real Server`。免费的基础版允许运行 25 个流。超过部分，服务器费用基于最大流数量。例如，一个 60 流服务器的价格为 1995 美元。商业版本包含了密码保护流的功能以及转售流服务的许可。

### 5.6.3 Real 播放器

`Real Player Basic` 适用于 Linux 和 Windows。它允许终端用户查看 Media 文件和流。它还支持许多其他音频和视频格式，包括 `MP3`。还有一个 29 美元的 Plus 版本，具有额外功能，如图形均衡器和录制流的能力。49 美元的 `Real Player Pro` 还具有创建带视频音频的幻灯片的能力。

`Windows` 版 `Real Player` 的支持比 Linux 版更好。`Windows` 版 `Real Player` 已经发布了几个月，而 Linux 版仍然是测试版。

`Real Player` 的之前的版本。随着 `Real Networks` 宣布与 `Red Hat` 达成协议，将其 `Real Server` 与 `Red Hat Linux` 绑定，这种情况现在应该发生变化。

### 苹果的 QuickTime
有几种基于 `Apple QuickTime Server` 的 Linux 媒体流媒体服务器。`Apple QuickTime Server` 适用于 Macintosh 和多个版本的 UNIX (`http://www.publicource.apple.com/projects/streaming/`)。由于 `Apple` 不更改流，因此它是一个比 `Real Networks` 便宜得多的解决方案。缺点是 `QuickTime` 文件的 Linux 播放器正在开发中。

还有一个名为 `PRISS`（便携 RTSP 互联网流服务器）的流媒体服务器，这是一个基于 `Apple` 代码的开源项目 (`http://www.streaming-server.org/priss.html`)。这是目前唯一的视频流媒体传输开源项目。

`QuickTime` 播放器目前仅适用于 Macintosh 和 Windows (`http://www.apple.com/quicktime/download/`)。免费的 `QuickTime` 播放器允许播放 `QuickTime` 文件和流。售价 29 美元的 `QuickTime Pro` 还具有创建和编辑 `QuickTime` 的功能。

目前正在尝试创建支持 `QuickTime` 的 Linux 播放器。主要问题在于解码器（`CODECS`）。解码器用于创建音频和视频文件。问题是所有的解码器都拥有专利，没有人愿意为免费的 Linux 播放器支付解码器付费。尽管如此，有几个 Linux 播放器正在开发中。

Linux 最好的视频播放器是 `xanim`，它包含在大多数 Linux 发行版中。但问题是 `QuickTime` 使用的最常见解码器并不被支持。支持的解码器列表可以在 `http://xanim.pubnrix.com/xa_whatisit.html#format_support` 查看。

此外还有适用于 Linux 的开源 `QuickTime`，即 `Xmovie` 和 `Broadcast 2000`，它们可以使用某些有限的解码器创建和播放 `QuickTime` 电影。更多信息和下载可以在 `http://heroine.boxlinux.com/quicktime.html` 找到。

### Windows Media Player
`Windows Media` 并不是一种真正的跨平台解决方案。编码工具、服务器和播放器都是基于 `Windows` 的，不适用于 Linux。不过，该播放器适用于 Macintosh 和 Windows。有关 `Windows Media` 的更多信息可以访问 `http://www.microsoft.com/windows/windowsmedia/en/default.asp`，而工具、服务器和播放器可以在 `http://www.microsoft.com/windows/windowsmedia/default.asp` 获得。

### 5.6.4 音频流



音频流有更广泛的选择，它们在标准拨号连接上运行更好。上述列出的所有流媒体播放器都支持音频流。还有几种纯音频的流媒体程序。Web 上最流行的音频是 `MP3`。

`MP3` 最初作为在互联网上进行交易的一种。`MP3` 的主要吸引力在于它能够轻松从音频 CD 中创建文件，这些文件的质量与原始 CD 轨目相似，但大小仅为 CD 轨目的十分之一。一首典型的 `MP3` 歌曲在 1 到 2 兆之间，通过标准拨号连接可以在 20 到 30 分钟内下载。

随着 `Shoutcast` 的引入，`MP3` 在音频流方面变得流行。`Shoutcast` 是一套工具，允许 Windows 机器使用 `MP3` 格式编码并传输音频。

`Shoutcast` 软件包包含多个组件。`Shoutcast` 是 `Winamp` 的一组插件，`Winamp` 是一款流行的 Windows `MP3` 播放器（www.winamp.com）。例如，`DSP` 插件允许 `Winamp` 连接到 `Shoutcast` 服务器并向服务器发送压缩音频（http://scastweb2-qfe61.spinner.com/download/scast15ob2.exe）。

`Shoutcast` 没有压缩工具。这是因为 `MP3` 解码器拥有专利。微软提供了免费的 `Netshow` 压缩工具，可以处理 `MP3` 压缩 http://mskyrus.com.connion/mdownload/netshow/3.01/x86/en/nstools.exe

编码实时音频（而不是音频文件），你需要 `Shoutcast Live` 插件（http://www.shoutcast.com/download/in_rec.zip）。另一个实用的插件是实时输出插件（http://www.shoutcast.com/download/out_null.zip），它允许你在没有声卡的情况下传输音频。在广播文件而非实时音频时通常很常见。如果你不想从 PC 听到广播，它也很有用。

`Shoutcast Server` 适用于所有当前版本的 Windows 和许多版本的 UNIX（http://www.shoutcast.com/download/files.html）。它可以是一台独立的机器，或者对于 Windows 版本，编码工具和服务器可以是同一台机器。

还有一个开源的 `MP3` 播放器 `Icecast`（http://www.icecast.org）。它适用于大多数版本的 UNIX 和所有当前版本的 Windows。`Icecast` 将传输编码的 `MP3` 文件，并有一个 `Liveice` 程序用于编码实时音频流。

## MP3 播放器

`MP3` 的优势之一是有大量的可用播放器。大多数音频和视频播放器，如 Real Player 和 Windows Media Player 都支持 `MP3`。Windows Media Player 随所有当前版本的 Windows 绑定。其他一些 Windows 播放器：

- `Winamp` (http://www.winamp.com/)——可能是 Windows 上最流行的播放器。
- `Sonique` (http://www.sonique.com/)。
- `K-Jofol` (http://www.kjofol.com/)。

对于 Linux 有：

- `xmms` (http://www.xmms.org/)——可能是 Linux 上最流行的播放器。
- `MPG123` (http://www.mpg123.org/)——另一个流行的流行的播放器。
- `Freeamp` (http://www.freeamp.org/)——一个轻量级的 Linux 播放器。
- `Xaudio` (http://www.xaudio.com/)——一个图形化的 Linux 播放器。

有多个 IRC 服务器网络。同一个网络上的所有服务器都相互连接并共享消息。这允许世界上任何地方的用户通过连接靠近家中的服务器来加入 IRC。大多数 IRC 客户端已经内置了服务器列表，因此只需选择一个服务器即可。

有三个大型服务器网络：`DALnet` (http://www.dal.net/)、`Efnet` (http://www.efnet.net/) 和 `Undernet` (http://servers.undernet.org/)。虽然还有许多其他网络，但这三个网络在全球范围内有数百个服务器。

端口号与服务器地址一起列出。它通常看起来像：`us.undernet.org:6677`，其中最后一个数字是端口号。典型的端口有 6667 和 7000。

一旦连接成功，你需要加入一个频道（channel）。要列出可用频道，请在命令窗口中使用 `/LIST`。找到频道后，输入 `/JOIN <CHANNEL NAME>` 加入该频道。还有许多其他命令，请参阅您的 IRC 客户端文档。

另一个程序是 IRC 机器人（Bot），它会在 IRC 服务器上维护一个频道。通常当所有人都离开时，频道会关闭。而机器人会在频道为空时继续维护它。机器人还可以用于管理频道，例如封禁用户或设置密码保护频道。

大多数机器人适用于 UNIX。机器人的一些示例包括 `Eggdrop` (http://www.eggheads.org/)、以及适用于 Linux 的 `Acid Blood` (http://www.darkice.com/site/acidblood/download.htm) 或是适用于 Linux 和 Windows 的 `Dancer` (http://www.contactor.se/~/dancer/)。

## 即时通讯

即时通讯对于互联网来说相当新。它演变为 20 世纪 90 年代流行的 AOL 即时消息 (`AIM`)。它的工作原理与电子邮件类似，但当你发送消息时，它会立即显示在接收端，而不需要点击来取回。

即时通讯的问题在于没有统一标准。最流行的即时通讯客户端包括 `AIM` (www.aol.com)、`ICQ` (www.icq.com)、`Yahoo` (www.yahoo.com) 和微软网络，即 `MSN` (http://www.hotmail.com))。`AIM`、`ICQ` 和 `Yahoo` 都有 Linux 客户端。在 Fresh Meat 上可以找到这些程序的完整页面，它是一个列出 Linux 开源软件的网站 (http://www.freshmeat.com/appendix/x11/communication.html)。

两个值得的程序有 `Everybody` 和 `licq`。`Everybody` 用一个程序管理多个不同的即时通讯账户。它目前支持 `AIM` 和 `ICQ`，并很快将支持 `Yahoo` 和 `MSN` (www.everybuddy.com)。

`licq` 仅支持 `ICQ`，但它支持 `ICQ` 的一些高级功能，如多人聊天 (www.liq.org)。

还有一个基于 XML 标准的开源即时通讯服务器和客户端项目（关于 XML 的解释请参见生产力应用程序章节）。`Jabber` 项目的详情，包括服务器和客户端，可以在 http://www.jabber.com/ 获取。

## 网络安全

将计算机连接到互联网意味着它与全球数百万台计算机连接。在大多数情况下，这是好事，但也让你的计算机容易受到远程攻击。

Linux 或 Windows 的标准加载并不安全。Linux 和 Windows 倾向于加载所有可用的后台程序，这为敌对黑客提供了攻击途径。关闭未使用的服务是网络安全的第一步。以 root 或等权限运行的特权进程允许连接到它们。这些端口用于 `FTP`、`telnet` 和 `HTTP` 等常用协议。

有几种方法可以查看你运行了哪些服务。一种是使用 `ps -ef|more` 列出进程。这将显示一个类似下方的列表：

| PID | STAT | COMMAND |
|---|---|---|
| 1 | S | 0:03 init [5] |
| 2 | ? | 0:00 [kflushd] |
| 3 | ? | 0:00 [update] |
| 4 | ? | 0:00 [kpiod] |
| 5 | ? | 0:05 [kswapd] |
| 6 | SW< | 0:00 [mdcoveryd] |
| 341 | S | 0:00 syslog -m 0 |
| 351 | S | 0:00 klogd |
| 366 | S | 0:00 /usr/sbin/atd |
| 381 | S | 0:00 cron |
| 396 | ? | 0:00 [lpd] |
| 435 | ? | 0:01 xifs -port -1 -daemon |
| 449 tty1 | SW | 0:00 [mingetty] |
| 450 tty2 | SW | 0:00 [mingetty] |
| 451 tty3 | SW | 0:00 [mingetty] |
| 452 tty4 | SW | 0:00 [mingetty] |
| 453 tty5 | SW | 0:00 [mingetty] |
| 454 tty6 | SW | 0:00 [mingetty] |
| 455 ? | S | 0:00 kdm -nodemon |



第一个字段是进程 ID（Process ID）。这是分配给每个进程的数字。第二个字段 TTY 是终端号。`?` 用于未知终端，这通常意味着它是系统或 X11 进程。第三个字段是进程状态，含义如下：

- D-不可中断睡眠（通常是在等待 IO）。
- R-可运行（在队列中）。
- S-睡眠。
- T-停止或已停止。
- Z-僵尸（"defunct"）进程。
- W-有驻内存。
- H-高优先级。
- N-低优先级。
- L-页面锁定到内存（实时）。

第四个字段是程序运行的时间。注意这里大部分值都是 0，原因是程序运行了一段时间后又进入睡眠。第五个字段是进程名。要检查开放端口，请使用 `netstat -a`。这将显示类似的内容：

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
|---|---|---|---|---|---|
| tcp | 0 | 0 | localhost:1600 | * | TIME_WAIT |
| tcp | 0 | 0 | | * | CLOSE |
| tcp | 0 | 0 | blue.aol.co:ftp | * | ESTABLISHED |
| tcp | 0 | 0 | yahoo.yahoo.com:5050 | * | ESTABLISHED |
| tcp | 0 | 0 | yahoo.yahoo.com:5050 | * | ESTABLISHED |
| tcp | 0 | 0 | yahoo.yahoo.com:5050 | * | ESTABLISHED |
| tcp | 0 | 0 | yahoo.yahoo.com:5050 | * | ESTABLISHED |
| tcp | 0 | 0 | yahoo.yahoo.com:5050 | * | ESTABLISHED |
| tcp | 0 | 0 | yahoo.yahoo.com:5050 | * | ESTABLISHED |
| tcp | 0 | 0 | :1536 | * | LISTEN |
| tcp | 0 | 0 | :1089 | msgr-ns.hotmail.com:1863 | ESTABLISHED |
| tcp | 0 | 0 | :6000 | * | LISTEN |
| tcp | 0 | 0 | :1024 | * | LISTEN |
| tcp | 0 | 0 | :printer | * | LISTEN |
| udp | 0 | 0 | :1024 | icq.aol.co:4000 | ESTABLISHED |
| udp | 0 | 0 | :xdmcp | * | |
| raw | 0 | 0 | :icmp | * | 7 |

最重要的字段是最后一个。如果是 `LISTEN`，则端口已准备接受连接。本地地址是主机名或端口。例如，`tcp 0 0 *:printer` 意味着打印服务正在监听 TCP 协议。

端口扫描器可以 http://www.insecure.org/nmap/ 下载。它可以用于扫描本地和网络连接机器的开放端口。例如，扫描本地机器输入 `nmap localhost`。这将给出开放端口列表：

| Port | State | Service |
|---|---|---|
| 515/tcp | open | printer |
| 1024/tcp | open | unknown |
| 1536/tcp | open | ampr-inter |
| 6000/tcp | open | X11 |

未经许可不要扫描别人的机器。他们可能会认为你正试图入侵他们的系统！

Gibson Research Corporation 提供了一个在线端口扫描器。该网站包含计算机安全的通用信息 (www.grc.com)。

## 第 5 章 互联网应用程序

一旦确定了哪些端口开放，我们需要关闭未使用的端口。要检查的第一地方是 `/etc/inetd.conf` 文件。该文件包含许多标准 UNIX 服务，如 FTP、telnet、POP 和 finger。如果你需要其他计算机通过这些服务连接到你的计算机，请在服务前加上 `#` 来关闭它们：

```
#ftpstreamtpcnowaitrootusr/sbin/tcp.. -1 -a
#telnet stream tcp nowait root /usr/sbin/tcp.telnet
```

如果你对服务的作用有任何疑问，请查看 man 页。例如，要了解 FTP 的作用，在命令行提示符输入 `man ftp`。如果你确实需要这些服务之一，Secure Shell (`SSH`) 提供了更好的安全性。参见 SSH 章。大多数其他服务在 `/etc/rc.d` 下的目录下启动。该目录有子目录：

```
[root@mmcune rc.d]# ls
init.d/ rc.firewall rc.sysinit* rc1.d/ rc3.d/ rc5.d/
rc* rc.local* rc0.d/ rc2.d/ rc4.d/ rc6.d/
```

子目录取决于运行级别（run level）。要确定运行级别，输入 `runlevel`：

```
[root@mmcune rc.d]# runlevel
N 5
```

在这个示例中，我们使用运行级别 5，因此子目录为 `rc5.d`。`rc5.d` 的内容如下：

```
[root@mmcune rc5.d]# ls
K20statd@ K42ecd@ K80ncd@ K99sendmail@ S40atd
S91local@K20users@ K50nms@ K87tybind@ S05kaddu@ S40crond@
K20rowhd@ K52imap@ K93portmap@ S10network@ S60lpd@
K35usb@ K73webited@ K98nfslock@ S30syslog@ S90xifs
```

第一个字母代表杀死或启动。只有带有 "s" 的文件会被加载。数字代表加载文件的顺序。数字越小，加载越早。某些服务必须在其他服务之前启动。例如，network 必须在 netfs 之前启动。最后是服务的名称。如果你想知道服务的作用，再次使用 man 页。要关闭某个服务，将第一个字母改为 "s"。例如，关闭 atd 输入：

```
mv S40atd K40atd
```

## 网络安全

在精简服务后，系统会再次检查开放端口。完成后，我们需要获取一些工具来监控和保护系统。

要做的第一件事是寻找更新。Linux 中大多数已知的安全漏洞都能被修复，但许多用户忽略了下载修复程序。大多数 Linux 发行版都会在自己的网站上发布补丁。你可能还想订阅 Cert (www.cert.org) 和 BugNet (www.bugnet.com) 邮件列表。

针对 Linux 和 Windows 都有个人防火墙。防火墙是一种限制从互联网到本地网络和计算机的访问的设备或程序。适用于 Linux 的免费防火墙是 Phoenix Adaptive Firewall (http://www.progressive-systems.com/products/phoenix)。对于 Windows，有 Zone Alarm (http://www.zonelab.com/)。这些程序供个人使用是免费的。Phoenix 和 Zone Labs 也提供商业许可。

Tripwire 是一款开源入侵检测软件。它的原理相当简单。Tripwire 会对系统设置进行快照并将其存储在软磁盘上。之后可以再次运行 Tripwire 来确定任何系统设置是否发生了变化。当黑客入侵系统时，他们会更改系统设置以便于再次轻松进入。Tripwire 可以检测到这一点。Tripwire 可于 http://www.tripwire.org。

在你的系统上安装端口扫描器也是一个好主意。最好的应该是 Psionic 的 PortEntry (http://www.psionic.com/abacus/portsentry/)。如果 PortEntry 检测到端口扫描，它将断开来自扫描机器的连接并阻止其进一步连接。该程序仅提供源码，但如果你按照安装说明操作，可能会遇到编译问题。

下载源码后，解压文件：

```
gunzip portsentry-1.0.tar.gz
tar xvf portsentry-1.0.tar.tar
```

接下来，编辑 `portsentry_config.h` 以添加 PortEntry 使用的文件位置。

在许多情况下，默认值为：

- CONFIG_FILE—PortEntry 配置文件的路径。默认位置为 `/local/psionic/portsentry/portsentry.conf`。
- WRAPPER_HOSTS_DENY—TCP Wrapper `hosts.deny` 文件的名称和路径。在大多数系统中，该文件位于 `/etc/hosts.deny`。
- SYSLOG_FACILITY—PortEntry 使用的 syslog 设施。



`SYSLOG_LEVEL`—发送消息的 syslog 级别。

然后，编辑 `portsentry.conf`。`README.install` 解释了不同的设置。

添加任何你希望 PortEntry 忽略的主机到 `portsentry.ignore`。

最后，编译程序：

```
make linux
make install
```

这将把程序和配置文件放在 `/usr/local/psionic/portsentry` 中。要启动 PortSentry，进入此目录并输入：

```
./portsentry <option>
```

选项在 `README.install` 中有详细解释。你一次只能使用一个选项，但如果你想同时监控 TCP 和 UDP 端口，可以加载多次 PortSentry。例如，若要在 TCP 和 UDP 端口上都使用高级扫描（最安全），请输入：

```
./portsentry -atcp
./portsentry -autp
```

# 业务应用程序

对于我们的目的而言，业务应用程序是指运行在个人 PC 上并执行业务功能的程序。最最销的软件标题加载了各种业务应用程序。例如，销量最畅销的 Microsoft Office 是一系列常用业务应用程序的组合，包括文字处理器 `Word`、电子表格 `Excel` 和演示文软件 `PowerPoint`。

某些版本的 Microsoft Office 包含电子邮件和日历程序 `Outlook` 以及数据库 `Access`。这两个应用程序在其他章节中都有介绍。

财务程序如 Intuit 的 Quicker 和 Microsoft Money 也是必重要的业务程序。图形程序如 Adobe Photoshop、Corel Draw 和 Microsoft Visio 完善了这一业务程序列表。

## 6.1 Microsoft Office

凭借 95% 的市场份额，Microsoft Office 是生产力套件中的“重量级选手”。如果你从别人那里得到一个文档、电子表格或演示文稿，它很有可能是一个 Microsoft Office 文件。

因此，为了让 Linux 在桌面端流行起来，它必须有一个与 Microsoft Office 相似的程序，并且必须能够读写 Office 文件。

Linux 有几个与 Microsoft Office 相似的程序。它们大部分都有 Windows 版本。但没有一个是 Microsoft Office 的完整、无缝替代品。每个程序都有需要考虑的优缺点。

处理 Office 文件是一个大问题。由于每个 Office 应用程序都使用专有格式，因此在其他程序打开它们之前，必须对文件格式进行反向工程。Office 应用程序彼此以及与 Windows 操作系统紧密集成，这一事实使得问题更加复杂。目前，没有任何 Linux 应用程序 100% 兼容 Office 文件，但某些比其他的要好。

## 6.2 Corel WordPerfect Office

虽然它的市场份额远不及 Microsoft Office，但 Corel WordPerfect Office 是市场上第二种受欢迎的生产力套件。它具有与 Microsoft Office 相同的所有功能，包括文字处理 `WordPerfect`、电子表格 `Quatro Pro`、演示 `Presentations`、日历 `CoreCENTRAL` 和 Web 发布 `Trellix`。豪华版还带有一个数据库 `Paradox`、更多字体、更多剪贴画、游戏《铁路大亨》以及服务器版 `http://www.corel.com/Office2000/index.htm`。Linux 版的 WordPerfect `WP` 与 Windows 版本代码相同，因此版本看起来几乎完全一样。Core 决定使用 `WINE` 库来实现低级兼容。`WP Office` 自带一个服务器。标准版带有 100 多种字体。服务器还允许通过将字体拷贝到目录来使用 Windows 和 TrueType 字体！`WP Office` 拥有任何 Linux 中效果最好的字体。加载 `WP Office` 程序大约需要 30 秒到 2 分钟。加载 `WINE` 仅需几秒钟。一旦程序加载，在良好的电脑上响应是合理的。请注意，`WP Office` 不适用于低端系统。为了获得良好的性能，你必须拥有 Pentium 200 或更好的处理器、64MB 内存和 540MB 空闲磁盘空间。Core 花了大量时间让 `WP Office` 能够读写 Office文档。`Word`、`Excel` 和 `PowerPoint` 文档导入 `WP Office` 并没有太大困难。在本章后面的部分，我们将讨论导入导出 MS Office 文件。`WP Office` 还具有导出 HTML、XML、RDF 和 TIFF 等便携格式的能力。HTML 是网页使用的标准格式。`WP Office` 允许将文档、电子表格和演示文稿直接导出为 HTML 发布在网页上，无需单独的 HTML 编辑器。XML 与 HTML 类似，但用户可以定义自己的数据格式。Adobe 的 PDF（文档格式）允许文档在不同平台上看起来完全相同。它是分文档和法律摘要的流行方式。最后，RTF（富文本格式）最早被 Microsoft Word 用于将 Word 文档导出到其他文字处理器。它不支持现代文字处理器的高级功能，但所有主要的文字处理器都支持它。`WP Office` 也有一些缺点。在某些 Linux 发行版上存在安装问题。它似乎在 Red Hat、Mandrake 和 Core Linux 上安装良好，但在其他发行版（包括 SuSE Linux）上存在问题。许多这些问题都有解决方法。更多信息请查看 Core 支持页面 `http://corel.com/support/wp2000-linux.htm`。运行 `WP Office` 还会导致稳定性问题。`WINE` 仍在开发，尚未稳定。幸运的是，`WP Office` 的崩溃不会导致整个桌面崩溃。只需确保开启了自动保存功能：前往工具 -> 设置 -> 文件 -> 文档，勾选定时文档备份并设置分钟数即可。

## 6.3 其他商业生产力套件

59

![](img/a1ad58e4259f15e8b2826ecf57a28362_74_0.png)

**图 6.1** 设置自动保存功能。在这种情况下，设置为每 10 分钟保存一次。

Linux 版 `WP Office` 缺少了大多数办公套件常见的两个功能：互联网集成和与个人数字助理（PDA）的热同步（HotSync）。`WP Office` 没有内置的 Web 浏览器或电子邮件。Netscape 捆绑 `WP Office` 并不是什么大问题，但有时在不打开另一个应用程序的情况下查看邮件或网页会更方便。

HotSync 将 Windows 版 `WP Office` 和所有版本的 Star Office 连接起来。如果与 PDA 同步日历对你很重要，你可能想要考虑 Linux 的 Star Office。

### 6.21 Linux 版 WordPerfect 8

WordPerfect 8 `WP8` 仍然可以从 Core 网站下载。虽然它作为版本 9 兼容 Microsoft Office，但它仍然保留了版本 9 的大部分功能。它的运行速度也快得多，因为它使用的是原生代码而非 `WINE`。它是低端系统的极佳选择，因为它可以在带有 16MB 内存的旧 486 电脑上运行。

`WP8` 提供免费版和完整的商业包，零售价约为 50 美元，尽管它的售价通常更低。个人版是一个功能齐全的程序。完整版包含了个人版未包含的额外图形、剪贴画和字体 `http://corel.com/products/wp8/`。

## 6.3 其他生产力套件

Lotus SmartSuite 还没有推出 Linux 版的官方计划，但我对 Lotus 决定将 SmartSuite 移植到 Linux并不并不意外，因为他们已经注意到母公司 IBM 正在向 Linux 开发投入大量资源。

### 6.3.1 Star Office

Sun 的 Star Office 对 Microsoft 文件支持非常出色。它提供了与文字处理 `Writer`、电子表格 `Calc`、演示文稿 `Impress`、图形 `Draw`、电子邮件 `Mail`、日历管理 `Schedule` 和数据库 `Base` 等效的程序。它还集成了一个 Web 浏览器。虽然它的功能没有像 Microsoft Office 那么丰富，但它提供了所有功能，如页眉、页脚和模板。

### Star Office 最大的缺点可能是它的体积和速度。它需要 60MB 的磁盘空间和至少 32MB 的内存才能获得体面的性能。即使在快速系统上，它的加载也需要时间。Star Office 确实具有 HotSync 功能，这是其他 Linux 办公套件所不具备的。如果将 PDA 与你的办公套件同步对你很重要，Star Office 提供了最好的支持。

Star Office 还内置了一个桌面。在 Windows 机器上，它用自己的桌面替换默认的 Windows 桌面。可以从 Sun 网站免费下载 Star Office，或者以约 40 美元的价格通过 CD 购买 `http://www.sun.com/staroffice/`。



Sun 通过在 Star Office 中提供 XML 支持，抢在了微软的前面。微软没有计划直到 2002 年才提供 XML 支持。办公套件的争夺可能会变得有趣。

### 6.3.2 Applix

虽然它对 MS Office 格式的支持没有 Star Office 那么，但许多人更喜欢 Applix 的界面和更整洁的字体。Applix 并不是接管桌面，而是在单独窗口中加载每个应用程序。

Applix 也是低端系统的良好选择，因为它可以在带有 32MB 内存和约 250MB 磁盘空间的 486 电脑上运行。

许多 Linux 发行版包含 Applix 的演示版。你也可以从 Applix 网站下载。然而，该程序并不是免费的。注册版花费 40 美元，开发者版升级需要 90 美元（`http://www.applix.com`）。

## 6.4 开源办公套件

KDE 和 Gnome 都有开发中的开源办公套件。两者目前尚未达到生产级水平，但功能都非常丰富。

### 6.4.1 Koffice

KDE 的办公套件包含一个文字处理器（Kword）、电子表格（Kspread）、演示文稿软件（Kpresent）、图表程序（Kchart）、一个矢量绘图工具（Karator）、一个图像处理程序（Kimage）、基于层的图像创建程序（KImagePaint）和一个数据库前端（Kabase）。

Koffice 仍在开发中，尚未准备好供日常使用。尽管如此，对于一个开发中的项目来说，Koffice 的稳定性非常惊人且功能完整。请关注 Koffice。它是一个崭露头角的竞争者！

### 6.4.2 Gnome Office

Gnome 也有办公套件；与 Koffice 不同，Gnome Office 是开源工具的集合，而不是从零开始设计的新套件。Gnome Office 的目标是提供 Microsoft Office 的功能，并与 Microsoft Office 文件具有良好的性。遗憾的是，组件仍在开发中。

Gnome Office 的核心是电子表格 Gnumeric。这是一个创建一个全功能 GPL 电子表格的 Gnome 项目。它的目标之一是克隆 Microsoft Excel 的外观和功能。AbiWord 是 Gnome 的文字处理器。它没有许多其他文字处理器的所有功能，但它运行非常快且界面简洁。

GNU 图像处理程序 (GIMP) 是 Linux 上最早的源码桌面应用程序之一。GIMP 是一个类似于 Adobe Photoshop 的照片和图像修饰程序。虽然它的界面没有 Photoshop 那么精致，但 GIMP 非常强大。作为一个类似于 Dia 的绘图程序，它是开发者绘制图表和流程图的快速工具。Eye of Gnome (EOG) 是一个快速图像查看器。它的设计是为了快速查看图像文件，而无需在 GIMP 等大型应用程序中打开。

Gnome-PIM 提供了商业办公套件中标准的日历和地址录。最后，Gnome-DB 为设计数据库前端提供了应用程序和库。关于 Gnome Office 的详情请访问 `http://www.gnome.org/gnome-office/`

## 6.5 Web 办公套件

很难判断它们是否会流行，但 Web办公套件是真正的跨平台。这些套件在 Netscape 或 Internet Explorer 内部运行，允许它们在任何操作系统上运行。

Web办公套件 (WBS) 分为两种：服务器端和客户端。服务器端应用程序在服务器上运行，并将图像发送到客户端。文件通常存储在服务器上。客户端应用程序使用 MS Office 作为后端，并提供近乎完美的兼容。其他的使用 Star Office、Apprix 或自定义应用程序。服务器端应用程序的一个示例是 FreeDesk.com，它使用免费的自定义应用程序（`www.freedisk.com`）。

[PAGE 77]

# 62

# 第 6 章 • 业务应用

![](img/a1ad58e4259f15e8b2826ecf57a28362_77_0.png)

**图 6.2** Free Desk 办公套件。

客户端应用程序需要你下载一个在浏览器内部运行的 Java 应用程序。这些应用程序的一个示例是 ThinkFree。注册后，你可以下载一个（约 10 MB）Java 程序，其中包含文字处理器、电子表格和演示文稿软件。下载程序后，它会在浏览器窗口中启动。相比于 MS Office 或 WordPerfect，它更像是 MS Words 那种轻量级套件。ThinkFree 仍然是测试版软件，因此它会随着时间的推移而改进（`www.thinkfree.com`）。

## 读取和写入 Microsoft Office 文件

![](img/a1ad58e4259f15e8b2826ecf57a28362_78_0.png)

基于 Web 的办公套件仍然相对较新。它们会流行吗？它们是否提供了跨平台兼容性以及在 Web 上存储文档的能力？缺点是，它们不像独立应用程序那样成熟且功能齐全。基于服务器的应用程序还有一个缺点是不允许离线使用。WBS（Web办公套件）是否流行只能时间检验。

## 读取和写入 Microsoft Office 文件

在其他程序中使用 Office 文件一直以来都是棘手的。即使在旧版本的 Office 中使用 Office 文件也会导致问题。将一个来自 Office 97 的复杂的 Word 文档转换为 Word 95 格式通常会导致格式丢失。为了使问题更加复杂，MS Office 在每个版本的 Office 中都更改了数据格式。这意味着 Office 95 将无法打开由 Office 97 创建的文档。这通常迫使人们升级他们的 MS Office 版本，以便能够读取由该版本 Office 创建的文档。这方面的情况可能会发生变化；MS Office 2000 使用与 MS Office 1997 相同的格式。

第 6 章 业务应用

## 6.7 导出 MS Office 文件

幸运的是，MS Office 允许用户以多种格式保存文件。除了允许保存旧格式外，MS Office 还允许以竞争性程序的格式保存文件，例如 WordPerfect、Lotus 123、Quatro Pro、Freelance 等许多许多格式。虽然转换并不完美，但只要 MS 用户知道对方在使用什么，它至少允许 MS 用户与非 MS Office 用户交换文件。

如果格式未知，您可以使用便携格式，如富文本格式 (RTF)、超文本标记语言 (HTML)、可扩展标记语言 (XML)、便携文档格式 (PDF)、数据交换格式 (DIF)、分隔符文本或纯文本 (`TXT` 或 `ASCII`)。所有这些格式都可能丢失数据，因此最好也以原生 Office 格式保存。

RTF 是最初由 MS Word 使用的格式，用于与其他文字处理器轻松交换文档。它不支持 MS Word 的所有高级功能，但所有现代文字处理程序都支持它（`http://msdn.microsoft.com/library/specs/richtformatrspecificationsamplereaderprogramversion5.html`）。

HTML 是全球维网 (WWW) 使用的格式。HTML 的主要优势是所有操作系统都包含 Web 浏览器。

XML 与 HTML 类似，但它更灵活。HTML 拥有一由 HTML 标准定义的有限格式选项集。XML 允许创建用户定义的标签，从而提供了更多的格式选项。XML 还承诺提供数据处理的“圣杯”之一——数据与格式的分离。这将允许数据存储在一个地方，然后以多种格式派送。XML 的问题在于它仍然是一个不断演进的标准，并不是所有的程序都支持它（`www.w3.org/xml`）。

PDF 是由 Adobe 创建的一种标准，允许文档在多种格式上显示。它是创建政府和法律文档的一种流行方式，因为它具有便携性并支持许多现代格式功能。Adobe 的程序可以在 Linux、Windows 和许多其他平台上创建和读取 PDF 文件。Adobe 有一个免费的 PDF 阅读器，还有一个免费的 Linux 视器。此外，许多其他程序（如文字处理器）也可以创建 PDF 文件。

有一些开源程序可以帮助处理 PDF 文件。`xpdf` 可以打开 PDF 文件，尽管它在查看某些 PDF 文件时有时会出现问题。`Ghostscript` 会将 PostScript 打印文件转换为 PDF。

DIF 是数据库使用的一种交换文件的格式。它被许多电子表格和数据库程序支持。

分隔符文本是电子表格和数据库程序交换数据的另一种方法。它比 DIF 格式简单得多，并且被所有现代文字处理、电子表格和数据库程序支持（`http://www.microsoft.com/enable/download/products/office/office97/part06.html`）。



标准文本也称为 ASCII（美国信息交换标准代码），是 DOS 和 UNIX 系统中存储文本的标准格式。它不支持任何格式，但可以被几乎任何计算机程序读取。不过，DOS 和 UNIX 使用不同的换行符。有一些程序可以将 DOS 文本转换为 UNIX，反之亦然。例如，在 Linux 提示符中，你可以输入以下命令将 DOS 文件转换为 UNIX：`tr -d '\15\032' < dosfile.txt > unixfile.txt`。你也可以使用 `awk` 进行翻译：

有一些技术可以使 MS Office 文件变得更容易处理。显然，越复杂的文件越难进行排序，因此如果你计划导出一个文件，请保持其简单。文档中的嵌入和链接也会导致问题。

嵌入和链接的主要区别在于，嵌入是将对象的副本放在 Office 文件中，而链接是在文件中放置指向对象的链接。如果原始对象被更改，嵌入对象不会更改，但链接对象将在所有文档中更新。链接非常方便，因为你不需要更新链接对象，但它也不利于导出。如果你打算导出，请使用嵌入而不是链接；只需将对象作为单独文件包含。有关如何在 MS Office 文档中嵌入和链接的信息，请参阅您的 MS Office 用户手册或本教程。

`WordArt`、`自动形状`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`。

## 6.8 导入和导出 MS Office 文件

幸运的是，MS Office 允许用户以多种格式保存文件。除了允许保存旧格式外，MS Office 还允许以竞争性程序的格式保存文件，例如 `WordPerfect`、`Lotus 123`、`Quatro Pro`、`Freelance` 等许多。虽然转换并不完美，但只要 MS 用户知道对方在使用什么，它至少允许 MS 用户与非 MS Office 用户交换文件。

如果格式未知，您可以使用便携格式，如富文本格式 `RTF`、超文本标记语言 `HTML`、可扩展标记语言 `XML`、便携文档格式 `PDF`、数据交换格式 `DIF`、分隔符文本或纯文本 `TXT` 或 `ASCII`。所有这些格式都可能丢失数据，因此最好也以原生 Office 格式保存。

`RTF` 是最初由 MS Word 使用的格式，用于与其他文字处理器轻松交换文档。它不支持 MS Word 的所有高级功能，但所有现代文字处理程序都支持它（http://msdn.microsoft.com/library/specs/richtformatrspecificationsamplereaderprogramversion5.html）。

`HTML` 是全球维网 `WWW` 使用的格式。`HTML` 的主要优势是所有操作系统都包含 Web 浏览器。

`XML` 与 `HTML` 类似，但它更灵活。`HTML` 拥有一由 `HTML` 标准定义的有限格式选项集。`XML` 允许创建用户定义的标签，从而提供了更多的格式选项。`XML` 还承诺提供数据处理的“圣杯”之一——数据与格式的分离。这将允许数据存储在一个地方，然后以多种格式派送。`XML` 的问题在于它仍然是一个不断演进的标准，并不是所有的程序都支持它（www.w3.org/xml）。

`PDF` 是由 Adobe 创建的一种标准，允许文档在多种格式上显示。它是创建政府和法律文档的一种流行方式，因为它具有便携性并支持许多现代格式功能。Adobe 的程序可以在 Linux、Windows 和许多其他平台上创建和读取 `PDF` 文件。Adobe 有一个免费的 `PDF` 阅读器，还有一个免费的 Linux 视器。此外，许多其他程序（如文字处理器）也可以创建 `PDF` 文件。

有一些开源程序可以帮助处理 `PDF` 文件。`xpdf` 可以打开 `PDF` 文件，尽管它在查看某些 `PDF` 文件时有时会出现问题。`Ghostscript` 会将 PostScript 打印文件转换为 `PDF`。

`DIF` 是数据库使用的一种交换文件的格式。它被许多电子表格和数据库程序支持。

分隔符文本是电子表格和数据库程序交换数据的另一种方法。它比 `DIF` 格式简单得多，并且被所有现代文字处理、电子表格和数据库程序支持（http://www.microsoft.com/enable/download/products/office/office97/part06.html）。

标准文本也称为 `ASCII`（美国信息交换标准代码），是 DOS 和 UNIX 系统中存储文本的标准格式。它不支持任何格式，但可以被几乎任何计算机程序读取。不过，DOS 和 UNIX 使用不同的换行符。有一些程序可以将 DOS 文本转换为 UNIX，反之亦然。例如，在 Linux 提示符中，你可以输入以下命令将 DOS 文件转换为 UNIX：`tr -d '\15\032' < dosfile.txt > unixfile.txt`。你也可以使用 `awk` 进行翻译：

有一些技术可以使 MS Office 文件变得更容易处理。显然，越复杂的文件越难进行排序，所以如果你计划导出一个文件，请保持其简单。文档中的嵌入和链接也会导致问题。

嵌入和链接的主要区别在于，嵌入是将对象的副本放在 Office 文件中，而链接是在文件中放置指向对象的链接。如果原始对象被更改，嵌入对象不会更改，但链接对象将在所有文档中更新。链接非常方便，因为你不需要更新链接对象，但它也不利于导出。如果你打算导出，请使用嵌入而不是链接；只需将对象作为单独文件包含。有关如何在 MS Office 文档中嵌入和链接的信息，请参阅您的 MS Office 用户手册或本教程。

`WordArt`、`自动形状`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`、`宏`、`透视表`、`垂直规则`（此处省略重复部分，由于原文包含大量重复词汇，此处按要求保留逻辑，实际翻译中）

## 6.8 导入和导出 MS Office 文件

由于 MS Office 占据了 90% 的市场，导入和导出 MS Office 文件是必要的。我将使用 Star Office 作为示例，因为它能很好地支持 MS Office 文件。Star Office 支持这些功能：

- Microsoft Word：

  - 自动形状

  - 修订标记

  - OLE 对象

  - 索引

  - 表、帧和多栏格式

  - 超链接和书签

- Microsoft Excel：

  - 透视表

  - 图表类型

  - 条件格式

  - 自动形状

  - OLE 对象

  - 大多数函数

- Microsoft PowerPoint：

  - 自动形状

  - 制表、行落间距

  - 主背景图形

  - 分组对象

  - 多媒体效果

## 6.9 在 Star Office 中使用 MS Office 文档

Star Office 对 Word 和 Excel 文件的支持非常好。尽管可能会丢失一些格式，但你几乎总是可以通过 Star Office 获取一个可读的文件。另一方面，PowerPoint 被列为支持的格式之一，但 Star Office 并不总是能打开它。

要打开 Excel 或 Word 文件，只需从菜单选择“文件 -> 打开”。Word 文件将显示熟悉的 Word 图标，Excel 文件将显示 Excel 图标。

![](img/a1ad58e4259f15e8b2826ecf57a28362_82_0.png)

图 6.5 Star Office 在 Microsoft Word 文档上显示熟悉的图标。接下来，只需点击文件并选择“打开”。如果 Star Office 识别该文件，它就会直接打开。如果文件有问题，它将显示以下错误消息：

![](img/a1ad58e4259f15e8b2826ecf57a28362_82_1.png)

图 6.6 保存文件出现问题时显示的错误消息。

保存文件时，建议使用“另存为”选项，以防覆盖现有文件。Star Office 的某些功能可能无法正确转换为 MS Office 格式。如果你担心丢失格式，最好将文档保存为 Star Office 格式。Star Office 使用 StarWriter 格式处理文本文档，使用 StarCalc 处理电子表格。

# 第 6 章 • 业务应用

![](img/a1ad58e4259f15e8b2826ecf57a28362_83_0.png)



图 6.7 以原生格式保存 `StarWriter` 文件。

## 6.10 导入和导出时的检查点

![](img/a1ad58e4259f15e8b2826ecf57a28362_84_0.png)

图 6.8 以原生格式保存 `StarCalc` 文件。

每当导入或导出文件时，都有可能丢失格式或数据的风险。一些需要检查的项包括：

- 总页数或工作表总数——字体和行间距的改变会改变文档的大小。检查电子表格的名称和布局。
- 页码、脚注、页眉和页脚——这些位置可能会发生变化，甚至可能重叠。还要检查字体大小。
- 字体——字体类型和大小可能已经发生了变化。
- 图形和图表——不支持的图形将显示为灰色方框。还要检查图形的位置。图表样式和数据可能已经发生了变化。
- 列——检查对齐方式、间隙和文字流。
- 表格——检查间距（高度和宽度）、阴影和字体。
- 文档属性——检查作者和日期等元数据信息。
- 特殊标记——检查索引和目录项等特殊标记。
- 宏和模板——宏和模板通常不会被导入或导出。你可能需要对文档进行格式化以使其看起来一致。
- 公式——长且复杂的公式可能会出现问题。特别注意绝对单元引用和依赖于计算顺序的操作。
- 特殊功能——数据验证、帮助注释、工作表保护和自定义函数可能无法正确导入。

虽然 `Star Office` 对 `MS Word` 和 `Excel` 文件有非常好的支持，但它对其他文字处理器或电子表格格式几乎没有支持。它不支持 `WordPerfect` 或 `Quattro Pro` 格式，并且它将 `Lotus 123` 文件作为文字文档打开，如果你想编辑 `Lotus` 文件，这并没什么用。如果你想在 `Star Office` 中导入这些文件之一，必须先将其保存为 `MS Office`、`RTF`、`HTML` 或 `DIF` 格式。

## 6.11 财务程序

跟踪个人财务是家用电脑最常用的用途之一，这就是为什么像 `Intuit` 的 `Quick` 和 `Microsoft Money` 这样的个人财务程序是家庭用户最常用的程序。虽然 Linux 上没有像这两个程序一样功能丰富的程序，但 `Moneydance` 和 `GnuCash` 补充了它们的许多功能。

`Moneydance` 是目前功能最丰富的 Linux 财务程序。它支持以下功能：

- 交易自动完成。
- 交易搜索。
- 支票打印（普通支票或带存根的支票）。
- 多货币（你可以定义自己的！）。
- 支持多账户和双式记账。
- 易用的支票簿式界面，带有许多快捷键。
- 自定义 3D 和 2D 图形，具有导入或导出到文件的能力。
- 报告生成器，具有导出到 `HTML` 和打印的功能。
- `QIF`（`Quicken` 交换格式）文件的导入和导出。
- 随着你的工作更新已结算余额与实际账户余额。
- 多语言（意大利语、德语、法语、巴西/葡萄牙语，英国和美国英语）以及日期/数字格式。
- 计划交易和提醒。
- 用于简化支票簿平衡的对账工具。
- 有可用升级时的自动通知。
- 广泛的交易排序选项。
- 支持每笔交易多个日期。
- 支持拆分交易。
- 货币字段支持数学表达式和自动货币转换。

还有几个正在开发的功能，包括：

- 在线银行。
- 预算管理和跟踪。
- 股票组合和投资管理。
- 在线组合更新。

`Moneydance` 使用 `Java` 编写，需要 `Java` 开发工具包 (`JDK`) 运行。它不是 `GPL` 程序且花费 50 美元。它可以在 Linux、Windows、macOS 和大多数 UNIX 版本下运行。然而，`GnuCash` 是免费且符合 `GPL` 的。由新的开源财务程序 `GnoCash` 和 `X-Account` 合并。虽然它没有 `Moneydance` 那么，但它正在快速发展。

- 易用的界面——如果你使用支票簿后面的寄存器，你可以使用 `Gnucash`。直接在寄存器中输入，在字段之间切换，并使用快速填充自动完成交易。
- 对账窗口带有运行中的已对账和已结算余额，对账变得简单。
- 股票/共同基金组合——单独跟踪股票（每个账户一个）或在账户组合中跟踪（一组可以一起显示的账户）。
- 多货币和货币交易——支持多种货币并可以买卖（交易）。当启用双式记账时，账户之间的货币移动是完全平衡的。（多货币支持的某些方面尚未完全实现。）
- 快速文件会自动合并以消除重复交易。
- 报告——显示负债表、损益表、组合估值，或将其打印为 `HTML`。
- 会计科目——主账户可以有一个下级明细账户层次。这允许将类似的账户类型（例如现金、银行、股票）分组在一个主账户（例如资产）之下。
- 拆分交易——单笔交易可以分成几部分，以记录税费、费用和其他复合分录。
- 双式记账——启用时，每笔交易必须借一个账户并贷另一个账户，金额相等。这确保了“账平”，或者收入和支出之间的差额恰好等于所有资产之和，无论它们是现金。

`GnuCash` 程序和文档可以在 `gnucash.org` 找到。

# 第 12 章 图形程序

使用图形的能力变得越来越重要。所有的办公套件都有不同程度的图形功能，但有时你需要更多。独立的图形程序分为两种：照片编辑器和绘图程序。

照片编辑器允许你处理照片和图像。这些程序需要艺术家熟悉的许多工具，包括画笔、笔和喷笔。最流行的程序是 `Adobe Photoshop`。开源程序 `GNU Image Manipulation Program` (`GIMP`) 为 Linux 相同的功能，尽管它的界面没有那么直观，Linux 和 Windows 版本都可以从 `gimp.org` 下载。

![](img/a1ad58e4259f15e8b2826ecf57a28362_87_0.png)



图 6.9 `Gimp` 为 Linux 提供了类似于 `Photoshop` 的功能。也有 Windows 版本。

绘图程序的目的与照片编辑器不同。绘图程序旨在创建图表、图形和演示。两个流行的程序是 `Microsoft Visio` 和 `Corel Draw`。幸运的是，`Corel Draw` 支持 Linux、Macintosh 和 Windows。

`Blender` 和 `POV-Ray` 是适用于 Linux、UNIX 和 Windows 的 3D 渲染工具。`Blender` 是一个用于建模、渲染和动画的集成套件。它基于数字动画工作室内部开发的工具。由于 `Blender` 是免费的，它是在不花费大量资金的情况下尝试数字渲染和动画的好方法（http://www.neoge.nl/）。

`POV-Ray` 是目前最好的渲染工具之一。它使用描述要渲染对象的文本文件。它有许多内置函数，如纹理、形状和颜色。它没有建模工具，但 `POV-Ray` 网站链接了几个共享软件和商业建模工具。和 `Blender` 一样，它是受版权保护的免费软件。与 `Blender` 不同，源代码也可以 http://www.povray.org 获取。

## 6.12.1 图形转换

`GIMP`、`Core Draw`、`Photoshop` 以及大多数图形程序都可以打开并转换许多不同的文件格式。然而，有时你会遇到你的程序不支持的图形文件。其他时候，你有大量文件需要转换，而打开并转换每一个文件将花费几天时间。对于这些情况，你需要一个图形转换程序。

图形转换程序有两种类型：查看器（viewers）和批量转换器（bulk converters）。查看器允许你查看图形并将其保存为另一种格式。这允许你在转换之前检查并调整文件的特性的。批量转换器通常不允许你在转换之前查看图形，但它能一次转换许多文件。

Windows 平台上有几十种免费和共享的图形转换程序。关于各种程序的良好列表，可以在 http://www.softseek.com/Graphics_and_Drawing/Graphics_Conversion_and_Optimization/ 找到。

Linux 下的图形转换器并不多。市场上最好的查看器之一捆绑在 Linux 发行版中。该程序费用为 25 美元，40 美元还额外包含印刷版手册。该程序、源代码和文档可以在 http://www.trilon.com/xv/xv.html 找到。

对于批量转换，可以使用免费工具 `NetPBM`。`NetPBM` 不是一个单一程序，而是由约 180 个命令行程序组成的集合。不同格式之间的转换有单独程序。例如，要将 `PNG`（一种在 UNIX 系统上流行的图形格式）转换为 `JPEG`（一种创建极小图形文件的图形格式），请使用以下命令：

```
for i in *.png; do pngtopnm |pmtojpeg >basename $i .png.jpg; done
```

让我们拆解该命令：

- `for i in *.png;`—这选择了所有的 PNG 文件。
- `do pngtopnm`—这是将 PNG 转换为 PNM 的程序。PNM 是 `NetPBM` 使用的中间格式。
- `nmtojpeg`—此程序将 PNG 转换为 JPEG。
- `'>basename $i .png.jpg;`—这会创建一个与 `.PNG` 文件同名的 JPG 文件。
- `done`—完成后退出程序。

`NetPBM` 的语法相当复杂，但它非常适合批量转换。该程序和文档可以在此处找到：http://netpbm.sourceforge.net/projects/netpbm。

`ImageMagick` 有一组非常实用的转换工具，可以在 http://www.izards.dupont.com/cristy/ImageMagick.html 获取。

## 6.13 最后的结论

Linux 远不如 Windows 桌面那样流行，但桌面工具的快速发展正在改变。大多数桌面应用程序现在都有相应的 Linux 应用程序。Linux 不具备的功能正在迅速被免费和商业应用程序填补。Linux 的低成本、稳定性和低硬件要求使其不仅成为 Windows 的可行替代品，有时甚至是更好的选择。

## 6.14 结论

那么，哪种 Linux 办公套件最好？答案显然取决于你的需求。如果与 `MS Office` 的兼容性是首要任务，目前没有什么能击败 `WP Office`。`WP Office` 也是 Linux 上可用功能最丰富的办公套件。

对于免费办公套件，`Star Office` 是很难比拟的。它拥有一套良好的功能，并与 `Word` 和 `Excel` 文档兼容。

`Applixware` 和 `WordPerfect 8` 是低端系统的明确选择，因为它们在带有 32MB 内存的 486 处理器上运行良好。

开源办公套件 `Koffice` 和 `Gnome Office` 尚未准备好供日常使用，但它们很快就会像 Linux 挑战 Windows 一样挑战商业产品。

尽管它们显示出前景，但要说 `WBS` 是否能挑战独立应用程序还为时尚早。

# 第 7 章 数据库

数据库对于存储业务使用的信息至关重要。传统和在线业务都使用数据库来跟踪订单、商品和客户。由于它们对业务如此重要，因此有几十种商业和免费的数据库以及数据库插件并不令人意外。

最流行的商业数据库同时适用于 Linux 和 Windows，以及几个版本的 UNIX。许多数据库也适用于流行的的主机和微型计算机。一些较受欢迎的商业数据库包括：

- `DB2`—IBM 的重型数据库，最初运行在 IBM 主机和微型计算机上。它也适用于 Linux、Windows、Os2 和大多数版本的 UNIX (http://www-4.ibm.com/software/data/db2/udb)。
- `Ingress`—这是来自 Computer Associates 的一个数据库，它是仅次于微软的第二大软件公司 (http://www.cai.com/products/ingress.html)。
- `Oracle`—最流行的商业数据库之一，适用于几乎所有的计算机平台 (http://www.oracle.com/)。
- `Informix`—提供数据库的免费开发版本和商业版本 (http://www.informix.com/)。
- `Sybase`—其旗舰数据库 Adaptive Server Enterprise 有作为一个不支持的免费版本提供给 Linux (http://www.sybase.com/adaptiveserver/ )。
- `Adabas`—这是第一个适用于 Linux 的商业数据库。它源自 Adabas 主机数据库。它捆绑在许多 Linux 发行版中，包括 Caldera (http://www.caldera.com/) 和 SuSE (http://www.suse.de/)。

有两种流行的开源数据库：

- `MySQL`—一个对 Linux 用户免费，对 Windows 用户收费 200 美元。无论哪种，它都是市场上最便宜的数据库之一。它也有商业支持 (www.mysql.com)。
- `PostgreSQL`—这个流行的 UNIX 数据库在功能上可以竞争许多商业数据库。它是免费提供的，并有商业支持 (http://www.postgresql.org/)。

有两个常用的 Windows 专用数据库：

- `Access`—该数据库捆绑在 Microsoft Office 中。它旨在作为轻级数据库，作为前端数据库非常流行。
- `SQL Server`—这是微软的重型数据库。它在基于微软的网络中非常流行。

虽然这个列表并不全面，但涵盖了一些流行的数据库。

## 7.1 使用数据库

所有主要的数据库都支持结构化查询语言 (`SQL`)。`SQL` 是国际标准组织 (`ISO`) 的标准，提供了一种操作数据库的统一语言。尽管如此，所有数据库都使用不同的 SQL 变体，某些对 ISO 标准的支持更好。

`SQL` 拥有创建数据库、添加数据和检索数据的命令。`Create` 用于创建和更改数据库表。命令有：

- `Create Table`—创建表。
- `Drop Table`—删除表。
- `Alter Table`—修改表。
- `Insert`—向表中插入数据。
- `Select`—从表中检索数据。

当然，`SQL` 中还有许多其他命令和子命令。此外，每个数据库都有自己的命令语法。如果你认真对待数据库，请买一本关于你计划使用的数据库的书。

## 7.3 连接数据库

微软的开放数据库连接 (`ODBC`) 软件是连接到或从微软数据库的最常用方法。许多数据库和 Web 开发工具都内置了 `ODBC` 连接功能。此外还有许多独立的 `ODBC` 程序，正如下一节列出的那些。

## 7.4 ODBC

`ODBC` 由服务器软件和客户端软件组成。服务器软件运行在数据库端，客户端运行在访问数据库的机器上。服务器通常作为 `NT` 服务运行，并在控制面板中配置。客户端既可以是 `NT` 服务，也可以独立程序。

将服务器与客户端分离使得 `ODBC` 成为一个良好的跨平台解决方案，但它让故障排除变得更加困难。`ODBC` 提供的错误往往相当晦涩，并不能真正告诉你问题所在。很难判断错误是由客户端还是服务器引起的。



锁定防止两个用户同时更新同一条信息。常用的锁定有两种类型：记录锁定和表锁定。记录锁定只锁定正在更新的单条记录。表锁定则锁定该记录所在的整个表。表锁定允许一次只有一个一个用户更新一张表。记录锁定可以允许多个用户更新一张表，但它的速度比表锁定慢。

支持和价格是并存的。依赖数据库的大型组织愿意为 IBM 或 Oracle 等大公司的数据库支付每用户高达数千美元。数据库本身和支持的成本远低于数据库崩溃的成本。个人和免费数据库没有同等水平的支持。

所有商业数据库（包括 Microsoft SQL Server）都支持事务、热备份和锁定。它们还提供广泛的支持以及与之匹配的定价。

所有免费的开源数据库（如 PostgreSQL）都拥有商业数据库的所有主要功能。也可以通过额外付费获得支持。

MySQL 是另一个流行的开源数据库。它的设计与 PostgreSQL 和商业数据库不同。MySQL 不支持事务，并使用表锁定而不是记录锁定。这使得 MySQL 与其他数据库相比，读取和更新表的速度要快得多。对于经常读取但很少更新的数据库，MySQL 是一个很好的选择。它是 Web 数据库的流行选择，因为许多 Web 数据库主要用于读取数据。

MySQL 也有其缺点。多个用户可以同时进行更新。而且没有事务，因此如果在更新表时发生错误，没有简单的方法恢复数据。这些局限性可以通过小表和频繁备份来部分克服。

虽然 Windows 包含了 ODBC 驱动，但 OpenLink Software 为 UNIX 平台制作了驱动。可以从 http://www.open-linksw.com/ 下载一个完全运行的演示版。商业版的价格 675 美元起。

OpenLink 还有一个名为 Virtuoso 的程序，它使用中间文件格式连接数据库。它提供 Linux 和 Windows NT 版本。Virtuoso 599 美元起。

FXML 还提供一个免费的开源 ODBC 程序。它包含一个 Windows NT 服务器以及适用于 Windows、Linux 和 UNIX 的客户端（http://odbc.linux-ave.com/）。FXML ODBC 服务器目前在 Windows NT 下运行。可以使用注册表编辑器进行轻松配置。可以配置的设置包括使用的端口、最大线程和连接数、允许连接的主机以及超时时间。如果你需要进一步的自定义，可以获取源码并使用 Microsoft C++ 6.0 进行编译。

FXML ODBC 带有适用于 COM（Microsoft C++ 使用）、Perl 和 PHP（用于 Web 页面）以及 C++（用于 Linux 和 UNIX）的客户端。如果这些不够，可以使用任何支持 TCP/IP 和 XML 的 ODBC 接口。

实现此目的的另一种廉价方法是使用免费数据库 MySQL 及其 MyODBC 驱动。首先，从 MySQL 网站 www.mysql.org 下载 Linux 版的 MySQL 和 Windows 版的 MyODBC。在 Linux 机器上进行安装和设置。一旦数据导入 MySQL，你就可以利用 PHP 对 MySQL 的支持支持来这些数据。

要在 Windows 机器上安装 MyODBC 驱动，请配置 ODBC 驱动连接到 Linux 机器上的 MySQL 数据库。打开 Access 并右键点击数据库。选择外部数据 -> 链接表。在弹出的框中选择 ODBC，然后选择 MyODBC 链接的。你现在可以编辑数据并创建查询、表单和报告，并将它们导出到 MySQL 数据库中。当将 Access 表导出到 MySQL 时，Access 表和 MySQL 表都必须有主键。如果使用 MySQL 对表进行了任何更改，你必须重新链接表。要在你的 Windows 机器上执行此操作，转到开始 -> 程序 -> 工具 -> 加载项 -> 链接表管理器。获取表的 ODBC DSN 并选择要重新链接的表。

## 8.1 游戏

让我们面对现实，对于家庭用户来说，拥有许多酷炫的游戏是使用电脑的一个极佳理由。Linux 的许多早期采用者往往是活跃的游戏玩家。正如 Redhat Linux 首席执行官 Bob Young 所说：“为 Linux 操作系统设计的游戏对于促进自由软件行业的发展至关重要”（http://www.techweb.com/wire/story/TWB199902S0014）。

目前，Windows 9x 是 PC 游戏平台的王者。这主要是由于 Windows 9x 占据了约 80% 的 PC 市场份额。

### 8.1.1 Mesa 与 OpenGL

Mesa 与 OpenGL 非常相似。它们相似到以至于大多数为 OpenGL 编写的应用程序只需少量修改或不修改即可使用 Mesa。许多开源程序（包括 WINE）都使用了 Mesa 库。

Mesa 支持许多流行的 3-D 显卡，包括 3dfx Voodoo、NVIDIA、Matrox MGA-G200 和 MGA-G400、ATI RagePro、Intel i810、NVIDIA Riva、S3 VirGE 以及基于 DRI 的硬件。信息和二进制文件可以在 http://mesa3d.sourceforge.net 获取。

### 8.1.2 id Software

Loki 目前正在将游戏推向 Linux 领域，但他们绝并非先行。id Software 是首批将其游戏移植到 Linux 的商业游戏公司之一。这并不令人意外，因为他们早期的游戏是在 Next 系统上开发的，该系统使用某种版本的 UNIX。

id Software 是由三位游戏开发者——John Carmack、Adrian Carmack 和 John Romero 在创作了《沃提科人入侵》（Invasion of the Vorticors）后离开 Softdisk 出版公司创立的。在工作一年多后，他们于 1992 年发布了第一款游戏《德意志堡垒3D》（Wolfenstein 3D）。这是一款流行的 FPS（第一人称射击游戏），你可以从纳粹手中营救一名女性——3-D 图形、快速射击以及屏幕底部无处不在的武器。

1993 年，id 发布了《毁灭战士》（Doom），这可能是史上最流行的游戏。它解决了只有固定天花板高度的问题，通过允许玩家抬头向下，赋予了游戏 3-D 感。它还将地形更改为地狱般的走廊和恶魔怪物。随后他们在 1994 年推出了了《毁灭战士 2》（Doom II）。

1996 年发生了两个重要事件。id 发布了《雷神之》（Quake），这是《毁灭战士》和《德意志堡垒》的续作。1999 年初，id Software 发布了《雷神之》的源代码。他们还发布了两款基于《毁灭战士》的流行游戏的源代码：《异教圣》（Heretic）和《魔界》（Hexen）。1999 年，他们以 GPL 协议重新发布了《毁灭战士》，这允许他人合法地销售基于《毁灭战士》源代码的游戏。

id 通过发布《雷神之 2》和《雷神之 3》继续改进《雷神之》。他们不仅改进了图形，还改进了游戏性。在单机模式下，敌人会站着，只有在你靠近时才会攻击。而在《雷神之》中，敌人可以躲避子弹并进攻。

当《雷神之 3》于 1999 年初发布时，这是商业游戏公司首次同时发布 DOS/Windows、Linux 和 Macintosh 版本的软件（www.idsoftware.com）。

### 8.1.3 虚拟竞技

id Software 并不是 Linux 上唯一的 FPS 游戏，尽管《虚拟竞技》（Unreal Tournament，UT）提供了一个不受支持的 Linux 版本。UT 是目前 FPS 游戏的尖端。系统配置要求 200MHz 处理器和 32MB 内存。实际上，你至少需要 400MHz 处理器、64MB 或更大的内存以及一张兼容 3dfx 的显卡。其他 3-D 显卡不受支持。

要安装 UT，你必须购买 Windows 版本，并从 http://fileplanet.com/index.asp?search=Linux+Unreal+Tournament&file=32058 下载 Linux 二进制文件。下载完成后，按照以下方式解压程序：

```
gunzip UT-Linux-400A.tar.gz
tar xvf UT-Linux-400A.tar
```

请注意 UT 需要大约 500MB 的空闲空间。你还需要拥有 libxml 和 libglade。如果你还没有安装这些库，它们包含在下载包中。此外，不要以 root 身份安装游戏，否则只有 root 能够玩游戏。此外，确保游戏 CD-ROM 已挂载为 `/mnt/cdrom`，否则安装程序将无法运行。

安装目录为 UT-Linux-400A。在该目录下有安装脚本 `setup.sh`。在 X11 中运行此程序应该会启动设置程序。如果设置脚本不起作用，你可以输入 `./setup.data/bin/x86-glibc-2.1/setup.gtk` 来启动它。



安装后，你可以通过 `UnrealTournament.ini` 和 `User.ini` 修改设置。修改这些文件的说明位于安装目录下的 README 文件中。Linux 版本的一个故障是它无法与 Enlightenment 窗口管理器配合。由于它是 Gnome 的默认窗口管理器，在使用 UT 时最好使用 KDE 或 FVWM。切换方法的详情请后文窗口管理器的章节。

UT 的游戏具有高度配置性。你可以与其他玩家对战，也可以在单机模式下与可配置的“机器人”对抗。你可以配置机器人的数量和技能。

UT 有 60 关，互联网上有更多供下载。还有许多 UT 粉丝和服务器网站。一个很好的起点是 http://www.unreal.com/index2.html。

该游戏还有几种变体：死亡赛（Death Match）、夺旗赛（CTF）、占领（Domination）、最后幸存者（Last Standing）和突击（Assault）。死亡赛是多人 FPS 游戏的经典玩法。每次击杀都会得分，每次被杀死都会扣分。得分最高的人获胜。夺旗赛正如其名：第一个夺到敌人旗帜的人获胜。占领是另一种变体，由团队控制地图。当一个团队控制了地图时，它就会得分。最后幸存者与死亡赛类似，但每个玩家有有限的生命。突击与夺旗赛类似，但完成攻击时间最短的团队获胜。

## 8.2 游戏服务器与额外内容

许多来自 世纪 80 年代的经典游戏在 Linux 下获得了新生命。这里有适用于 Amiga、Genesis、Coleco、Commodore、Atari、Gameboy 以及大多数原始街机系统的模拟器。

多街机模拟器（MAME）模拟了 2000 多款游戏，包括大多数流行的街机游戏。MAME 的 Linux 版本称为 XMAME。程序和文档可以在 http://x.mame.net/ 和 http://www.vintagegaming.com/mame.shtml 获取。XMAME 可用的游戏处于不同的开发阶段。有关游戏列表及其开发状态，请访问 http://x.mame.net/down-load/gamelist.mame。

Gameboy 也没有被落下。这些游戏看起来和原版一样，只是屏幕更清晰且是彩色的（http://www.vintagegaming.com/）。

# LINUX 桌面

X11 只是 Linux 桌面的基础部分。你还需要一个窗口管理器来处理菜单、图标和其他桌面功能。与只有一个单一界面的 Windows 不同，Linux 在桌面界面（即窗口管理器）方面有许多选择。最流行的是 FVWM、KDE 和 Gnome，因为它们与其他流行的桌面一样，它们都是不错的选择。

FVWM（http://www.fwwm.org/）代表 F Virtual Windows Manager（F 虚拟窗口管理器）。它非常稳定，且占用的内存较少。AfterStep（http://www.afterstep.org/）是 FVWM 的变体，在大多数 Red Hat 发行版中。对于低端系统，FVWM 不像其他那样友好或易于配置，尽管它比其他软件小得多也快得多。

如果你需要一个轻量级的窗口管理器，可以尝试 tw。它看起来并不漂亮，但非常节省资源（http://www.visi.com/~hawked/vwm.html）。

K 桌面环境 (KDE) 项目启动于 1996 年，旨在为 Linux 提供一个完整的集成桌面环境 (IDE)。它包含了窗口管理器、文件管理器、帮助系统和实用程序。它是第一个旨在为 Linux 提供现代图形界面 (GUI) 的程序。KDE 目前是 Linux 发行版的默认界面（http://www.kde.org/）。

GNU 对象模型环境，或 GNOME（http://www.gnome.org/）的启动是因为 KDE 使用来自 Troll Tech（http://www.troll.com/）的 Qt 库。Qt 库是一个商业库，不受 GNU 公共许可证 (GPL) 保护。GNOME 的启动是因为 Linux 社区的许多担心在 GPL 软件中包含此类产品会危及 GPL。虽然 Troll Tech 允许在 KDE 中免费使用 Qt 库，但 GNOME 提供了一个替代方案，以防情况发生变化。

尽管如此，GNOME 提供了目前 Linux 最丰富、可配置的桌面。GNOME 甚至允许你更改窗口管理器来改变桌面的视觉效果和感受。虽然 GNOME 的默认窗口管理器是 Enlightenment（http://www.enlightenment.org/），但还有许多其他窗口管理器可用（http://linux-directory.com/links/pages/WindowsManagers/）。

虽然 GNOME 比 FVWM 或 KDE 更易配置，但它消耗的资源也更多，使其成为低端系统的糟糕选择。它的运行时间也比 FVWM 或 KDE 少，因此调试的机会也较少。

## 9.1 切换桌面

使用一个名为 switchdesk 的图形化工具尝试不同的桌面是容易的，它可以允许轻松地切换桌面。

![](img/a1ad58e4259f15e8b2826ecf57a28362_103_0.png)

图 9.1 Switchdesk 更改默认桌面。

如你所见，switchdesk 提供了 Gnome、KDE 和 FVWM。只需选择其中一个，即可更改所有显示器的桌面。点击“仅应用于当前 (Change only applies to current)”框，可以仅在当前显示器上显示桌面。由于 Linux 允许你加载多个显示器，你可以同时加载多个桌面！

一旦选定了桌面，重启 X11，新桌面就会生效。如果你使用图形化登录，则不需要使用 switchdesk——只需在登录时选择窗口管理器即可。

## 9.2 配置桌面

在 KDE 或 Gnome 的桌面上点击右键会弹出一个菜单，其中包含更改桌面设置的选项（FVWM 不支持此项）。下面是更改 Gnome 和 KDE 设置的插图（参见图 9.2 和 9.3）。

![](img/a1ad58e4259f15e8b2826ecf57a28362_104_0.png)

图 9.2 在 KDE 中更改桌面设置。

![](img/a1ad58e4259f15e8b2826ecf57a28362_105_0.png)

图 9.3 在 Gnome 中更改桌面设置。

## 9.3 主题

所有的桌面管理器都允许对桌面进行大量的自定义化。例如，你可以下载主题，这些是预配置的桌面。获取这些主题的好地方是 Themes.org（http://www.themes.org/）。

要寻找你的桌面，请前往你窗口管理器的链接。FVWM 使用 Window Maker，KDE 使用 KDE，Gnome 使用 GTK。

从这里你可以浏览不同主题的截图，并下载任何符合你口味的主题。主题下载后，必须进行安装。一旦下载了主题，它看起来会像 `<theme name>.tar.gz`。

对于 FVWM，将主题拷贝到 WindowMaker 目录下的主题文件中：

```bash
cp <theme name>.tar.gz ~GNestep/Library/WindowMaker
```

接下来，进入 Window Maker 目录并解压文件：

```bash
cd ~GNestep/Library/WindowMaker
gunzip <theme name>.tar.gz
tar xvf <theme name>.tar
```

在 WindowMaker 中，在桌面上点击右键，进入 Appearance (外观) -> Themes (主题)，并选择你刚刚安装的 Gnome 下的主题。

在 Gnome 下安装主题要简单得多。首先，转到左下角并选择 Settings (设置) -> Theme (主题)。这将打开控制中心。由于 Gnome 的可定制性最高，因此有很多主题可用。要在 Gnome 下安装一个新主题，只需点击 New (新建) 并选择该文件。

![](img/a1ad58e4259f15e8b2826ecf57a28362_106_0.png)

图 9.4 在 Gnome 中设置主题。

在 KDE 下安装主题，首先转到左下角并选择 Settings (设置) -> Theme (主题)。这将打开主题管理器。一旦选择了主题，点击 OK (确定) 应用主题。

![](img/a1ad58e4259f15e8b2826ecf57a28362_107_0.png)

图 9.5 打开主题管理器。

![](img/a1ad58e4259f15e8b2826ecf57a28362_108_0.png)

图 9.6 在 KDE 中设置主题。

要在 KDE 中创建自己的主题，点击 Create (创建) 并提供作者、电子邮件和描述。如果你想与他人分享你的主题，使用 Save (保存) 功能。默认文件名将为 `<theme name>.tar.gz`。

虽然 Linux 还不如 Windows，但它是目前最热门的领域之一。Linux 未来可能会追赶甚至超越 Windows。

## 10 通过网络运行应用程序

### 10.1 X-Windows



# X-Windows 版本 11 (X11)

X-Windows 版本 11 (`X11`) 是 Linux 和 UNIX 的标准图形界面。它包含两个部分：客户端和服务器。

客户端和服务器通常运行在同一台机器上，这允许 Linux 本地运行。它们也可以运行在不同的机器上，允许你在一台机器上运行并在另一台机器上显示。客户端运行在程序的机器上，服务器运行在显示器的机器上。`X11` 在客户端和服务器之间分配负载。客户端运行应用程序，服务器处理图形。这减轻了服务器的负担，但也增加了网络流量。这在计算早期是为了让便宜的工作站运行在昂贵的服务器上。

## 10.1.1 Linux 上的 X-Windows

`X11` 几乎每个现代 Linux 发行版。通常在安装 Linux 时配置。配置 `X11` 需要支持的显卡、显示器的型号和规格以及鼠标类型。要确定你的显卡是否支持，请访问 http://www.xfree86.org/cardlist.html。显示器规格列在随附的文档中。如果你没有文档，显示器列在 http://ms.ha.md.us/~hawks/hardware/monitor.html。水平同步 (`Hsync`)、垂直同步 (`Vsync`) 和最大分辨率 (`Max Res`) 是最重要的设置。你的用户手册应该会有关于安装和配置 `X11` 的详细说明。配置说明的简要版本如下。

要配置 `X11`，请使用 `Xconfigurator`。

# 第 10 章 • 通过网络运行应用程序

手动配置驱动程序和视频显存。接下来，选择你拥有的显示器。如果列表中没有列你的显示器，请选择“自定义”(`Custom`)并手动输入 `Hsync`、`Vsync` 和最大分辨率 (`Max Res`)。

`Xconfig` 将探测分辨率并推荐一个分辨率。`X11` 将启动。如果屏幕无法访问，你始终可以通过按下 `<CTRL><ALT><BACKSPACE>` 重新启动 `X11` 并运行 `Xconfigurator`。

一旦显卡配置完成，唯一需要配置的就是鼠标。列出了几个品牌，以及通用的串口端口鼠标和 PS2 端口鼠标。你还可以选择模拟三键鼠标，它通过在双键鼠标上按下两个按键来模拟三键鼠标的中间键。使用三键鼠标是一个好主意，因为 Linux 使用中间键进行剪切和粘贴操作。

在在远程主机上运行 `X11` 之前，你必须将其添加到服务器的 `xhost` 列表中。要这样做，请输入 `xhost <机器名称或 IP 地址>`。你可以通过输入 `xhost +` 来启用连接。

一旦配置好 `X11`，可以使用启动脚本本地启动。要在另一台机器上启动 `X11` 会话，输入 `xinit` 后跟 `machine_name`，然后是以 `(0)` 开头的会话。例如，要在 `Server1` 上启动 0，输入：

```
xinit server:0
```

对于任何高级 `X11` 问题，请咨询良好的手册或你的 Linux 发行版的技术支持。解决 `X11` 问题的良好新闻组是：news.comp.windows.x.i38unix。记住在线寻求帮助的规则：阅读手册并具体地描述问题。

大多数较新的发行版使用 `xdm` 或类似的程序（如 `gdm`）来管理 `X11`。如果你的系统有图形登录界面，说明你正在使用 `xdm`。

`xdm` 使用主目录下的隐藏文件 `.Authority` 来为 `X11` 会话提供安全保护。如果你在远程使用 `X11`，你必须将 `.Authority` 复制到远程机器，或者使用 `xhost` 将该机器添加到访问列表（见上文）。

## 10.1.2 Microsoft Windows 上的 X-Windows

`X11` 包含在 Linux 和 UNIX 中，但对于 Microsoft Windows 来说，它是一个附加程序。许多软件包可以让 Windows 充当 `X11` 服务器，范围从免费产品到商业产品不等。

最便宜的程序是 `MI/X`，售价为 25 美元。它为 Microsoft Windows 提供了基本的 `X11` 服务器能力，但它只支持 `X11` 的第 5 版本，而 Linux 目前支持第 6 版本。这意味着许多较新的程序在 `MI/X` 上无法正常显示。

Windows 还有许多其他 `X11` 服务器，价格最高达 600 美元。在 http://www.microimages.com/mix/prices.htm 上有一份非常完整的列表。

## 10.2 Citrix WinFrame

### 10.2.1 服务器概述

`Citrix WinFrame` 是一款让 Windows NT 能够像 X-Windows 一样运行的产品。它允许多个用户在 NT 服务器上启动会话，并在工作站上显示该会话。

与其他 Windows 产品不同，`WinFrame` 为每个用户提供一个独立的会话。大多数其他 Windows 产品（如 `PC Anywhere` 或 `VNC`）允许多个用户登录，但不支持多个会话。换句话说，多个用户可以登录，但看到的都是同一个屏幕，而 `Citrix WinFrame` 则不同。

`Microsoft Terminal Server` 是从 Citrix 授权的，提供了与 `Citrix WinFrame` 相同的功能。尽管产品之间存在细微差异，但我们将讨论 `Citrix WinFrame`，因为 Citrix 也制作了 Linux 版本，它允许 Linux 机器在 NT 服务器上运行 Windows 软件并在 Linux 机器上显示。

由于应用程序完全运行在服务器上，请确保服务器能够处理这些负载。与 `X-Windows` 不同，所有的处理都是在服务器上完成的。这减轻了网络压力，但增加了服务器的压力。

我们将从确定处理客户端的最小配置开始。记住，这是最小配置；越多越好。

首先，数出用户数量并将用户分为普通用户和高级用户。普通用户一次只需要使用一个程序，而高级用户会同时使用几个程序。然后，为 NT 和 `WinFrame` 分配 48MB 内存，外为每个普通用户分配 10MB，为每个高级用户分配 16MB。

例如，如果你有 20 个普通用户和 10 个高级用户，你为普通用户需要 200MB（20 × 10），为高级用户需要 160MB（10 × 16），外加 NT 和 `WinFrame` 的 48MB。

CPU 速度也有差异。建议每个 CPU 不要承载超过约 50 个用户。如果你有超过 50 个用户，请购买一台带有多个 CPU（SMP）的 PC，或者增加一台 PC。如果你正在运行多个 `WinFrame` 服务器，Citrix 提供了一款可用的负载均衡软件，价格为 1,495 美元。

记住，`X11` 和 `WinFrame` 都需要大量的带宽。虽然 10MB 的网络对于非常小的网络可以运行，但实际上需要 100MB 的网络。如果带宽不足，请考虑在交换网络上安装多台 NT 服务器。

### 10.2.2 客户端配置

对于客户端，你有三个选择：你可以使用独立于 Citrix 的客户端架构 (`ICA`) 客户端、`Java` 客户端或 `X-Windows`。

`ICA` 客户端允许使用 `Metaframe` 的完整功能。要安装它，只需解压客户端文件 `linux.tar`。接下来，运行 `setup`。默认情况下，由于原文存在部分重复和乱码，已按逻辑处理。

### 10.3 VNC

`VNC` 由两个部分组成：一个在某机器上运行程序的服务器，以及一个在另一台机器上显示程序的查看器。它适用于 Linux、`Windows` 以及大多数其他操作系统。还有适用于 `Windows CE` 和 `Java` 的查看器。该查看器非常小（Win32 查看器仅为 150k），且不需要安装，这意味着它可以轻松地从软盘运行！

不过，服务器之间存在一些差异。Linux 和 UNIX 服务器是多用户系统的。这意味着多台机器可以在服务器上开启一个独立的会话。然而，Windows 服务器只允许单个会话。不过，它允许多个用户登录同一个会话。Windows 并不是一个真正的多用户操作系统。如果你需要打开多个会话，请使用 `Citrix WinFrame`。

`VNC` 优于 `X11` 的优点是查看器中不存储任何状态。这是一种形象的说法，意味着如果你丢失连接，可以重新连接而不会丢失任何内容。这对于调制解器连接和不可靠的网络来说，简直是天赐的礼物。

`VNC` 使用的带宽比 `X11` 少。有几个设置可以优化 `VNC` 在低高带宽连接下的表现，将在后文中讨论。一个经过适当优化的 `VNC` 会话甚至在拨号连接上也能良好运行！

### 10.3.1 为 Linux 安装 VNC 服务器

要安装 `VNC`，请从 http://www.uk.research.att.com/vnc 下载软件包。Linux 的安装包包含四个程序：

- `Vncviewer`——这是用于 `X-Windows` 的 `VNC` 查看器或客户端程序。
- `Vncserver`——这是一个封装脚本，使得启动 `X-Windows VNC` 服务器（即桌面）变得更加方便。它用 Perl 编写，因此使用该脚本时需要安装 Perl 环境。
- `Vncpasswd`——此程序允许你更改访问 X Windows VNC 桌面的密码。当你第一次启动 VNC 服务器时，`vncserver` 脚本会使用此程序。



- `Xvnc`——这是 X-Windows VNC 服务器。它既是一个 X-Windows 服务器，也是一个 VNC 服务器。你通常使用 `vncserver` 来启动 `Xvnc`。

将这些文件复制到 `/usr/local/bin` 就可以开始工作了。`vncserver` 是一个用 Perl 编写的脚本文件，如果需要可以进行编辑。这只有在软件包没有放在标准位置时才需要。例如，如果你的 Perl 程序不在 `/usr/bin` 目录，你可能需要编辑第一行 `/usr/bin/perl`。你可能还需要在标记部分恰当地地添加字体和颜色数据库路径。添加路径和颜色数据库。

完成后，通过输入 `vncserver` 启动 VNC 服务器。第一次运行时，系统会提示输入密码。这是在查看器上必须输入的密码。你稍后可以使用 `vncpasswd` 程序更改密码。

你可以根据需要打开任何 VNC 服务器会话。默认情况下，它会获取第一个可用 X11 会话。X11 的第一个显示是 0，因此第一个 VNC 服务器会话是 1。

## 10.3 VNC

你也可以指定要使用的会话号。例如，要使用会话 2，输入 `vncserver :2`。你可以通过输入 `vncserver -kill <:session number>` 来杀死服务器。

VNC 服务器有几个命令行参数。通过输入 `vncserver -help` 可以查看。以下是参数的含义（来自 VNC 文档）：

- `name <name>`—每个桌面都有一个名称，查看器可以显示该名称。默认是 'x'，但你可以通过此选项更改它。
- `geometry <width><height>`—指定要创建的桌面尺寸。默认是 `1024x768`。
- `depth <depth>`—指定要创建的桌面的像素深度（位）。默认是 `8`。
- `pixelformat <format>`—指定服务器使用的像素格式 (`BGRnnn`)。
- `kill <number>`—杀死指定的会话号。

你也可以从命令行向 `xvnc` 服务器传递参数。`Xnc` 是实际的 VNC 服务器，与 X11 非常相似，并使用了许多相同的命令。你可以传递给 `xvnc` 的参数（再次来自 VNC 文档）：

- `alwaysshared`—始终将新客户端视为共享的（即忽略客户端的共享标记）。
- `nevershared`—从不将新客户端视为共享的（即忽略客户端的共享标记）。
- `disconnect`—当新的“非共享”连接进入时，不断开现有客户端。相反，将拒绝连接。新的“共享”连接仍按正常方式允许。
- `localhost`—仅允许来自同一机器的连接。如果你想使用 SSH 并阻止来自任何其他主机的非 SSH 连接，这非常有用。使用 SSH 使用 VNC 的指南。
- `cc`—设置服务器使用的虚拟类颜色。某些 X-Windows 应用程序无法良好处理8位深度 `xvnc` 通常使用的真色彩（TrueColor）视觉。你可以通过指定 `-cc 3` 让服务器使用伪色（PseudoColor）。
- `translate`—当查看器请求与服务器原生格式不同的格式时，服务器通常使用查找表来翻译像素值。每个连接的查看器可能会耗多 `256KB`，因此如果你有很多查看器，你可能需要指定。

服务器在当查看器请求与服务器原生格式不同的格式时，通常会使用查找表来翻译像素值。每个连接的查看器可能会耗多 `256KB`，因此如果你有很多查看器，你可能需要指定。

![图10.2](img/aad58e4259f15e8b2826ecf57a283621170.png)

### 10.3.2 在 Linux 使用 VNC 查看器

你也可以指定要使用的会话号。例如，要使用会话 2，输入 `vncserver :2`。你可以通过输入 `vncserver -kill <:session number>` 来杀死服务器。

VNC 服务器有几个命令行参数。通过输入 `vncserver -help` 显示。以下是参数的含义（来自 VNC 文档）：

- `name <name>`—每个桌面都有一个名称，查看器可以显示该名称。默认是 'x'，但你可以通过此选项更改。
- `geometry <width><height>`—指定要创建的桌面尺寸。默认是 `1024x768`。
- `depth <depth>`—指定要创建的桌面的像素深度（位）。默认是 `8`。
- `pixelformat <format>`—指定服务器使用的像素格式 (`BGRnnn`)。
- `kill <number>`—杀死指定的会话号。

你也可以从命令行向 `xvnc` 服务器传递参数。`Xnc` 是实际的 VNC 服务器，与 X11 非常相似，并使用了许多相同的命令。你可以传递给 `xvnc` 的参数（再次来自 VNC 文档）：

- `alwaysshared`—始终将新客户端视为共享的（即忽略客户端的共享标记）。
- `nevershared`—从不将新客户端视为共享的（即忽略客户端的共享标记）。
- `disconnect`—当新的“非共享”连接进入时，不断开现有客户端。相反，将拒绝连接。新的“共享”连接仍按正常方式允许。
- `localhost`—仅允许来自同一机器的连接。如果你想使用 SSH 并阻止来自任何其他主机的非 SSH 连接，这非常有用。使用 SSH 使用 VNC 的指南。
- `cc`—设置服务器使用的虚拟类颜色。某些 X-Windows 应用程序无法良好处理8位深度 `xvnc` 通常使用的真色彩视觉。你可以通过指定 `-cc 3` 让服务器使用伪色。
- `translate`—当查看器请求与服务器原生格式不同的格式时，服务器通常使用查找表来翻译像素值。每个连接的查看器可能会耗多 `256KB`，因此如果你有很多查看器，你可能需要指定。

反向连接端口。这通过“新客户端”（New Client）菜单选项启动。它也用于我们内部版本的 VNC（参见 http://www.uk.research.att.com/vnc/internalversion.html）。

你还可以使用 VNC 命令行选项来修改 X11 资源。你可以通过输入 `vncviewer -xrm` 来找到这些选项。这些选项很少使用，但它们是必要的（来自 VNC 文档）：

- `-shareDesktop` (`option -shared`)—是否允许其他查看器保持连接。默认为 `false`。
- `viewOnly` (`option -viewonly`)—阻止菜单和键盘事件。默认为 `false`。
- `fullScreen` (`option -fullscreen`)—全屏模式。默认为 `false`。
- `passwordFile` (`option -password`)—从哪个文件获取密码（该密码由由 `vncpasswd` 程序生成）。默认为 `null`，即向用户请求密码。
- `passwordDialog`—是否使用对话框获取密码 (`true`) 或从用户处获取 (`false`)。如果设置了 `passwordFile` 则此项无效。默认为 `false`。
- `encodings` (`option -encodings`)—按偏好顺序使用的编码列表，用空格分隔。默认为 `null`，这意味着对于机器上的 VNC 服务器使用 `copyrect hextile core` 或 `raw hextile core`。
- `-useBGR233` (`option -bgr233`)—无论视觉效果如何，在网络上传输时始终使用 `BGR233`（8位）像素格式。默认为 `false`（尽管对于强制使用 cmap 的非真色彩视觉效果会使用 `BGR233`）。
- `-nCol`—使用 `BGR233` 时，从 `BGR233` 色彩立方中分配这些“精确”颜色。当使用共享颜色映射时，此资源会限制其他 X-Windows 客户端的颜色。使用 TrueColor 时此项无效。默认值为 `256`（即全部）。
- `-useSharedColors`—如果成功分配的“精确”`BGR233` 颜色数量少于 `256`，则剩余部分将使用可用的“最近”颜色填充。此资源的权重仅针对“精确”的 `BGR233` 颜色，或也使用其他客户端的共享颜色。默认为 `true`（即使用其他客户端的颜色）。
- `-forceOwncmap` (`-owncmap`)—尝试使用伪色彩（PseudoColor）视觉和私有颜色映射。由 VNC 服务器控制颜色映射。默认为 `false`。
- `-forceTrueColor` (`option -truecolour`)—尝试使用真色彩（TrueColor）视觉。如果 `forceTrueColor` 为 `true`，则尝试使用该深度的视觉。默认为 `0`（即任何深度）。
- `-requestedDepth` (`option -depth`)—如果与 X-Windows 服务器在同一台机器上，是否使用 MIT 共享内存扩展。默认为 `true`。

## 10.3 VNC

- `-wmDecorationWidth`, `wmDecorationHeight`—窗口管理器装饰占用的总宽度和高度。这用于计算 VNC 查看器窗口的最大尺寸。默认宽度`4`，高度`24`。



### bumpScrollTime, bumpScrollPixels
当处于全屏模式且且 VNC 桌面大于 X-Windows 显示器时，只要鼠标碰到屏幕边缘就会发生滚动。滚动最大速度为每 `bumpScrollTime` 毫秒 `bumpScrollPixels` 像素。当然，实际滚动速度会比这慢，取决于你的机器速度。默认为每 25 毫秒 20 像素。

### popupToggleButton
弹出窗口中的按钮数量。请见下文了解如何自定义按钮。

### rawDelay
这对于调试 VNC 服务器有用，可以检查服务器的具体哪些部分正在更新。对于每个更新矩形，VNC 查看器在显示像素数据之前，会在指定的毫秒时间内放置一个黑色矩形。这是使用 raw 编码的高像素数据设置。默认为 0（即不执行）。

### copyRectDelay
与 `rawDelay`，但会高亮使用 rect 编码复制的区域。

### 10.3.3 为 Windows 上安装 VNC 服务器

VNC 服务器将适用于任何 32 位版本的 Windows，如 Windows 95/98、NT 和 2000。对于 NT，你必须安装了 Service Pack 3 或更高版本。

首先，将文件提取到本地驱动器的目录中并运行 `setup`。安装完成后，通过“开始 -> 程序 -> VNC -> 管理工具”菜单安装默认注册表设置。这将修改某些注册表以帮助 VNC 运行得更好。

管理工具中有一个图标，允许你启动 VNC 服务器。你可以作为应用程序或服务运行 VNC。应用程序位于“开始 -> 程序 -> VNC”文件夹中。

```
C:
\Program Files\ORL\VNC
winvnc -install
```

第一次运行服务器时，它会要求密码。这将是连接到 VNC 服务器的每个人都将使用的密码。目前没有方法为多个用户或多个密码设置 VNC 服务器。

一旦 VNC 服务器运行，它会在系统托盘中添加 VNC 图标。右键点击此图标将显示以下内容：

- 属性（Properties）—这将显示属性对话框，允许用户更改各种 WinVNC 参数。见下文不同的参数。

## 第 10 章 — 通过网络运行应用程序

- 添加新客户端（Add New Client）这将允许用户更改各种 WinVNC 参数。见下文不同的参数。
- 杀死所有客户端（Kill All Clients）这将断开所有客户端连接。
- 关闭（Shut down）这将关闭服务器。
- 关于（About）这将显示服务器信息。
- 属性（Properties）这将允许用户更改各种 VNC 参数。

## 第 10 章 • 通过网络运行应用程序

![](img/a1ad58e4259f15e8b2826ecf57a28362_123_0.png)

图 10.4 VNC 选项框。

第一个选项是编码。默认设置可以正常工作。如果你愿意，可以对这些选项进行实验，看看不同的编码是否运行更快。

鼠标选项用于在双键鼠标上通过同时按下双键鼠标上的两个按键来模拟三键鼠标，并交换第 2 键和第 3 键。如果你用的是双键鼠标，请开启三键模拟。在 Linux 系统中，中间键是剪切和粘贴键。

显示选项默认关闭。如果你使用的连接较慢（如调制解调器），请开启 8 位显示（256 色颜色）。其他选项基本上是不言自明的。

杂项选项（misc options）除了 Deonify on Bell 选项外，都是不言自明的。此设置将允许显示铃声。当铃声响时，它还会打开 VNC 查看器。这是一个通知用户邮件或其他重要事件的好设置。

要连接，输入服务器名称（或 IP 地址）和会话编号，然后点击确定。系统会提示输入密码。

连接后，你将看到一个带有 xterm 会话的桌面窗口。点击左上角的 VNC 图标可以弹出如图 10.5 所示的窗口。

## 10.3 VNC

![](img/a1ad58e4259f15e8b2826ecf57a28362_124_0.png)

图 10.5 使用 Windows 版 VNC 在远程机器上打开会话。

菜单选项是不言自明的。连接选项与上述相同。其中一个允许你将按键发送到服务器。还有选项允许你开启新连接或将连接信息保存为文件。这将保存所有当前设置，以便在另一个会话中打开。一旦获取了所需的设置，就可以使用此选项进行保存。

与 Linux 查看器一样，Windows 查看器也有许多命令行选项。它们如下（来自 VNC 文档）：

- `shared`—当您连接到 VNC 服务器时，所有其他现有连接通常会被关闭。这是出于安全考虑，而且我们通常认为 VNC 是一个移动性工具；您的桌面随地移动。此选项请求保留任何现有连接，允许您与已经在使用该桌面的人一起使用。某些服务器具有更改默认行为并覆盖此请求的选项。
- `8bit`—查看器通常会接受服务器提供的像素格式并在本地进行转换。这强制它向服务器请求 8 位真彩 (BGR233)，从而减少网络流量。这在调制解调器上非常有用。
- `config file`—您可以使用菜单中的命令将打开连接的所有详细信息保存到文件中。之后您可以在稍后通过使用此开关指定文件名来重新启动该连接。
- `register`—这告诉 Windows 外壳 `.vnc` 文件与 VNC 查看器关联。您应该能够双击文件来启动会话。有时 Windows 不需要重启即可使效果生效。
- `scale-nm`—指定本地显示的缩放因子。值 n 和 m 应该是整数。如果 m=1，则可以省略 '/' 和 m。
- `emulate3`—如果在此命令行或对话框中启用了此项，使用双键鼠标的用户可以通过同时按下两个按钮来模拟一个按钮。注意：在查看器的最新版本中，这是默认设置，现在有一个 `-noemulate3` 选项可以将其关闭。
- `noemulate3`—`emulate3` 的反向选项。
- `swapmouse`—此选项在三键模拟出现之前更为常用。通常，PC 的左、右键被映射到 X 的 1、2 和 3。此开关将按钮更改为映射到 1、3 和 2，这对于只有左右键的双键用户来说可能更有用，因为他们将获得按钮 1 和 2，而不是 1 和 3。由于结合三键模拟，这也会导致鼠标模拟按钮 3 而不是按钮 2。如果您更频繁地使用第 2 键，这可能有用。
- `emulate3timeout`—使用三键模拟时，必须在一定时间内按下两个鼠标键，它们才会被注册为单个中间单击而不是左点击和右点击。此选项允许以毫秒 (`msec`) 指定时间范围。默认值为 100。
- `emulate3fuzz`—使用三键模拟时，两个鼠标键必须在彼此的一定距离内按下，它们才会被注册为单个中间单击。此选项允许以像素 (`pixels`) 指定距离。默认值为 4。
- `fullscreen`—导致连接默认以全屏模式启动。更多细节请见下文。



### 10.3.4 VNC 查看器选项

- `listen`—在 AT&T Labs Cambridge 使用的 VNC 内部版本中，服务器可以向 CORBA 下的发起连接。此开关将 VNC 查看器置于监听模式，在那里接受这些连接，但它也有可能产生 VNC 之外的人感兴趣的完整副作用。此选项禁用剪贴板。

- `disableclipboard`—除了记录到文件之外或代替，此选项会将调试信息发送到控制台。这是。

- `Deonify`—此设置将允许显示铃声。当铃声响时，它还会打开 VNC 查看器。这是一个通知用户邮件或其他重要事件的好设置。

- `belldeify`—此设置允许显示铃声。当铃声响时，它还会打开 VNC 查看器。这是一个通知用户邮件或其他重要事件的好设置。

- `nocursor,dotcursor,normalcursor`—大多数 VNC 服务器将光标作为图像的一部分发送。在此之外添加光标可能会分散注意力。查看器的默认设置是使用一个小点来显示本地光标的位置。这。

- `kbdname`—Windows 为应用程序当前选择的键盘布局使用内部且不太实用的名称。如果您从查看器窗口的系统菜单中选择“连接信息”，就可以看到 VNC 查看器正在使用的名称。如果您更改了键盘设置并记录下来，可以在命令行上指定它，以便 VNC 以后尝试加载此布局。

- `filename`—VNC 拥有一种日志机制，可以将某些调试信息保存到文件或在控制台上显示。此选项指定写入这些信息的文件。

- `level<n>`—这控制发送到日志文件的日志量。默认值为 0，较高值（最高到 12）提供更多详细信息。

- `console`—除了记录到文件之外或代替，此选项会将调试信息发送到控制台。

- `viewonly`—在只读模式下，不会向服务器发送任何鼠标或键盘事件。这对于教学课程或其他您希望观察但不进行干预的情况非常有用。

- `restricted`—在受限模式下，大多数项目将从菜单中移除，使用户无法向远程端发送 `<CTRL>`-`<ALT>`-`<DEL>` 等指令。

### 10.3.5 Java VNC 查看器

如果你有一个支持 Java 的浏览器，你甚至不需要 VNC 查看器。Netscape、Explorer 以及许多其他浏览器都支持 Java。所有的 VNC 服务器都集成了一个 Web 服务器，允许将 Java applet 发送到客户端的浏览器上。该 Web 服务器运行在端口 58xx，其中 xx 是显示器编号。例如，要连接到服务器 mmcune 上的显示器 2，请连接到此网页：

```
http://mmcune:5802
```

在 applet 下载完成后，浏览器将显示一个 VNC 会话。如果你正在连接到 Linux 服务器，你还必须输入 `vnc-server` 脚本的类文件。Windows 服务器则内置了此功能。

缺点是，Java 查看器没有像独立查看器那样快速或稳定。你可以尝试不同的编码方案，以，看看它们是否对速度产生任何影响。

### 10.3.6 优化 VNC

VNC 服务器比 Windows 版本要快得多。这是因为通过访问源代码，Linux 版本的 VNC 能够得到更好的优化。Windows 没有现成的源代码，因此优化程度较低。

不过，VNC 服务器上可以进行一些优化。如果 VNC 服务器以 100% 的负载运行，请检查是否需要轮全屏（Poll Full Screen）、轮名前台（Poll Foreground）或轮光标下窗口（Poll Windows Under Cursor）。如果你开启了任何一项，可以开启仅轮控制台窗口（Poll Console Windows Only）来降低 CPU 使用率。所有 VNC 系统都可以进行一些优化。如果 VNC 运行太慢，可以采取以下步骤提高性能：

- 清理桌面——一个充满色彩和图形的忙碌桌面更新需要更长时间。移除任何不需要的背景或额外的图形。
- 降低分辨率——降低桌面分辨率。当 16 位或 8 位的 800 x 600 足够时，不要使用 1280 x 1040、24 位的桌面。这在现代连接上尤为重要。
- 升级显卡——升级查看器上的旧显卡将极大提高屏幕更新速度。
- 升级应用程序——某些旧应用程序更新屏幕很慢。例如，某些旧版本的 Netscape 在滚动时会更新两次屏幕。
- 优化 Java——某些设置可以极大提高更新速度。尝试不同的设置以找到最佳方案。
- 关闭离线拖拽——使用 Windows 窗口管理器时。大多数情况下，这已经关闭了。如果启用，关于如何操作此点的 Linux 文档随不同设置而异。
- 使用安全 Shell (SSH)—SSH 会压缩数据并提高慢连接下的速度。SSH 的设置将在第 16 章中解释。让 VNC 与 SSH 工作将在在本章稍后的部分解释。

### 10.3.7 VNC 安全

VNC 对密码进行加密，但一旦会话开始，它就是未加密的。尽管未加密，监听 VNC 会话比监听 telnet 或 X11 会话要困难。如果你需要更多安全性，由于 VNC 使用 TCP/IP 套接，添加安全性相对容易。有几个可以为 VNC 添加安全性的包，例如 Secure Shell (SSH)、SSL、SOCKS 和 TCP Wrappers。

SSH 可以为任何 TCP/IP 服务添加加密。SSH 的安装在前面的章节中介绍过。它由客户端和一个服务器组成。要配合 SSH 使用 VNC，请在运行 VNC 服务器的机器上运行 SSH 服务器 (`sshd`)，在运行 VNC 查看器的机器上启动 SSH 客户端，然后启动 VNC 查看器。

`ssh` 连接的语法在拆解之前看起来很复杂。连接 `mmcune` 上的会话 1 的语法为：

```
ssh -L 5902:mmcune:5901 mmcune
```

这看起来很复杂，但在拆解后就明白了。SSH 是 SSH 客户端，-L 是本地机器，5902 是本地机器的端口号，`mmcune:5901` 是 `mmcune` 上的端口号，最后 `mmcune` 是远程 SSH 主机。

这将会将本地端口 5902 重定向到 `mmcune` 上的端口 5901。要启动 VNC 会话，我们将在本地机器的端口 5902（会话 2）上打开 VNC 客户端。这将被重定向到 `mmcune` 上的端口 5901（会话 1）：

```
vncviewer@localhost:2
```

如果你在命令行中添加 `-c` 选项，SSH 也支持压缩。这对于像调制解器连接这样的慢连接尤为重要。你也可以在配置中添加压缩。这些和其他选项将在 SSH 章节中解释。我们稍后将使用的另一个开关是 `-g`，它允许主机连接到本地端口。

现在让我们用 SSH 做一些更复杂的操作。假设我们有两个通过 Internet 连接的网络。在我们网络的每侧都有一个工作站。我们在 Internet 的两侧各使用一台运行 SSH 的 Linux 机器。我们在第一个网络 (`Windows1`) 的 Windows 机器上运行 VNC 客户端，连接到第二个网络 (`Windows2`) Windows 机器上的 VNC 服务器。

`Windows1` -> 本地网络 1 -> Internet -> Linux2 -> 本地网络 2 -> `Windows2`

每台机器的设置如下：

- `Windows1`—运行 `vncviewer`
- `Linux1`—运行 `ssh -L 5901:windows2`
- `Linux2`—运行 `sshd`
- `Windows2`—运行 `vncserver`

`Windows1` 上的 VNC 查看器连接到 `Linux1`，`Linux1` 将包转发给 `Linux2`。`Linux2` 将包转发给 `Windows2`。

## 第 10 章通过网络运行应用程序

这类似于虚拟专用网络 (VPN)，它简单地在 Internet 等不安全网络上发送加密数据包。它不会提供 VPN 的所有功能；通常使用 SSH 就能解决问题。

SSL 为 VNC 添加加密代码。补丁可在 `http://mit.edu/vnc/` 获取。要使用此选项，你必须重新编译 VNC 代码并安装 SSL 库。此代码经过良好测试，因此不建议在生产环境中使用。

SOCKS 允许 VNC 通过防火墙上的 SOCKS 端口工作。VNC 的补丁可在 `http://www.research.att.com/vnc/contrib/socks.txt` 获取。同样，这必须编译到代码中，你还必须确保防火墙已启用 SOCKS。这有助于通过防火墙运行 VNC。

TCP Wrappers 允许机器限制哪些 IP 地址可以连接它。二进制文件和源代码可在 `ftp://wiki.res.cmu.edu/pub/vnc_src.zip` 获取。文件来允许或拒绝 IP 地址的格式如下：

```
allow IP address
deny IP address
deny all
```

## 10.4 总结

本章展示了如何在一台机器上运行程序并在另一台机器上显示。如需完整列表，请访问 `http://www.research.att.com/vnc/extras.htm`。

# 11 章 Windows 和 Linux 网络介绍

## 11.1 NetBIOS



Windows 和 Linux 源自不同的背景，并以不同的方式进行网络。Windows 源于 DOS 并使用 `NetBIOS` 作为其原生协议。Windows 2000 用 `Active Directory` 替换了 `NetBIOS`，但 Linux 仍然使用从 UNIX 系统继承的 `TCP/IP` 协议。

幸运的是，两种操作系统都致力于确保能够相互操作。所有版本的 Windows 都内置了 `TCP/IP` 支持，Linux 也支持 `NetBIOS`。还有一些适用于 Windows 和 Linux 的程序，可以让系统模拟对方的协议。

## 11.2 TCP/IP 与活动目录

具有集中控制。每个域都有一个主域控制器和一个备用域控制器。域控制器的主要功能是跟踪用户名和密码。Windows 使用的域模型允许用户登录一次网络，但仍然允许他们使用整个网络的资源。多个域之间还可以建立信任关系，以便在域之间共享资源。

Windows2000 将用活动目录（`Active Directory`）取代 `NetBEUI` 和域模型，它将网络设备组织成层次树状结构。最好的类比是公司的组织结构。顶部是总裁，他对所有事务拥有权限。总裁下面是几位副总裁，副总裁下面是经理，然后是员工。活动目录树的工作原理相同（见图 11.1）。它允许对网络设备进行集中控制，还允许网络被划分为逻辑分级结构。

![](img/a1ad58e4259f15e8b2826ecf57a28362_131_0.png)

图 11.1 示例活动目录树。在这种情况下，它是按地理划分的。

活动目录克服了 `NetBEUI` 的一些缺点。它的大多数功能不依赖于广播包，因此网络可以处理超过 20 个主机。它不依赖于 `WINS` 服务器（后文将讨论）。由于活动目录使用 `TCP/IP`，因此它是可路由的，可以用于覆盖多个层级的网络。

`TCP/IP` 是传输控制协议/网络协议的缩写。它最初开发在 `ARPANET`（高级研究计划机构网络）上，这是互联网的前身。由于其上的大部分机器运行 UNIX，因此 `TCP/IP` 很大程度上是在 UNIX 上开发的。与 `NetBIOS` 不同，`TCP/IP` 是为大型网络设计的，并且是可写的。`TCP/IP` 没有使用简单的方法，而是使用一种称为 IP 地址的 32 位数值。IP 地址被写成四组位于 0-255 之间的数字，并用句点隔开。IP 地址的一个示例是 `10.23.64.1`。IP 地址中的第一个数字代表网络类别。

网络根据大小分为 A 类、B 类和 C 类网络。A 类网络最多可以有 16,777,214 个主机，B 类网络可以有 16,384 个主机，C 类网络可以有 254 个主机。

## 基于 TCP/IP 的 Net BIOS

IP 地址中的某些数字留用于特殊用途。数字 0 指当前网络或主机。数字 127 被称为回环，用于诊断目的，数字 255 用于向整个网络广播包。

`TCP/IP` 地址的另一部分是子网掩码。它可以用于子网划分或将网络划分为两个或多个网络。例如，在上述 `10.23.64.1` 网络中，`255.255.0.0` 子网掩码不会划分网络，但 `255.255.240.0` 子网掩码会划分网络。子网掩码可能是 `TCP/IP` 最复杂的部分，在这里解释它们需要大量时间。请参见附录 A 获取子网掩码以及其他 `TCP/IP` 问题的更详细说明。

IP 地址对机器很友好，但对用户来说并不友好。大多数设备还有一个称为主机名的用户友好名称。我们大多数人都见过这些主机名作为 Web 地址。例如，IBM 的 Web 站点是 `www.ibm.com`。与该网站关联的 IP 地址是 `204.146.80.99`。与 IP 地址一样，主机名也是层次化的。“www”代表服务器，“IBM”代表与 IBM 公司关联的域，“com”代表商业互联网。

将人类友好的名称转换为机器友好的 IP 地址的过程是使用 `DNS`（域名系统）完成的。`DNS` 简单来说是一个用于查找与主机名关联的 IP 地址的层次系统。当 Linux 机器被赋予主机名时，它首先查找文件 `/etc/hosts`，这是一个简单的列出主机名和地址的文本文件。如果找不到，它会查询主名称服务器。名称服务器维护一个主机名和 IP 地址的数据库。如果找不到主机名，将查询备名称服务器。如果找不到主机，将返回类似“unknown host”的错误信息。这是对 `DNS` 的简化描述。以后将进行更详细的描述。

多年来标准发生了变化。目前的 IP 版本是 4，写为 `IPv4`。下一个 IP 版本是 6 (`IPv6`)，它比 `IPv4` 有几项改进。最显著的变化是 `IPv6` 将具有 128 位而不是 32 位的地址。互联网正在耗尽 IP 地址。目前的 32 位 IP 地址将允许多得多的。`IPv6` 内置了增强的安全性和诊断功能。请访问 `www.ipv6.org` 查看 `IPv6` 的完整规范。

## 基于 TCP/IP 的 Net BIOS

当然，Windows 和 Linux 都有许多允许它们相互交互的功能和程序。Windows 和 Linux 机器都允许在 `TCP/IP` 上实现 `NetBIOS` (`NetBT`)。这允许它们拥有共同的协议，但也了一些独特的问题。主要问题是 `TCP/IP` 主机名并不总是能解析为 `NetBIOS` 名称。

# 第 12 章

## SAMBA 简介

### 12.1 Samba 的起源

`Samba` 是一组程序，允许非 Windows 机器使用服务器块（`SMB`）网络，这是微软产品（如 Windows 98 和 NT）的原生协议。`Samba` 由澳大利亚研究生 Andrew Triddell 发，他需要一种在 UNIX 机器和 DOS PC 之间共享文件的方法。他可以使用 UNIX 的原生网络网络文件服务（`NFS`，后文将讨论），但他的 DOS PC 上已经运行了 `NetBIOS`。由于无法同时加载 `NetBIOS` 和 `NFS`，他决定反向工程 `SMB` 并在 UNIX 机器上实现它，使 UNIX 机器像一台 PC 服务器。他在 1992 年在互联网上发布代码。在修复了一些错误后，他将项目搁置了。几年后，他需要将他的 Linux PC 与妻子的 Windows PC 连接。在没有其他选择的情况下，他尝试了他的旧代码，令惊讶的是它可以运行。通过研究，Andrew 发现 `NetBIOS` 和 `SMB` 至少有少量文档。在改进他的程序时，他尝试为它想一个名字。他在拼写检查器中输入“SMB”，出现的词是“Samba”。随着使用量的增长，`Samba` 聚集了一个整个程序员团队。它包含在大多数 Linux 发行版和许多商业 UNIX 版本中，例如 SGI (Silicon Graphics Inc.) 的 `IRIX`。除了 UNIX 之外，还有针对 MVS、MMS、OS/2、Stratus-OS、Amiga 和 PE/IX 的 `Samba` 版本。`Samba` 已经成为一套完整的工具，实现了 Windows NT 服务器的大部分 PC 和打印共享功能。

### 12.2 Samba 工作原理

`Samba` 使用基于 `TCP/IP` 的 `NetBIOS` (`NetBT`) 提供四种 `SMB` 服务：文件和打印服务、身份验证与授权、名称解析以及服务公告（也称为浏览）。目前我们简要介绍这些内容，并在书的后续部分进行详细说明。

文件和打印服务是这些中最重要的。它们允许 Windows（以及 `Samba`）通过网络共享文件和打印机。这些服务是最初局域网（LAN）产生的主要原因。

身份验证和授权使用登录名和密码允许经过授权的用户访问网络。它们限制了每个用户在网络上可以的操作。文件和打印机可以根据用户进行限制。文件也可以设置为只读，以防止意外更改。

名称解析是将 `NetBIOS` 名称转换为 IP 地址（通过 `NetBT` 实现）。这在 Windows 网络中是通过 Windows 内部名称服务器（`WINS`）完成的。`Samba` 可以执行 `WINS` 的大部分功能。

服务公告（或浏览）允许网络上的其他设备了解有哪些可用服务。服务列表存储在一个名为“主浏览器器”（master browser）的机器上。可以通过打开“网络邻域”（参见 12.1）来查看浏览列表。

![](img/a1ad58e4259f15e8b2826ecf57a28362_135_0.png)

图 12.1 “网络邻域”显示了网络上的 `SMB`（Windows 和 `Samba`）机器。

`Samba` 可以执行 Microsoft Windows NT Server 的几乎所有功能。那么，`Samba` 何是 Windows 网络的良好选择呢？

虽然 `Samba` 支持 Windows 主域控制器（`PDC`）的大部分功能，但不支持备用主域控制器（`BDC`）功能。完全实现 `BDC` 的唯一方法是使用 Windows NT。

此外，如果你已经有一个 Microsoft `WINS` 服务器，`Samba` 无法与它交换数据。所以如果你已经有一个 Microsoft `WINS` 服务器并需要添加另一个，请坚持使用 Windows NT。

这两个问题很快就会被轻量级目录访问协议（`LDAP`）解决，`LDAP` 等其他功能还允许为所有网络资源使用统一登录。微软和 Linux 社区都在其产品中开发 `LDAP` 功能。更多关于 `LDAP` 的信息，请访问 `http://www.ldap.org`。



那么为什么有人会在 Windows 网络上使用 Samba 呢？Samba 与 Linux 结合既快速又稳定，最重要的是，它是免费的。Windows NT 按用户收费，其十用户版本运行在较低的硬件上。仅在旧的 486 或低端 Pentium 上设置 Linux 和 Samba 是不够的。这对于运行一个小型的部门服务器来说绰绰有余，而 Windows NT 服务器则需要更好的计算机才能正常运行。

Samba 也是混合 UNIX 和 Windows 环境的良好选择。由于 Linux 包含了所有标准的 UNIX 网络工具，Linux 上的上的 Samba 可以与 UNIX 和 Windows 进行透明通信。

在完成对 Samba 的介绍后，下一章将介绍如何将 Samba 设置为文件服务器。

## 第 13 章

将 Samba 设置为 Windows NT 服务器

Linux 和 Samba 可以执行 Windows NT 服务器的许多功能。这种组合可以被设置为网络上的独立服务器，也可以作为现有网络的一部分。我们将设置一个 Linux 和 Samba 服务器，然后讨论使用 Linux 和 Samba 的优势和局限性。Windows NT。

### 13.1 将 Samba 设置为独立的 Windows NT 文件服务器

现在我们把把知识付诸实践。首先，我们将在新网络上将 Samba 设置为独立服务器。之后，我们将 Samba 服务器添加到现有网络中。

有一些 IP 地址是预留给私有网络的（不直接连接到互联网的网络）。见下表 13.1 的可在私有网络使用的地址列表。

表 13.1 私有 IP 网络的地址范围

| 类 | IP 地址 | 子网掩码 |
| --- | --- | --- |
| A | 10.X.X.X | 255.0.0.0 |
| B | 172.16.X.X | 255.255.0.0 |
| C | 192.168.X.X | 255.255.255.0 |

接下来，我们需要决定在工作站上使用固定 IP 地址还是动态 IP 地址。固定 IP 地址在每个站点单独设置。动态 IP 地址通过动态主机配置协议（DHCP）从服务器获取。由于在服务器上设置 IP 配置比在每个工作站上更容易，我们将使用 DHCP。然而，如果我们决定使用固定 IP 地址，那么设置 DHCP 就是没必要的。

### 13.1.1 设置 DHCP

在我们在服务器上安装 Linux 后，我们需要设置 DHCP。服务器的 IP 地址将是 10.0.0.2，子网掩码为 255.255.255.0。我们在 10.0.0.1 安装了一个路由器。路由器只是允许网络被划分为若干部分（子网）。DHCP 作为 DHCP 服务器由大多数 Linux 发行版提供安装。如果你的发行版没有带 DHCP，你可以从 Linuxberg http://www.linuxberg.net/ 下载。搜索 DHCP。关于 DHCP 的文档可以在 http://www.linuxdoc.org/doc/ip/howto/dhcp 获取。

安装 DHCP 后，必须创建并编辑配置文件 `/etc/dhcpd.conf`。此文件看起来非常像 `smb.conf`。它包含全局（global）、共享网络（shared network）和组部分。全局部分具有默认值。如果有必要，它可以被其他部分覆盖。注意所有行末尾都有一个分号（`;`）。

```
server identifier none
option subnet mask 255.255.255.0
option broadcast address 10.0.0.255
default lease time 86400
max lease time 259200;
```

有两个参数需要需要解释：`default-lease-time` 和 `max-lease-time`。通过 DHCP，服务器给出的 IP 地址在给定时间后过期。这防止了工作站和其他设备在不再使用地址后继续使用。`default-lease-time` 是设备保留 IP 的时间。在这种情况下，86400 秒等于一天（60 分 x 24 小时）。`max-lease-time` 是设备必须续约的时间。如果在这个时间之前没有续约，设备的 IP 地址将被禁用，且该 IP 可以分配给另一个设备。在这个示例中，`max-lease-time` 是三天（86400 秒 x 3）。

`subnet` 部分配置 DHCP 服务器。子网标识和网络掩码之后是选项：

```
subnet 10.0.0.0 netmask 255.255.255.0
{
  range 10.0.0.5 10.0.0.250;
  option netbios-name-servers 10.0.0.2;
  default lease time 86400
}
```

`range` 指定了用于 DHCP 租约的地址。我们包含了从 5 到 250 的地址。我们使用 251-254 用于服务器、路由器以及需要固定地址的设备的固定地址。在这种情况下，1 是路由器，2 是 Samba 服务器（10.0.0.1 和 10.0.0.2）。`netbios-name-servers` 参数指定 WINS 的 IP 地址。在这种情况下，我们使用 Samba 服务器（10.0.0.2）作为 WINS。

### 将 Samba 设置为独立的 Windows NT 服务器

`default-lease-time` 覆盖了全局部分的值。如果我们留空它，将使用全局值。

如果我们有多个子网，我们将使用 `shared network` 部分。在这个示例中，我们将使用两个子网：10.0.0.0 和 10.0.1.0。

```
shared network
{
  subnet 10.0.0.0 netmask 255.255.255.0
  range 10.0.0.0 10.0.0.250;
  option routers 10.0.0.1;
}
subnet 10.0.1.0 netmask 255.255.255.0
  range 10.0.1.1 10.0.1.250;
  option routers 10.0.1.1;
}
```

`shared network` 部分的选项划分为每个子网。子网中的选项与单个子网设置完全相同。在这种情况下，我们设置了路由器来连接子网，10.0.0.1 和 10.0.1.1。

`group` 部分用于出于特定原因分组。例如，你可以用它将 Windows 98 工作站与 Windows NT 工作站分开。由于我们的网络不需要这个，所以我们不使用 `group` 部分。

所以这就是 `dhcpd.conf` 文件：

```
server identifier none
option subnet mask 255.255.255.0
option broadcast address 10.0.0.255;
option lease time 86400;
max lease time 259200;
shared network
{
  subnet 10.0.0.0 netmask 255.255.255.0
  range 10.0.0.0 10.0.0.250;
  option routers 10.0.0.1;
}
subnet 10.0.1.0 netmask 255.255.255.0
  range 10.0.1.1 10.0.1.250;
  option routers 10.0.1.1;
}
```

接下来我们将设置 `smb.conf` 文件。我们将从默认文件开始并对其修改。以 `#` 开头的行是未使用的选项：

```
# 这是 Samba 的主配置文件。你应该阅读
# smb.conf(5) 手页以理解这里列出的选项。Samba 拥有大量的可配置选项（可能太多了！），其中大多数在示例中并未显示。
```

# 126 第 13 章 · 将 Samba 配置为 Windows NT 服务器



# 任何以 `;`（分号）或 `#`（井号）开头的行都是注释并会被忽略。在示例中，我们将使用 `#` 作为注释，并使用 `;` 表示配置文件中你可能想要启用的部分。

注意：每当你修改此文件时，你都应该运行 `"testparm"` 命令以检查你是否没有犯任何基本的语法错误。

## 全局设置
```
[global]

netbios name = mmccune

# workgroup = NT 域名称或工作组名称
workgroup = WORKGROUP

# server string 等于 NT 的描述（Description）字段
server string = Samba Server

# 此选项对于安全非常重要。它允许你限制
# 连接到本地局域网中的机器。
# 以下示例限制了访问两个 C 类网络和
# “回环”接口。有关该语法的更多示例，请参阅
# smb.conf 手册页。
hosts allow = 192.168.1.2, 192.168.2.127.

# 如果你想自动加载打印机列表而不是
# 逐个设置，那么你需要这个。
printcap name = /etc/printcap
load printers = yes

# 除非你的打印系统是非标准的，否则不需要
# 指出打印系统类型。目前支持的打印系统包括：
# bsd, sysv, plp, lprng, aix, hpux, 和 qnx。
printing = bsd

# 如果你想使用访客账户，请取消此注释。你必须将其添加到 /etc/passwd，
# 否则将使用 "nobody" 用户。
guest account = pcgues

# 这告诉 Samba 为每个连接的机器
# 使用独立的日志文件
log file = /var/log/samba.log%m

# 限制日志文件的大小（单位为 Kb）。
max size = 50

# 安全模式。大多数人会想要用户级安全。详情请参阅
# security_level.txt。
security = user
# 仅在 security = server 时使用 password server 选项
password server = <NT-Server-Name>
```

### 13.1 将 Samba 设置为独立 Windows NT 文件服务器

# level 允许对所有大小写组合

# 密码的 __ 字符进行匹配。

password level = 3

username level = 3

# 你可能想使用密码加密。请阅读 Samba 文档

# ENCRYPTION.txt、Win95.txt 和 WinNT.txt。

# 在阅读这些文档之前不要启用此选项。

# 默认情况下，Windows 95 不使用加密密码，但 Windows 98、NT

# 和 2000 使用加密密码。

encrypt passwords = yes

smb password file = /etc/smbpasswd

# 以下内容用于允许从 Windows 修改密码，

# 同时更新 Linux 系统密码。

# 配合上面的 'encrypt passwords' 和 'smb password file' 使用。

# 注意2：你不需要允许工作站仅更改

# 加密的 SMB 密码。它们允许 UNIX 密码

# 与 SMB 密码保持同步。

# unix password sync = Yes

# passwd program = /usr/bin/passwd %u

# passwd chat = *NewUNIX*password* %nn *ReType*newUNIX*password* %nn

*password:*allauthentication*updated*successfully*

# UNIX 用户可以映射到不同的 SMB 用户名。

username map = /etc/smbsusers

# 使用以下行允许你根据每台机器

# 自定义配置。%m 会被替换为连接机器的 NetBIOS

# 名称。

#include = /etc/smb.conf %m

# 大多数人会发现此选项提供了更好的性能。

# 详情请参阅 speed.txt 和手册页。

socket options = TCP_NODELAY SO=8192 RCVBUF=8192 SO_SBUF=8192

# 配置 Samba 使用多个接口。

# 如果你有多个网络接口，则你必须在这里

# 列出它们。详情请参阅手册页。

# interfaces = 192.168.12.2/24 192.168.13.2/24

# 在此处配置远程浏览列表同步。

# 请求公告或浏览列表同步到：

# 特定主机或 / 到整个子网（见下方）

# remote browse sync = 192.168.3.25 192.168.5.255

# 在此处让此主机向本地子网宣告自己。

# remote announce = 192.168.1.255 192.168.2.44

# 第 13 章 · 将 Samba 配置为 Windows NT 服务器

# 浏览器控制选项：

# 如果你不希望 Samba 成为网络中的主浏览器，请将 local master 设置为 no。否则，适用标准的选举规则。

# local master = no

# os level 决定了此服务器在主浏览器

# 选举中的优先级。默认值应该是合理的。

# os level = 33

# domain master 指定 Samba 为域主浏览器。这

# 允许 Samba 汇总不同子网之间的浏览列表。

# domain master = yes

# 主浏览器选举的偏好。

# os level 最高的服务器将成为主浏览器。

preferred master = yes

# 如果多个服务器具有相同的 os level，优先级最高的服务器将成为主浏览器。

# 在此处向本地子网宣告自己。

# remote announce = 192.168.1.255 192.168.2.44

[printers]

```
comment = All Printers
path = /var/spool/samba
browable = no
# 设置 public = yes 以允许用户 'guest account' 打印。
guest ok = no
writable = no
printable = yes
```

# 这对于用户共享文件非常有用。

[tmp]

```
comment = /tmp
path = /
read only = no
public = yes
```

# 这是一个公共访问的目录，但是只读的，"staff"

# 组的用户除外。

# 我将使用此目录存放像 Office 2000 这样的程序。

[public]

```
comment = Public Stuff
path = /home/samba
public = yes
writable = no
write list = @staff
```

# 其他示例：

#

一台私有打印机，仅供 Fred 使用。打印数据将放在 Fred 的

# 目录中。注意，Fred 必须对打印目录具有写入权限，

#无论它在哪里。

;[fredspn]

```
; comment = Fred's Printer
; valid users = fred
; path = /homes/fred
; printer = freds_printer
; public = no
; writable = no
; printable = yes
```

# 第一个私有目录，仅供 Fred 使用。注意 Fred 需要对

# 目录具有写入权限。

;[fdsdir]

```
; comment = Fred's Service
; path = /usr/somewhere/private
; valid users = fred
; public = no
; writable = no
; printable = no
```

## 13.1 将 Samba 作为独立的 Windows NT 文件服务器

# 为每个连接的机器提供不同目录的服务

# 允许你为接入的机器定制配置。你还可

# 使用 \u 选项根据用户名进行定制。

# \m 将被替换为连接的机器名称。

; [phome]

```
comment = PC Directories
path = /usr/pc/%m
public = no
writable = yes
```

# 一个所有用户均可读写的公共访问目录。注意，用户在

#目录中创建的所有文件将由默认用户所有，因此

# 任何有权限的用户都可以删除其他用户的文件。显然，

# 该目录必须允许默认用户写入。也可以指定另一个

# 用户，在这种情况下，所有文件将改由该用户所有。

; [public]



```
path = /usr/somewhere/else/public
public = yes
only guest = yes
writable = yes
printable = no
```

# 以下条目演示了如何共享目录，以便两个用户可以在那里放置文件，这些文件将归特定用户所有。在此设置下，目录应该对两个用户都可写，并设置滞位（sticky bit）以防止滥用。显然，这可以扩展到任意数量的用户。

; `[myshare]`

```
comment = Mary's and Fred's stuff
path = /usr/somewhere/shared
valid users = mary fred
public = no
writable = yes
printable = no
create mask = 0765
```

注意，我们正在使用 `/home/samba` 来存储用户程序，例如 Microsoft Office 2000 的安装文件。我们已经给了 `staff` 组写入该目录的权限。我们还需要赋予非 root 用户在此处安装程序的权限。

我们通过 `wins support = yes` 行创建了 WINS 服务器，并设置了打印机以允许客户用户打印。

在设置好 DHCP 和 Samba 后，我们需要创建用户和组账户以及加密登录密码，我们需要创建加密密码文件：

```
cat /etc/passwd | mksmbpasswd.sh > /etc/smbpasswd
```

Windows 95、Os2、Windows 98 以及安装了 Service Pack 3 或更高版本的 Windows NT 将默认支持加密密码。DOS 和较旧版本的 Windows 在不升级的情况下将不支持密码。

## 13.2 在现有网络中添加 Samba 服务器

将 Samba 服务器作为独立网络设置起来相对简单。在现有网络上设置它更为复杂。你将不得不获取现有网络的所有设置，包括 PDC 和 BDC、WINS 服务器、路由器和打印机。

Samba 加入 Windows 域没有问题，但它不能作为 BDC 运行，也无法与 WINS 服务器交换数据。此外，将 Samba 作为 PDC 仍处于实验阶段，因此在收到过警告的生产环境中请勿使用 Samba！

将 Samba 引入 Windows 域相对简单。首先，使用域服务器管理器（Server Manager for Domains）作为独立的服务器或工作站，在 Windows 域中为 Samba 机器创建一个账户。只需转到 计算 -> 加入域。输入计算机名称并点击添加。

![](img/a1ad58e4259f15e8b2826ecf57a28362_147_0.png)

图 13.1 使用服务器管理器在 Windows NT 中向域添加计算机。

接下来，我们需要在 Samba 机器上配置 `sm.conf`。在本例中，我们将域命名为 `NTDomain`，PDC 为 `NTPDC`，BDC 为 `NTIS`，而 WINS 服务器位于 IP 地址 `10.0.0.2`。首先，我们需要使用此命令停止 Samba：

```
samba stop
```

接下来在 `samba.conf` 中添加这些设置：

```
Security = Domain
Workgroup = NTDomain
Password Server = NTPDC ;（如果你想让 Samba
 自动定位密码服务器，可以设置为 *）
ennrypt passwords = yes
wins server = 10.0.0.2
```

## 13.3 Samba 作为主域控制器

重启 Samba（`samba start`）后，我们需要为计算机创建一个机器 ID。机器 ID 是域控制器识别域内每个设备的方式。创建此 ID，输入以下命令：

```
smbpassword -j NTDomain -r NTPDC
```

如果成功，你应该收到“Joined domain NTDomain”的消息。如果收到其他消息，请首先检查之前的步骤中是否存在错误或拼写错误。如果这不能解决问题，请使用最后一章中的故障排除步骤。此外，附录结尾处针对 NT 域的故障排除程序。

### Samba 作为主域控制器功能说明

如前所述，Samba 可以作为 PDC 运行，但功能尚不。。正常的功能包括：

- 信任关系
- BDC 集成
- Windows 打印
- 访问列表
- 用户数据库
- 用户名映射
- 相对识别
- LDAP
- Alpha 和 Beta 代码

尚未实现的功能包括：

- WINS 支持
- 登录脚本
- Windows 访问列表 (ACL)
- 机器更新
- 用户映射

# 第 14 章

## 将 Linux 连接到 Windows PC

Linux 可以通过 Windows 的原生网络能力连接到联网的 Windows PC。

首先，使用控制面板中的网络图标在 Windows 中设置网络。

Linux 允许几个程序连接到 Windows 机器。以下程序包含在大多数 Linux 发行版中以及 Samba 中：`smclient`, `smbfs`, `smwrapper`, `smsh`, `sharity` 和 `smprint`。

`smclient` 是一个命令行工具，允许 Linux 在 Linux 和 Windows 之间浏览和复制文件。

`smbfs` 和 `sharity` 允许 Linux 文件系统原生地挂载到 Linux 系统上。Windows 目录看起来像普通的 Linux 目录。`sharity` 和 `smclient` 还支持用于加密事务的 SSL。

`smwrapper` 和 `smsh` 允许从 Linux 机器浏览 Windows 文件。

`suntar-tar` 允许将 Windows 机器备份到 Linux 机器。

`smbprint` 允许 Linux 打印到共享的 Windows 打印机。

其他包使用这些工具访问 Windows 计算机。例如，某些 Linux 备份工具使用 `smclient` 备份 Windows 客户端。

`smbclient` 是类似于 FTP 的命令行工具。它允许 Linux 连接到 Windows 共享。一旦连接，`smbclient` 允许 Linux 如下列出和复制文件：

```
smclient //alias/c
Added interface ip=10.0.0.2 bcast=10.0.0.255 nmask=255.255.255.0
Password:
ls > ls
BOOTLOG.TXT      AH      89906 Nov 4 15:24:00 1999
COMMAND.COM      A       93890 Fri Apr 23 22:22:00 1999
SUHDOG.DAT       HR      51666 Fri 6 13:15:00 1999
....files deleted here for brevity....
64322 blocks of size 131072. 31108 blocks available
```

注意，这些使用正斜杠 (`/`) 而不是 Windows 标准的反斜杠 (`\`)。因为 Linux 将反斜杠视为转义字符，因此在大多数 Windows 使用反斜杠的情况下，Linux 会使用正斜杠。

我们使用 `ls` 来获取文件列表，但使用 `dir` 也可以。`smclient` 在连接后可以接受几个命令。可以通过输入 `help` 来列出这些命令：

```
smb: \> help
ls dir du lcd cd
pwd get mget put mput
rename more mask del open
rm md rmdir rd
prompt recurse translate lowercase print
print queue cancel quit q
exit newer tar blocksize
tarmode setmode help ? !
```

如果我们查看某个特定命令的帮助，输入 `help <command name>`。例如，如果我们想查看 `ls` 的帮助，我们将输入 `help ls`：

```
smb: \> help ls
HELP ls:
<mask> list the contents of the current directory
```

如你所见，`ls` 只有一个参数。它是一个掩码（`mask`），用于限制显示的文件。例如，`ls *.exe` 会找到所有以 exe 结尾的文件。

我们将介绍 `smbclient` 命令行。首先，我们需要介绍命令行选项。

### 14.1 smbclient 命令行选项

`smbclient` 命令行的通用形式为：

`smbclient <servicename> <password> <options>`

`servicename` 是你正在连接的 Windows 服务名称。它的格式为 `//server/share`。`password` 是共享的密码或登录服务的用户密码。这取决于 Windows 是共享安全还是用户级安全。选项在下方介绍：



## `-s` `smb.conf`
指向 `smb.conf` 的位置。与 Samba 软件包的其余部分一样，`smbclient` 从 `smb.conf` 获取设置。

## `-B` `ip`
允许 `smbclient` 使用 IP 地址查找 Windows 机器的 NetBIOS。

## `-O` `Socket Options`
允许你调整 `smbclient` 使用的 TCP 套接字。

## `-R` `Name Resolve Order`
Linux 有若干种方法来解析网络上的名称。默认情况下，Linux 使用以下顺序进行解析：

1. `localhost` — Samba 用于查找主机名的文件。它存储在与 `smb.conf` 相同的目录。
2. `host` — 这是 Linux 系统查找名称的默认文件。它保留在 `/etc` 目录。
3. `wins` — 如果可用，Linux 系统将使用 WINS 服务器解析名称。
4. `bcast` — 如果其他方法失败，Linux 将使用广播尝试解析名称。它使用 `smb.conf` 中的 `interfaces` 参数来决定如何广播。如果未设置 `interfaces` 参数，它将在所有节点接口上广播。此参数允许更改默认的名称解析顺序；例如，`-R host lmbcast` 会使 `host` 文件成为第一个，且不会使用 `wins` 进行解析。

## `-M` `Netbios name`
向其他计算机发送消息，这在 Windows 机器上称为 WinPopup 消息。在 Windows 9x 机器上，必须启用 WinPopup 此功能才能正常工作。注意，这仅对 NetBIOS 名称有效，不适用于 IP 地址或 IP 主机名。输入此命令后，你会被询问消息，然后是 `<CTRL>`：

```
smclient -M
Added interface ip=10.0.0.2 bcast=10.0.0.255 nmask=255.255.255.0
```

## `-i` `ip`
允许 `smbclient` 使用 IP 地址查找 Windows 机器的 NetBIOS。



## `-O` Socket Options
允许你调整 `smbclient` 使用的 TCP 套接字。

## `-R` Name Resolve Order
Linux 有若干种方法来解析网络上的名称。默认情况下，Linux 使用以下顺序进行解析：

1. `localhost` — Samba 用于查找主机名的文件。它存储在与 `smb.conf` 相同的目录。
2. `host` — 这是 Linux 系统查找名称的默认文件。它保留在 `/etc` 目录中。
3. `wins` — 如果可用，Linux 系统将使用 WINS 服务器解析名称。
4. `bcast` — 如果其他方法失败，Linux 将使用广播尝试解析名称。它使用 `smb.conf` 中的 `interfaces` 参数来决定如何广播。如果未设置 `interfaces` 参数，它将在所有节点接口上广播。此参数允许更改默认的名称解析顺序；例如，`-R host lmbcast` 会使 `host` 文件成为第一个，且不会使用 `wins` 进行解析。

## `-s` smb.conf
指向 `smb.conf` 的位置。与 Samba 软件包的其余部分一样，`smbclient` 从 `smb.conf` 获取设置。

## `-B` ip
允许 `smbclient` 使用 IP 地址查找 Windows 机器的 NetBIOS。

## `-M` Netbios name
向其他计算机发送消息，这在 Windows 机器上称为 WinPopup 消息。在 Windows 9x 机器上，必须启用 WinPopup 此功能才能正常工作。注意，这仅对 NetBIOS 名称有效，不适用于 IP 地址或 IP 主机名。输入此命令后，你会被询问消息，然后是 `<CTRL>`：

```
smclient -M
Added interface ip=10.0.0.2 bcast=10.0.0.255 nmask=255.255.255.0
```

## `-i` ip
允许 `smbclient` 使用 IP 地址查找 Windows 机器的 NetBIOS。



### smbclient 选项

- `bcast`—如果其他方法失败，Linux 将使用广播尝试解析名称。它使用 `smb.conf` 中的 `interfaces` 参数来决定如何广播。如果未设置 `interfaces` 参数，它将在所有节点接口上广播。此参数允许更改默认的名称解析顺序；例如，`-R host lmbcast` 会使 host 文件成为第一个，且不会使用 wins 进行解析。

- `-i ip`—允许 `smbclient` 使用 IP 地址查找 Windows 机器的 NetBIOS。

- `-O Socket Options`—允许你调整 `smbclient` 使用的 TCP 套接字。

- `-R Name Resolve Order`—Linux 有若干种方法来解析网络上的名称。默认情况下，Linux 使用以下顺序进行解析：

    1. `localhost`—Samba 用于查找主机名的文件。它存储在与 `smb.conf` 相同的目录。
    2. `host`—这是 Linux 系统查找名称的默认文件。它保留在 `/etc` 目录。
    3. `wins`—如果可用，Linux 系统将使用 WINS 服务器解析名称。
    4. `bcast`—如果其他方法失败，Linux 将使用广播尝试解析名称。它使用 `smb.conf` 中的 `interfaces` 参数来决定如何广播。如果未设置 `interfaces` 参数，它将在所有节点接口上广播。此参数允许更改默认的名称解析顺序；例如，`-R host lmbcast` 会使 host 文件成为第一个，且不会使用 wins 进行解析。

- `-s smb.conf`—指向 `smb.conf` 的位置。与 Samba 软件包的其余部分一样，`smbclient` 从 `smb.conf` 获取设置。

- `-B ip`—允许 `smbclient` 使用 IP 地址查找 Windows 机器的 NetBIOS。

- `-M Netbios name`—向其他计算机发送消息，这在 Windows 机器上称为 WinPopup 消息。在 Windows 9x 机器上，必须启用 WinPopup 此功能才能正常工作。注意，这仅对 NetBIOS 名称有效，不适用于 IP 地址或 IP 主机名。输入此命令后，你会被询问消息，然后是 `<CTRL>`：

```
smclient -M
Added interface ip=10.0.0.2 bcast=10.0.0.255 nmask=255.255.255.0
```

由于 tar 选项非常复杂，让我们检查使用它们的几个示例。要将 Windows PC `alisa` 上 `c` 共享的所有文件备份到 `backup.tar`，输入以下：

```
smclient //alisa/c -Tc backup.tar
```

要恢复 `alisa` 整个 `c` 共享，输入：

```
smclient //alisa/c -Tx backup.tar
```

要备份新文件并重置归档位，输入：

```
smclient //alisa/c -Tcga backup.tar
```

### 14.2 smbclient 命令

一旦 `smbclient` 登录到 Windows 机器，首先会看到一个提示符：

```
smb: \
```

这代表 Windows PC 上共享根目录。从这里，我们可以输入 smb-client 命令：

- `? [command]` 或 `help [command]`——`smbclient` 命令的帮助信息。该命令本身将提供所有 `smbclient` 命令的帮助，或者你也可以输入命令名称来查看单个命令的用法。

- `! [Linux command]`——允许在不退出 `smbclient` 的情况下在本地机器上运行 Linux 命令。例如，要查看本地硬盘上的文件：

```
smb: \! ls 
MSPRINT2.INF
MSPRINT3.INF
MSPRINT4.INF
smb: \>
```

- `archive [level]`——这允许 `get` 命令根据归档位（archive bit）检索 Windows 上的文件。不同的级别如下：

0 获取所有文件且不更改归档位。

1 获取带有归档位的文件且不更改归档位。

2 获取所有带有归档位的文件并重置这些文件的归档位。

3 获取所有文件并重置所有文件的归档位。

要查看当前设置的归档级别，在提示符处输入 `archive`：

```
smb: \> archive
Archive level is 0
smb: \>
```



- `Blocksize`——指定 tar 选项的块大小。块大小以 512 字节为增量。例如，要将块大小设置为 10 千字节 (10K)，请使用以下命令：

```
smb: \> blocksize 20
blocksize is now 20
smb: \>
```

- `cancel <jobid>`——取消打印队列中指定的 `jobid`。

```
smb: \> cancel 1
Job 1 cancelled
smb: \>
```

当然，你必须连接到打印机并知道打印作业编号才能执行此操作。

## 第 14 章 • 将 Linux 连接到 Windows 电脑

- `cd [directory]`——允许你更改 Windows 机器上的目录。如果指定了目录，它将像使用 Windows-`cd` 命令一样更改目录，包括通配符 `*` 和 `?`。

- `dir [expression]` 或 `ls [expression]`——这两个中的任一个都会显示 Windows 机器上匹配表达式的文件列表。它还支持通配符 `*` 和 `?`。

- `du`——此命令仅显示当前目录下所有文件占用的空间。如果开启了递归选项（`recursive`），它将显示所有目录的总和：

```
smb: \> recurse
direct recursion is now off
smb: \> du
    64322 blocks of size 131072. 31490 blocks available
Total number of bytes: 20794893
smb: \> recurse
direct recursion is now on
smb: \> du
    64322 blocks of size 131072. 31490 blocks available
Total number of bytes: 4240552435
smb: \>
```

注意，关闭递归时，总字节数为 20794893，而开启递归时的总字节数为 4240552435。

- `exit or quit or q`——顾名义，退出 `smclient`。

- `get <remote file> [local file]` 将远程文件从 Windows 机器复制到 Linux 机器。你可以可选地使用 `[local file]` 在 Linux 机器上为文件指定不同的名称。否则，Linux 文件名将与 Windows 文件名相同。如果开启了小写转换（`lowercase`），本地文件将是远程文件的全小写版本。

文件以二进制模式传输，除非开启了转换（`translate`），此时将以 ASCII 模式传输，该模式用于文本文件。ASCII 模式会将标准换行符转换为 Linux 标准换行符。例如：

```
smb: \> lowercase
filename lowerasing is now on
smb: \> lowercase
filename lowerasing is now off
smb: \> translate
CR/LF-->>LF and print text translation now on
smb: \> translate
CR/LF-->>LF and print text translation now on
smb: \> get config.sys
getting file config.sys of size 59 as config.sys (0.433212 kb/s)
(average 0.433212 kb/s)
smb: \> *
```

在下面的示例中，掩码（`mask`）和递归（`recursion`）关闭关闭，而提示（`prompt`）开启开启：

```
smb: \startoff\ ls
D 0 Fri Oct 18:40:18 1999
so51_lnx_01_n1.tar D 7442432 Fri Oct 18:47:34 1999
so51_lnx_01_n2.tar A 11600384 Fri Oct 18:48:52 1999
so51_lnx_01_n6.tar A 10398720 Fri Oct 18:48:54 1999
so51_lnx_01_n3.tar A 10718720 Fri Oct 18:49:49 1999
so51_lnx_01_n5.tar A 10459616 Fri Oct 18:50:00 1999
so51_lnx_01_n7.tar A 9664000 Fri Oct 18:50:06 1999
so51_lnx_01_n4.tar A 10122752 Fri Oct 18:50:16 1999
GUIL00 A 9604832 Fri 18:20:16 1999
player-6.0-9909291386.rpm A 7391228 Oct 20:18:11 1999
MSSPRINT_2 A 41315 Apr 23 22:22:00 1999
MSSPRINT_A 36013 Apr 23 22:22:00 1999
MSSPRINT_3 A 49761 Apr 23 22:22:00 1999
MSSPRINT_4 A 55837 Apr 23 22:22:00 1999
Phatlinux32.zip A 190371364 Nov 4 20:34:48 1999
knvwer-0_3_tar.gz A 159923 Nov 5:21:38 1999
``````

smb: \staroffice> mget *.inf

Get file SPRINT.INF y

getting file SPRINT.INF of size 41315 as SPRINT.INF (568.262 kb/s)

(average 382.173 kb/s)

Get file SPRINT.INF y

getting file SPRINT.INF of size 36013 as SPRINT.INF (567.24 kb/s)

(average 400.243 kb/s)

Get file SPRINT.INF y

getting file SPRINT.INF of size 49761 as SPRINT.INF (578.508 kb/s)

(average 421.07 kb/s)

Get file SPRINT.INF y

getting file SPRINT.INF of size 55837 as SPRINT.INF (586.325 kb/s)

(average 439.997 kb/s)

smb: \staroffice> 

    64322 blocks of size 131072. 31365 blocks available
```

- `more`——`more` 的工作类似于 Linux 中的 `more` 命令。它允许一次一页读取 Windows 机器上的文件。
- `mput <expression>`——此命令与 `mget` 命令一样，只是它从 Linux 机器复制文件到 Windows 机器。上述 `mget` 的规则适用于 `mput`。
- `newer <filename>`——允许仅复制比 `filename` 更新的文件。例如，获取比 linux core 更新的文件：
- `print <file>`——此命令使用 Linux 机器的打印服务在 Windows 机器上打印文件。通过使用 `put` 命令将文件复制到打印池目录来实现（见打印章节）。
- `put <local file> [remote file>`——此命令类似于 `get`，但它从 Linux 机器复制文件到 Windows 机器。`get` 的所有规则适用于 `put`。
- `pwd`——它的工作类似于 Linux 命令 `pwd`。它显示 Windows 机器上的当前目录。
- `queue`——可以使用此命令查看 Windows 机器上的打印队列。
- `rd <directory>` 或 `rmdir <directory>`——从 Windows 机器上删除目录。你必须拥有删除目录的权限且该目录必须为空。如果不为空，你将收到以下错误：

```
smb: \staroffice> newer

Getting files newer than Sun Nov 7 13:19:06 1999

smbb: \staroffice>
```

```
smb: \> rd staroffice

ERRDOS ERRaccess (Access denied.) removing remote directory file

\staroffice

smbb: \>
```

- `recurse`——此命令强制 `du`、`mget` 和 `mput` 进入子目录。`smbclient` 打开时它是关闭的。要开启它，输入 `recurse`：

```
smb: \> recurse

directory recursion is now on

smb: \>
```



- 如果开启了递归，使用 `mask` 命令指定由 `mget` 或 `mput` 复制的文件。
- `rm<expression>`——删除 Windows 机器当前目录下所有匹配表达式的文件。
- `setmode<file> [a b g r i X]>`——它的工作类似于 Windows 中的 `attrib` 命令。它允许你如下所示更改 Windows 机器上文件的属性：

+ 添加属性。
- 删除属性。
- `r`——读取属性。设置后，将文件变为只读。
- `s`——系统属性；用于系统文件。
- `h`——隐藏属性；使文件隐藏。
- `a`——归档位；当文件需要备份时设置该文件的归档位。

- `tar <cx> [a b g r i X]>`可以从 Windows 机器备份或恢复文件。与 `smbclient` 的 `-t` 命令行选项完全相同。
- `full`——备份所有文件，无论归档位如何。
- `inc`——备份带有归档位的文件。
- `reset`——重置所有备份文件的归档位。
- `system`——备份带有系统位的文件。
- `hidden`——备份带有隐藏位的文件。
- `verbose`——备份期间显示状态。
- `quiet`——备份期间不显示任何信息。

- `translate`—当从 Windows 机器复制文件时，`translate` 将转换

Windows 换行符会被转换为 Linux 换行符。这使得文本文件可以在 Linux 系统上正常读取。

### 14.3 smbtar

由于 `smbclient` 的 `tar` 命令非常复杂，Samba 包含了 `smbtar` 脚本以简化备份和恢复。`smbtar` 的格式如下：

`smbtar` 选项 文件
`smbtar` 的选项如下：

- `-s server`—指定你正在备份的服务器（Windows 机器）。此选项是强制性的。
- `-p password`—如果需要，这是共享的密码。
- `-x service`—要连接的服务。默认值是 `backup`。
- `-X filenames`—从备份中排除的文件。
- `-u user`—连接到服务的用户名。默认值是你当前登录 Linux 的 Linux 用户名。
- `-d directory`—开始备份或恢复的初始目录。
- `-t tape`—用于备份或恢复的设备或文件。默认是 Linux 中设置的 `tape` 变量。如果没有 `tape` 变量，则使用 `tar.out` 文件。
- `-b blocksize`—磁带块大小。默认值为 20。
- `-N filenames`—指定备份少于 `filenames` 的文件。
- `-i`—执行增量备份。仅备份设置了归档位（archive bit）的文件。
- `-a`—重置所有备份文件的归档位。
- `-r`—执行恢复而非备份。
- `-l log level`—指定调试级别。默认值为0。这与 `smbclient` 中的 `d` 选项效果相同。
- `-v`—将 `smbclient` 设置为详细模式（verbose）。
- `filenames`—在没有 `x` 参数的情况下，你可以列出要备份的文件。如果没有列出文件名，将默认为所有文件名。

### 14.4 smbprint

这是另一个 `smbclient` 脚本，允许在连接到 Windows 机器的打印机上打印 Linux 文件。它接收 Linux 机器上的标准输入并将其重定向到远程打印机。语法类似于：

```
smbprint <local.file>
```

### smbfs

为了让 `smbprint` 正常工作，必须创建一个包含以下参数的 .config 文件：

- `-s server`—Windows 机器的名称。
- `service`—共享名称。
- `- password`—如果需要，这是共享所需的密码。

### 14.5 smbfs

Server Message Block 文件系统 (`smbfs`) 允许你像挂载 Linux 或 UNIX 驱动器一样挂载 Windows 机器上的驱动器。挂载 Windows 驱动器需要两点：

1. Linux 内核中的 `smbfs` 支持。
2. 用于挂载和卸载 `smbfs` 的程序。

大多数当前的 Linux 发行版都内置了 `smbfs` 支持。如果你的内核没有 `smbfs` 支持，你需要重新编译带有 `smbfs` 支持的内核或使用 `load-module`。由于内核和内核模块超出了本书的范围，请咨询你的文档或良好的 Linux 书以了解如何操作。

一旦添加了内核对 `smbfs` 的支持，你需要使用 `smbmount` 和 `smbmount` 工具在你的 Linux 机器上挂载和卸载 Windows 共享。`smbmount` 使用与 `smbclient <share <mount point>>` 相同的命令行参数。命令的通用语法是 c 共享 在 Windows 上的别名，假设我们想在 Linux 驱动器的挂载点 `/mnt/alisa` 上挂载 c 共享。

```
smbmount //alisa/c /mnt/alisa

Added interface ip=10.0.0.2 bcast=10.0.0.255 nmask=255.255.250

[root@mmcune client]# #
```

我们现在更改挂载目录并运行 `ls`：

```
[root@mmcune alias]# cd /mnt/alisa

[root@mmcune alias]# ls -l

total 20230

-drwxr-xr-x 1 root      root 512 Aug 6 14:31 Acrobat3

-drwxr-xr-x 1 root      root 76503 Nov 8 12:22 BOOTLOG.PRV

-drwxr-xr-x 1 root      root 76127 Nov 8 12:35 BOOTLOG.TXT

-drwxr-xr-x 1 root      root 93890 Apr 23 1999 COMMAND.COM

-drwxr-xr-x 1 root      root 59 Nov 8 13:14 CONFIG.SYS

(deleted brevity)

[root@mmcune alias]#
```

注意，它看起来就像一个 Linux 目录。尽管 Windows 机器不支持与 Linux 相同的权限，但它仍然遵循标准的 Linux 权限。`smbfs` 模拟了权限。被列为可写的文件可能是只读的，反之亦然。如果你不小心，可能会导致问题。

`smbfs` 还有另一个主要问题。如果挂载的 `smbfs` 驱动器丢失与 Windows 机器的连接，挂载的驱动器将锁定，在重启 Linux 机器之前无法卸载或挂载。这个问题可能会在未来的 `smbfs` 版本中得到解决，但目前这是一个恼人的问题。

### 14.6 Sharity

解决 `smbfs` 死锁问题的方法是使用 `sharity`。`sharity` 是一个独立的程序，而不是像 `smbfs` 那样内核的一部分。它还允许通过 NFS 导出 SMB 共享。

缺点是 `sharity` 不文件锁定，并且经常在文件句柄上遇到问题，导致偶尔出现 NFS 文件错误。

`sharity` 有两个版本：`sharity` 和 `sharity-light`。`sharity` 是一个需要许可的商业程序。`sharity-light` 是该程序的 GPL 版本，缺少 `sharity` 的许多高级功能，例如：

- 加密密码。
- 从同一台服务器挂载多个共享。
- 显示正确的修改日期。
- 提高性能的各种缓存策略。
- 重叠请求提高性能。
- 自动挂载功能。
- 更好的文件操作映射。
- 多用户操作。
- 支持国际字符集。
- 可以链接到安全数据传输（在测试版版本 0 中首次实现）。

`sharity` 和 `sharity-light` 的语法与 `smbfs` 相似。`sharity-light` 的基本语法为：

```
sharity //server/service mount-point [options]
```



有关完整的选项列表，请访问 `ftp://dev.at/Products/Sharity-Light/README`。

`sharity` 的首页位于 `http://www.dev.at/Products/sharity.html`，而 `sharity-light` 的首页位于 `http://www.dev.at/Products/sharity-light.html`。

### 14.7 结论

绕过 `smbfs` 死锁问题的方法是使用 `sharity`。`sharity` 是一个独立的程序，而不是像 `smbfs` 那样是内核的一部分。它还允许通过 NFS 导出 SMB 共享。

缺点是 `sharity` 不支持文件锁定，并且经常在文件句柄上遇到问题，导致偶尔出现 NFS 文件错误。

`sharity` 有两个版本：`sharity` 和 `sharity-light`。`sharity` 是一个需要许可的商业程序。`sharity-light` 是该程序的 GPL 版本，缺少 `sharity` 的许多高级功能，例如：
- 加密密码。
- 从同一台服务器挂载多个共享。
- 显示正确的修改日期。
- 提高性能的各种缓存策略。
- 重叠请求提高性能。
- 自动挂载功能。
- 更好的文件操作映射。
- 多用户操作。
- 支持国际字符集。
- 可以链接到安全数据传输（在测试版版本 0 中首次实现）。

`sharity` 和 `sharity-light` 的语法与 `smbfs` 相似。`sharity-light` 的基本语法为：

```
sharity //server/service mount-point [options]
```

有关完整的选项列表，请访问 `ftp://dev.at/Products/Sharity-Light/README`。

`sharity` 的首页位于 `http://www.dev.at/Products/sharity.html`，而 `sharity-light` 的首页位于 `http://www.dev.at/Products/sharity-light.html`。

Windows 换行符会被转换为 Linux 换行符。这使得文本文件可以在 Linux 系统上正常读取。

### 14.3 smbtar

由于 `smbclient` 的 `tar` 命令非常复杂，Samba 包含了 `smbtar` 脚本以简化备份和恢复。`smbtar` 的格式如下：

```
smbtar 选项 文件
```

`smbtar` 的选项如下：
- `-s server`—指定你正在备份的服务器（Windows 机器）。此选项是强制性的。
- `-p password`—如果需要，这是共享的密码。
- `-x service`—要连接的服务。默认值是 `backup`。
- `-X filenames`—从备份中排除的文件。
- `-u user`—连接到服务的用户名。默认值是你当前登录 Linux 的 Linux 用户名。
- `-d directory`—开始备份或恢复的初始目录。
- `-t tape`—用于备份或恢复的设备或文件。默认是 Linux 中设置的 `tape` 变量。如果没有 `tape` 变量，则使用 `tar.out` 文件。
- `-b blocksize`—磁带块大小。默认值为 20。
- `-N filenames`—指定备份少于 `filenames` 的文件。
- `-i`—执行增量备份。仅备份设置了归档位的文件。
- `-a`—重置所有备份文件的归档位。
- `-r`—执行恢复而非备份。
- `-l log level`—指定调试级别。默认值为0。这与 `smbclient` 中的 `d` 选项效果相同。
- `-v`—将 `smbclient` 设置为详细模式。
- `filenames`—在没有 `x` 参数的情况下，你可以列出要备份的文件。如果没有列出文件名，将默认为所有文件名。

### 14.4 smbprint

这是另一个 `smbclient` 脚本，允许在连接到 Windows 机器的打印机上打印 Linux 文件。它接收 Linux 机器上的标准输入并将其重定向到远程打印机。语法类似于：

```
smbprint <local.file>
```

### smbfs

为了让 `smbprint` 正常工作，必须创建一个包含以下参数的 `.config` 文件：
- `-s server`—Windows 机器的名称。
- `service`—共享名称。
- `- password`—如果需要，这是共享所需的密码。

### 14.5 smbfs

Server Message Block 文件系统 (`smbfs`) 允许你像挂载 Linux 或 UNIX 驱动器一样挂载 Windows 机器上的驱动器。挂载 Windows 驱动器需要两点：
1. Linux 内核中的 `smbfs` 支持。
2. 用于挂载和卸载 `smbfs` 的程序。

大多数当前的 Linux 发行版都内置了 `smbfs` 支持。如果你的内核没有 `smbfs` 支持，你需要重新编译带有 `smbfs` 支持的内核或使用 `load-module`。由于内核和内核模块超出了本书的范围，请咨询你的文档或良好的 Linux 书以了解如何操作。

一旦添加了内核对 `smbfs` 的支持，你需要使用 `smbmount` 和 `smbmount` 工具在你的 Linux 机器上挂载和卸载 Windows 共享。`smbmount` 使用与 `smbclient <share <mount point>>` 相同的命令行参数。命令的通用语法是 `c` 共享 在 Windows 上的别名，假设我们想在 Linux 驱动器的挂载点 `/mnt/alisa` 上挂载 `c` 共享。

```
smbmount //alisa/c /mnt/alisa

Added interface ip=10.0.0.2 bcast=10.0.0.255 nmask=255.255.250

[root@mmcune client]# #
```

我们现在更改挂载目录并运行 `ls`：

```
[root@mmcune alias]# cd /mnt/alisa

[root@mmcune alias]# ls -l

total 20230

-drwxr-xr-x 1 root      root 512 Aug 6 14:31 Acrobat3

-drwxr-xr-x 1 root      root 76503 Nov 8 12:22 BOOTLOG.PRV

-drwxr-xr-x 1 root      root 76127 Nov 8 12:35 BOOTLOG.TXT

-drwxr-xr-x 1 root      root 93890 Apr 23 1999 COMMAND.COM

-drwxr-xr-x 1 root      root 59 Nov 8 13:14 CONFIG.SYS

(deleted brevity)

[root@mmcune alias]#
```

注意，它看起来就像一个 Linux 目录。尽管 Windows 机器不支持与 Linux 相同的权限，但它仍然遵循标准的 Linux 权限。`smbfs` 模拟了权限。被列为可写的文件可能是只读的，反之亦然。如果你不小心，可能会导致问题。

`smbfs` 还有另一个主要问题。如果挂载的 `smbfs` 驱动器丢失与 Windows 机器的连接，挂载的驱动器将锁定，在重启 Linux 机器之前无法卸载或挂载。这个问题可能会在未来的 `smbfs` 版本中得到解决，但目前这是一个恼人的问题。

### 14.6 Sharity

绕过 `smbfs` 死锁问题的方法是使用 `sharity`。`sharity` 是一个独立的程序，而不是像 `smbfs` 那样是内核的一部分。它还允许通过 NFS 导出 SMB 共享。

缺点是 `sharity` 不支持文件锁定，并且经常在文件句柄上遇到问题，导致偶尔出现 NFS 文件错误。

`sharity` 有两个版本：`sharity` 和 `sharity-light`。`sharity` 是一个需要许可的商业程序。`sharity-light` 是该程序的 GPL 版本，缺少 `sharity` 的许多高级功能，例如：
- 加密密码。
- 从同一台服务器挂载多个共享。
- 显示正确的修改日期。
- 提高性能的各种缓存策略。
- 重叠请求提高性能。
- 自动挂载功能。
- 更好的文件操作映射。
- 多用户操作。
- 支持国际字符集。
- 可以链接到安全数据传输（在测试版版本 0 中首次实现）。

`sharity` 和 `sharity-light` 的语法与 `smbfs` 相似。`sharity-light` 的基本语法为：

```
sharity //server/service mount-point [options]
```



有关完整的选项列表，请访问 `ftp://dev.at/Products/Sharity-Light/README`。

`sharity` 的首页位于 `http://www.dev.at/Products/sharity.html`，而 `sharity-light` 的首页位于 `http://www.dev.at/Products/sharity-light.html`。

### 14.7 结论

Windows 换行符会被转换为 Linux 换行符。这使得文本文件可以在 Linux 系统上正常读取。

# 150

## 第 15 章 — 使用 Samba 打印

![](img/a1ad58e4259f15e8b2826ecf57a28362_165_0.png)

图 15.4 在 PrintTool 中选择打印机。

- 远程 Unix 队列（Remote Unix Queue）——这与本地打印机相同，只需设置远程主机（Remote Host）和远程队列（Remote Queue）。远程主机是启用了 UNIX 的远程机器的名称或 IP 地址。远程队列是远程打印机的名称。此设置在远程机器上进行。
- SMB/Windows 打印机——SMB 打印选项允许安装了 Linux 的机器连接 Windows 机器上的共享打印机。这包含一些额外设置：
  - 打印服务器主机名（Host Name of Printer Server）——此主机名必须解析为 IP 地址。
  - 服务器 IP 号（IP Number of Server）——如果你在解析主机 IP 地址时遇到问题，请使用此项。
  - 打印机名称（Printer Name）——打印机的共享名称。
  - 用户（User）——如果需要，主机机的登录名。
  - 密码（Password）——仅用于登录。
  - 工作组（Workgroup）——如果需要，主机机所处的工作组。

## 15.2 测试打印机

- NetWare (NCP) 打印机——这允许 Linux 机器打印到 Novell NetWare 服务器。要使用此项，你必须在 Linux 上安装 NetWare 支持。它包含以下额外设置：
  - 打印机服务器名称（Printer Server Name）——NetWare 打印服务器的名称。
  - 打印队列名称（Printer Queue Name）——NetWare 打印服务器上队列的名称。

测试菜单（Test Menu）下有一些选项可以帮助诊断打印机。如果你有本地打印机，尝试“直接打印 ASCII 到端口”（Print ASCII directly to port）选项（不支持远程或 SMB 打印机）。如果无效，请检查线缆和打印机配置。此外，检查你是否选择了正确的端口（`lp0`、`lp1` 等）。

接下来，尝试“打印 ASCII 测试页”（Print ASCII test page）。如果无效，请检查 `lpd`（Linux 的打印程序）是否已加载，并确保远程打印机运行正常且设置正确。菜单上有一个重启 `lpd` 的选项（见图 15.5）。

![](img/a1ad58e4259f15e8b2826ecf57a28362_166_0.png)

图 15.5 使用 PrintTool 重启 `lpd`。

接下来，尝试“打印 PostScript 测试页”（Print PostScript test page）。如果 ASCII 测试页有效但 Postscript 不行，说明你的打印机驱动程序存在问题。确保你选择了正确的输入过滤器（或驱动）。接下来，检查 Ghostscript 是否安装正确。如果不是如此，请尝试不同的过滤器。许多打印机兼容其他打印机驱动程序。请参考上述网站的打印机兼容性和 Ghostscript 故障排除。

有时，关闭“抑制页眉”（Suppress Headers）选项可能会导致打印机不打印。如果打印机仍然不工作，请尝试开启它。

如果你在纯文本打印机上看到阶梯状文本，尝试开启“修复阶梯”（Fix Stair Stepping）选项。如果打印机看起来正在接收数据（大多数打印机都有闪烁的数据灯）但什么都没有打印，请尝试开启“发送 EOF”（Send EOF）选项。

惠尔惠惠德（HP）JetDirect 打印机需要在队列选项上将非文本输出作为原始格式发送，这在 JetDirect 端口上设置。JetDirect 打印机带有直接连接到网络的端口的 HP 打印机。

要设置 JetDirect 卡，请设置打印机的 IP 地址。这是通过面板面板菜单完成的。请参阅打印机说明书。

设置 JetDirect 卡有两种方法。一种是简单的 `telnet` 到 JetDirect 卡的 IP 地址，输入 `?` 获取帮助或查看当前设置列表。一旦连接，更改列出的参数，输入：`参数名: 设置`。

对于更高级的管理工具，请访问 `http://www.hp.com/support/net_printing` 并下载 Linux 版本的 HP JetAdmin（见图 15.6）。这将允许你从窗口管理 JetDirect 卡。

![](img/a1ad58e4259f15e8b2826ecf57a28362_167_0.png)

图 15.6 Linux 版 HP JetAdmin。

## 15.3 配置 Samba 用于打印

一旦配置了 JetDirect，在 `printtool` 中将其设置为远程 UNIX (`lpd`) 队列。确保留“输入过滤器”（Input Filter）字段为空。

一旦设置了 `printcap` 文件，为 Samba 设置打印机唯一需要的操作是在 `smb.conf` 文件中添加 `[printers]` 部分。

```
[printers]

path = <path of spool file>

printable = yes
```

这些是 `[printers]` 部分的参数。这将加载 `printcap` 并允许 Samba 打印。

如果不处理好，某些细节可能会导致 Samba 打印失败。确保 `path` 参数中的目录对所有人可写。这允许 Samba 将其打印文件写入该目录。如果 `path` 变量不可写，请使用 `chmod` 修改权限：

```
chmod 622 <path of spool file>
```

此外，`/dev/null` 需要是可写的。如果 `path` 变量不可写，请使用 `chmod` 修改权限：

```
chmod 622 /dev/null
```
（注：原文后续存在大量重复的 OCR 错误信息，已清理并保留核心技术指令。）

## 15.4 自动驱动安装

Samba 服务器允许安装打印机。当打印机时，请参见图 15.7。

![](img/a1ad58e4259f15e8b2826ecf57a28362_169_0.png)

图 15.7

```
Datasection: UNI_DATA

Datafile: PCL5EMS.DRV

Driverfile: PCL5EMS.DRV

Helpfile: UNIDRV.HLP

LanguageMonitor: PJL Language Monitor
```

将以下文件拷贝到你的打印机共享位置：

- `PCL5EMS.DRV`
- `PJLMON.DLL`
- `UNIDRV.DLL`
- `UNIDRV.HLP`
- `ICONBL.DLL`
- `FINSTALL.DLL`
- `FINSTALL.HLP`

`HP LaserJet 5:PCL5EMS.DRV:PCL5EMS.DRV:UNIDRV.HLP:PJL Language Monitor:EMP:PCL5EMS.DRV,PJLMON.DLL,UNIDRV.DLL,UNIDRV.HLP,(for Windows NT and LL,FINSTALL.DLL,FINSTALL,FINSTALL.HLP`

这些文件需要从现有的 Windows 95/98 上拷贝。首先，在机器上安装适当的驱动程序。然后在 PC 上找到这些文件。大多数文件位于 `\windows\system`（针对 Windows 9x）或 `\winnt\system32`（针对 Windows NT 和 200）。如果不在，请使用图 15.8 所示的功能查找它们：

![](img/a1ad58e4259f15e8b2826ecf57a28362_171_0.png)

图 15.8 Windows 查找程序。

一旦配置完成，在 `printtool` 中使用 `restart lpd` 选项重启 `lpd` 进程。然后重启 Samba：

```
samba stop

samba start
```



像往常一样，测试安装以确保一切正常工作。当 Windows 95/98 PC 连接到 Samba 打印机共享时，你会看到一个请求安装打印程序的屏幕对话框（图 15.7）。

这应该安装打印机驱动程序。如果没有，请检查拼写错误和明显的错误。你也应该能够打印到共享打印机。如果没有，请使用本章之前使用的故障排除步骤。

# 第 16 章 在 Linux 和 Windows 中使用 NFS 和 NIS

NFS 是原生的 UNIX 协议，允许 UNIX 机器通过网络共享驱动器。它执行了微软 SMB 协议的一些功能。NFS 是一个简单得协议，因为它不包含身份验证和打印功能。身份验证由 UNIX（或 Linux）主机处理，打印功能由 `lpr` 和 `lpd` 处理。

NFS 是混合网络的一个良好协议。它不仅用于 Linux 和所有其他形式的 UNIX，还适用于所有主要的操作系统，包括大型机、中型机和 PC 的操作系统。它比 SMB 简单得多，因此使用的系统和网络资源更少。它不是持久连接，这意味着如果 NFS 客户端失去了与 NFS 服务器的联系，它将在服务器上线时重新连接。

Linux 内核中拥有（内置的）NFS 支持，以及管理 NFS 的工具。NFS 允许 Linux 机器与另一台机器共享驱动器或目录（作为服务器）。它允许 Linux 机器在其他机器上挂载驱动器（作为客户端）。

Windows 不支持 NFS，但有许多第三方程序为 Windows 添加 NFS 支持。将 Windows 机器连接到机器的方法有两种：一种是在每台 Windows 机器上加载 NFS 程序；另一种是使用一台机器作为 NFS 机器和 Windows 机器之间的网关。这些程序和方法将在本章稍后讨论。

## 16.1 设置 Linux 为 NFS 服务器

将 Linux 设置为 NFS 服务器将允许你共享 Linux 机器上的驱动器和目录。虽然 Linux 发行版包含了 NFS 支持，但仍然需要进行设置。

需要做的第一件事是启动 `portmap` 服务。大多数发行版默认启动 `portmap`。要查看 `portmap` 是否已启动，输入：

```
rpcinfo -p

program vers proto port

100000 2 tcp 111 portmapper

100000 2 udp 111 portmapper
```

你应该能看到 `portmapper` 连接到 `tcp` 和 `udp` 端口。如果 `portmapper` 未启动，你需要将其添加到 `init` 脚本中。你可能需要检查手册或参考书查看如何这样做，因为这随发行版而异。`portmapper` 程序名为 `portmap`、`rpc` 或 `rpcbind`，位于 `/sbin` 或 `/usr/sbin` 目录。`init` 脚本位于 `/etc/rc.d`、`/etc/init.d` 或 `/etc/rc.d/init.d`。

例如，在 Red Hat Linux 发行版中，你会将脚本 `portmap` 添加到 `/etc/rc.d/init.d` 目录。Red Hat 自带的 `portmapper` 脚本如下：

```bash
#! /bin/sh

# portmap          Start/Stop RPC portmapper

# chkconfig: 345 11 89

# description: The portmapper manages RPC connections, which are used by \
#               protocols such as NFS and NIS. The portmapper server must be \
#               running on machines which acts as servers for protocols \
#               make use of the RPC mechanism.
```

## 16.2 在 Linux 上使用 NFS 客户端

这是一个对 NFS 的非常简单的解释，涵盖了基础知识。有整本书都在专门介绍 NFS 的细节。

为了让 NFS能够工作，内核中必须构建 NFS 支持。大多数发行版都已经在内核中内置了 NFS 支持。如果没有，则需要通过重新编译内核或添加 NFS 内核模块来添加 NFS 支持。如前所述，重新编译内核超出了本书的范围。有很多书籍提供了关于编译内核的详细介绍，或者你可以访问 `http://www.ibiblio.org/mdw/HOWTO/Kernel-HOWTO.html` 了解有关编译内核的详情。

一旦在内核中激活了 NFS，就可以直接使用 `mount` 命令来访问远程 NFS 驱动器：

```
mount -o rsize=4096,wsize=4096 mmcune:/mnt/home/alisa /mnt/alisa
```

当然，你必须是 `root` 或等效用户才能使用 `mount` 命令。让我们来看这些参数的含义：

- `-o` 表示有可以跟随的选项。
- `rsize`—以字节为单位的读缓冲区大小。
- `wsize`—以字节为单位的写缓冲区大小。
- `mmcune`—NFS 服务器的名称。
- `/mnt/home/alisa`—服务器上的 NFS 目录。
- `/mnt/alisa`—挂载 NFS 目录的本地目录。

### 16.2.1 优化 NFS

可以对 `rsize` 和 `wsize` 参数进行优化以获得更高的速度。遗憾的是，唯一的方法是不断尝试。通常情况下，`rsize` 和 `wsize` 应该在不牺牲可靠性的情况下尽可能大。大多数时候，保持这些值的默认值更好。

优化 `rsize` 和 `wsize`。从 `rsize` 和 `wsize` 为 `1024` 开始，观察拷贝一个大文件（64MB 或更大）需要多长时间。重复几次并取平均时间。然后将 `rsize` 和 `wsize` 的值各增加 `1024`，并重复此过程，直到两个值都达到 `16,384` 字节。

在确定了这些值的最佳大小后，我们需要确保它们是可靠的。这相当难以察觉到。尝试运行几个命令。然后尝试大文件。如果程序在没有错误消息的情况下终止或失败，那么说明 `rsize` 和 `wsize` 太大，需要调小。大多数 Linux 系统在 `rsize` 和 `wsize` 均为 `4096` 时性能最佳，尽管你的结果可能会有所不同。

### 16.2.2 硬挂载与软挂载

NFS 如何处理连接丢失同样重要。有硬挂载（hard mounts）和软挂载（soft mounts）。软挂载会向访问 NFS 卷的程序发送错误。某些程序可以处理这种情况，但大多数不能。

在大多数情况下，硬挂载是更好的选择。它会挂起任何访问 NFS 挂载的程序。它通过 `intr` 选项添加，该选项会停止使用 NFS 挂载的程序。在大多数情况下，硬 `intr` 是最佳选项。

一旦确定了各种选项，就可以将其添加到 `fstab`。`fstab` 是 Linux 中定义驱动器参数的地方。`fstab` 条目按此顺序排列，用空格分隔：驱动器、挂载点、文件系统类型、逗号分隔的选项、dump 和 fsck 顺序。例如：

```
mmcune:/mnt/home/alisa  /mnt/alisa  nfs
size=4096,hard,intr 0
```



在此示例中，NFS 驱动器是服务器 `mmcune` 上的目录 `/mnt/home/alisa`。`rsize` 和 `wsize` 为 4096 字节，并设置了 `hard` 和 `intr` 选项。`dump` 和 `fsck` 都被设置为 0，因为这不是本地驱动器。

## 16.3 在 Windows 上使用 NFS

任何版本的 Windows 都没有内置 NFS 支持，尽管有许多附加程序允许 Windows 充当 NFS 服务器或客户端。两个著名的商业软件包是 Hummingbird 的 NFS Maestro 和 NetManager 的 Chameleon NFS。微软还为 Windows NT 制作了一个“Windows for UNIX”附加包。还有十几个其他软件包，每个包都有其优缺点。我不会涵盖所有它们，但我将为你提供一个如何实现 NFS 的概述。大多数为 Windows 制作 NFS 软件的公司都提供评估版，因此你可以在决定是否使用之前先查看该软件包。

我将介绍微软的“Windows for UNIX”附加包，因为这个包经常安装在 NT 机器上，并且在混合 Windows 和 Linux（或 UNIX）环境中是必须的。

### 16.3.1 在 Windows NT 上设置 NFS 服务器

要在 Windows NT 机器上创建 NFS 共享，请控制面板并选择要共享的驱动器或目录。NT 上的驱动器在 NFS 共享中显示为 `/drive/`。例如，NT 上的 `D:` 盘在 NFS 共享中显示为 `/D/`。你可以使用别名（`aliases`）使名称更易于管理。例如，共享驱动器 `/D/public/user/share` 可以别名为 `share` 以便于记忆。别名的唯一问题是，别名在生效之前需要重启服务器。

你还可以在 NFS 共享上设置客户端组。这简化了 NFS 共享的管理，因为它允许以组为单位对用户进行管理。请注意 `sec`

### 16.3.2 设置 NFS 客户端

在 Windows 上设置 NFS 客户端。使用 Windows for UNIX 附加包。首先，在控制面板中选择。在 NFS 共享上，使用 Network Information Services (`NIS`) 或 NFS Daemon (`NFSD`)。首先，设置 NFS 客户端。如果你使用 `NIS`，选择。下一步，选择 NFS 客户端。像 Linux 客户端一样，硬挂载通常更好。Windows NFS 客户端也支持版本 3。如果 NFS 服务器支持版本 3，这将提供显著的性能提升。缺点是 NFS 服务器崩溃会导致。

名称映射在混合 Windows 和 Linux 环境中非常重要。Linux 区分大小写，而 Windows 将它们视为相同。例如，Linux 会认为 `Sample.txt` 和 `sample.txt` 是不同的文件名，但 Windows 会认为它们是相同的文件。有几种方法设置名称映射，但最简单的方法让 Windows 客户端在读取时忽略大小写。

NFS 客户端支持服务器上的符号链接（`symbol links links` 符号链接指向另一个文件的文件。它类似于 Windows 上的快捷方式。它可以指向本地文件，甚至是另一台机器。默认情况下，Windows 客户端不会解析或删除未解析链接。它不允许重命名或删除符号链接。除非你有理由，否则不要更改。重命名或删除符号链接除非你理解符号链接的工作原理。例如，如果你删除一个符号链接并创建一个同名的文件，它就不再是符号链接。你将有两个文件，而不是一个指向另一个文件。

### 16.3.3 使用 Windows 连接到 NFS 服务器

你可以通过在客户端输入 `show mounts <servername>` 来查找服务器上的 NFS 共享。然后可以使用 Windows 语法或 UNIX 语法连接到共享。例如，服务器 `mmcune` 上的 `home` 共享可以从命令行以两种不同的方式挂载。这样做是为了兼容 UNIX 和 Windows 系统。

```
use * \mmcune\home (使用 Windows 语法)
```

```
use * mmcune:/home (使用 UNIX 语法)
```

一旦完成，共享看起来和用起来就像系统上的任何其他网络驱动器一样。

Windows 和 Linux 的模型是不同的。Windows 用户可以属于多个组，而 Linux 用户一次只能属于一个组。这通常不会引起任何问题，但在某些情况下，它可能会导致问题。如果这是一个问题，你可以使用 `chgrp` 来更改组 ID。

Windows for UNIX 提供了名称映射服务。它作为标准服务运行，并将 UNIX ID (`UIDs`) 映射到 Windows ID (`SIDs`)。它在下表中的表中维护映射：

| Windows Username | Windows Domain | UNIX Username | UNIX Domain | UID/GID |
| :--- | :--- | :--- | :--- | :--- |
| JohnDoe | Indwinds | Johnd | Indux | 1090/2 |
| Maryjane | Indwinds | Maryj | Indux | 223/1 |

Windows 有几种商业化的 NFS 实现。它们的优势是可以在 Windows 95/98 下运行。其中一些商业程序包括 Hummingbird Maestro (`http://www.hummingbird.com/products/nfs/`)、NetManager (`http://www.netmanage.com/products/`)、Omni NFS (`http://www.xlink.com`) 和 Access NFS (`http://www.ssc.com`)。如果你想尝试，这些商业程序在他们的网站上提供了演示。

有一个免费的 Windows NFS 实现叫做 `NFSnt`。它没有商业程序那样的功能，但非常易于安装。它在 `http://www.com` 可以找到。它是开源的，因此可以。

# 在 Linux 上设置 NIS 服务器

用于共享 NFS 挂载。对于 Windows 客户端来说，该 NFS 共享 `own` 就像服务器上的普通共享。

对于 Windows NT，你将需要诸如 Hummingbird NFS Maestro Gateway、Access NFS Gateway 和 Reflections NFS Gateway 等程序。这些程序允许 Windows 机器通过运行网关软件的 Windows NT 机器连接到 NFS 导出。

## 16.3.5 NFS 安全

有许多广泛使用的工具可以利用 NFS 的安全漏洞。任何与外部的连接都应该通过防火墙或其他安全设备进行。

这不一定是 NFS 的功能，但是一个良好的通用安全策略。编辑 `/etc/inetd.conf` 文件并注释掉任何你不需要的服务。任何服务都代表着潜在的安全风险。例如，`logind` 和 `rexec` 允许你登录并执行远程程序。如果这些很方便但你不需要，请注释掉下面的代码：

```
#shellstreamtcpnowaitaitroot/usr/sbin/tcpd.rshd
```

```
#loginstreamtcpnowaitaitroot/usr/sbin/tcpd.rlogind
```

```
#execstreamtcpnowaitaitroot/usr/sbin/tcpd.rexec
```



此外，确保你的系统上所有程序都是最新版本和补丁。安全漏洞会以安全补丁的形式修复并发布。检查微软和你所使用的 Linux 发行版的网站以获取当前的安全服务。同时检查 `http://www.cert.org` 或 `http://www.security.com` 以获取当前的安全建议。

关于 NFS 特定的安全问题，请特别关注 `/etc/exports` 文件。以下是根据 `CERT advisory-94:15` 提取的七条导出规则：

- 1. 不要在 NIS 服务器的导出文件中对其自身进行自引用。
- 2. 不要允许导出文件包含 `"localhost"` 条目。
- 3. 仅向需要的主机导出文件系统。
- 4. 仅向完全限定主机名（fully-qualified host names）导出。
- 5. 确保导出列表不超过 256 个字符。如果你使用了别名，列表在*别名展开后*不应超过 256 个字符。（参见 `CA-04:02.REVISED.SunOS.rpc.mount.vulnerability`。）
- 6. 使用 `showmount` 工具检查导出是否正确。
- 7. 尽可能将要导出的文件系统挂载为只读，并以只读方式导出文件系统。

## 16.4 在 Linux 上设置 NIS 服务器

如上所述，NIS 是一种集中式管理用户名、密码和用户组的方法。所有的 UNIX、Linux 变体都使用它。由于大多数发行版不附带 NIS，首先需要做的事情是下载它。当前版本可以在 `ftp://ftp.kernel.org/pub/linux/utils/net/NIS` 下载。在 `http://rpmfind.net/linux/RPM` 也有二进制的 RPM（红帽软件包管理器）文件可用。只需搜索 `nis-server` 并选择版本号最高的即可。

在安装 NIS 之前，你必须确保 `portmap` 正在运行（见上文）。让时间服务也运行也是一个好主意。可以通过遵循 `/etc/inetd.conf` 中的行来启动它。

要安装 NIS 服务器，首先提取文件。压缩包的名称类似于 `psyserv-1.3.9.tar.gz`。按照以下方式解压压缩包：

```
gunzip psyserv-1.3.9.tar.gz
tar xvf psyserv-1.3.9.tar
```

这应该创建一个名为 `yp-1.3.9` 的目录。编译 `psyserv` 有两种方法：使用 TCP Wrappers 或 securenet。这些程序允许你限制访问 NIS 数据库的计算机。默认是 `securenet`。你也可以使用 TCP Wrappers，它的可配置性更高，但配置起来更复杂且问题更多。TCP Wrappers 还存在内存泄漏问题，可能会导致系统问题。为了演示之目的，我们将使用 `securenet`。

进入 `yp-1.3.9` 目录并输入 `./configure`。如果这是一个主（master）NIS 服务器，你需要编辑 `/var/yp/Makefile`。主 NIS 服务器将存储 NIS 数据库的主副本。如果这是唯一的 NIS 服务器，它显然将成为主服务器。从（slave）NIS 服务器将存储主数据库的副本。在大型网络中，如果为了与主服务器分担负载，或者当到主服务器的网络连接缓慢时，可以使用从服务器。

如果你正在运行主 NIS 服务器，请特别注意 `all` 部分。这里是设置被放入 NIS 数据库的地方。添加和删除任何需要共享的信息。`all` 部分的默认设置如下：

```
all: passwd hosts rpc services netgroup map \
shadow publickey # networks ethers bootmaps printcap \
# home.host.* master.host passwd.adjunct
```

完成后，进入对象目录。它的名称类似于 `<os version>`。输入 `make install`。这应该编译 NIS 所需的所有程序。

编译 NIS 之后，你需要编辑配置文件 `/var/yp/securenet` 和 `/etc/yperv.conf`。这些文件可能在 `psyserv-1.3.9` 目录中，并可能需要移动到正确的目录。

`securenet` 允许你限制可以访问 NIS 数据库的主机。默认允许所有访问，这并不是我们想要的。默认的 `securenet` 文件如下所示：

```
# securenet 此文件定义了对你的 NIS 服务器的访问权限
# 对于 NIS 客户端。此文件包含网掩码/网络
```

`securenet` 允许你限制可以访问 NIS 数据库的主机。默认允许所有访问，这并不是我们想要的。默认的 `securenet` 文件如下：

```
# securenet 此文件定义了对你的 NIS 服务器的访问权限
# 对于 NIS 客户端。此文件包含网掩码/网络
```

## 在 Linux 上设置 NIS 客户端

接下来，运行 `rpcinfo -u localhost ybind`，应该会得到以下结果：

接下来，运行 `ypcat passwd.byname`，这将向你显示整个 NIS 数据库。这应该确认 NIS 客户端正在正常工作。随后可以将其添加到 `/etc/rc.d/init.d` 中。

有一个可选的配置文件可以添加到 `/etc/nsswitch.conf`，它决定了 NIS 条目的查找顺序。该文件的功能与 `/etc/host.conf` 为 TCP/IP 主机名所执行的功能相同。下面的示例文件提供了一个良好的起点：

```
#
# /etc/nsswitch.conf
#
# 示例名称切换配置文件。该文件应该
# 将最常用的服务排在最前面。
#
# 条目 '[NOTFOUND=return]' 意味着如果上一个条目的搜索
# 没有返回结果，则停止对该条目的搜索。注意，如果搜索由于其他
# 原因（例如没有 NIS 服务器响应）而失败，则将继续搜索
# 下一个条目。
# 合法的条目有：
nisplus          使用 NIS+ (NIS 版本 3)
nis             使用 NIS (NIS 版本 2)，也称为 YP
dns             使用 DNS (域名解析服务)
files            使用本地文件
db               使用 /var/db 数据库
[NOTFOUND=return]  如果在下方未找到则停止搜索
passwd          compat
group:           compat
# 对于 libc5，你必须使用 shadow: files nis
shadow:          compat
passwd_compat: nis
group_compat: nis
shadow_compat: nis
hosts:
services:       nis [NOTFOUND=return] files
networks:       nis [NOTFOUND=return] files
protocols:      nis [NOTFOUND=return] files
rpc:             nis [NOTFOUND=return] files
ethers:         nis [NOTFOUND=return] files
netmasks:       nis [NOTFOUND=return] files
```

## 16.6 Windows 的 NIS 支持

```
netgroup: nis
bootparams: nis [NOTFOUND=return] files
publickey: nis [NOTFOUND=return] files
automont: files
aliases: nis [NOTFOUND=return] files
```



最后的一点：NIS 对影子密码（`Shadow passwords`）的支持并不良好。Linux 通常使用影子密码来增加密码安全性。由于它们没有为 NIS 提供任何额外的安全性，最好不要在 NIS 中使用影子密码。请参阅用户手册了解有关影子密码的详细信息以及你的发行版是否使用了它们。

Windows 不能作为 NIS 服务器，但 `NISGina` 是适用于 Windows NT 的可用 NIS 客户端。`GINA`（图形化识别与认证）是 Windows NT 的登录屏幕。`NISGina` 将 Windows NT 中的 `msgnina.dll` 替换为它自己的版本登录程序 `nisgina.dll`。在设置 `NISGina` 时要非常小心。如果设置错误，将把你锁在电脑之外并导致电脑无法使用！（参见 http://www.ldv.ei.tum.de/software/nisgina/）。

首先，下载并解压文件。`NISGina` 的最新版本使用 `Install Shield` 自动安装。以下是手动安装的说明。

假设 Windows NT 安装在 `/winnt` 目录（默认目录），以管理员身份登录，并将 `*.dll` 和 `*.exe` 文件复制到 `/winnt/system32` 目录。首先，通过输入以下命令安装 `portmap`：

```
installservice portmap \winnt\system32\portmapservice.exe
```

你应该会收到服务已成功安装的消息。创建目录 `\winnt\var\run` 和 `\winnt\var\yp`。接下来，启动 `portmap` 服务：

```
net start portmap
```

安装 `ypbind` 并指定它将使用 `portmap` 服务：

```
installservice ypbind portmap \winnt\System32\ypbindservice.exe
```

现在，需要修改几个注册表项。最简单的方法是使用 `NisConfig.exe`，我们稍早将其复制到了 `\winnt\system32` 目录。某些版本会在控制面板上显示图标。启动此程序后，进入 NIS 标签页（见下图 16.2）。

![](img/a1ad58e4259f15e8b2826ecf57a28362_188_0.png)

设置 NIS 域、密码映射（`Password Map`）和组映射（`Group Map`）。你一次只能配置一个 NIS 域。一旦设置了 NIS 域，启动 `ypbind`：

```
net start ypbind
```

接下来，我们将使用熟悉的 NIS 工具测试 CIS：`ypwhich.exe`、`ypcat.exe` 和 `ypmatch.exe`。这些文件稍早已复制到 `/wind/system32` 目录。`ypwhich` 将返回 NIS 服务器的主机名或 IP 地址。如果没有返回，请检查 NIS 服务器是否正常工作以及 NIS 域是否正确。`ypcat <password map>` 将显示 NIS 密码文件。如果没有显示，请确保密码映射正确。例如，如果密码映射为 `passwd.byname`，则命令为：

```
ypcat passwd.byname
```

`xp_port 2f8. Add 10.0.0.1, port 805`

`mmcune:x:500:Mike McCune:/home/mmcune:/bin/bash`

其余部分为了简洁已删除。



最后，我们将使用 `ymatch` 查找：
（此处由于原文内容重复已按要求处理）

## 第17章 • 在 Windows 中实现 FTP、telnet 以及其他 Unix 协议

| quit | struct ascii | form | mode | quote |
| :--- | :--- | :--- | :--- | :--- |
| system bell | get | modtime | recv | unique binary |
| glob | mput | regret | tenex bye | hash |
| newer | rstatus | tick case | help | nmap |
| rhelp | trace cd | idle | nlist | rename |
| type cd | image | ntrans | reset | user cmd |
| lcd | open | restart | umask case | ls |
| prompt | rmdir | verbose | macdef | passive |
| runique | ? delete | mdelete | proxy | send |

这些命令中有很多很少使用。你需要知道 `get` 和 `put` 会将文件从服务器传输到本地机器（下载），而 `put` 将文件从你的本地机器传输到 FTP 服务器（上传）。你还可以使用 `mput` 和 `mget` 传输多个文件。

## 17.1 为 Windows 设置 FTP 服务器

对于 Windows NT，你必须安装 Internet 信息服务（IIS）。操作方法是转到“开始 -> 程序 -> Microsoft Internet Server（常用程序） -> Internet 信息服务器设置”。在这里安装 FTP 服务。

安装 FTP 服务后，转到“程序 -> Microsoft Internet Server（常用程序） -> Internet 信息服务器管理器”。打开此程序时，你将看到服务列表。双击“FTP 服务”将打开 FTP 属性配置实用程序。第一个标签页是“服务”。在此标签页下：

- TCP 端口：默认为 21。除非你有充分理由更改它，否则请保持为 21。
- 连接超时（Connection Timeout）：这是空闲连接被断开之前的秒数。默认的 900 在大多数情况下都可以用。如果你的连接慢且由于超时被中断，请增大它。
- 最大连接数（Maximum Connections）：默认值为 1000。如果你的系统能够处理该负载，可以调高；如果不能，则需要降低。
- 允许匿名连接（Allow Anonymous Connections）：匿名连接登录使用的账户。请根据该账户设置相应的规则。
- 仅允许匿名连接（Allow Only Anonymous Connections）：不允许任何其他用户进行 FTP 连接。
- 注释（Comment）：这不影响任何内容。用于添加备注和注释。

“消息（Messages）”允许你添加欢迎消息、退出消息和最大连接数消息。这些应该是自而易懂的。

“目录（Directories）”允许你设置 FTP 用户访问的目录。别名（alias）是目录在 FTP 客户端中的显示方式`<Home>` 别名是 FTP 客户端的根目录。例如，假设 `<Home>` 别名设置为 `c:\data` 目录。当你在 FTP 客户端输入 `cd /`（或 `cd\`）时，你进入服务器上的 `c:\data` 目录。

### 为 Linux 设置 FTP

目录标签页底部有一个复选框，用于选择 UNIX 或 MSDOS 目录列表。这决定了 FTP 客户端如何感知目录。UNIX 样式看起来像 `ls` 命令，而 MS-DOS 样式看起来像 Windows 的 `dir` 命令。

“日志（Logging）”标签页允许记录一个跟踪 FTP 活动的文件。它记录了成功和失败登录的地址，以及传输的文件。一旦开启日志，就有几个参数可以设置。它们大部分都是自而易懂的。不过关于日志文件名有一点说明：你可以使用参数 `d`（代表天）、`m`（代表月）和 `y`（代表年）根据创建日期自动命名文件。这是跟踪 FTP 日志的好方法，因为日志文件目录下可能会有很多日志文件。

“高级（Advanced）”标签页用于访问控制。它可以控制哪些计算机访问 FTP 服务。“允许访问（Granted Access）”按钮将允许所有计算机访问 FTP，列表中的计算机除外。相反，“拒绝访问（Denied Access）”按钮将阻止所有列表中的计算机以外的计算机访问 FTP。

Windows 2000 的配置略有不同。要配置 FTP，转到“开始 -> 程序 -> 管理工具 -> 配置你的服务器”。这将弹出一个左侧带有菜单的图形窗口。在“Web/媒体服务器”下，选择“Web 服务器”选项。在窗口中间，点击“启动 Windows 组件 (IIS)”链接并点击“详细信息”。勾选并启用“文件传输协议 (FTP) 服务器”。然后点击上级菜单的“确定”。选择并下一步将要复制的文件。点击“完成并退出”安装向导。

要配置 FTP 服务，转到“开始 -> 管理工具 -> Internet 服务管理器”。这将调出一个类似于资源管理器的程序。在此程序中，右键点击你的服务器图标并选择“属性”。在“主属性（Master Properties）”下拉菜单中选择“FTP 服务”，然后点击“编辑”。这应该显示与我们配置 Windows NT FTP 时相同的配置界面。

### 17.2 为 Linux 设置 FTP

FTP 是所有 Linux 和 UNIX 机器上的标准服务。大多数时候，FTP 已经在运行，但如果没有运行，启动也非常简单。只需用你喜欢的文本编辑器打开 `/etc/inetd.conf`（位置可能有所不同）并添加该行（如果已存在，则取消注释）：

```
ftp stream tcp nowait root /usr/sbin/tcpd.ftpd -l -a
```

如果 `tcpd` 不位于 `/usr/sbin` 中，你可能需要更改其路径。Linux 使用普通用户账户处理 FTP 登录。如果你愿意，可以为 FTP 访问创建一个特殊的账户和目录。

你还可以通过 `hosts.allow` 和 `hosts.deny` 文件仅允许特定主机访问远程服务来限制访问。这些是简单的文本文件，包含主机名列表，用于限制 `inetd` 启动的远程服务，如 FTP 和 telnet。

## 17.3 Linux 的 telnet 和远程服务

此服务也在 `/etc/inetd.conf` 中启动。要启动它们，添加（或取消注释）以下行：

```
telnet stream tcp nowait root /usr/sbin/tcpd in.telnet

ftp stream tcp wait root /usr/sbin/tcpd in.ftpd -l -a
```



当然，你可以使用 `hosts.deny` 和 `hosts.allow` 来限制访问这些服务的客户端。像 FTP 一样，用户访问由用户账户控制。

## 17.4 Secure Shell (SSH)

### 17.4.1 什么是 SSH？

Secure Shell (`SSH`) 为 UNIX（以及 Linux）中的远程命令提供验证和强加密。它由服务器和客户端组成。服务器运行在你连接的机器上，客户端运行在连接服务器的机器上。大多数 UNIX 系统都有免费和商业版的 SSH，且所有版本的 Windows 都有相应的客户端。

## 安全外壳 (SSH)

`SSH1` 和 `SSH2` 之间并不完全兼容，你需要决定使用哪一个。虽然 Windows 上有一个免费的 SSH 客户端，但它没有经过充分的测试和调试（意味着使用它的风险需自负）。对于 Linux 和 Windows 环境，请使用 `SSH1` 或来自 Data Fellows 或 Van Dyke 的 `SSH2` 商业版本。

### 17.4.2 它能防止什么攻击？

有多种方法可以侵入 UNIX (`Linux`) 节点。其中大多数方法基于伪装成他人或在网络上捕获身份验证数据。`SSH` 不信任任何通过网络传输的内容。网络上的攻击者只能导致 `SSH` 断开，而无法接管会话或捕获密码。以下是 `SSH` 防护的一些攻击（来自 `SSH` 常见问题）：

- IP 伪造——远程主机发送伪装成来自另一个可信主机的数据包。`SSH` 甚至可以防止本地网络上的伪造者，该者可以向外部伪装成你的路由器。
- IP 路由——主机可以伪装 IP 数据包来自另一个可信主机。
- DNS 嗅探——攻击者伪造服务器记录。
- 数据包嗅探——中间主机拦截明文密码和其他数据。
- 中间攻击——控制中间主机的人对数据进行操纵。
- X11 伪造——基于监听 X-Windows 身份验证数据和与 X11 服务器连接的攻击。

### 17.4.3 SSH 无法防止什么

如果攻击者获得了你机器的 `root` 权限，他们也可以绕过 `SSH`。访问你的主目录也会损害 `SSH` 的安全性。这就是为什么通过 `NFS` 导出主目录是一个坏主意。

### 17.4.4 适用于 Windows 的 SSH 客户端

Windows 上有多个免费和商业版的 SSH 客户端。其中一些免费实现包括：

- Robert O'Callahan 的 `TTSSH`，它是 `TeraTerm` 客户端的 `SSH1` 扩展——http://www.zip.com/~roca/ttssh.html。
- Gordon Caffee——`SSH1` 和 `scp` 的命令行端口版本——http://bmrc.berkeley.edu/~people/caffe/winntntutil.html。
- Sergey Ohapkin 移植到 32 位 Windows 的 `SSH1` 和 `SSH2` 服务器及客户端——http://www.lexa.ru/sos/。
- `PuTTY`，Simon Latham 的 32 位 Windows SSH 客户端——http://www.chiark.greenend.org.uk/~sgthatham/putty.html。
- `FiSSH`，Mass Confusion 的 Windows 用 32 位 `SSH1` 客户端——http://www.massconfusion.com/ssh/。
- Raju Mathur 编写的 `SSH 1.2.2` 的 Cynus Win32 端口——http://reality.sgi.com/raju/software.html。

设置方法随不同的包而异，请检查其附带的文档。

### 17.4.5 在 Linux 上安装 SSH1

对于大多数 Linux 程序，`SSH1` 的源码和二进制文件（编译后的程序）均可用。使用源码的优点是可以获得最新的更新，但缺点是更难安装，因为你必须进行编译。二进制文件更容易安装，但并不总是最新版本。

`SSH1` 的源码可以在 http://ftp.cs.hut.fi/pub/ssh/ 获取。如果你可以访问该地址，在 http://www.onsight.com/sh/faq/ssh-faq-2.html 列出了几个镜像站点。

`RPM` 格式的编译版本可以在 http://rpmfind.net/linux/RPM/ssh.html 获取。只需为你的系统选择最新版本即可。例如，本文中 `SSH1` 的最新版本是 `1.2.27-5`，因此指向最新版本的链接为 `ssh-1.2.27-5_us386`。

### 17.4.6 为 Linux 设置 SSH 服务器

首先要做的是禁用 `rexec`、`rsh` 和 `login` 等远程服务。这通过在 `inetd.conf` 中的相应行前添加 `#` 来实现。这可以防止用户以不安全的方式登录，否则将违背 `SSH` 的初衷。

完成后，就可以加载 `sshd`（服务器程序）。这可以通过命令行加载。在配置文件 `/etc/sshd_config` 中可以设置多个选项。要获取这些设置的详细信息，请查看 `man` 页面（在提示符中输入 `man ssh`）。命令行选项将覆盖 `sshd_config` 文件中的设置。

### 17.4.7 使用 SSH 客户端

`SSH` 是 `rcp`、`rexec` 和 `login` 的替代品。通用语法是 `ssh <远程计算机名>`。你也可以发送一个用户名（除当前输入的用户外）`ssh - <用户名> <远程计算机名>`。要执行远程命令（如 `command`），输入 `ssh <远程计算机> <命令名>`。`man` 页面上还列出了 `SSH` 的许多其他选项（输入 `man ssh`）。

`scp` 是 `rcp` 的替代品。要运行它，输入 `scp <user@host:要复制的文件> <user@host:要拷贝文件的位置>`。你可以将文件的 `user@host` 替换为本地机器。此外，为了保留文件属性，请在命令行中添加 `-p`。例如，要使用 `root` 账户从本地机器将 `/root/test.file` 复制到 `/root/` 目录，输入 `scp -p /root/test.file root@remote-host:/root/test.file`。

`SSH2` 的客户端与 `SSH1` 相同，只是结尾带有一个“2”。除了结尾带有一个“2”之外，它们是完全相同的。

## Secure Shell (SSH)

`SGI GL`、数字证书和 `PGP` 密钥。`SSH2` 支持 `PGP` 密钥，但目前不支持 `SGI GL` 数字证书。在 X11 下运行的 `OpenGL` 是受支持的。

### 17.4.9 管理 SSH

此脚本生成一个日志文件，列出诸如更改密钥的客户端或其他错误或更改。http://www.kari-lissruhe.de/-ig25/ssh-faq/comp-host-list 提供了一个脚本，它可以处理该日志文件并以更易读的格式将其写入另一个文件中。这对于发现“中间人”类型的的攻击很有帮助。

还有针对 `Kerberos` 的补丁，允许其与 `SSH` 工作。`Kerberos` 允许在不安全的网络上进行安全身份验证。这些补丁允许 `SSH` 在使用 `Kerberos` 认证时更新其加密密钥。`Kerberos 4` 的补丁位于 http://www.monkey.org/-dusong/ssh-afs，`Kerberos 5` 的补丁位于 http://www.ncsa.uiuc.edu/General/CC/ssh/patch_repository/descriptions/AFS-KR5.html。

### 17.4.10 排除 SSH 故障

防止 `SSH` 问题的最佳方法是保持其更新。`SSH` 的补丁位于 http://www.ssh.org/。下载补丁后，进入源码目录并输入 `patch -pl -1 < /path/to/sspath`（`ssh` 和 `sshd` 所在）。然后运行 `make distclean`、`configure`、`make` 和 `install` 来编译 `SSH`。

`GMP` 汇编器在某些系统上无法运行，因此编译可能会由于汇编器的错误消息而失败，因此可以在没有这些程序的情况下编译 `SSH`。如下使用 `-disable-asm` 选项配置 `SSH`：

```bash
make distclean
configure --disable-asm
make
make install
```



进入 `/path/to/xxx` 目录，找到 `xxx.json`。

当 `configure` 过程找不到 `xauth` 时，通过输入 `wherexauth` 检查 `xauth` 是否在你的路径中。如果没有显示 `xauth` 的路径，请通过 `export PATH=$PATH: <path of xauth>` 将其添加到路径。如果你不知道 `xauth` 在哪里，可以通过输入 `find xauth` 找到它。之后，再次运行 `configure`。

如果编译因关于 `libc.so.4` 的错误消息终止，说明你的系统配置不当。运行 `cd /usr/lib`，然后执行 `ln -s libc.so lib..`，然后重新编译。

## 第 17 章 • 实现 FTP、telnet 和其他 UNIX 协议

如果你在多主机（多主机简单来说指超过一个 IP 地址）上遇到问题，这通常发生在具有多个网卡作为桥接器和网关的设备上，客户端可能没有主机使用的所有 IP 地址。配置恰当的网络将解决大部分此类问题。特别，确保 DNS 服务器拥有主机的所有 IP 地址，并且客户端正在使用该 DNS 服务器。此外，执行 `nslookup` 查看所有 IP 地址是否都已出现。

还有一个 Perl 脚本，它可以加载 SSH 客户端并帮助防止多主机上的问题。我无法说它是否有效，但可能值得一试：

```bash
# 仅在 stdin 上运行 perl

/usr/local/bin/perl5 /LOCAL/etc/ssshrc.pl

# 用于所有接口的 xauth perl 脚本 - 源自 Paul Pomes 的脚本。

# 检查是否有需要添加的 cookie：

exit unless $proto_cookie = <>;

# 检查是否需要 X11 转发

exit unless ($dpy = $ENV{'DISPLAY'});

# 提取 host/dpynum 

$dpy = /(.*):(.*)\$/ || die "Bad DISPLAY $dpy";n$host = $1;

$dpynum = $2;

# 找出接口

open(INTERFACES, "/usr/sbin/ifconfig -a") || die "Cannot execute ifconfig";

$xauth = "/usr/open/bin/xauth"; open(XAUTH, "$xauth -q -") die "Cannot execute xauth";

while (<INTERFACES>) {

  if (/inet\s+([0-9.]+)/) {

    $addr = $1;

    next if $addr eq "127.0.0.1";

    print XAUTH "add $addr:$dpynum $proto_cookie";

  }

}

# 只添加一次 unix 域套（注意）- 符合默认 sshd 行为

print XAUTH "add $host/unix:$dpynum $proto_cookie";

close(XAUTH);

close(INTERFACES);
```



## 17.4 Secure Shell (SSH)

如果尽管有 `.hosts`，SSH 仍向你请求密码，你可能遇到了以下问题之一：

- 远程主机 `/etc/ssh_known_hosts` 不是全局可读的。使用命令 `chmod 0+r /etc/ssh_known_hosts` 修复。
- 客户端密钥未存储在 `known_hosts` 文件中。注意这是针对规范（通常是全限定）域名的，例如 `myhost.mydomain.com`。
- 客户端主机在服务器名称中没有反向映射。SSH 需要反向映射和正向映射才能工作。反向映射使用主机查找 IP 地址。正向映射使用主机。

# 附录

## A 磁盘错误代码

`0x00` “内部错误”——当 LILO 引导程序检测到内部不一致时，其扇区读取程序会生成此代码。这可能是由文件损坏引起的。尝试重新构建映射文件（map file）。此错误的另一个可能是尝试使用 `LINEAR` 选项访问超过 1024 的的磁道。有关如何解决问题的详细信息，请参阅“BIOS Restrictions”章节。

`0x01` “非法命令”——这不应该发生，但如果发生了，可能表示尝试访问 BIOS 不支持的磁盘。

`0x02` “未找到地址标记”——这通常表示介质问题。请重试几次。

`0x03` “写保护磁盘”——这应该发生在写入操作上。

`0x04` “未找到扇区”——这通常表示几何结构不匹配。如果你正在从原始写入的磁盘启动，请验证该磁盘是否是与你正在使用的磁盘相同的几何结构创建的。如果你从 SCSI 磁盘或大型 IDE 磁盘启动，你应该检查 LILO 是否从内核获取了正确的几何结构数据，或者几何定义是否与真实的磁盘几何结构对应。（见“Disk Geometry”章节）。移除 `COMPACT` 可能有所帮助；可以通过添加 `LINEAR`。

`0x06` “线路切换激活”——这应该是一个瞬态错误。尝试第二次启动。

`0x07` “无效初始化”——BIOS 初始化磁盘控制失败。你应该修正 BIOS 设置参数。热启动也可能有帮助。

`0x08` “DMA 溢出”——这不应该发生。尝试再次启动。

`0x09` “跨 64k 边界的 DMA尝试”——这不应该发生。尝试省略 `COMPACT` 选项。

`0x0C` “无效介质”——这不应该发生，可能由介质错误引起。尝试再次启动。

`0x10` “CRC 错误”——检测到介质错误。尝试启动几次，第二次运行映射安装程序（以将映射文件放置在某些物理位置或在坏点上写入“良好数据”），映射掉坏扇区/坏道，如果所有方法都失败，请更换介质。

`ECC` 纠正成功——发生了读取错误，但已纠正。LILO 不识别此条件并仍然终止了加载过程。第二次加载尝试应该成功。

控制器错误——这不应该发生。

寻道失败——这可能是介质问题。尝试再次启动。

LILO 附带了大量的文档。文档的通常位于 `/usr/doc/lilo-x`，其中 x 是 LILO 的版本号。

# SAMBA 文档

- GNU 许可证
- Samba 常见问题解答 (FAQ)
- 什么是 SMB？

本附录包含你可能发现对学习 Samba 有帮助的文档。

## GNU 许可证

公共领域内的软件可以遵循几种许可证格式。某些允许你转售软件，但必须支付版税。另一些仅允许你销售并从复制成本中获利。此处显示 GNU 许可证，这是你在 Linux 和 UNIX 世界中经常遇到的内容。

### GNU 通用公共许可证

第 2 版，1991 年 6 月

版权所有 (C) 1989, 1991 Free Software Foundation, Inc.
675 Mas Ave, Cambridge, MA 02139, USA

允许任何人复制和分发本文的逐字副本，但不允许对其进行更改。

前言

大多数软件的许可证旨在剥夺你分享和更改它的自由。相比之下，GNU 通用公共许可证旨在保证你分享和更改自由软件的自由——确保软件对所有用户都是免费的。本通用公共许可证适用于自由软件基金会的大部分软件以及任何其他作者承诺使用它的程序的程序。（某些其他自由基金会的软件受 GNU 库通用公共许可证保护。）

## 附录 B：Samba 文档

软件。你也可以将它应用到你的程序中。

当我们谈论自由软件时，我们指的是自由，而不是价格。我们的通用公共许可证旨在确保你有分发自由软件副本的自由（如果你愿意，可以对这项服务收费），你能够接收源代码或在想要时获取它，并且你可以在新的自由程序中更改软件或其部分；并且你知晓可以做这些事情。

为了保护你的权利，我们需要制定一些限制，禁止任何人剥夺你的权利或要求你放弃权利。这些限制转化为你分发软件副本（或在对其进行修改时）需要承担的某些责任。

例如，如果你分发此类程序的副本（无论是免费还是付费），你必须向接收者提供你所拥的所有内容。你必须确保他们接收或获取源代码。你必须向他们展示这些条款，以便他们了解自己的权利。

我们通过两个步骤保护你的权利：(1) 对软件进行版权保护，(2) 向你提供此许可证，允许你复制、分发和/或修改软件。

此外，为了保护每个作者，并且我们希望确保每个人都理解这种自由软件没有担保。如果软件被他人修改并传递，我们希望其接收者知道他们不是原始版本，这样他人引入的任何问题都不会影响原始作者的声誉。

最后，任何自由程序都不断受到软件专利的威胁。我们希望避免自由程序的重新分发者单独获得专利许可，从而使该程序变为专有。为了防止这一点，我们已经明确说明，任何衍生作品都不能包含任何专利许可。

### GNU 通用公共许可证

复制、分发和修改的条款和条件

1. 你可以根据第 3 条的条款以任何媒介（包含或不修改）、目标代码或可执行格式复制并分发程序，前提是你还必须执行以下操作之一：

a) 附带完整的机器可读源代码，该源代码必须根据第 2 条和第 3 条的条款在通常用于软件交换的介质上分发；或者；

b) 附带一份书面报价，有效期至少至少 年，向任何第三方以不超过你物理执行源码分发的成本费用提供相应源代码的完整机器可读副本，该副本应根据第 2 条和第 3 条的条款在通常用于软件交换的介质上分发；或者；

c) 如果程序在以最普通方式运行时通常是交互式的，则打印或显示适当的版权声明以及关于没有担保的通知（或者，说明你提供担保），并告知用户如何查看许可证的副本。（例外：如果程序本身是交互式的但不打印公告，则你基于该程序的作品不需要打印此类公告。）

## 附录 B：Samba 文档

c) 随附您收有关分发相应源代码的信息。（此方案仅适用于非商业分发，且仅在您根据上述 b 节以目标代码或可执行形式接收程序并附带此类要约的情况下。）

作品的源代码是该作品进行修改的首选形式。对于可执行作品，完整的源代码意味着其包含的所有模块的源代码，加上任何相关的接口定义文件、用于控制可执行程序编译和安装的脚本。然而，作为一个特殊例外，分发的源代码不包括运行该可执行程序的操作系统上由主要组件（编译器、内核等）通常以（源代码或二进制形式）分发的任何内容，除非该组件本身与可执行程序一同提供。

如果通过提供访问指定位置复制的机会来分发可执行代码或对象代码，则从相同位置提供等效的源代码访问被视为分发源代码，即使第三方未被强制在复制对象代码的同时复制源代码。

- 4. 除非本许可明确规定，否则您不得复制、修改、分许可或分发本程序。任何其他复制、修改、分许可或分发本程序的尝试均无效，并将自动终止您在本许可下的权利。然而，根据本许可从您处获得副本或权利的方，只要其部分保持完全符合规定，其许可就不会被终止。

- 5. 您无需接受本许可，除非您已签署了它。然而，没有任何内容授权您修改或分发本程序或其衍生作品。如果您不接受本许可，这些行为是法律禁止的。因此，通过修改或分发本程序（或任何基于本程序的作品），您表示您接受本许可的这样做，以及所有复制、分发或修改本程序或基于其作品的条款和条件。

- 6. 每当您重新分发程序（或任何基于本程序的作品）时，接收者自动获得原始贡献者的许可，根据这些条款和条件复制、分发或修改本程序。您不能对接收者行使本许可授予的权利施加任何限制。您不对第三方强制遵守本许可的行为负责。

- 7. 如果由于法院判决、专利侵权指控或任何原因（不限于专利问题），对您施加了（无论通过法院命令、协议或其他）与本许可条件相矛盾的条件，这些条件并不能免除您本许可条件的义务。如果您无法分发以同时满足您在本许可下的义务和任何其他相关义务，那么作为结果，您可能无法分发本程序。例如，如果专利许可允许直接或间接通过您接收副本的人免特许费地重新分发程序，那么同时满足两者和本许可的唯一方法就是停止分发本程序。

如果本节的任何部分在任何情况下被认为无效或不可执行，则该节的其余部分旨在适用，且整体在其他情况下旨在适用。

## GNU 许可

本节的目的不是诱导您侵犯任何专利或其他权利主张，或质疑任何此类主张的有效性；本节的唯一目的是保护自由软件分发系统的完整性，该系统是通过公共许可实践来实现的。许多人基于对系统一致性的应用，对该系统分发的广泛软件做出了慷慨贡献；作者/捐赠者决定其是否愿意通过任何其他系统分发软件，被许可者不能施加这一选择。

本节旨在彻底阐明被认为是本许可其他部分的结果。

- 8. 如果程序的分发和/或使用在某些国家因专利或版权接口而受到限制，将程序置于本许可下的原始版权所有者可以增加地理分发限制以排除这些国家，因此仅在未被排除的国家或国家之间允许分发。在这种情况下，本许可包含了该限制，如同写在本许可正文中一样。

- 9. 自由软件基金可能会不时发布修订和/或新版本的通用公共许可。此类版本将与当前版本相似，但在细节上可能不同，以解决新的问题或关注。

每个版本都有一个不同的版本号。如果程序指定了适用于其及“任何稍后版本”的本许可版本号，则您可以选择遵循该版本或自由软件基金发布的任何稍后版本的条款和条件。如果程序未指定指定本许可的版本号，您可以选择自由软件基金发布过的任何版本。

10. 如果您希望将程序的某些部分整合到条件不同的其他自由程序中，请写信给作者寻求许可。对于自由软件基金拥有版权的软件，请写信给自由软件基金；我们有时会对此破例。我们的决策将受到两个目标的指导：即维护我们自由软件所有衍生品的自由状态，以及促进软件的的共享和重复利用。

## 免责声明

11. 由于程序是免费许可的，在适用法律允许的范围内，程序不提供任何保证，除非书面另行说明，版权所有者和/或其他方按“原样”提供程序，不提供任何形式的保证，无论是明示还是隐含的，包括但不限于对商品性和特定用途适用性的隐含保证。程序质量和性能的全部风险由您承担。如果程序被证明有缺陷，您将承担所有必要的维修、修理或纠正成本。

## 附录 B：Samba 文档

12. 在任何情况下，除非适用法律要求或书面同意，否则版权所有者或其他方均不对因使用或无法使用程序而引起的任何损害（包括对您或第三方造成的数据损失或数据渲染不准确的损失）承担责任，即使此类所有者或其他方已被告知此类损害。条件结束

## 附录：如何将这些条款应用于新程序

如果您开发了一个新程序，并希望它具有尽可能的用途，实现这一点的最佳方法是使其成为自由软件，供大家根据这些条款进行分发和修改。

为了这样，请将以下通知附加到文件的开头，以最有效地传达免责声明；每个文件应至少包含“版权”行以及指向全名所在处的指针。

```



<用一行给出程序名称及其功能的简要说明。>

版权 (C) 19yy <作者姓名>

本程序是自由软件；您可以根据自由软件基金发布的 GNU 许可分发它/或修改它，可以是该许可的 2 版，或（根据您的选择）任何稍后版本。

本程序的分发是希望它是实用的，但没有任何保证；甚至没有对商品性或特定用途适用性的隐含保证。更多信息请参阅 GNU 许可。

您应该随本程序收到一份 GNU 通用许可副本；如果没有，请写信自由软件基金会：675 Mass Ave, Cambridge, MA 02139, USA。

以及如何通过电子邮件和纸质邮件与您联系的信息。

如果程序是交互式的，让它在交互模式启动时输出如下简短通知：

Gnomision 版本 69, 版权所有 ©19yy 姓名
Gnomision 绝对没有任何保证；详情请输入 `show w`
这是自由软件，您可以根据这些条款对其进行分发；输入 `show c` 查看详情。

条件结束

# Samba 常见问题解答

假设命令 `show w` 和 `show c` 应该显示通用公共许可协议（General Public License）的相关部分。当然，你使用的命令名称可能不是 `show w` 和 `show c`；它们甚至可能是鼠标点击或菜单项——任何适合你程序的即可。

如有必要，你应该让你的雇主（如果你以程序员身份工作）或你的学校（如果有）为该程序提供一份“版权免责声明”。以下是一个示例；请修改名称：

Yoyodoy, Inc. 此处声明对程序

<Gnomovision> (该程序对编译器进行了讽刺) 的所有权益由 James Hacker 编写。
<Ty Coon 的签名>, 1989年4月1日

Ty Coon，Vice 公司行长

本通用公共许可协议不允许将你的程序整合到专有程序中。如果你的程序是一个子程序库，你可能认为允许专有应用程序链接到该库更有用。如果你想这样做，请使用 GNU 库通用公共许可协议代替本许可协议。

## 作者注释

以下常见问题解答复制自 http://www.samba.com 的在线文档 SAMBA。它是根据上述列出的 GNU 许可证复制的。

此常见问题解答由 Samba 错误跟踪系统自动生成。因此，它包含了我们经常发送向 `samba-bugs@samba.org` 报告问题的用户的答案。请报告不准确或过时的信息，以便进行修复。

### 索引

- CRLF-LF 转换
- 已停止的 1.9.18
- 无法打开状态文件 STATUS..LCK
- 域控制器 (Domain Controller)
- 获取 NTDOM 代码
- IP 地址更改
- Linux & mmap()
- NT 事件查看器中的登录错误
- Macintosh 客户端
- NT 客客访问
- NT SP3 与加密
- NTDOMAIN 代码

### 附录 B：Samba 文档

- NetWkstaUserLogon
- 未监听调用名称
- 操作中断错误 (Op Break Errors)
- 请先阅读文档！
- PWL 文件
- 密码破解
- 披萨代券
- SMBFS 不是 Samba 的部分
- Red Hat Linux 上的 SWAT
- Samba 2.x 和 PAM (特别是 FreeBSD)
- 系统错误 1240
- 这不是帮助台
- 时间偏差 1 小时
- 陷门 UID
- Unix 权限控制访问
- 用户访问控制
- 使用 NT 浏览 Samba 共享
- Win95 或 98 与加密
- 用户访问模式下的 Win9X
- Windows98 密码
- XXX 不在用户级安全模式下
- YEK
- 大小敏感
- Comp.protocols.smb
- 不进入与安全 (Dont descend & security)
- 文件缓存
- 显示的通用图标
- Linux 2.0.x 和 smbmount
- Linux 编译问题
- 非所有者时设置时间
- Setup.exe 和 16 位程序
- Smbclient -N
- 用于其他 Unix 系统的 Smbfs
- Smbpasswd: 拒绝话请求
- Smsh 和 glibc-2.1
- Smbtar 块大小
- 取消
- Win98 运行缓慢
- 你的服务器软件不友好

## CRLF-LF 转换

我们收到许多关于由 Samba 处理 CRLF/LF 格式转换的请求。问题在于，没有简单的方法来确定哪些文件应该/可以转换，哪些绝对不能转换。

由于 Unix 和 DOS/Windows 的用法都使用 `.txt` 表示包含 ASCII 文本的文件，我们无法可靠地使用文件扩展名。`.doc` 扩展名也是如此。

Samba 的运行前提是我们应该保持所有文件不变。通过不实现 CRLF/LF 转换，我们不会对损坏任何人的文件负责。

当有人提供能够保证文件完整性的良好实现方案时，我们将抓住机会实现此功能。在此之前，该主题没有行动的预期。

## 已停止的 1.9.18

感谢你报告在使用 `samba-1.9.18` 系列代码时遇到的困难。我们遗憾的是，随着 `samba-1.9.18p10` 的发布，对 1.9.18 代码树的所有工作均已停止。

现在所有的开发工作都集中在稳定 `samba-2.0.0` 上，使其能够尽快进入稳定代码发布。

如果你能下载最新的 beta 版本并反馈你可能遇到的任何困难，我们将尽力在稳定发布之前解决它们。

我们仍然会修复 1.98p10 中的主要错误和安全漏洞，但如果问题在 2.0 tree中仍然存在，我们将修复可能会错误。

有关访问最新 CVS 源代码的信息，请参阅 http://samba.org/cvs.html

## 无法打开状态文件 STATUS..LCK

如果你在任何人连接到你的新 Samba 安装之前运行 `smstatus`，你可能会得到错误：

```
Couldn't open status file /var/lock/samba/STATUS..LCK
```

或者可能的错误：

```
ERROR smb_shm_open : open failed with code No such file or directory

ERROR: Failed to initialize share modes!

Can't initialize shared memory - exiting
```



这两个错误都是无害的。适当的文件和内存段会在你第一次连接到 Samba 时自动创建。尝试使用 `smbclient` 连接，你会发现在第一次连接后 `smstatus` 就变正常了。

# 域控制器 (Domain Controller)

> 遇到未知参数: "domain controller"
> 忽略未知参数 "domain controller"

从 1.9.18 开始，“domain controller” 参数已经发生变化。你可能不需要它，但在它的位置可能需要 `networkstation user logon = yes`。

# NTDOM 代码

域控制器代码现在已集成到主源码中。请查看 http://samba.org/cvs.html 获取信息。你可能希望加入 ntdom 邮件列表。有一个单独的常见问题解答。

# IP 地址更改

以下是一个偶尔出现的问题：
Samba 之前运行良好。更改后无法工作。
检查：

- 遵循 `DIAGNOSIS.txt` 中的所有指令。
- 检查文件是否已重新创建。

Samba 在重启时会以只读方式预加载这些文件。

# 这里的 Samba 常见问题解答 199

删除会导致 samba 启动较慢，但否则运行正常。在 Samba 2.0 中，通过存储在相关文件中已修复。

# Linux & mmap()

早期 Linux 版本不支持可写的 `mmap()`。我相信它是在内核 2.0 中引入的。

有三种解决方法：

1. 升级到更高版本的 Linux 内核
2. 编译 Samba 时不要开启 `FAST_SHARE_MODES`
3. 使用通过 SysV 共享内存提供 `FAST_SHARE_MODES` 的 Samba 1.9.18

在 Samba 2.0 中，配置将自动检测功能并仅在可用时启用内存。

# NT 事件查看器中的登录错误

NT 事件查看器中的登录错误是由 Samba 尝试检测损坏的 NT 服务器引起的。

某些 NT 服务器会对话请求接受任何用户名/密码并始终进行验证，在没有设置用户的情况下返回正面会话状态。Samba 通过在调用密码服务器时故意发送错误密码来检查这一点。如果错误密码成功，Samba 会产生错误并拒绝使用密码服务器。

如果你愿意，可以从代码中删除此检查，但由于我们还没有弄清楚为什么 NT 服务器会导致这种行为，存在启动错误并导致 Samba 不安全的风险。

未来的 Samba 将有一个新的安全选项 `security = domain`，它将使用 NT 用于域认证的相同协议（目前 Samba 使用微软文档的方法，而不是微软实际使用的方法）。一旦到位问题应该解决。

# Macintosh 客户端

> 有 Samba 的 Macintosh 客户端吗？

有的。Thurs 现在有一个名为 DAVE 的 CIFS 客户端/服务器——见 http://www.thursby.com/。请针对 Windows 95、Windows NT 和 samba 进行兼容性测试。在写作时，DAVE 的版本为 1.0.1。1.0.0 到 1.0.1 的更新可以在 Thursby 网站免费下载（finder 拷贝速度已大大提高，并包含了错误修复）。

## 附录 B：Samba

替代方案——针对多种 UNIX 机器有两种 AppleTalk 的免费实现，以及若干种商业实现。这些产品允许你原生为 Macintosh 用户运行文件服务和打印服务，而无需在 Macintosh 上进行额外支持。两个免费实现是 Netatal，http://www.umich.edu/-rsug/netatal/atklalk。Samba 为 MS Windows 用户提供的功能，这些软件包也为 Mac 提供。有关这些软件包、Samba 以及 Linux（以及其他基于 UNIX 的系统）的更多信息，请参阅 http://www.eats.com/linux_mac_win.html

## NT 客客访问

你所看到的现象是正常且刻意为之。

MS Windows NT 可以配置启用访客账户。在这种情况下，任何登录尝试都不会失败。相反，如果用户名和/或密码错误，NT 将允许用户以访客账户身份访问。在 Samba 使用 NT 系统来验证用户密码的情况下，如果 NT 服务器的访客账户已启用，那么以“root”身份登录的用户将始终通过验证，无论密码正确并授予了普通用户权限，还是密码错误且用户仅被授予了“访客”权限。

简而言之，如果我们不采取目前的做法，就无法判断密码服务器是否仅允许访客登录。如果我们只是直接接受此类服务器的验证响应，用户就可以轻松获得 Samba 服务器的“root”级访问权限。

现在，你并不真的希望我们改变目前的行为，对吧？

> > 大家好……我不知道你们是否见过这个，是否已经修复了它，或者这是我的配置问题。
> 我正在使用公司的 PDC 进行密码验证，它运行正常，但有一个小故障。
> 我们的 Samba 服务器与 PDC 之间的身份验证过程始终包含一次失败的通过尝试。
> 初始通过验证具有一个错误的用户密码（1F1F1F....）。来自 PDC 的 SMB 拒绝强制使 Samba 服务器立即发送带有正确加密的 Bell Master Domain 用户密码的第二次验证。
> 如果能消除第一次糟糕的验证尝试将就太好了。

## Samba 常见问题解答

## NT SP3 与加密

微软在服务包 3 中更改了 WinNT，拒绝连接到不支持 SMB 密码加密的服务器。

有两种主要的解决方案：

- 1. 在 Samba 中启用 SMB 密码加密。请查看 Samba 文档中的 `ENCRYPTION.txt`（这最好使用 1.9.18 之后的最新 Samba 版本）
- 2. 在 NT 中禁用此行为。请查看 Samba 文档中的 `WinNT.txt`

注意，Samba-1.9.18 及更高版本支持加密密码，无需重新编译并链接 libdes (DES) 库。请参阅 `smb.conf` 的主页以及 `ENCRYPTION.txt` 以获取有关使用加密密码的信息。

有关此主题的更多信息，请参考以下 URL：http://support.microsoft.com/support/kb/articles/q166/7/30.asp

## NTDOMAIN 代码

如果你正在尝试 NTDOMAIN 版本的 Samba，请加入 samba-technical 列表并在那里观察一段时间。我也建议你阅读列表归档。更多信息请参阅 http://lists.samba.org/。

Samba 对 NT 域控制的支持仍处于实验阶段。只有当你是一个愿意实验的程序员时才请尝试。

所有关于此实验性代码的错误报告应仅发送至 samba-technical 或 samba-ntdom 邮件列表。

针对对配置文件处理的疑虑：一旦我们的域代码稳定，我们将处理配置文件处理问题。在此之前，我们在 Samba 中记录的内容与实际效果可能会冲突。我们再次强调所有 NTDOMAIN 代码具有高度的实验性。

针对对编译问题的疑虑：主分支树的代码更新版本是 `samba-2.1.0` 而不是 `samba-2.0.0`。Samba-2.1.0 代码可能在任何时间无法编译且无法工作。请自担风险使用。

## NetWstaUserLogon

密码服务器之所以发生变化，是因为我们发现某些 NT 服务器中的漏洞允许用户如果选择一个在密码服务器上不存在的账户名，就可以不带密码登录。当账户根本不存在时，NT 密码服务器竟然在说“是的，可以登录”！添加 NetWstaUserLogon 解决了这个问题，并遵循了微软最近文档说明的关于通过验证的“推荐”方法。

在 1.9.18p3 之后版本，你可以通过 `smb.conf` 中的“networkstation user login”选项来禁用 NetWkstaUserLogon 调用。

### 未监听调用名称

> > 会话请求失败 (131,129)，myname=HOBBES destination=CALVIN 未监听调用名称

如果你在与 Samba 机器通信时遇到此信息，意味着你的全局“hosts allow”或“hosts deny”设置导致 Samba 服务器拒绝连接。

请仔细检查 `smb.conf` 全局部分中的“hosts allow”和“hosts deny”行。

### OpLock 错误

提示信息意味着要么是你其中一个客户端的网卡有缺陷，要么是一个 Windows 拒绝响应另一个想要访问已锁定文件的 Windows 客户端发出的锁中断请求（opock break）。

这也可能是反向 DNS 查询无法正常工作导致 Samba 服务器出现的问题。

> > 会话请求失败 (131,129)，myname=HOBBES destination=CALVIN 未监听调用名称
> > 我在日志文件中无论使用哪个版本，都会多次看到此错误信息，并最终系统锁死
> > 我正在 AlphaStation 255 上运行此程序
> > 在不同的 Samba 版本中见过此错误信息。

## PWL 文件

如果你担心 PWL 文件的安全性，我建议你查看 http://samba.org/pub/samba/docs/security.html

## 密码破解

> > 你能发给我 Frank Stevenson 编写破解 .pwl 文件的程序吗？
> 如果你有任何其他破解 windows 95 pwl 文件的程序，请把它们发给我，或者告诉我在哪里可以找到它们。

这些不是 Samba 的一部分——我们只提供 Samba 组件。显而易见，我们无法提供任何其他软件，例如密码破解工具。这些可以在 BugTraq 这样的网站找到。

## 披萨金券

关于披萨金券的常见问题解答：

Samba 文档中关于披萨金券的注释最初只是个玩笑。因为我对那些竟然能以各种方式成功寄送披萨金券的人们感到非常惊讶！多亏了这些慷慨的人，我度过了许多快乐的披萨夜晚！

还有人写信问如何向澳大利亚寄送披萨金券。以下是对其他人有效的方法：

- 1. 有几人成功说服了当地的必胜客餐厅向澳大利亚发送金券。显然，员工起初看你的眼神有点奇怪，但至少有 2 个人成功了！
- 2. 还有人在堪培拉（我住的地方）的一家披萨店，并在电话中提供了信用卡号。他们给我邮件告诉我应该给哪家店打电话订披萨。这在堪培拉的两家不同的店都有效——必胜客和达美乐（Dominos）。
- 3. 我收到了几张在世界各地有效的披萨金券，并开始了一个小收藏。我希望有一天在访问这些地方时，能一路吃披萨走遍那里。
- 4. 我看到好几个披萨的 .gif 文件，甚至还有漂亮的图片和纸板！

请记住，“Samba 披萨金券”这件事起初只是个玩笑。这很有趣，你完全不需要发送任何东西。没有它们我也不会饿死，也许我还能再减一点体重 ::-)

## Samba 常见问题解答

同时也请记住其他帮助 Samba 的人。如果有人特别帮助了你，请给他们发一封感谢邮件。这种行为真的非常受感谢！

总之，如果你仍然想寄披萨给我，我的地址是：

3 Ballow Crescent
Macgregor A.C.T
2615 Australia
电话: +61 2 6254 8209

最近的披萨店是 “Kippax Pizza Hut”
谢谢！

## SMBFS 不属于 Samba

我们遗憾地通知您，在 Samba 压缩包中包含 `smbmount` 和 `smbm` 是一个错误。这些程序属于 `smbfs` 软件包，并且**不**由 Samba 团队维护。我们目前正在考虑从 samba 压缩包中移除这些程序，因为它们是不断的投诉来源，而我们**没有**额外的精力来处理这些负载。

## Red Hat Linux 上的 SWAT

> > 我希望这不是我以某种方式遗漏的愚错误。我浏览了邮件存档，发现我不是唯一一个遇到这个问题的人。发生的情况如下：

这是 Sinatra 方法的工作原理：

- 1. 解压 samba 压缩包
- 2. 将目录“samba-2.0.0.beta5”重命名为“samba-2.0.0.0”
- 3. cd samba-2.0.0/packaging/redHat
- 4. sh makerms.sh
- 5. cd /usr/src/redhat/RPMS/1386
- 6. rpm -Uvh samba-2.0.0-1.1386

注意：此安装对 `inetd` 的 PID 执行了“kill-HUP”，因此 SWAT 是可用的。

- 7. 从客户端（任何客户端）启动浏览器
- 8. 访问 URL http://“samba_host”:901
- 9. 用户 = root，输入 root 密码。

## 附录 B：Samba 文档

现在你准备好配置 samba 了。

> > 首先我使用了安装程序中的 Redhat 部分，该部分使用 `rpm` 语句来构建 rpm 软件包。我安装了该包并尝试使用 SWAT，图形化 Web 界面。

如果你构建了 Red Hat RPMs，那么你只需要安装二进制 RPM，一切都应该正常工作。如果不起作用，那么你很可能遇到了 TCP/IP 配置问题，而不是 Samba 问题。

> > 这失败了，因为它假设了 `/usr/local/samba` 中的 samba 目录树以及 redhat rpm 文件安装在 `/usr/share` 或类似位置。

请解释这一说明。在 `samba2.spec` 文件中，我们没有显示对 `/usr/local/samba` 的依赖，如果你使用提供的 shell 脚本构建包，所有路径都将更改为反映标准的 Linux 路径布局。

> > 最终，在创建了一些符号链接后，我认为以与发行无关的方式编译和安装更好（即只需 `make` 和 `make install`）。好了，现在 SWAT 似乎可以工作了。但我必须把它放在演示模式，因为当它要求登录时，我不能再使用 root 密码进行 root 登录了。这对 SWAT 无效了。

但 Samba 安装程序是为那些**真的**知道自己在做什么的人设计的，因此不会尝试安装 SWAT。噢，是的，它安装了二进制文件，但它没有修改 `/etc/inetd.conf` 和 `/etc/services`。

*(注：由于原文存在大量 OCR 导致的重复，以上译文已按逻辑合并处理)*

# Samba 常见问题解答

> 问题）。在我们的任何 NT 工作站客户端上（通过修改注册表允许明文密码），一旦使用 userid 和密码通过 `\host\anyuser` 映射了驱动器，该用户随后就可以执行 `\host\root` 并 Unix 机器挂载到根目录，而无需任何身份验证……他们可以访问整台机器。

Samba **不会**次要执行你希望在你的站点上施加的安全策略。作为 Unix 系统的管理员，你有责任通过设置正确的用户、用户组和其他权限，来决定谁可以访问你的 Unix 系统。

如果你确实想限制用户使其无法连接到任何其他用户的主目录，那么你需要将你的用户主目录的 Unix 权限设置为 `drwx------` (八进制 0700)。

# 用户访问控制

> 在 Windows 中，当我在“用户模式”下设置共享时，我收到了以下消息：
> “您现在无法查看用户列表。请稍后再试。”
> 我知道你们有用于访问和别名的用户列表，但我没有读到任何支持“这些列表会控制域用户列表”这一观点的内容……

Samba 目前**不支持** Windows 9x 的用户模式访问控制，尽管我们希望在未来的发布中支持它。

# 使用 NT 浏览 Samba 共享

> WIN-NT 工作站 (nt4.0, service pack 3)
> samba 配置：
> security = user
> encrypt passwords = yes
> guest account = guest
> 在 win-nt 工作站上启动资源管理器并选择网络。我发现我的 unix 服务器正在运行 samba，但我看不到共享列表，除非我是 unix 机器 `smbpasswd` 中已知的用户。

# 附录 B：Samba 文档

> 客客账户“guest”存在于我的 unix 机器上。为了测试，我甚至让他变成了一个带有密码的普通用户。

> 通过我的网络监控器，我看到

这正是 Windows NT 的工作方式。你**必须**在尝试查看资源列表的 Windows NT 机器上有一个有效账户。如果你当前登录的账户详情与你尝试访问的 NT 机器上的账户不匹配，你将看到该机器的登录框。当你输入该/域上的账户名称以及有效密码后，即可获得资源列表。如果账户详情不正确，则不会显示资源列表。

Samba 编译时可以将 `GUEST_SESSION_SETUP` 选项设置为 0、1 或 2。默认值为 0。如果将其设置为 1 或 2，在 Samba 服务器上没有账户的 Windows NT 机器将看到资源列表。遗憾的是，客户端 Bug 意味着该选项引起的问题可能比解决的多。我们不建议你使用它。

# Win95 或 98 与加密

关于 Win95（带有 TCP/IP 更新或 OSR2 版本）、Win98 和 Samba 的 FAQ 回答：微软在发布 OSR2 版本后更改了 Win95，拒绝连接到不支持 SMB 密码加密的服务器。此更改也发布在 Win95 的 TCP/IP 更新中，并包含在我们目前为止的所有 Win98 版本中。

有两个解决方案：

- 1. 在 Samba 中启用 SMB 密码加密。参见 Samba 文档中的 `ENCRYPTION.txt`。
- 2. 在 Win95/98 中禁用此新行为。参见 Samba 文档中的 `Win95.txt`。

任何最近的 Samba发行版都包含 Samba 目录，或可以在 http://samba.anu.edu.au/pub/samba/docs/ 获取。

注意：你必须重启机器以便这些注册表更改生效。

# Win9X 的用户级访问

> 我以 NT-Server 身份运行 Samba，但有一个问题：
> 当我想在 win95 客户端上共享内容时，该客户端想要来自 NT-Server (Samba) 的用户列表。
> 我如何让 Samba 提供用户列表？

# Samba 常见问题解答

抱歉。这尚未支持。在我们发布 samba-2.0.0 一段时间后，将开始实现此功能的长期任务。目前，你不应该将你的 Win95 或 Win98 系统设置为用户级访问模式。

# Windows98 密码

请参考以下 URL：
://support.microsoft.com/support/kb/articles/q187/2/28.asp
*** 注意 ***

在完成本文中提到的注册表更改后，你**必须**重启 Windows 98 电脑才能使更改生效。

注意——解决此问题的最佳方法是在你的 Samba 服务器上启用加密密码。当 Samba 运行在加密模式时，Windows 98 与 Samba 配合良好。Samba 1.9.18 及更高版本支持加密密码，前提是在 `smb.conf` 中正确配置并创建了 `smbpassd` 文件。

要在 Samba 上启用加密密码，请阅读 Samba 发行包中的 `docs/ENCRYPTION.txt` 文件。
在 `/tools/msutil/` 你应该能找到文件：`ptxt_on.inf` 和 `ptxt_off.inf`，它们是该目录下 `mtsutil.txt` 文件的片段：

# PTXT_ON.INF - 向你的网络发送明文密码 =====================================================

出于安全考虑，Windows 98 不允许你发送明文密码。密码默认是加密的。然而，可以配置 Samba 服务器以要求明文密码。

警告：启用明文密码可能会损害安全。

要启用明文密码，请添加注册表项 `EnablePassword`（dword 类型）并将值设置为 1：

- 1. 选择 `Tools/msutil/` 目录下的 `ptxt_on.inf`。
- 2. 选择 `Tools/msutil/` 目录下的 `ptxt_off.inf`。

# PTXT_OFF.INF - 向你的网络发送加密密码 =====================================================

出于安全考虑，Windows 98 不允许你发送明文密码。密码默认是加密的。然而，可以配置 Samba 服务器以要求明文密码。

此外，你可能希望尝试在 MS Windows NT4 下创建以下注册表项的效果：



[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]

`"BufFilesDenyWrite"=dword:00000000`

`"BufNamedPipes"=dword:00000000`

`"UseOptimisticLocking"=dword:00000000`

`"DormantFileLimit"=dword:00000000`

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Linkage]

`"UtilNtCaching"=dword:00000000`

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Filesystem]

`"Win95TruncateExtensions"=dword:00000000`

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanManServer\Parameters]

`"EnableOpLockClose"=dword:000000001`

`"EnableOpLocks"=dword:000000000`

```
以下注册表项在 Windows 9X 下可能也有帮助：
[HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VdX\VREDIR]\nDiscardCacheOnOpen"=string:000000001
```

### 通用图标显示

某些 Samba 用户报告了一个问题：存储在服务器上的程序图标无法显示，而是显示为“exe”图标。这似乎是由客户端检测到与服务器的连接为“慢”所导致的。当发生这种情况时，客户端尝试通过不从远程 .exe 文件中读取图标信息来加快速度。

该问题在运行 Samba 并使用 `"security=server"` 时尤为常见。在服务器级 Samba 中，在与密码服务器通信时，会延迟协商和会话设置的响应（这是必要的）。更糟糕的是，Samba 最初会特意向密码服务器发送一个错误的密码，用以检测 NT 服务器中的一个已知 Bug，即这些服务器会对所有密码都返回“是”。NT 服务器会缓慢地返回这个错误的密码（可能是为了阻止网络上的密码破解）。这导致在建立连接时引入了大约 3 秒的延迟，该延迟足以触发 Win95 的“不显示图标”代码。

## Samba FAQ 215

我们没有针对此问题的解决方案，但我们可以说（除了外观影响外），它是无害的。

## linux 2.0.x 和 smbount

如果你读过以下内容（从 1.9.18p1 Makefile 中剪切粘贴的），你会注意到第一句特别提到，2.1.70 之前的 Linux 内核无法使用与 Samba 自带的 smbount 版本。正如文中提到的，你应该使用从列表中通过 nftp 提供的 smbfs 实用程序。

```
# 如果你使用的 Linux 内核版本为 2.1.70 及更高，你应该

# 取消下面行的注释，将 smbount 实用程序与 Samba 一起编译。如果你使用的是 Linux 内核版本 2.0.x

# 你必须使用来自以下地址的 smbfs 实用程序

# ftp://ftp.gwdg.de/pub/linux/misc/smbfs
```

## linux 编译问题

```
[snip]

> 操作系统：Linux: Slackware 3.4

[snip]

> 发生了什么：

[snip]

> 正在编译 smbpass.c

> gcc: 内部错误：程序 ccl 收到致命信号 6

> make: *** [smbpass.o] 错误 1
```

Slackware 3.4 提供的 GCC 二进制文件似乎存在问题（可能还有其他几个也是如此）。出于某种原因，它们在尝试编译 Samba 中的加密密码代码时崩溃了。有两种解决方案，第一种是短期修复，但并不总是有效；据我所知，第二种方案应该总是有效：

1. 从你的 Makefile 中删除 `FLAGS1` 中的 `-O`。
2. 下载一组新的 GCC 二进制文件（在 `ftp://sunite.unc.edu/pub/Linux` 下的某处有一个）或从源码重新编译。

## 在非所有者身份设置时间

> 如果我从工作站打开一个 Microsoft Office 的文件（例如 Word），
> 而我不是该文件的所有者，但我有权写入它，
> 如果我进行了操作，Microsoft Office 将把文件的日期更改为当前日期。

## 216

## 附录 B：Samba 文档

> 不要对文件进行任何修改。如果我是文件的
> 所有者，这种情况似乎不会出现。
> 此问题的结果是，网络上的文件
> 日期没有任何意义，因为一旦所有者以外的
> 人打开了文件，文件的日期就会更改。

这是预期的行为，是 POSIX 语义的结果。然而，你可以要求 Samba 覆盖这一点。
请参阅 `smb.conf` 手页中的“dos filetimes”选项。

## setup.exe 和 16 位程序

在 Windows NT 上从 Samba 映射的驱动器运行 16 位程序

Windows NT 重定向器在针对 Samba 或 Windows 95 映射驱动器运行并尝试运行 16 位可执行文件时存在一个 Bug。

当 16 位可执行文件的路径名包含不符合 8.3 文件名规范的目录组件时，Windows NT 将无法加载该程序并抱怨找不到程序路径。

可以证实这是 Windows NT 的 Bug 而不是 Samba 的 Bug，因为尝试用相同的路径运行相同的程序时也会重现相同的问题。在 Windows NT 映射驱动器上运行 16 位程序时，如果路径不符合 8.3 规范，Windows NT 将无法加载程序。可以证实这是 Windows NT 的 Bug 而不是 Samba 的 Bug，因为尝试用相同的路径运行相同的程序时也会重现相同的问题。在 Windows NT 映射驱动器上运行 16 位程序时，如果路径不符合 8.3 规范，Windows NT 将无法加载程序。可以证实这是 Windows NT 的 Bug 而不是 Samba 的 Bug，因为尝试用相同的路径运行相同的程序时也会重现相同的问题。在 Windows NT 映射驱动器上运行 16 位程序时，如果路径不符合 8.3 规范，Windows NT 将无法加载程序。可以证实这是 Windows NT 的 Bug 而不是 Samba 的 Bug，因为尝试用相同的路径运行相同的程序时也会重现相同的问题。

## Samba FAQ 215

我们没有针对此问题的解决方案，但我们可以说（除了外观影响外），它是无害的。

## linux 2.0.x 和 smbount

如果你读过以下内容（从 1.9.18p1 Makefile 中剪切粘贴的），你会注意到第一句特别提到，2.1.70 之前的 Linux 内核无法使用与 Samba 自带的 smbount 版本。正如文中提到的，你应该使用从列表中通过 nftp 提供的 smbfs 实用程序。

## linux 编译问题

```
[snip]

> 操作系统：Linux: Slackware 3.4

[snip]

> 发生了什么：

[snip]

> 正在编译 smbpass.c

> gcc: 内部错误：程序 ccl 收到致命信号 6

> make: *** [smbpass.o] 错误 1
```



Slackware 3.4 提供的 GCC 二进制文件似乎存在问题（可能还有几个也是如此）。出于某种原因，它们在尝试编译 Samba 中的加密密码代码时崩溃了。有两种解决方案，第一种是短期修复，但并不总是有效；据我所知，第二种方案应该总是有效：

1. 从你的 Makefile 中删除 `FLAGS1` 中的 `-O`。
2. 下载一组新的 GCC 二进制文件（在 `ftp://sunite.unc.edu/pub/Linux` 下的某处有一个）或从源码重新编译。

## 在非所有者身份设置时间

> 如果我从工作站打开一个 Microsoft Office 的文件（例如 Word），
> 而我不是该文件的所有者，但我有权写入它，
> 如果我进行了操作，Microsoft Office 将把文件的日期更改为当前日期。

## 216

## 附录 B：Samba 文档

> 不要对文件进行任何修改。如果我是文件的
> 所有者，这种情况似乎不会出现。
> 此问题的结果是，网络上的文件
> 日期没有任何意义，因为一旦所有者以外的
> 人打开了文件，文件的日期就会更改。

这是预期的行为，是 POSIX 语义的结果。然而，你可以要求 Samba 覆盖这一点。
请参阅 `smb.conf` 手页中的“`dos filetimes`”选项。

## setup.exe 和 16 位程序

在 Windows NT 上从 Samba 映射的驱动器运行 16 位程序

Windows NT 重定向器在针对 Samba 或 Windows 95 映射驱动器运行并尝试运行 16 位可执行文件时存在一个 Bug。

当 16 位可执行文件的路径名包含不符合 8.3 文件名规范的目录组件时，Windows NT 将无法加载该程序并抱怨找不到程序路径。

可以证实这是 Windows NT 的 Bug 而不是 Samba 的 Bug，因为尝试用相同的路径运行相同的程序时也会重现相同的问题。

（注：由于原文文本后半部分存在大量重复内容，译文已根据翻译要求进行了整合处理，确保不遗漏信息且不产生冗余重复。）

（此处省略原文中重复的段落翻译，以符合“不要重复输出原文”的原则，以下为针对剩余核心语义的翻译汇总：）

## 你的服务器软件不友好

当你使用 `smclient` 连接服务器时，如果遇到“你的服务器软件不友好”，这意味着 `smclient` 与服务器建立了 TCP 连接，但在打开的套接字上进行 NBT “会话请求”时得到的是乱码（或为空）。“不友好”这个词源于客户端期望规范中定义的多种错误代码之一（参见 RFC1001/1002），但得到的是完全不同的内容。这通常意味着你根本没有成功与 SMB 服务器通信，套接字连接到了其他东西。如果 Samba 是服务器，常见原因是 `smbd` 启动失败并在回答会话请求之前就退出。

## Samba FAQ 217

不，首先确保你的 `smb.conf` 中没有设置 `bind interfaces = yes`。其次，如果你的 `hosts allow = xxx.xx/`，请添加 `localhost`。

## smshb 和 glibc-2.1

`smshb` 在 Linux 系统上不支持 `glibc-2.1`，这包括 以及许多其他的 Linux 发行版。因为 glibc 维护者刻意删除了 `smshb` 工作所需的钩子。他们不喜欢用户空间文件系统。我们目前唯一的建议是使用 `smbfs`。

## smbtar blocksize

早期版本的 `smbtar` 有一个小错误，导致 `blocksize` 参数无法正常工作。这在 Samba 1.9.18 版本中已修复。

## 取订阅

有关取消或更改订阅地址的信息，请参阅 http://lists.samba.org/

# 什么是 SMB？

作者注：我为原本只有链接的项目项目添加了网页地址。除此之外，文档内容与 http://www.samba.org 提供的版本相同。

什么是 SMB？

V1.1

Richard Sharpe

1999年4月24日

Copyright ©1996,1997,1998,1999 Richard Sharpe

# 复制说明

请参阅“本文档的复制”章节，了解我关于使用本文档的政策详情。

# 免责声明

本文档试图以某种方式为参与 SMB（即将更名为 CIFS）协议的人员提供服务。我们已尽一切确保信息的准确性，但不包含任何暗示保证。对于您使用或误用这些信息而导致的任何损失或后果，Richard Sharpe 不承担任何责任。

如果您有任何意见，请发送邮件至 sharpe@ns.aus.com。

# 致谢

我要感谢 Andrew Tridjell，他建议我开始开发 smlib，引导我进入该领域；感谢 Dan Sheer 提供的许多鼓励和信息；感谢 Paul Blackman 帮助制作本页面；以及许多未获得许可许可提及的其他人士。

我还感谢许多向我发送正面评论和建设性反馈的人士。

# 商标

Microsoft, MS, Windows, Windows 95 和 Windows NT 均为微软公司的注册商标或其商标。微软公司不以任何方式认可本文档，作者与微软公司也无任何关联。

所有其他商标均为其各自所有者的唯一财产。

## 目录

- 引言
- 新增内容？
- 什么是 SMB？
- 目前可用的 SMB 客户端和服务器
- SMB 服务器
- SMB 客户端
- 网络上的更多资源
- 复制本文档

## 引言

本文档解释了 SMB 协议，并讨论了许多许多 SMB 客户端和服务器实现。本文档源于我对实现 SMBlib 的兴趣，这是一个用于 SMB 客户端例程的可移植库。

SMB 是一个重要的协议，因为有大量的 PC 运行着客户端和服务器实现。所有的 Windows for Workgroups、Windows 95 和 Windows NT 系统都在（或能够运行）作为客户端、服务器或两者运行 SMB。

# 新增内容

虽然世界上有很多新事物，但就 SMB 协议而言，可能最感兴趣的内容是 CIFS，即通用互联网文件系统（Common Internet File System）。

# 什么是 SMB？

SMB 代表 Server Block（服务器块），是一种用于在计算机之间共享文件、打印机、串口端口以及作为命名管道和邮件槽的通信抽象的协议。

我拥有的关于 SMB 协议的最早的文档是 1985 年的一份 IBM 文档。它包含了 1985 年 5 月的 IBM 个人电脑研讨会议论文。其中包含了 IBM PC 网络 SMB 协议。该协议随后由微软和其他人进一步开发。定义 SMB 协议的许多文档可以从 1987 年起的 `ftp.microsoft.com/MicrosoftNetworks/OpenNET-FILE_SHARING_PROTOCOL` 以及 `microsoft.com` 的 SMB 文档区域获取。

SMB 是一种客户端-服务器、请求-响应模式。下图说明了 SMB 的工作方式。SMB 请求-响应性质的唯一例外（即客户端请求而服务器发回响应的情况）是当客户端请求了乐观锁（oplocks），而服务器随后必须中断已授予的 oplock，因为另一个客户端请求以与已授予 oplock 不兼容的模式打开文件。在这种情况下，服务器会向客户端发送一个未请求的消息来指示 oplock 的中断。

# 什么是 SMB？

服务器将文件系统和其他资源、邮件槽（打印机、命名管道、API）提供给网络上的客户端。客户端计算机可能有自己的硬盘，但它们也想访问服务器上的共享文件系统和打印机。

客户端使用 TCP/IP（实际上是 RFC1001 和 RFC1002 中指定的基于 TCP/IP 的 NetBIOS，即）、NetBEUI 或 IP/SPX 连接到服务器。一旦建立连接，客户端就可以向服务器发送命令（SMBs），允许它们访问共享、打开文件、读取和写入文件，并通常可以执行你想对文件系统进行的任何操作。然而，在 SMB 的情况下，这些操作是通过网络完成的。

如所述，SMB 可以运行在多种协议上。下面的图显示了这一点：SMB 可以用于 TCP/IP、NetBEUI 和 IP/SPX。如果正在使用 TCP/IP 或 NetBEUI，则正在使用 NetBIOS API。

NetBIOS over TCP/IP 需要通过名称引用。微软在某些名称中称之为 NBT，在另一些中称为 NetBT（特别是在他们的 Windows NT 文档和 Windows NT 表表中）。其他人将其称为 RFCNB，微软有时将 NetBEUI 称为 NBF（NetBIOS 帧格式？）。

NetBIOS 名称。如果要在 TCP/IP 或 NetBEUI 上使用 SMB，则在许多情况下必须使用 NetBIOS 名称。NetBIOS 名称长度可达 15 个字符，通常是运行 NetBIOS 的计算机名称。微软和其他实现者坚持要求 NetBIOS 名称使用大写，特别是当作为“被调用名称”呈现给服务器时。

SMB 协议变体。自 SMB 诞生以来，已经开发了许多协议变体，以处理其所采用环境日益复杂的性。

客户端和服务器实际使用的协议变体将通过 `neg` 进行协商。第一个协议变体是核心协议（Core Protocol），被称为 PC NETWORK 1.0。它可以处理：

- 连接和断开文件连接
- 打开和关闭文件
- 读取和写入文件
- 创建和删除文件
- 搜索目录
- 获取和设置文件属性
- 锁定和解锁字节范围

随着功能的需要，引入了后续的变体。这些变体包括：

# SMB 协议变体名称

| SMB 协议变体 | 协议名称 |or |
| :--- | :--- | :--- |
| PC NETWORK 1.0 | 核心协议 | MAN1.0 定义的 SMB 版本 |
| MICROSOFT NETWORKS 1.0 | 核心协议 | 包含了具有读取和写入版本的 SMB |
| MICROSOFT NETWORKS 3.0 | LAN Manager 1.0 | 与 MAN1.0 相同，但 OS/2 错误必须转换为错误 |
| LANMAN1.0 DOS LM1.2X02 | LAN Manager 1.0 LAN Manager 2.0 | 完整的 MAN1.0。与 LM1.2X02 相同，但错误必须转换为错误 |
| LM1.2X02 DOS LANMAN2.1 | LAN Manager 2.0 LAN Manager 2.1 | 完整的 MAN2.0。与 MAN2.1 相同，但错误必须转换为错误 |
| LANMAN2.1 Windows for Workgroups 3.1a NT 0.12 Samba | LAN Manager 2.1 LAN Manager 2.1 | 完整的 MAN2.1。Windows for Workgroups 包含了 Samba 版本的 NT 0.12 的特殊 SMB |
| CIFS 1.0 | | 真正的 NT 0.12 加上一点 |

安全性。该模型定义了两个安全级别：
**共享级别**。保护性应用于服务器上的共享级别。每个共享都可以设置密码，客户端只需要密码即可访问该共享下的所有文件。这是 SMB 曾经拥有的第一个安全模型，也是核心和增强协议中提供的唯一安全模型。Windows for Workgroups 的 vserver.exe 默认实现安全级别，Windows 9 也是如此。

**用户级别**。保护性应用于每个单独的文件，并基于用户访问权限。每个用户（客户端）必须登录服务器并经过服务器验证。通过验证后，客户端拥有一个 UID，在随后所有访问服务器的操作中提交该 UID。该模型自 LAN Manager 1.0 以来可用。

**网络浏览**。网络中有许多服务器，但如果用户找不到它们，也毫无意义。客户端可以简单地配置为其环境中的服务器，但在引入新服务器或移除旧服务器时这并没有帮助。

# 什么是 SMB？

223

为了解决这个问题，引入了浏览机制。每台服务器都会广播其存在的信息。客户端监听这些广播并建立列表。在 NetBEUI 环境中，这是行的，但在 TCP/IP 环境中就会出现问题。这些问题是因为 TCP/IP 广播通常不会发送到其源子网之外（尽管某些路由器可以将广播传输到其他子网）。

微软引入了浏览服务器（browse servers）和 Windows 命名服务（WINS）来帮助克服这些问题。

CIFS：最新形态！微软与一组其他供应商（Digital Equipment, Data General, SCO, Network Appliance Corp）正在开发 SMB 协议的公共版本。预计 CIFS 1.0 本质上是经过修改的 NT LM 0.12，以便在互联网上更容易使用。

SMB 交换（SMB Exchange）。客户端和服务器交换的协议元素（请求和响应）被称为 SMB。它们具有特定的格式，请求和响应的格式非常相似。每个 SMB 由一个固定大小的头部部分和一个变长度的参数和数据部分组成。

通过 NBF 或 NetBT 连接到 NetBIOS 后，客户端已准备好向服务器请求服务。然而，客户端和服务器必须首先识别它们各自理解哪种协议变体。

客户端向服务器发送 `negprot` SMB，列出它理解的方言（dialects）。服务器响应它想要使用的方言索引，如果没有哪个方言是可以接受的，则返回 0FFFF。

除了 Core 和 CorePlus 协议之外的方言在 `negprot` 协议中提供信息，以指示它们的能力（最大缓冲区大小、规范文件名等）。

一旦建立了协议，如果需要，客户端就可以继续登录服务器。它们通过 `sessetup` SMB 执行此操作。服务器响应它们是否提供了有效的用户名/密码值对，如果是，则可以提供额外信息。响应中最重要的方面之一是登录用户的 UID。此 UID 将在连接到服务器的所有后续 SMB 中提交。

一旦客户端完成登录（在较旧的协议中——Core 和 CorePlus——客户端无法登录），客户端就可以继续连接到树（tree）。

客户端发送 `tcon` 或 `tconX` SMB，指定它们想要连接的共享网络名称，如果一切正常，服务器将返回一个 TID，客户端将在未来所有与该共享相关的 SMB 中使用该 TID。

连接到树后，客户端现在可以使用 `open` SMB 打开文件，然后使用 `read` SMB 读取文件，使用 `write` SMB 写入，并使用 `close` SMB 关闭文件。

# 目前可用的 SMB 客户端和服务器

今天有几个 SMB 客户端，以及来自一系列供应商的相对大量的服务器。

主要的客户端来自微软，包含在 Windows WorkGroups 3.x、Windows 95 和 Windows NT 中。当你使用文件管理器或 Windows 95 资源管理器时，它们最为明显，因为这些工具允许你连接到跨网络的服务器。然而，当你使用 UNC（通用命名法）打开文件时，也会使用它们。

我了解的一些其他客户端：

- 用于 Samba 的 smbclient
- 用于 Linux 的 smbfs
- SMBlib（一个正在开发中的 SMB 客户端库）

服务器实现程序来自许多来源。我了解的一些包括：

- Samba
- Microsoft Windows for Workgroups 3.x
- Microsoft Windows 95
- Microsoft Windows NT
- 来自 Digital LAN Manager（适用于 OS/2, SCO 等）的 PATHWORKS 系列服务器
- 来自 SCO 的 VisionFS
- 来自 Syntax 的 TotalNET Advanced Server
- 来自 AT&T (NCR)? 的 Advanced Server for UNIX
- 来自 IBM 的 LAN Server for OS/2

接下来两个部分将分别讨论上述每个内容。

# SMB 服务器

在讨论 SMB 服务器之前，讨论工作组（Workgroups）和域（Domains）的区别是有用的。

工作组（Workgroups）。工作组是一组维护各自安全信息的计算机集合。对于 Windows for Workgroups，每台服务器基本上处于共享级安全状态。Windows 95 可以将用户验证交由 NT 或 LAN Manager 服务器。

工作组的点在于安全性是分布的，而不是集中的。

域（Domain）。域是计算机集合，其中安全性由集中处理。通常有一个主控制器和一个备用备份域控制器。域控制器维护与用户（客户端）相关的账户样式信息，如账户名、密码、授权使用时间、所属组等。

Samba 是一个用于 UNIX、OpenVMS（最近发布，可能不太稳定）的免费 SMB 服务器，由 Andrew Tridgill 开发并由世界范围内一个松散的人员维护。Samba 运行在许多出色的变体上（Linux, Solaris, SunOS, HP-UX, ULTRIX, DEC OSF1, Digital UNIX, Dynix (Sequent), IRIX (SGI), SCO Open Server, DG-UX, AIX, BSD, NetBSD, NEXTSTEP, A/UX）。

Samba 实现 NT LM 0.12 协议方言。Samba 现在可以参与浏览并成为浏览主（breeze master）。Samba 还可以处理 Windows 95 系统的登录请求（既作为域也作为域成员）。

Samba 实现层级安全，但共享可以是公共的，访问可以映射到共享的所有者等。

# 仅仅是 SMB？ 225

微软 Windows 服务器。微软为 Windows 系列操作系统提供了许多 SMB 实现。这些不是独立的产品，而是相应版本 Windows 操作系统的不可或缺的一部分。然而，可以通过控制面板或命令行（在 DOS 中运行 `net stop server`）将它们关闭。

从 Windows 95 和 Windows NT 对 SMB 序列的反应不同的事实可以看出，微软并没有为这些每一个使用相同的代码（尽管工作组和 Windows 95 可能派自相同的代码）。

Windows for Workgroups 3.1 实现工作组 3.0a 变体，并实现共享安全。

Windows 95 实现 NT LM 0.12 协议级，并实现共享和用户安全。

Windows NT 实现 NT LM 0.12 协议级，并实现共享和用户安全。

LAN Manager 和 LAN Manager for UNIX (LM/X)。微软和 ATT 将各种 LAN Manager 版本移植到 UNIX 系统。这些代码形成了许多供应商 SMB 服务器的基础。例如：适用于 SCO 的 LM、适用于 HP-UX 的 LM Server/9000 等。

该软件的最新版本似乎是 LAN Manager for UNIX 2.2，它实现了 LANMAN2.1 协议变体。

VisionFS。VisionFS 是来自 SCO 的服务器。适用于 Solaris 2.x、HP-UX 和 SCO（包括 OpenServer 和 UNIXware）。

TotalNet Advanced Server。该产品来自 Syntax。这是一个完全 SMB 服务器，可能是第一个 UNIX SMB 服务器。在其时代，通过附加模块提供了 AppleShare 和 NetWare 服务。

Advanced Server for UNIX。在 LM 之后，NCR（曾是 ATT）（可能得到了微软的帮助）将 Windows 服务器代码移植到 UNIX，以提供与 Windows 相同的功能。

PATHWORKS。PATHWORKS 是数字公司的一个产品名称。它包含了服务器和客户端，服务器运行在：

VAX 和 Alpha VMS

DEC OS/1 适用于 AXP 和 Digital UNIX（重名为 DEC OSF/1）

OS/2

客户端运行在 DOS、Windows、Windows for Workgroups、Windows NT 和 Windows 95 上，并在下方解释。

Digital 的客户端和服务器通过 DECNet 作为 TCP/IP 以及最近的 NetBEUI 实现 SMB。SMB over DECNet 规范从未发布。

Digital 最初的 PATHWORKS 服务器用于 VAX/VMS，并实现 CorePlus 协议（MICROSOFT NETWORKS 1.03 方言）。该产品经历了多个版本，最终达到了 4.2 版本。一段时间后，出了一个适用于 UL 的版本。

# 附录 B：Samba 文

TRIX 在 ULTRIX V1 中被称为 PATHWORKS，其最高版本为 1.3。这两个产品系列都是内部开发的。

随后，Digital 使用了 AT&T 和微软的 LAN Manager for UNIX (LM/X) 代码。该代码发布了针对 OpenVMS 的 PATHWORKS V5.0 (LAN Manager) 以及针对 Digital UNIX 的 PATHWORKS V5.0 (LAN Manager)。该产品实现了 UNIX 版 LAN Manager V2.2 以及它所识别的最高 SMB 方言，即 LANMAN2.1（以及 DOS LANMAN2.1）。每个产品名称末尾括号中带有 LAN Manager 的原因是因为这些产品也支持 NetWare 功能。

PATHWORKS V5 能够加入基于 Windows NT 的域，尽管只能作为备份域控制器或成员服务器。

最近，Digital 宣布了用于 UNIX 的 PATHWORKS V6.0（高级服务器），该版本基于 AT&T 的 ASU（UNIX 高级服务器）产品。

OS/2 的 LAN Server。这是一个 IBM 产品，似乎某种程度上源自其 LAN Manager 代码。

# SMB 客户端

目前有多种 SMB 客户端：

- 微软客户端
  - Windows NT
  - Windows 95
  - Windows 工作组版 3.11
- Digital 的 PATHWORKS 客户端
- Samba 的 smbclient
- Linux 的 smbfs
- SMBlib

# 网上更多资源

以下是你可以访问的与 SMB 协议相关的其他网页：

- Samba
  http://samba.anu.edu.au/samba
- SMBlib
  http://samba.anu.edu.au/samba/smblib
- SCO 的 VisionFS
  http://www.sco.com/products/visionfs
- Syntax 的 TotalNET Advanced Server
  http://www.syntax.com/totalnet/tasbody2.htm
- Digital 的 PATHWORKS 产品
  http://www.digital.com/info/pathworks
- 微软的 Windows NT 产品
  http://www.microsoft.com/NTServer

什么是 SMB？

IBM 的 LAN Server 产品
http://www.austin.ibm.com/pspinfo/lsinfo.html
IBM 与 AIX PC 集成
HTTP://www.austin.ibm.com/resource/technology/aixpncint.html
Data General 对 UNIX 高级服务器的支持
http://www.dg.com/products/html/dg_ux/00948 Lsm entry
smbfs
http://www.boutell.com/lsmbid.cgi/u00948 Lsm entry
（以及 smbfs ftp ftp://ftp.gwdg.de/pub/linux/misc/smbfs location）

CIFS 首页
http://www.microsoft.com/intdev/cifs
Network Appliance 对 CIFS 的支持
http://www.netapp.com/level3b/news_rel_960613.html

HP 在企业级 HP-UX 平台上发布 NT Server 操作系统
http://www.hp.com/pressrel/api/96/08apr96d.htm
AT&T GIS 宣布 UNIX 高级服务器系统
http://www.att.com/press/0894/940822.nca.html

Thursby 的 Dave，用于微软网络的的 Macintosh 客户端软件
http://www.thursby.com
Solstice LM 服务器
http://www.sun.com/sunsoft/solstice/Networking-products/lmserver.html

Triteal 的 TEDfs，一种用于 CDE (Unix) 机器的 SMB 服务器
http://www.triteal.com/WinTex/evalguide/index.html

# 复制本文档

我曾请求许可在其他材料中使用本文档。在其中一种情况下，我被询问是否有人可以将此文档作为附录包含在书中。在另一种情况下，我被询问是否可以将此文档提供给客户和潜在客户。在这两种情况下，我都觉得请求是合理的。

我对这些问题的看法是，本文档是为了阅读而编写的。然而，我要求你向我发送电子邮件说明你的用途并请求我的许可。

反馈

本文档将不定期更新。如果你有任何意见，请随时发送电子邮件至 sharpe@ns.au.com

请访问 NS Computer Software and Services P/L 了解更多关于我所在地的信息。

版权所有 1996, 1997, 1998, 1999, Richard Sharpe
最后更新于 1999年4月24日。

# SAMBA 手册

- Lhosts(5)
- Nmbd
- Samba(7)
- Samba.conf
- Smbclient(1)
- Smbd(8)
- Smbpasswd(5)
- Smbpasswd(8)
- Smbstatus(1)

以下是在操作 Samba 时可能对你有帮助的手手册。

# Lmhosts (5)

# Samba

# 1998年10月23日

# 名称

Lmhosts—Samba NetBIOS hosts 文件

# 概要

Lmhosts 是 Samba NetBIOS 名称到 IP 地址的映射文件。

# 描述

此文件是 Samba 软件包的一部分。Lmhosts 是 Samba NetBIOS 名称到 IP 地址的映射文件。它与 /etc/hosts 文件格式非常相似，但主机名部分必须对应 NetBIOS 命名格式。

# 文件格式

这是一个 ASCII 文件，每行包含一个 NetBIOS 名称。每行的两个字段之间通过空格分隔。任何以 # 开头的行会被忽略。Lmhosts 文件包含以下信息：

- IP 地址—十进制格式。
- NetBIOS 名称—最多十五字符，后面跟着可选的 '#' 字符，然后是 NetBIOS 类型（十六进制数字）。
- 如果省略了 '#'，则将为给定的名称返回给定的 IP 地址。

```



192.9.200.1 TESTPC
192.9.200.20 NTSERVER#
192.9.200.21 SAMBASERVER



包含三个 IP 到 NetBIOS 名称的映射。第一行和第三行将分别用于查询 `"TESTPC"` 和 `"SAMBASERVER"`。第二个映射仅在指定 NetBIOS 名称时返回。
`nmbd` 的默认位置取决于 `smbconf`。

# 版本

本手册版本为 2.0。

# 参见

- `smbconf(5)`
- `smbclient(1)`
- `smbpasswd(8)`
- `samba(7)`

# 作者

原始 Samba 软件由 Andrew Tidwell 创建。手册由 Jeremy Allison 更新。意见请邮件至 `samba-bugs@samba.org`。

# 名称

`nmbd`—Samba NetBIOS 服务器

# 概要

```
nmbd [-D] [-o] [-H lmhosts] [-d debuglevel]
```

# 描述

此程序是 Samba 软件包的一部分。`nmbd` 是一个提供 NetBIOS 命名的 NetBIOS 服务器。基本上意味着它将作为一个 WINS 数据库，创建接收到的请求数据库并对这些查询进行回复。

此外，`nmbd` 还可以作为 WINS 代理，将不理解 WINS 协议的客户端广播查询转发到 WINS 服务器。

# 参数

- `-D` 如果指定，此参数导致 `nmbd` 作为守护进程运行。它会脱离并在后台运行，在相应的端口处理请求。默认情况下 `nmbd` 不作为守护进程运行。
- `-a` 如果指定此参数，每个新连接会将日志消息追加到日志文件中。这是默认设置。
- `-o` 如果指定此参数，日志文件打开时将被覆盖。默认情况下，日志文件将追加。
- `-H lmhosts` `lmhosts` 文件是 NetBIOS 名称到 IP 地址的列表，由 `nmbd` 服务器加载，并根据 `smbconf(5)` 中的名称解析顺序解析任何所需的 NetBIOS 名称。注意，`nmbd` 不使用此文件的内容来回答任何查询。此文件的默认路径在构建 Samba 时已编译进去。常见的默认路径有 `/usr/local/samba/lmhosts`, `/usr/local/samba/lmhosts` 或 `/etc/lmhosts`。请参阅 `lm-hosts(5)` 了解此文件内容的详情。
- `-d debuglevel` 是 0 到 10 的整数。

如果未指定此参数，默认值为 0。
此值越高，日志文件中关于服务器活动的记录细节就越详尽。在 0 级下，仅记录关键错误和严重警告。
1 级是日常运行的合理级别——它会生成有关已执行操作的少量信息。
1 以上的级别将产生大量的日志数据，应仅在调查问题时使用。3 以上的级别专供开发人员使用，并会产生海量的日志数据，其中大部分内容极其晦懂。
请注意，在此处指定此参数将覆盖 `smb.conf(5)` 文件中的日志级别参数。

- `logfile`: `-l` 参数指定一个路径和文件名，运行中的 `nmbd` 服务器的运行数据将记录到该文件中。通过在指定的基准名称后附加扩展名 `".nmb"` 来实现。例如，如果指定的名称为 `"log"`，那么则 `log.nmb` 将包含调试数据。默认日志文件路径在构建过程中被编译到 Samba 中。常见的默认值有 `/usr/local/samba/var/log.nmb`、`/usr/samba/var/log.nmb` 或 `/var/log.nmb`。
- `primary NetBIOS name`: 此选项允许你覆盖 Samba 自身使用的 NetBIOS 名称。这与在 `smb.conf` 文件中设置 NetBIOS 名称参数相同，但它会覆盖 `smb.conf` 文件中的设置。
- `-p UDP port number`: UDP 端口号为一个正整数值。此选项更改 `nmbd` 响应名称查询的默认 UDP 端口（通常为 137）。除非你是专家，否则不要使用此选项，如果是专家的话，你就不需要帮助了！
- `-s configuration file`: 默认配置文件名在构建时设置，通常为 `/usr/local/samba/lib/smb.conf`，但这在 Samba 自动配置时可能会被更改。
- `-i scope`: 这指定了 `nmbd` 在生成 NetBIOS 名称时使用的 NetBIOS 范围（scope）。有关 NetBIOS 范围使用的详细信息，请参阅 `rfc1001.txt` 和 `rfc1002.txt`。NetBIOS 范围极少使用，只有当你是负责所有通信的 NetBIOS 系统的系统管理员时，才设置此参数。
- `-h print`: 此命令打印 `nmbd` 的帮助信息（用法）。

## Files

`/etc/inetd.conf`

如果服务要由 `inetd` 元守护进程运行，则此文件必须包含适用于该守护进程的启动信息。

`/etc/rc`

（或你的系统使用的任何初始化脚本）。

如果在启动时作为守护进程运行服务器，则此文件需要包含适当的服务器启动序列。

`/usr/local/samba/lib/smb.conf`

这是 `smb.conf` 服务器配置文件的默认位置。系统安装此文件的其他常见位置还有 `/usr/samba/lib/smb.conf` 和 `/etc/smb.conf`。

当作为 WINS 服务器运行时（参阅 `smb.conf(5)` 手页中的 `wins support` 参数），`nmbd` 将将 WINS 数据库存储在 Samba 安装目录下 `var/locks` 目录中的 `wins.dat` 文件中。

如果 `nmbd` 充当浏览主（browse master）（参阅 `smb.conf(5)` 手页中的 `local master` 参数），`nmbd` 将将浏览数据库存储在 Samba 安装目录下 `var/locks` 目录中的 `browse.dat` 文件中。

## 信号

为了关闭 `nmbd` 进程，建议不要使用 `SIGKILL (-9)`，除非作为最后的手段，因为这可能会导致名称数据库处于不一致状态。终止 `nmbd` 的方法是发送一个 `SIGTERM (-15)` 信号并等待它自行退出。

`nmbd` 会接受 `SIGHUP`，这将导致将其名称导出到 `/usr/local/samba/var/locks` 目录下的 `amelist.debug` 文件（或 Samba 安装目录下的 `var/locks` 目录）。这还会导致 `nmbd` 将其服务器数据库导出到 `log.name` 文件中。此外，可以通过发送 `SIGUSR1` (`kill -USR1 <nmbd-pid>`) 提高 `nmbd` 的调试日志级别，通过发送 `SIGUSR2` (`kill -USR2 <nmbd-pid>`) 降低级别。此举允许在正常低日志级别运行时，诊断客户端问题。

## 版本

本页适用于 Samba 套件的 2.0 版本。

## 另请

`inetd(8)`, `nmbd(8)`, `smb.conf(5)`, `smclient(1)`, `testpam(1)`, `testprns(1)`, 以及 Internet RFC 的 `rfc1001.txt`, `rfc1002.txt`。此外，CIFS（以前称为 SMB）规范可以通过网页上的链接获取：`http://samba.org/cifs/`

## 作者

原始 Samba 软件及相关工具由 Andrew Triggell (`samba-bugs@samba.org`) 创建。Samba 现在由 Samba 团队作为一个开源项目进行开发，类似于 Linux 内核的开发方式。
原始 Samba 手页由 Karl Auer 编写。手页源码由 Jeremy Allison 转换为 YODL 格式并针对 Samba 2.0 发布进行了更新。

# 摘要

Samba

# 描述

Samba 软件是一系列程序集合，它为 UNIX 系统实现了服务器消息块（通常缩写 SMB）协议。该协议有时被称为通用互联网文件系统 (`CIFS`)、LanManager 或 NetBIOS 协议。

# 组件

Samba 由多个组件组成。每个组件都在单独的手页中描述。强烈建议你阅读 Samba 附带的文档和手页。

## 录 C: Samba 手页

- `smbd`: `smbd(8)` 守护进程为 SMB 客户端提供文件和服务，例如 Windows 95/98、Windows NT 或 LanManager。该守护程序的配置文件请参阅 `smbd.conf(5)`。
- `nmbd`: `nmbd(8)` 守护进程提供 NetBIOS 名称和浏览支持。该守护程序的配置文件请参阅 `smb.conf(5)`。
- `smclient`: `smclient(1)` 程序实现了一个类似 ftp 的客户端。这对于访问其他服务器（如 Windows NT）上的 SMB 共享非常有用，也可以用于 UNIX
- `testparam`: `testparam(1)` 工具允许你测试 `smb.conf(5)` 配置文件。
- `testprns`: `testprns(1)` 工具允许你测试 printcap 文件定义的打印机。
- `smbustatus`: `smbustatus(1)` 工具允许查看 `smbd(8)` 服务器的当前连接。
- `nmblookup`: `nmblookup(1)` 工具允许对 UNIX 机器进行 NetBIOS 查询。
- `make_smbcodepage`: `make_smbcodepage(1)` 工具允许为 `smbd(8)` 服务器创建 SMB 页定义文件。
- `smbpasswd`: `smbpasswd(8)` 工具允许你更改 Samba 和 Windows NT(tm) 服务器的 SMB 加密密码。

## 可用性

Samba 套件根据通用公共许可证 (`GPL`) 许可。该许可的副本应随包中的 `COPYING` 文件一起。我们鼓励分发 Samba 套件，但请遵守此许可条款。

可以通过匿名 ftp 从 `samba.org` 的 `pub/samba/` 目录获取最新版本的 Samba 套件。它在世界的多个镜像站点也可用。

你还可以在新闻组 `comp.proto-cols.samba` 和 Samba 邮件列表找到有关 Samba 的有用信息。加入邮件列表的详情位于 Samba 附带的 `README` 文件中。

如果你可以使用 WWW 查看器（如 Netscape 或 Mosaic），你还可以在 `http://samba.org/samba/` 找到大量有用信息，包括 Samba 邮件列表的历史存档。

# 版本

本帮助页适用于 Samba 套件 2.0 版本。

# 贡献

如果你希望为 Samba 项目做出贡献，我建议你加入 `samba@samba.org` 的 Samba 邮件列表。详情信息请访问网页 `http://samba.org/listproc` 了解如何操作。

如果你有补丁要提交或要向他们报告问题，可以直接邮寄至 `samba-bugs@samba.org`。请注意，由于该软件包非常受欢迎，Samba 团队可能需要一些时间来回复邮件。我们倾向于使用 `diff -u` 格式的补丁。

# 致谢

项目的贡献者众多，在此无法一一列出，但他们值得所有 Samba 用户的感谢。要查看完整列表，请访问 `ftp://samba.org/pub/samba/alpha/change-log` 查看预-CVS 版本的更改，访问 `ftp://samba.org/pub/samba/alpha/cvs.log` 查看 CVS 之后的 Samba 贡献者。CVS 是 Samba 团队用于开发 Samba 的开源源码系统。如果没有它，该项目将无法管理。

此外，几家商业机构现在通过资金和设备为 Samba 团队提供支持。详情请参阅 Samba 网页 `http://samba.org/samba/samba-thanks.html`。

# 作者

原始 Samba 软件及相关工具由 Andrew Tridgill 创建，邮箱：`samba-bugs@samba.org`。Samba 现在由 Samba 团队作为一个开源项目开发，类似于 Linux 内核的模式。

原始的 Samba 帮助页由 Karl Auer 编写。帮助页源码由 Jeremy Allison 转换为 YODL 格式（另一项优秀的开源软件，可在 `ftp://ftp.icce.rug.nl/pub/unix/` 获取），并为 Samba 2.0 版本进行了更新。邮箱：`samba-bugs@samba.org`。

# smb.conf (5)

Samba

1998年10月23日

## 名称

`smb.conf`—Samba 套件的配置文件

## 概要

`smb.conf`，`smb.conf` 文件是 Samba 套件的配置文件。`smb.conf` 包含 Samba 程序的运行配置信息。`smb.conf` 文件设计用于通过 `swat(8)` 程序进行配置和管理。此处提供了该文件格式及其中可能参数的完整描述以供参考。

## 文件格式

文件由节和参数组成。节以方括号中的节名开始，并持续到下一个节开始。节包含如下格式的参数：

```
[/content]
```



`name = value`

文件是基于行的——也就是说，每一行以换行符结束的行代表注释、节名或参数。

节名和参数名不区分大小写。

参数中第一个等号是有效的。第一个等号前后的空格会被忽略。节和参数名开头、结尾和内部的空格无关。参数值开头和结尾的空格会被忽略。参数值内部的空格将原保留。

任何以分号（`';'`）或井号（`'#'`）字符开头的行都会忽略，仅包含空格的行也是如此。

任何以 `'\'` 结尾的行按照传统的 UNIX 习惯在下一行“延续”。

参数中等号后面的值可以是字符串（不需要引号）或布尔值，布尔值可以给为 `yes/no`、`0/true/false`。布尔值不区分大小写，但在字符串值中会保留。某些项目（如创建模式）是数字型的。

# 节描述

配置文件中的每个节（`[global]` 节除外）描述一个共享资源（称为“共享”）。节名是该共享资源的名称，节内的参数定义了共享的属性。

有三个特殊的节：`[global]`、`[homes]` 和 `[printers]`，它们在“特殊节”下描述。以下说明适用于普通节描述。

一个共享由一个被授予访问权限的目录以及授予该服务用户的访问权限描述组成。还可以指定一些管理选项。

节可以是文件服务（客户端将其作为其原生文件系统的扩展使用），也可以是打印服务（客户端通过它访问运行服务器的主机上的打印服务）。

节可以被指定为访客服务，在这种情况下，访问不需要密码。在这种情况下，使用一个 UNIX 访客账户来定义访问权限。

访客服务以外的节需要密码才能访问。客户端提供用户名。由于较旧的客户端只提供密码而不提供用户名，你可以在共享定义中使用 `user=` 指定一个用户名列表来与密码进行比对。对于 Windows 95/98 和 Windows NT 等现代客户端，这通常是不必要的。

请注意，服务器授予的访问权限会被主机系统授予指定用户或访客用户的访问权限所掩盖。服务器授予的权限不会多于主机系统。

以下示例节定义了一个文件空间共享。用户对路径 `/home/bar` 具有写权限。通过共享名“foo”访问该共享：

```
[foo]

path = /home/bar

writeable = true
```

以下示例节定义了一个打印共享。该共享是只读的，但可以打印。这意味着允许的唯一访问方式是通过调用打开、写入和关闭池化文件操作。`guest ok` 参数意味着允许以默认访客用户（在其他处指定）访问：

```
[aprinter]

path = /usr/spool/public

read only = true

printable = true

guest ok = true
```



# 特殊节

## `[global]`
`[global]` 节包含适用于整个 Samba 服务器的参数。这些是配置文件最重要的参数。

## `[homes]`
`[homes]` 节用于定义如何共享用户家目录。每个用户都有自己的家目录，通过其用户名进行访问。

## `[printers]`
`[printers]` 节用于定义服务器上可打印机。每台打印机由自己的节定义，其中包含了指向池目录路径以及其他访问控制的参数。

# 参数

参数定义了节的特定属性。某些参数特定于 `[global]`（全局）节（例如，安全性）。某些参数可以在所有节中使用（例如，创建模式）。其他所有参数都允许在普通节中使用。在后续描述中，`[homes]` 和 `[printers]` 节将被视为普通节。括号中的字母 'G' 表示该参数是 `[global]` 节特有的。字母 'S' 表示该参数可以在特定节中指定。请注意，所有 'S' 参数也可以在 `[global]` 节中指定——在这种情况下，它们将定义所有服务的默认行为。

参数在此处按字母顺序排列——这可能不是最符合操作逻辑的流，但至少你可以从中找到它们！在存在同义词的地方，将描述首选的同义词，其他词指向该首选同义词。

# 变量替换

配置文件中设置的许多字符串都可以进行替换。例如，选项 `path = /tmp/%u` 如果用户使用用户名连接，则被解释为 `path = /tmp/john`。

这些替换大部分在下方的描述中已注明，但也有一些通用替换适用于任何相关之处。这些是：

- `%S` = 当前服务的名称（如果存在）。
- `%P` = 当前服务的根目录（如果存在）。
- `%u` = 当前服务的用户名（如果存在）。
- `%g` = `%u` 的主组名。
- `%U` = 会话用户名（客户端想要的名称，不一定与其获得的名称相同）。
- `%G` = `%U` 的主组名。
- `%H` = `%u` 提供的用户主目录。
- `%v` = Samba 版本。
- `%h` = Samba 运行的主机名。
- `%m` = 客户端机器的 NetBIOS 名称（非常有用）。
- `%L` = 服务器的 NetBIOS 名称。这允许你根据客户端如何称呼你来更改配置。你的服务器可以拥有“双人格”。
- `%M` = 客户端机器的域名名称。
- `%N` = 你的 NIS 主目录服务器名称。这从你的 NIS auto.map 条目获取。如果你使用 `--automount` 选项命名 Samba，则此值将与 `%L` 相同。
- `%p` = 服务主目录的路径，从你的 NIS auto.map 条目获取。NIS auto.map 条目被分为 `"%N:%p"`。
- `%R` = 协议协商后选定的协议级别。可以是 CORE, COREPLUS, LANMAN1, LANMAN2 或 NT1 之一。
- `%d` = 当前服务器进程的进程 ID。
- `%a` = 远程机器的架构。只有部分架构会被识别，且这些可能并非 100% 可靠。它目前识别 Samba, WinWF, WinNT, Win95。其他任何内容将被视为“UNKNOWN”（未知）。如果出现这些情况，向 `samba-bugs@samba.org` 发送 level 3 信息将允许修复它。
- `%I` = 客户端机器的 IP 地址。
- `%T` = 当前日期和时间。利用这些替换和其他 `samba.conf` 选项可以实现一些非常有创意的操作。

# 名称混淆 (Name Mangling)

Samba 支持“名称混淆”，以便 DOS 和 Windows 客户端可以使用不符合 8.3 格式的文件。它也可以被设置为调整 8.3 格式文件名的大小写。

有几个控制混淆执行方式的选项，它们是分组而非列出的。默认值请查看 `test-param` 程序的输出。

所有这些内容都可以为每个服务单独设置（当然，也可以全局设置）。选项如下：

- `mangle case = yes/no` 控制具有非“默认”大小写字符的名称是否被混淆。例如，如果为 yes，那么像“Mail” 这样的名称会被混淆。默认为 no。
- `case sensitive = yes/no` 控制文件名是否区分大小写。如果不区分，samba 必须对传递的名称进行文件名搜索和匹配。默认为 no。
- `default case = upper/lower` 控制新文件名的名的默认大小写。默认为 lower。
- `preserve case = yes/no` 控制创建新文件时是使用客户端的大小写，还是强制使用“默认”大小写。默认为 yes。
- `short preserve case = yes/no` 控制符合 8.3 语法、全大写且长度合适的新文件，是大大写形式创建，还是被强制转换为“默认”大小写。此选项可以配合 `preserve case = yes` 使用，以允许长文件名保留其大小写，而短名称转换为小写。默认为 yes。

默认情况下，Samba 2.0 与 Windows NT 服务器具有相同的语义，即它对大小写不敏感但保留大小写。

# 关于用户名/密码验证的说明

用户有多种方式连接到服务。服务器决定是否允许连接到指定服务时遵循以下步骤。如果所有步骤失败，则连接请求被拒绝。如果其中一个步骤通过，则不再检查后续步骤。

如果服务标记为 `guest only = yes`，则跳过步骤 1 到 5。

步骤 1：如果客户端传递了用户名/密码对，且该用户名/密码对被 UNIX 系统验证。
步骤 2：如果客户端传递了用户名/密码对，且该用户名/密码对被 Samba 数据库验证。
步骤 3：如果客户端传递了用户名/密码对，且该用户名/密码对被 LDAP 服务器验证。
步骤 4：如果客户端传递了用户名/密码对，且该用户名/密码对被 Winbind 守护进程验证。
步骤 5：如果客户端传递了用户名/密码对，且该用户名/密码对被 Kerberos 服务器验证。
步骤 6：如果客户端传递了用户名/密码对，且该用户名/密码对被本地文件验证。

246

附录 C：Samba 手页

`mangled names` `postscript` `queueresume` `command` `user`
`mangling char` `preexec` `read list` `username`
`map archive` `preserve case` `read only` `users`
`map hidden` `print command` `revalidate` `valid users`
`map system` `print ok` `root` `poststxec` `veto files`
`map to guest` `printable` `root` `preexec` `veto oplock files`
`max connections` `printer` `set directory` `volume`
`min print space` `printer driver` `share modes` `wide links`
`only guest` `driver location` `short preserve case` `writable`
`only user name` `status` `write list`
`oplocks` `printing` `strict locking` `write ok`
`path` `public` `strict sync` `writeable`
`postexec` `queuepause command` `sync always`

# 各参数说明

### `+` - `admin users` (S)
- 这是一个在共享共享上将被授予管理员权限的用户列表。这意味着他们将以超级用户（root）的身份执行所有文件操作。
- 您应该非常谨慎地使用此选项，因为列表中的任何用户都可以在共享上执行任何他们想做的事，而不考虑文件权限。
- 默认值：
  no admin users
- 示例：`admin users = jason`

### `+` - `allow hosts` (S)
- 此参数的别名是‘hosts allow’。

此参数是一个由逗号、空格或制表符分隔的主机集，允许其访问服务。
如果在 `[global]` 部分中指定，它将适用于所有服务，无论单个服务是否有不同的设置。

您可以通过名称或 IP 地址来指定主机。例如，您可以使用诸如 `allow hosts = 150.203.5.*` 的设置限制对 C 类子网内主机的访问。列表的语法在主页 `hosts_access(5)` 中描述。注意，您的系统可能不存在此页面，因此在此处提供简要描述。
注意：如果您希望允许本地用户运行 `smpasswd (8)` 程序来通过本地 `smbd (8)` 守护进程更改其 Samba 密码，那么您必须确保 localhost 在您的 `allow hosts` 列表中，因为 `smpasswd (8)` 以客户端-服务器模式运行，并被本地 `smbd` 进程视为另一个客户端。

`smb.conf (5)`

您还可以通过网络/子网掩码对以及（如果系统支持 netgroups 的话）正则名称来指定主机。`EXCEPT` 关键字也可以用于限制通配符列表。以下示例提供了一些帮助：

示例 1：允许 localhost 和 150.203.* 中的所有 IP，排除一个

`hosts allow = localhost, 150.203. EXCEPT 150.203.666`

示例 2：允许 localhost 和匹配给定网络/子网掩码的主机

`hosts allow = localhost, 150.203.15.0/255.255.255.0`

示例 3：允许 localhost 加上几个主机

`hosts allow = localhost, lapland, arvidsjaur`

示例 4：仅允许 NIS 组“foonet”中的主机或 localhost，拒绝来自一个特定部分的访问

`hosts allow = @foonet, localhost hosts deny = pirate`

注意，访问仍然需要用户级密码保护。
使用 `Testparm` 测试您的主机访问方式，以查看其是否符合您的预期。

默认值：none（即允许所有主机访问）
示例：`allow hosts = 150.203.5. localhost host.mynet.edu`

### `+` - `alternate permissions` (S)
这是一个已弃用的参数。它在 Samba 2.0 中不再产生任何影响。在之前的 Samba 版本中，它影响了 DOS“只读”属性映射到文件的方式。在 Samba 2.0 中，如果 UNIX 文件没有为所有者设置'w' 位，则该文件被标记为“只读”，无论所有者当前是否已登录。

### `+` - `announce` (G)
这指定了 `nmbd` 向网络浏览列表公告其身份的服务器类型。默认情况下，它设置为 Windows NT。有效选项有：“NT”、“Win95”或“WFW”，分别代表工作组的 Windows NT、95 和 98。除非您有特定需求需要停止 Samba 显示为 NT 服务器，否则不要更改此参数，因为这可能会阻止 Samba 服务器作为浏览器服务器参与。

默认值：`announce as = NT`
示例：`announce as = Win95`

# `announce version` (G)
这指定了 `nmbd` 在公告其身份为服务器时使用的主版本和次版本号。默认值是 4.2。除非您有特定需求将 Samba 服务器设置为低版本服务器，否则不要更改此参数。

默认值：`announce version = 4.2`
示例：`announce version = 2.0`

# `auto services` (G)
这是一个您希望自动添加到浏览列表中的服务列表。这对于家庭和打印机服务最有用，否则这些服务是不可见的。

注意，如果您只是想加载 printcap 中的所有打印机，使用“load printers”选项更简单。



默认值：`no auto services`

示例：`auto services` = `freed` 1 `lp` `color1`



# `available` (S)

此参数允许您“关闭”某个服务。如果 `available = no`，则所有连接该服务的尝试都将失败。此类失败将被记录。

默认值：`available = yes`

示例：`available = no`

# `bind interfaces only` (G)

此全局参数允许 Samba 守护进程限制机器上哪些接口提供 `smbd` 请求。如果请求了文件服务，`smbd` 和名称服务 `nmbd` 将以略微不同的方式处理它。

对于名称，它会导致 `nmbd` 绑定到 `interfaces` 列出的接口上的 137 和 138 端口。如果设置了 `bind only`，则网络 `127.0.0.1` 在 `interfaces` 列表中，`smpasswd` 将无法连接到

`smb.conf` (5)

模式。`smpasswd` 可以强制使用其 `remote machine` 参数使用本地主接口，将 `remote machine` 设置为主接口的 IP 名称。

默认值：`bind interfaces only = False`
示例：`bind interfaces only = True`

### `blocking locks` (S)

此参数控制 `smbd` 在收到客户端请求获取打开文件的范围锁时的行为，并与之关联请求时间限制。
如果设置了此参数且无法立即满足锁范围，Samba 2.0 将在内部队列锁请求，并定期尝试获取锁，直到超时过期。
如果将此参数设置为 `False`，则 Samba 2.0 将表现得与之前的版本一样，在无法获取锁范围时立即失败锁请求。
此参数可以按共享进行设置。

默认值：`blocking locks = True`
示例：`blocking locks = False`

### `browsable` (S)

`browseable` 的别名。

### `browse list` (G)

这控制 `smbd` 是否向执行 `NetServerEnum` 调客户端提供浏览列表。通常设置为 true。您应该不需要更改此项。

默认值：`browse list = Yes`

### `browseable`

这控制此共享是否在网络查看的可用共享列表和浏览列表中可见。

默认值：`browseable = Yes`
示例：`browseable = No`

### `case sensitive` (G)

参见 NAME MANGLING（名称修饰）章节中的讨论。

### `casesenames` (G)

`case sensitive` 的别名。

### `change notify timeout` (G)

Samba 2.0 支持的新 NT SMB 请求之一是 `ChangeNotify` 请求。此 SMB 客户端告诉服务器“监控”特定目录的任何

更改并仅在发生更改时对 SMB 请求做出响应。在 UNIX 下，这种对目录的持续扫描是昂贵的，因此 `smbd` 守护进程每隔 `change notify timeout` 秒对每个请求的目录执行一次扫描。
`change notify timeout` 以秒为单位。

默认：`change notify timeout = 60`

示例：`change notify timeout = 300`
这将扫描时间变为每 5 分钟一次。

### `字符集` (G)

这允许 `smbd` 将传入的 DOS 代码页文件名（参见 `client code page` 参数）映射到多个内置的 UNIX 字符集。内置的代码页转换映射为：

- ISO8859-1 西欧 UNIX 字符集。如果 `character set` 参数设置为 iso8859-1，则 `client code page` 参数必须设置为 `code page 850`，以便能够正确转换为 UNIX 字符集。
- ISO8859-2 东欧 UNIX 字符集。如果 `character set` 参数设置为 ISO8859-2，则 `client code page` 参数必须设置为 `code page 852`，以便能够正确转换为 UNIX 字符集。
- ISO8859-5 俄语西尔字母 UNIX 字符集。如果 `character set` 参数设置为 ISO8859-2，则 `client code page` 参数必须设置为 `code page 866`，以便能够正确转换为 UNIX 字符集。
- KOIB8-R 俄语西尔字母 UNIX 字符集的备映射。如果 `character set` 参数设置为 KOIB8-R，则 `client code page` 参数必须设置为 `code page 866`，以便能够正确转换为 UNIX 字符集。

BUG：这些 MSDOS 代码页到 UNIX 字符集的映射应该是动态的（类似于 MS DOS 代码页的加载），而不是静态的。

参见 `client code page`。如果未设置此参数，意味着没有进行文件名翻译。

默认：`character set = <空字符串>`
示例：`character set = ISO8859-1`

### `客户端代码页` (G)

此参数指定访问 Samba 的客户端所使用的 DOS 代码页。要确定 Windows 或 DOS 客户端使用的是什么代码页，请打开 DOS 命令行提示符并输入命令 `chop`。这将输出代码页。美国版 MS-DOS、Windows 95 和 Windows NT 版本的默认代码页为 437。上述操作系统的西欧地区用户的默认代码页为 850。

此参数告诉 `smbd` 在启动时动态加载哪些 `.XXX` 编码页文件。这些文件在手册 `make_smbdcodpage (1)` 中有更详细的描述，告知 `smbd` 如何映射小写到大写字符，以提供 Windows 客户端期望的文件大小写不敏感。

Samba 目前带有以下代码页文件：

- Code Page 437—MS-DOS Latin US
- Code Page 737—Windows ‘95 Greek
- Code Page 850—MS-DOS Latin 1
- Code Page 852—MS-DOS Latin 2
- Code Page 861—MS-DOS Icelandic
- Code Page 866—MS-DOS Cyrillic
- Code Page 932—MS-DOS Japanese SJIS
- Code Page 949—MS-DOS Korean Hangul
- Code Page 950—MS-DOS Traditional Chinese

此参数可以是 437, 737, 850, 852, 861, 936, 949 或 950 中的任意值。如果你没有找到所需的转换，请阅读其他一个代码页文件的注释，并以 `_smbccodepage` (I) 命名并编写一个。请记住将其捐给 Samba 用户社区。

此参数与 `valid chars` 参数协同工作，确定文件名中哪些字符是有效的以及大小写如何处理。如果你同时设置了此参数和 `valid chars` 参数，在 `smb.conf` 文件中，`client code page` 参数必须设置在 `valid chars` 参数之前。`valid chars` 字符串将补充 `client code page` 参数设置中的字符集。

如果不是，`client code page` 默认为 850。

默认：`client code page = 850`
示例：`client code page = 936`

### `valid chars` (G)

此参数与 `valid chars` 参数协同工作，确定文件名中哪些字符是有效的以及大小写如何处理。如果你同时设置了此参数和 `valid chars` 参数，在 `smb.conf` 文件中，`client code page` 参数必须设置在 `valid chars` 参数之前。`valid chars` 字符串将补充 `client code page` 参数设置中的字符集。

如果不是，`client code page` 默认为 850。

默认：`client code page = 850`
示例：`client code page = 936`

### `valid chars` (G)

此参数与 `valid chars` 参数协同工作，确定文件名中哪些字符是有效的以及大小写如何处理。如果你同时设置了此参数和 `valid chars` 参数，在 `smb.conf` 文件中，`client code page` 参数必须设置在 `valid chars` 参数之前。`valid chars` 字符串将补充 `client code page` 参数设置中的字符集。

如果不是，`client code page` 默认为 850。

默认：`client code page = 850`
示例：`client code page = 936`

### `valid chars` (G)

此参数与 `valid chars` 参数协同工作，确定文件名中哪些字符是有效的以及大小写如何处理。如果你同时设置了此参数和 `valid chars` 参数，在 `smb.conf` 文件中，`client code page` 参数必须设置在 `valid chars` 参数之前。`valid chars` 字符串将补充 `client code page` 参数设置中的字符集。

如果不是，`client code page` 默认为 850。

默认：`client code page = 850`
示例：`client code page = 936`

### `valid chars` (G)

此参数与 `valid chars` 参数协同工作，确定文件名中哪些字符是有效的以及大小写如何处理。如果你同时设置了此参数和 `valid chars` 参数，在 `smb.conf` 文件中，`client code page` 参数必须设置在 `valid chars` 参数之前。`valid chars` 字符串将补充 `client code page` 参数设置中的字符集。

如果不是，`client code page` 默认为 850。

默认：`client code page = 850`
示例：`client code page = 936`

# 目录 C：Samba 手页

### 默认情况 (S)

请参见“NAME MANGLING”章节。另请注意“short preserve case”参数。

### 默认情况 (G)

此参数指定当实际请求的服务无法找到时，将连接的服务名称。注意参数值中**不包含**方括号（见下文示例）。

此参数没有默认值。如果提供此参数，尝试连接不存在的服务将导致错误。

通常，默认服务应该是一个允许来宾（`guest ok`）且只读的服务。

另请注意，显示的服务名称将更改为所请求的服务名称，这非常有用，因为它允许你使用宏 `%S` 来创建一个通配符服务。

请注意，默认服务中使用的名称中的任何 `_` 字符都将映射为 `/`。这可以实现一些有趣的功能。

示例：
```



# default service = pub [pub]

`path = %S`

## 删除只读 (S)

此参数允许删除只读文件。这不符合 DOS 语义，但 UNIX 允许这样做。

此选项在作为 `rcs` 运行应用程序时可能有用，此时 UNIX 所有权阻止了更改文件权限，而 DOS 语义阻止了删除只读文件。

默认：`delete readonly = No`
示例：`delete readonly = Yes`

## 删除否决文件 (S)

此选项用于 Samba 尝试删除包含一个或多个目录的目录时（即 `veto files` 选项）。如果此选项设置为 `False`（默认值），那么如果否决目录包含任何非否决文件或目录，则该目录的操作将失败。这正是你想要的结果。

如果将此选项设置为 `True`，则 Samba 将尝试递归删除否决目录内的任何文件和目录。这对于像 NetAtom 等文件服务器系统非常有用，这些系统会在你可能禁止 DOS/Windows 用户看到的目录中创建元文件（例如 `.AppleDouble`）。

设置 `veto files = True` 允许在用户有权限的情况下，在删除父目录时透明地删除这些目录。

另参见 `veto` 参数

# smb.conf (5)

默认：`delete veto files = False`
示例：`delete veto files = True`

## 拒绝主机 (S)

`allow hosts` 的反面——在此列出的主机 **不允许** 访问服务，除非特定服务有自己的列表来覆盖此列表。当列表冲突时，`allow` 列表优先。
默认：`none`（即没有专门排除的主机）
示例：`deny hosts = 150.203.4.badhost.mynet.edu.au`

## dfree 命令 (G)

`dfree` 命令设置仅应在内部磁盘空间计算出现问题的系统上。这在 Ultrix 上是已知的，也可能发生在其他操作系统上。看到的症状是每个目录列表结束时出现“Abort Retry Ignore”（中止、重试、忽略）错误。

此设置允许用外部程序替换计算总磁盘空间和可用量的内部程序。下面的示例提供了一个可能实现此功能的脚本。
外部程序将接收单个参数，指示正在查询的文件系统中的目录。这通常由字符串 `"./"` 组成。脚本应返回两个 ASCII 格式的整数。第一个应该是以块为单位的总磁盘空间，第二个是可用块的数量。可选的第三个返回值可以提供字节单位的块大小。默认块大小为 1024 字节。

注意：你的脚本 **不应** 设置 `setuid` 或 `setgid`，并且应由 `root` 所有（且仅允许 `root` 写入）。

默认：默认使用用于确定容量和剩余空间的内部程序。
示例：`dfree command = /usr/local/samba/bin/dfree`
其中脚本 `dfree`（必须赋予可执行权限）可以为：

```
#!/bin/sh

df $1 | tail -1 | awk '{print $2" "$4}'
```

或者（在基于 Sys V 的系统上）：

```bash
#!/bin/sh

usr/bin/df -k $1 | tail -1 | awk '{print $3" "$5}'
```

注意，你可能需要在系统上将命令名称替换为完整路径。

## 目录 (S)

`path` 的同义词。

## 目录掩码 (S)

此参数是在创建 UNIX 目录时将 DOS 模式转换为 UNIX 模式时使用的八进制模式。

当创建目录时，将根据从 DOS 模式到 UNIX 权限的映射计算必要的权限，然后将生成的 UNIX 模式与此参数进行位“与”（AND）操作。此参数可以被视为目录 UNIX 模式的位掩码（MASK）。此处 **未** 设置的任何位都将从创建目录时设置的模式中移除。

此参数的默认值移除了 UNIX 模式中的“组”和“其他”写入位，仅允许目录所有者修改它。

遵循 Samba 位“或”（OR）逻辑，将此参数创建的 UNIX 模式与 `force directory mode` 参数的值相结合。此参数默认设置为 `000`（即不添加额外的模式位）。

参见 `force directory mode` 参数以使特定的模式位始终应用于创建的目录。

另参见 `create mode` 参数以对创建的文件进行模式掩码处理。

```
Default: directory mask = 0755

Example: directory mask = 0775
```

## 目录模式 (S)

`directory mask` 的同义词。

## dns 代理 (G)

指定 `nmbd` 作为代理。注意 NetBIOS 名称的最大长度为 15 个字符，因此 DNS 别名同样可以是 15 个字符。

此设置允许用外部程序替换计算总磁盘空间和可用量的内部程序。示例提供了一个可能实现此功能的脚本。
外部程序将接收单个参数，指示正在查询的文件系统中的目录。这通常由字符串 `"./"` 组成。脚本应返回两个 ASCII 格式的整数。第一个应该是以块为单位的总磁盘空间，第二个是可用块的数量。可选的第三个返回值可以提供字节单位的块大小。默认块大小为 1024 字节。

注意：你的脚本 **不应** 设置 `setuid` 或 `setgid`，并且应由 `root` 所有（且仅允许 `root` 写入）。

默认：默认使用用于确定容量和剩余空间的内部程序。
示例：`dfree command = /usr/local/samba/bin/dfree`
其中脚本 `dfree`（必须赋予可执行权限）可以为：

```bash
#!/bin/sh

df $1 | tail -1 | awk '{print $2" "$4}'
```

或者（在基于 Sys V 的系统上）：

```bash
#!/bin/sh

usr/bin/df -k $1 | tail -1 | awk '{print $3" "$5}'
```

注意，你可能需要在系统上将命令名称替换为完整路径。

## 拒绝主机 (S)

`allow hosts` 的反面——在此列出的主机 **不允许** 访问服务，除非特定服务有自己的列表来覆盖此列表。当列表冲突时，`allow` 列表优先。
默认：`none`（即没有专门排除的主机）
示例：`deny hosts = 150.203.4.badhost.mynet.edu.au`

## 域控制器 (G)

这是一个 **已弃（DEPRECATED）** 参数。它目前未用于 Samba 源码，应该从所有当前的 `smb.conf` 文件中删除。出于兼容性原因将其保留。

## 域组映射 (G)

此选项允许你指定一个文件，其中包含 NT 域组（任何域）到 UNIX 组名的唯一映射。尽管 UNIX 缺乏原生支持 NT 模型（基于 VAX/VMS），这仍然允许 NT 域组能够向 NT 用户正确显示。建议读者熟悉 NT 域系统及其管理。此选项与 `local group map` 和 `domain user map` 配合使用。在 Samba 预期与任何 SAM 数据库（本地工作站或域控制器）交互的情况下，这三个选项的使用是简单且没有必要的。

映射文件按行解析。如果某行以 `#` 或 `;` 开头，则会被忽略。每行左侧应包含单个 UNIX 组名，右侧应包含单个 NT 域名，用制表符或 `=` 分隔。如果该行包含空格，则应用引号括起来。该行可以是以下格式：

```
UNIXgroupname \DOMAIN_NAME\DomainGroupName
```



或者：
`UNIXgroupname DomainGroupName`

在 Samba 是域控制器或使用 `security = domain` 的域成员的情况下，可以使用后一种格式：默认域名是 Samba 服务器的域名，由 `workgroup = MYGROUP` 指定。
映射文件中任何未指定的组都被假设为本地组或域组，取决于 Samba 服务器的角色。

在 Samba 是域控制器的情况下，Samba 将优先将所有未指定的 UNIX 组作为自身的同名域组。
在 Samba 是使用 `security = domain` 的域成员的情况下，Samba 将与其域控制器（参见 `password server`）检查 UNIX 名称以是否为 NT 域组。如果域控制器表示不是，则未指定的（未映射的）UNIX 组视为 Samba 服务器本地数据库中的本地组。NT 管理员会将这些识别为工作站本地组，通过运行 `USGRMEXE` 并选择名为 `\WORKSTATION_NAME` 的远程域，或者在本地工作站上运行 `MUSGRMEXE` 来管理。

### 域管理员组 (G)

这是一个`实验性（EXPERIMENTAL）`参数，属于未完成的 Samba 域代码。它已于 98 年删除，以便配合支持域功能的最新代码。

### 域管理员用户 (G)

这是一个`实验性（EXPERIMENTAL）`参数，属于未完成的 Samba 域代码。它已于 98 年删除，以便配合支持域功能的最新代码。

### 删除只读 (S)

此参数允许删除只读文件。这不符合 DOS 语义，但 UNIX 允许这样做。

此选项在作为 rcs 运行应用程序时可能有用，此时 UNIX 所有权阻止了更改文件权限，而 DOS 语义阻止了删除只读文件。

默认：`delete readonly = No`
示例：`delete readonly = Yes`

### 删除否决文件 (S)

此选项用于 Samba 尝试删除包含一个或多个目录的目录（即 `veto files` 选项）。如果此选项设置为 False（默认值），那么如果否决目录包含任何非否决文件或目录，则该目录的操作将失败。这正是你想要的结果。

如果将此选项设置为 True，则 Samba 将尝试递归删除否决目录内的任何文件和目录。这对于像 NetAtom 等文件服务器系统非常有用，这些系统会在你可能禁止 DOS/Windows 用户看到的目录中创建元文件（例如 `.AppleDouble`）。

设置 `veto files = True` 允许在用户有权限的情况下，在删除父目录时透明地删除这些目录。

另参见 `veto` 参数

### dfree 命令 (G)

`dfree` 命令设置仅应在内部磁盘空间计算出现问题的系统上。这在 Ultrix 上是已知的，也可能发生在其他操作系统上。看到的症状是每个目录列表结束时出现“Abort Retry Ignore”（中止、重试、忽略）错误。此设置允许用外部程序替换计算总磁盘空间和可用量的内部程序。示例示例提供了一个可能实现此功能的脚本。外部程序将接收单个参数，指示正在查询的文件系统中的目录。这通常由字符串 "./" 组成。脚本应返回两个 ASCII 格式的整数。第一个应该是以块为单位的总磁盘空间，第二个是可用块的数量。可选的第三个返回值可以提供字节单位的块大小。默认块大小为 1024 字节。

注意：你的脚本`不应`设置 `setuid` 或 `setgid`，并且应由 `root` 所有（且仅允许 `root` 写入）。

默认：默认使用用于确定容量和剩余空间的内部程序。
示例：`dfree command = /usr/local/samba/bin/dfree`
其中脚本 `dfree`（必须赋予可执行权限）可以为：

```bash
#!/bin/sh

df $1 | tail -1 | awk '{print $2" "$4}'
```

或者（在基于 Sys V 的系统上）：

```bash
#!/bin/sh

usr/bin/df -k $1 | tail -1 | awk '{print $3" "$5}'
```

注意，你可能需要在系统上将命令名称替换为完整路径。

### 目录 (S)

`path` 的同义词。

### 目录掩码 (S)

此参数是在创建 UNIX 目录时将 DOS 模式转换为 UNIX 模式时使用的八进制模式。

当创建目录时，将根据从 DOS 模式到 UNIX 权限的映射计算必要的权限，然后将生成的 UNIX 模式与此参数进行位“与”（AND）操作。此参数可以被视为目录 UNIX 模式的位掩码（MASK）。此处`未`设置的任何位都将从创建目录时设置的模式中移除。

此参数的默认值移除了 UNIX 模式中的“组”和“其他”写入位，仅允许目录所有者修改它。

遵循 Samba 位“或”（OR）逻辑，将此参数创建的 UNIX 模式与 `force directory mode` 参数的值相结合。此参数默认设置为 000（即不添加额外的模式位）。

参见 `force directory mode` 参数以使特定的模式位始终应用于创建的目录。

另参见 `create mode` 参数以对创建的文件进行模式掩码处理。

Default: `directory mask = 0755`

Example: `directory mask = 0775`

### 目录模式 (S)

`directory mask` 的同义词。

### dns 代理 (G)

指定 `nmbd` 作为代理。注意 NetBIOS 名称的最大长度为 15 个字符，因此 DNS 别名同样可以是 15 个字符。此设置允许用外部程序替换计算总磁盘空间和可用量的内部程序。示例提供了一个可能实现此功能的脚本。外部程序将接收单个参数，指示正在查询的文件系统中的目录。这通常由字符串 "./" 组成。脚本应返回两个 ASCII 格式的整数。第一个应该是以块为单位的总磁盘空间，第二个是可用块的数量。可选的第三个返回值可以提供字节单位的块大小。默认块大小为 1024 字节。注意：你的脚本`不应`设置 `setuid` 或 `setgid`，并且应由 `root` 所有（且仅允许 `root` 写入）。

默认：默认使用用于确定容量和剩余空间的内部程序。
示例：`dfree command = /usr/local/samba/bin/dfree`
其中脚本 `dfree`（必须赋予可执行权限）可以为：

```bash
#!/bin/sh

df $1 | tail -1 | awk '{print $2" "$4}'
```

或者（在基于 Sys V 的系统上）：

```bash
#!/bin/sh

usr/bin/df -k $1 | tail -1 | awk '{print $3" "$5}'
```

修正：

### 拒绝主机 (S)

`allow hosts` 的反面——在此列出的主机`不允许`访问服务，除非特定服务有自己的列表来覆盖此列表。当列表冲突时，`allow` 列表优先。
默认：`none`（即没有专门排除的主机）
示例：`deny hosts = 150.203.4.badhost.mynet.edu.au`

### 域控制器 (G)

这是一个`已弃（DEPRECATED）`参数。它目前未用于 Samba 源码，应该从所有当前的 `smb.conf` 文件中删除。出于兼容性原因将其保留。

### 域组映射 (G)

此选项允许你指定一个文件，其中包含 NT 域组（任何域）到 UNIX 组名的唯一映射。尽管 UNIX 缺乏原生支持 NT 模型（基于 VAX/VMS），这仍然允许 NT 域组能够向 NT 用户正确显示。建议读者熟悉 NT 域系统及其管理。此选项与 `local group map` 和 `domain user map` 配合使用。在 Samba 预期与任何 SAM 数据库（本地工作站或域控制器）交互的情况下，这三个选项的使用是简单且没有必要的。

映射文件按行解析。如果某行以 `#` 或 `;` 开头，则会被忽略。每行左侧应包含单个 UNIX 组名，右侧应包含单个 NT 域名，用制表符或 `=` 分隔。如果该行包含空格，则应用引号括起来。该行可以是以下格式之一：

```
UNIXgroupname \DOMAIN_NAME\DomainGroupName
```



或者：
`UNIXgroupname DomainGroupName`

在 Samba 是域控制器或使用 `security = domain` 的域成员的情况下，可以使用后一种格式：默认域名是 Samba 服务器的域名，由 `workgroup = MYGROUP` 指定。
映射文件中任何未指定的组都被假设为本地组或域组，取决于 Samba 服务器的角色。

在 Samba 是域控制器的情况下，Samba 将优先将所有未指定的 UNIX 组作为自身的同名域组。
在 Samba 是使用 `security = domain` 的域成员的情况下，Samba 将与其域控制器（参见 `password server`）检查 UNIX 名称以其是否为 NT 域组。如果域控制器表示不是，则未指定的（未映射的）UNIX 组视为 Samba 服务器本地数据库中的本地组。NT 管理员会将这些识别为工作站本地组，通过运行 `USGRMEXE` 并选择名为 `\WORKSTATION_NAME` 的远程域，或者在本地工作站上运行 `MUSGRMEXE` 来管理。

### 域管理员组 (G)

这是一个`EXPERIMENTAL`参数，属于未完成的 Samba 域代码。它已于 98 年删除，以便配合支持域功能的最新代码。

### 域管理员用户 (G)

这是一个`EXPERIMENTAL`参数，属于未完成的 Samba 域代码。它已于 98 年删除，以便配合支持域功能的最新代码。

## 附录 C: Samba 手页

这听起来可能很复杂，但这意味着 Samba 服务器作为域成员或实验性`EXPERIMENTAL`域控制器，将分别像 NT 工作站（带有本地 SAM 数据库）或 NT PDC（带有域 SAM 数据库）一样运行，完全不需要任何映射文件。如果你想玩得复杂点，也可以。

请注意，将任意域中的任意 NT 组添加到任意 UNIX 组**需要**满足以下条件：

- UNIX 组存在于 UNIX 服务器上。
- NT 域组存在于指定的 NT 域中。
- UNIX 服务器知道指定的域；
- UNIX 中的所有 UNIX 用户（他们期望以正确的 NT 用户身份和正确的 NT 组权限访问 Samba 服务器）都已使用`domain user map`映射到指定 NT 域中正确的 NT 域用户。

未能满足上述任何要求都可能导致日志文件中报告某项（或全部）错误，或者（以及）授予用户的访问权限不正确或缺失。

- `domain groups (G)`

这是一个实验性`EXPERIMENTAL`的参数，是未完成的 Samba NT 域控制器的一部分。它已于 1998 年 11 月移除。要使用可能对 Samba NT 域控制器功能支持更多的最新代码，请向 `listproc@samba.com` 发送邮件订阅 Samba-ntdom 邮件列表。

- `domain guest group (G)`

这是一个实验性`EXPERIMENTAL`的参数，是未完成的 Samba NT 域控制器代码的一部分。它已于 1998 年 11 月移除。要使用可能对 Samba NT 域控制器功能支持更多的最新代码，请向 `listproc@samba.com` 发送邮件订阅 Samba-ntdom 邮件列表。

- `domain logons (G)`

这是一个实验性`EXPERIMENTAL`的参数，是未完成的 NT 域控制器代码的一部分。它已于 1998 年 11 月移除。要使用可能对 Samba NT 域控制器功能支持更多的最新代码，请向 `listproc@samba.com` 发送邮件订阅 Samba-ntdom 邮件列表。

- `domain logons (G)`

如果设置为 true，Samba 将为其所在的工作组提供 Windows 95/98 域登录。有关设置此项的更多细节，请参阅源码随带的 Samba 文档目录中的 `DOMA.txt` 文件。

注意，Win95/98 域登录不同于 Windows NT 域。NT 登录需要一个域主控制器（PDC）。旨在未来的版本中 Samba 能为 Windows NT 客户端提供此功能。

默认值：`domain logons = no`

`smb.conf (5) 259`

- `domain master (G)`

告诉 `nmbd` 启用广域浏览列表排序。设置此选项会导致 `nmbd` 声明一个特殊的特定域的 NetBIOS 名称，标识其为给定工作组的域主。在广播隔离子网的同一工作组内的本地主浏览器将向 `nmbd` 提供它们的本地浏览列表，然后向 `smbd` 请求整个广域浏览列表的完整副本。浏览器客户端将联系其本地主浏览器，并将接收全域浏览列表，而不仅仅是针对广播隔离子网的列表。

注意，Windows NT 主域控制器默认期望能够声明该工作组的特殊 NetBIOS 名称，标识其为该工作组的域主浏览器（没有办法阻止 Windows NT DC 尝试这样做）。这意味着如果设置了此参数，且 `nmbd` 在 Windows NT DC 能够做到之前抢占了工作组的特殊名称，那么子网浏览将表现异常并失败。

默认情况下（`"auto"`），Samba 仅在它是主域控制器时才会尝试成为域主浏览器。

```
Default: domain master = auto

Example: domain master = no
```

- `user master (G)`

此选项允许你指定一个文件，其中包含单个 NT 用户名（任意域）到 UNIX 名称的唯一映射。这使得 NT 域用户能够正确地呈现 NT 系统，尽管 UNIX 缺乏对 NT 安全模型（基于 VAX/VMS）的原生支持。建议读者熟悉 NT 域系统及其管理。

此选项与`local group map`和`domain group map`结合使用。在 Samba 不预期与任何其他 SAM 数据库（无论是本地工作站还是域控制器）交互的情况下，使用这三个选项非常简单且通常没有必要。

此选项提供了（并维护了） UNIX 和 NT 用户之间的一一对应的链接，它不同于`username map`，后者并不维护其可以映射的名称与所映射名称之间的区别。

映射文件按行解析。如果任何行以 `#` 或 `;` 开头，则该行被忽略。每行左侧应包含单个 UNIX 用户名，右侧包含单个 NT 域名，用制表符或 `=` 分隔。如果任名称包含空格，则应用引号括起来。行可以是：

```
UNIXusername \DOMAIN_NAME\DomainUNIXName
```

或：

```
UNIXusername DomainName
```



进入 `/path/to/xxx` 目录，找到 `xxx.json`。

在 Samba 是实验性（EXPERIMENTAL）域控制器或它是使用 `'security = domain'` 的某些域的成员的情况下，后一种格式可以是：默认域名是 Samba 的服务器名称，由 `"workgroup = MYGROUP"` 指定。

任何未在此映射文件中指定的 UNIX 用户要么是域用户要么是工作站用户，取决于 Samba 服务器的角色。在 Samba 是实验性（EXPERIMENTAL）域控制器的情况下，Samba 将将所有未指定的 UNIX 用户作为具有相同的 NT 用户呈现。在 Samba 是使用 `"security = domain"` 的域成员的情况下，Samba 将检查 UNIX 名称就像它是 NT 用户一样。未映射的 UNIX 用户也不会被视为本地 SAM 数据库中的用户。这听起来可能很复杂，但这意味着 Samba 服务器作为域成员或实验性（EXPERIMENTAL）域控制器，将分别像 NT 工作站（带有本地 SAM 数据库）或 NT PDC（带有域 SAM 数据库）一样运行，完全不需要任何映射文件。如果你想玩得复杂点，也可以。

注意，将任意域中的任意 NT 用户添加到任意 UNIX 用户**需要**满足以下条件：

- UNIX 用户存在于 UNIX 服务器上。
- NT 域用户存在于指定的 NT 域中。
- UNIX 服务器知道指定的域。

未能满足上述任何要求都可能导致日志文件中报告某项（或全部）错误，或者（以及）授予用户的访问权限不正确或缺失。

### `descend (S)*`

某些系统上的某些目录（例如 Linux 的 `/proc` 树）客户端并不感兴趣，或者是无限深（递归的）。此参数允许你指定一个逗号分隔的目录列表，服务器应该始终显示为空为空。

注意 Samba 对 `"dont descend"` 条目的精确格式可能非常敏感。例如，你可以使用 `\./proc` 代替 `"/proc"`。实验是最好的策略 :-

Default: none（即所有目录都可以进入）
Example: `dont descend = /proc,/dev`

### `dos file resolution (S)*`

在 DOS 和 Windows 文件系统中，时间分辨率的最精细粒度是两秒。为共享设置此参数会导致当 `smbd` 需要一秒分辨率查询时，Samba 将报告的时间报告到最近的秒边界。

此选项主要作为 Visual C++ 使用 Samba 共享时的兼容性选项。如果共享上启用了 oplocks，Visual C++ 会使用两个不同的时间分辨率调用来检查文件自上次读取以来发生了变化。其中一个调用使用一秒粒度，另一个使用秒粒度。由于两个调用舍入任何

# smb.conf (5)

奇数秒向下，如果文件时间戳的秒数是奇数，那么两个时间戳将不匹配，Visual C++ 将不断报告文件已更改。设置此选项可使两个时间戳匹配，Visual C++ 即可正常工作。

**默认值:** `dos filetime resolution = False`

**示例:** `dos filetime resolution = True`

* `dos filetimes (S)*`

在 DOS 和 Windows 下，如果用户可以对文件进行写操作，他们就可以更改文件上的时间戳。在 POSIX 语义下，只有文件所有者或 root 用户可以更改时间戳。默认情况下，Samba 以 POSIX 语义运行，如果用户 `smbd` 代表非文件所有者进行操作，则将拒绝更改文件时间戳。将此选项设置为 True 允许 DOS 语义，`smbd` 将按照 DOS 的要求更改文件时间戳。

**默认值:** `dos filetimes = False`

**示例:** `dos filetimes = True`

* `encrypt passwords (G)*`

此布尔值控制是否与客户端协商加密密码。请注意，默认情况下 Windows NT 4.0 SP3 及以上版本以及 Windows 98 将期望加密密码，除非创建了注册表项。要在 Samba 中使用加密密码，请查看 Samba 文档目录 `docs/shipped` 中随源码提供的 `ENCRYPTION.txt` 文件。

为了让加密密码正常工作，`smbd` 必须访问本地的 `smbpasswd (5)` 文件，请参见 `smbdpasswd (8)` 获取有关如何设置和维护此文件的信息，或将 `security` 参数设置为“server”或“domain”，这会导致 `smbd` 向另一个服务器进行身份验证。

* `exec (S)*`

这是 `freepex` 的同义词。

* `fake directory create times (S)*`

NTFS 和 Windows VFAT 系统为所有文件和目录保留了创建时间。这与 Unix 保留的 `ctime`（状态更改时间）不同——默认情况下报告 Unix 保留的各种时间中最早的一个。为共享设置此参数会导致 Samba 始终将 1980 年 1 月 1 日午夜作为目录的创建时间。

这主要用作 Visual C++ 访问 Samba 共享时的兼容选项。Visual C++ 生成的 Makefile 将对象目录作为每个对象文件的依赖项，并有一个创建目录的 make 规则。此外，当 NMAKE 比较时，会比较创建目录创建时间。如果对象目录不存在，将创建它，但一旦它存在，其时间戳始终比包含的对象的文件早。

然而，Unix 语义意味着 Samba 报告的创建会在目录中创建或删除文件时被更新。因此，NMAKE 发现对象目录中的所有对象文件（最后一个）与目录相比已过期，并重新构建它们。启用此选项可确保目录始终早于其内容，且 NMAKE 构建将按预期进行。

**默认值:** `fake directory create times = False`

**示例:** `fake directory create times = True`

* `fake oplocks (S)*`

Oplocks（机会性锁）是 SMB 客户端从服务器获取权限以在本地缓存文件操作的方式。如果服务器授予了 oplock（机会性锁），则客户端可以认为它是访问该文件的唯一用户，并激进地缓存数据。对于某些 oplock 类型，客户端可以启用缓存文件打开/关闭操作。这可以带来巨大的性能收益。

当您设置 `"fake oplocks = yes"` 时，**`smbd`** 无论有多少客户端正在使用该文件，将始终授予 oplock 请求。

通常使用真实的 **oplocks** 支持远比使用只读共享或已知仅有一个客户端同时访问的共享（如 CD-ROM 等物理只读介质）好得多，您将在许多操作中看到性能的巨大提升。如果您在多个客户端可能同时读写文件的共享上启用此选项，将导致数据损坏。请谨慎使用此选项！

此选项默认禁用。

* `follow symlinks (S)*`

此参数允许 Samba 管理员停止让 `smbd` 遵循特定共享中的符号链接。将此参数设置为“No”可以阻止跟随任何符号链接的文件或目录（用户将收到错误）。这对于阻止用户在他们的主目录中使用指向 `/etc/passwd` 的符号链接等情况非常有用。然而，它会略微减慢文件名查找速度。

此选项默认启用（即 `smbd` 将遵循符号链接）。

* `force create mode (S)*`

此参数指定了一组 UNIX 模式权限，这些权限将*始终*设置在 Samba 创建的文件上。这是通过按位“或”操作将这些位应用到正在创建的文件的模式来实现的。该参数的默认值（八进制）为 000。此参数中的模式是在应用“create mask”中的掩码后，“或”到文件模式上的。

另参见参数“create mask”有关对创建的文件进行掩码处理的详情。

**默认值:** `force create mode = 000`

**示例:** `force create mode = 0755` 将强制所有创建的文件具有“组”和“其他”的读取和执行权限，并为“用户”设置读/写/执行位。

# `force directory mode (S)`

此参数指定了一组 UNIX 模式位权限，这些权限将*始终*设置在 Samba 创建的目录上。这是通过按位“或”操作将这些应用到正在创建的目录的模式位来实现的。该参数的默认值（八进制）为 0000，不会为创建的目录添加额外的权限位。此操作在应用“directory mask”中的掩码后进行。

另参见参数“directory mask”有关对创建的文件进行掩码处理。

**默认值:** `force directory mode = 000`

**示例:** `force directory mode = 0755` 将强制所有创建的文件具有“组”和“其他”的读取和执行权限，并为“用户”设置读/写/执行位。

# `force group (S)`

此参数指定了一组 UNIX 模式位权限，这些权限将*始终*设置在 Samba 创建的目录上。这是通过按位“或”操作将这些应用到正在创建的目录的模式位来实现的。该参数的默认值（八进制）为 000，不会为创建的目录添加任何额外的权限位。此操作在应用“directory mask”后进行。

另参见参数“directory mask”有关对创建的文件进行掩码处理。

**默认值:** `force directory mode = 000`

**示例:** `force directory mode = 0755`

# `force user (S)`

此参数指定了一组 UNIX 模式位权限，这些权限将*始终*设置在 Samba 创建的目录上。这是通过按位“或”操作将这些应用到正在创建的目录的模式位来实现的。该参数的默认值（八进制）为 000，不会为创建的目录添加任何额外的权限位。此操作在应用“directory mask”后进行。

另参见参数“directory mask”有关对创建的文件进行掩码处理。

**默认值:** `force directory mode = 000`

**示例:** `force directory mode = 0755`

# `ftype (S)`

此参数允许 Samba 管理员配置 `smbd` 在客户端查询时报告的共享所使用的文件系统类型字符串。“NTFS”是为了兼容 Windows，但可以根据需要更改其他字符串。

**默认值:** `ftype = NTFS`

**示例:** `ftype = Samba`

# 附 C: Samba 手页

* `getwd cache (G)`

这是一个调优选项。当启用此项时，将使用缓存算法来减少 `getwd()` 调用的时间。这对性能有显著影响，特别是当 `widlinks` 参数设置为 False 时。

**默认值:** `getwd cache = No`

**示例:** `getwd cache = Yes`

* `group (S)`

`"force group"` 的同义词：

* `guest account (S)`

这是一个用户名，用于访问指定为“guest ok”（见下文）的服务。任何连接到该宾客服务的客户端都将可以使用这些权限。通常此用户存在于密码文件中，但没有有效的登录权限。“ftp”用户账户通常是此参数的良好选择。如果在给的服务中指定了用户名，则指定的用户名将覆盖此用户名。

某些系统的默认宾客账户“nobody”可能无法打印。在这种情况下请使用另一个账户。您应该尝试作为宾客用户登录（例如使用“su -”命令）并使用系统打印命令尝试打印。

**默认值:** 编译时指定，通常为 `"nobody"`

**示例:** `guest account = ftp`

当服务设置为“yes”时，连接到服务不需要密码。权限将是宾客账户的权限。

参见下文关于安全的章节以获取更多信息。

**默认值:** `guest ok = no`

**示例:** `guest ok = yes`

* `guest only (S)`

当此服务设置为“yes”时，仅允许宾客连接到该服务。如果未为服务设置“guest ok”或“public”，则此参数将没有任何影响。

参见下文关于安全的章节以获取更多信息。

**默认值:** `guest only = no`

**示例:** `guest only = yes`

## smb.conf (5)

* `hide files(S)`

这是一份不可见但可以访问的文件或目录列表。DOS 的“隐藏”（hidden）属性将应用于任何匹配的文件或目录。

列表中的每个条目必须用 '/' 分隔，这允许条目中包含空格。'*' 和 '?' 可用于在 DOS 通配符中指定多个文件或目录。

每个条目必须是 Unix 路径，而不是 DOS 路径，且不能包含 Unix 目录分隔符 '/'。

请注意，大小写敏感选项也适用于隐藏文件。

设置此参数将影响 Samba 的性能，因为在扫描时它将强制检查所有文件和目录是否匹配项。

另请参见“hide dot files”（隐藏点文件）、“veto files”（拒绝文件）和“case sensitive”（大小写敏感）。

### 默认

此选项不隐藏任何文件或目录（点文件由于“hide dot files”选项的存在默认是隐藏的）。

示例 `hide files = .*/DesktopFolderDB/TrashFor&m/resource.frk/`

上述示例基于周四提供的 Macintosh SMB 客户端 (DAVE) 为内部使用创建的文件，并且仍然隐藏所有以点开头的文件。

* `homidir map (G)`

如果 `"homidir"` 为 true，且 `smbd` 同时也作为 Win95/98 登录服务器运行，则此参数指定家（或 YP）映射，从中从中提取用户主目录的服务器。目前支持 Sun 的 `auto.home` 映射格式。

```



`username server:/some/file/system`

```
程序将提取第一个 ':' 之前的服务器。可能应该有一个更好的解析系统，能够处理不同的映射格式以及 AMD（另一种自动挂载器映射）。
```

注意：系统上需要运行良好的 NIS，此选项才能生效。

另请参见“`homidir`”、“`domain logons`”（域登录）。

默认: `homidir map = auto.home`

示例: `homidir map = amd.homidir`

- - `hosts allow` (S)

`allow hosts` 的同义词。

- - `hosts deny` (S)

`denyhosts` 的同义词。

## Appendix C: Samba Man Pages

- - `hosts equiv` (G)

如果此全局参数为非空字符串，它指定要读取的文件名，用于获取无需指定密码即可允许访问的主机和用户列表。

这与 `allow hosts` 不要混淆，后者是关于主机对服务的访问，对访宾服务更有用。`hosts equiv` 对于不会向 samba 提供密码的 NT 客户端可能有用。

注意：使用 `hosts equiv` 可能会留下安全漏洞。因为这是信任 PC 来确保用户名正确。很容易让 PC 提供虚假的用户名。我建议只有在你确切知道自己在做什么时，或者在受信任的家里和孩子的家庭网络上，才使用 `hosts equiv` 选项。而且如果你真的信任他们的话（-）。

默认的主机等效关系 (`hosts equivalences`)
示例 `hosts equiv = /etc/hosts.equiv`

- - `interfaces` (G)

这允许你在一个配置文件内部包含另一个文件。该文件被原样包含，就像放置在原位一样。
它支持标准的替换，但 `%u`、`%P` 和 `%S` 除外。

- - `interfaces` (G)

此选项允许你设置多个网络接口，以便 Samba 能够正确处理所有接口上的浏览。
该选项接受一组 ip/子掩码对。子掩码可以是位掩码，也可以是位长度。
例如，以下行：

```
interfaces = 192.168.2.10/24 192.168.3.10/24
```

将配置两个 IP 地址为 `192.168.2.10` 和 `192.168.3.10` 的网络接口。
两个接口的子掩码都将设置为 `255.255.255.0`。
如果你更喜欢这种格式，可以使用以下产生相同的结果：

```
interfaces = 192.168.2.10/255.255.255.0 192.168.3.10/255.255.255.0
```

如果未设置此选项，Samba 将尝试寻找主接口，但不会尝试配置多个接口。
另请参见“`bind interfaces only`”（仅绑定接口）。

- - `invalid users` (S)

这是一个不应允许登录此服务的用户列表。这实际上是一个“偏执的”检查，以绝对确保不当设置不会破坏安全性。
以 '@' 开头的名称首先被解释为 NIS 网络组（如果你的系统支持 NIS），如果 NIS 网络组数据库中未找到该名称，则被解释为 UNIX 组。

以 '+' 开头的名称仅通过查找 UNIX 组数据库进行解释。
以 '&' 开头的名称仅通过查找 NIS 组数据库进行解释（要求你的系统上运行 NIS）。字符 '+' 和 '&' 可以以任何顺序位于名称开头，值 "&group" 意味着先检查 UNIX 组数据库，后检查 NIS 组数据库；值 "+group" 意味着先检查 NIS 组数据库，后检查 UNIX 组数据库（与 '@' 前缀相同）。

当前的 servicemen 会替换为 `%S`。这在 `[homes]` 部分很有用。
另请参见“`valid users`”（有效用户）。

默认：无无效用户 (`invalid users`)
示例：`invalid users = root fred`

- - `keepalive` (G)

此参数（整数）代表两次心跳包之间的秒数。如果设置为零，则不发送心跳包。
默认：`0`
示例：`keepalive = 60`

- - `kernel oplocks` (G)

此参数允许开启或关闭内核锁。此参数在支持它的系统上默认为 "on"，在不支持的系统默认为 "off"。
默认：`on (off)`

- - `ldap bind as` (G)

此参数是在 LDAP 上存储密码数据库的实验性 Samba 支持。只有当你的 Samba 版本配置了 `--with-ldap` 时，这些选项才可用。
此参数指定绑定到 LDAP 目录的实体。通常可以使用 root 账户。
默认：`none`
示例：`ldap bind as = "uid=root, dc=mydomain, dc=org"`

- - `ldap passwd file` (G)

此参数是在 LDAP 上存储密码数据库的实验性 Samba 支持。在使用 Samba-server 时必须提供此参数。
此参数指定包含 Samba 绑定 LDAP 服务器所需密码的文件。显而易见，该文件的权限必须设置为 700。
默认：`none`
示例：`ldap passwd file = /usr/local/samba/private/ldpass`

- - `ldap port` (G)

此参数是在 LDAP 上存储密码数据库的实验性 Samba 支持。此参数指定 LDAP 服务器的 TCP 端口号。
默认：`389`

- - `ldap server` (G)

此参数是在 LDAP 上存储密码数据库的实验性 Samba 支持。此参数指定在存储和检索 Samba 用户和组信息时使用的 LDAP 服务器 DNS 名称。
默认：`localhost`

- - `ldap suffix` (G)

此参数是在 LDAP 上存储密码数据库的实验性 Samba 支持。此参数指定 Samba 应该存储其信息的 LDAP 树分支节点。
默认：`none`
示例：`ldap suffix = "dc=mydomain, dc=org"`

## Im announcement (G)

此参数决定了 `nmbd` 是否产生 OS/2 客户端所需的 Lanman 广播，以便在其浏览列表中找到 Samba 服务器。此参数可以有三个值："true"、false" 或 "auto"。默认值为 "auto"。如果设置为 "false"，Samba 将永远不会产生这些广播。如果设置为 "true"，Samba 将按照 "Im interval" 设置的频率产生 Lanman 广播。如果设置为 "auto"，Samba 默认不发送 Lanman 广播，但会监听它们。如果它在总线上听到广播，它将开始按照 "Im interval" 设置的频率发送这些广播。

## smb.conf (5)

默认: `1m announce = auto`
示例: `1m announce = true`

- `lm interval` (G)
如果 Samba 设置为由 OS/2 客户端产生 Lanman 广播（参见 "`lm announce`" 参数），则此参数定义了产生广播的频率（以秒为单位）。如果将其设置为零，即使设置了 "`lm announce`" 参数，也不会产生任何 Lanman 广播。
另见 "`lm announce`".

- `lm interval = 60`
示例: `1m interval = 120`

- `load printers` (G)
一个布尔值，控制 printcap 中的所有打印机是否会被默认加载用于浏览。更多细节请参阅 "`printers`" 部分。
默认: `load printers = no`
示例: `load printers = no`

- `local group map` (G)
此选项允许你指定一个文件，该文件包含单个 NT 本地组（在任何域中）到 UNIX 组名的唯一映射。这使得尽管 UNIX 缺乏对基于 VAX/VMS 的 NT 安全模型的原生支持，但 NT 本地组（别名）仍可以呈现给 NT 用户。建议读者熟悉 NT 域系统及其管理。

此选项与 '`domain group map`' 和 '`domain name map`' 配合使用。当 Samba 不预期与任何 SAM 数据库（如工作站或域控制器）交互时，使用这些选项非常简单且通常是没必要的。

映射表按行解析。如果任何行以 '#' 或 ';' 开头，则会被被忽略。每行左侧应包含一个 UNIX 组名，右侧应包含一个 NT 本地组名，用制表符或 '=' 分隔。如果每个名称包含空格，则应用引号括起来。该行的格式可以是：

```
UNIXgroupname \DOMAIN_NAME\LocalGroupName
```

或：
```
UNIXgroupname LocalGroupName
```



当 Samba 是实验性（`EXPERIMENTAL`）域控制器或使用 `security = domain` 的域成员时，可以使用后一种格式：默认域名是 Samba 服务器的名称，由 `workgroup = MYGROUP` 指定。
任何未在映射映射文件中指定的 UNIX 组将根据 Samba 服务器的角色被视为本地组或域组。

在 Samba 处于实验性（`EXPERIMENTAL`）域控制器的情况下，Samba 将其所有未指定的 UNIX 组作为其自身的 NT 域组呈现，名称相同，且不是本地组。

在 Samba 是使用 `security = domain` 的域成员的情况下，Samba 将通过其域控制器（参见 `password server`）检查该 UNIX 名称是否为 NT 域组。如果域控制器确认是，则未指定的（未映射的）且非 NT 域组的 UNIX 组将被视为 Samba 本地 SAM 数据库中的本地组。NT 管理员将此强调为工作站本地组，通过运行 `USMGR.EXE` 并选择远程域 `WORKSTATION_NAME`，或在本地工作站上运行 `USMGR.EXE` 来管理。

这听起来可能很复杂，但这意味着 Samba 服务器将分别像域成员（带有本地 SAM 数据库的情况下）或不像 PDC（带有 Samba 数据库的情况下），而完全不需要任何映射文件。然而，如果你想花点心思，也可以这样做。

请注意，将任意域中的任意 NT 组映射到任意 UNIX 组`需要`以下条件：

- UNIX 组存在于 UNIX 服务器上。
- NT 域存在于指定的 NT 域中。
- UNIX 服务器知晓指定的域；
- UNIX 组中所有（期望以正确的 NT 用户身份和正确的组权限访问 Samba 服务器的） UNIX 用户已使用 `domain user map` 映射到指定 NT 域中的正确 NT 域。

未能满足任何这些要求都可能导致日志文件中报告任一（或两种）错误，以及授予用户的错误或缺失的访问权限。

### `local master` (G)
此选项允许 `nmbd` 尝试成为子网上的本地主（`local master browser`）。如果为 `False`，则 `nmbd` 将不会尝试成为子网上的本地主，并且将在所有浏览选举中失败。默认情况下，此值设置为 `true`。将此值设置为 `true` 意味着 Samba 将成为子网上的本地主，而是意味着 `nmbd` 将参与本地主选举。

将此项值设置为 `False` 将导致 `nmbd` 永远不会成为本地主。

默认: `local master = yes`

### `lock dir` (G)
`lock directory` 的同义词。

### `lock directory` (G)
此选项指定放置锁文件的目录。锁文件用于实现 `max connections` 选项。

默认: `lock directory = /tmp/samba`
示例: `lock directory = /usr/local/samba/var/locks`

### `locking` (S)
此选项控制服务器是否响应客户端的锁定请求执行锁定操作。

如果 `locking = no`，所有锁定和解锁请求都将显示成功，且所有锁定查询都将指示所查询的锁是空闲。

如果 `locking = yes`，服务器将执行真实的锁定。

此选项对于可能不需要锁定的只读文件系统（如 CD-ROM 驱动器）可能有用，尽管在这种情况下不真正建议将此参数设置为 `no`。

请小心在全局或在特定服务中禁用锁定，因为缺少锁定可能会导致数据损坏。
默认: `locking = yes`
示例: `locking = no`

### `log file` (G)
此选项指定日志文件的路径。日志文件用于记录错误和其他信息。
默认: `log file = /var/log/samba`
示例: `log file = /var/log/samba/custom.log`

### `log level` (G)
`debug level` 的同义词。

### `logon drive` (G)
此选项指定挂载主目录的驱动器。
默认: `logon drive = h`
示例: `logon drive = z`

### `logon home` (G)
此参数指定服务器上主目录的路径。
默认: `logon home = /home`
示例: `logon home = /home/%user`

## 附录 C: Samba 手页

### `logon path` (G)
此选项指定存储漫游配置路径。
默认: `logon path = /home/profiles`
示例: `logon path = /profiles/%user`

### `logon script` (G)
此参数指定用户成功登录时下载并在上运行的批处理文件（`.bat`）或 NT 命令文件（`.cmd`）。文件必须包含 DOS cr/lf 结尾。建议使用 DOS 风格的编辑器创建文件。

脚本必须是相对于 `[logon]` 服务的路径。如果 `[logon]` 服务指定的路径为 `/usr/local/samba/netlog`，且 `logon script = START.BAT`，那么下载的文件将是

```
/usr/local/samba/netlog/STARTUP.BAT
```

批处理文件的内容完全由你决定。建议命令是添加 `TIME \SERVER /SET /YES`，强制每台机器与同一时间服务器同步时。另一个用途是添加 `NET USE U: \SERVER\UTILS` 用于常用工具，或例如使用 `NET Q: \SERVERISO9001_QA`。

请注意，特别重要的是不要允许对 `[logon]` 共享进行写入，或者在安全环境中授予用户对批处理文件的写入权限，这将允许批处理文件被任意修改并导致安全漏洞。

此选项采用标准替换，允许你为每个用户或机器拥有登录脚本。

请注意，此选项仅在 Samba 设置为登录服务器时才有用。

示例: `logon path = \\N\%user`

## `lppause` 命令 (S)

此参数指定了在服务器主机上执行的命令，用于停止打印或排队特定的打印作业。

该命令应该是一个程序或脚本，它接收打印机名称和作业号来解析打印作业。实现此功能的一种方法是使用作业优先级，优先级过低的作业将不会发送到打印机。

如果给出了 `"-p"`，则该参数将替换该位置。`"&j"` 被替换为作业号（整数）。在 HPUX 上（看到 `printing=hpux`），如果在 `lpq` 命令中添加了 `"-p"` 选项，账单将显示正确的状态，即：如果作业优先级低于设置优先级，则状态为 `PAUSED`（已暂停）；如果优先级相等或高于优先级，则状态为 `SPOLED`（已排队）或 `PRINTING`（打印中）。

注意，在 `lppause` 命令中包含绝对路径是一个良好的习惯，因为服务器可能无法使用 `PATH`。

另请参考 `printing` 参数。

默认值：目前此字符串没有赋值，除非 `printing` 参数的值为 `SYSV`，在这种情况下，默认值为：

```
lp -i p-%j -H hold
```

或者如果 `printing` 参数的值为 `softq`，则默认值为：

```
qstat -s -j% -h
```



HPUX 示例：`lppause command=/usr/bin/lpalt %p-%j -p0`

### - lpq 缓存时间 (G)

此项控制 `lpq` 信息缓存的时间，以防止频繁调用 `lpq` 命令。系统为使用的每种 `lpq` 命令变体保留单独缓存，因此如果你为不同的用户使用不同的 `lpq` 命令，它们将不会共享缓存信息。

缓存文件存储在 `/tmp/lpq.xxxx`，其中 `xxxx` 是使用的 `lpq` 命令的哈希值。

默认值为 10 秒，这意味着如果之前相同 `lpq` 命令的缓存数据小于 10 秒，将使用其缓存结果。如果你的 `lpq` 命令非常慢，建议设置较大的值。

值为 0 则完全禁用缓存。

另请参考 `printing` 参数。

默认值：`lpq cache time = 10`

示例：`lpq cache time = 30`

### - lpq 缓存命令 (S)

此参数指定了在服务器主机上执行的命令，用于获取 "`lpq`"-风格的状态信息。

该命令应该是一个程序或脚本，它接收打印机名称作为唯一参数并输出打印机状态信息。

附录 C：Samba 手页

目前支持八种风格的打印机状态：BSD、AIX、LPRNG、PLP、SYSV、HPUX、QNX 和 SOFTQ。涵盖了大多数 UNIX 系统。你可以通过 `printing =` 选项控制所需的类型。

某些客户端（特别是 Windows 工作组）可能无法正确发送其请求状态信息的打印机连接号。为了解决这个问题，服务器将报告连接到客户端的第一个打印服务器。这仅在发送的连接号无效时才会发生。

如果给出了 `%p`，则打印机名称将放在该位置。否则，它将放在命令末尾。

注意，在 `lpq` 命令中包含绝对路径是一个良好的习惯，因为服务器可能无法使用 PATH。

另请参考 `printing` 参数。

默认值：取决于 `printing` 的设置
示例：`lpq command = /usr/bin/lpq %p`

### - lpresume 命令 (HPUX)

此参数指定了在服务器主机上执行的命令，用于重启或继续打印或排队特定的作业。
该命令应该是一个程序或脚本，它接收打印机名称和作业号来恢复作业打印。另请参考 `pause command` 参数。

如果给出了 `%p`，则打印机名称将放在该位置。`%j` 被替换为作业号（整数）。

注意，在 `lpresume` 命令中包含绝对路径是一个良好的习惯，因为服务器可能无法使用 PATH。

另请参考 `printing` 参数。

默认值：
目前此字符串没有给出默认值，除非 `printing` 参数的值为 SYSV，在这种情况下，默认值为：

```
lp -i %p-%j -H resume
```

或者如果 `printing` 参数的值为 softq，则默认值为：

```
nstat -s %j -r
```



```
HPUX 示例：lpresume command = /usr/bin/lpalt %p-%j -p2
```

### lprm 命令 (S)

此参数指定了在服务器主机上执行的命令，用于删除打印作业。
该命令应该是一个程序或脚本，它接收打印机名称和作业号，并删除打印作业。
如果给出了 `%p`，则打印机名称将放在该位置。`%j` 被替换为作业号（整数）。

注意，在 `lprm` 命令中包含绝对路径是一个良好的习惯，因为服务器可能无法使用 PATH。

默认值：取决于 `"printing ="` 的设置
示例 1：`lprm command = /usr/bin/lprm -P%b %j`
示例 2：`lprm command = /usr/bin/cancel %p-%j`

## smb.conf (5)

### 机器密码超时 (G)

如果 Samba 服务器是 Windows NT 域的成员（见 `"printing"` 参数），此项控制机器密码在必须更改之前保持有效的时间。值单位为秒。默认值为 604800（7 天）。
如果 `"printing"` 参数设置为 `SYSV`，默认值为 86400（1 天）。
如果 `"printing"` 参数设置为 `softq`，默认值为 3600（1 小时）。

### 魔数输出 (magic output) (S)

此参数指定文件名，如果该文件被打开，将被执行。
默认值：`magic output = .out`
示例：`magic output = .txt`

### 魔法数脚本 (magic script) (S)

此参数指定文件名，如果该文件被打开，将被执行。
注意，在 `magic script` 命令中包含绝对路径是一个良好的习惯，因为服务器可能无法使用 PATH。
默认值：无
示例：`magic script = .csh`

### 混淆映射 (mangled map) (S)

这适用于那些想要直接将 UNIX 文件名映射到 DOS 兼容名称的用户。
默认值：无混淆映射
示例：`mangled map = (*.*)`

### 混淆名称 (mangled names) (S)

此项控制 UNIX 下的非 DOS 名称是否应映射为 DOS 兼容名称（“混淆”）并可见，或者是否简单忽略非 DOS 名称。

请参阅“MANGLING”章节以了解如何控制混淆过程的详情。

名称混淆（如果启用）允许文件从 Windows/DOS 在 UNIX 目录之间进行复制，同时保留长长的 UNIX 文件名。UNIX 文件可以从 Windows/DOS 处重命名为新的扩展名，并保留相同的路径。混淆后的名称在不同会话之间不会改变。

默认：`mangled names = yes`
示例：`mangled names = no`

#### 混淆字符 (mangling char, S)

此选项控制用于名称混淆的“魔法”字符。默认是 `-`，但这可能会干扰某些软件。使用此选项将其设置为你喜好的任何字符。

默认：`mangling char = ~`
示例：`mangling char = ^`

#### 混淆栈 (mangled stack, G)

此参数控制 Samba 服务器 `smbd` 中应缓存的混淆名称数量。
该栈是最近混淆的基名的列表（只有当扩展大于 3 个字符或包含大写字母时，才会保留扩展）。
值越大，混淆名称被成功转换为正确 UNIX 文件名的概率就越高。然而，较大的栈大小会减慢大多数目录访问。较小的栈可以节省服务器内存（每个栈元素消耗 256 字节）。
无法绝对保证长文件名的正确，因此请准备好面对惊喜！

默认：`mangled stack = 50`
示例：`mangled stack = 100`

#### 映射归档 (map archive, S)

此选项控制是否将 DOS 归档属性映射到 UNIX 所有者执行位。当文件自上次备份以来被修改时，DOS 归档位会被设置。此选项的一个动机是防止 Samba/你的 PC 将触过的任何文件在 UNIX 下都变为可执行文件。这对于共享源代码、文档等可能会非常困扰。
注意，`create mask` 参数的设置应确保所有者执行位不被掩码掉（即它必须包含 100）。详情请参见参数 `create mask`。

默认：`map archive = yes`
示例：`map archive = no`

#### 映射隐藏 (map hidden, S)

此选项控制是否将隐藏 风格隐藏文件映射到 UNIX 所有者执行位。
注意，`create mask` 参数的设置应确保所有者执行位不被掩码掉（即它必须包含 001）。详情请参见参数 `create mask`。

默认：`map hidden = no`
示例：`map hidden = no`

#### 映射系统 (map system, S)

此选项控制是否将 DOS 风格系统文件映射到 UNIX 组执行位。

注意，这需要设置 `create mask` 以确保组执行位不被掩码掉（即它必须包含 010）。详情请参见参数 `create mask`。

默认：`map system = no`
示例：`map system = no`

#### 映射到访客 (map to guest, G)

此参数仅在 `security=share` 以外的安全模式下有用——即 `user`、`server` 和 `domain`。

此参数可以取三个不同的值，它们告诉 `smbd` 如何处理在某种程度上不匹配有效 UNIX 用户的登录请求。
这三个设置分别是：

- `Never`——意味着拒绝密码无效的用户登录请求。这是默认值。
- `Bad User`——意味着拒绝密码无效的用户登录，除非用户名不存在，此时将会被视为访客登录并映射到“访客账户”。
- `Bad Password`——意味着密码无效的用户将被视为访客登录并映射到“访客账户”。注意这可能会导致问题，因为它意味着任何输入错误密码的用户都会被静默登录为“访客”——且不会收到密码错误的提示消息。如果你这样设置 `map to guest` 参数，帮助台服务会*恨死*你的。

注意，在使用其他安全模式时设置“访客”共享时需要此参数。这是因为在这些模式下，请求资源在服务器成功验证客户端之前*并不是*，因此服务器无法在正确的时间（连接共享时）为“访客”共享做出认证决策。

对于熟悉旧版 Samba 的人，这相当于 `local.h` 中 `Guest_SESSETUP` 值的旧时间设置。

默认：`map to guest = Never`
示例：`map to guest = Bad User`

#### 最大连接数 (max connections, S)

此选项允许限制对服务的并发连接数。如果 `max connections` 大于 0，则当已经打开该数量的服务连接时，新连接将被拒绝。值为 0 表示可以建立无限数量的连接。

使用锁文件来实现此功能。锁文件将存储在 `lock directory` 选项指定的目录中。

默认：`max connections = 0`
示例：`max connections = 10`

#### 最大磁盘大小 (max disk size, G)

此选项允许你对磁盘的显示大小设置上限。如果你将此选项设置为 100，则所有共享的显示大小都不会大于 100 MB。
注意，此选项并不限制你可以在磁盘上放置的数据量。在上述情况下，你仍然可以在磁盘上存储多于 100 MB 的数据，但如果客户端请求可用空间或总磁盘大小，结果将受限于 `max disk size` 中指定的数量。
此选项主要用于规避某些无法处理大磁盘的软件的 Bug，特别是大小超过 1GB 的磁盘。

`max disk size` 为 0 表示无限制。
默认：`max disk size = 0`
示例：`max disk size = 1000`

#### 最大日志大小 (max log size, G)

此选项（以 KB 为单位）指定了日志文件增长的最大大小。Samba 定期检查大小，如果超过则会重命名文件（添加扩展名）。值为 0 表示无限制。
默认：`max log size = 5000`
示例：`max log size = 1000`

#### 最大并发操作数 (max mux, G)

此选项控制 Samba 允许的最大并发 SMB 操作数。你通常不需要设置此参数。
默认：`max mux = 50`

#### 最大打开文件数 (maxopenfiles, G)

此参数限制了一个 `smbd` 进程任何时候可以打开的文件数量。此参数的默认值很高（10000），因为打开文件的限制通常是由进程的文件描述符限制决定的，而不是由此参数。
默认：`max open files = 1000`

#### 最大包大小 (max packet, G)

`packetsize` 的同义词。

#### 最大 TTL (max ttl, G)

此选项指定 `nmbd` 使用广播包或从 WINS 服务器请求名称时，NetBIOS 名称的默认生存时间（秒为）。你通常不需要更改此参数。默认值为 3 天。

默认：`max ttl = 259200`

#### 最大 Wins TTL (max wins ttl, G)

默认：`max wins ttl = 518400`

#### 最大传输 (max xmit, G)

此选项控制 Samba 协商的最大数据包大小。默认值为 65535，这是最大值。在某些情况下，较小的值可能会提高性能。低于 2048 的值会导致问题。

默认：`max xmit = 65535`
示例：`max xmit = 8192`

#### 消息命令 (message command, G)

这指定了当服务器接收 WinPopup 消息时运行的命令。这通常应该是某种能够传递消息的命令。这取决于你的想象力。

示例：
```



`message command = csh -c 'xedit %s;rm %s' &`

这使用 `xedit` 传递消息，随后将其删除。注意，命令立即返回非常重要。如果它不立即返回，你的电脑在发送消息时可能会冻结（希望30秒后恢复）。

所有消息都以全局访客用户的身份传递。命令带有标准替换符，`%u` 不起（在这种情况下 `%U` 可能更好）。

除了标准替换符，还有额外的替换符适用。特别是：

* "`%s`" = 消息的文件。
* "`%t`" = 消息发送的目标（可能是服务器名称）。
* "`%f`" = 消息的发件者。

你可以让此命令发送电子邮件，或者任何你喜欢的其他。如果你有任何真正的想法，请告诉我们。

这里有一种将消息作为邮件发送给 `root` 的方法：

```
message command = /bin/mail -s 'message from %f on %m' root <
%s; rm %s
```



进入`/path/to/xxx`目录，找到`xxx.json`。

如果你没有配置 `message command`，则消息将无法送达，Samba 会向发送者报告错误。遗憾的是，WWg 会完全忽略错误代码并继续运行，静静地删除它们，如下：

`"message command = rm %s"`

**默认值：**无 `message command`
示例：`message command = csh -c 'xedit;rm %s' &`

## min print space (S)
此选项设置了用户缓存打印作业之前必须可用的最小空磁盘空间。以千字节（KB）计算。默认值为 0，这意味着用户可以始终缓存打印作业。

另请参考 `printing` 参数。
**默认值：** `min print space = 0`
示例：`min print space = 2000`

## min wins ttl (G)
此选项告诉 `nmbd` 在作为 WINS 服务器运行（`wins support = true`）时，`nmbd` 处理的 NetBIOS 名称的“生存时间”是多少（秒）。你通常不需要更改此参数。默认值为 6 小时（21600 秒）。
**默认值：** `min wins ttl = 21600`

## name resolve (G)
此选项用于 Samba 套件中的程序来确定命名服务并将主机解析为 IP 地址。该选项接受一个由空格分隔的多个名称解析选项字符串。
选项有“lmhosts”、“host”、“wins”和“bcast”。它们导致按以下方式解析名称：

- `lmhosts：` 在 Samba hosts 文件中查找 IP 地址。
- `host：` 执行标准的主机到 IP 地址的解析，使用系统的 `/etc/hosts`、NIS 或 DNS 查找。这种名称解析方法依赖于操作系统，例如在 IRIX 或 Solaris 上，可能由 `/etc/nsswitch.conf` 文件控制。
- `wins：` 向 `wins server` 中列出的 IP 地址 处查询名称。如果未指定 WINS 服务器，将忽略此方法。
- `bcast：` 在 `interfaces` 参数中列出的每个已知本地接口上进行广播。这是名称解析方法中最不可靠的，因为它取决于目标主机是否在本地连接的子网上。
**默认值：** `name resolve = lmhosts wins bcast`

# 附录 C：Samba 手页

示例：`name resolve order = lmhosts bcast host`
这将导致检查本地 hosts 文件，然后尝试广播，最后进行正常的系统主机名查找。

## netbios aliases (G)
这是一组 `nmbd` 将作为 Samba 服务器已知标识的额外名称进行广播的 NetBIOS 名称列表。这允许一台机器在多个名称的列表中出现。如果一台机器正作为浏览服务器或登录服务器运行，则这些名称都不会被作为浏览服务器或登录服务器发布，只有机器的主机名称会带有这些功能发布。
另请参考 `netbios name`。
默认值：空字符串（无额外名称）
示例：`netbios aliases = TEST1 TEST2`

## netbios name (G)
此选项设置了用于标识 Samba 服务器的 NetBIOS 名称。默认情况下，它与主机 DNS 名称的第一个部分相同。如果机器作为浏览服务器或登录服务器，此名称（或主机 DNS 名称的第一个部分）将是这些服务发布时的名称。
另请参考 `netbios aliases`。
默认值：机器的 DNS 名称。
示例：`netbios name = MYNAME`

## nis homedir (G)
从 NIS 映射获取家目录服务器。对于使用自动挂载器的 UNIX 系统，用户的家目录通常会根据需要从远程服务器挂载到工作站上。
当 Samba 登录不是家目录服务器，而是通过 NFS 挂载家目录时，如果登录服务器告诉客户端使用自己作为家目录的 SMB 服务器（通过 SMB 和一个 NFS），则访问用户的家目录将需要两次网络跳转。这可能会非常慢。
此选项允许 Samba 返回家目录服务器为与登录服务器不同的服务器，只要家目录服务器上运行着 Samba 守护进程，它就会直接从目录服务器挂载到 Samba 客户端。当 Samba 向客户端返回家目录服务器时，它将咨询 `homedir map` 中指定的 NIS 映射并返回列出的服务器。
注意，要使此选项生效，必须有一个运行的 NIS 系统，并且带有此选项的 Samba 服务器也必须是一个登录服务器。
默认值：`nis homedir = false`
示例：`nis homedir = true`

# smb.conf (5)

## nt pipe support (G)
此布尔参数控制 `smbd` 是否允许 Windows 客户端连接到 NT SMB 特有的 IPC$ 管道。这是一个开发者调试选项，可以保持不变。
默认值：`nt pipe support = yes`

## nt smb support (G)
此布尔参数控制 `smbd` 是否与 Windows 客户端协商 NT 特有的 SMB 支持。虽然这是一个开发者调试选项且应该保持不变，但基准测试发现，Windows 客户端在将此选项设置为“no”时获得更快的性能。这仍在调查中。如果此选项设置为“no”，则 Samba 提供的 SMB 调用与 Samba 2.0 之前的版本提供的完全一致。如果任何用户在 NT SMB 支持方面遇到问题，此信息可能派用用。
默认值：`nt support = yes`

## null passwords (G)
允许或不允许客户端访问具有空密码的账户。
另请参考 `smbpasswd(5)`。
默认值：`null passwords = no`
示例：`null passwords = yes`

## ole locking compatibility (G)
此参数允许管理员关闭 Samba 内部的字节范围锁定，以兼容 OLE 应用程序。Windows 应用程序使用字节锁定作为进程间通信的形式。将此参数设置为“no”会导致管理器崩溃或溢出问题。
默认值：`ole locking compatibility = yes`
示例：`ole locking compatibility = no`

## only guest (S)
`guest only` 的同义词。

## only user (S)
这是一个布尔选项，控制允许 `user` 列表中的用户名连接。默认情况下此选项是禁用的，以便提供一个供服务器使用的用户名。
注意，这意味着 Samba 不尝试从服务名推断用户名。
另请参考 `user` 参数。
默认值：`only user = False`
示例：`only user = False`

## oplocks (S)
此布尔选项告诉 `smbd` 是否对文件打开请求发布 oplocks（机会性锁）。oplock 可以极大地提高 Samba 上文件访问的速度（约 30% 或更多）。它允许客户端激进地缓存文件，你可以在不稳定的环境中禁用它（在 Windows 中默认开启）。更多信息请参见 Samba 目录下的 `Speed.txt`。可以根据共享选择性地关闭某些文件的 oplocks。在某些系统上，底层操作系统识别 oplocks。这允许通过 Samba 或 NFS 或本地 UNIX 进程访问已锁文件进行数据同步。详情请参见内核 oplocks 参数。
默认值：`opocks = True`
示例：`opocks = False`

## os level (G)
此值控制 Samba 在选举中的自我宣传程度。此参数的值决定了 `nmbd` 是否有机会成为本地广播区域 WORKGROUP 的主浏览器。将其设置为 0 将导致 `smbd` 总是输给 Windows 机器。详情请参见 Samba 目录下的 `BROWSING.txt`。
默认值：`os level = 32`
示例：`os level = 65` ; 这将赢得任何 NT 服务器

## packet size (G)
这是一个废弃的参数，对当前的 Samba 代码没有影响。它留在参数列表中是为了防止破坏旧的 `smb.conf` 文件。

## panic action (G)
这是一个 Samba ，允许在 `smbd` 或 `nmbd` 崩溃时调用系统命令。这通常用于引起对问题发生的注意。
默认值：`panic action = <empty string>`

## passwd chat (G)
此字符串控制 `smbd` 与本地密码更改程序之间更改用户密码时进行的“对话”过程。Samba 描述了一系列响应-接收对，`smbd` 使用这些对来确定向密码程序发送什么以及期望返回什么。如果没有收到预期的输出，则密码不会更改。

此对话序列通常是特定的，具体取决于使用了何种本地密码控制方法（如 NIS 等）。

字符串可以包含宏 `%o` 和 `%n`，分别替换为旧密码和新密码。它还可以包含标准宏 `\n`、`\r`、`\t` 和 `\s` 来提供换行、回车和制表符。

字符串还可以包含 `*`，它可以匹配任何字符序列。

双引号可用于对话序列的任何部分收集字符串，如果后面是句号 `.`，则不设置字符串。同样，如果预期的字符串是句号，则不期待字符串。

请注意，如果 `unix password sync` 参数设置为 `true`，当 `smbpasswd` 文件中的密码更改时，此序列会被调用为 `AS ROOT`，且无需访问旧密码明文。该旧密码明文被设置为 `""`（空字符串）。

另参见 `unix password sync` `passwd program` 和 `password debug`：示例：

```
# smb.conf (5) 285
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



当然，久而之可能会很烦人 :-)

### postscript (S)
此参数强制打印机将打印文件解释为 postscript。这是通过在输出开头添加 `!` 实现的。
当你有很多 PC 固执在打印作业开头放置控制-D 时，这在混淆你的打印机时非常有用。
默认：`postscript = False`
示例：`postscript = False`

### preferred master (S)
此布尔参数控制 `nmbd` 是否为其工作组的优选主浏览器。

# smb.conf (5) 289

如果此项设置为 true，启动时，`nmbd` 将强制进行选举，并且在选举中具有微弱优势。建议将此参数与 `domain master = yes` 配合使用，以便 `nmbd` 能够保证成为域主大师。默认值 `auto` 在 Samba 被配置为域主浏览器时会启用 `preferred master`。

请谨慎使用此选项，因为如果同一子网内有多个主机（无论是 Samba 服务器、Windows 95 还是 NT）都是首选主浏览器，它们将都会定期且持续地尝试成为本地主浏览器。这将导致不必要的广播流量并降低浏览能力。另请参阅 `os level`。

默认：`preferred master = auto`
示例：`preferred master = yes`

### preferred master (G)
对于不会拼写的人来说，`preferred master` 的同义词。

### preload
`auto services` 的同义词。

### preserve case (S)
这控制新文件名是使用客户端传递的大小写创建，还是强制使用 `默认` 大小写。

默认：`preserve case = yes`
更详细的讨论请参阅 `NAME MANGLING` 章节。

### print command (S)
在打印作业完成到服务的池化后，此命令将通过 `system()` 调用处理打印池文件。通常情况下，指定的命令会将打印池文件提交给主机的打印子系统，但并不要求这样做。服务器不会删除打印池文件，因此你指定的任何内容都应该在处理后删除打印池文件，否则你需要手动删除打印池文件。

`print command` 是文本字符串。它将原样使用，但有两个例外：所有的 `"%s"` 出现将被替换为相应的打印池文件名，`"%f"` 的出现将被替换为相应的打印机名称。打印池文件由服务器自动生成，打印机名称见下文讨论。

如果 `"%s"` 前没有 `'/'`，则将使用完整路径作为文件名。如果你不喜欢（这会弄乱 `lpq` 输出），请使用 `"%f"` 代替。`"%f"` 的出现将被替换为不带前面完整路径的打印池文件名。

`print command` 必须包含至少一次 `"%s"` 或 `"%f"`——`"%p"` 是可选的。在提交作业时，如果没有通过 `"%p"` 提供打印机名称，

如果在 `[global]` 部分指定，则给定的 `print command` 将用于任何没有指定单独 `print command` 的打印服务。

如果可打印服务既没有指定的 `print command`，也没有全局 `print command`，将创建打印池文件但不会进行处理（最重要的是）不会被删除。

注意，在某些 UNIX 上，打印可能会通过 `nobody` 账户失败。如果发生这种情况，请创建一个可以打印的备用访客账户，并在 `global` 部分设置 `guest account`。

通过意识到这些命令只是传递给 shell，你可以形成相当复杂的命令。例如，以下命令将记录打印作业、打印文件，然后删除它。注意 `;` 是 shell 脚本中命令的常用分隔符。

```
print command = echo Printing %s >> /tmp/print.log; lpr -P %p %s; rm %s
```

你可能需要根据你通常在系统中打印文件的方式大幅更改此命令。该参数的默认值取决于 `printing` 设置。

默认：`printing=` BSD, AIX, QNX, LPRNG 或 PLP : `print command = lpr -r -Pp %s`

对于 `printing=` SYS 或 HPUX ： `print command = lp -c -dp %s; rm %s`

对于 `printing=` SOFTQ ： `print command = lp -dp %s; rm %s`
示例：`print command = /usr/local/samba/bin/myprint-script %p %s`

### print ok (S)
`printable` 的同义词。

### printable (S)
如果为 `yes`，则客户端可以对服务的目录打开、写入并提交打印池文件。

注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。`read only` 参数只控制对资源的非打印访问。

默认：`printable = no`
示例：`printable = yes`

### printcap (G)
`printcapname` 的同义词。

### printcap name (G)
此参数可用于覆盖服务器编译的默认 `printcap`（通常为 `/etc/printcap`）。查看 `[printers]` 章节的讨论以了解你可能想这样做的原因。

在使用 `lpstat` 列出可用打印机的 System V 系统上，你可以使用 `printcap` 列出可用打印机，可以使用 `printcap name = lpstat` 自动获取可用打印机列表。这是

一个最小的 `printcap` 文件看起来如下：

```
print1|My Printer 1
print2|My Printer 2
print3|My Printer 3
print4|My Printer 4
print5|My Printer 5
```

其中 `|` 分隔打印机的别名。第二个别名包含空格，提示 Samba 这是一个注释。

> 注意：AIX 默认 `printcap name` 为 `"/etc/qconfig"`。如果 `printcap` 中出现 `"/etc/qconfig"` 字符串，Samba 将假设文件为 AIX `qconfig` 格式。

默认：`printcap name = /etc/qconfig`
示例：`printcap name = /etc/qconfig`

### print ok (S)
`printable` 的同义词。

### printer (S)
如果为 `yes`，则客户端可以对服务的目录打开、写入并提交打印池文件。注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。`read only` 参数只控制对资源的非打印访问。

默认：`printable = no`
示例：`printable = yes`

### printcap (G)
`printcapname` 的同义词。

### printcap name (G)
此参数可用于覆盖服务器编译的默认 `printcap`（通常为 `/etc/printcap`）。查看 `[printers]` 章节的讨论以了解你可能想这样做的原因。

在使用 `lpstat` 列出可用打印机的 System V 系统上，你可以使用 `printcap` 列出可用打印机，可以使用 `printcap name = lpstat` 自动获取可用打印机列表。这是

一个最小的 `printcap` 文件看起来如下：

```
print1|My Printer 1
print2|My Printer 2
print3|My Printer 3
print4|My Printer 4
print5|My Printer 5
```



其中 `|` 分隔打印机的别名。第二个别名包含空格，提示 Samba 这是一个注释。

> 注意：AIX 默认 printcap name 为 `"/etc/qconfig"`。如果 printcap 中出现 `"/etc/qconfig"` 字符串，Samba 将假设文件为 AIX `"qconfig"` 格式。

默认：`printcap name = /etc/qconfig`
示例：`printcap name = /etc/qconfig`

### `- print ok (S)`
`printable` 的同义词。

### `- printer (S)`
如果为 `yes`，则客户端可以对服务的目录打开、写入并提交打印池文件。注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。`read only` 参数只控制对资源的非打印访问。

默认：`printable = no`
示例：`printable = yes`

### `- printcap (G)`
`printcapname` 的同义词。

### `- printcap name (G)`
此参数可用于覆盖服务器编译的默认 printcap（通常为 `/etc/printcap`）。查看 `[printers]` 章节的讨论以了解你可能想这样做的原因。

在使用 `lpstat` 列出可用打印机的 System V 系统上，你可以使用 `"printcap"` 列出可用打印机，可以使用 `"printcap name = lpstat"` 自动获取可用打印机列表。这是

## smb.conf (5)

### `- preferred master (G)`
对于不会拼写的人来说，`preferred master` 的同义词。

### `- preload`
`auto services` 的同义词。

### `- preserve case (S)`
这控制新文件名是使用客户端传递的大小写创建，还是强制使用 `默认` 大小写。

默认：`preserve case = yes`
更详细的讨论请参阅 `NAME MANGLING`（名称转换）章节。

### `- print command (S)`
在打印作业完成到服务的池化后，此命令将通过 `system()` 调用处理打印池文件。通常情况下，指定的命令会将打印池文件提交给主机的打印子系统，但并不要求这样做。服务器不会删除打印池文件，因此你指定的任何内容都应该在处理后删除打印池文件，否则你需要手动删除打印池文件。

`print command` 是文本字符串。它将原样使用，但有两个例外：所有的 `"%s"` 出现将被替换为相应的打印池文件名，`"%f"` 的出现将被替换为相应的打印机名称。打印池文件由服务器自动生成，打印机名称见下文讨论。

如果 `"%s"` 前没有 `'/'`，则将使用完整路径作为文件名。如果你不喜欢（这会弄乱 `lpq` 输出），请使用 `"%f"` 代替。`""%f"` 的出现将被替换为不带前面完整路径的打印池文件名。

`print command` 必须包含至少一次 `"%s"` 或 `"%f"`——`"%p"` 是可选的。在提交作业时，如果没有通过 `"%p"` 提供打印机名称，

如果在 `"[global]"` 部分指定，则给定的 `print command` 将用于任何没有指定单独 `print command` 的打印服务。

如果可打印服务既没有指定的 `print command`，也没有全局 `print command`，将创建打印池文件但不会进行处理（最重要的是）不会被删除。

注意，在某些 UNIX 上，打印可能会通过 `nobody` 账户失败。如果发生这种情况，请创建一个可以打印的备用访客账户，并在 `global` 部分设置 `guest account`。

通过意识到这些命令只是传递给 `shell`，你可以形成相当复杂的命令。例如，以下命令将记录打印作业、打印文件，然后删除它。注意 `;` 是 `shell` 脚本中命令的常用分隔符。

```
print command = echo Printing %s >> /tmp/print.log; lpr -P %p %s; rm %s
```

你可能需要根据你通常在系统中打印文件的方式大幅更改此命令。该参数的默认值取决于 `printing` 设置。

默认：`printing=` BSD, AIX, QNX, LPRNG 或 PLP : `print command = lpr -r -Pp %s`

对于 `printing=` SYS 或 HPUX ： `print command = lp -c -dp %s; rm %s`

对于 `printing=` SOFTQ ： `print command = lp -dp %s; rm %s`
示例：`print command = /usr/local/samba/bin/myprint-script %p %s`

### `- print ok (S)`
`printable` 的同义词。

### `- printable (S)`
如果为 `yes`，则客户端可以对服务的目录打开、写入并提交打印池文件。注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。`read only` 参数只控制对资源的非打印访问。

默认：`printable = no`
示例：`printable = yes`

### `- printcap (G)`
`printcapname` 的同义词。

### `- printcap name (G)`
此参数可用于覆盖服务器编译的默认 printcap（通常为 `/etc/printcap`）。查看 `[printers]` 章节的讨论以了解你可能想这样做的原因。

一个最小的 printcap 文件看起来如下：

```
print1|My Printer 1
print2|My Printer 2
print3|My Printer 3
print4|My Printer 4
print5|My Printer 5
```

其中 `|` 分隔打印机的别名。第二个别名包含空格，提示 Samba 这是一个注释。

> 注意：AIX 默认 printcap name 为 `"/etc/qconfig"`。如果 printcap 中出现 `"/etc/qconfig"` 字符串，Samba 将假设文件为 AIX `"qconfig"` 格式。

默认：`printcap name = /etc/qconfig`
示例：`printcap name = /etc/qconfig`

## smb.conf (5) 291

## Appendix C: Samba Man Pages

客户端可以对服务的目录打开、写入并提交打印池文件。注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。



# smb.conf (5) 289

如果此项设置为 `true`，启动时，`nmbd` 将强制进行选举，并且在选举中具有微弱优势。建议将此参数与 `domain master = yes` 配合使用，以便 `nmbd` 能够保证成为域主大师。默认值 `auto` 在 Samba 被配置为域主浏览器时会启用 `preferred master`。

请谨慎使用此选项，因为如果同一子网内有多个主机（无论是 Samba 服务器、Windows 95 还是 NT）都是首选主浏览器，它们将都会定期且持续地尝试成为本地主浏览器。这将导致不必要的广播流量并降低浏览能力。另请参阅 `os level`。

默认：`preferred master = auto`

示例：`preferred master = yes`

## `preferred master` (G)

对于不会拼写的人来说，`preferred master` 的同义词。

## `preload`

`auto services` 的同义词。

## `preserve case` (S)

这控制新文件名是使用客户端传递的大小写创建，还是强制使用“默认”大小写。

默认：`preserve case = yes`

更详细的讨论请参阅 `NAME MANGLING` 章节。

## `print command` (S)

在打印作业完成到服务的池化后，此命令将通过 `system()` 调用处理打印池文件。通常情况下，指定的命令会将打印池文件提交给主机的打印子系统，但并不要求这样做。服务器不会删除打印池文件，因此你指定的任何内容都应该在处理后删除打印池文件。

`print command` 是文本字符串。它将原样使用，但有两个例外：所有的 `"%s"` 出现将被替换为相应的打印池文件名，`"%f"` 的出现将被替换为相应的打印机名称。打印池文件由服务器自动生成，打印机名称见下文讨论。

如果 `"%s"` 前没有 `'/'`，则将使用完整路径作为文件名。如果你不喜欢（这会弄乱 `lpq` 输出），请使用 `"%f"` 代替。`"%f"` 的出现将被替换为不带前面完整路径的打印池文件名。

`print command` 必须包含至少一次 `"%s"` 或 `"%f"`——`"%p"` 是可选的。在提交作业时，如果没有通过 `"%p"` 提供打印机名称，

如果在 `[global]` 部分指定，则给定的 `print command` 将用于任何没有指定单独 `print command` 的打印服务。

如果可打印服务既没有指定的 `print command`，也没有全局 `print command`，将创建打印池文件但不会进行处理（最重要的是）不会被删除。

注意，在某些 UNIX 上，打印可能会通过 `nobody` 账户失败。如果发生这种情况，请创建一个可以打印的备用访客账户，并在 `global` 部分设置 `guest account`。

通过意识到这些命令只是传递给 shell，你可以形成相当复杂的命令。例如，以下命令将记录打印作业、打印文件，然后删除它。注意 `;` 是 shell 脚本中命令的常用分隔符。

```
print command = echo Printing %s >> /tmp/print.log; lpr -P %p %s; rm %s
```

你可能需要根据你通常在系统中打印文件的方式大幅更改此命令。该参数的默认值取决于 `printing` 设置。

默认：
`printing = BSD, AIX, QNX, LPRNG` 或 `PLP` : `print command = lpr -r -Pp %s`
对于 `printing = SYS` 或 `HPUX` ： `print command = lp -c -dp %s; rm %s`
对于 `printing = SOFTQ` ： `print command = lp -dp %s; rm %s`

示例：`print command = /usr/local/samba/bin/myprint-script %p %s`

## `print ok` (S)

`printable` 的同义词。

## `printable` (S)

如果为 `yes`，则客户端可以对服务的目录打开、写入并提交打印池文件。注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。`read only` 参数只控制对资源的非打印访问。

默认：`printable = no`

示例：`printable = yes`

## `printcap` (G)

`printcapname` 的同义词。

## `printcap name` (G)

此参数可用于覆盖服务器编译的默认 `printcap`（通常为 `/etc/printcap`）。查看 `[printers]` 章节的讨论以了解你可能想这样做的原因。

在使用 `lpstat` 列出可用打印机的 System V 系统上，你可以使用 `printcap` 列出可用打印机，可以使用 `printcap name = lpstat` 自动获取可用打印机列表。这是

一个最小的 `printcap` 文件看起来如下：

```
print1|My Printer 1
print2|My Printer 2
print3|My Printer 3
print4|My Printer 4
print5|My Printer 5
```



其中 `|` 分隔打印机的别名。第二个别名包含空格，提示 Samba 这是一个注释。

> 注意：AIX 默认 printcap name 为 "/etc/qconfig"。如果 printcap 中出现 "/etc/qconfig" 字符串，Samba 将假设文件为 AIX "qconfig" 格式。

默认：`printcap name` = `/etc/qconfig`
示例：`printcap name` = `/etc/qconfig`

- - `print ok` (S)
`printable` 的同义词。

- - `printer` (S)
如果为“yes”，则客户端可以对服务的目录打开、写入并提交打印池文件。注意，可打印服务将始终允许（在用户权限允许的情况下）写入服务路径以进行打印数据的池化。“read only”参数只控制对资源的非打印访问。

默认：`printable` = no
示例：`printable` = yes

- - `printcap` (G)
`printcapname` 的同义词。

- - `printcap name` (G)
此参数可用于覆盖服务器编译的默认 printcap（通常为 `/etc/printcap`）。查看 `[printers]` 章节的讨论以了解你可能想这样做的原因。

## smb.conf (5) 291

## Appendix C: Samba Man Pages

此文件由 Windows 95 "`msprint.def`" 文件创建。对于设置 Windows 95 驱动程序的更多详细信息，请查看 `docs/` 目录下的 `PRINTER_DRIVER.txt` 文件。

默认：None（编译时设置）。

- - `protocol` (G)

参数的值（字符串）是服务器支持的最高协议级别。

- `CORE`：最早版本。没有用户名的概念。
- `COREPLUS`：在 `CORE` 基础上的效率微改进。
- `LANMAN1`：第一个“现代”版本。长文件名

## smb.conf (5)

- `LANMAN2`: 对 Lanman1 协议的更新。
- `NT1`: 协议的最新版本。供 Windows NT 使用。被称为 CIFS。

通常不应设置此选项，因为 SMB 协议中的自动协商阶段会处理选择合适的协议。

默认：`protocol` = NT1
示例：`protocol` = LANMAN1

- `public` (S)
"`guest ok`" 的同义词。

- - `queuepause command` (S)
此参数指定了在服务器主机上执行的命令，用于暂停打印机队列。

该命令应该是一个程序或脚本，它以打印机名称作为唯一参数，并停止打印机队列，使得不再有新的作业提交到打印机。

Windows for Workgroups 不支持此命令，但可以在 Windows 95 & NT 的打印机窗口发送该命令。

如果给出一个 `"%"`，则打印机名称将放在该处。否则，它将放置在命令的末尾。

注意，在命令中包含绝对路径是一个良好习惯，因为服务器可能无法使用 PATH 变量。

默认值取决于 "`printing`" 的设置
示例：`queuepause command` = `disable %p`

- - `queueservice command` (S)
此参数指定了在服务器主机上执行的命令，用于恢复打印机队列。它是用于取消由上一个参数（"`queuepause command`”）引起的行为的命令。

该命令应该是一个程序或脚本，它以打印机名称作为唯一参数并恢复打印机队列，使得队列中的作业重新提交到打印机。

Windows for Workgroups 不支持此命令，但可以在 Windows 95 & NT 的打印机窗口发送该命令。

如果给出一个 `"%"`，则打印机名称将放在该处。否则，它将放置在命令的末尾。

注意，在命令中包含绝对路径是一个良好习惯，因为服务器可能无法使用 PATH 变量。

默认值取决于 "`printing`" 的设置
示例：`queuepause command` = `enable %p`

## Appendix C: Samba Pages

- `read bmpx` (G)
此布尔参数控制 `smbd` 是否支持“读取块多复用”（Read Block Multiplex）SMB。这现在很少使用，且默认关闭。你通常不需要设置此参数。

默认：`read bmpx` = No

- `read list` (S)
这是一个被赋予服务只读权限的用户列表。如果连接的用户在此列表中，那么无论“read only”选项如何设置，他们都将没有写权限。该列表可以包含使用“invalid users”参数中描述语法的组名。

另见“write list”参数和“invalid users”参数。

默认：`read list` = `<empty string>`
示例：`read list` = `mary, @students`

- `read only` (S)
注意，这是“writeable”和“write ok”的反反义同义词。另见“writeable”和“write ok”。

- `read prediction` (G)
注意：此代码在 Samba 2.0 中已禁用，并可能在以后日期移除。因此，此参数不起作用。

此选项启用或禁用用于加速从服务器读取数据的读取预测代码。当当服务器在等待数据包时，它将尝试从以只读方式打开的最后访问的文件预读数据。

默认：`read prediction` = False

- `read raw` (G)
此参数控制服务器在向客户端传输数据时是否支持原始 SMB 请求。

如果启用，`read raw` 允许在一个数据包中读取 65535 字节。这通常会提供巨大的性能优势。

然而，某些客户端错误地协商了允许的块大小，或者无法支持更大的块大小，在这些情况下你需要禁用 raw raw。

通常，此参数应被视为系统调优工具并尽量不要动它。另见“write raw”。

默认：`read raw` = yes

- `read size` (G)
“`read size`”选项影响磁盘读/写与网络读/写的重叠。如果在几个 SMB 命令中传输的数据量（目前为 `SMBwrite`、`SMBwriteX` 和 `SMBreadraw`）大于该值，则服务器开始写入从网络接收到的整个包的数据，

```
remote announce = 192.168.2.255/SERVERS 192.168.4.255/STAFF
```

默认：`remote announce` = `<empty string>`

示例：`remote announce` = `192.168.2.255/SERVERS 192.168.4.255/STAFF`

```
remote browse sync = 192.168.2.255 192.168.4.255
```



上述行将导致 `nmbd` 请求指定子网或地址上的主服务器，以便将其浏览列表与本地服务器同步。

你选择的 IP 地址通常是远程网络的广播地址，但如果你的网络配置稳定，也可以是已知网主（grouse masters）的 IP 地址。如果给出机器 IP，Samba 不会尝试验证远程机器是否可用、正在监听，或它是否确实是该网段的网主。

默认：`remote browse sync = <empty string>`
示例：`remote browse sync = 192.168.2.255 192.168.4.255`

### revalidate (S)

注意，此选项仅与 `security = share` 有效，如果不是这种情况则将被忽略。

此选项控制 Samba 是否允许通过验证用户来访问共享。

如果 `revalidate` 设置为 `True`，则将允许。

默认：`revalidate = False`

# 298

# 附录 C: Samba 帮助页

请注意，`smbd` *始终* 会使用一个有效的 UNIX 用户来代表客户端执行操作，即使在 `security = share` 级安全下也是如此。

由于在共享级安全模式下，客户端不需要向服务器发送用户名，`smbd` 使用了多种技术来确定代表客户端使用的正确 UNIX 用户。

使用以下方法构建一个可能与客户端密码匹配的可能 UNIX 用户名列表：

- 如果设置了 `guest only` 参数，将跳过所有其他阶段，仅检查 `guest account` 用户名。
- 如果在共享连接请求设置了用户名，则该用户名（映射后——参见 `username map`）将作为潜在用户名添加。
- 如果客户端之前有过 `SessionSetup` SMB 调用，则此 SMB 中发送的用户名将作为潜在用户名添加。
- 所请求的客户端 NetBIOS 名称将作为潜在用户名添加到列表中。
- `user` 列表中的任何用户都将作为潜在用户名添加。

如果未设置 `guest only` 参数，则将使用提供的密码尝试此列表。密码匹配的用户将用作 UNIX 用户。

如果设置了 `guest only` 参数，或者无法确定用户名，那么如果该共享被标记为 `guest account` 可用，则将使用该访客用户，否则将被拒绝。

请注意，在共享级安全模式下，最终使用哪个 UNIX 用户授予访问权限可能会 *非常* 令人困惑。

另见 `NOTE ABOUT USERNAME/PASSWORD VALIDATION` 章节。

这是 Samba2 的默认设置。在用户级安全模式下，客户端必须使用有效的用户名和密码进行 `login`（可以使用 `username map` 参数进行映射）。在此模式下也可以使用加密密码（参见 `encrypted passwords` 参数）。诸如 `user` 和 `guest only` 等参数，如果设置，则会被应用并可能更改此连接使用的 UNIX 用户，但仅在用户通过身份验证后进行。

请注意，在服务器成功验证客户端之前，所请求的资源名称 *并不是* 服务器。这就是为什么在允许服务器自动将未知用户映射到 `guest account` 的情况下，访客在共享级安全模式下无法工作。有关此操作的详细信息，请参见 `map to guest` 参数。

另见 `NOTE ABOUT USERNAME/PASSWORD VALIDATION` 章节。

在这种模式下，Samba 将尝试通过将用户名/密码传递给另一个 SMB 服务器（作为 NT 节点）来验证它们。如果失败，它将回退到 `security = user`，但由于已经协商了加密密码，Samba 无法回退检查 UNIX 密码文件，它必须有一个有效的 `smbpasswd` 来检查用户。请查看 `docs/` 目录下的文档 `ENCRYPTION.txt` 了解如何设置的详情。

## smb.conf (5)

请注意，从客户端的角度来看，`security = server` 与 `security = user` 是相同的。它只影响服务器处理身份验证的方式，不会以任何方式影响客户端看到的内容。

请注意，在服务器成功验证客户端之前，所请求的资源名称 *不会* 发送给服务器。这就是为什么在允许服务器自动将未知用户映射到 `guest account` 的情况下，访客共享在服务器级安全模式下无法工作。有关此点的详细信息，请参见 `map to guest` 参数。

参见 `NOTE ABOUT USERNAME/PASSWORD VALIDATION` 章节。另参见 `password server` 参数以及 `encrypted passwords` 参数。

### security = domain

只有在用 `smbpasswd` 将此机器加入 Windows NT 域后，此才能正常工作。它期望 `encrypted passwords` 参数被设置为 `true`。在此模式下，Samba 通过将用户名/密码传递给 Windows NT 主域控制器或备份域控制器来验证它们，方法与 Windows NT Server 的完全相同。

### security = user

这与服务器的相同的，直到服务器成功验证客户端之后。请注意，在服务器成功验证客户端之前，所请求的资源名称 *并不是* 服务器的。这就是为什么在允许服务器自动将未知用户映射到访客账户的情况下，访客在共享级安全模式下无法工作。参见 `map to guest` 参数。

- 29

# 298

# 附录 C: Samba 帮助页



# 298

# 附录 C: Samba 帮助页

请注意，`smbd` *始终* 会使用一个有效的 UNIX 用户来代表客户端执行操作，即使在“安全共享”级安全模式下也是如此。

由于在共享级安全模式下，客户端不需要向服务器发送用户名，`smbd` 使用了多种技术来确定代表客户端使用的正确 UNIX 用户。

使用以下方法构建一个可能与客户端密码匹配的可能 UNIX 用户列表：

- 如果设置了“仅来”(`guest only`)参数，将跳过所有其他阶段，仅检查“访客账户”(`guest account`)用户名。
- 如果在共享连接请求设置了用户名，则该用户名（映射后——参见“用户名映射”(`username map`)）将作为潜在用户名添加。
- 如果客户端之前有过“登录”请求（`SessionSetup` SMB 调用），则此 SMB 中发送的用户名将作为潜在用户名添加。
- 所请求的客户端 NetBIOS 名称将作为潜在用户名添加到列表中。
- “user”列表中的任何用户都将作为潜在用户名添加。

如果未设置“仅来”参数，将使用提供的密码尝试此列表。密码匹配的用户将用作 UNIX 用户。

如果设置了“仅来”参数，或者无法确定用户名，那么如果该共享被标记为“访客账户”可用，则将使用该访客用户，否则将被拒绝。

请注意，在共享级安全模式下，最终使用哪个 UNIX 用户授予访问权限可能会*非常*令人困惑。

另见“关于用户名/密码验证的注意”（`NOTE ABOUT USERNAME/PASSWORD VALIDATION`）章节。

- `security=user`

这是 Samba2 的默认设置。在用户级安全模式下，客户端必须使用有效的用户名和密码进行“登录”（可以使用“用户名映射”参数进行映射）。在此模式下也可以使用加密密码（参见“加密密码”(`encrypted passwords`) 参数）。诸如“user”和“仅来”等参数，如果设置，则会被应用并可能更改此连接使用的 UNIX 用户，但仅在用户通过身份验证后进行。

请注意，在服务器成功验证客户端之前，所请求的资源名称*并不是*服务器。这就是为什么在允许服务器自动将未知用户映射到“访客账户”的情况下，访客在共享级安全模式下无法工作。有关此操作的详细信息，请参见“映射到访客”(`map to guest`) 参数。

另见“关于用户名/密码验证的注意”章节。

- `security=server`

在这种模式下 Samba 将尝试通过将用户名/密码传递给另一个 SMB 服务器（作为 NT 节点）来验证它们。如果失败，它将回退到 `security = user`，但由于已经协商了加密密码，Samba 无法回退检查 UNIX 密码文件，它必须有一个有效的 `smbpasswd` 来检查用户。请查看 `docs/` 目录下的文档 `ENCRYPTION.txt` 了解如何设置的详情。

## smb.conf (5)

请注意，从客户端的角度来看，`security=server` 与 `security=user` 是相同的。它只影响服务器处理身份验证的方式，不会以任何方式影响客户端看到的内容。

请注意，在服务器成功验证客户端之前，所请求的资源名称*不会*发送给服务器。这就是为什么在允许服务器自动将未知用户映射到访客账户的情况下，访客共享在服务器级安全模式下无法工作。有关此点的详细信息，请参见“映射到访客”(`map to guest`) 参数。

参见“关于用户名/密码验证的注意”章节。另参见“密码服务器”(`password server`) 参数以及“加密密码”(`encrypted passwords`) 参数。

- `security=domain`

只有在用 `smbpasswd` 将此机器加入 Windows NT 域后，此才能正常工作。它期望“加密密码”(`encrypted passwords`) 参数被设置为“true”。在此模式下，Samba 通过将用户名/密码传递给 Windows NT 主域控制器或备份域控制器来验证它们，方法与 Windows NT Server 的完全相同。

# 附录 C：Samba 手页

- `SO_RCVBUF`
- `SO_SNDLOWAT`
- `SO_RCVLOWAT`

标记为 * 的项接受一个整数参数。其他项可以可选地接受 1 或 0 参数来启用或禁用选项；默认情况下，如果不指定 1 或 0，它们将被启用。

要指定参数，请使用 `SOME_OPTION=VALUE` 语法，例如 `SO_SNDBUF=8192`。请注意，等号前后不能有任何空格。

如果你处于局域网中，一个合理的选项可能是：

```
socket options = IPTOS_LOWDELAY
```

如果你处于局域网中，你可以尝试：

```
socket options = IPTOS_LOWDELAY TCP_NODELAY
```

如果你处于广域网中，也许可以设置 `IPTOS_THROUGHPUT`。注意，某些选项可能会导致你的 Samba 服务器完全无法运行。请谨慎使用这些选项！

默认：`socket options = TCP_NODELAY`

示例：`socket options = IPTOS_LOWDELAY`

- `ssl` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

请注意，由于出口限制，此代码在你当前的 Samba 二进制版本中**没有**默认启用。

此变量启用或禁用 SSL 模式。如果设置为 "no"，则 SSL samba 的行为将与非 SSL 的 Samba 完全相同。如果设置为 "yes"，则取决于 `ssl hosts` 和 `ssl hosts resign` 变量来是否需要 SSL 连接。

默认：`ssl=no` 示例：`ssl=yes`

- `CA certDir` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

请注意，由于出口限制，此代码在你当前的 Samba 二进制版本中**没有**默认启用。

此变量定义了查找证书颁发机构（CA）的位置。通用目录应该包含每个 samba 信任的 CA 的一个文件。文件名必须是 CA 的“发行名称”（Distinguished Name）的哈希值。如何设置此目录将在本文稍后部分解释。目录中所有不符合此方案的文件都将被忽略。如果你不需要验证客户端证书，则不需要此变量。

默认：`CA certDir = /usr/local/ssl/certs`

- `ssl CA certFile` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

请注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

此变量是定义 CA 的另一种方法。受信任 CA 的证书被收集在一个大文件中，此变量指向该文件。你可能会使用定义 CA 的两种方法之一。如果你有许多 CA 或希望保持灵活，首种选择更优；如果你只有一个 CA 且想保持简单，第二种更优（你不需要创建哈希命名的文件）。如果你不验证客户端证书，则不需要此变量。

默认：`ssl CA certFile = /usr/local/ssl/certs/trustedCAs.pem`

- `ssl ciphers` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

请注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

此变量定义了在 SSL 协商期间应提供的加密算法。除非你清楚自己在做什么，否则不应设置此变量。

- `ssl client key` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

如果存在，文件中的证书将被 `smclient` 使用。如果服务器需要证书，则需要此文件。

默认：`ssl client key = /usr/local/ssl/certs/smclient.pem`

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

这是 `smclient` 的私钥。如果客户端应该拥有证书，则需要此文件。

默认：`ssl client key = /usr/local/ssl/private/smclient.pem`

- `ssl compatibility` (G)



此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

此变量定义了是否为了与其他 SSL 实现保持兼容。这可能是不需要的，因为目前没有其他 SSL 实现的客户端。

```
默认：ssl compatibility = no
```

### * ssl hosts (G)

查看 "ssl hosts"。

### * ssl hosts resign (G)

变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

这两个变量定义了 samba 是否进入 SSL 模式。如果定义了其中一个，samba 将仅允许连接。"ssl hosts" 变量（通过 IP 地址、IP 地址范围、组或名称）将强制进入 SSL 模式。这两个变量的语法与 "hosts allow" 和 "hosts deny" 变量相同，不同之处在于是否使用 SSL。"allow hosts" 参数示例要求来自局域网所有主机（即 192.168.*）的连接。

```
默认：ssl hosts = "" ssl hosts resign = ""
示例：ssl hosts resign = 192.168.*
```

### * ssl requirecert (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

如果此变量设置为 "yes"，服务器将不允许来自没有有效证书的客户端。"ssl CA certdir" 或 "ssl CA certFile" 中的目录/文件将用于查找签客户端证书的 CA。如果无法验证证书，连接将终止。如果此变量设置为 "no"，则客户端不需要证书。与 Web 应用不同，我们*应该*要求客户端证书。在客户端数据敏感的环境中，服务器必须证明自己是可信的；在服务器数据敏感的环境中，客户端必须证明自己是可信的。

**默认：**`ssl requirecert = no`

### * ssl requirecert (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

如果此变量设置为 "yes"，smbient 将向服务器请求证书。与服务器的 "ssl requirecert" 相同。

**默认：**`ssl requirecert = no`

### * ssl server cert (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

这是包含服务器证书的文件。服务器必须有一个证书。该文件可能包含服务器的私钥。有关如何创建证书和私钥请见后文。

**默认：**`ssl server cert = ""`

### * ssl server key (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

此文件包含服务器的私钥。如果未定义此变量，则会在证书文件中查找密钥（它可能附加在证书后面）。服务器*必须*有一个私钥，且证书*必须*匹配此私钥。

**默认：**`ssl server key = ""`

### * ssl version (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

# 附录 C: Samba 手页

此枚举变量定义了将使用的 SSL 协议版本。"ssl12or3" 允许 SSL v2 或 v3 的动态协商，“ssl12" 产生 SSL v2，“ssl13" 产生 SSL v3，而 "tls1" 产生 TLS v1。TLS（传输层安全）是 SSL 的（建议的？）新标准。

默认值：`ssl version = "ssl12or3"`

### * stat cache (G)

此参数决定 `smbd` 是否将使用缓存来加速不区分大小写的名称映射。你通常不需要更改此参数。

默认值：`stat cache = yes`

### * stat cache size (G)

此参数决定 stat 缓存中条目的数量。你通常不需要更改此参数。

默认值：`stat cache size = 50`

### * status (G)

此项允许禁用对 `smbtatus` 可以读取的状态文件的连接锁定。如果禁用了此项，`smbtatus` 将无法判断哪些连接是活跃的。你通常不需要更改此参数。

默认值：`status = yes`

### * strict locking (S)

这是一个控制服务器上文件锁处理的布尔值。当此设置为 "yes" 时，服务器将检查每次读写访问是否存在文件锁，如果存在锁则拒绝访问。这在某些系统上可能会很慢。

当 `strict locking` 为 "no" 时，服务器仅在客户端请求锁时才进行文件锁定。

良好的客户端在重要时总是会请求锁，在大多数情况下，“strict locking = no" 是优的。

默认值：`strict locking = no`

示例：`strict locking = yes`

### * strict sync (S)

许多 Windows 应用程序（包括 Windows 98 资源管理器外壳）似乎通过与磁盘同步（sync）将缓冲区内容刷到磁盘。在 UNIX 下，sync 调用会强制进程挂起，直到内核确保内核缓冲区中所有待处理的数据已安全地存储在稳定性存储设备上。这非常慢，应该极少执行。将此参数设置为 "no"（默认值）意味着 `smbd` 忽略 Windows 的 sync 请求。只有在运行 Samba 的操作系统本身崩溃时，才存在丢失数据的可能性，因此此默认值危险很小。此外，它修复了人们报告的关于新 Windows98 资源管理器外壳文件复制的许多性能问题。

# smb.conf (5)

另见“sync always”参数。

```
默认值：strict sync = no
示例：strict sync = yes
```

### - - strip dot (G)

这是一个布尔值，控制是否剥离 UNIX 文件名末尾的点。这有助于那些以单个点结尾的文件名的 CD-ROM。

默认值：`strip dot = no`

示例：`strip dot = yes`

### - - sync always (S)

这是一个布尔参数，控制在写入调用返回之前写入是否总是被写入存储器。如果为 false，则服务器将根据客户端每次写入调用的请求（客户端可以设置一个位来指示特定的写入应该是同步的）。如果为 true，则每次写入后都会跟随一个 `fsync()` 以确保数据写入磁盘。必须将“strict sync”参数设置为“yes”，此参数才能起作用。

另见“strict sync”参数。

默认值：`sync always = no`

示例：`sync always = yes`

### - - syslog (G)

此参数将 Samba 调试消息映射到系统 syslog 日志级别。Samba 调试级别 0 映射到 LOG_ERR，级别 1 映射到 LOG_WARNING，级别 2 映射到 LOG_DEBUG，级别 3 映射到 LOG_INFO。该参数设置了映射的阈值，所有高于此阈值的 Samba 调试消息都会映射到 syslog LOG_DEBUG 消息。

默认值：`syslog = 1`

### - - syslog only (G)

如果设置了此参数，Samba 调试消息将仅记录在系统中，而不是调试日志文件中。

默认值：`syslog only = no`

### - - time offset (G)

此参数是以分钟为单位的设置，用于在普通 GMT 到本地时间的转换上。如果你正在为许多夏令时间处理错误的 PC 提供服务，这非常有用。

默认值：`time offset = 0`

示例：`time offset = 0`

# 附录 C: Samba 手页

### - • time server (G)

此参数决定 `nmbd` 是否将自己作为时间服务器向 Windows 客户端广播。默认值为 False。

```
默认值：time server = False
```

```
示例：time server = True
```



### timestamp logs (G)

Samba2.0 默认会对所有日志目添加时间戳。如果你正在调试某个问题，这可能会分散注意力。此参数允许关闭时间戳。

```
默认值：timestamp logs = True
```

```
示例：timestamp logs = False
```

### unix password sync (G)

此布尔参数控制当加密的 `smpasswd` 文件更改时，Samba 是否尝试将 UNIX 密码与 SMB 密码同步。如果设置为 `true`，则 `password program` 参数中指定的密码——允许设置新的 UNIX 密码而无需访问旧 UNIX 密码（因为 SMB 密码已更改，对旧密码的访问已清除，只有新的）。默认情况下设置为 `false`。

另见 `password program`，`password chat`。

```
默认值：unix password sync = False
```

```
示例：unix password sync = True
```

### realmname (G)

此布尔参数在设置时会导致 Samba 提供域名（realm name）。这对于用户具有不同的用户名到用户名的情况有用。

```
默认值：realmname = no
```

```
示例：realmname = yes
```

### update encrypted (G)

此布尔参数在设置时允许用户更新加密后的密码。这对于迁移用户非常有用。

```
默认值：update encrypted = no
```

示例：`update encrypted = yes`

### use hosts (G)

如果此全局参数为真，它指定将读取用户家目录下的 UNIX `.hosts` 文件，以找到允许无密码访问的主机。

注意：使用 `hosts` 可能会导致严重的安全漏洞。因为你正在信任 PC 提供用户名。PC 很容易提供虚假的用户名。我建议只有在你确切知道做什么时才使用 `hosts` 选项。

```
默认值：use hosts = no
```

```
示例：use hosts = yes
```

### user (S)

`username` 的同义词。

### users (S)

`username` 的同义词。

### username (S)

可以在逗号分隔的列表中指定多个用户，在这种情况下，提供的密码将逐个对用户名进行测试（从左到右）。

`username` 行仅在 PC 无法提供自己的用户名时需要。这用于 COREPLUS 协议或你的用户名与 UNIX 用户名不同的情况。在这两种情况下，你可能也可以使用 `server\user` 语法。

在许多情况下，提供的行并不是一个很好的解决方案，因为 Samba 会尝试逐个对 `username` 行中的用户名验证密码。对于密码重复的用户来说，这很慢且是个坏主意。明智地使用此参数可能会导致超时或安全漏洞。

Samba 依赖于底 UNIX 安全。此参数并不限制谁可以登录，它只是向 Samba 服务器提示哪些用户可能同意提供的密码。守护以登录的用户身份运行，因此他们无法做用户启动 telnet 会话时无法做的事情。

要限制特定的用户组，可以使用 `valid users=` 参数。如果任何用户名以 `@` 开头，则首先在 netgroups 列表中查找该名称（如果 Samba 编译了长期支持功能），随后在 UNIX 组数据库中查找并扩展为该组名的用户列表。

如果任何用户名以 `+` 开头，则该名称仅在 UNIX 组数据库中查找，并展开为该名称组中所有用户的列表。

如果任何用户名以 `&` 开头，则该名称仅在 yp netgroups 数据库中查找（如果 Samba 编译时带有 netgroup 支持），并展开为该名称网络组中所有用户的列表。

请注意，搜索组数据库可能需要一些时间，某些客户端可能会在搜索期间超时。

有关此参数如何决定对服务的访问的更多信息，请参阅 `关于用户名/密码验证的注意事项` 章节。

默认：如果是访客服务则使用访客账户，否则使用服务名称。

示例：

```
username = fred
```

```
username = fred, mary, jack, jane, @users, @pcgroup
```

### username level (G)

此选项允许 Samba 尝试 `猜测` 真实的 UNIX 用户名，因为许多 DOS 客户端发送的是大写用户名。Samba 会尝试小写用户名、以及首字母大写的用户名，如果在该 UNIX 机器上未找到该用户名，则失败。

如果将此参数设置为非零，行为将发生变化。该参数是一个数字，指定了在确定 UNIX 用户名时尝试的大写组合数量。数字越大，尝试的组合越多，发现用户名的速度就越慢。当你的 UNIX 机器上有奇怪的用户名（例如 `AstrangeUser`）时，使用此参数。

默认：`username level = 0`
示例：`username level = 5`

### username map (G)

此选项允许你指定一个包含从客户端到服务器用户名映射的文件。这可以用于多个目的。最常见的是是将在 DOS 或 Windows 机器上使用的用户名映射到 UNIX 机器使用的用户名。多个映射可以映射到单个服务器，以便它们更方便地共享文件。

因此，此选项的使用涉及 UNIX 用户名，而不是 Windows（特别是 NT 域）用户名。换句话说，一旦使用此选项映射了名称，Samba 服务器将为内部和外部目的提供该映射后的名称。

此选项与 `domain map` 参数不同，后者维护 UNIX 用户名和 NT 域之间的一一对应映射：具体来说，Samba 服务器会同时映射两个用户名，将 NT 用户名呈现给外部 NT 世界，并在内部使用 UNIX 用户名。

映射文件按行解析。每行左侧应包含单个 UNIX 用户名，后面跟着 `=`，右侧是用户名列表。右侧用户名列表可能包含 `@group` 形式的名称，以便匹配该组中的任何 UNIX 用户名。特殊客户端 `*` 是通配符，匹配任何名称。映射文件的每行长度最多可达 1023 个字符。

文件每行被处理时，会将提供的用户名与 `=` 右侧的每个用户名进行比较。如果提供的名称匹配右侧的任何名称，则将其替换为左侧的名称。然后继续处理下一行。

如果任何行以 `#` 或 `;` 开头，则将其忽略。

如果任何行以 `!` 开头，则如果该行执行了映射，处理将在该行后停止。否则，映射继续并处理每一行。当文件后面有通配符映射行时，使用 `!` 最有用。

例如，将名称 `admin` 或 `administrator` 映射到 UNIX 名称 `root`，您可以使用：

```
root = admin administrator
```

或将 UNIX 组 `system` 中的任何人映射到 UNIX 名称 `sys`，您可以使用：

```
sys = @system
```

您可以在用户名映射文件中拥有尽可能数量的映射。

如果您的系统支持 NIS NETGROUP 选项，会在检查 `/etc/group` 数据库之前检查网络组数据库。

您可以通过名称周围的双引号来映射带有空格的 Windows 用户名。例如：

```
tridge = "Andrew Tridgell"
```

这将 windows 用户名 `Andrew Tridgell` 映射到 unix 用户名 `tridge`。

以下示例将 `mary` 和 `fred` 映射到 unix 用户 `sys`，并将其余部分映射到 `guest`。注意使用 `!` 告诉 Samba 如果在该行找到匹配项时停止处理。

```
!sys = mary fred
```

```
guest = *
```



请注意，映射适用于所有出现的情况。如果一个目录中仅包含匹配该参数的文件，则该目录连同文件将被删除。设置此参数将影响 Samba 的性能，因为它在扫描时将强制检查所有文件和目录的匹配项。

还有 `hide files` 和 `case sensitive`，

默认：`username map`
示例：`username map = *`

### * *valid chars (S)*
该选项允许您指定应该被考虑的额外字符。这对于国家字符集特别有用。该选项接受字符列表，这是默认值。如果为空，则认为任何字符都是有效的。注意 `case sensitive` 选项适用。

默认：`valid chars`
示例：`valid chars = *`

### * *valid users (S)*
这是一个允许登录的用户列表。以 `+` 和 `&` 开头的名称使用与 `invalid users` 相同的规则进行。如果此列表为空（默认值），任何用户都可以登录。

默认：`valid users` list.（任何人都可以登录）
示例：`valid users = @pcusers`

# 附录 C：Samba 手页

- **volume (S)**

这允许你覆盖为共享返回的卷标签。对于坚持使用特定卷标签的带有安装程序的 CDROM，这非常有用。

默认值是共享名称。

- **wide links (S)**

此参数控制服务器是否可以跟随 UNIX 文件系统中的链接。指向服务器导出目录树内区域的链接始终是允许的；此参数仅控制指向导出目录之外区域的链接。

默认值：`wide links = yes`
示例：`wide links = no`

- **wins proxy (G)**

这是一个布尔值，控制 `nmbd` 是否对来自其他主机半部分的广播名称查询做出响应。对于某些旧版客户端，你可能需要将其设置为 `yes`。

默认值：`wins proxy = no`

- **wins server (G)**

这指定了 `nmbd` 应该注册的 WINS 服务器的 IP 地址（或 DNS 名称：优先使用 IP 地址）。如果你在网络上有一个 WINS 服务器，则应将其设置为 WINS 服务器的 IP 地址。

如果你有多子网网络，你应该将所有客户端都指向 `wins server`。
注意：如果你有多个子网并希望跨子网浏览正常工作，则需要为 Samba 设置 WINS 服务器。

请查看 Samba 发行版中 `docs/` 目录下的文档 `BROWSING.txt`。

默认值：`wins server =`
示例：`wins server = 192.99.200.1`

- **wins support (G)**

此布尔值控制 Samba 中的 `nmbd` 进程是否作为 WINS 服务器运行。除非你有多子网网络并希望特定的 `nmbd` 作为你的 WINS 服务器，否则你不应将其设置为 true。请注意，你**永远不要**在网络中的多台机器上将其设置为 true。

默认值：`wins support = no`

- **workgroup (G)**

此参数控制当客户端查询时显示为哪个工作组服务器。
注意，此参数还控制了与 `security=domain` 设置一起使用的域名称。

默认值：在编译时设置为 `WORKGROUP`
示例：`Teifi workgroup = MYGROUP`

## smb.conf (5)

- **writeable (S)**

对于不会拼写“writeable”的人来说，它的同义词 (:-)。读作“ritter-bull”。

- **write list (S)**

这是一个被赋予服务读写权限的用户列表。如果连接的用户在此列表中，无论`read only`选项如何设置，他们都将获得写入权限。该列表可以使用 `@group` 语法包含组名。

注意，如果用户同时在读取列表（`read list`）和写入列表（`write list`）中，他们将获得访问权限。

另见`read list`选项。

默认值：`write list = <空字符串>`
示例：`write list = admin, root, @staff`

- **write ok (S)**

`writeable` 的同义词。

- **write raw (G)**

此参数控制服务器在从客户端传输数据时是否支持 SMB 的原始写入。你永远不需要更改此参数。

默认值：`write raw = yes`

- **writeable**

其反义同义词是`read only`（只读）。

如果此参数为`no`，则服务用户可能无法服务的目录中创建或修改文件。

注意，可打印服务（`printable = yes`）*始终*允许向目录写入（在用户权限允许的情况下），但仅通过打印程序操作。

默认值：`writeable = no`

示例：
```
read only = no
writeable = yes
write ok = yes
```

## 警告

尽管配置文件允许服务名称包含空格，但你的客户端软件可能不允许。在比较中空格将会被忽略，所以这不应该是一个问题——但请注意这种可能性。

与类似，许多客户端（尤其是 DOS 客户端）将服务名称限制为八个字符。`Smbd` 没有此类限制，但如果从此类客户端截断了服务名称，它将尝试连接。因此，你可能应该将你的服务名称长度保持在八个字符以内。

使用 `[homes]` 和 `[printers]` 特殊部分可以让管理员的工作变得简单，但默认属性的各种组合可能非常复杂。在设计这些部分时要务必小心。特别要确保打印程序目录（spool directories）的权限正确。

## 版本

本页适用于 Samba 套件 2.0 版本。

## 参见

- `smbd (8)`, `smclient (1)`, `nmbd (8)`, `testparm (1)`, `testprns (1)`, `[E] Samba`, `nmblookup (1)`, `smbpasswd (5)`, `smbpasswd (8)`

## 作者

原始 Samba 软件和相关工具由 Andrew Tridell 创建，`samba-bugs@samba.org`。Samba 现在由 Samba Team 作为一个开源项目开发，类似于 Linux 内核开发方式。

原始 Samba 手页由 Karl Auer 编写。手页源代码转换为 YODL 格式（另一项优秀的开源软件，可在 `ftp://ftp.icce.rugl/pub/unix/` 获取），并由 Jeremy Allison 为 Samba 2.0 发布进行了更新。`samba-bugs@samba.org`。

查看 `samba (7)` 以获取贡献者的完整列表以及如何提交错误报告、意见等。

## smclient (1)

## Samba

1998年10月23日

## 名称

`smclient`--一种用于访问服务器上 SMB/CIFS 资源的类 ftp 客户端

## 概览

```
smclient servicename [password] [-s smb.conf] [-B IP addr] [-O socket options][-R name order] [-M NetBIOS name] [-i scope] [-N] [-n NetBIOS] [-d debuglevel] [-P] [-p port] [-l log basename] [-h] [-I IP] [-E] [-U username] [-L NetBIOS [-t terminal command] [-m max protocol] [-W workgroup] [-T <cix>IXFqgbNan] [-R de
```

## 描述

此程序是 Samba 套件的一部分。

`smclient` 是一个可以与 SMB/CIFS 服务器“对话”的客户端。它提供了一个类似于 `ftp (1)` 程序的接口。操作包括从服务器获取文件到本地等内容。

## 选项

- **`servicename`** 是你想要使用的服务的名称。其格式为 `//service/service`，其中一个是 NetBIOS 名称。

- **`B IP address`** 在发送时使用的地址。

- **`O socket options`** 在客户端上设置的套接选项。

- **`R name order`** 此选项允许用户决定使用哪些解析服务。

- **`M NetBIOS name`** 此选项允许你使用“Win-Popup”协议发送消息到另一台计算机。

- **`U username`** 允许你控制发送和接收消息的部分。

- **`I IP`** 用于指定特定的广播地址。

## 描述

此程序是 Samba 套件的一部分。

`smclient` 是一个可以与 SMB/CIFS 服务器“对话”的客户端。它提供了一个类似于 `ftp (1)` 程序的接口。操作包括从服务器获取文件到本地等内容。

## 选项

- **`servicename`** 是你想要使用的服务的名称。其格式为 `//service/service`，其中一个是 NetBIOS 名称。

- **`B IP address`** 在发送时使用的地址。

- **`O socket options`** 在客户端上设置的套接选项。

- **`R name order`** 此选项允许用户决定使用哪些解析服务。

- **`M NetBIOS name`** 此选项允许你使用“Win-Popup”协议发送消息到另一台计算机。

- **`U username`** 允许你控制发送和接收消息的部分。

- **`I IP`** 用于指定特定的广播地址。

# smclient (1)

- `-N` 如果指定，此参数将抑制客户端向用户显示的正常密码提示。这在访问不需要密码的服务时非常有用。

除非在命令行上指定了密码或指定了此参数，否则客户端将要求输入密码。

- `-n NetBIOS` 名称。默认情况下，客户端将使用本地机器的主机名（大写）作为其 NetBIOS 名称。此参数允许你覆盖主机名以及任何你想要的 NetBIOS 名称。

- `-d debuglevel` 调试级别（`debuglevel`）是一个 0 到 10 的整数，或字母 `A`。

如果未指定此参数，默认值为零。
该此值越高，日志文件中记录的关于客户端活动的详细信息就越多。在 0 级，仅记录关键错误和严重警告。1 级是日常运行的合理级别——它会生成少量的执行信息。

1 以上的级别将产生大量的日志数据，应仅在调查问题时使用。3 以上级别专供开发者使用，并会产生巨大的日志数据，其中大部分内容极其晦懂。将打印调试消息。此设置仅供开发者（以及那些真正想知道代码内部如何工作的人）使用。

请注意，指定此参数将覆盖 `smb.conf (5)` 文件中的日志级别参数。

- `-P` 选项不再使用。Samba2.0 中的代码现在用于服务器设备类型，因此不需要特定的打印机标志。

- `-p port` 端口。连接到服务器时使用的 TCP 端口号。SMB/CIFS 服务器的标准（已知）TCP 端口号为 139，这是默认值。

- `-l logfilename` 日志文件名。如果指定，`logfilename` 指定一个基文件名，运行客户端的操作数据将记录在该文件中。

默认的基名称在编译时指定。
基名称用于生成日志文件文件名。例如，如果指定的名称为`log`，则调试文件将为 `log.client`。
生成的日志文件永远不会被客户端删除。

- `-h` 打印客户端的用法信息。

- `-I IP` 地址是要要连接的服务器地址。它应以标准的`a.b.c.d`格式指定。

通常，客户端会尝试通过上文 `name resolve order` 参数描述的 NetBIOS 名称解析机制来查找命名的 SMB/CIFS 服务器。使用此参数将强制客户端假设服务器位于指定 IP 地址的机器上，并且所连接的资源的 NetBIOS 名称部分将被忽略。

# 320 附录 C：Samba 手页

此参数没有默认值。如果不提供，将如上所述由客户端自动确定。

- `-E` 此参数导致客户端将消息写入标准错误流 (`stderr`) 而不是标准输出。

默认情况下，客户端将消息写入标准输出——通常是用户的 tty。

- `-U username` 用户名。指定客户端用于建立连接的用户名，假设你的服务器不是运行在共享使用密码协议水平的低级服务器（downlevel server），且某些人坚持它必须是有效的 NetBIOS 名称。

某些服务器对此名称的大小写很敏感，某些则坚持它必须是有效的 NetBIOS 名称。

如果没有提供用户名，它将按顺序默认为环境变量 `USER` 或 `LOGNAME` 的大写版本。如果未提供用户名且这两个环境变量都不存在，则将使用变量 `GUEST`。

如果 `USER` 环境变量包含 `%`，则该符号之后的所有内容都将被视为密码。这允许你将环境变量设置为 `USER%password`，这样密码就不会通过命令行传递（命令行可能会被 `ps` 命令看到）。

如果你要连接的服务需要密码：

在命令行上：

`-U fred%secret`

请注意，百分号周围没有空格。

如果你将密码作为用户名的一部分指定，则会提示 `-N` 选项（抑制密码）。

如果你将密码作为用户名的一部分指定，那么密码将作为用户名的一部分。百分号之前或之后的任何内容将分别创建一个空环境或空密码。

也可以通过设置一个名为 `PASSWORD` 的包含用户密码的环境变量来指定密码。注意这在某些系统上可能是不安全的，但在其他系统上，它允许用户编写 `smclient` 命令脚本，而无需在进程列表命令行中包含密码。

某些服务器（包括 OS/2 和用于工作组的 Windows）坚持使用大写密码。小写或混合大小写的密码可能会被这些服务器拒绝。

在脚本或 `PASSWORD` 环境变量中包含密码时要小心。此外，在许多系统中，运行进程的命令行可以通过 `ps` 命令看到，因此务始终让 `smclient` 直接输入密码和所需内容。

- `-L smclient -L host` 允许你查看服务器上可用的服务。你像 `host` 使用它，就会出现一个列表。如果你的 NetBIOS 名称与你的 tcp/ip dns 名称不匹配，或者你正在尝试访问另一个网络上的主机，`-I` 选项可能会有用。

`smclient (1)`

- **terminal code** 此选项告诉 `smclient` 如何解释来自远程服务器的文件名。通常，亚洲语言多字节的 UNIX 实现使用的字符集与 SMB/CIFS 服务器不同（例如使用 EUC 而不是 SJS）。设置此参数将允许 `smclient` 正确在 UNIX 文件名和 SMB 文件名之间进行转换。此选项未经过严格测试，可能会有些问题。

终端代码包括 `sjis`, `euc`, `jis7`, `jis8`, `junet`, `hex`, `cap`。这不是一个完整列表，请检查 Samba 源获取完整列表。

- **m protocol level** 协议级别。有了 Samba2.0 的新代码，`smclient` 始终尝试连接最高协议服务器。此参数是为了向下兼容，但 `m` 之后的任何字符串将被忽略。

- **WORKGROUP** 为此连接覆盖 `smb.conf` 文件中指定的默认工作组。某些服务器可能需要这样做。

- **Tar options** `Tar` 选项可用于创建 SMB/CIFS 服务器上所有文件的 `tar (i)` 兼容备份。传递给此选项的辅助 tar 标志有：

- `c` 在 UNIX 上创建 tar 文件。后面必须跟 tar 文件的文件名、磁带设备或 `"-"`（表示标准输出）。如果使用标准输出，必须将日志级别调至最低值 `-d0` 以避免损坏你的 tar 文件。这与 `x` 标志互斥。

- `x`（恢复）将本地 tar 文件恢复到共享中。除非给出 `-D`，否则 tar 文件将从共享的顶层恢复。后面必须跟 tar 文件的文件名、设备或 `"-"`（表示标准输入）。这与 `c` 标志互斥。恢复的文件其修改时间 (`mtime`) 将设置为 c 文件中保存的日期。目前目录无法正确获取其日期。

- `I` 包含文件和目录。这是指定上述文件名时的默认行为。导致提取或创建时包含文件（并排除所有其他内容）。参见下文。文件名通配符有两种工作方式。参见 `r`。

- `X` 排除文件和目录。导致 tar 文件的提取或创建。参见下文。文件名通配符有两种工作方式。参见下文 `r`。

- `b` 块大小。后面必须跟一个值（大于0）块大小。导致 tar 文件以块大小*TBLOCK（通常为 512 字节）写入。

- `g` 增量。仅备份设置了归档位的文件。仅配合 `c` 标志使用。

- `q` 静默。保持 tar 不打印诊断信息。这等同于 tarmode quiet。

正则表达式或排除操作可能非常慢。如果编译时没有定义 `HAVE_REGEX_H`，则仅对 `*` 和 `?` 进行有限通配符匹配。

# 附录 C：Samba 手页

- `-N` 新于。后面必须跟一个文件名，该文件的日期将在创建时与共享目录中找到的文件进行比较。只有比指定文件更新的文件会被备份到 tar 文件中。仅配合 `c` 标志有效。
- `-a` 设置归档位。计算在备份文件时需要重置的归档位。配合 `g` 和 `c` 标志使用。

## Tar 长文件名

`smclient` 的 `tar` 选项现在在备份和恢复时都支持文件名。然而，文件的完整路径名必须小于 1024 字节。此外，在创建 tar 归包时，`smclient` 的 `tar` 选项以相对名称将所有文件放入存档，而不是绝对名称。

## Tar 文件名

文件名都可以以 DOS 路径名（使用 `\` 作为组件分隔符）或 UNIX 路径名（使用 `/` 作为组件分隔符）给出。

## 示例

- 从 tar 文件 `backup.tar` 恢复到 `mypc` 上的 `myshare`（`mypc` 无需密码）
```



`smclient //mypc/myshare "" -N -Tx backup.tar`

```
- 恢复 users/docs 以外的所有内容
```

`smclient //mypc/myshare "" -N -Txx backup.tar users/docs`

```
- 为 users/docs 下的文件创建 tar 文件。
```

`smclient //mypc/myshare "" -N -Tc backup.tar users/docs`

```
- 创建与上述相同的 tar 文件，但这次使用 DOS 路径名。
```

`smclient //mypc/myshare "" -N -tc backup.tar users\edocs`

```
- 创建共享目录下所有文件和目录的 tar 文件。
```

`smclient //mypc/myshare "" -N -Tc backup.tar *`

```
- -D 初始目录 在开始前切换到初始目录。可能仅配合 `tar -T` 选项有用。
- -c 命令字符串是一个由分号分隔的命令列表，用于执行命令而不是提示标准输入（stdin）。`-N` 被 `-c` 隐含。

这在脚本以及将标准输入打印到服务器上时特别有用，例如 `-c 'print ' '-'`

## 操作

一旦客户端运行，用户将看到一个提示符：

```
smb: \\
```

提示符表示客户端已就绪并等待执行用户命令。每个命令都是单个单词，可选地带有参数以指定该命令。除非这些注释另有说明，否则命令和参数之间用空格分隔。所有命令均不区分大小写。命令参数可能敏感也可能不敏感，取决于具体命令。

你可以通过用双引号括起名称来指定包含空格的文件名，例如 `"a long file name"`。

显示在方括号中的参数（例如 `[parameter]` `）是可选的。如果不提供，命令将使用合适的默认值。显示在角括号中的参数（例如 `<parameter>`）是必填的。

请注意，所有在服务器上操作的命令实际上都是通过向服务器发送请求完成的。这种行为可能因服务器而异，取决于服务器的实现方式。

## 可用命令按字母顺序列出如下：

（注：此处命令列表翻译遵循了格式要求）

- * `[command]` 如果指定了 "`command`"，`?` 命令将显示关于指定命令的简要信息消息。如果未指定命令，将显示可用命令列表。
- `!` `[shell command]` 如果指定了 "`shell command`"，`!` 命令将在本地执行 shell 并运行指定的 shell 命令。如果未指定命令，将运行本地 shell。
- `cd` `[directory name]` 如果指定了 "`directory name`"，服务器上的当前工作目录将更改为指定的目录。由于任何原因导致指定的目录无法访问，此操作将失败。
- `del` `<mask>` 客户端将请求服务器尝试删除当前工作目录中匹配 "`mask`" 的所有文件。
- `dir` `<mask>` 将从服务器检索并显示服务器当前工作目录中匹配 "`mask`" 的文件列表。
- `exit` 退出程序。
- `get` `<remote file>` `[local file]` 将服务器上的 `<remote file>` 复制到 `[local file]`。
- `help` `[command]` 查看 `?` 命令。
- `lcd` `[directory name]` 如果指定了 "`directory name`"，服务器上的当前工作目录将更改为指定的目录。
- `ls` `<mask>` 查看 `dir` 命令。
- `mask` `<mask>` 允许在 `get` 和 `put` 命令中使用掩码过滤器。
- `lowercase` 切换文件名是否转换为小写。
- `md` `<mask>` 归档归档位。计算在备份文件时重置归档位。
- `md` `<mask>` 查看 `ls` 命令。
- `mkdir` `<directory name>` 在服务器上创建一个新目录。
- `mget` `<mask>` 从服务器复制匹配 "`mask`" 的所有文件到本地机器。
- `mput` `<local file>` `[remote file]` 将本地机器上的 `<local file>` 推送到服务器。
- `print` `<file>` 从服务器打印指定的 `<file>`。
- `printmode` `<binary or text>` 将打印模式设置为二进制或文本。
- `prompt` 切换在 `get` 和 `put` 命令执行期间的提示。
- `queue` 显示队列，显示作业 ID、名称和当前状态。
- `quit` 查看 `exit` 命令。
- `rd` `<directory>` 查看 `rmdir` 命令。
- `recurse` 切换目录递归。这些命令将处理所有目录（即它们正在复制的目录），并进入任何匹配指定掩码的目录。
- `rm` `<mask>` 删除服务器当前工作目录中所有匹配 `mask` 的文件。
- `rmdir` `<directory>` 在权限允许的情况下从服务器上删除指定的目录。
- `tar` `<cx>[IXBag]` 执行 tar 操作——见上面的 `-T` 命令。使用 `g`（增量）可能会受到 `tarmode` 命令的影响。使用 `N`（新于）将影响 tar 设置。注意，tar 的 `-x` 选项可能无效——请改用命令行。
- `blocksize` `<blocksize>` 块大小。后面必须跟一个有效的（大于零的）块大小。导致文件以 `blocksize*TBLOCK`（通常为 512 字节）为块写入。
- `tarmode` `<inlinereset>` 更改 tar 关于归档位的行为。在完整模式下，tar 将备份除归档设置以外的所有内容（这是默认模式）。在增量模式下，tar 将备份具有归档位的文件。

# 326
# 附录 C：Samba 手页

位设置。在重置模式下，tar 将重置其所备份的所有文件的归档位（这暗示意味着读/写共享）。

- `setmode` `<filename>` `<perm=[+\-rsha->]` DOS 属性命令的一个版本，用于设置文件权限。例如：

```
setmode myfile +r
```



将使 `myfile` 变为只读。

# 注意事项

某些服务器对提供的用户名、密码、共享名称（又称服务名称）和机器名称的大小写非常敏感。如果连接失败，请尝试将所有参数都大大写。

连接到某些类型的服务器时，通常需要使用 `-n` 选项。例如，OS/2 LanManager 强制要求使用有效的 NetBIOS 名称，因此你需要提供一个服务器能够识别的有效名称。

- 当服务器支持 LANMAN2 协议或更高版本时，`smclient` 支持文件名。

# 环境变量

变量 `USER` 可能包含使用客户端的用户的用户名。只有当协议级足够高以支持会话级密码时，才会使用此信息。

变量 `PASSWORD` 可能包含使用客户端的用户的密码。只有当协议级足够高以支持会话级密码时，才会使用此信息。

# 安装

客户端程序的位置由各个系统管理员决定。因此，以下仅供建议。

建议将 `smclient` 软件安装在 `/usr/local/samba/bin` 或 `/usr/samba/bin` 目录，该目录对所有人可读，仅对 `root` 可写。客户端本身应对所有人可执行。客户端不应被设置为 `setuid` 或 `gesetzt`！

客户端日志文件应放在一个可读的目录，并仅对用户可写。

要测试客户端，你需要知道正在运行的 SMB/CIFS 服务器的名称。可以使用普通用户运行 `smbd` (8)——将其作为守护进程运行在具有用户权限的端口（通常是 1024 以上的任何端口号）上，将提供一个合适的的测试服务器。

# 诊断

客户端产生的大多数问题都会记录在指定的日志文件中。日志文件名在编译时指定，但可以在命令行进行覆盖。

# smbd (8)

327
可用的诊断数量和性质取决于客户端使用的调试级别。如果你遇到问题，请将调试级别设置为 3 并仔细查阅日志文件。

# 版本

此手页适用于 Samba 套件的 2.0 版本。

# 作者

原始 Samba 及相关工具由 Andrew Tridell 创建（`samba-bugs@samba.org`）。Samba 现在由 Samba 团队作为一个开源项目开发，类似于 Linux 内核的方式。

原始的 Samba 手页由 Karl Auer 编写。手页源码转换为 YODL 格式（另一项优秀的开源软件，可在 `ftp://ftp.icce.rug/pub/unix/` 获取），并由 Jeremy Allison (`samba-bugs@samba.org`) 为 Samba 2.0 发布进行了更新。

请查看 `samba` (7) 以获取贡献者的完整列表以及关于提交错误报告、注释等的详细信息。

# smbd (8)

# Samba

1998年10月23日

# 名称

# smbd—向客户端提供 SMB/CIFS 服务的服务器

# 概要

`smbd [-D] [-a] [-o] [-d debuglevel] [-l log file] [-p port number] [-O socket options] [-s configuration file] [-i scope] [-P] [-h]`

# 描述

此程序用于 Samba 套件。

`smbd` 是一个服务器守护进程，使用 SMB（或 CIFS）协议为 Windows 客户端提供文件共享和打印服务。服务器为客户端提供文件空间和打印服务。这与 LanManager 协议兼容，并可以为 Lan-Manager 客户端服务。这些包括 DOS 的 MSCLIENT 3.0、工作组版 Windows 95、Windows NT、OS2、Macintosh 的 DAVE 以及 Linux 的 `smbfs`。

# 328
# 附录 C：Samba 手页

服务器可以提供的服务的详细描述在控制这些服务属性的配置文件手页中（参见 `smb.conf` (5)）。本页将不描述服务，而是侧重于运行服务器的管理方面。

请注意，运行此服务器具有重的安全影响，在继续安装之前，应将 `smb.conf` (5) 视为必读内容。

每当客户端请求时，就会创建一个会话。每个客户端每个会话获得一个服务器副本。该副本随后处理客户端在该会话期间建立的所有连接。当客户端的所有连接都关闭时，该服务器副本也将终止。

配置文件及其包含的任何文件如果发生变化，将每分钟自动重新加载。你可以通过向服务器发送 `SIGUP` 来强制重新加载。重新加载配置文件不会影响任何已建立的服务的连接。要么用户将断开服务，要么 `smbd` 被杀死并重启。

# 选项

- `-D` 自身，此参数使服务器作为守护进程运行。 也就是说，它会分离并在后台运行，在相应的端口上处理请求。对于提供比通常的文件和打印服务的服务器，以守护进程运行 `smbd` 是推荐的方法。

默认情况下，服务器不会作为守护进程运行。

- 如果指定此参数，每个新连接都将日志消息追加到日志文件中。 这是默认设置。

- 如果指定此参数，日志将在打开时被覆盖。 默认情况下，日志文件将被追加。

- `debuglevel` 调试级别是一个 0 到 10 的整数。

如果未指定此参数，默认值为零。

值越高，记录的服务器活动细节就越详细。在级别 0，仅记录关键错误和严重警告。级别 1 是一个合理的级别，会记录有关操作的少量信息。1以上的级别将产生大量的日志数据，仅供开发人员调试使用。请注意，指定此参数将覆盖 `smb.conf` (5) 文件中的 `log level` 参数。

- `log file` 日志文件 如果指定，此参数指定一个记录运行服务器的信息和调试消息的日志文件。生成的日志文件大小由 `smb.conf` (5) 文件中的 `max size` 控制。默认日志文件名在编译时指定。

# smbd (8)

329
- `O` `socket options` 套接字选项 详情参见 `smb.conf` (5) 中的 `socket` 参数。
- `p` `port number` 端口号是一个正整数。 如果未指定此参数，默认值为139。

该数字是从软件连接服务器时使用的端口号。SMB over TCP 标准（已知）端口为139，因此作为默认。如果你希望以普通用户而不是 `root` 运行服务器，你需要一个大于1024的端口——在这种情况下请寻求系统管理员的帮助。为了让服务器对大多数客户端有用，你应该将其配置在除139以外的端口上，你需要端口重定向服务，其详情见 `rfc1002.txt` 第 4.3.5 节。

通常不指定此参数。

- `s` `configuration file` 配置文件 指定的文件包含服务器所需的配置详细信息。此文件中的信息包括服务器特定信息，如使用什么打印文件，以及服务器要使用的所有服务的描述，更多信息参见 `smb.conf` (5)。默认配置文件名在编译时确定。
- `i` `scope` 范围 指定服务器用于与生成 NetBIOS 名称通信的 NetBIOS 范围。关于使用 NetBIOS 范围的详情参见 `rfc1001.txt` 和 `rfc1002.txt`。NetBIOS 范围极少使用，只有当你是你使用的所有 NetBIOS 系统的管理员时才设置此参数。
- `h` 打印 `smbd` 的帮助信息（用法）。
- `P` 被动选项。导致 `smbd` 不向外任何网络流量。仅供开发人员调试。

# 文件

# `/etc/inetd.conf`

如果服务器要由 `inetd` 元守护进程运行，此文件必须包含适用于元数据的启动信息。参见下文的安装部分。

# `/etc/rc`

（或你系统使用的任何初始化脚本）。

如果要在启动时作为守护进程运行服务器，此文件将需要包含适当的服务器启动序列。参见下文的安装部分。

## `/etc/services`

如果通过元守护进程 `inetd` 运行服务器，此文件必须包含服务名称（例如 `netbios-ssn`）到服务端口（例如 139）和协议类型（例如 `tcp`）的映射。请参阅下文的安装（安装）部分。

## `/usr/local/samba/lib/smb.conf`

这是 `smb.conf` 服务器配置文件的默认位置。系统安装此文件的其他常见位置还有 `/usr/samba/lib/smb.conf` 和 `/etc/smb.conf`。

此文件描述了服务器将向客户端提供的所有服务。更多信息请参阅 `smb.conf` (5)。

## 局限性

在某些系统上，`smbd` 在调用 `setuid()` 之后无法将 `uid` 改回 `root`。此类系统被称为“陷门（trapdoor）”`uid` 系统。如果你拥有这样的系统，你将无法以两个不同的用户身份同时从客户端（如 PC）连接。尝试连接第二个用户将导致“拒绝访问”或类似的错误。

## 环境变量

### 打印机

如果没有为可打印服务指定打印机名称，大多数系统将使用此变量的值（如果该变量未定义，则使用 "`lp`"）作为使用的打印机名称。然而，这并非特定于服务器。

## 安装

服务器及其支持文件的位置由个人系统管理员决定。以下仅供建议。

建议将服务器软件安装在 `/usr/local/samba` 层次结构下，该目录对所有用户可读，仅对 `root` 可写。服务器程序本身应允许所有用户执行，因为用户可能希望自己运行服务器（当然，如果它以他们的权限运行的话）。服务器**不应**设置 `setuid`。在某些系统上，将 `smbd` 设置 `setgid` 为空组可能是值得的。这是因为某些系统可能存在安全漏洞，用户可以附加到守护进程进程的调试器上。将 `smbd` 文件设置 `setgid` 为空组可能会防止该漏洞被利用。该安全漏洞和建议的修复方法在编写本文时，仅在 Linux 的旧版本（内核 2.0 之前的版本）中得到确认。该漏洞可能仅存在于 Linux，因为目前对其他系统的测试显示它们对此是免疫的。

## smbd (8)

服务器日志文件应放在仅供 `root` 可读和可写的目录中，因为日志文件可能包含敏感信息。

配置文件应存放在仅供 `root` 可读和可写的目录中，因为配置文件控制着服务器提供的服务的安全性。如果需要，可以将配置文件设为所有用户可读，但这对于修正服务器并非必要，而且不建议这样做。服务器源码提供了一个示例配置文件 "`smbd.conf.sample`"—你可以将其重命名为 "`smbd.conf`" 并根据你的单元进行修改。

其余的节点将假设以下情况：

- `smbd`（服务器程序）安装在 `/usr/local/samba/bin`
- `smbd.conf`（配置文件）安装在 `/usr/local/samba/lib`
- 日志文件存储在 `/var/adm/smblogs`

服务器可以作为用户的守护进程运行，也可以在启动时运行，或者根据请求从元守护进程（如 `inet`）运行。如果作为守护进程运行，服务器将始终就绪，因此会话会更快。如果从元守护进程运行，将节省一些内存，并可以使用 `tcpd` TCP-wrapper 等工具进行额外的安全。作为服务器文件使用时建议 `smbd` 以守护进程运行。

当你决定后，请继续“以守护进程运行服务器”或“按请求运行服务器”。

## 以守护进程运行服务器

要从命令行以守护进程运行服务器，只需在命令行上加上 `-D` 选项即可。不需要在命令行末尾添加安符（&）——因为 `-D` 选项会导致服务器本身从 tty 中脱离。

任何用户都可以以守护进程运行服务器（当然是在允许执行权限的情况下）。这对于测试目的非常有用，甚至可以作为 `ftp` 等工具的临时替代品。以这种方式运行时，服务器将仅具有运行它的用户的权限。

为了确保服务器在每次机器启动时都以守护进程运行，并确保它以 `root` 身份运行以便为多个客户端提供服务，你需要修改系统启动文件。在适当的地方（例如在 `/etc/rc` 中），插入以下行，并根据需要替换端口号、文件位置、配置文件位置和调试级别：

```



`/usr/local/samba/bin/smbd`
`-D -l /var/adm/smblogs/log -s`
`/usr/local/samba/lib/smbd.conf`

```
（上述内容应在你的初始化脚本中以单行形式出现。根据你的终端特性，它在该帮助页中可能不是这样显示的。如果上述内容显示为多行，请将任何换行或缩进视为单个空格或 TAB 字符。）
```

如果编译时使用的选项适用于你的系统，则除 `-D` 之外的所有参数都可以省略。请参阅上文的 OPTIONS 部分。

## 按请求运行服务器

如果你的系统使用如 `inet` 等元守护进程，你可以安排在进程尝试连接到它时启动 `smbd` 服务器。这需要对主机上的启动文件进行几处更改。如果你是以普通用户而非 `root` 身份进行实验，你需要系统管理员协助修改。

## 测试安装

如果以守护进程运行服务器，请在继续之前执行。如果使用元守护进程，请重启系统或重启元守护进程。某些版本的 `inetd` 如果接收到 HUP 信号会重新读取配置表。

如果你的名字是 "fred"，对方是 "mary"，你现在应该能够连接到。为了正确测试和实验服务器，我们建议使用 `smbclient` 程序（参见 `smbclient (I)`）并遵循 `docs/` 目录下 `DIAG.txt` 文件概述的步骤。

## 版本

本帮助页对于 Samba 套件 2.0 版本是正确的。

## 诊断

服务器发布的大多数诊断信息记录在指定的日志文件中。日志文件名在编译时指定，但可以在命令行上覆盖。

可用诊断信息的数量和性质取决于服务器使用的调试级别。如果你遇到问题，将调试级别设置为 3 并查阅日志文件。

大多数信息都是相当自显明的。遗憾的是，在创建本帮助页时，源码中提供的诊断信息太多，不值得描述每一个。在此阶段，最好的办法是 `grep` 源码并索引导致你看到的诊断信息的条件。

## 信号

向 `smbd` 发送 `SIGHUP` 信号将导致它在短时间内重新加载其 `smb.conf` 配置文件。

关闭 `smbd` 进程时，建议**不要**最后最后使用 `SIGKILL (-9)`，因为可能会导致内存区域处于不一致状态。终止 `smbd` 的安全方法是发送 `SIGTERM (-15)` 信号并等待它自行关闭。

通过向 `smbd` 发送 `SIGUSR1 (kill <smbd-pid>)` 可以提高其调试级别，通过向其发送 `SIGUSR2 (kill -USR2 <smbd-pid>)` 可以降低。这允许对瞬时性问题进行调试，同时保持以正常的低调试级别运行。

## 另参见

`hosts_access (5)`, `inet (8)`, `nmbd (8)`, `smb.conf (5)`, `smclient (1)`, `testparam (1)`, `prns (1)` 以及 Internet RFC 的 `rfc1001.txt`, `rfc1002.txt`。此外，CIFS（原为 SMB）规范可以通过网页链接访问：`http://samba.org/cifs/`

## 作者

原始的 Samba 软件及相关工具由 Andrew Tridell（`samba-bugs@samba.org`）创建。现在，Samba 由 Samba 团队作为一个开源项目进行开发，类似于 Linux 内核的开发方式。

原始的 Samba 帮助页由 Karl Auer 编写。帮助页源代码转换为 YODL 格式（另一项优秀的开源软件，可在 `ftp://ftp.icce.rug.nl/pub/unix/` 获取），并由 Jeremy Allison（`samba-bugs@samba.org`）更新至 Samba 2.0 版本。

请参阅 `samba (7)` 以了解获取贡献者完整列表以及提交错误报告、意见等的详细信息。

## `smbpasswd (5)`

## Samba

# 1998年10月23日

## 名称

`smbpasswd`—Samba 加密密码文件

## 概要

`smbpasswd` 是 Samba 加密密码文件。

## 描述

此文件是 Samba 套件的一部分。

`smbpasswd` 是 Samba 加密密码文件。它包含了用户名、Unix 用户 ID 以及用户的 SMB 哈希密码，账户标志信息以及最后修改密码的时间。该文件格式随着 Samba 的发展而演进，过去曾有多种格式。

## 文件格式

Samba 2.0 使用的 `smbpasswd` 文件格式与熟悉的 Unix `passwd (5)` 文件非常相似。它是一个 ASCII 文件，每个用户占一行。每行中的每个字段之间用冒号分隔。任何以 `#` 开头的条目都会被忽略。

`smbpasswd` 文件包含每个用户的以下信息：

- `name`（用户名）：这是用户名。它必须是标准 UNIX `passwd` 文件中已存在的名称。
- `uid`：这是 UNIX `uid`。它必须与标准 UNIX `passwd` 文件中相同用户条目的 `uid` 匹配。如果不匹配，Samba 将拒绝将该 `smbpasswd` 条目识别为有效用户。
- Lanman Password Hash（Lanman 密码哈希）：这是用户密码的 LANMAN 哈希，编码为 32 位十六进制数字。LANMAN 哈希是通过使用密码作为密钥对已知字符串进行 DES 加密生成的。这与 Windows 95/98 机器使用的密码相同。注意，此密码哈希被认为是弱的，因为它容易受到字典攻击的影响，且如果两个用户选择了相同的密码，该条目将完全相同（即密码没有经过“加盐”，就像 UNIX 密码那样）。如果用户拥有空密码，该字段将包含字符“NO PASSWORD”作为十六进制字符串的开头。如果十六进制字符串等于 32 个 `*X` 字符，则账户被标记为禁用，用户将无法登录 Samba 服务器。

**警告 !!** 注意，由于 SMB/CIFS 身份验证协议的挑战-响应机制，任何知道此密码哈希的人都能在网络上冒充该用户。由于此原因，这些哈希被称为“明文等效值”，绝不能提供给 root 用户。为了保护这些哈希，`smbpasswd` 文件被放置在仅允许 root 用户读取和遍历权限的目录中，不提供其他访问权限。

- NT Password Hash（NT 密码哈希）：这是用户密码的 Windows 哈希，编码为 32 位十六进制数字。Windows NT 哈希是通过取以 16 位小端序 UNIC 形式表示的用户密码，然后对其应用 MD4（internet `rfc1321`）算法生成的。

此密码哈希比 Lanman 密码哈希的情况更安全，因为它保留了密码的大小写，并使用了质量更高的哈希算法。然而，如果两个用户选择了相同的密码，该条目仍然是相同的（即密码没有加盐）。

**警告 !!** 注意，由于 SMB/CIFS 身份验证协议的挑战-响应机制，任何知道此密码哈希的人都能在网络上冒充该用户。由于此原因，这些哈希被称为“明文等效值”，绝不能提供给 root 用户。为了保护这些哈希，`smbpasswd` 文件被放置在仅允许 root 用户读取和遍历权限的目录中，且 `smbpasswd` 文件必须设为仅限 root 读/写，不提供其他访问权限。

- Account Flags（账户标志）：此部分包含描述用户账户属性的标志。在 Samba 2.0 版本中，该字段被 '[' 和 ' ]' 字符包围，长度始终为 13 个字符（包括 '[' 和 ']'）。该该字段的内容可以是任何字符。
'U' 表示这是一个“用户（User)”账户，即普通用户。目前 `smbpasswd` 文件仅支持用户和工作站账户。
'N' 表示该账户没有密码（Lanman 密码哈希和 NT 密码哈希中的密码将被忽略）。注意，只有当 `smb.conf (5)` 配置文件设置了空密码参数时，才允许用户无密码登录。
'D' 表示此账户已禁用，将不允许该用户进行任何 SMB/CIFS 登录。
'W' 表示此账户是“工作站信任（Workstation Trust）”账户。此类账户用于 Samba PDC 代码流，以允许 Windows 工作站服务器加入由 Samba PDC 托管的域。

随着未来代码的扩展可能会添加其他标志。该字段剩余的空间用空格填充。

- Last Change Time（最后更改时间）：此字段由账户最后修改的时间组成。它由字符 LCT（代表“Last Change Time”）组成，随后是自从纪元（1970年）以来最后一次更改的秒数 UNIX 时间数值编码。
- Following fields（后续字段）：此时忽略所有其他冒号字段。

## 注意

在 Samba 的之前的版本（特别是 1.9.18 系列）中，此文件不包含账户标志或最后更改时间字段。Samba 2.0 可以读取和写入旧的密码文件，但无法修改条目以添加新字段。然而，使用 `smbpasswd (8)` 添加的条目中的新增账户将包含新字段。因此，在 Samba 2.0 中使用的旧 `smbpasswd` 文件可能导致某些账户包含新字段而另一些没有。

为了将旧式的 `smbpasswd` 文件转换为新样式，可以使用 `convert-smbpasswd` 脚本。该脚本安装在 Samba 的 `bin/` 目录（与 `smbd` 和 `nmbbd` 相同的地方），用法如下：

```
cat old_smbpasswd_file | convert_smbpasswd > new_smbpasswd_file
```



# `convert-smbpasswd`

`convert-smbpasswd` 脚本从标准输入读取并输出到标准输出，以免意外覆盖文件。

运行此脚本后，检查新 `smbpasswd` 文件的内容，确保其没有被转换脚本（使用 `awk`）损坏，然后用 `<新 smbpasswd 文件>` 替换 `<旧 smbpasswd 文件>`。

## 版本

此帮助页适用于 Samba 套件的 2.0 版本。

## `smbpasswd` (8)

此选项仅在以 `root` 运行 `smbpasswd` 时可用。

- `-e` 此选项指定了如果账户之前被禁用，则应在本地 `smbpasswd` 文件中启用其后的用户名后的空间（即启用该账户）。如果账户未被禁用，则此选项将不起作用。一旦账户被启用，用户将能够再次对 SMB 进行身份验证。

如果 `smbpasswd` 文件采用“旧”格式，则 `smbpasswd` 将提示该用户输入密码，否则将通过删除 `smbpasswd` 文件中账户空间中的 'D' 标志来启用账户。有关“旧”和“新”密码格式的详情，请参阅 `smbpasswd` (5)。

此选项仅在以 `root` 运行 `smbpasswd` 时可用。

- `-debuglevel` `debuglevel` 是一个 0 到 10 的整数。如果此参数不为 0，则默认值为 0。

值越高，日志文件中记录的关于 `smbpasswd` 活动的详细信息就越多。在级别 0 下，仅将记录关键错误和严重警告。

1 以上的级别会产生大量的日志数据，应仅在调查问题时使用。3 以上的级别专供开发人员使用，并产生海量的日志数据，其中大部分完全是晦懂的。

- `-n` 此选项指定了其后的用户名在本地 `smbpasswd` 文件中的密码应设置为空（即空密码）。这是通过在 `smbpasswd` 文件中存储的第一个密码的第一部分写入字符串 `"NO PASSWORD"` 来的。

注意，要允许用户登录到密码在 `smbpasswd` 文件中设置为 `"NO PASSWORD"` 的 Samba 服务器，管理员必须在 `smb.conf` 文件的 `[global]` 节中设置以下参数：

```
null passwords = true
```



此选项仅在以 root 运行 `smbpasswd` 时可用。

- `-r` remote machine 允许用户更改密码的远程机器。如果没有此参数，`smbpasswd` 默认指向本地主机（`localhost`）。“远程机器名称”是尝试更改密码的 SMB/CIFS 服务器的 NetBIOS 名称。该名称将使用 Samba 套件中所有程序中的标准名称解析机制解析为 IP 地址。有关更改此解析顺序的详情，请参阅 `-R name resolve order` 参数。

更改密码的用户名是当前登录 UNIX 的用户。有关更改不同用户名密码的详情，请参阅 `-U username` 参数。

注意，如果加入 Windows NT 域，指定的远程名称必须是该域的主域控制器（备用域控制器仅拥有用户账户数据库的只读副本，将不允许更改密码）。

注意 Windows 95/98 没有真正的密码数据库，因此无法通过指定 Win95/98 机器作为远程目标来更改密码。

- `R name resolve order` 此选项允许 `smclient` 用户决定在查找正在连接的主机的 NetBIOS 名称时使用哪些名称解析服务。

选项有 "`hosts`”、“`host`”、“`wins`” 和 "`bcast`”。它们导致名称按以下方式进行解析：

- `hosts`: 在 Samba `hosts` 文件中查找 IP 地址。
- `host`: 执行标准的主机到 IP 地址的解析，使用系统的 `/etc/hosts`、NIS 或 DNS 查找。这种名称解析方法取决于操作系统系统。例如，在 IRIX 或 Solaris 上，这可能通过 `/etc/nwitch.conf` 文件进行控制。
- `wins`: 查询 `smb.conf` 文件中 `wins server` 参数中列出的 IP 地址。如果不在 `smb.conf` 文件的 `interfaces` 参数中找到 NIS 服务器。这是所有名称解析方法中最不可靠的，因为它取决于目标主机位于本地连接的子网上。

如果未设置此参数，则将使用 `smb.conf` 文件参数 `name resolve order` 中定义的解析顺序。
默认顺序是 `hosts`、`wins`、`bcast`，在 `smb.conf` 文件中没有任何条目的情况下，将按此顺序尝试名称解析方法。

- `m` 此选项告诉 `smbpasswd` 正在更改的账户是一个机器账户（MACHINE account）。目前这用于 Samba 被用作 NT 主域控制器时。PDC 支持在 Samba2.0 中不是支持的功能，但将在后续版本中获得支持。如果你想了解更多关于将 Samba 作为 NT DC 的信息，请订阅 `samba-ndom@samba.org` 邮件列表。

此选项仅在以 root 运行 `smbpasswd` 时可用。

- `-j DOM` 此选项用于将 Samba 服务器加入 Windows NT 域，作为域成员能够像 Windows NT 服务器一样对同一域内的域控制器进行用户身份验证。请参阅 `smb.conf (5)` 手页中的 `security=domain` 选项。

为了使用此项，Windows NT 域的管理员必须使用“Server Manager for Domains”程序将 Samba 服务器的主 NetBIOS 名称作为域成员添加。

完成后，通过使用此参数调用 `smbpasswd` 加入域。`smbpasswd` 将查找该域的主控制器（在 `smb.conf` 文件的 `password server` 参数中找到），并更改用于创建安全域通信的账户密码。此密码由 `smbpasswd` 存储在文件中，仅限 root，格式为 `<Domain>.<Machine>.mac`，其中 `<Domain>` 是我们加入的域名，`<Machine>` 是我们正在运行的机器的主 NetBIOS 名称。

一旦执行了此操作，可能会更新 `smb.conf` 文件以设置 `security-domain` 选项，所有未来对 Samba 服务器的登录都将对 PDC 进行身份验证。

注意，尽管身份验证是对 PDC 进行的，访问 Samba 服务器的用户在该机器上必须有一个有效的 UNIX 账户。
这仅在 root 运行 `smbpasswd` 时可用。

- `-U Username` 选项可以与 `-r` 参数配合使用。在远程机器上更改密码时，它允许指定要更改密码的用户名。它是为了允许在系统中不同用户名的用户更改这些密码。

- `-h` 此选项打印 `smbpasswd` 的帮助字符串，根据是以 root 还是普通用户运行选择正确的那个。

- `-s` 此选项导致 `smbpasswd` 静默运行（即不发出提示）并从标准输入读取旧和新密码，而不是 `/dev/tty (1)` 程序）。此选项是为了帮助编写脚本驱动 `smbpasswd` 的人员。

- `username` 指定了所有 root 选项操作的用户名。只有 root 可以指定此参数，因为 root 拥有直接修改本地 `smbpasswd` 文件属性的权限。

# 注意

由于 `smbpasswd` 以客户端服务器模式工作并与 `smbd` 通信，对于非 root 用户，`smbd` 守护进程必须运行。一个常见问题是在 `smb.conf` 文件中指定 "`allow hosts`" 或 "`deny hosts`" 条目以限制访问本地机器运行的 `smbd` 的主机，但忘记允许 "`localhost`" 访问 `smbd`。

此外，`smbpasswd` 命令仅在 Samba 设置为使用加密密码时有用。请查看 `docs` 目录下的 `ENCRYPTION.txt` 文件了解如何进行操作。

# 版本

此帮助页对于 Samba 套件 2.0 版本是正确的。

# 作者

原始 Samba 软件及相关工具由 Andrew Triddell 创建 `samba-bugs@sample.org`。Samba 现在由 Samba Team 作为开源项目开发，类似于 Linux 内核的开发方式。

原始帮助页由 Karl Auer 编写。帮助页源码转换为 YODL 格式（另一项优秀的开源软件，可在 `ftp.icce.ruc/nl/pub/unix/` 获得），并由 Jeremy Allison 为 Samba2.0 发布进行了更新。`samba-bugs@sample.org`.

参阅 `samba (7)` 以了解获取贡献者完整列表以及提交错误报告、注释等的详细信息。

# smbstatus (1)

# Samba

1998年10月23日

# 名称

`smbstatus`—当前 Samba 连接报告

# 概要

`smbstatus [-b] [-d] [-L] [-p] [-S] [-s configuration file] [-u username]`

# 描述

此程序是 Samba 套件的一部分。
`smbstatus` 是一个非常简单的程序，用于列出当前的 Samba 连接。

# 选项

- `-b` 提供简短输出。
- `-d` 提供详细输出。
- `-L` 让 `smbstatus` 仅列出锁情况。
- `-p` 列出 `smbd` 进程列表并退出。适用于脚本编写。
- `-s` 让 `smbstatus` 仅列出列表。
- `-s configuration file` 默认配置文件名在编译时确定。指定的文件包含服务器所需的配置详情。更多信息请参 `smbconf (5)`。
- `-u username` 仅选择与用户名相关的信息。

# 版本

本帮助页适用于 Samba 套件的 2.0 版本。

# 参见

`smb.conf (5)`, `smbd (8)`

# 作者

原始 Samba 软件及相关工具由 Andrew Tridell (`samba-bugs@samba.org`) 创建。Samba 现在由 Samba 团队作为一个开源项目开发，类似于 Linux 内核的开发方式。

原始 Samba 帮助页由 Karl Auer 编写。帮助页源码转换为 YODL 格式（另一个优秀的开源软件，可在 `ftp://ftp.icce.rug.nl/pub/unix/` 获取），并由 Jeremy Allison (`samba-bugs@samba.org`) 为 Samba 2.0 发布进行了更新。

参阅 `samba (7)` 以了解获取贡献者完整列表以及提交错误报告、注释等的详细信息。

# 附录

# TCP/IP 文档

# 附录目标

- TCP/IP 网络资源列表
- 私有 IP 网络地址

# 作者说明

在本附录中，我选择了我认为在操作 Samba 时对你最有帮助的手页。随着你学习 Samba 的深入，你会发现其他有用的命令。

# TCP/IP 网络资源列表

以下列表是互联网 TCP/IP 资源的极佳参考。该列表经 Uri 许可使用。如需最新列表，请访问下方列出的主 URL。如果你不熟悉存在哪些资源，可以查看下方列出的广泛材料范围。

# URI 的 TCP/IP 资源列表

# 关于 TCP/IP 的 FAQ、教程、指南、网页、站点以及书籍

作者：URI RAZ

本文包含了一个各种资源列表（书籍、网站、FAQ、新闻组和实用的网络技术），旨在帮助新手学习 TCP/IP 协议族。

可以通过 FTP 获取文章：
`ftp://rtfm.mit.edu/pub/usenet-by-group/news.answers/internet/tcp-ip/re-source-list`
`ftp://rtfm.mit.edu/pub/usenet-by-hierarchy/comp/protocols/tcp-ip/TCP_IP_Resources_List_*`

# TCP/IP 网络资源列表

- 1. 关于 TCP/IP 的书籍

Richard Stevens' TCP/IP illustrated.
Addison-Wesley 出版。
第 1 卷 - 描述 TCP/IP 协议。
ISBN 0220163469

第 2 卷 - 从源码层面描述在 4.4BSD-Lite 中实现的 TCP/IP 栈。
ISBN 0220163354

第 3 卷 - 描述 HTTP, NNTP 等。
ISBN 0220164953

Richard Stevens' UNIX Network Programming.
Prentice Hall 出版。

- 2. 使用 TCP/IP 网络

Douglas Comer's Internetworking with TCP/IP.
Prentice Hall 出版。
第 1 卷 - 描述架构和原理。
ISBN 013216987

第 2 卷 - 描述实现。
ISBN 013255274

第 3 卷 - 描述应用。
ISBN 013260969

- 3. TCP/IP 详解

作者 Philip Miller
Digital Press 出版。
ISBN 155588168

- 4. TCP/IP 故障排除

作者 Mark A. Miller
M & T Books 出版。
ISBN 155851453

- 5. SNMP, SNMPv2, SNMPv3 以及 RMON1 和 RMON2

作者 William Stallings
Addison-Wesley 出版。
ISBN 0201485346

- 6. 高速网络：TCP/IP 和 ATM 设计原理

作者 William Stallings
Prentice-Hall 出版。
ISBN 0132596657

- 7. TCP/IP: 架构、协议与实现（带 IPv6 和 IP 安全

作者 Sidnie Feit
McGraw-Hill 出版。
ISBN 0070213895

- 8. 使用 Microsoft TCP/IP 网络

作者 Drew Heywood
New Riders 出版。
ISBN 1562057138

- 9. TCP/IP 网络管理
作者 Craig Hunt.
O'Reilly 出版。

ISBN 093717582X

使用 TCP/IP 的个人电脑联网 - 构建 TCP/IP 网络
作者：Craig Hunt
由：O'Reilly 出版
ISBN 1565921232

14天自学 TCP/IP。
作者：Timothy Parker
由：SAM'S Publishing 出版
ISBN 0672305496

PPP 设计与调试
作者：James Carlson
由：Addison-Wesley 出版
ISBN 0201185393

NOSIntro - 基于数据包无线电的 TCP/IP（KA9Q 网络操作系统简介）
作者：Ian Wade
由：Dowermain 出版
ISBN 1897649002

IPv6：新一代互联网协议
作者：Christian Huitema
由：Prentice-Hall 出版
ISBN 0138505055

# 附录 D：TCP/IP 文档

Unix 网络编程
作者：W. Richard Stevens
由：Prentice-Hall 出版
ISBN 0139498761

Unix System V. 网络编程
作者：Steven A. Rago
由：Addison-Wesley 出版
ISBN 0201563185

4.4 BSD 操作系统的设计与实现
作者：Marshall Kirk McCullik, Keith Bostic, Michael J. Karels 和 John S. Quarterman。
由：Addison-Wesley 出版。

Linux 内核原理
作者：M. Beck, B. Bohne, M. Dziadzka, U. Kunitz, R. Magnus, 和 D. Wernerner。
由：Addison-Wesley 出版

Windows Sockets 网络编程
作者：Bob Quinn 和 Dave Shute
由：Addison-Wesley 出版
ISBN 0201637228

- Win32 网络编程
作者：Ralph Davis
由：Addison-Wesley 出版
ISBN 0201489309

# TCP/IP 网络资源列表

2. Win32 中的多线程应用
作者：Jim Beveridge 和 Robert Wiener
由：Addison-Wesley 出版
ISBN 0201442345

互连
作者：Radia Perlman
由：Addison-Wesley 出版
ISBN 0201563220

互联网路由
作者：Christian Huitema
由：Prentice Hall 出版
ISBN 0131321927

互联网路由架构
作者：Bassam Halabi
由：Cisco Press 出版
ISBN 156205522

OSPF，互联网解剖
作者：John T.
由：Addison-Wesley 出版
ISBN 02016372

# 附录 D：TCP/IP 文档

计算机网络网络通信
作者：William S.
由：Prentice-Hall 出版
ISBN 013849872



# TCP/IP 网络资源列表

ISBN `093717582X`

这是一本关于 TCP/IP 网络管理的优秀书籍，涵盖了所有需要的主题，包括 DNS、路由、sendmail、配置和故障排除。本书以 UNIX 为导向。

使用 TCP/IP 的个人电脑联网 - 构建 TCP/IP 网络

作者：Craig Hunt

由：O'Reilly 出版

ISBN `1565921232`

这是一本关于 TCP/IP 网络管理的良好的书籍，以 PC 为中心，涵盖了 DOS、Windows、Windows-95 和 Windows-NT。

14天自学 TCP/IP。

作者：Timothy Parker

由：SAM'S Publishing 出版

ISBN `0672305496`

这本书旨在面向网络管理员，并在一个简短的进度内从零开始提供 TCP/IP 的概览。

PPP 设计与调试

作者：James Carlson

由：Addison-Wesley 出版

ISBN `0201185393`

这是一本关于 PPP 的优秀书籍。这本精凑的书籍充满了关于 PPP 的信息，兼具深度和广，涵盖了 LCP、协商与认证、网络层协议、带宽管理等，包括跟踪解释、C 语言代码和伪代码，以及大量的资源和参考文献。

NOSIntro - 基于数据包无线电的 TCP/IP（KA9Q 网络操作系统简介）

作者：Ian Wade

由：Dowermain 出版

ISBN `1897649002`

NOSintro 详细描述了如何使用 Phil Karn 的 KA9Q 网络操作系统，是该领域的经典参考著作。它包含了关于如何安装和配置 KA9Q，以及如何使其在数据包环境中运行的完整信息。这本书插图非常精美，有许多图表和键盘命令的实操示例。

书中的节录可以在 `http://www.netro.co.uk/nosintro.html` 找到。

IPv6：新一代互联网协议

作者：Christian Huitema

由：Prentice-Hall 出版

ISBN `0138505055`

这本书由互联网架构委员会成员 Christian Huitema 编写，对 IPv6 进行了极好的描述，解释了它与 IPv4 的区别，以及开发的各种和原因。

# 附录 D：TCP/IP 文档

## Unix 网络编程

作者：W. Richard Stevens

由：Prentice-Hall 出版

ISBN `0139498761`

第二版已过时，很快将涵盖。

## Unix System V. 网络编程

作者：Steven A. Rago

由：Addison-Wesley 出版

ISBN `0201563185`

这本书对 UNIX 网络编程提供了很好的介绍。尽管它以 SVR4 为中心，但它涵盖了许多主题，包括 STREAMS、TLI、sockets、RPC 和内核级通信，包括以太网和 SLIP 驱动程序。

## 4.4 BSD 操作系统的设计与实现

作者：Marshall Kirk McCullik, Keith Bostic, Michael J. Karels 和 John S. Quarterman。

由：Addison-Wesley 出版。

这本书描述了 4.4 BSD 操作系统在 Net/2 TCP/IP 协议栈实现中的内部原理。对最常用的 TCP/IP 实现进行了良好的解释。

## Linux 内核原理

作者：M. Beck, B. Bohne, M. Dziadzka, U. Kunitz, R. Magnus, 和 D. Wernerner。

由：Addison-Wesley 出版

这本书描述了 2.0 版本 Linux 操作系统的内部原理，并有一章专门介绍 TCP/IP 栈。

## Windows Sockets 网络编程

作者：Bob Quinn 和 Dave Shute

由：Addison-Wesley 出版

ISBN `0201637228`

这是一本关于 winsock 编程的优秀书籍，包含了关于从 Unix 和 sockets 移植应用、DLLs、调试的章节，以及非常棒的附录。

以下书籍与 TCP/IP 无直接关系，但推荐给编写 TCP/IP 客户端和服务器的 Windows 程序员阅读，并与上述书籍互补：

- Win32 网络编程

作者：Ralph Davis

由：Addison-Wesley 出版

ISBN `0201489309`

这本书向程序员展示了如何使用 Win95 和 NT 的 32 位功能构建网络应用，并包含了一张带有所有示例代码的软盘。

- Win32 中的多线程应用

作者：Jim Beveridge 和 Robert Wiener

由：Addison-Wesley 出版

ISBN `0201442345`

这本书向开发者展示了如何在 Win32 应用中使用以及在哪里使用多线程，并包含了一张光盘。

## 互连接

作者：Radia Perlman

由：Addison-Wesley 出版

ISBN `0201563220`

这是一本关于桥接和路由的良好的书籍，兼具广泛的覆盖范围和技术深度。书中仅用一章涵盖了 TCP/IP 路由，但非常详尽，并对桥接、路由以及总体上提供了更广泛的视角。

## 互联网路由

作者：Christian Huitema

由：Prentice Hall 出版

ISBN `0131321927`

这是一本关于路由的清晰且详尽的书，尽管有点过时。涵盖了所有主要的路由协议（RIP, OSPF, EIGRP, IS-IS, BGP, BGP3 & BGP4 & CIDR），并涵盖了多播、移动性和资源预留。

## 互联网路由架构

作者：Bassam Halabi

由：Cisco Press 出版

ISBN `156205522`

一本关于域间路由设计的清晰且详尽的书，带有许多带图表的清晰示例。重点关注 BGP，自然地也关注 Cisco 的方法。

## OSPF，互联网解剖

作者：John T.

由：Addison-Wesley 出版

ISBN `02016372`

一本关于 OSPF 的优秀著作，包含了 O 的的。（注：原文此处不完整）

## 计算机网络

作者：William S.

由：Prentice-Hall 出版

ISBN `013849872`

（注：原文此处不完整）

groups 以及 news.newers.questions 是查找常见问题解答（FAQs）和技巧的好地方。

- `comp.protocols` 层次结构，它涵盖了各种网络协议，如 tcp/ip、kermit 和 iso。注意，某些 TCP/IP 相关的协议有自己的讨论组（例如 NFS、SNMP、 NTP、PPP）。

- `comp.dom` 层次结构，包括讨论局域网（lans）、调制解调器和以太网的组。

- `comp.mail` 层次结构，它涵盖了各种电子邮件程序（pine、elm、sendmail 等）。

- `news` 层次结构，它涵盖了 usenet 的各种主题，包括 NNTP 协议。

- 所有新闻组的 FAQ 以及所有其他介绍性文档都存储在：`~/rtfm.mit.edu/pub/`。该网站关于 TCP/IP 的一个很好的介绍是该文件：`rtfm.mit.edu/pub/net/internet.text`。也可以在网页上 `http://www.faqs.org/` 访问 FAQ。

由于 `rtfm.mit.edu` 和 `faqs.org` 网站可能负载非常重，因为许多站点镜像了 FAQ 存档，建议在地理位置更近的站点搜索 FAQ。镜像站点列表（允许通过 FTP、WWW、Gopher、mail 等访问）可以在此处获取：`rtfm.mit.edu/pub/faqs/answers/introduction`

`comp.protocols.tcp-ip` 组有一个 FAQ，该 FAQ最初由 George V. Neville-Neil 维护，现在由 Mike Oliver 维护，位于：`rtfm.mit.edu/pub/faqs/internet/tcp-ip/tcp-ip-faq/` `http://www.ipsrc.com/tcpipfaq/default.htm` `t2.techn.ac.il/~s284543/tcp-ip/default.htm`

`comp.protocols.tcp-ip` 新闻组有一个由 Bernard D. Aboba 编写的 FAQ，可以在这里找到：`ftp://ftp.netcom.com/pub/mail.com/IBTCP/ibmtcp.zip` `http://www.inetassist.com/faqs/tcpipmbcp.zip`



# TCP/IP 网络资源列表

`comp.protocols.tcp.domains` 新闻组有一个由 Chris Peckham 维护的 FAQ，可以在这里找到：`http://www.users.pfcm.net/-cdp-tcp-faq/rtfm.mit.edu/pub/usenet/news/answers/tcp-ip/domains-faq/`

由 Vic Metcalfe 编写的 `sockets` 编程 FAQ 位于：`ftp://rtfm.mit.edu/pub/usenet/news/answers/unix-faq/socket` `http://www.faqs.org/unix-faq/socket.index.html`

`alt-winsock` 新闻组有一个 Nancy Cedeno Aguero FAQ，位于：`http://www.news.com/user/alt-winsock-faq.html` `http://www.faqs.org/windows/winsock-faq/index.html` `ftp://rtfm.mit.edu/pub/usenet/news.answers/windows/winsock-faq`

由 Warren Young 编写的 Winsock 程序员 FAQ 位于：
`http://www.cyberport.com/~tangent/programming/winsock/`
`http://www.faqs.org/faqs/windows/winsock/programmer-faq/index.html`
`ftp://rtfnm.mit.edu/pub/usenet/news.answers/winsock/programmer-faq`

由 Bob Quinn 编写的 windows-sockets 页面位于：
`http://www.sockets.com/`

`sockadder.com` - WinSock 编程资源站点位于：
`http://www.sockadder.com/`

由 Thamer Al-Herbish 编写的 Raw IP Networking FAQ 可用：
`http://www.whitefang.com/rin/`

Dardust 有 winsock 页面，位于：
`http://www.stardust.com/wsresource/html`
`http://www.winsock.com/`

Wandel & Goltermann 推出了 `decodes.com`
尺寸列表旨在作为“网络协议分析资源”
`http://www.decodes.com/`

Secure Sockets Layer（SSL）讨论 FAQ 位于：
`http://www.consensus.com/security/ssl-talk-faq.html`
`ftp://ftp.consensus.com/pub/security/ssl-talk-faq.txt`

关于 Ssh（安全外壳）的信息可以在此处找到：
`http://www.ssh.org/`
`http://www.cs.fi/ssh/`
`http://www.faqs.org/faqs/computer-security/ssh-faq/index.html`
`ftp://rtfnm.mit.edu/pub/usenet-by-group/computer.security/ssh`

关于 SOCKS（使用代理/防火墙的安全套接字）
`http://www.socks.net.com/`
`ftp://coast.cs.purdue.edu/pub/doc/faq/faq_socks`

DNS 资源目录是一项极好的资源，可以找到
`http://www.dns.net/dnsrrd/`

Jarle Aase 的 FTP 协议资源中心网站可以找到
`http://war.jgaa.com:8080/ftp/`

关于源自 UNIX 工具的各种 TCP/IP 协议信息，以及 r-* 服务、lpd，可以在一个为了将信息集中在一个点而编写的文件找到
`http://t2.technicion.il/~s284554-tcpip.html`

- `comp.protocols.tcp-ip` 有一个 FAQ，以及 `news.newers.questions` 是查找常见问题解答和技巧的好地方。

`comp.protocols.tcp-ip` 有一个 FAQ，由 George V. Neville-Neil 维护，现在 Mike Oliver 维护，位于：`rtfm.mit.edu/pub/faqs/internet/tcp-ip/tcp-ip-faq/` `http://www.ipsrc.com/tcpipfaq/default.htm` `t2.techn.ac.il/~s284543/tcp-ip/default.htm`

`comp.protocols.tcp-ip` 新闻组有一个由 Bernard D. Aboba 编写的 FAQ，可以在这里找到：`ftp://ftp.netcom.com/pub/mail.com/IBTCP/ibmtcp.zip` `http://www.inetassist.com/faqs/tcpipmbcp.zip`



关于源自 UNIX 工具的各种 TCP/IP 协议信息，以及 r-* 服务、lpd，可以在一个为了将信息集中在一个点而编写的文件找到

http://t2.technicion.il/~s284554-tcpip.html

- 4. comp.protocols.tcp-ip 有一个 FAQ，以及 news.newers.questions 是查找常见问题解答和技巧的好地方。

comp.protocols.tcp-ip 有一个 FAQ，由 George V. Neville-Neil 维护，现在 Mike Oliver 维护，位于：rtfm.mit.edu/pub/faqs/internet/tcp-ip/tcp-ip-faq/ http://www.ipsrc.com/tcpipfaq/default.htm t2.techn.ac.il/~s284543/tcp-ip/default.htm

comp.protocols.tcp-ip 新闻组有一个由 Bernard D. Aboba 编写的 FAQ，可以在这里找到：ftp://ftp.netcom.com/pub/mail.com/IBTCP/ibmtcp.zip http://www.inetassist.com/faqs/tcpipmbcp.zip

comp.protocols.tcp.domains 新闻组有一个由 Chris Peckham 维护的 FAQ，可以在这里找到：http://www.users.pfcm.net/-cdp-tcp-faq/rtfm.mit.edu/pub/usenet/news/answers/tcp-ip/domains-faq/

由 Vic Metcalfe 编写的 sockets 编程 FAQ 位于：ftp://rtfm.mit.edu/pub/usenet/news/answers/unix-faq/socket http://www.faqs.org/unix-faq/socket.index.html

alt-winsock 新闻组有一个 Nancy Cedeno Aguero FAQ，位于：http://www.news.com/user/alt-winsock-faq.html http://www.faqs.org/windows/winsock-faq/index.html ftp://rtfm.mit.edu/pub/usenet/news.answers/windows/winsock-faq

# TCP/IP 网络资源列表

由 Warren Young 编写的 Winsock 程序员 FAQ 位于：

http://www.cyberport.com/~tangent/programming/winsock/

http://www.faqs.org/faqs/windows/winsock/programmer-faq/index.html

ftp://rtfnm.mit.edu/pub/usenet/news.answers/winsock/programmer-faq

由 Bob Quinn 编写的 windows-sockets 页面位于：

http://www.sockets.com/

sockadder.com - WinSock 编程资源站点位于：

http://www.sockadder.com/

由 Thamer Al-Herbish 编写的 Raw IP Networking FAQ 可用：

http://www.whitefang.com/rin/

Dardust 有 winsock 页面，位于：

http://www.stardust.com/wsresource/html

http://www.winsock.com/

Wandel & Goltermann 推出了 decodes.com

尺寸列表旨在作为“网络协议分析资源”

http://www.decodes.com/

Secure Sockets Layer（SSL）讨论 FAQ 位于：

http://www.consensus.com/security/ssl-talk-faq.html

ftp://ftp.consensus.com/pub/security/ssl-talk-faq.txt

关于 Ssh（安全外壳）的信息可以在此处找到：

http://www.ssh.org/

http://www.cs.fi/ssh/

http://www.faqs.org/faqs/computer-security/ssh-faq/index.html

ftp://rtfnm.mit.edu/pub/usenet-by-group/computer.security/ssh

关于 SOCKS（使用代理/防火墙的安全套接字）

http://www.socks.net.com/

ftp://coast.cs.purdue.edu/pub/doc/faq/faq_socks

DNS 资源目录是一项极好的资源，可以找到

http://www.dns.net/dnsrrd/

Jarle Aase 的 FTP 协议资源中心网站可以找到

http://war.jgaa.com:8080/ftp/

关于源自 UNIX 工具的各种 TCP/IP 协议信息，以及 r-* 服务、lpd，可以在一个为了将信息集中在一个点而编写的文件找到

http://t2.technicion.il/~s284554-tcpip.html

# Daryl 的 TCP/IP 入门指南

网络内侧的地址划分与子网划分

http://ipprimer.windorscs.com/

轻松掌握子网掩码，作者：John Lambert, MCSE 认证工程师

http://support.wrq.com/tutorials/tcipfundamentals.html

Al Vokan 的网络掩码计算器

该计算器通过 JavaScript 实现（而非 CGI），

速度非常快，但需要支持并启用 JavaScript。

http://www.telplant.net/public/sparkman/netcalc.html

另一个 CIDR 子网掩码计算器可以在此处找到

http://minnie.cs.adfa.edu.au/Gateways/range_check.html

- 12. 常见问题解答 (FAQ)

http://www.net/faqs/cdr.faq.html

- 13. 思科网络教程与缩写

http://cio-sys.cisco.com/univerd/data/doc/intrnet/ita.htm

- 14. IBM 提供的“TCP/IP 教程与技术概述”

http://publib.boulder.com/cgi-bin/bookm/BOOKS/GG243376/CONTENTS

- 15. TCP/IP 协议与互联网概述

http://www.hill.com/library/staffpubs/tcipip.html

- 16. IP 地址划分基础

http://support.wrq.com/tutorials/tcip/tcipfundamentals.html

- 17. 理解地址划分：关于你想了解的一切

http://www.3com.com/nsc/510302.html

- 18. 理解 IP 划分

http://noc.gate.net/doclib/faqs/help/net.html

- 19. hedrick 互联网协议简介

http://www.duth.gr/InfoBase/intro.ip.toc

- 20. 由 Chris Chambers, Justin Dolske 和 Jayaraman Iver 编写关于 TCP/IP 安全的短文

http://www.cis.ohio-state.edu/~dolske/gradwork/cis694q/

- 21. Von Welch 有一个网络性能页面，

其中一个次要部分解释了 TCP 窗口

http://www.nciuc.edu/People/velch/net_perf/

http://www.nciuc.edu/People/velch/net_perf/tcp_windows.html

- 22. Marc Slemko 的 MTU 发现与过滤 ICMP

http://www.worldgate.com/marcs/mtu/

- 23. Cliff 为新学者提供的互联网协议简介

http://www.halcyon.com/cliffg/utwech/shared_info/internet_protocols.html

- 24. Catalyst 的 TCP/IP 编程简介

http://www.catalyst.com/tcipintro.html

- 25. Frank Dekenzel 的 DNS 教程

http://www.geociles.com/SiliconValley/Network/4504/dns_tut.txt

Gary Keller: 设置你的 DNS



http://www.hill.com/library/staffpubs/dns.html

Criet Liu 编写的 DNS 安全扩展 (DNSSEC)

http://www.acmebbw.com/papers/dnssec.pdf

- 26. RPC (远程过程调用)

http://pandonia.canberra.edu.au/OS/114_1.html

http://www.ja.net/documents/NetworkNews/Issue44/rpc.html

http://www.mtm.be/~kiss/docs/dce/rpc.html

http://glacier.uni.nl/~samal/class/DIST/lectures/rpc.html

# TCP/IP 网络资源列表

## 27. DHCP

Ralph Doms DHCP 资源站点

http://www.dhcp.org/

Alan Dobkin 的 DHCP 资源

http://nws.cc.emory.edu/webstaff/alan/net-man/computing/dhcp/

## 28. BSD socket 编程教程

快速入门 - http://ttp.com/pages/jimf/sockets.html

入门导读 - http://cnga.waterloo.ca-/mlvioy/stuff/ipc_intro_tut.txt

高级教程 - http://cnga.waterloo.ca-/mlvioy/stuff/ipc_adv_tut.txt

Windows socket 编程

http://users.arca.com/vmis/wsockexp.htm

http://users.neca.com/vmis/wsockprg.htm

Socket 编程入门

http://www.uwo.ca/its/doc/courses/notes/socket/index.html

Beej 的网络编程指南

http://www.ect.suchnico.edu/~beej/guide/

Vijay Mukhi 的 Windows 编程页面

http://users.neca.com/vmis/wsockprg.htm

网络程序员员指南

http://www.ibr.cs.tu-bs.de/~harbaum/docs/netprog/contents.html

Unix 网络编程

http://gala.cs.umnass.edu/ntu_socket/

Spencer 的 Socket 站点

http://www.lowtek.com/sockets/

## 29. Xiaomi 的 WinSock 页面

http://omni.purdue.edu/~xniu/winsock.htm

## 30. 路由协议

通用 - http://www.bind.com/

http://www.cisco.com/unvercd/cc/td/cisintwk/ito_doc.html

IGRP

http://www.cisco.com/unvercd/cc/td/ito_doc.html

IGRP & Enhanced IGRP

http://www.cisco.com/unvercd/cc/td/ito_doc.html

IGRP & Enhanced IGRP

http://www.cisco.com/unvercd/cc/td/ito_doc.html

RIP

http://www.cisco.com/unvercd/cc/td/ito_doc.html

OSPF, BGP, IPv6, 网关 - http://www.roedu.net~cmi/network/

EGP

http://www.cisco.com/unvercd/cc/td/ito_doc.html

BGP

http://www.cisco.com/unvercd/cc/td/ito_doc.html

OSPF

http://www.cisco.com/unvercd/cc/td/ito_doc.html

OSPF

http://www.cisco.com/unvercd/cc/td/ito_doc.html

## 31. Merit 联盟

该站点包含了大量关于 GateD 的信息，包括源码发行等

http://www.gated.org/

GNU Zebra 站点

Zebra 项目实现了 OSPFv2、BGP 和 RIPv2。它与 GateD 不同之处在于它将计算从 CPU 卸载到 ASIC 并具有模块化。

http://www.zebra.org/

## 32. 交换：

“第 3 层和第 4 层交换”，来自 Performance Computing

http://www.performancecomputing.com/packets/9812

IP 交换：问题与替代，作者 R. Jain

http://www.cis.ohio-state.edu/~jain/talks/ipsw.html

“IP 交换”，作者 Shishir Agrawal 的课程

http://www.cis.ohio-state.edu/~jain/cis7889/ip_switching/index.html

“L5：自学”，来自 IBM 的报告

## 33. 互联网性能测量与分析首页

http://www.merit.edu/ipma/

## 34. 主机名到经度/纬度

http://cello.cs.uiuc.edu/cgi-bin/slamp/ill21/

## 35. 互联网天气

http://www.internet.com/

http://www3.mids.org/weather/

http://www.internettffic.com/

## 36. 连接：互联网百科全

http://www.freesoft.org/(CIE)/index.html

## 37. 网络工程师工具箱

http://www.wanresources.com/

## 38. 面向互联网管理员的 TCP/IP

http://techref.ezime.com/tec/

## 39. 你的内网页面

http://users.neca.com/vmls/roll.html

## 40. TCP/IP 网络资料

http://spectral.mscs.edu/NetworksClass/

## 41. 用于互联网访问的 Windows 和 TCP/IP

http://learning.lib.vt.edu/wtincip.html

## 42. Al 的 WinSock FAQ

http://www.cerberus-sys.com/beislu/mss_rwin.html

## 43. Schulzrinne 的 RTP (实时协议)站点

http://cs.columbia.edu/~hgs/rtp/

- 皇后大学实时传输协议 (QRTP)

http://44.queensu.ca:8000/link/QRTP.html

## 44. 我的 IP -> 地理位置检测页面

http://t2.technion.ac.il/-s2845543/IP2geo.html

## 45. 计算机网络与互联网协议

作者 Keith W. Ross 和 James F. Kurose

http://www.seas.upenn.edu/~ross/book/Contents.htm

## 47. 慢启动与延迟确认的解释

http://www.sun.com/sun-on-performance/tcp.slowstart.html

## 48. 关于 NetBIOS 和 NetBEUI 的信息可以在此处找到

http://www.s390.ibm.com/bookkr-cgi/bookkr.com/BOOKS/bk8p7001/CONTENTS

http://helloworld.computer.com/pages/timotheydev/nbf.html

## 49. RGB 的 TCP/IP 白皮书与指南

http://www.rgb.co.uk/support/tcpip.htm

## 50. ADTRAN PPP 网络

http://www.alliedataacom.com/dial-up-point-technology.html

## 51. Linux 的 IP 伪装 (Masquerade)

http://ipmasq.cjb.net/

大学提供的 TCP/IP 课程：

### 0. 互联网分析协作协会

维护了一份互联网工程相关大学课程的列表。

http://www.caida.org/iec/courses/index.html

### 1. Reuben Cohen 博士

互联网网络

以色列理工学院 - Technion

http://www.cs.technion.ac.il/~cs23641/

### 2. Shomi Dolev 博士

计算机通信与分布式算法

本·格利恩大学



http://www.cs.bgu.ac.il/~ccda982/（希伯来语）

- 3. Ofer Hadar 博士

计算机网络导论

以色列理工学院 - Technion

http://www.cs.technion.ac.il/~cs23634/（希伯来语）

- 4. Deborah Estrin 教授

计算机通信

南加州大学

http://www.catarina.usc.edu/cs551/cs551.html

- 5. Dave Hollinger

网络编程

http://www.cs.rpi.edu/courses/netprog/index.html

- 6. Jim Kurose 教授

计算机网络

http://gaia.cs.umass.edu:80/cs653/

- 7. David C. Blight

电信网络

http://www.ee.umanitoba.ca/~blight/c24759-97/

- 8. Phil Scott

数据通信，计算机网络

http://ironbark.bendigo.latrobe.edu.au/staff/pscott/pscott.home.html

- 9（注：此处原文漏掉编号，根据逻辑补全翻译）

- 32. 交换：

“第 3 层和第 4 层交换”，来自 Performance Computing。

http://www.performancecomputing.com/packets/9812

IP 交换：问题与替代，作者 R. Jain

http://www.cis.ohio-state.edu/~jain/talks/ipsw.html

“IP 交换”，作者 Shishir Agrawal 的课程。

http://www.cis.ohio-state.edu/~jain/cis7889/ip_switching/index.html

“L5：自学”，来自 IBM 的报告

## 附录 D：TCP/IP 文档

- 9. David Cygganski

电信传输技术

http://bugs.wpi.edu:8080/EE535/

- 10. S. Keshav

工程计算机网络

http://www.cs.cornell.edu/cs519/

- 11. Ralph Droms 教授

普渡大学

计算机网络

http://www.netbook.cs.purdue.edu/cs363/index.html

- 12. Simon Cleary

RMIT 大学

计算机网络与协议

http://www.cse.rmit.edu.au/-rdss/courses/ds454/

- 13. Phil Scott

拉特罗伯大学

计算机网络

http://ironbank.bendigo.latrobe.edu.au/subjects/bitcne/

以下链接将提供有关 IPv6 的信息：

- 1. 下一代 IP（IP Next Generation）

这是获取任何关于 IPv6 信息的首选网站，涵盖了从概述、RFC 和草案到实现的内容（包括各种平台上的协议栈可用性以及 IPv6 协议栈源代码）。

http://playground.sun.com/pub/ipng/html/ipng-main.html

- 2. 英国 IPv6 资源中心

http://www-cs6.lancs.ac.uk/

- 3. 6bone 首页

http://www.6bone.net/

- 4. 下一代 IP 概述

http://info.soc.org/RMF/PAPER/pt1/html/pt1.hinden

- 5. IPv6：新的互联网协议

作者：William Stallings

http://www.comsec.org/pubs/surveys/stallings-stallings-orig.html

- 6. 新型且改进的互联网协议

作者：William Stallings

http://www.byte.com/art/9609/sec5/art2.html

- 7. IP 组首页

http://gangen.cs.tcd.ie/4ba2/ipng/

- 8. IPv6 RFC 及链接合集

http://aloni.com/IPv6.htm

- 9. IPv6：互联网协议的新版本

作者：Steve Deering

http://trail.isi.edu/deering/

- 10. 互联网的未来：IPng 和 TCP/IP 协议

http://ccnga.uwaterloo.ca/-dkston/presentations/IPng_index.html

- 11. IPv6 规范 - 最新的 RFC 和互联网草案合集

http://heusa.sumimoto.com/htmls/randd/ipv6/doc.html

- 12. Process' IPv6 资源中心。

http://www.teief.com/ipv6.http

## TCP/IP 网络资源列表

- 13. IPv6：下一代互联网协议

作者：Gary C. Kessler

http://www.hill.com/library/staffpubs/ipv6_exp.html

- 14. IPv6：下一代互联网协议

http://www.3cm.com/nsc/ipv6.html

- 15. 文献研究 IPv6（IPng），作者：Mike Crawford。

http://www.mediaport.org/~iamano/lr.zip

- 16. 现有的路由协议与 IPv6

http://www.pub.ro/~cmatei/network/ipv6/

- 17. IPv6 组织网站。

http://www.ipv6.org/

有关互联网未来的信息查询：

- 1. Internet2 网站。

http://www.internet2.org/

- 2. 下一代互联网倡议

http://www.ngi.gov/

- 3. 服务质量论坛（QoS Forum）网站。

http://www.qosforum.com/tech_resources.html

以下链接将提供有关 IP 组播的信息：

- 1. IP 组播首页

http://www.ipmulticast.com/

- 2. Mbone（多播骨干网）常见问题解答

http://www.cs.columbia.edu/~hsg/internet/mbone-faq.html

- 3. 多播骨干网首页

http://www.mbone.com/

- 4. IP 组播简介

http://www.ganges.cs.tcd.ie/4ba2/multicast/index.html

- 5. IP 组播路由简介

http://www.3cm.com/nsc/013103.html

- 6. 解释多播路由的文档集。

ftp://ftpeng.cisco.com/ipmulticast/multicast_training.html

以下链接将提供有关 IP 安全的信息：

- 1. 互联网安全调查 - http://www.trouble.org/survey/

- 2. Phrack 杂志网站 - http://www.phrack.com/

- 3. SKIP - http://www.skip.org/

SKIP - 互联网协议的简单密钥管理（Simple Key management for Internet Protocols）在 IP 层对信息进行加密，使所有通过 IP（使用 TCP 或 UDP）通信的应用程序都能从中获益。

4. Peter Gutmann 的“安全与加密相关的资源和链接”包含了大量安全网站的链接。

http://www.cs.auckland.ac.nz/~pgut001/links.html

5. COAST 的热点列表：计算机安全、法律与隐私是一个包含大量安全问题链接的集合。

http://www.purdue.edu/homes/spaf/hotlist

# 附录 D：TCP/IP 文档

Linux 主页 http://www.linux.org/

Linux 主页 http://www.linux.org/

Linux 内核存档 http://www.kernel.org/

互联网软件协会（Internet Software Consortium）是一个非营利组织，发布并支持 BIND、DHCP 和 INN。这些软件免费提供，并通过邮件列表提供有限的支持。当然，支持合同是付费的。

http://www.isc.org/

Erick Engelke 有一个名为“WATTCP Locator”的页面，提供了关于 WATCP（一个用于 DOS 的 TCP/IP 包）的大信息。该页面指向 WATCP 的最新版本。

http://www.supro.com/wattcp/wattcp.html



Gisele Vanhem 升级了 WATTCP tcp/ip 栈，包含了 DHCP、RARP、基于文件的查找以及 BSD 兼容 API。支持多种编译器和 DOS 扩展器。WATT-32 位于 `http://www.bgnett.no/-ga/index.html`

Phil Karn 的 KA9Q（DOS TCP/IP 栈）位于 Karn 的主页下：

`http://people.qualcomm.com/code/ka9qnos/`

Michael Bernardi 的 MS-DOS 互联网常见问题解答，包含适用于 DOS 的 TCP/IP 栈和应用程序列表。

`ftp://ftp.demon.co.uk/doc/ibmpc/dos-apps.txt`

`http://www.dendarii.demon.co.uk/paqs/dos-apps.html`

Dan Kegel 有一个名为“MS-DOS TCP/IP 编程”的页面，其中充满了关于 DOS TCP/IP 的链接和信息。

`http://www.alumni.caltech.edu/-dank/trumpet/`

Public Netperf 主页由 HP 提供，地址为

`http://www.netperf.org/`

Linux 路由器项目制作软磁盘大小的 Linux 发行版，用于构建和维护路由器、终端服务器等。

`http://www.linuxrouter.org/`

- 7. 一个良好的搜索引擎可以提供更多信息。

位于 `http://www.yahoo.com/` 的 Yahoo 引擎拥有非常良好的索引，包括一个关于 TCP-IP 的页面。

其他一些搜索引擎是：

- 位于 `http://www.altavista.com/` 的 AltaVista
- 位于 `http://www.infoseek.com/` 的 InfoSeek
- 位于 `http://www.hotbot.com` 的 Hotbot

网络计算机科学技术参考库（Networked Computer Science Technical Reference Library）网站是一个计算机科学文章存档，可以通过强大的搜索引擎进行搜索。

`http://www.ncstrl.org/`

# TCP/IP 网络资源列表

DejaNews 网站存档了所有到 usenet 的帖子。

该网站 `http://www.dejanews.com/` 允许用户使用不同的方法搜索过去几年发送的帖子，这些方法可以结合文章内容、作者和新闻组的关键词进行搜索。

查找讨论陌生主题帖子的能力，可以为过去在 usenet 上提出的问题提供即时答案。

如果你希望自己的帖子不被 dejanews 存档，请在你的帖的表头中添加 "`X-On-Archive: Yes`"，或将其写在你文章的第一行。请注意，这并阻止他人引用你的文章，从而导致引用的材料被存档。

DejaNews 的其他有用功能：

- 发帖者简介。这显示了发帖者向每个新闻组发送了多少条帖子，通过电子邮件地址识别发帖者。
- 通过帖子中词汇出现的频率搜索新闻组，结果应谨慎对待，例如

## 人们讨论基督教（christianity）的新闻组：

以下列表中的所有新闻组在某篇文章中包含了基督教。

置信度评分表示我们有多大把握认为人们在新闻组中讨论了你的话题。点击新闻组名称将显示所有匹配你查询的文章。

| 置信度 | 新闻组 |
| :--- | :--- |
| 99% | alt.theism |
| 63% | rec.games.frp.misc |
| 54% | rec.music.christian |
| 39% | alt.religion.christian |
| 38% | soc.religion.christian |
| 38% | soc.penpals |
| 33% | austin.general |

位于特德海姆（Trondheim）的挪威科技科学大学在网上有一个 FTP 搜索引擎，地址为 `http://ftpsearch.ntnu.no/ftpsearch`，可以找到全球匿名 FTP 服务器上的文件。

该搜索方式与 `archie` 的操作类似，对于查找实用程序的源码、常见问题解答（FAQs）等非常有用。

## 单词单词 ping的快速搜索产生了以下输出：

- `ftp.cc.uec.ac.jp`（日本）
  1 `ftp.cc.uec.ac.jp` `/0/0.4/BSD-Lite/usr/src/sbin/ping`
  2 `ftp.cc.uec.ac.jp` `/0/0.4/BSD-Lite/usr/src/sys/i386/6floppy/ping`
  3 `ftp.cc.uec.ac.jp` `/0/Linux/redhat-4.1/i386/RedHat/imastage/usr/bin/ping`
  4 `ftp.cc.uec.ac.jp` `/0/Linux/redhat-devel/i386/RedHat/imastage/usr/bin/ping`
- `ftp.dwc.edu`（教育）
  5 `ftp.dwc.edu` `/03/redhat/i386/RedHat/imastage/usr/bin/ping`
  6 `ftp.dwc.edu` `/03/redhat/Sparc/imastage/usr/bin/ping`
  7 `ftp.dwc.edu` `/03/redhat/sparc/src/rescue/bin`
- `ftp.ujixer.co.jp`（日本）
  8 `ftp.ujixer.co.jp` `/1/NetBSD-current/src/sbin/ping`

其他文件搜索引擎位于 `http://www.file.com/` 和 `http://acsland.edu/cgi-bin/vsl-front/`，可以找到平台（如 unix, windows）或特定格式（如 midi, source code）的文件。

## 讨论网络与 TCP/IP 的新闻组

`news:alt.comp.sys.xy`: 关于 Whittaker/plex
`news:alt.com.slip-emulators`: SLIP/PPP 账户
`news:alt.com.telecom`: 电信技术
`news:alt.com.radius`: 远程拨号服务
`news:alt.com.mbone`: 全球互联网网络
`news:alt.com.winsock`: Windows Sockets。
`news:alt.com.programming`: Windows Sockets。

## TCP/IP 网络资源

`news:alt.com.trumpet`: Trumpet 阅读器
`news:alt.com.cabling`: 布线、安装和使用
`news:alt.com.cell-relay`: 基于单元的产品
`news:alt.com.frame-relay`: 关于帧继网络的技术
`news:alt.com.isdn`: 集成业务数字网络 (ISDN)。
`news:alt.com.lans.ethernet`: 以太网/IEEE 802.3 协议
`news:alt.com.lans.fdi`: FDDI 协议讨论
`news:alt.com.lans.hyperchannel`: IP 网络中的高速通道
`news:alt.com.lans.misc`: 局域网硬件和软件
`news:alt.com.lans.token-ring`: 安装环形网络
`news:alt.com.modems`: 数据通信硬件和软件
`news:alt.com.modems.cable`: 缆线调制解调器和通过缆电视接入
`news:alt.com.net-analysis`: 网络测试与分析
`news:alt.com.net-management`: 网络管理方法和应用程序
`news:alt.com.sys.bay-networks`: Bay 网络硬件、软件、其他产品
`news:alt.com.sys.cisco`: Cisco 路由器和桥接器信息
`news:alt.com.sys.nortel`: 电信产品和系统
`news:comp.d.telecom`: 电信摘要
`news:comp.d.telecom.tech`: 电信技术方面
`news:comp.d.wan`: 所有关于广域网络的话题
`news:comp.d.xdsl`: 不同 DSL 技术讨论
`news:os.linux.networking`: Linux 下的网络和通信
`news:os.ms-windows.apps.winsock.mail`: Winsock 电子邮件应用
`news:os.ms-windows.apps.winsock.misc`: 其他 Winsock 应用程序
`news:os.ms-windows.apps.winsock.news`: Winsock 新应用程序
`news:os.ms-windows.networking.misc`: Windows 和其他网络
`news:os.ms-windows.networking.ras`: Windows RAS 网络
`news:os.ms-windows.networking.tcp-ip`: Windows 和 TCP/IP 网络



`news:os.ms-windows.networking.win95`: Win95 到 Novell、TCP/IP、其他网络

`news:os.ms-windows.networking.windows`: Windows 内置网络

`news:os.ms-windows.nt.admin.networking`: Windows NT 网络管理

`news:os.ms-windows.programmer.networks`: 网络编程

`news:os.ms-windows.programmer.tools.winsock`: Winsock 编程

`news:os.os2.networking.tcp-ip`: OS/2 下的 TCP/IP

# TCP/IP 网络资源列表

`news:comp.protocols.dns.bind`: 伯克利互联网域名 (BIND)

`news:comp.protocols.dns.ops`: DNS 操作（非 BIND 特定）

`news:comp.protocols.dns.std`: DNS 标准活动，包括 IETF

`news:comp.protocols.iso`: ISO 协议栈

`news:comp.protocols.kerberos`: Kerberos 认证服务器

`news:comp.protocols.misc`: 各种形式和类型的协议

`news:comp.protocols.nfs`: 关于网络文件系统的讨论

`news:comp.protocols.ppp`: 互联网点点协议讨论

`news:comp.protocols.smb`: SMB 文件共享协议和 Samba SMB 服务器/客户端

`news:comp.protocols.snmp`: 简单网络管理协议

`news:comp.protocols.tcp-ip`: TCP 和 IP 网络协议

`news:comp.protocols.tcp-ip.domains`: 与域名风格名称相关的题

`news:comp.protocols.tcp-ip.ibmpc`: 用于 IBM 类个人电脑的 TCP/IP

`news:comp.protocols.time.ntp`: 网络时间协议

`news:comp.security.firewalls`: 任何网络防火墙安全的内容

`news:comp.security.misc`: 计算机和网络安全问题

`news.comp.std.wireless`: 无线网络技术标准审查

## 附录 D：TCP/IP 文档

`news:comp.unix.large`
大型机及大型网络中的 UNIX。

`news:trumpet.questions`
Trumpet Winsock 的问题与一般讨论。

`news:trumpet.bugs`
Trumpet Winsock 漏洞或“特性”的报告与讨论。

`news:microsoft.public.win16.programmer.networks`

`news:microsoft.public.win32.programmer.networks`

`news:microsoft.public.win95.dialupnetwork`

`news:microsoft.public.win95.networking`

`news:microsoft.public.win98.comm.dun`

`news:microsoft.public.win98.comm.modem`

`news:microsoft.public.win98.networking`

`news:microsoft.public.windowsnt.protocol`

`news:microsoft.public.windowsnt.protocol.tcpip`

## 5. 其他网络页面

- 1. 提供网络术语词典
http://www.ktek.com/ktek/Lans-Wans.html
- 2. 提供 `comp.protocols.ppp` 的常见问题解答 (FAQ)
http://www.faqs.org/faqs/faq/part1/index.html
ftp/rtfm.mit.edu/pub/usenet-by-group/comp.protocols.ppp/
提供 `comp.protocols.snmp` 的常见问题解答 (FAQ)
http://www.pantherdig.com/snmpfaq/index.html
ftp://ftp.cs.utente.nl/pub/src/snmp/
提供由 John Wobnus 编写的 DHCP 常见问题解答 (FAQ)
http://web.syr.edu/~jmwobus/comfaqs/dhcp.faq.html
提供由 Mike Meyer 编写的 Amiga TCP/IP 常见问题解答 (FAQ)
http://www.phone.net/ATCPFAQ/amitcpq.txt
http://www.phone.net/ATCPFAQ/amitcpq.html
Kermit 项目网站位于
http://www.kermit-project.org/

## TCP/IP 网络资源列表

- 3. `comp.dcom.lans` 以太网常见问题解答 (FAQ) 位于：
http://www.faqs.org/faqs/LANs/ethernet-faq/index.html
ftp://rtfm.mit.edu/pub/usenet-by-hierarchy/news/answers/LANs/ethernet-faq
Charles Spurgeon 的以太网页面发布在：
http://wwwhost.ots.utex.edu/ethernet/ethernet-home.html
`comp.dcom.lans` 令牌环常见问题解答 (FAQ) 位于：
http://home.spryn.com/spryn/jtmesser/faq/contents.html
`comp.dcom.cabling` 缆布常见问题解答 (FAQ) 位于：
http://www.faqs.org/faqs/LANs/cabling-faq/index.html
ftp://rtfm.mit.edu/pub/usenet-by-group/comp.dcom.cabling/
`comp.dcom.cell-relay` 中继常见问题解答 (FAQ) 位于：
http://cell-relay.indiana.edu/cell-relay/FAQ/ATM-FAQ/FAQ.html
- 4. Berkeley 的 Daedalus 项目讨论无线网络和移动计算，其网页包含了一些文章的链接。
http://daedalus.cs.berkeley.edu/
两页带有技术细节的 T1 描述是：
http://www.laruscorp.com/titut.html
http://www.gsnetworks.com/ezvu/ezvu500/TUTORIAL/PROTOCOL/genT1.txt
- 5. Big-LAN 常见问题解答 (FAQ) 为 big-lan@listserv.syr 邮件列表创建，讨论“校园规模局域网的设计与运行问题……”位于：
ftp://rtfm.mit.edu/pub/usenet-by-hierarchy/news/answers/LANs/big-lan-fq
`comp.security.firewalls` 新闻组有一个常见问题解答 (FAQ)，位于：
http://www.clark.net/pub/mjr
ftp://ftp.greatcircle.com/pub/firewalls/
还有一个防火墙邮件列表，通过 mailto:MajordoGreatCircle.com 服务，存档于 ftp://ftp.greatcircle.com/pub/firewalls/archive/
Daniel K. Kim 构建了一个可搜索的 Check Point Firewall-1 存档网站（其他邮件列表也已归档）。
http://mags.securepoint.com/
- 6. 在 IOL 的训练页面可以找到大量的通信教程，该页面包含有关 TCP/IP、局域网技术、编程与管理手册等材料的链接。
http://www.iol.enh/training/index.html
《数据通信》杂志在其网站上提供了一系列技术教程集，涵盖了 ATM、IP、高速网络等主题。
http://www.data.com/Tutorials/
利兹大学 ATM 多媒体小组拥有一系列关于 ATM 的文章、链接等等。
http://www.scs.leeds.ac.uk/atm-mm/links.html
3COM 有一个包含一系列网络文章链接的页面。
http://www.3com.com/technology/tech_net/white_papers/index.html
- 7. 可以在此处找到 `comp.unix.programmer` 常见问题解答 (FAQ)：
http://www.erlestar.demon.com



`http://www.windowsnt.protocol.tcpip`

`ftp://rtfm.mit.edu/pub/`

- 8. `comp.public.win95.networking` 常见问题解答 (FAQ) 涵盖 TCP/IP、网络等主题，位于：

`http://www.erlestar.demon.com`

`ftp://rtfm.mit.edu/pub/`

- 9. `comp.public.win98.com.modem` 常见问题解答 (FAQ) 涵盖 TCP/IP、网络等主题，位于：

`http://www.erlestar.demon.com`

`ftp://rtfm.mit.edu/pub/`

- 10. `comp.public.win98.comm.dun` 常见问题解答 (FAQ) 涵盖 TCP/IP、网络等主题，位于：

`http://www.erlestar.demon.com`

`ftp://rtfm.mit.edu/pub/`

# 私有 IP 网络地址

为了控制路由开销的增长，互联网提供商从地址注册机构获取一段地址空间，然后根据每个客户的需求从该区块内向其分配地址。这一过程的结果是，通往许多客户的路由将被聚合，对于提供商而言将是单条路由 [RFC1518], [RFC1519]。为了使路由聚合生效，互联网提供商鼓励加入其网络的客户使用提供商的区块，从而对其计算机进行重新编号。这种鼓励在未来可能会变成一项要求。

考虑到目前互联网的规模及其增长率，假设一个机构仅仅通过从互联网注册机构获取全球唯一的 IP 地址，一旦连接互联网就能获得全网的连通性已是不现实的。相反，很有可能当该机构连接到全网时，需要更改所有公共主机（需要全网 IP 连通性的主机）的 IP 地址（重新编号），无论该机构最初使用的地址是否是全球唯一的。

为所有使用 TCP/IP 的主机分配全球唯一的地址一直是一种常做法。为了延长 IPv4 地址空间的寿命，地址注册机构要求的比以往任何时候都更合理的理由，这使得机构获取额外的地址空间变得更加困难 [RFC1466]。

使用 IP 的企业内部主机可以分为三类：

- 类别 1：不需要访问其他企业或整个互联网的主机；此类类别的主机可以使用在企业内无歧义但在企业之间可能存在歧义的 IP 地址。
- 类别 2：需要访问有限外部服务（例如：电子邮件、FTP、网络、远程登录）的主机，这些服务可以通过媒体网关（例如应用层网关）处理。对于此类类别中的许多主机，通过 IP 连通性进行无限制的外部访问可能是没有必要的，出于隐私/安全考虑甚至是不可取的。与第一类中的主机一样，此类主机可以使用在企业内无歧义但在企业之间可能存在歧义的 IP 地址。
- 类别 3：需要企业外网络层访问（通过 IP 连通性提供）的主机；最后一类的主机需要全球无歧义的 IP 地址。

我们将第一类和第二类的主机称为“私有”。我们将第三类的主机称为“公共”。

许多应用程序只需要企业内部的连通性，对于大多数内部主机不需要外部（企业外）连通性。在较大的企业中，通常很容易识别出大量使用 TCP/IP 但不需要企业外网络层连通的主机。

以下是一些可能不需要外部连通性的示例：

- 一个大型机场，其到达/离开显示器可以通过 TCP/IP 单独寻址。这些显示器极不可能从其他网络直接访问。
- 银行和零售连锁等大型机构正在切换到 TCP/IP 进行内部通信。大量的本地工作站（如收银机、ATM 机和办公岗位设备）很少需要这种连通性。
- 出于安全考虑，许多企业使用应用层网关将内部网络连接到互联网。内部网络通常无法直接访问互联网，因此互联网只能看到一个或多个网关。在这种情况下，内部网络可以使用非唯一的 IP 网络号。
- 内部网络上的路由器接口通常需要能够从企业外直接访问。

# 私有地址空间

互联网分配编号机构 (IANA) 为私有网络预留了以下三个 IP 地址空间区块：

| 10.0.0.0 - 10.255.255.255 | 10/8 前缀 |
| 172.16.0.0 - 172.31.255.255 | 172.16/12 前缀 |
| 192.168.0.0 - 192.168.255.255 | 192.168/16 前缀 |

我们将第一个区块称为“24 位区块”，第二个称为“20 位区块”，第三个称为“16 位”区块。也就是说，在 CIDR 表示法之前，第一个区块仅仅是一个 A 类网络号，而第二个区块是 16 个连续的 B 类网络号集合，第三个区块是 256 个连续的 C 类网络号集合。

决定使用本文定义的地址空间之外 IP 地址的企业可以无需与 IANA 或互联网注册机构进行任何协调。此私有地址空间内的地址空间在企业内部是唯一的，或者在选择在此空间上协作的企业范围内是唯一的，以便它们可以在自己的私有网上相互通信。

与之前，任何任何全球唯一地址的企业都被要求从互联网注册机构获取此类地址。请求外部连通性 IP 地址的企业永远不会被分配来自上述定义区块的地址。

为了使用私有地址空间，企业需要确定哪些主机在可预见的不需要企业外的网络连通性并可以归类为私有。私有主机可以与企业内部的所有主机（包括公共和私有）通信。然而，它们无法与企业外的任何主机建立 IP 连通性。虽然没有外部（企业外）IP 连通性，私有主机仍然可以通过媒体网关（例如应用层网关）访问外部服务。

所有其他主机将是公共的，并使用全球唯一的地址空间。

## 私有 IP 地址

通过开发和部署有助于重编号的工具（例如动态主机配置协议 (DHCP)），可以减轻重编号的成本。在决定是否使用私有地址时，我们建议咨询计算和软件供应商关于此类工具的可用性。另一个独立的 IETF 工作（PIER 工作组）正在对重编号的节点和程序进行完整的文档编制。

## 运行考虑

一种可能的策略是先设计网络的私有部分，并对所有内部链路使用私有地址空间。然后在需要的地方规划公共子网，并设计外部连接。

这种设计不需要永久固定。如果以后有一组或多个主机需要更改其状态（从私有变为公有，或反之），可以通过仅对涉及的主机进行重编号，并在需要时更改物理连接来实现。在可以预见到此类更改的地方（如机房等），建议为公共子网和私有子网配置独立的介质。为了避免严重的网络中断，建议将具有相似连接需求的主机分组在自己的子网中。

如果可以设计出合适的子网方案并获得相关设备的支持，建议使用 24 位块（A 类网络）的私有地址空间，并制定具有良好增长路径的地址计划。如果子网划分有问题，可以使用 16 位块（C 类网络）或 20 位块（B 类网络）的私有地址空间。

人们可能会在同一个物理介质上同时使用公有和私有地址。虽然这是可能的，但这种设计存在陷阱（注意，这些陷阱与使用私有地址无关，而是由于在公共数据链路层子网络上存在多个 IP 子网导致的）。我们建议在此领域操作时保持谨慎。

强烈建议将连接企业与外部网络的路由器在链路的两端都设置适当的数据包和路由过滤器，以防止数据包和路由信息的泄露。企业还应该从入站路由信息中过滤任何私有网络，以保护自己免受可能出现的模糊路由情况（如果指向私有地址空间的路由指向了企业外部）。

两个协调了各自地址空间的站点可以通过公共网络进行通信。要实现这一点，它们必须在公共网络的边界使用某种封装方法，以保持其私有地址的私有性。

## 附录 D：TCP/IP 文档

如果两个（或多个）组织遵循本文规定的地址分配，并在以后希望彼此建立 IP 连接，那么存在违反地址唯一性的风险。为了将风险降至最低，强烈建议使用私有 IP 地址的企业在为其内部分配子块时，从预留的私有地址池中随机选择。

如果企业使用私有地址空间，或私有与公有地址空间的混合，那么该企业的 DNS 客户端不应看到企业使用的私有地址空间中的地址，因为这些地址是模糊的。确保此点的的一种方法是为每个包含公有和私有托管主机的 DNS 区域运行两个权威服务器。其中一个服务器从企业的地址空间可见，且仅包含可从公有地址访问的地址子集。另一个服务器仅可从私有网络访问，并包含完整数据集，包括私有地址以及私有网络可以访问的任何公有地址。为了确保一致性，两台服务器都应该根据相同的数据进行配置，其中公共可见区域仅包含过滤后的版本。提供这些功能具有某种程度的额外复杂性。

## 6. 安全考虑

本备忘录未涉及安全问题。

## 7. 结论

通过上述方案，许多大型企业将只需要全球唯一 IP 地址空间中相对较小的一块地址。整个互联网受益于全球唯一地址空间的节省，这将有效延长 IP 地址空间的寿命。企业则受益于相对较大的私有地址空间所提供的灵活性。然而，使用私有地址可能导致企业随着连接需求随时间的变化，需要对其部分或全部企业网络进行重编号。

## 8. 致谢



我们感谢 Tony Bates (MCI), Jordan Becker (ANS), Hans-Werner Braun (SDC), Ross Callahan (BayNetworks), John Curran (BBN Planet), Vince Fuller (BBN Planet), Tony Li (Cisco Systems), Anne Lord (RIPE NCC), Milo Medan (NSI), Martin Terpstra (BayNetworks), Geza Turchanyi (RIPE NCC), Christophe Wolflegel (Pasteur Institute), Anne Linton (connect.com), Brian Carpenter (CERN), Randy Bush (PSG), Erik Fair (Apple), Dave Crocker (Branden Consulting), Tom Kessler (SGI), Dave Piscatello (Core Competence), Matt Crawford (FNAL), Michael Patton (BBN) 以及 Paul Pixie (Internet Software Consortium) 的评审和建设性意见。

## 9. 参考文献

- [RFC1466] Gerich, E., "Guidelines for Management of IP Address Space", RFC 1466, Merit Network, Inc., May 1993.
- [RFC1518] Rekhter, Y., and T. Li, "An Architecture for IP Address Allocation with CIDR", RFC 1518, September 1993.
- [RFC1519] Fuller, V., Li, T., Yu, J., and K Varadhan, "Classless Inter-Domain Routing (CIDR): an Address Assignment and Aggregation Strategy", RFC 1519, September 1993.

## 10. 作者地址

Yakov Rekhter

Cisco systems

170 West West

San Jose, CA

Phone: 408-554-9512

Mail: yakov@cisco.com

# 386

# 索引

- 数据库, 77–80
  - 选择, 78–79
  - 商业数据库, 77
  - 连接, 79
  - 创建 (Create), 77
  - 容错性, 78
  - 热备用, 79
  - 锁定, 79
  - 开源数据库, 78
  - 表锁, 79
  - 事务备份, 77
  - 使用, 78
  - Windows 数据库, 78
- 邮件服务器, 45–46
  - 协作邮件, 46
  - 互联网服务器, 45–46
  - 标准, 44
- 嵌入到链接的, 65
- 紧急救援磁盘, 15
- 模拟器, 23–98
  - DOS, 29
  - DOSEmu, 29
  - FreeDOS, 29
  - 免费软件 (FreeWare), 37
  - VMware, 31–34
  - 优点, 33
  - 配置, 32–33
  - 安装, 31–33
  - 已知问题, 34
  - 调优, 34
- Fenris 在 跟踪系统 (Loki), 82
- 文件系统, 1–3
- 金融程序, 70–72
  - GnuCas, 70–72
  - Microsoft Money, 70
  - Moneyendance, 71
  - X-Accountant, 71
- FIPS, 12–25
  - 定义, 12
  - 限制, 12–13
  - 特殊情况, 15
  - 使用, 13–14
- FlashPlayer, 43
- Freespt, 49
- 数据接口格式 (DIF), 64, 70
- DB, 2, 77
- DCOM, 42
- 磁盘碎片整理 (defrag), 10
- 分隔符文本, 64
- 去碎片化器 (demonoriser), 41–42
- 桌面:
  - 配置, 89–90
  - 切换, 88
- DHCP 设置, 124–31
- 数字证书, 183
- DirectX, 8
- 磁盘管理员, 16
- 磁盘压缩程序与 FIPS
  - FreeDOS, 29
  - 免费软件 (FreeWare), 37
  - 前端扩展 (Front Extensions), 45
  - FSDEXT2, 21
- 为分区添加分区 (stab), 27–28
- FTP, 52, 54
- FTP 服务器
  - 为 Linux 设置, 175–76
  - 为 Windows 设置, 176–77
- 磁盘错误代码, 88
- 磁盘分区:
  - 现有硬盘, 10–18
  - 独立分区, 9–10
- DJVu, 43
- DMOS, 26–97
  - 选项类型, 26
  - 相关问题, 27
- DNS (域名服务), 117
- DNS 嗅探, 179
- Gameboy, 65
  - Geamas, 81–84
  - 经典游戏, 85
  - Gameboy, 85
  - 游戏服务器和额外物品, 84–85
  - id Software, 83
  - Loki, 81–83
  - 多街机模拟器 (MAME), 85
  - Quake 服务器, 85
  - 幻城竞技场 (UT), 83–85
  - XAME, 85
- 网关, NFS, 66–67
- DOSEmu, 27, 29
- DoubleSpace, 13, 15
- Double Space, 26
- 绘画程序, 73
- DR-ROS, 29
- 驱动器空间, 26, 27
- 双启动与 LILO, 9–10
- Gibson 研究公司 (Gibson Research Corporation), 65
- Gig, 43
- GI GL, 183
- Gnome Office, 61, 75
- Gnome-PIM, 61
- GnuCas, 70–72
  - 特性, 71–72
- Gnu 图像处理程序 (GIMP), 61, 72–74

# E

- Efnet, 51
- Eggrop, 51
- 电子邮件, 44–46
  - 邮件客户端, 44–55

# F

- FAT32, 1–2
- FATED, 1
- fdisk, 12
- WINE, 65
- 方程, 65
- 处账户, 2
- Exchange 服务器, 45–96
- 现有硬盘分区, 10–18
- 现有分区调整大小, 12
- Explore2f, 21–23
  - 创建选项, 23
  - 导出文件/导出为文本选项, 23
  - 特性支持, 22
  - 未来版本特性, 22
  - 导入文件选项, 23
  - 在 ext2 分区上操作文件, 22
  - 属性选项, 23
  - 重命名与删除选项, 23
  - 视图选项, 23
- Ext2ft 驱动, 23–24
- ext2* cools, 19
- 可扩展标记语言 (XML), 38, 64
- Ext/ext3, 3
- 眼睛之 (EOE), 61

# 387

- GNU 网络模型环境 (GOME), 87, 90
- 图形程序, 72–74, 72–77
  - Adobe Photoshop, 61, 72, 74
  - Blender, 73
  - Corel, 73, 74
  - 绘画工具, 73
  - 图像处理程序 (GIMP), 72, 72–74
  - 图形转换, 74
  - ImageMagick, 7
  - 照片编辑器, 72
  - 渲染工具, 73
  - Visio, 73
- 访客账户, 2
- Phoenix 自适应防火墙, 55
- 端口入口 (Psionic), 55–56
- 安全 Shell (SSH), 54
- Tripwire, 55
- Zone Alarm, 55

# K

- KDE (桌面环境), 61, 87, 89–93
- Kerberos, 183
- KFM, 43
- koffice, 75

# L

- LGPL (较小通用公共许可证), 37
- 轻级目录访问 (AD), 46
- LILO 程序, 5–6, 16–19
  - 启动, 9–10
  - Linux, 51
    - 桌面, 87–93
    - 隐藏系统, 2
- HotSync, 59



# M

- Hummingbird NFS 网关, 167
- Mime (多媒体接口), 44–45
- 宏，导出, 65
- 邮件客户端, 44–55
  - 邮件服务器, 45–46
    - 协作邮件, 46
    - 互联网服务器, 45–46
    - 中间邮件, 179, 183
- Mesa-Beta, 82–83
- Microsoft Exchange, 39, 45–46
- Microsoft Money, 70
- Microsoft Network (MSN), 51
- Microsoft Office, 39, 57
  - 使用 Star Office, 66–69
  - 使用 Web, 41–42
- Microsoft Outlook, 39, 45–46
- Microsoft Windows, 39
- 多街机模拟器 (MAME), 85
- MSQL, 77, 80
- Norton 系统 Commander, 1

# O

- ODBC, 40, 79–80
- 在线端口, 53
- OnTrack, 13
- OpenAI (Loki), 82
- 开放数据库连接 (ODBC) 驱动程序, 40
- OpenGL, 83, 183
- OpenLink Software, 80
- 开源 (Hewlett Packet), 46
- 开源浏览器, 43
- 开源办公, 60–61
- Opera, 43
- Oracle, 77
- 所有者系统内容, 2

# R

- RAR 压缩包, 23
- RCF82, 44
- 只读文件属性, 1
- Real Networks, 47
- 产生内容, 47
- Real Player, 43–48
- Real Server, 47
- 测试打印机, 151–53
- 设置 Windows NT 服务器, 123–34
- 独立式, 123
- scandisk, 10,23
- SDL JPEG 库 (Liboki), 82
- SDL MPEG Player, 43

# 388

- UMDSOS, 7–8
- Windows NT 引导加载程序, 16–18
- X-Windows, 05–96
- 网络类, 116
- TCP/IP, 116–17
- NFS (网络文件服务), 118
- Access NFS 网关, 167
- 网关, 166
- hand软 masters, 106
- 配置桌面, 89–90
- 切换桌面, 88
- 主题, 90–93
- 桌面, 90–93
- 导出, 64–65
- 读取/写入, 63
- 连接 Windows, 135
- 现有驱动器分区, 18–24
- 分区, 18
- 文件系统, 3
- 导入/导出 Microsoft Office 文件, 66
- 导入/导出检查点, 69–70
- 分区, 3–5
- 分区, 1
- DALNet, 51
- 电子邮件, 44–46
- FrontPage 扩展, 41
- Jabber 打印机, 51
- Java, 43
- JavaScript, 43
- Java VNC 查看器, 112
- JetDirect 打印机 (Hewlett Packard), 152
- 互联网工程任务组 (IETF), 39
- Internet Explorer (IE), 42–43, 61
- 互联网邮件服务器, 45
- 互联网邮件传输 (MTA), 45–46
- 互联网中继聊天 (IRC), 50–51
- 互联网安全, 52–56
- IP 地址, 117
- IP 源路由, 179
- IP 欺骗, 179
- IRC 机器人, 51
- 互联网应用, 39–56
- 即时消息, 59
- 即时消息, 51
- 文件属性, 25
- 分区, 15–26
- 权限, 2
- 写入, 20
- 查看, 3
- 名字命名, 243
- 分区命名, 3–5
- NIS, 115–16
  - 使用 Linux, 25–28
  - 使用 Linux 访问驱动器, 25
  - 问题, 174
  - 设置 Linux, 170
- 服务器, 174
- nmap, 53
- mbdi, 235
- 说明, 232
- 文件, 233–34
- 摘要, 231
- 播放器, 45–50
- Shoutcast, 49
- MPEGTV, 140
- MSTP, 45
- NTFS (网络文件系统), 1–2
- 使用启动时加载, 10
- 在 Linux 上设置, 59–63
- 在 Windows 上设置, 19–24
- 在 Linux 上设置, 59–63
- 在 Windows NT 上设置, 164–65
- 优化, 163–64
- Reflections NFS 网关, 167
- 安全, 167
- samba (7), 235–377
  - 作者, 237
  - 可用性
  - 组件, 236
  - 说明,
  - 向网络添加 Samba 服务器, 132–33
  - 基础, 119–121
  - 定义, 118
  - 文档, 189–228
  - FAS, 195–218
  - GNU 数字, 19–95
  - 历史, 119
  - 如何使用, 120–121
  - 页面, 229–345
- 数据包嗅探, 179
- 分区:
  - 现有硬盘, 10–18
  - 调整大小, 12

# 390

# 索引

- 命令行选项, 136–138
- 命令, 139–144
- smb.conf(5), 238–316
- 作者, 316
- 文件格式, 238
- 全局参数, 244–245
- 命名, 243
- 参数描述, 246–316
- 管理用户, 246
- 备用权限, 247
- 发布为, 247
- 通告版本, 248
- 自动操作系统服务, 248
- 可用, 248
- 仅绑定索引, 248–49
- 阻塞锁, 249
- 可视, 249
- 可视列表, 249
- 大写敏感, 249
- 大写签名, 249
- 更改通知, 249–50
- 字符集, 250
- 客户端代码页, 250–51
- 编码, 251–52
- 注释, 252
- 配置文件, 252
- 复制, 252
- 创建掩码, 253
- 空闲时间, 253
- 调试级别, 253
- 默认, 253
- 默认情况, 253
- 默认验证服务, 254
- 删除只读, 254
- 删除被否决的文件, 254–55
- dnsy hosts, 255
- dfree 命令, 255
- 目录, 255
- 目录映射, 255–56
- 目录模式, 256
- dns 代理, 256
- 域管理员组, 256
- 域管理员用户, 256
- 域控制器, 257
- 域组映射, 257–58
- 域组, 258
- 域宾客用户, 258
- 域宾客用户, 258
- 域登录, 258
- 域主, 259
- 域用户, 259–60
- 不计数, 260
- dos 文件解析, 260–61
- dos 文件, 261
- 加密密码, 261
- 执行, 261
- 伪造目录创建时间, 261–62
- 伪锁, 262
- 遵循符号链接, 262
- 强制创建模式, 262
- 强制目录模式, 263
- 强制组, 263
- 强制用户, 263
- 类型, 获取缓存, 264
- 组帐户, 264
- 宾客允许, 264
- 仅宾客, 264
- 隐藏文件, 264
- 主目录映射, 265
- hosts 允许, 265
- hosts 拒绝, 265
- hosts 允许, 266
- 包含, 266
- 接口, 266
- 无效用户, 266
- 保持活动, 267
- 内核选项, 267
- dip 绑定为, 267
- dip 密码文件, 268
- dip 端口, 268
- dip-server, 268
- dip 后缀, 268
- Im 登录, 268
- Im 级别, 269
- 加载打印机, 269
- 本地映射组, 269–70
- 本地主, 270
- 锁目录, 270
- 锁定目录, 270
- 锁定, 271
- 日志类型, 271
- 登录驱动器, 271
- 登录主目录, 271
- 登录路径, 272
- 登录脚本, 272
- lppause 命令, 273
- lpq 缓存时间, 273
- lpq 命令, 273–74
- lpr 命令, 274
- lpr 输入, 274–75
- 机器处理器超时, 275
- magic 输出, 275



# 索引

- `magic` 脚本, 275
- 混淆大小, 275
- 混淆映射, 276
- 混淆名称, 276–77
- 混淆栈, 277
- 混淆字符, 277
- 映射存档, 277
- 映射到宾客, 277
- 映射系统, 278
- 最大连接数, 278–79
- 最大大小限制, 279
- 最大复用, 279
- 最大打开文件数, 279
- 最大数据包, 279
- 最大 ttl, 280
- 最大窗口, 280
- 最大传输, 280
- `get`命令, 280–81
- 最小打印空间, 281
- 最小窗口, 281
- 名称解析顺序, 281–82
- netbios 别名, 282
- netbios 名称, 282
- netbiosider, 282
- ntp 管道支持, 283
- nt smb 支持, 283
- 空路径, 283
- ole 锁定兼容性, 283
- 仅宾客, 283
- 仅用户, 283–84
- oplock, 284
- os 级别, 284
- 数据包大小, 284
- 恐慌动作, 284
- 密码聊天, 284–85
- 密码聊天调试, 285
- 密码程序, 285
- 密码级别, 286
- 密码服务器, 286–87
- path-ext, 287
- postscript, 288
- preex, 288
- 首选方法, 288–89
- 预加载, 289
- 保留大小写, 289
- 可打印的, 290
- printcap 名称, 290–91
- print 绑定, 289–90
- 打印机, 291
- 打印机设备, 291
- 打印机驱动程序, 291–92
- 打印机位置, 292
- 打印, 292
- 协议, 292–93
- 公共, 293
- 队列暂停, 293
- 队列命令, 293
- 读取 hmps, 294
- 仅读取, 294
- 预测, 294
- 原始, 294
- 大小, 294–95
- 远程通告, 295
- 远程浏览, 295–96
- 验证, 296
- 根目录, 296
- 根 parce, 297
- 根 pretex, 297
- 安全域, 297
- 安全用户, 298–99
- 字符串, 299
- 共享 mem, 300
- 共享模式, 300
- 短情况, 300
- smb 文件, 301
- smbtun, 301
- socket 地址, 301
- socket 选项, 301–302
- sl, 302
- sl ca cert, 302
- sl ca file, 303
- sl ciphers, 303
- sl client cert, 303
- 兼容性, 303
- sl hosts, 304
- sl hosts resign, 304
- sl require client, 304–5
- sl require server, 305
- ssl server cert, 305
- ssl server key, 305
- ssl version, 305–6
- stat cache, 306
- stat size, 306
- 状态, 306
- 锁定, 306–7
- strict sot, 307
- sync always, 307
- syslog 仅, 307
- 时间偏移, 307
- 时间服务器, 308
- 时间戳, 308
- unix password sync, 308
- unix realm, 308
- 更新加密, 308–9
- 用户, 309
- 使用, 309
- 用户名, 309
- 用户级别, 310
- 用户名映射, 310–11
- 用户, 309
- 有效 chars, 312
- valid comes, 312–13
- 否决文件, 313
- 否决 optic 文件, 313
- 卷, 314
- 宽行, 314
- wins 代理, 314
- wins 服务器, 314
- wins 支持, 314
- 工作组, 314
- 可写, 315
- 可写, 315
- 列表, 315
- 写入 ok, 315
- 写入 wis, 315
- 参数, 242
- 章节, 239
- 服务参数, 245–46
- 特殊 womans, 240
- 摘要, 238
- 用户密码/验证, 243–44
- 变量替换, 242–43
- smbd, 327–34
- 作者, 334
- 描述, 327–28
- 诊断, 333
- 环境变量, 330–33
- 安装, 331
- 局限性, 330
- 选项, 328–29
- 打印机, 330–31
- 作为守护进程, 331
- 非请求, 332
- 信号, 333
- 摘要, 327
- smbfs, 135, 145–46
- smbpasswd (5), 334–37
- 作者, 337
- 描述, 334
- 文件格式, 335–36
- 注释, 336
- 摘要, 334
- smbpasswd (8), 337–42
- 作者, 341–42
- 描述, 338
- 注释, 341
- 选项, 338–41
- 摘要, 337
- smbprint, 135, 144–5
- smb (Server Message Block), 119
- smb.status, 342–43
- 作者, 343
- 描述, 342
- 选项, 342
- 摘要, 342
- smbtar, 135, 144
- smbwrapper,
- SMTP (简单邮件传输协议), 44
- SOCKS, 113–14
- SQL Server, 40
- SQL Server (Microsoft), 77, 79
- Stacker, 15, 25, 26
- Star Office, 42, 45, 59, 61
- Star Office, 使用微软文档, 66–69
- 流媒体音频, 48–50
- 流媒体媒体, 46–50
- 流媒体视频, 47–48
- Real Networks, 47
- Real Server, 47
- 结构查询语言 (SQL) 标准 (ISO), 78
- Sun Microsystems, 60
- SuSE Linux, 58
- Sybase, 70
- 系统文件, 8
- Windows 9x, 和 PC 游戏, 81
- Windows 98:6–7, 启动 Linux, 5–6
- Windows: 磁盘管理, 4, 分区, 3–5, 分区, 1
- Windows 浏览器, 42–43
- Windows Media Player, 39, 48
- Windows NT, 引导加载程序, 16–18
- WINE, 30, 58
- WINS (Windows 内部名称服务器), 117
- WordArt, 265
- WordPerfect Office (核心), 57–59
- Linux 版 WordPerfect 8, 59
- Wabi, 30
- Web 网站, 63–61
- Web 服务器, 39–40
- V11, 52, 54, 82, 87, 182, 186
- X11R6.3 远程执行, 43
- X-Accountant, 71
- Xaudio, 50
- x-chat, 50
- XMEAME, 85
- xms, 44
- Van Dyke Technologies 网站, 178
- VScript, 43
- 虚拟规则, 导出, 65
- 虚拟网络编译 (VNC), 99–114
- 组件, 100
- 定义, 99
- Java VNC 查看器, 112
- 优化, 112
- 安全, 113–14
- 安全 Shell (SSH), 113
- SOCKETS, 113–14
- Arachne, 22
- 跨平台兼容浏览器, 42–44
- K'M, 43
- Lynx, 42
- Mozilla, 43
- 开源浏览器, 43
- 插件, 33–44
- Star Office, 42
- Windows 浏览器, 42–43
- Active Server Pages (ASP), 40
- PHP, 40
- WinLin, 38
- Winamp, 49
- Windows 3.1, 和 FIPS, 15
- 插件, 44
- XVIEW, 43
- X-Windows, 96
- 在 Linux, 95–96
- 在 Linux, 96
- Linux 下 X-Windows, 96
- Yahoo, 和即时通讯, 51
- Young, Bob, 81
- Zone Alarm, 55



# 来自您熟悉并信赖的专家提供的 InformIT 解决方案

免费文章 电子书 专家问答 培训 职业中心 下载 我的InformIT

登录 注册 关于 InformIT

## 主题

操作系统 网页开发 编程 网络 认证及更多...

## www.informit.com

- 免费、深度的文章和补充资料
- 在您需要的时候掌握您所需的技能
- 从行业领先的书籍、电子书和培训中进行选择——来自专家的现场教学或
- 在您需要时获取答案 - InformIT 丰富的库
- 获得行业认证并提升您的职业

## 专家访问

![](img/a1ad58e4259f15e8b2826ecf57a28362_416_0.png)

免费内容

## 立即访问 InformIT 获取来自 PH PTR 的精彩内容

Prentice Hall 和 InformIT 是 Pearson plc 的商标 / 版权所有 © 2000 Pearson

## Prentice Hall: 专业技术参考

上页 向后 刷新 首页 搜索指南 图像 打印 安全 停止 PH PTR

`://www.phptr.com/`

## PRENTICE HALL

# 专业技术参考

为今天的专业人士提供明天的解决方案。

## 与 PH PTR 在线版保持同步！

我们致力于处于专业计算机科学和工程领域的最前沿。当您访问 `www.phptr.com` 时，可以发现以下内容：

- 特别领域：提供我们最新的书籍、丛书、软件、月度特色、相关链接和其他帮助您完成工作的有用信息。
- 优惠、优惠、优惠！来到我们的促销板块，获取我们的零售商独家提供的最新特价。
- 需要寻找书店吗？很可能您附近就有一家销售多种 PTR 书籍的书店。在 `www.phptr.com` 查找您附近的 Magnet 书店。
- PH PTR 有什么新品？我们不仅为专业社区出版书籍，我们也是该社区的一员。查看我们的会议日程，加入作者聊天，获取有关您感兴趣的话题的最新评论和新闻稿。

立即订阅！加入 PH PTR 的每月电子邮件通讯邮件！

想了解您感兴趣领域的最新动态吗？在我们的网站上选择一个目标类别，我们将向您通报感兴趣领域内的最新 PH PTR 产品、作者活动、评论和会议。

访问我们的邮箱箱立即订阅！`http://www.phptr.com/mail_lists`

![](img/a1ad58e4259f15e8b2826ecf57a28362_417_0.png)

## Forsyth 图书馆

海西斯州立大学

## 集成 Linux 和 Windows

每个 Linux/Windows 系统管理员的完整解决方案指南！

MIKE MCCCUNE

在同一环境中运行 Linux 和 Windows 吗？这就是您一直在寻找的全面、实时的解决方案。

在《集成 Linux 和 Windows》中，顶级顾问 Mike McCune 为 Linux/Windows 系统管理员最经常遇到的问题提供了数百种解决方案。McCune 关注现实企业面临的关键互操作性问题：网络、程序/数据兼容性、双启动系统等。您将发现具体如何做到：

- 使用 Samba 和 Windows 为工作站提供高性能、低成本的文件和业务
- 比较并实施最佳 Linux/Windows 连接技术：NFS、FTP、远程命令、安全壳 (`ssh`)、telnet 等
- 在 Microsoft Office® 和 Linux 版 StarOffice® 之间提供可靠的数据交换
- 通过 ODBC 提供高性能跨平台数据库访问
- 充分利用独立平台基于浏览器的应用程序
- 在同一工作站上管理 Linux 和 Windows：引导管理器、分区、压缩驱动器、文件系统等

如果您同时运行 Linux 和 Windows，McCune 将对您所有的集成方案提供诚实且客观的解释，以及在其他任何地方都找不到的现实、经过验证的解决方案。这本书将帮助您保持用户满意、控制成本并保持您的理智！

## 关于作者

MIKE McCUNE 是一位位于芝加哥的顾问，专门负责运行 Windows、Linux 和 NetWare 的 PC 网络和工作站。自1990年以来，他一直为 IBM、惠尔士-Packard、ITT 和通用在内的客户提供咨询服务。

`$39.99` 美元 | `$60.00` 加加元

Prentice Hall

Upper Saddle River, NJ

`www.phpptr.com`

![](img/a1ad58e4259f15e8b2826ecf57a28362_419_0.png)
