

在 Unix 系统中，数据目录在安装过程中由 `mysql_install_db` 脚本初始化。如果您通过 RPM 包在 Linux 上安装 MySQL，或使用 DMG 包在 Mac OS X 上安装，则 `mysql_install_db` 会自动为您运行。否则，您需要自行运行该脚本。详情请参见附录 A。

`mysql_install_db` 的一个目的是在 `mysql` 数据库中设置授权表。在一台名为 `cobra.snake.net` 的服务器主机上，`mysql_install_db` 使用下表所示的账户初始化 `user` 表。

| 主机 | 用户 | 密码 | 超级用户权限 |
| :--- | :--- | :--- | :--- |
| localhost | root | | 全部 |
| 127.0.0.1 | root | | 全部 |
| cobra.snake.net | root | | 全部 |
| localhost | | 无 | |
| cobra.snake.net | | 无 | |

这些 `user` 表账户条目允许客户端程序以如下方式建立连接：

-   `root` 条目允许您使用 `localhost`、`127.0.0.1` 或 `cobra.snake.net` 作为主机名连接到本地 MySQL 服务器。例如，如果您在 `cobra.snake.net` 上登录并调用 `mysql` 程序，可以使用以下任一命令以 `root` 身份连接：
    -   `$ mysql -localhost -u root`
    -   `$ mysql -h cobra.snake.net -u root`
-   作为 `root`，您拥有所有权限，可以执行任何操作。
-   `user` 值为空白的条目是匿名账户。它们允许使用 `localhost` 或 `cobra.snake.net` 作为主机名且不使用用户名连接到本地 MySQL 服务器：
    -   `$ mysql -h localhost`
    -   `$ mysql -h cobra.snake.net`

匿名用户没有超级用户权限。

在 Windows 系统中，数据目录和 `mysql` 数据库在 MySQL 发行版中已预先初始化完成，其中的账户与 Unix 系统上的账户略有不同。Windows 下 `user` 表的条目如下表所示。

## 12.1 保护新的 MySQL 安装

| 主机 | 用户 | 密码 | 超级用户权限 |
| :--- | :--- | :--- | :--- |
| localhost | root | | 全部 |
| 127.0.0.1 | root | | 全部 |
| localhost | | 取决于版本 | |

这些 `user` 表账户条目允许客户端程序以如下方式建立连接：

-   您可以从本地主机以 `root` 身份连接。作为 `root`，您拥有所有权限，可以执行任何操作。
-   您可以从本地主机以匿名身份（无用户名）连接。对于当前版本的 MySQL，该账户没有超级用户权限。在 MySQL 5.0.36/5.1.16 之前，该账户拥有与 `root` 相同的超级用户权限，可以执行任何操作。在这种情况下，您可能希望撤销该账户的权限并为其分配密码，或者干脆完全删除该账户。

另一个授权表（`db` 表，此处未显示）包含权限信息，允许匿名用户使用 `test` 数据库或任何以 `test_` 开头的数据库。

本节的其余部分描述了如何设置 `root` 和匿名用户密码。示例使用了一组具有代表性的账户，但具体需要使用的 SQL 语句集合取决于您系统上实际存在的账户。

根据您分配密码的方式，您可能还需要告知服务器重新加载授权表以注意到变更。服务器使用授权表的内存副本执行访问控制。对于在 `user` 表中更改密码的某些方法，服务器可能不会识别到任何变更，因此您必须明确告知其重新读取表。

一种密码分配方法是连接到服务器并作为 `root`，确定哪些账户没有密码，并为每个账户使用 `SET PASSWORD` 语句。假设您连接到服务器后发现以下账户没有密码：

```bash
% mysql -u root
mysql> SELECT Host, User FROM mysql.user WHERE Password = '';
+----------------+-----------------+
| Host           | User            |
+----------------+-----------------+
| localhost      | root            |
| cobra.snake.net| root            |
| 127.0.0.1      | root            |
| localhost      |                 |
| cobra.snake.net|                 |
+----------------+-----------------+
```

可以使用 `SET PASSWORD` 语句为这些账户分配密码。每个语句都应使用 `'user_name'@'host_name'` 格式指定账户名称，使用您要修改的 `user` 表行中的用户和主机值。（如果用户值为空白，则 user_name 值为 `''`，即空字符串。）要为上面显示的账户设置 `root` 和匿名用户密码，请使用以下语句：

```sql
mysql> SET PASSWORD FOR 'root'@'localhost' = PASSWORD('rootpass');
mysql> SET PASSWORD FOR 'root'@'cobra.snake.net' = PASSWORD('rootpass');
mysql> SET PASSWORD FOR 'root'@'127.0.0.1' = PASSWORD('rootpass');
mysql> SET PASSWORD FOR ''@'localhost' = PASSWORD('anonpass');
mysql> SET PASSWORD FOR ''@'cobra.snake.net' = PASSWORD('anonpass');
```

`SET PASSWORD` 的替代方案是使用 `UPDATE` 直接修改 `user` 表。此方法可用于为所有具有特定用户值的账户指定密码，而不管其主机值如何，从而同时修改多个账户。要为所有 `root` 账户和所有匿名用户设置密码，请使用这些语句：

```sql
mysql> UPDATE mysql.user SET Password=PASSWORD('rootpass') WHERE User='root';
mysql> UPDATE mysql.user SET Password=PASSWORD('anonpass') WHERE User='';
mysql> FLUSH PRIVILEGES;
```

当您使用 `SET PASSWORD` 更改密码时，服务器会注意到您对授权表进行了更改，并自动重新读取它们以刷新表的内存副本。如果您使用 `UPDATE` 直接修改 `user` 表，则必须明确告知服务器重新加载表。这就是在 `UPDATE` 语句之后 `FLUSH PRIVILEGES` 语句的目的所在。

在 Windows 系统中，如果存在拥有与 `root` 相同超级用户权限的匿名用户账户，那么该账户的权限可能过大。如果您想保留该账户但取消其超级用户权限，可以撤销其权限。使用以下语句检查该账户拥有的权限：

```sql
mysql> SHOW GRANTS FOR ''@'localhost';
```

如果该账户没有超级用户权限，输出将如下所示，且您无需采取进一步措施：

![](img/0652954e48dbb3680551a9f43e3cddda_638_0.png)

如果该账户拥有超级用户权限，您看到的将是以下内容：

![](img/0652954e48dbb3680551a9f43e3cddda_638_1.png)

要撤销该账户的权限，请使用这些 `REVOKE` 语句：

```sql
mysql> REVOKE ALL ON *.* FROM ''@'localhost';
mysql> REVOKE GRANT OPTION ON *.* FROM ''@'localhost';
```

处理匿名用户账户的另一个选择是将其完全删除。如果您不需要这些账户，我们建议这样做。要删除这些账户，请使用 `DROP USER`：

```sql
mysql> DROP USER ''@'localhost';
mysql> DROP USER ''@'cobra.snake.net';
```

删除匿名用户账户的主要好处是，它显著简化了设置非匿名账户的任务。否则，您可能不得不处理第 13.2.3 节“权限谜题”中描述的奇怪现象。您可以阅读该节以了解此现象背后的详细信息。

对于 `REVOKE` 和 `DROP USER`，服务器会自动重新读取授权表，不需要 `FLUSH PRIVILEGES` 语句。

现在，您已经建立了账户密码（并在必要时重新加载了授权表），每次尝试连接到服务器都需要适当的密码。特别是，任何人如果不知道密码，都无法以 `root` 身份连接：

```bash
% mysql -u root
ERROR 1045 (28000): Access denied for user 'root'@'localhost'
(using password: NO)
% mysql -p -u root
Enter password: rootpass
mysql>
```

从这一点开始，连接到服务器时指定密码的需求不仅适用于 `mysql`，还适用于 `mysqladmin` 和 `mysqldump` 等其他程序。为了简洁起见，本章后续部分中的许多示例并未显示 `-u` 或 `-p` 选项。我们假设您会在连接服务器时根据需要添加这些选项。

### 12.1.2 为第二个服务器设置密码

前面的说明假设您在一个未安装过 MySQL 的系统上建立密码。但是，如果 MySQL 已经在一个位置安装，而您正在为同一台机器上第二个位置安装的新服务器设置密码，当您尝试无密码连接新服务器时，可能会发现它拒绝了该尝试并显示以下错误：

```bash
% mysql -u root
ERROR 1045 (28000): Access denied for user 'root'@'localhost'
(using password: YES)
```

嗯！为什么服务器说它收到了密码，而你并未指定？这通常表示您配置了一个包含之前安装的服务器访问密码的选项文件。`mysql` 找到该选项文件并自动使用其中列出的密码。为了覆盖此行为并明确指定“无密码”，请使用 `-p` 选项，并在 `mysql` 提示输入密码时按 Enter 键：

```bash
% mysql -p -u root
Enter password:      ← 只需按 Enter
```

