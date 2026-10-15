
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

问题描述，请参阅 `www.ncfptd/doc/misc/ftp_and_firewalls.html` 上的 FTP 和您的防火墙页面。

# 获取更多关于 FTP 服务器的信息

有大量资源可以获取更多关于 FTP 服务器的信息。以下是一些选项：

- FAQ — 要查看 vsftpd 的常见问题（FAQ），请前往 `/usr/share/doc/vsftpd*/FAQ`。
- RFCs — 征求（Requests For Comments）是定义互联网使用的标准协议的文档。FTP 的主要 RFC 是 RFC959。您可以从互联网上的各种位置获取 RFCs，包括 RFC/STD/FYI/BCP 归档（`www.faqs.org/rfcs`）。
- CERT — 该机构为设置 FTP 服务器提供了有用文档。《匿名 FTP 滥用说明》（Anonymous FTP Abuses）描述了如何应对 FTP 服务器滥用并从从中恢复。它还告诉了如何处理软件盗版问题。《匿名 FTP 配置指南》（Anonymous FTP Configuration Guidelines）为设置您的 FTP 区域提供了通用指导，并说明了在设置可写 FTP 区域时面临的特定挑战。这两份文档均可在 CERT 技术提示页面（`www.cert.org/tech_tips`）获取。

> 提示：我强烈建议阅读 CERT 的 FTP 文档。这些文档中的技巧将帮助保持您的 FTP 服务器安全，同时让您提供您想要共享的服务。

## 总结

FTP 服务是通过互联网向用户提供文档和软件文件存档的主要方法。Fedora 和 RHEL 交付的唯一 FTP 服务器包是 Very Secure FTP（vsftpd）服务器。vsFtPD 服务器依靠标准的 Linux 文件和用户权限，为在 Fedora 中运行提供一个简单且安全的 FTP 环境。

# 第 21 章

## 设置 Web 服务器

本章内容

- Web 服务器简介
- 快速启动 Apache Web 服务器
- 配置 Apache Web 服务器
- 启动和停止服务器
- 监控服务器活动

如今约 50% 的 Web 网站都由开源的 Apache Web 服务器项目驱动（相比之下，微软 Web 服务器的占比约为 31%）。2008 年 2 月，Netcraft（`www.netcraft.com`）报告称，收到了来自超过 1.58 亿个网站的响应，其中超过 80,000 个网站正在运行 Apache。随着互联网域名的注册以每月超过 100 万的平均速度持续增长，Apache 正在获得新启动网站的大份额。

Web 对于寻求廉价手段发布和分发信息的组织来说也是一种福音。使用本书附带的 Fedora 发版或 RHEL，您可以使用来自 Apache 项目的软件启动您自己的 Web 网站。将您的域名、互联网连接以及 Fedora 或 RHEL 结合起来，在广域网上建立您自己的阵地。

本章将展示如何安装和配置 Apache Web 服务器。本章将详细描述并解释服务器的每一个配置文件。您将学习用于启动和停止服务器的各种选项，以及如何监控 Web 服务器的活动。整个章节的描述和示例中涵盖了相关的安全问题和实践，并在第 14 章的特殊 Web 服务器安全章节（“使用证书和加密保护 Web 服务器”）中也进行了专门说明。

> 注意：当前版本的 Fedora 带有 Apache 2.2 版本。Apache 2.2 包含了对新 Apache 应用程序接口的支持、UNIX 线程（用于多进程处理）、网协议版本 6（IPv6）以及多种协议。如果您一直在使用 Apache 2.0 之前的版本，请注意包名 `apache` 和 `apache-manual` 已更改为 `httpd` 和 `httpd-manual`。

# Web 服务器简介

现为人知的广域网（Wide Web）最初是 Tim Berners-Lee 在欧洲粒子物理中心（CERN）的一个项目。其最初的目标是为地理分散的研究人员和科学家提供一个统一的接口，以便他们访问各种格式的信息。这一想法催生使用一个客户端（Web 浏览器）从多种类型的服务器（HTTP、FTP、SMTP、GNNP、WAIS、Finger 和流媒体服务器）访问数据（文本、图像、声音、视频和二进制文件）。

Web 服务器通常的工作较简单：接收超文本传输协议（HTTP）请求并向客户端发送响应。然而，这项工作可能会变得更复杂（服务器也可以），执行如下功能，例如：

- 根据文件权限、用户名/密码对以及主机名/IP 地址解析执行访问控制。
- 在将文档发送给客户端之前解析文档（为文档中的任何条件字段替换适当的值）。
- 产生通用网关接口（CGI）脚本或自定义应用程序接口（API）程序以评估提交表单的内容、呈现动态创建的文档或访问数据库。
- 记录任何成功的访问、失败和错误。

# Apache Web 服务器

Apache Web 服务器最初基于 HTTPd，这是由国家超级计算机应用中心（NCSA）提供的一个免费服务器。当时，HTTPd 是互联网上第一个也是唯一的 Web 服务器。遗憾的是，服务器的发展没有跟上 Web 管理员的需求，并且发现了一些安全问题。许多 Web 管理员独立地对 NCSA 源码应用了自己的功能和修复。

1995 年初，这些开发者中的一部分人汇集力量，从该代码库创建了一个名为 Apache 的新项目。从那时起，现在的 Apache 软件基金（`www.apache.org`）已很大程度上重写了代码，并创建了一个稳定的、多平台的 Web 服务器守护进程。超过二十个相关项目也由 Apache 基金赞助。这些项目包括 mod_perl（使用 Perl 语言创建动态站点）、Jakarta（提供服务器端 Java）、DB（创建商业级数据库）以及 spammassassin（识别垃圾邮件）。

Apache Web 服务器的主要特性包括：

- 稳定性且开发周期快。

# 第 21 章：设置 Web 服务器

- 可免费获取的源代码。
- 使用纯文本文件易于配置。
- 基于客户端主机名/IP 地址或用户名/密码的访问控制。
- 支持服务器端脚本以及 CGI（以限制单个脚本被破坏时整个服务器的风险）。
- 允许服务器进程使用自定义 API（用于扩展日志功能、身份验证、缓存、连接跟踪等）。

Apache 不是 Fedora 和 RHEL 的唯一服务器，但它是 Linux 上最使用的。除了 Apache 之外，Fedora 和 RHEL 还带有 lighttpd 和 mph 轻级 Web 服务器。

# Fedora 和 RHEL 可用的其他 Web 服务器

列表列出了可以在 Fedora 或 RHEL 上运行的其他 Web 服务器，并提供了更多详细信息的 URL。

- lighttpd — lighttpd Web 服务器（`www.lighttpd.net`）为了安全、速度、合性和灵活性而构建。它特别针对高性能环境进行了优化，因为其内存占用低且 CPU 负载小。YouTube、Wikipedia 和 meebo 等网站曾使用 lighttpd 处理特殊应用程序。
- tclhttppd — THttpClient 服务器（`tclhttppd` 包）使用工具命令语言（TCL）创建。除了作为 Web 服务器，TclHttppd 还可以作为 TCL 服务器。
- thttpd — thttpd HTTP 服务器（`http://acme.com/software/thttpd`）设计简单、小巧、可移植、快速且安全。其创建者称之为微型、节流 HTTP 服务器。它仅实现了符合 HTTP/1.1 标准的最少功能，因此在极端负载下运行速度比许多 Web 服务器快。
- XSP — XSP Web 服务器（`xsp` 包）可以运行 ASP.NET 应用程序以及与 ASP.NET 工作的相关服务。
- Zope — 除了能够提供 Web 内容外，Zope 还包含新闻、成员信息和搜索功能。Zope 最初由 Zope 公司（`www.zope.org`）创建，现在作为受 GPL 保护的开源项目可用。当前版本的 Fedora 不包含 Zope。

RHEL。你可以从 Zope 开发网站 (`zope.sourceforge.net`) 获取 Zope。Zope 是基于 python 的。

- CERN (W3C) Jigsaw 2.2.6—这是最新的 HTTP/1.1 参考服务器，完全用 Java 编写并免费提供，可以在 `www.w3.org/Jigsaw` 找到。它具有广泛的缓存功能、改进的外部程序执行机制（尽管也支持 CGI）以及图形化管理工具。

## 快速启动 Apache Web 服务器

如果在安装 Fedora 过程中没有安装 Apache，你可以稍后从包含此书的 DVD 或 CD 进行安装。你需要 `httpd` 软件包，以及可选的 `httpd-manual` 包（在早期版本中命名为 `apache` 和 `apache-manual`）。

这里有一个让你的 Apache 服务器运行起来快速方法。从这里开始，你需要匹配你的网络和环境（在接下来的章节中描述）。

- 在终端窗口中输入以下命令，确保 Apache 已安装：
```
