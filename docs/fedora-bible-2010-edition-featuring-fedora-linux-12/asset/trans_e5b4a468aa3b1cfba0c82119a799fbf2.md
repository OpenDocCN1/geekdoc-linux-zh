
```
:1: - - [11/Nov/2009:17:20:04 -0600] "GET / HTTP/1.1" 403 3918
"-" "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.1.3)
Gecko/20090911 Fedora/3.5.3-1.fc12 Firefox/3.5.3"
:1: - [11/Nov/2009:17:20:04 -0600] "GET /icons/apache_pb2.gif HTTP/1.1" 200 1797
"http://localhost/" "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.1.3)
Gecko/20090911 Fedora/3.5.3-1.fc12 Firefox/3.5.3"
:1: - [11/Nov/2009:17:20:04 -0600] "GET /icons/poweredby.png HTTP/1.1" 200 3034
"http://localhost/" "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.1.3)
Gecko/20090911 Fedora/3.5.3-1.fc12 Firefox/3.5.3"
```

Apache 测试页面实际上是一个错误状态（403），这表明 Apache 服务器正在运行，但服务器管理员尚未添加主页。接下来的两行分别显示了 Fedora 测试页面上出现的 Apache（apache_pb2.gif）和 Fedora（poweredby.png）图标。

查看 server-info 和 server-status 页面（分别如图 20-3 和 20-4 所示）时，生成了以下条目：

```
127.0.0.1 - - [26/Nov/2008:23:40:41 -0400] "GET /server-info HTTP/1.1"
200 113446 "-" "Mozilla/5.0 (X11; U; Linux i686; en-US;
rv:1.9.1.3) Gecko/20090911 Fedora/3.5.3-1.fc12 Firefox/3.5.3"
127.0.0.1 - [26/Nov/2008:23:41:49 -0400] "GET /server-status
HTTP/1.1" 200 2582 "-" "Mozilla/5.0 (X11; U; Linux i686; en-US;
rv:1.9.1.3) Gecko/20090911 Fedora/3.5.3-1.fc12 Firefox/3.5.3"
```

试图访问 server-status 页面被拒绝时，记录了以下一行日志（注意 403 服务器响应代码）：

```
127.0.0.1 - - [26/Nov/2008:23:43:07 -0400] "GET /server-status
HTTP/1.1" 403 211 "-" "Mozilla/5.0 (X11; U; Linux i686; en-US;
rv:1.9.1.3) Gecko/20090911 Fedora/3.5.3-1.fc12 Firefox/3.5.3"
```

## 分析 Web 服务器流量

webalizer 包可以读取 Apache 日志文件并生成服务器使用报告。这些报告以 HTML 格式创建，以便您能够在浏览器中阅读信息。信息以表格和图表两种形式呈现。

要使用 webalizer 命令，必须安装 webalizer 包（yum install webalizer）。您可以不带任何选项运行 webalizer，让它读取 /etc/webalizer.conf 文件中的值以获取所需信息。或者，您可以使用命令行选项来覆盖 webalizer.conf 文件中的设置。若要使用默认值，只需运行以下命令：

```
# webalizer
```

> **提示：** 如果您看到类似“未找到有效记录！”（No valid records found!）的错误，这意味着您的 httpd 服务器尚未处理任何请求。

如果一切顺利，该命令应运行片刻后静默退出。根据 /etc/webalizer.conf 文件中的信息，系统会读取 /var/log/httpd/access_log 文件，并将一个 index.html 文件复制到 /var/www/html/usage/ 目录。您可以打开任意浏览器窗口查看该文件中的输出结果。例如，您可以在地址栏中输入以下内容：

```
http://localhost/usage
```

输出报告显示了 Web 服务器活动情况的 12 个月摘要。在柱状图中，每个月的绿色柱代表对网站的命中次数（hits），深蓝色柱表示不同文件的命中次数，浅蓝色柱表示打开的页面数。此外，右侧列还显示了访问次数和访问该网站的站点数量的数据。同时也会显示传输的数据量（以千字节为单位）。

图 20-5 展示了一个 Web 服务器仅运行很短时间的 webalizer 输出文件示例。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_831_0.png)

**图 20-5**：Webalizer 以图表和列表格式显示 Web 数据。

在图表下方，一个表格显示了每个月活动的每日和每月摘要。用户可以点击月份名称来查看详细活动。

> **提示：** 由于 Webalizer 同时支持通用日志格式（CLF）和组合日志格式，因此可用于显示除 Apache 生成的日志文件以外的其他日志文件的信息。例如，您可以显示 FTP 服务器或 Squid 服务器的统计信息。

还有其他一些软件工具可用于分析传输统计信息。关于 Fedora 可用的统计软件包的随附边栏描述了其中一些工具。

## Fedora 可用的统计软件包

手动分析传输日志并不太有趣。已经编写了若干软件包来自动化此任务，其中包括以下两个：

- **Analog** —— 这款免费的日志文件分析器速度非常快且易于配置，并能生成非常详细的输出（包括条形图和超链接）。更多信息请访问 http://www.analog.cx。
- **AWStats** —— Advanced Web Statistics 工具（awstats 包）生成表示 Web 服务器访问情况的图形统计信息。AWStats 可以处理 Apache 通用日志格式以及来自 sendmail、FTP 和其他网络服务器的日志文件。它可以报告统计信息，例如访问人数、每个人进行的访问次数、每位访问者的域名和国家/地区，以及机器人（bots）进行的访问次数。您可以访问 http://awstats.sourceforge.net 查找更多信息。

## 本章小结

Web 服务器负责存储并向全球各地的客户端提供万维网上可用的大量内容。虽然 Fedora 系统有几种可用的 Web 服务器软件包，但 Apache Web 服务器无疑是其中最受欢迎的。

本章介绍了如何在 Fedora 中安装、配置和运行 Apache 服务器。`httpd` 守护进程负责处理对 Web 内容（HTTP）的请求。配置文件定义了哪些内容可供访问以及如何访问这些内容。特别是，`/etc/httpd/conf/httpd.conf` 文件用于配置服务器。

Apache `httpd` 包还包括用于记录错误和传输消息的设施。您可以在 `/var/log/httpd` 目录中查找 `access_log` 和 `error_log` 文件。`access_log` 文件包含已由服务器处理的内容请求信息。`error_log` 文件列出了发生的错误状态以及拒绝服务的时间。您可以使用 Webalizer 等工具来简化 Apache 日志数据的查看。

# 第 21 章

## 设置 LDAP 地址簿服务器

**本章内容**

- 了解 LDAP
- 使用 OpenLDAP
- 配置 LDAP 服务器
- 创建 LDAP 地址簿
- 使用 Thunderbird 访问地址簿

有时，组织需要一种便捷的方式来收集、存储和分发信息，以便需要使用该信息的应用程序访问。轻量级目录访问协议（LDAP）简化了网络就绪应用程序创建和使用信息目录的过程。

LDAP 旨在简化 X.500 规范中描述的目录服务所需的开销。LDAP 是 X.500 功能的一个子集。通过标准化数据库信息的结构，LDAP 可以绕过专有存储格式，从而允许许多不同的应用程序共享数据。

> **注意：** X.500 是 CCITT 的一项规范，已成为开放系统互连（OSI）标准的一部分，这些标准定义了用于互连网络及相关服务的分层框架。随着 TCP/IP 网络（如互联网）在世界上的主导地位，OSI 并未成为某些人预期的那种主导网络框架。尽管如此，七层 OSI 参考模型仍常在课堂上用于教授网络理论。同样，其中一些规范（如 X.500）在需要标准的跨平台功能时已被采用（有时经过改编）。

Fedora 包含用于实现 LDAP 服务器和客户端服务的 OpenLDAP 软件包。为了说明如何使用 OpenLDAP 配置和使用 LDAP 服务器并将其对用户应用程序开放访问，本章介绍了在 Fedora 系统上设置共享地址簿的过程。它还描述了如何使用可以访问 LDAP 地址簿的电子邮件客户端。

