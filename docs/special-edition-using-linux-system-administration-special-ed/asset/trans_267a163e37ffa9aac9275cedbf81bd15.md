

| 选项 | 适用程序 | 说明 |
|---|---|---|
| `--socket=<socket文件>` | `mysqld, mysql, mysqladmin` | 用于连接的套接字文件。 |
| `--table` | `mysql` | 以表格格式生成输出。 |
| `--timeout=<秒>` | `mysqladmin` | 以秒为单位指定连接服务器的超时时间。 |
| `--user=<用户>` | `mysql, mysqladmin` | 连接时使用的用户（默认为当前登录用户）。 |
| `--user=<用户>` | `mysqld` | 以指定用户身份运行守护进程。 |
| `--vertical` | `mysql` | 以垂直方式生成行输出。 |

## 数据库管理

管理 MySQL 数据库包含以下几项任务：

- 启动和停止服务器
- 连接到服务器
- 创建和删除数据库与表
- 使用 SQL 与数据库交互
- 备份数据库
- 管理用户和权限

### 启动和停止服务器

`mysqld` 守护进程通过 `safe_mysqld` 脚本启动。该脚本会检查系统状态，并确保在调用 `mysqld` 守护进程之前，系统的环境变量已正确设置。

要启动服务器，只需使用不带任何参数的命令：

```sh
# /usr/local/bin/safe_mysqld &
```

末尾的与符号（`&`）会在后台运行该程序，这样 MySQL 守护进程便已启动，同时你仍可使用自己的 shell。

要停止 mysqld，请使用 mysqladmin 命令：

```sh
# /usr/local/bin/mysqladmin -u root --password=<密码> shutdown
```

### 连接到服务器

与正在运行的 MySQL 服务器交互最直接的方式是使用 `mysql` 客户端，它是 MySQL 软件包的一部分。要连接到服务器，请使用以下命令：

```text
# /usr/local/bin/mysql -u <用户名> --password=<密码>
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1 to server version: 3.22.30

Type 'help' for help.

mysql>
```

在命令提示符下，所有发给 SQL 服务器的命令都必须以分号或 `\g` 组合结尾。客户端处理但不会发送到服务器的任何命令不需要以分号或 `\g` 结尾，例如 `help` 命令，它只是显示客户端的本地帮助信息：

```text
mysql> help

MySQL commands:
help    (\h)    Display this text
?       (\h)    Synonym for `help`
clear   (\c)    Clear command
connect (\r)    Reconnect to the server. Optional arguments are db and host
edit    (\e)    Edit command with $EDITOR
exit    (\q)    Exit mysql. Same as quit
go      (\g)    Send command to mysql server
ego     (\G)    Send command to mysql server; Display result vertically
print   (\p)    Print current command
quit    (\q)    Quit mysql
rehash  (\#)    Rebuild completion hash
status  (\s)    Get status information from the server
use     (\u)    Use another database. Takes database name as argument

Connection id: 1 (Can be used with mysqladmin kill)

mysql>
```

要断开与服务器的连接，请使用 `\q` 命令：

```text
mysql> \q
Bye
```

或者，你也可以使用 Ctrl+D 关闭客户端并断开与服务器的连接。

### 创建和删除数据库与表

使用 MySQL 创建数据库是通过 mysqladmin 工具完成的：

```sh
# /usr/local/bin/mysqladmin -u <用户> --password=<密码> create <数据库名称>
```

例如，要创建一个名为 mydbase 的数据库，请使用以下命令：

```sh
# /usr/local/bin/mysqladmin -u root --password=<密码> create mydbase
Database "mydbase" created.
```

要删除已创建的数据库，同样使用 mysqladmin 命令：

```sh
# /usr/local/bin/mysqladmin -u <用户> --password=<密码> drop <数据库名称>
```

> **警告**
>
> 当你删除数据库时，`mysqladmin` 会提示你确认是否真的要删除该数据库。此时务必小心。如果你确认删除该数据库，数据库中的所有表及其包含的数据都将被删除，并且只能从备份中恢复。除非你完全确定不再需要其中包含的数据，否则不要在没有备份其内容的情况下删除数据库。

创建数据库后，必须先使用 `mysql` 客户端连接到服务器：

```sh
# mysql -u <用户名> --password=<密码>
```

接下来，使用 USE 命令选择要使用的数据库：

```sql
mysql> USE <数据库名称>;
Database changed
```

例如，要使用 mydbase 数据库，请使用以下命令：

```sql
mysql> USE mydbase;
```

如果你不确定要使用的数据库名称，可以使用 SHOW DATABASES 命令：

```sql
mysql> SHOW DATABASES;
```

| Database |
|----------|
| mydbase  |
| mysql    |
| test     |

3 rows in set (0.00 sec)

连接到数据库后，可以使用 CREATE TABLE 命令创建表，其一般形式为：

```sql
mysql> CREATE TABLE <表名称> (<字段名> <字段类型>, <字段名> <字段类型>,
<字段名> <字段类型> ...);
```

由于 MySQL 在收到分号之前不会将命令发送到服务器，因此你实际上可以将一条长命令拆分为多行：

```sql
mysql> CREATE TABLE <表名称> (
    -> <字段名> <字段类型>,
    -> <字段名> <字段类型>,
    -> <字段名> <字段类型> ...);
```

记录中的字段可以是表 24.5 中列出的类型之一。

**表 24.5：MySQL 数据类型**

| 数据类型 | 说明 |
|---|---|
| `TINYINT` | 整数，范围 -128–127 |
| `TINYINT UNSIGNED` | 整数，范围 0–255 |
| `SMALLINT` | 整数，范围 -32768–32767 |
| `SMALLINT UNSIGNED` | 整数，范围 0–65535 |
| `MEDIUMINT` | 整数，范围 -8388608–8388607 |
| `MEDIUMINT UNSIGNED` | 整数，范围 0–16777215 |
| `INT` | 整数，范围 -2147483648–2147483647 |
| `INT UNSIGNED` | 整数，范围 0–4294967295 |
| `INTEGER` | 整数，范围 -2147483648–2147483647 |
| `INTEGER UNSIGNED` | 整数，范围 0–4294967295 |
| `BIGINT` | 整数，范围 -9223372036854775808–9223372036854775807 |
| `BIGINT UNSIGNED` | 整数，范围 0–18446744073709551615 |
| `FLOAT` | 浮点数，范围 -3.402823466E+38–-1.175494351E-38 和 1.175494351E-38 到 3.402823466E+38，以及 0 |
| `DOUBLE` | 浮点数，范围 -1.7976931348623157E+308–-2.2250738585072014E-308 和 2.2250738585072014E-308 到 1.7976931348623157E+308，以及 0 |
| `DOUBLE PRECISION` | 浮点数，范围 -1.7976931348623157E+308–-2.2250738585072014E-308 和 2.2250738585072014E-308 到 1.7976931348623157E+308，以及 0 |
| `REAL` | 浮点数，范围 -1.7976931348623157E+308–-2.2250738585072014E-308 和 2.2250738585072014E-308 到 1.7976931348623157E+308，以及 0 |
| `DECIMAL` | 浮点数，范围 -1.7976931348623157E+308–-2.2250738585072014E-308 和 2.2250738585072014E-308 到 1.7976931348623157E+308，以及 0；该数字以字符串形式存储，而不是数值 |
| `NUMERIC` | 浮点数，范围 -1.7976931348623157E+308–-2.2250738585072014E-308 和 2.2250738585072014E-308 到 1.7976931348623157E+308，以及 0；该数字以字符串形式存储，而不是数值 |
| `DATE` | 日期，范围 1000-01-01–9999-12-31 |
| `DATETIME` | 日期和时间，范围 1000-01-01 00:00:00–9999-12-31 23:59:59 |
| `TIMESTAMP` | 时间戳，范围 1970-01-01 00:00:00 到 2037 年 |
| `TIME` | 时间，范围 -838:59:59 到 838:59:59 |
| `YEAR` | 年份，范围 1901 到 2155，以及 0000 |
| `CHAR(<长度>)` | 指定字符数的字符串，最多 255 个字符 |
| `VARCHAR(<最大长度>)` | 可变长度字符串，最大长度不超过指定字符数，最多 255 个字符 |
| `TINYBLOB` | 二进制大对象，最多 255 个字符 |
| `TINYTEXT` | 字符串，最多 255 个字符 |
| `BLOB` | 二进制大对象，最多 65535 个字符 |
| `TEXT` | 字符串，最多 65535 个字符 |
| `MEDIUMBLOB` | 二进制大对象，最多 16777215 个字符 |
| `MEDIUMTEXT` | 字符串，最多 16777215 个字符 |
| `LONGBLOB` | 二进制大对象，最多 4294967295 个字符 |
| `LONGTEXT` | 字符串，最多 4294967295 个字符 |
| `ENUM('值 1', '值 2', ...)` | 字符串，其值取自枚举列表中的某个值 |
| `SET('值 1', '值 2', ...)` | 字符串，其值为枚举列表中的零个或多个值 |

例如，以下表定义创建了一个名为 mytable 的表，包含四个字段：一个整数类型的 ID 字段、一个 255 字符字符串类型的姓氏字段、一个 255 字符字符串类型的名字字段，以及一个日期类型的出生日期字段：

```sql
mysql> CREATE TABLE mytable (
    -> ID INTEGER,
    -> last_name TINYTEXT,
    -> first_name TINYTEXT,
    -> birth_date DATE);
```

要删除已创建的表，可以使用以下命令：

```sql
mysql> drop table <表名称>;
```

> **警告**
>
> 当你删除表时，表中的所有数据都将被删除，并且只能从备份中恢复。除非你完全确定不再需要其中包含的数据，否则不要在没有备份其内容的情况下删除表。

