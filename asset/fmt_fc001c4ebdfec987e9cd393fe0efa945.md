
- RITCHIE, DENNIS M. “On the Security of UNIX.” May 1975.

- SCHNEIER, BRUCE. Applied Cryptography: Algorithms, and protocols. New York, NY: Wiley, 1996.

- THOMPSON, KEN. “Reflections on Trust.” in ACM, 1987.

- ZIMMERMANN, PHILIP. The Official UNIX User’s Guide. Cambridge: MIT Press, 1995.

然而，在简单的 HTTP 之外还有其他。目前已经定义了许多增强型协议，用于提供从加密到视频流的所有功能。这些额外的服务通常由独立的守护进程管理，即使它们是由物理服务器提供的。例如，最流行的增强型服务之一是安全 HTTP，简称 HTTPS。它由一个理解安全套接层（SSL）协议的守护进程处理，并监听 TCP 端口 `443` 上的请求。如果你的 UNIX 供应商没有作为操作系统的一部分提供你所需的所有内容，你可能需要从第三方供应商处获取额外的守护进程。

## 统一资源定位符

统一资源定位符（URL）是指向互联网上对象或服务的指针。它通过五个基本组件描述了如何访问该对象：

- 协议或应用程序
- 主机名
- TCP/IP 端口（可选）
- 目录（可选）
- 文件名（区分大小写；以 `".htm"` 或 `".html"` 结尾）

示例 A 展示了一个典型的 URL 及其组件。

### 示例 A URL 的组成部分

![](img/82d5468a9764b2eddb9763f51c9f233c_728_0.png)

表 22.1 显示了 URL 中常用的协议。

| 协议 | 用途 | 示例 |
|---|---|---|
| http | 通过 HTTP 访问远程文件 | http://admin.com/index.html |
| https | 通过 HTTP/SSL 访问远程文件 | https://admin.com/order.shtml |
| ftp | 通过 FTP 访问远程文件 | ftp.xor.com/adder.tar.gz |
| mailto | 向指定地址发送电子邮件 | mailto:sa-book@admin.com |
| news | 访问 Usenet 新闻组 | news:alt.cooking |
| telnet | 登录远程计算机 | telnet:spot.com |
| ldap | 访问 LDAP 目录服务 | ldap://ldap.bigfoot.com:389/cn=Herb |
| file | 访问本地文件（无网络） | file:/etc/syslog.conf |

## 表 22.1 URL 协议

第 22 章 Web 托管与互联网服务器

## HTTP 如何工作

HTTP 是使网页真正运行起来的协议，令许多人惊讶的是，它是一种极其基础、无状态的客户端/服务器协议。在 HTTP 范式中，连接的启动者始终是客户端（通常是浏览器）。客户端向服务器请求特定 URL 的“内容”。服务器返回某种数据或某种错误消息。在 HTTP 0.9 和 1.0 版本中，连接关闭；而在 HTTP 1.1 中，客户端可以继续请求另一个对象。

由于 HTTP 非常简单，你可以使用 `telnet` 轻松地变成一个网络浏览器。由于 HTTP 服务的标准端口是 `80`，只需直接 `telnet` 到所选服务器的该端口即可。一旦连接，你就可以 HTTP 命令。最常用的命令是 `GET`，它请求文档的内容。`GET /` 就是你想要的，因为它请求你所连接的任何服务器的根文档（通常是首页）。HTTP 对大小写敏感，所以请确保使用大写字母命令。

```
% telnet localhost 80
Trying 127.0.0.1...
Connected to localhost.xor.com.
Escape character is "*".
GET /
<contents of your index.html file appear here>
Connection closed by foreign host.
```

## CGI 脚本：动态生成内容

除了提供静态文档外，HTTP 服务器还可以为用户提供动态创建的内容。例如，如果你想为访问你网站的用户提供当前的时间和温度，你可能让 HTTP 服务器执行脚本来获取这些信息。这种让外行人大惊的技巧通常通过通用网关接口，即 CGI 实现。

CGI 并不是一种编程语言，而是一种允许 HTTP 服务器与其他程序交换信息的规范。通常是 Perl 或 C 语言程序，这些程序是专门为与 HTTP 服务器接口而编写的。但实际上，任何可以执行实时 I/O 的编程语言都是可以的。想想那些孤单的 FORTRAN 程序，现在可以将它们的技能应用到互联网了！

在大多数情况下，CGI 脚本是 Web 开发人员和程序员的事。遗憾的是，在一个领域，CGI 脚本与系统管理员的工作发生了冲突：安全性。由于 CGI 脚本可以访问文件、网络连接以及在不同位置移动数据的方法，它们的执行可能会影响运行 HTTP 服务器的机器的安全性。最终，CGI 脚本让世界上任何人都有在你的服务器上运行程序（即 CGI 脚本）。因此，CGI 脚本需要像任何其他网络可访问程序一样安全。

## UNIX 系统管理手册

关于安全处理 CGI 脚本的良好信息源，请参考文件 `www.w3.org/Security/Faq/www-security-faq.html`。

## 负载均衡

很难预测服务器能够处理多少次命中（对单个对象的请求，如文本文件或图像）或页面浏览（对单个可视页面上所有对象的请求）。服务器的精确容量取决于其运行的操作系统、调优程度、硬件架构（包括子系统）以及网站的结构（例如，它是静态 HTML 页面，还是有数据库类和数值计算）。

### 表 22.3 我们建议移除的 Apache 模块

| 模块 | 功能 |
| --- | --- |
| asis | 允许发送指定的文件类型而不带 HTTP 标头 |
| autoindex | 索引没有默认 HTML 文件的目录（例如，`index.html`） |
| env | 允许为 CGI 脚本设置特殊的环境变量 |
| include | 允许服务器包含，一种过时的即时内容创建方案 |
| userdir | 允许用户拥有自己的 HTML 目录 |

![](img/82d5468a9764b2eddb9763f51c9f233c_732_0.png)

在 FreeBSD 上，Apache 是可以从 `/usr/ports` 安装的额外软件包之一（有关 `/usr/ports` 机制的更多信息，请参阅第 808 页）。要安装 Apache，请 `cd` 到 `/usr/ports/www/apache13` 并输入 `make`。

## 配置 Apache

现在你已经安装了服务器，需要为你的应用程序进行配置。所有的配置文件都保存在 `conf` 目录中（例如 `/usr/local/apache/conf/`）。你需要检查并配置三个配置文件以匹配你网站的需求：`httpd.conf`、`srm.conf` 和 `access.conf`。

`httpd.conf` 指定了 Apache 守护进程 (`httpd`) 如何与你的系统交互。在此文件中，你可以设置 HTTP 服务器监听查询的 TCP 端口（通常是端口 `80`，你可以选择它——而且你可以在单台机器上通过不同的端口运行多个 HTTP 服务器）、日志文件的位置以及各种性能参数。`Httpd.conf` 也是配置 `httpd` 响应虚拟接口连接的文件；详情请参阅第 694 页。

服务器需要访问的资源在 `srm.conf` 文件中控制。该文件包含了至关重要的 `DocumentRoot` 定义，它定义了可服务文档所在的目录树根节点。该文件还处理诸如 `http://www.conf/~user~` 这样的“特殊”URL 处理问题。

你通过 `access.conf` 文件管理安全问题，该文件包含按文件或按目录控制访问的指令。这些权限防止从外部世界或你的网站内部通过 `httpd` 访问敏感文件。

你应该至少指定两个访问控制：一个覆盖整个目录，另一个仅适用于 `cgi-bin` 目录。只有指定的 `cgi-bin` 目录应该允许脚本执行。然而，单个用户不能通过自己的脚本创建安全漏洞（无论无意还是有意）。在 `srm.conf` 中使用 `ExecCGI` 来启用此限制。

## 运行 Apache

你可以手动启动 `httpd` 或从机器的 `rc` 脚本启动。后者更优，因为这种配置将确保 Web 服务器在机器重启时都会自动重启。要手动启动服务器，你需要输入类似的内容：

```
% /usr/local/apache/apachectl start
```
