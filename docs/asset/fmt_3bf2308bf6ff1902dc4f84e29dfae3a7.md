
虽然 ASCII 上传默认是禁用的，但你可以启用此功能。ASCII 上传涉及某些安全风险，默认情况下是关闭的。但是，如果你正在上传大型文本文件，你可能会在特殊情况下想要启用它们。使用 `ascii_upload_enable` 来允许 ASCII 上传。

# 匿名用户权限

你还可以允许匿名用户上传和删除文件，以及创建或删除目录。使用 `anon_upload_enable` 选项启用匿名用户上传。要允许匿名用户重命名或删除他们的文件，你设置 `anon_other_write_enable` 选项。要让他们也能创建目录，你设置 `anon_mkdir_write_enable` 选项。

### 匿名上传设置

`anon_upload_enable=YES`
`anon_other_write_enable=YES`
`anon_mkdir_write_enable=YES`

`anon_world_readable_only` 选项将使上传的文件变为只读（可下载），并限制对创建这些文件的用户的写入访问权限。只有上传文件的用户才能删除该文件。

所有上传的文件都归匿名 FTP 用户所有。你可以让文件归其他用户所有，从而增加潜在的安全性。实际上，拥有上传文件的实际用户会对匿名用户隐藏。要启用此选项，请使用 `chown_uploads` 并使用 `chown_username` 指定新用户。切勿将该用户设置为 root 等管理员用户。

`chown_uploads=YES`
`chown_username=myftpfiles`

上传目录本身应授予其他用户写入权限。

```
# chmod 777 /var/ftp/upload
```

你可以通过 `anon_mask` 选项控制用户对文件的访问类型，为上传的文件设置默认的读/写权限。默认值为 `077`，仅授予所有者读/写权限（600）。若要允许所有用户读取访问，应将 umask 设置为 022，其中 2 关闭写入权限但设置读取权限（644）。值 000 允许所有用户进行读和写。

## 连接时间限制

为了更有效地控制服务器负载，你可以为空闲用户和失败的传输设置时间限制。`idle_session_timeout` 选项将在指定时间后切断空闲用户连接，而 `data_connection_timeout` 将切断失败的数据连接。默认值如下所示：

`idle_session_timeout=600`
`data_connection_timeout=120`

## 消息

`dir_message_enable` 选项允许在用户访问该目录时显示存储在目录 `.message` 文件中的消息。`ftpd_banner` 选项允许你设置自己的 FTP 登录消息。默认值如下所示：

`ftpd_banner=Welcome to blah FTP service.`

## 日志记录

一组 `xferlog` 选项用于控制日志记录。你可以启用日志记录，并指定文件的格式和位置。

`xferlog_enable=YES`

使用 `xferlog_file` 选项指定你要使用的日志文件。默认值如下所示：

`xferlog_file=/var/log/vsftpd.log`

## vsftpd 访问控制

某些选项控制对 FTP 站点的访问。如前所述，`anonymous_enable` 选项允许匿名用户访问，而 `local_enable` 允许本地用户登录其帐户。

### 拒绝访问

`deny_email_enable` 选项允许拒绝匿名用户的访问，而 `banned_email` 文件选项指定包含这些用户电子邮件地址的文件（通常是 `vsftpd.banned`）。`vsftpd.ftpusers` 文件列出了永远无法访问的用户。这些通常是系统用户，如 root、mail 和 nobody。有关 vsftpd 文件的列表，请参见表 22-3。

### 用户访问

`userlist_enable` 选项控制用户的访问，拒绝 `userlist_file` 选项指定的文件（通常是 `vsftpd.user_list`）中列出的用户的访问。相反，如果你想将访问限制在少数特定用户，你可以更改 `vsftpd.user_list` 文件的含义和用法，使其指示仅允许访问的用户，而不是被拒绝访问的用户。为此，你需要将 `userlist_deny` 选项设置为 NO（其默认值为 YES）。只有列在 `vsftpd.user_list` 文件中的用户才会被授予访问 FTP 站点的权限。

### 用户限制

`chroot_list_enable` 选项控制本地用户的访问，允许他们仅访问其主目录，同时限制系统访问。`chroot_list_file` 选项指定列出允许访问的用户的文件（通常是 `vsftpd.chroot`）。你可以通过 `chroot_local_user` 选项允许所有本地用户访问。如果设置此选项，则 `chroot_list_file` 指定的文件将具有相反的含义，列出不允许访问的用户。在下面的示例中，本地用户的访问仅限于列在 `vsftpd.chroot_list` 中的用户：

`chroot_list_enable=YES`
`chroot_list_file=/etc/vsftpd.chroot_list`

表 22-3 **vsftpd** 文件

| 文件 | 描述 |
| :--- | :--- |
| `vsftpd.ftpusers` | 始终拒绝访问的用户 |
| `vsftpd.user_list` | 拒绝访问的指定用户（如果 `userlist_deny` 为 NO，则允许访问） |
| `vsftpd.chroot_list` | 允许访问的本地用户（如果 `chroot_local_user` 开启，则拒绝访问） |
| `/etc/vsftpd/vsftpd.conf` | vsftpd 配置文件 |
| `/etc/pam.d/vsftpd` | PAM vsftpd 脚本 |
| `/etc/rc.d/init.d/vsftpd` | vsftpd 服务器服务脚本，独立运行 |
| `/etc/xinetd.d/vsftpd` | Xinetd vsftpd 服务器脚本 |

## 用户身份验证

`vsftpd` 服务器使用 PAM 服务来验证通过 FTP 远程访问其帐户的本地用户。在 `vsftpd.conf` 文件中，使用 `pam_service_name` 选项指定服务器使用的 PAM 脚本。

`pam_service_name=vsftpd`

在 `/etc/pam.d` 目录中，你将找到一个名为 `vsftpd` 的 PAM 文件，其中包含控制对 `vsftpd` 服务器访问的条目。PAM 当前设置为验证拥有有效帐户的用户，并拒绝访问 `/etc/vsftpd.ftpusers` 文件中的用户。默认的 `/etc/pam.d/vsftpd` 文件如下所示：

```
#%PAM-1.0
auth required pam_listfile.so item=user sense=deny file=/etc/vsftpd.ftpusers onerr=succeed
auth required pam_stack.so service=system-auth
auth required pam_shells.so
account required pam_stack.so service=system-auth
session required pam_stack.so service=system-auth
```

## 命令访问

`vsftpd` 严格限制命令的使用。用于列出文件的 `ls` 命令的大多数选项均不被允许。仅支持星号文件匹配操作（参见第 8 章）。要启用对子目录中文件的递归列表，你必须通过将 `ls_recursive` `enable` 选项设置为 YES 来启用使用 `-R` 选项。某些客户端，例如 `ncftp`（参见第 14 章），将假设已启用递归选项。

## vsftpd 虚拟主机

虽然 `vsftpd` 本身不具备此功能，但你可以配置和设置 `vsftpd` 服务器以支持虚拟主机。*虚拟托管*是指单个 FTP 服务器表现得好像拥有两个或更多 IP 地址。然后可以使用几个 IP 地址访问同一台服务器。服务器将为每个主机使用单独的 FTP 用户目录和文件。对于 `vsftpd`，这涉及手动为每个虚拟主机创建单独的 FTP 用户和目录，以及在 `/etc/vsftpd` 目录中为每个虚拟主机创建单独的 `vsftpd` 配置文件。`vsftpd` 配置为作为独立服务运行。其 `/etc/rc.d/init.d/vsftpd` 启动脚本将自动搜索并读取 `/etc/vsftpd` 目录中列出的任何配置文件。

另一方面，如果你希望将 `vsftpd` 作为 `xinetd` 服务运行，你需要在 `/etc/xinetd.d` 目录中为每个主机创建单独的 `xinetd` 服务脚本。实际上，你为每个单独的虚拟主机并行运行了几个 `vsftpd` 服务。以下示例为 FTP 服务器使用两个 IP 地址：

- 首先，为每个主机创建一个 FTP 用户。为每个主机创建目录（你可以使用已为其中一个用户设置的目录）。例如，对于第一个虚拟主机，你可以使用 `FTP-host1`。务必设置 root 所有权和适当的权限。

```
useradd -d /var/ftp-host1 FTP-host1
chown root.root /var/ftp-host1
chmod a+rx /var/ftp-host1
umask 022
mkdir /var/ftp-host1/pub
```

- 在 `/etc/xinetd.d` 目录中设置两个相应的 vsftpd 服务脚本。`/usr/share/doc` 中的 vsftpd 目录包含一个 xinetd 示例脚本 `vsftpd.xinetd`。在每个脚本中，输入 bind 命令以指定服务器响应的 IP 地址。

```
bind 192.168.0.34
```

- 在相同的脚本中，输入 `server_args` 条目以指定要使用的配置文件的名称。

```
server_args = vsftpd-host1.conf
```

- 在 `/etc/vsftpd` 目录中，为每个虚拟主机创建单独的配置文件。在每个文件中，使用 `ftp_username` 条目指定你为每个主机创建的 FTP 用户。

```
ftp_username = FTP-host1
```

### vsftpd 虚拟用户

可以通过利用 PAM 来验证授权用户来实现虚拟用户。实际上，你正在允许某些用户访问，而无需在 FTP 服务器系统上实际为他们设置帐户。首先创建一个 PAM 登录数据库文件，并与 `/etc/pam.d` 目录中的 PAM 文件一起使用，该文件将访问数据库。然后创建虚拟 FTP 用户以及虚拟用户将访问的相应目录（有关更详细的信息，请参见 vsftpd.beasts.org 上的 vsftpd 文档）。然后在 `vsftpd.conf` 文件中，你可以禁用匿名 FTP：

```
anonymous_enable=NO
local_enable=YES
```

然后启用来宾访问：

```
guest_enable=YES
guest_username=virtual
```

# Web 服务器：Apache

Linux 发行版为您的系统提供了几种可供使用的 Web 服务器。主要的 Web 服务器是 Apache，它几乎已成为 Red Hat Linux 和 Fedora 发行版的标准 Web 服务器。这是一个非常强大、稳定且配置相对简单的系统。还有其他 Web 服务器可用，例如 Tux。Tux 体积较小，但速度非常快，在处理静态 Web 数据时效率极高。Red Hat 和 Fedora Linux 为这些 Web 服务器提供了默认配置，使得它们在安装后即可使用。

Apache 免费支持基于 OpenSSL 的全安全 shell 加密。还有仅提供于收费许可下的专有加密产品。除了直接获取许可外，您只需购买包含此类许可的商业版 Apache 即可，例如 Stronghold 和 Raven (www.covalent.net)。以前，这种限制仅适用于美国境内的 RSA 技术使用，因为该技术曾在此处拥有专利。RSA 专利现已过期，RSA 现可用于 OpenSSL 等自由分发的产品中。

### Tux

Tux，即 Red Hat Content Accelerator，是一个旨在在 Linux 内核中高速运行的静态内容 Web 服务器。实际上，它运行在内核空间，因此响应时间比 Apache 等标准用户空间 Web 服务器快得多。作为内核空间服务器，Tux 可以非常高效地处理图像等静态内容。同时，它可以与 Apache 等用户空间 Web 服务器协作，提供 CGI 程序等动态内容。Tux 甚至可以利用缓存来存储以前生成的动态内容，并将其当作静态内容使用。与用户空间 Web 服务器协作的能力使您可以将 Tux 用作主 Web 服务器。Tux 无法处理的任何请求，都会转交给用户空间 Web 服务器处理。

> **注意** Tux 基于 GNU 通用公共许可证免费分发，并包含在许多发行版中。

Tux 配置文件位于 `/proc/sys/net/tux`。在此处输入 `serverport`、`max_doc_size` 和 `logfile` 等参数（有关详细列表，请查阅位于 www.redhat.com/docs/manuals/tux 的 Tux 参考手册）。默认值已经输入；`serverport`、`clientport` 和 `documentroot` 是必须设置的必填参数。

- `serverport` 是 Tux 将使用的端口——如果是主 Web 服务器，则为 80。
- `clientport` 是与其协作的用户空间 Web 服务器（如 Apache）使用的端口。
- `documentroot` 指定 Web 文档的根目录（在 Red Hat 和 Fedora 上为 `/var/www/html`）。

理想情况下，Tux 运行为主 Web 服务器，而 Apache 运行次级 Web 服务器。为了配置 Apache 与 Tux 协同工作，需要将 Apache `httpd.conf` 文件中的端口条目从 80 更改为 8080。

您可以使用 `service` 命令和 `/etc/rc.d/init.d/tux` 脚本启动、停止和重新启动服务器。诸如 `DOCROOT` 等多个参数可以作为该 Tux 命令的参数指定。您可以将它们输入到 `/etc/sysconfig/tux` 文件中。

> **注意** 您还可以将 Tux 用作 FTP 服务器。在 `/proc/sys/net/tux` 目录中，您将文件 `serverport` 的内容更改为 21，`application_protocol` 更改为 1，`nonagle` 更改为 0，然后重启 Tux。在文档根目录中使用 `generatetuxlist` 命令生成 FTP 目录列表。

### 替代 Web 服务器

可用于 Linux 的其他 Web 服务器包括 Stronghold Enterprise Server 和 Apache-SSL 服务器。此处提供了一个列表。

- Apache-SSL (www.apache-ssl.org) 是一个基于 Apache 和 OpenSSL (www.openssl.org) 的加密 Web 服务器。
- lighttpd (www.lighttpd.net) 是一个小型、极快的 Web 服务器，包含在 Fedora 中。
- Sun Java System Web 服务器 (www.sun.com) 具备 Java 开发支持和安全性功能。
- Zope 应用服务器 (www.zope.org) 是一个开源 Web 服务器，集成了安全性、基于 Web 的管理和开发以及数据库接口功能。它由 Zope Corporation 开发，该公司还开发了 Python 编程语言。
- Stronghold Enterprise Server (www.redhat.com/software/stronghold) 是 Apache Web 服务器的商业版本，具有改进的安全性和管理工具。
- Netscape Enterprise Server (enterprise.netscape.com)，作为 Netscape 安全解决方案的一部分，具备基于开放标准的高性能特性。
- 您也可以使用原始的 NCSA Web 服务器，尽管它已不再处于开发状态且不再受支持 (hoohoo.ncsa.uiuc.edu)。

# Apache Web 服务器

Apache Web 服务器是一个功能齐全、免费的 HTTP (Web) 服务器，由 Apache 服务器项目开发和维护。该项目的目标是提供一个可靠、高效且易于扩展的 Web 服务器，其免费的开源代码在其自己的 Apache 软件许可证下提供。服务器软件包括服务器守护进程、配置文件、管理工具和文档。Apache 服务器项目由核心志愿者程序员团体维护，并得到全球众多贡献者的支持。Apache 服务器项目是目前由 Apache 软件基金会（前身为 Apache 小组）支持的多个项目之一。该非营利组织为各种 Apache 开源软件项目提供财务、法律和组织支持，包括 Apache HTTPD 服务器、Java Apache、Jakarta 和 XML-Apache。Apache 软件基金会的网站是 www.apache.org。表 23-1 列出了各种与 Apache 相关的网站。

Apache 最初基于位于伊利诺伊大学厄巴纳-香槟分校国家超级计算应用中心 (NCSA) 开发的 NCSA Web 服务器。Apache 后来已发展成为独立于自身的服务器，并已成为使用最广泛的 Web 服务器之一。尽管最初是为 Linux 和 Unix 系统开发的，但 Apache 已成为跨平台应用程序，拥有 Windows 和 OS/2 版本。Apache 在 httpd.apache.org 上为其 Web 服务器提供在线支持和文档。服务器安装时还附带提供基于 HTML 的手册。您可以使用 Apache 配置工具轻松配置您的 Apache 服务器。它适用于任何 X 窗口系统窗口管理器，包括 GNOME 和 KDE。此外，您还可以使用 Comanche 配置工具。Webmin conf 也提供 Apache 配置支持。

### Java：Apache Jakarta 项目

Apache Jakarta 项目支持开源 Java 软件的开发；其网站位于 jakarta.apache.org。目前，Jakarta 项目支持许多项目，包括库、工具、框架、引擎和服务器应用程序。Tomcat 是 Java Servlet 和 JavaServer Pages 规范的开源实现。Tomcat 专为在 Apache 服务器中使用而设计。JMeter 是一个用于测试服务器资源（如 servlet 和 CGI 脚本）性能的 Java 桌面工具。Velocity 是一个提供对 Java 对象轻松访问的模板引擎。Watchdog 是一个检查 servlet 容器兼容性的工具。Struts、Cactus 和 Tapestry 是 Java 框架，是开发 Java Web 应用程序的既定方法。

| 网站 | 描述 |
|---|---|
| www.apache.org | Apache 软件基金会 |
| httpd.apache.org | Apache HTTP 服务器项目 |
| jakarta.apache.org | Jakarta Apache 项目 |
| www.apache-gui.com | Apache GUI 项目 |
| www.comanche.org | Comanche (Apache 配置管理器) |
| www.apache-ssl.org | Apache-SSL 服务器 |
| www.openssl.org | OpenSSL 项目 (安全套接字层) |
| www.modssl.org | 用于向 Apache Web 服务器添加 SSL 加密的 SSL 模块 (mod_ssl) 项目 |
| www.php.net | PHP 超文本预处理器，嵌入式 Web 页面编程语言 |

**表 23-1 与 Apache 相关的网站**

### Linux Apache 安装

您的 Linux 发行版通常会在初始安装 Linux 系统时提供安装 Apache Web 服务器选项。所有必要的目录和配置文件都会为您自动生成。然后，只要您运行 Linux，您的系统就已经是一个功能完整的网站。每次启动系统时，Web 服务器也会启动并持续运行。在大多数发行版中，保留给网站数据文件的目录是 `/var/www/html`。将您的网页放置在此目录或任何子目录中。您的系统已配置为作为 Web 服务器运行。您只需要执行必要的网络服务器配置，然后指定对远程用户开放的文件和目录即可。您无需做其他任何事情。一旦您的网站连接到网络，远程用户就可以访问它。

Web 服务器通常将您的网站设置在 `/var/www` 目录中。它还设置了几个用于管理该网站的目录。`/var/www/cgi-bin` 目录保存 CGI 脚本，`/var/www/html/manual` 保存 HTML 格式的 Apache 手册。您可以使用浏览器查看它。您的网页应放置在 `/var/www/html` 目录中。将您的网站首页页面放置在那里。您的配置文件位于不同的目录 `/etc/httpd/conf`。表 23-2 列出了各种 Apache Web 服务器目录和配置文件。

### Apache 多处理模块：MPM

Apache 现在使用一种新架构，该架构使用多处理模块 (MPM)，旨在定制 Apache 以适应不同的操作系统，并处理某些多处理操作。对于主要 MPM，Linux 系统可以使用 prefork 或 worker MPM，而 Windows 则使用 mpm_winnt MPM。prefork 是一个标准的 MPM 模块，旨在与较旧的 Unix 和 Linux 系统（特别是那些不支持线程的系统）兼容。它是 Fedora 默认加载的模块。worker MPM 为 Apache 服务器进程实现了线程化，这是 Red Hat 和 Fedora 中作为原生 POSIX 线程库 (NPTL) 一部分所支持的功能。您可以在 Apache 配置文件 `/etc/httpd/conf/httpd.conf` 中配置两者的工作负载参数。

许多曾经位于 Apache 核心的指令现在被放置在相应的模块和 MPM 中。通过这种模块化设计，一些指令已被弃用，例如 ServerType。这些模块的配置文件位于 `/etc/httpd/conf.d` 目录中。

### 启动和停止 Web 服务器

在大多数系统中，Apache 安装为独立服务器，持续运行。如第 21 章中关于 init 脚本的讨论所述，您的系统会自动启动 Web 服务器守护进程，在每次启动系统时调用它。用于 Web 的服务脚本

## Apache Web 服务器文件和目录（RPM 安装）

| Web 站点目录 | 描述 |
|---|---|
| `/var/www/html` | Web 站点文件 |
| `/var/www/cgi-bin` | CGI 程序文件 |
| `/var/www/html/manual` | Apache Web 服务器手册 |

| 配置文件 | 描述 |
|---|---|
| `.htaccess` | 基于目录的配置文件；`.htaccess` 文件包含指令，用于控制其所在目录内文件的访问 |
| `/etc/httpd/conf` | Apache Web 服务器配置文件的目录 |
| `/etc/httpd/conf/httpd.conf` | Apache Web 服务器配置文件 |
| `/etc/httpd/conf.d` | 包含模块配置文件的目录，例如用于 SSL 的 `ssl.conf` 和用于 PHP 的 `php.conf` |

| 服务脚本 | 描述 |
|---|---|
| `/etc/rc.d/init.d/httpd` | Web 服务器守护进程的服务脚本 |
| `/etc/sysconfig/httpd` | 用于 httpd 服务脚本的 Red Hat 和 Fedora Web 服务器守护进程配置选项 |

| 应用程序和模块文件 | 描述 |
|---|---|
| `/usr/sbin` | Apache Web 服务器程序文件和工具的位置 |
| `/usr/share/doc/` | Apache Web 服务器文档 |
| `/var/log/http` | Apache 日志文件的位置 |
| `/etc/httpd/modules` | 包含 Apache 模块的目录 |
| `/etc/httpd/run` | 包含 Apache 进程 ID 的目录 |

名为 `httpd` 的 Web 服务器位于 `/etc/rc.d/init.d` 目录中。用于运行此脚本的符号链接位于相应的运行级别目录中。通常，您会在运行级别 3 和 5 的目录 `/etc/rc.d/rc3.d` 和 `/etc/rc.d/rc5.d` 中找到指向 `/etc/rc.d/init.d/httpd` 的 `$85$httpd` 链接。您可以使用 `chkconfig` 命令或 System V Init 编辑器来设置 httpd 服务器启动的运行级别，并在相应的运行级别目录中创建链接。以下命令将设置 Web 服务器（httpd）在运行级别 3 和 5 时启动（有关运行级别的更多详细信息，请参见第 21 章和第 27 章）：

```bash
