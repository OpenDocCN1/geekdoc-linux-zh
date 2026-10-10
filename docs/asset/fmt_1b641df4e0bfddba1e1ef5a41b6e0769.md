
### raidtab configuration for RAID 1 volume

```
raiddev /dev/md0
    raid-level          1
    nr-raid-disks       2
    nr-spare-disks      0
    persistent-superblock 1
    chunk-size          4

    device        /dev/yourfirstpartition
    raid-disk     0
    device        /dev/yoursecondpartition
    raid-disk      1
```

首先需要注意的是一个新选项，`nr-spare-disks`。如果你有任何想要用作备用盘（standby）的分区，你可以按如下方式将它们添加到驱动器列表中：

```
device      /dev/anotherpartition
spare-disk  0
```

然后，将`nr-spare-disks`的值更新为适当的数量。如果镜像磁盘向内核报告故障，你的备用磁盘将被征用，内核将开始在磁盘上重建镜像数据。请记住，由于数据是冗余地写入两个磁盘的，当备用驱动器被交换到镜像中时，需要同步过程将备用驱动器同步到其他镜像。幸运的是，在此过程中镜像仍然可用，但在完成之前运行速度会稍慢。

启动 RAID 1 卷的命令行方法与设置 RAID 0 的方法相同。但有一件事你应该观察：在你输入`mkraid /dev/md0`后，阵列将开始同步数据。你可以通过输入`cat /proc/mdstat`来观察进度：

```
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
```

![](img/df365d352a104b50fea29e59a052de4d_1034_0.png)

```
md1 : active raid1 sda6[1] hda5[0] 256896 blocks [2/2] [UU] resync=89%
finish=0.0min
unused devices: <none>
```

如图所示，重同步（resync）正在进行中，随时可能完成。在重同步完成后，`cat /proc/mdstat`将显示如下内容：

```
Personalities : [linear] [raid0] [raid1]
read_ahead 1024 sectors
md1 : active raid1 sda6[1] hda5[0] 256896 blocks [2/2] [UU]
unused devices: <none>
```

镜像现在已经同步。请注意，即使同步过程正在进行中，开始使用镜像也是完全安全的；驱动器 IO 会稍慢，但不会明显变慢，因为内核在重同步过程中会控制自身节奏，以确保镜像 IO 性能不受影响。现在你已经创建了 RAID 1 卷，请挂载它并进行操作。注意写入稍慢，读取稍快。

Linux 下的软件 RAID 1 实现极其灵活和健壮。使用 RAID 1 的一个主要优点是，在紧急情况下很容易将其关闭。例如，假设你镜像中的一个硬盘故障，且已过保修期。你身无分文，没有钱购买替换驱动器。关闭 RAID 1 镜像很容易：

```
> umount /mnt/raid
> raidstop /dev/md0
```

然后，假设`/dev/hda3`是位于正常工作驱动器上的 RAID 1 分区，请将`/etc/fstab`中所有对`/dev/md0`的引用更改为`/dev/hda3`。由于每个镜像本身都包含一个有效的`ext2`文件系统，你可以以非镜像模式继续正常操作你的机器：

```
> mount /dev/hda3 /dev/raid
```

现在系统可以关机，并将故障驱动器丢弃！这个技巧仅适用于 RAID 1；它不适用于 RAID 0、4、5 或线性模式。

现在你应该对 Linux 内核灵活的软件 RAID 能力有了很好的概述。如果你对设置 RAID 4 或 5 卷或线性卷感兴趣，请查看以下 man 页面：

```
> man mdraid
> man raidtab
```

它们应该提供你所需要的全部信息。不幸的是，大多数基于 Web 的信息（包括 Software-RAID HOWTO）严重过时，并且与在现代 Linux 上使软件 RAID 设置正常工作所需的步骤不同。考虑到这一点，你可能想要查看 `http://www.linux.org/linux/raid.html`，其中列出了当前 Linux 系统中所有可用的 RAID 资源。软件 RAID 是提升系统可靠性和性能的绝佳工具；我知道它对我的机器性能产生了巨大的积极影响！

### 摘要

Caldera OpenLinux 2.2 引入了一个名为 LIZARD 的创新图形化安装过程，为 Linux 用户提供了近乎理想的“开箱即用”体验。此外，Caldera 还提供其早期的文本安装程序 LISA。虽然 LISA 功能不如 LIZARD 先进，但它提供了对安装过程更多的控制。

虽然许多用户选择在一个分区中安装 Caldera，但也有几种值得考虑的其他分区选项。当选择的分区方案与系统的预期用途相配合时，磁盘性能往往可以得到显著增强。此外，Linux 软件 RAID 可用于提高关键数据的完整性和可用性，并进一步提升磁盘 I/O 性能。

## 附录 C

## 参考文献

Costales, Bryan, and Eric Allman. *sendmail, Second Edition.* O’Reilly and Associates, Inc., 1997. ISBN 1-56592-222-0. 这本厚重且令人望而生畏的书介绍了关于配置 `sendmail` 的所有你想要知道的内容。这本书索引完善、内容详尽，读起来就像加了类固醇的 GNU info 页面一样。

Garfinkel, Simson, and Gene Spafford. *Practical UNIX & Internet Security, Second Edition.* O’Reilly and Associates, Inc., 1996. ISBN 1-56592-148-8. 这本书是 UNIX 和网络安全的圣经。如果你甚至只是考虑将你的 Linux 机器接入 Internet，你就必须阅读这本书。

Harbison, Samuel P., and Guy L. Steele, Jr. *C: A Reference Manual, Fourth Edition.* Prentice Hall, 1995. ISBN 0-13-326224-3. 这是一本详细的 C 语言参考手册，涵盖了 ANSI C 和常见的预 ANSI C 方言。

Harrison, Mark, and Michael McLennan. *Effective Tcl/Tk Programming: Writing Better Programs with Tcl and Tk.* Addison-Wesley Publishing Company, 1998. ISBN 0-201-63474-0. 这本书假设读者具备 Tcl/Tk 的基础知识。它描述了高级特性和出色的编程技巧。书中附带了一个可自由重用的 Tcl 例程库。作者对 Tcl/Tk 有着深厚的赞赏，其示例程序清晰且优雅。

Lamport, Leslie. *LaTeX: A Document Preparation System, Second Edition.* Addison-Wesley Publishing Company, 1996. ISBN 0-201-52983-1. 这本由 LaTeX 作者撰写的书，清晰且幽默地介绍了排版系统。如果你想学习 LaTeX，强烈推荐此书。

Ousterhout, John K. *Tcl and the Tk Toolkit.* Addison-Wesley Publishing Company, 1994. ISBN 0-201-63337-X. 这本由 Tcl 和 Tk 作者撰写的书解释了如何使用该语言和工具包。虽然内容稍显陈旧，但大多仍然准确。这也是我读过的最清晰的 Tcl 和 Tk 教程。

Plauger, P. J. *The Standard C Library.* Prentice Hall, 1992. ISBN 0-13-131509-9. 这本书由 C 标准化委员会成员之一撰写，对 C 标准库进行了极其详尽的描述。书中还包含了标准 C 库完整实现的源代码。

Rubini, Alessandro. *Linux Device Drivers.* O’Reilly and Associates, Inc., 1998. ISBN 1-56592-292-1. 这本书从设备驱动的角度描述了 Linux 内核内部机制。鉴于 Linux 开发的速度极快，此类书籍很快就会过时。尽管如此，这本书在深入阅读 Linux 内核代码之前仍是一个绝佳的起点。

Schneier, Bruce. *Applied Cryptography: Protocols, Algorithms, and Source Code in C, Second Edition*. John Wiley and Sons, Inc., 1996. ISBN 0-471-11709-9. 这本书是加密协议和算法的百科全书式参考。作为额外福利，读起来很有趣。如果你被诱使去发明自己的加密算法，请阅读这本书以了解为什么这是一个坏主意。

Stevens, W. Richard. *Advanced Programming in the UNIX Environment*. Addison-Wesley Publishing Company, 1993. ISBN 0-201-56317-7. 这是一本精彩的参考书，描述了 UNIX API 和高级 UNIX 编程技术。这是首屈一指的 UNIX 编程参考文本。

*TCP/IP Illustrated, Volume 1: The Protocols*. Addison-Wesley Publishing Company, 1994. ISBN 0-201-63346-9. 这本书详细描述了 IP、TCP、UDP 和 ICMP 协议。Stevens 使用 `tcpdump` 工具展示了数百个测试用例，使抽象的协议描述通过具体且易于理解的示例得以阐明。

*UNIX Network Programming, Volume 1, Second Edition: Networking APIs: Sockets and XTI*. Prentice Hall, 1998. ISBN 0-13-490012-X. 这本书非常详细地描述了 Sockets API（Linux 使用此 API）。如果你希望在 UNIX 下编写客户端-服务器软件，请阅读这本书。

## 附录 D

### RPM 列表

本书中的所有示例都假设已完整安装 Caldera OpenLinux。如果没有进行完整安装，可能会缺失某些软件。下表列出了 `/bin`、`/sbin`、`/usr/bin` 和 `/usr/sbin` 中的所有可执行文件及其所属的 RPM 包。请注意，随着 Caldera OpenLinux 的更新，RPM 版本号可能会发生变化，但 RPM 的基础名称应保持不变。

有些文件不属于任何软件包。例如，`/bin/csh` 被标记为不属于任何软件包。这些文件都是在安装过程中设置的符号链接。要查找创建它们的软件包，请运行 `rpm -q -f real_file`，其中 `real_file` 是指符号链接指向的文件。

#### 表 D.1 OpenLinux 可执行文件及其源 RPM

| Executable | Directory | RPM |
| :--- | :--- | :--- |
| `activate` | `/sbin` | `lilo-0.21-6` |
| `addtosmbpass` | `/usr/sbin` | `samba-2.0.5-1` |
| `adduser` | `/usr/sbin` | `adduser-1.2-1` |
| `amd` | `/etc/rc.d/init.d` | `am-utils-6.0-4` |
| `amd` | `/usr/sbin` | `am-utils-6.0-4` |
| `arch` | `/bin` | `util-linux-2.99-4` |
| `arp` | `/sbin` | `net-tools-1.52-4` |
| `atd` | `/etc/rc.d/init.d` | `at-3.1.7-1` |
| `atd` | `/usr/sbin` | `at-3.1.7-1` |
| `avmcapctrl` | `/sbin` | `isdn4k-utils-3.0beta2-4` |
| `badblocks` | `/sbin` | `ext2fs-1.14-2` |
| `bash` | `/bin` | `bash-1.14.7-9` |
| `bash2` | `/bin` | `bash2-2.03-1` |
| `bigfs` | `/etc/rc.d/init.d` | `SysVinit-scripts-1.05-5` |
| `booteer` | `/sbin` | `SysVinit-scripts-1.05-5` |
| `booteerd` | `/sbin` | `SysVinit-scripts-1.05-5` |
| `box` | `/bin` | `lisa-4.0-7` |
| `bru` | `/bin` | `BRU-15.0P.11` |
| `build_menu` | `/bin` | `lisa-4.0-7` |
| `bunzip2` | `/bin` | `bzip2-0.9.0b-1` |
| `bzcat` | `/bin` | `bzip2-0.9.0b-1` |
| `bzip2` | `/bin` | `bzip2-0.9.0b-1` |
| `bzip2recover` | `/bin` | `bzip2-0.9.0b-1` |
| `cat` | `/bin` | `textutils-1.22-3` |
| `cfdisk` | `/sbin` | `util-linux-2.9s-4` |
| `chat` | `/usr/sbin` | `ppp-2.3.8-1` |
| `checkpc` | `/usr/sbin` | `LPRng-lpd-3.5.3-1` |
| `chgrp` | `/bin` | `fileutils-4.0-1` |
| `chmod` | `/bin` | `fileutils-4.0-1` |
| `chown` | `/bin` | `fileutils-4.0-1` |
| `chpasswd` | `/usr/sbin` | `shadow-misc-1.1-3` |
| `chroot` | `/usr/sbin` | `sh-utils-1.16-7` |
| `clcandir` | `/usr/sbin` | `cleandir-1.0-1` |
| `convert_smbpasswd` | `/usr/sbin` | `samba-2.0.5-1` |
| `convertsmbpasswd` | `/usr/sbin` | `samba-2.0.5-1` |
| `cp` | `/bin` | `fileutils-4.0-1` |
| `cpio` | `/bin` | `cpio-2.4.2-3` |
| `cron` | `/etc/rc.d/init.d` | `vixie-cron-3.0.1-18` |
| `cron` | `/usr/sbin` | `vixie-cron-3.0.1-18` |
| `cronloop` | `/usr/sbin` | `crontabs-1.12-1` |
| `ctags` | `/bin` | `vim-5.3-4` |
| `ctrlaltdel` | `/sbin` | `util-linux-2.9s-4` |
| `date` | `/bin` | `sh-utils-1.16-7` |
| `db_print` | `/bin` | `lisa-4.0-7` |
| `dd` | `/bin` | `fileutils-4.0-1` |
| `debugfs` | `/sbin` | `ext2fs-1.14-2` |
| `depmod` | `/sbin` | `modutils-2.1.121-9b` |
| `df` | `/bin` | `fileutils-4.0-1` |
| `dhcpcd` | `/sbin` | `dhcpd-1.3.17p4-0` |
| `dhcpd` | `/etc/rc.d/init.d` | `dhcpd-1.0pl2-3` |
| `dhcpd` | `/usr/sbin` | `dhcpd-1.0pl2-3` |
| `diald` | `/usr/sbin` | `diald-0.16-1` |
| `dip` | `/usr/sbin` | `dip-3.3.7a-9` |
| `diplogin` | `/usr/sbin` | `dip-3.3.7a-9` |

![continues](img/df365d352a104b50fea29e59a052de4d_1044_0.png)

## 附录 D

## 表 D.1

| 可执行文件 | 目录 | RPM |
| :--- | :--- | :--- |
| `dmseg` | `/bin` | `util-linux-2.9s-4` |
| `dnsdomainname` | `/bin` | `net-tools-1.52-4` |
| `do_calc` | `/bin` | `lisa-4.0-7` |
| `do_echo` | `/bin` | `lisa-4.0-7` |
| `do_netcalc` | `/bin` | `lisa-4.0-7` |
| `do_quote` | `/bin` | `lisa-4.0-7` |
| `domainname` | `/bin` | `nis-client-2.0-8` |
| `dpasswd` | `/usr/sbin` | `shadow-misc-1.1-3` |
| `dump` | `/sbin` | `dump-0.4b4-2` |
| `dumpe2fs` | `/sbin` | `ext2fs-1.14-2` |
| `dumpreg` | `/usr/sbin` | `svgalib-1.3.1-2` |
| `e2fsck` | `/sbin` | `ext2fs-1.14-2` |
| `e2label` | `/sbin` | `ext2fs-1.14-2` |
| `echo` | `/bin` | `sh-utils-1.16-7` |
