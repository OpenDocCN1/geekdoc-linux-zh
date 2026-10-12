

# 列表 12.3（续）

```
AddModule mod_rewrite.c
AddModule mod_access.c
#AddModule mod_auth.c
#AddModule mod_auth_anon.c
#AddModule mod_auth_db.c
#AddModule mod_digest.c
#AddModule mod_proxy.c
#AddModule mod_cern_meta.c
#AddModule mod_expire.c
AddModule mod_headers.c
#AddModule mod_usertrack.c
#AddModule mod_example.c
#AddModule mod_unique_id.c
AddModule mod_so.c
AddModule mod_setenvif.c
#AddModule mod_bandwidth.c
#AddModule mod_put.c
<IfDefine HAVE_PERL>
AddModule mod_perl.c
</IfDefine>
<IfDefine HAVE_PHP>
AddModule mod_php.c
</IfDefine>
<IfDefine HAVE_PHP3>
AddModule mod_php3.c
</IfDefine>
<IfDefine HAVE_PHP4>
AddModule mod_php4.c
</IfDefine>
<IfDefine HAVE_DAV>
AddModule mod_dav.c
</IfDefine>
<IfDefine HAVE_ROAMING>
AddModule mod_roaming.c
</IfDefine>
<IfDefine HAVE_SSL>
AddModule mod_ssl.c
</IfDefine>
```

#
#
# ExtendedStatus：控制 Apache 在调用 'server-status' 处理程序时生成“完整”状态
# 信息（ExtendedStatus On）还是仅生成基本信息（ExtendedStatus
# Off）。默认为 Off。
#
#ExtendedStatus On

### 第 2 节：'主' 服务器配置
#
# 此部分中的指令用于设置由 '主'
# 服务器使用的值，该服务器响应那些未被
# <VirtualHost> 定义处理的任何请求。这些值也为
# 文件中后续定义的 <VirtualHost> 容器提供默认值。
#
# 所有这些指令都可以出现在 <VirtualHost> 容器中，
# 在这种情况下，将为正在定义的
# 虚拟主机覆盖这些默认设置。
#
# 如果你的 ServerType 指令（在'全局环境'
# 部分中稍早设置）设置为 "inetd"，接下来的几个指令没有任何
# 效果，因为它们的设置由 inetd 配置定义。
# 直接跳到 ServerAdmin 指令。
#
# Port：独立服务器监听的端口。对于
# 小于 1023 的端口，最初需要以 root 身份运行 httpd。
#
Port 80

# 如果你希望 httpd 以不同的用户或组运行，你必须
# 最初以 root 身份运行 httpd，然后它会进行切换。
#
# User/Group：用于以 httpd 身份运行的用户/组的名称（或#数字）。
# . 在 SCO (ODT 3) 上使用 "User nouuser" 和 "Group nogroup"。
# . 在 HP-UX 上，你可能无法使用 nobody 作为共享内存，并且
# 建议的变通方法是创建一个用户 www 并使用该用户。
# 请注意，某些内核拒绝在 (unsigned)Group 的值大于 60000 时设置 setgid(Group) 或 semctl(IPC_SET,
# 在这些系统上不要使用 Group nobody！
#
User apache
Group apache

# ServerAdmin：你的地址，服务器有问题时应
# 发送电子邮件的地方。此地址会出现在某些服务器生成的页面上，例如
# 错误文档。
#
ServerAdmin webmaster@gnulix.org

# ServerName：允许你设置一个主机名，如果它与程序获取的主机名不同（即，
# 使用 "www" 而不是主机的真实名称），服务器会将其发送回给客户端。
#

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_438_0.png)

# 注意：你不能只是凭空发明主机名并希望它们能工作。你
# 在这里定义的名称必须是你主机的有效 DNS 名称。如果你不理解
# 这一点，请咨询你的网络管理员。
# 如果你的主机没有注册的 DNS 名称，请在此处输入其 IP 地址。
# 你将不得不通过其地址访问它（例如，http://123.45.67.89/）
# 无论如何，这将使重定向以合理的方式工作。
#
#ServerName localhost


#
# DocumentRoot：你提供文档的目录。默认情况下，所有请求都取自此目录，但
# 可以使用符号链接和别名指向其他位置。
DocumentRoot "/var/www/html"

#
# Apache 可访问的每个目录，都可以根据该
# 目录（及其子目录）中允许和/或禁用的服务和功能进行配置。
#
# 首先，我们将“默认值”配置为非常严格的
# 权限集。
#
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

#
# 请注意，从这一点开始，你必须明确允许
# 启用特定功能。因此，如果某项功能未按
# 你预期的那样工作，请确保你已明确
# 在下面启用了它。
#
#
# 这应该更改为你设置 DocumentRoot 的值。
#
<Directory "/var/www/html">

#
# 这也可能是 "None"、"All" 或 "Indexes" 的任何组合，
# "Includes"、"FollowSymLinks"、"ExecCGI" 或 "MultiViews"。
#
# 请注意，"MultiViews" 必须被*明确*命名——"Options All"
# 不会给你这个选项。
#
    Options Indexes Includes FollowSymLinks
#
# 这控制目录中的 .htaccess 文件可以
# 覆盖哪些选项。也可以是 "All" 或 "Options"、"FileInfo" 的任何组合，
# "AuthConfig" 和 "Limit"
#
    AllowOverride None

#
# 控制谁可以从此服务器获取内容。
#
    Order allow,deny
    Allow from all
</Directory>

#
# UserDir：如果收到 ~user 请求，则附加到用户主目录的目录名称。
#
UserDir public_html

#
# 控制对 UserDir 目录的访问。以下是一个
# 这些目录限制为只读的网站示例。
#
#<Directory /home/*/public_html>
#    AllowOverride FileInfo AuthConfig Limit
#    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
#    <Limit GET POST OPTIONS PROPFIND>
#        Order allow,deny
#        Allow from all
#    </Limit>
#    <Limit PUT DELETE PATCH PROPPATCH MKCOL COPY MOVE LOCK UNLOCK>
#        Order deny,allow
#        Deny from all
#    </Limit>
#</Directory>

#
# DirectoryIndex：用作预编写 HTML
# 目录索引的文件或文件名称。用空格分隔多个条目。
#
DirectoryIndex index.html index.htm index.shtml index.cgi

#
# AccessFileName：要在每个目录中查找的访问控制信息文件的名称。
#
AccessFileName .htaccess

# 以下几行防止 .htaccess 文件被 Web 客户端查看。由于 .htaccess 文件通常包含授权信息，出于安全原因禁止访问。如果你希望 Web 访问者查看 .htaccess 文件的内容，请注释掉这些行。如果你更改了上面的 AccessFileName 指令，请确保在此处进行相应的更改。

# 此外，人们倾向于使用诸如 .htpasswd 之类的名称作为密码文件，因此这也将保护它们。

<Files ~ "^\\.ht>"
    Order allow,deny
    Deny from all
</Files>

# CacheNegotiatedDocs：默认情况下，Apache 在每个基于内容协商的文档上发送 "Pragma: no-cache"。这是要求代理服务器不要缓存该文档。取消注释以下行会禁用此行为，并允许代理服务器缓存文档。

#CacheNegotiatedDocs

# UseCanonicalName：（1.3 新增）当此设置开启时，每当 Apache 需要构建自引用 URL（指向响应来源服务器的 URL）时，它将使用 ServerName 和 Port 形成“规范”名称。当此设置关闭时，Apache 将尽可能使用客户端提供的主机名:端口。这也影响 CGI 脚本中的 SERVER_NAME 和 SERVER_PORT。

UseCanonicalName On

# TypesConfig 描述了 mime.types 文件（或等效文件）的位置。

TypesConfig /etc/mime.types

# DefaultType 是服务器在无法通过其他方式（例如文件名扩展名）确定文档类型时使用的默认 MIME 类型。如果你的服务器主要包含文本或 HTML 文档，"text/plain" 是一个合适的值。如果你的内容大多是二进制的，例如应用程序或图像，你可能希望使用 "application/octet-stream" 来阻止浏览器将二进制文件作为文本显示。

DefaultType text/plain

# mod_mime_magic 模块允许服务器使用文件本身内容的各种提示来确定其类型。MIMEMagicFile
# 指令告诉模块提示定义的位置。
# mod_mime_magic 不是默认服务器的一部分（你必须使用 LoadModule 添加
# [参见“全局
# 环境”部分中的 DSO 段落]，或者重新编译服务器并将 mod_mime_magic
# 作为配置的一部分包含进来），因此它被包含在 <IfModule> 容器中。
# 这意味着只有当模块是服务器的一部分时，才会处理 MIMEMagicFile 指令。
<IfModule mod_mime_magic.c>
    MIMEMagicFile share/magic
</IfModule>

# HostnameLookups：记录客户端的名称或仅记录其 IP 地址
# 例如，www.apache.org（开）或 204.62.129.132（关）。
# 默认为关，因为如果人们
# 必须有意开启此功能，这对整个网络来说会更好，因为启用它意味着
# 每个客户端请求都会导致至少一次向
# 名称服务器发出的查找请求。

HostnameLookups Off

# ErrorLog：错误日志文件的位置。
# 如果你在 <VirtualHost>
# 容器内未指定 ErrorLog 指令，与该虚拟主机相关的错误消息将
# 记录在此处。如果你*确实*为 <VirtualHost>
# 容器定义了错误日志文件，该主机的错误将记录在那里而不是这里。
ErrorLog /var/log/httpd/error_log

# LogLevel：控制记录到 error_log 的消息数量。
# 可能的值包括：debug, info, notice, warn, error, crit,
# alert, emerg。
LogLevel warn

# 以下指令为使用
# CustomLog 指令定义了一些格式昵称（见下文）。
LogFormat "%h %l %u %t "%r" "%s" %b "%{Referer}i" "%{User-Agent}i"

