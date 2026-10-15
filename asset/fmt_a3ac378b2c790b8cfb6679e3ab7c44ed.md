
LoadModule `autoindex_module` `modules/mod_autoindex.so`

LoadModule `dir_module` `modules/mod_dir.so`

LoadModule `cgi_module` `modules/mod_cgi.so`

LoadModule `asis_module` `modules/mod_asis.so`

LoadModule `imap_module` `modules/mod_imap.so`

LoadModule `action_module` `modules/mod_actions.so`

你可以通过将 `LoadModule` 指令夹在 `<IfDefine>` 和 `</IfDefine>` 标签之间来条件条件加载模块。

### AddModule
此指令告诉 Apache 加载模块，通常与 `LoadModule` 指令结合使用，如下片段所示：

```
AddModule mod_env.c

AddModule mod_log_config.c

AddModule mod_log_agent.c

AddModule mod_log_referrer.c

#AddModule mod_mime_magic.c

AddModule mod_mime.c

AddModule mod_negotiation.c

AddModule mod_status.c

AddModule mod_info.c

AddModule mod_include.c
```

### ClearModuleList
此指令从 Apache 中移除模块。你可以通过将 `LoadModule` 指令夹在 `<IfDefine>` 和 `</IfDefine>` 标签之间来条件加载模块。例如，下面的块检查 PHP 是否可用，如果为真则条件地添加 `mod_php.c`（php 衍生自个人主页工具，是 Apache 可用于访问数据库的系统）：

```
<IfModule mod_PHP>

Module mod_php.c

</IfDefine>
```

本节介绍了全局环境变量。接节将描述在 `http.conf` 中找到的主要配置选项。

## 配置主服务器

本节介绍了全局环境变量。接节将描述在 `http.conf` 中找到的主要配置选项。

### 引入 Apache 指令

以下列表：

- `Listen`: 设置 `httpd` 监听的端口。默认值为 `80`。
- `DocumentRoot`: 本质上是 Web 服务器提供文档的根目录。
- `FollowSymLinks`: 允许 Apache跟随 `DocumentRoot` 内的符号链接。
- `AllowOverride`: 允许访问文件（如 `.htaccess`）覆盖 `<Directory>` 块配置。选项有 `All`, `None`, `Indexes`, `Includes`, `FollowSymLinks`, `ExecCGI` 和 `MultiViews`；`All` 和 `None` 会阻止任何选项生效。
- `Order allow, deny`: 指定允许和禁止访问目录的顺序。顺序 `allow, deny` 配置顺序为先允许、后拒绝，且拒绝具有优先级。
- `Allow from all`: 允许从任何地方访问。`Allow` 指令可以允许来自主机和网络的访问。例如，设置 `Allow from 192.168.1.0/24` 允许来自该网络的访问。
- `AccessFileName`: 定义服务器用来提供辅助访问的文件名。之前定义的访问控制指令通过 `httpd.conf` 文件直接控制 Web 服务器。默认名为 `.htaccess`。你可以在 `DocumentRoot` 内放置任意数量的 `.htaccess` 文件，以控制所在目录及其子目录的访问。控制指令（如 `Allow` 和 `Order`）放置在 `.htaccess` 文件中。这些控制指令放在访问文件中功能与放在 `httpd.conf` 中的功能相同。
- `UserDir`: Apache 允许你从个人账户提供 Web 页面。例如，设置 `UserDir :public_html` 会强制 Apache 在用户目录路径后附加字符串 `"public_html"`。当 `some.webserver.com` 服务器接收到 URL `http://some.webserver.com/~lupe` 的请求时，它会指向 `/home/lupe/public_html` 目录。
- `ErrorLog`: Apache 执行错误日志。`ErrorLog` 指令设置错误日志名称和位置。默认错误日志为 `log/error_log`，位于 `/var/www/html/logs` 目录。
- `LogLevel`: Apache 提供多个级别的错误日志。这些级别与 Linux `syslog` 系统相同；默认值为 `warn`。
- `LogFormat`: 控制错误日志的格式。默认值为
- `AddLanguage`: 你可以配置 Apache 解释国家域名后缀，并为指定文件使用相应的语言。表 6-1 列出了可用语言及其后缀。

## APA 块指令、别名和图标

以下列表描述了 Apache 块指令：

- `<Directory ... </Directory>`: 你可以使用此块对 `DocumentRoot` 树内的每个目录限制访问、重定向到另一个位置并执行其他过程。通过在这些标签内使用适当的指令，可以控制对指定文件系统的访问。第一个 `<Directory>` 容器实际上设置了所有后续 `<Directory>` 容器的默认行为。

```apache
<Directory /var/www/html>
Options Indexes FollowSymLinks
AllowOverride None
Order allow, deny
Allow from all
</Directory>
```

`<Directory /var/www/html>` 标签指定容器控制从 `DocumentRoot` 的顶部开始。（回想一下 `DocumentRoot` 之前在 `httpd.conf` 文件中定义为 `/var/www/html`。此容器的控制从 `/var/www/html` 开始）。

- `Alias`（别名）： 映射别名并允许访问 `DocumentRoot` 之外的文件系统。此指令允许 Web 服务器提供通常无法访问的对象，例如图标图像。默认是将图标映射到 `/var/www/icons`，如下：

```apache
Alias /icons/ "/var/www/icons/*
```

访问已别名的目录（例如图标）：

```apache
<Directory /var/www/icons>
Options Indexes MultiViews
AllowOverride None
Order allow, deny
Allow from all
</Directory>
```

- `ScriptAlias`（脚本别名）：对本地文件系统的访问通常限制在 `DocumentRoot` 指定的目录。然而，Web 服务器必须能够访问该空间外的某些文件。别名是文件的一种示例。`ScriptAlias` 将一个目录映射到另一个目录，允许服务器访问包含可执行服务器脚本的目录。默认是将 `cgi-bin` 映射到 `/var/www/cgi-bin`，如下：

```apache
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/*"
```

```apache
<Directory "var/www/cgi-bin">
AllowOverride None
Options None
Order allow,deny
Allow from all
</Directory>
```
