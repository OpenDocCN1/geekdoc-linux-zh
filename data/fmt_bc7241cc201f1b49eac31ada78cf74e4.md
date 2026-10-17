
```perl
use MySQL;
$dbh = MySQL->connect(undef, "PictureArchive", "frank", "franks-password");
```

在将这些行添加到脚本后，你就有了一个可以操作的数据库句柄：`$dbh`。可以在此句柄上执行全系列操作；本章没有讨论所有的操作——只讨论最重要的操作。你将在 `perdoc MySQL` 文档中找到其余。

# 编写管理脚本 779

使用 `$dbh->query` 方法向数据库发布任何类型的查询，并将其赋值给结果句柄的变量：

```perl
$queryh = $dbh->query("SELECT Filename,Type FROM Pictures WHERE User_ID='5'");
```

你现在可以使用 `fetchrow` 方法获取输出的第一行。其工作原理是你可以不断调用 `fetchrow`（在循环中），直到没有更多输出；这就是你如何将相同的 Perl 代码应用到数据库输出的每一行，无论 SQL 查询指定的顺序是怎样的：

```perl
while (($filename, $filetype) = $queryh->fetch) {
    print "$filename, $filetype\n";
}
```

以下是其他可能实用的运算符列表：

## Perl 和 PostgreSQL

要在 Perl 中连接到 PostgreSQL，你需要安装 `/usr/ports/databases/p5-pg` 端口。该模块提供的功能与 `p5-MySQL` 模块相同；你可以通过以下命令设置数据库连接：

```perl
use Pg;
$conn = Pg::connect(undef, "PictureArchive", "frank", "franks-password");
```

（此处对应示例）

接下来，使用 `$conn->exec` 方法提交查询：

```perl
$result = $conn->exec("SELECT Filename,Type FROM Pictures WHERE User_ID='5'");
```

然后使用 `fetchrow`（如之前在 MySQL 中所示）。你可以在 Pg 文档中找到这些可能性。

> 注意：对于这些连接包，示例描述了在自动提交模式下执行查询，这意味着一旦公式化（`$db->query` 或 `$conn->exec`），结果立即可用 `fetchrow` 命令。

## 使用 Python 进行数据库连接

Python 的连接是基于 Python API 2.0 构建的。除了设置行的细节和连接设置之外，访问 MySQL 和 PostgreSQL 数据库的语法完全相同。首先，构建 `py-MySQL` 或 `py-PySQL` 端口，都在 `/usr/ports/databases` 下，取决于你使用的数据库。

设置 MySQL 数据库，使用以下初始化行：

```python
import MySQLdb
db = MySQLdb.connect(database="PictureArchive")
```

如果你使用 PostgreSQL，设置行如下：

```python
from psycopg2 import PgSql
db = PgSql.connect(database="PictureArchive")
```

前面的行设置了数据库连接。接下来，你可以使用 `db.cursor()` 创建游标（或语句句柄）：

```python
cur = db.cursor()
```

现在你可以开始查询。Python 的数据库 API 默为非自动提交模式，因此可以在提交之前发布尽可能多的查询，如下所示：

```python
cur.execute("INSERT INTO Users (FullName,Age) VALUES(\'Joe Smith', '22')")
cur.execute("INSERT INTO Users (FullName,Age) VALUES(\'Alice Walker', '31')")
db.commit()
```

处理查询的多行响应最简单的方法是使用 `fetchall` 操作，它将检索所有结果到一个多维数组中。以下展示了如何使用此命令：

### 编写管理脚本 781

```python
cur.execute("SELECT * FROM Users")
r = cur.fetchall()
[[Joe Smith, 22], [Alice Walker, 31]]
```

与数据库连接的 Perl 模块一样，通过这些接口可以执行大量的操作。请参阅 Python Database API 规范 2.0 （http://www.python.org/topics/database/DatabaseAPI-2.0.html）获取这些功能的完整文档。

## 用于填充数据库的 Perl 脚本

在本节中，你将看到一个用 Perl 编写的简单脚本。该脚本与 MySQL 数据库交互。它的目的是读取一个目录中的一组文本文件，每个文件都包含系统中特定用户的信息。该脚本将解析每个文件，其格式如下所示：

- 用户全名

- 用户邮箱地址

- 用户年龄

然后，它会将每个用户插入到数据库的 Users 表中，并使用 `AUTO_INCREMENT` 列为每个用户创建唯一 ID，最后在所有操作完成后，返回表中的行数。该脚本如列表 29.1 所示。

### 列表 29.1 populateUsers.pl：用于填充数据库 Users 表的 Perl 脚本

```perl
#!/usr/local/bin/perl

use MySql;
$dbh = Mysql->connect(undef
```

### 列表 29.1 续

```php
$num++;
}

$Scount = $dbh->query("SELECT ID FROM Users");
$Scount = $Scount->numrows;
print("There are $Scount users in the table, $num of which are newly added.\n");
?>
```

> 注意

通常认为直接动态生成内容是一种不好的做法；相反，你的管理脚本应该生成一个 .sql 文件（一组 SQL 命令的“配方”），然后你再将其加载到数据库中。

## 将数据库连接到网络

在本章中目前为止讨论的所有内容并非专门与 Web 相关。你通过系统本地用户设置的数据库、通过管理脚本管理的数据库，以及如果配置当，还可以由其他机器上的数据库客户端远程访问。但大多数数据库的建立是为了让 Web 浏览器能够访问其内容。幸运的是，由于你现在已经学习了理解数据库连接所需的所有基本概念，迈出下一步应该是轻而易举的。

## 使用 Perl 和 CGI 数据库内容

如第 11 章“Perl 编程简介”和第 26 章“配置 Web 服务器”中所讨论，通用网关接口（CGI）是一种标准的 API，通过它，数据（存储在变量中）从 Web 表单传递到后端程序，后端程序处理数据并返回给 Web 服务器。只要确保以下几点，任何 Perl 脚本都可以变成可以工作的 CGI 程序：

- 它的权限设置正确。

- 它位于 Web 服务器可以访问的位置。

- 它在输出内容之前打印出适当的 HTTP 头部。

用 Python、C 或任何其他语言编写的程序也是如此。为了后续讨论的，我们将使用 Perl。

你已经看到过如何创建一个与 MySQL 或 PostgreSQL 后端交互的 Perl 脚本。而且，你已经见过（在第 26 章中）如何创建一个可以处理通过 Web 表单提交的数据的 Perl 脚本。创建一个同时完成这两项任务的脚本只需合并这两种脚本的功能。接下来的章节将解释如何实现这种合并。

## 向数据库插入数据

假设你有一个 Web 表单，可以接收用户信息（与你之前在 Users 表中看到的字段相同），并将这些信息传递给 CGI 程序，然后该程序将信息字段插入数据库中。要实现这一点，你只需要确保脚本配置为处理表单输入以及数据库连接即可。操作方法如下：

```perl
#!/usr/local/bin/perl

use MySql;
$dbh = Mysql->connect(undef, "PictureArchive", "frank", "password");

read(STDIN, $buffer, $ENV{CONTENT_LENGTH});
@pairs = split(/=/, $buffer);
foreach $pair (@pairs) {
    ($name, $value) = split(/=/, $pair);
    $value = tr/\+/ //;
    $value = s/%%([a-fA-0-9])([a-fA-0-9])/pack("C", hex($1))/eg;
    $value = s/\!/!/g;
    $FORM{$name} = $value;
}

print "Content-type: text/html\n\n";
```
