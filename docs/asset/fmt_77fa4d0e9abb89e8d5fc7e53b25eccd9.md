
`"TYPE"` 字段表示成员磁盘由 `"m"` 指示（`"q"` 代表仲区磁盘）。`"CFS"` 字段表示 `cluster_root` 域中的卷。最后一个字段是 `"LSM"` 字段，它持有序列号 (30)、设备以及它们的 LSM 磁盘类型（`/dev/disk/dsk5h|simp`、`/dev/disk/dsk6g|simp`、`/dev/disk/dsk5g|simp`）。

> **注意：** `clu_quorum` 命令将仲区磁盘的 cnx 分区信息存储在 `/cluster/admin` 目录下的 `clu_quorum_qdisk` 文件中。

我们将在 22 章中详细介绍如何恢复成员磁盘。关于 `clu_bdmgr` 命令的更多信息，请参阅 `clu_bdmgr` (8) 参考页。`clupt`。

### 17.8.5.1 cnx 分区的深度里有什么？

在深入研究 cnx 分区的深度之前，应该注意关于该主题的文档并不多。这是设计如此，因为大多数信息对于日常管理集群通常没有用处，尽管我们注意到，在某些情况下，这些信息对于处理仲区问题是有用的。最后，你应该意识到，由于工程师可以选择集群的布局，这里的信息在未来发布中是有效的。

那么，为什么要费心展示这些信息？嗯，许多管理员、学生和支持人员请求有关 cnx 分区的更多信息。根据 `/sys/include/sys/clust.h` 中的 `clout.h` 文件，cnx 分区被分为以下几个部分：

| 部分 | 描述 |
| :--- | :--- |
| 仲区 | ... |
| 成员 | ... |

仲区和成员分区被分为以下五个段：

| 分段 | 范围 |
| :--- | :--- |
| 仲区 (0 - 255K) | 0、96、112 |
| 成员分区 (256K - 511K) | 336、352、384 |
| 仲区 - 64K | |
| 仲区 - 18K | |
| AdvFS - 18K | |
| 备用 - 128K | |

cnx 分区在成员磁盘上，在仲区磁盘上。cnx 分区在写入时是未使用的。我们将使用 `cnxread` 来检查 cnx 分区的状况。

#### 看看我们的 cnx 分区里有什么

使用 `cnxread -q dsk2` 检查：

```
# cnxread -q dsk2
/dev/rdisk/dsk2h 的 CNX 分区信息。这是一个成员启动磁盘。
法定人数节（Quorum Section）信息：

nada (CSID: 0, incarn: 0):

| 成员 (Members) | 当前票数 (Current Votes) | 法定票数 (Quorum Votes) | Qdisk 票数 (Qdisk Votes) |
| --- | --- | --- | --- |
| 0 | 0 | 0 | 0 |

Qdisk 于 16921232 的 19:00:00 被成员申领：
nobody (CSID: 0, incarn: 0, member: 0):

Qdisk 于 16921232 的 19:00:00 被成员写入：
nobody (CSID: 0, incarn: 0, member: 0):

活动计数 = 0

法定人数节中不不包含任何关于成员磁盘的相关信息。
```

#### 17.8.5.1.2 时间中的分区 (PIT) 段

截至本文编写时，PIT 段已预留供未来使用。

#### 17.8.5.1.3 AdvFS cluster_root 设备段

该段在 `clupt.h` 文件中定义，包含以下信息：

- 魔数（magic number）
- 数据序列号
- `cluster_root` 域中的设备数量
- 设备 ID 数组

使用 `cnxread` 程序查看成员的启动磁盘 cnx 分区，我们可以看到 `cluster_root` 域只有一个设备。

```
# cnxread dsk2

/dev/rdisk/dsk2h 的 CNX 分区信息。这是一个成员启动磁盘。

集群根文件系统 (AdvFS) 段信息

Magic #: 0x42534, Sequence #: 88

maj,min

--- ---

Devices: [ 1]: 19, 52
```

我们可以通过以下命令快速确定哪个设备的主设备/次设备号为“19, 52”：

```
# ls -1 /dev/disk/* | grep "19, 52*"

brw---- 1 root       system 19, 52 Nov 27 03:59 /dev/disk/dsk1b
```

让我们临时向 `cluster_root` 域添加一个设备。

```
# addvol /dev/disk/dsk5g cluster_root

/dev/rdisk/dsk2h 的 CNX 分区信息。这是一个成员启动磁盘。
集群根文件系统 (AdvFS) 段信息
Magic #: 042534, Sequence #: 90
maj,min
---
Devices: [ 1]: 19, 142
[ 2]: 19, 52
```

输出中显示了第二个设备。

#### 17.8.5.1.4 CLSM cluster_root 设备段

CLSM 段与 AdvFS 段类似，因为它也包含设备信息。该段包含：

- 魔数
- 序列号
- LSM（或 Veritas）版本号
- 设备数量
- 设备信息数组（设备名称、类型、ID）

以下是使用 LSM 卷作为 `cluster_root` 设备的成员启动磁盘 cnx 分区的输出。有关在集群中使用 LSM 的更多信息，请参阅第 14 章。

```
# cnxread -1 dsk2

/dev/rdisk/dsk2h 的 CNX 分区信息。这是一个成员启动磁盘。

集群根文件系统 (AvFS) 段信息

Magic #: 0x42534, Sequence #: 116

maj,min
---
Devices: [ 1): 40, 5

CLSM 段信息

Magic #: 0x46185, Sequence #: 22, Version 3.1

maj,min
---
Devices: [ 1): 19,128 dsk5h (simp)
[ 2): 19,142 dsk6g (simp)
[ 3): 19,126 dsk5g (simp)
```

在我们的集群中，`dsk5` 和 `dsk6` 是镜像卷中的两个对节点，用于 `cluster_root`。列出的第一个设备 `dsk5` 是 `rootdg` 中的私有区域磁盘。我们并不确定它为什么会显示，因为不在 `cluster_root` 卷中，但看起来 `rootdg` 中的任何设备都会显示在输出中。

```
# volprint -g rootdg

| TY NAME ASSOC KSTATE LENGTH PLOFFS STATE TUTILO PUTILO |
| dg rootdg rootdg - - - - - - |
| dm clu_mroot dsk5g 8686058 - - - - - |
| dm clu_root dsk6g 8686058 - - - - - |
| dm dsk5h dsk5h 8686058 - - - - - |
| v cluster_root cluroot ENABLE 1048576 - - ACTIVE |
| pl cluster_rootvol-01 cluster_rootvol-01 ENABLE 1048576 - - ACTIVE |
| sd clu_mroot-01 cluster_rootvol-01 ENABLE 1048576 0 - - - - |
| pl cluster_rootvol-02 cluster_root ENABLE 1048576 - - ACTIVE |
| sd clu_root-01 cluster_rootvol-02 ENABLE 1048576 0 - - - - |
```

## 如何恢复法定人数

当丢失法定人数且无法通过启动额外的成员来恢复时，有方法可以在不重建集群的情况下解决此问题。

例如，假设我们有一个没有法定人数磁盘的六成员集群，其中三个成员由于某种原因（如宇宙射线击中等）崩溃了。剩余的三个成员将没有足够的票数来维持集群运行。由于丢失了法定人数，无法使用 `clu` 命令调整集群的预期票数。我们该怎么办？

我们可以停止一个挂起的集群成员并交互式地调整集群的预期票数。`clubase` 子系统中的 `cluster_adjust_expected_votes` 属性当设置为零时，将导致集群调整预期票数。

### 17.10.1 在票数不足和/或仲裁盘故障的情况下形成集群

如果我们把之前的场景修改为包含一个失败的仲裁盘，我们仅通过使用 `cluster_expected_votes` 就能进行交互式启动吗？答案是肯定的。虽然你可以在仲裁盘失败的情况下启动集群，但仲裁盘线程会在最终放弃之前尝试重试磁盘一段时间。在 V5.1A 之前，这会推迟启动过程。作为一种备替代方案，在交互式启动提示符中添加第二个属性 `cluster_qdisk_votes`。
