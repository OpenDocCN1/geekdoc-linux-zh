
```
LoadModule access_module modules/mod_access.so
LoadModule auth_module modules/mod_auth.so
LoadModule anon_auth_module modules/mod_auth_anon.so
LoadModule db_auth_module modules/mod_auth_db.so
LoadModule digest_module modules/mod_digest.so
LoadModule proxy_module modules/mod_proxy.so
LoadModule cern_meta_module modules/mod_cern_meta.so
LoadModule expires_module modules/mod_expires.so
LoadModule headers_module modules/mod_headers.so
LoadModule usertrack_module modules/mod_usertrack.so
LoadModule example_module modules/mod_example.so
LoadModule unique_id_module modules/mod_unique_id.so
LoadModule setenvif_module modules/mod_setenvif.so
LoadModule bandwidth_module modules/mod_bandwidth.so
LoadModule put_module modules/mod_put.so
```

### 从可用模块（静态和共享）重构

完整列表以实现正确的模块顺序。当你更改上方模块时，也请更新此处。

```
ClearModuleList
#AddModule mmap_static.c
#AddModule host_alias.c
#AddModule env.c
#AddModule log_config.c
#AddModule agent_log.c
#AddModule referer.c
#AddModule mime_magic.c
#AddModule mime.c
#AddModule negotiation.c
#AddModule status.c
#AddModule info.c
#AddModule include.c
#AddModule autoindex.c
#AddModule dir.c
#AddModule cgi.c
#AddModule alias.c
#AddModule imap.c
#AddModule action.c
#AddModule speling.c
#AddModule userdir.c
#AddModule alias.c
#AddModule rewrite.c

#AddModule access.c
#AddModule auth.c
#AddModule auth_anon.c
#AddModule auth_db.c
#AddModule digest.c
#AddModule proxy.c
#AddModule cern_meta.c
#AddModule expires.c
#AddModule headers.c
#AddModule usertrack.c
#AddModule example.c
#AddModule unique_id.c
#AddModule setenvif.c
#AddModule bandwidth.c
#AddModule put.c

# 额外模块
#AddModule perl.c
#AddModule php.c
```

### ExtendedStatus

`ExtendedStatus`：控制当调用 `server-status` 处理器时，Apache 是提供“完整”状态信息（`ExtendedStatus On`）还是仅基本信息（`ExtendedStatus Off`）。默认为 Off。

```
ExtendedStatus On
```

## 第 2 部分：'Main' 服务器配置

此节中的指令设置了“主”服务器使用的值，该服务器响应任何未由 `<VirtualHost>` 定义处理的请求。这些值也为你稍后在文件中定义任何 `<VirtualHost>` 容器提供了默认值。

这些指令都可能出现在 `<VirtualHost>` 容器内部，在这种情况下，这些设置将由定义的虚拟主机覆盖。

如果你的 `ServerType` 指令（在 'Global' 节之前）被设置为 `inetd`，则少数指令没有任何影响，因为设置是由 `inetd` 配置定义的。请跳转到 `ServerAdmin` 指令。

### Port

`Port`：独立服务器监听的端口。对于 `<1023` 的端口，你需要初始以 `root` 身份运行 `httpd`。

```
Port 80
```

如果你更改了 Apache 监听请求的端口，你需要公该端口，以便人们知道你的 Web 页面在哪里。浏览器默认向 80 端口发送请求。但是，如果你想在发布站点之前测试它，请将其设置为较大的端口，如 8080；只需完成后改回来。

如果你使用 `httpd` 以不同的用户或组运行，你必须初始以 `root` 身份运行 `httpd`，它会进行切换。

### User/Group

`User/Group`：运行 `httpd` 的用户/组的名称（或数字）。在 SCO (DOT 3) 上，使用 `User nouser` 和 `Group nogroup`。在 HPUX 上，你可能无法以 `nobody` 身份使用共享内存，建议的变通方法是创建一个用户 `www` 并使用该用户。请注意，当（无符号）`Group` 的值值大于 60000 时，某些内核会拒绝设置 `sgid(Group)` 或 `semctl(IPC_SET)`；在这些系统上不要使用 `Group nobody`！

```
User nobody
Group nobody
```

### ServerAdmin

`ServerAdmin`：你的地址，服务器出现问题时应通过电子邮件发送到该地址。该地址出现在某些服务器生成的页面上，例如错误文档。

```
ServerAdmin root@localhost
```

更改此条目以反映你希望服务器发送重要管理消息的地址。许多管理员喜欢在 `root@yourmachine.name` 接收此类邮件，但你可能想发送到特定的地址。

### ServerName

`ServerName`：允许你设置一个返回给客户端的主名，如果它与程序获取的机名不同（例如，使用 "www" 而不是主机的真实名称）。

注意：你不能注入主机名并寄希望它们有效。你在此定义的名称必须是主机的有效 DNS 名称。如果你不理解，请咨询你的网络管理员。如果你的主机没有注册 DNS 名称，请在此处输入其 IP 地址。无论如何你通过地址（例如 `http://123.45.67.89/`）访问它，这有助于重定向正常工作。

```
# ServerName localhost
```

如果你不对文件进行任何其他更改，必须将 `localhost` 替换为你的服务器名称。否则，Apache 将无法工作。

### DocumentRoot

`DocumentRoot`：你提供文档的目录。默认情况下，所有请求都从该目录获取，但可以使用符号链接和别名指向其他位置。

```
DocumentRoot '/home/httpd/html/'
```

存在。这是一种安全技术，旨在保护你的系统文件免受任何试图通过 Apache 侵入你网络的攻击。

Apache 可访问的每个目录都可以根据在该目录（及其子目录）中允许和/或禁用的哪些和服务和功能进行配置。

首先，我们将“默认”配置为一组非常严格的权限集。

```
<Directory>
  Options FollowSymLinks
  AllowOverride None
</Directory>
```

注意，从现在开始，你必须特别地允许启用特定的功能，如果某些功能没有按照你预期的那样工作，请确保你已经在下方特意启用了它们。

这应该被更改为你设置的 `DocumentRoot` 所在的路径。

```
<Directory> "/home/http/html">
```

这也可以是 `None`、`All` 或 `Indexes`、`Includes`、`FollowSymLinks`、`ExecCGI` 或 `MultiViews` 的组合。注意 `MultiViews` 必须显式命名——`Options All` 并不会提供它。

```
  Options Indexes Includes FollowSymLinks
```

这控制目录中的 `.htaccess` 文件可以覆盖哪些选项。也可以是 `All` 或 `Options`、`FileInfo`、`AuthConfig` 和 `Limit` 的组合。

```
AllowOverride None
```

控制谁可以从此服务器获取内容。

```
Order allow,deny
```
