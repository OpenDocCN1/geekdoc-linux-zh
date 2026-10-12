
- d. 使用 `Ctrl-F5` 或 `Shift-Reload` 强制重新加载页面（参见模块 14.16）。如果页面正确加载，则可能存在缓存问题，无论是在您的客户端还是代理服务器上

- e. 如果可能，将您的客户端配置为不使用代理服务器，并重新尝试

- f. 暂时禁用客户端中的所有缓存（“始终检查页面是否为最新”），并删除临时/缓存文件以确保无误。然后重试。

## 摘要

- Web 使用 `HTTP` 协议将 Web 页面从服务器传输到客户端浏览器

- 客户端浏览器向服务器请求页面，并解释和显示其接收到的页面。大多数浏览器使用全功能、窗口化 GUI，但也存在纯文本浏览器

- 大多数 Web 页面包含 `HTML`，其中可以包含超链接，允许用户跳转到当前服务器或另一个服务器上的不同页面

- `HTTP` 运行在 `TCP` 之上，并使用众所周知的端口 80

- `HTTP` 交互——与 `SMTP` 类似——由纯文本命令和响应组成。然而，与 `SMTP` 不同，`HTTP` 可以安全地传输任意二进制数据而无需特殊编码，因为它知道使用的是 `TCP` 连接

- 在 `HTTP` 1.0 和 1.1 版本中，客户端和服务器在请求和响应中发送报头，以提供关于其功能以及所请求/返回数据的信息

- `HTTP` 使用 `MIME` 指定内容类型和大小

- `HTTP/1.0` 为每个请求/回复使用单独的 `TCP` 连接，但 `HTTP/1.1` 可以为多个请求/回复事务使用单一连接

- `HTTP/1.1` 通过使用包含在客户端请求中的 `Host:` 报头来处理单个 IP 地址上的多个 Web 站点

- “Web 站点”的名称仅仅是处理该站点的服务器的 IP 地址，通常通过 `DNS` 查询获取。单个名称通常具有多个 IP 编号，这允许在多个 Web 服务器之间进行负载分担

- Web 页面可以是服务器上的静态文件，也可以由服务器根据客户端请求中包含的用户输入动态生成

- Web 代理服务器通常用于性能、安全或日志记录/控制目的

- Web 浏览器通常缓存已下载的页面。如有需要，您可以配置浏览器中缓存的操作方式

- Web 服务器可以在用户访问 Web 站点的特定部分时要求用户进行身份验证。身份验证信息通常以 base-64 编码的用户/密码信息形式，通过请求中的 `Authorization:` 报头发回

- 可以使用 `HTTPS` 协议在客户端和服务器之间安全地发送加密的 Web 流量

- 您可以手动使用 `telnet` 发出命令，并使用 `tcpdump` 或 `grep` 观察流量，从而排查 Web 连接故障。

## 接下来？

在下一章中，我们将介绍第二种广泛使用的传输协议 `UDP`（第一种是 `TCP`）。之后，我们将探讨更多应用及相关的高层协议。

![](img/a2132b646d336d5f9a21102d6320e537_418_0.png)

## 注释与延伸阅读

### HTTP 协议

最初的 `HTTP/0.9` 规范位于：

- http://www.w3.org/Protocols/HTTP/AsImplemented.html

`HTTP` 由 CERN（欧洲核子研究中心）发明，他们有一份关于其发展历史的文档，其中包含大量指向其他来源的链接：

- http://ref.cern.ch/CERN/CNL/2001/001/www-history/

`HTTP` 的规范包括：

- `RFC-1945` 1996年5月 超文本传输协议 – `HTTP/1.0`

- `RFC-2616` 1999年6月 超文本传输协议 – `HTTP/1.1`

如果你需要查找不同的 `HTTP` 请求头，可以查阅上述规范。（一些请求头是在后续的 `RFC` 中增加的。）

- `RFC-2396` 1998年8月 统一资源标识符（`URI`）– 通用语法

我们还没有处理服务器。然而，值得一提的是，与浏览器相比，服务器非常简单——它只需要接受 `TCP` 连接，读取几个请求头，并回复一块数据（即 Web 页面）。客户端非常复杂，因为它需要处理许多不同形式的图形、多窗口的用户交互、`JavaScript` 和 `Java` 可执行代码等。这是一个表明 Web 浏览器实际上是一个多么庞大的项目的指示。`Netscape` 将其浏览器的源代码公开，并建立了 `Mozilla.org`（http://www.mozilla.org）来管理开发，由数百名开发者和测试人员参与贡献——采用类似于 `Linux` 的开源模式。但即使拥有对源代码的完全访问权限，项目也花了大约两年时间才真正起飞并开始交付预期的成果——这比预期的时间要长得多。

出于好奇，这里有一些微小且/或怪异的 `HTTP` 服务器实现。它们分别是：一个用 `C` 语言编写的微型服务器（150 行代码）、一个 Shell 脚本服务器，以及一个用 Postscript 编写的服务器（供那些脑洞大开的人使用）：

- http://www.acme.com/software/micro_http/

- http://jtester.vip.net.pl:8081/

- http://www.pugo.org:8080/

PostScript 服务器当然只是一个新奇事物，但 `C` 语言的微型服务器作为嵌入到你自己的应用程序中的专用服务器，确实非常有用。

### 动态 Web 页面

在 Web 的早期，所有的 Web 页面都是“静态”的，即你收到的是驻留在 Web 服务器上的普通文件的内容。为了使 Web 能够作为应用程序的通用接口，需要一种方法来允许 Web 服务器调用其他程序，并将你在 Web 浏览器中输入的数据传递给这些程序。用于此目的的标准机制称为 `CGI`（`通用网关接口`）。这是一个花哨的名字，但事实上它非常简单。我们见过的最简单和清晰的 `CGI` 脚本介绍是：

- http://snowwhite.it.brighton.ac.uk/~mas/mas/courses/html/html3.html

其中包含一些优秀的示例。关于 `CGI` 的更概览，请参见：

- http://hoohoo.ncsa.uiuc.edu/cgi/overview.html `通用网关接口`

Web 服务器根据服务器配置和指定的 URL 来识别请求的页面是否是动态的。例如，一种常见的设置是，形式为 `http://servername/cgi-bin/pagename` 的 URL 意味着“运行名为 `pagename` 的 `CGI` 脚本”。在 Microsoft Web 服务器上，Active Server 页面的 URL 通常以 `.asp` 结尾。

`Java`、`JavaScript` 和 `ActiveX` 程序的工作方式不同。`JavaScript` 代码通常嵌入在 `HTML` 页面的文本中，并通过特殊的 `<script>` `HTML` 标签引入。`Java` 和 `ActiveX` 程序使用特殊的 `<applet>` 和 `<object>` 标签作为页面内的链接指定。

### 代理

- http://spywaresucks.org/prox/index.html `The Proxomitron – 一个通用的 Web 过滤器`

- http://www.flaaten.dk/prox `The Proxomitron`

- http://www.sankey.ws/proxomitron.html `The Proxomitron 简介`

Microsoft 的 Internet Explorer 支持 `WPAD`（Web 代理自动发现协议）以实现自动代理配置：

- http://www.microsoft.com/technet/prodtechnol/ie/reskit/ie5/part5/ch21auto.asp [IE 5.x > Resource Kits] `第 21 章 – 使用自动配置和自动代理`

以下注释描述了 `WPAD` 中的一个问题，但也清晰地说明了其工作原理：

- http://www.securiteam.com/windowsntfocus/3O5PTQAQAAA.html `已发布修复“WPAD 欺骗”漏洞的补丁`

`WPAD` 未获得 `IETF` 批准为互联网标准：

- http://www.ietf.org/proceedings/99nov/46th-99nov-ietf-35.html

- http://www.ietf.org/iesg/iesg.99-08-12

### 浏览器缓存

- `MS-KB-Q201535` `Internet Explorer 不检查 Web 页面的较新版本`

- `MS-KB-Q263070` `Internet Explorer 缓存设置如何影响 Web 浏览`

### 身份验证

你可以使用 Linux 程序 `mimencode` 对 base-64 数据进行编码和解码。像许多 `UNIX` 程序一样，该程序可以直接从键盘读取标准输入（按 `Ctrl-C` 终止），或者你可以使用 `echo` 程序将字符串通过管道传输给它。下面展示了两种方法的示例。解码非常相似，但你提供编码后的数据作为输入，并给 `mimencode` 提供 `-u` 解码选项。我们使用的示例来自模块 14.17 中的请求头。
