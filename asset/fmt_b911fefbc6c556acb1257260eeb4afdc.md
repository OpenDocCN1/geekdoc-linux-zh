
# Format the date.

```perl
$date = "$days[$wday], $months[$mon] $mday, $year at $time";
```

}

```perl
sub parse_form {
    # Define the configuration associative array.
    $Config = (
    'recipient', 'subject',
    'email', 'realname',
    'redirect', 'bgcolor',
    'background', 'link_color',
    'vlink_color', 'text_color',
    'alink_color', 'title',
    'sort', 'print_config',
    'required', 'env_report',
    'return_link_title', 'return_link_url',
    'print_blank_fields', 'missing_fields_redirect');
    # Determine the form's REQUEST_METHOD (GET or POST) and split the form
    # fields up into their name-value pairs. If the REQUEST_METHOD was
    # not GET or POST, send an error.
    if ($_SERVER['REQUEST_METHOD'] eq 'GET') {
        # Split the name-value pairs
        @pairs = split(/&/, $_SERVER['QUERY_STRING']);
    } elsif ($_SERVER['REQUEST_METHOD'] == 'POST') {
        # Get the input
        read(STDIN, $buffer);
        # Split the name-value pairs
        @pairs = split(/&/, $buffer);
    } else {
        &error('method');
    }
    # For each name-value pair
    foreach (@pairs) {
        # Split the name-value pair
        ($name,$value) = split(/=/, $pair);
        # Store the value in the configuration array
        $Config{$name} = $value;
    }
}
```

## 构建网站

## 关闭 Body 标签

```perl
print "\n <center>\n";
```

# 打印自定义标题或通用标题。

```perl
if ($Config['title']) { 
    print "<h1>$Config['title']</h1>\n" 
} else { 
    print "<h1>感谢您填写表单</h1>\n" 
}
print "以下是您提交给 $Config['recipient'] 的内容："
print "<p><hr size=1 width=75></p>\n";
```

- 如果指定，则按字母顺序排序：

```perl
if ($Config['sort'] eq 'alphabetic') {
    foreach $field (sort keys %Form) {
        # 如果字段有值，或者开启了打印空白字段
        # 选项，则打印表单字段和值。
        if ($Config('print_blank_fields') || $Form($field)) {
            print "<b>$field:</b> $Form($field)<p>\n";
        }
    }
}
```

- 如果指定了排序顺序，则根据该顺序对表单字段进行排序。

```perl
elsif ($Config('sort') =~ "/order:,*/") {
    # 将临时变量 $sort_order 设置为排序顺序，
    # 移除多余的换行和空格，移除 order: 指令
    #并将字段拆分为数组。
    $sort_order = $Config('sort');
    $sort_order =~ s/s(\s+)?\s(\n+)?//g;
    $sort_order =~ s/s(\s+)?\n(\s+)?//;
    $sorted_fields = split(/,/, $sort_order);
    # 对于每个排序后的字段，如果它有值或开启了打印空白
    # 字段选项，则打印表单字段和值。
    foreach $sorted_field (@sorted_fields) {
        if ($Config('print_blank_fields') || $Form($sorted_field)) {
            print "<b>$sorted_field:</b> $Form($sorted_field)<p>\n";
        }
    }
}
```

# 否则，默认按照字段发送的顺序。

```perl
else {
    # 对于每个表单字段，如果它有值或开启了打印空白
    # 字段选项，则打印表单字段和值。
    foreach ($field as @Field_Order) {
        if ($Config('print_blank_fields') || $Form($field)) {
            print "<b>$field</b>" $Form($field)."p>\n";
        }
    }
}
print "<p><hr size=1 width=75></p>\n";
# 检查是否存在返回链接，如果找到则打印。
if ($Config('return_link_url') && $Config('return_link_title')) {
    print "<ul>\n";
    print "<li><a href=\$Config('return_link_url')\">\$Config('return_link_title')</a></li>\n";
    print "</ul>\n";
}
# 打印页面页脚。
print "<<(END HTML FOOTER)>>";
```

```html
<hr size=1 width=75><p>
<center><font size=-1><a href="http://www.wididemidart.com/scripts/formmail.html">FormMail</a>a>
V1.6 & 1995 -1997 Matt Wright<br>
A Free Product of <a href="http://www.wididemidart.com/scripts/">Matt's Script Archive, Inc.</a></font></center>
</body
</html
```

```perl
sub send_mail [] {
    # 此子程序使用的局部变量。
    local($print_config,$key,$sort_order,$sorted_field,$env_report);
    # 开启邮件程序
    open(MAIL,"|mailprog -t");
    print MAIL "To: ${Config('recipient')}\n";
    print MAIL "From: ${Config('email')} (${Config('realname')})\n";
    # 检查邮件主题
    if ($Config('subject')) { 
        print MAIL "Subject: ${Config('subject')}\n\n" 
    } else { 
        print MAIL "Subject: WWW 表单提交\n\n" 
    }
    print MAIL "以下是您的反馈表单结果。提交时间为\n";
    print MAIL "${Config('realname')} (${Config('email')} 日期\n";
    print MAIL "* x 75, \n\n";
    if (@Print_Config) {
        foreach $print_config (@Print_Config) {
            if ($Config($print_config)) {
                print MAIL "$print_config: ${Config($print_config)}\n";
            }
        }
    }
    # 如果指定，按字母顺序排序
    if ($Config('sort') eq 'alphabetical') {
        foreach $field (sort keys %Form) {
            # 如果字段有值或开启了打印空白字段和值。
            # 选项，则打印表单字段和值。
            if ($Config('print_blank_fields') || $Form($field)) {
                # 注意：OCR 中的逻辑在 '0' 处略显混乱，但保留原始信息
            }
        }
    }
    # 如果指定了排序顺序，根据该顺序对表单字段进行排序。
    elif ($Config('sort') =~ "/order:.**/") {
        # 移除多余的换行和空格，移除 order: 
        # 指令并将排序字段拆分为数组。
        $Config('sort') = s/(\s+\n)?(\s+\n)?//g;
        $Config('sort') = s/(\s+)?\n(\s+)?//g;
        $Config('sort') = s/order://;
        $sorted_fields = split(/,/, $Config('sort'));
        # 对于每个排序后的字段，如果它有值或开启了打印空白
        # 字段选项，则打印表单字段和值。
        foreach $sorted_field($sorted_fields) {
            if ($Config('print_blank_fields') || $Form($sorted_field)) {
                if ($Form($sorted_field) eq '0') {
                    print MAIL "$sorted_field: $Form($sorted_field)\n";
                }
            }
        }
    } 
    # 否则，默认按照字段发送的顺序。
    # 对于每个表单字段，如果它有值或开启了打印空白
    # 字段选项，则打印表单字段和值。
    foreach $field($Field_Order) {
        if ($Config('print_blank_fields') || $Form($field)) {
            # ...来自  的逻辑
        }
    }
    # ... 剩余逻辑
}
```

```perl
sub error {
    # 局部变量并赋值输入。
    local($error,@error_fields) = @_;
    if ($error == 'bad_referrer') {
        if ($ENV['HTTP_REFERER'] =~ m|https?[\w\.]+)|i) {
            $host = $ENV['HTTP_REFERER'];
        }
    }
    # ... 错误处理剩余
}
```

# ... 其他函数 ...

```perl
sub body_attributes {
    # 检查背景颜色
    if ($Config('bgcolor')) { print " bgcolor=\$Config('bgcolor')" }
    # 检查背景图片
    if ($Config('background')) { print "-background=\$Config('background')" }
    # 检查链接颜色
    if ($Config('link_color')) { print " link=\$Config('link_color')" }
    # 检查已链接颜色
    if ($Config('vlink_color')) { print " vlink=\$Config('vlink_color')" }
    # 检查激活链接颜色
    if ($Config('alink_color')) { print " alink=\$Config('alink_color')" }
    # 检查文本颜色
    if ($Config('text_color')) { print " text=\$Config('text_color')" }
}
```

```html
</body>
</html>
(END ERROR HTML)
)
else {
  print <<"(END ERROR HTML)";
Content-type: text/html
```

```perl
elsif ($error eq 'request_method') {
  print <<"(END ERROR HTML)";
Content-type: text/html
```

```html
<html>
<head>
<title>错误：请求方法</title>
</head>
<body bgcolor=#FFFFFF text=#000000
<center>
<table border=0 width=600 bgcolor=#9C9C9C
```

# 626 页 第 27 章 构建你自己的 Web 服务器

```html
<tr><th><font size=+2>错误：请求方法</font></th></tr>
</table>
<table border=0 width=600 bgcolor=#FCFCCF>
<tr><<td>>提交的表单请求方法与 &lt;GET&gt; 或 &lt;POST&gt; 不匹配。请检查表单，确保
&lt;method&gt; 语句为大写并匹配 &lt;GET&gt; 或
&lt;POST&gt;。</td></tr></table>
```

<center><font size=-1>
<a href="http://www.widewidmart.com/scripts/formmail.shtml">FormMail/V1.6, 1995 - 1997 Matt Wright<br>
<a href="http://www.widewidmart.com/scripts/">Matt's Script Archive, Inc.</a> 的免费</a>
</font></center>
<table>
</center>
<body>
<html>
(END ERROR HTML)
}
```

```perl
elsif ($error eq 'no_recipient') {
    print "(END ERROR HTML)";
Content-type: text/html
<html>
<head>
<title>错误：无收件者</title>
</head>
<body bgcolor=#FFFFFF text=#000000>
<center>
<table border=0 width=600 bgcolor=#9C9C9C>
<tr><th><font size=+2>错误：无收件者</font></th></tr>
</table>
<table border=0 width=600 bgcolor=#FCFCCF>
<tr><<td>发送到 FormMail 的数据中未指定收件者。请确保您已经在 'recipient' 字段中填写了电子邮件地址。关于如何填写收件者表单字段的更多信息可以在 README 文件中找到。<hr size=1></td></tr></tr>
```

# 构建网站

```html
<center><font size=-1>
<a href="http://www.widewidart.com/scripts/formmail.shtml">FormMail/V1.6 &copy; 1995 - 1997 Matt Wright<br>
<a href="http://www.widewidart.com/scripts/">Matt's Script Archive, Inc.</a> 的免费产品
</center>
</td>
</tr>
</table>
</center>
<body>
</html>
(END ERROR HTML)
```

```perl
elsif ($error eq 'missing_fields') {
```
