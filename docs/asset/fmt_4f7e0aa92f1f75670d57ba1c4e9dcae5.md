
# 数据库文件路径

- `/db01/ACLE/tst9/temp01.dbf`
- `/db01/ACLE/tst9/users01.dbf`
- `/db01/ACLE/tst9/tools01.dbf`
- `/db01/ACLE/tst9/data01.dbf`
- `/db01/ACLE/tst9/indx01.dbf`

7 rows selected.

SQL>

```bash
rm /db01/ACLE/tst9/users01.dbf
```

## 5. 数据库并验证发生“无法识别/锁定数据文件”的错误

```bash
[oracle@DS-LINUX tst9]$ sqlplus /nolog
```

```
SQL*Plus: Release 9.0.1.0 - Production on Thu Nov 1 21:04:10 2001
(c) Copyright 2001 Oracle Corporation. All rights reserved.
```

```sql
SQL> connect / as sysdba
Connected.
SQL> instance started.
Total System Global Area      19504528 bytes
Fixed Size                    64912 bytes
Variable Size               16908288 bytes
Database Buffers             2457600 bytes
Redo Buffers                73728 bytes
Database mounted.
ORA-01157: cannot identify/lock data file 4 - see DBWR trace file
ORA-01110: data file 4: /db01/ORACLE/tst9/users01.dbf
```

## 6. 关闭数据库以执行完整恢复。必须关闭数据库以恢复冷备份

```sql
SQL> shutdown
ORA-01110: database not open
Database dismounted.
ORACLE instance shut down.
SQL>
```

## 7. 通过将所有数据文件、redo 日志和控制文件复制到原始位置来执行完整数据库恢复

```bash
cp /staging/cold/tst9/* /db01/ORACLE/tst9
```

## 8. 启动数据库并检查冷备份后输入的数据是否存在。当你检查时，会发现表 t1 不存在。备份后的所有数据都必须重新输入

```bash
[oracle@DS-LINUX backup]$ sqlplus /nolog
```

```
SQL*Plus: Release 9.0.1.0 - Production on Thu Nov 1 21:04:10 2001
(c) Copyright 2001 Oracle Corporation. All rights reserved.
```

```sql
SQL> connect test/test
Connected.
SQL> select * from t1;
ORA-00942: table or view does not exist
SQL>
```

## 结论

最明显的观察是，当数据库处于 `NOARCHIVELOG` 模式时，数据会丢失。备份后的所有数据都丢失且必须重新输入。为了恢复它，必须关闭数据库。此外，您必须恢复整个数据库，而不仅仅是丢失的文件，这可能会增加恢复时间。

# 在 ARCHIVELOG 模式下执行用户完整恢复

在本例中，由于处于 `ARCHIVELOG` 模式，数据库被完全恢复。该数据库每天可用 24 小时（维护期间除外）。每天执行热备份。数据文件、归档日志和控制文件被复制到阶段目录，然后复制到磁带。副本保留在磁盘上，直到第二天再次运行热备份。当备份再次运行时，阶段目录会被清除并重写。

## 诊断故障

周三早上，数据库中有一个丢失或删除的数据文件。启动时收到的错误如下：

```sql
SQL> startup
ORACLE instance started.
Total System Global Area 19504528 bytes
Fixed Size 64912 bytes
Variable Size 16908288 bytes
Database Buffers 2457600 bytes
Redo Buffers 73728 bytes
Database mounted.
ORA-01157: cannot identify/lock data file 4 - see DBWR trace file
ORA-01110: data file 4: /db01/ORACLE/tst9/users01.dbf
```

在这种情况下，您在 `ARCHIVELOG` 模式下操作，因此只需要替换损坏或丢失的文件：`/db01/oracle/tst9/users01.dbf`。然后，打开数据库后，可以将归档日志应用于数据库。此归档日志操作将重新应用数据库的所有更改；因此不会丢失数据。

## 逐步恢复

要恢复丢失的数据文件，请采取以下步骤：

### 1. 连接到用户 TEST 并在 USERS 表空间（包含 users01.dbf）中表 t1 输入数据。这将模拟 USERS 表空间热备份中的数据

```bash
oracle@DS-LINUX backup]$ sqlplus /nolog
```

```
SQL*Plus: Release 9.0.1.0 - Production on Thu Nov 1 21:04:10 2001
(c) Copyright 2001 Oracle Corporation. All rights reserved.
```

```sql
SQL> connect test/test
Connected.
SQL> insert into t1 values (1,'This is test one before hot backup')
1 row processed.
SQL> connect / as sysdba
SQL> commit;
Statement processed.
```

```sql
SQL> select username,default_tablespace from dba_users where username = 'TEST';
USERNAME                DEFAULT_TABLESPACE
------------------------------------
TEST                               USERS
1 row selected.
```

### 2. 通过将表空间置于备份模式执行 USERS 表空间的备份。将数据文件 users01.dbf 复制到阶段目录。然后备份 USERS 表空间

```
SQL*Plus: Release 9.0.1.0.0 - Production on Thu Nov 1 21:04:10 2001
(c) Copyright 2001 Oracle Corporation. All rights reserved.
```

```sql
SQL> connect /as sysdba
Connected.
SQL> alter tablespace users begin backup;
Statement processed.
SQL ! cp /db01/ORACLE/tst9/users01.dbf /stage
SQL> alter tablespace users end backup;
Statement processed.
SQL> alter system switchfile;
Statement processed.
```

### 3. 连接到用户 TEST 并向表 t1 添加更多数据。这些数据位于第 2 和第 3 行。这些数据是在 users01.dbf 数据文件备份之后添加的，因此这些数据不属于较早复制的文件。完成后，执行日志切换以模拟数据库的正常活动。这将激活归档进程，为新添加的数据生成归档日志

```sql
SQL> connect test/test
Connected.
SQL> insert into t1 values(2,'This is test two - after hot backup');
1 row processed.
SQL> insert into t1 values(3,'This is test three - after hot backup');
1 row processed.
SQL> commit;
Statement processed.
SQL> connect / as sysdba
Connected.
SQL> alter system switch logfile;
Statement processed.
SQL> alter system switch logfile;
Statement processed.
SQL> alter system switch logfile;
Statement processed.
SQL> alter system switch logfile;
Statement processed.
```

### 4. 验证 USERS 表空间空间数据文件的位置。然后移除或删除此文件

```sql
SQL> ! rm /db01/ORACLE/tst9/users01.dbf
```

### 5. 关闭数据库。在重启时，验证是否发生了数据丢失错误

```bash
[oracle@DS-LINUX tst9]$$ sql
```

```
SQL*Plus: Release 9.0.1.0.0 - Production on Thu Nov 1 21:04:10 2001
(c) Copyright 2001 Oracle Corporation. All rights reserved.
```

```sql
SQL> connect /as sysdba
Connected to an idle instance.
SQL> startup
ORACLE instance started.
```

| Total System Global Area | 19504528 bytes |
|--------------------------|----------------|
| Fixed Size               | 649128 bytes   |
| Variable Size            | 1690288 bytes  |
| Database Buffers         | 2457600 bytes  |
| Redo Buffers             | 73728 bytes    |

Database mounted.
ORA-01157: cannot identify/lock data file 4 - 请查看 BWDR trace文件
ORA-01110: data file 4: '/db01/ORACLE/tst9/users01.dbf'
SQL>

### 6. 将恢复的数据文件设为离线（offline）。这将允许你在数据库其他部分可用户访问的同时，恢复此数据文件和表空间

```sql
SQL> alter datafile '/db01/oracle/tst9/users01.dbf' offline;
Statement processed.
```

### 7. 通过将数据文件 users01.dbf 复制回原始位置来还原单个数据文件

```bash
[oracle@DS-LINUX tst9]$ cp /stage/users01.dbf /db01/oracle/tst9
```

### 8. 在数据库打开状态下，通过执行 RECOVER DATABASE 命令开始恢复过程。然后，应用所有可用的重做日志（redo logs）；这将实现完全恢复。最后，将数据文件恢复上线（online），以便用户访问

```sql
SQL> connect /as sysdba
Connected.
SQL> recover datafile '/db01/ORACLE/tst9/users01.dbf'
ORA-00279: change 48323 generated at 03/29/00 22:04:25 needed for thread 1
ORA-00289: suggestion : /oracle/admin/tst9/archchtst9_84.log
ORA-00280: change 48323 for thread 1 is in sequence #84
指定日志：{<RET>=suggested | filename | AUTO | CANCEL}
Log applied.
ORA-00279: change 48325 generated at 03/29/00 22:05:25 needed for thread 1
ORA-00289: suggestion : /oracle/admin/tst9/arch1/archst9_85.log
ORA-00280: change 48325 for thread 1 is in sequence #85
ORA-00278: log file '/oracle/admin/tst9/arch1/archst9_84.log' no longer needed for this recovery
指定日志：{<RET>=suggested | filename | AUTO | CANCEL}
Log applied.
ORA-00279: change 48330 generated at 03/29/00 22:08:41 needed for thread 1
ORA-00289: suggestion : /oracle/admin/tst9/arch1/archst9_86.log
ORA-00280: change 48330 for thread 1 is in sequence #86
ORA-00278: log file '/oracle/admin/tst9/arch1/archst9_85.log' no longer needed for this recovery
指定日志：{<RET>=suggested | filename | AUTO | CANCEL}
Log applied.
ORA-00279: change 48330 generated at 03/29/00 22:08:41 needed for thread 1
ORA-00289: suggestion : /oracle/admin/tst9/arch1/archst9_86.log
ORA-00280: change 48330 for thread 1 is in sequence #86
ORA-00278: log file '/oracle/admin/tst9/arch1/archst9_85.log' no longer needed for this recovery
指定日志：{<RET>=suggested | filename | AUTO | CANCEL}
Log applied.
Media recovery complete.
```

```sql
SQL> alter datafile '/db01/oracle/tst9/users01.dbf' online;
Statement processed.
```

### 9. 验证即使处于离线状态也没有数据丢失

```sql
SQL> select * from t1;
--------------------
1 test one
2 test two
3 test three
3 rows.
```

## 结论

关于此场景最明显的观察是，当数据库处于 `ARCHIVELOG` 模式时，没有数据丢失。另一个重要特性是在表空间恢复期间数据库可以保持打开状态。

# 将数据文件还原到不同位置

将文件还原到不同位置，数据库必须处于 `mount` 模式。主要区别在于在 `NOARCHIVELOG` 模式下，如果丢失了文件将无法完全恢复。将文件还原到不同位置，你需要执行操作系统复制，然后使用重做日志更新控制文件。让我们走一遍此流程。

### 1. 使用操作系统命令将文件还原到新位置

### 2. 启动并挂载数据库

```bash
cp /db01/oracle/tst9/users01.dbf /db02/oracle/tst9/users01.dbf
oracle@octilli:> oraenv
ORACLE_SID = [tst9]
acle@octilli:~ sqlplus /nolog
```

```
SQL*Plus: Release 9.0.1.0.0 - Production on Mon Oct 29 23:26:23 2001
(C) Copyright 2001 Oracle Corporation. All rights reserved.
```

```sql
SQL> connect /as sysdba
Connected.
SQL> startup mount
ORACLE instance started.
```

| Total System Global Area | 75854976 bytes |
|--------------------------|----------------|
| Fixed Size               | 279680 bytes   |
| Variable Size            | 71303168 bytes |
| Database Buffers         | 4194304 bytes  |
| Redo Buffers             | 77824 bytes    |

Database mounted.
SQL>
