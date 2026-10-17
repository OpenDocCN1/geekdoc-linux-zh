
当你刻刻 CD 时，你可能需要创建一个 CD 镜像文件。你可以从硬盘访问此类镜像文件，将其挂载为另一个文件系统（即使是提取的镜像也可以挂载）。为此，请使用 `loop` 选项并指定一个打开的 loop 设备，如 `/dev/loop0`。如果没有检测到 loop 设备，`mount` 会尝试寻找打开的。文件类型为 `iso9660`。

```
# -t iso9660 -o loop=/dev/loop0 image-file -mnt-directory
```

要将文件 `myymic.cdimage` 挂载到 `/mnt/mystuff` 目录并将其设置为只读，你会使用：

```
# -t iso9660 -o ro=/dev/loop0 myymic.cdimage /mnt/mystuff
```

一旦挂载，你就可以像访问任何目录一样访问 CD-ROM 上的文件。

提示 你可以使用 `mkisofs` 根据你的文件或另一个 CD-ROM 创建 CD-ROM 镜像。

## 挂载硬盘分区：Linux 和 Windows

你可以使用 `mount` 命令挂载 Linux 或 Windows 硬盘分区。然而，使用之前提到的 `/etc/fstab` 文件让它们自动挂载更具实用性。你在安装期间创建的 Linux 分区已经自动为你挂载了。正如之前提到的，要挂载 Linux 磁盘分区，请输入 `mount` 命令，并带有该分区的设备名称以及你想要挂载的目录。IDE 硬盘使用前缀 `hd`，并且

![](img/70a65fc8f3408711ddea7ea368f31720_688_0.png)

SCSI 硬盘使用前缀 `sd`。接下来的示例将 `/dev/hda4` 上的 Linux 硬盘分区挂载到目录 `/mnt/mydata`：

```
# mount ext3 /dev/hda4 /mnt/mydata
```

你也可以直接挂载 Windows 分区。在 Linux 中，你使用 `mount` 命令，但也必须指定文件系统类型为 Windows。为此，请使用 `-t` 选项，然后对 Windows 95/98/ME 使用 `vfat`（MS-DOS 使用 `msdos`）。对于 Windows XP、2000 和 NT，你应该使用 `ntfs`（具有完全的只读访问和有限的写访问权限）。在下一个示例中，用户将 Windows 磁盘分区 `/dev/hdl` 挂载到 Linux 文件结构下的 `/mnt/windows`。`/mnt/windows` 目录是 Windows 文件系统的常用命名，尽管你可以将其挂载到任何目录（例如用于 MS-DOS 的 `/mnt/dos`）。如果你有多个分区，可以创建一个 Windows 目录，然后使用驱动器的标签或字母为每个驱动器创建一个子目录，例如 `/mnt/windows/a` 或 `/mnt/windows/mystuff`。请确保在挂载文件之前已经创建了该目录。

```
# mount -t vfat /dev/hdl /mnt/windows
```

## 安装 IDE CD-R/RW 和 DVD-R/RW 设备

在当前的 2.6 内核中（现在包含了 SG_io），Linux CD 刻录程序会将 CD-R/RW 和 DVD-R/RW 驱动器视为相应的 IDE 或 SCSI 驱动器。这意味着 IDE CD-R/RW 驱动器不再需要模拟 SCSI 驱动器即可被刻刻录软件识别和使用。如果你想在刻录程序中使用 IDE CD-ROM 或 DVD-ROM——例如仅作为复制 CD 磁盘的读取器——该 IDE CD-ROM 可以作为 IDE 设备引用，例如 `/dev/hdc`。SCSI 驱动器将通过其设备名称引用，例如 `/dev/scsi0`。

> 注意 从 Fedora Core 2 开始，使用 SG_io 改进 I/O 支持消除了 IDE CD-R 和 DVD-R 驱动器模拟 SCSI 设备的需要。该支持由内核实现。

要检查你的 IDE/CD 驱动器是否被识别，请使用带有 `-scanbus` 选项的 `cdrecord`。

## 创建文件系统：mkfs, mkfs, mkswap, parted 和 fdisk

Linux 提供了多种工具来创建和管理文件系统，让你能够添加新的硬盘分区、CD 镜像并格式化。要使用新硬盘，你必须先对其进行分区，然后在上面创建文件系统。你可以使用 `parted` 或 `fdisk` 对硬盘进行分区。要在分区上创建文件系统，请使用 `mkfs` 命令，它是各种文件系统构建器的前端。对于交换分区，使用特殊工具 `mkswap`；在 CD-ROM 上创建文件系统，使用 `mkisoimage` 工具。要启动 `fdisk`，在命令行输入硬盘设备名称输入 `fdisk`。这是一个交互式程序，可以使用它创建 Linux 分区。小心使用 `fdisk`，它可以删除整个磁盘分区。

表 32-10 Linux 分区和文件创建工具

| 工具 | 描述 |
| --- | --- |
| fdisk | 用于创建和删除分区的菜单驱动程序。 |
| cfdisk | fdisk 的基于屏幕界面。 |
| parted | GNU 分区管理工具。 |
| mkfs | 在分区或软磁盘上创建文件系统。它是格式化工具的前端。 |
| mke2fs | 在 Linux 分区上创建 ext2 文件系统；使用 `-j` 选项创建 ext3 文件系统。 |
| mkfs.ext3 | 在 Linux 分区上创建 ext3 文件系统。 |
| mkfs.ext2 | 在 Linux 分区上创建 ext2 文件系统。 |
| mkfs.reiserfs | 在 Linux 分区上创建 Reiser 文件系统（链接到 mreiserfs）。 |
| mkfs.jfs | 在 Linux 分区上创建 JFS 文件系统。 |
| mkfs.xfs | 在 Linux 分区上创建 XFS 文件系统。 |
| mkfs.dos | 在指定的分区上创建 DOS 文件系统。 |
| mkfs.vfat | 在指定的分区上创建 Windows 16 位文件系统（Windows 95、98 和 ME）。 |
| mkfs.ams | 创建压缩闪存系统，只读（用于嵌入设备）。 |
| mkswap | 在设备或文件中设置 Linux 交换区的工具。 |
| dosfs | 在 Linux 下创建 MS-DOS 文件系统。 |
| mkisofs | 创建 ISO CD-ROM 磁盘。 |
| dump2fs | 显示文件系统的底层块信息。 |
| gloppy | 格式化软磁盘的 GNOME 工具（系统工具中的软磁盘格式化程序）。 |
| ext2online | 使用磁盘上闲空间扩展分区大小的工具。 |
| hdparm | IDE 硬盘调节器，设置 IDE 硬盘功能。 |
| tune2fs | 调节文件系统，设置标签、日志和预留空间等功能。 |

### fdisk

以下命令调用 `fdisk` 在 `hdb` 硬盘上创建分区：

```
fdisk /dev/hdb
```

分区有不同的类型需要你指定。`fdisk` 是一个面向行的程序。它有一组只需按的单字符命令。可能会被提示输入某些信息并按回车。如果你在 `fdisk` 过程中遇到问题，可以随时按 `q` 返回上一个屏幕，而不进行任何更改。在你按下 `w` 之前，对硬盘不会进行任何实际更改。这应该是你的最后一个命令；它会对硬盘进行实际更改并退出 `fdisk`，返回到安装程序。表 32-11 列出了常用的 `fdisk` 命令。

执行以下步骤创建 Linux 分区：

当你按 `n` 定义新分区时，它将被标记为主分区。Linux 支持多四个主分区。输入你正在创建的分区号。输入分区的起始磁道。这是提示末尾括号中的第一个数字。然后你会被提示输入磁道数。你可以输入该分区的最后一个磁道，也可以输入一个大小。输入 `+1000M` 表示 1GB，数量前加 "+"。注意大小不能超过你的可用空间。指定分区类型。Linux 分区的默认类型是 83。如果你正在创建不同类型的分区（例如交换分区），按 `t` 指定你想要的类型。输入分区号，交换分区为 82。完成后，按 `w` 将更改写入硬盘，然后按回车继续。

作为 `fdisk` 的替代方案，你可以使用 `parted` (`www.gnu.org/software/parted`)。`parted` 让你管理硬盘分区、创建新的和删除旧的。与 `fdisk` 不同，它调整分区大小。要在指定硬盘的分区上使用 `parted`，该硬盘上的所有分区都不能处于使用状态。这意味着如果你想使用与内核位于同一硬盘上的分区，你必须以救援模式启动系统并选择不挂载系统文件。对于任何其他硬盘，你只需要卸载分区并使用 `swap` 命令关闭。然后你可以通过 `parted` 命令和要处理的硬盘设备名称启动 `parted`。以下是针对硬盘的 `parted` 示例：

```
/dev/hda
```

你使用 `print` 命令列出所有分区。每个分区的分区号将列在 Minor 标题下的第一列。Start（开始）和 End（结束）列列出了分区在硬盘上使用的起始位置。

| 命令 | 操作 |
| --- | --- |
| a | 切换布尔标记 |
