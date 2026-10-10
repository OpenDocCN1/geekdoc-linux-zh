
Lightttpd 配置文件为 `/etc/lighthttpd/lighthttpd.conf`。该配置文件包含了一系列简单的 Web 配置选项，例如 `server.document-root` 用于 Web 站点文件（`/var/www/lighthttpd` 是默认值），`server.error_log` 用于日志文件，以及 `index-file.names` 用于指定的索引 HTML 文件名。服务器用户名 `server.username` 被设置为 `lightpasswd`。条目也可以是条件性的，用于检查某些值（如虚拟 Web 地址），然后在附加的块中，如果条件成立，则列出选项或条件。

详细文档位于 `/usr/share/doc/lighthttpd` 目录，其中存储了不同模块和功能的文本文件，例如用于增强虚拟主机的 `evhost.txt` 和用于身份验证方法的 `authentication.txt`。检查 `configuration.txt` 文件可以查到带有示例的配置选项的详细说明。

Lightpd 可以使用支持的模块进行轻松扩展。其中几个作为虚拟主机的 `mod_simple-host` 被包含在，尽管它们在 `lighthttpd.conf` 文件中最初都是被禁用的。在文件的 `server.modules` 块中，你会发现列出的被注释掉的基础模块。模块名以 `mod_` 前缀开头，例如 `mod_auth`。删除模块条目上的注释字符 `#` 即可启用模块的加载。Fedora 仓库提供了额外模块的包，包括 FastCGI、用于位置的 GeoIP，以及带有 MySQL 数据库支持的虚拟主机。Lightttpd 模块位于 `/usr/lib/lighthttpd`。

如果你想同时运行 Apache 和 Lightttpd，可以在 `/etc/lighthttpd.conf` 文件中将 Lightttpd 使用的端口改为 `81`。

可以使用 simple-host 选项中的 `server`、`default-host` 和 `document-root`（`mod_simple_host` 模块) 设置简单的虚拟主机。对于增强虚拟主机，Lightttpd 将将 URL 重写为由 `evhost.path-pattern` 选项指定的预定义目录（`mod_evhost` 模块）。

## Apache Web 服务器

Apache Web 服务器是由 Apache Server Project 开发和维护的全功能 HTTP（Web）服务器。该项目的目标是提供一个可靠、高效且易于扩展的 Web 服务器，并根据自身的 Apache 软件许可证提供免费的开源代码。服务器软件包括守护进程、配置文件、管理工具和文档。Apache Server Project 由一个核心志愿者小组维护，并受到全球许多贡献者的支持。Apache Server Project 是目前由 Apache 软件基金会（原 Apache 软件基金会）支持的项目之一。

Apache 最初基于在伊利诺伊大学厄巴纳-香槟分校开发的 NCSA Web 服务器。Apache 已经成为最流行的 Web 服务器之一。Apache 在 `http://httpd.apache.org` 提供在线支持和文档。虽然最初是为 Linux 和 Unix 开发的，但 Apache 从此已变为跨平台，包括 Windows 和 OS/2。Apache 支持许多项目，包括库、框架和服务器应用程序。

Apache Server Project 由一个核心志愿者小组维护，并受到全球许多贡献者的支持。Apache Server Project 是目前由 Apache 软件基金会（原 Apache 软件基金会）支持的项目之一。

Apache Server Project 包括守护进程、配置文件、管理工具和文档。Apache 支持 Java 软件开发。该项目的目标是提供一个可靠、高效且易于扩展的 Web 服务器，并根据自身的 Apache 软件许可证提供免费的开源代码。

| 站点目录 | 描述 |
| --- | --- |
| `/var/www/html` | 站点文件 |
| `/var/www/cgi-bin` | CGI 程序文件 |
| `/var/www/html/manual` | Apache 服务器手册 |
| 配置文件 |  |
| `.htaccess` | 目录配置文件；htaccess 文件包含控制其所在目录内访问的指令 |
| `/etc/httpd/conf` | Apache Web 服务器文件目录 |
| `/etc/httpd/conf/httpd.conf` | Apache Web 服务器配置文件 |
| `/etc/httpd/conf.d` | 模块配置文件目录，如用于 SSL 的 ssl.conf、用于 PHP 的 php.conf 和用于欢迎消息的 welcome.conf |
| 服务脚本 |  |
| `/etc/rc.d/init/httpd` | Web 服务器守护进程的服务脚本 |
| `/etc/sysconfig/httpd` | Red Hat 和 Fedora Web 服务器守护进程配置选项，供 httpd 服务脚本使用 |
| 应用和模块文件 |  |
| `/usr/sbin` | Apache Web 服务器程序文件和工具的位置 |
| `/usr/share/doc/` | Apache Web 服务器文档 |
| `/var/log/http` | Apache 日志文件的位置 |
| `/etc/httpd/modules` | Apache Apache 模块目录，链接到 `/usr/lib/httpd/modules` |
| `/etc/httpd/run` | 存储 Apache 进程 ID 的目录，链接到 `/var/run` |

表 22-2：Apache Web 服务器文件和目录

# Linux 安装 Apache

在初始安装 Linux 系统时，您的 Linux 发行版通常会提供安装 Apache 服务器的选项。所有必要的目录和配置文件都会自动为您生成。之后，每当你运行 Linux 时，您的系统已经是一个功能完备的网站。每次启动系统时，Web 服务器都会启动并持续运行。在大多数发行版中，为您的网站数据文件保留的目录是 `/var/www/html`。将您的 Web 页面放置在此目录或任何子目录中。您的系统已经配置好作为 Web 服务器运行。当您需要执行任何网络服务器配置，并为远程用户配置文件和目录时，无需进行任何其他操作。您的网站已连接到网络，远程用户可以访问它。

Web 服务器通常在 `/var/www` 目录下设置您的网站。它还设置了几个用于管理网站的目录。`/var/www/cgi-bin` 目录托管 CGI 脚本，`/var/www/html/manual` 处理 HTML 格式的 Apache 手册。您可以使用浏览器查看它。您的 Web 页面应该放置在 `/var/www/html` Web 主页中。您的配置文件位于不同的目录 `/etc/httpd/conf`。

Apache 还安装了如 `apachectl` 等管理应用程序用于启动和停止服务器。`/etc/init.d/httpd` 脚本设计用于安全运行 `apachectl`，并应用于手动启动和停止服务器。Apache 还通过 `system-config-services` 在系统启动或关闭时启动和停止 Web 服务器。您可以使用 `system-config-httpd` 配置您的 Web 服务器，可以通过“系统 | 管理 | 服务器设置 | HTTP”进行访问。表 22-3 列出了某些应用程序。

```
http://httpd.apache.org/docs/2.0/programs/ 可获取完整列表。
```

| 应用程序 | 说明 |
| :--- | :--- |
| `apachectl` | 控制启动、停止和重启 apache 服务器 |
| `system-config-httpd` | 用于 Apache Web 服务器的 Fedora 桌面配置工具 |
| `htcacheclean` | 限制网站磁盘缓存的大小 |
| `ab` | 用于网站性能基准的工具 |
| `htpasswd` | 管理网站目录的密码 |
| `/etc/init.d/httpd` | 为 Fedora 设计的启动、停止和重启服务器的脚本，调用 apachectl。由 system-config-services、系统 | 管理 | 服务 管理。 |

表 22-3：Apache 管理工具

# Apache 多进程模块：MPM
