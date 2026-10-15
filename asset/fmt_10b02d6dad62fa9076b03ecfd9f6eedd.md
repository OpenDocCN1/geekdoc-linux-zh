
提供条带数量。这等于分散逻辑卷的物理卷数量。在创建 RAID 4/5/6 逻辑卷时，用于校验所需的额外设备已完全考虑在内。使用 `-i3` 将为条带逻辑卷使用 3 个设备，为 RAID 4/5 使用 4 个设备，为 RAID 6 使用 5 个设备。或者，如果省略 `-i` 参数，RAID 4/5/6 将对卷组中的所有 PV 或指定的所有 PV 进行分散。

## --stripesSize

提供条带粒度的千字节数。为了符合 LVM 格式的元数据，条带大小必须是 2^n（n = 2 到 9）。对于元数据 LVM 格式，条带大小可以是 2 的更大幂，但不能超过物理范围区大小。

## --thin

创建精简池或精简逻辑卷或两者都有。指定可选参数 `--size` 或 `--extents virtualsize` 将导致从精简池卷创建精简逻辑卷。指定两个参数将导致使用该池创建精简池和精简卷。使用 `lvthin(7)` 获取更多关于精简配置的支持信息。精简配置需要 device mapper 内核版本 3.2 或更高。

## --thinpoolThinPoolLogicalVolume{Name|Path}

指定精简池卷的名称。另一种方法是在卷组参数后指定池名称。

## --type SegmentType

创建一个指定段类型的逻辑卷。支持的类型有：

`cache`, `cache-pool`, `error`, `linear`, `mirror`, `raid1`, `raid4`, `raid5_la`, `raid5_ls=(raid5)`, `raid5_ra`, `raid5_rs`, `raid6_nr`, `raid6_zr=(raid6)`, `raid10`, `snapshot`, `striped`, `thin-pool(or zero)`。段类型具有命令行别名以启用其使用。当未显式指定类型时，将从选项组合中选择：`-h|--cache--cachepool(cache or cachepool)`, `-T|--thin--thin-pool(thin or thinpool)`, `-m|--mirrors(raid1 or mirror)`, `-s|--snapshot|-V|--virtualSizeVirtualSize(bSSkkmMgGtTtpPeE)`

创建一个精简配置的设备或指定大小的设备（默认为 MiB）。参见 `lvm.conf(5)` 设置 `global/sparse_type_default` 以配置稀疏段类型。参见 `lvthin(7)` 获取更多关于配置支持的信息。写入稀疏快照的任何内容在从其读取时都会返回。从设备的其他区域读取将返回零块。虚拟快照通过使用零目标创建一个具有所请求大小的隐藏虚拟设备来实现。该设备使用 `_origin` 后缀。注意：使用稀疏快照对于较大的设备尺寸（GiB）是高效的，在这种情况下应使用精简配置。

## -W,--wipesignatures(y|n)

控制在新建的逻辑卷上擦除检测到的签名。如果未指定此选项，默认每次执行置零（`-Z--zero`）时都会擦除签名。此默认行为可以通过 `lvm.conf(5)` 中的 `allocation/wipe_signatures_when_zeroing_new_ls` 设置来控制。如果 blkid 擦除在使用 `lvm.conf(5)` 中的 `allocation/use_blkid_wiping` 设置且 LVM2 编译了 blkid 擦除支持，则使用 `blkid(8)` 库来检测签名（使用 `blkid -k` 命令列出识别的签名）。否则，使用原生 LVM2 代码检测签名（仅在此情况下会检测 MD RAID、swap 和 LUKS 签名）。如果仅设置了标志，则逻辑卷不会被擦除。

## -Z,--zero(y|n)

控制新建逻辑卷前 4KiB 数据置零。默认为 yes。快照 COW 卷始终置零。如果仅设置了标志，则逻辑卷不会被置零。

警告：尝试挂载未置零的逻辑卷可能会导致系统挂起。

## EXAMPLES

在名为 `vg00` 的卷组创建一个具有 3 个条带、条带大小为 8KiB 且大小为 100MiB 的条带逻辑卷。逻辑卷的名称将由 `lvcreate` 选择：

```
lvcreate -i 3 -I 8 -L 100M vg00
```

创建一个具有 2 个侧、可用大小为 500 MiB 的镜像逻辑卷。此操作需要 3 个设备（或选项 `--alloc anywhere`）——两个用于镜像设备，一个用于日志：

```
lvcreate -m1 -L 500M vg00
```

创建一个具有 2 个侧、可用大小为 500 MiB 的镜像逻辑卷。此操作需要 2 个设备——日志是“内存中”的：

```
lvcreate -m1--mirrorlog -L 500M vg00
```

创建一个名为“`vg00/snap`”的快照逻辑卷，在快照创建时访问名为“`vg00/lvol1`”的原始逻辑卷的内容。如果原始逻辑卷包含文件系统，你可以将快照逻辑卷挂载到任意目录以访问文件系统内容运行备份，同时原始文件系统继续。

```
lvcreate -s vg00/lvol1 --name vg00/snap
```

创建一个名为“`vg00/snap`”的快照逻辑卷，在快照创建时访问名为“`vg00/lvol1`”的原始逻辑卷的内容。如果原始逻辑卷包含文件系统，你可以将快照逻辑卷挂载到任意目录以访问文件系统内容运行备份，同时原始文件系统继续。

```
lvcreate -L 20% -s vg00/lvol1 --name snap
```

创建一个精简配置的设备或指定大小的设备（默认为 MiB）。参见 `lvm.conf(5)` 设置 `global/sparse_type_default` 以配置稀疏段类型。

创建一个名为“`vg00/snap`”的快照逻辑卷，在快照创建时访问名为“`vg00/lvol1`”的原始逻辑卷的内容。如果原始逻辑卷包含文件系统，你可以将快照逻辑卷挂载到任意目录以访问文件系统内容运行备份，同时原始文件系统继续。

```
lvcreate -s vg00/thinvol --name snap
```

另参见

`lvm(8)`, `lvm.conf(5)`, `lvmcache(7)`, `lvmthin(7)`, `lvconvert(8)`, `lvchange(8)`, `lvextend(8)`, `lvreduce(8)`, `lvremove(8)`, `lvrename(8)`, `lvs(8)`, `lvscan(8)`, `vgcreate(8)`, `blkid(8)`

# LVDISPLAY

## 名称

`lvdisplay` – 显示逻辑卷的属性

## 概要览

```
lvdisplay [-a|--all] [-c|--colon] [--commandprofile ProfileName] [-d|--debug] [-h|?|--help] [--ignorelockingfailure] [--ignoreskipcluster] [--maps] [--nosuffix] [-P|--partial] [-S|--select Selection] [--units hHbBsSkKmMgGtTpPeE] [-v|--verbose] [--version] [VolumeGroupNameLogicalVolume{Name|Path} ...]
```

```
lvdisplay -C|--columns [--aligned] [--binary] [-a|--all] [--commandprofile ProfileName] [-d|--debug] [-h|?|--help] [--ignorelockingfailure] [--ignoreskipcluster] [--headings] [--nosuffix] [-o|--options] [+|Field,Field...]] [-O|--sort] [+|Key1[+|Key2...]] [-P|--partial] [--segments] [-S|--select Selection] [--separator Separator] [--unbuffered] [--units hHbBsSkKmMgGtTpPeE] [-v|--verbose] [--version] [VolumeGroupNameLogicalVolume{Name|Path} ...]
```

`lvdisplay` 允许你查看逻辑卷的属性，如大小、读/写状态、快照信息等。

`lvs(8)` 是替代方案，以 ps(1) 的风格提供相同的信息。相比 `lvdisplay`，推荐使用 `lvs(8)`。

## 选项

常用选项参见 `lvm(8)`，使用 `--columns--all` 提供的选项参见 `lvs`。

- `-a` 在输出中包含关于内部逻辑卷的信息，这些卷是普通访问逻辑卷的组成部分（例如镜像），但无法独立访问（例如不可挂载）。例如，在使用 `lvcreate -ml --mirrorlog disk` 创建镜像后，此选项将显示三个带有后缀 `imageage_0`、`imageage_1` 和 `mlog` 的内部逻辑卷。

- `-columns` 以列输出，等同于 `lvs(8)`。列出的选项与 `lvs(8)` 中分隔的选项相同。

- `-c, colon` 生成用冒号分隔的输出，以便在脚本或程序中进行解析。注意：`lvs(8)` 对输出提供了更多的控制。其取值为：逻辑卷名称 | 卷组名称 | 逻辑卷访问权限 | 逻辑卷状态 | 内部卷编号 | 以扇区为单位的逻辑卷打开计数 | 与逻辑卷关联的逻辑区 | 逻辑卷的逻辑区 | 逻辑卷分配策略 | 逻辑卷预读扇区 | 逻辑卷设备 | 逻辑卷次设备号

- `-m,maps` 显示逻辑区到物理卷和物理区的映射。要将物理区映射到逻辑区，请使用：`pvs --segments -o+lv_name,seg_start_pe,segtype`

## 示例

显示该逻辑卷的属性。如果为此原始逻辑卷创建了快照逻辑卷，此命令将显示所有快照逻辑卷及其状态（活动或非活动）：

```
lvdisplay -v vg00/lvol2
```

显示此快照逻辑卷的属性以及它关联的原始逻辑卷：

```
lvdisplay vg00/snapshot
```

## 另参见

`lvm(8)`, `lvcreate(8)`, `lvs(8)`, `lvscan(8)`, `pvs(8)`

# LVEXTEND

## 名称

`lvextend` – 扩展逻辑卷的大小

## 概要览

```
lvextend [--alloc AllocationPolicy] [-A|--autobackup {yn}] [--commandprofile ProfileName] [-d|--debug] [-h|--help] [-f|--force] [-i|--stripes Stripes [-I|--stripe]] [-L|--extents [+LogicalExtentsNumber[%{VG|LV|PVS|FREE|ORIGIN}] -L|--size[+]LogicalVolumeSize[bBsSkKmMgGtptpPeE]] [-n|--nofckk] [-r|--noudevsync|--resizefs] [--use-policies] [-t|--test] [-v|--verbose] LogicalVolumePath[PhysicalVolumePath[:PE[-PE]]...
```

`lvextend` 允许你扩展逻辑卷的大小。支持扩展快照逻辑卷（创建快照的信息参见 `lvcreate(8)`）。但要更改镜像逻辑卷中的副本数量，请使用 `lvconvert(8)`。

## 选项

常用选项参见 `lvm(8)`。

- `-force` 无需提示直接进行大小扩展。

- `-size[+]LogicalVolumeSize[bBsSkKmMgGtptpPeE]` 允许你扩展逻辑卷的大小。

- `-stripes` 指定条带数量。

- `-I|--stripe` 指定条带数量。

- `-L|--extents [+LogicalExtentsNumber[%{VG|LV|PVS|FREE|ORIGIN}] -L|--size[+]LogicalVolumeSize[bBsSkKmMgGtptpPeE]]` 允许扩展逻辑卷。

- `-n|--nofckk` 在扩展文件系统时不执行 fsck。

- `-r|--noudevsync|--resizefs` 随逻辑卷调整底层文件系统的大小。

- `--use-policies` 根据策略调整逻辑卷的大小。

- `-t|--test` 执行空运行。

- `-v|--verbose` 详细输出。

## 示例

将物理卷 `/dev/sdk3` 逻辑卷 `vg01/lvol10` 扩展 54MiB。这只有在 `/dev/sdk3` 是卷组 `vg01` 成员且其中有空闲区的情况下可行：

```
lvextend -L+54 /vg01/lvol10 /dev/sdk3
```

根据物理卷 `/dev/sdk3` 的可用空间扩展逻辑卷 `vg01/lvol01`。这等同于在命令行中指定 `-100%PVS`：

```
lvextend /vg01/lvol01 /dev/sdk3
```

使用物理区 `/dev/sda-9` 和 `/dev/sdb-9` 将逻辑卷 `vg01/lvol01` 扩展 16MiB：

```
lvextend -L+16M vg01/lvol01 /dev/sda-9 /dev/sdb-9
```

# 说明

`lvmconfig` 根据 LVM 配置树生成格式化后的输出。该命令在发布 2.02.119 版本中添加，并有一个完全相同的长形式 `lvm dumpconfig`。

## 选项

- `-f`, `--file filename`

将输出发送到名为‘`filename`’的文件。

- `-l`, `--list`

列出带有摘要性注释的配置设置。这等同于使用 `lvmconfig --type list --summary`。

`--type {current|default|diff|full|missing|new}profilable|profilable-command|profilable-metadata`

选择要显示的配置类型。所显示的配置设置将根据所选的类型分配默认值或当前使用的值。如果未选择类型，则默认使用 `--type current`。每当带有默认值的配置设置被注释掉时，即意味着该设置没有定义任何具体的默认值。输出可以保存并用作适当的 `lvm.conf(5)` 文件。

`current`

显示当前的 `lvm.conf` 配置，并合并了已使用的任何标签配置（tag config）。有关关于 LVM 配置方法的更多信息，请参阅 `lvm.conf(5)`。

`default`

显示所有分配了默认值的配置设置。

`diff`

显示所有值与默认值不同的配置设置。每个配置设置分配的值为当前使用的值。这实际上是极简的 LVM 配置，可以在不更改当前配置行为的情况下使用。

`full`
