

## 17.8 管理仲裁

当你使用 `clu_add_member(8)` 命令向集群添加成员，或使用 `clu_delete_member(8)` 命令从集群中移除成员时，投票会自动调整以维持仲裁。通常这就足够了；然而，可能存在需要更改集群预期投票数或某个成员投票数的情况（例如，如果你需要为预防性维护而移除多个集群成员）。如果确实需要管理上修改投票，你应该使用 `clu_quorum(8)` 命令。

### 17.8.1 查看仲裁状态

判断是否拥有仲裁的最简单方法是查看你是否可以登录系统（或如果你已登录，查看在输入命令时系统是否做出响应）。撇开显而易见的情况不谈，你可能想了解集群当前的投票和仲裁状态。你可以不带任何命令选项使用 `clu_quorum` 命令。

```
# clu_quorum
Cluster Quorum Data for: babylon5 as of Thu Jan 10 03:37:04 EST 2002

Cluster Common Quorum Data
Quorum disk:    dsk4h
File:          /etc/sysconfigtab.cluster

Attribute                         File Value
expected votes                              3

Member 1 Quorum Data
Host name:       molnari.tcrchb.com          Status: UP
File:            /cluster/members/member1/boot_partition/etc/sysconfigtab

Attribute              Running Value       File Value
current votes                  3                 N/A
quorum votes                   2                 N/A
expected votes                 3                   3
node votes                     1                   1
qdisk votes                    1                   1
qdisk major                   19                  19
qdisk minor                  112                 112

Member 2 Quorum Data
Host name:       sheridan.tcrchb.com          Status: UP
File:            /cluster/members/member2/boot_partition/etc/sysconfigtab

Attribute              Running Value       File Value
current votes                  3                 N/A
quorum votes                   2                 N/A
expected votes                 3                   3
node votes                     1                   1
qdisk votes                    1                   1
qdisk major                   19                  19
qdisk minor                  112                 112
```

从 `clu_quorum` 命令的输出中，你可以看到我们的集群已配置了仲裁磁盘。此外，你可以看到集群当前正在使用的值（“Running Value”）以及成员下次启动时将使用的值（“File Value”）。

`clu_quorum` 命令从成员的 sysconfigtab 文件中获取“File Value”信息，如其所示，但“Running Value”来自哪里？此信息存储在连接管理器（cnx）内核子系统中。

#### 17.8.1.1 cnx 子系统

cnx 子系统包含系统当前正在使用的属性。

```
# sysconfig -q cnx

cnx:
name = Connection Manager
version = 1
cluster_name = babylon5
cluster_founder_cs id = 65537
node_cnt = 2
has_quorum = 1
qdisk_trusted = 1
member_cnt = 2
current_votes = 3
expected_votes = 3
quorum_votes = 2
qdisk_major = 19
qdisk_minor = 112
qdisk_votes = 1
mem_seq = 2
add_seq = 2
rem_seq = 0
node_id = 2
node_name = sheridan
node_cs id = 65537
node_votes = 1
node_expected_votes = 3
msg_level = 1
```

正如输出所示，`clu_quorum` 命令的“Running Value”中的所有属性（以及更多）都已表示出来。

有关 cnx 子系统的更多信息，请参阅 sys_attrs_cnx(5) 参考页。

#### 17.8.1.2 sysconfigtab 文件和 clubase 子系统

集群基础（clubase）子系统包含定义集群的属性，如 17.2.6 节所述。这些属性在系统启动时从系统的 sysconfigtab 文件加载。虽然属性值可以在成员的 sysconfigtab

