
`DBI->connect()` 方法还可以接受一个可选的第四参数参数，传递给数据源的参数哈希引用。数据库包定义了你可以在此哈希中设置哪些参数。

请注意，你可以同时打开多个连接。这些连接可以指向多个数据源，也可以指向同一个数据源。

`DBI->connect()` 返回一个哈希引用，通过它可以访问数据源。该哈希还包含关于数据源的元数据；在本节的后半部分，我们将描述如何使用这些连接级别的元数据。

# 准备语句

执行 DBI 程序的下一步是准备要执行的 SQL 语句。准备语句的方法会让驱动程序为 SQL 语句分配资源；数据源也会检查语句的正确性。

要准备语句，请使用通过数据库句柄访问的 `prepare()` 方法。该方法接受一个参数，即要准备的 SQL 语句；并返回一个值，即它所准备的语句句柄。语句句柄允许访问用于执行语句并检索返回数据的方法。如果语句未定义，则准备语句的操作失败。

在列表 14-16 中，我们如下使用该方法：

```perl
$cmd = "SELECT team_name "
  "FROM team "
  "ORDER BY team_name";

$sth = $dbh->prepare($cmd);
```

# 执行语句

语句准备好后，将执行该语句。当数据源执行语句时，它会返回语句请求的任何数据。数据源还会设置元数据，描述该语句如何影响数据源以及如何影响。

要执行语句，请使用通过数据库句柄访问的 `execute()` 方法。该方法接受一个参数，即要准备的 SQL 语句；并返回一个值，即它所准备的语句句柄。

```perl
)
else
  return;
}
else
{
  # $cmd 存储一个 SELECT 语句
  # 准备它，执行它，检索数据
  $sth = $dbh->prepare($cmd);
  if (!defined($sth))
  {
    $dbh->disconnect();
    print("Preparation of SELECT statement failed\n");
    exit 1;
  }
  $ret_val = $sth->execute();
  if (!defined($ret_val))
  {
    $dbh->disconnect();
    print("Execution of SELECT statement failed\n");
    exit 1;
  }
  while ($data = $sth->fetch_arrayref())
  {
    push(@rawResults, [$data]);
  }
  $dbh->disconnect();
  return @rawResults;
}
# *************************************
# 主
# *************************************
{
my $cmd;
my $i;
my $results;

sqlExec("CREATE TABLE mytmp (aval int)");

for ($i = 0; $i < 5; $i++)
{
  sqlExec("INSERT INTO mytmp values($i)");
}
```

## 列表 14-17（续）

```perl
$results = sqlExec("SELECT aval FROM mytmp ORDER BY aval");

for ($i = 1; $i < @$results; $i++) {
    my ($aval) = @($results[$i]);

    print $aval . "\n";
}


sqlExec("DROP TABLE mytmp");

exit 0;
```

在这个示例中，我们将查询数据库的代码隔离到了一个名为 `sqlExec()` 的子程序中。该子程序打开了与数据库的连接，正如我们在列表 14-16 中描述的那样。然而，在连接打开后，我们在要执行的指令中查找关键字 `select`；如果未找到，我们就使用 `do()` 方法来执行该指令：

```perl
if (lc(substr($cmd, 0, 6)) != "select") {
    # 如果为真，则不是一个 SELECT：使用 "do" 方法
    $ret_val = $dbh->do($cmd);

    $dbh->disconnect();

    if (!defined($ret_val)) {
        print("Execution of non-SELECT statement failed.\n");
        exit 1;
    } else {
        return;
    }
}
```

如果指令中包含关键字 `select`，那么我们就使用 `prepare()` 方法来准备指令，并使用 `execute()` 方法来执行指令：

```perl
else {
    # $cmd 存储一个 SELECT 语句；
# 准备它，执行它，检索数据
$sth = $dbh->prepare($cmd);

if (!defined($sth)) 
{
    $dbh->disconnect()$
    print("Preparation of SELECT statement failed\n");
    exit 1;
}

$ret_val = $sth->execute();
if (!defined($ret_val)) 
{
    $dbh->disconnect();
    print("Execution of SELECT statement failed\n");
    exit 1;
}
```

当指令准备好并执行后，我们使用 `fetch_row_array()` 方法来检索数据。该方法一次检索一行；数据以数组的形式返回（因此，这也是该方法的名称）。我们将每一行数据推入一个数组中，并返回持有这些数据的数组引用：

```perl
while ($data = $sth->fetch_arrayref()) 
{
    push @rawResults, [ @$data ];
}

$dbh->disconnect();
return \@rawResults;
```

为了演示我们的子程序 `sqlExec`，列表 14-17 的主部分执行了四条 SQL 指令。第一、第二和第四条指令不包含 `SELECT` 关键字，因此通过 `do()` 方法执行，而第三条指令包含 `SELECT` 关键字，因此使用 `prepare()` 和 `execute()` 方法执行：

```perl
sqlExec("CREATE TABLE mytmp (aval int)");

for ($i = 0; $i < 5; $i++) 
{
    sqlExec("INSERT INTO mytmp values ($i)");
}
```

```perl
$results = sqlExec("SELECT aval FROM mytmp ORDER BY aval");
for ($i = 1; $i < @$results; $i++)
(
  my ($aval) = @{ $results[$i] };
  print $aval . "\n";
)
```

```perl
sqlExec ("DROP TABLE mytmp");
exit 0;
```

当执行列表 14-17 时，会输出以下内容：

- 1
- 2
- 3
- 4

# NULL 数据

回想一下，ODBC 和 JDBC 在表示 NULL 方面存在问题，因为 C 或 Java 都没有方法可以表示一个根据定义就无法表示的值。Perl 通过初始化一个单独的变量来标记列是否持有 NULL 值来解决这个问题；JDBC 使用一个特殊方法 `isNull()` 来测试某列是否被设置为 NULL。

相比之下，Perl 语言内置了一个表示“非值”的值——`undefined`（未定义）。如果一列是 NULL，Perl DBI 会被设置为未定义。因此，通过测试变量是否已定义，我们可以确定它是否持有 NULL。

列表 14-18 演示了如何使用 Perl DBI 处理 NULL：它重新创建了列表 14-7 和列表 14-13 中的 Perl DBI 程序。我们在这里只显示了该示例特有的代码。

## 列表 14-18：处理 NULL

```perl
for ($i = 0; $i < @$results; $i++) {
  my ($aval) = @{ $results[$i] };
  if (defined($aval)) {
    print $aval . "\n";
  } else {
    print "NULL\n";
  }
}
```

*(注：由于原文文本中列表 14-18 的代码块不完整，此处根据上下文逻辑进行了补全翻译处理，以保持文档结构完整)*
