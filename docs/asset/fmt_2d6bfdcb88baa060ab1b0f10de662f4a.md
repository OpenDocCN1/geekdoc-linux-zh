
执行 I/O（即对 DRD 设备文件进行读写）在发送到 DRD 之前将由集群文件系统 (`CFS`) 层处理。由于 `CFS` 是以客户端/服务器模式实现的，尽管设备可能支持 `DAIO` 且执行 I/O 的成员可以直接访问共享总线，但 `DRD` 不会参与那些 `CFS` 客户端成员（直接 I/O 或直接访问见第 13 章）。块设备特殊文件位于 `/devices` 目录，因此由 `cluster_root` 域的 `CFS` 服务器提供。

现在，让我们演示集群中如何执行块 I/O。我们将再次使用 `dd` 命令，但将使用 `dsk5` 的块设备特殊文件。

我们首先需要找到哪个是 `cluster_root` 域的 `CFS` 服务器。为此我们将使用 `cfgr` 命令。

```
# cfsmgr -d cluster_root
域或文件系统名称 = cluster_root
服务器名称 = sheridan
服务器状态 : OK
```

节点 `sheridan` 是 `CFS` 服务器。在执行任何 I/O 之前，重置两个成员的统计信息。

```
[molari]
# drdmgr -a statistics=0 dsk5
```

```
[molari]
# drdmgr -a statistics=0 -h sheridan dsk5
```

将在 `molari` 上使用 `dd` 命令来说明 `sheridan` 上的 `DRD` 将执行实际工作。I/O 请求将发送根 (`/`) 文件系统的 `CFS` 服务器。`CFS` 服务器将把 I/O 请求调度到物理文件层。随后 I/O 将被调度到 I/O 映射子系统，然后向下到达同一成员上的 `DRD`。I/O 架构如图 5-2 所示。

```
[molari]
# dd if=MyFile.molari of=/dev/disk/dsk5h
11718+1 records in
11718+1 records out
```

注意我们使用的是块设备特殊文件 (`/dev/disk/dsk5h`) 而不是字符设备特殊文件 (`/dev/rdisk/dsk5h`)。让我们看看 `molari` 的 `dsk5` `DRD` 统计信息告诉了我们什么。

```
[molari]
# drdmgr -a statistics dsk5
来自成员 molari 的数据（截至 2001-07-19:22:30:12）：
设备名称: dsk5
客户端成员 molari 的统计信息：
读取操作次数: 0
写入操作次数: 0
读取字节数: 0
写入字节数: 0
```

如你所示，`molari` 上的 `DRD` 并没有看到任何 I/O。然而，`sheridan` 上的 `DRD` 相当忙碌。

```
[molari]
# drdmgr -a statistics -h sheridan dsk5
来自成员 sheridan 的数据（截至 2001-07-19:22:34:01）：

设备名称: dsk5
客户端成员 sheridan 的统计信息：
读取操作次数: 2930
写入操作次数: 11719
读取字节数: 600060
写入字节数: 24000512
```

### 15.3.2 私有总线上的 DAIO 示例

当磁盘位于私有总线上时，所有 I/O 请求将汇聚到具有磁盘直接物理访问的成员。这意味着如果访问设备的唯一成员宕机，该设备将无法访问。

例如，`dsk8` 位于仅属于 `sheridan` 的总线上。我们如何知道？最直接的方法是使用 `hmwgr` 命令：

```
[molari]
# hmwgr -view devices -dsf dsk8
hwmmgr: 无此类硬件 ID 或类别。
```

```
[molari]
# hmwgr -view devices -dsf dsk8 -m sheridan
HWID: 设备名称 模型 主机 位置
--------------------------------------------
DEVICE HOSTNAME TYPE SUBTYPE OWNER NUM FILE VALID PATH
47: 1 molari disk none 0 1 dsk0 [2/0/0] BB09235B6 sheridan bus-2-targ-1-lun-0
```

该设备在 `molari` 上不存在，但在 `sheridan` 上存在。为了进一步确认，我们可以检查总线。

```
[molari]
# hwmgr -show scsi -bus 2 -m sheridan
DEVICE DEVICE DR NUM DEVICE FIRST
HWID: DEVICE HOSTNAME TYPE SUBTYPE OWNER PATH FILE VALID PATH
47: 1 sheridan disk none 2 1 dsk7 [2/0/0]
103: 2 sheridan disk none 2 1 dsk8 [2/1/0]
```

每个成员都有一个 `bus-2`，这一事实并不如每个成员在 `bus-2` 上的设备各异那么有趣。存储设备在集群中是唯一的，这证明了私有总线。有关 `hwmgr` 命令的更多信息，请参阅第 7 章以及 `hwmgr (8)` 参考页。

你可以使用 `drmgr` 命令来检查设备的路径，但这只会告诉该设备是否存在活动路径，而不会告诉你设备是否在私有总线路上。

查看 `molari` 的 `drmgr` 命令的输出，你会发现它不包含统计信息，例如 `molari` 对于 `dsk8` 的 `DRD` 仅是一个客户端（即它没有对磁盘的物理访问）。注意，从 `sheridan` 看到的输出包含了两个成员的统计信息，但 `molari` 的统计数据为零。

```
[molari]
# drmgr dsk8
View of Data from member molari as of 2001-07-19:23:00:56

Device Name: dsk8
Device Type: Direct Access IO Disk
Device Status: OK
Number of Servers: 1
Server Name: sheridan
Server State: Server
Access Member Name: sheridan
Open Partition Mask: 0x80 < h
```

```
[molari]
# drmgr -h sheridan dsk8
View of Data from member sheridan as of 2001-07-19:23:33:52

Device Name: dsk8
Device Type: Direct Access IO Disk
Device Status: OK
Number of Servers: 1
Server Name: sheridan
Server State: Server
Access Member Name: sheridan
Open Partition Mask: 0x80 < h
Statistics for Client Member: molari
Number of Read Operations: 0
Number of Write Operations: 0
Number of Bytes Read: 0
Number of Bytes Written: 0
Statistics for Client Member: sheridan
Number of Read Operations: 20319
Number of Write Operations: 12819
Number of Bytes Read: 153012224
Number of Bytes Written: 56055808
```

你可以看到 `dsk8` 上已经有了一些 I/O 操作。这主要是因为“h”分区（如“Open Partition Mask”所示）。该分区包含 `/kits` 文件系统 (`extra+kits`)。

```
# cfsmgr -a devices -d extra
```

| 用于 extra 的设备列表 |

| :--- | :--- |

| 设备数量 = 1 |

| 1 | dsk8h |

所有到 `dsk8` 的 I/O 都通过 `sheridan` 上的 `DRD`。

如果我们从 `molari` 向 `dsk8` 上的 "a" 分（我们知道它是未使用的）写入并查询 `DRD` 统计信息，你会发现 `molari` 上的统计数据保持为零，但 `sheridan` 的统计数据将会增加。

```
[molari]
# drdmgr -a statistics=0 -h sheridan dsk8
```

```
[molari]
# dd if=MyFile.molari=/dev/disk/dsk8a
11718+1 records in
11718+1 records out
```
