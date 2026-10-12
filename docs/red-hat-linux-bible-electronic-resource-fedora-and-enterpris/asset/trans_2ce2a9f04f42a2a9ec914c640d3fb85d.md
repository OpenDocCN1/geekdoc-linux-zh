
1. 如果你尚未连接到 mysql 会话，请输入以下命令（假设 mysql 用户名为 root）：

```
# mysql -u root -p
Enter password: ********
mysql>
```

2. 要创建名为 bobby 的用户和密码 i8yer2shuz，请按如下方式使用 GRANT 命令：

```
mysql> GRANT USAGE ON *.*
   -> TO bobby@localhost IDENTIFIED BY "i8yer2shuz";
```

此时，某人可以使用名称 bobby 和密码 i8yer2shuz 从 localhost 登录（mysql -u bobby -p）。但该用户没有任何操作数据库的权限。接下来你需要授予权限。

3. 要授予 bobby 操作名为 allusers 的数据库的权限，可以输入以下内容：

```
mysql> GRANT DELETE,INSERT,SELECT,UPDATE ON allusers.*
   -> TO bobby@localhost;
```

在此示例中，用户 bobby 被允许登录到 localhost 上的 MySQL 服务器并访问 allusers 数据库中的所有表（USE allusers）。对于该数据库，bobby 可以使用 DELETE、INSERT、SELECT 和 UPDATE 命令。

4. 要查看刚刚授予的权限，可以将 mysql 选择为当前数据库，然后按如下方式选择 db 表：

```
mysql> USE mysql;
Database changed
mysql> SELECT * FROM db WHERE db="allusers";
```

| 主机 | 数据库 | 用户 | Select_priv | Insert_priv | Update_priv | Delete_priv | ... |
|------|----|------|-------------|-------------|-------------|-------------|-----|
| localhost | allusers | bobby | Y | Y | Y | Y | ... |

此处输出显示所有被明确授予 allusers 数据库权限的用户。此处仅显示部分输出，因为它非常长。你应该使终端窗口足够宽以查看输出，或学习如何阅读换行文本。行上的其他权限将被设置为 N（无访问权限）。

## 撤销访问

你可以使用 REVOKE 命令撤销授予的权限。要撤销用户对特定数据库的所有权限，请使用以下流程：

1. 如果你尚未连接到 mysql 会话，请输入以下命令（假设 mysql 用户名为 root）：

```
# mysql -u root -p
Enter password: ******
mysql>
```

2. 要撤销名为 bobby 的用户使用 MySQL 服务器上名为 allusers 的数据库的所有权限，可以输入以下内容：

```
mysql> REVOKE ALL PRIVILEGES ON allusers.*
-> FROM bobby@localhost;
```

此时，bobby 没有权限使用 allusers 数据库中的任何表。

3. 要查看刚刚授予的权限，可以将 mysql 选择为当前数据库，然后按如下方式选择 db 表：

```
mysql> USE mysql;
Database changed
mysql> SELECT * FROM db WHERE db="allusers";
```

输出应显示用户 bobby 不再列为具有访问 allusers 数据库的权限。（结果可能只是显示 Empty set。）

## 检查和修复数据库

随着时间的推移，数据库可能会损坏或存储信息效率低下。MySQL 附带了可用于检查和修复数据库的命令。myisamchk 和 isamchk 命令可分别用于检查 MyISAM 和 ISAM 数据库表。

MyISAM 表是 MySQL 的默认使用表。表默认存储在目录 /var/lib/mysql/dbname 中，其中 dbname 用你使用的数据库名称替换。每个表在该目录中有三个文件。每个文件以表名开头，以以下三个后缀之一结尾：

- .frm 包含表的定义（或表单）
- .MYI 包含表的索引。
- .MYD 包含表的数据。

以下流程描述如何使用 `myisamchk` 命令检查你的 MyISAM 表。（检查 ISAM 表的流程相同，只是改用 `isamchk` 命令。）

> **警告：** 在使用 `myisamchk` 进行修复之前，请备份你的数据库表。尽管 `myisamchk` 不太可能损坏你的数据，但备份仍然是良好的预防措施。

1. 通过在终端窗口中以 root 用户输入以下内容暂时停止 MySQL：

```
# /etc/init.d/mysql stop
```

2. 你可以一次检查所有或部分数据库表。第一个示例显示如何检查 `allusers` 数据库中名为 `names` 的表。

```
# myisamchk /var/lib/mysql/allusers/names.MYI
Checking MyISAM file: /var/lib/mysql/allusers/names.MYI
Data records:       5    Deleted blocks:       0
- check file-size
- check key delete-chain
- check record delete-chain
- check index reference
- check record links
```

你也可以按如下方式一次检查所有数据库的表：

```
# myisamchk /var/lib/mysql/*/*.MYI
```

前面的示例显示了一个简单的五条记录数据库，未遇到错误。如果看到与上面所示不同的如下输出，你可能需要修复数据库：

```
Checking MyISAM file: names.MYI
Data records:         5    Deleted blocks:       0
- check file-size
myisamchk: warning: Size of datafile is: 89  Should be: 204
- check key delete-chain
- check record delete-chain
- check index reference
- check record links
myisamchk: error: Found wrong record at 0
MyISAM-table 'names.MYI' is corrupted
Fix it using switch "-r" or "-o"
```

3. 要修复损坏的数据库，可以运行以下命令

```
# myisamchk -r /var/lib/mysql/allusers/names.MYI
- recovering (with keycache) MyISAM-table 'names.MYI'
```

```
Data records: 5
Found wrong stored record at 0
Data records: 4
```

4. 如果由于某种原因 -r 选项不起作用，你可以尝试使用 -o 选项运行 myisamchk 命令。这是一种较慢、较旧的修复方法，但可以处理 -r 选项无法处理的几个问题。以下是示例：

```
# myisamchk -o /var/lib/mysql/allusers/names.MYI
```

如果你的计算机内存充足，请提高 myisamchk 命令行上的键缓冲区大小值，这将减少检查数据库所需的时间。例如，你可以使用以下命令行：

```
myisamchk -r -O --key_buffer_size=64M *.MYI
```

这将把键缓冲区大小设置为 64MB。

## 摘要

MySQL 是一个结构化查询语言（SQL）服务器，可在 Red Hat Linux 以及其他操作系统上运行。使用启动脚本 (/etc/init.d/mysqld) 和配置文件 (/etc/my.cnf)，你可以快速启动并运行 MySQL 服务器。

使用 mysqladmin 和 mysql 等工具，你可以管理 MySQL 服务器并创建你需要的简单或复杂的数据库和表。在 mysql 会话期间，你可以修改数据库表的结构或添加、更新和删除数据库记录。你有多种查询数据和排序输出的选项。你还可以完全控制谁可以访问你的数据库表以及用户对你控制的数据库具有哪些修改、添加或删除的权限。

## 第 25 章

## 使用 DNS 使服务器公开

**本章内容**

- 确定服务器目标
- 连接公共服务器
- 配置公共服务器
- 设置 DNS 服务器

在前面的章节中，你在 Linux 中构建了 Web、邮件和 FTP 服务器。现在你想将这些服务器暴露给外部世界。选项范围从将它们交给托管公司并说“Take care of it”，到在家中或办公室自行管理服务器。

以下是你可能想要考虑一定程度的自托管的一些情况：

- 你愿意为组织服务器提供所需的支持级别。
- 你只想以低成本的方式在 Web 上发布一些文档或为少数人维护一个公共邮件服务器，并且 24/7 支持不是关键。
- 你只是觉得自托管很酷，想尝试一下。

本章的第一个目标是帮助你决定要维护多少服务器支持或交给他人。第二个是建议如何设置自己的公共服务器，包括可能配置自己的域名系统（DNS）服务器。

设置你的局域网（第 15 章）和将其连接到互联网（第 16 章）的描述分别侧重于如何在本地共享信息以及让本地用户共享外发互联网连接。基于这些信息，本章介绍如何设置 DNS 服务器，以及与保护和维护公共服务器相关的其他问题。

> **警告：** 在你将服务器开放给互联网流量后，入侵尝试将会发生。大多数来自互联网上受感染计算机发送的自动化脚本。因为 Red Hat Linux 具有良好的内置安全功能，许多攻击都会无害地被弹开（在记录消息之后）。然而，允许传入连接会产生仅外发互联网连接所没有的漏洞。我建议你使用第 14 章中描述的安全工具来保护你的服务器。
