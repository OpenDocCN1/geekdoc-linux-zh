
> 在创建分区表、索引组织表或包含大对象（LOB）的表时，不能使用 `UNRECOVERABLE`/`RECOVERABLE` 关键字。因此，自 Oracle 8.0.x 版本以来，它主要已被 `NOLOGGING` 选项所取代。

### NOLOGGING 关键字

与 `UNRECOVERABLE` 类似，`NOLOGGING` 选项也允许您指定在执行某些类型的 DML 时哪些表应跳过生成重做条目。然而，与 `UNRECOVERABLE` 不同，`NOLOGGING` 是表的属性，该属性在您禁用它之前一直有效。您可以在表创建时或创建后使用 `ALTER TABLE` 语句指定 `NOLOGGING` 属性。

#### 表创建期间的 NOLOGGING

以下示例展示了如何在表创建期间指定 `NOLOGGING` 关键字：

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

#### 表创建后的 NOLOGGING

也可以在 `ALTER TABLE` 命令中指定 `NOLOGGING` 选项：

```
SQL> ALTER TABLE employee_history NOLOGGING;
```

您还可以使用 `ALTER TABLE` 命令将表更改回 `LOGGING` 模式：

```
SQL> ALTER TABLE employee_history LOGGING;
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_375_0.png)

除非在表创建时或通过 `ALTER TABLE` 命令指定了 `NOLOGGING` 选项，否则所有表都是 `LOGGING` 表。

通过查询 `DBA_TABLES`，您可以确定哪些表具有 `NOLOGGING` 属性：

```
SQL> SELECT owner, table_name
   2   FROM dba_tables
   3   WHERE logging = 'NO';
```

一旦在表上设置了 `NOLOGGING` 属性，仅当后续针对该表的 DML 属于以下类型时，才会抑制重做条目生成：

- 使用 `SQL*Loader` 的直接路径加载
- 使用 `/*+ APPEND */` 提示的直接加载插入

对 `NOLOGGING` 表的任何后续 DML，如果不属于这两个类别之一，仍然会在重做日志缓冲区中生成常规重做条目。

除了上面显示的 `CREATE TABLE` 和 `ALTER TABLE` 命令外，以下命令也可以与 `NOLOGGING` 选项一起使用：

- `CREATE TABLE AS SELECT`
- `CREATE INDEX`
- `ALTER INDEX REBUILD`
- `CREATE TABLESPACE`

![](img/832fbc6aca8b6075843ca6f2356c0a8d_376_0.png)

> 在表上指定 `NOLOGGING` 属性意味着，如果在新增数据被纳入计划冷备份或热数据库备份之前需要介质恢复，则使用直接路径方法加载的任何数据都将丢失。

## 调优检查点

每当数据库中发生数据库检查点事件时，日志写入器后台进程会将重做日志缓冲区的内容写入在线重做日志。

### 目标：Oracle

#### 描述检查点的工作机制

数据库检查点事件代表数据库处于一致状态的某个时刻。检查点非常重要，因为在实例故障之后，实例恢复期间只需要恢复自上次检查点以来发生的那些事务。检查点分为两种类型：*增量和完整*。当发生增量检查点时，会执行以下操作：

- `CKPT` 后台进程立即更新控制文件头。
- `CKPT` 后台进程在新的重做日志切换时，再次更新控制文件头和数据文件头。

当发生完整检查点事件时，数据库中会发生以下操作：

- `DBW0` 后台进程将所有包含已提交事务的数据库缓冲池（Database Buffer Cache）中的缓冲区写入磁盘。
- `LGWR` 后台进程将重做日志缓冲区（Redo Log Buffer）中的所有内容写入联机重做日志（Online Redo Log）。
- `CKPT` 后台进程更新数据库控制文件和数据文件头，以指示检查点事件已经发生。

数据库在以下情况下会发生检查点：

- 使用除 `ABORT` 以外的任何方法关闭实例时。
- 当联机重做日志从当前日志切换到序列中的下一个重做日志时。
- 当 DBA 发出 `ALTER SYSTEM CHECKPOINT` 命令时。
- 当使用 `ALTER TABLESPACE ... BEGIN BACKUP` 命令将表空间置入热备份模式，或当表空间被置为离线时。此检查点是完整检查点的一种特殊形式，称为完整表空间检查点。在此类检查点期间，只有属于处于热备份模式的表空间的脏缓冲区会被写入磁盘。
- 当 `init.ora` 参数 `FAST_START_MTTR_TARGET` 指定的值被超过时。

监控检查点活动很重要，因为过多的检查点会导致不必要的 I/O，而过少的检查点会使数据库面临漫长的实例恢复时间。下一节描述测量数据库检查点性能的技术。

### 测量检查点性能

要在与检查点事件相关的 I/O 开销及其实例恢复收益之间取得适当平衡，需要利用 `V$SYSTEM_EVENT` 和 `V$SYSSTAT` 动态性能视图的内容、`STATSPACK`、`REPORT.TXT`、告警日志以及 `OEM` 性能管理器来监控检查点活动。

#### 使用 V$SYSTEM_EVENT 测量检查点性能

偶尔，检查点事件会启动，但由于第二个检查点请求紧随第一个请求之后发生，导致未能成功完成。您可以通过查询 `V$SYSTEM_EVENT` 中的统计项 `log file switch (checkpoint incomplete)` 来检测已启动但未完成的检查点。该动态性能视图报告自实例启动以来各种事件发生的等待次数。表 7.2 描述了在此查询中使用的 `V$SYSTEM_EVENT` 列的内容。

##### 表 7.2 V$SYSTEM_EVENT 中选定列的描述

| 列名 | 描述 |
| :--- | :--- |
| `EVENT` | 与等待相关联的事件名称 |
| `TOTAL_WAITS` | 此事件发生等待的总次数 |
| `AVERAGE_WAIT` | 等待此事件的平均时间，以百分之一秒为单位 |

图 7.5 展示了一个针对 `V$SYSTEM_EVENT` 的示例查询，显示了数据库中发生的与检查点活动相关的等待。

##### 图 7.5 V$SYSTEM_EVENT 中显示的检查点活动

```sql
SQL> SELECT event, total_waits, average_wait
   2  FROM V$SYSTEM_EVENT
   3  WHERE event LIKE '%check%'
   4  or event LIKE '%log file switch%';

EVENT                          TOTAL_WAITS AVERAGE_WAIT
checkpoint completed              1         10
log file switch (checkpoint incomplete) 54         38
```

`V$SYSTEM_EVENT` 视图中发现的两个事件是检查点性能的指示器：`checkpoint completed` 和 `log file switch (checkpoint incomplete)`。

`Checkpoint Completed`

此事件显示了为检查点完成其活动而发生等待的频率。该事件的高值或持续增加的值表明需要对检查点进行调优。图 7.5 中的输出显示，一个 `Checkpoint Complete` 事件必须等待 10 个百分之一秒才能完成。

`Log File Switch (Checkpoint Incomplete)`

此事件显示了在上一个日志切换的检查点有机会完成之前，联机重做日志从当前日志切换到下一个日志的频率。当这种情况发生时，正在进行的检查点会被放弃，并开始一个新的检查点。由于不完整的检查点会导致无法提供恢复收益的额外 I/O，因此该事件的频繁发生表明应该对检查点活动进行调优。图 7.5 中的输出显示，导致不完整检查点的日志切换发生了 54 次，平均等待时间为 38 个百分之一秒。
