
RAID 4 级别仅是 RAID 3 级别的一个微小变体。RAID 4 级别比 RAID 3 级别提供更高的访问速度，因为它可以按块存储数据，因此不需要同时访问阵列中的所有磁盘来读取数据。

RAID 5 级别取代了 RAID 3 和 4 级别；截至本文撰写时，它是最常见的 RAID 配置。它通常被称为**带奇偶校验的磁盘条带化**。与 RAID 3 和 4 级别一样，它至少需要三个硬盘驱动器才能实施；但是，奇偶校验信息不是存储在一个单独的驱动器上，而是混合存储在构成该集成的驱动器上的数据中。这提供了更好的性能和容错能力；如果 RAID 配置中任何驱动器故障，在更换故障硬盘后，可以使用其他驱动器上的信息来重新生失信息。如果两个硬盘故障，则必须从备份设备恢复系统。图 6-4 展示了如何使用奇偶校验信息恢复 RAID 5 级别配置。图 6-4 中显示的奇偶校验位是其他两个磁盘上信息的总和（$22 + 12 = 34$）。如果第三个硬盘故障，由于每个方程中只缺少一个元素，因此可以重新生成信息：

- $22 + 12 = 34$
- $68 - 65 = 3$
- $13 - 9 = 4$

![](img/c27875544958897d817484d558c208c8_292_0.png)

**图 6-4** RAID 5 级别的数据组织

RAID 6 级别基本上与 RAID 5 级别相同，但它增加了一组第二奇偶校验位以增强容错能力，并允许在保持容错性的同时最多容忍两个硬盘驱动器同时故障。

RAID 级别通常会组合使用；RAID 15 级别指的是一个带奇偶校验的条带集（RAID 5 级别），该集被镜像（RAID 1 级别）到另一个带奇偶校验的条带集。

![](img/c27875544958897d817484d558c208c8_292_1.png)

RAID 配置可以由运行在操作系统上的软件处理（称为**软件 RAID**），但更常见的是由 SCSI 或 SATA 硬盘控制器中包含的硬件处理（称为**硬件 RAID**），或者由系统 BIOS 处理（称为**固件 RAID**）。

![](img/c27875544958897d817484d558c208c8_293_0.png)

要配置硬件 RAID，你必须使用特定 SCSI 或 SATA 硬盘控制器的 RAID 设置实用程序。你可以通过在系统启动时进入系统 BIOS 或 SCSI BIOS，或使用制造商提供的启动 CD 或 DVD 来访问此设置实用程序。在设置实用程序中配置好硬件 RAID 卷后，它们将自动作为标准硬盘卷出现在 Linux 安装程序中。例如，如果你使用 RAID 设置实用程序配置三个硬盘组成一个 RAID 5 卷，它们将作为单个卷（/dev/sdb）出现在 Linux 安装程序中。然后，你可以像在 /dev/sdb 上放置任何物理硬盘一样，在其上放置文件系统。

要配置固件 RAID，你必须首先使用系统 BIOS 中的 RAID 设置实用程序配置一个 RAID 卷。接下来，你可以启动 Linux 安装并选择固件 RAID 卷。对于 Fedora 20 安装，选择*添加磁盘*，如图 2-10 所示，高亮显示如图 6-3 所示的*固件 RAID*选项卡，并选择你想用于 Linux 安装的固件 RAID 卷。

与硬件或固件 RAID 不同，软件 RAID 完全在安装过程中配置（前提是你的系统有多个硬盘）。要在 Fedora 20 安装期间配置软件 RAID，请确保图 2-10 所示的屏幕上存在并选择了多个磁盘。接下来，选择一种分区策略，以及图 2-11 中显示的*我希望在继续之前查看/修改我的磁盘分区*选项。之后，你可以创建用于承载 Linux 文件系统的分区，选择 RAID 作为设备类型，并选择合适的 RAID 级别和文件系统。图 6-5 中显示的 /（根）文件系统存储了 RAID 1，分布在两个 20GB 的硬盘上；每个磁盘将有 15GB 用于存储 /（根）文件系统。

你的第一个 RAID 卷将使用以数字 127 开头的多磁盘（md）设备文件（/dev/md127）。你的第二个 RAID 卷将使用设备文件 /dev/md128，依此类推。例如，图 6-5 中配置的 /（根）文件系统将在 `df` 命令的输出中显示为 /dev/md127，如下所示：

```bash
[root@server1 ~]# df
Filesystem	1K-blocks	Used	Available	Use%	Mounted on
/dev/md127	14987656	3242408	10960864	23%	/
devtmpfs	1014932	0	1014932	0%	/dev
tmpfs	1022260	80	1022180	1%	/sys/shm
tmpfs	1022260	684	1021576	1%	/run
tmpfs	1022260	0	1022260	0%	/sys/fs/cgroup
tmpfs	1022260	16	1022244	1%	/tmp
/dev/sda1	487652	90207	367749	20%	/boot
[root@server1 ~]#
```

![](img/c27875544958897d817484d558c208c8_294_0.png)

**图 6-5** 在 Fedora 20 安装过程中配置软件 RAID

安装后，你可以使用 **mdadm** 命令管理你的软件 RAID 配置，并通过查看 `/etc/mdadm.conf` 和 `/proc/mdstat` 文件的内容来获取已配置的软件 RAID 设备的详细信息，如下所示：

```bash
[root@server1 ~]# cat /etc/mdadm.conf
# mdadm.conf written out by anaconda
MAILADDR root
AUTO +imsm +1.x -all
ARRAY /dev/md/root level=raid1 num-devices=2 UUID=77d3f6c5:fbc71aa5:426b55b:1e0d9860
[root@server1 ~]#
[root@server1 ~]# cat /proc/mdstat
Personalities : [raid1]
md127 : active raid1 sda2[0] sdb1[1]
          15360000 blocks super 1.2 [2/2] [UU]
          bitmap: 0/1 pages [0KB], 65536KB chunk

unused devices: <none>
[root@server1 ~]#
```

## ZFS 配置

大多数 Linux 服务器将 Linux 操作系统和任何附加程序存储在标准分区、LVM 卷或 RAID 卷上的文件系统中。对于需要大量存储空间来存储附加数据（例如文件服务器或数据库服务器）的 Linux 服务器，通常会在 SAN 存储设备（例如与服务器位于同一机架上的 iSCSI SAN）上创建文件系统，并将其挂载到 Linux 系统中用于存储附加数据的目录上。

Zettabyte 文件系统（ZFS）是一种高性能的文件系统和卷管理软件，专为需要将在多个磁盘、SAN 和远程系统上存储数据的大型 Linux 系统设计。你可以创建类似 RAID 的 ZFS 卷，这些卷可以跨越数千个不同的本地和网络存储设备，例如本地硬盘、SSD、SAN 和远程文件共享，并且可以在文件系统挂载时调整卷大小。此外，ZFS 文件系统在数据和写入时自动检测和修复数据错误，并保护免受在将大量数据写入非 ZFS 文件系统的大型系统中常见的问题，包括：

- 静默数据损坏
- 比特衰变
- 磁盘固件错误
- 幻影写入
- 错误定向的写入
- 驱动程序和内核缓冲区错误
- 意外的驱动程序覆盖

ZFS 还支持新的存储技术，例如 PCIe SSD 和带有超低延迟电池后备 RAM 磁盘设备。此外，ZFS 在 RAM 和更快的存储设备（如 SSD）中缓存频繁访问的信息，以提供超快的性能。ZFS 还支持几乎所有高级文件系统功能，包括去重（存储位于多个目录中且直到其中一个文件更改为止的文件的一份副本）、快照、克隆、压缩、加密、NFSv4、卷管理等。

![](img/c27875544958897d817484d558c208c8_295_0.png)

ZFS 最初由 Sun Microsystems 于 2001 年创建，并经常用于世界上最大的 Linux 和 UNIX 系统。它可用于 Solaris UNIX、Mac OS X、Linux、FreeBSD、FreeNAS 等。由于 ZFS 目前没有与 GPL 兼容的许可证，因此不能打包在 Linux 发行版中，但可以稍后轻松添加。在 Linux 上，ZFS 支持由 [http://zfsonlinux.org](http://zfsonlinux.org) 维护。

虽然 ZFS 主要用于可能拥有数百或数千个存储设备的大型 Linux 系统，但它也用于需要易于配置的灵活卷管理数据中小型组织。

ZFS 池是 ZFS 可以管理的一组物理磁盘（本地磁盘、SAN、共享设备、大型原始文件、远程共享等），ZFS 卷 simply 就是从 ZFS 池创建的 ZFS 管理的文件系统。

例如，假设一个系统托管了几个 SATA 硬盘，Linux 操作系统安装在 /dev/sda 上。要从第二个 SATA 硬盘创建一个名为 datastorage1 的简单 ZFS 池，你可以使用以下 zpool 命令：

```bash
[root@server1 ~]# zpool create datastorage1 /dev/sdb
[root@server1 ~]#
```
