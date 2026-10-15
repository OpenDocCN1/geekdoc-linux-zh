
`protocol://host-domain/path`

协议标识你正在请求的内容类型。到目前为止，你最常见的协议是超文本传输协议 (`HTTP`)。`HTTP` 是请求网页时使用的协议。除了 `HTTP` 之外，还有其他协议可能出现在 Web 地址的开头。这些其他类型的协议可能不会为你显示网页，而是在你的浏览器中显示不同类型的信息，或者打开完全不同的应用程序来处理该内容。

表 9-1 列出了可能出现在 Web URL 中的某些协议。（如表所示，其中某些协议在现代浏览器中已不再被支持。）

## 表 9-1：Web URL 中的协议

| 协议名称 | 描述 |
| --- | --- |
| http | 超文本传输协议。用于识别 HTML 网页和相关内容。安全版本是基于安全套接字层的超文本传输协议 (`https`)。 |
| file | 标识特定主机上的文件。通常用于显示来自本地计算机的文件。 |
| ftp | 文件传输协议。标识文件存档的位置，你可能想从那里下载文件。 |
| gopher | Gopher 协议。提供分布在互联网上的基于文本的文档数据库。（Gopher 几乎过时。） |
| mailto | 电子邮件地址。识别电子邮件地址，例如 `mailto:joe@example.com`。（通常会打开邮件撰件器。） |
| news | USENET 识别新闻组，如 `news://news.mysisp.com/os.linux.networking`。如果你在 Mozilla Navigator 中输入此地址，将出现一个窗口，显示从你识别的服务器发送的新闻。（在 Firefox 中，`news` 默认不是一个注册协议。） |
| nntp | 使用 `nntp` 协议的 USENET 新闻。 |
| telnet | 登录远程计算机并开始交互会话。`telnet` 地址的一个示例是 `telnet://localhost`。（将 `localhost` 替换为任何允许你登录的主机或 IP 地址。） |
| wais | 广域信息服务器。`WAIS` 地址可能像如下：`wais://handshistory.com/waisdb`（与 `gopher` 一样，`WAIS` 数据库几乎过时。） |

URL 的第一部分是协议。你不总是需要输入协议。大多数浏览器都擅长猜测你正在寻找的内容（大部分猜的是 `HTTP`）。你输入的地址以 `www` 开头，浏览器会假设是 `HTTP`；如果以 `ftp` 开头，它会假设是 `FTP`。

URL 的第二部分带你到达托管 Web 内容的计算机。按照惯，Web 服务器以 `www`（有时是 `home`）开头。然而，如果你输入了正确的协议（通常是 `http`），你将被引导到主机计算机上的正确服务。

该名称的下一部分只是 `host.domain` 风格的互联网地址，这种格式一直用于互联网（例如 `redhat.com`、`linuxxtoys.net` 或 `whitehouse.gov`）。可选的端口号可以附加在 `host.domain` 名上。例如，为了从名为 `www.linuxxtoys.net` 的主机请求用于 `HTTP` 服务的端口（端口 80），你可以这样做。

URL 的第三部分是路径。路径指向服务器上的特定资源或目录。例如，在 `http://www.linuxxtoys.com/index.html` 中，路径为 `/index.html`。

## 网页

如果你查看 HTML 源，你会发现它由标记组成。标记由左右尖括号隔开。标记成对出现，有一个起始标记和一个结束标记。起始标记包含标记名称，而结束标记包含一个斜杠（`/`）和标记名称。这是一个最小的 HTML 页面：

```html
<html>
<head>
<title>来自威斯康星的问候</title>
</head>
<body>
我们在麦迪逊。
</body>
</html>
```

你可以看到文档以 `HTML` 标记开始和结束（`<html>` 和 `</html>`）。页面的起始部分位于 `head` 标记内。页面主体位于 `body` 标记内。页面标题由 `title` 标记隔开。

在起始和结束 `body` 标记之间，你可以添加各种内容。你可以有不同类型的项目列表或编号列表。你可以有标题、图像和文本。复杂的页面可以包含表单、动态 HTML（随你的移动或选择更改内容）或特殊数据。图 9-2 显示了在 Firefox 中显示的网页示例。

![](img/74f214fbb2938b570bec5f957507ac66_399_0.png)

用于创建图 9-2 所示网页的某些 HTML 代码所示。网页标题位于两个 `title` 标记之间：

```html
<title>Swan Bay Folk Art Center - 新泽州 Port Republic 的美国工艺</title>
```

以下代码用于创建一个打开新邮件窗口的链接：

```html
<a href="mailto:webmaster@hansonhistory.com">联系我们</a>
```

文本 `联系我们` 是一个指向电子邮件地址的链接。当有人点击此链接时，会弹一个新的消息窗口，允许他们向该地址发送电子邮件。

```html
<a href="bsched.htm">
新篮筐课程！
</a>
```
