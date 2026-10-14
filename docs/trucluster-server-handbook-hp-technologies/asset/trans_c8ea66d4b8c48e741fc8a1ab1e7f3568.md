

file，如果不重启系统，这些更改不会反映在 clu base 子系统中。这并不是什么大问题，因为这些属性仅用于配置或加入集群。系统的运行值存储在 cnx 子系统中，正如我们在上一节讨论的那样。

下面是一个示例，说明 sysconfigtab 文件可能与 clu base 子系统所能看到的内容不同。我们启动了一个单成员集群。系统的 sysconfigtab 文件显示没有配置仲裁盘，并且 cluster_expected_votes 的值为 1。

```
# sysconfigdb -l clu base

clu base:
    cluster_expected_votes = 1
    cluster_quorum_conf_active = 0
    cluster_qdisk_major = 0
    cluster_qdisk_minor = 0
    cluster_qdisk_votes = 0
    cluster_name = babylon5
    cluster_node_name = molari
    cluster_node_inter_name = molari-ics0
    cluster_node_votes = 1
    cluster_interconnect = mct
    cluster_seqdisk_major = 19
    cluster_seqdisk_minor = 96
```

系统上的 clu base 子系统确认了这些值。

```
# sysconfig -q clu base cluster_expected_votes \
> cluster_qdisk_major cluster_qdisk_minor cluster_qdisk_votes

clu base:
    cluster_expected_votes = 1
    cluster_qdisk_major = 0
    cluster_qdisk_minor = 0
    cluster_qdisk_votes = 0
```

我们现在将再添加一个集群成员以及一个仲裁盘。要添加第二个成员，我们将使用 clu_add_member(8) 命令，正如我们在第 11 章讨论的那样。我们将在第 17.8.3.1 节讨论如何添加仲裁盘。为了节省篇幅，我们这里不显示输出，而是说明这些操作如何影响集群。

查看在添加了仲裁盘和成员后我们成员上的 clu base 子系统，可以看到没有任何变化。

```
# sysconfig -q clu base cluster_expected_votes \
> cluster_qdisk_major cluster_qdisk_minor cluster_qdisk_votes

clu base:
    cluster_expected_votes = 1
    cluster_qdisk_major = 0
    cluster_qdisk_minor = 0
    cluster_qdisk_votes = 0
```

然而，sysconfigtab 文件确实反映了最近的更改。

```
# sysconfigdb -l clu base | grep -E "expected|_qdisk"
cluster_expected_votes = 3
cluster_qdisk_major = 19
cluster_qdisk_minor = 112
cluster_qdisk_votes = 1
```

## CAUTION:

不要修改成员的 sysconfigtab 文件来调整投票。应使用 clu_quorum 命令。clu_quorum 命令包含逻辑以确保你不会尝试设置会导致集群失去仲裁的值。此外，它还会确保每个成员的 cluster_expected_votes 值相同。

另一个重要点是，cluster_expected_votes 属性也存储在集群公共文件 /etc/sysconfigtab.cluster 中。clu_quorum 命令也会确保该文件得到正确更新。

你也可以使用带 “-v” 选项的 clu_quorum 命令来查看 clu base 子系统的值。它们位于 “Booted Value” 字段下。参见图 17-12。

当 molari 启动时，cluster_expected_votes 为 1，并且未配置仲裁盘。在执行 clu_add_member 命令后，你可以看到 sheridan 的 cluster_expected_votes 值为 2。最后，在 sheridan 启动后我们添加了仲裁盘。我们之所以知道这一点，是因为 “Running Value” 和 “File Value” 都表明已配置仲裁盘，但两个成员的 “Booted Value” 都未显示仲裁盘。

## NOTE:

clu_quorum 命令会将更改记录到位于 /cluster/admin 目录的 clu_quorum.log 文件中。

## 17.8.2 Modifying Votes

有时可能需要将成员的状态从投票成员（即拥有 1 票的成员）更改为非投票成员（即拥有零票的成员）。

为什么要将成员更改为非投票成员？每当系统将从集群中临时但长时间移除时，调整形成和维护集群所需的票数是个好主意。你可以使用 clu_delete_member(8) 命令删除该成员，但这会过度处理。通过将成员设为非投票成员，集群的预期票数也会减少一。

