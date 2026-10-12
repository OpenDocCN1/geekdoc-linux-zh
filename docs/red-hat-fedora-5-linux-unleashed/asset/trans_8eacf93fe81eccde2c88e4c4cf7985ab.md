
## OpenGroupware（原 SKYrix 4.1）

OpenGroupware（与 OpenOffice.org 无隶属关系）专注于团体办公和协作（并且不提供自己的邮件服务器）。它可以替代 SuSE OpenExchange 中的 Comfire 以节省授权费用，或者配合 Cyrus-imap 邮件服务器以及 PostgreSQL 和 FrontBase（不支持 MySQL）作为数据库使用。为了连接 Outlook，OpenGroupware 使用 ZedeLook MAP I Storage Provider（专有软件，它将 MAP I 映射到 WebDAV）和开源 WebDAV 中间件服务器 ZideStore。ZideStore 将 WebDAV 请求转换为对 OpenGroupware 的调用，同时也支持 Evolution 和 Mozilla 等客户端。主页地址为 http://www.opengroupware.org/en/。

## phpgroupware

phpgroupware 是一个用 PHP 编写的开源应用程序（配合 MySQL 或 postgresql 数据库、Web 服务器以及 IMAP 邮件服务器使用）。phpgroupware 提供基于 Web 的日历、任务列表、通讯录、电子邮件、新闻标题和文件管理器。主页地址为 http://www.phpgroupware.org/。

## PHPprojekt

PHPprojekt 是用 PHP 编写的开源软件（配合 MySQL、postgresql、Oracle、Informix 或 MS-SQL 使用）。PHPprojekt 提供日历、联系人管理器、工时卡系统、项目管理、在线聊天、线程讨论论坛、故障工单系统、电子邮件、公共文件、笔记书签、投票系统、任务列表、提醒、网站搜索以及与 PostNuke 新闻站点应用程序的集成。它完全不提供任何 Exchange/Outlook 兼容性。主页地址为 http://www.PHPprojekt.com/。

## IMP/ Horde

IMP/ Horde 是一个基于 PHP 的应用框架。当与 HTTP 服务器（Apache、Microsoft IIS、Netscape）和 MySQL 数据库结合使用时，IMP/ Horde 提供模块，实现 Webmail、联系人管理器、日历、CVS 查看器、文件管理器、时间跟踪、邮件过滤规则管理器、笔记、任务、聊天、新闻组、表单、Bug 跟踪、FAQ 库以及演示文稿功能。主页地址为 http://www.horde.org/。

## 结论

没有纯开源的替代方案能为 MS Outlook 客户端提供完整的 Exchange 类服务。如果你没有需要担心的 Outlook 客户端，OpenGroupware、IMP/ Horde 和 phpprojekt 看起来很有前景。它们都没有在 Fedora 中提供。

## 相关的 Fedora 和 Linux 命令

你将使用以下命令在 Fedora 中管理电子邮件：

- balsa— 一个适用于 X 的 GNOME 邮件用户代理
- biff— 一个基于控制台的邮件通知实用程序
- evolution— 一个功能全面的 Ximian GNOME X 邮件 PIM
- fetchmail— 一个基于控制台和守护进程模式的 Linux 邮件检索命令
- fetchmailconf— 一个适用于 X 的图形化 fetchmail 配置客户端
- kmail— 一个适用于 KDE 和 X 的图形化邮件用户客户端
- kedit— 一个适用于 KDE 和 X 的邮件小程序
- mail— 一个基于控制台的邮件用户代理
- mutt— 一个基于控制台的邮件用户代理
- sendmail— 一个适用于 UNIX 和 Linux 的全面邮件传输代理
- xbiff— 一个邮件通知 X 客户端

## 参考资料

以下是推荐的电子邮件配置阅读材料。当然，并非所有参考资料都适用于你。请选择适用于你正在使用的邮件服务器的资料。

### 网络资源

- http://www.sendmail.org/— 这是 Sendmail 的主页。你可以在这里找到关于 Sendmail MTA 的配置信息和常见问题解答。
- http://www.postfix.org/— 这是 Postfix 的主页。如果你正在使用 Postfix MTA，可以在该站点找到文档和示例配置。
- http://www.qmail.org/— 这是 Qmail MTA 的主页。它包含关于 Qmail 的文档和其他资源链接。
- http://www.linuxgazette.com/issue/35/ac.html— Linux 上的 IMAP：实用指南。互联网邮件访问协议允许用户访问存储在远程服务器上的电子邮件，而不是本地磁盘。
- http://www.redhat.com/support/resources/faq/RH-postfix-FAQ/book1.html— 一篇稍显过时但仍有很大用的 HOWTO，关于在 Red Hat 环境中设置 Postfix。
- http://www.imap.org/about/whatisIMAP.html— 一个描述 IMAP 是什么的页面。
- http://www.rfc-editor.org/— 一个 RFC 库— 请求意见— 定义了现代计算机使用的技术“规则”。
- http://www.procmail.org/— Procmail 的主页。
- http://www.moongroup.com/docs/procmail/— Procmail 常见问题解答，包括故障排除建议。该页面还引用了一个链接页面，进而引用其他链接集合以及来自 Procmail 邮件列表的片段。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/Other-formats/html_single/Qmail-VxMailMgr-Courier-imap-HOWTO.html— 如果你需要一些帮助来配置基于较少使用的应用程序的邮件系统，这个 HOWTO 可以提供帮助。

### 书籍

O'Reilly 出版社的《*Sendmail*》。这是 Sendmail 所有方面的事实标准指南。它包含 1000 多页内容，让你意识到 Sendmail 实际上是多么复杂。

Sams 出版社的《*Postfix*》。一本涵盖 Postfix MTA 的优秀书籍。

Sams 出版社的《*Running Qmail*》。这与 Sams 出版社的 Postfix 书类似，只不过它涵盖的是 Qmail MTA。

## 第 26 章

## 设置代理服务器

在这个世界上有两样东西是你永远无法拥有足够的：时间和带宽。Fedora 附带一个代理服务器— Squid— 它允许你在服务器上缓存 Web 流量，从而加快网站加载速度并减少用户的带宽消耗。

### 什么是代理服务器？

代理服务器位于客户端机器— 你公司的台式机— 和互联网之间。当客户端请求网站时，它们不直接连接到 Web 并发送 HTTP 请求。相反，它们连接到本地代理服务器。然后代理将它们的请求转发到 Web，获取结果，并将其返回给客户端。在最简单的层面上，代理服务器确实只是客户端和服务器之间的额外一层，为什么要麻烦呢？

部署代理服务器的三个主要原因是

- **内容控制**— 你想阻止人们在工作时间阅读新闻或下载 MP3 来消磨时间。
- **速度**— 你想缓存常见网站以最大限度地利用你的带宽。
- **安全**— 你想监控人们正在做什么。

Squid 能够实现所有这些目标以及更多。

### 本章内容

- 什么是代理服务器？
- 安装 Squid
- 配置客户端
- 访问控制列表
- 指定客户端 IP 地址
- 示例配置
- 参考资料

### 安装 Squid

Squid 的安装通过添加/删除软件对话框处理。Squid 包令人困惑地位于 Web 服务器组下；缺点是无论你喜不喜欢，它都会同时安装 Apache 和 Squid。话虽如此，你可以（并且应该）从 Web 服务器类别中取消选择其他你不需要自动启动的包。

安装完 Squid 后，切换到控制台并使用 su 获取 root 账户。你应该运行命令 `chkconfig --level 345 squid on` 以在运行级别 3、4 和 5 下运行 Squid，如下所示：

```
[root@susannah ~]# chkconfig --list squid
squid     0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root@susannah ~]# chkconfig --level 345 squid on
[root@susannah ~]# chkconfig --list squid
squid     0:off 1:off 2:off 3:on 4:on 5:on 6:off
```

这会在系统下次切换到运行级别 3、4 或 5 时运行 Squid，但此时它尚不会运行。

### 配置客户端

在配置新的 Squid 服务器之前，你应该设置本地 Web 浏览器使用 Squid 进行 Web 访问。这允许你在处理配置文件时测试你的规则。

要配置 Firefox，请从编辑菜单选择首选项。从出现的对话框中，点击连接设置按钮（在“常规”选项卡底部附近），并选择选项手动代理配置。勾选下方的方框，所有协议使用相同代理；然后输入 127.0.0.1 作为 IP 地址，3128 作为端口号。参见图 26.1 查看应有的样子。如果你正在配置远程客户端，请指定 Squid 服务器的 IP 地址而不是 127.0.0.1。

对于 Konqueror，进入设置菜单并选择配置 Konqueror。从左侧选项卡，向下滚动到代理，选择手动指定代理设置，然后点击设置。输入 127.0.0.1 作为代理 IP 地址，3128 作为端口。与 Firefox 一样，如果你正在配置远程客户端，请指定 Squid 服务器的 IP 地址而不是 127.0.0.1。

Internet Explorer 的代理设置在 工具/Internet 选项 中。从“连接”选项卡，点击 LAN 设置按钮并启用 使用你的局域网代理服务器 选项。将地址输入为你的 Squid 机器的 IP，然后指定 3128 作为端口。

