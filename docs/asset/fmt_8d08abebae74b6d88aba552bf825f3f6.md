
## 表 5.3 DB2 9 快照监控管理表和 SQL 表函数（续）

| 管理视图 | 表函数 | 描述 |
|---|---|---|
| `SYSIBADM.PLICATIONS` | N/A | 该管理视图包含连接数据库应用程序的信息。 |
| `SYSIBADM.APPL_PERFORMANCE` | N/A | 该管理视图包含每个应用程序的选择行数与读取行数的速率。 |
| `SYSIBADM.BP_HITRATIO` | N/A | 该管理视图包含缓冲池命中率，包括总计、数据和索引。 |
| `SYSIBADM.BP_READ_IO` | N/A | 该管理视图包含缓冲池读取性能信息。 |
| `SYSIBADM.BP_WRITE_IO` | N/A | 该管理视图包含缓冲池写入性能信息。 |
| `SYSIBADM.CONTAINER_UTILIZATION` | N/A | 该管理视图包含表空间容器和利用率的信息。 |
| `SYSIBADM.LOCKS_HELD` | N/A | 该管理视图包含当前持有锁的信息。 |

| 管理视图 | 表函数 | 描述 |
|---|---|---|
| `SYSIBMADM.LOCKWAITS` | N/A | 此管理视图包含等待授予的锁的信息。 |
| `SYSIBMADM.LOG_UTILIZATION` | N/A | 此管理视图包含关于当前连接数据库的日志使用情况的信息。 |
| `SYSIBMADM.LONG_RUNNING_SQL` | N/A | 此管理视图包含当前连接数据库中运行时间最长的 SQL 语句的信息。 |
| `SYSIBMADM.QUERY_PREP_COST` | N/A | 此管理视图包含 SQL 语句列表，以及关于准备每个语句所需时间的信息。 |
| N/A | `SNAP_WRITE_FILE()` | 此过程将系统快照数据写入该目录下 tmp 子目录中的文件中。 |
| `SYSIBMADM.SNAPAGENT` | `SNAP_GET_AGENT()` | 此管理视图和表函数返回来自应用程序快照的代理信息——特别是代理逻辑数据组。 |
| `SYSIBMADM.SNAPAGENT_MEMORY_POOL` | `SNAP_GET_AGENT_MEMORY_POOL()` | 此管理视图和表函数返回代理级别的内存使用信息。 |
| `SYSIBMADM.SNAPAPP` | `SNAP_GET_APPL()` | 此管理视图和表函数返回来自应用程序快照的应用程序信息——特别是 appl 逻辑数据组。 |
| `SYSIBMADM.SNAPAPPL_INFO` | `SNAP_GET_APPL_INFO()` | 此管理视图和表函数返回来自应用程序快照的应用程序信息——特别是 appl_info 逻辑数据组。 |
| `SYSIBMADM.SNAPBP` | `SNAP_GET_BP()` | 此管理视图和表函数返回来自缓冲区快照的缓冲区池信息——特别是 bufferpool 逻辑数据组。 |
| `SYSIBMADM.SNAPBP_PART` | `SNAP_GET_BP_PART()` | 此管理视图和表函数返回来自缓冲区快照的缓冲区池信息——特别是 bufferpool_nodeinfo 逻辑数据组。 |
| `SYSIBMADM.SNAPCONTAINER` | `SNAP_GET_CONTAINER_V91()` | 此管理视图和表函数返回来自 tablespace_container 逻辑数据组的表空间快照信息。 |

## 第 5 章：分析 DB2 活动

## 表 5.3 DB2 9 快照监控管理表和 SQL 表函数（续）

| 管理视图 | 表函数 | 描述 |
| --- | --- | --- |
| `SYSIBMADM.SNAPDB` | `SNAP_GET_DB_V91()` | 此管理视图和表函数返回来自数据库 (dbase) 和数据库存储 (db_storage_group) 逻辑分组的快照信息 |
| `SYSIBMADM.SNAPDB_MEMORY_POOL` | `SNAP_GET_MEMORY_POOL()` | 此管理视图和表函数仅限 UNIX(R) 平台返回数据库层的内存使用信息。 |
| `SYSIBMADM.SNAPDBM` | `SNAP_GET_DBM()` | 此管理视图和表函数返回 DB2 数据库管理器 (dbm) 逻辑分组信息 |
| `SYSIBMADM.SNAPDBM_MEMORY_POOL` | `SNAP_GET_DBM_MEMORY_POOL()` | 此管理视图和表函数返回数据库管理器的内存使用信息。 |
| `SYSIBMADM.SNAPDETAILLOG` | `SNAP_GET_DETALLOG_V91()` | 此管理视图和表函数返回来自 detail_log 逻辑数据组的快照信息。 |
| `SYSIBMADM.SNAPDYN_SQL` | `SNAP_GET_SQL_V91()` | 此管理视图和表函数返回来自 dysql 逻辑数据组的快照信息。 |
| `SYSIBMADM.SNAPFCM` | `SNAP_GET_FCM()` | 此管理视图和表函数返回来自数据库管理器快照的快速通信管理器 (FCM) 信息——特别是 fcm 逻辑数据组。 |
| `SYSIBMADM.SNAPFCM_PART` | `SNAP_GET_FCM_PART()` | 此管理视图和表函数返回来自数据库管理器快照的快速通信管理器 (FCM) 信息，特别是 fcm 逻辑数据组。 |
| `SYSIBMADM.SNAPHADR` | `SNAP_GET_HADR()` | 此管理视图和表函数返回来自数据库快照的高可用灾备恢复 (HADR) 信息——特别是 HADR 逻辑数据组。 |
| `SYSIBMADM.SNAPLOCK` | `SNAP_GET_LOCK()` | 此管理视图和表函数返回关于锁的快照信息——特别是 lock 逻辑数据组。 |
| `SYSIBMADM.SNAPLOCKWAIT` | `SNAP_GET_LOCKWAIT()` | 此管理视图和表函数返回关于锁等待的快照信息——特别是 lockwait 逻辑数据组。 |

## 表 5.3 DB2 9 快照监控管理表和 SQL 表函数（续）

| 管理视图 | 表函数 | 描述 |
|---|---|---|
| `SYSIBMADM.SNAPSTMT` | `SNAP_GET_STMT()` | 此管理视图和表函数返回来自应用程序快照的语句信息。 |
| `SYSIBMADM.SNAPSTORAGE_PATHS` | `SNAP_GET_STORAGE_PATHS()` | 此管理视图和表函数返回数据库自动存储路径列表，包括每个存储路径的文件系统信息——特别是来自 db_storage_group 逻辑数据组。 |
| `SYSIBMADM.SNAPSUBSECTION` | `SNAP_GET_SUBSECTION()` | 此管理视图和表函数返回关于子集的信息。 |
| `SYSIBMADM.SNAPSWITCHES` | `SNAP_GET_SWITCHES()` | 此管理视图和表函数返回关于开关的信息——即 switch 逻辑组。 |
| `SYSIBMADM.SNAPTAB` | `SNAP_GET_TAB_V91()` | 此管理视图和表函数返回来自表的快照信息。 |
| `SYSIBMADM.SNAPTAB_REORG` | `SNAP_GET_REORG()` | 此管理视图和表函数返回关于重组的信息。 |
| `SYSIBMADM.SNAPBSP` | `SNAP_GET_BSP()` | 此管理视图和表函数返回来自表的快照信息。 |
| `SYSIBMADM.SNAPBP_PART` | `SNAP_GET_BP_PART()` | 此管理视图和表函数返回来自 tablespace_nodeinfo 逻辑数据组的快照信息。 |
| `SYSIBMADM.SNAPAPQUIESER` | `SNAP_GET_QUIESER()` | 此管理视图和表函数返回关于静止的信息。 |
| `SYSIBMADM.SNAPRANGE` | `SNAP_GET_RANGE()` | 此管理视图和表函数返回来自范围的信息。 |
| `SYSIBMADM.SNAPUTIL` | `SNAP_GET_UTIL()` | 此管理视图和表函数返回关于实用程序的信息。 |
| `SYSIBMADM.SNAPUTIL_PROGRESS` | `SNAP_GET_PROGRESS()` | 此管理视图和表函数返回关于实用程序进度的信息——特别是 progress 逻辑数据组。 |
| `SYSIBMADM.TBSP_UTILIZATION` | N/A | 此管理视图包含表空间配置和使用率信息。 |
| `SYSIBMADM.TOP_DYNAMIC_SQL` | N/A | 此管理视图包含顶级 SQL 语句，可以按执行次数、平均执行时间、排序次数或每个语句排序次数进行排序。 |

数据库系统监控 365 或

```
RESET MONITOR FOR <UCS> [DATABASE | DB] [DatabaseAlias]
```

其中：

`DatabaseAlias` 标识为要重置快照监控计数器的数据库分配的别名。

因此，如果您想将某个实例控制下的所有数据库的快照监控计数器重置为零，可以通过连接到该实例并执行如下所示的 `RESET MONITOR` 命令来实现：
