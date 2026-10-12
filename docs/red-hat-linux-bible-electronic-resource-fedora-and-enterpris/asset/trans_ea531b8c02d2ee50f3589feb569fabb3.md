
> **TIP:** 我强烈建议阅读 CERT 提供的 FTP 文档。这些文档中的提示将有助于保持您的 FTP 服务器安全，同时使您能够提供想要共享的服务。

## 摘要

FTP 服务是向 Internet 上的用户提供文档和软件文件归档的主要方法。随 Red Hat Linux 提供的唯一 FTP 服务器软件包是 Very Secure FTP 服务器。虽然 WU-FTPD 服务器已不再包含在 Red Hat Linux 中，但您可以从 `rpmfind.net` 获取并安装 WU-FTPD 的 RPM。

## 第21章
### 设置 Web 服务器

### 本章内容

- Web 服务器简介
- 快速启动 Apache Web 服务器
- 配置 Apache Web 服务器
- 启动和停止服务器
- 监控服务器活动

万维网是互联网增长最快的领域，HTTP 流量占总网络带宽的 70% 以上。电子商务为试图保持技术领先的企业提供了一个新的虚拟店面。

Web 也为寻求廉价发布和分发信息手段的组织带来了福音。随着计算能力的提升、价格的下降，以及 Linux 等免费操作系统和 Apache、TUX 等免费 Web 服务器，任何人建立 Web 存在感变得更加容易。

本章向您展示如何安装和配置 Apache Web 服务器。服务器的每个配置文件都进行了详细描述和解释。您将了解启动和停止服务器的各种选项，以及如何监控 Web 服务器的活动。安全问题在整章的描述和示例中都有涉及。

> **NOTE:** 当前版本的 Red Hat Linux 随附 Apache 2.0。Apache 2.0 包括对新的 Apache 应用程序编程接口、UNIX 线程（用于多处理）、Internet 协议版本 6 和多协议的支持。还添加了一些新模块。在 2.0 中，软件包名称 apache 和 apache-manual 改为 httpd 和 httpd-manual。

### Web 服务器简介

当今所知的万维网始于蒂姆·伯纳斯-李在欧洲粒子物理中心（CERN）的项目。最初的目标是为需要以多种格式访问信息的地理分散的研究人员和科学家提供一个一致的界面。从这个想法中产生了使用一个客户端（Web 浏览器）从多种类型的服务器（HTTP、FTP、SMTP、Gopher、NNTP、WAIS、Finger 和流媒体服务器）访问数据（文本、图像、声音、视频和二进制文件）的概念。Web 服务器通常的工作更简单：接受 HTTP（超文本传输协议）请求并向客户端发送响应。然而，这项工作可能会变得更加复杂（服务器也是如此），执行的功能例如：

- 基于文件权限、用户名/密码对以及主机名/IP 地址限制执行访问控制。
- 在发送给客户端之前解析文档（为文档中任何条件字段替换适当的值）。
- 启动 CGI（通用网关接口）脚本或自定义 API（应用程序编程接口）程序以评估提交表单的内容，呈现动态创建的文档或访问数据库。
- 向客户端发送 Java 小程序。
- 记录任何成功的访问、失败和错误。

### Apache Web 服务器

Apache Web 服务器最初基于 HTTPd，由 NCSA（国家超级计算应用中心）提供的免费服务器。当时，HTTPd 是互联网上最常见的服务器。不幸的是，服务器的开发未能跟上网站管理员的需求，并且发现了几个安全问题。许多网站管理员已独立地将自己的功能和修复应用到 NCSA 源代码中。1995 年初，这些开发人员中的一群人汇集了他们的努力并创建了“一个补丁服务器”，最初只是对 HTTPd 代码的一组补丁。此后，Apache 组织在很大程度上重写了代码并创建了一个稳定、多平台的 Web 服务器守护进程。

Apache 也是多个其他 Web 服务器的基础，其中大多数使用 Apache 免费提供的源代码并添加了改进的安全功能，例如用于加密数据传输的 SSL（安全套接字层）或高级身份验证模块。

Apache Web 服务器的主要功能包括：

- 与大量合作志愿者程序员相关的稳定性和快速开发周期。
- 完整源代码，可免费下载。
- 使用纯文本文件进行配置的简便性。
- 基于客户端主机名/IP 地址或用户名/密码组合的访问控制。
- 支持服务器端脚本以及 CGI 脚本。
- 自定义 API，可使外部模块（例如，用于扩展日志记录功能、改进身份验证、缓存、连接跟踪等）被服务器守护进程利用。

Apache 并不是 Red Hat Linux 可用的唯一 Web 服务器，但它是与 Red Hat Linux 一起使用最常见的服务器，并且根据最近的 Netcraft 调查（www.netcraft.com/survey），它是互联网上使用最广泛的服务器。除了 Apache，Red Hat Linux 还附带 TUX Web 服务器。

### TUX Web 服务器

TUX Web 服务器（也称为 Red Hat 内容加速器）是 Red Hat Linux 发行版的一部分的高性能、基于内核的 Web 服务器。通过在 Linux 内核中运行，TUX 可以非常高效地提供静态内容（例如图像），同时与另一个 Web 服务器的守护进程集成，以处理 TUX 内核驱动程序尚未支持的内容（例如 TUX 不了解的各种脚本语言）。

在使用它的计算机上，TUX 服务器通常接管主要的 Web 服务器端口（端口 80）。（Apache Web 服务器将监听 8080 或其他端口。）TUX 服务由 /etc/init.d/tux 启动脚本启动，并根据您在 /proc/net/tux 中设置的内核参数运行。

至少您需要设置 serverport（用于 TUX）、clientport（用于 Apache）以及 Web 服务器内容位置的 DOCROOT 内核参数。该位置（通常为 /var/www/html）必须对 TUX 和 Apache 服务器相同。TUX 使用内核驱动程序处理其支持的部分数据类型，并使用可加载模块处理其他类型。随着这些模块的不断可用，更多数据类型将能够在内核中运行，而无需移交给较慢的用户级进程。

TUX 的特殊功能包括大规模虚拟主机，可在一个 Web 服务器上支持多个虚拟主机，以及 FTP 支持，可让您将 TUX 配置为匿名 FTP 服务器。此外，由于 TUX 不为每个客户端启动一个进程，因此一次可以有数千个客户端连接处于活动状态，而不会对内存分配造成过大的需求。

有关 TUX 的更多信息，请安装随 Red Hat Linux 提供的 tux 软件包。然后使用浏览器参考从 /usr/share/doc/tux-*/tux/index.html 开始的文档。

### Red Hat Linux 可用的其他 Web 服务器

下面描述了一些可在 Red Hat Linux 上运行的其他 Web 服务器，并提供了提供更详细信息的 URL。

- **Stronghold 3** — 这款来自 Red Hat 的基于 Apache 的 Web 服务器具有 128 位 SSL 加密和数字证书。根据 Netcraft（www.netcraft.com）的说法，Stronghold 是 UNIX 系统的顶级商业 SSL Web 服务器。详情请参阅 Red Hat 的 Stronghold 页面：www.redhat.com/software/apache/stronghold。
- **Zope** — 除了能够提供 Web 内容外，Zope 还包括添加新闻、会员信息和搜索功能的功能。Zope 最初由 Zope Corporation（www.zope.org）创建，现在作为一个在 GPL 下的开源项目（zope.sourceforge.net）提供。
- **AOIserver 3.5** — 原名 NaviPress，该服务器具有基于 Web 的管理、访问控制、SSL 加密和 SQL 数据库驱动程序。更多信息和可下载的源代码可在 aolserver.sourceforge.net 找到。
- **Boa 0.94** — 设计为快速、简单且不臃肿，Boa 比其他服务器需要的系统资源更少，非常适合旧硬件。它可以从 www.boa.org 下载。
- **CERN (W3C) Jigsaw 2.2** — 最新 HTTP/1.1 参考服务器，完全用 Java 编写且可免费获得，可在 www.w3.org/Jigsaw 找到。它具有广泛的缓存、改进的外部程序执行机制（尽管也支持 CGI）以及图形化管理工具。
- **Servertec iServer 1.1** — 用 Java 编写，这个相对较小的服务器在集群环境中提供负载均衡和容错，并且可以轻松地与应用程序和数据库服务器耦合。更多详情可在 www.servertec.com/products/iws/iws.html 获得。

### 快速启动 Apache Web 服务器

如果在 Red Hat 安装期间未安装 Apache，您可以稍后从随书附带的 CD-ROM 安装。您需要 httpd 软件包，并可选择 httpd-manual 软件包（在早期版本中名为 apache 和 apache-manual）。

> **NOTE:** 在可用的等效 Red Hat 软件包之前，可能会发布新版本的 Apache。或者您可能希望自定义服务器的编译时选项并直接从源代码构建 Apache。您可以从 www.apache.org/dist/ 下载完整的源代码发行版，或从 www.apache.org/dyn/closer.cgi 选择最近的镜像。

这里有一个快速启动 Apache Web 服务器的方法。从这里开始，您需要根据自己的需求和环境对其进行自定义（如下一节所述）。

1. 通过在终端窗口中输入以下命令确保已安装 Apache：

```
$ rpm -qa | grep httpd
redhat-config-httpd-1.1.0-1.1
httpd-devel-2.0.45-14
```
