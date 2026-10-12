
# 语言优先级

`LanguagePriority` 允许你在内容协商期间出现平局时为某些语言赋予优先级。只需按偏好程度递减的顺序列出语言。我们或多或少按字母顺序排列了它们。你可能需要更改此设置。

```
LanguagePriority en da nl et fr de el it ja ko no pl pt pt-br ru ltz ca es sv tw
```

`AddEncoding` 指令补充或覆盖 `TypesConfig` 文件（默认为 `/etc/mime.types`）提供的映射。了解 MIME 类型/编码可能会使某些浏览器在下载或检索文件时自动处理文件。

`AddLanguage` 指令执行类似的映射，将 MIME 语言定义与文件名扩展名关联起来。`LanguagePriority` 指令确定当特定文件以多种语言存在（并且客户端未指定偏好）时的优先级。使用前面的定义，如果从包含文件 `index.html.de`、`index.html.en`、`index.html.fr` 和 `index.html.it` 的目录请求文件 `index.html`，则会向客户端发送 `index.html.en` 文件。

使用 `LanguagePriority`，你可以在内容协商期间无法确定使用何种语言时设置使用的语言。如果你期望你的 Web 内容多语言使用，你应该检查（并且可能更改）此处的优先级。

## 选择字符集

要使用的默认字符集以及要为具有特定文件扩展名的文件使用的字符集分别使用 `AddDefaultCharset` 和 `AddCharset` 指令设置。虽然 UTF-8 是默认字符集，但建议在此明确设置它（如所示）。其他标准 ISO 字体以及一些非标准字体使用 `AddCharset` 指令设置。

```
AddDefaultCharset UTF-8
#
AddCharset  ISO-8859-1  .iso8859-1   .latin1
AddCharset  ISO-8859-2  .iso8859-2   .latin2 .cen
AddCharset  ISO-8859-3  .iso8859-3   .latin3
AddCharset  ISO-8859-4  .iso8859-4   .latin4
AddCharset  ISO-8859-5  .iso8859-5   .latin5 .cyr .iso-ru
AddCharset  ISO-8859-6  .iso8859-6   .latin6 .arb
```

你可以从以下地址获取官方的字符集列表及其分配的文件扩展名：`http://www.iana.org/assignments/character-sets`。

## 添加 MIME 类型和处理器

使用 `AddType` 指令，你可以在不编辑 `/etc/mime.types` 文件的情况下增强为 Apache Web 服务器分配的 MIME 类型。使用 `AddHandler` 指令，你可以将选定的文件扩展名映射到处理器（从而导致采取某些操作）：

```
# AddType allows you to add to or override the MIME configuration
# file mime.types for specific file types.
AddType application/x-tar .tgz
#
# For server-parsed imagemap files:
#
AddHandler imap-file map
#
# For type maps (negotiated resources):
# (This is enabled by default to allow the Apache "It Worked" page
#  to be distributed in multiple languages.)
#
AddHandler type-map var
```

## 定义操作和头信息

某些媒体类型可以设置为在打开时执行脚本。同样，某些处理器名称在打开时可以设置为执行指定的脚本。`Action` 指令可用于配置这些脚本：

```
# Action lets you define media types that execute a script whenever
# a matching file is called. This eliminates the need for repeated URL
# pathnames for oft-used CGI file processors.
# Format: Action media/type /cgi-script/location
# Format: Action handler-name /cgi-script/location
```

`Action` 指令将 CGI 脚本映射到处理器或 MIME 类型，而 `Script` 指令将 CGI 脚本映射到特定 HTTP 请求方法（GET、POST、PUT 或 DELETE）。这些选项允许在请求适当 MIME 类型的文件、调用处理器或调用请求方法时执行脚本。

## 自定义错误响应

对于发生的不同错误条件，你可以定义特定响应。响应可以是纯文本、重定向到本地服务器上的页面，或重定向到外部页面：

```
#
# Customizable error responses come in three flavors:
# 1) plain text 2) local redirects 3) external redirects
#
# Some examples:
#ErrorDocument 500 "The server made a boo hoo."
#ErrorDocument 404 /missing.html
#ErrorDocument 404 "/cgi-bin/missing_handler.pl"
#ErrorDocument 402 http://www.example.com/subscription_info.html
#
```

正如注释所建议的，`ErrorDocument` 指令可以自定义任何服务器响应代码，将其重定向到外部页面、本地文件或 CGI 脚本，或重定向到简单的文本句子。表 21-6 列出了最常见的服务器响应代码及其含义。

**表 21-6：服务器响应代码**

| 响应代码 | 含义 |
| --- | --- |
| 200 OK | 请求已成功处理。 |
| 201 Created | 使用 POST 请求方法，服务器上成功存储了新文件。 |
| 202 Accepted | 请求已收到，当前正在处理中。 |
| 204 No Content | 请求成功，但客户端显示的当前页面没有变化。 |
| 301 Moved Permanently | 所请求的页面已永久移动，今后对该页面的引用应使用显示的新 URL。 |
| 302 Moved Temporarily | 所请求的页面已被临时迁移。未来的引用应继续使用相同的 URL，但当前连接正在被重定向。 |
| 304 Not Modified | 页面的缓存版本与所请求的页面相同。 |
| 400 Bad Request | 客户端请求包含无效语法。 |
| 401 Unauthorized | 客户端指定的用户名/密码组合无效。 |
| 402 Payment Required | 客户端必须提供完成货币交易的方式。 |
| 403 Forbidden | 访问控制机制拒绝了客户端的请求。 |
| 404 Not Found | 所请求的页面在服务器上不存在。 |
| 500 Internal Server Error | 通常在运行 CGI 程序时遇到，此响应代码表示程序或脚本包含无效代码或被提供了无法处理的输入。 |
| 501 Not Implemented | 服务器不理解请求方法（例如 GET、POST、PUT、DELETE、HEAD）。 |
| 502 Bad Gateway | 使用 Web 服务器作为代理时，在履行对外部主机的请求时遇到错误。 |
| 503 Service Unavailable | 服务器当前正在处理太多请求。 |
| 505 HTTP Version Not Supported | 服务器不理解请求版本（例如 HTTP/1.0、HTTP/1.1）。 |

为了更轻松地国际化错误消息并标准化这些消息的呈现方式，最新版本的 Apache 包含所谓的变体页面（以 `.var` 后缀结尾）。这些变体页面提供基于语言的可变输出，存储在 `/var/www/error` 目录中。

```
Alias /error/ "/var/www/error/"

<IfModule mod_negotiation.c>
<IfModule mod_include.c>
<Directory "/var/www/error">
AllowOverride None
Options IncludesNoExec
AddOutputFilter Includes html
AddHandler type-map var
Order allow,deny
Allow from all
LanguagePriority en es de fr
ForceLanguagePriority Prefer Fallback
</Directory>

ErrorDocument 400 /error/HTTP_BAD_REQUEST.html.var
ErrorDocument 401 /error/HTTP_UNAUTHORIZED.html.var
ErrorDocument 403 /error/HTTP_FORBIDDEN.html.var
ErrorDocument 404 /error/HTTP_NOT_FOUND.html.var
ErrorDocument 405 /error/HTTP_METHOD_NOT_ALLOWED.html.var
.
.
```

`ErrorDocument` 指令将特定错误代码号与包含基于语言的多种可能响应的特定 `.var` 文件关联起来。

## 设置浏览器响应

如果文件扩展名不足以确定文件 MIME 类型，你可以使用 `MimeMagicFile` 指令定义提示。使用 `BrowserMatch` 指令，你可以根据特定浏览器类型设置响应条件：

```
#
# The following directives modify normal HTTP response behavior to
```
