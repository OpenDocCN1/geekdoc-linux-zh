
```
[root@server1 ~]# ls -l /dev/mapper/
lrwxr-xrwx 1 root 17,6 data1 -> dm-0
lrwxr-xrwx 1 root 17,6 data2 -> dm-1
[root@server1 ~]# ls -l /dev/mapper/vg0
lrwxr-xrwx 1 root 17,6 vg0-data1 -> dm-0
lrwxr-xrwx 1 root 17,6 vg0-data2 -> dm-1
[root@server1 ~]#
```

# CompTIA Linux+ 和 LPIC-1：Linux 认证指南

| | | ext4 | 150M | 757M | 17% | /boot |

|---|---|---|---|---|---|---|

| /dev/sda2 | | 974M | | | | |

| /dev/sda1 | vfat | 599M | 14M | 585M | 3% | /boot/efi |

| tmpfs | | 392M | 92K | 392M | 1% | /run/user/42 |

| tmpfs | | 392M | 76K | 392M | 1% | /run/user/0 |

| tmpfs | /dev/mapper/vg00-data ext4 | 9.8G | 24K | 9.3G | 1% | /data |

| | /dev/mapper/vg00-data ext2 | | 8.3G | 24K | 7.9G | 1% | /data2 |

> 注意 25

如果在扩展逻辑卷（LV）时没有在 `lxtend` 命令中使用 `-r` 参数来调整文件系统大小，你的系统将无法使用额外的空间。在这种情况下，你可以在扩展 LV 后使用命令来调整文件系统大小。例如，要扩展 ext2/ext3/ext4 文件系统，可以使用 `resize2fs` 命令；而要扩展 XFS 文件系统，可以使用 `xfs_info` 命令或 `xfs_growfs` 命令。

除了本节讨论的命令外，还有许多其他命令可以列出并配置 PV、VG 和 LV。表 5-6 总结了这些命令。

## 表 5-6 常用 LVM 命令

| 命令 |or |
|---|---|
| `pvdisplay` | 显示 PV 配置 |
| `pvscan` | | |
| `pvs` | | |
| `vgdisplay` | 显示 VG 配置 |
| `vgscan` | | |
| `vgs` | | |
| `lvdisplay` | 显示 LV 配置 |
| `lvscan` | | |
| `lvs` | | |
| `pvcreate` | 创建 PV |
| `vgcreate` | 创建包含一个或多个 PV 的 VG |
| `lvcreate` | 从 VG 的可用空间创建 LV |
| `pvremove` | 移除 PV |
| `vgremove` | 移除 VG |
| `lvremove` | 移除 LV |
| `vgxtend` |向 VG 添加额外的 PV |
| `vgreduce` | 从 VG 中移除 PV |
| `lvxtend` | 使用 VG 中的空闲空间扩展 LV 的大小 |
| `lvreduce` | 减小 LV 的大小并将空闲空间返回 VG |
| `lvresize` | 执行与 `lvxtend` 和 `lvreduce` 相同的功能 |
| `pvchange` | 修改现有 PV 的设置 |
| `vgchange` | 修改现有 VG 的设置 |
| `lvchange` | 修改现有 LV 的设置 |

# 监控文件系统

在设备上创建文件系统并将其挂载到目录树后，应该定期检查是否存在错误、磁盘空间使用情况和 inode 使用情况。这可以最大限度地减少由于文件系统损坏引起的问题，并降低因磁盘空间不足无法保存文件的概率。

## 磁盘使用情况

有多个文件系统挂载到目录树上。如前所述，文件系统越多，损坏的文件系统对系统正常运行的干扰就越大。相反，更多的文件系统通常意味着每个文件系统的空间越小，因此需要频繁监控，以确保每个文件系统都有足够的空间。除了 `/boot` 和根文件系统外，Linux 管理员在安装期间还创建了 `/home`、`/user` 和 `/var` 文件系统。随着用户存储更多数据，`/home` 文件系统的可用空间会减少；随着向系统添加更多程序，`/var` 文件系统的可用空间也会减少。文件和目录会定期清理。根文件系统是监控中最重要的；它应该包含大量的空闲空间作为操作系统空间。如果根文件系统的可用空间低于 10%，系统可能会出现性能低下的或停止运行。

通过挂载的文件系统监控空闲空间的最简单方法是使用之前讨论的 `df` 命令，并配合 `-h` 将大小限制为人类可读的格式：

```
[root@server1 ~]# df -h
Filesystem Size Avail Use% Mounted
devfs 4.0M 0.4M 0% /dev
tmpfs 2.0G 2.0G 1% /dev/shm
tmpfs 7.8G 1.2M 73% /run
/dev/sda3 5G 8.9G 28% /
8.0G 2.0G 1% /tmp
dev/sda2 974M 150M 757M 17% /boot
/dev/sda1 149M 585M 33% /
tmpfs 392M 392M 1% /run/user/42
tmpfs 392M 392M 1% /run/user/100
/dev/mapper/vg00-data 9.8G 24G 9.3% /data1
/dev/mapper/vg00-data2 8.3G 24K 79% /data2
[root@server1 ~]#
```

从前面的输出中，唯一使用的文件系统是根文件系统 `/`、`/boot`、`/home` 和 `/var` 文件系统；根文件系统上的简单目录增加了监控根文件系统的重要性。根文件系统应该包含大量空闲空间作为操作系统的空间。如果根文件系统的可用空间低于 10%，系统可能会遭受性能下降或停止运行。

要查看挂载文件系统的空闲空间，可以使用以下以下 命令：

```
[root@server1 ~]# du -sh
```

```
[root@server1 ~]# du -sh
```

```
[root@server1 ~]# du -sh
```
