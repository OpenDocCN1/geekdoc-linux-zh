
这两个十六进制数字构成的值可以映射到 ASCII（针对英语）表中以获取对应的字符。例如，`%20`（十六进制）是 32（十进制），并映射为 ASCII 表中的空格字符。

## Apache CGI 变量

Apache 有两种方式可以实现对 CGI 的支持。标准的 Apache 发行版包含一个 CGI 模块，用于实现传统的 CGI 支持；然而，有一个新的模块（`FastCGI`）实现了对高性能 CGI 应用程序的支持。本节讨论标准 CGI 支持问题。

在之前的章节中，你了解到符合 CGI 标准的 Web 服务器使用环境变量、标准输入（`STDIN`）和标准输出（`STDOUT`）来向 CGI 程序传输信息并从其获取信息。Apache 为 CGI 程序开发人员提供了一套灵活的环境变量。使用这些环境变量，CGI 程序不仅可以检索输入数据，还可以识别它所处理的客户端和服务器的类型。

在以下各节中，我将讨论从编译到 Apache 中的标准 CGI 模块中可用的环境变量。

> **注意**
> Apache `2.xx` 源码发行版支持 `configure` 脚本的 `--enable-cgid` 选项。此选项强制 Apache 使用脚本服务器（称为 CGI 守护进程）来管理 CGI 脚本进程，从而增强 Apache 的整体性能。

### 服务器变量

这些变量由 Apache 设置，以告知 CGI 程序关于 Apache 的信息。使用服务器变量，CGI 程序可以确定各种服务器特定的信息，例如 Apache 软件的版本、管理员的电子邮件地址等。

#### `SERVER_SOFTWARE`

`SERVER_SOFTWARE` 由 Apache 设置，其值通常具有以下形式：

```
Apache/Version (OS Info)
```

这里，Apache 是运行 CGI 程序的服务器软件名称，`Version` 是 Apache 的版本号。一个示例值如下：

```
Apache/2.0.14 (Unix)
```

当 CGI 程序需要利用新版本 Apache 中的新功能，同时仍需在旧版本上正常运行时，这很有用。

`GATEWAY_INTERFACE` 告诉 CGI 程序服务器当前支持哪个版本的 CGI 规范。一个示例值如下：

```
CGI/1.1
```

CGI 程序可以确定此变量的值，并根据不同版本的 CGI 规范中可用的不同功能进行条件性使用。例如，如果值是 `CGI/1.0`，程序可能不会使用任何 `CGI/1.1` 功能，反之亦然。

小数点前的第一个整数称为主要版本号，小数点后的整数称为次要版本号。由于这两个整数被视为独立的数字，`CGI/2.2` 是比 `CGI/2.15` 更旧的版本。

#### `SERVER_ADMIN`

如果你使用 `httpd.conf` 文件中的 `ServerAdmin` 指令设置站点管理员的电子邮件地址，此变量将设置为反映该值。此外，请注意，如果在虚拟主机配置容器中有 `ServerAdmin` 指令，并且被访问的 CGI 程序属于该虚拟主机，则 `SERVER_ADMIN` 变量将设置为该地址。

#### `DOCUMENT_ROOT`

此变量设置为被访问的 Web 站点的 `DocumentRoot` 指令的值。

### 客户端请求变量

Apache 从请求 CGI 程序的客户端接收的 HTTP 请求头中创建一组环境变量。它通过创建以下一组环境变量向 CGI 程序提供此信息。

#### `SERVER_NAME`

此变量告知 CGI 程序正在访问哪个主机。其值是一个 IP 地址或完全限定主机名，如下所示：

```
SERVER_NAME = 192.168.1.100
SERVER_NAME = www.domain.com
```

#### `HTTP_HOST`

参见 `SERVER_NAME` 变量。

#### `HTTP_ACCEPT`

此变量设置为客户端能够接受的 MIME 类型列表，包括以下类型：

```
HTTP_ACCEPT = image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, image/png, */*
```

在这里，客户端声称能够处理 GIF、JPEG、PNG 和其他图像。这使得 CGI 程序能够确定什么样的输出对客户端最理想。例如，CGI 程序可以生成 GIF 或 JPEG，并收到如下的 `HTTP_ACCEPT`：

```
HTTP_ACCEPT = image/gif, */*
```

然后，因为客户端更偏好 GIF 而非 JPEG，它可以发送 GIF 输出而不是 JPEG。

#### `HTTP_ACCEPT_CHARSET`

此变量指定客户端可接受的字符集，例如：

```
HTTP_ACCEPT_CHARSET = iso-8859-1,*,utf-8
```

#### `HTTP_ACCEPT_ENCODING`

此变量指定客户端可接受的编码方案，例如：

```
HTTP_ACCEPT_ENCODING = gzip
```

在这种情况下，客户端接受 `gzip`（压缩）文件。因此，CGI 脚本可以使用 `gzip` 压缩来压缩大型页面并发送它，Web 客户端能够对其进行解压缩。

#### `HTTP_ACCEPT_LANGUAGE`

此变量指定客户端可接受的语言，例如：

```
HTTP_ACCEPT_LANGUAGE = en
```

在这种情况下，客户端接受 `en`（英语）语言内容。

#### `HTTP_USER_AGENT`

此变量指定请求系统正在运行的客户端软件以及其运行的操作系统，例如：

```
HTTP_USER_AGENT = Mozilla/4.04 [en] (WinNT; I)
```

上述内容等同于以下内容：

```
Client Software = Netscape Navigator ()
Client Software Version = 4.04 (English version)
Operating System = Windows NT (Intel)
```

请注意，`Mozilla` 是 `Netscape` 用于 `Navigator` 代码库的关键字。虽然最初只有 `Netscape` 浏览器使用“`Mozilla`”这个词，但许多其他供应商已开始使用 `Mozilla` 作为 HTTP 头的一部分。例如，从同一台机器运行时，`Microsoft Internet Explorer` (`IE`) 5.5 会产生如下的 `HTTP_USER_AGENT` 数据：

```
HTTP_USER_AGENT = Mozilla/5.5 (compatible; MSIE 5.5; Windows NT)
```

许多 Web 站点大量使用此用户代理信息。一个为 `Netscape Navigator` 优化的站点（即，它使用在 `Netscape Navigator` 中运行良好的 `HTML`、`JavaScript` 或插件功能）可能会使用 `HTTP_USER_AGENT` 信息为使用 `IE` 或其他不太流行的浏览器访问该站点的用户返回不同的页面。然而，我建议你坚持使用标准 `HTML`（当前标准 `HTML` 规范可在 `www.w3.org` 获取），并且完全不实现浏览器特定的功能。虽然为你的页面针对单一浏览器进行优化可能使其在该浏览器中看起来很酷，但并不是每个人都使用该特定浏览器。这意味着你的浏览器特定的 `HTML` 标签或插件可能会使其他人（不使用你首选浏览器的人）访问你的 Web 站点变得更加困难。

#### `HTTP_REFERER`

此变量设置为将请求转发到被调用的 CGI 程序的统一资源标识符（URI）。通过使用此变量，你可以判断请求是来自你的某个 Web 页面上的链接，还是来自远程 URL。请注意，变量名的拼写错误是不幸的，经常让正确拼写该变量但在应用程序和脚本中发现其无法工作的 CGI 开发者感到困惑。因此，如果你计划使用此变量，请按照此处所述的拼写方式进行拼写。

### `HTTP_CONNECTION`

`HTTP_CONNECTION` 变量设置为客户端和服务器正在使用的连接类型。例如：

```
HTTP_CONNECTION = Keep-Alive
```

这表示客户端能够处理使用 `Keep-Alive` 的持久连接，并且当前正在使用它。

### `SERVER_PORT`

`SERVER_PORT` 变量的值告诉 CGI 程序当前正在使用哪个服务器端口来访问该程序。一个示例如下：

```
SERVER_PORT = 80
```

如果 CGI 程序创建了指向服务器的 URL，将端口地址（即此变量的值）包含在 URL 中可能很有用。

### `REMOTE_HOST`

`REMOTE_HOST` 变量告诉 CGI 程序客户端的 IP 地址或 IP 名称，如下所示：

```
REMOTE_HOST = dsl-666.isp24by7.net
```

请注意，如果 Apache 服务器是使用 `MINIMAL_DNS` 选项编译的，则此变量不会被设置。

### `REMOTE_PORT`

此端口号用于套接字连接的客户端一侧：

```
