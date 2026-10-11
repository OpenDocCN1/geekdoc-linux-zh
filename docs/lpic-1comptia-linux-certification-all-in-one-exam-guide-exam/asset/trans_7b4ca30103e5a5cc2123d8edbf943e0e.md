

## 快速复习

- 在将磁盘挂载到 Linux 文件系统之前，必须对磁盘进行分区和格式化。
- fdisk 实用程序用于对磁盘进行分区。
- 在对磁盘进行分区时，必须设置分区类型。
- 分区更改仅保存在内存中，直到将其提交到磁盘。
- 对磁盘进行分区后，需要使用 mkfs 或 mke2fs 对其进行格式化。
- 对磁盘进行格式化后，可以使用 mount 命令将其挂载。
- 可以使用 /etc/mtab 文件查看已挂载的文件系统。
- 也可以使用 /proc/mounts 查看已挂载的文件系统。
- 可以使用 umount 命令卸载已挂载的文件系统。
- 在关闭 Linux 之前，必须卸载所有文件系统。
- 除非在 /etc/fstab 文件中有条目，否则重启时不会重新挂载已挂载的文件系统。
- /etc/fstab 文件指定了特定设备的挂载点和其他选项。
- 可以使用 df 和 du 实用程序监控磁盘空间和使用率。
- fsck 实用程序用于检查和修复文件系统。
- e2fsck 可用于恢复 ext2/3/4 文件系统中损坏的超级块。
- tune2fs 实用程序用于调整 ext2/3/4 文件系统中的各种文件系统参数。
- reiserfstune 实用程序是 tune2fs 实用程序的 Reiser 等效工具。
- dumpe2fs 实用程序可以显示有关 ext2/3/4 文件系统的许多有用信息。
- debugfs 实用程序是一个交互式文件系统调试器。
- xfs_admin 实用程序是 tune2fs 的 xfs 等效工具。
- xfs_info 实用程序显示有关 xfs 文件系统有用信息。
- xfs_metadump 实用程序将 xfs 文件系统元数据（如文件名和大小）转储到文件。
- 你可以在 shell 提示符下使用 lsof 命令显示打开文件列表。
- fuser 命令显示使用指定文件或文件系统的进程的 PID。
- 可移动设备必须先挂载到 Linux 文件系统才能被访问。
- mount 命令可用于挂载软盘。
- 软盘通常使用 vfat 文件系统类型。
- 系统中的第一个软盘是 /dev/fd0。
- 可以使用 /etc/fstab 自动挂载软盘。
- 在从系统中移除软盘之前，必须使用 umount 将其卸载。
- 光盘必须先挂载到文件系统中才能被访问。
- 光盘使用 iso9660 文件系统类型挂载。
- 光盘通常挂载在 /media/cdrom、/media/cdrecorder、/media/dvd 或 /mnt/cdrom。
- Linux 将 USB 和 FireWire 设备视为 SCSI 设备。
- USB 和 FireWire 设备使用 mount 进行挂载。
- 如果你不知道 USB 或 FireWire 设备上使用的文件系统类型，可以使用 -t auto 让 mount 尝试确定正确的文件系统类型。
- 定期备份系统是绝对至关重要的。
- 磁带驱动器通常用于备份数据。
- 磁带驱动器可以存储大量数据，且相对便宜。
- 磁带驱动器速度较慢，且容易磨损。
- 可重写 CD 和 DVD 可用于备份，但它们真的无法容纳足够的信息。
- 可移动硬盘正在成为一种流行的备份方案。
- 可移动硬盘速度非常快且能存储大量数据；然而，它们也容易受到与被备份硬盘相同的数据损坏问题的影响。
- 完全备份会备份所有文件，并将文件标记为已备份。
- 增量备份会备份自上次完全备份或增量备份以来所有已修改的文件，并将文件标记为已备份。
- 差异备份会备份自上次完全备份以来所有已修改的文件。它不会将文件标记为已备份。
- 你可以将完全备份与增量或差异备份混合使用，但不能混合使用增量和差异备份。
- 你应该保留三到四周的备份轮换。
- 你应该验证你的备份。
- 你应该为你的备份设定时间表。
- 你应该仔细确定要备份哪些目录。
- 你应该考虑备份 /etc、/home、/opt、/root、/var 和 /srv。
- 你可以使用 tar 创建备份文件。
- tar 实用程序适用于大多数备份介质。
- 你也可以使用 cpio 来归档数据。
- 你可以使用 dd 命令来转换和复制文件。
- dd 实用程序可以将整个分区甚至整个硬盘复制到单个文件。

## 问题

1. 你需要使用 fdisk 为系统中的第四个 SATA 硬盘创建分区。以下哪个是正确的命令？
   - A. `fdisk /dev/hdd`
   - B. `fdisk /dev/sdcd`
   - C. `fdisk /dev/sda4`
   - D. `fdisk /dev/sdb2`

2. 你使用 fdisk 在 Linux 系统的第二个硬盘上创建了一个新分区。你希望将该分区用作系统的第二个交换分区。你需要将其更改为哪种分区类型？
   - A. 83
   - B. 82
   - C. 85
   - D. 1
   - E. 你不能在同一系统上使用两个交换分区。

3. 你需要使用 ext3 文件系统格式化次级 IDE 通道从驱上的第一个分区。以下哪个是正确的命令？
   - A. `mke2fs /dev/sdd1`
   - B. `mkfs -t ext3 /dev/sdd1`
   - C. `mkfs -t ext3 /dev/sda4`
   - D. `mkreiserfs -t ext3 /dev/sdd1`

4. 在 ext4 文件系统中，分区超级块的第一份冗余副本默认存储在第几个块？
   - A. 0
   - B. 32768
   - C. 98304
   - D. 163840

5. 你使用 fdisk 实用程序创建了一个新的交换分区（`/dev/sdb1`）。你需要格式化和启用该分区。应该使用哪些命令来执行此操作？（选择两项。）
   - A. `mkswap /dev/sdb1`
   - B. `mkfs -t swap /dev/sdb1`
   - C. `swapon /dev/sdb1`
   - D. `swapon -a`
   - E. `mkfs -t vfat /dev/sdb1`
   - F. `swapon --enable /dev/sdb1`

6. 你在系统第二个硬盘的第一个分区上创建了一个 ext4 文件系统，现在需要在 /mnt/extra space 中以读写模式挂载它。哪些命令可以实现此操作？（选择两项。）
   - A. `mount -t ext4 /dev/sda1 /mnt/extra\ space/`
   - B. `mount -t ext4 /dev/sdb1 /mnt/extra\ space/`
   - C. `mount -a /dev/sdb1 /mnt/extra\ space/`
   - D. `mount -t ext4 /dev/sdb1 /mnt/extra\ space/`
   - E. `mount -t ext4 -o ro /dev/sdb1 /mnt/extra\ space/`

7. 你的主目录中有一个名为 disc image.iso 的 ISO 映像文件，你想将其挂载到 Linux 文件系统的 /mnt 目录中，以便从中提取几个文件。哪个命令可以实现此操作？
   - A. `mount ~/disc\ image.\ iso /mnt`
   - B. `mount -a ~/disc\ image.\ iso /mnt`
   - C. `mount -t iso9660 ~/disc\ image.\ iso /mnt`
   - D. `mount -o loop ~/disc\ image.\ iso /mnt`

8. 你已经将 /dev/sdb1 分区挂载在 /mnt 目录中，现在需要卸载它。哪些命令可以实现此操作？（选择两项。）
   - A. `umount /mnt`
   - B. `unmount /mnt`
   - C. `umount /dev/sdb1`
   - D. `mount --unmount /dev/sdb1`
   - E. `unmount /dev/sdb1`

9. 哪个文件用于在系统初始启动时自动挂载文件系统？
   - A. `/etc/mtab`
   - B. `/proc/mounts`
   - C. `/etc/inittab`
   - D. `/etc/fstab`

10. 哪个 fstab 挂载选项会导致挂起的磁盘写入立即提交？
    - A. `async`
    - B. `sync`
    - C. `rw`
    - D. `auto`
    - E. `exec`

11. 哪个命令将为你提供 `/dev/sda2` 分区上 inode 消耗的摘要？
    - A. `df -i`
    - B. `df -h`
    - C. `df -hT`
    - D. `du -inode`
    - E. `df /dev/sda2`

12. 你的 Linux 系统上的 `/dev/sda1` 分区当前没有卷标签。已知它是一个 ext4 分区，哪个命令将把标签设置为“DATA”？
    - A. `dump2fs -L DATA /dev/sda1`
    - B. `tune2fs -L DATA /dev/sda1`
    - C. `lsOF /dev/sda1 --label "DATA"`
    - D. `mkfs -t ext4 -L "DATA" /dev/sda1`

13. 你担心包含一个重度使用的 ext3 磁盘分区（`/dev/sda2`）的硬盘状况。为了确保数据完整性，你想增加自动 fsck 检查的频率。你应该使用哪个实用程序来配置此设置？
    - A. `dump2fs`
    - B. `debugfs`
    - C. `e2fsck`
    - D. `fsck`
    - E. `tune2fs`

14. 你需要在 `/media/dvd` 中挂载光盘。哪个命令可以实现此操作？
    - A. `mount -t iso9660 /dev/cdrom /media/dvd`
    - B. `mount -t dvd /dev/cdrom /media/dvd`
    - C. `dvdmount -t iso9660 /dev/cdrom /media/dvd`
    - D. `mount -t iso9660 /dev/cdrom ~/dvd`

15. 你注意到你的 Linux 服务器上安装了一个流氓可执行文件，并且它目前正在运行。你需要：1) 识别使用该文件的进程以便杀死它，以及 2) 确定用于运行它的用户账户。你应该使用哪些 fuser 命令选项来执行此操作？（选择两项。）
    - A. `--a`
    - B. `--k`
    - C. `--i`
    - D. `--u`
    - E. `--p`

