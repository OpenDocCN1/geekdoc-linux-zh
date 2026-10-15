
最后，我们为每个记录声明一个数字标识标记。这是表的核心。你正在创建一个名为 `id` 的列，它存储整数（`INT` 代表 integer）。此外，此列是主键，这意味着存储在此列中的信息决定了数据库存储数据的顺序。除非你指定其他数据排序方法，否则从数据库读取数据时，低 ID 会在高 ID 之前。

现在你已经知道了如何在 MySQL 服务器上创建简单 SQL 数据库的基础知识，你准备好使用 MySQL 客户端以外的方法与数据库交互了。

# 使用脚本与 SQL Server 交互

SuSE Linux 的强大之处在于编写小型脚本与 SQL 数据库交互非常简单。在 MySQL 数据库上输入的任何命令也可以通过程序或脚本给出。这使得你能够编写程序来选择、更新、删除或向数据库插入信息。你甚至可以编写程序为你创建表。本节提供了用于交互和显示表中数据的简单脚本示例。

这些程序用 Perl 脚本语言编写，因为它简单高效。所有脚本都使用 `DBI` 模块来处理数据库交互。

`DBI` 模块是一个抽象层。如图 16-1 所示，这意味着向 `DBI` 请求数据，而 `DBI` 模块处理任何特定于数据库引擎的内容。有了 `DBI`，迁移到不同的数据库也很容易。如果你需要超出 MySQL 能力的功能或性能，可以安装新数据库并更改 Perl 脚本中的一个单词。突然间，你就在一个全新的环境中运行了。Tim Bunce 编写了 `DBI`，你可以从 `http://cpan.perl.org/` 下载它。

# 第 16 章：结构化查询语言数据库服务

![](img/1d90939eac39ca76d12e353542e54751_462_0.png)

图 16-1：使用 `DBI` 模块作为抽象层

> 你可以使用 `CGI` 模块 (`CGI.pm`) 通过 Web 浏览器与用户交互。这是一个编写 CGI 脚本的优秀工具；它让你的代码更易读，并消除了从头开始编写一切内容的负担。由 Lincoln Stein 编写，你可以从 `http://cpan.perl.org` 下载。

现在来看几个使用之前提到的模块与 MySQL 服务器交互的脚本。

# 从 UNIX 命令行提示进行 SQL 交互

让我们创建一个名为 `inventory` 的简单数据库，其中包含一个名为 `machines` 的表，存储联系信息：别名、电话、地址和年龄。要创建此数据库和表，请执行以下步骤：

- 使用 `mysql -u username -p` 命令启动 MySQL 客户端。
- 在 mysql 提示符处，输入 `create inventory;` 创建 `inventory` 数据库。然后输入 `inventory` 开始使用该数据库。

3. 现在，输入以下行创建一个名为 `machines` 的表。

```sql
create table machines (
alias char(12) not null,
ip char(15),
canonical char(20),
owner char(40),
misc char(80),
stype int,
id int auto_increment primary key
);
```

4. 一旦输入了这些行，输入 `describe machines;` 在输出中查看该表的描述：

| Field | Type | Null | Key | Default | Extra |
|---|---|---|---|---|---|
| alias | char(12) | | | | |
| ip | char(15) | YES | | NULL | |
| canonical | char(20) | YES | | NULL | |
| owner | char(40) | YES | | NULL | |
| misc | char(80) | YES | | NULL | |
| id | int(11) | | PRI | 0 | auto_increment |

7 rows in set (0.01 sec)

5. 现在，你准备好在数据库中插入一些示例数据了。这里是 SQL `insert` 命令的示例：

```sql
insert into machines (id, alias, IP, machinename, owner,
misc, ostype) values ('0', "veracruz", "192.168.1.254", "veracruz.paunchy.net", "paul", "SuSE Linux box", 1);
```

```sql
insert into machines (id, alias, IP, machinename, owner,
location) values ('1', "chivas", "192.168.1.1", "chivas.paunchy.net", "bill", "SuSE Linux box", 1);
```

6. 一旦你使用所示 `insert` 命令输入了几记录，可以通过输入 `exit;` 命令退出客户端。

列表 16-1 显示了一个相对简单的脚本，用于检索并打印存储在数据库中的数据。该程序假设你有一个名为 `root` 且密码为 `iamnotanumber` 的用户。

该脚本可以在第二张光盘的以下位置找到：`/cdrom/extras/select.pl`。

# 列表 16-1：select.pl 文件

```perl
#!/usr/bin/perl
# select.pl
# 从 SQL 子串中选择项的命令行脚本
# 修改为匹配子串
use DBI;
# 定义 - 如果你使用不同的数据库，需要更改这些
$db = "inventory";
$table = "machines";
$user = "root";
$password = "iamnotanumber";
# 定义结束
# 告诉脚本我们将使用
# MySQL 数据库
$drh = DBI->install_driver('mysql');
# 连接数据库
$dbh = $drh->connect($db, $password);
# 检查是否连接成功
die "连接失败: $DBI::errstr" unless $dbh;
# 从用户获取输入
print "IP: ";
$ip = <STDIN>;
chomp($ip);
# 构建并执行 SQL 语句
$SQLstatement = "select alias, ip from table where ip = '$ip'";
$sth = $dbh->prepare($SQLstatement);
$howmany = $sth->execute();
die "未找到匹配的 $ip" unless $howmany > 0;
print "$howmany 结果在数据库中";
printf("%18s %20s %24s %20s\n", "ALIAS", "IP", "CANONICAL", "OSTYPE");
# 遍历所有结果并打印
for ($i = 0; $i < $howmany; $i++) {
    my ($SQLalias, $SQLIP, $SQLcanonical, $SQLotype) = $sth->fetch_array();
    printf("%17s %20s %20s %20s\n", $SQLalias, $SQLIP, $SQLcanonical, $SQLotype);
}
```
*(注：由于原文代码块逻辑在提供时存在部分错乱，翻译时已根据常见的 Perl 逻辑进行了对齐处理以保持可读性)*

# 第四部分：设置文件共享和数据库服务器

这是由于你对以下行代码进行了修改：

```
SQLstatement = "select alias, ip, canonical, from $table
where ip like \"%%$ip\";";
```

作为一个副作用，如果你在不输入 IP 地址的情况下运行程序，数据库中的每个条目都会被显示。如果你发现数据库中遗漏了某人怎么办？你需要一个脚本来询问你每个字段的内容，并将新行数据放入数据库中。列表 16-3 正是这样做的。你可以在第二张光盘（CD-ROM）get路径找到该脚本：`/cdrom/extras/insert.pl`。

列表 16-3：insert.pl 文件

```perl
#!/usr/bin/perl
# ---> insert.pl <-
# 用于向 SQL 数据库插入记录的命令行脚本
use DBI;
# 定义 - 如果你使用不同的数据库，需要更改这些内容
$db = "inventory";
$table = "machines";
$user = "root";
$password = "iamnotnumber";
# 定义结束
# 告诉脚本我们将使用
# MySQL 数据库
$drhr = DBI->install_driver('mysql');
# 建立数据库连接
$dbh = $drhr->connect($db, $user, $password);
```
