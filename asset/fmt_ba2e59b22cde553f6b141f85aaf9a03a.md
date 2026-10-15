
在本章中，我们讨论在 Linux 服务器上安装和配置 *Apache HTTP* 服务器（`www.apache.org`）的过程。Apache 是根据 GNU GPL 发布的免费软件。根据网络上最受尊敬的统计数据之一（由 Netcraft Ltd 发布，`www.netcraft.co.uk`），Apache 的市场份额超过 50%。互联网社区给予如此高度的认可，源于 Apache 服务器软件提供的以下优势和利益：

- 它非常稳定
- 多个主要 Web 站点，包括 `www.hotmail.com`，都在使用它
- 整个程序及相关组件都是开源的
- 它支持大量平台（所有流行的 UNIX 变体，一些不太流行的 UNIX 变体，甚至 Windows NT）
- 它极其灵活
- 它已被证明是安全的

在介绍配置 Apache 的必要步骤之前，我们将回顾 HTTP 协议的一些基础知识，以及 Apache 的一些内部机制，例如其进程所有权模型。这些信息将帮助我们理解为什么 Apache 被配置为以这种方式工作。

## HTTP 的机制

HTTP（超文本传输协议）当然是万维网（World Wide Web）基础的重要组成部分，而 Apache 是 HTTP 协议的服务器端实现。诸如 Netscape Navigator 和 Microsoft Internet Explorer 等浏览器是 HTTP 的客户端实现。

截至撰写本文时，HTTP 协议版本为 1.1，并在 RFC 2616 中有文档记录（详情请参见 `ftp://ftp.isi.edu/in-notes/rfc2616.txt`）。

### 标头

当 Web 客户端连接到 Web 服务器时，客户端建立此连接的默认方法是联系服务器的 TCP 端口 `80`。一旦连接建立，Web 服务器保持沉默；必须由客户端发出符合 HTTP 规范的命令来向服务器提出请求。每个命令都附带一个请求标头，其中包含有关客户端的信息。例如，当在 Linux 下使用 Netscape Navigator 作为客户端时，Web 服务器将从客户端接收到以下信息：

```
GET / HTTP/1.0
Connection: Keep-Alive
User-Agent: Mozilla/4.06 [en] (X11; U; Linux 2.2.5-15 i686)
Host: localhost:8000
Accept: image/gif, image/x-xbitmap, image/jpeg, image/jpg,
image/png, */*
Accept-Encoding: gzip
Accept-Language: en
Accept-Charset: iso-8859-1,*,utf-8
```

第一行包含 HTTP GET 命令，该命令要求服务器获取文件。其余信息构成了标头，告知服务器关于客户端的信息、客户端将接受的文件类型等。许多服务器使用这些信息来确定可以向客户端发送什么以及不能发送什么，同时也用于日志记录目的。

除了请求标头外，还可能发送其他标头。例如，当客户端使用超链接获取服务器站点时，标头中还会出现一个显示客户端源站点的条目。

当服务器接收到一个空行时，它知道请求标头已完成。一旦接收到请求标头，服务器会响应实际请求的内容，前面加一个服务器标头。服务器标头告诉客户端关于服务器的信息、客户端即将接收的数据量以及传入的数据类型。例如，向 Red Hat 6.0 下默认安装的 Apache HTTP 服务器发送上述请求标头，会产生以下服务器响应标头：

```
HTTP/1.1 200 OK
Date: Tue, 24 Aug 1999 12:59:46 GMT
Server: Apache/1.3.6 (UNIX) (Red Hat/Linux)
Last-Modified: Wed, 07 Apr 1999 21:17:54 GMT
Etag: "1a005-799-370bcb82"
Accept-Ranges: bytes
Content-Length: 1945
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html
```

响应标头之后是一个空行，然后是传输的实际内容。

### 非标准端口

HTTP 请求的默认端口是 `80` 端口，但你也可以配置 Web 服务器使用其他（任意选择的）未被其他服务占用的端口。这允许站点在同一主机上运行多个 Web 服务器，每个服务器使用不同的端口。一些站点使用这种配置来支持多种 Web 服务器配置，以处理各种类型的客户端请求。

## 进程所有权

当网站在非标准端口上运行 Web 服务器时，你可以在网站 URL 中看到该端口号。例如，地址 `http://www.redhat.com/` 如果添加了端口号，将显示为 `http://www.redhat.com:80/`。

> 警告：不要犯“通过隐蔽性获取安全”的错误。如果你的服务器位于非标准端口上，这并不能保证互联网上的捣乱者找不到你的网站。由于攻击网站所用工具的自动化性质，扫描服务器并查找哪些端口正在运行 Web 服务器所需的 C 代码不到 100 行。使用非标准端口并不能使你的网站“安全”。

正如在其他章节中讨论的那样，在 UNIX 上运行 Web 服务器迫使你处理 Linux（以及通用 UNIX）模型。就权限而言，这意味着每个进程都有一个所有者，并且该所有者在系统上拥有有限的权限。

每当启动一个程序（进程）时，它都会继承其父进程的权限。例如，如果你以 root 身份登录，你用来执行所有工作的 shell 都具有与 root 用户相同的所有权限。此外，从这个 shell 启动的任何进程都将继承 root 用户的所有权限。进程可以放弃权限，但不能获取权限。

> 注意：Linux 继承原则有一个例外：配置了 setuid 位的程序（见第 6 章中的 `chmod` 命令）不会从父进程继承权限，而是以文件所有者本身指定的权限启动。例如，包含程序 `su` 的文件（`/bin/su`）由 root 拥有并设置了 setuid 位。如果用户 `sshah` 运行程序 `su`，该程序不会继承 `sshah` 的权限，而是将以 root 的权限启动。

## Apache 进程所有权

对于网络设置，Apache HTTP 服务器必须以 root 权限启动。具体来说，它需要绑定到端口 `80`，以便能够监听请求并接受连接。完成此操作后，Apache 可以放弃其权限并以非 root 用户身份运行，如配置文件中所指定。默认情况下，这是用户 `nobody`。

作为用户 `nobody`，Apache 只能读取用户 `nobody` 有权限读取的文件。因此，如果文件的权限设置为仅文件所有者可读，则所有者必须是 `nobody`。对于任何你想让用户 `nobody` 访问的文件，请将该文件的权限设置为可被所有人读取：

```
chmod a+r filename
```

其中 `filename` 是文件名。

对于使用 CGI 脚本的网站，安全性尤为重要。通过限制 Web 服务器的权限，你可以降低有人向服务器发送恶意请求的可能性。而且，服务器进程和相应的 CGI 脚本只能破坏它们可以访问的内容。作为用户 `nobody`，脚本和进程无法访问 root 可以访问的关键文件。（请记住：root 可以访问所有内容，无论权限如何。）

> 注意：如果你决定在服务器上允许 CGI 脚本，请严格关注其编写方式。务必确保通过网络输入的数据不能让 CGI 脚本执行它不应该做的事情。虽然没有这方面的统计数据，但大多数成功的网站攻击通常是因为 Web 服务器配置不当和/或 CGI 脚本编写不良所致。

## 安装 Apache HTTP 服务器

虽然大多数 Linux 发行版都预装了 Apache HTTP 服务器，但你可能需要执行升级或调整配置。本节将指导你完成下载 Apache 源代码、编译它并最终安装它的过程。Apache 配置命令将在后续章节中介绍。

如果你想继续使用 Linux 发行版默认的 Apache 安装，可以跳过本节。你只需要知道 Apache 配置文件和顶层页面的位置，以及如何重启服务器。对于 Red Hat Linux，这些位置如下：

- 配置文件：`/etc/httpd/conf`
- 顶层页面：`/home/httpd`
- 重启服务器：`/etc/rc.d/init.d/httpd restart`

Apache HTTP 服务器的最新版本始终位于 `http://www.apache.org/dist`。截稿时，最新版本是 Apache 1.3.9，可在 `apache_1.3.9.tar.gz` 归档文件中找到。

1. 下载 Apache 归档文件并将其放入工作目录。通常，`/usr/local/src` 是用于存储和编译程序的位置。
2. 使用以下命令解包程序：

```
[root@ford src]$ tar -xzvf apache_1.3.9.tar.gz
```

这将创建 `apache_1.3.9` 目录，其中包含编译程序所需的文件。

### 编译 Apache
