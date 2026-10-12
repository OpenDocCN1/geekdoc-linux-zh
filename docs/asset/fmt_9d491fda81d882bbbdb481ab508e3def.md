
我们创建了 `book_information` 表，并设置了一个主键，或者说一个相对于该字段所有其他值都具有唯一值的字段。我们决定使用 ISBN 作为键（`isbn`），因为它们是唯一的，所以非常适合这个用途，几乎就像它们是专为此设计的一样。

> 为 apache 用户授予此新数据库的权限：

```mysql
mysql> USE mysql;
Reading table information for completion of table column names
You can turn off this feature to get a quicker startup -A

Database changed
mysql> GRANT SELECT, INSERT, UPDATE, DELETE
-> ON books;
-> TO apache@localhost;
Query OK, 0 rows affected (0.00 sec)
```

注意，这次 `GRANT` 命令不需要使用 `IDENTIFIED BY` 来设置密码——在第 5 章第一次执行 `GRANT` 时，我们已经设置过 apache MySQL 用户的密码。

好了，现在表已经准备好了，需要填充数据了。我们已经有一个包含所有书籍的平文件，我们费了很大精力才输入的，所以如果能将这些数据传输到数据库就太好了。别担心——Perl 和 DBI 会来救场！重新格式化和传输数据是 Perl 非常擅长的领域之一。

`book.pl` 程序将书籍信息平文件的内容存入数据库：

我们可以使用 `mysqlimport` 命令来输入数据，因为 `book.data.txt` 是一个格式良好的、制表符分隔的文件。但使用 Perl 要有趣得多。详细信息请参见 `mysqlimport --help`。

# 第 8 章 mod.perl

```perl
#!/usr/bin/perl -w
# book.pl

use strict;
use DBI;

# 连接到数据库
my $dbh = DBI->connect('DBI:mysql:books', 'apache', 'LampIsCool')
or die "Can't connect: " . $dbh->errstr();

# 打开数据文件
open FH, $sth, '/var/www/misc/book.data.txt' or die $!;

my($line, $sth);
 # 遍历文件的每一行
while ($line = <FH>) {

    chomp($line);

    # 将行拆分为一些变量
    my($isbn, $author, $title, $publisher, $date, $description, $price) = split /\t/, $line;

    # 移除价格中的 $ 符号
    $price =~ s/^\$//;

    # 准备插入的 SQL
    $sth = $dbh->prepare('INSERT INTO book_information
(isbn,
    author,
    title,
    publisher,
    date,
    description,
    price
) VALUES (
    ?,
    ?,
    ?,
    ?,
    ?)') or die "Can't prepare SQL: " . $dbh->errstr();

# 执行查询，传递变量以填充
# 查询中的占位符
$sth->execute($isbn, $author, $title, $publisher, $date,
$description, $price)
or die("Can't execute SQL: " . $sth->errstr);
```

}

```
# 关闭文件，结束并断开
close FH
```

```
$sth->finish();
$dbh->disconnect();
```

脚本首先告诉 Perl `DBI` ；然后连接到 `books` 数据库如果失败则 `die`。它使用 `open()` 函数打开包含书籍的文件，如果打开失败则 `die`。

随后脚本遍历文件，在去掉换行符并按制表符分割后，将数据插入数据库。由于价格带有前面的美元符号，因此使用 `s///` 语句将其移除。

脚本构建用于插入数据的 SQL 查询，并调用 `execute()` 传入正确的变量，以填充查询中的占位符。

最后，按照良好的习惯，关闭文件，结束语句处理并断开数据库。现在运行程序：

```bash
$ book.pl ./book.pl
```

现在数据库已经填充了数据，所以是时候讨论显示数据库信息的 mod.perl 程序了。

首先，查看生成书籍列表的文件 `/var/www/mod.perl/BookListingMys.pm` 中的代码。完整代码请参见 http://localhost/mod/perl/BookListingMys.pm 或 opensourcewebhook.com/mod/perl/BookListingMys.pm。

这段代码的目的是以美观、易读的方式通过表格显示数据。程序的操作是首先连接到 MySQL 服务器，查询数据库读取书籍数据的子集（因为一次显示书籍太多，我们一次显示十本），并构建表格。

# 262

# 第三部分 动态

接下来，将 `html()` 函数设置为 `text/html`，发送标头，并调用 `top.html()` 函数来构建顶部和左侧边栏的 HTML；然后打印该 HTML。

现在进入连接数据库的代码，我们将获取所有的 ISBN：

```perl
# 连接到数据库，如果连接失败，
# 调用 handle_error()，返回其返回值：OK
my $dbh = DBI->connect('DBI:mysql=books', 'apache', 'LampIsCool')
or return handle_error($r, 'Connecting to db failed: ' . $dbh->errstr());
```

```perl
# 首先，我们需要获取所有的 ISBN 号，这样我们就能
# 抓取我们的页面 -
# 准备 SQL 语句，如果失败则处理错误 - 我们
# 将变量 $dbh 传递给 handle_error，以便它可以从数据库中断开连接
my $sth = $dbh->prepare('SELECT isbn FROM book.information
ORDER BY isbn');
```

```perl
or return handle_error($r, 'Prepare of SQL failed: ' . $$->errstr(), $dbh);
```

```perl
or return handle_error($r, 'Execute failed: ' . $sth->errstr(), $dbh, $sth);
```

```perl
# 声明一些变量
my @isbn = ();
my $isbn;
```

```perl
# 获取行
while (($isbn) = $sth->fetchrow()) {
    push @isbn, $isbn;
}
```

第一个 DBI 操作是连接数据库并检索所有书籍的 ISBN。所有 ISBN 都存储在 `@isbn` 数组中，这样就可以抓取其中的一个范围（例如 30-39 号）。

```perl
# 此代码打印所有书籍信息页面的导航
# - HTML 看起来类似于：
# 1 | 2 | 3 | 4 | 5
# 如果用户点击 '3'他们将进入下一页
### 书籍
my $bgcolor = '';
```

```perl
for ($i = 0; ($i+1)*NUM_BOOKS <= scalar(@isbn); $i++) {
    if ($i != 0) {
```

# 第 8 章 mod perl 263

```perl
$r->print('|');
if ($i * $NUM_BOOKS == $first_book) {
    $r->print($i + 1);
} else {
    $r->print("<a href=/booklisting?first=$isbn[$i]"><font color=\"999966\"><b>" . ($i + 1) . " </b></font></a>");
}
```

此代码打印用于页面导航的 HTML（例如书籍信息 1–10，11–20 等）。在示例示例中，我们查询数据库获取 ISBN，遍历查询结果，并将每个 `isbn` 推送到 `@isbn` 数组中。

```perl
# 打印我们表格的初始 HTML
$r->print("<<HTML>");
<table border="0" cellspacing="0" cellpadding="3">
<tr><th>Title（标题）</th><th>Author（作者）</th><th>Price（价格）</th></tr>
EOHTML;
```
