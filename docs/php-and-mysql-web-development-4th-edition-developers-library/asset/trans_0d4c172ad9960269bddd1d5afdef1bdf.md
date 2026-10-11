
-   `ssl_session_cache_mode`
    服务器使用的 SSL 缓存类型。
-   `ssl_session_cache_overflows`
    因缓存已满而从缓存中移除的会话数量。
-   `ssl_session_cache_size`
    SSL 会话缓存中可存储的会话数量。
-   `ssl_session_cache_timeouts`
    已超时的会话数量。
-   `ssl_sessions_reused`
    会话是否是从较早的会话中复用的。
-   `ssl_used_session_cache_entries`
    会话缓存中的会话数量。
-   `ssl_verify_depth`
    SSL 验证深度。
-   `ssl_verify_mode`
    SSL 验证模式。
-   `ssl_version`
    连接的 SSL 协议版本。

### D.4 用户定义变量

用户定义变量（或更简单地称为“用户变量”）可以被赋值，并且你可以在随后的其他语句中引用这些变量。

用户定义变量的名称由“@”后跟一个标识符组成，并遵循与合法标识符类似的规则（参见第 2.2 节，“MySQL 标识符语法和命名规则”）。然而，与标识符不同，用户变量名称可以包含“.”而不需要加引号。在 MySQL 5.0 之前，用户变量名称是区分大小写的，在此之后则不区分大小写。

用户变量可以通过 SET 语句中的 = 或 := 运算符，或者在 SELECT 等其他语句中的 := 运算符进行赋值。可以在单个语句中执行多个赋值。

```sql
mysql> SET @x = 0, @y = 2;
mysql> SET @color := 'red', @size := 'large';
mysql> SELECT @x, @y, @color, @size;
```

| @x | @y | @color | @size |
|----|----|--------|-------|
| 0  | 2  | red    | large |

```sql
mysql> SELECT @count := COUNT(*) FROM member;
+-------------------------+
| @count := COUNT(*) |
+-------------------------+
|                   102 |
+-------------------------+
```

用户变量可以被赋值为整数、十进制数、浮点数、字符串或 NULL 值，并且可以从任意表达式中赋值，包括引用其他变量的表达式。如果你访问一个尚未显式赋值的用户变量，其值为 NULL。

用户变量的值不会在服务器会话之间持久化。也就是说，当连接终止时，值会丢失。

在返回多行的 SELECT 语句中，变量赋值会对每一行执行。最终值是最后一行赋的值。

字符串值的用户变量具有与其赋值的值相同的字符集和排序规则：

```sql
mysql> SET @s = CONVERT('abc' USING latin2) COLLATE latin2_czech_cs;
mysql> SELECT CHARSET(@s), COLLATION(@s);
+------------+------------------+ 
| CHARSET(@s) | COLLATION(@s) | 
+------------+------------------+ 
| latin2     | latin2_czech_cs| 
+------------+------------------+
```

## SQL 语法参考

本附录描述了 MySQL 提供的 SQL 语句的语法。它包含三个部分：

-   除复合语句之外的 SQL 语句。
-   用于复合语句的 SQL 语句，这些语句使用 `BEGIN` 和 `END` 编写，可用于编写存储在服务器端的存储程序（函数、过程、触发器和事件）。
-   在 SQL 代码中编写注释的语法。注释用于编写被服务器忽略的描述性文本，以及隐藏将被 MySQL 执行但被其他数据库服务器忽略的 MySQL 特定关键字。

语句语法描述使用以下约定：

-   方括号 `([])` 表示可选信息。
-   竖线 `(|)` 分隔列表中的替代项。如果列表包含在方括号中，则可以选择一个替代项。如果列表包含在花括号 `({})` 中，则必须选择一个替代项。
-   省略号表示法 `(...)` 表示省略号前面的术语可以重复。
-   `n` 表示整数。
-   `'str'` 表示字符串值。诸如 `'file_name'` 或 `'pattern'` 这样带引号的值表示更具体的值类型，如文件名或模式。

除非另有说明，本附录中列出的语句至少从 MySQL 5.0.0 起就已存在。自从那时起引入或含义发生变化的语句已作标注。

一些语句已被弃用、计划移除或（在我看来）实用性极其有限，因此我没有在此列出：

-   BACKUP TABLE
-   LOAD DATA FROM MASTER
-   LOAD TABLE tbl_name FROM MASTER
-   RESTORE TABLE
-   SHOW AUTHORS
-   SHOW CONTRIBUTORS

我也没有涵盖与插件、用户定义函数 (UDFs)、XA 事务或 MySQL Cluster 特定的语句或语句子句。

存在一些始终成立的通用同义词，因此我将它们列在这里，而不是在每一个可以使用它们的地方列出：

要指定字符集，你可以使用以下任何格式：

```sql
CHARACTER SET charset
CHARSET = charset
CHARSET charset
```

这些同义形式可用于表和列定义，以及 CREATE DATABASE 和 ALTER DATABASE 语句中。

从 MySQL 5.0.2 开始，SCHEMA 和 SCHEMAs 分别是 DATABASE 和 DATABASES 的同义词，并可以在任何可能使用后两个关键字的语句中自由替换。例如，你可以使用 CREATE DATABASE 或 CREATE SCHEMA 创建数据库。

### E.1 SQL 语句语法 (非复合语句)

本节描述了 MySQL 的每个 SQL 语句的语法和含义，但不包括用于编写复合语句的语句（后者参见第 E.2 节，“复合语句语法”）。如果你没有执行某条语句所需的权限，该语句将会失败。例如，如果你没有访问数据库 db_name 的权限，USE db_name 将会失败。

### ALTER DATABASE

```sql
ALTER DATABASE [db_name] db_attr ...
ALTER DATABASE db_name UPGRADE DATA DIRECTORY NAME
```

此语句更改数据库属性或升级数据库目录名称的编码。它需要数据库的 ALTER 权限。

对于第一种语法，允许的 db_attr 数据库属性值与 CREATE DATABASE 条目中列出的值相同。如果省略数据库名称，该语句将应用于默认数据库。如果没有默认数据库，则会发生错误。

UPGRADE DATA DIRECTORY NAME 语法用于从旧版本升级到 MySQL 5.1 或更高版本时。如果目录名称包含特殊字符，它会将数据库目录的名称重新编码为 MySQL 当前使用的文件系统编码。此语法是在 MySQL 5.1.23 中引入的。

### ALTER EVENT

```sql
ALTER
  [DEFINER = definer_name]
  EVENT event_name
  [ON SCHEDULE schedule]
  [ON COMPLETION [NOT] PRESERVE]
  [RENAME TO new_event_name]
  [ENABLE | DISABLE [ON SLAVE]]
  [COMMENT 'str']
  [DO event_stmt]
```

更改现有事件以具有给定的定义。RENAME TO 子句重命名事件。其他子句在 CREATE EVENT 条目中进行了描述。你必须拥有事件所属数据库的 EVENT 权限。（在 MySQL 5.1.12 之前，你必须拥有 SUPER 权限或者是事件的定义者。）
ALTER EVENT 是在 MySQL 5.1.6 中引入的。

### ALTER FUNCTION, ALTER PROCEDURE

```sql
ALTER {FUNCTION | PROCEDURE} routine_name [characteristic] ...

characteristic:
  [NOT] DETERMINISTIC
  | LANGUAGE SQL
  | SQL SECURITY {DEFINER | INVOKER}
  | COMMENT 'str'
```

这些语句更改存储例程的特性。特性在 CREATE FUNCTION 和 CREATE PROCEDURE 语句的条目中进行了描述。
从 MySQL 5.0.3 开始，这些语句需要给定例程的 ALTER ROUTINE 权限。

### ALTER SERVER

```sql
ALTER SERVER server_name OPTIONS { option [, option] ...}
```

修改名为 server_name 的 FEDERATED 表服务器定义，并更新 mysql.servers 表中的相应行。省略的选项将保留其先前的值。你必须拥有 SUPER 权限。
参见 CREATE SERVER 中 OPTIONS 子句的允许值描述。此语句是在 MySQL 5.1.15 中引入的。

### ALTER TABLE

```sql
ALTER [IGNORE] TABLE tbl_name action [, action] ...
```

ALTER TABLE 允许你重命名表或修改其结构。要使用它，请指定表名以及要在表上执行的一个或多个操作。IGNORE

