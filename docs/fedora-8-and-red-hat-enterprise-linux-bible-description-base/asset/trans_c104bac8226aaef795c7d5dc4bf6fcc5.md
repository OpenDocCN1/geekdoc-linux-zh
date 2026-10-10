
## 网络网址

如今，网络网址（Web URLs）随处可见——从名片到麦片盒上都能找到——但你可能并不了解网址是如何构造的。网址的格式如下：

```
protocol://host-domain/path
```

协议（protocol）标识了你请求的内容类型。迄今为止，你遇到的最常见的协议是超文本传输协议（Hypertext Transfer Protocol，HTTP）。HTTP 是用于请求网页的协议。然而，除了 HTTP 之外，还有一些其他协议可能会出现在网址的开头。这些其他类型的协议可能不会向你展示网页，而是在浏览器中显示不同类型的信息，或者打开一个完全不同的应用程序来处理该内容。

表 9-1 列出了可出现在网络网址中的一些协议。（正如表中所述，其中一些已不再被现代浏览器支持。）

**表 9-1：网络网址中的协议**

| 协议名称 | 描述 |
|---|---|
| http | 超文本传输协议（Hypertext Transfer Protocol）。用于标识 HTML 网页及相关内容。其安全版本是安全套接字层超文本传输协议（https，Hypertext Transfer Protocol over Secure Socket Layer）。 |
| file | 标识特定主机上的文件。通常用于显示来自本地计算机的文件。 |
| ftp | 文件传输协议（File Transfer Protocol）。标识包含文件归档的位置，你可能希望从中下载文件。 |
| gopher | Gopher 协议。提供基于文本的文档数据库，这些文档分布在互联网上。（Gopher 几乎已废弃。） |
| mailto | 电子邮件地址。标识一个电子邮件地址，例如 `mailto:joe@example.com`。（通常会打开邮件撰写器。） |
| news | USENET 新闻组。标识一个新闻组，例如 `news://news.mypisp.com/comp.os.linux.networking`。如果你在 Mozilla Navigator 中输入此地址，将弹出一个窗口，显示你指定的新闻服务器上的新闻组。（在 Firefox 中，news 默认不是已注册的协议。） |
| nntp | 使用 nntp 协议的 USENET 新闻。 |
| telnet | 登录到远程计算机并开始交互式会话。一个 telnet 地址的示例是 `telnet://localhost`。（将 `localhost` 替换为任何允许你登录的主机或 IP 地址。） |
| wais | 广域信息服务器（Wide Area Information Server）协议。WAIS 地址可能如下所示：`wais://hacksonhistory.com/waisdb`。（与 gopher 类似，WAIS 数据库几乎已废弃。） |

URL 的第一部分是协议。你并不总是需要输入协议。大多数浏览器很擅长猜测你正在寻找的内容（它们通常猜测为 HTTP）。如果你输入的地址以 www 开头，浏览器假设是 HTTP；如果以 ftp 开头，则假设是 FTP。

URL 的第二部分带你去承载网络内容的计算机。按照惯例，Web 服务器以 www（有时是 home）开头。然而，如果你输入正确的协议（通常是 http），你将被引导到主机计算机上的正确服务。此名称的下一部分只是 Internet 上始终使用的 host.domain 样式的 Internet 地址（例如 rechat.com, linuxtoys.net 或 whitehouse.gov）。可以在 host.domain 名称后附加一个可选的端口号。例如，要从名为 www.linuxtoys.net 的主机请求用于 HTTP 服务的端口（80 端口），你可以输入 http://www.linuxtoys.net:80。

> **提示：** 你可以识别特定的端口号来请求你请求的计算机上与该端口关联的服务。端口号很像大公司里的分机号。主电话号码（如 host.domain 名称）让你到达公司总机。分机号（如端口号）让你连接到正确的人（如与端口关联的服务）。

URL 的第三部分标识了内容在主机计算机上的位置。网页中的部分可以用英镑符号（#）和跟随在网页位置后的标识符来识别。例如，handsonhistory.com 上 bashed.htm 页面的工艺（craft）部分将显示为：

```
http://www.handsonhistory.com/bashed.htm#craft
```

文件扩展名（例如 .htm 或 .html）进一步标识了内容类型。

## 网页

如果你查看生成网页的 HTML 源代码，你会发现它由信息和标记标签的组合组成，所有这些都处于纯文本格式。其想法是让网页非常便携和灵活。你可以使用 vi、emacs、gedit 或任何计算平台上的任何文本编辑器来创建网页。或者，可以使用简化的前端程序来提供 WYSIWYG（所见即所得）接口，让你在创建过程中看到你所创建的内容。

HTML 标签由左右尖括号分隔。标签成对出现，包括开始标签、信息以及结束标签。开始标签包含标签名称，而结束标签包含一个斜杠（/）和标签名称。以下是一个最小的 HTML 页面：

```
<html>
<head>
<title>Greetings from Wisconsin</title>
</head>
<body>
Here we are in beautiful Madison.
</body>
</html>
```

你可以看到文档以 HTML 标签（`<html>` 和 `</html>`）开始和结束。网页的开头部分包含在 `head` 标签内。页面的正文包含在 `body` 标签内。页面的标题由 `title` 标签分隔。

在开始和结束 `body` 标签之间，你可以添加各种各样的内容。你可以有标题、图像和文本。更多的不同类型的无序或有序列表。你可以添加表单、动态 HTML（当你移动或选择项目时改变内容）或特殊数据。图 9-2 展示了一个在 Firefox 中显示的网页示例。

![](img/fb202c163797a743c3c6cf236316bc96_405_0.png)

**图 9-2：** 许多网页包含文本、图像、标题和链接。

用于创建图 9-2 中所示网页的一些 HTML 代码如下所示。网页的标题出现在两个 `title` 标签之间：

```
<title>Swan Bay Folk Art Center - American Crafts in Port Republic, NJ</title>
```

以下代码用于创建一个打开新邮件消息窗口的链接：

```
<A HREF="mailto:webmaster@hands0nhistory.com">Contact Us</A>
```

文本 **Contact Us**（联系我们）是一个指向电子邮件地址的链接。当某人点击该链接时，会出现一个新消息窗口，允许该人向该地址发送电子邮件。

```
<A HREF="bsched.htm">
New Basket Class! </A>
```

“New Baskets Class!”（新课程！）这几个词指向另一个 HTML 页面的链接。如果有人点击这几个词，将显示 bsched.htm 页面。

## 使用 Firefox 浏览网络

使用 Firefox 网络浏览器（参见图 9-3），Mozilla 项目直接针对 Microsoft Internet Explorer。Firefox 轻便（因此运行速度快），包含许多易用性功能，并且以安全为高优先级构建。如果你还没有切换到 Fedora，你可以为 Windows、Mac OS X 和其他 Linux 系统获取 Firefox。如果你拥有随本书附带的 Fedora DVD，你可以立即试用 Firefox。

![](img/fb202c163797a743c3c6cf236316bc96_406_0.png)

由于 Firefox 是当前 Fedora 和 RHEL 的默认浏览器，如果你进行了包含桌面的安装，Firefox 应该已经安装。（如果没有，你需要从 Fedora DVD 安装 firefox 软件包。）要从你的 Fedora 桌面启动 Firefox，要么从你的面板选择地球图标，要么从应用程序菜单中选择 Internet ► Firefox Web Browser。Firefox 在其主窗口中直接提供了一些其最佳功能（如图 9-3 所示）。以下是一些示例：

- **标签式浏览** — 不必打开多个窗口以同时拥有多个网页，Firefox 包含一个非常高效的标签式浏览功能。选择 File ➔ New Tab（文件或按 Ctrl+T）。然后输入你所需新网页的 URL。图 9-3 显示了带有两个打开的浏览标签的 Firefox 窗口。从首选项窗口（Edit ➔ Preferences ➔ Tabs）设置的标签选项可以设置为自动强制在新标签中打开新链接，或在新标签中打开来自其他应用程序的链接。这有助于通过在一个窗口中包含多个网页来保护屏幕空间。

要关闭标签、打开新标签、将某个标签或一组标签加入书签，或重新加载一个或所有标签，请右键点击窗格顶部的其中一个标签。下拉菜单允许你选择你想要的功能。在新标签中打开链接最简单的方法之一是在 HTML 页面上的链接上右键点击。选择“Open Link in New Tab”（在新标签中打开链接）选项。

- **动态书签** — 对于提供 RSS 新闻和博客标题的网站，Firefox 屏幕的位置框中会出现一个小 RSS 徽标图标（参见图 9-3）。使用该图标，你可以将宣传的 RSS 源加入书签，以便从你的书签菜单中显示来自该站点的实时标题。

尝试像 http://fedoraforum.org 这样的网站。点击 RSS 按钮。当被提示时，选择为网站添加书签。选择 Bookmarks（书签），然后选择新书签。在书签的右侧，将显示该站点今天可用的文章列表。你可以点击直接前往一篇看起来有趣的文章。或者，你可以选择“Open in Tabs”（在标签中打开）以在单独的标签中打开所有文章。

如今，许多网站都包含 RSS 支持。尝试 packers.com, cnn.com, slashdot.org, abcnews.com 或 cbssportsline.com 以了解提供 RSS 新闻源的其他网站示例。

> **注意：** 如果你访问一个你知道是 RSS 站点的网站，但你想要的标题以 XML 代码形式出现，这意味着该页面没有向 Firefox 识别自己是一个 RSS 站点。你仍然可以通过选择 Bookmarks ➔ Manage Bookmarks 为该站点添加动态书签。从书签管理器屏幕，选择 File ➔ New Live Bookmark。当被提示时，为动态书签输入名称，然后将（或剪切并粘贴）RSS 页面的位置输入到 Feed Location 框中并点击 OK。该新动态书签以及该站点今天的文章将出现在你的书签列表中。

- **使用侧边栏** — 选择 View ➔ Sidebar 以选择让书签或历史记录作为 Firefox 窗口中的侧边栏显示。添加你自己的书签，从历史记录列表返回页面，或使用搜索框搜索这些列表中的内容。键入 Ctrl+B 和 Ctrl+H 分别切换书签和历史记录侧边栏的开启和关闭。

- **网络搜索** — 用于从 Google 进行关键字搜索的框直接内置在 Firefox 导航工具栏中。下拉菜单让你选择搜索 Yahoo!、Answers.com、Creative Commons、Amazon.com 或 eBay。或者，从下拉列表中选择“Manage Search Engines”（管理搜索引擎）进入 Firefox 搜索引擎页面，在那里你可以从 20 多种不同的搜索引擎中选择。
