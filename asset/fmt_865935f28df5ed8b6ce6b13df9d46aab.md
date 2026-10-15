
```
LOG[28843:1024]: SSLv3 write change cipher spec A
LOG[28843:1024]: SSLv3 write finished A
LOG[28843:1024]: SSLv3 flush data
LOG[28843:1024]: SSLv3 read finished A
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: 1 items in the session cache
LOG[28843:1024]: 1 client connects (SSL_connect())
LOG[28843:1024]: 1 client connects that finished
LOG[28843:1024]: 0 renegotiations requested
LOG[28843:1024]: 0 server connections (SSL_accept())
LOG[28843:1024]: 0 server connects that finished
LOG[28843:1024]: 0 renegotiations requested
LOG[28843:1024]: 0 session cache hits
LOG[28843:1024]: 0 session cache misses
LOG[28843:1024]: 0 session cache timeouts
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: www.example.com.443 opened with SSLv3,
cipher DES-CBC3-SHA (168 bits)
HEAD /HTTP/1.0

HTTP/1.1 200 OK
Server: Apache/1.3.14 (Unix) mod_perl/1.24_01
Date: Mon, 18 Dec 2000 15:53:08 GMT
Content-length: 152
Content-type: text/html
Connection: close
```

# Linux 破解深度揭秘：Linux 安全秘密

- Apache 是开源的。
- Apache 是免费的。

查看 Netcraft 调查，了解 Apache 较于其他 Web 服务器的流行程度：`http://www.netcraft.com/survey/`

除了这些原因外，Apache 也相对安全。它虽然有安全漏洞的记录，但当这些漏洞被发现时，互联网上几乎就能提供补丁。这与许多其他 Web 服务器，尤其是专有 Web 服务器不同，后者修复安全漏洞的速度很慢。

大多数 Linux 发行版都带了 Apache，如果你使用的是较新版本的 Linux，很可能 Apache 已经安装并运行。你可以通过检查处理器状态来查看它是否正在运行：

```
machine$ ps -ef grep httpd
root      3978 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3979 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3980 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3981 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3982 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3983 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3984 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3985 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3988 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3989 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
```

注意 Apache 程序被称为 `httpd`，即 HTTP 守护进程。存在多个 `httpd` 副本，这确保了可以同时处理多个连接。（任何时刻运行的进程数量是可配置的。）最后，请注意用户 `nobody` 拥有除了第一个的它之外的所有进程。`nobody` 用户是处理 HTTP 请求的普通用户（尽管这也可以进行配置）。

> 这里的核心思想是，Web 服务器不应该以 root 身份运行。如果由 root 运行 `httpd`，Web 服务器将拥有仅 root 可访问文件的权限，且 Web 服务器执行的 CGI 程序也将以 root 身份运行。这使得黑客有可能操纵 CGI 程序并以 root 身份执行操作。（参见后文对 CGI 编程问题的讨论。）

如果你发现 `httpd` 运行在你的机器上，只需将浏览器指向 `localhost`：

```
http://localhost/
```

你理应看到 Apache 的欢迎页面。

> 可以在 `http://www.apache.org` 找到最新版本的 Apache。

# Apache 配置

如上文所述，Apache Web 服务器相对安全，但我们需要讨论安全配置它的方法。Apache 的配置文件通常是 `httpd.conf`。该文件包含许多指令，告诉 Apache 如何运行。

> 注意：Apache 过去使用过三个配置文件：`httpd.conf`、`access.conf` 和 `srm.conf`，但这三个文件已经合并到单个文件 `httpd.conf` 中。

Apache 必须由 `root` 启动，因为它绑定到 80 端口，但一旦启动，它就有更改运行用户的能力。通常使用 `nobody` 用户来运行 `http`，尽管可以使用任何用户。（创建一个新用户，例如 `web`，其唯一目的是拥有 `http` 进程，这并不常见。）除了指定由哪个用户拥有 `http` 进程外，还应该配置所使用的组。`httpd.conf` 中的以下几行配置了用户和组：

```
User nobody
Group nobody
```

> 注意：端口 80 是默认的 HTTP 端口，但 Web 服务器可以绑定到任何端口。常见的例子有 8080 和 8888。

# 危险的符号链接

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 9 |
| 影响 | 5 |
| 风险等级 | 8 |

允许 Web 服务器跟随符号链接是一个潜在的安全风险。Web 服务器的设计初衷是只提供存在于 Web 文档树内的文档。该文档树的根通常位于 `/usr/local/apache/htdocs`（按照惯例，这可以在 `httpd.conf` 中进行配置）。当使用此 URL 请求根文档时：

```
http://localhost/
```

所提供的文件通常是 `index.html`，它位于 `httpdocs` 根目录内。限制 Web 服务器仅访问文档树内的文件是最安全的策略，但可以将服务器配置为允许访问文档树之外的符号链接。如果服务器允许符号链接，可能会出现以下场景：用户在她的 html 目录中放置一个指向 `/etc` 的符号链接。我们称该链接为

# Linux 破解深度揭秘：Linux 安全秘密与解决方案

`link_to_etc`。有一次，以下请求为黑客提供了信息，让他获取了一份 `/etc/passwd` 副本：

```
http://localhost/
```

# 安全地配置符号链接

允许符号链接并不完全是一个坏主意。然而，必须仔细考虑何时以及如何允许符号链接。为了说明这一点，假设一个开发者想要共享位于 `/etc` 的目录。他们在文档根目录下创建一个指向 `/etc` 的符号链接。我们称该链接为 `link_to_etc`。
