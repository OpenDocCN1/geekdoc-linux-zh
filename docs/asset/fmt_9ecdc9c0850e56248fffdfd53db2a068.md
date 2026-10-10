
# 第 21 章：设置 Web 服务器 869

如注释所示，`ErrorDocument`指令可以自定义任何响应代码，将其重定向到外部页面、本地文件或 CGI 脚本，或者简单的文本句子。表 21-6 列出了最常见的服务器响应代码及其含义。

## 表 21-6：HTTP 响应代码

| 响应代码 | 含义 |
| --- | --- |
| 200 OK | 请求已成功处理。 |
| 201 Created | 使用 POST 请求方法，新文件已成功存储在服务器上。 |
| 202 Accepted | 请求已接收，正在处理中。 |
| 204 No Content | 请求成功，但显示给客户端的当前页面没有变化。 |
| 301 Moved Permanently | 请求的页面已永久移动，未来对页面的引用应使用新的 URL。 |
| 302 Moved Temporarily | 请求的页面临时移动。未来的引用应继续使用相同的 URL，但当前连接已重定向。 |
| 304 Not Modified | 页面的缓存版本与请求的页面相同。 |
| 400 Bad Request | 客户端请求包含无效语法。 |
| 401 Unauthorized | 客户端指定的用户名/密码组合无效。 |
| 402 Payment Required | 客户端必须提供完成货币交易的手段。 |
| 403 Forbidden | 访问控制机制拒绝客户端的请求。 |
| 404 Not Found | 请求的页面在服务器上不存在。 |
| 500 Internal Server Error | 通常在运行 CGI 程序时遇到，此响应代码表示程序或脚本包含无效代码或无法处理的变量输入。 |
| 501 Not Implemented | 服务器不支持请求方法（例如 GET、POST、PUT、DELETE、HEAD）。 |
| 502 Bad Gateway | 当 Web 服务器作为代理服务器时，在履行外部主机的请求时遇到错误。 |
| 503 Service Unavailable | 服务器当前正在处理许多请求。 |
| 505 HTTP Version Not Supported | 服务器不支持请求版本（例如 HTTP/1.0、HTTP/1.1）。 |

为了更容易实现错误消息的国际化并标准化这些消息的呈现方式，最新版本的 Apache 包含了所谓的变体页面（以 `.var` 结尾）。这些变体页面根据语言提供变体输出，存储在 `/var/www/error` 目录下。

## 870 第四部分：Fedora RHEL 网络和服务器设置

`Alias /error/ "/var/www/error/"`

```
<IfModule mod_negotiation.c>
<IfModule mod_include.c>
  <Directory "/var/www/error">
    AllowOverride None
    Options IncludesNoExec html
    AddHandler type-map var
    Order allow,deny
    Allow from all
    LanguagePriority is es de fr
    ForceLanguagePriority Prefer Fallback
  </Directory>
```

```
ErrorDocument 400 /error/HTTP_BAD_REQUEST.html.var
ErrorDocument 401 /error/HTTP_UNAUTHORIZED.html.var
ErrorDocument 403 /error/HTTP_FORBIDDEN.html.var
ErrorDocument 404 /error/HTTP_NOT_FOUND.html
ErrorDocument 405 /error/HTTP_METHOD_ALLOWED.html
```

`ErrorDocument`指令将特定的错误代码与特定的文件关联，该文件包含基于语言的响应。

### 为浏览器设置响应

如果仅通过扩展名无法确定文件类型，你可以使用 `BrowserMatch`指令定义提示。通过 `BrowserMatch`指令，你可以根据特定的浏览器类型设置条件响应：

```
# 这些指令修改了正常的 HTTP 响应行为，以
# 处理浏览器实现中的已知问题
BrowserMatch "Mozilla*" keepalive
BrowserMatch "MSIE 4.0" downgrade-1.0
BrowserMatch "RealPlayer 4.0" force-response-1.0
BrowserMatch "Java/1.0" force-response-1.0
BrowserMatch "JDK/1.0" force-response-1.0
#
# 以下指令禁用了非 GET 请求在不包含尾部斜线的目录
# 上的定向。这修复了 WebFolders 无法正确处理
# 带有 DAV 的文件夹重定向的问题。Apple 的
# 文件系统和 Gnome VFS 对 DAV 的支持也是如此。
# 第 21 章：设置 Web 服务器 871
```

```
# BrowserMatch "不包含尾部斜线的目录" 
BrowserMatch "FrontPage"
BrowserMatch "WebDAV/1.0"
BrowserMatch "Data"
BrowserMatch "XML/1.0"
BrowserMatch "gnome-vfs/1.0"
BrowserMatch "Spy"
```

### 代理和缓存服务

代理和缓存服务默认是关闭的。要它们它们，可以取消注释以下行：

```
# 代理指令。
<IfModule mod_proxy.c>
  ProxyRequests On
</IfModule>
```

如果你只想启用缓存而不作为代理，可以将 `Proxy` 设置 `Off`：

```
# 启用缓存的 HTTP/1.1
Proxy Off
```

要启用磁盘缓存，可以取消注释以下行：

```
<IfModule mod_cache.c>
CacheEnable disk
CacheRoot "/var/cache/mod_proxy"
</IfModule>
```

### 配置虚拟主机

如果你有一台 Web 服务器计算机，但有多个想要通过该计算机提供服务的域名，你可以配置 Apache 使用虚拟主机。通过基于名称的虚拟主机，单个 IP 地址可以作为同一台计算机上多个域名的访问点。通过基于 IP 的虚拟主机，你为每个虚拟主机拥有一个不同的 IP 地址，这通过为计算机配备多个网络接口来实现。

使用虚拟主机时，当请求从 Web 浏览器通过你计算机上的特定 IP 地址进入你的 Apache 服务器时，Apache 会检查所请求的域名并显示与该域名关联的内容。作为支持虚拟主机的 Web 服务器管理员，你必须确保虚拟服务器需要配置的所有内容都已设置（你定义的项包括 Web 内容的位置、日志文件、管理员联系方式等）。

虚拟主机是通过 `VirtualHost` 标签定义的。`/etc/httpd/conf/httpd.conf` 文件中与虚拟主机相关的信息如下代码所示：

```
### 第 3 部分：虚拟主机

# VirtualHost: 如果你想在你的计算机上维护多个域名/主机名，
# 你可以为它们设置 VirtualHost 容器。大多数
# 配置仅使用基于名称的虚拟主机，因此服务器
# 不需要担心 IP 地址。这通过下面指令中的
# 星号标出。
#
# 在尝试设置虚拟主机之前，请参阅文档
# <URL:http://apache.org/docs/2.2/vhosts/>
# 以获取更多细节。
#
# 你可以使用命令行选项 '-S' 来验证你的虚拟主机
# 配置。
# 使用基于名称的虚拟主机。
# # 注意：如果使用了 mod_ssl，由于 SSL 协议
# 的性质，在没有端口指定符（例如 *:80）的情况下
无法使用 NameVirtualHost。
#
# VirtualHost 示例：
# 几乎任何 Apache 指令都可以进入 VirtualHost 容器。
# 第 VirtualHost 部分用于没有已知服务器
# 名称的请求。
#
<VirtualHost *:80>
# ServerAdmin webmaster@dummy-host.example.com
```

# 第 IV 部分：Fedora RHEL 网络和服务器设置

```
# DocumentRoot /www/docs/dummy-host.example.com
# ServerName dummy-host.example.com
# ErrorLog logs/dummy-host.example.com-error_log
# CustomLog logs/dummy-host.example.com-access_log common
#</VirtualHost>
```
