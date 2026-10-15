
| Chris      | Smith     | 167 Small Road     | Gig Harbor | WA    | 98999 |
+------------+-----------+--------------------+------+-----------------+

```
若要根据城市名称对记录排序，可以使用以下命令：
```
```
mysql> SELECT * FROM name ORDER BY city;
+------------------------------------------------------+
| firstname | lastname | streetaddr | city | state | zipcode |
+------------------------------------------------------+
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54899 |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+------------------------------------------------------+
```

# 添加和移除用户访问权限

你有几种不同的方法可以控制用户对 MySQL 数据库的访问权限。首先，为每个访问 MySQL 数据库的用户分配用户名和密码。然后，你可以使用 `mysql` 的 `GRANT` 和 `REVOKE` 命令来特定指定主机可以访问的数据库和表，以及它们对这些数据库和表拥有的权限。

> 警告：数据库服务器是黑客攻击的常见目标。本章为授予 MySQL 服务器访问权限提供了一些方向，如果你允许互联网访问，则需要对服务器提供更严格的保护。请参阅 MySQL 参考手册（`info mysql`）以获取有关加固 MySQL 服务器的更多信息。

## 添加用户并授予访问

尽管你有一个用于创建数据库的用户账户（在本例中为 `root` 用户），但在创建数据库时，你可能还想允许其他用户访问。以下步骤描述了如何为其他用户授予 MySQL 数据库权限。

> 注意：如果你正在将 MySQL 升级到 3.22 之前的版本，请运行 `mysql_fix_privilege_tables` 脚本。该脚本为你的数据库添加新的 `GRANT` 功能。如果不运行它，你将被拒绝访问数据库。

在本例中，我正在添加一个名为 `bobby` 的用户，他可以从 `localhost` 登录 MySQL 服务器。`bobby` 的密码是 `i8yer2shuz`。（记住，不一定非要有名为 `bobby` 的 Fedora 或 RHEL 用户。因此，`localhost` 上的用户都可以登录该 MySQL 账户。）

1. 如果你尚未连接到 `mysql` 会话，请输入以下命令（假设你的 `mysql` 用户名为 `root`）：
```
$ mysql -u root -p
Enter password: ***********
mysql>
```
2. 要创建名为 `bobby` 的用户并设置 `i8yer2shuz` 密码，请使用 `GRANT` 命令：
```
mysql> GRANT USAGE ON *.* TO bobby@localhost IDENTIFIED BY "i8yer2shuz";
```
此时，有人可以使用用户名 `bobby` 和密码 `i8yer2shuz` 从 `localhost` 登录（`mysql -u bobby -p`）。但该用户将没有任何权限来操作任何数据库。接下来，你需要授予权限。

3. 要授予 `bobby` 操作名为 `allusers` 数据库的权限，请输入以下内容：
```mysql
mysql> GRANT DELETE, INSERT, SELECT, UPDATE ON allusers.* TO bobby@localhost;
```
在本例中，用户 `bobby` 被允许在 `localhost` 上登录 MySQL 服务器，并访问 `allusers` 数据库中的所有表（`USE allusers`）。对于该数据库，`bobby` 可以使用 `DELETE`、`INSERT`、`SELECT` 和 `UPDATE` 命令。

4. 要查看你刚刚授予的权限，请选择 `mysql` 作为当前数据库，然后选择 `db` 表：
```mysql
mysql> USE mysql;
Database changed
mysql> SELECT * FROM db WHERE db="allusers"
```
| Host | User | Select_priv | Insert_priv | Update_priv | Delete_priv |
|---|---|---|---|---|---|
| localhost | allusers | bobby | | | | |
输出显示了所有被专门授予 `allusers` 数据库权限的用户。这里只显示了部分输出，因为内容非常长。如果你不喜欢阅读折行的文本，可以开启一个非常宽的终端窗口来查看输出。该行中的其他权限将被设置为 N（无访问权限）。

## 撤销访问

你可以通过 `REVOKE` 命令来撤销权限。要撤销用户对特定数据库的所有权限，请使用以下步骤：

1. 如果你尚未连接到 `mysql` 会话，请输入以下命令（假设 `mysql` 用户名为 `root`）：
```
$ mysql -u root -p
Enter password: ******
mysql>
```
2. 要撤销名为 `bobby` 的用户使用你 MySQL 服务器上名为 `allusers` 数据库的权限，请输入以下内容：
```mysql
mysql> REVOKE ALL PRIVILEGES ON allusers.* FROM bobby@localhost;
```
此时，`bobby` 没有任何权限使用 `allusers` 数据库中的任何表。

3. 要查看你刚刚授予的权限，请选择 `mysql` 作为当前数据库，并按如下方式选择 `db` 表：
```mysql
mysql> USE mysql;
Database changed
mysql> SELECT * FROM db WHERE db="allusers";
```
输出应该显示用户 `bobby` 不再列为具有访问 `allusers` 数据库权限。（结果可能只显示 Empty set。）

## 备份数据库

你可以使用 `mysqldump` 命令备份你的 MySQL 数据库。以下命令将备份你所有的 MySQL 数据库。
```bash
# mysqldump -u root -p --opt --all-databases > /home/chris/all-databases
```
在这种情况下，本地系统上的所有数据库都被复制到 `/home/chris` 目录下的 `all-databases` 文件。你也可以使用 `mysqldump` 备份单个数据库、多个数据库或数据库内部的内容。请参阅 `mysqldump` 手页以获取更多信息。

## 检查和修复数据库

随着时间的推移，数据库可能会损坏或存储更多信息。MySQL 自带了一些你可以用来检查和修复数据库的命令。`mysisamchk` 命令可检查 MyISAM 数据库表。

MySQL 默认使用 MyISAM 表。（要使用不同的表类型，你可以在选择 MySQL 表时指定）。表存储在 `/var/lib/mysql/` 目录下，其中 `dbname` 被替换为名称。每个文件都以以下后缀之一开头：
- `.frm` 包含定义
- `.MYI` 包含索引
- `.MYD` 包含数据

以下步骤描述了如何使用 `mysisamchk` 检查和修复你的数据库。警告：在运行 `mysisamchk` 之前请备份你的数据库。虽然 `mysisamchk` 不可能损坏你的数据。

1. 通过输入以下内容停止 MySQL：
`/etc/init.d/mysql stop`
2. 你可以一次检查所有表。第一个示例显示了如何检查名为 `name` 的表：
```
# mysisamchk /var/lib/mysql/name.MYI
```
前面的示例显示了一个没有遇到错误的示例记录数据库。如果在上一个示例的输出中看到如下内容，则你需要修复数据库：
```
Checking MyISAM file: name.MYI
Data records: 5 Deleted blocks: 0
misamck: checking file-size: Size of datafile is: 89 Should be: 204
- check key-chain
- check record-chain
- check index reference
- check record links
```
