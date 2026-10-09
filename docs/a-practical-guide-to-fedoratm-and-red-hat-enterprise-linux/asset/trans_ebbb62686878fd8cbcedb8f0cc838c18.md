

Apache 使用外部模块，称为动态共享对象（DSO），来实现基本和高级功能；如果没有这些模块，Apache 就没什么作用。Apache 还使用模块来扩展其功能。例如，模块可以处理用 Perl、PHP、Python 和其他语言编写的脚本；使用几种不同的方法对用户进行身份验证；促进内容发布；并处理非文本内容，如音频。由 Apache 软件基金会（ASF）和第三方开发者编写的模块列表在不断增长。更多信息请参阅第 968 页的“Modules”。

![](img/243613168ac865b539f12460d966088e_989_0.png)

您可以使用 HTTP Server Configuration 窗口（system-config-httpd 软件包）以图形化方式配置 Apache。通过输入命令 `system-config-httpd` 从“输入命令”窗口（Alt+F2）或终端模拟器中打开此窗口。在此窗口中点击“帮助”以获取更多信息。

## 更多信息

- **本地**
    - Apache 文档：在 Apache 正在运行且安装了 `httpd-manual` 软件包的情况下，用浏览器指向 `server/manual`。在服务器系统上，用 `localhost` 替换 *server*；在远程系统上，用 Apache 服务器的名称或 IP 地址替换 *server*。如果 Apache 未运行，请仅在服务器系统上用浏览器指向 `/usr/share/httpd/manual/index.html`。
    - `apachectl` 和 `httpd` 手册页
    - Apache 指令：`server/manual/mod/directives.html`
    - SSI 指令：`server/manual/howto/ssi.html`
- **Web**
    - Apache 文档：httpd.apache.org/docs/2.4
    - Apache 指令：httpd.apache.org/docs/2.4/mod/directives.html
    - Apache 软件基金会（新闻通讯、邮件列表、项目、模块注册表等）：www.apache.org
    - `webalizer`：www.webalizer.org
    - `awstats`：awstats.sourceforge.net
    - `mod_perl`：perl.apache.org
    - `mod_php`：www.php.net
    - `mod_python`：www.modpython.org；参见 `mod_wsgi`
    - `mod_ssl`：www.modssl.org
    - `mod_wsgi`：wsgi.readthedocs.org/en/latest, code.google.com/p/modwsgi
    - MR TG：oss.oettiker.ch/mrtg
    - SNMP：net-snmp.sourceforge.net
    - SSI 指令：httpd.apache.org/docs/2.4/howto/ssi.html

## 注意事项

- **术语：Apache 和 httpd**
    - *Apache* 是一个提供 HTTP 和其他内容服务的服务器名称。Apache 守护进程被命名为 *httpd*，因为它是 HTTP 服务器守护进程。本章互换使用术语 *Apache* 和 *httpd*。
- **术语：server 和 process**
    - Apache 的 *server* 与 Apache 的 *process* 是同一事物。Apache 子进程的存在是为了处理传入的客户端请求；因此它被称为服务器。

**防火墙** Apache 服务器通常使用 TCP 端口 80；安全服务器使用 TCP 端口 443。如果服务器正在运行防火墙或位于防火墙之后，您需要打开其中一个或两个端口。输入以下命令，以便在每次系统启动时（永久地）以及在运行中的系统上打开这些端口；有关 **firewall-cmd** 的信息请参阅第 906 页。

```bash
# firewall-cmd --add-port=80/tcp
# firewall-cmd --permanent --add-port=80/tcp
# firewall-cmd --add-port=443/tcp
# firewall-cmd --permanent --add-port=443/tcp
```

**SELinux** 当 SELinux 设置为使用基于目标的策略时，**httpd** 受 SELinux 保护。如有必要，您可以禁用此保护。更多信息请参阅第 475 页的“使用 **system-config-selinux** 设置基于目标的策略”。

**以 root 权限运行** 由于 Apache 在特权端口上提供内容服务，您必须以 **root** 权限启动它。出于安全原因，Fedora/RHEL 将 Apache 设置为生成以用户和组 **apache** 身份运行的进程。

**区域设置** **httpd** 守护进程默认使用 C 区域设置启动。您可以修改此行为——例如，使用已配置的系统区域设置——通过设置 /etc/sysconfig/httpd 文件中的 **HTTPD_LANG** 变量。

**文档根目录** Apache 提供内容服务的目录层级的根目录称为**文档根目录**，由 DocumentRoot 指令控制（第 942 页）。此指令定义了服务器上的一个目录，该目录映射到 / 。对于浏览网站的用户来说，此目录显示为根目录。在 Fedora/RHEL 分发版中，文档根目录为 /var/www/html。

**修改内容** 在 Fedora/RHEL 的默认 Apache 配置中，只有拥有 **root** 权限的用户才能向 /var/www/html 中添加或修改内容。为避免让人们在操作内容时使用 **root** 权限，请创建一个组（例如 **webwork**），将需要处理 Web 内容的人放入该组，并使从 /var/www/html（或其他文档根目录）开始的目录层级可被该组写入。此外，如果您赋予目录层级 setgid 权限，在此层级中创建的所有新文件都将属于该组，这有助于文件共享。下面前三个命令添加了新组，将文档根目录的模式更改为 setgid，并更改文档根目录所属的组。最后一个命令将 **username** 添加到 **webwork** 组；您必须对您想要添加到该组的每个用户重复执行此命令。

```bash
# groupadd webwork
# chmod g+rws /var/www/html
# chown :webwork /var/www/html

# usermod -aG webwork username
```

有关处理组的更多信息，请参阅第 600 页。

**版本** Fedora/RHEL 运行 Apache 2.4 版本。

## 运行 APACHE WEB 服务器

本节介绍如何安装、测试和配置一个基本的 Web 服务器。

### 前提条件

**组安装**
输入以下命令以安装 Web Server 组软件包。除了 **httpd** 之外，此命令还安装了对 PHP、Perl 和 Python 的支持；Apache 文档；使用 HTTPS 协议加密内容；以及数据库驱动的 Web 网站。

```bash
# yum groupinstall "Web Server"
```

**最小安装**
安装以下软件包：

- httpd
- apr（Apache 可移植运行时；随 **httpd** 一起安装）
- apr-util（随 **httpd** 一起安装）

**在设置 Apache 服务器之前**

> 在配置 Apache 服务器之前，为服务器系统设置一个静态 IP 地址。请参阅第 641 页的“为有线 NIC 配置静态 IP 地址”获取说明。

**启用并启动 httpd**
运行 **systemctl** 以便每次系统进入多用户模式时都启动 **httpd** 服务，然后启动 **httpd** 服务。使用 **systemctl status** 命令确保服务正在运行。

```bash
# systemctl enable httpd.service
# systemctl start httpd.service
```

在修改 Apache 配置文件后，再次输入第二个命令，将 **start** 替换为 **reload** 以使 Apache 重新读取这些文件。

**可选软件包**
您可能想要安装以下可选软件包：

- **httpd-manual** — Apache 手册；更多信息请参阅第 933 页的“本地”
- **webalizer** — Web 服务器日志分析器（第 975 页）
- **awstats** — Web 服务器日志分析器
- **mod_perl** — 嵌入式 Perl 脚本语言
- **mod_wsgi** — 嵌入式 Python 脚本语言
- **mod_ssl** — Secure Sockets Layer 扩展（第 970 页）
- **php** — 包含嵌入式 PHP 脚本语言，支持 IMAP 和 LDAP
- **mrtg** — MRTG 流量监视器（第 975 页）
- **net-snmp** 和 **net-snmp-utils** — SNMP，MRTG 所必需（第 975 页）

## 快速入门：让 APACHE 运行起来

要让 Apache 运行起来，请按照本节所述修改 /etc/httpd/conf/httpd.conf 配置文件。第 940 页的“开始使用时可能需要修改的指令”更详细地解释了此文件，并探讨了您可能想要对其他设置所做的更改。

## 修改 httpd.conf 配置文件

Apache 安装后即可运行，建议在启动 Apache 之前添加/修改 /etc/httpd/conf/httpd.conf 配置文件中本小节所述的三行内容。如果您不添加/修改这些行，Apache 将分配可能在服务器上不工作的值。

ServerName 行为服务器建立一个名称。向 httpd.conf 添加以下其中一行，以将服务器名称设置为服务器的域名，或者如果您没有域名，则设置为服务器的 IP 地址。在 httpd.conf 文件中，在已注释的 ServerName 行正下方添加该行。已注释的行指定端口 80（行尾的 :80）；由于端口 80 是默认值，因此您不需要指定它。

```apache
ServerName example.com
```

或者

```apache
ServerName IP_address
```

其中 example.com 是服务器的域名，IP_address 是服务器的 IP 地址。如果您未连接到网络，可以使用 localhost 地址 127.0.0.1，以便启动服务器并使用服务器系统上的浏览器对其进行实验。有关 ServerName 指令的更多信息，请参阅第 942 页。

当客户端从服务器获取信息遇到麻烦时，服务器通常会显示一个标识问题的错误页面。例如，当 Apache 找不到请求的页面时，它会显示一个写着 Error 404: Not Found 的错误页面。ServerSignature 指令（第 956 页）允许您向服务器生成的页面（包括错误页面）添加签名行。您可以使用此指令开启或关闭签名行。您还可以指定签名行包含一个 mailto: 链接，用户可点击该链接向服务器管理员发送邮件。此链接显示为用户在浏览器中访问的域名。ServerAdmin（第 941 页）指令指定当用户点击错误页面上的链接时，服务器发送邮件的电子邮件地址。在 httpd.conf 中修改这两行中的第一行，并添加第二行。

```apache
ServerAdmin email_address

ServerSignature EMail
```

