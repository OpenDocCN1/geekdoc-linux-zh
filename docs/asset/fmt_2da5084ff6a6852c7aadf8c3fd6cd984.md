
`access.conf`，包含控制文档访问的指令。文件名可以通过 `httpd.conf` 文件中的 `AccessConfig` 指令进行覆盖。

另一个较少使用的配置文件 `mime.types` 也会被服务器读取。它包含了 MIME 文档类型。

关于这些配置文件，周围环绕着许多奇怪的现象和困惑。基本上，任何指令都可以出现在任何配置文件中。尽管每个配置文件都关联了一些通用的使用指南，但你并不要求将所有的文档管理信息都放在 `srm.conf` 文件中；它们完全可以出现在 `httpd.conf` 文件中。然而，如果你这样做，你会发现你的配置任务变得太困难了，因为你每次想做更改时都必须搜索三个配置文件。因此，最好遵循与每个文件相关的通用原则。

### 编辑 Httpd.Conf 文件

为了让 Web 服务器运行起来，你的首要任务是使用 `emacs` 或 `elvis` 对 `httpd.conf` 文件进行细微修改。以下是文件的完整内容：

```
# 这是主服务器配置文件。请访问 URL http://www.apache.org/
# 查看说明。

# 在你不理解这些指令的作用之前，请不要仅仅阅读
# 这里的指令，如果不确定，请查阅在线文档。你已被
# 警告。

# 原由 Rob McCool 编写

# ServerType 有 inetd 或 standalone（独立模式）。

ServerType standalone

# 如果你从 inetd 运行，请前往 "ServerAdmin"。

# Port：standalone 模式监听的端口。对于小于 1023 的端口，你

# 需要最初让 httpd 以 root 身份运行。

Port 80

# 如果你想以不同的用户或组运行 httpd，你必须最初

# 以 root 身份运行 httpd，然后它会自动切换。

# User/Group：运行 httpd 的用户/组的名称（或 #数字）。

# 在 SCO (ODT 3) 上使用 user 和 Group nogroup

User nobody

Group #-1

# ServerAdmin：你的地址，当服务器出现问题时应向该地址

# 电子邮件。

ServerAdmin@your.address

# ServerRoot：服务器配置、错误和日志文件存放的目录

ServerRoot /usr/lib/httpd

# BindAddress：你可以通过此选项支持虚拟主机。此选项

# 用于告诉服务器监听哪个 IP 地址。它可以包含

# ***、一个 IP 地址或一个完全限定的 Internet 域名。

# 另请参阅 VirtualHost 指令。

# BindAddress *

# ErrorLog：错误日志文件的位置。如果它不是以 / 开头，

# 则会在前面加上 ServerRoot。

ErrorLog logs/error_log

# TransferLog：传输日志文件的位置。如果它不是以 / 开头，

# 则会在前面加上 ServerRoot。

TransferLog logs/access_log

# PidFile：服务器应该记录其 pid 的文件

PidFile logs/httpd.pid

# ServerName 允许你设置一个主机名，如果它与程序获取的

# 名称不同，则该名称将返回给客户端（例如使用

# "www" 而不是主机的真实名称）。

# 注意：你不能凭空发明主机名并希望它们有效。你在此

# 定义的名称必须是你主机的有效 DNS 名称。如果你不理解

# 这一点，请咨询你的网络管理员。

ServerName new.host.name

# CacheNegotiatedDocs：默认情况下，Apache 会对每个根据内容

# 协商的文档发送 Pragma: no-cache。这要求代理

# 服务器不要缓存该文档。取消下行的注释将禁用

# 这种行为，并允许代理缓存文档。

CacheNegotiatedDocs

# Timeout：在接收和发送超时之前的秒数。

# 注意：编译后的默认值为 1200（20 分钟！）

Timeout 400

# 进程池大小调节。与其让你猜测需要多少个

# 服务器进程，Apache 会根据它看到的负载进行动态调整

# 也就是说，它尝试保持足够的服务器进程来处理

# 当前负载，外加几个备用服务器以处理瞬时

# 负载峰值（例如，来自单个 Netscape 浏览器的多个

# 同时请求）。

# 它通过定期检查有多少个服务器正在等待

# 请求来实现这一点。如果少于 MinSpareServers，它会创建一个

# 新备用进程。如果多于 MaxSpareServers，某些备用

# 就会退出。这些值对于大多数网站来说可能足够了——

MinSpareServers 5

MaxSpareServers 10

# 启动的服务器数量，应当是合理的

StartServers 5

# 运行服务器总数的限制，达到后

MaxClients 150

# MaxRequestsPerChild：每个进程在退出之前允许处理的
# 请求数。事实上，如果你预期的流量很大，
# 你将被强制运行在

MaxRequestsPerChild 30

# VirtualHost：允许多个地址，这是

<VirtualHost host.com>
#ServerAdmin webmaster@host.com
#DocumentRoot /www/host.com
#ServerName host.com
#ErrorLog logs/error_log
TransferLog/access_log
</VirtualHost>
```

### ServerType

`ServerType standalone` 指的是服务器运行在独立模式（即服务器直接响应）还是运行在 `inetd` 模式（即服务器响应 `inetd`）。如果你在 `inetd` 模式下运行，启动服务器的命令将插入 `/inetd....`。在独立模式下运行时，它在启动文件（通常是 `/etc/local` 或 `/etc/rc3.d`）。当运行独立模式（默认），启动此项的命令在。事实上，如果你预期的流量很大，你将被强制运行在独立模式，除非你有很多用户。然而，在 `inetd` 模式下执行的 `httpd` 守护进程将更容易受到外部世界的攻击。

### Port

`Port 80` 指服务器监听的端口。数字 `80` 是默认值，但这个数字可以是 `0` 到 `65535` 之间的任何数字。Linux（以及通用的 UNIX）定义了一些端口（实际上，所有低于 `1024` 的端口）作为特定用途的保留（这些端口的列表在 `/etc/services` 中）。在大多数情况下，你可能希望将端口保持为 `80`，因为这似乎是 Web 服务器世界中的默认值。

此端口设置有一个副作用，如果安全是一个问题，你将会注意：由于端口数字较小，你必须以 `root` 身份启动服务器。在绑定端口之后、接受请求之前，Apache 将切换到 `User` 指令设置的低特权用户。

然而，你可以使用任何未使用的端口用于 Web 服务器。如果你允许除 `root` 以外的用户启动 `httpd` 守护进程，那么他们必须使用高于 `1023` 的端口（`8080` 是一个流行的替代方案）。

### 用户与组 (Users and Groups)

当启动 Web 服务器时，它必须拥有访问文件系统中文件的权限，并且能够切换到 `root`，因为从通上来说，出于安全考虑，让 Web 服务器以 `root` 运行并不是好主意（如果有人攻破 Web 服务器，他们就可以访问你的整个文件系统）。因此，你需要为它分配用户名和组名以进行权限。默认是用户 `nobody` 和组 `#1`。

## 服务器管理员 (ServerAdmin)

`Admin you@your.address` 是服务器管理员的邮箱地址，这也是错误信息返回给用户的地址。许多 Web 管理员会设置一个专用电子邮件帐户（例如 `webmaster@largecorp.com`）来处理这些情况，因为许多用户发送的消息非常模糊，没有提到他们具体是在抱怨 Web 服务器，而不是 Gopher 服务器或邮件服务器。在 Web 服务器启动之前，需要更改 `you@your.address` 部分。

## 根根目录 (ServerRoot)

`Root /usr/lib/httpd` 指包含 `httpd` 支持文件的目录。在配置文件中，对于 Slack Linux 安装来说，这是一个错误的位置；它是默认 Apache Web 服务器安装的文件位置，而不是通用 Slack 安装的一部分。你可能将其更改为 `/var/lib/httpd`（假设你没有对 Apache 文件位置进行任何更改）。在 Linux 下启动 Apache Web 服务器之前，需要更改此处。
