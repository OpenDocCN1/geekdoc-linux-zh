

使用它可以获取状态码、请求耗时、下载数据的大小以及内容类型：

```
$ curl -w "%{http_code} %{time_total} %{size_download} \\n%{content_type}" http://www.example.net
<html><body><h1>It works!</h1>
<p>This is the default web page for this server.</p>
<p>The web server software is running but no content has been added, yet.</p>
</body></html>
200 0.004 177 text/html
```

## 使用 Telnet 测试 Web 服务器

虽然 curl 是命令行下测试 Web 服务器的便捷且简单的工具，但有时你可能需要从一台未安装 curl 的主机测试 Web 服务器，或者你只是想查看底层的 HTTP 调用。在这些情况下，telnet 就派上用场了。几乎所有 Linux 系统都安装了 telnet，只要你了解一些基本的 HTTP 知识，就可以从 Web 服务器获取大量有价值的诊断数据。

首先，运行 telnet，将你要连接的主机作为参数传入，随后跟上端口 80，或者你的 Web 服务器监听的任何端口：

```
$ telnet www.example.net 80
Trying 10.1.2.5...
Connected to www.example.net.
Escape character is '^]'.
```

如果由于某种原因无法连接，那么你需要回到本章最初的网络故障排查部分。一旦连接成功，你将输入一些基本的 HTTP 请求：

```
GET / HTTP/1.1
host: www.example.net
```

这个示例使用了一个基本的 GET 请求（GET /），它请求该网站的默认索引页，后面跟着你正在使用的 HTTP 协议（HTTP/1.1）。如果你想测试 /admin/inventory.cgi 页面，例如，你会输入 GET /admin/inventory.cgi HTTP/1.1。然后按 Enter 键，并输入 host: 以及你要连接的主机名称（即在 URL 中 http:// 后面的部分）。这个 host 参数很重要，因为 Web 服务器通常在同一台机器上运行多个虚拟主机，如果你不指定想要的主机，可能无法获得预期的网页。

完成 host: 行后，按 Enter 键，你应该会从服务器获得完整的响应：

```
HTTP/1.1 200 OK
Date: Thu, 28 Jun 2012 03:56:32 GMT
Server: Apache/2.2.14 (Ubuntu)
Last-Modified: Mon, 24 May 2010 21:33:10 GMT
Etag: "38111c-b1-4875dc9938880"
Accept-Ranges: bytes
Content-Length: 177
Vary: Accept-Encoding
Content-Type: text/html
X-Pad: avoid browser bug

<html><body><h1>It works!</h1>
<p>This is the default web page for this server.</p>
<p>The web server software is running but no content has been added, yet.</p>
</body></html>
```

完成请求后，按 Ctrl-] 退出 telnet。默认情况下，通过 telnet 获得的故障排查数据比使用 curl 多得多。在这个示例中，你可以看到 HTTP 状态码（200 OK）、请求日期以及页面最后修改日期、Web 服务器及其版本，以及通常无法在 Web 浏览器中看到的其他数据。当然，缺点在于，如果你想执行比简单 GET 请求更复杂的操作，最好回顾一下你的 HTTP 知识，或者切换回 curl，因为它更容易处理重定向和其他复杂设置。

## HTTP 状态码

在排查 Web 服务器问题时，Web 服务器随每个请求返回的 HTTP 状态码极其宝贵。在之前的示例中，Web 服务器返回了状态码 200，这是你在一切正常运行时看到的标准代码——200 OK 表示请求已成功。还有许多其他状态码，各自属于不同的数字类别；例如，所有以 2 开头的状态码都表示成功，而以 4 开头的代码表示客户端错误。本节讨论每个状态码类别，并突出一些你可能会遇到的常见代码。

### 1xx 信息类代码

以 1 开头的状态码表示某种信息响应。此状态码范围用于 HTTP/1.1，不应发送给 HTTP/1.0 客户端。以下是该类中你会看到的两个主要响应：

- 100 Continue
  这告诉客户端继续其请求的其余部分。
- 101 Switching Protocol
  这表明服务器将响应客户端请求，切换到更新的 HTTP 版本。

### 2xx 成功代码

以 2 开头的状态码表示成功的请求。理想情况下，如果你在排查 Web 服务器问题，这是你希望看到的响应类型。这些状态码中最常见的是 200 OK，表示请求成功。以下是一些你可能看到的状态码：

- 200 Ok
  请求成功。
- 201 Created
  你的请求成功，并导致创建了一个新资源。
- 202 Accepted
  你的请求已被接受处理；但是，可能尚未处理完毕。
- 203 Non-Authoritative Information
  返回给你的信息并非来自原始来源，而是来自第三方，或是原始信息的子集。
- 204 No Content
  请求成功，但响应结果没有内容。
- 205 Reset Content
  客户端应重置文档视图。
- 206 Partial Content
  服务器满足了部分 GET 请求。

### 3xx 重定向代码

当状态码以 3 开头时，它表示从服务器到客户端的某种重定向消息。管理员经常使用这种响应，当他们将内容从一个 URL 移动到另一个 URL、将你从一个域名移动到另一个域名，甚至重定向你使用 HTTPS 而不是 HTTP 时。以下是该族中一些常见的状态码：

- 300 Multiple Choices
  来自服务器的回复将包含客户端可以选择重定向到的多个资源。
- 301 Moved Permanently
  当资源不再位于以前的 URI，而是已移动到新的资源时使用此代码。管理员使用此代码来指示客户端应将所有后续请求指向新的 URI。
- 302 Found
  与 301 状态不同，此代码表示资源只是暂时重定向。在未来，客户端仍应使用原始 URI。
- 303 See Other
  这通常是对 POST 请求的响应，其中响应可以通过对另一个 URI 的 GET 请求获取。
- 304 Not Modified
  当客户端发送基于文档已修改的 GET 请求时，使用此响应。此响应让客户端知道文档未发生变化。
- 305 Use Proxy
  服务器将在其响应 URI 中提供一个代理，必须遵循该代理才能访问请求的数据。
- 306 Unused
  状态码尚未使用。
- 307 Temporary Redirect
  这与 302 代码类似，当客户端请求的资源暂时可以在不同的 URI 下找到时使用，但在未来，客户端应使用原始 URI。

### 4xx 客户端错误代码

在排查服务器问题时，你可能会遇到一些以 4 开头的错误代码。此状态码族处理服务器认为在客户端侧的错误。其中最常见的是 404，当客户端请求一个不存在的页面时返回。以下是该类中一些常见的错误代码：

- 400 Bad Request
  此代码用于响应客户端侧的语法错误。
- 401 Unauthorized
  此请求需要用户身份验证，因此客户端应使用适当的身份验证重复请求。
- 403 Forbidden
  与 401 不同，此请求不被允许用户执行，且客户端不应尝试通过身份验证重复请求。此错误代码通常表明权限错误。
- 404 Not Found
  服务器找不到客户端请求的页面。此错误代码通常在用户请求中有拼写错误、请求指向已移动但未设置重定向的页面，或文件曾存在但已被删除时出现。
- 408 Request Timeout
  客户端花费太长时间生成请求。当你通过 telnet 进行 Web 服务器故障排查实验时，可能会看到此情况。
- 410 Gone
  与 3xx 重定向请求不同，当资源曾存在但现在永远消失时使用此代码。

### 5xx 服务器错误代码

与 4xx 状态码类似，5xx 状态码处理错误，但在这种情况下，错误可能位于服务器端。如果你是 Web 服务器管理员并看到这类错误代码，你需要深入查看 Web 服务器错误日志以获取有关错误原因的更多信息。以下是该类的一些示例代码：

- 500 Internal Server Error
  服务器在处理请求时收到内部错误。当你的 CGI 或 PHP 脚本中存在 bug，导致文件在运行时出错时，你可能会看到这种情况。
- 501 Not Implemented
  服务器不支持客户端请求的功能。
- 502 Bad Gateway
  当服务器配置为网关或代理设备，并且在联系其上游服务器时收到无效响应时，会出现此错误。
- 503 Service Unavailable
  服务器暂时无法提供客户端请求的服务，通常是由于服务器过载或正在对服务器进行某种维护。
- 504 Gateway Timeout
  服务器未能及时从其需要以满足请求的某个上游服务器处收到响应。上游服务器可能

