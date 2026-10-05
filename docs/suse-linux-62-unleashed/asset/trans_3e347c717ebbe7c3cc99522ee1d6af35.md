

# 列表 11.2 续

```c
AddModule mod_include.c
AddModule mod_autoindex.c
AddModule mod_dir.c
AddModule mod_cgi.c
AddModule mod_asis.c
AddModule mod_imap.c
AddModule mod_actions.c
AddModule mod_spelling.c
AddModule mod_userdir.c
AddModule mod_proxy.c
AddModule mod_alias.c
AddModule mod_rewrite.c
AddModule mod_access.c
AddModule mod_auth.c
AddModule mod_auth_anon.c
AddModule mod_auth_dbm.c
AddModule mod_auth_db.c
AddModule mod_digest.c
AddModule mod_cern_meta.c
AddModule mod_expires.c
AddModule mod_headers.c
AddModule mod_usrack.c
AddModule mod_example.c
AddModule mod_unique_id.c
AddModule mod_so.c
AddModule mod_setenvif.c
AddModule mod_perl.c
AddModule mod_php3.c
```

```apache
#
# ExtendedStatus 控制 Apache 是生成“完整”的状态
# 信息 (ExtendedStatus On) 还是仅生成基本信息 (ExtendedStatus
# Off)，当 "server-status" 处理器被调用时。默认值为 Off。

#ExtendedStatus On

### 第 2 节：'主'服务器配置
#
# 此节中的指令设置了“主”服务器使用的值，
# 该服务器响应任何未由 <VirtualHost> 定义处理的
# 请求。这些值为您稍后在文件中定义的任何
# <VirtualHost> 容器提供了默认值。
```

# Apache 服务器器
第 11 章

# 列表 11.2 续

# 11

```apache
#
# 所有这些指令都可能出现在 <VirtualHost> 容器内部，
# 在这种情况下，这些默认设置将为正在定义的
# 虚拟主机被重写。

#
# 如果 Server 指令（在早之前的“全局环境”部分
# 中设置）被设置为 'inetd'，接下来的几条指令将不起
# 作用，因为它们的设置是由 inetd 配置定义的。
# 跳到 ServerAdmin 指令。

#
# Port: 独立服务器监听的端口。对于
# < 1023 的端口，您将需要最初以 root 身份运行 httpd。

Port 80

# 如果您希望 httpd 以不同的用户或组运行，您必须
#最初以 root 身份运行 httpd，然后会自动切换。

# User/Group: 运行 httpd 的用户/组名称（或数字）。
# 在 SCO (DOT 3) 上使用 "User Peter" 和 "group nogroup"。
# 在 HPUX 上，您可能无法使用 nobody 的共享内存，
# 建议的解决办法是创建一个用户 www 并使用该用户。
# 注意，某些内核在 (无符号)Group 值大于 60000 时
# 会拒绝 setgid(Group) 或 semctl(IPC_SET)；
# 在这些系统上不要使用 Group nogroup！

User wwwrun
Group nogroup

# ServerAdmin: 您的地址，服务器出现问题时应邮件至此。
# 此地址出现在某些服务器生成的页面上，例如
# 错误文档。

ServerAdmin root@localhost
```

![](img/cbac72550c7126a22162e94d91a0c360_428_0.png)

# 网络与互联网服务
第二部分

# 列表 11.2 续

```apache
# ServerName 允许您设置一个主机名，如果该名称与程序
# 获取的名称不同，则将其返回给客户端（例如，
# 使用 "www" 而不是主机的真实名称）。

# 注意：您不能随意发明主机名并希望它们有效。
# 您在此处定义的名称必须是您主机的有效 DNS 名称。
# 如果您不懂这一点，请咨询您的网络管理员。
# 如果您的主机没有注册的 DNS 名称，请在此处输入其 IP 地址。
# 无论如何您都必须通过地址访问它（例如 http://123.45.67.89/），
# 这将使重定向以合理的方式工作。

# ServerName allen.suse.de

# DocumentRoot：您从中提供文档的目录。
# 默认情况下，所有请求都从此目录获取，但
# 可以使用符号链接和别名指向其他位置。

DocumentRoot "/usr/local/httpd/htdocs"

# Apache 拥有访问权的每个目录都可以配置
# 在该目录（及其子目录）中允许和/或禁用
# 哪些服务和功能。

# 首先，我们将“默认”值配置为一组非常严格的
# 权限。

<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>

# 注意，从现在开始，您必须特地允许
# 启用特定的功能——这意味着如果某些功能没有按照您
# 预期的那样工作，请确保您已在下方特地启用了它。

# 这应该更改为您设置 DocumentRoot 的任何值。
```

```apache
#<Directory "/usr/local/httpd/htdocs">

# 这也可以是 "None"、"All" 或 Indexes,"Includes",
# "FollowSymLinks","ExecCGI" 或 "MultiViews" 的任何组合
#
# 注意 "MultiViews" 必须是“显式”命名的——"Options All"
# 不会提供给它。

Options Indexes FollowSymLinks

# 这控制了目录中的 .htaccess 文件可以
# 覆盖哪些选项。也可以是 "All"，或 "Options","FileInfo",
# "AuthConfig" 和 "Limit" 的任何组合。

AllowOverride None

# 控制谁可以从此服务器获取内容。

Order allow,deny
Allow from all
</Directory>

# UserDir：当接收到 -user 请求时，附加到用户主
# 目录的名称。
UserDir public_html

# 控制对 UserDir 目录的访问。以下是一个网站
# 示例，其中这些目录被限制为只读。

#<Directory /*/public_html>
# AllowOverride FileInfo AuthConfig Limit
# Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
# <Limit GET POST OPTIONS PROIND>
# Order allow,deny
# Allow from all
```

```apache
# </Limit>
# <Limit> PUT DELETE PATCH PROPPAC MKCOL MOVE LOCK
# Order deny,allow
# Deny from all
# </Limit>
#</Directory>

# DirectoryIndex：作为索引使用的文件或文件。
# 用空格分隔多个项。
# DirectoryIndex index.html

# AccessFileName：在每个目录中查找访问控制
# 信息的文件。
AccessFileName .htaccess

# 以下几行阻止 Web 访问 .htaccess 文件。
# 由于 .htaccess 通常包含授权信息，因此禁止访问。
# 如果您希望 Web 访问可以看到 .htaccess 的内容，请注释
# 这些行。

<Files .htaccess>
Order allow,deny
Deny from all
</Files>

# CacheNegotiatedDocs：默认情况下，Apache 对根据
# 内容协商的文档发送 "Pragma: no-cache"，要求
# 代理服务器不要缓存。取消此注释将
# 允许缓存文档。
#
CacheNegotiatedDocs

# UseCanonicalName：（1.3 新功能）当此设置开启时，Apache
# 需要构造引用 URL（指向响应服务器的 URL）时，将
# 使用 ServerName 和 端口形成“规范”名称。如果关闭
# 设置，Apache 将尽可能使用客户端提供的主机:端口。
# 这影响 CGI 脚本中的 SERVER_NAME 和 SERVER_PORT。

```apache
UseCanonicalName On
```

```apache
# TypesConfig 描述 mime.types 文件（或等效文件）
# 所在。
```

```apache
TypesConfig /etc/httpd/mime.types
```

```apache
# DefaultType 是服务器无法通过扩展或其他方式
# 确定类型时使用的默认 MIME 类型。
# 如果您的服务器主要是文本或 HTML 文档，'text/plain'
# 是一个很好的值。如果大部分内容是二进制文件，如
 应用程序或图像，您可能希望使用 "application/octet-stream"
# 以防止浏览器将二进制文件显示为文本。

```apache
DefaultType text/plain
```

```apache
# mod_mime_magic 模块允许服务器使用 mime 文件
# 内容中的各种提示来确定其类型。MIMEMagicFile
# 指令告诉模块定义所在的位置。
# mod_mime_magic 不是默认的一部分（如果您必须通过
# LoadModule 手动添加它[参见“全局环境”部分的 DSO
# 段落]，或者重新编译服务器并将 mod_mime_magic
# Include），因此被封装在 <IfModule> 容器中。
# 这意味着只有当模块是服务器的一部分时，MIMEMagicFile
# 指令才会被处理。

```apache
<IfModule mod_mime_magic.c>
MIMEMagicFile /etc/httpd/magic
</IfModule>
```

```apache
# HostnameLookups：记录客户端的名称或仅其 IP 地址
```

