
此命令表示要为出生日期字段分配一个新值。WHERE 子句用于指定应受影响的记录，其方式与 SELECT 命令中 WHERE 子句指定要显示的记录相同。结果是在正确字段中的出生日期：

```text
mysql> SELECT * FROM mytable;
+----+----------+------------+------------+
| ID | last_name | first_name | birth_date |
+----+----------+------------+------------+
|  2 | Sawyer   | Jane       | 1973-10-22 |
|  1 | Smith    | Joe        | 1969-06-14 |
|  3 | Walters  | Bob        | 1969-01-01 |
|  4 | Roberts  | Susan      | 1982-11-15 |
|  5 | Philips  | Peter      | 1999-02-01 |
+----+----------+------------+------------+
5 rows in set (0.00 sec)
```

请务必指定 WHERE 子句并正确指定。例如，如果未能指定 WHERE 子句，所有记录都将被更新：

```text
mysql> UPDATE mytable SET birth_date = '2000-02-02';
Query OK, 5 rows affected (0.00 sec)
Rows matched: 5  Changed: 5  Warnings: 0
```

```text
mysql> SELECT * FROM mytable;
+----+----------+------------+------------+
| ID | last_name | first_name | birth_date |
+----+----------+------------+------------+
|  2 | Sawyer   | Jane       | 2000-02-02 |
|  1 | Smith    | Joe        | 2000-02-02 |
|  3 | Walters  | Bob        | 2000-02-02 |
|  4 | Roberts  | Susan      | 2000-02-02 |
|  5 | Philips  | Peter      | 2000-02-02 |
+----+----------+------------+------------+
5 rows in set (0.00 sec)
```

你可以通过列出所有用逗号分隔的字段来指定要更新的多个字段：

```text
mysql> UPDATE mytable SET last_name = 'Kent', first_name = 'Clark' WHERE ID = 5;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

```text
mysql> SELECT * FROM mytable;
+----+----------+------------+------------+
| ID | last_name | first_name | birth_date |
+----+----------+------------+------------+
|  2 | Sawyer   | Jane       | 2000-02-02 |
|  1 | Smith    | Joe        | 2000-02-02 |
|  3 | Walters  | Bob        | 2000-02-02 |
|  4 | Roberts  | Susan      | 2000-02-02 |
|  5 | Kent     | Clark      | 2000-02-02 |
+----+----------+------------+------------+
5 rows in set (0.00 sec)
```

你还可以指定多个条件来定义要更新的记录：

```text
mysql> UPDATE mytable SET ID = 10 WHERE last_name = 'Kent' and first_name = 'Clark';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

```text
mysql> SELECT * FROM mytable;
+----+----------+------------+------------+
| ID | last_name | first_name | birth_date |
+----+----------+------------+------------+
|  2 | Sawyer   | Jane       | 2000-02-02 |
|  1 | Smith    | Joe        | 2000-02-02 |
|  3 | Walters  | Bob        | 2000-02-02 |
|  4 | Roberts  | Susan      | 2000-02-02 |
| 10 | Kent     | Clark      | 2000-02-02 |
+----+----------+------------+------------+
5 rows in set (0.00 sec)
```

## 备份你的数据库

要备份你的数据库，请锁定表，使其无法被更改，然后备份 /usr/local/var/ 目录中包含你数据库文件的文件。在 /usr/local/var/ 目录中，你会为创建的每个数据库找到一个子目录。该目录包含使数据库正常运行所需的全部文件。你应该按如下方式一次备份一个数据库：

1. 运行 mysql 并连接到你要备份的数据库。例如，要备份本书中用作示例的 mydatabase 数据库，请使用以下命令：

   ```text
   # /usr/local/bin/mysql -u <user name> --password=<password>
   Welcome to the MySQL monitor. Commands end with ; or \g.
   Your MySQL connection id is 12 to server version: 3.23.20

   Type 'help' for help.

   mysql> use mydatabase;
   Reading table information for completion of table and column names
   Database changed
   mysql>
   ```

2. 锁定所有表以仅允许读取。这将使用户能够继续查询数据库，同时确保在备份表时不向表写入新数据。要锁定表以供读取，请使用 LOCK TABLES 命令：

   ```text
   mysql> LOCK TABLES <table name> READ, <table name> READ, ...;
   ```

   锁定你计划备份的数据库中的所有表。对于 mydatabase 数据库，我们只有一个表：

   ```text
   mysql> LOCK TABLES mytable READ;
   Query OK, 0 rows affected (0.00 sec)
   ```

3. 备份 /usr/local/var/mydatabase/ 目录中的所有文件。理想情况下，你应该快速将它们复制到另一个位置，该位置随后可以通过常规系统备份备份到磁带或其他备份介质。通过这样做，你可以快速解锁表，以便数据库恢复正常运行。

4. 使用 UNLOCK TABLES 命令解锁表：

   ```text
   mysql> UNLOCK TABLES;
   Query OK, 0 rows affected (0.00 sec)
   ```

你可以自动化此过程，以便自动备份你的数据库。例如，你可以安排将数据库文件复制到 /backups 目录，然后将 /backups 目录包含在常规系统备份中。

以下脚本将在 mydatabase 数据库中锁定表，复制相关文件，然后解锁表：

```sh
#!/bin/sh

/usr/local/bin/mysql --user=<user name> --password=<password> --database=mydatabase --execute='LOCK TABLES mytable READ'
cp /usr/local/var/mysql/mydatabase/* /backups
/usr/local/bin/mysql --user=<user name> --password=<password> --database=mydatabase --execute='UNLOCK TABLES'
```

在合理的位置（例如 /usr/local/bin/）创建此脚本，并为其指定一个描述性名称，例如 backupmysql。使脚本可执行：

```sh
# chmod 755 /usr/local/bin/backupmysql
```

然后，你可以使用 crond 安排脚本定期运行，如第 7 章“计划任务”中所述。例如，要每天下午 11:00 运行此脚本一次，请将以下条目添加到 root 用户的 crontab 文件中：

```cron
* 23 * * * /usr/local/bin/backupmysql
```

## 管理用户和权限

MySQL 允许使用你在 MySQL 授权表中创建的用户帐户来控制对数据库和表的访问。

你可以在四个级别上创建用户帐户并分配系统访问权限：

- **全局：** 适用于所有数据库的权限
- **数据库：** 适用于特定数据库中所有表的权限
- **表：** 适用于特定表中所有列的权限
- **列：** 适用于给定表中单个列的权限

GRANT 语句使你能够授予访问权限，其通用形式如下：

```text
mysql> GRANT <privilege>, <privilege>, ... ON <object to which privileges apply>
    -> TO <user name> IDENTIFIED BY <password>, <user name> IDENTIFIED BY <password>,
...
```

可能的权限如表 24.7 所示。

**表 24.7 MySQL 访问权限**

| 权限 | 描述 |
|---|---|
| `ALL PRIVILEGES` | 授予对所有操作的超级用户访问权限。 |
| `ALTER` | 授予使用 ALTER 命令的权限。 |
| `CREATE` | 授予使用 CREATE 命令的权限。 |
| `DELETE` | 授予使用 DELETE 命令的权限。 |
| `DROP` | 授予使用 DROP 命令的权限。 |
| `FILE` | 授予执行文件访问的权限。 |
| `INDEX` | 授予对表建立索引的权限。 |
| `INSERT` | 授予使用 INSERT 命令的权限。 |
| `PROCESS` | 授予查看服务器中活动线程列表的权限。 |
| `RELOAD` | 授予发出 reload、refresh 和 flush 命令的权限。 |
| `SELECT` | 授予使用 SELECT 命令的权限。 |
| `SHUTDOWN` | 授予关闭服务器的权限。 |
| `UPDATE` | 授予使用 UPDATE 命令的权限。 |
| `USAGE` | 不授予任何权限。 |

所授予权限的范围由 ON 子句决定，如下所示：

- 要授予全局权限，请使用以下 ON 子句：`ON *.*`。
- 要授予数据库权限，请使用以下 ON 子句：`ON <database name>.*`。或者，使用 `USE <database name>` 连接到所需数据库，然后使用以下 ON 子句：`ON *`。
- 要授予表权限，请使用以下 ON 子句：`ON <database name>.<table name>`。或者，使用 `USE <database name>` 连接到相关数据库，然后使用以下 ON 子句：`ON <table name>`。
- 要授予列权限，请在 ON 子句中指定表名称，然后在权限列表中指定列和权限的列表：`GRANT <privilege> <column name>, <privilege> <column name>, ... ON <database name>.<table name>`。

TO 子句指定被授予权限的用户。用户名可以通过以下几种方式指定：

- **`<user name>`**：对应从任何主机连接的用户。
- **`<user name>@%`**：对应从任何主机连接的用户。
- **`<user name>@<host name>`**：对应从特定主机连接的用户。
- **`<user name>@localhost`**：对应从服务器机器本身连接的用户。
