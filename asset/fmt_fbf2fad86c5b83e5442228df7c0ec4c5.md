
`modprobe` 命令临时加载模块。在下次系统重启时，这些模块会消失。要永久地将模块添加到系统，请将 `modprobe` 命令添加到启动时运行的脚本行中。

## 移除模块

你可以使用 `rmmod` 命令从运行内核中移除模块。例如，要移除当前内核类型的 `parport_pc`，请使用以下命令：

```
# rmmod parport_pc
```

如果模块当前没有被占用，`parport_pc` 模块将从运行内核中移除。（与其使用 `rmmod`，你可以使用 `modprobe -r` 来移除模块，以及相关模块。）

# 第10章：理解系统管理 427

## 管理文件系统和磁盘空间

Linux 中的文件系统采用层级结构，从根目录 (`/`) 开始，以目录和子目录的结构向下延伸。作为 Fedora 或 RHEL 系统的管理员，你的职责是确保所有代表文件系统的驱动器对计算机用户可用。你的工作还包括确保文件系统中适当的位置有足够的磁盘空间来存储他们需要的内容。

Linux 中文件系统的组织方式与 Microsoft Windows 操作系统不同。它不是为每个本地磁盘、网络文件系统、CD-ROM 或其他类型的存储介质分配驱动器（例如 A:, B:, C:），而是将一切整齐地整合到目录结构中。对于硬盘，由管理员在文件系统中创建挂载点。对于可移动介质（如 CD、USB 闪存盘或数字相机），当这些设备连接或加载时，系统会自动创建并连接挂载点（在 `/media` 目录下）。

> **交叉引用：** 第 2 章提供了使用 Disk Setup（以前称为 Disk Druid）配置磁盘分区的说明。第 4 章描述了 Linux 文件系统的组织方式。

文件系统的组织始于你安装 Linux 的时候。安装过程的一部分是将你的硬盘（或多个硬盘）划分为分区。然后这些分区可以分配给：

- Linux 文件系统的一部分，
- Linux 的交换空间（Swap space），或
- 其他文件系统分区（可能包含其他可启动操作系统）

出于我们的目的，我想关注用于 Linux 文件系统的硬盘分区。要查看你的硬盘上当前设置了哪些分区，请如下所示使用 `fdisk` 命令：

```bash
# fdisk -l
/dev/sda: 40.0 GB 40200664320
255 heads, 63 sectors/track, 4825 cylinders
Units = cylinders of 16065 * 512 bytes = 8225280 bytes
```

| Device | Start | End Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- |
| /dev/sda1 * | | 1 | 104 | b Win95 FAT32 |
| /dev/sda2 | | 84 | 89 | 48195 | Linux |
| /dev/sda3 | | 920 | 3478072* | 83 | Linux |
| /dev/sda4 | | 524 | 257040 | 5 | W95 Ext'd (LBA) |
| /dev/sda5 | | 554 | 257008 | 82 | Linux swap / Solaris |

此输出显示了可以同时运行 Linux 和 Microsoft Windows 的计算机磁盘分区情况。你可以看到 `/dev/sda3` 上的 Linux 分区拥有大部分可用数据空间。有一个 Windows 分区 (/dev/sda1) 和一个 Linux 交换分区 (/dev/sda5)。在 `/dev/sda2` 上还有一个较小的 `/boot` 分区 (46MB)。在这种情况下，Linux 的根分区有 3.3GB 的磁盘空间并位于 `/dev/sda3`。

接下来，要查看哪些分区被用于你的 Linux 系统，可以使用 `mount` 命令（不带任何选项）。`mount` 命令可以显示哪些可用的磁盘分区实际上已经挂载，以及它们挂载在何处。

```bash
# mounts
/dev/sda1 on / type ext3 (rw)
/dev/sda2 on /boot type ext3 (rw)
/dev/sda3 on /mnt/win type vfat (rw)
none on /proc type proc (rw)
one on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /proc/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
/dev/scd0 on /media/cdrecord type iso9660 (ro,nosuid,uhelper=hal)
```
