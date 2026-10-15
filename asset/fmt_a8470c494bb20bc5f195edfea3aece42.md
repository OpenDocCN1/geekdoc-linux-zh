
然后正常启动数据库。`V$CONTROLFILE` 现在将只显示现有数据库文件；你可以继续进行正常业务。

# Unix 和 Linux 上的 Oracle DBA

一个更好的长期方案是用良好的控制文件替换损坏的控制文件。要这样做，请遵循以下步骤：

- 1. 确保数据库已关闭，尽管在大多数情况下它已经崩溃。
- 2. 如果损坏的控制文件仍然存在，请将其删除。此删除操作是多余的，但它可以防止你不小心复制错误的文件。
- 3. 复制（使用 `cp`）良好的控制文件到损坏或缺失控制文件的位置。注意你不要使用 `mv`，因为你想将良好的副本保留在当前位置。
- 4.（使用 `mv`）将恢复的控制文件重命名为 `configSID.ora` 或 `initSID.files` 中列出的名称。
- 5. 正常重启数据库。Oracle 将在 `V$CONTROLFILE` 中确认该文件的存在，正常操作可以继续。

然而，如果你丢失了所有控制文件，恢复将变得困难得多。希望你已经在备份脚本中包含了 `ALTER DATABASE BACKUP CONTROLFILE TO TRACE`，这样你就有文件可以处理。你必须重新创建控制文件来恢复数据库；这项任务完全超出了本书的范围。在这种情况下，建议联系 Oracle 支持。

# 从多个文件丢失组合中恢复

本章涵盖了丢失单个数据、在线重做日志和控制文件的基础知识。只要你有备份并对控制文件和在线重做日志文件进行了多路备份，每个文件的恢复都是相当简单的。遗憾的是，磁盘崩溃很少只带走一个文件。通常，你会同时丢失多个文件，这增加了恢复的复杂性。本节列出了控制文件、在线重做日志文件、`SYSTEM` 表空间和 `INDEX` 表空间的恢复示例。

假设磁盘损坏并丢失了 `/u02`。

```bash
$ ls /u02/oradata/rhdev1

control01.ctl employee idx01.dbf redo03.dbf system01.dbf
```

由于你同时丢失了控制文件和 `SYSTEM` 表空间，数据库将崩溃。这个问题需要离线数据库恢复。你需要按照以下顺序还原并恢复文件：

- 1. 恢复控制文件。
- 2. 恢复 `SYSTEM` 表空间。由于你已经在进行恢复，在这一步中将 `INDEX` 表空间包含进来是一个好主意。
- 3. 丢弃在线重做日志文件。它将在数据库恢复后重新创建。

## 备份与恢复

# 第9章

按照以下步骤恢复数据库：

- 1. 确保数据库已关闭且所有后台进程已停止。如果实例尽管损坏仍在运行，请使用 `SHUTDOWN ABORT`。
- 2. 恢复控制文件。从 `/u01` 拷贝良好的控制文件到 `/u02`，并将其赋予 `init.ora` 中指定的名称。
- 3. 从最近的有效备份恢复 `SYSTEM` 和 `INDEX` 表空间的缺失数据文件。这些可以是冷备份或热备份，副本越新，数据库恢复得越快。此外，确保自这些备份以来的所有归档日志文件已恢复到归档转储区且未压缩。
- 4. 登录 `SQLPlus`，连接内部用户，并开启恢复。

```bash
$ sqlplus internal

SQLPlus: Release 8.1.6.0 - Production on Mon Apr 23 10:28:33

(c) Copyright 1999 Oracle Corporation. All rights reserved.

Connected to an idle instance.

SQL> set recovery on
```

- 5. 以 `mount` 模式启动数据库以分配 `SGA` 并打开控制文件。这恢复了缺失的控制文件。

```sql
SQL> startup mount;

ORACLE instance started.
```

| | |
| :--- | :--- |
| Total System Area | 12818430 bytes |
| Fixed Size | 69616 bytes |
| Variable Size | 7841382 bytes |
| Database Buffers | 4915200 bytes |
| Redo Buffers | 54864 bytes |
| Database mounted. | |

- 6. 识别缺失/损坏的数据文件。

```sql
SQL> select * from v$recover_file;
```

| FILE# | ERROR | CHANGE# | TIME |
| :--- | :--- | :--- | :--- |
| 1 | ONLINE | 288346 | 23-APR-01 |
| 7 | ONLINE | 288348 | 23-APR-01 |

```sql
SQL> select * from v$dbfile where file# in (1,7);
```

| FILE# | NAME |
| :--- | :--- |
| 1 | /u02/oradata/rhdev1/system01.dbf |
| 7 | /u02/oradata/rhdev1/employee.dbf |

- 7. 识别缺失的重做日志文件。根据情况，日志成员可能被识别为 `INVALID`。然而你知道由于 `/u02` 完全丢失，该文件系统上的成员也丢失了。解决方案是丢弃它并在数据库打开后恢复它。Oracle 会抱怨该文件是活动组的成员并且不让你丢弃它，这也是可以，但你需要在下一次重做切换后丢弃它。

```sql
SQL> select * from vlogfile
```

| GROUP# | STATUS MEMBER |
| :--- | :--- |
| 1 | /u03/oradata/rh1dev1/redo1a.redo |
| 2 | /u07/oradata/rh1dev1/redo2a.redo |
| 3 | /u11/oradata/rh1dev1/redo03a.redo |
| 3 | /u02/oradata/rh1dev1/redo3b.redo |
| 2 | /u08/oradata/rh1dev1/redo2b.redo |
| 1 | /u04/oradata/rh1dev1/redo1b.redo |

6 rows selected.

```sql
SQL> alter database drop logfile member
2 '/u02/oradata/rh1dev1/redo3b.redo' to group 3;
```
