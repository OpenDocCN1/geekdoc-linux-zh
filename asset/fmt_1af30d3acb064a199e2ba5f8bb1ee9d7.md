
# 对于每个键值对
```perl
foreach $pair (@pairs) {
```

# 将键值对拆分成单独变量。
```perl
local($name, $value) = split(/=/, $pair);
```

# 解码名称和值变量中的表单编码。
```perl
$name = ~tr+/ /;
$name = ~s/([a-fa-f0-9])([a-fa-f0-9])/pack("C", $1)/eg;

$value = ~tr+/ /;
$value = ~s/([a-fa-f0-9])([a-fa-f0-9])/pack("C", $1)/eg;
```

# 如果他们尝试包含服务器端包含（SSI），将其删除，以
# 防止在返回 HTML 时产生安全风险。这是另一个
# 被修复的安全漏洞。
```perl
$value = ~s|<(.|\n)->//g;
```

# 如果字段在 %Config 数组中已指定，则
# defined($Config($name)) 将返回 1，我们应该将
#此值与相应的配置变量关联。如果这
# 不是配置字段，则将其放入关联
# 数组 %Form，如果已存在值，则在值后追加一个空格 ' '。
# 我们还会在 @Field_Order 数组中保存表单字段的顺序，
#以便通用排序可以使用该顺序。
```perl
if ($Config($name)) {
    $Config($name) = $value;
} else {
    if (exists($Form($name))) {
        $Form($name) = "$Form($name), $value";
    }
} elsif (exists($Form($value))) {
    push(@Field_Order, $name);
    $Form($name) = $value;
}
```

# 构建一个网站

```perl
# 下六行从 % 配置

# 变量中移除多余的空格或换行，这可能是由于你的编辑器

# 在达到特定长度后自动换行，或者你在字段名称或

# 环境变量之间使用了空格导致的。

$Config('required') = s/(\s+|\n)?(\s+|\n)?//g;

$Config('required') = s/(\s+)?n(\s+)?//g;

$Config('env_report') = s/(\s+|\n)?(\s+|\n)?//g;

$Config('env_report') = s/(\s+)?n(\s+)?//g;

$Config('print_config') = s/(\s+|\n)?(\s+|\n)?//g;

$Config('print_config') = s/(\s+)?n(\s+)?//g;

# 将配置变量拆分成单独的字段名。%
@Required = split(/,/,Config('required'));

@Env_Report = split(/,/,Config('env_report'));

@Print_Config = split(/,/,Config('print_config'));

}
```

```perl
sub check_required (
```

# 本地化此子程序中使用的变量。%
```perl
local($require, @error);

if (!$Config('recipient')) {

    if (defined($Form)) { error('bad_referer'); }

    else { error('no_recipient'); }

}
```

# 对于表单中定义的每个必填字段：%
```perl
foreach $require (@Required) {
```

# 如果必填字段是邮箱字段，则检查邮箱语法
# 以确保它通过有效语法检查。
```perl
if ($require == 'email' && &check_email($Config($require))) {

    push(@error, $require);

}
```

# 否则，如果必填字段是配置字段且
# 没有值或被空格填充，则发送错误。
```perl
elsif (defined($Config($require))) {

    if (!$Config($require)) {

        push(@error, $require);

    }

}
```

# 如果字段没有值或被空格填充，则将其标记为错误。
```perl
elsif ($value =~ /^\s*$/) {

    push(@error, $require);

}
```

# 如果存在错误，则显示错误信息。
```perl
if (@error) {

    print "<h1>Error</h1>\n";

    print "Please fill all required fields：\n";

    print "<ul>\n";

    foreach $err (@error) {

        print "<li>$err</li>\n";

    }

    print "</ul>\n";

    print "<a href='Go Back</a>";

}
```

# 如果设置了重定向，输出重定向头。
```perl
if ($Config('redirect')) {

    print "Location: $Config('redirect')\n";

}
```

# 否则，开始打印页面。
```perl
else {
```

# 输出 HTTP 头
```perl
print "Content-type: text/html\n\n";
```

# 输出 <head> 标签
```perl
print "<head>\n";
```

# 打印自定义标题。
```perl
if ($Config('title')) { 

    print "<h1>$Config('title')</h1>\n";

} else { 

    print "<h1>Thank You</h1>\n";

}
```

```perl
print "</head>\n";
```

- 输出 <body> 标签
```perl
print "<body>\n";
```

# 输出 <center> 标签
```perl
print "<center>\n";
```

# 打印提交的信息。
```perl
if (keys %Form) {

    foreach $field (keys %Form) {

        # 如果字段有值，则打印。
        if ($Form($field)) {

            print "<b>$field:</b> $Form($field)<br>\n";

        }
    }

} else {

    print "No data submitted.\n";

}
```

```perl
print "</center>\n";
```

# 检查是否有返回链接，如果存在则输出。
```perl
if ($Config('return_link_url') && $Config('return_link_title')) {

    print "<ul>\n";

    print "<li><a href='$Config('return_link_url')$Config('return_link_title')</a></a>\n";

    print "</ul>\n";

}
```

# 打印页脚。
```perl
print "<<(END HTML FOOTER)>>\n";

<hr size=1 width=75%">

<font size=-1>

<a href="http://www.widewirect.com/scripts/formmail.shtml">FormMail V1.6 &copy; 1995 -1997 Matt Wright<br>nA Free Product of <a href="http://www.widewirect.com/scripts/">Matt's Archive, Inc.</a></font></center>

</body>

</html>

}
```

# 如果指定了排序顺序，则根据该顺序对字段进行排序。
```perl
elsif ($Config['sort'] = "/order:.**/") {
```

# 多余的换行符和空格，移除 order:
# 指令并将排序字段分割为数组。
```perl
$Config['sort'] = $s/(\s+\n)?(\s+)?//g;
$Config['sort'] = $s/(\s+)?(\s+)?//g;
$Config['sort'] = $s/order//;
$sorted_fields = split(\//, $Config['sort']);
```

# 对于每个排序字段，如果它有值或开启了打印空
# 选项，则打印表单字段和值。
```perl
foreach ($sorted_fields) {
    if ($Config['print_blank_fields'] || $Form[$sorted_field]) ||
    $Form[$sorted_field] eq '0') {
        print MAIL $sorted_field: $Form[$sorted_field]\n\n";
    }
}
```

否则，默认按照字段发送时的顺序。
```perl
else {
```

# 对于每个表单字段，如果它有值或开启了打印空
# 字段选项，则打印表单字段和值。
```perl
foreach ($field (@Field_Order) {
    if ($Config['print_blank_fields'] || $Form[$field]) ||
    $Form[$field] eq '0') {
        print MAIL $field: $Form[$field]\n\n";
    }
}
```

```perl
print MAIL "-" x 75 . "\n\n";
```

# 将任何指定的环境变量发送给接收者。
```perl
foreach $env_report (@Env_Report) {
    if ($ENV[$env_report]) {
        print MAIL "$env_report: $ENV[$env_report]\n\n";
    }
}
```

# 构建网站 797
```perl
close (MAIL);

)
```

```perl
sub check_email (
  # 使用输入内容初始化本地电子邮件变量。
  $email = $\$[0];
```

# 如果电子邮件地址包含：
```perl
if ($email =~ /\(\.\*)|(\\.)|(\\.)|([^\/])/ //
```

# 电子邮件地址包含无效语法。或者，如果
  # 语法不匹配正则表达式中的点，
  # 则未通过基础语法验证。
```perl
$email1 =~ /\+\*|[@\]?[a-zA-Z0-9\-]+\.([a-zA-Z]{2,3})([0-9]{1,3})\/\/);
```

# 基础语法要求：在 @ 符号之前有一个或多个字符，
# 随后是可选的 '[\，任意数量的字母、数字、
# 连字符或点（有效的域名/IP 字符），以点结尾，
# 然后后面是 2 或 3 个字母（域名后缀）或 1 到 3 个数字
#（用于 IP 地址）。也允许右括号结尾，因为像
# user@[255.255.255] 这样的电子邮件地址是合法的语法。
```perl
  # 返回假值，因为电子邮件地址未通过有效性检查
  return 0;
}

else (
```

# 返回真值，电子邮件验证通过。
```perl
  return 1;
}
```

```perl
sub body_attributes (
  # 检查背景颜色
  if ($Config('bgcolor')) { print "$bgcolor='\$Config('bgcolor')}"; }
```

### 检查背景图像
```perl
if ($Config{'background'}) { print "background=\$Config['background']\n"; }
```

### 检查链接颜色
```perl
if ($Config{'link_color'}) { print "link=\$Config['link_color']\n"; }
```

### 检查访问过的链接颜色
```perl
if ($Config{'vlink_color'}) { print "vlink=\$Config['vlink_color']\n"; }
```

### 检查激活链接颜色
```perl
if ($Config{'alink_color'}) { print "alink=\$Config['alink_color']\n"; }
```

### 检查正文颜色
```perl
if ($Config{'text_color'}) { print "text=\$Config['text_color']\n"; }
```

```perl
sub error {

# 局部化变量并赋值输入。
local($error,$error_fields) = @(\n);
local($host,$missing_field,$missing_field_list);
```

```perl
if ($error eq 'bad_referrer') {

if ($ENV{'HTTP_REFERER'} =~ m|^(https?([\w.]+))|(i)) {

$host = $1;

print <<<END ERROR HTML>";
```

```perl
Content-type: text/html
```

```html
<html>
<head>
<title>Bad Referrer - Access Denied</title>
</head>
<body bgcolor=#FFFFFF text=#00000>
<center>
<table border=0 width=600=#=#B9CC>>
<><><th size2>>Bad Refer - - Denied</</thtr>
</>
<< border border00 width6600=#=#CFCF>
<<<td> form单 <aaa="wwwwww........
/ $
('HTTP
ER') 不允许访问此 cgi 脚本。</p>
>如果你正尝试使用 FormMail 运行此表单，需要将以下内容
到 Referers 中，这些内容在 README 文件中有
有详细的说明。</p>
>将 'host' 添加到你的 <b> 数组中。
<center><font size=1>
<a href="http://www.worldwidart.com/com/scripts/formmail.shtml">FormMail v1.6 &copy; 1995 - 1997 Matt Wright</a>
A Free Product of <a href="http://www.worldwidart.com/com/scripts/">Matt's Script Archive, Inc.</a>
</font></center>
</td></tr>
</table>
</center>
</body>
</html>
```

```perl
(END ERROR HTML)
else {
print "(END ERROR HTML)";
Content-type: text/html
```

```html
<html>
<head>
<titletitle>FormMail v1.6</title>
</head>
<body bgcolor="#FFFFFF" text="#000000">
<center>
<table border="0" width="600" bgcolor="#F9C9C">
<tr><th size="2">FormMail</th></tr>
</table>
<table border="0" width="600" bgcolor="#CFCFC">
<tr><<td>>你提交的表单的请求方法（Request Method）不匹配 GET 或 POST. 请检查表单，并确保方法声明为大写并匹配 GET 或 POST.</td></tr>
```

<center><font size="1">
<a href="http://www.worldwidart.com/scripts/formmail.shtml">FormMail v1.6 &copy; 1995 - 1997 Matt Wright</a>
A Free Product of <a href="http://www.worldwidart.com/scripts/">Matt's Script Archive, Inc.</a>
</font></center>
</td></tr>
</table>
</center>
</body>
</html>
```

```perl
(END ERROR HTML)
```

```perl
}
elsif ($error == 'request_method') {
    print <<"END ERROR HTML>";
Content-type: text/html
```
