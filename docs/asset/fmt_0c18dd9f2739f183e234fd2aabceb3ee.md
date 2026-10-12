
`validation succeeded for datafile copy datafile filename=/staging/cold/tst9/data01.dbf recid=15 stamp=44249505`

# 在备份被删除时更新存储库

RMAN 可以将存储库（即恢复目录或控制文件）中的备份标记为已删除（`deleted`）状态。请记住，如果你使用恢复目录，备份信息将存储在目标数据库的控制文件中。RMAN 使用特殊的命令 `ALLOCATE CHANNEL FOR DELETE TYPE DISK` 来执行此维护活动。

1. 设计一个与存储介质（在本例中为磁带）协作工作的通道。

```bash
RMAN> allocate channel for delete type;
```

## 370 第 12 章 • RMAN 维护

2. 将备份集和控制文件标记为删除。

```bash
RMAN> change backupset 261 delete;
```

### 备份份 (Backup Pieces) 列表

| BP Key | BS Key | Pc# | Cp | 状态 | 设备类型 | 路径 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 262 | 261 | 1 | 1 | AVAILABLE | TAPE | /oracle/product/9.0.1/dbs/02d5p1 |

你确定要删除上述对象吗（输入 YES 或 NO？）YES
已删除备份份
backup piece handle=/oracle/product/9.0.1/dbs/02d5p88_1_1
recid=1 stamp=442289

3. 完成后，你必须释放该通道，以便 RMAN 内部其他作业可以使用。

```bash
RMAN> release channel;
```
已释放通道: ORA_MAINT_TAPE_1

```bash
RMAN>
```

# 修改备份和副本的可用状态

RMAN 可以将备份或副本标记为不可用（`unavailable`）或可用（`available`）。该功能主要用于指定备份，或者指定已移至异地或带回现场的副本。以下示例展示了如何将备份集设为不可用并再次恢复可用。要实现这一点，我们使用 `CHANGE`、`UNAVAILABLE` 和 `AVAILABLE` 命令。`CHANGE`、`UNAVAILABLE` 和 `AVAILABLE` 命令用于在恢复目录库（`recovery catalog`）中将备份集或副本标记为不可用或可用。与之前的示例一样，在执行这些命令之前，你必须连接到目标数据库和恢复目录库。

1. 执行 `CHANGE` 命令将备份集设为不可用。

```bash
RMAN> change backupset 283 unavailable
```

已更改备份份状态为不可用

backup piece handle=/oracle/product/9.0.1/dbs/03d5pe6s_1_1 recid=2 stamp=4422842

2. 执行 `CHANGE` 命令将备份集设为可用。

```bash
RMAN> change backupset 283 available;
```

已分配通道: ORA_DISK_1

channel ORA_DISK_1: sid=11 devtype=DISK

已更改备份份状态为可用

backup piece handle=/oracle/product/9.0.1/dbs/03d5pe6s_1_1 recid=2 stamp=4422842

```bash
RMAN>
```

下一个示例展示了如何将已编目录的复制文件设为不可用。操作方法与备份集相同，但我们将使用 `CHANGE DATAFILECOPY` 命令。

1. 首先，我们连接到 RMAN 并列出数据库中的所有副本。注意 S 列（状态列）的值为 A 表示可用。

```bash
oracle@octili:~> rman target / catalog rman/rmanrcat
```
Recovery Manager: Release 9.0.1.0.0 - Production版

(c) Copyright 2001 Oracle Corporation. 版权所有。

已连接到目标数据库: TST9 (DBID=1268700551)
已连接到恢复目录库数据库

```bash
RMAN> list copy of database;
```

### 数据文件副本列表

| Key | File | S | 完成时间 | CkpSCN | 备份时间 | 路径 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 502 | 6 | A | 06-OCT-01 | 67540 | 05-OCT-01 | staging/cold/tst9/data01.dbf |

2. 接下来，使用 `CHANGE DATCOPY` 命令更改数据文件使其变为不可用。

```bash
RMAN> change datafilecopy '/staging/cold/tst9/data01.dbf' unavailable;
```
已更改数据文件副本状态为不可用
datafile filename=/staging/cold/tst9/data01.dbf
recid=15 stamp=44249505

3. 使用 `LIST` 命令显示该副本不可用。在 S 列中可以看到状态（U 表示不可用）。

```bash
RMAN> list copy of database;
```

数据文件副本列表

| Key | File | S | 完成时间 | CkpSCN | 备份时间 | 路径 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 502 | 6 | U | 06-OCT-01 | 67540 | 05-OCT-01 | staging/cold/tst9/data01.dbf |

4. 现在可以使用以下命令将文件恢复为可用：

```bash
RMAN> change datafilecopy '/staging/cold/tst9/data01.dbf' available;
```

已分配通道: ORA_DISK_1

channel ORA_DISK_1: sid=11 devtype=DISK

已更改数据文件副本状态为可用

datafile filename=/staging/cold/tst9/data01.dbf

recid=15 stamp=44249505

5. 现在再次验证文件是可用的。注意 S 列的值为 A。

```bash
RMAN> list copy of database;
```
| Key | File | S | 完成时间 | CkpSCN | 备份时间 | 路径 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 502 | 6 | A | 06-OCT-01 | 67540 | 05-OCT-01 | staging/cold/tst9/data01.dbf |

# 使备份或副本免受保留策略

要使备份或副本免受保留策略，必须执行特定的 RMAN 命令。这些命令涉及使用下述配置参数。这些设置默认对所有 RMAN 连接生效。

1. 首先，你必须了解当前的 RMAN 配置设置。你可以通过执行 `ALL` 命令来实现。

```bash
RMAN> show all;
```
