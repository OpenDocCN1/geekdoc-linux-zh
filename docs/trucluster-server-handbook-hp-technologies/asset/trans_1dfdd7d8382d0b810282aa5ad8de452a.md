
已安装的硬件组件。”文件中还包含其他信息，如使用 `strings(1)` 命令的输出所示，该输出表明该文件除了 HWID 之外还用于唯一 ID，尽管这可能是其最常见的功能。

```
# strings /etc/dec_unia_db
DEC_UNID
hardware
dfs_group_id
cluster_minor
control_port_id
```

- `dfsc.dat` 和 `dfsl.dat`

设备文件状态数据文件是由 `dsfmgr` 命令维护的 ASCII 文件。`dfsl.dat` 文件用于记录本地（或成员特定）设备特殊文件的状态以及旧的设备特殊文件名。`dfsc.dat` 文件包含公共（或集群范围）设备特殊文件的状态。这些文件分为三个部分：

1. **实例**

实例记录包含三个字段：

- 类型
- 基名
- 实例

例如（请原谅这个双关语）：

```
"I: dsk 8"
```

2. **版本**

该记录看起来像注释，但其中包含文件格式版本以及主机名和操作系统版本。

```
"# 1.0    sheridan V5.1 (Rev. 732)  Tue Mar 20 01:23:34 2001"
```

3. **状态**

状态记录当前包含 12 个字段：

- 状态（A、C 或 d）
- 集群设备主/次编号
- 基名 ID
- 设备类型
- （块或字符）
- 设备路径
- 设备实例
- 本地设备主/次编号
- 硬件 ID
- 设备节点 ID
- 旧节点名称
- 设备前缀
- 设备后缀

以下是一些示例：

第一个示例来自 `/etc/dfsc.dat`，显示了集群设备的“A”（活动）状态。

```
A:       0 1300041      45       10       0  b  ""       /dev/disk/ cdrom 0 a
```

第二个示例同样来自 `/etc/dfsc.dat`，显示了集群设备的“d”（已停用）状态。

```
d:       0 1300043      45       10       1  b  ""       /dev/disk/ cdrom 0 b
```

最后一个示例展示了来自 `/etc/dfsl.dat` 的两个条目，说明了本地设备的“C”（集群）状态。

```
C: 550000 1300001      30        6       0  b  fda0     "" "*" "*"
C: 550000 1300002      30        6       0  c  rfda0    "" "*" "*"
```

- `gen_databases`

该文件包含硬件数据库列表、它们使用的文件，以及（可选）数据库处理程序。这是一个 ASCII 文本文件，但不应修改。

## 7.4 硬件管理器（hwmgr）

hwmgr 命令是一个新工具，在硬件管理方面类似于“一站式购物”。它取代了 scsimgr(8) 实用程序，并且可以执行 scu(8) 实用程序的许多功能——尽管 scu 并未过时。hwmgr 命令具有集群感知能力，其许多选项可以针对指定成员或整个集群进行操作。hwmgr 命令管理三个硬件子系统：

- `component`

组件子系统维护系统上所有硬件组件的信息。这些信息存储在两个数据库中：`dec_hwc_ldb`（本地）和 `dec_hwc_cdb`（集群）。

- `name`

名称子系统维护总线、控制器等硬件组件的硬件持久性信息。这些信息存储在 `dec_hw_db` 中。

- `scsi`

scsi 子系统维护 SCSI 设备的信息。这些信息存储在 `dec_scsi_db` 中。

有关各种硬件数据库的更多信息，请参阅本章前面的 7.3 节。

截至撰写本文时，有关 hwmgr 命令的绝对最佳信息来源是 hwmgr 命令本身。

```
# hwmgr -help | grep -E "^Usage:|^or"
Usage: hwmgr -flash light
or: hwmgr -get attribute [ saved | default | current ]
or: hwmgr -get category
or: hwmgr -help [ <command> ] [ <subsystem> ]
or: hwmgr -set attribute [ saved | current ] -a <attribute>=<value>
or: hwmgr -view cluster
or: hwmgr -view devices
or: hwmgr -view hierarchy
or: hwmgr -view env
or: hwmgr -view timestamps
or: hwmgr -view transaction
or: hwmgr <command> <subsystem> <args>
```

我们仅使用 grep(1) 命令展示了基本的命令用法，尽管最后一条 hwmgr 命令用法“or: hwmgr <command> <subsystem> <args>”实际上有许多变体。

```
# hwmgr -help | grep -p -E "^Where <command>"
Where <command> is:
  -add
  -delete
  -edit
  -locate
  -online
  -offline
  -power
  -redirect
  -refresh
  -reload
  -remove
  -scan
  -show
  -status
  -unconfigure
  -unindict
  -unload
```

我们不会尝试向您展示 hwmgr 命令的每一个可能选项，而是将重点放在一些更有用的选项上。

有关更多信息，请参阅 V5.0A 和 V5.1 上的 hwmgr(8) 参考手册页。在 V5.1A 中，hwmgr(8) 参考手册页增加了四个额外的参考手册页：
