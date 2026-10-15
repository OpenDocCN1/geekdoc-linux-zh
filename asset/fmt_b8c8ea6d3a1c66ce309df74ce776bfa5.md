
# DefaultType 是服务器无法通过其他方式（例如从文件名）确定类型时将使用的默认 MIME 类型

## 第 21 节：设置 Web 服务器

```
# extensions。如果你的服务器主要包含文本或 HTML 文档，
# "text/plain" 是一个很好的值。如果大部分内容是二进制文件，
# 例如应用程序或图像，你可能希望使用 "application/octet-
# stream" 流，以防止浏览器尝试将二进制文件
# 显示为文本。
# DefaultType text/plain
```

通过 `mod_mime_magic` 模块，服务器可以提供提示以帮助确定正在请求的文件是什么类型。你必须确保此模块已加载到 Apache 中才能使用它（默认已加载）。该模块可以使用来自 `/usr/share/magic.mime`（默认关闭）和 `/etc/httpd.conf`（默认开启）的提示来确定所请求文件的内容。以下是该模块可使用的指令：

```apache
<IfModule mod_mime_magic.c>
# MIMEMagicFile /usr/share/magic.mime
MIMEMagicFile conf/config
</IfModule>
```

## 设置主机名查找

在 Apache Web 中，你可以让服务器为传入的请求查找地址。开启 `HostnameLookups` 可以实现此功能：

- `# HostnameLookups: 客户端的名称或仅其 IP 地址`

`HostnameLookups Off`

如果开启了 `HostnameLookups` 指令，每个入站连接都会生成一个 DNS 查询，将客户端的 IP 地址翻译为主机名。如果你的网站接收请求，服务器的响应时间可能会受到不利影响。除非你使用日志分析程序或统计包，这些程序需要完全限定域名且无法自行进行查找），否则应该关闭 `HostnameLookups`。随 Apache 分发安装的 `logresolve` 程序可以调度在非高峰时间通过执行主机名查找来编辑日志文件。

## 配置 HTTP 日志

你可以设置多个与 Apache 信息日志相关的值。当指定一个相对路径时，默认会附加由 `ServerRoot` (`/etc/httpd/` ) 设置的目录（例如，`/etc/httpd/logs/error_log`）。如下所示，你可以设置错误日志的位置、日志级别以及一些日志别名：

```
# ErrorLog: 日志文件的位置。
# 如果你没有在 <VirtualHost> 容器内指定 ErrorLog 指令，
# 与该虚拟主机相关的错误消息将记录在此处。
# 如果你*确实*为 <VirtualHost> 容器定义了错误日志文件，
# 则该主机的错误将记录在那里，而不是这里。
ErrorLog logs/error_log
```

## 第四部分：Fedora 和 RHEL 网络与服务器设置

```
# LogLevel: 控制记录到 error_log 中的消息数量。
# 可能的值包括：debug, info, notice, warn, error, crit,
# alert, emerg。

LogLevel warn

# 以下指令定义了一些格式别名，供 CustomLog 
# 指令使用（见下文）。
LogFormat "%h %l u %t %r" %>s %b \"{Referer}i \"%{User-Agent}\"
LogFormat "%h %l u %t %r" %>s %b" common
LogFormat "%{Referer}i -> referer"
LogFormat "%{User-agent}i" agent

# 访问日志文件的位置和格式
# 以下行定义了（供以后使用）四种日志格式：
# 如果你在 <VirtualHost> 容器内定义了任何访问控制，
# 将记录在此处。访问日志的位置和格式
# Common 格式）：
CustomLog logs/access_log common

# 如果你想分开 agent 和 referer，使用以下：
CustomLog logs/access_log referer

# 对于 agent，使用以下：
CustomLog logs/access_log agent

# 你还可以添加第五种格式 combined
CustomLog logs/access_log combined
```

## 第 21 节：设置 Web 服务器

`LogLevel` 控制记录到 `error_log` 中的消息数量。消息的范围从非常详细的 `debug` 级别到非常安静的错误日志。对于 `debug` 级别，每当配置文件被读取、使用访问控制机制或服务器数量发生变化时，都会记录消息。对于 `emerg` 级别，只有系统级故障才会产生恐慌状态。

指定的 `LogLevel` 表示记录的最低程度的消息——该级别及以上的消息将被记录。例如，如果设置为 `warn`，日志将包含 `warn`、`error`、`alert` 和 `emerg` 级别的消息。默认 `warn` 是正常使用的良好选择（它只记录可能需要操作干预的重要事件），但 `info` 和 `debug` 非常适合测试服务器配置或追踪错误。

四行 `LogFormat` 行定义了四种日志格式：`combined`、`common`、`referer` 和 `agent`。你还可以添加第五种格式 `combined`。`LogFormat` 指令中可用的令牌见表 21-5。`LogFormat` 定义可以根据你的个人喜好进行修改，并创建自定义格式。

### 表 21-5：LogFormat 中的可用令牌

| 令牌 | 描述 |
| --- | --- |
| `%a` | 客户端的 IP 地址 |
| `%b` | 发送到客户端的字节数（不包括信息） |
| `%(VAR)e` | 环境变量 `VAR` 的内容 |
| `%f` | 请求 URL 引用的的文件 |
| `%h` | 客户端的主机名 |
| `%(Header)i` | HTTP 请求中指定标头的内容 |
| `%l` | 由 `identd` 守护进程报告（可用），发起请求的客户端用户 |
| `%(Note)n` | 来自不同模块的 Note 消息内容 |
| `%(Header)o` | HTTP 响应中指定标头的内容 |
| `%p` | 接收请求的端口号 |
| `%P` | 来自客户端的实际 HTTP 请求 |
| `%s` | 请求生成的服务器响应状态码 |

## 第四部分：Fedora 和 RHEL 网络与服务器设置

| Token | 描述 |
| --- | --- |
| `%t` | 当前的本地时间和日期。时间格式可以使用 `%(Format)t` 进行更改，其中 `Format` 在 `str(3)` man 页面中有描述。 |
| `%T` | 满足客户端请求所需的秒数。 |
| `%u` | 如果访问控制规则需要用户名和密码验证，这代表客户端提供的用户名。 |
| `%U` | 客户端请求的 URL。 |
| `%v` | 根据域名系统 (`DNS`)，服务器的主机名和域名名。 |
| `%V` | 根据 `ServerName` 指令，处理请求的服务器的主机名和域名名。 |

`通用`（`common`）格式包含了客户端主机名或 IP 地址、由 `ident` 守护进程报告的用户名以及服务器的身份验证方法（如果适用）、发送请求时的本地时间、实际的 HTTP 请求、服务器响应码以及传输的字节数。这种格式是 Web 服务器（以及后来的 FTP 服务器）的事实标准。

为了进行连接跟踪，*引用页*（`referer`）格式存储了链接到刚刚交付文档的 URL（来自同一站点或外部服务器）（相对于 *ServerRoot*）。例如，如果页面 `http://www.example.com/corp/about_us.html` 包含一个指向你主页 `http://my.box.com/linuxguy/bio.html` 的链接，当客户端访问该链接时，`www.mybox.com` 的 `referer` 日志将如下：

```
http://www.example.com/corp/about_us.html -> /linuxguy/bio.html
```

此信息可用于确定每个客户端访问你的站点所采取的路径。

*代理*（`agent`）格式存储了每个传入连接的 `User-agent:` HTTP 标头的内容。该字段通常指示浏览器名称和版本、语言，以及运行浏览器的操作系统或架构。在运行 Fedora 的 Pentium II 上，Mozilla 将产生以下条目：

```
Mozilla/5.0 (X11; Linux i686; rv:1.6)
```

**合**（`combined`）格式将其他三个日志文件格式的所有信息合并到一行中。`combinedio` 格式默认被注释掉，但可以（通过删除 `#` 字符）启用，以便在加载了 `mod_log` 模块的情况下记录实际接收的字节 (`%I`) 和发送的字节 (`%0`)。

# 第 21 节：设置 Web 服务器
