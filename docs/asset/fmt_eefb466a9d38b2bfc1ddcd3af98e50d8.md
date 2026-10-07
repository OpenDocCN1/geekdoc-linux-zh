
# 在 CENTOS 7 中创建 RAID 1

RAID 0 没有容错，但有一些优势：

- 高性能
- 不浪费空间
- 读写速度快

在虚拟机中设置 RAID 0：

要求：
- 虚拟机
- 两个磁盘
- 网络连接
- 静态 IP 地址（如果你想 `ssh` 连接服务器）

## 1

在 `centos7` 虚拟机中添加两个 `20GB` 磁盘。

### 硬件选项

| 设备 | 摘要 |
| :--- | :--- |
| 内存 | 2 GB |
| 处理器 | 1 |
| 硬盘 (SCSI) | 70 GB |

磁盘文件
`/home/tanvirrahman/vmware/raid0/CentOS 7 64-bit (fresh image)-cl1vi`

容量
当前大小: 8.8 MB
最大大小: 70 GB

## Tanvir Rahman

### UBUNTU $ CENTOS 管理员

```
[root@server2 -]#
```

```
[root@server2 -]# fdisk /dev/sdb
欢迎使用 fdisk (util-linux 2.23.2)。
```

更改将仅保留在内存中，直到你决定写入它们。
在使用 write 命令之前请小心。

设备不包含识别的分区表
正在创建一个磁盘符为 `0xc4707f2b` 的新 DOS 标签磁盘。

```
Command (m for help): n
```

分区类型:

  `p` (primary, 0 extended, 4 free)

  `e`

选择 (default `p`): `p`

分区编号 (1-4, default 1):

起始扇区 (2048-41943039, default 2048):

使用默认值 2048

类型为 Linux 的分区 1，大小为 20 Gib

```
最后一个扇区，+sectors +size(K,M,G) (2048-41943039, default 41943039)
使用默认值 41943039
```

```
Command (m for help): p
Disk /dev/sdb: 21.5 GB, 2147483640 bytes, 41943040 sectors

Units = sectors of 1 * 512 = 512 bytes

扇区大小 (逻辑/物理): 512 bytes / 512 bytes

I/O 大小 (minimum/optimal): 512 bytes / 512 bytes

磁盘类型: dos

磁盘符: 0xc470f2b
```

| Device | Boot | End | Blocks | Id | System |
| :--- | | | | | |
| `/dev/sdb1` | 2048 | 41943039 | 20970496 | Linux |

```
Command (m for help): p
```

> [在分区上创建 raid]

## Tanvir Rahman

```
[root@server2]# fdisk /dev/sdb
欢迎使用 fdisk (util-linux 2.23.2)。
更改将仅保留在内存中，直到你决定写入它们。
在使用 write 命令之前请小心。

Command (m for help): t
选择分区 1
Hex 代码 (type to list all): fd
将分区 'Linux' 类型更改为 'Linux raid autodet'

Command (m for help): p
Disk /dev/sdb: 21.5 GB, 2147483640 bytes, 41943040 sectors
Units = sectors of 1 + 512 = 512 bytes
扇区大小 (逻辑/物理): 512 bytes / 512 bytes
I/O (minimum/optimal): 512 bytes / 512 bytes
磁盘类型: dos
磁盘符: 0xc407f2b
```

| Device | Start | End | Blocks | Id | System |
| :--- | | | | | |
| `/dev/sdb1` | 2048 | 41943039 | 20970496 | Linux raid autodet |

```
Command (m for help): w
分区表已更改！

正在调用 ioctl() 重新读取分区表。
正在同步磁盘。
[root@server2]#
```

### 查看块设备

## 9

对 `'sdd'` 执行步骤

=>`fdisk /dev/sdb`

## 10

使用 `'lsblk'` 检查

=>`lsblk`

```
[root@server2 ~]# lsblk
NAME      MAJ:MIN SIZE TYPE MOUNTPOINT
sda       8:0    0 70G 0 disk
-sda1    8:1    0  1G 0 part /boot
-sda2    8:2    0 69G 0 part
-centos-root 253:0 0 45G lvm /
-centos-swap 253:1 0 20G lvm [SWAP]
-centos-home 253:2 0 22G lvm /home
sdb       8:16   0 20G 0 disk
-sdb1    8:17   0 20G 0 part
sdc       8:32   0 20G 0 disk
-sdc1    8:33   0 20G 0 part
sr0       11:0   1 4.3G 0 rom
```

## 11

使用 `'mdadm'` 检查

```
[root@server2 ~]# mdadm --examine /dev/sd[b-c]1
mdadm: 在 /dev/sdb1 未检测到 md 超块。
mdadm: 在 /dev/sdc1 未检测到 md 超块。
[root@server2 ~]#
[root@server2 ~]#
```

## Tanvir Rahman

## 12

创建 RAID md 设备

=>`mdadm --create /dev/md0 --level=stripe --raid-devices=2 /dev/sd[b-c]1`

```
[root@server2 ~]#
[root@server2 ~]# mdadm --create /dev/md0 --level=stripe --raid-devices=2 /dev/sd[b-c]1
mdadm: 默认版本 1
mdadm: 数组 /dev/md0 已启动。
[root@server2]#
```

## 13

查看 RAID 0 设备的详情

=>`mdadm --detail /dev/md0`

## 14

在系统上分配文件系统

=>`mkfs.ext4 /dev/md0`

```
[root@server2 ~]# mkfs.ext4 /dev/md0
文件系统类型 Linux
块大小=4096 (log=2)
碎片大小=4096 (log=2)
Stride=128, width=256
inodes=262144, 532480 blocks (5%) 留给 root
最大文件系统块=2157969408
groups=32768, 8192 inodes per group
Superblocks 存储在块上: 32768, 98304, 163840, 229376, 249412, 319200, 384736, 409600
分配组表: 完成
写入 inode 表: 完成
创建日志 (32768 块): 完成
写入超级块和文件系统信息: 完成
```

## 15

挂载卷

=>`mkdir /mnt/raid0`

=>`mount /dev/md0 /mnt/raid0`

## 16

检查挂载的卷

=>`df -h`

```
[root@server2 ~]# df Size Used Avail% Mounted on
Filesystem
/dev/mapper/centos-root 45G 3.8G 42% /dev
tmpfs 974M 0 974M 0% /dev/shm
tmpfs 991M 11M 981M 0% /run
tmpfs 991M 0 991M 0% /sys/fs/cgroup
dev/sda1 1014M 166M 849M 17% /boot
/dev/mapper/centos-home 22G 39M 22G 17% /home
tmpfs 199M 12K 199M 0% /run/user
tmpfs 199M 0 199M 0% /run/user/0
/dev/md0 40G 49M 38G 1% /mnt/raid0
[root@server2 ~]#
```

## 17

使用 `lsblk` 检查块设备

=>`lsblk`

```
[root@server2 ~]# lsblk
NAME MAJ:MIN RM TYPE MOUNTPOINT
sda 8:0 0 70G 0 disk
-sda1 8:1 0 1G 0 part /boot
-centos-root 253:0 0 45G 0 lvm /
-sda2 8:2 0 69G 0 part
-centos-swap 253:1 0 26G 0 lvm [SWAP]
-centos-home 253:2 0 22G 0 lvm /home
sdb 8:16 0 20G 0 disk
-sdb1 8:17 0 20G 0 part
-md0 9:0 0 20G 0 raid0 /mnt/raid0
sdc 8:32 0 20G 0 disk
-sdc1 8:33 0 20G 0 part
-md1 9:0 0 40G 0 raid0 /mnt/raid0
sr0 11:0 1 4.36G 0 rom
[root@server2 ~]#
```

## 创建分区

```bash
[root@server2 ~]# fdisk /dev/sdb
Welcome to fdisk (util-linux 2.23.2).

更改将仅保留在内存中，直到你决定写入它们。
在使用 write 命令前请务小心。

设备不包含可识别的分区表
正在构建标识符为 0xc4707f2b 的新 DOS 磁盘标签。

命令 (m 获取帮助): n
分区类型:
p primary (0 primary, 0 extended, 4 free)
e extended
选择 (默认 p): p
分区编号 (1-4, 默认 1):
起始扇区 (2048-4194309, 默认 2048):
使用默认值 4194309
结束扇区, +sectors +size(K,M,G) (2048-4194309, 默认 41943039):
使用默认值 4194309
设置类型为 Linux 且大小为 20 GiB 的分区 1

命令 (m 获取帮助): p
Disk /dev/sdb: 21.5 GB, 2147483648 bytes, 41943040 sectors
Units = sectors of 1 * 512 = 512 bytes
扇区大小 (逻辑/物理): 512 bytes / 512 bytes
I/O 大 (最小/最优): 512 bytes / 512 bytes
磁盘标签类型: dos
磁盘标识: 0xc4707f2b
```

| Device | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|
| `/dev/sdb1` | 2048 | 41943039 | 20970496 | 83 | Linux |

```
命令 (m 获取帮助): :
```

### 在该分区上创建 raid

### Tanvir Rahman

```bash
[root@server2 ~]# fdisk /dev/sdb
Welcome to fdisk (util-linux 2.23.2).
更改将仅保留在内存中，直到你决定写入它们。
在使用 write 命令前请务小心。
命令 (m 获取帮助): t
已选择分区 1
代码 (输入 L 列出所有代码): fd
已将分区 'Linux' 类型更改 'Linux raid autodetect'
命令 (m 获取帮助): P
Disk /dev/sdb: 21.5 GB, 2147483640 bytes, 41943040 sectors
Units = sectors of 1 * 512 = 512 bytes
扇区大小 (逻辑/物理): 512 bytes / 512 bytes
I/o 大 (最小/最优): 512 bytes / 512 bytes
磁盘标签类型: dos
Disk Identifier: 0xc4707f2b
Device Boot Start Blocks Id System
/dev/sdb1 2048 41943039 20970496 fd Linux raid autodetect
命令 (m 获取帮助): w
分区表已更改！
正在调用 ioctl() 重新读取分区表。
正在同步磁盘。
[root@server2 ~]#
```

### 查看块设备

### 步骤 9

对 `'sdc'` 执行步骤 8

=>`fdisk /dev/sdc`

### 步骤 10

使用 `'lsblk'` 检查

### UBUNTU $ CENTOS 员员

=>`lsblk`

| NAME | MAJ:MIN RM SIZE TYPE MOUNTPOINT |
|---|---|---|---|---|---|
| sda | 8:0 0 70G | disk | |
| ├-sda1 | 8:1 0 16G | part | /boot |
| └-sda2 | 8:2 0 69G | part | |
| ├-centos-root | 253:0 0 456G | lvm | |
| ├-centos-swap | 253:1 0 26G | lvm | [SWAP] |
| └-centos-home | 253:2 0 226G | lvm | /home |
| sdb | 8:16 0 200G | disk | |
| └-sdb1 | 8:17 0 200G | part | |
| sdc | 8:32 0 200G | disk | |
| └-sdc1 | 8:33 0 200G | part | |
| sr0 | 11:0 1 4.36G | rom | |

### 步骤 11

使用 `'mdadm'` 检查

```bash
[root@server2 ~# mdadm --dev/sd[b-c]1
mdadm: No md superblock detected on /dev/sdb1.
mdadm: No md superblock detected on /dev/sdc1.
[root@server2 ~#]
[root@server2 ~]#
```

### Tanvir Rahman

### 步骤 12

创建 RAID md 设备（带镜像）

=>`mdadm --create /dev/md0 --level=mirror --raid-devices=2 /dev/sd[b-c]1`

```bash
[root@server2 ~# mdadm --create /dev/md0 --level=mirror --raid-devices=2 /dev/sd[b-c]1
[root@server2 ~# mdadm --create /dev/md0 --level=mirror --raid-devices=2 /dev/sd[b-c]1
mdadm: Note: this array has metadata at the start may not be suitable as boot device. If you plan to store 'boot' on this device please use metadata=0, continue? y
mdadm: array /dev/md0 started.
[root@server2 ~#]
```

### 步骤 13

查看 RAID 设备的详情

=>`mdadm --detail /dev/md0`

### 步骤 14

文件系统分区

=>`mkfs.ext4 /dev/md0`

```bash
[root@server2 ~]# mkfs.ext4 /dev/md0
Filesystem /dev/md0 is ext4
Block size (4096)stride=128, stripe width=256
blocks: 524288 reserved for root
Maximum blocks=2157948
32768 blocks per group
8192 inodes per group
Superblock stored on blocks: 3768,8304,16384,22972,249412,319200,384736,405632,409600,6224
Allocating group tables: done
Writing inode tables: done
Creating journal (3768 blocks): done
Writing superblocks and filesystem information: done
```

### 步骤 15

挂载卷

=>`mkdir /mnt/raid0`

=>`mount /dev/md0 /mnt/raid0`

### Tanvir Rahman

### 步骤 16

检查挂载的卷
