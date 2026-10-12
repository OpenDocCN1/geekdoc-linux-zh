
- 自定义 Apache 服务器名称、地址、端口以及内容、日志和脚本的位置

- 允许用户从家目录发布内容

- 配置虚拟主机以显示不同的内容

- 配置密码保护目录层次、基于主机访问控制、目录选项和 SELinux 布值以保护 Web 内容访问

# 918 第 26 章 APACHE (httpd)：设置 Web 服务器

万维网（WWW 或简称为 Web）是一系列服务器的集合，这些服务器存储着名为内容的内容，浏览器可以显示这些内容。Web 上的每台服务器都连接到互联网，即一个网络的网络（互连）。Web 上的大部分内容使用 HTML（超文本标记语言，第 1168 页）编码。超文本是指你在网页上点击的链接，允许浏览器显示并响应指向互联网上其他网页的链接。

Apache 是互联网上流行的 Web 服务器。它既健壮又具有扩展性。在 Linux 环境下安装、配置和运行它的便利性，使其成为在万维网上发布内容的显而易见的选择。Apache 服务器相关项目由 Apache 基金会（ASF）开发和维护，ASF 是一家 1999 年 6 月成立的非营利机构。ASF 源于 Apache Group，该小组成立于 1995 年，旨在开发 Apache 服务器。

本章从关于 Apache 的介绍性信息开始。随其后的是第一个 JumpStart 部分，它描述了让 Apache 运行所需的最小步骤。接下来是“文件系统布局”，它告诉你各种 Apache 文件的位置。

配置差异（称为指令）是 Apache 的关键部分，将从 925 页开始讨论。该部分包含了对上下文（contexts）和容器（containers）的介绍，这是理解 Apache 的两个关键特性/概念。下一部分从 947 页介绍了 Fedora/RHEL 分发的主 Apache 配置文件 `httpd.conf`。本章的最后几页涵盖了 Apache 配置：重定向、内容协商、目录索引、虚拟主机、故障排除以及你可以与 Apache 一起使用的模块，包括 CGI 和 SSL。

## 引言

Apache 是一个响应 Web 浏览器或客户端（如 Firefox、Netscape、lynx、elinks 和 Internet Explorer）请求的服务器。当你在 Web 浏览器的地址栏中输入网页地址（统一 标识符，第 1195 页）时，浏览器将通过互联网向该地址的（Apache）服务器发送请求。作为响应，服务器将请求的内容发回浏览器。浏览器显示或播放这些内容，这些内容可能是文本文档、歌曲、图片、视频或其他信息。

除了与内容交互的模块，Apache 只查看它正在发送的数据类型，以便指定正确的 MIME（第 1176 页）类型；否则它对内容本身保持忽略。服务器管理和内容创建是建立网站的两个不同方面。本章侧重于设置和运行 Apache 服务器；花的时间讨论内容创建较少。

模块 Apache 像 Linux 内核一样，使用外部模块来增加加载时的灵活性，并允许在不重新编译整个程序的情况下对部分代码进行重新编译。模块不是 Apache 二进制文件的一部分，而是作为单独的文件存储的，可以在 Apache 启动时加载。

Apache 使用称为动态共享对象（DSO）的外部模块来实现基本和高级功能；没有这些模块，Apache 将变得大无形。Apache 还使用模块来扩展其功能。例如，模块可以处理 Perl、PHP、Python 和其他语言编写的脚本；使用不同的方法验证用户；促进内容的发布；以及处理文本内容（如音频）。由 ASF 和第三方开发者编写的模块列表正在不断增长。更多信息请参阅第 957 页的“模块”。

## 更多信息

- 本地 Apache 文档：在 Apache 运行并安装了 `http-manual` 包的情况下，将浏览器指向 `server/manual`。在服务器系统上，将 `server` 替换为 `localhost`；对于远程系统，将 Apache 服务器的名称或 IP 地址替换为 `server`。如果 Apache 未运行，仅将浏览器指向服务器系统上的 `/var/www/manual/index.html`。

- Apache 指令：`server/manual/mod/directives.html`

SSI 指令：`server/manual/howto/ssi.html`

- Web 版 Apache 文档：`http.apache.org/docs/2.2`

Apache 指令：`http.apache.org/docs/2.2/mod/directives.html`

Apache 基金会（通讯通讯、邮件列表、项目注册、webalizer：`www.mrunix.net/webalizer`

wstats：`stats.sourceforge.org`

- `mod_perl`: `perl.apache.org`

`mod_php`: `www.php.net`

`mod_python`: `www.modpython.org`

`mod_ssl`: `www.modssl.org`

`mod_wsgi`: `code.google.com/p/modwsgi`

MRTG: `oss.oietker.ch/mrtg`

SNMP: `net-snmp.sourceforge.org`

SSI 指令：`http.apache.org/docs/2.2/howto/ssi.html`

## 注释

术语 Apache 是一个提供 HTTP 和其他内容的服务器名称。Apache 和 `httpd` 守护进程命名为 `httpd`，因为它是一个 HTTP 服务器守护进程。本章交替使用 Apache 和 `httpd` 术语。

术语 server Apache 服务器等于 Apache 进程。Apache 子进程的存在是为了处理传入的客户端请求；因此它被称为服务器。

防火墙 Apache 服务器通常使用 TCP 端口 80；安全服务器使用 TCP 端口 443。如果 Apache 服务器系统正在运行防火墙或位于防火墙之后，你可以打开其中一个或两个端口。要开始，请打开端口 80 (HTTP)。使用 `system-config-firewall`，从 Trusted Services 选项卡（第 894 页）选择 WWW (HTTP) 和/或 Secure WWW (HTTPS) 以打开这些端口。

SELinux 因为 SELinux 使用的是目标策略（targeted policy），`httpd` 受 SELinux 保护。如有必要，你可以禁用它。更多信息请参阅“使用 SELinux 设置目标策略”。

## 运行 Apache Web 服务器

本节解释了如何安装、测试和配置基本的 Web 服务器。

### 前提条件

最小化安装 安装以下软件包：

- `httpd`

- `apr`（Apache 运行时，随 `httpd` 安装）

- `apr-util`（随 `httpd` 安装）

### 在你设置 Apache 服务器之前

提示 在配置 Apache 服务器之前，为服务器设置一个静态 IP 地址。指令请参阅第 652 页的“为网卡配置静态 IP 地址”。

`httpd` 初始化脚本 运行 `chkconfig` 以导致 `httpd` 在系统进入多用户模式时启动：

```
# chkconfig httpd
```

在配置 Apache 后，使用 `service` 启动 `httpd`：

```
# service httpd start
```

在更改 Apache 配置后，使用以下命令重启 `httpd`，这不会干扰连接到服务器的客户端：

```
# service httpd graceful
```
