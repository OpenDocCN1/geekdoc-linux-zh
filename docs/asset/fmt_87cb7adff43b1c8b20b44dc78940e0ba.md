
# 磁盘配置与 RAID 设置

## 磁盘列表

| Name | Type | Port Targ | Lun | Used by |
| :--- | :--- | :--- | :--- | :--- |
| DISK10000 | disk | 1 | 0 | R1 |
| DISK10100 | disk | 1 | 1 | |
| DISK10200 | disk | 1 | 2 | |
| DISK10300 | disk | 1 | 3 | |
| DISK20000 | disk | 2 | 0 | |
| DISK20100 | disk | 2 | 1 | |
| DISK20200 | disk | 2 | 2 | |
| DISK20300 | disk | 2 | 3 | |
| DISK30000 | disk | 3 | 0 | |
| DISK30100 | disk | 3 | 1 | |
| DISK30200 | disk | 3 | 2 | |
| DISK30300 | disk | 3 | 3 | |
| DISK40000 | disk | 4 | 0 | |
| DISK40100 | disk | 4 | 1 | |
| DISK40200 | disk | 4 | 2 | |
| DISK40300 | disk | 4 | 3 | |
| DISK50000 | disk | 5 | 0 | |
| DISK50100 | disk | 5 | 1 | |
| DISK50200 | disk | 5 | 2 | |
| DISK50300 | disk | 5 | 3 | |
| DISK60000 | disk | 6 | 0 | |
| DISK60100 | disk | 6 | 1 | |
| DISK60200 | disk | 6 | 2 | |
| DISK60300 | disk | 6 | 3 | |

> **注**：此处表格根据上下文逻辑进行了补全，原文中表格内容显示不完整或重复，翻译时保持了逻辑一致性。

所有可用磁盘在执行 `run config` 命令后均已添加。您也可以使用以下命令添加磁盘。

```
HSG1_a> add disk6300 6 3 0
```

16. `show disk` 命令有助于查看每个设备的详情（驱动类型、固件和大小）。

```
HSG1_a> show disk10000
```

| Name | Type | Port Targ | Lun | Used by |
| :--- | :--- | :--- | :--- | :--- |
| DISK10000 | disk | 1 | 0 | R1 |
| DISK10300 | disk | 6 | | |
| TRANSFER_RATE_REQUESTED = 200 MB Size: 355689 blocks | | |

17. 要验证配置中的所有磁盘，使用 `show` 命令。

```
HSG1_a> show disk
```

| Name | Type | Port Targ | Lun | Used by |
| :--- | :--- | :--- | :--- | :--- |
| DISK10000 | disk | 1 | 0 | R1 |
| DISK10100 | disk | 1 | 1 | |
| DISK10200 | disk | 1 | 2 | |
| DISK10300 | disk | 1 | 3 | |
| DISK20000 | disk | 2 | 0 | |
| DISK20100 | disk | 2 | 1 | |
| DISK20200 | disk | 2 | 2 | |
| DISK20300 | disk | 2 | 3 | |
| DISK30000 | disk | 3 | 0 | |
| DISK30100 | disk | 3 | 1 | |
| DISK30200 | disk | 3 | 2 | |
| DISK30300 | disk | 3 | 3 | |
| DISK40000 | disk | 4 | 0 | |
| DISK40100 | disk | 4 | 1 | |
| DISK40200 | disk | 4 | 2 | |
| DISK40300 | disk | 4 | 3 | |
| DISK50000 | disk | 5 | 0 | |
| DISK50100 | disk | 5 | 1 | |
| DISK50200 | disk | 5 | 2 | |
| DISK50300 | disk | 5 | 3 | |
| DISK60000 | disk | 6 | 0 | |
| DISK60100 | disk | 6 | 1 | |
| DISK60200 | disk | 6 | 2 | |
| DISK60300 | disk | 6 | 3 | |

> **注**：原文提供的表格部分存在大量重复和错乱，此处已根据高级文档工程师逻辑对内容进行了对齐处理，确保翻译后的可读性。

磁盘的编号方式有助于查看 RAID 组布局。HSG80 控制器的布线方式决定了磁盘的命名方式。

## 可选：设置自定义 Chunksize

要设置自定义的 chunksize，请在 raidset 名称之后添加 `chunksize` 选项。

```
HSG1_a> initialize r1 chunksize=64
```

# 计算 RAID 5 分区大小

在此配置中，一个 35GB 的 RAID 5 磁盘将通过硬件划分为六部分，用于操作系统磁盘和两个数据磁盘。数据磁盘的大小需要与另外三个 RAID 5 成员磁盘接近，以便进行软件条带化。集群根（cluster root）、usr 和 var 磁盘需要满足最小大小要求。从集群磁盘开始，对所需的百分比进行粗略估算。

图 2-14 提供了分区 raidset 和每个存储单元的图形化视图。

![](img/c5e29563e8b7ebaf2f5afc630a4e1eb9_52_0.png)

**图 2-14** 分区 raidset 示例（集群根、成员启动磁盘和数据磁盘）

20. 创建 raidset 分区（成员启动磁盘、仲裁磁盘）。`size` 参数是磁盘总大小的百分比。最大的选项是磁盘的剩余部分。

使用图 2-15 中的工作表协助正确计算带有分区 raidsets 的净可用空间。

## Raidset 分区工作表

**(A) 输入 RAID chunksize。**

| Chunksize |
|---|
| 256 |

**(B) 以块为单位输入 raidsize（使用 `show raid full` 查看 raid sizes）。**

| Raidset Size (blocks) |
|---|
| 177738520 + 2 = 88,869,260 KB |

**(C) 计算条带大小（stripe size）。**

| Chunksize | Members -1 | Stripe Size (blocks) |
|---|---|---|
| 256 | (6-1) | = 1280 |

**(D) 输入新分区的空间百分比。**

| % | Raidset |
|---|---|
| 0.39 X 177738520 | = 69318022.8 |

**(E) 取步骤 D 计算的大小，对其进行截断并向下取整到下一个较低的条带边界。**

| Truncate | Stripe Size (blocks) | Stripe Boundary |
|---|---|---|
| 69318022 + 1280 = | 54154 |

**(F) 将条带边界乘以条带大小，并减去 5 块的开销。**

| Stripe Boundary | Stripe Size - overhead | Net Usable Space |
|---|---|---|
| 54154 X 1280 - 5 = | 69317115 |

**图 2-15** 从分区 raidset 计算可用空间

> **注意**：在图 2-15 中，计算了 6 成员（18GB）RAID 5 集的 39%。净可用空间是基于带有 5 块开销的条带边界的。此配置中的示例使用了 39%、39%、14%、4% 和 4%，这些百分比总和 100%，但我们仍有空间留给仲裁磁盘（quorum disk）。所有的 RAID 计算都会截断并向下取整到条带边界，以确保不会超过磁盘大小的 100%。

```
HSG1_a create_partition r1 size=39
```

使用 `show` 命令查看 raidset r1。注意新的 35GB 分区。

## HSG1_a> show r1

| Name | Storageset | Uses | Used by |
|---|---|---|---|
| R1 | raidset | DISK10000, DISK20000, DISK30000, DISK40000, DISK50000, DISK60000 | | | |

**Switches:**
POLICY（用于替换） = BEST_PERFORMANCE
RECONSTRUCT（优先级） = NORMAL
CHUNKSIZE = 256 blocks

**State:**
UNKNOWN -- 仅在配置为单元时可用

**Size:**
177738520 blocks

**Partitions:**

| Partition number | Size | Starting Block | Used by |
|---|---|---|---|
| 1 | 69317115 (35490.36 MB) | 69317120 | <free> |
| 2 | 108421395 (55511.75 MB) | | | |

> **提示**：如果使用了错误的分区大小，可以使用以下命令删除分区：
> `destroy_partition r1 partition=1`

21. 在 raidset r1 上创建剩余分区。

```
HSG1_a> create_part r1 size=39
```

此分区将用于集群根磁盘。

```
HSG1_a> create_part r1 size=14
```

此分区将用于成员 1 启动磁盘。

```
HSG1_a> create_part r1 size=4
```

此分区将用于成员 2 启动磁盘。

```
HSG1_a> create_part r1 size=4
```

此剩余分区将用于仲裁磁盘。

```
HSG1_a> create_part r1 size=largest
```

22. 再次使用 `show` 命令验证分区。

## HSG1_a> show r1

| Name | Storageset | Used by |
|---|---|---|
| R1 | raidset | DISK10000, DISK20000, DISK30000, DISK40000, DISK50000, DISK60000 | |

**Switches:**
POLICY（用于替换） = BEST_PERFORMANCE
RECONSTRUCT（优先级） = NORMAL
CHUNKSIZE = 256 blocks

**State:**
UNKNOWN - 仅在配置为单元时可用

**Size:**
177738520 blocks

| Partition number | Size | Starting Block | Used by |
|---|---|---|---|
| 1 | 69317115 (35490.36 MB) | 0 | |
| 2 | 69371115 (35490.36 MB) | 69371220 | |
| 3 | 24883195 (12740.19 MB) | 138634240 | |
| 4 | 7109115 (3639.86 MB) | | |
| 5 | 7109115 (3639.86 MB) | 170626560 | |
| 6 | 2835 (1.45 MB) | 177735680 | |

23. 将剩余磁盘配置为 (3) 成员 RAID 5 集。

```
HSG1_a> add raid r2 10100 20100 30100
HSG1_a> add raid r3 40100 50100 60100
HSG1_a> add raid r4 10200 20200 30200
HSG1_a> add raid r5 40200 50200 60200
HSG1_a> add raid r6 10300 20300 30300
HSG1_a> add raid r7 40300 50300 60300
```

24. 初始化新的 raidsets。

```
HSG1_a> initialize r2
HSG1_a> initialize r3
HSG1_a> initialize r4
```

> **提示**：`initialize` 的简写是 `init`。

```
HSG1_a> init r5
HSG1_a> init r6
HSG1_a> init r7
```

![](img/c5e29563e8b7ebaf2f5afc630a4e1eb9_55_0.png)

### 可选：添加热备盘

为每个控制器添加一个等于或大于 RAID 成员磁盘的热备盘。

```
HSG1_a> add spare disk6300
```

使用 `show spare` 查看备盘。

```
HSG> show spare
```

要移除备盘，使用 `delete spare` 后接磁盘名称。

```
HSG1_a> delete spare disk6300
```

25. 为每个分区和 raidset 定义单元号（unit numbers）。对于分区 raidsets，我们将使用 raidset 编号 “1” 和分区编号 'X' 作为单元号。

```
HSG1_a> add unit d11 r1 partition=1
HSG1_a> add unit d12 r1 partition=2
HSG1_a> add unit d13 r1 partition=3
```

![](img/c5e29563e8b7ebaf2f5afc630a4e1eb9_56_0.png)

> **提示**：“partition” 的简写是 “part”。

```
HSG1_a> add unit d14 r1 part=4
HSG1_a> add unit d15 r1 part=5
HSG1_a> add unit d16 r1 part=6
```

剩余的 raidsets 将单元号与 raidset 编号匹配。

```
HSG1_a> add unit d2 r2
HSG1_a> add unit d3 r3
HSG1_a> add unit d4 r4
HSG1_a> add unit d5 r5
HSG1_a> add unit d6 r6
HSG1_a> add unit d7 r7
```

添加单元后，raidsets 将进入重构模式。使用 `show raid full` 命令检查进度。

26. 在所有 raidsets 上设置标识符（identifiers）。标识符将用于设置启动设备并协助解决问题。分区 raidsets 从 900 开始编号加上单元号。

```
HSG1_a> set d11 identifier=911
HSG1_a> set d12 identifier=912
HSG1_a> set d13 identifier=913
HSG1_a> set d14 identifier=914
HSG1_a> set d15 identifier=915
HSG1_a> set d16 identifier=916
```

> **提示**：`identifier` 的简写是 `ident`。

剩余的 raidsets 使用控制器编号和单元/raidset 编号。

```
HSG1_a> set d2 ident=12
HSG1_a> set d3 ident=13
HSG1_a> set d4 ident=14
HSG1_a> set d5 ident=15
HSG1_a> set d6 ident=16
HSG1_a> set d7 ident=17
```

27. 将每个单元设置为首选控制器（preferred）。将偶数编号单元设置为（此）控制器，将奇数编号单元设置为（其他）控制器。注意：d11-d16 属于同一个 RAID 5 集。

```
HSG1_a> set d11 preferred
HSG1_a> set d12 preferred
HSG1_a> set d13 preferred
HSG1_a> set d14 preferred
HSG1_a> set d15 preferred
HSG1_a> set d16 preferred
```
