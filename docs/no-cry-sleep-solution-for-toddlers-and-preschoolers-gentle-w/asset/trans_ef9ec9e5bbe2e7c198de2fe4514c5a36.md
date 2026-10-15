

## mkraid 命令

一旦你在 /etc/raidtab 文件中配置了你的 RAID 设备，你就可以使用 mkraid 命令来创建你的 RAID 设备。mkraid 以 RAID 设备的名称作为参数，例如第一个 RAID 设备的 /dev/md0。它随后在 /etc/raidtab 文件中查找该设备的条目，并使用该配置信息在该设备上创建 RAID 文件系统。如果你愿意，可以使用 -c 选项指定一个替代的配置文件。mkraid 可作为 RAID 设备的 mkfs 命令的一种，初始化分区并创建 RAID 文件系统。构成 RAID 阵列的分区上的任何数据都将被擦除。

```
mkraid /dev/md0
```

## raidstart 命令

一旦你创建了 RAID 设备，你就可以使用 raidstart 命令来激活它们。raidstart 使你的 RAID 文件系统可访问。raidstart 以你想要启动的 RAID 设备名称作为参数。-a 选项激活所有 RAID 设备。

```
raidstart /dev/md0
```

## 创建文件系统

一旦 RAID 设备被激活，你就可以在 RAID 设备上创建文件系统并挂载这些文件系统。以下示例在 /dev/md0 设备上创建了一个标准 Linux 文件系统：

```
mkfs.ext3 /dev/md0
```

在以下示例中，用户随后创建了一个名为 /myraid 的目录并将 RAID 设备挂载到那里：

```
mkdir /myraid
mount /dev/md0 /myraid
```

如果你计划使用你的 RAID 设备来维护你的用户目录和文件，你会将 RAID 设备挂载为你的 /home 分区。这种挂载点通常在你安装系统时创建 RAID 设备时使用。要将当前的主目录转移到 RAID 设备，首先将它们备份到另一个分区，然后挂载你的 RAID 设备，将主目录复制到其上。

## raidstop 命令

如果你决定更改 RAID 配置或添加新设备，你首先必须停用当前活动的 RAID 设备。要停用 RAID 设备，你使用 raidstop 命令。请务必先关闭设备上打开的任何文件并卸载任何文件系统。

```
umount /dev/md0
raidstop /dev/md0
```

提示：热插拔是指在系统运行时更换驱动器的操作。其可行性有限。切勿尝试热插拔 IDE 驱动器；你可能会损坏驱动器。SCSI 驱动器可能成功交换，但最有可能不会。IBM SCA 驱动器可以成功交换。你可以使用 raidhotadd 和 raidhotremove 命令执行此类交换。

## RAID 示例

本章前面，图 31-1 显示了一个简单的 RAID 配置，其中使用两个硬盘上的对应分区创建了三个 RAID 设备，用于 /boot、/（根）和 /home 分区。引导分区配置为 RAID 1 设备，因为系统只能从 RAID 1 设备启动，而不能从 RAID 5 启动。其他分区是 RAID 5 设备，这是一种更常用的 RAID 访问方法。

你可以在安装期间设置这样的系统，使用 Disk Druid 选择和格式化你的 RAID 设备及其分区。这里描述的步骤假设你已经在标准 IDE 驱动器上安装了系统，并且正在两个其他 IDE 磁盘驱动器上设置 RAID 设备。然后你可以将文件从你的标准驱动器复制到你的 RAID 设备。

首先使用像 parted 或 fdisk 这样的分区工具创建硬盘分区。然后在 /etc/raidtab 文件中配置三个 raid 设备。

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

