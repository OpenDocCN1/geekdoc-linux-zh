
这基本上意味着 `pppd` 不使用任何密钥（因为它使用系统密码过滤器）。

### 6. 为每个串口设置特定的 IP 地址
为该串口创建一个文件，路径格式为 `/etc/ppp/options.ttyXX`，其中 `ttyXX` 是串口设备名称。在该文件中列出本地 IP 和远程 IP 地址并用冒号分隔。例如，如果 `tty1` 串口的本地 IP 地址为 `192.168.0.100`，远程 IP 地址为 `192.168.0.200`，则在 `/etc/ppp/options.tty1` 中添加以下行：
`192.168.0.100:192.168.0.200`

### 7. 配置 `init` 启动
用文本编辑器打开 `/etc/initabb` 文件，并添加一行如下格式的行（此示例假设调制解器在第二个串口 `tty1` 上）：
`s123:respawn=/sbin/mtty -x 3 tty1`
`-O` 选项尝试将调制解器视为数据调制解器而非传真机。`x 3` 选项用于日志——日志文件为 `/tmp/log_mod.tty1`（对应调制解器设备 `/dev/tty1`）。

### 8. 重新加载配置并测试
将调制解器连接到串口，开启电源，然后使用以下命令重新加载 `/etc/initabb` 文件（从而运行 `mtty` 命令）：
`it q`

现在，你可以通过从另一台 PC 拨入来测试此 PPP 服务器设置。你需要让你的 Linux 系统连接到调制解器，而调制解器又连接到电话线。你应该在调制解器上拨号，然后你或你的朋友可以使用 Linux 系统上任何现有用户的用户名和密码拨入以建立 PPP 连接。

## 总结

我们的大多数人并没有直接连接到互联网的高带宽骨干网。我们依靠拨号调制解器、电缆调制解器或 DSL 连接到服务提供商（ISP），而这些又连接到骨干网（通常由 Sprint 和 AT&T 等电信公司提供）。你可以通过 SLIP 和 PPP 在串口线上实现 TCP/IP 网络。SLIP 和 PPP 的软件都随 Linux 提供。本章解释了 SLIP 和 PPP，并向你展示如何配置和使用 DSL、电缆调制解器、拨号调制解器 PPP 以及无线以太网将单个 PC 或局域网连接到互联网。

## 第13 章：互联网连接设置

在本章中，你学习了以下内容：

- DSL 和电缆调制解器提供了比拨号调制解器更快的互联网访问。你可以使用网络地址转换（NAT）路由器和集线机通过 DSL 或电缆调制解器将单个 PC 或小型局域网连接到互联网。
- 如果你有带有无线网卡的笔记本，可以通过将无线接入点连接到以太网集线机并在笔记本电脑上配置无线网络，将其带入局域网。
- PPP，即点点协议，是一种传输数据包的复杂协议。本章解释了什么是 PPP，并描述了超文本传输协议（HTTP）——使 Web 运行的信息交换协议。然后，它介绍了 Linux 自带的 Firefox 浏览器。
- 接下来，本章讨论了将 Web 作为发布信息的流行方式。Linux 包含了 Apache 服务器（HTTP 服务器是 Web 服务器的技术术语），你只需将 HTML 文件放置在相应的目录即可使用。本章展示了文件应该放在哪里以及如何配置 Apache 服务器。
- 设置 PPP 涉及两个基本步骤。首先，你必须使用浏览器——一种“知道”如何下载和显示文档的应用程序——以便能够享受互联网的好处。你还可以通过 Web 提供信息。
- 你可以使用网络地址转换（NAT）路由器和集线机通过 DSL 或电缆调制解器将单个 PC 或小型局域网连接到互联网。
- 如果你有带有无线网卡的笔记本，可以通过将无线接入点连接到以太网集线机并在笔记本电脑上配置无线网络，将其带入局域网。
- 标准的 Web 文档格式是超文本标记语言（HTML），传输 Web 文档的标准协议是超文本传输协议（HTTP）。

> Web 服务器是向任何发出 HTTP 请求的客户端发送 HTML 文档（以及其他文件）的软件。通常，Web 浏览器是从 Web 服务器下载 HTML 文档并以图形方式显示内容的客户端软件。

## 学习 URL

就像真实书籍的页面一样，网页包含文本和图形。然而，与真实书籍页不同，网页可以包含多媒体信息，如图像、视频片段、数字化声音和交叉引用。这些引用被称为“链接”，它们实际上可以将用户带到所引用的页面。

网页中的链接是对其他网页的引用。你通过跟随（点击）链接从一个页面跳转到另一个页面。浏览器通常将这些链接显示为带有下划线（颜色不同）的文本或图像。每个链接都是读者的指令——例如“欲需更多信息，请参阅第 14 章”，你可以在真实书中也找到这样的指令。在网页中，你只需要点击链接，浏览器就会调出引用的页面，即使它位于另一台计算机上。

> “超文本”（hypertext）指的是文本的非线性组织（与大多数书籍和杂志中文本的顺序、线性排列形成对比）。网页中的链接被称为超文本链接；通过点击链接，你可以跳转到不同的网页，这就是文本非线性组织的一个示例。

这种安排引发了一个问题。在真实书籍中，你可能会要求读者阅读特定的章节或页面。超文本链接是如何指示目标网页的位置的呢？每个网页都有一个特殊的名称，称为统一资源定位符（URL）。URL 唯一地指定了计算机上文件的位置，如图 14-1 所示。

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_453_0.png)

图 14-1：统一资源定位符 (URL) 由多个部分组成。

> 图 14-1 中的目录路径可以包含多个子目录，如斜线所示。

如图 14-1 所示，URL 具有以下组件序列：

- **协议（Protocol）：** 这是 Web 浏览器用于访问 URL 所指定文件内存储数据的名称。在图 14-1 中，协议是 `http://`，这意味着该 URL 指定了网页的位置。以下是常见的协议类型及其含义：
    - `file:`：指定要打开并显示的本地文件的名称。你可以在 URL 中使用它，在无需连接互联网的情况下查看 HTML 文件。例如，`file:///usr/share/doc/HTML/index.html` 打开来自你 Linux 系统的 `/usr/share/doc/HTML/index.html` 文件。
    - `ftp://`：指定通过文件传输协议（FTP）访问的文件。例如，`ftp://ftp.purdue.edu/pub/uns/NASA/nasa.jpg` 指向 FTP 服务器 `ftp.purdue.edu` 中 `/pub/uns/NASA/` 目录下的 `nasa.jpg` 图像。（如果你想通过 FTP 访问特定的用户账户，请使用 `ftp://username:password@somite.com/` 格式的 URL，将用户名和密码嵌入 URL 中）。
    - `http://`：指定通过超文本传输协议（HTTP）访问的文件。这是所有网站通用的 URL 格式，例如红 Hat 主页的 `http://www.redhat.com`。
    - `https://`：指定通过安全套接层（SSL）连接访问的文件，该协议由 Netscape Communications 设计，用于跨互联网的加密数据传输。当 Web 浏览器向 Web 服务器发送敏感信息（如信用卡号、姓名和密码）时，通常使用这种 URL 格式。例如，`https://some.site.com/secure/taker` 等 URL 会显示一个 HTML 表单，请求信用卡信息以及姓名、电话号码等个人信息。
    - `mail://`：指定用于发送电子邮件消息的电子邮件地址。例如，`mailmaster@someplace.com` 指向主机 `someplace.com` 的网站管理员。
    - `news://`：指定你可以通过新闻传输协议（NNTP）阅读的新闻组。例如，如果你有默认服务器名称，`news://psn.net/comp/infosystems.www.authoring` 会访问新闻服务器 `servers.net` 上的 `comp.infosystems.www.authoring` 新闻组，省略 URL `news:comp.infosystems.www.authoring.html` 来访问该新闻组。
    - `telnet://`：指定用于远程登录的用户名和系统名。例如，URL `telnet://guest:bemguest@someplace.com/` 使用用户名 `guest` 和密码 `bemguest` 登录主机 `someplace.com`。

**2. 域名（Domain name）：** 包含存储指定文件的计算机的完全限定域名。你也可以在此字段中指定 IP 地址（有关 IP 地址的更多信息请参阅第 6 章）。域名不区分大小写。

**3. 端口地址（Port address）：** 这是实现 URL 第一部分列出的协议的服务器端口地址（端口地址的讨论见第 6 章）。URL 的这部分是可选的，所有协议都有默认端口。例如，HTTP 的默认端口是 80。然而，某些网站可能会配置 Web 服务器监听不同的端口。在这种情况下，URL 必须包含端口地址。

**4. 目录路径（Directory path）：** 这是 URL 中所引用的文件的目录路径。对于网页，该字段是 HTML 文件的目录路径。目录路径区分大小写。

**5. 文件名（Filename）：** 这是文件名。对于网页，文件名通常以 `.htm` 或 `.html` 结尾。如果省略它，服务器将返回默认文件。

## 第三部分：Linux 网络化

## 第 14 章：Web 服务器

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_457_0.png)

图 14-2：用 Firefox 浏览器查看的 URL `www.google.com`。

尽管 HTTP 直此一直被广泛使用，但直到最近它才成为一种互联网标准。所有的互联网标准都以“请求回复”（RFC）的形式分发。第一个 HTTP-RFC 是 RFC 1945，“超文本传输协议–HTTP/1.0（T. Berners-Lee, R. Fielding 和 H. Frystock, 1996年5月）”。然而，RFC 1945 被认为是一个信息性文档，而非标准。

RFC 2616，“超文本传输协议–HTTP/1.1”（R. Fielding, J. Gettys, J. Mogul, H. Frystock, L. Masner, P. Leach, T. Berners-Lee, 1999年6月）是 HTTP 的数据标准。

要阅读这些 RFC，请将您的 Web 浏览器指向 `www.faqs.org/rfc/rfc-index.html`。

要了解更多关于 HTTP/1.1 和其他 Web 相关标准，请使用 Web 浏览器访问 `www.w3.org/pub/WWW/Protocols`。

## 冲浪网络

对于其他任何事物，在看到它的工作原理后，Web 会变得更容易理解。学习 Web 的最好方法之一是使用 Web 浏览器对其进行冲浪。浏览 Web 页面很有趣，因为典型的页面同时包含文本和图像，带有惊喜；你可以点击链接并进入意想不到的 Web 页面。链接是 Web 最奇人的方面。你可以从查看一个显示今天天气的页面开始，稍后一下，你就可以阅读《时间》杂志本周的内容了。

## 第三部分：Linux 网络化

在尝试任何操作之前，当然，你需要一个 Web 浏览器。（你的 Linux 系统也必须连接互联网，我假设你已经处理好了那部分。）

## 检查 Linux 中的 Web 浏览器

Linux 带有 Mozilla 和 Firefox Web 浏览器——来自 Mozilla 组织的开源 Web 浏览器（参见 `www.mozilla.org/products/firefox/`）。

Linux 还包含其他几个 Web 浏览器。我简要提到其他浏览器，但在剩余的讨论中我将关注 Firefox。以下是 Linux带的大主要 Web 浏览器：

- * Mozilla：那个老工作负载——Netscape Communicator 的转世，但它更好。它包含了邮件和阅读器。该 Web 浏览器被称为 Mozilla Navigator，或简称为 Navigator（就像它在 Netscape Communicator 中一样）。
- * Firefox：Mozilla 的下一代浏览器具有弹出广告，提供了标签页以便在单个窗口中轻松查看多个 Web 页面，并包含了一套隐私工具。你可以从 `www.mozilla.org/download.html` 下载 Firefox。
- * Epiphany：GNOME Web 浏览器，使用 Mozilla 代码的部分内容来绘制 Web 页面，但用户界面比 Mozilla 更简单。Epiphany 默认不安装，但它应该在 DVD 上。
- * Konquerer：KDE Web 浏览器，兼任文件管理器和通用查看器。

除了这四个之外，许多其他应用程序也能下载和分发 Web 页面。

## 启动 Firefox

从 GNOME 或 KDE 桌面，你可以通过两种方式启动 Firefox：

- * 点击 GNOME 或 KDE 面板上的 Web 浏览器图标。
- * 选择“应用程序：Internet Firefox Web 浏览器”（来自 GNOME 或 KDE）。

当 Firefox 启动时，它会显示一个带有默认首页的浏览器窗口（Web 服务器上的主 Web 页面被称为首页）。你可以配置 Firefox 使用不同的 Web 页面作为默认主页。

## 学习 Firefox 的用户界面

图 14-3 显示了 Wiley 网站（`www.wiley.com`）的一个 Web 页面，以及 Firefox 浏览器的主要元素。

Firefox 浏览器的用户界面有很多内容，但你可以轻松地掌握它。你可以关闭一些让它看起来很乱的项目。你也可以从 Firefox 的基础操作开始，然后逐渐扩展到你尚未探索的领域。

从窗口顶部开始，你可以看到标准的菜单栏，然后带有“主页”和“后退”图标的导航工具栏，接着是带有书签图标的较窄的书签工具栏。书签工具栏下方是当前 Web 页面出现的地方。

## 第 14 章：Web 服务器

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_459_0.png)

图 14-3：运行中的 Firefox 浏览器。

你可以使用紧接菜单栏下方的导航工具栏按钮执行以下操作（从左到右）：

- * Back（后退）：移动到上一个 Web 页面。
- * Forward（前进）：返回你使用“后退”按钮后离开的页面。
- * Reload（刷新）：重新加载当前 Web 页面。
- * Stop（停止）：停止当前页面。
- * Home（主页）：带你回到首页。
- Location 文本：显示当前 Web 页面的 URL（在此框中输入 URL 即可查看该 Web 页面）。
- * Go（跳转）：跳转到你在 Location 中输入的 URL。
- * Google Search（谷歌搜索）：输入搜索字符串并按回车执行 Google 搜索。

工具栏下方是书签工具栏，它可以带你进入 Red Hat 的首页或 Red Hat Network 站点。其余链接组织在几个文件夹中。点击文件夹查看下拉列表。

## 设置 Web 浏览器

## 设置 Apache 服务器

## 更多关于 Apache 服务器

## 安装 Apache 服务器

# 配置 Apache 服务器

Apache Web 服务器使用以下文件和目录：

- Web 服务器程序——`httpd` 安装在 `/usr/sbin` 目录。
- Apache Web 配置文件——`httpd.conf`——位于 `/etc/httpd/conf` 目录。该配置是一个文本文件，包含指定 Web 服务器各个方面属性的指令（后文将详细描述 apache 指令）。
- Apache Web 将 `/etc/httpd/conf.d` 目录下带有 `.conf` 扩展的文件视为 Apache 模块（如 `mod_perl`、`mod_python`、`mod_ssl` 等）的配置文件。例如，`/etc/httpd/conf` 包含了 SSL 所需的配置信息。
- Apache 服务器设置为存储来自 `/var/www/html` 目录的 HTML 文档。因此，您应该将 Web 页面放在此目录。
- 如果你有任何通用网关接口 (CGI) 程序——Web 服务器调用它们来访问其他文件和数据库——您应该将它们放在 `/var/www/cgi-bin/` 目录。
- `/var/log/httpd` 目录在 Linux 系统启动时开始运行。您可以使用命令 `/init.d/httpd` 来运行 Web 服务器（另一种方法是使用 `service httpd start`）。

如果您希望在系统启动时自动启动 Apache 服务器，请以 root 登录并输入以下命令来启用服务器：
```
```
