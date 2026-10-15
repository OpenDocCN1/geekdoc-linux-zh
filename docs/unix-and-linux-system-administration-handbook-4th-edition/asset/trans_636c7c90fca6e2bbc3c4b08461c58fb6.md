

Linux 没有磁盘或磁盘分区的原始设备文件，因此在你习惯于指定原始设备的地方，只需使用块设备即可。

parted -l 列出系统上每个磁盘的大小、分区表、型号和制造商。

## Solaris 的磁盘设备

Solaris 磁盘设备名称的形式为 /dev/[r]dsk/cWtXdYsZ，其中 W 是控制器号，X 是 SCSI 目标号，Y 是 SCSI 逻辑单元号（或 LUN，几乎总是 0），Z 是分区（切片）号。 有一些细微差别：ATA 驱动器显示为 cWdYsZ（没有 t 子句），并且磁盘可以具有一系列 DOS 风格的分区，用 pZ 表示，以及用 sZ 表示的 Solaris 风格的切片。

这些设备文件实际上只是指向 /devices 树的符号链接，真正的设备文件位于那里。 更一般地说，Solaris 努力在面对硬件更改时保持设备名称的连续性。 一旦磁盘出现在给定名称下，除非你更换控制器或 SCSI 目标 ID，否则它通常可以在未来在该名称下找到。

按照惯例，切片 2 表示完整的、未分区的磁盘。 与 Linux 不同，Solaris 为每个可能的切片和分区提供设备文件，无论这些切片和分区是否实际存在。 Solaris 还支持重叠分区，但这只是疯狂的言论。 Oracle 不妨随每台 Solaris 系统附带一把上膛的手枪。

热插拔在 Solaris 上应该能正常工作。 当你添加新磁盘时，devfsadmd 应该会检测到它并为你创建适当的设备文件。 如有必要，你可以手动运行 devfsadm。

## HP-UX 的磁盘设备

HP-UX 传统上使用与 Solaris 类似的磁盘设备名称模式，其中在设备路径中记录了大量硬件特定信息。 然而，从 HP-UX 11i v3 开始，这些路径名已被弃用，取而代之的是形式为 /dev/disk/disk1 的“敏捷地址”。 后者路径是稳定的，并且不会随着系统硬件配置的细节而改变。

在启动 UNIX 之前，你可以从 PROM 监视器中获取系统的 SCSI 设备列表。 不幸的是，具体操作方法因机器而异。 启动后，你可以通过运行 ioscan 来列出磁盘。

```
$ sudo ioscan -fnn -C disk
Class    I   H/W Path        Driver   S/W State   H/W Type Description
================================================================================
disk     3  64000/0xfa00/0x0  esdisk   CLAIMED    DEVICE    TEACDV-28E-B
          /dev/disk/disk3     /dev/rdisk/disk3
disk     4  64000/0xfa00/0x1  esdisk   CLAIMED    DEVICE    HP 73.4GMAS3735NC
          /dev/disk/disk4     /dev/rdisk/disk4
          /dev/disk/disk4_p1  /dev/rdisk/disk4_p1
/dev/disk/disk4_p2    /dev/rdisk/disk4_p2
/dev/disk/disk4_p3    /dev/rdisk/disk4_p3
disk 5 64000/0xf00/0x2 esdisk CLAIMED DEVICE HP 73.4GMAS3735NC
/dev/disk/disk5        /dev/rdisk/disk5
/dev/disk/disk5_p1     /dev/rdisk/disk5_p1
/dev/disk/disk5_p2     /dev/rdisk/disk5_p2
/dev/disk/disk5_p3     /dev/rdisk/disk5_p3
```

旧式设备名称仍然存在于 /dsk 和 /rdsk 目录中，如果你愿意，至少现在可以继续使用它们。 运行 ioscan -m dsf 以查看旧式和新式设备名称之间的当前映射。

```
hp-ux% ioscan -m dsf
Persistent DSF*          Legacy DSF(s)
=================================  ===================
/dev/rdisk/disk3        /dev/rdsk/c0t0d0
/dev/rdisk/disk4        /dev/rdsk/c2t1d0
/dev/rdisk/disk4_p1     /dev/rdsk/c2t1d0s1
/dev/rdisk/disk4_p2     /dev/rdsk/c2t1d0s2
/dev/rdisk/disk4_p3     /dev/rdsk/c2t1d0s3
/dev/rdisk/disk5        /dev/rdsk/c2t0d0
/dev/rdisk/disk5_p1     /dev/rdsk/c2t0d0s1
/dev/rdisk/disk5_p2     /dev/rdsk/c2t0d0s2
/dev/rdisk/disk5_p3     /dev/rdsk/c2t0d0s3
```

请注意，分区现在缩写为 p 而不是 Solaris 方式的 s（表示“slice”）。 与 Solaris 不同，HP-UX 使用诸如 disk3 之类的名称且没有分区后缀来表示整个磁盘。 在 Solaris 系统上，分区 2 表示整个磁盘；在 HP-UX 上，它只是另一个分区。

此示例来自基于 Itanium 的系统，因此具有磁盘分区。 其他 HP 系统使用逻辑卷管理而不是分区。

## AIX 的磁盘设备

AIX 的 /dev/hdiskX 和 /dev/rhdiskX 路径令人耳目一新地简单。 磁盘名称不幸会在硬件配置更改时发生变化。 然而，大多数 AIX 磁盘将处于逻辑卷管理之下，因此硬件设备名称并不那么重要。 逻辑卷管理器会在将磁盘纳入卷组的过程中向每个磁盘写入唯一的 ID。 此标签允许系统自动整理磁盘，因此设备名称的变化比在其他系统上可能的情况要少得多。

你可以运行 lsdev -C -c disk 来查看系统所知的磁盘列表。

## 格式化和坏块管理

所有硬盘都预先格式化，并且工厂格式化至少与你在现场可以做的任何格式化一样好。 最好避免在不需要时进行低级格式化。 不要将新驱动器作为常规操作重新格式化。

