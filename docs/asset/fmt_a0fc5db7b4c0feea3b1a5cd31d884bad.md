
`FW_REDIRECT_UDP="192.168.0.0/16,0/80,3128 192.168.0.0/16,0,21328"`

启动防火墙并使用新配置启动，更改 `/etc/sysconfig/SuSEfirewall2` 文件中的一个条目。`Start_FW` 条目必须设置为 `"yes"`。

按照第 429 页的“Starting Squid”所示所示启动 Squid。如果一切运行正常，请检查 `/var/log/squid/access.log` 中的 Squid 日志。

要验证所有端口是否配置正确，请从网络外的任何计算机对该机器进行端口扫描。只有 Web 服务端口 (`80`) 应该是开启的。使用 `nmap` 扫描端口，命令语法为 `nmap -O IP_address`。

# Squid 和其他程序

接下来查看其他应用程序如何与 Squid 交互。`cachemgr.cgi` 允许系统管理员检查缓存对象所需的内存。`squidGuard` 过滤网页。`Calamaris` 是 Squid 的报告生成器。

## cachemgr.cgi

缓存管理器 (`cachemgr.cgi`) 是一个显示运行中的 Squid 进程内存使用统计的 CGI 工具。它也是一种更方便的管理缓存和查看统计的方法，无需登录服务器。

### 设置

首先，你的系统中需要一个运行的 Web 服务器。要检查 Apache 是否已运行，以 root 身份输入 `rpcache status`。

如果出现如下消息：

Checking for service httpd: OK

Server uptime: 1 day 18 hours 29 minutes 39 seconds

Apache 正在你的机器上运行。否则，输入 `rcapache start` 使用 SuSE Linux 默认设置启动 Apache。设置的最后一步是将文件 `cachemgr.cgi` 复制到 Apache 的 cgi-bin 目录：

```
cp /usr/share/doc/packages/squid/scripts/cachemgr.cgi
/srv/www/cgi-bin/
```

# /etc/squid/squid.conf 中的缓存管理器 ACLs

原始文件中某些缓存管理器所需的默认设置：

```
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255
```

配合以下规则：

```
http_access allow manager localhost
http_access ACL deny manager
```

第一个 ACL 是最重要的，因为缓存管理器尝试通过 `cache_object` 协议与 Squid 通信。

以下规则假设 Web 服务器和 Squid 运行在同一台机器上。如果缓存管理器和 Squid 之间的通信源于另一台计算机上的 Web 服务器，请像示例所示包含一个额外的 ACL。

```
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255
acl webserver src 192.168.1.255.255.255
```

# 文件 57：访问规则

然后按照第 58 页添加规则。

```
http_access allow manager localhost
http_access allow webserver
http_access deny manager
```

# 文件 58：访问规则

为管理器配置密码，以便访问缓存并查看更多信息。这位于 `/etc/squid/squid.conf` 中的注释中。

每当配置文件更改时，重启 Squid。可以通过 `rsquid reload` 轻松完成。

# 查看统计信息

访问://webserver.org/cgi-bin/cachemgr.cgi

点击“继续”并浏览不同的统计数据。每个条目的更多详细信息见 Squid FAQ

# squidGuard

`squidGuard` 是 Squid 的免费、灵活且快速的过滤器、重定向和访问控制器插件。它允许为用户组定义多个访问规则。`squidGuard` 使用 Squid 标准重定向接口。

`squidGuard` 可用于：

- 限制某些用户访问列表中的已知 Web 服务器

- 禁止某些用户访问黑名单中的 Web 服务器

- 禁止某些用户访问匹配正则表达式或单词的 URL

- 将被阻止的 URL 重定向到“智能” CGI 页面

- 将未注册用户重定向到注册表

- 根据时间、星期、日期等设置不同的访问规则

- 为不同的用户组设置不同的规则

SquidGuard 或 Squid 都无法：

- 编辑、过滤或审查嵌入 的脚本语言，如 JavaScript 或 VScript

## 使用 squidGuard

安装 `squidGuard` 软件包。编辑最小配置文件 `/etc/squidguard.conf`。http://www.squguard.org/config/ 有许多配置示例。以后尝试更复杂的配置设置。

下一步创建一个虚拟的“拒绝访问”页面或智能智能 CGI 页面，以便客户端请求黑名单网站时重定向 Squid。强烈建议使用 Apache。

现在告诉 Squid 使用 `squidGuard`。在 `/etc/squid.conf` 文件中使用以下条目：

`redirect_program /usr/bin/squidGuard`

另一个选项是 `redirect_children`，用于配置机器上运行多少个“重定向”（在此例中为 SquidGuard）进程。SquidGuard 的速度足以应对请求（在 500MHz Pentium 上 10 秒内处理了 10 万次请求，涉及 5900 个域名、7880 个 URL，总计 13780 个）。

因此，不建议设置超过 4 个进程，因为这可能会导致分配这些进程的内存不必要增加。

`redirect_children 4`

最后，运行 `rsquid reload` 让 Squid 读取其新配置。现在，用浏览器测试你的设置。

### 使用 Calamaris 生成缓存报告

`Calamaris` own Perl 脚本，用于生成 ASCII 或 HTML 格式的缓存活动报告。它可以与原生的 Squid 访问日志文件配合工作。`Calamaris` 主页位于 http://Calamaris.cord.de/。

该程序的使用非常简单。以 root 身份登录，然后输入：

```
cat access.log.files | calamaris [options] > reportfile
```

在管道传输多个日志文件时，确保日志文件按时间顺序排序（旧文件在前）是非常关重要的。

各种选项如下：

- `-a`：通常用于输出可用的报告

- `-w`：HTML 报告

- `-l`：在报告头中显示消息或标志

关于各种选项的更多信息，可以通过执行 `man calamaris` 找到。

一个典型的示例：

```
cat access.log.2 access.log.1 access.log | calamaris -a -w > /usr/local/httpd/htdocs/Squid/squidreport.html
```

这会将报告放在 Web 服务器的目录中。查看报告需要 Apache。

另一个缓存报告生成工具是 SARG（Squid 分析报告生成器）。关于此的更多信息可以在相关的网络页面 http://web.onda.com.br/orso/ 找到。

# 关于 Squid 的更多信息

访问 Squid 的主页 http://www.squid-cache.org/。在这里，你可以找到 Squid 用户指南以及大量关于 Squid 的常见问题解答（FAQs）。

软件包 `howto /usr/share/doc/howto/en/mini/TransparentProxy.gz` 中有一个关于透明代理的 Mini-Howto。

此外，Squid 提供了邮件列表，地址为 `squid-users@squid-cache.org`。其归档文件位于：http://www.squid-cache.org/mail-archive/squid-users/

## 网络安全

伪装（Masquerading）、防火墙和 Kerberos 构成了安全网络的基础，能够控制数据流量。安全外壳（SSH）允许用户通过加密连接登录到远程主机。本章的信息为安全网络以及使用这些工具在网络中安全工作提供了基础。

- 伪装与防火墙 . . . . . . . . . . . . . . . . . . . . . . 444

- SSH — 安全外壳，安全的替代方案 . . . . . . . . . . . . . . . . 450

- 网络身份验证 — Kerberos . . . . . . . . . . . . . . . . 455

- 安装与管理 Kerberos . . . . . . . . . . . . . . . . . . 462
