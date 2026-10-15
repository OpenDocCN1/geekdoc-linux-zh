
`</Directory>`

内部指令的作用范围仅限于指定的目录（及其子目录）；不过，你只能使用在目录上下文中允许的指令（你将在下一章中详细了解这些指令）。

在这里，`Options` 和 `AllowOverride` 指令适用于 `%DocumentRoot%`，即根目录（`/`）或主 Web 站点的顶层目录。由于包裹在目录容器内的指令适用于指定目录下的所有子目录，因此这些指令适用于 `%DocumentRoot%` 内的所有目录。

`Options` 指令被设置为 `FollowSymLinks`，这指示 Apache 允许自己遍历 `%DocumentRoot%` 内的任何符号链接。因为 `Options` 指令仅设置为跟随符号链接，所以 `%DocumentRoot%` 内的任何目录都不提供其他选项。实际上，`Options` 指令等效于：

```apache
Options FollowSymLinks -ExecCGI -Includes -Indexes -MultiViews
```

其他选项将在下一章的 `Options` 指令部分中解释。不过，请确保这里的核心思想是创建一个非常封闭的服务器。由于只允许遍历符号链接，因此必须根据需要按目录显式启用其他选项。从安全角度来看，这是一件非常好的事情。下一个目录容器开放了 `%DocumentRoot%` 目录，如下所示：

```apache
<Directory "/usr/local/apache/htdocs">
Options Indexes FollowSymLinks MultiViews
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

如果你的 `%DocumentRoot%` 不同，请更改指定的目录路径。以下是上述配置对 Apache 的含义：

-   指定目录及其子目录可以被索引。如果存在索引文件，将显示该文件；如果不存在索引文件，服务器将为此目录创建一个动态索引。这是由 `Options` 指令指定的。
-   指定目录及其所有子目录可以拥有服务器可以跟随（即作为路径使用）的符号链接，以访问信息。这也是由 `Options` 指令指定的。
-   指定目录及其所有子目录可以成为内容协商的一部分。`Options` 指令的 `MultiViews` 选项设置了这一点。我并不是这个选项的拥趸，但也不至于将其移除。例如，当在 `%DocumentRoot%` 目录中启用了上述显示的 `Options` 指令时，对 `http://www.domain.com/ratecard.html` 的请求可以由名为 `ratecard.html.bak`、`ratecard.bak`、`ratecard.old` 等文件响应，如果在缺少 `ratecard.html` 的情况下。这可能并非总是令人期望的行为。

此处未指定任何选项可以被本地访问控制文件（由 `httpd.conf` 中的 `AccessFileName` 指令指定；默认值为 `.htaccess`）覆盖。这是通过 `AllowOverride` 指令指定的。

`Allow` 指令在 `Deny` 指令之前进行评估。默认情况下拒绝访问。任何不匹配 `Allow` 指令或匹配 `Deny` 指令的客户端都将被拒绝访问服务器。

允许所有访问。

默认设置应该足以满足需求。

> **注意**
>
> 如果你的服务器将连接到 Internet，你可能希望从 `Options` 指令行中移除 `FollowSymLinks` 选项。保留此选项会带来潜在的安全风险。例如，如果你的 Web 站点中的某个目录没有索引页面，服务器将显示一个自动索引，其中可能包含该目录中你拥有的任何符号链接。这可能会导致敏感信息被显示，甚至可能允许任何人运行位于粗心链接的目录中的可执行文件。

## UserDir

`UserDir` 指令告诉 Apache 将 `%UserDir%` 视为每个用户 Web 站点的文档根目录（`/username/%UserDir%`）。这只有在系统中有多个用户并且希望允许每个用户拥有自己的 Web 目录时才有意义。默认设置为：

```apache
UserDir public_html
```

这意味着，如果你将 Web 服务器名称设置为 `www.yourcompany.com`，并且你有两个用户（`joe` 和 `jenny`），他们的个人 Web 站点 URL 将是：

-   `http://www.yourcompany.com/~joe` 物理目录：`~joe/public_html`
-   `http://www.yourcompany.com/~jenny` 物理目录：`~jenny/public_html`

请注意，在 Unix 系统上，`~`（波浪号）扩展为用户的主目录。`UserDir` 指令指定的目录位于每个用户的主目录中，Apache 必须具有读取和执行权限才能读取 `public_html` 目录内的文件和目录。这可以通过在 Unix 系统上使用以下命令来实现：

```bash
chown -R <user>:<Apache server's group name> ~/<user>/<directory assigned in UserDir>
chmod -R 2770 ~/<user>/<directory assigned in UserDir>
```

例如，如果用户名是 `joe`，Apache 的组名为 `httpd`，并且 `UserDir` 指令中分配了 `public_html`，则前面的命令将如下所示：

```bash
chown -R joe:httpd ~/joe/public_html
chmod -R 2770 ~/joe/public_html
```

第一个命令 `chown` 更改了 `~/joe/public_html` 目录（以及其中所有文件和子目录）的所有权为 `joe:httpd`。换句话说，它授予用户 `joe` 和组 `httpd` 对 `public_html` 目录中所有文件和目录的完整所有权。下一个命令 `chmod` 将访问权限设置为 `2770`—换句话说，只有用户（`joe`）和组（`httpd`）在 `public_html` 及其下的所有文件和子目录中具有完整的读、写和执行权限。它还确保当在 `public_html` 目录中创建新文件或子目录时，新创建的文件设置了组 ID。这使得 Web 服务器能够在无需用户干预的情况下访问新文件。

> 如果你使用脚本（如 Linux 系统上的 `/usr/sbin/adduser` 脚本）在系统上创建用户账户，你可能希望将 Web 站点创建过程整合到该脚本中。只需添加一个 `mkdir` 命令来创建默认的 `public_html` 目录（如果这是你分配给 `UserDir` 指令的目录）以创建 Web 目录。添加 `chmod` 和 `chown` 命令以授予 Web 服务器用户读取和执行此 `public` 目录下文件和目录的权限。

## DirectoryIndex

接下来，你需要配置 `DirectoryIndex` 指令，其语法如下：

```apache
DirectoryIndex [ filename1, filename2, filename3, ... ]
```

该指令指定 Apache 服务器应将哪个文件视为被请求目录的索引。例如，当请求诸如 `www.yourcompany.com/` 这样的 URL 时，Apache 服务器确定这是对 Web 站点的 `/`（文档根目录）目录的访问请求。如果 `DocumentRoot` 指令设置为：

```apache
DocumentRoot "/www/www.yourcompany.com/public/htdocs"
```

### DirectoryIndex 配置

当请求一个目录时，Apache 服务器会查找名为 `/www/www.yourcompany.com/public/htdocs/index.html` 的文件；如果找到该文件，Apache 会通过将该文件的内容返回给请求的 Web 浏览器来处理此请求。然而，如果将 `DirectoryIndex` 指定为 `welcome.html` 而不是默认的 `index.html`，Web 服务器将改为查找 `/www/www.yourcompany.com/public/htdocs/welcome.html`。如果该文件不存在，Apache 将通过创建一个动态 HTML 页面来返回目录列表。图 3-3 展示了当目录中缺少 `index.html` 时，服务器为请求的浏览器生成目录列表时的情况。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_76_0.png)

**图 3-3：** 在缺失 `index.html` 时的动态目录列表

你可以在 `DirectoryIndex` 指令中指定多个索引文件名。例如：

```
DirectoryIndex index.html index.htm welcome.htm
```
