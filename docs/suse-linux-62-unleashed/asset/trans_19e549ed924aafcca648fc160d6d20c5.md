

# 网络与互联网服务
第二部分

为了在 ScriptAlias 目录之外执行 CGI 程序，你需要为该目录启用 ExecCGI 选项。这可以在你的 httpd.conf 文件（1.3.4 之前的版本为 access.conf）或该目录下的 .htaccess 文件中完成。

CGI 程序可以使用任何语言编写。用于 CGI 编程最流行的语言是 Perl、Python 和 C。你可能想找读一本关于 CGI 编程的好书，例如《第二版 Perl CGI 编程》（CGI Programming With Perl, Second Edition），因为本书并不是一本关于 CGI 的书。你也可以访问 http://www.perl.org 来帮助定位网络上的 Perl 资源。

对于 Python，一本好书是《网络编程》（Internet Programming With Python），或者你可以访问 http://www.python.org。

要测试 CGI 是否配置正确，可以尝试以下用 Perl 编写的 CGI 程序，它可以显示 HTTP 环境变量的值：

```perl
#!/usr/bin/perl
print "Content-type: text/html\n";
print "<html><head>Simple CGI program</title></head><body>\n";
for (keys %ENV) {
    print "\$_ = \$ENV{\$_}<br>\n";
}
print "</body></html>\n";
```

如果你打算用 Perl 编写 CGI 程序，你可能想查看随 Perl 带的模块。

# SSI

服务器端包含（Server Side Includes）是直接写入 HTML 页面中的指令，服务器在将页面提供给 Web 客户端时对其进行解析。它们可以用于包含其他文件、程序的输出或环境变量。

启用 SSI 最常见的方法是指定具有特定文件扩展名（通常为 .shtml）的文件在提供时由服务器解析。这通过在你的 httpd.conf 文件（1.3.4 之前的版本为 srm.conf）中使用以下几行来实现：

```apache
# 使用服务器解析的 HTML 文件
#AddType text/html .shtml
AddHandler server-parsed .shtml
```

通过取消 AddType 和 AddHandler 行的注释，你可以告诉服务器解析所有 .shtml 文件以查找 SSI 指令。

另一种不那么常用、但在我看来更好的启用 SSI 的方法是使用 XBitHack 指令。XBitHack 可以设置为 on 或 off，并可以在你的配置文件或 .htaccess 文件中设置。如果 XBitHack 指令开启，则表示所有带有用户执行位的文件都将被解析以查找 SSI 指令。这有两个主要优势：首先，你不需要重命名文件并更改指向该文件的所有链接，仅仅因为你想向其添加一点动态内容。另一个原因是美观考虑——当你动态生成页面时，查看你 Web 内容的用户无法看到文件名，因此你的“魔术”会显得更令人印象深刻一点。

除了这些指令外，对于你想要允许 SSI 的目录，必须指定以下指令：

Options Includes

或者，你也可以指定：

Options IncludesNOEXEC

此选项启用 SSI，但关闭几个最强大和/或危险的 SSI 指令：exec 和 include。

这可以在服务器配置文件或 .htaccess 文件中设置。

## 基础 SSI 指令

SSI 指令看起来很像 HTML 注释标签。语法如下：

```html
<!--element attribute=value attribute=value ... -->
```

该元素可以是以下之一：

- config 允许你设置有关如何处理文档解析的各种配置选项。由于页面是从上到下解析的，config 指令应该出现在 HTML 文档的顶部。使用此命令可以设置三种配置：
  - errrmsg 如果解析文档时出现错误，则设置返回给客户端的错误消息。通常是 [error occurred while processing this directive]，但可以使用此指令将其设置为任何内容。
  - 示例：<!--#config errMsg="[It's broken, dude]"-->
  - sizefmt 设置用于显示文件大小的格式。你可以将值设置为 bytes 以显示精确的字节大小，或者缩写为以 KB 或 MB 显示大小。
  - 示例：<!--#config sizefmt="bytes"-->
- timefmt 设置用于显示时间的格式。该值的格式与 C（以及 Perl）中用于显示日期的 strftime 函数相同，如下表所示。

| 占位符 | 说明 |
| :--- | :--- |
| %a | 星期缩写 |
| %A | 星期 |
| %b | 月份缩写 |
| %B | 月份 |
| %c | ctime 格式: Sat Nov 19 21:05:57 1994 |
| %d | 月中的数字日期 |
| %e | DD |
| %D | MM/DD/YY |
| %h | 月份缩写 |
| %H | 小时，24 小时制，前导零 |
| %I | 小时，12 小时制，前导零 |
| %j | 年中的第 |
| %k | 小时 |
| %l | 小时，12 小时制 |
| %m | 月份，从 01 开始 |
| %M | 分钟，前导零 |
| %n | 换行 |
| %o | 华丽日期—1st, 2nd, 25th 等 |
| %p | AM 或 PM |
| %r | 时间格式: 09:05:57 PM |
| %R | 时间格式: 21:05 |
| %S | 秒，前导零 |
| %t | 制表符 |
| %T | 时间格式: 21:05:57 |
| %U 以星期日为每周的第一天的周数 |
| %w | 星期几，数字形式；星期日 == 0 |
| %W 以星期一为每周的第一天的周数 |
| %x | 日期格式: 11/19/94 |
| %X | 时间格式: 21:05:57 |
| %y | 年（两位） |
| %Y | 年（四位） |
| %Z | ASCII 时区，例如 PST |

- echo 显示此处列出的任何一个嵌套变量。时间将按 fmt 指定的格式格式显示。要显示的变量由 var 属性指定。

- DATE_GMT 格林尼治标准时间的当前日期。
- DATE_LOCAL 本地区的当前日期。
- DOCUMENT_NAME 文件名
- DOCUMENT_URI 文档的 URL。
- LAST_MODIFIED 文档的最后修改日期。
- PATH_INFO 文档的路径信息。
- QUERY_STRING 传递给文档的查询字符串。
- REQUEST_METHOD 文档的请求方法。
- SERVER_SOFTWARE 服务器软件名称。
- USER_AGENT 客户端的用户代理字符串。

- cgi 要执行的程序。
- cmd 要执行的 shell 命令。
- fsize 文件大小。
- file 的文件系统路径。
- virtual 文件的 URL 路径。

- printenv 显示所有存在的变量。没有属性。
- set 设置变量的值。属性为 var 和 value。

- include 包含文件的内容。
- cgi 要执行的程序。
- file 的文件系统路径。
- virtual 文件的 URL 路径。

