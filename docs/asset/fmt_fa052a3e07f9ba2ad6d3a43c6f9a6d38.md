
![](img/cbac72550c7126a22162e94d91a0c360_428_0.png)

# 网络与互联网服务
## 第二部分
### 列表 11.2 续

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
```

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
```

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
```

```apache
<IfModule mod_mime_magic.c>
MIMEMagicFile /etc/httpd/magic
</IfModule>
```

```apache
# HostnameLookups：记录客户端的名称或仅其 IP 地址
```

# 网络与互联网服务
## 第二部分
### 列表 11.2 续

```apache
# 例如，www.apache.com (开启) 或 204.62.129.132 (关闭)。
# 默认是关闭的，因为如果人们必须有意识地开启此功能，
# 对整个网络来说会更好。开启此功能意味着
# 每个客户端请求都将导致至少向名称服务器发送
# 一次查询请求。
#
HostnameLookups Off
```

```apache
#
# ErrorLog: 错误日志文件的位置。
# 如果您没有 <VirtualHost> 容器内指定 ErrorLog 指令，
# 那么与该虚拟主机相关的错误信息将
# 记录在此处。如果您为 <VirtualHost> 容器定义了
# 错误日志文件，那么该主机的错误将记录在那里
# 而不是在此处。
#
ErrorLog /var/log/httpd.error_log
```

```apache
#
# LogLevel: 控制记录到 error_log 中的消息数量。
# 可能的值包括：debug, info, notice, warn, error, crit,
# alert, emerg。
LogLevel warn
```

```apache
#
# 下列指令定义了一些格式别名，用于配合
# CustomLog 指令（见下文）。
LogFormat "%h %l %u %t %%s %%b %%{Referer}i %%{User-Agent}i" combined
LogFormat "%h %l %u %t %%s %%b" common
LogFormat "%{Referer} -> %%u" referer
LogFormat "%{User-agent}i" agent
```
