
```perl
$password = "iamnotanumber";

# 定义结束

# 这是主分支。第一次通过时
# 向用户显示表单，当用户提交
# 表单时我们处理输入

if ($q->param('field') eq "") (&printform) else (&results()) {

sub printform {

print $q->header;

print $q->start_html(title=>'Network Machines Database',
-BGCOLOR=>'black',
-TEXT=>'white');

print "<CENTER>Network Machines Database</CENTER><HR>";

print $q->start_form;

print "Find all machines where :" -> field,

print $q->popup_menu(name => ["*alias", "ip",
-"canonical", "ostype"],
-defaultdefault => "alias");

print $q->popup_menu(name => searchtype,
-values => ["*is", "contains"],
-defaultdefault => "is");

print $q->textfield(name => text,
-size => 16), "<BR>

print $q->submit;

print $q->endform;

print $q->end_html;

}
```

## 第16 章：结构化查询语言数据库服务 447

```perl
sub results [

$field = $q->param('field');
$searchtype = $q->param('searchtype');
$text = $q->param('text');

@table=();

print $q->start_html(-title='Database Results',
-BGCOLOR=>'black',
-TEXT=>'white');

# 告诉脚本我们将使用
# MySQL 数据库
# $drh = DBI->install_driver('mysql');
# 建立数据库连接
$dbh = $drh->connect($dbh, $user, $password);

# 检查是否连接的简单检查
if (!$dbh) {
    print "无法连接: DBI::errstr<br>";
    print $q->end_html();
}

# 构建并执行 SQL 语句
if ($searchtype eq "contains") {
    $SQLStatement = "select alias, ip, canonical, otype from $table
    where $field like \%$text\%";
} else {
    $SQLStatement = "select alias, ip, canonical, otype from $table
    where $field = \"$text\";
}

my $sth = $dbh->prepare($SQLStatement);
my $howany = $sth->execute();

# 如果没有找到
# 匹配项，则打印错误消息
if ($howany == "0") {
    print $q->h3("<font color=red>在数据库中未匹配到文本</font>");
    die;
}

print "数据库中找到 $howany 条匹配<br>";
```

## 448 第四部分：设置文件共享和数据库服务器

```perl
push(@table,$q->th(["Alias", "IP", "Canonical", "OStype"]));

# 遍历所有匹配项并将它们
# 存储在 @table 中
for (my $i = 0; $i < $Showany; $i++) {
    my($SQLAlias, $SQLIP, $SQLcanonical, $SQLostype) = 
        $sth->fetch_array;
    push(@table,$q->td([$SQLAlias, $SQLIP, $SQLcanonical, $SQLostype]));
}

# 打印我们从 SQL
# 数据库获取的数据表格
print $q->table((-border -> 1, -align -> center),$q->Tr(\@table));
print $q->end_html;
```

图 16-2 显示了 Web 浏览器中的 HTML 表单屏幕。

![](img/1d90939eac39ca76d12e353542e54751_477_0.png)

图 16-2：选择屏幕

当带有带有标准的 HTML 表单时，CGI 脚本会再次运行并从 SQL 数据库检索请求的数据。然后，CGI 脚本将数据格式化为 HTML 表格并发送回 Web 浏览器进行显示。图 16-3 显示了结果页的示例。

![](img/1d90939eac39ca76d12e353542e54751_478_0.png)

图 16-3：输出屏幕

你还可以让 CGI 脚本执行其他功能，例如从数据库中插入、更新和删除信息。你可以修改之前讨论的 `insert.pl` 脚本以作为 CGI 脚本。列表 16-6 显示了修改后的脚本。该脚本为用户提供了一个 HTML 表单以输入新数据；当提交新数据时，脚本会显示状态消息，告诉用户数据已添加到数据库中。

该脚本可以在第二个光光盘的以下位置找到：`/cdrom/extras/insert.cgi`。

## 列表 16-6：insert.cgi 文件

```perl
# 定义 - 如果你使用不同的数据库，需要更改此处
$db = "inventory";
$stable = "machines";
$user = "root";
$password = "iamnotanumber";

# 定义结束
```
