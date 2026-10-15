
|---|---|---|---|---|

| ClientPid LkMot DBName | | | | |

| 0x0000002000000041235219 | 29568 | 0xF197AE61 | 0 | |

| Inst-Agent 9045 | db2bp | 131 | | NotSet ITSODB |

| 0x0000002223c140 | 1056 | [000-0156] | 554 | Coord |

| Inst-Agent 9045 | db2tskd | 2 | | NotSet ITSODB |

| 0x0000002007c008 | 1057 | [000-0157] | 555 | Coord |

| Inst-Agent 9045 | db2wlmd | | | NotSet ITSODB |

| 0x0000002223ac80 | 1058 | [000-0156] | 555 | Coord |

| Inst-Agent 9045 | db2evmg_ | | | 3 |

| 0x00000020007c1540 | 1054 | [000-0000] | 557 | Coord | Pooled |

| n/a | n/a | | 0 | | |

| 0x00000020007c2a00 | | [000-0000] | 558 | Coord | Pooled |

| n/a | n/a | n/a | | 0 | | NotSet ITSODB |

## db2pd 命令

我们已经展示了带有 `-memsets`、`-osinfo` 和 `-agents` 选项的 `db2pd`。在下面的列表中，我们提供了该工具的更多示例以及你可以检索的信息类型：

* - 所有数据库和实例范围的信息

  `db2pd -inst -allibs`

* - 活跃事务

  `db2pd -db itssob -transactions`

* - 锁

  `db2pd -db itssob -locks`

* - 特定应用程序：1072 是一个句柄

  `db2pd -db itssob -applications 1072`

* - 数据库日志

  `db2pd -db itssob -logs`

* - 围厂商进程（Fenced vendor process）

  `db2pd -db itssob -fvp 1lam`

该命令适用于备份、恢复、修剪历史、加载复制（滚动恢复）以及使用厂商媒体设备的日志管理器。

* - 为数据库定义的自动存储路径

  `db2pd -db itssob -storagepaths`

* - 表和数据分区重组

  `db2pd -db itssob -reorgs`

* - 表和索引统计

  `db2pd -db itssob -tbstats 7 4`

在之前的示例中，该命令返回了空间 ID 7 中表 ID 4 的信息。

还会返回 UPDATE、INSERT、DELETE (UDI) 的更新总数以及实时统计 UDI 计数器 (RTSDI)。UDI 是一个用于衡量自上次 RUSTATS 以来更改数据量的计数器。DB2 使用该值确定是否需要更新表的统计信息。

* - 列实例所有的引擎分发单元 (EDUs)

  `db2pd -edus`

在 DB2 9.5 版本中，DB2 引擎的实现已从进程模型演变为基于 Linux 和 UNIX 系统的线程模型。当使用 `-fu instancename` 调用 `ps` 命令时，输出仅列出两个 DB2 进程：`db2sysc` 和 `db2acd`。

要显示与 `db2sysc` 进程关联的各个线程，必须在 `ps` 命令上使用相应的线程选项。在 Linux 上，你可以使用 `-lfp` 选项，或使用带有新选项 `-edus` 的 `db2pd` 命令。

正如我们的示例所示，`db2pd` 命令是用于确定问题的极其强大的工具。使用 `db2pd -h` 查看所有选项。

更多示例和信息请参见《故障排除指南》(Troubleshooting Guide) GI11-7857，以及《DB2 Linux, UNIX 和 Windows 命令参考》SC23-5846-01。

## 7.5.3 DB2 snapshot 命令

与 `db2pd` 命令类似，你可以使用快照监控器在特定时间捕捉数据库及任何连接应用程序的信息。如果你定期间隔捕捉信息，快照对于观察趋势和不可预见的潜在问题也很有用。有多种快照请求类型，每个快照请求返回特定类型的监控数据。

在分区数据库环境中使用该命令时，可以在实例的任何分区或全局拍摄快照。全局快照聚合了在每个分区收集的数据并返回一组单一的值。示例 7-21 通过两个样本显示了差异。

> 示例 7-21 全局快照

```
db2inst1@mensa:> db2_all 'db2 get snapshot for all on itsoddb | grep 'Locks held currently'

Locks held currently = 1
mensa: db2 get snapshot for ... completed ok

Locks held currently = 8
gemini: db2 get snapshot for ... completed ok

db2inst1@mensa:> db2 get snapshot for all on itsoddb global | grep "Locks currently"
held currently = 9

db2inst1@mensa:> db2_all 'db2 get snapshot for all on itsoddb | grep "Lock list*'

Lock list memory in use (Bytes) = 5888
mensa: db2 get snapshot for ... completed ok
Lock list memory in use (Bytes) = 3392
gemini: db2 get snapshot for ... completed ok

db2inst1@mensa:> db2 get snapshot for all on itsdb global | grep "Lock list"
Lock memory in use (Bytes) = 9280
```

在 6.2.2 第 280 页“手动表维护”中，我们使用了 DB2 命令行 (CLP) 的 GET SNAPSHOT 命令来监控就地表重组。你可以从管理视图、SQL 表函数或通过在 C 或 C++ 应用程序中使用快照监控 API 来捕捉快照。

有多个快照管理视图供你查询快照信息。示例 7-22 显示了列表。

## 示例 7-22 Snapshot™ 管理视图

```
db2inst1@mens:> db2 select substr(tabchema,1,10) tabschema, substr(tabname,1,30) tabname from syscat.tabname like 'SNAP*'
```

| SYBSCHEMA | TABNAME |
|---|---|
| SYBSIMADM | SNAPAGENT |
| SYBSIMADM | SNAPAGENT_MEMORY_POOL |
| SYBSIMADM | SNAPAPPL |
| SYBSIMADM | SNAPAPP_INFO |
| SYBSIMADM | SNAPBP |
| SYBSIMADM | SNAPBP_PART |
| SYBSIMADM | SNAPCONTAINER |
| SYBSIMADM | SNAPDB |
| SYBSIMADM | SNAPDBM |
| SYBSIMADM | SNAPDB_MEMORY_POOL |
| SYBSIMADM | SNAPDB_MEMORY_POOL |
| SYBSIMADM | SNAPDETA |
| SYBSIMADM | SNAPFCM |
| SYBSIMADM | SNAPFCM_PART |
| SYBSIMADM | SNAPHOR |
| SYBSIMADM | SNAPLOCK |
| SYBSIMADM | SNAPWAIT |
| SYBSIMADM | SNAPSTMT |
| SYBSIMADM | SNAPSTORAGE_PATHS |
| SYBSIMADM | SNAPSECTION |
| SYBSIMADM | SNAPSWT |
| SYBSIMADM | SNAPTAB |
| SYBSIMADM | SNAP_REORG |
| SYBSIMADM | SNAPBSP_PART |
| SYBSIMADM | SNAP_QUIES |

在 6.2.2 第 280 页“手动表维护”中，我们使用了 DB2 命令行 (CLP) 的 GET SNAPSHOT 命令来监控就地表重组。你可以从管理视图、SQL 表函数或通过在 C 或 C++ 应用程序中使用快照 API 来捕捉快照。

有多个快照管理视图供你查询快照信息。示例 7-22 显示了列表。
