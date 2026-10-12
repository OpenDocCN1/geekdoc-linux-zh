
# VirtualHost

如果你想在机器上维护多个域名/主机名，你可以为它们设置 `VirtualHost` 容器。在尝试设置虚拟主机之前，请查阅文档 <http://www.apache.org/docs/vhosts/> 获取更多细节。你可以使用命令行选项 `-S` 来验证你的虚拟主机配置。

如果你想使用基于名称的虚拟主机，你必须为它们定义至少一个 IP 地址（以及端口号）。

```apache
#NameVirtualHost 12.34.56.78:80
#NameVirtualHost 12.34.56.78
```

## VirtualHost 示例

几乎任何 Apache 指令都可以进入 `VirtualHost` 容器。

```apache
<VirtualHost ip.address.of.host.some_domain.com>
    ServerAdmin webmaster@some_domain.com
    DocumentRoot /www/docs/some_domain.com
    ServerName some_domain.com
    ErrorLog logs/host.some_domain.com-error_log
    CustomLog logs/host.some_domain.com-access_log common
</VirtualHost>
```

```apache
<VirtualHost _default_:>
</VirtualHost>
```

# 其他 Web 服务器

出于许多原因，某些管理员选择不运行 Apache 作为他们的 Web 服务器软件。也许他们不需要像 Apache 这样功能复杂的系统，对于一个只提供有限数量静态页面的小型网络来说，Apache 的选项可能太多了。其他管理员更倾向于针对特定类型流量的服务器，或者设计用于安全或速度而非多种类型请求的服务器。还有一些管理员可能只想使用更新的服务器，因为他们喜欢在工作中心支持开发者。

无论你想要运行非 Apache Web 服务器的原因是什么，你可供选择的 Web 服务器其实并不多。本节将介绍一些流行的非 Apache Web 服务器，其中大多数都是构建使其可以运行在多个 Unix 平台上。只有其中一个——kHTTPD——是特定平台的，因为它需要 Linux 内核才能运行。然而，其他服务器可以在无数 Unix 变体上成功运行。

# boa

boa Web 服务器是一个采用 GNU 公共许可的程序，为速度和安全而设计。与许多其他 Web 服务器不同，boa 在运行时不需要通过派生进程（forking）来处理流量请求；相反，多个请求是在内部处理的。这种机制允许 boa 能够承受如潮般的请求，并能在快速响应时间内提供页面。根据 boa 开发团队的说法，官方基准测试显示 boa 在 Pentium 上每秒可以处理数千次访问，在 386 上每秒处理几十次。

尽管 boa 正在 Linux 平台上开发，但它已经在其他 Unix 变体（包括 FreeBSD 和 Solaris）上成功运行。它的安装方式与其他任何源码包一样，对于使用非 Linux Unix 的用户来说不应该是问题。boa 自 1991 年以来一直在开发，尽管它沉寂了几年，直到一个新的开发团队接手了它。当前版本是 0.9.83，当前团队表示开发将随着 0.95 版本的更新。

> 可以在项目网站 <http://www.boa.org> 了解更多关于 boa 的信息。该网站提供了下载和完整文档，包括安装指南。`boa.conf` 文件是 boa 的主配置文件，有详尽的注释，易于根据系统需求进行配置。

# dhttpd

这一系列较为人知的 Web 服务器中的第二个被称为 dhttpd。该服务器是为几种 Unix 变体编写的，书中涵盖了最主要的变体。它非常小，且仅为个人 Web 使用而设计；也就是说，如果你计划提供可能会成为热门访问地的页面，你可能不想使用 dhttpd。然而，如果你只想运行一些可以提供一两个个人 Web 页面的东西，并且你不认为全世界都会点击鼠标来到你的门，那么 dhttpd 可能是正确的选择。它比 Apache 显然需要的空间和 CPU 周期要少得多。

dhttpd 的优势之一是开发者使得该服务器可以从用户空间运行。运行此 Web 服务器不需要 root 权限，如果你在不向用户提供 Web 空间的机器上拥有用户账户，这可能会很有用。

# fhtpd

另一个根据 GNU 公共许可发布的小型服务器程序被称为 fhtpd，全称为“文件/超文本传输守护进程”（File/HyperText Daemon）。fhtpd 的设计目标是快速且高效，不需要像 Apache 那样复杂的配置，但在传输文件和 HTML 方面尽可能可靠。

大多数 Web 服务器针对 HTML 文档（尽管它们通常也能处理文件传输），而文件传输通常留给 FTP（文件传输协议）客户端。fhtpd 试图弥补这一差距。

fhtpd 目前处于 0.4.2 版本，这意味着它仍然是测试软件。然而，开发者声称它非常健壮且安全，除非是 0.3 版本左右否则没有重大漏洞。它可以运行在几乎任何 Unix 变体上，包括书中提到的三种。一个非常有用的举措是，开发者提供了一个异常详尽的 Unix Makefile。默认配置是为 Linux 设计的，如果你运行不同的 Unix，只需在行首添加注释符号取消 Linux 行，并取消你的特定变体相关的注释即可。

要了解更多关于 fhtpd 的信息（对于一个 Web 流量不大但文件传输与 HTML 页面相当的小网络，这可能是一个很好的解决方案），可以咨询项目网站 <http://www.fhtpd.org>。该网站上的文档组织得非常好，包含分步骤的安装指南以及配置文件 `fhtpd.conf` 的完整选项列表。

# Jigsaw

如果你想运行一个保证符合超文本传输协议标准每个组件的 Web 服务器，你应该运行 Jigsaw。Jigsaw 服务器由 W3C（万维网联盟）开发，W3C 负责管理 HTTP 协议。Jigsaw 的创建是为了作为 W3C 程序员设计的服务器，旨在实现随着协议演进的每一个方面。Jigsaw 在 Web 服务器中独一无二，因为它是用 Java 编写的，使其具有平台无关性。尽管它被设计为 W3C 用途的实验性服务器，但它足够健壮强大，供普通 Web 管理员作为常规服务器运行。该服务器主要面向倾向于处理各种 Java servlets 的程序员，而不是那些只想运行该程序的管理员。如果你想运行一个完全符合规范的 Web 服务器，Jigsaw 可能是你的理想选择。我们可以随时轻松支持完全符合既有协议的软件。

> **注意**：在 W3C 网站 <http://www.w3c.org/Jigsaw/> 获取 Jigsaw 及其详细文档。你可以在该网站阅读常见问题解答（FAQ）、程序员指南以及代码本身，也可以下载该服务器。Jigsaw 当前版本为 2.1.2，这是一个不稳定发布版本。2.0 版本是最新的稳定版本。

## 符合协议的浏览器

如果你打算使用 Jigsaw 是因为它符合 HTTP 标准，那么为什么不在客户端也使用符合规范的浏览器呢？Opera 浏览器将只显示符合当前 HTML 协议版本编写的 HTML 页面。我们认为 Opera 是一个极佳的浏览器；缺点是 Web 上的许多页面并不符合 HTML 规范。

特别是使用 Netscape Composer 和 Microsoft FrontPage 编写的页面会生成不符合规范的 HTML，Opera 将直接拒绝显示这些页面。然而，如果你愿意浏览有限的页面，Opera 可能是你的正确选择。请查看 <http://operasoware.com> 上的网页。请注意，如果你选择使用该浏览器，需要支付费用。

# kHTTPd

Linux 用户在 kHTTPd 程序中有一个不寻常的 Web 服务器选项。该服务器的工作方式与其他 Web 服务器完全不同：它是基于内核的。

这意味着 kHTTPd 作为内核模块运行而不是普通程序，这为它的运行提供了稳定性和速度。

由于运行方式，kHTTPd 只能提供静态 Web 页面。页面——即保存在公共目录文件中、每次调取时都保持不变且通常保存为 HTML 格式文本的文件——构成了互联网上个人 Web 页面的主体，并且可能仍是企业 Web 页面的重要部分。（并不是所有人都对采用华丽的动画型 Web 设计感兴趣，特别是那些关注为使用自适应 Web 浏览器的用户服务的人。）如果你需要同时提供动态页面和静态页面，则需要配合功能更全的 Web 服务器（如 Apache）运行 kHTTPd。然而，如果你的网站是完全静态的，使用 kHTTPd 可能是处理这些请求的合适方法。

kHTTPd 当前版本为 0.16b，集成在 2.3.14 Linux 内核中。你可以在项目网站 <http://www.fenrus.demon.nl/> 获取 kHTTPd 内核模块。

# WN
