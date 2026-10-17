
```
[rose@blob recordables] mkisofs -J -R -o cd.iso .
<-snap->
making a lot of conversions
<-snap->
98.95% done, estimate finish Fri Apr  5 13:54:25 2002
Total translation table size: 0
Total rockridge attributes bytes: 35971
Total directory bytes: 94208
Path table size(bytes): 452
Max brk space used 37e84
166768 extents written (325 Mb)
```

`-J` 和 `-R` 选项用于使 CD-ROM 能够在不同系统上挂载，更多详情请参见手册页。之后，可以使用 `cdrecord` 工具和适当的选项创建 CD：

```
[rose@blob recordables] cdrecord -dev 0,0,0 -speed=8 cd.iso
cdrecord 1.10 (i686-pc-linux-gnu) (C) 1995-2001 Joerg Schilling
```

```
scsidesev : '0,0,0'
scsi bus: 0 target: 0 lun: 0
Linux sg driver version : 3.1.20
Using libscg version 'schily-0.5'
Device type       : Removable CD-ROM
Version           : 0
Response Format: 1
Vendor_info   : 'HP'
Identification  : 'CD-Writer@ 8100 '
Revision          : '1.0g'
Device seems to be: Generic mmc CD-RW.
Using generic SCSI-3/mmc CD-R driver (mmc_cdr).
Driver flags : SWABAUDIO
Starting to write CD/DVD at speed 4 in mmc mode for single session.
Last chance to quit, starting real write in 0 seconds.
Operation starts.
```

根据你的 CD 刻录机性能，现在你有时间抽根烟^^H^H^H 吃点健康的零食和/或喝杯咖啡。任务完成后，你会收到确认信息：

```
Track 01: Total bytes read/written: 341540864/341540864
(166768 sectors).
```

有一些图形工具可以使操作更简便。其中之一是 xcdroast，可以从 X-CD-Roast 网站 [http://www.xcdroast.org/](http://www.xcdroast.org/) 免费获取，并且包含在大多数系统和 GNU 目录中。KDE 和 Gnome 桌面管理器都有制作自己 CD 的功能。

### 9.2.3 使用爵士驱动器、USB 设备等进行备份

这些设备通常挂载到文件系统。挂载过程完成后，它们像普通目录一样被访问，因此你可以使用标准命令来操作文件。

在下面的示例中，图片从 USB 相机复制到硬盘：

```
robin:~-> mount /mnt/camera

robin:~-> mount | grep camera
/dev/sda1 on /mnt/camera vfat (rw,nosuid,nodev)
```

如果相机是你唯一连接到系统的 USB 存储设备，这样做是安全的。但要记住，USB 设备在连接到系统时会被分配 `/dev` 条目。因此，如果你先连接 USB 闪存盘，它将是 `/dev/sda` 条目，如果你之后连接相机，它将被分配给 `/dev/sdb` —— 假设你没有 SCSI 磁盘，它们也在 `/dev/sd*` 上。在较新的系统上，自 2.6 内核以来，一个名为 HAL（硬件抽象层）的热插拔系统确保用户不必承担这种负担。如果你想检查你的设备在哪里，在插入后输入 `dmesg`。

现在你可以复制文件：

```
robin:-> cp -R /mnt/camera/* images/
robin:-> umount /mnt/camera
```

同样，爵士驱动器可以挂载在 `/mnt/jazz` 上。

需要在 `/etc/modules.conf` 和 `/etc/fstab` 中添加适当的行才能使其工作。有关更多信息，请参阅特定硬件的 HOWTO 文档。在使用 2.6.x 或更高版本内核的系统中，你可能还想查阅 `modprobe` 和 `modprobe.conf` 的手册页。

### 9.2.4 使用磁带设备备份数据

这是使用 `tar`（见上文）完成的。`mt` 工具用于控制磁设备，如 `/dev/st0`。关于磁带备份已经写了很多书，因此，有关更多信息，请参阅附录 B 中的阅读列表。请记住，由于数据库架构的原因，可能需要其他备份程序。

适当的备份命令通常放在其中一个 `cron` 目录中，以便定期执行。在较大的环境中，可能会实施免费提供的 Amanda 备份套件或商业解决方案来备份多台机器。然而，操作磁带是系统管理任务，超出了本文档的范围。

### 9.2.5 来自发行版的工具

大多数 Linux 发行版都提供自己的工具以简化你的生活。简要概述如下：

- SuSE：YaST 现在包含扩展的备份和恢复模块。
- RedHat：File Roller 工具提供（压缩）归档的可视化管理。他们似乎更喜欢使用 X-CD-Roast 工具将备份传输到外部设备。
- Mandrake：X-CD-Roast。
- 大多数发行版都附带 BSD `dump` 和 `restore` 实用程序，用于制作 ext2 和 ext3 文件系统的备份。此工具可以写入各种设备，并逐位转储文件（或文件系统）到指定设备。与 `dd` 一样，这允许备份特殊文件类型，例如 `/dev` 中的那些。

## 9.3 使用 rsync

### 9.3.1 简介

`rsync` 程序是一个快速且灵活的远程备份工具。它在 UNIX 和类 UNIX 系统中很常见，易于配置并用于脚本中。虽然 `rsync` 中的 r 代表“远程”，但你不必将此字面意思完全当真。你的“远程”设备也可以是一个 USB 存储设备或硬盘上的另一个分区，你不需要有两台分离的机器。

### 9.3.2 示例：rsync 到 USB 存储设备

如第 3.1.2.3 节所述，我们必须先挂载该设备。可能需要以 root 用户身份执行此操作：

```
root@theserver# mkdir /mnt/usbstore
```

```
root@theserver# mount -t vfat /dev/sda1 /mnt/usbstore
```

#### 用户友好性

越来越多的发行版允许非特权用户访问可移动设备，并自动挂载 USB 设备、CD-ROM 等。

请注意，本指南要求系统中安装了 USB 支持。如果不起作用，请参阅 [USB 指南](http://www.linux-usb.org/USB-guide/) 寻求帮助。使用 `dmesg` 检查 `/dev/sda1` 是否确实是您要挂载的设备。

然后你可以开始实际的备份，例如对 `/home/karl` 目录进行备份：

```
karl@theserver:-> rsync -avg /home/karl /mnt/usbstore
```

通常，请参考手册页以获取更多详细信息。

## 9.4 加密

### 9.4.1 一般说明

#### 9.4.1.1 为什么你应该加密数据？

加密是保密的同义词。在备份的背景下，加密可能非常有用，例如，如果你需要将备份的数据存放在你无法控制访问权限的地方，比如你的服务提供商的服务器上。

除此之外，加密还可以应用于电子邮件：通常，邮件不加密，并且经常在网络上或互联网上公开发送。如果你的消息包含敏感信息，最好对其进行加密。

#### 9.4.1.2 GNU 隐私保护器

在 Linux 系统上，你会找到 GnuPG（GNU 隐私保护器），这是一套与商业可用的 PGP（Pretty Good Privacy）工具兼容的程序。

在本指南中，我们仅讨论加密工具非常简单的用法，并展示你需要生成加密密钥以及使用该密钥为自己加密数据所需的步骤，然后你可以安全地将这些数据存储在公共位置。更高级的使用说明可以在各种命令的手册页中找到。

### 9.4.2 生成密钥

在你开始加密数据之前，你需要创建一对密钥。这对密钥由一个私钥和一个公钥组成。你可以将公钥发送给通信方，他们可以使用它为你加密数据，然后你用你的私钥解密。你始终保留私钥，绝不与其他任何人共享，否则他们将能够解密仅发给你个人数据。为了确保不会发生意外，私钥受密码保护。使用以下命令创建密钥对：
