
确保归档日志文件的路径始终可用。例如，如果您的文件系统满了，导致 Oracle 无法向该位置写入归档日志文件，数据库执行任何 DML 活动时将挂起。普通查询可以运行，但将不允许进行 DML，因为 Oracle 无法对其进行归档。诊断此类问题也将非常困难，因为错误对用户是不可见的，它们只会出现在告警日志（`alert log`）中。此外，请注意文件压缩或从归档转储地拷贝的速度。我曾一次开始大量数据加载时，归档日志文件写入转储地的速度非常快。虽然我们正在写入磁盘，但可写的 CD-ROM 无法跟上文件从磁盘移动到 CD 的速度。我们几乎导致数据库挂起。

要将数据库设置为 `ARCHIVELOG` 模式，请执行以下操作：

### 1. 编辑 `initSID` 文件以包含以下值：

```
log_archive_start = true
log_archive_dest = "/u01/app/oracle/admin/rhidev1/arch"
log_archive_format = arch_rhidev1_%t.arc
```

这些参数会自动启动归档，定义归档转储地为 `$ORACLE_BASE/admin/rhidev1/arch`，并定义每个转储文件的命名格式。

### 2. 以 `mount` 模式启动数据库。

```
SQL> startup mount
ORACLE 实例 started.
```

### 3. 将数据库设置为 `ARCHIVELOG` 模式。

```
SQL> alter database archivelog;
```

Database altered.

### 4. 验证数据库状态。

```
SQL> alter database archivelog;
```

Database altered.

```
SQL> archive log list;
Database log mode         Archive Mode
Automatic archival       Enabled
Archive destination      /u01/app/oracle/admin/rhidev1/arch
Oldest log sequence       37
Next log sequence to archive 39
Current log sequence      39
```

### 5. 打开数据库以供正常使用。

```
SQL> alter database open;
```

Database altered.

## 备份与恢复

第 9 章

### 6. 强制进行日志切换并验证日志已在正确位置创建。

```
SQL> alter system switch logfile;
```

System altered.

```
SQL> ls /u01/app/oracle/admin/rhdev1/arch
arch_rhdev1_1_39.arc 格式为 thread#_sequence#.arc。其中 thread# 仅适用于存在多个实例的并行服务器实例。
```

`Sequence#` 标识归档日志文件。例如，此文件被赋予值 39；下一个日志将是 40。

以上内容涵盖了将数据库设置为 `ARCHIVELOG` 模式的基础知识。其他需要考虑的参数是，您是否想将归档日志写入多个目标地。其核心思想是，如果一个位置无法写入，有效的归档日志也将写入到备份位置。旧的参数是 `LOG_ARCHIVE_DEST`，但现在您可以使用 `LOG_ARCHIVE_DEST[.]` 指定多达五个位置。此外，成功写入每个位置可以是可选的，也可以是强制的。如果您拥有高可用性系统和大量的磁盘空间，这些参数将非常有用，但大多数数据库不需要这种程度的保护。

关于归档转储的最后一点：它们可以在数据库运行期间进行更改。例如，如果某个转储位置满了，而您有其他可以存储的文件系统，那么这是一个非常有价值的选项。只需确保在写入多个位置时不会丢失任何日志文件即可。语法如下：

# 将数据库置于热备模式

热备（在线）要求数据库处于 `ARCHIVELOG` 模式。接下来，将每个表空间置于热备模式，这会有效地冻结日志头使其无法更改。然后将控制该表空间的文件复制到备份位置。一旦完成此过程，表空间将退出热备模式。

当数据库处于热备模式时，可以发生与表空间相关的正常数据库活动，但会产生更多的重做日志（`redo logs`）。这是因为更改将在块级别记录，而不是行级别。因此，这种重做活动的增加将影响性能，这就是为什么热备通常在数据库最空闲进行。

此外，并没有要求备份每个表空间，也不要求顺序备份每个表空间。然而，在夜备份中，请这样做。此外，顺序备份每个表空间比一次性将所有表空间置于热备模式要快。请记住，与 `NOARCHIVELOG` 模式下的冷备不同，你

![](img/0735bb12e1d45128c662b4b409eb1bf1_270_0.png)

# Unix 和 Linux 上的 Oracle DBA

不需要具有匹配时间戳的数据文件。此过程会恢复每个数据文件的有效备份副本（带有不同的时间戳），并允许通过重新应用归档日志文件的恢复过程，将数据文件恢复到最新状态。

在热备模式下备份表空间需要以下步骤。

### 1. 通过将表空间置于热备模式来冻结数据文件头；

```
SQL> alter tablespace users begin backup;
```

Tablespace altered.

请记住在此期间，允许对 `USERS` 表空间中的对象进行正常访问，但代价是重做活动增加。

### 2. 接下来，使用任何操作系统命令将 `USERS` 表空间的数据文件复制到您的备份位置。这可以是到磁盘、磁带或光介质。此外，一旦文件被压缩后。

```
SQL> cp /u04/oradata/rhdev1/users01.dbf /backup/rhdev1
```

### 3. 将表空间退出热备模式。

```
SQL> alter tablespace end backup;
```

Tablespace altered.

一旦此过程完成后，表空间将处于在线。在此阶段，执行以下任务：

### 1. 将控制文件备份为跟踪文件。

```
SQL> alter database backup controlfile;
```

Database altered.

文件将创建在 `udump` 定义的位置。

### 2. 将控制文件备份为二进制副本。提供带时间戳的唯一名称。

```
SQL> alter database backup controlfile to '/backup/rhdev1/control.22';
```

### 3. 刷新在线日志以确保备份期间的更改已归档。

```
SQL> alter system archive current;
```

System altered.

## 备份与恢复

第 9 章

显然这种任务最好通过脚本而不是手动执行。我过去用于动态生成表空间的脚本位于本书的附录中。建议在您的环境中测试它们。

注意没有尝试备份在线日志。记住在 `NOARCHIVOG` 模式的数据库中备份在线日志。备份控制文件不是热备的一部分，但逻辑上要在热备结束时备份。

这些步骤构成了热备的基础。它们提供了现在数据库在线时进行可靠备份的方法。一旦文件备份，就可以结合冷备或另一个热备的文件来恢复数据库。

# 从热备期间的崩溃恢复

由于完成热备可能需要几个小时，逻辑上可以假设数据库在热备期间会崩溃。如果发生这种情况，您不能简单重启数据库。Oracle 将尝试打开其数据文件，发现表空间处于热备模式，并请求介质恢复。幸运的是，尽管这是一个常见故障，修复相对容易。

在此示例中，假设 `USERS` 表空间处于热备模式，由于某种原因机器重启了。启动时，您需要执行以下操作。

### 1. 您启动数据库并遇到以下内容：

```
SQL> startup
ACLE instance started.
```

```
Total System Global Area 128184304 bytes
Fixed Size 69616 bytes
Variable Size 78413824 bytes
Database Buffers 49152000 bytes
Redo Buffers 548864 bytes
Database mounted.
ORA-01113: file 5 needs media recovery
ORA-01110: data file 5: '/u04/oradata/rhdev1/users01.dbf'
```

### 2. 识别需要恢复的文件名。

```
SQL> select from v$recover_file;
```

```
FILE ONLINE ERROR CHANGE# TIME
5 ONLINE 247341 22-APR-01
```

```
SQL> select name from v$dbfile where file# = 5;
```

'/u04/oradata/rhdev1/users01.dbf'

### 3. 因为你知道数据库在崩溃时正处于备份模式，所以这并不寻常。只需将数据文件移出备份模式并打开数据库即可。

```
