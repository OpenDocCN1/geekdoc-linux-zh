
连接到 CONNECTION 选项中的服务器名称。若要命名服务器 corn_sampdb_server，请使用此语句：

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

MySQL 服务器将此定义存储为 mysql 数据库中 servers 表中的一行。若要创建一个引用服务器定义的表，请在 CONNECTION 选项中使用如下语句的服务器名称：

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

使用服务器定义比在 CONNECTION 选项中列出连接参数更安全，因为该定义仅对拥有 mysql 数据库访问权限的用户可见。此外，服务器定义可以使表设置更加容易，因为共享相同连接参数的多个 FEDERATED 表可以使用相同的定义。

## 2.6.3 删除表

删除表比创建表容易得多，因为你不需要指定其内容格式的任何信息。你只需要给它命名：

```
DROP TABLE tbl_name;
```

MySQL 以几种有用的方式扩展了 DROP TABLE 语句。若要删除多个表，请在同一语句中指定它们：

```
DROP TABLE tbl_name1, tbl_name2, ... ;
```

如果你不确定某个表是否存在，但希望如果它存在则删除它，请在语句中包含 IF EXISTS：

```
DROP TABLE IF EXISTS tbl_name;
```

IF EXISTS 子句会抑制针对不存在表的错误。（对于每个表，服务器都会生成一个警告，你可以使用 SHOW WARNINGS 查看。）

IF EXISTS 在你用于 mysql 客户端的脚本中特别有用。默认情况下，mysql 在发生错误时会退出，而尝试删除一个不存在的表就是一个错误。例如，你可能有一个设置脚本，该脚本创建的表作为其他脚本中进一步处理的基础。在这种情况下，你希望确保设置脚本开始时处于干净状态。如果脚本开头使用普通的 DROP TABLE，第一次运行时它会失败，因为表从未被创建过。如果你使用 IF EXISTS，就不会有问题。如果表存在，它们会被删除。如果不存在，不会发生错误，脚本将继续执行。

若要仅在表是临时表时才删除该表，请包含 TEMPORARY 关键字：

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
- 对于 ENUM 或 SET 以外的字符串数据类型，你可以选择索引列的前缀；即仅最左边的 n 个字符，或对于二进制字符串类型，为 n 个字节。（对于 BLOB 和 TEXT 列，只有当你指定前缀长度时，才能设置索引。）如果列在指定的前缀长度内大部分是唯一的，你通常不会牺牲性能，甚至可能提高性能：索引列的前缀而不是整个列可以使索引更小，访问速度更快。

并非所有存储引擎都提供所有索引功能。表 2.3 总结了 MySQL 一些存储引擎的索引属性。该表不包括 MERGE 存储引擎，因为 MERGE 表由 MyISAM 表创建并具有类似的索引特性。也不包括 ARCHIVE、BLACKHOLE、CSV 或 EXAMPLE 引擎，这些引擎要么完全不支持索引，要么仅以有限的方式支持索引。

表 2.3 存储引擎索引特性

| 索引特性 | MyISAM | MEMORY | InnoDB | Falcon |
| :--- | :--- | :--- | :--- | :--- |
| 允许 NULL 值 | 是 | 是 | 是 | 是 |
| 每个索引的列数 | 16 | 16 | 16 | 16 |
| 每个表的索引数 | 64 | 64 | 64 | 64 |
| 最大索引行大小（字节） | 1000 | 1024/3072 | 1024/3072 | 1100 |
| 索引列前缀 | 是 | 是 | 是 | 是 |
| 最大前缀大小（字节） | 1000 | 1024/3072 | 767 | 1100 |
| BLOB/TEXT 索引 | 是 | 否 | 是 | 否 |
| FULLTEXT 索引 | 是 | 否 | 否 | 否 |
| SPATIAL 索引 | 是 | 否 | 否 | 否 |
| HASH 索引 | 否 | 是 | 否 | 否 |

对于 MEMORY 和 InnoDB 存储引擎，在 MySQL 5.0.17/5.1.4 之前，索引大小限制为 1024 字节，从 5.0.17/5.1.4 开始为 3072 字节。MEMORY 索引前缀大小限制也是如此。

各种存储引擎在索引特性上存在差异的一个含义是，如果你要求索引具有某些属性，你可能无法使用某些类型的表。例如，要使用 FULLTEXT 或 SPATIAL 索引，你必须使用 MyISAM 表。要索引 TEXT 列，你必须使用 MyISAM 或 InnoDB。

如果你有一个现有的表，想要将其转换为使用具有更合适索引特性的不同存储引擎，请使用 ALTER TABLE 更改引擎。假设你正在使用 MyISAM 表，但需要 InnoDB 或 Falcon 提供的功能特性。使用以下语句之一转换该表：

```
ALTER TABLE tbl_name ENGINE = InnoDB;
ALTER TABLE tbl_name ENGINE = Falcon;
```

#### 2.6.4.2 创建索引

MySQL 可以创建多种类型的索引：

- 唯一索引。此索引不允许重复值。对于单列索引，这确保列不包含重复值。对于多列（复合）索引，它确保表中列中值组合的行没有重复。
- 普通（非唯一）索引。此索引提供索引优势，但允许重复。
- FULLTEXT 索引，用于执行全文搜索。此索引类型仅支持 MyISAM 表。有关更多信息，请参阅第 2.15 节，“使用 FULLTEXT 搜索”。
- SPATIAL 索引。这些仅可用于使用空间数据类型的 MyISAM 表，这些类型在第 3 章中描述。（对于支持空间数据类型的其他存储引擎，你可以创建非 SPATIAL 索引。）
- HASH 索引。这是 MEMORY 表的默认索引类型，尽管你可以覆盖默认值以创建 B-TREE 索引。

你可以使用 CREATE TABLE 为新表创建索引。相关示例在第 1.4.6 节“创建表”中展示。要为现有表添加索引，请使用 ALTER TABLE 或 CREATE INDEX。（MySQL 内部将 CREATE INDEX 语句映射为 ALTER TABLE 操作。）

ALTER TABLE 比 CREATE INDEX 更通用，因为它可以创建 MySQL 支持的任意类型的索引。例如：

```
ALTER TABLE tbl_name ADD INDEX index_name (index_columns);
ALTER TABLE tbl_name ADD UNIQUE index_name (index_columns);
ALTER TABLE tbl_name ADD PRIMARY KEY (index_columns);
ALTER TABLE tbl_name ADD FULLTEXT index_name (index_columns);
ALTER TABLE tbl_name ADD SPATIAL index_name (index_columns);
```

tbl_name 是要添加索引的表的名称，index_columns 指示要索引哪个列。如果索引由多于一列组成，请用逗号分隔名称。索引名称 index_name 是可选的。如果你省略它，MySQL 将基于第一个索引列的名称来选择一个名称。

如果索引是 PRIMARY KEY 或 SPATIAL 索引，被索引的列必须是 NOT NULL。否则，它们可以包含 NULL 值。

单个 ALTER TABLE 语句可以包含多个表修改，如果用逗号分隔它们。这使你能够同时创建多个索引，这比使用单独的 ALTER TABLE 语句一次添加一个更快。

若要放置索引上的约束以使其仅包含唯一值，请将其创建为 PRIMARY KEY 或 UNIQUE 索引。两种索引类型非常相似，但有两个区别：

- 一个表只能包含一个 PRIMARY 键。（这是因为 PRIMARY KEY 的名称始终是 PRIMARY，并且表不能有具有相同名称的两个索引。）你可以将多个 UNIQUE 索引放置在表上。
- PRIMARY KEY 不能包含 NULL 值，而 UNIQUE 索引可以。如果 UNIQUE 索引可以包含 NULL 值，它可以包含多个 NULL 值。这样做的原因为不可能知道一个 NULL 是否代表与另一个相同的值，因此它们不能被视为相等。

CREATE INDEX 可以添加大多数类型的索引，但 PRIMARY KEY 除外：

```
CREATE INDEX index_name ON tbl_name (index_columns);
CREATE UNIQUE INDEX index_name ON tbl_name (index_columns);
```

