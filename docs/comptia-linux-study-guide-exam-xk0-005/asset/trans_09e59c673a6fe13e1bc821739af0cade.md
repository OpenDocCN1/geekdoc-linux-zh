
对文件和文件夹进行索引以及跟踪文件访问。`mkfs` 程序创建特定文件系统所需的所有索引文件和表格。

![](img/c0a399aca0d18f8822d714ad0a173123_409_0.png)

在指定分区设备文件名时要格外小心。当您格式化分区时，分区上任何现有数据都会丢失。如果您指定了错误的分区名称，可能会丢失重要数据，或者导致您的 Linux 系统无法启动。

## 挂载文件系统

一旦您使用文件系统格式化了磁盘分区，就可以将其添加到 Linux 系统的虚拟目录中。这个过程称为*挂载*文件系统。您可以从命令行手动将分区挂载到虚拟目录结构中，或者允许 Linux 在启动时自动挂载该分区。以下章节将介绍这两种方法。

## 手动挂载设备

要将文件系统临时挂载到 Linux 虚拟目录中，请使用 *mount* 命令。*mount* 命令的基本格式如下：

```bash
mount -t fstype device mountpoint
```

使用 *-t* 命令行选项来指定设备的文件系统类型：

```bash
$ sudo mount -t ext4 /dev/sdb1 /media/usbl
$ 
```

如果您在未指定任何参数的情况下使用 *mount* 命令，它将显示当前在 Linux 系统上挂载的所有设备。不过，请做好输出较长的心理准备，因为大多数 Linux 发行版会在虚拟目录中挂载许多虚拟设备以提供有关系统资源的信息。列表 11.1 显示了 *mount* 命令的部分输出。

### 列表 11.1 mount 命令的输出

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

为了节省空间，我们精简了 `mount` 命令的输出，仅显示系统上的物理设备。主硬盘设备（`/dev/sda`）包含两个分区，USB 闪存盘设备（`/dev/sdb`）也包含两个分区。

> **注意**
>
> `mount` 命令使用 `-o` 选项来指定文件系统的额外特性，例如以只读模式挂载、分配给挂载点的用户权限以及数据在设备上的存储方式。这些选项显示在 `mount` 命令的输出中。通常，您可以省略 `-o` 选项，让新的挂载点使用系统默认设置。

使用 `mount` 命令的缺点是它只是在虚拟目录中临时挂载设备。当您重启系统时，必须再次手动挂载这些设备。对于可移动设备（如 USB 闪存盘），这通常没问题，但对于更持久的设备，最好让 Linux 能自动为我们挂载它们。幸运的是，Linux 正好能做到这一点。

要从虚拟目录中移除已挂载的驱动器，请使用 `umount` 命令（注意少了个 `n`）。您可以通过指定设备文件名或挂载点目录来移除已挂载的驱动器。

## 自动挂载设备

对于永久性存储设备，Linux 维护 `/etc/fstab` 文件以指示哪些磁盘设备应在启动时挂载到虚拟目录中。`/etc/fstab` 文件是一个表格，指示磁盘设备文件（原始文件或其永久 `udev` 文件名之一）、挂载点位置、文件系统类型以及挂载磁盘所需的任何附加选项。列表 11.2 显示了 Ubuntu 工作站上的 `/etc/fstab` 文件。

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

此 `/etc/fstab` 文件通过设备的 `udev` UUID 值引用设备，确保无论其在原始设备表中的顺序如何，都能访问正确的磁盘分区。第一个分区挂载到虚拟目录中的 `/boot/efi` 挂载点。第二个分区挂载到虚拟目录的根目录（`/`），第三个分区挂载为虚拟内存的交换区域。

您可以手动将设备添加到 `/etc/fstab` 文件中，以便在 Linux 系统启动时自动挂载。但是，如果它们在启动时不存在，这将导致启动错误。

> **提示**
>
> 在基于 systemd 的 Linux 服务器中，如果您仅使用 `/etc/fstab` 文件，systemd 仍然会管理这些文件系统。当服务器重启或 systemd 重新加载时，`/etc/fstab` 中列出的挂载点会被转换为原生单元。实际上，对于持久性文件系统，使用 `/etc/fstab` 比手动创建挂载单元文件是首选方法。有关此过程的更多信息，请在命令行中输入 `man systemd-fstab-generator`。

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

