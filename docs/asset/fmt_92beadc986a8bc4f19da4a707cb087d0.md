
# 将多个服务器连接到单个 Internet 连接

DNAT（目标地址转换）可以设置规则，允许来自互联网的客户端向局域网（LAN）上的服务器发送包。本示例在 `192.168.1.33` 上设置了一个 SMTP 邮件服务器，在 `192.168.1.34` 上设置了一个 Apache（Web）服务器。这两个协议都使用 TCP；SMTP 使用 25 端口，Apache 使用 80 端口，因此规则匹配目标端口为 25 和 80 的 TCP 数据包。该示例假设邮件服务器不会建立出连接，并使用另一个服务器进行 DNS 和邮件中继。通过在 NAT 的 `PREROUTING` 链中放入命令（`-A PREROUTING -t NAT`）：

```
$ sudo iptables -A PREROUTING -t NAT -p tcp --dport 25 --to-192.168.0.33:25 -j DNAT
$ sudo iptables -A PREROUTING -t NAT -p tcp --dport 80 --to-192.168.0.34:80 -j DNAT
```

为了匹配这些规则，数据包必须使用 TCP 协议，且目标端口为 25（第一个，`--dport 25`）或 80（第二个，`--dport 80`）。

`--to` 是 NAT 表中 `PREROUTING` 和 `OUTPUT` 链中的一个目标；它按指定更改匹配数据包的目标地址和端口。通过 `MASQUERADE` 和 `SNAT`，相同及相关链中的后续数据包也将被同样修改。

服务器无法发起连接这一事实意味着，任何服务器都无法用于对互联网上的系统进行 DDoS 攻击（第 1144 页），也无法从本地系统将私有数据发送回恶意用户的系统。

## 本章总结

防火墙（如 `iptables`、`gufw` 或 `firestarter`）旨在防止对系统或网络未经授权的访问。`firestarter` 和 `gufw` 工具是复杂的图形化工具，用于构建和维护防火墙。每种工具都可以保护其运行的系统，或者保护其运行的系统以及通过 `firestarter` 或 `gufw` 连接到互联网的局域网内的系统。

`iptables` 命令在内核中设置或维护控制网络数据包流的规则；规则存储在链中。每条规则包含一个准则部分和一个动作部分（称为目标）。准则部分匹配网络数据包，内核将规则中的动作应用到数据包。

链被收集在三个表中：`Filter`、`NAT` 和 `Mangle`。`Filter`（默认表）根据内容丢弃（`DROP`）或接受（`ACCEPT`）数据包。`NAT`（网络地址转换表）转换数据包的源或目的字段。`Mangle` 用于修改数据包中的 `TOS`（服务类型）、`TTL`（存活时间）和 `MARK` 字段。连接跟踪机制由 `conntrack` 模块处理，它定义了根据数据包所处连接状态匹配准则的规则。

## 练习

1. 如何删除所有的 `iptables` 规则和链？
2. 什么是 `firestarter`？它与 `iptables` 有什么关系？
3. 使用 `firestarter` 设置规则最的方法是什么？
4. 如何列出所有当前的 `iptables` 规则？
5. 配置 `iptables` 与配置大多数 Linux 服务有什么不同？
6. 定义一个 `iptables` 规则，拒绝 `TEL-NET` 端口的入站连接。
7. `NAT` 代表什么？`NAT` 表的作用是什么？

# 高级练习

8. `conntrack` 模块的作用是什么？
9. 规则匹配准则的作用是什么？它们被用于什么？
10. 数据包匹配准则的作用是什么？它们被用于什么？
11. 哪些工具在内核与用户空间之间拷贝数据包过滤规则？它们是如何工作的？
12. 定义一条规则，静默拦截来自 `spmr.com` 的入站 SMTP 连接。

# 26 APACHE：设置 Web 服务器

### 本章内容

- 快速上手：让 Apache 运行起来 .... 903
- 配置 Apache ....................... 905
- 配置指令 ........................ 909
- 上下文与容器 ...................... 915
- Ubuntu apache2.conf 文件 ......... 932
- 重定向 ............................ 935
- 内容协商 .......................... 935
- 类型映射 .......................... 935
- 多视图 (MultiViews) ............... 936
- 虚拟主机 .......................... 937
- 故障排除 .......................... 940

万维网（WWW 或简称 Web）是一个服务器集合，这些服务器承载着 Web 浏览器（或简称浏览器）可以展示的——内容。Web 上的每个服务器都连接到互联网，这是一个网络网络（互联网络）。Web 上的大部分内容使用 HTML（超文本标记语言，第 1152 页）编码。超文本链接（即你在网页上点击的链接）允许浏览器显示并响应互联网上的其他网页。

Apache 是互联网上最流行的服务器。它既健壮又具扩展性。在 Linux 环境中安装、配置和运行的便捷性，使其成为在万维网上发布内容的明显选择。Apache 服务器及相关项目由 Apache 软件基金会（ASF）开发和维护，ASF 是一家 1999 年 6 月成立的非营利机构。ASF 源于 Apache小组，该小组成立于 1995 年，旨在开发 Apache 服务器。

本章首先提供关于 Apache 的介绍性信息。在这些信息之后是“快速上手”部分，描述了让 Apache 运行起来所需的最小步骤。接下来是“文件系统布局”，它告诉你 Apache 文件的位置。配置指令（简称为指令）是 Apache 的关键部分，从第 909 页开始讨论。本节还涵盖了上下文和容器，这是两个关键特性/概念。932 页开始的下一节介绍了 Ubuntu 分发的 Apache 主配置文件 `apache2.conf`。本章的最后几页涵盖了虚拟主机、故障排除以及可以使用 Apache 的模块。

# 引言

Apache 是一个响应 Web 浏览器（如 `Firefox`、`Netscape`、`lynx` 和 `Internet Explorer`）请求的服务器。当你在浏览器地址栏输入网页（URI，第 1179 页）地址时，浏览器通过互联网向该地址发送请求。作为响应，服务器将请求的内容发回浏览器。浏览器显示或播放这些内容，可能是歌曲、图片、视频剪或其他信息。

- **内容** 除了可以与内容交互的扩展模块外，Apache 只查看正在发送的数据类型，以便指定正确的 `MIME`（第 1160 页）；否则它对内容本身一无所知。服务器管理和内容创建是建立网站的两个不同方面。本章关注设置和运行 Apache 服务器；它像 Linux 内核一样，使用外部模块增加加载灵活性，并允许在不重新编译整个程序的情况下重新编译部分代码。模块不是 Apache 二进制的一部分，而是存储为单独的文件，可以在 Apache 启动时加载。
- **模块** Debian/Ubuntu Apache 团队提供了一个易用的 Apache；它使用外部模块（称为动态共享对象）来实现基础和高级功能；没有这些模块，Apache 作用不大。Apache 还使用模块来扩展功能。例如，模块可以处理 `Perl`、`PHP`、`Python` 和其他语言的脚本；可以使用多种方法验证用户；方便发布内容；处理上下文内容。ASF 和第三方开发者编写的模块列表不断增长。更多信息请参阅第 941 页的“模块”。
- **设置** 大多数提供 Web 界面并依赖 Apache 的包都是按安装设置运行的；通常你不需要修改配置文件。

# 引言 901

例如，安装 `phpmyadmin` (`sourceforge.net/projects/phpmyadmin`) 后，可以通过浏览器作为 `/phpmyadmin` 访问它。

本节描述了你需要安装的软件包，并为本章涵盖的程序提供了参考。“注释”部分引入了术语和其他可能帮助你更好地理解本章的其他主题。“快速启动（JumpStart）”部分（第 903 页）将帮助你尽快运行起 Apache。

### 更多信息

- 本地 Apache HTTP 服务器 2.2 文档：在 Apache 运行并安装了 `apache-2-doc` 的情况下，将浏览器指向 `server/manual`，其中 `server` 是 `localhost` 或 Apache 服务器名称或 IP 地址。
- Apache 指令：`server/manual/mod/directives.html`
- SSI 指令：`server/manual/howto/ssl.html`
- Web Apache 文档：`http.apache.org/docs/2.2`
- Apache 指令：`http.apache.org/docs/2.2/mod/directives.html`
- Apache 软件基金会（时事、邮件列表、项目、模块注册表等）：`www.apache.org`
- `webalizer`：`www.murunix.net/webalizer`
- `awstats`：`awstats.sourceforge.org`
- `libapache2-mod-perl`：`perl.apache.org` (`mod_perl`)
- `libapache2-mod-php5`：`www.php.net` (`mod_php`)
- `libapache2-mod-python`：`www.modpython.org` (`mod_python`)
- `SSL`：`modssl.org` (`mod_ssl`)
- `MRTG`：`mrtg.hartl/mrtg`
- `SNMP`：`net-snmp.sourceforge.net`
- SSI 指令：`http.apache.org/docs/2.2/howto/ssl.html`

# 注释

- **术语：Apache 和 apache2** Apache 是提供 HTTP 和其他内容的服务器名称。Apache 2 守护进程名称是 `apache2`。
- **术语：server（服务器）和 process（进程）** Apache 服务器等于 Apache 进程。Apache 子进程的存在是为了处理传入的客户端请求；它被称为服务器。
- **防火墙** Apache 服务器通常使用 TCP 端口 80；安全服务器使用 TCP 端口 443。如果 Apache 系统正在运行或位于防火墙后，你必须开启其中一个或两个端口。开始之前，打开端口 80 (HTTP)。使用 `gufw`（第 876 页），通过设置允许 HTTP 和或 HTTPS 服务的策略来打开这些端口。
- **以 root 权限运行** 由于 Apache 在特权端口上提供内容，你必须以权限启动运行。出于安全考虑，Ubuntu 将 Apache 设置为产生以 `www-data` 用户和组运行的进程。
- **语言环境（Locale）** `apache2` 守护进程默认以 C 语言环境启动。你可以修改此行为——例如，通过使用配置的系统语言环境——在 `/etc/init.d/apache2` 文件中设置 `LANG` 变量（在以 `ENV=-i LANG= ...` 开头的行中）。

Apache 提供内容的目录层次结构根节点称为文档根（document root），由 `DocumentRoot` 指令控制（第 913 页）。该指令定义了服务器上一个映射到 `/` 的目录。浏览 Web 网站的用户来说，该目录显示为根目录。作为 Ubuntu 分发的版本，文档根是 `/var/www`。

使用 Apache 的 Ubuntu 默认配置修改内容，只有具有 `root` 权限的用户才能在 `/var/www` 中添加或修改内容。为了避免人们在操作内容时以 `root` 身份工作，创建一个组（例如 `webwork`），让人们在该组中处理 Web 内容，并让从 `/var/www`（另一个文档根）开始的目录层次结构对该组可见。此外，如果你设置了目录权限，该层次结构内创建的所有新文件将属于该组，这有助于共享文件。下方的前三个命令添加新组，将文档根的模式更改为 `setgid`，并更改目录所属的组。最后一个命令将用户名添加到 `webwork` 组；你必须对每个想要添加到组的用户重复执行此命令。

```
$ sudo addgroup webwork
$ chmod g+s /var/www
$ sudo chown :webwork /var/www
```

有关与组操作的更多信息请参阅第 597 页。

运行 Apache 版本 2.2。

# 运行 Web 服务器 (APACHE)

本节解释了如何安装、测试和配置基础 Web 服务器。

# 先决条件

最小化安装 安装以下软件包：

- `apache2`

`apache2` init 脚本：当你安装 `apache2` 软件包时，`dpkg` `postinst` 脚本会启动 `apache2` 守护进程。配置 Apache 后，调用 `apache2` init 脚本来重启 `apache2` 守护进程。

```
$ sudo service apache2 restart
```

在活动服务器上更改 Apache 配置后，使用 `reload` 代替 `restart`。`reload` 在不干扰连接到服务器的客户端的情况下重新加载 Apache 配置。

可选软件包：`mod_ssl` 软件包作为 `apache2` 软件包的一部分安装——你不需要单独安装它。你可能想要安装以下可选软件包：

- `apache2-doc`—Apache 手册
- `webalizer`—Web 服务器日志分析器（第 948 页）
- `awstats`—Web 服务器日志分析器
- `libapache2-mod-perl2`—嵌入式 Perl 脚本语言 (`mod_perl`)
- `libapache2-mod-python`—安装嵌入 Python 脚本语言的元包 (`mod_python`)
- `libapache2-mod-php5`—嵌入式 PHP 脚本语言，包括 IMAP 和 LDAP 支持 (`mod_php`)
- `mrtg`—MRTG 流量监控（第 948 页）

**`apache2ctl` 工具**

> 提示：`apache2ctl` 用于重启 Apache。

# 快速启动：让 Apache 运行

为了让 Apache 运行，按照本节所述修改 `/etc/apache2/sites-available/default` 文件。

# 修改配置文件

Apache 以安装状态运行，但建议在 `/etc/apache2/sites-available/default` 文件中添加以下几行。`ServerName` 确定了服务器的名称。在默认配置文件中添加这些几行以重启 Apache（第 902 页）。

```
ServerName example.com
```

或者

```
ServerName IP_address
```

其中 `example.com` 是域名，`IP_address` 是服务器的 IP 地址。如果你没有域名，使用 IP 地址。在 `/etc/apache2/sites-available/default` 文件中添加这些行：

```
ServerAdmin email_address
ServerSignature EMail
```

`email_address` 是需要知道有人在使用服务器的电子邮件地址。确保有人经常检查此帐户。但也请参见提示中的“`ServerAdmin`”。

使用角色别名（例如 `webmaster@example.com`）而不是特定的用户名（例如 `max@example.com`）作为 `email_address`，可以让系统管理变得容易得多。见第 722 页关于电子邮件别名的讨论。

在对文件进行更改后，按照第 902 页所述重启 `apache2`。

# 测试 Apache

重启 `apache2` 守护进程后，你可以通过将浏览器指向本地（服务器）系统的 `http://localhost/` 来确认 Apache 是否正常工作。从远程系统，将浏览器指向 `http://` 后跟你在上一节中指定的 `ServerName`。如果你从本地以外显示页面，本地系统必须知道如何解析你输入的域名（例如使用 DNS 或 `/etc/hosts` 文件）。例如，你可能使用以下任一 URI 格式：`http://192.168.0.16` 或 `http://example.org`。

当你将浏览器包含 `index.html` 文件的目录时，Apache 会导致浏览器显示该文件的内容（否则将显示目录列表）。响应你的请求时，浏览器应该显示存储在服务器 `/var/www/index.html` 的页面。在这种情况下，浏览器应该显示内容！

# 将你的内容放置就位

将 Apache 自动显示的内容放置在 `/var/www` 中。如前所示，Apache 会自动显示此目录中名为 `index.html` 的文件。执行以下命令来创建一个页面以替换默认页面：

```
$ sudo tee /var/www/index.html
<html><body>This is <my> test page.</p></body></html>
<html><body>This is <my> test page.</p></body></html>
```
