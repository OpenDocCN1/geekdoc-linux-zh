
## db2pd 命令选项

| `-version` | `-v` | 指定收集并显示已安装 DB2 产品的当前版本和服务级别。 |
| `-inst` |  | 指定收集并显示所有可用的实例级信息。 |
| `-alldatabases` | `-alldbs` | 指定实用程序连接到所有数据库的所有内存集。 |
| `-full` |  | 指定所有输出都扩展到最大长度。（如果未指定此选项，输出将被截断以节省显示空间。） |
| `-everything` |  | 指定使用所有选项，并对服务器本地的所有数据库分区上的所有数据库收集并显示所有信息。 |
| `-hadr` |  | 指定收集并显示关于高可用性灾难备备（HADR）的信息。 |
| `-utilities` |  | 指定收集并显示关于实用程序的信息。 |
| `-applications` |  | 指定收集并显示关于应用程序的信息。 |
| `-agents` |  | 指定收集并显示关于代理的信息。 |
| `-transactions` |  | 指定收集并显示活动事务的信息。 |
| `-bufferpools` |  | 指定收集并显示关于缓冲池的信息。 |
| `-logs` |  | 指定收集并显示关于日志的信息。 |
| `-locks` |  | 指定收集并显示锁的信息。 |
| `-tablespaces` |  | 指定收集并显示表空间的信息。 |
| `-dynamic` |  | 指定收集并显示动态 SQL 语句的信息。 |
| `-static` |  | 指定收集并显示静态 SQL 包的信息。 |
| `-fcm` |  | 指定收集并显示快速通信管理器的信息。 |
| `-memsets` |  | 指定收集并显示内存集的信息。 |
| `-mempools` |  | 指定收集并显示内存池的信息。 |
| `-memblocks` |  | 指定收集并显示内存块的信息。 |

### 表 5.10 db2pd 命令选项（续）

| 选项 | 含义 |
|---|---|
| `-dbmcfg` | 指定收集并显示当前数据库管理器配置设置。 |
| `-dbcfg` | 指定收集并显示当前数据库参数设置。 |
| `-catalogcache` | 指定收集并显示目录缓存的信息。 |
| `-tcbstats` | 指定收集并显示关于表和索引的信息。 |
| `-reorg` | 指定收集并显示关于表分区重组的信息。 |
| `-recovery` | 指定收集并显示关于恢复活动的信息。 |
| `-reopt` | 指定收集并显示使用 REOPT 重新优化的缓存语句的信息。 |
| `-osinfo` | 指定收集并显示操作系统信息。 |
| `-storagepaths` | 指定收集并显示数据库定义的自动存储路径的信息。 |
| `-pages` | 指定收集并显示缓冲池页的信息。 |
| `-stack` | 指定收集并显示堆栈跟踪信息。 |
| `-repeat` | 指定在指定的秒数后按指定的次数重复命令。 |
| `-command` | 指定执行存储在文件中的 `db2pd` 命令。 |
| `-file` | 指定将收集的所有信息写入文件。 |
| `-interactive` | 表明在运行 `db2pd` 命令时将覆盖环境变量 `DB2OPT` 指定的值值。 |
| `-help` | `-h` | 显示帮助信息。当指定此选项时，所有其他选项将被忽略，仅显示帮助信息。 |

## 练习题

### 第 1

用户执行了以下命令：

```sql
UPDATE DBM CFG USING DFT_MON_SORT ON;
UPDATE MONITOR SWITCHES USING UOW ON;
UPDATE DBM CFG USING DFT_MON_TIMESTAMP ON;
UPDATE MONITOR SWITCHES USING BUFFERPOOL
```

假设没有设置其他监控开关，如果停止并重启 DB2 实例，哪一个数据库监控开关将被设置？

- A. SORT, UOW
- B. UOW, BUFFERPOOL
- C. SORT, TIMESTAMP
- D. TIMESTAMP, BUFFERPOOL

### 第 2

使用哪一个查询可以获取有关名为 `SAMPLE` 的 DB2 数据库定义的缓冲池使用情况的信息？

- A. `SELECT * FROM SNAPSHOT_INFO ('sample', BUFFERPOOL)`
- B. `SELECT * FROM SNAPSHOT_BP ('sample', -1)`
- C. `SELECT FROM TABLE(SNAPSHOT_INFO('sample', BUFFERPOOL)) AS snap_info`
- D. `SELECT * FROM TABLE(SNAP_GET_BP('sample', -1)) AS snap_info`

### 第 3

`RESET MONITOR` 命令的作用是什么？

- A. 将快照监控计数器重置为零。
- B. 将单个快照监控计数器重置为零。
- C. 关闭所有快照监控开关。
- D. 关闭除 TIMESTAMP 开以外的所有快照监控开关。

# 418 第 5 章：分析 DB2 活动

### 第 4

当多个应用程序与名为 `SAMPLE` 的数据库进行交互时，数据库管理员执行了以下命令：

```sql
GET SNAPSHOT FOR LOCKS ON sample
```

并收到以下输出：

```
Database name = SAMPLE
Database path = C:\DB2\NODE0000\SQL00002\
Database alias = SAMPLE
Locks held = 0
Applications currently connected = 1
Agents waiting on locks = 0
Snapshot timestamp = 05/14/2007 14:57:04.559027
Application handle = 110
Application ID = *LOCAL.DB2.07014185703
Sequence number = 00001
Application name = db2task
CONNECT Authorization ID = DBUSER
Application status = Connect Completed
Status change time = Not Collected
Application code page = 1252
Locks held = 0
Total wait time (ms) = Not Collected
```

为什么总锁等待时间返回值为 "Not Collected"？

- A. 在拍摄快照之前执行了 `RESET MONITOR` 命令
- B. 在拍摄快照时，`LOCK` 快照监控开关是关闭的。
- C. 在拍摄快照时没有持有锁。
- D. 在拍摄快照时，`UOW` 快照监控开关是关闭的。

### 第 5

关于 `DEADLOCKS` 事件监控器，以下哪一项不是正确的描述？

- A. 默认情况下，创建 DB2 9 数据库时会自动创建一个 `DEADLOCKS` 事件监控器。
- B. 一旦创建，默认的 `DEADLOCKS` 事件监控器无法删除。
- C. 在第一次连接到数据库时，默认的 `DEADLOCKS` 事件监控器会被激活。
- D. 事件监控数据在检测到死锁循环时收集。

# 练习题 419

### 第 6

在 `CREATE EVENT MONITOR` 语句中可以指定哪一个选项，以指示如果代理程序发现两个事件缓冲区已满，则其生成的每个受监控的事件无需等待事件缓冲区持久化到磁盘即可？

- A. `BLOCKED`
- B. `NONBLOCKED`
- C. `BUFFERED`
- D. `NONBUFFERED`

### 第 7

关于可以定义的事件监控器，以下哪一项不是正确的描述？

- A. 可以定义无限数量的事件监控器。
- B. 事件监控器在开始收集数据之前必须被激活。
- C. 同时最多有 16 个事件监控器激活。
- D. 激活的事件监控器在删除之前必须先停止。

### 第 8

使用健康中心（Health Center）可以执行哪些关键任务？

- A. 查看实例或数据库的警报。
- B. 清除日志中记录的所有之前的警报目
- C. 查看数据库阈值设置的历史。
- D. 停止健康监控器（Health Monitor）。
- E. 查看实例或数据库的警报历史。

### 第 9

以下哪一个不是健康指标设置可以定义的有效级别？

- A. 服务器 (Server)
- B. 全局 (Global)
- C. 实例 (Instance)
- D. 对象 (Object)

# 420 第 5 章：分析 DB2 活动

### 第 10

名为 `SAMPLE` 的数据库包含一个跨越五个文件的 DMS 表空间。其中三个文件大小为 4 GB，两个文件大小为 3 GB。数据库管理员希望当 3 GB 文件填充 80% 且 4 GB 文件填充 85% 时，能够生成警报。使用健康中心实现此目标的最佳方法是：

- A. 修改所有表空间容器的全局（Global）级别设置；更改 3 GB 表空间容器的实例（Instance）级别设置。
