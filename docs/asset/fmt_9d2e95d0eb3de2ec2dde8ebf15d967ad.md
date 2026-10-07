
`cdrecord -v dev=/dev/cdrom -audio fly_fly.wav big_name.wav`

`about_time.wav`

```
Grip 窗口也可用于播放 CD。使用显示底部的按钮来播放、跳进或后退以及弹出 CD。Toggle track display（切换曲目显示）可以缩小显示尺寸，使其不占用太多桌面空间。点击 Toggle discard（切换丢）来编辑和更改标题、艺术家和曲目信息。

除了 grip 之外，Fedora 还包含 Sound Juicer CD 刻录机，你可以通过从红帽菜单选择 Video -> Sound Juicer CD Ripper 来启动它。Sound Juicer 还可以从音频 CD 中提取（或刻录）文件。Sound Juicer 在刻录 CD 时质量可能略好。
```

## 使用 cdlabelgen 创建 CD 标签

`cdlabelgen` 命令可用于创建适应 CD 盒的托盘卡和封面卡。你收集 CD 的信息，`cdlabelgen` 会生成一个可以发送到打印机的 PostScript 输出文件。`cdlabelgen` 软件包还附带图形（位于 `/usr/share/cdlabelgen` 中），你可以将其整合到标签中。

这是一个你可以用于生成 PostScript 格式 CD 标签文件的 `cdlabelgen` 命令行示例。在一行中输入它，或如此处所示使用反斜杠将其放在多行。

```
cdlabelgen -c "Grunge is Gone" -s "Yep HipHop" \
-i "If You FeedMe Sock Years&City Road&Platinum and Copper&Fly Fly \
Fly&Best Man Spins&What A Headache&stayin Put Feelin&Dreams Do Go \
Blue&UsWild Schemes" -o yep.ps
```

在此示例中，CD 标题由 `-c "Grunge is Gone"` 指定，艺术家由 `-s "Yep HipHop"` 选项指定。曲目输入在 `-i` 选项之后，每行之间用 `%` 符号分隔。输出文件通过 `-o` 选项发送到文件 `yep.ps`。要查看并打印结果，你可以如下使用 `ggv` 命令：

```bash
$ ggv yep.ps
```

此示例的结果如图 8-11 所示。

你可能需要编辑命令并重新运行几次 `ggv`，以获得正确的 CD 标签。当你准备好打印标签时（假设你已为电脑配置了打印机），点击 Print All（全部打印）来打印标签。

## 总结

为你的 Fedora 系统配置音频视频可能需要一些工作，但一旦完成，你就可以播放今天可用的大多数音频视频内容。本章将引导你完成设置和排错声卡的步骤，并解释如何找到软件通过该声卡播放音乐。

在 Tvtime 和 GnomeMeeting 章节中分别介绍了来自电视卡和网络摄像头的实时视频。最后，我涵盖了用于播放各种视频格式的 xine 播放器以及用于从数字相机下载图像的 gtkam 窗口。如果你的电脑有 CD 刻录机，可以使用本章中的描述创建自己的音乐 CD。

# 第 9 章：网络工具

### 本章内容

- 浏览网页
- 通过电子邮件通信
- 参与新闻组
- 使用即时消息
- 使用登录 `login`
- 使用执行 `execution`

### 互联网工具概述

如今最重要的客户端是 Web 浏览器。本章介绍了 Fedora 中提供的用于浏览网页和下载文件的流行工具。这些：

- **Epiphany** —— 该浏览器与 GNOME 集成，允许你利用 GNOME 功能。
- **Konqueror** —— 虽然 Konqueror 是 KDE 桌面的文件管理器，但它也可以显示 Web 内容。

推荐的电子邮件客户端是 Mozilla（在网络标准中称为邮件用户代理，MUA）。其他选项包括 Sylfed 邮件客户端或 KDE 的 Kmail。还有一个名为 Contact 的 KDE 群组应用程序。

你可以从成千上万的新闻组中选择参与互联网讨论。Fedora 提供了几种阅读器。

此外，还有许多方法与互联网上的其他计算机和用户通信。旧 UNIX 命令如 `login`、`rsh` 和 `rcp` 在 Linux 中用于远程登录、运行命令和复制文件。近年来，OpenSSH 命令（`ssh`、`scp` 和 `sftp`）比“r-” 命令更受欢迎。

### 浏览网页

尽管互联网自 20 世纪 60 年代以来一直存在，但 Web是一项相对新的技术（它于 1985 年创建）。Web 为只有主机名和域名的互联网 地址提供了额外的框架。在 Web 出现之前，在互联网上寻找资源是很困难的。但 Web 现在提供了许多功能使得访问变得更容易：

- **统一资源定位符 `URL`** —— `URL` 标识 Web 上的资源。除了标识资源所在的域名和主机外，它们还可以标识内容类型和内容的具体位置。
- **超文本标记语言 `HTML` 页面** —— 当人们谈论 Web 页面时，通常指的是以 HTML 格式呈现的信息。HTML 改变了互联网，从纯文本资源变为可以呈现图形和字体的资源。HTML 页面还可以包含超链接。链接是把 Web 连接在一起的线，使得查看 Web 页面的人只需选择链接文本字符串或图像即可跳转到另一个 Web 页面（或其他内容）。

# 第 9 章：互联网和 Web 使用工具

显示 HTML 页面的主要工具是 Web 浏览器。Mozilla 是 Fedora 最受欢迎的 Web 浏览器。它可以显示 HTML（网页）以及其他类型的 Web 内容。现在，即使是用于显示本地文件和文件夹的文件管理器也扩展到了显示 Web 内容的功能（参见第 3 章中对 Konqueror 文件管理器的描述）。

本节包含关于 Web 的通用信息，以及关于如何在自己的系统中中使用 Mozilla 浏览网页的一些特定提示。

## 统一资源定位符 `URL`

要访问互联网上的站点，你可以在浏览器的位置框中输入 URL，或者点击链接（网页上的链接或来自菜单或按钮的链接）。URL 如今已无处不在——你从名片到麦片盒都能找到它们——但你可能不知道 URL 是如何构造的。URL 的格式如下：

```
protocol://domain/path
```

协议 `protocol` 标识你正在请求的内容类型。到目前，你最常用的协议是超文本传输协议 `HTTP`。HTTP 是请求网页时使用的协议。除了 HTTP 之外，还有其他可能出现在 Web 地址开头的协议。这些其他类型的协议可能不会在浏览器中显示 Web 页面，而是显示不同类型的信息，或者打开一个完全不同的应用程序来处理内容。

表 9-1 列出了可能出现在 Web URL 中的某些协议。

### 表 9-1：Web URL 中的协议

| 协议名称 | 描述 |
| --- | --- |
| http | 超文本传输协议。用于识别 HTML 网页和相关内容。 |
| file | 标识特定主机上的文件。通常用于显示来自本地计算机的文件。 |
| ftp | 文件传输协议。标识存放你可能想要下载的文件归包的位置。 |
| gopher | Gopher 协议。提供分布在互联网上的基于文本的数据库。（Gopher 几乎已过时。） |
| mailto | 电子邮件地址。识别电子邮件地址，例如 `mailto@example.com`（通常会打开邮件邮件撰写器）。 |
| news | USEN 新闻组。识别新闻组，例如 `news://news.myisp.com/comp.os.linux.networking`。如果你在 Mozilla 中输入此地址，将弹出一个窗口显示来自你识别服务器的新闻组。 |
| nntp | 使用 `nntp` 协议的 USEN 新闻。 |
| telnet | 登录远程计算机并开始交互会话。`tel` 地址的示例是 `telnet://localhost`。（将 `localhost` 替换为允许登录的任何主机或 IP 地址。） |
| wais | 广域网信息服务器协议。WAIS 地址可能如下所示：`wais://handsonhistory.com/waisdb`。（与 gopher 类似，WAIS 数据库几乎已过时。） |

URL 的第一部分是协议。你不总是必须输入协议。大多数浏览器都擅长猜测你正在寻找的内容（大多数情况下它猜是 HTTP）。如果你输入的地址以 `www` 开头，它假设是 HTTP；如果以 `ftp` 开头，它假设是 FTP。

URL 的第二部分将你带到托管 Web内容的计算机。按照惯例，Web 服务器以 `www`（有时是 `home`）开头。然而，如果你输入了正确的协议（通常是 `http`），你将被重定向到主机计算机上的正确服务。该名称的下一个部分只是主机。互联网地址的主机.domain 名称始终与互联网配合（如 `redhat.com`、`linuxtoys.net` 或 `whitehouse.gov`）。可以在主机.domain 名称后面附加一个可选的端口号。例如，要从主机 `wais.linuxoys.net` 请求用于 HTTP 服务的端口（端口 80），你可以输入 `http://linuxoys.net:80`。

> 提示：你可以指定特定的端口号，以请求请求计算机上连接到该端口的服务。端口号就像大公司里的电话分机。主电话号码（如主机.domain 名称）带你找到公司总机。电话分机（如端口号）将你连接到正确的人（如与端口关联的服务）。

URL 的第三部分标识内容在主机计算机上的位置。网页中的章节可以使用井号 `#` 和紧跟在网页位置后的标识符来识别。例如，`handsonhistory.com` 上 `bsched.html` 页面的 `craft` 部分将显示为：

```
http://www.handsonhistory.com/bsched.htm#craft
```

文件名扩展名（如 `.htm` 或 `.html`）进一步标识了内容类型。

## 网页

如果你查看生成网页的 HTML 源代码，你会发现它由信息和标记标签组合而成，所有内容都是纯文本格式。这种设计理念是为了让网页具有良好的可移植性和活性。你可以在任何计算平台上使用 `vi`、`emacs`、`edit`、`Notepad` 或任何文本编辑器创建网页。或者，可以使用简化的前端程序提供 WYSIWYG（所见即所得）界面，让你在创建过程中看到你正在创建的内容。

HTML 标签通过左、右尖角括号隔开。标签成对出现，包含一个起始标签、信息和一个结束标签。起始标签包含标签名称，而结束标签包含一个正斜线 `/`。

```
<HTML>
<HEAD>
<TITLE>Greetings from Washington</TITLE>
</HEAD>
<body>
Here we in Linux.
</body>
</HTML>
```

URL 的第一部分是协议。你你不总是必须输入协议。大多数浏览器都擅长猜测你正在寻找的内容（大多数情况下它猜是 HTTP）。如果你输入的地址以 `www` 开头，它假设是 HTTP；如果以 `ftp` 开头，它假设是 FTP。

URL 的第二部分将你带到托管 Web内容的计算机。按照惯例，Web 服务器以 `www`（有时是 `home`）开头。然而，如果你输入了正确的协议（通常是 `http`），你将被重定向到主机计算机上的正确服务。该名称的下一个部分只是主机。互联网地址的主机.domain 名称始终与互联网配合（如 `redhat.com`、`linuxtoys.net` 或 `whitehouse.gov`）。可以在主机.domain 名称后面附加一个可选的端口号。例如，要从主机 `wais.linuxoys.net` 请求用于 HTTP 服务的端口（端口 80），你可以输入 `http://linuxoys.net:80`。

> 提示：你可以指定特定的端口号，以请求请求计算机上连接到该端口的服务。端口号就像大公司里的电话分机。主电话号码（如主机.domain 名称）带你找到公司总机。电话分机（如端口号）将你连接到正确的人（如与端口关联的服务）。

URL 的第三部分标识内容在主机计算机上的位置。网页中的章节可以使用井号 `#` 和紧跟在网页位置后的标识符来识别。例如，`handsonhistory.com` 上 `bsched.html` 页面的 `craft` 部分将显示为：

```
http://www.handsonhistory.com/bsched.htm#craft
```

文件名扩展名（如 `.htm` 或 `.html`）进一步标识了内容类型。

```
<FONT FACE="Copperplate Gothic"><A HREF="bsched.html">Adult Basketry</A></FONT>
```

使用了特殊的字体用于 Adult Basketry 字词，这些词指向另一个页面的链接。如果有人点击这些词，将出现 `bsched.htm` 页面。

```html
<A HREF="mailto:webmaster@hansonhistory.com">Contact Us</a>;
```
