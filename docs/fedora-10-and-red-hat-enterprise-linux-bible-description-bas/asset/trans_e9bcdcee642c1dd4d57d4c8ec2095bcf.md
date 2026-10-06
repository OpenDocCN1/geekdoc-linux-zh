

## Web 服务器简介

如今为人知的广域网（Wide Wide Web）最初是蒂姆·伯纳斯李（Tim Berners-Lee）在欧洲粒子研究中心（CERN）的一个项目。其最初的目标是为地理分散的研究人员和科学家提供一个统一的接口，以便他们访问各种格式的信息。这一想法产生了这样一个概念：使用一个客户端（Web 浏览器）从多种类型的服务器（HTTP、FTP、SMTP、Gopher、NNTP、WAIS、Finger 和流服务器）访问数据（文本、图像、声音、视频和二进制文件）。

Web 服务器的工作通常简单：使用超文本传输协议（HTTP）请求并向客户端发送响应。然而，这项工作可能会变得复杂得多（因为服务器还可以执行以下功能）：

- 对文件权限、用户名/密码对，以及主机名/IP 地址限制进行访问控制。
- 在将文档发送到客户端之前对其进行解析（为文档中的任何条件替换适当的值）。
- 启动通用网关接口（CGI）脚本或自定义编程接口（API），以评估提交表单的内容、呈现动态创建的文档或访问数据库。
- 记录任何成功访问、失败和错误。

## Apache Web 服务器

Apache Web 服务器最初基于来自国家超级计算机应用中心（NCSA）的免费服务器 HTTPd。当时，HTTPd 是互联网上第一个也是唯一的 Web 服务器。遗憾的是，该服务器的开发未能跟上 Web 管理员的需求，并且发现了几个安全问题。许多 Web 管理员已经在 NCSA 源码中应用了自己的功能和修复程序。

1995 年，这些开发者中的一组汇集力量，基于这些代码创建了一个名为 Apache 的新项目。从那时起，Apache 软件基金会（http://www.apache.org）很大程度上重写了代码，并创建了一个稳定的多平台 Web 守护进程。Apache 软件基金会还赞助多个相关项目。这些项目包括 mod_perl（使用 Perl 语言创建动态 Web 网站）、Jakarta（提供服务器端 Java 内容）、DB（创建和维护商业级数据库解决方案）以及 spammassassin（识别和处理垃圾邮件）。

Apache Web 服务器的主要特性包括：

- 与大型协作志愿者程序员群体相关的稳定性和快速的开发周期。
- 完整的源代码，可免费下载。不适用最终用户许可协议（EULA）的限制，也不限制运行的服务器数量。
- 使用纯文本文件易于配置。
- 基于客户端主机/IP 地址或用户名/密码组合的访问控制。
- 支持服务器端脚本以及 CGI 脚本。这包括允许不同的用户控制脚本执行（以在单个脚本被攻破时限制整个服务器的脆弱性）。
- 自定义 API，允许模块（例如扩展的日志功能、改进的身份验证、缓存、连接跟踪等）被服务器守护进程使用。

Apache 不是 Fedora 和 RHEL 系统的唯一 Web 服务器，但它是 Linux 上最频繁使用的服务器，根据 Netcraft（http://news.netcraft.com/archives/web_server_survey.html），它仍然互联网上最流行的服务器。除了 Apache 之外，Fedora 和 RHEL 还带有了 lighttppd 和轻量级服务器。

## 第 21 章：设置 Web 服务器

## Fedora 和 RHEL 可用的其他 Web 服务器

以下列表描述了一些可以在 Fedora 和其他 Red Hat 发行版上运行的其他服务器，URL 提供了更详细的信息。

- lighttppd — lighttppd Web 服务器（http://www.lighttppd.net）为安全、速度、合性和灵活性而构建。它特别针对高性能环境进行了优化，因为它具有低占用率并能平衡 CPU 负载。YouTube、Wikipedia 和 meebo 等网站已将 lighttppd 用于某些 Web 应用。
- telchtpd — TelThtpd Web 服务器（telchtpd 包）包含在工具命令语言（TCL）中。作为 Web 服务器，TelThtpd 也可以用于 TCL 应用程序服务器。
- httpd — httpd HTTP 服务器（http://acme.com/software/httpd）设计为简单、小巧、可移植且快速。它的创建者将其称为微型、涡轮、节流的 HTTP 服务器。它实现的功能少于符合 HTTP/1.1 标准所需的最小值，因此在极端负载下其运行速度比许多大型 Web 服务器快。
- XSP — XSP Web 服务器（xsp 包）可以运行 ASP.NET 应用程序以及处理 ASP.NET 应用程序的相关服务。
- Zope — 除了能够提供 Web 内容外，Zope 还包含添加新闻、会员信息和搜索功能特性。Zope 最初由 Zope 公司（http://www.zope.org）创建，现在作为开源项目可用。

## 第四部分：Fedora RHEL 网络和服务器设置

受 GPL 协议保护的项目。当前版本的 Fedora 或 RHEL 中不包含 Zope。你可以从 Zope 开发网站（http://zope.sourceforge.net/）获取 Zope。Zope 是基于 Python 的。

- CERN (W3C) Jigsaw 2.2.6—该 HTTP/1.1 参考服务器，完全用 Java 编写并免费提供，可以在 http://www.w3.org/Jigsaw 找到。它具有广泛的缓存机制和改进的外部程序执行机制。

