
如果服务器由 root 启动，则以该账户运行。请确保程序是安全的。

## LogFormat 指令

该指令设置由 TransferLog 指令命名的默认日志文件的格式。如果你在指令行中包含格式的昵称，你可以在其他 LogFormat 和 CustomLog 指令中使用它，而不必重复整个格式字符串。

**语法:** LogFormat format [nickname]

**默认设置:** LogFormat "%h %l %u %t \"%r\" %>s %b"

**上下文:** Server config, virtual host

定义昵称的 LogFormat 指令不会做其他事情；也就是说，它仅定义昵称，并不会实际应用该格式。

## CustomLog 指令

与 TransferLog 指令类似，该指令使你能够将日志信息发送到日志文件或外部程序。与 TransferLog 指令不同的是，它使你能够使用可指定为参数的自定义日志格式。

**语法:** CustomLog file | pipe [format | nickname] [env=[!]environment_variable]

**上下文:** server config, virtual host

例如：

```
CustomLog logs/access.log "%h %l %u %t \"%r\" %>s %b"
```

access.log 文件中的每一行都将使用给定的格式说明符写入。格式指定日志文件每一行的格式。格式可用的选项与 LogFormat 指令参数的选项完全相同。如果格式包含空格（几乎所有情况下都会如此），应将其用双引号括起来。代替实际的格式字符串，你可以使用 LogFormat 指令定义的格式昵称。例如：

```
LogFormat "%h %t \"%r\" %>s" myrecfmt
CustomLog logs/access.log myrecfmt
```

这里 access.log 中的行将采用 myrecfmt 格式。
此外，请注意 TransferLog 和 CustomLog 指令可以在每个服务器中使用多次，以使每个请求都记录到多个文件。例如：

```
CustomLog logs/access1.log common
CustomLog logs/access2.log common
```

这里服务器为每个请求创建两个日志条目，并将每个条目分别存储在 access1.log 和 access2.log 中。除非为每个日志使用不同的格式并且出于不同原因需要每种格式，否则这真的没什么用。

最后，如果你使用 mod_setenvif（默认安装）或 URL 重写模块（mod_rewrite，默认未安装）根据请求 URL 设置环境变量，你可以使用 CustomLog 指令中的 env=[!]environment_variable 选项创建条件日志记录。例如，假设你允许人们下载 PDF 白皮书，并且希望在通常的日志目录中将所有下载记录到名为 whitepaper.log 的日志文件中。以下是必要的配置：

```
SetEnvIf Request_URI \.pdf$ whitepaper
CustomLog logs/whitepaper.log common env=whitepaper
CustomLog logs/access.log common env=!whitepaper
```

在前面的配置中，第一行在请求 URL 以 .pdf 扩展名结尾时设置环境变量 whitepaper。然后在记录条目时，Apache 使用第一个 CustomLog 指令的 env=whitepaper 设置来确定它是否已设置。如果已设置，则使用 common 格式的日志条目会写入 logs/whitepaper.log 文件。当 whitepaper 环境未设置时，日志条目会像往常一样写入 logs/access.log 文件。

## 自定义日志文件

尽管默认的 common 日志格式满足大多数日志需求，有时能够自定义日志数据还是很有用的。例如，你可能想要记录访问你网站的浏览器类型，以便你的 Web 设计团队确定使用何种浏览器特定的 HTML。或者，你可能想知道哪些网站正在发送（即引用）访问者到你的网站。所有这些在 Apache 中都很容易实现。默认日志模块 mod_log_config 支持自定义日志记录。

自定义格式通过该模块的 LogFormat 和 CustomLog 指令设置。LogFormat 和 CustomLog 的格式参数是一个字符串。该格式字符串可以同时包含文字字符和特殊的 % 格式说明符。当在此字符串中使用文字值时，它们会被复制到每个请求的日志文件中。% 说明符 however 会被替换为相应的值。特殊的 % 说明符如表 12-7 所示。

### 表 12-7 日志条目的特殊 % 说明符

| % 说明符 | 描述 |
|---|---|
| %a | 客户端的 IP 地址。 |
| %A | 服务器的 IP 地址。 |
| %B | 发送的字节数，不包括 HTTP 头部，无字节发送时为 0。 |
| %b | 发送的字节数，不包括 HTTP 头部，无字节发送时为 -。 |
| %c | 响应完成时的连接状态。如果客户端在响应完成前中止连接，则写入 'X' 字符。如果客户端使用 keep-alive 协议，则写入 '+' 表示响应后连接在超时前保持活动。写入 '-' 表示响应后连接已关闭。 |
| %{mycookie}C | cookie 名称为 mycookie 的内容。 |
| %D | 完成响应所需的时间（以微秒为单位）。 |
| %{myenv}e | 环境变量 myenv 的内容。 |
| %f | 请求的文件名。 |
| %h | 发出请求的远程主机。 |
| %H | 请求协议（例如，HTTP 1/1）。 |
| %{IncomingHeader}i | IncomingHeader 的内容；即发送到服务器的请求中的头部行。末尾的 i 字符表示这是一个客户端（传入）头部。 |
| %l | 如果启用了 IdentityCheck 指令并且客户端机器运行 identd，则这是客户端报告的身份信息。 |
| %m | 请求方法（GET、POST、PUT 等）。 |
| %{ModuleNote}n | 来自其他模块的 note ModuleNote 的内容。 |
| %{OutgoingHeader}o | OutgoingHeader 的内容；即回复中的头部行。末尾的 o 字符表示这是一个服务器（传出）头部。 |
| %p | 提供请求的端口。 |
| %P | 处理请求的子进程的进程 ID。 |
| %q | 查询字符串。 |
| %r | 请求的第一行。 |
| %s | 服务器对请求返回的状态。注意，当请求被重定向时，此格式说明符的值仍为原始请求状态。如果要存储重定向请求的状态，请改用 %>s。 |
| %t | 请求的时间。时间格式与 CLF 格式相同。 |
| %{format}t | 时间，以 format 给出的形式。你还可以查看 `strftime` 函数的手册页。 |
| %T | 提供请求所需的时间，以秒为单位。 |
| %u | 如果请求的 URL 需要成功的 Basic HTTP 身份验证，则此格式说明符的值为用户名。如果服务器在身份验证尝试后返回 401 状态（身份验证 required），该值可能无效。 |
| %U | 请求的 URL 路径。 |
| %v | 请求所来的服务器或虚拟主机的名称。 |
| %V | 根据 UseCanonicalName 指令的服务器名称。 |

可以在每个前述说明符中包含条件信息。条件可以是某些 HTTP 状态码的存在（或不存在）。例如，假设你想记录所有指向不存在页面的引用 URL。在这种情况下，服务器会生成 404 状态（未找到）头部。因此，要记录引用 URL，你可以使用格式说明符：

```
'%404{Referer}i'
```

类似地，要记录导致异常状态的引用 URL，你可以使用以下说明符：

```
'%!200,304,302{Referer}i'
```

注意使用 ! 字符表示服务器状态列表的缺失。

类似地，要在 CLF 格式说明符末尾包含额外信息，你可以扩展 CLF 格式，其由格式字符串定义：

```
"%h %l %u %t \"%r\" %s %b"
```

例如：

```
"%h %l %u %t \"%r\" %s %b \"%{Referer}i\" \"%{User-agent}i\""
```

此格式规范记录 CLF 格式数据，并在每个日志条目中添加客户端提供头部中的 Referer 和 User-agent 信息。

本节向你展示了在日志文件中添加自定义字段的方法，但如果需要将此数据存储在多个日志文件中怎么办？在下一节中，我将讨论如何使用多个日志文件。

## 使用错误日志

如果不记录错误，你将无法确定 CGI 脚本或目录或文件权限出了什么问题以及错误发生的位置。由于错误日志记录是必须的，因此它在 Apache 服务器的核心中得到支持，而不是在 mod_log_config 等模块中。

ErrorLog 指令使你能够记录 Apache 遇到的所有类型的错误。在本节中，我们将介绍如何将 Apache 错误日志合并到广泛使用的 syslog 设施中。syslog 是记录由守护进程（服务器进程）发送的消息的传统方式。你可能会问：“Apache 是一个守护进程，为什么它不能写入 syslog？”实际上可以。

你需要做的就是用以下内容替换 httpd.conf 配置文件中的现有 ErrorLog 指令

```
ErrorLog syslog
```

然后重启 Apache。使用 Web 浏览器访问 Web 服务器上不存在的页面，并查看 syslog 日志文件，看看是否显示 httpd 条目。你应该查看 /etc/syslog.conf 文件，以了解 httpd 消息会出现在哪里。

例如，列表 12-4 显示了 /etc/syslog.conf。
