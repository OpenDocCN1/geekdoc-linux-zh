

| 指令 | 描述 |
|---|---|
| `<IfDefine [ ]parameter-name ... </IfDefine>` | `<IfDefine test>...</IfDefine>` 部分用于指定条件指令。当测试为真时，`IfDefine` 部分内的指令会被处理，否则被忽略。测试由一个参数名组成，如果参数已定义，则为真；未定义则为假。如果在参数前放置 `!`，则当参数未定义（不存在）时测试为真。 |
| `<IfModule [ ]module-name ... </IfModule>` | `<IfModule test>...</IfModule>` 部分用于指定条件指令。该测试检查某个模块是否已编译进 Apache。如果存在则为真，否则为假。如果模块不存在，则 `!` 模块名为真。 |
| Include filename | 包含其他配置文件。 |
| KeepAlive on/off | 启用持久连接，"Off" 表示禁用。 |
| KeepAliveTimeout seconds | Apache 在关闭连接前等待下一个请求的秒数。 |
| Listen [IP address:]port number | 监听多个 IP 地址或端口。默认情况下，它响应所有 IP 接口上的请求，但仅响应 Port 指令指定的端口。上下文：服务器配置。 |
| ListenBacklog backlog | 待处理连接队列的最大长度。 |
| LoadFile filename filename ... | 在服务器启动或重启时链接指定的目标文件或库。用于加载某些模块运行所需的附加代码。 |
| LoadModule module filename | 链接目标文件或库文件，并将名为 module 的模块结构添加到活动模块列表中。 |
| LockFile filename | 编译 Apache 时使用的锁文件的路径。 |
| MaxClients number | 限制可支持的并发请求数。超出 MaxClients 限制的连接尝试通常会被排队，队列长度上限由 ListenBacklog 指令决定。 |
| MaxKeepAliveRequests number | 当 KeepAlive 开启时，限制每个连接允许的请求数。 |
| Port number | 如果不存在 Listen 或 BindAddress 指令，则 Port 指令设置服务器监听的网络端口。虚拟主机的端口由 VirtualHost 指令设置。 |
| ServerAdmin e-mail address | 服务器管理员的电子邮件地址。 |
| ServerAlias host1 host2 ... | 设置主机的备用名称，用于基于名称的虚拟主机。 |

| 指令 | 描述 |
|---|---|
| ServerName fully qualified domain name | 设置服务器的主机名。仅在创建重定向 URL 时使用。如果未指定，服务器将尝试根据其自身的 IP 地址推断出主机名。 |
| ServerPath pathname | 设置主机的旧版 URL 路径名，用于基于名称的虚拟主机。 |
| ServerRoot directory-filename | 设置服务器所在目录。 |
| ServerSignature Off | On | EMail | 配置服务器生成的文档（如错误消息）底部的页脚行。 |
| SetHandler handler-name | 强制所有匹配的文件通过 handler-name 指定的处理器进行解析。 |
| User unix-userid | 指定服务器的用户 ID。独立服务器最初必须以 root 身份运行。你可以使用用户名或用户 ID 号。该用户应无权访问系统文件。建议你专门建立一个新用户和组来运行服务器。 |
| UserDir directory/filename | 设置当收到对用户文档的请求时，在用户主目录中使用的实际目录。 |
| Redirect [ status ] url-path url | 将旧 URL 映射到新 URL。 |
| ScoreBoardFile filename | 指定 ScoreBoardFile 文件。 |
| TimeOut number | 设置接收 GET 请求、接收 POST 和 PUT 请求以及 TCP 数据包传输确认的超时时间（以秒为单位）。 |

## 表 22-4 服务器指令（续）

某些指令需要关于系统的特定信息。例如，ServerName 保存您的 Web 服务器的主机名。指定主机名很重要，可以避免不必要的 DNS 查找失败，这些失败可能导致服务器挂起。请注意，该条目前面带有 # 注释。只需删除 #，并在 new.host.name 处输入您的 Web 服务器的主机名。

```
# ServerName allows you to set a hostname which is sent
# back to clients for your server if it's different than the
# one the program would get (i.e. use
# "www" instead of the host's real name).

#ServerName new.host.name
```

在 Red Hat 系统上，对于使用 /var/www 作为网站目录的标准 Web 服务器安装，已经预先配置了条目。您可以通过更改相应的指令来按需调整您的网站。DocumentRoot 指令决定

