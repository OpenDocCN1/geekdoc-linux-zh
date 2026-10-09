
## 运行安全安装脚本

针对提示符，输入你为名为 **root** 的 MariaDB 用户设置的密码。

```
$ mysql -u root -p
Enter password:
...
MariaDB [(none)]> DELETE FROM mysql.user
                ->          WHERE user='';
Query OK, 2 rows affected (0.00 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> quit
Bye
```

作为上述两步的替代方案，你可以运行以下命令，该命令允许你为名为 **root** 的 MariaDB 用户分配密码，删除匿名用户，禁止远程 **MariaDB root** 登录，并删除 MariaDB 自带的测试数据库。

```
$ mysql_secure_installation
```

### ~/.my.cnf：配置 MariaDB 客户端

你可以使用 **~/.my.cnf** 文件来设置 MariaDB 客户端选项。以下示例展示了 Max 的 **~/.my.cnf** 文件。**[mysql]** 指定了 MariaDB 组。如果你的 Linux 和 MariaDB 用户名不同，user 行会很有用。当 Max 的 Linux 用户名为 **max** 时，将 **user** 设置为 **max** 并非必要。**password** 行将 Max 的 MariaDB 密码设置为 **mpasswd**。有了这个设置，Max 就不必在命令行上使用 **-p**；MariaDB 会自动让他登录。**database** 行指定了你要操作的 MariaDB 数据库的名称，这样你就不需要在 MariaDB 程序或会话的开头使用 USE 语句。在创建数据库（接下来会讲到）*之后*，不要向此文件添加 **database** 行，否则你将无法使用 MariaDB。

```
$ cat /home/max/.my.cnf
[mysql]
  user="max"
  password="mpasswd"
  database="maxdb"
```

由于此文件可能包含密码和其他敏感信息，设置此文件的权限，使其归属于该文件所在主目录的用户，且仅所有者可以读取该文件，可以使 MariaDB 数据更加安全。

### ~/.mysql_history：存储你的 MariaDB 历史

MariaDB 将执行的每条语句写入一个名为 **~/.mysql_history** 的文件。由于 MariaDB 可能会将密码写入此文件，设置此文件的权限，使其归属于该文件所在主目录的用户，且仅所有者可以读取该文件，可以使 MariaDB 数据更加安全。如果你不想存储 MariaDB 历史记录，请删除此文件并将其重新创建为指向 `/dev/null` 的符号链接。

```
$ rm ~/.mysql_history
$ ln -s /dev/null ~/.mysql_history
```

## 创建数据库

如果添加的 MariaDB 用户名与你的 Linux 用户名相同，你就不必在 MariaDB 命令行中指定用户名。在以下示例中，Max 作为名为 root 的 MariaDB 用户进行操作（`-u root`）。`p` 选项会使 MariaDB 提示输入密码。针对 `Enter password` 提示，Max 提供名为 root 的 MariaDB 用户的密码。如果名为 root 的 MariaDB 用户没有密码，请在提示时按 `RETURN`（回车）。

Max 使用 `CREATE DATABASE` 语句创建一个名为 `maxdb` 的数据库，并使用 `SHOW DATABASES` 语句显示所有数据库的名称。该命令显示了 `maxdb` 数据库的名称以及几个系统数据库。

```
$ mysql -u root -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 5
Server version: 5.5.31-MariaDB MariaDB Server

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> CREATE DATABASE maxdb;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| maxdb              |
| mysql              |
| performance_schema |
| test               |
+--------------------+
5 rows in set (0.00 sec)
```

如果你尝试创建一个已存在的数据库，MariaDB 将显示一条错误消息。

```
MariaDB [(none)]> CREATE DATABASE maxdb;
ERROR 1007 (HY000): Can't create database 'maxdb'; database exists
```

你必须告诉 MariaDB 你要操作的数据库名称。如果你没有提供此信息，你必须用数据库名称限定表名。例如，你需要指定 `maxdb` 数据库中的 `people` 表为 `maxdb.people`。当你在 `~/.my.cnf` 文件（第 1120 页）或 USE 语句中指定 `maxdb` 数据库时，你可以将同一个表称为 people。在以下示例中，Max 使用 USE 语句指定 `maxdb` 为他正在操作的数据库。一旦指定了数据库，MariaDB 就会在提示符中包含其名称。

```
$ mysql
MariaDB [(none)]> USE maxdb;
Database changed
MariaDB [maxdb]>
```

### 添加用户

在开始处理数据库之前，创建一个用户，这样你就不必作为名为 `root` 的 MariaDB 用户进行操作。你必须作为名为 `root` 的 MariaDB 用户来创建 MariaDB 用户。

接着之前的 MariaDB 会话，Max 添加了名为 `max` 的 MariaDB 用户，密码为 `mpasswd`。GRANT 语句赋予了 Max 操作（作为名为 `max` 的用户）`maxdb` 数据库所需的权限。在使用 MariaDB 解释器时，`Query OK` 表示前一条语句在语法上是正确的。在 SQL 语句中，必须用引号括住所有字符和日期字符串。

```
MariaDB [(none)]> GRANT ALL PRIVILEGES
    ON maxdb.* TO 'max'
    IDENTIFIED BY 'mpasswd'
    WITH GRANT OPTION;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> SELECT user, password
    FROM mysql.user;

+------+----------------------------------------+
| user | password                               |
+------+----------------------------------------+
| root | *9604C589348F896B08593EADEC1B65315679FDD | ...
| max  | *3443255DD6C778E7CB4A0E4551425CE3AC0E16 | |
+------+----------------------------------------+
5 rows in set (0.00 sec)

MariaDB [(none)]> quit
Bye
```

在前面的示例中，设置好新用户后，Max 使用 SELECT 语句查询 mysql 数据库的 user 表，并显示 user 和 password 列。`password` 列显示加密后的密码。现在存在两个用户：`root` 和 `max`。Max 输入 quit 命令退出 MariaDB 解释器。

作为 MariaDB 用户 `max` 进行操作，Max 现在可以设置一个简单的数据库来追踪人员信息。他不需要在命令行上使用 `-u` 选项，因为他的 Linux 用户名和 MariaDB 用户名相同。

# LPI 示例

本节跟随 Max 操作 MariaDB。你必须按照第 1119 页“设置 MariaDB”部分描述的步骤删除匿名用户，并按照第 1122 页“添加用户”部分描述的步骤创建 **maxdb** 数据库并添加名为 **max** 的 MariaDB 用户。如果你不遵循这些步骤，你将无法按照本节所述使用 MariaDB。

## 登录

在你能够交互式使用 MariaDB 之前，必须先登录到 MariaDB。

你可以在 `~/.my.cnf` 文件（第 1120 页）中指定 MariaDB 用户名，或者使用命令行中的 `--user (-u)` 选项。如果你没有通过这些方式中的任何一种指定用户，MariaDB 将假设你的 MariaDB 用户名与你的 Linux 用户名相同。本节的示例假设 Max 以 **max** 身份登录到 MariaDB（并且没有在 `~/.my.cnf` 文件中指定用户名）。

如果 MariaDB 账户有密码，你必须指定该密码才能登录。你可以在 `~/.my.cnf` 文件中指定密码，或者使用命令行中的 `--password (-p)` 选项。如果 Max 没有在 `~/.my.cnf` 文件中指定密码，他将使用以下命令登录到 MariaDB 交互式解释器：

```
$ mysql -p
Enter password: mpassword
…
```

如果他的密码如第 1120 页所示在 `~/.my.cnf` 文件中指定，Max 可以在不使用 `-p` 选项的情况下登录：

```
$ mysql
…
```

## 创建表

本节假设 Max 已在 `~/.my.cnf` 文件中指定了他的密码。

在你可以处理数据库之前，必须创建一个表来存储数据。一开始，Max 使用以下 CREATE TABLE 语句在 **maxdb** 数据库中创建一个名为 **people** 的表。该表有四个列。USE 语句指定了数据库的名称。

```
$ mysql
MariaDB [none]> USE maxdb;
Database changed

MariaDB [maxdb]> CREATE TABLE people (
->         name CHAR(10),
->         hired DATE,
->         store INTEGER,
->         hourly BOOL
->         );
Query OK, 0 rows affected (0.01 sec)
```

