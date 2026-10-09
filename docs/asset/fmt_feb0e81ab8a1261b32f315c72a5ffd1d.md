
| linux-modules-extra | kernel modules for version | 7860902563 |
| linux-modules-extra | kernel modules for v | 41721659017 |
| libreoffice-common | office productivity suite | 3551165846 |
| gnome-accessibility | GTK+2 theme and i | 3464371362 |
| ubuntu-common | additional terminal | 3025375593 |
| ncurses-term | | 2727198743 |
| manpages-dev | Manual pages about gu | 2120219260 |
| linux-firmware | for Linux kernel | 19383314725 |
| vim-runtime | Runtime | 16422794132 |
| codium | Code editing. Redefined. | 13072179108 |
| zsh-common | independent files f | 1256221607 |
| perl-modules-5.26 | | 1144180196 |
| adwaita-theme | default icon of GNOME (s) | 1127484878 |
| gimp-data | Data for GIMP | 10324501617 |

该查询运行需要一些时间（有很多工作要做），从结果可以看出它产生了 4 个包：包名、描述、包中的文件数量以及包的总大小。让我们拆解这个查询看看它是如何工作的。在最顶层我们看到了 `SELECT` 语句的正常模式。

```sql
SELECT list_of_items FROM Package_Descriptions
ORDER BY total_files DESC
LIMIT 20;
```

基础结构很简单。有趣的是 `WHERE` 子句中的子查询：这 `list_of_items` 部分。我们知道列表是逗号分隔的输出，或者如果我们跟随逗号可以看到：

1. `package_name`
2. `description`
3. `(SELECT COUNT(file) FROM Package_Files WHERE Package_Descriptions.package_name = Package_Files.package_name) AS files`
4. `(SELECT SUM(size_bytes) FROM Package_Files WHERE Package_Descriptions.package_name = Package_Files.package_name) AS size`

在 `WHERE` 子句中使用子查询也是可能的。当我们使用 `subquery_demo2.sql` 时：

```sql
-- subquery_demo2.sql

-- 列出所有包含超过1000个文件的包

.mode column
.header on
.width 20 60
SELECT package_name, description
FROM Package_Descriptions
WHERE 1000 < (SELECT COUNT(file) FROM Package_Files)
```

当我们执行此操作时，得到以下结果：

```bash
me@linuxbox:~/adventure-sql sqlite3 adv-sql.sqlite < query_demo2.sql
package_name description

| package_name | description |
|---|---|
| adwaita-icon-theme | default icon of GNOME (small subset) |
| codium | Code editing. Redefined. |
| gimp-data | Data files for GIMP |
| gnome-accessibility | High Contrast GT+ 2 theme and icons |
| humanity-icon-theme | Humanity icon theme |
| inkscape | vector-based drawing program |
| libreoffice-common | office productivity suite |
| linux-firmware | Drivers for Linux kernel |
| linux-headers-4.15.0 | Linux kernel version 4.15.0 |
| linux-headers-4.15.0 | Kernel headers for version 4.15.0 on 64 bit x86 SM |
| linux-headers-4.15.0 | Header files to Linux kernel version 4.15.0... |
| linux-headers-4.15.0 | Kernel headers for version 4.15.0 on 64 bit x86 SM |
| linux-modules-4.15.0 | Linux extra modules for version 4.15.0 on 64 bit |
| linux-modules-4.15.0 | Linux extra modules for version 4.15.0 on 64 bit |
| linux-modules-extra | Linux extra modules for version 4.15.0 on 64 bit |
| manpages-dev | Manual pages about userLinux for development |
| ncurses-term | additional terminal type definitions |
| perl-modules-5.26 | Core modules |
| tzdata | time zone and daylight-saving time data |
| ubuntu-mono | Ubuntu Mono Icon |
| vim-runtime | Vi Improved Runtime files |
| zsh-common | architecture independent files for Zsh |
```

# 更新表

`UPDATE` 语句用于更改一个或多行中的值。我们将通过向 `sqlite3` 包中每个文件的大小添加 `100` 来演示这一点。首先，让我们看看包中的文件：

```sqlite
sqlite> mode column
sqlite> headers on
sqlite> width 50 10
sqlite> SELECT file, size_bytes FROM Package_Files
file> ... WHERE package_name = 'sqlite3';
```

| file | size_bytes |
|---|---|
| /usr/bin/sqldiff | 1103280 |
| /usr/bin/sqlite3 | 1260976 |
| /usr/share/doc/sqlite3.1.gz | 1261 |
| /usr/share/man/man1/sqlite3.1 | 356 |
| /usr/share/doc/sqlite3/changelog.Debian.gz | 35 |

接下来，我们更新表，为每个文件的大小增加 `100`：

```sqlite
sqlite> UPDATE Package_Files set size_bytes = size_bytes + 100
...> WHERE package_name = 'sqlite3';
```

当我们检查结果时，就能看到变化：

```sqlite
sqlite> SELECT file, size_bytes FROM Package_Files
...> WHERE package_name = 'sqlite3'
```

| 文件名 | 字节大小 |
| :--- | :--- |
| /usr/bin/sqldiff | 1103380 |
| /usr/bin/sqlite3 | 1261076 |
| /usr/share/doc/sqlite3/man1/sqlite3.1.gz | 1361 |
| /usr/share/man/doc/sqlite3/changelog.Debian | 135 |

最后，我们将从每行减去 `100`，将大小恢复到原始值。

```sql
sqlite> UPDATE Package_Files SET size_bytes = size_bytes - 100
WHERE package_name = 'sqlite3';
```

`UPDATE` 可以一次修改多个值。为了演示这一点，我们将创建一个名为 `Package_Stats` 的新表，并使用 `UPDATE` 来填充这些值。由于这有点复杂，我们将将其放在名为 `create_Package_Stats.sql` 的文件中。

```sql
-- create_Package_Stats.sql

DROP TABLE IF EXISTS Package_Stats;

CREATE TABLE Package_Stats (
  package_name VARCHAR(60),
  count INTEGER,
  tot_size INTEGER,
  min_size INTEGER,
  max_size INTEGER,
  avg_size REAL
);

INSERT INTO Package_Stats (package_name)
SELECT package_name
FROM Package_Descriptions;

UPDATE Package_Stats
SET count = (SELECT COUNT(file)
 FROM Package_Files
 WHERE Package_Files.package_name = Package_Stats.package_name),
tot_size = (SELECT SUM(size_bytes)
 FROM Package_Files
 WHERE Package_Files.package_name = Package_Stats.package_name),
min_size = (SELECT MIN(size_bytes)
 FROM Package_Files
 WHERE Package_Files.package_name = Package_Stats.package_name),
max_size = (SELECT MAX(size_bytes)
 FROM Package_Files
 WHERE Package_Files.package_name = Package_Stats.package_name),
avg_size = (SELECT AVG(size_bytes)
 FROM Package_Files
 WHERE Package_Files.package_name = Package_Stats.package_name);
```

该文件包含四个 `SQL` 语句。前两个语句用于创建新表，正如我们之前看到的。第三条语句是 `INSERT` 语句的变体形式。这种形式非常有用，它可以将值从一个表复制到另一个表。`INSERT` 将创建我们所需的所有行，但只填充 `package_name` 列。为了填充其余部分，我们使用 `UPDATE` 根据对 `Package_Files` 表的某些查询结果来填充剩余值。请注意，如果没有 `WHERE` 子句，`UPDATE` 将更改应用到每一行。

一旦构建了表，我们就可以检查它的内容。

```sql
sqlite> .width 25 -5 -10 -8 -10
sqlite> SELECT * FROM Package_Stats LIMIT 10;

| package_name | count | tot_size | min_size | max_size | avg_size |
| :--- | :--- | :--- | :--- | :--- | :--- |
| a2ps | 299 | 3455890 | 117 | 388096 | 11558.165 |
| accountservice | 136 | 261704 | 42 | 182552 | 1373.8942 |
| alisa-base | 11 | 91936 | 30 | 35532 | 828.28364 |
| acpi-support | 13 | 13896 | 6 | 4922 | 772.0 |
| acpid | 19 | 86126 | 15 | 52064 | 4532.94736 |
| adusser | 1 | 246658 | 7 | 37322 | 3045.10649 |
| demium-theuntu | 137 | 126759 | 25 | 120502 | 952.96111 |
| adwaita-icon-theme | 1127 | 4848678 | 30 | 87850 | 4027.27848 |
| aislierot | 316 | 1890864 | 47 | 281544 | 5983.74636 |
| alisa-base | 42 | 195295 | 24 | 34160 | 469.88095 |
```

我们稍后会在查看此表时再次回到这里。

# 删除行

删除行非常简单。在 `DELETE` 语句中使用 `WHERE` 子句来指定目标。我们将演示这一点，但首先 `SQLite` 支持一个非常巧妙的功能。

我们可以将输出模式更改为写入 `INSERT` 语句。让我们试一下。

```sql
sqlite> .mode insert Package_Files
```

如果我们使用这个 `.mode`，我们就是告诉 `SQLite` 我们想要指向指定表（在这种情况下是 `Package_Files`）的 `INSERT` 语句。一旦设置输出模式，我们就可以查看结果。

```sql
sqlite> SELECT * FROM Package_Files WHERE package_name = 'sqlite3';

INSERT INTO Package_Files VALUES('sqlite3',/usr/bin/sqldiff,1103380);

INSERT INTO Package_Files VALUES('sqlite3',/usr/bin/sqlite3,1261076);

INSERT INTO Package_Files VALUES('sqlite3',/usr/share/doc/sqlite3/copytext,1361);

INSERT INTO Package_Files VALUES('sqlite3',/usr/share/man/man/sqlite3.1.gz',3696);

INSERT INTO Package_Files VALUES('sqlite3',/usr/share/doc/sqlite3/changelog.Debian.gz,135);
```

我们重复这个 `SELECT`，但首先我们可以将输出格式更改为名为 `sqlite3.sql` 的文件。

```sql
sqlite> .output insert_sqlite3.sql
sqlite> select from Package_Files where package_name = 'sqlite3';
```

这将把 `INSERT` 语句流写入指定的文件。接下来，我们将通过执行不带输出文件的 `.output` 命令来查看标准输出。

```sql
sqlite> .output
```

# 234 SQL

现在让我们删除 `Package_Files` 表中的行。

```sql
sqlite> DELETE FROM Package_Files WHERE package_name = 'sqlite3';
```

通过再次运行查询，我们可以确认删除。

```sql
sqlite> .header on
sqlite> .column
sqlite> .width 25 -5 -10 -8 -10
sqlite> SELECT FROM Package_Files WHERE package_name = 'sqlite3';
```

由于我们使用了 `SQL` 恢复表，我们现在可以放入它们。行已经恢复。

```sql
sqlite> .read insert_sqlite3.sql
```

| package_name | file | size_bytes |
| :--- | :--- | :--- |
| sqlite3 | /usr/bin/sqldiff | 1103380 |
| sqlite3 | /usr/bin/sqlite3 | 1261076 |
| sqlite3 | /usr/share/doc/sqlite3/copytext | 1361 |
| sqlite3 | /usr/share/man/man/sqlite3.1.gz | 3696 |
| sqlite3 | /usr/share/doc/sqlite3/changelog.Debian.gz | 135 |

# 235 SQL

## 添加和删除列

`SQL` 提供了 `ALTER TABLE` 语句来修改表结构。为了演示这一点，我们将向表中添加几列并填充值。

`SQL` 还提供了另一个用于从表中删除列的 `ALTER TABLE` 语句。它的格式如下：

```sql
```
