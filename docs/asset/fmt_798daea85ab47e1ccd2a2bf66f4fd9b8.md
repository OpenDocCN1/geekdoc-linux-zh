
![](img/a6dbf7df749be83c0faae2334e970c0b_173_0.png)

### 工作原理...

`PHPMyAdmin` 是一个基于 Web 的 `MySQL` 管理控制台。它用 `PHP` 开发，并与服务器配合进行 Web。通过 `PHPMyAdmin`，你可以执行数据库任务和表操作：创建数据库和表；选择、插入、更新数据；修改表定义以及更多操作。它提供了一个查询控制台，可以在其中输入自定义查询并在同一屏幕上执行它们。

由于 `Ubuntu` 服务器存储库的添加，通过单个命令安装 `PHPMyAdmin` 变得非常简单。一旦安装完成，`MySQL` 服务器上将创建一个新用户。它还支持连接到多个服务器。你可以在 `/etc/phpmyadmin` 目录下找到所有的配置文件。

### 更多内容...

如果你想安装最新版本的 `phpMyAdmin`，可以从其官方网站下载：`https://www.phpmy.net/downloads/`。你可以将下载的内容提取到你的 Web 目录，并在 `config.php` 文件中设置 `MySQL` 凭据。

### 参见

- 在 `Ubuntu` 服务器指南中通过[链接](https://help.ubuntu.com/lts/serverguide/phpmyadmin.html)了解更多关于 `phpMyAdmin` 的信息
- 在 [https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-ubuntu-14-04]( ) 安装并保护 `phpMyAdmin`

![](img/a6dbf7df749be83c0faae2334e970c0b_179_0.png)

### 处理数据库

### 设置备份

在本教程中，我们将学习如何备份 `MySQL` 数据库。

### 准备工作

你将需要 `MySQL` 数据库的管理员权限。

### 如何操作...

按照以下步骤设置备份：

1. 备份 `MySQL` 数据库与从服务器导出数据是相同的。使用 `mysqldump` 工具如下如下备份 `MySQL` 数据库：
   ```
   $ mysqldump -h localhost -u admin -p mydb > mydb_backup.sql
   ```
2. 系统将提示你输入 `admin` 账户密码。提供密码后，备份过程将根据数据库的大小需要一定的时间。
3. 若要备份所有数据库，请在前面的命令中使用 `--all-databases` 标志：
   ```
   $ mysqldump --all-databases -u admin -p alldb_backup.sql
   ```
4. 接下来，我们可以使用 `mysqldump` 工具或以下命令恢复我们创建的备份：
   ```
   $ mysqldadmin -u admin -p create mydb
   $ mysql -h localhost -u admin -p mydb < mydb_backup.sql
   ```
5. 若要恢复所有数据库，请跳过创建数据库的部分：
   ```
   $ mysqldump -h localhost -u admin -p < alldb_backup.sql
   ```

### 工作原理...

`MySQL` 提供了一个非常通用的工具 `mysqldump`，用于从数据库服务器导出所有数据。该工具可用于任何类型的数据库引擎，无论是 `MyISAM`、`InnoDB` 还是其他。为了为 `InnoDB` 表提供在线备份，`mysqldump` 提供了 `--single-transaction` 选项。使用此选项，`InnoDB` 表不会被锁定，在备份进行期间其他应用程序可以使用。

`Oracle` 为 `MySQL` 版用户提供了 `MySQL` Enterprise 备份工具。该工具包含了增量备份和压缩备份等功能。或者，`Percona` 提供了一个名为 `Xtrabackup` 的开源实用。它提供了增量备份、压缩备份以及许多其他功能。

![](img/a6dbf7df749be83c0faae2334e970c0b_180_0.png)

其他备份方法包括复制 `MySQL` 表文件和用于 `InnoDB` 表的 `mysqllogcopy` 脚本。为了让这些方法生效，你可能需要在备份之前暂停或停止 `MySQL` 服务器。

你可以启用复制将所有数据镜像到另一台服务器。这是一种通过自动将数据从一个复制到另一个来维护多个数据副本的机制。在这种情况下，主服务器被称为 `Master`（主），从服务器被称为 `Slave`（从）。这种配置被称为主从复制。通常情况下，应用程序对所有的读写请求都与 `Master` 服务器通信。如果 `Master` 宕机，`Slave` 将用作备份。在许多情况下，主从配置用于通过将所有读请求路由到 `Slave` 服务器、将写请求路由到 `Master` 服务器来实现数据库查询的负载均衡。复制也可以配置为主从模式，此时两台服务器都接收客户端的读写请求。

### 参见

- [http://dev.mysql.com/doc/refman/5.6/en/backup-methods.html]() 处的 `MySQL` 备份方法
- [https://www.percona.com/doc/percona-xtrabackup/2.2/index.html]() 处的 `Percona` `XtraBackup`
- [http://dev.mysql.com/doc/refman/5.6/en/binary-log.html]() 处的 `MySQL` 二进制日志

### 优化 MySQL 性能 – 查询

`MySQL` 性能优化可以分为两部分：查询优化和另一部分是 `MySQL` 服务器配置。为了获得最佳结果，你必须对这两个部分都入手。如果没有正确的配置，查询将无法提供一致的性能；另一方面，如果有正确的查询和数据库结构，查询可能需要更长时间才能产生结果。

在本教程中，我们将学习如何评估查询性能、设置索引并为我们的数据确定最佳数据库结构。

### 准备工作

你将需要 `MySQL` 服务器的管理员账户访问。

你需要一个大型数据集来测试查询。可以使用各种工具生成测试数据。我将使用位于 [https://github.com/datacharmer/test_db](https://github.com/datacharmer/test_db) 提供的测试数据。

### 如何操作...

按照以下步骤优化 `MySQL` 性能：

1. 第一步也是最基础的是识别关键列并添加索引：
   ```sql
   ALTER TABLE employees ADD INDEX (first_name);
   SELECT * FROM employees WHERE first_name = 'John';
   ```
2. 观察查询执行时间：
   ```sql
   SELECT COUNT(*) FROM employees WHERE first_name = 'John';
   ```
   执行耗时 `0.048` sec
3. 使用 `EXPLAIN` 命令查看执行计划：
   ```sql
   EXPLAIN SELECT * FROM employees WHERE first_name = 'John';
   ```
   你会看到 `type` 为 `ALL`，这意味着正在进行全表扫描。
4. 关键列并添加索引：
   ```sql
   ALTER TABLE employees ADD INDEX (first_name);
   ```
   执行耗时 `0.5` sec。
5. 添加索引后，再次运行查询：
   ```sql
   SELECT COUNT(*) FROM employees WHERE first_name = 'John';
   ```
   你会发现执行时间缩短到了 `0.005` sec。
6. 再次使用 `EXPLAIN` 查看执行计划：
   ```sql
   EXPLAIN SELECT * FROM employees WHERE first_name = 'John';
   ```
   现在你会看到 `type` 变为 `ref`，`key` 使用了 `first_name` 索引。
7. 进一步优化：如果查询涉及多个列，可以考虑复合索引：
   ```sql
   ALTER TABLE employees ADD INDEX (last_name, first_name);
   ```
8. 这种方法可以持续提升性能。

### 处理数据库

一旦接收到查询，`MySQL` 会为其生成查询执行计划。这一步骤包含了解析、预处理和优化等多个阶段。在解析和预处理阶段，系统会检查查询是否存在语法错误以及 `SQL` 语法的顺序是否正确。给定的查询可以通过多种方式执行。查询优化器会为查询执行选择最佳路径。最后，执行查询并将执行计划存储在查询缓存中以备后后用。

可以通过 `explain` 查询及其扩展命令从 `MySQL` 中获取查询执行计划。`explain` 在生成查询执行计划期间执行查询，然后将执行计划作为结果返回。查询执行计划包含了该查询使用的表名、用于搜索数据的字段、扫描的行数，以及（如果有的话）临时表和文件排序。查询执行计划显示了可能的键（`key`）和实际使用的列。键是带有索引的列，可以是主索引、唯一索引或非唯一索引。你可以查看 `MySQL` 文档以获取有关查询执行计划和 `explain` 输出的更多细节。

如果某个列被反复使用，请考虑为该列添加索引。索引将数据分组，从而缩短查找时间并减少扫描的总行数。请记住，索引会占用大量内存，因此添加索引时要谨慎选择。

如果你在所需的列上设置了适当的索引，但查询优化计划没有识别或使用该索引，你可以通过 `USE INDEX index_name` 语句强制 `MySQL` 使用特定索引。要忽略特定索引，请使用 `IGNORE INDEX index_name` 语句。

你可能会通过表维护命令获得微小的改进。当表的大部分被修改或删除时，`Optimize table` 非常有用。它会重组物理存储上的数据并提高 I/O 性能。`Flush table` 用于重新加载内部缓存`Check table` 和 `Analyze table` 分别检查表错误和数据分布。对于小表，这些命令带来的改进可能并不显著。减少为每个列分配的额外空间也有助于减少总物理存储。存储的减少将提高 I/O 性能和缓存利用率。

你还应该检查特定表使用的存储引擎。`MySQL` 中使用的两个主要存储引擎是 `MyISAM` 和 `InnoDB`。`InnoDB` 提供了完整的事务支持并使用行级锁，而 `MyISAM` 不支持事务并使用表级锁。对于数据量大但写入有限的情况，`MyISAM` 是快速读取的良好选择。`MySQL` 支持以插件的形式添加外部存储引擎。一个流行的开源存储引擎是 `Percona` 系统提供的 `XtraDB`。

## 还有更多……

如果你的表非常大，你应该考虑对它们进行分区。表分区将相关数据分布在磁盘上的多个文件上。在经常使用的键上进行分区可以带来快速提升。`MySQL` 支持多种类型的分区，如哈希分区（`hash`）、范围分区（`range`）、列表分区（`list`）、键分区（`key`）以及子分区（`sub-partitions`）。

你可以如下在创建表时指定哈希分区：

```sql
```
