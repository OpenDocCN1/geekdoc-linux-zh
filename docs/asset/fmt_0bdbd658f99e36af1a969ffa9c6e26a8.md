
```
HSG> add unit d11 partition=1 disable_access_path=all
HSG> add unit d12 partition=2 disable_access_path=all
HSG> add unit d13 partition=3 disable_access_path=all
HSG> add unit d14 partition=4 disable_access_path=all
HSG> add unit d15 partition=5 disable_access_path=all
HSG> add unit d16 partition=6 disable_access_path=all
```

配置分区的存储单元。

```
HSG> set d11 identifier=11 enable_access_path=(MOL1A1,MOL1RB2,SHER1A1,SHER1B2)
HSG> set d12 identifier=12 enable_access_path=(MOL1A1,MOL1RB2,SHER1A1,SHER1B2)
HSG> set d13 identifier=13 enable_access_path=(MOL1A1,MOL1RB2,SHER1A1,SHER1B2)
HSG> set d14 identifier=14 enable_access_path=(MOL1A1,MOL1RB2,SHER1A1,SHER1B2)
HSG> set d15 identifier=15 enable_access_path=(MOL1A1,MOL1RB2,SHER1A1,SHER1B2)
HSG> set d16 identifier=16 enable_access_path=(MOL1A1,MOL1RB2,SHER1A1,SHER1B2)
```

### 4.2.4.6 为“重要”文件系统构建 RAID 组

正如我们早期提到的，所有重要的文件系统都可以从使用 RAID 组中受益，包括用户区域、应用程序数据以及数据库所需的文件系统。

在任何情况下，RAID 组的创建和分配都需要仔细的规划。如果你投入时间进行规划，可以保证在可用性和扩展性方面获得巨大的回报。

### 4.2.4.7 RAID 组的备用组

在结束 RAID 配置的章节之前，让我们讨论最后一个经常被忽视的话题——使用组来支持 RAID 配置。我们已经看到许多情况下，RA 配置的实现非常有益。请记住，任何在控制器上构建的 RAID 组都应该包含一个备用组。备用组硬盘的作用是什么？如果 RAID 组的成员硬盘发生故障，备用组中的良好硬盘会自动取代故障硬盘。这是一个经常被忽视的高可用性问题之一。

以下是向备用组添加磁盘的示例。

```
HSG> add sparset disk20400
HSG> add sparset disk20400
```

### 4.2.4.8 在控制台查看存储设备 – wwidmgr

现在我们已经为集群系统磁盘配置了所有存储组，将来会有某个时刻，我们需要从控制台查看并访问每个集群成员的启动分区或启动磁盘。遗憾的是，这不是自动发生的。什么时候需要这样做？在完成 Tru64 UNIX 的安装和配置之后，但在安装 TruCluster Server 之前。在 TruCluster Server 的安装和运行期间，必须从每个集群成员的控制台查看并访问其启动磁盘。

我们将从控制台使用 `wwidmgr` 查看并使每个集群成员启动磁盘可见。如何操作以及我们到底在寻找什么？我们在寻找在 RAID 存储阵列创建的集群成员启动分区的标识符或 UUID。

在使用 `wwidmgr` 命令之前，请注意，如果集群成员是 AS1200、AS4x00、AS8x00、GS60、GS60E 或 GS140，控制台必须设置为诊断模式。

> 9 这仅适用于基于光纤的存储（HSG60 或 HSG80 控制器）。如果使用 SCSI 存储，可以跳过此步骤。

# 82

```
P00>>> set mode diag
```

```
Console is in diagnostic mode
```

在使用 `widmgr` 命令后，必须重新初始化系统以返回 SRM 控制台。这是通过控制台上的 `init` 命令完成的。

以下示例展示了我们如何发现并使集群成员的启动磁盘可见。此示例假设之前尚未安装集群。

此外，为了本示例，我们感兴趣的集群成员启动磁盘标识符为 1，它映射到存储单元 D1。

- 在系统控制台处显示设备。

```
P00>>> show dev
dck0.0.0.7.0     DKCO            RZ2DD-LS 0306
dqa0.0.0.105.0   DQAO            CD-224E 9.5B
dva0.0.0.0.0     DVAO            00-50-SB-AE-F3-23
eia0.0.0.9.1     EIAO            WWN 2000-0000-c924-7c58
pga0.0.0.7.1     PGAO
pka0.0.0.6.6       PKA0            SCSI Bus 7
pkb0.7.0.106.0   PKBO            SCSI Bus 7
pck0.7.0.7       PKCO            SCSI Bus 7
...
```

- 使用 `widmgr` 清除任何 wwid 条目并检查设备的可达性。

```
P00>>> widmgr -clear all
```

```
P00>>> init
```

```
P00>>> show ww*
wwid0
wwid1
wwid2
wid3
```

```
P00>>> show n*
N1
N2
N3
N4
```

"`widmgr -clear all`" 命令清除了存储的光纤通道变量 `wwid1`、`wwid2`、`wwid3`、`wwid4`、`N1`、`N2`、`N3` 和 `N4`。

# 第 4 章

```
P00>> wwidmgr -show reachability
初始化后的磁盘分配和可达性:
```

```
P00>> init
```

- 显示由 `wwidmgr` 发现的设备。

```
P00>> wwidmgr -show wwid
[0] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1420-0755-0048(ev:none)
[1] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-0755b(ev:none)
[2] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-0746(ev:none)
[3] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-004b(ev:none)
[4] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-0049(ev:none)
[5] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-1425-0747(ev:none)
[6] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-9216-0029(ev:none)
[7] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-0926-0055f(ev:none)
[8] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-9216-0028(ev:none)
[9] UUID: WWID:01000010:6000-1fe1-0001-6950-0089-9210-0827(ev:none)
```

我们感兴趣的设备标识符为 1，与 UUID 为 1 的条目相同。

- 使用 `wwidmgr` 命令使我们感兴趣的设备可访问，以便我们最终能够从中启动。

```
P00>> wwidmgr -quickset -item 0 -unit 1
```

```
P00>> init
```

"`wwidmgr -quickset`" 命令实际上设置了 "`wwid*`" 和 "`N*`" 控制台变量。

- 验证我们使用的 `wwidmgr -show wwid`
