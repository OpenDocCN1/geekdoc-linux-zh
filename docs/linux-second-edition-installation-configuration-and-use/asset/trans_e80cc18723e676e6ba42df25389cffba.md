

# 文件系统管理 153

如果你现在访问 /usr/local 中的数据，该链接将指向 /localpart，即指向新分区。这些链接是透明的，你在正常工作时不会注意到它们的存在。同样，你必须在每次系统启动时，在文件系统的 /localpart 处向 `fstab` 中添加条目：

```
# 向 /etc/fstab 的添加
# 将 /dev/sdc3 挂载为 /localpart 到文件系统
/dev/sdc3        localpart       defaults       0 2
```

原则上讲，你可以通过这种方式传输任意数量的目录。但请确保访问权限保持不变。在新创建的目录或链接中，你可能需要使用 `chown` 修改所有者，或使用 `chmod` 修改访问权限位。

# 挂载 DOS、Windows 和 OS/2 分区

在 Linux 下，你也可以访问 DOS、Windows 和 OS/2 分区。对于 DOS 文件系统，显然所有限制都适用（文件名最多为 8+3 个字符，没有链接）。对于 Windows，目前——即在内核 2.2 中——支持 Windows 9x（包括 FAT32）和 Windows NT 4 的文件系统。然而，NT 文件系统只能只读（不可修改）。对于 OS/2 分区，访问也仅限于只读。

取决于允许谁访问 DOS 分区，你必须在 `fstab` 中使用 `gid`、`uid` 和 `umask` 选项（见上文）。如果你只需要偶尔访问 DOS 分区，可以在 `fstab` 条目中指定 `noauto` 选项。这样做的好处是只需轻松执行 `mount /mnt/dos`，而无需指定任何额外选项。另一方面，DOS 分区不会一直被自动挂载，这是一个微小的安全风险（与其他任何分区一样）。

`fstab` 中必要的添加内容如下所示（再次，你必须替换为你系统中使用的设备名称和目录）：

```
# 向 /etc/fstab 的添加
# 将 DOS 分区 /dev/hda5 挂载为 /mnt/dos 到文件系统
/dev/sda5        /mnt/dos       defaults       0 0
# 如果需要只读（不可写）
/dev/sda6        /mnt/dos        ro             0 0
# Windows 9x 分区
/dev/sda7        /mnt/win95      vfat           0 0
# Windows 9x 分区，所有用户自由读写访问
/dev/sda8        /mnt/win95-rw  vfat           umask=111     0 0
# Windows NT 分区
/dev/sda9        /mnt/nt         ntfs           defaults       0 0
# OS/2 分区
/dev/hda10       /mnt/os2        hpfs           defaults       0 0
```

# 挂载 CD-ROM 驱动器

挂载硬盘分区与挂载 CD-ROM 驱动器没有太大区别。后者通常挂载到文件系统的 /mnt/cdrom 或 /cdrom 点。你必须指定你自己的 CD-ROM 驱动器的设备名称，而不是 /dev/hdb。

```
# 向 /etc/fstab 的添加
# 将 CD-ROM 驱动器挂载为 /cdrom 到文件系统
/dev/cdrom      iso9660  ro,user,noautopt  0 0
```

该选项意味着 CD-ROM 驱动器上的数据无法修改（只读）。`user` 允许每个用户（不仅仅是 root）使用 `mount` 和 `umount` 挂载和卸载 CD-ROM 驱动器（但仅需要时）。`noautopt` 确保 CD-ROM 不会在启动时自动挂载到文件系统。如果 CD-ROM 驱动器连接到第二个控制器，你必须将 /dev/hdb 指定为 /dev/hdc 或 /dev/hdd。

不同类型 CD-ROM 的设备名称列在第 102 页。更换光盘时，你必须执行 `mount` 和 `umount` 使 Linux 感知文件系统的变更改（见第 103 页）。只有当你使用内置支持你特定类型 CD-ROM 驱动器的内核时，你才能访问 CD-ROM 驱动器。

从内核 2.2 开始（确切地说，是从 2.0.x 之后），Linux 识别 Juliet 光盘。CD-ROM 用于带有长文件名的 Windows 95/NT。尽管这些 CD-ROM 符合 ISO-9660 标准，但它们没有采用 Unix 下常用的脊槽扩展（ridge extension），而是采用了微软引入的表示长文件名的 Juliet 扩展。如果你使用旧内核，你仍然可以使用 CD-ROM，但你只能看到文件名的短格式。

如果你想挂载 Linux CD 并在没有它的情况下立即执行程序，你需要使用 `mount` 选项 `exec`。通常，出于安全考虑，从 CD-ROM 执行程序是受保护的。

```
root# mount -o exec /cdrom
```

# 挂载交换分区

交换分区的创建通常在 Linux 安装的框架内完成。如果尚未完成，你需要一个专用的硬盘分区，可以使用 `fdisk` 命令创建。必须使用 `t` 将分区类型从 83 (Linux) 修改为 82 (Linux)。在分区用 `mkswap` 格式化后，可以使用 `swapon` 激活它。

如果交换分区要在 Linux 启动时自动使用，则必须将硬盘分区输入到 `fstab`：

```
# 向 /etc/fstab 的添加
# 挂载交换分区
/dev/sdc6 none swap sw 0 0
```

# 挂载交换文件

交换文件的创建通常在 Linux 安装的框架内完成。如果尚未完成，你需要一个专用的硬盘分区，可以使用 `fdisk` 命令创建。必须使用 `t` 将分区类型从 83 (Linux) 修改为 82 (Linux)。在分区用 `mkswap` 格式化后，可以使用 `swapon` 激活它。

如果交换分区要在 Linux 启动时自动使用，则必须将硬盘分区输入到 `fstab`：

```
# 向 /etc/fstab 的添加
# 挂载交换分区
/dev/sdc6 none swap sw 0 0
```

交换文件的创建通常在 Linux 安装的框架内完成。如果尚未完成，你需要一个专用的硬盘分区，可以使用 `fdisk` 命令创建。（*注：原文此处似乎有重复，已根据翻译逻辑处理*）。此处为交换文件的创建步骤：

```
root# dd bs=1024 if=/dev/zero of=/swapfile count=1000
1000+ records in
1000+ records out
root# mkswap /swapfile
Setting swapspace, size = 10194
root# sync
root# swapon /swapfile
```

交换文件要在 Linux 启动时自动使用，则必须将其输入到 `fstab`：

```
# 向 /etc/fstab
# 挂载交换文件
/swapfile none swap 0 0
```

# 硬盘调优

本节专门针对 Linux。它显示了根据硬件增加访问速度的两种方法。第一种方法——使用总线主模式——对所有用户感兴趣。第二种方法——数据分区。

# 总线 DMA

总线 DMA 允许硬盘和主内存之间进行高效的数据传输。传输不是通过 CPU，而是通过 DMA（直接内存访问）通道。总线 DMA 的优势显而易见：数据速率显著提高；同时减少了加载大文件的 CPU 负载。

为了使用 DMA 模式，主板和硬盘必须支持此模式。关于主板支持，建议阅读相应的手册并检查启动期间显示的内核消息：

```
root# dmesg
PIX4: IDE controller on PCI bus 00 dev 21
PIX4: 100% native mode; will probe irqs later
ide0: B-DMA at 0xc800-0xc807, BIOS settings: hdc:DMA, hdd:pio
ide1: B-DMA at 0xc808-0xc8ff, BIOS settings: hdc:DMA, hdd:pio
```

你的硬盘是否支持 DMA 传输可以通过第一个 IDE 硬盘轻松查出：

```
root# hdparm -i /dev/hda
...
DMA=yes, maxDMA=2(fast)
```

前提是可用相应的内核模块。（当前发行版提供的内核满足此要求。在其他发行版中，你可能需要重新编译内核，在 Floppy/IDE 其他块设备选项组将 Intel 82371 PII DMA 支持选项设置为 Y 或 M。）

> 注意 即使满足所有三个条件，出于安全考虑，DMA 模式通常也不会自动激活；取决于芯片组、硬盘长度（根据规范，最大长度为 45 厘米）等等。DMA 模式可能会导致可靠性问题。因此，进行 DMA 实验必须非常小心：对所有不需要的分区执行！理想情况下，你应该有一个不包含任何珍贵或未保存数据的独立分区用于 DMA 测试。

DMA 模式是否已经激活可以通过 `hdparm -d /dev/hda` 确定：

root# /dev/hda:
using_dma = 0 (off)

