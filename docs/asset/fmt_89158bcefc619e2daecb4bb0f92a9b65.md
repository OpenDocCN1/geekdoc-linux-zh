
```
Merge Join (cost=823.39..1012.88 rows=10000 width=63)
  -> Index Scan using Artists_pkey on Artists (cost=0.00..52.00 rows=1000 width=16)
  -> Sort (cost=823.39..823.39 rows=10000 width=16)
  -> Seq Scan on Pictures (cost=0.00..159.00 rows=10000 width=76)
```

`EXPLAIN`

在这里，你看到 `Artists` 和 `Pictures` 表之间正在执行一个连接，但 `Pictures` 表中没有键来帮助数据库引擎搜索用于连接的元素。每个操作的成本是向上累加的；随着你沿着树结构向上移动，你可以看到查询的总体成本在增加。树底部的顺序扫描（`Seq Scan`）操作对系统性能造成了显著影响。如果你在 `Pictures` 表的 `Artist_ID` 键上建立了索引，数据库将不再需要进行扫描，而是可以执行索引扫描（`Index Scan`），这要快得多，如下例所示：

`PictureArchive=# CREATE INDEX Pictures_Artist_ID_key ON Pictures ( Artist_ID );`

`CREATE`

`PictureArchive=# EXPLAIN SELECT Artists.Name, Pictures.Name FROM Artists LEFT JOIN Pictures ON Artists.ID=Pictures.Artist_ID;`

`NOTICE: QUERY PLAN:`

```
Merge Join (cost=0.00..628.56 rows=10000 width=62)
  -> Index Scan using Artists_pkey on Artists (cost=0.00..52.00 rows=1000 width=16)
  -> Index Scan using Pictures_Artist_ID_key on Pictures (cost=0.00..52.00 rows=1000 width=16)
```

`EXPLAIN`

在这里，你看到 `Artists` 和 `Pictures` 表之间正在执行一个连接，但 `Pictures` 表中没有键来帮助数据库引擎搜索用于连接的元素。每个操作的成本是向上累加的；随着你沿着树结构向上移动，你可以看到查询的总体成本在增加。树底部的顺序扫描（`Seq Scan`）操作对系统性能造成了显著影响。如果你在 `Pictures` 表的 `Artist_ID` 键上建立了索引，数据库将不再需要进行扫描，而是可以执行索引扫描，这要快得多，如下例所示：

## 优化数据库性能 795

创建临时表

（由于提供的待翻译文本在“优化数据库性能”后出现了大量重复和逻辑混乱的片段，此处翻译根据原文结构进行了对应性处理，并保持了技术术语的准确性。）

仅所有者可读的 `crontab` 文件；但如果你担心本地安全，可以创建一个特殊的“备份”用户，该用户对所有数据库拥有 `SELECT` 和 `LOCK TABLES` 权限，但没有其他权限。这样一来，即使该用户的密码被截获，攻击者也无法进行任何破坏性操作。

使用以下命令执行 `mysqldump`：

```bash
# mysqldump --user="frank" --password="franks-password" PictureArchive
-> /usr/local/www/db/PictureArchive.sql
```

如果你将其作为 `cron` 任务（定时任务）运行，你可能想在该命令前加上类似于 `mv /usr/local/www/db/PictureArchive.sql /usr/local/www/db/PictureArchive.sql-old` 的分号。这将旧的转储文件移走，以便创建新的转储文件。然后它将运行备份，所有操作都在一个命令中完成。

## 使用 mysqlhotcopy

如果你想快速为整个数据库目录创建一个快照而不创建转储文件，可以使用 `mysqlhotcopy`。这是一个 `Perl` 脚本，它会锁定表并将它们的所有关联文件复制到新的指定位置；如果你的数据库损坏或丢失，你只需关闭 `MySQL`，将文件移动到 `/var/db/mysql` 下相应的位置，然后重启服务器。要运行 `mysqlhotcopy`，请执行以下操作：

```bash
# mysqlhotcopy --user="frank" --password="franks-password" PictureArchive
-> /usr/local/www/db/PictureArchive
```

## 备份 PostgreSQL 数据库

对于 `PostgreSQL`，`pgump` 命令等同于 `mysqlhotcopy`。最简单的方法是以拥有数据库的 `pgsql` 用户身份运行 `pgump`：

```bash
# pgsql PictureArchive /usr/local/www/db/PictureArchive.sql
```

如你在第 15 章中看到的，使用 `crontab -u pgsql` 创建 `pgsql` 的 `crontab` 文件。

## 恢复数据库

从 `mysqldump` 或 `pgump` 输出的 `.sql` 文件恢复数据库在概念上非常简单。它仅仅是 `SQL` 命令的“重放”，这些命令将详尽地重新创建整个数据库——首先通过重建表及其所有索引，然后重新插入所有数据。

要从 `.sql` 文件恢复 `MySQL` 数据库，你必须先创建数据库（如果已被删除或删除），然后使用以下命令：

```bash
# mysql -p PictureArchive < /usr/local/www/db/PictureArchive.sql
```

系统会提示你输入密码。（或者，你可以像在本章之前看到中，使用 `-u` 或 `--user=` 指定 `frank` 用户，使用 `-p` 或 `--password=` 指定 `frank` 的密码。）接受后，`.sql` 文件将被读取到数据库中，通过 `SHOW TABLES` 以及一些 `DESCRIBE table` 和 `SELECT` 查询，你应该能够验证所有内容都已正确恢复。

该过程与 `PostgreSQL` 完全一致。首先，使用 `psql` 切换到 `pgsql` 用户，如果数据库不存在，则创建它（使用 `createdb`，如你之前所示）。然后启动 `psql` 并读取 `.sql` 文件：

```bash
$ psql < /usr/local/www/db/PictureArchive.sql
```

如果一切顺利，你应该已经恢复正常运行了。

## 设计可恢复性

然而，备份/恢复过程并不完美。因为命令和表是从系列命令重新创建的，而且由于这些命令是由转储程序自动生成的，可以想象，你手动设置的配置可能无法通过自动化工具重建。

一个增加复杂性的因素（特别是在 `MySQL` 中）是 `AUTO_INCREMENT`。这种特殊的 `INT` 列定义上必须是主键、唯一的（`UNIQUE`）且非空的（`NOT NULL`）。理想情况下，你应该手动指定 `AUTO_INCREMENT` 列中的值；你最终会为每一行得到一个不同的正整数。

## 802 替代 FTP 服务器

- `vsftpd`, 738-739
- `WU-FTPD`, 738
- `amd` (自动挂载守护进程), PDF:892-893
- `amd.conf` 文件, PDF:893
- `ampersand` (&), 128, 328, 465
- `AND` 语句, 278, 290
- 匿名 `FTP`, 48, 731, 736
- `Apache` 项目, 693
- `Apache` 服务器, PDF:817
- 通过地址访问控制, 706-707
- 通过地址和密码访问控制, 711
- 通过密码访问控制, 708-710
- 组，添加, 710
- 用户，添加, 709-710
- `Apache-SSL`, PDF:818
- 使用 `apxs` 编译, 715-716
- 内置模块, 714
- `CGI` (通用网关接口), 720
- 直接访问, 725
- 通过表单访问, 722-725
- 启用, 721-722
- 示例 `Perl` 程序, 724-725
- `CGIWrap`, PDF:819-821
- 配置文件, 700-701
- `.htaccess`, 702-704
- `httpd.conf`, 702
- `magic`, 700
- `mime.types`, 700
- `srm.conf`, 700
- 动态模块, 714-715
- 文件布局, 699-700
- `HTTP` (超文本传输协议)
- `apachectl` 程序, 705-706
- `httpd`, 启动/停止, 704-706
- 请求, 694-696
- 响应码, 697
- 安装, 698-699
- `mod_perl` 模块, 716
- `mod_php` 模块, 716
