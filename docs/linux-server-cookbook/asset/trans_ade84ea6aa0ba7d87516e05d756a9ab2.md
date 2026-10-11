
| 选项 | 描述 |
| :--- | :--- |
| -e, -execute=name | 执行语句并退出。 |
| -h, -host=name | 连接到指定的主机，而不是使用 Unix Socket。 |
| --max-allowed-packet=num | 发送到服务器或从服务器接收的最大数据包长度。默认值为 16 MB，最大值为 1 GB。在导入大文件时使用此选项非常有用。 |
| -p, -password[=name] | 连接服务器时使用的密码。 |
| -P, -port=num | 用于连接端口，替代默认的 3306。 |
| --print-defaults | 输出客户端选项列表。 |
| -u, -user=name | 如果登录用户不是当前用户，则指定登录用户名。 |
| -v, -verbose | 显示更多信息。 |
| -V, -version | 输出版本信息并退出。 |

表 11.5：mariadb (mysql) 命令的常用选项

客户端可以以两种不同的模式工作：

-   **交互模式：** 连接到数据库服务器后，用户可以编写多条语句来操作服务器，并通过编写 QUIT 命令来退出客户端。
-   **一次性模式：** 客户端从标准输入读取一条或多条语句，将它们发送到服务器执行，然后退出客户端执行。

客户端允许指定一个参数来指定要使用的数据库。如果未指定，则与服务器的连接将不使用数据库，用户需要手动（使用 USE 语句）指定要操作的数据库。用户可以在数据库之间切换。

图 11.17 显示了以 root 用户身份从数据库服务器运行客户端是不必要的，并且也不需要提供用户名和密码。

```
root@ubuntu:~# mariadb
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.6.7-MariaDB-2ubuntu.1 Ubuntu 22.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

> 图 11.17：命令 mariadb 的输出示例

MariaDB（和 MySQL）允许使用 `CREATE USER` 语句创建用户。其简单语法如下：

```
CREATE [OR REPLACE] USER user_specification [authentication_options]
```

图 11.18 展示了如何创建名为 agonzalez 的用户，密码为 P@ssw0rd。

该用户将仅从 IP 192.168.122.226 通过该密码访问。

```
MariaDB [(none)]> CREATE USER agonzalez@192.168.122.226 IDENTIFIED BY 'P@ssw0rd';
Query OK, 0 rows affected (0.007 sec)
```

> 图 11.18：在 MariaDB 上创建用户的示例

客户端可以使用指定的认证参数并从允许的主机进行连接。可以指定字符 % 以接受来自所有源 IP 地址的连接。图 11.19 显示了从远程系统连接到数据库的示例：

```
[agonzalez@rhel ~]$ mysql -uagonzalez -pP@ssw0rd -h192.168.122.43
Welcome to the MariaDB monitor. Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.6.7-MariaDB-2ubuntu1.1 Ubuntu 22.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

> 图 11.19：连接到远程 MariaDB 服务器的示例

`SHOW DATABASES` 语句列出用户可用的数据库。创建的用户仅对名为 information_schema 的数据库具有读取权限，该数据库包含关于数据库和表的信息。其他权限需要由管理员授予。图 11.20 展示了列出可用数据库的输出示例。

![](img/863afa537de4eed7deb11978bfbfa90e_347_0.png)

管理员（或具有创建新数据库特定权限的用户）可以使用 **CREATE DATABASE** 语句创建数据库。创建数据库后，可以使用 **GRANT** 为现有用户分配权限。*图 11.21* 说明了数据库创建和权限分配。

![](img/863afa537de4eed7deb11978bfbfa90e_347_1.png)

为普通用户授予权限后，用户将能够看到被授予访问权限的数据库。*图 11.22* 说明了设置权限后的输出。

*图 11.22：MariaDB 输出示例*

用户可以使用 *USE* 语句后跟想要工作的数据库名称，在数据库之间切换。选择数据库后，用户可以在该数据库内部创建表或执行其他任务，例如查询现有表。*图 11.23* 显示了切换到数据库 `school` 并在其中创建表的示例。

```
MariaDB [(none)]> USE school;
Database changed
MariaDB [school]> CREATE TABLE students  (id INTEGER PRIMARY KEY, name CHAR(20),
lastname CHAR(50));
Query OK, 0 rows affected (0.024 sec)
```

图 11.23：MariaDB 输出示例

要列出数据库内部可用的表，使用的语句是 SHOW TABLES，它将列出当前数据库内部的表，如图 11.24 所示。

```
MariaDB [school]> SHOW TABLES;
+--------------------+
| Tables_in_school   |
+--------------------+
| students           |
+--------------------+
1 row in set (0.001 sec)
```

图 11.24：MariaDB 输出示例。

可以使用 DESCRIBE 语句后跟表名，以获取列列表及其类型定义。图 11.25 显示了使用之前创建的表时该语句的输出。

```
MariaDB [school]> DESCRIBE students;
+----------+-----------+------+-----+---------+-------+
| Field    | Type      | Null | Key | Default | Extra |
+----------+-----------+------+-----+---------+-------+
| id       | int(11)   | NO   | PRI | NULL    |       |
| name     | char(20)  | YES  |     | NULL    |       |
| lastname | char(50)  | YES  |     | NULL    |       |
+----------+-----------+------+-----+---------+-------+
3 rows in set (0.001 sec)
```

图 11.25：MariaDB 输出示例

图 11.26 展示了 INSERT 语句的使用以及主键的重要性。

```
MariaDB [school]> INSERT INTO students VALUES(1, "Alberto", "Gonzalez");
Query OK, 1 row affected (0.001 sec)

MariaDB [school]> INSERT INTO students VALUES(1, "John", "Doe");
ERROR 1062 (23000): Duplicate entry '1' for key 'PRIMARY'
```

*图 11.26：MariaDB 输出示例*

使用 **SELECT** 语句，可以获取表中的所有记录或部分信息，如 *图 11.27* 所示：

```
MariaDB [school]> SELECT * FROM students;
+------+------+----------+
| id | name | lastname |
+------+------+----------+
| 1 | Alberto | Gonzalez |
+------+------+----------+
1 row in set (0.002 sec)

MariaDB [school]> SELECT name FROM students;
+--------+
| name |
+--------+
| Alberto |
+--------+
1 row in set (0.002 sec)
```

*图 11.27：MariaDB 输出示例*

**MariaDB** 客户端包包含一个名为 **mariadb-dump** (*mysqldump*) 的命令，用于导出数据库（或特定表）的内容，以生成包含重建该数据库所需指令的文件。以下摘录展示了使用该命令生成的内容示例：

```
--
-- Table structure for table `students`
--
DROP TABLE IF EXISTS `students`;
/*!40101 SET @saved_cs_client = @@character_set_client */;
```

