
`/etc/httpd`

`/usr/sbin/httpd`

`/etc/httpd`

`/usr/share/man8`

这表明 `httpd` 守护进程位于 `/etc`，帮助页位于 `/usr/share/man8`。如果你看到这样的，说明你的软件已安装，只需要启动。Apache Web 服务器是下一节的基础。

# 获取和安装软件

Apache 的最新版本是 1.34，你可以从 Apache 网站 `www.apache.org` 获取。你也可以从那里获取源码或二进制文件。

# 配置文件

如果你查看 `/etc/httpd/conf`，你可以看到主配置文件 `httpd.conf`。在 Apache 的早期版本中有三个配置文件：`httpd.conf`、`ssl_conf` 和 `access.conf`。

在 1.34 版本中只有 `httpd.conf`，这是你唯一需要关注的文件。`/etc/httpd/conf` 目录包含两个文件：`magic` 文件和 `mime.types` 文件。

这两个文件都指定了不同扩展名的 MIME 类型。

最后，以 `-dist` 结尾的文件是由 Apache 组织分发的示例配置文件。可以通过删除 `-dist` 文件夹来使用这些文件。

位于 `/etc/httpd` 的是 `logs` 和 `modules` 文件夹。这两个分别是 `/var/log/httpd` 和 `/usr/lib/apache` 的符号链接。记住，根据你的发行版，这些文件位置可能不同。

远程用户可以访问的目录位于 `/home/httpd/html`。这是服务器访问系统时的默认目录。`home/httpd` 中还有 `cgi-bin` 和 `icon` 目录。远程用户可以通过服务器调用这些目录。

# 配置指令

`/etc/httpd/conf/httpd.conf` 文件如图 26-2 所示，包含许多为 Web 服务器运行提供指令的章节。这些章节包含配置选项，称为指令，有近 200 个。我们通过分解默认 `httpd.conf` 文件并查看默认设置来研究一些常用的指令。要获取所有指令及其使用的完整列表，请参考位于 `/home/http/html/manual/` 的 Apache 手册。

该部分的第一部分 *Modules* 详细介绍了服务器启动 `httpd` 守护进程时将加载的模块。你必须加载相应的模块才能激活。Apache 手册包含了对模块及其使用的完整描述。

## 第 26 章 ♦ 配置 Web 服务器 449

紧接 `httpd.conf` 文件中的 DSO 部分之后是命名空间（Name Space）和服务器设置部分。该部分中的指令会影响命名空间用户看到的内容显示方式，以及请求如何被处理和格式化以显示。

命名空间指令如表 26-1 所示，每个指令都带有描述和用法示例。

| 指令 | 功能 | 示例 |
|---|---|---|
| DocumentRoot |呈现给用户的文件的默认目录位置。 | DocumentRoot /home/httpd |
| UserDir | 当接收到用户请求时，附加用户主目录的目录名称。 | UserDir public_html |
| DirectoryIndex | 网站进行 HTML 请求时使用的文件。 | 命名为 index.htm, index.html 的文件 |
| FancyIndexing | 指明是否应该使用花式（fancy）或标准的索引切换。 | FancyIndexing on/off |
| AddIcons | 服务器为每种文件类型显示哪个图标。 | AddIconByType (TXT,icons/text.gif) text/* |
| DefaultIcon | 为没有显式设置图标的文件设置图标。 | DefaultIcon /icons/unknown.gif |
| ReadName | 默认的 readme 文件。 | ReadName readme |
| HeaderName | 应附加在目录索引之前的文件名。 | HeaderName header |
| IndexIgnore | 目录索引应忽略的文件名。 | IndexIgnore filename1 filename2 |
| AccessFileName | 每个目录中提供访问控制信息的文件。 | AccessFileName .htaccess |
| TypesConfig | 指定 mime.types 文件的位置。 | TypesConfig /etc/httpd/conf/mime.types |

## 表 26-1（续）

| 指令 | 功能 | 示例 |
|---|---|---|
| DefaultType | 为未列出文件类型的文档指定默认 MIME 类型。 | DefaultType text/plain |
| AddEncoding | 如果浏览器支持，浏览器可以在接收信息时解压缩信息。 | AddEncoding -x gz |
| AddLanguage | 指定文档的默认语言。 | AddLanguage en.. |
| LanguagePriority | 设置显示语言的优先级，按优先级递减列出语言。 | LanguagePriority en it |
| Redirect | 告诉用户在哪里找到移动后的文档。 | Redirect different url |
| Alias | 列出指向其他项的指针。 | /icons /home/httpd/icons |
| ScriptAlias | 指定包含服务器脚本的目录。 | ScriptAlias filename realtime |
| AddType | 允许在不编辑文件的情况下更改 mime.types。 | AddType type/subtype |
| AddHandler | 允许将某些文件扩展名映射到处理器。 | AddHandler send-as-is |
| Action | 当找到匹配的文件时通过定义的媒体类型执行脚本。消除了频繁使用的 cgi 文件重复使用 url 路径的需求。 | Action media/type / cgi-script/location |
| MetaDir | 指定元信息文件所在的目录。 | MetaDir .Web |
| MetaSuffix | 指定包含元信息的文件的文件名后缀。 | MetaSuffix .meta |
| ErrorDocument | 允许指定处理错误的例程。返回一个字符串作为 ErrorDocument 的值，或可以将错误重定向到静态页面或 cgi 脚本。下所示示例。 | | |
| ErrorDocument 401 | 将用户重定向到订阅服务的本地 URL。 | | |

## 第 26 章 ✦ 配置 Web 服务器 451

| 指令 | 功能 | 示例 |
|---|---|---|
| ErrorDocument 403 | 显示指定的消息。 | | |
| ErrorDocument 404 | 重定向到本地静态页面（ErrorDocument 404 /whatever.html）或 cgi 脚本（ErrorDocument 404 / cgi-bin/whatever.pl）。 | | |
| ErrorDocument 500 | 不向用户显示消息的内部服务器错误。 | | |
| MimeMagicFile | 使用指定的文件，服务器可以获取文件类型的提示。 | MimMagicFile /etc/httpd/config |
| BrowserMatch | 禁用持久连接（keepalives）和 HTTP 标头刷新。也可以对不支持标准的浏览器禁用 HTTP/1.1 响应。用于旧版浏览器，如 Netscape 2.x 和 Internet Explorer 4.0。 | BrowserMatch "Mozilla/2" nokeepalive |
| BrowserMatch "MSIE4,0b"; | nokeepalive downgrade-1.0 force-response-1.0 | | |

`httpd.conf` 文件的下一部分称为“全局访问配置”（Global Access Configuration）。该部分指定了服务器可以访问的目录，以及在指定目录中启用或禁用的服务。

你可以在 `<Directory>` 和 `</Directory>` 标签内放置一个或多个指令。这些指令仅适用于指定的目录及其子目录。可以使用任何在目录上下文中允许的指令。在通配符字符串中，`*` 匹配任何单个字符，`#` 匹配字符序列。你还可以在 shell 中使用字符范围。例如：

```
<Directory /home>

Options Indexes FollowSymLinks

AllowOverride none

</Directory>
```

图 26-3 显示了 `httpd.conf` 的全局访问配置部分。可以看到，该部分包含各种指令。

452 部分 IV 配置和管理 TCP/IP 网络

```
# 全局访问配置

# 此部分指定了服务器可以访问的目录以及在指定目录中

#启用或禁用的服务。你可以在 <Directory> 和 </Directory>

# 标签内放置一个或多个指令。这些指令仅适用于指定的目录
```
