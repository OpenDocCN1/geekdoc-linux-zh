
如果在被修改的表中，该操作可能产生唯一索引中的重复键值，则 `keyword` 将发挥作用。如果没有 `IGNORE`，`ALTER TABLE` 语句的效果将被取消。如果有 `IGNORE`，则具有唯一键值中重复值的行会被删除。

除了重命名表的操作外，`ALTER TABLE` 的工作原理是创建一个新的表，该表基于原始表并包含要做的更改。如果发生错误，新表将被丢弃，原始表保持不变。如果操作成功完成，原始表将被丢弃并由新表替换。在操作期间，其他客户端可能从原始表中读取数据。任何尝试更新表的客户端都会被阻塞，直到 `ALTER TABLE` 语句完成，此时更新将应用于新表。

`action` 值指定修改操作，每个操作依次执行。某些操作不能与其他操作组合使用，这在操作说明中有指出。

对于包含 `index_type` 或 `index_option` 子句的索引定义操作，某些存储引擎允许你指定索引算法或其他索引定义修饰符。有关不同版本 MySQL 中允许哪些索引值的详细信息，请参阅 `CREATE INDEX` 条目。有关索引创建的更多信息，请参阅第 2.6.4 节，“索引表”。

`action` 值可以是以下任意一项：

### `table_option`

指定在 `CREATE TABLE` 语句的 `table_option` 部分中可能给出的表选项类型。

```sql
ALTER TABLE score ENGINE = MyISAM CHECKSUM = 1;
ALTER TABLE sayings CHARACTER SET utf8;
```

关于给定表选项可用性的版本特定或存储引擎特定限制，如 `CREATE TABLE` 条目中所述。如果你尝试将表更改为使用不可用的存储引擎，`ALTER TABLE` 语句的效果取决于 `NO_ENGINE_SUBSTITUTION` SQL 模式的设置。从 MySQL 5.0.23/5.1.11 开始，不允许将表更改为使用 `MERGE` 或 `BLACKHOLE` 引擎，因为更改可能导致数据丢失。

`[DEFAULT] CHARACTER SET` 表选项更改了默认表字符集，但不会将现有列转换为该字符集。要执行后一种操作，请使用 `CONVERT TO CHARACTER SET` 操作。

```sql
ALTER TABLE IGNOREs the DATA DIRECTORY and INDEX DIRECTORY table options.
```

### `ADD [COLUMN] col_name col_definition [FIRST | AFTER col_name]`

向表中添加列。`col_name` 是列名。`col_definition` 是列定义；其格式与 `CREATE TABLE` 语句中使用的格式相同。如果给出 `FIRST` 关键字，则该列成为表中的第一列；如果给出 `AFTER col_name`，则放置在指定列之后。如果未指定列的位置，则该列成为表的最后一列。

```sql
ALTER TABLE t ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY;  
ALTER TABLE t ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY FIRST;  
ALTER TABLE t ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY  
    AFTER suffix;
```

### `ADD [COLUMN] (create_definition, . . . )`

向表中添加列或索引。每个 `create_definition` 是列或索引定义，格式与 `CREATE TABLE` 相同。

### `ADD [CONSTRAINT [name]] FOREIGN KEY {fk_name}`

`(index_columns) reference_definition`

向表中添加外键定义。此功能仅支持 InnoDB 表。

外键基于 `index_columns` 中命名的列，它是表中由逗号分隔的一个或多个列的列表。任何 `CONSTRAINT` 名称，如果给定，将被忽略。`fk_name` 是外键 ID。如果给定，除非 InnoDB 自动为外键创建索引，否则会被忽略；在这种情况下，`fk_name` 成为索引名称。`reference_definition` 定义外键如何与父表相关。语法如 `CREATE TABLE` 条目中所述。

```sql
ALTER TABLE child  
    ADD FOREIGN KEY (par_id) REFERENCES parent (par_id) ON DELETE CASCADE;  
ADD FOREIGN KEY and DROP FOREIGN KEY actions cannot appear in the same  
ALTER TABLE statement.
```

### `ADD [FULLTEXT [INDEX | KEY] [index_name} (index_columns) {index_option} . . .`

向 MyISAM 表添加 `FULLTEXT` 索引。该索引基于 `index_columns` 中命名的列，它是表中由逗号分隔的一个或多个非二进制字符串列的列表。`index_name` 的指定方式与 `ADD INDEX` 操作相同。

```sql
ALTER TABLE poetry ADD FULLTEXT (author,title,stanza);
```

### `ADD {INDEX | KEY} [index_name} [index_type] (index_columns) [index_option] . . .`

向表中添加索引。该索引基于 `index_columns` 中命名的列，它是表中由逗号分隔的一个或多个列的列表。如果未指定索引名称 `index_name`，MySQL 将根据第一个索引列的名称自动选择一个名称。

### `ADD [CONSTRAINT [name]] PRIMARY KEY [index_type] (index_columns) [index_option] ...`

在给定列上添加主键。键的名称为 `PRIMARY`。`index_columns` 的指定方式与添加 `INDEX` 操作相同。每个列必须定义为 NOT NULL。如果已经存在主键，则会发生错误。

```sql
ALTER TABLE president ADD PRIMARY KEY (last_name, first_name);
```

### `ADD SPATIAL [INDEX | KEY] [index_name] (index_columns) [index_option] ...`

向 MySQL 表添加 `SPATIAL` 索引。该索引基于 `index_columns` 中命名的列，它是表中由逗号分隔的一个或多个空间列的列表。每个列必须定义为 NOT NULL。`index_name` 的指定方式与添加 `INDEX` 操作相同。

```sql
ALTER TABLE coordinates ADD SPATIAL (x,y);
```

### `ADD [CONSTRAINT [name]] UNIQUE [INDEX | KEY] [index_name] [index_type] (index_columns) [index_option] ...`

向 `tbl_name` 添加唯一值索引。`index_name` 和 `index_columns` 的指定方式与添加 `INDEX` 操作相同。

```sql
ALTER TABLE absence ADD UNIQUE id_date (student_id, date);
```

### `ALTER [COLUMN] col_name (SET DEFAULT value | DROP DEFAULT)`

修改给定列的默认值，要么设置为指定值，要么删除当前默认值。在后一种情况下，可能会分配新的隐式默认值，如第 3.2.3 节“指定列默认值”中所述。

```sql
ALTER TABLE grade_event ALTER category SET DEFAULT 'Q';
ALTER TABLE grade_event ALTER category DROP DEFAULT;
```

### `CHANGE [COLUMN] old_col_name new_col_name col_definition [FIRST | AFTER col_name]`
