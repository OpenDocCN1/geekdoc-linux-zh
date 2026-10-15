
要为 Apache 创建用户文件，请使用 `htpasswd` 命令。它包含在 Apache 包中。如果你是通过包安装的，它在 `/usr/bin`。运行不带任何选项的 `htpasswd` 会产生如下：

用法：

```
htpasswd [-cmds] passwordfile username
htpasswd -b[cmds] passwordfile username

htpasswd -n[mdps] username
htpasswd -nb[mdps] password
```
`-c` 创建新文件。
`-n` 不更新文件；将结果显示在标准输出上。
`-m` 强制对密码进行 MD5 加密。
`-d` 强制对密码进行 CRYPT 加密（默认）。
`-p` 不对密码加密（明文）。
`-s` 强制对密码进行 SHA加密。
`-b` 使用命令行中的密码而不是提示输入。
`-D` 删除指定的用户。

在 Windows 上，TPF 和 NetWare 系统默认使用 `'-m'` 标记。

在其他系统上，`'-p'` 标记可能不起作用。

如你所见，这并不是一个很难使用的命令。要创建一个名为 `gniluxers`、用户名为 `wsb` 的用户文件，你需要执行类似的操作：

`sudo htpasswd -c gniluxers wsb`

然后你会被提示为用户输入密码。要添加更多用户，你需要重复相同的步骤，只需省略 `-c` 标记。

你还可以创建用户组。这些格式与 `/etc/groups` 类似。在每行中，输入组名，后跟冒号，然后列出用户。例如，一个用户组项可能如下：`gniluxers: wsb`

## 身份验证与访问控制

现在你已经知道如何创建用户文件，现在该查看 Apache 如何使用它来保护资源。要让 Apache 指向用户文件，使用 `AuthUserFile` 指令。`AuthUserFile` 接受路径作为参数。如果路径不是绝对路径（即不以 `/` 开头），假设假设路径相对于 `ServerRoot`。使用 `AuthGroup` 指令相同的方式指定组。

接下来，使用 `AuthType` 指令设置用于此资源的身份验证类型。在这里，类型被设置为 `Basic`。

现在你需要决定资源属于哪个领域（realm）。领域用于对资源分组，由任何字符串组成。领域显示在用户的浏览器对话框中。因此，你应该将领域字符串设置为具有描述性的内容。领域由 `AuthName` 指令定义。

最后，说明什么类型的用户授权使用资源。你可以通过 `require` 指令来实现。该指令的三种用法如下：

- 如果指定 `user-id` 为选项，用户文件中的任何用户都被允许访问资源（前提是输入了正确的密码）。
- 你可以使用 `users` 选项指定允许访问的用户列表。
- 你可以使用 `group` 选项指定组。组列表和用户列表之间用空格分隔。

回到你之前看到的 `server-status` 示例，与其根据主机名允许用户访问 `server-status` 资源，不如要求用户经过身份验证后访问该资源。你可以通过配置文件中的以下项来实现：

```
<Location /server-status>
SetHandler server-status
AuthType Basic
AuthName "Server status"
AuthUserFile "gnuluxers"
Require valid-user
</Location>
```

### 访问控制的总结

如果你对资源同时设置了基于主机和基于用户的访问保护，Apache 的行为是要求请求者同时满足这两个控制。但假设你想混合基于主机和基于用户的保护，并只要其中一种方法足够就允许访问资源。你可以使用 `satisfy` 指令来实现。你可以将 `satisfy` 指令设置为 `All`（默认值）或 `Any`。当设置为 `All` 时，必须满足所有访问控制方法才能提供资源。如果 `satisfy` 设置为 `Any`，只要满足任何一个访问条件，就会提供资源。

这是另一个访问控制示例，再次使用了之前的 `server-status` 示例。这次，你结合了访问方法，使得来自 `gnulix` 域的所有用户都被允许访问，而域之外的用户在获得访问权限之前必须标识身份。可以通过以下方式实现：

```apache
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

还有更多方法可以保护你 Web 服务器上的内容，但这里讨论的方法应该足够让你入门，并且对于大多数情况可能绰绰有余。请参考 Apache 的在线文档获取更多关于如何保护网站区域的示例。

## Apache 模块

核心部分的作用较少；Apache 的功能通过模块实现。每个模块通过添加必要的特性来解决定义良好的问题。通过添加或删除模块来提供你 Apache 所需的功能，你可以定制 Apache 服务器以满足你的需求。

基础 Apache 服务器包含了近 50 个核心模块。其他开发者还提供了更多模块。Apache 注册表（Apache Registry）是 Apache 附加模块的存储库，可以在 `http://modules.apache.org/`。模块目录（你的列表可能不同）：

| mod_access.so | mod_cdn_meta.so | mod_log_config.so | mod_setenvif.so |

| mod_actions.so | mod_cgi.so | mod_mime_magic.so | mod_spelling.so |

| mod_alias.so | mod_dav_fs.so | mod_mime.so | mod_ssl.so |

| mod_asis.so | mod_dav.so | mod_negotiation.so | mod_status.so |

| mod_auth_anon.so | mod_dir.so | mod_perl.so | mod_suexec.so |

| mod_auth_dbm.so | mod_env.so | mod_proxy_connect.so | mod_unique_id.so |

| mod_auth_digest.so | mod_expires.so | mod_proxy_ftp.so | mod_userdir.so |

| mod_auth_mysql.so | mod_headers.so | mod_proxy_http.so | mod_usertrack.so |

| mod_auth_pgsql.so | mod_imap.so | mod_proxy.so | mod_vhost_alias.so |

| mod_auth.so | mod_include.so | mod_python.so | mod_autoindex.so | mod_info.so | mod_rewrite.so |

每个模块都添加了可以在配置文件中使用的新指令。正如你所猜的，有许多额外的命令、开关和选项来描述所有内容。接下来的章节将简要描述 Ubuntu 的 Apache 安装中提供的这些模块子集。

### mod_access

`mod_access` 根据 IP 地址、主机名或环境变量控制对你 Web 服务器上某些区域的访问。例如，你可能希望允许来自你自己域的任何人访问网站的某些区域。更多信息请参阅“文件认证与访问控制”章节。

### mod_alias

`mod_alias` 处理传入的 HTTP 请求的 URL，例如将客户端请求重定向到另一个 URL。它还可以将文件系统的部分映射到你的 Web 层次结构中。例如，

`Alias /images/ /home/wsb/graphics/`

对于任何以 `/images/` 开头的 URL，都会从 `/home/wsb/graphics/` 目录获取内容。这是在客户端不知情的情况下完成的。如果你进行重定向，客户端将被指示去另一个 URL 寻找请求的内容。更高级的 URL 处理可以通过 `mod_rewrite` 完成。

### mod_asis

`mod_asis` 用于精细地指定包含在响应中的所有信息。这完全绕过了 Apache 可能会向响应中添加的任何标头。所有带有 `.asis` 扩展的文件在不进行任何更改的情况下发送给客户端。

作为一个 `mod_asis` 使用的简短示例，假设你已经将网站上的内容从一个位置移动到另一个位置。现在你通知尝试访问此资源的人它已移动，并自动将他们重定向到新位置。为了提供这些信息和重定向，你可以向带有 `.asis` 扩展的文件添加以下代码：

```
Status: 301 No old stuff!
Location: http://gnulix.org/newstuff/
```

第 17 章 Apache Web 服务器管理

Content-type: text/html
