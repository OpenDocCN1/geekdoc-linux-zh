
## SHOW COLUMNS
## SHOW CREATE DATABASE
## SHOW CREATE EVENT
## SHOW CREATE [FUNCTION | PROCEDURE]
## SHOW CREATE TABLE
## SHOW CREATE TRIGGER
## SHOW CREATE VIEW
## SHOW DATABASES
## SHOW ENGINE
## SHOW ENGINES
## SHOW ERRORS
## SHOW EVENTS
## SHOW [FUNCTION | PROCEDURE] STATUS
## SHOW GRANTS
## SHOW INDEX
## SHOW INNODB STATUS
## SHOW [MASTER | BINARY] LOGS
## SHOW MASTER STATUS
## SHOW MUTEX STATUS
## SHOW OPEN TABLES
## SHOW PRIVILEGES
## SHOW PROCESSLIST
## SHOW SLAVE HOSTS
## SHOW SLAVE STATUS
## SHOW STATUS
## SHOW TABLE STATUS
## SHOW TABLE TYPES
## SHOW TABLES
## SHOW TRIGGERS
## SHOW VARIABLES
## SHOW WARNINGS

各种 `SHOW` 语句提供有关数据库及其内部对象（如表或存储程序）的信息，或提供有关服务器运行的信息。其中一些语句接受可选的 `FROM db_name` 子句，允许你指定要显示信息的数据库。如果不存在该子句，则使用默认数据库。在支持使用 `FROM` 来指定表或数据库名称的每个语句中，可以使用 `IN` 作为同义词。

某些形式允许可选的 `LIKE 'pattern'` 子句，将输出限制为匹配该模式的值。*pattern* 被视为 SQL 模式，并且可以包含 *%* 或 *_* 通配符。

从 MySQL 5.0.2 开始，INFORMATION_SCHEMA 提供了另一种获取数据库元数据的方式，并且许多 INFORMATION_SCHEMA 表包含与 `SHOW` 语句显示的信息类似的信息。此外，支持 `LIKE` *'pattern'* 的那些 `SHOW` 语句可以改为使用 WHERE 子句来指定要显示的行。有关更多信息，请参阅 2.7 节，“获取数据库元数据”。

### SHOW BINLOG EVENTS

```sql
SHOW BINLOG EVENTS [IN 'file_name'] [FROM position]
    [LIMIT [skip_count,] show_count]
```

该语句用于在复制主服务器上显示二进制日志文件中的事件。事件大致对应于 SQL 语句。

此语句的输出包括以下列：

- **`Log_name`**
  - 二进制日志文件名。
- **`Pos`**
  - 事件在日志文件中的位置。
- **`Event_type`**
  - 事件类型，例如 Query（对于要执行的语句）。
- **`Server_id`**
  - 记录该事件的服务器 ID。
- **`End_log_pos`**
  - 日志文件中事件之后下一个字节的位置。
- **`Info`**
  - 事件信息，例如 Query 事件的语句文本。

此语句需要 REPLICATION SLAVE 权限。

### SHOW CHARACTER SET

```sql
SHOW CHARACTER SET [LIKE 'pattern' | WHERE where_expr]
```

显示服务器支持的字符集列表。可以包含 LIKE 子句，以仅显示名称匹配给定模式的字符集的信息。WHERE 子句将输出限制为满足给定表达式的行。

SHOW CHARACTER SET 的输出包括以下列：

- **`Charset`**
  - 简短的字符集名称。这是在 SQL 语句中使用的名称。
- **`Description`**
  - 描述性字符集名称。
- **`Default collation`**
  - 该字符集的默认排序规则名称。
- **`Maxlen`**
  - 字符集中“最宽”字符的长度，以字节为单位。对于多字节字符集，此值大于 1。对于非多字节字符集，所有字符都占用单个字节，因此值为 1。

### SHOW COLLATION

```sql
SHOW COLLATION [LIKE 'pattern' | WHERE where_expr]
```

显示每个字符集的可用排序规则列表。可以包含 LIKE 子句，以仅显示名称匹配给定模式的排序规则的信息。WHERE 子句将输出限制为满足给定表达式的行。

SHOW COLLATION 的输出包括以下列：

- Collation
  - 排序规则名称。
- Charset
  - 与该排序规则关联的字符集名称。
- Id
  - 排序规则 ID 号。
- Default
  - 如果该排序规则是其字符集的默认排序规则，则为 Yes，否则为空白。
- Compiled
  - 如果该排序规则已编译到服务器中，则为 Yes，否则为空白。
- Sortlen
  - 与内存成本因素相关，当使用该排序规则对值进行排序时，必须为内部字符串转换操作分配的内存量。

### SHOW COLUMNS

```sql
SHOW [FULL] COLUMNS {FROM | IN} tbl_name
    [(FROM | IN) db_name] [LIKE 'pattern' | WHERE where_expr]
```

显示给定表（从 MySQL 5.0.1 开始也包括视图）的列。输出仅包括你拥有一些权限的列。SHOW FIELDS 是 SHOW COLUMNS 的同义词。使用 FULL 关键字时，该语句会显示 Collation、Privilege 和 Comment 输出字段。可以包含 LIKE 子句，以仅显示名称匹配给定模式的列的信息。WHERE 子句将输出限制为满足给定表达式的行。

要指定包含该表的数据库，请使用 FROM db_name 子句，或者以 db_name.tbl_name 格式书写表名：

```sql
SHOW COLUMNS FROM president;
SHOW COLUMNS FROM president FROM samdb;
SHOW COLUMNS FROM samdb.president;
```

SHOW COLUMNS 的输出提供了表中每列的以下类型信息：

- Field
  - 列名。
- Type
  - 列数据类型。这可能包括跟随在类型名称后面的类型属性。
- Collation
  - 非二进制字符串列的排序规则名称，其他列则为 NULL。排序规则名称隐含了字符集名称。此信息仅在指定 FULL 关键字时显示。
- Null
  - 如果列可以包含 NULL 值，则为 YES。否则，从 MySQL 5.0.3 开始值为 NO，在此之前为空白。
- Key
  - 该列是否已建立索引。
- Default
  - 列的默认值。
- Extra
  - 关于该列的附加信息。对于具有 AUTO_INCREMENT 属性的列，此处显示 auto_increment，否则值为空白。
- Privileges
  - 你拥有的列权限。此信息仅在指定 FULL 关键字时显示。
- Comment
  - 列定义中任何 COMMENT 属性的值。此信息仅在指定 FULL 关键字时显示。

### SHOW CREATE

```sql
SHOW CREATE DATABASE [IF NOT EXISTS] db_name
SHOW CREATE EVENT event_name
SHOW CREATE FUNCTION func_name
SHOW CREATE PROCEDURE proc_name
SHOW CREATE TABLE tbl_name
SHOW CREATE TRIGGER trigger_name
SHOW CREATE VIEW view_name
```

SHOW CREATE obj_type 语句显示创建指定名称对象的 CREATE obj_type 语句。其中一些语句还显示有关对象的其他信息，例如创建时生效的 sql_mode 值。

对于 SHOW CREATE DATABASE，如果该语句包含 IF NOT EXISTS 子句，则输出的 CREATE DATABASE 语句也将包含此子句。

SHOW CREATE VIEW 在 MySQL 5.0.1 中引入，SHOW CREATE EVENT 在 MySQL 5.1.6 中引入，SHOW CREATE TRIGGER 在 MySQL 5.1.21 中引入。

### SHOW DATABASES

```sql
SHOW DATABASES [LIKE 'pattern' | WHERE where_expr]
```

显示服务器主机上可用的数据库。可以包含 LIKE 子句，以仅显示名称匹配给定模式的数据库的信息。WHERE 子句将输出限制为满足给定表达式的行。

如果你没有 SHOW DATABASES 权限，你将只看到你拥有任何访问权限的数据库。如果服务器使用 --skip-show-database 选项启动，如果你拥有 SHOW DATABASES 权限，你将看到所有数据库；否则你什么也看不到。

### SHOW ENGINE

```sql
SHOW ENGINE engine_name info_type
```

此语句显示有关存储引擎的信息。对于 InnoDB，支持以下语句变体：

- SHOW ENGINE INNODB STATUS
  - 显示 InnoDB 存储引擎内部操作的信息。此语句取代了 SHOW INNODB STATUS。它需要 PROCESS 权限（MySQL 5.1.24 之前需要 SUPER 权限）。
- SHOW ENGINE INNODB MUTEX
  - 显示有关 InnoDB 互斥锁的信息。此语句在 MySQL 5.1.2 中引入；它取代了 SHOW MUTEX STATUS。它需要 PROCESS 权限（MySQL 5.1.24 之前需要 SUPER 权限）。

### SHOW ENGINES

```sql
SHOW [STORAGE] ENGINES
```

显示服务器所知道的存储引擎。对于每个引擎，输出指示支持级别，并提供引擎特征的简要描述。此语句的输出包括以下列：

- Engine
  - 存储引擎名称（MyISAM、InnoDB 等）。
- Support
  - 引擎的支持级别：YES 表示受支持，NO 表示不受支持，DISABLED 表示受支持但在运行时被禁用，或者 DEFAULT 表示该存储引擎是默认引擎。默认引擎始终处于启用状态。

