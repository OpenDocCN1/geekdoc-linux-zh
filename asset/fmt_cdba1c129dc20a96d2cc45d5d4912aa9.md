
接下来，点击左侧的“账户”（Accounts），然后点击右侧的“新闻组服务器”（Newsgroup Servers）选项卡，查看你将从中阅读新闻的新服务器信息。点击“新闻组服务器”选项卡中的“添加”（Add），显示一个可以在其中输入新闻服务器信息的对话框。你的 ISP 应该已经为你提供了访问新闻服务器的信息。如果新闻服务器需要登录名和密码，你也必须输入这些信息。

设置账户后，KNode 窗口左侧会显示新闻服务器名称。右键点击服务器名称，从弹出菜单中选择“订阅新闻组”（Subscribe to Newsgroups）。将弹出一个对话框，你可以在其中订阅选定的新闻组（例如 `comp.linux.announce`）。

第一次访问此菜单时，必须获取新闻组列表。

KNode 的用户界面与许多其他邮件和新闻阅读器类似，包括 Thunderbird。

如果你无法通过 ISP 访问新闻组，你仍然可以在许多网站上阅读新闻组并发布文章。其中一些存档了旧新闻文章并提供了良好的搜索功能，因此你可以在这些网站上搜索与你可能的问题相关的文章。

通过网站阅读新闻组最好的处是，你甚至不需要访问新闻服务器，就可以从网络浏览器阅读新闻。

表 2-2 列出了提供免费访问 Usenet 新闻组的网站。要获取所有提供新闻组访问的网站列表（包括收费的），请使用 Google (`www.google.com`) 并输入搜索词 `usenet groups access`。

| 表 2-2 免费访问 Usenet 新闻组的网站 |
| :--- | :--- |
| 网站 | URL |
| Google Groups | http://groups.google.com |
| InterBulletin | http://news.interbullet.com |
| Usenet Replayer | www.usenet-replayer.com |

* www.it-ebooks.info

## 228 阅读 RSS 馈

阅读新闻组、发布文章和搜索旧新闻组存档的最佳地点之一是位于 `http://groups.google.com` 的网页 Google Groups（Google 的 Usenet 讨论论坛）。在该网站上，你可以选择一个新闻组进行浏览，并对在各种新闻组上发布的文章发表回复。

Google Groups 最棒的部分是它的搜索功能。目前，你已经知道 Google 的网页搜索有多强大了；你拥有同样全面的搜索能力来定位与你的搜索词相关的新闻组帖子。要搜索新闻组，请填写 `http://groups.google.com` 上的搜索表单并按回车。

要在 Google Groups 中浏览新闻组，请忽略搜索框并寻找高级列表...

## RSS 馈

### 检查 RSS 馈

RSS 馈是一个带有标签的文件，这些标签了网站的内容。你通常使用自动化程序生成 RSS 馈，但也可以使用文本编辑器准备 RSS 馈。了解 RSS 馈的外观很有帮助，这样可以调试馈的问题。

最简单的格式是 RSS 0.91，这里是典型的 RSS 0.91：

```xml
<?xml version="1.0" ?>
<!-- 注释行 -->
<rss version="0.91">
<channel><!-- 此标签指定有关馈的常规信息 -->
<title>此馈的标题</title>
<link>此馈的 URL，例如 http://edulaney.typeepad.com/</link>
<description>馈的摘要描述</description>
<language>en-us</language>
<item>
<title>此项目的标题</title>
<link>此项目的 URL</link>
<description>此项目的描述</description>
</item>
 <!-- 更多项目 ..
</channel>
</rss>
```

如列表所示，RSS 馈包含一个带有标题、链接和语言的通道，随后是一系列项目，每个项目都有标题、链接和描述。

RSS 1.0 格式更加冗长，它使用了 RDF 格式。RSS 1.0 基本上提供了 RSS 0.91 中的基本信息，并增加了项目级别的详细信息，如作者、主题和发布日期，这些是 RSS 0.91 不支持。

有很多 GUI 程序可以订阅 RSS 馈并读取馈中的项目。这些程序被称为 RSS 聚合器，因为它们可以从多个 RSS 馈收集信息并将所有内容集中在一个处。

两种类型的 RSS 聚合器是浏览器插件或独立程序。浏览器插件（如 NewsMonster (`www.newsmonster.org`)）运行在浏览器中，因此馈显示在网络浏览器中。独立程序如 GNOME Straw (`http://projects.gnome.org/straw`) 和 KDE Akregator (`http://aggregator.kde.org`) 是完整的 GUI 应用程序，通常外观彼此相似。

## 230 阅读 RSS 订阅

![](img/71f80d7808bf5b5ad1239cc29be7bab2_249_0.png)

Fedora 和 SUSE 都配备了 Akregator 程序，这是一个独立的 RSS 订阅聚合器。要运行它，请在 GUI 桌面面的应用程序菜单中查找链接（选择 应用程序；Internet；Akregator）。如果你没有看到 Akregator 列表，请在终端窗口中输入 `akregator`。在 Debian 中，你可以通过输入 `apt-get install akregator`（在输入 `su -` 成为 root 用户后）来安装 Akregator。

当 Akregator 首次运行时，它会显示一个没有任何 RSS 馈源的主窗口。要订阅一个源，请从菜单中选择“订阅：添加源”（Feed:Add Feed），或者在窗口左侧面板中右键点击“所有源”（All Feeds）并在弹出菜单中选择“添加源”（Add Feed）。然后在“添加源”对话框中使用该源的 URL 并点击确定（OK）。例如，要读取 Slashdot 的 RSS 订阅，请输入 `http://slashdot.org/index.rss`。源的标题出现在窗口的左侧面板中。点击源标题查看此源中的项目。然后你可以点击上方面板中的某个项目，该项目将出现在右下面板。你可以添加许多不同的 RSS 订阅，将它们组织到文件夹中并在 Akregator 中浏览它们。

# 第 3 章：使用 FTP

本章内容

- 使用 FTP 客户端
- 使用任何网络浏览器作为 FTP 客户端
- 了解 FTP 命令

顾如其名，*文件传输协议（FTP）* 用于在计算机之间传输文件。例如，如果你的互联网服务提供商（ISP）为你提供了个人网站空间，你可能已经使用过 FTP 上传了构成网站的文件。在你的计算机上使用 FTP 客户端，登录你的 ISP 账户，提供密码密码（password），并将文件从你的系统复制到 ISP 服务器。

你也可以使用 FTP 下载其他文件，例如从互联网上的其他计算机下载开源软件——在这种情况下，你不需要在远程系统上有账户即可下载文件。你只需要使用 *anonymous*（匿名）作为用户名登录，并提供你的电子邮件地址作为密码（事实上，你的浏览器可以代为此操作，你可能甚至不知道正在发生这种情况）。这种*匿名 FTP* 非常适合向任何想要文件的人分发文件。例如，硬件供应商可能会使用匿名 FTP 为任何需要的人提供更新的设备。

Linux 带有几个 FTP 客户端，包括命令行和 GUI（图形用户界面）客户端。本节将向你介绍几个 GUI 客户端和一个命令行客户端。它还描述了用于处理远程目录的命令。

![](img/71f80d7808bf5b5ad1239cc29be7bab_250_0.png)

根据你使用的 Linux 发行版和版本，你可能需要安装本章讨论的 FTP 客户端。你可以在 Linux 中使用以下 GUI 客户端之一：

- `gFTP`: 适用于 GNOME 的图形客户端，地址为 `http://gftp.org`。
- `FileZilla`: 适用于 Linux 和 Windows 平台的图形客户端，地址为 `https://filezilla-project.org`。
- 网络浏览器: 如 Firefox 等浏览器，用于匿名下载。

![](img/71f80d7808bf5b5ad1239cc29be7bab_250_1.png)

对于上传文件，你可能想使用 `gFTP` 或 `FileZilla`，因为你通常需要为此类传输提供用户名和密码。网络浏览器对于匿名下载运行良好，这通常是你从互联网上下载软件的方式。接下来的几节将讨论所有三个 GUI 客户端。

## 使用 gFTP

某些版本的 Ubuntu 自带了 `gFTP`，这是一个图形客户端。它不是默认安装的，但你可以从 `http://gftp.org` 下载并安装它。在某些发行版中，`gFTP` 可能包含在软件包中，你只需要安装它。`gFTP` 已经多年没有更新了，但仍被广泛使用，这证明了它的健壮性和工作的适用性。

安装好后，在主菜单中启动 `gFTP`，就会出现 `gFTP` 窗口，如图 3-1 所示。
