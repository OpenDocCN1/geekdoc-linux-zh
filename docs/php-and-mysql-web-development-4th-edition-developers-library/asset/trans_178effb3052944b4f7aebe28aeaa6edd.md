
## 8.2 Perl DBI 概览

历史联盟（Historical League）的会员列表采用制表符分隔（tab-delimited）格式。该格式本身并不特别有趣。在此阶段，比生成美观的输出更重要的是了解如何使用 DBI。`dump_members.pl` 脚本看起来是这样的：

```perl
#!/usr/bin/perl
# dump_members.pl - dump Historical League's membership list

use strict;
use warnings;
use DBI;

# data source name, username, password, connection attributes
my $dsn = "DBI:mysql:sampdb:localhost";
my $user_name = "sampdm";
my $password = "secret";
my %conn_attrs = (RaiseError => 1, PrintError => 0, AutoCommit => 1);

# connect to database
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);

# issue query
my $sth = $dbh->prepare ("SELECT last_name, first_name, suffix, email,"
. " street, city, state, zip, phone FROM member ORDER BY last_name");
$sth->execute ();

# read and display query result
while (my @ary = $sth->fetchrow_array ())
{
print join ("\t", @ary), "\n";
}
$sth->finish ();

$dbh->disconnect ();
```

若要自行尝试该脚本，可以使用 `sampdb` 发行版中包含的副本，或者使用文本编辑器创建它。如果您使用字处理器，请务必将脚本保存为纯文本。不要将其保存为字处理器的原生格式。您很可能需要更改至少部分连接参数，例如主机名、数据库名称、用户名或密码。（这对于本章中其他同样使用连接参数的脚本也适用。）稍后，在第 8.2.9 节“指定连接参数”中，我们将了解如何从选项文件获取参数，而不是直接在脚本中设置它们。

现在让我们逐段分析该脚本。第一行包含标准的 Perl 查找位置指示符：

```perl
#!/usr/bin/perl
```

这一行是本章讨论的所有脚本的一部分；我不再进一步提及它。

在脚本中包含对其目的至少最简明的描述是个好习惯，因此下一行是一个注释，旨在为查看该脚本的人提供关于其功能的线索：

```perl
# dump_members.pl - dump Historical League’s membership list
```

从 `#` 字符到行尾的文本被视为注释。在脚本中散布注释以解释其工作原理是一种有用的做法。

接下来我们有几条 use 语句：

```perl
use strict;
use warnings;
use DBI;
```

`use strict` 告知 Perl 要求你在使用前声明变量。你可以编写不包含 `use strict` 行的脚本，但它对于捕获错误非常有用，所以我建议始终包含它。例如，如果你声明了一个变量 `$my_var`，但后来错误地将其引用为 `$mw_var`，当你在严格模式下运行脚本时，将显示以下消息：

```
Global symbol "$mw_var" requires explicit package name at line n
```

当你看到那个时，你会想：“什么？我从未使用过名为 `$mw_var` 的变量！”然后你查看脚本的第 n 行，发现你把 `$my_var` 拼写错误成了 `$mw_var`，并修复它。没有严格模式，Perl 不会因 `$mw_var` 而抱怨；它只是创建一个具有 `undef`（未定义）值的新变量并使用它，且不加抱怨。于是你只能纳闷为什么你的脚本不起作用。

`use warnings` 告知 Perl，如果它发现你使用了可疑的语言结构或执行诸如打印未初始化变量等操作，则发出警告。这很有用，因为它可以提醒你哪些代码应该重写。

`use DBI` 告知 Perl 解释器需要引入 DBI 模块。没有这一行，一旦你尝试在脚本中执行任何与 DBI 相关的操作，就会发生错误。无需指示要使用哪个 DBD 级驱动模块；当你连接到数据库时，DBI 会为你激活正确的那个。

由于我们运行在严格模式下，我们必须通过 `my` 关键字来声明脚本使用的变量。可以把它看作脚本在说“我正在明确表明这些是我的变量”。脚本的下一部分设置了指定连接参数的变量，然后使用它们连接到数据库：

```perl
# data source name, username, password, connection attributes
my $dsn = "DBI:mysql:sampdb:localhost";
my $user_name = "sampadm";
my $password = "secret";
my %conn_attrs = (RaiseError => 1, PrintError => 0, AutoCommit => 1);

# connect to database
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);
```

`connect()` 调用是作为 `DBI->connect()` 调用的，因为它是 DBI 类的一个方法。你不需要真正知道那意味着什么；这只是让头疼的一点点面向对象术语。（如果你确实想知道，它的意思是 `connect()` 是一个“属于” `DBI` 的函数。）`connect()` 接受几个参数：

- 数据源，也称为“数据源名称”，或“DSN”。DSN 指示使用哪个 DBD 模块，可能还有其他参数。
- 你的 MySQL 账户的用户名和密码。
- 一个可选参数，指示额外的连接属性。如果给出，此参数应作为指向指定连接属性名称和值的哈希引用的参数传递。

数据源格式由你想要使用的特定 DBD 模块的要求决定。对于 MySQL 驱动程序，允许的 DSN 格式包括以下任一种：

`DBI:mysql:db_name`
`DBI:mysql:db_name:hostname`

`dbi` 的大小写无关紧要，但 `mysql` 必须是小写。`db_name` 代表你想使用的数据库的名称，`host_name` 指示服务器运行的主机。如果省略主机名，默认值为 `localhost`（第 8.2.9 节“指定连接参数”讨论其他允许的数据源格式。）

我们作为 `connect_attrs` 的值指定的连接属性哈希启用了 `RaiseError` 属性并禁用了 `PrintError`。这些设置导致 DBI 检查与数据库相关的错误，如果在检测到错误时以错误消息退出。（这就是为什么你在 `dump_members.pl` 脚本的任何地方都没有看到错误检查代码的原因；DBI 处理了一切。）第 8.2.3 节“处理错误”涵盖了处理错误的方法。

属性哈希还启用了 `AutoCommit` 属性。目前，这并非严格必要，但它确实明确表明脚本为事务处理启用了自动提交模式。脚本不包含任何显式事务，但存在 DBI 在未来要求脚本显式指定 `AutoCommit` 属性的可能性。现在在脚本中这样做可以确保如果发生此类更改，它们已准备就绪。

要指定连接属性，你可以选择在 `connect()` 调用中直接提供哈希引用：

```perl
my $dbh = DBI->connect( $dsn, $user_name, $password,
 { RaiseError => 1, PrintError => 0, AutoCommit => 1 } );
```

不同的人觉得一种风格或另一种风格更容易阅读或编辑，但在操作上两种方法是相同的。

如果 `connect()` 调用成功，它返回一个数据库句柄，我们将其分配给 `$dbh`。默认情况下，`connect()` 在失败时返回 `undef`。然而，由于脚本启用了 `RaiseError`，如果 `connect()` 调用中出现问题，DBI 将在显示错误消息后退出。（这对于其他 DBI 方法也是如此。我将描述它们返回什么以指示错误，但如果启用了 RaiseError，它们根本不会返回。）

连接到数据库后，`dump_members.pl` 发出 SELECT 语句以检索会员列表，然后执行循环以处理返回的每一行。这些行构成了结果集。要执行 SELECT，首先准备语句，然后执行它：

```perl
# issue query
my $sth = $dbh->prepare ("SELECT last_name, first_name, suffix, email,"
. " street, city, state, zip, phone FROM member ORDER BY last_name");
$sth->execute ();
```

`prepare()` 使用数据库句柄调用；它将 SQL 语句传递给驱动程序，以便在执行前进行预处理。一些驱动程序在此时确实会对语句做些什么。其他驱动程序只是记住它，直到你调用 `execute()` 以执行语句为止。`prepare()` 的返回值是一个语句句柄，这里分配给 `$sth`。语句句柄用于与语句相关的所有进一步处理。

请注意，语句字符串本身没有结尾分号。你无疑有习惯用 ';' 字符结束 SQL 语句（通过长时间与 `mysql` 程序交互培养的习惯）。然而，使用 DBI 时最好改掉这个习惯，因为分号通常会导致语句因语法错误而失败。同样的情况适用于在语句字符串中添加 `\n` 或 `\G`——不要这样做。这些语句终止符是 `mysql` 的约定，在 DBI 脚本中发出语句时不使用。语句字符串的结尾隐式地终止了语句，不需要显式的终止符。

当你调用方法而不传递任何参数时，你可以省略括号。这两个调用是等效的：

```perl
$sth->execute ();
$sth->execute;
```

我更喜欢包含括号，因为它们让调用在我看来不那么像变量引用。你的偏好可能不同。

调用 `execute()` 后，会员列表的行可供处理。在 `dump_members.pl` 脚本中，行获取循环简单地将每行的内容打印为制表符分隔的值集合：

```perl
# read and display query result
while (my @ary = $sth->fetchrow_array ())
{
print join ("\t", @ary), "\n";
}
$sth->finish ();
```

