
| 505 HTTP Version Not Supported | 请求版本（例如 HTTP/1.0、HTTP/1.1）不被服务器理解。 |

为了更容易地国际化错误消息并标准化这些消息的呈现方式，最新版本的 Apache 包含了所谓的变体页面（以 `.var` 扩展名结尾）。这些根据语言提供可变输出的变体页面存储在 `/var/www/error` 目录中。

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
</IfModule>
</IfModule>

ErrorDocument 400 /error/HTTP_BAD_REQUEST.html.var
ErrorDocument 401 /error/HTTP_UNAUTHORIZED.html.var
ErrorDocument 403 /error/HTTP_FORBIDDEN.html.var
ErrorDocument 404 /error/HTTP_NOT_FOUND.html.var
ErrorDocument 405 /error/HTTP_METHOD_NOT_ALLOWED.html.var
...
```

`ErrorDocument` 指令将一个特定的错误代码号与一个包含基于语言的多种可能响应的特定 `.var` 文件关联起来。

### 设置浏览器响应

如果文件扩展名不足以确定文件的 MIME 类型，您可以使用 `MimeMagicFile` 指令定义提示。使用 `BrowserMatch` 指令，您可以基于特定的浏览器类型设置响应条件：

```
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\\.0b2;" nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\\.0" force-response-1.0
BrowserMatch "Java/1.0" force-response-1.0
BrowserMatch "JDK/1.0" force-response-1.0

BrowserMatch "Microsoft Data Access Internet Publishing Provider"        redirect-carefully
BrowserMatch "MS FrontPage" redirect-carefully
BrowserMatch "^WebDrive" redirect-carefully
BrowserMatch "^WebDAVFS/[1.,0123]" redirect-carefully
BrowserMatch "^gnome-vfs/1.0" redirect-carefully
BrowserMatch "^XML Spy" redirect-carefully
BrowserMatch "Dreamweaver-WebDAV-SCM1" redirect-carefully
```

`BrowserMatch` 指令允许您根据 `User-agent:` 头部字段的内容设置环境变量。`force-response-1.0` 变量会导致 `HTTP/1.0` 响应，表明 Apache 将使用基本的 `HTTP 1.0` 操作来响应浏览器。

> **注意：** 如果您正在查看 `httpd.conf` 文件，您会注意到我们跳过了对 `server-status` 行和 `server-info` 行的描述。它们在本章后面的“监控服务器活动”部分中有描述。

### 启用代理和缓存服务

代理和缓存服务默认是关闭的。您可以通过取消注释以下指令来启用它们：

```
#  代理服务器指令。取消注释以下行以
#  启用代理服务器：
#
#<IfModule mod_proxy.c>
#   ProxyRequests On
#
#<Proxy * >
#   Order deny,allow
#   Deny from all
#   Allow from .example.com
#</Proxy>
#
# 启用/禁用对 HTTP/1.1 "Via:" 头的处理。
# ("Pull" 添加服务器版本；"Block" 移除发出的 Via: 头)
# 设置为以下之一：Off | On | Pull | Block
#
#ProxyVia On
#
# 若要启用代理内容的缓存，请取消注释以下各行。
# 详情请参阅 http://httpd.apache.org/docs/2.2/mod/mod_cache.html
#
#<IfModule mod_cache.c>
# CacheEnable disk /
# CacheRoot "/var/cache/mod_proxy"
#</IfModule>
#
#</IfModule>
#
# 代理指令结束。
```

Apache 可以作为代理服务器、缓存服务器，或两者的组合运行。如果 `ProxyRequests` 设置为 `Off`，服务器将仅缓存文件而不充当代理。如果 `CacheRoot`（指定用于包含缓存文件的目录）未定义，则不会执行缓存。代理和缓存服务默认都是 `Off`（被注释掉的）。

**注意：** 如果您使用 Tomcat Java 应用服务器配合 Apache，您还需要设置 `ProxyPass` 和 `ProxyPassReverse` 值。关于此主题的更多信息，请参阅 http://tomcat.apache.org/tomcat-6.0-doc/proxy-howto.html。如果启用缓存，`CacheRoot` 应存在于具有足够空闲空间的文件系统上以容纳缓存，该缓存受 `CacheSize` 指令限制。但是，您应在文件系统中保留多出 20% 到 40% 的空间，因为缓存清理（以维持 `CacheSize`，单位为千字节）仅定期发生（您可以使用 `CacheGCInterval` 指令设置此间隔）。

您可以在此示例中添加其他指令以启用其他缓存功能。`CacheMaxExpire` 指令可以指示文档在 Apache 检查原始文档是否有修改之前，在缓存中存在的最大小时数。`CacheLastModifiedFactor` 适用于没有过期时间的文档，即使协议支持该功能。为了形成过期日期，因子（一个浮点数）乘以自文档上次修改以来经过的小时数。例如，如果文档在三天前被修改且 `CacheLastModifiedFactor` 为 0.25，则文档将在 18 小时后从缓存中过期（只要该值仍低于 `CacheMaxExpire` 的值）。

`CacheDefaultExpire` 指令（指定文档过期前的小时数）适用于通过不支持过期时间协议接收的文档。

`NoCache` 指令包含一个由空格分隔的列表，其中包括 IP 地址、主机名或主机名中的关键字，这些条目对应的文档不应被缓存。

如果你取消注释前面的 Cache 行，缓存服务器将表现如下：

- 缓存文件位于 `/var/cache/mod_proxy`。
- 缓存大小限制为 500KB。

你可能希望允许一个更大的 `CacheSize`，并可能设置一个较短的 `CacheGcInterval`，但除此以外，提供的值是合理的。`CacheGcInterval` 的值可以是一个浮点数（例如，1.25 表示 75 分钟）。

### 配置虚拟主机

如果你只有一台 Web 服务器计算机，但希望使用这台计算机服务多个域名，你可以设置 Apache 进行虚拟主机配置。使用基于名称的虚拟主机，单个 IP 地址可以是同一台计算机上多个域名的访问点。使用基于 IP 的虚拟主机，每个虚拟主机都有一个不同的 IP 地址，这是通过为机器配置多个网络接口来实现的。

在使用虚拟主机时，当请求通过你计算机上的特定 IP 地址从 Web 浏览器进入你的 Apache 服务器时，Apache 会检查被请求的域名，并显示与该域名关联的内容。作为支持虚拟主机的 Web 服务器的管理员，你必须确保该虚拟服务器所需配置的所有内容都已正确设置（例如，定义 Web 内容位置、日志文件、管理联系人等）。

虚拟主机通过 `VirtualHost` 标签定义。与虚拟主机相关的信息在 `/etc/httpd/conf/httpd.conf` 文件中，如下面的代码所示：
