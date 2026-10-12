

您可以通过查看列出 Web 服务器对 GET 命令响应内容的清单来识别此布局。由于示例使用 telnet 命令获取文档，因此您看到的 HTML 内容是文本行。如果您使用 Web 浏览器（例如 Mozilla）访问同一网站 (www.gao.gov)，您将以图形形式（如**图 2-1** 所示）看到该页面。

HTTP 命令示例展示了 GET 命令的结果。GET 是最常见的 HTTP 命令；它导致服务器返回指定的 HTML 文档。

另外两个 HTTP 命令是 HEAD 和 POST。HEAD 命令几乎类似于 GET：它导致服务器返回文档中除正文外的所有内容。POST 命令向服务器发送信息；如何根据该信息采取行动取决于服务器。

## 探索 Apache Web 服务器

您可能已经知道如何使用 Web，但您可能不知道如何设置 Web 服务器，以便您也能够通过网页向世界提供信息。要成为 Web 上的信息提供者，您必须在互联网上的 Fedora Core 计算机上运行 Web 服务器。您还必须为您的网站准备网页——这项任务可能比设置 Web 服务器更具挑战性。

![](img/9f89727199836b0f871f1745838aa8b2_644_0.png)

- **图 2-1：** 使用 Mozilla Web 浏览器查看的 www.gao.gov 网站。

### 为什么叫 Apache？

根据 `www.apache.org/foundation/faq.html` 上关于 Apache Web 服务器项目的信息，Apache 小组于 1995 年 3 月由许多提供补丁文件的人员组成，这些补丁文件是为了修复 NCSA HTTPD 1.3 中的错误而编写的。将补丁应用于 NCSA HTTPD 后的结果是他们称之为一个*补丁式*的服务器（这就是 Apache 名称的由来）。Apache 小组现已演变为 Apache 软件基金会（ASF），这是一家于 1999 年 6 月在美国特拉华州注册的非营利公司。ASF 还有其他一些正在进行的项目。您可以在 `www.apache.org` 上阅读有关这些项目的信息。特别是，请访问 `httpd.apache.org` 以获取更多关于 Apache Web 服务器项目的信息。

根据 2004 年 4 月 `news.netcraft.com/archives/web_server_survey.html` 上的 Netcraft Web 服务器调查，Apache Web 服务器是最受欢迎的——在报告的 49,750,568 个站点中，有 66.99% 使用 Apache 服务器。微软 Internet 信息服务器（IIS）远远落后于 Apache，占站点的 21.49%。

在可用的 Web 服务器中，Apache Web 服务器是最受欢迎的，并且随 Fedora Core 一起提供。Apache Web 服务器最初是 NCSA HTTPD 服务器的改进版本，但很快发展为独立的开发工作。与 NCSA HTTPD 一样，Apache 服务器由合作团队开发和维护。Apache 可通过互联网免费获得。

### 安装 Apache Web 服务器

根据 Fedora Core 安装选项，Apache Web 服务器可能已经安装在您的系统中。要了解它是否已安装，请输入以下命令：

```bash
rpm -q httpd
```

如果 Web 服务器已安装，您会看到如下的输出：

```bash
httpd-2.0.48-16.1
```

如果您收到消息称 `httpd` 未安装，您可以轻松使用本书的配套 DVD-ROM 通过以下步骤进行安装：

1. **以 root 身份登录并将 DVD-ROM 插入 DVD 驱动器。**
   - 如果您在 GNOME 或 KDE 图形桌面环境中，DVD 会自动挂载。如果没有，请输入命令 `mount /dev/cdrom` 来挂载 DVD-ROM。
2. **输入以下命令安装 Apache Web 服务器：**

```bash
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh httpd*
```

就这么简单！现在您可以运行 Apache Web 服务器了。

### 启动 Apache Web 服务器

即使 Apache Web 服务器已安装，它也可能未设置为在启动时运行。如果您想尝试使用它，必须启动服务器。为此，请以 `root` 身份登录并输入以下命令：

```bash
service httpd start
```

要查看 `httpd` 进程（`httpd` 是 Apache Web 服务器程序的名称）是否正在运行，请输入以下命令：

```bash
ps ax | grep httpd
```

输出显示许多 `httpd` 进程。运行多个 Web 服务器进程——一个父进程和多个子进程——是一种常见方法，以便通过为每个 `httpd` 进程分配每个请求来高效处理多个 HTTP 请求。

如果找不到 `httpd` 进程，Apache 配置文件中可能存在错误。如果是这种情况，会出现一些错误消息，并为您提供有关错误原因的线索。您必须修复配置文件中的问题并重新启动服务器。

如果 `httpd` 进程正在运行，您可以使用 TELNET 程序查看它是否正常工作，但首先您必须在 `/var/www/html` 目录中添加一个默认主页。如果您没有时间准备一个，请复制在出错情况下应发送的网页。这是您在（以 `root` 身份登录时）输入的命令，用于获取它：

```bash
cp /var/www/error/noindex.html /var/www/html/index.html
```

现在您有了一个默认主页，并且可以在终端窗口中输入以下命令来检查 Web 服务器是否正常工作：

```bash
telnet localhost 80
```

收到 Connected 消息后，输入：

```bash
HEAD / HTTP/1.0
```

然后按两次 Enter。您会得到一个类似于以下的响应（当然，日期和数字不同）：

```bash
HTTP/1.1 200 OK
Date: Sat, 13 Mar 2004 21:51:18 GMT
Server: Apache/2.0.48 (Fedora)
Last-Modified: Sat, 13 Mar 2004 21:51:08 GMT
ETag: "8c246-f30-3eec2c00"
Accept-Ranges: bytes
Content-Length: 3888
Connection: close
Content-Type: text/html; charset=UTF-8

Connection closed by foreign host.
```

响应显示了有关 Web 服务器和默认主页的一些信息。您还可以使用运行在您的 Fedora Core 系统上的 Web 浏览器（如 Mozilla）来检查 Web 服务器。使用 URL `http://localhost/` 并查看会发生什么。您会看到一个标题为“Fedora Core 上 Apache HTTP 服务器的测试页面”的网页。

![](img/9f89727199836b0f871f1745838aa8b2_647_0.png)

如果您希望在启动时自动启动 Apache Web 服务器，请输入以下命令进行设置：

```bash
chkconfig --levels 35 httpd on
```

## 配置 Apache Web 服务器

默认情况下，Apache Web 服务器软件配置为使用以下文件和目录：

- Web 服务器程序 — *httpd* — 安装在 `/usr/sbin` 目录中。
- Apache Web 服务器配置文件 — *httpd.conf* — 位于 `/etc/httpd/conf` 目录中。配置文件是一个包含指令的文本文件，这些指令指定 Web 服务器的各个方面。`/etc/httpd/conf` 目录还包含关于安全套接字层（SSL）实现需求的信息。（SSL 实现作为 Apache Web 服务器的一部分提供。）
- Apache Web 服务器设置为从 `/var/www/html` 目录提供 HTML 文档。因此，请将您的网页放在此目录中。
- 如果您有任何通用网关接口（CGI）程序——Web 服务器可以调用来访问其他文件和数据库的程序——请将这些放在 `/var/www/cgi-bin/` 目录中。
- `/var/log/httpd` 目录用于 Web 服务器日志文件（访问日志和错误日志）。
- `/etc/init.d/httpd` 脚本在您的 Fedora Core 系统启动时启动 `httpd` 进程，前提是您使用 `chkconfig` 命令启用了它。

### 使用 Apache 配置工具

Fedora Core 附带了一个图形配置工具，您可以使用它来配置 Apache Web 服务器。要运行此配置工具，请以 `root` 身份登录，并从 GNOME 桌面中选择 **主菜单** → **系统设置** → **服务器设置** → **HTTP**。将显示 Apache 配置窗口（如**图 2-2** 所示）。

![](img/9f89727199836b0f871f1745838aa8b2_648_0.png)

Apache 配置窗口组织为四个选项卡。您可以从每个选项卡中设置各种选项：

- **主：** 从这个选项卡，您可以指定 Apache 期望接收 Web 服务请求的 IP 地址和端口号。您还可以设置 Web 管理员的电子邮件地址。
- **虚拟主机：** 在此处您可以设置虚拟主机。我将在本章后面讨论虚拟主机的选项。您还可以编辑适用于所有虚拟主机的默认设置。单击虚拟主机选项卡上的“编辑默认设置”按钮会弹出另一个窗口（如**图 2-3** 所示），您可以从中设置许多不同的选项。
- **服务器：** 此选项卡包含服务器的设置，例如 HTTP 服务器运行的用户和组名称以及存储进程 ID 的文件位置。

