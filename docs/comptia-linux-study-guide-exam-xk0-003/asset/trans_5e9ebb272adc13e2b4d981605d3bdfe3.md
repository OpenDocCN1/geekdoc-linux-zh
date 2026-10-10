

描述 RAID 阵列的用途。RAID 阵列可用于提高磁盘速度、磁盘可靠性或两者兼得。该阵列使用多个磁盘来绕过单个磁盘的速度限制，或存储数据的重复副本（或校验和）。

描述 LVM 的用途。LVM 用逻辑卷代替分区，从而提高了灵活性。与分区相比，逻辑卷可以更轻松地调整大小，这简化了未来的系统重新配置。LVM 还可以通过以类似 RAID 0 的方式将多个磁盘进行条带化来提高磁盘性能。

## 复习题

1. 在 x86 Linux 计算机上输入 `fdisk -1 /dev/hda` 会列出四个分区：`/dev/hda1`、`/dev/hda2`、`/dev/hda5` 和 `/dev/hda6`。以下哪项是正确的？
    - A. 该磁盘包含两个主分区和两个扩展分区。
    - B. `/dev/hda1` 或 `/dev/hda2` 中有一个是扩展分区。
    - C. 分区表已损坏；在 `/dev/hda5` 之前应该有 `/dev/hda3` 和 `/dev/hda4`。
    - D. 如果你使用 `fdisk` 添加了一个 `/dev/hda3`，那么 `/dev/hda5` 将变为 `/dev/hda6`，并且 `/dev/hda6` 将变为 `/dev/hda7`。

2. 以下哪类信息 `df` *无法* 报告？
    - A. 文件系统挂载的时长
    - B. ext3fs 分区上已使用的 inode 数量
    - C. 分区的文件系统类型
    - D. 分区上已使用的可用磁盘空间百分比

3. 一位新的 Linux 管理员计划创建一个具有独立的 `/home`、`/usr/local` 和 `/etc` 分区的系统。以下哪项最好地描述了这种配置？
    - A. 系统无法启动，因为 `/etc` 包含挂载非根分区所需的配置文件。
    - B. 系统可以启动，但 `/usr/local` 不可用，因为挂载的分区必须直接挂载在其父分区上，而不是子目录中。
    - C. 只有当 `/home` 分区位于与 `/usr/local` 分区不同的物理磁盘上时，系统才能启动。
    - D. 只要每个分区的大小足以满足其预期用途，系统就会正确启动并运行。

4. 你应该将哪个挂载点与交换分区关联？
    - A. `/\`
    - B. `/swap`
    - C. `/boot`
    - D. 无

5. 你运行了 Linux 的 `fdisk` 并修改了分区布局。但在退出程序之前，你意识到你正在错误的磁盘上操作。你可以做什么来纠正这个问题？
    - A. 什么都不能做；损害已经造成，你不得不从备份中恢复数据。
    - B. 输入 `w` 以退出 `fdisk` 而不保存磁盘上的更改。
    - C. 输入 `q` 以退出 `fdisk` 而不保存磁盘上的更改。
    - D. 重复输入 `u` 以撤销你错误执行的操作。

6. 以下命令实现了什么功能？
   `# mkfs -V -t ext2 /dev/sda4`
    - A. 它将 /dev/sda4 的分区表类型代码设置为 ext2。
    - B. 它将 FAT 分区转换为 ext2fs 分区，而不破坏分区上的现有文件。
    - C. 它在 /dev/sda4 上创建一个新的 ext2 文件系统，覆盖任何现有的文件系统和数据。
    - D. 没有；-V 选项无效，因此它导致 mkfs 中止其操作。

7. 你希望允许运行 OpenOffice.org 的 Linux 用户直接编辑存储在 Windows 2000 SMB/CIFS 文件服务器上的文件。以下哪项可用于启用此功能？
    - A. Linux 的标准 NFS 文件共享支持
    - B. 运行在 Windows 系统上的 FTP 服务器
    - C. Linux 的 smbclient 程序
    - D. Linux 的 smbmount 程序

8. 以下 /etc/fstab 文件条目有什么问题？（选择所有适用项。）
   `/dev/hda8 nfs default 0 0`
    - A. 该条目缺少挂载点规范。
    - B. /etc/fstab 中的所有字段都应使用逗号分隔。
    - C. default 选项只能用于 ext2 文件系统。
    - D. /dev/hda8 是磁盘分区，但 nfs 表示网络文件系统。

9. 交换文件可能位于哪里？
    - A. 仅在根 (/) Linux 文件系统中
    - B. 在本地读写 Linux 文件系统中
    - C. 在 NFS 或 ext2 文件系统中
    - D. 在任何拥有超过 512MB 空闲磁盘空间的分区上

10. 在以下哪种情况下，创建一个新的交换分区是最合理的？
    - A. 你常用的服务器几乎用尽了交换空间，且不需要常规维护。
    - B. 一台工作站的用户一直在使用内存密集型程序，超出了内存容量，需要快速修复。
    - C. 你正在向多用户系统添加一块新硬盘，并预计下个月左右会有几个新用户加入。
    - D. 系统因过度交换而经历性能缓慢。

11. 你向一台已经使用 LVM 的计算机添加了一块新磁盘。你对新磁盘进行了分区，并使用 pvcreate 在其一个分区上操作，以将其添加到现有的 LVM 中做准备。你应该使用哪个命令将这个分区 (/dev/sdb1) 添加到现有的 biglvm 卷组中？
    - A. pvdisplay /dev/sdb1
    - B. vgcreate biglvm /dev/sdb1
    - C. vgx extend biglvm /dev/sdb1
    - D. lvextend biglvm /dev/sdb1

12. 以下哪项是一个支持调整多个文件系统大小的 GUI 工具，包括 FAT、ext2fs 和 ReiserFS？
    - A. QTParted
    - B. GNU Parted
    - C. Part
    - D. cfdisk

13. 以下哪个选项与 fsck 一起使用，以强制其使用特定的文件系统类型？
    - A. -A
    - B. -N
    - C. -t
    - D. -C

14. 以下哪个实用程序会产生以下显示？
   ```
   total used free shared buffers cached
   Mem: 256452 251600 4852 0 10360 130192
   -/+ buffers/cache: 111048 145404
   Swap: 515100 1332 513768
   ```
    - A. mt
    - B. df
    - C. swapinfo
    - D. free

15. 当 root 用户运行以下命令时，结果是什么？
   `# mount /dev/sdc5 /home2`
    - A. /home2 的内容将使用默认文件系统挂载到 /dev/sdc5 上，并且会出现选项提示。
    - B. /home2 的内容将使用自动检测的文件系统类型和默认选项挂载到 /dev/sdc5 上。
    - C. /dev/sdc5 的内容将使用自动检测的文件系统类型和默认选项挂载到 /home2 上。
    - D. /dev/sdc5 的内容将使用默认文件系统挂载到 /home2 上，并且会出现选项提示。

16. 作为管理员，你希望增加 Linux SMB/CIFS 客户端系统的安全性。你希望通过将授权信息存储在其自己的文件中，而不是 /etc/fstab 中来实现这一点。当这样做时，你必须使用哪个 /etc/fstab 挂载选项来指向该文件？
    - A. certs=
    - B. securefile=
    - C. authorization=
    - D. credentials=

17. 一台新服务器将在周末到达。它将安装四个 1TB 的硬盘，并配置为 RAID 5 阵列，没有热备用硬盘。这个阵列可以存储多少数据？
    - A. 4TB
    - B. 3TB
    - C. 2TB
    - D. 1TB

18. 你的经理告诉你，从测试实验室移到生产环境的服务器必须将其中的两个硬盘镜像。使用哪种级别的 RAID 进行镜像？
    - A. RAID 6
    - B. RAID 5
    - C. RAID 1
    - D. RAID 0

19. 你要输入哪个命令来总结所有文件系统上的配额信息？
    - A. repquota
    - B. repquota -a
    - C. quotacheck
    - D. quotacheck -a

20. 在安装前为 Linux 创建分区时，你可以使用以下哪些工具？（选择所有适用项。）
    - A. Linux 的 fdisk，从紧急磁盘运行，在系统安装前执行
    - B. 从系统安装磁盘运行的 GNU Parted
    - C. 特定发行版的安装时实用工具
    - D. DOS FORMAT 实用工具，在系统安装前运行

