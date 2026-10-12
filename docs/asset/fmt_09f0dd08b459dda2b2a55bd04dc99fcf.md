
# 分区、文件系统与文件 3

此命令在不显式卸载的情况下更新文件系统的挂载模式。

## 挂载 CD 或 DVD

CD 和 DVD 与硬盘有所不同，因为它们可能由由分区组成且挂载时不可写入。SUSE 中的 CD 或 DVD 现在是自动化的，因为系统在插入时会感知新磁盘。当你实际上尝试访问 CD 或 DVD 时，系统会自动为你挂载。

当这种情况发生时，SUSE 会在 `/media` 下动态创建一个代表你的光学设备的目录。根据你挂载的光学磁盘，`/media` 下会创建不同的目录。例如，如果了名为 SUSE_BIBLE 的 CD，将创建 `/media/SUSE_BIBLE` 目录，CD 将挂载在该目录下。同样，当你使用 USB 外部设备或“优盘”时，会出现类似 `/media/disk/VOLUME NAME` 的目录。

| 设备 | 起始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|
| /dev/sda | * | 1 | 1306 | 1049014+ | 83 | Linux |
| /dev/sda2 | | 1568 | 2104515 | 82 | Linux |
| swap / Solaris | | 1569 | 2906 | 1074785 | 83 | Linux |
| /dev/sda4 | | 2907 | 7296 | 35262675 | 83 | Linux |

现在插入设备：

```
# fdisk -l

Disk /dev/sda: 60.0 GB, 6001642880 bytes

255 heads, 62 sectors/track, 7296 cylinders

Units = 16065 * 512 = 8225280 bytes

Disk identifier: 0x00a7c9bnDevice Boot Start End Blocks Id System

/dev/sda1 * | 1306 | 10490013+ | 83 | Linux

/dev/sda2 | | 1568 | 2104515 | 82 | Linux

swap / Solaris | | 1569 | 2906 | 1074785 | 83 | Linux

/dev/sda4 | | 2907 | 7296 | 35262675 | 83 | Linux

Disk /dev/sdb: 128 MB, 134216656 bytes

32 heads, 62 sectors/track, 1009 cylinders

Units = 1984 * 512 = 1015808 bytes

Disk identifier: 0xe853db8bDevice Boot Start End Blocks Id System

/dev/sdb1 | | 1009 | 1000897 | 83 | Linux
```

因此该设备是 `/dev/sdb`，你可以挂载它，在其上创建一个新的文件系统，或者根据意愿进行挂载。

由于光驱设备没有分区，你访问的是整个设备。SUSE 会检测光驱设备并在 `/dev` 设备中创建一个合适的符号链接。该链接是 `/dev/cdrom`，它可能是指向（例如）IDE 设备的 `/dev/hdc` 或指向 SCSI/SATA 设备的 `/dev/sr0`。事实上，取决于设备的功能，通常会有多个指向光驱设备的链接。如果它是一个刻录机，它还可能是 `/dev/cdrw`；如果你可以读取 DVD，那么

你可以使用这样的命令挂载 CD-ROM：

```
# mount /dev/cdrom /mnt
```

SUSE 现在使用硬件抽象层 (HAL)、`udev` 和 `sysfs` 来处理硬件并自动感应插入计算机的介质。如果你使用 KDE 或 Gnome 桌面，插入新的 CD-ROM 或外部磁盘可能会导致屏幕弹出警报，并且文件管理器（Konqueror 或 Nautilus）会在屏幕上显示介质内容。

## SUSE 自动挂载文件系统

`/etc/fstab` 文件用于存储为系统永久定义的文件系统信息。这包括交换分区和根分区，以及安装期间创建的任何分区。如果你创建了将永久使用的新分区，并在每次系统启动时将其集成到系统中，那么 `fstab` 文件将非常有用。在启动过程中，系统会初始化挂载 `fstab` 文件中的所有文件系统，除非在特定文件系统的选项中添加了 `noauto` 选项。

在这个示例中，我们创建了一个新的 Reiser 文件系统，并在每次系统启动时自动将其挂载到 `/spare` 下。

要编辑 `/etc/fstab` 文件或类似文件，你需要使用文本编辑器。有关编辑的更多信息，请参考第 11 章。

要添加启动时自动挂载的文件系统，需要在 `fstab` 文件中添加一行，指定分区、挂载点、文件系统类型、你的选项以及关于备份和挂载顺序的系统信息：

```
/dev/sda2 /spare reiserfs default 0 0
```

可以通过原始设备名称（如 `/dev/sda2`）指定设备，可以使用基于 ID 的命名法（如 `/dev/disk/by-id/`，这是安装时的默认设置）。使用该方法，上述行可能像这样：

```
/dev/disk/by-id/scsi-SATA_Hitachi_HTS7210_MPC3B2YJGUMOE-2 /space reiserfs default 0 0
```
