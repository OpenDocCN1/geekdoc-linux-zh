
对于在 `/etc/fstab` 中有条目的任何分区，你只需要使用其 `fstab` 条目指定的挂载目录即可挂载该分区；你不需要设备文件名。`mount` 命令会在 `fstab` 文件中查找该分区的条目，使用目录来识别条目，并以此方式找到设备名称。例如，要挂载上示例中的 `/dev/hda1` Windows 分区，`mount` 命令只需要知道它要被挂载的目录——在本例中为 `/mnt/windows`。

```bash
# mount /mnt/windows
```

如果你不确定磁盘包含什么种文件系统类型，可以使用 `-t` 选项指定自动（`auto`）文件系统类型进行挂载。在给定自动文件系统类型的情况下，`mount` 会尝试自动检测磁盘上的文件系统类型。这在你手动挂载不熟悉的软盘系统类型时非常有用（`HAL` 硬件抽象层也会自动检测任何可移动介质（包括软盘）的文件系统类型）。

```bash
# mount -t auto /dev/fd0 /media/floppy
```

## mount 命令

如果你想用一个文件系统替换另一个，必须先显式卸载已挂载的。假设你挂载了一张软盘，现在想将其取出并放入一张新的。在放入并挂载新软盘之前，你必须卸载该软盘。`unmount` 命令可以接受设备名称或其挂载目录作为参数。语法如下：

```bash
# unmount device-or-mountpoint
```

示例显示了在软盘所在的位置进行卸载：

```bash
# unmount /dev/fd0
```

在设备挂载到 `/mydir` 目录的示例中，你可以使用该目录来卸载文件系统：

```bash
# unmount /mydir
```

`unmount` 命令有一个固有的限制：你无法卸载当前正在使用的文件系统。如果你切换到一个文件系统内部的目录并尝试卸载它，你会收到文件系统正忙的错误。例如，假设 CD-ROM 挂载在 `/media/disk` 目录，然后你切换到了 `/media/disk` 目录。如果你决定更换 CD-ROM，必须先用 `unmount` 命令卸载当前的。由于你正处于其挂载的目录中，操作将失败。你必须离开该目录才能卸载 CD-ROM。

```bash
# mount /dev/hdc /media/disk
# cd /media/disk
# unmount /media/disk
unmount: dev/hdc: device is busy

# cd /root
# unmount /media/disk
```

> **TIP** 如果其他用户正在使用你尝试卸载的文件系统，可以使用 `lsof` 命令找出是谁。

## 挂载软盘

如前所述，要访问软盘上的文件，必须先将磁盘挂载到你的 Linux 系统。软驱器设备名称为 `fd0`，位于 `/dev` 目录。输入 `/dev/fd0` 指的是你的软驱器。注意 `fd` 后的数字 `0`。如果你有多个软驱器，额外的驱动器由 `fd1`、`fd2` 等表示。你可以挂载到任何目录。某些发行版为软盘创建了方便的目录 `/media/floppy`。以下示例将软驱器挂载到 `/media/floppy` 目录：

```bash
# mount /dev/fd0 /media/floppy
```

> **Tip** 在 `GNOME` 中，你可以通过右键点击桌面显示桌面菜单，然后在磁盘（Disk）条目中选择 `Floppy` 来挂载软驱器。要卸载，右键点击软盘图标并在弹出菜单中选择弹出（Eject）。

记住，你挂载的是特定的软盘，而不是软驱器。你不能简单地取出软盘并放入另一张。`mount` 命令已将这些文件连接到你的主目录树，你的系统期望在软驱器的软盘上找到文件。如果你取出磁盘并放入另一张，你会收到错误。`unmount` 命令可以接受设备名称或其挂载目录作为参数。语法如下：

```bash
# unmount device-or-mountpoint
```

示例显示了在软盘所在的位置进行卸载：

```bash
# unmount /dev/fd0
```

在设备挂载到 `/mydir` 目录的示例中，你可以使用该目录来卸载文件系统：

```bash
# unmount /mydir
```

`unmount` 命令有一个固有的限制：你无法卸载当前正在使用的文件系统。如果你切换到一个文件系统内部的目录并尝试卸载它，你会收到文件系统正忙的错误。例如，假设 CD-ROM 挂载在 `/media/disk` 目录，然后你切换到了 `/media/disk` 目录。如果你决定更换 CD-ROM，必须先用 `unmount` 命令卸载当前的。由于你正处于其挂载的目录中，操作将失败。你必须离开该目录才能卸载 CD-ROM。

```bash
# mount /dev/hdc /media/disk
# cd /media/disk
# unmount /media/disk
unmount: dev/hdc: device is busy

# cd /root
# unmount /media/disk
```

> **TIP** 如果其他用户正在使用你尝试卸载的文件系统，可以使用 `lsof` 命令找出是谁。

## 挂载软盘

如前所述，要访问软盘上的文件，必须先将磁盘挂载到你的 Linux 系统。软驱器设备名称为 `fd0`，位于 `/dev` 目录。输入 `/dev/fd0` 指的是你的软驱器。注意 `fd` 后的数字 `0`。如果你有多个软驱器，额外的驱动器由 `fd1`、`fd2` 等表示。你可以挂载到任何你想要的目录。某些发行版为软盘创建了方便的目录 `/media/floppy`。以下示例将软驱器挂载到 `/media/floppy` 目录：

```bash
# mount /dev/fd0 /media/floppy
```

> **Tip** 在 `GNOME` 中，你可以通过右键点击桌面背景显示桌面菜单，然后在磁盘（Disk）条目中选择 `Floppy` 来挂载软驱器。要卸载，右键点击软盘图标并在弹出菜单中选择弹出（Eject）。

记住，你挂载的是特定的软盘，而不是软驱器。你不能简单地取出软盘并放入另一张。`mount` 命令已将这些文件连接到你的主目录树，你的系统期望在软驱器的软盘上找到文件。如果你取出磁盘并放入另一张，你会收到错误。`unmount` 命令可以接受设备名称或其挂载目录作为参数。语法如下：

```bash
# unmount device-or-mountpoint
```

示例显示了在软盘所在的位置进行卸载：

```bash
# unmount /dev/fd0
```

在设备挂载到 `/mydir` 目录的示例中，你可以使用该目录来卸载文件系统：

```bash
# unmount /mydir
```

`unmount` 命令有一个固有的限制：你无法卸载当前正在使用的文件系统。如果你切换到一个文件系统内部的目录并尝试卸载它，你会收到文件系统正忙的错误。例如，假设 CD-ROM 挂载在 `/media/disk` 目录，然后你切换到了 `/media/disk` 目录。如果你决定更换 CD-ROM，必须先用 `unmount` 命令卸载当前的。由于你正处于其挂载的目录中，操作将失败。你必须离开该目录才能卸载 CD-ROM。

```bash
# mount /dev/hdc /media/disk
# cd /media/disk
# unmount /media/disk
unmount: dev/hdc: device is busy

# cd /root
# unmount /media/disk
```

> **TIP** 如果其他用户正在使用你尝试卸载的文件系统，可以使用 `lsof` 命令找出是谁。

## 挂载软盘

如前所述，要访问软盘上的文件，必须先将磁盘挂载到你的 Linux 系统。软驱器设备名称为 `fd0`，位于 `/dev` 目录。输入 `/dev/fd0` 指的是你的软驱器。注意 `fd` 后的数字 `0`。如果你有多个软驱器，额外的驱动器由 `fd1`、`fd2` 等表示。你可以挂载到任何你想要的目录。某些发行版为软盘创建了方便的目录 `/media/floppy`。以下示例将软驱器挂载到 `/media/floppy` 目录：

```bash
# mount /dev/fd0 /media/floppy
```

> **Tip** 在 `GNOME` 中，你可以通过右键点击桌面背景显示桌面菜单，然后在磁盘（Disk）条目中选择 `Floppy` 来挂载软驱器。要卸载，右键点击软盘图标并在弹出弹出菜单中选择弹出（Eject）。

记住，你挂载的是特定的软盘，而不是软驱器。你不能简单地取出软盘并放入另一张。`mount` 命令已将这些文件连接到你的主目录树，你的系统期望在软驱器的软盘上找到文件。如果你取出磁盘并放入另一张，你会收到错误。`unmount` 命令可以接受设备名称或其挂载目录作为参数。语法如下：

```bash
# unmount device-or-mountpoint
```

示例显示了在软盘所在的位置进行卸载：

```bash
# unmount /dev/fd0
```

在设备挂载到 `/mydir` 目录的示例中，你可以使用该目录来卸载文件系统：

```bash
# unmount /mydir
```
