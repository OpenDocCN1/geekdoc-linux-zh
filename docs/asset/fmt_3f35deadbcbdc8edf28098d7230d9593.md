
| Log Cpy%Sync Convert | | | | | | | |

| var-lv | data-vg | -wi-a----- | 20.00g | | | | |

| home-lv | data-vg | -wi-a----- | 40.00g | | | | |

```
[lb@rhel9_bpp ~]$ 格式化并挂载 LV：
[lb@rhel9_bpp ~]$ sudo mkfs.xfs /dev/data-vg/var-lv
[lb@rhel9_bpp ~]$ sudo mkfs.ext4 /dev/data-vg/home-lv
[lb@rhel9_bpp ~]$ sudo mkdir /mnt/newvar /mnt/newhome
[lb@rhel9_bpp ~]$ sudo mount /dev/data-vg/var-lv /mnt/newvar
[lb@rhel9_bpp ~]$ sudo mount /dev/data-vg/home-lv /mnt/newhome
```

```
[lb@rhel9_bpp ~]$ 移动数据并更新 /etc/fstab：
[lb@rhel9_bpp ~]$ sudo rsync -av /var/ /mnt/newvar/
[lb@rhel9_bpp ~]$ sudo rsync /home/ /mnt/newhome
```

```
[lb@rhel9_bpp ~]$ 在切换前验证：
diff -r /var /mnt/newvar
diff -r /home /mnt/newhome
```

```
[lb@rhel9_bpp ~]$ 更新 fstab 并重启：
/dev/data-vg/var-lv /var xfs defaults 0 0
/dev/data-vg/home-lv /home ext4 0 0
[lb@rhel9_bpp ~]$ sudo mount /mnt/newvar /mnt/newhome
sudo mount -a
```

```
[lb@rhel9_bpp ~]$ 为 /var 卷创建 LVM 快照：
[lb@rhel9_bpp ~]$ sudo lvcreate -s -n var-snapshot -L 5G /dev/data-vg/var-lv
```

```
[lb@rhel9_bpp ~]$ 从 LVM 快照恢复：
[lb@rhel9_bpp ~]$ sudo lvconvert --merge /dev/data-vg/var-snapshot
```

```
[lb@rhel9_bpp ~]$ 删除 LVM 快照：
[lb@rhel9_bpp ~]$ sudo lvremove /dev/data-vg/var-snapshot
```

```
[lb@rhel9_bpp ~]$ 扩展卷：例如 /var 中的数据库需要更多空间：
[lb@rhel9_bpp ~]$ sudo lxtend -L +10G /dev/data-vg/var-lv
[lb@rhel9_bpp ~]$ sudo xfs_growfs /var
```

# 适用于管理员的 Red Hat Linux 9

- 扩展卷以使用所有剩余空间：

`[lb@rhel9_bpp ~]$ sudo lxtend -l +100%FREE /dev/data-vg/var-lv`

`[lb@rhel9_bpp ~]$ sudo xfs_growfs /var`

- 监控 LVM：

`[lb@rhel9_bpp ~]$ sudo vgdisplay`

`[lb@rhel9_bpp ~]$ sudo lvdisplay`

`[lb@rhel9_bpp ~]$ sudo pvsdisplay`

- 更好的视图

`[lb@rhel9_bpp ~]$ sudo lvs -o +devices`

| LV | VG | Attr | LSize | Pool | Origin | Data% | Meta% | Move | Log %Sync Convert | Devices |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| var-lv | data-vg | -wi-a----- | 30.00g | | | | | | /dev/sdb2(0) |

| home-lv | data-vg | -wi-a----- | 40.00g | | | | | | /dev/sdb2(1024),dev/sdc(0) |

| swap-lv | data-vg | -wi-a----- | 10.00g | | | | | | /dev/sdb2(11264) |

| root-lv | rhel-vg | -wi-a----- | 34.60g | | | | | | /dev/sda3(0) |

| swap-lv | rhel-vg | -wi-a----- | 3.90g | | | | | | /dev/sda3(8847) |

| archive-lv | backup-vg | -wi-a----- | <64.30g | | | | | | /dev/sdc2(1024) |

在本教程中，我们利用了 RHEL 9 中 LVM 的力量创建一个灵活且健壮的存储设置。LVM 在物理磁盘和文件系统之间引入了抽象层：

字体 PVs：原始磁盘或分区。

- VGs：PV 池，存储桶。

- LVs：从 VG 中划分出的虚拟分区。

这种抽象提供了许多益处：

- 灵活性：我们轻松地创建了 `/var` 和 `/home` 卷，而不必担心物理分区边界。当 `/var` 需要更多空间时，我们动态扩展了它而不会影响 `/home`。

- 性能：通过跨两个 PV（在 `data-vg` 和 `backup-vg` 中）划分 `home-lv`，我们提高了 I/O 性能。每个读写操作都可以同时利用两个磁盘。

## 处理网络、文件和存储服务

- 安全性：LVM 快照是一个游戏规则。在更新 `/var` 之前，我们创建了快照。如果出现问题，可以使用 `lvconvert` 快速恢复。这对于系统更新、应用程序升级或任何风险操作都非常有价值。

- 效率：通过精配置（未显示），你可以过度分区。例如，你可以在 50 GB 的 VG 上创建一个 100 GB 的卷，它将随着数据的增加而增长。这对于希望大量分配但节省实际磁盘空间的环境非常好。

- 迁移：更换旧磁盘？将新磁盘加入 VG，镜像数据，然后删除旧磁盘——这一切无需停机。

RHEL 9 中的 LVM 不仅仅是一个工具，它是一种存储哲学。它鼓励以抽象、动态的术语进行思考，不再受限于物理磁盘。

## 教程 #64：管理远程 iSCSI 存储

在你的分布式环境中，存储通常位于中心位置，远离你使用的服务器。互联网小型计算机接口 (`iSCSI`) 是一种强大的协议，允许服务器像访问本地存储器一样访问远程存储。在本教程中，我们将配置 RHEL 9 管理远程 iSCSI 存储，展示了其对网络附加存储解决方案的健壮支持。

首先，让我们安装必要的包：

```
$ [lb@rhel9_bp]$ sudo dnf install iscsi-initiator-utils
```

# 面系统管理员的 Red Hat Enterprise Linux 9

正在更新订阅存储库。

上次元数据过期检查：2024年6月4日 11:30:15，0:15:29 之前。

依赖关系已解析。

| 软件包 | 版本 | 存储库 | 大小 |

|---|---|---|---|

| scsi-initiator-utils | x86_64 6.2.1.4.el9 | rhel-9-appstream | 491 k |

正在安装：

1 个软件包

总下载大小：491 k

是否确认？ [y/N]: y

已完成！

此软件包提供了 iSCSI 启动器工具，使我们的 RHEL 9 系统能够连接到 iSCSI 目标。

现在让我们假设有一个 iSCSI 目标服务器（我们将其命名为 `storage.example.com`），它提供了多个逻辑单元号（LUN）。首先，我们将发现可用的目标：

```
$@rhel9_bpp ~$ sudo scsiadm --mode discover --type sendarget
--portal storage.example.com
192.168.50.100:3260,1 iqn.2024-06.com.example.storage:array1
192.168.50.100:3260,1 iqn.2024-06.com.example.storage:array1:lun1
192.168.50.100:3260,1 iqn.2024-06.com.example.storage:array1:lun2
192.168.50.100:3260,1 iqn.2024-06.com.example.storage:array1:lun3
```

太棒了！服务器有三个可用的 LUN。让我们进行身份验证并连接到它们：
