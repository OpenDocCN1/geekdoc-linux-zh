
为了使网络启动正常工作，你需要确保用于启动的网络接口具有 PXE 启动能力。

# 总结

在本章中，你学习了如何使用各种方法进行 RHEL 网络安装。你准备了一个可以通过 NFS、FTP 或 HTTP 协议访问的安装服务器。你查看了启动客户端的各种方法，以及如何准备可启动 CD 和 USB 盘。你使用安装 CD、可启动 CD 和可启动 USB 盘启动本地客户端，从 NFS、FTP 和 HTTP 服务器上拉取 OS 镜像并进行安装。本章的下一个主要部分讨论了无人干预安装，包括通过编辑现有文件或使用 Kickstart 配置器创建 kickstart 配置文件，并使用它执行安装。在章节的末尾，提到了网络启动和网络安装的主题。

# Web 服务器与缓存代理服务器

本章涵盖了以下主要主题：

- Apache Web 服务器及其功能
- Apache 配置和日志文件
- `httpd.conf` 文件分析
- 防火墙、SELinux 和安全上下文层面的 Apache 安全
- 理解通用、主机级和用户级安全指令
- 配置并测试 Apache Web 服务器
- Apache 虚拟主机概述
- 配置并测试虚拟主机和安全虚拟主机
- HTTP 配置器概述
- Squid Web 缓存代理服务器基础
- Squid 守护进程及相关文件
- 理解 Squid 启动和配置文件
- Squid 的 SELinux 要求
- 配置并测试 Squid 服务器

# Web 服务器软件允许你在互联网或企业内网上发布网站。

该软件运行在称为 Web 服务器的系统中，并为互联网或企业网络的用户提供托管网站的访问。目前有数百万个 Web 服务器，运行着多种 Web 服务器软件，其中 Apache 最受欢迎。本章介绍了 Apache Web 服务器以及用于本地缓存访问网页的 Squid 代理服务器的详细信息。

### Apache Web 服务器

Apache 无疑是目前互联网和企业网络上最流行、稳定且安全的 Web 服务器软件。最新版本是 2.2.11，但本章将涵盖 2.2.3 版本，它支持虚拟主机、访问控制、动态模块加载和安全 HTTP 等功能。Apache 使用 http（超文本传输协议）守护进程通过 HTTP 和 HTTPS 协议为客户端提供网页访问。

# Apache 特性

与 Apache Web 服务器的一些关键特性包括：

- 支持大小大于 2GB 的文件。
- 支持加密身份验证方法。
- 支持 LDAP 身份验证。
- 支持虚拟主机，在单个服务器上托管多个网站，且所有网站共享一个 IP 地址。
- 可以为不同的服务定义单独的配置文件，并存储在不同的目录位置。

# Apache 关键文件

Apache 配置文件位于 `/etc/httpd` 目录。表 29-1 列出并解释了关键配置和其他文件。

| 文件 | 描述 |
| --- | --- |
| /etc/httpd/conf/httpd.conf | 主 Web 服务器配置文件。 |
| /etc/httpd/conf/ssl.conf | 安全 Web 服务器配置文件。 |
| /etc/httpd/conf/*.conf | 支持其他服务的配置文件。 |
| .htaccess | 允许用户管理整个 DocumentRoot 或 DocumentRoot 内的特定目录，取决于放置位置。 |
| /usr/lib/httpd/modules | httpd 特定模块的目录。 |
| /var/run/httpd.pid |  httpd 守护进程的 PID 文件。 |

表 29-1 Apache 文件

Web 服务器的主配置文件位于 `/etc/httpd/conf` 目录。另一个文件 `/etc/httpd/conf/ssl.conf` 用于设置安全 Web 服务器。`/etc/httpd/conf.d` 目录下有很多以 `.conf` 结尾的其他配置文件，在 Apache 服务器启动时会被引用。该目录产生以下输出：

# /etc/httpd/conf.d

| 总计 88 |
| --- |
| -rw-r---- 1 | root | 295 | 8月 7日 | manual.conf |
| -rw-r---- 1 | root | 1796 | 4月 22日 | perl.conf |
| -rw-r---- 1 | root | 560 | 9月 12日 | php.conf |
| -rw-r---- 1 | root | 566 | 8月 7日 | proxy_ajp.conf |
| -rw-r---- 1 | root | 1671 | 7月 12日 | python.conf |
| -rw-r---- 1 | root | 392 | 8月 7日 | README |
| -rw-r---- 1 | root | 332 | 3月 23日 | squid.conf |
| -rw-r---- 1 | root | 9677 | 8月 7日 | ssl.conf |
| -rw-r---- 1 | root | 352 | 7月 12日 | webalizer.conf |
| -rw-r---- 1 | root | 299 | 8月 7日 | welcome.conf |

这些文件可以根据需要进行自定义。此外，你可以在此目录下根据需要创建许多额外文件。所有文件的语法与 `httpd.conf` 几乎相同。以下子节解释了通用指令：

## httpd.conf 文件

`httpd.conf` 文件的内容分为三个部分：全局环境、主服务器配置和虚拟主机，说明如下：

**第 1 部分：全局环境 – 此部分定义的指令影响 Web 服务器的整体运行。一些关键指令列在表 29-2 中。**

| 指令 | 描述 |
| --- | --- |
| ServerTokens | 默认为 OS。当用户访问不存在的网页时，限制浏览器中显示的信息。 |
| ServerRoot | 默认为 /etc/httpd。配置文件的目录位置。 |
| PidFile | 默认为 /run/httpd.pid。存储进程的 PID。 |
| Timeout | 默认为 120 秒。指定接收和发送请求之前的时间。 |
| KeepAlive | 默认为关闭。启用或禁用每个连接（持久连接）多个请求。 |
| MaxKeepAliveRequests | 默认为 100。指定持久连接期间的最大请求数。 |
| KeepAliveTimeout | 默认为 15 秒。指定服务器上同一连接等待下一个请求的时间。 |
| StartServers | 默认为 0。指定要启动的服务器进程数量。 |

| 指令 | 描述 |
| --- | --- |
| MinSpareServers | 指定最小空闲进程数。 |
| MaxSpareServers | 指定最大空闲进程数。 |
| ServerLimit | 指定的最大服务器进程。 |
| MaxClients | 限制并发请求数。 |
| MaxRequestsPerChild | 限制每个进程的请求数。 |
| MinThreads | 指定最小线程数。 |
| MaxThreads | 指定最大线程数。 |
| ThreadsPerChild | 指定每个服务器进程的线程数。 |
| Listen | 默认为 80。为客户端请求指定端口号。如果你想将 Web 服务器限制在特定地址，请指定 IP 地址和端口。 |
| LoadModule | 指定 Web 服务器启动时加载的模块。 |
| Include | 默认相对于 ServerRoot 为 conf.*。指定要加载的额外配置的位置。 |
| ExtendedStatus | 默认为关闭。控制是否生成完整（开启）或部分（开启）状态信息。 |
| User | 默认为 apache。指定 httpd 守护进程的所有者名称。 |
| Group | 默认为 apache。指定 httpd 守护进程的组名。 |

表 29-2 第 1 部分指令 – 全局环境

# 第 2 部分：‘主’服务器配置 – 此部分定义的指令与主服务器相关，并为文件第 3 部分可能定义的任何虚拟主机容器设置默认值。一些关键指令列在表 29-3 中解释。

| 指令 | 描述 |
| --- | --- |
| ServerAdmin | 默认为 root@localhost。指定管理员电子邮件地址。 |
| ServerName | 指定服务器名称（或 IP 地址）和端口号。 |
| UseCanonicalName | 默认为关闭。使用客户端提供的主机名和端口。如果为“开启”，则将使用 ServerName 作为正式名称。 |
| DocumentRoot | 默认为 /var/www/html。指定网站文件的目录位置。 |
| Options | 设置与 Web 目录相关的 Indexes、FileInfo、AuthConfig、Limit 和 FollowLinks 功能。 |
| AllowOverride | 默认为无。启用或禁用 .access 文件中定义的指令。 |
| Order | 定义评估 allow 和 deny 指令的顺序。 |
| Allow | 允许访问指定主机。 |
| Deny | 拒绝访问指定主机。 |
| UserDir | 默认禁用。指定用户网页的目录位置。如果启用，~/home 目录下的内容对 Web 用户可见。 |
| DirectoryIndex | 默认为 /usr/share/doc/HTML/index.html。指定当用户请求目录索引时提供的网页。 |
| AccessFileName | 默认为 .htaccess。指定每个目录中服务器将用于访问控制信息的文件名。 |
| TypesConfig | 默认为 /etc/mime.types。设置包含默认文件类型映射的文件名。 |

# 指令 | 描述

| 指令 | 描述 |
| :--- | :--- |
| DefaultType | 默认为 text/plain。如果在 /etc/mime.types 中未找到文档的 MIME 类型，则设置其使用的默认内容类型。 |
| MIMagicFile | 默认是相对于 ServerRoot 的 config/magic 文件。告知 mod_magic 模块用于提示定义的魔数文件。 |
| HostNameLookup | 默认是关闭。设置是否为 IP 地址解析 URL。 |
| EnableMMAP | 默认是关闭。定义是否在文件传输时使用内存映射。 |
| EnableSendfile | 默认是关闭。定义是否启用内核对文件传输的支持。 |
| ErrorLog | 默认是相对于 ServerRoot 的 logs/error_log。指定错误文件所在的位置。 |
| LogLevel | 默认为 warn。指定要记录消息的详尽程度。 |
| LogFormat | 默认为 combined 并存储在相对于 ServerRoot 的 logs/http/access_log 中。指定自定义日志文件并标识其格式。 |
| ServerSignature | 默认是开启。在任何生成的内容（如错误消息）中添加包含 Apache 服务器版本、ServerName 指令和（可选的）ServerAdmin 指令（电子邮件）的行。 |
| Alias | 定义 DocumentRoot 之外的目录。 |
| ScriptAlias | 指定 CGI（通用网关接口）脚本存储的位置。 |
| IndexOptions | 控制目录列表如何显示。 |
| AddIconByEncoding | 为带有编码的文件指定显示的图标。 |
| AddIconByType | 为指定类型的文件指定显示的图标。 |
| AddIcon | 为指定扩展的文件指定显示的图标。 |
| DefaultIcon | 为没有显式定义图标的文件指定一个图标。 |
| AddDescription | 为服务器生成的索引中的文件定义简短描述。 |
| ReadName | 默认是 README.html。定义附加在目录列表末部的 README 文件名。 |
| HeaderName | 默认是 HEADER.html。定义置于目录列表开头的 HEADER文件名。 |
| Indexno | 列出不包含在目录列表中的文件项、部分名、全名以及通配符表达式。 |
| DefaultLanguage | 为未指定标签的文件指定默认语言。 |
| AddLanguage | 将文件名扩展名分配给特定语言。适用于多语言网站。 |
| LanguagePriority | 如果客户端浏览器中未配置，则设置语言偏好。 |
| ForLanguagePriority | 如果未找到对应语言的网页，指定要采取的操作。 |
| AddCharset | 默认是 UTF-8。为所有提供的 Web 内容设置默认字符集。 |
| AddType | 将文件扩展名映射到指定的 MIME 类型。 |
| AddEncoding | 允许浏览器在线解压信息。 |
| AddHandler | 将文件扩展名映射到指定的处理器。 |
| AddFilter | 将文件扩展名映射到指定的过滤器。 |
| BrowserMatch | 允许服务器向不同类型的浏览器发送响应。 |

表 29-3 第 2 部分指令 – 主服务器配置

# 第 3 部分：虚拟主机 – 如果你想在同一台服务器上运行网站，将使用本节定义的指令。部分关键指令在表 29-4 中列出并解释。

| 指令 | 描述 |
| :--- | :--- |
| VirtualHost | 为虚拟主机指定主机名或 IP 地址。 |
| ServerAdmin | 为管理员指定电子邮件地址。 |
| DocumentRoot | 指定虚拟主机文件所在的根目录。 |
| ServerName | 为虚拟主机指定 URL。 |
| ErrorLog | 指定相对于 ServerRoot 的错误日志文件的位置。 |
| CustomLog | 指定相对于 ServerRoot 的自定义日志文件的位置。 |

表 29-4 第 3 部分指令 – 虚拟主机

| 容器开始 | 容器结束 |
| :--- | :--- |
| <VirtualHost ....> | </VirtualHost> |
| <IfModule> | </IfModule> |
| <Files> | </Files> |
| <Directory> | </Directory> |

表 29-5 容器开始和结束语法

# Apache 日志文件

Apache 日志文件位于 `/var/log/httpd` 目录，该目录是 `/etc/httpd logs` 目录的符号链接。该目录的 ll 输出所示。`access_log` 和 `error_log` 文件分别访问 Web 服务器访问和错误消息。`ssl*` 文件仅在安装了 SSL 证书时才使用。
