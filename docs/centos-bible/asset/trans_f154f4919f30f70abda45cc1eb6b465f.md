

CentOS5.0-beta5.6.e15.centos Firefox/3.0b5" 127.0.0.1 - [12/Feb/2009:05:21:16 -0500] "GET /icons/apache_pb.gif HTTP/1.1" 200 2326 "http://localhost/" "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9b5) Gecko/2008052519 CentOS/5.0b5-0.beta5.6.e15.centos Firefox/3.0b5" 127.0.0.1 - - [12/Feb/2009:05:21:16 -0500] "GET /icons/powered_by_rh.png HTTP/1.1" 200 1213 "http://localhost/" "Mozilla/5.0 ; Linux i686; en-US; rv:1.9b5) Gecko/200805219 CentOS5.0-beta5.6.e15.centos Firefox/3.0b5" 

Apache 测试页实际上是一种错误状态（403），这表明 Apache 服务器正在运行，但服务器管理员尚未添加主页。接下来的两行显示了分别出现在 CentOS 测试页面上的 Apache（apache_pb.gif）和 CentOS（powered_by_rh.png）图标。

## 分析 Web 服务器流量

*webalizer* 包可以读取 Apache 日志文件并为您的服务器生成使用报告。这些报告以 HTML 格式创建，因此您可以图形化地显示信息。信息以表格和图形两种形式呈现。

要使用 *webalizer* 命令，必须安装 *webalizer* 包（输入 **yum install webalizer**）。您可以不带任何选项运行 Webalizer，让它读取 /etc/webalizer.conf 文件中的值以获取所需的信息。或者，您可以使用命令行选项来覆盖 webalizer.conf 文件中的设置。若要使用默认设置，只需运行以下内容：

```
# webalizer
```

如果一切顺利，命令应该会运行几秒钟然后静默退出。根据 /etc/webalizer.conf 文件中的信息，系统将读取 /var/log/httpd/access_log 日志文件，并将 index.html 文件复制到 /var/www/html/Usage/ 目录。您可以通过在任何浏览器窗口中打开该文件来查看输出。例如，您可以在地址栏中输入以下内容：

```
http://localhost/Usage
```

输出报告显示了 Web 服务器活动的 12 个月摘要。在柱状图中，对于每个月份，绿色柱代表网站命中的次数，深蓝色柱显示被命中的不同文件数量，浅蓝色柱显示打开的页面数量。右侧列还显示了访问次数和访问网站的站点数量的数据。传输的数据量（以千字节为单位）也会显示出来。

图 20-5 展示了一个运行了数月的 Web 服务器的 Webalizer 输出文件示例。

在图表下方，一个表格显示了每个月份的日常和月度活动摘要。用户可以点击月份名称以查看详细活动。

![](img/2f265415ceec72538dd3c78ffca75c10_846_0.png)

> **提示** 由于 Webalizer 支持通用日志格式（CLF）和组合日志格式，因此它可用于显示除 Apache 生成的日志文件以外的其他日志文件的信息。例如，您可以显示 FTP 服务器或 Squid 服务器的统计信息。

还有其他多种软件工具可用于分析传输统计信息。随附的关于 CentOS 系统中可用的统计软件包的边栏介绍了其中的一些工具。

## CentOS 可用的统计软件包

手动分析传输日志并不是什么有趣的事情。已经编写了几个软件包来自动化此任务，包括以下两个：

- **Anolog** — 这款免费的日志文件分析器速度非常快且易于配置，并生成非常详细的输出（包括柱状图和超文本链接）。更多信息可在 www.analog.cx 找到。
- **AWStats** — 高级 Web 统计工具（*awstats* 包）生成代表 Web 服务器访问的图形化统计信息。AWStats 可以处理 Apache 通用日志格式的日志文件，以及来自 Sendmail、FTP 和其他网络服务器的日志文件。它可以报告统计信息，例如访问人数、每人访问次数、每个访问者的域名和国家/地区，以及机器人（robots）的访问次数。

## 摘要

Web 服务器负责存储和向全球各地的客户端提供世界上可用的海量内容。尽管 CentOS 系统有多种 Web 服务器软件包可用，但迄今为止最受欢迎的是 Apache Web 服务器。

本章描述了如何在 CentOS 中安装、配置和运行 Apache 服务器。httpd 守护进程处理 Web 内容（HTTP）请求。配置文件定义了哪些内容可以被共享以及访问方式。特别是，/etc/httpd/conf/httpd.conf 文件用于配置服务器。

Apache httpd 包还包括记录错误和传输消息的设施。您可以在 /etc/httpd/logs 目录中查找 access_log 和 error_log 文件。access_log 文件包含已由服务器处理的请求内容信息。error_log 文件列出了已发生的错误状态和服务被拒绝的时间。您可以使用 Webalizer 等工具简化 Apache 日志数据的查看。

# 第四部分 网络

# 第 21 章

# 设置 LDAP 地址簿服务器

有时，组织需要一种方便的方式来收集、存储和分发信息，以便供需要这些信息的应用程序访问。轻量级目录访问协议（LDAP）简化了为网络就绪应用程序创建和使用信息目录的过程。

LDAP 的意图是简化提供 X.500 规范中描述的目录服务所需的开销。LDAP 是 X.500 功能的一个子集。通过标准化数据库信息的结构，LDAP 可以绕过专有的存储格式，从而允许许多不同的应用程序共享相同的数据。

> **注意** X.500 是一项 CCITT 规范，已成为开放系统互连（OSI）标准的一部分，这些标准定义了连接网络和相关服务的分层框架。随着 TCP/IP 网络（如互联网）在世界范围内的主导地位，OSI 从未成为某些人预期的主导网络框架。尽管如此，七层 OSI 参考模型经常用于课堂中教授网络理论。同样，其中一些规范，如 X.500，在一些需要标准、跨平台功能的地方已被采用（有时是调整采用）。

CentOS 系统包含 OpenLDAP 软件包，用于实现 LDAP 服务器和客户端服务。为了说明如何使用 OpenLDAP 配置和使用 LDAP 服务器并使其对用户应用程序可访问，本章将介绍在 CentOS 系统上设置共享地址簿的过程。它还描述了如何使用可以访问 LDAP 地址簿的电子邮件客户端。

**本章内容**

- 了解 LDAP
- 使用 OpenLDAP
- 配置 LDAP 服务器
- 创建 LDAP 地址簿
- 使用 Thunderbird 访问地址簿

## 了解 LDAP

LDAP 允许人们创建可以在网络上共享给客户端应用程序的信息目录。它特别适用于那些反复查找相对稳定信息的应用程序（换句话说，信息被查看的次数多于被更改的次数）。这就是为什么 LDAP 常用于存储关于人员、地址和其他可能需要高访问频率但变更较少的数据。

由于 LDAP 极其灵活的设计，作为 LDAP 开发人员或管理员，您可以对以下方面拥有很大的控制权：

- 目录中信息的组织方式。
- 信息如何访问以及由谁访问。
- 信息分发的规模，从本地到全球。（信息可以复制到您选择的任何规模的其他服务器上，并自动同步。）

例如，LDAP 地址簿可能类似于以下内容：

```text
dc=example,dc=com
    ou=members
        cn=Andrew Smith
            homeAddress
            homeTelephone
            workAddress
            workTelephone
        cn=John Wilson
            homeAddress
            homeTelephone
            workAddress
            workTelephone
    ...
```

然而，尽管具有灵活性，您无需从头开始设计创建的每个目录。LDAP 有许多预定义的信息结构可供依赖，以构建您的 LDAP 目录。

> **提示** 微软的 Active Directory（AD）通常被称为基于“LDAP”的实体，这让一些用户对整合 OpenLDAP 和 AD 抱有极高的期望。虽然可以在 AD 和 OpenLDAP 之间交换信息，但设置这需要大量的耐心和技巧。除非您必须与 AD 互操作，否则支持 Windows 客户端的更好途径是通过使用 OpenLDAP 和 Samba。

