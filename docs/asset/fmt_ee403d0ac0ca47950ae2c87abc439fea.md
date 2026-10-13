
```
# mkswap /newswap
Setting up swapspace version 1, size = 1.9 GiB (2047995904 bytes)
no label, UUID=28d314e9-492f-46f8-bdcf-3a734c4426db5
```

交换文件创建并配置后，可以使用 `swapon` 实用程序实时将其添加到系统中：

```
# swapon /newswap
```

重新运行 `swapon` 现在应报告新文件现在正被用作交换：

```
# swapon
NAME    TYPE    SIZE USED PRIO
/dev/dm-1 partition 3.7G 1M -2
/newswap file    1.9G 0B -3
```

交换空间可以通过以下方式使用 `swapoff` 实用程序动态删除：

```
# swapoff /newswap
```

最后，通过添加以下行修改 `/etc/fstab` 文件，以在系统启动时自动添加新的交换：

`/newswap  swap  swap  defaults 0 0`

### 33.5 将交换添加为分区

作为将文件指定为交换空间的替代方案，整个磁盘分区也可以指定为交换。实现此目的的步骤与添加交换文件相同。在将分区分配给交换之前，请确保相应文件系统上的任何现有数据已备份或不再需要，并且文件系统已卸载。

假设例如磁盘驱动器上存在一个由 `/dev/sdb1` 表示的分区，第一步将是使用 `mkswap` 实用程序再次将其转换为交换分区：

```
# mkswap /dev/sdb1
Setting up swapspace version 1, size = 14.5 GiB (15524163584 bytes)
no label, UUID=306b7fee-eb20-4679-9f14-f94548683557
```

接下来，将新分区添加到系统交换中并验证它是否确实已添加：

```
# swapon /dev/sdb1
[root@demoser ver ~]# swapon
NAME      TYPE      SIZE USED PRIO
/dev/dm-1 partition 3.7G 996K  -2
/dev/sdb1 partition 14.5G 0B   -3
```

再次，`/etc/fstab` 文件可以按如下方式修改，以便在启动时自动添加交换分区：

`/dev/sdb1  swap  swap  defaults 0 0`

### 33.6 向 RHEL 9 LVM 交换卷添加空间

在使用逻辑卷管理的系统上，除了通过文件或磁盘分区添加交换之外，还可以选择扩展用于交换空间的逻辑卷。

第一步是使用 `lvdisplay` 实用程序识别当前可用的交换量以及用于交换空间的卷组和逻辑卷（有关 LVM 的更多信息，请参阅题为“将新磁盘添加到 RHEL 9 卷组和逻辑卷”的章节）：

```
# lvdisplay
--- Logical volume ---
LV Path              /dev/rhel/swap00
LV Name              swap00
VG Name              rhel
LV UUID              EbOScj-1qXw-bB9d-LU61-ZjdC-L7u5-Uhj8De
LV Write Access      read/write
LV Creation host, time demoserver, 2023-04-12 09:34:29 -0400
LV Status            available
# open                2
LV Size              3.75 GiB
Current LE           960
```

## 添加和管理 RHEL 9 交换空间

|  |  |

|---|---|

| 段 | 1 |

| 分配 | inherit |

| 预读扇区 | auto |

| - 当前设置为 | 256 |

| 块设备 | 253:1 |

显然，交换空间位于名为 `swap00` 的逻辑卷上，该逻辑卷属于名为 `rhel` 的卷组。下一步是验证卷组上是否有可分配给交换卷的可用空间：

```
# vgs
  VG   #PV #LV #SN Attr   VSize   VFree
  rhel   2   3   0 wz--n- 197.66g <22.00g
```

如果可用空间足以满足额外的交换需求，请关闭交换并扩展交换逻辑卷，以使用尽可能多的可用空间来满足系统的交换需求：

```
# swapoff /dev/rhel/swap
# lvextend -L+8GB /dev/rhel/swap
  Logical volume rhel/swap successfully resized.
```

接下来，重新格式化交换卷并重新启用交换：

```
# mkswap /dev/rhel/swap
mkswap: /dev/rhel/swap: warning: wiping old swap signature.
Setting up swapspace version 1, size = 12 GiB (12754874368 bytes)
no label, UUID=241a4818-e51c-4b8c-9bc9-1697fc2ce26e

# swapon /dev/rhel/swap
```

完成更改后，检查交换空间是否已增加：

```
# swapon
NAME      TYPE      SIZE USED PRIO
/dev/dm-1 partition 12G  0B   -2
```

### 33.7 向卷组添加交换空间

在上一节中，我们扩展了交换逻辑卷以使用卷组中已有的空间。如果卷组中没有可用空间，则必须在扩展交换之前添加空间。

首先检查卷组的状态：

```
# vgs
  VG     #PV #LV #SN Attr   VSize   VFree
  rhel     1   3   0 wz--n- <297.09g     0
```

上述输出表明卷组内部没有可用空间。但是，假设系统需要向交换空间添加 14 GB。这将需要向卷组添加更多空间。对于本示例，将假设有一个大小为 16 GB 且由 `/dev/sdb` 表示的磁盘可用于添加到卷组。因此，第一步是使用 `pvcreate` 将此分区转换为物理卷：

```
# pvcreate /dev/sdb
Physical volume "/dev/sdb" successfully created.
```

如果创建失败并出现类似“Device /dev/sdb excluded by a filter”的消息，则可能需要在创建物理卷之前擦除磁盘：

```
# wipefs -a /dev/sdb
/dev/sdb: 8 bytes were erased at offset 0x00000200 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 8 bytes were erased at offset 0x1fffffe00 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 2 bytes were erased at offset 0x000001fe (PMBR): 55 aa
/dev/sdb: calling ioctl to re-read partition table: Success
```

接下来，需要扩展卷组以使用此额外的物理卷：

```
# vgextend rhel /dev/sdb
Volume group "rhel" successfully extended
```

在这一点上，`vgs` 命令应报告 `/dev/sdb` 的空间已添加到卷组：

```
# vgs
VG #PV #LV #SN Attr VSize VFree
rhel 2 3 0 wz--n- 311.54g <14.46g
```

现在卷组中已有额外空间可用，可以扩展交换逻辑卷以利用该空间。但首先，使用 `swapoff` 实用程序关闭交换：

```
# swapoff /dev/rhel/swap00
```

接下来，扩展逻辑卷以使用新空间：

```
# lvextend -L+14GB /dev/rhel/swap00
Size of logical volume rhel/swap00 changed from 3.75 GiB (960 extents) to 17.75 GiB (4544 extents).
Logical volume rhel/swap00 successfully resized.
```

在逻辑卷上重新创建交换：
