
```
# lvrename /dev/vg_group01/lv00 /dev/vg_group01/SecretData
Renamed "lv00" to "SecretData" in volume group "vg_group01"
```

# 第 9 步。

通过以下命令验证：

```
# lvdisplay vg_group01
-- Logical volume --
LV Name                 /dev/vg_group01/SecretData
VG Name                 vg_group01
VG UUID                 mk9d3-3q7-ypbC-I8Gh-V93d-4NE6s
LV Write Access         read/write
LV Status               available
# open                  0
Size                    2.93 GiB
```

## 调整 LVM 分区的大小

LVM 最强大的特性是，您可以缩小或扩展逻辑卷和卷组。如果某个逻辑卷或卷组的空间不足，可以向卷组添加另一个物理卷，并扩展逻辑卷以提供更多空间。

> 考试提示

当您调整一个已包含格式化文件系统的卷大时，您需要将文件系统扩展到新产生的空间中。我们将在第 4 章“文件系统等”中讨论扩展文件系统，但如果在考试中遇到这种情况，请务必记在心中。

要扩展逻辑卷，请使用 `lxtend` 命令。

第 1 步。为 `SecretData` 逻辑卷添加 2GB：

```
# lxtend -L +2000 /dev/vg_group01/SecretData
Extending logical volume SecretData to 4.88 GB
Logical volume SecretData successfully resized
```

第 2 步。您也可以指定新大小而不是使用 `+` 号来增加：

```
# lxtend -L 6000 /dev/vg_group01/SecretData
Extending logical volume SecretData to 5.86 GB
Logical volume SecretData successfully resized
```

第 3 步。上述任一命令的结果都是相同的。作为第三种替代方案，您还可以使用 `lresize` 命令：

```
# lresize -L 7000 /dev/vg_group01/SecretData
Extending logical volume SecretData to 6.44 GB
Logical volume SecretData successfully resized
```

第 4 步。使用以下命令验证更改：

```
# lvdisplay vg_group01
Using logical volume(s) on command line
-- /dev/vg_group01/SecretData
LV Name vg_group01
VG Name UUID mk9dJm-7typbc-csks-I8Gh-9V3d-4NE6s
LV Write Access read/write
LV Status available
# open 0
LV Size 6.84 GB
Current LE 1750
```

假设您想添加一个新的物理卷，以便扩展逻辑卷。第 5 步。创建一个新的物理卷：

```
# pvcreate /dev/sdb
```

第 6 步。扩展卷组：

```
# vgxtend vg_group01 /dev/sdb
```

第 7 步。现在查看增加后的卷组的详情：

```
# vgdisplay -v vg_group01
Using volume group(s) on command line
-- Volume group --
VG Name vg_group01
System ID lvm2
Format 2
Metadata Areas 1
Metadata Sequence No 2
VG Access read/write
VG Status resizable
MAX LV 0
Cur LV 1
Open LV 0
Max PV 2
Cur PV 2
Act PV 2
VG Size 8.00 GiB
```

| PE Size | Total PE |
| :--- | :--- |
| 4.00 MiB | 2047 |
| 2.93 GiB | 750 |
| 2.07 GiB | 1297 |
| 2.93 GiB | 150 |

# Red Hat® 考试 96 实战指南：RHCSA™ 和 RHCE® 认证与实验手册

| 元数据序列号 | 12 |
| :--- | :--- |
| VG 访问 | 读/写 |
| VG 状态 | 可调整 |
| MAX LV | 0 |
| Cur LV | 1 |
| Open LV | 0 |
| Max PV | 0 |
| Cur PV | 1 |
| Act PV | 1 |
| VG Size | 8.0 GiB |
| PE Size | 4.00 MiB |
| Total PE | 2047 |
| 已分配 PE / 大小 | 500 / 1.95 GiB |
| 空闲 PE / 大小 | 1547 / 6.04 GiB |
| VG UUID | IvjXga-889Y-1vCC-azRt-pszL-PeWR-E5zath |

## 数据迁移

假设你有一个旧驱动器并想从系统中移除。在具有普通分区的系统上，你必须在磁盘离线时将所有数据从一块磁盘复制到另一块磁盘（文件锁除外）。LVM 让这一切变得简单，因为你可以将数据从一个磁盘迁移到另一个磁盘，即使在磁盘在线时也是如此！当你需要更换磁盘时，此功能非常有用。如果你因为 `/dev/hdb` 故障而替换它，可以使用 `pvmove` 命令将物理区（实际上就是你的数据）迁移到另一个物理卷（`/dev/hdc`）。由于你在上一节中从卷组中移除了 `/dev/hdc`，你需要将其添加回来。

**步骤 1.** 验证 `vg_group01` 卷组内有两个物理卷：

```
# vgdisplay -v vg_group01
Using volume group(s) on command line
Finding volume group 'vg_group01'
- Volume group -- vg_group01
VG Name
System ID lvm2
Format
Metadata Areas
Metadata Sequence No | 14
VG Access | read/write
VG Status | resizable
MAX LV | 0
Cur LV | 2
Open LV | 0
Max PV | 0 |
Cur LV | 2
Act PV | 2
VG Size | 15.99 MiB
PE Size | 4.00 MiB
Total PE | 4094
Alloc PE / Size | 1750 / 6.84 GiB
Free PE / Size | 2344 / 9.16 GiB
VG UUID | IvjXga-889Y-1vCC-azRt-pszL-PeWR-E5zath
```

+ - 逻辑卷 -

# 第 3 章：磁盘与分区 97

| LV 名称 | /dev/vg_group01/SecretData |
| :--- | :--- |
| VG 名称 | vg_group01 |
| LV UUID | mk9DJM-3qqt7-ypbC-nsks-I8Gh-9V3d-4BNE6s |
| LV Write Access | 读/写 |
| LV Status | available |
| # open | 0 |
| LV Size | 1.95 GiB |
| Current LE | 500 |
| Segments | 1 |
| Allocation | inherit |
| Read ahead sectors | auto |
| - currently set to | 256 |
| Block device | 253:2 |
| PV 名称 | /dev/sdb |
| PV UUID | B0K2Gh-0UF4-gphE-MLI3-RFXH-HEP9-9FMba9 |
| PV Status | allocatable |
| Total PE / Free PE | 2047 / 297 |

**步骤 2.** 因为只有一个物理磁盘，你需要将 `/dev/sdc` 添加回卷组：

```
# vgextend vg_group01 /dev/sdc
Volume group "vg_group01" successfully extended
```

**步骤 3.** 同样，创建一个逻辑卷来存放修改后的数据：
