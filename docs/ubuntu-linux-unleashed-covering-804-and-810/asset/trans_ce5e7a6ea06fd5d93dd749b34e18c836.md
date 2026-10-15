

mod_auth.so        mod_include.so        mod_python.so        mod_autoindex.so
mod_info.so        mod_rewrite.so

每个模块都会在你的配置文件中添加新的指令。正如你可能猜到的，本章中描述所有额外的命令、开关和选项实在太多了。以下各节简要描述了 Ubuntu 的 Apache 安装中可用的部分模块。

## mod_access

mod_access 根据 IP 地址、主机名或环境变量控制对 Web 服务器区域的访问。例如，你可能希望允许来自自己域内的人员访问 Web 服务器的某些区域。有关更多信息，请参阅“文件系统身份验证和访问控制”部分。

## mod_alias

mod_alias 操作传入 HTTP 请求的 URL，例如将客户端请求重定向到另一个 URL。它还可以将文件系统的一部分映射到你的 Web 层次结构中。例如。

```
Alias /images/ /home/wsb/graphics/
```

为任何以 /images/ 开头的 URL 从 /home/wsb/graphics 目录获取内容。这是在客户端一无所知的情况下完成的。如果你使用重定向，客户端会被指示前往另一个 URL 以找到请求的内容。更高级的 URL 操作可以使用 mod_rewrite 实现。

## mod_asis

mod_asis 用于详细指定响应中包含的所有信息。这完全绕过了 Apache 否则可能会添加到响应中的任何头部。所有 .asis 扩展名的文件都会原封不动地直接发送给客户端。

作为 mod_asis 用法的简短示例，假设你已将站点上的内容从一个位置移动到另一个位置。现在你必须通知尝试访问此资源的人它已移动，并自动将他们重定向到新位置。为了提供此信息和重定向，你可以在 .asis 扩展名的文件中添加以下代码：

```
Status: 301 No more old stuff!
Location: http://gnulix.org/newstuff/
```

```
Content-type: text/html

<HTML>
<HEAD>
<TITLE>We've moved...</TITLE>
</HEAD>
<BODY>
<P>We've moved the old stuff and now you'll find it at:<P>
<A HREF="http://gnulix.org/newstuff/">New stuff</A>.
</BODY>
</HTML>
```

## mod_auth

mod_auth 使用一种简单的用户身份验证方案，称为基本身份验证，它基于将用户名和加密密码存储在文本文件中。该文件看起来非常像 UNIX 的 /etc/passwd 文件，并使用 htpasswd 命令创建。有关此主题的更多信息，请参阅本章前面的“文件系统身份验证和访问控制”部分。

## mod_auth_anon

mod_auth_anon 模块提供与匿名 FTP 类似的匿名身份验证。该模块使你能够定义作为访客用户处理的那些用户 ID。当此类用户尝试登录时，他会被提示输入其电子邮件地址作为密码。你可以让 Apache 检查密码以确保它是一个或多或少正确的电子邮件地址。基本上，它确保密码包含 @ 字符和至少一个 . 字符。

## mod_auth_dbm

mod_auth_dbm 使用 Berkeley DB 文件而不是文本作为用户身份验证文件。

## mod_auth_digest

作为基本 mod_auth 模块的扩展，mod_auth_digest 不是以明文发送用户信息，而是通过 MD5 摘要身份验证过程发送。该身份验证方案定义在 RFC 2617 中。与使用基本身份验证相比，这是通过 Internet 发送用户数据的一种更安全的方式。不幸的是，并非所有 Web 浏览器都支持此身份验证方案。

要为 mod_auth_dbm 创建密码文件，你必须使用 htdigest 实用程序。它的功能或多或少与 htpasswd 实用程序相同。有关更多信息，请参阅 htdigest 的手册页。

## mod_autoindex

mod_autoindex 模块动态创建目录索引的文件列表。该列表以用户友好的方式呈现，类似于 FTP 内置 ls 命令提供的列表。

## mod_cgi

mod_cgi 允许在你的服务器上执行 CGI 程序。CGI 程序是驻留在 `/var/www/cgi-bin` 目录中的可执行文件，用于在请求时为远程浏览器动态生成数据（通常是 HTML）。

## mod_dir and mod_env

mod_dir 模块用于确定当用户尝试访问目录时自动返回哪些文件。默认是 index.html。如果你有在 Windows 系统上创建网页的用户，你还应包含 index.htm，如下所示：

```
DirectoryIndex index.html index.htm
```

mod_env 控制环境变量如何传递给 CGI 和 SSI 脚本。

## mod_expires

mod_expires 用于通过在 HTTP 响应中添加 Expires 头来为站点上的内容添加过期日期。Web 浏览器或缓存服务器不会缓存已过期的内容。

## mod_headers

mod_headers 用于操作服务器响应的 HTTP 头部。你可以根据需要替换、添加、合并或删除头部。该模块为此提供了一个 Header 指令。Header 指令的顺序很重要。先设置后取消设置同一个 HTTP 头部将完全删除该头部。你可以在配置文件中的几乎任何位置放置 Header 指令。这些指令按以下顺序处理：

- 1. 核心服务器
- 2. 虚拟主机
- 3. `<Directory>` 和 `.htaccess` 文件
  `<Location>`
  `<Files>`

## mod_include

mod_include 使你的服务器能够使用服务器端包含，在 PHP 占据这一市场部分之前，它非常流行。

