
- `b` 编辑 `bsdlabel`
- `c` 切换 `dos` 兼容性标记
- `d` 删除分区
- `l` 列出已知的分区类型
- `print` 打印此菜单
- `a` 添加新分区
- `o` 创建新的空 `DOS` 分区表
- `p` 打印分区表
- `q` 退出且不保存更改
- `s` 创建新的空 `Sun` 磁盘标签
- `t` 修改分区的系统 `ID`
- `u` 更改显示/条目单位
- `v` 验证分区表
- `w` 将表写入磁盘并退出
- `x` 额外功能（仅限专家）

`Command (m 获取帮助) : _`

若要打印当前在 `/dev/hdc` 上设置的分区列表，你可以在 `fdisk` 提示处按下 `p` 键：

```
Command (m 获取帮助) : p
```

`Disk /dev/hdc: 20.4 GB, 20490559488 bytes`

`255 heads, 63 sectors/track, 2491 cylinders`

`Units = cylinders of 16065 * 512 = 8225280 bytes`

| 设备 | 起始 | 结束 | 块 | Id 系统 |
| :--- | :--- | :--- | :--- | :--- |
| `/dev/hdc1` | 1 | 510 | 4096543+ | 83 Linux |
| `/dev/hdc2` | 511 | 561 | 409657+ | 82 Linux swap |
| `/dev/hdc3` | 562 | 1247 | 5510295 | 83 Linux |

`Command (m 获取帮助) : _`

注意设备名称出现在前述输出的左侧，包括启动的分区（`/dev/hdc1`）、物理硬硬盘上分区的起始和结束位置（起始和结束磁道）、分区内用于存储信息的总块数，以及分区的类型和描述（83 是 Linux 分区，82 是 Linux 交换分区）。Linux 分区可以包含 Linux 文件系统，例如 `ext2` 或 `ext3`。

# 第 6 章 Linux 文件系统管理

要删除 `/dev/hdc3` 分区以及你所在文件系统中包含的所有数据，你可以使用之前未说明的 `n` 键：

```
Command (m 获取帮助): d
Partition number (1-4): 3
Command (m 获取帮助): p
```

`/dev/hdc: 20.4 GB, 2049055948 bytes`

`255 heads, 63 sectors/track, 2491 cylinders`

`Units = cylinders of 16065 * 512 = 8225280`

| 设备 | 起始 | 结束 | 块 | Id | 系统 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hdc1` | 1 | 510 | 4096543+ | 83 | Linux |
| `/dev/hdc2` | 511 | 561 | 409657+ | 82 | Linux swap |

`Command (m 获取帮助): _`

若要使用第四个分区（`/dev/hdc4`）创建一个带有两个逻辑驱动器（`/dev/hdc5` 和 `/dev/hdc6`）的扩展分区，可以使用之前说明的 `n` 键，并指定要创建的分区、硬盘上的起始磁道以及以块为单位的大小（`+1000M` 会创建一个 1000MB 的分区）：

```
Command (m 获取帮助): n
Command action
- - extended
- primary partition (1-4) 
e
Partition number (1-4): 4
First cylinder (562-2491, default 562): 562
Last cylinder or +size or sizeM or +sizeK (562-2491, default 2491): 1247
Command (m 获取帮助): p
```

`/dev/hdc: 20.4 GB, 2049055948 bytes`

`255 heads, 63 sectors/track, 2491 cylinders`

`Units = cylinders of 16065 * 512 = 8225280`

| 设备 | 起始 | 结束 | 块 | Id | 系统 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hdc1` | 1 | 510 | 4096543+ | 83 | Linux |
| `/dev/hdc2` | 511 | 561 | 409657+ | 82 | Linux swap |
| `/dev/hdc4` | 562 | 1247 | 5510295 | 5 | Extended |

```
Command (m 获取帮助): n
Command action
- - logical (5 or over)
- primary partition (1-4)
First cylinder (562-1247, default 562): 562
Last cylinder or +size or +sizeM or +sizeK (562-1247, default 1247): +1000M
Command (m 获取帮助): p
```

`/dev/hdc: 20.4 GB, 2049055948 bytes`

`255 heads, 63 sectors/track, 2491 cylinders`

`Units = cylinders of 16065 * 512 = 8225280 bytes`

| 设备 | Boot | 起始 | 结束 | 块 | Id | 系统 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hdc1` |  | 1 | 510 | 4096543+ | 83 | Linux |
| `/dev/hdc2` |  | 511 | 561 | 409657+ | 82 | Linux swap |
| `/dev/hdc4` |  | 562 | 1247 | 5510295 | 5 | Extended |
| `/dev/hdc5` |  | 562 | 689 | 102818+ | 83 | Linux |
| `/dev/hdc6` |  | 690 | 944 | 204826 | 82 | Linux |

`Command (m 获取帮助) : _`

从前述输出可以注意到，设备名称出现在左侧，包括启动的分区（`/dev/hdc1`）、物理硬硬盘上分区的起始和结束位置（起始和结束磁道）、分区内用于存储信息的总块数，以及分区的类型和描述（83 是 Linux 分区，82 是 Linux 交换分区）。

## Linux 文件系统管理

写入超级块和文件系统计数信息：

此文件系统每隔 36 次挂载或 180 天自动检查一次，以先者为准。使用 `tune2fs -c` 或 `-i` 可以覆盖。

```
[root@server1 root]#
```

随后，你可以使用 `tune2fs` 命令将此文件系统转换为 `ext3`，并在文件系统上创建一个日志文件：

```
[root@server1 root]# tune2fs -j /dev/hdc5
tune2fs 1.35 (28-Feb-2004)
```

创建日志 `inode`：完成

此文件系统每隔 36 次挂载或 180 天自动检查一次，以先者为准。使用 `tune2fs -c` 或 `-i` 可以覆盖。

```
[root@server1 root]#
```

或者，你也可以使用 `mke2fs -j /dev/hdc5` 或 `mkfs.ext3 /dev/hdc5` 命令创建一个 `ext3` 文件系统。要将此文件系统挂载到名为 `/data` 的新挂载点并查看内容，你可以使用以下命令：

```
[root@server1 root]# mkdir /data
[root@server1 root]# mount -t ext3 /dev/hdc5 /data
[root@server1 root]# mount
/dev/hdc1 / type ext3 (rw)
none on /proc type (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usbdevfs on /proc/bus/usb type usdevfs (rw)
none on /dev/shm type tmpfs (rw)
/dev/hdc5 /data type ext3 (rw)
[root@server1 root]# ls -F /data
lost-found/
[root@server1 root]#
```

为了让系统在每次启动时自动挂载此文件系统，只需编辑 `/etc/fstab` 文件，其中包含针对 `/dev/hdc5` 的以下条目：

```
[root@server1 root]# cat /etc/fstab
```
