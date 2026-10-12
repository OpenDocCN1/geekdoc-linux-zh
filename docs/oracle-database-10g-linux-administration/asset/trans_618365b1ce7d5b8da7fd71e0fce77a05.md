

```
VERSIONS BETWEEN TIMESTAMP
        TO_TIMESTAMP('2004-05-16 11:00:00', 'YYYY-MM-DD HH24:MI:SS')
   AND TO_TIMESTAMP('2004-05-16 13:55:00', 'YYYY-MM-DD HH24:MI:SS')
WHERE ename='MILLER');
```

如您所见，此查询提供的数据可能非常有用：

```
SQL> @fbtransaction;

XID         User    Oper       UNDO SQL
----------   -------  ----------  ---------------------------
010022006A020000   SYSTEM  UPDATE    update "SCOTT"."EMP" set "SAL" = '1300'
010022006A020000   SYSTEM  BEGIN
0300260084060000   SYSTEM  UPDATE    update "SCOTT"."EMP" set "SAL" = '1400'
0300260084060000   SYSTEM  BEGIN
0B002C0018000000   SYSTEM  UPDATE    update "SCOTT"."EMP" set "SAL" = '1500'
0B002C0018000000   SYSTEM  BEGIN

6 rows selected.
```

与闪回版本查询一样，闪回事务查询在追踪特定对象的变化方面可以是一个强大且有用的工具。但请记住，与闪回版本一样，它仅在 `UNDO_RETENTION` 周期内有效。一旦 UNDO 信息被清除，您将无法再以此方式追踪变化。

## 闪回表

闪回表允许您将表恢复到以前的某个时间点。闪回表功能可以通过 Oracle Enterprise Manager 或 `FLASHBACK TABLE` 命令来访问。无论哪种方式，结果都是一样的。与之前的闪回功能一样，闪回表功能也使用 UNDO 信息，因此您只能闪回一定的时间段。

此外，执行闪回表需要满足几个先决条件。这些先决条件是

- 您必须拥有 `FLASHBACK ANY TABLE` 系统权限，或对要闪回的表拥有 `FLASHBACK` 对象权限。
- 您必须对涉及的表拥有 SELECT、UPDATE、INSERT 和 DELETE 权限。
- 表上必须启用行移动（Row movement）。这可以通过以下命令完成：`ALTER TABLE *tname* ENABLE ROW MOVEMENT`。行移动允许在更新时将行移动到另一个分区。

一旦这些先决条件就位，就可以通过执行 `FLASHBACK TABLE` 命令将表还原到较早的状态，如下所示：

```
SQL> FLASHBACK TABLE scott.emp TO TIMESTAMP
     TO_TIMESTAMP('2004-05-16 11:00:00', 'YYYY-MM-DD HH24:MI:SS');
Flashback complete.
```

> 注意
> `FLASHBACK TABLE` 命令是危险的，因为它会还原整个表。与闪回查询不同，后者可以还原单条记录或特定用户的更改，此命令会还原所有内容。

与其他闪回功能一样，闪回事务查询可能非常强大且有用，但请记住，与其他功能一样，它仅在 `UNDO_RETENTION` 周期内有效。一旦 UNDO 信息被清除，您将无法再以此方式追踪变化。

这个工具根据使用方式不同，既可以是建设性的，也可能是破坏性的。由于闪回表会还原整个表，因此在使用它时必须进行仔细的规划，并了解对该表所做的更改。

### 闪回删除

闪回删除是 Oracle 撤销 `DROP TABLE` 语句的方式。闪回删除功能通过保留已删除的表一段时间，以便在必要时进行恢复。被删除的表会被重命名并移动到回收站。此回收站可用于撤销删除表操作。可以通过查询回收站表（recyclebin table）来查看当前存在于回收站中的表，如图 12-1 所示。

为了恢复被删除的表，您可以使用带有 `BEFORE DROP` 限定符的 `FLASHBACK TABLE` 命令。此命令如下所示：

```
SQL> FLASHBACK TABLE emp TO BEFORE DROP;
Flashback complete.
SQL> SELECT COUNT(*) FROM emp;
COUNT(*)
-------
14
```

```
SQL> DROP TABLE tmap;
Table dropped.

SQL> INSERT INTO dept VALUES (50, 'NEW DEPT', 'SALES COUNTY');
1 row created.

1 row selected.

SQL> SELECT * from tmap where emp_id
  2> =3256245001 or emp_age between 15 and 19 order by emp_id;

EMP#        DEPT#        DEPT_NAME      EMP_ADDR         EMP_AGE     EMP_DEPT#    SPACE
---------- ---------- -------------------- -------------------- ----------- -------- -------
3256245001 4250 1881 05-06-21001 18 143318 35 14610
3256245002 1881 05-06-21001 19 143318 35 14610
```

![](img/9479df2d00f5e62b87366b125224950f_345_0.png)

图 12-1. 回收站的内容

与其他闪回功能一样，闪回删除查询是一项很棒的功能。由于闪回删除功能将数据存储在回收站中，因此在删除表时，您实际上并没有释放数据库中的空间。

为了永久从数据库中移除空间，您必须紧随 `DROP TABLE` 语句之后执行 `PURGE` 命令。`PURGE` 命令用于永久从数据库中移除被删除的对象。根据您想要实现的目标，`PURGE` 命令可以通过几种不同的方式使用。

| **Purge 命令** | **效果** |
|---|---|
| `PURGE TABLE *table*` | 从回收区域清除列出的表。 |
| `PURGE TABLESPACE *tablespace_name*` | 清除指定表空间中所有被删除的表。 |
| `PURGE TABLESPACE *tablespace_name* USER *user*` | 这将清除表空间中特定用户的所有被删除的表。 |
| `PURGE RECYCLEBIN` | 清除当前用户的回收站。 |
| `PURGE DBA_RECYCLEBIN` | 具有 SYSDBA 权限的用户可以清除所有用户的回收站。 |

与其他闪回功能一样，如果正确使用，此功能可以为您节省大量的时间和精力。

![](img/9479df2d00f5e62b87366b125224950f_346_0.png)

> 说明
> 闪回删除功能仅适用于表。表空间、用户和其他对象会立即被删除，无法通过闪回删除功能恢复。

## 闪回数据库

闪回数据库功能将两种闪回功能与 RMAN 结合起来，自动将数据库闪回到某个时间点。闪回数据库功能需要基于磁盘的自动备份和闪回复用区。使用闪回数据库时，存储在闪回复用区中的备份文件和归档日志用于将数据库恢复到特定的时间点。

闪回数据库命令在性质上类似于时间点恢复，只是其中大部分操作是自动完成的。闪回数据库设置为默认的闪回复用周期，并将数据库配置为闪回模式。一旦完成此操作，就可以使用 RMAN 中的 `FLASHBACK DATABASE` 命令将数据库恢复到某个时间点。指定闪回点有几种方法，如下表所示：

| 命令 | 描述 |
| :--- | :--- |
| `FLASHBACK DATABASE TO SCN scn#` | 闪回到特定的 SCN。 |
| `FLASHBACK DATABASE TO SEQUENCE sequence#` | 闪回到特定的日志序列。 |
| `FLASHBACK DATABASE TO TIME (SYSDATE-1/24);` | 闪回到过去的某个特定点。 |
| `FLASHBACK DATABASE TO TIME timestamp('2004-05-16 14:00:00');` | 闪回到特定的时间点。 |

与其他闪回功能一样，这可能非常强大，也可能非常危险。闪回数据库功能会将数据库还原到以前的某个时间点，从而覆盖此后所做的任何更改。这可能非常有用，但也可能导致更多问题。

## 制定恢复策略

规划您的恢复过程和恢复策略非常重要，以便在系统故障发生时做好准备。根据故障类型，必须为多种场景制定计划。需要恢复的故障类型包括

- 实例故障
- 介质故障
- 操作员错误

每种故障都不同，且需要不同的恢复策略。

### 规划实例恢复

如前所述，实例故障通常不需要操作员干预。主要的规划工作应侧重于并行恢复选项。通过评估您的系统，您应该确定恢复过程的并行度。这是通过 Oracle 初始化参数 `RECOVERY_PARALLELISM` 设置的。

磁盘驱动器和 CPU 的数量通常决定了系统中的并行度。我的经验法则是每两个磁盘驱动器对应一个进程（线程），上限为二十个。如果将此值设置得太高，可能会导致额外的开销。

