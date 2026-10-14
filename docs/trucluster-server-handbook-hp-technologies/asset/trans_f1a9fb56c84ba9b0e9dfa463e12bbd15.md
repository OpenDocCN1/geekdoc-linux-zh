

# clu quorum -v
集群仲裁数据 for: babylon5 于 Wed Jan 23 04:48:03 EST 2002

## Cluster Common Quorum Data

仲裁磁盘: dsk4h
文件: /etc/sysconfigtab.cluster

| Attribute | File Value |
|---|---|
| expected votes | 3 |

## Member 1 Quorum Data

主机名: molari.tcrhb.com          状态: UP
文件: /cluster/members/member1/boot_partition/etc/sysconfigtab

| Attribute | Running Value | File Value | Booted Value |
|---|---:|---:|---:|
| current votes | 3 | N/A | N/A |
| quorum votes | 2 | N/A | N/A |
| expected votes | 3 | 3 | 1 |
| node votes | 1 | 1 | 1 |
| qdisk votes | 1 | 1 | 0 |
| qdisk major | 19 | 19 | 0 |
| qdisk minor | 256 | 256 | 0 |

## Member 2 Quorum Data

主机名: sheridan.tcrhb.com          状态: UP
文件: /cluster/members/member2/boot_partition/etc/sysconfigtab

| Attribute | Running Value | File Value | Booted Value |
|---|---:|---:|---:|
| current votes | 3 | N/A | N/A |
| quorum votes | 2 | N/A | N/A |
| expected votes | 3 | 3 | 2 |
| node votes | 1 | 1 | 1 |
| qdisk votes | 1 | 1 | 0 |
| qdisk major | 19 | 19 | 0 |
| qdisk minor | 256 | 256 | 0 |

cnx — sysconfigtab — clubase

Figure 17-12: "clu_quorum -v" explained

## IMPORTANT:

如果将一个成员变为非投票成员导致集群拥有奇数个投票成员，你还应将仲裁磁盘的投票调整为零（或暂时从集群中移除仲裁磁盘）。请参阅第 17.8.3 节了解有关管理仲裁磁盘的更多信息。

### 17.8.2.1 How to Adjust a Member's Votes

你可以使用带有 "-m" 选项的 clu_quorum 命令来调整成员可以贡献的投票数。

```
clu_quorum -m member_name #votes
```

截至本文撰写时，#votes 参数的唯一可接受值是 0 或 1。

```
# clu_quorum -m molari 0
Collecting quorum data for Member(s): 1 2

Member votes successfully adjusted.
```

要验证投票是否已更改，可以发出以下命令：

```
# clu_get_info -m 1 -full | grep -E "Hostname|votes"

Hostname = molari.tcrhb.com
Member votes = 0
```

clu_get_info(8) 命令的 “-m 1” 选项获取 member1 的信息。注意两个命令中 “-m” 选项的细微差别 -- clu_quorum 使用成员的名称，而 clu_get_info 使用 memberid。由于这种不一致，可能更容易坚持使用不带选项的 clu_quorum 命令。

```
# clu_quorum | grep -E "^Host|^node|Running"

Host name:       molari.tcrhb.com                 Status:              UP
Attribute                 Running Value             File Value
node votes                         0                       0
Host name:       sheridan.tcrhb.com                Status:              UP
Attribute                 Running Value             File Value
node votes                         1                       1
```

为了调整成员的投票，集群必须能够访问该成员的 boot_partition。然而，如果成员处于关闭状态，boot_partition 将被卸载。如果成员处于关闭状态，但集群中至少有一个成员可以物理访问该成员的启动磁盘，你可以向 clu_quorum 命令添加 “-f” 选项以“强制”操作。“-f” 选项会挂载成员的 boot_partition，修改 sysconfigtab 文件，然后卸载成员的 boot_partition。这就是为什么成员启动磁盘应可被多个集群成员访问的一个好理由。如果成员处于关闭状态，clu_quorum 命令会通知你。

```
# clu_quorum -m molari 1
Collecting quorum data for Member(s): 1 2

*** Error ***
One or more cluster members are DOWN. You may use the -f option to force the quorum operation.
```

添加 “-f” 选项后，clu_quorum 命令会成功完成。

```
# clu_quorum -f -m molari 1
Collecting quorum data for Member(s): 1 2

Member votes successfully adjusted.
```

你也可以使用 “-f” 选项查看已关闭系统的 sysconfigtab 值。

```
# clu_quorum -f | grep -E "^Host|^node|Value" | tail -6
Host name: molari.tcrhb.com Status: DOWN
Attribute File Value
node votes 3
Host name: sheridan.tcrhb.com Status: UP
Attribute Running Value File Value
node votes 1 1
```

### 17.8.2.2 How to Adjust the Cluster’s Expected Votes

用于确定集群的仲裁投票（形成集群和保持集群运行所需的投票数）的就是集群的预期投票（CEV）值。

一旦集群形成，如果成员加入或离开集群，CEV 值不会被降低。请记住，CEV 值等于以下各项的最大值：

- 之前的 CEV 值。这是当前集群 incarnation 中上一次状态转换时计算的 CEV 值。
- 所有成员的 cluster_expected_votes 值中的最大值。该值应在每个成员上相同。
- 所有 cluster_node_votes 的总和，加上 cluster_qdisk_votes（如果仲裁磁盘已配置并分配了投票）。

那么如果足够多的集群成员发生故障，以至于再发生一次故障就会导致集群失去仲裁会发生什么？

降低 CEV 值只有两种方法。你可以使用 clu_delete_member 命令删除一个成员，或使用带有 “-e” 选项的 clu_quorum 命令。

例如，假设一场雷暴袭击了包含一个集群的建筑物，导致 50% 的集群成员崩溃。由于雷暴的严重性，为这些成员供电的变压器停止工作，导致这些成员在不确定的时间内处于关闭状态。

