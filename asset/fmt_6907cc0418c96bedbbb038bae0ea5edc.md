
```
<VirtualHost>
www.my_domain.com
ServerAdmin webmaster@my_domain.com
DocumentRoot /var/www/my_domain.com
ServerName www.my_domain.com
ErrorLog /var/log/apache/my_domain.com-error.log
TransferLog /var/log/apache/my_domain.com-access.log
</VirtualHost>
```

然而，当使用一个 IP 地址对应多个域名时，你需要更改 `httpd.conf` 文件中的一行来分配 IP 地址。你必须添加 `NameVirtualHost` 指令来向 Apache Web 服务器标识 IP 地址。此行在你的配置文件中可能如下：

`NameVirtualHost 192.168.0.32`

服务器随后使用客户端浏览器提交给服务器的变量名来指示主机名。特定的主机名被添加到 `httpd.conf` 文件中的 `VirtualHost` 指令部分。我更倾向于使用独立的 IP 地址，因为这样更容易设置，以后更改也同样容易。你可以从这个示例中看到，每个主机名的 `VirtualHost` 都是相同的。区别在于别名。

```
<VirtualHost 192.168.0.32>
ServerAdmin webmaster@my_domain.com
DocumentRoot /var/www/my_domain/parts
ServerName parts.my_domain.com
ErrorLog /var/log/apache/parts/my_domain-error.log
TransferLog /var/log/apache/parts/my_domain-access.log
</VirtualHost>
<VirtualHost 192.168.0.32>
ServerAdmin webmaster@my_other_domain.com
DocumentRoot /var/www/my_other_domain/data
ServerName data.my_other_domain.com
ErrorLog /var/log/apache/data.my_other_domain-error.log
TransferLog /var/log/apache/data.my_other_domain-access.log
</VirtualHost>
```

### 总结

无论你是将 Web 服务器作为单台工作站来显示你开发的 Web 页面示例，还是作为主要的企业 Web 服务器，或是为了互联网上托管多个域名的页面，Apache Web 服务器都能处理你所有的需求。希望在读完本章后，你对这台服务器有了更好的理解。你可以对其进行定制以满足你的特定需求。

互联网上超过三分之二的服务器使用 Apache 作为它们的服务器，因此拥有庞大的追随。如果你有本章范围之外的问题，我鼓励你进一步调查关于这台优秀的服务器。你可以参考以下网站获取信息：

- www.apache.org—Apache 软件基金会提供 Apache 的完整文档。
- www.apache-ssl.org—Apache SSL 提供关于 Apache SSL 版本的文档。
- modules.apache.org—Apache 模块库为 Apache 提供额外的模块。
- www.w3.org—万维网联盟致力于维护互联网上使用的通用标准和协议。
- www.apacheweek.com—Apache 周刊提供有关 Apache 的文章和新闻。

## FTP 服务器

在考虑网络传输文件便利性的对立面时，脑海中会浮出“肉身网络”（sneakernet）这个词。在网络上的计算机上工作时，通过拨号连接或互联网，将文件从一台计算机传输到另一台计算机就变成了一个全新的维度。你不再需要穿着运动鞋把文件从其中一台电脑运行到另一台。相反，你可以使用文件传输协议（FTP）。

本章试图减轻对“肉身网络”的使用，并回答如何设置 FTP 供你使用的问题。你越使用 FTP，就越会好奇你以前用它做了什么。FTP 有两个组件——服务器和客户端。本章将描述每个部分的示例。

## 关于 FTP 的一切

FTP 是在计算机之间传输文件的流行方式，特别是因为大多数文件已经无法装进小小的软盘了。它允许你连接到远程计算机，无论它只有5英尺远还是5000英里远。有了互联网，距离不再是问题。连接的唯一要求是某些相互的网络，例如互联网。

你有两种方式来配置 FTP 服务器使用：私有和公共（也称为匿名 FTP）。私有 FTP 服务器最安全，被强烈建议使用。私有 FTP 服务器仅允许具有有效账户和密码的人访问。匿名 FTP 服务器允许任何人在没有账户的情况下连接计算机。其他人被拒绝。

### 本章内容

- FTP 基础知识
- 安装和配置 FTP 服务器
- 理解公共和私有 FTP
- 管理 FTP 服务器
- 一些 FTP 客户端

FTP 通过 `TCP/IP` 协议工作，默认使用 `21` 端口。你可以更改它，但任何尝试连接到你服务器的客户端都需要知道这一点。你可以在配置文件中更改端口，但并不总是如此。FTP 服务作为独立（始终运行）服务器工作，或者根据每个请求由 `inetd` 守护进程启动。`inetd.conf` 文件包含了启动 FTP 服务的信息。你将在本章后面学习如何设置服务器。

### 匿名 FTP

在继续之前，我想深入探讨匿名 FTP。你知道匿名 FTP 服务器是通用的且公开的，因此访问它们消除了管理账户和密码的。你的账户是匿名的，密码是（或应该是）你的电子邮件地址。这可以被伪造，除了作为你连接到主机的确认外，密码不再重要。

如果每个人都可以连接到你的计算机，你该如何管理安全？这是一个很好的问题！匿名 FTP 服务器提供了限制到主机的连接数、连接时间以及访问服务器区域的功能。首先，匿名连接不允许访问整个服务器。它仅允许访问特定的预定义目录。这并不能消除涉及的安全风险。毕竟，由于现在都可以连接到你的机器，黑客的可能性仍然存在。然而，对访问者实施的限制越多，成功的概率就越小。

![](img/0d314422de05113fe6acc6b5e7b494ff_497_0.png)

匿名服务器可能会给其他服务器带来安全风险。黑客有时会将匿名服务器作为传输点，上传和下载供其他黑客使用的代码。明智的选择是在匿名服务器上没有任何上传（或传入）目录。如果（由于某种原因）你需要上传区域，请密切监控流量和内容。

匿名服务器的安全关乎每个人，所以这里有一些帮助你减少风险的提示：

- 限制到匿名服务器的连接数以维护其性能。允许到你计算机的连接越多，使用的资源就越多。

# 第 22 章 ✦ FTP 服务器 465

- 移除上传区域。这可以防止攻击者通过占用你所有的磁盘空间、交换数据等手段来利用你的站点。
- 匿名访问时验证电子邮件地址。某些服务器提供此选项。它要求一个看起来有效的电子邮件地址，而无论该邮箱是否真实有效。这不能保证该电子邮件地址确实是登录者的邮箱，但每一分努力都是有帮助。
- 当然，日志记录让你能够日后追溯服务器上的活动。这些记录可以让你回溯到攻击者访问你机器的源头地。
- 将匿名 FTP 机器与其他所有机器隔离开。使用与包含个人或业务信息的机器分开的独立机器，可以防止即使发生入侵，他人无法获得任何有价值的内容。

## 安装和配置 FTP 服务器

你即将开启一段旅程，这将让你的文件传输变得简单得多。本章介绍了三个 Debian 软件包中的 FTP 服务器，它们都有各自的安装和配置方法：`ftpd`、`wu-ftpd` 和 `proftpd`。

我将解释如何运行每一个服务器，以及如何对它们进行修改，以及各自的优缺点。你可以通过使用 `dselect` 程序简单地安装每个服务器，因为列出的所有服务器都包含在 Debian 软件包中。

> 在三个 FTP 服务器中，我推荐 ProFTPD 服务器，因为它的安全且易于配置——特别是在设置匿名 FTP 时。

### ftpd 服务器

大多数发行版都认为该服务器是最容易安装的——它们可能是对的。该服务器的安装和配置涉及非常少。你可以安装 `ftpd` 软件包，它会安装基础配置文件。位于系统中的两个文件是 `ftpdusers` 和 `ftchroot`。让我们更仔细地查看这两个文件。

> `ftpd` 也是可用最薄弱的 FTP 服务器之一。如果你在闭网网络中工作，可以随意使用它；但如果你在互联网上，我建议使用不同的 FTP 服务器。

## `/etc/ftpdusers`

这个简单的文件包含了一个列表，该机器不允许通过 FTP 连接登录的用户。如果一个用户名出现在此文件中，该用户将无法访问服务器。这与你预期的可能相反——不要将其与允许的用户列表混淆：

```
# /etc/ftpusers: 禁止 ftp 访问的用户列表。
# 详参见 ftpusers(5)。
```

```
root
ftp
anonymous
```

此文件中包含了 `root` 用户。这样做是为了增加你系统的安全性。通过绝对防止 `root` 在任何情况下登录，你可能会切断一个潜在的攻击途径。

## `/etc/ftpchroot` 文件
