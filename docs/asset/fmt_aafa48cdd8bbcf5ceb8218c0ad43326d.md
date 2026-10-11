
- 如何设置允许使用虚拟用户的 FTP 服务器
- 如何使用 FTP 客户端连接到 FTP 服务器进行测试

这些信息足够让你的 FTP 服务器运行很一段时间了。当然，就像任何关于软件的纸质媒体一样，这些文字会随着时间的推移而老化，信息也会缓慢但确定地过时。因此，请务必定期访问 `vsftpd` 网站，不仅是为了了解最新进展，也是为了获取最新的文档。

# 第 19 章 Apache Web 服务器

Apache 是一种广受欢迎的开源超文本传输协议（HTTP）服务器软件。它根据 Apache 许可证发布。Apache 在使用量和部署方面继续主导 Web 服务器市场。因此，它一直受到互联网社区的一定程度的认可和尊重。Apache 提供了以下一些 set 和优势：

- 它是稳定、灵活且安全的。
- 它被多个主要的网站和组织使用、支持和维护。
- 整个程序及相关组件都是开源的。
- 它可以在大多数 Linux/UNIX 变体 Microsoft Windows 上运行。

在本章中，我们将介绍 Linux 服务器上安装和配置 Apache HTTP 服务器的过程。但在进入配置 Apache 的步骤之前，让我们先回顾 HTTP 的一些基础知识，这将帮助你理解 Apache 为何要这样工作。

# 理解 HTTP

HTTP 流量构成了互联网流量的重要部分，Apache 是 HTTP 的一种实现。Firefox、Chrome、Opera、wget、Edge、Safari 等都是 HTTP 的客户端实现。截至目前，HTTP 处于版本 2，但 HTTP/1.1 仍然是最广泛使用的版本。

# 标头

当客户端连接 Web 服务器时，客户端的默认方法是连接 TCP 端口 80。一旦连接，客户端向服务器发出 HTTP 命令（也称为动词或方法）。每个命令都带有一个请求头部，其中包含了客户端的信息。例如，当在 Linux 上使用 Firefox 浏览器（客户端）时，Web 服务器可能会从客户端接收到以下信息：

```
GET /HTTP/1.1
Connection: Keep-Alive
User-Agent: Mozilla/* (X11;Linux x86_64;rv:*) Firefox/*
Host: localhost:80
Accept: text/xml, image/gif, image/jpeg, image/png...
Accept-Encoding: gzip
Accept-Language: en-us
Accept-Charset: iso-8859-1,utf-8
```

第一行包含 HTTP GET 命令，请求服务器获取文件。其余部分是头部，它告诉服务器有关客户端的信息。许多服务器使用这些信息来决定可以向客户端发送的内容，以及用于记录。

请求头部还可能带有额外的标头。例如，当客户端使用超链接访问服务器站点时，标头还会显示客户端的源地址。

当接收到空行时，服务器就知道请求头部已完成。一旦接收到请求头部，它将响应请求的内容，并在前面带有服务器头部。服务器为客户端提供有关服务器的信息、客户端即将接收的数据量、数据类型以及其他信息。例如，上述请求头部发送到 HTTP 服务器后，会产生如下响应头部：

```
HTTP/1.1 200 OK
Date: Sun, 07 Jun 2026 14:03:31 GMT
Server: Apache/2.4.* (Fedora)
Last-Modified: Sun, 07 Jun 2026 11:41:32 GMT
ETag: "7888-1f-b08bf300"
Accept-Ranges: bytes
Content-Length: 31
Connection: close
Content-Type: text/html; charset=UTF-8
```

响应头部之后是一个空行，然后是传输的实际内容。

# 端口

HTTP 请求的默认端口是 80，但你也可以配置 Web 服务器使用不同的（任意选择的）未被其他服务占用的端口。这是在同一台主机上运行多个 Web 服务器的机制之一，每个服务器或站点都运行在不同的端口上。某些站点还利用这种安排对其 Web 服务器进行多重配置，以支持各种类型的客户端请求。

当网站在非标准端口上运行 Web 服务器时，你可以在网站的 URL 中看到该端口号。例如，带有默认端口（80）的网络地址 www.example.com 隐式和显式读取 http://www.example.com 和 http://www.example.com:80。但要在端口 8080 等非端口上提供相同网站的服务需要显式指定端口号，如 http://www.example.com:8080。

# 进程所有权与安全

在 Linux 平台上运行 Web 服务器遵循传统的 Linux/UNIX 权限和所有权模型。在权限方面，这意味着每个进程都有一个所有者，该所有者在系统上拥有有限的。

每当启动（进程）时，它都会继承其父进程的权限。例如，如果你以 root 身份登录，你用来执行所有工作的 shell 就拥有与 root 用户完全相同的。你从该 shell 启动的任何进程将继承你所有的权限。进程可以放弃权限，但不能获得权限。

> 注意：Linux 继承原则有一个例外。配置了 SetUID 位的程序不会继承其父进程的权限，而是以文件本身所有者指定的权限运行。例如，包含程序 `/bin/su` 的文件所有者为 root，并设置了 SetUID 位。如果用户 yyang 运行程序 `/au`，该程序不会继承 yyang 的权限，而是将以超级用户（root）的权限启动。要了解更多关于 SetUID 的信息，请参阅第 6 章。

# Apache 如何处理进程所有权

为了执行初始网络相关功能，Apache HTTP 服务器必须以 root 权限启动。具体而言，它需要绑定到端口 80，以便监听并接受连接。一旦完成绑定，Apache 就可以放弃权限并按照配置文件的指定以非 root 用户（无权限用户）身份运行。不同的 Linux 发行版对此可能有不同的默认值，但通常是以下之一：nobody、www、apache、wwwrun、www-data 或 daemon。

记住，当作为无权限用户运行时，Apache 只能读取该用户具有权限读取的文件。

对于使用可执行脚本作为通用网关接口 (CGI)、PHP 或 Python 脚本的站点，安全特别为重要。通过限制 Web 服务器的权限，你降低了向服务器发送恶意可执行请求的可能性。服务器和相应的脚本只能破坏它们可以访问。作为用户 nobody，脚本和进程无法访问 root 用户可以访问的关键文件（记住，默认情况下，root 可以访问一切，无论权限如何）。

![](img/206cceb3dded456e2347d07189576dd7_436_0.png)

# 安装 Apache HTTP 服务器

大多数 Linux 发行版都将 Apache HTTP 服务器重新封装为 RPM、deb 或其他文件，因此安装软件通常像使用系统上的包管理工具一样简单。本节将引导你通过 RPM 和高级软件包工具 (APT) 获取并安装程序。如果选择从源代码安装，文中也会提到相关方法。在后续章节中涵盖的服务器实际配置适用于这两类安装方式（源码或二进制包）。

在 Fedora/RHEL/CentOS 系统上，提供 Apache HTTP 服务器的包名非常直观地命名为 `httpd.rpm`。我们将在示例服务器上使用包管理器（`dnf` 或 `yum`）来安装和获取程序。

使用 `dnf` 安装程序，输入以下命令：

```
[master@fedora-server ~]$ sudo d install httpd
```

确认软件已安装，输入以下命令：

```
[master@fedora-server ~]$ sudo rpm -q httpd
```

对于像 基于 Debian 的发行版，提供 Apache HTTP 服务器（版本 2）的包名更直观地命名为 "apache2"。你可以运行以下命令使用 APT 安装 Apache：

```
master@ubuntu-server ~]$ sudo apt-get -y install apache2
```

在 Ubuntu 系统上使用 `apt-get` 安装后，Web 服务器会自动启动。

大功告成！你现在已经安装了 Apache。

# Apache 模块

Apache 之所以强大且灵活的部分原因在于，它可以通过模块进行扩展。Apache 默认带有许多模块，并在默认安装中自动包含它们。

如果你想象出“某个功能”，你几乎可以肯定已经有人为 Apache Web 服务器编写了一个模块。Apache 模块编程接口 (API) 有完善的文档，如果你有此意向（并且懂），你可以为 Apache 编写自己的模块以提供任何想要的功能。

为了让你对人们正在用模块做什么有所了解，请访问 modules.org。你将在那里找到如何使用模块扩展 Apache 能力的信息。这里是一些常见的 Apache 模块：

- `mod_wsgi` 为托管基于 Python 的 Web 应用程序提供符合 Web 网关接口 (WSGI) 标准的接口
- `mod_authnz_ldap` 提供支持通过 LDAP 验证 Apache 服务器用户的功能
