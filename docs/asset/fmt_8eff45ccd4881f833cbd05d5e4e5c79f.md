
现在你知道如何创建用户文件，是时候查看 Apache 如何使用它了。

要让 Apache 指向用户文件，使用 `AuthFile` 指令。`AuthFile` 接受文件路径作为参数。如果文件路径不是绝对的（即不以 `/` 开头），则假设路径相对于 `ServerRoot`。使用 `AuthGroupFile` 指令，你可以以相同的方式指定组文件。

接下来，使用 `AuthType` 指令设置用于该资源的身份验证类型。在这里，类型被设置为 `Basic`。

现在你需要决定该资源属于哪个域（realm）。域用于将共享相同授权用户的不同资源分组。域可以由任何内容组成。域将显示在用户浏览器的身份验证对话框中。因此，最好将域字符串设置为具有信息量的内容。域通过 `AuthName` 指令定义。

最后，什么种类型的用户被授权使用该资源。你通过以下三种使用此指令的方法：

- 如果你指定 `valid-user` 为任何选项，用户文件中的用户将被访问资源（前提是她也输入了正确的密码）。
- 你可以使用 `group` 选项指定允许访问的用户列表。
- 你可以使用 `group` 选项指定一组组。组列表和用户列表中的条目都用空格隔开。

## 文件系统身份验证与访问控制

回到你之前看到的 `server-status` 示例，与其让用户访问主机名上的 `server-status` 资源，你你可以要求用户经过身份验证后才能访问该资源。你可以在配置文件中使用以下条目来实现：

```
<Location /server-status>

  SetHandler server-status

  AuthType Basic

  AuthName "Server status"

  AuthUserFile "gnulixusers"

  Require valid-user

</Location>
```

## 关于访问控制的结语

如果你对资源同时设置了基于主机的和基于用户的访问保护，Apache 的默认行为是要求请求者同时满足这两项控制。但假设你想混合基于主机的和基于用户的保护，并在任一种方法成功时允许访问资源。你可以使用 `satisfy` 指令来实现。你可以将 `satisfy` 指令设置为 `All`（默认值）或 `Any`。当设置为 `All` 时，提供资源之前必须满足访问控制方法。如果 `satisfy` 设置为 `Any`，只要满足任何一个访问条件，就会提供资源。

这里另一个控制示例，再次使用之前的 `server-status` 示例。这次，结合访问方法，允许所有来自 `Gnuix` 域的用户访问，而域之外的用户在获得访问之前必须标识自己的身份。你可以通过以下方式实现：

```
<Location /server-status>

  SetHandler server-status

  Order deny,allow

  Deny from all

  Allow from gnulix.org

  AuthType Basic

  AuthName "Server status"

  AuthUserFile "gnulixusers"

  Require valid-user

  Satisfy Any

</Location>
```

还有更多保护 Web 服务器上内容的方法，但这里讨论的方法应该足够让你入门，并且对于大多数情况可能绰绰有余。请参阅 Apache 在线文档以获取更多关于保护网站的示例。

## Apache 模块

Apache 核心功能相对较少；Apache 通过模块获取功能。每个模块都通过添加必要的特性来解决一个定义良好的问题。通过添加或删除模块来提供 Apache 所需的功能，你可以定制 Apache 服务器以满足你的确切需求。

基础 Apache 服务器包含了近 50 个核心模块。其他开发者还提供了更多模块。Apache 模块注册表（Apache Module Registry）是 Apache 附加模块的仓库，可以在 `http://modules.apache/` 找到。模块列在 `/etc/httpd/` 下的 `modules` 目录下，但该目录是 `/usr/lib/httpd/modules` 目录的链接，模块位于那里（你的列表可能可能有不同）：

- `mod_access.so` `mod_core_meta.so` `mod_log_config.so` `mod_setenvif.so`
- `mod_actions.so` `mod_cgi.so` `mod_magic.so` `mod_spelling.so`
- `mod_alias.so` `mod_dav_fs.so` `mod_mime.so` `mod_ssl.so`
- `mod_asis.so` `mod_dav.so` `mod_negotiation.so` `mod_status.so`
- `mod_auth_anon.so` `mod_dir.so` `mod_perl.so` `mod_suex.so`
- `mod_auth_dbm.so` `mod_env.so` `mod_proxy_connect.so` `mod_unique_id.so`
- `mod_auth_digest.so` `mod_expires.so` `mod_proxy_ftp.so` `mod_userdir.so`
- `mod_auth_mysql.so` `mod_headers.so` `mod_proxy_http.so` `mod_usertrack.so`
- `mod_auth_pgsql.so` `mod_map.so` `mod_proxy.so` `mod_vhost_alias.so`
- `mod_auth.so` `mod_include.so` `mod_python.so` `mod_autoindex.so`
- `mod_info.so` `mod_rewrite.so`

每个模块都添加了可以在你的配置文件使用的新指令。正如你所猜到的，额外的命令、开关和选项远多到无法在本章中全部描述。接下来的章节简要描述了 Fedora Apache 安装中可用的这些模块子集。

### mod_access

`mod_access` 根据 IP 地址、主机名或环境变量控制对 Web 服务器上某些区域的访问。例如，你可能允许来自域内的任何人访问你 Web 的某些区域。更多信息请参阅“文件系统身份验证与访问控制”章节。

### mod_alias

`mod_alias` 处理入站 HTTP 请求的 URL，例如将客户端请求重定向到另一个 URL。它还可以将文件系统的部分映射到你的 Web 结构中。例如，

```
Alias /images/ /home/wsb/graphics/
```

对于任何以 `/images/` 开头的 URL，它将从 `/home/wsb/graphics` 目录获取内容。这是在客户端完全不知情的情况下完成的。如果你使用 `redirect`（重定向），客户端将被指示去另一个 URL 寻找请求的内容。更高级的 URL 操作可以通过 `mod_rewrite` 完成。

### mod_asis

`mod_asis` 用于在响应中详细地指定要包含的所有信息。这将完全跳过 Apache 可能会向响应中添加的任何标头。所有带有 `.asis` 扩展名的文件将直接发送给客户端而不进行任何更改。

作为一个 `mod_asis` 的简短示例，假设你已经将网站上的内容从一个位置移动到另一个位置。你必须通知访问此资源的人它已移动，并自动将他们重定向到新位置。为了提供这些信息和重定向，你可以向带有 `.asis` 扩展的文件添加以下代码：

```
Status: 301 No old stuff!

Location: http://gnulix.org/newstuff/

Content-type: text/html
```

```
<HTML>
<HEAD>
<TITLE>We moved...</TITLE>
</HEAD>
<BODY>
<P>We moved the old stuff and now you'll find it at:</P>
<A HREF="http://gnulix.org/newstuff/">New stuff!</A>
</BODY>
</HTML>
```
