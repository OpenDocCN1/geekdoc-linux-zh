
`edit_member.pl` 需要知道的第一件事是 `member` 表中各列的名称，以及它们是否可以被赋值为 NULL。后一种属性将在清除列值时用到（如果列允许为 NULL，我们就将列赋值为 NULL，否则赋值为空字符串）。所需的信息可从 `INFORMATION_SCHEMA` 数据库的 `COLUMNS` 表中获取：

```perl
my @col_name = ();   # 列名数组
my %nullable = ();   # 列的空值允许性，以列名为键
# 获取 member 表的列名
my $sth = $dbh->prepare (qq{
    SELECT COLUMN_NAME, UPPER(IS_NULLABLE)
    FROM INFORMATION_SCHEMA.COLUMNS
    WHERE TABLE_SCHEMA = ? AND TABLE_NAME = ?
});
$sth->execute ('s&mpdb', 'member');
while (my ($col_name, $is_nullable) = $sth->fetchrow_array ())
{
  push (@col_name, $col_name);
  $nullable{$col_name} = ($is_nullable eq "YES");
}
```

利用这些列信息，脚本生成一个按顺序包含列名的数组，以及一个以列名为键、指示每列是否*可为空（nullable）*的哈希表。随后，`edit_member.pl` 进入主循环：

```perl
if (@ARGV == 0) { # 如果未提供参数，则创建新条目
{
    # 传递列名数组的引用
    new_member (\@col_name);
}
else        # 否则，使用参数作为成员 ID 来编辑条目
{
    # 保存 @ARGV，然后清空它，以便脚本从 STDIN 读取时，
    # 不会将 @ARGV 的内容解释为输入文件名
    my @id = @ARGV;
    @ARGV = ();
    # 对每个 ID 值，查找对应条目，然后进行编辑
    while (my $id = shift (@id))
    {
        $sth = $dbh->prepare (qq{
            SELECT * FROM member WHERE member_id = ?
        });
        $sth->execute ($id);
        my $entry_ref = $sth->fetchrow_hashref ();
        $sth->finish ();
        if (!$entry_ref)
        {
            warn "No member exists with member ID = $id\n";
            next;
        }
        # 传递列名数组的引用和条目的引用
        edit_member (\@col_name, $entry_ref);
    }
}
```

创建新成员条目的代码会提示用户输入每个成员表列的值，然后发出一个 `INSERT` 语句以添加新行：

```perl
sub new_member
{
    my $col_name_ref = shift;    # 列名数组的引用
    my $entry_ref = { };         # 将新条目创建为哈希表

    return unless prompt ('Create new entry (y/n)? ') =~ /y/i;
    # 提示输入新值；用户输入新值，或按 Enter
    # 保持原值不变，输入 'NONE' 清除值，或
    # 输入 'EXIT' 退出而不创建记录。
    foreach my $col_name (@{$col_name_ref})
    {
        next if $col_name eq 'member_id';    # 跳过键字段
        my $col_val = col_prompt ($col_name, undef);
        next if $col_val eq '' ;          # 用户按下了 Enter
        return if uc ($col_val) eq 'EXIT';   # 提前退出
        if (uc ($col_val) eq 'NONE')
        {
            # 如果列允许为 NULL，则填入 NULL，否则填入空字符串
            $col_val = ($nullable{$col_name} ? undef : '');
        }
        $entry_ref->{$col_name} = $col_val;
    }
    # 显示值，在插入前询问确认
    show_member ($col_name_ref, $entry_ref)
    return unless prompt ('\nInsert this entry (y/n)? ') =~ /y/i;

    # 构建 INSERT 查询，然后执行。
    my $stmt = "INSERT INTO member";
    my $delim = ' SET ';  # 在第一列前放 'SET'，其余列前放 ','
    foreach my $col_name (@{$col_name_ref})
    {
        # 仅为已赋值的那些列指定值
        next if !defined ($entry_ref->{$col_name});
        # quote() 将 undef 引为单词 NULL（无引号），
        # 这正是我们想要的。非 NULL 列将被赋为其默认值。
        $stmt .= sprintf ('%s%s=%s', $delim, $col_name,
                          $dbh->quote ($entry_ref->{$col_name}));
        $delim = ',';
    }
    $dbh->do ($stmt) or warn 'Warning: new entry not created!\n'
}
```

`edit_member.pl` 使用两个例程提示用户输入信息。`prompt()` 提出一个问题并返回答案：

```perl
sub prompt
{
    my $str = shift;
    print STDERR $str;
    chomp ($str = <STDIN>);
    return ($str);
}
```

`col_prompt()` 接收一个列名参数。它打印列名作为提示以获取新的列值，并返回用户输入的值：

```perl
sub col_prompt
{
    my ($col_name, $entry_ref) = @_;
    my $prompt = $col_name;
    if (defined ($entry_ref))
    {
        my $cur_val = $entry_ref->{$col_name};
        $cur_val = 'NULL' if !defined ($cur_val);
        $prompt .= " [$cur_val]";
    }
    $prompt .= ": ";
    print STDERR $prompt;
    my $str = <STDIN>;
    chomp ($str);
    return ($str);
}
```

`col_prompt()` 的第二个参数是一个指向表示成员条目的哈希表的引用。对于创建新条目，此值将为 `undef`；但在编辑现有行时，它将指向条目的当前内容。在这种情况下，`col_prompt()` 会在提示字符串中包含当前列的值，以便用户能看到该值。用户只需按 Enter 即可接受该值。

编辑现有成员条目的代码与创建新成员条目的代码类似。不过，由于我们要处理的是一个已存在的条目，提示例程会显示当前条目的值，且 `edit_member()` 函数会发出 `UPDATE` 语句而非 `INSERT`：
