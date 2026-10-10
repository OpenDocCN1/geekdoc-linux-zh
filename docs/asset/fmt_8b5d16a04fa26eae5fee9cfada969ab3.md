
这告诉服务器执行 `/cgi-bin/search.cgi` CGI 程序，并将 `books=cgi` 和 `author=kabir` 输入数据传递给它。

当 Apache 等符合 CGI 规范的 Web 服务器收到此类请求时，它遵循 CGI 规范并将输入数据传递给应用程序（在这种情况下，是 `cgi-bin` 目录中的 `search.cgi`）。当通过 HTTP GET 请求方法请求 CGI 资源时，Apache：

- 为 CGI 程序设置环境变量，这包括将 HTTP 请求方法名称存储在名为 `REQUEST_METHOD` 的环境变量中，并将从客户端接收到的数据存储在名为 `QUERY_STRING` 的环境变量中。
- 执行请求的 CGI 程序。
- 等待程序完成并返回输出。
- 如果它不是非解析头程序，则解析 CGI 程序的输出。（*非解析头 CGI 程序创建自己的 HTTP 头，因此服务器无需解析头。*）
- 创建必要的 HTTP 头。
- 将程序的头和输出发送到请求的客户端。

图 12-2 说明了这个过程。

现在让我们看看 CGI 程序必须做什么才能检索输入并将其用于内部目的。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_354_0.png)

**图 12-2：** CGI 服务器处理。

如图 12-3 所示，一个 CGI 程序

- 读取 `REQUEST_METHOD` 环境变量。
- 通过使用存储在 `REQUEST_METHOD` 变量中的值来确定是否使用了 `GET` 方法。
- 如果使用 `GET` 方法，则检索存储在 `QUERY_STRING` 环境变量中的数据。
- 解码数据。
- 按自己的意愿处理解码后的数据。
- 处理完成后，将输出的 `Content-Type` 写入其标准输出设备（`STDOUT`）。
- 将输出数据写入 `STDOUT` 并退出。

Web 服务器读取应用程序的 `STDOUT` 并解析它以定位输出的 `Content-Type`。然后，它在将输出传输到客户端之前传输适当的 HTTP 头和 `Content-Type`。CGI 程序退出，整个 CGI 事务完成。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_355_0.png)

图 12-3：CGI 程序处理。

> 如果 CGI 程序需要自己提供所有必要的 HTTP 头和 `Content-Type` 信息，其名称必须以 `nph` 为前缀（代表 nonparsed header，即非解析头）。`nph` CGI 程序的输出不会被服务器解析，而是直接传输给客户端；大多数 CGI 程序让服务器编写 HTTP 头，因此是解析头程序。

使用 `GET` 请求方法将输入数据传递给 CGI 程序在许多方面都有限制，包括以下方式：

- 作为 URL 一部分传输的数据总大小受客户端的 URL 长度限制。许多流行的 Web 浏览器对 URL 的长度有硬性限制，因此，通过编码 URL 可以发送的总数据量相当有限。然而，偶尔通过 URL 向 CGI 程序传递数据可能是一个好主意。例如，如果你有一个使用 `GET` 方法将数据发送到 CGI 程序的 HTML 表单，提交的 URL 可以被书签以便稍后使用，而无需再次通过数据输入表单。这对数据库查询应用程序来说是一个用户友好的功能。

- 单个环境变量（`QUERY_STRING`）的值长度是有限的。许多甚至所有操作系统都限制环境变量值可以包含的字节数。这实际上限制了可以存储为输入数据的总字节数。

这些限制对于需要极少或不需要用户输入的 CGI 程序可能无关紧要。然而，对于需要大量用户输入数据的程序，另一种 HTTP 请求方法——POST——更适用。POST 请求方法将在下一节中讨论。

### POST 请求

HTTP POST 请求方法广泛用于向 CGI 程序传递数据。此方法的典型用途可以在你在网络上填写的许多 HTML 表单中找到。例如，清单 12-1 显示了这样一个表单。

#### 清单 12-1：使用 HTTP POST 请求方法的 HTML 表单

```html
<HTML>
<HEAD>
<TITLE> Apache Server 2.0 - Chapter 12 Listing 12-1</TITLE>
</HEAD>
<BODY>
<H1>Listing 12-1</H1>
<H2>An Example HTML Form Using the HTTP POST Request Method</H2>
<HR>
<FORM ACTION="/cgi-bin/search.cgi" METHOD="POST">
<PRE>
Type of Book <INPUT TYPE="TEXT" NAME="book" SIZE="10" MAXSIZE="20">
Author's Name <INPUT TYPE="TEXT" NAME="author" SIZE="10" MAXSIZE="20">
</PRE>
<INPUT TYPE=SUBMIT VALUE="Search Now">
</FORM>
</BODY>
</HTML>
```

请注意，清单中有一个 `<FORM> </FORM>` 部分。HTML 表单通常有一个起始的 `<FORM>` 标签，它定义表单的 `ACTION` 和请求 `METHOD`。在上例中，动作是 `/cgi-bin/search.cgi` CGI 程序，方法是 POST。

在起始的 `<FORM>` 标签之后，通常有一个或多个 `INPUT` 实体；`INPUT` 实体可能包括文本输入框、下拉菜单和列表。在我们的例子中，有三个输入实体。第一个允许用户为 `book` 变量输入值。下一个类似，允许用户为 `author` 变量输入值。第三个有点特殊；它允许用户提交表单。当用户提交表单时，客户端软件向 `ACTION`（即 `/cgi-bin/search.cgi`）资源发送 POST 请求到服务器，并且以编码格式传输 `book=<用户输入的值>` 和 `author=<用户输入的值>`。

## 比较 GET 和 POST

GET 和 POST 请求有什么区别？POST 数据不会存储在 CGI 程序的 `QUERY_STRING` 环境变量中。相反，它存储在 CGI 程序的标准输入（`STDIN`）中。`REQUEST_METHOD` 变量被设置为 POST，而编码数据存储在 CGI 程序的 `STDIN` 中，并且一个新名为 `CONTENT_LENGTH` 的环境变量被设置为存储在 `STDIN` 中的字节数。

现在，CGI 程序必须检查 `REQUEST_METHOD` 环境变量的值。如果对于 HTTP POST 请求它被设置为 POST，程序应首先从 `CONTENT_LENGTH` 环境变量的值确定输入数据的大小，然后从 `STDIN` 读取数据。请注意，Web 服务器不负责在 `STDIN` 中插入文件结束（EOF）标记，这就是为什么将 `CONTENT_LENGTH` 变量设置为数据长度（以字节为单位），这使得 CGI 程序更容易确定数据的总字节数。

可以同时使用 GET 和 POST。下面是一个示例 HTML 表单，它正式使用 POST 方法，但也悄悄地将查询字符串 `username=joe` 作为 CGI `ACTION` 的一部分混入其中。

```html
<FORM ACTION="/cgi-bin/edit.cgi?username=joe" METHOD=POST>
<input TYPE=TEXT NAME="PhoneNumber"> 
</FORM>
```

在这个示例中，`username=joe` 查询将是 URL 的一部分，但其他字段（`PhoneNumber`）将是 POST 数据的一部分。效果：最终用户可以书签该 URL，并始终作为 `joe` 运行 `edit.cgi` 脚本，而无需为任何其他字段设置值。这对于在线数据库应用程序和搜索引擎非常有用。

无论你使用 GET 还是 POST，或者两者兼用，数据都会被编码，解码它取决于 CGI 程序。下一节讨论解码编码数据所涉及的步骤。

## 解码输入数据

原始 HTTP 协议的设计者计划让该协议在任何系统上都能轻松实现。此外，他们还使数据编码方案变得简单。

该方案将某些字符定义为特殊字符。例如，等号（`=`）有助于创建键值对；加号（`+`）替代空格字符，而和号字符（`&`）用于分隔两个键值对。

如果数据本身包含具有特殊含义的字符，你可能会疑惑传输的是什么。在这种情况下，会使用一种三字符编码方案，它可以编码任何字符。百分号（`%`）表示一个由两个十六进制数字组成的编码字符序列的开始。

十六进制是一种基数为 16 的计数系统，其中 0 到 9 与十进制中的 0 到 9 代表相同的值，但它还有一组额外的数字。这些数字是 `A`（=10）、`B`（=11）、`C`（=12）、`D`（=13）、`E`（=14）和 `F`（=15）。例如，十六进制的 20 等于十进制的 32。转换方案如下：

```
20 = 2 x (16^1) + 0 x (16^0)
```

这两个十六进制数字构成的值可以映射到 ASCII（针对英语）表中以获取对应的字符。例如，`%20`（十六进制）是 32（十进制），并映射为 ASCII 表中的空格字符。

## Apache CGI 变量

Apache 有两种方式可以实现对 CGI 的支持。标准的 Apache 发行版包含一个 CGI 模块，用于实现传统的 CGI 支持；然而，有一个新的模块（FastCGI）实现了对高性能 CGI 应用程序的支持。本节讨论标准 CGI 支持问题。

在之前的章节中，你了解到符合 CGI 标准的 Web 服务器使用环境变量、标准输入（`STDIN`）和标准输出（`STDOUT`）来向 CGI 程序传输信息并从其获取信息。Apache 为 CGI 程序开发人员提供了一套灵活的环境变量。使用这些环境变量，CGI 程序不仅可以检索输入数据，还可以识别它所处理的客户端和服务器的类型。

在以下各节中，我将讨论从编译到 Apache 中的标准 CGI 模块中可用的环境变量。

> **注意**
> Apache 2.xx 源码发行版支持 `configure` 脚本的 `--enable-cgid` 选项。此选项强制 Apache 使用脚本服务器（称为 CGI 守护进程）来管理 CGI 脚本进程，从而增强 Apache 的整体性能。

### 服务器变量

这些变量由 Apache 设置，以告知 CGI 程序关于 Apache 的信息。使用服务器变量，CGI 程序可以确定各种服务器特定的信息，例如 Apache 软件的版本、管理员的电子邮件地址等。

#### **SERVER_SOFTWARE**

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

#### **SERVER_ADMIN**

如果你使用 `httpd.conf` 文件中的 `ServerAdmin` 指令设置站点管理员的电子邮件地址，此变量将设置为反映该值。此外，请注意，如果在虚拟主机配置容器中有 `ServerAdmin` 指令，并且被访问的 CGI 程序属于该虚拟主机，则 `SERVER_ADMIN` 变量将设置为该地址。

#### **DOCUMENT_ROOT**

此变量设置为被访问的 Web 站点的 `DocumentRoot` 指令的值。

### 客户端请求变量

Apache 从请求 CGI 程序的客户端接收的 HTTP 请求头中创建一组环境变量。它通过创建以下一组环境变量向 CGI 程序提供此信息。

#### **SERVER_NAME**

此变量告知 CGI 程序正在访问哪个主机。其值是一个 IP 地址或完全限定主机名，如下所示：

```
SERVER_NAME = 192.168.1.100
SERVER_NAME = www.domain.com
```

#### **HTTP_HOST**

参见 `SERVER_NAME` 变量。

#### **HTTP_ACCEPT**

此变量设置为客户端能够接受的 MIME 类型列表，包括以下类型：

```
HTTP_ACCEPT = image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, image/png, */*
```

在这里，客户端声称能够处理 GIF、JPEG、PNG 和其他图像。这使得 CGI 程序能够确定什么样的输出对客户端最理想。例如，CGI 程序可以生成 GIF 或 JPEG，并收到如下的 `HTTP_ACCEPT`：

```
HTTP_ACCEPT = image/gif, */*
```

然后，因为客户端更偏好 GIF 而非 JPEG，它可以发送 GIF 输出而不是 JPEG。

#### **HTTP_ACCEPT_CHARSET**

此变量指定客户端可接受的字符集，例如：

```
HTTP_ACCEPT_CHARSET = iso-8859-1,*,utf-8
```

#### **HTTP_ACCEPT_ENCODING**

此变量指定客户端可接受的编码方案，例如：

```
HTTP_ACCEPT_ENCODING = gzip
```

在这种情况下，客户端接受 `gzip`（压缩）文件。因此，CGI 脚本可以使用 `gzip` 压缩来压缩大型页面并发送它，Web 客户端能够对其进行解压缩。

#### **HTTP_ACCEPT_LANGUAGE**

此变量指定客户端可接受的语言，例如：

```
HTTP_ACCEPT_LANGUAGE = en
```

在这种情况下，客户端接受 `en`（英语）语言内容。

#### **HTTP_USER_AGENT**

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

请注意，`Mozilla` 是 `Netscape` 用于 `Navigator` 代码库的关键字。虽然最初只有 Netscape 浏览器使用“Mozilla”这个词，但许多其他供应商已开始使用 `Mozilla` 作为 HTTP 头的一部分。例如，从同一台机器运行时，`Microsoft Internet Explorer (IE) 5.5` 会产生如下的 `HTTP_USER_AGENT` 数据：

```
HTTP_USER_AGENT = Mozilla/5.5 (compatible; MSIE 5.5; Windows NT)
```

许多 Web 站点大量使用此用户代理信息。一个为 Netscape Navigator 优化的站点（即，它使用在 Netscape Navigator 中运行良好的 HTML、JavaScript 或插件功能）可能会使用 `HTTP_USER_AGENT` 信息为使用 IE 或其他不太流行的浏览器访问该站点的用户返回不同的页面。然而，我建议你坚持使用标准 HTML（当前标准 HTML 规范可在 `www.w3.org` 获取），并且完全不实现浏览器特定的功能。虽然为你的页面针对单一浏览器进行优化可能使其在该浏览器中看起来很酷，但并不是每个人都使用该特定浏览器。这意味着你的浏览器特定的 HTML 标签或插件可能会使其他人（不使用你首选浏览器的人）访问你的 Web 站点变得更加困难。

#### **HTTP_REFERER**

此变量设置为将请求转发到被调用的 CGI 程序的统一资源标识符（URI）。通过使用此变量，你可以判断请求是来自你的某个 Web 页面上的链接，还是来自远程 URL。请注意，变量名的拼写错误是不幸的，经常让正确拼写该变量但在应用程序和脚本中发现其无法工作的 CGI 开发者感到困惑。因此，如果你计划使用此变量，请按照此处所述的拼写方式进行拼写。

## HTTP_CONNECTION

`HTTP_CONNECTION` 变量设置为客户端和服务器正在使用的连接类型。例如：

```
HTTP_CONNECTION = Keep-Alive
```

这表示客户端能够处理使用 `Keep-Alive` 的持久连接，并且当前正在使用它。

## SERVER_PORT

`SERVER_PORT` 变量的值告诉 CGI 程序当前正在使用哪个服务器端口来访问该程序。一个示例如下：

```
SERVER_PORT = 80
```

如果 CGI 程序创建了指向服务器的 URL，将端口地址（即此变量的值）包含在 URL 中可能很有用。

## REMOTE_HOST

`REMOTE_HOST` 变量告诉 CGI 程序客户端的 IP 地址或 IP 名称，如下所示：

```
REMOTE_HOST = dsl-666.isp24by7.net
```

请注意，如果 Apache 服务器是使用 `MINIMAL_DNS` 选项编译的，则此变量不会被设置。

## REMOTE_PORT

此端口号用于套接字连接的客户端一侧：

```
REMOTE_PORT = 1163
```
