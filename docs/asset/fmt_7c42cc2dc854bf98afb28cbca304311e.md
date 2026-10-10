
- `ZFS`：泽塔字节文件系统（`ZFS`）由 `Sun Microsystems`（现为 `Oracle` 的一部分）为其 `Unix` 工作站和服务器创建。这是另一种高性能文件系统，具有类似 `btrfs` Linux 文件系统的功能。

如果你计划仅将驱动器用于 Linux 系统，通常不建议使用非 Linux 文件系统格式化分区。Linux 支持这些文件系统主要作为一种与其他操作系统共享数据的方法。

## 创建文件系统

在 Linux 中创建文件系统的“瑞士军刀”是 `mkfs` 程序。`mkfs` 程序实际上是几个用于创建特定文件系统的独立工具的前端，例如用于创建 `ext4` 文件系统的 `mkfs.ext4` 程序。

`mkfs` 程序的美妙之处在于，你只需记住一个程序名称即可在 Linux 系统上创建任何类型的文件系统。只需使用 `-t` 选项来指定文件系统类型：

```bash
$ sudo mkfs -t ext4 /dev/sdb1
mk2fs 1.44.1 (24-Mar-2018)
Creating filesystem with 2621440 4k blocks and 655360 inodes
Filesystem UUID: f9137b26-0caf-4a8a-afdo-39200242ae8
Superblock backups stored on blocks:

32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632
Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done
$
```

指定 `-t` 选项后，只需在命令行中指定要格式化的分区设备文件名。请注意，`mkfs` 程序在格式化文件系统时幕后执行了许多操作。每种文件系统都有自己的方法

对文件和文件夹进行索引以及跟踪文件访问。`mkfs` 程序创建特定文件系统所需的所有索引文件和表格。

![](img/c0a399aca0d18f8822d714ad0a173123_409_0.png)

在指定分区设备文件名时要格外小心。当您格式化分区时，分区上任何现有数据都会丢失。如果您指定了错误的分区名称，可能会丢失重要数据，或者导致您的 Linux 系统无法启动。

## 挂载文件系统

一旦您使用文件系统格式化了磁盘分区，就可以将其添加到 Linux 系统的虚拟目录中。这个过程称为`挂载`文件系统。您可以从命令行手动将分区挂载到虚拟目录结构中，或者允许 Linux 在启动时自动挂载该分区。以下章节将介绍这两种方法。

## 手动挂载设备

要将文件系统临时挂载到 Linux 虚拟目录中，请使用 `mount` 命令。`mount` 命令的基本格式如下：

```bash
mount -t fstype device mountpoint
```

使用 `-t` 命令行选项来指定设备的文件系统类型：

```bash
$ sudo mount -t ext4 /dev/sdb1 /media/usbl
$ 
```

如果您在未指定任何参数的情况下使用 `mount` 命令，它将显示当前在 Linux 系统上挂载的所有设备。不过，请做好输出较长的心理准备，因为大多数 Linux 发行版会在虚拟目录中挂载许多虚拟设备以提供有关系统资源的信息。列表 11.1 显示了 `mount` 命令的部分输出。

### 列表 11.1 `mount` 命令的输出

```bash
$ mount
...
/dev/sda2 on / type ext4 (rw,relatime,errors=remount-ro,data=ordered)
/dev/sda1 on /boot/efi type vfat
(rw,relatime,fmask=0077,dmask=0077,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro)
...
/dev/sdb1 on /media/usbl type ext4 (rw,relatime,data=ordered)
/dev/sdb2 on /media/usb2 type ext4 (rw,relatime,data=ordered)
rich@rich-TestBox2:~$
```

为了节省空间，我们精简了 `mount` 命令的输出，仅显示系统上的物理设备。主硬盘设备（`/dev/sda`）包含两个分区，`USB` 闪存盘设备（`/dev/sdb`）也包含两个分区。

> **注意**
>
> `mount` 命令使用 `-o` 选项来指定文件系统的额外特性，例如以只读模式挂载、分配给挂载点的用户权限以及数据在设备上的存储方式。这些选项显示在 `mount` 命令的输出中。通常，您可以省略 `-o` 选项，让新的挂载点使用系统默认设置。

使用 `mount` 命令的缺点是它只是在虚拟目录中临时挂载设备。当您重启系统时，必须再次手动挂载这些设备。对于可移动设备（如 `USB` 闪存盘），这通常没问题，但对于更持久的设备，最好让 Linux 能自动为我们挂载它们。幸运的是，Linux 正好能做到这一点。

要从虚拟目录中移除已挂载的驱动器，请使用 `umount` 命令（注意少了个 `n`）。您可以通过指定设备文件名或挂载点目录来移除已挂载的驱动器。

## 自动挂载设备

对于永久性存储设备，Linux 维护 `/etc/fstab` 文件以指示哪些磁盘设备应在启动时挂载到虚拟目录中。`/etc/fstab` 文件是一个表格，指示磁盘设备文件（原始文件或其永久 `udev` 文件名之一）、挂载点位置、文件系统类型以及挂载磁盘所需的任何附加选项。列表 11.2 显示了 `Ubuntu` 工作站上的 `/etc/fstab` 文件。

### 列表 11.2 `/etc/fstab` 文件

```bash
$ cat /etc/fstab

# /etc/fstab: static file system information.
#

# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda2 during installation
UUID=46a8473c-8437-4d5f-a6a1-6596c492c3ce / ext4 errors=remount-ro 0 1
# /boot/efi was on /dev/sda1 during installation
UUID=864B-62F5 /boot/efi vfat umask=0877 0 1
# swap was on /dev/sda3 during installation
UUID=8673447a-0227-47d7-a67a-e68b37dd7188 none swap sw
/ 0
```

此 `/etc/fstab` 文件通过设备的 `udev` `UUID` 值引用设备，确保无论其在原始设备表中的顺序如何，都能访问正确的磁盘分区。第一个分区挂载到虚拟目录中的 `/boot/efi` 挂载点。第二个分区挂载到虚拟目录的根目录（`/`），第三个分区挂载为虚拟内存的交换区域。

您可以手动将设备添加到 `/etc/fstab` 文件中，以便在 Linux 系统启动时自动挂载。但是，如果它们在启动时不存在，这将导致启动错误。

> **提示**
>
> 在基于 `systemd` 的 Linux 服务器中，如果您仅使用 `/etc/fstab` 文件，`systemd` 仍然会管理这些文件系统。当服务器重启或 `systemd` 重新加载时，`/etc/fstab` 中列出的挂载点会被转换为原生单元。实际上，对于持久性文件系统，使用 `/etc/fstab` 比手动创建挂载单元文件是首选方法。有关此过程的更多信息，请在命令行中输入 `man systemd-fstab-generator`。

> **注意**
>
> 如果在任何分区上使用 `encryptfs` 文件系统类型，它们将出现在 `/etc/crypttab` 文件中，并会在启动时自动挂载。在系统运行期间，通过查看 `/etc/mtab` 文件，您还可以查看所有当前挂载的设备，无论它们是由系统自动挂载的还是由用户手动挂载的。

## 管理文件系统

一旦您创建了文件系统并将其挂载到虚拟目录中，您可能需要对其进行管理和维护，以确保一切顺利运行。以下章节介绍了 Linux 系统中用于管理文件系统的几种实用程序。

### 获取文件系统统计信息

在使用 Linux 系统时，毫无疑问，您最终需要监控磁盘性能和使用情况。有几种不同的工具可以帮助您做到这一点：

- `df` 显示按分区划分的磁盘使用情况。

- `du` 显示按目录划分的磁盘使用情况，适用于查找占用最多磁盘空间的用户或应用程序。

- `iostat` 显示按分区划分的磁盘统计信息实时图表。

- `lsblk` 显示当前分区大小和挂载点。

获取 Linux 系统磁盘空间状况快照的快速方法是使用 `df` 和 `du` 命令：

```bash
$ df -t xfs -h
Filesystem    Size Used Avail Use% Mounted on
/dev/mapper/r1-root   15G  6.6G  7.7G  47% /
/dev/sda1     1014M  351M  664M  35% /boot

$ sudo du -d 1
318632    ./boot
0         ./dev
0         ./proc
9448      ./run
0         ./sys
32400     ./etc
48        ./root
704712    ./var
5711056   ./usr
114656    ./home
369421    ./media
0         ./mnt
18856     ./opt
0         ./srv
12        ./tmp
7279241   .
$  
```

`df` 命令显示系统可用的总体磁盘空间，而 `du` 命令则帮助显示哪些目录包含最多的数据。

除了这些工具外，`/proc` 和 `/sys` 文件夹是内核用于记录系统统计信息的特殊文件系统。两个在与文件系统工作时可能很有用的目录是 `/proc/partitions` 和 `/proc/mounts` 文件夹，它们分别提供有关系统分区和挂载点的信息。此外，`/sys/block` 文件夹为每个挂载的驱动器包含单独的文件夹，显示分区和内核级统计数据。

如果你的 Linux 系统使用了专用存储设备，通常除了标准的 Linux 工具外，还有额外的命令工具可用。例如，如果你的 Linux 系统使用 `SCSI` 控制器，你可以使用 `lsscsi` 命令来显示连接到 `SCSI` 控制器的硬盘信息；或者对于使用光纤通道网络将存储区域网络（`SAN`）连接到你的 Linux 系统的系统，`fcstat` 命令非常有用。

![](img/c0a399aca0d18f8822d714ad0a173123_413_0.png)

某些文件系统，如 `ext3` 和 `ext4`，在创建时会分配特定数量的 `inode`。`inode` 是索引表中的一个条目，用于跟踪存储在文件系统上的文件。如果文件系统表中的 `inode` 条目用完，即使驱动器上还有可用空间，你也无法再创建更多文件。使用带有 `-i` 选项的 `df` 命令可以显示文件系统上已使用的 `inode` 百分比，这在关键时刻可能非常有用。

## 文件系统工具

Linux 使用 `e2fsprogs` 工具包为处理 `ext` 文件系统（如 `ext3` 和 `ext4`）提供实用工具。`e2fsprogs` 包中最流行的工具如下：

- `blkid` 显示有关块设备（如存储驱动器）的信息。

- `chattr` 更改文件系统上的文件属性。

- `debugfs` 手动查看和修改文件系统结构，例如恢复删除的文件或提取损坏的文件。

- `dumpe2fs` 显示块和超级块组信息。

- `e2label` 更改文件系统上的标签。

- `resize2fs` 扩展或缩小文件系统。

- `tune2fs` 修改文件系统参数。

这些工具有助于你微调 `ext` 文件系统上的参数，但如果文件系统发生损坏，你将需要 `fsck` 程序。

`XFS` 文件系统也有一套用于调优文件系统的工具。以下是你最常遇到的两个：

- `xfs_admin` 显示或更改文件系统参数，例如分配的标签或 `UUID`。

- `xfs_info` 显示已挂载文件系统的信息，包括块大小和扇区大小，以及标签和 `UUID` 信息。

如果你正在使用 `btrfs` 文件系统，`btrfs` 命令提供了访问多个管理文件系统实用工具的功能：

- `balance` 在多个设备之间平衡文件系统块

- `check` 对 `btrfs` 文件系统执行离线检查

- `device` 通过添加或删除物理设备，为 `btrfs` 文件系统提供设备管理。

- `filesystem` 为现有的 `btrfs` 文件系统提供文件系统管理实用工具，例如显示信息和调整文件系统大小。

- `quota` 允许你在 `btrfs` 文件系统上设置配额。

- `restore` 允许你从损坏的 `btrfs` 文件系统恢复文件。

虽然这些 `ext`、`XFS` 和 `btrfs` 工具很有用，但如果文件系统本身存在错误，它们无法帮助修复问题。为此，`fsck` 程序是应使用的工具：

```bash
$ sudo fsck -f /dev/sdb1
fsck from util-linux 2.31.1
e2fsck 1.44.1 (24-Mar-2018)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/sdb1: 11/655360 files (0.0% non-contiguous), 66753/2621440 blocks
$
```

> **注意**
>
> 截至本文撰写时，`fsck` 的 `XFS` 模块不修复 `XFS` 文件系统。目前你需要使用 `xfs_repair` 工具。

`fsck` 程序是几个不同程序的前端，这些程序检查各种文件系统，以将索引与存储在该文件系统中的实际文件进行匹配。如果发生任何不一致，请运行 `fsck` 程序进入修复模式，它将尝试协调这些差异并修复文件系统。

## 存储替代方案

存储设备上的标准分区布局确实有其局限性。一旦你创建并格式化一个分区，扩大或缩小它就不太容易。单个分区也容易受到磁盘故障的影响，在这种情况下，存储在该分区中的所有数据都将丢失。

为了适应更动态的存储选项以及容错功能，Linux 引入了几种高级存储管理技术。以下各节介绍了三种流行的技术。

### 多路径

Linux 内核现在支持设备映射多路径（`DM-multipathing`），它允许你在 Linux 系统和网络存储设备之间配置多条路径。多路径通过聚合路径，在所有路径都处于活动状态时提供更高的吞吐量，或在其中一条路径变得不活动时提供容错功能。

Linux `DM-multipathing` 包括以下工具：

- `dm-multipath`：提供多路径支持的内核模块

- `multipath`：用于查看多路径设备的命令行命令

- `multipathd`：用于监控路径并激活/停用路径的后台进程

- `kpartx`：用于为多路径存储创建设备条目的命令行工具

`DM-multipath` 功能使用 Linux 中动态的 `/dev/mapper` 设备文件文件夹。Linux 为你添加到系统中的每个新多路径存储设备创建一个名为 `mpathN` 的 `/dev/mapper` 设备文件，其中 `N` 是多路径驱动器的编号。该文件对 Linux 系统而言充当普通设备文件，允许你在多路径设备上创建分区和文件系统，就像在普通驱动器分区上一样。

### 逻辑卷管理器

Linux 逻辑卷管理器（`LVM`）也利用 `/dev/mapper` 动态设备文件夹来允许你创建虚拟设备驱动器。你可以将多个物理驱动器分区聚合为虚拟卷，然后将其作为系统中的单个分区进行处理。

`LVM` 的好处在于，你可以根据需要添加或移除逻辑卷中的物理分区，从而扩展或缩小逻辑卷。

使用 `LVM` 有点复杂。图 11.3 演示了 `LVM` 环境的布局。

#### 图 11.3 Linux `LVM` 布局

![](img/c0a399aca0d18f8822d714ad0a173123_415_0.png)

在图 11.3 所示的示例中，三个物理驱动器各包含三个分区。第一个逻辑卷由第一个驱动器的前两个分区组成。第二个逻辑卷跨驱动器，将第一个驱动器的第三个分区与第二个驱动器的第一和第二分区组合以创建一个卷。第三个逻辑卷由第二个驱动器的第三个分区和第三个驱动器的前两个分区组成。第三个驱动器的第三个分区未分配，需要时可以稍后添加到任何逻辑卷中。

对于每个物理分区，你必须使用 `fdisk` 或 `gdisk` 将分区类型标记为 `Linux LVM` 文件系统类型。然后，你必须使用几个 `LVM` 工具来创建和管理逻辑卷。表 11.4 列出了 Linux 中可用的 `LVM` 工具。

**表 11.4** Linux `LVM` 命令

| 命令 | 描述 |
| :--- | :--- |
| `lvchange` | 修改逻辑卷的设置 |
| `lvconvert` | 向非镜像逻辑卷添加或移除镜像 |
