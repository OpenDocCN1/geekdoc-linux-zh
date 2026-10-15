
- http://www.schirmacher.de/arne/dvgrab/dvgrab_features_e.html—用于 Linux 的数字视频抓取软件（通过 Firewire）。
- http://www.elks.ecs.soton.ac.uk/—适用于 x286 及以下 CPU 的 ELKS Linux 主页。
- http://open-projects.linuxcare.org/BBC/**—启动名片（Bootable Business Card）主页，一个 50MB 的压缩 Linux 发行版，提供数百个网络客户端、实时 X 会话、浏览、PDA 备份、无线网络、救援会话和文件恢复。
- http://www.oyote.com—提供防火墙和 VPN 服务的紧凑 Linux 发行版主页；基于软盘的发行版在旧 PC 上运行良好，且不需要硬盘。
- http://www.freeco.org/—基于软盘的路由器解决方案主页，适用于 386 PC，仅需 6MB RAM，并提供桥接、防火墙、IP 伪装、DNS、DHCP、Web、telnet、打印、时间和远程访问功能。
- http://www.bitwizard.nl/sig11/—关于 Linux Signal 11 错误某些原因的详细概述。
- http://www.gnu.org/software/parted/parted.html#introduction—GNU parted 工具主页。
- http://www.linux.org/vendors/systems.html—可以在此处检查附近是否有销售在 PC、笔记本电脑、服务器或硬盘上预装了 Linux 的供应商。

# 第 3 章

## 本章内容

### 安装 Red Hat Linux

- 如何安装 Red Hat
- 逐步安装步骤
- 登录与关机
- 参考资料

在本章中，你将学习如何使用你在 Kickstart Configurator 中概述并保存在 `ks.cfg` 中的规范来安装 Red Hat Linux。

下一步是将你的新的 `ks.cfg` 复制到使用 Red Hat 启动软盘镜像创建的启动磁盘（在第一张 Red Hat Linux CD-ROM 的 `images` 目录下找到）。在 Linux 中，你可以通过 `mount` 和 `cp` 命令完成此操作。例如，取你的 Red Hat 启动磁盘（根据第 3 章“制作启动软盘”节中的说明创建），将其插入 PC，然后以 root 身份像如下所示使用 `mount` 命令：

```bash
mount /mnt floppy
```

如果 Red Hat 自动挂载了你的软盘，你将收到错误消息，提示 `/dev/fd0` 已挂载。此时你只需按照如下所示将 `ks.cfg` 文件复制到软盘：

```bash
cp ks.cfg
```

你可以像这样使用 `ls` 命令验证软盘的内容：

```bash
ls /mnt/floppy
boot.msg general.msg inititrd.img ks.cfg ldllinux.sys
options.msg param.msg rescue.msg snake.msg splash.lss
syslinux.cfg syslinux.png vmlinuz
```

然后像如下所示使用 `umount` 命令卸载软盘：

```bash
umount /mnt/floppy
```

取出磁盘。它现在已准备好可以使用。当你使用该磁盘启动 PC 时，启动后，告知安装启动镜像你想执行 kickstart 安装，如下所示：

```bash
linux ks=floppy
```

安装程序随后将使用你在 Kickstart Configurator 中概述并保存在 `ks.cfg` 中的规范来安装 Red Hat Linux。

### 准备安装

规划自定义系统的一部分是根据你计划如何使用 Red Hat，以及如之前提到的，现有硬件的能力来实施分区策略。例如，如果你计划托管成千上万个图形图像或音频文件，你需要多少存储空间？如果你计划备份此集合，是使用磁带驱动器还是简单地将文件复制到另一块硬盘？

如果你计划为公司或企业级环境进行安装，还必须考虑系统未来的扩展或演进。你希望构建一个灵活的系统，能够随着你的业务及其系统需求而演进。

了解 Linux 如何在你的硬盘上分配软件涉及到了解 Red Hat Linux 如何组织其文件系统，或者在存储介质上的目录布局。这些知识将帮助你充分利用硬盘空间；在某些情况下（例如，计划通过 NFS 或其他手段监控用户目录），它可以帮助防止数据丢失、增加安全性并适应未来需求。创建一个出色的系统，你将成为信息服务部门的英雄。

规划最佳分区方案，请研究并了解这些问题的答案：

- 你的系统需要多少磁盘空间？
- 你预计磁盘空间需求在未来会显著增长吗？
- 系统将只启动 Red Hat Linux，还是你需要一个双启动系统？
- 有多少数据需要备份，哪种备份系统最有效？有关备份 Red Hat Linux 的更多信息，请参阅第 11 章“备份、恢复与重置”。

## CD-ROM 安装启动

要从书中附带的 CD 安装 Red Hat Linux，你至少需要一个 Pentium 类 CPU、650MB 硬盘和 64MB RAM。如果使用 Red Hat 的图形化安装程序，至少需要 128MB。一个 10GB 的硬盘可以轻松容纳整个 Red Hat 发行版，留出 5GB 以上的空间给其他数据。

要开始安装，将 PC 的 BIOS 设置为从 CD-ROM 启动。接下来，插入第一个 CD-ROM 并启动计算机。在第一个屏幕按回车，并按照后续对话框进行安装。

记住或记下系统的 root 密码。此外，即使你彻底测试了图形化安装的配置，也选择让 Red Hat 到文本登录（参见后文的“分步安装”）。你可以在完成安装、重启并登录后启动图形化会话。你可以随时设置 Red Hat 以后启动到图形登录（参阅第 6 章“窗口系统”查看如何操作）。

如果你有软驱驱动器，在安装期间创建一个启动盘（参见本章的“分步安装”部分）。最后，完成安装，从计算机中取出 CD-ROM 并重启。然后登录并享受 Red Hat Linux！

## 选择引导加载程序

你需要决定如何启动你的 Red Hat Linux 系统。例如，你可以使用默认的引导加载程序通用引导加载程序（称为 GRUB）或 Linux 加载程序（称为 LILO）从硬盘或软盘启动 Red Hat。

LILO 是一个通常安装在 IDE 硬盘的主引导记录 `MBR`、Linux 根分区或软盘上的引导加载程序。该加载程序（与其它引导加载程序一样）可以被用于在启动过程中将关键的内核参数传递给 Linux 内核。某些参数可能包括特殊的磁盘几何设置或指定额外的网络接口。你可以使用其他引导加载程序（如 GRUB）来支持特殊操作，例如从只读存储器 `ROM` 或包含引导加载器代码的闪存芯片启动。并非所有 PC 硬件 BIOS 都支持通过通用总线 `USB` 可移动介质或软盘通过网络启动。

GRUB 加载程序适用于所有 BSD 变体和许多专有操作系统。此实用程序支持菜单、命令行、已安装的 RAM 检测以及无盘启动和网络启动。

另一方面，LILO 的历史要久得多，对于资深 Linux 用户来说可能更加熟悉。两种引导加载程序都提供密码保护，但根据 Red Hat 公司的说法，LILO 的密码保护必须在安装之前配置，且 Red Hat Linux 的未来版本可能不支持 LILO。

> Red Hat 的 `mkbootdisk` 命令可以创建软盘和 CD-ROM 启动介质。要这样做，请使用 Linux 内核发布版本（通过 `uname -r` 返回）和指定的设备。例如，要创建一个软盘，使用如下命令：

```
## mkbootdisk --dev/fd0 `uname -r`
```

要创建 CD-ROM 启动镜像（必须刻录到空白的 CDR 或 CDRW 上），请使用带有 `-iso` 选项的命令：

```
## mkbootdisk --iso --device boot_cd.img `uname -r`
```

Red Hat Linux 还可以使用 `LOADLIN` 程序、指向内核的 DOS 路径以及 Linux 内核的位置从 DOS 会话启动，例如：

```
LOADLIN c:\KERNEL\VMLINUX root=/dev/hda2 ro
```

在此示例中，名为 `VMLINUX` 的内核被加载，并将第一个 IDE 硬盘的第二个主分区指定为 Red Hat Linux 系统的根 `/` 分区。

## 选择如何安装 Red Linux

> 注意
>
> 如果你发现 `LOADLIN` 无法启动 Linux 并提示内核大小过大，你可以使用 `make bimage` 构建一个较小的内核，或者重新构建一个少依赖内置功能、多依赖可加载模块的内核。更多信息请参阅第 24 章“内核与模块管理”。

在选择商业引导加载程序时，请权衡其功能和选项。良好的引导加载程序将支持你启动不同 Linux 内核的能力（以便更改系统特性或轻松适应新硬件）、密码保护以及自定义启动显示。如果你发现 `LOADLIN` 无法启动 Linux 并提示内核大小过大，你可以使用 `make bimage` 构建一个较小的内核，或者重新构建一个少依赖内置功能、多依赖可加载模块的内核。

（注：原文中存在多段重复的描述，此处已按指令要求完成翻译并保持逻辑一致）

## 选择如何安装 Red Hat Linux

表 3.1 中列出的大多数镜像都支持启动到安装程序。`pxboot` 目录包含一个支持名为 PXE 的远程启动协议的内核，该协议能够为仅限网络的 PC 启用或升级 Red Hat Linux。使用此软件需要一个配置恰当的 DHCP 服务器和受支持的 BIOS。虽然可能可以使用软盘，但 Red Hat 不支持这种方法。访问 http://www.compaq.com/products/servers/webpapers.html 并阅读 Compaq 题为 "Using Compaq ProLiant Servers with Red Hat Linux 7.1 to Configure a Boot Execution Environment (PXE)" 的论文，以了解使用 PXE 启动到安装程序的一种。访问 http://www.europe.redhat.com/documentation/mini-HOWTO/Remote-Boot.php3 了解如何使用旧版本的 Red Hat 设置启动环境。

> 提示
>
> 如果您电脑的 BIOS 支持从 USB 设备启动，您可以使用 USB 软盘启动到安装程序。如果您的电脑的 BIOS 支持，也可以从 IEEE-1394（火线线）CD-ROM 启动。

您可以使用 DOS 的 `RAWWRITE` 命令或 Linux 命令启动软盘。您需要一个或多个空白软盘。在启动 DOS 后像如下使用 `RAWWRITE` 命令：

```
dosutils\rawwrite
```

按照提示创建镜像，输入源文件名和目标驱动器（如 A 或 B）。要获取 RAWWRITE 最新版本的副本，请访问 http://www.tux.org/pub/dos/rawwrite/

在运行 Linux 时创建创建磁盘镜像，请使用 `dd` 命令。第一步是插入第一张 Red Hat Linux CD-ROM 并确保它已挂载：

| 文件系统 | 1k-块 | 可用空间 | 使用率% | 挂载点 |
| --- | --- | --- | --- | --- |
| `/dev/hda2` | 1871468 | 10410280 | 7353444 | 59% |
| `/dev/hda1` | 46636 | 13247 | 30981 | 30% | `/boot` |
| none | 120016 | 0 | 0% | `/dev/shm` |
| `/dev/cdrom` | 655808 | 655808 | | 100% | `/mnt/cdrom` |

此示例使用磁盘系统或 `dd` 命令来显示空闲硬盘空间以及当前挂载的设备和分区。如您所示，Red Hat CD-ROM 的内容位于 `/mnt/cdrom` 目录下。如果 CD-ROM 未挂载，请使用 `mount` 命令手动挂载 CD-ROM。您需要超级用户或 Linux root 才能操作此磁盘（详情请参见第 5 章“Linux 入门”，有关如何成为 root 的说明）：

```
## mount -t iso9660 /dev/cdrom /mnt/cdrom
```

## 第 3 章 安装 Red Hat Linux

您可以像如下使用 `convert` 配合 `copy` 或 `dd of=/dev`：

```
## dd if=/cdrom/images/nameofimage.img of=/dev/fd0
```

这将提取指定镜像文件（来自表 3.1）的内容并在 DOS 驱动器 A（由 `/dev/fd0` 表示）中创建一个磁盘镜像。如果您想使用已安装的辅助软盘，请使用 `/dev/fd1`。

> 提示
>
> 通过网络或外部 CD-ROM 驱动器使用 PCMIA 适配器安装的笔记本用户也应该创建 `pcmciadd.img` 磁盘镜像。

## 硬盘分区安装

安装 Red Hat 的另一种方法是使用 Linux 或 DOS 分区来启动 Red Hat Linux 安装或存放安装所需的软件。该分区必须足够大。分区必须足够大以启动 Red Hat Linux 安装或存放安装所需的软件。分区必须足够大。分区必须足够大。访问 http://www.compaq.com/products/servers/webpapers.html 并阅读 Compaq 题为的论文以了解使用 PXE 启动到安装程序的一种方法。访问 http://www.europe.redhat.com/documentation/mini-HOWTO/Remote-Boot.php3 了解如何使用旧版本的 Red Hat 设置启动环境。

## 使用网络安装

通过网络或外部 CD-ROM 驱动器使用 PCMIA 适配器安装的笔记本用户也应该创建 `pcmciadd.img` 磁盘镜像。

## 硬盘分区安装

安装 Red Hat 的另一种方法是使用 Linux 或 DOS 分区来启动 Red Hat Linux 安装或存放安装所需的软件。分区必须足够大。分区必须足够大以启动 Red Hat Linux 安装或存放安装所需的软件。分区必须足够大。

（此处重复部分）通过网络或外部 CD-ROM 驱动器使用 PCMIA 适配器安装的笔记本用户也应该创建 `pcmciadd.img` 磁盘镜像。

## 硬盘分区安装

（略）

## 使用网络安装

通过 FTP 准备 Red Hat 安装的一种方法是：

1. 在 FTP 服务器的目录下创建一个名为 `RedHat` 的目录。该目录将是 `var/ftp/pub`。
2. 在 `RedHat` 目录下创建名为 `base` 的目录和名为 `RPMS` 的目录。
3. 将 Red Hat 包含的所有 RPM 软件包复制或下载到 `pub/RedHat/RPMS` 目录。
4. 将所有原始文件（`comps`, `hlist`, `hlist2.img`, `hdstg1.img`, `netstg1.img`, `stage2.img`, `TRANS.TBL`）从第一个 Red Hat CD-ROM 的 `base` 目录复制到 `pub/RedHat/base` 目录。

从远程挂载的文件系统 `NFS` 安装 Red Hat 与从硬盘安装类似，但需要允许的 IP 地址或主机名。

使用 HTTP 安装 Red Hat，您需要服务器的主机名或 IP 地址，以及镜像路径。参见第 16 章“Apache 管理”以了解如何设置。

## 分步安装

本节提供了从 CD-ROM 进行基本分步安装的方法。此示例为作为通用服务器准备计算机，例如托管 FTP 站点、使用 Apache 的 Web 服务器或 SMB 服务。

在开始之前，请确保您的计算机没有连接到互联网。虽然可以使用 Red Hat 安装程序在安装期间设置网络保护，但最好在任何安装后检查系统设置（参见本章稍后的“防火墙和安全配置”）。

## 开始安装

要开始，插入第一张 Red Hat Linux CD-ROM 并重启电脑。您将首先看到一个具有多种启动选项的屏幕（图 3.1）。这些选项有：

- `<ENTER>` 使用图形界面启动安装。图形界面支持鼠标，并提供选择框和字段用于选择软件、配置选项和输入信息。
- `linux text` 使用图形文本界面启动安装。（这是我们将使用的选择。）

可以使用功能键循环浏览四个带有额外安装信息的帮助屏幕。在启动提示符处使用这些功能键跳转到描述不同安装选项和模式的屏幕。

## 逐步安装

- 按下 `F1` 返回到初始启动屏幕。
- 按下 `F3` 获取通用安装信息（本章接下来将描述）。
- 按下 `F4` 描述如何传递内核视频参数，用于配置视频硬件以支持在特定分辨率下进行图形安装（例如 800-600 像素）。
- 按下 `F5` 描述 Red Hat 的救援模式。

`F3` 屏幕列出了您可以在启动提示符处使用的若干选项，例如：

- `linux noprobe`——禁用系统硬件的探测。
- `linux mediacheck`——验证一个或多张 Red Hat 安装 CD-ROM 的完整性。
- `linux rescue`——引导到具有 root 提示符的单用户模式，禁用 X、多任务处理和网络；如果您需要重新配置 Red Hat 引导程序或从系统中恢复数据，可以使用此选项。
- `linux dd`——使用驱动磁盘（软磁盘镜像）以及可能的一个或多个内核参数（如 `linux mem=512m`）来启用某些硬件，如网卡。
- `linux askmethod`——提示要执行的安装类型，例如通过网络进行。
- `linux updates`——启动安装更新。
- `linux lowers`——使用 640x480 像素的图形显示进行安装，如果您的 PC 拥有较旧或性能较低的显示器，这可能会很有帮助。

`F4` 屏幕列出了可以在启动提示符处设置安装特定分辨率的选项。例如，可以通过在启动提示符处输入 `linux resolution=` 并配合如 `800x600` 等选项来实现。
