
# 构建网站

## 图 32.24：联系表单

![](img/bc3027047bbbcc0b55a71a4b67c60968_800_0.png)

此页面的特殊之处在于它包含一个表单，以及一个用于处理表单数据的`CGI`程序的引用。在此例中，你使用的程序被称为`formmail`，它是一个用`Perl`编写的免费提供的`CGI`脚本，用于获取表单内容并将其发送到预定义的邮件地址。事实上，表单中的联系信息可以通过电子邮件发送到书店的主邮箱地址。

`formmail`由Matthew M. Wright编写，可以在`http://www.worldwidemart.com/scripts/formmail.html`获得。尽管本章没有讨论`Perl`或`CGI`编程，但此处展示了其源代码，以便你看到如何用较少的力气就能创建基础的`CGI`程序：

```perl
# 定义星期和月份的数组。
@days = ('Sunday', 'Monday', 'Tuesday', 'Wednesday',
    'Thursday', 'Friday', 'Saturday');
@months = ('January', 'February', 'March', 'April', 'May', 'June', 'July',
    'August', 'September', 'October', 'November', 'December');
```

```perl
# 获取当前时间并格式化小时、分钟和秒。
# 在年份上加上 1900 以得到完整的 4 位年份。
($sec,$min,$hour,$day,$mon,$wday) = (localtime($time))[0,1,2,3,4,5];
$time = sprintf("%02d:%02d:%02d",$hour,$min,$sec);
$year += 1900;

# 格式化日期。
$date = "$days[$wday] $months[$mon] $year at $time";

sub sub_parse_form {

# 定义配置数组。
%Config = ('recipient', 'subject', 'email', 'realname',
    'redirect', 'bgcolor', 'background', 'link_color',
    'text_color', 'title', 'sort', 'print_config',
    'required', 'env_report', 'return_link_url',
    'missing_fields','');

# 确定表单的 REQUEST_METHOD (GET 或 POST)并将表单
# 字段拆分为键值对。
if ($_ENV['REQUEST_METHOD'] == 'GET') {
    # 拆分键-值对
    @pairs = split(/&/, $_ENV['HTTP_REFERER']);
}
```
