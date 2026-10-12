

## 添加 MIME 类型和处理程序

使用 `AddType` 指令，您可以在不编辑 `/etc/mime.types` 文件的情况下增强分配给 Apache Web 服务器的 MIME 类型。使用 `AddHandler` 指令，您可以将选定的文件扩展名映射到处理程序（从而导致执行某些操作）：

```
# AddType allows you to add to or override the MIME configuration
# file mime.types for specific file types.

AddType application/x-tar.tgz

#

# For server-parsed imagemap files:

AddHandler imap-file map

# For type maps (negotiated resources):
# (This is enabled by default to allow the Apache "It Worked" page
# to be distributed in multiple languages.)

AddHandler type-map var
```

## 定义操作和头部

某些类型的媒体可以在打开时被设置为执行脚本。同样，某些处理程序名称在打开时也可以被设置为执行指定的脚本。可以使用 `Action` 指令来配置这些脚本：

```
# Action lets you define media types that execute a script whenever
# a matching file is called. This eliminates the need for repeated URL
# pathnames for oft-used CGI file processors.
# Format: Action media/type /cgi-script/location
# Format: Action handler-name /cgi-script/location
```

`Action` 指令将 CGI 脚本映射到处理程序或 MIME 类型，而 `Script` 指令将 CGI 脚本映射到特定的 HTTP 请求方法（GET、POST、PUT 或 DELETE）。这些选项允许在请求适当 MIME 类型的文件、调用处理程序或调用请求方法时执行脚本。

## 自定义错误响应

对于发生的不同错误条件，您可以定义特定的响应。响应可以是纯文本、重定向到本地服务器上的页面，或重定向到外部页面：

```
#
# Customizable error responses come in three flavors:
# 1) plain text 2) local redirects 3) external redirects
#
# Some examples:
#ErrorDocument 500 "The server made a boo boo."
#ErrorDocument 404 /missing.html
#ErrorDocument 404 /cgi-bin/missing_handler.pl
#ErrorDocument 402 http://www.example.com/subscription_info.html
#
```

正如注释所建议的那样，`ErrorDocument` 指令可以自定义任何服务器响应代码，将其重定向到外部页面、本地文件或 CGI 脚本，或简单的文本句子。表 21-6 列出了最常见的服务器响应代码及其含义。

### 表 21-6：HTTP 响应代码

| 响应代码 | 含义 |
| :--- | :--- |
| 200 OK | 请求已成功处理。 |
| 201 Created | 使用 POST 请求方法，新文件已成功存储在服务器上。 |
| 202 Accepted | 请求已被接收，目前正在处理中。 |
| 204 No Content | 请求成功，但显示给客户端的当前页面没有变化。 |
| 301 Moved Permanently | 请求的页面已永久移动，对将来该页面的引用应使用显示的新 URL。 |
| 302 Moved Temporarily | 请求的页面已被临时移走。将来的引用应继续使用相同的 URL，但当前连接正在被重定向。 |
| 304 Not Modified | 页面的缓存版本与请求的页面相同。 |
| 400 Bad Request | 客户端的请求包含无效语法。 |
| 401 Unauthorized | 客户端指定了无效的用户名/密码组合。 |
| 402 Payment Required | 客户端必须提供完成货币交易的手段。 |
| 403 Forbidden | 访问控制机制拒绝了客户端的请求。 |
| 404 Not Found | 请求的页面在服务器上不存在。 |
| 500 Internal Server Error | 通常在运行 CGI 程序时遇到，此响应代码表示该程序或脚本包含无效代码或接收到了无法处理的输入。 |
| 501 Not Implemented | 请求方法（例如，GET、POST、PUT、DELETE、HEAD）不被服务器理解。 |
| 502 Bad Gateway | 使用 Web 服务器作为代理时，在满足对外部主机的请求过程中遇到了错误。 |
| 503 Service Unavailable | 服务器当前正在处理过多的请求。 |
| 505 HTTP Version Not Supported | 请求版本（例如，HTTP/1.0、HTTP/1.1）不被服务器理解。 |

为了使错误消息更容易国际化，并标准化这些消息的展示方式，最新版本的 Apache 包含了所谓的变体页面（以 .var 后缀结尾）。这些基于语言提供可变输出的变体页面存储于 `/var/www/error` 目录中。

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
```

`ErrorDocument` 指令将特定的错误代码编号与包含基于语言的多种可能响应的特定 `.var` 文件相关联。

## 设置浏览器响应

如果文件扩展名不足以确定文件的 MIME 类型，您可以使用 `MimeTypeMagicFile` 指令定义提示。使用 `BrowserMatch` 指令，您可以基于特定的浏览器类型设置响应条件：

```
#
# The following directives modify normal HTTP response behavior to
# handle known problems with browser implementations.
# 
BrowserMatch "Mozilla/2" nokeepalive 
BrowserMatch "MSIE 4\\.0b2"  nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\\.0" force-response-1.0
BrowserMatch "Java/1\\.0" force-response-1.0
BrowserMatch "jdk/1\\.0" force-response-1.0
 
#
# The following directive disables redirects on non-GET requests for 
# a directory that does not include the trailing slash.  This fixes a 
# problem with Microsoft WebFolders which does not appropriately handle 
# redirects for folders with DAV methods.
# Same deal with Apple's DAV filesystem and Gnome VFS support for DAV.
 
BrowserMatch "Microsoft Data Access Internet Publishing Provider" 
           redirect-carefully 
BrowserMatch "WebDrive" redirect-carefully 
BrowserMatch "WebDAVFS/1\.0[12]" redirect-carefully
BrowserMatch "gnome-vfs" redirect-carefully
```

`BrowserMatch` 指令使您能够基于 `User-agent:` 头部字段的内容设置环境变量。`force-response-1.0` 变量会导致 HTTP/1.0 响应，表示 Apache 将以基本 HTTP 1.0 操作响应浏览器。

> **注意：** 如果您正在阅读 httpd.conf 文件，您会发现我们跳过了服务器状态行和服务器信息行的描述。它们在本章后面的“监控服务器活动”部分中有描述。

## 启用代理和缓存服务

代理和缓存服务默认是关闭的。您可以通过取消注释以下指令来启用它们：

```
# Proxy Server directives. Uncomment the following lines to
# enable the proxy server:

#<IfModule mod_proxy.c> 
#     ProxyRequests On 
#
#<Proxy:*> 
#    Order deny,allow 
#    Deny from all 
#    Allow from .example.com 
#</Proxy>
#
# Enable/disable the handling of HTTP/1.1 "Via:" headers.
# ("Full" adds server version; "Block" removes outgoing Via: headers)
# Set to one of: Off | On | Full | Block
#
#ProxyVia On

# To enable a cache of proxied content, uncomment the following lines.
# See http://httpd.apache.org/docs-2.0/mod/mod_cache.html for more details.
#
#<IfModule mod_disk_cache.c>
# CacheEnable disk /
# CacheRoot "/var/cache/mod_proxy"
#</IfModule>

#</IfModule>
# End of proxy directives.
```

Apache 可以作为代理服务器、缓存服务器或两者的组合运行。如果 `ProxyRequests` 设置为 *Off*，服务器将仅缓存文件，而不作为代理运行。如果 `CacheRoot`（指定用于包含缓存文件的目录）未定义，则不会执行缓存。默认情况下，代理和缓存服务均为 *Off*（被注释掉）。

如果启用缓存，`CacheRoot` 应存在于具有足够可用空间的文件系统上，以容纳缓存，缓存受 `CacheSize` 指令限制。但是，您应该在文件系统中拥有 20% 到 40% 的额外可用空间，因为缓存清理（为维护 `CacheSize`，以千字节为单位）仅周期性发生（您可以使用 `CacheGcInterval` 指令设置）。

您可以在此示例中添加其他指令以启用其他缓存功能。`CacheMaxExpire` 指令可以指示文档在缓存中存在的最大小时数，而无需检查原始文档是否有修改。`CacheLastModifiedFactor` 适用于没有过期时间但协议支持过期时间的文档。为了制定过期日期，该因子（浮点数）乘以自文档最后修改以来经过的小时数。例如，如果文档三天前经过修改，且 `CacheLastModifiedFactor` 为 0.25，则文档将在 18 小时后从缓存中过期（只要此值仍低于 `CacheMaxExpire` 的值）。

`CacheDefaultExpire` 指令（指定文档过期前的小时数）适用于通过不支持过期时间的协议接收的文档。`NoCache` 指令包含一个空格分隔的 IP 地址、主机名或主机名中的关键字列表，这些不应缓存文档。

如果您取消注释上面的 `Cache` 行，缓存服务器的行为如下：

