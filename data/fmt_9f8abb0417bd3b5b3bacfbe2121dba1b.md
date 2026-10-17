
```
# umount /mydir
```

`umount` 命令有一个重要的约束。你永远无法卸载当前正在其中工作的文件系统。如果你切换到某个文件系统内的目录，然后尝试卸载该文件系统，你会收到一条错误消息，指出该文件系统正忙。例如，假设你将 CD-ROM 挂载到 `/mnt/cdrom` 目录，然后切换到该 `/mnt/cdrom` 目录。如果你决定更换 CD-ROM，你首先必须使用 `umount` 命令卸载当前的 CD-ROM。这将会失败，因为你正处在该目录中。

目前在挂载它的目录中。你必须先离开该目录，然后才能卸载 CD-ROM。

```
# mount /dev/hdc /mnt/cdrom
# cd /mnt/cdrom
# umount /mnt/cdrom
umount: /dev/hdd: device is busy
# cd /root
# umount /mnt/cdrom
```

> 提示 如果其他用户正在使用你尝试卸载的文件系统，你可以使用 `lsof` 或 `fuser` 命令来找出他们是谁。

## 挂载软盘

如前所述，要访问软盘上的文件，该磁盘首先必须在你的 Linux 系统上挂载。你的软盘驱动器的设备名为 `fd0`，位于 `/dev` 目录中。输入 `/dev/fd0` 即可引用你的软盘驱动器。注意 `fd` 后面的数字 `0`。如果有多于一个软盘驱动器，额外的驱动器将表示为 `fd1`、`fd2` 等。你可以挂载到任何你想要的目录。Red Hat 创建了一个方便用于软盘的目录 `/mnt/floppy`。以下示例将软盘驱动器中的软盘挂载到 `/mnt/floppy` 目录：

```
# mount /dev/fd0 /mnt/floppy
```

> 提示 在 GNOME 上，你可以通过右键单击桌面背景显示桌面菜单，然后在磁盘条目中选择软盘来挂载软盘驱动器。要卸载，请右键单击软盘图标并从弹出菜单中选择弹出。

记住，你挂载的是特定的软盘，而不是软盘驱动器。你不能简单地取出软盘并放入另一张。`mount` 命令已将这些文件附加到你的主目录树中，你的系统期望在软盘驱动器中找到这些文件在软盘上。如果你取出磁盘并放入另一张，当你尝试访问它时会收到错误消息。

要更换磁盘，你必须首先卸载已在磁盘驱动器中的软盘。然后，在放入新磁盘后，你必须显式挂载该新磁盘。为此，使用 `umount` 命令。

```
# umount /dev/fd0
```

对于 `umount` 或 `mount` 操作，你可以指定它所挂载的目录或 `/dev/fd0` 设备。

```
# umount /mnt/floppy
```

现在你可以取出软盘，放入新的，然后挂载它：

```
# mount /mnt/floppy
```

当你关闭系统时，任何已挂载的磁盘都会自动卸载。你无需显式卸载它。

## 挂载 CD-ROM

记住，当你挂载 CD-ROM 或软盘时，不能简单地取出它以便在驱动器中放入另一张。你首先必须卸载它，将文件系统从整体目录树中分离。事实上，CD-ROM 驱动器在你卸载它之前保持锁定状态。一旦你卸载 CD-ROM，你就可以取出它并放入另一张，然后必须挂载后才能访问它。在更换多个 CD-ROM 或软盘时，你会不断地挂载和卸载它们。对于 CD-ROM，除了使用 `umount` 命令外，你还可以使用 `eject` 命令并指定设备名称或挂载点，它将卸载然后弹出 CD-ROM。

你也可以使用 `mount` 命令将 CD-ROM 磁盘挂载到你的 Linux 系统。在许多发行版中，目录 `/mnt/cdrom` 已保留用于 CD-ROM 文件系统。你可以在本章前面介绍的 `/etc/fstab` 文件中看到此条目。有了这样的条目，要挂载 CD-ROM，你只需输入命令 `mount` 和目录 `/mnt/cdrom`。你无需指定设备名称。一旦挂载，你就可以通过 `/mnt/cdrom` 目录访问 CD-ROM。

```
# mount /mnt/cdrom
```

> 提示 在 GNOME 上，CD-ROM 会自动挂载，不过你也可以通过右键单击桌面背景显示桌面菜单，然后在磁盘条目中选择 CD-ROM 来手动挂载它们。要卸载，请右键单击 CD-ROM 图标并从弹出菜单中选择弹出。

```
# umount /mnt/cdrom
```

如果你想将 CD-ROM 挂载到另一个目录，你必须在 `mount` 命令中包含设备名称。以下示例将 CD-ROM 驱动器中的光盘挂载到 `/mydir` 目录。此示例中 CD-ROM 的特定设备名称为 `/dev/hdc`。

```
# mount /dev/hdc /mydir
```

当你刻录 CD 时，你可能需要创建一个 CD 映像文件。你可以从硬盘访问此类映像文件，就像它是一个文件系统一样挂载它（甚至是被抓取的映像也可以这样挂载）。为此，你使用 `loop` 选项，指定一个开放的 loop 设备，如 `/dev/loop0`。如果未指示 loop 设备，`mount` 将尝试找到一个空闲的。文件系统类型为 `iso9660`，一种 CD-ROM iso 映像文件类型。

安装完成后，你可以像访问任何目录一样访问 CD-ROM 上的文件。

Tip 你可以使用 `mkisofs` 来创建由你的文件或另一张 CD-ROM 组成的 CD-ROM 映像。

## 挂载硬盘分区：Linux 和 Windows

你可以使用 `mount` 命令挂载 Linux 或 Windows 硬盘分区。然而，使用 `/etc/fstab` 文件自动挂载它们更为实用，如前所述。你在安装期间创建的 Linux 硬盘分区已经为你自动挂载了。如前所述，要挂载 Linux 硬盘分区，请使用分区设备名和要挂载到的目录输入 `mount` 命令。IDE 硬盘使用前缀 `hd`，SCSI 硬盘使用前缀 `sd`。下一个示例将 Linux 硬盘分区 `/dev/hda4` 挂载到目录 `/mnt/mydata`：

```
# mount -t ext3 /dev/hda4 /mnt/mydata
```

你也可以挂载 Windows 分区并直接访问其上的文件。与 Linux 分区一样，你使用 `mount` 命令，但你还必须指定文件系统类型为 Windows。为此，使用 `-t` 选项，然后为 Windows 95/98/ME 输入 `vfat`（`vfat` 用于 MS-DOS）。对于 Windows XP、2000 和 NT，你将使用 `ntfs`（仅限只读访问；写访问为实验性，不推荐）。在下一个示例中，用户将 Windows 硬盘分区 `/dev/hda1` 挂载到 Linux 文件结构中的目录 `/mnt/windows`。`/mnt/windows` 目录是 Windows 文件系统的常用名称，尽管你可以将其挂载到任何目录（例如 `/mnt/dos` 用于 MS-DOS）。如果你有多个 Windows 分区，你可以创建一个 Windows 目录，然后为每个驱动器使用驱动器标签或字母创建子目录，例如 `/mnt/windows/a` 或 `/mnt/windows/mystuff`。请确保在挂载文件系统之前已创建该目录。

```
# mount -t vfat /dev/hda1 /mnt/windows
```

## 安装 IDE CD-R/RW 和 DVD R/RW 设备

Linux CD 刻录应用程序都将 CD-R/RW 和 DVDR/RW 驱动器视为 SCSI 驱动器。这意味着 IDE CD-R/RW 驱动器必须模拟 SCSI 驱动器，才能被 CD 或 DVD 写入软件识别和使用。即使你只想在 CD 写入应用程序中使用 IDE CD-ROM 或 DVD-ROM——例如仅作为读取器来复制 CD 光盘——该 IDE CD-ROM 驱动器仍必须模拟 SCSI CD-ROM 驱动器。只有 SCSI 驱动器（CD-R/RW/ROM 或 DVDR/RW/ROM）才会被 Linux CD 或 DVD 写入软件识别。例如，如果你有一个普通的 IDE CD-ROM 并希望将其与 Linux CD 刻录软件一起使用来复制 CD（抓取），你仍必须让该 IDE CD-ROM 模拟 SCSI CD-ROM。请查阅 `www.tldp.org` 上的 CD-Writing HOW-TO 了解更多详情。下面提供简要说明。

Tip IDE 设备的 SCSI 模拟在内核中作为 ATA/IDE/MFM/RLL 支持窗口中 IDE、ATA 和 ATAPI 块设备条目下的 SCSI 模拟支持来实现，该窗口从主内核配置菜单打开。通常，它被编译为模块。

IDE CD 和 DVD 驱动器（CD-R/RW/ROM 或 DVDR/RW/ROM）在安装期间被识别为 IDE 设备并作为此类安装。然而，当你启动系统时，你需要指示 Linux 内核让 IDE CD 和 DVD 驱动器模拟 SCSI CD 或 DVD 驱动器。这意味着通常会被识别为 `/dev/hdc` 驱动器的 CD-R 驱动器必须被识别为 `/dev/scd0` 设备，即第一个 SCSI CD-ROM 驱动器。你通过加载 `ide-scsi` 模块来实现这一点，该模块允许 IDE CD 驱动器模拟 SCSI CD 驱动器。

## SCSI 模拟
