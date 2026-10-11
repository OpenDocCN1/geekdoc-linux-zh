

本章前面简要列举了可能会导致排序的 SQL 语句列表。下面将解释避免与这些 SQL 语句相关的排序的一些技术。

SQL 语句语法  
如果所需的输出不会受到负面影响，使用 `UNION ALL` 运算符代替 `UNION` 运算符可以避免通常用于消除两个联合 SQL 查询中重叠值的排序。避免使用 `INTERSECT`、`MINUS` 和 `DISTINCT` 关键字也能产生类似的效果。

索引的适当使用  
对应用程序 SQL 语句中 `ORDER BY` 和 `GROUP BY` 子句引用的列进行索引，可以最大限度地减少不必要的排序。确保所有外键列都被索引也有助于减少通过主键和外键列连接表时的排序。这将有助于鼓励优化器执行嵌套循环连接而不是排序合并连接来连接表。

索引创建开销  
如果被索引的表数据已经按索引顺序存储，可以使用 `CREATE INDEX` 命令的 `NOSORT` 选项来消除通常在索引创建期间发生的排序。

统计信息计算开销  
每当收集表和索引统计信息时，都可能会发生排序。为了最小化与该过程相关的开销，建议在收集表和索引统计信息时使用 `ESTIMATE` 选项而不是 `COMPUTE`。通过使用 `ANALYZE ... FOR COLUMNS` 命令，仅收集与应用程序 SQL 相关的列的统计信息，可以进一步减少统计信息收集开销。

## 增大排序区域

另一种改善与排序相关的 I/O 的技术是，通过增加 `init.ora` 中 `SORT_AREA_SIZE` 的值，来最小化写入磁盘的排序次数。然而，在增加此参数时必须小心。尽管 `SORT_AREA_SIZE` 指定的内存量直到用户启动排序时才分配给该用户的会话，但在排序处理期间，服务器的可用内存必须足以容纳用户的排序区域。特别是，如果 `SORT_AREA_SIZE` 设置为一个大值，并且许多用户同时排序，则对服务器内存的需求可能会产生不利影响，直到排序完成并释放分配给这些排序的内存。当 `SORT_AREA_SIZE` 增加时，减小 `SORT_AREA_RETAINED_SIZE` 的大小有助于最大限度地减少与排序相关的过度内存使用问题。

在使用并行查询功能时，在增加 `SORT_AREA_SIZE` 之前必须给予特别考虑。在并行查询环境中，单个 SQL 语句可能需要等于 `SORT_AREA_SIZE` × 2 × 指定并行度 的内存。

Oracle 表示，`SORT_AREA_SIZE` 的默认值对大多数 OLTP 系统来说是足够的。Oracle 还建议，对于使用 Oracle 并行查询选项的系统，1MB 的 `SORT_AREA_SIZE` 通常是最佳的。

**Oracle 目标**
创建和监控临时表空间

## 创建临时表空间

当用户的服务器进程将排序块写入磁盘时，它将数据写入用户的*临时*表空间。虽然该表空间被称为用户的*临时*表空间，但其表空间属性可以是永久的或临时的。表 8.7 比较了临时表空间和永久表空间。

### 表 8.7 临时表空间与永久表空间的比较

| 表空间类型 | 描述 |
| :--- | :--- |
| 永久 | 可以包含永久段，如表和索引，以及由每个用户服务器进程拥有的多个临时排序段 |
| 临时 | 只能包含由所有执行磁盘排序的用户共享的单个临时段 |

你可以使用以下查询在 `DBA_TABLESPACES` 数据字典视图上确定表空间是永久还是临时：

```sql
SQL> SELECT tablespace_name, contents
  2  FROM dba_tablespaces;
```

```text
TABLESPACE_NAME   CONTENTS
SYSTEM             PERMANENT
TEMP               TEMPORARY
APPL_DATA          PERMANENT
OEMGR              PERMANENT
RBS                PERMANENT
TOOLS              PERMANENT
USERS              PERMANENT
WEBDB              PERMANENT
APPL_IDX           PERMANENT
```

临时表空间概念进一步延伸为 tempfile 的概念。Tempfile 类似于数据文件，除了它们专门用于存储写入临时表空间的排序段数据。以下 SQL 命令可用于使用 tempfile 创建本地管理的临时表空间：

```sql
SQL> CREATE TEMPORARY TABLESPACE temp
  2  TEMPFILE '/u04/oradata/PROD/PRODO1.dbf' SIZE 500M
  3  AUTOEXTEND ON NEXT 50M MAXSIZE 2000M
  4  EXTENT MANAGEMENT LOCAL
  5  UNIFORM SIZE 64K;
```

> 为临时表空间指定的 `UNIFORM SIZE` 值应等于 `SORT_AREA_SIZE` + 1 个块，或者是其倍数。这允许每个排序块通过一次 I/O 写入。

如本章前面所述，在多设备上对 tempfile 进行条带化可以提供卓越的性能提升。一旦创建，可以使用 `V$TEMPFILE` 和 `DBA_TEMP_FILES` 数据字典视图来监控数据库 tempfile。这些视图的内容类似于 `V$DATAFILE` 和 `DBA_DATA_FILES` 视图的内容。

Oracle9i 还允许你使用 `ALTER DATABASE` 命令指定临时表空间作为所有数据库用户的默认临时表空间：

```sql
SQL> ALTER DATABASE DEFAULT TEMPORARY TABLESPACE temp;
```

上述命令将 `TEMP`（而不是 `SYSTEM`）表空间设为所有数据库用户的默认临时表空间。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_461_0.png)

**将非 SYSTEM 表空间指定为默认临时表空间**对数据库管理有一些影响。默认临时表空间必须是临时类型（即不能是永久的），并且一旦被指定为默认，就不能转换为永久表空间。此外，在创建另一个表空间之前，你无法删除默认临时表空间，因为这样会导致数据库没有地方执行到磁盘的排序。同样，默认临时表空间也不能被置于离线状态。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_461_1.png)

由于临时表空间不能包含任何永久对象，因此不需要将其包含在数据库备份策略中。

如果数据库不使用临时表空间进行排序，每个执行排序的用户必须在其临时表空间中构建，然后删除一个排序段。这种对单个排序段的动态管理在 I/O 和递归数据字典调用方面都很昂贵。

与存储在永久表空间中的排序段不同，临时表空间中的排序段在用户排序完成时不会被删除。相反，实例启动后的第一个排序操作创建一个排序段，该排序段保留在临时表空间中，供随后也执行磁盘排序的用户重用。此排序段将保留在临时表空间中，直到实例关闭。你可以使用 `V$SORT_SEGMENT` 和 `V$SORT_USAGE` 动态性能视图来监控排序段的大小和使用情况。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_462_0.png)

默认情况下，在临时表空间中创建的排序段的 `MAXEXTENTS` 值为 `UNLIMITED`。

## 使用 V$SORT_SEGMENT

`V$SORT_SEGMENT` 视图允许你监控驻留在临时表空间中的排序段的大小和增长。随着用户提出需求，排序段将动态增长。以下查询显示了该视图中三个更有用的列：

```sql
SQL> SELECT tablespace_name, 
>       current_users,
>       max_sort_blocks
> FROM v$sort_segment;
```

| TABLESPACE_NAME | CURRENT_USERS | MAX_SORT_BLOCKS |
| :--- | :--- | :--- |
| TEMP | 11 | 300 |

此查询输出显示，目前有 11 个用户正在使用存储在 `TEMP` 表空间中的排序段。此外，单个用户执行的最大排序相当于 300 个 Oracle 块的大小。特别是最后一个统计数据 `MAX_SORT_BLOCKS`，在试图确定 `SORT_AREA_SIZE` 和 `SORT_AREA_RETAINED_SIZE` 的最佳设置时可能非常有用。通过将 `init.ora` 中的这些参数设置为至少 `MAX_SORT_BLOCKS * DB_BLOCK_SIZE`，你可以在内存中容纳更多排序并减少 I/O。

## 使用 V$SORT_USAGE

虽然 `V$SORT_SEGMENT` 很好地显示了整体排序操作，但它不让你看到哪些个别用户导致大量磁盘排序。然而，`V$SORT_USAGE` 视图确实包含一个 `USER` 列，可以使用它来监控按用户划分的排序活动，如下面的查询所示：

```sql
SQL> SELECT user, tablespace, 
>       blocks
> FROM v$sort_usage 
> ORDER BY blocks;
```

