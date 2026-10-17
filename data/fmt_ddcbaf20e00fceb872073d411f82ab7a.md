
虽然 Internet 自 1960 年代起就已存在，但 Web 是一项相对较新的技术（它创建于 1985 年）。Web 在曾经仅限于主机名和域名上的 Internet 地址之上添加了一个额外的框架。在 Web 出现之前，在 Internet 上查找资源是很困难的。然而，Web 现在提供了多项功能，使访问这些资源变得更加容易：

- **统一资源定位器（URL）** — URL 用于标识 Web 上资源的位置。除了标识资源所在的域和主机外，它们还可以标识内容的类型和内容的具体位置。
- **超文本标记语言（HTML）Web 页面** — 当人们提到 Web 页面时，通常指的是以 HTML 格式呈现的信息。HTML 将 Internet 从纯粹的基于纯文本的资源转变为可以呈现图形和字体变化的资源。HTML 页面还可以包含超文本链接。链接是将 Web 连接在一起的线索，使浏览 Web 页面的人只需选择页面上的链接文本字符串或图像，即可立即传输到另一个 Web 页面（或其他内容）。

显示 HTML Web 页面的主要工具是 Web 浏览器。Mozilla 和 Netscape Communicator 是 Red Hat Linux 上最受欢迎的 Web 浏览器。两者都可以显示 HTML（Web 页面）以及各种其他类型的 Web 内容。如今，甚至用于显示本地文件和文件夹的文件管理器也已被扩展，能够显示 Web 内容（参见第 4 章中 Nautilus 图形外壳的描述）。

本节包含有关 Web 的一般信息，以及一些有关使用 Netscape Communicator 或 Mozilla 从您的 Red Hat Linux 系统浏览 Web 的具体提示。

## 统一资源定位器

要访问 Internet 上的站点，您要么在浏览器的位置框中输入 URL，要么单击链接（无论是在 Web 页面上，还是在浏览器的菜单或按钮上）。虽然 URL 如今已随处可见——您可以在从名片到麦片盒子的所有东西上找到它们——您可能并不了解 URL 是如何构建的。URL 的形式通常如下：

```
protocol://host-domain/path
```

协议标识了您请求的内容类型。迄今为止，您遇到的最常见的协议是超文本传输协议（HTTP）。HTTP 是用于请求 Web 页面的协议。然而，除了 HTTP 之外，还有其他协议可能会出现在 Web 地址的开头。这些其他类型的协议不会向您显示 Web 页面，而是可能在您的浏览器中显示不同类型的信息，或者打开一个完全不同的应用程序来处理该内容。

表 9-1 列出了一些可能出现在 Web URL 中的协议。

## 表 9-1：Web URL 中的协议

| 协议名称 | 描述 |
|---|---|
| http | 超文本传输协议。用于标识 HTML Web 页面及相关内容。 |
| file | 标识特定主机上的文件。最常用于显示来自本地计算机的文件。 |
| ftp | 文件传输协议。标识包含您可能想要下载文件的文件归档的位置。 |
| gopher | Gopher 协议。提供主要由基于文本的文档组成的数据库，这些文档分布在 Internet 上。（Web 页面和搜索引擎已使 gopher 几乎被淘汰。） |
| mailto | 电子邮件地址。标识电子邮件地址，例如 mailto://webmaster@handsonhistory.com。在 Netscape 中输入此类型的地址会导致打开一个新的邮件消息窗口，准备创建消息。 |
| news | USENET 新闻组。标识一个新闻组，例如 news://news.myisp.com/comp.os.linux.networking。如果在 Netscape 中输入此地址，会出现一个消息窗口，显示来自您指定的新闻服务器的新闻组。 |
| nntp | 使用 nntp 协议的 USENET 新闻。使用 nntp 协议标识一个 USENET 新闻组。 |

## 表 9-1（续）

| 协议名称 | 描述 |
|---|---|
| telnet | 登录到远程计算机并开始交互式会话。Telnet 地址的一个示例是 `telnet://localhost`。在 Netscape 中输入一个 Telnet 地址，Telnet 窗口将打开并尝试让你登录到指定的计算机。（你可以将 `localhost` 替换为任何允许你登录的计算机名称或 IP 地址。） |
| wais | 广域信息服务（Wide Area Information Server）协议。一个 WAIS 地址可能如下所示：`wais://handsonhistory.com/waisdb`。WAIS 地址提供了对 WAIS 数据库的访问。（与 gopher 类似，WAIS 数据库几乎已经过时。） |

URL 的第一部分是协议。如果你以前使用过 Netscape Communicator 或其他 Web 浏览器，你会发现你并不总是需要输入协议。Netscape 很擅长猜测你想要查找的内容类型（它通常猜测为 HTTP）。如果你输入的地址以 www 开头，它假定是 HTTP；如果以 ftp 开头，它假定是 FTP 协议。

URL 的第二部分将你引导到托管 Web 内容的计算机。按照惯例，Web 服务器以 www 开头（有时是 home）。然而，只要你输入正确的协议（通常是 http），你就会被重定向到主机计算机内的正确服务。该名称的下一部分始终是与互联网一起使用的 host.domain 样式的互联网地址（例如 redhat.com、handsonhistory.com 或 whitehouse.gov）。最后，可以在 host.domain 名称后附加一个可选的端口号。例如，要具体请求从名为 www.handsonhistory.com 的主机使用 HTTP 服务的端口（80 端口），你可以输入：

`http://www.handsonhistory.com:80`

> **提示：** 你可以查看你的 Red Hat Linux 计算机使用的标准端口和服务。大多数都包含在你的 Red Hat Linux 系统的 `/etc/services` 文件中。端口号非常像大公司里的分机号。主电话号码（就像 host.domain 名称）让你到达公司总机。分机号（就像端口号）将你连接到正确的人（就像端口关联的服务）。

URL 的第三部分也是最后一部分，标识内容在主机计算机上的具体位置。Web 页面内的部分可以通过在 Web 页面位置后加上井号（#）和标识符来识别。例如，handsonhistory.com 上 bsched.htm 页面中的手工艺部分将由以下 URL 标识：

`http://www.handsonhistory.com/bsched.htm#craft`

请注意，文件扩展名（如 .htm 或 .html）可以进一步标识内容类型（在本例中为 HTML 页面）。

### Web 页面

如果你查看生成 Web 页面的 HTML 源代码，你会发现它由信息和标记标签的组合组成，所有这些都以纯文本格式呈现。其目的是使 Web 页面具有高度的可移植性和灵活性。你可以使用 vi、emacs、记事本或任何计算平台上的任何文本编辑器来创建 Web 页面。或者可以使用简化的前端程序提供所见即所得（WYSIWYG，What You See Is What You Get）界面，让你在选择过程中看到正在创建的内容。

HTML 标签由右尖括号和左尖括号分隔。标签成对出现，包括开始标签，后跟信息，然后是结束标签。开始标签包含标签名称，而结束标签包含前斜杠（/）和标签名称。一个最小的 HTML 页面包含以下代码：

```html
<HTML>
<HEAD>
<TITLE>Greetings from Washington</TITLE>
</HEAD>
<BODY>
Here we are in beautiful Gig Harbor.
</BODY>
</HTML>
```

你可以看到文档以 HTML 标签开始和结束（`<HTML>` 和 `</HTML>`）。Web 页面的开头部分包含在 HEAD 标签内。页面的主体包含在 BODY 标签内。页面的标题（显示在浏览器标题栏中）由 TITLE 标签分隔。

在开始和结束 BODY 标签之间，你可以添加各种内容。你可以拥有不同类型的带项目符号或编号的列表。你可以拥有标题、图像和文本。更复杂的页面可以包含表单、动态 HTML（随着你移动或选择项目而改变内容）或特殊数据。图 9-1 是 Netscape Communicator 中显示的 Web 页面的一个示例。

用于创建图 9-1 中显示的 Web 页面的一些 HTML 代码如下。Web 页面的标题出现在两个 TITLE 标签之间。

```html
<TITLE>Swan Bay Folk Art Center - American Crafts
in Port Republic, NJ</TITLE>
```

![](img/1744bde8c889adfab3fc911e1687fecf_347_0.png)

图 9-1：许多 Web 页面包含文本、图像、标题和链接。

以下代码用于创建一个打开新邮件消息窗口的链接：
