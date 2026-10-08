
```
$ curl -w "%{http_code} %{time_total} %{size_download}\
%{content_type}\
" http://www.example.net
<html><body>-它可以工作!</html>
<p>这是此服务器的默认网页。</p>
<p>Web 服务器软件正在运行，但尚未添加任何内容。</p>
</</body>></html>
200 0.014 177 text/html
```

## 使用 Telnet 测试 Web 服务器

虽然 `curl` 是一个在命令行中测试 Web 服务器的方便且简单的工具，但有时你可能需要在一个没有安装 `curl` 的主机上测试 Web 服务器，或者你可能只需要查看更底层的 HTTP 调用。无论哪种情况，这就是 `telnet` 派上用场。几乎任何 Linux 系统都安装了 `telnet`，而且只要你能从 Web 服务器获取大量的价值诊断数据。

要运行 `telnet`，请将要连接的主机作为参数，后面跟着端口 `80`，或者你的 Web 服务器监听的任何端口：

```
$ telnet www.example.net 80
Trying 10.1.2.5...
Connected to www.example.net.
Escape character is '^'
```

如果出于某种原因你无法连接，那么你需要回到本章最初的网络故障排除部分。一旦连接成功，你将输入一些基础的 HTTP 命令：

```
GET / HTTP/1.1
host: www.example.net
```

此示例使用了基本的 GET 请求（`GET /`），它请求站点的默认索引页，随后是你正在使用的 HTTP 协议（`HTTP/1.1`）。例如，如果你想测试 `/admin/inventory.cgi` 页面，你需要说 `GET /admin/inventory.cgi HTTP/1.1`。然后按回车键，并输入你想要连接的主机名（在 URL 中 `http://` 之后直接跟的内容）。这个主机参数非常重要，因为 Web 服务器通常在同一台机器上提供许多虚拟主机，因此如果你不指定使用哪个主机，可能无法获得你预期的网页。

一旦完成主机名的输入并按回车，你就应该会收到服务器的完整响应：

```
HTTP/1.1 200 OK
Date: Thu, 28 Jun 2012 03:56:32 GMT
Server: Apache/2.2.14 (Ubuntu)
Last-Modified: Mon, 24 May 2010 21:33:10 GMT
ETag: "38111c-bl-487dc9938880"
Accept-Ranges: bytes
Content-Length: 177
Vary: Accept-Encoding
Content-Type: text/html
X-Powered: avoid browser bug
```

```
<html><<body><h1>它可以工作！</h1>
<p>这是此服务器的默认网页。</p>
<p>Web 服务器软件正在运行，但尚未添加任何内容。</p>
</body></html>
```

一旦完成请求，按下 `Ctrl-]` 退出 `telnet`。默认情况下，相比于 `curl`，你可以从 `telnet` 获取到多得故障排除数据。在这个示例中，你可以看到 HTTP 状态码（`200 OK`）、请求日期以及页面最后修改日期、Web 服务器版本以及你在 Web 浏览器中通常看不到的其他数据。当然，缺点是，如果你想执行任何比简单 GET 请求复杂得多的操作，最好复习一下 HTTP 知识或切换回 `curl`，后者可以更轻松地处理重定向和其他复杂的设置。

## HTTP 状态码

当你排排除 Web 服务器问题时，Web 服务器返回的 HTTP 状态码是无价之宝。在前面的示例中，Web 服务器返回了状态码 `200`，这是当一切运行正常时你会看到的标准代码——`200 OK` 表示请求成功。还有许多其他状态码，每个状态码都有它们自己的数字分类；例如，所有以 `2` 开头的状态码都表示成功，所有以 `4` 开头的代码都表示客户端错误。本节将介绍每类状态码类别，并重点介绍你可能会遇到的一些常见代码。

### 1xx 信息状态码 (Informational Codes)

以 `1` 开头的状态码表示某种信息响应。此状态码范围适用于 `HTTP/1.1`，不应发送给 `HTTP/1.0` 客户端。以下是你将在该类中看到的主要响应：

- `100 Continue` 告诉客户端继续其其余部分的请求。
- `101 Switching Protocols` 表示服务器将响应客户端的请求，切换到更新后的 HTTP 版本。

### 2xx 成功状态码 (Successful Codes)

以 `2` 开头的状态码表示请求成功。理想情况下，如果你在排排除 Web 服务器问题，这些代码是你希望看到的响应类型。这些状态码中最常见的是 `200 OK`，表示请求成功。以下是你可能会看到的一些状态码：

- `200 OK`: 请求成功。
- `201 Created`: 你的请求成功并导致创建了新资源。
- `202 Accepted`: 你的请求已被接受进行处理；但它可能尚未完成。
- `203 Non-Authoritative Information`: 你的请求已被接受，但不是权威信息。
- `204 No Content`: 请求成功，但没有返回内容。
- `205 Reset Content`: 客户端重置发送器。
- `206 Partial Content`: 服务器满足了请求中的部分内容。

### 3xx 重定向状态码 (Redirection Codes)

当状态码以 `3` 开头时，表示请求需要进一步的操作。此状态码范围适用于 `HTTP/1.1`，不应发送给 `HTTP/1.0` 客户端。以下是你将在该类中看到的主要响应：

- `300 Multiple Choices`: 请求有多个选项可供客户端选择。
- `301 Moved Permanently`: 资源永久移动到新 URL。
- `302 Found`: 资源临时移动到新 URL。
- `303 See Other`: 应该从另一个 URI 获取响应。
- `304 Not Modified`: 资源未更改。
- `305 Use Proxy`: 客户端应通过代理访问资源。
- `307 Temporary Redirect`: 请求临时重定向。
- `308 Permanent Redirect`: 请求永久重定向。

### 4xx 客户端错误状态码 (Client Error Codes)

当你排排除服务器问题时，可能会遇到一些以 `4` 开头的错误代码。此状态码族处理服务器认为位于客户端的错误。这些错误中最常见的是 `404`，当客户端请求不存在的页面时返回。以下是该类中的常见代码：

- `400 Bad Request`: 客户端语法错误。
- `401 Unauthorized`: 请求需要用户身份验证，因此客户端应提供正确的身份验证。
- `403 Forbidden`: 与 `401` 不同，该请求不允许用户，客户端不应尝试重复。此错误代码通常指示权限问题。
- `404 Not Found`: 此错误通常发生在用户请求中有拼写错误、请求的页面没有重定向或文件曾存在但已删除时。
- `408 Request Timeout`: 客户端产生请求花费的时间过长。你在进行 Web 服务器故障排除时可能会遇到此问题。
- `405 Method Not Allowed`: 请求方法不被允许。
- `411 Length Too Large`: 请求实体长度过大。
- `412 Precondition Failed`: 客户端的先决条件不满足。
- `413 Payload Too Large`: 请求实体超过了服务器允许的限制。
- `415 Unsupported Media Type`: 请求的媒体类型不受服务器支持。
- `410 Gone`: 与 `3xx` 重定向请求不同，此代码用于资源曾经存在但现在永久消失。
- `429 Too Many Requests`: 客户端发送的请求过多。

### 5xx 服务器错误状态码 (Server Error Codes)

与 `4xx` 状态码类似，`5xx` 状态码也处理错误，只是在这种情况下，错误可能位于服务器端。如果你是 Web 服务器管理员并看到这些错误代码，你将需要深入研究 Web 服务器错误日志以获取有关原因的更多信息。以下是该类的一些示例代码：

- `500 Internal Server Error`: 服务器在处理请求时收到内部错误。当 CGI 或 PHP 脚本中存在导致文件运行出错的 Bug 时，可能会看到此错误。
- `501 Not Implemented`: 服务器不支持请求的功能。
- `502 Bad Gateway`: 当服务器配置为网关或代理设备且在连接上游服务器时收到无效响应时，会出现此错误。
- `503 Service Unavailable`: 服务器暂时无法提供客户端的服务，由于服务器过载或正在进行某些维护。
- `504 Gateway Timeout`: 服务器没有从需要以完成请求的上游服务器及时收到响应。

## 第 8 章 网站宕机了吗？追踪 Nginx 服务器问题

HTTP，但也可能是由于上游 FTP、LDAP 甚至 DNS 器的超时引起的。

- `505 HTTP 版本不支持`

不言而易懂；当服务器不支持客户端请求的 HTTP 版本时，就会使用此错误代码。

## 解析 Web 服务器日志

排查 Web 服务器问题的主要方法之一是通过日志。发送到 Web 服务器的每个请求都会以标准格式记录，这种格式初看起可能有些奇怪，但每一行都包含了许多用于排障的有用信息。Apache 和 Nginx 分别将日志存储在 `/var/log/apache2`（取决于你的发行版，可能是 `apache httpd`）和 `/var/log/nginx` 下的自定义目录下。两个 Web 服务器默认使用相似的日志格式，并将请求日志存储在 `access.log` 中，将错误存储在 `errors.log` 中。此外，大多数管理员会配置服务器，使得每个站点（虚拟主机）都有自己的日志，因此，访问日志最终可能是空的，而你的 `www.example.org.log` 则可能包含了你的大部分数据。

为了演示你可以从 Web 服务器日志中获取哪些信息，让我们看看在本章早期使用的 `curl` 命令并查看其响应日志：

```
$ curl -w "%{http_code}\n" http://www.example.net
<html><body>It works!</h1>
<p>这是该服务器的默认 Web 页面。</p>
<p>Web 服务器软件正在运行，但尚未添加任何内容。</p>
</body></html>
200
```

```
10.1.2.3 - [04/Jul/2012:12:08:05 -0700] GET /HTTP/1.1 "-" 200 303 - "curl/7.19.7"
```

```
(x86_64-linux-gnu) libcurl/7.19.7 OpenSSL/0.9.8k zlib/2.2.3.33/1.15
```

日志条目被分为若干个不同的字段，如果某个字段没有数据或不适用，它会被替换为 `-`。在这个例中，即使在不十分了解日志格式的情况下，我们可以得出几点重点。首先，请求来自 IP `10.1.2.3`。其次，我们可以识别出请求的时间戳。之后，我们可以看到被处理的精确 HTTP 请求（`GET / HTTP/1.1`），日志中随后的 `200` 对应 HTTP 返回码。最后，在日志的末尾是客户端传递给服务器的 User-Agent 字符串；在这种情况下，它标识了客户端。

注意：如果你像我一样是一个用户，可能习惯了打开任何文本文件，包括日志文件。遗憾的是，我们习惯于将任何文本文件的完整副本存储到临时空间（有时是 `/tmp`，有时在用户的家目录中）。虽然这种做法对于小文本文件没有问题，但 Web 服务器日志的大小可能会增长到 GB 级。我记不清有多少次去排查一个磁盘空间耗尽的 Web 服务器，结果发现是某人打开了一个几 GB 的 Web 日志文件并填满了 `/tmp` 目录。由于我们并不想编辑 Web 日志——只想查看它们——请使用像 `less` 这样的命令行工具来查看日志，而不是直接打开。

每个 Web 服务器都允许你自定义日志输出，以便获取有关每个请求的更多信息，Apache 配置文件中默认的日志格式如下：

```
LogFormat "%h %l %u \%r" %s %b "%{Referer}i" "%{User-Agent}i" combined
```

每个以 `%` 开头的符号都代表存储在日志中的某个值。这些选项的完整列表在 Apache 文档中，这里是这些字符串的描述：

- `%h`: 远程主机（主机名或 IP）
- `%l`: 远程日志名（除非开启了 IdentCheck，否则通常返回 -）
- `%u`: 远程用户（如果页面需要身份验证，否则返回 -）
- `%t`: 接收请求的时间
- `%r`: 请求的第一行
- `%s`: 状态码
- `%b`: 发送的字节数，包含头部头
- `%[Header]i`: 请求中指定头部的内容

由于大多数 Web 服务器日志都是标准格式，许多不同的工具可以解析并显示日志中的数据。这些软件对于获取统计和趋势非常有用；但在排查故障时，你通常只想提取特定 IP 或特定 URI 的数据。对于这一点，像 `grep` 和 `perl` 这样的命令行工具仍然是最好的工具，因为它们最可能存在于你登录的任何 Web 服务器上。

网上有很多从 Web 日志中提取数据的单行命令示例，但这里有几个你可以从这里开始构建的示例示例。首先是一个简单的 `grep` 命令，它将提取来自特定源 IP 的所有日志。在这个例中，我们将查找来自主机 `10.1.2.3` 的所有日志条目：

```
$ grep '^10.1.2.3' /var/log/apache2/access.log
...
10.1.2.3 - - [04/Jul/2012:12:04:05 -0700] "GET /HTTP/1.1" 200 303 "curl/7.19.7" - (x86_64-linux-gnu) libcurl/7.19.7 OpenSSL/0.9.8 zlib/1.2.33/1.15
```

或者，如果你想知道来自该 IP 的请求，可以将数据传递给 `wc -l`，它将统计输出的行数：

```
$ grep '^10.1.2.3' /var/log/apache2/access.log | wc -l
37
```

当然，如果你的日志文件包含多天的日志，你可能对某天的日志感兴趣：

```
$ grep '^10.1.2.3.*[04/Jul/2012' /var/log/apache2/access.log
```

或者该天某个小时的：

```
$ egrep '^10.1.2.3.*[04/Jul/2012' /var/log/apache2/access.log
```

使用 `perl`，你可以提取更多数据。例如，如果你发现那个单行命令难以解析，这里是正则表达式：

```bash
perl -ne 'print($1) if /(\d+\.\d+\.\d+\.\d+)/' /var/log/apache2/access.log
```

## 获取 Web 服务器统计信息

```
# 使用 URL：http://servername/server-status
# 取消注释并更改 ".example.com" 以允许
# 来自其他主机的访问
# #
<Location /server-status>
SetHandler server-status
Order deny,allow
Deny from all
Allow from localhost ip6-localhost
# Allow from .example.com
</Location>
```

请注意，在这个配置示例中，我们通过设置 `deny from all`（拒绝所有主机）并仅允许 `localhost`，真正锁定了访问该页面的人。这是一个安全的默认设置，因为你通常不希望他人查看此类调试信息。正如注释掉的示例所示，你可以添加额外的 `Allow from` 语句来添加允许查看页面的 IP 地址或主机。

对于 Nginx，你需要在现有的 Nginx 配置中添加如下的配置。在此示例中，Nginx 将仅监听在 `localhost`，但你可以将其更改为允许本地局网上的其他机器访问：

```
server {
listen 127.0.0.1:80;

location /nginx_status {
stub_status on;
access_log off;
allow 127.0.0.1;
deny all;
}
}
```

一旦设置好配置并重新加载了 Web 服务器，如果你允许某些远程 IP 查看该页面，请打开浏览器并访问 Web 服务器上的 `/server-status`。例如，如果你的 Web 服务器位于 `www.example.net`，你将加载 `http://www.example.net/server-status` 并看到如图 8-1 所示的页面。

## 第 8 章 网站宕机？排查 Web 服务器问题

### localhost 的 Apache 服务器状态

服务器版本: Apache/2.2.14 PHP/5.3.2-1ubuntu4 带 Soft-Patch

服务器构建: Mar 5 2012 16:42:17

当前时间: Wednesday, 04-Jul-2012 15:23:44 PDT

重启时间: 16-Jun-2012 22:52:21 PDT

服务器运行时间: 78 天 16 小时 31 分 23 秒

总访问量: 2542631 - 流量: 23.5 GB

CPU 使用率: 48.5% / 60.2% / 69.3% - 76.6% CPU 负载

384 请求/秒 - 18.1 Kb/秒 - 115.8 Mb/秒

正在处理 2 个请求，18 个空闲进程

- 等待连接 ("Keepalive"), "正在启动", "读取请求",

- 发送请求 ("Keepalive"), "DNS 查找",

- 关闭连接 ("日志记录"), "读取请求体",

- 空闲工作线程清理, 无空槽进程
