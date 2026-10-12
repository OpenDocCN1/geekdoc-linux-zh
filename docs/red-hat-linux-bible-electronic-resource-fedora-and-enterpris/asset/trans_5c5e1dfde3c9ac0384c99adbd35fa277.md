
本节包含有关 Web 的一般信息以及使用 Mozilla 在 Red Hat Linux 系统上浏览 Web 的一些具体提示。

## 统一资源定位符

要访问互联网上的站点，您可以输入浏览器地址栏中的 URL，或点击链接（网页上的链接，或浏览器菜单或按钮上的链接）。虽然 URL 如今随处可见——您可以在名片到麦片盒等一切东西上找到它们——您可能不知道 URL 是如何构造的。URL 的格式如下：

```
protocol://host-domain/path
```

协议标识您请求的内容类型。迄今为止，您遇到的最常见协议是超文本传输协议（HTTP）。HTTP 是用于请求网页的协议。然而，除了 HTTP 之外，在网页地址开头还可能出现其他协议。与其显示网页，这些其他类型的协议可能会在浏览器中显示不同类型的信息，或打开完全不同的应用程序来处理内容。

表 9-1 列出了可能出现在 Web URL 中的一些协议。

### 表 9-1：Web URL 中的协议

| 协议名称 | 描述 |
| :--- | :--- |
| http | 超文本传输协议。用于标识 HTML 网页及相关内容。 |
| file | 标识特定主机上的文件。最常用于显示本地计算机上的文件。 |
| ftp | 文件传输协议。标识包含可下载文件归档的位置。 |
| gopher | Gopher 协议。提供分布在互联网上的基于文本的文档数据库。（Gopher 已近乎废弃。） |
| mailto | 电子邮件地址。标识电子邮件地址，例如 mailto://joe@example.com。（通常打开邮件撰写器。） |
| news | USENET 新闻组。标识新闻组，例如 news://news.mysp.com/comp.os.linux.networking。如果您将此地址输入 Mozilla，将出现一个窗口，显示来自您指定的新闻服务器的新闻组。 |
| nntp | 使用 nntp 协议的 USENET 新闻。 |
| telnet | 登录远程计算机并开始交互式会话。telnet 地址的示例是 telnet://localhost。（将 localhost 替换为允许您登录的任何主机或 IP 地址。） |
| wais | 广域信息服务器协议。WAIS 地址可能如下所示：wais://handsonhistory.com/waisdb。（与 gopher 类似，WAIS 数据库已近乎废弃。） |

URL 的第一部分是协议。您并不总是需要输入协议。大多数浏览器擅长猜测您要查找的内容（大多猜测为 HTTP）。如果您输入的地址以 `www` 开头，它会假定为 HTTP；如果以 `ftp` 开头，则假定为 FTP。

URL 的第二部分会带您到托管网页内容的计算机。按惯例，Web 服务器以 `www` 开头（有时为 `home`）。然而，如果您输入正确的协议（通常为 `http`），您将被定向到主机计算机上的正确服务。此名称的下一部分只是互联网上始终使用的 `host.domain` 样式的互联网地址（例如 `redhat.com`、`linuxtoys.net` 或 `whitehouse.gov`）。可以在 `host.domain` 名称上附加可选的端口号。例如，要从名为 `www.linuxtoys.net` 的主机请求用于 HTTP 服务的端口（端口 80），您可以输入 `http://www.linuxtoys.net:80`。

**提示：** 您可以在请求时指定特定的端口号以请求计算机上端口所附带的服务。端口号很像大公司中的电话分机。一个主电话号码（如 `host.domain` 名称）会让您连接到公司总机。电话分机（如端口号）会将您连接到正确的人（如与端口关联的服务）。

URL 的第三部分标识主机计算机上内容的位置。网页中的各节可以用井号（#）和位于网页位置之后的标识符来标识。例如，`handsonhistory.com` 上 `bsched.htm` 页面的 `craft` 部分将显示为 `http://www.handsonhistory.com/bsched.htm#craft`。文件名扩展名（如 `.htm` 或 `.html`）进一步标识内容类型。

## 网页

如果您查看生成网页的 HTML 源代码，您会看到它由信息和标记标签的组合组成，所有这些都以纯文本格式呈现。想法是让网页非常便携和灵活。您可以使用 `vi`、`emacs`、记事本或任何文本编辑器在任何计算平台上创建网页。或者可以使用简化的前端程序来提供所见即所得（What You See Is What You Get）界面，让您在创建过程中看到正在创建的内容。

HTML 标签由右尖括号和左尖括号分隔。标签成对出现，包含开始标签、信息，然后是结束标签。开始标签包含标签名，而结束标签包含正斜杠（/）和标签名。下面是一个最简的 HTML 页面：

```
<HTML>
<HEAD>
<TITLE>Greetings from Washington</TITLE>
</HEAD>
<BODY>
Here we are in beautiful Tacoma.
</BODY>
</HTML>
```

您可以看到文档以 HTML 标签开始和结束（ `<HTML>` 和 `</HTML>` ）。网页的开头部分包含在 `HEAD` 标签内。页面的主体包含在 `BODY` 标签内。页面的标题由 `TITLE` 标签分隔。

在开始和结束 `BODY` 标签之间，您可以添加各种内容。您可以拥有不同类型的项目符号或编号列表。您可以拥有标题、图像和文本。更复杂的页面可以包含表单、动态 HTML（在您移动或选择项目时更改内容）或特殊数据。图 9-1 是 Mozilla 中网页的外观示例。

下面显示了用于创建图 9-1 所示网页的一些 HTML 代码。网页的标题出现在两个 `TITLE` 标签之间。

```
<TITLE>Swan Bay Folk Art Center - American Crafts in Port Republic, NJ</TITLE>
```

![](img/27a85d56d393921ced6412ae6e8336bf_326_0.png)

**图 9-1：许多网页包含文本、图像、标题和链接。**

以下代码用于创建打开新邮件消息窗口的链接：

```
<A HREF="mailto:webmaster@hudsonhistory.com">Contact Us</A>
```

文本 **联系我们** 是指向电子邮件地址的链接。当有人点击该链接时，会出现一个新的消息窗口，允许该人向该地址发送电子邮件。

```
<FONT FACE="Copperplate Gothic Bold"><A HREF="bsched.htm">Bakery Classes</A></FONT>
```

使用了特殊的字体来显示 **烘焙课程** 字样，并将这些字指向另一个 HTML 页面的链接。如果有人点击这些字，**bsched.htm** 页面将会出现。

## 使用 Mozilla 进行网页浏览

在 1990 年代初期，Netscape Navigator 是最流行的网页浏览器。当 Netscape 明显失去对 MS Internet Explorer 的领先地位时，Netscape 的源代码作为开源代码发布给了世界。

Mozilla.org 成立是为了协调从该代码开发新浏览器。结果是 Mozilla 浏览器，现在可与 Red Hat Linux 以及许多其他计算平台一起使用。最近，Mozilla 基金会成立（www.mozillafoundation.org），以便为 Mozilla 项目今后的发展获得非营利地位。

当然，Mozilla 的核心是 Navigator 网页浏览器。Mozilla 还包括以下功能：

- **邮件和新闻组** — 用于发送、接收和管理电子邮件以及使用新闻组的全功能程序。（必须安装 mozilla-mail RPM。）
- **IRC 聊天** — 用于参与在线文字对话的 Internet Relay Chat（IRC）窗口，名为 ChatZilla。（必须安装 mozilla-chat 软件包。）
- **Composer** — 网页（HTML）撰写应用程序。
- **地址簿** — 用于管理姓名、地址和电话号码的应用程序。（此功能也是 mozilla-mail RPM 软件包的一部分。）

您可以直接在桌面面板上点击 Mozilla Web Browser 图标来启动 Mozilla。或者您可以从桌面菜单（从红帽开始）打开 Mozilla，选择 Internet → Mozilla Web Browser。图 9-2 显示了 Mozilla 浏览器显示 Mozilla 主页（www.mozilla.org）的示例。

![](img/27a85d56d393921ced6412ae6e8336bf_327_0.png)
