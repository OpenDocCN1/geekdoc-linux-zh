
链被收集在三个表中：`Filter`（过滤）、`NAT`（网络地址转换）和 `Mangle`（修整）。`Filter` 是默认表，根据数据包的内容 `DROP`（丢弃）或 `ACCEPT`（接受）数据包。`NAT` 是网络地址转换表，它转换数据包的源字段或目标字段。`Mangle` 专门用于修改数据包中的 `TOS`（服务类型）、`TTL`（生存时间）和 `MARK` 字段。连接跟踪机制由 `conntrack` 模块处理，它定义基于数据包所属连接状态的标准匹配规则。

在紧急情况下，您可以执行以下命令，从内核卸载所有 `iptables` 模块，并为所有表设置 `DROP` 策略：

```bash
# /sbin/service iptables panic
```

## 练习

- 如何删除所有 `iptables` 规则和链？

- 如何列出所有当前 `iptables` 规则？

- 配置 `iptables` 与配置大多数 Linux 服务有何不同？

- 定义一个 `iptables` 规则，以拒绝 `TELNET` 端口的传入连接。

- `NAT` 代表什么？`NAT` 表做什么？

## 高级练习

- `conntrack` 模块做什么？

- 规则匹配标准做什么？它们用于什么？

- 数据包匹配标准做什么？它们用于什么？

- 哪些实用程序将数据包过滤规则复制到内核和从内核复制？它们如何工作？

- 定义一条规则，以静默阻止来自 `spmr.com` 的传入 `SMTP` 连接。

# Apache (httpd)：设置 Web 服务器

### 本章内容

- JumpStart I：让 Apache 运行起来 ... 844

- JumpStart II：使用 `system-config-httpd` 设置 Apache ... 846

- 文件系统布局 ... 848

- 指令 I：你可能需要修改的入门指令 ... 850

- 上下文和容器 ... 854

- Fedora/RHEL 的 `httpd.conf` 文件 ... 870

- 重定向 ... 873

- Multiviews ... 874

- 虚拟主机 ... 874

- 故障排除 ... 875

万维网（简称 `WWW` 或 `Web`）是一个由持有被称为*内容*的材料的服务器组成的集合，Web 浏览器（或简称为*浏览器*）可以显示这些内容。Web 上的每个服务器都连接到互联网，这是一个网络的网络（即*互联网*）。Web 上的许多内容是用 `HTML`（超文本标记语言，见第 1086 页）编码的。*超文本*，即你点击 Web 页面上的链接背后的代码，允许浏览器显示并响应指向互联网上其他 Web 页面的链接。

`Apache` 是目前互联网上最流行的 Web 服务器。它既坚固又可扩展。在 Linux 环境中安装、配置和运行它的便利性使其成为在万维网上发布内容的明确选择。Apache 服务器及相关项目由 Apache 软件基金会（ASF）开发和维护，该基金会是一家于 1999 年 6 月成立的非营利公司。ASF 源于 Apache 组，该组成立于 1995 年，旨在开发 Apache 服务器。

本章首先提供关于 Apache 的介绍性信息。在此信息之后是第一个 JumpStart 部分，它描述了让 Apache 运行起来所需的最少步骤。第二个 JumpStart 部分介绍了 Fedora/RHEL `system-config-httpd` 配置脚本的使用。在这些部分之后是“文件系统布局”，它告诉你各个 Apache 文件的位置。

配置指令是 Apache 的关键部分，从第 850 页开始讨论。本节包括对上下文和容器的介绍，这是理解 Apache 的两个关键特性/概念。下一节解释主要的 Apache 配置文件 `/etc/httpd/conf/httpd.conf`，该文件经 Fedora/RHEL 修改。本章的最后一页涵盖了虚拟主机、故障排除以及你可以与 Apache 一起使用的模块，包括 CGI 和 SSL。

## 简介

Apache 是一个响应来自 Web 浏览器或*客户端*（如 Firefox、Netscape、lynx 和 Internet Explorer）请求的服务器。当你在 Web 浏览器的地址栏中输入 Web 页面的地址（即*URL*，见第 1113 页）时，浏览器会通过互联网向该地址的（Apache）服务器发送请求。作为响应，服务器将请求的内容发送回浏览器。然后浏览器显示或播放该内容，这可能是一首歌、一张图片、一个视频片段或其他信息。

- **内容**：除了可以与客户端交互的附加模块外，Apache 本身对内容本身并不知情。服务器管理和内容创建是建立 Web 站点的两个方面。本章集中讨论设置和运行 Apache 服务器；它很少花时间讨论内容创建。

- **模块**：Apache 与 Linux 内核类似，使用外部模块来增加加载时的灵活性，并允许部分代码重新编译而无需重新编译整个程序。模块不是 Apache 二进制文件的一部分，而是存储为单独的文件，可以在启动 Apache 时加载。

Apache 使用称为动态共享对象（DSO）的外部模块来执行基本和高级功能；没有这些模块，Apache 的功能就很有限。Apache 还使用模块来扩展其功能：模块可以处理用 Perl、PHP、Python 和其他语言编写的脚本；使用几种不同的方法对用户进行身份验证；促进内容发布；并处理非上下文内容，如音频。由 Apache 组和第三方开发人员编写的模块列表一直在增长。有关更多信息，请参见第 876 页的“模块”。

## 关于 Apache

本节描述你需要安装的包，并提供本章所涵盖程序的参考。“注释”部分（第 844 页）介绍术语和其他主题，将有助于你更好地理解本章。“JumpStart 1”（第 844 页）尽可能快速地让 Apache 运行起来。

### 前提条件

**最小安装** 安装以下包：

- `httpd`

- `apr`（Apache 可移植运行时）

- `apr-util`

**启动 Apache** 运行 `chkconfig` 以便在系统进入多用户模式时启动 `httpd`：

```
# /sbin/chkconfig httpd on
```

配置 Apache 后，使用 `service` 启动 `httpd`：

```
# /sbin/service httpd start
```

更改 Apache 配置后，使用以下命令重启 `httpd`，这将不会干扰连接到服务器的客户端：

```
# /sbin/service httpd graceful
```

**可选包** 你可以安装以下可选包：

- `httpd-manual` — Apache 手册

- `system-config-httpd` — GUI 配置工具

- `webalizer` — Web 服务器日志分析器（第 881 页）

- `mod_perl` — 嵌入式 Perl 脚本语言

- `mod_python` — 嵌入式 Python 脚本语言

- `mod_ssl` — 安全套接字层扩展（第 877 页）

- `php` — 嵌入式 PHP 脚本语言，包括 IMAP 和 LDAP 支持

- `mrtg` — MRTG 流量监视器（第 882 页）

- `net-snmp` 和 `net-snmp-utils` — SNMP，MRTG 所需（第 882 页）。

## 更多信息

**本地** Apache*参考手册和用户指南*：如果 `httpd` 正在运行，将浏览器指向 `http://localhost/manual`；如果 `httpd` 未运行，指向 `/var/www/manual/index.html`。只有安装了 `httpd-manual` 包时，手册才在线可用。

**Web**

- Apache 文档：`httpd.apache.org/docs/2.2`

- Apache 指令列表：`httpd.apache.org/docs/2.2/mod/directives.html`

- Apache 软件基金会（新闻简报、邮件列表、项目、模块注册表等）：`www.apache.org`

- `mod_perl`：`perl.apache.org`

- `mod_php`：`www.php.net`

- `mod_python`：`www.modpython.org`

- `mod_ssl`：`www.modssl.org`

- MRTG：`mrtg.hdl.com/mrtg`

- SNMP：`net-snmp.sourceforge.net`

- SSL：`httpd.apache.org/docs/2.2/howto/ssi.html`

- webalizer：`www.mrunix.net/webalizer`

## 注释

**术语**：Apache 是提供 HTTP 和其他内容的服务器的名称。Apache 守护进程名为 `httpd`，因为它是一个 HTTP 服务器守护进程。本章互换使用术语 *Apache* 和 `httpd`。
