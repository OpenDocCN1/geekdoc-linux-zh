
### 创建基于浏览器匹配的内容 URL

你可以使用重写规则向不同的浏览器分发不同的内容（使用内部子请求）。你不能为此使用内容协商，因为浏览器不会以那种形式提供它们的类型。相反，你必须对 HTTP 头 `User-Agent` 进行操作。例如，如果浏览器的 `User-Agent` 头匹配 `Mozilla/5`，则你可以发送一个支持 Netscape Navigator 5（或更高版本）特性的页面，或者如果浏览器是旧版本的 Navigator 或其他类型的浏览器，你可以发送一个不同的页面。

如果 HTTP 头 `User-Agent` 以 `Mozilla/5` 开头，则页面 `foo.html` 会被重写为 `foo.ns.html`，并且重写停止。如果浏览器是 Lynx 或 Mozilla 1 到 4 版本，则 URL 变为 `foo.dull.html`。所有其他浏览器都会收到页面 `foo.cool.html`。这是通过以下规则完成的：

```
RewriteCond %{HTTP_USER_AGENT}    "Mozilla/5.*"

RewriteRule ^foo\.html$         foo.cool.html  [L]

RewriteCond %{HTTP_USER_AGENT}    "Lynx/.*"       [OR]

RewriteCond %{HTTP_USER_AGENT}    "Mozilla/[1234].*"

RewriteRule ^foo\.html$           foo.dull.html  [L]
```

当收到对诸如 `http://hostname/foo.html` 这样的 URL 的请求时，第一个条件测试环境变量 `HTTP_USER_AGENT` 是否包含字符串 `Mozilla/5`。如果包含该字符串，则应用第一条规则。此规则将 `foo.cool.html` 替换为原始 URL，并完成所有重写；然而，当第一条规则未应用时，将调用第二条规则。有两个 OR 条件。换句话说，在应用此规则之前，这些条件中必须有一个匹配。

第一个条件测试环境变量中是否包含子串 `Lynx/`，第二个条件测试环境变量中是否包含子串 `Mozilla/1` 到 `Mozilla/4`。如果满足这些条件中的任何一个，则应用该规则。该规则用 `foo.dull.html` 替换原始 URL。替换后的 URL 会被转换为子请求，并由 Apache 按常规处理。

### 创建 HTML 到 CGI 网关

如果你想将静态页面 `foo.html` 无缝转换为动态变体 `foo.cgi`——也就是说，不通知浏览器或用户——方法如下：

```
RewriteRule ^foo\.html$ foo.cgi [T=application/x-http-cgi]
```

该规则将对 `foo.html` 的请求重写为对 `foo.cgi` 的请求。它还强制使用正确的 MIME 类型，以便作为 CGI 脚本运行。对 `http://hostname/foo.html` 这样的请求会在内部转换为对 CGI 脚本的请求。浏览器并不知道其请求已被重定向。

## 访问限制

这些示例涉及访问控制问题。在本节中，我将向你展示如何使用 URL 重写模块来控制对 Web 站点特定区域的访问。

### 屏蔽爬虫

屏蔽烦人的 Web 爬虫程序（也称为 robots）检索特定 Web 站点的页面很容易。你可能尝试过包含机器人排除协议（Robot Exclusion Protocol）条目的 `/robots.txt` 文件，但这通常不足以摆脱此类爬虫。一个示例解决方案是：

```
RewriteCond %{HTTP_USER_AGENT} ^NameOfBadRobot.*

RewriteCond %{REMOTE_ADDR} ^123\.45\.67\.[879]$

RewriteRule ^/not/to/be/indexed/by/robots/.+ - [F]
```

此规则有两个条件：

```
If (`HTTP_USER_AGENT of the robot matches a pattern "NameOfBadRobot"` ) and

(`REMOTE_ADDR of the requesting host is 123.45.67.8 to 123.45.67.9` ) then

    No substitution but send a HTTP "Forbidden" header (status code 403)

endif
```

如你所见，机器人的 `User-Agent` 标头已匹配，同时还检查了其使用的主机 IP 地址（`123.45.67.8` 和 `123.45.67.9`）。

## 创建基于 HTTP 推荐人的 URL 重定向器

你可以编写一个灵活的 URL 重定向器，使其作用于 Referrer HTTP 标头，并配置任意数量的推荐页面。方法如下：

```apache
RewriteMap  deflector txt:path/to/deflector.map

RewriteRule  ^/(.*)

  $1deflector:&(HTTP_REFERER)|/$1

RewriteRule .*DEFLECTED  &[HTTP_REFERER] [R,L]

RewriteRule .* - [PT]
```
