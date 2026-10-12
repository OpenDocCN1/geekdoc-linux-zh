
```
oracle@octilli~ > oraenv
orACLE_SID = [tst9] ?
noracle@octilli~ > sqlplus /nolog
```

SQL*Plus: Release 9.0.1.0.0 - Production on Mon Oct 23:36:19 2001

(c) Copyright 2001 Oracle Corporation. All rights reserved.

```
SQL> connect /as sysdba
Connected to an idle instance.
SQL> startup mount
ORACLE instance started.
```

| Total System Global Area | 75854976 bytes |
| Fixed Size | 279680 bytes |
| Variable Size | 71303168 bytes |
| Database Buffers | 4194304 bytes |
| Redo Buffers | 77824 bytes |

```
SQL>
```

## 2. 在命令行提示符处启动 RMAN 工具并连接到目标和恢复目录数据库 `rcat`

```
oracle@octilli: ~ rman
```

Recovery Manager: Release 9.0.1.0.0 - Production

(c) Copyright 2001 Oracle Corporation. All rights reserved.

```
RMAN> connect target
connected to target database: tst9 (not mounted)
RMAN> connect catalog rman@rcat
connected to recovery catalog
RMAN>
```

## 3. 一旦你连接到目标和恢复目录，就可以将目标数据库备份到磁盘或磁带

在本示例中，选择磁盘。为数据库指定一个备份集唯一标识符格式，然后将备份编号接到数据库名后。

```
RMAN> run
{
allocate channel c1 type disk;
backup database format 'db_%u_%d_%s';
release channel c1;
}
allocated channel: c1
channel c1: sid=DISK
Starting backup at 29-OCT-01
channel c1: starting full backupset
channel c1: specifying datafile(s) in backupset including current controlfile in backupset
input datafile fno=00001 name=/oracle/product/9.0.1/dbs/system01.dbf
input datafile fno=00002 name=/oracle/or/db/tst9/system01.dbf
input datafile fno=00003 name=/oracle/or/db/tst9/undo01.dbf
input datafile fno=00004 name=/oracle/or/db/tst9/temp01.dbf
input datafile fno=00005 name=/oracle/or/db/tst9/users01.dbf
input datafile fno=00006 name=/oracle/or/db/tst9/data01.dbf
input datafile fno=00007 name=/oracle/or/db/tst9/idx01.dbf
channel c1: starting piece 1 at 29-OCT-01
channel c1: finished piece 1 at 29-OCT-01
channel c1: backup set complete, elapsed time: 00:01:57
Finished backup at 29-OCT-01
released channel: c1
```

## 4. 一旦备份完成，即可还原数据库

数据库必须处于挂载状态而非打开。在还原脚本中，选择三个通道来利用还原过程的并行化。`RESTORE` 命令负责 RMAN 内部的还原过程。由于数据库处于 NOARCHELOG 模式且还原了整个数据库，因此不需要恢复。

```
RMAN> run
{
  allocate channel c1 type disk;
  allocate channel c2 type disk;
  allocate channel c3 type disk;
  restore database;
}
```

## 5. 一旦数据库还原完成，就可以打开它然后正常关闭

此时，应该执行一次启动以确保还原过程成功。

```
SQL> alter database open;
```

Database altered.

```
SQL> shutdown
Database closed.
Database dismounted.
ORACLE instance shut down.
```

```
SQL> startup
ORACLE instance started.
Total System Global Area 75854976 bytes
Fixed Size 279680 bytes
Variable Size 71303168 bytes
Database Buffers 4194304 bytes
Redo Buffers 77824 bytes
Database mounted.
Database opened.
SQL>
```

# 在 ARCHIVOG 模式下执行 RMAN 完整恢复

作为用 RMAN 进行恢复的第二个示例，你将在 ARCHIVOG 模式下恢复数据库。在这种情况下，数据库可以挂载，也可以打开。这是因为当数据库处于打开且处于 ARCHIVOG 模式时，可以备份数据库文件，其方式类似于用户管理的 `ALTER TABLESPACE <tablespace_name> BEGIN BACKUP` 命令。

# 314 第10 章 • 用户管理的完全恢复与 RMAN 的完全恢复

(c) Copyright 2001 Oracle Corporation. 保留所有权利。

```
RMAN> connect target
```

连接到目标数据库: `tst9` (未挂载)

```
RMAN> connect catalog rman/rman@rcat
```

连接到恢复目录数据库

```
RMAN>
```

## 3. 一旦你连接到目标数据库和恢复目录，你就可以将目标数据库（包括归档日志）备份到磁盘或磁带

在例例中，你选择了磁盘。为格式 `db_%u_%d_%s` 设定一个数据库名称，这意味着 `db_` 将与备份集的唯一标识符拼接，然后与备份集编号拼接。

```
RMAN> run
{
3> allocate channel c1 type disk;
4> backup database format 'db_%u_%d_%s';
5> backup format 'log_%t_s_%s_%p'
6> (archivelog all);
7 )
```

allocated channel: c1

channel c1: sid=11 devtype=DISK

Starting backup at 30-OCT-01

channel c1: starting full datafile backup

channel c1: specifying datafile(s) in backup

including current controlfile in backup

input datafile fno=00001 name=/db01/oracle/tst9/system01.dbf

input datafile fno=00006 name=/db01/oracle/tst9/data01.dbf

Copyright©2002 SYBEX, Inc., Alameda, CA www.sysex.com

# 在 ARCHIVELOG 模式下执行 RMAN 完全恢复 315
