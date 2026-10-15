
### 示例配置

为了帮助你充分理解 Squid 访问控制是如何工作的，并帮助你制定自己的规则时抢先一步，以下是一些你可以尝试的 ACL 行。每行之前都有带有说明其功能的注释行（以 `#` 开头）：

```
# 包含域 news.bbc.co.uk 和 slashdot.org
# 但不包含 newsimg.bbc.co.uk 或 www.slashdot.org
acl newssites dstdomain news.bbc.co.uk slashdot.org
```

```
# 包含 bbc.co.uk 或 slashdot.org 的任何子域
acl newssites dstdomain .bbc.co.uk .slashdot.org
```

```
# 仅包含位于加拿大的网站
acl canadasites dstdomain .ca
```

```
# 仅包含工作时间
acl workhours time MTWHF 9:00-18:00
```

```
# 仅包含午餐时间
acl lunchtimes time MTHWF 13:00-14:00
```

```
# 仅包含周末
acl weekends time AS 00:00-23:59
```

```
# 包含以 ".zip" 结尾的 URL。注意：\ 很重要，
否则 "." 具有特殊含义
acl zipfiles url_regex -i \.zip$
```

```
# 包含以 https 开头的 URL
acl httpsurls url_regex -i ^https
```

```
# 包含所有匹配 "hotmail" 的 URL
acl hotmail url_regex -i hotmail
```

```
# 包含三个特定的 IP 地址
acl directors src 10.0.0.14 10.0.0.28 10.0.0.31
```

```
# 包含从 192.168.0.0 到 192.168.0.255 的所有 IP
acl internal src 192.168.0.0/24
```

```
# 包含从 192.168.0.0 到 192.168.0.255 的所有 IP
# 以及从 10.0.0.0 到 10.255.255.255 的所有 IP
acl internal src 192.168.0.0/24 10.0.0.0/8
```

当你的 ACL 规则配置好后，你就可以组合出适当的 `http_access` 指令了。例如，你可能希望使用多层访问系统，使得某些用户（例如，公司董事）拥有完全访问权限，而其他用户则受到过滤。例如：

```
http_access allow directors
http_access deny hotmail
http_access deny zipfiles
http_access allow internal lunchtimes
http_access deny all
```

由于 Squid 按顺序匹配这些指令，因此董事将拥有完全且无过滤的 Web 访问权限。如果客户端 IP 地址不在 `directors` 列表中，则处理这两个 `deny` 指令，以防止用户下载 `.zip` 文件或在 Hotmail 上阅读在线邮件。在屏蔽了这两种类型的请求后，第四行的 `allow` 指令允许内部用户访问 Web，前提是他们只能在午餐时间进行访问。最后一行（强烈建议保留）阻止其他所有用户通过代理访问。

## 参考

- `http://www.squid-cache.org/` — Squid Web Proxy Cache 的首页。

- `http://www.deckle.co.za/squid-users-guide/Main_Page` — *Squid: A User's Guide* 的首页，这是一本关于 Squid 的免费在线书籍。

- `http://www.faq.org/docs/securing/netproxy-squid.html` — 配置本地 Squid 服务器的简要在线指南。

- `http://squid.visolove.com/squid/index.htm` — 一家提供 Squid 商业支持和部署服务的公司的首页。

- `http://squid.visolove.com/squid/reverseproxy.htm` — ViSolve 关于配置 Squid 作为反向代理以缓存本地 Web 服务器供外部访客访问的指南。

除了这些网址，还有两本关于 Web 缓存主题的绝佳书籍。第一本是杜安·韦塞尔（Duane Wessel）著的 *Squid: The Definitive Guide*（O'Reilly 出版），ISBN: 0-596-00162-2。第二本是同一作者著的 *Web Caching*（O'Reilly 出版），ISBN: 1-56592-536-X。

这两本书中，前者更实用，深入涵盖了 Squid 服务器。后者更具理论性，讨论缓存的实现方式。韦塞尔是 Squid 的主要开发人员之一，因此两本书的技术准确性都无可挑剔。

## 第 23 章

# 管理 DNS

网络中的计算机需要有用，这意味着你需要能够识别每台计算机，以便与其连接和通信。如今大多数网络使用 *Internet Protocol*（*IP*），因此该网络中的每台计算机都有一个独特的 IP 地址用于标识。

IP 地址是一个非常庞大的 32 位数字，但有一种显示该数字的快捷方法，称为 *dotted-quad address*（点分十进制地址）。点分十进制形式的地址由四个用点分隔的 8 位数字组成。例如，地址为 3232250992 的计算机的点分十进制形式为 192.168.60.112。使用并记忆 IP 地址的点分十进制形式更容易，但即便如此，记住许多数字仍然相当困难。*domain name system*（*DNS*，域名系统）允许你为这些 IP 地址分配主机名，这些名称更容易记忆。这些名称（如 fedoraproject.org）由 DNS 翻译成点分十进制 IP 地址，节省了时间——还有记忆力！

这种翻译过程被称为 *name resolution*（名称解析），由称为 *resolver*（解析器）的软件执行。对于普通用户而言，本地配置涉及 DNS 客户端，它查询远程 DNS 服务器以交换信息。DNS 服务器通常由 *Internet service providers*（*ISPs*，互联网服务提供商）和大型企业网络维护，尽管任何人都可以配置和运行自己的 DNS 服务器。网络中的所有计算机都需要配置好 DNS 客户端。

本章介绍使用 *Berkeley Internet Name Domain*（*BIND*，伯克利互联网域名服务）的 DNS 概念和实践，BIND 是 UNIX 的事实标准 DNS 软件。在本章中，你将学习一些 DNS 及其功能的基本概念，包括 DNS 结构信息的存储方式、DNS 如何向用户提供名称信息，以及名称解析的实际工作原理。你将学习如何使用 BIND 配置名称服务器，以及如何为域名提供 DNS 服务。本章还将向你介绍一些保持 DNS 功能安全的重要技术，以及追踪与你 DNS 功能相关潜在问题的一些最重要的故障排除技术。

如果你不会成为 DNS 管理员，本章中的许多信息对你可能没有实际用处。话虽如此，你在本章中获得的 DNS 知识可能有助于你理解发生的 DNS 问题——这样你就会意识到并不是你的计算机坏了！你还将看到，在注册域名后，如何获取第三方 DNS 服务，从而无需自己维护 DNS 服务器。此外，常用的 DNS 相关工具也会进行讲解，重点介绍如何使用它们来排除你很可能遇到的域名解析问题。

DNS 对许多类型的网络操作至关重要，尤其是当你的网络通过互联网提供与外部世界的连接时。DNS 旨在使主机名的分配和翻译快速可靠，并为网络资源提供一致、可移植的命名空间。其数据库以分布式方式维护，以适应其规模以及频繁更新的需求。通过广泛使用本地缓存，提高了性能和带宽利用率。数据库部分的权限被委托给能够并愿意及时维护数据库的人，因此更新不再受中央管理机构日程安排的限制。

DNS 是一个简单——但容易配置错误——的系统。主机名解析错误可能会以非常不明显的方式表现出来，甚至在导致错误的更改发生很久之后。这样的命名错误会导致不可接受且令人尴尬的服务中断。

理解处理 BIND 所涉概念和流程将有助于确保你作为 DNS 管理者的体验是愉快的。

## 本章内容

- 为客户端配置 DNS
- 基本 DNS 概念
- 使用 DNS 工具
- 配置本地缓存名称服务器
- 你自己的域名和第三方 DNS
- 使用 BIND 为真实域名提供 DNS
- 为真实域名提供 DNS
- 故障排除 DNS
- 管理 DNS 安全
- 参考

## 为客户端配置 DNS

本章稍后部分将重点介绍提供 DNS 的设置和配置。本节简要检查计算机使用 DNS 服务所需的设置和配置。重要的用户设置和配置过程很可能已在 Fedora 的初始安装过程中完成。初始安装后，进一步的 DNS 配置可以通过以下一种或多种方法完成：
