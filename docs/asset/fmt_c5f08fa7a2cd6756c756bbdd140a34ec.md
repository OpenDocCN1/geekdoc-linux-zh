
```
AddModule mod_log_config.c
AddModule mod_log_agent.c
AddModule mod_log_referer.c
#AddModule mod_mime_magic.c
AddModule mod_mime.c
AddModule mod_negotiation.c
AddModule mod_status.c
AddModule mod_info.c
AddModule mod_include.c
AddModule mod_autoindex.c
AddModule mod_dir.c
AddModule mod_cgi.c
AddModule mod_asis.c
AddModule mod_imap.c
AddModule mod_actions.c
#AddModule mod_speling.c
AddModule mod_userdir.c
AddModule mod_alias.c
AddModule mod_rewrite.c
AddModule mod_access.c
AddModule mod_auth.c
AddModule mod_auth_anon.c
AddModule mod_auth_db.c
#AddModule mod_digest.c
#AddModule mod_proxy.c
#AddModule mod_cern_meta.c
AddModule mod_expires.c
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
AddModule mod_ssl1.c
</IfDefine>
```

# ExtendedStatus: 控制 Apache 是生成“完整”状态信息

# (`ExtendedStatus On`) 还是仅生成基本信息 (`ExtendedStatus Off`) 当调用 "server-status" 处理器时。默认值为 `Off`。

#`ExtendedStatus On`

### 第 2 部分：'Main' 服务器配置

# 本节中的指令设置了“主”服务器使用的值，

# 该服务器响应任何未被 `<VirtualHost>` 定义处理的

# 请求。这些值也为你在文件中稍后定义的

# 任何 `<VirtualHost>` 容器提供了默认值。

# 所有这些指令都可以出现在 `<VirtualHost>` 容器内部，

# 在这种情况下，这些默认设置将对正在定义的

# 虚拟主机覆盖。

# 如果你的 `ServerType` 指令（在之前的“全局环境”

# 部分中设置）被设置为 `'inetd'`，则接下来的几条指令将不会

# 产生任何影响，因为它们的设置是由 `inetd` 配置定义的。

# 跳到 `ServerAdmin` 指令。

# 配置 Apache 729

```
# Port: 独立服务器监听的端口。对于
# 小于 1023 的端口，你可能需要最初以 root 身份运行 httpd。
#
Port 80
```

```
# 如果你希望 httpd 以不同的用户或组运行，你必须
# 最初以 root 身份运行 httpd，然后它将切换。
#
# User/Group: 运行 httpd 的用户/组的名称（或数字）。
# . 在 SCO (OS 3) 上使用 'User nouser' 和 'Group nogroup'。
# . 在 httpd 上你可能无法作为 nobody 使用共享内存，
# 建议的解决方法是创建一个用户 www 并使用该用户。
# 注意，某些内核当 (无符号)Group 的值高于 60000 时
# 会拒绝设置 setgid(Group) 或 setcmtl(IPC_SET)；
# . 在这些系统上不要使用 Group nobody！
```

`User apache`

`Group apache`

```
# ServerAdmin: 你的地址，服务器出现问题时应向该地址
# 电子邮件。该地址出现在某些服务器生成的页面上，
# 以及错误文档中。
#
ServerAdmin root@localhost
```

```
# ServerName: 允许设置一个主机名，如果该主机名与客户端
# 获取的主机名不同，则发送给客户端作为你的服务器
# 使用（例如，'www' 而不是主机名）。
# 注意：你不能发明主机名并希望它们有效。
# 此处的名称必须是你的主机的有效 DNS 名称。如果
# 它没有注册 DNS 名称，请在此处输入其 IP 地址。
# 无论如何，你通过地址（例如 http://localhost/）
# 访问它，这将使重定向合理地工作。
ServerName localhost
```

```
# DocumentRoot: 你从中提供文档的目录。
# 默认情况下，所有请求都来自此目录，但可以使用
# 符号链接和别名来指向其他位置。
DocumentRoot "/var/www/html"
```

```
# Apache 能够访问的每个目录都根据允许
# 哪些和服务和功能（及其子目录）进行配置。
# 首先，我们将“默认”值配置为一组限制性的
# 权限。
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

```
# 注意，从现在起必须专门允许特定的
# 特性 - 如果某些功能无法工作，请确保你已经在下方
# 启用了它。
# 这应该更改为你设置 DocumentRoot 的任何值。
<Directory "/var/www/html">
# 也可以是 "None", "All" 或 "Indexes", "Includes",
# "FollowSymLinks", "ExecCGI", 或 "MultiViews" 的任何组合。
# 注意 "MultiViews" 必须*显式*命名 -- "Options All"
# 不会提供给它。
Options Indexes FollowSymLinks
```

## 这控制目录中的哪些 `.htaccess` 文件可以被覆盖。

# 也可以是 `'All'` 或 `'Options'`、`'FileInfo'`、

# `'AuthConfig'` 和 `'Limit'` 的组合。

`AllowOverride None`

```
# 控制谁可以从此服务器获取内容。
Order allow,deny
Allow from all
```

```
## UserDir: 当接收到 `user` 请求时，附加到用户主
# 目录后的目录名称。
UserDir public_html
```

# 控制对 `UserDir` 目录的访问。以下是一个示例，

# 该站的目录被限制为只读。

`<Directory ~public_html>`

# 这里的配置是只读的

# `Order allow,deny`

# `Allow from all`

`</Directory>`

```
# DirectoryIndex: 用于索引文件的多个文件名，
# 用空格分隔。
DirectoryIndex index.html index.shtml index.php
```

# `AccessFileName`: 用于 Apache 在每个目录中查找

# 信息的文件名。

`AccessFileName .htaccess`

```
# Files: 出于安全原因，以下行阻止
# 查看 .htaccess 文件。如果你希望 Web 客户端
# 查看这些文件，请取消这些行。
<Files ~\.ht*>
Order allow,deny
Deny from all
</Files>
```

# `CacheNegotiatedDocs`: 默认情况下，Apache 向每个根据

# 内容协商的文档发送 "Pragma: no-cache"，这要求

# 服务器不要缓存。取消以下行

# 将允许代理缓存文档。

`CacheNegotiatedDocs`

```
```

# `UseCanonicalName`: (1.3 版本新功能) 当此设置开启时，当 Apache
