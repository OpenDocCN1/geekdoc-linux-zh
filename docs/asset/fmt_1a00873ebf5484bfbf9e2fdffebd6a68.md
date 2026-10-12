
```sql
ALTER TABLE log_partition REORGANIZE PARTITION p4
  INTO (
    PARTITION p4 VALUES LESS THAN (2009),
    PARTITION p5 VALUES LESS THAN MAXVALUE
  );
```

默认情况下，分区存储在分区表所属数据库的目录下。要将存储分布到其他位置（例如，将它们放在不同的物理设备上），请使用 `DATA_DIRECTORY` 和 `INDEX_DIRECTORY` 分区选项。有关这些及其他分区选项语法的更多信息，请参见附录 E 中 `CREATE TABLE` 的说明。

## 2.6.2.7 使用 FEDERATED 表

`FEDERATED` 存储引擎允许你访问由另一个服务器管理的，但实际上位于一个 MySQL 服务器上的表。

假设你的本地服务器上没有 `sampdb` 数据库，但在主机 `corn.snake.net` 上运行的 MySQL 服务器上有一个可用，并且你有一个用于访问该服务器的账户。本地服务器可以通过 `FEDERATED` 存储引擎使用该账户在本地服务器上使 `sampdb` 表可用。对于你想以这种方式访问的每个表，创建一个具有与远程表相同列的 `FEDERATED` 表，但包含一个指示本地服务器如何连接远程服务器的连接字符串。

假设远程服务器上的 `student` 表具有以下定义：

```sql
CREATE TABLE student
(
  name        VARCHAR(20) NOT NULL,
  sex         ENUM('F','M') NOT NULL,
  student_id  INT UNSIGNED NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (student_id)
) ENGINE = InnoDB;
```

要在本地服务器上创建 `FEDERATED` 表，使用相同的定义，只是 `ENGINE` 选项应为 `FEDERATED`，并且应提供提供连接信息的 `CONNECTION` 表选项。（在 MySQL 5.0.13 之前，使用 `COMMENT` 选项代替 `CONNECTION`。）以下定义创建一个名为 `federated_student` 的表，该表访问 `corn.snake.net` 上的 `student` 表：

```sql
CREATE TABLE federated_student
(
  name        VARCHAR(20) NOT NULL,
  sex         ENUM('F','M') NOT NULL,
  student_id  INT UNSIGNED NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (student_id)
) ENGINE = FEDERATED
CONNECTION = 'mysql://sampadm:secret@corn.snake.net/sampdb/student';
```

`CONNECTION` 值中的连接字符串表明远程服务器上 MySQL 账户的用户名和密码分别是 `sampadm` 和 `secret`。通用的连接字符串语法如下，其中方括号表示可选信息：

```
mysql://user_name[:password]@host_name[:port_num]/db_name/[tbl_name]
```

创建 `federated_student` 表后，你可以从中选择以访问远程 `student` 表。你还可以对 `federated_student` 执行 `INSERT`、`UPDATE` 和 `DELETE` 操作，以修改 `student` 表的内容。

请注意，整个 `CONNECTION` 字符串（包括用户名和密码）对任何可以使用 `SHOW CREATE TABLE` 或类似语句针对 `FEDERATED` 表的人都是可见的。从 MySQL 5.1.15 开始，你可以避免这个问题：使用 `CREATE SERVER` 语句创建存储的服务器定义（这需要 `SUPER` 权限），并引用

连接到 `CONNECTION` 选项中的服务器名称。若要命名服务器 `corn_sampdb_server`，请使用此语句：

```
CREATE SERVER corn_sampdb_server
FOREIGN DATA WRAPPER mysql
OPTIONS (
  USER 'sampadm',
  PASSWORD 'secret',
  HOST 'corn.snake.net',
  DATABASE 'sampdb'
);
```

MySQL 服务器将此定义存储为 `mysql` 数据库中 `servers` 表中的一行。若要创建一个引用服务器定义的表，请在 `CONNECTION` 选项中使用如下语句的服务器名称：

```
CREATE TABLE federated_student2
(
    name     VARCHAR(20) NOT NULL,
    sex      ENUM('F', 'M') NOT NULL,
    student_id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    PRIMARY KEY (student_id)
) ENGINE = FEDERATED
  CONNECTION = 'corn_sampdb_server/student';
```

使用服务器定义比在 `CONNECTION` 选项中列出连接参数更安全，因为该定义仅对拥有 `mysql` 数据库访问权限的用户可见。此外，服务器定义可以使表设置更加容易，因为共享相同连接参数的多个 `FEDERATED` 表可以使用相同的定义。

### 2.6.3 删除表

删除表比创建表容易得多，因为你不需要指定其内容格式的任何信息。你只需要给它命名：

```
DROP TABLE tbl_name;
```

MySQL 以几种有用的方式扩展了 `DROP TABLE` 语句。若要删除多个表，请在同一语句中指定它们：

```
DROP TABLE tbl_name1, tbl_name2, ... ;
```

如果你不确定某个表是否存在，但希望如果它存在则删除它，请在语句中包含 `IF EXISTS`：

```
DROP TABLE IF EXISTS tbl_name;
```

`IF EXISTS` 子句会抑制针对不存在表的错误。（对于每个表，服务器都会生成一个警告，你可以使用 `SHOW WARNINGS` 查看。）

`IF EXISTS` 在你用于 `mysql` 客户端的脚本中特别有用。默认情况下，`mysql` 在发生错误时会退出，而尝试删除一个不存在的表就是一个错误。例如，你可能有一个设置脚本，该脚本创建的表作为其他脚本中进一步处理的基础。在这种情况下，你希望确保设置脚本开始时处于干净状态。如果脚本开头使用普通的 `DROP TABLE`，第一次运行时它会失败，因为表从未被创建过。如果你使用 `IF EXISTS`，就不会有问题。如果表存在，它们会被删除。如果不存在，不会发生错误，脚本将继续执行。

若要仅在表是临时表时才删除该表，请包含 `TEMPORARY` 关键字：

```
DROP TEMPORARY TABLE tbl_name;
```

### 2.6.4 表索引

索引是加速访问表中内容的主要手段，特别是对于涉及多表连接的查询。这是一个足够重要的话题，以至于有一整章讨论了为什么使用索引、它们如何工作，以及如何最好地利用它们来优化查询（第 5 章，“查询优化”）。本节涵盖各种表类型索引的特性以及创建和删除索引的语法。

#### 2.6.4.1 存储引擎索引特性

MySQL 在构建索引的方式上提供了相当大的灵活性：

- 你可以索引单列，或构建包含多个列的复合索引。
- 索引可以限制为仅包含唯一值，或允许包含重复值。
- 你可以在一个表上拥有多个索引，以有助于优化基于不同列的表中不同查询。
- 对于 `ENUM` 或 `SET` 以外的字符串数据类型，你可以选择索引列的前缀；即仅最左边的 n 个字符，或对于二进制字符串类型，为 n 个字节。（对于 `BLOB` 和 `TEXT` 列，只有当你指定前缀长度时，才能设置索引。）如果列在指定的前缀长度内大部分是唯一的，你通常不会牺牲性能，甚至可能提高性能：索引列的前缀而不是整个列可以使索引更小，访问速度更快。

并非所有存储引擎都提供所有索引功能。表 2.3 总结了 MySQL 一些存储引擎的索引属性。该表不包括 `MERGE` 存储引擎，因为 `MERGE` 表由 `MyISAM` 表创建并具有类似的索引特性。也不包括 `ARCHIVE`、`BLACKHOLE`、`CSV` 或 `EXAMPLE` 引擎，这些引擎要么完全不支持索引，要么仅以有限的方式支持索引。

表 2.3 存储引擎索引特性

| 索引特性 | MyISAM | MEMORY | InnoDB | Falcon |
| :--- | :--- | :--- | :--- | :--- |
| 允许 NULL 值 | 是 | 是 | 是 | 是 |
| 每个索引的列数 | 16 | 16 | 16 | 16 |
| 每个表的索引数 | 64 | 64 | 64 | 64 |
