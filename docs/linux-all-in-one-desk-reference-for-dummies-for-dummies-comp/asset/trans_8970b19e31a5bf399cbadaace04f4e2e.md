
## HTTP 是互联网标准吗？

尽管 HTTP 自 1990 年以来在 Web 中广泛使用，但直到最近它才成为互联网标准。所有互联网标准最初都以请求意见稿（Request for Comment，简称 RFC）的形式分发。第一个与 HTTP 相关的 RFC 是 RFC 1945《超文本传输协议 — HTTP/1.0》（T. Berners-Lee, R. Fielding, and H. Frystyk，1996 年 5 月）。然而，RFC 1945 被视为信息性文档，而非标准。

RFC 2616《超文本传输协议 — HTTP/1.1》（R. Fielding, J. Gettys, J. Mogul, H. Frystyk, L. Masinter, P. Leach, T. Berners-Lee，1999 年 6 月）是 HTTP 的草案互联网标准。

要阅读这些 RFC，请将您的 Web 浏览器指向 www.ietf.org/rfc/ 或 www.faqs.org/rfcs。

要了解有关 HTTP/1.1 及其他与 Web 相关的标准的更多信息，请使用 Web 浏览器访问 www.w3.org/Protocols。

要查看 HTTP 实际工作的示例，请按照以下步骤操作：

1. 确保您的 Linux 计算机与互联网的连接正常运作。
   - 例如，如果您使用 PPP，请确保已建立连接。如果您拥有宽带电缆或 DSL 连接，您的连接很可能始终处于开启状态。
2. 输入以下命令。（我使用美国政府网站 URL 来说明 HTTP 协议的工作原理。）
   - `telnet www.gao.gov 80`
3. 看到 `Connected...` 消息后，输入以下 HTTP 命令并按两次 Enter：
   - `GET / HTTP/1.0`

作为对该 HTTP 命令的响应，Web 服务器返回一些有用信息，随后是默认 HTML 文件的内容（通常称为 `index.html`）。

以下是我在美国政府网站尝试 GET 命令时得到的结果。（在下文中，我展示了你需要输入 GET 命令的位置。）

```
Trying 161.203.16.2...
Connected to www.gao.gov.
Escape character is '^}'.
GET / HTTP/1.0    (输入此行然后按两次 Enter)

HTTP/1.1 200 OK
Date: Wed, 14 Dec 2005 22:53:26 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1

<html>
<head>
<title>The Government Accountability Office</title>
... (省略行) ...
</head>
<body>

... (省略行) ...

</body>
</html>

Connection closed by foreign host.
```

当您尝试这个 TELNET 示例时，您将看到 Web 服务器发送给 Web 浏览器的确切内容。前几行是供浏览器使用的管理信息。服务器返回此信息：

- 一行显示服务器使用 HTTP 协议版本 1.1 以及表示成功的状态码 200：
  ```
  HTTP/1.1 200 OK
  ```
- 当前日期和时间。一个日期和时间字符串的示例如下：
  ```
  Date: Wed, 14 Dec 2005 22:53:26 GMT
  ```
- Web 服务器软件的名称、版本及其他详细信息。如今，常见的做法是仅显示软件的通用名称（例如 *Apache*），而不提供任何其他详细信息，因为有人可能会利用版本信息来攻击该版本的特定漏洞。
- Web 服务器返回的文档类型。对于 HTML 文档，内容类型报告如下：
  ```
  Content-Type: text/html; charset=ISO-8859-1
  ```

文档本身跟随在管理信息之后。HTML 文档具有以下通用布局：

```
<html>
<head>
<title>文档标题在此处</title>
</head>
<body 可选属性在此处>
.... 文档其余部分在此处
</body>
</html>
```

通过查看显示 Web 服务器响应 **GET** 命令所返回内容的列表，您可以识别出此布局。由于示例使用 **telnet** 命令获取文档，您会看到 HTML 内容以文本行的形式显示。如果您使用 Web 浏览器（如 Mozilla Firefox）访问同一网站（**www.gao.gov**），您将以图形形式看到该页面，如 **图 2-1** 所示。

HTTP 命令的示例展示了 **GET** 命令的结果。**GET** 是最常见的 HTTP 命令；它使服务器返回指定的 HTML 文档或图像。

另外两个 HTTP 命令是 **HEAD** 和 **POST**。**HEAD** 命令几乎像 **GET**：它使服务器返回文档中除主体外的所有内容。**POST** 命令向服务器发送信息；至于如何处理这些信息，由服务器自行决定。

![](img/11709a8f88c8cd03868a929dc94c0e2b_611_0.png)

## 探索 Apache Web 服务器

您可能已经知道如何使用 Web，但您可能不知道如何设置 Web 服务器，以便您也能通过 Web 页面向世界提供信息。要在 Web 上成为信息提供商，您必须在位于互联网上的 Linux 计算机上运行 Web 服务器。您还必须为您的网站准备 Web 页面——这项任务可能比设置 Web 服务器更具挑战性。

在可用的 Web 服务器中，Apache Web 服务器是最受欢迎的，并且适用于所有 Linux 发行版。Apache Web 服务器最初是 NCSA HTTPD 服务器的改进版本，但很快发展为一个独立的项目。与 NCSA HTTPD 一样，Apache 服务器由一个合作团队开发和维护。Apache 在网络上免费提供。

### 安装 Apache Web 服务器

根据您在安装 Linux 发行版时所做的选择，Apache Web 服务器可能已安装在您的系统中。如果已安装，它可能已在运行，或者您可能需要启动它。例如，Apache Web 服务器安装在 Knoppix 和 Xandros 中，但默认情况下并未开启。

![](img/11709a8f88c8cd03868a929dc94c0e2b_612_0.png)

Apache Web 服务器软件包名称因发行版而异——Fedora Core 称之为 `httpd`，而 Knoppix 和 Xandros 称之为 `apache`。Debian 和 SUSE 将软件包称为 `apache2`。要检查 Apache Web 服务器是否已安装，在 Debian、Knoppix、MEPIS 和 Xandros 中输入 `dpkg -l apache*`，在 Ubuntu 中输入 `sudo dpkg -l apache*`。如果在输出第一列中看到以 `apache` 开头的软件包名称前有 `ii` 或 `pn`，则表示它已完全或部分安装。在 Fedora Core 中，输入 `rpm -q httpd`。在 SUSE 中，输入 `rpm -q apache2`。

![](img/11709a8f88c8cd03868a929dc94c0e2b_612_1.png)

如果 Web 服务器未安装，您可以轻松安装。步骤取决于您的 Linux 发行版。在 Debian 和 MEPIS 中，以 `root` 身份登录并输入 `apt-get install apache2`，在 Ubuntu 中输入 `sudo apt-get install apache2`。在 Fedora Core 中，挂载伴随 DVD，并通过输入以下命令安装 Apache Web 服务器：

```bash
cd /media/cdrom/Fedora/RPMS
rpm -ivh httpd*
```

### 为什么叫 Apache？

根据 www.apache.org/foundation/faq.html 上关于 Apache Web 服务器项目的信息，Apache 小组于 1995 年 3 月由一批提供补丁文件的人员组成，这些补丁文件旨在修复 NCSA HTTPD 1.3 中的 bug。将补丁应用到 NCSA HTTPD 后的结果是他们所谓的“补丁式”服务器（这就是 Apache 名称的由来）。Apache 小组现已演变为 Apache 软件基金会（ASF），这是一家于 1999 年 6 月在美国特拉华州注册的非营利公司。ASF 拥有其他多个正在进行的项目。您可以访问 www.apache.org 阅读有关这些项目的信息。特别是，请访问 http://httpd.apache.org 以获取更多关于 Apache Web 服务器项目的信息。

根据 2005 年 8 月 Netcraft Web 服务器调查 http://news.netcraft.com/archives/web_server_survey.html，Apache Web 服务器是市面上最流行的 Web 服务器——报告的 70,392,567 个站点中，69.46% 使用了 Apache 服务器。微软 Internet Information Services (IIS) 位居第二，份额为 20.43%。

![](img/11709a8f88c8cd03868a929dc94c0e2b_613_0.png)

在 SUSE 中，从 YaST 控制中心中的 Software 类别点击“安装和移除软件”——主菜单 → 系统 → 控制中心 (YaST)——然后使用 YaST 的搜索功能查找 Apache。找到您想要安装的软件包后，选中它们并点击“接受”以进行安装。

就是这样！安装好 Apache Web 服务器后，您就可以运行它了。

### 启动 Apache Web 服务器

即使安装了 Apache Web 服务器，它也可能未设置为在启动时自动运行。如果您想尝试使用它，必须手动启动服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_613_1.png)

要启动 Apache Web 服务器，请以 root 身份登录并输入 `/etc/init.d/apache2 start`。在 Debian、MEPIS、Ubuntu 和 SUSE 中，输入 `service httpd start` 于 Fedora Core。在 Knoppix 和 Xandros 中，输入 `/etc/init.d/apache2 start`。如果您希望服务器在启动时自动启动 Apache Web 服务器，请在 Debian、MEPIS 和 Ubuntu 中输入 `update-rc.d apache2 defaults`。在 Knoppix 和 Xandros 中，输入 `update-rc.d apache2 defaults`。在 Fedora Core 中，输入 `chkconfig -levels 35 httpd on`。在 SUSE 中，输入 `chkconfig -levels 35 apache2 on`。

要查看服务器是否正在运行，请输入 `ps ax | grep processname`，其中 `processname` 在 Fedora Core 和 SUSE 中是 `httpd`，在 Debian、Knoppix 和 Xandros 中是 `apache`。如果在输出中看到多个 Web 服务器进程，则一切正常。运行多个 Web 服务器进程——一个父进程和若干子进程——是一种常见做法，以便通过为每个请求分配一个 Web 服务器进程来高效处理多个 HTTP 请求。
