
# 15.3 MySQL 入门

## 删除列

示例 15.18 展示了如何使用 `ALTER TABLE` 命令中的 `DROP` 子句从表中删除一列。

### 示例 15.18

```
mysql> ALTER TABLE teams DROP captain;
Query OK, 11 rows affected (0.34 sec)

Records: 11  Duplicates: 0  Warnings: 0
```

## 添加主键

在示例 15.19 中，通过使 *name* 字段成为主键来修改 *teams* 表。这意味着所有新加入的球队必须有唯一的名称。

### 示例 15.19

```
1 mysql> ALTER TABLE teams MODIFY name VARCHAR(100) NOT NULL,
  -> ADD PRIMARY KEY(name);
Query OK, 10 rows affected (0.06 sec)

Records: 10  Duplicates: 0  Warnings: 0

2 mysql> DESCRIBE teams;
+--------+---------------+------+-----+---------+-------+
| Field  | Type          | Null | Key | Default | Extra |
+--------+---------------+------+-----+---------+-------+
| name   | varchar(100)  | NO   | PRI | NULL    |       |
| wins   | int(10) unsigned| YES |     | NULL    |       |
| losses | int(10) unsigned| YES |     | NULL    |       |
+--------+---------------+------+-----+---------+-------+
3 rows in set (0.05 sec)
```

## 删除表

删除表相对简单。只需使用 `DROP` 命令并加上表名即可。

### 示例 15.20

```
mysql> DROP TABLE teams;
Query OK, 5 rows affected (0.11 sec)
```

## 删除数据库

要删除数据库，请使用 `DROP DATABASE` 命令。

### 示例 15.21

```
mysql> DROP DATABASE sample_db;
Query OK, 1 row affected (0.45 sec)
```

# 15.4 什么是 Perl DBI？

DBI 是应用程序与一个或多个数据库驱动模块之间的“胶水”层。

> —Tim Bunce，DBI 的作者

**DBI 代表数据库独立接口（Database Independent Interface）。** DBI 是一个面向对象的模块，它允许你的 Perl 应用程序使用相同的方法调用、变量和约定与许多不同类型的数据库进行通信。它会定位特定数据库系统的数据库驱动模块（DBD），并动态加载相应的 DBD 模块。数据库驱动包含与特定数据库通信所需的库。例如，要连接到 MySQL 数据库，你需要安装 DBD-MySQL 驱动；而要连接 Oracle 数据库，则需要 DBD-Oracle 驱动。

DBI 充当你的 Perl 脚本与数据库驱动模块之间的接口；也就是说，它将 Perl 输出翻译成特定驱动（无论是 Oracle、Sybase、MySQL 还是其他驱动）能理解的代码（参见图 15.19）。你设置 SQL 查询字符串，并通过 DBI 方法将其发送给适当的数据库驱动，然后获得可以在 Perl 程序中以相同方式管理的结果，无论使用什么数据库都是如此。关于 DBI 作者 Tim Bunce 的优秀教程，请访问 http://www.slideshare.net/TimBunce/dbi-advanced-tutorial-2007。

![](img/8556abcb353c0991f12099420ec28735_585_0.png)

**图 15.19** DBI 和驱动。

## 15.4.1 安装 DBD 驱动

**使用 PPM 安装 DBD-MySQL。** 对于最近大多数版本的 Perl，DBI 模块已包含在标准 Perl 库中，但可以在 CPAN 上获取用于 UNIX、Mac 和 Linux 的 DBD-MySQL 驱动。（Strawberry for Windows 包含了该驱动。）有关在 Mac 上获取 mysql 驱动的说明，请访问 http://bixsolutions.net/forum/thread-8.html。

安装 DBI 或任何 DBD 驱动的一个简单方法是使用 PPM，这是 ActiveState 提供的一个包管理实用工具，简化了 Perl 模块的查找、安装、升级和移除。要获取 PPM 的完整教程，请访问 http://docs.activestate.com/activeperl/5.10/faq/ActivePerl-faq2.html。

为了使用 PPM，首先确保你的计算机已连接互联网。你还必须能够访问 PPM 存储库，无论是在本地硬盘、网络上，还是通过访问已挂载的 ActiveState ActiveDVD。请记住，如果互联网连接通过防火墙或代理，你可能需要设置 http_proxy 环境变量。

访问 Solaris PPM 存储库需要 ActivePerl Business Edition 许可证。

要在命令行启动 PPM，可以输入以下命令：

```
ppm
```

当 Perl 包管理器首次显示时，它会从数据库同步 ActiveState 存储库的包列表。你可以查看当前安装的所有包或存储库中的所有包，并使用搜索框查找你正在查找的模块。如果找到，它将被高亮显示（参见图 15.20）。

![](img/8556abcb353c0991f12099420ec28735_586_0.png)

**图 15.20** 标记为安装的包。

PPM 窗口顶部工具栏上的小图标表示一旦你从存储库中选择一个包后可以执行的操作。通常，你选择包，将其标记为安装，然后点击工具栏右侧的绿色箭头。

### 在 Linux 上使用 PPM。

如果你使用 Linux，可以从 ActiveState 下载 Perl 5.18.2，文件格式为 *rpm*（RedHat 包管理器）文件或者 *tarfile*。下载 ActivePerl 的说明位于 http://www.activestate.com/activeperl。然后运行位于 *perl 目录* 中的 *install.sh* shell 脚本。运行安装脚本后，将你的 *PATH* 设置为 *perl* 目录。然后你可以使用 *PPM* 程序从 *CPAN* 安装模块，就像在 Windows 上一样。这比使用带有各种问题和疑问的 *CPAN* 要容易得多。

安装所需的软件包需要连接到互联网。要查看已安装的软件包，请键入以下命令：

```
\rpm -i Active-State......rpm
sh install.sh
```

### 从 CPAN 安装 DBD:mysql 驱动。

用于维护本地 Perl 发行版的主要工具是 *CPAN* 模块，用于访问综合 Perl 档案网络，即 *CPAN*。在附录 D“Perlbrew、CPAN 和 cpanm”中，你将找到如何使用 *cpan* 和 *cpanm* 安装模块的详细说明。

要安装 *DBD-mysql* 驱动，请在命令行提示符下输入以下命令：

```
$ cpan DBD::mysql
```

或者通过输入以下内容检查它是否已经存在：

```
$ perldoc -l DBD::mysql
```

## 15.4.2 DBI 类方法

*DBI* 模块是面向对象的，并附带许多方法和变量。该模块的文档列于下文。数据库对象被称为 **句柄（handles）**。数据库句柄连接到特定数据库，而语句句柄用于向数据库发送 SQL 语句。请注意，诸如 $dbh、$sth、$rc 等名称用于描述语句句柄、返回码、数据行等。（这些名称仅仅是文档中的约定；例如，$dbh 代表数据库句柄，$sth 代表语句句柄。）

```
$ perldoc DBI
Notation and Conventions
The following conventions are used in this document:
$dbh       Database handle object
$sth       Statement handle object
```

| 变量 | 描述 |
| :--- | :--- |
| $dbh | 驱动句柄对象（在应用程序中很少见到或用到） |
| $h | 上述句柄类型中的任意一种（$dbh、$sth 或 $dbh） |
| $rc | 通用返回码（布尔值：true=成功, false=错误） |
| $rv | 通用返回值（通常为整数） |
| @ary | 从数据库返回的值列表，通常是一行数据 |
| $rows | 处理的行数（如果可用，否则为 -1） |
| $fh | 文件句柄 |
| undef | NULL 值在 Perl 中由未定义值表示 |
| \%attr | 传递给方法的属性值哈希引用 |

请注意，如果删除了对数据库和语句句柄对象的所有引用，Perl 将自动销毁这些对象。

### NAME

DBI - Perl 的数据库独立接口

### SYNOPSIS

```
use DBI;
@driver_names = DBI->available_drivers;
@data_sources = DBI->data_sources($driver_name, \%attr);
$dbh = DBI->connect($data_source, $username, $auth, \%attr);


$rv = $dbh->do($statement);
$rv = $dbh->do($statement, \%attr);
$rv = $dbh->do($statement, \%attr, @bind_values);


$array_ref = $dbh->selectall_arrayref($statement);
$hash_ref = $dbh->selectall_hashref($statement, $key_field);


$array_ref = $dbh->selectcol_arrayref($statement);
$array_ref = $dbh->selectcol_arrayref($statement, \%attr);


$row_ary = $dbh->selectrow_array($statement);
$array_ref = $dbh->selectrow_arrayref($statement);
$hash_ref = $dbh->selectrow_hashref($statement);



$sth = $dbh->prepare($statement);
$sth = $dbh->prepare_cached($statement);



$rc = $sth->bind_param($p_num, $bind_value);
$rc = $sth->bind_param($p_num, $bind_value, $bind_type);
$rc = $sth->bind_param($p_num, $bind_value, \%attr);



$rv = $sth->execute();
$rv = $sth->execute(@bind_values);
$rv = $sth->execute_array(\%attr);



$rc = $sth->bind_col($col_num, $col_variable);
$rc = $sth->bind_columns(\@list_of_refs_to_vars_to_bind);
```
