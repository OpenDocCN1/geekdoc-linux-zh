
## 为什么它叫做 Apache？

根据 www.apache.org/foundation/faq.html 上关于 Apache Web 服务器项目的信息，Apache 组织由一批在 1995 年 3 月提供用于修复 NCSA HTTPd 1.3 错误的补丁文件的人组成。应用补丁到 NCSA HTTPd 后的结果被他们称为 patchy server（这就是 Apache 这个名字来源）。Apache 组织现已发展为 Apache 软件基金会（ASF），这是一个非营利公司，于 1999 年 6 月在美国特拉华州注册成立。ASF 有许多其他正在进行中的项目。你可以在 www.apache.org 上阅读这些项目。特别是，访问 httpd.apache.org 以获取有关 Apache Web 服务器项目的更多信息。

根据 news.netcraft.com/archives/web_server_survey.html 上 2003 年 7 月的 Netcraft Web 服务器调查，Apache Web 服务器是最受欢迎的——据报道有 63.72% 的 42,298,371 个站点使用 Apache 服务器。微软 Internet Information Server（IIS）遥居第二，占 25.95% 的站点。

输出应显示多个 httpd 进程。运行多个 Web 服务器进程是一种常见做法——一个父进程和多个子进程——这样可以通过为每个请求分配一个 httpd 进程来高效处理多个 HTTP 请求。

如果没有 httpd 进程，Apache 配置文件可能潜藏着错误。如果是这种情况，应该会出现一些错误消息，给出错误原因的线索。你必须在配置文件中修复问题并重新启动服务器。

如果 httpd 进程正在运行，你可以使用 TELNET 程序来检查它是否工作，但首先你必须在 /var/www/html 目录中添加一个默认主页。如果你没有时间准备一个，复制在出现错误时应发送的网页。以下是你以 root 登录时输入的命令来获取它：

```
cp /var/www/error/noindex.html /var/www/html/index.html
```

现在你有了默认主页，你可以在终端窗口中输入以下命令来检查 Web 服务器是否工作：

```
telnet localhost 80
```

收到 Connected 消息后，输入

```
HEAD / HTTP/1.0
```

然后按两次 Enter。你应该会得到类似以下的响应（日期和数字当然会不同）：

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
HTTP/1.1 200 OK
Date: Sun, 13 Jul 2003 18:11:11 GMT
Server: Apache/2.0.45 (Red Hat Linux)
Last-Modified: Sun, 13 Jul 2003 18:10:15 GMT
ETag: "bdf93-b52-b7b3efc0"
Accept-Ranges: bytes
Content-Length: 2898
Connection: close
Content-Type: text/html; charset=UTF-8

Connection closed by foreign host.
```

响应显示了有关 Web 服务器和默认主页的一些信息。你也可以使用在 Red Hat Linux 系统上运行的 Mozilla 等 Web 浏览器来检查 Web 服务器。例如，如果你的系统 IP 地址是 192.168.0.5，使用 URL http://192.168.0.5/ 看看会发生什么。你应该会看到一个标题为 "Test Page for the Apache Web Server on Red Hat Linux." 的网页。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_644_0.png)

如果你想在启动时自动启动 Apache Web 服务器，输入以下命令进行设置：

```
chkconfig --levels 35 httpd on
```

## 配置 Apache Web 服务器

Red Hat Linux 配置 Apache Web 服务器软件使用以下目录：

- Web 服务器程序 — httpd — 安装在 /usr/sbin 目录中。
- Apache Web 服务器配置文件 — httpd.conf — 位于 /etc/httpd/conf 目录中。配置文件是一个文本文件，其中包含指令指定 Web 服务器的各个方面。/etc/httpd/conf 目录还包含有关安全套接字层（SSL）实现需求的信息。（SSL 实现是 Apache Web 服务器的一部分。）
- Apache Web 服务器设置为从 /var/www/html 目录提供 HTML 文档。因此你应该将你的网页放在此目录中。
- 如果你有任何通用网关接口（CGI）程序——Web 服务器可以调用的程序来访问其他文件和数据库——你应该将它们放在 `/var/www/cgi-bin/` 目录中。
- `/var/log/httpd` 目录用于 Web 服务器日志文件（访问日志和错误日志）。
- `/etc/init.d/httpd` 脚本在你的 Red Hat Linux 系统启动时启动 `httpd` 进程，前提是你已使用 `chkconfig` 命令启用它。

## 使用 Apache 配置工具

Red Hat Linux 附带一个图形配置工具，可用于配置 Apache Web 服务器。要运行此配置工具，以 root 登录并从 GNOME 桌面选择 主菜单→系统设置→服务器设置→HTTP 服务器。Apache 配置对话框出现（如图 2-2 所示）。

Figure 2-2:
你可以从此配置窗口配置 Apache HTTP 服务器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_645_0.png)

Apache 配置对话框分为四个选项卡。你可以从每个选项卡设置各种选项：

- **Main:** 从此选项卡你可以指定 Apache 应期望 Web 服务请求的 IP 地址和端口号。你还可以设置网站管理员的电子邮件地址。
- **Virtual Hosts:** 在这里你可以设置虚拟主机。我将在本章后面讨论虚拟主机的选项。你还可以编辑适用于所有虚拟主机的默认设置。单击虚拟主机选项卡中的编辑默认设置按钮会弹出另一个对话框（如图 2-3 所示），从中你可以设置许多不同的选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_646_0.png)

Figure 2-3: 你可以从此配置窗口配置虚拟主机属性。

- **Server:** 此选项卡具有服务器设置，例如 HTTP 服务器应运行的用户和组名称以及存储进程 ID 的文件位置。
- **Performance Tuning:** 在此选项卡你可以设置控制整体性能的一些参数。你可以设置允许的最大连接数、连接的超时时间以及每个连接的最大请求数。

最初配置窗口显示配置文件 `/etc/httpd/conf/httpd.conf` 中的默认值。进行任何更改后，单击确定按钮。配置工具会提示你是否真的要保存更改并退出。如果是，单击是，你就完成了。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_646_1.png)

当你从此配置工具配置 Apache HTTP 服务器时，你所做的只是更改存储在 `/etc/httpd/conf/httpd.conf` 文件中的选项和属性。你也可以通过编辑配置文件（这是一个纯文本文件）轻松地进行更改。在下一节中，我将向你介绍 Apache 配置文件中的一些常见配置指令。

## Apache 配置文件

Apache 服务器的操作由位于 `/etc/httpd/conf` 目录中的 `httpd.conf` 配置文件控制。此文件控制服务器如何运行、提供哪些文档以及谁可以访问这些文档。

在接下来的几节中，我总结了有关 `httpd.conf` 配置文件的重要信息。通常，你不需要更改配置文件中的任何内容即可运行 Apache Web 服务器。然而，了解

配置文件的格式以及其中使用的各种关键字的含义是有用的。

在研究 `/etc/httpd/conf` 目录中的配置文件时，请记住以下语法规则：

- 每个配置文件都是一个文本文件，你可以用喜欢的文本编辑器编辑并用 `more` 命令查看。
- 所有注释行都以 `#` 开头。
- 每行只能有一个指令。
- 额外的空格和空行会被忽略。
- 除路径名和 URL 外，所有条目都不区分大小写。

## httpd.conf 配置文件

`/etc/httpd/conf/httpd.conf` 文件是主要的 HTTP 守护进程配置文件——它包含控制 Apache Web 服务器如何运行的指令。例如，`httpd.conf` 文件指定服务器使用的端口号、网站名称以及在服务器出现任何问题时发送邮件的电子邮件地址。此外，`httpd.conf` 还包含有关网页位置以及谁可以访问哪些目录的信息。

在以下各节中，我将 Apache 指令分为三个类别呈现：通用 HTTPD 指令、资源配置指令和访问控制指令。最后，我将解释如何在 Apache Web 服务器中设置虚拟主机，以便单个 Web 服务器可以处理发送到多个 IP 地址或主机名的 Web 请求。

## 通用 HTTPD 指令

`httpd.conf` 文件中的一些有趣项目是

- `ServerName` 指定你的网站的主机名（形式为 `www.your.domain`）以及 Web 服务器接受连接的端口号。`ServerName` 仅在将网页重定向到另一个网页时使用。名称应为已注册的域名，其他用户可通过其名称服务器找到。以下是示例：
  
  ```
  ServerName www.myhost.com:80
  ```
  
  如果你没有注册的域名，使用你的 Red Hat Linux 系统的 IP 地址。
- `ServerAdmin` 是 Web 服务器在发生任何错误时提供给客户端的电子邮件地址。`ServerAdmin` 的默认值是 `root@localhost`。你应该将其设置为有效的电子邮件地址，任何互联网用户都可以使用它来报告你的网站中的错误。
