
- `parity-algorithm algorithm`：对于 RAID 5 设备，指定要使用的奇偶校验算法：`left-asymmetric`、`right-asymmetric`、`left-symmetric` 或 `right-symmetric`。
- `failed-disk index`：最近定义的设备作为故障设备添加到 RAID 阵列中指定位置。

## `mkraid` 命令

一旦你在`/etc/raidtab`文件中配置了你的 RAID 设备，你就可以使用`mkraid`命令来创建你的 RAID 设备。`mkraid`以 RAID 设备的名称作为参数，例如第一个 RAID 设备的`/dev/md0`。它随后在`/etc/raidtab`文件中查找该设备的条目，并使用该配置信息在该设备上创建 RAID 文件系统。如果你愿意，可以使用`-c`选项指定一个替代的配置文件。`mkraid`可作为 RAID 设备的`mkfs`命令的一种，初始化分区并创建 RAID 文件系统。构成 RAID 阵列的分区上的任何数据都将被擦除。

```
mkraid /dev/md0
```

## `raidstart` 命令

一旦你创建了 RAID 设备，你就可以使用`raidstart`命令来激活它们。`raidstart`使你的 RAID 文件系统可访问。`raidstart`以你想要启动的 RAID 设备名称作为参数。`-a`选项激活所有 RAID 设备。

```
raidstart /dev/md0
```

## 创建文件系统

一旦 RAID 设备被激活，你就可以在 RAID 设备上创建文件系统并挂载这些文件系统。以下示例在`/dev/md0`设备上创建了一个标准 Linux 文件系统：

```
mkfs.ext3 /dev/md0
```

在以下示例中，用户随后创建了一个名为`/myraid`的目录并将 RAID 设备挂载到那里：

```
mkdir /myraid
mount /dev/md0 /myraid
```

如果你计划使用你的 RAID 设备来维护你的用户目录和文件，你会将 RAID 设备挂载为你的`/home`分区。这种挂载点通常在你安装系统时创建 RAID 设备时使用。要将当前的主目录转移到 RAID 设备，首先将它们备份到另一个分区，然后挂载你的 RAID 设备，将主目录复制到其上。

## `raidstop` 命令

如果你决定更改 RAID 配置或添加新设备，你首先必须停用当前活动的 RAID 设备。要停用 RAID 设备，你使用`raidstop`命令。请务必先关闭设备上打开的任何文件并卸载任何文件系统。

```
umount /dev/md0
raidstop /dev/md0
```

提示：热插拔是指在系统运行时更换驱动器的操作。其可行性有限。切勿尝试热插拔 IDE 驱动器；你可能会损坏驱动器。SCSI 驱动器可能成功交换，但最有可能不会。IBM SCA 驱动器可以成功交换。你可以使用`raidhotadd`和`raidhotremove`命令执行此类交换。

## RAID 示例

本章前面，图 31-1 显示了一个简单的 RAID 配置，其中使用两个硬盘上的对应分区创建了三个 RAID 设备，用于`/boot`、`/`（根）和`/home`分区。引导分区配置为 RAID 1 设备，因为系统只能从 RAID 1 设备启动，而不能从 RAID 5 启动。其他分区是 RAID 5 设备，这是一种更常用的 RAID 访问方法。

你可以在安装期间设置这样的系统，使用 Disk Druid 选择和格式化你的 RAID 设备及其分区。这里描述的步骤假设你已经在标准 IDE 驱动器上安装了系统，并且正在两个其他 IDE 磁盘驱动器上设置 RAID 设备。然后你可以将文件从你的标准驱动器复制到你的 RAID 设备。

首先使用像`parted`或`fdisk`这样的分区工具创建硬盘分区。然后在`/etc/raidtab`文件中配置三个 RAID 设备。

```
raiddev /dev/md0
    raid-level        1
    nr-raid-disks     2
    nr-spare-disks    0
    persistent-superblock 1
    chunk-size        4
    device            /dev/hda1
    raid-disk         0
    device            /dev/hdc1
    raid-disk         1
```

```
raiddev /dev/md1
    raid-level        5
    nr-raid-disks     2
    persistent-superblock 1
    chunk-size        4
    parity-algorithm  left-symmetric
    device            /dev/hda2
    raid-disk         0
    device            /dev/hdc2
    raid-disk         1
```

```
raiddev /dev/md2
    raid-level        5
    nr-raid-disks     2
    persistent-superblock 1
    chunk-size        4
    parity-algorithm  left-symmetric
    device            /dev/hda3
    raid-disk         0
    device            /dev/hdc3
    raid-disk         1
```

然后，使用`mkraid`创建 RAID 设备。

```
mkraid md0 md1 md2
```

使用`raidstart`激活 RAID 设备。

```
raidstart md0 md1 md2
```

在 RAID 设备上创建文件系统。

```
mkfs.ext3 md0 md1 md2
```

然后，你可以将`/boot`、`/`和`/home`下的文件从当前硬盘迁移到 RAID 设备。将引导加载程序安装在第一个 RAID 设备`md0`上，并从第二个 RAID 设备`md1`加载根文件系统。

## 逻辑卷管理器

为了更方便地管理硬盘存储，你可以将系统设置为使用逻辑卷管理器（LVM），创建 LVM 分区，这些分区被组织为逻辑卷，并自动分配空闲空间。逻辑卷提供了一种更灵活、更强大的磁盘存储管理方式，将物理分区组织为逻辑卷，从而可以轻松管理磁盘空间。逻辑卷的磁盘存储被视为一个存储池，尽管该卷实际上可能包含分布在多个不同硬盘上的若干硬盘分区。添加一个新的 LVM 分区只会增加整个系统可访问的存储池。

### LVM 结构

在 LVM 结构中，LVM 物理分区（也称为区段）被组织成逻辑组，逻辑组又被逻辑卷使用。实际上，你面对的是三个不同层次的组织。最低层是物理卷，即你用`parted`或`fdisk`等分区创建工具创建的物理硬盘分区。分区类型可以是任何标准 Linux 分区类型，如`ext3`或`ext2`。这些物理卷被组织成逻辑组（称为卷组），其作用类似于逻辑硬盘。你将物理卷集合分配给不同的逻辑组。例如，如果你有物理卷，由两个硬盘`hda`和`hdb`上的硬盘分区`hda2`、`hda3`、`hdb1`、`hdb2`和`hdb3`组成，你可以将其中一些分配给一个逻辑组，另一些分配给另一个逻辑组。组成不同逻辑组的分区可以来自不同的物理硬盘。例如，`hda2`和`hdb3`可以属于逻辑组`turtle`，而`hda3`、`hdb2`和`hdb3`可以组成另一个不同的逻辑组，比如`rabbit`。逻辑组名称可以是任何你想赋予的名称，就像给硬盘命名一样。

一旦有了逻辑组，就可以创建逻辑卷。逻辑卷的功能很像标准设置中的硬盘分区。例如，在`turtle`逻辑组上，你可以创建一个`/var`逻辑卷；在`rabbit`逻辑组上，你可以创建`/home`和`/projects`逻辑卷。一个逻辑组上可以有多个逻辑卷，就像一块硬盘上可以有多个分区一样。

你可以像对待任何普通硬盘分区一样对待逻辑卷。使用`mkfs`命令在其上创建文件系统，然后可以使用`mount`命令挂载该文件系统以供使用。

逻辑卷上的存储使用所谓的区段来管理。逻辑组为区段定义一个标准大小，比如 4MB，然后将组内的每个物理卷划分为该大小的区段。逻辑卷也被划分为相同大小的区段，然后映射到物理卷上的区段。

对于逻辑卷，有一个限制和一个建议。引导分区不能是逻辑卷的一部分。你仍然必须创建一个单独的硬盘分区作为引导分区，挂载点为`/boot`，并在其中安装内核和所有必需的引导文件。此外，建议你不要将`/`（根）分区放在逻辑卷上，否则会使任何必要的数据恢复变得复杂。

### 使用 Disk Druid 创建 LVM

创建逻辑卷涉及几个步骤。首先，创建物理 LVM 分区；然后创建放置这些分区的卷组；接着，从卷组中创建逻辑卷，并为这些逻辑卷指定挂载点和文件系统类型。
