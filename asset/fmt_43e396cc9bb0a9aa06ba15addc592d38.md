
该实用程序从 `/etc/mtstab`（第 961 页）获取这些信息。该文件涵盖挂载的文件系统；有关挂载远程文件系统的 NFS 信息，请参阅第 1019 页。

上述示例中的前六项显示了标准 Linux `ext2` 和 `ext3` 文件系统的磁盘分区。这三个三个磁盘上的磁盘分区：两个 IDE 磁盘（`hda`, `hdb`）和一个 SCSI 磁盘（`sda`）。磁盘分区 `/dev/hda1` 挂载在 Linux 文件系统的 `/dos` 目录下，这是一个 DOS (`ms`) 文件系统。你可以使用 GNU Linux 实用程序和应用程序像访问 Linux 文件目录一样访问该分区上的 DOS 文件和目录。以 `none` 开头的行显示了特殊的 `/proc` 文件系统（第 966 页）。最后一行显示 CD-ROM 已经挂载在 SCSI CD-ROM 驱动器（`/dev/scd0`）上。

有时，`/etc/mtstab` 中的文件列表可能与已挂载的分区不同步。你可以通过重启系统来修复此，或者参考 `/proc/mounts` 文件的内容，其信息可能与 `mtab` 略有不同，但后者总是准确的。你可以将 `mtab` 替换为 `/proc/mounts` 的符号链接：

```bash
# rm /etc/mtstab
# ln -s /proc/mounts /etc/mtstab
```

## 不要在根目录 (`/`) 上挂载任何内容

务始终将网络文件系统和可移动设备挂载在文件系统根目录至少下一层。根文件系统挂载在 `/`，你不能在同一个位置挂载两个文件系统。如果你尝试在 `/` 上挂载某些内容，根目录下的所有文件、目录和文件系统将不再可用，并导致系统崩溃。

当你向 `/etc/fstab` 文件（第 959 页）为文件系统添加一行时，超级用户（Superuser）可以通过提供关联的挂载点（或设备）作为 `mount` 的参数来挂载文件系统。例如，列出的 SCSI CD-ROM 是使用以下命令挂载的：

```bash
$ mount /mnt/cdrom
```

该命令之所以生效，是因为 `/etc/fstab` 包含了挂载该文件所需的额外信息：

```
/dev/scd0 /mnt/cdrom iso9660 user,noauto,ro
```

你也可以挂载未出现在 `/etc/fstab` 中的文件系统。例如，当你向软驱器插入一个存有 DOS 文件系统的软盘时，你可以使用命令挂载该文件系统：

```bash
# mount -t mdsdos /dev/fd0 /mnt/floppy
```

`-t mdsdos` 指定了文件系统类型 `mdsdos`。只有在你配置了 Linux 内核（1031 版本之后）接受 DOS 文件系统时，才能挂载 DOS 文件系统。你不需要为了读写 DOS 文件系统而挂载它；请参阅第 1256 页的“Mtools”。你需要挂载 DOS 文件系统，以便程序（例如 `vi` 在在磁盘上使用 GNU/Linux 命令。

## 挂载选项

`mount` 实用程序带有许多选项，你可以在命令行或 `/etc/fstab` 文件（第 978 页）中指定它们。要查看本地文件系统的挂载选项完整列表，请查看 `mount` 手页；对于远程文件系统，请查看 `nfs mount` 页面。

`noauto` 选项意味着文件系统将不会自动挂载。`nosuid` 选项强制挂载的可执行文件在本地系统（拥有该文件系统的系统）上普通普通运行（不更改有效用户 ID）。

除非指定了 `user`、`users` 或 `owner` 选项，否则只有超级用户可以挂载和卸载文件系统。`user` 选项意味着任何用户都可以挂载该文件系统，但必须由挂载它的用户卸载；`users` 意味着任何用户都可以挂载和卸载该文件系统。这些常用于 CD-ROM 和软驱器。`owner` 选项仅在特殊情况下使用，与 `user` 选项的区别在于挂载用户必须拥有该设备。

## 挂载 Linux 软盘

挂载软盘与挂载硬盘分区类似。在 `/etc/fstab` 中为第一个软驱写入类似的条目。

```
/dev/fd0 /mnt/floppy ext2 noauto,users 0 0
```

必要时创建 `/mnt/floppy` 目录。插入软盘并尝试挂载第一个命令。在以下示例中，第一个命令后的错误消息通常表示软盘上没有文件系统：使用 `mkfs`（第 1057 页）创建文件系统，但要小心 `mkfs` 会破坏磁盘上的数据：

```bash
# mount /dev/fd0
mount: wrong fs type, bad option, bad superblock on /dev/fd0,
or too many mounted file systems
# mkfs /dev/fd0
mke2fs 1.17, 26-Oct-1999 for EXT
```

*注：由于原文后半部分存在大量重复的无意义字符，已根据技术语境对核心操作指令进行了清理翻译。*

5. `Dump`: 用于确定何时备份文件系统（见第 1002 页）。

6. `Fck`: 决定先对哪个文件系统进行 `fsck` 检查。根目录 (`/`) 在此列中应为 1，其他需要检查的文件系统应为 2，而不需要检查的文件系统（例如远程挂载的文件系统或 CD-ROM 刻驱驱动器）应为 0。

以下示例显示了一个典型的 `fstab` 文件：

```
# cat /etc/fstab
/dev/hda2  /           ext3 defaults        1 1
/dev/hda1  /boot       ext2 defaults        1 2
/dev/hda5   /home       ext3 defaults        1 2
/dev/cdrom  mnt/cdrom  iso9660 noauto,owner,ro  0 0
/dev/hda7   /tmp        ext2 defaults        1 2
/dev/hda6   /usr        ext3 defaults        1 2
/dev/hda11  swap        swap    defaults        0 0
/dev/fd0    /mnt/floppy ext2 noauto,owner      0 0
none        /dev/pts    proc    defaults        0 0
none        /dev/pts      devopts gid=3,mode=620  0 0
bravo:/home/alex  /bravo_home  nfs     defaults        1 2
kudos:/home/alex  /kudos_alex  nfs     defaults        0 0
```

## 导出符号链接和设备文件

当导出符号链接时，请确保链接的对象在客户端（远程）机器上是用的。如果链接的对象在客户端机器上不存在，你必须连同链接一起导出并挂载；否则，它将无法指向服务器上原本指向的文件。

设备文件指的是 Linux 内核接口。当你导出设备文件时，你导出的是该接口。如果客户端机器没有相同类型的设备，则导出的设备将无法工作。

在已导出的文件系统内部具有挂载点的文件系统将不会被导出。你需要导出每一个想要导出的文件系统，即使它位于一个已经导出的文件系统中。当你有两个位于两个分区上需要导出的文件系统 `/opt/apps` 和 `/opt/apps/oracle` 时，你必须显式地导出每一个。大多数其他子目录和文件都会自动导出。

## autofs: 自动挂载文件系统

`autofs` 文件系统与其他任何文件系统类似，但在需要它之前一直保持未挂载状态，在需要时系统会自动挂载它（按需挂载）。当 `autofs` 文件系统不再被需要时，系统会卸载它，这是以一致方式管理大量机器的一个重要组成部分。`automount` 实用程序在存在大量服务器或大量文件系统时特别有用。它还有助于消除服务器依赖。当你有两台服务器，它们都挂载对方的文件系统且都处于宕机状态时，两者可能会挂起，因为它们都会尝试使用传统的基于 `fstab` 的挂载方式从对方那里挂载文件系统。`automount` 机制通过仅在进程尝试访问它时才从对方挂载文件系统，解决了这个问题。

`automount` 进程通常在系统进入运行级别 3 或 5 时由 `/etc/rc.d/init/autofs` 脚本启动。当进程访问未挂载的 `autofs` 文件系统中的某个目录时，该文件系统会通知 `automount`，随后 `automount` 挂载该 `autofs` 文件系统。你必须执行类似 `cd /home` 这样访问 `autofs` 挂载点的命令，以便创建你可以看到的挂载文件系统。Linux 内核必须支持 `autofs` 你才能使用它。Red Hat 包含了 `autofs` 内核模块。使用以下测试之一来查看 `autofs` 模块是否启用：

```
/proc/mount | grep autofs
```

或者

```
/sbin/lsmod | grep autofs
```
