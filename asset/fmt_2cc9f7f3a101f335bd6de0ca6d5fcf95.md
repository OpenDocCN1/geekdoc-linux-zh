
```sql
mysql> SELECT * FROM name ORDER BY lastname;
+-----------+-----------+----------------------+-----------+-------+---------+
| firstname | lastname  | streetaddr           | city      | state | zipcode |
+-----------+-----------+----------------------+-----------+-------+---------+
| John      | Jones     | 18 Talbot Road NW    | Coventry  | NJ    | 54889   |
| Howard    | Manty     | 1515 Broadway        | New York  | NY    | 10028   |
| Chris     | Smith     | 167 Small Road       | Gig Harbor| WA    | 98999   |
+-----------+-----------+----------------------+-----------+-------+---------+
```

要根据城市名称对记录进行排序，可以使用以下命令：

```sql
mysql> SELECT * FROM name ORDER BY city;
+-----------+-----------+---------------------+------------+-------+---------+
| firstname | lastname  | streetaddr          | city       | state | zipcode |
+-----------+-----------+---------------------+------------+-------+---------+
| John      | Jones     | 18 Talbot Road NW   | Coventry   | NJ    | 54889   |
| Chris     | Smith     | 167 Small Road      | Gig Harbor | WA    | 98999   |
| Howard    | Manty     | 1515 Broadway       | New York   | NY    | 10028   |
+-----------+-----------+---------------------+------------+-------+---------+
```

你还可以添加 `ASC` 或 `DESC` 来指示排序顺序，因为 `MySQL` 否则并不保证数据显示顺序。既然你已经输入并显示了数据库记录，你可能会发现需要更改其中的一些记录。以下部分介绍了如何在 `mysql` 会话期间更新数据库记录。

## 更改表和记录

当你开始使用 `MySQL` 数据库时，你会发现需要对数据库表的结构和内容进行更改。以下部分介绍了如何更改 `MySQL` 表的结构以及更改 `MySQL` 记录的内容。如果你尚未连接到 `mysql` 会话，请输入以下命令（假设 `mysql` 用户名为 `root`）：

```text
$ mysql -u root -p
Enter password: ********
mysql>
```

要使用以下各节中显示的示例，通过输入以下内容将数据库（本例中为 `allusers`）识别为当前数据库：

```sql
mysql> USE allusers;
Database changed
```

### 更改 MySQL 表的结构

创建数据库表后，你不可避免地会想要对它们进行一些更改。本节介绍了如何在 `mysql` 会话期间使用 `ALTER` 命令执行以下任务：添加列、删除列、重命名列以及更改列的数据类型。

要在表的末尾添加一列以显示当前日期，请输入以下内容：

```sql
mysql> ALTER TABLE name ADD curdate TIMESTAMP;
```

上一行告诉 `mysql` 更改当前数据库中名为 `name` 的表（`ALTER TABLE name`），添加一个名为 `curdate` 的列（`ADD curdate`），并将该列的值分配为显示最后编辑日期（`TIMESTAMP` 数据类型）。如果你后来决定要删除该列，可以通过输入以下内容来删除它：

```sql
mysql> ALTER TABLE name DROP COLUMN curdate;
```

如果更改现有列的名称，可以使用 `ALTER` 的 `CHANGE` 选项来完成。示例如下：

```
mysql> ALTER TABLE name CHANGE city town varchar(20);
```

在上一个示例中，选择了名称表（`ALTER TABLE name`）将 `city` 列的名称更改为 `town`（`CHANGE city town`）。即使不更改列的数据类型，也必须输入列的数据类型（`varchar(20)`）。事实上，如果你只想更改列的数据类型，可以使用与上一个示例相同的语法，但只需将列名重复两次即可（在这种情况下，`zipcode`）。示例如下：

```
mysql> ALTER TABLE name CHANGE zipcode zipcode INTEGER;
```

上一个示例将 `zipcode` 列的数据类型从之前的类型（`varchar`）更改为 `INTEGER` 类型。

> **注意：** 如果你第一次创建表（`CREATE TABLE` 命令）时指定了列，它会更改列的默认值。通过运行 `ALTER TABLE` 语句，如果你希望恢复该值，可以重新指定列的默认值。

## 更新和删除 MySQL 记录

你可以基于任何选择的值选择记录，并更新这些记录中的任何值。当你在 `mysql` 会话中时，可以使用 `UPDATE` 来更改选定表中的值。示例如下：

```
mysql> UPDATE name SET streetaddr = "933 3rd Avenue" WHERE firstname = "Chris";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1 Changed: 1 Warnings: 0
```

此示例尝试更新名称表（`UPDATE name`）。在此示例中，每条 `firstname` 列设置为 `"Chris"` 的记录，其 `streetaddr` 列的值将更改为 `"933 3rd Avenue"`。注意查询找到了一条匹配的行。该行也被更改，无需错误警告。你可以使用任何值的组合来匹配记录（使用 `WHERE`）并更改列值（使用 `SET`）。进行更改后，最好显示结果以确认更改是否符合预期。

若要删除整行（即一条记录），可以使用 `DELETE` 命令。例如，如果要删除 `firstname` 列的值为 `"Chris"` 的任何行，请键入以下内容：

```
mysql> DELETE FROM name WHERE firstname = "Chris";
Query OK, 1 row affected (0.00 sec)
```

下次显示该表时，应该没有名为 `Chris` 的记录。

## 添加和移除用户访问

有几种不同的方法可以控制用户对你的 `MySQL` 数据库的访问。首先，为每个访问你的 `MySQL` 数据库的用户分配用户名和密码。然后你可以使用 `mysql` 的 `GRANT` 和 `REVOKE` 命令来具体指定用户可以访问的数据库和表，以及用户对这些数据库和表拥有的权限。

> **警告：** 数据库服务器是黑客攻击的常见目标。虽然本章提供了一些授予访问权限的方向，但如果你允许通过 Internet 访问，则必须为服务器提供更严格的保护。请参阅 `MySQL` 手册（`/usr/share/doc/mysql-*/manual1.txt`）中“通用安全问题”部分，以获取有关保护你的 `MySQL` 服务器的更多信息。

### 添加用户并授予访问权限

尽管你已定义了用于创建数据库的用户账户（在本例中为 `root` 用户），但为了使数据库有用，你可能也希望允许其他用户访问。以下程序描述了如何向其他用户授予对 `MySQL` 数据库的特权。

> **注意：** 如果你正在将 `MySQL` 从 3.22 之前的版本升级，请运行 `mysql_fix_privilege_tables` 脚本。该脚本为你的数据库添加了新的 `GRANT` 功能。如果你不运行该脚本，你将无法访问数据库。

在此示例中，我正在添加一个名为 `bobby` 的用户，该用户可以登录到 `localhost` 上的 `MySQL` 服务器。`bobby` 的密码是 `i8yer2shuz`。（请记住，不一定需要一个名为 `bobby` 的 `Fedora` 或 `RHEL` 用户账户。因此，`localhost` 上任何拥有 `bobby` 密码的用户都可以登录到该 `MySQL` 账户。）
