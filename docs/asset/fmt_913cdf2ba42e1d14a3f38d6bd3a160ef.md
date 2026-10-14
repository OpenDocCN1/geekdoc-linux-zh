
```perl
#!/usr/local/bin/perl
#
# fruit.cgi
#
# 应用将为 Cyber Corner Market 生成 HTML
# 蔬菜部分。
#
# 表单中将包含包含 user_name 的隐藏字段
# 以及包含文件名的隐藏字段。
#
BEGIN {
    push(@INC,'/opt2/web/guide/unix/book-bin');
}

use CGI;

$query = new CGI;
# 如果存在现有参数，获取 user_name 的值
if ($query->param()) {
    $user_name = $query->param('user_name');
    $file_name = $query->param('file_name');
}

# 打印头部和标题信息
print $query->header;

print $query->start_html('Cyber Corner Market-Veggies');

print $query->h1('Cyber Corner Market');
print<<end_of_page;
<p>
<hr>
<p>
<FORM name="fruit" ACTION="http://unix.yasd.com/book-bin/process_order.cgi">
<TABLE width=600 cellpadding=5
<STRONG>
<tr><td>Quantity</td><td>Item</td><td>Total</td></tr></strong>
<p>
<INPUT TYPE="hidden" name="user_name" value="$user_name">
<INPUT TYPE="hidden" name="file_name" value="$file_name">
<tr><<td>
<INPUT TYPE="text" name="apple_qty" size=5
OnChange="document.fruit.apple_total.value=parseFloat(this.value) * .80">
</td><td>
Apples - .80 per lb
</td></tr><tr><td>
<INPUT TYPE="text" name="apple_total" size=10>
</td></tr><td>

<INPUT TYPE="text" name="grapes_qty" size=5
OnChange="document.fruit.grapes_total.value=parseFloat(this.value) * 1.50">
</td><td>
Seedless Green Grapes - 1.50 per lb
</td></tr><td>
<INPUT TYPE="text" name="grapes_total" size=10>
</td></tr>
<<tr><td>
<INPUT TYPE="text" name="pears_qty" size=5
OnChange="document.fruit.pears_total.value=parseFloat(this.value) * 1.80">
</td><td>
Pears - 1.80 per lb
</td></tr><td>
<INPUT TYPE="text" name="pears_total" size=10>
</td></tr>
<<tr><td>
<INPUT TYPE="text" name="peaches_qty" size=5
OnChange="document.fruit.peaches_total.value=parseFloat(this.value) * 1.80">
</td><td>
Peaches - 1.80 per lb
</td></tr><td>
<INPUT TYPE="text" name="peaches_total" size=10>
</td></tr>
```

[第 347 页]

```html
<table>
  <!-- ... 之前的行此处未显示 ... -->
  <tr>
    <td>桃子 - 每磅 1.80</td>
    <td><input type="text" name="peaches_total" size=10></td>
  </tr>
  <tr>
    <td>
      <input type="text" name="pineapple_qty" size=5
      change="document.fruit.pineapple_total.value=parseFloat(this.value) * 2.0">
    </td>
    <td>菠萝 - 每个个 2.00</td>
    <td><input type="text" name="pineapple_total" size=10></td>
  </tr>
  <tr>
    <td></td>
    <td><input type="submit" value="发送订单"></td>
  </tr>
</table>
```

<p>

<hr>

end_of_page

print $query->end_html;

exit(0);</p>

与蔬菜表单一样，点击“发送订单”（Send Order）按钮会调用 `process_order.cgi` 程序，该程序会将订单追加到文件中。此时，读者可以选择完成文件的处理，这将弹出一个列出其订单的文档（见图 7.15）。

图 7.15：Cyber Market 表单的最终文档列出了所订购的项目及其总额。

生成此访问表单的程序包含了包含订单信息并显示数值的文件。该程序使用 Perl 的 `unlink` 函数删除指向该文件的链接。由于该文件只有一个链接，因此该文件被删除。

# 列表 7.20 完成订单处理并删除订单文件的程序 (finish.cgi)

```perl
#!/usr/local/bin/perl
#
# finish.cgi
#
# Corner Cyber Market 的最终订单
#
# 打开订单文件并将每个总额加载到
# 数组中并打印每一个
#
# 完成后，关闭并删除文件。
#
BEGIN {
    push(@INC, '/opt2/web/guide/unix/book-bin');
}
use CGI;
$query = new CGI;
#
# 如果存在参数，获取 user_name 的值
if ($query->param()) {
    $user_name = $query->param('user_name');
    $file_name = $query->param('file_name');
}
print $query->header();
print $query->start_html('确认最终订单');
print $query->h1("正在完成 $user_name . 的订单");
```

# 打开订单文件并打印总额

print "<p><hr> 以下是每个项目和总价值：<p>";

```perl
open(USER_FILE, "<", $file_name) || die "无法打开订单文件.";
print "<CENTER><TABLE width=200>";

foreach $line(<USER_FILE>) {
    @order_line = split(/\/,,$line);

    print "<tr>";

    foreach $elem (@order_line) {
        ($object,$value) = split(/\/,,$elem);

        if ($value <= 0) {
            last;
        }

        print "<td>" . $object . "</td><td>";
        printf("%7.2f", $value);

        print "</td></tr>";
    }
}

print "</TABLE></CENTER>";

close(USER_FILE);

link($file_name);

print "<p><hr><p><h3>感谢您的订单</h3>";

print $query->end_html;

exit(0);
```

本节描述的程序是复杂的订单系统的极简化版本。这种设置存在几个潜在问题，包括：

- 在名称处输入多个单词将导致不会创建文件名。应该在代码中对名称进行检查。
- 订单输入系统是不安全的；它应该被放在受保护环境中。
- 用户在操作系统中被识别为 `nobody`，这是从 Web 访问网站的标准用户。为了让此用户创建文件，创建文件的目录必须保持开放可写状态。
