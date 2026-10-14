

```
$ mysqldump wordpress > wordpress_backup.sql
```

如果你想在导出数据库的同时进行压缩，可以在中间加上管道到 gzip：

```
$ mysqldump wordpress | gzip > wordpress_backup.sql.gz
```

现在如果你想备份不止一个数据库，主要有两种方法。第一种方法是使用 --databases 参数，后面跟要备份的数据库的空格分隔列表。另一种方法是使用 --all-databases 参数，它会备份所有内容：

```
$ mysqldump --all-databases > all_databases_backup.sql
```

当然，我假设你为数据库用户设置了密码，因此这些命令对这些用户不起作用。特别是如果你想备份所有数据库，就尤其不会起作用，因为其中至少有一些是 root 用户拥有的。解决方案是使用 -u 和 -p 选项来指定要使用的用户和密码：

```
$ mysqldump --all-databases -u root -pinsecure > all_databases_backup.sql
```

上面的命令将使用密码 insecure 以 root 用户身份备份所有数据库。我列出这个例子只是想说，虽然这个选项可行，但它是不安全的。原因在于，完整的参数列表，包括密码，会对系统上运行 ps 命令的所有用户可见。更好的方法是使用 -p 但不指定密码：

```
$ mysqldump --all-databases -u root -p > all_databases_backup.sql
```

当你指定 -p 而不带密码时，mysqldump 的行为就像 mysql 命令一样，会提示你输入密码。这提供了良好的安全性，但当然也意味着你必须手动输入密码。大多数备份 MySQL 数据库的人会设置一个 cron 作业在夜间执行。MySQL 建议你解决这个问题的方法是，在执行备份的用户 ~/.my.cnf 文件的 client 部分中添加密码。如果你还没有 ~/.my.cnf 文件，创建一个新文件并添加以下文本：

```
[client]
password=moresecure
```

将 moresecure 替换为你的用户登录时使用的密码。一旦设置好此文件，你就不再需要指定 -p 选项，因为 mysqldump 会从此文件中读取密码。当然，这里的问题是该密码以明文形式存储在系统文件中，因此你需要设置其权限以便只有你的用户可以查看：

```
$ chmod 400 ~/.my.cnf
```

## 恢复 MySQL 备份

如果无法从中恢复，备份就没什么用。要在 MySQL 中恢复备份，请使用 mysql 命令行工具并指向你的备份。例如，要将 test 数据库备份到 test_backup.sql，你需要输入

```
$ mysql test < test_backup.sql
```

如果你备份的是多个数据库，只需输入

```
$ mysql < multiple_database_backup.sql
```

要恢复所有数据库，你需要以 root 用户身份登录。当然，你是一位安全的 MySQL 管理员，并且已设置了 root 密码，因此你必须使用 -p 选项（除非你设置了 .my.cnf 文件，在这种情况下可以省略 -p）：

```
$ mysql -u root -p < all_databases.sql
```

## MySQL 备份 Cron 作业

由于大多数人通常希望至少每天提供一次 MySQL 备份，这里有一个快速简单的方法来设置 cron 作业。首先选择你要存储备份的位置。在此示例中，我仍然将备份存储在 /root 中，因为我知道只有 root 可以读取该目录，但你可能希望将其存储在其他有更多空间的位置。

主要需要考虑的是你要保留多少个备份。如果你已经有某种备份系统来备份所有文件，你可能只需要保留一个数据库备份文件在系统上，因为旧版本将存储在你的远程备份服务器上。如果你想存储比如一周的备份，可以使用一个简单的 shell 技巧。date 命令不带参数可以输出当前日期，但你可以添加一些参数使其仅输出，例如当前星期几：

```
$ date +%A
Friday
```

运行 mysqldump 时，你可以将整个命令用反引号括起来，shell 将用命令的输出替换脚本的该部分。因此，如果你写

```
$ mysqldump -u root --all-databases > /root/all_databases_backup-`date +%A`.sql
```

shell 实际上会将数据库保存到 /root/all_databases_backup-Friday.sql。这意味着第二天运行该命令时它会命名为 Saturday，以此类推。一周后，新备份将自动覆盖前一周的备份，而无需你编写额外的 shell 逻辑。要使此命令每晚运行，你只需以 root 身份创建一个名为 /etc/cron.daily/mysqlbackup 的文件，其中包含以下脚本：

```
#!/bin/sh

mysqldump -u root --all-databases > /root/all_databases_backup-`date +%A`.sql
```

然后你需要输入 chmod a+x /etc/cron.daily/mysqlbackup 使脚本可执行。

最后，如果你为 MySQL 设置了 root 密码，你必须创建 /root/.my.cnf 文件并在其中放入密码，如前所述。现在每晚当 cron.daily 脚本运行时，此脚本也会运行。如果你想更改要保留的备份数量，只需更改反引号中的 date 命令即可。如果你只想要一个备份，可以

