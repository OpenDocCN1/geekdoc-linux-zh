
## 第 8 章 使用 Perl DBI 编写 MySQL 程序

`read_file()` 函数读取文件的内容（假设文件已打开）并检查每行的第一个字段。（如果我们把 `renewal_renewal.pl` 的输出提供给 `renewal_notify.pl`，每行会有多个字段，但我们只想查看第一个字段，其中将包含成员 ID 号码。）

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

`interpret_argument()` 函数对每个参数进行分类，以确定它是 ID 号码、电子邮件地址还是文件名。对于 ID 号码和电子邮件地址，它会查找相应的成员条目并将其传递给 `notify_member()`。对于通过电子邮件地址指定的成员，我们必须小心。两个成员可能拥有相同的地址（例如，丈夫和妻子），我们不希望向与其无关的人发送消息。为了避免这种情况，我们会查找对应于该电子邮件地址的成员 ID，以确保恰好有一个。如果该地址匹配多个 ID 号码，则存在歧义，我们在打印警告后将其忽略。如果参数看起来不像 ID 号码或电子邮件地址，则将其视为要读取以获取进一步输入的文件名。我们在这里也必须小心——如果正在读取文件，我们就不要再读取文件，以避免无限循环的可能性：

```perl
sub interpret_argument
(
    my ($arg, $recurse) = @_;

    if ($arg =~ /^(\d+$)/)        # 数字成员 ID
    {
        notify_member ($arg);
    }
    elsif ($arg =~ /@/)    # 电子邮件地址
    {
        # 获取与地址相关的 member_id
        # （应该恰好有一个）
        my $stmt = qq( SELECT member_id FROM member WHERE email = ? );
        my $ary_ref = $dbh->selectcol_arrayref ($stmt, undef, $arg);
        if (scalar (@$ary_ref)) == 0) {
            warn "电子邮件地址 $arg 不匹配任何条目：已忽略\n";
        }
        elif (scalar (@{$ary_ref}) > 1)
        {
            warn "电子邮件地址 $arg 匹配多个条目：已忽略\n";
        }
        else
        {
            notify_member ($ary_ref->[0]);
        }
    }
    else                    # 文件名
    {
        if (!$recurse)
        {
            warn "文件内的文件名 $arg：已忽略\n";
        }
        else
        {
            open (IN, $arg) or die "无法打开 $arg: $!\n";
            read_file (*IN);
            close (IN);
        }
    }
)
```

`notify_member()` 函数负责实际发送续费通知。如果结果是成员没有电子邮件地址，`notify_member()` 无法发送任何消息，但它会打印警告，以便你知道需要通过其他方式联系该成员。你可以调用 `show_member.pl` 并传入消息中显示的成员 ID 号码来查看完整条目——例如，找出该成员的电话号码和地址。`notify_member()` 如下所示：

```perl
sub notify_member
{
    my $member_id = shift;

    warn "正在通知 $member_id...\n";
    my $stmt = qq( SELECT * FROM member WHERE member_id = ? );
    my $sth = $dbh->prepare ($stmt);
    $sth->execute ($member_id);
    my %col_name = @{$sth->{NAME}};
    my $entry_ref = $sth->fetchrow_hashref ();
    $sth->finish ();
    if (!$entry_ref)            # 未找到成员！
    {
        warn "未找到成员 $member_id 的条目\n";
        return;
    }
    if (!defined ($entry_ref->{email}))   # 条目中无电子邮件地址
    {
        warn "成员 $member_id 没有电子邮件地址；未发送消息\n";
        return;
    }
    open (OUT, "| sendmail") or die "无法打开邮件发送器\n";
    print OUT <<EOF;
To: $entry_ref->{email}
Subject: Your USHL membership is in need of renewal

Greetings: Your membership in the U.S. Historical League is
due to expire soon. We hope that you'll take a few minutes to
contact the League office to renew your membership. The
contents of your member entry are shown below. Please note
particularly the expiration date.

Thank you.
EOF
    foreach my $col_name (@col_names)
    {
        print OUT "$col_name:";
        print OUT " $entry_ref->{$col_name}"
        if defined ($entry_ref->{$col_name});
        print OUT "\n";
    }
    close (OUT);
}
```

`notify_member()` 函数通过打开指向 `sendmail` 程序的管道并将邮件消息推入管道来发送邮件。`sendmail` 的路径名作为参数在 `renewal_notify.pl` 脚本的开头附近设置。你可能需要更改此路径，因为 `sendmail` 的位置因系统而异：

```perl
# 更改路径以匹配你的系统
my $sendmail = '/usr/sbin/sendmail -t -oi';
```

如果你没有 `sendmail`，脚本将无法正常工作。（例如，Windows 系统通常没有安装 `sendmail`。）为了处理这种情况，`sample` 发行版包含一个名为 `renewal_notify2.pl` 的 `renewal_notify.pl` 修改版本，它使用无需 `sendmail` 程序即可工作的 Mail::Sendmail 模块。如果你安装了该模块，可以使用 `renewal_notify2.pl` 代替。

你可以让此脚本变得更复杂。例如，你可以在 `member` 表中添加一列，记录最近一次续费提醒发送的时间，然后修改 `renewal_notify.pl` 在发送邮件时更新该列。这样做将有助于避免过于频繁地发送通知。就目前而言，我们假设你不会比大约每月一次更频繁地运行此程序。

这两个脚本现在完成了。你可以按如下方式使用它们：

1.  运行 **need_renewal.pl** 生成已过期或即将过期的会员资格列表：
    `% ./need_renewal.pl > tmp`
2.  查看 **tmp** 以检查其是否合理。
3.  如果合理，将其用作 **renewal_notify.pl** 的输入以发送续费消息：
    `% ./renewal_notify.pl tmp`

要通知单个成员，你可以通过 ID 号码或电子邮件地址指定他们。例如，以下命令通知成员 18 以及拥有电子邮件地址 **g.steve@pluto.com** 的成员：
`% ./renewal_notify.pl 18 g.steve@pluto.com`

### 8.3.3 历史学会成员条目编辑

在我们开始发送续费通知后，我们可以合理地假设我们要通知的一些人会更新他们的会员资格。当这种情况发生时，我们需要一种方法来用新的到期日期更新他们的条目。在下一章中，我们将开发一种通过 Web 编辑成员行的方法，但本节展示了如何编写一个命令行脚本 **edit_member.pl**，它使你能够使用提示输入条目每个部分的新值这种简单方法更新条目。它的工作原理如下：

-   如果在命令行上没有参数调用，**edit_member.pl** 假设你想输入一个新成员。它会提示输入要放置在成员条目中的初始信息，并创建一个新的条目。
-   如果在命令行上带有成员 ID 号码调用，**edit_member.pl** 查找条目的现有内容，然后提示更新每一列。如果你为某列输入一个值，它将替换当前值。如果你按 Enter，该列不会更改。如果你输入单词 "none"，它将清除该列的当前值。（如果你不知道成员的 ID 号码，你可以运行 **show_member.pl last_name** 来查看哪些条目匹配给定的姓氏，并由此确定正确的 ID。）

如果只是想更新成员的到期日期，允许以这种方式编辑整个条目可能有点过度了。另一方面，像这样的脚本也为其用户提供了一种简单的通用方法，用于更新条目的任何部分而无需知道任何 SQL。（一个特殊情况是，**edit_member.pl** 不允许你更改 **member_id** 字段，因为该字段在创建条目时自动分配，之后不应更改。）

