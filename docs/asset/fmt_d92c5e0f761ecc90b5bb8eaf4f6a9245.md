
### mod_auth

`mod_auth`使用一种简单的身份验证方案，称为基本认证，它基于在文本文件中存储用户名和加密密码。该文件非常像 UNIX 的`/passwd`文件，使用`htpasswd`命令创建。关于此主题的更多信息请参阅本章前面的“文件系统身份验证与访问控制”章节。

### mod_auth_anon

`mod_auth_anon`提供了类似于 FTP 的匿名认证。该模块允许你定义被处理为游客的用户 ID。当此类用户尝试登录时，将提示输入电子邮件地址和密码。它可以检查密码以确保它是正确的电子邮件地址。基本上，它确保密码中有一个`@`字符和一个`.`字符。

### mod_auth_dbm

`mod_auth_dbm`使用 Berkeley DB 文件而不是文本进行用户验证。要创建用于密码文件，必须使用`hdigest`工具。它的功能与`htpasswd`工具类似。更多信息请查看`hdigest`主页。

### mod_auth_digest

`mod_auth`模块的扩展；不是以明文发送用户信息，而是通过 MD5 摘要认证过程发送。这种身份验证方案在 RFC 2617 中定义。与使用基本认证相比，这是在互联网上发送数据的更安全的方法。遗憾的是，并不是所有的浏览器都支持这种身份验证方案。

### mod_autoindex

`mod_autoindex`动态创建目录索引文件。列表将以用户的方式渲染，类似于 ftp 内置命令提供的列表。

### mod_cgi

`mod_cgi`允许在服务器上执行 CGI 程序。CGI 程序是位于`/var/*/cgi-bin`目录的可执行文件，并在请求时为远程浏览器动态生成数据（通常是 HTML）。

### mod_dir 和 mod_env

`mod_dir`用于确定用户访问目录时自动返回哪些文件。默认是`index.html`。如果你有在 Windows 系统上创建 Web 页的用户，你可能也想包含`index.htm`，如下：

```
DirectoryIndex index.html index.htm
```

`mod_env`控制环境变量如何传递给 CGI 和 SSI 脚本。

### mod_expires

`mod_expires`用于通过向 HTTP 响应添加 Expires 标头为网站上的内容添加过期日期。浏览器或缓存服务器不会缓存过期内容。

## mod_headers

`mod_headers`用于操作服务器响应的 HTTP 标头。你可以根据需要替换、添加、合并或删除标头。该模块提供了`Header`指令来实现此功能。`Header`指令的顺序非常重要。对于同一个 HTTP 标头，如果一个`set`后面跟着一个`unset`，将完全移除该`Header`指令。你可以将`Header`指令放置在配置文件的任何位置。这些指令按以下顺序进行处理：

- 核心服务器
- 虚拟主机
- `<Directory>`和`.htaccess`文件
- `<Location>`
- `<Files>`

## mod_imap

`mod_imap`模块提供服务器端处理图像映射（imagemap）文件。可点击区域定义在`.map`文件中。`.map`文件中有六个指令可用。这些指令用于描述可点击区域的布局以及它们指向的 URL。

## mod_include

`mod_include`允许在服务器上使用服务器端包含（SSI）。关于如何使用 SSL 的更多信息，请参阅章节后面的“动态内容”部分。

## mod_info and mod_log_config

`mod_info`提供有关服务器配置的全面信息。例如，它将显示所有已安装的模块，以及配置文件中使用的所有指令。

`mod_log_config`定义了日志文件的格式。关于此主题的更多信息，请参阅“日志记录”部分。

## mod_mime and mod_mime_magic

`mod_mime`模块尝试根据文件扩展名确定文件的 MIME 类型。

`mod_mime_magic`模块尝试通过检查文件内容的部分来确定文件的 MIME 类型。

## mod_negotiation

使用`mod_negotiation`模块，可以在多个文档版本中选择最适合客户端能力的一个。有多个选项可用于选择在协商过程中使用哪些标准。例如，你可以在不同的语言、图形文件格式和压缩方法之间进行选择。

## mod_proxy

`mod_proxy`为 Apache 服务器实现了代理和缓存功能。它可以代理和缓存 FTP、CONNECT、HTTP/0.9 和 HTTP/1.0 请求。对于用户量巨大且对代理和缓存要求极高的网站来说，这并不是理想的解决方案。然而，对于少数用户，它是更合适的。

## mod_rewrite

`mod_rewrite`是 URL 操作的“瑞士军刀”。它允许你使用强大的正则表达式对 URL 进行任何可以想象的修改。它提供了重写、重定向、代理等功能。使用该模块几乎没有你无法实现的事情。

> 提示
> 请查看`http://localhost/manual/misc/rewriteguide.html`获取食谱，它将为你深入解释`.mod_rewrite`模块的能力。

## mod_setenvif

`mod_setenvif`允许操作环境变量。使用正则表达式，可以有条件地更改环境变量的内容。`SetEnvIf`指令在配置文件中出现的顺序非常重要。当用于同一个环境变量时，每个`SetEnvIf`指令可能会拒绝早之前的`SetEnvIf`指令。在使用此模块的指令时，请记住这一点。

## mod_spelling

`mod_spelling`用于修正 URL 中的轻微拼写错误。如果没有文件匹配请求的 URL，该模块将构建请求目录下的文件列表，并提取与请求最匹配的文件。它只会尝试纠正一个拼写错误。

## mod_status

你可以使用`mod_status`创建一个包含大量运行 Apache 服务器信息的 Web 。该页面将包含内部状态信息以及运行 Apache 进程的统计数据。当你尝试配置服务器以获得最大性能时，这是一个极大的帮助。它也是判断 Apache 服务器出现问题的良好指标。

## mod_ssl

`mod_ssl`为 Apache 提供安全套接层（版本 2 和 3）和传输层安全（版本 1）支持。至少有 30 个处理加密和客户端验证选项的指令可以与此模块配合。

## mod_unique_id

`mod_unique_id`为每个传入请求生成唯一的请求标识符。此 ID 将放入`UNIQUE_ID`环境变量中。

## mod_userdir

`mod_userdir`模块允许每个用户主目录下的子目录映射到你的 Web 树中。该模块提供了多种实现此的方法。

## mod_usrack

`mod_usrack`为每个用户会话生成 cookie。它可以跟踪用户在 Web 树内的点击流。你必须启用自定义日志将此 cookie 记录到日志文件中。

## mod_vhost_alias

`mod_vhost_alias`支持动态配置批量虚拟主机，这对于拥有许多虚拟主机的互联网服务供应商非常有用。然而，对于普通用户，Apache 普通的虚拟主机支持已经足够了。

在 Apache 服务器上托管虚拟主机有两种方法。你可以使用一个 IP 地址对应多个 CNAME，或者使用多个 IP 地址，每个地址对应一个名称。Apache 有不同的指令集来处理这些每个选项。（在本节的下一节中学习更多关于 Apache 虚拟主机知识）。

再次，Apache 模块的可用选项和功能过多，在本章无法完全描述。你可以在 Fedora 自带的服务器在线文档或 Apache 组网站上找到关于 Apache 模块的完整信息。

## 虚拟主机

Web 服务器提供的最流行的服务之一是托管虚拟域名。虚拟域名也称为虚拟主机，如果是一台独立的机器，它是一个拥有自己名称的完整网站，但它与其他虚拟站点共同托管在同一台机器上。Apache 通过`httpd.conf`文件中的指令以简单的方式实现了这一点。

## 基于地址的虚拟主机

在你为 Linux 机器配置了多个 IP 地址后，设置 Apache 将它们作为不同的网站非常简单。你只需要为每个想要作为独立网站的地址在 conf 文件中提供一个`VirtualHost`指令：

```
<VirtualHost 212.85.67.67>
ServerName gnulix
DocumentRoot /home/virtual/gnulix/public_html
TransferLog /home/virtual/gnulix/logs/access_log
ErrorLog /home/virtual/gnulix/logs/error_log
</VirtualHost>
```
