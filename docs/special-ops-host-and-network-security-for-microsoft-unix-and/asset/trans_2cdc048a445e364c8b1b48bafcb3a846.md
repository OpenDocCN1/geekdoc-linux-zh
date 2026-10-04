

# WebDAV 默认启用

Web 分布式授权与版本（WebDAV）协议本质上是将超文本传输协议（HTTP）或 Web 转换为文件系统。用户可以上传、编辑和删除文件。OracleAS 默认启用 WebDAV。这意味着未经身份验证的用户可以向 Web 服务器上传任意文件。通过 telnet 连接到 Web 服务器端口，并使用 `PUT` 方法创建文件，可以轻松地将 Oracle Web 服务器变成恶意软件站点：

```
PUT /dav_public/foo.jsp HTTP/1.1
Host: oraclewebserver
Content-Type: text/plain
Content-Length: 10
AAAAAAAAAA
```

为了防止这种情况，请关闭 WebDAV。要执行此操作，请编辑 `midday.conf` 文件并将条目“DAV on”更改为“DAV off”。完成后，停止并重启 Web 服务器。管理员通过检查 Web 服务器的访问日志中的 `PUT` 请求方法，可以判断该站点是否被滥用。

# WebDAV 模块中的格式字符串漏洞

`COPY` 和 `MOVE` 请求方法包含格式字符串漏洞，该漏洞允许攻击者控制 Apache 进程的执行路径。例如，通过 telnet 进入 Web 服务器进程并发送以下内容，攻击者可以导致 Web 服务器崩溃：

```
COPY /dav_public/foo.jsp HTTP/1.1
Host: oraclewebserver
Destination: %AAAA%x%x%x%n@n@n@n/foo
```

格式字符串漏洞发生的原因是目标统一资源标识符（URI）指向不同的服务器，而在构建错误消息并写入 `error_log` 文件时，触发了格式字符串漏洞。通过提供特殊的格式字符串，可能会控制远程服务器。如果已关闭 WebDAV，则不会出现此问题。

# 从 Oracle Application Server 调用 PL/SQL

PL/SQL 是 Oracle 对结构化查询语言（SQL）的过程语言扩展。PL/SQL 程序包本质上是数据库中的存储过程。程序包暴露了可以直接调用的过程，也包含从另一个包内部调用的函数。Apache 的 PL/SQL 模块扩展了 Web 服务器的功能，允许 Web 服务器执行数据库中的这些存储 PL/SQL 程序包。想象 PL/SQL 模块的最佳方式是将其作为一个通过 Web 使用存储过程进入 Oracle 数据库服务器的网关。默认情况下，所有以 `/pls` 开头的 Web 服务器请求都会被发送到 PL/SQL 模块进行调度。客户端请求 URI 将包含数据库访问描述符（DAD）名称、数据库服务器中的 PL/SQL 程序包名称以及正在访问的过程名称。任何需要传递给过程的参数都在查询字符串中：

```
http://oracleserver/pls/bookstore/books.search?name=Special+Ops
```

此 URL 的 DAD 为 `bookstore`，名为 `books` 的 PL/SQL 程序包以及 `search` 过程，它接受一个参数 `name`（即要搜索的书名）。DAD 描述了 `wdbsvr.app` 文件中的一个部分，描述了 Apache 如何连接到数据库服务器，并包含了用于验证的 UserID 和密码等细节。如果没有提供凭据，请求将导致 Web 客户端提示凭据。连接到数据库服务器后，数据库将加载 `books` 程序包并执行 `search`过程；搜索结果将返回给 Web 服务器，然后由其传递给请求客户端。

# PL/SQL 模块中的格式字符串漏洞

如果攻击者向 Web 服务器请求不存在的程序包和/或过程，数据库服务器将返回消息：

```
XXXX: PROCEDURE DOES NOT EXIST
```

问题在于，该消息随后被作为格式字符串传递给 `_sprintf()` 函数。不用说，通过攻击者提供的格式字符串向 Web 服务器发送请求，可能会控制 Apache 服务器。例如，URL `http://oraclewebserver/pls/%25x%25x%25x%25n%25n%25n.foo` 将导致 Web 服务器崩溃。由于这是来自堆而不是栈，可能通过创建特殊的格式字符串来控制远程服务器。如果已关闭 WebDAV，则不会出现此问题。

