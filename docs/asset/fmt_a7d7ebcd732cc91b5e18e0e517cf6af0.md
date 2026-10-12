
```perl
sub edit_member
{
    # 列名数组的引用和条目哈希表的引用
    my ($col_name_ref, $entry_ref) = @_;

    # 显示初始值，询问是否继续编辑
    show_member ($col_name_ref, $entry_ref);
    return unless prompt ("\nEdit this entry (y/n)? ") =~ /y/i;
    # 提示输入新值；用户输入新值，或按 Enter
    # 保持原值不变，输入 'NONE' 清除值，或
    # 输入 'EXIT' 退出不修改记录。
    foreach my $col_name @{$col_name_ref}
    {
        next if $col_name eq 'member_id'; # 跳过键字段
        my $col_val = col_prompt ($col_name, $entry_ref);
        next if $col_val eq ''; # 用户按下了 Enter
        return if uc ($col_val) eq 'EXIT'; # 提前退出
        if (uc ($col_val) eq 'NONE')
        {
            # 如果列允许为 NULL，则填入 NULL，否则填入空字符串
            $col_val = ($nullable{$col_name} ? undef : '');
        }
        $entry_ref->{$col_name} = $col_val;
    }

    # 显示新值，在更新前询问确认
    show_member ($col_name_ref, $entry_ref);
    return unless prompt ("\nUpdate this entry (y/n)? ") =~ /y/i;

    # 构建 UPDATE 查询，然后执行。
    my $stmt = 'UPDATE member';
    my $delim = ' SET '; # 在第一列前放 'SET'，其余列前放 ','
    foreach my $col_name @{$col_name_ref}
    {
        next if $col_name eq 'member_id'; # 跳过键字段
        # quote() 将输入引为单词 NULL（无引号），
        # 这正是我们想要的。
        $stmt .= sprintf ('%s %s%s', $delim, $col_name,
            $dbh->quote ($entry_ref->{$col_name}));
        $delim = ','; 
    }
    $stmt .= " WHERE member_id = " . $dbh->quote ($entry_ref->{member_id});
    $dbh->do ($stmt) or warn "Warning: entry not updated!\n"
}
```

看起来像日期。在一个通用数据录入应用程序中，你可能希望提取表的元信息以确定其所有列的类型。然后你可以基于这些类型设定验证约束。这比本文要涉及的内容要复杂，所以我只在 `col_prompt()` 函数中添加了一个快速的“临时方案”来检查输入格式（当列为 *expiration* 时）。一个最小化的数据值检查可以这样进行：

```perl
sub col_prompt
{
    my ($col_name, $entry_ref) = @_;
    loop:
    my $prompt = $col_name;
    if (defined ($entry_ref))
    {
        my $cur_val = $entry_ref->{$col_name};
        $cur_val = "NULL" if !defined ($cur_val);
        $prompt .= " [$cur_val]";
    }
    $prompt .= ": ";
    print STDERR $prompt;
    my $str = <STDIN>;
    chomp ($str);
    # 对 expiration 日期进行初步检查
    if ($str && $col_name eq 'expiration') # 检查 expiration 日期格式
    {
        if ($str !~ /^\d+\D\d+\D\d+\d$/)
        {
            warn "$str is not a legal date, try again\n";
            goto loop;
        }
    }
    return ($str);
}
```

该模式测试的是由非数字字符分隔的三组数字序列。这只是一个部分检查，因为它无法检测出诸如 "1999-14-92" 这样的非法值。为了改进脚本，你可以实施更严格的日期检查，或添加其他检查，例如要求姓和名字段必须填入非空值。还可以进行其他改进：

- 如果用户未对现有条目做任何更改，则跳过更新操作。你可以通过保存成员条目各列的原始值来实现，然后编写 `UPDATE` 语句，仅更新那些发生变化的列。如果没有列变化，甚至无需发出该语句。

- 如果在用户编辑期间该行已被其他人修改，则通知用户。要做到这一点，可以在 `WHERE` 子句中加入条件：对每个原始列值，添加 `AND col_name = col_val`。这样，如果其他人已经修改过该行，`UPDATE` 操作将会失败。

修改了该行，这会提供反馈，表明有两个人正在同时尝试更改该条目。

- 启用严格 SQL 模式和其他输入限制，这会导致 MySQL 本身拒绝无效值，并且如果输入无法按给定方式使用，则返回错误：

```sql
$dbh->do ("SET sql_mode = 'TRADITIONAL';");
```

这是 `edit_member.pl` 脚本的另一个你可能需要考虑如何处理 shortcomings（缺陷/不足之处）：如前所述，该脚本在执行提示循环之前打开了数据库连接，并且直到在循环内写完该行之后才关闭连接。如果用户花了很长时间输入或更新该行，或者只是碰巧做了一会儿其他事情，连接可能会保持打开状态很长时间。你如何修改 `edit_member.pl` 以仅在必要时保持连接打开？

### 8.3.4 寻找具有共同兴趣的历史联盟成员

历史联盟秘书的职责之一是处理成员关于美国历史领域内特定兴趣（如大萧条或亚伯拉罕·林肯的生平）的其他成员名单的请求。当目录通过文字处理文档维护时，使用文字处理器的“查找”功能查找这样的成员相当容易。然而，生成仅由符合条件的成员条目组成的列表要困难得多，因为这涉及大量的复制和粘贴。使用 MySQL 后，这项工作变得容易得多，因为我们只需运行这样的查询：

```sql
SELECT * FROM member WHERE interests LIKE '%lincoln%'
ORDER BY last_name, first_name
```

不幸的是，如果我们从 `mysql` 客户端运行此查询，结果看起来并不太美观。让我们编写一个小型 DBI 脚本 `interests.pl`，为我们执行搜索并生成更美观的输出。`interests.pl` 首先检查命令行上是否至少有一个命名参数，因为否则就没有可搜索的内容。然后，对于每个参数，脚本在 `member` 表的 `interests` 列上执行搜索：

```perl
@ARGV or die "Usage: interests.pl keyword\n";
search_members (shift (@ARGV)) while @ARGV;
```

为了搜索关键词字符串，我们在每侧添加 `'%'` 通配符字符并执行模式匹配，以便字符串可以在 `interests` 列的任何位置找到。然后我们打印匹配的条目：
