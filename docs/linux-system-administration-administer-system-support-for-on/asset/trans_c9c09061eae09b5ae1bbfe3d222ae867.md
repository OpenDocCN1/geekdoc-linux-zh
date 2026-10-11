

![](img/8ad518fddafc7f5e73715a2604b61d50_354_0.png)

> 务必特别注意确保该命令语法的准确性。例如，如果反过来使用上述语法，将会把软盘驱动器的内容倾倒到 /zImage 文件中。我想我不必告诉你不要这样做，但还是请勿尝试。

## 使用 cpio 进行备份

cpio 命令用于在归档文件和目录之间复制文件。它与 find 命令配合使用效果极佳，因此你可以构建一些用于备份的便捷命令。

find 命令有一个 -cpio 选项，允许你对找到的文件进行归档。例如，你找到了所有的 .rhosts 文件。你希望将这些文件归档到磁带驱动器中，以便记录哪些用户不够谨慎：

```
find / -name .rhosts -cpio /dev/rmt0;
```

列表 10-3 展示了如何使用 cpio 命令进行备份。

### 列表 10-3：使用 cpio 进行备份

```
# cpio -help

Usage: cpio [-o|--create] [-OacvABLV] [-C bytes] [-H format] [-M message]
    [-0 [user@]host::archive] [-F [user@]host::archive]
    [--file=[user@]host::archive] [--format=format] [--message=message]
    [-null] [--reset-access-time] [-verbose] [-dot] [--append]
    [-block-size=blocks] [--dereference] [-io-size=bytes] [--quiet]
    [--force-local] [--help] [-version] < name-list > archive
    cpio [-i|--extract] [-bcdfmnrtuvBSV] [-C bytes] [-E file] [-H format]
    [-M message] [-R [user]::[group]] [-I [user@]host::archive]
    [-F [user@]host::archive] [--file=[user@]host::archive]
    [-make-directories] [--nomatching] [--preserve-modification-time]
    [--numeric-uid-gid] [--rename] [-list] [-swap-bytes] [-swap] [-dot]
    [-unconditional] [-verbose] [-block-size=blocks] [-swap-halfwords]
    [-io-size=bytes] [-pattern-file=file] [-format=format]
    [-owner=[user]::[group]] [-no-preserve-owner] [--message=message]
    [-force-local] [-no-absolute-filenames] [-sparse] [-only-verify-crc]
    [-quiet] [-help] [-version] [pattern...] < archive
    cpio [-p|--pass-through] [-OadmuvLV] [-R [user]::[group]]
    [-null] [--reset-access-time] [--make-directories] [-link] [--quiet]
    [--preserve-modification-time] [-unconditional] [-verbose] [-dot]
    [--dereference] [-owner=[user]::[group]] [-no-preserve-owner]
    [-sparse] [-help] [-version] destination-directory < name-list
```

如果你希望将整个磁盘备份到另一个硬盘，你可以这样做：

```
# find / -cpio /dev/hbd
```

你也可以单独使用 cpio 命令。使用 -o 选项，可以将输出读取到 cpio 命令中。

```
# ls -R /home | cpio -o > /dev/rmt0
```

这将递归列出 /home 目录的内容，并将输出重定向到第一个磁带驱动器。

## 恢复文件

当你做好备份后，你很快就会庆幸自己这样做了。如果你的某个用户意外删除了其主目录，你不必恐慌。如果你使用的是 tar，可以简单地纠正这个问题。

```
# tar -xvfZ /zipdrive/backup-home-dir.tar.gz /opt/restore
```

![](img/8ad518fddafc7f5e73715a2604b61d50_355_0.png)

即使你知道备份数据的内容，设置一个单独的恢复目录也是有益的，这样你就不会无意中覆盖掉不希望删除的文件。

如果你使用的是 dd 命令，操作类似。再次确保不要颠倒 if 和 of 设备。

```
# dd if=/dev/rmt0 of=/opt/restore
```

对于 cpio，其语法与上述创建备份的示例不同。以下命令将从磁带驱动器恢复特定文件。

```
# cd /opt/restore
# cpio -id filename < /dev/rmt0
```

## 电源管理

你如何应对停电？从基础做起：为你的台式计算机配备不间断电源（UPS），并确保持续给笔记本电脑电池充满电。

### UPS 状态

对于 UPS 电池状态，`upsd` 守护进程专门用于监控 UPS。目前有一些工具可在 <http://sunsite.unc.edu/pub/Linux/system/ups> 获取。还有一些其他监控工具，如 Genpower，它们具备自动关机和低电量检测功能。表 10-3 列出了许多当前可用的工具。

**表 10-3 UPS 电源管理工具**

| 工具 | 文件 | 描述 |
| :--- | :--- | :--- |
| Apcd | apcd-0.5.tar.gz | 在“智能”模式下监控 APC SmartUPS |
| Apcupsd | apcupsd-3.3.0.bin.linux.tar.gz | 在“简单”模式下为 APCC 产品提供 UPS 电源管理 |
| DumpUPSd | dumbupsd-0.1.tar.gz | 提供 dump UPS 的启动和关闭脚本 |
| Genpower | genpower-1.0.1.tgz | 高度可配置的 UPS 监控器 |
| Powerd | powerd-2.0.tar.gz | 网络感知守护进程，用于连接简单 UPS 的主机的开机和关机 |
| SmartUPS | smartups-1.1.tgz | SmartUPS 的 X11 负载监控器 |
| Upsd | ups.tar.gz | 用于与 Powerbox UPS 交互的程序 |
| Upsd Power Monitor Daemon | upsd-1.0.tgz | 在“简单”模式下监控 APC BackUPS 或 SmartUPS |
| Usyd | usyd-2.0.0.tgz | 不间断电源监控器 |

### 笔记本电脑电池状态

电源管理支持可以直接编译到 Linux 内核中。这意味着，例如，你可以关闭笔记本电脑而无需手动关机。（除了内核支持，你还可以从 <http://sunsite.unc.edu/pub/Linux/system/power> 获取实用程序。）表 10-4 列出了笔记本电脑电源管理工具。

**表 10-4 笔记本电脑电源管理工具**

| 工具 | 文件 | 描述 |
| :--- | :--- | :--- |
| Apm Daemon | apmd-2.4.tar.gz | 通过高级电源管理监控电池状态 |
| Apm X | apmx-0.00.tgz | 通过百分比、充电和电池离线状态监控电池电量 |
| Tkbattery | tkbattery-1.0.tgz | 基于 X 的低电量警告监控器 |
| Xbatcheck | xbatcheck-1.2.tar.gz | 带有临界电量警报的基于 X 的电池监控器 |
| X Battery Status Viewer | xbatstat-0.5.2.tar.gz | 通过 /proc/apm 监控电池状态，需要 XFORMS-0.81 |
| Xbattery | xbattery-1.0.tar.gz | 在 X 窗口中监控电池和交流电源状态 |

你有多种程序可用于笔记本电脑的电源管理。其中包括 *apmd*，它是一个用于监控电池电量的守护进程。要在 X 环境下进行监控，你可以使用 *apmx*。*tkbattery* 是一个高度可配置的电池监控器，它像上面列出的两个程序一样使用 APM。此外，还有三种其他工具允许你在 X 中监控电池状态甚至交流电源。它们是 *xbatcheck*、*xbatstat* 和 *xbattery*。

## 救援磁盘

如果你正在折腾你的系统，或者你的系统出于不明原因恰好崩溃了（这也会发生在我们每个人身上），你应该准备某种救援磁盘。

你可以始终使用内核中的 *make zdisk* 命令制作启动磁盘，但手头有一个救援磁盘总是好的。在 http://sunsite.unc.edu/pub/Linux/system/recovery/ 可以下载到许多实用工具，或者你也可以使用 *rawrite* 命令将 *rescue.gz* 映像写入软盘。表 10-5 概述了一些增加你创建救援磁盘选项的实用工具。

在 *sunsite.unc.edu/pub/Linux/system/recovery/images/* 目录中，你可以找到 *cramdisk*——它在一个软盘上同时具备启动磁盘和 RAM 磁盘——提供对并口 Zip 驱动器、PPP、Lynx 和其他网络实用工具的救援支持。它们可以与至少具有 4MB 内存的主机配合工作。

改编一句老话，做系统管理员固然好，但做一个准备充分、拥有多种选择的系统管理员更好。

**表 10-5 创建救援磁盘的实用工具**

| 工具 | 文件 | 描述 |
| :--- | :--- | :--- |
| The Linux Bootkit | Bootkit-1.01.tar.gz | 用于创建和维护应急启动、根和用户磁盘的对话驱动包 |
| CatRescue | CatRescue101E.tgz | 应急启动软盘生成器 |
| Search and Rescue Set | SAR-2.25.tar.gz | 与你的内核一起使用以创建救援软盘 |
| Disk recovery tools for ext2fs | disc-recovery-utils-1.0.tgz | 第二扩展文件系统 (ext2fs) 的磁盘和 inode 恢复工具 |
| Fspace | f space.tgz | 一个静态链接的实用工具，告诉你有多少可用空间 |
| Genromfs | Genromfs-0.1.tar.gz | 创建仅 ROM 文件系统——适用于构建救援磁盘和启动磁盘 |
| Pico Rescue Disk | Pico.boot-0.95.tar.gz | 带有 pico 编辑器和其他工具的救援磁盘 |
| Rescue disk | Rescue02.zip | 可恢复磁带备份（使用 1.3.84 内核制作）的恢复磁盘 |
| Rescue boot/root disk | Resque_disk-2.0.22.tar.gz | 包含一些基本实用工具和文件系统类型 |
| Small Shell | sash.tar.z | 用于恢复脚本的小型静态链接 shell |
| Sbin utilities | sbin.tar.z | 静态链接的 /sbin 实用工具，因此你不需要动态库 |
| The ln utility | sln.tar.z | 静态链接的 ln 实用工具，因此你不需要动态库 |
| Tom’s Root/Boot Rescue disk | Tomsrtbt-1.4.68.tar.gz | 尽可能多地将 Linux 加载到 RAM 磁盘上 |
| Yard | yard-1.15.tar.gz | 用于创建自定义救援磁盘的 Perl 工具脚本 |
| Yard-prefabs | yard-prefabs-2.tgz | yard 的预制磁盘内容（目前仅包含 Slackware） |

