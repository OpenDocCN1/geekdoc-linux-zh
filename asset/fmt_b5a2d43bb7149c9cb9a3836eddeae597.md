
`mysqldump` 比二进制备份技术更慢，因为转储操作涉及在 `mysqldump` 和服务器之间的网络连接上传输信息。二进制备份方法通过在文件系统级别复制文件来工作，不需要网络流量。

`mysqldump` 生成包含 SQL 语句的文本文件。这些文件可以移植到其他机器，甚至是具有不同硬件架构的机器。因此，它们可用于将数据库从一台服务器复制到另一台服务器。由直接复制二进制备份方法生成的文件可能可以移植到其他机器，也可能不能。这取决于表是否使用机器无关的存储格式。`MyISAM` 和 `InnoDB` 表通常是机器无关的。对于这些存储引擎，直接复制的文件可以移动到运行在具有不同硬件架构的机器上的服务器。`Falcon` 日志和表空间文件以机器相关的格式存储。它们只能在具有相同硬件特性的机器之间二进制移植。关于各种存储引擎可移植性的进一步讨论，请参阅第 2.6.1.11 节，“存储引擎可移植性特性”。

`mysqldump` 输出由数据库内容（表、视图、存储例程等）组成的转储。它不会备份未存储在数据库内的信息，如配置文件、日志文件或复制状态文件。二进制备份可以包括这些文件中的任何或全部，因为你可以作为备份的一部分复制任何你喜欢的文件。

无论你选择哪种备份方法，遵守以下原则可确保在你需要恢复数据库内容时获得最佳结果：

定期执行备份。设定时间表并坚持执行。

配置服务器以执行二进制日志记录（请参阅第 12.5 节，“维护日志”）。二进制日志可以在你需要在崩溃后恢复数据库时提供帮助。在使用备份文件将数据库恢复到备份时的状态后，你可以重新执行日志文件的内容来重新应用备份发生后发生的更改。这将恢复数据库中的表到崩溃发生时的状态。

对你的备份文件使用一致且有意义的命名方案。像 `backup1`、`backup2` 等名称并没有特别大的帮助。当到了执行恢复操作的时候，你会浪费时间去弄清楚文件里有什么。你可能会发现使用数据库名称和日期构建备份文件名很有用。例如，如果你在 2008 年 1 月 2 日转储 `sampdb` 数据库，你可能会将备份文件命名为 `sampdb-2008-01-02`。如果你运行多台服务器，请在名称中包含服务器标识符。

将你的备份文件放在与你用于数据库不同的文件系统上。这降低了因生成备份而填满包含数据目录的文件系统的可能性。如果你存储备份的文件系统位于不同的物理磁盘上，你进一步减少了磁盘故障可能造成的损坏程度，因为丢失任何一个磁盘都不能同时销毁你的数据目录和你的备份。

将您的数据库备份文件纳入常规的文件系统备份中。如果发生严重崩溃，不仅数据目录被清除，连存储数据库备份的磁盘驱动器也一并损坏，那您将陷入极大的困境。同时，请备份您的日志文件。

定期使备份文件过期，以免它们占满磁盘。实现这一点的一种方法是使用文件轮转技术。第 12.5.7 节“日志管理”讨论了这些技术与日志文件的关系，但同样的原理也适用于备份文件的过期处理。

紧随其后的章节描述了几种具体的备份方法。如果您正在使用复制功能，第 14.8.4 节“使用复制从机进行备份”描述了一种方法，该方法可以让您的主服务器完全不受干扰。

### 14.4.1 使用 mysqldump 创建文本备份

`mysqldump` 程序用于创建文本转储文件。默认情况下，它会以 SQL 格式写入转储文件，该文件包含用于创建被转储表的 `CREATE TABLE` 语句，以及包含表中行数据的 `INSERT` 语句。为了稍后重新创建被转储的表，请将转储文件作为输入重新加载到 MySQL 中，即使用 `mysql` 命令。例如，要转储并重载单个表（`sampdb.member`），请使用以下命令：

```
$ mysqldump sampdb member > member.sql
$ mysql sampdb < member.sql
```

不要使用 `mysqlimport` 来重新加载 SQL 格式的 `mysqldump` 输出。`mysqlimport` 期望读取的是数据行，而不是 SQL 语句。

要将所有数据库中的所有表备份到单个文件中，可以使用如下命令：

```
$ mysqldump --all-databases > /archive/mysql/mysql-dump-2008-01-02
```

然而，如果您拥有大量数据，生成的转储文件将相当大。您可以将每个数据库单独转储到其自己的文件中，方法如下：

```
$ mysqldump mysql > /archive/mysql/mysql.2008-01-02
$ mysqldump sampdb > /archive/mysql/sampdb.2008-01-02
$
...
```

`mysqldump` 输出文件的开头看起来像这样：

```
-- MySQL Dump 10.11
--
-- Host: localhost   Database: sampdb
-- ------------------------------------------------------
-- Server version   5.0.54-log

... 几条 SET 语句 ...

--
-- Table structure for table `absence`
--
DROP TABLE IF EXISTS `absence` ;
CREATE TABLE `absence` {
 `student_id` int(10) unsigned NOT NULL,
 `date` date NOT NULL,
 PRIMARY KEY (`student_id`,`date`),
 CONSTRAINT `absence_ibfk_1` FOREIGN KEY (`student_id`)
 REFERENCES `student` (`student_id`)
} ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Dumping data for table `absence`
--
LOCK TABLES `absence` WRITE;
/*!40000 ALTER TABLE `absence` DISABLE KEYS */;
INSERT INTO `absence` VALUES (3,'2008-09-03'),(5,'2008-09-03'),
(10,'2008-09-06'),(10,'2008-09-09'),(17,'2008-09-07'),(20,'2008-09-07');
/*!40000 ALTER TABLE `absence` ENABLE KEYS */;
UNLOCK TABLES;
```

文件的其余部分由更多的 SQL 语句组成，例如 `CREATE TABLE` 和 `INSERT`。

转储文件通常很大，因此您很可能希望尽可能缩小它们的体积。`mysqldump` 有一个 `--opt` 选项，它可以启用多个其他选项，从而优化转储过程以生成更小的输出。这些选项还优化了恢复过程，因为稍后重新加载转储文件时，输出可以更快地被处理。例如，`--opt` 的一个作用是使 `mysqldump` 写入多行 `INSERT` 语句。这些语句占用的空间更少，且比等效的单行 `INSERT` 语句集合加载得更快。

`--opt` 选项默认是启用的（从 MySQL 4.1 开始就是如此），因此无需明确指定。如果您想禁用它，请使用 `--skip-opt`。

减小转储文件体积的另一种方法是压缩它。在 Windows 上，您可以使用 WinZip 或类似程序来压缩转储文件并生成 Zip 格式的文件。在 Unix 上，您可以使用 `gzip` 或 `bzip2`。您甚至可以通过使用命令管道在生成备份的同时对其进行压缩：

```
$ mysqldump sampdb | gzip > /archive/mysql/sampdb.2008-01-02.gz
$ mysqldump sampdb | bzip2 > /archive/mysql/sampdb.2008-01-02.bz2
```

如果大型转储文件难以管理，可以通过在 `mysqldump` 命令行的数据库名称后指定具体的表名，来转储单个表的内容。`mysqldump` 将仅转储指定的表，而不是数据库中的所有表，从而生成更小、更易管理的文件。以下示例展示了如何将 `sampdb` 表的子集转储到单独的文件中：

```
$ mysqldump sampdb member president > hist-league.sql
$ mysqldump sampdb student score grade_event absence > gradebook.sql
```

`mysqldump` 有许多选项。您可能觉得有用的选项包括以下几个：
