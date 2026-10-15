

## 自定义日志

使用 LogFormat 和 CustomLog 指令，您可以自定义日志记录以添加更多字段并具有不同的详细程度。这些指令使用由字段说明符组成的格式字符串来确定在日志记录中记录的字段。您可以添加任意想要的字段并且按任意顺序排列。字段说明符由百分号 (%) 符号后跟一个标识字符组成。例如，%h 是远程主机的字段说明符，%b 为字节大小，%s 为状态。有关完整列表，请参阅 mod_log_config 模块的文档。表 22-11 列出了其中一些常用的说明符。您应该引用内容可能包含多个单词的字段。引号本身必须用反斜杠引用才能包含在格式字符串中。以下示例是作为 LogFormat 指令实现的通用日志格式：

```
LogFormat "%h %l %u %t \"%r\" %s %b"
```

日志格式中的某些字段说明符可以限定以记录特定信息。%i 说明符记录服务器接收到的请求中的标头行。特定标头行的引用放在 % 和字段说明符之间的花括号内。例如，User-agent 是指示请求中使用的浏览器软件的标头行。要记录 User-agent 标头信息，请使用转换说明符 %{User-agent}i。

为了与 NCSA 服务器保持兼容，Apache 最初实现了 AgentLog 和 RefererLog 指令来记录 User-agent 和 Referer 标头。这些指令后来已被用于 LogFormat 和 CustomLog 指令的限定 %i 字段说明符所取代。Referer 标头记录来自客户端的链接信息，可检测谁可能链接到您的站点。以下是一个符合 NCSA 的日志格式：

```
"%h %l %u %t \"%r\" %s %b" "%{Referer}i" "%{User-agent}i"
```

| 指令 | 描述 |
|---|---|
| CustomLog file-pipe format-or-nickname | 使用指定的格式创建新的日志文件。 |
| ErrorDocument error-code document | 重定向到本地或外部 URL 以处理问题/错误。 |
| ErrorLog filename|syslog[:facility] | 服务器记录错误的文件。 |
| LogFormat format [nickname] | 设置由 TransferLog 指令命名的默认日志文件的格式。默认值：LogFormat "%h %l %u %t \"%r\" %s %b" |
| TransferLog file-pipe | 以最近的 LogFormat 指令定义或默认指定的通用日志格式添加日志文件。 |
| LogLevel level | 调整记录在错误日志中的消息的详细程度。 |

表 22-10 日志指令

| 字段说明符 | 描述 |
|---|---|
| %a | 远程 IP 地址 |
| %A | 本地 IP 地址 |
| %b | 发送的字节数，不包括 HTTP 标头 |
| %{variable}e: | 环境变量的内容 |
| %f | 文件名 |
| %h | 远程主机 |
| %l | 远程登录名（来自 identd，如提供） |
| %m | 请求方法 |
| %P | 为请求提供服务的子进程的进程 ID |
| %r | 请求的第一行 |
| %s | 状态 |
| %t | 时间，采用通用日志格式时间格式（标准英语格式） |
| %u | 远程用户（来自 auth；如果返回状态 (%s) 为 401，则可能为假） |
| %U | 请求的 URL 路径 |
| %v | 为请求提供服务的服务器的规范 ServerName |

## 表 22-11 Apache 日志字段说明符

## 生成和管理日志文件

与其维护一个大型日志文件，您可以使用 CustomLog 或 TransferLog 指令创建多个日志文件。这对于虚拟主机很有帮助，您可能希望为每个主机维护一个单独的日志文件。您使用 LogFormat 指令定义日志记录的默认格式。TransferLog 然后在创建新日志文件时使用此默认值作为其格式。CustomLog 将这两个操作结合起来，使您能够创建新文件并为其定义格式。

```
LogFormat "%h %l %u %t \"%r\" %s %b"
# 使用 LogFormat 格式创建名为 myprojlog 的新日志文件
TransferLog myprojlog
# 使用其自己的格式创建名为 mypicslog 的新日志文件
CustomLog mypicslog "%h %l %u %t \"%r\" %s %b"
```

Apache 提供了两个用于处理和管理日志文件的实用程序。logresolve 将日志文件中的 IP 地址解析为主机名。rotatelogs 在无需杀死服务器的情况下轮换日志文件。您可以指定轮换时间。

> 注意 Apache Web 服务器还可以提供有关服务器活动和配置的详细报告，让您将此信息显示给远程服务器。Location 指令 server-info 将显示 Web 服务器的配置详细信息，而 server-status 指令将显示 Web 进程。页面 server-info 和 server-status 将显示报告，如 http://localhost/server-info。 使用 ExtendedStatus 指令启用详细报告。

