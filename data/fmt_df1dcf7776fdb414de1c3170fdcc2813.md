
在 Basic Authentication 下，Apache 要求用户提供用户名和密码来访问受保护的资源。然后 Apache 验证用户是否被允许访问相关资源。如果用户名可接受，Apache 会验证密码。如果密码也通过检查，用户将被授权，Apache 将提供请求。

HTTP 是一种无状态协议；发送到服务器的每个请求和每个响应都是单独处理的，而不是以智能的方式处理。因此，身份验证信息必须随每个请求一起包含。这意味着对受密码保护区域的每个请求都更大，因此会稍慢一些。为了避免不必要的系统使用和延迟，仅保护绝对需要保护的网站区域。

要使用 Basic Authentication，你需要一个列出哪些用户被允许访问资源的文件。该文件由包含名称和密码对的纯文本列表组成。它看起来非常像你的 Linux 系统的 `/etc/passwd` 用户文件。

### CAUTION

不要使用 `/etc/passwd` 作为身份验证的用户列表。当你使用 Basic Authentication 时，密码和用户名以 base64 编码文本的形式从客户端发送到服务器——这与纯文本一样可读。用户名和密码包含在发送到服务器的每个请求中。因此，任何可能在网络流量中窃听的人都能够获取这些信息！

要为 Apache 创建用户文件，请使用 `htpasswd` 命令。它包含在 Apache 软件包中。如果你使用软件包安装，它位于 `/usr/bin`。运行不带任何选项的 `htpasswd` 会产生以下输出：

```
Usage:
htpasswd [-cm dps] passwordfile username
htpasswd -b[cm dps] passwordfile username password

htpasswd -n[mdps] username
htpasswd -nb[mdps] username password
```

- `-c` 创建新文件。
- `-n` 不更新文件；将结果显示在 stdout。
- `-m` 强制使用 MD5 加密密码。
- `-d` 强制使用 CRYPT 加密密码（默认）。
- `-p` 不加密密码（明文）。
- `-s` 强制使用 SHA 加密密码。
- `-b` 使用命令行上的密码而不是提示输入。
- `-D` 删除指定的用户。

在 Windows、TPF 和 Netware 系统上，默认使用 `'-m'` 标志。

在所有其他系统上，`'-p'` 标志可能无法工作。

正如你所见，这是一个非常难以使用的命令。例如，要创建一个名为 `gnulixusers` 的新用户文件，并添加一个名为 `wsb` 的用户，你需要执行类似以下操作：

```
sudo htpasswd -c gnulixusers wsb
```

然后你将被提示为该用户输入密码。要添加更多用户，你将重复相同的过程，只是省略 `-c` 标志。

你也可以创建用户组文件。这些文件的格式与 `/etc/groups` 类似。在每一行中，输入组名，后跟冒号，然后列出所有用户，每个用户之间用空格分隔。例如，用户组文件中的条目可能如下所示：

```
gnulixusers: wsb pgj jp ajje nadia rkr hak
```

现在你已经知道如何创建用户文件，是时候看看 Apache 如何使用它来保护 Web 资源了。

要将 Apache 指向用户文件，请使用 `AuthUserFile` 指令。`AuthUserFile` 以用户文件的路径作为参数。如果文件路径不是绝对路径——即以 `/` 开头——则假定该路径相对于 `ServerRoot`。使用 `AuthGroupFile` 指令，你可以以相同的方式指定一个组文件。

接下来，使用 `AuthType` 指令设置对此资源使用的身份验证类型。在这里，类型设置为 Basic。

现在你需要决定资源将属于哪个 realm。Realm 用于将不同的资源分组，这些资源将共享相同的用户进行授权。Realm 可以是几乎任何字符串。Realm 会显示在用户 Web 浏览器的授权对话框中。因此，你应该将 realm 字符串设置为具有信息性的内容。Realm 由 `AuthName` 指令定义。

最后，声明哪种类型的用户有权使用该资源。你可以用 `Require` 指令来做到这一点。该指令的三种使用方式如下：

- 如果你将 `valid-user` 指定为选项，则用户文件中的任何用户都可以访问该资源（即，前提是她也输入了正确的密码）。
- 你可以用 `users` 选项指定允许访问的用户列表。
- 你可以用 `group` 选项指定一组组列表。组列表以及用户列表中的条目以空格分隔。

回到你之前看到的 `server-status` 示例，而不是让用户基于主机名访问 `server-status` 资源，你可以要求用户通过身份验证后才能访问该资源。你可以在配置文件中通过以下条目来实现：

```
<Location /server-status>
SetHandler server-status
AuthType Basic
AuthName 'Server status'
AuthUserFile "gnulinuxusers"
Require valid-user
</Location>
```

### 关于访问控制的最后说明

如果资源同时具有基于主机的访问保护和基于用户的访问保护，Apache 的默认行为是要求请求者同时满足这两种控制。但假设你想混合基于主机和基于用户的保护，并允许在任一方法成功时访问资源。你可以这样做，使用 `satisfy` 指令。你可以将 `satisfy` 指令设置为 `All`（这是默认值）或 `Any`。当设置为 `All` 时，所有访问控制方法都必须得到满足后才会提供资源。如果 `satisfy` 设置为 `Any`，只要满足任何访问条件，资源就会被提供。

下面是另一个访问控制示例，同样使用之前的 `server-status` 示例。这次，你组合访问方法，以便 `gnulix.org` 域的所有用户都被允许访问，而域外的用户必须先识别自己才能获得访问权限。你可以这样做：

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

有更多方法可以保护 Web 服务器上的内容，但这里讨论的方法应该足以让你入门，并且对于大多数情况来说可能已经足够了。请查阅 Apache 的在线文档，了解更多有关如何保护站点区域的示例。

## Apache 模块

Apache 核心功能相对较少；Apache 的功能来自模块。每个模块通过添加必要功能来解决一个明确定义的问题。通过添加或删除模块以提供你希望 Apache 具备的功能，你可以定制 Apache 服务器以满足你的确切需求。

近 50 个核心模块包含在基本的 Apache 服务器中。还有更多模块可从其他开发者处获得。Apache Module Registry 是 Apache 附加模块的存储库，可在 `http://modules.apache.org/` 找到。模块存储在 `/usr/local/apache2/modules` 目录中（你的列表可能看起来不同）：

- `mod_access.so`
- `mod_actions.so`
- `mod_alias.so`
- `mod_asis.so`
- `mod_auth_anon.so`
- `mod_auth_dbm.so`
- `mod_auth_digest.so`
- `mod_auth_mysql.so`
- `mod_auth_pgsql.so`
- `mod_cern_meta.so`
- `mod_cgi.so`
- `mod_fs.so`
- `mod_dav.so`
- `mod_dir.so`
- `mod_env.so`
- `mod_expires.so`
- `mod_headers.so`
- `mod_imap.so`
- `mod_log_config.so`
- `mod_mime_magic.so`
- `mod_mime.so`
- `mod_negotiation.so`
- `mod_perl.so`
- `mod_proxy_connect.so`
- `mod_proxy_ftp.so`
- `mod_proxy_http.so`
- `mod_proxy.so`
- `mod_setenvif.so`
- `mod_speling.so`
- `mod_ssl.so`
- `mod_status.so`
- `mod_suexec.so`
- `mod_unique_id.so`
- `mod_userdir.so`
- `mod_usertrack.so`
- `mod_vhost_alias.so`
