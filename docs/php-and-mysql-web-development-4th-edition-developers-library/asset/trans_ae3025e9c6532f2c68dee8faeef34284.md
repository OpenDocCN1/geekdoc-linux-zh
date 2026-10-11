
### 8.4.6.2 使用 FULLTEXT 索引执行搜索

```perl
if defined ($entry_ref->{state});
$address .= " . $entry_ref->{zip};
if defined ($entry_ref->{zip});
print "Address: $address"; br ()
if $address ne "";
print "Telephone: $entry_ref->{phone}"; br ()
if defined ($entry_ref->{phone});
print "Email: $entry_ref->{email}"; br ()
if defined ($entry_ref->{email});
print "Interests: $entry_ref->{interests}", br ()
if defined ($entry_ref->{interests});
print br ();
```

`html_format_entry()` 使用 `format_name()` 函数将 `first_name`、`last_name` 和 `suffix` 列的值拼接在一起。它与 `gen_dir.pl` 脚本中同名函数的功能完全相同。

历史上的联盟成员可能拥有多个兴趣。如果有多个兴趣，它们在 `member` 表的 `interests` 列中用逗号分隔。例如：
`Revolutionary War,Spanish-American War,Colonial period,Gold rush,Lincoln`

你能使用 `ushl_browse.pl` 来搜索匹配多个关键词中任意一个的行吗？某种程度上可以，但实际上并不行。你可以在搜索表单中输入多个单词，但除非你构造一个更复杂的查询，要求每个单词都匹配，否则行不会匹配。处理兴趣搜索任务的一种更灵活的方式是使用 `FULLTEXT` 索引。本节描述了一个执行此操作的脚本 `ushl_ft_browse.pl`。有关 MySQL `FULLTEXT` 功能的更多信息，请参阅第 2.15 节“使用 FULLTEXT 搜索”。

在使用 `member` 表进行 `FULLTEXT` 搜索之前，它必须是一个 MyISAM 表。如果你使用其他存储引擎创建了 `member` 表，请使用 `ALTER TABLE` 将其转换为 MyISAM 表：
`ALTER TABLE member ENGINE = MyISAM;`

接下来，有必要正确地为 `member` 表建立索引。为此，请使用以下语句：
`ALTER TABLE member ADD FULLTEXT (interests);`

这使得 `interests` 列可以被用于 `FULLTEXT` 搜索。`sampdb` 发行版中的 `ushl_ft_browse.pl` 脚本基于 `ushl_browse.pl`，两者仅在构建搜索查询的 `search_members()` 函数上有所不同。该函数的修改版本如下所示：

```perl
sub search_members (
my ($dbh, $interest) = @_;
print p ("Search results for keyword: " . escapeHTML ($interest));
my $sth = $dbh->prepare (qq{
    SELECT * FROM member WHERE MATCH(interests) AGAINST(?)
    ORDER BY last_name, first_name
});
# look for string anywhere in interest field
$sth->execute ($interest);
my $count = 0;
while (my $ref = $sth->fetchrow_hashref ())
{
    html_format_entry ($ref);
    ++$count;
}
print p ("Number of matching entries: $count");
```

与之前相比，这个版本的 `search_members()` 有以下变化：
-   查询使用 `MATCH() ... AGAINST()` 而不是 `LIKE`。
-   不再向关键词字符串添加 `%` 或 `*` 通配符字符以将其转换为模式。

通过这些更改，你可以从 Web 浏览器调用 `ushl_ft_browse.pl`，并在搜索表单中输入多个关键词（无论是否有逗号）。该脚本将找到匹配其中任何一个的成员条目。

你可以让该脚本变得更加复杂。一种可能性是利用 `FULLTEXT` 搜索可以一次搜索多个列的事实，通过设置索引跨越多列，然后修改 `ushl_ft_browse.pl` 以搜索所有这些列。例如，你可以删除原始的 `FULLTEXT` 索引，并添加另一个使用 `last_name` 和 `first_name` 列（除 `interests` 列外）的索引：

```sql
ALTER TABLE member DROP INDEX interests;
ALTER TABLE member ADD FULLTEXT (interests,last_name,first_name);
```

要使用新索引，请修改 `search_members()` 函数中的 `SELECT` 语句，将 `MATCH (interests)` 更改为 `MATCH(interests,last_name,first_name)`。你可能对 `ushl_ft_browse.pl` 做的另一个更改是在表单中添加两个单选按钮，以便用户可以选择“匹配任意关键词”和“匹配所有关键词”模式。“匹配任意”模式是脚本当前使用的模式。要实现“匹配所有”模式，请更改语句以使用 `IN BOOLEAN MODE` 类型的 `FULLTEXT` 搜索，并在每个关键词前加上“+”字符，以要求它在匹配的行中存在。有关布尔模式搜索的信息，请参阅第 2.15.2 节“布尔模式 FULLTEXT 搜索”。

## 9 使用 PHP 编写 MySQL 程序

PHP 是一种脚本语言，用于编写包含嵌入代码的 Web 页面，这些代码在访问页面时执行，并可以生成动态内容作为发送给客户端 Web 浏览器输出的一部分。本章描述了如何编写使用 MySQL 的基于 PHP 的 Web 应用程序。有关 PHP 与 C 和 Perl DBI API 在 MySQL 编程中的比较，请参阅第 6 章“MySQL 编程入门”。

本章中的示例基于我们的 `sampledb` 示例数据库，使用第 1 章“MySQL 入门”中为成绩管理项目和历史联盟创建的表。这里描述的应用程序应在 PHP 5 或更高版本下运行。

本章使用 PHP 5.1 及更高版本的类常量表示法引用 PDO 常量（例如，`PDO::FETCH_NUM`）。对于 PHP 5.0，请使用全局常量表示法（例如，`PDO_FETCH_NUM`）。

本章假设你将使用 PHP 与 Apache Web 服务器配合使用，尽管你可能可以替换为其他服务器。此外，PHP 当前必须链接到 MySQL C 客户端库进行构建，否则它将不知道如何访问 MySQL 数据库。（当 `mysqli` 变得可用时，如前所述，这一要求将被取消。）如果你需要获取此软件中的任何部分，请参阅附录 A“获取和安装软件”。该附录还提供了获取包含本章开发的示例脚本的 `sampledb` 发行版的说明。你可以下载这些脚本，以避免自己输入。你将在本章脚本的 `phpapi` 目录下找到它们。

在 Unix 下，PHP 可以作为 Apache 模块使用，也可以作为独立的解释器（作为传统的 CGI 程序）使用。在 Windows 下，除非使用 Apache 2.x，否则 PHP 只能作为独立程序运行。在这种情况下，你有选择将 PHP 作为 Apache 模块运行的选项。在任一平台上，出于性能原因，作为模块运行 PHP 是更可取的。

PHP 提供了与 MySQL 接口的几种方式：
-   在 PHP 5 及更高版本中，你可以使用“MySQL 改进”扩展，`mysqli`。此扩展提供两种调用风格。你可以将其用作一组名称形式为 `mysqli_xxx()` 的函数，或通过面向对象接口使用。
-   `mysql` 扩展是 MySQL 的原始接口。它由名称形式为 `mysql_xxx()` 的函数组成。在大多数情况下，这些直接映射到具有相同名称的 C API 函数。此扩展没有面向对象接口。`mysql` 的能力不如 `mysqli`，不仅因为它的调用风格灵活性较差，而且因为它不提供对 MySQL 4.1 及更高版本开发的功能的访问。`mysql` 是在 MySQL 4.1 之前开发的，可能应该被视为已弃用。
-   其他接口与特定的数据库引擎的绑定较少。本章使用 PHP 数据对象 (PDO)，这是一个扩展，提供类似于 Perl DBI 模块设计的面向对象、数据库无关接口。它使用两级架构，其中顶层呈现统一接口，底层由各种数据库引擎的驱动程序组成。要从一个驱动器切换到另一个，你修改传递给连接调用的参数，使其适合你想要使用的驱动器。

PDO 要求 PHP 5.0 或更高版本，因为它使用了旧版本 PHP 中不可用的面向对象特性。

`mysql` 和 `mysqli` 扩展以及 MySQL 的 PDO 驱动器最初设计为链接到 MySQL C 客户端库（附录 G“C API 参考”中描述的 `libmysqlclient` 库 [在线]）。这种设计的一个后果是，如果你想安装 PHP 以访问 MySQL 数据库，它会引入 PHP 对 MySQL 发行版的一部分的依赖。一个较新的库 `mysqlnd` 正在开发中，可以作为 `libmysqlclient` 的替代品。`mysqlnd` 是一个原生驱动程序，实现相同的通信协议，但不需要 MySQL 发行版的任何部分。从 PHP 5.3 版本开始将包括 `mysqlnd`，这意味着可以在不安装 MySQL 客户端库的情况下从 PHP 访问 MySQL 数据库。

在大多数情况下，本章仅描述讨论所需的 PDO 对象和方法。它还仅涵盖 PDO 的 MySQL 驱动器。其他数据库引擎的驱动器也可用，但这里不讨论。有关 PDO 接口的更完整列表，请参阅附录 I“PHP API 参考”（在线）。你也可能想查阅 PHP 手册，它描述了所有 PHP 功能。手册可从 PHP 网站获取：http://www.php.net/。

PHP 脚本的文件名通常以一个后缀结尾，该后缀使你的 Web 服务器能够识别它们应通过调用 PHP 解释器来执行。如果你使用服务器不识别的后缀，它将把你的 PHP 脚本作为纯文本提供。本章中的脚本使用 `.php` 后缀。有关配置 Apache 以识别你想使用的后缀的说明，请参阅附录 A。（如果你没有控制你机器上的 Apache 安装，请与系统管理员联系以了解正确的后缀
