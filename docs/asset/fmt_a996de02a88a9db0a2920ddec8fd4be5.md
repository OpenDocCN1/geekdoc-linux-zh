
系统已更改。

注意没有尝试备份在线日志。记住你只有冷备份中才有在线日志。备份控制文件不是热备份的一部分。

这些步骤构成了热备份的基础。它们提供了一种在数据库可用时进行备份的方法。一旦文件备份，就可以结合冷备份来恢复数据库。

# 从热备份期间的崩溃恢复

由于热备份可能需要几个小时，逻辑上可以假设数据库在热备份期间会发生崩溃。如果发生这种情况，你不能简单重启数据库。Oracle 需要打开其数据，发现某个表空间处于热备份模式，并请求介质恢复。幸运的是，尽管这是一个常见故障，修复相对容易。

在此示例中，假设 `USERS` 表空间处于热备份模式，由于某种原因机器重启了。启动时，你需要执行以下操作：

1. 你启动数据库并遇到以下内容：

```sql
SQL> startup

ORACLE instance started.

Total Global Area  128184304 bytes
Fixed Size         69616 bytes
Variable Size      78413824 bytes
Database Buffers   49152000 bytes
Redo Buffers       548864 bytes
Database mounted.

ORA-01113: file 5 needs media recovery
ORA-01110: data file 5: '/u04/oradata/rhdev1/users01.dbf'
```

2. 识别需要的文件。

```sql
SQL> select * from v$recover_file;

FILE ONLINE ERROR CHANGE TIME
--------------------------------------------
5 ONLINE 247341 22-APR-01

SQL> select name from v$dbfile where file# = 5;

NAME
----------------------------------------------------------------------------
/u04/oradata/rhdev1/users01.dbf
```

3. 因为你知道数据库在崩溃时正处于热备模式，这并不寻常。只需将数据文件从热备模式中移出并打开数据库即可。

```sql
SQL> alter database datafile
2 '/u04/oradata/rhdev1/users01.dbf'
3 end backup;

数据库已更改。

SQL> alter database open;

数据库已更改。
```

这已经是尽可能简单的“恢复”操作了。实际上，你并没有恢复任何东西，你只是更改了 Oracle 可以使用的文件状态。

# 从丢失的数据文件中恢复

数据文件的丢失本身不不应该导致数据库崩溃（变为无法访问）。假设通过热备份或冷备份提供了可用的备份，并且自该备份以来的所有归档日志文件都可用，那么就可以进行完全恢复。在此过程中，你将恢复 `USERS` 表空间。

1. 识别出存在的问题。数据字典视图 `V$RECOVER_FILE` 和 `alert.log` 是获取此类信息的两个最佳来源。

```sql
SQL> select * from v$recover_file;

ONLINE ERROR CHANGE TIME
--------------------------------------------
5 OFFLINE FILE NOT FOUND 0
```

`alert.log` 显示：

```
Sun Apr 22 23:02:21 2001
Errors in file 5: '/u01/app/oracle/admin/rhdev1/bdump/ckpt_9977.trc:
ORA-01171: datafile 5 going offline due to error advancing checkpoint
ORA-01116: error in opening database file 5
ORA-01110: data file 5: '/u04/oradata/rhdev1/users01.dbf'
ORA-27041
Linux Error: 2: No such file or directory
```

2. 在此阶段，该表空间的内容是无法访问的。然而，根据丢失的性质，文件可能在 `DBA_DATA_FILES` 或 `DBA_TABLESPACES` 中被标记为 `OFFLINE`（离线）。

```sql
SQL> select * from danw.test_table;
select * from danw.test_table
*
ERROR at line 1:
ORA-00376: file 5 cannot be read at this time
ORA-01110: data file 5: '/u04/oradata/rhdev11/users01.dbf'
```

3. 将相应的表空间离线。

```sql
SQL> alter tablespace users offline temporary;

表空间已更改。
```

4. 恢复丢失或损坏的文件。如果无法恢复到原文件，将其重命名到不同的位置。在这种情况下，你从热备位置恢复文件。

```bash
$ cp /backup/rh1dev1/hot_backups/users01.dbf /u04/oradata/rhdev11/users01.dbf
```

5. 通过应用归档日志恢复数据库文件。这样做最简单的方法是使用 `ALTER DATABASE RECOVER TABLESPACE AUTOMATIC`。通过这种方式，Oracle 将自动应用归档目标位置中的归档日志文件，而无需提示 DBA。这确保了每个归档日志都是未压缩的。

```sql
SQL> alter database recover automatic tablespace users;

数据库已更改。
```

6. 验证文件不再需要恢复，并将表空间上线。

```sql
SQL> select * from v$recover_file;

no rows selected

SQL> alter tablespace users online;

表空间已更改。
```

7. 验证该表空间中的对象是否可用。

```sql
SQL> select count(*) from danw.test_table;

COUNT(*)
----------
```

数据文件（因此表空间）现在可以用了。虽然只丢失了数据文件，但此示例恢复了整个表空间。选择这种方法是因为你可能需要从一个表空间恢复多个数据文件。然而，步骤 #5 也可以使用以下语句：

```sql
SQL> alter database recover automatic datafile
2 /u04/oradata/rhdev1/users01.dbf;

数据库已更改。
```

这次恢复是 Oracle 健壮性的一个良好示例。尽管表空间不可用，但数据库的其他部分仍保持打开状态。还要注意，数据没有丢失，在备份文件和一系列归档日志文件之间，Oracle 能够重建对 `USERS` 表空间中任何对象进行的所有更改。

# 从丢失的临时或索引表空间恢复

理论上，如果你丢失了临时或索引表空间，你只需要删除并重新创建它们即可。步骤如下：

```sql
SQL> drop tablespace temp;

表空间已删除。

SQL> select * from v$recover_file;

no rows selected

SQL> create tablespace temp
2 datafile /u03/oradata/rhdev1/temp01.dbf size 200M
3 minimum extent 64K
4 default storage (initial 64K next 64K
5 maxextents unlimited pctincrease 0)
6 temporary;

表空间已创建。
```

原理是临时或索引表空间都不包含关键数据，它们更容易重建。在重建临时表空间时我倾向于同意这一点，但在重建索引表空间时不然。如果丢失了索引表空间，只要不使用索引，表空间中的数据是可以访问的。例如，全表扫描可以运行，但插入新行将失败。

```sql
SQL> insert into test_table values ('c', 3);
ERROR at line 1:
ORA-00376: file 8 cannot be read at this time
ORA-01110: data file 8: '/u04/oradata/rhdev1/employee_idx.dbf'
```

如果你知道丢失表空间中的索引并有重建它们的脚本，这可能是最快的。否则，像恢复其他表空间一样恢复索引文件。

```sql
SQL> alter database recover tablespace employee_idx;

数据库已更改。

SQL> alter tablespace employee_idx online;

表空间已更改。
```

# 从丢失的重做日志成员恢复

如果是多余的，丢失在线 redo 日志文件并不是大问题。理论上，只要成员是冗余，数据库就不会崩溃，尽管 Oracle 会在 `alert log` 中发出错误。然而，如果丢失了整个组，预计数据库将崩溃。这种情况假设你对重做日志做了镜像并且至少有两个成员。在危机发生之前，让我们查看组和成员。从下面可以看出，你有三个组，每组有两个成员。

```sql
SQL> select * from v$log order by group;

GROUP STATUS MEMBER
--------------------------------------------
1 | /u03/oradata/rhdev1/redo01a.redo
1 | /u04/oradata/rhdev1/redo01b.redo
2 | /u07/oracle/rhdev1/redo02a.redo
2 | /u08/oracle/rhdev1/redo02b.redo
3 | /u11/oracle/rhdev1/redo03a.redo
3 | /u12/oracle/rhdev1/redo03b.redo

6 rows selected。
```

接下来，你恢复当前日志，它恰好是第 2 组。

```sql
SQL> select group#, members, status from v$log;

GROUP MEMBERS BYTES STATUS ARC
--------------------------------------------
1 2 768000 INACTIVE YES
2 2 768000 CURRENT NO
3 2 768000 INACTIVE YES
```

如果你突然丢失了 `redo01a.redo`，你会在 `alert log` 中看到以下错误。此错误会在 redo 日志切换（尝试使第 1 组激活）时出现。

```
Sun Apr 23 08:54:13 2001
Errors in file /u01/app/oracle/admin/rhdev1/bdump/lgwr_074.src:
ORA-00313: open failed for members of group 1 of thread 1
ORA-00312: online log thread 1: '/u03/oradata/rhdev1/redo01a.redo'
ORA-27037: 2: No such file or directory
Additional information: 3
Mon Apr 23 08:54:13 2001
Errors in file /u01/app/oracle/admin/rhdev1/bdump/lgwr_074.src:
ORA-00312: log of thread 1, cannot update log file header
ORA-00312: online log thread 1: '/u03/oradata/rhdev1/redo01a.redo'
Mon Apr 23 08:54:13 2001
Errors in file /u01/app/oracle/admin/rhdev1/bdump/lgwr_074.src:
ORA-00313: open failed for members of group 1 of thread 1
```

在此阶段，不要惊慌，因为数据库仍在运行。Oracle 只是知道它缺少了一个成员。这里要记住重要的是不要从备份中恢复 redo 日志副本，如果这样做，你将丢失尝试“修复”的 redo 日志中的任何数据。解决此问题的方法是删除丢失的成员，然后在相同或不同的位置重建它。

1. 强制日志切换使该组不再处于激活状态。这是必要的，因为你不能删除“当前”（current）日志成员。

```sql
SQL> alter system logfile;

系统已更改。

SQL> select group#, status, members from v$log;

GROUP# STATUS MEMBERS
--------------------------------------------
1 INACTIVE 2
2 CURRENT 2
3 INACTIVE 2
```

2. 删除丢失的成员。

```sql
SQL> alter database drop logfile member
2 '/u03/oradata/rhdev1/redo01a.redo'

数据库已更改。
```

如你所见，第 1 组只有一个成员。

```
组 状态 成员
--------------------------------------------
1 | /u04/oradata/rh1dev/redo01b.rdo
2 | /u07/oradata/rh1dev/redo02a.rdo
2 | /u08/oradata/rh1dev/redo02b.rdo
3 | /u11/oradata/rh1dev/redo03a.rdo
/u12/oradata/rh1dev1/redo03b.rdo
```

3. 为组 1 添加缺失的成员。这可以位于相同的位置，也可以位于不同的位置。

```sql
alter database logfile member
'/u03/oradata/rh1dev/redo01a.rdo' to group 1;
Database altered.
```

4. 一旦日志文件成员被添加，它将显示为 `INVALID`（无效）。不要担心这个周期；通过几次 redo 切换来使文件变为有效。

```sql
SQL> select * from vfile where group# = 1;
GROUP STATUS MEMBER
1 INVALID /u03/oradata/rh1dev/redo01a.rdo
1 /u04/oradata/rh1dev/redo01b.rdo

SQL> alter system switch logfile;

System altered.
```

以上涵盖了联机重做日志（online redo log files）的基本恢复过程。只要你没有丢失整个组，或者尝试从备份中恢复 redo 日志，恢复应该相当简单。

# 从丢失的控制文件中恢复

如果你丢失了控制文件（control file），你的数据库需要关闭。有时实例在崩溃前仍能存，但用户会遇到问题。最佳解决方案是执行 `SHUTDOWN ABORT` 并恢复控制文件。虽然你可能丢失了一个控制文件，只要你有一个控制文件的良好副本，就有两个非常简单的恢复选项。

恢复此问题的简单方法是编辑 `config.ora` 或 `init.ora` 文件以包含良好的控制文件。例如，如果丢失了 2 号控制文件，只需从数据库启动时读取的控制文件列表中将其移除即可。

```sql
control_files = ("/u01/app/oracle/oradata/rh1st1/control01.ctl",
"/u03/oradata/rh1st1/control03.ctl")
```

然后正常启动数据库。`V$CONTROLFILE` 现在将显示现有数据库文件；你可以继续正常业务。

一个更好的长期方案是用一个良好的控制文件替换坏掉的控制文件。要做到这一点，请遵循以下步骤：

1. 确保数据库已关闭，尽管在大多数情况下它已经崩溃了。
2. 如果损坏的控制文件仍然存在，请将其删除。此删除操作是多余的，但可以防止你不小心复制错误的文件。
3. 使用 `cp` 将一个良好的控制文件复制到损坏或缺失控制文件的位置。注意你不要使用 `mv`，因为你不想将良好的副本保留在当前位置。
4. 使用 `mv` 将恢复的控制文件重命名为 `configSID.ora` 或 `initSID.ora` 文件列出的名称。
5. 正常启动数据库。Oracle 将在 `V$CONTROLFILE` 中确认该文件的存在，正常操作可以继续。

如果你丢失了所有控制文件，恢复将困难得多。希望你已经在热备脚本中包含了 `ALTER DATABASE BACKUP CONTROLFILE TO TRACE`，这样你就有文件可以处理。你必须重新创建控制文件来恢复数据库；这项任务完全超出了本书的范畴。在这种情况下，建议联系 Oracle 支持。

# 从多个文件丢失组合恢复
