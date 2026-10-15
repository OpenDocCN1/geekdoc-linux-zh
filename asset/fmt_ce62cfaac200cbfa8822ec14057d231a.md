
httpd 使用 Web 服务器目录下的 lighthttpd 目录，即 `/var/www/lighthttpd`。其配置文件位于 `/etc/lighthttpd`。服务器变量未在 `/etc/sysconfig/lighthttpd` 文件中设置。你可以使用 `/etc/init.d/lighthttpd` 服务脚本来启动和停止服务器，该脚本也可以通过 `system-config-services` 作为 `lighthttpd` 进行管理（系统 | 管理 | 服务）。

```
service lighthttpd start
```

就像 Apache 一样，你可以使用端口 80 的 localhost URL 访问 Web 服务器。

`http://localhost:80`

Lighthttpd 配置文件为 `/etc/lighthttpd/lighthttpd.conf`。该配置文件包含了一系列简单的 Web 配置选项，例如 `server.document-root` 用于 Web 站点文件（`/var/www/lighthttpd` 是默认值），`server.error_log` 用于日志文件，以及 `index-file.names` 用于指定的索引 HTML 文件名。服务器用户名 `server.username` 被设置为 `lightpasswd`。条目也可以是条件性的，用于检查某些值（如虚拟 Web 地址），然后在附加的块中，如果条件成立，则列出选项或条件。

详细文档位于 `/usr/share/doc/lighthttpd` 目录，其中存储了不同模块和功能的文本文件，例如用于增强虚拟主机的 `evhost.txt` 和用于身份验证方法的 `authentication.txt`。检查 `configuration.txt` 文件可以查到带有示例的配置选项的详细说明。

Lightpd 可以使用支持的模块进行轻松扩展。其中几个作为虚拟主机的 `mod_simple-host` 被包含在，尽管它们在 `lighthttpd.conf` 文件中最初都是被禁用的。在文件的 `server.modules` 块中，你会发现列出的被注释掉的基础模块。模块名以 `mod_` 前缀开头，例如 `mod_auth`。删除模块条目上的注释字符 `#` 即可启用模块的加载。Fedora 仓库提供了额外模块的包，包括 FastCGI、用于位置的 GeoIP，以及带有 MySQL 数据库支持的虚拟主机。Lightttpd 模块位于 `/usr/lib/lighthttpd`。

如果你想同时运行 Apache 和 Lightttpd，可以在 `/etc/lighthttpd.conf` 文件中将 Lightttpd 使用的端口改为 `81`。

可以使用 simple-host 选项中的 `server`、`default-host` 和 `document-root`（`mod_simple_host` 模块) 设置简单的虚拟主机。对于增强虚拟主机，Lightttpd 将将 URL 重写为由 `evhost.path-pattern` 选项指定的预定义目录（`mod_evhost` 模块）。

### Apache Web 服务器

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
| `/etc/httpd/conf.d` | 模块配置文件目录，如用于 SSL 的 `ssl.conf`、用于 PHP 的 `php.conf` 和用于欢迎消息的 `welcome.conf` |
| 服务脚本 |  |
| `/etc/rc.d/init/httpd` | Web 服务器守护进程的服务脚本 |
| `/etc/sysconfig/httpd` | Red Hat 和 Fedora Web 服务器守护进程配置选项，供 `httpd` 服务脚本使用 |
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
| `/etc/init.d/httpd` | 为 Fedora 设计的启动、停止和重启服务器的脚本，调用 `apachectl`。由 `system-config-services`、系统 | 管理 | 服务 管理。 |

表 22-3：Apache 管理工具

# Apache 多进程模块：MPM

Apache 现在使用一种使用多进程模块（MPMs）的新型架构，这些模块设计用于使 Apache 适应不同的操作系统，并处理某些多进程操作。对于主 MPM，Linux 系统使用 `prefork` 或 `worker` MPM，而 Windows 则使用 `mpm_win` MPM。`prefork` 是一个标准的 MPM 模块，设计用于兼容旧的 Unix 和 Linux 系统，特别是那些不支持线程的系统。它是 Fedora 默认加载的模块。`worker` MPM 为 Apache 服务器进程实现了线程支持，该功能由 Red Hat 和 Fedora 包含的 Native POSIX 线程库（NPTL）支持。您可以在 Apache 配置文件 `/etc/httpd/httpd.conf` 中为两者配置工作负载参数。

许多曾经存在于 Apache 核心的指令现在被放在相应的模块和 MPM 中。通过这种模块化设计，某些指令已被弃用，例如 `ServerType`。这些模块的配置文件位于 `/etc/httpd/conf.d`。

# 启动和停止 Web 服务器

在大多数系统上，Apache 是作为独立服务器安装并持续运行的。正如第 3 节在 init 脚本讨论中提到的，您的系统会自动启动 Web 服务器守护进程，每当您启动系统时就会调用。名为 `httpd` 的 Web 服务器服务脚本位于 `/etc/rc.d/`。运行此脚本的符号链接位于相应的运行级别（runlevels）中。您可以在运行级别 3 和 5 中找到指向 `/etc/rc.d/init` 的 `S85httpd` 链接，以及 `/etc/rc.d/rc5.d`，您可以使用 `chkconfig` 命令或 System V Init 编辑器设置 `httpd` 服务器（`httpd`）在运行级别 3 和 5 启动 Web 服务器的运行级别。以下命令

```
chkconfig --level 35 httpd
```

您还可以使用 `service` 命令手动启动和停止 `httpd` 服务器。当您测试或修改服务器时，这可能会有所帮助。`stop` 选项停止它，`restart` 选项启动服务器，而 `restart` 将重新启动它。不建议直接杀掉 Web 进程。

```
/sbin/service httpd restart
```

您也可以直接运行 `httpd` 脚本。

`/etc/sysconfig/httpd` 配置文件用于为 `httpd` 服务脚本设置选项。在这里，您可以指定诸如是否使用 `worker` 或 `prefork` MPM 模块。

Apache 还提供了名为 `apachectl`（Apache 控制）的控制工具来管理您的 Web 服务器。通过 `apachectl`，您可以启动、停止和重启服务器：`start` 启动服务器，`stop` 停止，`restart` 重启，以及 `graceful` 优雅地重启。此外，您可以使用 `apachectl` 配合 `config` 参数检查配置文件的语法，位于 `/etc/rc.d/` 目录。记住，`httpd` 是一个调用守护进程的脚本。可以通过 `-d` 选项指定目录。`-f` 选项允许指定配置文件 `httpd.conf`。`-v` 选项显示版本。

```
/usr/sbin/httpd -v
```

# 第 22 章：Web 服务器

要检查您的 Web 服务器，启动 浏览器并输入系统的域名地址。对于系统，输入 `http://localhost`。这应该显示您放置在 Web 根目录下的主页。请先在 `/var/www/html` 目录下放置一个 `index.html` 文件。一旦您的服务器运行，您可以使用 Apache 检查其性能：`ab` 显示服务器可以处理的并发请求。选项包括 `-v`（允许您控制详细程度）和 `-n`。

# 配置

配置指令位于 `httpd.conf` 配置文件中。文档化的 `httpd.conf` 版本自动安装在 `/etc/httpd`。强烈建议您查阅该文件。它包含了 Apache 指令的详细说明和默认项。主配置文件中的任何指令都可以使用目录内的 `.htaccess` 文件按目录进行覆盖。虽然 `.htaccess` 文件最初仅为访问指令设计，但它也可以包含任何资源指令，从而允许 `httpd.conf` 文件中配置 `.htaccess` 文件。

此外，许多为 Apache提供的模块都有自己的配置文件。这些文件位于 `/etc/httpd/conf.d` 目录。

# 使用 system-config-httpd 配置 Apache

您可以使用 Fedora Web 管理工具 `system-config-httpd` 通过桌面界面执行配置任务。选择“系统 | 管理 | 服务器设置 | HTTP”，这将打开 HTTP 配置窗口，具有四个选项卡：主、虚拟主机、服务器和性能调优（见图 22-1）。在每个卡中，您都会看到打开对话框以设置的按钮。点击“帮助”按钮将显示基于 Web 页的参考手册，说明如何使用每个选项卡。

- 在“主（Main）”选项卡上，您可以输入服务器地址、Web 管理员电子邮件地址以及服务器监听的地址。

- 在“虚拟主机（Virtual Hosts）”选项卡上，选择默认虚拟主机并点击“编辑”以设置服务器选项、页面搜索、SSL 支持、日志文件、环境支持和目录的默认设置。要添加虚拟主机，点击“添加”打开一个窗口，在其中输入主机信息，如虚拟主机名和 IP 地址。您可以为虚拟主机选择不同的配置选项卡，例如日志文件

## 第 4 部分：网络服务

- 在“服务器（Server）”选项卡中，您可以设置管理设置，例如 Apache 服务器的用户 ID 和进程 ID 文件，以及用户和组。

- “性能调优（Performance Tuning）”选项卡允许您设置不同的使用限制，例如最大请求数和每个连接的请求数。

![](img/74df054815dc70d661e697bc3d5ff87a_537_0.png)

图 22-1：system-config-httpd 服务器配置

当 Apache 配置工具保存设置时，它将覆盖 Apache 配置文件 `/etc/httpd/conf/httpd.conf`。建议您先为 `httpd.conf` 文件创建一个备份副本，以防您需要恢复发行版为 Apache 创建的原始设置。如果您已经编辑了此文件，将收到一个警告，Apache 配置工具会在 `/etc/httpd/conf/httpd.conf.bak` 中创建一个备份副本。

![](img/74df054815dc70d661e697bc3d5ff87a_537_1.png)

图 22-2：system-config-httpd 性能调优

“服务器（Server）”选项卡设置服务器功能，如服务器的用户和组。“性能调优”选项卡设置连接限制，例如最大连接数和超时时间（见图 22-2）。

“虚拟主机（Virtual Hosts）”面板是您配置特定站点的地方，包括默认站点（见图 22-3）。虚拟主机列出，从“默认虚拟主机”开始。使用“添加（Add）”按钮添加新主机，使用“编辑（Edit）”按钮修改现有主机。“删除（delete）”按钮移除主机。要更改全局设置，点击“编辑默认设置（Edit Default Settings）”按钮。

![](img/74df054815dc70d661e697bc3d5ff87a_538_0.png)

图 22-3：system-config-httpd 虚拟主机

添加或编辑虚拟主机会打开“虚拟主机属性”窗口，其中列有五个选项卡：常规选项（General Options）、页面选项（Page Options）、SSL、日志（Logging）、环境（Environment）和性能（Performance）（见图 22-4）。

![](img/74df054815dc70d661e697bc3d5ff87a_538_1.png)

图 22-4：system-config-httpd 虚拟主机属性，常规选项

在“常规选项”选项卡上，您可以指定主机名、站点目录、管理员地址以及虚拟主机的类型（名称或 IP）。您还可以添加别名（aliases）。

在“页面选项”中，您可以指定将自动搜索并显示的文件类型。这通常是 `index.html` 及其任何变体（如 `index.htm`）。您可以指定自己的。

## 第 4 部分：网络服务

### 顺序（Order）

- 允许所有主机访问此目录

- 在允许列表（Allow list）之前处理拒绝列表（Deny list）

- 在拒绝列表（Deny list）之前处理允许列表（Allow list）

### 选项（Options）

- FollowSymLinks

- Includes

- IncludesNOEXEC

- Indexes

- MultiViews

- SymLinksIfOwnerMatch

让 `.htaccess` 文件覆盖目录

### 目录（Directory:）：

```
/var/www/html
```

帮助 | 取消 确定
