

`fetchrow_array()` 返回一个包含当前行各列值的数组，如果没有更多行，则返回一个空数组。因此，该循环获取由 `SELECT` 语句返回的连续行，并打印每一行，各列值之间用制表符分隔。

数据库中的 `NULL` 值在 Perl 脚本中返回为 `undef` 值，但这些值打印为空字符串，而不是单词 “`NULL`。” 当你运行脚本时，`undef` 列值还有另一个影响；它们会导致 Perl 解释器发出如下警告：

```
Use of uninitialized value in join at dump_members.pl line `n`.
```

这些警告是由包含 `use warnings` 语句触发的。如果移除该语句并重新运行脚本，这些警告将消失。然而，警告模式对于发现问题（例如打印未初始化的变量）非常有用，因此消除警告的更好方法是检测和处理 `undef` 值。8.2.5 节“处理返回结果集的语句”讨论了一些相关技术。

在 `print` 语句中，请注意，制表符和换行符（分别表示为 `\t` 和 `\n` 序列）是用双引号括起来的。在 Perl 中，转义序列仅在双引号内部被解释，而在单引号内部则不会。如果使用单引号，输出将充满字面上的 `\t` 和 `\n`。

在获取行的循环结束后，对 `finish()` 的调用表明语句句柄不再需要，分配给它的任何临时资源都可以被释放。在此脚本中，对 `finish()` 的调用仅用于说明目的。实际上，这里不需要调用它，因为获取行的调用在遇到结果集末尾时会自动执行此操作。`finish()` 在只获取结果集的一部分而未到达其末尾的情况下更为有用（例如，如果你只获取第一行）。从此处开始的示例除非必要，否则不使用 `finish()`。

打印完会员列表后，我们的工作就完成了，因此可以在退出之前从服务器断开连接：

```
$dbh->disconnect();
```

`dump_members.pl` 展示了大多数 DBI 程序中都涉及的一些常见概念，在此处你很可能已经可以开始编写自己的 DBI 程序，而无需知道更多细节。例如，要输出其他表的内容，你只需更改传递给 `prepare()` 方法的 `SELECT` 语句的文本即可。事实上，如果你想了解这种技术的应用，你可以直接跳到 8.3 节“将 DBI 付诸实践”中讨论如何为历史联赛年度会议手册和联赛印刷目录生成会员列表的部分。然而，DBI 提供了许多其他有用的功能。接下来的章节将更详细地介绍其中的一些，以便你可以看到如何在 Perl 脚本中执行比运行简单 `SELECT` 语句更多的操作。

## 8.2.3 处理错误

dump_members.pl 在调用 connect() 方法时启用了 RaiseError 错误处理属性，以便在发生错误时自动终止脚本并显示错误消息，而不仅仅是返回错误代码。也可以通过其他方式处理错误。例如，你可以自己检查错误，而不是让 DBI 来处理。为了查看如何控制 DBI 的错误处理行为，让我们仔细看看传递给 connect() 作为最后参数的连接属性哈希：

```
# 数据源名称、用户名、密码、连接属性
my $dsn = "DBI:mysql:sampdb:localhost";
my $user_name = "sampur";
my $password = "secret";
my $conn_attrs = {RaiseError => 1, PrintError => 0, AutoCommit => 1};

# 连接到数据库
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);
```

与错误处理相关的两个属性是 RaiseError 和 PrintError：

- 如果启用 RaiseError（设置为非零值），当 DBI 方法中出现错误时，DBI 会引发异常。默认情况下，这会导致调用 die() 来打印消息并退出脚本。
- 如果启用 PrintError，当发生 DBI 错误时，DBI 会调用 warn() 来打印消息，但脚本会继续执行。

默认情况下，RaiseError 被禁用，而 PrintError 被启用。在这种情况下，如果 connect() 调用失败，DBI 会打印消息但继续执行。因此，如果你省略了 connect() 的第四个参数，从而获得默认的错误处理行为，你可能像这样检查错误：

```
my $dbh = DBI->connect ($dsn, $user_name, $password) or exit (1);
```

在这种情况下，如果发生错误，connect() 返回 undef 以表示失败，这将触发 exit() 的调用。你不需要打印错误消息，因为 DBI 已经打印了一个。

如果你显式指定错误检查属性的默认值，传递给 connect() 的设置将如下所示：

```
my $conn_attrs = {RaiseError => 0, PrintError => 1, AutoCommit => 1};
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs)
    or exit (1);
```

这样写的工作量稍大，但对于普通读者来说，错误处理的行为也更加明显。

要自己检查错误并打印自己的消息，请禁用 `RaiseError` 和 `PrintError` 两者：

```
my %conn_attrs = {RaiseError => 0, PrintError => 0, AutoCommit => 1};
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);
or die "Could not connect to server: $DBI::err ($DBI::errstr)\n";
```

在刚才显示的代码中使用的 `$DBI::err` 和 `$DBI::errstr` 变量对于构建错误消息非常有用。它们包含 MySQL 错误代码和错误字符串，类似于 C API 函数 `mysql_errno()` 和 `mysql_error()`。如果没有发生错误，`$DBI::err` 将为 0 或 undef，`$DBI::errstr` 将为空字符串或 undef。（换句话说，两个变量都将为假。）

如果你希望 DBI 为你处理错误，这样你就不必自己检查它们，请启用 `RaiseError` 并禁用 `PrintError`：

```
my %conn_attrs = {RaiseError => 1, PrintError => 0, AutoCommit => 1};
my $dbh = DBI->connect ($dsn, $user_name, $password, \%conn_attrs);
```

这是最简单的方法，本章中展示的大多数脚本都是这样编写的。在启用 `RaiseError` 时禁用 `PrintError` 的原因是防止错误消息被打印两次的可能性。（如果两个属性都启用，在某些情况下两个 DBI 处理程序都可能被调用。）

如果你希望在脚本退出时执行自己的某种清理代码，启用 `RaiseError` 可能并不合适，尽管在这种情况下，你可能能够通过重新定义 `SIG(__DIE__)` 信号处理程序来实现你的目的。避免启用 `RaiseError` 属性的另一个原因是 DBI 在其消息中打印技术性信息，例如：

```
disconnect (DBI::db:HASH(0x197aae4)) invalidates 1 active statement. Either destroy statement handles or call finish on them before disconnecting.
```

这对程序员来说是有用的信息，但它可能是你不想向日常用户展示的那类信息。在这种情况下，自己检查错误可能更好，这样你可以显示对预计使用脚本的人更有意义的消息。或者你也可以考虑在此重新定义 `SIG(__DIE__)` 处理程序。这可能很有用，因为你可以启用 `RaiseError` 以简化错误处理，但用你自己的消息替换 DBI 呈现的默认错误消息。为了提供自己的 `__DIE__` 处理程序，在执行任何 DBI 调用之前，请执行类似以下操作：

```
$SIG(__DIE__) = sub { die "Sorry, an error occurred\n"; };
```

你还可以以常规方式定义子例程，并使用子例程引用来设置信号处理程序值：

```
sub die_handler
{
    die "Sorry, an error occurred\n";
}
```

