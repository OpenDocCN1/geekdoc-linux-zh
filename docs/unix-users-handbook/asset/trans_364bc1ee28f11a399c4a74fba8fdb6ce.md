

调用 **mailx** 后，按下“Return（回车）”键即可读取第一封邮件。

文件 **trip** 是在使用 **s trip** 保存该邮件时创建的，现在我们可以将所有相关邮件存储到文件 **trip** 中。

保存到文件的邮件可以通过 **lp** 命令打印出来。我们将在本书的系统管理章节中详细讨论 **lp**；但目前只需知道，通过执行命令 **lp** *filename* 即可将文件打印到默认打印机。要打印文件 **trip**，我们需要执行命令 **lp trip**。

发送电子邮件和阅读电子邮件一样简单。发送信息的最简单方法是输入 **mailx** 或 **mail**，然后输入你想发送消息的人的*用户名*。我们将在下面的消息中对 *tomf* 执行此操作：

```
martyp $ mail tomf
Subject: Pickup
I'll be at the airport in NY to give you a ride.
Marty
Cc:
martyp $
```

使用 ^D（控制 D）结束了邮件消息。这条消息将位于 *tomf* 的邮箱中。如果你的系统启用了此功能，可以使用 Internet 命名法来发送消息。下面的示例展示了将同样的消息发送到 *tomf* 的 Internet 电子邮件地址：

```
martyp $ mail tomf@tomcompany.com
Subject: Pickup
I'll be at the airport in NY to give you a ride.
Marty
Cc:
martyp $
```

向其他系统和 Internet 地址发送消息的功能需要系统管理员设置此功能。

如果你的系统有图形用户界面，你很可能拥有一个帮助你管理邮件的工具。尽管该工具在你的图形环境中运行，但它可能正在使用我们之前介绍过的某个邮件程序。图 1-2 展示了在通用桌面环境中访问邮件。

![](img/75f39fc91296b889c0653851accdfd46_63_0.png)

图 1-2 在通用桌面环境中访问邮件

图 1-2 顶部的下拉菜单提供了选项，这些选项执行与之前介绍的保存、转发、删除等命令相同的功能。

## 访问 Internet

自 Internet 问世以来，它已在 UNIX 系统上得到广泛应用。第一个被广泛使用的 Web 浏览器是伊利诺伊大学开发的 X Window System 应用程序 Mosaic。如今，有许多可用于 UNIX 系统的 Web 浏览器，包括 Mosaic、Netscape Communicator 以及其他多种。本节将重点介绍 Netscape Communicator，因为它是 UNIX 系统上使用最广泛的浏览器。有许多 Netscape Communicator 软件包可用，有些选项与其他软件包不同，还有 Netscape Navigator，它是一种基础 Web 浏览器。因此，请记住，你可能没有 Netscape 浏览器，或者你拥有的 Netscape 浏览器与本节介绍的不同，但相同的原则适用于大多数浏览器。

你的系统管理员可能已经为你的 UNIX 系统配置了浏览器。许多 UNIX 发行版，例如本书许多示例中使用的 Linux Red Hat，都将浏览器作为操作系统发行版的一部分提供。在使用 UNIX 系统时，浏览器和 Internet 是宝贵的工具。你可以在提供该 UNIX 操作系统的公司的网站上找到有关该系统的最新信息。图 1-3 显示了 Netscape Communicator 窗口显示 Red Hat 主页。

![](img/75f39fc91296b889c0653851accdfd46_65_0.png)

从该主页，你可以搜索任何与 Red Hat Linux 操作系统相关的主题。我们通过指定浏览器*位置*框中的统一资源定位符（URL）来连接主页。在这种情况下，我们指定了 www.redhat.com，这是 Red Hat 的 URL。表 1-1 以字母顺序列出了本书中使用的四种引用最多的 UNIX 变体供应商的 URL。

**表 1-1 本书中使用的 UNIX 变体供应商 URL**

| URL | 结果 |
| --- | --- |
| www.hp.com | Hewlett-Packard 公司 |
| www.ibm.com | International Business Machines Corp. |
| www.redhat.com | Red Hat, Inc. |
| www.sun.com | Sun Microsystems, Inc. |

从这些主页开始，你可以逐步浏览网站以找到所需的信息。“逐步浏览”是这里的关键词。你很可能会使用正在查看的主页上的搜索机制，快速在网站上找到你需要的内容。另一方面，你可能需要花费大量时间在一个网站上寻找你想要的信息，并最终访问许多相关的网站以获取所需信息。

请注意，在图 1-3 中，www.redhat.com 前面是 http://。这是 URL 的协议部分。http:// 是用于指定 Web 页面的协议。存在许多此类协议。表 1-2 列出了一些常用的协议。

表 1-2 常用协议指定符

| 协议 | 结果 |
| :--- | :--- |
| file:<path name> | 按照 <path name> 指定的路径将本地文件加载到浏览器中。 |
| ftp:// | 将使用文件传输协议（ftp）。 |
| gopher:// | 将使用提供 Gopher 服务的主机。 |
| http:// | 将使用要访问的目标 Web 页面。 |
| https:// | 将使用要访问的目标安全 Web 页面。 |
| news:// | 将使用网络新闻服务器。 |

这些是与浏览器一起最常用的协议。

接下来的几幅图展示了你可以对浏览器进行的一些基本自定义设置。这些内容旨在让你了解大多数浏览器可执行的自定义类型。

尽管你的浏览器可能已经为你加载完成，但可能仍需要一些配置使其完全运行，或者你希望进行某些自定义。图 1-4 左侧展示了在 Netscape Communicator 中我们可以进行的几个自定义区域，在此示例中选择了 Fonts（字体）：

![](img/75f39fc91296b889c0653851accdfd46_68_0.png)

图 1-4 指定浏览器字体

在此示例中，我们选择 *Appearance*（外观）下的 *Fonts*（字体）以获取图 1-4 中显示的信息。在自定义选项中，我们可以指定在此应用程序中希望使用的字体大小。在 *Appearance* 下还有一个 *Colors*（颜色）选项，我们也可以通过类似的一组选项来调整此应用程序的颜色。

我们可以修改的下一类选项位于 *Navigator*（浏览器）下，如图 1-5 所示。

![](img/75f39fc91296b889c0653851accdfd46_69_0.png)

图 1-5 浏览器应用程序

在 *Navigator* 下，我们有三个潜在的自定义区域。我们正在查看 *Applications*（应用程序）窗口。此窗口列出了应用程序及其关联的“helper”（辅助程序）。

下一类选项是 *Mail and Newsgroups*（邮件和新闻组），如图 1-6 所示。

![](img/75f39fc91296b889c0653851accdfd46_70_0.png)

图 1-6 浏览器磁盘空间

在图 1-6 中，我们正在指定消息可以占用的磁盘空间量。由于邮件和新闻组都可能导致大量大消息发送到你的系统，因此你需要控制接收消息的大小以及根据消息年龄清除哪些消息。

下一类选项是 *Roaming User*（漫游用户），这与 Netscape 在漫游模式下使用时的设置有关。你可以选择要传输的配置文件的哪些方面，如图 1-7 所示。

![](img/75f39fc91296b889c0653851accdfd46_71_0.png)

图 1-7 漫游用户项目

图 1-7 展示了如果你使用漫游访问服务器，将会传输的一些项目。无论你在哪里使用 Netscape，你都希望你的 *User Preferences*（用户首选项）设置保持一致，此类选项为你的漫游设置提供了选择。

下一类选项是 *Composing*（撰写），它提供与你发布的 Web 文档相关的选项，如图 1-8 所示。

![](img/75f39fc91296b889c0653851accdfd46_72_0.png)

图 1-8 与发布相关的选择

我们在图 1-8 中查看 *Composing* 下的 *Publish*（发布），它提供关于你可能执行的与 Web 相关的发布的选项，例如文档的位置。

最后一类选项是 *Advanced*（高级），其中包含有关 *Cache*（缓存）和 *Proxies*（代理）的信息，如图 1-9 所示。

