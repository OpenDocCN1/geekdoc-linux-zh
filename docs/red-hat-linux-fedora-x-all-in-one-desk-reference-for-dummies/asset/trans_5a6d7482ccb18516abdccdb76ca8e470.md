

# 618 探索 Apache Web 服务器

你可以通过查看显示 Web 服务器对 GET 命令响应返回内容的列表来识别此布局。由于示例使用了 telnet 命令来获取文档，因此你看到的 HTML 内容是以文本行的形式。如果你使用 Web 浏览器（如 Mozilla）访问网站（www.gao.gov），你将看到图形化形式的页面（如图 2-1 所示）。

HTTP 命令示例显示了 GET 命令的结果，GET 是常用的 HTTP 命令；它导致服务器返回指定的 HTML 文档。

另外两个 HTTP 命令是 HEAD 和 POST。HEAD 命令几乎与 GET 相似：它导致服务器返回文档中正文（body）以外的所有内容。POST 命令向服务器发送信息；至于如何处理这些信息，则由服务器来决定。

# 探索 Apache Web 服务器

你可能已经知道如何使用 Web，但可能不知道如何设置 Web 服务器或如何通过 Web 页面向世界提供信息。要成为 Web 上的信息提供者，你必须在互联网上的 Fedora PC 上运行 Web 服务器。你必须为你的网站准备 Web 页面——这项任务可能比设置 Web 服务器更具挑战性。

![](img/d9230b719dc0efd80851f363d8c6f571_644_0.png)

图 2-1：使用 Mozilla 浏览器查看的 www.gao.gov 网站。

美国政府问责办公室是美国国会的立法、审计和调查机构。其使命是为国会提供信息，以提高政府运营效率和效果。GAO 对联邦计划、政策和决策进行审计、评估和调查，以独立提高政府计划和服务的效率。GAO 旨在审查与国会相关的问题，并确保联邦资金支出对民众负责。

# 探索 Apache Web 服务器

## 为什么叫 Apache？

根据 www.apache.org/foundation/faq.html 上关于 Apache Web 服务器项目的信息，Apache 组由若干人员于 1995 年 3 月组建，他们提供了用于修复 NCSA HTTP 1.3 漏洞的补丁文件（patch files）。将补丁应用到 NCSA HTTP 后的结果被他们称为一个“patchy server”（补丁服务器，这就是 Apache 名称的由来）。Apache 组现在已演变为 Apache 软件基金会（The Apache Software Foundation），该基金会于 1999 年 6 月在美国特拉华州注册。ASF 还有许多其他正在进行的项目。你可以在 www.apache.org 阅读这些项目的信息。特别是访问 httpd.apache.org 获取更多有关 Apache 服务器项目的信息。

根据 news.netcraft.com/archives/web_server_survey.html 2004 年 4 月的 Netcraft Web 服务器调查，Apache 服务器是最受欢迎的——在 49,750,568 个使用 Apache 服务器的站点中占了 66.99%。微软互联网信息服务器 (IIS) 是一个遥远的亲戚，占比 21.49%。

在所有可用的 Web 服务器中，Apache Web 服务器最受欢迎，并随 Fedora Core 一起提供。Apache 服务器最初是 NCSA HTTP 服务器的改进版本，很快变成了一项独立的开发工作。与 NCSA HTTP 一样，Apache 服务器由一个协作团队开发和维护。Apache 在互联网上免费提供。

## 安装 Apache Web 服务器

根据 Fedora Core 的选项，系统中可能已经安装了 Apache 服务器。要检查它是否已安装，请输入以下命令：

```
rpm -q httpd
```

如果已安装 Web 服务器，你会看到类似这样的输出：

```
httpd-2.0.48-16.1
```

如果你收到 httpd 未安装的消息，可以按照以下步骤从本书的附带 DVD-ROM 中轻松安装它：

- 1. 以 root 身份登录并将 DVD-ROM 插入 DVD 驱动器。

如果你处于 GNOME 或 KDE 图形桌面中，DVD 会自动挂载。如果没有，请输入命令 `mount /dev/cdrom` 来挂载 DVD-ROM。

2. 输入以下命令安装 Apache Web 服务器：
```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh httpd*
```

搞定！你现在可以运行 Apache Web 服务器了。

# 启动 Apache 服务器

即使安装了 Web 服务器，它可能还没有被设置为开机自启动。如果你想尝试一下，必须启动服务器。为此，请以 root 身份输入以下命令：

```
service httpd start
```

要查看 httpd 进程（httpd 是 Apache Web 服务器程序的名称）正在运行，请输入以下命令：

```
ps ax | grep httpd
```

输出显示了多个 httpd 进程。运行多个 Web 进程——一个父进程和多个子进程——是处理多个 HTTP 请求的常用方法，通过将每个请求分配给一个 httpd 进程可以高效处理请求。

如果你找不到 httpd 进程，错误可能隐藏在 Apache 配置文件中。如果是这种情况，会出现一些错误消息并提供错误原因的提示。你必须在配置文件中修复问题并重新启动服务器。

如果 httpd 进程正在运行，你可以使用 TELNET 命令检查它是否有效，但你必须先在 `/var/www/html` 目录下添加一个默认主页。如果你没有时间准备，可以复制本要发送的 Web 页面。以下是你（以 root 身份登录时）输入的获取它的命令：

```
cp /var/www/error/noindex.html /var/www/html/index.html
```

现在你有了一个默认主页，可以在终端窗口中输入以下命令检查 Web 服务器是否工作：

```
telnet localhost 80
```

在收到“Connected”消息后，输入

```
HEAD / HTTP/1.0
```

然后按两次回车。你将得到一个类似下面的响应（带有不同的日期和数字，当然如此）：

```
HTTP/1.1 200 OK
Date: Sat, 13 Mar 2004 21:51:18 GMT
Server: Apache/2.0.48 (Fedora)
Last-Modified: Sat, 13 Mar 2004 21:51:18 GMT
ETag: "
Accept-Ranges: bytes
Connection: close
Content-Type: text/html; charset=utf-8
```

响应显示了关于服务器的一些信息。

![](img/d9230b719dc0efd80851f363d8c6f571_647_0.png)

如果你要在启动时自动启动 Apache 服务器，请输入：

```
chkconfig --levels httpd on
```

## 配置 Apache 服务器

默认情况下，Apache 服务器配置如下：

- 服务器程序——httpd 安装在 `/usr/sbin/`。
- 服务器配置文件——httpd.conf 位于 `/etc/httpd/conf/`。该文件是包含服务器各个方面指令的文本文件。`/etc/httpd/conf` 目录还包含有关安全套层 (SSL) 需要的信息。（SSL 实现作为服务器的一部分）。
- Apache 服务器设置为从 `/var/www/html/` 提供文档。因此，将你的网页放在该目录中。
- 如果你有任何网关接口 (CGI) 程序——服务器可以调用以访问其他文件和数据库的程序——将它们放在 `/var/www/cgi-bin/`。
- `/var/log/httpd` 目录用于服务器日志。
- `/etc/init.d/httpd` 脚本启动 httpd 进程。

# 使用 Apache 工具

Fedora Core 提供了一个用于配置 Apache Web 服务器的图形工具。要运行此工具，请以 root 登录并在 GNOME 桌面选择主菜单>设置>服务器设置>HTTP。Apache 配置窗口将会出现（如图 2-2 ）。

图 2-2：你可以从此配置窗口配置 Apache 服务器。

![](img/d9230b719dc0efd80851f363d8c6f571_648_0.png)

Apache 配置窗口由四个标签页组成。你可以从这些标签页中设置各种选项：

- 主页：通过此标签页，你可以指定 Apache 接收 Web 服务请求的 IP 地址和端口。你还可以设置管理员的电子邮件地址。
- 虚拟主机：在这里你可以设置虚拟主机。我将在本章稍后讨论虚拟主机的选项。你还可以编辑适用于所有虚拟主机的默认设置。点击虚拟主机页上的“编辑默认设置”按钮会弹出另一个窗口（如图 2-3 ）。
- 服务器：此标签页具有服务器设置，例如运行 HTTP 服务器的用户名和组名，以及存储进程 ID 的文件位置。

