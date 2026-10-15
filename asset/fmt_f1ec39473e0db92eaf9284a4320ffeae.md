
如果数据库没有使用临时表空间进行排序，每个执行排序的用户都必须在其临时表空间内构建并删除一个排序段。这种对单个排序段的动态管理在 I/O 和递归数据字典调用方面是非常昂贵的。与存储在永久表空间中的排序段不同，临时表空间中的排序段在用户断开时不会被删除。相反，实例启动后的第一次排序操作会创建一个排序段，该段留在临时表空间中，供后续执行磁盘排序的用户复用。该排序段将一直保留到实例关闭。你可以使用 `V$SORT_SEGMENT` 和 `V$SORT_USAGE` 数据视图监控排序段的大小和用法。这些视图的内容与

Copyright ©2002 SYBEX, Inc., Alameda, CA www.syex.com

[第461 页]

默认情况下，排序段的 `MAXENTS` 值为 `UNLIMITED`。

# 使用 V$SORT_SEGMENT

`V$SORT_SEGMENT` 视图允许你监控位于临时表空间中的排序段的大小和用法。以下查询显示了该视图更有用的列：

```sql
SQL> SELECT tablespace_name,
2      current_users,
3      max_sort_blocks
4      FROM v$sort_segment;
```

TABLESPACE_NAME CURRENT_USERS MAX_SORT_BLOCKS

-----------------------------

TEMP

此查询输出显示用户正在使用 TEMP。此外，特别是某个特定用户的最大排序，在以下情况下可能很有用：

通过设置这些 `init.ora` 参数至少达到 `MAX_SORT_BLOCKS * DB_BLOCK_SIZE`，你可以在内存中容纳更多排序并减少 I/O。

# 使用 V$SORT_USAGE

虽然 `V$SORT_SEGMENT` 显示了整体排序操作，但它不允许你看到哪些特定用户导致了大量的磁盘排序。然而，`V$SORT_USAGE` 视图包含一个 `USER` 列，可以如下所示所示监控用户的排序活动：

```sql
SQL> SELECT user, tablespace,
2      blocks
3      FROM v$sort_usage
4      ORDER BY blocks;
```

[第462 页]

# 424 第 8 章 · 磁盘 I/O 调优

| USER | TABLESPACE | BLOCKS |
| --- | --- | --- |
| APPS | TEMP | 200 |
| JOE | TEMP | 110 |
| BRENDA | TEMP | 20 |

`TABLESPACE` 列告诉你排序在哪个表空间执行。`BLOCKS` 列表示 Oracle 块中的排序大小。在设置 `init.ora` 参数 `SORT_AREA_SIZE` 和 `SORT_AREA_RETAINED_SIZE` 时，监控此值也很有用。

> 注意：`V$SORT_USAGE` 视图仅在至少有一个排序进行时包含条目。如果你在没有用户连接或没有执行排序时查询此视图，将不会返回行。

# 排序：全貌

了解哪些用户在数据库中执行最多的排序是有用的信息。然而，具体知道他们在执行哪些 SQL 操作通常更有用。通过这些信息，你可能识别出可以通过创建新索引或重写应用程序代码来消除排序的 SQL 语句。

对 `v$SESSION`、`v$SQLAREA` 和 `v$SORT_USAGE` 执行以下查询显示了如何识别高排序活动用户发出的 SQL：

```sql
SQL> SELECT sess.username,
2 sql.sql_text,
3 sort.blocks
4 FROM v$session sess,
5 v$sqltext sort,
6 v$sort_usage sort
7 WHERE sess.serial# = sess.session_num
8 AND sort.sqladdr = sql.address
9 AND sort.sqlhash = sql.hash_value
10 AND sort.blocks > 200;
```

## 优化回滚段 I/O 425

| USERNAME | SQL_TEXT | BLOCKS |
|--- |--- |--- |
| APPS | SELECT customer_id, customer_name FROM customer ORDER BY city, state | 210 |

## 优化回滚段 I/O

Oracle 的基本原则之一是绝不允许用户查看来自另一个用户未提交事务的数据。为了实现这一目标，当应用程序执行 DML 活动时，Oracle 必须使用回滚段（rollback segments）来存储被更改数据的之前的映像（before-image）。Oracle 不使用缓冲区缓存（Buffer Cache）中未提交的脏缓冲区包含的数据，而是在其他应用程序用户请求时，使用这些之前的映像来显示修改数据的原始版本。反之，回滚段在每个数据库 DML 事务中都起着至关重要的作用。因此，应该检查回滚段以可能的性能改进。本节提供了有关如何使用回滚段处理用户事务的更多细节。

## 理解回滚段

当用户启动一个 DML 事务时，更改数据的之前的映像会被缓存在 SGA 中的数据库缓冲区缓存（Database Buffer Cache）中。这些缓冲区的副本也会被写入存储在表空间（tablespace）中的回滚段。该表空间由一个或多个物理数据文件（Datafiles）组成。存储在回滚段中的之前的映像数据有三个重要用途：

- 如果执行 DML 命令的用户发布 ROLLBACK 命令，可以使用它可以恢复数据的原始状态。
- 它为在 DML 用户发布 COMMIT 命令之前访问相同数据的其他用户提供更改数据的读一致性视图。
- 在实例恢复期间，它被用于撤销在实例故障发生前正在进行的未提交事务。

Copyright ©2002 SYBEX, Inc., Alameda, CA www.syex.com

## 426 第 8 章 • 优化磁盘 I/O

回滚段也被称为撤销段（undo segments），因为它们在发布 ROLLBACK 命令时被用于撤销事务。

与任何其他数据库段一样，回滚段由区段（extents）组成，而区段又由五个或更多连续的 Oracle 数据块（blocks）组成。在每个回滚段内部，Oracle 以循环方式使用区段，直到回滚段填满。一旦填满，在用户发布 COMMIT 或 ROLLBACK 命令释放部分回滚段空间之前，将不会为其分配新事务。单个回滚段可以存储多个不同事务的之前的映像。然而，一个事务仅将其之前的映像信息写入一个回滚段中。图 8.23 说明了由八个区段组成的回滚段 RBS01 的这种情况。

### 图 8.23 事务如何使用回滚段

![](img/c36db8fbb4893c630ad429a99bfd63e3_464_0.png)

图 8.23 显示，事务 A 和 B 都将它们的之前的映像存储在回滚段 RBS01 的区段 1 中，而一个较大的事务（C）正在使用区段 2 到 6 来存储其撤销信息。区段 7 和 8 目前处于非活动状态。

## 优化回滚段 I/O 427

一旦事务被分配给回滚段，该事务永远不会切换到不同的回滚段，即使原始的回滚段不是最选择。如果一个事务的之前的映像从回滚段的某个区段开始增长并填满了该区段，该事务将绕入相邻的区段并继续向该区段写入之前的映像信息。图 8.24 描述了上述事务 C 的这一概念。

### 图 8.24 事务之前的映像环绕到下一个区段

![](img/c36db8fbb4893c630ad429a99bfd63e3_465_0.png)

如果相邻的区段已经包含其他活动事务的之前的映像信息，Oracle 将不会覆盖该信息，而是向回滚段添加新的区段，以存储事务不断增长的之前的映像。图 8.25 显示了当大事务需要额外空间存储其之前的映像时，这种分配是如何发生的。

图 8.25 显示了需要额外空间存储之前的映像的事务 C 无法从区段 6 绕到区段 7，因为事务 D 已经在使用区段 7 存储其之前的映像。Oracle 也不允许事务 C 跳过区段 7 直接使用空区段 (8)。这导致添加了一个新的区段 (N)，事务 C 随后绕入该区段以存储其之前的映像。

## 428 第 8 章 • 优化磁盘 I/O

事务导致回滚段环绕和扩展的频率将是优化其性能的关键。

### 动态回滚段区段分配

### 图 8.25 动态回滚段区段分配

![](img/c36db8fbb4893c630ad429a99bfd63e3_466_0.png)

除非你使用 SET ROLLBACK SEGMENT 命令请求特定的回滚段，否则 Oracle Server 分配事务到回滚段的方式使得每个段管理相同数量的事务。回滚段能够处理的事务总数取决于数据库的 Oracle 块大小。

> 使用大对象 (LOB) 数据类型的列将不会使用回滚段来存储 LOB 之前的映像。这些段使用创建时分配给段的 PCTVERSION 值相关的空间来存储 LOB 之前的映像。

## 优化回滚段 I/O
