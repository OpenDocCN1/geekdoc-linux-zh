

![](img/9479df2d00f5e62b87366b125224950f_417_0.png)

> *提示*
> *我发现 ORDERED 和 INDEX_JOIN /INDEX_COMBINE 提示符（hints）最为有用。通常，当基于成本的优化器（CBO）选择不使用索引时，往往有特定的原因（例如聚集因子等）。*

![](img/9479df2d00f5e62b87366b125224950f_417_1.png)

> *提示*
> *如果 FROM 子句使用了表别名，请确保在提示符（HINT）中使用表别名而不是表名。*

## SQL 调优技巧

从编码角度来看，有一些做法可以帮助 CBO 做出更好的决策，或者在原本可能无法使用索引的情况下启用索引。另一种做法是编写代码以生成更短的执行计划，从而减少对数据库的访问次数。

如果某列上存在任何形式的函数，Oracle 将不会使用该列上的索引。例如，…WHERE SUBSTR(ename,1,5) = 'SMITH' 不会使用 ename 列上可用的索引，但像这样的编码风格就可以：…WHERE ename LIKE 'SMITH%'。当搜索前导列时，这种编码风格效果良好。如果 LIKE 函数以字符串开头而不是其通配字符，它将使用该索引。Oracle6i 引入了函数索引，当没有简单的变通方法且带函数的列的性能成为问题时，允许在这些情况下使用索引。

确保 WHERE 子句两侧的字段具有相同的数据类型。Oracle 只比较具有相同数据类型的项。在解析 SQL 语句时，如果 Oracle 注意到被比较的两个列具有不同的数据类型，它会在其中一侧添加 TO_CHAR 或 TO_NUMBER 函数。这种内部添加在用户界面上不可见，但在该示例中假设列已建立索引，这将在已建立索引的列上成为一个函数，而 Oracle 根本不会使用该列上可用的索引。如果必须比较不同的数据类型，请通过在 WHERE 子句中自行添加适当的函数来控制 Oracle 执行转换的位置。

WHERE 子句中的计算也会导致 Oracle 不使用可用的索引。诸如 …WHERE SAL * 1.1 > 100 这样的 WHERE 子句代码应编写为 WHERE SAL > 100/1.1，将计算从已建立索引的列中移开。

不要在 WHERE 子句中将已建立索引的列连接在一起与字符串进行比较，例如 WHERE deptno || manager = '201346'。始终在 WHERE 子句中将每个已建立索引的列放在单独的一行，例如：WHERE deptno = 20 AND manager = 1346。

在引用已建立索引的列时，尽量避免使用 NOT。例如，‘NOT `<`’ 等同于 ‘`>=`’，‘NOT `<=`’ 等同于 ‘`>`’，‘NOT `>`’ 等同于 ‘`<=`’，并且 ‘NOT `>=`’ 等同于 ‘`<`’。

使用 IN 子句比多个查询同一列多个值的 WHERE 语句更高效。在 WHERE 子句中使用 EXISTS 优于在 SELECT 子句中使用 DISTINCT（DISTINCT 在所有行返回后应用；WHERE 子句谓词限制了返回的行数）。

使用 GROUP BY 子句时，使用 WHERE 子句行来限制行数，优于使用 HAVING 子句。WHERE 子句将限制返回的行数，而 HAVING 子句将在所有行返回后应用。

### 查找性能不佳的 SQL

有几种方法可以查找性能不佳的 SQL。Oracle 提供了几个有用的工具，例如 Enterprise Manager 的 TOP（列出符合所选条件的主要 SQL，如 IO、时间等）、Oracle 跟踪设施（又称跟踪文件和 TKProf/Trace Analyzer）以及 Statspack（统计信息和 SQL 文本收集）。许多专家/DBA/IT 人员编写了许多脚本，用于深入研究 Oracle 的动态性能视图（又称 V$ 表），以识别特定的性能问题。

### 使用脚本

Oracle 运行的 SQL 可以从几个位置轻松访问。列表 16-3 展示了 V_$SQLAREA 视图。该视图显示了 SQL 以及关于特定 SQL 语句的大量信息。可以轻松编写 SQL 来查看符合各种条件的 SQL 语句。还可以将该视图中的信息与其他 V$ 信息结合使用，以找出导致特定问题的特定 SQL。

### 列表 16-3：V_$SQLAREA 列表

```
dhotkaun:ORA10g:SYSTEM>desc v_$sqlarea
```
Name                     Null?    Type
---                    -------    ----
SQL_TEXT                 VARCHAR2(1000)
SQL_ID                   VARCHAR2(13)
SHARABLE_MEM             NUMBER
PERSISTENT_MEM           NUMBER
RUNTIME_MEM              NUMBER
SORTS                    NUMBER
VERSION_COUNT            NUMBER
LOADED_VERSIONS          NUMBER
OPEN_VERSIONS            NUMBER
USERS_OPENING            NUMBER
FETCHES                  NUMBER

| EXECUTIONS | NUMBER |
| --- | --- |
| END_OF_FETCH_COUNT | NUMBER |
| USERS_EXECUTING | NUMBER |
| LOADS | NUMBER |
| FIRST_LOAD_TIME | VARCHAR2(19) |
| INVALIDATIONS | NUMBER |
| PARSE_CALLS | NUMBER |
| DISK_READS | NUMBER |
| DIRECT_WRITES | NUMBER |
| BUFFER_GETS | NUMBER |
| APPLICATION_WAIT_TIME | NUMBER |
| CONCURRENCY_WAIT_TIME | NUMBER |
| CLUSTER_WAIT_TIME | NUMBER |
| USER_IO_WAIT_TIME | NUMBER |
| PLSQL_EXEC_TIME | NUMBER |
| JAVA_EXEC_TIME | NUMBER |
| ROWS_PROCESSED | NUMBER |
| COMMAND_TYPE | NUMBER |
| OPTIMIZER_MODE | VARCHAR2(25) |
| PARSING_USER_ID | NUMBER |
| PARSING_SCHEMA_ID | NUMBER |
| KEPT_VERSIONS | NUMBER |
| ADDRESS | RAW(4) |
| HASH_VALUE | NUMBER |
| OLD_HASH_VALUE | NUMBER |
| MODULE | VARCHAR2(64) |
| MODULE_HASH | NUMBER |
| ACTION | VARCHAR2(64) |
| ACTION_HASH | NUMBER |
| SERIALIZABLE_ABORTS | NUMBER |
| CPU_TIME | NUMBER |
| ELAPSED_TIME | NUMBER |
| IS_OBSOLETE | VARCHAR2(1) |
| CHILD_LATCH | NUMBER |
| PROGRAM_ID | NUMBER |

查找任何 SQL 语句文本的关键列是 ADDRESS 和 HASH_VALUE。使用这两个字段可以唯一地识别所需的特定 SQL。列表 16-6 和 16-7 中的脚本返回导致所识别特定问题的 SQL 的 ADDRESS 和 HASH_VALUE。这些脚本可以轻松修改以包含实际的 SQL 文本。列表 16-4 和 16-5 是另外两个显示 SQL 文本的 V$ 表。列表 16-4 显示了 V_$SQLTEXT 中可用的列，图 16-8 显示了 V_$SQLTEXT_WITH_NEWLINES 中可用的列。这个 V$ 表在字符模式显示器或报告中格式化显示 SQL 时更加美观。V_$SQLAREA 和 V_$SQLTEXT 都将 SQL 语句存储在一个连续字符串中。

![](img/9479df2d00f5e62b87366b125224950f_420_0.png)

图 16-8. Oracle Enterprise Manager 的 Top Sessions 窗口

审查 V_$SQLAREA 列，并注意在查找问题 SQL 时可以访问的各种类型的 SQL。

### 列表 16-4：V_$SQLTEXT 列表

```
dhotkaun:ORA10g:SYSTEM>desc v_$sqltext
```
Name        Null?     Type
----------   --------- ------------------------
ADDRESS                 RAW(4)
HASH_VALUE              NUMBER
SQL_ID                  VARCHAR2(13)
COMMAND_TYPE            NUMBER
PIECE                   NUMBER
SQL_TEXT                VARCHAR2(64)

### 列表 16-5：V_$SQLTEXT_WITH_NEWLINES 列表

```
dhotkaun:ORA10g:SYSTEM>desc v_$sqltext_with_newlines
```
Name        Null?     Type
----------   --------- ------------------------
ADDRESS                 RAW(4)
HASH_VALUE              NUMBER

| Name | Type |
|---|---|
| SQL_ID | VARCHAR2(13) |
| COMMAND_TYPE | NUMBER |
| PIECE | NUMBER |
| SQL_TEXT |  |

### 列表 16-6：查找长时间运行的 SQL 语句的脚本

```
/***********************************************
* File: Long_Running_SQL.sql
* Type: SQL*Plus script
* Author: Dan Hotka (www.DanHotka.com)
* Date: July 9, 2003
*
* Description:
* This script lists the SQL statements associated with IO Activity
*
* Modifications:
**********************************************/
select a.event, a.sid, d.name, b.segment_name, c.sql_address,
 c.sql_hash_value from v$session_wait a, dba_extents b, v$session c,
v$datafile d
where a.event in ('buffer busy waits','db file sequential read','db file
scattered read')
and b.file_id = a.p1
and a.p2 between b.block_id and b.block_id + b.blocks + 1
and a.sid = c.sid
and a.p1 = d.file#;
```

列表 16-6 中的脚本对于查找长时间运行的 SQL 很有用。它主要基于 V$SESSION_WAIT 视图，查找等待缓冲区缓存加载的事件（表明 SQL 正在访问大量数据块）和顺序读取（全表扫描）。该脚本通过可用信息标识正在访问的表。然后可以使用该脚本提供的 HASH_VALUE 和 ADDRESS 轻松查找 SQL 语句。

### 列表 16-7：查找问题 SQL 的脚本

```
/***********************************************
* File: waiting.sql
* Type: SQL*Plus script
* Author: Dan Hotka (www.DanHotka.com)
* Date: Feb 21, 2003
*
* Description:
* This script lists top wait events
*
* Modifications:
```

