
- 磁盘设备由`/dev`目录表示。每个设备指定了数据传输类型、内核中的主号和次号。每个磁盘必须包含一个文件系统，然后通过`mount`命令挂载到 Linux 树中。

- `mount`命令。文件系统随后可以使用`umount`命令卸载。在创建文件系统之前，必须对磁盘进行分区。

- Linux 有许多文件系统，每种都有特定的用途。大多数可移动媒体设备被 Linux 系统识别为 SCSI 设备并在 GUI 环境中挂载。
- 使用`df`、`du`和`dump2fs`命令监控磁盘使用情况以避免空间不足。同样，使用`fsck`命令及其变体检查磁盘错误。
- 如果磁盘空间有限，可以使用磁盘配额来限制用户在文件系统上的空间。

### 关键术语

`/dev`目录
`/etc/fstab`
`/etc/mtab`
`/proc/devices`
坏块
`blkid`命令
块
块设备
`cdfisk`命令
字符设备
柱面
设备文件
`df` (disk free)命令
磁盘配额
`du` (directory usage)命令
`e22label`命令
`edquota`命令
`eject`命令
`fatlabel`命令
`fatlabel`命令
`fdisk`命令
文件系统

文件系统损坏
格式化
`fsck` (filesystem check)命令
`fuser`命令
`gdisk` (GPT fdisk)命令
硬限制
日志记录
逻辑卷 (LV)
逻辑卷管理器 (LVM)
`lsblk`命令
`lvsbm`命令
`lvcreate`命令
`vldisplay`命令
`lxtend`命令
`lvscan`命令
主号
次号
`mkfs` (make filesystem)命令
`mkmissoff`命令
`mknod`命令
`mkswap`命令

`mount`命令
挂载点
挂载
`parted` (GNU Parted)命令
分区
`partprobe`命令
物理分区 (PE)大小
物理卷 (PVs)
伪文件系统
`pvcreate`命令
`pvdisplay`命令
`pscan`命令
`quota`命令
`quotaoff`命令
`repquota`命令
`resize2fs`命令
根文件系统
扇区
软限制
`swoff`命令
`swapon`命令

## 第 5 章 Linux 文件系统管理

- 同步跟踪 (syncing track)
- `tune2fs`命令
- `dedev`守护进程
- `umount`命令
- 通用标识符 (UUID)
- `vgcreate`命令
- `vgdisplay`命令
- `vgxtend`命令
- `vgscan`命令
- 虚拟文件系统
- 卷组 (VG)
- `xfs_admin`命令
- `xfs_db`命令
- `xfs_fsr`命令
- `xfs_growfs`命令
- `xfs_info`命令
- `xfs_quota`命令
- `xfs_repair`命令

### 复习题

1. 下列命令只能用于在 GPT 硬盘上创建分区？
   a. `gdisk`
   b. `cfdisk`
   c. `fdisk`
   d. `parted`

2. Jim 刚刚在他的系统中安装了两个新的 SAS SSD。他已在正确安装了硬件。在使用这些设备进行数据存储和检索之前，他必须做什么？（选择所有适用项）
   a. 挂载这两个 SSD 以便操作系统访问。
   b. 在每个 SSD 上挂载文件系统。
   c. 在每个 SSD 上创建一个或多个分区。
   d. 使用 `vi` 编辑器编辑 `/etc/mtab` 并为它们创建条目。
   e. 挂载在两个 SSD 上创建的任何分区，以便操作系统访问。
   f. 将 SSD 上创建的任何分区格式化为 Linux 识别的有效文件系统。

3. 硬盘上的分区用文件系统格式化后，该硬盘上的所有分区必须使用相同的文件系统。对或错？

4. 你想查看系统中正在被使用的文件。哪个命令可以帮助你？（选择所有适用项）
   a. `cat /etc/fstab`
   b. `df -T`
   c. `cat /etc/mtab`
   d. `ls /sys/block`

5. 给 `/etc/fstab` 的输出，哪些文件系统将在启动时由 `fsck` 自动检查？

| 设备 | 挂载点 | 类型 | 选项 | Pass | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/sda` | `/` | ext4 | defaults | 1 | 1 |
| none | `/dev/pts` | devpts | gid=5,mode=620 | 1 | 0 |
| none | `/proc` | | defaults | 0 | 1 |
| none | `/dev/shm` | tmpfs | defaults | 1 | 0 |
| `/dev/sd2` | swap | | defaults | 0 | 1 |
| `/dev/dvd` | `/media/dev` | iso9660 | noauto,ro | 0 | 0 |

   a. 无，因为 `fsck` 必须手动为每个文件系统运行
   b. `/`, `/dev/pts` 和 `/dev/shm`
   c. `/`, `/proc` 和 swap
   d. 所有，因为 `fsck` 在启动时自动为所有文件系统运行

6. 用户将一个设备挂载到挂载点目录，随后发现需要之前在挂载目录中找到的文件。该用户应该做什么？
   a. 什么都不做；文件已丢失且永远无法访问。
   b. 什么都不做；文件可能不在那里，因为你只能挂载到空目录。
   c. 从目录中卸载设备。
   d. 运行 `fsck` 命令来恢复文件。
   e. 在 `lost+found` 目录中查找文件。

7. 哪个命令用于显示文件系统上的可用空间？
   a. `fsck`
   b. `quota`
   c. `du`
   d. `df`

8. 为了在文件系统上成功运行 `fsck` 命令，你必须做什么？
   a. 使用 `-u` 运行 `fsck` 命令先自动卸载文件系统。
   b. 当警告在挂载的文件系统上运行 `fsck` 可能会导致损坏时选择继续。
   c. 卸载文件系统。
   d. 确保文件系统已挂载。

9. 字符设备传输数据的速度通常比块设备快。对或错？

10. `-s /var` 命令的作用是什么？
    a. 显示连接到 `/var` 目录的用户
    b. 显示 `/var` 目录下所有目录的大小
    c. 倾储 `/var` 目录
    d. 显示 `/var` 目录的总大小

11. 命令 `dumpefs -h` 的作用是什么？
    a. 备份 ext2 文件系统
    b. 显示 ext2/ext3/ext4 文件系统使用的和可用的 inode 数量
    c. 倾储 ext2 文件系统
    d. 无；它不是有效命令

12. 哪个命令可以修复 XFS 文件系统？
    a. `fsck -t fs /dev/sdb1`
    b. `e2fsck /dev/sdb1`
    c. `fsck.xfs /dev/sdb1`
    d. `xfs_repair /dev/sdb1`

13. 下列哪些陈正确的？（选择所有适用项）
    a. 配额只能限制用户空间。
    b. 配额只能限制用户可以拥有的文件数量
    c. 配额可以同时限制用户空间和用户可以拥有的文件数量
    d. 硬限制永远不会被超过。
    e. 硬限制允许用户在一段时间内超过它。
    f. 软限制允许用户在一段时间内超过它。
    g. 可以设置硬限制或软限制，但不能完全设置。

14. 设备文件（选择所有适用项）
    a. 没有 section（部分）
    b. 没有 data section
    c. 显示主号和次号
    d. 固定大小为 300 千字节

15. 关于 LVM 的以下哪个陈述正确？
    a. PV 是 VG 的集合。
    b. LV 是从 PV 内空闲空间创建的。
    c. VG 由一个或多个 PV 组成。
    d. PV 使用 LV 内的空间创建。

16. `lvextend` 命令可以向现有逻辑卷添加未使用的空间。对或错？

17. 你将 USB 闪存插入到带有两个硬盘的系统中。Linux 如何识别该 USB 闪存？
    a. `/dev/sda1`
    b. `/dev/sda2`
    c. `/dev/sdb1`
    d. `/dev/sdc1`

18. 哪个命令挂载 `/etc/fstab` 中的所有文件系统？
    a. `mount -f`
    b. `mount /etc/fstab`
    c. `mount /etc/mtab`

19. 用户在显示损坏的 ext4 文件系统上带有 `-f` 选项运行 `fsck` 命令。如何定位系统无法修复的文件？
    a. 查看文件系统的根目录。
    b. 当遇到无法修复的文件时，系统会提示用户位置。
    c. 查看挂载点下的 `lost+found` 目录。

20. 哪个命令用于格式化带有 ext4 文件系统的硬盘分区？
    a. `format -ext4`
    b. `ext4mkfs`
    c. `e2mkfs -t ext4`
    d. `makeext4`

### 实验

这些实验应该按照给顺序完成。本章的实验总共需要三小时。实验要求包括：
- 一安装了 Fedora 28 的计算机

### 实验 5-1 在此实验中查看并创建设备文件。

1. 启动你的 Linux 虚拟机。Linux 系统加载后，按 `Ctrl+Alt+F5` 切换到终端 (tty5)。使用用户 root 和密码 `LINUXrocks` 登录。
2. 在命令行提示符下输入 `ls -l /dev/tty6` 并按回车 `getdev/tty6` 代表什么？它是块设备还是字符设备？它的主号和次号是多少？
3. 在命令行提示符下输入 `rm -f /dev/tty6` 并按回车。接下来在命令行提示符下输入 `ls -l /dev/tty6`。文件是否成功删除？
4. 按 `Ctrl+Alt+F6` 切换到 tty6，使用用户 root 和密码 `LINUXrocks` 尝试登录。成功了吗？
5. 按 `Ctrl+Alt+F5` 切换回 tty5，在命令行提示符下输入命令 `mknod /dev/tty6 c 4 6` 并按回车。这做了什么？接下来输入 `ls -l /dev/tty6`。文件是否成功重新创建？
6. 按 `Ctrl+Alt+F6` 切换回 tty6，使用用户 root 和密码 `LINUXrocks` 登录。为什么你成功了？
7. 在命令行提示符下输入 `find /dev /dev` 并按回车列出 `/dev` 目录下所有的文件名。文件多吗？这些文件有什么共同之处？每个文件的主号不同吗？每个文件的次号不同吗？
8. 在命令行提示符下输入 `less /proc/devices` 并按回车。系统中哪些设备存在主号和次号？接下来在命令行提示符下输入 `du -s /dev` 并按回车。`/dev` 目录下的所有文件有多大？为什么？
9. 在命令行提示符下输入 `less /proc/devices` 并按回车。哪些设备的主号为 47？这与你在步骤2中观察到的结果如何？完成后按 `q` 退出 `less` 工具。
10. 输入 `exit` 并按回车退出 shell。

### 实验 5-2 在此实验中，你正在挂载一个移动 DVD。

1. 按 `Ctrl+Alt+F1` 切换到图形终端 (tty1)，使用你的用户账户和密码 `LINUXrocks` 登录 GNOME 桌面！
2. 在你的虚拟化软件中，将 Fedora Linux 的 DVD ISO (`Fedora-Workstation-x86_64-28-1.iso`) 附加虚拟机的 DVD 光。完成此操作后，查看你的文件应用程序。左侧面板是否有代表你的 Fedora 桌面 DVD 的图标？将鼠标悬停在该图标上查看挂载点。你的 DVD 自动挂载到了哪个目录？花几分钟在文件应用程序中探索 DVD 的内容。完成后，关闭应用程序。
3. 按 `Ctrl+Alt+F5` 切换到命令行终端 (tty5)。使用用户名 root 和密码 `LINUXrocks` 登录终端！
4. 在命令行提示符下输入 `du -hT` 并按回车。你的 Fedora DVD 仍然挂载吗？使用了什么文件系统？接下来输入 `ls -l /dev/cdrom` 并按回车。`/dev/cdrom` 是指向该设备的符号链接吗？
5. 在命令行提示符下输入 `umount /dev/cdrom` 并按回车以卸载你的 Fedora DVD。接下来输入 `du -hT` 并按回车验证它已不再挂载。

## 第 5 章 Linux 文件系统管理 `/mnt` 并按回车

- 在命令提示符下，输入 `cp /etc/hosts` 并按回车。接下来，输入 `ls /mnt` 并按回车以验证 `/etc/hosts` 是否已成功复制到 `/mnt` 目录。

- 在命令提示符下，输入 `mount /dev/cdrom /mnt` 并按回车。你收到了什么警告？输入 `du -hT` 并按回车验证你的 Fedora DVD 是否已挂载到 `/mnt` 目录。

- 在命令提示符下，输入 `mount /mnt` 并按回车查看输出。接下来，输入 `cat /etc/mtab` 并按回车。这些命令显示的输出是否比第 7 步更详细？

- 在命令提示符下，输入 `cd /mnt` 并按回车。接下来，输入 `ls -F` 并按回车。DVD 的内容与第 2 步相同吗？

- 在命令提示符下，输入 `mount /mnt` 并按回车。你收到了什么错误？接下来，输入 `fuser -u /mnt` 并按回车。注意你当前正在使用 `/mnt` 目录，这阻止了卸载。

- 在命令提示符下，输入 `cd` 并按回车返回主目录，然后输入 `umount /mnt` 并按回车卸载你的 Fedora DVD。

- 在命令提示符下，输入 `ls /mnt` 并按回车。在 Fedora DVD 卸载后，`/etc/hosts` 的副本是否可用？

- 输入 `exit` 并按回车退出你的 shell。

## 项目 5-3

在这个实操项目中，你将处理标准硬分区（hard partitions）。首先，你将使用 `fdisk` 工具创建一个硬盘分区。接下来，你将创建一个 ext4 分区并将其挂载到目录树中。最后，你将使用 `/etc/fstab` 在启动时自动挂载该分区。

- 1. 按 `Ctrl+Alt+F5` 切换到命令行终端 (tty5)，并使用用户名 `root` 和密码 `LINUXrocks!` 登录终端。

- 2. 在命令提示符下，输入 `fdisk /dev/sda` 并按回车。哪个块设备持有你在 Fedora 安装期间创建的分区？同时注意该块设备下有三个分区：第一个分区挂载到 `/boot` 目录，第二个分区用作 Linux 交换分区（swap），第三个分区挂载到 `/directory`。

- 3. 在命令提示符下，输入 `fdisk /dev/sda` 并按回车。在 `fdisk` 提示符下输入 `m` 并按回车查看 `fdisk` 命令。

- 4. 在 `fdisk` 提示符下，输入 `p` 并按回车查看硬盘上的分区表。这些分区与第 2 步的输出匹配吗？

- 5. 在 `fdisk` 提示符下，输入 `n` 并按回车创建一个新分区。接下来，输入 `e` 选择扩展分区，观察括号内的有效范围并按回车选择默认值（第一个可用扇区）。当提示输入结束柱体（end cylinder）时，观察括号内的有效范围并按回车选择默认值（最后一个可用扇区）。

- 在 `fdisk` 提示符下，输入 `p` 并按回车查看硬盘上的分区表。存在多少个分区？`/dev/sda4` 是什么类型的分区？

- 6. 在 `fdisk` 提示符下，输入 `n` 并按回车创建一个新分区。注意，由于所有主分区已用且已存在扩展分区，系统会自动选择逻辑驱动作为分区类型。当提示起始扇区（start sector）时，观察括号内的有效范围并按回车选择默认值（第一个可用扇区）。当提示结束柱体时，输入 `+1GB` 并按回车。

- 7. 在 `fdisk` 提示符下，输入 `p` 并按回车查看硬盘上的分区表。存在多少个分区？`/dev/sda5` 是什么类型的分区？

- 8. 在 `fdisk` 提示符下，输入 `1` 并按回车查看不同的分区类型。Linux swap 使用什么类型？在 `fdisk` 提示符下输入什么字符可以更改分区类型？

- 9. 在 `fdisk` 提示符下，输入 `w` 并按回车保存更改保存硬盘并退出 `fdisk` 工具。

- 10. 在命令提示符下，输入 `reboot` 并按回车重启，确保分区表已正确读入内存。系统加载后，按 `Ctrl+Alt+F5` 切换到命令行终端 (tty5)，并使用用户名 `root` 和密码 `LINUXrocks!` 登录终端。

- 11. 在命令提示符下，输入 `mkfs -t ext4 /dev/sda5` 并按回车，用 ext4 文件系统格式化硬盘上的第一个逻辑驱动。

- 12. 在命令提示符下，输入 `mkdir /newmount` 并按回车，在 `/` 下创建一个挂载点目录，用于挂载第一个硬盘上的第三个分区。

- 13. 在命令提示符下，输入 `mount -t ext4 /dev/sda5 /newmount` 并按回车，将扩展分区中第一个逻辑驱动的文件系统挂载到 `/newmount`。接下来，输入 `df -hT` 命令并按回车验证文件系统已正确挂载。

- 14. 在命令提示符下，输入 `ls -F /newmount` 并按回车。看到发现的目录了吗？接下来，在命令提示符下输入 `cp /etc/hosts /newmount` 将 hosts 文件复制到新分区。再次在命令提示符下输入 `ls -F /newmount` 命令并按回车验证复制成功。

- 15. 在命令提示符下，输入 `umount /newmount` 并按回车，验证文件系统已正确卸载。

- 16. 在命令提示符下，输入 `vi /etc/fstab` 并按回车。在文件底部添加一行：
```
