
## 第 21 章：设置 Web 服务器

```apache
# 一些示例：
#ErrorDocument 500 "服务器发生了错误。"
#ErrorDocument 404 "/missing.html"
#ErrorDocument 404 "/cgi-bin/missing_handler.pl"
#ErrorDocument 402 http://www.example.com/subscription_info.html
#
```

如注释所示，`ErrorDocument` 指令可以自定义任何服务器响应码，将其重定向到外部页面、本地文件、CGI 脚本，或者一个简单的文本句子。表 21-6 列出了最常见的服务器响应码及其含义。

### 表 21-6：HTTP 响应码

| 响应码 | 含义 |
|---|---|
| 200 OK | 请求已成功处理。 |
| 201 Created | 使用 POST 请求方法，已在服务器上存储了新文件。 |
| 202 Accepted | 请求已接收，当前正在处理中。 |
| 204 No Content | 请求成功，但显示给客户端的当前页面没有变化。 |
| 301 Moved Permanently | 请求的页面已永久移动，未来对页面的引用应使用显示的新 URL。 |
| 302 Moved Temporarily | 请求的页面临时移动。未来的引用应继续使用相同的 URL，但当前连接已重定向。 |
| 304 Not Modified | 页面的缓存版本与请求的页面完全相同。 |
| 400 Bad Request | 客户端请求包含无效语法。 |
| 401 Unauthorized | 客户端指定的用户名/密码组合无效。 |
| 402 Payment Required | 客户端必须提供完成货币交易的方法。 |
| 403 Forbidden | 访问控制机制拒绝了客户端的请求。 |
| 404 Not Found | 请求的页面在服务器上不存在。 |
| 500 Internal Server Error | 通常在运行 CGI 程序时遇到，此响应码表示程序或脚本包含无效代码，或收到了无法处理的输入。 |
| 501 Not Implemented | 服务器不支持该请求方法（例如 GET, POST, PUT, DELETE, HEAD）。 |
| 502 Bad Gateway | 当 Web 服务器作为代理服务器时，在尝试履行外部主机的请求时遇到错误。 |
| 503 Service Unavailable | 服务器当前正在处理过多请求。 |
| 505 HTTP Version Not Supported | 服务器不支持请求版本（例如 HTTP/1.0, HTTP/1.1）。 |

## 第四部分：Fedora 和 RHEL 网络与服务器设置

为了更容易实现错误信息的国际化并标准化这些消息的呈现方式，Apache 的最新版本包含了所谓的变体页面（以 `.var` 后缀结尾）。这些根据语言提供变量输出的变体存储存储 `/var/www/error/` 目录下。

```apache
Alias /error/ "/var/www/error/"
```

```apache
<IfModule mod_negotiation.c>
<IfModule mod_include.c>
  <Directory "/var/www/error">
    AllowOverride None
    Options IncludesNoExec
    AddOutputFilter Includes html
    AddHandler type-map var
    Order allow, deny
    Allow from all
    LanguagePriority en es de fr
    ForceLanguagePriority Prefer Fallback
  </Directory>
</IfModule>
```

```apache
ErrorDocument 400 /error/HTTP_BAD_REQUEST.html.var
ErrorDocument 401 /error/HTTP_UNAUTHORIZED.html.var
ErrorDocument 403 /error/HTTP_FORBIDDEN.html.var
ErrorDocument 404 /error/HTTP_NOT_FOUND.html.var
ErrorDocument 405 /error/HTTP_METHOD_NOT_ALLOWED.html.var
```

`ErrorDocument` 指令将特定的错误码与包含基于语言的多种可能响应的 `.var` 文件关联。

## 设置到浏览器的响应

如果仅通过文件扩展名无法确定文件的 MIME 类型，你可以使用 `MIMEMagicFile` 指令定义提示。通过 `BrowserMatch` 指令，你可以根据特定浏览器类型的条件设置响应：

```apache
# 以下指令修改了正常的 HTTP 响应行为，以
# 处理浏览器实现中的已知问题。
#BrowserMatch "Mozilla/2" nokeepalive
```

```apache
BrowserMatch "MSIE 4.0;b2"; nokepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4.0" force-response-1.0
BrowserMatch "Java/1.0" force-response-1.0
BrowserMatch "JDK/1.0" force-response-1.0
```

```apache
#
# 以下指令禁用了非 GET 请求在不包含
# 末尾斜线的目录上的重定向。这修复了
# Microsoft WebFolders 的问题，它无法正确处理
# 使用 DAV 方法文件夹的重定向。
# Apple 的 DAV 文件系统和 Gnome VFS 对 DAV 的支持也是如此。
BrowserMatch "Microsoft Data Access Internet Publishing Provider"
redirect-carefully
BrowserMatch "MS FrontPage" redirect-carefully
BrowserMatch "WebDrive" redirect-carefully
BrowserMatch "WebDAVFS" redirect-carefully
BrowserMatch "gnome" redirect-carefully
BrowserMatch "XML" redirect-carefully
BrowserMatch "Spy" redirect-carefully
```
