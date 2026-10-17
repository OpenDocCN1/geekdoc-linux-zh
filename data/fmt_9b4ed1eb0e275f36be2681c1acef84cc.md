
# 3) 外部重定向

`#ErrorDocument 402 http://some_server.com/subscription_info.html`

`# 注意：与请求相关的许多环境变量对该脚本无效。`

如注释所示，`ErrorDocument`指令可以自定义任何响应代码，将其重定向到外部页面、本地文件或 CGI 脚本或简单的文本句子。表格 21-6 列出了最常见的服务器响应代码及其含义。

# 第四部分 Red Hat Linux 网络与服务器设置

| 表格 21-6 | 服务器响应代码 |
| 响应代码 | 含义 |
| --- | --- |
| 200 OK | 请求处理成功。 |
| 201 Created | 使用 POST 请求，服务器上成功存储了新文件。 |
| 202 Accepted | 请求已接收并正在处理中。 |
| 204 No Content | 请求成功，但向客户端显示的当前页面没有变化。 |
| 301 Moved Permanently | 请求的页面已永久移动，未来对该面的引用应使用显示的新 URL。 |
| 302 Moved Temporarily | 请求的页面临时移动。未来的引用应继续使用相同的 URL，但当前连接被重定向。 |
| 304 Not Modified | 页面的缓存版本与请求页面相同。 |
| 400 Bad Request | 客户端请求包含无效语法。 |
| 401 Unauthorized | 客户端指定的用户名/密码组合无效。 |
| 402 Payment Required | 客户端必须提供完成货币交易的方法。 |
| 403 Forbidden | 访问控制机制拒绝客户端的请求。 |
| 404 Not Found | 请求的页面在服务器上不存在。 |
| 500 Internal Server Error | 通常在运行 CGI 程序时遇到，此响应代码表示程序或脚本包含无效代码，或收到了无法处理的输入。 |
| 501 Not Implemented | 服务器不支持请求方法（例如 GET, POST, PUT, DELETE, HEAD）。 |
| 502 Bad Gateway | 使用 Web 服务器作为代理时，在履行外部主机的请求时遇到错误。 |
| 503 Service Unavailable | 服务器正在处理过多的请求。 |
| 505 HTTP Version Not Supported | 服务器不支持请求版本（例如 HTTP/1.0, HTTP/1.1）。 |

## 为浏览器设置响应

如果文件扩展名不足以确定文件的 MIME 类型，你可以通过 `MimeMagicFile` 指令定义提示。通过 `BrowserMatch` 指令，你可以根据特定的浏览器类型设置响应。

# 第 21 章 + 设置 Web 服务器 822

```apache
# 以下指令修改了正常的 HTTP 响应行为。

# 第一条指令禁用 Netscape 2.x 以及伪造该功能的浏览器的 keepalive。这些浏览器的实现存在已知问题。

# 第二条指令用于 Microsoft Internet Explorer 4.0b2

# 它具有损坏的 HTTP/1.1 实现，并且在用于 301 或 302（重定向）响应时

# 无法正确支持 keepalive。
```

```apache
BrowserMatch "Mozilla/2" keepalive

BrowserMatch "MSIE 4.0.b2": keepalive downgrade-1.0 force-response-1.0
```

```apache
# 以下指令禁用了对浏览器的 HTTP/1.1 响应

# 因为它们无法理解基本的 1.1 响应，从而违反了 HTTP/1.0 规范。
```

```apache
BrowserMatch "RealPlayer 4.0" force-response-1.0

BrowserMatch "Java/1.0" force-response-1.0

BrowserMatch "JDK/1.0" force-response-1.0
```

`BrowserMatch` 指令允许根据 `User-agent:` 头部字段的内容设置环境变量。

# 启用 perl 模块

如果安装了 perl 模块（`mod_perl.c`），以下几行将启用 Perl 脚本的使用。这些行允许从 `/var/www/perl/` 目录使用 `perl-script`。`Options +ExecCGI` 允许执行 CGI 脚本执行。

```apache
# 如果安装了 perl 模块，此处将被启用。
<IfModule mod_perl.c>

  Alias /perl/ /var/www/perl/

  <Directory /var/www/perl>

    SetHandler perl-script

    PerlHandler Apache::Registry

    Options +ExecCGI

  </Directory>
</IfModule>
```

# 允许更新密码

通过启用以下行（默认关闭），你可以允许使用 http put 功能来生成新密码。正如注释所示，此功能允许诸如 Netscape Gold 发布功能之类的应用程序更改 HTTP 用户的身份验证。

```apache
# 允许 http put（例如 Netscape Gold 的发布功能）
# 使用 htpasswd 生成 /etc/httpd/conf/passwd。
<IfModule mod_put.c>
```

![](img/0823b2119053dace3be4993846bb1ee1_856_0.png)

# 824 第四部分 热热 Linux 网络和服务器设置

```apache
# Alias /upload /tmp
# <Directory /tmp>
# EnablePut On
# AuthType Basic
# AuthName Temporary
# AuthFile /etc/httpd/conf/passwd
# EnableDelete Off
# umask 027
# <Limit PUT>
# require valid-user
# </Limit>
# </Directory>
#<IfModule
```

如果你正在同步操作 `httpd.conf` 文件，我们注意到我们跳过了 `server-status` 行和 `server-info` 行的描述。这些功能将在稍后的“监控服务器活动”部分进行描述。

# 允许访问本地文档

随 Red Hat Linux 安装的每个软件软件包附带的文档存储在 `/usr/share/doc` 目录中。以下行允许用户通过 `httpd` 服务访问本地计算机上的该目录（即从他们的 Web 浏览器）：

```apache
# 允许从本地访问本地系统文档
Alias /doc/ /usr/share/doc/
<Directory /usr/share/doc>
order deny,allow
deny from all
allow from localhost .localdomain
Options Indexes FollowSymlinks
</Directory>
```

# 启用代理/缓存服务

代理和缓存服务默认关闭。你可以通过取消注释下面显示的几个值来启用它们：

```apache
# 代理服务器指令。取消以下行
# 启用代理服务器：
#<IfModule mod_proxy.c>
# ProxyRequests On
# <Directory proxy:\*>
# Order deny,allow
# Deny from all
# Allow from .your_domain.com
```

```apache
# </Directory>
# 启用/禁用对 HTTP/1.1 "Via:" 头的处理。
# (Full*) 添加服务器版本；"Block" 移除所有出的 Via: 头部
# 设置为之一：Off | On | Full | Block
# ProxyVia On
# 要同时启用缓存，请编辑并取消以下行：
#（不使用 CacheRoot 缓存）
#CacheRoot "/var/cache/httpd"
#CacheSize 5
#CacheGcInterval 4
#CacheMaxExpire 24
#CacheLastModifiedFactor 0.1
#CacheBefaultExpire 1
#NoCache a_domain.com another_domain.edu joes.garage_sale.com
</Module>
# 代理指令结束。
```
