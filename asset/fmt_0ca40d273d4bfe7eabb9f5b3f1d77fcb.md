
此指令设置目录授权域（realm）名称。将此域提供给客户端，以便用户知道应该发送哪个用户名

# 第 4 章：设置 Web 服务器 245 页

和密码。它必须配合 `AuthType` `require` 指令（如 `AuthUserFile` 和 `AuthGroupFile`）才能工作。

### AuthType

- 语法：`AuthType type`
- 上下文：目录 (directory),.htaccess
- 覆盖：`AuthConfig`
- 状态：核心 (core)

此指令选择目录的用户身份验证类型。
目前仅实现了基础认证（basic authentication）。它必须配合 `AuthName` 和 `require` 指令（如 `AuthUserFile` 和 `AuthGroupFile`）才能工作。

## BindAddress

- 语法：`BindAddress saddr`
- 默认值：`BindAddress *`
- 上下文：服务器配置 (server config)
- 状态：核心 (core)

UNIX HTTP 服务器可以监听服务器机器上每个 IP 地址的连接，也可以仅监听服务器机器的一个 IP 地址。`saddr` 可以是通配符 (`*`)、IP 地址或完全限定的 Internet 域名名。如果值为 `*`，则服务器将在每个 IP 地址上监听；否则，它将仅在指定的地址上监听。

### DefaultType

- 语法：`DefaultType mime-type`
- 默认值：`DefaultType text/html`
- 上下文：服务器配置 (server config)，虚拟主机 (virtual host)
- 覆盖：`FileInfo`
- 状态：核心 (core)

当服务器被要求提供无法通过 MIME 映射确定类型的文档时，在未知类型的情况下将使用 `DefaultType`。例如，

```
DefaultType image/gif
```

## `<Directory>`

```
语法：      <Directory directory> ... </Directory>

上下文：     服务器配置 (server config)，虚拟主机 (virtual host)

状态：      
```

`<Directory>` 和 `</Directory>` 用于封装适用于指定目录及其子目录的指令。目录可以是完整路径或通配符字符串。在通配符字符串中，`?` 匹配单个字符，`*` 匹配字符序列。例如，

```
<Directory /usr/local/httpdocs
Options Indexes FollowLinks
</Directory>
```

[269-271]

如果多个目录匹配包含文档的目录，则指令将按照匹配顺序应用，并穿插来自 `.htaccess` 的指令。例如，

```
<Directory />
AllowOverride None
</Directory>
```

```
<Directory /home/*
AllowOverride FileInfo
</Directory>
```

# 248 页 第 4 章：设置 Web 服务器

发生问题或错误时，Apache 可以配置为执行四个操作之一：

- 像 NCSA httpd 1.3 那样。
- 输出自定义消息。
- 重定向到本地 URL 处理问题/错误。
- 重定向到外部 URL 处理问题/错误。

后三个选项使用 `ErrorDocument` 配置，其后跟随 HTTP 响应码和消息或 URL。此上下文中的消息以引号(`"`)开头，引号本身不是消息的一部分。Apache 有时会提供有关问题错误的额外信息。可以使用 `%s` 将其嵌入消息中。是一些示例：

```
ErrorDocument 500 /cgi-bin/tester
ErrorDocument 404 /cgi-bin/bad_urls.pl
ErrorDocument 401 http://www2.foo.bar/subscription_info.html
ErrorDocument 403 "Sorry can't allow you access today
```

## ErrorLog

- 语法：`ErrorLog filename`
- 默认值：`ErrorLog logs/error_log`
- 上下文：服务器配置 (server config)，虚拟主机 (virtual host)
- 状态：核心 (core)

`error-log` 指令设置服务器记录其遇到的任何错误错误的文件名。如果文件名不以斜杠 (`/`)开头，则假设它相对于 `ServerRoot`。例如，

```
ErrorLog /dev/null
```

这实际上关闭了错误日志。

## 第 4 章：设置 Web 服务器 249

### Group

语法: `Group unix-group`
默认: `Group #-1`
上下文: 服务器配置
状态:核心

`Group` 指令设置了服务器响应请求时使用的组。为了使用此指令，独立服务器必须最初以 root 身份运行。`unix-group` 既可以是组名，也可以是组 ID（必须以 `#` 开头）。

建议您专门为运行服务器创建一个新组。某些系统管理员使用 `nobody` 用户，但这并不总是可行或符合需求的。如果您以非 root 用户身份启动服务器，它将无法切换到指定的组，而是继续以原始用户的组身份运行。

### IdentityCheck

语法: `IdentityCheck boolean`
默认: `IdentityCheck off`
上下文: 服务器配置，虚拟主机，目录，.htaccess
状态:核心

此指令允许对每个连接进行符合 RFC931 标准的远程用户名记录，前提是客户端机器运行了 `ident` 或类似的程序。这些信息将记录在访问日志中。布尔值为 `on` 或 `off`。

除了基础用法追踪外，不应以任何方式信任此信息。

### KeepAlive

语法: `KeepAlive max-requests`
默认: `KeepAlive 5`
上下文: 服务器配置
状态:核心

此指令启用 Keep-Alive 支持。将 `max-requests` 设置为您希望 Apache 对每个连接处理的最大请求数。设置此限制是为了防止客户端占用您的服务器资源。将其设置为 0 可禁用支持。

根据 HTTP/1.1 草案定义的 HTTP Keep-Alive 扩展允许持久连接。这些长时间的 HTTP 会话允许在同一个 TCP 连接上发送多个请求，在某些情况下，已被证明可以使包含大量图像的 HTML 文档的延迟提升近 50%。

Apache 1.1 默认带有 Keep-Alive 支持。使用 `KeepAlive` 和 `KeepAliveTimeout` 指令（`KeepAliveTimeout` 在下一节介绍）来修改 Apache 的行为。

为了使用 Keep-Alive 支持，第一个浏览器必须支持它。许多当前浏览器包括 Netscape Navigator、Microsoft Internet Explorer 和基于 Spyglass Mosaic 的浏览器，某些基于 Windows 95 的浏览器在支持 Keep-Alive 的服务器上表现异常；它们可能会在连接时挂起。这种现象在连接到任何 Keep-Alive 服务器（不仅仅是 Apache）时在多个 Windows 浏览器中均被观察到。Netscape 3.0b5 及更高版本已知可以解决此问题。

然而，Keep-Alive 支持仅对预先已知长度的文件有效。这意味着大多数 CGI 脚本、服务器端包含文件和目录列表将不会使用 Keep-Alive 协议。这对终端用户来说应该是完全透明的，但 Web 管理员可能需要这一点。

### KeepAliveTimeout

- 语法: `KeepAliveTimeout seconds`
- 默认: `KeepAliveTimeout 15`
- 上下文: 服务器配置
- 状态:核心

这指定了 Apache 在关闭连接之前等待后续请求的秒数。一旦收到请求，将应用 `Timeout` 指令指定的超时值。

### Listen

语法: `Listen [IP address]:port number`
上下文: 服务器配置
状态:核心

`Listen` 指令指示 Apache 监听多个地址或端口；默认情况下，它响应来自所有 IP 接口的请求，但仅限于 `Port` 指令指定的端口。

### `<Limit>`

语法: `<Limit method ... > ... </Limit>`
上下文: 任意
状态:核心

`<Limit>` 和 `</Limit>` 用于封装一组访问控制指令，这些指令仅适用于指定的访问方法，其中 `method` 是任何有效的 HTTP 方法。可以使用除另一个 `<Limit>` 或 `<Directory>` 以外的指令；大多数指令不受 `<Limit>` 的影响。示例：

```
<Limit GET POST>
require valid-user
</Limit>
```
