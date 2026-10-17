
| 风格 | 命令 |
| --- | --- |
| Debian | `apt-cache show package_name` |
| Red Hat | `yum info package_name` |

例如，要在 Debian 风格的系统上查看 `emacs` 包的描述，我们可以使用以下命令：

```
apt-cache show emacs
```

### 查找安装文件的包

要确定哪个包负责安装某个特定文件，我们可以使用表 14-12 中的命令。

表 14-12：包文件识别命令

| 风格 | 命令 |
| --- | --- |
| Debian | `dpkg -S file_name` |
| Red Hat | `rpm -qf file_name` |

要查看 Red Hat 系统上 `/usr/bin/vim` 文件是由哪个包安装的，我们可以使用以下命令：

```
rpm -qf /usr/bin/vim
```

### 小结

在接下来的章节中，我们将探索许多不同类型的程序，涵盖广泛的应用领域。虽然大多数这些程序通常默认已安装，但如果系统上尚未安装必要的程序，我们可能需要安装额外的包。有了我们新获得的知识和对包管理的认识，我们应该能够毫无问题地安装和管理所需的程序。

### Linux 软件安装的神话

从其他平台迁移过来的用户有时会陷入这样一个神话：认为在 Linux 下安装软件 somehow 很困难，并且不同发行版使用的各种打包方案是阻碍。嗯，这确实是阻碍，但只对那些想要分发仅二进制版本的秘密软件的专有软件厂商而言。

Linux 软件生态系统基于开源代码的理念。如果程序开发者发布了程序的源代码，那么很可能与某个发行版相关的人员会打包该程序并将其包含在其仓库中。这种方法确保程序能很好地集成到发行版中，并且用户可以享受“软件一站式购物”的便利，而不必为每个程序搜索其网站。最近，主要的专有平台厂商开始构建模仿这一想法的应用商店。

设备驱动程序的处理方式大致相同，只是它们不是发行版仓库中的独立条目，而是成为 Linux 内核的一部分。一般来说，在 Linux 中不存在“驱动盘”这种东西。内核要么支持某个设备，要么不支持，而 Linux 内核支持的设备非常多——事实上，比 Windows 支持的还要多。当然，如果你需要的特定设备不受支持，这就毫无安慰了。当这种情况发生时，你需要查看原因。缺乏驱动支持通常由以下三种原因之一造成。

- **设备太新了。** 由于许多硬件厂商并不积极支持 Linux 开发，因此编写内核驱动代码的工作就落在了 Linux 社区成员身上。这需要时间。

- **设备太冷门了。** 并非所有发行版都包含每一种可能的设备驱动。每个发行版都构建自己的内核，而由于内核是可配置的（这使得 Linux 能够运行在从手表到大型机等各种设备上），它们可能忽略了某个特定设备。通过定位并下载驱动的源代码，你（没错，就是你）可以自行编译并安装驱动。这个过程并不过于困难，但相当繁琐。我们将在后面的章节中讨论编译软件。

- **硬件厂商在隐瞒某些东西。** 它既没有发布 Linux 驱动的源代码，也没有发布技术文档供他人为其创建。这意味着硬件厂商试图将设备编程接口保密。由于我们不希望在电脑中存在秘密设备，最好避免此类产品。

`genisoimage` (`mkisofs`) 创建 ISO 9660 映像文件

`wodim` (`cdrecord`) 将数据写入光学存储介质

`md5sum` 计算 MD5 校验和

### 挂载和卸载存储设备

Linux 桌面的最新进展使得桌面用户对存储设备的管理变得极其简单。大多数情况下，我们将设备连接到系统，它就能“即插即用”。在旧时代（比如 2004 年），这些操作必须手动完成。在非桌面系统（即服务器）上，这仍然是一个主要的手工操作，因为服务器通常有极端的存储需求和复杂的配置要求。

管理存储设备的第一步是将设备附加到文件系统树中。这个过程称为挂载，允许设备与操作系统交互。正如我们在第 2 章中所回忆的那样，类 Unix 操作系统（如 Linux）维护着一棵单一的文件系统树，设备附加在各个点上。这与 Windows 等其他操作系统形成对比，后者为每个设备维护单独的文件系统树（例如 C:\、D:\ 等）。

一个名为 `/etc/fstab` 的文件（“file system table”的缩写）列出了在启动时要挂载的设备（通常是硬盘分区）。以下是早期 Fedora 系统的一个 `/etc/fstab` 文件示例：

| LABEL=/12 | / | ext4 | defaults | 1 | 1 |
| LABEL=/home | /home | ext4 | defaults | 1 | 2 |
| LABEL=/boot | /boot | ext4 | defaults | 1 | 2 |
| tmpfs | /dev/shm | tmpfs | defaults | 0 | 0 |
| devpts | /dev/pts | devpts | gid=5,mode=620 | 0 | 0 |
| sysfs | /sys | sysfs | defaults | 0 | 0 |
| proc | /proc | proc | defaults | 0 | 0 |
| LABEL=SWAP-sda3 | swap | swap | defaults | 0 | 0 |

这个示例文件中列出的大多数文件系统是虚拟的，与我们的讨论不适用。对我们而言，有趣的是前三个。

| LABEL=/12 | / | ext4 | defaults | 1 | 1 |
| LABEL=/home | /home | ext4 | defaults | 1 | 2 |

| 字段 | 内容 | 描述 |
|---|---|---|
| 5 | Frequency | 一个数字，用于指定是否以及何时使用 `dump` 命令备份文件系统。 |
| 6 | Order | 一个数字，用于指定应以何种顺序使用 `fsck` 命令检查文件系统。 |

### 查看已挂载文件系统列表

`mount` 命令用于挂载文件系统。不带参数输入该命令将显示当前已挂载的文件系统列表。

```
[me@linuxbox ~]$ mount
/dev/sda2 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda5 on /home type ext4 (rw)
/dev/sda1 on /boot type ext4 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
fusectl on /sys/fs/fuse/connections type fusectl (rw)
/dev/sdd1 on /media/disk type vfat (rw,nosuid,nodev,noatime,uhelper=hal,uid=500,utf8,shortname=lower)
twin4:/musicbox on /misc/musicbox type nfs4 (rw,addr=192.168.1.4)
```

列表的格式如下：`device on mount_point type filesystem_type (options)`。例如，第一行显示设备 `/dev/sda2` 已挂载为根文件系统，类型为 `ext4`，且可读可写（选项 `rw`）。该列表在底部还有两个有趣的条目。倒数第二个条目显示一个 2GB SD 存储卡在读卡器中挂载在 `/media/disk`，而最后一个条目是挂载在 `/misc/musicbox` 的网络驱动器。

在我们的第一个实验中，我们将使用 CD-ROM。首先，让我们查看在插入 CD-ROM 之前系统的状态。

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext4 (rw)
```

```
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda1 on /boot type ext4 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
```
