

满足 All（默认值）或 Any 指令。当 `satisfy` 设置为 `All` 时，在提供资源之前必须满足访问控制方法。如果 `satisfy` 设置为 `Any`，只要满足任一访问条件就会提供资源。

这里另一个访问控制示例，再次使用之前的 server-status 示例。这次结合了访问方法，使得允许来自 Gnulix 域的所有用户访问，而该域之外的用户在获得访问之前必须验证身份。
你可以通过以下方式实现：

```
<Location /server-status>
SetHandler server-status
Order deny,allow
Deny from all
Allow from gnulix.org
AuthType Basic
AuthName "Server status"
AuthFile *gnulixusers
Require valid-user
Satisfy Any
</Location>
```

还有更多方法可以保护 Web 服务器上的内容，但这里讨论的方法让你入门，并且对于大多数情况可能已经足够。请参考 Apache 的在线文档以获取更多如何保护网站区域的示例。

## Apache 模块

Apache 核心功能相对较少；Apache 通过模块获取功能。每个模块通过添加必要的功能来解决定义良好的问题。通过添加或移除模块来提供你希望 Apache 拥，你可以定制 Apache 服务器以满足你的精确需求。

基础 Apache 服务器包含了近 50 个核心模块。其他开发人员还可以提供更多模块。Apache 模块注册（Apache Module Registry）是 Apache 附加模块的仓库，可以在 http://modules.apache.org 找到。模块列在 `/etc/httpd/` 目录中，但该目录是指向模块所在 `/usr/lib/httpd` 模块目录的链接：

| mod_access.so | mod_cern_meta.so | mod_log_config.so | mod_setenvif.so |
| mod_actions.so | mod_cgi.so | mod_mime_magic.so | mod_speling.so |
| mod_alias.so | mod_dav_fs.so | mod_mime.so | mod_ssl.so |
| mod_asis.so | mod_dav.so | mod_negotiation.so | mod_status.so |
| mod_auth_anon.so | mod_dir.so | mod_perl.so | mod_suexec.so |
| mod_auth_dbm.so | mod_env.so | mod_proxy_connect.so | mod_unique_id.so |
| mod_auth_digest.so | mod_expires.so | mod_proxy_ftp.so | mod_userdir.so |
| mod_auth_mysql.so | mod_headers.so | mod_proxy_http.so | mod_usertrack.so |
| mod_auth_pgsql.so | mod_imap.so | mod_proxy.so | mod_vhost_alias.so |
| mod_auth.so | mod_include.so | mod_python.so | mod_autoindex.so |
| mod_info.so | mod_rewrite.so | |

每个模块都添加了可以在配置文件文件中使用的指令。正如你猜想的，额外的命令、开关和选项太多，无法在本章中描述所有的它们。接下来的章节简要描述了 Red Hat Apache 安装中提供的这些模块。

## mod_access

mod_access 通过 IP 地址、主机名或环境变量控制对 Web 服务器某些区域的访问。例如，你可能希望允许来自自己域的任何人访问 Web 的某些区域。更多信息请参阅“文件系统认证与访问控制”部分。

## mod_alias

mod_alias 处理传入 HTTP 请求的 URL，例如将客户端请求重定向到另一个 URL。它还可以将文件系统的部分映射到你的 Web 层级结构中。例如，

```
Alias /images/ /home/wsb/graphics/
```

任何以 /images/ 开头的 URL 都将从 /home/wsb/graphics/ 目录获取内容。这是在客户端完全不知道的情况下完成。如果你使用重定向，客户端将被指示去另一个 URL 查找请求的内容。更高级的 URL 操作可以通过 mod_rewrite 完成。

## mod_asis

mod_asis 用于详细指定要包含在响应中的所有信息。这将完全跳过 Apache 可能会向响应中添加的标头。所有带有 .asis 扩展的文件都将直接发送给客户端，而不进行任何更改。

作为一个 mod_asis 使用的简短示例，假设你已经将网站上的内容从一个位置移动到另一个位置。你必须告知尝试访问此资源的人它已移动，并自动将他们重定向到新位置。为了提供这些信息和重定向，可以在带有 .asis 扩展的文件中添加以下代码：

```
Status: 301 No more old stuff!
Location: http://gnulix.org/newstuff/
Content-type: text/html

```

<HTML>
<HEAD>
<TITLE>We've moved...</TITLE>
</HEAD>
<BODY>
<P>We've moved the old stuff and now you'll find it at:</P>
<A HREF="http://gnulix.org/newstuff/">New stuff</a>!.
</BODY>
</HTML>
```

## mod_auth

mod_auth 使用简单的用户认证方案（称为 Basic 认证），基于在文本文件中存储用户名和加密后的密码。该文件看起来非常像 Unix 的 /etc/passwd 文件。该文件通过 htpasswd 工具创建。更多信息请参阅“文件系统认证与访问控制”。

## mod_auth_anon

mod_auth_anon 模块为用户提供匿名凭证。这对于公共信息很有用。

## mod_auth_dbm

mod_auth_dbm 使用 DB 代替文本来存储用户信息。这比使用纯文本更安全。

## mod_auth_digest

mod_auth_digest 使用 MD5 哈希密码。这比 Basic 认证更安全，因为密码不会通过网络传输。

## mod_auth_mysql

mod_auth_mysql 使用 MySQL 数据库存储用户信息。这允许通过数据库管理用户。

## mod_auth_pgsql

mod_auth_pgsql 使用 PostgreSQL 数据库存储用户信息。这与 mod_auth_mysql 类似。

## mod_imap

mod_imap 提供对图像映射文件的服务器处理。可点击区域定义在 .map 文件中。在 .map 文件可以使用六种指令。指令用于描述布局以及它们指向的 URL。

## mod_include

mod_include 在你的服务器上启用服务器包含。关于如何使用 SSI 的更多信息请参见本章后面的“动态内容”。

## mod_info

mod_info 提供有关服务器配置的全面信息。例如，它将显示所有安装的模块以及配置文件中使用的指令。

## mod_autoindex

mod_autoindex 模块在请求目录且不存在索引文件时创建文件列表。

## mod_cgi

mod_cgi 允许在你的服务器上执行 CGI 程序。

## mod_dir

mod_dir 控制传递给 CGI 的环境变量。

## mod_expires

mod_expires 用于为内容添加过期日期。这对于缓存很有用。

## mod_headers

mod_headers 用于操作你响应的标头。你可以根据需要添加、合并或删除标头。

## mod_proxy

mod_proxy 为 Apache 服务器实现代理和缓存功能。它可以代理缓存 FTP、CONNECT、HTTP/0.9 和 HTTP/1.0 请求。对于拥有大量用户并产生极高代理和缓存需求的站点来说，这不是理想的解决方案。对于少量用户，这里足够。

## mod_rewrite

mod_rewrite 是 URL 操作的瑞士军刀。它允许你使用强大的正则表达式执行任何可以想象的 URL 操作。它提供了重写、重定向、代理等。几乎没有什么是该模块无法完成的。

