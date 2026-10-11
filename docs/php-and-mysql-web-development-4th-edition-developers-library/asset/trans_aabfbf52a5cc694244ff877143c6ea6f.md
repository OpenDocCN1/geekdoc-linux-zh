

### 8.2.5.4 处理完整结果集

```perl
    print "Query returned no result\n";
}
else
{
    print "Most recently born president: $first_name $last_name ($birth)\n";
}
```

当你使用获取循环时，DBI 无法以任何顺序处理行，除了循环返回它们的顺序。此外，获取一行后，除非采取措施在内存中保持它，否则前一行的数据将丢失。这些行为并不总是理想的。例如，如果你需要对行进行多次遍历以执行统计计算，它们就不太合适。（也许你想先遍历结果集一次以评估数据的一些一般数值特征，然后再遍历行以执行更具体的分析。）

有几种不同的方法可以将结果集作为一个整体来访问。你可以执行常规的获取循环并在获取时保存每一行，或者你可以使用一种方法一次性返回整个结果集。无论哪种方式，你最终都会得到一个矩阵，其中包含结果集中的每一行，以及你选择的列数。然后，你可以按任意顺序、任意次数处理矩阵中的元素。以下讨论描述了这两种方法。

使用获取循环捕获结果集的一种方法是使用 `fetchrow_array()` 并保存指向行的引用数组。以下代码执行了与 `dump_members.pl` 中获取并打印循环相同的工作，只是它保存了所有行，然后打印矩阵。它说明了如何确定矩阵的行数和列数，以及如何访问矩阵的单个元素：

```perl
my @matrix = (); # 数组引用的数组

while (my @ary = $sth->fetchrow_array ()) # 获取每一行
{
    push (@matrix, [ @ary ]); # 保存刚刚获取的行引用
}

# 确定矩阵的维度
my $rows = scalar (@matrix);
my $cols = ($rows == 0 ? 0 : scalar (@{$matrix[0]}));

for (my $i = 0; $i < $rows; $i++) # 打印每一行
{
    my $delim = "";
    for (my $j = 0; $j < $cols; $j++)
    {
        $matrix[$i][$j] = "" if !defined ($matrix[$i][$j]); # NULL 值？
        print $delim, $matrix[$i][$j];
        $delim = ",";
    }
    print "\n";
}
```

在检查矩阵维度时，必须先确定行数，因为列数的计算取决于矩阵是否为空。如果 $rows 为 0，矩阵为空，$cols 也将变为 0。否则，可以使用语法 @$matrix[0] 将整行作为整体访问，并以第一行的元素数量计算列数。

前面的示例将每一行作为数组获取，然后保存其引用。你可能认为调用 `fetchrow_arrayref()` 直接获取行引用会更高效：

```perl
my @matrix = (); # 数组引用的数组

while (my $ary_ref = $sth->fetchrow_arrayref ())
{
    push (@matrix, $ary_ref); # 保存刚刚获取的行引用
}
```

这是行不通的，因为 `fetchrow_arrayref()` 会重用它所指向的数组。结果矩阵是一个引用数组，每个引用都指向同一行——即最后获取的那一行。因此，如果你想通过逐行获取来构建矩阵，请使用 `fetchrow_array()` 而不是 `fetchrow_arrayref()`。

作为使用获取循环的替代方案，可以调用返回整个结果集的 DBI 方法之一。例如，`fetchall_arrayref()` 返回一个指向引用数组的引用，每个引用都指向结果集中一行的内容。（这是一个长难句；意思是返回值是一个指向矩阵的引用。）要使用 `fetchall_arrayref()`，请调用 `prepare()` 和 `execute()`，然后像这样获取结果：

```perl
# 将所有行获取为引用数组的引用
my $matrix_ref = $sth->fetchall_arrayref ();
```

你可以按照以下方式确定数组的维度并访问其元素：

```perl
# 确定矩阵的维度
my $rows = !(defined ($matrix_ref) ? 0 : scalar (@{$matrix_ref}));
my $cols = ($rows == 0 ? 0 : scalar @{$matrix_ref->[0]});

for (my $i = 0; $i < $rows; $i++)    # 打印每一行
{
    my $delim = "";
    for (my $j = 0; $j < $cols; $j++)
    {
        $matrix_ref->[$i][$j] = "" if !defined ($matrix_ref->[$i][$j]); # NULL？
        print $delim, $matrix_ref->[$i][$j];
        $delim = ",";
    }
    print "\n";
}
```

如果结果集为空，`fetchall_arrayref()` 返回一个指向空数组的引用。如果发生错误，结果为 `undef`，因此如果你没有启用 RaiseError，必须在使用返回值之前检查它。

行数和列数由矩阵是否为空来决定。如果你想将矩阵的第 $i 行作为数组访问，请使用语法 `@{$matrix_ref->[$i]}`。

使用 `fetchall_arrayref()` 获取结果集当然比编写逐行获取循环更简单，尽管访问数组元素的语法稍微复杂一些。另一种类似于 `fetchall_arrayref()` 但执行更多工作的是 `selectall_arrayref()`。该方法为你执行整个 `prepare()`、`execute()` 和获取循环序列。要使用 `selectall_arrayref()`，使用数据库句柄将你的语句直接传递给它：

```perl
# 将所有行获取为引用数组的引用
my $matrix_ref = $dbh->selectall_arrayref($stmt);

# 确定矩阵的维度
my $rows = (defined @{$matrix_ref} ? 0 : scalar (@{@matrix_ref}));
my $cols = ($rows == 0 ? 0 : scalar (@{@matrix_ref->[0]}));

for (my $i = 0; $i < $rows; $i++)  # 打印每一行
{
    my $delim = "";
    for (my $j = 0; $j < $cols; $j++)
    {
        $matrix_ref->[$i][$j] = "" if !defined ($matrix_ref->[$i][$j]); # NULL？
        print $delim, $matrix_ref->[$i][$j];
        $delim = ",";
    }
    print "\n";
}
```

### 8.2.5.5 检查 NULL 值

当你从数据库中检索信息时，可能需要区分 NULL 列值与零或空字符串。这很容易做到，因为 DBI 将 NULL 列值作为 `undef` 返回。但是，你必须确保使用正确的测试。如果你尝试以下代码片段，它会三次打印“false!\n”：

```perl
$col_val = undef;  if (!$col_val) { print "false!\n"; }
$col_val = 0;      if (!$col_val) { print "false!\n"; }
$col_val = "";     if (!$col_val) { print "false!\n"; }
```

这证明这种测试形式无法区分 `undef`、0 和空字符串。下一个片段在两个测试中都打印 `*false!*`，表明该测试无法区分 `undef` 和空字符串：

```perl
$col_val = undef;  if ($col_val eq "") { print "false!\n"; }
$col_val = "";     if ($col_val eq "") { print "false!\n"; }
```

这个片段打印相同的输出，表明第二个测试无法区分 0 和空字符串：

```perl
$col_val = 0;
if (!$col_val eq "") { print "false!\n"; }
if ($col_val == 0)   { print "false!\n"; }
```

要区分 `undef` (NULL) 列值和非 `undef` 值，请使用 `defined()`。在知道某个值不代表 NULL 之后，你可以使用适当的测试来区分其他类型的值。例如：

```perl
if (!defined ($col_val))    { print "NULL\n"; }
elsif ($col_val eq "")       { print "empty string\n"; }
elsif ($col_val == 0)       { print "zero\n"; }
else                        { print "other\n"; }
```

按正确顺序执行测试很重要，因为如果 `$col_val` 是空字符串，第二个和第三个比较都为真。如果你颠倒了这些比较的顺序，你会错误地将空字符串解释为零。

### 8.2.6 在语句字符串中引用特殊字符

到目前为止，我们以最基本的方式构建语句，使用简单的引号字符串。当你的引号字符串包含引号值时，这会在 Perl 词法层面引起问题。当你要插入或选择包含引号、反斜杠或二进制数据的值时，也可能在 SQL 层面遇到问题。如果你将语句指定为 Perl 引号字符串，必须转义语句字符串本身中出现的任何引号字符：

```perl
$stmt = 'INSERT INTO absence VALUES(14, \'2008-09-16\')';
$stmt = "INSERT INTO absence VALUES(14, \'2008-09-16\')";
```

Perl 和 MySQL 都允许使用单引号或双引号来引用字符串，因此有时可以通过混合使用引号字符来避免转义：

```perl
$stmt = 'INSERT INTO absence VALUES(14, "2008-09-16")';
$stmt = "INSERT INTO absence VALUES(14, '2008-09-16')";
```

