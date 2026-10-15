
用户并不急需这些打包格式，而且它们对开源社区的提升也微小。因此，在解决各种性能问题之前，不建议使用这些格式。

### 总结

在接下来的章节中，我们将探索许多涵盖广泛应用领域的不同程序。虽然这些程序中的大多数是默认已安装的，但如果没有提供必要的程序，我们可能需要安装额外的包。凭借我们对包管理新获得的知识，我们在安装和管理所需的程序时应该不会遇到任何问题。

## Linux 软件安装的迷言

从其他平台迁移到 Linux 的用户有时会成为一种“迷言”的受害者，这种迷言认为在 Linux 下安装软件很困难，而且不同发行版之间的各种打包方案是一种障碍。好吧，这确实是一个障碍，但仅对于那些分发仅二进制版本秘密软件的专有软件供应商而言。

Linux 软件生态系统基于开源代码理念。如果一个程序开发者发布了代码，那么发行版的相关人员可能会对该程序进行打包并将其他们的仓库中。这种方法确保了程序很好地集成到发行版中，并为用户提供了“一站式购物”软件的便利，而不是去搜索每个程序的网站。

设备驱动的处理方式相同，只不过它们不再是发行版仓库中的独立项目，而是变成了 Linux 内核的一部分。通常来说，Linux 中没有所谓的“驱动器光盘”。要么内核支持某个设备，要么不支持，而 Linux 内核支持很多设备。事实上，支持的设备比 Windows 的多得多。

缺乏驱动支持通常由三个原因之一引起：

## 14 – 包管理

1. **设备太新了。** 由于许多硬件厂商并不会积极支持 Linux 开发，因此需要 Linux 社区的成员来编写内核驱动代码。这需要时间。

2. **设备非常奇特。** 并不是所有的发行版都包含所有可能的设备驱动。每个发行版都构建自己的内核，由于内核是可配置的，它们可能会忽略某个特定的设备。通过定位并下载驱动的源代码，你完全可以自己去编译并安装驱动。这个过程并不困难，但相当繁琐。我们将在后面的章节中讨论编译软件。

3. **硬件厂商隐藏了某些东西。** 它既没有发布 Linux 驱动的源代码，也没有发布技术文档供人创建驱动。这意味着硬件厂商正试图对设备的编程接口保密。

## 进阶阅读

花些时间了解你所在发行版的包管理系统。每个发行版都为其包管理工具提供了文档。此外，这里有一些通用资源：

- Debian GNU/Linux FAQ 中关于包管理的章节提供了 Debian 系统上包管理的概述：https://www.debian.org/doc/manuals/debian-faq/pkg-basics.en.html
- RPM 项目的主页：http://www.rpm.org
- 了解背景知识，维基百科有一篇关于元数据的文章：http://en.wikipedia.org/wiki/Metadata
- 一篇 Snap、Flatpak 和 AppImage 格式的优秀文章：https://www.baeldung.com/linux/snaps-flatpak-appimage

## 15 – 存储媒体

在之前的章节中，我们查看了如何在文件级别操作数据。在本章中，我们将考虑设备级别的数据。Linux 在处理存储设备方面具有强大的能力，无论是物理存储、网络存储，还是虚拟存储设备如 RAID 和 LVM。

### 挂载与卸载设备

`mount` 命令用于挂载文件系统。不带详细信息的输入命令将显示当前挂载的文件系统：

```
me@linuxbox ~$ mount
/dev/sda2 on / type ext4 (rw)
proc on /proc type proc (rw)
sys on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
```

列表的格式如下：设备在 挂载点 类型 文件系统类型 (选项)。例如，第一行显示 `/dev/sda2` 是根文件系统，类型为 `ext4`，且可读可写。

**提示：** 用户会发现此列表充满了系统上安装的 snap 软件包创建的“loop”设备。要查看更整洁的列表，请使用 `mount | grep -v snap` 或 `mount | grep ^dev`

对于我们的第一个实验，我们将使用一个 4 GB 的闪存盘。首先，让我们看看在插入设备之前的系统：

```
[me@linuxbox ~]$ mount | grep /dev/sd
/dev/sda2 on / type ext4 (rw,relative,errors=remount-ro)
/dev/sda1 on /boot/efi type vfat (rw,relime,fmask=0077,dmask=0077,codepage=437,charset=iso8859-1,shortname=mixed,errors=remount-ro)
/dev/sd1 on /home type ext4 (rw)
```

我们通过 `grep` 管道处理输出，只列出 `/dev/sd*` 设备。

插入闪存盘后：

```
[me@linuxbox ~]$ mount | grep /dev/sd
/dev/sda2 on / type ext4 (rw,relatine,errors=remount-ro)
/dev/sda1 on /boot/efi type vfat (rw,relatine,fmask=0077,dmask=0077,codepage=437,charset=iso8859-1,shortname=mixed,errors=remount-ro)
/dev/sdb1 on /home type ext4 (rw,relatine)
/dev/sdc on /media/me/C911-C314 type vfat (rw,nisuid,nodev,relatime,uid=1000,gid=1000,fmask=0022,dmask=0022,codepage=437,charset=iso8859-1,shortname=mixed,showexec,utf8,errors=remount-ro)
```

闪存盘在该系统中为 `/dev/sdc`，已挂载到 `/media/me/C911-C314`，类型为 `vfat`。

> 警告：在接下来的示例中，务必注意你系统中所使用的实际设备名称，不要使用本文中的名称！

现在卸载驱动器并重新挂载到文件树的另一个位置：

```
[me@linuxbox ~]$ sudo -i
[sudo] password for me:
[root@linuxbox ~]# umount /dev/sdc
[root@linuxbox ~]# mkdir /mnt/flash
[root@linuxbox ~]# mount -t vfat /dev/sdc /mnt/flash
[root@linuxbox ~]# cd /mnt/flash
[root@linuxbox ~]# ls
```

注意看当我们尝试卸载设备时发生了什么：

```
[root@linuxbox ~]# umount /mnt/flash
mount: /dev/sdc is busy
```

可以通过杀死占用进程来卸载：

```
[root@linuxbox ~]# fuser -k /mnt/flash
[root@linuxbox ~]# umount /mnt/flash
```

### 卸载设备的重要性

在卸载设备之前，确保数据已写入至关重要。在某些情况下，不卸载设备会导致文件系统损坏。

### 设备名称

如果我们列出 `/dev` 目录，我们可以看到有很多设备。表 15-2 列出了一些命名的模式。

```
[me@linuxbox ~]$ ls /dev
```

表 15-2：Linux 存储设备名称

| 模式 | 设备 |
| :--- | :--- |
| `/dev/fd*` | 软盘。 |
| `/dev/hd*` | 旧版系统上的 IDE 磁盘。 |
| `/dev/lp*` | 打印机。 |
| `/dev/sd*` | SCSI 磁盘。在现代 Linux 系统中，内核将所有类磁盘设备视为 SCSI 磁盘。 |
| `/dev/sr*` | 光驱器。 |

在现代基于 systemd 的系统中，使用此命令来跟踪 systemd 日志：

```
[me@linuxbox ~]$ sudo journalctl -f
```

插入可移动设备后，内核会进行探测并分配名称，如 `[sdc]`。

我们还有另一种方法确定设备名称：`lsblk` 命令。该命令列出所有连接到系统的块设备，无论它们是否已挂载。

```
[me@linuxbox ~]$ lsblk
```

| NAME | MAJ:MIN | RO | TYPE | MOUNTPOINTS |
| :--- | :--- | :--- | :--- | :--- |
| sda | 8:0 | 0 | 111.8G disk | |
| ├─sda1 | 8:1 | 0 | 976M part | /boot/efi |
| └─sda3 | 8:3 | 0 | 14.9G part | [SWAP] |
| sdb | 8:16 | 0 | 931.5G disk | |
| ├─db1 | 8:17 | 0 | 922.2G part | /home |
| └─db2 | 8:18 | 0 | 9.3G part | |
| sr0 | 11:0 | 1 | 1024M rom | |

> 提示：使用 `tail -f /var/log/syslog` 或 `journalctl -f` 技术是近实时观察系统运行的好方法。
