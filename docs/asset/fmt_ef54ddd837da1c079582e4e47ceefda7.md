
### 6.3. 更新系统的 systemd 进程，以便系统注册新的 `/etc/fstab` 配置。

```
@servera ~# systemctl daemon-reload
```

### 6.4. 通过输入 `/etc/fstab` 文件中的条目来启用交换空间。

```
@servera ~# swapon -a
```

### 6.5. 验证新的交换空间已启用。

```
@servera ~# swapon --show
NAME TYPE SIZE USED PRIO
/dev/vdb2 partition 47M 0B -2
```

- 7. 重启服务器机器。服务器重启后，登录并验证交换空间已启用。从服务器注销。

#### 7.1. 重启服务器机器。

```
@servera ~# systemctl reboot
Connection to server closed by remote host.
Connection to server closed.
[student@workstation]$
```

#### 7.2. 等待服务器重启并以 student 用户身份登录。

```
[student@workstation ~] ssh student@servera
...output omitted...
[student@servera ~$]
```

### 7.3. 验证交换空间已启用。

```
[student@servera ~# swapon --show
NAME TYPE SIZE USED PRIO
/dev/vdb2 partition 476M 0B -2
```

### 7.4. 回到工作站机器作为 student 用户。

```
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation ~$]
```

## 完成

在工作站机器上，更改 student 用户的家目录和 lab 命令以完成本次练习。这一步非常重要，可以确保之前练习的资源不会影响随后的练习。

```
[student@workstation ~]$ finish storage-swap
```

本节介绍结束。

## 实验

## 管理基础存储

在本次实验中，你将在新磁盘上创建分区，使用某些文件系统进行格式化并挂载它们，最后将它们激活为交换空间。

## 学习成果

- 使用 `parted` 命令显示并创建分区。
- 在分区上创建文件系统并持久化挂载它们。
- 创建交换空间并在启动时激活它们。

## 准备工作

以 student 用户身份登录工作站机器，使用 `lab` 命令为本次练习准备系统。

此命令将准备你的环境并确保所有所需资源均可用。

```
$student@workstation ~$ lab start storage-review
```

## 指南

- 1. 服务器机器有几块未使用的磁盘。在第一个未使用的磁盘上创建一个 2 GB 的备份分区。由于很难设置精确的大小，1.8 GB 到 2.2 GB 之间的大小都是可以的。配置备份分区以托管 XFS 文件系统。
2. 使用 XFS 文件系统格式化 2 GB 的备份分区，并将其持久化地挂载到 `/backup` 目录。
3. 在同一块磁盘上创建两个 512 MB 的分区，命名为 `swap1` 和 `swap2`。460 MB 到 564 MB 之间的大小都是可以的。配置分区的类型以托管交换空间。
4. 将两个 512 MB 分区初始化为交换空间并激活它们。设置 `swap2` 分区的优先级高于另一个分区。
5. 为了验证你的工作，重启服务器机器。确认系统自动将第一个分区挂载到 `/backup` 目录，并确认系统激活了交换空间。

## 评估

在工作站机器上作为 student 用户使用 `lab` 命令评估你的工作。修复任何报告的错误并重新运行命令直到成功。

```
$student@workstation ~$ lab grade-review
```

## 完成

在工作站机器上，切换到 student 用户目录并使用 `lab` 命令完成本次练习。这一步对于确保之前的练习资源不影响后续练习非常重要。

```
[student@workstation ~]$ finish storage-review
```

本节结束。

## 管理基础存储

## 解决方案

在本次实验中，你在新磁盘上创建分区，格式化某些文件系统并挂载它们，并将它们激活为交换空间。

## 学习成果

- 使用 `parted` 命令显示并创建分区。
- 在分区上创建文件系统并持久化挂载它们。
- 在启动时激活它们。

## 准备工作

以 student 用户身份登录工作站机器，使用 `lab` 命令为本次练习准备系统。

此命令将准备你的环境并确保所有所需资源均可用。

```
[student@workstation ~$ lab start storage-review
```

## 指南

- 1. 服务器机器有几块未使用的磁盘。创建一个 2 GB 的备份分区。由于很难设置精确的大小，1.8 GB 到 2.2 GB 之间的大小都是可以的。配置备份分区以托管 XFS 文件系统。
1. 登录服务器并切换到 student 用户，然后切换到 root 用户。

```
[student@workstation ~]$ ssh student@server
... omitted...
[student@server ~]$ sudo -i
[sudo] password for student:
[root@server ~]#
```

2. 识别未使用的磁盘。确认第一个未使用的 `/dev/vdb` 没有分区。

```
[root@server ~]# lsblk
NAME  SIZE TYPE MOUNTPOINTS
da    20G  
da1   1M  part
da2   200M part /boot/efi
da3   500M part /boot
da4   9G  part
vdb   2G
```

3. 确认 `/dev/vdb` 磁盘没有标签。

```
[root@server ~]# parted /dev/vdb
Error: /dev/vdb: unrecognized label
Model: Virtio Device (virtblk)
Disk /dev/vdb: 5360M
Sector size (logical/physical): 512B
Partition Table: unknown
```

4. 定义 GPT 分区方案。

```
[root@server ~]# parted /dev/vdb mklabel gpt
Information: You may need to update /etc/fstab.
```

5. 创建 xfs 文件系统的 2 GB 备份分区。从 2048 开始分区。

```
[root@server ~]# parted /dev/vdb mkpart backup 2048 2GB
Information: You may need to update /etc/fstab.
```

6. 确认备份分区的创建。

```
[root@server ~]# parted /dev/vdb print
Model: Virtio Device (virtblk)
Disk /dev/vdb: 5360M
Sector size (logical/physical): 512B
Partition Table: gpt
Disk Flags:
| Number | Start | End | Size | Name | Flags |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1048K | 20000M | 1999MB | backup | |
```

- 7. 运行 `udev settle` 命令。此命令等待系统检测新分区并创建 `/dev/vdb` 设备。

```
[root@server ~]# udevadm settle
```

2. 使用 XFS 文件系统格式化 2 GB 的备份分区，并将其持久化地挂载到 `/backup` 目录。

- 2.1. 格式化 `/dev/vdb1`。

```
[root@server ~]# mkfs.xfs /dev/vdb1
meta-data=/dev/vdb1
  isize=512
  agsize=121984 blks
  sects=512 attr  2,projid32bit=1
  crc=1 inline=1,sparse=1,realloc=0
  reflink=1 bigtime=1 incount=1
  data bsize=4096 blocks=487936,maxpart=25
  sunit=0 swidth=0 blks
```
