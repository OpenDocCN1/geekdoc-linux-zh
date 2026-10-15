

Squid 还支持 ident 和 proxy 身份验证方法来控制用户访问。以下示例仅允许用户 dylan 和 chris 使用 Squid 缓存：

```
ident_lookup on
acl goodusers user chris dylan
http_access allow goodusers
http_access deny all
```

| 选项 | 描述 |
|---|---|
| src ip-address/netmask | 客户端的 IP 地址 |
| src addr1-addr2/netmask | 地址范围 |
| dst ip-address/netmask | 目标 IP 地址 |
| myip ip-address/netmask | 本地套接字 IP 地址 |
| srcdomain domain | 反向查找，客户端 IP |
| dstdomain domain | 来自 URL 的目标服务器；对于 dstdomain 和 dstdom_regex，如果使用基于 IP 的 URL，则会尝试反向查找 |
| srcdom_regex [-i] expression | 匹配客户端名称的正则表达式 |
| dstdom_regex [-i] expression | 匹配目标的正则表达式 |
| time [day-abbrevs] [h1:m1-h2:m2] | 按天、小时和分钟指定的时间。星期缩写：S = 星期日，M = 星期一，T = 星期二，W = 星期三，H = 星期四，F = 星期五，A = 星期六 |
| url_regex [-i] expression | 匹配整个 URL 的正则表达式 |
| urlpath_regex [-i] expression | 匹配 URL 路径的正则表达式 |
| port ports | 指定端口或端口范围 |
| proto protocol | 指定协议，例如 HTTP 或 FTP |
| method method | 指定方法，例如 GET 和 POST |
| browser [-i] regexp | 在 user-agent 头上进行模式匹配 |
| ident username | 在 ident 输出上进行字符串匹配 |
| src_as number | 用于将请求路由到特定缓存 |
| dst_as number | 用于将请求路由到特定缓存 |
| proxy_auth username | 有效用户名列表 |
| snmp_community string | 用于限制对 SNMP 代理访问的社区字符串 |

**表 23-1 Squid ACL 选项**

## 缓存

Squid 使用 Internet 缓存协议 (ICP) 与其他 Web 缓存通信。使用 ICP 协议，您的 Squid 缓存可以连接到其他 Squid 缓存或其他缓存服务器，例如 Microsoft 代理服务器、Netscape 代理服务器和 Novell BorderManager。这样，如果您的网络的 Squid 缓存没有请求的 Web 页面的副本，它可以联系另一个缓存，看看是否在那里，而不是访问原始站点。您可以通过将其连接到缓存层次结构来配置 Squid 以连接到其他 Squid 缓存。Squid 支持由 child、sibling 和 parent 术语表示的缓存层次结构。Sibling 和 child 缓存可在同一级别访问，并在请求无法在您自己的 Squid 缓存中找到时自动查询。如果这些查询失败，则会查询父缓存，然后父缓存会搜索其自己的子缓存和兄弟缓存——或其自己的父缓存（如有需要）——依此类推。使用 cache_host 设置父级和兄弟级层次结构连接。

```
cache_host sd.cache.nlanr.net parent 3128 3130
```

您可以通过在 squid.conf 文件中使用以下条目注册您的缓存来设置缓存层次结构以连接到主 NLANR 服务器：

```
cache_announce 24
announce_to sd.cache.nlanr.net:3131
```

## 日志

Squid 保留多个日志。access.log 包含发送到您的代理的请求，cache.log 包含 Squid 服务器消息，例如错误和启动消息，而 store.log 包含有关 Squid 缓存的信息，例如添加或删除的对象。您可以使用缓存管理器 (cachemgr.cgi) 来管理缓存并在缓存管理器运行时查看其统计信息。要运行缓存管理器，请使用浏览器执行 cachemgr.cgi 脚本（此脚本应放置在您的 Web 服务器的 cgi-bin 目录中）。

## Web 服务器加速：反向代理缓存

尽管 Squid 缓存可以通过客户端增强对 Web 服务器的访问，但 Squid 也可以减轻 Web 服务器的负载。被请求压垮的 Web 服务器可以将可缓存页面移至 Squid 代理服务器，该服务器可以充当一种替代站点，处理对这些页面的请求。实际上，Web 服务器变得加速了。这种缓存被称为反向代理缓存，关注的是服务器而不是客户端。反向代理缓存将拦截对服务器的请求，处理其缓存页面的请求。只有对未缓存页面的请求才会被转发到原始 Web 服务器。

要配置反向代理缓存，您使用 httpd_accel 指令。httpd_accel_host 指定原始 Web 服务器的地址，而 httpd_accel_port 是其使用的端口。如果代理仅支持一个 Web 服务器，则将 httpd_accel_single_host 设置为 on，而如果代理支持多个 Web 服务器，则将其设置为 off。如果您希望代理服务器既用作客户端的代理，又用作 Web 服务器的反向代理，则将 httpd_accel_with_proxy 选项设置为 on。但是，客户端随后需要配置其浏览器以访问 Web 服务器，就像访问任何标准代理一样。

