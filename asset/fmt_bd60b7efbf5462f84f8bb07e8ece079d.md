
## SET

```text
SET [OPTION] assignment [, assignment ] . . .

assignment: var_name = expr
```

`SET` 语句用于给系统变量、用户定义变量或存储程序局部变量赋值。附录 D“系统、状态和用户变量参考”提供了关于系统和用户定义变量的信息。第 E.2.2 节“声明语句”描述了存储程序局部变量的声明语法。`SET` 还用于一些杂项设置，将在本条目中稍后描述。

其他以 `SET` 开头的语句（`SET PASSWORD` 和 `SET TRANSACTION`）在本附录后面的独立条目中描述。

当使用 `SET` 给变量赋值时，每个赋值中的 `var_name` 是要赋值的变量，而 `expr` 是指示要赋给变量的值的表达式。`SET` 语句中的赋值运算符可以是 `=` 或 `:=`。

`SET` 可用于给使用 `@var_name` 语法命名的用户定义变量赋值：

```sql
SET @day = CURDATE(), @time = CURTIME();
```

`SET` 还可以给系统变量赋值，其中许多是动态的，可以在服务器运行时更改。动态系统变量存在于两个级别。全局系统变量适用于整个服务器，并影响所有客户端。会话系统变量（也称为局部系统变量）仅适用于给定的客户端连接。对于同时存在于两个级别的变量，当客户端连接时，该客户端的会话变量会从相应全局变量的值进行初始化。修改全局变量需要 `SUPER` 权限，但任何客户端都可以修改其自身的会话变量。

设置系统变量的语法有几种形式。要设置全局变量（例如，全局 `sql_mode` 值），请使用具有以下任一形式的语句：

```sql
SET GLOBAL sql_mode = 'ANSI_QUOTES';
SET @@GLOBAL.sql_mode = 'ANSI_QUOTES';
```

要设置会话变量，用 `SESSION` 替换 `GLOBAL`：

```sql
SET SESSION sql_mode = 'ANSI_QUOTES';
SET @@SESSION.sql_mode = 'ANSI_QUOTES';
```

你也可以使用 `LOCAL` 作为 `SESSION` 的同义词：

```sql
SET LOCAL sql_mode = 'ANSI_QUOTES';
SET @@LOCAL.sql_mode = 'ANSI_QUOTES';
```

如果不存在 `GLOBAL`、`SESSION` 或 `LOCAL` 中的任何一个，`SET` 语句将修改会话级变量：

```sql
SET sql_mode = 'ANSI_QUOTES';
SET @@sql_mode = 'ANSI_QUOTES';
```

要检查系统变量的值，请使用 `SHOW VARIABLES` 语句。你也可以通过使用 `SELECT` 获取单个系统变量的值：

```sql
SELECT @@GLOBAL.sql_mode, @@SESSION.sql_mode, @@LOCAL.sql_mode;
```

第 12.6.1 节“检查和设置系统变量值”进一步讨论系统变量的使用。

以下列表描述了可以用 `SET` 控制的杂项设置。

- `SET CHARACTER SET ({charset} | DEFAULT)`

  将 `character_set_client` 和 `character_set_results` 会话变量设置为指定的字符集，并将 `character_set_connection` 会话变量设置为 `character_set_database` 的值。这些变量会影响发送到服务器和从服务器发送的字符数据的转换。`ucs2`、`utf8` 或 `utf32` 的字符集值不起作用。

  `SET CHARACTER SET DEFAULT` 恢复默认字符集映射。

- `SET NAMES ({charset} | '{charset}' | DEFAULT)`

  将 `character_set_client`、`character_set_connection` 和 `character_set_results` 会话变量设置为指定的字符集，并将 `collation_connection` 设置为 `character_set_connection` 的默认排序规则。这些变量会影响发送到服务器和从服务器发送的字符数据的转换。`ucs2`、`utf8` 或 `utf32` 的字符集值不起作用。

  `SET NAMES DEFAULT` 恢复默认字符集映射。

## SET PASSWORD

```text
SET PASSWORD [FOR account] = PASSWORD('pass_val')
SET PASSWORD [FOR account] = OLD_PASSWORD('pass_val')
SET PASSWORD [FOR account] = 'encrypted_pass_val'
```

`SET PASSWORD` 更改 MySQL 账户的密码。除非你作为匿名用户连接，否则你始终可以更改自己的密码。要更改其他账户的密码，你必须拥有 `mysql` 数据库的 `UPDATE` 权限。

如果没有 `FOR` 子句，该语句为当前账户设置密码。如果使用 `FOR` 子句，它将为指定的账户设置密码，该账户应以 `'user_name'@'host_name'` 格式给出，如第 12.4.1.1 节“指定账户名称”中所述。

密码值 `'pass_val'` 应使用 `PASSWORD()` 进行标准加密，或使用 `OLD_PASSWORD()` 进行较旧（MySQL 4.1 之前）的加密。如果你不使用这两个函数中的任何一个，`'encrypted_pass_val'` 应作为已加密的密码字符串给出。

```sql
SET PASSWORD = PASSWORD('secret');
SET PASSWORD FOR 'paul' = PASSWORD('secret');
SET PASSWORD FOR 'paul'@'localhost' = PASSWORD('secret');
SET PASSWORD FOR 'bill'@'%.bigcorp.com' = PASSWORD('old-sneep');
```

## SET TRANSACTION

`SET [GLOBAL | SESSION] TRANSACTION ISOLATION LEVEL level`

该语句设置事务处理的隔离级别：

- 使用 `GLOBAL` 选项，它设置全局（整个服务器）隔离级别，该级别将成为此后连接的所有客户端的默认级别。

- 使用 `SESSION` 选项，它设置会话（客户端特定）隔离级别，该级别将成为当前会话内后续事务的级别。

- 如果没有任一选项，它仅为当前会话内的下一个事务设置隔离级别。

设置全局隔离级别需要 `SUPER` 权限。任何客户端都可以更改其自身的会话或下一事务隔离级别。由 `level` 指示的事务级别应是以下值之一：

- `READ UNCOMMITTED`

  即使其他事务尚未提交，事务也可以看到它们对行所做的修改。

- `READ COMMITTED`

  事务只能看到其他事务已提交的行修改。

- `REPEATABLE READ`

  如果一个事务两次执行给定的 `SELECT`，结果是可重复的。也就是说，即使其他事务在此期间更改或插入了行，它每次都会得到相同的结果。

- `SERIALIZABLE`

  此隔离级别类似于 `REPEATABLE READ`，但更完全地隔离事务：由一个事务选择的行在第一个事务完成之前不能由其他事务修改。此级别受 InnoDB 支持，但 Falcon 尚不支持。

`SET TRANSACTION` 语句适用于 InnoDB 和 Falcon 存储引擎。默认隔离级别为 `REPEATABLE READ`。非事务性存储引擎没有隔离级别。第 2.13.3 节“事务隔离”进一步讨论事务隔离和隔离级别。

## SHOW

- `SHOW BINLOG EVENTS`
- `SHOW CHARACTER SET`
- `SHOW COLLATION`

### SHOW COLUMNS

### SHOW CREATE DATABASE

### SHOW CREATE EVENT

### SHOW CREATE [FUNCTION | PROCEDURE]

### SHOW CREATE TABLE

### SHOW CREATE TRIGGER

### SHOW CREATE VIEW

### SHOW DATABASES

### SHOW ENGINE

### SHOW ENGINES

### SHOW ERRORS

### SHOW EVENTS

### SHOW [FUNCTION | PROCEDURE] STATUS

### SHOW GRANTS

### SHOW INDEX

### SHOW INNODB STATUS

### SHOW [MASTER | BINARY] LOGS

### SHOW MASTER STATUS

### SHOW MUTEX STATUS
