
`httpd.conf` 文件是 Apache Web 服务器的主要配置文件。它包含了与服务器通用运行相关的选项。默认文件名（`/etc/httpd/httpd.conf`）可以通过 `-f filename` 命令行参数或 `ServerConfigFile` 指令进行覆盖。以下章节列出了 `httpd.conf` 文件的内容并描述了如何使用它：

## httpd.conf -- Apache HTTP 服务器配置文件

```
# 这是主服务器配置文件。请参阅 URL http://www.apache.org/
# 获取说明。

# 如果您不确定这些指令的作用，请勿简单地
# 阅读这里的指令，如果不确定，请查阅在线文档。
# 你已经收到警告了。

# 最初由 Rob McCool 创建

# 动态共享对象 (DSO) 支持
# 为了能够使用构建为 DSO 的模块的功能，您
# 必须在此处放置相应的 'LoadModule' 行，以便其中包含
# 的指令在被使用 *之前* 是可用的。
# 请阅读 Apache 1.3 分发中的 README.DSO 以获取更多
# 关于 DSO 机制的详细信息，并运行 'httpd -l' 获取已
# 内置（静态链接，因此始终可用）的 httpd
# 二进制文件模块列表。
```

```
# 示例:
# LoadModule foo_module libexec/mod_foo.so
# 模块的文档位于 "/home/httpd/manual/mod" 中的 HTML 格式。
# LoadModule mmap_static_module modules/mod_mmap_static.so
LoadModule env_module modules/mod_env.so
LoadModule config_log_module modules/mod_log_config.so
LoadModule agent_log_module modules/mod_log_agent.so
LoadModule referer_log_module modules/mod_log_referrer.so
# LoadModule mime_magic_module modules/mod_mime_magic.so
LoadModule mime_module modules/mod_mime.so
LoadModule negotiation_module modules/mod_negotiation.so
LoadModule status_module modules/mod_status.so
LoadModule info_module modules/mod_info.so
LoadModule include_module modules/mod_include.so
LoadModule autoindex_module modules/mod_autoindex.so
LoadModule dir_module modules/mod_dir.so
LoadModule cgi_module modules/mod_cgi.so
LoadModule asis_module modules/mod_asis.so
LoadModule imap_module modules/mod_imap.so
LoadModule action_module modules/mod_actions.so
# LoadModule speling_module modules/mod_speling.so
LoadModule userdir_module modules/mod_userdir.so
LoadModule proxy_module modules/libproxy.so
LoadModule alias_module modules/mod_alias.so
LoadModule rewrite_module modules/mod_rewrite.so
LoadModule access_module modules/mod_access.so
LoadModule auth_module modules/mod_auth.so
LoadModule anon_auth_module modules/mod_auth_anon.so
# LoadModule dbm_auth_module modules/mod_auth_dbm.so
LoadModule db_auth_module modules/mod_auth_db.so
LoadModule digest_module modules/mod_digest.so
# LoadModule cern_meta_module modules/mod_cern_meta.so
LoadModule expires_module modules/mod_expires.so
LoadModule headers_module modules/mod_headers.so
LoadModule usrack_module modules/mod_usrack.so
# LoadModule example_module modules/mod_example.so
# LoadModule unique_id_module modules/mod_unique_id.so
LoadModule setenvif_module modules/mod_setenvif.so

# 额外模块
# LoadModule php_module modules/mod_php.so
# LoadModule php3_module modules/libphp3.so
# LoadModule perl_module modules/libperl.so
```

### 从所有可用模块（静态和共享模块）重构完整的模块列表

# 以实现正确的模块执行顺序。

# [每当您更改上面的 LOADMODULE 部分时，请同步更新此处]

ClearModuleList

# AddModule mod_mmap_static.c

```
AddModule mod_env.c
AddModule mod_log_config.c
AddModule mod_log_agent.c
AddModule mod_log_referer.c
#AddModule mod_mime_magic.c
AddModule mod_mime.c
AddModule mod_negotiation.c
AddModule mod_status.c
AddModule mod_info.c
AddModule mod_include.c
AddModule mod_autoindex.c
AddModule mod_dir.c
AddModule mod_cgi.c
AddModule mod_asis.c
AddModule mod_imap.c
AddModule mod_userdir.c
AddModule mod_proxy.c
AddModule mod_alias.c
AddModule mod_rewrite.c
AddModule mod_access.c
AddModule mod_auth.c
AddModule mod_auth_anon.c
AddModule mod_auth_db.c
AddModule mod_digest.c
AddModule mod_expires.c
AddModule mod_headers.c
AddModule mod_usrack.c
AddModule setenvif.c
```

### 在 httpd.conf 中选择模块

在编译过程中，可以对单个模块进行动态链接。必须同步上面的 `LoadModule` 和 `AddModule` 代码，否则模块对服务器无效。

如果某个模块包含不需要的功能，可以很容易地从列表中注释掉。同样，您可能希望通过在列表中包含第三方模块（例如，为了更快执行脚本而集成的 Perl ，或者在 HTML 文档中嵌入脚本语言的 mod_php）来添加功能或特性。每个标准的动态链接 Apache 模块都在表 21-1 中描述。

#### 表 21-1

动态共享对象 (DSO) 模块

| 模块 | 描述 |
| :--- | :--- |
| core | 两个必须静态链接的模块之一，它实现了 Apache 最基础的核心。两个必须静态链接的模块之一，它实现了 Apache 最基础的核心。 |
| mod_access | 基于源主机名/IP 地址提供访问控制。 |
| mod_actions | 根据文件的 MIME 类型或请求方法条件执行 CGI 脚本。 |
| mod_alias | 允许重并将物理文件系统的部分映射为 Web 服务器访问的逻辑实体。 |
| mod_asis | 允许传输文件而不添加任何 HTTP 头部（即 Status、Location 和 Content-type 头部字段）。 |
| mod_auth | 基于用户名/密码对提供访问控制。身份验证信息存储在纯文本文件中，尽管密码使用 crypt(3) 系统调用进行了加密。 |
| mod_auth_anon | 对于匿名 FTP，此模块允许使用有效电子邮件地址作为密码的预定义用户名访问授权区域。 |
| mod_auth_db | 基于用户名/密码对提供访问控制。身份验证信息存储在 Berkeley DB 数据库文件中，密码经过加密。 |
| mod_auth_dbm | 基于用户名/密码对提供访问控制。身份验证信息存储在 DBM 二进制数据库文件中，密码经过加密。 |
| 模块 | 描述 |
| --- | --- |
| mod_autoindex | 实现自动生成的目录索引。 |
| mod_cerm_meta | 模拟原始 CERN http 中的 Meta 文件（可以包含 HTTP 头部信息）。 |
| mod_cgi | 控制由 "cgi-script" 处理器解析或 MIME 类型为 x-httpd-cgi 的文件的执行。 |
| mod_digest | 提供对用户名/密码对的访问控制。身份验证信息经过 MD5 加密并存储在纯文本文件中。| |
| mod_dir | 当引用目录的 URL 中未选择显式文件名时，设置可能被使用的文件名列表。 |
| mod_env | 控制传递给 CGI 脚本的环境变量。 |
| mod_example | 阐述服务器如何处理模块引用。 |
| mod_expires | 通过 Expires HTTP 头部对缓存的文档实施时间限制。 |
| mod_headers | 允许创建和生成自定义的 HTTP 头部。 |
| mod_imap | 控制内联图像映射文件，这些文件的 MIME 类型为 x-httpd-imap 或由图像处理器解析。 |
| mod_include | 实现服务器端包含 (SSI)，这些是 HTML 文档，包含在发送给客户端之前由服务器解析的条件语句。 |
| mod_info | 提供服务器配置的详细摘要，包括活动加载的模块列表以及每个模块中每个条指令的当前设置。 |
| mod_log_agent | 允许记录传入客户端请求 HTTP 头部中的 UserAgent 字段。 |
| mod_log_config | 允许对日志文件中包含的信息进行自定义格式。 |
| mod_log_referer | 允许记录传入客户端请求 HTTP 头部中的 Referer 字段。 |
| mod_mime | 根据预定义值或文件的 MIME 类型更改对文档的处理。 |
| mod_mime_magic | 类似于 UNIX 的 `file` 命令，此模块尝试根据文件内容的几个字节确定文件的 MIME 类型。 |
| mod_mmap_static | 如果文件可能不会变化，此模块允许在服务器启动时将文件加载到内存中，在请求文件时无需访问磁盘。 |

#### 表 21-1（续）

| 模块 | 描述 |
| --- | --- |
| mod_negotiation | 根据 Content-Encoding、Content-Language、Content-Length 和 Content-Type HTTP 头部字段提供文档条件显示。 |
| mod_proxy | 实现缓存代理服务器。 |
| mod_rewrite | 提供一种重定向客户端请求并将 URL 映射到文件系统中其他位置的灵活且扩展的方法。 |
| mod_setenvif | 根据各种 HTTP 头部字段的内容有条件的设置环境变量。 |
| mod_so | 除 http_core 之外的唯一必须在服务器中进行静态编译的模块，此模块包含实现动态共享对象所需的指令。 |
| mod_speling | 尝试自动纠正请求 URL 中的拼写错误。 |
| mod_status | 提供每个单独 httpd 服务器进程活动的摘要，包括 CPU 和带宽使用水平。 |
| mod_unique_id | 尝试为每个客户端分配令牌令牌，令牌令牌集群内所有机器的所有服务器进程中是唯一的。 |
| mod_userdir | 指定可以包含单个用户 HTML 文档的位置。 |
| mod_usertrack | 使用 cookie 跟踪用户在网站上的浏览进度。 |

关于每个模块（以及可以在其中定义的指令）的更多信息，可以在您的服务器上 http://localhost/manual/mod/ 找到。

### 选择服务器类型

你可以选择如何产生服务器守护进程来处理 HTTP 请求。要做到这一点，你可以如下设置 `ServerType` 值：

```
# ServerType 可以是 inetd 或 standalone。
ServerType standalone
```

```
# 如果你从 inetd 运行，请前往 "ServerAdmin"。
```

### 第 21 章：设置 Web 服务器

使用“inetd”服务器时，每当接收一个新的 HTTP 请求时，inetd 守护进程中就会产生一个服务器。这不建议这样做，因为每个新请求都必须加载并配置一个新的守护进程。`standalone` `ServerType`（它将启动一个主守护进程来产生几个等待传入请求的服务器）会导致更好的响应时间，并允许同时处理更多请求。

### 选择 HTTP 端口号

Apache 在特定的端口监听 HTTP 请求。由 `Port` 条目使用的端口如下：

```
# Port: standalone 监听的端口。对于小于 1023 的端口，你
# 需要初始以 root 身份运行 httpd。

Port 80
```

端口 80 是 HTTP 流量的默认端口，这也就是为什么 URL http://www.apache.org:80/ 等同于 http://www.apache.org/。如果服务器绑定到不同的端口，则必须在 URL 中指定端口号（例如 http://video.dl1b.vt.edu:90/history/）。大多数服务器运行在端口 80 上，尽管它们可以接受任何未被绑定到特定服务的端口（65536 以下）的连接（请参阅 `/etc/services` 以获取常用服务/协议及其使用的端口列表）。只有 root 才能运行在特权端口（1024 以下）上监听连接的程序。

### 设置主机名查找

在 Apache Web 服务器中，你可以让服务器查找传入请求的地址。如果开启 `Hostnameups` 指令，每个连接都将客户端的 IP 地址转换为主机名。如果你的请求很多，可能会影响响应时间。默认是关闭。

```
# Hostnameups: 开启或关闭
# 默认关闭，除非你使用在空闲时间进行查找的日志包。

Hostnameups off
```

### 选择的用户/组

httpd 守护进程不需要以 root 用户运行。通过设置 `User` 和 `Group` 条目，你可以让守护进程由不同的用户运行：

```
# 如果你希望 httpd 以不同的用户运行，你必须
# 以 root 运行，它将切换。
```

- User/Group：运行 httpd 的用户名称或数字。

- 在 SCO 上可能无法使用 Group nobody，建议的解决方法是创建 www 并使用该用户。

- 在 HPUX 上，当 Group 值大于 60000 时，内核拒绝 setgid(Group) 或 semctl(IPC_SET)。

User nobody

Group nobody

建议 `User` 和 `Group` 指令指定非特权实体。这可以降低服务器被破坏时的风险。第一个守护进程将以 root 身份启动。这对于绑定低数字端口以及切换到 `User` 和 `Group` 指令指定的用户/组是必要的。所有其他服务器将在该用户 ID (UID) 和组 ID (GID) 下运行。

### 设置电子邮件和日志文件位置

你可以指定服务器出现问题时发送电子邮件。你还可以指定服务器配置、错误文件和日志文件的目录：

```
# ServerAdmin: 你的地址，服务器问题将发送至此处。
```

ServerAdmin root@localhost

```
# ServerRoot: 服务器配置、错误和日志文件存放的目录。
# 注意！如果你打算将此放置在 NFS（或其他网络）
# 挂的文件系统上，请阅读 LockFile 文档，
# 将为你节省很多麻烦。
```

ServerRoot /etc/httpd

`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。它可以简单地指向 root 账户（如上所示）、向用户账户发送邮件（在相同或其他机器上），或将邮件重定向到别名（如 Webmaster），该别名可以将邮件分发给多个人。

ServerRoot 指令指定包含配置文件、指向日志文件目录的链接以及指向模块目录链接的目录。可以使用 httpd 的 -d 命令行参数指定备用的 ServerRoot 路径。

### 在虚拟地址上绑定

Apache 宿支持虚拟主机概念。通过使用 `BindAddress` 条目，你可以告诉服务器监听哪个 IP 地址：
