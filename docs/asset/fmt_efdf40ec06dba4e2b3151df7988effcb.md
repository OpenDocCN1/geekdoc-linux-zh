
| 最大索引行大小（字节） | 1000 | 1024/3072 | 1024/3072 | 1100 |

| 索引列前缀 | 是 | 是 | 是 | 是 |

| 最大前缀大小（字节） | 1000 | 1024/3072 | 767 | 1100 |

| BLOB/TEXT 索引 | 是 | 否 | 是 | 否 |

| FULLTEXT 索引 | 是 | 否 | 否 | 否 |

| SPATIAL 索引 | 是 | 否 | 否 | 否 |

| HASH 索引 | 否 | 是 | 否 | 否 |

对于 `MEMORY` 和 `InnoDB` 存储引擎，在 `MySQL 5.0.17/5.1.4` 之前，索引大小限制为 1024 字节，从 5.0.17/5.1.4 开始为 3072 字节。`MEMORY` 索引前缀大小限制也是如此。

各种存储引擎在索引特性上存在差异的一个含义是，如果你要求索引具有某些属性，你可能无法使用某些类型的表。例如，要使用 `FULLTEXT` 或 `SPATIAL` 索引，你必须使用 `MyISAM` 表。要索引 `TEXT` 列，你必须使用 `MyISAM` 或 `InnoDB`。

如果你有一个现有的表，想要将其转换为使用具有更合适索引特性的不同存储引擎，请使用 `ALTER TABLE` 更改引擎。假设你正在使用 `MyISAM` 表，但需要 `InnoDB` 或 `Falcon` 提供的功能特性。使用以下语句之一转换该表：

```
ALTER TABLE tbl_name ENGINE = InnoDB;
ALTER TABLE tbl_name ENGINE = Falcon;
```

## 2.6.4.2 创建索引

`MySQL` 可以创建多种类型的索引：

- 唯一索引。此索引不允许重复值。对于单列索引，这确保列不包含重复值。对于多列（复合）索引，它确保表中列中值组合的行没有重复。
- 普通（非唯一）索引。此索引提供索引优势，但允许重复。
- `FULLTEXT` 索引，用于执行全文搜索。此索引类型仅支持 `MyISAM` 表。有关更多信息，请参阅第 2.15 节，“使用 `FULLTEXT` 搜索”。
- `SPATIAL` 索引。这些仅可用于使用空间数据类型的 `MyISAM` 表，这些类型在第 3 章中描述。（对于支持空间数据类型的其他存储引擎，你可以创建非 `SPATIAL` 索引。）
- `HASH` 索引。这是 `MEMORY` 表的默认索引类型，尽管你可以覆盖默认值以创建 `B-TREE` 索引。

你可以使用 `CREATE TABLE` 为新表创建索引。相关示例在第 1.4.6 节“创建表”中展示。要为现有表添加索引，请使用 `ALTER TABLE` 或 `CREATE INDEX`。`MySQL` 内部将 `CREATE INDEX` 语句映射为 `ALTER TABLE` 操作。

`ALTER TABLE` 比 `CREATE INDEX` 更通用，因为它可以创建 `MySQL` 支持的任意类型的索引。例如：

```
ALTER TABLE tbl_name ADD INDEX index_name (index_columns);
ALTER TABLE tbl_name ADD UNIQUE index_name (index_columns);
ALTER TABLE tbl_name ADD PRIMARY KEY (index_columns);
ALTER TABLE tbl_name ADD FULLTEXT index_name (index_columns);
ALTER TABLE tbl_name ADD SPATIAL index_name (index_columns);
```

`tbl_name` 是要添加索引的表的名称，`index_columns` 指示要索引哪个列。如果索引由多于一列组成，请用逗号分隔名称。索引名称 `index_name` 是可选的。如果你省略它，`MySQL` 将基于第一个索引列的名称来选择一个名称。

如果索引是 `PRIMARY KEY` 或 `SPATIAL` 索引，被索引的列必须是 `NOT NULL`。否则，它们可以包含 `NULL` 值。

单个 `ALTER TABLE` 语句可以包含多个表修改，如果用逗号分隔它们。这使你能够同时创建多个索引，这比使用单独的 `ALTER TABLE` 语句一次添加一个更快。

若要放置索引上的约束以使其仅包含唯一值，请将其创建为 `PRIMARY KEY` 或 `UNIQUE` 索引。两种索引类型非常相似，但有两个区别：

- 一个表只能包含一个 `PRIMARY` 键。（这是因为 `PRIMARY KEY` 的名称始终是 `PRIMARY`，并且表不能有具有相同名称的两个索引。）你可以将多个 `UNIQUE` 索引放置在表上。
- `PRIMARY KEY` 不能包含 `NULL` 值，而 `UNIQUE` 索引可以。如果 `UNIQUE` 索引可以包含 `NULL` 值，它可以包含多个 `NULL` 值。这样做的原因为不可能知道一个 `NULL` 是否代表与另一个相同的值，因此它们不能被视为相等。

`CREATE INDEX` 可以添加大多数类型的索引，但 `PRIMARY KEY` 除外：

```
CREATE INDEX index_name ON tbl_name (index_columns);
CREATE UNIQUE INDEX index_name ON tbl_name (index_columns);
```

`FULLTEXT`（全文）索引 `index_name` ON `tbl_name` [`index_columns`]; `SPATIAL`（空间）索引 `index_name` ON `tbl_name` [`index_columns`];

`tbl_name`、`index_name` 和 `index_columns` 的含义与 `ALTER TABLE` 中的相同。与 `ALTER TABLE` 不同，在 `CREATE INDEX` 中，索引名称不是可选的，并且你无法在单个语句中创建多个索引。

当发出 `CREATE TABLE` 语句为新表创建索引时，语法与用于 `ALTER TABLE` 的语法类似，但你除了指定列定义外，还需指定索引创建子句：

```sql
CREATE TABLE tbl_name (
    ... 列定义 ...
    INDEX index_name [index_columns],
    UNIQUE index_name [index_columns],
    PRIMARY KEY [index_columns],
    FULLTEXT index_name [index_columns],
    SPATIAL index_name [index_columns],
    ...
);
```

与 `ALTER TABLE` 一样，`index_name` 是可选的。如果你省略它，`MySQL` 会选择一个索引名称。

作为一个特殊情况，你可以通过在列定义的末尾添加 `PRIMARY KEY` 或 `UNIQUE` 子句来创建单列的 `PRIMARY KEY`（主键）或 `UNIQUE`（唯一）索引。例如，以下两个 `CREATE TABLE` 语句是等价的：

```sql
CREATE TABLE mytbl (
    i INT NOT NULL PRIMARY KEY,
    j CHAR(10) NOT NULL UNIQUE
);

CREATE TABLE mytbl (
    i INT NOT NULL,
    j CHAR(10) NOT NULL,
    PRIMARY KEY (i),
    UNIQUE (j)
);
```

`MEMORY` 表的默认索引类型是 `HASH`（哈希）。哈希索引对于精确值查找非常快，这是使用 `MEMORY` 表的典型方式。然而，如果你打算将 `MEMORY` 表用于可以匹配值范围（例如，`id` < 100）的比较，则哈希索引效果不佳。在这种情况下，最好创建 `BTREE`（B 树）索引。你可以通过在索引定义中添加 `USING BTREE` 子句来实现：

```sql
CREATE TABLE nametbl
```

要为字符串列的前缀创建索引，索引定义中指定列名的语法是 `col_name(n)`，而不仅仅是 `col_name`。前缀值 `n` 表示索引应包含二进制字符串类型的前 `n` 个字节，或非二进制字符串类型的前 `n` 个字符。例如，以下语句创建一个包含 `CHAR` 列和 `BINARY` 列的表。它对 `CHAR` 列的前 10 个字符和 `BINARY` 列的前 15 个字节创建索引：

```sql
CREATE TABLE addresslist
(
    name     CHAR(30)  NOT NULL,
    address  BINARY(60)  NOT NULL,
    INDEX (name(10)),
    INDEX (address(15))
);
```
