
这种方式挂载后，只有执行挂载的用户或超级用户才能卸载它。

为延续前面的示例，以下是 /etc/fstab 中所需的条目，以便普通用户可以挂载 DOS 软盘、Linux 软盘、CD 和 Zip 磁盘：

```
# For mounting Linux formatted floppies
/dev/fd0   /mnt/fd0   ext2   noauto,nosuid,user,rw   1   0

# For mounting DOS/Windows formatted floppies
/dev/fd0   /mnt/dosA  vfat   noauto,nosuid,user,rw   1   0

# For mounting CD-ROM disks
/dev/cdrom /mnt/cdrom iso9660 noauto,nosuid,user,ro 1 0

# For mounting Linux formatted ZIP disks
/dev/sda1 /mnt/zip ext2 noauto,nosuid,user,rw 1 0

# For mounting DOS/Windows formatted ZIP disks
/dev/sda4 /mnt/zipdos vfat noauto,nosuid,user,rw 1 0
```

## 可移动媒体的自动挂载

处理可移动媒体的另一种选择是配置 Linux autofs，以便在用户只需插入媒体并访问相应目录时即可支持这些设备。默认情况下，只要安装了 autofs 支持，Red Hat Linux 就为 CD 驱动器支持此功能。使用此默认设置，用户可以通过将 CD 放入驱动器并将目录更改为 /misc/cd 来访问 CD 驱动器。用户使用完 CD 后，他只需将目录更改到 CD 文件系统之外的其他位置，然后等待 60 秒的超时时间到期后再从驱动器中卸载 CD 即可。

设置此支持所需的配置文件是 /etc/auto.master，即主 autofs 配置文件，以及由其指定的包含可移动媒体条目的文件。为延续上一节的示例，以下是需要创建以支持自动挂载的必需配置文件：

```
/etc/auto.master

# Sample auto.master file
# Format of this file:
# mountpoint map options
# For details of the format look at autofs(8).
```

```
# An entry for mountpoint /misc, which is used for mounting removable
# media devices as defined in the map file /etc/auto.misc. These
# devices will be unmounted following an inactivity timeout of 30
# seconds.
/misc    /etc/auto.misc    -timeout 30

/etc/auto.misc

# Allow the mounting of CD-ROM disks on /misc/cdrom
cdrom    -fstype=iso9660,ro    :/dev/cdrom

# For mounting Linux formatted floppies
fd0      -fstype=ext2,nosuid    :/dev/fd0

# For mounting DOS/Windows formatted floppies
dosA     -fstype=vfat,nosuid    :/dev/fd0

# For mounting Linux formatted ZIP disks
zip      -fstype=ext2,nosuid    :/dev/sda1

# For mounting DOS/Windows formatted ZIP disks
zipdos   -fstype=vfat,nosuid    :/dev/sda4
```

有了这些配置文件，并且在启动时运行 /etc/rc.d/init.d 中的 autofs 脚本，用户将能够访问系统上的软盘驱动器、Zip 磁盘和 CD。他们可以通过将目录更改为 misc 下对应于 auto.misc 文件中某个键的目录来实现。

允许访问的这种方法有许多优点。其中之一是用户无需学习任何特殊命令即可使用它们。此外，auto.master 和 auto.misc 文件可以纳入 NIS 设置中，从而消除了在您希望授予访问权限的每台主机上修改 fstab 文件的需要。缺点是，超时参数可能成为一个问题，尤其是在用户缺乏耐心的情况下。他们可能不喜欢必须等待 30 秒才能取出媒体的想法。

有关配置和使用 autofs 以及使用 amd、Berkeley automount 守护进程的信息，请参阅第 15 章“共享资源（打印和文件服务）”，其中更详细地描述了它们的使用。

## 混合方法

授予对可移动媒体访问权限的另一种潜在方法是采用混合方法。在这种方法中，您可能会配置 mtools 以允许访问 DOS 格式的软盘和 zip 磁盘，并使用 autofs 或用户挂载方法来允许访问 Linux 格式的文件系统和 CD-ROM 驱动器。这种方法体现了使用合适工具完成工作的原则。再次需要指出的是，不应随意授予用户对可移动媒体设备的访问权限，在做出决定时应考虑安全问题。

## 摘要

本章介绍了 Linux 支持的一些可移动媒体设备，包括软盘驱动器、CD-ROM、CD-R、CD-RW 以及连接到并行端口的设备，如 Zip 驱动器和便携式 ATAPI/IDE 设备。它详细介绍了使用 CD-R 和 CD-RW 驱动器创建自己的 CD 数据盘以及这些设备的一些用途。它还简要介绍了如何通过并行端口将 Zip 驱动器连接到系统，并介绍了使用 paride 驱动程序支持其他类型的设备（如 MicroSolutions 背包设备）的信息。最后，本章介绍了几种允许用户访问这些可移动设备的方法，而无需授予他们 root 访问权限或损害安全性。您可以在 Red Hat 系统的以下文件中找到更多信息来源：

- `/usr/src/linux/Documentation/paride.txt`
- `/usr/doc/HOWTO/mini/ZIP-Drive`

## 备份和恢复

## 第四部分

## 本部分内容

- 11 如何备份以及备份什么 .299
- 12 媒体选择与存储 333
- 13 数据丢失恢复 345

## 11
章节

## 如何备份以及备份什么

## 本章内容

- 文件系统内容 301
- 查找新文件 303
- 备份策略 305
- 部分备份 309
- 将新的 Red Hat Linux 系统上线 310
- 备份类型 313
- 制定轮换计划 315
- 开发备份脚本 323

你一定听说过墨菲定律，其最简单的形式表述为：“凡是可能出错的，终会出错。” 我并不是第一个观察到这种自然现象的人，但我确实观察到了。反复如此。当处理计算机时尤其如此。

在某个时间点，我保证，你将有一份或多份文件因某种原因变得完全无法读取。原因可能是硬件故障、火灾、水灾、地震、静电、用户手指问题，甚至是太阳黑子（别笑——根据天文学家的说法，2000 年将是太阳黑子活动的一年。查看 NASA 的网页 http://wwws1.msfc.nasa.gov/newhome/headlines/ast190ct98_1.htm。你已被警告！）硬盘和软盘驱动器都有活动部件，而活动部件最终会磨损。

如果发生任何上述情况，你和你的用户会非常感激有备份。在廉价存储媒体的今天，没有备份是不可原谅的。作为系统管理员，你的首要任务是保持系统运行。备份排在第二位。对“备份什么，如何备份？”这一问题的简短回答是系统管理员可能被问到的几乎任何计算机问题的最受欢迎的单一答案。那就是，当然，“视情况而定。” 你即将学习它取决于什么，以便你能用终极的系统管理员武器——知识——来应对你的特定需求。

正确实施备份所需的知识可分为四个大类：

- 要备份的内容（文件系统内容）
  确定需要备份什么以及不需要备份什么，可以让你在任何资源上都能做出最佳利用。
- 备份到哪里（备份设备）
  有些备份设备在每台计算机上都可用。其他设备则只有少数人才能使用。
- 如何备份（备份命令）
  用于执行备份的程序种类越来越多，但“老牌”命令仍然和以前一样有用。
- 何时备份（站点策略）
  备份的频率和彻底程度取决于许多因素，包括数据价值与备份成本之间的权衡。

