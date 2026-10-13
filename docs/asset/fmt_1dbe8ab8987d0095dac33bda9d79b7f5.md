
以下行使 Apache 从 `/etc/httpd/conf.d` 目录加载配置文件。此目录包含与特定模块关联的配置文件。

```text
# Load config files from the config directory "/etc/httpd/conf.d".
#   Include conf.d/*.conf
```

> **交叉引用：** 本章后面的“配置模块 (`/etc/httpd/conf.d/*.conf`)”部分描述了 `conf.d` 目录中您可能感兴趣的一些配置文件。

### 在 httpd.conf 中选择模块

在编译过程中，可以选择单独的 Apache 模块进行动态链接。动态链接的模块不会加载到内存中的 httpd 服务器进程中，除非 `LoadModule` 指令明确标识要加载的模块。接下来的代码块通过使用 `LoadModule` 指令以及模块名称和模块路径（相对于 `ServerRoot`）来选择几个模块以加载到内存中。以下文本显示了这些模块的部分列表：

```text
# Dynamic Shared Object (DSO) Support
# Example:
# LoadModule foo_module modules/mod_foo.so
#
LoadModule access_module modules/mod_access.so
LoadModule auth_module modules/mod_auth.so
LoadModule auth_anon_module modules/mod_auth_anon.so
LoadModule auth_dbm_module modules/mod_auth_dbm.so
LoadModule auth_digest_module modules/mod_auth_digest.so
LoadModule include_module modules/mod_include.so
LoadModule log_config_module modules/mod_log_config.so
LoadModule env_module modules/mod_env.so
LoadModule mime_magic_module modules/mod_mime_magic.so
...

LoadModule actions_module modules/mod_actions.so
LoadModule speling_module modules/mod_speling.so
LoadModule userdir_module modules/mod_userdir.so
LoadModule alias_module modules/mod_alias.so
LoadModule rewrite_module modules/mod_rewrite.so
```

通过 `LoadModule` 指令将 Apache 模块包含在活动模块列表中。`ClearModuleList` 指令从当前活动模块列表中删除所有条目。Apache 随附的每个标准模块都在表 21-1 中进行了描述。

### 动态共享对象（DSO）模块

如果某个模块包含不必要的功能，可以很容易地在上述列表中将其注释掉。同样，您可能希望通过在列表中包含这些模块来添加第三方模块的功能或特性（例如，`mod_perl` 集成了 Perl 运行时库以加快 Perl 脚本的执行速度，或者 `mod_php` 提供了一种嵌入在 HTML 文档中的脚本语言）。

| 模块 | 描述 |
| :--- | :--- |
| `mod_access` | 提供基于源主机名/IP 地址的访问控制。 |
| `mod_actions` | 根据文件的 MIME 类型或请求方法有条件地执行 CGI 脚本。 |
| `mod_alias` | 允许将物理文件系统的部分重定向和映射为可通过 Web 服务器访问的逻辑实体。 |
| `mod_asis` | 允许在不添加任何 HTTP 头部（例如 Status、Location 和 Content-type 头字段）的情况下传输文件。 |
| `mod_auth` | 提供基于用户名/密码对的访问控制。认证信息存储在纯文本文件中，尽管密码是使用 `crypt()` 系统调用加密的。 |
| `mod_auth_anon` | 类似于匿名 FTP，此模块允许预定义的用户名通过使用有效的电子邮件地址作为密码来访问经过认证的区域。 |
| `mod_auth_dbm` | 提供基于用户名/密码对的访问控制。认证信息存储在 DBM 二进制数据库文件中，密码经过加密。 |
| `mod_auth_digest` | 提供 MD5 摘要用户身份验证。 |
| `mod_auth_ldap` | 允许您使用 LDAP 目录来存储 HTTP Basic 认证数据库。 |
| `mod_autoindex` | 实现自动生成的目录索引。 |
| `mod_cache` | 允许缓存本地或代理的 Web 内容。与 `mod_disk_cache` 或 `mod_file_cache` 模块配合使用。 |
| `mod_cern-meta` | 提供一种模拟 CERN HTTPD 元文件语义的方法。 |
| `mod_cgi` | 控制由 "cgi-script" 处理器解析或 MIME 类型为 `x-http-cgi` 的文件执行。`ScriptAlias` 设置默认目录。 |
| `mod_dav` | 提供基于 Web 的分布式创作和版本控制（WebDAV），用于通过复制、创建、移动和删除资源来上传 Web 内容。 |
| `mod_dav_fs` | 用于向 *mod_dav* 模块提供文件系统功能。 |
| `mod_deflate` | 包含 DEFLATE 输出过滤器，用于在发送到客户端之前压缩数据。 |
| `mod_dir` | 设置当 URL 引用目录且未明确选择文件名时可能使用的文件名列表。 |
| `mod_disk_cache` | 启用磁盘存储管理器，供 *mod_proxy* 使用。 |
| `mod_env` | 控制传递给 CGI 脚本的环境变量。 |
| `mod_expires* | 通过使用 *Expires* HTTP 头实现对缓存文档的时间限制。 |
| `mod_file_cache` | 允许缓存频繁请求的静态文件。 |
| `mod_headers` | 允许创建和生成自定义 HTTP 头部。 |
| `mod_imap` | 控制内联图像映射文件，这些文件的 MIME 类型为 x-http-imap 或由 imap 处理器解析。 |
| `mod_include` | 实现服务器端包含（SSI），即包含在发送到客户端之前由服务器解析的条件语句的 HTML 文档。此模块还具备将一个文件包含到另一个文件中的能力。 |
| `mod_info` | 提供服务器配置的详细摘要，包括活动加载模块的列表以及每个模块内定义的每个指令的当前设置。 |
| `mod_ldap` | 用于提高使用 LDAP 服务器的网站性能。 |
| `mod_log_config` | 允许自定义日志文件中包含信息的格式。 |
| `mod_mem_cache` | 与 *mod_cache* 配合使用以提供基于内存的存储。 |
| `mod_mime` | 根据预定义值或文件的 MIME 类型改变文档的处理方式。 |
| `mod_mime_magic` | 类似于 UNIX *file* 命令，此模块尝试根据文件内容的前几个字节来确定文件的 MIME 类型。 |
| `mod_negotiation` | 提供基于 Content-Encoding、Content-Language、Content-Length 和 Content-Type HTTP 头字段的文档条件显示。 |
| `mod_proxy` | 实现 HTTP 1.1 代理/网关服务器。 |
| `mod_proxy_connect` | `mod_proxy` 的扩展，用于处理 CONNECT 请求。 |
| `mod_proxy_ftp` | `mod_proxy` 的扩展，用于处理 FTP 请求。 |
| `mod_proxy_http` | `mod_proxy` 的扩展，用于处理 HTTP 请求。 |
| `mod_rewrite` | 提供灵活且可扩展的方法来重定向客户端请求并将传入的 URL 映射到文件系统中的其他位置。 |
| `mod_setenvif` | 根据各种 HTTP 头字段的内容有条件地设置环境变量。 |
| `mod_speling` | 尝试自动更正请求 URL 中的拼写错误。 |
| `mod_ssl` | 使用 SSL 和 TLS 协议实现加密。 |
| `mod_status` | 提供每个 httpd 服务器进程活动的摘要，包括 CPU 和带宽使用情况。 |
| `mod_suexec` | 允许 CGI 脚本以特定用户或组的权限运行。 |
| `mod_userdir` | 指定可以包含各个用户 HTML 文档的位置。 |
