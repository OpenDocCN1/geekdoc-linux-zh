

NoCache 指令包含一个由空格分隔的列表，其中包括 IP 地址、主机名或主机名中的关键字，这些条目对应的文档不应被缓存。

如果你取消注释前面的 Cache 行，缓存服务器将表现如下：

- 缓存文件位于 `/var/cache/mod_proxy`。
- 缓存大小限制为 500KB。

你可能希望允许一个更大的 `CacheSize`，并可能设置一个较短的 `CacheGcInterval`，但除此以外，提供的值是合理的。`CacheGcInterval` 的值可以是一个浮点数（例如，1.25 表示 75 分钟）。

## 配置虚拟主机

如果你只有一台 Web 服务器计算机，但希望使用这台计算机服务多个域名，你可以设置 Apache 进行虚拟主机配置。使用基于名称的虚拟主机，单个 IP 地址可以是同一台计算机上多个域名的访问点。使用基于 IP 的虚拟主机，每个虚拟主机都有一个不同的 IP 地址，这是通过为机器配置多个网络接口来实现的。

在使用虚拟主机时，当请求通过你计算机上的特定 IP 地址从 Web 浏览器进入你的 Apache 服务器时，Apache 会检查被请求的域名，并显示与该域名关联的内容。作为支持虚拟主机的 Web 服务器的管理员，你必须确保该虚拟服务器所需配置的所有内容都已正确设置（例如，定义 Web 内容位置、日志文件、管理联系人等）。

虚拟主机通过 `VirtualHost` 标签定义。与虚拟主机相关的信息在 `/etc/httpd/conf/httpd.conf` 文件中，如下面的代码所示：

```
### Section 3: Virtual Hosts
...
# VirtualHost example:
# Almost any Apache directive may go into a VirtualHost container.
# The first VirtualHost section is used for requests without a known
# server name.
#
#<VirtualHost *:80>
#   ServerAdmin webmaster@dummy-host.example.com
#   DocumentRoot  /www/docs/dummy-host.example.com
#   ServerName    dummy-host.example.com
#   ErrorLog  logs/dummy-host.example.com-error_log
#   CustomLog logs/dummy-host.example.com-access_log common
#</VirtualHost>
```

以下示例列出了虚拟主机指令，这些指令允许你在同一台计算机上托管域名 `handsonhistory.com` 和 `linuxtoys.net`：

```
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

要实验虚拟主机，你可以将新的主机名添加到本地的 /etc/hosts 文件，并指向你的本地主机 IP 地址。例如：

```
127.0.0.1 www.linuxtoys.net
```

如果你看到的是你为虚拟主机设置的内容，而不是 Fedora 错误页面或你设置的默认内容，那么你可能已经正确设置了虚拟主机。

## 配置模块和相关服务 (/etc/httpd/conf.d/*.conf)

任何需要特殊配置的模块通常会在 /etc/httpd/conf.d/ 目录中有一个配置文件（.conf 文件）。以下是该目录中可能包含的模块化配置文件，以及使用这些文件及其相关软件包的一些方法（使用 yum install package 安装每个你想安装的软件包）：

- **auth_kerb.conf** — 配置通过 Web（HTTP）连接的 Kerberos 身份验证。该文件中的示例建议在 SSL 连接上使用该 Kerberos 身份验证。（安装 mod_auth_kerb 软件包。）
- **auth_mysql.conf** — 配置基于你添加到 MySQL 数据库中的数据的身份验证。文件中的注释描述了如何设置数据库，然后使用它在进行用户或组身份验证之前允许客户端访问你的 Web 内容。（安装 mod_auth_mysql 软件包。）
- **auth_pgsql.conf** — 配置基于 PostgreSQL 数据库中数据的身份验证。（安装 mod_auth_pgsql 软件包。）
- **authz_ldap.conf** — 配置访问 LDAP 数据库以进行用户身份验证。（安装 mod_auth_ldap 软件包。）
- **htdig.conf** — 识别可以在你的 Web 站点上使用的 htdig 搜索内容的位置（/usr/share/htdig 是默认位置）。要从 Web 浏览器查看 htdig 搜索屏幕，请输入 http://localhost/htdig。htdig 系统允许你设置用于索引和搜索你的 Web 站点或公司内网网的工具。这对你的 Web 服务器来说是可选的。（安装 htdig-web 软件包。）
- **mailman.conf** — 设置 mailman 邮件列表服务器软件，允许从 Apache 提供邮件列表存档等功能。（安装 mailman 软件包。）
- **manual.conf** — 定义服务器上不同语言的 Apache 手册位置（/var/www/manual）。在浏览器窗口中键入 http://localhost/manual。（安装 httpd-manual 软件包。）
- **mrtg.conf** — 定义每日 mrtg 输出的位置（/var/www/mrtg），用于跟踪网络流量。在浏览器窗口中键入 http://localhost/mrtg。（安装 mrtg 软件包。）
- **perl.conf** — 识别并加载 mod_perl 模块，以便你的 Web 页面可以包含 Perl 代码。（安装 mod_perl 软件包。）
- **php.conf** — 识别并加载 libphp5 模块，以便你的 Web 页面可以包含 PHP 脚本语言。还有一个 DirectoryIndex 设置，允许你添加到目录中的 index.php 文件作为目录索引提供服务。（安装 php 软件包。）
- **python.conf** — 识别并加载 mod_python 模块，以便 Web 页面可以包含用 Python 编写的 Apache 处理器。（安装 mod_python 软件包。）
- **squirrelmail.conf** — 识别基于 Web 的 SquirrelMail 邮件接口的位置，以便将其整合到你的 Apache Web 服务器中。要查看 SquirrelMail 登录屏幕，请在浏览器窗口中键入 http://localhost/webmail。（安装 squirrelmail 软件包。）
- **ssl.conf** — 配置 SSL 支持，以便 Apache 知道如何提供通过安全连接（https）请求的页面。（安装 mod_ssl 软件包。）
- **subversion.conf** — 加载 mod_dav_svn 和 mod_authz_svn 模块，以便从 Apache 访问 Subversion 仓库。通过取消此文件中的行的注释，你可以将 /home/svnroot 设置为存放授权文件的位置。（安装 mod_dav_svn 软件包。）
- **webalizer.conf** — 允许你识别谁可以访问 webalizer 数据（关于你的 Web 站点的信息统计）。（安装 webalizer 软件包。）
- **wordtrans.conf** — 识别 WordTrans 语言翻译窗口的位置，以便将其整合到你的 Apache Web 服务器中。要查看 WordTrans 登录屏幕，请在浏览器窗口中键入 http://localhost/wordtrans。（安装 wordtrans 软件包。）

这些配置文件在 httpd 服务器启动时读取。这些文件中的信息本可以添加到 `httpd.conf` 中。但是，将这些文件放在这里，是为了让不同的软件包能够添加自己的配置设置，而不需要 RPM 软件包采用某种自动化方法将其配置信息添加到 `httpd.conf` 文件中。

## 启动和停止服务器

启动和停止 Apache Web 服务器的步骤与其他许多守护进程没有区别。你可以使用 `chkconfig` 命令设置 httpd 服务在启动时运行。

> **交叉引用：** 请参阅第 11 章了解有关控制守护进程和服务器进程启动与停止的 shell 脚本内部工作机制的详细信息。

`/etc/init.d/httpd` shell 脚本接受少量命令行参数中的任何一个。如果以参数 **start** 调用，`httpd` 脚本将运行一个主守护进程（由 **root** 拥有），该进程将生成其他守护进程（数量等于 `StartServers` 指令指定的数量），这些进程由用户进程（来自 **User** 和 **Group** 指令）拥有。这些进程负责响应传入的 HTTP 请求。如果以 **stop** 调用，随着所有 `httpd` 进程的终止，服务器将被关闭。

如果给定命令行参数 **restart**，脚本将依次执行 **stop** 和 **start** 过程。使用 **reload** 作为参数将向主 `httpd` 守护进程发送挂起信号（-HUP），这将导致其重新读取其配置文件并重启所有其他 `httpd` 守护进程。shell 脚本还支持参数 **status**，它将报告守护进程是否正在运行，如果正在运行，则报告正在运行的进程的 PID。所有其他命令行参数都会导致错误并打印使用信息。

Apache 的实际二进制文件 `/usr/sbin/httpd` 支持几个命令行参数，尽管通常使用默认值。可能的命令行参数列在表 20-7 中。

### 表 20-7: httpd 的命令行参数

| 参数 | 描述 |
| :--- | :--- |
| `-c directive` | 读取配置文件，然后处理该指令。这可能覆盖配置文件中该指令的定义。 |
| `-C directive` | 处理该指令，然后读取配置文件。该指令可能会改变配置文件的评估，但也可能被配置文件中的另一个定义覆盖。 |
| `-d directory` | 使用目录作为 ServerRoot 指令，指定模块、配置和日志文件目录的位置。 |
| `-D parameter` | 定义参数，用于 IfDefine 中的条件求值 |

