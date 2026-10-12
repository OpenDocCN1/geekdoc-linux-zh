

- mod_access.so
- mod_actions.so
- mod_alias.so
- mod_asis.so
- mod_auth_anon.so
- mod_auth_dbm.so
- mod_auth_digest.so
- mod_auth_mysql.so
- mod_auth_pgsql.so
- mod_auth.so
- mod_info.so
- mod_cern_meta.so
- mod_cgi.so
- mod_dav_fs.so
- mod_dav.so
- mod_dir.so
- mod_expires.so
- mod_env.so
- mod_headers.so
- mod_imap.so
- mod_include.so
- mod_rewrite.so
- mod_log_config.so
- mod_mime_magic.so
- mod_mime.so
- mod_negotiation.so
- mod_perl.so
- mod_proxy_connect.so
- mod_proxy_ftp.so
- mod_proxy_http.so
- mod_proxy.so
- mod_python.so
- mod_setenvif.so
- mod_speling.so
- mod_ssl.so
- mod_status.so
- mod_suexec.so
- mod_unique_id.so
- mod_userdir.so
- mod_usertrack.so
- mod_vhost_alias.so
- mod_autoindex.so

每个模块都会添加新的指令，这些指令可在您的配置文件中使用。正如您可能猜测的那样，额外的命令、开关和选项太多，本章无法一一描述。接下来的章节简要描述了 Fedora 的 Apache 安装中可用的模块子集。

## mod_access

mod_access 根据 IP 地址、主机名或环境变量控制对您 Web 服务器区域访问权限。例如，您可能希望允许来自您自身域名内的任何人访问您 Web 的特定区域。有关更多信息，请参阅本章前面的“文件系统认证和访问控制”章节。

## mod_alias

mod_alias 操纵传入的 HTTP 请求的 URL，例如将客户端请求重定向到另一个 URL。它还可以将文件系统的一部分映射到您的 Web 层级中。例如，

*Alias /images/ /home/wsb/graphics/*

会为任何以 */images* 开头的 URL 获取 */home/wsb/graphics* 目录中的内容。这是在客户端不知情的情况下完成的。如果使用重定向，客户端会被告知去另一个 URL 查找请求的内容。可以使用 mod_rewrite 实现更高级的 URL 操作。

## mod_asis

mod_asis 用于以详细的方式指定响应中包含的所有信息。这会完全绕过 Apache 可能添加到响应中的任何标头。所有扩展名为 *.asis* 的文件都会未经任何更改直接发送到客户端。

作为使用 mod_asis 的一个简短示例，假设您已将内容从一个位置移动到网站上的另一个位置。现在，您必须通知尝试访问此资源的人该内容已移动，并自动将其重定向到新位置。为了提供这些信息并重定向，您可以将以下代码添加到具有 .asis 扩展名的文件中：

```
Status: 301 No more old stuff!
Location: http://gnu1ix.org/newstuff/
Content-type: text/html

<HTML>
  <HEAD>
    <TITLE>We've moved... </TITLE>
  </HEAD>
  <BODY>
    <P>We've moved the old stuff and now you'll find it at:</P>
    <A HREF="http://gnu1ix.org/newstuff/">New stuff</A>.
  </BODY>
</HTML>
```

## mod_auth

mod_auth 使用一种简单的用户身份验证方案，称为基本身份验证（Basic Authentication），该方案基于在文本文件中存储用户名和加密的密码。这个文件看起来非常像 UNIX 的 /etc/passwd 文件，并使用 htpasswd 命令创建。有关此主题的更多信息，请参阅本章前面的“文件系统认证和访问控制”章节。

## mod_auth_anon

mod_auth_anon 模块提供类似于匿名 FTP 的匿名身份验证。该模块允许您定义应作为来宾用户处理的用户的用户 ID。当此类用户尝试登录时，系统会提示其输入电子邮件地址作为密码。您可以让 Apache 检查密码，以确保它是（或多或少）正确的电子邮件地址。基本上，它确保密码包含一个 @ 字符和至少一个 . 字符。

## mod_auth_dbm

mod_auth_dbm 使用 Berkeley DB 文件而不是文本文件作为用户身份验证文件。

## mod_auth_digest

基本 mod_auth 模块的扩展，mod_auth_digest 通过 MD5 摘要身份验证过程发送用户信息，而不是以纯文本形式发送。此身份验证方案在 RFC 2617 中定义。与使用基本身份验证相比，这是通过互联网发送用户数据的一种更安全的方式。不幸的是，并非所有 Web 浏览器都支持此身份验证方案。

要为 `mod_auth_dbm` 创建密码文件，您必须使用 `htdigest` 实用工具。它或多或少具有与 `htpasswd` 实用工具相同的功能。有关更多信息，请参阅 `htdigest` 的手册页。

## mod_autoindex

`mod_autoindex` 模块动态创建文件列表用于目录索引。该列表以用户友好的方式渲染，类似于 FTP 内置 `ls` 命令提供的列表。

## mod_cgi

`mod_cgi` 允许在您的服务器上执行 CGI 程序。CGI 程序是驻留在 `/var/www/cgi-bin` 目录中的可执行文件，用于在请求时动态生成数据（通常是 HTML）供远程浏览器使用。

## mod_dir 和 mod_env

`mod_dir` 模块用于确定当用户尝试访问目录时自动返回哪些文件。默认值是 `index.html`。如果您有在 Windows 系统上创建 Web 页面的用户，您还应该包括 `index.htm`，如下所示：

```
DirectoryIndex index.html index.htm
```

`mod_env` 控制环境变量如何传递给 CGI 和 SSI 脚本。

## mod_expires

`mod_expires` 用于通过向 HTTP 响应添加 `Expires` 标头来为网站内容添加过期日期。Web 浏览器或缓存服务器不会缓存过期的内容。

## mod_headers

`mod_headers` 用于操纵服务器响应的 HTTP 标头。您可以随心所欲地替换、添加、合并或删除标头。该模块为此提供了一个 `Header` 指令。`Header` 指令的顺序很重要。对同一 HTTP 标头的 `set` 后跟 `unset` 将完全移除该标头。您可以在配置文件中几乎任何地方放置 `Header` 指令。这些指令按以下顺序处理：

1. 核心服务器
2. 虚拟主机
3. `<Directory>` 和 `.htaccess` 文件
4. `<Location>`
5. `<Files>`

## mod_include

mod_include 启用在您服务器上使用服务器端包含。有关如何使用 SSI 的更多信息，请参阅本章后面关于“动态内容”的章节。

## mod_info 和 mod_log_config

mod_info 提供有关您服务器配置的综合信息。例如，它显示所有已安装的模块，以及配置文件中使用的所指令。

mod_log_config 定义您的日志文件应如何呈现。有关此主题的更多信息，请参阅“日志记录”章节。

## mod_mime 和 mod_mime_magic

mod_mime 模块试图根据文件扩展名确定文件的 MIME 类型。

mod_mime_magic 模块试图通过检查文件内容的部分来确定文件的 MIME 类型。

## mod_negotiation

使用 mod_negotiation 模块，您可以选择最适合客户端功能的多个文档版本之一。有几个选项可选择在协商过程中使用哪些标准。例如，您可以选择不同的语言、图形文件格式和压缩方法。

## mod_proxy

mod_proxy 为 Apache 服务器实现代理和缓存功能。它可以代理和缓存 FTP、CONNECT、HTTP/0.9 和 HTTP/1.0 请求。对于拥有大量用户因而对代理和缓存有高要求的网站来说，这并不是理想的解决方案。然而，对于少量用户来说，它是绰绰有余的。

## mod_rewrite

mod_rewrite 是 URL 操作的“瑞士军刀”。它使您能够使用强大的正则表达式对 URL 进行任何可想象的操作。它提供重写、重定向、代理等功能。使用此模块，几乎没有您无法完成的事情。

> 参见 http://localhost/manual/misc/rewritetutorial.html，该指南详细说明了 mod_rewrite 模块的功能。

