
Before the Web came along, you had to use arcane UNIX commands to download and use files — it was simply too complicated for most of us. With the Web, however, anyone could enjoy the benefits of the Internet by using a Web browser — a graphical application that downloads and displays Web documents. A click of the mouse is all it takes to go from reading a document from your company Web site to downloading a video clip from across the country.

在网络出现之前，你必须使用晦涩的 UNIX 命令来下载和使用文件——这对我们大多数人来说太复杂了。然而，有了网络，任何人只需使用网页浏览器——一种下载并显示网页文档的图形应用程序——就能享受互联网的便利。只需点击鼠标，就能从阅读公司网站上的文档切换到从全国各地下载视频剪辑。

In this chapter, I briefly describe the Web and introduce Mozilla — the primary Web browser (and, for that matter, a mail and news reader, too) in Red Hat Linux. I also briefly discuss how you can create your own Web pages.

在本章中，我简要描述网络并介绍 Mozilla——Red Hat Linux 中的主要网页浏览器（顺便说一下，它也是邮件和新闻阅读器）。我还简要讨论如何创建自己的网页。

## Discovering the World Wide Web

## 探索万维网

If you have used a file server at work, you know the convenience of sharing files. You can use the word processor on your desktop to get to any document on the shared server.

如果你在工作中使用过文件服务器，你就知道共享文件的便利。你可以使用桌面上的文字处理器访问共享服务器上的任何文档。

Now imagine a word processor that enables you to open and view a document that resides on any computer on the Internet. You can view the document in its full glory, with formatted text and graphics. If the document makes a reference to another document (possibly residing on yet another computer), you can open that linked document by clicking the reference. That kind of easy access to distributed documents is essentially what the World Wide Web provides.

现在想象一个文字处理器，它能让你打开并查看互联网上任何计算机上的文档。你可以以其完整形式查看文档，包含格式化的文本和图形。如果文档引用了另一份文档（可能位于另一台计算机上），你可以通过点击引用打开该链接文档。这种对分布式文档的便捷访问本质上就是万维网提供的功能。

当然，文档必须采用标准格式，以便任何计算机（安装了适当的 Web 浏览器软件）都可以访问和解释该文档。而且在不同系统之间传输 Web 文档需要一种标准协议。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_387_0.png)

标准 Web 文档格式是超文本标记语言（`HTML`），而交换 Web 文档的标准协议是超文本传输协议（`HTTP`）。`HTML` 文档是文本文件，不依赖于任何特定的操作系统，因此可以在从 Windows 和 Mac 到任何类型的 UNIX 和 Linux 的任何系统上运行。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_387_1.png)

Web 服务器是一种软件，它向发出适当 `HTTP` 请求的任何客户端提供 `HTML` 文档。Web 浏览器是客户端软件，它实际从 Web 服务器下载 `HTML` 文档并以图形方式显示其内容。

### 像一只巨大的蜘蛛网

万维网是 Web 服务器及其提供的 `HTML` 文档的组合。这样来看，Web 就像一本巨大的书，其页面散布在整个互联网中。你使用计算机上运行的 Web 浏览器来查看这些页面——页面像巨大的蜘蛛网一样相互连接，文档遍布各地（如图 2-1 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_387_2.png)

图 2-1：

Web 就像数十亿个页面，散布在网络各处，你可以使用 Web 浏览器从计算机上阅读它们。

如果你能想象 Web 页面——`HTML` 文档——是由类似于巨大蜘蛛网的网络连接链接起来的，你就能明白为什么 Web 被称为“Web”。“World Wide”这一部分源于 Web 页面散布在世界各地这一事实。

### 链接和 URL

就像真正的书籍的页面一样，Web 页面包含文本和图形。然而，与真正的书籍不同，Web 页面可以包含多媒体，例如视频剪辑、声音以及可以实际带你前往这些页面的其他 Web 页面的链接。

Web 页面中的链接是对其他 Web 页面的引用，你可以沿着这些引用从一个页面跳转到另一个页面。Web 浏览器通常将这些链接显示为下划线文本（不同颜色）或图像。每个链接都像是对你的一个指示——类似于你在真正的书中可能会找到的“有关更多信息，请参阅第 4 章”。在 Web 页面中，你只需单击链接即可；Web 浏览器会调出引用的页面，即使该文档实际上可能位于互联网上某个遥远的计算机上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_388_0.png)

Web 页面中的链接被称为超文本链接，因为当你单击链接时，Web 浏览器会跳转到该链接引用的 Web 页面。

这种安排引发了一个问题。在真正的书中，你可能会要求读者前往书中的特定章节或页面。超文本链接如何指示所引用 Web 页面的位置？在万维网中，每个 Web 页面都有一个特殊名称，称为统一资源定位符（URL）。URL 唯一指定计算机上文件的位置。图 2-2 显示了 URL 的各部分。

图 2-2：

统一资源定位符（URL）的各部分。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_388_1.png)

如图 2-2 所示，URL 有以下各部分：

**协议：** Web 浏览器用于访问 URL 指定的文件数据的协议名称。在图 2-2 中，协议是 `http://`，这意味着 URL 指定了 Web 页面的位置。以下是一些常见的协议类型及其含义：

- `file://` 表示 URL 指向本地文件。你可以使用此 URL 在无需连接到互联网的情况下查看 HTML 文件。例如，`file:///var/www/html/index.html` 打开来自你的 Red Hat Linux 系统的文件 `/var/www/html/index.html`。

- `ftp://` 表示你可以使用文件传输协议（FTP）下载文件。例如，`ftp://ftp.purdue.edu/pub/uns/NASA/nasa.jpg` 指的是 FTP 服务器 `ftp.purdue.edu` 的 `/pub/uns/NASA` 目录中的图像文件 `nasa.jpg`。如果你想通过 FTP 访问特定的用户账户，请使用以下形式的 URL：

  `ftp://username:password@ftp.somesite.com/`

  用户名和密码嵌入在 URL 中（请注意，密码以明文形式出现且不安全）。

- `http://` 表示文件应使用超文本传输协议（HTTP）下载。这是所有网站的众所周知的 URL 格式，例如 Red Hat 主页的 `http://www.redhat.com`。如果 URL 没有文件名，Web 服务器会发送一个名为 `index.html` 的默认 HTML 文件（这是流行的基于 UNIX 的 Apache Web 服务器的默认文件名；Microsoft Windows Web 服务器使用不同的默认文件名）。
