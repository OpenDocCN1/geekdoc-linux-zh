
```
RMAN 配置参数如下：
CONFIGURE RETENTION POLICY TO REDUNDANCY 1; # 默认
CONFIGURE BACKUP OPTIMIZATION OFF; # 默认
CONFIGURE DEFAULT DEVICE TYPE TO DISK; # 默认
CONFIGURE CONTROLFILE AUTBACKUP OFF; # 默认
CONFIGURE CONTROLFILE AUTBACKUP FORMAT FOR DEVICE DISK TO '%F'; # 默认
CONFIGURE DEVICE TYPE DISK PARALLELISM 1; # 默认
CONFIGURE DATAFILE BACKUP COPIES FOR DEVICE DISK TO 1; # 默认
CONFIGURE ARCHLOG BACKUP COPIES FOR DEVICE DISK TO 1; # 默认
CONFIGURE MAXSIZE TO UNLIMITED; # 默认
CONFIGURE SNAPSHOT CONTROLFILE NAME TO '/oracle/product/9.0.1/dbs/spf_tst9.cfg'
```

- 2. 接下来，你应该将保留策略设置为天数。在示例中，我们将保留期任意设置为 10 天。在现实生活中，该值应由 IT 管理层确定。此设置的结果是恢复目录库仅保留 10 天的备份。要设置保留策略，使用 `CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF N days` 设置。

```
RMAN> CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 10 DAYS;
```

```
新的 RMAN 配置参数：
CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 10 DAYS;
新的 RMAN 配置参数已存储
开始同步恢复目录库
完全同步完成
```

- 3. 接下来，你应该使用 `KEEP` 命令创建备份。`KEEP` 命令可以使用定义的时间段或永久保留。在示例中，我们将使用设定的日期或时间 `01-DEC-02`。这意味着即使保留策略为 10 天，在到达该日期之前，数据库和日志也不会过期。

```
RMAN> run
2> allocate channel c1 type disk;
3> backup database keep until time '01-DEC-02' logs;
4> backup (archivelog all);
5> release channel c1;
6> )
```

# 第 12 章 • RMAN 维护

```
input archive log thread=1 sequence=1 recid=8
stamp=442361669
```

```
input archive log thread=1 sequence=2 recid=9
stamp=442361872
```

```
input archive log thread=1 sequence=3 recid=10
stamp=442362056
```

```
input archive log thread=1 sequence=4 recid=11
stamp=442362297
```

```
input archive log thread=1 sequence=5 recid=12
stamp=442362415
```

```
input archive log thread=1 sequence=6 recid=13
stamp=442792220
```

```
channel c1: starting piece 1 at 10-OCT-02
channel c1: finished piece 1 at 10-OCT-02
```

```
piece handle=/oracle/product/9.0.1/dbs/id68u8_1_1
comment=NONE
channel c1: backup set complete, elapsed time: 00:00:01
Finished backup at 10-OCT-02
```

```
RMAN>
```

## 现实场景

### 磁带上的多种备份类型

您的磁带设备可以支持多种备份，其中可能包括基于 RMAN 的备份和普通文件系统备份。大多数自动磁带库（ATL）及其相关软件都支持文件系统备份以及 RMAN 备份。这意味着您可以在磁带上拥有每种类型的备份，特别是因为数字线性磁带（DLT）支持大容量存储——每张磁带 40–200 兆字节——这意味着文件系统备份和 RMAN 备份可以交错存储单条磁带上。

# 使用操作系统命令创建的目录备份

您应该意识到这种可能性。首先，确保您的组织能够满足文件系统备份和 RMAN 备份所需的最长时间保留的要求。例如，文件系统备份只需要一周时间——直到下周进行下一次文件系统备份。但某些 RMAN 备份可能需要长达一个月以满足业务需求。因此，在这种情况下，您应该将所有磁带保存一个月。

# 使用操作系统命令创建的目录备份

RMAN 可以在目录中分类或存储有关基于系统的备份的信息。在传统备份中，您将使用 `ALTER TABLESPACE BEGIN BACKUP` 命令来实现此。然后您将在 Unix 中执行 `cp` 命令将文件复制到磁盘上的另一个位置。该新位置会在 RMAN 中进行分类。分类意味着恢复目录中的信息被存储了。以下是对 `data01.dbf` 文件的分类示例。对任何数据库都可以执行此操作，类似于对于用户管理的备份。

- 1. 将 `data01.dbf` 数据文件复制到备份位置。

  `oracle@octilli:~ cp /db01/ORACLE/tst9/data01.dbf /staging/data01.dbf`

- 2. 连接到目标数据库和恢复目录。

  `oracle@octilli:~ rman target / catalog rman/rman@rcat`

- 3. 通过执行 `CATALOG DATAFILECOPY` 命令将数据文件存储在恢复目录中。

```
RMAN> catalog datafilecopy '/staging/cold/tst9/data01.dbf;
```

cataloged datafile copy

datafile filename=/staging/cold/tst9/data01.dbf

recid=15 stamp=44242905

RMAN>:

现在您已经已经在 RMAN 仓库中分类了该文件，可以使用 `LIST` 命令的变体来查询仓库。此 `LIST` 命令将查看目标数据库的所有已分类信息。

```
RMAN> list copy of database;
```

# 数据文件副本列表

| Key | File S Completion CkpSCN Ckp Time Name |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 502 | 6 | A | 06-OCT-01 | 67540 | |

## 总结

在本章中，我们讨论了 RMAN 维护的各个方面。我们学习了如何将基于系统的备份分类到 RMAN 仓库中。我们还探索了如何管理已分类的信息。最后，我们讨论了维护健康的恢复目录的重要性。

### 13. 在 RMAN 中，以下哪个命令将把保留策略设定为 7 天？

- A. `CONFIGURE RETENTION POLICY TO RECOVERY PERIOD OF 7 DAYS;`
- B. `CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 7 DAYS;`
- C. `CONFIGURE RETENTION POLICY TO RECOVERY TIME OF 7 DAYS;`
- D. `CONFIGURE RETENTION POLICY TO RECOVERY TIMEFRAME OF 7 DAYS;`

### 14. 下面哪个命令将显示保留策略？

- A. `show retention plan`
- B. `display all`
- C. `show all`
- D. `display retention plan`

### 15. 下面哪个命令可以允许你识别数据文件副本的可用性性变化？

- A. `LIST COPY OF DATABASE AVAILABILITY`
- B. `LIST COPY OF DATABASE`
- C. `LIST COPY OF AVAILABILITY`
- D. `LIST BACKUP OF AVAILBILITY`

## 复习题答案

- 1. `CROSSCHECK` 命令需要使用恢复目录。这是必须与恢复目录进行检查的备份信息，以便与存储实际备份的磁带或磁盘介质进行比较。

- 2. 为 `CROSSCHECK` 命令分配的通道是仅用于维护的特殊通道。`c1` 和 `t1` 仅仅是通道设备的名称。
