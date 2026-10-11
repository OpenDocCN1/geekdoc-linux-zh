
# 文件系统管理

本章向你介绍文件系统管理的概念。文件 system（目录布局）和文件系统（存储介质上文件处理的底层布局或结构）之间存在区别。文件系统管理包括将你的存储介质保持在最佳状态。它还涉及使用各种实用程序来修复、挂载、读取、擦除、清除、格式化或卸载介质。管理你的 Linux 文件系统包括归档和备份重要数据，运行计划维护任务以清理或删除冗余、无用的文件。管理系统资源还包括管理用户对存储的使用以及实施磁盘配额。

这些任务都是系统管理员工作的一部分。如果你是唯一使用该系统的人，那么猜猜看，你就是系统管理员！

Linux 是一个健壮、稳定的操作系统，因此你不必做很多工作。一些 Linux 发行版，如 SuSE PPC Linux，已设置为为你完成大部分工作。然而，不要轻视这项工作。你应该仍然了解 Linux 是如何工作的，以便在需要排除故障或修复系统时能够处理。

可能导致故障的最大错误之一是没有正确关机。始终使用 `shutdown` 命令重启或关闭计算机。如果未在正确卸载的情况下移除存储介质，可能会出现其他问题。不要在没有卸载其文件系统的情况下直接拔出 Zip 磁盘、可移动硬盘、PCMCIA 闪存卡或软盘。

Linux 能够识别并使用各种文件系统，如表 16.1 中列出的那样。在 Linux 会话期间你将主要使用的文件系统类型是 `ext2`、`nfs`、`iso9660`、`hfs`、`ufs` 和 `smbfs`，可能还有 `vfat`（以及 `mdos`）。这是因为你通常使用的是 Linux `ext2` 文件系统（交换分区在会话期间自动挂载，在文件系统中不可见）。如果你挂载远程目录，可以轻松地使用 NFS 服务来实现。如果你使用 CD-ROM，你很可能会使用 `iso9660` 格式进行挂载。要挂载 Mac OS 分区，你需要使用 `hfs`，这是标准而非扩展的 Mac OS 文件系统（Mac OS X 和 Linux 支持 `ufs`，但 Linux 尚不支持 HFS+）。如果挂载 DVD，请使用 `iso9660`。如果挂载远程 Windows 分区，请使用 Samba，它使用 `smbfs`。挂载和读取 DOS 软盘涉及使用 `vfat` 或 `mdos` 文件系统（很可能是 `vfat`）。

## 文件系统表

本节介绍 Linux 文件系统表的概念，该表在安装 Linux 时最初进行配置。

### 表 16.1 Linux 的文件系统

| 类型 | 描述 |
| :--- | :--- |
| adfs | Acorn 高级磁盘文件系统（只读） |
| affs | Amiga 快速文件系统 |
| bfs | BeOS 文件系统（适用于 2.2 内核） |
| coda | 高级网络文件系统 |
| coherent | Coherent UNIX 文件系统 |
| cramfs | ROM、嵌入式文件系统 |
| devfs | 设备（虚拟）文件系统 |
| devpts | 支持 UNIX98 伪终端 |
| efs | 扩展（IRIX）文件系统 |
| ext | 约 1992 年用于 Linux 的扩展文件系统（已弃用） |
| ext2 | 第二扩展文件系统（Linux 原生） |
| gfs | 全局文件系统（用于集群） |
| hfs | Mac OS 分层文件系统 |
| hpfs | 高性能（OS/2）文件系统 |
| iso9660 | CD-ROM 文件系统 |
| minix | Minix 操作系统文件系统 |
| msdos | DOS 文件系统 |
| ncptfs | Novell NetWare 文件系统 |
| nfs | 网络文件系统 |
| ntfs | Windows NT 文件系统 |
| proc | 进程表（虚拟）文件系统 |
| qnx4 | QNX 操作系统文件系统 |
| rfs | Reiser 文件系统（日志型） |
| romfs | 只读存储器文件系统 |
| smbfs | Samba 文件系统 |
| swap | Linux 交换空间 |
| sysv | SysV UNIX 文件系统 |
| udf | DVD-ROM 文件格式 |
| ufs | UNIX 文件系统 |
| umsdos | DOS 下的 Linux 文件系统 |
| vfat | Windows 文件系统 |
| xenix | Xenix 文件系统 |
| xiafs | 早期 Linux 文件系统（已弃用） |

此文件可能会稍作修改，以添加额外的硬件，例如新的外部驱动器或可移动介质。您将学习如何编辑文件系统表，了解如何配置系统以允许使用 NFS（网络文件系统）挂载远程硬盘，以及如何挂载其他本地分区，例如您的 Mac OS 桌面或卷。

### 编辑 `/etc/fstab`

您系统的文件系统表 `/etc/fstab` 是已知存储或可移动设备介质的列表，包含相关的设备名称、*挂载点*（设备在文件系统中出现的位置）、挂载选项和检查选项。您还会在那里找到列出的虚拟文件系统，这些文件系统可用于您的系统进程表 `/proc`，以及 USB 设备 `usbdevfs`。

例如，这里是一个文件系统表示例（在运行 SuSE Linux 的 Apple G4 Cube 上）：

```
/dev/hda10    /mac        hfs     ro,noauto,user        0 0
/dev/hda11    /           ext2    defaults                1 1
/dev/hda12    swap        swap    defaults                0 0
/dev/hda13    /d2         ext2    defaults                1 2
/dev/cdrom    /cdrom      auto    ro,noauto,user,exec     0 0
proc          /proc       proc    defaults                0 0
usbdevfs      /proc/bus/usb     usbdevfs  defaults        0 0
devpts      /dev/pts    devpts  defaults                0 0
```

第一列显示关联的设备。在这个例子中，根目录或 `/` 目录位于 `/dev/hda11`。一个小的 Mac OS 分区，由 `/dev/hda10` 表示，如果挂载，将出现在 `/mac` 目录中。`/dev/cdrom` 设备（实际上是一个符号链接，可能是 `/dev/sr0` 或 `/dev/hdb`）将挂载在 `/cdrom` 目录。如前所述，第二列指定了挂载点。SuSE Linux 发行版默认使用此目录，而基于 Red Hat 的 Linux 发行版将使用 `/mnt/cdrom` 目录。第二个 Linux 卷是 `/dev/hda13`，被指定为 `/d2`。您可以知道这一点，因为第三列显示了该设备使用的文件系统类型。

`proc`、`usbdevfs` 和 `devpts` 条目是仅在 Linux 运行时才出现的虚拟文件系统。它们包含用于内核、设备驱动程序、模块和其他实用程序的信息文件。例如，您可以通过查看 `/proc/mounts` 文件来查看已挂载的文件系统列表，如下所示：

```
$ cat /proc/mounts
/dev/root / ext2 rw 0 0
proc proc proc rw 0 0
/dev/hda13 /d2 ext2 rw 0 0
usbdevfs /proc/bus/usb usbdevfs rw 0 0
devpts /dev/pts devpts rw 0 0
//gigi/public . smbfs rw 0 0
```

这个例子表明，根文件系统、进程文件系统、第二卷、USB、设备以及 Samba `smbfs` 文件系统已被挂载。使用 `df` 命令，您可以获取几乎相同的信息，如下所示：

```
$ df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda11 6102696 5300008 492668 91% /
/dev/hda13 7133580 657616 6113576 10% /d2
usbdevfs 1783395 1783395 0 100% /proc/bus/usb
//gigi/public 18940416 6287672 12652544 33% /d2/gigi
```

这个例子显示了已挂载的设备及其位置。它还显示了设备上剩余多少空间。`df` 命令用于显示已挂载文件系统的剩余空闲空间。`usbdevfs` 文件系统没有剩余空间，因为它动态地扩展和收缩，并且是一个虚拟文件系统。

`/etc/fstab` 条目中的第四列列出了在 `mount` 命令中使用的期望选项。这些选项中的一些包括：

| 选项 | 描述 |
| :--- | :--- |
