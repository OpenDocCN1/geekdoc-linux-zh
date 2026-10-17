
```
mysql> ALTER TABLE names ADD curdate TIMESTAMP;
```

前面的示例指示 `mysql` 更改当前数据库中名为 `names` 的表（`ALTER TABLE names`），添加一个名为 `curdate` 的列（`ADD curdate`），并将该列的值分配为显示当前日期（`TIMESTAMP` data_type）。如果你之后决定删除该列，可以输入以下内容来删除它：

```sql
mysql> ALTER TABLE names DROP COLUMN curdate;
```

如果你想更改现有列的名称，可以使用 `ALTER` 的 `CHANGE` 选项来完成。以下是一个示例：

```sql
mysql> ALTER TABLE names CHANGE city town varchar(20);
```

在前面的示例中，选择 `names` 表（`ALTER TABLE names`）将 `city` 列的名称更改为 `town`（`CHANGE city town`）。必须输入列的数据类型（`varchar(20)`），即使你并不更改它。事实上，如果你只想更改列的数据类型，你只需使用与前面示例相同的语法，但将列名重复输入两次即可。以下是一个示例：

```sql
mysql> ALTER TABLE names CHANGE zipcode zipcode INTEGER;
```

前面的示例将 `zipcode` 列的数据类型从其以前的类型（`varchar`）更改为 `INTEGER` 类型。

#### 更新和删除 MySQL 记录

你可以基于任何选定的值选择记录，并更新这些记录中的任何值。当你在 `mysql` 会话中时，可以使用 `UPDATE` 来更改所选表中的值。以下是一个示例：

```sql
mysql> UPDATE names SET streetaddr = "933 3rd Avenue" WHERE firstname = "Chris";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

前面的示例尝试更新 `names` 表（`UPDATE names`）。在本例中，每个 `firstname` 列设置为 `"Chris"` 的记录，其 `streetaddr` 列的值都会被更改为 `"933 3rd Avenue"`。请注意，`Query` 找到了 1 行匹配项。该匹配行也被更改，无需错误警告。你可以使用任意值的组合来匹配记录（使用 `WHERE`）并更改你希望更改的列值（使用 `SET`）。在做出更改后，最好显示结果以确保更改按预期完成。要删除整行（即一条记录），可以使用 `DELETE` 命令。例如，如果你想删除 `firstname` 列值为 `"Chris"` 的任何行，可以输入以下内容：

```sql
mysql> DELETE FROM names WHERE firstname = "Chris";
Query OK, 1 row affected (0.00 sec)
```

下次你显示该表时，将不再有姓名为 Chris 的记录。

### 添加和移除用户访问权限

你可以使用多种不同方法来控制用户对你 MySQL 数据库的访问。首先，为每个访问你的 MySQL 数据库的用户分配一个用户名和密码。然后你可以使用 mysql 的 `GRANT` 和 `REVOKE` 命令，具体指示用户和主机计算机可以访问的数据库和表，以及它们对这些数据库和表的权限。

> **交叉引用：** 数据库服务器是黑客攻击的常见目标。虽然本章为授予 MySQL 服务器访问权限提供了一些指导，但如果你允许互联网访问，则必须为服务器提供更严格的保护。有关保护 MySQL 服务器的更多信息，请参阅 MySQL 手册中的 General Security Issues 部分（`/usr/share/doc/mysql*/manual.html`）。

#### 添加用户和授予访问权限

虽然你已定义了一个用于创建数据库的用户账户（本例中为 root 用户），但为了使数据库有用，你可能希望允许其他用户访问。以下程序描述了如何为你的 MySQL 数据库向其他用户授予权限。

> **注意：** 如果你正在从 3.22 之前的版本升级 MySQL，请运行 `mysql_fix_privilege_tables` 脚本。此脚本会为数据库添加新的 `GRANT` 功能。如果你不运行该脚本，你将无法访问数据库。

在本例中，我将添加一个名为 `bobby` 的用户，该用户可以从本地主机登录到 MySQL 服务器。`bobby` 的密码为 `i8yer2shuz`。（请记住，不一定需要一个名为 `bobby` 的 Red Hat Linux 用户账户。因此，本地主机上任何拥有 `bobby` 密码的用户都可以登录该 MySQL 账户。）

- 如果你尚未连接到 `mysql` 会话，请键入以下命令（假设 `mysql` 用户名为 `root`）：

```
# mysql -u root -p
Enter password: ******
mysql>
```

- 要创建名为 `bobby` 的用户和密码 `i8yer2shuz`，请按照以下方式使用 `GRANT` 命令：

```
mysql> GRANT USAGE ON *.*
-> TO bobby@localhost IDENTIFIED BY "i8yer2shuz";
```

在此时，某个人可以使用 `bobby` 的名称和 `i8yer2shuz` 密码从本地主机登录（`mysql -u bobby -p`）。但该用户没有权限处理任何数据库。接下来你需要授予权限。

- 若要授予 `bobby` 处理名为 `allusers` 的数据库的权限，你可以键入以下内容：

#### 撤销访问权限

您可以使用 `REVOKE` 命令撤销所授予的特权。若要撤销用户对特定数据库的所有特权，请遵循以下步骤：

1. 如果您尚未连接到 `mysql` 会话，请键入以下命令（假设 `mysql` 用户名为 `root`）：

```
mysql -u root -p
Enter password: ******
mysql>
```

2. 若要撤销用户 `bobby` 对 MySQL 服务器上名为 `allusers` 的数据库的所有特权，您可以键入以下内容：

```
mysql> REVOKE ALL PRIVILEGES ON allusers.*
    -> FROM bobby@localhost;
```

此时，`bobby` 不再拥有使用 `allusers` 数据库中任何表的特权。

3. 若要查看您刚刚授予的特权，您可以将 `mysql` 选择为当前数据库，然后选择 `db` 表，如下所示：

```
mysql> USE mysql;
Database changed
mysql> SELECT * FROM db WHERE db='allusers';
```

输出结果应显示名为 `bobby` 的用户不再被列在拥有 `allusers` 数据库访问权限的用户中。（结果可能只显示“Empty set”。）

### 检查和修复数据库

随着时间推移，数据库可能会损坏或低效地存储信息。MySQL 附带了一些用于检查和修复数据库的命令。`myisamchk` 和 `isamchk` 命令分别用于检查 MyISAM 和 ISAM 数据库表。

MySQL 默认使用 MyISAM 表。这些表默认存储在 `/var/lib/mysql/dbname` 目录中，其中 `dbname` 被替换为您使用的数据库名称。对于每个表，该目录中有三个文件。每个文件都以表名开头，并以以下三个后缀之一结尾：

- `.frm` 包含表的定义（或形式）

- `.MYI` 包含表的索引。

- `.MYD` 包含表的数据。

以下过程描述了如何使用 `myisamchk` 命令来检查您的 MyISAM 表。（检查 ISAM 表的过程相同，只是您使用 `isamchk` 命令代替。）

> 注意：在运行 `myisamchk` 进行修复之前，请务必备份您的数据库表。虽然 `myisamchk` 不太可能会损坏您的数据，但备份仍然是一个良好的预防措施。

1. 临时停止您的 MySQL 服务器，以 root 用户身份在终端窗口中键入以下内容：

```
/etc/init.d/mysql stop
```

2. 您可以一次检查所有或部分数据库表。第一个示例展示了如何检查“allusers”数据库中名为“names”的表。

```
myisamchk /var/lib/mysql/allusers/names.MYI
Checking MyISAM file: /var/lib/mysql/allusers/names.MYI
Data records:  5  Deleted blocks:  0
- check file-size
- check key delete-chain
- check record delete-chain
- check index reference
- check record links
```

您也可以按如下方式一次检查所有数据库中的表：
