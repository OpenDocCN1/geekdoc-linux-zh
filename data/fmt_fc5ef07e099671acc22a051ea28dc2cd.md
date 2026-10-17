
`<device>` `<mountpoint>` `<filesystem>` `<options>` `<dump>` `<fsck>`

```
```

第一个字段是要待挂载的文件系统的名称。它通常以 `/dev/` 开头，例如表示第三个硬盘分区的 `/dev/hda3`。下一个字段是你文件结构中的目录，你想将该设备上的文件系统附加在此。第三个字段是正在挂载的文件系统类型。表 32-7 提供了你可以挂载的所有不同类型的列表。标准 Linux 硬盘分区的类型是 `ext2`。下一个示例显示了主 Linux 硬盘分区的条目。该条目挂载在根目录 `/` 下，文件类型为 `ext2`。

### 表 32-7：文件系统类型

| 类型 | 描述 |
| --- | --- |
| auto | 尝试自动检测文件系统类型 |
| minux | Minux 文件系统（文件名限制为 30 个字符） |
| ext | 早期版本的 Linux 文件系统，不再使用 |
| ext2 | 标准 Linux 文件系统，支持文件名和文件大小；不包含日志 |
| ext3 | 标准 Linux 文件系统，支持文件名和文件大小；包含日志 |
| xiaf | Xiaf 文件系统 |
| mdos | MS-DOS 分区的文件系统（16 位） |
| vfat | Windows 95, 98 和 Millennium 分区的文件系统（32 位） |
| ntfs | NT 和 Windows 2000 文件系统 |
| hbfs | 用于 OS/2 高性能分区的文件系统 |
| proc | 操作系统用于进程的文件系统 |
| nfs | 用于从远程系统挂载分区的 NFS 文件系统 |
| umsdos | U-DOS 文件系统 |
| swap | Linux 交换分区 |
| sysv | 系统 V 文件系统 |
| iso960 | 用于 CD-ROM 文件系统 |

在 `/etc/fstab` 文件中，你可以直接编辑 `/etc/fstab` 文件，或者使用 `Linuxconf`，它会提示你输入信息并并将正确的条目写入你的 `/etc/fstab` 文件。你可以参考此处的 `/etc/fstab` 示例作为指南，了解你的条目应该是什么样子 `/proc` 和交换分区尤为关键。

# `/etc/fstab`

```
# <device> <mountpoint> <filesystem> <options> <dump> <fsck>

/dev/hda3      ext3             defaults 0 1

/dev/hdc       mnt/cdrom      iso9660        ro,noauto 0

/dev/fd0       mnt/floppy    auto           defaults,

/dev/proc      proc           proc           defaults 0

/dev/hda2      none           swap           sw

/dev/hda1      mnt/windows   vfat           defaults 0 0
```

你可以通过你的 MS-DOS 或 Windows 操作系统将 MS-DOS 或 Windows 95 分区挂载到你的 Linux 结构中，就像挂载任何 Linux 文件系统一样。你只需要为 Windows 95 指定类型为 `vfat`，为 MSDOS 指定类型为 `msdos`。你可能会发现，在启动 Linux 系统时自动挂载 Windows 分区非常方便（MS-DOS 分区也是如此）。要实现这一点，你需要在 `/etc/fstab` 文件中为你的 Windows 分区添加条目，并赋予其 `defaults` 选项或 `auto` 选项。你需要为想要挂载的每个 Windows 分区创建一个条目，然后指定该分区的设备名称，随后是你想挂载它的目录。`/mnt/windows` 目录后面会跟一个选择（因为 windows 目录已经在 `/mnt/` 下创建了）。对于文件系统类型，输入 `vfat`。下一个示例显示了 `/etc/fstab` 文件中标准的 MS-DOS 分区条目。最后一个是 `/etc/fstab` 示例中用于挂载 Windows 分区的条目。

如果你的 `/etc/fstab` 文件损坏、导致某行被删除或更改——你的系统将进入维护模式，让你对分区仅有只读访问权限。要获得读/写权限，你可以修复 `/etc/fstab` 文件，但这必须先卸载你的主分区。以下命令执行此类操作：

```
# -n -o remount,rw /
```

`/etc/fstab` 中列出的文件系统在每次启动时都会自动挂载，除非使用 `noauto` 选项显式禁用此功能。注意，CD-ROM 和软磁盘具有 noauto 选项。此外，如果你执行了 `mount -a` 命令，所有没有 `noauto` 选项的系统都会被挂载。如果你想让 CD-ROM 支持用户手动挂载，请添加 `user` 选项。

```
/dev/hdc /mnt/cdrom iso9660 ro,noauto,user 0 0
```

注意：来自 `/etc/fstab` 文件系统的“自动”挂载命令实际上是通过在 `/etc/rc.d/sysinit` 中执行每次启动时运行的 `mount -a` 命令来实现的。`mount -a` 命令将挂载 `/etc/fstab` 文件中列出的任何没有 `noauto` 选项的文件系统。`umount` 选项将卸载 `/etc/fstab` 中的文件系统（该操作在系统关闭时执行）。

## 安装 IDE CD-R 和 CD-RW 设备

Linux CD 刻录程序将所有 CD-R 和 CD-RW 驱动器视为 SCSI 驱动器。这意味着 IDE CD-R 和 CD-RW 驱动器必须模拟 SCSI 驱动器才能被 CD 软件识别和使用。如果你只想在 CD 刻录程序中使用 IDE CD-ROM（例如仅作为读取器复制 CD 光盘），IDE CD-ROM 也必须模拟 SCSI CD-ROM。只有 SCSI 驱动器（CD-R、CD-WR 或 CD-ROM）会被 Linux CD 刻录机识别。例如，如果你有一个普通的 IDE ROM 想在 Linux CD 刻录软件中复制 CD（刻录），那么你必须让 IDE CD-ROM 模拟 SCSI CD-ROM。访问 `www.linuxdoc.org` 查看 CD-Writing HOWTO 以获取更多详情。此处显示了简要描述：

注意，IDE 设备的 SCSI 模拟是在内核中实现的（“IDE, ATA, and ATAPI Block devices”中的“SCSI Emulation Support”）。

```
alias scdl sr_mod
pre-install sg modprobe ide-scsi
pre-install sr_mod modprobe ide-scsi
pre-install ide-scsi modprobe ide-cd
```

一旦你安装了 SCSI 仿真，就应该检查 IDE 驱动器是否被识别为 SCSI 驱动器。要做到这一点，你需要运行带有 `scanbus` 选项的 `cdrecord` 程序。以下示例显示了两个作为 SCSI 驱动器运行的 IDE 驱动器。一个是 Plextor IDE CD-ROM (`scd0`)，另一个是东芝 Toshiba CD-ROM 驱动器 (`scd1`)。

```
# cdrecord -scanbus

Cdrecord 1.9 (i686-pc-linux-gnu) Copyright (C) 1995-2000 Jörg Schilling

Linux driver version: 3.1.17

Using libseqc 'shily-0.1'

scsi:

0,0, 0) 'PLEXTOR' 'CD-R PX-W1210A' '1.02' Removable CD-ROM

0,1, 1) 'TOSHIBA' 'DVD-ROM SD-M1402' '1010'

0,2, 2) *

0,3, 3) *

0,4, 4) *

0,5, 5) *

0,6, 6) *

0,7, 7) *
```
