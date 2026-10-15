
```
INSERT INTO cd_collection VALUES(9, 'Nevermind', 'Nirvana', 1991, NULL);
```

如果您不想包含评分，MySQL 需要为最后一列（`rating`）使用 `NULL` 值。另一方面，PostgreSQL 允许您只需省略最后一个

`column`。当然，如果中间有列是空值，则需要在 `INSERT` 语句中显式声明 `NULL`。

通常，`INSERT` 语句被编码到前端程序中，这样用户在向数据库添加数据时就无需担心涉及的 SQL 语句。

## 从数据库检索数据

当然，将数据存储在数据库中的主要原因是为了以后可以查找、排序并生成该数据的报告。基本的数据检索是通过 `SELECT` 语句完成的，其语法如下：

```
SELECT column1, column2, column3 FROM table_name WHERE search_criteria;
```

语句的前两部分——`SELECT` 和 `FROM` 部分——是必需的。语句的 `WHERE` 部分是可选的。如果省略它，则返回表 `table_name` 中的所有行。

`column1`、`column2`、`column3` 表示你想要查看的列的名称。如果想查看所有列，也可以使用通配符 `*` 来显示符合搜索条件的所有列。例如，以下语句显示 `cd_collection` 表中的所有列：

```
SELECT * FROM cd_collection;
```

如果你只想查看表中所有 CD 的标题，则可以使用如下语句：

```
SELECT title FROM cd_collection;
```

要选择 CD 的标题和年份，可以使用以下语句：

```
SELECT title, year FROM cd_collection;
```

如果你想要更精细一些，可以使用 SQL 将 CD 标题后跟年份用括号括起来，就像惯例那样。MySQL 和 PostgreSQL 都提供了字符串连接函数来处理此类问题。然而，这两个系统的语法是不同的。

在 MySQL 中，你可以使用 `CONCAT()` 函数将 `title` 和 `year` 列合并为一个输出列，并加上括号。以下语句是一个示例：

```
SELECT CONCAT(title, " (",year,")") AS TitleYear FROM cd_collection;
```

该语句将标题和年份列在同一列下，该列的标签为 `TitleYear`。注意 `CONCAT()` 函数中除了字段外还有两个字符串——这些用于添加空白和括号。

在 PostgreSQL 中，字符串连接函数就是双竖线 (`||`)。以下命令是前述 MySQL 命令的 PostgreSQL 等价命令：

```
SELECT (genus||' '||'('||species||')') AS TitleYear FROM cd_collection;
```

注意括号是可选的，但它们使语句更易读。同样，中间和末尾的字符串（注意引号之间的空格）用于在标题和年份之间插入空格和括号。

当然，更多时候，你并不想要数据库中每一行的列表。相反，你只想找到符合某些特征的行。为此，你在 `SELECT` 语句中添加 `WHERE` 语句。例如，假设你想查找 `cd_collection` 表中评分为 5 的所有 CD。你可以使用如下语句：

```
SELECT * FROM cd_collection WHERE rating = 5;
```

使用图 21.2 中的表，你可以看到此查询将返回 Trouser Jazz、Life for Rent 和 The Two Towers 的行。这是一个简单的查询，SQL 能够处理比这复杂得多的查询。复杂查询可以使用逻辑 `AND` 和逻辑 `OR` 语句编写。例如，假设你想细化查询，只列出那些未在 2003 年发行的 CD。你可以使用如下查询：

```
SELECT * FROM cd_collection WHERE rating = 5 AND year != 2003;
```

在 SQL 中，`!=` 表示“不等于”。因此再次查看图 21.2 中的表，你可以看到此查询返回 Trouser Jazz 和 The Two Towers 的行，但不会返回 Life for Rent 的行，因为它是在 2003 年发行的。

那么，如果你想列出所有评分为 3 或 4 的 CD，但排除 2000 年发行的呢？这时，你需要组合逻辑 `AND` 和逻辑 `OR` 语句：

```
SELECT * FROM cd_collection WHERE rating = 3 OR rating = 4 AND year != 2000;
```

此查询将返回 Mind Bomb、Natural Elements 和 Combat Rock 的条目。然而，它不会返回 Adiemus 4 的条目，因为它是在 2000 年发行的。

### TIP

新数据库程序员最常见的错误之一是混淆逻辑 `AND` 和逻辑 `OR`。例如，在日常用语中，你可能会说“帮我找所有在 2003 年和 2004 年发行的 CD。”乍一看，你可能会认为如果你以 SQL 格式将此语句输入数据库，它将返回 For All You’ve Done 和 Life for Rent 的行。事实上，它将完全不返回任何行。这是因为数据库将该语句解释为“查找 CD 同时在 2003 年发行且在 2004 年发行的所有行。”当然，同一张 CD 不可能发行两次，因此无论表中存储了多少张 CD，此语句永远不会返回任何行。形成此语句的正确方法是使用 `OR` 语句而不是 `AND` 语句。

SQL 的能力远不止于此所展示的。但正如前面提到的，本节并非旨在教你 SQL 编程的全部知识；相反，它教你基础知识，以便你能成为更有效的 DBA。

## 选择数据库：MySQL 与 PostgreSQL

如果你刚开始学习在 Linux 上使用数据库，那么第一步就是研究哪种数据库最能满足你的需求。有许多数据库软件包可用于 Linux；有些是免费的，而另一些则花费数十万美元。昂贵的商业数据库，如 Oracle，已超出本书的范围。相反，本章重点介绍两种可免费获得的数据库：MySQL 和 PostgreSQL。

这两种数据库都相当强大，其中任何一种可能都能满足你的需求。然而，每个数据库都有其独特的功能和能力，可能会更好地满足你的需求，或使开发数据库应用程序变得更容易。

### 速度

直到最近，速度选择很简单：如果查询执行的速度对你的应用程序至关重要，你就使用 MySQL。MySQL 以其极快的数据库而闻名。直到最近，与之相比，PostgreSQL 速度相当慢。

PostgreSQL 的新版本在速度方面有所改进（在磁盘访问、排序等方面）。在某些情况下，例如在大量同时访问期间，PostgreSQL 可以比 MySQL 快得多，正如你在下一节中将看到的那样。然而，与许多其他数据库相比，MySQL 仍然极快。

### 数据锁定

为了防止数据损坏，数据库需要在数据被访问时对其进行锁定。只要锁存在，就没有任何其他进程可以在第一个进程释放锁之前访问数据。这意味着任何尝试访问数据的其他进程都必须等待当前进程完成。下一个排队的进程然后锁定数据直到完成，其余进程必须等待轮到自己，依此类推。

当然，数据库上的操作通常会很快完成，因此在同时访问数据库的用户数量较少的环境中，锁的持续时间通常很短，不会造成明显的延迟。然而，在许多人同时访问数据库的环境中，锁定可能会导致性能问题，因为人们必须等待轮到自己访问数据库。

旧版本的 MySQL 在表级锁定数据，这在访问量大的期间可被视为更新的瓶颈。这意味着当有人在表中写入一行数据时，整个表都会被锁定，因此没有人可以输入数据。如果你的表中有 500,000 行（或记录），只要访问 1 行，所有 500,000 行都会被锁定。再一次，在同时用户相对较少的环境中，这不会导致严重的性能问题，因为大多数操作完成得如此之快，以至于锁定的时间极短。然而，在许多人同时访问数据的情况下，MySQL 的表级锁定可能是一个重大的性能瓶颈。

另一方面，PostgreSQL 在行级锁定数据。在 PostgreSQL 中，只有当前被访问的行被锁定。表的其余部分可以被其他用户访问。这种行级锁定显著降低了在同时用户数量众多的环境中锁定对性能的影响。因此，作为一般规则，PostgreSQL 比 MySQL 更适合高负载环境。

随 Ubuntu 捆绑的 MySQL 版本让你可以选择使用表级或行级锁定的表。在 MySQL 术语中，`MyISAM` 表使用表级锁定，而 `InnoDB` 表使用行级锁定。

### NOTE

MySQL 的数据锁定方法在 http://www.mysql.com/doc/en/internal_locking.html 有更深入的讨论。

你可以在 http://www.postgresql.org/idocs/index.php?locking-tables.html 找到有关 PostgreSQL 锁定的更多信息。

### ACID 合规性在事务处理中以保护数据完整性

MySQL 和 PostgreSQL 不同的另一个方面是它们为防止数据损坏提供保护的程度。缩写 `ACID` 通常用于描述数据保护的几个方面：
