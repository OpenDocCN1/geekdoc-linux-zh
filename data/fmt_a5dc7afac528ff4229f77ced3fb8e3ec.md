
# lvconvert 用法

```
background] [-f--force] [-i--interval Seconds] [--commandProfile ProfileName
[-h-?]--noudevsync] [-v--verbose] [-y--yes] [--version]
```

`LogicalVolume[Path] [PhysicalVolume[Path]:PE-[PE]]...`

```
lvconvert --split [--commandProfile ProfileName] [-h-?]--help] [--noudevsync
[-v--verbose] SplittableLogicalVolume[NamePath]
```

```
lvconvert --splitcache --uncache [--commandProfile ProfileName] [-h-?]--help]
--noudevsync [-v--verbose] [--version] CacheLogicalVolume[NamePath]
```

```
lvconvert --splitmirrors Images [--nameSplitLogicalVolumeName] [---
trackchanges MirrorLogicalVolume[Path] [--commandProfile ProfileName]
SplittablePhysicalVolume[Path]:PE-[PE]]...
```

```
lvconvert --snapshot [--commandProfile ProfileName] [-h-?]--help] [---
noudevsync] [-v--verbose] [--version] SnapshotLogicalVolume[Path]
```

```
lvconvert --s--snapshot [-cchunkize Size[BBskmG]] [-Z--zero {yn}] [---
commandProfile ProfileName] [-h-?]--help] [--noudevsync] [-v--verbose] [---
version] OriginalLogicalVolume[Path] SnapshotLogicalVolume[Path]
```

```
lvconvert --merge [-b--background] [-i--interval Seconds] [--commandprofile
ProfileName] [-h-?]--help] [-v--verbose] [--version] LogicalVolume[Path]...
```

```
lvconvert --repair [-s--stripes Stripes [-I--stripize StripeSize] [---
commandProfile ProfileName] [-h-?]--help] [-v--verbose] [--version]
LogicalVolume[Path] [PhysicalVolume[Path]...
```

```
lvconvert --type thin[--pool] [-T--thin] [--originate
ExternalOriginLogicalVolume[Name] [--thinpool ThinLogicalVolume[Name|Path]
[-c--chunkize Size[BBskmG]] [--discards
ignorepassdonpassdown] [--poolmetadata
ThinPoolMetadataLogicalVolume[Name|Path] [--poolmetadata
ThinPoolMetadataSize[BBskmG]] [-r--readhead
[ReadAddSectors(auto|one)] [-s--stripes Stripes [-I--stripize StripeSize]] [---
polmetadataspace[yn}] [-Z--zero {yn}] [--commandProfile ProfileName] [--
h--?] [-v--verbose] [--version]
[[ExternalOriginThinLogicalVolume[Name|Path] [PhysicalVolume[Path]:PE
PE]]...
```

```
lvconvert --type cache[--pool] [--cachepool
CachePoolLogicalVolume[Name|Path] [-c--chunkize Size[BBskmGmg]]
[—cachemode {writeback|writethrough}] [—cachepolicy policy] [—cachesettings key=value] [—poolmetadata CachePoolMetadataLogicalVolume{Name|Path} |—poolmetadatasize CachePoolMetadataSize[bBsSkKmMgG]] [—polmetadataspare {y|n}] [—commandprofile ProfileName [-h|-?|--help] [-v|--verbose] [--version] LogicalVolume[Path} [PhysicalVolume[Path]]...
```

## 描述

`lvconvert` 用于更改分段类型（例如线性、镜像、快照）或逻辑卷的特征。它可以添加或移除镜像的冗余镜像，更改逻辑卷的日志类型，将逻辑卷指定为快照。如果指定了物理卷，它会释放这些特定 `PE` 范围的物理段，这些物理段将从镜像中分离。`--split` 分离 `SplittableLogicalVolume`。`--splitcache` 从缓存池中分离 `CacheLogicalVolume`。`--splitmirrors` 指定要分离的冗余镜像数量。

## 选项

参见 `lvm(8)` 获取常用选项。`--cache,--corelog,--merge,--mirror,--mirrors,--repair,--snapshot,--split,--splitcache,--splitnap,--type` 或 `--uncache`。

`-b--background` 在后台运行。

`-c--chunkize Size[BBskmG]` 为快照、缓存池和逻辑卷指定块的大小。

`-cachemode {writeback|writethrough}` 设置缓存模式。

`-cachepolicy policy` 设置缓存策略。

`-cachesettings key=value` 设置缓存设置。

`--corelog` 等同于 `mirrorlog`。

`-commandprofile ProfileName` 设置命令配置。

`--discards ignorepassdonpassdown`（未详，但列为选项）。

`--cache` 是。

`--cachepool CachePoolLogicalVolume[Name|Path]` 指定缓存池。

`--poolmetadata CachePoolMetadataLogicalVolume[Name|Path] |—poolmetadatasize CachePoolMetadataSize[bBsSkKmMgG]` 设置池元数据。

`--polmetadataspare {y|n}` 设置池元数据备用。

`--noudevsync` 禁用设备同步。

`--interval Seconds` 每隔一段时间以百分比报告进度。

`--mirrors Mirrors` 镜像的冗余镜像数量。

`--merge` 将镜像卷合并回线性卷。

`-h--?` 或 `-h|-?|--help` 显示帮助。

`-i--interval Seconds`（重复列表）。

`-n--name` 应用于从镜像分离出的逻辑卷的名称。

`-R--resize MirrorLogRegionSize` 镜像被分为此大小的区域（MB）。

`-repair` 修复卷（未详）。

`-type SegmentType` 指定类型（例如线性、镜像、快照、精简）。

`-v--verbose` 启用更详细的输出。

`--version` 显示版本。

`--split` 分离 `SplittableLogicalVolume`。

`--splitcache` 从缓存池中分离 `CacheLogicalVolume`。

`--splitmirrors` 指定要分离的冗余镜像数量。

`--snapshot` 从组成逻辑卷重建快照。

`--trackchanges` 跟踪 `raid1` 设备的变化以允许合并。

`--uncache` 取消缓存并移除缓存池。

`--zero {yn}` 设置置零选项。

默认单位为千字节（KB）。

对于快照，该值必须是 `4KiB` 到 `512KiB` 之间 2 的幂次方，默认值为 `4`。

对于缓存池（cache pools），该值必须在 `32KiB` 到 `1GiB` 之间，默认值为 `64`。

对于精简池（thin pools），该值必须在 `64KiB` 到 `1GiB` 之间，默认值从 `64` 开始，并向上扩展以适应池元数据大小 `128MiB`（在未指定池元数据大小时如此）。该值必须是 `64KiB` 的倍数。（在 thin target 版本 `1.4` 之前的早期内核要求该值为 2 的幂次方。除非 thin target 版本为 `1.5`，否则不支持非 2 幂值的丢弃（Discards）。）

- `-discards {ignore|nopassdownpassdown}`

指定精简层在传递给物理卷（Physical Volume）时是否处理丢弃操作。目前选项仅支持精简池。默认为透传（passdown）。

- `-Z, --zero {y|n}`

控制快照中前 `4KiB` 数据的置零。如果卷是只读的，快照将不会置零。对于精简池卷，它控制已分配块的置零。注意：分配大型置零块会负面影响性能。

- `-merge`

将快照合并到其源卷，或将从镜像中分出的带有跟踪更改（trackchanges）的 `raid1` 镜像合并回镜像。

要检查您的内核是否支持快照合并功能，请在 `dmset targets` 的输出中查找 `'snapshot-merge'`。如果源卷和快照卷未打开，合并将立即启动。否则，将在源卷或快照卷首次激活且两者都处于激活状态时启动。将快照合并到源卷（例如根文件系统）无法关闭，直到源卷下次激活。当合并开始时，生成的逻辑卷将具有源卷名称、次设备号和 UUID。在合并期间，对源卷的读写操作似乎是定向到正在合并的快照。当合并完成后，合并的快照将被移除。可以在命令行上指定多个快照，或使用 `@tag` 来指定多个要合并到各自源卷的快照。

- `-originExternalOriginVolumeName`

原始逻辑卷的新名称，它将使用 `--thinpool`。如果没有此选项，将生成默认名称 `"lv<n>"`，其中 `<n>` 是 LVM 内部逻辑卷编号。只要该卷被用作外部源，它将是只读的且无法进一步修改。

- `-poolmetadata PoolMetadataLogicalVolume{Name|Path}`

指定缓存池或精简池的元数据逻辑卷。大小应在 `2MiB` 到 `16GiB` 之间。缓存池通过选项 `--cachepool` 指定。精简池通过选项 `--thinpool` 指定。当指定的指定的池已存在时，该池的元数据卷将与给定的 LV 交换交换。在这种情况下，池属性（如块大小或置零）默认会被保留。这对于池元数据的修复或其离线扩容非常有用，因为元数据卷可以作为普通卷供使用 `cache_dump(8)`、`cache_repair(8)`、`cache_restore(8)`、`thin_dump(8)`、`thin_repair(8)` 和 `thin_restore(8)` 等配置工具的用户使用。

- `--poolmetadatase PoolMetadataSize|BsSkKmMgG`

如果池元数据卷未定义，则设置缓存或精简池元数据卷的大小。通过选项 `--cachepool` 或 `--thinpool` 指定池。精简池支持的值范围在 `2MiB` 到 `16GiB` 之间。默认值通过此公式估计（Pool_LV_size / Pool_LV_chunk_size * 64b），单位为兆字节。

- `--poolmetadataspare [yn]`

控制池元数据备用卷的创建和维护，卷组内将维护一个大小等于最大池元数据卷的备用卷。默认是 yes。

- `-r, --reahead [ReadAheadSectors](autone)`

设置池元数据卷的预读扇数。默认值为“auto”，允许内核自动选择合适的值。*None* 等同于指定零。

- `--repair`

在发生磁盘故障后修复镜像或修复精简池元数据。

默认情况下，如果可能将恢复原始镜像数量。在命令行上指定 `-y` 以跳过提示。如果不替换任何替换项则使用 `-U`。此外，您可以使用 `--use-policies` 使用 `lvm.conf(5)` 中指定的设备替换策略，即 `activation/mirror_log_fault_policy` 或 `activation/mirror_device_fault_policy`。

精简池更新了 `thin_repair(8)` 工具的使用。只有非激活的精简池可以修复。内核和 Lvm2 之间没有元数据校验。这需要进一步的手动操作。修复后，未修改的旧元数据仍然存在于“`<pool>_meta<n>`”中。

- `--replaceVolume`

移除指定的设备（物理卷），并用卷组可用或特定列表中设备替换。此选项适用于 RAID 类型（例如 `raid1, raid5` 等）。

- `--stripes`

给出条带数。这等于分散逻辑卷的物理卷数量。这不适用于已分配的空间，只有新分配的空间可以条带化。

- `-I, --stripesize`

给出条带粒度的千字节数。`StripeSize` 必须是 `2^n`。

- `--type thin`

将逻辑卷转换为精简池。原始卷重命名为源。

- `--thinpool ThinLogicalVolume{Name|Path}`

指定要使用的精简池。卷转换为该池。

- `--uncache`

取消卷的缓存。

在卷变为未缓存状态之前，缓存会被刷新。

## 示例

将线性卷“`vg00/lvol1`”转换为双路镜像：

```
lvconvert -m1 vg00/lvol1
```

将线性卷“`vg00/lvol1`”转换为精简卷：

```
lvconvert --type thin -m1 vg00/lvol1
```

将磁盘日志的镜像转换为内存日志镜像：

```
lvconvert --mirrorlog core vg00/lvol1
```

将内存日志的镜像转换为磁盘日志镜像：

```
lvconvert --mirrorlog disk vg00/lvol1
```

将镜像转换为线性卷：

```
lvconvert -m0 vg00/lvol1
```

将镜像转换为具有相同数量的 `raid1` 逻辑卷：

```
lvconvert --type raid1 vg00/lvol1
```

将逻辑卷“`vg00/lvol2`”转换为源卷“`vg00/lvol1`”的快照：

```
lvconvert -s vg00/lvol1 vg00/lvol2
```

将线性卷“`vg00/lvol1`”转换为双路镜像，分配新扇区时使用 `/dev/sda:0-15` 和 `/dev/sdb:0-15`：

```
lvconvert -m1 vg00/lvol1 /dev/sda:0-15 /dev/sdb:0-15
```

将镜像卷“`vg00/lvmirror1`”转换为线性，释放来自 `/dev/sda` 的扇区：

```
lvconvert -m0 vg00/lvmirror1 /dev/sda
```

将“`vg00/lvol1_snap`”合并到其源：

```
lvconvert --merge vg00/lvol1_snap
```

如果“`vg00/lvol1`”、“`vg00/lvol2`”和“`vg00/lvol3`”都标记了“some_tag”，则每个快照卷将顺序合并，例如：“`vg00/lvol1`”，然后是“`vg00/lvol2`”，最后是“`vg00/lvol3`”。如果使用 `--background` 并启动所有快照逻辑卷：

```
lvconvert --merge @some_tag
```

从镜像中提取出一个镜像，使其成为名为“`lv_split`”的新逻辑卷。镜像数量将相应减少。

```
lvconvert --splitmirrors 1 --name lv_split vg00/lvmirror1
```

使用 `--type raid1` 创建的镜像逻辑卷在拆分镜像时可以使用 `--trackchanges` 参数。从镜像逻辑卷 `lv_raid1` 中分离出一个镜像作为单独的只读设备，并跟踪该镜像在分离状态下对镜像所所的更改。拆分出的设备名称格式为 `lv_raid1_image_N`，其中 `N` 是数字，且无法重命名。

```
lvconvert --splitmirrors 1 --trackchanges vg00/lv_raid1
```

将之前从镜像中临时分离并带有 `--trackchanges` 参数的镜像合并回原始镜像，并将其内容更新为最新。

```
lvconvert --merge vg00/lv_raid1_image_1
```

将 RAID1 逻辑卷 "`my_raid1`" 中的物理卷 "`/dev/sdb1`" 替换为指定的物理卷 "`/dev/sdf1`"。如果未提供参数 "`/dev/sdf1`"，`lvconvert` 将尝试从卷组的可用设备中寻找合适的设备。

```
lvconvert --replace/dev vg00/my_raid1 /dev/sdf1
```

将逻辑卷 "`vg00/lvpool`" 转换为块大小为 `128KiB` 的精池，并将 "`vg00/lv1`" 转换为使用该池的精卷。原始的 "`vg00/lv1`" 用作外部只读源，所有对该卷的写入将存储在 "`vg00/lvpool`" 中。

```
lvconvert --type --thin vg00/lvpool -c 128 lv1
```

将逻辑卷 "`vg00/origin`" 转换为来自精池 "`vg00/lvpool`" 的精卷。该卷将使用 "`vg00/origin`" 作为该卷未分配区域的外部卷。只读源使用新名称 "`vg00/external`"。

```
lvconvert --T --thin vg00/lvpool --originname external vg00/origin
```

使用给定的缓存元数据将现有逻辑卷转换为缓存池 LV。
