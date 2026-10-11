

直至该点的追踪输出。例如，如果你在某个特定的 SELECT 查询中遇到问题，你可以追踪与该查询相关的语句句柄：

```perl
my $sth = $dbh->prepare (qq{ SELECT ... }); # 创建语句句柄
$sth->trace (1); # 对语句启用追踪
$sth->execute ();
```

如果你为任何 trace() 调用指定了文件名参数，无论是针对整个 DBI 还是针对单个句柄，所有追踪输出都会写入该文件。

TraceLevel 属性是 trace() 方法的一种替代方式。该属性允许你为给定的句柄设置或获取追踪级别：

```perl
$dbh->{TraceLevel} = 3; # 设置数据库句柄的追踪级别
my $cur_level = $sth->{TraceLevel}; # 获取语句句柄的追踪级别
```

若要全局开启追踪，使其对你运行的所有 DBI 脚本生效，请在你的 shell 中设置 DBI_TRACE 环境变量。具体语法取决于你使用的 shell：

- 对于 csh 或 tcsh：
  - `setenv DBI_TRACE value`
- 对于 sh, bash 或 ksh：
  - `export DBI_TRACE=value`
- 对于 Windows：
  - `C:\> set DBI_TRACE=value`

value 的格式在所有 shell 中都是相同的：一个数字 n 表示在级别 n 向 STDERR 开启追踪，一个文件名表示向指定文件开启级别 2 的追踪，或者 n=filename 表示向指定文件开启级别 n 的追踪。以下是一些使用 tcsh 语法的示例：

- 向 STDERR 进行级别 1 的追踪：
  - `setenv DBI_TRACE 1`
- 向文件 trace.out 进行级别 1 的追踪：
  - `setenv DBI_TRACE 1=trace.out`
- 向文件 trace.out 进行级别 2 的追踪：
  - `setenv DBI_TRACE 2=trace.out`

使用 DBI_TRACE 的优势在于，你可以在不修改脚本的情况下启用 DBI 脚本追踪。但如果你从 shell 开启向文件追踪，请在解决问题后务必将其关闭。调试输出是追加到追踪文件中的，而不会覆盖它，因此如果你不小心，该文件可能会变得非常大。

在 shell 启动文件（如 .cshrc, .tcshrc, .login 或 .profile）中定义 `DBI_TRACE` 是一个特别糟糕的主意！

要在各种命令解释器中关闭 `DBI_TRACE`，请使用以下任一命令：

- 对于 csh 或 tcsh：
  ```bash
  setenv DBI_TRACE 0
  unsetenv DBI_TRACE
  ```
- 对于 sh, bash 或 ksh：
  ```bash
  unset DBI_TRACE
  export DBI_TRACE=0
  ```
- 对于 Windows：
  ```bash
  C:\> unset DBI_TRACE
  C:\> set DBI_TRACE=0
  ```

### 8.2.11 使用结果集元数据

你可以使用 DBI 来访问结果集元数据——即关于查询所选行的描述信息。要获取这些信息，请访问与生成结果集的查询相关的语句句柄的属性。其中一些是标准 DBI 属性，适用于所有数据库驱动程序（例如 `NUM_OF_FIELDS`，表示结果集中的列数）。其他则是 MySQL 特有的属性，由 DBI 的 MySQL 驱动程序 DBD::mysql 提供。这些属性（例如 `mysql_max_length`，它告诉你每列值的最大宽度）不适用于其他数据库系统。如果你使用任何 MySQL 特有的属性，你都有风险使脚本无法移植到其他数据库。另一方面，它们可以使你更容易获取想要的信息。

你必须在正确的时间请求元数据。通常，结果集属性在你调用 `prepare()` 和 `execute()` 之前对 `SELECT` 语句是不可用的。此外，当你使用行获取函数到达结果集的末尾，或者在你调用 `finish()` 之后，属性可能会变得无效。

下面的示例展示了如何结合使用其中一个 MySQL 特有的元数据属性 `mysql_max_length` 与更通用的属性 `NUM_OF_FIELDS`（指示结果集中的列数）和 `NAME`（保存列名）。我们可以结合这些属性提供的信息来编写一个脚本 `tabular.pl`，该脚本以你在交互模式下运行 `mysql` 客户端程序时获得的相同表格（带框）风格，从 `SELECT` 查询中生成输出。`tabular.pl` 的主体如下所示。你可以用其他任何语句替换 `SELECT` 语句；输出写入例程与特定语句无关。

```perl
my $sth = $dbh->prepare (qq{
SELECT last_name, first_name, suffix, city, state
FROM president ORDER BY last_name, first_name
    });
$sth->execute (); # 在此调用后，属性应该可用

# 结果集中列值实际最大宽度
my $wid = @{$sth->{mysql_q1_max_length()}};
# 结果集中的列数
my $ncols = $sth->{NUM_OF_FIELDS};

# 如果数据值比列标题窄，或者比单词 'NULL' 窄，则调整列宽
for (my $i = 0; $i < $ncols; $i++)
{
  my $name_wid = length ($sth->{NAME}>[$i]);
  $wid[$i] = $name_wid if $wid[$i] < $name_wid;
  $wid[$i] = 4 if $wid[$i] < 4;
}

# 打印表格格式输出
print_dashes (\@wid, $ncols);        # 破折号行
print_row ($sth->{NAME}, \@wid, $ncols); # 列标题
print_dashes (\@wid, $ncols);        # 破折号行
while (my $ary_ref = $sth->fetchrow_arrayref ())
{
  print_row ($ary_ref, \@wid, $ncols);   # 行数据值
}
print_dashes (\@wid, $ncols);        # 破折号行
```

在通过 execute() 启动语句后，我们可以获取所需的元数据。$sth->{NUM_OF_FIELDS} 是一个标量值，指示结果集中有多少列。$sth->{NAME} 和 $sth->{mysql_q1_max_length()} 给我们提供了列名和每列值的最大宽度。这两个属性中每一个的值都是指向数组的引用，该数组为结果集中的每一列包含一个元素，顺序与语句中列名的顺序一致。

其余计算与第 7 章中开发的 exec_stmt 程序所使用的非常相似。例如，为了避免输出错位，如果列名比该列中的任何数据值都宽，我们会向上调整列宽值。

输出函数 print_dashes() 和 print_row() 编写如下。它们也与 exec_stmt 中对应的代码相似：

```perl
sub print_dashes
{
  my $wid_ary_ref = shift;  # 列宽数组的引用
  my $cols = shift;         # 列数

  for (my $i = 0; $i < $cols; $i++)
  {
    print "*", "-" x ($wid_ary_ref>[$i]+2);
  }
  print "*\n";
}

# 打印数据行。（不右对齐数值列）
sub print_row
{
  my $val_ary_ref = shift; # 列值数组的引用
  my $wid_ary_ref = shift; # 列宽数组的引用
  my $cols = shift; # 列数
  for (my $i = 0; $i < $cols; $i++)
  {
    printf "| %-*s ", $wid_ary_ref->[$i],
    defined ($val_ary_ref->[$i]) ? $val_ary_ref->[$i] : 'NULL';
  }
  print "|\n";
}
```

`tabular.pl` 的输出如下所示：

| last_name | first_name | suffix | city | state |
|---|---|---|---|---|
| Adams | John | NULL | Braintree | MA |
| Adams | John Quincy | NULL | Braintree | MA |
| Arthur | Chester A. | NULL | Fairfield | VT |
| Buchanan | James | NULL | Mercersburg | PA |
| Bush | George H.W. | NULL | Milton | MA |
| Bush | George W. | NULL | New Haven | CT |
| Carter | James E. | Jr. | Plains | GA |
| ... | | | | |

我们的下一个脚本使用列元数据以不同的格式生成输出。这个脚本 `show_member.pl` 允许你在不输入任何查询的情况下快速查看 Historical League 成员条目。给定成员的姓氏，它会像这样显示选定的条目：

```text
$ ./show_member.pl artel
last_name: Artel
first_name: Mike
suffix: expiration: 2011-04-16 email: mike_artel@venus.org street: 4264 Lovering Rd. city: Miami
state:          FL
zip:            12777
phone:          075-961-0712
interests:      Civil Rights, Education, Revolutionary War
member_id:      63
```

你也可以使用会员编号或 SQL 模式匹配多个姓氏来调用 show_member.pl。以下命令显示了会员 23 或姓氏以 "C" 开头的会员的条目：

```bash
% ./show_member.pl 23
% ./show_member.pl C%
```

show_member.pl 脚本的主体如下所示。它使用 NAME 属性来确定每行输出使用的标签，并使用 NUM_OF_FIELDS 属性来确定结果集包含多少列：

```perl
my $count = 0;    # 迄今为止打印的条目数
my @label = ();   # 列标签数组
my $label_wid = 0;

while (@ARGV) {    # 为命令行上的每个参数运行查询
{
  my $arg = shift (@ARGV);

  # 默认是按姓氏进行模式搜索...
  my $clause = 'last_name LIKE ' . $dbh->quote ($arg);
  # ...但如果参数是数字，则改为 ID 搜索
  $clause = "member_id = " . $dbh->quote ($arg) if $arg =~ /^\d+$/;

  # 发出查询
  my $sth = $dbh->prepare (qq{
    SELECT * FROM member
      WHERE $clause
      ORDER BY last_name, first_name
  });
  $sth->execute ();

  # 获取用于标签的列名，
  # 并确定最大列名宽度以进行格式化
  # （但仅在循环的第一次遍历时执行此操作）
  if ($label_wid == 0)
  {
    @label = @{$sth->{NAME}};
    foreach my $label (@label)
    {
      $label_wid = length ($label) if $label_wid < length ($label);
    }
  }
```

