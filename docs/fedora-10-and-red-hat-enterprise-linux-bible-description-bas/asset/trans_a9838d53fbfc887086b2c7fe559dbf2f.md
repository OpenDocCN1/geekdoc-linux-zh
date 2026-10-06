

# 第四部分：Fedora 和 RHEL 网络与服务器设置

.frm 包含表的定义（或格式）

.MYI 包含表的索引

.MYD 包含表的数据

以下步骤描述了如何使用 `myisamchk` 命令检查您的 MyISAM 表格。

> 注意：在运行 `myisamchk` 修复之前，请对您的数据库表进行备份。虽然 `myisamchk` 不太可能会损坏您的数据，但备份仍然是一个良好的预防措施。

- 1. 以 root 用户身份在终端窗口中执行以下命令临时停止 MySQL：

```
# /etc/init.d/mysqld stop
```

- 2. 你可以一次检查所有或部分数据库表。第一个示例显示了如何检查 `allusers` 数据库中的表名。

```
# myisamchk /var/lib/mysql/allusers/name.MYI
Checking MyISAM file: /var/lib/mysql/allusers/name.MYI
Data records: 5 Deleted blocks: 0
- check file-size
- check key delete-chain
- check record delete-chain
- check index reference
- check record links
```

你也可以按照以下方式一次性检查所有的数据库：

```
# myisamchk /var/lib/mysql/*.MYI
```

前面的示例显示了一个简单的五记录数据库，其中没有遇到任何错误。如果看到的输出不是上一个示例中的输出，而是如下所示所示，你可能需要修复数据库：

```
Checking MyISAM file: name.MYI
Data records: 5 Deleted blocks: 0
- check file-size
myisamchk: warning: Size of datafile is: 89 Should be: 204
- check key delete-chain
- check record delete-chain
- check index reference
- check record links
myisamchk: error: Found wrong record at 0
MyISAM-table 'name.MYI' is corrupted
Fix it using switch "-r" or "-o"
```

# 第 24 章：设置 MySQL 数据库服务器 953

- 3. 为了修复损坏的数据库，你可以运行以下命令：

```
# myisamchk -r /var/lib/mysql/allusers/name.MYI
recovering (with keycache) MyISAM-table 'name.MYI'
Data records: 5
Found stored record at 0
Data records: 4
```

- 4. 如果由于原因 `-r` 选项不起，你可以尝试使用 `-o` 选项运行 `myisamchk` 命令。这是一种较慢的旧式修复方法，但它可以处理 `-r` 选项无法处理的问题。这是一个示例：

```
# myisamchk -o /var/lib/mysql/allusers/name.MYI
```

如果你的计算机有大量内存，你可以在 `myisamchk` 命令行上增加键缓冲区大小，这将缩短检查数据库的时间。例如，你可以使用以下命令：

```
myisamchk -r -O --key_buffer_size=64M *.MYI
```

这将键缓冲区大小设置为 64MB。

# 总结

MySQL 是一个结构化查询语言 (SQL) 数据库服务器，运行在 Fedora、RHEL 以及其他操作系统上。通过启动脚本 (`/etc/init.d/mysqld`) 和配置文件 (`/etc/my.cnf`)，你可以启动并运行 MySQL 服务器。

通过 `mysqladmin` 和 `mysql` 命令等工具，你可以管理 MySQL 服务器，并根据需要创建简单或复杂的数据库和表。在 `mysql` 会话期间，你可以修改数据库表的结构，或添加、更新和删除数据库记录。你有多种选项来查询数据并对输出排序。你还可以控制谁可以访问你的数据库表，以及用户对修改、添加或删除你所控制的数据库拥有何种权限。

# 第 25 章：使用 DNS 使服务器公开化

本章内容

- 确定你服务器的目标
- 连接公共服务器
- 配置公共服务器
- 设置 DNS 服务器

在之前的章节中，你构建了 Web、邮件和 FTP 服务器，并将它们连接到互联网。现在，你想要将这些服务器暴露给外部世界。方案从将它们交给托管公司并说“由你们来吧”，到在你自己的家里或办公室管理这些服务器。

以下是你可能考虑进行某种程度自托管的一些情况：

- 你愿意提供你的组织所需的支持水平。
- 你只是想用廉价的方式为少数人在网络上发布一些文档，且 24/7 的支持至关重要。
- 你觉得自托管很酷，想尝试一下。

本章的首要目标是帮助你决定想要维护或为他人提供多少支持。第二个目标是建议如何设置你的公共服务器，可能包括配置你自己的域名系统 (DNS) 服务器。

关于设置局域网（LAN）（见第 15 章）并将其连接到互联网（见第 16 章）的描述分别侧重于信息共享和访问。在此基础上，本章解释了如何设置 DNS 服务器，以及其他与安全和维护公共服务器相关的问题。

> 注意：当你向互联网开放服务器后，将会发生安全攻击。大多数攻击来自自动化脚本。虽然 Fedora 和 RHEL 自带了良好的安全功能，但允许入站连接会产生漏洞。我强烈建议你使用第 14 章描述的安全工具来保护你的服务器。

# 确定你服务器的目标

在你开放该服务器之前，请停下来考虑一下你服务器的目标。以下是你可能需要问自己的问题：

- 服务器对你的业务有多重要？
- 你期望服务器产生多少流量？
- 你是否需要 24 小时 365 天的支持？
- 你是否有足够的知识维护服务器？
- 你是否能获得满足你要求的带宽？
- 你是否需要如不间断电源（UPS）、RAID 设备等来维护服务器？

维护公共服务器需要资源。如果你的服务器在互联网上是高需求的，你可能需要某些托管服务（也就是说，在你注册域名并加入托管服务后，你可能可以跳过本章）。

# 使用托管

假设你将在工作场所或住所托管服务器，你需要从潜在的 ISP 获取以下信息：

- 它的服务条款是否允许你通过连接提供服务？
- 它是否有愿意分配给你的静态 IP 地址？
- 它是否足够健壮以处理你服务器的流量需求？

# 检查服务条款

任何超过几个用户的 ISP 都拥有一份描述你可以对它提供的互联网连接做什么的文档。该文档的名称如下

