

集群包含八个投票成员，并配置了一个投票仲裁磁盘。鉴于此配置，CEV 值为 9，这意味着形成仲裁所需的票数将为 5。由于集群成员的 50% 崩溃，集群当前的 votes 值为 5（4 个投票成员和仲裁磁盘）。

如果再出现一次故障，集群将失去仲裁。由于宕机的成员在一段时间内不会通电，我们希望通过降低形成集群所需的成员数量来调整 CEV 值，从而提高集群的可用性。

你可以使用带有 “-e” 选项的 clu_quorum 命令来调整 cluster_expected_votes 属性（以及集群当前的预期票数值）。

```
clu_quorum -e #votes
```

#votes 参数不能设置为会导致集群失去仲裁的任何值。

```
# clu_quorum -e 12

*** Error ***
The requested expected vote adjustment would result in an
expected votes value of '12'. This value would cause all members of the
current cluster configuration to lose quorum.
```

#votes 参数不能设置为低于当前 votes 值减一的任何值。这会增加集群分区的可能性，这是不好的。

在我们的示例中，当前 votes 值为 5，因此低于 4 的任何值都是非法的。

```
# clu_quorum -e 3

*** Error ***
The requested expected vote adjustment would result in an illegal
expected votes value of '3'. This value is too low.
```

#votes 参数不能设置为零。

```
# clu_quorum -e 0

*** Error ***
Expected Votes cannot be set to 0 (Zero).
```

#votes 参数通常可以设置为当前 votes 的 +/-1，前提是不会失去仲裁。我们将预期票数设置为当前 votes 值。

```
# clu_quorum -e 5

Collecting quorum data for Member(s): 1 2 3 4 5 6 7 8

*** Error ***
One or more cluster members are DOWN. You may use the -f option to force the
quorum operation.
```

由于某些成员宕机，我们将需要使用 “-f” 选项。

```
# clu_quorum -f -e 5

Collecting quorum data for Member(s): 1 2 3 4 5 6 7 8

Expected vote successfully adjusted.
```

如前所述，clu_quorum 命令会修改每个成员的 syncftab 文件中的 cluster_expected_votes 值以及 /etc/sysconfigtab.cluster 文件（一个集群公共文件）。

## 17.8.3 管理仲裁磁盘

我们之前提到过，添加仲裁磁盘是通过向集群当前的 votes 值添加一票来提高集群可用性的一种方法。我们还提到，仲裁磁盘应仅在具有偶数个成员的集群中使用。

这如何提高集群的可用性？让我们看看。图 17-13 显示了一个未配置仲裁磁盘的四成员集群。

如果我们失去一个成员，是否会失去仲裁？由于一图胜千言，让我们看看图 17-14 有什么说法。

到目前为止，一切都很好。一个成员宕机，但由于当前 votes 等于仲裁 votes，集群将继续运行。现在，让我们再关闭一个成员。

我们已失去仲裁，因此集群被挂起（见图 17-15）。

![](img/a0df85c2e542a8d6c913113908553aa4_516_0.png)

### 图 17-14：无仲裁磁盘的四成员集群 – 一个成员宕机

![](img/a0df85c2e542a8d6c913113908553aa4_517_0.png)

### 图 17-15：无仲裁磁盘的四成员集群 – 两个成员宕机

![](img/a0df85c2e542a8d6c913113908553aa4_517_1.png)

### 图 17-16：带仲裁磁盘的四成员集群

![](img/a0df85c2e542a8d6c913113908553aa4_517_2.png)

好的，让我们再试一次，这次使用仲裁磁盘。我们将从图 17-16 开始。

有什么不同？嗯，集群的预期 votes 以及当前 votes 都增加了，但仲裁 votes 保持不变。你可能已经看出接下来会怎样。让我们快进到之前相同的场景——两个成员宕机。这次我们会失去仲裁吗？我们提供图 17-17 供您审阅。

具有偶数个成员并带有仲裁磁盘的集群具有更高的可用性。

