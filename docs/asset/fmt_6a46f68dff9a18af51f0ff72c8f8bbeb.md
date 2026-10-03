
Starting restore at 30-OCT-01
using channel c3
channel c3: sid=13 devtype=DISK
channel c3: starting datafile backupset restore
using channel c1
channel c1: specifying datafile(s) to restore
from backup set
restoring datafile 00001 to `/db01/oracle/tst9/system01.dbf`
restoring datafile 00002 to `/db01/oracle/tst9/rbs01.dbf`
restoring datafile 00003 to `/db01/oracle/tst9/temp01.dbf`
restoring datafile 00004 to `/db01/oracle/tst9/users01.dbf`
restoring datafile 00005 to `/db01/oracle/tst9/tools01.dbf`
restoring datafile 00006 to `/db01/oracle/tst9/data01.dbf`
restoring datafile 00007 to `/db01/oracle/tst9/idx01.dbf`
restoring datafile 00008 to `/db01/oracle/tst9/data02.dbf`
channel c1: restored backup piece 1
piece handle=`/oracle/product/9.0.1/dbs/db_0kd7qts_TST9_20` tag=null params=NULL
channel c1: restore complete
Finished restore at 30-OCT-01
using channel c1
channel c1: sid=12 devtype=DISK
channel c1: starting datafile backupset restore
channel c1: specifying datafile(s) to restore
from backup set
restoring datafile 00008 to `/db01/oracle/tst9/data copy`
channel c1: starting piece 1 at 30-OCT-01
channel c1: finished piece 1 at 30-OCT-01
piece handle=`/oracle/product/9.0.1/dbs/TST9_`
channel c1: backup complete, elapsed time: 00:00:01

Finished restore at 30-OCT-01
released of channel: c1

RMAN>
一旦数据库完成恢复、故障备并打开，应将其正常关闭。随后应执行一次启动操作以确保恢复过程成功。

```
SQL> shutdown
SQL> startup
```

## 使用归档日志进行表空间迁移和恢复

database opened

在此示例中，你将把一个表空间迁移到新的文件系统。你可以使用之前提到的 `SET NEWNAME` 和 `SWITCH` 命令来实现。此外，`RECOVER` 命令会对数据文件和归档日志进行备份。此过程与移动文件的主要区别在于，表空间需要离线才能将关联的数据文件移动到新位置。然而，数据库在此过程中可以打开。以下是该操作的示例。

## 使用归档日志进行表空间迁移和恢复 324

1. 将 `ORACLE_SID` 设置为 ORCL（即你的目标数据库），以便可以使用 SQL*Plus 启动或挂载数据库。

```
oracle@octilli:~ \ oraenv

ORACLE_SID = [tst9] ?
```

2. 一次性连接到 RMAN、目标数据库以及恢复目录。

```
oracle@octilli:~ > rman target / catalog rman/rman@rcat
```

```
Recovery Manager: Release 9.0.1.0.0 - Production

(c) Copyright 2001 Oracle Corporation. All rights reserved.

connected to target database: TST9 (DBID=1268700551)
connected to recovery catalog database
```

3. 运行适当的 RMAN 脚本，将 tst9 数据库备份到磁盘。

```
RMAN> run

2> {

3> allocate channel c1 type disk;

4> backup database format 'db_%u_%d_%s';

5> backup format 'log_%t_t_%s_p%p'

6> (archivelog all);

7> }
```

sql 语句: `alter tablespace tools offline immediate`

执行命令: `SET NEWNAME`

开始恢复于 31-OCT-01
分配通道: ORA_DISK_1
channel ORA_DISK_1: sid=11 devtype=backupset
channel ORA_DISK_1: 启动数据文件备份
channel ORA_DISK_1: 正在指定要从备份集中恢复的数据文件
正在恢复数据文件 00005 到 `/db02/oracle/tst9/tools01.dbf`
channel ORA_DISK_1: 已恢复备份分 1
piece handle=`/oracle/product/9.0.1/dbs/db_0kd7qtqs-TST9_20` tag=null params=NULL
channel ORA_DISK_1: 恢复完成
结束恢复于31-OCT-01

数据文件 5 已切换到数据文件副本
input datafilecopy recid=344 stamp=444610301 filename=db02/oracle/tst9/tools01.f
开始恢复目录的全量同步
全量同步完成

开始恢复于 31-OCT-01
使用通道 ORA_DISK_1

开始介恢复
介恢复
归档日志线程 1 序号 16 已在磁盘上，文件 `/oracle/admin/tst9/arch/archst9_16.log`
归档日志线程 1 序号 17 已在磁盘上，`/oracle/admin/tst9/arch/archst9_17.log`
归档日志线程 1 序号 18 已在磁盘上，文件 `/oracle/admin/tst9/arch/archst9_18.log`
归档日志
filename=`oracle/admin/tst9/arch/archst9_16.log`
thread=1 sequence=6
介恢复完成

结束恢复于 31-OCT-01

sql 语句: `alter tablespace tools online`

RMAN>

## 总结

在本章中，我们强调了介恢复。我们描述了执行介质故障 Oracle 数据库恢复的两种方法（用户管理恢复和基于 RMAN 的恢复），并对每种方法执行了特定示例。

此外，我们识别了 ARCHIVELOG 模式和 NOARCHIVELOG 模式之间的区别，并描述了两种模式对备份和恢复过程的重大影响。我们还展示了使用用户管理和 RMAN 方法进行 ARCHIVELOG 模式和 NOARCHIVELOG 模式恢复的示例。

然后，我们讨论了只读表空间恢复及其相关的三个恢复场景。每种场景都需要不同的恢复操作。我们还执行了需要文件重定位的用户管理恢复和基于 RMAN 的恢复情况。

介恢复是测试和实际工作中的一个重要课题。如何处理介质恢复情况取决于执行介恢复的 DBA 的信心程度。通过在上述所有情况的练习介恢复，你可以获得信心。这样，当你需要执行介恢复时，你的不确定性将显著减少。此类练习场景也将为你应对测试以及作为 DBA 会遇到的情况做好准备。

# 考点

理解介恢复。当数据库文件（如数据文件、控制文件或联机重做日志）不可用时，就需要介恢复。这些文件可能由于硬件故障、损坏或意外删除而变得不可用。

了解 ARCHIVELOG 模式和 NOARCHIVELOG 模式之间的恢复差异。为了执行完全恢复，数据库必须处于 ARCHIVELOG 模式。在 NOARCHIVELOG 模式下，必须执行不完全恢复——否则从上次备份到故障点之间的所有事务将丢失。

熟悉将数据文件恢复到不同位置的过程。要将数据文件恢复到不同位置，你必须使用操作系统命令将文件从备份位置复制到新位置。然后你将使用 `ALTER DATABASE RENAME FILE` 命令在控制文件中记录新的数据文件位置。

列出只读表空间恢复场景。三个只读恢复场景包括只读备份和只读恢复、只读备份和读写恢复，以及读写备份和只读恢复。你应该理解在这些场景中恢复方式有何不同。

理解执行 RMAN 备份和恢复所需的命令。`RESTORE` 命令将确定用于恢复的最佳可用备份集或镜像副本。`RECOVER` 命令将把来自联机重做日志、归档日志以及增量备份（如果使用）的必要更改应用到恢复的文件。

理解 ARCHIVELOG 和 NOARCHIVELOG 模式下的 RMAN 恢复。在 NOARCHIVELOG 模式下，你对一致性数据库使用 `RESTORE` 命令，但不使用 `RECOVER` 命令。在 ARCHIVELOG 模式下，`RESTORE` 和 `RECOVER` 命令均会被使用。

使用 RMAN 命令将数据文件恢复到不同位置。`SET NEWNAME` 命令用于指定数据文件的新位置，`SWITCH` 命令用于用新位置更新控制文件。之后，数据库将进行恢复。

使用 RMAN 命令使用归档日志重定位并恢复表空间。`SET NEWNAME` 命令用于指定数据文件的新位置，`SWITCH` 命令用于用新位置更新控制文件。注意，执行恢复前必须将表空间离线，并在恢复完成后在数据库保持打开的情况下将其置回联机状态。

## 关键术语

在考试之前，请确保你熟悉以下术语：

- ARCHIVELOG 模式
- 不完全恢复
- 冷备
- 介质恢复
- 完全恢复
- NOARCHIVELOG 模式
- 热备
- RECOVER DATABASE
- 镜像副本
- RESTORE

## 复习题

1. 哪些情况最能描述介质故障并需要恢复？（选择所有适用项）
A. 删除的文件
B. 删除的控制文件
C. 带有数据文件的磁盘
D. 存储数据文件的镜像阵列

2. 在何种模式下数据库必须执行到故障点的完全恢复？
A. NOARCHIVELOG
B. ARCHIVELOG
C. 导出
D. 日志

3. 在 ARCHIVELOG 模式下执行的是哪种类型的恢复？
A. 完全恢复
B. 部分恢复
C. 不完全恢复
D. 无恢复

4. 用户管理恢复需要哪种命令？
A. ALTER DATABASE RENAME
B. SETENAME
C. ALTER DATABASE NEWENAME
D. RENAME

5. 你对只读表空间进行了备份并将其变为读写。在下次备份之前，表空间已变为读写。你需要进行哪种操作？
A. 因为备份是只读的。
B. 因为变为只读后没有更改。
C. 因为表空间已变为读写。
D. 恢复只读表空间即可。

6. ARCH 模式需要哪种 RMAN 命令？
A. RESTORE
B. RECOVER
C. SET NEWENAME
D. SWITCH

7. 哪种 RMAN 命令负责应用增量备份和归档日志？
A. RESTORE
B. RECOVER
C. SET NEWENAME
D. SWITCH

8. 使用 RMAN 时，数据库需要处于什么模式才能执行备份恢复？
A. Opened
B. Nomount
C. Closed
D. Mount

9. 在数据库文件重定位过程中，`SWITCH` 命令负责哪些活动？
A. 重命名位置
B. 更新控制文件
C. 移动物理文件
D. 更新数据字典中的文件

10. 下列哪种恢复不需要你恢复数据库？
A. 只读表空间备份且恢复时是只读的
B. 只读表空间备份且恢复时是读写的
C. 读写表空间备份且恢复时是只读的
D. 读写表空间备份且恢复时是读写的

11. 哪些是只读表空间恢复场景？（选择所有适用项）
A. 只读备份到只读恢复
B. 只读备份到读写恢复
C. 读写备份到读写恢复
D. 读写备份到只读恢复

12. 如果按照建议程序操作，DBA 可以避免哪种只读恢复？
A. 只读备份到只读恢复
B. 只读备份到读写恢复
C. 读写备份到读写恢复
D. 读写备份到只读恢复

13. RMAN 映像复制（image copy）的独特之处在于？

- A. 它只能备份数据文件。
- B. 它只能备份到磁带。
- C. 它只能备份到磁盘。
- D. 它无法备份控制文件。

14. 关于备份集（backup set），以下哪项陈述是正确的？

- A. 它不存储在特殊的 RMAN 格式中。
- B. 它可以包含多个数据文件。
- C. 它可以包含多个数据文件和归档日志。
- D. 每个备份集只能包含一个数据文件。

15. 哪条 RMAN 命令负责从备份介质复制文件？

- A. RESTORE
- B. RENAME
- C. RECOVER
- D. SWITCH

## 复习题答案

1. E. 所有这些失败都需要进行介恢复。每次失败都会导致数据库文件不可用，这意味着需要进行还原。
2. B. 只有当数据库处于 ARCHIVELOG 模式时，才能执行到故障点之前的完全恢复。
3. A. 在 NOARCHIVELOG 模式下进行完全恢复是正确答案。尽管你正在执行完全恢复，但并不是所有的事务都被应用了，可能会丢失数据。这是因为数据库未处于 ARCHIVELOG 模式或没有生成日志。
4. A. `ALTER DATABASE RENAME FILE` 命令用于用户管理的备份。
5. C. 当只读表空间变为读写，且备份是在表空间为只读时采取的，就需要进行恢复。这意味着数据文件标头中的 SCN 已经更改，在恢复过程中需要与数据库的其他部分重新同步。
6. A. 当数据库处于 NOARCHIVELOG 模式时，`RESTORE` 命令负责恢复过程，因为不需要进行恢复。
7. B. `RECOVER` 命令将增量备份和归档日志应用到恢复过程中。
8. D. 数据库应挂载（mounted）以执行数据库还原和恢复，这样就可以读取控制文件并连接到目标数据库。
9. B. `SWITCH` 命令负责用移动文件的新位置更新控制文件。
10. A. 当表空间在备份期间是只读的，在恢复期间也是只读的，则不需要恢复。只读表空间的数据文件可以被还原，因为数据文件标头的 SCN 没有发生变化。
11. A, B, D. 只读表空间恢复的场景包括：只读到只读恢复、只读备份到读写恢复，以及读写备份到只读恢复。
12. D. 每当你将表空间设为只读时，应在之后立即进行备份。这消除了在“读写备份到只读恢复”场景下进行恢复的必要。
13. C. RMAN 映像复制类似于操作系统的复制。它只能在磁盘上执行。
14. B. 备份集可以在同一个备份集内包含多个数据文件，但不能在同一个备份集中同时包含数据文件和归档日志。与映像复制不同，备份集存储在特殊的 RMAN 格式中。
15. A. `RESTORE` 命令负责将文件从备份介质复制到目标位置。

# 用户管理和基于 RMAN 的不完全恢复

ORACLE9i: DBA 基础 II 本章涵盖的考试目标：

- 描述不完全恢复的步骤。
- 执行不完全数据库恢复。
- 识别当前重做日志文件的丢失。
- 使用 UNTIL TIME 执行不完全数据库恢复。
- 使用 UNTIL SEQUENCE 执行不完全数据库恢复。

> 考试目标可能会随时更改，恕不另行通知，并由 Oracle 酌情决定。请访问 Oracle 认证网站 (http://www.oracle.com/education/certification/) 获取最新的考试目标列表。

不完全数据库恢复需要理解重做日志（redo log）和 ARCHIVELOG 过程、Oracle 数据库的同步以及允许执行不完全恢复的选项。本章讨论了不完全恢复过程以及与每个不完全恢复选项相关的命令。还包含一个示例，展示了如何由于日志丢失或损坏执行不完全恢复。

除了用户管理的不完全恢复外，本章还演示了如何使用 RMAN 处理此过程。涵盖的 RMAN 示例介绍了如何使用 `SET UNTIL TIME` 和 `UNTIL SEQUENCE` 子句。

不完全恢复是某些类型故障的唯一恢复方法。了解何时以及如何使用不完全恢复方法非常重要。每当会导致你无法将所有更改应用回数据库的故障时，你都需要使用本章中讨论的不完全恢复方法之一。

# 描述用户管理的不完全恢复

不完全恢复发生在数据库没有完全恢复到数据库故障的时间点时。这是数据库的部分恢复，其中某些归档日志被应用到数据库，但并非全部。通过这种恢复，只有一部分事务被应用。

有三种类型的不完全介质恢复：
- 基于取消的 (Cancel-based)
- 基于时间的 (Time-based)
- 基于更改的 (Change-based)

(注：原文中后续部分存在大量重复段落，此处已按逻辑合并处理)

4. 将数据文件从备份位置恢复到正确的位置。
你通过发布操作系统命令来实现这一点。在 Unix 中，你将使用 `cp` 命令，例如所示：

```
cp /stage/data01.dbf /oracle/database/tst9/data01.dbf

cp /stage/system01.dbf /oracle/database/tst9/system01.dbf

cp /stage/rbs01.dbf /oracle/database/tst9/rbs01.dbf

cp /stage/temp01.dbf /oracle/database/tst9/temp01.dbf

cp /stage/users01.dbf /oracle/database/tst9/users01.dbf
```
