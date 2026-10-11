

# 输出页面的初始部分
my $title = "$db_name 数据库浏览器";
print header ();
print start_html (-title => $title, -bgcolor => "white");
print h1 ($title);

# 在 URL 中查找的参数
my $tbl_name = param ("tbl_name");
my $sort_col = param ("sort_col");

# 如果 $tbl_name 没有值，则显示一个可点击的表列表。
# 否则，显示给定表的内容。如果设置了
# $sort_col，则表示要按该列进行排序。

if (!defined ($tbl_name))
{
    display_table_names ($dbh, $db_name);
}
else
{
    display_table_contents ($dbh, $db_name, $tbl_name, $sort_col);
}

print end_html ();

很容易找出某个参数的值，因为 CGI.pm 完成了所有查找 Web 服务器传递给脚本的信息的工作。我们只需要调用 `param()` 并传入感兴趣的参数名称即可。在 `db_browse.pl` 的主体中，该参数名为 `tbl_name`。如果未设置该参数，这是脚本的初始调用，它将显示表列表。否则，它将显示由 `tbl_name` 参数命名的表的内容，并按 `sort_col` 参数命名的列进行排序。

`display_table_names()` 函数生成初始页面。`display_table_names()` 检索表列表，并输出一个无序列表，其中每个项目都是同一数据库中某个表的名称：

```perl
sub display_table_names
{
    my ($dbh, $db_name) = @_;

    print p ("点击其名称选择一个表：");

    # 检索单列表名称数组的引用
    my $sth = $dbh->prepare (qq
    SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES
    WHERE TABLE_SCHEMA = ? ORDER BY TABLE_NAME
    );
    $sth->execute($db_name);

    # 使用 ul()（无序列表）和
    # li()（列表项）函数构建无序列表。每个项目都是
    # 一个超链接，该链接重新调用脚本以显示特定表。
    my @item;
    while (my $tbl_name = $sth->fetchrow_array())
    {
        my $url = sprintf("%s?tbl_name=%s", url(), escape($tbl_name));
        my $link = a ( {-href => $url}, escapeHTML($tbl_name)) ;
        push(@item, li($link));
    }
    print ul(@item);
}
```

`li()` 函数在每个列表项周围添加 `<li>` 和 `</li>` 标签，而 `ul()` 在项目集合周围添加 `<ul>` 和 `</ul>` 标签。列表中的每个表名都以超链接的形式呈现，该超链接重新调用脚本以显示命名表的内容。由 `display_table_names()` 生成的列表看起来像这样：

```html
<ul>
<li><a href="/cgi-bin/db_browse.pl?tbl_name=absence">absence</a></li>
<li><a href="/cgi-bin/db_browse.pl?tbl_name=grade_event">grade_event</a></li>
<li><a href="/cgi-bin/db_browse.pl?tbl_name=member">member</a></li>
...
</ul>
```

如果在调用 `db_browse.pl` 时 `tbl_name` 参数有值，脚本会将该值传递给 `display_table_contents()`，如果给定了排序列，还会传递要按哪列对结果进行排序的名称：

```perl
sub display_table_contents
{
    my ($dbh, $db_name, $tbl_name, $sort_col) = @_;
    my $sort_clause = "";
    my @rows;
    my @cells;

    # 如果指定了排序列，则用它对结果进行排序
    if (defined($sort_col))
    {
        $sort_clause = " ORDER BY " . $dbh->quote_identifier($sort_col);
    }

    # 提供一个链接，让用户返回表列表页面
    print p(a ( {-href => url()}, "显示表列表"));

    print p (strong ("$tbl_name 表的内容："));

    my $sth = $dbh->prepare (
        "SELECT * FROM "
        . $dbh->quote_identifier ($db_name, $tbl_name)
        . "$sort_clause LIMIT 200"
    );
    $sth->execute ();

    # 使用数据库表中的列名作为
    # HTML 表中的标题。让每个名称成为一个超链接，
    # 该超链接会导致脚本被重新调用以重新显示该表，
    # 并按命名列排序。

    foreach my $col_name (@{$sth->{NAME}})
    {
        my $url = sprintf ("%s?tbl_name=%s;sort_col=%s",
            url (),
            escape ($tbl_name),
            escape ($col_name));
        my $link = a ({-href => $url}, escapeHTML ($col_name));
        push (@cells, th ($link));
    }
    push (@rows, tr (@cells));

    # 显示表行
    while (my @ary = $sth->fetchrow_array ())
    {
        @cells = ();
        foreach my $val (@ary)
        {
            # 如果非空则显示值，否则显示不换行空格
            if (defined ($val) && $val ne "")
            {
                $val = escapeHTML ($val);
            }
            else
            {
                $val = "&nbsp;";
            }
            push (@cells, td ($val));
        }
        push (@rows, tr (@cells));
    }

    # 显示带有边框的表
    print table (|-border => "1", @rows);
}
```

查询还包括一个 `LIMIT 200` 子句，作为防止脚本向浏览器发送大量数据的简单预防措施。（对于示例数据库中的表，这种情况不太可能发生，但如果你修改脚本来显示其他数据库中表的内容，则可能会发生这种情况。）`display_table_contents()` 将表中的行作为 HTML 表显示，使用 `th()` 和 `td()` 函数生成表头和单元数据单元格，使用 `tr()` 将单元格组合成行，并使用 `table()` 生成包围这些行的 `<table>` 标签。

HTML 表将列标题显示为重新显示数据库表的超链接。这些链接包含一个 `sort_col` 参数，明确指定用于排序的列。例如，对于显示 `grade_event` 表内容的页面，列标题链接看起来像这样：

```html
<a href="/cgi-bin/db_browse.pl?tbl_name=grade_event&sort_col=date">
   date</a>
<a href="/cgi-bin/db_browse.pl?tbl_name=grade_event&sort_col=category">
   category</a>
<a href="/cgi-bin/db_browse.pl?tbl_name=grade_event&sort_col=event_id">
   event_id</a>
```

`display_table_contents()` 使用一个小技巧将空值转换为不换行空格（`&nbsp;`）。在带边框的表中，某些浏览器无法正确显示空单元格的边框；在单元格中放入不换行空格可以解决这个问题。

如果你想编写更通用的脚本，你可以修改 `db_browse.pl` 以浏览多个数据库。例如，你可以让脚本首先显示服务器上的数据库列表，而不是特定数据库内的表列表。然后你可以选择一个数据库来获取其表列表，并从这里开始。

## 8.4.5 成绩管理项目成绩浏览器

我们下一个 Web 脚本 `score_browse.pl` 旨在显示为成绩管理项目记录的成绩。严格来说，我们应该先有一种输入成绩的方法，然后再创建一种检索成绩的方法，但我将成绩输入脚本留到下一章。在此期间，我们在数据库早期部分已经拥有几组成绩。我们可以使用脚本来显示这些成绩，即使没有便捷的成绩输入方法。脚本显示任何测试或测验的成绩有序列表，这对于确定评分曲线和分配字母等级很有用。

`score_browse.pl` 与 `db_browse.pl` 有一些相似之处（两者都作为信息浏览器），但旨在用于更具体的目的，即查看给定测验或测试的成绩。初始页面显示可选成绩事件的列表，并允许用户选择其中任何一个以查看与该事件关联的成绩。给定事件的成绩按分数排序，最高分优先，因此你可以使用结果来确定评分曲线。

`score_browse.pl` 脚本只需检查一个参数 `event_id`，以查看是否指定了成绩事件。如果没有，`score_browse.pl` 显示 `grade_event` 表的行，以便用户可以选择其中一个。否则，它显示与所选事件关联的成绩：

```perl
# ... 设置数据库连接（未显示）...

# 输出页面的初始部分
my $title = "成绩管理项目 -- 成绩浏览器";
print header ();
print start_html (-title => $title, -bgcolor => "white");
print h1 ($title);

# 告知我们要显示哪个成绩事件成绩的参数
my $event_id = param ("event_id");

# 如果 $event_id 没有值，显示事件列表。
# 否则显示给定事件的成绩。
if (!defined ($event_id))
{
    display_events ($dbh);
}
else
{
    display_scores ($dbh, $event_id);
}

print end_html ();
```

`display_events()` 函数从 `grade_event` 表中提取信息并将其显示为表，使用查询中的列名作为表列标题。在每一行中，`event_id` 值显示为可选择的超链接，以触发检索该事件成绩的查询。每个事件的 URL 仅仅是指向 `score_browse.pl` 的路径，附带一个指定事件编号的参数：

```
/cgi-bin/score_browse.pl?event_id=n
```

`display_events()` 看起来像这样：

```perl
sub display_events
{
    my $dbh = shift;
    my @rows;
    my @cells;

    print p ("点击其编号选择一个事件：");
    ...
```

