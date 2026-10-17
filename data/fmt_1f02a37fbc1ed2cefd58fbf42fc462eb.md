
### 1. 设备太新
由于许多硬件厂商并不积极支持 Linux 开发，因此编写内核驱动代码的工作就落在了 Linux 社区成员身上。这需要时间。

### 2. 设备太特殊
并非所有发行版都包含每一种可能的设备驱动。每个发行版都构建自己的内核，而由于内核非常可配置，这使得 Linux 能够运行在从手表到大型机等各种设备上，因此它们可能忽略了某个特定设备。通过定位并下载驱动的源代码，你可以自己编译并安装驱动。这个过程并不过于困难，但相当复杂。我们将在后面的章节中讨论编译软件。

### 3. 硬件厂商在隐瞒某些东西
他们既没有发布 Linux 驱动的源代码，也没有发布技术文档供他人为其创建。这意味着硬件厂商试图将设备编程接口保密。由于我们不希望在计算机中拥有秘密设备，我建议你移除有问题的硬件并将其扔进垃圾桶，与你的其他无用物品一起丢弃。

# 15 – 存储介质

在之前的章节中，我们研究了在文件级别操作数据。在本章中，我们将考虑设备级别的数据。Linux 在处理存储设备方面具有惊人的能力，无论是物理存储，例如硬盘，还是网络存储，或是 RAID（独立磁盘冗余阵列）和 LVM（逻辑卷管理器）等虚拟存储设备。

然而，由于这不是一本关于系统管理的书籍，我们不会尝试深入涵盖整个主题。我们将尝试做的是介绍一些用于管理存储设备的概念和关键命令。

为了完成本章中的练习，我们将使用一个 USB 闪存驱动器、一个 CD-RW 光盘（适用于配备 CD-ROM 刻录机的系统）和一个软盘（同样，如果系统配备了）。

我们将研究以下命令：

- `mount` – 挂载文件系统
- `umount` – 卸载文件系统
- `fsck` – 检查和修复文件系统
- `fdisk` – 分区表操作工具
- `mkfs` – 创建文件系统
- `fdformat` – 格式化软盘
- `dd` – 直接向设备写入块导向数据
- `genisoimage` (`mkisofs`) – 创建 ISO 9660 映像文件
- `wodim` (`cdrecord`) – 向光学存储介质写入数据
- `md5sum` – 计算 MD5 校验和

## 挂载和卸载存储设备

Linux 桌面最近的进步使得存储设备管理对桌面用户来说变得极其简单。在大多数情况下，我们将设备连接到系统，它就能“即插即用”。在旧时代（比如 2004 年），这些东西必须手动完成。在非桌面系统（即服务器）上，这仍然是一个主要的手工过程，因为服务器通常有极端的存储需求和复杂的配置要求。

管理存储设备的第一步是将设备连接到文件系统树。这个过程称为挂载，它允许设备参与操作系统。正如我们在第 2 章中回忆的那样，像 Linux 这样的类 Unix 操作系统维护一个单一的文件系统树，设备附加在各个点上。这与 MS-DOS 和 Windows 等其他操作系统形成对比，后者为每个设备维护单独的文件系统树（例如 C:\、D:\ 等）。

文件 `/etc/fstab` 列出了要在启动时挂载的设备（通常是硬盘分区）。以下是来自 Fedora 7 系统的示例 `/etc/fstab` 文件：

| LABEL=/12 | / | ext3 | defaults | 1 | 1 |
| LABEL=/home | /home | ext3 | defaults | 1 | 2 |
| LABEL=/boot | /boot | ext3 | defaults | 1 | 2 |
| tmpfs | /dev/shm | tmpfs | defaults | 0 | 0 |
| devpts | /dev/pts | devpts | gid=5,mode=620 | 0 | 0 |
| sysfs | /sys | sysfs |  | 0 | 0 |
| proc | /proc | proc | defaults | 0 | 0 |
| LABEL=SWAP-sda3 | swap | swap | defaults | 0 | 0 |

在此示例文件中列出的大多数文件系统是虚拟的，与我们的讨论不适用。对我们而言，有趣的是前三个：

| LABEL=/12 | / | ext3 | defaults | 1 | 1 |
| LABEL=/home | /home | ext3 | defaults | 1 | 2 |
| LABEL=/boot | /boot | ext3 | defaults | 1 | 2 |

这些是硬盘分区。文件的每一行由六个字段组成，如下所示：

### 表 15-1：/etc/fstab 字段

| 字段 | 内容 | 描述 |
|---|---|---|
| 1 | 设备 | 传统上，此字段包含与物理设备关联的设备文件的实际名称，例如 `/dev/hda1`（第一个 IDE 通道上主设备的第一个分区）。但在今天的计算机中，有许多热插拔设备（如 USB 驱动器），许多现代 Linux 发行版将设备与文本标签关联。此标签（在存储介质格式化时添加到存储介质上）由操作系统在设备连接到系统时读取。这样，无论将哪个设备文件分配给实际物理设备，它仍能被正确识别。 |
| 2 | 挂载点 | 设备附加到文件系统树的目录。 |
| 3 | 文件系统类型 | Linux 允许挂载许多文件系统类型。大多数原生 Linux 文件系统是 ext3，但还支持许多其他类型，例如 FAT16 (`msdos`)、FAT32 (`vfat`)、NTFS (`ntfs`)、CD-ROM (`iso9660`) 等。 |
| 4 | 选项 | 文件系统可以带各种选项挂载。例如，可以将文件系统挂载为只读，或防止任何程序从中执行（这是可移动介质的有用安全功能）。 |
| 5 | 频率 | 一个指定是否以及何时使用 `dump` 命令备份文件系统的数字。 |
| 6 | 顺序 | 一个指定应以何种顺序使用 `fsck` 命令检查文件系统的数字。 |

### 查看已挂载文件系统列表

`mount` 命令用于挂载文件系统。不带参数输入该命令将显示当前已挂载的文件系统列表：

```
[me@linuxbox ~]$ mount
/dev/sda2 on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda5 on /home type ext3 (rw)
/dev/sda1 on /boot type ext3 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
fusectl on /sys/fs/fuse/connections type fusectl (rw)
/dev/sdd1 on /media/disk type vfat (rw,nosuid,nodev,noatime,
uhelper=hal,uid=500,utf8,shortname=lower)
twin4:/musicbox on /misc/musicbox type nfs4 (rw,addr=192.168.1.4)
```

该列表的格式为：device on mount_point type file_system_type (options)。例如，第一行显示设备 `/dev/sda2` 被挂载为根文件系统，类型为 ext3，且可读可写（选项“rw”）。此列表在底部还有两个有趣的条目。倒数第二个条目显示一个 2 GB 的 SD 内存卡在读卡器中挂载于 `/media/disk`，而最后一个条目是一个网络工作驱动器挂载于 `/misc/musicbox`。

对于我们的第一个实验，我们将使用 CD-ROM。首先，让我们看一下在插入 CD-ROM 之前系统的状态：

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/hda1 on /boot type ext3 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
```

此列表来自 CentOS 5 系统，该系统使用 LVM（逻辑卷管理器）创建其根文件系统。与许多现代 Linux 发行版一样，此系统在插入后会尝试自动挂载 CD-ROM。插入光盘后，我们看到以下内容：
