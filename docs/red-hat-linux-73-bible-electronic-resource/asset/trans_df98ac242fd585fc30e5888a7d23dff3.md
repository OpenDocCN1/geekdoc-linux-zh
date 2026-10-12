
# LanguagePriority：允许你在内容协商出现平局时
# 给予某些语言优先权。
#
# 只需按偏好程度从高到低列出语言即可。我们大致按字母顺序
# 排列了它们。你可能需要更改此设置。
#
<IfModule mod_negotiation.c>
LanguagePriority en da nl et fr de el it ja kr no pl pt pt-br ru ltz ca
es sv tw
</IfModule>

`AddEncoding` 指令用于补充或覆盖由 `TypesConfig` 文件提供的映射关系。了解 MIME 类型/编码可能使某些浏览器在下载或获取文件时自动对文件进行操作。

`AddLanguage` 指令执行类似的映射，将 MIME 语言定义与文件扩展名关联起来。如果特定文件存在多种语言版本（且客户端未指定偏好），则由 `LanguagePriority` 指令确定优先级。根据上述定义，如果请求目录中的 `index.html` 文件，而该目录包含文件 `index.html.de`、`index.html.en`、`index.html.fr` 和 `index.html.it`，则客户端将收到 `index.html.en` 文件。

## 添加 MIME 类型和处理器

使用 `AddType` 指令，您可以在不编辑 `/etc/mime.types` 文件的情况下增强为您的 Apache Web 服务器分配的 MIME 类型。使用 `AddHandler` 指令，您可以将特定的文件扩展名映射到处理器（这会导致执行某些操作）：

```
# AddType: allows you to tweak mime.types without actually editing it,
# or to make certain files to be certain types.

AddType application/x-tar .tgz

#
# These types cause httpd to let the PHP interpreter handle files with
# the specified extensions.
#
<IfModule mod_php4.c>
	AddType application/x-httpd-php .php .php4 .phtml
	AddType application/x-httpd-php-source .phps
</IfModule>
<IfModule mod_php3.c>
	AddType application/x-httpd-php3 .php3
	AddType application/x-httpd-php3-source .phps
</IfModule>
<IfModule mod_php.c>
	AddType application/x-httpd-php .phtml
</IfModule>

# 
# AddHandler: allows you to map certain file extensions to "handlers",
# actions unrelated to filetype. These can be either built into the
# server or added with the Action command (see below)
#
# If you want to use server side includes, or CGI outside
# ScriptAliased directories, uncomment the following lines.
# To use CGI scripts:
#
#AddHandler cgi-script .cgi
#
# To use server-parsed HTML files
#
AddType text/html .shtml
AddHandler server-parsed .shtml

#
# Uncomment the following line to enable Apache's send-as-is HTTP file
# feature
#
#AddHandler send-as-is asis

#
# If you wish to use server-parsed imagemap files, use
#
AddHandler imap-file map

#
# To enable type maps, you may want to use
#
#AddHandler type-map var
```

## 定义动作和头部

某些类型的媒体可以设置为在打开时执行脚本。同样，某些处理器名称在打开时也可以被设置为执行指定脚本。可以使用 Action 指令来配置这些脚本：

```
# Action lets you define media types that execute a script whenever
# a matching file is called. This eliminates the need for repeated URL
# pathnames for oft-used CGI file processors.
# Format: Action media/type /cgi-script/location
# Format: Action handler-name /cgi-script/location

# MetaDir: specifies the name of the directory in which Apache can find
# meta information files. These files contain additional HTTP headers
# to include when sending the document

#MetaDir .web

# MetaSuffix: specifies the file name suffix for the file containing
# the meta information.

#MetaSuffix .meta
```

**Action** 指令将 CGI 脚本映射到处理器或 MIME 类型，而 **Script** 指令将 CGI 脚本映射到特定的 HTTP 请求方法（GET、POST、PUT 或 DELETE）。这些选项允许在请求具有适当 MIME 类型的文件、调用处理器或触发请求方法时执行脚本。

**MetaDir** 和 **MetaSuffix** 指令实现了原始 CERN httpd 守护进程的一项功能，允许随请求文件发送额外的 HTTP 头信息。如果上面的两行代码被取消注释，对文件的任何请求都将包括搜索同一目录下名为 .web 的子目录，然后在该目录中搜索与请求文件同名但带有 .meta 后缀的文件。例如，如果客户端请求 `http://www.mybox.com/services/grant.html`（存储为 `/home/httpd/html/services/grant.html`），则文件 `/home/httpd/html/services/.web/grant.html.meta` 将为客户端提供额外的 HTTP 头信息。

## 自定义错误响应

对于发生的不同错误状况，您可以定义特定的响应。响应可以是纯文本、重定向到本地服务器上的页面，或重定向到外部页面：

```
# Customizable error response (Apache style)
#  these come in three flavors
#
#    1) plain text
#ErrorDocument 500 "The server made a boo boo.
# n.b. the (" ) marks it as text, it does not get output
#
#    2) local redirects
#ErrorDocument 404 /missing.html
#  to redirect to local url /missing.html
#ErrorDocument 404 /cgi-bin/missing_handler.pl
#  N.B. can redirect to a script or a document using server-side
#  includes.
#
#    3) external redirects
#ErrorDocument 402 http://some.other_server.com/subscription_info.html
#  N.B.: Many of the environment variables associated with the original
#  request will *not* be available to such a script.
```

正如注释所示，*ErrorDocument* 指令可以自定义任何服务器响应代码，将其重定向到外部页面、本地文件或 CGI 脚本，或重定向到简单的文本语句。表 21-6 列出了最常见的服务器响应代码及其含义。

### 表 21-6：服务器响应代码

| 响应代码 | 含义 |
|---|---|
| 200 OK | 请求已成功处理。 |
| 201 Created | 使用 POST 请求方法，新文件已成功存储在服务器上。 |
| 202 Accepted | 请求已收到，目前正在处理中。 |
| 204 No Content | 请求成功，但显示给客户端的当前页面没有变化。 |
| 301 Moved Permanently | 请求的页面已永久移动，对该页面的后续引用应使用显示的新 URL。 |
| 302 Moved Temporarily | 请求的页面已临时迁移。后续引用应继续使用相同的 URL，但当前连接正在被重定向。 |
| 304 Not Modified | 该页面的缓存版本与请求的页面完全相同。 |
| 400 Bad Request | 客户端的请求包含无效语法。 |
| 401 Unauthorized | 客户端指定了无效的用户名/密码组合。 |
| 402 Payment Required | 客户端必须提供完成货币交易的方式。 |
| 403 Forbidden | 访问控制机制拒绝了客户端的请求。 |
| 404 Not Found | 请求的页面在服务器上不存在。 |
| 500 Internal Server Error | 通常在运行 CGI 程序时遇到，此响应代码表示该程序或脚本包含无效代码，或收到了其无法处理的输入。 |
| 501 Not Implemented | 请求方法（例如，GET、POST、PUT、DELETE、HEAD）不被服务器理解。 |
| 502 Bad Gateway | 将 Web 服务器用作代理时，在满足对外部主机的请求时遇到错误。 |
| 503 Service Unavailable | 服务器当前正在处理过多的请求。 |
| 505 HTTP Version Not Supported | 请求版本（例如，HTTP/1.0、HTTP/1.1）不被服务器理解。 |

## 设置对浏览器的响应

如果文件扩展名不足以确定文件的 MIME 类型，您可以使用 `MimeMagicFile` 指令定义提示。使用 `BrowserMatch` 指令，您可以根据特定浏览器类型设置基于条件的响应：

```
# The following directives modify normal HTTP response behavior.
# First directive disables keepalive for Netscape 2.x and browsers that
# spoof. There are known problems with these browser implementations.
# The second directive is for Microsoft Internet Explorer 4.0b2
# which has a broken HTTP/1.1 implementation and does not properly
# support keepalive when it is used on 301 or 302 (redirect) responses.
#
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\\.0b2;" nokeepalive downgrade-1.0 force-response-1.0
#
# The following directive disables HTTP/1.1 responses to browsers which
# are in violation of the HTTP/1.0 spec by not being able to grok a
# basic 1.1 response.
#
BrowserMatch "RealPlayer 4\\.0" force-response-1.0
BrowserMatch "Java/1\\.0" force-response-1.0
BrowserMatch "JDK/1\\.0" force-response-1.0
```

`BrowserMatch` 指令允许您根据 `User-agent` 头字段的内容设置环境变量。`force-response-1.0` 变量会导致产生 HTTP/1.0 响应，表明该浏览器无法支持基本的 HTTP 操作。

## 启用 perl 模块

如果已安装 perl 模块（mod_perl.c），则以下行允许使用 Perl 脚本。这些行允许从 /var/www/perl 目录使用 perl-script。Options +ExecCGI 行允许执行 CGI 脚本。

```
# If the perl module is installed, this will allow execution of
# mod_perl to compile your scripts to subroutines which it will execute
# directly, avoiding the costly compile process for most requests.
#
<IfModule mod_perl.c>
    Alias /perl/ /var/www/perl/
    <Directory /var/www/perl>
        SetHandler perl-script
        PerlHandler Apache::Registry
        Options +ExecCGI
    </Directory>
</IfModule>
```

