
`WHERE expiration < DATE_ADD(CURDATE(), INTERVAL cutoff DAY)`

`cutoff`表示我们希望给予的宽限天数。该查询选择那些在少于该天数内到期续费（或已过期）的会员条目。要仅查找已过期的会员资格，`cutoff`值为0可识别出过期日期在过去的那些行。

# 8.3 应用 DBI

在确定了需要通知的行之后，我们应该如何处理它们？一种选择是直接在同一脚本中发送邮件，但可能先审查列表再发送消息会更有用。因此，我们将采用两阶段方法：

1. 运行`need_renewal.pl`脚本，生成需要续费的会员列表。你可以审查并验证或编辑该列表，然后将其作为第二阶段发送续费通知的输入。
2. 运行`renewal_notify.pl`脚本，通过电子邮件向会员发送“请续费”通知。该脚本应警告你那些没有电子邮件地址的会员，以便你通过其他方式联系他们。

对于该任务的第一部分，`need_renewal.pl`脚本必须识别哪些会员需要续费。脚本的主要部分如下所示：

```
# use default cutoff of 30 days…
my $cutoff = 30;

# …but reset if a numeric argument is given on the command line
$cutoff = shift (@ARGV) if @ARGV && $ARGV[0] =~ /^\d+$/;

# inform user what cutoff the script is using
warn "Using cutoff of $cutoff days\n";

my $sth = $dbh->prepare (qq{
 SELECT
 member_id, email, last_name, first_name, expiration,
 TO_DAYS(expiration) - TO_DAYS(CURDATE()) AS days
 FROM member
 WHERE expiration < DATE_ADD(CURDATE(), INTERVAL ? DAY)
 ORDER BY expiration, last_name, first_name
});

$sth->execute ($cutoff); # pass cutoff as placeholder value

while (my $entry_ref = $sth->fetchrow_hashref ())
{
 # convert undef values to empty strings for printing
foreach my $key (keys %{$entry_ref}))
{
 $entry_ref->{$key} = '' if !defined ($entry_ref->{$key});
}

print join ("\t",
 $entry_ref->{member_id},
 $entry_ref->{email},
 $entry_ref->{last_name},
 $entry_ref->{first_name},
 $entry_ref->{expiration},
 $entry_ref->{days},
);
}
```

`needed_renewal.pl`脚本的输出类似于以下内容（由于结果是根据当前日期确定的，而你在阅读本书时与我写作时的当前日期不同，因此你会得到不同的输出）：

```
89 g_steve@pluto.com         Garner Steve    2007-08-03  -38 days
18 york_mark@earth.com       York Mark       2007-08-24  -17 days
82 john_edwards@venus.org    Edwards John     2007-09-12   2 days
```

请注意，有些会员资格需要在负天数内续费。这意味着它们已经过期！（这种情况发生在你手动维护行数据时；人们可能会从缝隙中溜过去。现在既然我们将信息存入数据库，我们发现之前遗漏了少数人。）

续费通知任务的第二部分涉及一个名为`renewal_notify.pl`的脚本，它通过电子邮件发出通知。为了使`renewal_notify.pl`更易用，我们可以让它理解三种类型的命令行参数：会员 ID 号、电子邮件地址和文件名。数字参数表示会员 ID 值，包含`@`字符的参数表示电子邮件地址。其他任何内容都被解释为应读取以查找 ID 号或电子邮件地址的文件名。这种方法允许你通过 ID 号或电子邮件地址指定会员，你可以直接在命令行上这样做，也可以将它们列在文件中。（特别是，你可以将`needed_renewal.pl`的输出保存在文件中，然后使用该文件作为`renewal_notify.pl`的输入。）

对于每个需要发送通知的会员，脚本查找相关的成员表条目，提取电子邮件地址，并向该地址发送消息。如果条目中没有地址，`renewal_notify.pl`将生成一条警告消息，提示你需以其他方式联系这些会员。

主要的参数处理循环如下。如果未在命令行上指定任何参数，我们则读取标准输入作为输入值。否则，我们将每个参数传递给`interpret_argument()`以将其分类为 ID 号、电子邮件地址或文件名：

```
if (@ARGV == 0)   # no arguments, read STDIN for values
{
    read_file (\*STDIN);
}
else
{
    while (my $arg = shift (@ARGV))
    {
        # interpret argument, with filename recursion
        interpret_argument ($arg, 1);
    }
}
```

## 第 8 章 使用 Perl DBI 编写 MySQL 程序

`read_file()`函数读取文件的内容（假设文件已打开）并检查每行的第一个字段。（如果我们把`renewal_renewal.pl`的输出提供给`renewal_notify.pl`，每行会有多个字段，但我们只想查看第一个字段，其中将包含成员 ID 号码。）

```perl
sub read_file
(
    my $fh = shift;    # 已打开文件的句柄
    my $arg;

    while (defined ($arg = <$fh>)) {
        # 去除第 1 列之后的所有内容，包括换行符
        $arg =~ s/\b.*/|/g;
        # 解析参数，不进行文件名递归
        interpret_argument ($arg, 0);
    }
)
```

`interpret_argument()`函数对每个参数进行分类，以确定它是 ID 号码、电子邮件地址还是文件名。对于 ID 号码和电子邮件地址，它会查找相应的成员条目并将其传递给`notify_member()`。对于通过电子邮件地址指定的成员，我们必须小心。两个成员可能拥有相同的地址（例如，丈夫和妻子），我们不希望向与其无关的人发送消息。为了避免这种情况，我们会查找对应于该电子邮件地址的成员 ID，以确保恰好有一个。如果该地址匹配多个 ID 号码，则存在歧义，我们在打印警告后将其忽略。如果参数看起来不像 ID 号码或电子邮件地址，则将其视为要读取以获取进一步输入的文件名。我们在这里也必须小心——如果正在读取文件，我们就不要再读取文件，以避免无限循环的可能性：
