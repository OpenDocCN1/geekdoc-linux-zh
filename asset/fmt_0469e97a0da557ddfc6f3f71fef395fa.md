
`LABEL=/` `/` `ext3` `defaults` `0` `1`

对于 `ext2` 和 `ext3` 分区，你可以使用 `e2label` 工具或带有 `-L` 选项的 `tune2fs` 来更改或添加标签。指定设备和标签。如果你命名了标签，请务必更改 `/etc/fstab` 文件中相应的条目。只需使用带设备名的 `e2label` 来查找当前标签。在下一个示例中，用户将 `/dev/hda3` 设备的标签更改为 `TURTLE`：

```
e2label /dev/hda3 TURTLE
```

## Windows 分区

你可以将操作系统所使用的 MS-DOS、Windows 95/98/ME 以及 Windows XP 和 2000 分区挂载到你的 Linux 文件系统中，就像挂载任何 Linux 文件系统一样。你必须为 Windows 95/98/ME 指定 `vfat` 类型，为 MS-DOS 指定 `mdos`。Windows XP 和 2000 使用 `ntfs` 文件类型。你可能会发现，在启动 Linux 时自动挂载分区非常方便。为了实现这一点，你需要在 `/etc/fstab` 文件中为每个分区创建一个条目。

### 提示
在启动 Linux 时，你可能会发现将分区自动挂载非常方便。为了实现这一点，你需要在 `/etc/fstab` 文件中为每个分区创建一个条目。

### 示例
要将 `hda1` 挂载到 `/mnt/windows`，指定设备名后跟目录。以下示例显示了如何将 `hda1` 挂载到 `/mnt/windows`：

```
mount /dev/hda1 /mnt/windows vfat 0 0
```

### 提示
CD-ROM 和软盘条目在 `/etc/fstab` 中使用以下选项：

```
/dev/hdc /mnt/cdrom isoc9660 noauto, owner, kudzu 0 0
```

从 `/etc/fstab` “自动”挂载文件系统的功能实际上是通过执行 `mount -a` 实现的。在关闭系统时使用 `umount` 命令。

## 直接挂载文件系统：`mount` 和 `umount`

你也可以使用 `mount` 和 `umount` 命令直接挂载或卸载任何文件系统。之前节中讨论的挂载操作使用了 `mount` 命令。通常，文件系统可以由 root 用户挂载，而 CD-ROM 和软盘可以由任何用户挂载。

### `mount` 命令

`mount` 命令接受两个参数：Linux 访问文件系统的存储设备，以及要挂载新文件系统的目录。挂载点位于你的目录树中。设备是连接系统到硬件的特殊文件。`mount` 的语法如下：
`mount device mountpoint`

如前所述，设备文件位于 `/dev` 目录，通常以设备数字结尾。例如，`fd0` 指向连接到系统的第一个软盘驱动器。以下示例将第一个软盘驱动器 `fd0` 挂载到 `/mnt/floppy` 目录。挂载点应该是空的。如果你已经在那里挂载了文件系统，将收到文件系统已挂载且目录正忙的消息。如果你将文件系统挂载到一个已经包含文件和子目录的目录，这些内容将被跳过，你只能访问挂载文件系统的文件。当然，卸载文件系统将恢复对原始目录的访问。

| 挂载选项 | 说明 |
| -f | 伪挂载文件系统。它用于检查文件系统是否可以被挂载。 |
| -v | 详细模式。`mount` 会显示它正在执行的操作。配合 `-f` 使用时可以检查挂载文件系统时的任何问题，`-fv`。 |
| -w | 以可读/写权限挂载文件系统。 |
| -r | 以只读权限挂载文件系统。 |

| -n | 挂载文件系统且不在 `fstab` 文件中为其创建条目。 |
| -t type | 指定指定要挂载的文件系统类型。有效的文件系统类型请参见表 30-7。 |
| -a | 挂载 `/etc/fstab` 中列出的所有文件系统。 |
| -o option-list | 使用选项列表挂载文件系统。这是 `-o` 之后的一个逗号分隔的选项列表。选项列表请参见表 30-8。 |

```
# mount /dev/fd0 /mnt/floppy
```

对于任何在 `/etc/fstab` 中有条目的分区，你都可以仅使用 `fstab` 条目中指定的目录来挂载该分区；`mount` 命令会在 `fstab` 中查找该分区的条目，使用该目录来识别条目，并从从中找到设备名称。例如，要挂载上一个示例中的 `/dev/hd1` Windows 分区，`mount` 命令只需要知道它被挂载到的目录 `/mnt/windows` 即可。

```
# mount /mnt/floppy
```

如果你不确定软盘包含的文件系统类型，可以使用 `-t` 选项指定自动文件系统来挂载它。给定了自动文件系统类型，`mount` 会尝试自动检测软盘上的文件系统类型。

```
# mount -t auto /dev/fd0 /mnt/floppy own
```

## `unmount` 命令

如果你想用另一个挂载的文件系统替换当前挂载的，你必须先显式地卸载已经挂载的那个。假设你已经挂载了一张软盘，现在想将其取出并插入一张新的。在插入新软盘并挂载它之前，你必须卸载那张软盘。你使用 `unmount` 命令卸载文件系统。`unmount` 命令可以接受设备名称或其挂载的目录作为参数。

```
# device-name-or-mountpoint
```

以下示例将卸载挂载在任何位置的软盘：

```
# unmount /dev/fd0
```

使用设备被挂载在 `/mydir` 目录的示例，你可以使用该目录来卸载文件系统：

```
# unmount /mydir
```

`unmount` 命令有一个重要的限制。你不能卸载当前正在其中运行工作的文件系统。如果你想在一个正尝试卸载的系统中更改文件系统，你将收到一条提示该文件系统正忙的错误消息。例如，假设你将 CD-ROM 挂载到 `/mnt/cdrom` 目录，然后决定更换 CD-ROM。你必须首先用 `unmount` 命令卸载当前的这一个。这将失败，因为你正处于它挂载的目录中。你必须离开该目录后才能卸载 CD-ROM。

```
# unmount /dev/hdc /mnt/cdrom
```

```
# cd /mnt/cdrom
# umount /mnt/cdrom
umount: /dev/hdd: device is busy
# cd /root
# umount /mnt/cdrom
```

提示

如果其他用户正在使用他们尝试挂载的文件系统，你可以使用 `lsof` 或 `fuser` 命令来查找是谁。

## 挂载软盘

如前所述，要访问软盘上的文件，必须先将该磁盘挂载到你的 Linux 系统上。你的软盘驱动器设备名称为 `fd0`，它位于 `/dev` 目录。输入 `/dev/fd0` 引用了你的软盘驱动器。`fd` 后面的数字 `0` 表示如果你有多个软盘驱动器，额外的驱动器由 `fd1`、`fd2` 等表示。你可以挂载到你想要的任何目录。Red Hat 为软盘提供了一个方便使用的目录 `/mnt/floppy`。以下示例将你软盘驱动器中的软盘挂载到：

- `mount /dev/fd0 /mnt/floppy`

提示

在 GNOME 中，你可以通过右键点击桌面显示菜单并选择“软盘”磁盘条目来挂载软盘。要卸载，右键点击软盘图标并在弹出菜单中选择“弹出”。

记住，你挂载的是特定的软盘，而不是软盘驱动器。你不能简单地取出磁盘并放入另一个。`mount` 命令已将文件连接到你的主目录树，系统期望在软盘驱动器中找到文件。如果你取出磁盘并放入另一个，在尝试访问它时会产生错误。

要更换磁盘，你必须先卸载软盘驱动器中的软盘。然后在放入新磁盘后，你必须显式地挂载该新磁盘。执行此操作，请使用 `unmount` 命令。

- `umount /dev/fd0`

对于卸载或挂载操作，你可以指定它挂载的目录或 `/dev/fd0` 设备。

- `umount /mnt/floppy`

当你关闭系统时，任何挂载的磁盘都会自动卸载。你不需要显式卸载它们。

## 挂载 CD-ROM

记住，当你挂载 CD-ROM 或软盘时，你不能简单地将其取出并向驱动器放入另一个。你必须卸载它，将文件系统从整个目录树中分离。事实上，CD-ROM 在卸载之前是锁定的。要挂载 CD-ROM，你必须先将其插入驱动器。CD-ROM 的设备名称通常为 `/dev/cdrom` 或 `/dev/hdc`。使用 `mount` 命令将其挂载到目录，例如：

```
# mount /dev/cdrom /mnt/cdrom
```

如果你想更换 CD-ROM，必须首先卸载当前的这一个。然后插入新的 CD-ROM 并挂载它：

```
# umount /mnt/cdrom
# mount /dev/cdrom /mnt/cdrom
```

## 安装 IDE CD-R/RW 和 DVD R/RW 设备

Linux CD 刻录程序都将 CD-R/RW 和 DVD 驱动器视为 SCSI 驱动器。这意味着 IDE CD-R/RW 驱动器必须模拟 SCSI 驱动器，以便被 CD 或 DVD 写入软件识别和使用。如果你想在 CD 写入应用程序中使用 IDE CD-ROM 或 DVD-ROM，它仍然必须模拟 SCSI CD-ROM。只有 SCSI 驱动器才能被 CD 或 DVD 写入软件识别。更多信息请参阅 www.tldp.org 上的 CD 写入 HOW-TO。

### 提示
IDE 设备的 SCSI 模拟在内核中实现，位于“IDE, ATA, and ATAPI Block/Devices”条目下的“SCSI Emulation Support”，该项目位于主内核配置菜单的“ATA/IDE/MFM/RLL Support”窗口中。通常，它被编译为模块。

IDE CD 和 DVD 驱动器在安装期间被识别为 IDE 设备并以此方式安装。然而，当你启动系统时，你需要指示 Linux 内核让 IDE CD 和 DVD 驱动器模拟 SCSI CD 或 DVD 驱动器。这意味着通常识别为 `/dev/hda` 的 CD-R 驱动器必须识别为 `/dev/sd0` 设备，即第一个 SCSI CD-ROM 驱动器。你通过加载 `ide-scsi` 模块来实现这一点，它允许 IDE CD 驱动器模拟 SCSI 驱动器。

## SCSI 模拟

你可以通过以下方式之一为 IDE CD 和 DVD 驱动器实现 SCSI 模拟：作为内核参数加载 `ide-scsi` 模块或在 `/etc/modules.conf` 2.5 和 2.6 内核为 `/etc/modprobe.conf` 中指定该模块。你还需要指示要模拟的 IDE 驱动器。`ide-scsi` 模块编译在内核中，你必须将其作为内核参数加载。

### 提示
在安装期间，Red Hat 会识别你安装在系统上的 IDE CD DVD 驱动器，并将 `ide-scsi` 内核参数作为 LILO 或 GRUB 引导加载程序配置的一部分自动包含。

## 启动时的内核参数

作为内核参数，你可以在启动提示符处手动输入 `ide-scsi` 参数，或者在 `/etc/grub.conf` 或 `/etc/lilo.conf` 文件中进行自动设置。参数在系统启动时注册。列出每个需要使用 `ide-scsi` 模块模拟 SCSI 驱动器的 CD 或 DVD 驱动器。

以下示例引导 `ide-scsi` 模块让次级连接 `hdc` 上的主 IDE 驱动器模拟 SCSI 驱动器：

```
hdc=ide-scsi
```

## Grub 和 CD 写入器

如果你在连接好 IDE CD-R/RW 驱动器时安装了 Red Hat，GRUB 会自动检测它并在其引导参数中列出 `ide-scsi` 模块。你始终可以在启动电脑时在显示的 Linux 系统 GRUB 引导项处通过输入它来手动输入参数。

以下示例显示如何在 Linux 启动提示符处指定两个 IDE 驱动器：

```
grub append root=/dev/hd3 hdc=ide-scsi
```

## 创建文件系统

Linux 提供了多种工具用于创建文件系统、设置交换区和管理分区。

### `fdisk`

要启动 `fdisk`，使用磁盘名称：

```
fdisk /dev/hdb
```
