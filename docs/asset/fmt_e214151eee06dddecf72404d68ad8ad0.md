
Linux 可以在硬硬盘分区上为 ext2 和 ext3 文件系统使用文件系统标签。因此，在所示的 `/etc/fstab` 文件中，第一个条目使用标签作为其设备名称，所示。在这种情况下，标签是斜杠 `/`，表示根分区。你可以使用 `e2label` 更改此设备的标签，但务必更改其在 `/etc/fstab` 中的条目。

```
LABEL=/ /  ext3 defaults 0 1
```

对于 ext2 和 ext3 分区，你可以使用 `e2label` 工具或带有 `-L` 选项的 `tune2fs` 来更改或添加标签。指定设备和标签名称。如果你更改了标签，确保更改 `/etc/fstab` 文件中对应的条目。只需使用设备名配合 `e2label` 来查找当前标签。在下一个示例中，用户将 `/dev/hda3` 的标签更改为 TURTLE：

```
e2label /dev/hda3 TURTLE
```

# Windows 分区

Windows 分区在 `/media` 目录下使用 NTFS-3 驱动程序自动检测和监控。然而，如果你需要，可以手动挂载 Windows 分区，对于服务器系统你可能需要这样做。你可以将 MS-DOS: Windows 95/98/Me 挂载到你的 Linux 文件结构中，就像你想对待任何 Linux 文件系统一样。你必须为 Windows 95/98/Me 指定 `vfat` 类型，为 MS-DOS 指定 `msdos` 类型。Windows XP、Vista、NT 和 2000 使用 `nfs` 文件类型。要让你手动挂的分区自动挂载，你需要在 `/etc/fstab` 文件中为你的 Windows 分区添加条目，并赋予其 `defaults` 选项或确保使用 `auto` 选项。你指定分区的设备名，然后是你想挂载它的目录。下一个示例显示了 `/etc/fstab` 文件中的 Windows 95/98/Me (vfat) 条目。注意 `/etc/fstab` 文件中的最后一个条目是监控 Windows 分区的条目。

```
/dev/hd1 /mnt/windows vfat defaults 0 0
```

```
/dev/hd2 /mnt/windows ntfs-3g defaults 0 0
```

NTFS-3G 驱动程序使用用户空间文件系统（FUSE）。FUSE 在用户空间实现虚拟文件系统，作为内核文件系统管理操作的连接。通过 NTFS-3G，用户为 NTFS 分区设置虚拟文件系统。

# 第 23 章：文件系统

## 手动挂载文件系统

### 挂载命令

`mount` 命令载。在 `/media` 目录下使用 NTFS-3 驱动程序自动检测和监控 Windows 分区。然而，如果你需要，可以手动挂载 Windows 分区，对于服务器系统你可能需要这样做。你可以将 MS-DOS: Windows 95/98/Me 挂载到你的 Linux 文件结构中，就像你想对待任何 Linux 文件系统一样。你必须为 Windows 95/98/Me 指定 `vfat` 类型，为 MS-DOS 指定 `msdos` 类型。Windows XP、Vista、NT 和 2000 使用 `nfs` 文件类型。要让你手动挂的分区自动挂载，你需要在 `/etc/fstab` 文件中为你的 Windows 分区添加条目，并赋予其 `defaults` 选项或确保使用 `auto` 选项。你指定分区的设备名，然后是你想挂载它的目录。下一个示例显示了 `/etc/fstab` 文件中的 Windows 95/98/Me (vfat) 条目。注意 `/etc/fstab` 文件中的最后一个条目是监控 Windows 分区的条目。

使用设备挂载在 `/mydir` 目录的示例，你可以使用该目录来卸载文件系统：

```
sudo umount /mydir
```

`umount` 命令有一个重要的限制：你永远无法卸载当前正在使用的文件系统。如果你切换到一个正尝试卸载的文件系统内部的目录，你将收到一条提示文件系统正忙（busy）的错误消息。假设一个 CD-ROM 挂载在 `/media/disk` 目录，然后你切换到了该 `/media/disk` 目录。如果你决定更换 CD-ROM，你必须先使用 `umount` 命令卸载当前的设备。这将失败，因为你当前正在挂载点的目录中工作。在挂载 CD-ROM 之前，你必须离开该目录。这里是一个示例：

```
sudo mount /dev/hdc /media/disk
cd /media/disk
umount /media/disk
umount /dev/hdc: device is busy
cd /root
umount /media/disk
```

> 提示：如果其他人正在使用你尝试卸载的文件系统，你可以使用 `lsof` 或 `fuser` 来查找他们是谁。

## 管理 CD/DVD、USB 驱动器和软盘

相反，如果你想从命令行通过 `mount` 命令手动挂载驱动器，你首先需要决定一个挂载它的目录（如果该目录不存在，你可以创建它）。`/media/disk` 目录会在插入磁盘时动态创建，并在移除时被删除。要使用 `mount` 命令手动挂载磁盘，请指定设备名称为 `/dev/cdrom` 以及要挂载的目录：

```
# mount /dev/cdrom /media/cdrom1
```

如果你想从命令行手动卸载该名称，可以使用 `umount` 命令以及挂载该文件的的目录名：

```
# umount /media/cdrom1
```

### 第七部分：系统管理

或者如果是由 HAL 挂载的，你可以使用此命令：

```
# umount /media/disk
```

当你刻录一张 CD 时，你可能需要创建一个 CD 镜像文件。你可以从硬盘访问此类镜像，将其挂载为就像另一个文件系统一样（即使是刻录的镜像也可以通过这种方式挂载）。为此，你使用 `loop` 选项，并指定一个打开的 loop 设备为 `/dev/loop0`。如果没有指定 loop 设备，mount 将尝试寻找一个打开的设备。文件系统类型为 iso9660，一种 CD-ROM ISO 镜像类型：

```
# -t iso9660 -o loop=/dev/loop0 image-file mount-directory
```

要将文件 mymycdimage 挂载到 `/mnt/mystuff` 目录并将其设置为只读，你将使用：

```
# -t iso9660 -o loop=/dev/loop0 mymycdimage.cdimage /mnt/mystuff
```

一旦镜像文件挂载，你就可以像访问任何目录一样访问 CD-ROM 上的文件。

> 你使用 `mkisofs` 创建由你的文件或其他 CD-ROM 的 CD-ROM 镜像。

## 硬盘分区：Linux 和 Windows

你可以使用 `mount` 命令挂载 Linux 或 Windows 硬盘分区。然而，使用上述的 `/etc/fstab` 文件将它们自动挂载更为实用。在安装期间创建的 Linux 硬盘分区会自动挂载。如所述，要挂载 Linux 硬盘分区，请输入 `mount` 命令，并带有分区的设备名称以及你想将其挂载的目录。IDE 硬盘使用 hd 前缀，SCSI 驱动器使用 sd 前缀。下一个示例显示将你的硬盘分区 `/dev/hda4` 挂载到目录 `/mnt/mydata`：

```
# mount -t ext3 /dev/hda4 /mnt/mydata
```

## 挂载 DVD/CD 镜像

挂载 DVD/CD 磁盘镜像同样通过 `mount` 命令执行，但需要使用 loop 设备。如下一个示例所示，使用 `loop` 选项指定 loop 设备。在这里，mydociso 被挂载到 `/media/cdrom`，文件系统类型为 iso9660。完成后请务必卸载。它可以挂载到你系统上的一个空目录。

```
# -t iso9660 -o loop=/dev/loop0 mydocuments.iso /media/mycdrom
```

## 创建文件系统：mkfs, mke2fs, mkswap, parted 和 fdisk

Linux 提供了多种创建和管理文件系统的工具，允许你添加新的硬盘分区、创建 CD 镜像并格式化软盘。要使用新硬盘，你首先必须对其进行分区并在上面创建文件系统。你可以使用：

`parted` 或 `fdisk` 对你的硬盘进行分区。然而，使用 parted 的 GUI 前端（如 GParted 和 QParted）可能会更容易且更安全。它们都提供了清晰的图形界面和易于使用的界面，用于管理、创建和删除文件系统。

要在分区上创建文件系统，你可以在终端窗口中使用 `mkfs` 命令，它是各种文件系统构建器的前端。对于交换分区，你使用特殊工具 `mkswap`，而要在 CD-ROM 上创建文件系统，你使用 `mkisofs` 工具。Linux 分区和文件系统工具如表 23-10 所示。

| 工具 | 说明 |
|---|---|
| cfdisk | 设置分区 |
| dumpe2fs | 显示文件系统信息 |
| fdisk | 分区 |
| GParted | GNOME 分区 |
| hdparm | IDE 特性 |
| mkfs | 创建文件系统 |
| mke2fs | 创建 ext2 |
| mkfs.ext2 | 创建 ext2 |
| mkfs.ext3 | 创建 ext3 |
| mkfs.bfs | 创建 bfs |
| mkfs.cramfs | 创建 RAMFS |
| mkfs.jext2 | 创建 ext2 |
| mkfs.reiserfs | 创建 ReiserFS |
| mkfs.msdos | 创建 MS-DOS |
| mkfs.vfat | 创建 vfat |
| mkswap | 创建交换区 |
| mkisofs | 创建 ISO 镜像 |
| parted | GNU 分区 |
| QParted | KDE 界面 |
| resize2fs | 扩展分区大小 |
| tune2fs | 调整文件系统 |

**表 23-10：Linux 分区和文件系统工具**

### 第七部分：系统管理

#### Parted 和 GParted

大多数用户使用 GNU Parted (`www.gnu.org/software/parted/index.html`) 管理硬盘分区、创建新分区并删除旧分区。与 Fdisk 不同，Parted 允许调整分区大小。在硬盘上使用 Parted 时，硬盘上的任何分区都不能被使用。这意味着如果你想对与内核同一硬盘上的分区使用 Parted，你必须以救援模式启动系统并选择不挂载你的系统文件。对于任何其他硬盘，你只需要卸载分区并使用 `swapoff` 命令关闭交换空间。

注意 QParted 的工作方式与 GParted 相同。你需要安装支持的 KDE 库。侧边栏显示可用磁盘。它还提供了分区的图形显示和可展开的树状结构。

e2fsprogs 用于 ext3 分区，nfsprogs 用于 NTFS 分区，两者都已随桌面发行光盘进行安装。更多信息请参阅 http://gparted.sourceforge.org。请记住，尽管 GParted 和 QTParted 已证明可靠，但它们仍在开发中。Parted 和 Fdisk 等命令行工具仍然是主要的分区工具。

图形化界面会显示所选磁盘上的分区情况，显示分区标签、设备名称以及每个分区的比例大小。你可以使用右上角的弹出菜单来选择系统上的分区。磁盘将通过其设备名称（例如 `/dev/sda`）和大小进行标识。Parted 的下半部分以可展开的树形结构显示所选驱动器的硬盘。每个分区的类型系统、挂载点和大小都会被显示出来。还会显示已用空间大小以及任何标记（如磁盘是否可启动）。从“视图”（View）菜单中，你可以选择显示所选设备的信息并列出将要执行的任务。

你可以创建、调整大小、格式化和删除分区。空闲空间将列为“未分配空间”。已挂载的分区在其条目上显示锁图标。如果你想对它们执行任何操作，必须先卸载。右键点击分区条目并在弹出菜单中选择“卸载”（Unmount）。

要创建分区，点击“新建”（New）按钮。这将打开“创建分区”窗口，你可以在其中指定分区大小、它是主分区还是扩展分区以及其文件系统类型。

要对分区进行操作，右键点击分区名称显示弹出菜单，你可以在其中选择这些任务。你也可以选择条目并在“格式化分区”（Format the partition）菜单中选择任务。格式化项会展开到另一个子菜单，列出所有支持的文件类型，如 nfs 或 ext3。删除分区将永久删除数据。如果两侧都有可用空间，你可以将分区调整为更大的尺寸。如果未使用空间位于分区内，则可以减小分区。调整大小窗口会显示可用空间并允许你更改大小。

你还可以添加磁盘标签和标记。要更改磁盘标签，选择“设备（Device） | 设置磁盘标签（Set Disklabel）”。磁盘标签为分区命名，允许你的系统通过标签而不是使用设备名称来引用它。这对于设备名称可能会发生但标签不会改变的可移动设备非常有帮助。标记指示分区的用途，例如可启动分区、使用 lvm 文件系统的 lvm，以及用于 RAID 阵列的 raid。

一旦完成所有更改，点击“应用”（Apply）按钮使更改生效。在点击“应用”按钮之前，任何更改都不会生效。

#### parted 命令

或者，你可以在终端窗口中使用 `parted` 命令来管理分区。你可以通过 `parted` 命令加上要操作的硬盘设备名称来启动 Parted。或者，你可以在 GNOME 上使用 GParted 或在 KDE 上使用 QTParted。以下示例为硬盘 `/dev/sda` 启动 parted：

```
parted /dev/sda
```

使用 `print` 命令列出所有的分区。每个分区的分区编号将列在“次要”（Minor）标题下的第一列中。“开始”（Start）列和“结束”（End）列列出了该分区在硬盘上使用的起始和结束位置。这些数字以兆字节为单位，从第一个兆字节到总可用空间。

要创建新分区，使用 `mkpart` 命令并指定主分区或扩展分区、文件系统类型以及起始和结束位置。你最多可以创建三个主分区和一个扩展分区（如果没有扩展分区，则可以创建四个主分区）。扩展分区反过来可以几个逻辑分区。一旦创建了分区，稍后可以使用 `mkfs` 用文件系统对其进行格式化。要调整分区大小，使用 `resize` 命令并指定分区编号以及起始和结束位置。你甚至可以使用 `move` 命令移动分区。`help` 命令列出所有命令。

##### Fdisk

启动 Fdisk，在命令行输入 `fdisk` 并加上硬盘的设备名称。使用 `/dev/sda`。

使用 `print` 命令列出你所有的分区。每个分区的分区编号将列在“次要”标题下的第一列中。“开始”和“结束”列列出了分区在硬盘上使用的起始和结束位置。这些数字以兆字节为单位，从第一个兆字节到总可用空间。

```
fdisk /dev/sda
```

在使用整个分区时要小心。在分区过程中，会提示你输入类型。交互式显示 fdisk。在不保存任何更改的情况下退出 fdisk。在创建分区时会显示交互式程序。

| 命令 | 操作 |
|---|---|
| a | 切换可启动标记 |
| l | 列出已知分区类型 |
| m | 列出命令 |
| n | 添加新分区 |
| p | 打印分区表 |
| q | 在不保存的情况下退出 |
| t | 分区系统 ID |
| w | 写入表并退出 |

表 23-11 常用 fdisk 命令

## mkfs

一旦你创建了分区，就可以为其创建一个文件系统。要为此，使用 `mkfs` 命令对分区进行格式化并将分区的名称作为参数。你必须通过 `mkfs` 命令指定其完整路径。

```
fdisk /dev/sda
```

| 选项 | 描述 |
|---|---|
| Blocks | 指定块数 |
| -c | 检查分区坏块 |
| file-system-options | 文件系统的选项 |
| -l | 读取坏块列表 |
| -t | 指定类型 |
| -V | 详细模式；显示每个操作 |
| -v | 指示文件系统显示 |

表 23-12 mkfs 参数

一旦你创建了分区，就可以为其创建一个文件系统。要为此，使用 `mkfs` 命令对分区进行格式化并将分区的名称作为参数。你必须通过 `mkfs` 命令指定其完整路径。

```
mkfs -t ext3 /dev/hdb
```

## mkswap

如果你想创建一个交换分区，首先使用 Fdisk 或 Parted 创建该分区（如果它不存在），然后使用 `mkswap` 命令将其格式化为交换分区。除非另有指示，否则 mkswap 会格式化整个分区。它接受交换分区设备名称作为参数：

```
mkswap /dev/hdb2
```

你需要在 `/etc/fstab` 文件中创建一个条目，以便在系统启动时自动挂载。

## CD/DVD 光刻

向 DVD/CD 光盘刻录数据现在由 GNOME 和 KDE 桌面直接处理。在空白的 DVD/CD 上进行简单的拖放操作即可刻录光盘。你也可以使用 GNOME 和 KDE 的刻刻应用程序，例如 Brasero。

GNOME（见第 3 章）和 KOnCD 用于创建你的 DVD/CD。所有这些都涉及 `mkisofs` 和 `cdrecord` 工具。在 DVD 刻录机上刻录 DVD，你可以针对 DVD-RW 设备使用 `cdrecord`，针对 DVD+/RW 设备使用 DVD+RW 工具。如果你想在 DVD 刻录机上刻录 CD-ROM，只需使用带有许多选项的 `cdrecord` 应用即可。

`cdrecord` 应用目前仅适用于 DVD-R/RW 驱动器；它是 `dvdtools` 软件包的一部分。如果你想使用 DVD+/RW 驱动器，请使用 DVD+ 工具，如 `growisofs` 和 `dvd-rw-format`。某些 DVD+RW 工具包含 dvd-rw 工具集中，更多信息请访问：http://fy.chalmers.com/~apro/linux/DVD+RW。
