
存在特殊的列类型，例如 `DATE`，它只接受特定格式的数据；以及 `ENUM`（枚举），它可以用于指定只允许某些值。例如，如果你想记录 CD 的流，可以使用 `ENUM` 列，它只接受 `POP`、`ROCK`、`EASY_LISTENING` 等值。你将在后面的章节中学习更多关于 `ENUM` 的知识。

查看 `cd_collection` 表，你可以看到其中三列存储数值数据，其他列存储字符串数据。此外，这些字符串是变长度的。根据这些信息，你可以判断出用于文本列的最佳类型是 `VARCHAR`，而其他列的最佳类型是 `INT`。你还注意到 `cd_collection` 表的另一个一点：其中一张 CD 缺少评分，也许可能是因为我们还没有听过它。因此，这个值是可选的；它初始为空，并且稍后可以填充。

你现在准备好创建一个表了。如前所述，你可以使用 `CREATE` 语句来创建表，其语法如下：

```
CREATE TABLE table_name (column_name column_type(parameters) options, ...);
```

你应该知道如何格式化 `CREATE` 语句：

- `SQL` 命令是不区分大小大小的——例如，`CREATE TABLE`、`create table` 和 `Create Table` 都是有效的。
- 空格通常会被忽略——这意味着你应该使用空格来让你的 `SQL` 命令更清晰。

接下来的示例显示了如何为 `cd_collection` 数据库创建表：

```sql
CREATE TABLE cd_collection
(
id INT NOT NULL,
title VARCHAR(50) NOT NULL,
artist VARCHAR(50) NOT NULL,
year VARCHAR(50) NOT NULL,
rating VARCHAR(50) NOT NULL
);
```

注意该语句以分号结束。这是 `SQL` 知道你已完成语句中所有条目的方式。在某些情况下，可以省略分号，我们会在它们出现时指出来。

> 提示 `SQL` 有许多保留关键字，不能用在表名或字段名中。例如，如果你在记录想要带去度假的 CD，你将无法使用 `select` 作为字段名，因为它是保留关键字。相反，你应该选择一个不同的名称（如 `selected?`）或者直接在字段名前加上前缀 `f`，例如 `fselect`。

## 向表中插入数据

创建表后，你就可以向它们放入数据。你可以使用 `INSERT` 语句手动插入数据，其语法如下：

```
INSERT INTO table_name VALUES('value1', 'value2', 'value3', ...);
```

该语句将 `value1`、`value2` 等插入到 `table_name` 表中。插入的值构成了数据库中的一行（或一条记录）。除非另有说明，否则值的插入顺序与列在数据库表中列出的顺序一致。如果由于某种原因，你想以不同的顺序插入值（或者你只想插入少数几个值且这些它们不是连续的），你可以使用以下语法指定数据要去的列：

```sql
INSERT INTO table_name (column1,column4) VALUES('value1', 'value2');
```

你还可以使用单个 `INSERT` 语句填充多行数据，使用如下语法：

```sql
INSERT INTO table_name VALUES('value1', 'value2'),('value3', 'value4');
```

在该语句中，`value1` 和 `value2` 被插入到第一行，`value3` 和 `value4` 被插入到第二行。

接下来的示例显示了你如何向 `cd_collection` 表插入 `Nevermind` 条目：

```sql
INSERT INTO cd_collection VALUES(9, 'Nevermind', 'Nirvana', '1991', NULL);
```

如果你不想包含评分，`MySQL` 要求最后一列（`rating`）为 `NULL` 值。相比之下，`PostgreSQL` 允许省略最后一列。当然，如果你中间的列为空，你需要在 `INSERT` 语句中显式声明 `NULL`。

通常，`INSERT` 语句被编码在前端程序中，这样向数据库添加数据的用户就不必担心涉及 `SQL` 语句。

## 从数据库检索数据

当然，在数据库中存储数据的主要原因是你之后可以对这些数据进行查询、排序和生成报告。基本的数据检索通过 `SELECT` 语句完成。

接下来的示例显示了你如何从 `cd_collection` 表检索所有数据：

```sql
SELECT * FROM cd_collection;
```

接下来的示例显示了你如何只检索特定的列：

```sql
SELECT title, artist FROM cd_collection;
```

接下来的示例显示了你如何使用 `WHERE` 子句过滤结果：

```sql
SELECT * FROM cd_collection WHERE year = 1991;
```

接下来的示例显示了你如何使用 `ORDER BY` 子句对结果进行排序：

```sql
SELECT * FROM cd_collection ORDER BY year;
```

# 速度

直到最近，速度的选择一直非常简单：如果查询速度对你的应用程序至关重要，你就会使用 `MySQL`。`MySQL` 以极快的数据库而闻名。直到最近，相比之下，`PostgreSQL` 的速度相当慢。

较新版本的 `PostgreSQL` 在速度方面有所改进（涉及磁盘访问、排序等）。在某些情况下，例如并发访问期间，`PostgreSQL` 的速度可以比 `MySQL` 快得多，正如你将在下一节中看到的。但与许多其他数据库相比，`MySQL` 仍然极快。

# 数据锁定

为了防止数据损坏，数据库在访问数据时需要对数据加锁。只要锁存在，在第一个进程释放之前，任何其他进程都无法访问数据。这意味着任何尝试访问数据的其他进程都必须等待当前进程完成。下一个进程锁定数据直到其完成，其余进程则必须轮流等待，依此类推。

当然，在数据库上执行的操作通常完成得很快。在同时访问数据库的用户较少的环境中，锁的持续时间通常很短，不会导致任何显著的延迟。然而，在许多人同时访问数据库的环境中，锁定可能会产生性能问题，因为人们必须等待访问数据库。

旧版本的 `MySQL` 在表级上锁定数据，这可以被认为是密集访问期间的瓶颈。这意味着当有人在表中写入某行数据时，整个表都会被锁定，导致其他人无法输入数据。如果你的表中有 500,000 行（或记录），每当访问一行时，所有 500,000 行都会锁定。再次，在并发用户较少的环境中，这不会导致性能问题，因为大多数操作完成得非常快，锁定时间极短。然而，在许多人同时访问数据的环境中，`MySQL` 的表级锁定可能成为一个巨大的瓶颈。

另一方面，`PostgreSQL` 在行级上锁定数据。在 `PostgreSQL` 中，只有当前正在访问的行被锁定。其他用户可以访问表的其余部分。这种行级锁定显著减少了在大量并发用户环境中锁定对性能的影响。因此，作为一条通用规则，`PostgreSQL` 比 `MySQL` 更适用于高负载环境。

`Fedora` 随附的 `MySQL` 版本为你提供了使用表级锁定或行级锁定表的选项。在 `MySQL` 术语中，`MyISAM` 使用表级锁定，而 `InnoDB` 表使用行级锁定。

# 选择数据库：MySQL 对比 PostgreSQL 399

注意

`MySQL` 的数据锁定方法在 http://www.mysql.com/doc/en/Internal_locking.html 有更深入的讨论。

你可以在 http://www.postgresql.org/docs/7.4/interactive/sql-lock.html 找到关于 `PostgreSQL` 定的更多信息。

# 事务处理中的 ACID 合规性以保护数据完整性

`MySQL` 和 `PostgreSQL` 的另一个不同点在于它们为防止数据损坏所提供的保护程度。`ACID` 缩写通常用于描述数据保护的几个方面：

- **原子性（Atom）**——这意味着多个数据库操作被视为一个不可分割（原子）的单元。在事务中，要么执行所有单元操作，要么一个都不执行。换句话说，如果原子单元中的任何操作失败，整个原子单元都将取消。
- **一致性（Consistency）**——确保任何事务都不会导致数据库处于不一致状态。不一致的情况可能由数据库客户端崩溃、网络故障和类似情况引起。一致性确保了在这样的情况下，任何会导致数据处于不一致状态的事务或部分完成的事务将得到回滚或撤销。
- **隔离性（Isolation）**——确保在相同数据上操作的多个事务彼此完全隔离。这防止了当两个用户尝试同时写入同一条记录时发生的数据损坏。隔离性通常由数据库程序员通过配置来处理。如之前讨论的，处理隔离性的一种方法是通过锁定。
