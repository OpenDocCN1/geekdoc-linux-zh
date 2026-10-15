
在下面的示例中，我们将使用两种方法将数据加载到 `LOADTAB` 中，分别使用外部源文件和使用 `CURSOR` 答案集作为加载的源。

## 示例 5-32 从源 DEL 文件加载数据到分区表

```
db2inst1@UDBLNX08:"/its0> db2 "load from empl.del of del insert into loadtab"
Agent Type   Node   SQL Code   Result
```

| Agent | Type | Node | SQL Code | Result |

|---|---|---|---|---|

| LOAD |  | 000 | +00000000 | Success. |

| LOAD |  | 001 | +00000000 | Success. |

| LOAD |  | 002 | +00000000 | Success. |

| PARTITION |  | 001 | +00000000 | Success. |

| PRE_PARTITION |  | 000 | +00000000 | Success. |

| RESULTS: | 3 of 3 LOADs completed successfully. |  |  |  |

Summary of Partitioning Agents:

Rows Read          = 32

Rows Rejected      = 0

Rows Partitioned   = 32

Summary of LOAD Agents:

Number of rows read        = 32

Number of rows skipped     = 0

Number of rows loaded      = 32

Number of rows rejected    = 0

Number of rows deleted     = 0

Number of rows committed   = 32

```
db2inst1@UDBLNX08:"/its0> db2 "select dbpartitionnum(empno),count(*) from loadtab group by dbpartitionnum(empno)"
```

```
1       2
------------ ------------
        0       10
        1       11
        2       11

3 record(s) selected.
```

在示例 5-32 中，源文件被加载到分布在三个分区上的 `LOADTAB` 中。该命令与单分区环境中的命令一样。为了验证加载结果，在同一示例中，我们使用了一个 SQL 语句来统计不同分区上的行数，从 SQL 执行的输出中，我们发现行被均匀地分布到各分区。

## 示例 5-33 从 CURSOR 加载数据到分区表

```
db2inst1@UDBLNX08:"/itso> db2 "declare mycur cursor for select * from employee"
DB20000I  The SQL command completed successfully.
db2inst1@UDBLNX08:"/itso> db2 "load from mycur of cursor replace into loadtab"
```

| Agent Type | Node | SQL Code | Result |

|------------|------|----------|--------|

| LOAD       | 000  | +00000000 | Success. |

| LOAD       | 001  | +00000000 | Success. |

| LOAD       | 002  | +00000000 | Success. |

| PARTITION  | 001  | +00000000 | Success. |

| RESULTS:   | 3 of 3 LOADs completed successfully. | | |

```
Summary of Partitioning Agents:
Rows Read              = 32
Rows Rejected          = 0
Rows Partitioned       = 32

Summary of LOAD Agents:
Number of rows read     = 32
Number of rows skipped  = 0
Number of rows loaded   = 32
Number of rows rejected = 0
Number of rows deleted  = 0
Number of rows committed = 32
```

在分区数据库环境中加载数据时，只有非定界 ASCII（`ASC`）和定界 ASCII（`DEL`）文件可以被分区。`PC/IXF` 文件不能被分区。要将 `PC/IXF` 文件加载到多分区表中，可以先将其加载到单分区表中，然后使用 `CURSOR` 文件类型执行加载操作，将数据移动到多分区表（示例 5-33）。如果尝试直接将 IXF 格式的源文件加载到分区表，将导致错误 `SQL3004N`。这意味着 `filetype` 参数无效，因为 IXF 文件不能用于加载到定义在多分区节点组上的表。

有一些选项是特定于在分区数据库环境中加载的，例如：

- `PART_FILE_LOCATION`：分区文件的完全限定位置。
- `OUTPUT_DBPARTNUMS`：表示将执行加载操作的数据库分区的分区号列表。
- `PARTITIONING_DBPARTNUMS`：在分区过程中将使用的分区号列表。
- `MODE`：加载分区数据库时加载操作将进行的模式，例如 `PARTITION_AND_LOAD`、`PARTITION_ONLY`、`LOAD_ONLY` 等。
- `PARTITIONED DB CONFIG`：允许您在 `LOAD` 命令中指定分区数据库特定的配置选项。

如果在分区数据库环境中使用 `LOAD` 命令时未指定分区数据库特定的配置选项（当 `DB2` 注册表变量 `DB2_PARTITIONEDLOAD_DEFAULT` 未设置为 `NO` 时），则将使用默认值。例如，`MODE` 将默认为 `PARTITION_AND_LOAD`。

在前两个示例中，使用了在分区数据库环境中加载的默认选项。

## 示例 5-34 在 LOAD 命令中使用 PARTITIONED DB CONFIG 参数

```
db2inst1@UDBLNX08:"/itso> db2 "load from empl.del of del replace into loadtab partitioned db config mode partition_only part_file_location /db2home/db2inst1/itso partitioning_dbpartnums (1,2)"
```

| Agent Type | Node | SQL Code | Result |

|---|---|---|---|

| LOAD_TO_FILE | 000 | +00000000 | Success. |

LOAD_TO_FILE 001 +00000000 成功。

LOAD_TO_FILE 002 +00000000 成功。

PARTITION 001 +00000000 成功。

PARTITION 002 +00000000 成功。

PRE_PARTITION 000 +00000000 成功。

分区代理摘要：

已读取行数 = 32

已拒绝行数 = 0

已分区行数 = 32

## 装载时使用 ALLOW READ ACCESS 的示例

`ALLOW READ ACCESS` 选项在装载大量数据时非常有用，因为它几乎始终允许用户访问表数据，即使在装载操作正在进行或装载操作失败之后也是如此。在 `ALLOW READ ACCESS` 模式下，装载操作的行为与应用程序的隔离级别无关。也就是说，任何隔离级别的读取方始终可以读取原有数据，但在装载操作完成之前，它们无法读取新装载的数据。

除了最后阶段之外，整个装载操作期间都提供读访问。在数据提交之前，装载实用程序会在表上获取排他锁（Z-lock）。装载实用程序将一直等待，直到所有持有该表锁的应用程序释放锁。这可能会导致数据提交出现延迟。可以使用 `LOCK WITH FORCE` 选项强制冲突的应用程序退出，使装载操作无需等待即可继续。

在示例 5-35 中，首先我们创建名为 `LOADREAD` 的表，然后插入三行作为已有数据；接着，我们将使用 `ALLOW READ ACCESS` 从 `DEL` 格式的源文件装载其他行，并且在装载进行的同时尝试从另一个会话访问该表。

### 示例 5-35 使用 ALLOW READ ACCESS 装载数据
