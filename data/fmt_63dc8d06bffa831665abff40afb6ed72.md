
```
matthew@semour:-$ sudo a2mod module_name
```

要禁用模块，请使用此命令：

```
matthew@semour:-$ sudo a2dismod module_name
```

注意，这两个命令都需要使用模块的实际名称而不是文件名；例如，`mod_version.so` 是文件名，而 `version` 是模块名称。你必须知道模块名称才能使用这两个命令，但在大多数情况下，它就像这个例子中一样简单。此外，在运行任一命令后，你需要重启 `apache2` 以激活新配置。

## mod_access

`mod_access` 根据 IP 地址、主机名或环境变量控制对服务器上区域的访问。

## mod_alias

`mod_alias` 将网站的部分映射到文件系统。例如，你可能将 `/images/` 映射到 `/home/wsb/graphics/`。

## mod_asis

`mod_asis` 用于详细指定响应中包含的所有信息。所有 `.asis` 扩展的文件直接发送给客户端，而不进行任何更改。

作为 `mod_asis` 使用的一个简短示例，假设你将内容从一个位置移动到了另一个位置。现在你必须告知尝试访问此资源的人已移动，并且将他们自动重定向到新位置。为了提供这些信息并重定向，你可以在 `.asis` 文件中添加以下代码：

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
<A HREF="http://gnulix.org/newstuff/">New stuff</A>
</BODY>
</HTML>
```

## mod_auth

`mod_auth` 使用一种简单的身份认证方案，基于在文本文件中存储用户名和加密密码。该文件非常类似于 UNIX 的 `/passwd` 文件，并通过 `htpasswd` 命令创建。关于此主题的更多信息，请参考本章前面的“文件系统身份验证与访问控制”。

## mod_auth_anon

`mod_auth_anon` 模块提供了类似于匿名 FTP 的匿名认证。该模块允许你定义被处理为访客的用户 ID。当此类用户尝试登录时，会提示他输入电子邮件地址作为密码。你可以让 Apache 检查密码以确保它是一个（大致的）正确的电子邮件地址。基本上，Apache 会确保密码包含一个 @ 字符和至少一个字符。

## mod_auth_dbm

`mod_auth_dbm` 使用 Berkeley DB 文件作为用户验证文件的文本。

## mod_auth_digest

`mod_auth_digest` 是基础 `mod_auth` 模块的扩展。它不是以明文形式发送用户信息，而是通过消息摘要 5 `MD5` 身份验证过程发送。这种身份验证方案定义在 RFC 2617《HTTP Authentication: Basic and Digest Access Authentication》中。

要为 `mod_auth_dbm` 创建密码文件，你必须使用 `htdigestest` 工具。它的功能与 `htpasswd` 工具大同小异。更多信息请参阅 `htdigestest` 的手册页。

## mod_autoindex

`mod_autoindex` 模块为目录索引动态创建文件列表。该列表以一种易于用户的方式进行渲染，类似于 FTP 内置 `ls` 命令所提供的列表。

## mod_cgi

`mod_cgi` 允许在你的服务器上执行 CGI 程序。CGI 程序是位于 `/var/www/cgi-bin` 目录下的可执行文件，用于在收到请求时为远程浏览器动态生成数据（通常是 HTML）。

## mod_dir and mod_env

`mod_dir` 模块用于确定当用户尝试访问目录时自动返回哪些文件。默认值是 `index.html`。如果你有在 Windows 系统上创建网页面的用户，你还应该包含 `index.htm`，如下所示：

```
DirectoryIndex index.html index.htm
```

`mod_env` 控制环境变量如何传递给 CGI 和 SSI 脚本。

## mod_expires

`mod_expires` 用于通过向 HTTP 响应添加 `Expires` 头部，为你网站上的内容添加过期日期。网络浏览器和缓存服务器不会缓存降低顺序。

## mod_headers

`mod_headers` 用于处理服务器响应的 HTTP 头部。你可以根据需要替换、添加或删除头部。该模块提供了一个 `Header` 指令来实现此功能。`Header` 指令的顺序非常重要。对于同一个 HTTP 头部，`set` 后接 `unset` 将完全删除该头部。你可以将 `Header` 指令放置在配置文件的任何位置。这些指令按以下顺序进行处理：

1. 核心服务器
2. 虚拟主机
3. `<Directory>` 和 `.htaccess` 文件
4. `<Location>`
5. `<Files>`

## mod_include

`mod_include` 允许在你的服务器上使用服务器包含 `SSI`，这在 PHP 接管该市场之前非常流行。

## mod_info and mod_log_config

`mod_info` 提供有关服务器配置的全面信息。例如，它会显示所有已安装的模块以及配置文件中使用的指令。

`mod_log_config` 定义了日志文件的格式。关于此主题的更多信息，请参阅本章后文“日志”部分。

## mod_mime and mod_mime_magic

`mod_mime` 模块尝试通过检查扩展名来确定文件的 MIME 类型。

`mod_mime_magic` 模块尝试通过检查文件内容部分来确定文件的 MIME 类型。

## mod_negotiation

使用 `mod_negotiation` 模块，你可以从多个文档版本中选择最适合你客户端能力的版本。有多个选项可以选择在协商过程中使用哪些标准。例如，你可以在不同的语言、图形文件格式和压缩方法之间进行选择。

## mod_proxy

`mod_proxy` 为 Apache 服务器实现了代理和缓存功能。它可以代理和缓存 FTP、CONNECT、HTTP/0.9 和 HTTP/1.0 请求。对于拥有大量用户并因此有高代理和缓存要求的站点来说，这并不是理想的。然而，对于用户较少的站点，它更为合适。

## mod_rewrite

`mod_rewrite` 是 URL 操作的“瑞士军刀”。它允许你使用强大的正则表达式对 URL 进行任何可以想象的操控。它提供了重写、重定向、代理等功能。使用此模块，几乎没有什么是你无法完成的了。

> 提示：如果你安装并运行了 Apache，请访问 https://localhost/manual/misc/rewrite-guide.html 查看教程，该教程将为你深入解释 `mod_rewrite` 模块的功能。

## mod_setenvif

`mod_setenvif` 允许操作环境变量。通过使用被称为正则表达式的短文本匹配代码段，你可以条件地更改环境变量的内容。`SetEnvif` 指令在配置文件中出现的顺序很重要。在使用此模块时，每个 `SetEnvif` 指令可以重置环境变量。

## mod_speling

`mod_speling` 用于修正 URL 中的细微拼写错误。如果没有文件匹配请求，该模块将构建请求文件的列表。它尝试纠正拼写错误。

## mod_status

你可以使用 `mod_status` 创建一个包含运行中服务器信息的网页。该页面包含关于 Apache 进程的统计信息。当你尝试配置服务器以获得最大性能时，这非常有帮助。它提供了服务器问题的良好指示。

## mod_ssl

`mod_ssl` 为 Apache 提供了安全套字层（版本 2 和 3）和传输层安全（版本 1）支持。你可以配合此模块进行加密和客户端认证。此模块要求你安装 OpenSSL 并生成证书。（这将在本章后文的“HTTPS”部分介绍。）

## mod_unique_id

`mod_unique_id` 为每个传入请求生成一个唯一标识。该 ID 被放入 `UNIQUE_ID` 环境变量。

## mod_userdir

`userdir` 模块允许将用户 `/home` 目录下的子目录映射到你的 树中。该模块提供了实现此目标的方法。

## mod_usertrack

`mod_usertrack` 用于为每个会话生成 cookie，例如跟踪用户流。你可以将自定义日志写入文件。

## mod_vhost_alias

`mod_vhost_alias` 支持动态映射，这对于拥有许多主机的服务提供商（ISP）非常有用。然而，对于普通用户，普通的托管支持就足够。

## 虚拟主机
