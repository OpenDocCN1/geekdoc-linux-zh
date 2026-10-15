
cp `/stage/tools01.dbf` `/oracle/database/tst9/tools01.dbf`

cp `/stage/indx01.dbf` `/oracle/database/tst9/indx01.dbf`

```
5. 以 MOUNT 模式启动数据库。
```

```
SQL> startup mount
```

```
6. 验证所有需要恢复的数据文件均已在线。以下查询显示了每个在线数据文件的状态（系统数据文件除外，它是始终在线的；状态等于 system）。
```

```
SQL> select file#,status,enabled,name from v$datafile;
```

| FILE | STATUS | ENABLED | NAME |
| :--- | :--- | :--- | :--- |
| 1 | SYSTEM | READ WRITE | `/oracle/database/tst9/system01.dbf` |
| 2 | ONLINE | READ WRITE | `/oracle/database/tst9/rbs01.dbf` |
| 3 | ONLINE | READ WRITE | `/oracle/database/tst9/temp01.dbf` |
| 4 | ONLINE | READ WRITE | `/oracle/database/tst9/users01.dbf` |
| 5 | ONLINE | READ WRITE | `/oracle/database/tst9/tools01.dbf` |
| 6 | ONLINE | READ WRITE | `/oracle/database/tst9/data01.dbf` |
| 7 | ONLINE | READ WRITE | `/oracle/database/tst9/indx01.dbf` |

7行已。

- 7. 在 `RECOVER DATABASE` 命令中使用 `UNTIL CANCEL` 子句执行不完全恢复。

```
SQL> recover database until cancel;
```

- 8. 使用 `RESETLOGS` 选项打开数据库。

```
SQL> alter database open resetlogs;
```

对于所有类型的不完全恢复，你都必须在 `ALTER DATABASE` 命令中使用 `RESETLOGS` 子句。`RESETLOGS` 选项通过重置日志序列号并重建现有的在线 redo 日志，确保在恢复中应用的日志文件永远无法被再次使用。此过程将永久停用未归档日志文件中的所有事务，使其永远无法被恢复。同时，它会将日志文件与数据文件和控制文件同步。如果这些事务没有被清除，日志文件将产生错误的归档日志。这就是为什么在执行不完全恢复之前应该对控制文件、数据文件和 redo 日志进行备份的主要原因。

- 9. 对数据库进行新的冷或热备份。现有的备份不再有效。

> 记住，在应用 `ALTER DATABASE OPEN RESETLOGS` 命令后，之前的日志文件和备份的数据文件对于这个新恢复的数据库是无用的。这是因为日志文件中存在空隙。旧的备份数据文件和日志无法再次与数据库同步。因此，在进行任何类型的不完全恢复后，必须执行完全备份。

## 真实世界场景：使用不完全恢复迁移数据库

恢复操作可以作为工具，执行典型故障恢复以外的活动。由于原因，你需要熟悉与不完全恢复相关的备份和恢复功能及能力。

### 执行数据库不完全恢复

不完全恢复选项（例如备份控制文件结合 `RECOVER DATABASE USING BACKUP CONTROLFILE UNTIL CANCEL` 命令使用）在你尝试将数据库从一个位置移动到另一个位置时会非常有用。当你使用此类选项时，你可以出于任何目的迁移数据库，例如为了测试迁移数据库，或将数据库迁移到新服务器。你必须确保，如果你正在将数据库迁移到新服务器，新服务器上的 Oracle 数据库软件和操作系统是类似的。

这种迁移数据库的方法通过对要迁移的数据库进行热或冷备份，并将数据文件和初始化文件移动到新位置来实现。然后，你需要更改备份控制文件，指向所有物理数据库文件（如 redo 日志和数据文件）的路径引用。完成后，你需要验证你的 `ORACLE_SID` 并确保它指向正确的数据库；然后你需要在 SQL 提示符处以 `sysdba` 身份执行备份控制文件。这将在新服务器和不同位置上生成一个新的数据库。请参考 Oracle 文档获取执行此任务的精确步骤，并始终尝试在测试环境中运行此过程。

作为一名 DBA，你将由于许多原因负责建立测试环境。你会发现，为了测试和升级目的，在不同服务器之间迁移并设置数据库及应用程序的能力是一项必备技能。每当有任何重大升级时，都需要在生产环境之外的环境中进行测试。这种移动数据文件并重建控制文件的方法在许多测试和升级场景中效果良好。

### 基于时间的恢复

基于时间的恢复允许将数据库恢复到某个时间点。基于时间的恢复比基于 cancel 的选项更具灵活性。

特别是，基于时间的恢复允许将数据库恢复到某个时间点。基于时间的恢复比基于 cancel 的选项更具灵活性。

### 基于 SCN 的恢复

SCN（系统更改号）是 Oracle 用于唯一标识事务的。每个 SCN 是一个时间点。

### 丢失 redo 日志后的恢复

这些 SCN 之间的事务都包含在这些日志中。SCN 也记录在回滚段、控制文件和数据文件头中。

不完全恢复在当丢失了当前和/或活动未归档的 redo 日志时是必要的。在这种情况下，你没有故障点之前的所有 redo 日志文件，因此唯一的替代方案是恢复到故障点之前。

Oracle 已经通过改进来补偿这种失败，提供了……

在警报日志中可能会看到的错误消息有 `ORA-00255`、`ORA-00312`、`ORA-00286`，以及这些消息都指示了写入在线 redo 日志文件的问题。

在在线 redo 日志丢失后执行不完全恢复，你执行以下操作：

1. 启动 Server Manager 并执行 `CONNECT INTERNAL` 命令。
```
SQL> connect / sysdba ;
```
2. 执行 `SHUTDOWN` 命令并复制所有数据文件。
```
SQL> shutdown;
cp /stage/data01.dbf /oracle/database/tst9/data01.dbf
cp /stage/rbs01.dbf /oracle/database/tst9/rbs01.dbf
cp /stage/temp01.dbf /oracle/database/tst9/temp01.dbf
cp /stage/users01.dbf /oracle/database/tst9/users01.dbf
cp /stage/tools01.dbf /oracle/database/tst9/tools01.dbf
cp /stage/indx01.dbf /oracle/database/tst9/indx01.dbf
```
3. 执行 `STARTUP MOUNT` 命令以读取控制文件的内容。
```
SQL> startup mount;
```
4. 执行 `RECOVER DATABASE UNTIL CANCEL` 命令以启动恢复过程。
```
SQL> recover database until cancel;
```
5. 应用必要的归档日志，但不包括丢失或损坏的日志。
6. 打开数据库并重置日志文件。
```
SQL> alter database open resetlogs;
```
7. 切换日志文件，以检查新日志是否工作正常。
```
SQL> alter system switch logfile;
```
8. 关闭数据库。
```
SQL> shutdown normal;
```
9. 执行 `STARTUP` 和 `SHUTDOWN NORMAL` 命令，通过检查执行这些命令后的 alert 日志来验证数据库功能正常。
```
SQL> startup;
```
```
SQL> shutdown normal;
```
10. 执行冷备份或热备份。

![](img/a183fd041839741f5ab6df3caffc6b52_405_0.png)

如果你需要从不同的位置恢复归档日志，只需将 `LOG_ARCHIVE_DEST` 更改为归档日志文件的新位置。这可能发生在恢复场景中，即你从磁带将归档日志恢复到磁盘上的临时暂存位置。

## 使用 UNTIL TIME 执行基于 RMAN 的不完全恢复

在本例中，你将执行一种特定类型的 RMAN 不完全恢复。你将把数据库恢复到特定的时间点。为了实现这一目标，你将创建一个名为 TEST 的用户，并创建两个存储了日期和时间数据的表。然后，你将在 ARCHIVELOG 模式下执行数据库备份，恢复到 2:31（数据存储在第一个表中）和 3:59（数据存储在第二个表中）之间的某个时间。你通过 RMAN 中的 `SET UNTIL TIME` 子句完成所有这些操作；执行不完全恢复时需要使用该子句。因此，当数据库恢复后，你将看不到第二个表的数据。当恢复完成并验证后，你需要在恢复目录中注册数据库。让我们来看这个示例：

1. 将 `ORACLE_SID` 设置为 tst9（即你的目标数据库），以便可以使用 SQL 在 MOUNT 或 OPEN 模式下启动数据库。
```
oracle@octilli:~ > . oraenv
ORACLE_SID = [tst9] tst9
oracle@octilli:~ >
```
```
SQL> startup mount
Oracle instance started
database mounted
```

| 总系统全局区 (Total System Global Area) | 75854976 bytes |
| :--- | :--- |
| 固定大小 (Fixed Size) | 279680 bytes |
| 可变大小 (Variable Size) | 71303168 bytes |
| 数据库缓冲区 (Database Buffers) | 4194304 bytes |

或者
```
SQL> startup mount
ORACLE instance started.
Total System Global Area | 75854976 bytes |
Fixed Size | 279680 bytes
Variable Size | 71303168 bytes
Database Buffers | 4194304 bytes
Redo Buffers | 77824 bytes
Database mounted.
```
