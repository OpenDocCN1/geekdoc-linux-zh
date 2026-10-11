
`fstab` 文件中包含一条关于 `/proc` 的条目。这个伪文件系统包含有关系统进程、可用内存以及内核所知道的其他系统信息。`/proc` 是一个伪文件系统，因为它实际上不使用硬盘上的磁盘空间。手动挂载文件系统的典型命令是 `mount -t [type] [device] [directory]`。例如，要将设备 `/dev/hda2` 上的 `ext3` 文件系统挂载到目录 `/home`，请使用 `mount -t ext3 /dev/hda2 /home` 命令。

手动挂载文件系统并不常见，但如果需要临时挂载，该命令是可用的。大多数挂载发生在启动时，使用 `mount -av` 命令完成。

已挂载的文件系统在系统关机时会自动卸载。如果系统意外停止，文件系统可能会损坏。要修复或检查文件系统，请使用 `fsck` 命令。如果未指定文件系统，`fsck` 命令将依次检查 `fstab` 文件中的所有文件系统。

要卸载文件系统，语法为 `umount [mount point or device name]`。例如，要将 `/dev/hda2` 从 `/home` 目录卸载，请输入 `umount /dev/hda2` 或 `umount /home`，设备即可卸载。

要检查文件系统类型为 `ext3` 且挂载点为 `/home` 的文件系统，请输入 `fsck -t ext3 /home` 命令。

`fsck` 返回的退出代码是以下条件的总和：

| 代码 | 条件 |
| :--- | :--- |
| 0 | 无错误 |
| 1 | 文件系统错误已修复 |
| 2 | 系统应重启 |
| 4 | 文件系统错误未修复 |
| 8 | 操作错误 |
| 16 | 使用或语法错误 |
| 32 | `fsck` 由用户请求取消 |
| 128 | 共享库错误 |

`fsck` 程序默认以交互方式运行。如果发现错误，系统会提示用户采取什么操作。可以使用 `-a` 选项自动修复文件系统而不进行任何询问。要查看 `fsck` 的选项列表，请参考手册页。

## 使用软驱

使用软驱的第一步是了解其在文件系统中的位置。如果您只有一个软驱，它通常位于 `/dev/fd0`。您可以通过查看 `/etc/fstab` 文件（`cat /etc/fstab`）来验证位置。您的软盘在 `fstab` 文件中的有效条目应为：

```text
/media/floppy /dev/fd0 /mnt/floppy auto noauto,owner,kudzu 0 0
```

其中：

- `/dev/fd0` — 软盘设备位置
- `/mnt/floppy` — 文件系统的读写挂载位置
- `auto` — 文件系统类型
- `noauto, owner, kudzu` — 挂载选项
- `0` — 文件系统转储频率
- `0` — 文件系统检查频率

要在上述位置格式化软盘，请使用 `mkfs` 命令。以下操作将格式化 1.44 MB 的软盘：

```bash
mkfs -t ext3 /dev/fd0 1440
```

软盘格式化后，可以使用命令 `mount /dev/fd0 /mnt/floppy` 将其挂载。`/mnt/floppy` 位置是软盘的挂载点。除非软驱中有磁盘，否则此命令无法工作。

软驱挂载后，您可以使用挂载点 `/mnt/floppy` 来读取和写入驱动器。要查看软驱的内容，请使用 `ls` 命令。要查看新挂载的软驱，请使用 `ls /mnt/floppy` 命令。使用 `rm`、`cp`、`mv` 和其他命令来操作软盘内的文件和目录。

要卸载软驱，请使用 `umount` 命令。要卸载挂载在 `/mnt/floppy` 的软盘，请使用命令 `umount /mnt/floppy`。

若要更换正在使用的软盘，必须先卸载驱动器，更换软盘，然后再重新挂载驱动器。

## 目标 2.9 使用光盘

使用光盘与使用软驱类似。光盘在使用前必须挂载，使用后必须卸载。也可以使用 `cdrrecord` 命令向 `CD-R` 或 `CD-RW` 写入数据。

要挂载光盘，必须先找到设备。查看 `/etc/fstab` 文件以查看可用设备。通常，第一个光驱会有以下条目：

```text
/dev/cdrom       /mnt/cdrom        udaf, iso9660     noauto, owner, kudzu, ro  0 0
```

类似于软盘设备，此光盘位于 `/dev/cdrom`，并使用挂载点 `/mnt/cdrom`。要挂载光盘，请使用命令 `mount /dev/cdrom /mnt/cdrom`。

光盘挂载后，可以使用 `ls` 或 `cp` 命令读取它。光盘是以只读设备形式挂载的。

要更换光盘，可以卸载驱动器或使用 `eject` 命令。您可以通过输入 `eject cdrom` 使用 `eject` 命令弹出光盘。驱动器弹出光盘后，插入下一张光盘并重新开始。

`CD-R` 和 `CD-RW` 可以写入数据。`cdrrecord` 命令可用，并且几乎适用于所有 Linux 系统。如果您的系统未加载 `cdrrecord` 命令，可以从官方站点 `ftp://ftp.berlios.de/pub/cdrrecord/` 下载该软件包。

要找到您的光驱，请使用 `-scdbus` 选项。输入 `cdrrecord -scdbus` 将显示已安装并被识别的驱动器。例如：

```text
# cdrrecord -scdbus

cdrrecord 2.0 (1686-pc-linux-gnu) Copyright (C) 1995-2002 Jörg Schilling
Linux sg driver version:  3.1.24
Using libscg version 'schily-0.7'

scsibus0:
  0,0,0  0) '  ' '48X12X50 CD-RW' '1.00' Removable CD-ROM
  0,1,0  1) *
```

上述显示表明该设备是 `0,0,0`。

要烧录 `ISO` 镜像，请使用以下 `cdrrecord` 命令：

`cdrrecord -v dev=0,0,0 speed=0 driveropts=burnfree -eject -data myfile.iso`

其中：

- `-v` — 详细模式
- `dev=0,0,0` — 设置光盘记录器的 `SCSI` 目标
- `speed=0` — 设置写入过程的速度因子
- `driveropts=burnfree` — 驱动程序选项 `burnfree` 开启无缓冲欠载功能
- `-eject` — 过程完成后弹出光盘
- `-data` — 使用光盘模式 1
- `myfile.iso` — 使用 `ISO` 文件 `myfile.iso`

可以使用 `man cdrrecord` 命令找到 `cdrrecord` 的选项。

## 摘要

启动时，Linux 操作系统执行开机自检（`POST`），从 `ROM` 加载 `BIOS`，然后通过引导加载程序（通常是 `GRUB` 或 `LILO`）显示启动选项。

Linux 内核从启动设备加载到内存中，控制权随之移交。随后执行 `init` 程序，并控制启动过程的其余部分。

`Init` 在启动过程中使用几个脚本：

- `/etc/rc.d/rc.sysinit` 设置环境值，如路径、启动交换分区以及检查文件系统。`rc.sysinit` 使用 `/etc/sysconfig` 配置文件和脚本。
- `/etc/inittab` 描述系统在每个运行级别中应如何设置。
- `/sbin/update` 由 `inittab` 执行，用于刷新脏缓冲区。
- `/etc/rc.d/rc*.d` 目录包含在启动和关机过程中由 `init` 执行的脚本。最常用的运行级别是 3 和 5。3 是默认的命令行运行级别，5 是默认的图形用户界面（`GUI`）运行级别。

共有七种不同的运行级别。

- `0` 关机
- `1` 单用户模式
- `2` 未使用（可由用户定义）
- `3` 完整多用户模式
- `4` 未使用（可由用户定义）
- `5` 基于 `X` 的登录屏幕（`GUI`）的完整多用户模式
- `6` 重启

运行级别 2 到 5 具有虚拟控制台，可通过 `Ctrl+Alt+F1-7` 键组合访问。

关闭 Linux 系统可以确保文件被保存且文件系统被卸载。如果不执行关机操作直接断电，可能会导致文件损坏。

用户通过用户名进行标识，通过密码进行身份验证。可以使用 `useradd` 命令轻松添加用户，并使用 `passwd` 命令更改密码。用户还通过 `UID` 进行标识，`UID` 是一个唯一标识符，值大于或等于 500。也有 `GUI` 工具可以轻松地添加用户和组。

用户总是属于一个组。一个组可以包含一个或多个用户。组用于简化在处理文件权限时的管理问题。

Linux 中的文件分为可共享和不可共享、变量和静态文件。可共享文件可供多个用户使用，不可共享文件仅供一个用户使用。变量文件可以根据需要进行更改，而静态文件具有恒定值。
