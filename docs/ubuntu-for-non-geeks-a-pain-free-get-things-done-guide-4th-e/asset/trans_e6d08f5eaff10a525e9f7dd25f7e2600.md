

# 5

## SLIPPING AND SLIDING

*以 Linux 方式探索互联网*

![](img/f7cef0df22f9dba5a41777808c98eece_96_0.png)

现在你已经拥有了一个可用的互联网连接，你能用它做什么？好消息是 Linux 可以胜任你之前操作系统在网上能做的一切，而且在很多情况下它做得更快或更简单。Ubuntu 诞生于网络，因此不足为奇的是，它开箱即用就自带了一套非常完善的互联网就绪应用程序。

在本章中，你将对 Ubuntu 的互联网软件进行一次巡览，以便真正感受到这种 Linux 东西的能力。你将从像网页浏览器和邮件客户端这样的老牌工具开始，简要浏览即时通讯，然后转向更时髦的 Twitter 和微博方向。

## Firefox: Your Internet Browser

你 Ubuntu 系统中的默认网页浏览器是 Firefox，它在 Linux 世界中越来越受欢迎，在 Windows 和 Mac 世界中也同样如此。你很可能已经是 Firefox 用户了，但如果你不是，也不用担心——在所有浏览器中事物或多或少都一样。那样的话，你应该能够在没有任何指导的情况下使用 Firefox 的基本功能。当然，它的一些功能确实使其有别于竞争对手，所以我会提到这些。

### Controlling Browser Window Clutter with Tabs

通常当你在网页上点击一个链接时，新页面会在同一窗口中打开。在某些页面上，链接被编码为在新的独立窗口中打开新页面，或者你偶尔也可以通过右键点击链接然后选择“在新窗口中打开链接”选项来打开链接在新窗口中。这可能非常有用；然而，一旦你打开了不止几个浏览器窗口，就很难在所有打开的窗口中找到你要找的东西。这也会稍微减慢速度。

这就是 Firefox 的标签功能派上用场的地方（事实上非常方便，以至于几乎所有其他浏览器都复制了它）。要了解它是如何工作的，现在就亲自试试。点击顶部 GNOME 面板上的启动器打开你的 Firefox 浏览器（或选择 Applications ▸ Internet ▸ Firefox Web Browser）；然后使用 Firefox 方便的搜索框搜索单词 nyckelharpa，该搜索框位于浏览器窗口的右上角（见图 5-1）。默认情况下，Firefox 会使用 Google 对在搜索框中输入的关键词进行搜索。如果你愿意，可以通过点击搜索框中的彩色 gicon 然后做出选择来选择其他网站进行搜索。Amazon.com、eBay 和 Yahoo! 都可用，等等，你甚至可以添加其他网站。现在，让我们坚持使用 Google 进行本次搜索，在该搜索框中输入 nyckelharpa。输入完毕后，按 ENTER 键，之后搜索结果页面应该会出现在 Firefox 窗口的主窗格中。

顶部结果之一应该是美国 Nyckelharpa 协会，现在你将以新标签页而不是在同一窗口或新窗口中打开该页面。为此，右键点击该链接，并在出现的弹出菜单中选择“在新标签页中打开链接”。如果你愿意，也可以让事情变得稍微简单一些，省去弹出菜单选择步骤，只需用鼠标中键点击链接（或同时用两个鼠标按钮点击）或按住 CTRL 键的同时点击链接即可。无论哪种方式，新页面都会出现在新标签页中，而你的原始搜索结果页面仍保留在另一个标签页中，准备就绪（见图 5-2）。我很有信心地说，一旦你习惯了这个功能，你会想知道你以前怎么没有它。

Figure 5-1: Performing a Google search from the Firefox search box

Figure 5-2: A link opened in a new tab in Firefox

### Keeping Up-to-Date with Live Bookmarks

网络充斥着各种新闻和信息，很难跟踪所有内容。个人而言，我讨厌错过 Boing Boing 的每日离奇故事剂量，这个网站的副标题恰如其分地是“奇妙事物目录”（http://www.boingboing.net/）。幸运的是，Firefox 有一种巧妙的处理信息过载的方法，称为实时书签（也称为 RSS 订阅）。它们为任何支持它们的网站提供自动更新的文章列表。要看一个例子，点击 Firefox 地址栏下方的 Latest Headlines 链接——它是 BBC News 网站的实时书签，应该会显示给你一份长长的当前新闻故事列表。

你可以通过在地址栏中寻找橙色信标符号来检查网站是否具有 RSS 订阅（如下图 5-3 所示）。如果有，你就成功了！让我们以 Boing Boing 为例：在 Firefox 中加载 http://www.boingboing.net/，并点击信标图标。你会看到一份最新文章的列表以及页面顶部框中的订阅邀请。点击 Subscribe Now，然后在出现的窗口中点击 Subscribe，将实时书签添加到与 Latest Headlines 链接相同的工具栏中。

![](img/f7cef0df22f9dba5a41777808c98eece_99_0.png)

Figure 5-3: The beacon icon is displayed when a website has an associated RSS feed.

一些网站提供指向其 RSS 订阅的链接，而不是在地址栏中显示它们。如果你找到其中一个链接（它通常称为 ATOM 或 RSS/XML），点击它，你应该会被带到一份文章列表，顶部有一个框，就像前面的例子一样。从那里，将订阅源添加到书签中的步骤是相同的。

### Pop-up Manager

Firefox 还有许多其他有用的功能。其中之一是其弹出窗口管理器，它会抑制访问新网页时经常出现的那些烦人的弹出窗口。你可以从首选项窗口（Edit ▸ Preferences）启用或禁用此功能，点击该窗口顶部窗格中的 Content 图标，然后勾选或取消勾选 Block pop-up windows 框。你也可以允许某些站点提供弹出窗口（一些弹出窗口不仅有用，而且对站点正确运行是必要的），方法是点击该 Block pop-up windows 条目右侧的 Exceptions 按钮并输入相关站点的网址。

### Multimedia Plug-Ins

Firefox 最酷的事情之一是它允许你通过添加各种扩展来进一步扩展其功能。最常用的扩展以插件的形式出现。这些允许网页做的不只是显示文本和图片——你通常需要一个插件来观看视频或在线玩游戏。有三种插件比任何其他插件使用得更广泛，所以我将在这里集中介绍它们。

