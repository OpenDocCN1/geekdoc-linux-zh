
oracle@ocommit: ~ `sqlplus /nolog`

```
SQL*Plus: Release 9.0.1.0.0 - Production on Tue Sep 25 19:08:25
```

oracle@ocommit: ~ `sqlplus /nolog`

```
SQL*Plus: Release 9.0.1.0.0 - Production on Tue Sep 25 19:08:25
```

Copyright©2002 SYBEX, Inc., Alameda, CA
www.sysex.com

# 配置数据库的 ARCHIVLOG 模式和自动归档 205

Copyright©2002 SYBEX, Inc., Alameda, CA
www.sysex.com

## 210 第 7 章 配置数据库归档模式

1. 首先，编辑 `init.ora` 文件并将参数 `LOG_ARCHIVE_START` 修改为 `TRUE`。结果是数据库将进入自动 `ARCHIVELOG` 模式。见下面的 `init.ora` 文件示例。

```
###########################################
# Init.ora 文件部分示例
###########################################
###########################################
## 归档日志
###########################################
log_archive_start=true
log_archive_dest=/oracle/admin/orc9/%arch
log_archive_format=archorc9_%s.log
```

2. 接下来在 SQL 中运行以下命令：

```sql
SQL shutdown
SQL startup mount
SQL alter database archlog;
SQL alter database open;
```

该数据库现在已启用自动功能。要验证数据库是否配置正确，可以执行以下检查。

1. 首先，执行 `ALTER SYSTEM SWITCH LOGFILE`。这需要执行 $n + 1$ 次，其中 $n$ 是数据库中重做日志（redo logs）的数量。

```sql
SQL alter system switch logfile;
```

2. 接下来，对 `LOG_ARCHIVE_DEST` 中的归档目标执行目录列表。Unix 命令 `pwd` 显示当前工作目录，`ls` 显示目录内容。

```
oracle@octilli:/oracle/admin/orc9/arch > ls -ltr
total 276
-rw-r---- 1 oracle dba 133632 Sep 25 00:27 archorc9_3.log
-rw-r---- 1 oracle dba 125952 Sep 25 00:28 archorc9_4.log
-rw-r---- 1 oracle dba 1024 Sep 25 00:28 archorc9_5.log
-rw-r---- 1 oracle dba 1536 Sep 25 00:28 archorc9_6.log
-rw-r---- 1 oracle dba 1024 Sep 25 00:28 archorc9_7.log
oracle@octilli:/oracle/admin/orc9/arch >
```

另一种验证自动归档功能已启的方法是执行 `ARCHIVE LOG LIST` 命令，它显示这些设置的状态（如下）。

```sql
SQL> archive log list;
Database mode Archive Mode
Automatic archival Enabled
Archive destination /oracle/admin/orc9/arch
Oldest log sequence 6
Next log sequence to archive 8
Current log sequence 8
SQL>
```

> 如果启用了 `ARCHIVOG` 但由于没有通过编辑 `init.ora` 并将 `LOG_ARCHIVE_START` 更改为 `TRUE` 而未能启用自动归档，数据库在达到最后一个可用重做日志时将会挂起。您需要执行手动归档作为临时修复，或者在更改 `LOG_ARCHIVE_START` 参数后关闭并启动数据库。

![](img/4d4ebf1b63c52ce2a364aa79830c39e0_254_0.png)

| 现实世界场景 |
| :--- |
| 为归档日志提供足够的空间 |
| `ARCHIVLOG` 模式所需的额外磁盘空间经常被忽略或低估。对于普通数据库，您应该有足够的空间保留一到两天的归档日志在线运行。为了估算文件的正确大小，您需要估算交易高峰期间的量。峰值时间通常是事务活动或批处理活动最频繁的时候。将此估算大小乘以设置的 `log_archive_dest_n_locations` 数量。如果您在系统上进行每晚热备，从归档日志的角度来看，一到两天的归档日志应该满足您大多数的恢复需求。 |

> 但如果归档进程没有足够的磁盘空间写入归档日志，数据库将挂起或停止所有活动。这种挂起状态将一直持续，直到您通过将旧的归档日志移出系统、压缩日志文件或通过设置自动化作业在日志写入磁带后将其删除。在尝试为归档进程释放空间时，您必须小心不要放错或删除归档日志。请记住，这些归档日志在恢复情况下可能是需要的。

## 手动归档日志

日志的手动归档包括启用数据库以启用 `ARCHIVLOG` 模式，然后从 SQL 手动执行 `ARCHIVE LOG` 命令。`init.ora` 参数 `LOG_ARCHIVE_START` 必须设置为 `FALSE` 以禁用自动归档。下一步是通过执行以下命令将数据库置于 `ARCHIVLOG` 模式：

```sql
SQL> shutdown
SQL> startup mount
SQL> alter database archivel;
SQL> alter database open;
```

现在您准备可以使用以下命令进行重做日志的手动归档：

```sql
SQL> archive log all;
```

或

```sql
SQL> archive log next;
```
