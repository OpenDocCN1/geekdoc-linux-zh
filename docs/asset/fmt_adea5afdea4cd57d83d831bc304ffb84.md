
```
$ lvdisplay -v /dev/vg00/lvol1

--- 逻辑卷 ---
LV Name /dev/vg00/lvol1
VG Name /dev/vg00
LV Permission read/write
LV Status available/syncd
Mirror copies 0
Consistency Recovery MWC
Schedule parallel
LV Size (Mbytes) 48
Current LE 12
Allocated PE 12
Stripes 0
Stripe Size (Kbytes) 0
Bad block off
Allocation strict/contiguous

--- 逻辑卷的分布 ---
PV Name LE on PV PE on PV
/dev/dsk/c0t1d0 12 12

--- 逻辑扩展区 ---
LE PV1 PE1 Status 1
0000 /dev/dsk/c0t1d0 0000 current
```

### 逻辑卷管理器背景

```
0001 /dev/dsk/c0t1d0  0001 current
0002 /dev/dsk/c0t1d0  0002 current
0003 /dev/dsk/c0t1d0  0003 current
0004 /dev/dsk/c0t1d0  0004 current
0005 /dev/dsk/c0t1d0  0005 current
0006 /dev/dsk/c0t1d0  0006 current
0007 /dev/dsk/c0t1d0  0007 current
0008 /dev/dsk/c0t1d0  0008 current
0009 /dev/dsk/c0t1d0  0009 current
0010 /dev/dsk/c0t1d0  0010 current
0011 /dev/dsk/c0t1d0  0011 current
```

尽管此示例中显示的大部分内容不言自明，但有些条目需要解释。逻辑卷的大小为 48 MBytes，由 12 个逻辑扩展区 `LEs` 和 12 个物理扩展区 `PE` 组成。这意味着每个物理扩展区的大小为 4 MBytes `4 MBytes x 12 个扩展区 = 48 MBytes`。我们可以通过运行显示物理卷特征的命令来验证这一点。在该列表的底部，您可以看到逻辑扩展区映射到物理扩展区的情况。在这种情况下，逻辑扩展区 0000 - 0011 与物理扩展区 0000 - 0011 之间存在直接映射。

#### `lvextend`

此命令用于增加分配给逻辑卷的物理扩展区数量。我们有时会低估逻辑卷所需的大小，使用此命令可以轻松解决此问题。您可能希望扩展逻辑卷以增加镜像副本数量 `使用 -m 选项`、增加逻辑卷的大小 `使用 -L 选项` 或增加逻辑扩展区数量 `使用 -l 选项`。

#### `extendfs`

在 `lvextend` 之后使用此命令。虽然 `lvextend` 命令扩展逻辑卷，但 `extendfs` 扩展逻辑卷内的文件系统。如果您忘记发出 `extendfs` 命令，SAM 中的逻辑卷看起来已扩展，但发出 `bdf` 命令不会显示扩展情况。

### `lvlnboot`

使用此命令将逻辑卷设置为主、引导、主要交换或转储卷 `这可以使用 lvrmbboot 撤消`。发出带有 `-v` 选项的 `lvlnboot` 命令可显示当前设置。

### `lvsplt` 和 `lvmerge`

这些命令分别用于拆分和合并镜像逻辑卷。如果您有一个镜像逻辑卷，`lvsplt` 将把它拆分为两个逻辑卷。`lvmerge` 合并两个大小相同的逻辑卷，增加镜像副本数量。

### `lvmmigrate`

此命令为磁盘分区中的根文件系统准备迁移到逻辑卷。如果您有一个需要转换为逻辑卷的分区，就会使用此命令。

### `lvreduce`

使用此命令减少分配给逻辑卷的物理扩展区数量。在创建逻辑卷时，我们有时会高估逻辑卷的大小。此命令可用于设置镜像副本数量 `使用 -m 选项`、减少逻辑扩展区数量 `使用 -l 选项` 或减少逻辑卷的大小 `使用 -L 选项`。在减小逻辑卷大小时请小心。您可能会将其设置得比其中的数据还要小。如果选择这样做，请确保您有良好的数据备份。

清空逻辑卷后，您可以使用此命令从卷组中删除逻辑卷。

如果您不希望某个逻辑卷作为根设备、引导设备、主交换设备或转储设备 `这与 lvlnboot 命令相反`，则使用此命令。但是，除非您有用于引导的磁盘分区，否则请确保使用 `lvlnboot` 命令指定了根设备或引导设备，否则系统将不知道该从哪里引导。

有时，逻辑卷中的镜像数据会变得“陈旧”或过时。`lvsync` 用于同步逻辑卷中的物理区域。

## 添加磁盘

在本节中，我们将对 XP 256 磁盘进行一些操作。我们希望创建十个卷组，每个卷组包含五个主磁盘和五个备用磁盘。

让我们查看包含用于 XP 256 主路径和备用路径的物理磁盘的文件。XP 256 是一种高级存储设备，具备在主控制器故障时故障转移到备用控制器的能力。同一组磁盘连接到主控制器和备用控制器，但这些磁盘被赋予了两个不同的设备文件集。一组是磁盘连接到主控制器时使用的，另一组是同一组磁盘连接到备用控制器时使用的。如果您曾使用过 ServiceGuard，可能会遇到过相同的概念。有一组磁盘通过两条不同的路径连接，因此您必须根据磁盘是通过主路径还是备用路径连接，用不同的名称来定义这些磁盘。以下是文件 `pri` 的内容，其中以每五个为一组列出了主磁盘：

```
c9t0d0 c9t0d1 c9t0d2 c8t0d0 c8t0d1

c7t0d0 c7t0d1 c7t0d2 c10t0d0 c10t0d1

c9t0d3 c9t0d4 c9t0d5 c8t0d3 c8t0d4

c7t0d3 c7t0d4 c7t0d5 c10t0d3 c10t0d4

c9t0d6 c9t0d7 c9t1d0 c8t0d6 c8t0d7

c7t0d6 c7t0d7 c7t1d0 c10t0d6 c10t0d7

c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2

c7t1d1 c7t1d2 c7t1d3 c10t1d1 c10t1d2

c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5

c7t1d4 c7t1d5 c7t1d6 c10t1d4 c10t1d5
```

请注意，在此列表中，磁盘被分为每五个一组。每五个磁盘将构成一个卷组。总共有 10 组五个磁盘，它们将放入卷组 `vgu01` 到 `vgu10` 中。

还将有一个备用磁盘组，每组五个磁盘。备用磁盘将用于在之前描述的磁盘控制器故障转移情况下使用。以下是文件 `alt` 的内容，其中以每五个为一组列出了备用磁盘：

```
c8t8d0 c8t8d1 c8t8d2 c9t8d0 c9t8d1

c10t8d0 c10t8d1 c10t8d2 c7t8d0 c7t8d1

c8t8d3 c8t8d4 c8t8d5 c9t8d3 c9t8d4

c10t8d3 c10t8d4 c10t8d5 c7t8d3 c7t8d4

c8t8d6 c8t8d7 c8t9d0 c9t8d6 c9t8d7

c10t8d6 c10t8d7 c10t9d0 c7t8d6 c7t8d7

c8t9d1 c8t9d2 c8t9d3 c9t9d1 c9t9d2

c10t9d1 c10t9d2 c10t9d3 c7t9d1 c7t9d2

c8t9d4 c8t9d5 c8t9d6 c9t9d4 c9t9d5

c10t9d4 c10t9d5 c10t9d6 c7t9d4 c7t9d5
```

此列表中总共显示了 10 组备用磁盘，它们也将是卷组 `vgu01` 到 `vgu10` 的一部分。使用在 XP 256 上设置好的这些主磁盘和备用磁盘，我们将在主机系统上设置相应的卷。在此示例中，主机系统是 V-Class 系统。

现在，让我们介绍创建其中一个卷组的步骤。首先，我们将使用 `pvcreate` 命令为卷组中的每个磁盘创建一个物理卷。接下来，我们将使用 `mkdir` 创建卷组的目录。然后，我们使用 `mknod` 在该目录内为卷组创建设备特殊文件。这将设置创建 10 个卷组中的第一个所需的目录和特殊文件。然后，我们将使用 `vgcreate` 创建包含五个主磁盘的卷组。在创建卷组时，我们指定第一个磁盘，然后使用 `vgextend` 将其他磁盘加入卷组。接着，我们使用 `vgextend` 扩展卷组以包含五个备用磁盘。最后一步是为整个卷组创建一个单一逻辑卷。您可能希望在一个卷组内创建多个逻辑卷，但在我们的示例中，我们只需要一个消耗卷组全部容量的逻辑卷，即 8755 个物理区域。以下流程列出了创建第一个卷组的手动步骤：
