
**表 23.3（续）**

| 指令名称 | 描述 |
|---|---|
| `deny from` | 指定不允许访问此目录及其子目录的主机名或 IP 地址。主机之间以空格分隔列出，遵循以下规则：特殊关键字 `all` 允许所有客户端访问；可以使用主机名的尾部来匹配所有以该尾部结尾的主机（如 `cnn.com`）；可以使用 IP 地址的前缀部分来匹配所有以该前缀开头的 IP 地址（如 `192.168.147`），或者使用一个 `<network address>/<network mask>` 对。 |
| `Options` | 指定在该目录及其子目录中启用的服务器选项。可能的值有：`None`（不启用任何选项）、`All`（启用所有选项）、`ExecCGI`（可以执行 CGI 脚本）、`FollowSymLinks`（可以跟随符号链接）、`Includes`（允许服务器端包含）、`IncludesNOEXEC`（允许服务器端包含，但 `#exec` 和 `#include` 除外）、`Indexes`（允许目录列表）、`SymLinksIfOwnerMatch`（仅当目标文件或目录与链接本身具有相同所有者时，才可以跟随符号链接），以及 `MultiViews`（应根据文档的语言进行内容协商）。该指令的值中可以包含由空格分隔的多个选项列表。 |
| `order` | 指定 `allow` 和 `deny` 指令的处理顺序。可能的值有：`deny,allow`（先评估 deny 指令，再评估 allow 指令）、`allow,deny`（先评估 allow 指令，再评估 deny 指令），以及 `mutual-failure`（只允许出现在 allow 列表中且不出现在 deny 列表中的主机）。 |

这些指令也可以用于本地访问控制文件（如 `.htaccess`），以覆盖 `access.conf` 中的设置，前提是 `access.conf` 中的 `AllowOverride` 指令允许这样做。

> **注意：**请记住，子目录中的访问配置会覆盖父目录中的配置。因此，在使用多个 `<Directory ...>` 块时，必须确保系统中所有目录都已设置必要的访问控制设置。

## 一个典型的 `access.conf` 文件

Apache Web 服务器的一个典型 `access.conf` 文件可能如下所示：

```apache
<Directory />
Options None
AllowOverride None
</Directory>

<Directory /home/httpd/html>
Options Indexes Includes FollowSymLinks
AllowOverride None
order allow,deny
allow from all
</Directory>

<Directory /home/httpd/cgi-bin>
AllowOverride None
Options ExecCGI
</Directory>

<Directory /usr/doc>
order deny,allow
deny from all
allow from localhost
Options Indexes FollowSymLinks
</Directory>
```

> **注意**
>
> access.conf 文件通常包含大量描述条目及其用途的注释。为了本书表述简洁清晰，这些注释已被删除。与大多数 Linux 配置文件一样，注释以井号（#）开头，直到行尾。

## APACHE 模块

Apache 提供了在启动时动态加载预编译模块的能力，而无需将这些模块编译进 httpd 二进制文件本身。Apache 随附了大量此类预编译二进制文件，它们提供了 Apache 的大部分功能，包括访问控制、目录别名和授权。表 23.4 概述了这些模块。

**表 23.4 — Apache 预编译模块**

| 模块名称 | 功能 |
|---|---|
| `mod_access` | 根据客户端的主机名或 IP 地址提供访问控制。 |
| `mod_actions` | 通过 HTTP 请求头的文件 MIME 类型提供 CGI-BIN 脚本支持。 |
| `mod_alias` | 提供创建目录别名的能力。 |
| `mod_asis` | 提供无需标准 HTTP 头即可向浏览器发送文档的能力。 |
| `mod_auth` | 针对包含用户帐户的标准 Apache htpasswd 文本文件提供基本 HTTP 认证。 |
| `mod_auth_anon` | 以类似 FTP 匿名访问的方式，提供对受认证区域的匿名访问。 |
| `mod_auth_db` | 针对存储在 Berkeley DB 文件中的用户帐户提供基本 HTTP 认证。 |
| `mod_auth_dbm` | 针对存储在 DBM 文件中的用户帐户提供基本 HTTP 认证。 |
| `mod_auth_external` | 使用外部程序执行实际授权，提供基本 HTTP 认证。 |
| `mod_autoindex` | 控制 Apache 生成自动目录索引的方式。 |
| `mod_cern_meta` | 提供对附加元信息（如附加 HTTP 头）的支持。 |
| `mod_cgi` | 提供 CGI-BIN 脚本支持。 |
| `mod_digest` | 使用 MD5 摘要认证方案提供用户认证。 |
| `mod_dir` | 提供重定向任何不包含尾部斜杠的目录请求的能力。 |
| `mod_env` | 提供将环境变量传递给 CGI-BIN 脚本或服务器端包含文件的能力。 |
| `mod_expires` | 控制 Apache 对 Expires HTTP 头的处理。 |
| `mod_headers` | 提供操作 HTTP 头的能力。 |
| `mod_imap` | 提供图像映射支持。 |
| `mod_include` | 提供服务器端包含支持。 |
| `mod_info` | 提供服务器运行和状态的概览。 |
| `mod_log_agent` | 提供在日志文件中存储用户代理信息的能力。 |
| `mod_log_config` | 提供控制日志条目格式的能力。 |
| `mod_log_referer` | 提供在日志文件中存储传入 Referer 头的能力。 |
| `mod_mime` | 向客户端提供关于文件的元信息。 |
| `mod_mime_magic` | 提供通过 magic 文件确定文件 MIME 类型的能力。 |
| `mod_negotiation` | 提供内容协商支持。 |
| `mod_proxy` | 提供 HTTP 代理功能。 |
| `mod_rewrite` | 提供 URL 重写功能。 |
| `mod_setenvif` | 提供创建自定义环境变量以供后续决策使用的能力。 |
| `mod_spelling` | 提供处理客户端请求的 URL 拼写错误和大小写错误的能力。 |
| `mod_status` | 提供通过 Web 监控 Apache 服务器状态的能力。 |
| `mod_unique_id` | 为每个请求提供唯一 ID。 |
| `mod_usertrack` | 提供 HTTP Cookie 支持。 |

这些模块中的每一个在 `httpd.conf` 文件中启用后，都会提供可用于配置该模块功能的配置指令。有关这些指令的完整详细信息以及这些模块的用法，请参阅 Apache 文档，网址为 `http://www.apache.org/`。

> **注意**
>
> Apache 有大量第三方模块可用。位于 `http://modules.apache.org/` 的 Apache 模块注册表是获取这些模块的良好来源。

## 管理 Apache

Apache Web 服务器通常需要执行几项管理任务，包括：

- 启动服务器
- 停止服务器
- 重启服务器
- 检查服务器状态
- 测试服务器配置文件

### 启动服务器

只需启动 `httpd` 守护进程即可启动 Apache 服务器，该守护进程通常位于 `/usr/sbin/` 目录中：

```bash
# /usr/sbin/httpd
```

请以 root 用户身份启动 Apache。Apache 将使用 `httpd.conf` 文件中指定的用户和组继续启动守护进程以监听连接。

如果你的 Apache 配置文件不在 Apache 安装的默认位置，或者你想确保 Apache 使用正确的文件，请使用 `-f` 标志指定你的 `httpd.conf` 文件的路径：

```bash
# /usr/local/apache/httpd -f /usr/local/apache/conf/httpd.conf
```

