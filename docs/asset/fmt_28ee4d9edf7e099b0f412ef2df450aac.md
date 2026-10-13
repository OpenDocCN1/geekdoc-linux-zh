
| Total PE | 0 |
| Free PE | 0 |
| Allocated PE | 0 |
| PV UUID | EQ7ElZ-WiGK-Z0m5-5gSN-gP95-MFSk-pKyTvS |

### 创建卷组 (VG)

`vgcreate VG_name PV_name`

```
[root@redhat1 ~]# vgcreate vg01 /dev/sdb3
Volume group "vg01" successfully created
```

### 创建新的逻辑卷(LV)

`lvcreate -n LV_name -L size VG_name`

```
[root@redhat1 ~]# lvcreate -n lv01 -L 1G vg01
Logical volume "lv01" created
```

### 在 LV 上创建文件系统

`mkfs -t ext4 /dev/VG_name/LV_name`

```
[root@redhat1 ~]# mkfs -t ext4 /dev/vg01/lv01
```

### 将条目添加到 /etc/fstab 以在启动时自动挂载文件系统

```
UUID=6acaa400-0cd3-4708-ba05-5541139ee830e /newfs ext4 defaults 1 2
```

挂载文件系统
`mount -a`

### PV 命令

| 说明 | 命令 |
| :--- | :--- |
| 显示 PV 属性 | `pvdisplay` |
| 显示所有 LVM 块设备 | `pvscan` |
| 防止在 PV 上分配 PE | `pvchange -xn /dev/PV_name` |
| 移除 PV | `pvremove /dev/PV_name` |

### 卷组 (VG) 命令

| 说明 | 命令 |
| :--- | :--- |
| 显示 VG 属性 | `vgdisplay` |
| 显示 VG 列表 | `vgs` |
| 将 PV 添加到 VG | `vgextend vgname /dev/PV_name` |
| 示例 | `# vgextend vg01 /dev/sdb5` |
| 从 VG 移除 PV | `vgreduce vg1 /dev/PV_name` |
| 示例 | `# vgreduce vg01 /dev/sdb5` |
| 激活 VG | `vgchange -ay VG_name` |
| 取消 VG | `vgchange -an VG_name` |
| 移除 VG | `vgremove VG_name` |

|  | 示例 |
| :--- | :--- |
|  | `vgremove /dev/vg02` |
| 重建 VG 目录 | `vgmknodes` |

### 将卷组从一个系统移动到另一个系统

在当前运行 VG 的第一个系统上，卸载所有属于该 VG 的文件系统

```
umount /newfs
```

使用 `vgchange -an VG_name` 命令停用 VG

```
[root@redhat1 /]# vgchange -an sharedvg
```

使用 `vgexport VG_name` 命令导出 VG

```
[root@redhat1 /]# vgexport sharedvg
```

将硬盘连接到新系统后，使用 `vgimport VG_name` 命令导入 VG

```
[root@redhat2 ~]# vgimport sharedvg
```

使用 `vgchange -ay VG_name` 激活 VG

```
[root@redhat2 ~]# vgchange -ay sharedvg
```

挂载 VG 文件系统

```
[root@redhat2 ~]# mount

/dev/sharedvg/sharedlv/mnt
```

检查文件系统内容

```
[root@redhat2 ~]# cd /mnt
```

### 扩展文件系统

检查当前 FS 大小

```
df -h /fsname
```

| /dev/mapper/vg01-lv01 | 1008M 34M |
| 924M 4% /newfs |

检查你是否有足够的空闲空间，即想要扩展 FS 的 LV 所在的 VG 是否有空 PE。

```
[root@redhat1 ~]# vgdisplay vg01

--- Volume group ---

VG Name vg01

System ID  

Format lvm2

Metadata Areas 1
```

| 元数据序列号 | 5 |
| :--- | :--- |
| VG Access | read/write |
| VG Status | resizable |
| MAX LV | 0 |
| Cur LV | 1 |
| Open LV | 1 |
| Max PV | 0 |
| Cur PV | 1 |
| Act PV | 1 |
| VG Size | 5.00 GiB |
| PE Size | 4.00 MiB |
| Total PE | 1280 |
| Alloc PE / Size | 256 / 1.00 GiB |
| Free PE / Size | 1024 / 4.00 GiB |
| VG UUID | EXKfhW-MfE4-4ZtU-uQuM-v9e4-AJ9k-Uo6z4B |

### 扩展逻辑卷

`lvextend -L size /dev/vgname/lvname`

```
[root@redhat1 ~]# lvextend -L+200M /dev/vg01/lv01

Extending logical volume lv01 to 1.20 GiB

Logical volume lv01 successfully resized
```

### 使用 resize2fs 扩展文件系统

`resize2fs -p /dev/vgname/lvname`

```
[root@redhat1 ~]# resize2fs -p /dev/mapper/vg01-lv01
```

### 检查 FS 大小

`df -h /fsname`

| /dev/mapper/vg01-lv01 | 1.2G 34M 1.1G 3% | /newfs |

### 缩小文件系统

检查当前 FS 大小

```
df -h /fs_name
```

`/dev/mapper/vg01-lv01  1.2G 34M 1.1G`
`3% /newfs`

卸载文件系统

```
umount /fs_name
```

```
[root@redhat1 ~]# umount /fs_name
```

检查文件系统

```
[root@redhat1 ~]# e2fsck -f /dev/mapper/vg01-lv1
```

使用 `resize2fs -p /dev/vgname/lvname` 调整 FS

```
[root@redhat1 ~]# resize2fs -p /dev/mapper/vg01-lv01 1G
```

在此示例中，将 FS 大小设为 GB，现在缩小 LV 大小，留出一些额外空间使用 `lvreduce -L size /dev/vgname/lvname`

```
[root@redhat1 ~]# lvreduce -L 1G /dev/mapper/vg01-lv01
```

挂载文件系统

```
[root@redhat1 ~]# mount /newfs
```

### LVM 快照

LVM 快照是逻辑卷的时间点拷贝。快照提供了原始卷的静态视图。一旦拍摄了快照，我们就可以使用此快照进行备份，因为快照是静态的，不会像动态的原始卷那样变化。快照卷应该足够存储快照拍摄后发生变化的数据。

### 创建快照 LV

检查想要创建快照的文件系统名称和大小

```
[root@redhat1 /]# df -hT /newfs

Filesystem      Type Size Avail Use% Mounted on

/dev/mapper/vg01-lv01 ext4 1.2G 34M 1.1G 3% /newfs
```

使用 `vgchange -an VG_name` 命令停用 VG

```
[root@redhat1 /]# vgchange -an sharedvg
```

使用 `vgexport VG_name` 命令导出 VG

```
[root@redhat1 /]# vgexport sharedvg
```

在将硬盘连接到新系统后，使用 `vgimport VG_name` 命令导入 VG

```
[root@redhat2 ~]# vgimport sharedvg
```

使用 `vgchange -ay VG_name` 激活 VG
