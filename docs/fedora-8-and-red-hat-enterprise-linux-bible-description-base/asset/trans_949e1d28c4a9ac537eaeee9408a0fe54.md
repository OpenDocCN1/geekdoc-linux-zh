

## 配置虚拟主机

如果你只有一台 Web 服务器计算机，但希望使用这台计算机托管多个域名，可以配置 Apache 以实现虚拟主机。在使用基于名称的虚拟主机时，单个 IP 地址可以是同一台计算机上多个域名的访问入口。在使用基于 IP 的虚拟主机时，每个虚拟主机拥有不同的 IP 地址，这通过为机器配置多个网络接口来实现。

在虚拟主机配置中，当请求从 Web 浏览器通过计算机上的特定 IP 地址进入你的 Apache 服务器时，Apache 会检查请求的域名，并显示与该域名关联的内容。作为支持虚拟主机的 Web 服务器管理员，你必须确保该虚拟服务器所需的所有配置项都已正确设置（你需要定义诸如 Web 内容位置、日志文件、管理员联系方式等）。

虚拟主机通过 `VirtualHost` 标签定义。`/etc/httpd/conf/httpd.conf` 文件中与虚拟主机相关的信息如下面的代码所示：

```text
### Section 3: Virtual Hosts
#
# VirtualHost: If you want to maintain multiple domains/hostnames on
# your machine you can setup VirtualHost containers for them. Most
# configurations use only name-based virtual hosts so the server
# doesn't need to worry about IP addresses. This is indicated by the
# asterisks in the directives below.
#
# Please see the documentation at
# <URL:http://httpd.apache.org/docs/2.2/vhosts/>
# for further details before you try to setup virtual hosts.
#
# You may use the command line option '-S' to verify your virtual host
# configuration.
#
# Use name-based virtual hosting.
#
#NameVirtualHost *:80
#
# NOTE: NameVirtualHost cannot be used without a port specifier
# (e.g. :80) if mod_ssl is being used, due to the nature of the
# SSL protocol.
#
# VirtualHost example:
# Almost any Apache directive may go into a VirtualHost container.
# The first VirtualHost section is used for requests without a known
# server name.
#
#<VirtualHost *:80>
#  ServerAdmin webmaster@dummy-host.example.com
# DocumentRoot /www/docs/dummy-host.example.com
# ServerName dummy-host.example.com
# ErrorLog logs/dummy-host.example.com-error_log
# CustomLog logs/dummy-host.example.com-access_log common
#</VirtualHost>
```

以下示例列出了允许你在同一台计算机上托管 handsomhistory.com 和 linuxtoys.net 这两个域名的虚拟主机指令：

```text
NameVirtualHost *:80
<VirtualHost *:80>
 DocumentRoot /var/www/handsonhistory
 ServerName www.handsonhistory.com
 ServerAlias handsonhistory.com
 ServerAdmin webmaster@handsonhistory.com
 ErrorLog logs/handsonhistory.com-error_log
 CustomLog logs/handsonhistory.com-access_log common
</VirtualHost>
<VirtualHost *:80>
 DocumentRoot /var/www/linuxtoys
 ServerName www.linuxtoys.net
 ServerAlias linuxtoys.net
 ServerAdmin webmaster@linuxtoys.net
 ErrorLog logs/linuxtoys.net-error_log
 CustomLog logs/linuxtoys.net-access_log common
</VirtualHost>
```

若要试验虚拟主机，你可以将新的主机名添加到本地的 `/etc/hosts` 文件中，并将其指向你的本地主机 IP 地址。例如：

```text
127.0.0.1 www.linuxtoys.net
```

如果你看到的是为你设置的虚拟主机内容，而不是 Fedora 错误页面或你设置的默认内容，那么说明你很可能已正确设置了虚拟主机。

## 配置模块及相关服务 (/etc/httpd/conf.d/*.conf)

任何需要特殊配置的模块通常都会在 `/etc/httpd/conf.d` 目录中拥有配置文件（.conf 文件）。以下是可能包含在该目录中的模块化配置文件，以及使用这些文件及其相关包的一些方法（使用 `yum install package` 安装每个所需的包）：

- **auth_kerb.conf** — 配置通过 Web（HTTP）连接进行 Kerberos 认证。
  - 该文件中的示例建议在 SSL 连接上使用 Kerberos 认证。（安装 `mod_auth_kerb` 包。）
- **auth_mysql.conf** — 配置基于添加到 MySQL 数据库中的数据进行的认证。文件中的注释描述了如何设置数据库，然后使用它进行用户或组认证，再允许客户端访问你的 Web 内容。（安装 `mod_auth_mysql` 包。）
- **auth_pgsql.conf** — 配置基于 PostgreSQL 数据库中数据的认证。（安装 `mod_auth_pgsql` 包。）
- **authz_ldap.conf** — 配置认证以访问 LDAP 数据库来验证用户。（安装 `mod_authz_ldap` 包。）
- **htdig.conf** — 识别 htdig 搜索内容的位置，这些内容可用于你的网站（`/usr/share/htdig` 是默认位置）。要从 Web 浏览器查看 htdig 搜索界面，请输入 `http://localhost/htdig`。htdig 系统允许你设置用于索引和搜索网站或公司内网的工具。这对你的 Web 服务器来说是可选的。（安装 htdig-web 包。）
- **mailman.conf** — 设置 mailman 邮件列表服务器软件，以实现诸如从 Apache 提供邮件列表存档等功能。（安装 mailman 包。）
- **manual.conf** — 定义服务器上不同语言的 Apache 手册（`/var/www/manual`）的位置。在浏览器窗口中输入 `http://localhost/manual`。（安装 httpd-manual 包。）
- **mrkg.conf** — 定义每日 mrkg 输出（`/var/www/mrkg`）的位置，它用于跟踪网络流量。在浏览器窗口中输入 `http://localhost/mrkg`。（安装 mrkg 包。）
- **perl.conf** — 识别并加载 `mod_perl` 模块，使你的网页能够包含 Perl 代码。（安装 `mod_perl` 包。）
- **php.conf** — 识别并加载 `libphp5` 模块，使你的网页能够包含 PHP 脚本语言。还有一个 `DirectoryIndex` 设置，允许你添加到目录中的 `index.php` 文件作为目录索引被服务。（安装 php 包。）
- **python.conf** — 识别并加载 `mod_python` 模块，使网页能够包含用 Python 编写的 Apache 处理器。（安装 `mod_python` 包。）
- **squirmail.conf** — 识别基于 Web 的 SquirrelMail 邮件界面的位置，以便将其集成到你的 Apache Web 服务器中。要查看 SquirrelMail 登录界面，请在浏览器窗口中输入 `http://localhost/webmail`。（安装 squirrelmail 包。）
- **ssl.conf** — 配置 SSL 支持，使 Apache 知道如何提供通过安全连接（https）请求的页面。（安装 `mod_ssl` 包。）
- **subversion.conf** — 加载 `mod_dav_svn` 和 `mod_authz_svn` 模块，以便从 Apache 访问 Subversion 仓库。通过取消该文件中某些行的注释，你可以将 `/home/svnroot` 设置为存放授权文件的位置。（安装 `mod_dav_svn` 包。）
- **webalizer.conf** — 允许你识别谁可以访问 webalizer 数据（关于你网站的统计数据）。（安装 webalizer 包。）
- **wordtrans.conf** — 识别 WordTrans 语言翻译窗口的位置，以便将其集成到你的 Apache Web 服务器中。要查看 WordTrans 登录界面，请在浏览器窗口中输入 `http://localhost/wordtrans`。（安装 `mod_wordtrans` 包。）

这些配置文件在 httpd 服务器启动时会被读取。这些文件中的信息本可以添加到 `httpd.conf` 中。然而，将这些文件放在这里是为了让不同的包能够添加自己的配置设置，而无需 RPM 软件包采用某种自动方法将它们的配置信息添加到 `httpd.conf` 文件中。

## 启动和停止服务器

启动和停止 Apache Web 服务器的程序与许多其他守护进程没有区别。你可以使用 `chkconfig` 命令设置 httpd 服务在启动时运行。

> **交叉参考：** 有关控制守护进程和服务器进程启动与停止的 shell 脚本内部工作原理的详细信息，请参阅第 12 章。

`/etc/init.d/httpd` shell 脚本接受少数几个命令行参数中的任意一个。如果以参数 `start` 调用，httpd 脚本将运行一个主守护进程（由 `root` 拥有），该进程将生成其他守护进程（数量由 `StartServers` 指令指定），这些进程由用户 `apache`（由 `User` 和 `Group` 指令指定）拥有。这些进程负责响应传入的 HTTP 请求。如果以 `stop` 调用，当所有 httpd 进程被终止时，服务器将停止运行。

如果给定时命令行参数 `restart`，脚本将简单地按顺序执行 `stop` 和 `start` 程序。使用 `reload` 作为参数将向主 httpd 守护进程发送挂起信号（-HUP），这会导致其重新读取配置文件并重启所有其他 httpd 守护进程。该 shell 脚本还支持参数 `status`，它将报告守护进程是否正在运行，如果正在运行，还会报告运行中进程的 PID。其他所有命令行参数都会导致错误，并打印用法消息。

Apache 的实际二进制文件 `/usr/sbin/httpd` 支持几个命令行参数，尽管通常使用默认值。可能的命令行参数列在表 21-7 中。

