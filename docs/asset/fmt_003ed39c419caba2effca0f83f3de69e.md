
validation succeeded for datafile datafile copy filename=`staging/cold/tst9/data01.dbf` recid-15 stamp=442429505

RMAN>

# 在备份被删除后更新存储库

RMAN 可以将存储库（无论是恢复目录库还是控制文件）中的备份标记为已删除（deleted）。请记住，如果不使用恢复目录库，备份信息将存储在目标数据库的控制文件中。以这种方式标记的备份在查询恢复目录库时不会出现在输出列表中。RMAN 使用特殊的命令 `ALLOCATE CHANNEL FOR DELETE TYPE DISK` 来执行此维护活动。我们将在这些示例中使用 `CHANGE` 命令和 `DELETE` 命令。

此示例显示了删除部分备份集和控制文件的过程：

1. 指定一个通道与存储介质工作——在本示例中为磁带。

```
RMAN> allocate channel for delete type tape;
```

```
allocated channel: ORA_MAINT_TAPE_1
channel ORA_MAINT_TAPE_1: sid=12 devtype=DISK
```

# 第 12 章 · RMAN 维护

2. 标记备份集和控制文件：

```
RMAN> change backupet 261 delete;
```

# 备份碎片列表

| BP Key | Key | Type | Name |
| --- | --- | --- | --- |
| 261 | 1 | AVAILABLE | oracle/product/9.0.1/dbs/03d5pe6s_1_1 |

3. 完成后，释放通道。

```
RMAN> release channel;
```

```
allocated channel: ORA_MAINT_TAPE_1
channel ORA_MAINT_TAPE_1: sid=12 devtype=DISK
```

```
CONFIGURE DATAFILE BACKUP COPIES FOR DEVICE TYPE DISK
TO 1; # default

CONFIGURE ARCHIVE BACKUP COPIES FOR DEVICE TYPE DISK
TO 1; # default

CONFIGURE MAXSIZE TO UNLIMITED; # default

CONFIGURE SNAPSHOT CONTROLFILE NAME TO '/oracle/product/9.0.1/dbs/snapcf_tst_9.ft'
```

RMAN>

2. 接下来，您应该将保留策略设置为天数。在本示例中，我们将任意将保留策略设置为 10 天。在现实生活中，此值将由 IT 管理层达成一致，意味着恢复目录将仅保留 10 天的备份。要设置保留策略，您将使用 `CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF N DAYS` 配置设置。

```
RMAN> CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 0 DAYS;
```

```
新的 RMAN 配置参数已更新：

CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 10 DAYS;

new RMAN configuration parameters are successfully stored

starting full resync of recovery catalog
full resync complete
```

3. 接下来，您应该使用 `KEEP` 命令创建备份。`KEEP` 命令定义了一个特定的时间段或永久保留。在本示例中，我们将使用指定的日期或时间 `01-DEC-02`。这意味着即使保留策略仅设置为 10 天，数据库和日志在到达该日期之前也不会过期。

```
RMAN> run {
2> allocate channel c1 type disk;
3> backup database keep until '01-DEC-02' logs;
4> backup (archivelog all);
5> release channel c1;
6> }
```

# 使备份或拷贝免受保留策略限制 375

```
分配通道: c1
channel c1: sid=9 devtype=DISK

正在于 10-OCT-02 开始备份
备份将于 01-DEC-02 过期
从此备份恢复所需的归档日志
expire when this backups 在此备份时过期

channel c1: starting full datafile backupset
channel c1: specifying datafile(s) in backupset
including current controlfile in backupset
input datafile fno=00001 name=/db01/oracle/tst9/system01.dbf
input datafile fno=00006 name=/db01/oracle/tst9/data01.dbf
input datafile fno=00002 name=/db01/oracle/tst9/rbs01.dbf
input datafile fno=00003 name=/db01/oracle/tst9/temp01.dbf
input datafile fno=00004 name=/db01/oracle/tst9/users01.dbf
input datafile fno=00007 name=/db01/oracle/tst9/idx01.dbf
input datafile fno=00005 name=/db01/oracle/tst9/tools01.dbf
channel c1: starting piece 1 at 10-OCT-02
channel c1: finished piece 1 at 10-OCT-02
piece handle=/oracle/product/9.0.1/dbs/0hd68u54_1_1
comment=NONE
channel c1: backup set complete, elapsed time: 00:01:58
Finished backup at 10-OCT-02

正在于 10-OCT-01 开始备份
current log archived
channel c1: starting archive log backupset
channel c1: specifying archive log(s) in backup set
```

# 第 12 章 • RMAN 维护

```
input archive log thread=1 sequence=1 recid=8
stamp=442361669
input archive log thread=1 sequence=2 recid=9
stamp=442361872
input archive log thread=1 sequence=3 recid=10
stamp=442362056
input archive log thread=1 sequence=4 recid=11
stamp=442362297
input archive log thread=1 sequence=5 recid=12
stamp=442362415
input archive log thread=1 sequence=6 recid=13
stamp=442792220
channel c1: starting piece 1 at 10-OCT-02
channel c1: finished piece 1 at 10-OCT-02
piece handle=/oracle/product/9.0.1/dbs/0id68u8u_1_
comment=NONE
channel c1: backup set complete, elapsed time: 00:00:01
Finished backup at 10-OCT-02
```

released channel: c1

RMAN>

您的磁带备份设备可能支持多个备份，其中包含基于 RMAN 的备份和普通文件系统备份。大多数自动磁带库 (ATL) 及其相关软件都支持文件系统备份以及 RMAN 备份。这意味着可以将每种备份都放在磁带上，特别是因为数字磁带 (DLT) 将支持巨大的存储容量——

## 复习题

1. RMAN `CROSSCHECK` 命令需要使用以下哪项？

   A. 恢复目录库 (Recovery catalog)

   B. 仅需 RMAN 存储库

   C. 标准通道分配

   D. 用于恢复的分配通道

2. 为 `CROSSCHECK` 命令分配的是什么类型的通道？

   A. c1

   B. t1

   C. MAINTENANCE（维护）

   D. 仅限 sbt_tape

3. `CROSSCHECK` 命令只能对什么种类型的备份执行？（选择所有适用项）。

   A. 仅限备份分片 (Backup pieces)

   B. 备份集 (Backup sets)

   C. 副本 (Copies)

   D. 仅限备份集

4. 使用哪个命令从恢复目录库中删除备份集和副本？

   A. REMOVE

   B. UNAVAILBLE

   C. DELETE

   D. MARK UNUSUABLE（标记为不可用）

5. 使用 `DELETE` 命令需要什么类型的通道？

   A. DELETE

   B. c1

   C. MAINTENANCE

   D. t1

6. `CHANGE AVAILABILITY` 命令可以用于什么种类型的备份？（选择所有适用项。）

   A. 副本

   B. 用户管理备份

   C. 备份集

   D. 目录化备份 (Cataloged backups)

7. 不可用备份的状态是什么？

   A. Unavailable（不可用）

   B. Deleted（已删除）

   C. U

   D. UA

8. RMAN 保留策略被称为什么？

   A. Command（命令）

   B. Report（报告）

   C. List（列表）

   D. CONFIGURATION 参数（配置参数）

9. 什么命令可以跳过保留策略？

   A. EXTEND

   B. KEEP

   C. EXEMPT

   D. UNLIMITED

10. 在 RMAN 存储库中记录非 RMAN 备份的术语是什么？

    A. OS 文件副本

    B. 备份集

    C. 备份分片

    D. 目录化备份

11. 当备份集被设置为不可用时，必须使用哪些命令？

    A. `CHANGE` 和 `UNAVAILABLE`

    B. `SET` 和 `UNAVAILABLE`

    C. `MAKE` 和 `UNAVAILABLE`

    D. `CHANGE` 和 `REMOVE`

12. 为了从磁盘上删除备份，你必须执行以下哪个命令？

    A. `ALLOCATE CHANNEL FOR REMOVE TYPE DISK`

    B. `ALLOCATE CHANNEL FOR DELETE TYPE DISK`

    C. `ALLOCATE CHANNEL FOR UNAVAILABLE TYPE DISK`

    D. `ALLOCATE CHANNEL TO DELETE TYPE DISK`

13. 以下哪个命令将在 RMAN 中设置 7 天的保留策略？

    A. `CONFIGURE RETENTION POLICY TO RECOVERY PERIOD OF 7 DAYS;`

    B. `CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 7 DAYS;`

    C. `CONFIGURE RETENTION POLICY TO RECOVERY TIME OF 7 DAYS;`

    D. `CONFIGURE RETENTION POLICY TO RECOVERY TIMFRAME OF 7 DAYS;`

14. 下面哪个命令将显示保留策略？

    A. `show retention plan`

    B. `display all`

    C. `show all`

    D. `display retention plan`

15. 下面哪个命令将允许你识别数据文件副本的可用性是否发生了变化？

    A. `LIST COPY OF DATABASE AVAILABILITY`

    B. `LIST COPY OF DATABASE`

    C. `LIST COPY OF AVAILABILITY`

    D. `LIST BACKUP OF AVAILBILITY`

## 复习题答案

1. **A.** `CROSSCHECK` 命令需要使用恢复目录库。这是必须通过恢复目录库检查的备份信息，以便与存储实际备份的磁带或磁盘介进行比较。

2. **C.** 为 `CROSSCHECK` 命令分配的通道是仅用于维护的特殊通道。`c1` 和 `t1` 仅仅是通道设备的名称。

3. **B, C.** `CROSSCHECK` 命令可以同时执行备份集和副本。

4. **C.** `DELETE` 命令从目录中删除备份集和副本。

5. **C.** 使用 `DELETE` 命令时，需要分配用于维护的通道。`c1` 和 `t1` 是通道设备的名称。

6. **A, C, D.** `CHANGE AVAILABILITY` 命令可以用于备份集、副本以及作为文件副本的目录化备份。

7. **C.** 不可用（unavailable）状态在 `list` 命令的输出中显示为 `U`。

8. **D.** 保留策略是一个被称为 `CONFIGURATION` 参数的参数。还有许多其他配置参数。

9. **B.** RMAN `KEEP` 命令导致备份跳过或持续超过保留策略。

10. **D.** 目录化备份是为 OS 或用户管理的备份进行备份的文件。

11. **A.** 将备份集设为不可用的命令是 `CHANGE BACKUPSET <upset_number> UNAVAILABLE`。

12. **B.** `ALLOCATE CHANNEL FOR DELETE TYPE DISK` 命令会在你可以在 RMAN 内删除备份之前分配所有必要的资源。

13. **B.** 正确的命令是 `CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 7 DAYS`。其他选项是配置参数的无效语法。

14. **C.** `show all` 命令将显示 RMAN 中所有的配置参数。这些其中一个配置参数就是保留策略。

15. **B.** `LIST COPY OF DATABASE` 命令将显示状态。

## 恢复目录库的创建与维护

本章涵盖的 ORACLE FUNDAMENTALS II 目标：

- 描述目录的内容。
- 创建恢复目录库。
- 使用 RMAN 维护恢复目录库。
- 使用 RMAN 注册、同步和重置数据库。
- 查询恢复目录库以生成报告。
- 创建、存储和脚本。
- 描述备份和恢复的方法。

考试目标可能会随时更改。

请访问 Oracle 认证网站获取最新信息。

本章讨论了与 RMAN 和恢复目录库相关的实际和概念主题。你将学习使用恢复目录库的原因和考虑因素，并探索构成它的组件。本章重点关注目录库的实际方面，例如安装和配置。你将使用本章介绍的 RMAN 命令来管理和维护恢复目录库，并处理脚本来完成活动。本章涵盖的主题在测试和现实场景中都是需要的。恢复目录库是一个关键组件，并允许完整的功能。理解如何存储和利用这些信息非常重要。

## 使用恢复目录库的考虑因素

使用恢复目录库的决定是在使用 RMAN 时所做的最重要的决策之一。与使用目标数据库的控制文件作为 RMAN 存储库相比，恢复目录库提供了更多的备份和恢复功能。因此，我们建议尽可能使用恢复目录库。

使用恢复目录库的主要考虑因素如下：

- 除非存在恢复目录库，否则某些功能不支持。
- 你应该创建一个独立的目录数据库。
- 你必须像管理其他数据库一样管理目录数据库，包括数据增长和存储的数据库对象（如脚本）。
- 你必须备份目录数据库。
- 你必须决定是否将每个目标数据库保留在独立的恢复目录库中。

除非维护和创建目录数据库的过程消耗了站点多的资源，否则 Oracle 建议使用恢复目录库。任何拥有经验且合格的 DBA 和系统管理员的站点都能够维护和创建目录数据库。然而，如果数据库较小且不重要，不使用恢复目录库使用 RMAN 是可以接受的，并且在之前的 Oracle 版本中有所改进。

图 13.1 显示了恢复目录库与整个 RMAN 备份过程的关联。

# 图 13.1 与恢复目录交互的 RMAN 实用程序

![](img/a183fd041839741f5ab6df3caffc6b52_451_0.png)

## 恢复目录的组件

RMAN 恢复目录的主要组件用于支持在目录中记录备份和恢复信息。这些信息存储在 Oracle 数据库的表、视图和其他数据库对象中。备份经过了压缩处理以实现优化存储。以下是恢复目录中包含的组件列表：

- 为目标数据库记录的、供长期使用的备份和恢复信息
- 可以存储和重用的 RMAN 脚本
- 关于数据文件和归档日志的备份信息
- 关于目标数据库物理结构（或模式，schema）的信息

## 创建恢复目录

如前所述，恢复目录是 RMAN 的一个可选功能。该目录与标准数据库目录相似，因为它存储了关于恢复过程的信息，正就像数据库目录存储关于数据库的信息一样。

RMAN 可以在不使用目录的情况下运行。由于原因，恢复目录必须存储在自己的数据库中，最好存储在与目标数据库不同的服务器上。要启用目录，必须创建一个具有 `CONNECT`、`RESOURCE` 和 `RECOVERY_CATALOG_OWNER` 权限的账户来存放目录表。完成后，必须以连接到 RMAN 实用程序的数据库用户身份执行目录创建脚本。

让我们介绍创建恢复目录的步骤。此示例假设你已经建立了一个名为 `rcat` 的数据库，并计划在其中存储恢复目录。

1. 首先，你必须选择恢复目录将所在的数据库。这并不是目标数据库。在这种情况下，此 RMAN 数据库被称为 `rcat`。在这种情况下，你将使用 `oraenv` 脚本（由 Oracle 提供）切换到同一服务器上的其他数据库。
