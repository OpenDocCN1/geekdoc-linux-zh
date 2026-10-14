
第一个 ACL 最为重要，因为缓存管理器尝试通过 cache_object 协议与 Squid 通信。
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

为管理器配置密码以访问更多选项，如远程关闭缓存或查看有关缓存的更多信息。为此，请为管理器配置条目 cachemgr_passwd 的密码以及要查看的选项列表。该列表作为 /etc/squid.conf 中条目注释的一部分出现。
每次配置文件更改时，使用选项 -k reconfigure 重启 Squid。

## 查看统计信息

前往对应的网站：
http://webserver.example.org/cgi-bin/cachemgr.cgi
按“继续”并浏览不同的统计信息。缓存管理器显示的每个条目的更多详细信息可在 Squid FAQ 中找到，网址为 http://www.squid-cache.org/Doc/FAQ/FAQ-9.html

## SquidGuard

本节无意详细介绍 SquidGuard 的配置，仅介绍它并提供使用建议。有关更深入的配置问题，请参阅 SquidGuard 网站 http://www.squidguard.org

SquidGuard 是一个免费（GPL）、灵活且快速的过滤器、重定向器和访问控制器插件，适用于 Squid。它允许您为 Squid 缓存中的不同用户组定义具有不同限制的多个访问规则。SquidGuard 使用 Squid 的标准重定向器接口。

SquidGuard 可用于以下用途：
-   将某些用户的 Web 访问限制为接受的或众所周知的 Web 服务器或 URL 列表
-   对某些用户阻止访问某些列出或黑名单的 Web 服务器或 URL
-   对某些用户阻止访问匹配正则表达式列表或单词的 URL
-   将被阻止的 URL 重定向到基于 CGI 的“智能”信息页面
-   将未注册用户重定向到注册表单
-   将横幅重定向为空 GIF
-   根据一天中的时间、星期几、日期等设置不同的访问规则
-   为不同用户组设置不同的规则
-   以及更多

SquidGuard 或 Squid 不能用于：
-   编辑、过滤或审查文档内部的文本
-   编辑、过滤或审查嵌入 HTML 的脚本语言，如 JavaScript 或 VBscript

## 使用 SquidGuard

从系列 n 安装软件包 squidguard。编辑最小的配置文件 /etc/squidguard.conf。http://www.squidguard.org/config/ 中有大量配置示例。稍后可尝试更复杂的配置设置。

下一步是创建一个虚拟的“访问被拒绝”页面或一个或多或少智能的 CGI 页面，以便在客户端请求黑名单网站时重定向 Squid。强烈建议使用 Apache。

现在，告诉 Squid 使用 SquidGuard。在 /etc/squid.conf 文件中使用以下条目：

```
redirect_program /usr/bin/squidGuard
```

还有另一个名为 redirect_children 的选项，用于配置机器上运行的多少个不同的“重定向”（本例中为 SquidGuard）进程。SquidGuard 足够快，可以处理大量请求（SquidGuard 速度相当快：在 500MHz Pentium 上，5900 个域名、7880 个 URL、总计 13780 个，10 秒内可处理 100,000 个请求）。因此，不建议设置超过 4 个进程，因为这可能导致为这些进程分配内存而造成不必要的增加。

```
redirect_children 4
```

最后，发送 HUP 信号给 Squid 使其读取新配置：

```
squid -k reconfigure
```

使用浏览器测试您的设置。

## 使用 Calamaris 生成缓存报告

Calamaris 是一个 Perl 脚本，用于以 ASCII 或 HTML 格式生成缓存活动报告。它使用原生的 Squid 访问日志文件。Calamaris 主页位于 http://Calamaris.Cord.de/

该程序的使用相当简单。以 root 登录，然后：

```
cat access.log.files | calamaris [options] > reportfile
```

在管道传输多个日志文件时，日志文件必须按时间顺序排列，较旧的文件在前。
各种选项：
-   `-a` 通常用于输出可用报告
-   `-w` HTML 报告
-   `-l` 报告头部的消息或标志

有关各种选项的更多信息可在手册页中找到

```
man calamaris.
```

一个典型示例是：

```
cat access.log.2 access.log.1 access.log | calamaris -a -w \
  >/usr/local/httpd/htdocs/Squid/squidreport.html
```

这会将报告放在 Web 服务器的目录中。需要 Apache 才能查看报告。

另一个功能强大的缓存报告生成工具是 SARG（Squid Analysis Report Generator），包含在系列 n 中。有关此工具的更多信息可在 http://web.onda.com.br/orso/ 的相关互联网页面中找到。

## 有关 Squid 的更多信息

访问 Squid 的主页 http://www.squid-cache.org/。在这里可以找到 Squid 用户指南以及大量关于 Squid 的常见问题解答。

在包 howtoen 中，位于 /usr/share/doc/howto/en/mini/TransparentProxy.gz 下，有一份关于透明代理的 Mini-Howto。

此外，Squid 的邮件列表可在以下地址获取：
squid-users@squid-cache.org.

其归档位于：
http://www.squid-cache.org/mail_archive/squid_users/

## SSH — Secure Shell，安全替代方案

在网络日益增多的时代，访问远程系统也变得越来越常见。无论活动如何，访问系统的人员必须经过身份验证。

大多数用户现在应该知道用户名和密码仅用于个人使用。雇主、计算机中心或服务提供商之间通常保证个人数据的严格保密。然而，以明文形式进行身份验证和传输数据的持续做法是一种令人恐惧的现象。受影响最直接的是常用的服务，即用于检索邮件的邮局协议（POP）和用于登录远程系统的 telnet。使用这些方法，用户信息和被视为敏感的数据（如信件内容或通过 talk 命令进行的聊天）会以开放且不安全的方式在网络上传输。这侵犯了用户的隐私，并使此类访问方法容易被滥用。通常，这种滥用是通过访问一个系统来攻击另一个系统或获取管理员或 root 权限发生的。

参与数据传输或在本地网络上运行的任何设备，如防火墙、路由器、交换机、邮件服务器或工作站，也都可以访问数据。虽然有法律禁止此类行为，但很难检测到。

SSH 软件提供了必要的保护。完整的身份验证，通常是用户名和密码，以及通信都被加密。即使在这里，窃取传输的数据也是可能的，但入侵者没有密钥就无法破译内容。这使得通过不安全的网络（如互联网）进行安全通信成为可能。在 SuSE Linux 中，OpenSSH 软件包可在 sec 系列中找到。

## OpenSSH 软件包

安装 OpenSSH 软件包后，以下程序将可用：ssh、scp 和 sftp，作为 telnet、rlogin、rsh、rcp 和 ftp 的替代方案。

## ssh 程序

使用 ssh 程序，可以登录远程系统并进行交互式工作。它同时取代了 telnet 和 rlogin。符号名称 login 指向 ssh。例如，通过输入 `ssh sun` 登录到主机 sun。然后系统会提示您输入 sun 系统上的密码。

身份验证成功后，可在该处从命令行工作或使用交互式应用程序。如果本地用户名与远程用户名不同，请使用不同的登录名登录，命令为 `ssh -l augustine sun` 或 `ssh augustine@sun`。

此外，ssh 提供了在另一系统上运行命令的选项，与 rsh 类似。在以下示例中，我们将在主机 sun 上运行 uptime 命令并创建一个名为 tmp 的目录。程序输出将显示在主机 earth 的本地终端上。

```
hannah@earth:~> ssh sun 'uptime; mkdir tmp' hannah@sun password:
1:21am up 2:17, 9 users, load average: 0.15, 0.04, 0.02
```

这里需要使用单引号来一次性发送两个指令。

## scp — 安全复制

scp 将文件复制到远程机器。它是 rcp 的安全且加密的替代品。例如，`scp MyLetter.tex sun:` 将文件 MyLetter.tex 从机器 earth 复制到机器 sun。要指定不同的用户名，请使用 username@machine 格式。

输入正确的密码后，scp 开始数据传输并显示一系列星号，逐渐从左到右标记进度。此外，预计到达时间将显示在右侧边距。所有输出都可以通过使用选项 `-q` 来抑制。

scp 还提供了用于整个目录的递归复制功能。

```
scp -r src/ sun:backup/
```

将目录 src/ 的全部内容，包括所有子目录，复制到机器 sun 的 backup/ 子目录中。如果该子目录尚不存在，将自动创建。

通过选项 `-p`，scp 保持文件的时间戳不变。`-C` 压缩数据传输。这最大限度地减少了需要传输的数据量，但会给处理器带来更大的负担。
