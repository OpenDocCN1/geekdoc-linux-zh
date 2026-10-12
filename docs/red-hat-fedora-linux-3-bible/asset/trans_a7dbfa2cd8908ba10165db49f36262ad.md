
## 动态共享对象（DSO）模块

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
| `mod_cgi` | 控制由 "cgi-script" 处理器解析或 MIME 类型为 `x-http-cgi` 的文件执行。ScriptAlias 设置默认目录。 |
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
| `mod_usertrack` | 使用 cookie 跟踪用户通过网站浏览的进度。 |
| `mod_vhost_alias` | 包含对动态配置的大规模虚拟主机的支持。 |

有关每个模块（以及可以在其中定义的指令）的更多信息可以在我们位于 http://localhost/manual/mod/ 的服务器上找到。

## 设置主服务器配置

`http.conf` 文件的第二部分涉及由主服务器处理的指令。换句话说，除非在虚拟主机定义中进行了更改，否则这些值在所有情况下都有效。要为特定的虚拟主机更改相同的指令，请将它们添加在虚拟主机容器内。

## 选择服务器的用户和组

`httpd` 守护进程不必以 root 用户身份运行；实际上，如果它不以 root 身份运行，系统的安全性会更高。通过设置 User 和 Group 条目，您可以让 `httpd` 守护进程使用与不同用户和组关联的权限运行。

```
# 如果您希望 httpd 以不同的用户或组运行，您必须
# 最初以 root 身份运行 httpd，然后它会进行切换。
#
```

### 第四部分：Fedora 网络和服务器设置

```
# User/Group：以该用户/组运行 httpd 的名称（或 #数字）。
#       . 在 SCO (ODT 3) 上使用 "User nouser" 和 "Group nogroup"。
#       . 在 HP-UX 上，您可能无法以 nobody 身份使用共享内存，
#       建议的变通方法是创建一个用户 www 并使用该用户。
# 请注意，某些内核拒绝在 (unsigned)Group 的值超过 60000 时
# 设置 setgid(Group) 或 semctl(IPC_SET)；
# 在这些系统上不要使用 Group #-1！
#
User apache
Group apache
```

默认情况下，apache 被定义为服务器的用户和组。如果您更改 **User** 和 **Group** 指令，应指定一个非特权实体。这可以将站点被入侵时的损坏风险降至最低。启动的第一个守护进程以 root 身份运行。这是必要的，以便将服务器绑定到低编号端口，并切换到由 **User** 和 **Group** 指令指定的用户和组。所有其他进程都在这些指令定义的用户 ID (UID) 和组 ID (GID) 下运行。

## 选择 HTTP 端口号

Apache 在特定端口上监听 HTTP 请求。使用的端口由 **Port** 条目设置如下：

```
# Port：独立服务器监听的端口。对于
# 端口 < 1023，您需要最初以 root 身份运行 httpd。
#
Port 80
```

端口 80 是 HTTP 流量的默认值，这就是为什么 `http://www.apache.org:80/` 与 `http://www.apache.org/` 相同的原因。如果服务器绑定到不同的端口，则必须在 URL 中指定端口号。大多数 Web 服务器运行在端口 80 上，尽管它们可以接受任何未绑定到特定服务的端口（最高 65535）的连接（有关常见服务和协议及其使用端口的列表，请参阅 `/etc/services` 文件）。只有 root 才能运行监听特权端口（1024 以下端口）上连接的程序。

## 设置电子邮件地址

您可以指定一个地址，以便当服务器出现问题时用户可以创建电子邮件。这是通过 **ServerAdmin** 指令完成的：

```
# ServerAdmin：您的地址，服务器出现问题的电子邮件发送处。
# 该地址显示在服务器生成的某些页面上，例如
# 错误文档，例如 admin@your-domain.com
#
ServerAdmin you@your.address
```

