
### 3. 将批处理作业分配到回滚段

接下来，使用 `SQL` 命令 `SET TRANSACTION` 或 `DBMS_TRANSACTION` 存储过程将批处理作业分配到此回滚段：

```sql
SQL> SET TRANSACTION USE ROLLBACK SEGMENT rbsbatch;
```

或

```sql
SQL> EXECUTE DBMS_TRANSACTION.USE_ROLLBACK_SEGMENT('rbsbatch');
```

### 4. 启动批处理作业

现在，启动批处理作业：

```sql
SQL> EXECUTE posting_job;
```

### 5. 将大型回滚段设为离线

接下来，从执行批处理作业以外的数据库会话中，立即将大型回滚段设置为离线：

```sql
SQL> ALTER ROLLBACK SEGMENT rbsbatch OFFLINE;
```

回滚段不会立即离线，直到批处理事务完成。然而，由于已在数据字典中标记为离线，其他事务不会被分配给它。手动将事务分配给其专用的回滚段有助于确保事务能找到足够的撤销空间来存储事务的前像。

**警告** 批处理作业中发生的任何提交操作都会导致大型回滚段离线并不可用。因此，在每次提交后，你必须将回滚段重新设为在线，并重新发出 `SET TRANSACTION` 或 `DBMS_TRANSACTION` 命令，以防止批处理作业使用其他回滚段。

#### 通过最小化回滚段活动来提升性能

另一种解决与回滚段相关的性能问题的方法是尽量最小化写入回滚段的条目数量和大小。这可以通过频繁提交来减少大型回滚条目、在执行数据库导入时使用 `COMMIT=Y` 选项、在使用数据库 `EXPORT` 实用程序时避免使用 `CONSISTENT` 选项，以及在使用 `SQL*Loader` 实用程序时设置适当的 `COMMIT` 值来实现。

**注意** 有关 `EXPORT`、`IMPORT` 和 `SQL*Loader` 实用程序选项的更多信息，请参阅《Oracle9i Database Utilities, Release 1 (9.0.1) (Part Number A90192-01)》。

#### 使用自动撤销管理功能来提升性能

`Oracle9i` 提供了一项新功能：自动撤销管理（`AUM`），它减轻了前几节中描述的许多手动回滚段撤销（`RBU`）管理的负担。

自动撤销管理（也称为系统管理的撤销）旨在通过动态管理撤销段的大小和数量来最小化撤销段的性能问题。此概念类似于临时表空间中排序段的动态管理。在 `AUM` 中，创建专用的表空间（称为撤销表空间）来存储前像数据。`Oracle` 根据系统需求自动管理这些撤销段的数量和大小。以下各节介绍了使用此新功能改善撤销段 I/O 的技巧。

**Oracle 目标**

解释自动撤销管理的概念

##### 配置自动撤销管理

为了在数据库中使用 `AUM`，你必须首先将四个 `init.ora` 参数设置为适当的值。这些参数的说明如下：

- **`UNDO_MANAGEMENT`** 用于指示数据库中使用的是自动（`AUTO`）还是手动（`MANUAL`）撤销管理。默认值为 `MANUAL`。

- **`UNDO_TABLESPACE`** 指定存储 `AUM` 撤销段的表空间名称。默认值是数据库启动时找到的第一个撤销表空间。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_488_0.png)

如果不存在撤销表空间，`SYSTEM` 回滚段将被用于存储撤销数据。

- **`UNDO_RETENTION`** 指定（以秒为单位）在生成撤销信息的事务提交后保留撤销信息的时间。默认值为 `900` 秒。此参数旨在帮助减少因事务需要已被覆盖的前像数据用于读一致性而导致的 *Snapshot Too Old* 错误。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_488_1.png)

只有当撤销表空间已分配了足够的空间时，撤销数据才能保留到 `UNDO_RETENTION` 指定的时间。

- **`UNDO_SUPPRESS_ERRORS`** 用于抑制在 `AUM` 模式下使用在 `RBU` 模式下有效的命令（例如 `SET TRANSACTION USE ROLLBACK SEGMENT ...`）时本应发生的错误。

配置这些参数后，你接下来必须创建一个撤销表空间来存储系统管理的撤销段。

**Oracle 目标**

创建和维护自动管理的撤销表空间

##### 创建撤销表空间

一旦将 `UNDO_MANAGEMENT` `init.ora` 参数设置为 `AUTO`，你就必须创建一个表空间来存储系统管理的撤销段。创建 `AUM` 表空间的语法如下所示：

```sql
SQL> CREATE UNDO TABLESPACE undo
2  DATAFILE 'd:\oradata\PROD\undo01.dbf' SIZE 500M
3  AUTOEXTEND ON
4  NEXT 5M MAXSIZE 2000M;
```

一旦使用上述语法创建了 `UNDO` 表空间，必须在 `init.ora` 中添加参数 `UNDO_TABLESPACE=UNDO`，并重启实例，新的表空间才会被用于 `AUM`。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_489_0.png)

你无法为 `UNDO` 表空间指定默认的初始和下次扩展大小。这些值将由系统生成。

撤销表空间也可以在数据库创建时的 `CREATE DATABASE` 语句中定义。图 8.34 展示了该语法的示例。

**图 8.34** 在数据库创建时指定的撤销表空间

```sql
SQL> CREATE DATABASE PROD
2  MAXDATAFILES 500
3  MAXLOGMEMBERS 4
4  DATAFILE 'D:\oradata\PROD\system01.dbf' SIZE 250M
5  UNDO TABLESPACE rbs DATAFILE 'F:\oradata\PROD\rbs01.dbf' SIZE 500M
6  LOGFILE GROUP 1 ('d:\oradata\PROD\log1a.rdo','e:\oradata\PROD\log1b.rdo') SIZE 5M,
7  GROUP 2 ('d:\oradata\PROD\log2a.rdo','e:\oradata\PROD\log2b.rdo') SIZE 5M;
```

图 8.34 展示了如何在创建名为 `PROD` 的新数据库时，指定一个名为 `RBS` 的 500MB 撤销表空间。如果 `UNDO_MANAGEMENT` 参数设置为 `AUTO`，且在创建数据库时未指定撤销表空间，`Oracle` 将创建一个名为 `SYS_UNDOTBS` 的表空间来存储撤销段。在 Unix 系统上，该表空间的数据文件将创建在 `$ORACLE_HOME/dbs` 目录中；在 Windows 2000 系统上，则创建在 `%ORACLE_HOME%\dbs` 目录中。

##### 管理撤销表空间

虽然数据库可以拥有多个撤销表空间，但一旦配置了自动撤销管理，数据库中同时只能有一个活动的撤销表空间。然而，如果需要将数据库从一个系统管理的撤销表空间切换到另一个，可以使用以下 SQL 命令来实现：

```
SQL> ALTER SYSTEM SET UNDO_TABLESPACE=rbs;
```

一旦发出上述命令，任何新事务都会将前镜像数据写入 `UNDO` 表空间。但是，在发出 `ALTER SYSTEM` 命令之前已经开始的事务，其前镜像数据将保留在之前的撤销表空间中，直到这些事务完成并且 `UNDO_RETENTION` 期限已过。

基于这些限制，如果发现某个撤销表空间不再需要，还可以使用 `DROP TABLESPACE` 命令将其删除：

- 要删除的表空间不能是当前的活动撤销表空间

- 该表空间中不能有正在运行的、未提交的前镜像数据事务

> **警告**
>
> 如果需要读取一致性数据，而该数据存储在已删除的撤销表空间中，相关事务在需要这些数据时将收到错误。

##### 监控系统管理的撤销性能

创建之后，可以使用 `DBA_TABLESPACES` 和 `V$UNDOSTAT` 视图来监控系统管理的撤销表空间。

###### 使用 DBA_TABLESPACES 管理撤销表空间

`DBA_TABLESPACES` 数据字典视图中的 `CONTENTS` 列将为数据库中每个 `AUM`（自动撤销管理）表空间包含一个 `UNDO` 条目。以下查询显示该数据库有三个撤销表空间：默认撤销表空间 `UNDOTBS`，以及另外两个撤销表空间 `UNDO` 和 `RBS`：

```
SQL> SELECT tablespace_name, contents
2  FROM dba_tablespaces;
```

| 表空间名称 | 内容 |

| :-- | :-- |

| SYSTEM | PERMANENT |

| UNDOTBS | UNDO |

| APPL_IDX | PERMANENT |

| APPL_TAB | PERMANENT |

| TEMP | TEMPORARY |

| TOOLS | PERMANENT |
