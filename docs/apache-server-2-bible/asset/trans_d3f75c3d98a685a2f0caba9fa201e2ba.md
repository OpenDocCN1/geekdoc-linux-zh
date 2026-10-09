

```perl
my $num1 = $query->param('num1');
my $num2 = $query->param('num2');
```

```perl
#print $query->header;

print $query->start_html('Calculator');
print $query->h1("Calculator");
print $query->p("Number 1: $num1");
print $query->p("Number 2: $num2");
print $query->end_html;

exit 0;
```

我故意注释掉了 `$query->header` 这一行，因为该行通常会在 Web 浏览器上生成内部服务器错误消息。但是，由于我在这个脚本中添加了 `use CGI::Debug;` 语句，当通过 `http://www.domain.com/c/s.dll/cgidebug.pl?num1=1&num2=200` 访问该脚本时，它将显示以下内容：

```text
/cgi-bin/cgidebug.pl

Malformed header!

--- Program output below  ----------------------
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html
  PUBLIC "-//W3C//DTD XHTML Basic 1.0//EN"
  "http://www.w3.org/TR/xhtml-basic/xhtml-basic10.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en- US"><head><title>Calculator</title>
</head><body><h1>Calculator</h1><p>Number 1: 1</p><p>Number 2: 200</p></body></html>
-----------------------------------------------

This program finished in 0.078 seconds.

Parameters
----------
num1 -- 1[1]
num2 -- 3[200]

Cookies
-------

Environment
-----------
DOCUMENT_ROOT   -- 15[/home/kabir/www]
GATEWAY_INTERFACE = 7[CGI/1.1]
HTTP_ACCEPT = 133[image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, applica]... 
HTTP_ACCEPT_ENCODING = 13[gzip, deflate]
HTTP_ACCEPT_LANGUAGE = 5[en-us]
HTTP_CONNECTION = 10[Keep-Alive]
HTTP_HOST = 14[rhat.nitec.com]
HTTP_USER_AGENT = 50[Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 5.0)]
PATH = 60[/usr/bin:/bin:/usr/sbin:/sbin:/X11R6/bin:/home/kabir/bin]
QUERY_STRING = 15[num1=1&num2=200]
REMOTE_ADDR = 14[207.183.233.19]
REMOTE_PORT = 4[2841]
REQUEST_METHOD = 3[GET]
REQUEST_URI = 36[/cgi-bin/cgidebug.pl?num1=1&num2=200]
SCRIPT_FILENAME = 37[/home/kabir/www/asb2/ch12/cgidebug.pl]
SCRIPT_NAME = 20[/cgi-bin/cgidebug.pl]
SERVER_ADDR = 14[207.183.233.20]
SERVER_ADMIN = 16[you@your.address]
SERVER_NAME = 14[rhat.nitec.com]
SERVER_PORT = 2[80]
SERVER_PROTOCOL = 8[HTTP/1.1]
SERVER_SIGNATURE = 66[<ADDRESS>Apache/2.0.14 Server at rhat.nitec.com Port 80</ADD>... 
SERVER_SOFTWARE = 20[Apache/2.0.14 (Unix)]
```

如您所见，这里有大量的信息，可帮助您快速排查问题并修复脚本。例如，上述程序输出中的一行指出请求头格式错误。

## 13 章

# 服务器端包含 (SSI)

在第 12 章中，我讨论了如何使用 CGI 程序创建动态 Web 内容；然而，有些任务可能不需要开发完整的 CGI 程序，但依然需要一定的动态干预。

例如，假设您希望向所有 HTML 页面添加标准的版权声明；您将如何实现这一点？嗯，您有两种解决方案：

- 将版权声明的内容添加到每个 HTML 页面中。
- 编写一个 CGI 程序，将消息添加到每个 HTML 页面中。

这两个选项都不够优雅。第一个选项要求每当您修改版权声明时，必须手动更新所有文件。第二个选项要求您找到一种方法，在将每个页面发送到 Web 浏览器之前运行您的 CGI 程序。这也意味着每个页面上的每个链接都必须调用这个 CGI 程序，以便它可以向下一个页面附加该消息。像这样的情况需要一个更简单的解决方案。**服务器端包含** (SSI)，即本章的主题，就是那个更简单的解决方案。

### 什么是服务器端包含？

通常，SSI 页面是包含嵌入式命令的 HTML 页面，这些命令用于 Apache Web 服务器。Web 服务器通常不会在将 HTML 页面提供给 Web 浏览器（或任何其他 Web 客户端）之前解析这些页面。但是，在提供之前，Web 服务器始终会解析启用了 SSI 的 HTML 页面，如果发现页面中有任何特殊的 SSI 命令，就会执行该命令。图 13-1 展示了 Web 服务器简化后的 HTML 页面和启用 SSI 的 HTML (SHTML) 页面的传输周期。

### 本章内容

- 理解服务器端包含
- 为服务器端包含配置 Apache
- 在 Web 页面中应用服务器端包含

### 简化的 HTML 传输周期

![](img/e11fcbd2818a3495ac70085e5d8d1c26_408_0.png)

### 简化的 SHTML 传输周期

![](img/e11fcbd2818a3495ac70085e5d8d1c26_408_1.png)

图 13-1：HTML 页面和 SHTML 页面的简化传输周期示意图

如您所见，HTML 页面的 SSI 版本首先会被解析以查找 SSI 命令。这些命令被执行，然后新的输出会被传输到 Web 浏览器（即 Web 客户端）。

Apache 将 SSI 实现为 `INCLUDES` 过滤器。在配置 Apache 以支持 SSI 之前，您需要检查当前的 Apache 可执行文件（`httpd`），以确保其中包含了 `mod_include` 模块。我将在下一节中展示如何执行此操作。

## 为 SSI 配置 Apache

在使用 Apache 进行 SSI 之前，您需要确保已启用 SSI 支持。要了解当前的 Apache 二进制文件中是否内置了 `mod_include`，请从 `/usr/local/apache/bin` 目录或您安装 Apache 二进制文件的任何其他位置运行 `httpd -l | grep include` 命令。这将使您能够查看用于构建 Apache 可执行文件的所有模块列表。默认情况下，应该已经编译了该模块；如果没有，您需要使用 `-enable-include` 选项配置 Apache 源代码，然后重新编译并重新安装 Apache。

虽然标准的 Apache 发行版中默认编译了 `mod_include` 模块，但默认情况下并未启用 HTML 页面的解析。您可以如下一节所述，为整个目录或单一文件类型启用 SSI。

### 为整个目录启用 SSI

若要为名为 `/www/mysite/htdocs/parsed` 的目录启用 SSI，请将以下配置添加到 `httpd.conf` 中：

```apache
<Directory "/www/mysite/htdocs/parsed">
Options +Includes
SetOutputFilter INCLUDES
</Directory>
```

在这里，`Options` 指令设置为 `+Includes`，这启用了该目录中的 SSI 解析。`SetOutputFilter` 指令指示 Apache 解析来自该目录的所有页面以查找 SSI 命令。这意味着该目录中具有任何扩展名的文件都将进行服务器端解析。

例如，假设您具有以下虚拟主机配置：

```apache
<VirtualHost 192.168.1.100>
ServerName wh1.domain.com
DocumentRoot "/www/mysite/htdocs"
ScriptAlias "/cgi-bin/" "/www/mysite/htdocs/cgi-bin/"
<Directory "/www/mysite/htdocs/parsed">
Options +Includes
SetOutputFilter INCLUDES
</Directory>
</VirtualHost>
```

现在，如果 `/www/mysite/htdocs/parsed` 目录中包含任何 `.txt`、`.any`、`.html` 或任何 `.shtml` 文件，以下 URL 请求将被解析：

```text
http://wh1.domain.com/parsed/any.txt
http://wh1.domain.com/parsed/any.shtml
```

在大多数情况下，不需要解析文本文件（`.txt`）或 HTML 文件（`.html`），因为通常不会在这些文件中用于 SSI 命令。因此，除非您有意要解析所有类型的文件，否则上述配置会让 Apache 执行额外的工作。现在让我们看看如何将 SSI 解析限制为特定的文件类型。

### 为特定文件类型启用 SSI

若要限制目录中 SSI 解析的范围，只需使用 `AddType` 指令为启用了 SSI 的文件类型设置所需的 Content-Type 头，然后将 `INCLUDES` 过滤器包裹在 `FilesMatch` 容器中。例如：

```apache
Options +Includes
AddType text/html .shtml

<FilesMatch "\.shtml[.$]">
SetOutputFilter INCLUDES
</FilesMatch>
```

在这里，`Options` 指令设置为 `+Includes`，这启用了 SSI 解析。`AddType` 指令用于将名为 `.shtml` 的文件类型的 Content-Type 头设置为 `text/html`。然后，使用 `FilesMatch` 指令和正则表达式 `"\.shtml[.$]"` 将 `SetOutputFilter` 指令针对 `.shtml` 文件设置为 `INCLUDES`。现在再次查看上一节中的虚拟主机示例。这次让我们添加 `FilesMatch` 容器，如所示：

```apache
<VirtualHost 192.168.1.100>

ServerName vhl.domain.com
DocumentRoot "/www/mysite/htdocs"
ScriptAlias "/cgi-bin/" "/www/mysite/htdocs/cgi-bin/"

<Directory "/www/mysite/htdocs/parsed">
Options +Includes

AddType text/html .shtml

<FilesMatch ".shtml[.$]">
SetOutputFilter INCLUDES
</FilesMatch>

</Directory>

</VirtualHost>
```

现在，如果 `parsed` 子目录中有任何 `.txt`、`.html` 或 `.shtml` 文件，只有以下 URL 请求会告诉 Apache 解析 `.shtml` 文件的输出。

```text
http://vhl.domain.com/parsed/any.shtml
```

服务器不会解析另外两个 URL，即 `http://vhl.domain.com/parsed/any.txt` 和 `http://vhl.domain.com/parsed/any.html`，以查找 SSI 命令。这是大多数网站的首选配置，因为出于性能和站点组织的目的，您希望将服务器端解析限制在特定类型的文件上。

