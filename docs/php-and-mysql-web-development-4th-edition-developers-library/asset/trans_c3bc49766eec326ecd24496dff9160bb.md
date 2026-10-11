
一种称为“参数绑定”的技术（参见第 8.2.7 节，“占位符和预处理语句”）。

如果你将单个值获取到一个变量中，请小心书写赋值方式。如果你像这样编写循环的开头，它将正确工作：

```perl
while (my $val = $sth->fetchrow_array ()) {
    ...
}
```

该值是在列表上下文中获取的，因此只有当没有更多行时，测试才会失败。但如果你像这样编写测试，它将以神秘的方式失败：

```perl
while (my $val = $sth->fetchrow_array ()) {
    ...
}
```

这里的区别在于，该值是在标量上下文中获取的，因此如果 $val 恰好为零、undef 或空字符串，测试将评估为假并终止循环，即使你尚未到达结果集的末尾。

第二种行获取方法 `fetchrow_arrayref()` 类似于 `fetchrow_array()`，但它返回的不是包含当前行列值的数组，而是指向数组的引用，当没有更多行时返回 `undef`。像这样使用它：

```perl
while (my $ary_ref = $sth->fetchrow_arrayref ()) {
    my $delim = "";
    for (my $i = 0; $i < @$ary_ref; $i++)
    {
        $ary_ref->[$i] = "" if !defined ($ary_ref->[$i]); # NULL value?
        print $delim, $ary_ref->[$i];
        $delim = ",";
    }
    print "\n";
}
```

你通过数组引用 $ary_ref 访问数组元素。这有点像解引用指针，因此你使用 $ary_ref->[$i] 而不是 $ary[$i]。要将引用转换为数组，使用 `@$ary_ref` 构造。

`fetchrow_arrayref()` 不适合将变量获取到列表中。例如，以下循环不起作用：

```perl
while (my ($var1, $var2, $var3, $var4) = @{$sth->fetchrow_arrayref ()})
{
    # do something with variables
}
```

只要 `fetchrow_arrayref()` 实际获取了一行，循环就能正常工作。但当没有更多行时，`fetchrow_arrayref()` 返回 `undef`，而 `@(undef)` 是非法的。（这就像在 C 程序中试图解引用一个 `NULL` 指针。）

第三种行获取方法 `fetchrow_hashref()` 像这样使用：

```perl
while (my $hash_ref = $sth->fetchrow_hashref ()) {
    my $delim = ",";
    foreach my $key (keys %{$hash_ref})
    {
        $hash_ref->{$key} = "" if !defined ($hash_ref->{$key}); # NULL value?
        print $delim, $hash_ref->{$key};
        $delim = ",";
    }
    print "\n";
}
```

每次调用 `fetchrow_hashref()` 都会返回一个指向以列名为键的行值哈希的引用，当没有更多行时返回 `undef`。在这种情况下，列值不会以任何特定顺序输出，因为 Perl 哈希的成员是无序的。然而，DBI 使用列名作为哈希元素的键，因此 `$hash_ref` 给你一个单一变量，通过它可以按名称访问任何列值。这意味着你可以以任意顺序提取值（或其中任何子集），你不需要知道列在 `SELECT` 语句中被检索的顺序。例如，要访问 `name` 和 `email` 列，你可以这样做：

```perl
while (my $hash_ref = $sth->fetchrow_hashref ())
{
    my $delim = "";
    foreach my $key ("last_name", "first_name", "suffix", "email")
    {
        $hash_ref->{$key} = "" if !defined ($hash_ref->{$key}); # NULL value?
        print $delim, $hash_ref->{$key};
        $delim = ",";
    }
    print "\n";
}
```

当你想要将一行值传递给函数，而不要求该函数知道列在 `SELECT` 语句中的命名顺序时，`fetchrow_hashref()` 特别有用。在这种情况下，你会调用 `fetchrow_hashref()` 来获取行，并编写一个函数，使用列名从行哈希中访问值。使用 `fetchrow_hashref()` 时，请记住以下注意事项：

- 如果你需要每一比特的性能，`fetchrow_hashref()` 不是最佳选择。它比 `fetchrow_array()` 或 `fetchrow_arrayref()` 效率低。

- 默认情况下，列名用作键值，其大小写与 `SELECT` 语句中编写的列名相同。在 MySQL 中，列名不区分大小写，因此无论使用什么大小写编写列名，语句都会以相同的方式工作。但 Perl 哈希键名区分大小写，这可能会给你带来麻烦。为了避免潜在的大小写不匹配问题，你可以通过传递 `NAME_lc` 或 `NAME_uc` 属性来告诉 `fetchrow_hashref()` 将列名强制为特定大小写：

```perl
$hash_ref = $sth->fetchrow_hashref ('NAME_lc'); # use lowercase names
$hash_ref = $sth->fetchrow_hashref ('NAME_uc'); # use uppercase names
```

- 哈希中包含每个唯一列名的一个元素。如果你执行一个连接，该连接从具有重叠名称的多个表中返回列，你将无法访问所有列值。如果你发出以下语句，`fetchrow_hashref()` 将返回一个仅包含一个元素 `name` 的哈希：

```sql
SELECT a.name, b.name FROM a INNER JOIN b WHERE a.name = b.name
```

为了避免这个问题，使用别名确保每个列都有一个不同的名称。例如，如果你将语句重写如下，`fetchrow_hashref()` 将返回一个指向包含两个元素 `name` 和 `name2` 的哈希的引用：

```sql
SELECT a.name, b.name AS name2 FROM a INNER JOIN b WHERE a.name = b.name
```

### 8.2.5.2 确定语句返回的行数

如何知道 SELECT 或类似 SELECT 语句返回的行数？一种方法是在获取行时进行计数。实际上，这是 DBI 中知道 SELECT 语句返回了多少行的*唯一*可移植方法。如果你使用 MySQL 驱动程序，可以在调用 `execute()` 后使用语句句柄调用 `rows()` 方法。但这不能移植到其他数据库系统，并且 DBI 文档明确不鼓励对 SELECT 语句使用 `rows()`。即使是对于 MySQL，如果你设置了 `mysql_use_result` 属性，`rows()` 也不会返回正确的结果，直到你获取了所有行。因此，你最好只是在获取行时计数。（有关 `mysql_use_result` 的更多信息，请参阅附录 H（在线）。）

### 8.2.5.3 获取单行结果

如果结果集只包含一行，就不需要运行循环来获取结果。假设你想编写一个脚本 `count_members.pl`，告诉你当前历史联盟成员的数量。执行该语句的代码如下所示：

```perl
# issue query
my $sth = $dbh->prepare ('SELECT COUNT(*) FROM member');
$sth->execute ();

# read and display query result
my $count = $sth->fetchrow_array ();
$sth->finish ();
$count = "can't tell" if !defined ($count);
print "$count\n";
```

SELECT 语句只返回一行，因此不需要循环；我们只调用一次 `fetchrow_array()`。此外，因为我们只选择一个列，甚至不需要将返回值赋给数组。当在标量上下文中（期望单个值而不是列表）调用 `fetchrow_array()` 时，它返回该行的一列，如果没有可用行则返回 `undef`。DBI 没有定义在标量上下文中 `fetchrow_array()` 返回行的哪个元素，但对于刚才显示的语句来说这是没问题的。它只检索单个值，因此关于返回什么值没有歧义。

这段代码调用 `finish()` 来释放结果集，即使该集只包含一行。（`fetchrow_array()` 在注意到你已到达集末尾时会隐式释放结果集，但在这里只有你第二次调用它时才会发生。）

另一种你期望最多只有一行结果的查询类型是那些包含 `LIMIT 1` 以限制返回行数的查询。这种用法的一个常见用途是返回包含特定列最大值或最小值的行。例如，以下查询查找出生最近的总统的姓名和出生日期：

```perl
my $stmt = "SELECT last_name, first_name, birth FROM president"
         . " WHERE birth = (SELECT MAX(birth) FROM president)";
my $sth = $dbh->prepare ($stmt);
$sth->execute ();

my ($last_name, $first_name, $birth) = $sth->fetchrow_array ();
$sth->finish ();
if (!defined ($last_name))
{
    print "Query returned no result\n";
}
else
{
    print "Most recently born president: $first_name $last_name ($birth)\n";
}
```

不需要获取循环的另一类语句是使用 `MAX()` 或 `MIN()` 选择单行的语句。但在所有这些情况下，获取单行结果更容易的方法是数据库句柄方法 `selectrow_array()`，它将 `prepare()`、`execute()` 和行获取合并为单个调用。它返回一个数组（不是引用），或者如果查询未返回行或发生错误则返回空数组。前面的例子可以使用 `selectrow_array()` 重写如下：

```perl
my $stmt = "SELECT last_name, first_name, birth FROM president"
         . " WHERE birth = (SELECT MAX(birth) FROM president)";
my ($last_name, $first_name, $birth) = $dbh->selectrow_array ($stmt);
if (!defined ($last_name))
{
```

