

## 图 7.3 显示重做日志缓冲区统计信息的 STATSPACK 输出

| 统计信息 | 总计 | 每秒 | 每事务 |
| :--- | :--- | :--- | :--- |
| 直接物理写 | 147 | 0.2 | 49.0 |
| 非检查点物理写 | 147 | 0.2 | 49.0 |
| 预取块 | 0 | 0.0 | 0.0 |
| 递归调用 | 917 | 1.4 | 305.7 |
| 已写入的重做块 | 707 | 1.1 | 235.0 |
| 重做缓冲区分配重试 | 0 | 0.0 | 0.0 |
| 重做条目 | 340 | 0.5 | 113.3 |
| 重做日志空间请求 | 0 | 0.0 | 0.0 |
| 重做排序标记 | 0 | 0.0 | 0.0 |
| 重做大小 | 364,364 | 553.7 | 121,454.7 |
| 重做同步写 | 0 | 0.0 | 1.0 |
| 重做浪费 | 3,028 | 4.6 | 1,009.3 |
| 重做写 | 9 | 0.0 | 3.0 |

## 使用 REPORT.TXT 输出测量重做日志缓冲区性能

通过运行 UTLBSTAT.SQL 和 UTLESTAT.SQL 生成的 REPORT.TXT 文件还包含一个部分，显示与 V$SYSSTAT 和 STATSPACK 输出中发现的与重做日志缓冲区性能相关的相同统计信息。图 7.4 展示了样例 REPORT.TXT 的相关部分。

## 图 7.4 显示重做日志缓冲区统计信息的 REPORT.TXT 输出

```
SQL> select nls.name "statistic",
   2  nls.change\("total",
   3  round(nls.change(\"start_users + end_user\",/2),2) "Per Transaction"
   4  round(nls.change(\"start_users + end_user\",/2),2) "Per Logon"
   5  round(nls.change(to_number(to_char(end_time, 'MM/DD/YYYY HH24:MI:SS'))/
   6  to_number(to_char(start_time, 'MM/DD/YYYY HH24:MI:SS'))
   7  + to_number(to_char(start_time, 'SSSS'))) -
   8  to_number(to_char(start_time, 'SSSS')))
   9  , 2) "Per Second"
  10  from  stats@stats nls,
  11  stats@stats trans,
  12  stats@stats
  13  where  trans.name= 'user_commits'
  14  and nls.change = 0
  15  order by nls.name;
```

| 统计信息 | 总计 | 每事务 | 每登录 | 每秒 |
| :--- | :--- | :--- | :--- | :--- |
| 此会话使用的 CPU | 5878 | 54.43 | 734.75 | 28.26 |
| 调用开始时使用的 CPU | 5878 | 54.43 | 734.75 | 28.26 |
| ... | | | | |
| 递归 CPU 使用量 | 4031 | 37.32 | 503.88 | 19.38 |
| 已写入的重做块 | 127510 | 1188.46 | 15588.75 | 828.48 |
| 重做缓冲区分配重试 | 307 | 2.84 | 38.38 | 1.48 |
| 重做条目 | 271852 | 2517.15 | 33981.1 | 1306.98 |
| 重做日志空间请求 | 109 | 1.01 | 13.63 | .52 |
| 重做日志切换等待时间 | 2670 | 24.81 | 304.88 | 12.88 |
| 重做大小 | 8559492 | 791754.59 | 10688606.5 | 411103.28 |
| 重做同步时间 | 1118 | 10.35 | 139.75 | .58 |
| 重做同步写 | 98 | 12.25 | 166.68 | 4.76 |
| 重做浪费 | 199948 | 1851.37 | 24909.5 | 961.29 |
| 重做写入时间 | 9311 | 86.21 | 1165.88 | 44.76 |
| 重做写入器闩锁时间 | 109 | 1.84 | 24.88 | .96 |
| 重做写 | 765 | 7.08 | 95.63 | 3.68 |

图 7.4 中显示的输出表明，在 UTLBSTAT.SQL 和 UTLESTAT.SQL 执行期间放入重做日志缓冲区的 271,852 个重做条目（redo_entries）中，有 307 个条目（redo_buffer_allocation_retries）经历了等待，并不得不重试将条目放入重做日志缓冲区。

> **提示**  
> REPORT.TXT 输出中的一些统计信息名称被截断。例如，统计信息 `redo_buffer_allocation_retry` 被截断为 `redo_buffer_allocation_retr`。

## 提高重做日志缓冲区性能

现在，您已经了解了重做日志缓冲区机制的工作原理以及如何监控其性能，您可以研究提高其性能的方法。重做日志缓冲区调优的目标是确保用户服务器进程能够访问重做日志缓冲区并在其中放置条目，而无需经历等待。这些技术分为两类：

- 将其变大
- 减少重做生成

| **Oracle 目标** | 监控和确定重做日志缓冲区的大小 |

### 将其变大

提高重做日志缓冲区性能最简单的方法是增加其大小。重做日志缓冲区越大，用户服务器进程在尝试将重做条目放入缓冲区时经历等待的可能性就越小。

重做日志缓冲区的大小以字节为单位，使用 `init.ora` 参数 `LOG_BUFFER` 指定。`LOG_BUFFER` 的默认值是 512KB，或者是服务器中 CPU 数量的 128KB，取较大者。取值范围是从 64K 到操作系统特定的最大值。

> **提示**  
> 如果您通过将 `LOG_BUFFER` 设置为非常低的值而使重做日志缓冲区的大小过小，Oracle 服务器将覆盖您的设置并将重做日志缓冲区增加至其默认大小。

与共享池和数据库缓冲区缓存一样，继续进行调优练习以持续增加重做日志缓冲区的大小，直到重做日志缓冲区重试比率显示不再进一步改善，或者统计信息 `log buffer space in V$SESSION_WAIT` 的值停止减少，这是一种可接受的调优做法。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_374_0.png)

> 减少重做日志缓冲区闩锁的竞争是重做日志缓冲区性能改善的次要指标。闩锁调优在第 9 章“调优竞争”中讨论。

### 减少重做生成

提高重做日志缓冲区性能的另一种方法是减少某些 DML 语句生成的重做信息量，从而减轻对其的压力。该技术通过以下方法之一实现：

- `UNRECOVERABLE` 关键字
- `NOLOGGING` 关键字

#### UNRECOVERABLE 关键字

在使用 `CREATE TABLE AS SELECT` SQL 命令创建表时使用 `UNRECOVERABLE` 关键字：

```
SQL> CREATE TABLE employee_history
   2  AS
   3  SELECT *
   4  FROM employee
   5  UNRECOVERABLE;
```

以这种方式创建的表不会为 `CREATE` 语句的子查询生成的插入操作生成任何重做信息。但是，该表上的任何后续 DML 都将在重做日志缓冲区中生成条目。默认情况下，使用 `CREATE TABLE AS SELECT` 语法创建的所有表都是可恢复的。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_374_1.png)

> 在创建分区表、索引组织表或包含大对象（LOB）的表时，不能使用 `UNRECOVERABLE`/`RECOVERABLE` 关键字。因此，自 Oracle 8.0.x 版本以来，它主要已被 `NOLOGGING` 选项所取代。

#### NOLOGGING 关键字

与 UNRECOVERABLE 类似，NOLOGGING 选项也允许您指定在执行某些类型的 DML 时哪些表应跳过生成重做条目。然而，与 UNRECOVERABLE 不同，NOLOGGING 是表的属性，该属性在您禁用它之前一直有效。您可以在表创建时或创建后使用 ALTER TABLE 语句指定 NOLOGGING 属性。

**表创建期间的 NOLOGGING** 以下示例展示了如何在表创建期间指定 NOLOGGING 关键字：

```
SQL> CREATE TABLE employee_history
   2   (employee_id number,
   3    last_name varchar2(30),
   4    first_name varchar2(30),
   5    hired_date date,
   6    start_date date,
   7    end_date date)
   8   TABLESPACE appl_tab
   9   STORAGE (INITIAL 500k NEXT 500k PCTINCREASE 0)
  10  NOLOGGING;
```

**表创建后的 NOLOGGING** 也可以在 ALTER TABLE 命令中指定 NOLOGGING 选项：

```
SQL> ALTER TABLE employee_history NOLOGGING;
```

您还可以使用 ALTER TABLE 命令将表更改回 LOGGING 模式：

```
SQL> ALTER TABLE employee_history LOGGING;
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_375_0.png)

除非在表创建时或通过 ALTER TABLE 命令指定了 NOLOGGING 选项，否则所有表都是 LOGGING 表。

通过查询 DBA_TABLES，您可以确定哪些表具有 NOLOGGING 属性：

```
SQL> SELECT owner, table_name
   2   FROM dba_tables
   3   WHERE logging = 'NO';
```

一旦在表上设置了 NOLOGGING 属性，仅当后续针对该表的 DML 属于以下类型时，才会抑制重做条目生成：

- 使用 SQL*Loader 的直接路径加载
- 使用 /*+ APPEND */ 提示的直接加载插入

对 NOLOGGING 表的任何后续 DML，如果不属于这两个类别之一，仍然会在重做日志缓冲区中生成常规重做条目。

除了上面显示的 CREATE TABLE 和 ALTER TABLE 命令外，以下命令也可以与 NOLOGGING 选项一起使用：

- CREATE TABLE AS SELECT
- CREATE INDEX
- ALTER INDEX REBUILD
- CREATE TABLESPACE

![](img/832fbc6aca8b6075843ca6f2356c0a8d_376_0.png)

> 在表上指定 NOLOGGING 属性意味着，如果在新增数据被纳入计划冷备份或热数据库备份之前需要介质恢复，则使用直接路径方法加载的任何数据都将丢失。

## 调优检查点

每当数据库中发生数据库检查点事件时，日志写入器后台进程会将重做日志缓冲区的内容写入在线重做日志。

