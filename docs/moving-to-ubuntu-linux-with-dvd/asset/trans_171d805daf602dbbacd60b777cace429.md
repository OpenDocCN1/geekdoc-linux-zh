

# 深入了解 IRC

IRC 有一些你可能想要了解的有趣命令。IRC 命令由斜杠字符 (/) 开头，后跟命令名称。有些命令所有用户都可以使用，而有些则仅供频道管理员使用。要了解你可以使用哪些命令，请在文本字段中输入 /help 并按 <Enter>。命令列表会直接显示在聊天窗口中。以下是一些更常见且有用的命令：

- /help 列出 IRC 命令。
- /help command_name 获取特定命令的帮助信息。
- /nick new_name 更改你的昵称。
- /join #channel 加入指定频道。
- /part 离开频道。
- /list 列出可用频道。
- /me Some_action 打印你的昵称，后接你的动作文本，并以不同颜色突出显示该消息。试试看吧，这很有趣。

![](img/0e9cf4c65a042f4a9bea644dc50153a7_203_0.png)

> 注意 /list 命令。在某些服务器上，此命令可能会返回一个庞大的频道列表。

IRC 是一个绝佳的资源，我强烈推荐它，但附有一个谨慎的建议。这个庞大的分布式实时讨论组网络已经发展出一种独特的文化，拥有自己的礼仪规则，这些规则应当被遵守。频道有操作员（operators）来监控流量和来自用户的请求。如果你不守规矩，操作员也可以将你驱逐出去。可能还存在机器人，即设计用于处理简单管理请求的小型程序，因此你看到的每个用户不一定都是人类。

当你手头有如此丰富的工具时，很容易沉迷于 IRC，但也花点时间阅读一篇关于其基本原理的小指南是很好的。查看 Resources 部分中的 IRC 入门指南，它是对 IRC 世界的一个绝佳介绍。

另一个绝佳资源是 netsplit.de IRC 信息网站，你可以在那里找到频道和主题的搜索引擎，以及 IRC 服务器和网络的综合列表。

我会在网上等你。

## Resources

- **Gaim Instant Messaging**
  `http://gaim.sourceforge.net`
- **Google Talk**
  `http://talk.google.com`
- **Jabber Software Foundation**
  `http://www.jabber.org`
- **A Short IRC Primer**
  `http://www.irchelp.org/irchelp/ircprimer.html`
- **Netsplit.de IRC Information Site**
  `http://irc.netsplit.de`

# 第 10 章

## 使用 Firefox 浏览网络

说到桌面上的 Web 浏览器，Linux 用户面临着选择过多的尴尬局面，有很多替代方案可供选择。对于那些寻求极速浏览体验且不需要图形界面的人，Linux 提供了许多基于文本的浏览器。（我将在本章末尾简要提及这些浏览器。）

在大多数人花费浏览时间的图形化世界中，当今最热门、最酷的浏览器是 Firefox，而它恰好是 Ubuntu Linux 中的默认浏览器。在 Firefox 不久前出现之前，人们都以为浏览器世界属于来自 Redmond（微软所在地）的、饱受安全问题困扰的 Internet Explorer。就在我写这段话时，Internet Explorer 在北美浏览器市场份额已跌破 90%，在欧洲则跌破 80%。考虑到在 Firefox 出现之前，Internet Explorer 曾占据约 95% 的市场份额，这一成就是相当了不起的。更好的安全性和先进功能将数百万用户从微软的浏览器吸引到了 Firefox。Firefox 是一个令人兴奋的程序，我将在本章向你展示它的运作方式。

## Mozilla 与 Firefox

Firefox 由分发 Mozilla 浏览器的同一群人分发。事实上，Firefox 是一款 Mozilla 产品。

Mozilla 和 Firefox 有什么区别？实际的 Mozilla 浏览器更像是浏览器中的瑞士军刀。它包含电子邮件包和 IRC 客户端，非常适合阅读新闻组，并附带 HTML 编辑器。另一方面，Firefox 纯粹是一个 Web 浏览器（见图 10–1）。它更小、更快，更专注于其主要任务，为你提供卓越的冲浪体验。若要获取同等独立的电子邮件包，你需要下载 Thunderbird（在第 11 章中有提及）。目前，我想专注于 Firefox，所以让我们开始吧。

![](img/0e9cf4c65a042f4a9bea644dc50153a7_206_0.png)

要启动 Firefox，请点击顶部面板中的应用菜单，导航到 Internet 子菜单，然后选择 Firefox Web Browser。顶部面板中还有一个 Firefox 的快捷访问图标。在“System”菜单的右侧，有一个蓝色地球图标。将鼠标光标悬停在图标上，它会显示自己为 Firefox。

### 从主页开始

当你第一次启动 Firefox 时，它会带你到其主页，目前是本地安装在你系统上的“Welcome to Ubuntu”页面。该位置在菜单栏正下方的 URL/位置栏中标识出来。访问网站并导航 Firefox 的操作与你使用过的任何其他浏览器都非常相似，特别是如果你之前使用 Mozilla（或 Firefox）搭配旧操作系统的体验。你只需在位置栏中输入你要访问的网站 URL，就可以开始了。如果你想每次从个人主页开始，这很容易做到。

![](img/0e9cf4c65a042f4a9bea644dc50153a7_207_0.png)

> 提示 花时间查看并访问 Ubuntu 欢迎页面上的链接。它们指向一些有价值的资源，其中一些你可能想要加入书签。

点击 Firefox 菜单栏中的 Edit，然后选择 Preferences。偏好设置窗口打开后，顶部标题栏下方有一排图标，你可以从中选择要修改 Firefox 的哪个部分。默认情况下，它打开的是 General 类别（见图 10-2）。正下方的 Home Page 部分有三个按钮。第一个按钮 Use Current Page 会将你当前访问的 URL（或页面）输入到 Location 字段作为你的主页。中间的按钮 Use Bookmark 会弹出一个对话框，显示你当前的书签。点击 Use Blank Page 按钮将从空白页启动 Firefox。当然，你也可以直接键入 URL 到 Location 字段，点击 OK，完成设置。

![](img/0e9cf4c65a042f4a9bea644dc50153a7_207_1.png)

> 快速提示 在关闭偏好设置对话框之前，你是否注意到 Location 字段实际上写的是 Location(s)？没错，它可以是复数。如果你打开了多个标签页（我接下来会详细介绍），Use Current Page 按钮会变成 Use Current Pages。当你点击 Home 图标时，Firefox 会为所有你喜爱的页面打开标签。如果你想手动在位置栏中输入页面列表，只需使用竖线符号 |（通常位于键盘上反斜杠键上方）将每个页面分隔开即可。

![](img/0e9cf4c65a042f4a9bea644dc50153a7_208_0.png)

Figure 10-2 Setting your home page in Firefox's Preferences menu.

### 以 Firefox 风格保持标签

Firefox 拥有一项名为标签浏览的强大功能。以下是其工作原理。有时在浏览网站时，你想保持某个特定网站打开，同时转到网络上的另一个地方。通常，你会点击 File 并选择 New Window。这没问题，但如果你一直这样做，最终会在桌面上打开许多个浏览器窗口。从一个切换到另一个需要进行一点数字杂耍。标签使得原本可能变得非常杂乱的任务栏（或桌面）能够保持整洁有序。通过标签浏览，你在同一个浏览器窗口中打开额外的网站，然后通过点击对应打开网站的标签来切换。

以下是操作方法。首先访问你选择的网站。然后点击 File，选择 New，并从下拉菜单中选择 New Tab。你也可以使用 <Ctrl+T> 键盘快捷键完成相同操作。请注意，Firefox 在位置栏（见图 10-3）下方以标签标识你的网站，或者如果你开启了书签工具栏，它会显示在那里。添加第三个或

