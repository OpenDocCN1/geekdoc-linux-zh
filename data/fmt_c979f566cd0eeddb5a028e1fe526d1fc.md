
directive option ...

```
某些指令会创建块（blocks）来包含指定特定组件（也称为节 sections）的指令。`<Directory>` 指令用于定义一个块，在该块内你放置仅适用于特定目录的指令。块指令通过匹配的指令和一个终止指令来结束。终止指令通过以斜线开头的同名块定义结束。块指令接受一个参数，指定指令适用的特定对象。例如，`<Directory mydir>` 指令创建一个块，并在其中应用该指令。该块由 `</Directory>` 终止。`<VirtualHost hostname>` 块用于配置特定的虚拟 Web 服务器，而 `</VirtualHost>` 是其终止指令。你放置在该块内的指令将应用于虚拟 Web 服务器。`<Limit method>` 指定你想要限制的访问方法类型，例如 GET 或 POST。位于块内的访问控制指令列出了你对它们所施加的控制措施。
```

`<block-directive option ...>`

directive option ...

directive option ...

`</block-directive>`

通常，指令放置在主配置文件之一中。这些文件中的 `Directory` 指令可用于配置特定目录。然而，任何目录都可以有其自己的 `.htaccess` 文件来仅配置该目录。如果你的站点有目录，或者目录有特殊需求，你可以在 `.htaccess` 文件中配置它们的指令，而向主配置文件中填充针对每个目录的特定指令。你可以控制 `.htaccess` 文件中的哪些指令优于主配置文件中的指令。如果你的站点允许用户控制指令，你可能需要仔细监控或禁用它们对 `.htaccess` 文件的使用。（除非 `AllowOverrides` 指示，否则 `.htaccess` 文件中的指令可能会覆盖标准配置中的指令。）

Apache 服务器的强大之处和灵活性源于它使用模块来扩展其功能。Apache 是一组核心指令来实现的。可以创建包含其他指令定义的模块。这些模块被加载到 Apache 中，允许你为你的服务器使用这些指令。Apache 分发包包含了一组标准模块，你可以在那里下载其他模块并创建自己的模块。例如，`mod_autoindex` 模块处理自动索引目录的指令（见下节描述）。`mod_mime` 模块处理 MIME 类型和处理器指令。模块通过 `LoadModule` 指令加载。你可以在大多数标准模块的 `httpd` 配置文件中找到 `LoadModule` 指令。

```
LoadModule mime_module modules/mod_mime.so
```

Apache 软件包提供的应用程序可用于构建 Apache 扩展模块。通过这些应用程序，你可以用 C 语言编译模块代码，并创建 Apache 可以通过 `LoadModule` 指令加载的动态共享对象。这要求 `mod_module` 是你 Apache 应用的一部分。它包含了广泛的选项，例如用 `-n` 指定模块名称，`-a` 在 `httpd.conf` 文件中添加其条目，以及 `-i` 将模块安装到你的 Web 服务器上。

你可以在 Apache 网站 (`http://apache.org`) 以及位于你站点 Web 根目录下的 Apache 手册中找到 Apache 配置指令的完整列表。在许多系统中，它位于分发版设置的站点默认目录下的 `manual` 子目录（在 Red Hat 上为 `/var/www/manual`）。许多最常用的指令列在表 22-4 中。

## 服务器配置

某些指令用于配置服务器的整体操作。这些指令放置在 `httpd.conf` 文件中。某些指令需要参数，而另一些只需要通过 `on` 和 `off` 关键字开启或关闭。Apache 提供了一个默认的 `httpd.conf` 配置文件。`httpd.conf` 文件已经包含了这些指令，它们前面带有一个 `#` 符号被注释掉了。你可以通过删除 `#` 符号来激活指令。许多关于目的的说明列在表 22-4 中。`ServerAdmin` 指令用于设置接收邮件的地址。

表 22-4：服务器指令

| 指令 | 说明 |
| --- | --- |
| AddModule module ... | Apache 1.3: 启用已编译但未使用的模块（在 2.0 中弃用）。上下文：server config |
| Alias url-path directory-filename | 允许存储在本地文件系统的其他目录。 |
| BindAddress saddr | 将服务器绑定到指定的 IP 地址。如需进一步控制地址和端口，请使用 Listen 指令。 |
| DefaultLanguage MIME-lang | 指定默认的语言。上下文：server config, virtual host, .htaccess |
| DefaultType MIME-type | 对于无法通过 MIME 类型确定文档的默认类型。 |
| DocumentRoot directory-filename | httpd 提供服务的目录：DocumentRoot /usr/local/apache/htdocs /var/www/html |
| Group unix-group | 设置服务器的组。独立服务器最初以该组运行。建议为运行服务器设置新组。 |
| HostNameLookups on\|off\|double | 启用 DNS 查询以便记录主机名。双指的是反向 DNS。 |
| <IfDefine [!]parameter-name> ... </IfDefine> | <IfDefine test>...</IfDefine> 节指定条件指令。Ifdefine 节内的指令在测试为真时处理，否则被忽略。测试由参数名称组成，如果参数定义则为真，未定义则为假。在参数前加 ! 使测试在未定义时为真。 |
| <IfModule [!]module-name> ... </IfModule> | <IfModule test>...</IfModule> 节指定条件指令。测试检查模块是否编译在 Apache 中。如果存在则为真，不存在则为假。! module-name 表示模块不存在时为真。 |
| Include filename | 包含其他配置文件。 |
| KeepAlive on\|off | 启用持久连接，“Off” 禁用。 |
| KeepAliveTimeout seconds | Apache 在关闭连接之前等待另一个请求的秒数。 |
| Listen [IP address:]port number] | 监听多个 IP 地址或端口。默认情况下，它响应所有 IP 接口上的请求，但仅限 Port 指令指定的端口。上下文：server config |
| ListenBacklog backlog | 等待队列的最大长度。 |

| LoadFile filename ... | 当服务器启动或重启时，链接命名对象文件或库中的文件。用于加载某些模块运行所需的额外代码。 |
| LoadModule module filename | 链接对象文件或库文件名中的模块，并将名为 module 的模块结构添加到活动模块列表中。 |
| LockFile filename | Apache 编译时使用的锁文件路径。 |
| MaxClients number | 限制可以支持的并发请求数。任何超过 MaxClients 的连接尝试通常会排队，最多基于 ListenBacklog 指令确定的数量。 |
| MaxKeepAliveRequests number | 在开启 KeepAlive 的情况下，限制每个连接允许的请求数。 |
| Port number | 如果不存在 Listen 或 BindAddress 指令，则 port 指令将设置服务器监听的网络端口。虚拟主机的端口由 VirtualHost 指令设置。 |
| ServerAdmin e-mail-address | 服务器管理员的电子邮件地址。 |
| ServerAlias host1 host2 ... | 为主机设置备用名称，用于基于名称的虚拟主机。 |
| ServerName fully qualified domain name | 设置服务器的主机。这仅在创建重定向 URL 时使用。如果未指定，服务器将尝试从其 IP 地址中推断。 |
| ServerPath pathname | 设置主机的遗留 URL 路径，用于基于名称的虚拟主机。 |
| ServerRoot directory-filename | 设置服务器所在的目录。 |
| ServerSignature Off | On | EMail | 在服务器生成的文档（如错误消息）下方配置一个尾部页脚行。 |
| SetHandler handler-name | 强制所有匹配的文件通过通过 handler 名称进行解析。 |
| User unix-userid | 指定服务器的用户 ID。独立服务器初始必须以 root 身份运行。您可以使用用户名或用户 ID 编号。该用户不应具有访问系统文件的权限。建议您专门为运行服务器设置一个用户名和用户组。 |
| UserDir directory/filename | 当接收到文档请求时，设置用户主目录中使用的实际目录。 |
| Redirect [ status ] url-path | 将任何旧 URL 映射到新 URL。 |
| ScoreBoard filename | 指定 ScoreBoard 文件。 |
| TimeOut number | 设置接收 GET 请求、接收 POST 和 PUT 请求以及 TCP 数据包传输确认的超时时间（秒为单位）。 |

某些指令需要关于您的 Web 服务器的特定信息。例如，ServerName 包含您的 Web 服务器的主机名。指定主机名对于避免可能导致服务器挂起的意外 DNS 查找失败非常重要。注意该条目开头有注释符号 `#`。只需删除 `#` 并在 new.host.name 处输入您的 Web 服务器主机名即可。

```
# ServerName 允许您设置一个主机名，

# 并发送给客户端，如果它与程序获取的

# 名称不同（例如，使用

# "www" 而不是主机的真实名称）。

#ServerName new.host.name
```

在 Hot Hats 上，已经为使用 `/var/www` 或您的站点目录的 Web 服务器安装创建了条目。您可以通过更改适当的指令来根据自己的需求定制 Web 站点。DocumentRoot 指令决定 Web 页的家目录。ServerRoot 指令指定 Web 服务器配置、错误和日志文件的存放位置。

DocumentRoot /var/www/html
ServerRoot /etc/httpd

MaxClients 指令设置同时连接到您的服务器的客户端最大数量。MaxClients 150

您还可以配置 Apache 仅作为代理或缓存服务器运行。默认的代理和缓存服务器指令已包含在 httpd.conf 文件中。ProxyRequests 指令开启代理活动。缓存可以使用 CacheRoot 等指令进行配置，以指定缓存目录，CacheSize 指定缓存大小（默认 500KB），以及 CacheMaxExpire 为未修改的文档设置时间限制。

注意

## 目录级配置：.htaccess 和 <Directory>

Apache 最灵活的方面是配置单个目录。通过 Directory 指令，您可以定义一组仅适用于特定目录的指令块。Directory 指令列在表 22-5 所示。此类指令可以放置在 httpd.conf 或 access.conf 配置文件中。您也可以在特定目录内使用 .htaccess 文件来存放配置指令。这些指令随后仅适用于该目录。"htaccess" 的名称实际上是由 AccessFileName 指令设置的。如果您需要，可以更改它。

AccessFileName .htaccess

### 表 22-5：目录指令

| 指令 | 描述 |
| --- | --- |
| AccessFileName filename filename ... | 位于目录内的默认目录配置文件名。 |
| <Directory> ... </Directory> | <Directory> 和 </Directory> 指令作为标签操作，封装一组仅适用于命名目录及其子目录的指令。 |
| <DirectoryMatch regex> ... </DirectoryMatch> | <DirectoryMatch> 和 </DirectoryMatch> 封装一组仅适用于命名目录的指令。它的操作类似于 <Directory>，但接受正则表达式作为参数。 |
| DirectoryIndex local-url local-url ... | 指定客户端通过在目录名末尾指定 / 请求目录索引时，要查找的资源列表（通常是 index.html）。 |

### Options [+]-option [++]-option ...

控制特定目录中可用的服务器功能。OPTIONS

- **None**: 如果设置为 None，则不启用任何额外功能。
- **All**: 除了 MultiViews 之外的所有选项。这是默认设置。
- **ExecCGI**: 允许执行 CGI 脚本。
- **FollowSymLinks**: 服务器将跟踪该目录中的符号链接。
- **Includes**: 允许服务器端包含。
- **IncludesNOEXEC**: 允许服务器端包含，但禁用 CGI 脚本执行。
- **Indexes**: 为没有 DirectoryIndex 的目录返回格式化后的目录列表。
- **MultiViews**: 允许内容 MultiViews。
- **SymLinksIfOwnerMatch**: 服务器仅跟踪目标文件或目录由同一用户拥有的符号链接。

### AllowOverride override ...

在配置文件或上级目录中通过指令所做的配置会被下级目录继承。允许 .htaccess 文件和 <Directory> 块中的特定指令覆盖这些配置。此功能可以通过 AllowOverride 指令控制。使用 all 参数时，htaccess 可以覆盖之前的任何配置。使用 none 参数则禁止覆盖。您可以进一步控制对特定指令组的覆盖。AuthConfig 允许使用授权指令，FileInfo 用于类型指令，Indexes 用于索引，Limit 用于访问控制，Options 用于 *options* 指令。

**Directory 块以 `<Directory path>` 开始，其中 *path* 是要配置的目录。结束指令使用 `<` 符号，并在 Directory 一词前有一个斜杠：`</Directory>`。在此块内的指令仅适用于指定的目录。以下示例阻止了来自 www.myviews.com 的请求对 mypics 目录的访问。

```
<Directory /var/www/mypics>

Order Deny,Allow

Deny from www.myviews

</Directory>
```

通过访问控制指令（如 `allow` 和 `deny`），你可以控制远程用户和主机对你网站的访问。访问控制指令如表 22-6 所示。`allow` 指令后跟一个主机列表，将限制仅允许这些主机访问。`deny` 指令后跟一个主机列表，则将拒绝来自这些系统的访问。该参数适用于所有主机。访问控制指令的执行顺序非常重要。其他控制指令（如 `require`）可以建立身份验证，要求用户登录。其他访问控制指令可以全局使用以控制整个站点，也可以放置在 `Directory` 指令中以控制单个目录的访问。在下面的示例中，允许所有用户访问：

```
order allow,deny

allow from all
```
