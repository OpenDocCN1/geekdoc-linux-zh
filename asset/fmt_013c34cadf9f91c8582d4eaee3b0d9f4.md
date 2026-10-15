
这将产生类似于图 4.4 的内容。

![](img/878462b29f2b7b00190db4a77480e642_204_0.png)

图 4.4 XSSI `printenv` 命令截图。

要在 XSSI 中设置变量，使用 `set` 命令：

```
<!--#set var="boat" value='Titanic' -->
```

现在

作为其他参考，请参见 Apache 的 SSI 教程：

`http://httpd.apache.org/docs/howto/ssl.html`。

# ModSSL 与 Apache+SSL

Apache 安装中可以使用两个主要的 SSL 软件包：ModSSL 和 Apache+SSL 补丁。本节介绍了这两个包的优点、缺点以及安装问题。

## SSL-mod_ssl

`mod_ssl` 是源自 Ben Laurie 的 Apache+SSL 补丁的模块。

本质上，这些补丁提供给整个社区，作为彼此的替代方案。它们与选择使用 Vi 还是 Vim 没有区别。

安全套接层（SSL）协议由 Netscape 开发，旨在为敏感信息（如在线信用卡交易中使用的信息）提供一个安全的传输通道。SSL 现在是一项互联网标准，Apache 能够通过模块来实现它。

## SSL–安全套接层

安全套接层协议（SSL 协议）是一个协议层，可以放置在可靠的面向连接的网络层层协议（例如 TCP/IP）和应用协议层（例如 HTTP）之间。SSL 通过允许双方身份验证、使用数字签名确保完整性以及使用加密保护隐私，在客户端和服务器之间提供安全通信。

SSL 协议设计用于支持对加密、摘要和签名特定算法的多种选择。这允许特定服务器的算法选择基于法律、出口或其他考虑，并使该协议能够利用新算法。在建立协议会话时，客户端和服务器之间会进行协商。

（注：此处原文中存在大量重复的定义段落，已在翻译中去重处理）

请求在启用 SSL 的目录中存储内容的客户端必须使用 `https://` URL 而不是 `http` 格式。原因之一是启用 SSL 的服务通常提供与非安全传输不同的端口（通常为 443）。

## 在 Apache 中实现 SSL

有两种方法向 Apache 增加 SSL。第一种方法是用 Apache-SSL 替换 Apache。这是一个包含的 SSL 版本（实际上，它是作为 Apache 源码的补丁分发的）。可以在 `apache-ssl.org` 网站获取。另一种方法是向标准版本的 Apache 添加 `mod_ssl` 模块（在大多数情况下，必须重新编译 Apache 才能使 `mod_ssl` 工作）。关于 `mod_ssl` 的更多信息可以在 `www.modssl.org/` 找到。在本课程的剩余部分我们将关注 Apache-SSL。

## 法律问题

SSL 数据传输需要加密，许多政府对加密技术的进口、出口和使用有限制。此外，某些加密算法在某些国家拥有专利。当 SSL 包含在软件软件包中时，其分发涉及许多法律问题。这就是为什么 SSL 与标准 Apache 分开分发。

直到最近，美国还禁止强加密（通常定义为超过 40 位）。这一禁令最近已放宽，但新法的完全影响尚未完全分析。在美国境内，由于 RSA Data Security 持有的 RSAREF 专利过期，SSL 可用于任何用途。该专利以前通常不适用于美国境外。

尽管你的 Apache 服务器现在应该建立得良好，但它仍然需要持续的维护。下一章将讨论一些可能出现问题的简单解决方案。

# 第 5 章

# 故障排除

## 目标

- 列出 Apache 在线故障排除资源
- 列出常见的 Apache 信息和调试选项
- 列出常见的配置和日志问题

## 在线故障排除资源

Apache 在线手册 `www.apache.org/docs/` 始终是一个很好的起点。这里还有一个通用的 Apache FAQ 位于 `www.apache.org/docs/misc/FAQ.html`。

在问题报告（PR）数据库 `http://bugs.apache.org` 进行搜索。在此页面顶部，你可以输入搜索字符串并搜索整个数据库。在页面下方，你可以输入若干参数来缩小搜索范围。

在 `http://dev.apache.org`，你还会找到 `new-httpd` 邮件列表的存档。该存档是 Apache 开发者多年来一直用于讨论与 Web 服务器开发相关问题的列表。这些存档中包含大量信息。仅订阅 `new-httpd` 邮件列表进行收听是一个好主意。订阅说明以及其他邮件列表可以在此处找到：`http://dev.apache.org/mailing-lists.html`。

Apache 主要的用户用户支持形式是 USENET 上的 `comp.infosystems-www.servers.unix` 新闻组。该组的存档可以在 `www.deja.com/group/comp.infosystems.www.servers.unix` 找到。

## 追踪 Apache 核心转储 (Core Dump)

偶尔会出现意外情况。Apache 崩溃有很多原因，例如 Apache 代码中的 bug、机器内存故障，或者添加的第三方模块存在 bug。为了理解可能导致崩溃的原因，可以采取一些措施。

检查 `/var/apache/logs/error_log` 文件。

以下是一些可能的消息：

```
Tue May 2 09:20:46 2000 [notice] Apache/1.3.14
(Unix) mod_perl/1.21 configured - resuming normal operations
```

这是一条良好的消息。意味着服务器已经启动并且运行正常。

```
Tue May 2 09:21:17 2000 [notice] caught
SIGTERM, shutting down
```

这也是一条良好的消息。意味着服务器通过类似 `apachectl stop` 的命令正常关闭了。

```
Tue May 2 09:41:25 2000 [notice] SIGHUP
received. Attempting to restart
```

这是一条良好的消息。意味着服务器通过类似 `apachectl restart` 的命令重启了。

## 故障排除 189

```
Tue May 2 09:31:14 2000] [warn] pid file
/var/run/httpd.pid overwritten - Clean
shutdown of previous Apache run?
```

这并不是一条非常糟糕的消息。意味着 Apache 服务器在上次运行中发生了某些情况，并且没有正常关闭。

```
Tue May 2 09:31:44 2000] [notice] child pid
10187 exit signal Segmentation Fault (11)
```

这是一条非常糟糕的消息。意味着其中一个 `httpd` 子进程发生了转储（dump）。

如果在 `error_log` 文件中发现段错误（Segmentation Fault）或可能的总错误（Bus Error），可以使用一些工具提供关于问题原因的提示：

```
/opt/sfw/bin/gdb
/usr/bin/truss
/usr/bin/mdb
```

## gdb 的典型用法：

```
# gdb /usr/apache/bin/httpd
GNU gdb 4.18
Copyright 1998 Free Software Foundation, Inc.
GDS 是自由软件，受 GNU 通用公共许可协议保护，欢迎在特定条件下更改它并分发其副本。
输入 "show copying" 查看条件。
GDB 不提供任何担保。输入 "show warranty" 了解详情。
你可以从源码包中编译 httpd。
PATH=/usr/sbin:/usr/bin:/opt/sfw/ccs/bin
cd /usr/share/src/apache
```

> 注意：我们使用 `-X` 标志运行 `httpd`，这意味着它将在非派生模式（non-forking mode）下启动。这使得追踪变得容易得多，因为这种方式我们只需要担心一个 `httpd` 进程。

## 一些有用网站

以下网站将帮助你的故障排除工作：

## 190 第 5 章

- `cronolog` (`www.ford-mason.co.uk/resources/cronolog`)。用于 Apache Web 服务器的日志文件轮转程序。
- ApacheWeek (`www.apacheweek.com`)。提供技巧的免费在线杂志。
- O’Reilly Network Apache Forum (`www.oreillynet.com/cgi-bin/conf/summary?group=oreillynet.apache`)。Apache 用户的讨论论坛。
- `nDevshed Forums` (`www.devshed.com`)。涵盖大量 Apache 问题和解决方案的讨论论坛。

## 配置问题

配置问题可能导致 Apache 无法启动，也可能导致请求失败，或者以非预期的方式提供服务。
