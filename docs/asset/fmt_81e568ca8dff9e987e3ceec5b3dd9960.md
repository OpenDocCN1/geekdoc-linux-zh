
系统变量可以存在于两个级别：全局和会话特定。全局变量影响服务器整体的运行。会话特定变量仅影响服务器如何处理特定的客户端连接。对于在两个级别都存在的变量，全局值用于初始化相应的会话变量。这只在新客户端连接开始时发生；在连接期间更改全局变量不会影响客户端相应会话变量的当前值。

系统变量可以同时具有全局和会话形式，仅具有全局形式，或仅具有会话形式：

- 表示默认 SQL 模式的 `sql_mode` 系统变量是一个在会话和会话级别都存在的变量的示例。SQL 模式影响服务器处理 SQL 语句的几个方面。每个客户端连接时，它获得自己会话特定的 `sql_mode` 变量，该变量初始值与全局变量相同。任何客户端都可以修改其会话变量的值，以改变服务器对其自身连接的行为，而不影响服务器处理其他客户端的方式。具有 `SUPER` 权限的客户端也可以更改全局 `sql_mode` 变量。新的全局值用于初始化在更改后连接的客户端的会话变量。

- `key_buffer_size` 系统变量是一个仅全局变量的示例。它控制缓冲 MyISAM 表索引内容的默认键缓存的大小。这个键缓存由所有客户端共享，因此没有理由为每个客户端拥有会话值。

某些变量仅存在于会话级别。`autocommit`（自动提交）变量就是其中之一。每个客户端默认启用自动提交模式，但可根据需要将其禁用。

附录 D “系统、状态和用户参考”列出了所有系统变量，并指明了哪些变量可以在启动时和运行时进行设置。以下讨论介绍了检查系统变量和设置其值的语法。

### 12.6.1.1 检查系统变量值

要查看系统变量的当前值，请使用 `SHOW VARIABLES`：

```sql
mysql> SHOW VARIABLES;
| Variable_name            | Value    |
+-------------------------+----------+
| auto_increment_increment | 1        |
| auto_increment_offset    | 1        |
| autocommit               | ON       |
| automatic_sp_privileges  | ON       |
| back_log                 | 50       |
| basedir                  | /usr/local/mysql |
| big_tables               | OFF      |
| ...
```

使用 `LIKE` 子句，您可以将输出限制为变量名称与给定 SQL 模式匹配的行：

```sql
mysql> SHOW VARIABLES LIKE 'key%';
| Variable_name              | Value    |
+----------------------------+----------+
| key_buffer_size            | 8388572  |
| key_cache_age_threshold    | 300      |
| key_cache_block_size       | 1024     |
| key_cache_division_limit   | 100      |
+----------------------------+----------+
```

从 MySQL 5.0.2 开始，可以使用 `WHERE` 子句来指定用于选择行的一般条件。以下语句查找设置小于 60 秒的超时值：

```sql
mysql> SHOW VARIABLES
    -> WHERE Variable_name LIKE 'timeout%' AND Value < 60;
| Variable_name              | Value    |
+----------------------------+----------+
| connect_timeout            | 10       |
| innodb_lock_wait_timeout   | 50       |
| innodb_rollback_on_timeout | OFF      |
| net_read_timeout           | 30       |
| table_lock_wait_timeout    | 50       |
+----------------------------+----------+
```

如果存在会话值，`SHOW VARIABLES` 将返回每个变量的会话值；否则返回全局值。若要专门请求全局或会话变量的值，请在语句中添加 `GLOBAL` 或 `SESSION`：

* `SHOW GLOBAL VARIABLES;`

* `SHOW SESSION VARIABLES;`

`LOCAL` 是 `SESSION` 的同义词。

`mysqladmin variables` 命令显示服务器全局系统变量的当前值。

可以使用 `@GLOBAL.var_name` 语法选择全局变量的个别值，或使用 `@SESSION.var_name` 或 `@LOCAL.var_name` 选择会话变量的值。如果在不带级别限定符的情况下使用 `@var_name` 语法，若存在会话变量则使用会话变量，否则使用全局值。

`@` 语法是通用的，可用于 `SET`、`SELECT` 或其他 SQL 语句：

```sql
SELECT 'Default storage engine:', @@storage_engine;
```

大多数仅属于会话的变量根本不会通过 `SHOW VARIABLES` 显示，但你可以通过名称访问它们的值：

```sql
SELECT @@autocommit, @@warning_count;
```

从 MySQL 5.1.12 开始，你还可以查询名为 `GLOBAL_VARIABLES` 和 `SESSION_VARIABLES` 的 `INFORMATION_SCHEMA` 表来获取系统变量信息。

### 12.6.1.2 在服务器启动时设置系统变量

许多全局系统变量可以在服务器启动时进行设置。有两种语法可以实现此操作：

- 您可以将变量名视为选项名并直接设置它。例如，`max_connections` 变量控制最大同时客户端连接数。若要将其设置为 200，您可以在 `mysql` 命令行上使用该选项来实现：

  - `$ mysql --max_connections=200`

  您还可以使用以下语法在选项文件中设置该变量：

  ```ini
  [mysql]
  max_connections=200
  ```

变量作为选项语法的另一个特性是，下划线可以用破折号表示，从而使变量引用看起来更像其他选项。在命令行上，请这样设置变量：

```bash
$ mysqld --max-connections=200
```

在选项文件中，请这样设置：

```ini
[mysqld]
max-connections=200
```

- 您可以使用 `--set-variable` 或 `-O` 选项在服务器启动时设置变量。这种语法较旧，已弃用，但目前仍受支持。在命令行上，请这样设置变量：

```bash
$ mysqld --set-variable=max_connections=200
$ mysqld -O max_connections=200
```

在选项文件中，只允许使用长选项形式：

```ini
[mysqld]
set-variable=max_connections=200
```

通常，在选项文件中设置系统变量比在命令行上更方便，因为你不需要每次启动服务器时都记得设置它们。对于表示缓冲区大小或长度的变量，如果指定为不带后缀的数字，值可以是字节；或者可以使用后缀 ‘K’、‘M’ 或 ‘G’ 来指定，分别表示千字节、兆字节或吉字节。后缀不区分大小写，因此你也可以使用 ‘k’、‘m’ 或 ‘g’。

某些系统变量不能直接通过启动选项进行设置。在这种情况下，通常会有相关的选项。例如，你不能在启动时直接设置 `storage_engine` 变量，但可以改用 `--default-storage-engine` 选项。附录 D 指明了哪些全局系统变量可以直接设置。对于不能直接设置的变量，如果存在相关选项，附录将列出用于设置该变量的相关选项。

### 12.6.1.3 在运行时设置系统变量

运行时设置系统变量的语法取决于你想设置的是全局变量还是会话变量。要设置名为 `var_name` 的全局变量，请使用具有以下格式之一的 `SET` 语句：

```sql
SET GLOBAL var_name = value;
SET @@GLOBAL.var_name = value;
```

要设置会话变量，应用类似的语法：

```sql
SET SESSION var_name = value;
SET @@SESSION.var_name = value;
```

`LOCAL` 是 `SESSION` 的同义词。
