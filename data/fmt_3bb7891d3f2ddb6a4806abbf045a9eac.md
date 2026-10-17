
`mod_cgi.c`

`mod_asis.c`

`mod_imap.c`

`mod_actions.c`

`mod_userdir.c`

`mod_alias.c`

`mod_rewrite.c`

`mod_access.c`

`mod_auth.c`

`mod_so.c`

`mod_setenvif.c`

## 第22章 设置Web服务器

这些标准的动态链接 Apache 模块全部在表 22-1 中描述。

## 表 22-1

| Module | Description |
| :--- | :--- |
| `http_core` | 其中之一必须静态链接，实现 Apache 最基本的核心 |
| `mod_access` | 基于源主机名/IP 地址提供访问控制 |
| `mod_actions` | 根据文件的 MIME 类型或请求方法有条件地执行 CGI 脚本 |
| `mod_alias` | 允许重定向并将物理系统的部分映射为通过 Web 服务器可访问的逻辑实体 |
| `mod_asis` | 使文件在传输时不添加任何 HTTP 头部（即 `Status`、`Location` 和 `Content-type` 头） |
| `mod_auth` | 基于用户名/密码对提供访问控制。认证信息存储在纯文本文件中，尽管密码使用 `crypt` 系统调用进行加密 |
| `mod_autoindex` | 实现自动生成的目录索引 |
| `mod_cgi` | 控制由 `"cgi-script"` 处理器解析或具有 MIME 类型 `x-httpd-cgi` 的文件的执行 |
| `mod_dir` | 在 URL 引用目录且未选择明确文件名时设置可用文件列表 |
| `mod_env` | 控制传递给 CGI 脚本的环境变量 |
| `mod_imap` | 控制内联图像映射文件，这些文件的 MIME 类型为 `x-httpd-imap` 或由图像处理器解析 |
| `mod_include` | 实现服务器端包含 (`SSI`)，即在发送给客户端之前由服务器解析的包含条件语句的 `HTML` 文档 |
| `mod_log_config` | 允许为日志文件中的信息自定义格式 |
| `mod_mime` | 根据预定义值或文件的 MIME 类型改变文档的处理方式 |

## 724 第四章 IV OpenLinux 网络与服务器设置

### 表 22-1 (继续)

| Module | Description |
| :--- | :--- |
| `mod_negotiation` | 基于 `Content-Encoding`、`Content-Language`、`Content-Length` 和 `Content-Type` HTTP 头字段有条件显示文档。 |
| `mod_rewrite` | 提供灵活且可扩展的方法，用于重定向客户端请求并将 incoming URLs 映射到文件系统中的其他位置。 |
| `mod_setenvif` | 根据各种 HTTP 头的内容有条件地设置环境变量。 |
| `mod_so` | 除 `http_core` 外唯一必须在服务器上静态编译的模块，该模块包含实现动态共享对象所需的指令。 |
| `mod_status` | 提供每个单独 http 服务器进程的活动摘要，包括 CPU 和带宽使用水平。 |
| `mod_userdir` | 指定可包含个人用户 HTML 文档的位置。 |

## 第22章 设置Web服务器 725

使用 `inetd` `ServerType` 时，每当收到新的 HTTP 请求时，会由 `inetd` 守护进程启动一个服务器。这不推荐，因为每个新请求都需要加载并配置一个新守护进程。`ServerType` 为 `standalone`（它会启动一个主守护进程来 `spawn` 多个等待 incoming requests 的服务器）会提高响应时间，并一次性处理更多请求。

## 选择服务器类型

您可以选择如何启动服务器守护进程以处理 http 请求。为此，可以按以下方式设置 `ServerType` 值：

- `ServerType` 可以是 `inetd` 或 `standalone`。
- `ServerType standalone`

`standalone` 监听的端口。对于端口小于 `1023`，需要先以 `root` 运行 `httpd`。

### `Port 80`

`Port 80` 是 HTTP 流量的默认端口，对应的 URL `http://www.apache.org/80` 等同于 `http://www.apache.org/`。如果服务器绑定到其他端口，则 URL 中必须指定端口号（例如 `http://video.dlib.vt.du:90/history/`）。大多数 Web 服务器运行在端口 `80`，但它们可以接受除 `65536` 以下且未被特定服务占用的任何端口的连接（请参阅 `/etc/services` 文件以获取常用服务/协议及其端口列表）。只有 `root` 用户才能运行在特权端口（低于 `1024`）上的连接程序。然而，主服务器会启动使用 `"nobody"` 用户和组的子服务器（出于安全考虑）。

## 设置主机名查找

- `HostnameLookups`: 记录客户端的名称或您的 IP 地址
    - 例如 `www.apache.org` (`on`) 或 `204.62.129.132` (`off`)
    - `HostnameLooks off`
    - 默认关闭，因为如果人们有意打开此功能，整体上对网络更好。

- `HostnameLooks off`
    - 如果将 `HostnameLookups` 打开，每个 incoming 连接都会进行 DNS 查找以将客户端 IP 转换为主机名。如果您的站点接收大量请求，服务器的响应时间可能会显著下降。除非您使用需要完全限定域名且无法自行进行统计的日志分析程序或包，否则应关闭 `HostnameLookups`。Apache 发行版随附的 `logresolve` 程序可以在非高峰时段调度编辑日志文件，进行主机名查找。

...

## 选择服务器的用户/组

`httpd` 守护进程不必作为 `root` 用户运行。通过设置 `User` 和 `Group` 条目，您可以让守护进程由不同的用户和组运行：

- `#` 如果您希望 `httpd` 以不同的用户或组运行，您必须先
- `#` 以 `root` 为初始运行 `httpd`，然后它会切换。
- `#` 用户/组：要运行 `httpd` 的用户或组的名称（或 #号码）。
- `#` 在 SCO（ODT 3）系统中，使用 `User nogroup` `Group nogroup`
- `#` 在 HPUX 系统中，您可能无法使用共享内存，并且
- `#` 建议的解决办法是创建用户 `www` 并使用该用户。
- `#` 注意：某些内核拒绝执行 `setgid(Group)` 或 `semctl(IPC_SET)`
- `#` 当 `(unsigned)Group` 的值超过 `60000` 时；
- `#` 在这些系统上请勿使用 `Group nobody`！

`User nobody`
`Group nobody`

建议 `User` 和 `Group` 指令指定一个非特权实体。这样可以在您的站点被入侵时降低损害风险。第一个启动的守护进程将以 `root` 运行。这对于将服务器绑定到低位端口以及切换到 `User` 和 `Group` 指令指定的用户/组是必要的。所有其他服务器都将在该用户 ID (`UID`) 和组 ID (`GID`) 下运行。

## 设置电子邮件地址和日志文件位置

如果服务器的配置文件、错误文件和日志文件所在的目录存在，您可以确定电子邮件应发送的位置：

- `#` `ServerAdmin`：您的地址，出现服务器问题时应发送电子邮件。
- `#` `ServerRoot`：服务器的配置文件、错误文件和日志文件保存的目录。
- `#` 注意！如果您计划将其放置在 NFS（或其他网络）挂载的文件系统上，请阅读 `LockFile` 文档，以免出现很多麻烦。

`ServerAdmin`: 您的地址，出现服务器问题时应发送电子邮件。
`ServerRoot`: 服务器的配置文件、错误文件和日志文件保存的目录。
