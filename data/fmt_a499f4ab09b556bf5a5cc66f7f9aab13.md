
- `fetchmailconf`——用于 X 的图形化 fetchmail 配置客户端
- `kmail`——用于 KDE 和 X 的图形邮件客户端
- `korn`——用于 KDE 和 X 的 biff 小程序
- `mutt`——基于控制台的邮件用户代理

## 参考

以下参考资料推荐用于邮件配置阅读。当然，并非所有参考资料都适用于您。请选择适用于您所使用的邮件服务器的资料。

### 网络资源

- `http://www.sendmail.org/`—这是 Sendmail 主页。在这里您可以找到有关 Sendmail MTA 的配置信息和常见问题解答。
- `http://www.postfix.org/`—这是 Postfix 主页。如果您使用的是 Postfix MTA，您可以在此站点找到文档和示例配置。
- `http://www.qmail.org/`—这是 Qmail MTA 的主页。它包含文档以及指向 Qmail 其他资源的链接。
- `http://www.linuxgazette.com/issue35/jao.html`—IMAP on Linux: A Practical Guide。Internet Mail Access Protocol 允许用户访问存储在远程服务器而非本地磁盘上的电子邮件。
- `http://www.imap.org/about/whatisIMAP.html`—此页面描述了 IMAP。
- `http://www.rfc-editor.org/`—RFCs—Request for Comments 的存储库，它定义了现代计算机使用的技术“规则”。
- `http://www.procmail.org/`—Procmail 主页。
- `http://www.moongroup.com/docs/procmail/`—Procmail 常见问题解答，其中包含故障排除问题的建议。该页面还引用了一个链接页面，该页面反过来引用了其他链接集合以及来自 Procmail 邮件列表的要点。
- `http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Qmail-VMailMgr-Courier-imap-HOWTO.html`—如果您需要一些帮助来配置基于较少使用的应用程序的邮件系统，本 HOWTO 将会有所帮助。

### 书籍

- Sendmail (O’Reilly Publishing)—这是 Sendmail 的事实标准指南。它包含超过 1,000 页的内容，这足以说明 Sendmail 的复杂程度。
- Postfix (Sams Publishing)—Sams Publishing 出版的一本优秀书籍，涵盖 Postfix MTA。
- Running Qmail (Sams Publishing)—这与 Sams Publishing 的 Postfix 书籍类似，只是它涵盖了 Qmail MTA。

## 第 20 章 代理和反向代理

在这个世界上，有两样东西永远不够：时间和带宽。Ubuntu 自带一个代理服务器——Squid——它使您能够在服务器上缓存网络流量，以便网站加载更快，用户消耗更少的带宽。

### 什么是代理服务器？

代理服务器位于客户端机器——您公司中的桌面——与互联网之间。当客户端请求网站时，它们不会直接连接到网络并发送 HTTP 请求。相反，它们连接到本地代理服务器。代理随后将请求转发到网络，检索结果并将其交还给客户端。最简单地说，代理服务器只是在客户端和服务器之间多了一层，那为什么还要费事呢？

部署代理服务器的三个主要原因如下：

- 内容控制—您希望阻止人们在工作时间浪费时间阅读新闻或下载 MP3。
- 速度—您希望缓存常用站点以充分利用带宽。
- 安全—您希望监控人们正在做什么。

### 本章内容

- What Is a Proxy Server?
- Installing Squid
- Configuring Clients
- Access Control Lists
- Specifying Client IP Addresses
- Example Configurations
- Reference

### 安装 Squid

与大多数 Ubuntu 软件一样，Squid 的安装通过 `synaptic` 处理。安装 Squid 后，它会自动为每次启动启用。您可以通过在机器启动时运行 `ps aux | grep squid` 来检查这一点。如果出于某种原因您在那里看不到任何内容，请运行 `/etc/init.d/squid start`。

### 配置客户端

在配置新的 Squid 服务器之前，请设置本地网页浏览器以使用它进行网络访问。这样做可以让您在处理配置文件时测试规则。

要配置 Firefox，请从 `Edit` 菜单中选择 `Preferences`。从出现的对话框中，单击 `Connection Settings` 按钮（在 `General` 选项卡底部附近）并选择 `Manual Proxy Configuration` 选项。选中下方 `Use the Same Proxy for All Protocols` 复选框；然后输入 `127.0.0.1` 作为 IP 地址，`3128` 作为端口号。参见图 20.1，了解它应如何显示。如果您正在配置远程客户端，请指定 Squid 服务器的 IP 地址而不是 `127.0.0.1`。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_504_0.png)

对于 Konqueror，请转到 `Settings` 菜单并选择 `Configure Konqueror`。从左侧选项卡向下滚动到 `Proxy`，选择 `Manually Specify the Proxy Settings`，然后单击 `Setup`。输入 `127.0.0.1` 作为代理 IP 地址，`3128` 作为端口。与 Firefox 一样，如果您正在配置远程客户端，请指定 Squid 服务器的 IP 地址而不是 `127.0.0.1`。

Internet Explorer 的代理设置位于“工具/Internet 选项”中。在“连接”选项卡中，单击“局域网设置”按钮，并启用“为 LAN 使用代理服务器”选项。输入地址为你的 Squid 机器的 IP，然后将端口指定为 `3128`。

### 访问控制列表

Squid 的主配置文件是 `/etc/squid/squid.conf`，默认的 Ubuntu 配置文件充满注释以帮助指导你。默认配置文件允许本地机器的完全访问，但拒绝你网络中的其余部分。这是一个安全起点；我们建议你先在本地机器（`localhost`）上尝试所有规则，然后再推广到其他机器。

开始之前，打开两个终端窗口。在第一个窗口中，切换到 `/var/log/squid` 目录并运行以下命令：

```
sudo tail -f access.log cache.log
```

该命令读取两个文件的最后几行，并（得益于 `-f` 标志）持续跟踪它们，以便任何更改都会显示在那里。这让你可以观察 Squid 在人们访问它时的行为。我们将此窗口称为“日志窗口”，请保持其打开。在另一个窗口中（同样使用 `sudo`），在你喜欢的编辑器中打开文件 `/etc/squid/squid.conf`。此窗口称为“配置编辑器”，你也应该保持它打开。

要开始，请搜索字符串 `acl all`——这会带你到访问控制部分，这是需要完成大部分工作的地方。你可以在其他地方配置很多内容，但除非你有特殊要求，否则可以保留默认设置。

> **注意**
>
> Squid 的默认端口是 `3128`，但你可以通过编辑 `http_port` 行来更改。或者，你可以通过设置多个 `http_port` 行让 Squid 监听多个端口：`80`、`8000` 和 `8080` 都是代理服务器的常用端口。

`acl` 行构成了你的访问控制列表（ACL）。前 16 行左右定义了建议的最小配置，设置要监听的端口等等。你可以放心忽略这些。如果继续向下滚动（经过另一段简短的注释块），你会看到 `http_access` 行，它们与 `acl` 行结合以决定谁可以做什么。你可以（并且应该）混合搭配 `acl` 和 `http_access` 行，以使你的配置文件易于阅读。

就在第一组 `http_access` 行的下方，有一条类似 `# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS` 的注释。这正是我们要做的。不过，首先只需再向下滚动几行；你应该会看到以下两行：

```
http_access allow localhost
http_access deny all
```
