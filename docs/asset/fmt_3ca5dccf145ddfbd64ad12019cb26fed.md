
[root@wallace images]# `dd if=rescue.img of=/dev/fd0`

2880+0 records in

2880+0 records out

你也可以从 DOS 创建救援磁盘。将格式化的 DOS 磁盘插入 DOS A: 驱动器并输入以下内容（如果你的 CD-ROM 驱动器不是 `E:`，请替换为你的 CD-ROM 驱动器字母）：

```
C:\>cd e:

E:\>cd dosutils

E:\DOSUTILS>rawrite

The image file is ..\images\rescue.img

The destination is a:
```

这会创建一个 Red Hat 救援磁盘。它设计为与 Red Hat 引导磁盘一起使用。如果你没有 Red Hat 引导磁盘，可以使用 Red Hat `mkbootdisk` 实用程序创建一个。

要查看是否具有 `mkbootdisk` 实用程序，请输入 `rpm -q mkbootdisk`。你还需要知道你的内核版本，它作为参数传递给 `mkbootdisk`。你可以使用 `uname -r` 确定它。再次插入一张新的 1.44Mb 3.5 英寸软盘并输入以下命令：

```
[root@wallace /root]# rpm -q mkbootdisk

mkbootdisk 1.2-2

[root@wallace /root]# fdformat /dev/fd0H1440

Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.

Formatting ... done

Verifying ... done

[root@wallace /root]# mount /dev/cdrom /mnt/cdrom

[root@wallace /root]# cd /mnt/cdrom/images

[root@wallace images]# uname -r

2.2.5-15

[root@wallace images]# mkbootdisk --device /dev/fd0 2.2.5-15

Insert a disk in /dev/fd0. Any information on the disk will be lost.

Press <Enter> to continue or ^C to abort:
```

## 启动救援会话

要启动救援会话，请插入你的 Red Hat 引导磁盘并启动系统。当 LILO 提示出现时输入 `rescue` 并按 Enter。当系统到达行 “VFS: Insert root floppy disk to be loaded into RAM disk and press ENTER” 时，插入你的 Red Hat 救援磁盘并按 Enter。

你将在屏幕上看到以下内容：

```
RAMDISK: Compressed image found at block 0

VFS: Mounted root (ext2 filesystem) readonly

change_root: old root has d_count=1

Trying to unmount old root ... okay

Freeing unused kernel memory: 60k freed

This is the Red Hat rescue disk. Most of the basic system commands are in /bin

Type exit to halt the system.

#
```

## 救援磁盘工具包

救援磁盘提供了一个故障排除环境。您可以根据需要和对 Linux 的了解执行简单或复杂的操作。当您在 `#` 提示符下输入 `ls` 时，您会看到一个熟悉的目录结构：

```
# ls

bin      etc      lost+found  proc     tmp

dev      lib      mnt         sbin     usr
```

更有趣的是 `/bin` 中列出的工具：

```
# cd /bin

# ls

ash      df       init      modprobe  rm       tac

badblocks e2fsck   insmod    mount     route    tail

cat      fdisk    ln        mt        rpm      tar

chmod    grep     ls        mv        sed      traceroute

chroot   gunzip   lsm       open      sh       umount

cp       gzip     mkdir     pico      swapoff

cpio     head     mke2fs    ping      swapon

dd       ifconfig mknod     ps        sync

#
```

此环境中仅包含足够多的工具来执行许多修复和调整操作。请注意，所包含的编辑器是 Pico，即来自 Pine 邮件阅读器的迷你编辑器。其中一个关键实用程序是 `e2fsck`，它允许您尝试修复损坏的分区。

## 重建 LILO

让我们考虑一个常见问题。在双启动系统上，您使用全新重新安装或升级来升级 Windows 分区，而 LILO 消失了。这是因为 Windows 会覆盖 LILO 所在的 master boot record，即使它本身并不使用 MBR。

要重新安装 LILO，您需要知道哪个分区保存着您的 Linux 根文件系统。在下面的救援示例中，根文件系统位于 `/dev/hda4` 上：

```
# mount -t ext2 /dev/hda4 /mnt/image

# chroot /mnt/image

bash# /sbin/lilo

Added linux *

Added dos

bash# exit
```

```
# cd /

# umount /mnt/image
```

有更简单的方法可以做到这一点（例如，使用启动软盘启动，以 root 身份登录并输入 `lilo`），但使用救援磁盘解决此问题是进行更严重紧急会话的良好练习。在这个简单示例中，我们将 Linux 文件系统挂载到 `/mnt/image`，然后 `chroot` 到 `/mnt/image` 使该目录成为我们的根目录。它还启动了一个 `bash` shell。从那里，简单地执行 `/sbin/lilo` 命令就会将 LILO 重新写入 MBR。

此技术也可用于修复另一个常见问题：构建新内核但忘记运行 `/sbin/lilo` 将新的引导信息写入 MBR。这种情况通常会阻止您完全启动 Linux，需要进行救援操作来恢复系统的使用。

## 重写配置文件

救援模式下可以轻松修复配置文件的简单错误配置。假设我们在编辑 `/etc/fstab` 时不小心输入了错误，导致无法进入系统。我们本打算在第一行写入 `/dev/hda4` 作为要挂载的关键分区，但键盘弹跳导致我们输入了 `/dev/hda44` 而未注意到，现在 Linux 无法启动。

返回救援模式，如前所述挂载 `/dev/hda4`，编辑 `/etc/fstab` 文件，保存它，然后重新启动，放心：

```
# mount -t ext2 /dev/hda4 /mnt/image

# pico -w /mnt/image/etc/fstab

# umount /mnt/image
```

## 修复分区

Linux 启动时，`fsck` 会尝试修复在完整性检查期间未干净启动的任何分区。这通常发生在非正常关机后，系统在关机程序完成之前就被断电，例如在停电期间或因意外关闭计算机而发生的非故意关机。

救援磁盘集可用于手动运行 `e2fsck` 以检查并尝试修复磁盘损坏。

```
# e2fsck -f /dev/hda4

e2fsck 1.14, 9-Jan-1999 for EXT2 FS 0.5b, 95/08/09

Pass 1: Checking inodes, blocks, and sizes

Pass 2: Checking directory structure

Pass 3: Checking directory connectivity
```

```
Pass 4: Checking reference counts

Pass 5: Checking group summary information

/dev/hda4: 68381/499712 files (0.7% noncontiguous), 1367942/1992060 blocks

#
```
