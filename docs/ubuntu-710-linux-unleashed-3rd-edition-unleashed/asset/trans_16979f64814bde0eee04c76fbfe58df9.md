

Zope 与 Apache 的不同之处在于它是通过一个完全基于网络的图形界面进行管理的。对于那些对仅命令行界面不感兴趣的人来说，这具有广泛的吸引力。

Zope 是 Zope Corporation（前身为 Digital Creations）的产品，该公司也是 Python 编程语言的创造者。与所有开源事物一样，它是免费的。有关 Zope 的信息可以在 http://www.zope.com（商业版）和 http://www.zope.org（开源版）找到。

## Zeus Web Server

Ubuntu 站点也可以使用 Zeus Technology 的 Zeus Web Server。该服务器提供可扩展的 SSL 实现、跨多个网站的安全设置以及在线管理服务器。当前价格为一台最多配备两颗 CPU 的主机平台 1,700 美元，但通过 Zeus Load Balancer 进行负载平衡的费用为（截至撰写时）每对负载平衡计算机 12,000 美元。

您可以在 http://www.zeus.com/products/zws/ 获取有关 Zeus Web Server 的更多信息。

## Related Ubuntu and Linux Commands

在 Ubuntu 中管理 Apache Web 服务器时，您将使用以下命令：

- apache2ctl—随 Apache 提供的服务器控制 shell 脚本
- apache2—Apache Web 服务器
- konqueror—KDE 的图形网页浏览器
- elinks—基于文本的、带图形菜单的网页浏览器
- firefox—首屈一指的开源网页浏览器

## Reference

网上有大量关于 Apache 的文档。有关 Apache 以及本章讨论的主题的更多信息，请查看以下资源：

- http://news.netcraft.com/archives/web_server_survey.html—数百万台服务器的 Web 服务器使用统计图。研究指出 Apache 是互联网站点使用最广泛的服务器。
- http://www.apache.org/—在 Apache 项目网站上可以获得关于 Apache 的大量文档和信息。
- http://www.apacheweek.com/—您可以在 Apache Week 网站上获得关于 Apache 的最新新闻和优秀技术文章。
- http://apachetody.com/—另一个优秀的 Apache 网站。Apache Today 网站上可以找到原创内容以及指向其他网站上 Apache 相关报道的链接。
- http://www.hwg.org/—HTML、CGI 及相关主题可在 HTML Writers Guild 网站上获得。
- http://modules.apache.org/—可在 Apache Module Registry 网站上找到 Apache 的可用附加模块。

关于 Apache 有几本好书。例如，《Apache Server Unleashed》（Sams Publishing），ISBN 0-672-31808-3。

有关 Zope 的更多信息，请参阅《The Zope Book》（New Riders Publishing），ISBN 0-7357-11372。

## CHAPTER 18

## Remote File Serving with FTP

### IN THIS CHAPTER

- Choosing an FTP Server
- Installing FTP Software
- The FTP User
- inetd Configuration for wu-ftpd
- Configuring the Very Secure FTP Server
- Configuring the Wu-FTPd Server
- Using Commands in the ftpaccess File to Configure wu-ftpd
- Configure FTP Server File-Conversion Actions
- Using ftphosts to Allow or Deny FTP Server Connection
- Using Commands for Server Administration
- Reference

文件传输协议（FTP）曾经被认为是从一台计算机到另一台计算机通过网络传输文件的首要方法。FTP 在今天仍然被大量使用，尽管许多图形化 FTP 客户端现在补充了原始的基于文本的界面命令。随着计算机的演进，FTP 也随之发展，Ubuntu 包含许多使用图形界面通过 FTP 传输文件的方法。

本章概述了 Ubuntu 中包含的可用 FTP 软件，以及有关 FTP 特定客户端的初始设置、配置和使用的一些细节。Ubuntu 还包含一个名为 vsftpd 的 FTP 服务器软件包，即 Very Secure FTP Daemon，以及一些可用于通过 FTP 协议提供服务和传输文件的相关程序。

## Choosing an FTP Server

FTP 使用客户端/服务器模型。作为客户端，FTP 访问服务器；作为服务器，FTP 提供对文件或存储的访问。几乎所有可用的计算机平台上都有软件编写用于使计算机充当 FTP 服务器，但 Ubuntu 为普通用户提供了在无需支付高额许可费且不受客户端使用限制的情况下实现此功能的能力。

FTP 服务器和访问有两种类型：匿名和标准。标准 FTP 服务器要求任何尝试访问服务器的人提供账户名和密码。匿名服务器允许任何人连接到服务器以检索文件。匿名服务器提供最大的灵活性，但也可能带来安全风险。幸运的是，正如您将在本章中阅读的那样，Ubuntu 已设置

