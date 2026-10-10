

尽可能用 HTML 和 JavaScript 实现；然后使用 CGI 编程层来捕获更多特殊的情况。理想情况下，数据库本身不应该暴露于从这些上层传递下来的输入错误。

## 创建搜索表单

既然你已经知道如何从 Web 表单向数据库插入数据，那么你已经准备好实现一个具有更普遍实用性的功能：一个搜索表单。单个 HTML 输入字段（`$FORM{'keywords'}`）可以接受由空格分隔的任意单词集合。然后，其底层的 Perl 代码会将该字符串分解为其组成部分单词，并在数据库中搜索每个单词的匹配项。如果不止一个单词匹配某个条目，你希望为该条目获得更好的“得分”，并根据该得分对结果进行排序。更进一步，你希望按顺序为匹配所有关键词的条目增加权重。以下是创建后端代码以处理此类搜索表单的基本步骤：

1.  检查输入字段中是否有内容。然后，创建一个*临时表*，即仅存在于该程序执行期间并在 $dbh 会话结束时被删除的表。（这张名为 Queries 的表将保存你计划执行的所有查询——包括所有通配符。）
2.  将输入字段的内容拆分到 @querywords 数组中。
3.  创建 $comboquery，它将是一个由 % 通配符分隔的所有关键词组成的字符串；这将是一个应该按顺序匹配包含所有关键词的条目的查询术语。如果你搜索这个术语以及所有单独的关键词，其得分应反映所有单个单词的匹配项，加上其组合匹配的得分。因此，它应该是你的最高结果。在其末尾添加一个最终的 %，然后将其推入 @querywords 数组。
4.  遍历每个关键词，创建一个用 % 通配符包围该单词的变量，并对其进行引用以保护你的数据库。然后，将其插入到临时的 Queries 数据库中。

现在你有一个充满了待执行查询的表。

下面的示例展示了如何在 Perl 中执行这些步骤。我们从前面讨论过的表单处理前言开始；之后，你刚刚看到的步骤将在代码中的注释中指明。

```perl
#!/usr/bin/perl

use Mysql;

$dbh = Mysql->connect(undef, "PictureArchive", "fred", "fred's password");

read(STDIN, $buffer, $ENV{'CONTENT_LENGTH'});
@pairs = split(/&/, $buffer);
foreach $pair (@pairs)
{
    ($name, $value) = split(/=/, $pair);
    $value =~ tr/+/ /;
    $value =~ s/%([a-fA-F0-9][a-fA-F0-9])/pack("C", hex($1))/eg;
    $value =~ s/-/ /-1/g;
    $FORM{$name} = $value;
}

print "Content-type: text/html\n\n";

# Here begins the handling of the form input.
if ($FORM{'keywords'}) {            # Step 1
    $sth = $dbh->query("CREATE TEMPORARY TABLE Queries (Query VARCHAR(255))");
    @querywords = split(/\s/, $FORM{'keywords'});   # Step 2
    $comboquery = $FORM{'keywords'};      # Step 3
    $comboquery =~ s/\s+/%/g;
    push (@querywords, $comboquery);
    foreach (@querywords) {              # Step 4
        $s_ = $dbh->quote('%'.$s_.'%');
        $sth = $dbh->query("insert into Queries (Query) VALUES ($s_)");
    }
}
```

现在，你可以执行查询。在这里，你正在 Pictures 中搜索文件名，且唯一的图片由 User_ID 和 Filename 共同定义，因此我们将按这两个字段分组。你将对结果的 COUNT() 称为 Score，并按该列降序排序：

```sql
$search = $dbh->query("SELECT Filename,User_ID,COUNT(Filename) AS Score
FROM Pictures WHERE Filename LIKE Query GROUP BY Filename,User_ID
ORDER BY Score DESC");
```

最后，你可以将每个结果行的内容分配给一个数组，并输出一些适当的 HTML 代码，你可以根据自己的喜好调整：

```perl
while (@searchdata = $search->fetchrow) {
    print "$searchdata[0] (Score: $searchdata[2])<BR>\n";
}
```

不言而喻，可以构建一个更复杂的搜索算法，甚至更容易设计一个更高效的算法。MySQL 有一个称为*全文索引*的概念，你可以定义一个 `TEXT` 字段具有 `FULLTEXT` 索引，然后你可以对该列进行专门化的搜索，具有极高的速度和效率。有关如何执行的详细信息，请参阅 MySQL 文档（[http://www.mysql.com/doc/en/Fulltext_Search.html](http://www.mysql.com/doc/en/Fulltext_Search.html)）。

> **注意**
>
> 请注意，`FULLTEXT` 搜索对于小于四个字母的关键词不起作用；由于索引代码针对非常大的数据集进行了最佳调整，因此在小型数据集上的搜索会产生非常奇怪的结果。

## 会话锁和数据完整性

如果你的 Web 应用程序有很多用户同时访问，重要的是要编码你的应用程序的数据库操作，使其尽可能具有原子性。正如我们之前讨论的，原子操作是指所有命令和响应都在单个指令中执行的操作，因此没有竞争进程可以干扰并可能导致你的操作执行期间数据库状态的变化。

MySQL 和 PostgreSQL 都支持*事务*的概念，在这种模式下，你不再以自动提交模式发出查询（即命令一输入就发送到数据库引擎，响应数据立即返回），而是通过使用 `BEGIN` 和 `COMMIT` 命令以及中间任意数量的查询操作来创建原子操作。这里展示了在事务中使用这些命令的方法：

```sql
BEGIN;
SELECT * FROM Users;
UPDATE User_Prefs SET Last_mod='Snow' WHERE Last_mod > 'Snow';
COMMIT;
```

在给出 `COMMIT` 命令之前，这些查询不会被执行，而在查询运行期间，正在使用的表会被锁定。当被锁定时，这些表不能被任何其他进程访问，这些进程必须等待此过程完成。

为了在 MySQL 中使用此类事务，你必须使用以下命令开始会话：

```sql
SET AUTOCOMMIT=0;
```

PostgreSQL 会在第一个 `BEGIN` 语句时自动退出自动提交模式。此外，如果你使用 Perl 或 Python 模块连接到 PostgreSQL，它将自动处于非自动提交模式。事实上，你可以选择在查询上下文中使用 `BEGIN` 和 `COMMIT` 方法，或者通过专用的数据库 API 命令来执行，它们做的是同样的事情。在 MySQL 中，事务是引擎中较新的增加，最容易直接作为 SQL 查询命令执行。

可以使用 ROLLBACK 命令代替 COMMIT 来取消自 BEGIN 命令以来发出的任何查询。例如，如果你在数据库命令行工作并错误地发出 DELETE FROM User 命令，只要你以 BEGIN 语句开始，你可以输入 ROLLBACK 并撤消删除操作。不言而喻，使用 BEGIN 命令是一个值得培养的（虽然有些麻烦的）习惯！

> **警告**
> 如果你正在使用事务，不要忘记在你（有意）做出更改后使用 COMMIT！这是一个容易在代码中遗漏的步骤，但如果你这样做，在调试时可能并不明显。

## 安全问题

连接到数据库后端的 CGI 程序（特别是 MySQL，它完全基于密码）有一个巨大的安全弱点：连接数据库的密码必须硬编码到脚本中或从另一个文件中读取。无论你怎么选择实现这一点，如果 Web 服务器作为 nobody 用户运行，它将会在 nobody 的所有权下执行 CGI 程序；包含密码的任何文件必须可由 nobody 用户读取。

如果你将密码放在只有 root 可读的文件中，CGI 程序将无法访问它。然而，如果你将其硬编码到 nobody 用户可读的文件中，系统上的任何人都可以编写自己的 CGI 程序来读取同一文件并将其打印出来供所有人查看——或者使用它来连接到你的数据库并发出一些 DROP DATABASE 命令。这是当前 Unix 世界中数据库安全固有的缺陷，没有优雅解决方案。

最简单的变通方法是禁止普通用户运行 CGI 脚本。你可能还可以想出使用 CGIwrap（在第 29 章“网络安全”中介绍）的创造性解决方案。但最终归结为一个问题：你想实施什么样的安全级别？*你信任你的本地用户吗？* 如果是这样，你可能可以勉强做到冒险生活。但如果你不信任系统中拥有账户的用户不会试图从你的脚本中获取数据库访问密码，你最好不应该在同一服务器上运行包含敏感或关键数据的数据库。

然而，如果你正在运行 PostgreSQL，你可以实施不依赖密码的安全性。我们之前讨论的配置，使用 ident 和 sameuser，仅允许用户访问他自己的数据库；它不允许用户访问任何其他数据库。这种类型的配置有助于防止本地用户闯入他们不属于的数据库——你也不必担心你的密码被恶意的 CGI 程序暴露。

