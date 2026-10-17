
如果愿意，你可以在 `/usr/local/pgsql/data` 中创建一个名为 `admins` 的文件，每行包含一个数据库用户名；只有这些用户才被允许操作数据库。你可以对每个新创建的数据库执行相同操作——只需为每个数据库添加不同的文件，包含拥有该数据库的用户名，并用该文件名代替本例中的 `admins`。

或者，你可以执行一项策略，即本地用户无需密码仅能连接到他们自己的数据库（那些名称与用户名匹配的数据库）。例如，用户 `frank` 将拥有一个名为 “frank” 的数据库。可以通过以下配置行来实现：

```
local           all                                 ident  sameuser
```

### 编写管理脚本

你在我们飞速的数据库世界之旅中达到了下一个层次；既然示例数据库中的表已经设置好，我们现在可以超越交互式命令行，学习如何自动化一些较长且更繁琐的查询。MySQL 或 PostgreSQL 命令行对于设计和调试目的始终有用。然而，一些必须定期执行且需要长而复杂的查询的任务要求你找到一种更不令人沮丧的方式来完成任务。

Perl 和 Python 都提供工具包，你可以编写脚本与数据库进行接口。这些工具包使你能够发出查询、提取数据、处理数据并将数据反馈到系统中，这一切都在循环和条件等所有这些语言提供的程序化优势中完成。

#### 使用 Perl 进行数据库连接

作为便利措施，连接 MySQL 所需的 Perl 模块是随 MySQL 端口一起安装的。这些模块也位于 `/usr/ports/databases/p5-mysql`；文档可以通过 `perldoc Mysql` 阅读。

这些模块的关键部分是任何打算连接 MySQL 数据库的脚本的设置部分。这个设置块包括以下行，应该放在脚本的最顶部：

```perl
use Mysql;

$dbh = Mysql->connect(undef, "PictureArchive", "frank", "<frank's password>");
```

将这些行添加到脚本后，你就有了一个可供操作数据库句柄：`$dbh`。可以在此句柄上执行一系列操作；本章不会讨论所有操作——只讨论最重要的操作。你可以在 `perldoc Mysql` 文档中找到其余内容。

通过使用 `$dbh->query` 方法并将其设置为作为结果句柄的变量，向数据库发出任何类型的查询：

```perl
$query = $dbh->query("SELECT Filename, Type FROM Pictures WHERE User_ID='5'");
```

你现在可以使用 `fetchrow` 方法获取输出的第一行。这样工作，你可以不断调用 `fetchrow`（在循环中），直到没有更多输出；这就是你可以对数据库输出的每一行应用相同的 Perl 代码的方式，按照 SQL 查询指定的任何顺序：

```perl
while (@picdata = $query->fetchrow) {
    print "$picdata[0], $picdata[1]\n";
}
```

以下是其他可能有用的运算符列表：

- `$dbh->query`—使用此运算符围绕变量，以在查询中正确引用其内容；例如，为确保像 “Bob O'Shea” 这样的全名能够正确插入，而撇号不会在查询字符串中引起混淆，使用 `$dbh->query("INSERT INTO Users (Fullname) VALUES ('$dbh->quote($fullname)')");`。
- `$query->numrows`—这将返回 `$query` 中查询将返回的行数。
- `$query->insertid`—如果你的查询是 `INSERT` 并且表有一个生成了新 ID 的 `AUTO_INCREMENT` 列，此函数将返回该 ID，以便你在未来的查询中使用。

要在 Perl 中连接 PostgreSQL，你需要安装 `/usr/ports/databases/p5-Pg` 端口。此模块提供的功能与 p5-Mysql 模块非常相似；你可以使用以下命令设置数据库连接：

```perl
use Pg;

$conn = Pg::setdbLogin(undef, undef, undef, undef, "PictureArchive", "frank", "frank's password");
```

接下来，使用 `$conn->exec` 方法提交查询：

```perl
$result = $conn->exec("SELECT Filename,Type FROM Pictures WHERE User_ID='5'");
```

然后像本章前面看到的 MySQL 示例一样使用 `$result->fetchrow`。`$result` 句柄的所有可能性都可以在 `perldoc Pg` 文档中找到，在标题为 “2. Result” 的部分。

> **注意**
> 对于这两个连接包，示例描述在 *自动提交* 模式下执行的查询，这意味着每个查询一旦形成就立即发送到数据库（使用 `$dbh->query` 或 `$conn->exec`），结果立即可用于 `fetchrow` 命令。每个包都包含类似命令，可用于在查询不自动提交的模式下操作。这种方法对于必须 *原子*（即，*被视为不能被其他进程中断的单一指令*，这些进程可能会改变操作的开始和结束之间的数据库状态）的操作通常非常有用。原子操作被认为比非原子操作更安全，在可能的情况下使用它们是良好的数据库编码实践。关于每个包的每个数据库文档详情。

### 使用 Python 进行数据库连接

Python 的连接建立在 Python 数据库 API 规范 2.0 之上。除了设置行细节和连接本身如何设置外，访问 MySQL 和 PostgreSQL 数据库的命令语法是完全相同的。首先，构建并安装 `py-MySQLdb` 或 `py-pyPgSQL` 端口，两者都在 `/usr/ports/databases` 中，具体取决于你使用的是哪个数据库。

要设置到 MySQL 数据库的连接，使用以下初始化行：

```python
import MySQLdb

db = MySQLdb.connect(database="PictureArchive");
```

如果你使用的是 PostgreSQL，设置行将如下所示：

```python
from pyPgSQL import PgSQL

db = PgSQL.connect(database="PictureArchive");
```

前面的行设置了到数据库的连接。接下来，你可以使用 `db.cursor()` 运算符创建一个 *游标* 或语句句柄：

```python
cur = db.cursor()
```

现在你可以开始发出查询。Python 的数据库 API 默认为非自动提交模式，因此你可以在提交之前发出尽可能多的查询，如下所示：

```python
cur.execute("INSERT INTO Users (FullName,Age) VALUES ('Joe Smith', '22')")
cur.execute("INSERT INTO Users (FullName,Age) VALUES ('Alice Walker', '31')")
db.commit()
```

处理查询多行响应最简单的方法可能是使用 `fetchall` 命令，该命令会将所有结果行检索到一个多维数组中。以下行展示了如何使用此命令：

```
cur.execute( "SELECT * FROM Users" )
r = cur.fetchall()
r
[[Joe Smith, 22], [Alice Walker, 31]]
```

与 Perl 数据库连接模块类似，通过这些接口可以执行许多其他操作。欲了解这些功能的完整文档，请参见 Python 数据库 API 规范 2.0 站点（http://www.python.org/topics/database/DatabaseAPI-2.0.html）。

## 用于填充数据库的 Perl 脚本

在本节中，我们将查看一个用 Perl 编写的简单脚本。此脚本与 MySQL 数据库进行交互。它的目的是读取目录中的一组文本文件，每个文件包含系统中特定用户的信息。该脚本将解析每个文件，这些文件具有以下格式：

- 用户的完整姓名
- 用户的电子邮件地址
- 用户的年龄

然后，它将使用 `AUTO_INCREMENT` 列将每个用户插入到数据库的 Users 表中，为每个用户创建唯一的 ID 编号，最后在所有操作完成后返回表中的行数。该脚本如清单 28.1 所示，并作为 `populateUsers.pl` 包含在 CD 中。

### 清单 28.1 populateUsers.pl—用于填充数据库 Users 表的 Perl 脚本

```perl
#!/usr/bin/perl

use Mysql;

$filepath = "/usr/local/www/data/users";
```
