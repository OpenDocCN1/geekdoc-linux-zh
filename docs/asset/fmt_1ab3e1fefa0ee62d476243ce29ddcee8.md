
## 注意

别忘了将`database_name`、`password_table_name`、`username_field_name`、`password_field_name`、`group_table_name`和`group_field_name`替换为相应的具体信息。

- `Auth_MySQL`指令用于开启或关闭`mod_auth_mysql`。
- `Auth_MySQL_DB`指令指定数据库名称，该数据库包含由`Auth_MySQL_Password_Table`指定的密码表和由`Auth_MySQL_Group_Table`指定的组表。
- `Auth_MySQL_Username_Field`和`Auth_MySQL_Password_Field`指令指定用于在密码表中存储用户名和密码的字段名称。
- `Auth_MySQL_Group_Field`指令指定组名称字段。
- `Auth_MySQL_Empty_Passwords`设置为`off`，因为空密码不适合大多数认证需求。
- 使用`Auth_MySQL_Encrypted_Passwords`开启加密密码支持，并通过使用`Auth_MySQL_Encryption_Types`将加密类型设置为传统的 Unix 风格`Crypt_DES`。

## 注意

虽然你可以从`Plaintext`、`Crypt_DES`和`MySQL`加密类型中任选一种，但我从不推荐使用明文密码。由于`Auth_MySQL_Scrambled_Passwords`在大多数场景下并不适用，因此支持该功能的选项已被关闭。

- 由于允许一种“降级认证”方案（即如果一种方案未能允许用户访问，则可以使用另一种方案来允许访问）并非好主意，因此开启了`Auth_MySQL_Authoritative`指令。这告诉 Apache 忽略用于同一目录的所有其他认证方案。如果`mod_auth_mysql`无法允许用户访问受限目录，Apache 将简单地重新发出认证请求。
- 最后一个指令`Auth_MySQL_Non_Persistent`告诉 Apache 不要针对每个认证请求断开与数据库服务器的连接。针对每个请求断开连接意味着 Apache 必须为每个新的认证请求重新建立连接，这对性能不利。因此，建议使用默认值（`off`）。

3. 如果你将上述配置添加到`httpd.conf`中的`<Directory>`或`<Location>`容器内，你需要使用`/usr/local/apache/bin/apachectl restart`命令重启 Apache 服务器。另一方面，如果你在上述配置中使用了`.htaccess`文件，则无需重启服务器即可使用。

## 使用其他数据库进行用户认证

你可以使用 Postgres、IBM DB2、Oracle 或其他服务器作为数据库，而不是使用 MySQL 服务器来为 Apache 进行用户认证。虽然你可能找不到适用于你特定关系型数据库管理系统（RDBM）的 Apache 模块（如`mod_auth_mysql`），但你可以在`mod_perl`中使用`Apache::AuthDBI`模块（有关如何安装`mod_perl`的详细信息，请参阅第 16 章，该章讨论了`mod_perl`的使用）来与你的数据库服务器通信并执行用户认证。请按照以下步骤操作：

1. 确保已安装随你的数据库服务器包提供的所有必要库和头文件。通常，这意味着你需要为你的 RDBM 安装软件开发套件（SDK）。
2. 使用`perl -MCPAN -e 'install DBI'`命令安装最新版本的 DBI 模块。
3. 使用`perl -MCPAN -e 'install DBD:database'`命令安装 Perl（DBD）的相应数据库驱动器的最新版本。例如，要安装 IBM DB2 的数据库驱动器，你需要运行`perl -MCPAN -e 'install DBD::db2'`。
4. 使用`perl -MCPAN -e 'install Apache::AuthDBI'`命令安装最新版本的`Apache::AuthDBI`。
5. 创建一个数据库用户账户，供 Apache 连接数据库服务器使用。这不是用于访问系统（如 Linux 服务器本身）的账户。它是数据库引擎上的一个账户，授予 Apache 访问用户数据库及其表的权限。
6. 接下来，你需要创建前面“在 mysql 服务器中创建用户认证数据库”一节中讨论的`auth`数据库和`wwwuser`表。此外，务必使用本章后面“在任何 RDBM 中管理用户和组”一节中讨论的`manage_users.pl`脚本创建一个或多个测试用户。
7. 在`httpd.conf`中添加以下行：

```
PerlModule Apache::AuthenDBI
```

这告诉 Apache 你希望使用`Apache::AuthenDBI`模块。

8. 创建一个名为`/memberonly/`的别名，指向你希望限制访问的目录，使用以下`Alias`指令：

```
Alias /memberonly/ "path_to_restricted_access_directory"
```

例如：

```
Alias /memberonly/ "/usr/local/apache/htdocs/protected/"
```

这里`/memberonly/`别名指向`/usr/local/apache/htdocs/protected/`目录。

9. 现在在`httpd.conf`中创建以下配置段：

```
<Location /memberonly/>

AuthName "Home"

AuthType Basic

PerlAuthenHandler Apache::AuthenDBI

PerlSetVar Auth_DBI_data_source dbi:mysql:database=auth

PerlSetVar Auth_DBI_username httpd

PerlSetVar Auth_DBI_password 2manysecrets

PerlSetVar Auth_DBI_pwd_table wwwusers

PerlSetVar Auth_DBI_uid_field user

PerlSetVar Auth_DBI_pwd_field passwd

PerlSetVar Auth_DBI_encrypted on

require valid-user

</Location>
```

以下列表帮助你快速了解上述配置中正在发生的事情：

- 上述配置告诉 Apache 使用`Apache::AuthenDBI`作为`/memberonly/`别名对应的处理器。
- `PerlSetVar`指令用于设置该模块所需的关键-值对。
    - `Auth_DBI_data_source`键设置数据库 DSN，告诉模块使用哪个 Perl DBD 连接到哪个数据库。在这里，值设置为连接到名为`auth`的 MySQL 数据库。你应该将驱动器设置为你正在使用的任何 RDBM。例如，如果你使用的是 IBM DB2，你的数据库源名称（DSN）可能是`dbi:db2:database=auth`。
- `Auth_DBI_username`和`Auth_DBI_password`键设置用于连接到命名用户数据库（即`auth`）的数据库用户名和密码。
    - 密码表的名称由`Auth_DBI_pwd_table`键指定；类似地，用户名和密码字段分别由`Auth_DBI_uid_field`和`Auth_DBI_pwd_field`键指定。
    - `Auth_DBI_encrypted`键设置为`on`，因此假设存储在数据库中的密码是使用名为`crypt`的传统 Unix 风格单向哈希加密函数加密的。
- 最后，`require valid-user`指令告诉 Apache 仅允许通过认证测试的用户访问。

10. 你可以通过使用`/usr/local/apache/bin/apachectl restart`命令重启 Apache 服务器，并尝试访问`http://your_server_name/memberonly`目录，以查看是否可以使用无效的用户名和密码访问该目录。如果你输入有效的用户名和密码，你应该能够完成认证。

## 在任何 RDBM 中管理用户和组

手动管理数据库中的用户和组非常繁琐。幸运的是，你不必处理这类任务。你可以使用一组 Perl 脚本来相当高效地处理这些杂务。方法如下。

1. 你需要从 Perl 综合存档网络（CPAN）安装`DBI`包和相应的`DBD::database`模块。例如，如果你安装了 MySQL 数据库，你可以作为 root 用户通过命令行安装`DBI`和`DBD`模块，如下所示：

```
perl -MCPAN -e 'install DBI'
```
