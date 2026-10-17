
| PrimaryFile PrimaryPg PrimaryLSN | | | | |

| S000031.LOG 289 | 0x0000000000890D9F3B | | | |

| StandByFile StandByPg StandByLSN | | | | |

| S000031.LOG 289 | 0x0000000000890D9F3B | | | | |

示例 4-3 显示了使用 `db2pd` 命令获取 HADR 备服务器（POLONIUM）上 SAMPLE 数据库的 HADR 信息的输出。

### 示例 4-3 POLONIUM（备节点）的 db2pd 输出

```
db2inst1@> db2pd -d sample -hadr
```

Database Partition 0 -- Database SAMPLE -- Active -- Up 1 days 01:54:36

HADR Information:

Role State SyncHeartbeatsMissed LogGapRunAvg(bytes)

Standby Peer Sync 0 0

ConnectStatus ConnectTime Timeout

Connected Tue Oct 31 14:37:16 2006 (1162334236) 3

LocalHost LocalService

polonium DB2_HADR_2

RemoteHost RemoteService RemoteInstance

LEAD DB2_HADR_1 db2inst1

PrimaryFile PrimaryPg PrimaryLSN

S000031.LOG 289 00000000008909F3B

StandByFile StandByPg StandByLSN

S000031.LOG 289 00000000008909F3B

正如预期的的一样，`db2pd` 在 HADR 主节点和备节点上的输出存在差异和相似之处。在我们的示例中（参见第 101 页的示例 4-2 和上面的示例 4-3），唯一的明显区别是——除了 HADR 角色为 Primary 且 POLONIUM 为 Standby 之外——`LocalHost`、`LocalService` 监控元素的值与 `RemoteHost` 和 `RemoteService` 交换了位置。

在长时间运行的 HADR 对中，经过多次日志写入和 HADR 停止/启动活动后，主节点和备节点的日志信息（`PrimaryFile`、`StandByFile`、`PrimaryPg`、`StandByPg`、`PrimaryLSN`、`StandByLSN`）可能会有所不同。尽管如此，在 HADR 状态为 Peer 时，主节点上 `db2pd` 命令显示的每个值的输出必须与此时在备节点上运行 `db2pd` 命令显示的该值匹配。也就是说，如果主节点的 `db2pd` StandBy 输出为 289，那么备节点的 `db2pd` StandBy 输出也应为 289，即使 `PrimaryPg` 是其他值。

你可能还会注意到，当 HADR 状态为 Peer 时，`LogGapRunAvg` 值并不是 0 字节。`LogGapRunAvg` 值实际上代表了主节点和备节点最后一次通信时 LSN 之间的平均差异。如果主日志由于某种原因被截断，则会出现一个差异，即主节点移动到了下一个日志，而备节点仍留在最后一个日志。这个差异会在主节点写入下一个日志后关闭。

关于 `db2pd` 和 HADR 监控的更多信息，请参考以下资源：

- DB2 9.1 Data Recovery and High Availability Guide and Reference, SC10-428
- DB2 9.1 Command Reference, SC10-226
- System Monitor Guide and Reference, SC10-251

### 4.4 监控 HADR：管理视图和表函数

在 DB2 9 中，查看各种 R 监控元素的新方法是使用管理视图或表函数。监控元素是 DB2 内部监控的各种属性。也就是说，它们在相关事件发生时更新值。这些监控元素被称为逻辑数据组（logical groups）。

对于 DB2 9 中的 HADR 逻辑数据组，管理视图和表函数允许应用程序和脚本使用简单的 SQL 查询获取每个 HADR 监控元素的单值（而不是编写复杂的字符串处理程序或使用 `awk` 和 `grep` 来提取 `db2pd` 的多列输出）。

示例 4-4 和示例 4-5 显示了有效获取相同结果、特别是 `HADR_STATE` 监控值的语法。

#### 示例 4-4 获取 HADR_STATE 的 SQL 函数

```
HADR_STATE
-------
PEER
record(s) selected.
```

#### 示例 4-5 获取 HADR_STATE 的管理视图

```
> db2 select HADR_STATE from sysibm.snaphadr
```

HADR_STATE

-------

PEER

record(s) selected.
