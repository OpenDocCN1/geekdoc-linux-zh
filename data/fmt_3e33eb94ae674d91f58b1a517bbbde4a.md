
选项文件在包含不应公开暴露的选项方面代表着潜在的妥协点：

- 如果选项文件包含敏感信息（例如 MySQL 账户名称或密码），请不要使其公开可读。
- `/etc/my.cnf` 通常公开可读，因为它是指定全局客户端选项的常见位置。这意味着你不应该用它来存储服务器选项，例如复制密码。
- 每个用户特定的 `.my.cnf` 选项文件应由该用户拥有且仅可被该用户访问，该文件出现在用户的家目录中。为了对你的文件这样做，在你的家目录中执行以下命令：

```
% chmod u=rwx,go-rwx .my.cnf
```
+ 其他选项文件需要根据其用途设置相应的访问模式。

确保用户特定的选项文件具有正确的模式和属主的一种方法是运行一个程序，该程序会在每个用户的 home 目录中查找 `.my.cnf` 文件并修正任何问题。下面的 Perl 脚本 `chk_mysql_opt_files.pl` 即可完成此任务：

```perl
#!/usr/bin/perl
# chk_mysql_opt_files.pl - check user-specific .my.cnf files and make sure
# the ownership and mode is correct. Each file should be owned by the
# user in whose home directory it is found. The mode should
# have the "group" and "other" permissions turned off.

# This script must be run as root. Execute it with your password file as
# input. If you have an /etc/passwd file, run it like this:
# chk_mysql_opt_file.pl /etc/passwd
# For Mac OS X, use the netinfo database:
# nidump passwd . | chk_mysql_opt_file.pl

use strict;
use warnings;

while (<>)
{
    my ($uid, $home) = (split /\/:/, $_)[2,5];
    my $cnf_file = "$home/.my.cnf";
    next unless -f $cnf_file;   # is there a .my.cnf file?
    if ((stat ($cnf_file))[4] != $uid)  # test ownership
    {
        warn "Changing ownership of $cnf_file to $uid\n";
        chown ($uid, (stat ($cnf_file))[5], $cnf_file);
    }
    my $mode = (stat ($cnf_file))[ 2];
    if ($mode & 077)
    {
        warn sprintf ("Changing mode of %s from %o to %o\n",
                      $cnf_file, $mode, $mode & ~077);
        chmod ($mode & ~077, $cnf_file);
    }
}
```

您可以在 `samp db` 发行版的 `admin` 目录中找到 `chk_mysql_opt_files.pl`。您必须以 root 身份运行此脚本，因为它需要能够修改属于其他用户的文件的模式和属主。若要自动执行该脚本，请将其设置为由 root 运行的每晚定时 cron 任务。

## 13.2 外部安全：防止未经授权的网络访问

MySQL 安全系统具有灵活性。它允许您以多种不同的方式设置用户访问权限。通常，您通过使用权管理语句（如 `CREATE USER`、`GRANT` 和 `REVOKE`）来完成此操作，这些语句会代您修改控制客户端访问权限的授权表。然而，您可能会发现用户权限并未按您期望的方式工作。对于此类情况，了解 MySQL 授权表的结构以及服务器如何使用它们来确定访问权限将非常有帮助。这种理解使您能够直接修改授权表来添加、删除或修改用户权限。它还可以让您在检查这些表时诊断权限问题。

假设您已经阅读了第 12.4 节“管理 MySQL 用户帐户”，并且了解各种权管理语句的工作原理。这些语句为您提供了一种便捷的方式来设置 MySQL 用户帐户并为其关联权限，但它们只是前端。所有真正的操作都发生在 MySQL 授权表中。

### 13.2.1 MySQL 授权表的结构和内容

通过服务器通过网络连接的客户端对 MySQL 数据库的访问由授权表的内容控制。这些表位于 `mysql` 数据库中，并在机器上首次安装 MySQL 的过程中初始化（例如，如附录 A“获取和安装软件”中所描述）。这些表的名称为 `user`、`db`、`tables_priv`、`columns_priv` 和 `proc_priv`。服务器使用这些表的方式如下：

- **`user`** 表列出了可以连接到服务器的用户帐户、它们的密码以及每个用户拥有的全局（超级用户）权限（如果有）。重要的是要认识到，在 `user` 表中启用的任何权限都是适用于所有数据库的全局权限。例如，如果在 `user` 表的某一行中启用了 `DELETE` 权限，则与该帐户相关的行将能够删除任何数据库中任何表的行。在执行此操作之前请仔细考虑。

由于在 `user` 表中指定的权限具有超级用户性质，通常最好关闭此表中所有行的所有权限，并在其他限制更严格的表中列出更具体的权限。这一原则有两个例外：

第一，如 root 和其他管理帐户等超级用户需要全局权限来操作服务器。这些帐户通常较少。

第二，一些特定的全局权限通常可以安全地授予。这些权限涉及创建临时表、锁定表以及（可能）使用 `SHOW DATABASES` 语句的能力。许多安装会授予这些权限；而对于需要更严格控制的其他安装则不会。

`**user**` 表还包含用于 SSL 连接的 SSL 选项列，以及可用于防止特定帐户独占服务器的资源管理列。

- **`db`** 表列出了具有权限的帐户及其对应的数据库。如果您在此处授予权限，它将适用于数据库中的所有对象（表、存储例程等）。
- **`tables_priv`** 表列出了表级权限。在此处指定的权限适用于表中的所有列。
- **`columns_priv`** 表列出了列级权限。在此处指定的权限适用于表中的特定列。
- **`procs_priv`** 表包含存储例程（函数和过程）的权限。在此处指定的权限适用于数据库中的特定例程。该表是在 MySQL 5.0.3 中引入的。

`**mysql**` 数据库还包含一个名为 **`host`** 的授权表，它与 **`db`** 表结合使用。然而，`**host**` 表已过时，此处不再进一步讨论。

每个授权表的结构显示在以下几个表中，按列类型划分。每个授权表包含两种主要类型的列：确定行何时适用的访问范围列，以及确定行授予哪些权限的权限列。权限列可以进一步细分为用于管理操作的列和与特定类型对象操作相关的列。`**user**` 表还有用于 SSL 连接和资源管理的附加列；这些列仅存在于 **`user`** 表中，因为它们具有全局适用性。一些授权表包含其他杂项列，但由于它们与帐户管理无关，因此此处不予讨论。

#### 表 13.1 授权表访问范围列

| **`user`** | **`db`** | **`tables_priv`** | **`columns_priv`** | **`procs_priv`** |
| :--- | :--- | :--- | :--- | :--- |
| Table | Table | Table | Table | Table |
| Host | Host | Host | Host | Host |
| User | User | User | User | User |
| Password | Db | Db | Db | Db |
| | | Table_name | Table_name | Routine_name |
| | | | Column_name | Routine_type |

#### 表 13.2 授权表管理权限列

| `user` 表 | `db` 表 | `host` 表 |
| --- | --- | --- |
| Create_user_priv | | |
| File_priv | | |
| Grant_priv | Grant_priv | Grant_priv |
| Process_priv | | |
| Reload_priv | | |
| Repl_client_priv | | |
| Repl_slave_priv | | |
| Show_db_priv | | |
| Shutdown_priv | | |
| Super_priv | | |

#### 表 13.3 授权表对象权限列

| `user` 表 | `db` 表 |
