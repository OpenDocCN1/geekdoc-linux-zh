
```
[server1 root]# edquota -u user
Disk quotas for user user (uid 500):
```

| Filesystem | blocks | soft | hard | inodes | soft | hard |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hd1` | 1188 | 0 | 0 | 326 | 0 | 0 |

```
~
~
*/tmp/edquota.aclsave* 3L, 216C
```

## 磁盘配额 269

接下来，在提供的列中填入相应的值，然后保存并退出编辑器：

Disk quotas for user user1 (uid 500):

| Filesystem | blocks | soft | hard | inodes | soft | hard |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/sda1` | 1188 | 18420 | 20480 | 326 | 900 | 1000 |

```
~~
~~
wq
"/tmp/edquota.aclsave" 3L, 216C written
[rootserver]#
```

6. 使用 `edquota -u -t` 命令编辑允许超出配额的用户限制。软限制的默认限制为七天，可以如下所示进行更改：

```
[rootserver]# edquota -u -t
Grace period before enforcing soft limits for users:
Time units may be: days, hours, minutes, or seconds
Filesystem | Block grace period | Inode grace period
/dev/sda1 | 7Days | 7days
```

```
"/tmp/edquota.aclsave" 4L, 233C
```

7. 使用 `repquota` 命令收集 `/` 文件系统的配额报告，以确保配额已正确更新，输出如下所示：

```
[rootserver]# repquota /
*** Report for user quotas on device /dev/hdc1
Block grace time: 7days; Inode grace time: 7days
| Block limits | File limits |
| User | used | soft | hard | grace | used | soft | hard |
| root | 6420573 | 0 | 0 | 376520 | 0 | 0 |
| bin | 14912 | 0 | 0 | 47 | 0 | 0 |
| daemon | 16 | 0 | 0 | 5 | 0 | 0 |
| lp | 8 | 0 | 0 | 2 | 0 | 0 |
| news | 4396 | 0 | 0 | 228 | 0 | 0 |
| uucp | 9612 | 0 | 0 | 23 | 0 | 0 |
| games | 0 | 0 | 0 | 65 | 0 | 0 |
| rpm | 101056 | 0 | 0 | 120 | 0 | 0 |
| vsync | 8 | 0 | 0 | 143 | 0 | 0 |
| rpcuser | 32 | 0 | 0 | 8 | 0 | 0 |
| cap | 256 | 0 | 0 | 14 | 0 | 0 |
| smm | 12 | 0 | 0 | 3 | 0 | 0 |
| apache | 48 | 0 | 0 | 12 | 0 | 0 |
| squid | 16 | 0 | 0 | 4 | 0 | 0 |
| webal | 24 | 0 | 0 | 6 | 0 | 0 |
| xfs | 8 | 0 | 0 | 3 | 0 | 0 |
| named | 36 | 0 | 0 | 9 | 0 | 0 |
| ntp | 12 | 0 | 0 | 1 | 0 | 0 |
| gdm | 28 | 0 | 0 | 2 | 0 | 0 |
| pvm | 8 | 0 | 0 | 2 | 0 | 0 |
| wnn | 4184 | 0 | 0 | 44 | 0 | 0 |
| postfix | 88 | 0 | 0 | 22 | 0 | 0 |
| mailman | 4 | 0 | 0 | 2 | 0 | 0 |
| amanda | 1108 | 0 | 0 | 74 | 0 | 0 |
| netdump | 32 | 0 | 0 | 9 | 0 | 0 |
| quagga | 32 | 0 | 0 | 8 | 0 | 0 |
| radvd | 8 | 0 | 0 | 2 | 0 | 0 |
| radiusd | 24 | 0 | 0 | 2 | 0 | 0 |
| ldap | 8 | 0 | 0 | 0 | 0 | 0 |
| mysql | 16 | 0 | 0 | 5 | 0 | 0 |
| postgres | 5352 | 0 | 0 | 279 | 0 | 0 |
| fax | 60 | 0 | 0 | 5 | 0 | 0 |
| nut | 28 | 0 | 0 | 48 | 0 | 0 |
| privoxy | 624 | 0 | 0 | 6 | 0 | 0 |
| tomcat | 24 | 0 | 0 | 6 | 0 | 0 |
| cyrus | 16888 | 0 | 0 | 34 | 0 | 0 |
| exim | 40 | 0 | 0 | 10 | 0 | 0 |
| user1 | 1188 | 18432 | 20480 | 326 | 900 | 1000 |
```

```
[root@server1]#
```

注意，上述输出中的大多数用户都是系统用户，未对其应用配额。这些用户在第 10 章“管理 Linux 进程”中讨论。

上述命令必须由 `root` 用户执行；但普通用户可以使用 **`quota` 命令**查看自己的配额。`root` 用户也可以使用 `quota` 命令来查看其他用户的配额：

```
[root@server1]# quota

Disk quotas for user root (uid 0): none

[root@server1]# quota -u user1

Disk quotas for user user1 (uid 500):

Filesystem blocks limit quota limit

/dev/hdc1 1188 18432 20480 900 1000

[root@server1]#
```

## 章总结

- 磁盘设备由位于 `/dev` 目录下的设备文件表示。这些设备文件指定了数据传输类型、Linux内核中设备驱动程序的主设备以及特定设备的设备号。
- 每个设备必须包含一个文件系统，通过 `mount` 命令将其挂载到 Linux 目录树中。稍后可以使用 `umount` 命令将其卸载。用于挂载设备的目录在未被登录用户使用的时才能进行挂载和卸载。
- 在分区上创建文件系统之前，必须将硬盘划分不同的区域。可以使用 `fdisk` 命令对硬盘进行分区。
- Linux 可多种不同的文件系统；每个文件系统针对特定用途，可以将多个不同的文件系统挂载到目录树上的不同挂载点。您可以使用 `mkfs` 命令及其变体在设备上创建文件系统。
- 使用 `df` 和 `du` 命令监控磁盘空间对于避免存储空间不足非常重要。同样，使用 `fsck` 命令及其变体检查错误也是重要的。
- 如果磁盘空间有限，可以使用硬配额来限制每个用户在文件系统上的可用空间。

## 关键术语

- **`dev directory`** — 根目录下通常用于存储设备文件的目录。
- **`dev/mknod`** — 当设备信息（主设备号、次设备号或类型（字符或块））未知时，用于重新创建设备文件的命令。
- **`etc/fstab`** — 包含启动时挂载的文件系统信息的文件。
- **`edquota`** — 用于编辑用户配额的命令。
- **`fsck`** — 用于检查和修复文件系统的命令。
- **`hard limit`** — 无法超过的强制限制。
- **`major number`** — 内核用于识别调用哪个设备驱动程序与硬件交互的主号。
- **`minor number`** — 内核用于识别特定硬件设备的设备号。
- **`mkfs`** — 用于格式化或创建文件系统的命令。
- **`mount`** — 用于将文件系统挂载到设备的命令。
- **`mount point`** — 文件系统中用于挂载某些内容的目录。
- **`mounting`** — 将设备与逻辑树中的目录关联起来的过程。
- **`partition`** — 硬盘的物理划分。
- **`quota`** — 用于查看施加给用户配额的命令。
- **`quotaoff`** — 用于禁用磁盘配额的命令。
- **`quotaon`** — 用于激活磁盘配额的命令。
- **`quotas`** — 施加在用户文件系统上的限制。
- **`repquota`** — 用于生成特定文件系统配额报告的命令。

## 复习题 273

**扇区 (sector)** — 硬盘上数据存储的最小单元；扇区排列成称为“轨道”的同心圆，并可以组成块供系统使用。
**软限制 (soft limit)** — 一种施加的限制，但在一定时间内可以被超过。
**同步 (syncing)** — 将存储在 RAM 中的数据写入硬盘驱动器的过程。
**轨道 (track)** — 硬盘上由扇区组成同心圆形状的区域。

**tune2fs 命令** — 用于修改 ext2 和 ext3 文件系统参数的命令。
**umount 命令** — 用于断开逻辑目录树中设备与目录之间关联的命令。

## 复习题

1. 你发现 `/dev` 目录下的一个设备文件损坏了。你知道该设备是 `/dev/tty3` 且且它是一个字符设备文件。你应该怎么做？
   a. 使用 `fsck` 命令修复文件。
   b. 使用 `mknod` 命令重新创建文件。
   c. 使用 `/dev/MAKEDEV` 命令重新创建文件。
   d. 什么都不做；没有次设备号，你无法重新创建文件。

2. 硬盘上的分区用文件系统格式化后，该硬盘上的所有分区都必须使用相同的文件系统。对还是错？

3. 你想查看系统当前正在使用的文件系统。你可以使用什么？
   a. `cat /etc/stab`
   b. `ls -l /etc/stab`
   c. `cat /etc/mtab`
   d. `ls -l /etc/stab`

4. Jim 刚刚购买了两个新的 SCSI 硬盘和一个控制器卡。他正确地将硬件安装在了机器中。在使用它们进行数据存储和检索之前，他必须做什么？（选择所有适用项）
   a. 挂载这两个硬盘，以便操作系统可以访问它们。
   b. 在每个硬盘驱动器上挂载文件系统。
   c. 使用 `fdisk` 命令在每个硬盘上创建一个或多个分区。
   d. 使用 `vi` 编辑器编辑 `/etc/mtab` 并为控制器卡和硬盘创建条目。
   e. 挂载在两个硬盘上创建的任何分区，以便操作系统可以访问它们。
   f. 使用 Linux 识别的有效文件系统格式化创建的任何分区。

## 第 6 章 Linux 文件系统管理

5. 给定来自 `/etc/fstab` 的输出，哪些文件系统将在启动时由 `fsck` 命令自动检查？

| 设备 | 挂载点 | 类型 | 选项 | 储储 | 检查 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| LABEL=/ | | ext3 | defaults | 1 | 1 |
| none | /dev/pts | devpts | gid=5,mode=620 | 1 | 0 |
| none | /dev/proc | proc | defaults | 0 | 1 |
| none | /dev/shm | tmpfs | defaults | 1 | 0 |
| /dev/hdc2 | swap | swap | defaults | 0 | 0 |
| /dev/cdrom | /mnt/cdrom | iso9660 | noauto,owner,kudzu | 0 | 0 |
| /dev/fd0 | /mnt/floppy | auto | noauto,owner,kudzu | 0 | 0 |

   a. none，因为 `fsck` 必须为每个文件系统手动运行
   b. `/dev/pts` 和 `/dev/shm`
   c. `/proc` 和 swap，因为 `fsck` 在启动时会自动为所有文件系统运行

6. 用户将一个设备挂载到挂载点目录，随后发现需要之前在 particular挂载目录中找到的文件。该用户应该怎么做？

   a. 什么都不做：文件丢失了且永远无法访问。
   b. 什么都不做：文件不可能在那里，因为你只能向空目录挂载。
   c. 从目录中卸载设备。
   d. 运行 `fsck` 命令恢复文件。
   e. 在 `lost+found` 目录中查找文件。

7. 哪个命令用于显示文件系统的空闲空间？

   a. fsck
   b. quota
   c. du
   d. df

8. 为了在文件系统上成功运行 `fsck` 命令，你必须做什么？

   a. 带有 `-u` 选项运行 `fsck` 命令以先自动卸载文件系统。
   b. 当警告在挂载的文件系统上运行 `fsck` 会导致损坏时，选择 yes。
   c. 卸载文件系统。
   d. 确保文件系统已挂载。

9. 字符设备传输数据的速度通常比块设备快。对还是错？

## 复习题 275

10. `du /var` 命令的作用是什么？

    a. 显示连接到 `/var` 目录的用户
    b. 显示 `/var` 目录内所有目录的大小
    c. 倾储 `/var` 目录
    d. 显示 `/var` 目录中的空闲空间

11. 命令 `tune2fs -h` 的什么？

    a. 备份一个 ext2 文件系统
    b. 显示 ext2 文件系统中已用和可用的 inode 数量
    c. 倾储一个 ext2 文件系统
    d. 不是一个有效命令

12. 系统上的第一个软盘没有响应。你输入 `/dev/fd0` 命令并收到以下输出。问题出在哪里？

```
[root@server1 root]# file /dev/fd0

/dev/fd0: ASCII text

[root@server1 root]#
```
