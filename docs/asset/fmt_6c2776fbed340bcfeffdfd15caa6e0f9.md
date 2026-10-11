
# Apache 模块

Apache 之所以强大且灵活的部分原因在于其设计允许通过模块进行扩展。Apache 默认带有许多模块。

为了让你对人们在使用模块做什么有一个直观了解，请访问 `http://modules.apache.org`。在在那里你可以找到如何使用模块扩展 Apache 的信息。一些常见的 Apache 模块包括

- `mod_cgi`：允许在 Web 服务器上执行 CGI 脚本
- `mod_perl`：用于将 Perl 解释器整合到 Web 服务器中
- `mod_aspnet`：为微软的 ASP.NET 引擎提供 ASP.NET 托管接口
- `mod_authz_ldap`：提供通过轻量级访问协议 (LDAP) 数据库验证 Apache 服务器用户的支持
- `mod_ssl`：通过安全套接层 (SSL) 和传输层安全 (TLS) 协议为 Apache 服务器提供强加密
- `mod_ftpd`：允许 Apache 接受 FTP 连接
- `mod_userid`：允许通过 HTTP 从 Web 服务器上的用户目录提供内容

如果你知道某个特定模块（如果该模块足够流行），你可能会发现它已经以 RPM 格式封装，因此可以使用可以使用的 RPM 方法安装它。例如，如果你想在 Web 服务器设置中包含 SSL 模块 `mod_ssl`，在 Fedora 系统上，你可以使用此 Yum 命令自动为你下载并安装：

```
[root@fedora-serverA ~]# yum install mod_ssl
```

或者，你可以前往 Apache 模块项目网站，搜索、下载、编译并安装你需要的模块。

> 确保运行用户存在！如果你从源码编译 Apache，示例配置文件 `httpd.conf` 期望 Web 服务器以守护进程身份运行。虽然该用户在几乎 Linux 发行版中存在，但如果过程中出现问题，你可能需要检查用户数据库 `/etc/passwd` 以确保守护进程用户确实存在。

# 启动和停止 Apache

在大多数 Linux 发行版中启动和停止 Apache 非常简单。在 Fedora 系统或任何其他 Red Hat 系上启动 Apache，使用此命令：

```
[root@fedora-serverA ~]# service httpd start
```

要停止 Apache，输入此命令：

```
[root@fedora-serverA ~]# service httpd stop
```

# Linux 管理：入门指南

对 Web 服务器进行配置更改并需要重启 Apache 后，输入

```
[root@serverA ~]# service httpd restart
```

> 提示 在运行 OpenSUSE 或 SLE（SUSE Linux 企业版）的系统上，分别启动和停止 Web 服务器的命令分别为：
`[opensuse-serverA ~]# rcapache2 start`

`[opensuse-serverA ~]# rcapache2 stop`

> 提示 在像 Ubuntu 这样的 Debian 系统上，可以通过运行启动 Apache：
`nyang@ubuntu-serverA:-$ sudo /etc/init.d/apache2 start`
运行以下命令可以停止 Apache 进程
`nyang@ubuntu-serverA:-$ sudo /etc/init.d/apache2 stop`

# 在启动时启动 Apache

安装 Web 服务器后，如果你发现该 Web 服务是你希望系统始终提供的服务，那么你将需要配置系统在系统重启之间自动为你启动该服务。在一个运行很长时间且不需要重启的系统中，很容易忘记这样做，因为如果你由于无关问题而必须关闭系统，你可能会困惑为什么 Web 服务器之前运行得完美无缺，现在却在启动机器时失败了。所以，在配置服务的早期阶段处理这个问题是一个良好的习惯。

大多数 Linux 发行版都提供了 `chkconfig` 工具，可用于控制哪些服务在什么级别启动。
要查看 Web 服务器配置为在什么级别启动，输入：

```
[root@fedora-serverA ~]# chkconfig --list httpd

httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

此输出显示 Web 服务器在默认状态下未配置在任何运行级别（runlevel）下启动。要更改并让 Apache 在运行级别 2、3、4 和 5 下自动启动，输入：

```
[root@fedora-serverA ~]# chkconfig httpd on
```

在 Ubuntu 中，你可以使用 `sysv-rc-conf` 或 `update-rc.d` 工具来管理 Apache 启动的运行级别。

# 第 18 章：Apache Web 服务器

> 注意 以防你正在使用的是从源码安装的 Apache 版本，你应该意识到，除非你显式告知该工具，否则 `chkconfig` 工具将不知道你 Web 服务器的启动和停止脚本。而且，你将不得不求助于一些技巧来配置主机系统在系统重启期间自动调起 Web 服务器。你可以轻松地从另一个系统获取现有脚本（通常来自 `/etc/init.d/` 目录），并对其进行修改以反映你自定义 Apache 设置的正确路径（例如 `/usr/local/http/`）。现有脚本可能被命名为 `httpd` 或 `apache2`。

# 测试你的安装

你可以使用默认主页对安装进行快速测试。要执行此操作，请使用以下命令确认 Web 服务器已启动运行：

```
[root@serverA httpd-2.2.8]# service httpd status

httpd (pid 31090 31089 31084 31083 31081) is running...
```

在我们的示例 Fedora 系统上，Apache 自带一个页面，会提供给默认主页（例如 `index.html` 或 `index.html`）的访问者。当没有默认主页时，显示给访问者的文件是 `/var/www/error/noindex.html`。

> 提示 如果你使用的是从源码构建的 Apache 版本，则提供 Web 页面的工作目录是 `<PREFIX>/htdocs`。例如，如果你的安装前缀是 `/usr/local/httpd/`，那么页面默认位于 `/usr/local/httpd/htdocs` 下。

要检查你的 Apache 安装是否成功，只需访问你机器上的 Web 服务器。要执行此操作，只需在 浏览器的地址栏中输入 `http://localhost`（或 Internet协议版本 6 [IPv6] 等效项 `http://[::]/`）。你应该能看到一个页面，上面显示类似于“你的 Apache 服务器在站点运行正常”之类。如果没有，请回溯你的 Apache 安装步骤，确保在此过程中没有遇到任何错误。

# 配置 Apache

Apache 支持丰富的配置选项，这些选项非常合理且易于遵循。这使得在各种配置下设置 Web 服务器成为了一项简单任务。
本节将介绍基础配置。默认配置实际上非常好，而且（你可能不信）开箱即用，如果默认设置对你来说可以，只需创建你的超文本标记语言（HTML）文档即可！Apache 允许多种自定义。在我们创建一个简单的 Web 页面之后，我们将展示如何在 Apache 配置文件中进行常见的自定义。

# 创建简单的根级别页面

如果你愿意，可以立即在 `/var/www/html` 目录中为 Apache 添加文件以创建顶级页面（对于源码安装，目录将是 `/usr/local/httpd/htdocs`）。放置在该目录中的任何文件必须是全球可读的。

如前所述，Apache 的默认 页面是 `index.html`。让我们查看创建和更改默认主页，使其显示为“Welcome to serverA.example.org.”。命令如下：

```
[root@serverA ~]# cd /var/www/html/

[root@serverA #] echo "Welcome to serverA.example.org" >> index.html

[root@serverA #]# chmod 644 index.html
```
