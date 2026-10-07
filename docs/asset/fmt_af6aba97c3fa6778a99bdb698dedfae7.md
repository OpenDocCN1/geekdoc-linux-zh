
为了获得最佳安全性，请使用专用系统作为路由器。由于通过互联网连接传输数据（即使是宽带连接）也相对缓慢，因此使用速度较慢的旧系统作为路由器通常不会降低局域网（LAN）的速度。这种设置还能对来自互联网的入侵提供防御。局域网上的工作站也可以作为路由器，但这意味着你直接连接到互联网的系统上维护数据。以下将讨论每种设置的安全性。

本节中的示例假设名为 `eth0` 的设备通过 `10.255.255.255` 连接互联网，`eth1` 通过 `10.168.0.1` 连接局域网。请根据本地系统的实际情况替换设备和 IP 地址。如果你使用调制解调器连接互联网，需要在示例中将 `eth0` 替换为 `ppp0`（或其他设备）。

要使本节中的示例生效，你必须开启 IP 转发。首先执行以下命令并确保输出如所示：

```
$ sysctl -w ipv4.ip_forward=1

net.ipv4.ip_forward = 1
```

如果你想转发 IPv6 数据包，请执行此命令：

```
$ sysctl -w net.ipv6.conf.all.forwarding=1

net.ipv6.conf.all.forwarding=1
```

一旦确认 `iptables` 正常工作，请按照 `/etc/sysctl.conf` 中的说明，取消以下一个或两个赋值的注释，使内核始终对 IPv4/或 IPv6 执行 IP 转发：

```
# 取消下一行的注释以启用 IPv4 包转发

net.ipv4.ip_forward=1
```

```
# 取消下一行的注释以启用 IPv6 包转发

net.ipv6.conf.all.forwarding=1
```

执行此更改后，执行命令 `/bin/sysctl -p` 应用更改，并确保配置文件没有拼写错误。

## 将多个客户端连接到单个互联网连接

配置路由器系统的内核以允许局域网内多个本地系统的客户端连接到互联网，需要设置 IP 伪装或 SNAT（源网络地址转换）。IP 伪装会翻译源自本地系统的数据包头中的源地址和目的地址，以及远程服务器响应这些数据包时发送的数据包。这些数据包是源自本地系统连接的一部分。本节中的示例对源自远程系统（互联网）的数据包不做任何操作：这些数据包无法进入路由器系统，这提供了某种程度的安全性。

重写数据包头的目的是允许具有不同本地 IP 地址的系统共享互联网上的同一个 IP 地址。路由器系统将来自本地系统的数据包的源地址翻译为互联网连接的地址，使得所有从路由器传输到互联网的数据包看起来都来自同一个系统——示例中为 `10.255.255.255`。互联网上的远程系统向路由器发送的所有响应包具有互联网连接的地址——示例中为 `10.255.255.255`——路由器记住每个连接，并将每个响应包的目的地址更改为本地源系统的地址。

路由器系统通过四个 `iptables` 命令建立，其中一个命令在 filter（默认）表的 `FORWARD` 链中设置了规则（`-A FORWARD`）：

```
sudo iptables -A FORWARD -i eth0 -o eth1 -m state --state ESTABLISHED,RELATED -j ACCEPT
```

要匹配此规则，数据包必须满足：
- 在 `eth0` 上接收（来自互联网）：`-i eth0`。
- 准备从 `eth1` 发出（往局域网）：`-o eth1`。
- 是已建立连接或与已建立连接相关的：`--state ESTABLISHED,RELATED`。

内核接受（`- ACCEPT`）符合这三个标准的数据包。数据包传递到下一个适当的链或表。尝试创建新连接的数据包不会匹配，因此不会被此规则接受。不被接受的数据包传递到 `FORWARD` 链中的下一条规则。

第二个命令在 Filter 表的 `FORWARD` 链中放置了第二条规则：

```bash
sudo iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```

要匹配此规则，数据包必须满足：
- 在 `eth1` 上接收（来自局域网）：`-i eth1`。
- 准备从 `eth1` 发出（往局域网）：`-o eth1`。

# 26
# APACHE：搭建 Web 服务器

## 本章内容

- 快速上手：让 Apache 运行起来 . . . . . . 903
- 配置与容器 . . . . . . . . . . . . 905
- 配置指令 . . . . . . . . . . . . 909
- 上下文与网络 . . . . . . . . . . . . . 915
- Ubuntu 的 apache2.conf 文件 . . . . . . . . . 932
- 重定向 . . . . . . . . . . . . . . . . 935
- 内容协商 . . . . . . . . . . . . 935
- 类型映射 . . . . . . . . . . . . . . . . . 935
- 多视图 (MultiViews) . . . . . . . . . . . . . . . . 936
- 虚拟主机 . . . . . . . . . . . . . . . . 937
- 故障排除 . . . . . . . . . . . . . . . 940

世界维网（WWW 或简称为 Web）是一个包含名为*内容*的服务器集合，Web 浏览器（或简称浏览器）可以显示这些内容。Web 上的每个服务器都连接到互联网，即一个网络网络（*网络互联*）。Web 上的大部分内容使用 HTML（超文本标记语言，第 1152 页）编写。超文本（你在 页面上点击的链接）允许浏览器显示并响应指向互联网上其他 Web 页面的链接。

Apache 是互联网上最流行的 Web 服务器。它既健壮又具扩展性。在 Linux 环境中安装、配置和运行它的便利性，使其成为在世界维网上发布内容的明显选择。Apache 服务器及相关项目由 Apache 软件基金会（ASF）开发和维护，ASF 是 1999 年 6 月成立的非营利机构。ASF 源于 Apache Group，该小组成立于 1995 年用于开发 Apache 服务器。

本章首先提供关于 Apache 的介绍性信息。之后是“快速上手”部分，描述了让 Apache 运行起来所需的最少步骤。接下来是“文件系统布局”，它告诉你各种 Apache 文件的位置。

配置指令（简单称为指令）是 Apache 的关键部分，从第 909 页开始讨论。本节涵盖了上下文和容器，这是理解 Apache 至关重要的两个功能/概念。下一节从第 932 页开始，解释了 Ubuntu 分发的主要的 Apache 配置文件 `apache2.conf`。本章的最后几页涵盖了虚拟主机、故障排除以及你可以配合 Apache 使用的模块，包括 CGI 和 SSL。

## 绪言

Apache 是一个响应 Web 浏览器或客户端（如 Firefox、Netscape、lynx 和 Internet Explorer）请求的服务器。当你在 Web 浏览器的地址栏中输入 Web 页面的地址（URI，第 1179 页）时，浏览器会通过互联网向该地址的（Apache）服务器发送请求。作为响应，服务器会将请求的内容传回浏览器。浏览器随后显示或播放该内容，这些内容可能是歌曲、图片、视频剪或其他信息。

除了可以与内容交互的 `add-modules` 之外，Apache 只查看它正在发送的数据类型，以便能够指定正确的 MIME（第 1160 页）；否则它对内容本身一无所知。服务器管理和内容创建是建立网站的两个不同方面。本章重点关注设置和运行 Apache 服务器；花费较少的时间讨论内容创建。

Apache 像 Linux 内核一样，使用外部模块来增加加载时的灵活性，并允许在不重新编译整个程序的情况下替换其代码部分。模块不是 Apache 二进制执行文件的一部分，而是作为单独的文件存储，可以在 Apache 启动时加载。

Apache 使用外部模块（动态共享对象，DSOs）来实现基本和高级功能；没有这些模块，Apache 将大打折扣。Apache 还使用模块来扩展其功能。例如，模块可以处理 Perl、PHP、Python 和其他语言的脚本；使用多种方法验证用户身份；促进内容发布；以及处理非文本内容（如音频）。由 ASF 和第三方开发者编写的模块列表在不断增长。更多信息请参阅第 941 页的“模块”。

Debian/Ubuntu Apache 团队提供了任何发行版中最易于使用的 Apache 设置方案之一。大多数提供 Web 界面并要求 Apache 按安装方式运行的包；通常情况下你不需要修改配置文件。

例如，安装 phpmyadmin 可以使其通过 `/phpmyadmin` 供浏览器访问。

本节描述了你需要安装的包，以及本章涵盖的程序的参考资料。“注释”部分介绍了术语和其他可能帮助你更好地理解本章的话题。快速上手部分（第 903 页）让你尽可能让 Apache 运行起来。

## 更多信息

- 本地 Apache HTTP 服务器版本 2.2 文档：在 Apache 运行并安装了 `apache2-doc` 的情况下，将浏览器指向 `server/manual`，其中 `server` 是 `localhost` 或 Apache 服务器的名称或 IP 地址。
- Apache 指令：`server/manual/mod/directives.html`
- SSL 指令：`server/manual/howto/ssl.html`
- Web Apache 文档：`httpd.apache.org/docs/2.2`
- Apache 指令：`httpd.apache.org/docs/2.2`

## 运行 Web 服务器 (APACHE)

- `apache2doc`—Apache 手册
- `webalizer`—Web 服务器日志分析器（第 948 页）
- `awstats`—Web 服务器日志分析器
- `libapache2-mod-perl2`—嵌入 Perl 脚本语言 (`mod_perl`)
- `libapache2-mod-python`—元包，安装嵌入 Python 脚本语言 (`mod_python`)
- `libapache2-mod-php5`—嵌入 PHP 脚本语言，包括 IMAP 和 LDAP 支持 (`mod_php`)
- `mrrtG`—流量监控器（第 948 页）

## apache2ctl 工具与优雅重启 Apache

`apache2` init 脚本使用 `apache2ctl` 来启动和停止 Apache。`reload` 参数会带上 `graceful`（优雅）参数调用该工具，这不会干扰连接到服务器的客户端。`restart` 和 `force-reload` 参数会带 `stop` 和 `start` 参数调用该工具；这对命令会在重启服务器之前完全关闭服务器。

## JumpStart：让 Apache 运行起来

要让 Apache 运行起来，请按照本节所述修改 `/etc/apache2/sites-available/default` 配置文件。第 910 页的“指令 I：在开始时可能想要修改的指令”详细说明了该文件的更多信息，并探索了你可能想要进行的其他更改。

## 修改配置文件

Apache 按安装状态即可运行，但将本节中的三行添加到 `/etc/apache2/sites-available/default` 配置文件中是一个好主意。如果不添加这些行，Apache 分配的值可能并不适用。修改此文件后，你必须重启 Apache（第 902 页）。

`ServerName` 为服务器建立一个名称。在 `/etc/apache2/sites-available/default` 中添加以下行之一，以将服务器名称设置为服务器的域名，或者如果你没有域名，则设置为服务器的 IP 地址。将该行添加到文件顶部附近的 `ServerAdmin` 行下方。

```
ServerName example.com
```

或

```
ServerName IP_address
```

其中 `example.com` 是服务器的域名，`IP_address` 是服务器的 IP 地址。如果你没有连接到网络，可以使用 `localhost` 地址 `127.0.0.1`，这样你就可以启动服务器并进行实验。有关 `ServerName` 指令的更多信息，请参见第 934 页。

当客户端从服务器获取信息遇到困难时，服务器通常会显示一个标识问题的错误页面。例如，当 Apache 找不到请求的页面时，它会显示一个“404: Not Found”的页面。每个错误页面都可以包含一个用户可以点击发送给管理员的链接。`ServerSignature` 指令可以指定你想在错误页面上显示的信息。`ServerAdmin` 指令指定服务器发送给用户的电子邮箱地址。在名为 `default` 的文件中，紧跟在 `ServerAdmin` 指令添加这两行：

```
ServerAdmin email_address

ServerSignature
```

其中 `email_address` 是在人们使用服务器时需要知情的人的电子邮件地址。确保有人经常检查此邮箱。但是，如果你使用别名（例如 `webmaster@example.com`）而不是特定的用户名（例如 `max@example.com`），也会让系统管理变得容易得多。请参见第 722 页关于电子邮件别名的讨论。

在对名为 `default` 的文件进行更改后，按照第 902 页的说明重启 `apache2`。

## 测试 Apache

一旦你重启了 `apache2` 守护进程，你可以通过将本地系统的浏览器指向 `http://localhost/` 来确认 Apache 正在工作。从远程系统，将浏览器指向 `http://` 加上上一节中指定的 `ServerName`。如果你正在显示来自本地系统以外的系统的页面，本地系统必须知道如何解析用户输入的域名（例如通过 `/etc/hosts` 文件）。例如，你可以使用以下任一 URI 格式：`http://192.168.0.16` 或 `http://example.org`。

当你将浏览器指向包含名为 `index.html` 文件的目录时，Apache 会导致浏览器显示该文件的内容（否则将显示目录列表）。响应你的请求，浏览器应该显示存储在 `/var/www/index.html` 的页面。在这种情况下，服务器工作正常！如果服务器在防火墙后面，请使用 TCP 端口 80（第 901 页）。如果你在让 Apache 工作方面遇到问题，请参见第 940 页的“故障排除”。

## 放置你的内容

将让 Apache 服务的内容放置在 `/var/www` 中。如前所示，Apache 会自动显示此目录中名为 `index.html` 的文件。使用以下命令创建此类页面以替换默认页面：

```
$ sudo tee /var/www/index.html

<html><body><p>This is <i>my</i> test page.</p></body></html>
```

`tee` 工具（第 254 页）将标准输入（第 243 页）复制到你提供的参数文件以及标准输出（第 243 页）。由于这种重定向，在你按下回车键后，`tee` 会重复你输入的每一行。创建完成后，刷新浏览器上的页面（如果它仍在运行）或重新启动并指向服务器。浏览器应该显示你刚刚创建的页面。

## 配置 Apache

本节描述了你可以用来简化工作的配置工具。它还告诉你可以在哪里找到你需要的文件。

## 配置工具

本节描述了你可以使用来让工作变得更轻松的配置工具。它还告诉你可以在哪里找到你需要的文件。

`a2mod` 和 `a2dismod` 简化了 Apache 管理。与其在配置文件中添加或注释掉 `LoadModule` 指令，你可以使用这些程序来启用或禁用模块。

`a2ensite`（启用站点）和 `a2dissite`（禁用站点）的工作与模块命令类似。首先在 `/etc/apache/sites-available` 目录中创建一个虚拟主机。然后将站点名称作为参数调用 `a2ensite`，在 `/etc/apache/sites-enabled` 目录中创建一个符号链接。`a2dissite` 删除符号链接。

## 指令

在 Ubuntu 下，主配置文件是 `/etc/apache2/apache2.conf`。该文件通过 `Include` 指令（第 927 页）包含其他文件：

```
$ grep ^Include ' /etc/apache2/apache2.conf
Include /etc/apache2/mods-enabled/*.load
Include /etc/apache2/mods-enabled/*.conf
Include /etc/apache2/httpd.conf
Include /etc/apache2/ports.conf
Include /etc/apache2/conf.d/
Include /etc/apache2/sites-enabled/
```
