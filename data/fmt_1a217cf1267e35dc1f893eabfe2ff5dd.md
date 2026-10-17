
User 和 Group 指令定义了运行 `httpd` 进程组的 UID 和 GID。当 `httpd` 在启动时运行时，它首先以 root 进程身份运行，然后启动一组提供活动 Web 服务的子进程。`httpd.conf` 文件定义的 UID 和 GID 会分配给这些进程。UID 和 GID 应该为 Web 服务器提供尽可能少的系统权限。在大多数 Linux 系统上，这是 `nobody` 组。使用 `nobody` 的替代方案是为 `httpd` 创建一个用户 ID 和组 ID。Red Hat 使用了这种方法，并创建了特殊的用户 `apache` 和特殊的组 `apache`。为 Web 服务器创建特殊的 UID 和 GID 的优势在于，你可以使用组权限来增加额外保护，而不会完全依赖授予 `nobody` 的全访问权限（world permission）。如果你为 Apache 创建了自己的用户和组，请仔细地设置新用户账户的文件权限。（有关文件系统安全的信息，请参阅第 9 章“文件共享”。）

## PerformanceAlive 指令指令

KeepAlive 指令启用或禁用持久连接的使用。如果没有持久连接，客户端每想探索一个链接就必须与服务器建立新连接。由于 HTTP 运行在 TCP 之上，每个连接都需要建立连接，这增加了文件检索的时间。有了持久连接后，服务器会在关闭连接之前等待查看客户端是否有额外的请求。因此，客户端不需要为新文档创建新连接。`KeepAliveTimeout` 定义了服务器持有持久连接的秒数，以等待客户端是否有额外的请求。

`MaxAliveRequests` 定义了在需要新的 TCP 连接之前，在“保持活动”连接上允许接受的最大请求数。默认值为 100。将 `MaxAliveRequests` 设置为 0 允许无限请求。100 是该参数的一个良好值。很少用户会请求 100 次文档传输，该值从合理角度考虑实际上创建了一个持久连接。此外，如果客户端执行了超过 100 次文档传输，可能表明客户端系统存在问题。在这种情况下，要求另一个连接请求是一个好主意。

`Timeout` 定义了服务器等待传输完成的秒数。该值需要足够大以处理你的网站大小以及现代连接的低性能。

### 缓存指令

若干指令控制服务器的缓存。缓存是服务器本地维护的副本。

-   `ProxyRequests`: 设置此选项会将你的服务器转换为代理服务器。默认情况下它是关闭的。

-   `ProxyVia`: 启用 `Via:` 头部，有助于跟踪缓存页面的来源。

-   `CacheRoot`: 定义写入缓存页面的目录。为了避免让用户对该目录可写，请创建一个特殊用户。

-   `CacheSize`: 定义缓存的最大字节数。默认值为 5KB，许多管理员认为 100MB 是一个合理的设置。

-   `CacheInterval`: 定义服务器修剪缓存的时间间隔。以小时为单位定义，默认值为 4。

-   `CacheExpire`: 定义了文档在缓存中保留而不从远程服务器请求新副本的最大小时数。默认为 24 小时。

-   `CacheLastModifiedFactor`: 根据文档的修改时间定义文档缓存的时间。默认因子为 0.1。

-   `CacheDefaultExpire`: 为未提供该值的协议定义默认的缓存过期值。默认为一小时。

-   `NoCache`: 定义一个你不想缓存的页面的服务器主机名列表。

### 定义虚拟主机

虚拟主机允许服务器通过不同的主机名托管多个网站。Red Hat 配置中有一个专门用于虚拟主机的区域，但所有内容都经过了注释。它仅作为示例。要使用虚拟主机，必须首先取消 `NameVirtualHost` 指令的注释以启用基于主机名的虚拟主机。还有基于 IP 的虚拟主机，但那些消耗可用的 IP 地址。基于主机名的虚拟主机是 Apache 开发者推荐的，也是大多数管理员的首选。

在某些 Red Hat 系统上，`NameVirtualHost` 指令是被注释掉的。该行如下：

```
#NameVirtualHost
```

使用第 9 章中的 Linux 权限来保护存储 Web 文档的文件和目录。服务器不需要写权限，但需要对这些文件的读取和执行权限。可执行文件如果设计不当，将始终是一个潜在的安全威胁。

# CGI 和 SSI 威胁

Apache 本身非常可靠且相当安全。对服务器最大的威胁是你或你的用户为服务器执行而编写的代码。这些问题的两个来源是通用网关接口 (CGI) 程序和服务器端包含 (SSI)。

服务器安全面临的最大威胁之一是编写不劣的 CGI 程序。入侵者通过向程序向系统强制发送 shell 命令行来利用糟糕的代码。避免这种情况并同时保留 CGI 程序优势（这些程序可以用 C、Perl、Python 和其他编程语言编写）的唯一方法，就是对你在系统中提供的代码要非常小心。以下是一些需要记住的预防措施：

- 逐一检查 `c-bin` 目录下的所有程序。

- 尝试编写不允许表单用户输入的程序。

- 使用下拉菜单代替键盘输入。

- 限制从用户进入系统的内容。

为了方便检查所有 CGI 脚本，请将它们都放在 `ScriptAlias` 目录中。不要在任何其他目录中允许 `ExecCGI`，除非你确定没有人可以放置你未曾亲自检查过的脚本。（控制 `ExecCGI` 和其他服务器选项的方法将在下一节中介绍。）

服务器端包含（SSI）也被称为服务器解析的 HTML，文件通常具有 `.shtml` 扩展名。这些文件在发送给客户端之前会由服务器处理。这些文件可以包含其他文件或执行脚本文件的代码。如果使用输入来动态修改 SSI 文件，它将受到与 CGI 脚本相同类型的攻击。

SSI 命令嵌入在 HTML 注释中。因此，每个 SSI 命令都以 `<!---->` 开头。SSI 命令列于表 6.2。

# 表 6.2：服务器端包含命令

| 命令 | 用途 |
| :--- | :--- |
| `#config` | 格式化文件大小和时间的显示。 |
| `#echo` | 显示变量。 |
| `#exec` | 执行 CGI 脚本或 shell 命令。 |
| `#lastmod` | 显示文档修改的日期。 |
| `#fsize` | 显示文档的大小。 |
| `#include` | 将另一个文件插入当前文档中。 |

操作服务器最安全的方法是禁用所有的 SSI 处理。除非 `httpd.conf` 文件中的 `Options` 指令指定了 `All` 或 `Includes`，否则这就是默认设置。一种折中方案是允许 SSI，但禁止 `#include` 和 `#exec` 命令，这些是最大的安全威胁。在此设置中，在 `Options` 指令上使用 `IncludesNOEXEC`。

# 目录和文档的服务器选项

`httpd.conf` 文件可以为所有 Web 文档或单独目录中的文档定义服务器控制。`Options` 指令指定了文档允许哪些服务器选项。将 `Options` 指令放在 `Directory` 容器内部会将指令的范围限制在该特定目录。Red Hat Linux 7.2 的配置提供了列表 6.3 所示的示例。

# 列表 6.3：Red Hat httpd.conf 中的活动目录容器

```
<Directory / />
  Options FollowSymLinks
  AllowOverride None
</Directory>
<Directory "/var/www/html/">
  Options Indexes FollowSymLinks
  AllowOverride None
  Order allow,deny
  Allow from all
</Directory>
<Directory "/var/www/icons/">
  Options Indexes MultiViews
  AllowOverride None
  Order allow,deny
  Allow from all
</Directory>
<Directory "/var/www/cgi-bin/">
  AllowOverride None
  Options None
  Order allow,deny
  Allow from all
</Directory>
<Directory /usr/share/doc>
  Order deny,allow
  deny from all
  allow from localhost.localdomain
  Options Indexes FollowSymLinks
</Directory>
```

此配置为五个目录定义了服务器选项控制：根目录 `/`、`/var/www/html/`、`/var/www/icons/`、`/var/www/cgi-bin` 和 `/usr/share/doc`。示例显示了 `Options` 指令的四种可能值：`FollowSymLinks`、`Indexes`、`None` 和 `MultiViews`。`Options` 指令有几种可能的设置：

- `All`：允许使用所有服务器选项。

- `ExecCGI`：允许执行 CGI。

- `FollowSymLinks`：允许服务器跟随符号链接。
