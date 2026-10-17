
默认情况下，Apache 在本地计算机的所有接口上监听 80 端口（用于标准 `http` 服务）和 443 端口（用于安全的 `https` 服务）（这是 Web 浏览器预期发现 Web 内容的位置）。仅监听 `localhost:80` 会将访问限制在本地机器的用户。由非特权用户运行的 Web 服务器通常会绑定到 `8080` 端口（只有 `root` 才能绑定低于 `1024` 的端口）。如果你有多个网络接口卡，你可以限制 Apache 监听的接口（例如，你可以拥有一个仅面向公司 LAN 且不暴露在 Internet 接口上的 Web 服务器）。

### 在 `httpd.conf` 中选择模块

在编译过程中，可以选择单独的 Apache 模块进行动态链接。动态链接的模块除非通过 `LoadModule` 指令明确标识要加载的模块，否则不会随 `httpd` 服务器进程加载到内存中。接下来的代码块使用 `LoadModule` 指令，通过模块名称和模块路径（相对于 `ServerRoot`）选择多个模块加载到内存中。以下文本列出了这些模块的部分列表：

```
#
###### Dynamic Shared Object (DSO) Support
###### Example:
###### LoadModule foo_module modules/mod_foo.so
#
LoadModule auth_basic_module modules/mod_auth_basic.so
LoadModule auth_digest_module modules/mod_auth_digest.so
LoadModule authn_file_module modules/mod_authn_file.so
....
LoadModule file_cache_module modules/mod_file_cache.so
LoadModule mem_cache_module modules/mod_mem_cache.so
LoadModule cgi_module modules/mod_cgi.so
```

Apache 模块通过 `LoadModule` 指令包含在激活模块列表中。`ClearModuleList` 指令从当前激活模块列表中移除所有条目。随 Apache 提供的每个标准模块都在表 20-1 中进行了描述。

**表 20-1：动态共享对象 (DSO) 模块**

| 模块 | 描述 |
| :--- | :--- |
| `mod_actions` | 基于文件的 MIME 类型或请求方法有条件地执行 CGI 脚本。 |
| `mod_alias` | 允许将物理文件系统的一部分重定向和映射为可通过 Web 服务器访问的逻辑实体。 |
| `mod_asis` | 允许在不添加任何 HTTP 头（例如，`Status`、`Location` 和 `Content-Type` 头字段）的情况下传输文件。 |
| `mod_auth_basic` | 提供 HTTP 基本身份验证。它与身份验证模块（如 `mod_authn_file`）和授权模块（如 `mod_authz_user`）结合使用。 |
| `mod_auth_digest` | 提供 MD5 摘要用户身份验证。 |
| `mod_authn_alias` | 允许你创建分配给别名的扩展身份验证提供程序。稍后你可以通过 `AuthBasicProvider` 或 `AuthDigestProvider` 指令引用这些别名。 |
| `mod_authn_anon` | 类似于匿名 FTP，此模块通过使用有效的电子邮件地址作为密码，允许预定义的用户名访问经过身份验证的区域。 |
| `mod_authn_dbd` | 提供对 SQL 表的访问以进行用户身份验证。它允许你使用 `mod_auth_basic` 和 `mod_auth_digest` 前端。 |
| `mod_authn_dbm` | 提供基于用户名/密码对的访问控制。身份验证信息存储在一个 DBM 二进制数据库文件中，密码经过加密。 |
| `mod_authn_default` | 如果未使用其他模块，则提供回退身份验证模块。用户呈现的任何凭据都将被拒绝。 |
| `mod_authn_file` | 通过用户查找明文密码文件提供访问控制（类似于 `mod_authn_dbm`，但没有加密）。 |
| `mod_authn_ldap` | 允许你使用 LDAP 目录存储 HTTP 基本身份验证数据库。 |
| `mod_authz_dbm` | 提供基于组名称的已认证用户的访问控制。身份验证信息存储在一个 DBM 二进制数据库文件中。 |
| `mod_authz_default` | 如果未配置 `mod_authz_user` 或 `mod_authz_groupfile` 等模块，该模块提供回退功能（简单地拒绝授权请求）。 |
| `mod_authz_groupfile` | 提供基于组成员的访问控制。 |
| `mod_authz_host` | 提供基于客户端主机名、IP 地址或其他环境变量特征的访问控制。 |
| `mod_authz_owner` | 在验证用户名和密码后，此模块允许基于所有权访问文件。 |
| `mod_authz_user` | 基于已认证用户是否列在 `Require` 指令中，允许访问文件。 |
| `mod_autoindex` | 实现自动生成的目录索引。 |
| `mod_cache` | 允许缓存本地或代理的 Web 内容。与 `mod_disk_cache` 或 `mod_mem_cache` 模块一起使用。 |
| `mod_cern_meta` | 提供一种模拟 CERN HTTPD 元文件语义的方法。 |
| `mod_cgi` | 控制由 `cgi-script` 处理器解析或 MIME 类型为 `x-httpd-cgi` 的文件执行。`ScriptAlias` 设置默认目录。 |
| `mod_cgid` | 类似于 `mod_cgi`，除了该模块提供一个 `ScriptSock` 指令来命名与 `cgi` 守护程序一起使用的套接字。 |
| `mod_dav` | 提供基于 Web 的分布式创作和版本控制 (`WebDAV`)，使用复制、创建、移动和删除资源来上传 Web 内容。 |
| `mod_dav_fs` | 用于向 `mod_dav` 模块提供文件系统功能，与基于 Web 的分布式创作和版本控制 (`WebDAV`) 一起使用。 |
| `mod_dbd` | 使用 `apr_dbd` 管理 SQL 数据库连接。（`apr_dbd` 框架为不同的 SQL 数据库提供通用 API。） |
| `mod_deflate` | 包含 `DEFLATE` 输出过滤器，在将数据发送到客户端之前对其进行压缩。 |
| `mod_dir` | 如果在引用目录的 URL 中未明确选择文件名，则设置可用于该目录的文件名列表。 |
| `mod_disk_cache` | 启用基于磁盘的存储管理器以与 `mod_proxy` 一起使用。 |
| `mod_dumpio` | 允许记录接收到的所有输入或由 Apache 发送的数据。由于这可能涉及大量数据，因此主要用于调试目的。 |
| `mod_env` | 控制传递给 CGI 脚本的环境变量。 |

### 第四部分 网络

### 表 20-1

| 模块 | 描述 |
| :--- | :--- |
| `mod_expires` | 通过 `Expires` HTTP 头实现对缓存文档的时间限制。 |
| `mod_ext_filter` | 在向客户端交付响应之前，将其通过外部过滤器进行处理。 |
| `mod_file_cache` | 允许缓存频繁请求的静态文件。 |
| `mod_filter` | 允许配置基于上下文的输出过滤。 |
| `mod_headers` | 允许创建和生成自定义 HTTP 头。 |
| `mod_ident` | 允许查询远程主机上兼容 RFC 1413 的守护进程，以请求连接所有者的信息。 |
| `mod_imagemap` | 取代 `imagemap` CGI 程序的功能，用于处理 `.map` 文件。 |
| `mod_include` | 实现服务器端包含（SSI），这是一种在发送给客户端之前由服务器解析的包含条件语句的 HTML 文档。该模块还具备包含一个或多个文件的能力。 |
| `mod_info` | 提供服务器配置的详细摘要，包括活动加载的模块列表以及每个模块中定义的各个指令的当前设置。 |
| `mod_ldap` | 用于加速使用 LDAP 服务器的网站性能。 |
| `mod_logio` | 可用于记录发送和接收的数据字节数。 |
| `mod_log_config` | 允许自定义日志文件中包含信息的格式。 |
| `mod_log_forensic` | 提供对客户请求进行取证日志记录的能力。 |
| `mod_mem_cache` | 与 `mod_cache` 一起使用，提供基于内存的存储。 |
| `mod_mime` | 根据预定义值或文件的 MIME 类型更改文档的处理方式。 |
| `mod_mime_magic` | 类似于 UNIX `file` 命令，该模块尝试根据文件内容的前几个字节来确定文件的 MIME 类型。 |
| `mod_negotiation` | 基于 `Content-Encoding`、`Content-Language`、`Content-Length` 和 `Content-Type` HTTP 头字段，提供文档的条件显示。 |
| `mod_proxy` | 实现 HTTP 1.1 代理/网关服务器。 |
| `mod_proxy_ajp` | 使用 `mod_proxy` 提供对 Apache JServ Protocol（版本 1.3）的支持。 |
| `mod_proxy_balancer` | `mod_proxy` 的扩展，用于处理负载均衡。 |
| `mod_proxy_connect` | `mod_proxy` 的扩展，用于处理 CONNECT 请求。 |
| `mod_proxy_ftp` | `mod_proxy` 的扩展，用于处理 FTP 请求。 |
| `mod_proxy_http` | `mod_proxy` 的扩展，用于处理 HTTP 请求。 |
| `mod_rewrite` | 提供一种灵活且可扩展的方法，用于重定向客户端请求并将传入的 URL 映射到文件系统中的其他位置。 |
| `mod_setenvif` | 根据各种 HTTP 头字段的内容有条件地设置环境变量。 |
| `mod_speling` | 尝试自动纠正请求 URL 中的拼写错误。 |
| `mod_ssl` | 使用 SSL 和 TLS 协议实现加密。 |
| `mod_status` | 提供每个 `httpd` 服务器进程活动的摘要，包括 CPU 和带宽使用水平。 |
| `mod_suexec` | 允许 CGI 脚本以特定用户或组的权限运行。 |
| `mod_unique_id` | 分配 `UNIQUE_ID` 环境变量，为每个请求提供唯一的标识符。 |
| `mod_userdir` | 指定可以包含个人用户 HTML 文档的位置。 |
| `mod_usertrack` | 使用 cookie 跟踪用户通过网站的过程。 |
| `mod_version` | 允许使用 `<IfVersion>` 容器来实现基于版本的配置。 |
| `mod_vhost_alias` | 包含对动态配置的大规模虚拟主机的支持。 |

如果某个模块包含不必要的功能，可以很容易地在上述列表中将其注释掉。事实上，注释掉未使用的模块是一种良好的安全实践。同样，你可能希望通过在列表中包含这些模块来添加第三方模块的功能或特性（例如，`mod_perl` 集成了 Perl 运行时库以加快 Perl 脚本执行速度，或 `mod_php` 提供了嵌入在 HTML 文档中的脚本语言）。

> **注意** 一些模块，包括 `core`、`prefork`、`http_core` 和 `mod_so`，在 CentOS 中被编译进 `httpd` 守护进程。要查看编译到守护进程中的模块列表，请输入 `httpd -l`。

有关每个模块（以及可以在其中定义的指令）的更多信息，可以在服务器的 `http://localhost/manual/mod/` 上找到（前提是你已经安装了 `httpd-manual` 包）。

### 包含特定模块的配置文件

以下行使 Apache 从 `/etc/httpd/conf.d/` 目录加载配置文件。此目录包含与特定模块相关的配置文件。

```
#
###### Load config files from the config directory `/etc/httpd/conf.d`.
#
Include conf.d/*.conf
```

> **交叉引用** 本章后面“配置模块和相关服务 `/etc/httpd/conf.d/`”一节，描述了 `conf.d` 目录中一些你可能感兴趣的配置文件。

### 选择服务器的用户和组

`httpd` 守护进程不必以 `root` 用户运行；它默认不以 `root` 身份运行这一事实使你的系统更安全。通过设置 `User` 和 `Group` 条目，你可以让 `httpd` 守护进程使用与不同用户和组关联的权限运行：

```
###### If you wish `httpd` to run as a different user or group, you must run
###### `httpd` as `root` initially and it will switch.
#
###### User/Group: The name (or `#number`) of the user/group to run `httpd` as.
# 	- On SCO (ODT 3) use "User nouser" and "Group nogroup".
# 	- On HP-UX you may not be able to use shared memory as `nobody`, and
# 	the suggested workaround is to create a user `www` and use that user.
#
###### NOTE that some kernels refuse to setgid(2) (`#group`) or setuid(2) (`#user`)
###### when the value of `(unsigned)` GID is above 60000;
###### don’t use Group `#1` on these systems!
#
User apache
Group apache
```

默认情况下，`apache` 被定义为用户和组。如果你更改 `User` 和 `Group` 指令，你应该指定一个非特权条目。这可以最小化如果网站被入侵时损害的风险。启动的第一个守护进程以 `root` 身份运行。这是必要的，以便将服务器绑定到低编号端口，并切换到由 `User` 和 `Group` 指令指定的用户和组。所有其他进程都在由这些指令定义的用户 ID (UID) 和组 ID (GID) 下运行。

### 设置主服务器的配置

`http` conf 文件的第二节涉及由主服务器（由 `ServerName` 指令定义的那个）处理的指令。换句话说，除非显式为虚拟主机更改，否则这些值被默认服务器和所有虚拟主机使用。要为特定的虚拟主机更改相同的指令，请添加在虚拟主机容器内。

### 设置电子邮件地址

你可以识别一个地址，如果服务器有问题，用户可以发送电子邮件。这是通过 `ServerAdmin` 指令完成的：

```
#
###### `ServerAdmin`: Your address, where problems with the server should be
###### e-mailed. This address appears on some server-generated pages, such
###### as error documents, e.g. `admin@your_domain.com`
#
ServerAdmin you@your.address
```

`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。默认值是 `root@localhost`。

### 设置服务器名称

如果你的服务器名称不是确切的注册主机名或域名，你应该在这里指定你的服务器名称。正如注释指出的，`ServerName` 指令可以设置为不同于机器实际主机名的值。然而，如果服务器要作为公共 Internet 服务器，这个其他名称仍然应在 DNS 中指向你的机器。通常，www 只是机器真实名称的别名（例如，机器可能响应 `www.linuxtoys.net`，但其真实名称可能是 `al.linuxtoys.net`）。

```
ServerName jusebox.linuxtoys.net
```

如果你没有输入有效的服务器名称，Apache 会尝试使用你的主机名作为 `ServerName`。建议在此处显式输入一个 `ServerName`。

### 设置规范名称

使用 `UseCanonicalName` 指令创建自引用 URL，如下所示：

```
###### `UseCanonicalName`: Determines how Apache constructs self-referencing
###### URLs and the `SERVER_NAME` and `SERVER_PORT` variables.
###### When set "Off", Apache will use the Hostname and Port supplied
###### by the client. When set "On", Apache will use the value of the
###### `ServerName` directive.
#
UseCanonicalName Off
```
