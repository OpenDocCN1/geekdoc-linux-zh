

# 理解 Unix • 第2章

第一块磁盘。`/dev/sda` 是整个磁盘的设备。它们被用于挂载文件系统。稍后会详细介绍。

## 挂载点（Mount points）：它们到底是什么？

我们已经多次提到文件系统和挂载。挂载点简单来说就是在文件层次结构中某处的一个空目录，通过它来访问内部磁盘分区、闪存器或外部硬盘。在 Windows 术语中，“c:\”可以被视为启动时识别的驱动器第一个分区的挂载点。虽然 Windows 驱动器的 ARC 名称是像 `multi(X):disk(Y)disk(Z)partition` 这种晦涩且糟糕的内容，但 Windows 好地将该硬件挂载到一个友好的挂载点 `c:\`，在命令行和 Windows 资源管理器中看起来更漂亮。同样，Windows 喜欢将第二个主盘挂载到 `d:\`，而不是用一长串难看的括号和数字来引用 CD-ROM 驱动器。*Unix 避免了驱动器字母，允许你灵活地将磁盘挂载到你喜欢的几乎任何目录名称下。这允许 `/var` 如果你喜欢的话拥有它自己的文件系统，如果日志填满了磁盘，也不会卡死你的系统。你可以专门分配一个分区给 `/home`，这样 Joe User 就不会因为从 bittor 下载大量电影而卡死系统。相反，他会填满 `/home` 挂载所在的磁盘。用户仍然会讨厌他，但至少运行守护进程（相当于 Windows 的“服务”）能够向它们的日志写入内容，电子邮件仍然可以送达。

Linux 将此磁盘设备到文件系统的目录名称的映射信息存储在所谓的“挂载表”（mount table）中。`mount` 命令允许你列出它，并且你可以手动控制 Linux 挂载了哪些设备：

```
ubuntu@ubuntu:~$ mount
proc /proc type proc (rw)
sysfs / /sys type sysfs (rw)
tmpfs / /lib/modules/2.6.22-14-generic/volatile type tmpfs (rw,mode=0755)
tmpfs / /lib/modules/2.6.22-14-generic/volatile type tmpfs (rw,mode=0755)
varrun /var/run type tmpfs (rw,noexec,nosuid,nodev,mode=0755)
varlock /var/lock type tmpfs (rw,noexec,nosuid,nodev,mode=1777)
udev /dev type tmpfs (rw,mode=0755)
devsm /dev/shm type tmpfs (rw)
devpts /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs /tmp type tmpfs (rw,nosuid,nodedev)
```

挂载表告诉你可以已挂载的设备、它被挂载的挂载点、它被解释的文件系统类型以及任何挂载选项，例如 `rw`（以读写权限挂载）。

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_39_0.png)

你可以以“ro”（只读）模式挂载磁盘；这可能在进行法医调查时你可能需要的（尽管对于确保连接了并行 ATA 磁盘的写线已物理断开，这种保证是无可比拟的）。详情请参阅挂载 页面，我们将通过一些示例来让你大胃口。

LiveCD 的一个优点是，你可以用它在 Windows 运行异常或在恶意软件感染时无法信任它时查看 Windows 磁盘事件。这样做的方法是挂载你的内部硬盘。在 *nix 中，由于默认安装了 `mount` 和 `finger` 等工具，你只需要学会使用这些东西。

要以只读模式挂载本地驱动器，你首先需要创建一个挂载点（空目录），然后我们尝试挂载它：

```
ubuntu@ubuntu~$ ls /dev/sd*
/dev/sda /dev/sda
```

```
ubuntu@ubuntu~$ mkdir /mnt/mywindrive
mdir: cannot create directory '/mnt/mywindrive': Permission denied
ubuntu@ubuntu~$ # 噢！凡人没有 /mnt 的写权限
ubuntu@ubuntu~$ sudo mkdir /mnt/mywindrive
```

```
ubuntu@ubuntu~$ ls /mnt
mywindrive
```

```
ubuntu@ubuntu~$ sudo mount -o ro -t auto /dev/sda1 /mnt/mywindrive
ubuntu@ubuntu~$ mount
proc on /proc type sysfs (rw)
sysfs on /sys type sysfs (rw)
tmpfs on /lib/modules/2.62.22-14-generic/volatile type tmpfs (rw,mode=0755)
tmpfs on /lib/modules/2.62.22-14-generic-volatile type tmpfs (rw,mode=0755)
varrun on /var/run type tmpfs (rw,noexec,nosuid,mode=0755)
varlock on /var/lock type tmpfs (rw,noexec,nosuid,mode=0777)
udev on /dev type tmpfs (rw,mode=0755)
devshm on /dev/shm type tmpfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /tmp type tmpfs (rw,nosuid,nodev)
/dev/sda1 /mnt/mywindrive type fuseblk(ro,nosuid,nodev,allow_other,blockSize=4096)
```

极有可能，如果你有一个相对“正常”的 Windows PC，且没有进行创意分区或安装到非默认磁盘，你的 Windows 分区可能名为 `/dev/sda`。在我们的示例中，我们列出了启动时 Linux 填充到 `/dev/sd*` 的所有内容以确保。不过，如果你看到 `/dev/sda1` 和 `/dev/sda2`，你可能有一台包含用于恢复的“服务分区” `/dev/sda1` 的 OEM 电脑。如果你正在使用不同的 Linux 且没有任何以 `sd` 开头的设备，那么 `/dev/sda` 可能是你找到内部硬盘第一个分区的地方。顺便说一下，除了 Linux 之外，硬件设备的命名完全不同，所以当你遇到它们时，你得靠手指去 Google 搜索相关信息。接下来，我们在 `/mnt` 中创建了一个包含目录的挂载点。在 `mount` 命令本身中，为了安全起见指定了只读选项，并允许挂载确定你分区的文件系统类型。“mount”命令的最后一行揭示了 `/dev/sda1 /mnt/mywindrive type fuseblk(ro,nosuid,nodev,allow_other,blockSize=4096)`。

在所有情况下，如果你有一个相对“正常”的 Windows PC，且没有进行创意分区或安装到非默认磁盘，你的 Windows 分区可能名为 `/dev/sda`。在我们的示例中，我们列出了启动时 Linux 填充到 `/dev/sd*` 的所有内容以确保。不过，如果你看到 `/dev/sda1` 和 `/dev/sda2`，你可能有一台包含用于恢复的“服务分区” `/dev/sda1` 的 OEM 电脑。如果你正在使用不同的 Linux 且没有任何以 `sd` 开头的设备，那么 `/dev/sda` 可能是你找到内部硬盘第一个分区的地方。顺便说一下，除了 Linux 之外，硬件设备的命名完全不同，所以当你遇到它们时，你得靠手指去 Google 搜索相关信息。接下来，我们在 `/mnt` 中创建了一个包含目录的挂载点。在 `mount` 命令本身中，为了安全起见指定了只读选项，并允许挂载确定你分区的文件系统类型。“mount”命令的最后一行揭示了 `/dev/sda /mnt/mywindrive type fuseblk(ro,nosuid,nodev,allow_other,blockSize=4096)`。

*(注：此处由于原文中存在部分重复，译文已根据“不要重复输出原文”的原则进行了去重处理，保持逻辑连贯)*

在所有情况下，如果你有一个相对“正常”的 Windows PC，且没有进行创意分区或安装到非默认磁盘，你的 Windows 分区可能名为 `/dev/sda`。

文件系统

```
AUTOEXEC.BAT      file.sys
boot.ini          Program Files
CONFIG.SYS        System Volume
drivers.dll       Documents and Settings
ntldr             WINDOWS
```

在 Windows 中，文件系统领域的生活非常简单。你只有两个磁盘文件系统需要担心（FAT 和 NTFS），并且每个系统都有几次迭代。FAT 这一派（你现在似乎只在移动驱动器上找到），FAT32 统治着根目录。我们怀念过去 FAT16 和它的 2-4GB 最大分区大小。FAT32 为我们提供了更大的卷空间，高达 2-8TB，但被 4GB 的文件大小限制了手肘。此外，所有的 FAT 变体都不支持文件权限概念，这使得它们对于企业来说不是一个选择。

NTFS 及其自 Windows NT 3.1 时代来的五个版本解决了权限问题，因为它对文件访问控制列表（ACL）有非常灵活的支持。NTFS 还为文件系统增加了日志功能，这使得 NTFS 文件系统对于电源中断或在未正常弹出的情况下拔掉外部硬盘导致的损坏更加健壮。因此，我们不需要像过去 Windows 95/98 那样经常运行 `scandsk` 或 `chkdsk`。对法医调查人员更有趣的是NTFS 包含了备用数据流（ADS），坏人可以在那里隐藏躲避敏锐眼睛的数据。

在 Linux 中，文件系统方面的情况变得更加复杂，因为它支持许多文件系统。Linux 支持的文件系统列表包括 FAT16、几种变体的 FAT32 以及几种变体的 NTFS。Linux 的原生文件系统是 ext2。

