
## 救援磁盘工具包

救援磁盘提供了一个故障排除环境。您可以根据需要和对 Linux 的了解执行简单或复杂的操作。当您在 `#` 提示符下输入 ls 时，您会看到一个熟悉的目录结构：

```
# ls
bin      etc      lost+found  proc     tmp
dev      lib      mnt         sbin     usr
```

更有趣的是 /bin 中列出的工具：

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

此环境中仅包含足够多的工具来执行许多修复和调整操作。请注意，所包含的编辑器是 Pico，即来自 Pine 邮件阅读器的迷你编辑器。其中一个关键实用程序是 e2fsck，它允许您尝试修复损坏的分区。

## 重建 LILO

让我们考虑一个常见问题。在双启动系统上，您使用全新重新安装或升级来升级 Windows 分区，而 LILO 消失了。这是因为 Windows 会覆盖 LILO 所在的 master boot record，即使它本身并不使用 MBR。

要重新安装 LILO，您需要知道哪个分区保存着您的 Linux 根文件系统。在下面的救援示例中，根文件系统位于 /dev/hda4 上：

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

有更简单的方法可以做到这一点（例如，使用启动软盘启动，以 root 身份登录并输入 lilo），但使用救援磁盘解决此问题是进行更严重紧急会话的良好练习。在这个简单示例中，我们将 Linux 文件系统挂载到 /mnt/image，然后 chroot 到 /mnt/image 使该目录成为我们的根目录。它还启动了一个 bash shell。从那里，简单地执行 /sbin/lilo 命令就会将 LILO 重新写入 MBR。

此技术也可用于修复另一个常见问题：构建新内核但忘记运行 /sbin/lilo 将新的引导信息写入 MBR。这种情况通常会阻止您完全启动 Linux，需要进行救援操作来恢复系统的使用。

## 重写配置文件

救援模式下可以轻松修复配置文件的简单错误配置。假设我们在编辑 /etc/fstab 时不小心输入了错误，导致无法进入系统。我们本打算在第一行写入 /dev/hda4 作为要挂载的关键分区，但键盘弹跳导致我们输入了 /dev/hda44 而未注意到，现在 Linux 无法启动。

返回救援模式，如前所述挂载 /dev/hda4，编辑 /etc/fstab 文件，保存它，然后重新启动，放心：

```
# mount -t ext2 /dev/hda4 /mnt/image
# pico -w /mnt/image/etc/fstab
# umount /mnt/image
```

## 修复分区

Linux 启动时，fsck 会尝试修复在完整性检查期间未干净启动的任何分区。这通常发生在非正常关机后，系统在关机程序完成之前就被断电，例如在停电期间或因意外关闭计算机而发生的非故意关机。

救援磁盘集可用于手动运行 e2fsck 以检查并尝试修复磁盘损坏。

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

修复严重损坏的文件系统可能需要您按顺序多次运行 e2fsck，直到所有问题清除。

## 紧急文件复制

如果硬盘损坏程度超出 e2fsck 完全修复的能力，但其中部分仍可访问，则可以使用救援磁盘集尝试复制重要文件。如果没有单独的 Linux 分区可挂载和复制，则可以使用软盘。以下是一个紧急文件复制过程的示例，其中软盘被格式化并使用 Linux 文件系统初始化，并将损坏硬盘上的选定配置文件复制到软盘：

```
# fdformat /dev/fd0H1440
# mke2fs /dev/fd0
mke2fs 1.14, 9-Jan-1999 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label=
360 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1 block group
8192 blocks per group, 8192 fragments per group
360 inodes per group

Writing inode tables: done
Writing superblocks and filesystem accounting information: done
# mount -t ext2 /dev/hda4 /mnt/image
# mount -t ext2 /dev/fd0 /mnt/floppy
# cd /mnt/floppy
# cp /mnt/image/etc/*.conf .
# cp /mnt/image/etc/conf.modules .
# ls
conf.modules inett.conf logrotate.conf nsswitch.conf resolv.conf
dosemu.conf isapnp.conf lost+found ntp.conf smb.conf
gpmroot.conf ld.so.conf mtools.conf pine.conf syslog.conf
host.conf lilo.conf named.conf pwdb.conf yp.conf
# cd /mnt
```

```
# umount floppy
# umount image
#
```

此过程可重复用于 passwd 文件、用户文件、httpd 文件——简而言之，任何仍可恢复的文件。可以初始化并挂载额外的软盘，对除大文件之外的所有文件重复该过程。

## 提示

尽管 Red Hat 救援磁盘集很有用，但它包含的工具不如一些也可以用于救援任务的“Linux on a floppy”发行版那么多。例如，Red Hat 救援集没有 vi 或 emacs 模拟器，也不支持 vfat 和 fat32 DOS/Windows 分区的文件。

一种非常流行的单盘 Linux 是 tomsrtbt，可在 http://www.toms.net/rb/ 获得。这种极其多功能的工具将惊人的数量的程序和设备驱动程序打包到单个压缩的 1.7Mb 3.5 英寸软盘上。以下来自 tomsrtbt 网站的列表显示了包含的程序和驱动程序：

## 3) 内容

Stuff（模块、manpages、脚本、二进制文件、内核）：

```
2.0.36 3c589_cs BusLogic CVF DEC_ELCP EEXPRESS EEXPRESS_PRO
EL2 EL3 EXT2 FAT FAT32 FD IDE IDECU IDEFL... IDETAPE ISQ9600 JOLIET LOOP MATH EMULATION MINIX MSDOS
NE2000 NFS PROC RAM SD SERIAL SLIP SMC SR TR ULTRA VFAT
VORTEX W0B3x aha152x_cs aha152x aha1542 aic7xxx ash awk
badblocks bdfblk bzip2 bzip2 cardbus cardmgr cat ce ce.help chatr
chgrp chmod chown chroot clear cmp cp cpio cut date dd ddate
debugfs df dirname dmseg dmesg dosfs ds du dump2fs util udevsck
eata echo egrep elvis emacs extend false fdflush fdformat
fdisk fdomain filesize find fmt fsck.ext2 fsck.msdos fsatab
grep gzip halt head hexedit hostname i82365 ifconfig ifport
ile init initatab insmod kill killall ksyms length less
libc.so.4.5.13 lilo lilo.conf in loadlin login losetup ls
lsattr mawk memtest mingetty mips mtr mkdir mkdosfs mk2fs
mkfifo mkfs.msdos mklist mknod mknod mknod mknod mount more
mt nv nc rcs... etc.
```

```
sort split stty swapoff swapon sync tail tar tcio telnet
test touch tune2fs umount update vi vi.help wc
```

磁盘甚至包含 man 页面。使用 tom'srtbt，您可以使用 DOS/Windows 分区（如果有的话）来复制文件，如果您是从严重损坏的 Linux 分区救援文件的话。这比将关键文件复制到软盘要高效得多，并且如果需要重新格式化 Linux 分区，它还提供了一个方便的位置来将文件复制回新的 Linux 设置中。这也是在 Linux 系统上维护一个适度大小的 DOS 分区的又一个原因。

## 提示

使用已启动的 tom'srtbt 进行文件救援任务如下所示：

```
# mkdir /mnt/image
# mkdir /mnt/dos
# mount -t ext2 /dev/hda4 /mnt/image
# mount -t vfat /dev/hda1 /mnt/dos
# mkdir /mnt/dos/rescuefiles
# cd /mnt/dos/rescuefiles
/mnt/dos/rescuefiles# cp /mnt/image/etc/*.conf .
/mnt/dos/rescuefiles# ls
dosemu.conf   isapnp.conf   mtools.conf   pine.conf     syslog.conf
gpm-root.conf ld.so.conf    named.conf    pwdb.conf     yp.conf
host.conf     lilo.conf     nsswitch.conf resolv.conf
inetd.conf    logrotate.conf ntp.conf      smb.conf
/mnt/dos/rescuefiles# cd /mnt
/mnt# umount dos ; umount image
/mnt#
```

与 Red Hat 救援会话相比，此会话在彩色显示器上以彩色显示文件，在提示符处显示路径名，并包含命令行历史记录。作为系统管理员，您会惊叹于 tom'srtbt 的多功能性，并会发现许多其他用途。将其保留在工具包中。您可以用它将几乎任何 Intel PC 变成一台即时、 albeit 有限的 Linux 计算机。
