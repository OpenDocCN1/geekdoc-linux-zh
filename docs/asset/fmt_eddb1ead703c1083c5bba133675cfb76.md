
- 如果他们拥有某个表的 `INSERT` 权限，他们可以使用 `LOAD` 命令或 `AutoLoader` 工具将数据加载到表中。
- 如果他们拥有某个表的 `INSERT` 权限，且之前的加载操作是插入数据的加载，则可以使用 `LOAD RESTART` 或 `LOAD TERMINATE`。
- 如果之前的加载操作是 `LOAD REPLACE`，则在用户执行 `LOAD RESTART` 或 `LOAD TERMINATE` 之前，必须也授予该用户 `DELETE` 权限。
- 如果使用异常表作为 `LOAD` 的一部分，用户必须对异常表拥有 `INSERT` 权限。
- 拥有 `LOAD` 权限的用户可以执行 `QUIESCE TABLESPACES FOR TABLE`、`RUNSTATS` 和 `LIST TABLESPACES` 命令。

![](img/ca7cfad01341360e684d5dd2379b19e9_178_0.png)

## DBADM 权限

在数据库级别，存在 `DBADM` 权限。`DBADM` 可以执行任何管理任务，例如加载数据、在数据库内创建对象以及监控数据库活动。`DBADM` 对数据库拥有完全权限，可以查询、删除或创建任何表，并为数据库内的用户设置权限。数据库创建者将自动获得新数据库的 `DBADM` 权限。`SYSADM` 用户可以通过 `GRANT` 语句向其他用户授予 `DBADM` 权限。可以持有多个数据库的 `DBADM` 权限。

# 第 4 章 控制数据访问

表 4–3 显示了各种 DB2 权限级别的一些有效任务。`DBADM` 列中与 `LOAD` 权限相关的条目带有 `*` 号。

## 表 4–3 数据库权限与有效任务

| 功能 | SYSADM | SYSCTRL | SYSINT | DBADM |
| :--- | :--- | :--- | :--- | :--- |
| UPDATE DBM CFG | YES | | | |
| GRANT/REVOKE DBADM | YES | | | |
| ESTABLISH/CHANGE SYSCTRL | YES | | | |
| ESTABLISH/CHANGE SYSMAINT | YES | | | |
| FORCE USERS | YES | YES | | |
| CREATE/DROP DATABASE | YES | YES | | |
| RESTORE TO NEW DATABASE | YES | YES | | |
| UPDATE DB CFG | YES | YES | YES | |
| BACKUP DATABASE/TABLE SPACE | YES | YES | YES | |
| RESTORE TO EXISTING DATABASE | YES | YES | | |
| START AND STOP DB2 INSTANCE | YES | YES | | |
| RESTORE TABLE SPACES | YES | YES | | |
| RUN THE DATABASE MONITOR | YES | | | |
| START AND STOP TRACES | YES | | | |
| QUERY THE STATE OF A TABLE SPACE | YES | | | |
| UPDATE LOG HISTORY FILES | YES | | | |
| QUIESCE A TABLE SPACE | YES | | | |
| REORGANIZE A TABLE | YES | | | |
| EXECUTE THE RUNSTATS UTILITY | YES | | | |

## 安全 155

(注：OCR 文本 "Security 155" 似乎是原始文档的页眉/页脚，根据指令将其在此处保留所有信息。)

*(注：上述表格是根据源文本中表 4-3 的碎片化数据重建的，该表跨跨了第 178 页和 179 页。）*

![](img/ca7cfad01341360e684d5dd2379b19e9_182_0.png)

图 4–8 授权与权限层次结构

## 数据库权限

数据库权限涉及对整个数据库的操作，只有具有 `SYSADM` 或 `DBADM` 权限的用户才能向其他用户授予或撤销这些权限：

# 第 4 章 控制数据访问

- `CONNECT` 允许用户访问数据库
- `BINDALL` 允许用户在数据库中创建新的包（packages）
- `CREATAB` 允许用户在数据库中创建新表
- `CREATE_NOT_FENCED` 允许用户创建“非围栏”（not fenced）的用户定义函数 (`UDF`) 或过程。“非围栏”的 `UDF` 或过程必须经过极其严格的测试，因为数据库管理器不会保护这些 `UDF` 或过程保护其存储或控制块。因此，一个编写不当且测试不充分并允许以“非围栏”运行的 `UDF` 或过程可能会给您的系统带来严重问题！
- `IMPLICIT_SCHEMA` 允许任何用户通过使用带有不存在的模式名称的 `CREATE` 语句创建对象来隐式创建模式。`SYSIBM` 成为隐式创建模式的所有者，`PUBLIC` 被授予在该模式下创建对象的权限。
- `LOAD` 允许用户将数据加载到表中
- `QUIESCE_CONNECT` 允许用户在数据库静态（quiesced）时访问数据库
- `CREATE_EXTERNAL_ROUTINE` 允许用户创建供应用程序及数据库其他用户使用的过程

1. `QUIESCE_CONNECT` 和 `CREATE_EXTERNAL_ROUTINE` 选项是 DB2 8.1 版本的新功能。`QUIESCE_CONNECT` 赋予用户连接到静止状态数据库的能力。可以将数据库置于静止状态以便独立维护，或允许单个用户或用户组对数据库进行独占使用。
2. `CREATE_EXTERNAL_ROUTINE` 权限允许用户创建在数据库地址空间内运行的 `UDF`。在此模式下运行 `UDF` 可以由于数据库与例程序之间调用开销的减少而获得更快的性能。然而，在开发此类 `UDF` 时必须非常小心，因为任何错误的内存分配都可能影响数据库的操作。

## 注意：

## 数据库对象权限

对于每个 DB2 对象，创建它时需要特定的权限或权利，而控制它则需要特定的权限或权利。以下列表描述了数据库中各种对象的权限。

- 数据库权限 - 这些包括创建和访问数据库的能力。

![](img/ca7cfad01341360e684d5dd2379b19e9_183_0.png)

## 安全 161

任何数据库的创建者都会自动获得 `DBADM` 权限。`DBADM` 可以针对数据库执行任何 SQL 语句。`DBADM` 可以授予连接权限、在数据库中创建表或新包的权限、隐式创建模式的权限，以及创建非围栏存储过程或用户定义函数的权限。

`IMPLICIT_SCHEMA` 权限允许用户在不指定模式名称的情况下创建对象。该对象将被分配一个用户授权 ID 的模式。此隐式创建的模式由 `SYSBM` 所有。`PUBLIC` 组（任何可以连接到数据库的用户）被授予在该模式下创建对象的权限。

> 注意：当创建数据库时，某些权限会自动授予 `PUBLIC` 组。如果您想控制谁可以在数据库上执行什么操作，必须由 `DBADM` 或 `SYSADM` 用户从 `PUBLIC` 中撤销这些权限（这些包括 `CREATAB` 和 `BINDADD`）。

![](img/ca7cfad01341360e684d5dd2379b19e9_184_0.png)

- **模式权限** - 这些包括在模式内创建、修改或删除对象的权限。模式所有者拥有所有这些权限以及将其授予他人的能力。属于模式的对象包括表、视图、索引、包、用户定义数据类型、用户定义函数、触发器、存储过程和别名。
- **表权限** - 表或视图的 `CONTROL` 权限只能由具有 `SYSADM` 或 `DBADM` 权限的用户授予。（然而，表的创建者隐式地获得该表的 `CONTROL` 权限。）对表拥有 `CONTROL` 权限允许您添加列、创建主键、检索、更新或插入行、创建索引、创建引用约束、向他人授予权限、使用 `EXPORT` 工具并执行维护（如重组表或更新表统计信息）。

列的 `UPDATE` 权限允许用户仅修改表或视图的指定列。类似地，列的 `REFERENCE` 权限允许仅在指定的列上创建外键。
- **视图权限** - 要要创建视图，您必须能够执行 SQL `SELECT` 语句，或对所引用的每个视图或表拥有 `CONTROL` 权限。您需要拥有视图的 `CONTROL` 权限才能授予该视图的删除、插入和更新权限，除非该视图被定义为只读视图。所需的权限必须由用户显式持有或授予 `PUBLIC`。（或者，对每个额外权限持有 `WITH GRANT OPTION` 也足够了）。

![](img/ca7cfad01341360e684d5dd2379b19e9_184_0.png)

# 第 4 章 控制数据访问

- **索引权限** - 索引的创建者自动获得该索引的 `CONTROL` 权限。这允许创建者删除索引。授予索引 `CONTROL` 权限只能由具有 `SYSADM` 或 `DBADM` 权限的用户执行。
