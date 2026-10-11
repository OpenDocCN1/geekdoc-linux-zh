
# 衡量数据文件 I/O

可以使用 V$FILESTAT 和 V$DATAFILE 动态性能视图、STATSPACK 和 REPORT.TXT 的输出，以及 OEM 性能管理器 GUI 工具的输出，来衡量数据库中数据文件的物理 I/O 性能。

**Oracle 目标**
诊断表空间使用问题

## 使用 V$FILESTAT、V$DATAFILE 和 V$TEMPFILE 衡量数据文件 I/O

V$FILESTAT、V$DATAFILE 和 V$TEMPFILE 动态性能视图可用于监控数据库中各个数据文件和表空间的读写活动性能。这三个视图中选定列的描述见表 8.2、8.3 和 8.4。

**表 8.2** V$FILESTAT 选定列描述

| 列名 | 描述 |
| :--- | :--- |
| FILE# | Oracle 在创建表空间时分配给该数据文件的内部标识符 |
| PHYRDS | 对该数据文件执行物理读的次数 |
| PHYWRts | 对该数据文件执行物理写的次数 |
| AVGIOTIM | 对该数据文件执行 I/O 操作的**平均时间**，以毫秒为单位 |
| MINIOTIM | 对该数据文件执行 I/O 操作的**最短时间**，以毫秒为单位 |
| MAXIOWTM | 对该数据文件写入的**最长耗时**，以毫秒为单位 |
| MAXIORTM | 对该数据文件读取的**最长耗时**，以毫秒为单位 |

**表 8.3** V$DATAFILE 选定列描述

| 列名 | 描述 |
| :--- | :--- |
| FILE# | Oracle 在创建表空间时分配给该数据文件的内部标识符 |
| NAME | 数据文件的完全限定路径和名称 |

**表 8.4** V$TEMPFILE 选定列描述

| 列名 | 描述 |
| :--- | :--- |
| FILE# | Oracle 在创建表空间时分配给该数据文件的内部标识符 |
| NAME | 数据文件的完全限定路径和名称 |

图 8.1 展示了针对这三个视图的查询，显示了数据库中所有数据文件（在第一列用 D 表示）和临时文件（在第一列用 T 表示）的总体统计信息。

**图 8.1** V$FILESTAT、V$DATAFILE 和 V$TEMPFILE 上的性能查询

```sql
SQL> SELECT s.file#||'D' "FILE#TYPE", d.name "DATAFILE",
  2          s.phyrds, s.phywrts,
  3          s.avgiotm, s.minitiorm,
  4          s.maxiowtm, s.maxiortm
  5    FROM v$filestat s, v$datafile d
  6   WHERE s.file# = d.file#
  7  UNION ALL
  8 SELECT s.file#||'T', t.name "DATAFILE",
  9          s.phyrds, s.phywrts,
 10          s.avgiotm, s.minitiorm,
 11          s.maxiowtm, s.maxiortm
 12   FROM v$filestat s, v$tempfile t
 13  WHERE s.file# = t.file#
 14 ORDER BY 1;
```

FILE#TYPE DATAFILE PHYRDS PHYWRTS AVGIOTM MINIOTIM MAXIOWTM MAXIORTM
10 D:\ORACLE\ORADATA\PROD\SYSTEM01.DBF 956 728 4.82 0 57.30 61.39
20 D:\ORACLE\ORADATA\PROD\TEMP01.DBF 956 735 1.69 0 37.30 61.39
30 D:\ORACLE\ORADATA\PROD\UNDO01.DBF 64 770 11.4 0 57.30 41.09
40 D:\ORACLE\ORADATA\PROD\APPL_IDX01.DBF 31 1202 0.0 0 37.30 61.39
40 D:\ORACLE\ORADATA\PROD\APPL_T101.DBF 2311 13250 9.0 0 57.30 61.34
40 D:\ORACLE\ORADATA\PROD\APPL_T201.DBF 0 12 1.9 0 57.30 61.32
50 D:\ORACLE\ORADATA\PROD\USER01.DBF 1123 62 2.2 0 57.30 61.32
60 D:\ORACLE\ORADATA\PROD\OEM_REPOSITORY1.DBF 2 0 57.32 61.30
70 D:\ORACLE\ORADATA\PROD\WEA01.DBF 4701 0 0 0 38.31 72.71

![图 8.1 输出](img/832fbc6aca8b6075843ca6f2356c0a8d_411_0.png)

init.ora 参数 TIMED STATISTICS 必须设置为 TRUE；否则，PHYRDS、PHYWRTS、AVGIOTM、MINIOTIM、MAXIOWTM 和 MAXIORTM 列的值都将为零。

## 调整表空间和文件 I/O

有关临时文件的更多详细信息，请参阅本章后面标题为“调整排序 I/O”的部分。

使用图 8.1 中的输出，可以看到大多数物理写操作发生在三个数据文件上：app1_idx01.dbf、undo01.dbf 和 app1_tab01.dbf，它们分别是应用程序索引、回滚段和表的文件。大多数物理读操作发生在组成只读表空间的数据文件（readonly01.dbf）上。正如您在下一节中看到的那样，这些文件在磁盘上的相对位置是一个重要的调整考虑因素。

SYSTEM 表空间的数据文件经常会经历较高的读取活动，因为 Oracle 用于执行递归 SQL 的数据字典表位于 SYSTEM 表空间中。然而，对 SYSTEM 表空间的过多写入活动可能表明非数据字典段存储在其中。

## 使用 STATSPACK 衡量文件 I/O

STATSPACK 特性的输出包含有关数据文件和表空间 I/O 特征的类似信息。图 8.2 展示了 STATSPACK 报告的示例输出。

![图 8.2 输出](img/832fbc6aca8b6075843ca6f2356c0a8d_412_0.png)

图 8.2 中显示的输出表明，在两个 STATSPACK 快照期间，TEMP 表空间接收了最多的读写活动。请注意，与 V$FILESTAT 的输出不同，STATSPACK 输出以秒和毫秒两种单位表示读写活动的持续时间。当确定数据文件在可用的磁盘驱动器、卷组和控制器上的物理位置时，此信息非常有用。

## 使用 REPORT.TXT 衡量文件 I/O

由 UTLBSTAT.SQL 和 UTLSTAT.SQL 生成的 REPORT.TXT 文件也包含表空间级别和文件级别的文件 I/O 信息。图 8.3 显示了显示表空间 I/O 统计信息的 REPORT.TXT 输出。图 8.4 显示了包含表空间和文件 I/O 统计信息的 REPORT.TXT 部分。

**图 8.3** 显示表空间 I/O 统计信息的 REPORT.TXT 示例

```sql
SQL> rem sum I/O operations over tablespaces.
SQL> select
  2 table_space,
  3 sum(phys_reads) reads,
  4 sum(phys_blks_rd) blks_read,
  5 sum(phys_rd_time) read_time,
  6 sum(phys_writes) writes,
  7 sum(phys_blks_wr) blks_wr,
  8 sum(phys_wrt_time) write_time,
  9 sum(megabytes_size) megabytes
 10 from stats$xfiles
 11 group by table_space
 12 order by table_space;
```

| 表空间 | 读次数 | 读取块数 | 读时间 | 写次数 | 写入块数 | 写时间 | 兆字节 |
| :------------ | :------ | :---------- | :---------- | :------- | :--------- | :----------- | :--------- |
| APPL_IDX | 19 | 19 | 0 | 19 | 19 | 0 | 28 |
| APPL_TAB | 27 | 19 | 0 | 19 | 19 | 0 | 10 |
| ORA_REPOSITORY | 19 | 19 | 0 | 19 | 19 | 0 | 21 |
| SYSTEM | 107 | 107 | 481 | 356 | 356 | 2597 | 341 |
| TOOLS | 19 | 19 | 0 | 19 | 19 | 0 | 28 |
| UNDO | 19 | 19 | 0 | 5499 | 5499 | 69719 | 210 |
| USERS | 648 | 3755 | 2577 | 13946 | 13946 | 144108 | 60 |

**图 8.4** 显示表空间和文件 I/O 统计信息的 REPORT.TXT 示例

```sql
SQL> rem I/O should be spread evenly across drives. A big difference between
SQL> phys_reads and phys_blks_rd implies table scans are going on.
SQL> select table_space, file_name,
  2 phys_reads reads, phys_blks_rd blks_read, phys_rd_time read_time,
  3 phys_writes writes, phys_blks_wr blks_wrt, phys_wrt_time write_time,
  4 megabytes_size megabytes,
  5 round(decode(phys_blks_rd,0,0,phys_rd_time/phys_blks_rd),2) avg_rt,
  6 round(decode(phys_reads,0,0,phys_blks_rd/phys_reads),2) "blocks/rd"
  7 from stats$xfiles
  8 order by table_space, file_name;
```

| 表空间 | 文件名 | 读次数 | 读取块数 | 读时间 | 写次数 | 写入块数 | 写时间 |
| :------------ | :---------- | :------ | :---------- | :---------- | :------- | :--------- | :---------- |
| APPL_IDX | 0:\ORACLE\ORADATA\PROD\APPLIDX01.DBF | 112 | 19 | 0 | 19 | 19 | 0 |
| APPL_TAB | 0:\ORACLE\ORADATA\PROD\APPLT1\APLTAB01.DBF | 19 | 19 | 0 | 19 | 19 | 0 |
| APPL_TAB | 0:\ORACLE\ORADATA\PROD\APPLT2\APLTAB02.DBF | 8 | 8 | 0 | 8 | 8 | 0 |
| ORA_REPOSITORY | 0:\ORACLE\ORADATA\PROD\ORAREPOSITORY.DBF | 19 | 19 | 0 | 19 | 19 | 0 |
| SYSTEM | 0:\ORACLE\ORADATA\PROD\SYSTEM01.DBF | 107 | 107 | 481 | 356 | 356 | 2597 |
| TOOLS | 0:\ORACLE\ORADATA\PROD\TOOLS01.DBF | 19 | 19 | 0 | 19 | 19 | 0 |
| UNDO | 0:\ORACLE\ORADATA\PROD\UNDOTBS01.DBF | 19 | 19 | 0 | 5499 | 5499 | 69719 |
| USERS | 0:\ORACLE\ORADATA\PROD\USERS01.DBF | 648 | 3755 | 2577 | 13946 | 13946 | 144108 |

在图 8.3 中，您可以看到大多数读写 I/O 活动发生在 **APPL_IDX**、**USERS** 和 **SYSTEM** 表空间上。您还可以看到，在某些情况下，单次 I/O 操作读取和写入了多个块。例如，**USERS** 表空间执行了 648 次物理读，读取了 3,755 个块。这大约相当于该表空间每次物理读读取五个到六个数据库块。这种多块读取的调整在本章后面的数据文件和表空间调整部分有讨论。图 8.4 显示 **APPL_TAB** 表空间的 I/O 分布在该表空间的两个文件 **APPL_TAB01.DBF** 和 **APPL_TAB02.DBF** 上。然而，大约 70% 的 I/O 发生在 **APPL_TAB01.DBF** 文件上。当调整文件磁盘 I/O 时，这些信息也非常有用。

关于哪些文件应接收最多或最少 I/O 没有标准规则。然而，一般来说，您应努力在多个文件之间平衡 I/O 请求。

## 使用性能管理器衡量文件 I/O

Oracle 企业管理器诊断包中的性能管理器组件包含有关文件 I/O 性能的几种图形表示。图 8.5 显示了一个示例性能管理器屏幕，其中显示基于每个数据库中文件时间的 I/O 活动。

![图 8.5 输出](img/832fbc6aca8b6075843ca6f2356c0a8d_414_0.png)
