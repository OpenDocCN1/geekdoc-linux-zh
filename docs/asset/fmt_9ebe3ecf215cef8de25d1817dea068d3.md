
如果 Web 服务器未安装，你可以轻松安装它。步骤取决于你的 Linux 发行版。在 Debian 和 MEPIS 中，以 `root` 身份登录并键入 `apt-get install apache2`，在 Ubuntu 中键入 `sudo apt-get install apache2`。在 Fedora Core 中，挂载随附 DVD 并通过键入以下命令安装 Apache Web 服务器：

```bash
cd /media/cdrom/Fedora/RPMS
rpm -ivh httpd*
```

### 为什么叫 Apache？

根据 `www.apache.org/foundation/faq.html` 上关于 Apache Web 服务器项目的信息，Apache 小组于 1995 年 3 月由一些提供补丁文件的人成立，这些补丁文件旨在修复 NCSA HTTPD 1.3 中的错误。将补丁应用于 NCSA HTTPD 后的结果就是他们所称的*补丁服务器*（Apache 名称的由来）。Apache 小组现在已演变为 Apache 软件基金会（ASF），这是一个于 1999 年 6 月在美国特拉华州注册的非营利公司。ASF 还有其他正在进行的项目。你可以在 `www.apache.org` 上阅读关于这些项目的介绍。特别是，请访问 `http://httpd.apache.org` 以获取更多关于 Apache Web 服务器项目的信息。

根据 `2005 年 8 月 Netcraft Web 服务器调查`（位于 `http://news.netcraft.com/archives/web_server_survey.html`），Apache Web 服务器是其中最受欢迎的 Web 服务器——`70,392,567` 个网站中 `69.46%` 的网站报告使用 Apache 服务器。`微软 Internet 信息服务（IIS）` 位居第二，占有 `20.43%` 的网站份额。

![](img/792720823146d68f19fd50c99ebfce4b_613_0.png)

在 SUSE 中，从 `YaST 控制中心` 中的 `软件` 类别点击 `安装和移除软件`——`主菜单：系统：控制中心（YaST）`——然后使用 YaST 的搜索功能查找 `apache`。找到想要的软件包后，选中它们并点击 `接受` 进行安装。

就这么简单！安装好 Apache Web 服务器后，你就可以运行它了。

### 启动 Apache Web 服务器

即使 Apache Web 服务器已安装，它也可能未设置开机自动启动。如果你想尝试使用它，你必须启动服务器。

![](img/792720823146d68f19fd50c99ebfce4b_613_1.png)

要启动 Apache Web 服务器，以 `root` 身份登录并键入 `/etc/init.d/apache2 start`。在 Debian、MEPIS、Ubuntu 和 SUSE 中，在 Fedora Core 中键入 `service httpd start`。在 Knoppix 和 Xandros 中，键入 `/etc/init.d/apache2 start`。如果你希望在启动时自动启动 Apache Web 服务器，在 Debian、MEPIS 和 Ubuntu 中键入 `update-rc.d apache2 defaults`。在 Knoppix 和 Xandros 中，键入 `update-rc.d apache2 defaults`。在 Fedora Core 中，键入 `chkconfig -levels 35 httpd on`。在 SUSE 中，键入 `chkconfig -levels 35 apache2 on`。

要查看服务器是否正在运行，键入 `ps ax | grep processname`，其中 `processname` 在 Fedora Core 和 SUSE 中为 `httpd`，在 Debian、Knoppix 和 Xandros 中为 `apache`。如果在输出中看到多个 Web 服务器进程，则一切正常。运行多个 Web 服务器进程——一个父进程和多个子进程——是一种常见方法，以便通过为每个请求分配一个 Web 服务器进程来高效地处理多个 HTTP 请求。

如果 `ps ax` 的输出未显示任何 Web 服务器进程，则错误可能隐藏在 Apache 配置文件中。若情况如此，你必须修复配置文件中的任何问题，并重新启动服务器。

如果 Web 服务器正在运行，你可以使用 TELNET 程序连接到 80 端口，查看服务器是否正常工作。开始在终端窗口中输入以下命令：

```
telnet localhost 80
```

当收到 `Connected` 消息后，输入：

```
HEAD / HTTP/1.0
```

然后按两次 Enter。你会得到一个类似的响应，当然日期和数字会有所不同：

```
HTTP/1.1 200 OK
Date: Sat, 17 Dec 2005 20:57:20 GMT
Server: Apache/2.0.54 (Fedora)
Last-Modified: Sat, 17 Dec 2005 20:57:05 GMT
ETag: "156946-25b-8f6d64a0"
Accept-Ranges: bytes
Content-Length: 603
Connection: close
Content-Type: text/html; charset=UTF-8

Connection closed by foreign host.
```

该响应显示了一些关于 Web 服务器和默认主页的信息。你还可以通过在 Linux 系统上运行 Web 浏览器（例如 Firefox）来检查 Web 服务器。使用 URL `http://localhost/` 并查看发生的情况。

![](img/792720823146d68f19fd50c99ebfce4b_614_0.png)

如果在 Web 浏览器中尝试 `http://localhost/` URL 时收到错误消息，这意味着由 `DocumentRoot` 配置指令指定的目录中没有 `index.html` 文件（默认 Web 页面）。要修正此问题，只需在适当的目录（查看 HTTP 服务器配置文件中由 `DocumentRoot` 指定的目录名称）中创建一个名为 `index.html` 的简单 HTML 文档。我将在下一节中解释诸如 `DocumentRoot` 这样的配置指令。

## 配置 Apache Web 服务器

Apache Web 服务器程序文件和配置文件在不同的发行版中存储在不同的位置。Apache Web 服务器配置文件在 Fedora Core、Knoppix、SUSE 和 Xandros 中名为 `httpd.conf`，而在 Debian、MEPIS 和 Ubuntu 中名为 `apache2.conf`。配置文件是一个文本文件，其中包含指定 Web 服务器各个方面的指令。

![](img/792720823146d68f19fd50c99ebfce4b_615_0.png)

在 Debian、MEPIS、SUSE 和 Ubuntu 中，配置文件位于 `/etc/apache2` 目录。在 Fedora Core 中，`httpd.conf` 文件位于 `/etc/httpd/conf` 目录。在 Knoppix 和 Xandros 中，文件位于 `/etc/apache` 目录。

包含 `httpd.conf` 文件的目录还包含有关安全套接字层（SSL）实现需求的信息。（SSL 实现作为 Apache Web 服务器的一部分提供。）

### 使用 Apache 配置工具

在某些 Linux 发行版中，你可以使用图形用户界面工具来配置 Apache Web 服务器。特别是，Fedora Core 和 SUSE 附带了用于配置 Apache Web 服务器的 GUI 工具。我将在本节中向你介绍这些 GUI 工具。

![](img/792720823146d68f19fd50c99ebfce4b_615_1.png)

在 Fedora Core 中，以 `root` 身份登录，并从 GUI 桌面选择“系统管理”>“服务器设置”>“HTTP”。将出现 HTTP 对话框，如图 2-2 所示。

![](img/792720823146d68f19fd50c99ebfce4b_615_2.png)

图 2-2：在 Fedora Core 中，从此对话框配置 Apache HTTP 服务器。

Apache 配置对话框分为四个选项卡。你可以从这些选项卡中的每一个设置各种选项：

- 主选项卡（Main）：从此选项卡中，你可以指定 Apache 期望接收 Web 服务请求的 IP 地址和端口号。你还可以设置 Webmaster 的电子邮件地址。
