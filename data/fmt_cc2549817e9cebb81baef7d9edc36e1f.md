
```bash
fs2: # ls /boot/grub/ -l
total 216
-rw------- 1 root root   30 Jan 19 10:37 device.map
-rw-r--r-- 1 root root   29 Jan 19 10:24 device.map.old
-rw-r--r-- 1 root root  8608 Jul  5  2010 e2fs_stage1_5
-rwxr-xr-x 1 root root  7872 Jul  5  2010 fat_stage1_5
-rwxr-xr-x 1 root root  7136 Jul  5  2010 ffs_stage1_5
-rwxr-xr-x 1 root root  7136 Jul  5  2010 iso9660_stage1_5
-rwxr-xr-x 1 root root  8576 Jul  5  2010 jfs_stage1_5
-rw------- 1 root root  1088 Jan 19 10:37 menu.lst
-rw-r--r-- 1 root root   983 Jan 19 10:24 menu.lst.old
-rwxr-xr-x 1 root root  7236 Jul  5  2010 minix_stage1_5
-rwxr-xr-x 1 root root  9632 Jul  5  2010 reiserfs_stage1_5
-rwxr-xr-x 1 root root   512 Jul  5  2010 stage1
-rw-r--r-- 1 root root 10226 Feb 11 12:18 stage2
-rwxr-xr-x 1 root root  7456 Jul  5  2010 ufs2_stage1_5
-rwxr-xr-x 1 root root  6680 Jul  5  2010 vfatfs_stage1_5
-rwxr-xr-x 1 root root  9280 Jul  5  2010 xfs_stage1_5
fs2: #
```

无论你的 `GRUB` 配置文件使用哪个文件，它都会使用标准的结构。请记住，你的 `LILO` 配置文件使用了一个全局部分，然后是一个或多个特定镜像的部分。`GRUB` 配置文件以非常相似的方式工作。`GRUB` 配置文件的第一部分包含应用于所有菜单项的全局选项。然后它有一个或多个 `title` 部分，用于启动特定的操作系统。这里展示了一个典型的 `GRUB` 配置文件：

### 表 6-2：`GRUB` 配置文件

| `GRUB` 配置文件 | 发行版 |
| :-- | :-- |
| `/boot/grub/grub.conf` | `Fedora` |
| `/boot/grub/menu.lst` | `SUSE Linux`, `Debian` |

```bash
fs2:~ # cat /boot/grub/menu.lst
###### Modified by YaST2. Last modification on Wed Jan 19 10:37:45 MST 2011
###### THIS FILE WILL BE PARTIALLY OVERWRITTEN by perl-Bootloader
###### Configure custom boot parameters for updated kernels in /etc/sysconfig/
bootloader

default 0
timeout 8
#YaST - generic_mbr
gfxmenu (hd0,1)/Boot/message
##YaST - activate

###Don't change this comment - YaST2 identifier: Original name: linux##
title Desktop -- openSUSE 11.3 - 2.6.34-12
root (hd0,1)
kernel /boot/vmlinuz-2.6.34-12-desktop root=/dev/sda2 resume=/dev/sda5
splash=silent quiet showspec vga=0x317
initrd /boot/initrd-2.6.34-12-desktop

###Don't change this comment - YaST2 identifier: Original name: failsafe##
title Failsafe -- openSUSE 11.3 - 2.6.34-12
root (hd0,1)
kernel /boot/vmlinuz-2.6.34-12-desktop root=/dev/sda2 showopts apm=off
nomodeset edd=off powersaved=off nohpet=off highres=off processor.max_cstate=1
initrd /boot/initrd-2.6.34-12-desktop

###Don't change this comment - YaST2 identifier: Original name: floppy##
title Floppy
rootnoverify (fd0)
chainloader +1
fs2:~ #
```

在我们探索这个示例 `GRUB` 配置文件中的条目之前，我们需要回顾一下 `GRUB` 的术语。首先，`GRUB` 引用系统中磁盘和分区的方式可能令人不熟悉。在处理 `LILO` 时，我们使用 `/dev` 中的设备文件来引用设备和分区，例如 `/dev/sda1`。`GRUB` 以不同的方式引用这些设备。`GRUB` 不使用 `/dev` 条目，而是使用以下语法：

```
(hd#ive_number,partition_number)
```

例如，第一个硬盘上的第一个分区（`/dev/sda1`）被 `GRUB` 称为 `hd0,0`。无论第一个磁盘是 `IDE`、`SATA` 还是 `SCSI` 驱动器——`GRUB` 都将其称为 `hd0`。

另一件可能会让你困惑的事情是，`GRUB` 创建了自己的“根”，称为 `GRUB` 根。这并不一定是挂载在 `/` 处的根文件系统。相反，它是 `/boot` 目录所在的分区（阶段 2 安装的位置）。这里令人困惑的部分是：如果你最初分区硬盘时没有为 `/boot` 创建独立的分区，那么 `GRUB` 将使用完整路径来引用 `GRUB` 根，通常是 `/boot/grub`。另一方面，如果你为 `/boot` 创建了独立的分区（这是一个很好的做法），那么这个分区就变成了 `GRUB` 根。`GRUB` 在引用 `GRUB` 根中的文件时不包含 `/boot` 路径。这会让你抓狂，直到你习惯它为止。在继续之前，你需要理解这两个事实；否则，`GRUB` 配置文件中的许多条目将毫无意义。

### 表 6-3 `GRUB` 配置文件选项

表 6-3 逐步解析了 `GRUB` 配置文件中的行，并描述了每行函数的作用。

| 部分 | 选项 | 描述 |
| :--- | :--- | :--- |
| 全局 | `Color` | 指定在 `GRUB` 菜单中使用的颜色。 |
| | `default` | 指定如果用户未进行手动选择，将自动引导的菜单项。在本章所示的示例中，如果用户未另外指定，第一个菜单选项 `(1)` 将被自动引导。 |
| | `timeout` | 指定等待自动引导默认菜单项的秒数。在本章所示的示例中，超时时间设置为 `8` 秒。 |
| | `gfxmenu` | 指定用于显示图形化 `GRUB` 引导菜单的图像文件位置。在本章所示的示例中，将使用第一块硬盘 (`hd0`) 的第二个分区 `(1)` 上的 `/boot/message` 文件作为 `GRUB` 引导菜单。 |
| 标题 | `title` | 指定 `GRUB` 引导菜单中菜单项的标题。 |
| `root` | | 指定要挂载为 `GRUB` 根目录的分区位置。在本章的示例中，这是 `hd0,1`，它指定了第一块硬盘 (`hd0`) 的第二个分区 `(1)`。 |
| | `kernel` | 指定 `Linux` 内核的位置。在本章所示的示例中，`GRUB` 菜单指向 `/boot/vmlinuz-2.6.34-12-desktop`。某些发行版仅指向 `/boot/vmlinuz` 文件，该文件实际上是指向真实内核文件的符号链接。 |
| | | `root=` 选项指定要挂载为根文件系统的分区。`vga=` 选项指定系统在引导期间应使用的 `VGA` 模式。`resume=` 选项指向系统的交换分区。 |
| | `initrd` | 指定 `GRUB` 在引导过程中用于创建初始 `ramdisk` 映像的 `initrd` 映像。在本章所示的示例中，指定了 `/boot/initrd-2.6.34-12-desktop`。某些发行版仅指向 `/boot/initrd` 映像。请记住，与 `vmlinuz` 一样，`/boot` 中的 `initrd` 文件实际上是真正的 `initrd` 映像文件的链接。 |
