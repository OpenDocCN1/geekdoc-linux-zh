

## df

`df` 实用程序用于显示已挂载文件系统中已使用和可用的磁盘空间。当不使用任何选项时，`df` 实用程序会报告当前所有已挂载文件系统中已使用和可用的空间。可以使用多种选项来控制 `df` 实用程序的输出；这些选项在表 5-10 中列出。

| 选项 | 用途 |
| :--- | :--- |
| -a | 显示所有文件系统的计数。 |
| -t 文件系统 | 将列表限制为指定文件系统的类型。 |
| -h | 创建人类可读的输出，并添加 M 代表兆字节等字母。 |
| -k | 以千字节为单位显示大小。 |
| -m | 以兆字节为单位显示大小。 |
| -i | 显示 inode 使用信息。 |
| -l | 将列表限制为本地文件系统中的那些。 |
| -x 文件系统 | 从列表中排除指定的文件系统。 |

以下是使用 `df` 实用程序生成的一些输出示例。第一个示例是使用无选项的 `df` 实用程序。第二个示例为列出的文件系统生成人类可读的大小。第三个示例显示所有已挂载文件系统的 inode 信息。

```
# df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda8 4096380 1469176 2672704 36% /
/dev/hda5 15522 3710 11011 25% /boot
/dev/hdb1 9740592 6861408 2384384 74% /fun
# df -h
Filesystem Size Used Avail Use% Mounted on
/dev/hda8 3.9G 1.4G 2.5G 36% /
/dev/hda5 15M 3.6M 11M 25% /boot
/dev/hdb1 9.3G 6.5G 2.3G 74% /fun
# df -i
Filesystem Inodes IUsed IFree IUse% Mounted on
/dev/hda8 4294967295 0 4294967295 0% /
/dev/hda5 4016 27 3989 1% /boot
/dev/hdb1 1237888 9692 1228196 1% /fun
```

![](img/96d9ccd181675a8ae8b6a1146c919d2b_249_0.png)

务必了解用于显示文件系统 inode 信息的选项。

## 挂载和卸载文件系统

![](img/96d9ccd181675a8ae8b6a1146c919d2b_249_1.png)

### 2.4 设备、Linux 文件系统、文件系统层次标准

- 控制文件系统的挂载和卸载。手动挂载和卸载文件系统，配置开机时挂载文件系统，配置用户可挂载的可移动文件系统。包括管理 /etc/fstab 文件。

使用文件系统所需的最后一步是必须将其**挂载**。挂载文件系统使其对系统和用户可用。本节涵盖用于挂载和卸载文件系统的实用程序。这里还涵盖了 Linux 系统中包含文件系统信息的文件。这些工具在处理 Linux 系统时每天都使用，在准备使用系统以及准备考试时特别值得关注。

### 挂载文件系统

`mount` 命令用于在 Linux 上挂载文件系统。`mount` 命令的标准形式如下：

```
mount -t type device mountpoint
```

此命令指定文件系统类型、包含文件系统的设备以及文件系统所在的目录。在许多发行版中，挂载文件系统的常见位置是 `/mnt` 目录。此目录可以配置为具有如 `/mnt/floppy` 和 `/mnt/cdrom` 这样的子目录。此命令的使用示例如下所示，使用 ext2 文件系统将 `/dev/hda2` 设备挂载到 `/fun` 挂载点。

```
# mount -t ext2 /dev/hda2 /fun
```

`mount` 命令可以使用多个选项；这些在表 5-11 中涵盖。

| **选项** | **用途** |
| :--- | :--- |
| -V | 显示版本信息。 |
| -h | 显示帮助信息。 |
| -v | 详细挂载文件系统。 |
| -a | 挂载 `/etc/fstab` 中列出的所有文件系统。 |
| -f | 模拟挂载文件系统。 |
| -l | 在显示的输出中添加 ext2 标签。 |
| -n | 挂载文件系统而不将其添加到 `/etc/mtab` 文件。 |
| -r | 以只读模式挂载文件系统。 |
| -w | 以写模式挂载文件系统。 |
| -L | 以指定标签挂载文件系统。 |
| -t 文件系统类型 | 将设备作为指定文件系统类型挂载。 |

### 卸载文件系统

`umount` 命令用于在 Linux 系统上卸载文件系统。这通常用于在弹出可移动媒体设备之前将其卸载。在卸载时，文件系统中不能有打开的文件。可以使用设备名称或挂载目录来卸载文件系统。`umount` 命令可以使用多个选项；这些在表 5-12 中涵盖。

表 5-12 用于 umount 的选项

| 选项 | 用途 |
| :----- | :--- |
| -V | 显示版本信息。 |
| -h | 显示帮助信息。 |
| -v | 详细卸载文件系统。 |
| -n | 不写入 /etc/mtab 文件而卸载。 |
| -r | 如果卸载失败，尝试以只读模式重新挂载。 |
| -a | 卸载 /etc/mtab 文件中列出的所有文件系统。 |
| -f | 强制卸载文件系统。 |

以下是正确使用 *umount* 命令的示例。

```
# umount /mnt/cdrom
```

此命令将卸载当前挂载到 /mnt/cdrom 的设备，以便可以弹出。

在挂载和卸载文件时，你需要了解两个文件：/etc/fstab 和 /etc/mtab。

### 使用 /etc/fstab 检查可用文件系统

/etc/fstab 文件包含 Linux 系统启动时挂载的文件系统。此文件还包含手动挂载的文件系统。如果文件系统列在此文件中并设置了正确的权限，则只需发出 *mount* 命令和目录即可挂载，如下所示：

```
# mount /mnt/floppy
```

以下是 /etc/fstab 文件的示例。从该文件可以看出，设备名称列出后跟着挂载点。接下来是文件系统类型以及文件系统是由操作系统自动挂载还是由用户手动挂载。Umask 信息也存储在这里。umask 信息用于设置新创建文件和目录的默认权限。此示例显示了使用某些 Linux 内核中可用的 supermount 选项作为选项挂载的设备。Supermount 旨在防止当前在更换软盘和 CD-ROM 等可移动媒体时需要的手动挂载和卸载。在使用 mount 命令和存储媒体时，请记住系统同等对待固定设备和可移动设备。一旦设备已挂载，就可以使用，直到它被卸载或移除。

```
/dev/hda8 / ext2 defaults 1 1
/dev/hda5 /boot ext2 defaults 1 2
none /dev/pts devpts mode=0620 0 0
/dev/hd1 /fun ext2 defaults 1 2
/mnt/cdrom /mnt/cdrom supermount fs=iso9660,dev=/dev/cdrom 0 0
/mnt/cdrom2 /mnt/cdrom2 supermount fs=iso9660,dev=/dev/cdrom2 0 0
/mnt/floppy /mnt/floppy supermount fs=vfat,dev=/dev/fd0 0 0
/dev/hda1 /mnt/win_c vfat user,exec,umask=0 0 0
/dev/hda7 /mnt/win_d vfat user,exec,umask=0 0 0
none /proc proc defaults 0 0 0
/dev/hda9 swap_upgrade swap defaults 0 0 0
```

例如，行 `/dev/hda8 / ext2 defaults 1 1` 表示硬盘 A 的分区 8 挂载在根 (/) 目录。文件系统类型为 ext2，并且此设备使用默认选项。可用的一些选项包括 noauto，它指定设备不应自动挂载，以及 user，它指定设备可由用户挂载。文件 0 0 字段用于确定哪些设备需要转储。此处的值 0 指定不应执行转储。

这里的 user 选项非常重要，应该仔细关注此选项。它指定文件系统可由用户挂载。这种权限对于可移动媒体设备等非常有用，允许用户挂载和卸载设备，以便更换媒体。由于此权限允许用户挂载和卸载设备，因此不应授予关键文件系统。

### 使用 `/etc/mtab` 检查已挂载的文件系统

`/etc/mtab` 文件包含系统当前挂载的文件系统列表。以下是 `/etc/mtab` 文件的示例。如您所见，设备名称与挂载点一起列出。此文件中的字段对应于 `/etc/fstab` 文件中使用的字段。文件系统类型和访问权限也在此显示。

```
/dev/hda8 / reiserfs rw 0 0
proc /proc proc rw 0 0
/dev/hda5 /boot ext2 rw 0 0
devpts /dev/pts devpts rw 0 0
/dev/hd1 /fun ext2 rw,noexec,nosuid,nodev 0 0 0
/mnt/cdrom2 /mnt/cdrom2 supermount fs=iso9660,dev=/dev/cdrom2 0 0
/mnt/floppy /mnt/floppy supermount fs=vfat,dev=/dev/fd0 0 0
/dev/hda1 /mnt/win_c vfat user,exec,umask=0 0 0
/dev/hda7 /mnt/win_d vfat user,exec,umask=0 0 0
none /proc proc defaults 0 0 0
/dev/hda9 swap_upgrade swap defaults 0 0 0
```

