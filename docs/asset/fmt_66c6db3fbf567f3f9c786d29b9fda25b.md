
此脚本中正在进行以下操作：

- 该脚本创建一个名为`$query`的CGI对象，并在另一个名为`$cfg`的对象中加载`mime-mail.ini`配置文件。然后，它将HTTP来源信息存储在名为`$referrerURL`的变量中，并使用`get_form_name()`子例程确定调用此脚本的页面名称。页面名称存储在`$pageName`变量中。
- 使用`$query->header`方法打印默认内容头（`text/html`）。然后检查该命名页面是否存在配置部分。它使用`$cfg->val($pageName, 'from')`方法在`mime-mail.ini`配置文件中定位名为`'from'`的参数。此参数必须在页面的相应部分中设置。以下是一个`mime-mail.ini`配置文件的示例。

```ini
[default]  
subject = A Web page forwarded by a friend
from = webmaster@domain.com

[mybooks.html]  
subject = Check out Kabir's linux books!
from = webmaster@domain.com
```

例如，如果CGI脚本是从类似`http://www.domain.com/mybooks.html`的URL调用的，那么脚本将把`$pageName`设置为`‘mybooks.html’`，并使用`$cfg->val($pageName, ‘from’)`方法在`[mybooks.html]`部分中查找`‘from’`参数。如果该参数因未设置或该部分缺失而缺失，则它将`$pageName`设置为`‘default’`，从而允许它使用`[default]`部分中的参数。因此，如果您不希望为显示通过电子邮件发送页面表单的每个页面定义单独的部分，那么拥有一个`[default]`部分是个好主意。

接下来，脚本确定用户是否输入了电子邮件地址，如果输入了，则检查电子邮件地址是否为`user@host`格式。如果电子邮件缺失或无效，则显示错误消息，脚本使用`abort()`子例程终止。如果接受电子邮件地址，它会检查用户是否在Web表单的名称字段中输入了其姓名。如果缺少姓名，则终止。

如果电子邮件地址和姓名均被接受，脚本使用`format_name()`子例程格式化用户名，并创建`MIME::Lite::HTML`对象。此对象使用`From`、`To`和`Subject`信息初始化。`From`地址由用户名和从配置文件读取的电子邮件信息组成。例如，如果名为`John Olson`的用户在`http://www.domain.com/mybooks.html`页面上填写通过电子邮件发送页面表单，脚本将创建`From`头为`John Olson <webmaster@domain.com>`。用户的电子邮件地址用于名称中，以告知接收电子邮件的朋友或同事是谁发起了该电子邮件。如果我们还收集了用户的电子邮件地址，我们也可以使用它来设置`From`头。但在两个小文本框中收集用户的电子邮件和朋友们的电子邮件地址可能会变得太令人困惑，如果没有适当的标签，这将占用页面的大量空间；因此，避免使用这种方案。

然后，`$mailHTML`对象用于解析来源URL。在此阶段，CGI脚本实际上充当嵌入式Web客户端，获取来源Web页面并创建发送电子邮件所需的MIME内容。使用`$mailHTML->send`方法发送电子邮件。使用`$mailHTML->errorstr`方法检测错误并将其存储在`@errors`中。如果没有错误，脚本显示页面已发送的消息并终止；如果有错误，则显示错误消息并终止。

# 在 Apache 中启用 CGI 调试支持

为了帮助CGI开发人员，Apache提供了CGI输出日志。对于每个CGI程序错误，日志文件包含几行日志条目。前两行包含请求时间、请求URL、HTTP状态码、CGI程序名称等信息。如果CGI程序无法运行，会有额外的两行包含错误信息。或者，如果错误是由于脚本返回了错误的头部信息，则信息会记录为：所有HTTP请求头部、CGI程序输出的所有头部，以及CGI程序的`STDOUT`（标准输出）和`STDIN`（标准输入）。如果脚本未能输出任何内容，则不包含`STDOUT`。

要在Apache中记录CGI输出，请使用以下部分描述的`mod_cgi`模块（它是标准发行版的一部分）中的指令。通过这些指令，您可以设置对您正在开发或尝试在系统上安装的CGI程序的记录。

## `ScriptLog`

`ScriptLog`指令设置CGI程序错误的日志文件名。如果日志文件是相对路径（即，不以`/`开头），则被视为相对于由`ServerRoot`指令设置的服务器根目录的相对路径。

- 语法：`ScriptLog filename`
- 上下文：`Resource config`

![](img/e11fcbd2818a3495ac70085e5d8d1c26_400_0.png)

使用此指令时，请确保日志目录可由`UserDir`指令指定的用户写入。出于效率或性能考虑，日常使用此指令可能不是一个好主意。我建议仅在需要时使用它，并在调试完成后将其关闭。

## `ScriptLogLength`

`ScriptLogLength`指令限制由`ScriptLog`指令指定的日志文件的大小。脚本日志文件可以为每个CGI错误记录大量信息，因此可能会迅速增长。通过使用此指令，您可以限制日志大小，以便当文件达到最大长度时，不再记录更多信息。

- 语法：`ScriptLogLength size`
- 默认：`ScriptLogLength 10385760`
- 上下文：`Resource config`

## `ScriptLogBuffer`

`ScriptLogBuffer`指令限制被记录的`POST`或`PUT`数据的大小。

- 语法：`ScriptLogBuffer size`
- 默认：`ScriptLogBuffer size 1024`
- 上下文：`Resource config`

# 调试您的基于 Perl 的 CGI 脚本

如果您使用基于Perl的CGI脚本，如本章前面所述，除了Apache提供的CGI日志外，您在故障排除方面还有很多其他帮助。您可以使用著名的`CGI.pm`模块从命令行调试基于Perl的CGI脚本。或者，您可以将调试消息写入标准错误日志（`STDERR`）文件，Apache会自动将其重定向到Apache错误日志。我将在以下部分讨论这些技术。

## 从命令行进行调试

如果您使用著名的CGI模块，如我在此章中讨论的所有实用CGI脚本中所做的那样，那您就很幸运了。CGI模块使您能够从命令行对CGI脚本进行故障排除，这使得调试脚本变得非常方便。让我们看一个名为`badcalc.pl`的示例CGI脚本，如清单 12-7 所示。

### 清单 12-7: `badcalc.pl`

```perl
#!/usr/bin/perl -w

use CGI;

my $query = new CGI;

my $num1 = $query->param('num1');

my $num2 = $query->param('num2');

my $sum = $num1 + $num2;

#print $query->header;

print "$num1 + $num2 = $sum";

exit 0;
```
