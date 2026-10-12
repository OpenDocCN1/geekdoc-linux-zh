
| `mod_so` | 为共享对象（DSO）提供运行时支持。 |
| `mod_ssl` | 提供 Secure Socket Layer 支持。 |
| `mod_status` | 提供基于 Web 的 server-info 访问。 |
| `mod_throttle` | 限制单个用户的使用量。 |
| `mod_userid` | 为用户 ID 提供支持。 |
| `mod_vhost_alias` | 为虚拟主机提供支持。 |

除了 `LoadModule` 指令外，Red Hat 配置使用 `AddModule` 指令来标识每个模块。这会将模块名称添加到运行时实际加载的模块列表中。模块列表包含所有可选模块——编译到服务器中的模块和动态加载的模块——但核心模块不是可选。例如，要将 `agent_log_module` 添加到模块列表中，请向 `httpd.conf` 中添加以下行：

```
AddModule mod_log_agent.c
```

`AddModule` 指令后面是正在加载模块的源代码。它不是 `LoadModule` 行上的模块名称；而是产生对象模块的源代码文件名，这与对象的扩展名相同。在 `LoadModule` 行中，对象文件名是 `mod_log_agent.so`。在这里，源代码是 `mod_log_agent.c`。可执行模块、共享对象使用 `.so` 扩展，而列表中的 C 语言模块使用 `.c` 扩展。

表 6.1 列出了 Red Hat Linux 7.2 在其示例 `httpd.conf` 文件中使用 `AddModule` 指令标识的模块。

表 6.1：Red Hat 配置中加载的 DSO 模块

| 模块 | 目的 |
| --- | --- |
| `mod_access` | 指定基于主机和域的访问控制。 |
| `mod_actions` | 将 CGI 脚本映射到 MIME 文件类型。 |
| `mod_alias` | 指向文档树之外的目录。 |
| `mod_asis` | 定义不带头部的返回文件类型。 |
| `mod_auth` | 启用用户认证。 |
| `mod_auth_anon` | 启用匿名登录。 |
| `mod_auth_db` | 启用使用数据库认证文件。 |
| `mod_autoindex` | 启用自动生成索引。 |
| `mod_bandwidth` | 设置服务器使用的带宽限制。 |
| `mod_cgi` | 启用执行 CGI 程序。 |
| `mod_dav` | 提供 WebDAV 协议扩展。 |
| `mod_dir` | 控制目录列表的格式。 |
| `mod_env` | 允许 CGI 和 SSI 继承所有 shell 环境变量。 |
| `mod_expires` | 设置 `Expires` 头的日期。 |
| `mod_headers` | 启用自定义响应头。 |
| `mod_imap` | 处理图像映射文件。 |
| `mod_include` | 处理 SSI 文件。 |
| `mod_info` | 启用 server-info 处理程序。 |
| `mod_log_agent` | 指向代理日志文件。 |
| `mod_log_config` | 启用自定义日志格式。 |
| `mod_log_referer` | 指向引用者日志，记录引用你站点的远程站点信息。 |
| `mod_mime` | 为 MIME 文件提供支持。 |
| `mod_negotiation` | 启用 MIME 内容协商。 |
| `mod_perl` | 为 Perl 语言提供支持。 |
| `mod_php` | 为 PHP 语言提供支持。 |
| `mod_php3` | 额外的 PHP 支持。 |
| `mod_php4` | 额外的 PHP 支持 |
| `mod_put` | 支持使用 `PUT` 和 `DELETE` 命令进行文件传输。 |
| `mod_python` | 为 Python 语言提供支持。 |
| `mod_rewrite` | 启用 URI 到文件的映射。 |
| `mod_roaming` | 提供 Netscape 访问支持。 |
| `mod_setenv` | 从客户端信息设置环境变量。 |
| `mod_so` | 为共享对象（DSO）提供运行时支持。 |
| `mod_ssl` | 提供 Secure Socket Layer 支持。 |
| `mod_status` | 提供基于 Web 的 server-info 访问。 |
| `mod_throttle` | 限制单个用户的使用量。 |
| `mod_userid` | 为用户 ID 提供支持。 |
| `mod_vhost_alias` | 为虚拟主机提供支持。 |

### 基本指令

除了 `LoadModule` 指令外，Red Hat 配置使用 `AddModule` 指令来标识每个模块。这会将模块名称添加到运行时实际加载的模块列表中。模块列表包含所有可选模块——编译到服务器中的模块和动态加载的模块——但核心模块不是可选。例如，要将 `agent_log_module` 添加到模块列表中，请向 `httpd.conf` 中添加以下行：

```
AddModule mod_log_agent.c
```

`AddModule` 指令后面是正在加载模块的源代码。它不是 `LoadModule` 行上的模块名称；而是产生对象模块的源代码文件名，这与对象的扩展名相同。在 `LoadModule` 行中，对象文件名是 `mod_log_agent.so`。在这里，源代码是 `mod_log_agent.c`。可执行模块、共享对象使用 `.so` 扩展，而列表中的 C 语言模块使用 `.c` 扩展。

### ServerName

少数指令定义了服务器的基本信息。在示例中，我们使用：

```
ServerName localhost:80
```

`ServerName` 指令定义了服务器监听的主机名和端口。它还用于在错误消息中构建绝对 URL。如果没有指定端口，默认为 80。

### ServerRoot

`ServerRoot` 定义了包含 `httpd` 文件的目录。这与服务器向客户端提供的 `DocumentRoot` 不同。在 Red Hat 以及所有其他系统中，这是 `/etc/httpd`。`conf` 目录包含了配置文件。因此，`httpd.conf` 位于其定义的 `ServerRoot` 下。

### ServerType

`ServerType` 定义了服务器如何启动。如果服务器在启动时从启动脚本启动，则设置为 `standalone`。如果服务器通过 `inetd` 或 `xinet` 按需运行，则 `ServerType` 设置为 `inet`。大多数情况下，服务器的需求很大，因此最好在启动时启动它们。用户可能会在 Linux 桌面上设置一个不经常使用的网站。在这种情况下，通过 `inetd` 或 `xinet` 运行可能更好。

### Port

`Port` 定义了服务器使用的 TCP 端口号。标准号是 80。有时，私有 Web 服务器运行在其他端口。8080 和 8000 是私有网站的流行选择。如果你更改了数字，必须告诉用户私有网站使用的标准端口。

当 `ServerType` 为 `standalone` 时，建议将 `Port` 设置为 80 以外的数字。这是因为 1024 以下的端口是“特权”端口。如果端口是 80，`httpd` 必须以 `root` ID 运行 `inetd`。这是一个潜在的安全问题，因为入侵者可能利用网站获取 `root` 权限。当 `ServerType` 为 `standalone` 时，使用端口 80 是安全的，因为初始 `http` 进程不提供直接的客户端服务。相反，它启动其他不以 `root` 权限运行的 HTTP 守护。

### UseCanonicalName

`UseCanonicalName` 指令控制是否使用 `ServerName` 定义的值。`CanonicalName` 定义了 http 如何处理自引用 URL。当设置为 `on` 时（如 Red Hat 配置所示），将使用 `ServerName` 中的值。如果设置为 `off`，则使用来自客户端的值。如果你的网站使用主机名，你可能希望将其关闭，以便用户看到他们预期的名称。

## 多宿主服务器配置

连接到多个物理网络的 Web 服务器被称为“多宿主服务器”。此类服务器具有多个 IP 地址。如果是这样，系统需要知道它应该监听哪个地址来接收服务器请求。有两种配置选项可以处理这个问题：

- `Bind`：告诉 `httpd` 应该使用哪个地址进行服务器交互。默认值为 `*`，这意味着服务器应该响应发往其任何有效 IP 地址的 Web 请求。如果从命令行上使用了特定地址，则只处理发往该地址的请求。Red Hat 配置中没有显式设置 `BindAddress`。
