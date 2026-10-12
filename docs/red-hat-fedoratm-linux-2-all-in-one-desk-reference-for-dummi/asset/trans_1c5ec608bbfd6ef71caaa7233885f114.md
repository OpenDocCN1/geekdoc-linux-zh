

# Web 服务器与 Web 浏览器

如 **图 2-2** 所示，URL 包含以下部分：

-   **协议：** 协议名称，用于指定 Web 浏览器如何访问 URL 所指定文件中的数据。在 **图 2-2** 中，协议是 `http://`，这意味着该 URL 指定了一个 Web 页面的位置。以下是一些常见协议类型及其含义：
    -   `file://` 表示该 URL 指向一个本地文件。您可以使用这种 URL 在不连接互联网的情况下查看 HTML 文件。例如，`file:///var/www/html/index.html` 会打开 Fedora Core 系统中的 `/var/www/html/index.html` 文件。
    -   `ftp://` 表示您可以使用文件传输协议（FTP）下载文件。例如，`ftp://ftp.purdue.edu/pub/uns/NASA/nasa.jpg` 指的是 FTP 服务器 `ftp.purdue.edu` 的 `/pub/uns/NASA` 目录下的图像文件 `nasa.jpg`。如果您想通过 FTP 访问特定的用户账户，请使用以下形式的 URL：`ftp://username:password@ftp.somesite.com/`，其中用户名和密码嵌入在 URL 中（请注意，密码是明文形式，不安全）。
    -   `http://` 表示文件使用超文本传输协议（HTTP）下载。这是所有 Web 站点 URL 的知名格式，例如 Fedora 项目主页的 `http://fedora.redhat.com`。如果 URL 没有文件名，Web 服务器会发送一个默认的 HTML 文件，通常名为 `index.html`（这是流行的基于 UNIX 的 Apache Web 服务器的默认文件名；Microsoft Windows Web 服务器使用不同的默认文件名）。
    -   `https://` 指定文件通过安全套接字层（SSL）连接访问——这是一种由 Netscape Communications 设计的、用于在互联网上进行加密数据传输的协议。这种形式的 URL 通常用于 Web 浏览器向 Web 服务器发送敏感信息（如信用卡号、用户名和密码）时。例如，像 `https://some.site.com/secure/takeorder.html` 这样的 URL 可能会显示一个 HTML 表单，请求信用卡信息和其他个人信息（如姓名、地址和电话号码）。
    -   `mailto:` 指定一个您可以用来发送电子邮件消息的电子邮件地址。此 URL 会打开您的电子邮件程序，您可以从中发送消息。例如，`mailto:webmaster@someplace.com` 指的是主机 `someplace.com` 的 Web 管理员。
    -   `news://` 指定一个可以通过网络新闻传输协议（NNTP）阅读的新闻组。例如，`news://news.md.comcast.giganews.com/comp.os.linux.setup` 访问新闻服务器 `news.md.comcast.giganews.com` 上的 `comp.os.linux.setup` 新闻组。如果您为 Web 浏览器配置了默认的新闻服务器，您可以省略新闻服务器名称，并使用 URL `news:comp.os.linux.setup` 来访问该新闻组。

-   **域名：** 包含有该 URL 所指文件的计算机的完全限定域名。您也可以在字段中提供 IP 地址。域名不区分大小写。
-   **端口：** 协议（URL 第一部分中列出的协议）正在使用的端口号。URL 的这一部分是可选的；所有协议都有默认端口。例如，HTTP 的默认端口是 80。如果站点配置 Web 服务器监听不同的端口，则 URL 必须包含端口号。
-   **目录路径：** URL 中引用文件的目录路径。对于 Web 页面，此字段是 HTML 文件的目录路径。目录路径区分大小写。
-   **文件名：** 文件的名称。对于 Web 页面，文件名通常以 `.html` 结尾。如果省略文件名，Web 服务器将返回默认文件（通常名为 `index.html`）。文件名区分大小写。
-   **HTML 锚点：** URL 的可选部分，使 Web 浏览器跳转到文件中的特定位置。如果这部分以问号 (?) 而不是井号 (#) 开头，浏览器将问号后面的文本视为查询。Web 服务器将根据此类查询返回信息。

Web 服务器提供 Web 页面，Web 浏览器下载它们并将其显示给用户。这就是这两个协同工作的软件包使 Web 运行起来的大致故事。

在一个典型的场景中，用户坐在连接到互联网并运行 Web 浏览器的计算机前。当用户点击链接或在 Web 浏览器中输入 URL 时，浏览器连接到 Web 服务器并向服务器请求文档。Web 服务器发送文档（通常以 HTML 格式）并结束连接。Web 浏览器解释并显示带有文本和图形的 HTML 文档。**图 2-3** 说明了这种典型的用户浏览 Web 的场景。

### 356 Fedora Core 中的 Web 浏览

![](img/9f89727199836b0f871f1745838aa8b2_382_0.png)

Web 浏览器与 Web 服务器的连接在服务器发送文档后结束。当用户浏览已下载的文档并点击另一个超文本链接时，Web 浏览器再次连接到超文本链接中命名的 Web 服务器，下载文档，结束连接，并显示新文档。这就是用户可以轻松从一个文档移动到另一个文档的方式。

Web 浏览器可以做的不仅仅是简单地与 Web 服务器进行“HTTP 对话”——事实上，Web 浏览器还可以使用 **FTP** 下载文档，许多浏览器还集成了邮件和新闻阅读器。

## Fedora Core 中的 Web 浏览

Web 浏览很有趣，因为当今许多 Web 页面充满了图形和多媒体。此外还有意外之喜的元素——点击一个链接，最终可能会到达意想不到的 Web 页面。链接是 Web 最奇特（也有用）的方面。您可以从一个显示今天天气的页面开始，点击几次后，您可能正在阅读本周的 *Time* 杂志。

要浏览 Web，您只需要一个 Web 浏览器和一个互联网连接。我假设您已经处理好了互联网连接，因此您只需要了解 Fedora Core 中的 Web 浏览器。

# 检查 Fedora Core 中的 Web 浏览器

Fedora Core 附带 Mozilla Web 浏览器。Mozilla 是 Netscape Communicator 的开源版本，它是 Fedora Core 的主要 Web 浏览器。

Fedora Core 包含其他几个 Web 浏览器。我简要提及了其他浏览器，但在其余讨论中重点介绍 Mozilla。以下是 Fedora Core 附带的主要 Web 浏览器：

-   **Mozilla**：那匹老黄牛——Netscape Communicator——的重生，而且更好。包括邮件和新闻阅读器。该 Web 浏览器被称为 Mozilla Navigator，或简称为 Navigator（正如在 Netscape Communicator 中那样）。
-   **Epiphany**：使用部分 Mozilla 代码来绘制 Web 页面的 GNOME Web 浏览器，但比 Mozilla 有更简单的用户界面。Epiphany 默认不安装，但它位于随本书附带的光盘上。如果您在光盘中找不到 Epiphany，可以从 www.gnome.org/projects/epiphany/ 下载。
-   **Konqueror**：也是文件管理器和通用查看器的 KDE Web 浏览器。

除了这三个，还有许多其他应用程序能够下载和显示 Web 页面。

# 启动 Mozilla

在 GNOME 桌面上，您可以通过两种方式之一启动 Mozilla：

-   点击 GNOME 或 KDE 面板上的 Web 浏览器图标（地球和鼠标）。
-   在 GNOME 中，选择 主菜单 > 互联网 > Mozilla Web Browser。

当 Mozilla 启动时，它显示一个带有默认主页的浏览器窗口（Web 服务器上的主 Web 页面被称为 *主页*）。您可以配置 Mozilla 使用不同的 Web 页面作为默认主页。

# 学习 Mozilla 的用户界面

**图 2-4** 显示了来自美国一个政府 Web 站点（www.gao.gov）的 Web 页面，以及 Mozilla 浏览器窗口的主要元素。

