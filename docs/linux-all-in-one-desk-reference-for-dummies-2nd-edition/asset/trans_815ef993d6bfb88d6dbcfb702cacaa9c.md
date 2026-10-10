
## HTTP 是互联网标准吗？

尽管自 1990 年以来 HTTP 在 Web 中得到了广泛使用，但直到最近它才成为互联网标准。所有互联网标准首先都以注释请求（RFC, Request for Comment）的形式分发。第一份与 HTTP 相关的 RFC 是 RFC 1945，“超文本传输协议 — HTTP/1.0”（T. Berners-Lee、R. Fielding 和 H. Frystyk，1996 年 5 月）。然而，RFC 1945 被视为信息性文档，而非标准。

RFC 2616，“超文本传输协议 — HTTP/1.1”（R. Fielding、J. Gettys、J. Mogul、H. Frystyk、L. Masinter、P. Leach、T. Berners-Lee，1999 年 6 月）是 HTTP 的草案互联网标准。

要阅读这些 RFC，请将你的 Web 浏览器指向 `www.ietf.org/rfc/` 或 `www.faqs.org/rfcs`。

要了解有关 HTTP/1.1 和其他与 Web 相关的标准的更多信息，请使用 Web 浏览器访问 `www.w3.org/protocols`。

要查看 HTTP 工作示例，请遵循以下步骤：

- **1. 确保你的 Linux 电脑连接到互联网的连接处于活动状态。**
  - 例如，如果你使用 PPP，请确保已建立连接。如果你拥有宽带电缆或 DSL 连接，你的连接很可能是始终开启的。
- **2. 输入以下命令。（我使用一个美国政府网站 URL 来说明 HTTP 协议的工作原理。）**
  ```
  telnet www.gao.gov 80
  ```
- **3. 当你看到“已连接...”消息后，输入以下 HTTP 命令并按两次 Enter 键：**
  ```
  GET / HTTP/1.0
  ```
  - 作为对此 HTTP 命令的响应，Web 服务器返回一些有用信息，随后是默认 HTML 文件（通常称为 `index.html`）的内容。

以下是在我对美国政府网站执行 GET 命令时所得到的结果。（在下文中，我标出了你需要输入 GET 命令的位置。）

```text
Trying 161.203.16.2...
Connected to www.gao.gov.
Escape character is '^]'.
GET / HTTP/1.0    (输入此行并按两次 Enter 键)
```

```text
HTTP/1.1 200 OK
Date: Wed, 14 Dec 2005 22:53:26 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1
```

```html
<html>
<head>
<title>The Government Accountability Office</title>
... (删除的行) ...
</head>
<body>
...
(删除的行)
...
</body>
</html>
```

连接被远程主机关闭。

当你使用 TELNET 尝试这个示例时，你会看到 Web 服务器确切发送回给 Web 浏览器的内容。前几行是为浏览器提供的管理信息。服务器返回这些信息：

- 一行显示服务器使用的 HTTP 协议版本为 1.1，状态码为 200 表示成功：
  ```
  HTTP/1.1 200 OK
  ```
- 当前日期和时间。日期和时间字符串示例如下：
  ```
  Date: Wed, 14 Dec 2005 22:53:26 GMT
  ```
- Web 服务器软件的名称、版本及其他详细信息。如今，常见的做法是仅显示软件的通用名称（例如 `Apache`），而不提供其他详细信息，因为某人可能会利用版本信息来攻击该版本的特定漏洞。
- Web 服务器返回的文档类型。对于 HTML 文档，内容类型报告如下：
  ```
  Content-Type: text/html; charset=ISO-8859-1
  ```

文档本身位于管理信息之后。HTML 文档具有以下一般布局：

```html
<html>
<head>
<title>文档标题在此处</title>
</head>
<body 属性在此处 >
... 文档其余部分在此处
</body>
</html>
```

你可以通过查看显示 Web 服务器响应 GET 命令内容的列表来识别此布局。由于示例使用 telnet 命令获取文档，因此你会以文本行的形式看到 HTML 内容。如果你使用 Web 浏览器（如 Mozilla Firefox）访问同一个网站（www.gao.gov），你会看到如图 2-1 所示的页面图形形式。

HTTP 命令示例展示了 GET 命令的结果。GET 是最常用的 HTTP 命令；它使服务器返回指定的 HTML 文档或图像。

另外两个 HTTP 命令是 HEAD 和 POST。HEAD 命令几乎与 GET 相同：它使服务器返回文档中除正文以外的所有内容。POST 命令向服务器发送信息；如何操作这些信息由服务器决定。

![](img/792720823146d68f19fd50c99ebfce4b_611_0.png)

**图 2-1：** 通过 Web 浏览器查看的 www.gao.gov 网站。

## 探索 Apache Web 服务器

你可能已经知道如何使用 Web，但你可能不知道如何设置 Web 服务器，以便你也能够通过网页向全世界提供信息。要成为 Web 上的信息提供者，你需要在互联网上的 Linux 电脑上运行一个 Web 服务器。你还必须为你网站准备网页——这可能比设置 Web 服务器更具挑战性。

在可用的 Web 服务器中，Apache Web 服务器是最流行的，并且适用于所有 Linux 发行版。Apache Web 服务器最初是 NCSA HTTPD 服务器的改进版本，但很快发展成为独立开发项目。与 NCSA HTTPD 一样，Apache 服务器由协作团队开发和维护。Apache 可通过互联网免费获取。

### 安装 Apache Web 服务器

根据你在安装 Linux 发行版时所做的选择，Apache Web 服务器可能已安装在你的系统中。如果已安装，它可能已在运行，或者你需要启动它。例如，Apache Web 服务器在 Knoppix 和 Xandros 中已安装，但默认情况下未开启。

![](img/792720823146d68f19fd50c99ebfce4b_612_0.png)

Apache Web 服务器的软件包名称在不同发行版中有所不同——Fedora Core 称其为 `httpd`，而 Knoppix 和 Xandros 称其为 `apache`。Debian 和 SUSE 称该软件包为 `apache2`。要查看 Apache Web 服务器是否已安装，在 Debian、Knoppix、MEPS 和 Xandros 中键入 `dpkg -l apache*`，在 Ubuntu 中键入 `sudo dpkg -l apache*`。如果在显示以 `apache` 开头的软件包名称的输出第一列中看到 `ii` 或 `pn`，则说明它已完全或部分安装。在 Fedora Core 中，键入 `rpm -q httpd`。在 SUSE 中，键入 `rpm -q apache2`。

![](img/792720823146d68f19fd50c99ebfce4b_612_1.png)

如果 Web 服务器未安装，你可以轻松安装它。步骤取决于你的 Linux 发行版。在 Debian 和 MEPIS 中，以 `root` 身份登录并键入 `apt-get install apache2`，在 Ubuntu 中键入 `sudo apt-get install apache2`。在 Fedora Core 中，挂载随附 DVD 并通过键入以下命令安装 Apache Web 服务器：

```bash
cd /media/cdrom/Fedora/RPMS
rpm -ivh httpd*
```

### 为什么叫 Apache？

根据 **www.apache.org/foundation/faq.html** 上关于 Apache Web 服务器项目的信息，Apache 小组于 1995 年 3 月由一些提供补丁文件的人成立，这些补丁文件旨在修复 NCSA HTTPD 1.3 中的错误。将补丁应用于 NCSA HTTPD 后的结果就是他们所称的*补丁服务器*（Apache 名称的由来）。Apache 小组现在已演变为 Apache 软件基金会（ASF），这是一个于 1999 年 6 月在美国特拉华州注册的非营利公司。ASF 还有其他正在进行的项目。你可以在 **www.apache.org** 上阅读关于这些项目的介绍。特别是，请访问 **http://httpd.apache.org** 以获取更多关于 Apache Web 服务器项目的信息。

根据 **2005 年 8 月 Netcraft Web 服务器调查**（位于 **http://news.netcraft.com/archives/web_server_survey.html**），Apache Web 服务器是其中最受欢迎的 Web 服务器——**70,392,567** 个网站中 **69.46%** 的网站报告使用 Apache 服务器。**微软 Internet 信息服务（IIS）** 位居第二，占有 **20.43%** 的网站份额。

![](img/792720823146d68f19fd50c99ebfce4b_613_0.png)

在 SUSE 中，从 **YaST 控制中心** 中的 **软件** 类别点击 **安装和移除软件**——**主菜单：系统：控制中心（YaST）**——然后使用 YaST 的搜索功能查找 **apache**。找到想要的软件包后，选中它们并点击 **接受** 进行安装。

就这么简单！安装好 Apache Web 服务器后，你就可以运行它了。

### 启动 Apache Web 服务器

即使 Apache Web 服务器已安装，它也可能未设置开机自动启动。如果你想尝试使用它，你必须启动服务器。

![](img/792720823146d68f19fd50c99ebfce4b_613_1.png)

要启动 Apache Web 服务器，以 **root** 身份登录并键入 `/etc/init.d/apache2 start`。在 Debian、MEPIS、Ubuntu 和 SUSE 中，在 Fedora Core 中键入 **service httpd start**。在 Knoppix 和 Xandros 中，键入 `/etc/init.d/apache2 start`。如果你希望在启动时自动启动 Apache Web 服务器，在 Debian、MEPIS 和 Ubuntu 中键入 **update-rc.d apache2 defaults**。在 Knoppix 和 Xandros 中，键入 **update-rc.d apache2 defaults**。在 Fedora Core 中，键入 **chkconfig -levels 35 httpd on**。在 SUSE 中，键入 **chkconfig -levels 35 apache2 on**。

要查看服务器是否正在运行，键入 `ps ax | grep processname`，其中 **processname** 在 Fedora Core 和 SUSE 中为 **httpd**，在 Debian、Knoppix 和 Xandros 中为 **apache**。如果在输出中看到多个 Web 服务器进程，则一切正常。运行多个 Web 服务器进程——一个父进程和多个子进程——是一种常见方法，以便通过为每个请求分配一个 Web 服务器进程来高效地处理多个 HTTP 请求。

