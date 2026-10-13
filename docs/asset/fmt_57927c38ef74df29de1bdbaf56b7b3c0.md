
某些指令用于配置服务器的整体操作。这些指令放置在 `httpd.conf` 配置文件中。有些需要路径名，而其他只需要使用关键字 `on` 和 `off` 打开或关闭。Apache 提供默认的 `httpd.conf` 配置文件。`httpd.conf` 文件已包含这些指令。其中一些前面带有 `#` 符号被注释掉了。您可以通过删除其 `#` 符号来激活指令。许多条目前面都有注释来解释其用途。表 22-4 中列出了几个常用的服务器级指令。以下是 `ServerAdmin` 指令的示例，用于设置用户可以发送管理问题邮件的地址。您将 `you@your.address` 条目替换为您想要用于接收系统管理邮件的地址。默认情况下，它设置为 `root@localhost`。

```
# ServerAdmin: Your address, where problems should be e-mailed.
ServerAdmin you@your.address
```

### 表 22-4：服务器指令

| 指令 | 描述 |
|---|---|
| `AddModule module module ...` | Apache 1.3：启用已编译但未使用的模块（在 Apache 2.0 中已删除）。上下文：服务器配置 |
| `Alias url-path directory-filename` | 启用对存储在本地文件系统中、除文档根目录之外的文档的访问。 |
| `BindAddress saddr` | 将服务器绑定到指定的 IP 地址。如需对侦听的地址和端口进行更精细控制，请使用 `Listen` 指令。（在 Apache 2.0 中已被 `Listen` 指令取代。） |
| `DefaultLanguage MIME-lang` | 指定 `MIME-lang` 为默认文件语言。上下文：服务器配置、虚拟主机、目录、`.htaccess` |
| `DefaultType MIME-type` | 对于无法通过其 MIME 类型映射确定类型的文档的默认类型。 |
| `DocumentRoot directory-filename` | `httpd` 提供文件的目录。默认值：`DocumentRoot /usr/local/apache/htdocs`（Red Hat 系统上为 `/var/www/html`） |
| `Group unix-group` | 设置服务器的组。独立服务器必须最初以 `root` 身份运行。建议您专门为运行服务器设置一个新组。 |
| `HostNameLookups on \| off \| double` | 启用 DNS 查找以便可以记录主机名。`Double` 指双向反向 DNS。 |
| `<IfDefine 参数名> ... </IfDefine>` | `<IfDefine 测试>...</IfDefine>` 部分指定条件指令。如果测试为真，则处理 `IfDefine` 部分内的指令；否则忽略。测试由参数名组成，如果参数已定义，则测试为真；如果未定义，则为假。在参数前添加 `!` 符号，如果参数未定义，则测试为真（非）。 |
| `<IfModule 模块名> ... </IfModule>` | `<IfModule 测试>...</IfModule>` 部分指定条件指令。测试检查模块是否已编译到 Apache 中。如果存在，则为真；如果不存在，则为假。`!模块名` 在模块不存在时为真。 |
| `Include 文件名` | 包含其他配置文件。 |
| `KeepAlive on/off` | 启用持久连接，设为 `"Off"` 以禁用。 |
| `KeepAliveTimeout 秒数` | Apache 在关闭连接前等待另一个请求的秒数。 |
| `Listen [IP 地址:]端口号` | 监听多个 IP 地址或端口。默认情况下，它响应所有 IP 接口上的请求，但仅响应 `Port` 指令指定的端口。上下文：服务器配置 |
| `ListenBacklog 积压值` | 待定连接队列的最大长度。 |
| `LoadFile 文件名 文件名 ...` | 在服务器启动或重启时链接命名的对象文件或库。用于加载某些模块运行所需的额外代码。 |
| `LoadModule 模块 文件名` | 链接对象文件或库文件名，并将名为 `module` 的模块结构添加到活动模块列表中。 |
| `LockFile 文件名` | Apache 编译时使用的锁文件路径。 |
| `MaxClients 数量` | 限制可同时支持的请求数。超出 `MaxClients` 限制的尝试通常会被排队，队列长度基于 `ListenBacklog` 指令。 |
| `MaxKeepAliveRequests 数量` | 当 `KeepAlive` 开启时，限制每个连接允许的请求数。 |
| `Port 数量` | 如果不存在 `Listen` 或 `BindAddress` 指令，`Port` 指令设置服务器监听的网络端口。虚拟主机的端口由 `VirtualHost` 指令设置。 |
| `ServerAdmin 电子邮件地址` | 服务器管理员的电子邮件地址。 |
| `ServerAlias 主机1 主机2 ...` | 为主机设置备用名称，用于基于名称的虚拟主机。 |
| `ServerName` *完全限定域名* | 设置服务器的主机名。这仅用于创建重定向 URL。如果未指定，服务器会尝试从其自身的 IP 地址推导。 |
| `ServerPath` *路径名* | 为主机设置传统 URL 路径名，用于基于名称的虚拟主机。 |
| `ServerRoot` *目录文件名* | 设置服务器所在的目录。 |
| `ServerSignature` *Off \| On \| EMail* | 配置服务器生成的文档（如错误消息）下方的尾注行。 |
| `SetHandler` *处理器名称* | 强制所有匹配的文件通过 *处理器名称* 指定的处理器进行解析。 |
| `User` *unix用户ID* | 指定服务器的用户 ID。独立服务器最初必须以 `root` 身份运行。您可以使用用户名或用户 ID 号。该用户不应有访问系统文件的权限。建议专门创建一个新用户和组用于运行服务器。 |
| `UserDir` *目录/文件名* | 当收到请求用户的文档请求时，设置用户主目录中使用的实际目录。 |
| `Redirect` [ *状态* ] *url路径 url* | 将旧 URL 映射到新 URL。 |
| `ScoreBoardFile` *文件名* | 指定 `ScoreBoardFile` 文件。 |
| `TimeOut` *数量* | 设置接收 GET 请求、接收 POST 和 PUT 请求以及 TCP 数据包传输确认的超时秒数。 |

某些指令需要关于您系统的具体信息。例如，`ServerName` 保存您的 Web 服务器的主机名。指定主机名对于避免不必要的 DNS 查找失败至关重要，这些失败可能会挂起您的服务器。请注意，该条目通过前面的 `#` 注释掉了。只需删除 `#` 并输入您的 Web 服务器的主机名以替代 `new.host.name`。

```
# ServerName allows you to set a hostname which is sent
# back to clients for your server if it's different than the
# one the program would get (i.e. use
# "www" instead of the host's real name).

#ServerName new.host.name
```

在 Red Hat 系统中，标准 Web 服务器安装已经使用 `/var/www` 作为您的 Web 站点目录创建了条目。您可以通过更改相应的指令来根据您的需要定制 Web 站点。`DocumentRoot` 指令确定 Web 页面的主目录。`ServerRoot` 指令指定 Web 服务器配置、错误和日志文件的存储位置。

```
DocumentRoot /var/www/html
ServerRoot /etc/httpd
```

`MaxClients` 指令设置可以同时连接到您服务器的最大客户端数。

`MaxClients 150`

注 您还可以配置 Apache 仅作为代理和/或缓存服务器运行。`httpd.conf` 文件中已包含默认的代理和缓存服务器指令。`Proxy Request`

#### 目录级配置：`.htaccess` 和 `<Directory>`

Apache 最灵活的特性之一是能够配置单个目录。使用 `Directory` 指令，您可以定义仅应用于特定目录的指令块。目录指令列在表 22-5 中。该指令可以放在 `httpd.conf` 或 `access.conf` 配置文件中。您也可以在特定目录内使用 `.htaccess` 文件来保存配置指令。这些指令仅应用于该目录。`".htaccess"` 的名称实际上是通过 `AccessFileName` 指令设置的。如果需要，您可以更改此名称。
