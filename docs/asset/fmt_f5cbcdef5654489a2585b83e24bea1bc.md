
为了验证所有端口是否正确配置，请从网络外的任何计算机对该机器执行端口扫描。仅 Web 服务端口（`80`）应处于打开状态。使用 `nmap` 执行端口扫描：

```
nmap -O IP_address
```

# 透明代理配置

## Squid 和其他程序

在以下部分中，查看其他应用程序如何与 Squid 交互。`cachemgr.cgi` 使系统管理员能够检查缓存对象所需的内存量。`squidGuard` 过滤网页。`Calamaris` 是 Squid 的报告生成器。

### cachemgr.cgi

缓存管理器（`cachemgr.cgi`）是一个 CGI 实用程序，用于显示正在运行的 Squid 进程的内存使用情况统计信息。它也是在不登录服务器的情况下管理缓存和查看统计信息的一种更方便的方式。

### 设置

首先，系统上需要一个正在运行的 Web 服务器。要检查 Apache 是否已在运行，请以 root 身份输入 `rcapache status`。

如果出现如下消息：

```
Checking for service httpd: OK
Server uptime: 1 day 18 hours 29 minutes 39 seconds
```

Apache 正在您的机器上运行。否则，输入 `rcapache start` 以使用 SuSE Linux 默认设置启动 Apache。设置最后一步是将文件 `cachemgr.cgi` 复制到 Apache 目录 `cgi-bin`：

```
cp /usr/share/doc/packages/squid/scripts/cachemgr.cgi /usr/local/httpd/cgi-bin
```

### /etc/squid.conf 中的缓存管理器 ACL

原始文件中需要缓存管理器的一些默认设置：

```
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
```

使用以下规则：

```
http_access allow manager localhost
http_access deny manager
```

第一个 ACL 最为重要，因为缓存管理器尝试通过 `cache_object` 协议与 Squid 通信。

以下规则假设 Web 服务器和 Squid 运行在同一台机器上。如果缓存管理器与 Squid 之间的通信源自另一台计算机上的 Web 服务器，请按图 65 添加一个额外的 ACL。

```
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
acl webserver src 192.168.1.7/255.255.255.255 # IP of webserver
```

图 65：访问规则

然后按图 66 添加规则。

```
http_access allow manager localhost
http_access allow manager webserver
http_access deny manager
```

图 66：访问规则

为管理器配置密码以访问更多选项，如远程关闭缓存或查看有关缓存的更多信息。为此，请为管理器配置条目 `cachemgr_passwd` 的密码以及要查看的选项列表。该列表作为 `/etc/squid.conf` 中条目注释的一部分出现。

每次配置文件更改时，使用选项 `-k reconfigure` 重启 Squid。

### 查看统计信息

前往对应的网站：

`http://webserver.example.org/cgi-bin/cachemgr.cgi`

按“继续”并浏览不同的统计信息。缓存管理器显示的每个条目的更多详细信息可在 Squid FAQ 中找到，网址为 `http://www.squid-cache.org/Doc/FAQ/FAQ-9.html`

## SquidGuard

本节无意详细介绍 SquidGuard 的配置，仅介绍它并提供使用建议。有关更深入的配置问题，请参阅 SquidGuard 网站 `http://www.squidguard.org`

`SquidGuard` 是一个免费（GPL）、灵活且快速的过滤器、重定向器和访问控制器插件，适用于 Squid。它允许您为 Squid 缓存中的不同用户组定义具有不同限制的多个访问规则。`SquidGuard` 使用 Squid 的标准重定向器接口。

`SquidGuard` 可用于以下用途：

- 将某些用户的 Web 访问限制为接受的或众所周知的 Web 服务器或 URL 列表
- 对某些用户阻止访问某些列出或黑名单的 Web 服务器或 URL
- 对某些用户阻止访问匹配正则表达式列表或单词的 URL
- 将被阻止的 URL 重定向到基于 CGI 的“智能”信息页面
- 将未注册用户重定向到注册表单
- 将横幅重定向为空 GIF
- 根据一天中的时间、星期几、日期等设置不同的访问规则
- 为不同用户组设置不同的规则
- 以及更多

`SquidGuard` 或 Squid 不能用于：

- 编辑、过滤或审查文档内部的文本
- 编辑、过滤或审查嵌入 HTML 的脚本语言，如 JavaScript 或 VBscript

### 使用 SquidGuard

从系列 n 安装软件包 `squidguard`。编辑最小的配置文件 `/etc/squidguard.conf`。`http://www.squidguard.org/config/` 中有大量配置示例。稍后可尝试更复杂的配置设置。

下一步是创建一个虚拟的“访问被拒绝”页面或一个或多或少智能的 CGI 页面，以便在客户端请求黑名单网站时重定向 Squid。强烈建议使用 Apache。

现在，告诉 Squid 使用 SquidGuard。在 `/etc/squid.conf` 文件中使用以下条目：

```
redirect_program /usr/bin/squidGuard
```

还有另一个名为 `redirect_children` 的选项，用于配置机器上运行的多少个不同的“重定向”（本例中为 SquidGuard）进程。`SquidGuard` 足够快，可以处理大量请求（`SquidGuard` 速度相当快：在 500MHz Pentium 上，5900 个域名、7880 个 URL、总计 13780 个，10 秒内可处理 100,000 个请求）。因此，不建议设置超过 4 个进程，因为这可能导致为这些进程分配内存而造成不必要的增加。

```
redirect_children 4
```

最后，发送 HUP 信号给 Squid 使其读取新配置：

```
squid -k reconfigure
```

使用浏览器测试您的设置。

## 使用 Calamaris 生成缓存报告

`Calamaris` 是一个 Perl 脚本，用于以 ASCII 或 HTML 格式生成缓存活动报告。它使用原生的 Squid 访问日志文件。`Calamaris` 主页位于 `http://Calamaris.Cord.de/`

该程序的使用相当简单。以 root 登录，然后：

```
cat access.log.files | calamaris [options] > reportfile
```

在管道传输多个日志文件时，日志文件必须按时间顺序排列，较旧的文件在前。

各种选项：

- `-a` 通常用于输出可用报告
- `-w` HTML 报告
- `-l` 报告头部的消息或标志

有关各种选项的更多信息可在手册页中找到

```
man calamaris.
```

一个典型示例是：

```
cat access.log.2 access.log.1 access.log | calamaris -a -w > /usr/local/httpd/htdocs/Squid/squidreport.html
```

这会将报告放在 Web 服务器的目录中。需要 Apache 才能查看报告。

另一个功能强大的缓存报告生成工具是 `SARG`（Squid Analysis Report Generator），包含在系列 n 中。有关此工具的更多信息可在 `http://web.onda.com.br/orso/` 的相关互联网页面中找到。

## 有关 Squid 的更多信息

访问 Squid 的主页 `http://www.squid-cache.org/`。在这里可以找到 Squid 用户指南以及大量关于 Squid 的常见问题解答。

在包 `howtoen` 中，位于 `/usr/share/doc/howto/en/mini/TransparentProxy.gz` 下，有一份关于透明代理的 Mini-Howto。

此外，Squid 的邮件列表可在以下地址获取：

`squid-users@squid-cache.org`.

其归档位于：

`http://www.squid-cache.org/mail_archive/squid_users/`

## SSH — Secure Shell，安全替代方案
